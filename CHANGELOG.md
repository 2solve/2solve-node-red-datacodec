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

## 0.15.0 (2024-10-22)
