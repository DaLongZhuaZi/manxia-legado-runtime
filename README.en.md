# ManXia Legado Runtime Assets

[中文](README.md)

This repository hosts static WebView runtime assets for ManXia's Legado compatibility layer.

It only provides runtime HTML, JavaScript, and Rhino sandbox assets. It does not provide any book source and does not contain third-party source rules.

## Default App URL

```text
https://raw.githubusercontent.com/DaLongZhuaZi/manxia-legado-runtime/master/index.main.json
```

## Layout

```text
index.main.json
legado_runtime.html
rhino_sandbox/
```

## Runtime Install Flow

ManXia installs runtime assets with the following flow:

1. Download `index.main.json`.
2. Download files declared in `files[]` into `staging`.
3. Validate paths, file sizes, and SHA-256 hashes.
4. Check that `legado_runtime.html` contains `__manxiaLegadoRuntimeExecute`.
5. Switch the verified package to `active`.
6. Keep the old `active` runtime and fall back to bundled rawfile assets when validation fails.

## Index Format

```json
{
  "schemaVersion": "1.0.0",
  "runtimeApi": 1,
  "code": 1,
  "version": "0.1.0",
  "minAppVersionCode": 0,
  "entry": "legado_runtime.html",
  "files": []
}
```

Each file item must include:

```json
{
  "path": "legado_runtime.html",
  "url": "legado_runtime.html",
  "sha256": "<file sha256>",
  "size": 0,
  "mimeType": "text/html",
  "required": true
}
```

After changing any runtime file, update `code`, `version`, and the changed file's `sha256` and `size`.

