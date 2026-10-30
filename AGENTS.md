# Tommy-skills — 工作环境与协作约定

本文件记录智能体在本仓库工作所需的事实与约定。项目目标、skill 清单与安装方式见 [README.md](README.md)。

## 工作环境

| 项目 | 约定 |
|---|---|
| 执行位置 | 本机（macOS），工作目录为仓库根目录 |
| 运行环境 | 纯 Markdown 仓库，无虚拟环境、无构建步骤 |
| 验证方式 | 推送后用 `npx skills@latest add cucu11039004-web/Tommy-skills` 安装，确认 `~/.claude/skills/<skill 名>` 出现；再在真实任务上试跑该 skill |

## 协作约定

- 新 skill 放在 `skills/<分类>/<skill 名>/`，必须有 `SKILL.md`；按需加载的模板与范例放 `references/`，Codex 显示名放 `agents/openai.yaml`。
- 写 skill 时遵循 `writing-for-agents` skill 的规范：步骤有完成标准，只有部分分支需要的内容下放到 `references/`，不写智能体默认就会做的话。
- Skill 内容不写死某个智能体的工具名，保证在 Claude Code 与 Codex 下都能跑。
- 新增或删除 skill 时同步更新 README 的 skill 清单。
- 项目目标与范围由用户决定；需要改变目标或关键取舍时先说明问题，交由用户决定。

## Git 提交约定

| 项目 | 约定 |
|---|---|
| 标题 | `type: 摘要`，需要限定模块时用 `type(scope): 摘要`，scope 用 skill 名；英文冒号加一个空格 |
| 类型 | `feat` 新 skill 或新能力、`fix` 修正 skill 行为、`docs` 文档；按需使用 `refactor`、`chore` |
| 说明语言 | 中文；类型始终用英文 |
| 分批提交 | 按独立目的分组，每组一个 commit；一个 skill 的 SKILL.md、references 与 README 清单条目一起提交 |
| 说明内容 | 只说明本次做了什么；标题足够时不加正文，需要补充时空行后列少量具体改动 |
