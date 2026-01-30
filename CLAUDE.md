# CLAUDE.md

此文件为 Claude Code (claude.ai/code) 在处理本仓库代码时提供指导。

## 常用命令

- **安装依赖**: `pnpm install`
- **启动开发服务器**: `pnpm dev` (运行在 http://localhost:4444)
- **生产环境构建**: `pnpm build`
- **代码检查 (Lint)**: `pnpm lint` (使用 ESLint 和 `@antfu/eslint-config`)
- **运行测试**: `pnpm test` (使用 Vitest)
- **更新成语数据**: `pnpm run update` (处理 `src/data/new.txt` 并更新 `src/data/idioms.txt`)

## 代码架构

- **框架**: Vue 3 (Composition API) + Vite
- **样式**: UnoCSS
- **状态管理**: 使用 Vue 的 `reactive`/`ref` 实现响应式状态，位于 `src/state.ts`；持久化存储位于 `src/storage.ts`。
- **游戏逻辑**: 核心逻辑位于 `src/logic/` 目录下。`check.ts` 处理答案校验。
- **游戏模式**:
  - **每日挑战**: 基于日期计算索引（`src/state.ts`）。
  - **随机挑战**: 通过 `src/answers/index.ts` 中的 `getRandomAnswer` 获取随机成语，并使用 URL 参数 `?word=...` 触发。
- **数据源**:
  - 成语存储在 `src/data/idioms.txt`。
  - 多音字存储在 `src/data/polyphones.json`。
  - 新增成语应添加到 `src/data/new.txt`，并通过更新脚本合并。
- **组件**: UI 组件位于 `src/components/`，主应用入口为 `src/App.vue`。
- **国际化**: 配置位于 `src/locales` 和 `src/i18n.ts`。

## 开发指南

- **Linting**: 禁用了 Prettier；依赖 ESLint 进行格式化 (已配置 `editor.codeActionsOnSave` 来修复 ESLint 错误)。
- **数据更新**: 不要手动编辑 `idioms.txt` 添加新条目。请将它们添加到 `new.txt` 并运行 `pnpm run update`。
- **导入**: Vue API 和组件已配置自动导入 (见 `vite.config.ts`, `auto-imports.d.ts`, `components.d.ts`)。通常不需要手动导入 `ref`, `computed` 或通用组件。
