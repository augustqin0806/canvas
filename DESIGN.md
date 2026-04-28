# 设计与样式规范 (DESIGN.md)

本文档定义 Canvas Portfolio 的设计系统、样式规范和组件开发约定。

---

## 1. 设计系统概览

### 设计理念

- **极简专业**：干净、优雅、留白充足，突出内容
- **暗色优先**：默认暗色模式，亮色模式为辅助
- **响应式优先**：Mobile-first 设计，适配所有设备
- **性能导向**：动画尊重 `prefers-reduced-motion`，图片使用 WebP 格式

### 核心 UI 框架

| 框架 | 版本 | 用途 |
|---|---|---|
| Nuxt UI | v4 | 组件库（基于 Reka UI + Tailwind CSS） |
| Tailwind CSS | v4 | 原子化 CSS 框架 |
| Reka UI | - | 无头 UI 原语（Nuxt UI 底层） |

---

## 2. 颜色系统

### 主题色配置

在 `app/app.config.ts` 中配置：

```ts
ui: {
  colors: {
    primary: 'emerald',    // 主色调：翡翠绿
    neutral: 'neutral',    // 中性色调
  },
}
```

### 语义化颜色变量

在 `app/assets/style/main.css` 的 `@theme` 块中定义，所有组件通过 CSS 变量引用：

| CSS 变量 | 用途 | 暗色模式值 |
|---|---|---|
| `--color-main` | 主背景 | `var(--ui-bg)` → `#0a0a0a` |
| `--color-secondary` | 次背景 | `#282828` |
| `--color-card` | 卡片背景 | `#282828` |
| `--color-card-hover` | 卡片悬停背景 | `#343434` |
| `--color-primary` | 主文字 | `#ededed` |
| `--color-muted` | 次文字/辅助文字 | `#808080` |
| `--color-inverted` | 反转文字 | `#282828` |
| `--color-border-primary` | 主边框 | `#2E2E2E` |
| `--color-border-primary-hover` | 边框悬停 | `#3E3E3E` |
| `--color-border-muted` | 次边框 | `#1C1822` |
| `--color-placeholder` | 占位符文字 | `#707070` |

### 暗色模式

- 通过 `html.dark` 选择器覆盖 CSS 变量值
- 默认偏好：`dark`（在 `nuxt.config.ts` 的 `colorMode` 中配置）
- 使用 `@nuxt/ui` 的 `useColorMode` 切换

### 颜色使用规范

1. **必须**使用语义化 CSS 变量（如 `var(--color-primary)`），而非硬编码颜色值
2. **禁止**在组件中直接使用 Tailwind 的颜色类（如 `text-gray-500`），应使用语义类（如 `text-muted`）
3. 新增颜色必须先在 `@theme` 块中定义 CSS 变量
4. 暗色/亮色模式差异通过 CSS 变量切换实现，不使用条件类名

---

## 3. 字体系统

### 字体定义

在 `app/assets/style/main.css` 中声明：

```css
@theme {
  --font-newsreader: "Newsreader", serif;    // 衬线字体（展示用）
  --font-geist: "Geist", sans-serif;         // 无衬线字体（UI 用）
}
```

### 字体使用规范

| 字体 | 用途 | Tailwind 类 |
|---|---|---|
| Geist | 正文、按钮、导航、表单等 UI 元素 | `font-geist`（默认） |
| Newsreader | 标题、引用、签名等展示文字 | `font-newsreader` |

- Geist 是 Nuxt UI 的默认字体，无需显式指定
- Newsreader 仅用于需要衬线效果的展示场景

---

## 4. 布局规范

### 最大宽度

- 内容区最大宽度：`max-w-7xl`（80rem / 1280px）
- 居中布局：`mx-auto`

### 间距系统

使用 Tailwind 默认间距比例（4px 基数）：

| Token | 值 | 常用场景 |
|---|---|---|
| `1` | 4px | 图标与文字间距 |
| `2` | 8px | 紧凑元素间距 |
| `3` | 12px | - |
| `4` | 16px | 组件内间距 |
| `6` | 24px | 区块间距 |
| `8` | 32px | 区块间大间距 |
| `12` | 48px | 页面段落间距 |
| `20` | 80px | 大型留白 |

