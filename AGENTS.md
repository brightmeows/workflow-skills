# workflow-skills — Agent Guide

## 仓库定位

个人维护的工作流类代理技能集。每个技能一个目录（`skills/<name>/SKILL.md`），无脚本依赖。

| 技能 | 用途 |
|------|------|
| [grilling](skills/grilling/SKILL.md) | 方案压力测试：持续盘问每个细节直到达成共识 |
| [writing-for-agents](skills/writing-for-agents/SKILL.md) | 给代理写文档的规范：上下文指针、两种负载、信息层级、完成判据 |
| [ai-taste](skills/ai-taste/SKILL.md) | 中文文本的 AI 味审计：提示词文档与散文两轨，逐条病征带判定动作 |
| [tech-doc-zh](skills/tech-doc-zh/SKILL.md) | 中文技术文档的清晰度写作与审计：受控语言、一句一指令、术语漂移 |
| [abstraction-design](skills/abstraction-design/SKILL.md) | 抽象设计与整理：边界按变化划、深模块、错抽象的回退 |

## 边界

### Always

- 修改 `.md` 后通过 `pre-commit run markdownlint` 验证格式
- 修改任何 `SKILL.md` 后，重算 sha256 写入 `.well-known/agent-skills/index.json` 的 `digest`；同步该文件的 `description`，使其与 frontmatter 逐字一致
- 新增或移除技能目录时，同步更新 `.well-known/agent-skills/index.json` 与 `.claude-plugin/marketplace.json` 的 `skills`
- 提交信息使用 Conventional Commits；每完成一个逻辑单元立即原子提交
- 提交前执行 `git status` + `git diff` 确认只包含预期变更
- 中文文本使用全角标点与弯引号；代码、命令与路径保持原样
- 技能的外部参考文献（来自互联网的引用，非技能自带参考文件）放 docs/，不放技能目录

### Ask

- 需修改 `.markdownlint.toml` 基线或 `.pre-commit-config.yaml` 钩子逻辑时先确认
- 需要新增、移除或拆分技能时先确认

### Never

- 勿启用 `.markdownlint.toml` 中禁用的规则（注释已说明原因）
- 勿在未更新 digest 的情况下提交 `SKILL.md`（`check-well-known-digest` 会拦截）
- 勿在 SKILL.md 中写入未经验证的事实；页面结构、命令用法一类事实改动后必须实机复核

## 命令

```bash
# 全量校验（提交前必跑）
pre-commit run --all-files

# 单独任务
pre-commit run markdownlint
pre-commit run check-well-known-list        # skills/ 目录与 index.json 双向一致
pre-commit run check-well-known-digest      # index.json digest 与 SKILL.md 匹配
pre-commit run check-skill-name-consistency # frontmatter name/description 与 index.json 一致
pre-commit run check-plugin-skills-list     # marketplace.json skills 与技能目录一致
pre-commit run check-skill-md-format        # frontmatter 字段格式与 body 行数合规

# 修改 SKILL.md 后更新 digest
sha256sum skills/<name>/SKILL.md
```

## 技能安装（npx skills）

本仓通过 `npx skills` 分发。改动推送后，按下面的命令重装全局技能：

```bash
# 列出仓库内可装技能，确认远程已包含本次改动
npx -y skills add brightmeows/workflow-skills -l

# 全局安装或更新全部技能
npx -y skills add brightmeows/workflow-skills -g -y -s '*' \
  -a codebuddy -a codex -a opencode -a pi

# 查看全局已装技能与来源
npx -y skills ls -g
```

- `-a` 的值用小写 agent ID，重复写；逗号串会被判成无效 agent。
- 安装目标按当前环境填写；要装到全部 agent，可用 `--all` 代替 `-s '*'` 与重复的 `-a`。
- `npx skills add` 从 GitHub 拉取，本地改动要先推送再安装。

## SKILL.md 编写约定

- frontmatter `name` 与父目录名一致，小写连字符
- `description` 先写触发条件（何时取），再写功能与覆盖范围；触发词放最前；总长不超过 1024 字符；如需写关键词，用 `Keywords:`，中文在前英文在后
- 正文少于 500 行；事实类内容须在改动时重新验证，不依赖记忆
- 技能名用反引号包裹
- 规则的决策理由、证据与否决记录放 `docs/<skill>-rationale.md`，不写进 SKILL.md 正文；翻译技能可用 frontmatter `source` 代替，调研台账用 `-probes.md` 或 `-references.md` 作附属证据；改规则时同提交更新对应文档
- `docs/` 不随技能分发；维护理由的索引放 README，不写进 SKILL.md 末尾

## 维护指南

按“起步、观察、补充、精简、重复”的增量迭代维护本文件：

- 代理反复忽略某条规则时，补充到对应边界节
- 代理已能稳定遵循某条规则时，从边界节移除（已内化）
- 规则可被 hook 或 lint 强制时，迁移到 `.pre-commit-config.yaml`，指向工具配置
- 单节边界超过 10 条，或三节合计超过 12 条时，审计精简，工具可强制的移出
