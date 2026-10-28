# workflow-skills

个人维护的工作流类代理技能集。每个技能一个目录，无脚本依赖。

| 技能 | 用途 | 维护参考 |
|------|------|----------|
| [grilling](skills/grilling/SKILL.md) | 方案压力测试：持续盘问每个细节直到达成共识 | frontmatter `source` |
| [writing-for-agents](skills/writing-for-agents/SKILL.md) | 给代理写文档的规范：上下文指针、两种负载、信息层级、完成判据 | frontmatter `source` |
| [ai-taste](skills/ai-taste/SKILL.md) | 中文文本的 AI 味审计：提示词文档与散文两轨，逐条病征带判定动作 | [探针调研](docs/ai-taste-probes.md) |
| [tech-doc-zh](skills/tech-doc-zh/SKILL.md) | 中文技术文档的清晰度写作与审计：受控语言、一句一指令、术语漂移 | frontmatter `source` |
| [abstraction-design](skills/abstraction-design/SKILL.md) | 抽象设计与整理：边界按变化划、深模块、错抽象的回退 | [参考与证据](docs/abstraction-design-references.md) |
| [commit-discipline](skills/commit-discipline/SKILL.md) | 提交纪律：Conventional Commits 格式、粒度、revert 安全与检查门槛 | [维护理由](docs/commit-discipline-rationale.md) |
| [doc-governance](skills/doc-governance/SKILL.md) | 内容治理：增改废炼四种操作、单一事实源、存放层级与旧账清理 | [维护理由](docs/doc-governance-rationale.md) |
| [retrieval-discipline](skills/retrieval-discipline/SKILL.md) | 取数纪律：完整获取、先定位再回读、工具自精简、并行与落盘 | [维护理由](docs/retrieval-discipline-rationale.md) |

## 安装

```bash
npx skills add brightmeows/workflow-skills
```

或直接复制技能目录到任意代理的技能目录。
