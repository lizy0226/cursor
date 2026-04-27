# PM 快速上手：Git 协作与 Cursor Skill 使用

面向不熟悉 Git 的产品经理，目标是：**会拉代码、会改 Skill、会提 PR**。

## 1. 你会用到的两个目录

- 仓库目录（你克隆下来的项目）：例如 `C:\Users\<你>\cursor`
- Cursor 本机技能目录：`%USERPROFILE%\.cursor\skills\`

## 2. 首次准备（只做一次）

1. 安装 Git。
2. 克隆仓库：

```bash
git clone https://github.com/lizy0226/cursor.git
```

3. 把仓库里的技能目录复制到 Cursor 技能目录：
   - `skills/SenseCare-product-master`
   - `skills/prd-to-vue-prototype`

## 3. 每次开始改动前

在终端进入仓库后执行：

```bash
git checkout main
git pull origin main
git checkout -b feat/<你的主题名>
```

示例：

```bash
git checkout -b docs/prd-template-update
```

## 4. 在 Cursor 中使用 Skill（产品同学常用）

在对话里直接引用：

- `@skills/SenseCare-product-master`：写/改/评审 PRD
- `@skills/prd-to-vue-prototype`：把 PRD 转成可跑的 Vue 原型

建议提问方式：

- “请基于 `@skills/SenseCare-product-master` 输出 XX 模块 PRD，包含 4.x.2 Mermaid。”
- “请用 `@skills/prd-to-vue-prototype` 按 R1-R5 映射到页面与 Pinia。”

## 5. 完成改动后提 PR

```bash
git status
git add -A
git commit -m "docs: update skill onboarding guide"
git push -u origin <你的分支名>
```

然后去 GitHub 发起 PR（目标分支 `main`），按模板填完整。

## 6. 一眼识别“我是不是走错了”

- 如果你在 `main` 分支直接改文件：停下来，新建分支再改。
- 如果一个 PR 同时改了很多无关主题：拆成多个 PR。
- 如果改了 Skill 名称但没改引用：会导致 `@skills/...` 找不到。

## 7. 常见问题（FAQ）

### Q1：我只改了文案，也要走分支 + PR 吗？

要。这样团队能 review，并且有历史可追踪。

### Q2：我不会处理冲突怎么办？

先不要强行提交，联系评审同学协助；或在 Cursor 里描述冲突文件让 AI 帮你解释差异再处理。

### Q3：怎么确认我改动真的生效？

在 Cursor 对话中用 `@skills/技能目录名` 引用并执行一个最小示例，能按预期输出即视为通过。
