# C++ 统计颜色次数的字典

来源：codex

项目：/Users/oyamahappa/Documents/GitHub/labs/cpp-labs

## developer · 2026-11-07T05:17:39Z

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

Open and read the skill according to its location: filesystem skills should be read from the filesystem, environment-owned skills should be access via the corresponding environment, and cloud skills should be discovered by calling `skills.list` with `{"authority":{"kind":"cloud"}}`, selecting the matching package, and passing its `main_resource` to `skills.read`. Avoid re-reading skills when possible.

When a `SKILL.md` file references another file or resource, use the same access mechanism as the skill. Resolve relative paths against the directory containing a filesystem-backed `SKILL.md`. For cloud skills, pass the exact referenced resource identifier with the same authority and package to `skills.read`; do not treat `skill://` identifiers as filesystem paths.

# Plugins and Apps

Plugins are bundles of skills, tools, or both. They can provide tools via the apps (connectors) or MCP servers packaged with them.

Filter `ALL_TOOLS` by name or description to find relevant tools. Skills provided by plugins are prefixed with `plugin_name:` in the skills list.

Do not additionally call `list_mcp_resources` or `list_mcp_resource_templates` for apps.

## Decision Boundary

Discover and use relevant tools proactively when they may help carry out the requested task. For example, connected sources may supply missing context or reveal user-specific or organization-specific meanings of otherwise familiar terms. Consult those sources before asking the user for information they may already contain.

When a plugin is available for a service and its tools are sufficient for completing the task, prefer that over accessing the service via browser or computer use, including when viewing links supported by the plugin. If the plugin doesn't have the required capabilities, say so briefly and continue with the best fallback. If the user has an explicit preference, defer to that instead.

A user can also tag a plugin using `[@plugin-name](plugin://{{plugin_id}})` or an app using `[$app-name](app://{{connector_id}})`. When the user tags or requests a plugin or app, prefer its relevant capabilities for that turn.



