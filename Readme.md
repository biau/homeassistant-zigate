# ZiGate component for Home Assistant
A new component to use the ZiGate (http://zigate.fr)

[![Build Status](https://travis-ci.org/doudz/homeassistant-zigate.svg?branch=master)](https://travis-ci.org/doudz/homeassistant-zigate)
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://paypal.me/sebramage)

To install:
- if not exists, create folder 'custom\_components' under your home assitant directory (beside configuration.yaml)
- copy all the files in your hass folder, under 'custom\_components' like that :

```
custom_components/
├── binary_sensor
│   └── zigate.py
├── light
│   └── zigate.py
├── sensor
│   └── zigate.py
├── switch
│   └── zigate.py
└── zigate
    ├── __init__.py
    └── services.yaml
```
    
- adapt your configuration.yaml

To pair a new device, go in developer/services and call the 'zigate.permit\_join' service.
You have 30 seconds to pair your device.

# WARNING : Since commit [ddf141e](https://github.com/doudz/homeassistant-zigate/commit/ddf141ebb103eaa4f6d585b645262446fd77d202), you have to rename the file .zigate.json to zigate.json to avoid loosing your configuration !


Configuration example :

```
# Enable ZiGate (port will be auto-discovered)
zigate:

```
or

```
# Enable ZiGate
zigate:
  port: /dev/ttyS0
  channel: 24

```

or
if you want to use Wifi ZiGate (or usb zigate forwarded with ser2net for example)
Port is optionnal, default is 9999 

```
# Enable ZiGate Wifi
zigate:
  host: 192.168.0.10:9999

```

Currently it supports sensor, binary_sensor and switch and light

## How enable debug log

```yaml
logger:
  default: error
  logs:
    zigate: debug
    custom_components.zigate: debug

```
Alternatively you could call the service `logger.set_level` with data `{"custom_components.zigate": "debug", "zigate": "debug"}`

## How to adjust device parameter

Some devices have the ability to change some parameters, for example on the Xiaomi vibration sensor you can adujst the sensibility. You'll be able to do that using the service `write_attribute` with parameters :
`{ "addr": "8c37", "endpoint":"1", "cluster":"0", "attribute_id":"0xFF0D", "manufacturer_code":"0x115F", "attribute_type":"0x20", "value":"0x01" }`

In this example, the value is the sensiblity, it could be 0x01 for "high sens", 0x0B for "medium" and 0x15 for "low"
