# Cursor 技能仓库（团队共建）

本仓库用于集中维护 [Cursor](https://cursor.com) **Agent Skills**，供小组成员拉取、评审与回灌到本机，保持 PRD 撰写与「PRD → Vue 原型」流程一致。

在线仓库： [https://github.com/lizy0226/cursor](https://github.com/lizy0226/cursor)

## 本仓库包含哪些技能

| 目录 | 说明 |
| --- | --- |
| [`skills/SenseCare-product-master/`](./skills/SenseCare-product-master/) | SenseCare 标准 PRD 撰写/扩写/评审（含 `reference-context` 等产品上下文基线） |
| [`skills/prd-to-vue-prototype/`](./skills/prd-to-vue-prototype/) | 将 PRD 落地为可运行的 Vue3 原型（Vite、Pinia、Ant Design Vue、Mock） |

## 本机使用方式

技能需放在本机 **Cursor 用户配置目录** 下的 `skills` 中（与 [Cursor 技能文档](https://docs.cursor.com) 中 Agent Skills 的约定一致）：

1. 克隆本仓库到任意本地路径，例如：
   ```bash
   git clone https://github.com/lizy0226/cursor.git
   ```
2. 将本仓库中的技能 **整个文件夹** 复制到 Cursor 的 `skills` 目录（需保留目录名与 `SKILL.md`）：
   - Windows 示例路径：  
     `%USERPROFILE%\.cursor\skills\`  
   - 应存在例如：  
     `%USERPROFILE%\.cursor\skills\SenseCare-product-master\SKILL.md`  
     `%USERPROFILE%\.cursor\skills\prd-to-vue-prototype\SKILL.md`
3. 重启 Cursor 或在对话中通过 `@skills/技能文件夹名` 引用技能，确认能加载到对应 `SKILL.md`。

若你已在本地用符号链接/快捷方式把该仓库挂到 `~/.cursor/skills/`，需自行保证链接目标更新后仍指向本仓库的同名目录，避免单文件断链。

## 协作与贡献

1. **改前拉取最新**：`git pull origin main`（或你所在分支名）。
2. **小步提交**：一个 PR 只改一个技能或一个主题，便于 review。
3. **描述清楚**：`SKILL.md` 中若修改了 PRD/原型约定，在 PR 说明里写清**适用场景**与**对既有文档的兼容性**（例如章节约束变更）。
4. **发布同步**：合并进 `main` 后，各成员在本地对 `~/.cursor/skills/` 中对应技能执行覆盖复制或 `git pull` 后再次复制，避免长期漂移。

## 许可与敏感信息

- `reference-context/` 下的产品基线为说明用途，**勿提交**内网专有机密、真实患者数据或未脱敏的账号信息。
- 若发现误提交，请从历史中移除后轮换相关凭据，并知会维护者。

## 相关链接

- 仓库： [lizy0226/cursor](https://github.com/lizy0226/cursor)
- 上游产品技能若与 SenseCare 命名约定调整，以本仓库 `SKILL.md` 中 `name` 与正文章节为准。
