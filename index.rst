--------------

*DISCLAIMER*

Most of the information here has been taken directly from the P4wnP1
Githib page. In the near future, I will go through every page and make
the formatting and wording similar throughout the wiki as well as try to
make it a bit easier to understand (for the not-so-advanced users).

| *This wiki is a HUGE work in progress just like the P4wnP1 project
  itself. The info here comes from FAQ.md, README.md, and many issues in
  the original project. Keep in mind this block of text won't be here
  forever (hopefully).*
| \*\*\*

About P4wnP1
============

Introduction
~~~~~~~~~~~~

P4wnP1 is a highly customizable USB attack platform, based on a low cost
Raspberry Pi Zero or Raspberry Pi Zero W. Since the initial release in
February 2017, P4wnP1 has come along way. A lot of the time has been
spent troubleshooting new features and bugs in the old.

P4wnP1 Features
~~~~~~~~~~~~~~~

-  **HID covert channel [[Frontdoor\|Frontdoor
   Payload]]/[[Backdoor\|Backdoor Payload]]** \| Get remote shell access
   to Windows targets via HID devices)
-  **[[Windows 10 Lockpicker\|Windows 10 Lockpicker]]** \| Unlock
   Windows boxes with weak passwords (fully automated)
-  **[[Stealing Browser Credentials\|Stealing Browser Credentials]]** \|
   Dumps stored Browser Credentials and copys them to the builtin
   flashdrive
-  **[[WiFi Hotspot\|Wifi Hotspot]]** \| SSH access (Pi Zero W only),
   supports hidden ESSID
-  **[[Client Mode\|Wifi Client]]** \| Relays USB net attacks over WiFi
   with internet access (MitM)
