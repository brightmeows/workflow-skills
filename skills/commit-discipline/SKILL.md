---
name: commit-discipline
description: 在写提交说明、拆分提交或判断提交时机时使用。管 Conventional Commits 格式、提交粒度、revert 安全与提交前检查门槛，也覆盖提交说明的常见反模式。
---

# 提交纪律

提交说明写给未来的自己看。格式、语言、粒度、检查门槛四件事，缺一件都会在半年后变成考古。

## 格式

`type(scope)!: subject`

- `type` 与 `scope` 用英文约定，`subject` 用简体中文
- `!` 表示破坏性变更，放在冒号前：`feat(api)!: 移除 v1 端点`
- `scope` 是改动的模块名，小写 kebab-case，比如 `core`、`api`、`cli`
- 例子：`feat(fetcher): 支持自动发现全部活动`

常用 type：`feat`、`fix`、`refactor`、`docs`、`test`、`chore`、`perf`、`build`、`ci`。

## 粒度

- 一个提交只装一个逻辑变更；`type` 或 `scope` 不同的改动分开提交
- 能独立验证的逻辑变更做完就提交，不攒到任务收尾
- 每个提交都能安全 revert：单独回滚不破坏仓库自洽

拆不开时看这个信号：说明里需要用“顺便”连接两件事，那就是两个提交。

## 提交前检查

- 有 hook 的仓库以 hook 为准，原样运行，不绕过
- hook 失败先本地修复（格式化、lint 的修复模式），再重新暂存
- 没有 hook 的项目，收尾至少跑一次基本检查，按仓库实际工具选：`pnpm check`、`cargo check`、`cargo test`、`eslint`
- 暂存后看一眼 `git diff --cached`，确认没夹带无关文件

## 反模式

- 只写“更新了配置”“修复问题”这类笼统说明。落笔前问两句：改了什么，为什么改
- 格式化、重命名、行为变更混在一个提交里
- 用 `--no-verify` 绕过检查，事后也不补跑
- 任务结束时攒一个大提交，说明里列五个 scope

## 完成判据

- 不看 diff 也能从说明知道改了什么、为什么
- `git log --oneline` 里每个提交都能单独 revert
- 检查命令在提交前跑过，失败项已修复或如实报告