### 响应式断点

使用 Tailwind 默认断点：

| 断点 | 宽度 | 常用前缀 |
|---|---|---|
| `sm` | ≥640px | `sm:grid-cols-2` |
| `md` | ≥768px | `md:flex-row` |
| `lg` | ≥1024px | `lg:grid-cols-3` |
| `xl` | ≥1280px | `xl:max-w-7xl` |

### 页面结构

```
┌─────────────────────────────────────┐
│              Navbar                  │
├─────────────────────────────────────┤
│                                     │
│          Content Area               │
│        (max-w-7xl mx-auto)          │
│                                     │
├─────────────────────────────────────┤
│              Footer                  │
└─────────────────────────────────────┘
```

---

## 5. 组件设计规范

### 组件架构

组件按职责分层：

```
components/
├── content/          # 页面级内容组件（通过 MDC 引用）
├── home/             # 首页子组件
├── about/            # 关于页子组件
├── layout/           # 布局组件（Navbar, Footer, ScrollToTop）
├── project/          # 项目展示组件
├── settings/         # 功能设置组件
└── *.vue             # 通用组件（SpotlightCard, Divider 等）
```

### 组件命名规范

| 类型 | 命名规则 | 示例 |
|---|---|---|
| 页面内容组件 | PascalCase | `Home.vue`, `Works.vue`, `About.vue` |
| 子组件 | PascalCase | `ProfilePicture.vue`, `Faq.vue` |
| 通用组件 | PascalCase | `SpotlightCard.vue`, `Divider.vue` |
| 布局组件 | PascalCase | `Navbar.vue`, `Footer.vue` |

> 注意：项目已通过 ESLint 关闭 `vue/multi-word-component-names` 规则，允许单词组件名。

### 组件样式约定

1. **使用 Tailwind 工具类**：所有样式通过 Tailwind 类实现，不使用 `<style>` 块或 scoped CSS
2. **语义化类名**：使用 `text-muted`、`text-primary`、`bg-card` 等语义化类
3. **响应式**：使用 Tailwind 响应式前缀（`sm:`, `md:`, `lg:`）
4. **Nuxt UI 组件**：优先使用 Nuxt UI 组件（`UButton`, `UInput`, `UForm` 等），通过 `app.config.ts` 统一定制默认样式

### Spotlight 效果

`SpotlightCard.vue` 和 `SpotlightButton.vue` 提供鼠标追踪的聚光灯效果：

- 基于 `@vueuse/core` 的 `useMouse` 实时追踪鼠标位置
- 通过 CSS `radial-gradient` 实现光晕
- 用于项目卡片和主要操作按钮

---

## 6. 动画系统

定义在 `app/assets/style/animation.css` 中。

### 入场动画

使用 `data-animate` 属性驱动，支持交错延迟：

```html
<div data-animate>首次可见时淡入上移</div>
<div data-animate style="--stagger: 1">延迟 1 个周期</div>
<div data-animate style="--stagger: 2">延迟 2 个周期</div>
```

| CSS 变量 | 默认值 | 说明 |
|---|---|---|
| `--stagger` | `0` | 交错序号 |
| `--delay` | `180ms` | 每个交错周期时长 |
| `--start` | `0ms` | 额外起始延迟 |

### 无障碍：减少动画

```css
@media (prefers-reduced-motion: no-preference) {
  [data-animate] {
    animation: enter 0.6s both;
    animation-delay: calc(var(--stagger) * var(--delay) + var(--start));
  }
}
```

用户开启「减少动画」系统设置时，入场动画自动禁用。

也可通过 `data-animation-controller="false"` 手动关闭子元素动画。

### Vue 过渡动画

| 名称 | 效果 | 用途 |
|---|---|---|
| `list` | 淡入上移 + 位置移动 | TransitionGroup 列表动画（如标签切换） |
| `fade` | 简单淡入淡出 | 条件渲染过渡 |

### 签名动画

`.signature` 类实现 SVG 路径描边动画（stroke-dasharray → stroke-dashoffset），用于关于页签名展示。

### 动画使用规范

