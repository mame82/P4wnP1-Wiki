# Quickstart

The full P4wnP1 A.L.O.A installation consists of Kali Linux, a custom Kernel and a modified WiFi Driver which can be quite difficult to install. Because of that, ready to go Kali Images are distributed as Releases on the [Releases Page](https://github.com/MaMe82/P4wnP1_aloa/releases).
Installation:
* Linux & Mac OS: `xzcat kali-linux-v0.1.0-alpha1-rpi0w-nexmon-p4wnp1-aloa.img.xz | dd of=/dev/sdb bs=4M`
* Windows: Unarchive with 7-Zip and flash with Rufus.

**screenshots coming soon**


The Raspberry will setup network connections via RNDIS/ECM (USB Networking) and WiFi AccessPoint when booting.
    * SSID: :collision::desktop computer::collision: Ⓟ➃ⓌⓃ&#24C5❶
    * PSK: `MaMe82-P4wnP1`
    * User: `root`
    * Password: `toor`
    * Web UI Address Wifi: `http://172.24.0.1:8000`
    * Web UI Address USB-Ethernet: `http://172.16.0.1:8000`
