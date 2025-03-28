<a href="https://github.com/cubi1337/homebridge-shelly-ng"><img src="homebridge-shelly-ng.png" height="120"></a>

# homebridge-shelly-ds9

[![npm-version](https://badgen.net/npm/v/homebridge-shelly-ds9)](https://www.npmjs.com/package/homebridge-shelly-ds9)

[Homebridge](https://homebridge.io) plugin for [Shelly](https://shelly.cloud),
enabling HomeKit support for the next generation of Shelly devices.This Package is only to pimp up the existing package [https://badgen.net/npm/v/homebridge-shelly-ng](https://badgen.net/npm/v/homebridge-shelly-ng). Because I'm lost if my Minis don't run in the Homebridge.

<a href='https://ko-fi.com/cubi1337' target='_blank'><img height='35' style='border:0px;height:46px;' src='https://az743702.vo.msecnd.net/cdn/kofi3.png?v=0' border='0' alt='Buy Me a Coffee at ko-fi.com' />

For the first generation, see [homebridge-shelly](https://github.com/alexryd/homebridge-shelly).

## Supported devices

- [Shelly Plus 1 + V3](https://kb.shelly.cloud/knowledge-base/shelly-plus-1)
- [Shelly Plus 1 PM + V3](https://kb.shelly.cloud/knowledge-base/shelly-plus-1pm)
- [Shelly Plus 1 Mini + V3](https://kb.shelly.cloud/knowledge-base/shelly-plus-1-mini)
- [Shelly Plus 1 PM Mini + V3](https://kb.shelly.cloud/knowledge-base/shelly-plus-1pm-mini)
- [Shelly Plus PM Mini + V3](https://kb.shelly.cloud/knowledge-base/shelly-plus-pm-mini)
- [Shelly Plus 2 PM](https://kb.shelly.cloud/knowledge-base/shelly-plus-2pm)
- [Shelly Plus i4](https://kb.shelly.cloud/knowledge-base/shelly-plus-i4)
- [Shelly Plus Plug US](https://kb.shelly.cloud/knowledge-base/shelly-plus-plug-us)
- [Shelly Plus Plug S](https://kb.shelly.cloud/knowledge-base/shelly-plus-plug-s-1)
- [Shelly Plus Plug UK](https://kb.shelly.cloud/knowledge-base/shelly-plus-plug-uk)
- [Shelly Plus Plug IT](https://kb.shelly.cloud/knowledge-base/shelly-plus-plug-it)
- [Shelly Plus 0-10V Dimmer](https://kb.shelly.cloud/knowledge-base/shelly-plus-0-10v-dimmer)
- [Shelly Plug S Gen3 Eu](https://kb.shelly.cloud/knowledge-base/shelly-plug-s-mtr-gen3)
- [Shelly Dimmer 0/1-10V PM Gen3](https://kb.shelly.cloud/knowledge-base/shelly-dimmer-0-1-10v-pm-gen3)
- [Shelly Dimmer Gen3](https://kb.shelly.cloud/knowledge-base/shelly-dimmer-gen3)
- [Shelly Pro 1](https://kb.shelly.cloud/knowledge-base/shelly-pro-1)
- [Shelly Pro 1 PM](https://kb.shelly.cloud/knowledge-base/shelly-pro-1pm)
- [Shelly Pro 2](https://kb.shelly.cloud/knowledge-base/shelly-pro-2)
- [Shelly Pro 2 PM](https://kb.shelly.cloud/knowledge-base/shelly-pro-2pm)
- [Shelly Pro 3](https://kb.shelly.cloud/knowledge-base/shelly-pro-3-v1)
- [Shelly Pro 4 PM](https://kb.shelly.cloud/knowledge-base/shelly-pro-4pm)
- [Shelly Pro Dual Cover PM](https://kb.shelly.cloud/knowledge-base/shelly-pro-dual-cover-pm)
- [Shelly Pro Dimmer 1PM](https://kb.shelly.cloud/knowledge-base/shelly-pro-dimmer-1pm)
- [Shelly Pro Dimmer 0/1-10V PM](https://kb.shelly.cloud/knowledge-base/shelly-pro-dimmer-0-1-10v-pm)
- [Shelly Pro Dimmer 2PM](https://kb.shelly.cloud/knowledge-base/shelly-pro-dimmer-2pm)

## Installation

Either install this plugin through [Homebridge Config UI X](https://github.com/oznu/homebridge-config-ui-x)
or manually by following these instructions:

1. Install Homebridge by [following the instructions](https://github.com/homebridge/homebridge/wiki).
2. Install this plugin by running `npm install -g homebridge-shelly-ds9`.
3. Add this plugin to the Homebridge config.json:

```
"platforms": [
  {
    "platform": "ShellyDS9",
    "name": "Shelly DS9"
  }
]
```

By default, devices will be discovered on your local network using mDNS and
WebSockets will then be used to communicate with them.

## Configuration

The following configuration options are available. Note that they are all optional.

```
{
  "devices": [
    {
      "id": "e.g. shellyplus1-abcdef123456",
      "name": "My Device",
      "exclude": false,
      "hostname": "e.g. 192.168.1.200",
      "password": "pa$$word",
      "switch:0": {
        "exclude": false,
        "type": "switch"
      },
      "switch:1": {
        "exclude": false,
        "type": "outlet"
      },
      "switch:2": {
        "exclude": false,
        "type": "switch"
      },
      "switch:3": {
        "exclude": false,
        "type": "switch"
      },
      "cover:0": {
        "exclude": false,
        "type": "windowCovering"
      }
    }
  ],
  "mdns": {
    "enable": true,
    "interface": "e.g. eth0 or 192.168.1.100"
  },
  "websocket": {
    "requestTimeout": 10,
    "pingInterval": 60,
    "reconnectInterval": [ 5, 10, 30, 60, 300, 600 ]
  }
}
```

See below for descriptions of each configuration option.

| Option                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `devices`                      | An array of one or more objects with options for specific devices.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `devices. id`                  | The device ID. [Here's how to find it](https://github.com/alexryd/homebridge-shelly-ng/wiki/Finding-a-device-ID).                                                                                                                                                                                                                                                                                                                                                                  |
| `devices. name`                | The name of the device. This will be shown in the homebridge log and will be used as the default name when the device is added to HomeKit. Note though that setting this value after the device has been added will not change the name in HomeKit. If no name is specified, this plugin will use the device name set in the Shelly app, or the name of the device model.                                                                                                          |
| `devices. exclude`             | Set this option to `true` to make this plugin ignore this device.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `devices. hostname`            | The IP address or hostname of the device. Set this value if your device can't be discovered automatically.                                                                                                                                                                                                                                                                                                                                                                         |
| `devices. password`            | The password to use if authentication has been enabled for the device.                                                                                                                                                                                                                                                                                                                                                                                                             |
| `devices. switch:0-3.exclude`  | Set this option to `true` to prevent the switch with the specified index number from being added to HomeKit.                                                                                                                                                                                                                                                                                                                                                                       |
| `devices. switch:0-3.type`     | The type of accessory used to represent the switch with the specified index number. Available options are `"outlet"` and `"switch"` (default).                                                                                                                                                                                                                                                                                                                                     |
| `devices. cover:0.exclude`     | Set this option to `true` to prevent this cover from being added to HomeKit.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `devices. cover:0.type`        | Only available for devices in cover mode. The type of accessory used to represent the cover. Available options are `"door"`, `"window"` (default) and `"windowCovering"`.                                                                                                                                                                                                                                                                                                          |
| `devices. light:0.exclude`     | Set this option to `true` to prevent this light from being added to HomeKit.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `mdns`                         | Settings for the mDNS device discovery service.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `mdns. enable`                 | Set this option to `false` to disable automatic device discovery using mDNS.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `mdns. interface`              | The network interface to use when sending and receiving mDNS packets. You probably don't need to use this setting unless you know what you're doing. If not specified, all available network interfaces will be used.                                                                                                                                                                                                                                                              |
| `websocket. requestTimeout`    | The time, in seconds, to wait for a response before a request is aborted.                                                                                                                                                                                                                                                                                                                                                                                                          |
| `websocket. pingInterval`      | The interval, in seconds, at which ping requests should be made to verify that the connection is open. Set to `0` to disable.                                                                                                                                                                                                                                                                                                                                                      |
| `websocket. reconnectInterval` | The interval, in seconds, at which a connection attempt should be made after a socket has been closed. If an array or a comma-separated list of numbers is specified, the first value will be used for the first connection attempt, the second value for the second attempt and so on. When the last value has been reached, it will be used for all subsequent connection attempts; unless the value is `0`, in which case no more attempts will be made. Set to `0` to disable. |