-  **[[USB device\|Refrence??????????]]** \| Works with Windows Plug and
   Play support

   -  Device Types:
   -  **HID covert channel communication device** \|
      [[Frontdoor\|Frontdoor Payload]]/[[Backdoor\|Backdoor Payload]]
   -  **[[HID Keyboard/Mouse\|Advanced Features#Advanced HID
      Features]]**
   -  **[[USB Mass storage\|Advanced Features]]** \| Currently only in
      demo setup with 128 Megabyte drive
   -  **[[RNDIS\|Advanced Features#Advanced Network Features]]** \|
      Windows Networking
   -  **[[CDC ECM\|Advanced Features]]** \| MacOS / Linux Networking

-  **[[Bash based payload scripts\|Module development]]** \| See
   ``payloads/`` subfolder for examples example
-  **[[Responder\|Windows-10-Lockpicker#attack-chain-short-summary]]**
-  **[[John the Ripper
   Jumbo\|Windows-10-Lockpicker#attack-chain-short-summary]]** \|
   Pre-compiled version ready to go
-  **[[AutoSSH integration\|AutoSSH]]** \| For easy reverse ssh tunnels
-  **[[Auto attack\|Refrence]]** \| P4wnP1 automatically boots to
   standard shell if an OTG adapter is attached
-  **[[LED state feedback\|Refrence]]** \| with a simple bash command
   (``led_blink``)
-  **[[Advanced Features\|Advanced Features]]**

Communication
~~~~~~~~~~~~~

|Diagramm|

Feature Comparison with BashBunny
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some days after initial P4wnP1 commit, Hak5's BashBunny was announced
(and ordered by myself). Here's a little feature comparison:

+----------+-------------+-----------------------------------------------------+
| Feature  | BashBunny   | P4wnP1                                              |
+==========+=============+=====================================================+
| RNDIS,   | supported,  | supported, usable in most combinations, Windows     |
| CDC ECM, | usable in   | Class driver support (Plug and Play) in all modes   |
| HID ,    | several     | as composite device                                 |
| serial   | combination |                                                     |
| and Mass | s,          |                                                     |
| storage  | Windows     |                                                     |
| support  | Class       |                                                     |
|          | driver      |                                                     |
|          | support     |                                                     |
|          | (Plug and   |                                                     |
|          | Play) in    |                                                     |
|          | most modes  |                                                     |
+----------+-------------+-----------------------------------------------------+
| Target   | no          | Raw HID device allows communication with Windows    |
| to       |             | Targets (PowerShell 2.0+ present) via raw HID       |
| device   |             | There's a full automated payload, allowing to       |
| communic |             | access P4wnP1 bash via a custom PowerShell console  |
| ation    |             | from target device (see 'hid\_frontdoor.txt'        |
| on       |             | payload). An additional payload based on this       |
| covert   |             | technique, allows to expose a backdoor session to   |
| HID      |             | P4wnP1 via HID covert channel and relaying it via   |
| channel  |             | WiFi/Bluetooth to any SSH capable device (bridging  |
|          |             | airgaps, payload 'hid\_backdoor.txt')               |
+----------+-------------+-----------------------------------------------------+
| **Mouse  | no          | Supported: relative Mouse positioning (most OS,     |
| emulatio |             | including Android) + ABSOLUTE mouse positioning     |
| n**      |             | (Windows); dedicated scripting language             |
|          |             | "MouseScript" to control the Mouse, MouseScripts    |
|          |             | on-demand from HID backdoor shell                   |
+----------+-------------+-----------------------------------------------------+
| Trigger  | No          | Hardware based: LEDs for CAPSLOCK/SCROLLLOCK and    |
| payloads |             | NUMLOCK are read back and used to branch or trigger |
| via      |             | payloads (see ``hid_keyboard2.txt`` payload)        |
| target   |             |                                                     |
| keyboard |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Interact | Not         | supported, HID backdoor could be used to fire       |
| ive      | supported   | scripts on-demand (via WiFi, Bluetooth or from      |
| DuckyScr |             | Internet using the HID remote backdoor)             |
| ipt      |             |                                                     |
| executio |             |                                                     |
| n        |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| USB      | supported   | will maybe be implemented                           |
| configur |             |                                                     |
| ation    |             |                                                     |
| changabl |             |                                                     |
| e        |             |                                                     |
| during   |             |                                                     |
| runtime  |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Support  | supported   | supported                                           |
| for      |             |                                                     |
| RubberDu |             |                                                     |
| cky      |             |                                                     |
| payloads |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Support  | no          | supported                                           |
| for      |             |                                                     |
| piping   |             |                                                     |
| command  |             |                                                     |
| output   |             |                                                     |
| to HID   |             |                                                     |
| keyboard |             |                                                     |
| out      |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Switchab | Hardware    | manually in interactive mode (Hardware switch could |
| le       | switch      | be soldered, script support is a low priority ToDo. |
| payloads |             | At least till somebody prints a housing for the Pi  |
|          |             | which has such a switch and PIN connectors)         |
+----------+-------------+-----------------------------------------------------+
| Interact | SSH /       | SSH / serial / stand-alone (USB OTG + HDMI)         |
| ive      | serial      |                                                     |
| Login    |             |                                                     |
| with     |             |                                                     |
| display  |             |                                                     |
| out      |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Performa | High        | Low performance single core ARM CPU, SDCARD         |
| nce      | performance |                                                     |
|          | ARM quad    |                                                     |
|          | core CPU,   |                                                     |
|          | SSD Flash   |                                                     |
+----------+-------------+-----------------------------------------------------+
| Network  | Windows     | Windows RNDIS: **20 GBit/s**\ Linux/MacOS ECM: **4  |
| interfac | RNDIS: **2  | GBit/s** (detected as 1 GBit/s interface on         |
| e        | GBit/s**\ L | MacOS)Real bitrate 450 MBit max (USB 2.0)\ `Here's  |
| bitrate  | inux/MacOS  | the needed P4wnP1                                   |
|          | ECM: **100  | patch <https://github.com/mame82/ratepatch>`__      |
|          | MBit/s**\ R |                                                     |
|          | eal         |                                                     |
|          | bitrate 450 |                                                     |
|          | MBit max    |                                                     |
|          | (USB 2.0)   |                                                     |
+----------+-------------+-----------------------------------------------------+
| LED      | RGB Led,    | mono color LED, driven by a single payload command  |
| indicato | driven by   |                                                     |
| r        | single      |                                                     |
|          | payload     |                                                     |
|          | command     |                                                     |
+----------+-------------+-----------------------------------------------------+
| Customiz | Debian      | Debian based OS with package manager                |
| ation    | based OS    |                                                     |
|          | with        |                                                     |
|          | package     |                                                     |
|          | manager     |                                                     |
+----------+-------------+-----------------------------------------------------+
| External | Not         | supported with Pi Zero W                            |
| network  | possible,   |                                                     |
| access   | no external |                                                     |
| via WLAN | interface   |                                                     |
| (relay   |             |                                                     |
| attacks, |             |                                                     |
| MitM     |             |                                                     |
| attacks, |             |                                                     |
| airgap   |             |                                                     |
| bridging |             |                                                     |
| )        |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| SSH      | not         | supported (Pi Zero W)                               |
| access   | possible    |                                                     |
| via      |             |                                                     |
| **Blueto |             |                                                     |
| oth**    |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Connect  | not         | supported (Pi Zero W)                               |
| to       | possible    |                                                     |
| existing |             |                                                     |
| WiFi     |             |                                                     |
| networks |             |                                                     |
| (headles |             |                                                     |
| s)       |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Shell    | not         | supported (WiFi client connection + SSH remote port |
| **access | possible    | forwarding to SSH server owned by the pentester via |
| via      |             | AutoSSH)                                            |
| Internet |             |                                                     |
| **       |             |                                                     |
+----------+-------------+-----------------------------------------------------+
| Ease of  | Easy,       | Medium, bash based event driven payloads, inline    |
| use      | change      | commands for HID (DuckyScript and ASCII keyboard    |
|          | payloads    | printing, as well as LED control)                   |
|          | based on    |                                                     |
|          | USB drive,  |                                                     |
|          | simple bash |                                                     |
|          | based       |                                                     |
|          | scripting   |                                                     |
|          | language    |                                                     |
+----------+-------------+-----------------------------------------------------+
| Availabl | Fast        | Slowly growing github repo (spare time one man show |
| e        | growing     | ;-)) Edit: Growing community, but no payload        |
| payloads | github repo | contributions so far                                |
|          | (big        |                                                     |
|          | community)  |                                                     |
+----------+-------------+-----------------------------------------------------+
| In one   | "World's    | A open source project for the pentesting and red    |
| sentence | most        | teaming community.                                  |
| ...      | advanced    |                                                     |
|          | USB attack  |                                                     |
|          | platform."  |                                                     |
+----------+-------------+-----------------------------------------------------+
| Total    | about 99    | about 5 USD (11 USD fow WLAN capability with Pi     |
| Costs of | USD         | Zero W)                                             |
| Ownershi |             |                                                     |
| p        |             |                                                     |
+----------+-------------+-----------------------------------------------------+

SumUp: BashBunny is directed to easy usage, but costs 20 times as much
as the basic P4wnP1 hardware. P4wnP1 is directed to a more advanced
user, but allows outbound communication on a separate network interface
(routing and MitM traffic to upstream internet, hardware backdoor etc.)

External Resources using P4wnP1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Dan The IOT Man, Introduction + Install instructions "P4wnP1 – The Pi
   Zero based USB attack-Platform": `Dan the IOT
   Man <https://dantheiotman.com/2017/09/15/p4wnp1-the-pi-zero-based-usb-attack-platform/>`__
-  Black Hat Sessions XV, workshop material "Weaponizing the Raspberry
   Pi Zero" (Workshop material + slides):
   `BHSXV <https://www.madison-gurkha.com/hands-onhacking-raspberrypi-en>`__
-  ihacklabs[dot]com, tutorial "Red Team Arsenal – Hardware :: P4wnp1
   Walkthrough" (Spanish): `part
   1 <https://www.ihacklabs.com/es/red-team-arsenal-hardware-p4wnp1-walkthrough-cargando-y-disparando-con-la-raspberry-pi-zero-w-parte-1/>`__,
   `part
   2 <https://www.ihacklabs.com/es/red-team-arsenal-hardware-p4wnp1-walkthrough-cargando-y-disparando-con-la-raspberry-pi-zero-w-parte-2/>`__,
   `part
   3 <https://www.ihacklabs.com/es/red-team-arsenal-hardware-p4wnp1-walkthrough-cargando-y-disparando-con-la-raspberry-pi-zero-w-parte-3/>`__

Credits to
~~~~~~~~~~

-  [[Seytonic\|https://www.youtube.com/channel/UCW6xlqxSY3gGur4PkGPEUeA]],
   youtube channel on hacking and hardware projects
-  Rogan Dawes, Sensepost, core developer of Universal Serial Abuse -
   [[USaBUSe\|https://github.com/sensepost/USaBUSe]]
-  Samy Kamkar, [[PoisonTap\|https://github.com/samyk/poisontap]]
-  Rob ‘[[MUBIX\|\ https://github.com/mubix]]’ Fuller, [[“Snagging creds
   from locked
   machines”\|\ https://room362.com/post/2016/snagging-creds-from-locked-machines/]]
-  Laurent Gaffie (lgandx),
   [[Responder\|https://github.com/lgandx/Responder]]
-  Darren Kitchen (hak5darren), [[DuckEncoder\|
   https://github.com/hak5darren/USB-Rubber-Ducky/]], time to implement
   a WiFi capable successor for BashBunny ;-)
-  All of the Github supporters

.. |Diagramm| image:: https://user-images.githubusercontent.com/13119970/30510901-d2ad38e6-9acd-11e7-8751-93f592de8d3f.jpg

