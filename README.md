# WDA ipa 云构建器

在 GitHub Actions 的免费 macOS 云跑机上，从**官方 [appium/WebDriverAgent](https://github.com/appium/WebDriverAgent) 源码**构建未签名 WDA ipa。产物自己构建、来源可查，不含任何第三方改动。

## 使用步骤（全程网页操作，无需装任何工具）

1. 在 GitHub **新建一个公开仓库**（名字随意，如 `wda-builder`），勾选 Public
2. 把本文件夹里的 `.github/workflows/build.yml` 和 `README.md` 上传到仓库（网页端 `Add file → Upload files`，注意保持目录结构：build.yml 必须在 `.github/workflows/` 下）
3. 上传完成后 Actions 会自动开始构建（也可手动：Actions → Build WDA ipa → Run workflow）
4. 等约 5-10 分钟，进入该次运行页面，到底部 **Artifacts** 下载 `WDA-ipa-master`
5. zip 解压得到 **WDA.ipa**（未签名，待下一步自签）

## 构建参数

- `wda_ref`：要构建的 appium/WebDriverAgent 分支或 tag，默认 `master`
- 如果 `master` 构建失败，去 [官方 releases](https://github.com/appium/WebDriverAgent/releases) 找最新的 tag 名填进去重跑

## 下载之后

1. **爱思助手自签**：工具箱 → IPA 签名 → 选 WDA.ipa + 登录你的 Apple ID
   - ⚠️ 签名时**把 Bundle ID 改成唯一值**（如 `你的名字缩写.wda`），默认的 `com.facebook.*` 用免费账号签不上
2. 签好的包装进 iPhone，手机开启 **开发者模式**（设置 → 隐私与安全性 → 开发者模式）
3. 后续（go-ios 隧道 + 端口转发 + 启动 WDA）由 Claude 继续指导

## 注意事项

- 免费 Apple ID 签名 **7 天过期**，过期后 WDA 无法重新启动，需重签重装；付费开发者账号（688 元/年）可一年有效
- WDA ipa 是 **XCTest runner 形态**，装好后不能靠点图标启动，需要电脑端 go-ios 拉起（后续步骤）
- 本仓库构建产物仅用于自己设备的自动化测试用途
