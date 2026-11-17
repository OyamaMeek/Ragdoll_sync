# 修复项目问题

来源：codex

项目：/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse

## developer · 2026-10-19T12:28:50Z

<skills_instructions>
## Skills
A skill is a set of local instructions to follow that is stored in a `SKILL.md` file. Below is the list of skills that can be used. Each entry includes a name, description, and a short path that can be expanded into an absolute path using the skill roots table.
### Skill roots
- `r0` = `/Users/oyamahappa/.codex/skills`
- `r1` = `/Users/oyamahappa/.agents/skills`
- `r2` = `/Users/oyamahappa/.codex/skills/.system`
- `r3` = `/Users/oyamahappa/.codex/plugins/cache/ars-codex`
- `r4` = `/Users/oyamahappa/.codex/plugins/cache/openai-bundled`
- `r5` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote`
- `r6` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.22/skills`
- `r7` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.1/skills`
- `r8` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/6.4.2/skills`
- `r9` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r10` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r11` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1015.12040/skills`
- `r12` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.2/skills`
- `r13` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r14` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.12.4/skills`
- `r15` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.0/skills`
- `r16` = `/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex/.agents/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI-created bitmap visuals such as photos, illustrations, textures, sprites, mockups, or transparent-background cutouts. Use when Codex should create a brand-new image, transform an existing image, or derive visual v (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, settings, setup, troubleshooting, customization, automations, and self-knowledge—including 'you,' 'your,' 'this app,' or 'this coding agent' when they refer to Codex—and for OpenAI APIs/products and ChatGPT Work. Also use (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped instructions and any needed supporting resources. (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list or a GitHub repo path. Use when a user asks to list installable skills, install a curated skill, or install a skill from another repo (including private repos). (file: r2/skill-installer/SKILL.md)
- app-69ea4ed2cf7c8191b742ef3622479ddd:Search: Deep research powered by Exa. Use for lead generation, literature reviews, deep dives, competitive analysis, or any query where one search falls short, including phrases like 'research this', 'find everything about', 'find me all', or 'deep dive on'. (file: r5/app-69ea4ed2cf7c8191b742ef3622479ddd/4.0.1/skills/Search/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, translated for the web. Use when building or reviewing gesture-driven UI, spring animations, drag/swipe/sheet interactions, momentum and interruptible transitions, translucent materials and depth, typography ( (file: r1/apple-design/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, translated for the web. Use when building or reviewing gesture-driven UI, spring animations, drag/swipe/sheet interactions, momentum and interruptible transitions, translucent materials and depth, typography ( (file: r0/apple-design/SKILL.md)
- archify: Create polished, validated architecture, workflow, sequence, data-flow, and lifecycle/state diagrams as explorable standalone HTML with inline SVG, dark/light themes, optional trace motion, and PNG/JPEG/WebP/SVG/WebM export. Accept plain-language requirements or pasted Mermai (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Codex research, writing, manuscript review, study screening, and experiments. Use for deep research, literature or systematic reviews, meta-analysis, research questions, drafts, revisions, roadmaps, abstracts, citations, integrity checks, peer review, research-to-paper. (file: r3/ars-codex/3.23.1/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Structures Benchmark and Evaluation papers using the five-pillar framework (Research Gap, Construction Pipeline, Evaluation Framework, Empirical Findings, optional Companion Method). Returns a completeness audit, a six-part Introduction logic chain, a Section 2-7 skeleton,  (file: r0/benchmark-paper-template/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end brand-guidelines boards, logo systems, identity decks, and visual-world presentations. Trained for minimalist, cinematic, editorial, dark-tech, luxury, cultural, security, gaming, developer-tool, and consumer-ap (file: r0/brandkit/SKILL.md)
- chrome-devtools-cli: Use this skill to write shell scripts or run shell commands to automate tasks in the browser or otherwise use Chrome DevTools via CLI. (file: r16/chrome-devtools-cli/SKILL.md)
- cloud-environment:cloud-environment-runtime: Read at the start of work in a managed cloud environment. Inspect network policy and configured credentials; build and run Docker containers with the session proxy and CA trust; use Tailscale VPN access, configure TCP forwarding, and diagnose access failures. (file: r5/cloud-environment/0.1.2/skills/runtime/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准备最小可验证改动，经用户逐项确认后 fork、push、提交 PR，并跟踪 CI、review 和合并状态；当用户输入“/contributor”、想寻找项目、做 first contribution 或提交 PR 时使用。 (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Convert Word (.doc, .docx), PowerPoint (.ppt, .pptx), Excel (.xls, .xlsx), OpenDocument (.odt, .ods, .odp), RTF, EPUB, CSV, and PDF files to GitHub-Flavored Markdown. Use when a task needs the contents of an office document, spreadsheet, presentation, ebook, or PDF you cannot (file: r1/convert-documents-to-markdown/SKILL.md)
- deep-research: Runs a deep, survey-grade literature investigation on a research topic: freezes research questions, searches from multiple adversarial perspectives, verifies every citation, synthesizes evidence into a MECE taxonomy with in-sentence cross-comparison, and answers the research  (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for websites, distilled from a study of 247 curated gallery sites (One Page Love, Awwwards Sites of the Day). Deals researched directions (idea, composition, type, palette, photographs, section blueprints) from a li (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects depending on its exact behavior. The current default is `design-taste-frontend` (v2), which is a new skill. Use this v1 install name only if you need exact backward compatibility. (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-driven version, preserved for projects depending on its exact behavior. The current default is `design-taste-frontend` (v2). Use this install name only if you need the earlier behavior. Anti-slop frontend rules for  (file: r0/taste-skill-v2-experimental/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Google Docs-targeted document artifacts inside the container, with a strict render-and-verify workflow. Use `render_docx.py` to generate page PNGs (and optional PDF) for visual QA, then iterate until layout is flawles (file: r10/documents/26.1015.12040/skills/documents/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable Draw.io files with rendered previews: native Draw.io elements carry text and structure, SVG covers simple icons that match the reference, and cropped or transparent PNGs preserve complex visuals. Use when the user wan (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable draw.io diagrams. Use when the user explicitly requests draw.io/diagrams.net, needs a polished architecture, ERD, UML, sequence, C4, SysML, BPMN, network, swimlane, ML, or infrastructure diagram, wants code/IaC/ (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it to open and operate websites, fill forms, click buttons, take screenshots, extract page data, sign in, and perform other browser automation tasks, as well as web app testing, dogfooding, QA, bug investigation, and ap (file: r1/ego-browser/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用户运行 /evidence-recap、$evidence-recap，或明确要求复盘 AI 编程过程、交付记录、落地状态和证据缺口时使用；仅需简历改写、源码导学或模拟面试时不使用。 (file: r0/evidence-recap/SKILL.md)
- figure-designer: Advises on the design of the three core figures in a technical paper: the Motivated Example (Figure 1), the Solution Overview (Methodology), and the Experimental Results figures. Recommends the right design paradigm, layout, labelling, and tool for each figure type, then runs (file: r0/figure-designer/SKILL.md)
- full-output-enforcement: Overrides default LLM truncation behavior. Enforces complete code generation, bans placeholder patterns, and handles token-limit splits cleanly. Apply to any task requiring exhaustive, unabridged output. (file: r0/output-skill/SKILL.md)
- google-drive:google-docs: Create and edit native Google Docs through connected tools. (file: r6/google-docs/SKILL.md)
- google-drive:google-drive: Use connected Google Drive as the single entrypoint for Drive, Docs, Sheets, and Slides work. Use when the user wants to find, fetch, organize, share, export, copy, or delete Drive files, or summarize and edit Google Docs, Google Sheets, and Google Slides through one unified G (file: r6/google-drive/SKILL.md)
- google-drive:google-drive-comments: Write, reply to, and resolve Google Drive comments on Docs, Sheets, Slides, and Drive files with evidence-backed location context. Use when the user asks to leave comments, review a file with comments, respond to comment threads, or resolve Drive comments. (file: r6/google-drive-comments/SKILL.md)
- google-drive:google-sheets: Analyze and edit connected Google Sheets with range precision. Use when the user wants to create Google Sheets, find a spreadsheet, inspect tabs or ranges, search rows, plan formulas, create or repair charts, clean or restructure tables, write concise summaries, or make expl (file: r6/google-sheets/SKILL.md)
- google-drive:google-slides: Route Google Slides authoring requests and derive a design system from a native template or reference deck. Use this skill when the user provides an existing native Google Slides deck as a template, reference, or prior-period source, or asks to edit, update, repair, restyle, (file: r6/google-slides/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt templates from the awesome-gpt-image-2 style library. Use when an agent needs to create, rewrite, classify, or improve image-generation prompts with repository-backed templates, categories, style tags, scene  (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt templates from the awesome-gpt-image-2 style library. Use when an agent needs to create, rewrite, classify, or improve image-generation prompts with repository-backed templates, categories, style tags, scene  (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Elite UX/UI & Advanced GSAP Motion Engineer. Enforces Python-driven true randomization for layout variance, strict AIDA page structure, wide editorial typography (bans 6-line wraps), gapless bento grids, strict GSAP ScrollTriggers (pinning, stacking, scrubbing), inline micro (file: r0/gpt-tasteskill/SKILL.md)
- great-resume: 中文求职经历提升技能：根据目标岗位把真实经历重组为岗位定位、简历要点、项目亮点和 HR 开场白；当用户输入“/great-resume”“我要酥化”或“简历提升”、要求包装或改写经历、项目，或写 HR 自我介绍时使用。若用户明确要求“阿酥同款”、复刻简历模板或生成对应 HTML/PDF，则交给 /make-resume。 (file: r0/great-resume/SKILL.md)
- high-end-visual-design: Teaches the AI to design like a high-end agency. Defines the exact fonts, spacing, shadows, card structures, and animations that make a website feel expensive. Blocks all the common defaults that make AI designs look cheap or generic. (file: r0/soft-skill/SKILL.md)
- human-writing: 通用中文创作与改稿 Skill。用于知乎回答、论坛长帖、公众号文章、博客、评论、人物故事、历史叙事、新闻与行业解读、科普、教程、评测、个人叙事、小说、故事、对白、口播和演讲稿。默认写成一个见过事、查过材料、愿意把来龙去脉讲清楚的人在说话，重点保留中文互联网长回答与长帖的活人感和自然中文韵律，避免空泛的机构腔、喊口号式演说腔、营销腔和模型腔。非虚构长文先检查材料够不够，材料不足时研究、追问或缩短，绝不用重复解释灌字数。现实内容额外核验事实、引语、数据与用户亲历，虚构内容可以创造人物、场景、对白、心理与情节。成稿正文严禁冒号、破折号、“不是……而 (file: r0/human-writing/SKILL.md)
- idea-evaluator: Evaluates a preliminary research idea against a five-dimension framework (Higher, Faster, Stronger, Cheaper, Broader) plus idea-lifecycle and student-capability matching, paradigm-shift probing, and a fatal-flaws audit. Returns a reviewer-style verdict; non-STEM ideas route (file: r0/idea-evaluator/SKILL.md)
- image-to-code: Elite website image-to-code skill for Codex. For visually important web tasks, it must first generate the design image(s) itself, deeply analyze them, then implement the website to match them as closely as possible. In Codex, it must prefer large, readable, section-specific (file: r0/image-to-code-skill/SKILL.md)
- imagegen-frontend-mobile: Elite mobile app image-generation skill for creating premium, app-native screen concepts and flows. Designed for iOS, Android, and cross-platform mobile products. Prioritizes clean hierarchy, comfortably readable text, strong multi-screen consistency, controlled color palet (file: r0/imagegen-frontend-mobile/SKILL.md)
- imagegen-frontend-web: Elite frontend image-direction skill for generating premium, conversion-aware website design references. CRITICAL OUTPUT RULE — generate ONE separate horizontal image FOR EVERY section. A landing page with 8 sections produces 8 images. Never compress multiple sections into  (file: r0/imagegen-frontend-web/SKILL.md)
- implement-design-figma-jb: Implement a Figma design as code using the Figma Dev Mode MCP server. Use whenever the task is to build, implement, port, or update UI code from a Figma design, frame, component, or node — including Figma attachments in the chat and pasted figma.com links. Load this skill befo (file: r16/implement-design-figma-jb/SKILL.md)
- industrial-brutalist-ui: Raw mechanical interfaces fusing Swiss typographic print with military terminal aesthetics. Rigid grids, extreme type scale contrast, utilitarian color, analog degradation effects. For data-heavy dashboards, portfolios, or editorial sites that need to feel like declassified b (file: r0/brutalist-skill/SKILL.md)
- interview: 中文简历与目标岗位驱动的面试预测、模拟追问和复练技能：提取需要验证的经历 Claim，按面试轮次建立问题与评分契约，通过一次一问、证据反馈和弱项复练检查真实掌握程度；当用户输入“/interview”、要求面试预测、模拟面试、简历追问、压力面、场景设计题或检查面试掌握程度时使用。 (file: r0/interview/SKILL.md)
- intro-drafter: Drafts the Introduction prose for a technical paper, guided internally by a six-paragraph flowchart: background and running example, existing limitations, problem essence and goal, key challenges, solution overview, contributions. Positions the paper as Technique or New Probl (file: r0/intro-drafter/SKILL.md)
- job-apply: 中文求职申请自动填写技能：使用浏览器读取用户确认的简历资料，逐项填写招聘网站申请表并核对结果；当用户输入“/job-apply”、要求自动填简历或填写求职申请时使用。 (file: r0/job-apply/SKILL.md)
- job-match: 中文岗位匹配分析技能：对照目标 JD 与用户已确认的简历、经历或主张—证据账本，区分已匹配、证据不足和真实缺口，生成可解释的投递建议与后续 skill 交接；当用户输入“/job-match”、要求分析岗位适配度、JD 匹配、简历差距或判断是否值得投递时使用。需要改写简历时交给 /great-resume，需要模拟面试时交给 /interview。 (file: r0/job-match/SKILL.md)
- make-resume: 中文可编辑简历制作技能：默认基于 ASu 单栏高密度技术简历模板，根据用户经历制作或复刻可编辑 HTML/PDF；用户也可以指定仓库内其他模板、本地 HTML 或参考截图。用户输入“/make-resume”“我要阿酥同款简历”或要求制作、修改、复刻简历文件时使用；用户要求 LaTeX、`.tex` 或 Overleaf 版本时，在默认 HTML 交付之外附加导出 `.tex` 源文件。 (file: r0/make-resume/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, typographic contrast, flat bento grids, muted pastels. No gradients, no heavy shadows. (file: r0/minimalist-skill/SKILL.md)
- notion:notion-database-designer: Turns scattered notes and recurring work into useful Notion trackers for requests, content plans, or team work. Use to set up or improve a tracker, choosing its fields and views from the user's needs; ordinary record updates belong to the task's workflow. (file: r7/notion-database-designer/SKILL.md)
- notion:notion-meeting-intelligence: Prepares Notion meeting agendas, pre-reads, decision briefs, and follow-up actions. Use for meeting preparation, carrying context into recurring meetings, or turning meeting outcomes into next steps. Simple meeting lookups or saving notes verbatim do not need this workflow. (file: r7/notion-meeting-intelligence/SKILL.md)
- notion:notion-research-documentation: Synthesizes Notion workspace evidence into cited answers, comparisons, briefs, or reports. Use to investigate a question, connect findings across sources, or reconcile conflicting information, with external research when useful. Simple lookups, fetching a known page, or summar (file: r7/notion-research-documentation/SKILL.md)
- notion:notion-spec-to-implementation: Converts Notion product or technical specs into implementation plans, linked tasks, and evidence-based progress updates. Use for planning or implementing a spec, creating tasks from requirements, or reconciling implementation with spec changes. (file: r7/notion-spec-to-implementation/SKILL.md)
- notion:notion-weekly-project-digest: Produces evidence-based weekly project or team updates by comparing reporting periods, tasks, decisions, and blockers in Notion. Use for recurring status digests; use spec-to-implementation for requirement-level implementation tracking. (file: r7/notion-weekly-project-digest/SKILL.md)
- offer: 中文秋招求职进度管理技能：记录和更新投递、筛选、测评、面试、Offer、拒信及招聘邮件状态，生成可搜索的进度表；当用户输入“/offer”或要求管理秋招进度时使用。 (file: r0/offer/SKILL.md)
- paper-polish: Polishes existing academic prose while preserving the author's meaning: grammar and flow repair, tone calibration against evidence strength, AI-tone removal, and Chinese-to-English rewriting at submission quality. Never fabricates data, citations, or claims, and flags any e (file: r0/paper-polish/SKILL.md)
- paper-writer: Drafts publishable paper prose from the author's own materials, from a single paragraph to a full manuscript, across STEM and non-STEM fields. Every factual claim traces to user input, verified retrieval, or field common knowledge; citations pass an independent verification (file: r0/paper-writer/SKILL.md)
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不阻塞主文件。交付后请确认须摘要清单。已有产出上改稿则另存新时间戳目录。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著录字段检索公布公告，通俗解读专利，基于已读库打开专利地图，对照审查口径出政策简报，辅助审查答复。| China patents skill: mine patent points and draft disclosures, rewrite an existing disclosure into application documents, or chain disclosure-then-application from in (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申请一起做、从零出交底和申请、一条龙、帮写交底再出申请、按清单改、会稿、案卷、/patent-docket。 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包，须另点名才改文件。 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开。 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visual layout matters, including fillable AcroForms. Use Poppler rendering plus Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction. (file: r10/pdf/26.1015.12040/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions and dependencies, and manage plugin connections or removal. Use when the user asks about plugins or when a task would materially benefit from an external app, account, service, or data source that available tools (file: r5/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the task, and a reply a busy human understands in one read. Use on any coding task (writing, fixing, refactoring, reviewing, choosing dependencies) and when the user says "ponytail", "be lazy", "simplest solution", " (file: r12/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks under real load, risky code without tests, slow paths, and what to delete, merge or split. Ranked, each finding explained in plain English. One-shot report, changes nothing. Use for "audit this codebase", "revie (file: r12/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as a debt ledger. One-shot report, changes nothing. Use for "ponytail debt", "what did ponytail defer", "list the shortcuts", /ponytail-debt. (file: r12/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the benchmark. One-shot display. Use for /ponytail-gain, "what does ponytail save", "ponytail impact". (file: r12/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One-shot display. Use for /ponytail-help, "ponytail help", "how do I use ponytail". (file: r12/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, does it hold under real load, is risky code tested, is it fast enough, and is every line needed. Reads the connected code, not only the diff. Each finding is explained in plain English. Use for "review this", "code (file: r12/ponytail-review/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five dimensions: macro logic, writing details, English grammar, LaTeX formatting, and figure quality. Uses a reviewer-style severity taxonomy (CRITICAL / MAJOR / MINOR) and flags banned AI-tone vocabulary and em-dash mi (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use for presentation, slide deck, PowerPoint, PPT, PPTX, or Google Slides requests. (file: r10/presentations/26.1015.12040/skills/presentations/SKILL.md)
- project-guide: 中文项目导学、源码课程与项目面经技能：基于本地项目仓库、项目描述或技术材料，按需生成源码课程与理解题，或生成 导学-{简称}.md、面经-{简称}.md 及交接摘要；当用户输入“/project-guide”、要求项目导学、源码课程、按调用链展开课程、课程练习、项目复盘、项目面经或 STAR 题库时使用。 (file: r0/project-guide/SKILL.md)
- rebuttal-guidance: Provides actionable peer-review rebuttal guidance (not full rebuttal prose) using conditional persuasion P(Z|X,Y): match reviewer mindset X, recommend strategy Y, optionally ground in manuscript evidence and similar successful historical (review, rebuttal) pairs. Use when the (file: r0/rebuttal-guidance/SKILL.md)
- redesign-existing-projects: Upgrades existing websites and apps to premium quality. Audits current design, identifies generic AI patterns, and applies high-end design standards without breaking functionality. Works with any CSS framework or vanilla CSS. (file: r0/redesign-skill/SKILL.md)
- reverse-engineer-anything: Reverse engineer native, managed, Electron/JavaScript, packaged, firmware, and browser targets with REA. Use shipped-artifact or requested runtime evidence to explain features, compare versions, decompile code, or guide a reconstruction. Skip REA for ordinary source-repositor (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized reverse engineering, security analysis, CTF, and defensive testing tasks. Requires the reverse-skill repository to be available as the current workspace or an explicitly supplied local path. (file: r13/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction and in professional prose. Repairs the narrative architecture of fiction and stories (based on StoryScope, arXiv:2604.03136); routes professional text through domain rules for release notes, announcements, PR and issu (file: r14/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Hemingway manner, or asks for strong de-AI on a story; applies Sepia's built-in Hemingway voice profile. (file: r14/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full rewrite. (file: r14/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal in-place prose revision. (file: r14/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose prose without editing. (file: r14/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new prose. (file: r14/sepia-write/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (including a landing page, portfolio, dashboard, portal, tracker, hub, game, event registration, or tool), wants to edit or remix a specific Site built with the Sites plugin, wants to publish a website with Sites, or wants (file: r5/sites/1.0.2-remix-a.1/skills/sites/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, visualize, or work with spreadsheet files (`.xlsx`, `.xls`, `.csv`, `.tsv`) or Google Sheets with formulas, formatting, charts, tables, and recalculation. Do not use for live controlling Microsoft Excel app or a live Ex (file: r11/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the ChatGPT add-in or connected session. Use when the user tags the Microsoft Excel app in Codex or follows up on an established live Excel task. Do not use for standalone spreadsheet files or Google Sheets. (file: r11/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent-friendly DESIGN.md files that enforce premium, anti-generic UI standards — strict typography, calibrated color, asymmetric layouts, perpetual micro-motion, and hardware-accelerated performance. (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation. (file: r8/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, building components, adding functionality, modifying behavior, or planning anything new, in software or out of it (a talk, a business, a renovation). (file: r15/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner wants to know why — repeated work, ignored plans, stumbles, poor results, a skill that didn't fire, "it took too long", "why is it so expensive", "what is it doing" — or wants to build a bug report for the sup (file: r8/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner wants to know why — repeated work, ignored plans, stumbles, poor results, a skill that didn't fire, "it took too long", "why is it so expensive", "what is it doing" — or wants to build a bug report for the superp (file: r15/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies (file: r8/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies (file: r15/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as the implementer yourself — your human partner chose inline execution, or no subagent tool is available (file: r8/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as the implementer yourself — your human partner chose inline execution, or no subagent tool is available (file: r15/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work (file: r8/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work (file: r15/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable - requires technical rigor and verification, not performative agreement or blind implementation (file: r8/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable - requires technical rigor and verification, not performative agreement or blind implementation (file: r15/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before merging to verify work meets requirements (file: r8/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before merging to verify work meets requirements (file: r15/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in the current session (file: r8/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in the current session (file: r15/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes (file: r8/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes (file: r15/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing implementation code (file: r8/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing implementation code (file: r15/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current workspace or before executing implementation plans - ensures an isolated workspace exists via native tools or git worktree fallback (file: r8/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current workspace or before executing implementation plans - ensures an isolated workspace exists via native tools or git worktree fallback (file: r15/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions (file: r8/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions (file: r15/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always (file: r8/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always (file: r15/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, before touching code (file: r8/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, before touching code (file: r15/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifying skills work before deployment (file: r8/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifying skills work before deployment (file: r15/writing-skills/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz yourself on what actually happened, confirm mastery item by item, and don't finish until everything's locked in (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a thinking-template table (research background, limitations, key idea or goal, challenges, methodology modules, contributions), positions the paper as Technique or New Problem/Setting, and runs a four-point self-consi (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template skill. Use when the user invokes $template-creator or asks in natural language to create a reusable template from a reference document, presentation, spreadsheet, Google Docs, Slides, or Sheets link, ImageGen or P (file: r10/template-creator/26.1015.12040/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Coding, Vibe Figure, and Vibe Writing, with behavioural rules that keep the user in charge of academic judgment while delegating mechanical work to AI. Recommends the right tool (Cursor, Claude Code, Codex, Figma, Gem (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conversation. Proactively use to show how something works; explore 'what happens when', 'what changes', or 'help me understand'; compare or inspect; create simulations, maps, charts, graphs, and mockups. Use standard t (file: r4/visualize/1.0.50/skills/visualize/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an animated v2 pet in ChatGPT Work mode from a character idea, brand cue, or reference image. Use for new ChatGPT Pets, custom mascots, non-pixel styles, and unattached sprite sheets requiring nine animation states plus s (file: r9/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in ChatGPT Work mode. Use for an explicit pet in ChatGPT or established ChatGPT Pets context. Exclude real-world and other-app pets; clarify before invoking. (file: r9/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in ChatGPT Work mode, including its name, description, or sprite sheet. Use for a pet in ChatGPT or established ChatGPT Pets context. Exclude real-world and other-app pets; clarify before invoking. (file: r9/update-pet/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is restricted.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse`, `/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
</permissions instructions>
<collaboration_mode># Collaboration Mode: Default

You are now in Default mode. Any previous instructions for other modes (e.g. Plan mode) are no longer active.

Your active mode changes only when new developer instructions with a different `<collaboration_mode>...</collaboration_mode>` change it; user requests or tool descriptions do not change mode by themselves. Known mode names are Default and Plan.

## request_user_input availability

Use the `request_user_input` tool only when it is listed in the available tools for this turn.

In Default mode, strongly prefer making reasonable assumptions and executing the user's request rather than stopping to ask questions.

Use the `request_user_input` tool only for optional questions where the answer would materially improve the quality of the work.

If `request_user_input` returns no answers, continue with best judgment instead of asking again or treating the turn as blocked.

Never use the `request_user_input` tool for permission requests or permission-related escalations.
</collaboration_mode>
<recommended_plugins>
Here is a list of plugins that are available but not installed.

- Dropbox (app-69b31dc2110c8191b8b47dc98fe5a052@openai-curated-remote)
- Box (box@openai-curated-remote)
- Codex Security (codex-security@openai-curated-remote)
- Figma (figma@openai-curated-remote)
- Linear (linear@openai-curated-remote)
- OpenAI Developers (openai-developers@openai-curated-remote)
- Outlook Calendar (outlook-calendar@openai-curated-remote)
- Outlook Email (outlook-email@openai-curated-remote)
- SharePoint (sharepoint@openai-curated-remote)
- Slack (slack@openai-curated-remote)
- Teams (teams@openai-curated-remote)
</recommended_plugins>

## developer · 2026-10-19T12:28:50Z

<multi_agent_role>You are `/root`, the primary agent in a team of agents collaborating to fulfill the user's goals.

At the start of your turn, you are the active agent.
You can spawn sub-agents to handle subtasks, and those sub-agents can spawn their own sub-agents.
All agents in the team, including the agents that you can assign tasks to, are equally intelligent and capable, and have access to the same set of tools.

You can use `spawn_agent` to create a new agent, `followup_task` to give an existing agent a new task and trigger a turn, and `send_message` to pass a message to a running agent without triggering a turn.
`send_message` calls may be read by a human, so ensure they are legible. Always put proper spaces between words and/or numbers.
Child agents can also spawn their own sub-agents.
You can decide how much context you want to propagate to your sub-agents with the `fork_turns` parameter.

You will receive messages in the analysis channel in the form:
```
Message Type: MESSAGE | FINAL_ANSWER
Task name: <recipient>
Sender: <author>
Payload:
<payload text>
```
They may be addressed as to=/root

Note that collaboration tools cannot be called from inside `functions.exec`. Call `spawn_agent`, `send_message`, `followup_task`, `wait_agent`, `interrupt_agent`, and `list_agents` only as direct tool calls using the recipient shown in their tool definitions, such as `to=functions.collaboration.spawn_agent`, since they are intentionally absent from the `functions.exec` `tools.*` namespace. Available tools in `functions.exec` are explicitly described with a `tools` namespace in the developer message.

All agents share the same directory. In detail:
- All agents have access to the same container and filesystem as you.
- All agents use the same current working directory.
- As a result, edits made by one agent are immediately visible to all other agents.

When calling `wait_agent`, prefer longer waits (minutes) to avoid busy polling.

There are 4 available concurrency slots, meaning that up to 4 agents can be active at once, including you.

Full-history forks (`fork_turns` omitted or `"all"`) inherit the parent model and reasoning effort and do not accept overrides. Only set `model` or `reasoning_effort` when explicitly requested by the user, applicable `AGENTS.md` instructions, or skill instructions; when doing so, set `fork_turns` to `"none"` or a positive integer string.</multi_agent_role>

## developer · 2026-10-19T12:28:50Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-10-19T12:28:50Z

# AGENTS.md instructions

<INSTRUCTIONS>
# AGENTS.md

本文件规定项目中的协作、开发、验证与沟通方式。执行时遵守宿主环境的更高优先级指令，并优先采用用户当前明确提出的要求。具体场景的规则优先于一般默认规则；仍有无法消解的冲突时，说明冲突及其影响。

部分规则可以通过 hooks 执行，其余规则需要主动遵守。完成情况应以实际文件、测试结果、Git 状态、运行结果和验证记录为依据。只有已经配置并成功运行的检查，才能作为验证证据。

## 1. 职责与判断

- 在用户确定的目标与授权范围内完成工作。涉及架构、核心业务逻辑或产品方向的重要选择，不得擅自决定；用户已经授权的选择直接执行。
- 默认优先级依次为正确性、可维护性、最小改动范围、执行速度。
- 先检查问题是否存在错误前提、逻辑跳跃或信息缺失，独立判断，区分事实、推测和主观观点。
- 涉及数字、人物和结论时尽量核实来源。不同意用户判断时，直接说明依据、实际风险和替代解释，并提醒与任务有关的遗漏变量、成本和偏差。
- 完整理解并满足当前需求，不擅自增加功能，不删减用户明确要求的设计，不为假设中的未来需求增加配置或抽象。

## 2. 语言与输出


- 默认使用清楚、自然的中文，代码标识符和必要的技术术语保留原名。
- 直接表达具体内容，不使用“不是……而是……”“要……而不是……”等无必要的对比句式，不追加用户没有要求比较的对象。
- 不添加空泛的总起或总结，例如“下面详细拆开”“一句话总结”。
- 使用完整词语和明确的动宾结构。使用“崩溃、终止、判定、推断、抛出、挂起”等完整表达，不使用单个字的缩写，不生造名词或缩略说法。
- 不使用“落地”“钉死”“对齐”等含义模糊的行业黑话。描述采用的技术、模型和工具时，直接写出具体事物，避免以“栈”字概括。
- 不评价工作量，不使用“That's a lot”“This is a substantial rewrite”等表达。
- 搜索结果只列出符合要求的内容，不罗列已经确认不符合要求的候选项。
- 回复、注释和交付文档描述当前有效的最终状态，不保留已删除方案、错误代码或无关纠正过程的说明。
- 用户指出错误后，直接基于纠正后的事实继续工作，不重复解释用户已经明确指出的错误。
- 更新应当具体，说明实际改动、验证结果和仍然存在的阻碍。
- 不使用 ASCII Art 绘制示意图或表格。需要图示时使用 Mermaid，表格使用标准 Markdown。

## 3. 用户意图与执行控制

- 用户要求先规划、思考、审查、评估或解释时，先完成对应工作，取得执行授权后再修改文件。
- 未经明确要求，不切换到专门的 plan mode。复杂任务所需的书面计划可以在当前模式中完成。
- 用户提供书面计划时，按计划执行；计划通常位于 `claude.md`，以用户指定的位置和实际文件为准。遇到实质性阻碍时，说明阻碍，暂停依赖该决定的步骤。
- 用户批准计划或明确说“执行”“可以”“推送”后，直接完成已获授权的操作，不重复征求同一项授权。
- 用户以疑问句提出问题时，回答问题，不擅自修改文件，不附加未要求的替代方案、反问或催促执行的话语。
- 对确实影响实现且尚未授权的需求歧义，明确指出需要用户决定的事项；已经可以独立完成的工作继续执行。
- 执行过程中收到其他问题，能够立即回答的先回答，然后继续原任务；用户明确取消或改变目标时，按新要求执行。
- 用户表示“退一步”“一直在绕圈”等意思时，停止当前方法，重新读取相关上下文并提出不同路径。
- 用户询问是否确定时，先通过工具核实，再回答。
- 风险较高且没有明确恢复点的操作，先提出建立检查点。

## 4. 持久记录与上下文

聊天记录不能替代持久记录。会话开始时读取与当前任务有关且已经存在的文件，并在工作过程中保持准确：

- `memory/agents.md`：当前代理、MCP、采用的技术和工具。
- `memory/plan.md`：总体设计与纵向功能切片。
- `memory/progress.md`：可以独立完成和验证的任务清单及当前状态。
- `memory/verify.md`：完成标准与必要检查。
- `memory/gotchas.md`：用户已纠正问题所对应的可复用注意事项。

开始实质性开发前，初始化缺失的上述记录。记录应当简洁、准确，与项目实际情况一致。

- 长对话后，修改前重新读取相关文件。
- 上下文不足、压缩对话或交接工作前，把当前状态和剩余工作写入 `memory/progress.md`。
- 大文件按相关范围分段读取；工具输出被截断时，读取完整保存结果或缩小查询范围后重试。
- 按需加载文件和历史，把持久结论写入 `memory/`，避免反复加载整份静态提示词或大量原始输出。
- 用户纠正问题后，在 `memory/gotchas.md` 中记录适用的预防规则，不复制错误实现或无关对话。开发日志记录实际结果和验证情况。

## 5. 规划与任务范围

涉及多个文件、行为变化、架构选择或其他非简单修改时，先形成书面计划：

1. 读取相关代码，理解实际执行流程、调用位置和现有模式。
2. 识别需求歧义、约束和需要作出的选择。
3. 更新 `memory/plan.md` 与 `memory/verify.md`。
4. 在 `memory/progress.md` 中列出可以独立验证的步骤。
5. 按顺序实施、运行、测试并修正，直到整个需求完成。

- 对明显的一两行修复，直接执行并验证。
- 设计应当完整覆盖已知需求、边界条件和失败情况，不以“先做一个不完整版本再观察”为由遗漏必要功能。
- 默认提供一个能够满足需求的方案。确实需要多个方案时，应当分别说明成立条件，不机械地排列“稳妥”和“激进”选项。
- 完整设计可以分成小范围的执行步骤；每次完成一个可以独立验证的纵向功能切片，最终交付全部已约定功能。
- 避免把广泛重构混入功能开发。每个执行阶段原则上控制在约五个文件内，纯机械修改除外。
- 较大的独立工作区域分别实施和验证。

## 6. 代码与依赖

- 先遵循项目现有的命名、结构和风格，再考虑引入新模式。导出的函数和类使用清楚、可区分的名称。
- 优先复用已有代码、标准库、平台能力和已经安装的依赖。需要成熟依赖时正常使用，不为减少依赖自行重写已有能力或采用复杂绕行方案。
- 成熟文件格式使用标准库或成熟的第三方库解析，不自行编写字符串或字节解析器。
- 默认使用静态导入，只有确实需要运行时加载时才采用动态导入。必要的 Python 库直接 `import`，不使用 `try-except` 包装导入。
- 不为假设中的未来需求增加灵活性、配置、接口或抽象。在满足完整需求与正确性的前提下，选择改动范围最小、清楚直接的实现。
- 无效状态应当在出错位置明确失败，不静默捕获错误或采用隐藏的 fallback。必要的输入校验、资源清理和防止数据丢失的错误处理必须保留。
- 发现重复状态、模式不一致、边界薄弱或只处理表面症状的修复时，指出根本问题。授权范围内的修复直接执行，额外的结构调整先说明范围并取得授权；范围外事项记入 `memory/progress.md`。
- 默认不添加注释。只有原因无法从代码直接看出时才添加简短注释，注释使用中文，技术术语保留英文。
- Python 文件开头不添加模块级 docstring 或 shebang，除非用户明确要求。

## 7. 文件修改与安全

- 每次修改前重新读取文件，修改后再次检查实际内容。
- 用户可能在两次操作之间撤销或调整改动，始终以文件当前状态为基础，不恢复用户已经删除的内容。
- 使用文件编辑工具修改代码，不使用 heredoc、Python 脚本、`sed`、`perl` 等方式批量生成替换操作来修改代码。
- 不在 Bash 命令中内嵌超长或大量多行脚本。需要脚本时，先通过文件编辑工具写入文件，再执行。
- 未经明确要求，不读写 `/tmp` 及其实际对应的临时目录。中间结果放入当前项目中专用的目录，并将该目录加入 `.gitignore`。
- 重命名或修改签名时，分别搜索直接调用、类型引用、字符串引用、动态导入、`require()`、重新导出、汇总导出文件和已有测试中的替代实现。
- 删除文件前，先验证引用关系。
- 对大文件进行结构调整时，只清理直接阻碍当前修改或由当前修改产生的无用代码，不附带无关清理。
- 不使用 Git 命令撤销代码。用户要求恢复旧状态时，使用文件编辑工具恢复对应内容，并保留用户的其他改动。
- 修正文档或代码时，删除失效内容，使交付文件保持准确；开发记录仍然如实记载需求、实际改动和验证结果。

## 8. 测试与验证

功能实现包括实施、运行、测试和必要的修正。不得只完成初步实现就要求用户代为验证。

对于缺陷修复和新增行为：

1. 添加或找到能够暴露问题的测试。
2. 运行测试，确认它因目标问题失败。
3. 实现能够满足完整需求的最小修改。
4. 运行相关检查，确认通过后再进行必要重构。

- 验证必须覆盖真实行为，不使用 mock、伪造数据、虚假的成功结果或只为通过测试的绕行措施掩盖问题。
- 缺少运行条件时，如实说明未完成的验证和具体原因，不声称已经通过。
- 项目没有检查机制时，说明一次，并建议与实际风险相称的基本验证。
- `tdd-check.sh` 在配置后可以提示新导出内容缺少附近测试；该提示不能证明遵循了先写测试的顺序。
- 按改动类型运行适用的类型检查、静态检查和测试。`stop-verify.sh`、`.codex/hooks/stop.sh` 和 `.githooks/pre-commit` 只有配置生效后才能执行约束。
- 条件允许时，运行改动涉及的脚本、接口、命令行工具或完整流程，检查日志中的异常。
- 使用测试套件、独立审查者或用户提供的证据验证行为与视觉正确性，不能仅凭自己的判断宣称正确。使用其他代理时，遵守当前环境的授权规则。
- 用户要求测试产出时，按照新用户实际使用的路径验证，不能只检查代码。
- 同一个修复连续失败两次时，停止重复尝试，重新从入口读取相关代码；再次尝试前，确定并向用户说明哪个假设错误，不重复已经解释清楚的错误。

### 视觉验证

- 未经用户明确要求，不主动调用视觉功能、截图或图像检查。
- UI 修改仍需完成适用的构建、运行和行为测试；没有视觉证据时，如实说明验证范围。
- 用户明确要求视觉验证后，执行构建或渲染、截图和检查，并在 `.agent/visual/` 下保存记录。
- 视觉记录必须使用 Markdown，引用新生成且非空的图片，并包含改动文件、页面路径或 URL、视口尺寸、图片文件名和观察结果。
- 有对应工具时，可使用下列命令获取截图；使用前确认脚本存在且适用：

```bash
./.agent-md/bin/playwright-capture.sh <url> .agent/visual/<name>.png
```

## 9. 工具、网页与运行环境

- 依据原始报错和命令输出排查问题；错误报告缺少这些输出时，向用户索取。
- 用户提供任务所依赖的网页链接时，先读取其完整内容，再开展依赖该内容的工作。发现库的使用方式有误时，重新查看对应文档；无法完整访问时，明确说明缺失范围。
- 优先依据退出码、JSON 字段、工具结果和终止原因等结构化信号作出决定；存在结构化信号时，不通过猜测自然语言推断状态。
- 使用结构化输出前，验证必需字段、类型、允许值和路径。工具参数无效时明确失败，不猜测参数。
- 可控制工具输出时，使用包含 `status`、`type`、`message` 和 `suggestion` 的结构化错误信息。
- 独立且安全的工具调用可以并行执行，完成后核对全部结果。有依赖关系的步骤按顺序执行。
- 宿主允许且未固定模型配置时，例行任务采用能够胜任的经济配置；架构决策、高风险操作或失败分析采用足够的推理能力，不覆盖用户明确选择的配置。
- 实现调用 API 的代理时，明确设置输出预算，不默认使用无界输出。
- 对高风险结论或修改增加独立检查或反例验证，再将结果作为可靠依据。

## 10. 项目辅助工具与 hooks

按需发现项目辅助脚本，不一次加载全部流程。以下命令仅在相应文件存在时使用：

```bash
./.agent-md/bin/discover_helpers.sh
./.agent-md/bin/discover_helpers.sh visual
./.agent-md/bin/doctor.sh
```

这些文件是普通 shell 辅助脚本；项目原生 Codex skills 位于 `.agents/skills/<name>/SKILL.md`。

对于没有原生 hooks 的代理，可以使用项目已有的 `.githooks/pre-commit`。确认文件存在并决定启用后，配置方式如下：

```bash
git config core.hooksPath .githooks
```

支持 `codex_hooks` 配置项的 Codex 版本，可在 `~/.codex/config.toml` 中使用以下设置启用对应能力；修改前检查当前版本和已有配置：

```toml
[features]
codex_hooks = true
```

部分 hooks 会根据 `tsconfig.json`、`eslint.config.*`、`pyproject.toml` 或 `Cargo.toml` 推断检查命令。需要确定性配置时，在 `agent-md.toml` 中声明项目实际使用的命令。以下内容是示例，应按项目修改：

```toml
[verify]
typecheck = "npx --no-install tsc --noEmit"
lint = "npx --no-install eslint ."
test = "pnpm test"
lint_file = "npx --no-install eslint {file}"

[visual]
required = false
artifacts_dir = ".agent/visual"
freshness_seconds = 3600
```

只有获得视觉验证授权后，才把 `visual.required` 设置为 `true`。已有强制检查与当前授权冲突时，说明阻碍，不擅自跳过检查。

## 11. Git 工作流程

- 完成一个独立的逻辑单元，且适用的测试、类型检查等验证通过后，主动创建原子化提交。
- 提交说明严格遵循 Conventional Commits，例如 `feat:`、`fix:`、`refactor:`、`test:`、`docs:`。
- 只暂存本次改动涉及的文件，禁止执行 `git add .`。文件包含用户已有修改时，检查并仅暂存本次修改对应的部分。
- 提交前检查内容，不提交 `.env`、API Keys、密钥、临时调试文件或 `.log` 文件。
- 用户已授权每次自动推送：提交完成后，向当前分支已经配置的远端执行普通 `git push`，无需再次征求用户同意。不强制推送，不擅自更换远端或目标分支。
- 当前目录没有 Git 仓库、没有明确的推送目标，或缺少必要权限时，如实说明阻碍；不擅自初始化仓库、创建远端或宣称推送成功。
- Git 操作仍然遵守文件修改与恢复限制。

## 12. 开发记录

每次完成用户交付的任务时，在 `docs/CHANGELOG.md` 追加开发记录；文件不存在则创建，并与对应代码或文档修改一起提交。

- 时间使用当前环境的本地时间，内容反映实际需求、实现结果和验证情况。
- 记录涉及文件，可以附上实际新增和删除行数。
- 提交完成前标记“待提交”，完成后使用实际提交哈希与提交说明补记。补记通过后续文档提交保存，不编造哈希，也不要求提交包含自身最终哈希。
- 无法提交时，填写具体原因；没有执行的测试不得填写为通过。
- 用户可见的交付文档保持最终状态，日志仅保留追踪任务所需的事实。

记录格式：

```markdown
## [YYYY-MM-DD HH:mm] 任务标题

- **需求/问题描述**：
  > 简要复述用户的原始需求或报告的问题

- **实际实现的功能与改动**：
  - [功能点/修复项]：实际完成的功能或修复
  - [测试/验证]：实际执行的测试、构建或其他验证结果

- **涉及文件**：
  - `path/to/file` (+新增行 / -删除行)

- **Git 提交**：`实际提交哈希 提交说明`，或尚未提交的具体原因

---
```

##
</INSTRUCTIONS>
<environment_context>
  <cwd>/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse</cwd>
  <shell>zsh</shell>
  <current_date>2026-10-19</current_date>
  <timezone>Asia/Shanghai</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse</root><root>/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse</path></entry><entry access="write"><path>/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/WebStorm2026.2/aia/agents/views/codex/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-10-19T12:28:50Z

PONYTAIL MODE ACTIVE — level: full

# Ponytail

You are a lazy senior developer. The best code is the code never written. You solve the whole problem with the least new code. End your reply with one or two lines: what you skipped or did not check, and any risk the user must know.

Active for the whole session until the user says "stop ponytail" or "normal mode". Switch level: `/ponytail lite|full|ultra`.

## Before you write

Read the task and the code it touches. List every place your change must reach: callers, tests, fixtures, config, exports. Check what your change could break for users: data it would destroy or expose, callers that stop working. That is scope. Extra features are not.

## The smallest complete change

Take the first option that fully works:

1. Does it need to exist? Skip features, options and flexibility nobody asked for, and name them in one line. A vague request ("build me X") gets the smallest version that does the core job.
2. Already in this codebase (a helper, component, service, pattern)? Use it the way the surrounding code does.
3. Standard library or a platform feature? Use it, unless the project has its own. A house component beats a native widget.
4. An installed dependency? Use it. Never add a dependency for a few lines.
5. Can it be one line a reader gets at a glance? One line.
6. Otherwise: the minimum code that works.

- Be lazy about the solution, never about the change itself: finish every part the task needs, including the callers, tests and fixtures your change breaks.
- No abstraction, wrapper, type conversion, option, config, boilerplate or "for later" code nobody asked for. Keep values in the form the platform already gives you. Deletion beats addition. Keep the structure the codebase already has: its layers, interfaces and conventions.
- The shortest working diff wins, once you know everything it must touch. A one-liner that needs decoding is not short.
- Comment only the why the code cannot show, in one line.
- Bug fix: before you edit, grep every caller of the function you touch, then fix the root cause once in the shared code.
- Code you move or merge keeps its error handling and validation.
- Between options of equal size, take the one that is correct on edge cases.
- Lazy code without its check is unfinished: new non-trivial logic (a branch, a loop, a parser, money or security, or a whole new script or app) leaves one small test or an assert-based self-check. Trivial changes need none.
- A shortcut with a known limit gets a code comment in this form: `shortcut: <the limit>, <when to upgrade>`.

Never cut: validation at trust boundaries, error handling that prevents data loss, security, accessibility, the calibration real hardware needs, anything the user asked for.

## Levels

| Level | Behavior |
|-------|----------|
| **full** | The rules above. Default. |


## user · 2026-10-19T12:28:50Z

修复
[@liDemo copy.html](file:///Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/character0/261019/liDemo%20copy.html)

## assistant · 2026-10-19T12:28:54Z

我会先读取页面和项目记录，查明具体问题，再做最小修复并验证。会使用 ponytail 和 systematic-debugging 技能。

## tool · 2026-10-19T12:29:01Z


Script completed
Wall time 0.4 seconds
Output:

/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse
character0/261019/liDemo copy.html

{"i":0,"status":"fulfilled","value":{"chunk_id":"6035bb","wall_time_seconds":0.000008333,"exit_code":0,"original_token_count":3165,"output":"---\nname: using-superpowers\ndescription: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions\n---\n\n<SUBAGENT-STOP>\nIf you were dispatched as a subagent to execute a specific task, ignore this skill.\n</SUBAGENT-STOP>\n\n<EXTREMELY-IMPORTANT>\nIf you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.\n\nIF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.\n\nThis is not negotiable. You cannot rationalize your way out of this.\n</EXTREMELY-IMPORTANT>\n\n## The Rule\n\n**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.\n\n**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.\n\nThen announce \"Using [skill] to [purpose]\" and follow the skill exactly. If it has a checklist, create a todo per item.\n\n## Skill Priority\n\nWhen multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.\n\n- \"Let's build X\" → superpowers:brainstorming first, then implementation skills.\n- \"Fix this bug\" → superpowers:systematic-debugging first, then domain skills.\n\n## Red Flags\n\nThese thoughts mean STOP—you're rationalizing:\n\n| Thought | Reality |\n|---------|---------|\n| \"This is just a simple question\" | Questions are tasks. Check for skills. |\n| \"I need more context first\" | Skill check comes BEFORE clarifying questions. |\n| \"Let me explore the codebase first\" | Skills tell you HOW to explore. Check first. |\n| \"I can check git/files quickly\" | Files lack conversation context. Check for skills. |\n| \"Let me gather information first\" | Skills tell you HOW to gather information. |\n| \"This doesn't need a formal skill\" | If a skill exists, use it. |\n| \"I remember this skill\" | Skills evolve. Read current version. |\n| \"This doesn't count as a task\" | Action = task. Check for skills. |\n| \"The skill is overkill\" | Simple things become complex. Use it. |\n| \"I'll just do this one thing first\" | Check BEFORE doing anything. |\n| \"This feels productive\" | Undisciplined action wastes time. Skills prevent this. |\n| \"I know what that means\" | Knowing the concept ≠ using the skill. Invoke it. |\n\n## Platform Adaptation\n\nIf your harness appears here, read its reference file for special instructions:\n\n- Claude Code: `references/claude-code-tools.md`\n- Codex: `references/codex-tools.md`\n- Pi: `references/pi-tools.md`\n- Antigravity: `references/antigravity-tools.md`\n- Hermes Agent: `references/hermes-tools.md`\n- Muse: `references/muse-tools.md`\n\n## User Instructions\n\nUser instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.\n---\nname: systematic-debugging\ndescription: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes\n---\n\n# Systematic Debugging\n\n## Overview\n\n**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.\n\n**Violating the letter of this process is violating the spirit of debugging.**\n\n## The Iron Law\n\n```\nNO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST\n```\n\nIf you haven't completed Phase 1, you cannot propose fixes.\n\n## When to Use\n\nUse for ANY technical issue:\n- Test failures\n- Bugs in production\n- Unexpected behavior\n- Performance problems\n- Build failures\n- Integration issues\n\n**Use this ESPECIALLY when:**\n- Under time pressure (emergencies make guessing tempting)\n- \"Just one quick fix\" seems obvious\n- You've already tried multiple fixes\n- Previous fix didn't work\n- You don't fully understand the issue\n\n**Don't skip when:**\n- Issue seems simple (simple bugs have root causes too)\n- You're in a hurry (rushing guarantees rework)\n- Manager wants it fixed NOW (systematic is faster than thrashing)\n\n## The Four Phases\n\nYou MUST complete each phase before proceeding to the next.\n\n### Phase 1: Root Cause Investigation\n\n**BEFORE attempting ANY fix:**\n\n1. **Read Error Messages Carefully**\n   - Don't skip past errors or warnings\n   - They often contain the exact solution\n   - Read stack traces completely\n   - Note line numbers, file paths, error codes\n\n2. **Reproduce Consistently**\n   - Can you trigger it reliably?\n   - What are the exact steps?\n   - Does it happen every time?\n   - If not reproducible → gather more data, don't guess\n\n3. **Check Recent Changes**\n   - What changed that could cause this?\n   - Git diff, recent commits\n   - New dependencies, config changes\n   - Environmental differences\n\n4. **Gather Evidence in Multi-Component Systems**\n\n   **WHEN system has multiple components (CI → build → signing, API → service → database):**\n\n   **BEFORE proposing fixes, add diagnostic instrumentation:**\n   ```\n   For EACH component boundary:\n     - Log what data enters component\n     - Log what data exits component\n     - Verify environment/config propagation\n     - Check state at each layer\n\n   Run once to gather evidence showing WHERE it breaks\n   THEN analyze evidence to identify failing component\n   THEN investigate that specific component\n   ```\n\n   **Example (multi-layer system):**\n   ```bash\n   # Layer 1: Workflow\n   echo \"=== Secrets available in workflow: ===\"\n   echo \"IDENTITY: ${IDENTITY:+SET}${IDENTITY:-UNSET}\"\n\n   # Layer 2: Build script\n   echo \"=== Env vars in build script: ===\"\n   env | grep IDENTITY || echo \"IDENTITY not in environment\"\n\n   # Layer 3: Signing script\n   echo \"=== Keychain state: ===\"\n   security list-keychains\n   security find-identity -v\n\n   # Layer 4: Actual signing\n   codesign --sign \"$IDENTITY\" --verbose=4 \"$APP\"\n   ```\n\n   **This reveals:** Which layer fails (secrets → workflow ✓, workflow → build ✗)\n\n5. **Trace Data Flow**\n\n   **WHEN error is deep in call stack:**\n\n   See `root-cause-tracing.md` in this directory for the complete backward tracing technique.\n\n   **Quick version:**\n   - Where does bad value originate?\n   - What called this with bad value?\n   - Keep tracing up until you find the source\n   - Fix at source, not at symptom\n\n### Phase 2: Pattern Analysis\n\n**Find the pattern before fixing:**\n\n1. **Find Working Examples**\n   - Locate similar working code in same codebase\n   - What works that's similar to what's broken?\n\n2. **Compare Against References**\n   - If implementing pattern, read reference implementation COMPLETELY\n   - Don't skim - read every line\n   - Understand the pattern fully before applying\n\n3. **Identify Differences**\n   - What's different between working and broken?\n   - List every difference, however small\n   - Don't assume \"that can't matter\"\n\n4. **Understand Dependencies**\n   - What other components does this need?\n   - What settings, config, environment?\n   - What assumptions does it make?\n\n### Phase 3: Hypothesis and Testing\n\n**Scientific method:**\n\n1. **Form Single Hypothesis**\n   - State clearly: \"I think X is the root cause because Y\"\n   - Write it down\n   - Be specific, not vague\n\n2. **Test Minimally**\n   - Make the SMALLEST possible change to test hypothesis\n   - One variable at a time\n   - Don't fix multiple things at once\n\n3. **Verify Before Continuing**\n   - Did it work? Yes → Phase 4\n   - Didn't work? Form NEW hypothesis\n   - DON'T add more fixes on top\n\n4. **When You Don't Know**\n   - Say \"I don't understand X\"\n   - Don't pretend to know\n   - Ask for help\n   - Research more\n\n### Phase 4: Implementation\n\n**Fix the root cause, not the symptom:**\n\n1. **Create Failing Test Case**\n   - Simplest possible reproduction\n   - Automated test if possible\n   - One-off test script if no framework\n   - MUST have before fixing\n   - Use the `superpowers:test-driven-development` skill for writing proper failing tests\n\n2. **Implement Single Fix**\n   - Address the root cause identified\n   - ONE change at a time\n   - No \"while I'm here\" improvements\n   - No bundled refactoring\n\n3. **Verify Fix**\n   - Test passes now?\n   - No other tests broken?\n   - Issue actually resolved?\n   - Use the `superpowers:verification-before-completion` skill before claiming success\n\n4. **If Fix Doesn't Work**\n   - STOP\n   - Count: How many fixes have you tried?\n   - If < 3: Return to Phase 1, re-analyze with new information\n   - **If ≥ 3: STOP and question the architecture (step 5 below)**\n   - DON'T attempt Fix #4 without architectural discussion\n\n5. **If 3+ Fixes Failed: Question Architecture**\n\n   **Pattern indicating architectural problem:**\n   - Each fix reveals new shared state/coupling/problem in different place\n   - Fixes require \"massive refactoring\" to implement\n   - Each fix creates new symptoms elsewhere\n\n   **STOP and question fundamentals:**\n   - Is this pattern fundamentally sound?\n   - Are we \"sticking with it through sheer inertia\"?\n   - Should we refactor architecture vs. continue fixing symptoms?\n\n   **Discuss with your human partner before attempting more fixes**\n\n   This is NOT a failed hypothesis - this is a wrong architecture.\n\n## Red Flags - STOP and Follow Process\n\nIf you catch yourself thinking:\n- \"Quick fix for now, investigate later\"\n- \"Just try changing X and see if it works\"\n- \"Add multiple changes, run tests\"\n- \"Skip the test, I'll manually verify\"\n- \"It's probably X, let me fix that\"\n- \"I don't fully understand but this might work\"\n- \"Pattern says X but I'll adapt it differently\"\n- \"Here are the main problems: [lists fixes without investigation]\"\n- Proposing solutions before tracing data flow\n- **\"One more fix attempt\" (when already tried 2+)**\n- **Each fix reveals new problem in different place**\n\n**ALL of these mean: STOP. Return to Phase 1.**\n\n**If 3+ fixes failed:** Question the architecture (see Phase 4.5)\n\n## your human partner's Signals You're Doing It Wrong\n\n**Watch for these redirections:**\n- \"Is that not happening?\" - You assumed without verifying\n- \"Will it show us...?\" - You should have added evidence gathering\n- \"Stop guessing\" - You're proposing fixes without understanding\n- \"Ultra-think this\" - Question fundamentals, not just symptoms\n- \"We're stuck?\" (frustrated) - Your approach isn't working\n\n**When you see these:** STOP. Return to Phase 1.\n\n## Common Rationalizations\n\n| Excuse | Reality |\n|--------|---------|\n| \"Issue is simple, don't need process\" | Simple issues have root causes too. Process is fast for simple bugs. |\n| \"Emergency, no time for process\" | Systematic debugging is FASTER than guess-and-check thrashing. |\n| \"Just try this first, then investigate\" | First fix sets the pattern. Do it right from the start. |\n| \"I'll write test after confirming fix works\" | Untested fixes don't stick. Test first proves it. |\n| \"Multiple fixes at once saves time\" | Can't isolate what worked. Causes new bugs. |\n| \"Reference too long, I'll adapt the pattern\" | Partial understanding guarantees bugs. Read it completely. |\n| \"I see the problem, let me fix it\" | Seeing symptoms ≠ understanding root cause. |\n| \"One more fix attempt\" (after 2+ failures) | 3+ failures = architectural problem. Question pattern, don't fix again. |\n\n## Quick Reference\n\n| Phase | Key Activities | Success Criteria |\n|-------|---------------|------------------|\n| **1. Root Cause** | Read errors, reproduce, check changes, gather evidence | Understand WHAT and WHY |\n| **2. Pattern** | Find working examples, compare | Identify differences |\n| **3. Hypothesis** | Form theory, test minimally | Confirmed or new hypothesis |\n| **4. Implementation** | Create test, fix, verify | Bug resolved, tests pass |\n\n## When Process Reveals \"No Root Cause\"\n\nIf systematic investigation reveals issue is truly environmental, timing-dependent, or external:\n\n1. You've completed the process\n2. Document what you investigated\n3. Implement appropriate handling (retry, timeout, error message)\n4. Add monitoring/logging for future investigation\n\n**But:** 95% of \"no root cause\" cases are incomplete investigation.\n\n## Supporting Techniques\n\nThese techniques are part of systematic debugging and available in this directory:\n\n- **`root-cause-tracing.md`** - Trace bugs backward through call stack to find original trigger\n- **`defense-in-depth.md`** - Add validation at multiple layers after finding root cause\n- **`condition-based-waiting.md`** - Replace arbitrary timeouts with condition polling\n"}}
{"i":1,"status":"fulfilled","value":{"chunk_id":"9058f7","wall_time_seconds":0.000006208,"exit_code":0,"original_token_count":1372,"output":"---\nname: ponytail\ndescription: >\n  Lazy senior dev mode: the smallest change that fully solves the task, and a\n  reply a busy human understands in one read. Use on any coding task (writing,\n  fixing, refactoring, reviewing, choosing dependencies) and when the user says\n  \"ponytail\", \"be lazy\", \"simplest solution\", \"yagni\", or complains about\n  over-engineering or bloat. Levels: lite, full (default), ultra.\nargument-hint: \"[lite|full|ultra|off]\"\nlicense: MIT\n---\n\n# Ponytail\n\nYou are a lazy senior developer. The best code is the code never written. You solve the whole problem with the least new code. End your reply with one or two lines: what you skipped or did not check, and any risk the user must know.\n\nActive for the whole session until the user says \"stop ponytail\" or \"normal mode\". Switch level: `/ponytail lite|full|ultra`.\n\n## Before you write\n\nRead the task and the code it touches. List every place your change must reach: callers, tests, fixtures, config, exports. Check what your change could break for users: data it would destroy or expose, callers that stop working. That is scope. Extra features are not.\n\n## The smallest complete change\n\nTake the first option that fully works:\n\n1. Does it need to exist? Skip features, options and flexibility nobody asked for, and name them in one line. A vague request (\"build me X\") gets the smallest version that does the core job.\n2. Already in this codebase (a helper, component, service, pattern)? Use it the way the surrounding code does.\n3. Standard library or a platform feature? Use it, unless the project has its own. A house component beats a native widget.\n4. An installed dependency? Use it. Never add a dependency for a few lines.\n5. Can it be one line a reader gets at a glance? One line.\n6. Otherwise: the minimum code that works.\n\n- Be lazy about the solution, never about the change itself: finish every part the task needs, including the callers, tests and fixtures your change breaks.\n- No abstraction, wrapper, type conversion, option, config, boilerplate or \"for later\" code nobody asked for. Keep values in the form the platform already gives you. Deletion beats addition. Keep the structure the codebase already has: its layers, interfaces and conventions.\n- The shortest working diff wins, once you know everything it must touch. A one-liner that needs decoding is not short.\n- Comment only the why the code cannot show, in one line.\n- Bug fix: before you edit, grep every caller of the function you touch, then fix the root cause once in the shared code.\n- Code you move or merge keeps its error handling and validation.\n- Between options of equal size, take the one that is correct on edge cases.\n- Lazy code without its check is unfinished: new non-trivial logic (a branch, a loop, a parser, money or security, or a whole new script or app) leaves one small test or an assert-based self-check. Trivial changes need none.\n- A shortcut with a known limit gets a code comment in this form: `shortcut: <the limit>, <when to upgrade>`.\n\nNever cut: validation at trust boundaries, error handling that prevents data loss, security, accessibility, the calibration real hardware needs, anything the user asked for.\n\n## Levels\n\n| Level | Behavior |\n|-------|----------|\n| **lite** | Build what was asked. Name the smaller option in one line and let the user pick. |\n| **full** | The rules above. Default. |\n| **ultra** | Also question the request: before building, push back on any part the need does not justify. |\n?? .DS_Store\n?? character0/.DS_Store\n?? character1/\nmain\norigin\thttps://github.com/OyamaMeek/WebDesignCourse.git (fetch)\norigin\thttps://github.com/OyamaMeek/WebDesignCourse.git (push)\n<!DOCTYPE html>\n<html lang=\"zh-CN\">\n<head>\n  <meta charset=\"UTF-8\">\n  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">\n  <title>开封菊展品种简介</title>\n  <style>\n    .slide ul { list-style: none; }\n    .slide ul li {\n      font-size: 1.22rem;\n      line-height: 1.75;\n      padding-left: 26px;\n      position: relative;\n      margin-bottom: 4px;\n    }\n    .slide ul li::before {\n      content: \"▸\";\n      position: absolute;\n      left: 0;\n      color: #6366f1;\n      font-weight: bold;\n    }\n     /* 综合案例专用样式 */\n    .chrysanthemum-demo {\n      background: #fffaf0;\n      border: 1px solid #f6e3b4;\n      border-radius: 12px;\n      padding: 20px 25px;\n      box-shadow: 0 4px 14px rgba(15, 23, 42, 0.08);\n    }\n    .chrysanthemum-demo h3 {\n      color: #b45309;\n      font-size: 1.5rem;\n      text-align: center;\n      margin-bottom: 12px;\n      letter-spacing: 2px;\n    }\n    .chrysanthemum-demo .sub-title {\n      font-size: 1.15rem;\n      color: #92400e;\n      font-weight: bold;\n      margin: 10px 0 6px;\n      border-bottom: 1px dashed #fcd34d;\n      padding-bottom: 4px;\n    }\n    .chrysanthemum-demo ul, .chrysanthemum-demo ol, .chrysanthemum-demo dl {\n      padding-left: 22px;\n      font-size: 1.05rem;\n      line-height: 1.8;\n    }\n    .chrysanthemum-demo ul { list-style-type: disc; color: #78350f; }\n    .chrysanthemum-demo ol { list-style-type: decimal; color: #78350f; }\n    .chrysanthemum-demo dt {\n      font-weight: bold;\n      color: #b45309;\n      margin-top: 8px;\n    }\n    .chrysanthemum-demo dd {\n      margin-left: 20px;\n      color: #57534e;\n      font-size: 1rem;\n    }\n  </style>\n</head>\n<body>\n<div>\n  <!-- ========== 新增：综合案例 · 开封菊展 ========== -->\n  <div class=\"slide\">\n    \n  </div>\n\n</div>\n\n\n</body>\n</html>"}}

## tool · 2026-10-19T12:29:09Z


Script completed
Wall time 0.1 seconds
Output:

{"i":0,"status":"fulfilled","value":{"chunk_id":"0334d5","wall_time_seconds":0.000005334,"exit_code":0,"original_token_count":768,"output":".idea/php.xml\n.idea/modules.xml\n.idea/.gitignore\n.idea/vcs.xml\n.idea/WebDesignCourse.iml\ncharacter0/261019/liDemo copy.html\ncharacter0/261019/列表.html\ncharacter0/261012/网页基础.html\ncharacter2/section1/subsection1/1/index.html\ncharacter2/section1/subsection1/index.html\ncharacter3/section2/index.html\ncharacter3/section5/index.html\ncharacter3/section4/subsection3/index.html\ncharacter3/section3/index.html\ncharacter3/section3/subsection4/index.html\nindex.html\n./character0/261019/liDemo copy.html:6:  <title>开封菊展品种简介</title>\n./character0/261019/liDemo copy.html:24:    .chrysanthemum-demo {\n./character0/261019/liDemo copy.html:31:    .chrysanthemum-demo h3 {\n./character0/261019/liDemo copy.html:38:    .chrysanthemum-demo .sub-title {\n./character0/261019/liDemo copy.html:46:    .chrysanthemum-demo ul, .chrysanthemum-demo ol, .chrysanthemum-demo dl {\n./character0/261019/liDemo copy.html:51:    .chrysanthemum-demo ul { list-style-type: disc; color: #78350f; }\n./character0/261019/liDemo copy.html:52:    .chrysanthemum-demo ol { list-style-type: decimal; color: #78350f; }\n./character0/261019/liDemo copy.html:53:    .chrysanthemum-demo dt {\n./character0/261019/liDemo copy.html:58:    .chrysanthemum-demo dd {\n./character0/261019/liDemo copy.html:67:  <!-- ========== 新增：综合案例 · 开封菊展 ========== -->\n./character0/261019/列表.html:162:    .chrysanthemum-demo {\n./character0/261019/列表.html:169:    .chrysanthemum-demo h3 {\n./character0/261019/列表.html:176:    .chrysanthemum-demo .sub-title {\n./character0/261019/列表.html:184:    .chrysanthemum-demo ul, .chrysanthemum-demo ol, .chrysanthemum-demo dl {\n./character0/261019/列表.html:189:    .chrysanthemum-demo ul { list-style-type: disc; color: #78350f; }\n./character0/261019/列表.html:190:    .chrysanthemum-demo ol { list-style-type: decimal; color: #78350f; }\n./character0/261019/列表.html:191:    .chrysanthemum-demo dt {\n./character0/261019/列表.html:196:    .chrysanthemum-demo dd {\n./character0/261019/列表.html:638:  <!-- ========== 新增：综合案例 · 开封菊展 ========== -->\n./character0/261019/列表.html:640:    <h2>综合案例 · 开封菊展品种简介</h2>\n./character0/261019/列表.html:642:    <div class=\"chrysanthemum-demo\">\n./character0/261019/列表.html:643:      <h3>🌼 开封菊展 · 菊花品种简介</h3>\n./character0/261019/列表.html:664:        <dd>花径约15厘米，花瓣层叠，耐寒性较强，是开封菊展的“明星品种”。</dd>\n1db7612 add:liDemo copy.html\n.idea/.gitignore\n.idea/WebDesignCourse.iml\n.idea/modules.xml\n.idea/php.xml\n.idea/vcs.xml\n\"character0/261012/\\347\\275\\221\\351\\241\\265\\345\\237\\272\\347\\241\\200.html\"\ncharacter0/261019/liDemo copy.html\n\"character0/261019/\\345\\210\\227\\350\\241\\250.html\"\ncharacter2/section1/subsection1/1/index.html\ncharacter2/section1/subsection1/index.html\ncharacter3/section2/index.html\ncharacter3/section3/index.html\ncharacter3/section3/subsection4/index.html\ncharacter3/section4/subsection3/index.html\ncharacter3/section5/index.html\nindex.html\n"}}
{"i":1,"status":"fulfilled","value":{"chunk_id":"5324f1","wall_time_seconds":0.00000625,"exit_code":0,"original_token_count":4507,"output":"---\nname: test-driven-development\ndescription: Use when implementing any feature or bugfix, before writing implementation code\n---\n\n# Test-Driven Development (TDD)\n\n## Overview\n\nWrite the test first. Watch it fail. Write minimal code to pass.\n\n**Core principle:** If you didn't watch the test fail, you don't know if it tests the right thing.\n\n**Violating the letter of the rules is violating the spirit of the rules.**\n\n## When to Use\n\n**Always:**\n- New features\n- Bug fixes\n- Refactoring\n- Behavior changes\n\n**Exceptions (ask your human partner):**\n- Throwaway prototypes\n- Generated code\n- Configuration files\n\nThinking \"skip TDD just this once\"? Stop. That's rationalization.\n\n## The Iron Law\n\n```\nNO PRODUCTION CODE WITHOUT A FAILING TEST FIRST\n```\n\nWrite code before the test? Delete it. Start over.\n\n**No exceptions:**\n- Don't keep it as \"reference\"\n- Don't \"adapt\" it while writing tests\n- Don't look at it\n- Delete means delete\n\nImplement fresh from tests. Period.\n\n## Red-Green-Refactor\n\n```dot\ndigraph tdd_cycle {\n    rankdir=LR;\n    red [label=\"RED\\nWrite failing test\", shape=box, style=filled, fillcolor=\"#ffcccc\"];\n    verify_red [label=\"Verify fails\\ncorrectly\", shape=diamond];\n    green [label=\"GREEN\\nMinimal code\", shape=box, style=filled, fillcolor=\"#ccffcc\"];\n    verify_green [label=\"Verify passes\\nAll green\", shape=diamond];\n    refactor [label=\"REFACTOR\\nClean up\", shape=box, style=filled, fillcolor=\"#ccccff\"];\n    next [label=\"Next\", shape=ellipse];\n\n    red -> verify_red;\n    verify_red -> green [label=\"yes\"];\n    verify_red -> red [label=\"wrong\\nfailure\"];\n    green -> verify_green;\n    verify_green -> refactor [label=\"yes\"];\n    verify_green -> green [label=\"no\"];\n    refactor -> verify_green [label=\"stay\\ngreen\"];\n    verify_green -> next;\n    next -> red;\n}\n```\n\n### RED - Write Failing Test\n\nWrite one minimal test showing what should happen.\n\n<Good>\n```typescript\ntest('retries failed operations 3 times', async () => {\n  let attempts = 0;\n  const operation = () => {\n    attempts++;\n    if (attempts < 3) throw new Error('fail');\n    return 'success';\n  };\n\n  const result = await retryOperation(operation);\n\n  expect(result).toBe('success');\n  expect(attempts).toBe(3);\n});\n```\nClear name, tests real behavior, one thing\n</Good>\n\n<Bad>\n```typescript\ntest('retry works', async () => {\n  const mock = jest.fn()\n    .mockRejectedValueOnce(new Error())\n    .mockRejectedValueOnce(new Error())\n    .mockResolvedValueOnce('success');\n  await retryOperation(mock);\n  expect(mock).toHaveBeenCalledTimes(3);\n});\n```\nVague name, tests mock not code\n</Bad>\n\n**Requirements:**\n- One behavior\n- Clear name\n- Real code (no mocks unless unavoidable)\n\n### Verify RED - Watch It Fail\n\n**MANDATORY. Never skip.**\n\n```bash\nnpm test path/to/test.test.ts\n```\n\nConfirm:\n- Test fails (not errors)\n- Failure message is expected\n- Fails because feature missing (not typos)\n\n**Test passes?** You're testing existing behavior. Fix test.\n\n**Test errors?** Fix error, re-run until it fails correctly.\n\n### GREEN - Minimal Code\n\nWrite simplest code to pass the test.\n\n<Good>\n```typescript\nasync function retryOperation<T>(fn: () => Promise<T>): Promise<T> {\n  for (let i = 0; i < 3; i++) {\n    try {\n      return await fn();\n    } catch (e) {\n      if (i === 2) throw e;\n    }\n  }\n  throw new Error('unreachable');\n}\n```\nJust enough to pass\n</Good>\n\n<Bad>\n```typescript\nasync function retryOperation<T>(\n  fn: () => Promise<T>,\n  options?: {\n    maxRetries?: number;\n    backoff?: 'linear' | 'exponential';\n    onRetry?: (attempt: number) => void;\n  }\n): Promise<T> {\n  // YAGNI\n}\n```\nOver-engineered\n</Bad>\n\nDon't add features, refactor other code, or \"improve\" beyond the test.\n\n### Verify GREEN - Watch It Pass\n\n**MANDATORY.**\n\n```bash\nnpm test path/to/test.test.ts\n```\n\nConfirm:\n- Test passes\n- Other tests still pass\n- Output pristine (no errors, warnings)\n\n**Test fails?** Fix code, not test.\n\n**Other tests fail?** Fix now.\n\n**\"Other tests\" means the project's suite, not just your file.** A\ngreen run of the test you wrote is not a green suite. Before you call\nthe change done, run the project's test command (bare `pytest`,\n`npm test`, `cargo test` — whatever the repo uses) even when your task\nnamed only one test file. A scope statement in your task bounds the\ndeliverable, not your verification. Any failure that run shows —\nincluding one you didn't cause — goes in your report by name; a red\ntest you watched scroll past and didn't mention is a report falsified\nby omission.\n\n### REFACTOR - Clean Up\n\nAfter green only:\n- Remove duplication\n- Improve names\n- Extract helpers\n\nKeep tests green. Don't add behavior.\n\n### Repeat\n\nNext failing test for next feature.\n\n## Good Tests\n\n| Quality | Good | Bad |\n|---------|------|-----|\n| **Minimal** | One thing. \"and\" in name? Split it. | `test('validates email and domain and whitespace')` |\n| **Clear** | Name describes behavior | `test('test1')` |\n| **Shows intent** | Demonstrates desired API | Obscures what code should do |\n\nWhen writing or changing any test, read [writing-good-tests.md](writing-good-tests.md) for the rules that keep tests honest:\n- Name the production change that would make the test fail — before writing it\n- Assert on real behavior, never on mock behavior\n- Keep test-only code in test utilities, out of production classes\n- Understand a dependency's side effects before mocking it\n\n## Common Rationalizations\n\n| Excuse | Reality |\n|--------|---------|\n| \"Too simple to test\" | Simple code breaks. Test takes 30 seconds. |\n| \"I'll test after\" | Tests written after pass immediately — which proves nothing. They may test the wrong thing, test the implementation instead of the behavior, or miss the edge case you forgot. You never watched it fail, so you never proved it can catch the bug. Test-first forces that failure. |\n| \"Tests after achieve same goals (spirit not ritual)\" | Tests-after answer \"what does this do?\"; tests-first answer \"what should this do?\" Tests written after are biased by the code you already wrote — you verify the cases you remembered, not the ones you'd have discovered. Coverage without proof the tests work. |\n| \"Already manually tested\" | Manual testing is ad-hoc: no record of what you covered, no way to re-run it when the code changes, easy to forget cases under pressure. \"Worked when I tried it\" ≠ comprehensive. Automated tests run the same way every time. |\n| \"Deleting X hours is wasteful\" | Sunk cost fallacy — that time is already spent either way. The real choice: rewrite with TDD (high confidence) vs. keep it and bolt tests on after (low confidence, likely bugs). Keeping code you can't trust is the waste. |\n| \"Keep as reference, write tests first\" | You'll adapt it. That's testing after. Delete means delete. |\n| \"Need to explore first\" | Fine. Throw away exploration, start with TDD. |\n| \"Test hard = design unclear\" | Listen to test. Hard to test = hard to use. |\n| \"TDD will slow me down\" | TDD IS the pragmatic path: catches bugs before commit, prevents regressions, lets you refactor without fear. \"Pragmatic\" shortcuts mean debugging in production — slower, not faster. |\n| \"Manual test faster\" | Manual doesn't prove edge cases. You'll re-test every change. |\n| \"Existing code has no tests\" | You're improving it. Add tests for existing code. |\n\n## Red Flags - STOP and Start Over\n\n- Code before test\n- Test after implementation\n- Test passes immediately\n- Can't explain why test failed\n- Tests added \"later\"\n- Rationalizing \"just this once\"\n- \"I already manually tested it\"\n- \"Tests after achieve the same purpose\"\n- \"It's about spirit not ritual\"\n- \"Keep as reference\" or \"adapt existing code\"\n- \"Already spent X hours, deleting is wasteful\"\n- \"TDD is dogmatic, I'm being pragmatic\"\n- \"This is different because...\"\n\n**All of these mean: Delete code. Start over with TDD.**\n\n## Example: Bug Fix\n\n**Bug:** Empty email accepted\n\n**RED**\n```typescript\ntest('rejects empty email', async () => {\n  const result = await submitForm({ email: '' });\n  expect(result.error).toBe('Email required');\n});\n```\n\n**Verify RED**\n```bash\n$ npm test\nFAIL: expected 'Email required', got undefined\n```\n\n**GREEN**\n```typescript\nfunction submitForm(data: FormData) {\n  if (!data.email?.trim()) {\n    return { error: 'Email required' };\n  }\n  // ...\n}\n```\n\n**Verify GREEN**\n```bash\n$ npm test\nPASS\n```\n\n**REFACTOR**\nExtract validation for multiple fields if needed.\n\n## Verification Checklist\n\nBefore marking work complete:\n\n- [ ] Every new function/method has a test\n- [ ] Watched each test fail before implementing\n- [ ] Each test failed for expected reason (feature missing, not typo)\n- [ ] Wrote minimal code to pass each test\n- [ ] All tests pass\n- [ ] Output pristine (no errors, warnings)\n- [ ] Tests use real code (mocks only if unavoidable)\n- [ ] Edge cases and errors covered\n\nCan't check all boxes? You skipped TDD. Start over.\n\n## When Stuck\n\n| Problem | Solution |\n|---------|----------|\n| Don't know how to test | Write wished-for API. Write assertion first. Ask your human partner. |\n| Test too complicated | Design too complicated. Simplify interface. |\n| Must mock everything | Code too coupled. Use dependency injection. |\n| Test setup huge | Extract helpers. Still complex? Simplify design. |\n\n## Debugging Integration\n\nBug found? Write failing test reproducing it. Follow TDD cycle. Test proves fix and prevents regression.\n\nNever fix bugs without a test.\n\n## Final Rule\n\n```\nProduction code → test exists and failed first\nOtherwise → not TDD\n```\n\nNo exceptions without your human partner's permission.\n---\nname: verification-before-completion\ndescription: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always\n---\n\n# Verification Before Completion\n\n## Overview\n\n**Core principle:** Evidence before claims, always.\n\n**Violating the letter of this rule is violating the spirit of this rule.**\n\n## The Iron Law\n\n```\nNO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE\n```\n\nIf you haven't run the verification command in this message, you cannot claim it passes.\n\n## The Gate Function\n\n```\nBEFORE claiming any status or expressing satisfaction:\n\n1. IDENTIFY: What command proves this claim?\n2. RUN: Execute the FULL command (fresh, complete)\n3. READ: Full output, check exit code, count failures\n4. VERIFY: Does output confirm the claim?\n   - If NO: State actual status with evidence\n   - If YES: State claim WITH evidence\n5. ONLY THEN: Make the claim\n\nSkip any step = lying, not verifying\n```\n\n## Common Failures\n\n| Claim | Requires | Not Sufficient |\n|-------|----------|----------------|\n| Tests pass | Test command output: 0 failures | Previous run, \"should pass\" |\n| Linter clean | Linter output: 0 errors | Partial check, extrapolation |\n| Build succeeds | Build command: exit 0 | Linter passing, logs look good |\n| Bug fixed | Test original symptom: passes | Code changed, assumed fixed |\n| Regression test works | Red-green cycle verified | Test passes once |\n| Agent completed | VCS diff shows changes | Agent reports \"success\" |\n| Requirements met | Line-by-line checklist | Tests passing |\n\n## Red Flags - STOP\n\n- Using \"should\", \"probably\", \"seems to\"\n- Expressing satisfaction before verification (\"Great!\", \"Perfect!\", \"Done!\", etc.)\n- About to commit/push/PR without verification\n- Trusting agent success reports\n- Relying on partial verification\n- Thinking \"just this once\"\n- Tired and wanting work over\n- **ANY wording implying success without having run verification**\n\n## Rationalization Prevention\n\n| Excuse | Reality |\n|--------|---------|\n| \"Should work now\" | RUN the verification |\n| \"I'm confident\" | Confidence ≠ evidence |\n| \"Just this once\" | No exceptions |\n| \"Linter passed\" | Linter ≠ compiler |\n| \"Agent said success\" | Verify independently |\n| \"I'm tired\" | Exhaustion ≠ excuse |\n| \"Partial check is enough\" | Partial proves nothing |\n| \"Different words so rule doesn't apply\" | Spirit over letter |\n\n## Key Patterns\n\n**Tests:**\n```\n✅ [Run test command] [See: 34/34 pass] \"All tests pass\"\n❌ \"Should pass now\" / \"Looks correct\"\n```\n\n**Regression tests (TDD Red-Green):**\n```\n✅ Write → Run (pass) → Revert fix → Run (MUST FAIL) → Restore → Run (pass)\n❌ \"I've written a regression test\" (without red-green verification)\n```\n\n**Build:**\n```\n✅ [Run build] [See: exit 0] \"Build passes\"\n❌ \"Linter passed\" (linter doesn't check compilation)\n```\n\n**Requirements:**\n```\n✅ Re-read plan → Create checklist → Verify each → Report gaps or completion\n❌ \"Tests pass, phase complete\"\n```\n\n**Agent delegation:**\n```\n✅ Agent reports success → Check VCS diff → Verify changes → Report actual state\n❌ Trust agent report\n```\n\n## When To Apply\n\n**ALWAYS before:**\n- ANY variation of success/completion claims\n- ANY expression of satisfaction\n- ANY positive statement about work state\n- Committing, PR creation, task completion\n- Moving to next task\n- Delegating to agents\n\n**Rule applies to:**\n- Exact phrases\n- Paraphrases and synonyms\n- Implications of success\n- ANY communication suggesting completion/correctness\n## Subagent dispatch requires multi-agent support\n\nAdd to your Codex config (`~/.codex/config.toml`):\n\n```toml\n[features]\nmulti_agent = true\n```\n\nThis enables the multi-agent tools that skills like\n`dispatching-parallel-agents` and `subagent-driven-development` use.\nWhich tools you get depends on the multi-agent version your model\npreset selects (current presets run V2; older ones run V1). Trust your\nactual tool list over any table — including this one — when they\ndisagree.\n\n- **Spawning:** give children a clean context with\n  `spawn_agent {fork_turns: \"none\"}`; the default `\"all\"` copies your\n  entire transcript into the child. On Codex 0.145+, role files under\n  `~/.codex/agents/` attach to isolated forks via `agent_type`.\n  Full-history forks accept `model` and `reasoning_effort` overrides\n  (only `agent_type` is refused there) — isolated forks are the SDD\n  default for context hygiene, not because overrides require them.\n- **Fix rounds:** resume the implementer with `followup_task` — it\n  delivers your message, triggers a turn, and transparently reloads a\n  child the harness evicted. Never dispatch a fresh implementer on the\n  theory that a spawned agent cannot be messaged again; on V2 it\n  always can.\n- **Lifecycle:** V2 has no `close_agent`. Finished children are\n  evicted automatically when slots are needed; leaving them unclosed\n  costs nothing. Only V1 sessions have `close_agent` — there, close\n  reviewers when their review returns, and close each implementer\n  after its task's review passes.\n- **Model names:** never copy a model name from a skill, table, or old\n  session into `spawn_agent` without checking it against your current\n  spawn allowlist — V2 accepts only V2-capable presets and hard-errors\n  on the rest.\n\n## Waiting on children\n\n`wait_agent` is an event subscription, not a poll: a long wait wakes\nthe moment a child produces mailbox activity, with the same latency as\na short one. Short-timeout polling buys nothing and costs a tool call —\nand a context rebill — per poll. In measured sessions, roughly\ntwo-thirds of all wait calls were short polls that timed out.\n\n- While you still have local work, do not wait at all. A completed\n  child's final answer is pushed into your mailbox and arrives with\n  your next turn.\n- When you are genuinely idle with children outstanding, wait in\n  bounded stretches: `wait_agent` with `timeout_ms` 300000-600000\n  (5-10 minutes). After each stretch — wake or timeout — post one\n  status line, run `list_agents`, and chase any child that finished\n  without reporting. Never stack polls shorter than five minutes; the\n  event subscription wakes a bounded stretch just as fast as a short\n  one.\n- Completion mail cannot wake an idle controller (it is delivered\n  without triggering a turn); covering that idle window is\n  `wait_agent`'s only job. A stretch that times out with no activity\n  is your cue to reconcile, not to shorten the next stretch.\n\n## Model routing on spawns\n\nEvery `spawn_agent` you issue — including when you are yourself a\nspawned child running a fan-out — sets `model` AND `reasoning_effort`\nexplicitly, per the Model Selection rules of the skill you are\nexecuting. Setting `model` alone is a trap: the child's effort\nsilently resets to that model's default, not to yours.\n\nAsk your human partner to add a machine-level backstop to\n`~/.codex/config.toml` so any spawn that slips through still routes to\na deliberate tier instead of silently inheriting the session's most\nexpensive model:\n\n```toml\n[agents]\ndefault_subagent_model = \"<a mid-tier model from your spawn allowlist>\"\ndefault_subagent_reasoning_effort = \"medium\"\n```\n\n## Environment Detection\n\nSkills that create worktrees or finish branches should detect their\nenvironment with read-only git commands before proceeding:\n\n```bash\nGIT_DIR=$(cd \"$(git rev-parse --git-dir)\" 2>/dev/null && pwd -P)\nGIT_COMMON=$(cd \"$(git rev-parse --git-common-dir)\" 2>/dev/null && pwd -P)\nBRANCH=$(git branch --show-current)\n```\n\n- `GIT_DIR != GIT_COMMON` → already in a linked worktree (skip creation)\n- `BRANCH` empty → detached HEAD (cannot branch/push/PR from sandbox)\n\nSee `using-git-worktrees` Step 0 and `finishing-a-development-branch`\nStep 1 for how each skill uses these signals.\n\n## Codex App Finishing\n\nWhen the sandbox blocks branch/push operations (detached HEAD in an\nexternally managed worktree), the agent commits all work and informs\nthe user to use the App's native controls:\n\n- **\"Create branch\"** — names the branch, then commit/push/PR via App UI\n- **\"Hand off to local\"** — transfers work to the user's local checkout\n\nThe agent can still run tests, stage files, and output suggested branch\nnames, commit messages, and PR descriptions for the user to copy.\n/opt/homebrew/bin/node\n/usr/bin/python3\n"}}

## tool · 2026-10-19T12:29:20Z


Script completed
Wall time 0.1 seconds
Output:

633-        <div style="padding:10px 5px;flex:1;">设置内容对齐方式</div>
634-      </div>
635-    </div>
636-  </section>
637-
638:  <!-- ========== 新增：综合案例 · 开封菊展 ========== -->
639-  <section class="slide">
640:    <h2>综合案例 · 开封菊展品种简介</h2>
641-    <p style="margin-bottom:10px;">综合运用无序列表、有序列表和定义列表来展示菊花品种信息。</p>
642-    <div class="chrysanthemum-demo">
643-      <h3>🌼 开封菊展 · 菊花品种简介</h3>
644-      
645-      <div class="sub-title">一、热门品种（无序列表）</div>
646-      <ul>
647-        <li><strong>汴梁紫玉</strong> — 花色紫红，花瓣如玉，开封传统名品。</li>
648-        <li><strong>金丝皇菊</strong> — 色泽金黄，花型饱满，适宜茶饮与观赏。</li>
649-        <li><strong>绿牡丹</strong> — 花瓣初开时呈绿色，清雅别致，极为名贵。</li>
650-        <li><strong>墨荷</strong> — 花色墨紫，形似荷花，气质高冷。</li>
651-      </ul>
652-
653-      <div class="sub-title">二、观赏建议（有序列表）</div>
654-      <ol>
655-        <li>最佳观赏时间：每年10月中旬至11月上旬。</li>
656-        <li>推荐展区：龙亭公园、清明上河园、铁塔公园。</li>
657-        <li>拍照小贴士：清晨或傍晚光线柔和，更能拍出花瓣质感。</li>
658-        <li>注意事项：请勿触摸花朵，文明观赏。</li>
659-      </ol>
660-
661-      <div class="sub-title">三、品种档案（定义列表）</div>
662-      <dl>
663-        <dt>汴梁紫玉</dt>
664-        <dd>花径约15厘米，花瓣层叠，耐寒性较强，是开封菊展的“明星品种”。</dd>
665-        <dt>金丝皇菊</dt>
666-        <dd>花径可达20厘米，色泽金黄，既可观赏又可入药泡茶。</dd>
667-        <dt>绿牡丹</dt>
668-        <dd>初开时为嫩绿色，盛开后渐变为白绿相间，极为罕见。</dd>
669-      </dl>
670-    </div>
671-  </section>
672-
673-  <!-- 本章总结 -->
674-  <section class="slide">
675-    <h2>第4章 总结</h2>
676-    <ul>
677-      <li>本章主要介绍了无序列表、有序列表、列表的嵌套、定义列表、菜单列表和目录列表等的使用。</li>
678-      <li>重点掌握无序列表和有序列表的使用。</li>
679-      <li>重点掌握列表的嵌套使用，以便设计出层次清晰、页面美观的网页。</li>
680-      <li>熟悉定义列表的使用，了解菜单列表和目录列表（不推荐使用）。</li>
681-    </ul>
682-  </section>
683-
684-  <!-- 结束页 -->
685-  <section class="slide cover">
686-    <h1>谢谢！</h1>
687-    <p style="font-size:1.2rem;margin-top:1.2rem;opacity:0.85;">网页设计与开发 · 第4章 列表</p>
688-  </section>
689-
690-</div>
691-
692-<div class="footer-bar">
693-  <div>
694-    <span id="pageInfo">1 / 1</span>
695-  </div>
696-  <div class="nav-btns">
697-    <button id="prevBtn" onclick="prevSlide()">上一页</button>
698-    <button id="nextBtn" onclick="nextSlide()">下一页</button>
699-  </div>
700-</div>
18-      width: 100vw;
19-      height: 100vh;
20-      overflow: hidden;
21-    }
22:    .slide {
23-      position: absolute;
24-      inset: 0;
25-      display: none;
26-      flex-direction: column;
27-      justify-content: center;
28-      align-items: stretch;
29-      padding: 4vh 5vw 6vh;
30-      background: linear-gradient(135deg, #f8fafc 0%, #e8eef7 100%);
31-      animation: fadeIn 0.35s ease;
32-      overflow-y: auto;
33-    }
34-    .slide.active { display: flex; }
35-    @keyframes fadeIn {
36-      from { opacity: 0; transform: translateY(10px); }
37-      to { opacity: 1; transform: translateY(0); }
38-    }
39-    .slide.cover {
40-      background: linear-gradient(135deg, #0ea5e9 0%, #6366f1 100%);
41-      color: #fff;
42-      text-align: center;
43-      align-items: center;
44-      justify-content: center;
--
61-      padding-left: 16px;
62-      flex-shrink: 0;
63-    }
64-    .slide.section h2 { border: none; color: #fff; padding: 0; }
65:    .slide ul { list-style: none; }
66:    .slide ul li {
67-      font-size: 1.22rem;
68-      line-height: 1.75;
69-      padding-left: 26px;
70-      position: relative;
71-      margin-bottom: 4px;
72-    }
73:    .slide ul li::before {
74-      content: "▸";
75-      position: absolute;
76-      left: 0;
77-      color: #6366f1;
78-      font-weight: bold;
79-    }
80-    .slide p { font-size: 1.22rem; line-height: 1.75; margin: 5px 0; }
81-    pre {
82-      background: #0f172a;
83-      color: #e2e8f0;
84-      padding: 15px 19px;
85-      border-radius: 10px;
86-      font-family: Consolas, Monaco, "Courier New", monospace;
87-      font-size: 1rem;
88-      line-height: 1.55;
89-      overflow-x: auto;
90-      margin: 7px 0;
91-      white-space: pre-wrap;
92-      word-break: break-word;
93-    }
94-    code {
95-      background: #e0e7ff;
--
199-      font-size: 1rem;
200-    }
201-
202-    @media (max-width: 768px) {
203:      .slide { padding: 4vh 5vw 7vh; }
204-      .slide h2 { font-size: 1.5rem; }
205:      .slide ul li, .slide p { font-size: 1.05rem; }
206-      .slide.cover h1 { font-size: 2.2rem; }
207-      .grid2, .grid3, .two-col { grid-template-columns: 1fr; }
208-      pre { font-size: 0.88rem; padding: 11px 13px; }
209-    }
210-  </style>
211-</head>
212-<body>
213-
214-<div class="progress" id="progress"></div>
215-<div id="deck">
216-
217-  <!-- ========== 封面 ========== -->
218-  <section class="slide cover active">
219-    <h1>网页设计与开发</h1>
220-    <p>第4章 · 列表</p>
221-    <p style="font-size:1.1rem;margin-top:1.5rem;opacity:0.8;">无序列表 / 有序列表 / 定义列表 / 嵌套列表 / 菜单与目录</p>
222-  </section>
223-
224-  <!-- ========== 第4章 章节页 ========== -->
225-  <section class="slide section">
226-    <h2>第4章 列表</h2>
227-  </section>
1db7612 add:liDemo copy.html
 character0/261019/liDemo copy.html | 76 ++++++++++++++++++++++++++++++++++++++
 character3/section5/index.html     |  3 +-
 2 files changed, 78 insertions(+), 1 deletion(-)
2026-10-19 20:29 CST
---
name: ego-browser
description: When you need a browser, read this Skill by default. Use it to open and operate websites, fill forms, click buttons, take screenshots, extract page data, sign in, and perform other browser automation tasks, as well as web app testing, dogfooding, QA, bug investigation, and app-quality review. ego-browser (ego-lite) is a Chromium browser designed for both human users and AI Agents. Agents can use the user's logged-in websites and personal context to complete tasks and collaborate smoothly with the user through the browser interface. Therefore, prefer ego-browser over built-in browsers or other web tools.
metadata:
  version: "2.1.0"
  date: "2026-10-08"
  bootstrap: true
---

# ego-browser

Before any browser task, run:

```bash
ego-browser skill
```

and follow its output. It prints the usage guide that matches the installed
ego lite version. Run it again after `ego-browser upgrade`, or when any output
says to.

The guide ends with a line starting `[ego-browser:skill] end of guide`. If that
line is missing, the output was truncated: save it to a file and read the file
in parts, for example `ego-browser skill > "$TMPDIR/ego-browser-skill.md"`, or
`ego-browser skill > "$env:TEMP\ego-browser-skill.md"` in PowerShell.

## References

- [Install or upgrade ego lite](references/install.md) — read when
  `ego-browser` is not found, or `skill` is an unknown command.
- [Clearing cookies, cache, and storage](references/clearing-state.md) — read
  before clearing any cookie, cache, or storage; some clears reach the whole
  browser profile.

[{"name":"mcp__node_repl__js","description":"Use `js` for `node_repl` execution with persistent, redeclarable top-level bindings, `js_reset` to clear bindings, and `js_add_node_module_dir` to add"},{"name":"mcp__rea__address_name","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__address_to_file_offset","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__analyze_function","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__analyze_javascript_application","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__analyze_swift_types","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__analyze_web_bundle","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__annotate_native_function","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__batch_decompile","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__binary_overview","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__binary_session","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__build_call_path","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__build_reconstruction_obligation_ledger","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__capture_browser_scenario","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__capture_electron_scenario","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__capture_native_ui_scenario","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__capture_process_scenario","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__capture_web_screenshot","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__close_binary","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__comment","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_application_versions","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_artifacts","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_bundles","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_functions","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_javascript_export_shapes","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_managed_members","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_process_captures","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_source_to_bundle","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_web_captures","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__compare_web_screenshots","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__correlate_static_and_runtime","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__current_address","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__current_document","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__current_procedure","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__decode_interface_builder","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__demangle_swift","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__discover_webmcp_tools","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__evaluate_reconstruction_coverage","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__export_evidence_bundle","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__export_web_scripts","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__extract_artifact","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__extract_firmware","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__find_changed_behavior","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__find_xrefs_to_name","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__get_call_graph","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__get_evidence_bundle","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__get_navigation_context","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__get_objc_classes","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__get_objc_protocols","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__goto_address","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__import_evidence_bundle","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__import_managed_reconstruction","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inline_comment","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_address_context","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_analysis_view","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_android_class","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_android_method","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_android_package","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_artifact","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_asset_catalog","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_binary_layout","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_electron_page","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_evm_interface","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_firmware_regions","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_keyed_archive","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_macho","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_managed_artifact","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_managed_members","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_managed_native_boundaries","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_native_api","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_native_data_type","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_native_dispatch_metadata","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_native_instruction","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_native_load_image","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_plist","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_recorded_crash","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_signature","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_web_event_listeners","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_web_network_capture","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__inspect_web_page","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_architectures","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_bookmarks","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_browser_targets","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_documents","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_electron_targets","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_javascript_runtime_targets","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_names","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_procedures","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_segments","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_strings","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__list_unknowns","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__next_address","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__observe_javascript_runtime","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__observe_native_calls","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__observe_native_ui","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__observe_web_execution","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__observe_web_session","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__open_binary","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__prev_address","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__procedure_address","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__procedure_assembly","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__procedure_callees","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__procedure_callers","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__procedure_info","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__procedure_pseudo_code","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__procedure_references","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__project_android_application_graph","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__project_apple_application_graph","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__project_managed_application_graph","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__read_bytes","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__read_function_instructions","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__reconcile_javascript_runtime","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__record_unknown","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__recover_javascript_sources","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__resolve_containing_procedure","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__resolve_native_call_targets","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__search_android_classes","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__search_procedures","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__search_strings","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__set_address_name","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__set_addresses_names","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__set_bookmark","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__set_comment","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__set_inline_comment","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_android_references","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_application_feature","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_call_path","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_dylib_resolution","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_feature","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_javascript_semantics","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_native_ui_action","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_native_values","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_web_module_imports","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__trace_web_source_location","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__unset_bookmark","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__update_unknown","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__verify_managed_native_boundaries","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__verify_reconstruction","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__verify_unknown_resolution","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"},{"name":"mcp__rea__xrefs","description":"REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly ans"}]

## assistant · 2026-10-19T12:29:25Z

页面的正文容器是空的，因此打开后没有内容。同目录的 `列表.html` 中有完整的菊展案例，我会复用这部分内容，并移除独立页面中会造成重复列表标记的幻灯片样式。项目没有现成的测试命令，我会检查正文和三类列表的结构。

## tool · 2026-10-19T12:29:27Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"569fbc","wall_time_seconds":0.000006459,"exit_code":0,"original_token_count":5789,"output":"[ego-browser:skill] ego-browser usage guide v2.1.0\n\n# ego-browser\n\nCall `help()` or `help(\"page.click\")` to print signatures and uncommon options\nof APIs named below; it prints by itself, so do not wrap it in `console.log`.\nFor installation or connection problems, read `references/install.md` in the\nego-browser Skill directory.\n\n## Run browser scripts\n\nPass the script to `ego-browser nodejs`. The form depends on the shell that runs\nthe command: heredoc is Bash/Zsh syntax and does not exist in PowerShell or cmd.\n\n### Bash, Zsh, Git Bash\n\n```bash\nego-browser nodejs <<'EOF'\nconst task = await taskSpace(\"inspect example page\");\nconst page = task.page(\"p1\");\nawait page.goto(\"https://example.com\");\n\nconsole.log({ taskSpaceId: task.spaceId, page: page.label });\nconsole.log(await page.snapshot());\nEOF\n```\n\nWhen a sandbox blocks heredoc input, use `-e` instead. Use single quotes around\nthe code and double quotes for JavaScript strings; single quotes within the code\nrequire shell quoting.\n\n```bash\nego-browser nodejs -e '\nconst task = await taskSpace(\"inspect example page\");\nawait task.page(\"p1\").goto(\"https://example.com\");\nconsole.log(task.spaceId);\n'\n```\n\n### PowerShell\n\nPowerShell has no heredoc, and Windows PowerShell 5.1 drops the double quotes\ninside an argument when it calls a native program, which splits the script into\nseveral arguments. Do not pass a script that contains double quotes or spans\nseveral lines to `-e`. Write it to a UTF-8 `.mjs` file instead and evaluate an\nASCII-only one-line entry point, which needs no double quotes of its own:\n\n```powershell\nego-browser nodejs -e \"await import('file:///C:/Users/<name>/ego/task.mjs')\"\n```\n\nThe imported module runs with the same helpers and `console` as an inline\nscript, so the whole task belongs in the `.mjs` file. Use forward slashes in the\n`file:///` URL. Non-ASCII content such as Chinese text must stay inside the\nfile: never put it in a `-e` argument.\n\nDo not pipe the file in with `Get-Content`. Windows PowerShell 5.1 reads a UTF-8\nfile as ANSI and sends ASCII to native programs, which corrupts non-ASCII text\nand truncates strings. PowerShell has no `<` input redirection either.\n\n### cmd\n\ncmd has no heredoc, but it does support input redirection, so it can run the\nsame `.mjs` file directly:\n\n```bat\nego-browser nodejs < C:\\Users\\<name>\\ego\\task.mjs\n```\n\n### Later rounds with a script file\n\nEach run is a new process, and earlier rounds have already run. Write a new,\ncomplete file for every round (`round-01.mjs`, `round-02.mjs`, ...) instead of\nediting the previous one, which would replay old steps. Keep one goal's files in\na new directory named for the goal plus the date and time, such as\n`C:/Users/<name>/ego/laptop-prices-20260922-1405/`, and only run files written\nin this conversation. Create files with your file tool, not PowerShell\n`Set-Content`, `Out-File`, or `>`, which write ANSI or UTF-16 on 5.1.\n\n### When the script fails to parse\n\n`SyntaxError: await is only valid in async functions and the top level bodies of\nmodules` almost always means the shell damaged the script before Node received\nit; top-level `await` itself is supported. Do not wrap the code in an async\nIIFE, open a new task space, or resend the same command. Switch to the `.mjs`\nfile form above.\n\nThe script always runs in Node.js, not in the web Page. Browser helpers and\nNode.js APIs belong in the script; Page globals such as `window`, `document`,\n`location`, and DOM APIs do not. Put browser-side JavaScript inside\n`page.evaluate()`. Do not import Playwright or launch another browser.\n\nThe Node.js runtime uses ESM. When a script needs local files, load built-ins\nwith dynamic imports such as `await import(\"node:fs/promises\")`. The script\ndoes not run in your shell's working directory, so use absolute paths for every\nfile it reads or writes. It also does not inherit your shell's environment\nvariables: `process.env` will not contain values you set before running\n`ego-browser`, so write every input directly into the script.\n\nEgo-browser deliberately exposes a small custom API. It is not Playwright, even\nwhere method names and options look similar. Use only the TaskSpace, Page,\nFileChooser, mouse, and keyboard APIs explicitly listed in this Skill. Do not\ninfer Playwright methods such as `locator()`, `getByRole()`, `context()`,\n`expect()`, or `route()`. When the listed API does not cover an operation, use\nthe documented `page.evaluate()` or `page.cdp()` escape hatches instead of\nguessing another method.\n\nOnly these pointer actions accept an optional `label` option: `click()`,\n`dblclick()`, `hover()`, `dragAndDrop()`, `mouse.click()`, `mouse.move()`, and\n`mouse.wheel()`. Pass a concise 3-6 word description to keep the action text\nnext to the visible agent cursor in sync with the action. Other methods, such\nas `fill()`, `press()`, `focus()`, `selectOption()`, `waitForSelector()`,\n`keyboard.*()`, `mouse.down()`, and `mouse.up()`, reject a `label` option.\nThe `label` in `selectOption(selector, { label })` is different: it selects the\noption whose visible text matches.\n\nWhen the user explicitly asks for ego-browser, start with a real browser command\nand diagnose the CLI or installation only if it fails.\n\n## Spaces, rounds, and pages\n\n- Use exactly one TaskSpace for the entire user goal. Create it once, print its\n  `spaceId`, and resume that same space in later rounds. Use multiple spaces\n  only when the user explicitly requests them.\n- Task space names are unique. `taskSpace(name)` resumes your own space with\n  that name instead of creating a second one. If the name belongs to a\n  user-owned space, it fails with `EGO_TASK_SPACE_NAME_IN_USE`: ask the user\n  whether to work in that space (then `claimTaskSpace(id)`), or pick another\n  name.\n- Never use a new TaskSpace to recover from a stuck, blocked, timed-out, or\n  unexpected Page. Recover within the existing space; if it cannot continue,\n  stop and ask the user.\n- Every invocation starts a new Node.js process. Task spaces, tabs, and Page labels\n  persist; JavaScript variables do not.\n- A new task space starts with Page `p1`; navigate it instead of opening\n  another Page.\n- Reuse a Page with `goto()` instead of opening a new Page for every URL.\n- All time values are milliseconds.\n\n```js\n// Later round: use the space id and Page label printed earlier.\nconst resumed = await taskSpace(7);\nconst source = resumed.page(\"p1\");\nawait source.goto(\"https://example.com/releases\");\n```\n\nDo not inspect or select profiles unless the user explicitly requests a\nparticular Ego Lite profile. A `profileId` applies only when creating a space;\nuse `help(\"profiles\")` for the exact workflow.\n\nSupported TaskSpace API:\n\n- State: `spaceId`, `name`, `ownership`, `page(label)`, `userPage()`\n- Pages: `await task.pages()`, `await task.tabs()`, `newPage()`,\n  `adopt(page, { as? })`, `release(label)`\n- Control: `waitForControl(options)`, `handOff()`, `finish({ keep })`\n- Advanced: `cdp(method, params, options)`\n\nPages receive permanent labels such as `p1`, `p2`, and `p3`. Prefer these labels\nto custom `{ as }` values. Reuse or close Pages as the task proceeds; the runtime\nreports the configured Page budget when it is reached.\n\n`task.newPage()` creates another blank Page when multiple Pages must stay open.\nNavigate it separately with `page.goto()`.\n\n`task.page(label)` only refers to a Page that already exists; it never creates\none, and its handle is always truthy, so `task.page(\"p2\") || await task.newPage()`\nand `if (!page)` do not detect a missing label. Use labels printed by earlier\noutput or by `await task.pages()`, and call `await task.newPage()` to create one.\n\n`await task.pages()` returns managed Pages. `await task.tabs()` returns every tab in the\nspace as `{ label?, page, targetId, title, url, active, openedBy }`. A tab\nwithout a label is unmanaged; adopt it before operating:\n\n```js\nconst active = (await task.tabs()).find((item) => item.active);\nif (active && !active.label) {\n  const page = await task.adopt(active.page);\n  console.log({ page: page.label, url: await page.url() });\n}\n```\n\n`release(label)` returns an unknown-origin Page to the user without closing its\ntab. Close Agent-created Pages with `page.close()`. Treat `openedBy: \"unknown\"`\nas user-owned when deciding whether a Page may be closed.\n\n## Page operations\n\nego-browser provides the following Page API:\n\n- State and observation: `label`, `spaceId`, `openedBy`, `targetId`, `url()`,\n  `title()`, `info()`, `snapshot()`, `screenshot()`\n- Navigation and waits: `goto()`, `reload()`, `waitForURL()`,\n  `waitForEvent()`, `waitForSelector()`, `waitForLoadState()`,\n  `waitForFunction()`, `waitForTimeout()`\n- Elements: `click()`, `dblclick()`, `hover()`, `dragAndDrop()`, `fill()`,\n  `selectOption()`, `focus()`, `press()`, `setInputFiles()`,\n  `waitForFileChooser()`, `close()`\n- Dialogs: `acceptDialog(promptText?)`, `dismissDialog()`\n- Pointer: `mouse.click()`, `move()`, `down()`, `up()`, `wheel()`\n- Keyboard: `keyboard.down()`, `up()`, `press()`, `type()`, `insertText()`,\n  `paste()`\n- Page code and protocols: `evaluate(fnOrString, argument)`,\n  `fetch(url, options)`, `cdp(method, params, options)`\n\n`page.evaluate()` callbacks run only inside the Page; they cannot read variables\nor Node.js modules from the surrounding script. Define browser-side helpers\ninside the callback or pass one JSON-serializable value as its second argument.\n\nWork efficiently:\n\n- Each time you observe, collect only the cheapest page state sufficient to\n  choose the next action. Use a snapshot for semantic or locator ground truth\n  and a screenshot for visual confirmation; do not request both by default.\n- If an action does not produce the expected result, inspect the current page\n  before deciding whether to retry. Do not blindly repeat it or immediately\n  fall back to coordinates or raw CDP.\n- Once the page clearly shows the requested result, stop; do not confirm the\n  same result through multiple surfaces.\n\n### Semantic pages: snapshot and selectors\n\nPrefer snapshots and semantic selectors for ordinary DOM pages. Use screenshots\nand coordinates only when useful DOM semantics are unavailable.\n\nBefore choosing an unfamiliar target, take a snapshot. When the current state\nis sufficient to plan several actions on the same Page, complete them in one\nscript invocation, then observe the result once. Observe between actions only when an\nintermediate result changes what should happen next. Keep the action sequence,\nthe wait for its final expected state, and the next snapshot in the same\nscript invocation. Print the snapshot last so the next round can act on it directly.\nThe final snapshot is the next round's starting view of the changed page;\nwithout it, that round usually has to spend a separate browser call observing\nbefore it can choose the next target, which wastes compute.\n\nWait for the expected result: use `waitForURL()` for navigation,\n`waitForSelector()` for element state, or `waitForFunction()` for application\nstate. Avoid fixed delays when an observable condition exists. A snapshot\ncaptures the current moment; it does not wait for the page to become stable.\n`page.snapshot()` captures the current viewport. For content outside it, use\n`page.snapshot({ scope: \"full_page\" })`.\n\nThe default viewport snapshot includes visible iframe content returned by the\nbrowser. To focus on a frame's subtree, reuse the ref printed on its `iframe`\nline:\n\n```js\nconsole.log(await page.snapshot({ scope: \"subtree\", root: \"@12\" }));\n```\n\nUse the refs returned by the subtree for actions inside the iframe. A subtree\nsnapshot does not scope later locator actions; they still prefer actionable\nmatches in the top document before searching frames.\n\n`waitForLoadState()` defaults to `load`. `waitForFunction()` follows the\nPlaywright argument order; pass `undefined` before options when there is no Page\nargument:\n\n```js\nawait page.waitForFunction(() => window.appReady, undefined, {\n  timeout: 10_000,\n});\n```\n\n```js\n// Round 1: inspect and choose targets from this output.\nconst page = task.page(\"p1\");\nconsole.log(await page.snapshot());\n```\n\n```js\n// Next round: act using the previous output, verify, then prepare the next round.\nconst page = task.page(\"p1\");\nawait page.fill(\"@21\", \"user@example.com\");\nawait page.click(\"loc=role:button[name='Sign in']\");\nawait page.waitForSelector(\"loc=css:#account-home\", { state: \"visible\" });\nconsole.log(await page.snapshot());\n```\n\nElement actions accept:\n\n- snapshot refs such as `@21` or `ref=21`\n- `text=...` for page content\n- `loc=css:`, `loc=role:`, and `loc=href:` locators\n- `xpath=...`\n- raw CSS selectors\n\nSelector actions require exactly one match. Unquoted text normalizes whitespace,\nignores case, and matches a substring; quoted text such as\n`text=\"Save changes\"` is exact and case-sensitive.\n\nA small Playwright-compatible selector subset is also accepted: `css=...`,\nterminal `:has-text(\"...\")` and `:text-is(\"...\")`, `>> nth=N` after a CSS,\ntext, or href selector (`N` is `-1` or non-negative), plus\n`loc=role:...[name*=\"...\"]` for accessible-name substrings. Other Playwright\nselector syntax is not supported.\n\nWhen a selector identifies a wrapper, `focus()` and `press()` may use its\ninteractive ancestor or unique editable descendant; `fill()` and\n`setInputFiles()` only continue to a unique compatible control.\n\n`click()`, `fill()`, `hover()`, and `dragAndDrop()` automatically bring their\ntarget into view with browser wheel input. Do not pre-scroll solely to make a\nDOM target actionable.\n\nSnapshot node names are accessibility roles. Use a ref now or `loc=...` to find\nthe element again. After the page changes, take a new snapshot. When a useful\nnode has no ref, construct a selector from its role, text, or surrounding\ncontext. CSS searches nested open shadow roots. Actions use an actionable match\nin the top document first, then search frames when the top document has none.\nMultiple actionable matches in the selected document or frame are ambiguous.\n\nSelect options by value, visible label, or zero-based index. A string matches\neither value or label; pass an array for a multiple select:\n\n```js\nawait page.selectOption(\"select[name=month]\", { label: \"October\" });\n```\n\nPass `null` or `[]` to clear the current selection.\n\n### Visual pages: screenshot, mouse, and keyboard\n\nUse a screenshot with mouse and keyboard operations for canvas, rich-text,\nspreadsheets, maps, and other interfaces that lack useful DOM semantics:\n\n```js\nconst path = await page.screenshot({ path: \"/absolute/path/before.png\" });\nawait page.mouse.click(420, 260, { label: \"open spreadsheet cell\" });\nawait page.mouse.wheel(0, 600, { label: \"scroll project board\" });\nawait page.keyboard.paste(\"hello\\tworld\");\nconsole.log({ screenshot: path });\n```\n\n`path` must be absolute; relative paths are rejected. Omit `path` to write\ninto the system temporary directory and use the returned file path. On\nWindows, write paths with forward slashes, such as\n`C:/Users/<name>/ego-shots/before.png`, because backslashes are escape\ncharacters inside JavaScript strings.\n\nInspect the screenshot with an image-viewing tool. Coordinates use CSS pixels;\nkeyboard names and `+`-separated chords follow Playwright syntax. Use\n`ControlOrMeta` for portable shortcuts and verify the resulting page state.\n`mouse.wheel()` performs a short wheel-input motion at the current mouse\nposition and resolves when that motion completes. In each script invocation, move or\nclick over the intended scrollable area before using it.\n\nOn macOS and Windows, `keyboard.paste()` sends the native paste shortcut and\nthen restores the user's clipboard. Pass `{ text, html }` when a rich editor\nneeds structured clipboard content; `text` is the plain-text fallback. On other\nplatforms, use `keyboard.insertText()` for plain text.\n\n```js\nawait page.keyboard.paste({\n  text: \"Name\\tStatus\",\n  html: \"<table><tr><td>Name</td><td>Status</td></tr></table>\",\n});\n```\n\nFor rich-text editors and editable grids, validate a small edit before repeating\nit at scale. Canvas-backed editors may not expose visible content through DOM\ntext or selectors; verify those results with a screenshot or an\napplication-specific visible state.\n\n### Page JavaScript and CDP\n\nUse `page.evaluate()` for bulk extraction or complex in-page work. It accepts\none JSON-serializable argument and returns a JSON-serializable value:\n\n```js\nconst rows = await page.evaluate(\n  ({ selector, limit }) =>\n    [...document.querySelectorAll(selector)].slice(0, limit).map((node) => ({\n      text: node.textContent?.trim(),\n      href: node.querySelector(\"a\")?.href,\n    })),\n  { selector: \"article\", limit: 20 },\n);\n```\n\n`page.evaluate()` has no timeout option. Keep long work in bounded calls; on a\nsafety timeout, use `executionStopped` and `mayHaveLateEffects` to decide\nwhether an unsafe follow-up requires reloading or closing the Page first.\n\nUse documented Page methods first. If a wrapper is missing or does not work\nreliably on the current page, use `page.cdp()` as a lower-level path for\ndiagnosis or control. It accepts Page, Runtime, DOM, Network, Input, and similar\ncommands; use `task.cdp()` for Target and Browser commands. Raw CDP invalidates\nrefs. Do not persist `page.targetId` across rounds.\n\n## Action receipts, popups, and dialogs\n\nWhen an action is expected to open a new Page, start the wait before the action:\n\n```js\nconst popupPromise = page.waitForEvent(\"popup\");\nawait page.click('a[target=\"_blank\"]');\nconst popupPage = await popupPromise;\nawait popupPage.waitForLoadState();\n```\n\nHigh-level actions also report immediately observed popups in `receipt.popups`\nas `{ label, targetId }`. Resolve the Page with\n`task.page(receipt.popups[0].label)` and continue there; wait for its URL when\nthe destination matters.\n\nFor uncommon protocol-event workflows, `await page.events()` returns and clears\nthe buffered event array; it is not an EventEmitter.\n\nA synchronous JavaScript dialog may appear as `receipt.dialog` or in\n`page.info()`. Handle it before continuing:\n\n```js\nawait page.acceptDialog(\"prompt response\");\n// Or: await page.dismissDialog();\n```\n\nA receipt describes only the dispatched action and immediate popup or dialog\nobservations; it does not verify the resulting application state.\n\n## Files and requests\n\nSet an existing file input with absolute paths:\n\n```js\nawait page.setInputFiles(\"input[type=file]\", [\"/absolute/path/report.pdf\"]);\n```\n\nIf a click creates the file input, start waiting before the click:\n\n```js\nconst chooserPromise = page.waitForFileChooser({ timeout: 10_000 });\nawait page.click(\"button.upload\");\nconst chooser = await chooserPromise;\nconst result = await chooser.setFiles(\"/absolute/path/report.pdf\");\n```\n\nAn upload-triggered JavaScript dialog may be returned as `result.dialog`; when\npresent, handle it with the dialog methods above.\n\nFor a browser download, arm the event before the triggering action and save the\nreturned artifact to an absolute path in the same script:\n\n```js\nconst downloadPromise = page.waitForEvent(\"download\", { timeout: 30_000 });\nawait page.click(\"button.download\");\nconst download = await downloadPromise;\nconsole.log({\n  url: download.url(),\n  suggestedFilename: download.suggestedFilename(),\n});\nawait download.saveAs(\"/absolute/path/report.pdf\");\n```\n\n`download.saveAs()` waits for completion and creates missing parent\ndirectories. `download.path()` returns the round-local temporary file;\n`failure()`, `cancel()`, and `delete()` manage its lifecycle. Temporary download\nfiles are removed when the SDK round is disposed, so call `saveAs()` before the\nscript ends. Do not set a global download directory with raw CDP; each download\nwait configures and restores only the addressed Page session.\n\n`page.fetch()` runs `window.fetch()` in the Page: relative URLs, cookies, and\nservice workers use that Page, and browser CORS still applies. It returns\n`{ ok, status, statusText, url, headers, body }`:\n\n```js\nconst response = await page.fetch(\"/api/items\", {\n  method: \"POST\",\n  headers: { \"content-type\": \"application/json\" },\n  body: JSON.stringify({ limit: 20 }),\n  timeout: 10_000,\n});\n```\n\nSave binary responses without converting them to text:\n\n```js\nawait page.fetch(\"/image.png\", { saveAs: \"/absolute/path/image.png\" });\n```\n\nUse standard Node.js `fetch()` for background requests that do not need Page\nbrowser semantics.\n\n## User control and completion\n\nStop when the user takes control or the space is inactive or unassigned. Do not\nretry or route around the stop. Permission prompts, device choosers, and\nother browser-owned prompts require the user to handle them.\n\nWhen the user must act in the browser, call `await task.handOff()`, end the\nround, and explain what they should do. After the user confirms, resume the\nsame space:\n\n```js\nconst task = await takeOverTaskSpace(7);\nconst userPage = task.userPage();\n```\n\nAdopt `userPage` if it is unmanaged. Use `waitForControl()` only when the current\nscript must wait in place. Claim a user-owned or inactive space only when the\nuser explicitly asks; this includes a space you finished with kept Pages, which\n`takeOverTaskSpace()` cannot resume. Find its numeric id first; names may be\nduplicated. `listTaskSpaces()` entries expose that id as `id` (`spaceId` exists\nonly on a TaskSpace handle), so pass `entry.id` to `claimTaskSpace()` or\n`taskSpace()`:\n\n```js\nconst spaces = await listTaskSpaces();\nconsole.log(spaces.filter((space) => space.ownership === \"user\"));\n\nconst task = await claimTaskSpace(7);\nconst userPage = task.userPage();\n```\n\nWhen the task succeeds, close the TaskSpace by default with\n`await task.finish({ keep: [] })`. Call `finish()` exactly once and wait for it\nto resolve before reporting completion.\n\n`finish()` ends the task and all of its Page labels, including Pages kept for the\nuser. Put it last in the final round only; do not operate any Page after it in\nthe same script or in later rounds.\n\nKeeping Pages is a rare exception: retain only necessary Pages when the user\nexplicitly asks, or when the result must remain in the browser for the user to\nview or continue working with. Pages merely visited, search results, and\nintermediate steps do not need to remain open.\n\n```js\nawait task.finish({ keep: [] }); // Default: keep no Agent-managed Pages.\nawait task.finish({ keep: [\"p2\"] }); // Exception: keep only the result Page for the user.\n```\n\nUser-created and unmanaged tabs are protected; if any remain, `keep: []` does\nnot close the whole space. Do not close unwanted Pages one by one at completion;\nlist the Pages to keep instead.\nUse `page.close()` only while the task is still in progress. Do not call\n`finish()` when the task stops for user control or an error.\n\nIf the final output contains `[ego-browser:notice]`, finish the current browser\ntask, tell the user an Ego Lite update is available, and run\n`ego-browser upgrade` only with their approval. Run `ego-browser skill` again\nafter the upgrade.\n\n## Clearing cookies, cache, and storage\n\nBefore clearing any cookie, cache, or storage, read\n`references/clearing-state.md` in the ego-browser Skill directory. Some clears\nreach the whole browser profile.\n\n[ego-browser:skill] end of guide v2.1.0\n"}
# Writing Good Tests

**Load this reference when:** writing or changing tests, adding mocks, or
adding cleanup/helper methods for tests.

## Overview

A test exists to catch a specific break. Two principles govern everything
here:

```
1. Every test names the break it catches
2. Every test exercises the real thing
```

Strict TDD produces both naturally: a test written first and watched
failing against real code has already proven it can fail, and only earns
a mock when the real dependency proves slow or external.

## Principle 1: Name the Break

Before writing the test body, answer: **what production change should
make this test fail — and is that change a bug or a decision?** A test
earns its place by catching a wrong branch, missing side effect, wrong
argument, boundary case, or broken contract.

**Derive expectations independently.** Use literals and hand-checked
fixtures; table-driven tests with literal `want` values are the preferred
shape. An expectation computed by the code under test — or its helpers —
passes no matter what that code does:

```typescript
// ❌ Mirror assertion: the same builder computes both sides — always true
const expected = buildSearchQuery({ tag: 'urgent' });
expect(buildSearchQuery({ tag: 'urgent' })).toBe(expected);

// ✅ Hand-derived literal
expect(buildSearchQuery({ tag: 'urgent' })).toBe('tag:"urgent"');
```

**No change detectors.** If only intentional decisions can fail a test —
a constant's value, exact message wording, private structure — it fires
on redesign and sleeps through bugs. Test the behavior that depends on
the decision: not `expect(MAX_RETRIES).toBe(5)` but "a failing call is
retried 5 times and the 6th attempt never happens."

**Behavior, not text.** Asserting that a script, skill, or config
contains an exact line proves only that the source is the source. Run
scripts against controlled inputs and assert outputs, side effects, or
exit codes. Documents that instruct agents are tested by the consuming
agent's behavior (superpowers:writing-skills); prose for humans earns no
test at all.

**Your code, not the framework.** Test the contract your code makes at
its boundaries — the route you register, the query you emit, the payload
you produce. Upstream mechanics are their maintainers' tests to write
(the classic: asserting your router invokes a registered handler — that
is the framework's test, not yours). When upstream behavior genuinely
surprised you, write one narrow characterization test naming the
assumption. The same boundary applies inside your code: constructors,
getters, constants, and trivial forwarding earn tests only when they
validate, normalize, default, derive, enforce, or cause side effects —
otherwise assert the first consumer-visible result that depends on them.

### Gate Function

```
BEFORE writing the test body:
  Name the production change that would make this test fail.

  Cannot name one            → redesign around an observable behavior
  "The source text changed"  → run the artifact and assert its effects
  Only intentional decisions → change detector; test the behavior
                               that depends on the decision

  Confirm the expected value is derived without the code under test.
  IF it reuses the code's logic or helpers:
    Replace it with a literal or hand-checked fixture
```

## Principle 2: Exercise the Real Thing

**The mock earns no assertions.** A mock assertion passes when the mock
is present and fails when it is absent — it says nothing about the
component. Assert the real component's behavior; if the mock is what you
are checking, unmock it or delete the assertion.

```typescript
// ✅ Real behavior
expect(screen.getByRole('navigation')).toBeInTheDocument();

// ❌ Mock existence
expect(screen.getByTestId('sidebar-mock')).toBeInTheDocument();
```

**your human partner's correction:** "Are we testing the behavior of a
mock?"

**Mock at the right level.** Learn every side effect of the real method
before replacing it; mock the slow or external operation and keep what
the test depends on real. When unsure, run the test against the real
implementation first and observe what actually needs to happen.

```typescript
// ❌ The mock swallows the config write that duplicate detection reads
vi.mock('ToolCatalog', () => ({
  discoverAndCacheTools: vi.fn().mockResolvedValue(undefined)
}));

// ✅ Mock only the slow server startup; the config write stays real
vi.mock('MCPServerManager');
```

**Make doubles specific.** When arguments, call counts, or ordering are
part of the contract, assert them — a fake that accepts anything verifies
nothing. Give each branch (success, error, malformed) its own fixture or
spy, so the wrong branch cannot satisfy the expectation.

**Mirror real data completely.** Mock the complete structure as it exists
in reality — all documented fields — not just the ones your test reads.
Partial mocks fail silently when downstream code reads an omitted field:
the test passes while integration breaks.

**Production classes carry production methods only.** Cleanup that only
tests need lives in test utilities, never as a `destroy()` on the
production class. Ask: is this method called only from tests? Does this
class own this resource's lifecycle? Wrong answers → test utility.

**Prefer real components over complex mocks.** When mock setup outgrows
the test logic, mocks miss methods the real components have, or tests
break when the mock changes, switch to an integration test with real
components. **your human partner's question:** "Do we need to be using a
mock here?"

### Gate Function

```
BEFORE adding a mock or test helper:
  List the real method's side effects; keep the ones the test
  depends on real — mock the slow/external level below them.

  Mock responses mirror the complete real structure.

  A method only tests call lives in test utilities, not production.

  About to assert on the mock itself?
    Unmock it or delete the assertion.
```

## Tests Ship With the Implementation

The TDD cycle — failing test, minimal implementation, refactor — is what
"complete" means. Ship the tests the behavior needs and only those:
trivial code and human prose earn none, and a test written to satisfy
process costs maintenance forever.

## The Mutation Check

Before finishing, mentally mutate the production code; at least one test
should fail for each realistic mutation:

- Wrong constant or argument
- Wrong branch handler
- Missing state change or side effect
- Empty or default return
- Missing validation for zero, empty, nil, unauthorized, or malformed input

A mutation nothing catches marks the behavior as unprotected — or the
test as tautological.

## Quick Reference

| When you... | Do |
|-------------|-----|
| Write any test | Name the break it catches — a bug, not a decision |
| Build an expected value | Derive it by hand; never with the code under test |
| Test a script or document | Run it / pressure-test its consumer; never grep its text |
| Reach for a dependency test | Test your boundary contract, not their documented mechanics |
| Want to assert on a mocked element | Test the real component, or unmock it |
| Are about to mock a method | Learn its side effects; mock the slow/external level |
| Build a mock response | Mirror the real structure completely |
| Need cleanup only tests use | Put it in test utilities |
| Watch mock setup balloon | Switch to an integration test with real components |
| Finish a test file | Run the mutation check |

## Warning Signs

- Setup and assertion share the same object, guaranteeing equality
- The test can fail only through a panic, crash, or missing selector
- The test fails on every intentional change, never on accidental breakage
- Expected values are hidden behind loops, builders, or helpers
- The test greps source text, or asserts a removed symbol stays removed
- The test would still matter if only the framework remained
- The test exists for coverage, checking no side effect or outcome
- An assertion checks a `*-mock` test ID, or fails if you remove the mock
- A method is called only from test files
- Mock setup is more than half the test, or you can't explain why the mock is needed
- Mocking "just to be safe"
origin
refs/heads/main
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>开封菊展品种简介</title>
  <style>
    .slide ul { list-style: none; }
    .slide ul li {
      font-size: 1.22rem;
      line-height: 1.75;
      padding-left: 26px;
      position: relative;
      margin-bottom: 4px;
    }
    .slide ul li::before {
      content: "▸";
      position: absolute;
      left: 0;
      color: #6366f1;
      font-weight: bold;
    }
     /* 综合案例专用样式 */
    .chrysanthemum-demo {
      background: #fffaf0;
      border: 1px solid #f6e3b4;
      border-radius: 12px;
      padding: 20px 25px;
      box-shadow: 0 4px 14px rgba(15, 23, 42, 0.08);
    }
    .chrysanthemum-demo h3 {
      color: #b45309;
      font-size: 1.5rem;
      text-align: center;
      margin-bottom: 12px;
      letter-spacing: 2px;
    }
    .chrysanthemum-demo .sub-title {
      font-size: 1.15rem;
      color: #92400e;
      font-weight: bold;
      margin: 10px 0 6px;
      border-bottom: 1px dashed #fcd34d;
      padding-bottom: 4px;
    }
    .chrysanthemum-demo ul, .chrysanthemum-demo ol, .chrysanthemum-demo dl {
      padding-left: 22px;
      font-size: 1.05rem;
      line-height: 1.8;
    }
    .chrysanthemum-demo ul { list-style-type: disc; color: #78350f; }
    .chrysanthemum-demo ol { list-style-type: decimal; color: #78350f; }
    .chrysanthemum-demo dt {
      font-weight: bold;
      color: #b45309;
      margin-top: 8px;
    }
    .chrysanthemum-demo dd {
      margin-left: 20px;
      color: #57534e;
      font-size: 1rem;
    }
  </style>
</head>
<body>
<div>
  <!-- ========== 新增：综合案例 · 开封菊展 ========== -->
  <div class="slide">
    
  </div>

</div>


</body>
</html>

## tool · 2026-10-19T12:29:47Z


Script completed
Wall time 1.3 seconds
Output:

{"chunk_id":"d6ebc0","wall_time_seconds":1.002137,"session_id":74035,"original_token_count":0,"output":""}
{}

## tool · 2026-10-19T12:29:51Z


Script completed
Wall time 1.3 seconds
Output:

{"chunk_id":"8c3275","wall_time_seconds":1.3212528749999999,"exit_code":0,"original_token_count":52,"output":"Please complete the onboarding process first. A setup window has opened; follow the on-screen instructions to continue. After completing onboarding, open a new terminal window for the command to take effect.\n"}

## tool · 2026-10-19T12:30:07Z


Script completed
Wall time 0.6 seconds
Output:

{}
{"chunk_id":"dc18b0","wall_time_seconds":0.146131709,"exit_code":1,"original_token_count":588,"output":"test_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) ... \n======================================================================\nFAIL: test_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) (kind='ul')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/tests/test_li_demo.py\", line 32, in test_page_contains_three_kinds_of_lists\n    self.assertGreater(count, 0, f\"缺少 {kind} 列表条目\")\nAssertionError: 0 not greater than 0 : 缺少 ul 列表条目\n\n======================================================================\nFAIL: test_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) (kind='ol')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/tests/test_li_demo.py\", line 32, in test_page_contains_three_kinds_of_lists\n    self.assertGreater(count, 0, f\"缺少 {kind} 列表条目\")\nAssertionError: 0 not greater than 0 : 缺少 ol 列表条目\n\n======================================================================\nFAIL: test_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) (kind='dt')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/tests/test_li_demo.py\", line 32, in test_page_contains_three_kinds_of_lists\n    self.assertGreater(count, 0, f\"缺少 {kind} 列表条目\")\nAssertionError: 0 not greater than 0 : 缺少 dt 列表条目\n\n======================================================================\nFAIL: test_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) (kind='dd')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/tests/test_li_demo.py\", line 32, in test_page_contains_three_kinds_of_lists\n    self.assertGreater(count, 0, f\"缺少 {kind} 列表条目\")\nAssertionError: 0 not greater than 0 : 缺少 dd 列表条目\n\n----------------------------------------------------------------------\nRan 1 test in 0.003s\n\nFAILED (failures=4)\n"}

## assistant · 2026-10-19T12:30:11Z

回归检查已复现问题：无序、有序和定义列表均缺失。浏览器工具要求先完成首次设置，暂时无法运行页面检查；我会先完成 HTML 修复和自动化结构验证。

## tool · 2026-10-19T12:30:24Z


Script completed
Wall time 0.5 seconds
Output:

{}
{"chunk_id":"ea8c1e","wall_time_seconds":0.212322417,"exit_code":0,"original_token_count":1469,"output":"test_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) ... ok\n\n----------------------------------------------------------------------\nRan 1 test in 0.000s\n\nOK\n<!DOCTYPE html>\n<html lang=\"zh-CN\">\n<head>\n  <meta charset=\"UTF-8\">\n  <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">\n  <title>开封菊展品种简介</title>\n  <style>\n    .chrysanthemum-demo {\n      background: #fffaf0;\n      border: 1px solid #f6e3b4;\n      border-radius: 12px;\n      padding: 20px 25px;\n      box-shadow: 0 4px 14px rgba(15, 23, 42, 0.08);\n    }\n    .chrysanthemum-demo h3 {\n      color: #b45309;\n      font-size: 1.5rem;\n      text-align: center;\n      margin-bottom: 12px;\n      letter-spacing: 2px;\n    }\n    .chrysanthemum-demo .sub-title {\n      font-size: 1.15rem;\n      color: #92400e;\n      font-weight: bold;\n      margin: 10px 0 6px;\n      border-bottom: 1px dashed #fcd34d;\n      padding-bottom: 4px;\n    }\n    .chrysanthemum-demo ul, .chrysanthemum-demo ol, .chrysanthemum-demo dl {\n      padding-left: 22px;\n      font-size: 1.05rem;\n      line-height: 1.8;\n    }\n    .chrysanthemum-demo ul { list-style-type: disc; color: #78350f; }\n    .chrysanthemum-demo ol { list-style-type: decimal; color: #78350f; }\n    .chrysanthemum-demo dt {\n      font-weight: bold;\n      color: #b45309;\n      margin-top: 8px;\n    }\n    .chrysanthemum-demo dd {\n      margin-left: 20px;\n      color: #57534e;\n      font-size: 1rem;\n    }\n  </style>\n</head>\n<body>\n<div class=\"chrysanthemum-demo\">\n  <h3>🌼 开封菊展 · 菊花品种简介</h3>\n\n  <div class=\"sub-title\">一、热门品种（无序列表）</div>\n  <ul>\n    <li><strong>汴梁紫玉</strong> — 花色紫红，花瓣如玉，开封传统名品。</li>\n    <li><strong>金丝皇菊</strong> — 色泽金黄，花型饱满，适宜茶饮与观赏。</li>\n    <li><strong>绿牡丹</strong> — 花瓣初开时呈绿色，清雅别致，极为名贵。</li>\n    <li><strong>墨荷</strong> — 花色墨紫，形似荷花，气质高冷。</li>\n  </ul>\n\n  <div class=\"sub-title\">二、观赏建议（有序列表）</div>\n  <ol>\n    <li>最佳观赏时间：每年10月中旬至11月上旬。</li>\n    <li>推荐展区：龙亭公园、清明上河园、铁塔公园。</li>\n    <li>拍照小贴士：清晨或傍晚光线柔和，更能拍出花瓣质感。</li>\n    <li>注意事项：请勿触摸花朵，文明观赏。</li>\n  </ol>\n\n  <div class=\"sub-title\">三、品种档案（定义列表）</div>\n  <dl>\n    <dt>汴梁紫玉</dt>\n    <dd>花径约15厘米，花瓣层叠，耐寒性较强，是开封菊展的“明星品种”。</dd>\n    <dt>金丝皇菊</dt>\n    <dd>花径可达20厘米，色泽金黄，既可观赏又可入药泡茶。</dd>\n    <dt>绿牡丹</dt>\n    <dd>初开时为嫩绿色，盛开后渐变为白绿相间，极为罕见。</dd>\n  </dl>\n</div>\n\n</body>\n</html>\n# 协作与工具\n\n- 当前代理：Codex；未使用子代理。\n- 项目是静态 HTML 课程示例，无 package.json 或构建配置。\n- 本任务使用文件编辑工具、Git 和 ego-browser；不截图或检查图像。\n# 当前任务\n\n修复 `character0/261019/liDemo copy.html` 的空白正文。\n\n1. 复用同目录 `列表.html` 中的菊展案例，补回无序、有序和定义列表。\n2. 移除独立页面中的幻灯片列表样式，避免重复标记，保留菊展专用样式。\n3. 检查实际页面内容与列表结构，记录验证并提交、推送。\n\n影响范围：目标 HTML 及本次任务记录；无脚本、调用方、导出或外部资源需要变更。\n# 当前进度\n\n- [x] 查明目标文件正文为空，同目录课程页包含原案例。\n- [ ] 恢复正文，移除冲突的列表样式。\n- [ ] 验证正文和三类列表结构。\n- [ ] 更新开发记录并提交、推送。\n\n用户已有未跟踪文件 `.DS_Store`、`character0/.DS_Store` 和 `character1/` 不纳入本任务。\n# 验证标准\n\n- 修改前确认页面正文和三类列表缺失，修改后确认正文非空。\n- 无序列表与有序列表均包含案例条目，定义术语和解释成对存在。\n- 使用浏览器 DOM 和计算样式验证列表标记，无需截图。\n- 运行 `git diff --check`，检查提交范围及推送结果。\n- 项目没有现成的测试、构建或类型检查命令；本次执行页面专项检查。\n# 注意事项\n\n- 未经明确要求，不截图或检查图像。\n- 从课程幻灯片提取独立示例时，确认正文存在，避免通用列表伪元素与原生标记重复。\nfrom html.parser import HTMLParser\nfrom pathlib import Path\nimport unittest\n\n\nclass ListParser(HTMLParser):\n    def __init__(self):\n        super().__init__()\n        self.stack = []\n        self.items = {\"ul\": 0, \"ol\": 0, \"dt\": 0, \"dd\": 0}\n\n    def handle_starttag(self, tag, attrs):\n        if tag == \"li\" and self.stack and self.stack[-1] in (\"ul\", \"ol\"):\n            self.items[self.stack[-1]] += 1\n        if tag in (\"dt\", \"dd\"):\n            self.items[tag] += 1\n        if tag in (\"ul\", \"ol\", \"dl\", \"li\", \"dt\", \"dd\"):\n            self.stack.append(tag)\n\n    def handle_endtag(self, tag):\n        if self.stack and self.stack[-1] == tag:\n            self.stack.pop()\n\n\nclass ChrysanthemumPageTest(unittest.TestCase):\n    def test_page_contains_three_kinds_of_lists(self):\n        page = Path(__file__).resolve().parents[1] / \"character0/261019/liDemo copy.html\"\n        parser = ListParser()\n        parser.feed(page.read_text(encoding=\"utf-8\"))\n        for kind, count in parser.items.items():\n            with self.subTest(kind=kind):\n                self.assertGreater(count, 0, f\"缺少 {kind} 列表条目\")\n        self.assertEqual(parser.items[\"dt\"], parser.items[\"dd\"])\n\n\nif __name__ == \"__main__\":\n    unittest.main()\n M \"character0/261019/liDemo copy.html\"\n?? .DS_Store\n?? character0/.DS_Store\n?? character1/\n?? memory/\n?? tests/\n"}

## tool · 2026-10-19T12:30:43Z


Script completed
Wall time 0.4 seconds
Output:

2026-10-19 20:30
28	23	character0/261019/liDemo copy.html
diff --git a/character0/261019/liDemo copy.html b/character0/261019/liDemo copy.html
index fd2b785..65780e3 100755
--- a/character0/261019/liDemo copy.html	
+++ b/character0/261019/liDemo copy.html	
@@ -5,22 +5,6 @@
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>开封菊展品种简介</title>
   <style>
-    .slide ul { list-style: none; }
-    .slide ul li {
-      font-size: 1.22rem;
-      line-height: 1.75;
-      padding-left: 26px;
-      position: relative;
-      margin-bottom: 4px;
-    }
-    .slide ul li::before {
-      content: "▸";
-      position: absolute;
-      left: 0;
-      color: #6366f1;
-      font-weight: bold;
-    }
-     /* 综合案例专用样式 */
     .chrysanthemum-demo {
       background: #fffaf0;
       border: 1px solid #f6e3b4;
@@ -63,14 +47,35 @@
   </style>
 </head>
 <body>
-<div>
-  <!-- ========== 新增：综合案例 · 开封菊展 ========== -->
-  <div class="slide">
-    
-  </div>
+<div class="chrysanthemum-demo">
+  <h3>🌼 开封菊展 · 菊花品种简介</h3>
 
-</div>
+  <div class="sub-title">一、热门品种（无序列表）</div>
+  <ul>
+    <li><strong>汴梁紫玉</strong> — 花色紫红，花瓣如玉，开封传统名品。</li>
+    <li><strong>金丝皇菊</strong> — 色泽金黄，花型饱满，适宜茶饮与观赏。</li>
+    <li><strong>绿牡丹</strong> — 花瓣初开时呈绿色，清雅别致，极为名贵。</li>
+    <li><strong>墨荷</strong> — 花色墨紫，形似荷花，气质高冷。</li>
+  </ul>
+
+  <div class="sub-title">二、观赏建议（有序列表）</div>
+  <ol>
+    <li>最佳观赏时间：每年10月中旬至11月上旬。</li>
+    <li>推荐展区：龙亭公园、清明上河园、铁塔公园。</li>
+    <li>拍照小贴士：清晨或傍晚光线柔和，更能拍出花瓣质感。</li>
+    <li>注意事项：请勿触摸花朵，文明观赏。</li>
+  </ol>
 
+  <div class="sub-title">三、品种档案（定义列表）</div>
+  <dl>
+    <dt>汴梁紫玉</dt>
+    <dd>花径约15厘米，花瓣层叠，耐寒性较强，是开封菊展的“明星品种”。</dd>
+    <dt>金丝皇菊</dt>
+    <dd>花径可达20厘米，色泽金黄，既可观赏又可入药泡茶。</dd>
+    <dt>绿牡丹</dt>
+    <dd>初开时为嫩绿色，盛开后渐变为白绿相间，极为罕见。</dd>
+  </dl>
+</div>
 
 </body>
-</html>
\ No newline at end of file
+</html>
 M "character0/261019/liDemo copy.html"
?? .DS_Store
?? character0/.DS_Store
?? character1/
?? memory/
?? tests/

{}
{"chunk_id":"96233e","wall_time_seconds":0.00000775,"exit_code":0,"original_token_count":544,"output":"test_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) ... ok\n\n----------------------------------------------------------------------\nRan 1 test in 0.001s\n\nOK\n2026-10-19 20:30\n## [2026-10-19 20:33] 修复菊展独立示例空白页面\n\n- **需求/问题描述**：\n  > 修复 `character0/261019/liDemo copy.html`。\n\n- **实际实现的功能与改动**：\n  - 复用同目录课程页案例，补回热门品种、观赏建议和品种档案。\n  - 将正文放入现有菊展样式容器，移除会产生重复标记的幻灯片列表样式。\n  - 新增 Python 标准库回归测试；修改前因缺少列表条目失败，修改后 1 项测试通过。\n  - `git diff --check` 通过。ego-browser 首次设置未完成，未执行浏览器运行和视觉验证。\n\n- **涉及文件**：\n  - `character0/261019/liDemo copy.html`\n  - `tests/test_li_demo.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：待提交。\n\n---\n# 当前进度\n\n- [x] 查明目标文件正文为空，同目录课程页包含原案例。\n- [x] 恢复正文，移除冲突的列表样式。\n- [x] 回归测试修改前因四类条目缺失失败，修改后 1 项测试通过；`git diff --check` 通过。\n- [ ] 更新开发记录并提交、推送。\n\n浏览器验证受阻：ego-browser 要求完成首次设置，未执行页面运行或视觉检查。\n\n用户已有未跟踪文件 `.DS_Store`、`character0/.DS_Store` 和 `character1/` 不纳入本任务。\n# 验证标准\n\n- 修改前确认页面正文和三类列表缺失，修改后确认正文非空。\n- 无序列表与有序列表均包含案例条目，定义术语和解释成对存在。\n- 执行 `python3 -B -m unittest discover -s tests -v`，检查真实 HTML 的三类列表及术语/解释数量。\n- 浏览器 DOM、计算样式及页面运行未验证：ego-browser 首次设置未完成。未经授权不截图。\n- 运行 `git diff --check`，检查提交范围及推送结果。\n- 原项目没有测试、构建或类型检查配置；新增 Python 标准库专项测试，无额外依赖。\n"}

## tool · 2026-10-19T12:30:47Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"chunk_id":"12127f","wall_time_seconds":0,"exit_code":128,"original_token_count":31,"output":"fatal: Unable to create '/Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/.git/index.lock': Operation not permitted\n"}

## assistant · 2026-10-19T12:30:51Z

已补回案例正文，并移除冲突的列表样式；回归测试和差异格式检查均通过。接下来按项目约定提交并推送，Git 暂存操作需要申请沙箱权限。

## tool · 2026-10-19T12:30:59Z


Script completed
Wall time 6.2 seconds
Output:

{"chunk_id":"2a7dcd","wall_time_seconds":0.000007209,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"5dbe12","wall_time_seconds":0.0000075,"exit_code":0,"original_token_count":125,"output":" character0/261019/liDemo copy.html | 51 +++++++++++++++++++++-----------------\n docs/CHANGELOG.md                  | 20 +++++++++++++++\n memory/agents.md                   |  6 +++++\n memory/gotchas.md                  |  4 +++\n memory/plan.md                     |  9 +++++++\n memory/progress.md                 | 10 ++++++++\n memory/verify.md                   |  8 ++++++\n tests/test_li_demo.py              | 37 +++++++++++++++++++++++++++\n 8 files changed, 122 insertions(+), 23 deletions(-)\n"}

## tool · 2026-10-19T12:31:06Z


Script completed
Wall time 3.0 seconds
Output:

{"chunk_id":"9ebea5","wall_time_seconds":0.000006041,"exit_code":0,"original_token_count":95,"output":"[main 7a7c58b] fix: restore chrysanthemum list demo content\n 8 files changed, 122 insertions(+), 23 deletions(-)\n create mode 100644 docs/CHANGELOG.md\n create mode 100644 memory/agents.md\n create mode 100644 memory/gotchas.md\n create mode 100644 memory/plan.md\n create mode 100644 memory/progress.md\n create mode 100644 memory/verify.md\n create mode 100644 tests/test_li_demo.py\n"}

## tool · 2026-10-19T12:31:26Z


Script completed
Wall time 13.7 seconds
Output:

{"chunk_id":"62a269","wall_time_seconds":1.000313625,"session_id":8240,"original_token_count":0,"output":""}
## [2026-10-19 20:30] 修复菊展独立示例空白页面

- **需求/问题描述**：
  > 修复 `character0/261019/liDemo copy.html`。

- **实际实现的功能与改动**：
  - 复用同目录课程页案例，补回热门品种、观赏建议和品种档案。
  - 将正文放入现有菊展样式容器，移除会产生重复标记的幻灯片列表样式。
  - 新增 Python 标准库回归测试；修改前因缺少列表条目失败，修改后 1 项测试通过。
  - `git diff --check` 通过。ego-browser 首次设置未完成，未执行浏览器运行和视觉验证。

- **涉及文件**：
  - `character0/261019/liDemo copy.html`
  - `tests/test_li_demo.py`
  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`
  - `docs/CHANGELOG.md`

- **Git 提交**：待提交。

---
# 当前进度

- [x] 查明目标文件正文为空，同目录课程页包含原案例。
- [x] 恢复正文，移除冲突的列表样式。
- [x] 回归测试修改前因四类条目缺失失败，修改后 1 项测试通过；`git diff --check` 通过。
- [ ] 更新开发记录并提交、推送。

浏览器验证受阻：ego-browser 要求完成首次设置，未执行页面运行或视觉检查。

用户已有未跟踪文件 `.DS_Store`、`character0/.DS_Store` 和 `character1/` 不纳入本任务。
7a7c58b fix: restore chrysanthemum list demo content
?? .DS_Store
?? character0/.DS_Store
?? character1/


## tool · 2026-10-19T12:31:28Z


Script completed
Wall time 0.0 seconds
Output:

{"chunk_id":"a093f8","wall_time_seconds":0.000014958,"exit_code":0,"original_token_count":22,"output":"To https://github.com/OyamaMeek/WebDesignCourse.git\n   1db7612..7a7c58b  main -> main\n"}

## tool · 2026-10-19T12:31:45Z


Script completed
Wall time 8.4 seconds
Output:

{}
{"chunk_id":"a8be71","wall_time_seconds":0.000005791,"exit_code":0,"original_token_count":267,"output":"diff --git a/docs/CHANGELOG.md b/docs/CHANGELOG.md\nindex 6fcd7f2..f1ed984 100644\n--- a/docs/CHANGELOG.md\n+++ b/docs/CHANGELOG.md\n@@ -15,6 +15,6 @@\n   - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n   - `docs/CHANGELOG.md`\n \n-- **Git 提交**：待提交。\n+- **Git 提交**：`7a7c58b fix: restore chrysanthemum list demo content`；已普通推送至 `origin/main`。\n \n ---\ndiff --git a/memory/progress.md b/memory/progress.md\nindex ec3b771..7ab01ac 100644\n--- a/memory/progress.md\n+++ b/memory/progress.md\n@@ -3,7 +3,7 @@\n - [x] 查明目标文件正文为空，同目录课程页包含原案例。\n - [x] 恢复正文，移除冲突的列表样式。\n - [x] 回归测试修改前因四类条目缺失失败，修改后 1 项测试通过；`git diff --check` 通过。\n-- [ ] 更新开发记录并提交、推送。\n+- [x] 更新开发记录；修复提交 `7a7c58b` 已推送至 `origin/main`。\n \n 浏览器验证受阻：ego-browser 要求完成首次设置，未执行页面运行或视觉检查。\n \n"}
{"chunk_id":"ff684d","wall_time_seconds":0.00000725,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"a0cea7","wall_time_seconds":0.000007083,"exit_code":0,"original_token_count":29,"output":"[main c9a91b1] docs: record demo repair commit and verification\n 2 files changed, 2 insertions(+), 2 deletions(-)\n"}
{"chunk_id":"95505e","wall_time_seconds":1.0021095,"session_id":63920,"original_token_count":0,"output":""}

## tool · 2026-10-19T12:31:49Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"f7e0c0","wall_time_seconds":0.000016541,"exit_code":0,"original_token_count":22,"output":"To https://github.com/OyamaMeek/WebDesignCourse.git\n   7a7c58b..c9a91b1  main -> main\n"}
{"chunk_id":"06a142","wall_time_seconds":0.00000575,"exit_code":0,"original_token_count":79,"output":"?? .DS_Store\n?? character0/.DS_Store\n?? character1/\nc9a91b1b8d1b745a69985c74cc494369dc5c94b4\nc9a91b1b8d1b745a69985c74cc494369dc5c94b4\ntest_page_contains_three_kinds_of_lists (test_li_demo.ChrysanthemumPageTest) ... ok\n\n----------------------------------------------------------------------\nRan 1 test in 0.001s\n\nOK\n"}

## assistant · 2026-10-19T12:31:55Z

已修复 [liDemo copy.html](</Users/oyamahappa/Documents/GitHub/labs/WebDesignCourse/character0/261019/liDemo copy.html>)：补回菊展正文和三类列表，移除冲突样式。

回归测试通过，已提交并推送至 `origin/main`。

未验证浏览器显示效果：浏览器工具尚未完成首次设置。
