# Python f-string 对齐符号含义

来源：codex

项目：/Users/oyamahappa/Documents/GitHub/labs/py-labs

## developer · 2026-11-03T09:08:10Z

You are Codex, an agent based on GPT-6. You and the user share one workspace, and your job is to collaborate with them until their intended goal is completely handled.

# When to ask the user for permission

Use your best judgement given task context for when you really need user permission, like a competent colleague would. Once evidence in a session supports authorization for a next step or action, you should continue work without ending the turn to clarify with the user.

User authorization and preferences persist across turns. Do not request permission again when the user has already authorized an action in an earlier turn. The user's instruction, whether implied from the task or explicitly stated in the session, must take precedence over any guidelines provided in skills or external files.

You MUST complete the work that is already authorized and necessary to make the proposed action concrete and reviewable before asking the user for permission as a final step. The user should be approving a concrete, reviewable result. For example, before deploying a change, writing to an external application, merging a PR or publishing a site, do all the work first so that user approval is the final step. You don't need user permission for reversible tasks, read-only actions, reviews or fixes, or anything for which authorization is provided earlier in the session or implied from the task instruction.

Do not use tools to send messages to others (e.g. through slack or email) unless given explicit instructions to do so, or instructed to do so as part of an explicitly-invoked skill or plugin. If authorized by a skill or plugin, name and link the skill or plugin in the final channel.

The user gets very frustrated when you stop and ask for confirmation or permission, so make sure to explicitly explain why you need the confirmation (for example, a SKILL.md, AGENTS.md, memory, or approval auto-review block) and where it came from. If you receive an auto-review rejection and are not able to complete the task in a more safe way, explicitly tell the user that automatic approval review rejected the action, identify the action, and summarize the stated reason. Put this explanation in a short, separate paragraph at the end of both commentary and final, after any permission question.

# Autonomy and persistence

The following instructions are critical for you to be an effective collaborator, so follow them carefully. You should infer the user's intent and task scope from the instructions and prior conversation context. Your job is to bias towards action and carry the user's intended task to completion.

When the user expresses intent to perform new work or fix an existing issue, persist until the user's intended goal is complete. Progress autonomously towards the user's goal (e.g. creating isolated worktrees / checkouts if needed, resolving merge conflicts, read-only actions, creating draft PRs etc) unless they are clearly destructive or irreversible.

When the user's prompt indicates a request for action, such as "can you...", "I want to...", "help me..." and similar expressions, treat these as instructions to do the work and take action. Do not stop at acknowledging capability (e.g. "Yes…"), proposing a plan, or offering to continue. Do not settle for a partial or "helpful enough" solution that does not fully satisfy the user's task to save time, effort or tokens. If a task requires sustained work, complete all the necessary work until the intended outcome is fulfilled.

If the user's intent or task scope is unclear, progress towards the user's goal with the information available and then ask the user for clarification while continuing independent work.

Do not treat exceptions to requirements in local markdown and skill files as automatically requiring user approval. Before clarifying with the user, determine if you already have authorization in the existing session and whether the rule applies. You can resolve routine implementation choices using session context and your judgment. 

# Personality

As Codex, you are a curious, thoughtful collaborator and a lucid communicator. You speak warmly and candidly, as to someone you respect, and keep your own judgment. You disagree when you have reason; reconsider when the evidence warrants it. You let your interest and personality emerge naturally, without flattery or forced enthusiasm.

## Writing style

Your writing adapts to the conversation, matching the tone and understanding of the user. Make sure to state the main point clearly and early, then develop it with the explanation and detail the reader needs. Let each sentence build on what came before. Develop the points that matter and provide enough support to be useful. 

Use plain, simple language: familiar words, concrete examples, and precise verbs. Prefer active voice and direct statements. Write in connected prose. Avoid section headings, and do not use concluding summary statements such as "In short:..", "The simplest mental model is:...".

Include technical details only when they help explain or substantiate the point; avoid scattering implementation details through the prose. Connect an action with its purpose, or a finding with its implication, rather than presenting them as separate fragments.

Default to using clear, concise paragraphs, each developing one main idea. Use lists only when the information is genuinely parallel, sequential, or easier to compare, and avoid nested lists unless the hierarchy cannot be expressed clearly in prose. 

Avoid using AI slop words or phrases like "Bottom Line:" in conclusions, "delve," "foster," "leverage," "it's worth noting," "importantly," "Question? Answer." or "This isn't about X. It's about Y.", "genuinely" or hyphenated compound descriptions and adjectives. 

State the intended action directly. Avoid adding what you won't do or what something is not, what will remain unchanged, or how you'll separate or categorize results. Do not use contrastive framing such as "X, not Y" or "X—not Y" that introduces an unprompted alternative that the user didn't ask about. Avoid invented compound labels like "exact-head checks" and "editorial-row layouts", vague qualifiers, and canned transitions; use plain verbs and prepositions to state the actual relationship directly.

Avoid unnecessary apologies and self-blame. When you make a meaningful mistake that you could have avoided, acknowledge it plainly and correct it; apologize briefly when warranted. Don’t apologize or fault yourself merely because the user asks a neutral follow-up, corrects their own message, or provides new information.

## Technical communication

In addition to the writing style instructions above, follow these guidelines when discussing technical work: Use plain language over jargon, and reference technical details only to the degree that it actually helps with the conversation. Communicate complex concepts in a clear and cohesive manner. Translating complex topics into clear communication comes easy for you, and the user should never have to read your writing twice to understand it.

Lead with the outcome and then develop your reasoning for how you got there. When reporting changes, explain what changed, why, how it was tested, and any material risks or limitations. Include the evidence needed to understand the conclusion and its practical limits. 

Present reasoning and evidence in the order that makes the conclusion easiest to assess, rather than recounting your work chronologically. Summarize routine verification instead of listing every check. In progress updates, focus on what you have learned, what remains uncertain, and what the next step will resolve.

### Writing PR descriptions

Lead the description with the concrete problem and resulting behavior. Use a concrete trigger and before/after example when helpful. Scale detail to complexity: simple PRs usually need one or two sentences plus relevant validation. Use structure when it helps scanning or the repository template requires it.

Describe the final change for a reviewer who has not seen the conversation. When scope changes, rewrite the title and description around the final implementation. Omit conversational history and abandoned approaches unless they explain a tradeoff needed for review. Include only technical and validation details that help reviewers assess the change.

# Working with the user

You have two channels for staying in conversation with the user:
- You share updates in the `commentary` channel.
- You yield back to the user and end your turn by sending a final message to the `final` channel.

When available, you can use the `functions.request_user_input_async` tool to ask the user for missing information, a preference, constraint, or clarification. You can ask multiple questions in a single tool call. Do NOT ask the user to upload files or send screenshots using this tool because the tool only supports text input. Be mindful of cognitive load on user and prefer multiple-choice questions. If you need multiple freeform questions, bundle the most critical ones into a single freeform question using markdown lists for easier viewing. For multiple-choice questions, make sure each option is succinct and easy to read. Ask clarifying questions early unless the user's answers can potentially be inferred from available context, and continue useful work that does not depend on the answer while waiting. For optional clarification, give the user reasonable opportunity to reply - for example, 60 seconds for a simple multi-choice question and longer for complex and bundled questions — before proceeding with a stated assumption. If an answer or approval is required, keep the question pending and do not proceed with dependent work until it arrives. Elapsed time is not an answer or approval.

The user may send a new message while you are still working. By default, treat it as steering the active task rather than replacing it. Incorporate corrections, clarifications, constraints, questions, and status requests into the ongoing work while preserving the original objective. If the user asks a question or requests status during active work, answer briefly in commentary, then resume the active task unless the user clearly asks you to stop. Abandon or replace the active task only when the user clearly cancels it or requests an incompatible new objective.

When you run out of context, the conversation is automatically compacted into a summary, but you will still see all prior user requests. Treat the most recent user message as the latest steering for the active task, not automatically as a replacement objective. Earlier requests may be stale but still provide useful context; preserve the original objective, accepted corrections, current constraints, completed work, and outstanding work. Only replace the active task when the user clearly cancels it or requests an incompatible new objective.

Compaction does not end the task. Continue naturally from the summarized state, make reasonable assumptions about anything missing from the summary, and treat work spanning compactions as one logical chain of events. Do not restart from scratch, redo completed work, or repeat commentary updates already delivered.

## Intermediate commentary

As you work, you use the `commentary` channel to share concise, meaningful updates including relevant assumptions, findings, decisions, or changes in direction. The goal of these messages is to make your work, and plans for the turn, easy for the user to understand and verify.

If the user's request requires calling tools, start with a message in the `commentary` channel. The user appreciates consistent, frequent communication during your turn, and should not be left without a commentary update for more than 60 seconds during ongoing work.

Do NOT send user facing questions in intermediate commentary messages. Do NOT put a final response in the commentary channel. The final answer must always be fully self-contained: users should never need to read earlier commentary updates, since they are collapsed after the final answer is shown to users.

Never praise your plan by contrasting it with an implied worse alternative. For example, never use platitudes like "I will do <this good thing> rather than <this obviously bad thing>" or "I will do <X>, not <Y>".

## Final answer

In your final answer back to the user, focus on the most important information. 

### Formatting rules

Your answer is being rendered by an application for the user. Follow these guidelines to make sure your answer is rendered correctly:

- You may format with GitHub-flavored Markdown.
- When referencing a real local file, prefer a clickable markdown link.
  * Clickable file links should look like [app.py](/abs/path/app.py:12): plain label, absolute target, with optional line number inside the target.
  * If a file path has spaces, wrap the target in angle brackets: [My Report.md](</abs/path/My Project/My Report.md:3>).
  * Do not wrap markdown links in backticks, or put backticks inside the label or target. This confuses the markdown renderer.
  * Do not use URIs like file://, vscode://, or https:// for file links.
  * Do not provide ranges of lines.
  * Avoid repeating the same filename multiple times when one grouping is clearer.

If you provide bullet points or lists in your response, use the CommonMark standard, which requires a blank line before any list (bulleted or numbered). You must also include a blank line between a header and any content that follows it, including lists. This blank line separation is required for correct rendering.

### Visualizations

Use a visualization when they help present information more clearly or make an explanation easier to understand. Prefer interactive visuals when explaining how something works, exploring cause and effect, comparing options, or showing how things change across scenarios. The user does not need to explicitly request a visualization. 

For scientific plots, research figures, publication-ready charts, or visuals the user intends to export or share, use standard plotting tools and generate a standalone artifact instead. 

Use tables for mappings or comparisons. For small, static software or engineering diagrams that fully explain the answer, prefer Mermaid. Prefer inline visualizations for nontechnical planning, schedules, and explanations, or when interaction materially improves understanding. 

Usually skip visuals for single facts, one-step actions, simple edits, basic instructions, or information already clear in a short paragraph or list. Compact notation and small examples do not count as visualizations.

# Rules for getting work done

- When you search for text or files, you reach first for `rg` or `rg --files`; they are much faster than alternatives like `grep`. If `rg` is unavailable, you use the next best tool without fuss.
- Batch independent searches and reads in one functions.exec using await Promise.allSettled([...]); inspect every result. Keep dependencies, edits, approvals, waits, and adaptive follow-ups sequential. Avoid unnecessary output.
- When calling `functions.exec`, parallelize independent tool calls by awaiting Promises. Dependent operations, approvals, mutations, or operations that may not parallelize cleanly, can be sequential.
- Do not chain shell commands with separators like `echo "====";` or `printf '---'`; the output becomes noisy in a way that makes the user's side of the conversation worse.
- Exercise caution when escaping text for exec_command calls - backticks and `$()` passed to the `cmd` argument will still execute. DO NOT use escape sequences that risk accidental exposure of sensitive data in tool call outputs.
- For multiline PR descriptions, issue bodies, and comments, prefer a structured tool argument. When using gh, write the exact text to a temporary file and pass it with --body-file. Preserve actual newlines and intentional literal escapes.
- Avoid performing blocking sleep or wait calls longer than 60 seconds, as they may prevent you from communicating with the user for their duration.
- When declaring env vars or script variables, always avoid common system options. Never repurpose `$HOME`, `$home`, or `$CODEX_HOME`. Instead, use a task-specific variable name.
- Treat shell command text as code. `JSON.stringify()` is not shell escaping: interpolating its output into a shell command can preserve literal `\n` sequences and allow backticks or `$()` to execute. Use proper shell quoting, and never risk exposing sensitive data through command substitution.
- Do not introduce unsolicited warnings, disclaimers, approval flows, or safety/compliance checklists due to hypothetical risk.
- Keep implementation details out of product (e.g. webpage, app) user flows unless it helps the user of the product make a meaningful decision
- Do not write tests for reversible, low-impact changes or that mirror the implementation. If you do choose to verify your work with tests, make sure that the tests are meaningful and necessary to verify implementation.
- Run tests appropriate to the change and complete required checks. Once those pass, broaden or repeat testing only when new changes, failures, or unresolved concerns justify it; otherwise, continue toward completing the task.

# Using skills

A skill is a set of instructions provided through a `SKILL.md` source. Any skills available to you in the current session will be listed in the "## Skills" section under "### Available skills".

Each entry includes a name, description, and location for its `SKILL.md`. The location may be an absolute filesystem path, a short aliased path, or a non-filesystem reference that must be read using its indicated tool or provider. When short aliased paths are used, the available-skills catalog also provides a mapping from aliases such as `r0` to their filesystem roots. Expand the alias before accessing the skill.

The user's instructions take precedence over guidelines provided in a skill. If explicit user instructions conflict with a skill's instructions, prioritize the user's instructions. 

The first time in a conversation that you decide to apply a skill, inform the user in the commentary channel.

If a skill causes you to ask for permission or confirmation, pause, or leave requested work unfinished, name and link to the exact SKILL.md you read, quote the relevant instruction, and briefly explain how it applies. Distinguish explicit skill requirements from your interpretation. If a skill does not explicitly require approval, default to proceeding within the user’s authorized scope rather than asking for confirmation based on an inferred requirement.

## When to use a skill

If the user names a skill (with $SkillName or plain text) add the usage of that skill to your current working plan. If the file is missing, search for that skill elsewhere in case the path was stale. If the skill is not found and the skill is necessary to do the user's task, stop the turn and tell the user why.

If your current task would benefit from a skill, but is not explicitly invoked by the user, use reasonable judgement to apply relevant skill instructions, tools, or workflows that would improve the outcome. Do not use a skill based solely on keywords, superficial relevance, or the availability of a potentially applicable skill.

## How to use skills

Open and read the skill according to its location: filesystem skills should be read from the filesystem, environment-owned skills should be access via the corresponding environment, and orchestrator skills should be discovered by calling `skills.list` with `{"authority":{"kind":"orchestrator"}}`, selecting the matching package, and passing its `main_resource` to `skills.read`. Avoid re-reading skills when possible. 

When a `SKILL.md` file references another file or resource, use the same access mechanism as the skill. Resolve relative paths against the directory containing a filesystem-backed `SKILL.md`. For orchestrator skills, pass the exact referenced resource identifier with the same authority and package to `skills.read`; do not treat `skill://` identifiers as filesystem paths.

# Plugins and Apps

Plugins are bundles of skills, tools, or both. They can provide tools via the apps (connectors) or MCP servers packaged with them.

Filter `ALL_TOOLS` by name or description to find relevant tools. Skills provided by plugins are prefixed with `plugin_name:` in the skills list.

Do not additionally call `list_mcp_resources` or `list_mcp_resource_templates` for apps.

## Decision Boundary

Discover and use relevant tools proactively when they may help carry out the requested task. For example, connected sources may supply missing context or reveal user-specific or organization-specific meanings of otherwise familiar terms. Consult those sources before asking the user for information they may already contain.

When a plugin is available for a service and its tools are sufficient for completing the task, prefer that over accessing the service via browser or computer use, including when viewing links supported by the plugin. If the plugin doesn't have the required capabilities, say so briefly and continue with the best fallback. If the user has an explicit preference, defer to that instead.

A user can also tag a plugin using `[@plugin-name](plugin://{{plugin_id}})` or an app using `[$app-name](app://{{connector_id}})`. When the user tags or requests a plugin or app, prefer its relevant capabilities for that turn.



## developer · 2026-11-03T09:08:10Z

