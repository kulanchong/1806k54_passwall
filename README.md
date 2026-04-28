# ImmortalWrt 18.06-k5.4 PassWall SDK 自动编译

这个仓库提供一套 GitHub Actions 工作流，用来基于 ImmortalWrt SDK 自动编译 `PassWall` 插件包。

当前默认 SDK：

```text
https://downloads.immortalwrt.org/releases/18.06-k5.4-SNAPSHOT/targets/sunxi/cortexa53/immortalwrt-sdk-18.06-k5.4-SNAPSHOT-sunxi-cortexa53_gcc-8.4.0_musl.Linux-x86_64.tar.xz
```

目标平台和包架构：

```text
sunxi/cortexa53
aarch64_cortex-a53
```

## 已做好的内容

- 自动下载并解压 `sunxi/cortexa53` SDK
- 自动添加 `Openwrt-Passwall/openwrt-passwall` 和 `openwrt-passwall-packages` feed
- 自动执行 `feeds update/install`
- 自动编译选中的 PassWall 软件包
- 自动上传 SDK 产出的 `ipk` 构件

## 配置

默认配置在 `build/passwall.env`：

```bash
SDK_URL="https://downloads.immortalwrt.org/releases/18.06-k5.4-SNAPSHOT/targets/sunxi/cortexa53/immortalwrt-sdk-18.06-k5.4-SNAPSHOT-sunxi-cortexa53_gcc-8.4.0_musl.Linux-x86_64.tar.xz"
PASSWALL_PACKAGES="luci-app-passwall luci-i18n-passwall-zh-cn xray-core"
```

## 默认编译的包

默认包列表在 `build/passwall.env` 里：

```bash
PASSWALL_PACKAGES="luci-app-passwall luci-i18n-passwall-zh-cn xray-core"
```

你可以按需增加，比如：

```bash
PASSWALL_PACKAGES="luci-app-passwall luci-i18n-passwall-zh-cn xray-core sing-box hysteria2"
```

## 触发方式

### 方式 1：推送到 `main`

当你修改下面文件并推送到 `main` 时，会自动触发：

- `.github/workflows/build-passwall.yml`
- `build/passwall.env`

### 方式 2：手动运行

进入 GitHub 仓库的 `Actions` 页面，选择 `Build PassWall with ImmortalWrt SDK`，然后点击 `Run workflow`。

你也可以在手动运行时直接填写：

- `sdk_url`
- `passwall_packages`

手动输入的值会覆盖 `build/passwall.env` 里的默认值。

## 产物位置

编译完成后，到 Actions 的 Artifacts 下载：

```text
passwall-sdk-sunxi-cortexa53-aarch64_cortex-a53
```
