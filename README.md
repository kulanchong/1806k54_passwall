# ImmortalWrt 18.06-k5.4 PassWall 自动编译

这个仓库提供一套 GitHub Actions 工作流，用来基于 `immortalwrt/immortalwrt` 的 `openwrt-18.06-k5.4` 分支自动编译 `PassWall` 插件包。

当前工作流固定筛选的包架构是：

```text
aarch64_cortex-a53
```

## 已做好的内容

- 自动拉取 `immortalwrt/immortalwrt` 的 `openwrt-18.06-k5.4`
- 自动添加 `Openwrt-Passwall/openwrt-passwall` 和 `openwrt-passwall-packages` feed
- 自动执行 `feeds update/install`
- 自动编译 `luci-app-passwall`
- 自动筛选并上传 `aarch64_cortex-a53` 架构的 `ipk`/`apk` 构件

## 你还需要改的地方

编辑 `build/passwall.env`，至少填写这两个参数：

```bash
TARGET_BOARD_DEFAULT=你的 target
TARGET_SUBTARGET_DEFAULT=你的 subtarget
```

注意：`aarch64_cortex-a53` 只是软件包架构，不等于 OpenWrt 的 `target/subtarget`。  
如果只知道 CPU 架构，但不知道设备对应的平台，工作流会直接报错，这是为了避免给你编出错误平台的包。

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

进入 GitHub 仓库的 `Actions` 页面，选择 `Build PassWall for ImmortalWrt 18.06-k5.4`，然后点击 `Run workflow`。

你也可以在手动运行时直接填写：

- `target_board`
- `target_subtarget`
- `target_profile`
- `passwall_packages`

手动输入的值会覆盖 `build/passwall.env` 里的默认值。

## 产物位置

编译完成后，到 Actions 的 Artifacts 下载：

```text
passwall-<target_board>-<target_subtarget>-aarch64_cortex-a53
```

## 建议

如果你告诉我你的具体设备型号，或者直接告诉我它对应的 `TARGET_BOARD` / `TARGET_SUBTARGET`，我可以继续帮你把 `build/passwall.env` 直接填好，做到开箱即用。