## developer · 2026-11-07T05:17:39Z

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
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/cloud-environment/0.2.0/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.22/skills`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.8/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.4/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1105.12137/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r27` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.2/skills`
- `r28` = `/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.agents/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI- (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, settings, (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped instruc (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list (file: r2/skill-installer/SKILL.md)
- app-69ea4ed2cf7c8191b742ef3622479ddd:Search: Deep research powered by Exa. Use for lead generation, literat (file: r15/app-69ea4ed2cf7c8191b742ef3622479ddd/4.0.1/skills/Search/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motio (file: r1/apple-design/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motio (file: r0/apple-design/SKILL.md)
- archify: Create polished, validated architecture, workflow, sequence, dat (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Codex research, writing, manuscript review, study screenin (file: r3/ars-codex/3.24.2/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Structures Benchmark and Evaluation papers using the five-pill (file: r0/benchmark-paper-template/SKILL.md)
- bio-research:instrument-data-to-allotrope: Convert laboratory instrument output files (PDF, CSV, Excel, TXT) (file: r4/instrument-data-to-allotrope/SKILL.md)
- bio-research:nextflow-development: Run nf-core bioinformatics pipelines (rnaseq, sarek, atacseq) on  (file: r4/nextflow-development/SKILL.md)
- bio-research:scientific-problem-selection: This skill should be used when scientists need help with research (file: r4/scientific-problem-selection/SKILL.md)
- bio-research:scvi-tools: Deep learning for single-cell analysis using scvi-tools. This ski (file: r4/scvi-tools/SKILL.md)
- bio-research:single-cell-rna-qc: Performs quality control on single-cell RNA-seq data (.h5ad or .h (file: r4/single-cell-rna-qc/SKILL.md)
- bio-research:start: Set up your bio-research environment and explore available tool (file: r4/start/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end (file: r0/brandkit/SKILL.md)
- cli-anything: Use when the user wants Codex to build, refine, test, validate (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Discover agent-native CLIs for professional software. Access t (file: r0/cli-hub-meta-skill/SKILL.md)
- clion-debugger: Debugger-first runtime root-cause analysis for native and multi-l (file: r28/clion-debugger/SKILL.md)
- cloud-environment:cloud-desktop: Use in a managed Codex Cloud chat to open a URL in shared Chrome, (file: r16/cloud-desktop/SKILL.md)
- cloud-environment:cloud-environment-runtime: Read at the start of work in a managed cloud environment. Run b (file: r16/runtime/SKILL.md)
- code-review: Review the changes since a fixed point (commit, branch, tag, or  (file: r0/code-review/SKILL.md)
- codebase-design: Shared vocabulary for designing deep modules. Use when the user  (file: r0/codebase-design/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准备最小 (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Convert Word (.doc, .docx), PowerPoint (.ppt, .pptx), Excel (.xl (file: r1/convert-documents-to-markdown/SKILL.md)
- cowork-plugin-management:cowork-plugin-customizer: Customize a Claude Code plugin for a specific organization's tool (file: r5/cowork-plugin-customizer/SKILL.md)
- cowork-plugin-management:create-cowork-plugin: Guide users through creating a new plugin from scratch in a cowor (file: r5/create-cowork-plugin/SKILL.md)
- customer-support:customer-escalation: Package an escalation for engineering, product, or leadership w (file: r6/customer-escalation/SKILL.md)
- customer-support:customer-research: Multi-source research on a customer question or topic with sour (file: r6/customer-research/SKILL.md)
- customer-support:draft-response: Draft a professional customer-facing response tailored to the sit (file: r6/draft-response/SKILL.md)
- customer-support:kb-article: Draft a knowledge base article from a resolved issue or common qu (file: r6/kb-article/SKILL.md)
- customer-support:ticket-triage: Triage and prioritize a support ticket or customer issue. Use w (file: r6/ticket-triage/SKILL.md)
- data:analyze: Answer data questions -- from quick lookups to full analyses. U (file: r7/analyze/SKILL.md)
- data:build-dashboard: Build an interactive HTML dashboard with charts, filters, and t (file: r7/build-dashboard/SKILL.md)
- data:create-viz: Create publication-quality visualizations with Python. Use when t (file: r7/create-viz/SKILL.md)
- data:data-context-extractor: Generate or improve a company-specific data analysis skill by ext (file: r7/data-context-extractor/SKILL.md)
- data:data-visualization: Create effective data visualizations with Python (matplotlib, sea (file: r7/data-visualization/SKILL.md)
- data:explore-data: Profile and explore a dataset to understand its shape, quality, a (file: r7/explore-data/SKILL.md)
- data:sql-queries: Write correct, performant SQL across all major data warehouse d (file: r7/sql-queries/SKILL.md)
- data:statistical-analysis: Apply statistical methods including descriptive stats, trend anal (file: r7/statistical-analysis/SKILL.md)
- data:validate-data: QA an analysis before sharing -- methodology, accuracy, and bia (file: r7/validate-data/SKILL.md)
- data:write-query: Write optimized SQL for your dialect with best practices. Use w (file: r7/write-query/SKILL.md)
- deep-research: Runs a deep, survey-grade literature investigation on a research (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects depending on (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-dri (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diagnosis loop for hard bugs and performance regressions. Use wh (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r22/documents/26.1105.12137/skills/documents/SKILL.md)
- domain-modeling: Build and sharpen a project's domain model. Use when discussing  (file: r0/domain-modeling/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable Draw. (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it to o (file: r1/ego-browser/SKILL.md)
- enterprise-search:digest: Generate a daily or weekly digest of activity across all connect (file: r8/digest/SKILL.md)
- enterprise-search:knowledge-synthesis: Combines search results from multiple sources into coherent, d (file: r8/knowledge-synthesis/SKILL.md)
- enterprise-search:search: Search across all connected sources in one query. Trigger with " (file: r8/search/SKILL.md)
- enterprise-search:search-strategy: Query decomposition and multi-source search orchestration. Bre (file: r8/search-strategy/SKILL.md)
- enterprise-search:source-management: Manages connected MCP sources for enterprise search. Detects a (file: r8/source-management/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用户运行 (file: r0/evidence-recap/SKILL.md)
- figure-designer: Advises on the design of the three core figures in a technical p (file: r0/figure-designer/SKILL.md)
- finance:audit-support: Support SOX 404 compliance with control testing methodology, sam (file: r9/audit-support/SKILL.md)
- finance:close-management: Manage the month-end close process with task sequencing, depen (file: r9/close-management/SKILL.md)
- finance:financial-statements: Generate financial statements (income statement, balance sheet (file: r9/financial-statements/SKILL.md)
- finance:journal-entry: Prepare journal entries with proper debits, credits, and support (file: r9/journal-entry/SKILL.md)
- finance:journal-entry-prep: Prepare journal entries with proper debits, credits, and suppo (file: r9/journal-entry-prep/SKILL.md)
- finance:reconciliation: Reconcile accounts by comparing GL balances to subledgers, ban (file: r9/reconciliation/SKILL.md)
- finance:sox-testing: Generate SOX sample selections, testing workpapers, and control  (file: r9/sox-testing/SKILL.md)
- finance:variance-analysis: Decompose financial variances into drivers with narrative explan (file: r9/variance-analysis/SKILL.md)
- full-output-enforcement: Overrides default LLM truncation behavior. Enforces complete co (file: r0/output-skill/SKILL.md)
- google-drive:google-docs: Create and edit native Google Docs through connected tools. (file: r17/google-docs/SKILL.md)
- google-drive:google-drive: Use connected Google Drive as the single entrypoint for Drive, D (file: r17/google-drive/SKILL.md)
- google-drive:google-drive-comments: Write, reply to, and resolve Google Drive comments on Docs, Sh (file: r17/google-drive-comments/SKILL.md)
- google-drive:google-sheets: Analyze and edit connected Google Sheets with range precision. (file: r17/google-sheets/SKILL.md)
- google-drive:google-slides: Route Google Slides authoring requests and derive a design sys (file: r17/google-slides/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial pro (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial pro (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Elite UX/UI & Advanced GSAP Motion Engineer. Enforces Python-dr (file: r0/gpt-tasteskill/SKILL.md)
- graphify: Use for any question about a codebase, its architecture, file  (file: r0/graphify/SKILL.md)
- great-resume: 中文求职经历提升技能：根据目标岗位把真实经历重组为岗位定位、简历要点、项目亮点和 HR 开场白；当用户输入“/great-r (file: r0/great-resume/SKILL.md)
- grilling: Grill the user relentlessly about a plan, decision, or idea. U (file: r0/grilling/SKILL.md)
- gsap-core: Official GSAP skill for the core API — gsap.to(), from(), from (file: r0/gsap-core/SKILL.md)
- gsap-frameworks: Official GSAP skill for Vue, Svelte, and other non-React framewo (file: r0/gsap-frameworks/SKILL.md)
- gsap-performance: Official GSAP skill for performance — prefer transforms, avoid l (file: r0/gsap-performance/SKILL.md)
- gsap-plugins: Official GSAP skill for GSAP plugins — registration, ScrollToPlu (file: r0/gsap-plugins/SKILL.md)
- gsap-react: Official GSAP skill for React — useGSAP hook, refs, gsap.context (file: r0/gsap-react/SKILL.md)
- gsap-scrolltrigger: Official GSAP skill for ScrollTrigger — scroll-linked animations (file: r0/gsap-scrolltrigger/SKILL.md)
- gsap-timeline: Official GSAP skill for timelines — gsap.timeline(), position  (file: r0/gsap-timeline/SKILL.md)
- gsap-utils: Official GSAP skill for gsap.utils — clamp, mapRange, normalize, (file: r0/gsap-utils/SKILL.md)
- high-end-visual-design: Teaches the AI to design like a high-end agency. Defines the e (file: r0/soft-skill/SKILL.md)
- human-writing: 通用中文创作与改稿 Skill。用于知乎回答、论坛长帖、公众号文章、博客、评论、人物故事、历史叙事、新闻与行业解读、科普、教 (file: r0/human-writing/SKILL.md)
- humanizer:humanizer: Rewrite AI-sounding text so it reads like the writer without c (file: r1/humanizer/SKILL.md)
- humanizer:humanizer: Rewrite AI-sounding text so it reads like the writer without c (file: r0/humanizer/SKILL.md)
- hyperframes: Read first to make, edit, animate or render any video with Hyper (file: r0/hyperframes/SKILL.md)
- hyperframes-cli: The HyperFrames CLI by job - scaffold, check, look at frames, ed (file: r0/hyperframes-cli/SKILL.md)
- hyperframes-registry: About 450 ready-made HyperFrames blocks and components install (file: r0/hyperframes-registry/SKILL.md)
- idea-evaluator: Evaluates a preliminary research idea against a five-dimension (file: r0/idea-evaluator/SKILL.md)
- image-to-code: Elite website image-to-code skill for Codex. For visually impo (file: r0/image-to-code-skill/SKILL.md)
- imagegen-frontend-mobile: Elite mobile app image-generation skill for creating premium,  (file: r0/imagegen-frontend-mobile/SKILL.md)
- imagegen-frontend-web: Elite frontend image-direction skill for generating premium, con (file: r0/imagegen-frontend-web/SKILL.md)
- industrial-brutalist-ui: Raw mechanical interfaces fusing Swiss typographic print with mi (file: r0/brutalist-skill/SKILL.md)
- interview: 中文简历与目标岗位驱动的面试预测、模拟追问和复练技能：提取需要验证的经历 Claim，按面试轮次建立问题与评分契约，通过一次 (file: r0/interview/SKILL.md)
- intro-drafter: Drafts the Introduction prose for a technical paper, guided inte (file: r0/intro-drafter/SKILL.md)
- iphone-use: Use when a task needs a real iPhone — operating iOS apps that ha (file: r1/iphone-use/SKILL.md)
- job-apply: 中文求职申请自动填写技能：使用浏览器读取用户确认的简历资料，逐项填写招聘网站申请表并核对结果；当用户输入“/job-appl (file: r0/job-apply/SKILL.md)
- job-match: 中文岗位匹配分析技能：对照目标 JD 与用户已确认的简历、经历或主张—证据账本，区分已匹配、证据不足和真实缺口，生成可解释的 (file: r0/job-match/SKILL.md)
- legal:brief: Generate contextual briefings for legal work — daily summary, t (file: r10/brief/SKILL.md)
- legal:compliance-check: Run a compliance check on a proposed action, product feature, o (file: r10/compliance-check/SKILL.md)
- legal:legal-response: Generate a response to a common legal inquiry using configured  (file: r10/legal-response/SKILL.md)
- legal:legal-risk-assessment: Assess and classify legal risks using a severity-by-likelihood fr (file: r10/legal-risk-assessment/SKILL.md)
- legal:meeting-briefing: Prepare structured briefings for meetings with legal relevance  (file: r10/meeting-briefing/SKILL.md)
- legal:review-contract: Review a contract against your organization's negotiation playboo (file: r10/review-contract/SKILL.md)
- legal:signature-request: Prepare and route a document for e-signature — run a pre-signat (file: r10/signature-request/SKILL.md)
- legal:triage-nda: Rapidly triage an incoming NDA and classify it as GREEN (standa (file: r10/triage-nda/SKILL.md)
- legal:vendor-check: Check the status of existing agreements with a vendor across al (file: r10/vendor-check/SKILL.md)
- lemo-opuscar: Direct and produce a short film made entirely in code, in one  (file: r0/lemo-opuscar/SKILL.md)
- make-resume: 中文可编辑简历制作技能：默认基于 ASu 单栏高密度技术简历模板，根据用户经历制作或复刻可编辑 HTML/PDF；用户也可以 (file: r0/make-resume/SKILL.md)
- marketing:brand-review: Review content against your brand voice, style guide, and messa (file: r11/brand-review/SKILL.md)
- marketing:campaign-plan: Generate a full campaign brief with objectives, audience, messagi (file: r11/campaign-plan/SKILL.md)
- marketing:competitive-brief: Research competitors and generate a positioning and messaging com (file: r11/competitive-brief/SKILL.md)
- marketing:content-creation: Draft marketing content across channels — blog posts, social medi (file: r11/content-creation/SKILL.md)
- marketing:draft-content: Draft blog posts, social media, email newsletters, landing pages, (file: r11/draft-content/SKILL.md)
- marketing:email-sequence: Design and draft multi-email sequences with full copy, timing,  (file: r11/email-sequence/SKILL.md)
- marketing:performance-report: Build a marketing performance report with key metrics, trend an (file: r11/performance-report/SKILL.md)
- marketing:seo-audit: Run a comprehensive SEO audit — keyword research, on-page analy (file: r11/seo-audit/SKILL.md)
- media-use: Get or make any media for a HyperFrames video - music, sound eff (file: r0/media-use/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, typogr (file: r0/minimalist-skill/SKILL.md)
- notion:notion-build-my-engineering-wiki: Build a personalized Notion engineering home from technical do (file: r18/notion-build-my-engineering-wiki/SKILL.md)
- notion:notion-create-my-team-handbook: Create a team handbook in Notion from scattered processes, tea (file: r18/notion-create-my-team-handbook/SKILL.md)
- notion:notion-database-designer: Turns scattered notes and recurring work into useful Notion tr (file: r18/notion-database-designer/SKILL.md)
- notion:notion-knowledge-capture: Captures conversations and supplied notes as Notion wiki pages (file: r18/notion-knowledge-capture/SKILL.md)
- notion:notion-meeting-prep: Prepares meeting agendas, internal pre-reads, and decision brief (file: r18/notion-meeting-prep/SKILL.md)
- notion:notion-organize-my-semester: Organize a semester in Notion from course notes, syllabi, assign (file: r18/notion-organize-my-semester/SKILL.md)
- notion:notion-plan-marketing-campaigns: Organize campaign briefs, content ideas, and production work in  (file: r18/notion-plan-marketing-campaigns/SKILL.md)
- notion:notion-research-documentation: Researches questions across Notion sources and synthesizes cited (file: r18/notion-research-documentation/SKILL.md)
- notion:notion-set-up-my-project: Create a useful initial Notion project home with tasks, docs,  (file: r18/notion-set-up-my-project/SKILL.md)
- notion:notion-setup: Set up Notion so your agents can remember your preferences, fi (file: r18/notion-setup/SKILL.md)
- notion:notion-spec-to-implementation: Converts Notion product or technical specs into implementation p (file: r18/notion-spec-to-implementation/SKILL.md)
- notion:notion-weekly-project-digest: Produces evidence-based weekly project or team updates by comp (file: r18/notion-weekly-project-digest/SKILL.md)
- offer: 中文秋招求职进度管理技能：记录和更新投递、筛选、测评、面试、Offer、拒信及招聘邮件状态，生成可搜索的进度表；当用户输入“ (file: r0/offer/SKILL.md)
- paper-polish: Polishes existing academic prose while preserving the author's (file: r0/paper-polish/SKILL.md)
- paper-writer: Drafts publishable paper prose from the author's own materials (file: r0/paper-writer/SKILL.md)
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不阻塞主 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著录字 (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申请一起 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包，须另点名 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开。 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r22/pdf/26.1105.12137/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r15/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the  (file: r24/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks (file: r24/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r24/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r24/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r24/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r24/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five di (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r22/presentations/26.1105.12137/skills/presentations/SKILL.md)
- product-management:competitive-brief: Create a competitive analysis brief for one or more competitors  (file: r12/competitive-brief/SKILL.md)
- product-management:metrics-review: Review and analyze product metrics with trend analysis and act (file: r12/metrics-review/SKILL.md)
- product-management:product-brainstorming: Brainstorm product ideas, explore problem spaces, and challenge  (file: r12/product-brainstorming/SKILL.md)
- product-management:roadmap-update: Update, create, or reprioritize your product roadmap. Use when (file: r12/roadmap-update/SKILL.md)
- product-management:sprint-planning: Plan a sprint — scope work, estimate capacity, set goals, and  (file: r12/sprint-planning/SKILL.md)
- product-management:stakeholder-update: Generate a stakeholder update tailored to audience and cadence (file: r12/stakeholder-update/SKILL.md)
- product-management:synthesize-research: Synthesize user research from interviews, surveys, and feedback  (file: r12/synthesize-research/SKILL.md)
- product-management:write-spec: Write a feature spec or PRD from a problem statement or featur (file: r12/write-spec/SKILL.md)
- productivity:memory-management: Two-tier memory system that makes Claude a true workplace coll (file: r13/memory-management/SKILL.md)
- productivity:start: Initialize the productivity system and open the dashboard. Use (file: r13/start/SKILL.md)
- productivity:task-management: Simple task management using a shared TASKS.md file. Reference (file: r13/task-management/SKILL.md)
- productivity:update: Sync tasks and refresh memory from your current activity. Use wh (file: r13/update/SKILL.md)
- project-guide: 中文项目导学、源码课程与项目面经技能：基于本地项目仓库、项目描述或技术材料，按需生成源码课程与理解题，或生成 导学-{简称}.m (file: r0/project-guide/SKILL.md)
- prototype: Build a throwaway prototype to answer a design question. Use whe (file: r0/prototype/SKILL.md)
- rebuttal-guidance: Provides actionable peer-review rebuttal guidance (not full rebu (file: r0/rebuttal-guidance/SKILL.md)
- redesign-existing-projects: Upgrades existing websites and apps to premium quality. Audits (file: r0/redesign-skill/SKILL.md)
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
- research: Investigate a question against high-trust primary sources and  (file: r0/research/SKILL.md)
- reverse-engineer-anything: Reverse engineer native, managed, Electron/JavaScript, packaged, (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized rever (file: r25/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sales:account-context: 360-degree view of an account - CRM data, recent email threads, d (file: r14/account-context/SKILL.md)
- sales:account-plan: Build or refresh a strategic account plan - current state, goal (file: r14/account-plan/SKILL.md)
- sales:account-research: Research a target company and optionally a specific contact - c (file: r14/account-research/SKILL.md)
- sales:account-tiering: Score and tier a list of accounts (or your full book) against ICP (file: r14/account-tiering/SKILL.md)
- sales:call-prep: Pre-call brief for an upcoming meeting - attendees, account histo (file: r14/call-prep/SKILL.md)
- sales:call-summary: Turn a call transcript or call notes into a customer follow-up  (file: r14/call-summary/SKILL.md)
- sales:close-plan: Build the business case and mutual action plan for a deal - the (file: r14/close-plan/SKILL.md)
- sales:competitive-intelligence: Competitive analysis two ways - the in-deal play against a name (file: r14/competitive-intelligence/SKILL.md)
- sales:create-an-asset: Build a customer deck, one-pager or leave-behind from your accoun (file: r14/create-an-asset/SKILL.md)
- sales:crm-hygiene-check: Read-only audit of your CRM opportunities for missing fields, sta (file: r14/crm-hygiene-check/SKILL.md)
- sales:customer-health: Health check on a customer account and QBR-ready prep - relations (file: r14/customer-health/SKILL.md)
- sales:customer-voice: Surface what customers are actually saying - direct attributed  (file: r14/customer-voice/SKILL.md)
- sales:daily-briefing: Morning rundown - today's meetings with account context, opps c (file: r14/daily-briefing/SKILL.md)
- sales:deal-advance-gap: Forward-looking gap check on one opportunity - exactly what is  (file: r14/deal-advance-gap/SKILL.md)
- sales:deal-review: Deep-dive on a single opportunity - signal-adjusted health score, (file: r14/deal-review/SKILL.md)
- sales:deal-signals: Proactive watch over your book - deals gone quiet, close dates  (file: r14/deal-signals/SKILL.md)
- sales:deal-slip-scenario: Model what happens to your number if a deal slips, shrinks, or  (file: r14/deal-slip-scenario/SKILL.md)
- sales:draft-outreach: Draft a personalized outreach email or multi-touch sequence to  (file: r14/draft-outreach/SKILL.md)
- sales:end-of-day: The closing beat of the day - every call processed or explicitl (file: r14/end-of-day/SKILL.md)
- sales:expansion-whitespace: Find the expansion whitespace in an account or a book - what th (file: r14/expansion-whitespace/SKILL.md)
- sales:forecast: Generate the commit / best-case / pipeline narrative for a fore (file: r14/forecast/SKILL.md)
- sales:handle-objection: Work through a live objection or competitive threat - what's re (file: r14/handle-objection/SKILL.md)
- sales:inbox-sweep: Batch-process unread customer emails - classify, prioritize,  (file: r14/inbox-sweep/SKILL.md)
- sales:lead-triage: Score and route an inbound lead, or rank a backlog of leads,  (file: r14/lead-triage/SKILL.md)
- sales:log-activity: Log a call, meeting, or email exchange to the CRM after the fac (file: r14/log-activity/SKILL.md)
- sales:pipeline-review: Stage-by-stage pipeline health check - coverage, aging, conve (file: r14/pipeline-review/SKILL.md)
- sales:renewal-radar: Upcoming renewals with timing, risk, and uplift potential - a (file: r14/renewal-radar/SKILL.md)
- sales:rep-context: Leader's prep on a single rep before a 1:1 - their pipeline,  (file: r14/rep-context/SKILL.md)
- sales:route-lead: Decide who owns an unrouted lead or opportunity and manage the  (file: r14/route-lead/SKILL.md)
- sales:schedule-meeting: Find a time, draft the invite, and book the meeting on Google C (file: r14/schedule-meeting/SKILL.md)
- sales:setup: First-run setup - checks which tools are connected, shows wha (file: r14/setup/SKILL.md)
- sales:stakeholder-map: Map the people in a deal or account - roles, influence, senti (file: r14/stakeholder-map/SKILL.md)
- sales:team-pipeline: Leader view - roll up a team's pipeline by rep and stage, fla (file: r14/team-pipeline/SKILL.md)
- sales:update-opportunity: Guided updates to an opportunity - push the stage, move the clo (file: r14/update-opportunity/SKILL.md)
- sales:weekly-wrap: End-of-week summary for a rep or leader - what closed, what m (file: r14/weekly-wrap/SKILL.md)
- sales:win-loss-review: Analyze recently closed opportunities to find patterns in wha (file: r14/win-loss-review/SKILL.md)
- security-audit: Security guidance and vulnerability review for codebases, APIs (file: r0/security-audit/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction a (file: r26/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Heming (file: r26/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full r (file: r26/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal  (file: r26/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose pr (file: r26/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new (file: r26/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching, fixi (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (inclu (file: r19/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use (file: r19/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, visuali (file: r23/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the C (file: r23/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r20/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r27/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r20/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r27/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r20/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r27/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r20/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r27/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r20/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r27/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing su (file: r20/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing su (file: r27/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r20/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r27/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks  (file: r20/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks  (file: r27/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r20/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r27/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing imp (file: r20/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing imp (file: r27/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from curren (file: r20/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from curren (file: r27/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find an (file: r20/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find an (file: r27/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r20/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r27/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, (file: r20/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, (file: r27/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r20/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r27/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build featur (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz your (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a thi (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r22/template-creator/26.1105.12137/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Codin (file: r0/vibe-research-workflow/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an anima (file: r21/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in Cha (file: r21/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in C (file: r21/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing ski (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is restricted.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/Documents/GitHub/labs/cpp-labs`, `/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-11-07T05:17:39Z

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

## developer · 2026-11-07T05:17:39Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-07T05:17:39Z

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
  <cwd>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs</cwd>
  <shell>zsh</shell>
  <current_date>2026-11-07</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs</root><root>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs</path></entry><entry access="write"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-07T05:17:39Z

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


## user · 2026-11-07T05:17:39Z

这道题我想创建一个字典用来保存每种颜色的次数 cpp中有这种写法吗
[@1004.cpp](file:///Users/oyamahappa/Documents/GitHub/labs/cpp-labs/HDOJ/1000-1010/1004.cpp)
[@ai-chat-attachment-6933571724316854898.png](file:///var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T/ai-chat-attachment-6933571724316854898.png)

## assistant · 2026-11-07T05:17:45Z

我先看一下 `1004.cpp`，结合你当前的代码说明怎么统计颜色次数。

## tool · 2026-11-07T05:17:48Z


Script completed
Wall time 0.2 seconds
Output:

---
name: using-superpowers
description: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions
---

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, ignore this skill.
</SUBAGENT-STOP>

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. You cannot rationalize your way out of this.
</EXTREMELY-IMPORTANT>

## The Rule

**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.

**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.

Then announce "Using [skill] to [purpose]" and follow the skill exactly. If it has a checklist, create a todo per item.

## Skill Priority

When multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.

- "Let's build X" → superpowers:brainstorming first, then implementation skills.
- "Fix this bug" → superpowers:systematic-debugging first, then domain skills.

## Red Flags

These thoughts mean STOP—you're rationalizing:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "I can check git/files quickly" | Files lack conversation context. Check for skills. |
| "Let me gather information first" | Skills tell you HOW to gather information. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |
| "This doesn't count as a task" | Action = task. Check for skills. |
| "The skill is overkill" | Simple things become complex. Use it. |
| "I'll just do this one thing first" | Check BEFORE doing anything. |
| "This feels productive" | Undisciplined action wastes time. Skills prevent this. |
| "I know what that means" | Knowing the concept ≠ using the skill. Invoke it. |

## Platform Adaptation

If your harness appears here, read its reference file for special instructions:

- Claude Code: `references/claude-code-tools.md`
- Codex: `references/codex-tools.md`
- Pi: `references/pi-tools.md`
- Antigravity: `references/antigravity-tools.md`
- Hermes Agent: `references/hermes-tools.md`
- Muse: `references/muse-tools.md`

## User Instructions

User instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.

{"i":0,"status":"fulfilled","value":{"chunk_id":"d4657a","wall_time_seconds":0.000006583,"exit_code":0,"original_token_count":327,"output":"//\n// Created by OyamaHappa on 2026/11/7.\n//\n// Let the Balloon Rise\n// Time Limit: 2000/1000 MS (Java/Others)    Memory Limit: 65536/32768 K (Java/Others)\n// Total Submission(s): 212148    Accepted Submission(s): 86458\n//\n//\n// Problem Description\n// Contest time again! How excited it is to see balloons floating around. But to tell you a secret, the judges' favorite time is guessing the most popular problem. When the contest is over, they will count the balloons of each color and find the result.\n//\n// This year, they decide to leave this lovely job to you.\n//\n//\n// Input\n// Input contains multiple test cases. Each test case starts with a number N (0 < N <= 1000) -- the total number of balloons distributed. The next N lines contain one color each. The color of a balloon is a string of up to 15 lower-case letters.\n//\n// A test case with N = 0 terminates the input and this test case is not to be processed.\n//\n//\n// Output\n// For each case, print the color of balloon for the most popular problem on a single line. It is guaranteed that there is a unique solution for each test case.\n//\n#include <iostream>\nusing namespace std;\n\nint main()\n{\n    int n=0;\n    cin>>n;\n\n    for (int i=0;i<n;i++){\n        string color;\n        cin>>color;\n        // Process the color input\n\n\n\n    }\n    return 0;\n}"}}
{"i":1,"status":"fulfilled","value":{"chunk_id":"edd35d","wall_time_seconds":0.000012875,"exit_code":0,"original_token_count":22,"output":"memory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\n"}}

## tool · 2026-11-07T05:17:56Z


Script completed
Wall time 0.1 seconds
Output:

## Subagent dispatch requires multi-agent support

Add to your Codex config (`~/.codex/config.toml`):

```toml
[features]
multi_agent = true
```

This enables the multi-agent tools that skills like
`dispatching-parallel-agents` and `subagent-driven-development` use.
Which tools you get depends on the multi-agent version your model
preset selects (current presets run V2; older ones run V1). Trust your
actual tool list over any table — including this one — when they
disagree.

- **Spawning:** give children a clean context with
  `spawn_agent {fork_turns: "none"}`; the default `"all"` copies your
  entire transcript into the child. On Codex 0.145+, role files under
  `~/.codex/agents/` attach to isolated forks via `agent_type`.
  Full-history forks accept `model` and `reasoning_effort` overrides
  (only `agent_type` is refused there) — isolated forks are the SDD
  default for context hygiene, not because overrides require them.
- **Fix rounds:** resume the implementer with `followup_task` — it
  delivers your message, triggers a turn, and transparently reloads a
  child the harness evicted. Never dispatch a fresh implementer on the
  theory that a spawned agent cannot be messaged again; on V2 it
  always can.
- **Lifecycle:** V2 has no `close_agent`. Finished children are
  evicted automatically when slots are needed; leaving them unclosed
  costs nothing. Only V1 sessions have `close_agent` — there, close
  reviewers when their review returns, and close each implementer
  after its task's review passes.
- **Model names:** never copy a model name from a skill, table, or old
  session into `spawn_agent` without checking it against your current
  spawn allowlist — V2 accepts only V2-capable presets and hard-errors
  on the rest.

## Waiting on children

`wait_agent` is an event subscription, not a poll: a long wait wakes
the moment a child produces mailbox activity, with the same latency as
a short one. Short-timeout polling buys nothing and costs a tool call —
and a context rebill — per poll. In measured sessions, roughly
two-thirds of all wait calls were short polls that timed out.

- While you still have local work, do not wait at all. A completed
  child's final answer is pushed into your mailbox and arrives with
  your next turn.
- When you are genuinely idle with children outstanding, wait in
  bounded stretches: `wait_agent` with `timeout_ms` 300000-600000
  (5-10 minutes). After each stretch — wake or timeout — post one
  status line, run `list_agents`, and chase any child that finished
  without reporting. Never stack polls shorter than five minutes; the
  event subscription wakes a bounded stretch just as fast as a short
  one.
- Completion mail cannot wake an idle controller (it is delivered
  without triggering a turn); covering that idle window is
  `wait_agent`'s only job. A stretch that times out with no activity
  is your cue to reconcile, not to shorten the next stretch.

## Model routing on spawns

Every `spawn_agent` you issue — including when you are yourself a
spawned child running a fan-out — sets `model` AND `reasoning_effort`
explicitly, per the Model Selection rules of the skill you are
executing. Setting `model` alone is a trap: the child's effort
silently resets to that model's default, not to yours.

Ask your human partner to add a machine-level backstop to
`~/.codex/config.toml` so any spawn that slips through still routes to
a deliberate tier instead of silently inheriting the session's most
expensive model:

```toml
[agents]
default_subagent_model = "<a mid-tier model from your spawn allowlist>"
default_subagent_reasoning_effort = "medium"
```

## Environment Detection

Skills that create worktrees or finish branches should detect their
environment with read-only git commands before proceeding:

```bash
GIT_DIR=$(cd "$(git rev-parse --git-dir)" 2>/dev/null && pwd -P)
GIT_COMMON=$(cd "$(git rev-parse --git-common-dir)" 2>/dev/null && pwd -P)
BRANCH=$(git branch --show-current)
```

- `GIT_DIR != GIT_COMMON` → already in a linked worktree (skip creation)
- `BRANCH` empty → detached HEAD (cannot branch/push/PR from sandbox)

See `using-git-worktrees` Step 0 and `finishing-a-development-branch`
Step 1 for how each skill uses these signals.

## Codex App Finishing

When the sandbox blocks branch/push operations (detached HEAD in an
externally managed worktree), the agent commits all work and informs
the user to use the App's native controls:

- **"Create branch"** — names the branch, then commit/push/PR via App UI
- **"Hand off to local"** — transfers work to the user's local checkout

The agent can still run tests, stage files, and output suggested branch
names, commit messages, and PR descriptions for the user to copy.


## assistant · 2026-11-07T05:18:01Z

有，可以用 C++ 的 **`map<string, int>`**，把颜色作为键、出现次数作为值。

先添加头文件：

```cpp
#include <map>
#include <string>
```

然后在你的 `for` 循环前创建字典，循环里统计：

```cpp
map<string, int> counts;

for (int i = 0; i < n; i++) {
    string color;
    cin >> color;
    counts[color]++;
}
```

**`counts[color]++` 就是给这个颜色的次数加一。** 如果颜色第一次出现，`map` 会自动创建对应项，将整数初始值设为 `0`，再递增为 `1`。

例如依次输入 `red`、`blue`、`red`，最终：

```cpp
counts["red"]   // 2
counts["blue"]  // 1
```

这道题有多组测试数据，每组都需要重新创建 `counts`，避免把上一组的次数累加进来。

未修改文件，示例未编译运行。

## user · 2026-11-07T06:55:18Z

或者说有没有更合适的写法
[@1004.cpp](file:///Users/oyamahappa/Documents/GitHub/labs/cpp-labs/HDOJ/1000-1010/1004.cpp)

## assistant · 2026-11-07T06:55:26Z

我再看一下当前代码，判断这题用哪种容器更合适。

## tool · 2026-11-07T06:55:26Z


Script completed
Wall time 0.1 seconds
Output:

//
// Created by OyamaHappa on 2026/11/7.
//
// Let the Balloon Rise
// Time Limit: 2000/1000 MS (Java/Others)    Memory Limit: 65536/32768 K (Java/Others)
// Total Submission(s): 212148    Accepted Submission(s): 86458
//
//
// Problem Description
// Contest time again! How excited it is to see balloons floating around. But to tell you a secret, the judges' favorite time is guessing the most popular problem. When the contest is over, they will count the balloons of each color and find the result.
//
// This year, they decide to leave this lovely job to you.
//
//
// Input
// Input contains multiple test cases. Each test case starts with a number N (0 < N <= 1000) -- the total number of balloons distributed. The next N lines contain one color each. The color of a balloon is a string of up to 15 lower-case letters.
//
// A test case with N = 0 terminates the input and this test case is not to be processed.
//
//
// Output
// For each case, print the color of balloon for the most popular problem on a single line. It is guaranteed that there is a unique solution for each test case.
//
#include <iostream>
using namespace std;

int main()
{
    int n=0;
    cin>>n;

    for (int i=0;i<n;i++){
        string color;
        cin>>color;
        // Process the color input



    }
    return 0;
}

## assistant · 2026-11-07T06:55:32Z

这题更适合用 **`unordered_map<string, int>`**：你只需要按颜色统计次数，不需要让颜色按字典序排列。

- `map`：键有序，查找和更新是 \(O(\log k)\)。
- `unordered_map`：键无序，查找和更新平均是 \(O(1)\)。

这里 \(k\) 是不同颜色的数量。这题最多 1000 个气球，两种都够用。

还可以**边统计，边记录出现次数最多的颜色**，这样不用最后再遍历字典：

```cpp
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;

int main()
{
    int n;
    while (cin >> n && n != 0) {
        unordered_map<string, int> counts;
        string answer;
        int maxCount = 0;

        for (int i = 0; i < n; i++) {
            string color;
            cin >> color;

            int count = ++counts[color];
            if (count > maxCount) {
                maxCount = count;
                answer = color;
            }
        }

        cout << answer << '\n';
    }
    return 0;
}
```

`++counts[color]` 会先递增，再返回更新后的次数。外层 `while` 处理多组输入，读到 `0` 就结束；每组的字典都会重新创建。

未修改文件，示例未编译运行；`unordered_map` 需要 C++11 或更新标准。

## user · 2026-11-07T07:23:45Z

在C++primerPlus第几章第几节有讲
[@1004.cpp](file:///Users/oyamahappa/Documents/GitHub/labs/cpp-labs/HDOJ/1000-1010/1004.cpp)

## assistant · 2026-11-07T07:23:54Z

我查一下《C++ Primer Plus》的目录，确认 `map` 和 `unordered_map` 所在的小节；不同版本的编号可能有差异。

## tool · 2026-11-07T07:23:58Z


Script completed
Wall time 4.2 seconds
Output:

C++ Primer Plus：中文版（第六版） (https://book.sjtt.cc/details/169898020036159503)
citeturn0search0 [wordlim: 200] Published: 3.0 years ago; Crawled: last week; 13.3.1 开发Brass类和BrassPlus类 367 ... 16.3.2 可对矢量执行的操作 467 ... 16.4.4 概念、改进和模型 476 ... 16.4.5 无序关联容器（C++11） 488 ... G.4 无序关联容器（C++11） 625
第16章 string类和标准模板库 453
16.1 string类 454
16.1.1 构造字符串 454
16.1.2 string类输入 457
16.1.3 使用字符串 458
16.1.4 string还提供了哪些功能 460
16.1.5 字符串种类 461
16.2 智能指针模板类 461
16.2.1 使用智能指针 462
16.2.2 有关智能指针的注意事项 464
16.2.3 unique_ptr为何优于auto_ptr 465
16.2.4 选择智能指针 466
16.3 标准模板库 466
16.3.1 模板类vector 467
16.3.2 可对矢量执行的操作 467
16.3.3 对矢量可执行的其他操作 469
16.3.4 基于范围的for循环（C++11） 471
16.4 泛型编程 471
16.4.1 为何使用迭代器 472
16.4.2 迭代器类型 474
16.4.3 迭代器层次结构 475
16.4.4 概念、改进和模型 476
16.4.5 容器种类 480
16.4.4 关联容器 485
16.4.5 无序关联容器（C++11） 488
16.5 函数对象 488
16.5.1 函数符概念 489
16.5.2 预定义的函数符 490
16.5.3 自适应函数符和函数适配器 491
16.6 算法 493
16.6.1 算法组 493
16.6.2 算法的通用特征 493
16.6.3 STL和string类 494
F.2.8 使用初始化列表的构造函数（C++11） 609
F.2.9 内存杂记 610
F.3 字符串存取 610
F.4 基本赋值 611
F.5 字符串搜索 611
F.5.1 find( )系列 611
F.5.2 rfind( )系列 612
F.5.3 find_first_of( )系列 612
F.5.4 find_last_of( )系列 612
F.5.5 find_first_not_of( )系列 612
F.5.6 find_last_not_of( )系列 613
F.6 比较方法和函数 613
F.7 字符串修改方法 614
F.7.1 用于追加和相加的方法 614
F.7.2 其他赋值方法 614
F.7.3 插入方法 614
F.7.4 清除方法 615
F.7.5 替换方法 615
F.7.6 其他修改方法：copy( )和swap( ) 615
F.8 输出和输入 616
附录G 标准模板库方法和函数 617
G.1 STL和C++11 618
G.1.1 新增的容器 618
G.1.2 对C++98容器所做的修改 618
G.2 大部分容器都有的成员 619
G.3 序列容器的其他成员 621
G.4 set和map的其他操作 623
G.4 无序关联容器（C++11） 625
G.5 STL函数 626
G.5.1 非修改式序列操作 626
G.5.2 修改式序列操作 629
G.5.3 排序和相关操作 635
G.5.4 数值运算 642
--------------------------------------------------------------------------------
C++ Primer Plus中文版第六6版 - 人民邮电出版社有限公司 (https://detail.youzan.com/show/goods?alias=3nhsnx55zm4n5&from_source=gbox_seo)
citeturn0search1 [wordlim: 200] Published: 6.4 years ago; Crawled: last month; 书名：C++ Primer Plus（第6版）中文版 ... 16.3.4 基于范围的for循环（C++11） 553
16.2.4 选择智能指针 545  
16.3 标准模板库 545  
16.3.1 模板类vector 546  
16.3.2 可对矢量执行的操作 547  
16.3.3 对矢量可执行的其他操作 550  
16.3.4 基于范围的for循环（C++11） 553  
16.4 泛型编程 553  
16.4.1 为何使用迭代器 553  
16.4.2 迭代器类型 556  
16.4.3 迭代器层次结构 557  
16.4.4 概念、改进和模型 558  
16.4.5 容器种类 562  
16.4.6 关联容器 568  
16.4.7 无序关联容器（C++11） 572  
16.5 函数对象 572  
16.5.1 函数符概念 573  
16.5.2 预定义的函数符 575  
16.5.3 自适应函数符和函数适配器 576  
16.6 算法 577  
16.6.1 算法组 578  
16.6.2 算法的通用特征 578  
16.6.3 STL和string类 579  
16.6.4 函数和容器方法 579  
16.6.5 使用STL 581  
16.7 其他库 583  
16.7.1 vector、valarray和array 583  
16.7.2 模板initializer_list（C++11） 586  
16.7.3 使用initializer_list 587  
16.8 总结 588  
16.9 复习题 589  
16.10 编程练习 590  
第 17章 输入、输出和文件 592  
17.1 C++输入和输出概述 592  
17.1.1 流和缓冲区 593  
17.1.2 流、缓冲区和iostream文件 594  
17.1.3 重定向 596  
17.2 使用cout进行输出 597  
17.2.1 重载的<  <运算符 597
--------------------------------------------------------------------------------
C++ Primer Plus 第6版 中文版(异步图书出品)-程序员书单-w3cschool (https://m.w3cschool.cn/booklist/booklist-ibpm3fj3.html)
citeturn0search2 [wordlim: 200] Published: 6.4 years ago; Crawled: last month; 16．3．4　基于范围的for循环（C++11）　553 ... 16．4．6　关联容器　568
16．1．4　string还提供了哪些功能　538
16．1．5　字符串种类　539
16．2　智能指针模板类　539
16．2．1　使用智能指针　540
16．2．2　有关智能指针的注意事项　542
16．2．3　unique_ptr为何优于auto_ptr　543
16．2．4　选择智能指针　545
16．3　标准模板库　545
16．3．1　模板类vector　546
16．3．2　可对矢量执行的操作　547
16．3．3　对矢量可执行的其他操作　550
16．3．4　基于范围的for循环（C++11）　553
16．4　泛型编程　553
16．4．1　为何使用迭代器　553
16．4．2　迭代器类型　556
16．4．3　迭代器层次结构　557
16．4．4　概念、改进和模型　558
16．4．5　容器种类　562
16．4．6　关联容器　568
16．4．7　无序关联容器（C++11）　572
16．5　函数对象　572
16．5．1　函数符概念　573
16．5．2　预定义的函数符　575
16．5．3　自适应函数符和函数适配器　576
16．6　算法　577
16．6．1　算法组　578
16．6．2　算法的通用特征　578
16．6．3　STL和string类　579
16．6．4　函数和容器方法　579
16．6．5　使用STL　581
16．7　其他库　583
16．7．1　vector、valarray和array　583
16．7．2　模板initializer_list（C++11）　586
16．7．3　使用initializer_list　587
16．8　总结　588
16．9　复习题　589
16．10　编程练习　590
第　17章 输入、输出和文件　592
--------------------------------------------------------------------------------
全国大中专教材网络采选系统 (https://www.aijiaocai.com/textbook/details?textbook_id=5974068)
citeturn0search3 [wordlim: 200] Published: 6.4 years ago; Crawled: last month; 以下为《C++ Primer Plus（第6版·中文版）》的配套数字资源，这些资源在您购买图书后将免费附送给您： ...   * 版次：1-16

C++ Primer Plus（第6版·中文版）

定价：￥118.00

作者： [美]史蒂芬·普拉达

出版时间：2020-07

最新印次日期：2024-8

出版社：人民邮电出版社

免费配套资源 查看资源链接

以下为《C++ Primer Plus（第6版·中文版）》的配套数字资源，这些资源在您购买图书后将免费附送给您：

基本信息 评价

  * 出版社：人民邮电出版社
  * ISBN：9787115521644
  * 版次：1-16
  * 本季征订号：49266466-9
  * 开本：16开
  * 出版时间：2020-07
  * 本科门类：工学
  * 本科专业类：计算机类
  * 职教专业大类：电子与信息大类
  * 适用专业：编程开发
  * 适用分级：本科 高职

作者简介

Stephen Prata曾在加利福尼亚的马林学院（肯特菲尔德）教授天文学、物理学和程序设计课程，现已退休。他在加州理工学院获得学士学位，在加州大学伯克利分校获得博士学位。他最早接触程序设计，是为了利用计算机给星团建模。--------------------------------------------------------------------------------
C++ Primer Plus：中文版（第六版） | PDF (https://www.scribd.com/document/814715257/C-Primer-Plus-%E4%B8%AD%E6%96%87%E7%89%88-%E7%AC%AC%E5%85%AD%E7%89%88)
citeturn0search4 [wordlim: 200] Published: 14.4 years ago; Crawled: 1.8 years ago; ## 可对矢量执行的操作 ............... ... 16.4.5 无序关联容器（C++11） ........ ... 16.5.2 预定义的函数符 .......................
695
第 18 章 探讨 C++新标准 .......................... 795
16.4.4 关联容器 ................................... 702 18.1 复习前面介绍过的 C++11 功能 ......... 795
16.4.5 无序关联容器（C++11） ........ 707 18.1.1 新类型 ....................................... 795
16.5 函数对象.............................................. 707 18.8.2 统一的初始化 ........................... 795
16.5.1 函数符概念 ............................... 707 18.1.3 声明 ........................................... 796
16.5.2 预定义的函数符 ....................... 710 18.1.4 智能指针 ................................... 798
16.5.3 自适应函数符和函数适配器 .... 711 18.1.5 异常规范方面的修改 ............... 798
16.6 算法 ..................................................... 713 18.1.6 作用域内枚举 ........................... 799
16.6.1 算法组....................................... 713 18.1.7 对类的修改 ............................... 799
16.6.2 算法的通用特征 ....................... --------------------------------------------------------------------------------
C++ Primer Plus(第6版)中文版(畅销30年C++必读经典教程全新升级，蔡学镛、孟岩、高博倾力推荐) – 东东购 | EasternEast (https://easterneast.com/product/5c238adb421aa9858779e606/)
citeturn0search5 [wordlim: 200] Crawled: 5 months ago; 16.3.2　可对矢量执行的操作　676 ... 16.4.5　无序关联容器(C 11)　707
16.2.2　有关智能指针的注意事项　670
16.2.3　unique_ptr为何优于auto_ptr　672
16.2.4　选择智能指针　673
16.3　标准模板库　674
16.3.1　模板类vector　675
16.3.2　可对矢量执行的操作　676
16.3.3　对矢量可执行的其他操作　680
16.3.4　基于范围的for循环(C 11)　684
16.4　泛型编程　684
16.4.1　为何使用迭代器　685
16.4.2　迭代器类型　688
16.4.3　迭代器层次结构　689
16.4.4　概念、改进和模型　690
16.4.5　容器种类　695
16.4.4　关联容器　702
16.4.5　无序关联容器(C 11)　707
16.5　函数对象　707
16.5.1　函数符概念　707
16.5.2　预定义的函数符　710
16.5.3　自适应函数符和函数适配器　711
16.6　算法　713
16.6.1　算法组　713
16.6.2　算法的通用特征　714
16.6.3　STL和string类　715
16.6.4　函数和容器方法　716
16.6.5　使用STL　717
16.7　其他库　720
16.7.1　vector、valarray和array　720
16.7.2　模板initializer_list(C 11)　724
16.7.3　使用initializer_list　725
16.8　总结　727
16.9　复习题　728
16.10　编程练习　728

--------------------------------------------------------------------------------
C++ Primer Plus（第6版）中文版 PDF下载 - java菜市场 (https://www.javaweb.shop/article/396.html)
citeturn0search6 [wordlim: 200] Published: 7.3 years ago; Crawled: last month; 16.3.2　可对矢量执行的操作　676 ... 16.4.5　无序关联容器(C++11)　707
16.2.1　使用智能指针　668

16.2.2　有关智能指针的注意事项　670

16.2.3　unique_ptr为何优于auto_ptr　672

16.2.4　选择智能指针　673

16.3　标准模板库　674

16.3.1　模板类vector　675

16.3.2　可对矢量执行的操作　676

16.3.3　对矢量可执行的其他操作　680

16.3.4　基于范围的for循环(C++11)　684

16.4　泛型编程　684

16.4.1　为何使用迭代器　685

16.4.2　迭代器类型　688

16.4.3　迭代器层次结构　689

16.4.4　概念、改进和模型　690

16.4.5　容器种类　695

16.4.4　关联容器　702

16.4.5　无序关联容器(C++11)　707

16.5　函数对象　707

16.5.1　函数符概念　707

16.5.2　预定义的函数符　710

16.5.3　自适应函数符和函数适配器　711

16.6　算法　713

16.6.1　算法组　713

16.6.2　算法的通用特征　714

16.6.3　STL和string类　715

16.6.4　函数和容器方法　716

16.6.5　使用STL　717

16.7　其他库　720

16.7.1　vector、valarray和array　720

16.7.2　模板initializer_list(C++11)　724

16.7.3　使用initializer_list　725

16.8　总结　727

16.9　复习题　728

16.10　编程练习　728

第17章　输入、输出和文件　731

17.1　C++输入和输出概述　731

17.1.1　流和缓冲区　732

17.1.2　流、缓冲区和iostream文件　733

17.1.3　重定向　735

17.2　使用cout进行输出　736

17.2.1　重载的<<运算符　736

--------------------------------------------------------------------------------
NeoDB Bog | C++ Primer Plus (https://neodb.social/book/1aM42SXUNMoJAVSNaBFMFS?lang=da)
citeturn0search7 [wordlim: 200] Published: 14.4 years ago; Crawled: last month; 16.3.4 基于范围的for循环（C++11） 471 ... 16.4.5 无序关联容器（C++11） 488
16.3.4 基于范围的for循环（C++11） 471
16.4 泛型编程 471
16.4.1 为何使用迭代器 472
16.4.2 迭代器类型 474
16.4.3 迭代器层次结构 475
16.4.4 概念、改进和模型 476
16.4.5 容器种类 480
16.4.4 关联容器 485
16.4.5 无序关联容器（C++11） 488
16.5 函数对象 488
16.5.1 函数符概念 489
16.5.2 预定义的函数符 490
16.5.3 自适应函数符和函数适配器 491
16.6 算法 493
16.6.1 算法组 493
16.6.2 算法的通用特征 493
16.6.3 STL和string类 494
16.6.4 函数和容器方法 494
16.6.5 使用STL 495
16.7 其他库 496
16.7.1 vector、valarray和array 497
16.7.2 模板initializer_list（C++11） 500
16.7.3 使用initializer_list 500
16.8 总结 501
16.9 复习题 502
16.10 编程练习 503
第17章 输入、输出和文件 505
17.1 C++输入和输出概述 506
17.1.1 流和缓冲区 506
17.1.2 流、缓冲区和iostream文件 508
17.1.3 重定向 510
17.2 使用cout进行输出 510
17.2.1 重载的<<运算符 511
17.2.2 其他ostream方法 512
17.2.3 刷新输出缓冲区 514
17.2.4 用cout进行格式化 515
17.3 使用cin进行输入 522
17.3.1 cin>>如何检查输入 523
17.3.2 流状态 524
17.3.3 其他istream类方法 527
17.3.4 其他istream方法 530
17.4 文件输入和输出 532
17.4.1 简单的文件I/O 532
--------------------------------------------------------------------------------
C++ Primer Plus 第六版 - redufa - 博客园 (https://www.cnblogs.com/redufa/p/18582493)
citeturn0search8 [wordlim: 200] Published: 1.9 years ago; Crawled: last month; 16.4.5 无序关联容器（C++11） 725 ... 16.5.2 预定义的函数符 728 ... G.4 无序关联容器（C++11） 902
16.4.3 迭代器层次结构 707
16.4.4 概念、改进和模型 708
16.4.5 容器种类 713
16.4.4 关联容器 720
16.4.5 无序关联容器（C++11） 725
16.5 函数对象 725
16.5.1 函数符概念 725
16.5.2 预定义的函数符 728
16.5.3 自适应函数符和函数适配器 729
16.6 算法 731
16.6.1 算法组 731
16.6.2 算法的通用特征 732
16.6.3 STL和string类 733
16.6.4 函数和容器方法 734
16.6.5 使用STL 735
16.7 其他库 738
16.7.1 vector、valarray和array 738
16.7.2 模板initializer_list(C++11) 742
16.7.3 使用initializer_list 743
16.8 总结 745
16.9 复习题 746
16.10 编程练习 746
第17章 输入、输出和文件 749
17.1 C++输入和输出概述 749
17.1.1 流和缓冲区 750
17.1.2 流、缓冲区和iostream文件 751
17.1.3 重定向 753
17.2 使用cout进行输出 754
17.2.1 重载的＜＜运算符 754
17.2.2 其他ostream方法 756
17.2.3 刷新输出缓冲区 758
17.2.4 用cout进行格式化 759
17.3 使用cin进行输入 771
17.3.1 cin＞＞如何检查输入 772
17.3.2 流状态 774
17.3.3 其他istream类方法 777
17.3.4 其他istream方法 782
17.4 文件输入和输出 786
17.4.1 简单的文件I/O 786
17.4.2 流状态检查和is_open() 788
--------------------------------------------------------------------------------
📘 第 16 章：string 类和标准模板库 (https://liazun.com/c%2B%2B-primer-plus/cpp16)
citeturn0search9 [wordlim: 200] Published: 2 months ago; Crawled: last month; description  | Stephen Prata《C++ Primer Plus》6th · Chapter 16 — 从 string 与智能指针走进 STL，掌握容器、迭代器、函数对象与泛型编程思想 ... 本章的重头戏是 STL（标准模板库）——C++ 里最常用的一套”容器 + 迭代器 + 算法”组合拳，它体现的泛型编程思想将贯穿你后续的 C++ 生涯。

  * # 📘 第 16 章：string 类和标准模板库

Properties 2
description  | Stephen Prata《C++ Primer Plus》6th · Chapter 16 — 从 string 与智能指针走进 STL，掌握容器、迭代器、函数对象与泛型编程思想
tags  | c++-primer-plus

2026年9月06日28分钟阅读

> 这一章在干嘛？
> 
> 前面各章你已经用过 `string`，这一章把它彻底讲透：构造、输入、查找、容量。接着介绍三个”会自己删内存”的智能指针，解决 `new`/`delete` 配对的老大难问题。本章的重头戏是 STL（标准模板库）——C++ 里最常用的一套”容器 + 迭代器 + 算法”组合拳，它体现的泛型编程思想将贯穿你后续的 C++ 生涯。最后补上 C++11 的 `initializer_list`。

16.1 string 类详解

16.2 智能指针模板类

16.3 STL 与 vector

16.4 迭代器与泛型编程

16.5 容器大点兵

16.6 函数对象

16.7 STL 算法

16.8 vector、valarray 与 array
--------------------------------------------------------------------------------
《C++ Primer Plus（第6版）中文版》电子书在线阅读-〖美〗Stephen Prata-得到APP (https://www.dedao.cn/ebook/detail?id=ORa2P4NNLqmQPG2178z5gvkDndlOxWyj4l3ajK6BEVXYRrJpA9M4oybeZpqAKQgj)
citeturn0search10 [wordlim: 200] Published: 14.4 years ago; Crawled: last month;   * 16.4.7 无序关联容器（C++11） ...   * 16.5.2 预定义的函数符
  * 16.4.6 关联容器
  * 16.4.7 无序关联容器（C++11）
  * 16.5 函数对象
  * 16.5.1 函数符概念
  * 16.5.2 预定义的函数符
  * 16.5.3 自适应函数符和函数适配器
  * 16.6 算法
  * 16.6.1 算法组
  * 16.6.2 算法的通用特征
  * 16.6.3 STL和string类
  * 16.6.4 函数和容器方法
  * 16.6.5 使用STL
  * 16.7 其他库
  * 16.7.1 vector、valarray和array
  * 16.7.2 模板initializer_list（C++11）
  * 16.7.3 使用initializer_list
  * 16.8 总结
  * 16.9 复习题
  * 16.10 编程练习
  * 第17章 输入、输出和文件
  * 17.1 C++输入和输出概述
  * 17.1.1 流和缓冲区
  * 17.1.2 流、缓冲区和iostream文件
  * 17.1.3 重定向
  * 17.2 使用cout进行输出
  * 17.2.1 重载的<<运算符
  * 17.2.2 其他ostream方法
  * 17.2.3 刷新输出缓冲区
  * 17.2.4 用cout进行格式化
  * 17.3 使用cin进行输入
  * 17.3.1 cin>>如何检查输入
  * 17.3.2 流状态
  * 17.3.3 其他istream类方法
  * 17.3.4 其他istream方法
  * 17.4 文件输入和输出
  * 17.4.1 简单的文件I/O
  * 17.4.2 流状态检查和is_open( )
  * 17.4.3 打开多个文件
  * 17.4.4 命令行处理技术
  * 17.4.5 文件模式
  * 17.4.6 随机存取
  * 17.5 内核格式化
  * 17.6 总结
  * 17.7 复习题
  * 17.8 编程练习
--------------------------------------------------------------------------------
c++ primer plus - Powered by MinDoc (https://morninglu.cn/docs/rd/cpp_primer_plus)
citeturn0search11 [wordlim: 200] Published: 7 months ago; Crawled: 2 months ago; # c++ primer plus ... 存入容器内的元素必须是可默认构造、可以拷贝构造的、可赋值的、可比较的(关联式容器) ... 无序关联容器，内部是hash
##### 12.内存职责划分 (涉及:默认构造 拷贝构造 赋值 析构 移动构造/赋值)

  0. 关于对象中有对象的嵌套问题，包括继承和组合 (示例519-522页)
  1. 当A类和B类中都有动态内存分配时
    1. 继承
1.构造和拷贝构造使用初始化链表先调用父类对应的构造函数
2.子类的赋值需要使用父类的作用域显示的调用父类的赋值
3.析构会自动完成所以在析构函数中子类只需要管好自己的动态内存就好
    2. 组合
1.构造和拷贝构造使用初始化链表先初始化成员对象
2.赋值不用加作用域直接调用
3.析构需要手动调用
  2. 如果B类没有动态内存分配则都可以使用编译器提供的默认函数(只有构造还是需要使用初始化链表)，其他函数编译器提供的默认函数会自动调用A类的对应方法

#### 7.STL

###### 1.杂

  1. stl的算法都是[ )左闭右开的区间
  2. 存入容器内的元素必须是可默认构造、可以拷贝构造的、可赋值的、可比较的(关联式容器)

###### 2.概念

  1. 容器、迭代器、算法、仿函数、适配器、配置器
  2. 迭代器提供能够遍历容器的对象，是广义的指针
  3. 为什么要使用迭代器，是使得算法独立于容器
  4. 迭代器分为输入输出/正向/双向/随机访问

###### 3.容器的分类

  1. 序列容器
vector: 在尾部插入O(1) 头部插入O(n)，衍生类型stack(栈)、priorityqueue_(排序了的vector)
deque: 相比vector多了个中控器，头插入也是O(1)，衍生类型queue(队列)
list: 不提供随机迭代器，衍生类型forward_list只支持正向迭代器
array: 非stl容器，因为长度固定，但是可以使用stl的部分算法
  2. 关联容器 key value类型，通过key找value，内部结构是某种树
set，multiset: key和value相同
map，multimap: key和value不相同
  3. 无序关联容器，内部是hash
unorderedset_，unorderedmultiset_: key和value相同
unorderedmap_，unorderedmultimap_: key和value不相同



## tool · 2026-11-07T07:24:07Z


Script completed
Wall time 3.1 seconds
Output:

C++ Primer Plus中文版第六6版 - 人民邮电出版社有限公司 (https://detail.youzan.com/show/goods?alias=3nhsnx55zm4n5&from_source=gbox_seo)
citeturn1view0 [wordlim: 200] Crawled: today; Content type: text/html; Source: open({"ref_id":"https://detail.youzan.com/show/goods?alias=3nhsnx55zm4n5&from_source=gbox_seo","lineno":null}); Total lines: 634
L0: 人民邮电出版社有限公司 微店铺首页
L1: 
L2:   * |
L3:   * 【0†最新商品】
L4:   * |
L5:   * 【1†店铺笔记】
L6: 
L7: 【2†Image: 人民邮电出版社有限公司店铺主页二维码†h5.youzan.com】
L8: 
L9: 人民邮电出版社有限公司 （ 微信认证 ）
L10:     人民邮电出版社微店，为您提供最全面，最专业的一站式购书服务
L11: 微信扫描二维码，访问我们的微信店铺
L12:     你可以使用微信联系我们，随时随地的购物、客服咨询、查询订单和物流...
L13: # C++ Primer Plus中文版第六6版
L14: 
L15: ￥88.50
L16: 
L17: 运费：  | ¥ 0.00-20.00
L18: 
L19: 立即购买
L20: 
L21: 支付：
L22:     微信支付 银行卡 支付宝
L23: 
L24: 【3†Image: C++ Primer Plus中文版第六6版 商品图0†img01.yzcdn.cn】
L25: 
L26: 【4†Image: C++ Primer Plus中文版第六6版 商品图1†img01.yzcdn.cn】
L27: 
L28: 【5†Image: C++ Primer Plus中文版第六6版 商品图2†img01.yzcdn.cn】
L29: 
L30: 【6†Image: C++ Primer Plus中文版第六6版 商品图3†img01.yzcdn.cn】
L31: 
L32: 【7†Image: C++ Primer Plus中文版第六6版 商品图4†img01.yzcdn.cn】
L33: 
L34: 【8†Image: C++ Primer Plus中文版第六6版 商品图5†img01.yzcdn.cn】
L35: 
L36: 【9†Image: C++ Primer Plus中文版第六6版 商品图6†img01.yzcdn.cn】
L37: 【10†Image: C++ Primer Plus中文版第六6版 商品图7†img01.yzcdn.cn】
L38: 
L39: 【11†Image: C++ Primer Plus中文版第六6版 商品图8†img01.yzcdn.cn】
L40: 
L41: 【12†Image: C++ Primer Plus中文版第六6版 商品图9†img01.yzcdn.cn】
L42: 【13†Image: C++ Primer Plus中文版第六6版 商品缩略图0†img01.yzcdn.cn】 【14†Image: C++ Primer Plus中文版第六6版 商品缩略图1†img01.yzcdn.cn】 【15†Image: C++ Primer Plus中文版第六6版 商品缩略图2†img01.yzcdn.cn】 【16†Image: C++ Primer Plus中文版第六6版 商品缩略图3†img01.yzcdn.cn】 【17†Image: C++ Primer Plus中文版第六6版 商品缩略图4†img01.yzcdn.cn】 【18†Image: C++ Primer Plus中文版第六6版 商品缩略图5†img01.yzcdn.cn】 【19†Image: C++ Primer Plus中文版第六6版 商品缩略图6†img01.yzcdn.cn】 【20†Image: C++ Primer Plus中文版第六6版 商品缩略图7†img01.yzcdn.cn】 【21†Image: C++ Primer Plus中文版第六6版 商品缩略图8†img01.yzcdn.cn】 【22†Image: C++ Primer Plus中文版第六6版 商品缩略图9†img01.yzcdn.cn】
L43: ## 商品详情
L44: 书名：C++ Primer Plus（第6版）中文版
L45: 定价：118.0
L46: ISBN：9787115521644
L47: 作者：史蒂芬·普拉达
L48: 版次：第1版
L49: 出版时间：2020-07
L50: 【23†Image†img01.yzcdn.cn】内容提要：
L51: C++是在 C 语言基础上开发的一种集面向对象编程、泛型编程和过程化编程于一体的编程语言，是C语言的超集。本书是根据2003年的ISO/ANSI C++标准编写的，通过大量短小精悍的程序详细而全面地阐述了 C++的基本概念和技术，并专辟一章介绍了C++11新增的功能。 《C++ Primer Plus（第6版）中文版》分18章，分别介绍了C++程序的运行方式、基本数据类型、复合数据类型、循环和关系表达式、分支语句和逻辑运算符、函数重载和函数模板、内存模型和名称空间、类的设计和使用、多态、虚函数、动态内存分配、继承、代码重用、友元、异常处理技术、string类和标准模板库、输入/输出、C++11新增功能等内容。 《C++ Primer Plus（第6版）中文版》针对C++初学者，从C语言基础知识开始介绍，然后在此基础上详细阐述C++新增的特性，因此不要求读者有C语言方面的背景知识。《C++ Primer Plus（第6版）中文版》可作为高等院校教授C++课程的教材，也可供初学者自学C++时使用。
L52: 作者简介：
L53: Stephen Prata曾在加利福尼亚的马林学院（肯特菲尔德）教授天文学、物理学和程序设计课程，现已退休。他在加州理工学院获得学士学位，在加州大学伯克利分校获得博士学位。他*早接触程序设计，是为了利用计算机给星团建模。Stephen撰写和与他人合著了十几本书籍，其中包括C++ Primer Plus和Unix Primer Plus。
L54: 目录：
L55: 第 1章 预备知识 1
L56: 1.1 C++简介 1
L57: 1.2 C++简史 2
L58: 1.2.1 C语言 2
L59: 1.2.2 C语言编程原理 2
L60: 1.2.3 面向对象编程 3
L61: 1.2.4 C++和泛型编程 3
L62: 1.2.5 C++的起源 4
L63: 1.3 可移植性和标准 5
L64: 1.3.1 C++的发展 5
L65: 1.3.2 本书遵循的C++标准 6
L66: 1.4 程序创建的技巧 6
L67: 1.4.1 创建源代码文件 6
L68: 1.4.2 编译和链接 7
L69: 1.5 总结 10
L70: 第 2章 开始学习C++ 11
L71: 2.1 进入C++ 11
L72: 2.1.1 main( )函数 12
L73: 2.1.2 C++注释 14
L74: 2.1.3 C++预处理器和iostream文件 14
L75: 2.1.4 头文件名 15
L76: 2.1.5 名称空间 15
L77: 2.1.6 使用cout进行C++输出 16
L78: 2.1.7 C++源代码的格式化 17
L79: 2.2 C++语句 18
L80: 2.2.1 声明语句和变量 19
L81: 2.2.2 赋值语句 20
L82: 2.2.3 cout的新花样 20
L83: 2.3 其他C++语句 21
L84: 2.3.1 使用cin 21
L85: 2.3.2 使用cout进行拼接 21
L86: 2.3.3 类简介 22
L87: 2.4 函数 23
L88: 2.4.1 使用有返回值的函数 23
L89: 2.4.2 函数变体 25
L90: 2.4.3 用户定义的函数 26
L91: 2.4.4 用户定义的有返回值的函数 28
L92: 2.4.5 在多函数程序中使用using编译指令 29
L93: 2.5 总结 30
L94: 2.6 复习题 30
L95: 2.7 编程练习 30
L96: 第3章 处理数据 32
L97: 3.1 简单变量 32
L98: 3.1.1 变量名 33
L99: 3.1.2 整型 34
L100: 3.1.3 整型short、int、long和long long 34
L101: 3.1.4 无符号类型 37
L102: 3.1.5 选择整型类型 38
L103: 3.1.6 整型字面值 39
L104: 3.1.7 C++如何确定常量的类型 40
L105: 3.1.8 char类型：字符和小整数 41
L106: 3.1.9 bool类型 46
L107: 3.2 const限定符 46
L108: 3.3 浮点数 47
L109: 3.3.1 书写浮点数 47
L110: 3.3.2 浮点类型 48
L111: 3.3.3 浮点常量 49
L112: 3.3.4 浮点数的优缺点 49
L113: 3.4 C++算术运算符 50
L114: 3.4.1 运算符优先级和结合性 51
L115: 3.4.2 除法分支 51
L116: 3.4.3 求模运算符 52
L117: 3.4.4 类型转换 53
L118: 3.4.5 C++11中的auto声明 56
L119: 3.5 总结 57
L120: 3.6 复习题 57
L121: 3.7 编程练习 58
L122: 第4章 复合类型 59
L123: 4.1 数组 59
L124: 4.1.1 程序说明 61
L125: 4.1.2 数组的初始化规则 61
L126: 4.1.3 C++11数组初始化方法 62
L127: 4.2 字符串 62
L128: 4.2.1 拼接字符串常量 63
L129: 4.2.2 在数组中使用字符串 63
L130: 4.2.3 字符串输入 64
L131: 4.2.4 每次读取一行字符串输入 65
L132: 4.2.5 混合输入字符串和数字 67
L133: 4.3 string类简介 68
L134: 4.3.1 C++11字符串初始化 69
L135: 4.3.2 赋值、拼接和附加 69
L136: 4.3.3 string类的其他操作 70
L137: 4.3.4 string类I/O 71
L138: 4.3.5 其他形式的字符串字面值 72
L139: 4.4 结构简介 73
L140: 4.4.1 在程序中使用结构 74
L141: 4.4.2 C++11结构初始化 75
L142: 4.4.3 结构可以将string类作为成员吗 75
L143: 4.4.4 其他结构属性 76
L144: 4.4.5 结构数组 77
L145: 4.4.6 结构中的位字段 78
L146: 4.5 共用体 78
L147: 4.6 枚举 79
L148: 4.6.1 设置枚举量的值 80
L149: 4.6.2 枚举的取值范围 80
L150: 4.7 指针和自由存储空间 80
L151: 4.7.1 声明和初始化指针 82
L152: 4.7.2 指针的危险 84
L153: 4.7.3 指针和数字 84
L154: 4.7.4 使用new来分配内存 84
L155: 4.7.5 使用delete释放内存 86
L156: 4.7.6 使用new来创建动态数组 86
L157: 4.8 指针、数组和指针算术 88
L158: 4.8.1 程序说明 89
L159: 4.8.2 指针小结 90
L160: 4.8.3 指针和字符串 92
L161: 4.8.4 使用new创建动态结构 94
L162: 4.8.5 自动存储、静态存储和动态存储 96
L163: 4.9 类型组合 97
L164: 4.10 数组的替代品 99
L165: 4.10.1 模板类vector 99
L166: 4.10.2 模板类array（C++11） 99
L167: 4.10.3 比较数组、vector对象和array对象 99
L168: 4.11 总结 101
L169: 4.12 复习题 101
L170: 4.13 编程练习 102
L171: 第5章 循环和关系表达式 104
L172: 5.1 for循环 104
L173: 5.1.1 for循环的组成部分 105
L174: 5.1.2 回到for循环 109
L175: 5.1.3 修改步长 110
L176: 5.1.4 使用for循环访问字符串 110
L177: 5.1.5 递增运算符（++）和递减运算符（ ） 111
L178: 5.1.6 副作用和顺序点 112
L179: 5.1.7 前缀格式和后缀格式 112
L180: 5.1.8 递增/递减运算符和指针 112
L181: 5.1.9 组合赋值运算符 113
L182: 5.1.10 复合语句（语句块） 113
L183: 5.1.11 其他语法技巧——逗号运算符 115
L184: 5.1.12 关系表达式 116
L185: 5.1.13 赋值、比较和可能犯的错误 117
L186: 5.1.14 C-风格字符串的比较 118
L187: 5.1.15 比较string类字符串 120
L188: 5.2 while循环 120
L189: 5.2.1 for与while 121
L190: 5.2.2 等待一段时间：编写延时循环 123
L191: 5.3 do while循环 124
L192: 5.4 基于范围的for循环（C++11） 125
L193: 5.5 循环和文本输入 125
L194: 5.5.1 使用原始的cin进行输入 126
L195: 5.5.2 使用cin.get(char)进行补救 126
L196: 5.5.3 使用哪一个cin.get( ) 127
L197: 5.5.4 文件尾条件 128
L198: 5.5.5 另一个cin.get( )版本 129
L199: 5.6 嵌套循环和二维数组 131
L200: 5.6.1 初始化二维数组 132
L201: 5.6.2 使用二维数组 133
L202: 5.7 总结 134
L203: 5.8 复习题 134
L204: 5.9 编程练习 135
L205: 第6章 分支语句和逻辑运算符 137
L206: 6.1 if语句 137
L207: 6.1.1 if else语句 138
L208: 6.1.2 格式化if else语句 139
L209: 6.1.3 if else if else结构 140
L210: 6.2 逻辑表达式 141


## assistant · 2026-11-07T07:24:13Z

如果你用的是 **《C++ Primer Plus》第6版中文版**，相关内容在 **第16章《string类和标准模板库》→ 16.4 泛型编程**：

| 容器 | 对应小节 | 页码 |
|---|---|---|
| `map` | **16.4.6 关联容器** | 568 |
| `unordered_map` | **16.4.7 无序关联容器（C++11）** | 572 |

以上按[人民邮电出版社公布的目录](https://detail.youzan.com/show/goods?alias=3nhsnx55zm4n5)核实。

未核对你手中书籍的版本；页码可能不同，可以按小节标题查找。

## user · 2026-11-07T07:25:16Z

C++有哪些数据类型
[@1004.cpp](file:///Users/oyamahappa/Documents/GitHub/labs/cpp-labs/HDOJ/1000-1010/1004.cpp)

## assistant · 2026-11-07T07:25:27Z

C++ 的类型可以先分成 **基本类型**和**复合类型**来理解。

**1. 基本类型**

| 类别 | 常见类型 | 示例 | 用途 |
|---|---|---|---|
| 整数 | `short`、`int`、`long`、`long long` | `int count = 0;` | 保存数量、下标等整数 |
| 浮点数 | `float`、`double`、`long double` | `double price = 3.5;` | 保存带小数的数值 |
| 字符 | `char` | `char letter = 'a';` | 保存一个字符 |
| 布尔值 | `bool` | `bool found = true;` | 保存 `true` 或 `false` |
| 空类型 | `void` | `void print();` | 表示函数不返回值等 |
| 空指针类型 | `std::nullptr_t` | `std::nullptr_t p = nullptr;` | 表示 `nullptr` 的类型 |

整数还可以使用 `unsigned` 表示无符号，例如：

```cpp
unsigned int count = 10;
```

它只能保存非负整数。各整数类型的具体大小与实现有关，`int` 通常占 4 字节。

**2. 复合类型**

复合类型包括数组、指针、引用、函数、枚举，以及类和结构体等：

```cpp
int numbers[3] = {1, 2, 3};  // 数组
int* p = &numbers[0];        // 指针
int& ref = numbers[0];      // 引用

enum Color { red, blue };    // 枚举

struct Student {            // 结构体
    int age;
};
```

**3. 你刚接触的 `string`、`map` 属于哪一种？**

它们来自 C++ 标准库，属于类类型；`map`、`vector` 等由类模板提供。

| 类型写法 | 保存的内容 |
|---|---|
| `string` | 字符串 |
| `vector<int>` | 长度可以变化的整数序列 |
| `map<string, int>` | 按字符串键排序的“字符串 → 整数”映射 |
| `unordered_map<string, int>` | 使用哈希表保存的“字符串 → 整数”映射 |
| `set<int>` | 不重复、按顺序保存的整数集合 |

对应你这道题：

```cpp
int n = 0;                          // 气球数量
string color;                       // 颜色名称
unordered_map<string, int> counts;   // 每种颜色 → 出现次数
```

`string` 保存一个颜色名称，`counts` 保存多个颜色名称及其对应次数。

本次仅解释类型，未修改或运行代码。
