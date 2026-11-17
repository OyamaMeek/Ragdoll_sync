# 请基于以下 Obsidian Vault 盘点，

来源：dsh

项目：/Users/oyamahappa/Documents/Obsidian/Happa

## user · 2026-09-28T15:40:50Z

请基于以下 Obsidian Vault 盘点，独立分析哪些文件适合从 RAG 检索中排除、哪些重复文件可合并/标记、哪些内容有时效/安全/个人隐私风险。不要修改文件，只输出分组建议与理由。

当前工作区是一个 Obsidian Vault，约 192 个 Markdown 文件，其中 188 个内容笔记、4 个 .claudian 运行记录；主要主题目录：AI编程与Agent工具(41)、大学学习与校园生活(24)、网络安全(14)、求职就业与职场(14)、计算机与电子信息专业(13)、考研与升学(13)等。现状：内容笔记均无真正的 YAML frontmatter；大多有 H1/H2/H3 结构；存在 5 组同名重复文件（GitHub开源宝藏与实用工具汇总、Git的正确使用姿势与最佳实践、Skill、节点自动填充器、AI Agent Codex 热门Skill整理），其中前两组和 Skill 完全重复；有 1 个空文件“个人杂记与待分类/未命名.md”；有根目录日记 260808.md、260819.md、根目录 Skill.md、已安装skill.md、GFW 调查简报等混合内容。收件箱.md 已基本完成归档索引。目标是提高 RAG 问答质量，优先安全、可回滚、少破坏。
Your parent agent id is "session-fd9154ab-8dc3-4add-a39c-b32ebab83182". Before you finish, send your result to that agent with send_message({ agent_id: "session-fd9154ab-8dc3-4add-a39c-b32ebab83182", message: "<self-contained result>" }). The parent shares your workspace but does not automatically receive your transcript, tool output, or reasoning. Send earlier messages as well when a finding changes what the parent should do next; sending a message does not end your turn.

## assistant · 2026-09-28T15:42:01Z

**Planning structured inventory analysis**

**Classifying inventory groups for RAG policy**

**Excluding logs and empty files from RAG**
**Defining exclusion criteria for duplicates and skill docs**

**Classifying sensitive and personal note exclusions**

**Proposing canonical merge for exact duplicates**
**Planning merging of skill documentation**

**Classifying and separating skill and diary notes**

**Labeling and sanitizing sensitive operational notes**
**Planning secret scanning and redaction**

