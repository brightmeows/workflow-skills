# 提交纪律的维护理由

本文记录 `skills/commit-discipline/SKILL.md` 的决策理由、证据与否决记录。技能正文是操作规则，本文是维护参考；dotfiles 的 `AGENTS.ref.md` 只留索引。

## 规则取舍

- Conventional Commits（`type(scope)!: subject`，`!` 表 breaking）、简体中文、type 与 scope 保留英文约定；一个提交一个逻辑变更（type 或 scope 不同就拆开）、完成可独立验证的逻辑变更立即提交、每个提交都能安全 revert 不破坏仓库自洽；
  提交检查以仓库 hook 为准，没有 hook 的项目收尾至少跑一次基本检查。
- jj 条款移出常驻规则（维护者裁决）：当前维护环境已回退 git、无现役 jj 仓库，探测条款成为常驻死重；操作知识归档在 dotfiles 的 `docs/dev/jujutsu-migration.md`（探测 flag、hooks 缺口、colocated 失真、undo/op log），重用触发条件与重建底稿见该文档重启用路径。

## 否决

- jj-hp 第三方补位（只识别 pre-commit.com 等四种 runner 格式，对自定义 hook 脚本静默放行）。
- shell 层包装 push 作闸门（检查延迟到 push 时才发现，收益低于新增维护面）。

## 措辞教训

- “粒度随意、执行期别纠结”曾实际授权攒大提交，与“高频小提交”自相矛盾。放宽措辞必须限定适用范围：只放宽信息措辞，不放宽拆分纪律。“默认不用问”管编辑请示的节奏，不管提交时机，两条款各管一域不冲突。

## 维护信号

- 其他仓库迁 jj 时，按 dotfiles 的 `docs/dev/jujutsu-migration.md` 谱系评估接入形态；重建常驻探测条款时以该文档为底稿。jj 升级补齐 hooks（#405 落地）时重议 hook 缺口结论。
- 大提交再现时改机制而不是加字，比如 pre-commit 检测单提交跨多 scope 或巨量 diff 时告警；“执行期别纠结”这类元注恢复时同此判断。
