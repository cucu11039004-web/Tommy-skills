# Tommy-skills

个人 Claude Code / Codex skill 集合，按 [mattpocock/skills](https://github.com/mattpocock/skills) 的目录结构组织，可用 skills.sh 一键安装与升级。

## Skill 清单

| Skill | 用途 | 触发方式 |
|---|---|---|
| [paper-digest](skills/research/paper-digest/SKILL.md) | 通读一篇论文，先问关注点与对比论文，再按固定模板写成中文「论文分享」笔记 | 给出 arXiv 链接或 PDF 并要求总结、分享、精读论文；或 `/paper-digest <链接>` |

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

## 目录结构

```
skills/
  <分类>/
    <skill 名>/
      SKILL.md          # 流程与规则
      references/       # 模板、范例等按需加载的参考
      agents/openai.yaml # Codex 列表里的显示名
```

## 文档入口

| 文档 | 用途 |
|---|---|
| [AGENTS.md](AGENTS.md) | 协作与 Git 提交约定 |
