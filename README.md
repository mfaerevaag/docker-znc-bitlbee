Dockerfiles
===========

Modified from [Squishtech](https://squishtech.com/2014/02/12/chat-proxy/) to:

 - include purplelib support
 - include Off-the-Record crypto
 - include [Facebook protocol](https://github.com/bitlbee/bitlbee-facebook)
 - **not** include Campfire


## Images

### ZNC

Version: 1.2

Extra modules:

 * clientaway


### Bitlbee

Version: 3.4.2

Configuration params:

 * `--ssl=openssl`
 * `--jabber=1`
 * `--otr=1`
 * `--purple=1`

plus [bitlbee-facebook](https://github.com/bitlbee/bitlbee-facebook).


## Installation

Clone repo and `cd` into it

With root privelidges:

    ./initialize <username> <znc-password> <bitlbee-password>
    ./start
