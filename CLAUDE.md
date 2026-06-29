# 项目审查规范

## 项目信息

- 仓库名：`vue-test`
- 技术栈：Vue 3 + Vite
- 部署：GitHub Pages
- `vite.config.js` 中 `base` 必须为 `/vue-test/`

## 自动审查标准

### 可直接 APPROVE（low 风险）

- 仅修改 `src/` 下的 UI、文案、样式
- 不影响构建与部署配置
- 无密钥、无 `.env`、无 `node_modules`

### 必须 BLOCK（high 风险）

- 修改 `.github/workflows/` 且配置明显错误
- 提交密钥、token、`.env`
- `vite.config.js` 的 `base` 与仓库名不一致
- 会导致 `npm ci` 或 `npm run build` 失败

### 需人工确认（medium 风险）

- 修改 `package.json` 依赖大版本
- 修改 `deploy.yml` 或 Pages 相关配置
- 删除重要文件

## 审查输出格式

必须在 PR 评论中包含：

```markdown
## 审查结论
- 状态: APPROVE 或 BLOCK
- 风险等级: low / medium / high
- 能否自动部署: yes 或 no
- 理由: （一句话）

## 问题列表
（无则写「无」）

## 修改建议
（无则写「无」）
```

## 自动合并条件

仅当同时满足时可标记 `能否自动部署: yes`：

1. 状态为 `APPROVE`
2. 风险等级为 `low`
3. 改动范围仅在 `src/` 内

否则写 `能否自动部署: no`。
