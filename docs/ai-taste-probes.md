# AI 味探针调研记录

> 本文记录 2026-10 ai-taste 病征体系两次调研的来源、分类轴分析与候选探针台账。它是探索记录，与技能正文无关：技能正文只保留当前有效状态，这里保留演进时间线与落选裁定，供复审与后续扩格引用。

## 一、来源清单

### 学术与量化

| 来源 | 内容 |
|------|------|
| Kobak et al.，arXiv 2406.07016（Science Advances 2025） | 超额词汇法：1500 万篇 PubMed 摘要 pre/post-LLM 对比，delve、intricate、pivotal 等词超额暴涨，估算 2024 年 13.5% 摘要经 LLM 处理 |
| Liang et al.，arXiv 2403.07183 | 同法打学术同行评审语料：commendable、notable 等 |
| Antislop（Samuel Paech，ICLR 2026，openreview gLcyM1khyp） | 对 2000 生成样本做词/bigram/trigram 超额统计，画模型专属 slop 指纹；部分模式超人类基线 1000 倍；Elara 超额 8.5 万倍 |
| EQ-Bench Slop Score | 超额词 60% + “not X but Y”对比句式 25% + slop trigram 15% |
| sepia research/rhythm-syntax.md | 裁定档案：破折号千字率因模型而异（GPT-4.1 10.62、GPT-5.4 1.43、Llama 0，属 release 属性非通用 tell）；段落绝对长度跨语料矛盾不进指纹，篇内一致性保留；主题句位置规律仅质性描述不进；burstiness 无公式且已停用不进 |
| sepia skills/sepia/references/discourse-pass.md | 篇章级证据卷：QUD 线性面试（后果/程序类段落约 19%，比较/验证类 0.2–0.3%，QUDsim/COLM 2025）；书挡最像人、中段露馅（Tripto/EMNLP 2025）；位置特征经全文改写反而更显眼（Russell/ACL 2025）；大纲测试（首句连读成摘要即机器形） |
| UCC 文体计量研究（Nature HSSC 2025） | AI 创意写作文风“窄而均匀”，人类风格范围远大于模型 |
| 日语超额词研究（Zenodo 2026） | 7 模型 1684 候选筛出 651 个显著超额词，方法跨语言可迁移 |
| Beyond Checkmate（EMNLP 2025） | 开头/主体/结尾三段signature不同，中段是 choke point |

### 工程化清单

| 来源 | 特色 |
|------|------|
| Wikipedia:Signs of AI writing（英）；中文维基《AI 生成文的特徵》 | 两语社群维护的主清单 |
| adam-s/grammar docs/signs-of-ai-slop.md | 五处三段即病；系动词回避（serves as 族）、假过渡、同源声腔、居高临下 |
| rampstackco editorial-qa ai-content-audit-patterns | 11 tells 带阈值（破折号 8 处/千字、however 4+ 次/1500 词）、幻觉六式、声音漂移三段取样 |
| 38 種 AI 寫作痕跡（Raymondhou0917/speak-human-tw，繁中） | 中文维基+朱宥勳 AI 腔分析，38 条全带误杀边界；立场真空、假坦白钩子、金句公式、罐头反应镜头 |
| VincentOld/stop-slop-zh structures.md | 三件套排比（中文最强指纹，六模板）、总分总八股、段落等长、节奏单调 |
| ai-zixun/humanizer-zh patterns.md | 口号化收束、预告式收尾、编号枚举撑全文、首中尾脱节、文章级默认形状（定义→分点→拔高） |
| tance-mang/chinese-webnovel-skills | 12 项量化指标带阈值（比喻密度 ≤3/千字、连续同句式 ≥3 报警、句长波动 ≥3 倍）；无缘无故的修辞（头号病）、语域错位引用 |
| joshuadavidthomas ai-writing-tropes tone.md | 假悬念过渡（“Here's the thing”）、居高临下类比（“把它想象成”） |
| bjcoombs deslop full-checklist | 过渡副词只在扎堆时算；系动词回避细分（A1 抬意义 vs B7 平句替换） |
| Mathews-Tom/armory detection-patterns | 17 patterns 带“weak alone”分级与改写例 |
| yfge/salt-story anti-ai.md | 底层五根因：均值回归、对称性、情感正确性、无损信息传递、视角稳定性 |
| 其他 | cc-polymath detect_slop.py（正则分级）、hedgehog tells-detector（lint gate）、shir-danishyar/humanize 词表（世代漂移标注）、humzakt/ai-writing-markers（HF 数据集）、Firefox LLM Slop Detector（隐形 Unicode）、writinglint-rulepack-ai-style、chrisgherbert gist、diglot.ai |

### 中文评论与报道

社科院简圣宇《智能写作的“AI味”问题》（安全词偏好、万能格式、衔接词当虚假逻辑装饰）；科技日报引西班牙《国家报》（语言扁平化、过于正确）；36kr/新智元（鉴别攻略失效、厂商按公开探针降频）；中时引 Threads 众测（中文新指纹“稳/撑/懂”、段内句号过密）；阿里云开发者社区（后训练概率抹平成因说）。

