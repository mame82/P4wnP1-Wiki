# Setup.cfg

**In this file, you can find extend documentation on every option in the setup.cfg file.**

The setup.cfg is the first file that gets loaded on start of the P4wnP1 service.  
The Payload gets loaded directly afterwards and **has the ability to override variables defined setup.cfg** (so if some features don't behave like they should, their settings are probably getting overridden by the payload)
***
## Gadgets
### **USB_VID**
**defines the USB-VendorID**  
Can be any 4-digit hexadecimal number, but if you want the Pi to like a certain device, you can look up VIDs by name at [the-sz.com](http://www.the-sz.com/products/usbid/).  
_Note:_ Mac OS only plug'n'plays Apple accessories. So you should change the VID to `0x05ac` if you plan on using the P4wnP1 only Apple devices.
### **USB_PID**
**defines the USB-ProductID**  
Can be any 4-digit hexadecimal number.  

***
### **USE_ECM**
**defines if the Pi should act as ethernet adapter on Mac OS / Linux machines**  
can be either true or false
### **USE_RNDIS**
**defines if the Pi should act as ethernet adapter on Windows machines**  
can be either true or false  
_Note:_ Since P4wnP1 is limited to USB 2.0 speeds, the reported internet speed is only 450 Mbit/s max.
You can use [this](https://github.com/mame82/ratepatch#bitrate-patch-for-p4wnp1) kernel Patch to maximize reported Internet speeds to 20Gbit/s (RNDIS) and 4Gbit/s (ECM)
### **USE_HID**
**defines if the Pi should act as keyboard.**  
can be either true or false; can be used in combination with USE_HID_MOUSE.
### **USE_HID_MOUSE**
**defines if the Pi should act as mouse.**  
can be either true or false; can be used in combination with USE_HID.
### **USE_RAWHID**
**defines if the covert HID channel is enabled.**
Used for bidirectional communication between P4wnP1 and Backdoor-Agent.
### **USE_UMS**
**defines if the pi should act as a mass storage unit**  
can be either true or false  
_Note:_ currently only 128MB capacity.

***
## Wired Network
### **IF_IP**
**defines the local IP of the P4wnP1 which can be used to connect to it from the target machine.**
### **IF_MASK**
**defines the netmask**
### **IF_DHCP_RANGE**
**defines the range of possible IPs assignable to the target**

### **ROUTE_SPOOF**
**defines the traffic from the target should be routed through P4wnP1**  
_Note:_ P4wnP1 needs internet connectivity and ipv4-forwarding enabled so requests go through.

### **WPAD_ENTRY**
TODO

## WIFI Network

***
### **WIFI_REG**
**defines the WiFi regulatory domain**  
if this is not set to the country you are currently in, you may be using banned bands or not using bands you are allowed to use.

***
### **WIFI_ACCESSPOINT**
**defines if an accesspoint should be started**
can be either true or false

### **WIFI_ACCESSPOINT_NAME**
**defines the name as which P4wnP1 will appear**
can be a string

### **WIFI_ACCESSPOINT_PSK**
**defines the password of the AP**
can be a string

### **WIFI_ACCESSPOINT_IP**
**defines the IP P4wnP1 will be accessible from the target**
can be a normal IP-address

### **WIFI_ACCESSPOINT_NETMASK**
**defines the Netmask**
can be a regular netmask

### **WIFI_ACCESSPOINT_DHCP_RANGE**
**defines a the range of possible IP addresses assigned via DHCP**
can be a two IP-addresses seperated by a comma.

### **WIFI_ACCESSPOINT_HIDE_SSID**
**defines if the WIFI_ACCESSPOINT_NAME is hidden**
might evade suspicious network admins that like to watch their wireless infrastructure :-)

***
### **WIFI_CLIENT**
**defines if P4wnP1 should try to connect to an already existing WiFi**
can be true or false; will fall back into AP mode if WIFI_ACCESSPOINT is true

### **WIFI_CLIENT_SSID**
**Name of the target network to connect to**

### **WIFI_CLIENT_PSK**
**Passphrase of the target network to connect to**

***
### **lang**
**defines the default language**
gets overridden in most payloads; so be aware that the language might got reset by the used payload.

### **HID_KEYBOARD_TEST**
**test if keyboard driver got installed and is ready to be used**
calls callback 'onKeyboardUp' afterwards; mostly there to provide a default if not set explicitly in payload.


***
## Bluetooth Network

_Note:_ Connecting Bluetooth Network Access Point (NAP) with a mobile device
requires to disable other networks with internet access on this device in most cases (like WiFi).
NAP provided by P4wnP1 doesn't necessarily provide Internet access, but is used to grant network access on P4wnP1 via bluetooth. The alternative would be to establish a "Group Network (GN)" instead of NAP, which unfortunately didn't work in most test cases, when it cames to connection of a mobile device.
So if Internet should be provided from P4wnP1 via NAP (which isn't the purpose of P4wnP1), P4wnP1 itself has to be connected to Internet (for example using RNDIS + ICS on windows or using the WiFi client mode). Additionally iptables rules have to be deployed to enable MASQUERADING on the respective outbound interface.

To summerize: P4wnP1 provides NAP as access option to SSH via bluetooth, not to serve Internet, although this could be achieved.

### BLUETOOTH_NAP=
Enable Bluetooth NAP to SSH in via Bluetooth
### BLUETOOTH_NAP_PIN=1337
unused, PIN authentication currently not working (custom agent for bluez 5 needed)
### BLUETOOTH_NAP_IP
IP used by P4wnP1
### BLUETOOTH_NAP_NETMASK
Mandantory Netmask
### BLUETOOTH_NAP_DHCP_RANGE
DHCP Server IP Range

***
## AutoSSH

### **AUTOSSH_ENABLED**
**defines if AUTOSSH reachback is enabled**
if enabled P4wnP1 will continuously try to bring up a SSH connection tunneling out its internal SSH server to a remote SSH Server
### **AUTOSSH_REMOTE_HOST**
**host address of the remote SSH server**
Should be a hostname like "_YourSSH-server.com_"
### **AUTOSSH_REMOTE_USER**
**valid user of the remote SSH server**
passwordless login has to be possible with the key given by AUTOSSH_PRIVATE_KEY
### **AUTOSSH_PRIVATE_KEY**
**path to private key used to login to the remote server**
(has to be present in ~/.ssh/authorized_keys file of AUTOSSH_REMOTE_USER)
### **AUTOSSH_PUBLIC_KEY**
**path to public key**
this key has to be present in ~/.ssh/authorized_keys file of AUTOSSH_REMOTE_USER (use ./ssh/pushkey.sh to assist)
### **AUTOSSH_REMOTE_PORT**
**port number**
P4wnP1's SSH shell will be reachable at this port on the remote SSH server (the port is bound to localhost and thus not exposed to public facing IP)
