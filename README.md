# Tommy-skills

个人 AI 定制集合：Claude Code / Codex / Copilot 通用的 skill，以及 VS Code Copilot 模式用的自定义 agent。Skill 按 [mattpocock/skills](https://github.com/mattpocock/skills) 的目录结构组织，用 skills.sh 安装与更新。

## Skill 清单

| Skill | 用途 | 触发方式 |
|---|---|---|
| [paper-digest](skills/research/paper-digest/SKILL.md) | 通读一篇论文或技术博客，先问关注点与对比论文，再按固定模板写成中文「论文分享」笔记；网页里的 GIF 动图原样保留 | 给出本地 PDF、arXiv 链接或网页链接并要求总结、分享、精读；或 `/paper-digest <链接或路径>` |
| [code-tour](skills/coding/code-tour/SKILL.md) | vibe coding 完成一次功能升级后，先给这批改动的总览，再按需逐个文件讲职责、结构、新增部分和联动；默认不跑代码 | 仅手动：`/code-tour [文件]`（Codex 用 `$code-tour`）；不带文件时讲最近一批改动 |

## 外部 skill

除本仓库自己的 skill 外，全量安装 [mattpocock/skills](https://github.com/mattpocock/skills)（MIT）。这些 skill 不拷进本仓库，清单以上游为准。

## Agent 清单

| Agent | 用途 | 使用位置 |
|---|---|---|
| [Chat](copilot/agents/Chat.agent.md) | 简单问题直接回答，按需查公开网页，不读项目上下文 | VS Code Chat 视图，Session Target 选 Copilot，再在 Agent 下拉中选 Chat |

## 飞书专用 skill

只在飞书（豆包）里使用的 skill，放在仓库作为工作流记录。下面的一键安装命令不会安装它们，需要时在飞书里单独安装；文档 ID、token 等私人标识已替换为占位符。

| Skill | 用途 |
|---|---|
| [todo-quick-add](feishu/skills/todo-quick-add/SKILL.md) | 把口述或录音转写里的事项整理成待办，预览确认后写入飞书「To Do List」文档的对应分类 |

## 飞书自动任务

飞书（豆包）里的定时任务，每个任务记录调度时间和提示词原文，链接与 ID 已替换为占位符。时间均为 Asia/Shanghai，均在云电脑运行。

| 任务 | 调度 | 用途 |
|---|---|---|
| [每日科技进展推送](feishu/automations/每日科技进展推送.md) | 每天 08:50 | 精选机器人与 AI 领域的论文、开源项目和新闻，生成日报文档并在对话里附摘要 |
| [更新项目文档入口](feishu/automations/更新项目文档入口.md) | 每天 18:30 | 按文档库当前目录重算 6 个页面的「文档入口」，不动正文和结构 |
| [每日文档归档与台账同步](feishu/automations/每日文档归档与台账同步.md) | 每天 21:00 | 把云盘根目录的文档经收件箱归档进文档库，回写《文档审阅台账》并清理快捷方式 |
| [每日归档已完成事项](feishu/automations/每日归档已完成事项.md) | 每天 22:00 | 把《待办事项》里已勾选的条目加日期搬进《已完成事项》，验证后删源 |

## 安装与更新 skill

新电脑第一次安装，两条命令各装一个来源的全部 skill：

```bash
npx skills@latest add cucu11039004-web/Tommy-skills -g -a claude-code -a codex -a github-copilot -y
```

```bash
npx skills@latest add mattpocock/skills -g -a claude-code -a codex -a github-copilot -y
```

日常更新，一条命令更新本机已装的全部 skill：

```bash
npx skills@latest update -g -y
```

- `update` 只更新已装的 skill：删掉的不会被装回来，两个来源新加的也不会自动装上。想拿到新加的 skill，就重跑对应来源的 `add` 命令。
- 重跑 `add` 会把这个来源里删过的 skill 一并装回，所以平时更新用 `update`，不用 `add`。
- 不想要的 skill 直接删：`npx skills@latest remove <skill 名> -g`。本仓库删掉的 skill 也不会随更新被删，同样要手动执行这条命令。
- Skill 实际装在 `~/.agents/skills/<skill 名>/`，CLI 按 `-a` 在各客户端目录建链接：Claude Code 是 `~/.claude/skills/`，Copilot 是 `~/.copilot/skills/`，Codex 直接读 `~/.agents/skills/`。新电脑上第一次安装就会自动建好，不用手动建软链；如果 `~/.claude/skills` 已经整个链到 `~/.agents/skills`，CLI 会识别出是同一位置并跳过。

## 安装与更新 agent

Agent 不经过 skills CLI，通过本仓库的克隆软链到 Copilot 的用户 agent 目录 `~/.copilot/agents/`：

```bash
git clone git@github.com:cucu11039004-web/Tommy-skills.git ~/WorkSpace/Tommy-skills
mkdir -p ~/.copilot
ln -s ~/WorkSpace/Tommy-skills/copilot/agents ~/.copilot/agents
```

- 已有克隆时跳过 `git clone`；克隆在别处时把路径换成实际位置。
- `~/.copilot/agents` 已经是普通目录时，不要整个替换，改为逐个链接文件：`ln -s ~/WorkSpace/Tommy-skills/copilot/agents/Chat.agent.md ~/.copilot/agents/`。
- 更新只需在克隆里 `git pull`；新加的 agent 通过目录链接自动生效。
- 安装后在 VS Code 的 Copilot 模式下打开 Agent 下拉，确认出现 Chat。

## 目录结构

```
skills/
  <分类>/
    <skill 名>/
      SKILL.md           # 流程与规则
      references/        # 模板、范例等按需加载的参考
      agents/openai.yaml # Codex 列表里的显示名
copilot/
  agents/
    <名称>.agent.md      # VS Code Copilot 模式的自定义 agent
feishu/
  skills/
    <skill 名>/SKILL.md  # 飞书专用 skill，不随一键安装
  automations/
    <任务名>.md          # 飞书定时任务的调度与提示词原文
```

## 文档入口

| 文档 | 用途 |
|---|---|
| [AGENTS.md](AGENTS.md) | 协作与 Git 提交约定 |
| [CODEBASE_MAP.md](CODEBASE_MAP.md) | 全局地图：目录结构与各部分职责 |
