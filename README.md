# BbangEditor 编辑器

基于 Electron 的 Markdown 编辑器桌面应用。

## 下载

| 版本 | 平台 | 文件 | 日期 |
|------|------|------|------|
| v0.1.0 | macOS (Apple Silicon) | [BbangEditor-0.1.0-arm64.dmg](https://github.com/JiuYoStar/editor-demo/releases/download/v0.1.0/BbangEditor-0.1.0-arm64.dmg) | 2026-04-20 |

> 注意：当前未配置 Apple Developer ID 代码签名，macOS 首次打开会提示"无法验证开发者"。
> 解决方案：系统设置 → 隐私与安全性 → 仍要打开，或在终端执行：
> ```shell
> xattr -dr com.apple.quarantine /Applications/BbangEditor.app
> ```

## 更新日志

### v0.1.0 (2026-04-20)

首次发布版本，包含以下功能：
- Markdown 编辑器核心功能
- 自动保存功能
- 模式切换功能
- ne-list 折行问题修复
- 屏蔽开发者工具
- Electron 桌面客户端打包

---

## 功能特性

- 支持多种 Markdown 语法
- 实时预览
- 自动保存
- 纯净桌面体验