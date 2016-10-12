Dockerfiles
===========

Modified from [Squishtech](https://squishtech.com/2014/02/12/chat-proxy/) to:

 - **not** include Campfire.
 - include Facebook protocol 
 - include Purplelib support 
 - include OTR crypto 

ZNC
---

Version: 1.2

Extra modules:

 * clientaway


Bitlbee
-------

Version: 3.4.2

Configuration params:

 * `--ssl=openssl`
 * `--jabber=1`
 * `--otr=1`
 * `--purple=1`
