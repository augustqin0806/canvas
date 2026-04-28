# 个人信息定制指南

本项目是 Canvas Portfolio 模板，包含原作者 Hugo Richard 的个人信息。使用前**必须**将所有个人信息替换为你自己的。以下是完整的替换清单。

---

## 1. 核心配置文件（必改）

### `app/app.config.ts`

这是最重要的配置文件，包含绝大部分个人信息：

```ts
export default defineAppConfig({
  global: {
    meetingLink: 'https://cal.com/hugorcd/15min',    // → 你的预约会议链接
    available: true,                                   // → 你的可接单状态
  },
  profile: {
    name: 'Hugo Richard',                              // → 你的姓名
    job: 'Frontend Architect and Designer',            // → 你的职位/头衔
    email: 'contact@hrcd.fr',                          // → 你的邮箱
    phone: '(+33) 6 21 56 22 18',                      // → 你的电话
    picture: 'https://avatars.githubusercontent.com/u/71938701?v=4',  // → 你的头像 URL
  },
  socials: {
    github: 'https://github.com/HugoRCD',              // → 你的 GitHub 主页
    twitter: 'https://twitter.com/HugoRCD__',          // → 你的 Twitter 主页
    linkedin: 'https://www.linkedin.com/in/hugo-richard-0801',  // → 你的 LinkedIn 主页
    instagram: 'https://www.instagram.com/hugo.rcd_',  // → 你的 Instagram 主页
    spotify: 'https://open.spotify.com/user/...',      // → 你的 Spotify 主页（可选）
  },
  seo: {
    title: 'Canvas a Nuxt portfolio template',         // → 你的网站标题
    description: 'Canvas is a simple...',              // → 你的网站描述
    url: 'https://canvas.hrcd.fr',                     // → 你的网站 URL
  },
})
```

---

## 2. Nuxt 配置文件

### `nuxt.config.ts`

需要修改以下字段：

| 字段 | 当前值 | 说明 |
|---|---|---|
| `site.url` | `https://canvas.hrcd.fr` | → 你的网站域名 |
| `studio.repository.owner` | `HugoRCD` | → 你的 GitHub 用户名 |
| `studio.repository.repo` | `canvas` | → 你的仓库名 |
| `studio.repository.branch` | `main` | → 你的主分支名 |

### `nuxt.schema.ts`

此文件定义 Nuxt Studio 可编辑字段的默认值，需同步修改：

| 字段 | 当前默认值 |
|---|---|
| `profile.name` | `Hugo Richard` |
| `profile.job` | `Front-end developer` |
| `profile.email` | `contact@hrcd.fr` |
| `profile.phone` | `(+33) 6 21 56 22 18` |
| `profile.picture` | `https://avatars.githubusercontent.com/u/71938701?v=4` |

---

## 3. 邮件服务

### `server/emails/send.ts`

修改邮件发送的 `from` 和 `to` 地址：

```ts
// 当前值
from: 'HR Folio <contact@hrcd.fr>',    // → '你的名字 <你的邮箱>'
to: ['contact@hrcd.fr'],               // → ['你的接收邮箱']
subject: 'Nouveau message de HR Folio', // → 邮件主题（建议改为英文或你的语言）
```

HTML 模板中的法语文本也应替换为你的语言：

```html
<p>Un nouveau message a été envoyé depuis le formulaire de contact de HR Folio.</p>
<!-- → 替换为你的语言，如 "A new message has been sent from the contact form." -->
```

---

## 4. 布局组件

### `app/components/layout/Footer.vue`

修改页脚链接和名称：

```html
<!-- 当前值 -->
<ULink to="https://dub.sh/hrcd">HugoRCD</ULink>
<!-- → 替换为你的链接和名称，如 -->
<ULink to="https://yourwebsite.com">YourName</ULink>
```

---

## 5. 内容文件

### `content/en/` 和 `content/fr/` 目录

所有 Markdown 和 JSON 内容文件都包含原作者的信息，需逐一替换：

