# WUJI Paper-to-Web

**Developer: Wenji Li**

WUJI 内部论文转网页设计规范。此仓库为个人私有仓库；未公开发布网页预览。

## 使用入口

- [DESIGN.md](DESIGN.md)：在线阅读核心设计规范。
- [完整规范包](WUJI-Paper-to-Web-v1.0-local-review-20261125.zip)：下载并完整解压后使用，包含 tokens、字体、Logo、SVG 图标与画框、网页白模、开发骨架、流程文档及校验文件。

本次保留已审核的 Local Review 1.0 包作为完整快照。包内有关“尚未创建仓库”的文字描述该快照制作时的状态；当前已上传此私有仓库。在线 DESIGN.md 中涉及包内文件的相对路径，请在完整解压后的目录中使用。

## 本地预览

在解压后的包根目录运行：

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

然后打开 `http://localhost:8000/reference/` 查看规范白模，打开 `http://localhost:8000/starter/` 查看论文网页骨架。停止服务按 Ctrl+C。

先阅读 DESIGN.md，再阅读 docs/content-workflow.md、docs/components.md 和 docs/deployment.md。不要只复制 HTML 而遗漏 CSS、JavaScript、字体和素材目录。

## 资产与使用范围

- 内部使用；不授予对外传播或再分发权限。
- Algorytm 字体保留原有 TRIAL 文件名与状态，不能视为正式字体授权证明。
- 白模为演示状态，生产时需替换真实论文内容、数据、视频与时间映射。
- Logo、交互蓝 #207FFF、4px 画框圆角等以包内规范和 tokens.css 为准。
- 当前没有公开在线预览，也未邀请其他协作者。
