# @tosolve/node-red-datacodec

[![npm version](https://img.shields.io/npm/v/@tosolve/node-red-datacodec)](https://www.npmjs.com/package/@tosolve/node-red-datacodec)
[![license](https://img.shields.io/npm/l/@tosolve/node-red-datacodec)](LICENSE)
[![Node-RED](https://img.shields.io/badge/Node--RED-compatible-red)](https://nodered.org)

A Node-RED node that decodes hexadecimal IoT sensor packets into structured JSON, powered by [@tosolve/datacodec](https://github.com/2solve/2solve-datacodec).

---

## Installation

Via the Node-RED palette manager, or from the command line:

```bash
cd ~/.node-red
npm install @tosolve/node-red-datacodec
```

Restart Node-RED after installation.

---

## Node: `2stools-datacodec`

**Category:** Function  
**Inputs:** 1 &nbsp;|&nbsp; **Outputs:** 1

### How it works

The node reads the incoming payload, decodes the hex-encoded sensor packet using the `@tosolve/datacodec` library, and outputs the decoded sensor data as a JSON object on `msg.payload`.

### Input

| Property | Type | Description |
|---|---|---|
| `msg.payload` | `string` \| `object` | Raw hex string, or an object containing a `payload_raw` field |
| `msg.offset` | `number` | _(optional)_ Byte offset to apply when decoding. Overrides the node's configured offset |

If `msg.payload` is an object with a `payload_raw` field (e.g. a LoRaWAN uplink envelope), that field is used as the raw payload automatically.

### Output

| Property | Type | Description |
|---|---|---|
| `msg.payload` | `object` | Decoded sensor data as a key-value JSON object |

### Configuration

| Property | Default | Description |
|---|---|---|
| Name | — | Optional label displayed in the Node-RED editor |
| Offset | `0` | Byte offset applied during decoding |

---

## Usage example

**Minimal flow:**

```
[inject] → [2stools-datacodec] → [debug]
```

Set the inject node payload to a hex string such as `010045001B0200FA` and connect it to the node. The debug panel will show the decoded sensor values.

**LoRaWAN envelope input:**

If the upstream node outputs a LoRaWAN envelope, the node automatically extracts `msg.payload.payload_raw` before decoding — no function node required.

---

## Migration from `node-red-2stools-packetdecode`

If you are upgrading from the previous package, see the [CHANGELOG](CHANGELOG.md) for full migration instructions, including how to update existing flows that reference the old node type `2stools-packetdecode`.

---

## Requirements

- Node-RED `>= 1.0.0`
- Node.js `>= 12.0.0`

---

## Author

[2Solve Engenharia e Tecnologia Ltda](https://www.2solve.com.br)

---

## License

[ISC](LICENSE)
