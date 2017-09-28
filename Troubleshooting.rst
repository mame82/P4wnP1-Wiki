Troubleshooting
===============

| This contains the most common mistakes people make. Obviously, not
  every possible issue can be resolved by this this Guide. So if you
  can't figure out what is wrong, post an issue to the `P4wnP1 issue
  page <https://github.com/MaMe82/P4wnP1/issues>`__.
| If you want us to help you more efficiently, please post the output of
  ``sudo journalctl -u P4wnP1.service``, ``uname -v`` and the contents
  of the setup.cfg as well as an exact description of your problem.

hid\_backdoor and hid\_frontdoor are not working!
-------------------------------------------------

| The most common problem is that you did not use --recursive when
  cloning.
| If you are not sure if you did and already executed install.sh, it is
  enough to delete the your current copy and clone the repository again
  with the --recursive flag (and execute install.sh again).

issue with hid not outputting anything
--------------------------------------

Make sure you are piping your script/text to the correct function!

-  ``outhid`` for raw ASCII (can be used to easily pipe logfiles to HID)
-  ``duckhid`` for sending modifiers via DuckyScript (there is no way to
   send a non-character keys via outhid)

USB-Interfaces are not working but AccessPoint starts up.
---------------------------------------------------------

Make sure you plugged the Pi in via the power+data usb port, not the
power-only port.

My settings in setup.cfg are not used by the payload.
-----------------------------------------------------

Since the settings in setup.cfg are just default, some of them get
overwritten by the payload to fit them. So check if the currently used
payload overwrites your settings and edit the payload if necessary.

hid\_backdoor: "there is no screen to be detached"
--------------------------------------------------

| This is mostly due to a broken USB-cable or some issue in the
  installation process.
| Try to redo the steps
  `here <#hid_backdoor-and-hid_frontdoor-are-not-working>`__. If that
  doesnt fix the issue, do a clean reinstall of raspbian.

How do I get Internet on my P4wnP1 installation .
-------------------------------------------------

| The easiest way would be to have a WPA2-PSK network with Internet
  access and connect to it via the wifi client options in setup.cfg.
  P4wnP1 will automatically take care of getting an IP-address via DHCP.
| Most other solutions will interfere with the P4wnP1 internals.

Errors when injection the client code via PowerShell
----------------------------------------------------

`This Issue <https://github.com/MaMe82/P4wnP1/issues/33>`__ describes a
case where the McAffee antivirus blocks the loading of normal
(non-malicious) powershell modules. The injectionprocess chosen by
P4wnP1 is AV-safe and this is an issue with McAffe AV blocking the
ordinary execution of powershell. Try to disable/uninstall the AV and
test it again. (dont forget to reinstall it afterwards)

P4wnP1 booting into interactive mode instead of usb-client
----------------------------------------------------------

This is mostly likely due to a broken USB-Cable.
