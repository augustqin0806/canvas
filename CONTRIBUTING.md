# 开发规范与贡献指南 (CONTRIBUTING.md)

本文档定义 Canvas Portfolio 的代码规范、提交规范、分支策略和贡献流程。

---

## 1. 开发环境要求

| 工具 | 版本要求 |
|---|---|
| Node.js | ≥ 18.x（推荐最新 LTS） |
| pnpm | 10.x（通过 `corepack enable` 启用） |
| Git | ≥ 2.x |

### 本地开发

```bash
# 克隆仓库
git clone git@github.com:HugoRCD/canvas.git
cd canvas

# 启用 Corepack
corepack enable

# 安装依赖
pnpm install

# 配置环境变量
cp .env.example .env

# 启动开发服务器
pnpm dev

# 打开浏览器访问
# http://localhost:3000
```

---

## 2. 代码风格规范

### EditorConfig

项目根目录 `.editorconfig` 定义了全局格式约定：

| 规则 | 值 |
|---|---|
| 缩进风格 | space |
| 缩进大小 | 2 |
| 换行符 | LF (`\n`) |
| 字符编码 | UTF-8 |
| 行尾空白 | 自动移除 |
| 文件末尾换行 | 是 |

### TypeScript

- **严格模式**：项目使用 TypeScript 严格模式
- **类型检查命令**：`pnpm typecheck`
- 所有新代码**必须**包含类型注解
- 禁止使用 `any`，使用 `unknown` 或具体类型替代
- 优先使用 `interface` 定义对象类型，`type` 定义联合/交叉类型

### Vue 组件

- 使用 `<script setup lang="ts">` 语法
- 组件 Props 使用 `defineProps<T>()` 带类型声明
- 组件 Emits 使用 `defineEmits<T>()` 带类型声明
- 样式使用 Tailwind 工具类，不使用 `<style>` 块（除非有特殊需求）
- 组件名使用 PascalCase

### ESLint

- 使用 ESLint 9 Flat Config（`eslint.config.mjs`）
- 基于 `@nuxt/eslint-config`
- 启用 stylistic 规则
- 关闭 `vue/multi-word-component-names`（允许单词组件名）

```bash
# 检查代码规范
pnpm lint

# 自动修复
pnpm lint:fix
```

### CSS / Tailwind

- **工具类优先**：所有样式通过 Tailwind 工具类实现
- **禁止 scoped CSS**：不在 Vue 组件中使用 `<style scoped>`
- **语义化颜色**：使用 `text-muted`、`bg-card` 等语义类，而非 `text-gray-500`
- **类名顺序**：按逻辑分组排列（布局 → 间距 → 尺寸 → 排版 → 颜色 → 状态）

---

## 3. 项目架构约定

### 目录结构约定

| 目录 | 用途 | 规则 |
|---|---|---|
| `app/components/content/` | 页面级内容组件 | 通过 Nuxt Content MDC 语法引用 |
| `app/components/{page}/` | 页面子组件 | 与对应页面同名目录 |
| `app/components/layout/` | 布局组件 | Navbar, Footer, ScrollToTop |
| `app/composables/` | 组合式函数 | `use` 前缀命名 |
| `app/utils/` | 工具函数 | `use` 前缀命名（自动导入） |
| `content/{locale}/` | 内容文件 | Markdown + JSON，数字前缀控制排序 |
| `server/` | 服务端代码 | API 路由、邮件、中间件 |
| `i18n/locales/{locale}/` | UI 翻译 | JSON 格式，按功能分文件 |
| `public/` | 静态资源 | 图片、图标、manifest |

### 文件命名约定

| 类型 | 约定 | 示例 |
|---|---|---|
| Vue 组件 | PascalCase | `SpotlightCard.vue` |
| TypeScript 工具 | camelCase + use 前缀 | `useNavigation.ts` |
| 内容页面 | 数字前缀 + kebab-case | `1.index.md`, `2.works.md` |
| 项目数据 | kebab-case + `.json` | `my-project.json` |
| 文章 | kebab-case + `.md` | `my-article.md` |
| i18n 文件 | kebab-case + `.json` | `navigation.json` |

### 自动导入

Nuxt 自动导入以下内容，无需手动 import：

- `app/components/` 下的所有 Vue 组件
- `app/composables/` 下的所有组合式函数
- `app/utils/` 下的所有工具函数
- Nuxt 和 Vue 的内建组合式函数和组件

---

## 4. 内容管理约定

### Nuxt Content 规范

1. 页面文件使用数字前缀控制渲染顺序：`1.index.md` → `2.works.md` → ...
2. 页面内容使用 MDC 语法引用 Vue 组件：`::home{}`、`::works{}`
3. 项目数据使用 JSON 格式，存放在 `content/{locale}/projects/`
4. 文章使用 Markdown 格式，存放在 `content/{locale}/articles/`
5. 每种语言的内容必须保持结构一致

### 内容 Schema

`nuxt.schema.ts` 定义了 Nuxt Studio 可编辑的字段。新增可编辑配置时需同步更新此文件。

---

## 5. Git 规范

### 分支策略

