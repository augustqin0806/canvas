# Canvas Portfolio 模板

Canvas Portfolio 是一个完全可定制的国际化（i18n）个人作品集模板，基于 **Nuxt 4** 和 **Nuxt UI v4** 构建，帮助你轻松展示作品、文章和个人信息。模板集成了 Nuxt Studio 可视化编辑器，并使用 Nuxt Content v3 进行内容管理。

## 在线演示

访问 [canvas.hrcd.fr](https://canvas.hrcd.fr/) 查看在线演示。

---

## 功能特性

- **现代化组件与布局** – 内置丰富的 UI 组件
- **Nuxt UI v4** – 基于 Reka UI 和 Tailwind CSS 的预构建可定制组件
- **Nuxt Studio** – 内置可视化编辑器，直接在浏览器中编辑内容（`/admin`）
- **NuxtHub 就绪** – 几秒钟即可部署到 NuxtHub
- **Tailwind CSS v4** – 美观、响应式的设计系统
- **工作联系表单** – 集成 Resend 邮件服务
- **多语言支持** – 基于 Nuxt i18n（默认支持英语和法语）
- **SEO 就绪** – OG Image、Robots 自动生成、Sitemap 自动生成
- **最佳实践** – 图片优化（Nuxt Image）、ESLint（Flat Config）、TypeScript 严格模式
- **完全响应式** – 适配所有现代浏览器和设备
- **极简专业设计** – 干净、优雅、易于定制

---

## 技术栈

| 层级 | 技术 |
|---|---|
| **框架** | Nuxt 4 (Vue 3) |
| **UI 组件库** | @nuxt/ui v4 (Reka UI + Tailwind CSS) |
| **样式** | Tailwind CSS v4 |
| **内容管理** | @nuxt/content v3 (SQLite) |
| **国际化** | @nuxtjs/i18n (英语 + 法语) |
| **SEO** | @nuxtjs/seo (OG Image, Robots, Sitemap) |
| **图片优化** | @nuxt/image v2 |
| **邮件服务** | Resend |
| **工具库** | @vueuse/core, @vueuse/nuxt |
| **包管理器** | pnpm |
| **类型检查** | TypeScript (strict) |
| **代码规范** | ESLint 9 (Flat Config) |

---

## 项目结构

```
canvas/
├── app/                        # 应用主目录
│   ├── app.config.ts           # 运行时配置（个人信息、社交链接、SEO、UI 颜色）
│   ├── app.vue                 # 根组件
│   ├── assets/                 # 静态资源
│   │   ├── icons/              # 25 个自定义 SVG 图标
│   │   └── style/              # 全局样式（main.css, animation.css）
│   ├── components/             # Vue 组件
│   │   ├── content/            # 页面级组件（Home, Works, Writing, About, Contact）
│   │   ├── home/               # 首页子组件（CTA, Faq, Projects, Social）
│   │   ├── about/              # 关于页子组件（Intro, ProfilePicture, Signature）
│   │   ├── layout/             # 布局组件（Navbar, Footer, ScrollToTop）
│   │   ├── project/            # 项目展示（Card, List）
│   │   └── settings/           # 设置组件（Availability, LanguageToggle, Tools）
│   ├── composables/            # 组合式函数
│   ├── layouts/                # 布局模板
│   ├── pages/                  # 页面路由（基于文件的路由）
│   └── utils/                  # 工具函数
├── content/                    # Nuxt Content 内容目录
│   ├── stack.json              # 技术栈数据
│   ├── en/                     # 英文内容（Markdown 页面 + JSON 数据）
│   │   ├── 1.index.md          # 首页
│   │   ├── 2.works.md          # 作品页
│   │   ├── 3.writing.md        # 文章页
│   │   ├── 4.about.md          # 关于页
│   │   ├── 5.contact.md        # 联系页
│   │   ├── faq.json            # FAQ 数据
│   │   ├── articles/           # 文章 Markdown 文件
│   │   └── projects/           # 项目 JSON 文件
│   └── fr/                     # 法文内容（同结构）
├── i18n/                       # 国际化配置
│   └── locales/                # 各语言 UI 翻译文件
├── public/                     # 公共静态文件（favicon、OG 图片、项目图片等）
├── server/                     # 服务端
│   ├── api/                    # API 路由
│   ├── emails/                 # 邮件发送（Resend）
│   └── routes/                 # 服务端路由（sitemap）
├── nuxt.config.ts              # Nuxt 核心配置
├── nuxt.schema.ts              # Nuxt Studio 预览 Schema
├── eslint.config.mjs           # ESLint 配置
├── tsconfig.json               # TypeScript 配置
└── package.json                # 项目依赖与脚本
```

---

## 快速开始

### 1. 克隆仓库

```bash
git clone git@github.com:HugoRCD/canvas.git
cd canvas
```

### 2. 安装依赖

```bash
pnpm install
```

### 3. 配置环境变量

```bash
cp .env.example .env
```

编辑 `.env` 文件填入你的配置值。

### 4. 启动开发服务器

```bash
pnpm dev
```

访问 [http://localhost:3000](http://localhost:3000) 查看效果。

### 5. 构建与部署

```bash
# 生成静态站点
pnpm generate

# 或构建生产版本
pnpm build

# 启动生产服务器
pnpm start
```

---

## 常用脚本

| 命令 | 说明 |
|---|---|
| `pnpm dev` | 启动开发服务器 |
| `pnpm build` | 构建生产版本 |
| `pnpm generate` | 生成静态站点 |
| `pnpm preview` | 预览生产构建 |
| `pnpm start` | 启动生产服务器 |
| `pnpm lint` | 运行 ESLint 检查 |
| `pnpm lint:fix` | 运行 ESLint 自动修复 |
| `pnpm typecheck` | 运行 TypeScript 类型检查 |

---

## 内容编辑

本项目使用 [Nuxt Content v3](https://content.nuxt.com/) 管理所有内容。

### 核心配置

首先修改 `app/app.config.ts`，这是全局配置文件，包含个人信息、社交链接、SEO 设置和 UI 颜色配置。

### 页面内容

- **首页 / 作品 / 文章 / 关于 / 联系**：编辑 `content/{locale}/` 下的对应 Markdown 文件
- **项目数据**：在 `content/{locale}/projects/` 下添加或修改 JSON 文件
- **文章内容**：在 `content/{locale}/articles/` 下添加或修改 Markdown 文件
- **FAQ 数据**：编辑 `content/{locale}/faq.json`
- **技术栈**：编辑 `content/stack.json`

### 特色项目

在项目 JSON 文件中添加 `"featured": true` 可将项目展示在首页。

### Nuxt Studio 可视化编辑

启动开发服务器后访问 `/admin`，可通过可视化界面直接编辑内容。

---

## 国际化

项目默认支持英语（`en`）和法语（`fr`），使用 URL 前缀策略（如 `/en/works`、`/fr/works`）。

### 添加新语言

1. 在 `nuxt.config.ts` 的 `i18n.locales` 中添加新语言配置
2. 在 `content/` 下创建对应语言目录（如 `content/zh/`），复制并翻译所有内容文件
3. 在 `i18n/locales/` 下创建对应语言的 UI 翻译文件
4. 更新 `nuxt.schema.ts` 中的 `lang` 字段 `required` 选项

---

## 联系表单

项目使用 [Resend](https://resend.com/) 处理联系表单邮件发送。若不设置 `NUXT_PRIVATE_RESEND_API_KEY` 环境变量，邮件功能将不会启用。

### 设置步骤

1. 在 [Resend](https://resend.com/api-keys) 获取 API Key
2. 将 API Key 添加到 `.env` 文件
3. 修改 `server/emails/send.ts` 中的 `from` 和 `to` 邮件地址

---

## 部署

### Vercel / Netlify 等 Serverless 平台

Nuxt Content v3 默认使用 SQLite，Serverless 平台不支持 SQLite，需连接外部数据库（PostgreSQL / Turso / D1）。详见 [Nuxt Content Serverless 部署文档](https://content.nuxt.com/docs/deploy/serverless)。

### Docker

```bash
docker pull ghcr.io/hugorcd/canvas:latest
```

也可使用 `docker-compose.local.yml` 或 `docker-compose.community.yml` 快速部署。

---

## 相关文档

- [个人信息定制指南](./PERSONALIZATION.md) – 需要修改哪些文件和字段来替换为你的个人信息
- [设计与样式规范](./DESIGN.md) – 设计系统、颜色、字体、动画、组件规范
- [开发规范与贡献指南](./CONTRIBUTING.md) – 代码风格、提交规范、分支策略、PR 流程

---

## 许可证

[Apache-2.0](./LICENSE)
