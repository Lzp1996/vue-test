# 分支保护配置（GitHub 网页操作，一次性）

仓库：**Settings → Branches → Add branch ruleset**（或 **Add classic branch protection rule**）

## 规则

| 配置项 | 设置 |
|--------|------|
| Branch name pattern | `master` |
| Require a pull request before merging | ✅ 开启 |
| Required approvals | `0`（靠 Claude 审查 + CI） |
| Require status checks to pass | ✅ 开启 |
| Required checks | 勾选 **`build`**（来自 `CI` workflow） |
| Require branches to be up to date | ✅ 建议开启 |
| Do not allow bypassing | ✅ 建议开启 |

## 说明

- Status check 名称是 **`build`**，对应 `.github/workflows/ci.yml` 里的 job 名
- 配置完成后：不能直接 push 到 `master`，必须走 PR
- PR 必须 CI 绿色才能 Merge（或等 auto-merge 自动合并）

## 验证

1. 尝试直接 push 到 `master` → 应被拒绝
2. 开 PR 但不通过 CI → Merge 按钮灰色
3. CI 绿 + Claude APPROVE → auto-merge 自动合并
