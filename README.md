# 漫匣 Legado 运行时资产仓库

[English](README.en.md)

这是漫匣 Legado 兼容层的 WebView 运行时静态资产仓库。

本仓库只提供运行时 HTML、JavaScript、Rhino 沙箱等引擎资产，不提供任何书源，也不包含任何第三方内容规则。

## 应用默认读取地址

```text
https://raw.githubusercontent.com/DaLongZhuaZi/manxia-legado-runtime/master/index.main.json
```

## 目录结构

```text
index.main.json
legado_runtime.html
rhino_sandbox/
```

## 运行时安装逻辑

漫匣会按以下顺序安装运行时资产：

1. 下载 `index.main.json`。
2. 将 `files[]` 中声明的文件下载到 `staging`。
3. 校验路径、文件大小和 SHA-256。
4. 检查 `legado_runtime.html` 是否包含 `__manxiaLegadoRuntimeExecute`。
5. 健康检查通过后切换到 `active`。
6. 失败时保留旧版 `active`，并回退到 App 内置 rawfile。

## 索引格式

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

每个文件项必须包含：

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

更新任意运行时文件后，必须同步更新 `code`、`version`、对应文件的 `sha256` 和 `size`。

