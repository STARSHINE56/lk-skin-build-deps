XC换肤 构建依赖
=================

本仓库只放 **XC换肤（LK 2.4.0 改名版）** 构建时需要的第三方二进制，
因为体积过大（共 ~110 MB 解压后）不适合塞进工程仓库。

下载：见 [Releases](../../releases) 页面的 `v1`。

| 附件 | 解压到 | 内容 | sha256 |
|---|---|---|---|
| `blobs_so.tar.gz` | `lib/arm64-v8a/` | libclash.so / liblkengine.so / libc++_shared.so | 见 Release 说明 |
| `blobs_skins.tar.gz` | `assets/` | lk-skins（10,925 个 webp 缩略图） | 见 Release 说明 |

## 用法

```bash
mkdir xc-build && cd xc-build
git clone https://github.com/STARSHINE56/lk-skin-rebuild.git src
cd src

curl -L -o /tmp/so.tar.gz     https://github.com/STARSHINE56/lk-skin-build-deps/releases/download/v1/blobs_so.tar.gz
curl -L -o /tmp/skins.tar.gz  https://github.com/STARSHINE56/lk-skin-build-deps/releases/download/v1/blobs_skins.tar.gz

tar -xzf /tmp/so.tar.gz    -C lib/arm64-v8a/
tar -xzf /tmp/skins.tar.gz -C assets/

apktool b . -o unsigned.apk --use-aapt2
zipalign -f -p 4 unsigned.apk aligned.apk
apksigner sign --ks release.jks --out ../../XC换肤.apk aligned.apk
```

## 说明

这些文件不是我的产出，是从原 APK 中原样提取的（`lib/arm64-v8a/` 与 `assets/lk-skins/`）。
放这里只是为了让构建流程能一键跑通，不构成任何授权或分发承诺。
