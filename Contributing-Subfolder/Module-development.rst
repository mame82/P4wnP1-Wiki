Module Development
==================

The Architecture
~~~~~~~~~~~~~~~~

| If you want to develop custom payloads, you have to understand how
  P4wnP1 includes files and invokes functions.
| When the P4wnP1 boots, the P4wnP1.service is run which invokes the
  file ``boot/boot_P4wnP1``
| It it reads the ``setup.cfg`` and the payload in ``payload/$PAYLOAD``
  which overrides variables defined in ``setup.cfg``. Since this happens
  at the start, any functionality thats outside the callbacks (seen
  below) is executed immediately!
| When P4wnP1 configures the different gadgets, it looks at the
  variables defined earlier by the setup.cfg and the selected payload.
| When running through this routine, P4wnP1 uses
  ``declare -f <callback function> > /dev/null && <callback function>``
  to determine if ``callback function`` is defined and executes it when
  it is.
| Available callbacks are (listed by their usual sequence of execution:

#. onNetworkUp (gets called when the target connected to the interface)
#. onTargetGotIP (gets called when the target got an IP-address assigned
   by the P4wnP1)
#. onKeyboardUp (gets called when the target finished installing the
   driver)
#. onLogin (gets called when somebody ssh's into P4wnP1)

**Note:** This order isn't guaranteed since some functions are run
asynchronously.

Available utility functions:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| In addition to having the freedom of bash and 3rd party tools, P4wnP1
  comes also in equipped with various functions to interface with its
  USB-Gadget abilities:
| *(some of these are only available through the payload)*

-  ``duckhid``,\ ``outhid`` & ``mousescript``
   Detailed description [[here\|OS independent features Home]]
-  | ``led_blink``
   | Usage: ``led_blink <blink amount>``
   | Causes the Pi's onboard Led to blink times.
   | ``led_blink 0``: Off
   | ``led_blink 255``: On
   | ``led_blink x`` blink for x times.
   | blink-cycles are 0.3s long and pause is 0.8s long.

-  ``scan_for_essid``
   Usage: ``scan_for_essid <network name>``
   possible returnvalues:
-  *WPA2\_PSK*
-  *WPA2 no CCMP PSK*
-  *Network not found*

Available utility variables:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  ``WIFI`` *bool*
   determines if wlan0 interface is present (can be used to check if the
   Pi has wireless capabilities)
-  ``WIFI_CLIENT_CONNECTION_SUCCESS`` *bool*
   determines if connecting as a wifi client went successful
   **Note:** These are supposed to be read-only and only accessible
   inside the callbacks since this might cause unexpected behavior in
   the boot process!
-  **Every setting in [[setup.cfg]]**
   these are supposed to be overridden **outside** the callback
   functions, not during the boot process

Styleguide
~~~~~~~~~~

TODO

``payload/template.txt`` is a good place to start and it contains some
further documentation.
