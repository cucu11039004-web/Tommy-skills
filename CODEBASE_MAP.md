# 代码地图

Tommy-skills 收录我的个人 AI 配置，面向我自己：包括通用 skill、Copilot agent、飞书专用 skill 和飞书自动任务。

本文件用于看清全局：每个目录装什么，每类配置分别负责什么。项目目标见 [README.md](README.md)，环境与协作约定见 [AGENTS.md](AGENTS.md)。

## 目录结构

- `skills/`：通用 skill，Claude Code / Codex / Copilot 都能用，随一键安装分发
  - `research/paper-digest/`：把论文或技术博客写成中文「论文分享」笔记
  - `coding/code-tour/`：讲解 vibe coding 刚生成的一批代码
- `copilot/agents/`：VS Code Copilot 模式的自定义 agent
  - `Chat.agent.md`：简单问题直接回答，按需查公开网页
- `feishu/skills/`：飞书（豆包）专用 skill，不随一键安装
  - `todo-quick-add/`：把口述或录音转写整理成待办，写入「To Do List」
- `feishu/automations/`：飞书（豆包）定时任务，记录调度与提示词原文
  - `每日科技进展推送.md`：08:50，机器人与 AI 日报
  - `更新项目文档入口.md`：18:30，重算文档库各页面的「文档入口」
  - `每日文档归档与台账同步.md`：21:00，把云盘文档归档进文档库，并同步台账
  - `每日归档已完成事项.md`：22:00，把已勾选的待办搬进《已完成事项》
- `README.md`：清单与安装方式
- `AGENTS.md`：协作与 Git 提交约定

## 各部分职责

| 分组 | 涉及位置 | 职责 | 典型改动 |
|---|---|---|---|
| 通用 skill | `skills/<分类>/<skill 名>/` | 跨智能体通用的工作流程；`SKILL.md` 写流程，`references/` 放模板与范例，`agents/openai.yaml` 写 Codex 显示名 | 新增 skill、调整步骤或模板 |
| Copilot agent | `copilot/agents/` | VS Code Copilot 模式下的专用对话角色 | 新增 agent、调整工具或回答风格 |
| 飞书 skill | `feishu/skills/` | 飞书里手动触发的工作流，依赖 lark-cli 和文档库结构 | 用户在飞书改版后覆盖原文件 |
| 飞书自动任务 | `feishu/automations/` | 飞书里按时运行的维护任务，负责日报、文档归档、入口与待办整理 | 用户在飞书改版后覆盖原文件；新增任务 |
| 文档 | `README.md`、`AGENTS.md`、本文件 | 清单、安装方式、协作约定、全局地图 | 增删配置时同步清单与本文件 |
