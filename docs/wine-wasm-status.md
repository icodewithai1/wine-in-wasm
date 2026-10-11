# Wine → WebAssembly: status

Status: **not built yet.** Nothing in this repo compiles Wine to WASM yet.

## What the Wind app expects

Wind (kept outside this repo) loads the runtime from the gamedumprepo raw URL:

    https://raw.githubusercontent.com/icodewithai1/gamedumprepo/refs/heads/main/wine/manifest.json

The manifest is JSON:

    { "version": "x.y.z", "entry": "wine.js", "files": ["wine.wasm", "wine.data"] }

- Every listed file is downloaded and cached in IndexedDB.
- The entry script is loaded and must set `window.WineRuntime.run({ blob, name, container })`.
- `window.WindWineFiles[name]` gives a blob URL for each part, for use in `locateFile`.

## Remaining work

1. Build Wine (Windows-compat layer) for wasm32 with Emscripten/WASI. Threads, file system and syscall shims are the hard parts.
2. Graphics: WebGPU first, WebGL fallback. Test both.
3. Publish the artifacts and manifest to the gamedumprepo `wine/` folder.
4. Test a few small Windows programs before enabling "Install to Home".
