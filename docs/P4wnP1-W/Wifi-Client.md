P4wnP1 starts an Accesspoint by default. Which is desired on most cases when on an Assessment. Unfortunately, the Pi doesn't have internet access. So the Wifi client feature was introduced which opens up multiple new possibilities.

1. Easy update of P4wnP1 and Raspbian.
2. Forwarding requests from the target machine.
3. Extending the wifi distance by using a stronger accesspoint as router
4. [AutoSSH integration](P4wnP1-W/AutoSSH.md) for automatic reverse connections.

The client setting can be configured in the `setup.cfg` in the P4wnP1 root directory:

* WIFI_CLIENT=false # enables the client functionality
* WIFI_CLIENT_SSID="Accespoint Name" # the SSID of the AccessPoint
* WIFI_CLIENT_PSK="AccessPoint password" # cleartext passphrase for the network
* WIFI_CLIENT_STORE_NETWORK=false # currently unused
* WIFI_CLIENT_OVERWRITE_PSK=true # currently unused

**Note:**  
Currently only supports WPA2 PSK networks. Enterprise networks might be difficult to debug if you dont have on so you have to write your own implementation. [related issue](https://github.com/mame82/P4wnP1/issues/106)
Could slow down boot because the scan for the desired network is issued upfront and the DHCP client gets started and waits for a lease.  
if [WIFI_ACCESSPOINT](P4wnP1-W/Wifi-Hotspot.md) is set to true as well, P4wnP1 starts an Accesspoint if the target network was not found.
