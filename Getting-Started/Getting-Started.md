# Getting started

The default payload (payloads/network_only.txt) makes the Pi accessible via Ethernet over USB, WiFi (and Bluetooth?).
You could SSH into P4wnP1

via USB

    pi@172.16.0.1

or via WiFi

	pi@172.24.0.1
	Network name: P4wnP1
	Key: MaMe82-P4wnP1

or via Bluetooth PAN

  TODO


From there you could alter `setup.cfg` to change the current payload (`PAYLOAD` parameter) and keyboard language (`LANG` parameter).

Caution:
If the chosen payload overwites the global `LANG` parameter (like the hid_keyboard demo payloads), you have to change the `LANG` parameter in the payload, too. If your remove the `LANG` parameter from the payload, the setting from `setup.cfg` is taken. In short words, settings in payloads have higher priority than settings in `setup.cfg`