1. 列表过渡使用 `<TransitionGroup name="list">`
2. 条件显示使用 `<Transition name="fade">`
3. 入场动画使用 `data-animate` + `--stagger`
4. **禁止**使用 `!important` 覆盖动画
5. 确保动画在 `prefers-reduced-motion: reduce` 下优雅降级

---

## 7. 图标系统

### 图标来源

| 来源 | 前缀 | 说明 |
|---|---|---|
| Iconify (lucide) | `lucide:` | 主要图标集，如 `lucide:github` |
| 自定义 SVG | `custom:` | 项目专属图标，存放在 `app/assets/icons/` |

### 自定义图标

在 `app/assets/icons/` 目录添加 SVG 文件，通过 `custom:` 前缀引用：

```html
<UIcon name="custom:my-icon" />
```

配置在 `nuxt.config.ts` 的 `icon.customCollections` 中。

### 图标使用规范

1. 优先使用 `lucide` 图标集
2. 特定品牌或项目图标使用 `custom` 集合
3. 图标尺寸通过 `size` prop 或 Tailwind 类控制
4. 保持 SVG 图标的 `viewBox` 一致性

---

## 8. 暗色/亮色模式

### 实现方式

- 使用 `@nuxt/ui` 的 `useColorMode()` 组合式函数
- CSS 变量在 `html.dark` 选择器下覆盖
- 偏好持久化到 localStorage

### 切换组件

`app/components/settings/LanguageToggle.vue` 提供语言切换，暗色切换由 Nuxt UI 内置支持。

### 开发规范

1. 所有颜色必须通过 CSS 变量或语义化 Tailwind 类引用
2. 测试新组件时**必须**同时验证暗色和亮色模式
3. 图片资源需同时提供暗色/亮色版本（如 `hr-sign-dark.svg` / `hr-sign-light.svg`）

---

## 9. 自定义 CSS 类

定义在 `app/assets/style/main.css` 的 `@layer components` 中：

| 类名 | 效果 | 用途 |
|---|---|---|
| `.linebreak` | 渐变分隔线 | 区块间的视觉分隔 |
| `.text-white-shadow` | 文字光晕阴影 | 标题特效文字 |

### 自定义滚动条

```css
::-webkit-scrollbar {
  width: 0.5rem;
  padding: 0.5rem;
}
::-webkit-scrollbar-thumb {
  background: var(--bg-card);
  border-radius: 0.5rem;
}
```

---

## 10. 图片规范

| 规范 | 说明 |
|---|---|
| 格式 | 项目图片使用 **WebP**，图标使用 **SVG** |
| 优化 | 通过 `@nuxt/image` 自动优化和懒加载 |
| 响应式 | 使用 `NuxtImg` 组件，提供 `width`/`height` 避免布局偏移 |
| OG 图片 | `public/og.png` 用于社交分享预览 |
| 项目图片 | 存放于 `public/projects/`，命名与 `content/*/projects/*.json` 对应 |
| 文章图片 | 存放于 `public/articles/`，通过 Markdown 相对路径引用 |

---

## 11. 代码高亮

在 `nuxt.config.ts` 的 `mdc.highlight.theme` 中配置：

- 暗色模式：`github-dark`
- 亮色模式：`github-light`
- 默认：`github-dark`

---

## 12. 通知系统

使用 `vue-sonner` 提供 Toast 通知：

- 位置配置：`app.config.ts` 的 `ui.notifications.position`（默认顶部居中）
- 进度条：自定义透明进度条样式
- 使用方式：直接调用 `toast('消息')` 或 `toast.success('成功')`

---

## 13. 设计检查清单

新增或修改组件时，确保：

- [ ] 颜色使用语义化变量/类，无硬编码色值
- [ ] 暗色和亮色模式均正常显示
- [ ] 响应式：移动端、平板、桌面端布局正确
- [ ] 动画尊重 `prefers-reduced-motion`
- [ ] 图片使用 `NuxtImg` 并提供尺寸属性
- [ ] 遵循 Tailwind 工具类优先，避免 scoped CSS
- [ ] 交互元素有合适的 hover/focus 状态
- [ ] 组件通过 `app.config.ts` 暴露可定制项
