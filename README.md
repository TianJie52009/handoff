# handoff · 通用 Agent 交接 Skill

让任何 agent（Codex / Claude / DSH / 任意模型与提供商）在接手项目时，**用最少的 token** 写出一份下一任能直接照着干活的 `HANDOFF.md`。

```
触发：交接 / handoff / 换 agent / 接手 / 写交接文档 / 给下一个 agent
产物：项目根目录一个 HANDOFF.md（≤150 行），外加在 AGENTS.md / CLAUDE.md / README.md 顶部一行入口声明
依赖：只要能读写文件 —— 不需要 git、shell、网络
```

## 为什么需要它

换 agent（或换人）时最贵的是重新摸清项目。大多数交接要么没写、要么把 README 重抄一遍。这个 skill 只让 agent 记录三件真正值钱的事：**现在是什么状态、哪里会踩坑、下一步该干什么**——其余一律用「文件路径 + 一句话」引用，不复制。

## 特性

- **通用**：不限项目类型——程序、数据、文档、配置、agent/提示词工程都适用；有 git 用 git，没有就用文件修改时间。
- **省 token**：单文件 ≤150 行，每节 3~10 条；收集信息用 grep/head，不整篇通读。
- **跨 harness**：就是一份标准 `SKILL.md`（YAML frontmatter），Codex / Claude / DSH 的 skill 目录都能直接放。
- **有入口**：自动在 `AGENTS.md` / `CLAUDE.md` / `README.md` 顶部加「接手先读 HANDOFF.md」，保证下一位一定看得到。
- **职责移交**：文档里自带维护规则——每次接手/大改动更新状态快照与变更历史，换 agent 时必须写清「未完成 / 下一步 / 待确认」。

## 安装

把本仓库文件夹整个复制进对应 harness 的 skills 目录即可（同名文件夹）：

| 工具 | 技能目录（示例） |
|---|---|
| Codex | `~/.codex/skills/handoff/` 或 `~/.agents/skills/handoff/` |
| Claude | `~/.claude/skills/handoff/` |
| DSH | `~/.dsh/skills/handoff/`（服务器上为 `/root/.dsh/skills/handoff/`） |

## 使用

对 agent 说任意触发词，例如：

```text
写一下交接文档
给下一个 agent 写个交接
更新 HANDOFF.md
```

agent 会：快扫项目 → 写/更新 `HANDOFF.md` → 在入口文件加一行声明 → 追加变更历史。

生成的文档骨架见 [`SKILL.md`](SKILL.md) 里的模板，一个填好的例子见 [`examples/HANDOFF.example.md`](examples/HANDOFF.example.md)。

## 维护

- 每次大改动：更新状态快照 + 在变更历史追加一行；大功能同步进项目 README。
- 换 agent：必须写清「当前状态 / 未完成 / 下一步建议 / 待确认点」，不能只写「已完成」。

## English

A harness-agnostic **handoff skill** for any coding/agent environment. It produces a single terse `HANDOFF.md` (≤150 lines) at the project root so that the next agent — Codex, Claude, DSH, or any other — can pick the work up with minimal token cost. It only needs file read/write; git, shell and network are optional. Install by copying the folder into your harness's skills directory.

## License

[MIT](LICENSE)
