# node-red-contrib-sonoff-tasmota-multichannel

[![NPM version][npm-image]][npm-url]

> A [Node-RED](https://nodered.org) node, to control [Sonoff](https://www.itead.cc/) switches running the awesome [Sonoff-Tasmota](https://github.com/arendst/Sonoff-Tasmota) firmware

This Release based on https://github.com/EdgarM73/node-red-contrib-sonoff-tasmota which is based on the original work by [Steffen Müller](http://steffen.io) I only added Multichannel support for Devices up to 8-Channel

## Installation

Install `node-red-contrib-sonoff-tasmota-multichannel` using [npm](https://www.npmjs.com/):

```bash
npm install --save node-red-contrib-sonoff-tasmota-multichannel
```

## Usage

To use the node, just drag the node from the Sonoff section to the Flow, add the id and the mqtt broker. 
To control the switch you can use a true/false input node or connect a UI Button.

Toggle:
send a Message with topic 'command' and payload 'toggle' to the node to toggle the tasmota device

ON/OFF:
send a Message with topic 'command' and payload 'on' or 'off' to the node to turn ON or OFF the tasmota device

Color:
send a Message with topic 'color' and payload Color

Dimmer:
send a Message with topic 'dimmer' and payload number in percent


## Sample FLOW

![Sample Flow](/media/flow.png?raw=true)

```json
[
    {
        "id": "13346fe3.f9dbb",
        "type": "tab",
        "label": "Flow 3",
        "disabled": false,
        "info": ""
    },
    {
        "id": "44ae399c.bb1f98",
        "type": "Sonoff device Enhanced",
        "z": "13346fe3.f9dbb",
        "mode": "0",
        "broker": "29d7744c.2a685c",
        "device": "wzindirekt",
        "name": "",
        "onValue": "ON",
        "offValue": "OFF",
        "toggleValue": "toggle",
        "cmdPrefix": "cmnd",
        "statPrefix": "stat",
        "telePrefix": "tele",
        "x": 580,
        "y": 200,
        "wires": [
            [
                "5f49cd7a.34a5d4",
                "a622f4f8.d75468"
            ]
        ]
    },
    {
        "id": "5f49cd7a.34a5d4",
        "type": "ui_switch",
        "z": "13346fe3.f9dbb",
        "name": "",
        "label": "switch",
        "tooltip": "",
        "group": "9d03a37c.7d0558",
        "order": 3,
        "width": 0,
        "height": 0,
        "passthru": false,
        "decouple": "false",
        "topic": "",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "",
        "oncolor": "",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "",
        "offcolor": "",
        "x": 580,
        "y": 120,
        "wires": [
            [
                "44ae399c.bb1f98"
            ]
        ]
    },
    {
        "id": "bf67af5f.71565",
        "type": "inject",
        "z": "13346fe3.f9dbb",
        "name": "",
        "topic": "command",
        "payload": "toggle",
        "payloadType": "str",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "x": 320,
        "y": 180,
        "wires": [
            [
                "44ae399c.bb1f98"
            ]
        ]
    },
    {
        "id": "be4c48bd.0668f8",
        "type": "inject",
        "z": "13346fe3.f9dbb",
        "name": "",
        "topic": "color",
        "payload": "#ff4500",
        "payloadType": "str",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "x": 310,
        "y": 120,
        "wires": [
            [
                "44ae399c.bb1f98"
            ]
        ]
    },
    {
        "id": "a622f4f8.d75468",
        "type": "debug",
        "z": "13346fe3.f9dbb",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "x": 760,
        "y": 200,
        "wires": []
    },
    {
        "id": "29d7744c.2a685c",
        "type": "mqtt-broker",
        "z": "",
        "name": "pinky MQTT",
        "broker": "192.168.178.55",
        "port": "1883",
        "clientid": "",
        "usetls": false,
        "compatmode": true,
        "keepalive": "60",
        "cleansession": true,
        "birthTopic": "",
        "birthQos": "0",
        "birthPayload": "",
        "closeTopic": "",
        "closeQos": "0",
        "closePayload": "",
        "willTopic": "",
        "willQos": "0",
        "willPayload": ""
    },
    {
        "id": "9d03a37c.7d0558",
        "type": "ui_group",
        "z": "",
        "name": "Raum-Temperatur",
        "tab": "b132103a.17961",
        "disp": true,
        "width": "6",
        "collapse": true
    },
    {
        "id": "b132103a.17961",
        "type": "ui_tab",
        "z": "",
        "name": "Wohnzimmer",
        "icon": "dashboard",
        "order": 12,
        "disabled": false,
        "hidden": false
    }
]
```

## License

MIT © [Steffen Müller](http://steffen.io)

[npm-url]: https://www.npmjs.com/package/node-red-contrib-sonoff-tasmota-enhanced
[npm-image]: https://www.npmjs.com/package/node-red-contrib-sonoff-tasmota-enhanced.svg
