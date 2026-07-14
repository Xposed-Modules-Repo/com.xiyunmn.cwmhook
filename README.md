# CWMHook

<a href="https://github.com/Xposed-Modules-Repo/com.xiyunmn.cwmhook/releases/latest"><img alt="GitHub all releases" src="https://img.shields.io/github/downloads/Xposed-Modules-Repo/com.xiyunmn.cwmhook/total?label=Downloads"></a>
<a href="https://github.com/Xposed-Modules-Repo/com.xiyunmn.cwmhook/releases/latest"><img alt="GitHub latest release" src="https://img.shields.io/github/v/release/Xposed-Modules-Repo/com.xiyunmn.cwmhook"></a>

CWMHook 是面向刺猬猫阅读的 Xposed 功能增强模块，基于现代 libxposed API 102 开发。

当前已验证兼容：

```text
刺猬猫阅读 2.9.362 - 2.9.365
com.kuangxiangciweimao.novel
```

## 安装

1. 在支持 libxposed API 102 的 LSPosed 中安装并启用模块。
2. 将作用域设置为刺猬猫阅读。
3. 强制停止并重新启动刺猬猫阅读。
4. 长按书架页或阅读页的“更多”按钮进入模块设置。
5. 在模块设置的“关于”区域连续点击版本号 5 次，可解锁被隐藏的功能。


其它框架即使能加载本模块，也不代表已经完整实现 API 102 热重载；当前经过验证的支持版本为 LSPosed v2.1.0。

## 主要功能

- 优化状态栏背景与日间、夜间页面适配。
- 自定义底栏 Tab 的显示和顺序。
- 隐藏书架继续阅读浮层。
- 设置冷启动默认页面并提供可选启动优化。
- 导入和管理阅读字体。
- 自动签到。
- 将个人已拥有阅读权限或已缓存的章节导出为 TXT/EPUB。
- API 102 热重载。

## 热重载边界

- 自动签到请求、章节导出或宿主章节下载进行中时会拒绝热重载，避免旧代际回调被提前卸载。
- 热重载会关闭模块设置/章节导出窗口、解绑模块监听、清理注入 View、停止模块线程，并重建当前前台 Activity。
- 配置仍保存在宿主本地 `SharedPreferences`，配置保存后按各功能既有机制生效；热重载只用于替换模块代码，不用于同步配置。
- 模块没有手动热重载入口；安装新版 APK 后由 LSPosed 根据 `autoHotReload=true` 自动触发。
- 当前支持 API 102 的框架版本为 LSPosed v2.1.0。

宿主版本更新后，部分功能可能因内部实现变化而失效。遇到异常时请先关闭对应功能，并提供宿主版本、模块版本、复现步骤和详细日志。

## 版权与章节导出说明

章节导出功能仅用于备份用户本人已合法取得阅读权限的内容，供个人临时收藏、离线阅读与数据迁移使用。模块不会绕过购买、订阅或章节权限校验，也不应被用于传播、共享、售卖或制作盗版资源。

导出的内容版权归原作者及相关权利人所有。请在导出后 **24 小时内删除相关文件**；如需长期阅读，请通过官方渠道购买和使用正版内容。用户应自行确保使用行为符合当地法律法规、平台规则和版权许可，因违规使用产生的责任由使用者自行承担。

## 免责声明

本项目仅供学习、技术研究和个人设备功能增强使用，与刺猬猫阅读及其运营方无关。使用 Xposed 模块可能导致宿主异常、功能失效、数据损坏、账号风险或其它不可预期后果，请在使用前自行审查源码并做好数据备份。

## 构建

```powershell
.\gradlew.bat verifyArchitecture
.\gradlew.bat :app:lintDebug :app:assembleDebug :app:assembleBeta :app:assembleRelease
```

构建需要 JDK 17 和 Android SDK Platform 37；应用 `targetSdk` 当前保持 36。

`.github/workflows/` 提供 Debug、Beta 和 Release 三组手动构建任务。Beta/Release 签名需要配置 `KEYSTORE_BASE64`、`KEYSTORE_PASSWORD`、`KEY_ALIAS`、`KEY_PASSWORD` 四个 GitHub Actions Secrets；本地未提供完整签名参数时会生成未签名 APK。

## 开源许可

Copyright (C) 2026 xiyunmn

本项目依据 [GNU General Public License v3.0](LICENSE)（SPDX：`GPL-3.0-only`）开源。分发或修改本项目时必须遵守许可证规定，并向接收者提供对应源代码和相同的许可权利。本许可证不涵盖刺猬猫阅读、导出内容或其他第三方作品；相关权利仍归各自权利人所有。
