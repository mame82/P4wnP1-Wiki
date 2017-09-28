P4wnP1 starts an Accesspoint by default. Which is desired on most cases
when on an Assessment. Unfortunately, the Pi doesn't have internet
access. So the Wifi client feature was introduced which opens up
multiple new possibilities.

#. Easy update of P4wnP1 and Raspbian.
#. Forwarding requests from the target machine.
#. Extending the wifi distance by using a stronger accesspoint as router
#. [[AutoSSH integration\|AutoSSH]] for automatic reverse connections.

The client setting can be configured in the ``setup.cfg`` in the P4wnP1
root directory:

-  WIFI\_CLIENT=false # enables the client functionality
-  WIFI\_CLIENT\_SSID="Accespoint Name" # the SSID of the AccessPoint
-  WIFI\_CLIENT\_PSK="AccessPoint password" # cleartext passphrase for
   the network
-  WIFI\_CLIENT\_STORE\_NETWORK=false # currently unused
-  WIFI\_CLIENT\_OVERWRITE\_PSK=true # currently unused

| **Note:**
| Currently only supports WPA2 PSK networks. Enterprise networks might
  be difficult to debug if you dont have on so you have to write your
  own implementation. `related
  issue <https://github.com/mame82/P4wnP1/issues/106>`__
| Could slow down boot because the scan for the desired network is
  issued upfront and the DHCP client gets started and waits for a lease.
| if [[WIFI\_ACCESSPOINT\|Wifi Hotspot]] is set to true as well, P4wnP1
  starts an Accesspoint if the target network was not found.
