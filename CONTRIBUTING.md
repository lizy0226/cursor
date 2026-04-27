# 贡献指南（Git 协作 + Cursor Skill）

本仓库面向产品、设计、研发协作维护 Cursor Skills。为降低协作成本，请统一遵循以下规范。

## 1. 分支策略

- 保护分支：`main`（禁止直接在本地改完就推送）。
- 日常开发分支命名：
  - `feat/<skill>-<topic>`：新增能力，例如 `feat/sensecare-prd-mermaid-rules`
  - `fix/<skill>-<topic>`：修复问题，例如 `fix/prototype-routing-mapping`
  - `docs/<topic>`：文档优化，例如 `docs/git-collab-guide`
- 一个分支只做一件事，避免“混合修改”。

## 2. 提交信息规范（建议）

推荐格式：

`<type>: <what-and-why>`

常用 `type`：

- `feat`：新增能力
- `fix`：修复缺陷或错误规则
- `docs`：文档或示例更新
- `refactor`：结构重组，不改变语义

示例：

- `feat: add SenseCare PRD section-4 mapping constraints`
- `fix: align prd-to-vue with SenseCare naming`
- `docs: add PM quick start for git and Cursor skills`

## 3. Pull Request 流程（团队标准）

1. 同步主分支：
   - `git checkout main`
   - `git pull origin main`
2. 新建功能分支：
   - `git checkout -b feat/<skill>-<topic>`
3. 修改并本地自检（至少检查：路径、命名、示例是否可复制使用）。
4. 提交：
   - `git add -A`
   - `git commit -m "feat: ..."`
5. 推送并发起 PR：
   - `git push -u origin <branch>`
   - 在 GitHub 发起 PR 到 `main`
6. 至少 1 位同事 review 后再合并。

## 4. PR 必须写清楚的内容

请使用仓库内置 PR 模板，并确保以下字段完整：

- 变更背景（为什么改）
- 影响范围（哪些 skill / 文档受影响）
- 验证方式（如何复现/验证）
- 兼容性说明（是否影响旧用法）
- 风险与回滚（如果线上团队已在使用）

## 5. Skill 修改边界规范

- 每个 Skill 目录必须保留 `SKILL.md`。
- 重命名 Skill 时，需同时更新：
  - `SKILL.md` 的 `name`
  - 其他 Skill 对它的引用说明
  - README / 文档中的目录名与示例
- 对 PRD 结构做强约束调整（如章节编号变化）时，必须同步更新示例与映射模板。

## 6. 给产品经理的最小 Git 命令清单

日常只需要掌握以下 8 条：

```bash
git clone <repo-url>
git checkout main
git pull origin main
git checkout -b feat/<name>
git status
git add -A
git commit -m "docs: update ..."
git push -u origin <branch>
```

## 7. 禁止事项

- 不要在 `main` 直接开发并 push。
- 不要把多个主题塞进一个 PR（例如同时改命名、改流程、改示例）。
- 不要提交敏感数据（账号、密钥、患者隐私、内网地址）。
- 不要在未说明兼容性的情况下修改技能核心语义。
