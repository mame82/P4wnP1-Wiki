# Commands

### KillProc
	Try to kill the given remote process

### KillClient
	Try to kill the remote client

### CreateProc
	This remote Powershell method calls "core_create_proc" in order to create a 
	remote process
	The response is handled by "handler_client_core_create_proc()"

### GetClientProcs
	Print a list of processes managed by the remote client

### shell
	Start a shell inside the target computer

### SendKeys
	Prints out everything on target through HID keyboard. Be sure
	to set the correct keyboard language for your target  (use 
	'GetKeyboardLanguage' and 'SetKeyboardLanguage' commands.).

### FireStage1
	usage: FireStage1 <trigger_type> <trigger_delay in milliseconds> [nohide] [uac]
	
	Fires stage 1 via HID keyboard against a PowerShell process
	on a Windows client.
	The code downloads stage 2 and after successful execution 
	commands like "shell" could be used, to get a remote shell 
	(communicating through HID covert channel only).
	
	THE KEYBOARD LANGUAGE HAS TO BE SET ACCORDING TO THE TARGETS 
	KEYBOARD LAYOUT, TO MAKE THIS WORK (use 'GetKeyboardLanguage' 
	and 'SetKeyboardLanguage' commands.)
	
	
	trigger_type = 1 (default):
	  Is faster, because less keys have to be printed out. As the
	  PowerShell script isn't capable of reading serial and 
	  manufacturer of a USB HID composite device, PID  and VID have 
	  to be perpended in front of the payload. This leaves a larger 
	  footprint.
	  
	trigger_type = 2:
	  Is slower, because around 6000 chars have to be printed to 
	  build the needed assembly. There's no need to account on PID 
	  and VID, as the code is using the device serial "deadbeef
	  deadbeef" and the manufacturer "MaMe82". These are hardcoded
	  in the assembly, and leave a smaller footprint (not ad-hoc 
	  readable, if powershell script content is logged).
	  
	trigger_delay (default 1000):
	  The payload is started by running powershell.exe and directly
	  entering the script with HID keyboard.
	  This part is critical, as if keystrokes get lost the initial
	  stage won't execute. This could be caused by user interaction
	  during stage 1 typeout or due to PowerShell.exe starting too
	  slow and thus getting ready for keyboard input too late. 
	  The latter case could be handled by increasing the trigger delay,
	  to give the target host more time between start of powershell
	  nd start of typing out stage1.
	  The value defaults to 1000 ms if omitted.
	  
	nohide
	  If "nohide" is added, the setup hiding the powershell window on
	  the target is omitted
	  
	uac
	  If "uac" is added P4wnP1 tries to run an elevated PowerShell
	  session homing the payload.
	  
	  Caution: The target user has to be member of the "Local
	  Administrators" group, otherwise this would fail.
	  The option is disabled by default.
	  
### GetKeyboardLanguage
	Shows which language is set for HID keyboard.

### interact
	Interact with processes on the target
	Usage: Interact <process ID>

	use GetClientProcs for target process IDs

### exit
	Exit the Backdoor payload to the pi's command-line

### state
	See details about the target computer
		
### echotest
	If the client is connected, command arguments given should be reflected back.
	Communications happen through a pure HID covert channel.

### SendDuckyScript
	Deploys a pre-compiled Ducky script saved in P4wnP1/duckyscrips/

### lcd
	Change directory on the Pi

### lpwd
	Print the name of the Pi's current directory

### lls
	Print the contents of the Pi's current directory

### pwd
	Print the target's current directory

### ls
	List contents of the target's current directory

### cd
	Change the target's current directory


### upload
	Upload a file from the Pi to the target
	Usage: upload <Pi/directory.filetype> <target/directory.filetype>
		
### download
	Download a file from the Pi to the target
	Usage: download <target/directory.filetype> <Pi/directory.filetype>

### run_method
	undocumented for now