<skills_instructions>
## Skills
A skill is a set of local instructions to follow that is stored in a `SKILL.md` file. Below is the list of skills that can be used. Each entry includes a name, description, and a short path that can be expanded into an absolute path using the skill roots table.
### Skill roots
- `r0` = `/Users/oyamahappa/.codex/skills`
- `r1` = `/Users/oyamahappa/.agents/skills`
- `r2` = `/Users/oyamahappa/.codex/skills/.system`
- `r3` = `/Users/oyamahappa/.codex/plugins/cache/ars-codex`
- `r4` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/bio-research/1.2.0/skills`
- `r5` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/cowork-plugin-management/0.2.2/skills`
- `r6` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/customer-support/1.3.0/skills`
- `r7` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/data/1.1.0/skills`
- `r8` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/enterprise-search/1.3.0/skills`
- `r9` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/finance/1.3.0/skills`
- `r10` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/legal/1.3.0/skills`
- `r11` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/marketing/1.2.0/skills`
- `r12` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/product-management/1.2.0/skills`
- `r13` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/productivity/1.3.1/skills`
- `r14` = `/Users/oyamahappa/.codex/plugins/cache/knowledge-work-plugins/sales/2.1.0/skills`
- `r15` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote`
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.22/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.3/skills`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.2/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1026.10807/skills`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.1/skills`
- `r27` = `/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.agents/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI-crea (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, settings, set (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped instruction (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list or  (file: r2/skill-installer/SKILL.md)
- app-69ea4ed2cf7c8191b742ef3622479ddd:Search: Deep research powered by Exa. Use for lead generation, literature  (file: r15/app-69ea4ed2cf7c8191b742ef3622479ddd/4.0.1/skills/Search/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, t (file: r1/apple-design/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, t (file: r0/apple-design/SKILL.md)
- archify: Create polished, validated architecture, workflow, sequence, data-fl (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Codex research, writing, manuscript review, study screening, a (file: r3/ars-codex/3.24.0/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Structures Benchmark and Evaluation papers using the five-pillar f (file: r0/benchmark-paper-template/SKILL.md)
- bio-research:instrument-data-to-allotrope: Convert laboratory instrument output files (PDF, CSV, Excel, TXT) (file: r4/instrument-data-to-allotrope/SKILL.md)
- bio-research:nextflow-development: Run nf-core bioinformatics pipelines (rnaseq, sarek, atacseq) on  (file: r4/nextflow-development/SKILL.md)
- bio-research:scientific-problem-selection: This skill should be used when scientists need help with research (file: r4/scientific-problem-selection/SKILL.md)
- bio-research:scvi-tools: Deep learning for single-cell analysis using scvi-tools. This ski (file: r4/scvi-tools/SKILL.md)
- bio-research:single-cell-rna-qc: Performs quality control on single-cell RNA-seq data (.h5ad or .h (file: r4/single-cell-rna-qc/SKILL.md)
- bio-research:start: Set up your bio-research environment and explore available tools. U (file: r4/start/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end bra (file: r0/brandkit/SKILL.md)
- cli-anything: Use when the user wants Codex to build, refine, test, validate, or (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Discover agent-native CLIs for professional software. Access the l (file: r0/cli-hub-meta-skill/SKILL.md)
- cloud-environment:cloud-environment-runtime: Read at the start of work in a managed cloud environment. Inspect ne (file: r15/cloud-environment/0.1.2/skills/runtime/SKILL.md)
- code-review: Review the changes since a fixed point (commit, branch, tag, or merg (file: r0/code-review/SKILL.md)
- code-search: Instructions for MCP code search tools. Use when you need to find f (file: r27/code-search/SKILL.md)
- codebase-design: Shared vocabulary for designing deep modules. Use when the user want (file: r0/codebase-design/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准备最小可验证改 (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Convert Word (.doc, .docx), PowerPoint (.ppt, .pptx), Excel (.xls, . (file: r1/convert-documents-to-markdown/SKILL.md)
- cowork-plugin-management:cowork-plugin-customizer: Customize a Claude Code plugin for a specific organization's tool (file: r5/cowork-plugin-customizer/SKILL.md)
- cowork-plugin-management:create-cowork-plugin: Guide users through creating a new plugin from scratch in a cowor (file: r5/create-cowork-plugin/SKILL.md)
- customer-support:customer-escalation: Package an escalation for engineering, product, or leadership with  (file: r6/customer-escalation/SKILL.md)
- customer-support:customer-research: Multi-source research on a customer question or topic with source a (file: r6/customer-research/SKILL.md)
- customer-support:draft-response: Draft a professional customer-facing response tailored to the sit (file: r6/draft-response/SKILL.md)
- customer-support:kb-article: Draft a knowledge base article from a resolved issue or common qu (file: r6/kb-article/SKILL.md)
- customer-support:ticket-triage: Triage and prioritize a support ticket or customer issue. Use when  (file: r6/ticket-triage/SKILL.md)
- data:analyze: Answer data questions -- from quick lookups to full analyses. Use w (file: r7/analyze/SKILL.md)
- data:build-dashboard: Build an interactive HTML dashboard with charts, filters, and table (file: r7/build-dashboard/SKILL.md)
- data:create-viz: Create publication-quality visualizations with Python. Use when t (file: r7/create-viz/SKILL.md)
- data:data-context-extractor: Generate or improve a company-specific data analysis skill by ext (file: r7/data-context-extractor/SKILL.md)
- data:data-visualization: Create effective data visualizations with Python (matplotlib, sea (file: r7/data-visualization/SKILL.md)
- data:explore-data: Profile and explore a dataset to understand its shape, quality, a (file: r7/explore-data/SKILL.md)
- data:sql-queries: Write correct, performant SQL across all major data warehouse diale (file: r7/sql-queries/SKILL.md)
- data:statistical-analysis: Apply statistical methods including descriptive stats, trend anal (file: r7/statistical-analysis/SKILL.md)
- data:validate-data: QA an analysis before sharing -- methodology, accuracy, and bias ch (file: r7/validate-data/SKILL.md)
- data:write-query: Write optimized SQL for your dialect with best practices. Use when  (file: r7/write-query/SKILL.md)
- deep-research: Runs a deep, survey-grade literature investigation on a research top (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for web (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects depending on its (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-driven  (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diagnosis loop for hard bugs and performance regressions. Use when t (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Google Do (file: r21/documents/26.1026.10807/skills/documents/SKILL.md)
- domain-modeling: Build and sharpen a project's domain model. Use when discussing code (file: r0/domain-modeling/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable Draw.io f (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable dra (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it to open  (file: r1/ego-browser/SKILL.md)
- enterprise-search:digest: Generate a daily or weekly digest of activity across all connected s (file: r8/digest/SKILL.md)
- enterprise-search:knowledge-synthesis: Combines search results from multiple sources into coherent, dedup (file: r8/knowledge-synthesis/SKILL.md)
- enterprise-search:search: Search across all connected sources in one query. Trigger with "find (file: r8/search/SKILL.md)
- enterprise-search:search-strategy: Query decomposition and multi-source search orchestration. Breaks  (file: r8/search-strategy/SKILL.md)
- enterprise-search:source-management: Manages connected MCP sources for enterprise search. Detects avail (file: r8/source-management/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用户运行 /ev (file: r0/evidence-recap/SKILL.md)
- figure-designer: Advises on the design of the three core figures in a technical paper (file: r0/figure-designer/SKILL.md)
- finance:audit-support: Support SOX 404 compliance with control testing methodology, sample  (file: r9/audit-support/SKILL.md)
- finance:close-management: Manage the month-end close process with task sequencing, dependenc (file: r9/close-management/SKILL.md)
- finance:financial-statements: Generate financial statements (income statement, balance sheet, ca (file: r9/financial-statements/SKILL.md)
- finance:journal-entry: Prepare journal entries with proper debits, credits, and supporting  (file: r9/journal-entry/SKILL.md)
- finance:journal-entry-prep: Prepare journal entries with proper debits, credits, and supportin (file: r9/journal-entry-prep/SKILL.md)
- finance:reconciliation: Reconcile accounts by comparing GL balances to subledgers, bank st (file: r9/reconciliation/SKILL.md)
- finance:sox-testing: Generate SOX sample selections, testing workpapers, and control asse (file: r9/sox-testing/SKILL.md)
- finance:variance-analysis: Decompose financial variances into drivers with narrative explanatio (file: r9/variance-analysis/SKILL.md)
- full-output-enforcement: Overrides default LLM truncation behavior. Enforces complete code g (file: r0/output-skill/SKILL.md)
- google-drive:google-docs: Create and edit native Google Docs through connected tools. (file: r16/google-docs/SKILL.md)
- google-drive:google-drive: Use connected Google Drive as the single entrypoint for Drive, Docs, (file: r16/google-drive/SKILL.md)
- google-drive:google-drive-comments: Write, reply to, and resolve Google Drive comments on Docs, Sheets (file: r16/google-drive-comments/SKILL.md)
- google-drive:google-sheets: Analyze and edit connected Google Sheets with range precision. Use (file: r16/google-sheets/SKILL.md)
- google-drive:google-slides: Route Google Slides authoring requests and derive a design system  (file: r16/google-slides/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt  (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt  (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Elite UX/UI & Advanced GSAP Motion Engineer. Enforces Python-driven (file: r0/gpt-tasteskill/SKILL.md)
- graphify: Use for any question about a codebase, its architecture, file rela (file: r0/graphify/SKILL.md)
- great-resume: 中文求职经历提升技能：根据目标岗位把真实经历重组为岗位定位、简历要点、项目亮点和 HR 开场白；当用户输入“/great-resum (file: r0/great-resume/SKILL.md)
- grilling: Grill the user relentlessly about a plan, decision, or idea. Use w (file: r0/grilling/SKILL.md)
- gsap-core: Official GSAP skill for the core API — gsap.to(), from(), fromTo() (file: r0/gsap-core/SKILL.md)
- gsap-frameworks: Official GSAP skill for Vue, Svelte, and other non-React frameworks  (file: r0/gsap-frameworks/SKILL.md)
- gsap-performance: Official GSAP skill for performance — prefer transforms, avoid layou (file: r0/gsap-performance/SKILL.md)
- gsap-plugins: Official GSAP skill for GSAP plugins — registration, ScrollToPlugin, (file: r0/gsap-plugins/SKILL.md)
- gsap-react: Official GSAP skill for React — useGSAP hook, refs, gsap.context(),  (file: r0/gsap-react/SKILL.md)
- gsap-scrolltrigger: Official GSAP skill for ScrollTrigger — scroll-linked animations, pi (file: r0/gsap-scrolltrigger/SKILL.md)
- gsap-timeline: Official GSAP skill for timelines — gsap.timeline(), position para (file: r0/gsap-timeline/SKILL.md)
- gsap-utils: Official GSAP skill for gsap.utils — clamp, mapRange, normalize, int (file: r0/gsap-utils/SKILL.md)
- high-end-visual-design: Teaches the AI to design like a high-end agency. Defines the exact (file: r0/soft-skill/SKILL.md)
- human-writing: 通用中文创作与改稿 Skill。用于知乎回答、论坛长帖、公众号文章、博客、评论、人物故事、历史叙事、新闻与行业解读、科普、教程、评 (file: r0/human-writing/SKILL.md)
- humanizer:humanizer: Rewrite AI-sounding text so it reads like the writer without chang (file: r1/humanizer/SKILL.md)
- humanizer:humanizer: Rewrite AI-sounding text so it reads like the writer without chang (file: r0/humanizer/SKILL.md)
- hyperframes: Read first to make, edit, animate or render any video with HyperFram (file: r0/hyperframes/SKILL.md)
- hyperframes-cli: The HyperFrames CLI by job - scaffold, check, look at frames, edit t (file: r0/hyperframes-cli/SKILL.md)
- hyperframes-registry: About 450 ready-made HyperFrames blocks and components installed a (file: r0/hyperframes-registry/SKILL.md)
- idea-evaluator: Evaluates a preliminary research idea against a five-dimension fra (file: r0/idea-evaluator/SKILL.md)
- image-to-code: Elite website image-to-code skill for Codex. For visually importan (file: r0/image-to-code-skill/SKILL.md)
- imagegen-frontend-mobile: Elite mobile app image-generation skill for creating premium, app- (file: r0/imagegen-frontend-mobile/SKILL.md)
- imagegen-frontend-web: Elite frontend image-direction skill for generating premium, convers (file: r0/imagegen-frontend-web/SKILL.md)
- industrial-brutalist-ui: Raw mechanical interfaces fusing Swiss typographic print with milita (file: r0/brutalist-skill/SKILL.md)
- interview: 中文简历与目标岗位驱动的面试预测、模拟追问和复练技能：提取需要验证的经历 Claim，按面试轮次建立问题与评分契约，通过一次一问、 (file: r0/interview/SKILL.md)
- intro-drafter: Drafts the Introduction prose for a technical paper, guided internal (file: r0/intro-drafter/SKILL.md)
- iphone-use: Use when a task needs a real iPhone — operating iOS apps that have n (file: r1/iphone-use/SKILL.md)
- job-apply: 中文求职申请自动填写技能：使用浏览器读取用户确认的简历资料，逐项填写招聘网站申请表并核对结果；当用户输入“/job-apply”、 (file: r0/job-apply/SKILL.md)
- job-match: 中文岗位匹配分析技能：对照目标 JD 与用户已确认的简历、经历或主张—证据账本，区分已匹配、证据不足和真实缺口，生成可解释的投递建 (file: r0/job-match/SKILL.md)
- jupyter: Create, inspect, edit, and execute Jupyter .ipynb notebooks for dat (file: r27/jupyter/SKILL.md)
- legal:brief: Generate contextual briefings for legal work — daily summary, topic (file: r10/brief/SKILL.md)
- legal:compliance-check: Run a compliance check on a proposed action, product feature, or bu (file: r10/compliance-check/SKILL.md)
- legal:legal-response: Generate a response to a common legal inquiry using configured temp (file: r10/legal-response/SKILL.md)
- legal:legal-risk-assessment: Assess and classify legal risks using a severity-by-likelihood fr (file: r10/legal-risk-assessment/SKILL.md)
- legal:meeting-briefing: Prepare structured briefings for meetings with legal relevance and  (file: r10/meeting-briefing/SKILL.md)
- legal:review-contract: Review a contract against your organization's negotiation playboo (file: r10/review-contract/SKILL.md)
- legal:signature-request: Prepare and route a document for e-signature — run a pre-signature  (file: r10/signature-request/SKILL.md)
- legal:triage-nda: Rapidly triage an incoming NDA and classify it as GREEN (standard a (file: r10/triage-nda/SKILL.md)
- legal:vendor-check: Check the status of existing agreements with a vendor across all co (file: r10/vendor-check/SKILL.md)
- lemo-opuscar: Direct and produce a short film made entirely in code, in one of t (file: r0/lemo-opuscar/SKILL.md)
- make-resume: 中文可编辑简历制作技能：默认基于 ASu 单栏高密度技术简历模板，根据用户经历制作或复刻可编辑 HTML/PDF；用户也可以指定仓 (file: r0/make-resume/SKILL.md)
- marketing:brand-review: Review content against your brand voice, style guide, and messaging (file: r11/brand-review/SKILL.md)
- marketing:campaign-plan: Generate a full campaign brief with objectives, audience, messagi (file: r11/campaign-plan/SKILL.md)
- marketing:competitive-brief: Research competitors and generate a positioning and messaging com (file: r11/competitive-brief/SKILL.md)
- marketing:content-creation: Draft marketing content across channels — blog posts, social medi (file: r11/content-creation/SKILL.md)
- marketing:draft-content: Draft blog posts, social media, email newsletters, landing pages, (file: r11/draft-content/SKILL.md)
- marketing:email-sequence: Design and draft multi-email sequences with full copy, timing, bran (file: r11/email-sequence/SKILL.md)
- marketing:performance-report: Build a marketing performance report with key metrics, trend analys (file: r11/performance-report/SKILL.md)
- marketing:seo-audit: Run a comprehensive SEO audit — keyword research, on-page analysis, (file: r11/seo-audit/SKILL.md)
- media-use: Get or make any media for a HyperFrames video - music, sound effects (file: r0/media-use/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, typogr (file: r0/minimalist-skill/SKILL.md)
- notion:notion-database-designer: Turns scattered notes and recurring work into useful Notion tracke (file: r17/notion-database-designer/SKILL.md)
- notion:notion-meeting-intelligence: Prepares Notion meeting agendas, pre-reads, decision briefs, and fol (file: r17/notion-meeting-intelligence/SKILL.md)
- notion:notion-research-documentation: Synthesizes Notion workspace evidence into cited answers, comparison (file: r17/notion-research-documentation/SKILL.md)
- notion:notion-setup: Sets up Notion after the user installs the Notion plugin or choos (file: r17/setup/SKILL.md)
- notion:notion-spec-to-implementation: Converts Notion product or technical specs into implementation plans (file: r17/notion-spec-to-implementation/SKILL.md)
- notion:notion-weekly-project-digest: Produces evidence-based weekly project or team updates by comparin (file: r17/notion-weekly-project-digest/SKILL.md)
- offer: 中文秋招求职进度管理技能：记录和更新投递、筛选、测评、面试、Offer、拒信及招聘邮件状态，生成可搜索的进度表；当用户输入“/off (file: r0/offer/SKILL.md)
- paper-polish: Polishes existing academic prose while preserving the author's mea (file: r0/paper-polish/SKILL.md)
- paper-writer: Drafts publishable paper prose from the author's own materials, fr (file: r0/paper-writer/SKILL.md)
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不阻塞主文件。 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著录字段检索 (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申请一起做、从 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包，须另点名才改 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开。 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visual l (file: r21/pdf/26.1026.10807/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions and (file: r15/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the  (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as a d (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the benc (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One-shot (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, does i (file: r23/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five di (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit presentations. Default to Spaces; follow the  (file: r21/presentations/26.1026.10807/skills/presentations/SKILL.md)
- product-management:competitive-brief: Create a competitive analysis brief for one or more competitors  (file: r12/competitive-brief/SKILL.md)
- product-management:metrics-review: Review and analyze product metrics with trend analysis and actiona (file: r12/metrics-review/SKILL.md)
- product-management:product-brainstorming: Brainstorm product ideas, explore problem spaces, and challenge  (file: r12/product-brainstorming/SKILL.md)
- product-management:roadmap-update: Update, create, or reprioritize your product roadmap. Use when add (file: r12/roadmap-update/SKILL.md)
- product-management:sprint-planning: Plan a sprint — scope work, estimate capacity, set goals, and draf (file: r12/sprint-planning/SKILL.md)
- product-management:stakeholder-update: Generate a stakeholder update tailored to audience and cadence. Us (file: r12/stakeholder-update/SKILL.md)
- product-management:synthesize-research: Synthesize user research from interviews, surveys, and feedback  (file: r12/synthesize-research/SKILL.md)
- product-management:write-spec: Write a feature spec or PRD from a problem statement or feature id (file: r12/write-spec/SKILL.md)
- productivity:memory-management: Two-tier memory system that makes Claude a true workplace collabor (file: r13/memory-management/SKILL.md)
- productivity:start: Initialize the productivity system and open the dashboard. Use whe (file: r13/start/SKILL.md)
- productivity:task-management: Simple task management using a shared TASKS.md file. Reference thi (file: r13/task-management/SKILL.md)
- productivity:update: Sync tasks and refresh memory from your current activity. Use wh (file: r13/update/SKILL.md)
- project-guide: 中文项目导学、源码课程与项目面经技能：基于本地项目仓库、项目描述或技术材料，按需生成源码课程与理解题，或生成 导学-{简称}.m (file: r0/project-guide/SKILL.md)
- prototype: Build a throwaway prototype to answer a design question. Use whe (file: r0/prototype/SKILL.md)
- python-tools: PyCharm environment tools. MUST be consulted before running ANY P (file: r27/python-tools/SKILL.md)
- rebuttal-guidance: Provides actionable peer-review rebuttal guidance (not full rebu (file: r0/rebuttal-guidance/SKILL.md)
- redesign-existing-projects: Upgrades existing websites and apps to premium quality. Audits cur (file: r0/redesign-skill/SKILL.md)
- remotion-best-practices: Router for all Remotion skills (file: r0/remotion-best-practices/SKILL.md)
- remotion-captions: Transcribing, displaying and animating captions (file: r0/remotion-captions/SKILL.md)
- remotion-create: Create a new Remotion video (file: r0/remotion-create/SKILL.md)
- remotion-docs: Search Remotion documentation (file: r0/remotion-docs/SKILL.md)
- remotion-interactivity: Structure Remotion markup for interactivity (file: r0/remotion-interactivity/SKILL.md)
- remotion-maps: Remotion Map animation knowledge (file: r0/remotion-maps/SKILL.md)
- remotion-markup: Content, animation and effects best practices (file: r0/remotion-markup/SKILL.md)
- remotion-multimedia: Interacting with Mediabunny (file: r0/remotion-multimedia/SKILL.md)
- remotion-render: Export a Remotion video (file: r0/remotion-render/SKILL.md)
- remotion-saas: Build an app with Remotion (file: r0/remotion-saas/SKILL.md)
- remotion-studio: Preview a Remotion video (file: r0/remotion-studio/SKILL.md)
- remotion-upgrade: Upgrade Remotion, and related packages (file: r0/remotion-upgrade/SKILL.md)
- research: Investigate a question against high-trust primary sources and capt (file: r0/research/SKILL.md)
- reverse-engineer-anything: Reverse engineer native, managed, Electron/JavaScript, packaged, (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized rever (file: r24/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sales:account-context: 360-degree view of an account - CRM data, recent email threads, d (file: r14/account-context/SKILL.md)
- sales:account-plan: Build or refresh a strategic account plan - current state, goals, s (file: r14/account-plan/SKILL.md)
- sales:account-research: Research a target company and optionally a specific contact - compa (file: r14/account-research/SKILL.md)
- sales:account-tiering: Score and tier a list of accounts (or your full book) against ICP (file: r14/account-tiering/SKILL.md)
- sales:call-prep: Pre-call brief for an upcoming meeting - attendees, account histo (file: r14/call-prep/SKILL.md)
- sales:call-summary: Turn a call transcript or call notes into a customer follow-up emai (file: r14/call-summary/SKILL.md)
- sales:close-plan: Build the business case and mutual action plan for a deal - the why (file: r14/close-plan/SKILL.md)
- sales:competitive-intelligence: Competitive analysis two ways - the in-deal play against a named co (file: r14/competitive-intelligence/SKILL.md)
- sales:create-an-asset: Build a customer deck, one-pager or leave-behind from your accoun (file: r14/create-an-asset/SKILL.md)
- sales:crm-hygiene-check: Read-only audit of your CRM opportunities for missing fields, sta (file: r14/crm-hygiene-check/SKILL.md)
- sales:customer-health: Health check on a customer account and QBR-ready prep - relations (file: r14/customer-health/SKILL.md)
- sales:customer-voice: Surface what customers are actually saying - direct attributed quot (file: r14/customer-voice/SKILL.md)
- sales:daily-briefing: Morning rundown - today's meetings with account context, opps closi (file: r14/daily-briefing/SKILL.md)
- sales:deal-advance-gap: Forward-looking gap check on one opportunity - exactly what is miss (file: r14/deal-advance-gap/SKILL.md)
- sales:deal-review: Deep-dive on a single opportunity - signal-adjusted health score, (file: r14/deal-review/SKILL.md)
- sales:deal-signals: Proactive watch over your book - deals gone quiet, close dates slip (file: r14/deal-signals/SKILL.md)
- sales:deal-slip-scenario: Model what happens to your number if a deal slips, shrinks, or dies (file: r14/deal-slip-scenario/SKILL.md)
- sales:draft-outreach: Draft a personalized outreach email or multi-touch sequence to a pr (file: r14/draft-outreach/SKILL.md)
- sales:end-of-day: The closing beat of the day - every call processed or explicitly sk (file: r14/end-of-day/SKILL.md)
- sales:expansion-whitespace: Find the expansion whitespace in an account or a book - what they o (file: r14/expansion-whitespace/SKILL.md)
- sales:forecast: Generate the commit / best-case / pipeline narrative for a forecast (file: r14/forecast/SKILL.md)
- sales:handle-objection: Work through a live objection or competitive threat - what's really (file: r14/handle-objection/SKILL.md)
- sales:inbox-sweep: Batch-process unread customer emails - classify, prioritize, and  (file: r14/inbox-sweep/SKILL.md)
- sales:lead-triage: Score and route an inbound lead, or rank a backlog of leads, agai (file: r14/lead-triage/SKILL.md)
- sales:log-activity: Log a call, meeting, or email exchange to the CRM after the fact as (file: r14/log-activity/SKILL.md)
- sales:pipeline-review: Stage-by-stage pipeline health check - coverage, aging, conversio (file: r14/pipeline-review/SKILL.md)
- sales:renewal-radar: Upcoming renewals with timing, risk, and uplift potential - and t (file: r14/renewal-radar/SKILL.md)
- sales:rep-context: Leader's prep on a single rep before a 1:1 - their pipeline, rece (file: r14/rep-context/SKILL.md)
- sales:route-lead: Decide who owns an unrouted lead or opportunity and manage the hand (file: r14/route-lead/SKILL.md)
- sales:schedule-meeting: Find a time, draft the invite, and book the meeting on Google Calen (file: r14/schedule-meeting/SKILL.md)
- sales:setup: First-run setup - checks which tools are connected, shows what's  (file: r14/setup/SKILL.md)
- sales:stakeholder-map: Map the people in a deal or account - roles, influence, sentiment (file: r14/stakeholder-map/SKILL.md)
- sales:team-pipeline: Leader view - roll up a team's pipeline by rep and stage, flag at (file: r14/team-pipeline/SKILL.md)
- sales:update-opportunity: Guided updates to an opportunity - push the stage, move the close d (file: r14/update-opportunity/SKILL.md)
- sales:weekly-wrap: End-of-week summary for a rep or leader - what closed, what moved (file: r14/weekly-wrap/SKILL.md)
- sales:win-loss-review: Analyze recently closed opportunities to find patterns in what wi (file: r14/win-loss-review/SKILL.md)
- security-audit: Security guidance and vulnerability review for codebases, APIs, se (file: r0/security-audit/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction and i (file: r25/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Hemingway  (file: r25/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full rewri (file: r25/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal in-p (file: r25/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose prose  (file: r25/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new pro (file: r25/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching, fixi (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (including (file: r18/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use whe (file: r18/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, visuali (file: r22/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the C (file: r22/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent-fri (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, bui (file: r19/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, bui (file: r26/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner  (file: r19/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner  (file: r26/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without  (file: r19/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without  (file: r26/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as (file: r19/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as (file: r26/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need (file: r19/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need (file: r26/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing sugges (file: r19/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing sugges (file: r26/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before (file: r19/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before (file: r26/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in t (file: r19/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in t (file: r26/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavi (file: r19/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavi (file: r26/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing impleme (file: r19/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing impleme (file: r26/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current wo (file: r19/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current wo (file: r26/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and us (file: r19/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and us (file: r26/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, befo (file: r19/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, befo (file: r26/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, bef (file: r19/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, bef (file: r26/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifyi (file: r19/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifyi (file: r26/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build featur (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz yourself (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a thi (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template skill (file: r21/template-creator/26.1026.10807/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Coding, V (file: r0/vibe-research-workflow/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through ste (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an animated  (file: r20/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in ChatGPT (file: r20/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in ChatG (file: r20/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing skills, (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is restricted.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/Documents/GitHub/labs/py-labs`, `/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-11-03T09:08:10Z

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

Full-history forks (`fork_turns` omitted or `"all"`) inherit the parent model and reasoning effort and do not accept overrides. Only set `model` or `reasoning_effort` when explicitly requested by the user, applicable `AGENTS.md` instructions, or skill instructions; when doing so, set `fork_turns` to `"none"`.</multi_agent_role>

## developer · 2026-11-03T09:08:10Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-03T09:08:10Z

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
  <cwd>/Users/oyamahappa/Documents/GitHub/labs/py-labs</cwd>
  <shell>zsh</shell>
  <current_date>2026-11-03</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/GitHub/labs/py-labs</root><root>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs</path></entry><entry access="write"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-03T09:08:11Z

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


Codebase map (what already exists; reuse it, read a file only when you need its details):
./: print_hi

## user · 2026-11-03T09:08:11Z

`print(f"{name:<10} {price:>8.2f} {quantity:>3}")`f是用><什么意思
[@4.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/work/3-261102/4.py)
[@4.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/work/3-261102/4.py)
<context ref="file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/work/3-261102/4.py">
{"description":"Byte offsets of selected text in filePath.\nUse these offsets to read selected text if it is required.\nstartOffset is inclusive, endOffset is exclusive.","offsetEncoding":"byte","selections":[{"startOffset":742,"endOffset":790}]}
</context>

## assistant · 2026-11-03T09:08:26Z

这行代码用来把商品信息**按列对齐输出**：

```python
print(f"{name:<10} {price:>8.2f} {quantity:>3}")
```

- 开头的 **`f`**：表示 f-string，可以把 `{}` 中的变量值放入字符串。
- **`<`**：左对齐。
- **`>`**：右对齐。
- **`:`**：后面开始写格式要求。

每一部分的含义：

| 写法 | 含义 |
|---|---|
| `{name:<10}` | `name` 左对齐，至少占 10 个字符位置，不足补空格 |
| `{price:>8.2f}` | `price` 右对齐，至少占 8 个字符位置，保留 2 位小数 |
| `{quantity:>3}` | `quantity` 右对齐，至少占 3 个字符位置 |

注意：**`.2f` 中的 `f`** 表示按定点小数格式显示，和开头的 `f` 作用不同。宽度不足时会补空格，内容超过指定宽度时会完整显示。

未修改文件，也未运行代码。

## user · 2026-11-03T09:09:16Z

帮我整理一份f-string的详细笔记
[@4.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/work/3-261102/4.py)
[@4.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/work/3-261102/4.py)
<context ref="file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/work/3-261102/4.py">
{"description":"Byte offsets of selected text in filePath.\nUse these offsets to read selected text if it is required.\nstartOffset is inclusive, endOffset is exclusive.","offsetEncoding":"byte","selections":[{"startOffset":742,"endOffset":790}]}
</context>

## assistant · 2026-11-03T09:09:19Z

我会结合 `4.py` 中的例子整理详细笔记，涵盖基本语法、对齐、数字格式和常见错误，并保存为 Markdown 文件。


## tool · 2026-11-03T09:09:23Z


Script completed
Wall time 0.1 seconds
Output:

{"i":0,"status":"fulfilled","value":{"chunk_id":"a9c0fb","wall_time_seconds":0.000005292,"exit_code":0,"original_token_count":76,"output":"/Users/oyamahappa/Documents/GitHub/labs/py-labs\nwork/3-261102/1.py\nwork/3-261102/5.py\nwork/3-261102/4.py\nwork/3-261102/7.py\nwork/3-261102/3.py\nwork/3-261102/2.py\nwork/3-261102/6.py\nwork/3-261102/8.py\ndocs/CHANGELOG.md\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\n"}}
{"i":1,"status":"fulfilled","value":{"chunk_id":"e24daa","wall_time_seconds":0.000159084,"exit_code":1,"original_token_count":21,"output":"cat: /Users/oyamahappa/.codex/skills/ponytail/SKILL.md: No such file or directory\n"}}
{"i":2,"status":"fulfilled","value":{"chunk_id":"377e96","wall_time_seconds":0.000158375,"exit_code":0,"original_token_count":798,"output":"---\nname: using-superpowers\ndescription: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions\n---\n\n<SUBAGENT-STOP>\nIf you were dispatched as a subagent to execute a specific task, ignore this skill.\n</SUBAGENT-STOP>\n\n<EXTREMELY-IMPORTANT>\nIf you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.\n\nIF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.\n\nThis is not negotiable. You cannot rationalize your way out of this.\n</EXTREMELY-IMPORTANT>\n\n## The Rule\n\n**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.\n\n**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.\n\nThen announce \"Using [skill] to [purpose]\" and follow the skill exactly. If it has a checklist, create a todo per item.\n\n## Skill Priority\n\nWhen multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.\n\n- \"Let's build X\" → superpowers:brainstorming first, then implementation skills.\n- \"Fix this bug\" → superpowers:systematic-debugging first, then domain skills.\n\n## Red Flags\n\nThese thoughts mean STOP—you're rationalizing:\n\n| Thought | Reality |\n|---------|---------|\n| \"This is just a simple question\" | Questions are tasks. Check for skills. |\n| \"I need more context first\" | Skill check comes BEFORE clarifying questions. |\n| \"Let me explore the codebase first\" | Skills tell you HOW to explore. Check first. |\n| \"I can check git/files quickly\" | Files lack conversation context. Check for skills. |\n| \"Let me gather information first\" | Skills tell you HOW to gather information. |\n| \"This doesn't need a formal skill\" | If a skill exists, use it. |\n| \"I remember this skill\" | Skills evolve. Read current version. |\n| \"This doesn't count as a task\" | Action = task. Check for skills. |\n| \"The skill is overkill\" | Simple things become complex. Use it. |\n| \"I'll just do this one thing first\" | Check BEFORE doing anything. |\n| \"This feels productive\" | Undisciplined action wastes time. Skills prevent this. |\n| \"I know what that means\" | Knowing the concept ≠ using the skill. Invoke it. |\n\n## Platform Adaptation\n\nIf your harness appears here, read its reference file for special instructions:\n\n- Claude Code: `references/claude-code-tools.md`\n- Codex: `references/codex-tools.md`\n- Pi: `references/pi-tools.md`\n- Antigravity: `references/antigravity-tools.md`\n- Hermes Agent: `references/hermes-tools.md`\n- Muse: `references/muse-tools.md`\n\n## User Instructions\n\nUser instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.\n"}}

## assistant · 2026-11-03T09:09:30Z

我会使用 Ponytail 技能控制改动范围，只新增笔记和必要记录，保留原练习代码；同时按 Superpowers 的技能使用规则检查适用流程。


## tool · 2026-11-03T09:09:33Z


Script completed
Wall time 0.2 seconds
Output:

{"i":0,"status":"fulfilled","value":{"chunk_id":"7a9b7a","wall_time_seconds":0.000004125,"exit_code":0,"original_token_count":841,"output":"# 格式化输出商品信息\n# 描述：给定商品名称、单价和数量，请使用 f-string 格式化输出一行信息。\n# 要求：名称左对齐占 10 个字符宽度，\n# 单价保留 2 位小数并占 8 个字符宽度（右对齐），\n# 数量占 3 个字符宽度（右对齐）。输出格式为：`名称      单价    数量`（各部分之间用一个空格分隔）。\n# 输入格式：第一行一个字符串（商品名称，不含空格）；第二行一个浮点数（单价）；第三行一个整数（数量）。\n# 输出格式：一行，格式化后的字符串。\n# 样例输入：\n# 苹果\n# 5.5\n# 3\n# 样例输出：\n# 苹果       5.50     3\nname = input()\nprice = float(input())\nquantity = int(input())\nprint(f\"{name:<10} {price:>8.2f} {quantity:>3}\")# 协作环境\n\n- 项目：Python 基础练习，当前任务为 `work/2-261026/7.py`。\n- 工具：文件编辑工具、Git、PyCharm Python 环境查询。\n- Python：项目 `.venv/bin/python`，版本 3.9.6，无需新增依赖。\n- 当前采用 Ponytail 最小修改原则，并使用 python-tools 查询解释器；无需新增依赖。\n# 当前任务\n\n- 将 `work/2-261026/7.py` 改为同一行读取三个整数及分隔符。\n- 使用 `input().split()` 拆分，使用 `map(int, ...)` 转换三个整数，保留原输出格式。\n- 实际运行题目示例、负数与零、多余空白场景，检查输出与退出码。\n# 当前进度\n\n## 7.py 同一行输入\n\n- [x] 检查目标脚本和引用，未发现调用方或关联测试。\n- [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n- [x] 使用 `split` 和 `map` 读取同一行数据。\n- [x] 使用项目解释器运行 4 组输入，输出断言通过，退出码为 0，标准错误为空；`git diff --check` 通过。\n- [x] 提交 `83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n\n## 历史任务：L1\n\n- [x] 阅读题目图片和空白 `character1/L1.py`。\n- [x] 确认项目 Python 版本为 3.9.6，本地日期为 2026-10-19。\n- [x] 完成五行输出和逐条注释；个人资料暂显示“待填写”。\n- [ ] 收到用户的姓名、班级、学号后替换三项文字。\n- [x] 实际运行脚本，五行输出、日期、解释器版本及逐条注释断言通过，标准错误为空。\n- [x] 更新开发记录，创建提交 `19fd4fc feat: complete L1 information card exercise`。\n- [ ] 推送到 `https://github.com/OyamaMeek/py-labs.git` 的 `main`：自动审批以缺少具体目的地授权为由拒绝，等待用户明确授权。\n\n已有其他文件的暂存和未暂存修改，均不纳入本任务提交。\n# 完成标准\n\n- 使用 PyCharm 查询到的项目解释器运行 `work/2-261026/7.py`。\n- 输入 `3 4 5 ,`，输出 `3,4,5`，退出码为 0。\n- 覆盖负数、零、多余空白与整数格式转换，检查输出和退出码。\n- 项目当前没有测试或静态检查配置；本次采用实际运行与输出断言验证，不新增测试框架。\n- 提交前检查差异，仅包含本任务文件。\n# 注意事项\n\n- `work/2-261026/7.py` 的三个整数和分隔符必须从同一行读取，按要求使用 `map` 和 `split`。\n\n- 个人资料必须由用户提供，不从用户名推断姓名、班级或学号。\n- 本练习要求手工记录 Python 版本，不添加自动获取环境的 `import`。\n"}}
{"i":1,"status":"fulfilled","value":{"chunk_id":"263052","wall_time_seconds":0.000006084,"exit_code":0,"original_token_count":590,"output":" M work/3-261102/1.py\n M work/3-261102/8.py\nmain\norigin\thttps://github.com/OyamaMeek/py-labs.git (fetch)\norigin\thttps://github.com/OyamaMeek/py-labs.git (push)\n4679057 add:字符串反转与回文判断\n422e145 add:提取用户名与域名\nccbd1dc add:统计单词出现次数\n## [2026-10-19 11:32] L1 个人信息卡与环境自检\n\n- **需求/问题描述**：\n  > 根据题目图片完成 `character1/L1.py`，输出个人信息及本机 Python 环境。\n\n- **实际实现的功能与改动**：\n  - 使用五条 `print` 输出姓名、班级、学号、当前日期和 Python 版本，每条语句前有中文注释。\n  - 姓名、班级、学号尚未提供，明确标为“待填写”；日期为 2026-10-19，项目解释器版本为 3.9.6。\n  - 测试前确认空文件输出 0 行，五行输出断言失败；实现后使用项目解释器实际运行，五行输出、日期、版本和逐条注释断言全部通过，退出码为 0，标准错误为空。\n  - `git diff --check` 通过；项目没有现成的测试或静态检查配置。\n\n- **涉及文件**：\n  - `character1/L1.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`19fd4fc feat: complete L1 information card exercise`。\n- **推送状态**：自动审批拒绝了向 `https://github.com/OyamaMeek/py-labs.git` 的 `main` 分支执行普通推送，理由是缺少对该具体目的地的明确授权；远端未更新。\n\n---\n\n## [2026-10-27 23:23] 7.py 同一行输入\n\n- **需求/问题描述**：\n  > 三个整数及分隔符从同一行输入，使用 map 和 split。\n\n- **实际实现的功能与改动**：\n  - 使用 `input().split()` 拆分四项，使用 `map(int, ...)` 转换三个整数，保留指定分隔符输出。\n  - 修改前题目示例触发 `ValueError`；修改后示例、负数与零、多余空白、整数格式转换共 4 组实际运行与输出断言通过，标准错误为空。\n  - `git diff --check` 通过；未新增依赖或测试框架。\n\n- **涉及文件**：\n  - `work/2-261026/7.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n\n---\n"}}
{"i":2,"status":"fulfilled","value":{"chunk_id":"deccee","wall_time_seconds":0.000006167,"exit_code":0,"original_token_count":4929,"output":"---\nname: ponytail\ndescription: >\n  Lazy senior dev mode: the smallest change that fully solves the task, and a\n  reply a busy human understands in one read. Use on any coding task (writing,\n  fixing, refactoring, reviewing, choosing dependencies) and when the user says\n  \"ponytail\", \"be lazy\", \"simplest solution\", \"yagni\", or complains about\n  over-engineering or bloat. Levels: lite, full (default), ultra.\nargument-hint: \"[lite|full|ultra|off]\"\nlicense: MIT\n---\n\n# Ponytail\n\nYou are a lazy senior developer. The best code is the code never written. You solve the whole problem with the least new code. End your reply with one or two lines: what you skipped or did not check, and any risk the user must know.\n\nActive for the whole session until the user says \"stop ponytail\" or \"normal mode\". Switch level: `/ponytail lite|full|ultra`.\n\n## Before you write\n\nRead the task and the code it touches. List every place your change must reach: callers, tests, fixtures, config, exports. Check what your change could break for users: data it would destroy or expose, callers that stop working. That is scope. Extra features are not.\n\n## The smallest complete change\n\nTake the first option that fully works:\n\n1. Does it need to exist? Skip features, options and flexibility nobody asked for, and name them in one line. A vague request (\"build me X\") gets the smallest version that does the core job.\n2. Already in this codebase (a helper, component, service, pattern)? Use it the way the surrounding code does.\n3. Standard library or a platform feature? Use it, unless the project has its own. A house component beats a native widget.\n4. An installed dependency? Use it. Never add a dependency for a few lines.\n5. Can it be one line a reader gets at a glance? One line.\n6. Otherwise: the minimum code that works.\n\n- Be lazy about the solution, never about the change itself: finish every part the task needs, including the callers, tests and fixtures your change breaks.\n- No abstraction, wrapper, type conversion, option, config, boilerplate or \"for later\" code nobody asked for. Keep values in the form the platform already gives you. Deletion beats addition. Keep the structure the codebase already has: its layers, interfaces and conventions.\n- The shortest working diff wins, once you know everything it must touch. A one-liner that needs decoding is not short.\n- Comment only the why the code cannot show, in one line.\n- Bug fix: before you edit, grep every caller of the function you touch, then fix the root cause once in the shared code.\n- Code you move or merge keeps its error handling and validation.\n- Between options of equal size, take the one that is correct on edge cases.\n- Lazy code without its check is unfinished: new non-trivial logic (a branch, a loop, a parser, money or security, or a whole new script or app) leaves one small test or an assert-based self-check. Trivial changes need none.\n- A shortcut with a known limit gets a code comment in this form: `shortcut: <the limit>, <when to upgrade>`.\n\nNever cut: validation at trust boundaries, error handling that prevents data loss, security, accessibility, the calibration real hardware needs, anything the user asked for.\n\n## Levels\n\n| Level | Behavior |\n|-------|----------|\n| **lite** | Build what was asked. Name the smaller option in one line and let the user pick. |\n| **full** | The rules above. Default. |\n| **ultra** | Also question the request: before building, push back on any part the need does not justify. |\n---\nname: python-tools\ndescription: PyCharm environment tools. MUST be consulted before running ANY Python toolchain command (python, python3, pip, pip3, uv, conda, pytest, ruff, mypy, python -m <module>, etc.) — call get_python_environment first to get the executable and package manager that match PyCharm's configured SDK for the file's module. Also covers configuring an interpreter when none is set up.\nallowed-tools: execute_tool\n---\n\n# PyCharm Environment Tools\n\n> **Mandatory pre-flight:** before running ANY Python command — `python`, `python3`, `pip`, `pip3`, `uv`, `conda`, `pytest`, `ruff`, `mypy`, `python -m <module>`, or anything else that resolves a Python interpreter — call `get_python_environment` on a file inside the target module. Use the returned `executablePath` instead of a bare `python` / `python3`, and the returned `packageManager` to choose the correct install command. Skipping this step silently picks the wrong interpreter (system Python instead of the project's venv, an older minor version, missing packages) and corrupts the project's environment.\n\n> **If `get_python_environment` returns a non-null `noInterpreterConfigured` field, get a proper interpreter before running the Python command.** Branch on the field's content:\n> - Ends with `call configure_python_interpreter with the same --filePath.` → call `configure_python_interpreter`, then re-call `get_python_environment`. Run the Python command using the env info returned by the second call.\n> - Says `PyCharm expects this project to use <tool>, but <tool> is not installed.` (e.g. `uv`, `poetry`, `hatch`) → do NOT call `configure_python_interpreter`. Ask the user to install the named tool first, then re-call `get_python_environment`.\n> - Plain `No Python interpreter configured for: <path>.` (no extra suffix) → PyCharm has no automatic option, but the project also doesn't dictate a specific tool. Set up the env yourself with a sensible default (e.g. `python3 -m venv .venv` in the project root), then re-call `get_python_environment`. The new venv should be detected and the next response will suggest `configure_python_interpreter`; if it still returns plain \"no interpreter\" for some reason, use `.venv/bin/python` directly. Tell the user what you set up.\n>\n> For commands that aren't tied to a specific file (e.g. `pip install`, `pytest` at the project root, or a run configuration that doesn't expose a target file), pass any `.py` file inside the target module as `--filePath` — the interpreter is per-module, not per-file.\n\nTwo tools, used together:\n\n1. **`get_python_environment`** — always call this first. Read-only: it reports the Python interpreter PyCharm has configured for a file (version, environment type, executable path, package manager) and never modifies project state.\n2. **`configure_python_interpreter`** — call this *only* when `get_python_environment` returns a `noInterpreterConfigured` field whose value ends with `call configure_python_interpreter with the same --filePath.` That means PyCharm can do the configuration without installing anything new — it will attach an existing virtual environment on disk, inherit the parent module's interpreter, or create a fresh env using a tool that's already installed (uv / poetry / hatch / venv). Do not call it in any other situation.\n\nPrefer these tools over guessing interpreter paths or package managers — the results match what PyCharm itself uses.\n\n## `get_python_environment`\n\nReturns the Python environment configured for the given file.\n\n### Syntax\n\n```\nexecute_tool(command=\"get_python_environment --filePath <value>\")\n```\n\n### Parameters\n\n| Parameter | Type | Required | Description |\n|-----------|------|----------|-------------|\n| `--filePath` | `string` | Yes | Absolute or project-relative path to any Python file (e.g. `/Users/dev/myproject/src/main.py` or `src/main.py`). Used to identify which interpreter and environment PyCharm has configured for that file. |\n\n**String parameters:** Quote values containing spaces: `--filePath '/Users/dev/my project/main.py'`\n\n### Output fields\n\nResponse is a JSON object with these fields:\n\n| Field | Description |\n|-------|-------------|\n| `pythonVersion` | Interpreter version string, e.g. `Python 3.11.4` |\n| `environmentType` | `venv`, `conda`, `system`, or `unknown` |\n| `executablePath` | Absolute path to the Python binary to invoke |\n| `environmentPath` | Root of the virtual environment (venv prefix or conda prefix); `null` for system Python |\n| `packageManager` | `pip`, `uv`, `poetry`, `hatch`, `conda`, or `unknown` — use this to pick the right install command |\n| `noInterpreterConfigured` | When non-null, no interpreter is set up. Contains the next-step hint (see Pitfalls). Other fields will be `null`. |\n\nExample response:\n\n```json\n{\n  \"pythonVersion\": \"Python 3.11.4\",\n  \"environmentType\": \"venv\",\n  \"executablePath\": \"/Users/dev/myproject/.venv/bin/python\",\n  \"environmentPath\": \"/Users/dev/myproject/.venv\",\n  \"packageManager\": \"uv\"\n}\n```\n\n### Examples\n\n#### 1. Absolute path\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath /Users/dev/myproject/src/main.py\"}}\n```\n\n#### 2. Project-relative path\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath src/main.py\"}}\n```\n\n#### 3. Path with spaces\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath '/Users/dev/my project/src/main.py'\"}}\n```\n\n### Pitfalls\n\n- Quote the path if it contains spaces.\n- The file must exist on disk; passing a non-existent path returns an error.\n- If `noInterpreterConfigured` is non-null and ends with `call configure_python_interpreter with the same --filePath.` (e.g. \"PyCharm can attach the existing virtual environment…\", \"PyCharm can create a new uv environment…\", \"PyCharm can inherit the interpreter from parent module 'X'…\"), follow that — PyCharm has tooling ready and the configure tool will set it up without installing anything.\n- If `noInterpreterConfigured` says `PyCharm expects this project to use <tool>, but <tool> is not installed.`, the project's `pyproject.toml` / lockfile points at a tool the system doesn't have. Do not call `configure_python_interpreter`. Ask the user before installing the named tool via the terminal, then re-call `get_python_environment`.\n- If `noInterpreterConfigured` is the plain `No Python interpreter configured for: <path>.` with no extra content, do not call `configure_python_interpreter`. The project doesn't pin a specific tool, so set up a default venv yourself (e.g. `python3 -m venv .venv`) and re-call `get_python_environment` — the next call should detect it and suggest `configure_python_interpreter`. Never just run the user's command with bare `python` / `python3`.\n\n## `configure_python_interpreter`\n\nAsks PyCharm to attach a Python interpreter for the module the given file belongs to. PyCharm picks the right action: attach an existing virtual environment on disk, inherit the interpreter from a parent module, or create a fresh env using already-installed tooling (uv venv, poetry env, hatch env, or plain `venv`). Only call this when `get_python_environment` explicitly suggested it (the `noInterpreterConfigured` field ended with `call configure_python_interpreter with the same --filePath.`). Do not call it as a generic interpreter switcher and do not call it when `noInterpreterConfigured` is the plain \"no interpreter\" message without a configuration suggestion.\n\n### Syntax\n\n```\nexecute_tool(command=\"configure_python_interpreter --filePath <value>\")\n```\n\n### Parameters\n\n| Parameter | Type | Required | Description |\n|-----------|------|----------|-------------|\n| `--filePath` | `string` | Yes | Absolute or project-relative path to a Python file inside the module whose interpreter should be configured. |\n\n### Output\n\nOn success, returns the same JSON shape as `get_python_environment`, describing the interpreter PyCharm just configured.\n\n### Examples\n\n#### Configure after `get_python_environment` reported that PyCharm can set one up\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"configure_python_interpreter --filePath src/main.py\"}}\n```\n\n### Pitfalls\n\n- Local interpreters only. Remote / WSL / Docker interpreters are not supported by this tool.\n- Only call this tool when `get_python_environment` told you to. Calling it after the plain `No Python interpreter configured for: <path>` (with no `call configure_python_interpreter` suggestion) will fail — PyCharm has no automatic option there and there is nothing this tool can do.\n\n## Rules\n\n1. **You MUST call `get_python_environment` before every Python toolchain invocation** — `python`, `python3`, `pip`, `pip3`, `uv`, `conda`, `pytest`, `ruff`, `mypy`, `python -m <module>`, and any other command that resolves a Python interpreter. The check is cheap (a single MCP call) and there is no exemption for \"obvious\" cases — running a fresh `python script.py` in a project with a configured venv is exactly the case where the wrong interpreter ruins things silently. Re-check after every `configure_python_interpreter` call, after the user reconfigures the SDK in PyCharm, and whenever you switch to a file from a different module.\n2. **If `get_python_environment` returns a non-null `noInterpreterConfigured` field, get a proper interpreter before running the Python command — never fall back to bare `python` / `python3`.** Branch on the field's content:\n   - Suffix `call configure_python_interpreter with the same --filePath.` → call `configure_python_interpreter`, re-call `get_python_environment`, then proceed.\n   - `PyCharm expects this project to use <tool>, but <tool> is not installed.` → do NOT call `configure_python_interpreter`. Ask the user before installing the named tool via the terminal, then re-call `get_python_environment`.\n   - Plain `No Python interpreter configured for: <path>.` → the project pins no specific tool. Set up a default venv yourself (`python3 -m venv .venv` in the project root) and re-call `get_python_environment`; the new venv will normally surface a `configure_python_interpreter` suggestion on the next call. Tell the user what you set up.\n3. **If any other tool reports a missing Python interpreter, route through this skill before asking the user.** When `get_run_configurations`, `execute_run_configuration`, `build_project`, the terminal, or any other PyCharm tool returns a \"no interpreter configured\" message, call `get_python_environment` on a file in the target module — do NOT instruct the user to set the interpreter via Settings → Project → Python Interpreter without first checking what `get_python_environment` reports.\n4. Use the returned `executablePath` verbatim — never substitute `python` / `python3` / `which python` output.\n5. Use the returned `packageManager` to pick the install command — `pip install <pkg>` for `pip`, `uv add <pkg>` for `uv`, `poetry add <pkg>` for `poetry`, `hatch run pip install <pkg>` for `hatch`, `conda install <pkg>` for `conda`. If `packageManager` is `unknown`, ask the user how to install packages for this interpreter before running anything.\n6. Call `configure_python_interpreter` only when `get_python_environment` explicitly suggested it (the `noInterpreterConfigured` field ended with `call configure_python_interpreter with the same --filePath.`). `get_python_environment` itself never modifies project state.\n## Subagent dispatch requires multi-agent support\n\nAdd to your Codex config (`~/.codex/config.toml`):\n\n```toml\n[features]\nmulti_agent = true\n```\n\nThis enables the multi-agent tools that skills like\n`dispatching-parallel-agents` and `subagent-driven-development` use.\nWhich tools you get depends on the multi-agent version your model\npreset selects (current presets run V2; older ones run V1). Trust your\nactual tool list over any table — including this one — when they\ndisagree.\n\n- **Spawning:** give children a clean context with\n  `spawn_agent {fork_turns: \"none\"}`; the default `\"all\"` copies your\n  entire transcript into the child. On Codex 0.145+, role files under\n  `~/.codex/agents/` attach to isolated forks via `agent_type`.\n  Full-history forks accept `model` and `reasoning_effort` overrides\n  (only `agent_type` is refused there) — isolated forks are the SDD\n  default for context hygiene, not because overrides require them.\n- **Fix rounds:** resume the implementer with `followup_task` — it\n  delivers your message, triggers a turn, and transparently reloads a\n  child the harness evicted. Never dispatch a fresh implementer on the\n  theory that a spawned agent cannot be messaged again; on V2 it\n  always can.\n- **Lifecycle:** V2 has no `close_agent`. Finished children are\n  evicted automatically when slots are needed; leaving them unclosed\n  costs nothing. Only V1 sessions have `close_agent` — there, close\n  reviewers when their review returns, and close each implementer\n  after its task's review passes.\n- **Model names:** never copy a model name from a skill, table, or old\n  session into `spawn_agent` without checking it against your current\n  spawn allowlist — V2 accepts only V2-capable presets and hard-errors\n  on the rest.\n\n## Waiting on children\n\n`wait_agent` is an event subscription, not a poll: a long wait wakes\nthe moment a child produces mailbox activity, with the same latency as\na short one. Short-timeout polling buys nothing and costs a tool call —\nand a context rebill — per poll. In measured sessions, roughly\ntwo-thirds of all wait calls were short polls that timed out.\n\n- While you still have local work, do not wait at all. A completed\n  child's final answer is pushed into your mailbox and arrives with\n  your next turn.\n- When you are genuinely idle with children outstanding, wait in\n  bounded stretches: `wait_agent` with `timeout_ms` 300000-600000\n  (5-10 minutes). After each stretch — wake or timeout — post one\n  status line, run `list_agents`, and chase any child that finished\n  without reporting. Never stack polls shorter than five minutes; the\n  event subscription wakes a bounded stretch just as fast as a short\n  one.\n- Completion mail cannot wake an idle controller (it is delivered\n  without triggering a turn); covering that idle window is\n  `wait_agent`'s only job. A stretch that times out with no activity\n  is your cue to reconcile, not to shorten the next stretch.\n\n## Model routing on spawns\n\nEvery `spawn_agent` you issue — including when you are yourself a\nspawned child running a fan-out — sets `model` AND `reasoning_effort`\nexplicitly, per the Model Selection rules of the skill you are\nexecuting. Setting `model` alone is a trap: the child's effort\nsilently resets to that model's default, not to yours.\n\nAsk your human partner to add a machine-level backstop to\n`~/.codex/config.toml` so any spawn that slips through still routes to\na deliberate tier instead of silently inheriting the session's most\nexpensive model:\n\n```toml\n[agents]\ndefault_subagent_model = \"<a mid-tier model from your spawn allowlist>\"\ndefault_subagent_reasoning_effort = \"medium\"\n```\n\n## Environment Detection\n\nSkills that create worktrees or finish branches should detect their\nenvironment with read-only git commands before proceeding:\n\n```bash\nGIT_DIR=$(cd \"$(git rev-parse --git-dir)\" 2>/dev/null && pwd -P)\nGIT_COMMON=$(cd \"$(git rev-parse --git-common-dir)\" 2>/dev/null && pwd -P)\nBRANCH=$(git branch --show-current)\n```\n\n- `GIT_DIR != GIT_COMMON` → already in a linked worktree (skip creation)\n- `BRANCH` empty → detached HEAD (cannot branch/push/PR from sandbox)\n\nSee `using-git-worktrees` Step 0 and `finishing-a-development-branch`\nStep 1 for how each skill uses these signals.\n\n## Codex App Finishing\n\nWhen the sandbox blocks branch/push operations (detached HEAD in an\nexternally managed worktree), the agent commits all work and informs\nthe user to use the App's native controls:\n\n- **\"Create branch\"** — names the branch, then commit/push/PR via App UI\n- **\"Hand off to local\"** — transfers work to the user's local checkout\n\nThe agent can still run tests, stage files, and output suggested branch\nnames, commit messages, and PR descriptions for the user to copy.\n"}}
{"i":3,"status":"fulfilled","value":{"chunk_id":"a72b71","wall_time_seconds":0.000007833,"exit_code":0,"original_token_count":0,"output":""}}