**Designing metadata and collection filters**
{
  "type": "tool-call",
  "id": "call_JoI2gmbLyY6A70eoslnyOnnG|fc_0ff7712d5500a313016aba8aa8c4b887d0a9ff648fd2132a54",
  "name": "run_code",
  "arguments": "{\"code\":\"const msg = `基于用户给出的 Vault 盘点（未读取/修改文件），建议将 RAG 设计成“默认公共知识库 + 独立受控集合”，优先排除噪音、可变内容和敏感内容；不建议现在删除任何文件。\\\\n\\\\n一、建议从“默认 RAG”排除（保留原文件，按路径/集合排除，完全可回滚）\\\\n1) 4 个 .claudian 运行记录：运行日志、提示词/工具调用/路径/会话信息可能泄露，且重复噪声大；默认不嵌入。\\\\n2) 个人杂记与待分类/未命名.md：空文件无检索收益；若以后写入个人内容，仍应进入个人/私有集合。\\\\n3) 同名重复文件中的非主副本：至少“GitHub开源宝藏与实用工具汇总”“Git的正确使用姿势与最佳实践”“Skill”已知完全重复；非主副本排除，避免答案重复和版本混淆。\\\\n4) 根目录日记 260808.md、260819.md：默认不检索；日记可能含位置、作息、关系、健康等个人隐私。仅在明确开启个人上下文时单独检索。\\\\n5) 已安装skill.md：更像当前环境/安装状态清单，快速过期，通常不应作为一般知识回答来源；若有用，置于“工具状态/配置”集合并低权重、按日期检索。\\\\n6) 收件箱.md：既然基本完成归档且主要是索引/链接，建议不做普通语义向量；保留作为导航/元数据或单独低权重索引，避免检索到目录标题而不是正文。\\\\n7) GFW 调查简报：默认从通用问答排除，放入“安全/敏感/时效”受控集合；涉及网络、法律/政策、地缘政治和可能的操作性内容，须按权限、日期、来源检索。\\\\n8) 任何实际含 API key、token、密码、Cookie、SSH 私钥、内部 URL/IP、个人证件/学号、电话邮箱、住址、求职材料等的笔记：发现后先隔离/脱敏，再决定是否索引；不要仅靠文件名判断。\\\\n\\\\n二、重复文件的合并/标记策略（先比对、后合并；不物理删除）\\\\n- 完全重复的三组：各选一份“规范主文档”（优先内容完整、链接稳定、位置符合主题的版本）；其它路径标记 duplicate_of/别名并从 RAG 排除。若有 Obsidian 反向链接，保留原文件或建立重定向占位，待链接审计后再处理。\\\\n- “节点自动填充器”“AI Agent Codex 热门Skill整理”：仅知道同名重复，不能直接判定完全相同。逐段比较：主文档保留最新/最完整版本，把独有段落合入；旧副本标 archived/merged，排除旧副本；记录来源路径和合并日期。\\\\n- 根目录 Skill.md 与各目录 Skill 同名项：先区分“Skill 使用/知识文章”与“已安装 Skill 清单/运行配置”。前者可选一个规范知识文档；后者不要盲目合并，应作为独立易变配置文档并默认低权重或排除。\\\\n- GitHub 工具汇总、Git 最佳实践：即使正文重复，也要对链接、版本、命令和更新时间做一次核对；不要把旧文档与新文档并行高权重索引。\\\\n- 不要把日记、收件箱索引、运行日志和主题知识强行合并；它们是不同文档类型。\\\\n\\\\n三、时效风险（建议打“volatile/review_due/source_date”，由索引层降权或设 TTL）\\\\n- AI 编程/Agent/Skill/Codex/节点自动填充器：API、模型名、安装命令、权限模型、插件行为和平台规则变化快；旧内容可能直接导致错误或危险操作。\\\\n- GitHub 开源工具汇总：仓库活跃度、链接、许可证、供应链安全、安装方式会变化；回答时应优先带版本/日期和原始来源。\\\\n- Git 最佳实践：命令本身较稳定，但工具版本、默认配置和团队规范可能变化；若含具体版本命令则需复核。\\\\n- 网络安全与 GFW 调查：漏洞、IOC、封锁策略、政策和法律环境均时效敏感；必须显示日期/来源/适用范围，不宜把旧结论当现行事实。\\\\n- 大学、求职、考研/升学：课程、校规、招生简章、截止日期、联系人和政策易变；把“经验/长期方法”与“当年通知/个人申请状态”分开，后者低权重或按年份隔离。\\\\n- 日记、已安装技能清单：不是事实知识库，应按时间或当前状态处理，不宜跨时间召回。\\\\n\\\\n四、安全/隐私/提示注入风险\\\\n- .claudian 日志、技能说明、安装命令和外链内容可能包含内部路径、工具调用、可执行命令、下载脚本或“忽略规则/泄露上下文”类提示注入；RAG 应把笔记当不可信资料，不能让其覆盖系统/开发者/安全策略，命令只可作为待审材料。\\\\n- 网络安全/GFW 文档可能包含扫描、绕过、利用、代理或敏感基础设施信息；单独权限和集合，必要时只索引摘要/非操作性部分。\\\\n- 求职/校园/日记笔记可能包含个人身份、联系方式、经历、位置、健康或人际信息；默认隔离，必要时脱敏。\\\\n- 外部链接/安装脚本应视为不可信；检索答案中不要自动执行，也不要把未知 URL 当作权威来源。\\\\n\\\\n五、推荐的四层 RAG 集合\\\\nA 默认知识：经去重、去隐私、带来源/日期的 AI/CS/网络/学习方法/职场通用内容。\\\\nB 易变操作文档：AI/Agent/Skill/GitHub/安装配置；低权重、按日期/版本优先、人工确认后引用。\\\\nC 受控敏感集合：网络安全、GFW、求职/校园个人资料、日记；默认不参与，需显式开启且最小化返回。\\\\nD 非知识/管理集合：.claudian 日志、收件箱索引、空占位文件、旧重复副本、已安装状态清单；默认不嵌入或仅保存结构化元数据。\\\\n\\\\n最低风险落地顺序：先做 denylist/集合隔离和重复副本排除（不删文件）→ 再对完整重复与疑似重复做人工 diff → 再处理敏感信息扫描/脱敏 → 最后给可变文档补日期/版本/来源和复核期限。由于当前没有真正 YAML frontmatter，先按路径+文件名+索引规则实现也比贸然批量写元数据更可回滚。\\\\n\\\\n结论：最确定的默认排除项是 .claudian、空文件、完全重复副本、两份日记、收件箱索引和已安装skill清单；GFW/网络安全及含个人或秘密信息的内容应进入受控集合而非简单删除。`;\\nawait tools.send_message({agent_id:\\\"session-fd9154ab-8dc3-4add-a39c-b32ebab83182\\\", message:msg});\\nreturn \\\"已将分组建议、重复处理策略与时效/安全/隐私风险发送给父代理。\\\";\",\"description\":\"Send RAG exclusion and risk analysis\"}"
}

