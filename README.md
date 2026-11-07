# Tommy-skills

个人 AI 定制集合：Claude Code / Codex / Copilot 通用的 skill，以及 VS Code Copilot 模式用的自定义 agent。Skill 按 [mattpocock/skills](https://github.com/mattpocock/skills) 的目录结构组织，用 skills.sh 安装与更新。

## Skill 清单

| Skill | 用途 | 触发方式 |
|---|---|---|
| [paper-digest](skills/research/paper-digest/SKILL.md) | 通读一篇论文或技术博客，先问关注点与对比论文，再按固定模板写成中文「论文分享」笔记；网页里的 GIF 动图原样保留 | 给出本地 PDF、arXiv 链接或网页链接并要求总结、分享、精读；或 `/paper-digest <链接或路径>` |

## Agent 清单

| Agent | 用途 | 使用位置 |
|---|---|---|
| [Chat](copilot/agents/Chat.agent.md) | 简单问题直接回答，按需查公开网页，不读项目上下文 | VS Code Chat 视图，Session Target 选 Copilot，再在 Agent 下拉中选 Chat |

## 安装

```bash
npx skills@latest add cucu11039004-web/Tommy-skills
```

Codex 加 `-a codex`，不加 `-a` 则交互选择目标智能体。Skill 会装到 `~/.agents/skills/<skill 名>/`，与 mattpocock 的 skill 同目录；Claude Code 读取的 `~/.claude/skills` 是 CLI 第一次安装时自动建立的指向 `~/.agents/skills` 的软链，无需手动处理。

## 升级

```bash
npx skills@latest update
```

仓库里新增了 skill 时，重新执行一次安装命令即可拉取。

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
```

## 文档入口

| 文档 | 用途 |
|---|---|
| [AGENTS.md](AGENTS.md) | 协作与 Git 提交约定 |
