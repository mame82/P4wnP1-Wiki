# Payload: HID covert channel frontdoor

### Video demo

[![P4wnP1 HID demo youtube](https://img.youtube.com/vi/MI8DFlKLHBk/0.jpg)](https://www.youtube.com/watch?v=MI8DFlKLHBk&yt:cc=on)

### HID frontdoor features

-    Plug and Play install of HID device on Windows (tested on Windows 7 and Windows 10)
-    Covert channel based on a raw HID device
-    Pure **in memory PowerShell payload** - nothing is written to disk
-    Synchronous data transfer with about 32KBytes/s (fast enough for shells and small file transfers)
-    Custom protocol stack to handle HID communication and deal with HID data fragmentation
-    HID based file transfer from P4wnP1 to target memory
-    **Stage 0:** P4wnP1 sits and waits, till the attacker triggers the payload stage 1 (frequently pressing NUMLOCK)
-    **Stage 1:** payload with "user space driver" for HID covert channel communication protocols is **typed out to the target via USB keyboard**
-    **Stage 2:** Communications switches to HID channel and gives access to a custom shell on P4wnP1. This could be used to upload and run PowerShell scripts, which are hosted on P4wnP1, directly into memory of the PowerShell process running on the target. This happens without touching disc or using network communications, at any time.