| 分支 | 用途 | 命名 |
|---|---|---|
| `main` | 生产分支，始终保持可部署状态 | `main` |
| 功能分支 | 新功能开发 | `feat/{issue-number}-{description}` |
| 修复分支 | Bug 修复 | `fix/{issue-number}-{description}` |
| 文档分支 | 文档更新 | `docs/{description}` |
| 重构分支 | 代码重构 | `refactor/{description}` |

示例：
```
feat/42-add-dark-mode-toggle
fix/88-fix-mobile-nav
docs/update-readme
```

### 提交信息规范

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>(<scope>): <subject>

<body>

<footer>
```

#### Type（必填）

| Type | 说明 |
|---|---|
| `feat` | 新功能 |
| `fix` | Bug 修复 |
| `docs` | 文档变更 |
| `style` | 代码格式（不影响逻辑） |
| `refactor` | 重构（非新功能、非修复） |
| `perf` | 性能优化 |
| `test` | 测试相关 |
| `build` | 构建系统或依赖变更 |
| `ci` | CI/CD 配置变更 |
| `chore` | 其他不修改 src 或 test 的变更 |
| `revert` | 回退提交 |

#### Scope（可选）

常用 scope：

| Scope | 说明 |
|---|---|
| `content` | 内容文件变更 |
| `ui` | UI 组件变更 |
| `config` | 配置文件变更 |
| `i18n` | 国际化相关 |
| `seo` | SEO 相关 |
| `email` | 邮件服务 |

#### 示例

```
feat(ui): add SpotlightButton component

fix(content): resolve article rendering order

docs: update deployment guide

refactor(ui): simplify SpotlightCard mouse tracking logic
```

### PR 标题规范

PR 标题同样遵循 Conventional Commits 格式，项目通过 CI 自动校验。

---

## 6. 质量检查

### 提交前必做

```bash
# 1. ESLint 检查
pnpm lint

# 2. TypeScript 类型检查
pnpm typecheck

# 3. 本地构建验证
pnpm build
```

所有命令通过后才能提交和创建 PR。

### CI 流水线

项目配置了以下 GitHub Actions 工作流：

| 工作流 | 触发条件 | 检查内容 |
|---|---|---|
| `build.yml` | PR 到 main | 构建验证 |
| `build-image.yml` | Release Tag | Docker 镜像构建与推送 |
| `label-pr.yml` | PR 创建/更新 | 自动标签 |
| `semantic-pull-request.yml` | PR 创建/更新 | PR 标题格式校验 |

---

## 7. 贡献流程

### 步骤

1. **提出 Issue**：先创建 Issue 讨论你想要的变更
2. **Fork 仓库**：点击 GitHub 页面右上角 Fork 按钮
3. **创建分支**：
   ```bash
   git checkout -b feat/123-add-new-feature
   ```
4. **开发与测试**：在本地进行开发和验证
5. **代码规范**：运行 `pnpm lint:fix` 和 `pnpm typecheck` 确保代码合规
6. **提交变更**：遵循 Conventional Commits 规范
   ```bash
   git add .
   git commit -m "feat(ui): add new feature"
   ```
7. **推送分支**：
   ```bash
   git push origin feat/123-add-new-feature
   ```
8. **创建 Pull Request**：
   - 填写 PR 模板中的所有必填项
   - 关联对应 Issue（如 `Closes #123`）
   - PR 标题遵循 Conventional Commits 格式
9. **代码审查**：等待维护者审查和批准
10. **合并**：审查通过后合并到 main

### PR 要求

- [ ] 通过所有 CI 检查
- [ ] 至少一位维护者批准
- [ ] PR 标题符合 Conventional Commits 格式
- [ ] 关联对应 Issue
- [ ] 代码变更影响文档时，同步更新文档
- [ ] 新增功能需更新 `nuxt.schema.ts`（如涉及 Studio 可编辑配置）

---

## 8. 发布与部署

### 版本号

遵循 [Semantic Versioning](https://semver.org/)（语义化版本）：`MAJOR.MINOR.PATCH`

### Docker 镜像

- 发布新版本时，GitHub Actions 自动构建并推送 Docker 镜像到 `ghcr.io`
- 本地可通过 `docker-compose.local.yml` 测试

---

## 9. 国际化开发规范

1. 所有用户可见文本**必须**通过 i18n 系统管理，禁止硬编码
2. UI 文本放在 `i18n/locales/{locale}/` 下的 JSON 文件中
3. 内容文本放在 `content/{locale}/` 下
4. 新增语言时，需同时提供 UI 翻译和内容翻译
5. 翻译键使用点分隔的命名空间：`global.all_rights_reserved`

---

## 10. 安全规范

1. **禁止**在代码中硬编码密钥、Token 或敏感信息
2. 所有敏感配置通过 `.env` 环境变量注入
3. `.env` 文件已在 `.gitignore` 中排除
4. API Key 等敏感字段使用 `NUXT_PRIVATE_` 前缀（Nuxt 仅在服务端暴露）
5. 邮件服务仅在设置 `NUXT_PRIVATE_RESEND_API_KEY` 后启用