## tool · 2026-09-28T15:42:01Z

run_code
{"code":"const msg = `基于用户给出的 Vault 盘点（未读取/修改文件），建议将 RAG 设计成“默认公共知识库 + 独立受控集合”，优先排除噪音、可变内容和敏感内容；不建议现在删除任何文件。\\n\\n一、建议从“默认 RAG”排除（保留原文件，按路径/集合排除，完全可回滚）\\n1) 4 个 .claudian 运行记录：运行日志、提示词/工具调用/路径/会话信息可能泄露，且重复噪声大；默认不嵌入。\\n2) 个人杂记与待分类/未命名.md：空文件无检索收益；若以后写入个人内容，仍应进入个人/私有集合。\\n3) 同名重复文件中的非主副本：至少“GitHub开源宝藏与实用工具汇总”“Git的正确使用姿势与最佳实践”“Skill”已知完全重复；非主副本排除，避免答案重复和版本混淆。\\n4) 根目录日记 260808.md、260819.md：默认不检索；日记可能含位置、作息、关系、健康等个人隐私。仅在明确开启个人上下文时单独检索。\\n5) 已安装skill.md：更像当前环境/安装状态清单，快速过期，通常不应作为一般知识回答来源；若有用，置于“工具状态/配置”集合并低权重、按日期检索。\\n6) 收件箱.md：既然基本完成归档且主要是索引/链接，建议不做普通语义向量；保留作为导航/元数据或单独低权重索引，避免检索到目录标题而不是正文。\\n7) GFW 调查简报：默认从通用问答排除，放入“安全/敏感/时效”受控集合；涉及网络、法律/政策、地缘政治和可能的操作性内容，须按权限、日期、来源检索。\\n8) 任何实际含 API key、token、密码、Cookie、SSH 私钥、内部 URL/IP、个人证件/学号、电话邮箱、住址、求职材料等的笔记：发现后先隔离/脱敏，再决定是否索引；不要仅靠文件名判断。\\n\\n二、重复文件的合并/标记策略（先比对、后合并；不物理删除）\\n- 完全重复的三组：各选一份“规范主文档”（优先内容完整、链接稳定、位置符合主题的版本）；其它路径标记 duplicate_of/别名并从 RAG 排除。若有 Obsidian 反向链接，保留原文件或建立重定向占位，待链接审计后再处理。\\n- “节点自动填充器”“AI Agent Codex 热门Skill整理”：仅知道同名重复，不能直接判定完全相同。逐段比较：主文档保留最新/最完整版本，把独有段落合入；旧副本标 archived/merged，排除旧副本；记录来源路径和合并日期。\\n- 根目录 Skill.md 与各目录 Skill 同名项：先区分“Skill 使用/知识文章”与“已安装 Skill 清单/运行配置”。前者可选一个规范知识文档；后者不要盲目合并，应作为独立易变配置文档并默认低权重或排除。\\n- GitHub 工具汇总、Git 最佳实践：即使正文重复，也要对链接、版本、命令和更新时间做一次核对；不要把旧文档与新文档并行高权重索引。\\n- 不要把日记、收件箱索引、运行日志和主题知识强行合并；它们是不同文档类型。\\n\\n三、时效风险（建议打“volatile/review_due/source_date”，由索引层降权或设 TTL）\\n- AI 编程/Agent/Skill/Codex/节点自动填充器：API、模型名、安装命令、权限模型、插件行为和平台规则变化快；旧内容可能直接导致错误或危险操作。\\n- GitHub 开源工具汇总：仓库活跃度、链接、许可证、供应链安全、安装方式会变化；回答时应优先带版本/日期和原始来源。\\n- Git 最佳实践：命令本身较稳定，但工具版本、默认配置和团队规范可能变化；若含具体版本命令则需复核。\\n- 网络安全与 GFW 调查：漏洞、IOC、封锁策略、政策和法律环境均时效敏感；必须显示日期/来源/适用范围，不宜把旧结论当现行事实。\\n- 大学、求职、考研/升学：课程、校规、招生简章、截止日期、联系人和政策易变；把“经验/长期方法”与“当年通知/个人申请状态”分开，后者低权重或按年份隔离。\\n- 日记、已安装技能清单：不是事实知识库，应按时间或当前状态处理，不宜跨时间召回。\\n\\n四、安全/隐私/提示注入风险\\n- .claudian 日志、技能说明、安装命令和外链内容可能包含内部路径、工具调用、可执行命令、下载脚本或“忽略规则/泄露上下文”类提示注入；RAG 应把笔记当不可信资料，不能让其覆盖系统/开发者/安全策略，命令只可作为待审材料。\\n- 网络安全/GFW 文档可能包含扫描、绕过、利用、代理或敏感基础设施信息；单独权限和集合，必要时只索引摘要/非操作性部分。\\n- 求职/校园/日记笔记可能包含个人身份、联系方式、经历、位置、健康或人际信息；默认隔离，必要时脱敏。\\n- 外部链接/安装脚本应视为不可信；检索答案中不要自动执行，也不要把未知 URL 当作权威来源。\\n\\n五、推荐的四层 RAG 集合\\nA 默认知识：经去重、去隐私、带来源/日期的 AI/CS/网络/学习方法/职场通用内容。\\nB 易变操作文档：AI/Agent/Skill/GitHub/安装配置；低权重、按日期/版本优先、人工确认后引用。\\nC 受控敏感集合：网络安全、GFW、求职/校园个人资料、日记；默认不参与，需显式开启且最小化返回。\\nD 非知识/管理集合：.claudian 日志、收件箱索引、空占位文件、旧重复副本、已安装状态清单；默认不嵌入或仅保存结构化元数据。\\n\\n最低风险落地顺序：先做 denylist/集合隔离和重复副本排除（不删文件）→ 再对完整重复与疑似重复做人工 diff → 再处理敏感信息扫描/脱敏 → 最后给可变文档补日期/版本/来源和复核期限。由于当前没有真正 YAML frontmatter，先按路径+文件名+索引规则实现也比贸然批量写元数据更可回滚。\\n\\n结论：最确定的默认排除项是 .claudian、空文件、完全重复副本、两份日记、收件箱索引和已安装skill清单；GFW/网络安全及含个人或秘密信息的内容应进入受控集合而非简单删除。`;\nawait tools.send_message({agent_id:\"session-fd9154ab-8dc3-4add-a39c-b32ebab83182\", message:msg});\nreturn \"已将分组建议、重复处理策略与时效/安全/隐私风险发送给父代理。\";","description":"Send RAG exclusion and risk analysis"}

