P4wnP1 more advanced features (excerpt)
=======================================

Advanced HID Features
~~~~~~~~~~~~~~~~~~~~~

-  Keyboard payloads could be **triggered by targets main keyboard
   LEDs** (NUMLOCK, CAPSLOCK and SCROLLLOCK)
-  **dynamic payload branching** based on LED triggers
-  Supports **DuckyScript** (see
   `hid\_keyboard2.txt <payloads/hid_keyboard2.txt>`__ payload for an
   advanced example)
-  Supports **raw ASCII Output via HID Keyboard** (could be used to
   print out character based files via keyboard, like
   ``cat /var/log syslog | outhid``)
-  **Multi Keyboard language layout support** (no need to worry about
   target language when using HID commands)
-  Output starts when target keyboard driver is loaded (no need for
   manual delays, ``onKeyboardUp`` callback could be used in payloads)
-  Supports **[[MouseScript\|OS Independent Features
   Home#mousescript]]**

Advanced Network Features
~~~~~~~~~~~~~~~~~~~~~~~~~

-  Fake **RNDIS network interface speed up to 20GB/s** to get the lowest
   metric and win every fight for the dominating 'default gateway' entry
   in routing tables, while carrying out network attacks (patch could be
   found `here <https://github.com/mame82/ratepatch/commits/master>`__
   and the README
   `here <https://github.com/mame82/ratepatch/blob/master/README.md>`__)
-  **Automatic link detection** and interface switching, if a payload
   enables both RNDIS and ECM network
-  SSH server is running by default, so P4wnP1 could be connected on
   172.16.0.1 (as long as the payload enables RNDIS, CDC ECM or both) or
   on 172.24.0.1 via WiFi
-  if both, WiFi client mode and WiFi Access Point mode, are enable -
   **P4wnP1 fails over to open an Access Point in case the target WiFi
   isn't reachable** (Pi Zero W only)

Advanced payload features
~~~~~~~~~~~~~~~~~~~~~~~~~

-  bash **payloads based on callbacks** (see
   ```template.txt`` <payloads/template.txt>`__ payload for details)

   -  **onNetworkUp** (when target host gets network link active)
   -  **onTargetGotIP** (if the target received an IP, the IP could be
      accessed from the payload script)
   -  **onKeyboardUp** (when keyboard driver installation on target has
      finished and keyboard is usable)
   -  **onLogin** (when a user logs in to P4wnP1 via SSH)

-  configuration can be done globally (``setup.cfg``) or overwritten per
   payload (if the same parameter is defined in the payload script)
-  settings include:

   -  USB config (Vendor ID, Product ID, **device types to enable** ...)
   -  WiFi config (SSID, password ...)
   -  HID keyboard config (**target keyboard language** etc.)
   -  Network and DHCP config
   -  **Payload Selection**
