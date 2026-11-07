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

## 安装与更新 skill

安装和更新是同一条命令，作用范围是本仓库的全部 skill：

```bash
npx skills@latest add cucu11039004-web/Tommy-skills -g -a claude-code -a codex -a github-copilot -y
```

- 这条命令只克隆本仓库：已装的 skill 覆盖为最新版，仓库新加的一并装上，不会碰 mattpocock 等其他来源的 skill。
- `-y` 跳过交互选择，默认选中本仓库的全部 skill。
- Skill 实际装在 `~/.agents/skills/<skill 名>/`，CLI 按 `-a` 在各客户端目录建链接：Claude Code 是 `~/.claude/skills/`，Copilot 是 `~/.copilot/skills/`，Codex 直接读 `~/.agents/skills/`。新电脑上第一次安装就会自动建好，不用手动建软链；如果 `~/.claude/skills` 已经整个链到 `~/.agents/skills`，CLI 会识别出是同一位置并跳过。
- 不要用不带名字的 `npx skills update`，它会把 mattpocock 等所有来源的 skill 一起更新。
- 本仓库删掉的 skill 不会随重装被删，需要手动执行 `npx skills@latest remove <skill 名> -g`。

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
