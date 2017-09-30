
# Payload: HID covert channel backdoor (Pi Zero W only)

### Video demo
[![P4wnP1 HID demo youtube](https://img.youtube.com/vi/Pft7voW5ui8/0.jpg)](https://www.youtube.com/watch?v=Pft7voW5ui8)

The video is produced by @Seytonic, you should check out his youtube channel with hacking related tutorials and various projects, if you're interested in more stuff like this (link in credits).

**@Seytonic** thanks for the great tutorial

### HID backdoor features
- Payload to bridge an Airgap target, by relaying a shell over raw HID and provide it from P4wnP1 via WiFi
- Plug and Play install of HID device on Windows (tested on Windows 7 and Windows 10)
- Covert channel based on raw HID
- Pure **in memory, multi stage payload** - nothing is written to disk, small footprint (compared to typical PowerShell IOCs)
- RAT like control server with custom shell:
    - Auto completition for core commands
	- Send keystrokes on demand
	- Excute DuckyScripts (menu driven)
	- Trigger remote backdoor to bring up HID covert channel
	- creation of **multiple** remote processes (only with covert channel connection)
	- console interaction with managed remote processes (only with covert channel connection)
	- auto kill of remote payload on disconnect
	- `shell` command to  create remote shell (only with covert channel connection)
	- server could be accessed with SSH via WiFi when the `hid_backdoor.txt` payload is running

# HID backdoor attack chain and usage

### 1. Preparation

- Choose the `hid_backdoor.txt` payload in `setup.cfg` (using the interactive USB OTG mode or one of the payloads with SSH network access, like `network_only.txt`)
- Attach P4wnp1 to the target host (Windows 7 to 10)

### 2. Access the P4wnP1 backdoor shell

- During boot up, P4wnP1 opens a wireless network called `P4wnP1` (password: `MaMe82-P4wnP1`)
- Connect to the network and SSH in with `pi@172.24.0.1`
- If everything went fine, you should be greeted by the interactive P4wnP1 backdoor shell (If not, it is likely that the target hasn't finished loading the USB keyboard drivers). The SSH password is the password of the user `pi`, which is `raspberry` in the default configuration.

### 3. Ad-Hoc keyboard attacks from P4wnP1 backdoor shell (without using the covert channel), could be done from here:

- Entering `help` shows available commands
- Use the `SetKeyboardLayout` to set the keyboard layout according to your targets language. **This step is important and should always be taken first, otherwise most keyboard based attacks fail.**
- to print the current keyboard layout use `GetKeyboardLayout`. The default keyboard language for the P4wnP1 backdoor shell could be changed in `hidtools/backdoor/config.txt`
- use the `SendKeys` command followed by an ASCII key sequence to send keystrokes to the target
- As you will notice, the `SendKeys` command is somehow restricted, no control keys could be sent, even a RETURN is problematic. So for more complex key sequences the `FireDuckyScript` command comes to help.
- `FireDuckyScript` accepts the name of a script residing in the `DuckyScript/` folder. The folder is prefilled with some demo scripts. If you omit the script name behind the `FireDuckyScript` command, you will be presented with a menue to choose a script. If you wonder why one would write a DuckyScript sending an `<ALT> + <F4>` only, you're thinking in the old world of RubberDucky. With P4wnP1 and its capbility to run DuckyScripts dynamically, such short scripts come in handy. If you don't know what I'm talking about run the `P4wnP1_youtube.duck` script and you'll know where scripts like `AltF4_Return.duck` are needed ;-)

### 4. Fire stage 1 of the covert channel payload ('FireStage1' command)
- As we are able to print characters to the target, we are able to remotly execute code. P4wnP1 uses this capability to type out a PowerShell script, which builds and executes the covert channel communication stack. This attack works in multiple steps:
    1. Keystrokes are injected to start a PowerShell session and type out stage 1 of the payload. Depending on how the command `FireStage1` is used, this happens in different flavours. By default a short stub is executed, which hides the command windows from the user, followed by the stage 1 main script.
	2. The stage 1 main script comes in two fashions:
       - Type 1: A pure PowerShell script which is short and thus fast, but uses the infamous IEX command (this command has the capability to make threat hunters and blue teamers happy). This is the default stage 1 payload.
       - Type 2: A dot NET assembly, which is loaded and executed via PowerShell. This stage 1 payload takes longer to execute, as more characters are needed. But, as you may already know, it doesn't use the IEX command.
- It is worth mentioning, that the PowerShell session is started without command line arguments, so there's nothing which triggers detection mechanisms for malicious command lines. Theres no parameter like `-exec bypass`, `-enc`, `-NoProfile` or `hidden` ... nothing suspicious! The shortcoming is, that we need to wait till the PowerShell window opens before typing is continued. As we are not able to detect for input readiness and there are boxes which take years to bring up an interactive PowerShell window, the delay between running `powershell.exe` and starting of stage1 typeout could be changed with the second parameter to the `FireStage1` command (default is 1000 milliseconds).
- Last but not least, if you append `nohide` to the end of the `FireStage1` command line, the Window hiding stub isn't executed in upfront and you should be able to see all my sh**ty debug output.

### 5. Loading stage 2
- There's no rocket sience here. The stage 1 payload initializes the basic interface to the custom HID device and receives stage 2 **fully automated**. Stage 2 includes all the protocol layers and the final backdoor. It gets directly loaded into memory as dot NET assembly.
- So why dot NET ? The early versions of the backdoor have been fully developed in PowerShell. This resulted in a big mess when it comes to multi threading, PS 2.0 compatability without class inheritance and multi thread debugging with ISE. I don't want to say that is impossible (if you watched the commit history, there's the proof that it is possible), but there's no benefit. To be precise, there are disadvantages: Much more code is needed to achieve the same, the code is slower and **PowerShell Module Logging would be able to catch every single script command from the payload**. In contrast to using a dot NET assembly, where the only PowerShell commands which could get logged, are the ones which load the assembly and run the stage 2 trigger. Everything else is gone as soon as the payload quits. So ... small footprint, yeah.
- But don't get "PowerShell inline assemlies" compiled to a temporary file on disc ?!?! Yes, they do! At least if they're written with CSharp inline code. Luckily P4wnP1 doesn't do this. The assemblies are shipped pre-compiled.

### 6. Using the backdoor connection
- After stage 2 has successfully ran, the prompt of the P4wnP1 backdoor shell should indicate a client connection.
- From here on, P4wnP1 shell commands are usable run `help`.

### HID backdoor attack - summary

1. Choose `hid_backdoor.txt` payload
2. Connect P4wnP1 device to Windows target
3. Connect to the newly spawned `P4wnP1` WiFi with a different device (could be a smartphone, as long as a SSH client is installed)
4. Set the correct target keyboard layout with `SetKeyboardLayout` (or alter `hidtools/backdoor/config.txt`)
5. On the P4wnP1 shell run `SendKeys` or `FireDuckyScript` to inject key strokes
6. To fire up the covert channel HID backdoor, issue the command `FireStage1`
7. After the target connected back, enter `shell` to create a remote shell through the covert channel

**Detailed explanation of every command can be found in [Backdoor Commands](Payload-Subfolder/Backdoor-Payload/Backdoor-Commands.md)**

# Currently missing features

- Run TCP sockets through the HID channel. Yes, it would be really nice to have a SOCKS4a or SOCKS5 listening on P4wnP1, tunneling comms through the target client. I'm not sure when this will get done, as this PoC project consumed far too much time. But hey, the underlying communication layers are prepared to handle multiple channels and as far as I know, you're staring at the source code, right now!
