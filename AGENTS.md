# Tommy-skills — 工作环境与协作约定

本文件记录智能体在本仓库工作所需的事实与约定。项目目标、skill 与 agent 清单、安装方式见 [README.md](README.md)。

## 工作环境

| 项目 | 约定 |
|---|---|
| 执行位置 | 本机（macOS），工作目录为仓库根目录 |
| 运行环境 | 纯 Markdown 仓库，无虚拟环境、无构建步骤 |
| 验证方式 | Skill：推送后用 README「安装与更新 skill」的命令安装，确认 `~/.claude/skills/<skill 名>` 出现，再在真实任务上试跑；Agent：确认 VS Code Copilot 模式的 Agent 下拉中出现它，再试问一个典型问题 |

## 协作约定

- 新 skill 放在 `skills/<分类>/<skill 名>/`，必须有 `SKILL.md`；按需加载的模板与范例放 `references/`，Codex 显示名放 `agents/openai.yaml`。
- 写 skill 时遵循 `writing-for-agents` skill 的规范：步骤有完成标准，只有部分分支需要的内容下放到 `references/`，不写智能体默认就会做的话。
- Skill 内容不写死某个智能体的工具名，保证在 Claude Code 与 Codex 下都能跑。
- 新增或删除 skill 时同步更新 README 的 skill 清单。
- 外部来源的 skill（如 mattpocock/skills）整仓安装，不拷进本仓库，也不在本仓库列 skill 名单；新增外部来源时在 README「外部 skill」里加一句说明，并在「安装与更新 skill」里加一条 `add` 命令。
- VS Code Copilot 模式的自定义 agent 放在 `copilot/agents/<名称>.agent.md`，frontmatter 写 `target: github-copilot`，tools 用 Copilot 的工具别名（如 `read`、`search`、`web`）。agent 只服务 Copilot，不受「Skill 内容不写死工具名」那条的限制；新增或删除时同步更新 README 的 agent 清单。
- 只在飞书（豆包）里用的 skill 放在 `feishu/skills/<skill 名>/SKILL.md`，作为工作流记录，可以写死 `lark-cli` 命令。不能放进 `skills/`，也不能写进 `skills.sh.json`，否则会被一键安装装到 Claude Code / Codex / Copilot。文档 ID、token、租户域名用 `<…>` 占位符代替。用户在飞书更新后发来新版时，覆盖该文件，同时保留占位符。新增或删除时同步更新 README 的「飞书专用 skill」清单。
- 飞书（豆包）的定时任务放在 `feishu/automations/<任务名>.md`，文件名用飞书里的中文任务名，内容只记调度（cron 与时区）和提示词原文。用户从飞书复制新版发来时，覆盖对应文件，原文照抄，只把链接、域名、space_id、node、token 等换成 `<…>` 占位符。新增或删除时同步更新 README 的「飞书自动任务」清单。
- 修改前先用 [CODEBASE_MAP.md](CODEBASE_MAP.md) 定位目录与职责；增删 skill、agent、飞书 skill 或飞书自动任务时同步更新它。
- 项目目标与范围由用户决定；需要改变目标或关键取舍时先说明问题，交由用户决定。

## Git 提交约定

| 项目 | 约定 |
|---|---|
| 标题 | `type: 摘要`，需要限定模块时用 `type(scope): 摘要`，scope 用 skill 名；英文冒号加一个空格 |
| 类型 | `feat` 新 skill 或新能力、`fix` 修正 skill 行为、`docs` 文档；按需使用 `refactor`、`chore` |
| 说明语言 | 中文；类型始终用英文 |
| 分批提交 | 按独立目的分组，每组一个 commit；一个 skill 的 SKILL.md、references 与 README 清单条目一起提交 |
| 说明内容 | 只说明本次做了什么；标题足够时不加正文，需要补充时空行后列少量具体改动 |
