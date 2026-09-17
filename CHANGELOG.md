## Unreleased

### Breaking Changes

#### Package renamed: `node-red-2stools-packetdecode` → `@tosolve/node-red-datacodec`

Uninstall the old package and install the new one:

```bash
cd ~/.node-red
npm uninstall node-red-2stools-packetdecode
npm install @tosolve/node-red-datacodec
```

#### Node type renamed: `2stools-packetdecode` → `2stools-datacodec`

All existing flows that use the `2stools-packetdecode` node **must be updated** manually. After installing the new package:

1. Open your `flows.json` (usually at `~/.node-red/flows.json`)
2. Find all nodes with `"type": "2stools-packetdecode"`
3. Replace with `"type": "2stools-datacodec"`
4. Restart Node-RED

#### Dependency replaced: `2stools-daq` → `@tosolve/datacodec`

The underlying codec library has been replaced with [`@tosolve/datacodec`](https://github.com/2solve/2solve-datacodec). The `packetDecode` function signature is unchanged — no changes to message payloads or node configuration are required.

---

## 0.20.0 (2026-09-17)

### Build

- Bumped `@tosolve/datacodec` to `^0.20.0`.

The underlying codec gained the IOT-NDDI-2602 (NanoDAq) digital input tags, so flows
using this node now decode eight additional keys without any flow change:

| Tag | ID | Meaning |
|---|---|---|
| `EngInp0`..`EngInp3` | 183-186 | Value already converted to engineering units on the device |
| `FreInp2`, `FreInp3` | 187, 188 | Frequency inputs, channels 3 and 4 |
| `IntInp2`, `IntInp3` | 189, 190 | Pulse counters, channels 3 and 4 |

The addition is additive: no existing tag, ID, size or type changed, and the node's
configuration and message contract are unchanged.

Note: the caret range matters here. `^0.19.0` resolves to `>=0.19.0 <0.20.0`, so a
`npm update` alone would never have picked these tags up -- the dependency range had
to be bumped explicitly.

---

## 0.15.0 (2024-10-22)
