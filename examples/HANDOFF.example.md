# HANDOFF（给接手 agent）

> 接手先读本文件；读完再决定读哪些细节。维护规则见最后一节。
> 示例项目：一个用 Node + SQLite 的小型记单词 Web 应用。

## 0. 接手第一步

1) 读 `package.json`、`src/server.js`、`docs/architecture.md`；2) 备份 `data/words.db`；3) 跑 `npm test` 与 `npm run dev` 确认环境可用。

## 1. 当前状态

- 项目一句话：个人记单词 Web 应用，支持导入词表、每日复习、统计。
- 技术栈 / 关键路径：Node 20 + Express（`src/`）、SQLite（`data/words.db`）、前端原生 JS（`public/`）、部署脚本 `deploy.sh`。
- 现在能跑吗：能。`npm test` 18 项全绿，最近一次发布 v0.6.1（2026-10-12）。
- 最近改动：新增「每日复习」算法（间隔重复简化版）；修了导入 CSV 时中文乱码；统计页加了周视图。

## 2. 运行 / 测试 / 部署

- 安装：`npm ci`
- 运行：`npm run dev`（默认 3000）
- 测试：`npm test`
- 部署：`bash deploy.sh prod`（需要环境变量 `APP_KEY`，见 `.env.example`）

## 3. 约定与纪律

- 提交信息用 `feat:/fix:/docs:` 前缀；一个 PR 只做一件事。
- 所有接口必须先写测试；涉及数据库的改动要附迁移脚本。
- 文档改动同步 `docs/`，不要散落在 README。

## 4. 已知坑

- SQLite 在 Windows 上对文件锁敏感：并发写测试要串行跑（`--runInBand`）。
- 导入 CSV 必须 UTF-8；GBK 文件先在外部转码。
- `deploy.sh` 会重启 systemd 服务 `words-app`，本地测试别执行。

## 5. 未完成 / 下一步

- [ ] 复习算法的遗忘曲线参数还是拍脑袋的，建议对照文献调一版并加基准测试。
- [ ] 统计页移动端布局在 375px 宽度会溢出，负责人：无（待认领）。
- [ ] v1.0 前把 `data/words.db` 换成带迁移的版本（当前是手动改表）。

## 6. 变更历史

| 日期 | agent | 改动 |
|---|---|---|
| 2026-10-14 | handoff-skill 示例 | 建立本文件 |
