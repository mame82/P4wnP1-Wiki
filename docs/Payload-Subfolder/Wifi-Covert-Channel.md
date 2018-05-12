
# P4wnP1 WiFi covert channel

!!! warning  
      **EXPERIMENTAL**

!!! note ""
      For additional notes see comments in code ... no time to document, right now ... sorry!!


## Usage:

1. Client infection
* be sure to have the `lang` option in this payload set according to the clients keyboard layout (default us)
* attach P4wnP1 to clients, wait till LED blinks twice (target is ready to receive keyboard input)
* press NUMLOCK on target about 5-times (fast)
* P4wnP1 starts typing out the payload, if `HIDE_AGENT_WINDOW` is enabled, the console window gets hidden
* During typing the LED stops blinking, wait till the LED blinks again (P4wnP1 is still typing out the payload
  even if the window is hidden)
* When the LED blinks again, the client payload should be running and P4wnP1 could be removed
* THE CLIENT NEEDS A WIFI ENABLED INTERFACE FOR THE CHANNEL TO WORK. BUT, THERE'S NO NEED TO HAVE THE CLIENT CONNECTED
  TO ANY WIFI (that's what this is all about)

2. Bring up C2 Server
* Attach P4wnP1 to another host OR POWER SOURCE (there's no host needed, as C2 server is accessed via WiFi/Bluetooth (Depends on the chosen Payload))
* P4wnP1 spawns a WiFi hotspot / Bluetooth NAP with name and password set according to the options in this payload
* connect to the network/bluetooth and login to P4wnP1 with user `pi` and your password
* on login the C2 serve is attached to the SSH session
		* issue `sessions` to list currently connected clients
		* use `interact <SESSION NUMBER>` to spawn a shell (comms are slow on this channel, so be patient)
		* press [CTRL + C] during interaction to bring up a menu for the session

Additional notes:

* the target is still able to connect to WiFi networks and use them, but the payload impacts throughput of valid
communications as scans are issued rapidly
* the client agent is tested against Win 7 64 / Win 10 64 with Intel WiFi adapters, but still considered
experimental (no support)
* If HIDE_AGENT_WINDOW=false is set, the client agent console is kept visible and displays debug output (the curently
shipped payload is a DEBUG build)
* the payload requires latest P4wnP1 installation (modifications to WiFi kernel modules and driver stack) to
work and should run on kernel 4.9.78+
* The payload comes in three different variatons, hid_only_delivery32.txt, hid_only_delivery64.txt and hid_only_delivery64_bt_only.txt
their differences are explained in comments in setup.cfg


Client agent code:
	https://github.com/mame82/P4wnP1_WiFi_covert_channel_client/blob/master/NWiFi/Agent.cs
C2 server code:
	https://github.com/mame82/P4wnP1_nexmon_additions/blob/master/wifi_server.py
WiFi driver + firmware mod:
	not yet published, compiled version in latest P4wnP1_nexmon_additions
Firmware interaction layer:
	https://github.com/mame82/P4wnP1_nexmon_additions/blob/master/mame82_util.py
More detailed descrition:
	https://github.com/mame82/P4wnP1_WiFi_covert_channel_client/blob/master/README.md
Video demo:
  https://www.youtube.com/watch?v=fbUBQeD0JtA