| 文件 | 需修改内容 |
|---|---|
| `content/en/4.about.md` | 关于页的个人介绍、工作经历 |
| `content/fr/4.about.md` | 法语版关于页（如不需要法语可删除 `content/fr/` 目录） |
| `content/en/projects/*.json` | 项目数据（标题、描述、链接、图片） |
| `content/fr/projects/*.json` | 法语版项目数据 |
| `content/en/articles/*.md` | 文章内容 |
| `content/fr/articles/*.md` | 法语版文章内容 |
| `content/en/faq.json` | FAQ 数据 |
| `content/fr/faq.json` | 法语版 FAQ |
| `content/stack.json` | 技术栈展示数据 |

---

## 6. 静态资源

### `public/` 目录

| 文件 | 说明 |
|---|---|
| `public/og.png` | Open Graph 分享图片，替换为你的品牌图片 |
| `public/favicon.ico` | 网站图标 |
| `public/favicon-16x16.png` | 16x16 favicon |
| `public/favicon-32x32.png` | 32x32 favicon |
| `public/apple-touch-icon.png` | Apple 设备图标 |
| `public/android-chrome-192x192.png` | Android 192x192 图标 |
| `public/android-chrome-512x512.png` | Android 512x512 图标 |
| `public/site.webmanifest` | PWA manifest（名称、颜色等） |
| `public/assets/hr-sign-*.svg` | 签名 SVG（关于页使用） |
| `public/projects/*.webp` | 项目图片 |
| `public/articles/*` | 文章图片 |

---

## 7. 包管理与 CI/CD

### `package.json`

| 字段 | 当前值 | 说明 |
|---|---|---|
| `name` | `canvas-template` | → 你的项目名 |
| `author` | `HugoRCD` | → 你的名字 |

### `docker-compose.community.yml`

当前引用 `ghcr.io/hugorcd/canvas:latest`，如使用 Docker 部署需替换为你自己的镜像地址。

### `.github/workflows/build-image.yml`

Docker 镜像构建工作流，如 fork 后使用需更新镜像名称。

### `renovate.json`

当前 `extends` 引用 `local>HugoRCD/renovate-config`，如不使用原作者的 Renovate 配置需修改或删除。

---

## 8. 环境变量

### `.env` 文件（从 `.env.example` 复制）

| 变量 | 说明 |
|---|---|
| `NUXT_PRIVATE_RESEND_API_KEY` | Resend 邮件 API Key |
| `STUDIO_GITHUB_CLIENT_ID` | Nuxt Studio GitHub OAuth Client ID |
| `STUDIO_GITHUB_CLIENT_SECRET` | Nuxt Studio GitHub OAuth Client Secret |

---

## 9. 国际化（可选）

如不需要法语支持：

1. 删除 `content/fr/` 目录
2. 删除 `i18n/locales/fr/` 目录
3. 在 `nuxt.config.ts` 的 `i18n.locales` 中移除法语配置
4. 在 `nuxt.config.ts` 的 `nitro.prerender.routes` 中移除 `/fr`
5. 将 `i18n.strategy` 改为 `'no_prefix'`（如仅保留一种语言）

如需添加中文：

1. 在 `nuxt.config.ts` 添加 `{ code: 'zh', name: 'Chinese', language: 'zh-CN' }`
2. 创建 `content/zh/` 目录，翻译所有内容文件
3. 创建 `i18n/locales/zh/` 目录，添加 UI 翻译文件

---

## 快速替换检查清单

- [ ] `app/app.config.ts` – 个人信息、社交链接、SEO
- [ ] `nuxt.config.ts` – 网站 URL、Studio 仓库配置
- [ ] `nuxt.schema.ts` – Studio 默认值
- [ ] `server/emails/send.ts` – 邮件地址
- [ ] `app/components/layout/Footer.vue` – 页脚链接
- [ ] `content/*/` – 所有内容文件
- [ ] `public/` – 所有图片和图标资源
- [ ] `package.json` – 项目名和作者
- [ ] `.env` – 环境变量
- [ ] Docker / CI 配置（如需使用）
