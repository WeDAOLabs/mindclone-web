# mindclone-web — Agent 协作说明

本文档面向在本仓库中协助开发的 AI Agent 与人类协作者，概括项目定位、技术栈与约定。

## 项目是什么

- **产品**：「真我 Agent / TrueSelf」——面向创始人、CEO 与高价值个体的**数字分身**落地页（单页营销站点），强调价值观与决策逻辑的沉淀与放大。
- **形态**：纯前端 SPA，入口为 `index.html` → `src/main.tsx` → `src/App.tsx`。
- **来源**：自 Google AI Studio 应用模板演进；`metadata.json` 含应用名称与描述；线上可参考 README 中的 AI Studio 链接。

## 技术栈

| 类别 | 选型 |
|------|------|
| 构建 | Vite 6（`type: "module"`） |
| UI | React 19 + TypeScript |
| 样式 | Tailwind CSS v4（`@import "tailwindcss"` + `@tailwindcss/vite`） |
| 动画 | `motion`（原 Framer Motion 生态） |
| 图表 | Mermaid（架构示意图，见 `Visualization` 组件） |
| 图标 | `lucide-react` |
| 类名工具 | `clsx`、`tailwind-merge`（已依赖，按需使用） |

**Lint**：`pnpm lint` 等价于 `tsc --noEmit`（无 ESLint 配置）。

## 目录与关键文件

```
mindclone-web/
├── index.html              # 入口 HTML，Google Fonts（Noto Sans/Serif SC）
├── vite.config.ts          # React、Tailwind、环境变量、路径别名、HMR
├── tsconfig.json           # paths: "@/*" -> 仓库根目录
├── src/
│   ├── main.tsx            # React 挂载
│   ├── index.css           # Tailwind、@theme、glass-card、section-padding 等
│   └── App.tsx             # 整站 UI（导航、各区块、弹窗、暗色模式）— 体量较大
├── metadata.json           # AI Studio 应用元数据
├── .env.example            # GEMINI_API_KEY、APP_URL 说明
└── README.md               # 本地运行说明（pnpm、GEMINI_API_KEY）
```

**静态资源**：`ContactModal` 引用 `/qrcode.png`，需放在 Vite 的 `public/`（若目录尚不存在，添加 `public/qrcode.png`）。

## 常用命令

- **开发**：`pnpm dev`（默认端口 **3000**，host `0.0.0.0`）
- **构建**：`pnpm build` → `dist/`
- **预览构建**：`pnpm preview`
- **类型检查**：`pnpm lint`
- **清理构建产物**：`pnpm clean`

包管理：仓库当前使用 **pnpm**（存在 `pnpm-lock.yaml`）。新增依赖时请由维护者在本地执行安装命令，勿在自动化环境中假设 `node_modules` 已同步。

## 环境变量

- **`GEMINI_API_KEY`**：在 `vite.config.ts` 中通过 `define` 注入为 `process.env.GEMINI_API_KEY`。本地可复制 `.env.example` 为 `.env` / `.env.local` 并按 README 填写。
- **`DISABLE_HMR`**：设为 `true` 时关闭 HMR（AI Studio 等场景避免代理编辑时闪烁），**不要随意改动** `vite.config.ts` 中与此相关的注释与逻辑。
- **`APP_URL`**：`.env.example` 中说明用于托管 URL / 回调等；当前前端代码未强制依赖，以实际业务为准。

**说明**：`package.json` 含 `@google/genai`，但**当前 `src/` 未调用**；若新增 Gemini 相关逻辑，需与密钥注入方式保持一致并注意前端暴露密钥的风险（通常应通过后端代理）。

## 路径别名

- `@/` 指向**仓库根目录**（与 `tsconfig` 一致），不是仅 `src/`。新增模块时保持与现有 import 风格一致。

## UI 与代码约定

- **暗色模式**：`document.documentElement` 的 `dark` class，与 Tailwind `dark:` 配套。
- **复用样式**：优先使用 `index.css` 中已有工具类（如 `glass-card`、`section-padding`）。
- **单文件现状**：业务组件集中在 `App.tsx`。小幅改动可就地修改；若区块持续膨胀，再按区块拆文件，避免一次性大重构。
- **文案与品牌**：对外文案以中文为主，产品名 TrueSelf / 真我 Agent；修改时注意导航锚点 `#home`、`#value` 等与 `Navbar` 一致。

## Agent 协作建议

1. **最小改动**：只改与任务相关的文件；不顺带大规模格式化或无关重构。
2. **动效与可访问性**：新增交互时保持与现有 `motion`、焦点与语义化标签习惯一致。
3. **Mermaid**：`Visualization` 内图为字符串模板；改图时注意主题变量与 `isDark` 触发重新渲染的行为。
4. **依赖变更**：若需新增依赖，在说明中给出安装命令（如 `pnpm add <pkg>`），由项目维护者在本地执行并提交 lockfile。

## 相关文档

- 人类可读运行步骤：`README.md`
- 应用标题与描述：`metadata.json`、根目录 `index.html` 的 `<title>`
