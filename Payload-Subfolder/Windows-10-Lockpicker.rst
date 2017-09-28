Payload: Windows LockPicker
===========================

This payload extends the "Snagging creds from locked machine" approach,
presented by Mubix (see credits), to its obvious successor:

**P4wnP1 LockPicker cracks grabbed hashes and unlocks the target on
success, using its keyboard capabilities.** This happens fully
automated, without further user interaction.

Video demo
~~~~~~~~~~

| I'm still no video producer, so maybe somebody feels called upon to do
  a demo.
| Here's my (sh\*\*ty) attempt:

|P4wnP1 LockPicker demo youtube|

Here's a version of someone doing this much better, thanks @Seytonic

|P4wnP1 LockPicker demo youtube|

Attack chain (short summary):
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. The USB network interface of P4wnP1 is used to bring up a DHCP which
   provides its configuration to the target client.
#. Among other options, a WPAD entry is placed and static routes for the
   whole IPv4 address space are deployed to the target.
#. P4wnP1 redirects traffic dedicated to remote hosts to itself using
   different techniques.
#. Requests for various protocols originating from the target, are
   fetched by "Responder.py", which forces authentication and tries to
   steal the hashes used for authentication.
#. If a hash gets grabbed, P4wnP1 LED is blinking three times in
   sequence, to signal that you could unplug and walk away with the
   hashes for offline cracking. **Or...**
#. ... you leave P4wnP1 plugged and the hashes are handed over to John
   the Ripper, which tries to bruteforce the captured hash.
#. If the ´password of the user who locked the box is weakly choosen,
   chances are high that John the Ripper is able to crack it, which
   leads to...
#. ... **P4wnP1** ultimately enters the password, in order to unlock the
   box and you're able to access the box (the cracked password is stored
   in ``collected`` folder, along with the hashes).

The payload ``Win10_LockPicker.txt`` has to be choosen in ``setup.cfg``
to carry out the attack. **It is important to modify the payloads "lang"
parameter to your target's language**. If you attach a HDMI monitor to
P4wnP1, you could watch the status output of the attack (including
captured hash and plain creds, if you made it this far).

.. |P4wnP1 LockPicker demo youtube| image:: https://img.youtube.com/vi/7fCPsb6quKc/0.jpg
   :target: https://www.youtube.com/watch?v=7fCPsb6quKc
.. |P4wnP1 LockPicker demo youtube| image:: https://img.youtube.com/vi/KDJKE10LCjM/0.jpg
   :target: https://www.youtube.com/watch?v=KDJKE10LCjM
