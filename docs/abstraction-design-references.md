# abstraction-design 参考与证据

技能 `skills/abstraction-design/SKILL.md` 为原创归纳，本文档是其方法论出处与证据明细。技能正文保持操作密度，来源核对集中在这里。调研日期：2026-10-23。

## 方法论来源

- John Ousterhout《A Philosophy of Software Design》（2018）：深模块（价值 = 功能量 ÷ 接口面积）、信息隐藏、接口围绕调用者需要知道什么设计、至少对比两个设计。
  - 全文整理：<https://raw.githubusercontent.com/magnus919/agent-skills/refs/heads/main/programming-principles/references/a-philosophy-of-software-design.full.md>
- Sandi Metz《The Wrong Abstraction》：duplication is far cheaper than the wrong abstraction；错抽象变质轨迹（提取、弯折、加条件，循环到不可理解）；内联、删减、重提炼（与 Dan Abramov 的 inline first, re-extract later 同源）。
  - Metz 访谈转述：<https://thoughtbot.com/blog/refactor-until-you-feel-almost-comfortable>
- Don Roberts 的 Rule of Three；Kent C. Dodds 的 AHA（Avoid Hasty Abstractions）：提取时机，过早抽象是信息不全时的架构决策。
  - <https://github.com/pproenca/dot-claude/blob/master/plugins/dev-workflow/skills/pragmatic-architecture/SKILL.md>
- Joel Spolsky《The Law of Leaky Abstractions》（2002）：所有非平凡抽象都会泄漏。
  - <https://blog.ndepend.com/plugging-leaky-abstractions/>
- Dave Cheney《Avoid package names like base, util, or common》（2019）：命名承接抽象，不泄漏技术。
  - <https://dave.cheney.net/2019/01/08/avoid-package-names-like-base-util-or-common>

## Code Smell 目录

Martin Fowler《Refactoring》：变更散布（shotgun surgery）与多变更原因（divergent change）互为镜像，修法是集中变更点；数据结伴（data clumps）该收成结构，原始类型偏执（primitive obsession）同族；投机通用性（speculative generality）指为不需要的东西准备的钩子与特例。

- 第二版摘要：<https://github.com/ittus/Refactoring-summary-2nd-javascript>
- Bad Smells in Code 讲义：<http://sis36.berkeley.edu/projects/streek/agile/bad-smells-in-code.pdf>

## 学科模型来源

- 过拟合：抽象 = 归纳假设、用例 = 样本，统计学习通识。
- 认知负荷与分块：Sweller 认知负荷理论、Miller 的 7±2；深模块是其工程表述。
- 内聚与耦合：Yourdon / Constantine 结构化设计；单一变更原因与 SRP 同源。
- 康威定律：模块边界对齐沟通结构；防腐层出自 DDD（Evans）。
- 实物期权与技术债：技术债隐喻出自 Ward Cunningham。

## 数据建模来源

- Make illegal states unrepresentable（Yaron Minsky）：类型编码状态机，校验前移到编译期。
  - <https://inside.java/2024/06/03/dop-v1-1-illegal-states/>
  - <https://github.com/evryg-org/evryg/blob/main/apps/evryg-kb/content/en/advanced-software-engineering/type-design/make-illegal-states-unrepresentable/index.mdx>
- 反向警告——验证不做成数据丢弃：<https://avdi.codes/dont-throw-away-invalid-data/>
- Data-Oriented Programming（数据形状先行、不可变、显式状态转换）：<https://livebook.manning.com/book/data-oriented-programming-in-java/chapter-4/v-16>

## 架构模式来源

- Functional Core, Imperative Shell；Hexagonal / Ports and Adapters；依赖规则（内层不提名外层）：
  - <https://github.com/wahidyankf/beaver-nest/blob/main/repo-governance/development/quality/code/hexagonal-architecture/002-layers-and-the-dependency-rule.md>
  - <https://raw.githubusercontent.com/wahidyankf/ose-public/refs/heads/main/repo-governance/development/pattern/hexagonal-architecture.md>

## AI 产出偏差证据

- Abstraction bloat（反模式库，标记 established）：代理优化看起来完备的产出而非最小实现。<https://github.com/agentpatterns-ai/website/blob/main/patterns/anti-patterns/abstraction-bloat.md>
- Code slop 清单：76% 开发者认为 AI 代码需要重构；AI 采纳期代码重复率 8.3% 升至 12.3%（2021 至 2024）。<https://github.com/oakoss/agent-skills/blob/main/skills/de-slopify/references/code-slop.md>
- Ox Security《Army of Juniors》（2025-10）：AI 代码“高度可用但系统性缺乏架构判断”，300 个开源项目中 10 类架构反模式高频出现。InfoQ 转述：<https://www.infoq.com/news/2025/11/ai-code-technical-debt/>
- Chris Lattner 对 vibe coding 的批评（黑盒试错取代系统推演）：<https://cloud.tencent.cn/developer/article/2690909>

## 清扫轮与写前搜现成来源

主指令文件的变更后清扫习惯与技能“代理协作”先搜再写条的核对来源。调研日期：2026-10-24。

- 官方插件 code-simplifier agent 全文：行为保持、跟随项目规范、增强清晰度、防过度简化、聚焦最近修改的代码。<https://github.com/anthropics/claude-plugins-official/blob/main/plugins/code-simplifier/agents/code-simplifier.md>
- Anthropic Help Center 官方技巧页：证实 /simplify 以并行代理审查变更代码的复用、品质、效率与 CLAUDE.md 合规。<https://support.claude.com/zh-TW/articles/14554000-claude-code-%E9%AB%98%E7%B4%9A%E7%94%A8%E6%88%B7%E6%8A%80%E5%B7%A7>
- 官方 changelog：v2.1.147 将 /simplify 改名 /code-review 并移除清理行为；v2.1.152 起 /simplify 为 /code-review --fix 的别名，审查复用、简化、效率与层级（altitude）清理后落地修复。<https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md>
- /simplify 未见于官方文档与 changelog 的问题记录，含二进制 strings 中的现行工具描述（只管质量，不找 bug）。<https://github.com/anthropics/claude-code/issues/97711>
- 三代理并行架构（复用/品质/效率）为 v2.1.63 时代行为，来源是社区重构稿，仅作流程参考，不引为官方事实。<https://github.com/Leonxlnx/agentic-ai-prompt-research/blob/main/prompts/19_simplify_skill.md>
