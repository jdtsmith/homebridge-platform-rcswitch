# homebridge-platform-rcswitch
[![NPM Version](https://img.shields.io/npm/v/homebridge-platform-rcswitch.svg)](https://www.npmjs.com/package/homebridge-platform-rcswitch)

RCSwitch plugin for the awesome
[Homebridge](https://github.com/nfarina/homebridge) project.

Modified to use the new gpiomem WiringPi system and GPIO pin numbering
system (BCM pin numbers) for compatibility with other GPIO-using
Homebridge modules.


## Currently supports
- Etekcity Tap 5 port Power plug
- other 433 Mhz remote plugs should work.

# Installation

1. Install libuv-dev using: `apt-get install libuv-dev`
2. Install homebridge using: `npm install -g homebridge`
3. Install this plugin using: `npm install -g homebridge-platform-rcswitch`
4. Update your configuration file. See the sample below.

# Configuration

Configuration sample:

`send_pin`, `sniffer_pin` is the gpio pin you are using to send/receive signal.   If `sniffer_pin` is not set, no receiving will be enabled.  This module uses the BCM pin numbering system, which is different than the physical pin you are using. see [wireingpi.com](http://wiringpi.com/pins/) for details (or try `gpio readall`)

`switches` is the list of the "buttons" codes on your remote. If you have the modular sniffing module active, start without any switch configed, press the button on your remote, you should get your code in homebridge log console.  Or just invent a code and train your remote with it.


 ```javascript
{
    "bridge": {
        "name": "#####",
        "username": "",
        "port": 51826,
        "pin": ""
    },

    "description": "",

    "platforms": [
        {
          "platform": "RCSwitch",
          "name": "RCSwitch Platform",
          "send_pin": 0,
          "sniffer_pin": 2,
          "tolerance": 90,
          "switches": [
                {
                        "name" : "Zap Plug Port 1",
                        "on": {
                                "code":xxxxxx,
                                "pulse":188
                        },
                        "off": {
                                "code":xxxxxx,
                                "pulse":188
                        }
                }
          ]
        }
    ]
}

```


# Credits

Credit goes to
- [wireing pi](http://wiringpi.com/pins/)
- 433 control codes ported from [433Utils](https://github.com/ninjablocks/433Utils)
- [rfoutlet project](https://github.com/timleland/rfoutlet) and his [blog post](https://timleland.com/wireless-power-outlets/)
- [http://scottfrees.com/](http://scottfrees.com/) for his great tutorial for asynchronous call.
- inspired by [homebridge-platform-wemo] https://github.com/rudders/homebridge-platform-wemo
- rainlake rewrote this
- jdtsmith adapted the pin numbering scheme for [compatibility with other plugins](https://github.com/n8henrie/homebridge-rcswitch-gpiomem/issues/11).


# License

Published under the MIT License.
