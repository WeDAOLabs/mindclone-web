# 思维克隆体（Mind Clone Agent）

**你的数字分身系统** —— 面向创始人、CEO 与高价值个体的单页营销站点，沉淀价值观、决策逻辑与思维方式。

## 技术栈

- **构建**：Vite 6、TypeScript  
- **UI**：React 19、Tailwind CSS v4  
- **动效**：motion；**图表**：Mermaid；**图标**：lucide-react  

更细的目录与协作约定见 [AGENTS.md](./AGENTS.md)。

## 本地开发

**前置条件**：已安装 Node.js；包管理使用 [pnpm](https://pnpm.io/installation)（也可启用 [Corepack](https://nodejs.org/api/corepack.html)，与 `package.json` 中的 `packageManager` 对齐版本）。

1. 安装依赖：`pnpm install`  
2. （可选）复制环境变量模板：将 [.env.example](./.env.example) 复制为 `.env` 或 `.env.local`，按需填写。  
3. 启动开发服务器：`pnpm dev`  

开发服务器默认监听 **3000** 端口、host `0.0.0.0`，浏览器访问：<http://localhost:3000>。

当前前端页面**不依赖** Gemini 即可浏览；`GEMINI_API_KEY`、`APP_URL` 等为模板预留或与后续能力对接时使用。仓库内 `src/` 暂未调用 Gemini API，若在前端接入请注意密钥暴露风险（通常应经后端代理）。

## 构建与检查

| 命令 | 说明 |
|------|------|
| `pnpm run build` | 生产构建，输出至 `dist/` |
| `pnpm run preview` | 本地预览构建结果 |
| `pnpm run lint` | TypeScript 检查（`tsc --noEmit`） |
| `pnpm run clean` | 删除 `dist/` |

## 相关文件

- [metadata.json](./metadata.json) — 应用名称与描述（可与 AI Studio 等托管元数据对齐）  
- [AGENTS.md](./AGENTS.md) — 面向协作者与 Agent 的项目说明与约定  


