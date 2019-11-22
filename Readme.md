# node-red-contrib-sonoff-tasmota-multichannel

[![NPM version][npm-image]][npm-url]

> A [Node-RED](https://nodered.org) node, to control [Sonoff](https://www.itead.cc/) switches running the awesome [Sonoff-Tasmota](https://github.com/arendst/Sonoff-Tasmota) firmware with support for Multichannel Devices

This Release based on the Work from [EdgarM73](https://github.com/EdgarM73/node-red-contrib-sonoff-tasmota) which is based on the original work by [Steffen Müller](http://steffen.io) I only added Multichannel support for Devices up to 8-Channel (this Multichannel Support was created by [gitolicious](https://github.com/gitolicious/node-red-contrib-sonoff-tasmota)) but never released. So first i tested it on my local maschine and after that i put it on Github so everyone could use it.

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

## Screenshot

![Sample Config Interface](/media/config-ui.png?raw=true)


## Sample FLOW

![Sample Flow](/media/sample.png?raw=true)

In my Sample ia also use [WeMo-Emulator](https://flows.nodered.org/node/node-red-contrib-wemo-emulator) to make my Amazon Alexa Device controll the Tasmato Port

```json
[
    {
        "id": "f946cb9c.c50878",
        "type": "ui_switch",
        "z": "4352e0fd.48412",
        "name": "",
        "label": "Steckdose 1",
        "tooltip": "",
        "group": "adc57193.8c48b",
        "order": 1,
        "width": 0,
        "height": 0,
        "passthru": false,
        "decouple": "true",
        "topic": "",
        "style": "",
        "onvalue": "true",
        "onvalueType": "bool",
        "onicon": "fa-plug",
        "oncolor": "green",
        "offvalue": "false",
        "offvalueType": "bool",
        "officon": "fa-plug",
        "offcolor": "gray",
        "x": 390,
        "y": 20,
        "wires": [
            [
                "67481b8f.dbbeb4"
            ]
        ]
    },
    {
        "id": "41ffeeb4.ea6d9",
        "type": "inject",
        "z": "4352e0fd.48412",
        "name": "",
        "topic": "command",
        "payload": "toggle",
        "payloadType": "str",
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "x": 110,
        "y": 100,
        "wires": [
            [
                "99cde518.a2fae8"
            ]
        ]
    },
    {
        "id": "50450f96.e87be",
        "type": "debug",
        "z": "4352e0fd.48412",
        "name": "",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "true",
        "targetType": "full",
        "x": 560,
        "y": 100,
        "wires": []
    },
    {
        "id": "99cde518.a2fae8",
        "type": "Sonoff device Enhanced",
        "z": "4352e0fd.48412",
        "mode": "0",
        "channel": "POWER1",
        "broker": "4333ee38.d379a",
        "device": "tasmota",
        "name": "Port1",
        "onValue": "ON",
        "offValue": "OFF",
        "toggleValue": "toggle",
        "cmdPrefix": "cmnd",
        "statPrefix": "stat",
        "telePrefix": "tele",
        "x": 370,
        "y": 100,
        "wires": [
            [
                "50450f96.e87be",
                "f946cb9c.c50878"
            ]
        ]
    },
    {
        "id": "67481b8f.dbbeb4",
        "type": "change",
        "z": "4352e0fd.48412",
        "name": "",
        "rules": [
            {
                "t": "change",
                "p": "payload",
                "pt": "msg",
                "from": "true",
                "fromt": "bool",
                "to": "toggle",
                "tot": "str"
            },
            {
                "t": "change",
                "p": "payload",
                "pt": "msg",
                "from": "false",
                "fromt": "bool",
                "to": "toggle",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 580,
        "y": 20,
        "wires": [
            [
                "99cde518.a2fae8"
            ]
        ]
    },
    {
        "id": "a8ea0c0c.01558",
        "type": "wemo-emulator",
        "z": "4352e0fd.48412",
        "name": "Steckdose 1",
        "friendlyName": "Port 1",
        "serial": "port1",
        "port": "1",
        "onTopic": "an",
        "onPayload": "true",
        "offTopic": "aus",
        "offPayload": "false",
        "x": 90,
        "y": 40,
        "wires": [
            [
                "67481b8f.dbbeb4"
            ]
        ]
    },
    {
        "id": "adc57193.8c48b",
        "type": "ui_group",
        "z": "",
        "name": "Tasmota",
        "tab": "7e885294.f7eb1c",
        "disp": true,
        "width": "6",
        "collapse": true
    },
    {
        "id": "4333ee38.d379a",
        "type": "mqtt-broker",
        "z": "",
        "name": "",
        "broker": "192.168.178.105",
        "port": "1883",
        "clientid": "",
        "usetls": false,
        "compatmode": false,
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
        "id": "7e885294.f7eb1c",
        "type": "ui_tab",
        "z": "",
        "name": "Tasmato Leiste",
        "icon": "dashboard",
        "order": 13,
        "disabled": false,
        "hidden": false
    }
]
```

I think this Sample could be a bit dirty, but in my case it works perfect

## NOTE!!
As I am not an developer (this project is an Copy and Past reuslt of wanted and unpublished features) i will try to keep it up-to-date with the Base i merged this from

## License

MIT © [Steffen Müller](http://steffen.io)

[npm-url]: https://www.npmjs.com/package/node-red-contrib-sonoff-tasmota-enhanced
[npm-image]: https://www.npmjs.com/package/node-red-contrib-sonoff-tasmota-enhanced.svg