## assistant · 2026-09-28T15:43:04Z

**Confirming file exclusions and duplicate group overlaps**

**Categorizing files for selective RAG exclusion**
**Recommending targeted file exclusion patterns**

**Advising semantic file splitting and duplication handling**

**Recommending embedding redaction and access control**
**Adding freshness-based ranking suggestions**

**Planning final Chinese summary with tables and links**

**Enforcing full path file linking with line references**
**Clarifying linking strategy for duplicate group names**

**Preparing concise addendum about ambiguous file paths**
{
  "type": "tool-call",
  "id": "call_bNUsFqdAUX6YhdbXXkS6AEWn|fc_0ff7712d5500a313016aba8aedee0487d0b78858f40e23ef6a",
  "name": "run_code",
  "arguments": "{\"code\":\"await tools.send_message({agent_id:\\\"session-fd9154ab-8dc3-4add-a39c-b32ebab83182\\\", message:\\\"补充关键边界：根目录混合内容不要按目录粗暴全排；应按文档类型/段落路由。若无法拆分，Skill/已安装清单走易变集合，GFW/安全走受控集合，日记走私有集合。收件箱保留导航功能但不做普通向量召回。对重复文件优先做内容 hash/逐段 diff，旧路径保留为别名或归档且 no-index，避免断掉 Obsidian 反向链接；不直接删除。\\\"});\\nreturn \\\"已发送混合文档路由与可回滚处理补充。\\\";\",\"description\":\"Send mixed-content routing addendum\"}"
}

