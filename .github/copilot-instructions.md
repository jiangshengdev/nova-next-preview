# Nova Next Preview – Copilot 指南

## 技术栈与布局

- Vue 3 RC（`@vue/runtime-dom`）应用，入口固定在 `src/main.js`，根组件为 `src/App.vue`。
- Webpack 4 + `vue-loader` + `MiniCssExtractPlugin` 负责编译，最终将 CSS 输出到 `dist/main.css` 并在 `index.html` 引用。
- UI 主要演示 `@jiangshengdev/nova-next` 提供的 `NovaColorPicker`，没有 Vue Router 或全局状态库。

## 外部依赖与资源

- 在组件内显式引入 Nova Next 的 `themes.css`、`dropdown.css`、`color-picker.css`，缺失会导致控件无样式。
- `webpack.config.js` 中将 `vue` 映射到 `@vue/runtime-dom` 用于稳定 HMR，除非同步调整 dev server，否则不要移除。
- 二进制资源通过 `url-loader`（8 KB 内联阈值）与 `file-loader` 处理，新增资源沿用该策略避免构建异常。

## 构建与运行

- 安装依赖：`npm install`（仓库无 lockfile，保持 npm）。
- 开发预览：`npm run dev` 使用 `webpack-dev-server` 从仓库根目录服务 `/dist/main.js`，带 HMR 与报错遮罩。
- 生产构建：`npm run build` 等同 `webpack --env.prod`，开启 `mode: "production"`、source map，并关闭 CSS HMR。
- 代码格式化：`npm run prettier` 只覆盖 `src/**/*.{js,vue}`，提交 UI 变更前务必运行。

## 编码模式

- 统一使用 Composition API（`setup`、`reactive`），新增逻辑应避免回退至 Options API。
- 颜色值存放在 `state` 代理并通过 `NovaColorPicker` 的 `value` 传递，使用 `@update` 事件保持同步。
- 样例数据（如 `preset` 调色板）与组件同文件定义，方便快速调试与演示。
- 所需 CSS/组件必须在使用处显式 import，以保证 tree shaking 行为可预测。

## Webpack 约定

- 入口仅限 `src/main.js`，如需额外 bundle 同步修改 `webpack.config.js` 与 `index.html`。
- CSS loader 顺序为 `[MiniCssExtractPlugin.loader, css-loader]`；若引入预处理器，在数组末尾追加而不是替换现有步骤。
- Dev server 通过 `contentBase: __dirname` 提供静态文件，请将生成产物放在 `dist/`，避免触发额外配置。

## 测试与文档

- 当前无自动化测试或 Storybook，变更需通过浏览器运行 `npm run dev` 手动验证。
- `README.md` 仅包含占位信息，如需记录实验或发现，请直接在组件注释或 PR 说明中补充。

## 规则

- 所有文档、代码注释与机器人回复统一使用中文，保持术语一致。
- 引入新依赖或配置时，应在本文件补充相应指引，方便后续代理快速上手。
- 遇到 `NovaColorPicker` 以外的新 Nova Next 组件，复用“就地数据 + 事件同步”的模式，保持演示一致性。
