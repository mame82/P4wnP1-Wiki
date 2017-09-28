Payload: Stealing Browser credentials (hakin9\_tutorial)
========================================================

| This payload runs a PowerShell script, typed out via P4wnP1's built-in
  keyboard, in order to dump stored credentials of Microsoft Edge or
  Internet Explorer. Fetched credentials are stored to P4wnP1's
  flashdrive (USB Mass Storage).
| As the name implies, this payload is the result of an hakin9 article
  on payload development for P4wnP1, which is yet unpublished. For this
  reason, the payload has RNDIS enabled, although not needed to carry
  out the attack.
| It's main purpose is to show how to store the result from a keyboard
  based attack, to P4wnP1's flashdrive, although the driver letter is
  only known at runtime of the payload.

Video demo
~~~~~~~~~~

|P4wnP1 LockPicker demo youtube|

.. |P4wnP1 LockPicker demo youtube| image:: https://img.youtube.com/vi/iZXNQNIpm7s/0.jpg
   :target: https://www.youtube.com/watch?v=iZXNQNIpm7s
