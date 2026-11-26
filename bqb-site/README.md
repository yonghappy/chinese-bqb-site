# chinese-bqb-site

Sotaku 表情包站（sticker.sotaku.com）的部署仓库。

基于 [zhaoolee/ChineseBQB](https://github.com/zhaoolee/ChineseBQB) 官方 Hugo 站构建，改动：

- 站点品牌 Sotaku 化（标题、favicon、侧栏品牌）
- 去除页面上的 GitHub 链接（侧栏 GitHub 入口、v2fy 旧版页链接等）
- 图片不进部署包：原图通过 jsDelivr CDN 引用上游仓库，缩略图构建时生成并自托管
- 分类打包下载改为纯浏览器端打包（zip.js，官方自带能力），不使用 GitHub Releases
- 注入 GTM-KXR2XR 统计

## 部署

push 到 `main` 自动触发 `.github/workflows/deploy.yml`：
克隆上游仓库 → 应用本仓库的 Hugo 配置与模板 → `build_site.py` 生成 → Hugo 构建 → `wrangler pages deploy` 到 Cloudflare Pages 项目 `sticker`。

## 本地结构

- `hugo.toml` — 站点配置（baseURL=sticker.sotaku.com）
- `site/` — Hugo 模板与静态资源（改自上游）
- `scripts/build_site.py` — 上游生成脚本 + CDN 化补丁
