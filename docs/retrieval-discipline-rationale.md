# 取数纪律的维护理由

本文记录 `skills/retrieval-discipline/SKILL.md` 的决策理由、证据与粒度裁决。技能正文是操作规则，本文是维护参考；dotfiles 的 `AGENTS.ref.md` 只留索引。

## 语气备案

维护者已裁决整体放松措辞。历史证据：早期实测观察到代理在温和表述下主动中断获取、截断输出、跳过查证，因此本节曾刻意取强断言。若截断、跳过查证的行为回退，恢复强断言措辞是第一杠杆；强措辞对照表已从 dotfiles 删除，可从其 git 历史取回。

## 事实基础

Pi 有 auto-compaction（保留最近 keepRecentTokens、结构化摘要）加 branch summarization 加 session 持久化（Pi 包内文档 `docs/compaction.md` 已核对），所以 dotfiles 主文件“上下文管理有运行时兜底”是事实准确的表述。

## 关键 nuance

不设限不等于无脑塞。context rot 与 lost-in-the-middle 是真实限制（arXiv:2510.05381）；正确应对是完整获取不动摇，用机制管理信噪比（落盘复用、批次调用、让工具自己精简）。JetBrains 研究（arXiv:2508.21433）：observation masking 与 LLM summarization 效果相当但成本减半，机制比担心管用。

## 粒度裁决

- 查证与完整获取优先于往返效率。
- 效率手段（缓存、并行、收窄）不得以截断信息为代价。
- “读完整相关范围”而非机械全文。
- “拿不准或涉及随时间变化的事实”才联网确认。