## tool · 2026-09-28T15:43:04Z

run_code
{"code":"await tools.send_message({agent_id:\"session-fd9154ab-8dc3-4add-a39c-b32ebab83182\", message:\"补充关键边界：根目录混合内容不要按目录粗暴全排；应按文档类型/段落路由。若无法拆分，Skill/已安装清单走易变集合，GFW/安全走受控集合，日记走私有集合。收件箱保留导航功能但不做普通向量召回。对重复文件优先做内容 hash/逐段 diff，旧路径保留为别名或归档且 no-index，避免断掉 Obsidian 反向链接；不直接删除。\"});\nreturn \"已发送混合文档路由与可回滚处理补充。\";","description":"Send mixed-content routing addendum"}

## assistant · 2026-09-28T15:43:57Z

**Outlining detailed Chinese response with tables**

**Categorizing duplicates and defining collection links**
**Assessing markdown link handling for duplicate filenames**

**Confirming markdown linking approach for files**
以下仅基于你提供的 Vault 盘点信息分析，未读取或修改任何文件。

## 一、建议从默认 RAG 中排除

| 对象 | 建议 | 理由 |
|---|---|---|
| 4 个 `.claudian` 运行记录 | 默认 `noindex` | 属于运行日志，可能含提示词、工具调用、工作区路径、会话信息，且对知识问答噪声较大 |
| [`个人杂记与待分类/未命名.md`](个人杂记与待分类/未命名.md) | 排除 | 当前为空，无检索价值；以后若写入内容，应归入个人私有集合 |
| 完全重复文件的非主副本 | 排除非规范副本 | 避免同一内容多次召回、版本冲突和答案重复；原文件先保留，不要直接删除 |
| [`260808.md`](260808.md)、[`260819.md`](260819.md) | 默认排除 | 日记可能包含位置、作息、健康、关系等个人隐私；仅在明确开启个人上下文时检索 |
| [`收件箱.md`](收件箱.md) | 不做普通向量检索 | 它主要是归档索引，适合作为导航或结构化元数据，而不是知识正文 |
| [`已安装skill.md`](已安装skill.md) | 默认低权重或排除 | 属于当前环境状态清单，变化快，不适合回答一般知识问题 |
| [`Skill.md`](Skill.md) | 视内容拆分 | 如果是 Skill 使用知识，可保留一个规范版本；如果是运行配置或安装说明，应归入易变配置集合 |
| [`GFW 调查简报.md`](GFW%20调查简报.md) | 不进入默认公共集合 | 具有安全、政策、法律和时效敏感性，应放入受控集合 |

另外，凡是实际包含以下信息的笔记，都应先隔离或脱敏，再决定是否建立嵌入：

- API Key、Token、密码、Cookie、SSH 私钥；
- 内部 IP、内部 URL、服务器信息；
- 身份证件、学号、手机号、邮箱、住址；
- 求职材料、校园个人信息、健康或人际关系信息。

## 二、重复文件的合并与标记建议

### 1. 可以确认完全重复的组

以下三组应优先人工确认后各选一个规范文档：

- [`GitHub开源宝藏与实用工具汇总.md`](GitHub开源宝藏与实用工具汇总.md)
- [`Git的正确使用姿势与最佳实践.md`](Git的正确使用姿势与最佳实践.md)
- [`Skill.md`](Skill.md)

建议：

1. 选择内容最完整、来源最清楚、链接最稳定的一份作为 canonical；
2. 其他副本标记为 `duplicate_of` 或 `archived`；
3. 非 canonical 副本从 RAG 排除；
4. 在确认 Obsidian 反向链接已处理前，不物理删除；
5. 如需保留原路径，可保留极短的重定向占位，但占位文件本身也应 `noindex`。

### 2. 需要逐段比较的组

以下两组不能仅根据同名直接判定完全重复：

- [`节点自动填充器.md`](节点自动填充器.md)
- [`AI Agent Codex 热门Skill整理.md`](AI%20Agent%20Codex%20热门Skill整理.md)

建议比较：