### 反方与失效警告

FT《No, you can't tell》（每条 tell 人类也用）；模型世代漂移（delve 2024 退潮、OpenAI 2025-11 破折号可关）；维基清单内部张力；检测器公司自承不可靠。结论：词面探针有保质期，位置与结构探针抗改写。

## 二、分类轴分析

入选判据：服务工作流真实阶段、改变审计动作、不制造双计。

| 轴 | 分格 | 服务阶段 | 裁定 |
|----|------|----------|------|
| A 位置/判定单元 | 句内/句间/段内/篇章 | 扫描 | 采纳 |
| B 判定方式 | 定点检查/通读语感 | 扫描 | 采纳（风格组） |
| C 语言学层次 | 词汇/句法/语义/修辞/语用 | 理解教学 | 不设组：病征名已隐性携带 |
| D 判定机制 | 存在匹配/密度计数/关系检查/分布统计/替换测试 | 工具化 | 记档：配 lint 时启用 |
| E 修复动作 | 删/换/拆/并/补/重排 | 改写 | 不设组：改写红线与逐条手法已承载 |
| F 置信度分级 | 铁证/强信号/弱信号 | 报告分级 | 不设组：豁免线统一管辖 |
| G 生成成因 | 均值回归/RLHF 讨好/模板复用 | 病理解释 | 不设组：越“不判作者身份”界，世代警告已承载 |
| H 文体轨 | 网文/公文/学术 | 范围扩展 | 需求出现再议 |

收敛结论：双轴（判定单元 × 判定方式）定稿，结构为格在上、文体做标签：篇章/段内/句间/句内/风格五格；通用条两体通用，专属条打文体标签，提示词文档跳过段内与风格格。共病合并：报幕过渡、缓冲词、翻译腔、系动词回避、意义膨胀五条两体通用，条目从 43 收敛到 38，交叉引用清零。归格规则：按判定单元归格，统计窗口留在判定动作里。

## 三、候选探针台账（含落选裁定）

### 已采纳

| 探针 | 格 | 出处 | 落选出处备注 |
|------|----|------|--------------|
| 结构可预测 | 散文·篇章 | sepia 大纲测试+QUD；humanizer-zh 默认形状 | 首中尾脱节并入此条 |
| 分布均匀 | 散文·篇章 | sepia（篇内一致性）；stop-slop-zh | 声音漂移、中段塌陷并入此条 |
| 编号枚举撑全文 | 散文·篇章 | humanizer-zh | —— |
| 口号化收束与金句铸句 | 散文·段内 | humanizer-zh、stop-slop-zh、speak-tw | —— |
| 时代帽开场 | 散文·段内 | speak-tw、adam-s、社科院 | —— |
| 系动词回避 | 散文·句内 + 提示词轨变体 | speak-tw、adam-s、bjcoombs B7 | —— |
| 语域单调 | 散文·风格 | UCC、sepia/EMNLP 2025、科技日报 | —— |
| 修辞无目的 | 散文·风格 | webnovel 头号病；预防块比喻三问病征化 | —— |
| 词汇同质化 | 散文·风格 | 社科院、科普中国 | —— |
| 假坦白钩子 | 并入假口语 | speak-tw | —— |
| 解说导引 | 并入总结填充 | speak-tw | —— |
| 短句轰炸 | 并入句式死板 | speak-tw、stop-slop-zh | —— |
| 假悬念过渡 | 并入报幕过渡 | tone.md、adam-s | —— |

### 落选（含理由）

| 候选 | 理由 |
|------|------|
| 英文超额词表（delve 族） | 世代窗口会烂；词面特征抗改写性差；清单以密度结构判据为主是刻意选择 |
| 幻觉六式 | 越界成事实核查，非文风 |
| 工具残留（utm、占位符） | 是作者身份证据，越“不判身份”自我声明 |
| 预告式收尾 | 密度价值不足，单次有牵引作用 |
| 语域错位引用 | 散文场景偏窄，网文场景才高频，需求出现再议 |
| 分词尾巴抬意义 | 意义拔高与意义膨胀现有判定已覆盖 |
| 首中尾脱节、段落节奏模板、三项列表偏好 | 分别由结构可预测、分布均匀覆盖，不双计 |
| 网文 12 项量化指标 | 网文超出当前两轨范围，H 轴需求再议 |
| 中文新词指纹（稳/撑/懂） | 词面探针，观察项不收 |

## 四、决策时间线

- 2026-10-22 一轮：全仓 AI 味审计（grilling 3 处、writing-for-agents 16 处、ai-taste 2 处），24 处修毕并回流部署。
- 2026-10-22 二轮：探针互联网调研与分类设计。采纳双轴五组；散文轨 16 → 26 条，提示词轨 17 条重排不动内容；世代警告入豁免线；三处变体并入；预防块与 frontmatter description 不动。
- 2026-10-22 三轮：共病审计发现五对两体通用条目（报幕过渡、缓冲词、翻译腔、系动词回避、意义膨胀），结构翻转为格在上、文体做标签，条目 43 → 38，交叉引用清零。
- 落选分类轴见第二节；落选探针见第三节。
