# Flow

一款基于 [halo-theme-ethereal](https://github.com/AloneNanNan/halo-theme-ethereal) 二次开发，为 Halo 打造的 Fuwari 风格增强型主题。

[![Halo](https://img.shields.io/badge/Halo-%3E%3D2.25.0-blue)](https://www.halo.run/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

作者：[Akagi_Zen](https://github.com/fhfzfy1231)

适用于 Halo 2.25.0 及以上版本。

## 界面预览

<p align="center">
  <img src="./screenshot/home.png" alt="Flow 主题预览" width="800" />
</p>

## 功能

- 三栏 / 两栏自由布局，右侧栏无组件时自动收列为两栏
- 导航栏磨砂玻璃模糊效果，支持全屏透明壁纸背景
- Banner 支持关闭 / 横幅 / 全屏 / 全屏透明多种形态，可配置图片、视频或多图轮播
- 丰富的侧边栏小组件：公告、个人简介、天气、音乐播放器、一言、站点统计、分类 / 标签导航、热门文章、目录等
- 图片 CDN / 对象存储实时压缩，降低封面与正文图片加载体积
- 自定义主题色，访客可前台实时切换主题色相、列表 / 网格布局与卡片样式
- 前台简体中文 / 繁體中文 / English 三语实时切换
- 分享海报与赞赏、自定义字体、外链跳转模态框、页面过渡动画
- 内置时间轴、技能、朋友圈、心愿便签等页面模板

## 页面支持

- [x] 首页、文章页、归档、标签 / 分类列表与详情
- [x] 图库、瞬间、友情链接、朋友圈、装备、项目作品集、心愿便签、日程日历、追番
- [x] 自定义页面、404 错误页

## 插件支持

主题与以下 Halo 插件深度集成，建议搭配使用以获得完整体验：

| 插件             | 功能                         |
| ---------------- | ---------------------------- |
| 搜索插件         | 文章全文搜索                 |
| 评论插件         | 文章评论系统                 |
| 瞬间插件         | 瞬间 / 说说功能              |
| 图库插件         | 图库展示                     |
| 链接管理插件     | 友情链接管理 & 朋友圈 & 友链 |
| 装备管理         | 装备展示                     |
| 项目集           | 项目作品集展示               |
| 心愿便签         | 心愿墙便签发布与展示         |
| 日程日历         | 日程 / 日历展示              |
| Bilibili Bangumi | 追番 / 追剧展示页面          |

## 安装

前往 [Releases](https://github.com/fhfzfy1231/Halo-Theme-Flow/releases) 下载最新版本主题包（`.zip`），在「Halo 后台 → 主题 → 安装」中上传主题包即可使用。

## 本地构建

环境要求：Node.js >= 22.12.0（推荐 24.x，见 `.nvmrc`）、pnpm。

```bash
git clone https://github.com/fhfzfy1231/Halo-Theme-Flow.git
cd Halo-Theme-Flow

# 安装依赖
pnpm install

# 开发模式（监听文件变更自动重建）
pnpm dev

# 构建主题
pnpm build

# 构建并打包为主题安装包
pnpm build:pkg
```

## 致谢

- [Halo](https://halo.run) — 优秀的 Java 博客系统
- [halo-theme-ethereal](https://github.com/AloneNanNan/halo-theme-ethereal) — 上游主题
- [halo-theme-fuwari](https://github.com/jiewenhuang/halo-theme-fuwari) — 原始 Fuwari 移植主题，MIT 许可
- [Fuwari](https://github.com/saicaca/fuwari) — 原始 Astro 主题，MIT 许可

## 许可

[MIT License](./LICENSE) © Akagi_Zen

本主题基于 [halo-theme-ethereal](https://github.com/AloneNanNan/halo-theme-ethereal)（MIT 许可）二次开发，遵守原始许可证条款。