- 是否只是标题相同；
- 命令、版本、链接是否不同；
- 哪一份更新；
- 是否存在各自独有的步骤或风险说明。

若内容部分重叠，应把独有段落合入最新版本，旧文件标记为归档并排除，而不是让多个旧版本同时参与检索。

### 3. 不建议强行合并的文件

- 日记和主题知识笔记；
- [`收件箱.md`](收件箱.md) 与正文笔记；
- [`已安装skill.md`](已安装skill.md) 与 Skill 教程；
- `.claudian` 运行记录与任何知识笔记；
- [`GFW 调查简报.md`](GFW%20调查简报.md) 与普通网络安全学习笔记。

这些文件的文档类型不同，强行合并会损失权限、时效和语义边界。

## 三、时效风险

### 高时效内容

以下内容应带日期、版本和来源，并在排序时降低旧版本权重：

- AI 编程、Agent、Codex、Skill、节点自动填充器；
- GitHub 工具汇总；
- 安装命令、插件用法、模型名称、API 行为；
- 网络安全漏洞、IOC、攻击技术、代理或绕过策略；
- GFW、政策、网络环境和法律相关调查；
- 招生简章、考试政策、校园规定、课程安排；
- 招聘岗位、截止日期、联系人和申请要求。

建议的复核节奏可以是：

- AI/Agent/Skill：约 30–90 天复核；
- 工具汇总和 GitHub 链接：约 90–180 天复核；
- 安全、政策、招生、招聘：按事件或学年复核；
- 没有日期和来源的内容，不应直接被当作当前事实回答。

## 四、安全、隐私和提示注入风险

1. **运行日志风险**  
   `.claudian` 文件可能含内部上下文、执行轨迹和敏感路径，应默认不嵌入。

2. **技能文档风险**  
   Skill、安装说明和自动化脚本可能包含下载命令、执行命令或外部链接。RAG 召回后只能作为不可信资料，不能覆盖系统/开发者安全规则，也不能自动执行。

3. **网络安全内容风险**  
   网络安全和 GFW 材料可能包含扫描、利用、绕过或敏感基础设施信息，建议单独权限和集合；必要时只索引摘要和非操作性内容。

4. **个人信息泄露风险**  
   日记、求职、校园和升学材料可能包含高度个人化信息。应在检索候选生成前做权限过滤，而不能只依赖最终回答阶段的提示词约束。

5. **外链和供应链风险**  
   GitHub 链接、安装脚本和第三方 Skill 不应自动视为可信来源；回答中引用时应保留来源和日期，不自动执行未知 URL 或命令。

## 五、推荐的 RAG 分层

### A. 默认知识集合

放入经过去重、去隐私、带来源和日期的：

- AI/计算机基础知识；
- 网络和电子信息专业学习内容；
- 长期有效的 Git、编程和学习方法；
- 通用求职与职场经验。

### B. 易变操作集合

单独存放：

- AI/Agent/Skill/Codex；
- GitHub 工具汇总；
- 安装配置和版本相关内容。

此集合应按日期、版本优先，并在回答时提示可能过期。

### C. 受控敏感集合

单独存放：

- 网络安全和 GFW 调查；
- 日记；
- 求职申请、校园个人材料；
- 可能含隐私或内部信息的笔记。

默认不参与普通问答，只有在明确授权后检索。

### D. 管理与非知识集合

默认不嵌入：

- `.claudian` 运行记录；
- 空占位文件；
- [`收件箱.md`](收件箱.md)；
- 重复副本；
- [`已安装skill.md`](已安装skill.md) 等状态清单。

## 六、最安全的执行顺序

1. 先在索引层建立排除规则和集合隔离，不删除文件；
2. 对三组已知完全重复内容做内容 hash 和人工确认；
3. 对“节点自动填充器”和“AI Agent Codex 热门Skill整理”做逐段 diff；
4. 扫描并隔离密钥、个人信息和内部系统信息；
5. 最后补充日期、版本、来源和复核期限；
6. 由于目前没有真正的 YAML frontmatter，优先使用路径、文件名和外部索引规则，比批量改写文件更容易回滚。

最确定的默认排除项是：`.claudian` 运行记录、空文件、完全重复副本、两份日记、收件箱索引和已安装 Skill 状态清单。网络安全、GFW、求职/校园个人内容则更适合进入受控集合，而不是直接删除。
