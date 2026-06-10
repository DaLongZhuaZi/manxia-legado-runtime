# ManXia Legado Runtime

Official Legado WebView runtime asset repository for ManXia.

The application reads:

```text
https://raw.githubusercontent.com/DaLongZhuaZi/manxia-legado-runtime/master/index.main.json
```

## Layout

```text
index.main.json
legado_runtime.html
rhino_sandbox/
```

The runtime manifest is intentionally strict. Every file listed in
`index.main.json` includes a fixed path, byte size, SHA-256 digest, MIME type,
and required flag. The app downloads files into `staging`, validates them, then
switches the verified package into `active`.

When a runtime file changes, increase `code` and `version`, then refresh the
changed file's `sha256` and `size`.

