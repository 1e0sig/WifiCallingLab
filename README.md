# WifiCallingLab
WFC Control for Android and Magisk

## Magisk / Shizuku 整合预览版 0.6.0-preview.2

[下载整合版 APK、Magisk 模块及源码](https://github.com/1e0sig/WifiCallingLab/releases/tag/v0.6.0-preview.2)

同一个 WFC Control 应用内可选择 Magisk 或 Shizuku。**整合版和模式切换未经真机验证。** 旧 Magisk 版仅在 Redmi Note 12 Turbo（marble）、江南 4.0.5、Android 17、Magisk 31.1、VOXI 单实体 SIM 环境验证过。Shizuku 模式的 IMS 注册和卡槽复原仍待验证。

### 安装与切换

1. **免 root 使用**。安装发布页的 APK，在 Android 12 或更高版本通过无线调试配对并启动 Shizuku 13+。打开 WFC Control，选「Shizuku（无线调试）」，点「连接 Shizuku」并授权。手机重启后需再次启动 Shizuku。[Shizuku 操作指南](https://shizuku.rikka.app/guide/setup/)
2. **Magisk 使用或从 0.5.7 升级**。在 Magisk 31.0 或更高版本安装发布页的模块 ZIP，重启手机。模块内含同一个 APK。首次按模块方式安装时默认进入 Magisk，按提示授予电话及 root 权限。原 Magisk 版沿用相同包名和签名。
3. **Magisk → Shizuku**。进入右上角「⋯」→「运行模式 · Magisk」→「切换」。应用会检查卡槽并关闭 Magisk 后台自动恢复。若有进行中的 SIM 操作，等它结束后重试。若提示映射待恢复，先点「恢复原卡槽映射」。
4. **Shizuku → Magisk**。点击「切换到 Magisk 模式」。如有待恢复映射，先点「恢复原卡槽」。如尚未安装模块，按第 2 步操作。应用会记住成功选择的模式。切回后可在 Magisk 工具页按需重新开启后台自动恢复。
5. **连接 WFC**。在已验证的使用环境中，保持飞行模式开启、移动数据关闭，连接支持 WFC 的 Wi-Fi 并结束通话。点当前模式的连接按钮。Shizuku 模式下若仍未确认连接，可在只插一张实体 SIM 的双实体卡槽设备上点「尝试切换 SIM 卡槽」。请等待原卡槽复原，并以应用确认 Wi-Fi 注册和语音可用为准。

原独立 ADB 预览版使用另一个包名。如果它提示有待恢复映射，请先在旧应用恢复，再改用整合版。后台自动重连需要 Magisk。已安装的独立 LSPosed 体验优化模块由 LSPosed 管理。

## 已验证的使用环境

- 手机与 ROM：Redmi Note 12 Turbo（marble），江南官改 ROM 4.0.5，实机报告 Android 17（API 37）。
- 模块环境：WFC Control 0.5.7 使用 Magisk 31.1。体验优化 APK 0.2.0 使用 LSPosed 2.2.1。
- 网络与 SIM：连接 Wi-Fi、开启飞行模式、关闭移动数据，只插一张实体 SIM。
- **运营商仅在 VOXI 上实测可用。** 其他运营商、机型和 ROM 的兼容性尚未验证。

## WFC Control ADB 0.1.0 · 实验预览

**未经真机验证。** Redmi Note 12 Turbo（marble）／江南 4.0.5／Android 17／VOXI 是计划验证的环境。现有 Magisk 版曾在这套环境验证，免 root 版的 IMS 状态读取、启用、切槽和复原都还需要真机确认。

这个 APK 通过无线调试启动的 Shizuku 使用 ADB 的 `shell` 身份。支持手动查看状态和尝试连接 Wi-Fi Calling。后台自动重连、LSPosed 体验优化和小米 SIM 激活短信拦截目前仅在原版提供。

### 操作流程

1. 在 Android 12 或更新版本安装 [Shizuku 13+](https://shizuku.rikka.app/download/) 和[预发布页](https://github.com/1e0sig/WifiCallingLab/releases/tag/adb-v0.1.0-preview)的 `WFC-Control-ADB-0.1.0-preview.apk`。
2. 连接 Wi-Fi。在开发者选项开启「无线调试」，按 [Shizuku 启动指南](https://shizuku.rikka.app/guide/setup/#start-via-wireless-debugging) 完成配对并启动。确认 Shizuku 显示正在运行。手机重启后需再次启动 Shizuku。
3. 保留一张活动实体 SIM，开启飞行模式，确认移动数据关闭，并确认 Wi-Fi 仍连接。先结束正在进行的通话。
4. 打开 WFC Control ADB，点「连接 Shizuku」并授权。如果显示「Wi-Fi Calling 已连接」，状态已满足 Wi-Fi IMS 注册、语音能力及系统 WFC 可用三项检查。
5. 未连接时点「连接 Wi-Fi Calling」，等待 IMS 注册。如果仍未连接，并且手机有两个可拆卸实体卡槽、只插了一张卡，可以点「尝试切换 SIM 卡槽」。这会短暂切断 SIM 服务，随后尝试恢复原卡槽并重新核验 WFC。
6. 如果界面提示卡槽恢复待确认，保持 SIM 原样、飞行模式开启，重新连上 Shizuku 后点「恢复原卡槽」。恢复确认前请保留 APK 及应用数据，其中保存了原始映射。

首次试用建议避开依赖通话的时段。若试用时设备已运行 Magisk 版，请先在原版关闭后台自动重连，避免两个程序同时切槽。