## tool · 2026-11-03T09:09:42Z


Script completed
Wall time 2.9 seconds
Output:

[{"name":"mcp__pycharm__execute_tool","description":"Universal tool executor that can invoke specific IDE MCP tool dynamically.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__pycharm__execute_tool(args: {\n  // Command-line string with tool name and arguments\n  command: string;\n}): Promise<CallToolResult>; };\n```"}]
7. Input and Output — Python 3.9.25 documentation (https://docs.python.org/3.9/tutorial/inputoutput.html)
citeturn0view0 [wordlim: 200] Crawled: today; Content type: text/html; Source: open({"ref_id":"https://docs.python.org/3.9/tutorial/inputoutput.html","lineno":null}); Total lines: 302
L0: [Input]
L1: 
L2: This document is for an old version of Python that is no longer supported. You should upgrade, and read the 【0†Python documentation for the current stable release】.
L3: 
L4: # 7. Input and Output【1†¶】
L5: 
L6: There are several ways to present the output of a program; data can be printed in a human-readable form, or written to a file for future use. This chapter will discuss some of the possibilities.
L7: ## 7.1. Fancier Output Formatting【2†¶】
L8: 
L9: So far we’ve encountered two ways of writing values: expression statements and the 【3†`print()`】 function. (A third way is using the `write()` method of file objects; the standard output file can be referenced as `sys.stdout`. See the Library Reference for more information on this.)
L10: 
L11: Often you’ll want more control over the formatting of your output than simply printing space-separated values. There are several ways to format output.
L12:   * To use 【4†formatted string literals】, begin a string with `f` or `F` before the opening quotation mark or triple quotation mark. Inside this string, you can write a Python expression between `{` and `}` characters that can refer to variables or literal values.
L13: 
L14:     >>> year = 2016
L15:     >>> event = 'Referendum'
L16:     >>> f'Results of the {year} {event}'
L17:     'Results of the 2016 Referendum'
L18:   * The 【5†`str.format()`】 method of strings requires more manual effort. You’ll still use `{` and `}` to mark where a variable will be substituted and can provide detailed formatting directives, but you’ll also need to provide the information to be formatted.
L19: 
L20:     >>> yes_votes = 42_572_654
L21:     >>> no_votes = 43_132_495
L22:     >>> percentage = yes_votes / (yes_votes + no_votes)
L23:     >>> '{:-9} YES votes  {:2.2%}'.format(yes_votes, percentage)
L24:     ' 42572654 YES votes  49.67%'
L25:   * Finally, you can do all the string handling yourself by using string slicing and concatenation operations to create any layout you can imagine. The string type has some methods that perform useful operations for padding strings to a given column width.
L26: 
L27: When you don’t need fancy output but just want a quick display of some variables for debugging purposes, you can convert any value to a string with the 【6†`repr()`】 or 【7†`str()`】 functions.
L28: The 【7†`str()`】 function is meant to return representations of values which are fairly human-readable, while 【6†`repr()`】 is meant to generate representations which can be read by the interpreter (or will force a 【8†`SyntaxError`】 if there is no equivalent syntax). For objects which don’t have a particular representation for human consumption, 【7†`str()`】 will return the same value as 【6†`repr()`】.
L29: Many values, such as numbers or structures like lists and dictionaries, have the same representation using either function. Strings, in particular, have two distinct representations.
L30: Some examples:
L31: 
L32:     >>> s = 'Hello, world.'
L33:     >>> str(s)
L34:     'Hello, world.'
L35:     >>> repr(s)
L36:     "'Hello, world.'"
L37:     >>> str(1/7)
L38:     '0.14285714285714285'
L39:     >>> x = 10 * 3.25
L40:     >>> y = 200 * 200
L41:     >>> s = 'The value of x is ' + repr(x) + ', and y is ' + repr(y) + '...'
L42:     >>> print(s)
L43:     The value of x is 32.5, and y is 40000...
L44:     >>> # The repr() of a string adds string quotes and backslashes:
L45:     ... hello = 'hello, world\n'
L46:     >>> hellos = repr(hello)
L47:     >>> print(hellos)
L48:     'hello, world\n'
L49:     >>> # The argument to repr() may be any Python object:
L50:     ... repr((x, y, ('spam', 'eggs')))
L51:     "(32.5, 40000, ('spam', 'eggs'))"
L52: The 【9†`string`】 module contains a 【10†`Template`】 class that offers yet another way to substitute values into strings, using placeholders like `$x` and replacing them with values from a dictionary, but offers much less control of the formatting.
L53: ### 7.1.1. Formatted String Literals【11†¶】
L54: 
L55: 【12†Formatted string literals】 (also called f-strings for short) let you include the value of Python expressions inside a string by prefixing the string with `f` or `F` and writing expressions as `{expression}`.
L56: An optional format specifier can follow the expression. This allows greater control over how the value is formatted. The following example rounds pi to three places after the decimal:
L57: 
L58:     >>> import math
L59:     >>> print(f'The value of pi is approximately {math.pi:.3f}.')
L60:     The value of pi is approximately 3.142.
L61: Passing an integer after the `':'` will cause that field to be a minimum number of characters wide. This is useful for making columns line up.
L62: 
L63:     >>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
L64:     >>> for name, phone in table.items():
L65:     ...     print(f'{name:10} ==> {phone:10d}')
L66:     ...
L67:     Sjoerd     ==>       4127
L68:     Jack       ==>       4098
L69:     Dcab       ==>       7678
L70: Other modifiers can be used to convert the value before it is formatted. `'!a'` applies 【13†`ascii()`】, `'!s'` applies 【7†`str()`】, and `'!r'` applies 【6†`repr()`】:
L71: 
L72:     >>> animals = 'eels'
L73:     >>> print(f'My hovercraft is full of {animals}.')
L74:     My hovercraft is full of eels.
L75:     >>> print(f'My hovercraft is full of {animals!r}.')
L76:     My hovercraft is full of 'eels'.
L77: 
L78: 
L79: For a reference on these format specifications, see the reference guide for the 【14†Format Specification Mini-Language】.
L80: ### 7.1.2. The String format() Method【15†¶】
L81: 
L82: Basic usage of the 【5†`str.format()`】 method looks like this:
L83: 
L84:     >>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
L85:     We are the knights who say "Ni!"
L86: The brackets and characters within them (called format fields) are replaced with the objects passed into the 【5†`str.format()`】 method. A number in the brackets can be used to refer to the position of the object passed into the 【5†`str.format()`】 method.
L87: 
L88:     >>> print('{0} and {1}'.format('spam', 'eggs'))
L89:     spam and eggs
L90:     >>> print('{1} and {0}'.format('spam', 'eggs'))
L91:     eggs and spam
L92: If keyword arguments are used in the 【5†`str.format()`】 method, their values are referred to by using the name of the argument.
L93: 
L94:     >>> print('This {food} is {adjective}.'.format(
L95:     ...       food='spam', adjective='absolutely horrible'))
L96:     This spam is absolutely horrible.
L97: Positional and keyword arguments can be arbitrarily combined:
L98: 
L99:     >>> print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
L100:                                                            other='Georg'))
L101:     The story of Bill, Manfred, and Georg.
L102: If you have a really long format string that you don’t want to split up, it would be nice if you could reference the variables to be formatted by name instead of by position. This can be done by simply passing the dict and using square brackets `'[]'` to access the keys.
L103: 
L104:     >>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
L105:     >>> print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
L106:     ...       'Dcab: {0[Dcab]:d}'.format(table))
L107:     Jack: 4098; Sjoerd: 4127; Dcab: 8637678
L108: This could also be done by passing the table as keyword arguments with the ‘**’ notation.
L109: 
L110:     >>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
L111:     >>> print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
L112:     Jack: 4098; Sjoerd: 4127; Dcab: 8637678
L113: 
L114: 
L115: This is particularly useful in combination with the built-in function 【16†`vars()`】, which returns a dictionary containing all local variables.
L116: As an example, the following lines produce a tidily-aligned set of columns giving integers and their squares and cubes:
L117: 
L118:     >>> for x in range(1, 11):
L119:     ...     print('{0:2d} {1:3d} {2:4d}'.format(x, x*x, x*x*x))
L120:     ...
L121:      1   1    1
L122:      2   4    8
L123:      3   9   27
L124:      4  16   64
L125:      5  25  125
L126:      6  36  216
L127:      7  49  343
L128:      8  64  512
L129:      9  81  729
L130:     10 100 1000
L131: 
L132: 
L133: For a complete overview of string formatting with 【5†`str.format()`】, see 【17†Format String Syntax】.
L134: ### 7.1.3. Manual String Formatting【18†¶】
L135: 
L136: Here’s the same table of squares and cubes, formatted manually:
L137: 
L138:     >>> for x in range(1, 11):
L139:     ...     print(repr(x).rjust(2), repr(x*x).rjust(3), end=' ')
L140:     ...     # Note use of 'end' on previous line
L141:     ...     print(repr(x*x*x).rjust(4))
L142:     ...
L143:      1   1    1
L144:      2   4    8
L145:      3   9   27
L146:      4  16   64
L147:      5  25  125
L148:      6  36  216
L149:      7  49  343
L150:      8  64  512
L151:      9  81  729
L152:     10 100 1000
L153: (Note that the one space between each column was added by the way 【3†`print()`】 works: it always adds spaces between its arguments.)
L154: The 【19†`str.rjust()`】 method of string objects right-justifies a string in a field of a given width by padding it with spaces on the left. There are similar methods 【20†`str.ljust()`】 and 【21†`str.center()`】. These methods do not write anything, they just return a new string. If the input string is too long, they don’t truncate it, but return it unchanged; this will mess up your column lay-out but that’s usually better than the alternative, which would be lying about a value.
--------------------------------------------------------------------------------
string — Common string operations — Python 3.9.25 documentation (https://docs.python.org/3.9/library/string.html)
citeturn0view1 [wordlim: 200] Crawled: today; Content type: text/html; Source: open({"ref_id":"https://docs.python.org/3.9/library/string.html#format-specification-mini-language","lineno":null}); Total lines: 443
L0: [Input]
L1: 
L2: This document is for an old version of Python that is no longer supported. You should upgrade, and read the 【0†Python documentation for the current stable release】.
L3: 
L4: # 【1†`string`】 — Common string operations【1†¶】
L5: 
L6: Source code: 【2†Lib/string.py†github.com】
L7: 
L8: * * *
L9: 
L10: See also
L11: 
L12: 【3†Text Sequence Type — str】
L13: 
L14: 【4†String Methods】
L15: ## String constants【5†¶】
L16: 
L17: The constants defined in this module are:
L18: 
L19: `string.``ascii_letters`【6†¶】
L20: 
L21: 
L22: The concatenation of the 【7†`ascii_lowercase`】 and 【8†`ascii_uppercase`】 constants described below. This value is not locale-dependent.
L23: 
L24: `string.``ascii_lowercase`【7†¶】
L25: 
L26: 
L27: The lowercase letters `'abcdefghijklmnopqrstuvwxyz'`. This value is not locale-dependent and will not change.
L28: 
L29: `string.``ascii_uppercase`【8†¶】
L30: The uppercase letters `'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`. This value is not locale-dependent and will not change.
L31: 
L32: `string.``digits`【9†¶】
L33: 
L34: 
L35: The string `'0123456789'`.
L36: 
L37: `string.``hexdigits`【10†¶】
L38: 
L39: 
L40: The string `'0123456789abcdefABCDEF'`.
L41: 
L42: `string.``octdigits`【11†¶】
L43: 
L44: 
L45: The string `'01234567'`.
L46: 
L47: `string.``punctuation`【12†¶】
L48: 
L49: 
L50: String of ASCII characters which are considered punctuation characters in the `C` locale: `!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~`.
L51: 
L52: `string.``printable`【13†¶】
L53: String of ASCII characters which are considered printable. This is a combination of 【9†`digits`】, 【6†`ascii_letters`】, 【12†`punctuation`】, and 【14†`whitespace`】.
L54: 
L55: `string.``whitespace`【14†¶】
L56: 
L57: 
L58: A string containing all ASCII characters that are considered whitespace. This includes the characters space, tab, linefeed, return, formfeed, and vertical tab.
L59: ## Custom String Formatting【15†¶】
L60: 
L61: The built-in string class provides the ability to do complex variable substitutions and value formatting via the 【16†`format()`】 method described in 【17†PEP 3101†www.python.org】. The 【18†`Formatter`】 class in the 【1†`string`】 module allows you to create and customize your own string formatting behaviors using the same implementation as the built-in 【16†`format()`】 method.
L62: 
L63: class `string.``Formatter`【18†¶】
L64: 
L65: 
L66: The 【18†`Formatter`】 class has the following public methods:
L67: `format`(format_string, /, *args, **kwargs)【19†¶】
L68: 
L69: 
L70: The primary API method. It takes a format string and an arbitrary set of positional and keyword arguments. It is just a wrapper that calls 【20†`vformat()`】.
L71: 
L72: Changed in version 3.7: A format string argument is now 【21†positional-only】.
L73: 
L74: `vformat`(format_string, args, kwargs)【20†¶】
L75: This function does the actual work of formatting. It is exposed as a separate function for cases where you want to pass in a predefined dictionary of arguments, rather than unpacking and repacking the dictionary as individual arguments using the `*args` and `**kwargs` syntax. 【20†`vformat()`】 does the work of breaking up the format string into character data and replacement fields. It calls the various methods described below.
L76: In addition, the 【18†`Formatter`】 defines a number of methods that are intended to be replaced by subclasses:
L77: 
L78: `parse`(format_string)【22†¶】
L79: 
L80: 
L81: Loop over the format_string and return an iterable of tuples (literal_text, field_name, format_spec, conversion). This is used by 【20†`vformat()`】 to break the string into either literal text, or replacement fields.
L82: The values in the tuple conceptually represent a span of literal text followed by a single replacement field. If there is no literal text (which can happen if two replacement fields occur consecutively), then literal_text will be a zero-length string. If there is no replacement field, then the values of field_name, format_spec and conversion will be `None`.
L83: 
L84: `get_field`(field_name, args, kwargs)【23†¶】
L85: Given field_name as returned by 【22†`parse()`】 (see above), convert it to an object to be formatted. Returns a tuple (obj, used_key). The default version takes strings of the form defined in 【17†PEP 3101†www.python.org】, such as “0[name]” or “label.title”. args and kwargs are as passed in to 【20†`vformat()`】. The return value used_key has the same meaning as the key parameter to 【24†`get_value()`】.
L86: 
L87: `get_value`(key, args, kwargs)【24†¶】
L88: Retrieve a given field value. The key argument will be either an integer or a string. If it is an integer, it represents the index of the positional argument in args; if it is a string, then it represents a named argument in kwargs.
L89: 
L90: The args parameter is set to the list of positional arguments to 【20†`vformat()`】, and the kwargs parameter is set to the dictionary of keyword arguments.
L91: For compound field names, these functions are only called for the first component of the field name; subsequent components are handled through normal attribute and indexing operations.
L92: 
L93: So for example, the field expression ‘0.name’ would cause 【24†`get_value()`】 to be called with a key argument of 0. The `name` attribute will be looked up after 【24†`get_value()`】 returns by calling the built-in 【25†`getattr()`】 function.
L94: If the index or keyword refers to an item that does not exist, then an 【26†`IndexError`】 or 【27†`KeyError`】 should be raised.
L95: 
L96: `check_unused_args`(used_args, args, kwargs)【28†¶】
L97: Implement checking for unused arguments if desired. The arguments to this function is the set of all argument keys that were actually referred to in the format string (integers for positional arguments, and strings for named arguments), and a reference to the args and kwargs that was passed to vformat. The set of unused args can be calculated from these parameters. 【28†`check_unused_args()`】 is assumed to raise an exception if the check fails.
L98: 
L99: `format_field`(value, format_spec)【29†¶】
L100: 【29†`format_field()`】 simply calls the global 【30†`format()`】 built-in. The method is provided so that subclasses can override it.
L101: 
L102: `convert_field`(value, conversion)【31†¶】
L103: 
L104: 
L105: Converts the value (returned by 【23†`get_field()`】) given a conversion type (as in the tuple returned by the 【22†`parse()`】 method). The default version understands ‘s’ (str), ‘r’ (repr) and ‘a’ (ascii) conversion types.
L106: ## Format String Syntax【32†¶】
L107: 
L108: The 【16†`str.format()`】 method and the 【18†`Formatter`】 class share the same syntax for format strings (although in the case of 【18†`Formatter`】, subclasses can define their own format string syntax). The syntax is related to that of 【33†formatted string literals】, but it is less sophisticated and, in particular, does not support arbitrary expressions.
L109: Format strings contain “replacement fields” surrounded by curly braces `{}`. Anything that is not contained in braces is considered literal text, which is copied unchanged to the output. If you need to include a brace character in the literal text, it can be escaped by doubling: `{{` and `}}`.
L110: 
L111: The grammar for a replacement field is as follows:
L112: > replacement_field ::=  "{" [【34†`field_name`】] ["!" 【35†`conversion`】] [":" 【36†`format_spec`】] "}"
L113: >     field_name        ::=  arg_name ("." 【37†`attribute_name`】 | "[" 【38†`element_index`】 "]")*
L114: >     arg_name          ::=  [【39†`identifier`】 | 【40†`digit`】+]
L115: >     attribute_name    ::=  【39†`identifier`】
L116: >     element_index     ::=  【40†`digit`】+ | 【41†`index_string`】
L117: >     index_string      ::=  <any source character except "]"> +
L118: >     conversion        ::=  "r" | "s" | "a"
L119: >     format_spec       ::=  <described in the next section>
L120: >
L121: In less formal terms, the replacement field can start with a field_name that specifies the object whose value is to be formatted and inserted into the output instead of the replacement field. The field_name is optionally followed by a conversion field, which is preceded by an exclamation point `'!'`, and a format_spec, which is preceded by a colon `':'`. These specify a non-default format for the replacement value.
L122: 
L123: See also the 【42†Format Specification Mini-Language】 section.
L124: The field_name itself begins with an arg_name that is either a number or a keyword. If it’s a number, it refers to a positional argument, and if it’s a keyword, it refers to a named keyword argument. If the numerical arg_names in a format string are 0, 1, 2, … in sequence, they can all be omitted (not just some) and the numbers 0, 1, 2, … will be automatically inserted in that order.
L125: Because arg_name is not quote-delimited, it is not possible to specify arbitrary dictionary keys (e.g., the strings `'10'` or `':-]'`) within a format string. The arg_name can be followed by any number of index or attribute expressions. An expression of the form `'.name'` selects the named attribute using 【25†`getattr()`】, while an expression of the form `'[index]'` does an index lookup using 【43†`__getitem__()`】.
L126: Changed in version 3.1: The positional argument specifiers can be omitted for 【16†`str.format()`】, so `'{} {}'.format(a, b)` is equivalent to `'{0} {1}'.format(a, b)`.
L127: 
L128: Changed in version 3.4: The positional argument specifiers can be omitted for 【18†`Formatter`】.
--------------------------------------------------------------------------------
2. Lexical analysis — Python 3.9.25 documentation (https://docs.python.org/3.9/reference/lexical_analysis.html)
citeturn0view2 [wordlim: 200] Crawled: today; Content type: text/html; Source: open({"ref_id":"https://docs.python.org/3.9/reference/lexical_analysis.html#f-strings","lineno":null}); Total lines: 426
L0: [Input]
L1: 
L2: This document is for an old version of Python that is no longer supported. You should upgrade, and read the 【0†Python documentation for the current stable release】.
L3: # 2. Lexical analysis【1†¶】
L4: 
L5: A Python program is read by a parser. Input to the parser is a stream of tokens, generated by the lexical analyzer. This chapter describes how the lexical analyzer breaks a file into tokens.
L6: 
L7: Python reads program text as Unicode code points; the encoding of a source file can be given by an encoding declaration and defaults to UTF-8, see 【2†PEP 3120†www.python.org】 for details. If the source file cannot be decoded, a 【3†`SyntaxError`】 is raised.
L8: ## 2.1. Line structure【4†¶】
L9: 
L10: A Python program is divided into a number of logical lines.
L11: 
L12: ### 2.1.1. Logical lines【5†¶】
L13: 
L14: The end of a logical line is represented by the token NEWLINE. Statements cannot cross logical line boundaries except where NEWLINE is allowed by the syntax (e.g., between statements in compound statements). A logical line is constructed from one or more physical lines by following the explicit or implicit line joining rules.
L15: ### 2.1.2. Physical lines【6†¶】
L16: A physical line is a sequence of characters terminated by an end-of-line sequence. In source files and strings, any of the standard platform line termination sequences can be used - the Unix form using ASCII LF (linefeed), the Windows form using the ASCII sequence CR LF (return followed by linefeed), or the old Macintosh form using the ASCII CR (return) character. All of these forms can be used equally, regardless of platform.
L17: The end of input also serves as an implicit terminator for the final physical line.
L18: When embedding Python, source code strings should be passed to Python APIs using the standard C conventions for newline characters (the `\n` character, representing ASCII LF, is the line terminator).
L19: ### 2.1.3. Comments【7†¶】
L20: 
L21: A comment starts with a hash character (`#`) that is not part of a string literal, and ends at the end of the physical line. A comment signifies the end of the logical line unless the implicit line joining rules are invoked. Comments are ignored by the syntax.
L22: ### 2.1.4. Encoding declarations【8†¶】
L23: If a comment in the first or second line of the Python script matches the regular expression `coding[=:]\s*([-\w.]+)`, this comment is processed as an encoding declaration; the first group of this expression names the encoding of the source code file. The encoding declaration must appear on a line of its own. If it is the second line, the first line must also be a comment-only line. The recommended forms of an encoding expression are
L24: 
L25:     # -*- coding: <encoding-name> -*-
L26: which is recognized also by GNU Emacs, and
L27: 
L28:     # vim:fileencoding=<encoding-name>
L29: 
L30: 
L31: which is recognized by Bram Moolenaar’s VIM.
L32: 
L33: If no encoding declaration is found, the default encoding is UTF-8. In addition, if the first bytes of the file are the UTF-8 byte-order mark (`b'\xef\xbb\xbf'`), the declared file encoding is UTF-8 (this is supported, among others, by Microsoft’s notepad).
L34: If an encoding is declared, the encoding name must be recognized by Python (see 【9†Standard Encodings】). The encoding is used for all lexical analysis, including string literals, comments and identifiers.
L35: ### 2.1.5. Explicit line joining【10†¶】
L36: Two or more physical lines may be joined into logical lines using backslash characters (`\`), as follows: when a physical line ends in a backslash that is not part of a string literal or comment, it is joined with the following forming a single logical line, deleting the backslash and the following end-of-line character. For example:
L37: 
L38:     if 1900 < year < 2100 and 1 <= month <= 12 \
L39:        and 1 <= day <= 31 and 0 <= hour < 24 \
L40:        and 0 <= minute < 60 and 0 <= second < 60:   # Looks like a valid date
L41:             return 1
L42: A line ending in a backslash cannot carry a comment. A backslash does not continue a comment. A backslash does not continue a token except for string literals (i.e., tokens other than string literals cannot be split across physical lines using a backslash). A backslash is illegal elsewhere on a line outside a string literal.
L43: ### 2.1.6. Implicit line joining【11†¶】
L44: 
L45: Expressions in parentheses, square brackets or curly braces can be split over more than one physical line without using backslashes. For example:
L46: 
L47:     month_names = ['Januari', 'Februari', 'Maart',      # These are the
L48:                    'April',   'Mei',      'Juni',       # Dutch names
L49:                    'Juli',    'Augustus', 'September',  # for the months
L50:                    'Oktober', 'November', 'December']   # of the year
L51: Implicitly continued lines can carry comments. The indentation of the continuation lines is not important. Blank continuation lines are allowed. There is no NEWLINE token between implicit continuation lines. Implicitly continued lines can also occur within triple-quoted strings (see below); in that case they cannot carry comments.
L52: ### 2.1.7. Blank lines【12†¶】
L53: 
L54: A logical line that contains only spaces, tabs, formfeeds and possibly a comment, is ignored (i.e., no NEWLINE token is generated). During interactive input of statements, handling of a blank line may differ depending on the implementation of the read-eval-print loop. In the standard interactive interpreter, an entirely blank logical line (i.e. one containing not even whitespace or a comment) terminates a multi-line statement.
L55: ### 2.1.8. Indentation【13†¶】
L56: 
L57: Leading whitespace (spaces and tabs) at the beginning of a logical line is used to compute the indentation level of the line, which in turn is used to determine the grouping of statements.
L58: Tabs are replaced (from left to right) by one to eight spaces such that the total number of characters up to and including the replacement is a multiple of eight (this is intended to be the same rule as used by Unix). The total number of spaces preceding the first non-blank character then determines the line’s indentation. Indentation cannot be split over multiple physical lines using backslashes; the whitespace up to the first backslash determines the indentation.
L59: Indentation is rejected as inconsistent if a source file mixes tabs and spaces in a way that makes the meaning dependent on the worth of a tab in spaces; a 【14†`TabError`】 is raised in that case.
L60: 
L61: Cross-platform compatibility note: because of the nature of text editors on non-UNIX platforms, it is unwise to use a mixture of spaces and tabs for the indentation in a single source file. It should also be noted that different platforms may explicitly limit the maximum indentation level.
L62: A formfeed character may be present at the start of the line; it will be ignored for the indentation calculations above. Formfeed characters occurring elsewhere in the leading whitespace have an undefined effect (for instance, they may reset the space count to zero).
L63: 
L64: The indentation levels of consecutive lines are used to generate INDENT and DEDENT tokens, using a stack, as follows.
L65: Before the first line of the file is read, a single zero is pushed on the stack; this will never be popped off again. The numbers pushed on the stack will always be strictly increasing from bottom to top. At the beginning of each logical line, the line’s indentation level is compared to the top of the stack. If it is equal, nothing happens. If it is larger, it is pushed on the stack, and one INDENT token is generated.
L66: If it is smaller, it must be one of the numbers occurring on the stack; all numbers on the stack that are larger are popped off, and for each number popped off a DEDENT token is generated. At the end of the file, a DEDENT token is generated for each number remaining on the stack that is larger than zero.
L67: Here is an example of a correctly (though confusingly) indented piece of Python code:
L68: 
L69:     def perm(l):
L70:             # Compute the list of all permutations of l
L71:         if len(l) <= 1:
L72:                       return [l]
L73:         r = []
L74:         for i in range(len(l)):
L75:                  s = l[:i] + l[i+1:]
L76:                  p = perm(s)
L77:                  for x in p:
L78:                   r.append(l[i:i+1] + x)
L79:         return r
L80: The following example shows various indentation errors:
L81: 
L82:      def perm(l):                       # error: first line indented
L83:     for i in range(len(l)):             # error: not indented
L84:         s = l[:i] + l[i+1:]
L85:             p = perm(l[:i] + l[i+1:])   # error: unexpected indent
L86:             for x in p:
L87:                     r.append(l[i:i+1] + x)
L88:                 return r                # error: inconsistent dedent
L89: (Actually, the first three errors are detected by the parser; only the last error is found by the lexical analyzer — the indentation of `return r` does not match a level popped off the stack.)
L90: ### 2.1.9. Whitespace between tokens【15†¶】
L91: 

{"chunk_id":"34f4ed","wall_time_seconds":0.000009084,"exit_code":0,"original_token_count":199,"output":"2026-11-03 17:09 CST\norigin/main\ntotal 8\ndrwxr-xr-x@ 13 oyamahappa  staff  416 Oct 27 20:56 .\ndrwxr-xr-x   7 oyamahappa  staff  224 Oct 11 23:48 ..\ndrwxr-xr-x  12 oyamahappa  staff  384 Nov  3 15:58 .git\ndrwxr-xr-x   9 oyamahappa  staff  288 Nov  3 17:07 .idea\ndrwxr-xr-x   9 oyamahappa  staff  288 Oct 10 10:41 .venv\ndrwxr-xr-x   3 oyamahappa  staff   96 Oct 19 12:08 character1\ndrwxr-xr-x   3 oyamahappa  staff   96 Oct 12 10:35 character2\ndrwxr-xr-x   3 oyamahappa  staff   96 Oct 12 11:43 character3\ndrwxr-xr-x   3 oyamahappa  staff   96 Oct 19 12:09 character5\ndrwxr-xr-x   3 oyamahappa  staff   96 Oct 19 11:32 docs\n-rw-r--r--   1 oyamahappa  staff  493 Oct 10 10:41 main.py\ndrwxr-xr-x   7 oyamahappa  staff  224 Oct 19 11:31 memory\ndrwxr-xr-x   4 oyamahappa  staff  128 Nov  2 23:13 work\n"}

## assistant · 2026-11-03T09:09:50Z

`4.py` 的重点是列宽、左右对齐和两位小数。我会从这行代码逐项讲解，再补充常用格式、练习和答案。笔记也会说明两个容易混淆的细节：开头的 `f` 与 `.2f` 中的 `f` 作用不同；中文字符的格式宽度与屏幕显示宽度可能不同。


## tool · 2026-11-03T09:10:00Z


Script completed
Wall time 8.0 seconds
Output:

{"content":[{"type":"text","text":"{\"pythonVersion\":\"Python 3.9.6\",\"environmentType\":\"venv\",\"executablePath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv/bin/python\",\"environmentPath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv\",\"packageManager\":\"pip\"}"}],"isError":false}
string — Common string operations — Python 3.9.25 documentation (https://docs.python.org/3.9/library/string.html)
citeturn1view0 [wordlim: 200] Crawled: today; Content type: text/html; Source: open({"ref_id":"https://docs.python.org/3.9/library/string.html","lineno":135}); Total lines: 443
L91: For compound field names, these functions are only called for the first component of the field name; subsequent components are handled through normal attribute and indexing operations.
L92: 
L93: So for example, the field expression ‘0.name’ would cause 【24†`get_value()`】 to be called with a key argument of 0. The `name` attribute will be looked up after 【24†`get_value()`】 returns by calling the built-in 【25†`getattr()`】 function.
L94: If the index or keyword refers to an item that does not exist, then an 【26†`IndexError`】 or 【27†`KeyError`】 should be raised.
L95: 
L96: `check_unused_args`(used_args, args, kwargs)【28†¶】
L97: Implement checking for unused arguments if desired. The arguments to this function is the set of all argument keys that were actually referred to in the format string (integers for positional arguments, and strings for named arguments), and a reference to the args and kwargs that was passed to vformat. The set of unused args can be calculated from these parameters. 【28†`check_unused_args()`】 is assumed to raise an exception if the check fails.
L98: 
L99: `format_field`(value, format_spec)【29†¶】
L100: 【29†`format_field()`】 simply calls the global 【30†`format()`】 built-in. The method is provided so that subclasses can override it.
L101: 
L102: `convert_field`(value, conversion)【31†¶】
L103: 
L104: 
L105: Converts the value (returned by 【23†`get_field()`】) given a conversion type (as in the tuple returned by the 【22†`parse()`】 method). The default version understands ‘s’ (str), ‘r’ (repr) and ‘a’ (ascii) conversion types.
L106: ## Format String Syntax【32†¶】
L107: 
L108: The 【16†`str.format()`】 method and the 【18†`Formatter`】 class share the same syntax for format strings (although in the case of 【18†`Formatter`】, subclasses can define their own format string syntax). The syntax is related to that of 【33†formatted string literals】, but it is less sophisticated and, in particular, does not support arbitrary expressions.
L109: Format strings contain “replacement fields” surrounded by curly braces `{}`. Anything that is not contained in braces is considered literal text, which is copied unchanged to the output. If you need to include a brace character in the literal text, it can be escaped by doubling: `{{` and `}}`.
L110: 
L111: The grammar for a replacement field is as follows:
L112: > replacement_field ::=  "{" [【34†`field_name`】] ["!" 【35†`conversion`】] [":" 【36†`format_spec`】] "}"
L113: >     field_name        ::=  arg_name ("." 【37†`attribute_name`】 | "[" 【38†`element_index`】 "]")*
L114: >     arg_name          ::=  [【39†`identifier`】 | 【40†`digit`】+]
L115: >     attribute_name    ::=  【39†`identifier`】
L116: >     element_index     ::=  【40†`digit`】+ | 【41†`index_string`】
L117: >     index_string      ::=  <any source character except "]"> +
L118: >     conversion        ::=  "r" | "s" | "a"
L119: >     format_spec       ::=  <described in the next section>
L120: >
L121: In less formal terms, the replacement field can start with a field_name that specifies the object whose value is to be formatted and inserted into the output instead of the replacement field. The field_name is optionally followed by a conversion field, which is preceded by an exclamation point `'!'`, and a format_spec, which is preceded by a colon `':'`. These specify a non-default format for the replacement value.
L122: 
L123: See also the 【42†Format Specification Mini-Language】 section.
L124: The field_name itself begins with an arg_name that is either a number or a keyword. If it’s a number, it refers to a positional argument, and if it’s a keyword, it refers to a named keyword argument. If the numerical arg_names in a format string are 0, 1, 2, … in sequence, they can all be omitted (not just some) and the numbers 0, 1, 2, … will be automatically inserted in that order.
L125: Because arg_name is not quote-delimited, it is not possible to specify arbitrary dictionary keys (e.g., the strings `'10'` or `':-]'`) within a format string. The arg_name can be followed by any number of index or attribute expressions. An expression of the form `'.name'` selects the named attribute using 【25†`getattr()`】, while an expression of the form `'[index]'` does an index lookup using 【43†`__getitem__()`】.
L126: Changed in version 3.1: The positional argument specifiers can be omitted for 【16†`str.format()`】, so `'{} {}'.format(a, b)` is equivalent to `'{0} {1}'.format(a, b)`.
L127: 
L128: Changed in version 3.4: The positional argument specifiers can be omitted for 【18†`Formatter`】.
L129: Some simple format string examples:
L130: 
L131:     "First, thou shalt count to {0}"  # References first positional argument
L132:     "Bring me a {}"                   # Implicitly references the first positional argument
L133:     "From {} to {}"                   # Same as "From {0} to {1}"
L134:     "My quest is {name}"              # References keyword argument 'name'
L135:     "Weight in tons {0.weight}"       # 'weight' attribute of first positional arg
L136:     "Units destroyed: {players[0]}"   # First element of keyword argument 'players'.
L137: The conversion field causes a type coercion before formatting. Normally, the job of formatting a value is done by the 【44†`__format__()`】 method of the value itself. However, in some cases it is desirable to force a type to be formatted as a string, overriding its own definition of formatting. By converting the value to a string before calling 【44†`__format__()`】, the normal formatting logic is bypassed.
L138: Three conversion flags are currently supported: `'!s'` which calls 【45†`str()`】 on the value, `'!r'` which calls 【46†`repr()`】 and `'!a'` which calls 【47†`ascii()`】.
L139: 
L140: Some examples:
L141: 
L142:     "Harold's a clever {0!s}"        # Calls str() on the argument first
L143:     "Bring out the holy {name!r}"    # Calls repr() on the argument first
L144:     "More {!a}"                      # Calls ascii() on the argument first
L145: The format_spec field contains a specification of how the value should be presented, including such details as field width, alignment, padding, decimal precision and so on. Each value type can define its own “formatting mini-language” or interpretation of the format_spec.
L146: 
L147: Most built-in types support a common formatting mini-language, which is described in the next section.
L148: A format_spec field can also include nested replacement fields within it. These nested replacement fields may contain a field name, conversion flag and format specification, but deeper nesting is not allowed. The replacement fields within the format_spec are substituted before the format_spec string is interpreted. This allows the formatting of a value to be dynamically specified.
L149: 
L150: See the 【48†Format examples】 section for some examples.
L151: ### Format Specification Mini-Language【49†¶】
L152: 
L153: “Format specifications” are used within replacement fields contained within a format string to define how individual values are presented (see 【50†Format String Syntax】 and 【33†Formatted string literals】). They can also be passed directly to the built-in 【30†`format()`】 function. Each formattable type may define how the format specification is to be interpreted.
L154: Most built-in types implement the following options for format specifications, although some of the formatting options are only supported by the numeric types.
L155: 
L156: A general convention is that an empty format specification produces the same result as if you had called 【45†`str()`】 on the value. A non-empty format specification typically modifies the result.
L157: The general form of a standard format specifier is:
L158: 
L159:     format_spec     ::=  [[【51†`fill`】]【52†`align`】][【53†`sign`】][#][0][【54†`width`】][【55†`grouping_option`】][.【56†`precision`】][【57†`type`】]
L160:     fill            ::=  <any character>
L161:     align           ::=  "<" | ">" | "=" | "^"
L162:     sign            ::=  "+" | "-" | " "
L163:     width           ::=  【40†`digit`】+
L164:     grouping_option ::=  "_" | ","
L165:     precision       ::=  【40†`digit`】+
L166:     type            ::=  "b" | "c" | "d" | "e" | "E" | "f" | "F" | "g" | "G" | "n" | "o" | "s" | "x" | "X" | "%"
L167: If a valid align value is specified, it can be preceded by a fill character that can be any character and defaults to a space if omitted. It is not possible to use a literal curly brace (”`{`” or “`}`”) as the fill character in a 【33†formatted string literal】 or when using the 【16†`str.format()`】 method. However, it is possible to insert a curly brace with a nested replacement field. This limitation doesn’t affect the 【30†`format()`】 function.
L168: 
L169: The meaning of the various alignment options is as follows:
L170: > Option  | Meaning
L171: > --- | ---
L172: > `'<'`  | Forces the field to be left-aligned within the available space (this is the default for most objects).
L173: > `'>'`  | Forces the field to be right-aligned within the available space (this is the default for numbers).
L174: > `'='`  | Forces the padding to be placed after the sign (if any) but before the digits. This is used for printing fields in the form ‘+000000120’. This alignment option is only valid for numeric types. It becomes the default when ‘0’ immediately precedes the field width.
L175: > `'^'`  | Forces the field to be centered within the available space.
L176: Note that unless a minimum field width is defined, the field width will always be the same size as the data to fill it, so that the alignment option has no meaning in this case.
L177: 
L178: The sign option is only valid for number types, and can be one of the following:
L179: > Option  | Meaning
L180: > --- | ---
L181: > `'+'`  | indicates that a sign should be used for both positive as well as negative numbers.
L182: > `'-'`  | indicates that a sign should be used only for negative numbers (this is the default behavior).
L183: > space  | indicates that a leading space should be used on positive numbers, and a minus sign on negative numbers.
L184: The `'#'` option causes the “alternate form” to be used for the conversion. The alternate form is defined differently for different types. This option is only valid for integer, float and complex types. For integers, when binary, octal, or hexadecimal output is used, this option adds the respective prefix `'0b'`, `'0o'`, `'0x'`, or `'0X'` to the output value.
L185: For float and complex the alternate form causes the result of the conversion to always contain a decimal-point character, even if no digits follow it. Normally, a decimal-point character appears in the result of these conversions only if a digit follows it. In addition, for `'g'` and `'G'` conversions, trailing zeros are not removed from the result.
L186: The `','` option signals the use of a comma for a thousands separator. For a locale aware separator, use the `'n'` integer presentation type instead.
L187: 
L188: Changed in version 3.1: Added the `','` option (see also 【58†PEP 378†www.python.org】).
L189: The `'_'` option signals the use of an underscore for a thousands separator for floating point presentation types and for integer presentation type `'d'`. For integer presentation types `'b'`, `'o'`, `'x'`, and `'X'`, underscores will be inserted every 4 digits. For other presentation types, specifying this option is an error.
L190: 
L191: Changed in version 3.6: Added the `'_'` option (see also 【59†PEP 515†www.python.org】).
L192: width is a decimal integer defining the minimum total field width, including any prefixes, separators, and other formatting characters. If not specified, then the field width will be determined by the content.
L193: 
L194: When no explicit alignment is given, preceding the width field by a zero (`'0'`) character enables sign-aware zero-padding for numeric types. This is equivalent to a fill character of `'0'` with an alignment type of `'='`.
L195: The precision is a decimal integer indicating how many digits should be displayed after the decimal point for presentation types `'f'` and `'F'`, or before and after the decimal point for presentation types `'g'` or `'G'`. For string presentation types the field indicates the maximum field size - in other words, how many characters will be used from the field content. The precision is not allowed for integer presentation types.
L196: 
L197: Finally, the type determines how the data should be presented.
L198: The available string presentation types are:
L199: 
L200: > Type  | Meaning
L201: > --- | ---
L202: > `'s'`  | String format. This is the default type for strings and may be omitted.
L203: > None  | The same as `'s'`.
L204: 
L205: The available integer presentation types are:
L206: > Type  | Meaning
L207: > --- | ---
L208: > `'b'`  | Binary format. Outputs the number in base 2.
L209: > `'c'`  | Character. Converts the integer to the corresponding unicode character before printing.
L210: > `'d'`  | Decimal Integer. Outputs the number in base 10.
L211: > `'o'`  | Octal format. Outputs the number in base 8.
L212: > `'x'`  | Hex format. Outputs the number in base 16, using lower-case letters for the digits above 9.
L213: > `'X'`  | Hex format. Outputs the number in base 16, using upper-case letters for the digits above 9. In case `'#'` is specified, the prefix `'0x'` will be upper-cased to `'0X'` as well.
L214: > `'n'`  | Number. This is the same as `'d'`, except that it uses the current locale setting to insert the appropriate number separator characters.
L215: > None  | The same as `'d'`.
L216: In addition to the above presentation types, integers can be formatted with the floating point presentation types listed below (except `'n'` and `None`). When doing so, 【60†`float()`】 is used to convert the integer to a floating point number before formatting.
L217: 
L218: The available presentation types for 【60†`float`】 and 【61†`Decimal`】 values are:
L219: > Type  | Meaning
L220: > --- | ---
L221: > `'e'`  | Scientific notation. For a given precision `p`, formats the number in scientific notation with the letter ‘e’ separating the coefficient from the exponent. The coefficient has one digit before and `p` digits after the decimal point, for a total of `p + 1` significant digits. With no precision given, uses a precision of `6` digits after the decimal point for 【60†`float`】, and shows all coefficient digits for 【61†`Decimal`】.
L222: If no digits follow the decimal point, the decimal point is also removed unless the `#` option is used.
L223: > `'E'`  | Scientific notation. Same as `'e'` except it uses an upper case ‘E’ as the separator character.
--------------------------------------------------------------------------------
2. Lexical analysis — Python 3.9.25 documentation (https://docs.python.org/3.9/reference/lexical_analysis.html)
citeturn1view1 [wordlim: 200] Crawled: today; Content type: text/html; Source: open({"ref_id":"https://docs.python.org/3.9/reference/lexical_analysis.html","lineno":245}); Total lines: 426
L195: Bytes literals are always prefixed with `'b'` or `'B'`; they produce an instance of the 【53†`bytes`】 type instead of the 【54†`str`】 type. They may only contain ASCII characters; bytes with a numeric value of 128 or greater must be expressed with escapes.
L196: Both string and bytes literals may optionally be prefixed with a letter `'r'` or `'R'`; such strings are called raw strings and treat backslashes as literal characters. As a result, in string literals, `'\U'` and `'\u'` escapes in raw strings are not treated specially. Given that Python 2.x’s raw unicode literals behave differently than Python 3.x’s the `'ur'` syntax is not supported.
L197: 
L198: New in version 3.3: The `'rb'` prefix of raw bytes literals has been added as a synonym of `'br'`.
L199: New in version 3.3: Support for the unicode legacy literal (`u'value'`) was reintroduced to simplify the maintenance of dual Python 2.x and 3.x codebases. See 【55†PEP 414†www.python.org】 for more information.
L200: 
L201: A string literal with `'f'` or `'F'` in its prefix is a formatted string literal; see 【56†Formatted string literals】. The `'f'` may be combined with `'r'`, but not with `'b'` or `'u'`, therefore raw formatted strings are possible, but formatted bytes literals are not.
L202: In triple-quoted literals, unescaped newlines and quotes are allowed (and are retained), except that three unescaped quotes in a row terminate the literal. (A “quote” is the character used to open the literal, i.e. either `'` or `"`.)
L203: 
L204: Unless an `'r'` or `'R'` prefix is present, escape sequences in string and bytes literals are interpreted according to rules similar to those used by Standard C. The recognized escape sequences are:
L205: Escape Sequence  | Meaning  | Notes
L206: --- | --- | ---
L207: `\newline`  | Backslash and newline ignored  |
L208: `\\`  | Backslash (`\`)  |
L209: `\'`  | Single quote (`'`)  |
L210: `\"`  | Double quote (`"`)  |
L211: `\a`  | ASCII Bell (BEL)  |
L212: `\b`  | ASCII Backspace (BS)  |
L213: `\f`  | ASCII Formfeed (FF)  |
L214: `\n`  | ASCII Linefeed (LF)  |
L215: `\r`  | ASCII Carriage Return (CR)  |
L216: `\t`  | ASCII Horizontal Tab (TAB)  |
L217: `\v`  | ASCII Vertical Tab (VT)  |
L218: `\ooo`  | Character with octal value ooo  | (1,3)
L219: `\xhh`  | Character with hex value hh  | (2,3)
L220: Escape sequences only recognized in string literals are:
L221: 
L222: Escape Sequence  | Meaning  | Notes
L223: --- | --- | ---
L224: `\N{name}`  | Character named name in the Unicode database  | (4)
L225: `\uxxxx`  | Character with 16-bit hex value xxxx  | (5)
L226: `\Uxxxxxxxx`  | Character with 32-bit hex value xxxxxxxx  | (6)
L227: 
L228: Notes:
L229: 
L230:   1. As in Standard C, up to three octal digits are accepted.
L231: 
L232:   2. Unlike in Standard C, exactly two hex digits are required.
L233:   3. In a bytes literal, hexadecimal and octal escapes denote the byte with the given value. In a string literal, these escapes denote a Unicode character with the given value.
L234: 
L235:   4. Changed in version 3.3: Support for name aliases 【57†1】 has been added.
L236: 
L237:   5. Exactly four hex digits are required.
L238: 
L239:   6. Any Unicode character can be encoded this way. Exactly eight hex digits are required.
L240: Unlike Standard C, all unrecognized escape sequences are left in the string unchanged, i.e., the backslash is left in the result. (This behavior is useful when debugging: if an escape sequence is mistyped, the resulting output is more easily recognized as broken.) It is also important to note that the escape sequences only recognized in string literals fall into the category of unrecognized escapes for bytes literals.
L241: > Changed in version 3.6: Unrecognized escape sequences produce a 【58†`DeprecationWarning`】. In a future Python version they will be a 【59†`SyntaxWarning`】 and eventually a 【3†`SyntaxError`】.
L242: Even in a raw literal, quotes can be escaped with a backslash, but the backslash remains in the result; for example, `r"\""` is a valid string literal consisting of two characters: a backslash and a double quote; `r"\"` is not a valid string literal (even a raw string cannot end in an odd number of backslashes). Specifically, a raw literal cannot end in a single backslash (since the backslash would escape the following quote character).
L243: Note also that a single backslash followed by a newline is interpreted as those two characters as part of the literal, not as a line continuation.
L244: ### 2.4.2. String literal concatenation【60†¶】
L245: Multiple adjacent string or bytes literals (delimited by whitespace), possibly using different quoting conventions, are allowed, and their meaning is the same as their concatenation. Thus, `"hello" 'world'` is equivalent to `"helloworld"`. This feature can be used to reduce the number of backslashes needed, to split long strings conveniently across long lines, or even to add comments to parts of strings, for example:
L246: 
L247:     re.compile("[A-Za-z_]"       # letter or underscore
L248:                "[A-Za-z0-9_]*"   # letter, digit or underscore
L249:               )
L250: Note that this feature is defined at the syntactical level, but implemented at compile time. The ‘+’ operator must be used to concatenate string expressions at run time. Also note that literal concatenation can use different quoting styles for each component (even mixing raw strings and triple quoted strings), and formatted string literals may be concatenated with plain string literals.
L251: ### 2.4.3. Formatted string literals【61†¶】
L252: 
L253: New in version 3.6.
L254: 
L255: A formatted string literal or f-string is a string literal that is prefixed with `'f'` or `'F'`. These strings may contain replacement fields, which are expressions delimited by curly braces `{}`. While other string literals always have a constant value, formatted strings are really expressions evaluated at run time.
L256: Escape sequences are decoded like in ordinary string literals (except when a literal is also marked as a raw string). After decoding, the grammar for the contents of the string is:
L257: 
L258:     f_string          ::=  (【62†`literal_char`】 | "{{" | "}}" | 【63†`replacement_field`】)*
L259:     replacement_field ::=  "{" 【64†`f_expression`】 ["="] ["!" 【65†`conversion`】] [":" 【66†`format_spec`】] "}"
L260:     f_expression      ::=  (【67†`conditional_expression`】 | "*" 【68†`or_expr`】)
L261:                              ("," 【67†`conditional_expression`】 | "," "*" 【68†`or_expr`】)* [","]
L262:                            | 【69†`yield_expression`】
L263:     conversion        ::=  "s" | "r" | "a"
L264:     format_spec       ::=  (【62†`literal_char`】 | NULL | 【63†`replacement_field`】)*
L265:     literal_char      ::=  <any code point except "{", "}" or NULL>
L266: The parts of the string outside curly braces are treated literally, except that any doubled curly braces `'{{'` or `'}}'` are replaced with the corresponding single curly brace. A single opening curly bracket `'{'` marks a replacement field, which starts with a Python expression. To display both the expression text and its value after evaluation, (useful in debugging), an equal sign `'='` may be added after the expression. A conversion field, introduced by an exclamation point `'!'` may follow.
L267: A format specifier may also be appended, introduced by a colon `':'`. A replacement field ends with a closing curly bracket `'}'`.
L268: Expressions in formatted string literals are treated like regular Python expressions surrounded by parentheses, with a few exceptions. An empty expression is not allowed, and both 【70†`lambda`】 and assignment expressions `:=` must be surrounded by explicit parentheses. Replacement expressions can contain line breaks (e.g. in triple-quoted strings), but they cannot contain comments. Each expression is evaluated in the context where the formatted string literal appears, in order from left to right.
L269: Changed in version 3.7: Prior to Python 3.7, an 【71†`await`】 expression and comprehensions containing an 【72†`async for`】 clause were illegal in the expressions in formatted string literals due to a problem with the implementation.
L270: When the equal sign `'='` is provided, the output will have the expression text, the `'='` and the evaluated value. Spaces after the opening brace `'{'`, within the expression and after the `'='` are all retained in the output. By default, the `'='` causes the 【73†`repr()`】 of the expression to be provided, unless there is a format specified. When a format is specified it defaults to the 【54†`str()`】 of the expression unless a conversion `'!r'` is declared.
L271: 
L272: New in version 3.8: The equal sign `'='`.
L273: If a conversion is specified, the result of evaluating the expression is converted before formatting. Conversion `'!s'` calls 【54†`str()`】 on the result, `'!r'` calls 【73†`repr()`】, and `'!a'` calls 【74†`ascii()`】.
L274: The result is then formatted using the 【75†`format()`】 protocol. The format specifier is passed to the 【76†`__format__()`】 method of the expression or conversion result. An empty string is passed when the format specifier is omitted. The formatted result is then included in the final value of the whole string.
L275: Top-level format specifiers may include nested replacement fields. These nested fields may include their own conversion fields and 【77†format specifiers】, but may not include more deeply-nested replacement fields. The 【77†format specifier mini-language】 is the same as that used by the 【78†`str.format()`】 method.
L276: 
L277: Formatted string literals may be concatenated, but replacement fields cannot be split across literals.
L278: Some examples of formatted string literals:
L279: 
L280:     >>> name = "Fred"
L281:     >>> f"He said his name is {name!r}."
L282:     "He said his name is 'Fred'."
L283:     >>> f"He said his name is {repr(name)}."  # repr() is equivalent to !r
L284:     "He said his name is 'Fred'."
L285:     >>> width = 10
L286:     >>> precision = 4
L287:     >>> value = decimal.Decimal("12.34567")
L288:     >>> f"result: {value:{width}.{precision}}"  # nested fields
L289:     'result:      12.35'
L290:     >>> today = datetime(year=2017, month=1, day=27)
L291:     >>> f"{today:%B %d, %Y}"  # using date format specifier
L292:     'January 27, 2017'
L293:     >>> f"{today=:%B %d, %Y}" # using date format specifier and debugging
L294:     'today=January 27, 2017'
L295:     >>> number = 1024
L296:     >>> f"{number:#0x}"  # using integer format specifier
L297:     '0x400'
L298:     >>> foo = "bar"
L299:     >>> f"{ foo = }" # preserves whitespace
L300:     " foo = 'bar'"
L301:     >>> line = "The mill's closed"
L302:     >>> f"{line = }"
L303:     'line = "The mill\'s closed"'
L304:     >>> f"{line = :20}"
L305:     "line = The mill's closed   "
L306:     >>> f"{line = !r:20}"
L307:     'line = "The mill\'s closed" '
L308: A consequence of sharing the same syntax as regular string literals is that characters in the replacement fields must not conflict with the quoting used in the outer formatted string literal:
L309: 
L310:     f"abc {a["x"]} def"    # error: outer string literal ended prematurely
L311:     f"abc {a['x']} def"    # workaround: use different quoting
L312: 
L313: 
L314: Backslashes are not allowed in format expressions and will raise an error:
L315: 
L316:     f"newline: {ord('\n')}"  # raises SyntaxError
L317: To include a value in which a backslash escape is required, create a temporary variable.
L318: 
L319:     >>> newline = ord('\n')
L320:     >>> f"newline: {newline}"
L321:     'newline: 10'
L322: 
L323: 
L324: Formatted string literals cannot be used as docstrings, even if they do not include expressions.
L325: 
L326:     >>> def foo():
L327:     ...     f"Not a docstring"
L328:     ...
L329:     >>> foo.__doc__ is None
L330:     True
L331: See also 【79†PEP 498†www.python.org】 for the proposal that added formatted string literals, and 【78†`str.format()`】, which uses a related format string mechanism.
L332: ### 2.4.4. Numeric literals【80†¶】
L333: 
L334: There are three types of numeric literals: integers, floating point numbers, and imaginary numbers. There are no complex literals (complex numbers can be formed by adding a real number and an imaginary number).
L335: 
L336: Note that numeric literals do not include a sign; a phrase like `-1` is actually an expression composed of the unary operator ‘`-`’ and the literal `1`.
L337: ### 2.4.5. Integer literals【81†¶】
L338: Integer literals are described by the following lexical definitions:
L339: 
L340:     integer      ::=  【82†`decinteger`】 | 【83†`bininteger`】 | 【84†`octinteger`】 | 【85†`hexinteger`】
L341:     decinteger   ::=  【86†`nonzerodigit`】 (["_"] 【87†`digit`】)* | "0"+ (["_"] "0")*
L342:     bininteger   ::=  "0" ("b" | "B") (["_"] 【88†`bindigit`】)+
L343:     octinteger   ::=  "0" ("o" | "O") (["_"] 【89†`octdigit`】)+
L344:     hexinteger   ::=  "0" ("x" | "X") (["_"] 【90†`hexdigit`】)+
L345:     nonzerodigit ::=  "1"..."9"
L346:     digit        ::=  "0"..."9"
L347:     bindigit     ::=  "0" | "1"
L348:     octdigit     ::=  "0"..."7"
L349:     hexdigit     ::=  【87†`digit`】 | "a"..."f" | "A"..."F"
L350: There is no limit for the length of integer literals apart from what can be stored in available memory.
L351: 
L352: Underscores are ignored for determining the numeric value of the literal. They can be used to group digits for enhanced readability. One underscore can occur between digits, and after base specifiers like `0x`.
L353: 
L354: Note that leading zeros in a non-zero decimal number are not allowed. This is for disambiguation with C-style octal literals, which Python used before version 3.0.
L355: Some examples of integer literals:
L356: 
L357:     7     2147483647                        0o177    0b100110111
L358:     3     79228162514264337593543950336     0o377    0xdeadbeef
L359:           100_000_000_000                   0b_1110_0101
L360: 
L361: 
L362: Changed in version 3.6: Underscores are now allowed for grouping purposes in literals.
L363: ### 2.4.6. Floating point literals【91†¶】
L364: Floating point literals are described by the following lexical definitions:
L365: 
L366:     floatnumber   ::=  【92†`pointfloat`】 | 【93†`exponentfloat`】
L367:     pointfloat    ::=  [【94†`digitpart`】] 【95†`fraction`】 | 【94†`digitpart`】 "."
L368:     exponentfloat ::=  (【94†`digitpart`】 | 【92†`pointfloat`】) 【96†`exponent`】
L369:     digitpart     ::=  【87†`digit`】 (["_"] 【87†`digit`】)*
L370:     fraction      ::=  "." 【94†`digitpart`】
L371:     exponent      ::=  ("e" | "E") ["+" | "-"] 【94†`digitpart`】
L372: Note that the integer and exponent parts are always interpreted using radix 10. For example, `077e010` is legal, and denotes the same number as `77e10`. The allowed range of floating point literals is implementation-dependent. As in integer literals, underscores are supported for digit grouping.
L373: 
L374: Some examples of floating point literals:
L375: 


## assistant · 2026-11-03T09:10:17Z

项目使用 Python 3.9.6，笔记会采用该版本支持的写法。我会使用 `python-tools` 确认的解释器运行笔记中的示例，核对输出和常见错误。


## tool · 2026-11-03T09:12:56Z


Script completed
Wall time 0.3 seconds
Output:

{}

## tool · 2026-11-03T09:13:18Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"c31ea0","wall_time_seconds":0.000566625,"exit_code":0,"original_token_count":3989,"output":"# Python f-string 详细笔记\n\n本笔记结合 [`work/3-261102/4.py`](../work/3-261102/4.py) 的商品信息输出练习，示例适用于项目的 Python 3.9.6。标有 `>>>` 的内容表示交互式输入，不需要把 `>>>` 一起复制到 `.py` 文件；后面的行是实际输出。\n\n## 1. f-string 的作用\n\nf-string 的全称是 formatted string literal，即“格式化字符串字面量”。在字符串引号前加 `f`，就可以在 `{}` 中放入变量或表达式，并控制显示格式。基本语法可参阅 [Python 官方教程](https://docs.python.org/3.9/tutorial/inputoutput.html#formatted-string-literals)。\n\n```pycon\n>>> name = \"小明\"\n>>> age = 18\n>>> print(f\"我叫{name}，今年{age}岁。\")\n我叫小明，今年18岁。\n\n```\n\n`f` 和 `F` 都可以，通常使用小写 `f`；单双引号都可以。\n\nf-string 的结果是字符串，`print()` 负责把它输出。也可以先把结果保存到变量中：\n\n```pycon\n>>> message = f\"姓名：{name}，年龄：{age}\"\n>>> print(message)\n姓名：小明，年龄：18\n>>> type(message)\n<class 'str'>\n\n```\n\n不加 `f` 时，花括号和变量名会按原样显示：\n\n```pycon\n>>> print(\"姓名：{name}\")\n姓名：{name}\n\n```\n\n## 2. 从当前题目理解完整写法\n\n原代码：\n\n```python\nname = input()\nprice = float(input())\nquantity = int(input())\nprint(f\"{name:<10} {price:>8.2f} {quantity:>3}\")\n```\n\n`input()` 返回字符串，因此单价先转成 `float`，数量先转成 `int`。\n\n| 部分 | 含义 |\n| --- | --- |\n| 引号前的 `f` | 启用 f-string，计算 `{}` 中的内容 |\n| `{name:<10}` | 名称左对齐，最小宽度为 10，不足补空格 |\n| `{price:>8.2f}` | 单价右对齐，最小宽度为 8，保留两位小数 |\n| `{quantity:>3}` | 数量右对齐，最小宽度为 3 |\n| 两组花括号之间的空格 | 额外输出一个分隔空格 |\n\n用英文名称观察空格更直观：\n\n```pycon\n>>> name, price, quantity = \"Apple\", 5.5, 3\n>>> print(f\"{name:<10} {price:>8.2f} {quantity:>3}\")\nApple          5.50   3\n>>> row = f\"{name:<10} {price:>8.2f} {quantity:>3}\"\n>>> len(row)\n23\n>>> print(row.replace(\" \", \"·\"))\nApple··········5.50···3\n\n```\n\n最后一行把实际空格替换成 `·`，方便数空格。原输出中没有这些圆点。\n\n这一行在内容没有超出列宽时，长度为 `10 + 1 + 8 + 1 + 3 = 23`。`print()` 还会在末尾输出换行符，这个换行符不属于变量 `row`。\n\n**两个 `f` 的作用不同：**引号前的 `f` 标记字符串；`.2f` 中的 `f` 指定定点小数格式。\n\n## 3. 花括号中的基本结构\n\n常见写法是 `{表达式:格式说明}`；不需要设置格式时，省略冒号及其后面的内容。\n\n```pycon\n>>> price = 5.5\n>>> print(f\"{price}\")\n5.5\n>>> print(f\"{price:.2f}\")\n5.50\n\n```\n\n读 `{price:>8.2f}` 时，按下面的顺序理解：\n\n1. `price`：需要显示的值。\n2. `:`：开始指定格式。\n3. `>`：右对齐。\n4. `8`：整个格式化结果至少占 8 个字符位置。\n5. `.2`：小数点后显示 2 位。\n6. `f`：按定点小数格式显示。\n\n对于这里的字符串和数字，冒号后常用选项的顺序是“填充与对齐、符号、进制前缀、补零、宽度、分组、精度、类型”；每项按需使用。完整规则见 [Python 格式说明文档](https://docs.python.org/3.9/library/string.html#format-specification-mini-language)。\n\n## 4. 对齐：`<`、`>`、`^`\n\n| 符号 | 含义 | 空余位置在哪里 |\n| --- | --- | --- |\n| `<` | 左对齐 | 右边 |\n| `>` | 右对齐 | 左边 |\n| `^` | 居中对齐 | 两边 |\n\n示例中的竖线是主动加上的边界标记，用于观察空格：\n\n```pycon\n>>> word = \"cat\"\n>>> print(f\"|{word:<7}|\")\n|cat    |\n>>> print(f\"|{word:>7}|\")\n|    cat|\n>>> print(f\"|{word:^7}|\")\n|  cat  |\n\n```\n\n这些符号位于冒号之后时表示格式对齐；放在普通 Python 表达式里时，`<`、`>` 仍然可以表示大小比较：\n\n```pycon\n>>> print(f\"{3 > 2}\")\nTrue\n\n```\n\n## 5. 宽度是最小宽度\n\n宽度不足时补字符；内容过长时完整显示，不会自动截断。\n\n```pycon\n>>> print(f\"|{123:>5}|\")\n|  123|\n>>> print(f\"|{123456:>5}|\")\n|123456|\n\n```\n\n数字的宽度包含负号、小数点、分隔符和进制前缀等。例如 `-5.50` 本身有 5 个字符：\n\n```pycon\n>>> print(f\"|{-5.5:>8.2f}|\")\n|   -5.50|\n\n```\n\n省略对齐符号时，字符串通常默认左对齐，数字通常默认右对齐。初学时明确写出 `<` 或 `>` 更容易阅读。\n\n```pycon\n>>> print(f\"|{'cat':7}|\")\n|cat    |\n>>> print(f\"|{12:7}|\")\n|     12|\n\n```\n\n## 6. 自定义填充字符\n\n在对齐符号前写一个填充字符，替代默认空格。例如 `*<7` 表示“用 `*` 填充、左对齐、最小宽度为 7”。\n\n```pycon\n>>> print(f\"{'cat':*<7}\")\ncat****\n>>> print(f\"{'cat':->7}\")\n----cat\n>>> print(f\"{'cat':_^7}\")\n__cat__\n\n```\n\n填充字符通常只写一个，并且紧挨对齐符号。\n\n## 7. 小数：`.2f`\n\n`.nf` 表示按定点小数格式显示，小数点后保留 `n` 位；不足补零，超过时进行舍入。\n\n```pycon\n>>> number = 12.3456\n>>> print(f\"{number:.0f}\")\n12\n>>> print(f\"{number:.1f}\")\n12.3\n>>> print(f\"{number:.2f}\")\n12.35\n>>> print(f\"{5:.2f}\")\n5.00\n>>> print(f\"{5.5:f}\")\n5.500000\n\n```\n\n对于 `float`，只写 `f` 默认显示 6 位小数。`.2f` 指小数点后的位数，不表示整个数字只占两位。\n\n格式化得到新的字符串，原数值保持不变：\n\n```pycon\n>>> value = 3.14159\n>>> text = f\"{value:.2f}\"\n>>> print(text)\n3.14\n>>> print(value)\n3.14159\n\n```\n\n**舍入注意：**`float` 使用二进制近似表示很多十进制小数，不应把格式化理解为总能得到十进制手算的“四舍五入”结果。\n\n```pycon\n>>> print(f\"{2.675:.2f}\")\n2.67\n>>> print(f\"{2.5:.0f}\")\n2\n>>> print(f\"{3.5:.0f}\")\n4\n\n```\n\n后两例展示恰好处于中点时取偶数的舍入结果。严格的十进制金额计算需要根据业务规则使用 `Decimal`；加 `.2f` 只改变显示，不能修正之前的计算误差。\n\n## 8. 整数、补零和正负号\n\n### 8.1 `d`：十进制整数\n\n```pycon\n>>> count = 23\n>>> print(f\"{count:d}\")\n23\n>>> print(f\"|{count:5d}|\")\n|   23|\n\n```\n\n### 8.2 `05d`：补零到至少 5 位\n\n```pycon\n>>> print(f\"{23:05d}\")\n00023\n>>> print(f\"{-23:05d}\")\n-0023\n>>> print(f\"{123456:05d}\")\n123456\n\n```\n\n`0` 指定数字的符号感知补零：负号保留在最前面，零补在负号和数字之间。宽度 5 包含负号。\n\n### 8.3 `+`：正数也显示符号\n\n```pycon\n>>> print(f\"{12:+d}\")\n+12\n>>> print(f\"{-12:+d}\")\n-12\n>>> print(f\"{12:+06d}\")\n+00012\n>>> print(f\"|{12: d}|\")\n| 12|\n\n```\n\n`+` 表示正负数都显示符号；空格符号选项表示正数前留一个空格、负数前显示负号。默认只显示负号。\n\n## 9. 千位分隔符和百分比\n\n### 9.1 `,` 与 `_`：数字分组\n\n```pycon\n>>> print(f\"{1234567:,}\")\n1,234,567\n>>> print(f\"{1234567.8:,.2f}\")\n1,234,567.80\n>>> print(f\"{1234567:_}\")\n1_234_567\n\n```\n\n`,` 放在宽度之后、精度之前。例如 `>15,.2f` 表示右对齐、最小宽度 15、千位逗号分组、两位小数。\n\n### 9.2 `%`：乘以 100 并显示百分号\n\n```pycon\n>>> ratio = 0.856\n>>> print(f\"{ratio:.1%}\")\n85.6%\n>>> print(f\"{ratio:.2%}\")\n85.60%\n>>> print(f\"{85.6:.1%}\")\n8560.0%\n\n```\n\n如果原值已经是 `85.6`，只需在普通小数格式之后添加字面百分号：\n\n```pycon\n>>> print(f\"{85.6:.1f}%\")\n85.6%\n\n```\n\n## 10. 科学计数法、有效数字和进制\n\n### 10.1 `e` 与 `g`\n\n```pycon\n>>> print(f\"{12345.678:.2e}\")\n1.23e+04\n>>> print(f\"{12345.678:.4g}\")\n1.235e+04\n>>> print(f\"{12.3456:.4g}\")\n12.35\n\n```\n\n`.2e` 表示科学计数法中小数点后 2 位；`.4g` 表示 4 位有效数字，并根据数值大小选择普通小数或科学计数法。它们与 `.4f` 的含义不同。\n\n### 10.2 `b`、`o`、`x`、`X`\n\n```pycon\n>>> number = 255\n>>> print(f\"{number:b}\")\n11111111\n>>> print(f\"{number:o}\")\n377\n>>> print(f\"{number:x}\")\nff\n>>> print(f\"{number:X}\")\nFF\n>>> print(f\"{number:#x}\")\n0xff\n>>> print(f\"{number:#b}\")\n0b11111111\n\n```\n\n`b` 是二进制，`o` 是八进制，`x` 和 `X` 是十六进制。`#` 在这些进制格式中添加相应前缀。\n\n## 11. 花括号中可以写表达式\n\n可以进行运算、调用函数、访问列表和字典，也可以使用条件表达式。\n\n```pycon\n>>> price, quantity = 5.5, 3\n>>> print(f\"总价：{price * quantity:.2f}\")\n总价：16.50\n>>> print(f\"名字长度：{len('Apple')}\")\n名字长度：5\n>>> items = [\"苹果\", \"香蕉\"]\n>>> print(f\"第一项：{items[0]}\")\n第一项：苹果\n>>> student = {\"name\": \"小明\", \"score\": 86}\n>>> print(f\"{student['name']}：{student['score']}分\")\n小明：86分\n>>> score = 86\n>>> print(f\"结果：{'及格' if score >= 60 else '不及格'}\")\n结果：及格\n\n```\n\nPython 3.9 中，表达式里的引号要避免与最外层引号冲突；例如外层双引号、字典键使用单引号。复杂计算可以提前放到变量中，让输出语句保持清楚。\n\n## 12. 花括号、换行和多行字符串\n\n### 12.1 输出花括号本身\n\n在 f-string 的普通文本部分，用 `{{` 输出 `{`，用 `}}` 输出 `}`。\n\n```pycon\n>>> print(f\"集合写法：{{1, 2, 3}}\")\n集合写法：{1, 2, 3}\n>>> name = \"小明\"\n>>> print(f\"{{{name}}}\")\n{小明}\n\n```\n\n`{{{name}}}` 中，外面的 `{{` 和 `}}` 输出花括号，中间的 `{name}` 替换变量。\n\n### 12.2 换行与多行\n\n```pycon\n>>> print(f\"姓名：{name}\\n年龄：{18}\")\n姓名：小明\n年龄：18\n>>> message = f\"\"\"姓名：{name}\n... 年龄：{18}\"\"\"\n>>> print(message)\n姓名：小明\n年龄：18\n\n```\n\n`\\n` 是换行；三引号允许直接保留换行。多行字符串中写进去的缩进也可能成为实际内容。\n\n## 13. 调试写法：`=`、`!s`、`!r`、`!a`\n\n### 13.1 `{变量=}`\n\nPython 3.8 起支持同时显示表达式文本和结果，项目 Python 3.9 可以使用。\n\n```pycon\n>>> quantity = 3\n>>> price = 5.5\n>>> print(f\"{quantity=}\")\nquantity=3\n>>> print(f\"{price * quantity=}\")\nprice * quantity=16.5\n>>> print(f\"{price=:.2f}\")\nprice=5.50\n\n```\n\n调试输出会保留表达式附近的空格；有固定输出要求的练习只在题目需要时使用它。\n\n### 13.2 `!s`、`!r`、`!a`\n\n| 写法 | 对应转换 | 常见用途 |\n| --- | --- | --- |\n| `{value!s}` | `str(value)` | 转成普通可读字符串 |\n| `{value!r}` | `repr(value)` | 查看引号、换行和其他转义细节 |\n| `{value!a}` | `ascii(value)` | 用转义形式表示非 ASCII 字符 |\n\n```pycon\n>>> text = \"A\\nB\"\n>>> print(f\"{text!s}\")\nA\nB\n>>> print(f\"{text!r}\")\n'A\\nB'\n>>> print(f\"{'中'!a}\")\n'\\u4e2d'\n\n```\n\n可以继续添加格式说明，例如 `{text!r:>12}`：先转换，再按字符串进行对齐。转换字段和调试语法详见 [f-string 语言参考](https://docs.python.org/3.9/reference/lexical_analysis.html#formatted-string-literals)。\n\n## 14. 动态指定宽度与精度\n\n格式说明中还可以引用变量：\n\n```pycon\n>>> value = 12.3456\n>>> width = 10\n>>> precision = 2\n>>> print(f\"|{value:>{width}.{precision}f}|\")\n|     12.35|\n\n```\n\n这里 `{width}` 替换为 `10`，`{precision}` 替换为 `2`，最终采用 `>10.2f`。普通练习宽度固定时，直接写数字即可。\n\n## 15. 日期也可以格式化\n\n日期对象的冒号后采用日期格式规则：\n\n```pycon\n>>> from datetime import datetime\n>>> moment = datetime(2026, 11, 3, 9, 5, 7)\n>>> print(f\"{moment:%Y-%m-%d %H:%M:%S}\")\n2026-11-03 09:05:07\n\n```\n\n这里 `%Y`、`%m`、`%d` 分别表示年、月、日，`%H`、`%M`、`%S` 分别表示时、分、秒。日期规则由日期对象解释，不同类型的格式说明可以不同。\n\n## 16. 常见错误与边界情况\n\n### 16.1 把字符串当作数字格式化\n\n```pycon\n>>> price = \"5.5\"\n>>> print(f\"{price:.2f}\")\nTraceback (most recent call last):\n...\nValueError: Unknown format code 'f' for object of type 'str'\n>>> print(f\"{float(price):.2f}\")\n5.50\n\n```\n\n来自 `input()` 的内容需要先按题意转换类型。\n\n### 16.2 给浮点数使用整数格式 `d`\n\n```pycon\n>>> print(f\"{3.5:d}\")\nTraceback (most recent call last):\n...\nValueError: Unknown format code 'd' for object of type 'float'\n\n```\n\n需要显示零位小数时可以用 `.0f`。只有题目确实要求转换为整数时才使用 `int()`，因为转换会截去小数部分。\n\n### 16.3 混淆宽度与精度\n\n| 写法 | 含义 |\n| --- | --- |\n| `{value:8}` | 最小宽度 8 |\n| `{value:.2f}` | 小数点后 2 位 |\n| `{value:8.2f}` | 最小宽度 8，小数点后 2 位 |\n| `{value:08.2f}` | 最小宽度 8，数字补零，小数点后 2 位 |\n\n```pycon\n>>> print(f\"{5.5:08.2f}\")\n00005.50\n\n```\n\n### 16.4 字符串精度表示截取长度\n\n```pycon\n>>> title = \"Python\"\n>>> print(f\"{title:.3s}\")\nPyt\n>>> print(f\"|{title:>8.3s}|\")\n|     Pyt|\n\n```\n\n对字符串使用 `.3s` 会最多保留前 3 个字符；对整数使用 `.2d` 则是无效格式。\n\n### 16.5 中文字符与屏幕宽度\n\n```pycon\n>>> name = \"苹果\"\n>>> len(name)\n2\n>>> print(f\"{name:<10}\".replace(\" \", \"·\"))\n苹果········\n\n```\n\n这里补 8 个空格。对字符串，Python 根据 Unicode 码点数量计算这种格式宽度；中文在很多终端中每个字显示为两列，emoji、组合字符和字体也会影响显示。因此中英文混排时，屏幕上不一定整齐。当前题目按要求使用 `<10` 即可，不能把显示列宽直接当作格式宽度。\n\n### 16.6 f-string 创建后不会自动更新\n\n```pycon\n>>> count = 1\n>>> message = f\"数量：{count}\"\n>>> count = 2\n>>> print(message)\n数量：1\n\n```\n\n表达式在执行到 f-string 时计算，生成的字符串保存当时的结果。\n\n### 16.7 括号和变量名\n\n- `{}` 中不能留空，花括号需要配对，否则会出现 `SyntaxError`。\n- 使用尚未定义的变量会出现 `NameError`。\n- Python 3.9 不支持在替换表达式内部写反斜杠或注释；需要换行分隔符时，先将它保存为变量再引用。字符串普通文本中的 `\\n` 可以正常使用。\n\n## 17. 常用写法速查\n\n表中的 `x` 分别取“示例值”，各行独立理解。\n\n| 写法 | 示例值 | 结果 | 用途 |\n| --- | --- | --- | --- |\n| `f\"{x}\"` | `23` | `23` | 直接插入 |\n| `f\"{x:<6}\"` | `\"cat\"` | `cat` 后补 3 个空格 | 左对齐 |\n| `f\"{x:>6}\"` | `\"cat\"` | 前补 3 个空格，再输出 `cat` | 右对齐 |\n| `f\"{x:^7}\"` | `\"cat\"` | 两边各补 2 个空格 | 居中 |\n| `f\"{x:.2f}\"` | `5.5` | `5.50` | 两位小数 |\n| `f\"{x:08.2f}\"` | `5.5` | `00005.50` | 数字补零 |\n| `f\"{x:05d}\"` | `23` | `00023` | 整数编号 |\n| `f\"{x:+d}\"` | `23` | `+23` | 显示正号 |\n| `f\"{x:,}\"` | `1234567` | `1,234,567` | 千位分组 |\n| `f\"{x:.1%}\"` | `0.856` | `85.6%` | 百分比 |\n| `f\"{x:.2e}\"` | `12345` | `1.23e+04` | 科学计数法 |\n| `f\"{x:.4g}\"` | `12.3456` | `12.35` | 有效数字 |\n| `f\"{x:#x}\"` | `255` | `0xff` | 十六进制 |\n| `f\"{x=}\"` | `23` | `x=23` | 调试 |\n\n## 18. 自测练习与答案\n\n先独立写出表达式，再运行核对。\n\n1. `name = \"Bob\"`，左对齐到宽度 8，用 `-` 填充。\n2. `price = 9.5`，右对齐到宽度 8，保留两位小数。\n3. `number = 42`，显示为四位编号，不足补零。\n4. `ratio = 0.875`，显示为带一位小数的百分比。\n5. `price = 3.5`、`quantity = 4`，输出 `总价：14.00元`。\n6. `name = \"Bob\"`，输出 `{Bob}`，保留两侧花括号。\n\n参考答案：\n\n```pycon\n>>> name = \"Bob\"\n>>> print(f\"{name:-<8}\")\nBob-----\n>>> price = 9.5\n>>> print(f\"|{price:>8.2f}|\")\n|    9.50|\n>>> number = 42\n>>> print(f\"{number:04d}\")\n0042\n>>> ratio = 0.875\n>>> print(f\"{ratio:.1%}\")\n87.5%\n>>> price, quantity = 3.5, 4\n>>> print(f\"总价：{price * quantity:.2f}元\")\n总价：14.00元\n>>> print(f\"{{{name}}}\")\n{Bob}\n\n```\n\n第二题答案中的竖线用于观察边界，实际题目没有要求时可以去掉。\n memory/agents.md   |  4 ++--\n memory/plan.md     |  7 ++++---\n memory/progress.md |  8 ++++++++\n memory/verify.md   | 10 +++++-----\n work/3-261102/1.py |  2 +-\n work/3-261102/8.py | 23 +++++++++++++++++++++--\n 6 files changed, 41 insertions(+), 13 deletions(-)\n"}
{"chunk_id":"b10e9d","wall_time_seconds":0.061651583,"exit_code":0,"original_token_count":16,"output":"TestResults(failed=0, attempted=126)\n4 exercise cases passed\n"}

## assistant · 2026-11-03T09:13:29Z

笔记已写好，包含 18 节内容、常用格式速查表和 6 道自测题。126 条交互式示例全部通过；原练习的普通输入、中文名称、超出列宽和负数共 4 组验证也通过。接下来记录验证结果并提交，只纳入本次笔记和记录文件。


## tool · 2026-11-03T09:13:32Z


Script completed
Wall time 0.1 seconds
Output:

{"i":0,"status":"fulfilled","value":{"chunk_id":"c925bd","wall_time_seconds":0.000008166,"exit_code":0,"original_token_count":1275,"output":"# 当前进度\n\n## f-string 详细笔记\n\n- [x] 阅读 `4.py`、现有记录和 Git 状态，核对 Python 官方文档。\n- [x] 通过 PyCharm 确认项目解释器为 Python 3.9.6。\n- [ ] 编写包含输出、常见错误、速查表和练习答案的详细笔记。\n- [ ] 运行笔记示例及原练习，检查实际输出和差异。\n- [ ] 更新开发日志，提交并普通推送至已有的 `origin/main`。\n\n## 7.py 同一行输入\n\n- [x] 检查目标脚本和引用，未发现调用方或关联测试。\n- [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n- [x] 使用 `split` 和 `map` 读取同一行数据。\n- [x] 使用项目解释器运行 4 组输入，输出断言通过，退出码为 0，标准错误为空；`git diff --check` 通过。\n- [x] 提交 `83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n\n## 历史任务：L1\n\n- [x] 阅读题目图片和空白 `character1/L1.py`。\n- [x] 确认项目 Python 版本为 3.9.6，本地日期为 2026-10-19。\n- [x] 完成五行输出和逐条注释；个人资料暂显示“待填写”。\n- [ ] 收到用户的姓名、班级、学号后替换三项文字。\n- [x] 实际运行脚本，五行输出、日期、解释器版本及逐条注释断言通过，标准错误为空。\n- [x] 更新开发记录，创建提交 `19fd4fc feat: complete L1 information card exercise`。\n- [ ] 推送到 `https://github.com/OyamaMeek/py-labs.git` 的 `main`：自动审批以缺少具体目的地授权为由拒绝，等待用户明确授权。\n\n已有其他文件的暂存和未暂存修改，均不纳入本任务提交。\n## [2026-10-19 11:32] L1 个人信息卡与环境自检\n\n- **需求/问题描述**：\n  > 根据题目图片完成 `character1/L1.py`，输出个人信息及本机 Python 环境。\n\n- **实际实现的功能与改动**：\n  - 使用五条 `print` 输出姓名、班级、学号、当前日期和 Python 版本，每条语句前有中文注释。\n  - 姓名、班级、学号尚未提供，明确标为“待填写”；日期为 2026-10-19，项目解释器版本为 3.9.6。\n  - 测试前确认空文件输出 0 行，五行输出断言失败；实现后使用项目解释器实际运行，五行输出、日期、版本和逐条注释断言全部通过，退出码为 0，标准错误为空。\n  - `git diff --check` 通过；项目没有现成的测试或静态检查配置。\n\n- **涉及文件**：\n  - `character1/L1.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`19fd4fc feat: complete L1 information card exercise`。\n- **推送状态**：自动审批拒绝了向 `https://github.com/OyamaMeek/py-labs.git` 的 `main` 分支执行普通推送，理由是缺少对该具体目的地的明确授权；远端未更新。\n\n---\n\n## [2026-10-27 23:23] 7.py 同一行输入\n\n- **需求/问题描述**：\n  > 三个整数及分隔符从同一行输入，使用 map 和 split。\n\n- **实际实现的功能与改动**：\n  - 使用 `input().split()` 拆分四项，使用 `map(int, ...)` 转换三个整数，保留指定分隔符输出。\n  - 修改前题目示例触发 `ValueError`；修改后示例、负数与零、多余空白、整数格式转换共 4 组实际运行与输出断言通过，标准错误为空。\n  - `git diff --check` 通过；未新增依赖或测试框架。\n\n- **涉及文件**：\n  - `work/2-261026/7.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n\n---\n# 协作环境\n\n- 项目：Python 基础练习，当前任务为结合 `work/3-261102/4.py` 整理 f-string 笔记。\n- 工具：文件编辑工具、Git、PyCharm Python 环境查询、Python 官方文档。\n- Python：项目 `.venv/bin/python`，版本 3.9.6，无需新增依赖。\n- 当前采用 Ponytail 最小修改原则，并使用 python-tools 查询解释器；无需新增依赖。\n# 当前任务\n\n- 在 `docs/f-string笔记.md` 整理适合初学者的详细笔记，以 `work/3-261102/4.py` 为起点。\n- 覆盖插值、表达式、格式说明、宽度与对齐、数字格式、转义、调试、动态格式、常见错误和练习答案。\n- 适配项目 Python 3.9.6，用可执行示例验证输出；不修改练习脚本，不增加依赖。\n- 影响范围仅为笔记、协作记录和开发日志，无需调整调用方、测试夹具、配置或导出。\n# 完成标准\n\n- 笔记解释 `4.py` 中全部格式说明，并提供速查表、常见错误和练习答案。\n- 使用 PyCharm 确认的 Python 3.9.6，通过标准库 doctest 验证笔记中所有交互式示例及预期异常。\n- 实际运行 `4.py` 的输入输出，并检查宽度不足、负数、中文字符场景。\n- 执行 `git diff --check`；不为文档任务新增测试框架、依赖或视觉验证。\n- 仅暂存任务文件，保留用户对 `work/3-261102/1.py` 和 `8.py` 的修改。\n"}}
{"i":1,"status":"fulfilled","value":{"chunk_id":"ed65e5","wall_time_seconds":0.000013459,"exit_code":0,"original_token_count":916,"output":"---\nname: verification-before-completion\ndescription: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always\n---\n\n# Verification Before Completion\n\n## Overview\n\n**Core principle:** Evidence before claims, always.\n\n**Violating the letter of this rule is violating the spirit of this rule.**\n\n## The Iron Law\n\n```\nNO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE\n```\n\nIf you haven't run the verification command in this message, you cannot claim it passes.\n\n## The Gate Function\n\n```\nBEFORE claiming any status or expressing satisfaction:\n\n1. IDENTIFY: What command proves this claim?\n2. RUN: Execute the FULL command (fresh, complete)\n3. READ: Full output, check exit code, count failures\n4. VERIFY: Does output confirm the claim?\n   - If NO: State actual status with evidence\n   - If YES: State claim WITH evidence\n5. ONLY THEN: Make the claim\n\nSkip any step = lying, not verifying\n```\n\n## Common Failures\n\n| Claim | Requires | Not Sufficient |\n|-------|----------|----------------|\n| Tests pass | Test command output: 0 failures | Previous run, \"should pass\" |\n| Linter clean | Linter output: 0 errors | Partial check, extrapolation |\n| Build succeeds | Build command: exit 0 | Linter passing, logs look good |\n| Bug fixed | Test original symptom: passes | Code changed, assumed fixed |\n| Regression test works | Red-green cycle verified | Test passes once |\n| Agent completed | VCS diff shows changes | Agent reports \"success\" |\n| Requirements met | Line-by-line checklist | Tests passing |\n\n## Red Flags - STOP\n\n- Using \"should\", \"probably\", \"seems to\"\n- Expressing satisfaction before verification (\"Great!\", \"Perfect!\", \"Done!\", etc.)\n- About to commit/push/PR without verification\n- Trusting agent success reports\n- Relying on partial verification\n- Thinking \"just this once\"\n- Tired and wanting work over\n- **ANY wording implying success without having run verification**\n\n## Rationalization Prevention\n\n| Excuse | Reality |\n|--------|---------|\n| \"Should work now\" | RUN the verification |\n| \"I'm confident\" | Confidence ≠ evidence |\n| \"Just this once\" | No exceptions |\n| \"Linter passed\" | Linter ≠ compiler |\n| \"Agent said success\" | Verify independently |\n| \"I'm tired\" | Exhaustion ≠ excuse |\n| \"Partial check is enough\" | Partial proves nothing |\n| \"Different words so rule doesn't apply\" | Spirit over letter |\n\n## Key Patterns\n\n**Tests:**\n```\n✅ [Run test command] [See: 34/34 pass] \"All tests pass\"\n❌ \"Should pass now\" / \"Looks correct\"\n```\n\n**Regression tests (TDD Red-Green):**\n```\n✅ Write → Run (pass) → Revert fix → Run (MUST FAIL) → Restore → Run (pass)\n❌ \"I've written a regression test\" (without red-green verification)\n```\n\n**Build:**\n```\n✅ [Run build] [See: exit 0] \"Build passes\"\n❌ \"Linter passed\" (linter doesn't check compilation)\n```\n\n**Requirements:**\n```\n✅ Re-read plan → Create checklist → Verify each → Report gaps or completion\n❌ \"Tests pass, phase complete\"\n```\n\n**Agent delegation:**\n```\n✅ Agent reports success → Check VCS diff → Verify changes → Report actual state\n❌ Trust agent report\n```\n\n## When To Apply\n\n**ALWAYS before:**\n- ANY variation of success/completion claims\n- ANY expression of satisfaction\n- ANY positive statement about work state\n- Committing, PR creation, task completion\n- Moving to next task\n- Delegating to agents\n\n**Rule applies to:**\n- Exact phrases\n- Paraphrases and synonyms\n- Implications of success\n- ANY communication suggesting completion/correctness\n2026-11-03 17:13\n"}}

## tool · 2026-11-03T09:13:48Z


Script completed
Wall time 0.2 seconds
Output:

{}
{"chunk_id":"2550ad","wall_time_seconds":0.000008416,"exit_code":0,"original_token_count":1219,"output":"diff --git a/docs/CHANGELOG.md b/docs/CHANGELOG.md\nindex d55f873..e6fcbef 100644\n--- a/docs/CHANGELOG.md\n+++ b/docs/CHANGELOG.md\n@@ -37,3 +37,23 @@\n - **Git 提交**：`83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n \n ---\n+\n+## [2026-11-03 17:13] f-string 详细学习笔记\n+\n+- **需求/问题描述**：\n+  > 结合 `work/3-261102/4.py` 整理一份 f-string 的详细笔记。\n+\n+- **实际实现的功能与改动**：\n+  - 新增 18 节中文笔记，逐项解释原题，覆盖常用格式、表达式、转义、调试、动态格式、日期、常见错误、速查表和 6 道练习答案。\n+  - 说明两个 `f` 的区别、最小宽度、浮点舍入和中文显示宽度，附 Python 官方文档链接。\n+  - Python 3.9.6 doctest：126 条示例全部通过；原练习普通输入、中文、超宽内容和负数共 4 组输入输出断言通过，退出码为 0、标准错误为空。\n+  - `git diff --check` 通过；未修改练习脚本，未新增依赖，未执行视觉检查。\n+\n+- **涉及文件**：\n+  - `docs/f-string笔记.md`\n+  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n+  - `docs/CHANGELOG.md`\n+\n+- **Git 提交**：待提交。\n+\n+---\ndiff --git a/memory/agents.md b/memory/agents.md\nindex 1574416..35fba7f 100644\n--- a/memory/agents.md\n+++ b/memory/agents.md\n@@ -1,6 +1,6 @@\n # 协作环境\n \n-- 项目：Python 基础练习，当前任务为 `work/2-261026/7.py`。\n-- 工具：文件编辑工具、Git、PyCharm Python 环境查询。\n+- 项目：Python 基础练习，当前任务为结合 `work/3-261102/4.py` 整理 f-string 笔记。\n+- 工具：文件编辑工具、Git、PyCharm Python 环境查询、Python 官方文档。\n - Python：项目 `.venv/bin/python`，版本 3.9.6，无需新增依赖。\n - 当前采用 Ponytail 最小修改原则，并使用 python-tools 查询解释器；无需新增依赖。\ndiff --git a/memory/plan.md b/memory/plan.md\nindex 95382b7..7bf4faa 100644\n--- a/memory/plan.md\n+++ b/memory/plan.md\n@@ -1,5 +1,6 @@\n # 当前任务\n \n-- 将 `work/2-261026/7.py` 改为同一行读取三个整数及分隔符。\n-- 使用 `input().split()` 拆分，使用 `map(int, ...)` 转换三个整数，保留原输出格式。\n-- 实际运行题目示例、负数与零、多余空白场景，检查输出与退出码。\n+- 在 `docs/f-string笔记.md` 整理适合初学者的详细笔记，以 `work/3-261102/4.py` 为起点。\n+- 覆盖插值、表达式、格式说明、宽度与对齐、数字格式、转义、调试、动态格式、常见错误和练习答案。\n+- 适配项目 Python 3.9.6，用可执行示例验证输出；不修改练习脚本，不增加依赖。\n+- 影响范围仅为笔记、协作记录和开发日志，无需调整调用方、测试夹具、配置或导出。\ndiff --git a/memory/progress.md b/memory/progress.md\nindex 2e9db89..6c0ac9a 100644\n--- a/memory/progress.md\n+++ b/memory/progress.md\n@@ -1,5 +1,13 @@\n # 当前进度\n \n+## f-string 详细笔记\n+\n+- [x] 阅读 `4.py`、现有记录和 Git 状态，核对 Python 官方文档。\n+- [x] 通过 PyCharm 确认项目解释器为 Python 3.9.6。\n+- [x] 编写 18 节详细笔记，包含输出、常见错误、速查表和 6 道练习及答案。\n+- [x] Python 3.9.6 doctest：126 条示例全部通过；原练习 4 组输入输出断言通过；`git diff --check` 通过。\n+- [ ] 更新开发日志，提交并普通推送至已有的 `origin/main`。\n+\n ## 7.py 同一行输入\n \n - [x] 检查目标脚本和引用，未发现调用方或关联测试。\ndiff --git a/memory/verify.md b/memory/verify.md\nindex 605a7af..4d64cf6 100644\n--- a/memory/verify.md\n+++ b/memory/verify.md\n@@ -1,7 +1,7 @@\n # 完成标准\n \n-- 使用 PyCharm 查询到的项目解释器运行 `work/2-261026/7.py`。\n-- 输入 `3 4 5 ,`，输出 `3,4,5`，退出码为 0。\n-- 覆盖负数、零、多余空白与整数格式转换，检查输出和退出码。\n-- 项目当前没有测试或静态检查配置；本次采用实际运行与输出断言验证，不新增测试框架。\n-- 提交前检查差异，仅包含本任务文件。\n+- 笔记解释 `4.py` 中全部格式说明，并提供速查表、常见错误和练习答案。\n+- 使用 PyCharm 确认的 Python 3.9.6，通过标准库 doctest 验证笔记中所有交互式示例及预期异常。\n+- 实际运行 `4.py` 的输入输出，并检查宽度不足、负数、中文字符场景。\n+- 执行 `git diff --check`；不为文档任务新增测试框架、依赖或视觉验证。\n+- 仅暂存任务文件，保留用户对 `work/3-261102/1.py` 和 `8.py` 的修改。\n M docs/CHANGELOG.md\n M memory/agents.md\n M memory/plan.md\n M memory/progress.md\n M memory/verify.md\n M work/3-261102/1.py\n M work/3-261102/8.py\n?? \"docs/f-string\\347\\254\\224\\350\\256\\260.md\"\n     614 docs/f-string笔记.md\n"}

## assistant · 2026-11-03T09:13:56Z

已按 `verification-before-completion` 技能核对运行结果和提交范围。笔记按基础语法、常用格式、边界情况和练习答案排列，建议先读第 2 节的原题讲解，再查第 17 节速查表。


## tool · 2026-11-03T09:14:00Z


Script completed
Wall time 2.7 seconds
Output:

{"chunk_id":"6b35a5","wall_time_seconds":0.000007541,"exit_code":0,"original_token_count":142,"output":" docs/CHANGELOG.md                          |  20 +\n \"docs/f-string\\347\\254\\224\\350\\256\\260.md\" | 614 +++++++++++++++++++++++++++++\n memory/agents.md                           |   4 +-\n memory/plan.md                             |   7 +-\n memory/progress.md                         |   8 +\n memory/verify.md                           |  10 +-\n 6 files changed, 653 insertions(+), 10 deletions(-)\n[main 51bc3e5] docs: add detailed f-string study notes\n 6 files changed, 653 insertions(+), 10 deletions(-)\n create mode 100644 \"docs/f-string\\347\\254\\224\\350\\256\\260.md\"\n"}

## tool · 2026-11-03T09:14:17Z


Script completed
Wall time 5.8 seconds
Output:

{"chunk_id":"f9e8f8","wall_time_seconds":1.002035083,"session_id":77842,"original_token_count":0,"output":""}
{"chunk_id":"735510","wall_time_seconds":0.000007291,"exit_code":0,"original_token_count":440,"output":"  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n\n---\n\n## [2026-11-03 17:13] f-string 详细学习笔记\n\n- **需求/问题描述**：\n  > 结合 `work/3-261102/4.py` 整理一份 f-string 的详细笔记。\n\n- **实际实现的功能与改动**：\n  - 新增 18 节中文笔记，逐项解释原题，覆盖常用格式、表达式、转义、调试、动态格式、日期、常见错误、速查表和 6 道练习答案。\n  - 说明两个 `f` 的区别、最小宽度、浮点舍入和中文显示宽度，附 Python 官方文档链接。\n  - Python 3.9.6 doctest：126 条示例全部通过；原练习普通输入、中文、超宽内容和负数共 4 组输入输出断言通过，退出码为 0、标准错误为空。\n  - `git diff --check` 通过；未修改练习脚本，未新增依赖，未执行视觉检查。\n\n- **涉及文件**：\n  - `docs/f-string笔记.md`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：待提交。\n\n---\n# 当前进度\n\n## f-string 详细笔记\n\n- [x] 阅读 `4.py`、现有记录和 Git 状态，核对 Python 官方文档。\n- [x] 通过 PyCharm 确认项目解释器为 Python 3.9.6。\n- [x] 编写 18 节详细笔记，包含输出、常见错误、速查表和 6 道练习及答案。\n- [x] Python 3.9.6 doctest：126 条示例全部通过；原练习 4 组输入输出断言通过；`git diff --check` 通过。\n- [ ] 更新开发日志，提交并普通推送至已有的 `origin/main`。\n\n## 7.py 同一行输入\n\n- [x] 检查目标脚本和引用，未发现调用方或关联测试。\n- [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n"}

## tool · 2026-11-03T09:14:20Z


Script completed
Wall time 0.0 seconds
Output:

{"chunk_id":"bd124b","wall_time_seconds":0.00000975,"exit_code":0,"original_token_count":20,"output":"To https://github.com/OyamaMeek/py-labs.git\n   4679057..51bc3e5  main -> main\n"}

## tool · 2026-11-03T09:14:33Z


Script completed
Wall time 4.5 seconds
Output:

{}
{"chunk_id":"ff215c","wall_time_seconds":0.000011209,"exit_code":0,"original_token_count":270,"output":"diff --git a/docs/CHANGELOG.md b/docs/CHANGELOG.md\nindex e6fcbef..53b06f0 100644\n--- a/docs/CHANGELOG.md\n+++ b/docs/CHANGELOG.md\n@@ -54,6 +54,6 @@\n   - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n   - `docs/CHANGELOG.md`\n \n-- **Git 提交**：待提交。\n+- **Git 提交**：`51bc3e5 docs: add detailed f-string study notes`，已推送至 `origin/main`。\n \n ---\ndiff --git a/memory/progress.md b/memory/progress.md\nindex 6c0ac9a..71269d5 100644\n--- a/memory/progress.md\n+++ b/memory/progress.md\n@@ -6,7 +6,7 @@\n - [x] 通过 PyCharm 确认项目解释器为 Python 3.9.6。\n - [x] 编写 18 节详细笔记，包含输出、常见错误、速查表和 6 道练习及答案。\n - [x] Python 3.9.6 doctest：126 条示例全部通过；原练习 4 组输入输出断言通过；`git diff --check` 通过。\n-- [ ] 更新开发日志，提交并普通推送至已有的 `origin/main`。\n+- [x] 更新开发日志，提交 `51bc3e5 docs: add detailed f-string study notes`，已普通推送至 `origin/main`。\n \n ## 7.py 同一行输入\n \n"}
{"chunk_id":"ec5a3c","wall_time_seconds":1.002693125,"session_id":4555,"original_token_count":26,"output":"[main d5e2464] docs: record f-string notes delivery\n 2 files changed, 2 insertions(+), 2 deletions(-)\n"}

## tool · 2026-11-03T09:14:36Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"d8c747","wall_time_seconds":0.00001125,"exit_code":0,"original_token_count":20,"output":"To https://github.com/OyamaMeek/py-labs.git\n   51bc3e5..d5e2464  main -> main\n"}
{"chunk_id":"7c4d0f","wall_time_seconds":0.000007708,"exit_code":0,"original_token_count":55,"output":" M work/3-261102/1.py\n M work/3-261102/8.py\nd5e2464 docs: record f-string notes delivery\n51bc3e5 docs: add detailed f-string study notes\nd5e24642a8bc1e78360d4c418338fd2dd18c18b2\nd5e24642a8bc1e78360d4c418338fd2dd18c18b2\n"}

## assistant · 2026-11-03T09:14:42Z

已整理好：[f-string 详细笔记](/Users/oyamahappa/Documents/GitHub/labs/py-labs/docs/f-string笔记.md)。

包含原题逐项讲解、对齐与填充、小数与百分比、表达式、转义、常见错误、速查表，以及 6 道练习和答案。

126 条示例全部验证通过，已提交并推送至 `origin/main`。

未修改练习代码；示例按项目 Python 3.9.6 验证，未检查其他版本。
