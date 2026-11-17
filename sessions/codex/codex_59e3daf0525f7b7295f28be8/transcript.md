# 使用 map 和 split 处理输入

来源：codex

项目：/Users/oyamahappa/Documents/GitHub/labs/py-labs

## developer · 2026-10-27T15:23:05Z

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



## developer · 2026-10-27T15:23:05Z

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
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.2/skills`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.2/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1025.11240/skills`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.2/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.12.4/skills`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.1/skills`
- `r27` = `/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.agents/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI-created bitm (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, settings, setup, trou (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped instructions and an (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list or a GitHub (file: r2/skill-installer/SKILL.md)
- app-69ea4ed2cf7c8191b742ef3622479ddd:Search: Deep research powered by Exa. Use for lead generation, literature reviews, (file: r15/app-69ea4ed2cf7c8191b742ef3622479ddd/4.0.1/skills/Search/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, translate (file: r1/apple-design/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, translate (file: r0/apple-design/SKILL.md)
- archify: Create polished, validated architecture, workflow, sequence, data-flow, and  (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Codex research, writing, manuscript review, study screening, and exper (file: r3/ars-codex/3.24.0/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Structures Benchmark and Evaluation papers using the five-pillar framework (file: r0/benchmark-paper-template/SKILL.md)
- bio-research:instrument-data-to-allotrope: Convert laboratory instrument output files (PDF, CSV, Excel, TXT) to Allotrop (file: r4/instrument-data-to-allotrope/SKILL.md)
- bio-research:nextflow-development: Run nf-core bioinformatics pipelines (rnaseq, sarek, atacseq) on sequencing d (file: r4/nextflow-development/SKILL.md)
- bio-research:scientific-problem-selection: This skill should be used when scientists need help with research problem sel (file: r4/scientific-problem-selection/SKILL.md)
- bio-research:scvi-tools: Deep learning for single-cell analysis using scvi-tools. This skill should be (file: r4/scvi-tools/SKILL.md)
- bio-research:single-cell-rna-qc: Performs quality control on single-cell RNA-seq data (.h5ad or .h5 files) usi (file: r4/single-cell-rna-qc/SKILL.md)
- bio-research:start: Set up your bio-research environment and explore available tools. Use when  (file: r4/start/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end brand-guide (file: r0/brandkit/SKILL.md)
- cli-anything: Use when the user wants Codex to build, refine, test, validate, or list CL (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Discover agent-native CLIs for professional software. Access the live cata (file: r0/cli-hub-meta-skill/SKILL.md)
- cloud-environment:cloud-environment-runtime: Read at the start of work in a managed cloud environment. Inspect network po (file: r15/cloud-environment/0.1.2/skills/runtime/SKILL.md)
- code-review: Review the changes since a fixed point (commit, branch, tag, or merge-base)  (file: r0/code-review/SKILL.md)
- code-search: Instructions for MCP code search tools. Use when you need to find files, te (file: r27/code-search/SKILL.md)
- codebase-design: Shared vocabulary for designing deep modules. Use when the user wants to des (file: r0/codebase-design/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准备最小可验证改动，经用户逐项确 (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Convert Word (.doc, .docx), PowerPoint (.ppt, .pptx), Excel (.xls, .xlsx), O (file: r1/convert-documents-to-markdown/SKILL.md)
- cowork-plugin-management:cowork-plugin-customizer: Customize a Claude Code plugin for a specific organization's tools and workfl (file: r5/cowork-plugin-customizer/SKILL.md)
- cowork-plugin-management:create-cowork-plugin: Guide users through creating a new plugin from scratch in a cowork session. U (file: r5/create-cowork-plugin/SKILL.md)
- customer-support:customer-escalation: Package an escalation for engineering, product, or leadership with full con (file: r6/customer-escalation/SKILL.md)
- customer-support:customer-research: Multi-source research on a customer question or topic with source attributi (file: r6/customer-research/SKILL.md)
- customer-support:draft-response: Draft a professional customer-facing response tailored to the situation and r (file: r6/draft-response/SKILL.md)
- customer-support:kb-article: Draft a knowledge base article from a resolved issue or common question. Use  (file: r6/kb-article/SKILL.md)
- customer-support:ticket-triage: Triage and prioritize a support ticket or customer issue. Use when a new ti (file: r6/ticket-triage/SKILL.md)
- data:analyze: Answer data questions -- from quick lookups to full analyses. Use when look (file: r7/analyze/SKILL.md)
- data:build-dashboard: Build an interactive HTML dashboard with charts, filters, and tables. Use w (file: r7/build-dashboard/SKILL.md)
- data:create-viz: Create publication-quality visualizations with Python. Use when turning query (file: r7/create-viz/SKILL.md)
- data:data-context-extractor: Generate or improve a company-specific data analysis skill by extracting trib (file: r7/data-context-extractor/SKILL.md)
- data:data-visualization: Create effective data visualizations with Python (matplotlib, seaborn, plotly (file: r7/data-visualization/SKILL.md)
- data:explore-data: Profile and explore a dataset to understand its shape, quality, and patterns. (file: r7/explore-data/SKILL.md)
- data:sql-queries: Write correct, performant SQL across all major data warehouse dialects (Sno (file: r7/sql-queries/SKILL.md)
- data:statistical-analysis: Apply statistical methods including descriptive stats, trend analysis, outlie (file: r7/statistical-analysis/SKILL.md)
- data:validate-data: QA an analysis before sharing -- methodology, accuracy, and bias checks. Us (file: r7/validate-data/SKILL.md)
- data:write-query: Write optimized SQL for your dialect with best practices. Use when translat (file: r7/write-query/SKILL.md)
- deep-research: Runs a deep, survey-grade literature investigation on a research topic: free (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for websites, d (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects depending on its exact b (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-driven version, (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diagnosis loop for hard bugs and performance regressions. Use when the user  (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Google Docs-targe (file: r21/documents/26.1025.11240/skills/documents/SKILL.md)
- domain-modeling: Build and sharpen a project's domain model. Use when discussing codebase ter (file: r0/domain-modeling/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable Draw.io files wit (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable draw.io dia (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it to open and oper (file: r1/ego-browser/SKILL.md)
- enterprise-search:digest: Generate a daily or weekly digest of activity across all connected sources.  (file: r8/digest/SKILL.md)
- enterprise-search:knowledge-synthesis: Combines search results from multiple sources into coherent, deduplicated  (file: r8/knowledge-synthesis/SKILL.md)
- enterprise-search:search: Search across all connected sources in one query. Trigger with "find that do (file: r8/search/SKILL.md)
- enterprise-search:search-strategy: Query decomposition and multi-source search orchestration. Breaks natural  (file: r8/search-strategy/SKILL.md)
- enterprise-search:source-management: Manages connected MCP sources for enterprise search. Detects available sou (file: r8/source-management/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用户运行 /evidence-r (file: r0/evidence-recap/SKILL.md)
- figure-designer: Advises on the design of the three core figures in a technical paper: the Mo (file: r0/figure-designer/SKILL.md)
- finance:audit-support: Support SOX 404 compliance with control testing methodology, sample selectio (file: r9/audit-support/SKILL.md)
- finance:close-management: Manage the month-end close process with task sequencing, dependencies, and (file: r9/close-management/SKILL.md)
- finance:financial-statements: Generate financial statements (income statement, balance sheet, cash flow) (file: r9/financial-statements/SKILL.md)
- finance:journal-entry: Prepare journal entries with proper debits, credits, and supporting detail.  (file: r9/journal-entry/SKILL.md)
- finance:journal-entry-prep: Prepare journal entries with proper debits, credits, and supporting docume (file: r9/journal-entry-prep/SKILL.md)
- finance:reconciliation: Reconcile accounts by comparing GL balances to subledgers, bank statements (file: r9/reconciliation/SKILL.md)
- finance:sox-testing: Generate SOX sample selections, testing workpapers, and control assessments. (file: r9/sox-testing/SKILL.md)
- finance:variance-analysis: Decompose financial variances into drivers with narrative explanations and w (file: r9/variance-analysis/SKILL.md)
- full-output-enforcement: Overrides default LLM truncation behavior. Enforces complete code generatio (file: r0/output-skill/SKILL.md)
- google-drive:google-docs: Create and edit native Google Docs through connected tools. (file: r16/google-docs/SKILL.md)
- google-drive:google-drive: Use connected Google Drive as the single entrypoint for Drive, Docs, Sheets, (file: r16/google-drive/SKILL.md)
- google-drive:google-drive-comments: Write, reply to, and resolve Google Drive comments on Docs, Sheets, Slides (file: r16/google-drive-comments/SKILL.md)
- google-drive:google-sheets: Analyze and edit connected Google Sheets with range precision. Use when th (file: r16/google-sheets/SKILL.md)
- google-drive:google-slides: Route Google Slides authoring requests and derive a design system from a n (file: r16/google-slides/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt template (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt template (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Elite UX/UI & Advanced GSAP Motion Engineer. Enforces Python-driven true ra (file: r0/gpt-tasteskill/SKILL.md)
- graphify: Use for any question about a codebase, its architecture, file relationship (file: r0/graphify/SKILL.md)
- great-resume: 中文求职经历提升技能：根据目标岗位把真实经历重组为岗位定位、简历要点、项目亮点和 HR 开场白；当用户输入“/great-resume”“我要酥化” (file: r0/great-resume/SKILL.md)
- grilling: Grill the user relentlessly about a plan, decision, or idea. Use when the  (file: r0/grilling/SKILL.md)
- gsap-core: Official GSAP skill for the core API — gsap.to(), from(), fromTo(), easing (file: r0/gsap-core/SKILL.md)
- gsap-frameworks: Official GSAP skill for Vue, Svelte, and other non-React frameworks — life (file: r0/gsap-frameworks/SKILL.md)
- gsap-performance: Official GSAP skill for performance — prefer transforms, avoid layout thrash (file: r0/gsap-performance/SKILL.md)
- gsap-plugins: Official GSAP skill for GSAP plugins — registration, ScrollToPlugin, ScrollS (file: r0/gsap-plugins/SKILL.md)
- gsap-react: Official GSAP skill for React — useGSAP hook, refs, gsap.context(), cleanup. (file: r0/gsap-react/SKILL.md)
- gsap-scrolltrigger: Official GSAP skill for ScrollTrigger — scroll-linked animations, pinning, s (file: r0/gsap-scrolltrigger/SKILL.md)
- gsap-timeline: Official GSAP skill for timelines — gsap.timeline(), position parameter, n (file: r0/gsap-timeline/SKILL.md)
- gsap-utils: Official GSAP skill for gsap.utils — clamp, mapRange, normalize, interpolate (file: r0/gsap-utils/SKILL.md)
- high-end-visual-design: Teaches the AI to design like a high-end agency. Defines the exact fonts,  (file: r0/soft-skill/SKILL.md)
- human-writing: 通用中文创作与改稿 Skill。用于知乎回答、论坛长帖、公众号文章、博客、评论、人物故事、历史叙事、新闻与行业解读、科普、教程、评测、个人叙事、小说 (file: r0/human-writing/SKILL.md)
- idea-evaluator: Evaluates a preliminary research idea against a five-dimension framework ( (file: r0/idea-evaluator/SKILL.md)
- image-to-code: Elite website image-to-code skill for Codex. For visually important web ta (file: r0/image-to-code-skill/SKILL.md)
- imagegen-frontend-mobile: Elite mobile app image-generation skill for creating premium, app-native s (file: r0/imagegen-frontend-mobile/SKILL.md)
- imagegen-frontend-web: Elite frontend image-direction skill for generating premium, conversion-awar (file: r0/imagegen-frontend-web/SKILL.md)
- industrial-brutalist-ui: Raw mechanical interfaces fusing Swiss typographic print with military termi (file: r0/brutalist-skill/SKILL.md)
- interview: 中文简历与目标岗位驱动的面试预测、模拟追问和复练技能：提取需要验证的经历 Claim，按面试轮次建立问题与评分契约，通过一次一问、证据反馈和弱项复练 (file: r0/interview/SKILL.md)
- intro-drafter: Drafts the Introduction prose for a technical paper, guided internally by a  (file: r0/intro-drafter/SKILL.md)
- job-apply: 中文求职申请自动填写技能：使用浏览器读取用户确认的简历资料，逐项填写招聘网站申请表并核对结果；当用户输入“/job-apply”、要求自动填简历或填 (file: r0/job-apply/SKILL.md)
- job-match: 中文岗位匹配分析技能：对照目标 JD 与用户已确认的简历、经历或主张—证据账本，区分已匹配、证据不足和真实缺口，生成可解释的投递建议与后续 skil (file: r0/job-match/SKILL.md)
- jupyter: Create, inspect, edit, and execute Jupyter .ipynb notebooks for data analys (file: r27/jupyter/SKILL.md)
- legal:brief: Generate contextual briefings for legal work — daily summary, topic researc (file: r10/brief/SKILL.md)
- legal:compliance-check: Run a compliance check on a proposed action, product feature, or business i (file: r10/compliance-check/SKILL.md)
- legal:legal-response: Generate a response to a common legal inquiry using configured templates, w (file: r10/legal-response/SKILL.md)
- legal:legal-risk-assessment: Assess and classify legal risks using a severity-by-likelihood framework with (file: r10/legal-risk-assessment/SKILL.md)
- legal:meeting-briefing: Prepare structured briefings for meetings with legal relevance and track re (file: r10/meeting-briefing/SKILL.md)
- legal:review-contract: Review a contract against your organization's negotiation playbook — flag d (file: r10/review-contract/SKILL.md)
- legal:signature-request: Prepare and route a document for e-signature — run a pre-signature checklis (file: r10/signature-request/SKILL.md)
- legal:triage-nda: Rapidly triage an incoming NDA and classify it as GREEN (standard approval) (file: r10/triage-nda/SKILL.md)
- legal:vendor-check: Check the status of existing agreements with a vendor across all connected  (file: r10/vendor-check/SKILL.md)
- make-resume: 中文可编辑简历制作技能：默认基于 ASu 单栏高密度技术简历模板，根据用户经历制作或复刻可编辑 HTML/PDF；用户也可以指定仓库内其他模板、本地 H (file: r0/make-resume/SKILL.md)
- marketing:brand-review: Review content against your brand voice, style guide, and messaging pillars (file: r11/brand-review/SKILL.md)
- marketing:campaign-plan: Generate a full campaign brief with objectives, audience, messaging, channel  (file: r11/campaign-plan/SKILL.md)
- marketing:competitive-brief: Research competitors and generate a positioning and messaging comparison with (file: r11/competitive-brief/SKILL.md)
- marketing:content-creation: Draft marketing content across channels — blog posts, social media, email (file: r11/content-creation/SKILL.md)
- marketing:draft-content: Draft blog posts, social media, email newsletters, landing pages, press r (file: r11/draft-content/SKILL.md)
- marketing:email-sequence: Design and draft multi-email sequences with full copy, timing, branching lo (file: r11/email-sequence/SKILL.md)
- marketing:performance-report: Build a marketing performance report with key metrics, trend analysis, wins (file: r11/performance-report/SKILL.md)
- marketing:seo-audit: Run a comprehensive SEO audit — keyword research, on-page analysis, content (file: r11/seo-audit/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, typographic co (file: r0/minimalist-skill/SKILL.md)
- notion:notion-database-designer: Turns scattered notes and recurring work into useful Notion trackers for r (file: r17/notion-database-designer/SKILL.md)
- notion:notion-meeting-intelligence: Prepares Notion meeting agendas, pre-reads, decision briefs, and follow-up a (file: r17/notion-meeting-intelligence/SKILL.md)
- notion:notion-research-documentation: Synthesizes Notion workspace evidence into cited answers, comparisons, brief (file: r17/notion-research-documentation/SKILL.md)
- notion:notion-setup: Sets up Notion after the user installs the Notion plugin or chooses Set u (file: r17/setup/SKILL.md)
- notion:notion-spec-to-implementation: Converts Notion product or technical specs into implementation plans, linked (file: r17/notion-spec-to-implementation/SKILL.md)
- notion:notion-weekly-project-digest: Produces evidence-based weekly project or team updates by comparing report (file: r17/notion-weekly-project-digest/SKILL.md)
- offer: 中文秋招求职进度管理技能：记录和更新投递、筛选、测评、面试、Offer、拒信及招聘邮件状态，生成可搜索的进度表；当用户输入“/offer”或要求管理 (file: r0/offer/SKILL.md)
- paper-polish: Polishes existing academic prose while preserving the author's meaning: gr (file: r0/paper-polish/SKILL.md)
- paper-writer: Drafts publishable paper prose from the author's own materials, from a sin (file: r0/paper-writer/SKILL.md)
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不阻塞主文件。交付后请确认须摘 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著录字段检索公布公告，通俗解 (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申请一起做、从零出交底和申请、 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包，须另点名才改文件。 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开。 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visual layout ma (file: r21/pdf/26.1025.11240/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions and depende (file: r15/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the task, and a  (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks under real  (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as a debt ledg (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the benchmark. O (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One-shot display (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, does it hold u (file: r23/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five dimensions: ma (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use for presentati (file: r21/presentations/26.1025.11240/skills/presentations/SKILL.md)
- product-management:competitive-brief: Create a competitive analysis brief for one or more competitors or a feature (file: r12/competitive-brief/SKILL.md)
- product-management:metrics-review: Review and analyze product metrics with trend analysis and actionable insi (file: r12/metrics-review/SKILL.md)
- product-management:product-brainstorming: Brainstorm product ideas, explore problem spaces, and challenge assumptions  (file: r12/product-brainstorming/SKILL.md)
- product-management:roadmap-update: Update, create, or reprioritize your product roadmap. Use when adding a ne (file: r12/roadmap-update/SKILL.md)
- product-management:sprint-planning: Plan a sprint — scope work, estimate capacity, set goals, and draft a spri (file: r12/sprint-planning/SKILL.md)
- product-management:stakeholder-update: Generate a stakeholder update tailored to audience and cadence. Use when w (file: r12/stakeholder-update/SKILL.md)
- product-management:synthesize-research: Synthesize user research from interviews, surveys, and feedback into structu (file: r12/synthesize-research/SKILL.md)
- product-management:write-spec: Write a feature spec or PRD from a problem statement or feature idea. Use  (file: r12/write-spec/SKILL.md)
- productivity:memory-management: Two-tier memory system that makes Claude a true workplace collaborator. De (file: r13/memory-management/SKILL.md)
- productivity:start: Initialize the productivity system and open the dashboard. Use when settin (file: r13/start/SKILL.md)
- productivity:task-management: Simple task management using a shared TASKS.md file. Reference this when t (file: r13/task-management/SKILL.md)
- productivity:update: Sync tasks and refresh memory from your current activity. Use when pulling n (file: r13/update/SKILL.md)
- project-guide: 中文项目导学、源码课程与项目面经技能：基于本地项目仓库、项目描述或技术材料，按需生成源码课程与理解题，或生成 导学-{简称}.md、面经-{简称}. (file: r0/project-guide/SKILL.md)
- prototype: Build a throwaway prototype to answer a design question. Use when the user w (file: r0/prototype/SKILL.md)
- python-tools: PyCharm environment tools. MUST be consulted before running ANY Python to (file: r27/python-tools/SKILL.md)
- rebuttal-guidance: Provides actionable peer-review rebuttal guidance (not full rebuttal prose)  (file: r0/rebuttal-guidance/SKILL.md)
- redesign-existing-projects: Upgrades existing websites and apps to premium quality. Audits current des (file: r0/redesign-skill/SKILL.md)
- research: Investigate a question against high-trust primary sources and capture the  (file: r0/research/SKILL.md)
- reverse-engineer-anything: Reverse engineer native, managed, Electron/JavaScript, packaged, firmware, a (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized reverse engineeri (file: r24/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sales:account-context: 360-degree view of an account - CRM data, recent email threads, docs, tra (file: r14/account-context/SKILL.md)
- sales:account-plan: Build or refresh a strategic account plan - current state, goals, stakehold (file: r14/account-plan/SKILL.md)
- sales:account-research: Research a target company and optionally a specific contact - company overv (file: r14/account-research/SKILL.md)
- sales:account-tiering: Score and tier a list of accounts (or your full book) against ICP fit and (file: r14/account-tiering/SKILL.md)
- sales:call-prep: Pre-call brief for an upcoming meeting - attendees, account history, prio (file: r14/call-prep/SKILL.md)
- sales:call-summary: Turn a call transcript or call notes into a customer follow-up email draft, (file: r14/call-summary/SKILL.md)
- sales:close-plan: Build the business case and mutual action plan for a deal - the why-buy/why (file: r14/close-plan/SKILL.md)
- sales:competitive-intelligence: Competitive analysis two ways - the in-deal play against a named competitor (file: r14/competitive-intelligence/SKILL.md)
- sales:create-an-asset: Build a customer deck, one-pager or leave-behind from your account data,  (file: r14/create-an-asset/SKILL.md)
- sales:crm-hygiene-check: Read-only audit of your CRM opportunities for missing fields, stale dates (file: r14/crm-hygiene-check/SKILL.md)
- sales:customer-health: Health check on a customer account and QBR-ready prep - relationship stre (file: r14/customer-health/SKILL.md)
- sales:customer-voice: Surface what customers are actually saying - direct attributed quotes on a  (file: r14/customer-voice/SKILL.md)
- sales:daily-briefing: Morning rundown - today's meetings with account context, opps closing soon  (file: r14/daily-briefing/SKILL.md)
- sales:deal-advance-gap: Forward-looking gap check on one opportunity - exactly what is missing to a (file: r14/deal-advance-gap/SKILL.md)
- sales:deal-review: Deep-dive on a single opportunity - signal-adjusted health score, risks,  (file: r14/deal-review/SKILL.md)
- sales:deal-signals: Proactive watch over your book - deals gone quiet, close dates slipping int (file: r14/deal-signals/SKILL.md)
- sales:deal-slip-scenario: Model what happens to your number if a deal slips, shrinks, or dies - quota (file: r14/deal-slip-scenario/SKILL.md)
- sales:draft-outreach: Draft a personalized outreach email or multi-touch sequence to a prospect,  (file: r14/draft-outreach/SKILL.md)
- sales:end-of-day: The closing beat of the day - every call processed or explicitly skipped, t (file: r14/end-of-day/SKILL.md)
- sales:expansion-whitespace: Find the expansion whitespace in an account or a book - what they own vs. w (file: r14/expansion-whitespace/SKILL.md)
- sales:forecast: Generate the commit / best-case / pipeline narrative for a forecast call or (file: r14/forecast/SKILL.md)
- sales:handle-objection: Work through a live objection or competitive threat - what's really being s (file: r14/handle-objection/SKILL.md)
- sales:inbox-sweep: Batch-process unread customer emails - classify, prioritize, and draft re (file: r14/inbox-sweep/SKILL.md)
- sales:lead-triage: Score and route an inbound lead, or rank a backlog of leads, against your (file: r14/lead-triage/SKILL.md)
- sales:log-activity: Log a call, meeting, or email exchange to the CRM after the fact as a compl (file: r14/log-activity/SKILL.md)
- sales:pipeline-review: Stage-by-stage pipeline health check - coverage, aging, conversion, and a (file: r14/pipeline-review/SKILL.md)
- sales:renewal-radar: Upcoming renewals with timing, risk, and uplift potential - and the renew (file: r14/renewal-radar/SKILL.md)
- sales:rep-context: Leader's prep on a single rep before a 1:1 - their pipeline, recent activ (file: r14/rep-context/SKILL.md)
- sales:route-lead: Decide who owns an unrouted lead or opportunity and manage the handoff - de (file: r14/route-lead/SKILL.md)
- sales:schedule-meeting: Find a time, draft the invite, and book the meeting on Google Calendar or O (file: r14/schedule-meeting/SKILL.md)
- sales:setup: First-run setup - checks which tools are connected, shows what's connecte (file: r14/setup/SKILL.md)
- sales:stakeholder-map: Map the people in a deal or account - roles, influence, sentiment, who's  (file: r14/stakeholder-map/SKILL.md)
- sales:team-pipeline: Leader view - roll up a team's pipeline by rep and stage, flag at-risk de (file: r14/team-pipeline/SKILL.md)
- sales:update-opportunity: Guided updates to an opportunity - push the stage, move the close date, set (file: r14/update-opportunity/SKILL.md)
- sales:weekly-wrap: End-of-week summary for a rep or leader - what closed, what moved, what s (file: r14/weekly-wrap/SKILL.md)
- sales:win-loss-review: Analyze recently closed opportunities to find patterns in what wins and w (file: r14/win-loss-review/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction and in profes (file: r25/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Hemingway manner,  (file: r25/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full rewrite. (file: r25/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal in-place pro (file: r25/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose prose without  (file: r25/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new prose. (file: r25/sepia-write/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (including a landi (file: r18/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use when the us (file: r18/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, visualize, or work  (file: r22/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the ChatGPT add-i (file: r22/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent-friendly DE (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, building co (file: r19/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, building co (file: r26/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner wants to (file: r19/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner wants to (file: r26/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without shared s (file: r19/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without shared s (file: r26/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as the imp (file: r19/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as the imp (file: r26/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need to deci (file: r19/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need to deci (file: r26/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing suggestions, e (file: r19/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing suggestions, e (file: r26/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before merging (file: r19/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before merging (file: r26/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in the curre (file: r19/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in the curre (file: r26/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavior, befo (file: r19/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavior, befo (file: r26/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing implementation  (file: r19/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing implementation  (file: r26/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current workspace  (file: r19/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current workspace  (file: r26/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and use skills (file: r19/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and use skills (file: r26/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, before commi (file: r19/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, before commi (file: r26/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, before touc (file: r19/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, before touc (file: r26/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifying skill (file: r19/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifying skill (file: r26/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build features or fix bu (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz yourself on what (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a thinking-templa (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template skill. Use wh (file: r21/template-creator/26.1025.11240/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Coding, Vibe Figu (file: r0/vibe-research-workflow/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through steps only  (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an animated v2 pet i (file: r20/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in ChatGPT Work mo (file: r20/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in ChatGPT Work  (file: r20/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing skills, or modi (file: r0/writing-for-agents/SKILL.md)
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

## developer · 2026-10-27T15:23:05Z

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

## developer · 2026-10-27T15:23:05Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-10-27T15:23:05Z

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
  <current_date>2026-10-27</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/GitHub/labs/py-labs</root><root>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs</path></entry><entry access="write"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-10-27T15:23:05Z

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

## user · 2026-10-27T15:23:05Z

输入的要求是同一行 用map split
[@7.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/work/2-261026/7.py)

## assistant · 2026-10-27T15:23:09Z

我会先查看 `7.py` 的输入方式，按你的要求改成同一行输入，并使用 `map` 和 `split`。

## tool · 2026-10-27T15:23:12Z


Script completed
Wall time 0.3 seconds
Output:

/Users/oyamahappa/Documents/GitHub/labs/py-labs
work/2-261026/7.py
docs/CHANGELOG.md
memory/agents.md
memory/plan.md
memory/verify.md
memory/progress.md
memory/gotchas.md

{"chunk_id":"a1fae5","wall_time_seconds":0.000007583,"exit_code":0,"original_token_count":798,"output":"---\nname: using-superpowers\ndescription: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions\n---\n\n<SUBAGENT-STOP>\nIf you were dispatched as a subagent to execute a specific task, ignore this skill.\n</SUBAGENT-STOP>\n\n<EXTREMELY-IMPORTANT>\nIf you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.\n\nIF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.\n\nThis is not negotiable. You cannot rationalize your way out of this.\n</EXTREMELY-IMPORTANT>\n\n## The Rule\n\n**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.\n\n**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.\n\nThen announce \"Using [skill] to [purpose]\" and follow the skill exactly. If it has a checklist, create a todo per item.\n\n## Skill Priority\n\nWhen multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.\n\n- \"Let's build X\" → superpowers:brainstorming first, then implementation skills.\n- \"Fix this bug\" → superpowers:systematic-debugging first, then domain skills.\n\n## Red Flags\n\nThese thoughts mean STOP—you're rationalizing:\n\n| Thought | Reality |\n|---------|---------|\n| \"This is just a simple question\" | Questions are tasks. Check for skills. |\n| \"I need more context first\" | Skill check comes BEFORE clarifying questions. |\n| \"Let me explore the codebase first\" | Skills tell you HOW to explore. Check first. |\n| \"I can check git/files quickly\" | Files lack conversation context. Check for skills. |\n| \"Let me gather information first\" | Skills tell you HOW to gather information. |\n| \"This doesn't need a formal skill\" | If a skill exists, use it. |\n| \"I remember this skill\" | Skills evolve. Read current version. |\n| \"This doesn't count as a task\" | Action = task. Check for skills. |\n| \"The skill is overkill\" | Simple things become complex. Use it. |\n| \"I'll just do this one thing first\" | Check BEFORE doing anything. |\n| \"This feels productive\" | Undisciplined action wastes time. Skills prevent this. |\n| \"I know what that means\" | Knowing the concept ≠ using the skill. Invoke it. |\n\n## Platform Adaptation\n\nIf your harness appears here, read its reference file for special instructions:\n\n- Claude Code: `references/claude-code-tools.md`\n- Codex: `references/codex-tools.md`\n- Pi: `references/pi-tools.md`\n- Antigravity: `references/antigravity-tools.md`\n- Hermes Agent: `references/hermes-tools.md`\n- Muse: `references/muse-tools.md`\n\n## User Instructions\n\nUser instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.\n"}
{"chunk_id":"6ef1bf","wall_time_seconds":0.000006542,"exit_code":0,"original_token_count":2864,"output":"---\nname: python-tools\ndescription: PyCharm environment tools. MUST be consulted before running ANY Python toolchain command (python, python3, pip, pip3, uv, conda, pytest, ruff, mypy, python -m <module>, etc.) — call get_python_environment first to get the executable and package manager that match PyCharm's configured SDK for the file's module. Also covers configuring an interpreter when none is set up.\nallowed-tools: execute_tool\n---\n\n# PyCharm Environment Tools\n\n> **Mandatory pre-flight:** before running ANY Python command — `python`, `python3`, `pip`, `pip3`, `uv`, `conda`, `pytest`, `ruff`, `mypy`, `python -m <module>`, or anything else that resolves a Python interpreter — call `get_python_environment` on a file inside the target module. Use the returned `executablePath` instead of a bare `python` / `python3`, and the returned `packageManager` to choose the correct install command. Skipping this step silently picks the wrong interpreter (system Python instead of the project's venv, an older minor version, missing packages) and corrupts the project's environment.\n\n> **If `get_python_environment` returns a non-null `noInterpreterConfigured` field, get a proper interpreter before running the Python command.** Branch on the field's content:\n> - Ends with `call configure_python_interpreter with the same --filePath.` → call `configure_python_interpreter`, then re-call `get_python_environment`. Run the Python command using the env info returned by the second call.\n> - Says `PyCharm expects this project to use <tool>, but <tool> is not installed.` (e.g. `uv`, `poetry`, `hatch`) → do NOT call `configure_python_interpreter`. Ask the user to install the named tool first, then re-call `get_python_environment`.\n> - Plain `No Python interpreter configured for: <path>.` (no extra suffix) → PyCharm has no automatic option, but the project also doesn't dictate a specific tool. Set up the env yourself with a sensible default (e.g. `python3 -m venv .venv` in the project root), then re-call `get_python_environment`. The new venv should be detected and the next response will suggest `configure_python_interpreter`; if it still returns plain \"no interpreter\" for some reason, use `.venv/bin/python` directly. Tell the user what you set up.\n>\n> For commands that aren't tied to a specific file (e.g. `pip install`, `pytest` at the project root, or a run configuration that doesn't expose a target file), pass any `.py` file inside the target module as `--filePath` — the interpreter is per-module, not per-file.\n\nTwo tools, used together:\n\n1. **`get_python_environment`** — always call this first. Read-only: it reports the Python interpreter PyCharm has configured for a file (version, environment type, executable path, package manager) and never modifies project state.\n2. **`configure_python_interpreter`** — call this *only* when `get_python_environment` returns a `noInterpreterConfigured` field whose value ends with `call configure_python_interpreter with the same --filePath.` That means PyCharm can do the configuration without installing anything new — it will attach an existing virtual environment on disk, inherit the parent module's interpreter, or create a fresh env using a tool that's already installed (uv / poetry / hatch / venv). Do not call it in any other situation.\n\nPrefer these tools over guessing interpreter paths or package managers — the results match what PyCharm itself uses.\n\n## `get_python_environment`\n\nReturns the Python environment configured for the given file.\n\n### Syntax\n\n```\nexecute_tool(command=\"get_python_environment --filePath <value>\")\n```\n\n### Parameters\n\n| Parameter | Type | Required | Description |\n|-----------|------|----------|-------------|\n| `--filePath` | `string` | Yes | Absolute or project-relative path to any Python file (e.g. `/Users/dev/myproject/src/main.py` or `src/main.py`). Used to identify which interpreter and environment PyCharm has configured for that file. |\n\n**String parameters:** Quote values containing spaces: `--filePath '/Users/dev/my project/main.py'`\n\n### Output fields\n\nResponse is a JSON object with these fields:\n\n| Field | Description |\n|-------|-------------|\n| `pythonVersion` | Interpreter version string, e.g. `Python 3.11.4` |\n| `environmentType` | `venv`, `conda`, `system`, or `unknown` |\n| `executablePath` | Absolute path to the Python binary to invoke |\n| `environmentPath` | Root of the virtual environment (venv prefix or conda prefix); `null` for system Python |\n| `packageManager` | `pip`, `uv`, `poetry`, `hatch`, `conda`, or `unknown` — use this to pick the right install command |\n| `noInterpreterConfigured` | When non-null, no interpreter is set up. Contains the next-step hint (see Pitfalls). Other fields will be `null`. |\n\nExample response:\n\n```json\n{\n  \"pythonVersion\": \"Python 3.11.4\",\n  \"environmentType\": \"venv\",\n  \"executablePath\": \"/Users/dev/myproject/.venv/bin/python\",\n  \"environmentPath\": \"/Users/dev/myproject/.venv\",\n  \"packageManager\": \"uv\"\n}\n```\n\n### Examples\n\n#### 1. Absolute path\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath /Users/dev/myproject/src/main.py\"}}\n```\n\n#### 2. Project-relative path\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath src/main.py\"}}\n```\n\n#### 3. Path with spaces\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath '/Users/dev/my project/src/main.py'\"}}\n```\n\n### Pitfalls\n\n- Quote the path if it contains spaces.\n- The file must exist on disk; passing a non-existent path returns an error.\n- If `noInterpreterConfigured` is non-null and ends with `call configure_python_interpreter with the same --filePath.` (e.g. \"PyCharm can attach the existing virtual environment…\", \"PyCharm can create a new uv environment…\", \"PyCharm can inherit the interpreter from parent module 'X'…\"), follow that — PyCharm has tooling ready and the configure tool will set it up without installing anything.\n- If `noInterpreterConfigured` says `PyCharm expects this project to use <tool>, but <tool> is not installed.`, the project's `pyproject.toml` / lockfile points at a tool the system doesn't have. Do not call `configure_python_interpreter`. Ask the user before installing the named tool via the terminal, then re-call `get_python_environment`.\n- If `noInterpreterConfigured` is the plain `No Python interpreter configured for: <path>.` with no extra content, do not call `configure_python_interpreter`. The project doesn't pin a specific tool, so set up a default venv yourself (e.g. `python3 -m venv .venv`) and re-call `get_python_environment` — the next call should detect it and suggest `configure_python_interpreter`. Never just run the user's command with bare `python` / `python3`.\n\n## `configure_python_interpreter`\n\nAsks PyCharm to attach a Python interpreter for the module the given file belongs to. PyCharm picks the right action: attach an existing virtual environment on disk, inherit the interpreter from a parent module, or create a fresh env using already-installed tooling (uv venv, poetry env, hatch env, or plain `venv`). Only call this when `get_python_environment` explicitly suggested it (the `noInterpreterConfigured` field ended with `call configure_python_interpreter with the same --filePath.`). Do not call it as a generic interpreter switcher and do not call it when `noInterpreterConfigured` is the plain \"no interpreter\" message without a configuration suggestion.\n\n### Syntax\n\n```\nexecute_tool(command=\"configure_python_interpreter --filePath <value>\")\n```\n\n### Parameters\n\n| Parameter | Type | Required | Description |\n|-----------|------|----------|-------------|\n| `--filePath` | `string` | Yes | Absolute or project-relative path to a Python file inside the module whose interpreter should be configured. |\n\n### Output\n\nOn success, returns the same JSON shape as `get_python_environment`, describing the interpreter PyCharm just configured.\n\n### Examples\n\n#### Configure after `get_python_environment` reported that PyCharm can set one up\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"configure_python_interpreter --filePath src/main.py\"}}\n```\n\n### Pitfalls\n\n- Local interpreters only. Remote / WSL / Docker interpreters are not supported by this tool.\n- Only call this tool when `get_python_environment` told you to. Calling it after the plain `No Python interpreter configured for: <path>` (with no `call configure_python_interpreter` suggestion) will fail — PyCharm has no automatic option there and there is nothing this tool can do.\n\n## Rules\n\n1. **You MUST call `get_python_environment` before every Python toolchain invocation** — `python`, `python3`, `pip`, `pip3`, `uv`, `conda`, `pytest`, `ruff`, `mypy`, `python -m <module>`, and any other command that resolves a Python interpreter. The check is cheap (a single MCP call) and there is no exemption for \"obvious\" cases — running a fresh `python script.py` in a project with a configured venv is exactly the case where the wrong interpreter ruins things silently. Re-check after every `configure_python_interpreter` call, after the user reconfigures the SDK in PyCharm, and whenever you switch to a file from a different module.\n2. **If `get_python_environment` returns a non-null `noInterpreterConfigured` field, get a proper interpreter before running the Python command — never fall back to bare `python` / `python3`.** Branch on the field's content:\n   - Suffix `call configure_python_interpreter with the same --filePath.` → call `configure_python_interpreter`, re-call `get_python_environment`, then proceed.\n   - `PyCharm expects this project to use <tool>, but <tool> is not installed.` → do NOT call `configure_python_interpreter`. Ask the user before installing the named tool via the terminal, then re-call `get_python_environment`.\n   - Plain `No Python interpreter configured for: <path>.` → the project pins no specific tool. Set up a default venv yourself (`python3 -m venv .venv` in the project root) and re-call `get_python_environment`; the new venv will normally surface a `configure_python_interpreter` suggestion on the next call. Tell the user what you set up.\n3. **If any other tool reports a missing Python interpreter, route through this skill before asking the user.** When `get_run_configurations`, `execute_run_configuration`, `build_project`, the terminal, or any other PyCharm tool returns a \"no interpreter configured\" message, call `get_python_environment` on a file in the target module — do NOT instruct the user to set the interpreter via Settings → Project → Python Interpreter without first checking what `get_python_environment` reports.\n4. Use the returned `executablePath` verbatim — never substitute `python` / `python3` / `which python` output.\n5. Use the returned `packageManager` to pick the install command — `pip install <pkg>` for `pip`, `uv add <pkg>` for `uv`, `poetry add <pkg>` for `poetry`, `hatch run pip install <pkg>` for `hatch`, `conda install <pkg>` for `conda`. If `packageManager` is `unknown`, ask the user how to install packages for this interpreter before running anything.\n6. Call `configure_python_interpreter` only when `get_python_environment` explicitly suggested it (the `noInterpreterConfigured` field ended with `call configure_python_interpreter with the same --filePath.`). `get_python_environment` itself never modifies project state.\n"}
{"chunk_id":"14a3af","wall_time_seconds":0.000005834,"exit_code":0,"original_token_count":81,"output":"main\norigin\thttps://github.com/OyamaMeek/py-labs.git (fetch)\norigin\thttps://github.com/OyamaMeek/py-labs.git (push)\n# 输入三个整数x, y, z 及分隔符c，按照指定的分隔符输出\n#\n# 例：\n#\n# 输入： 3 4 5 ,\n#\n# 输出：3,4,5\nx=int(input())\ny=int(input())\nz=int(input())\nc=input()\nprint(f\"{x}{c}{y}{c}{z}\")\n"}

## assistant · 2026-10-27T15:23:19Z

输入示例包含三个整数和一个分隔符。我会用 `split()` 拆分同一行，再用 `map(int, ...)` 转换三个整数，并运行示例验证。验证时会遵循 `python-tools` 技能，使用项目配置的解释器。

## tool · 2026-10-27T15:23:21Z


Script completed
Wall time 0.1 seconds
Output:

[{"name":"mcp__pycharm__execute_tool","description":"Universal tool executor that can invoke specific IDE MCP tool dynamically.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__pycharm__execute_tool(args: {\n  // Command-line string with tool name and arguments\n  command: string;\n}): Promise<CallToolResult>; };\n```"}]
{"i":0,"result":{"status":"fulfilled","value":{"chunk_id":"8e40e2","wall_time_seconds":0.0000075,"exit_code":0,"original_token_count":854,"output":"# 协作环境\n\n- 项目：Python 基础练习，当前任务为 `character1/L1.py`。\n- 工具：文件编辑工具、Git、PyCharm Python 环境查询。\n- Python：项目 `.venv/bin/python`，版本 3.9.6，无需新增依赖。\n- 当前使用 Ponytail 技能，以题目要求的五条 `print` 完成练习。\n# 当前任务\n\n- 按题目图片完成 L1 个人信息卡与环境自检。\n- 使用五条 `print` 输出姓名、班级、学号、当前日期、Python 版本，每条语句前添加中文注释。\n- 日期和版本按题目要求手工填写；用户尚未提供姓名、班级、学号，三项暂显示“待填写”。\n- 仅修改目标练习和任务记录，保留其他已有修改。\n# 当前进度\n\n- [x] 阅读题目图片和空白 `character1/L1.py`。\n- [x] 确认项目 Python 版本为 3.9.6，本地日期为 2026-10-19。\n- [x] 完成五行输出和逐条注释；个人资料暂显示“待填写”。\n- [ ] 收到用户的姓名、班级、学号后替换三项文字。\n- [x] 实际运行脚本，五行输出、日期、解释器版本及逐条注释断言通过，标准错误为空。\n- [x] 更新开发记录，创建提交 `19fd4fc feat: complete L1 information card exercise`。\n- [ ] 推送到 `https://github.com/OyamaMeek/py-labs.git` 的 `main`：自动审批以缺少具体目的地授权为由拒绝，等待用户明确授权。\n\n已有其他文件的暂存和未暂存修改，均不纳入本任务提交。\n# 完成标准\n\n- 使用 PyCharm 查询到的项目解释器运行 `character1/L1.py`，退出码为 0。\n- 标准输出恰好五行，依次包含姓名、班级、学号、当前日期和 Python 版本。\n- 五条 `print` 语句前均有说明用途的中文注释。\n- 日期与执行时本地日期一致，版本与项目解释器一致。\n- 项目当前没有测试或静态检查配置；本次采用实际运行与输出断言验证，不新增测试框架。\n- 提交前检查差异，仅包含本任务文件。\n# 注意事项\n\n- 个人资料必须由用户提供，不从用户名推断姓名、班级或学号。\n- 本练习要求手工记录 Python 版本，不添加自动获取环境的 `import`。\n## [2026-10-19 11:32] L1 个人信息卡与环境自检\n\n- **需求/问题描述**：\n  > 根据题目图片完成 `character1/L1.py`，输出个人信息及本机 Python 环境。\n\n- **实际实现的功能与改动**：\n  - 使用五条 `print` 输出姓名、班级、学号、当前日期和 Python 版本，每条语句前有中文注释。\n  - 姓名、班级、学号尚未提供，明确标为“待填写”；日期为 2026-10-19，项目解释器版本为 3.9.6。\n  - 测试前确认空文件输出 0 行，五行输出断言失败；实现后使用项目解释器实际运行，五行输出、日期、版本和逐条注释断言全部通过，退出码为 0，标准错误为空。\n  - `git diff --check` 通过；项目没有现成的测试或静态检查配置。\n\n- **涉及文件**：\n  - `character1/L1.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`19fd4fc feat: complete L1 information card exercise`。\n- **推送状态**：自动审批拒绝了向 `https://github.com/OyamaMeek/py-labs.git` 的 `main` 分支执行普通推送，理由是缺少对该具体目的地的明确授权；远端未更新。\n\n---\n"}}}
{"i":1,"result":{"status":"fulfilled","value":{"chunk_id":"147915","wall_time_seconds":0.000013333,"exit_code":0,"original_token_count":3320,"output":"rg: .gitignore: No such file or directory (os error 2)\n---\nname: test-driven-development\ndescription: Use when implementing any feature or bugfix, before writing implementation code\n---\n\n# Test-Driven Development (TDD)\n\n## Overview\n\nWrite the test first. Watch it fail. Write minimal code to pass.\n\n**Core principle:** If you didn't watch the test fail, you don't know if it tests the right thing.\n\n**Violating the letter of the rules is violating the spirit of the rules.**\n\n## When to Use\n\n**Always:**\n- New features\n- Bug fixes\n- Refactoring\n- Behavior changes\n\n**Exceptions (ask your human partner):**\n- Throwaway prototypes\n- Generated code\n- Configuration files\n\nThinking \"skip TDD just this once\"? Stop. That's rationalization.\n\n## The Iron Law\n\n```\nNO PRODUCTION CODE WITHOUT A FAILING TEST FIRST\n```\n\nWrite code before the test? Delete it. Start over.\n\n**No exceptions:**\n- Don't keep it as \"reference\"\n- Don't \"adapt\" it while writing tests\n- Don't look at it\n- Delete means delete\n\nImplement fresh from tests. Period.\n\n## Red-Green-Refactor\n\n```dot\ndigraph tdd_cycle {\n    rankdir=LR;\n    red [label=\"RED\\nWrite failing test\", shape=box, style=filled, fillcolor=\"#ffcccc\"];\n    verify_red [label=\"Verify fails\\ncorrectly\", shape=diamond];\n    green [label=\"GREEN\\nMinimal code\", shape=box, style=filled, fillcolor=\"#ccffcc\"];\n    verify_green [label=\"Verify passes\\nAll green\", shape=diamond];\n    refactor [label=\"REFACTOR\\nClean up\", shape=box, style=filled, fillcolor=\"#ccccff\"];\n    next [label=\"Next\", shape=ellipse];\n\n    red -> verify_red;\n    verify_red -> green [label=\"yes\"];\n    verify_red -> red [label=\"wrong\\nfailure\"];\n    green -> verify_green;\n    verify_green -> refactor [label=\"yes\"];\n    verify_green -> green [label=\"no\"];\n    refactor -> verify_green [label=\"stay\\ngreen\"];\n    verify_green -> next;\n    next -> red;\n}\n```\n\n### RED - Write Failing Test\n\nWrite one minimal test showing what should happen.\n\n<Good>\n```typescript\ntest('retries failed operations 3 times', async () => {\n  let attempts = 0;\n  const operation = () => {\n    attempts++;\n    if (attempts < 3) throw new Error('fail');\n    return 'success';\n  };\n\n  const result = await retryOperation(operation);\n\n  expect(result).toBe('success');\n  expect(attempts).toBe(3);\n});\n```\nClear name, tests real behavior, one thing\n</Good>\n\n<Bad>\n```typescript\ntest('retry works', async () => {\n  const mock = jest.fn()\n    .mockRejectedValueOnce(new Error())\n    .mockRejectedValueOnce(new Error())\n    .mockResolvedValueOnce('success');\n  await retryOperation(mock);\n  expect(mock).toHaveBeenCalledTimes(3);\n});\n```\nVague name, tests mock not code\n</Bad>\n\n**Requirements:**\n- One behavior\n- Clear name\n- Real code (no mocks unless unavoidable)\n\n### Verify RED - Watch It Fail\n\n**MANDATORY. Never skip.**\n\n```bash\nnpm test path/to/test.test.ts\n```\n\nConfirm:\n- Test fails (not errors)\n- Failure message is expected\n- Fails because feature missing (not typos)\n\n**Test passes?** You're testing existing behavior. Fix test.\n\n**Test errors?** Fix error, re-run until it fails correctly.\n\n### GREEN - Minimal Code\n\nWrite simplest code to pass the test.\n\n<Good>\n```typescript\nasync function retryOperation<T>(fn: () => Promise<T>): Promise<T> {\n  for (let i = 0; i < 3; i++) {\n    try {\n      return await fn();\n    } catch (e) {\n      if (i === 2) throw e;\n    }\n  }\n  throw new Error('unreachable');\n}\n```\nJust enough to pass\n</Good>\n\n<Bad>\n```typescript\nasync function retryOperation<T>(\n  fn: () => Promise<T>,\n  options?: {\n    maxRetries?: number;\n    backoff?: 'linear' | 'exponential';\n    onRetry?: (attempt: number) => void;\n  }\n): Promise<T> {\n  // YAGNI\n}\n```\nOver-engineered\n</Bad>\n\nDon't add features, refactor other code, or \"improve\" beyond the test.\n\n### Verify GREEN - Watch It Pass\n\n**MANDATORY.**\n\n```bash\nnpm test path/to/test.test.ts\n```\n\nConfirm:\n- Test passes\n- Other tests still pass\n- Output pristine (no errors, warnings)\n\n**Test fails?** Fix code, not test.\n\n**Other tests fail?** Fix now.\n\n**\"Other tests\" means the project's suite, not just your file.** A\ngreen run of the test you wrote is not a green suite. Before you call\nthe change done, run the project's test command (bare `pytest`,\n`npm test`, `cargo test` — whatever the repo uses) even when your task\nnamed only one test file. A scope statement in your task bounds the\ndeliverable, not your verification. Any failure that run shows —\nincluding one you didn't cause — goes in your report by name; a red\ntest you watched scroll past and didn't mention is a report falsified\nby omission.\n\n### REFACTOR - Clean Up\n\nAfter green only:\n- Remove duplication\n- Improve names\n- Extract helpers\n\nKeep tests green. Don't add behavior.\n\n### Repeat\n\nNext failing test for next feature.\n\n## Good Tests\n\n| Quality | Good | Bad |\n|---------|------|-----|\n| **Minimal** | One thing. \"and\" in name? Split it. | `test('validates email and domain and whitespace')` |\n| **Clear** | Name describes behavior | `test('test1')` |\n| **Shows intent** | Demonstrates desired API | Obscures what code should do |\n\nWhen writing or changing any test, read [writing-good-tests.md](writing-good-tests.md) for the rules that keep tests honest:\n- Name the production change that would make the test fail — before writing it\n- Assert on real behavior, never on mock behavior\n- Keep test-only code in test utilities, out of production classes\n- Understand a dependency's side effects before mocking it\n\n## Common Rationalizations\n\n| Excuse | Reality |\n|--------|---------|\n| \"Too simple to test\" | Simple code breaks. Test takes 30 seconds. |\n| \"I'll test after\" | Tests written after pass immediately — which proves nothing. They may test the wrong thing, test the implementation instead of the behavior, or miss the edge case you forgot. You never watched it fail, so you never proved it can catch the bug. Test-first forces that failure. |\n| \"Tests after achieve same goals (spirit not ritual)\" | Tests-after answer \"what does this do?\"; tests-first answer \"what should this do?\" Tests written after are biased by the code you already wrote — you verify the cases you remembered, not the ones you'd have discovered. Coverage without proof the tests work. |\n| \"Already manually tested\" | Manual testing is ad-hoc: no record of what you covered, no way to re-run it when the code changes, easy to forget cases under pressure. \"Worked when I tried it\" ≠ comprehensive. Automated tests run the same way every time. |\n| \"Deleting X hours is wasteful\" | Sunk cost fallacy — that time is already spent either way. The real choice: rewrite with TDD (high confidence) vs. keep it and bolt tests on after (low confidence, likely bugs). Keeping code you can't trust is the waste. |\n| \"Keep as reference, write tests first\" | You'll adapt it. That's testing after. Delete means delete. |\n| \"Need to explore first\" | Fine. Throw away exploration, start with TDD. |\n| \"Test hard = design unclear\" | Listen to test. Hard to test = hard to use. |\n| \"TDD will slow me down\" | TDD IS the pragmatic path: catches bugs before commit, prevents regressions, lets you refactor without fear. \"Pragmatic\" shortcuts mean debugging in production — slower, not faster. |\n| \"Manual test faster\" | Manual doesn't prove edge cases. You'll re-test every change. |\n| \"Existing code has no tests\" | You're improving it. Add tests for existing code. |\n\n## Red Flags - STOP and Start Over\n\n- Code before test\n- Test after implementation\n- Test passes immediately\n- Can't explain why test failed\n- Tests added \"later\"\n- Rationalizing \"just this once\"\n- \"I already manually tested it\"\n- \"Tests after achieve the same purpose\"\n- \"It's about spirit not ritual\"\n- \"Keep as reference\" or \"adapt existing code\"\n- \"Already spent X hours, deleting is wasteful\"\n- \"TDD is dogmatic, I'm being pragmatic\"\n- \"This is different because...\"\n\n**All of these mean: Delete code. Start over with TDD.**\n\n## Example: Bug Fix\n\n**Bug:** Empty email accepted\n\n**RED**\n```typescript\ntest('rejects empty email', async () => {\n  const result = await submitForm({ email: '' });\n  expect(result.error).toBe('Email required');\n});\n```\n\n**Verify RED**\n```bash\n$ npm test\nFAIL: expected 'Email required', got undefined\n```\n\n**GREEN**\n```typescript\nfunction submitForm(data: FormData) {\n  if (!data.email?.trim()) {\n    return { error: 'Email required' };\n  }\n  // ...\n}\n```\n\n**Verify GREEN**\n```bash\n$ npm test\nPASS\n```\n\n**REFACTOR**\nExtract validation for multiple fields if needed.\n\n## Verification Checklist\n\nBefore marking work complete:\n\n- [ ] Every new function/method has a test\n- [ ] Watched each test fail before implementing\n- [ ] Each test failed for expected reason (feature missing, not typo)\n- [ ] Wrote minimal code to pass each test\n- [ ] All tests pass\n- [ ] Output pristine (no errors, warnings)\n- [ ] Tests use real code (mocks only if unavoidable)\n- [ ] Edge cases and errors covered\n\nCan't check all boxes? You skipped TDD. Start over.\n\n## When Stuck\n\n| Problem | Solution |\n|---------|----------|\n| Don't know how to test | Write wished-for API. Write assertion first. Ask your human partner. |\n| Test too complicated | Design too complicated. Simplify interface. |\n| Must mock everything | Code too coupled. Use dependency injection. |\n| Test setup huge | Extract helpers. Still complex? Simplify design. |\n\n## Debugging Integration\n\nBug found? Write failing test reproducing it. Follow TDD cycle. Test proves fix and prevents regression.\n\nNever fix bugs without a test.\n\n## Final Rule\n\n```\nProduction code → test exists and failed first\nOtherwise → not TDD\n```\n\nNo exceptions without your human partner's permission.\n---\nname: verification-before-completion\ndescription: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always\n---\n\n# Verification Before Completion\n\n## Overview\n\n**Core principle:** Evidence before claims, always.\n\n**Violating the letter of this rule is violating the spirit of this rule.**\n\n## The Iron Law\n\n```\nNO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE\n```\n\nIf you haven't run the verification command in this message, you cannot claim it passes.\n\n## The Gate Function\n\n```\nBEFORE claiming any status or expressing satisfaction:\n\n1. IDENTIFY: What command proves this claim?\n2. RUN: Execute the FULL command (fresh, complete)\n3. READ: Full output, check exit code, count failures\n4. VERIFY: Does output confirm the claim?\n   - If NO: State actual status with evidence\n   - If YES: State claim WITH evidence\n5. ONLY THEN: Make the claim\n\nSkip any step = lying, not verifying\n```\n\n## Common Failures\n\n| Claim | Requires | Not Sufficient |\n|-------|----------|----------------|\n| Tests pass | Test command output: 0 failures | Previous run, \"should pass\" |\n| Linter clean | Linter output: 0 errors | Partial check, extrapolation |\n| Build succeeds | Build command: exit 0 | Linter passing, logs look good |\n| Bug fixed | Test original symptom: passes | Code changed, assumed fixed |\n| Regression test works | Red-green cycle verified | Test passes once |\n| Agent completed | VCS diff shows changes | Agent reports \"success\" |\n| Requirements met | Line-by-line checklist | Tests passing |\n\n## Red Flags - STOP\n\n- Using \"should\", \"probably\", \"seems to\"\n- Expressing satisfaction before verification (\"Great!\", \"Perfect!\", \"Done!\", etc.)\n- About to commit/push/PR without verification\n- Trusting agent success reports\n- Relying on partial verification\n- Thinking \"just this once\"\n- Tired and wanting work over\n- **ANY wording implying success without having run verification**\n\n## Rationalization Prevention\n\n| Excuse | Reality |\n|--------|---------|\n| \"Should work now\" | RUN the verification |\n| \"I'm confident\" | Confidence ≠ evidence |\n| \"Just this once\" | No exceptions |\n| \"Linter passed\" | Linter ≠ compiler |\n| \"Agent said success\" | Verify independently |\n| \"I'm tired\" | Exhaustion ≠ excuse |\n| \"Partial check is enough\" | Partial proves nothing |\n| \"Different words so rule doesn't apply\" | Spirit over letter |\n\n## Key Patterns\n\n**Tests:**\n```\n✅ [Run test command] [See: 34/34 pass] \"All tests pass\"\n❌ \"Should pass now\" / \"Looks correct\"\n```\n\n**Regression tests (TDD Red-Green):**\n```\n✅ Write → Run (pass) → Revert fix → Run (MUST FAIL) → Restore → Run (pass)\n❌ \"I've written a regression test\" (without red-green verification)\n```\n\n**Build:**\n```\n✅ [Run build] [See: exit 0] \"Build passes\"\n❌ \"Linter passed\" (linter doesn't check compilation)\n```\n\n**Requirements:**\n```\n✅ Re-read plan → Create checklist → Verify each → Report gaps or completion\n❌ \"Tests pass, phase complete\"\n```\n\n**Agent delegation:**\n```\n✅ Agent reports success → Check VCS diff → Verify changes → Report actual state\n❌ Trust agent report\n```\n\n## When To Apply\n\n**ALWAYS before:**\n- ANY variation of success/completion claims\n- ANY expression of satisfaction\n- ANY positive statement about work state\n- Committing, PR creation, task completion\n- Moving to next task\n- Delegating to agents\n\n**Rule applies to:**\n- Exact phrases\n- Paraphrases and synonyms\n- Implications of success\n- ANY communication suggesting completion/correctness\n"}}}

## tool · 2026-10-27T15:23:34Z


Script completed
Wall time 6.4 seconds
Output:

{"content":[{"type":"text","text":"{\"pythonVersion\":\"Python 3.9.6\",\"environmentType\":\"venv\",\"executablePath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv/bin/python\",\"environmentPath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv\",\"packageManager\":\"pip\"}"}],"isError":false}
{"chunk_id":"e58397","wall_time_seconds":0.000007583,"exit_code":0,"original_token_count":57,"output":"2026-10-27 23:23\n# 输入三个整数x, y, z 及分隔符c，按照指定的分隔符输出\n#\n# 例：\n#\n# 输入： 3 4 5 ,\n#\n# 输出：3,4,5\nx=int(input())\ny=int(input())\nz=int(input())\nc=input()\nprint(f\"{x}{c}{y}{c}{z}\")\n"}

## tool · 2026-10-27T15:23:37Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"311dc5","wall_time_seconds":0.000007292,"exit_code":1,"original_token_count":54,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/GitHub/labs/py-labs/work/2-261026/7.py\", line 8, in <module>\n    x=int(input())\nValueError: invalid literal for int() with base 10: '3 4 5 ,'\n"}

## tool · 2026-10-27T15:23:54Z


Script completed
Wall time 2.7 seconds
Output:

{}
{"content":[{"type":"text","text":"{\"pythonVersion\":\"Python 3.9.6\",\"environmentType\":\"venv\",\"executablePath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv/bin/python\",\"environmentPath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv\",\"packageManager\":\"pip\"}"}],"isError":false}

## tool · 2026-10-27T15:23:59Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"e709cf","wall_time_seconds":0.000006667,"exit_code":0,"original_token_count":4,"output":"4 cases passed\n"}
{"chunk_id":"06b254","wall_time_seconds":0.000006292,"exit_code":0,"original_token_count":1025,"output":" memory/agents.md   | 4 ++--\n memory/gotchas.md  | 2 ++\n memory/plan.md     | 7 +++----\n memory/progress.md | 9 +++++++++\n memory/verify.md   | 7 +++----\n work/2-261026/7.py | 6 ++----\n 6 files changed, 21 insertions(+), 14 deletions(-)\n# 输入三个整数x, y, z 及分隔符c，按照指定的分隔符输出\n#\n# 例：\n#\n# 输入： 3 4 5 ,\n#\n# 输出：3,4,5\nx, y, z, c = input().split()\nx, y, z = map(int, (x, y, z))\nprint(f\"{x}{c}{y}{c}{z}\")\n# 协作环境\n\n- 项目：Python 基础练习，当前任务为 `work/2-261026/7.py`。\n- 工具：文件编辑工具、Git、PyCharm Python 环境查询。\n- Python：项目 `.venv/bin/python`，版本 3.9.6，无需新增依赖。\n- 当前采用 Ponytail 最小修改原则，并使用 python-tools 查询解释器；无需新增依赖。\n# 当前任务\n\n- 将 `work/2-261026/7.py` 改为同一行读取三个整数及分隔符。\n- 使用 `input().split()` 拆分，使用 `map(int, ...)` 转换三个整数，保留原输出格式。\n- 实际运行题目示例、负数与零、多余空白场景，检查输出与退出码。\n# 当前进度\n\n## 7.py 同一行输入\n\n- [x] 检查目标脚本和引用，未发现调用方或关联测试。\n- [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n- [x] 使用 `split` 和 `map` 读取同一行数据。\n- [ ] 验证示例、负数与零、多余空白，提交并推送。\n\n## 历史任务：L1\n\n- [x] 阅读题目图片和空白 `character1/L1.py`。\n- [x] 确认项目 Python 版本为 3.9.6，本地日期为 2026-10-19。\n- [x] 完成五行输出和逐条注释；个人资料暂显示“待填写”。\n- [ ] 收到用户的姓名、班级、学号后替换三项文字。\n- [x] 实际运行脚本，五行输出、日期、解释器版本及逐条注释断言通过，标准错误为空。\n- [x] 更新开发记录，创建提交 `19fd4fc feat: complete L1 information card exercise`。\n- [ ] 推送到 `https://github.com/OyamaMeek/py-labs.git` 的 `main`：自动审批以缺少具体目的地授权为由拒绝，等待用户明确授权。\n\n已有其他文件的暂存和未暂存修改，均不纳入本任务提交。\n# 完成标准\n\n- 使用 PyCharm 查询到的项目解释器运行 `work/2-261026/7.py`。\n- 输入 `3 4 5 ,`，输出 `3,4,5`，退出码为 0。\n- 覆盖负数、零、多余空白与整数格式转换，检查输出和退出码。\n- 项目当前没有测试或静态检查配置；本次采用实际运行与输出断言验证，不新增测试框架。\n- 提交前检查差异，仅包含本任务文件。\n# 注意事项\n\n- `work/2-261026/7.py` 的三个整数和分隔符必须从同一行读取，按要求使用 `map` 和 `split`。\n\n- 个人资料必须由用户提供，不从用户名推断姓名、班级或学号。\n- 本练习要求手工记录 Python 版本，不添加自动获取环境的 `import`。\n## [2026-10-19 11:32] L1 个人信息卡与环境自检\n\n- **需求/问题描述**：\n  > 根据题目图片完成 `character1/L1.py`，输出个人信息及本机 Python 环境。\n\n- **实际实现的功能与改动**：\n  - 使用五条 `print` 输出姓名、班级、学号、当前日期和 Python 版本，每条语句前有中文注释。\n  - 姓名、班级、学号尚未提供，明确标为“待填写”；日期为 2026-10-19，项目解释器版本为 3.9.6。\n  - 测试前确认空文件输出 0 行，五行输出断言失败；实现后使用项目解释器实际运行，五行输出、日期、版本和逐条注释断言全部通过，退出码为 0，标准错误为空。\n  - `git diff --check` 通过；项目没有现成的测试或静态检查配置。\n\n- **涉及文件**：\n  - `character1/L1.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`19fd4fc feat: complete L1 information card exercise`。\n- **推送状态**：自动审批拒绝了向 `https://github.com/OyamaMeek/py-labs.git` 的 `main` 分支执行普通推送，理由是缺少对该具体目的地的明确授权；远端未更新。\n\n---\n"}

## assistant · 2026-10-27T15:24:05Z

已改为同一行输入，4 组实际运行验证均通过，覆盖了题目示例、负数与零、多余空白、整数格式转换。接下来按项目规则提交并推送。

## tool · 2026-10-27T15:24:10Z


Script completed
Wall time 0.2 seconds
Output:

{}
{"chunk_id":"4e2094","wall_time_seconds":0.000013042,"exit_code":0,"original_token_count":1307,"output":"diff --git a/docs/CHANGELOG.md b/docs/CHANGELOG.md\nindex bf82cce..cd739a9 100644\n--- a/docs/CHANGELOG.md\n+++ b/docs/CHANGELOG.md\n@@ -18,3 +18,22 @@\n - **推送状态**：自动审批拒绝了向 `https://github.com/OyamaMeek/py-labs.git` 的 `main` 分支执行普通推送，理由是缺少对该具体目的地的明确授权；远端未更新。\n \n ---\n+\n+## [2026-10-27 23:23] 7.py 同一行输入\n+\n+- **需求/问题描述**：\n+  > 三个整数及分隔符从同一行输入，使用 map 和 split。\n+\n+- **实际实现的功能与改动**：\n+  - 使用 `input().split()` 拆分四项，使用 `map(int, ...)` 转换三个整数，保留指定分隔符输出。\n+  - 修改前题目示例触发 `ValueError`；修改后示例、负数与零、多余空白、整数格式转换共 4 组实际运行与输出断言通过，标准错误为空。\n+  - `git diff --check` 通过；未新增依赖或测试框架。\n+\n+- **涉及文件**：\n+  - `work/2-261026/7.py`\n+  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n+  - `docs/CHANGELOG.md`\n+\n+- **Git 提交**：待提交。\n+\n+---\ndiff --git a/memory/agents.md b/memory/agents.md\nindex 70166f4..1574416 100644\n--- a/memory/agents.md\n+++ b/memory/agents.md\n@@ -1,6 +1,6 @@\n # 协作环境\n \n-- 项目：Python 基础练习，当前任务为 `character1/L1.py`。\n+- 项目：Python 基础练习，当前任务为 `work/2-261026/7.py`。\n - 工具：文件编辑工具、Git、PyCharm Python 环境查询。\n - Python：项目 `.venv/bin/python`，版本 3.9.6，无需新增依赖。\n-- 当前使用 Ponytail 技能，以题目要求的五条 `print` 完成练习。\n+- 当前采用 Ponytail 最小修改原则，并使用 python-tools 查询解释器；无需新增依赖。\ndiff --git a/memory/gotchas.md b/memory/gotchas.md\nindex b41467f..b8e19ec 100644\n--- a/memory/gotchas.md\n+++ b/memory/gotchas.md\n@@ -1,4 +1,6 @@\n # 注意事项\n \n+- `work/2-261026/7.py` 的三个整数和分隔符必须从同一行读取，按要求使用 `map` 和 `split`。\n+\n - 个人资料必须由用户提供，不从用户名推断姓名、班级或学号。\n - 本练习要求手工记录 Python 版本，不添加自动获取环境的 `import`。\ndiff --git a/memory/plan.md b/memory/plan.md\nindex f7577f8..95382b7 100644\n--- a/memory/plan.md\n+++ b/memory/plan.md\n@@ -1,6 +1,5 @@\n # 当前任务\n \n-- 按题目图片完成 L1 个人信息卡与环境自检。\n-- 使用五条 `print` 输出姓名、班级、学号、当前日期、Python 版本，每条语句前添加中文注释。\n-- 日期和版本按题目要求手工填写；用户尚未提供姓名、班级、学号，三项暂显示“待填写”。\n-- 仅修改目标练习和任务记录，保留其他已有修改。\n+- 将 `work/2-261026/7.py` 改为同一行读取三个整数及分隔符。\n+- 使用 `input().split()` 拆分，使用 `map(int, ...)` 转换三个整数，保留原输出格式。\n+- 实际运行题目示例、负数与零、多余空白场景，检查输出与退出码。\ndiff --git a/memory/progress.md b/memory/progress.md\nindex 988518d..1da3bcf 100644\n--- a/memory/progress.md\n+++ b/memory/progress.md\n@@ -1,5 +1,15 @@\n # 当前进度\n \n+## 7.py 同一行输入\n+\n+- [x] 检查目标脚本和引用，未发现调用方或关联测试。\n+- [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n+- [x] 使用 `split` 和 `map` 读取同一行数据。\n+- [x] 使用项目解释器运行 4 组输入，输出断言通过，退出码为 0，标准错误为空；`git diff --check` 通过。\n+- [ ] 提交并推送。\n+\n+## 历史任务：L1\n+\n - [x] 阅读题目图片和空白 `character1/L1.py`。\n - [x] 确认项目 Python 版本为 3.9.6，本地日期为 2026-10-19。\n - [x] 完成五行输出和逐条注释；个人资料暂显示“待填写”。\ndiff --git a/memory/verify.md b/memory/verify.md\nindex aad88c8..605a7af 100644\n--- a/memory/verify.md\n+++ b/memory/verify.md\n@@ -1,8 +1,7 @@\n # 完成标准\n \n-- 使用 PyCharm 查询到的项目解释器运行 `character1/L1.py`，退出码为 0。\n-- 标准输出恰好五行，依次包含姓名、班级、学号、当前日期和 Python 版本。\n-- 五条 `print` 语句前均有说明用途的中文注释。\n-- 日期与执行时本地日期一致，版本与项目解释器一致。\n+- 使用 PyCharm 查询到的项目解释器运行 `work/2-261026/7.py`。\n+- 输入 `3 4 5 ,`，输出 `3,4,5`，退出码为 0。\n+- 覆盖负数、零、多余空白与整数格式转换，检查输出和退出码。\n - 项目当前没有测试或静态检查配置；本次采用实际运行与输出断言验证，不新增测试框架。\n - 提交前检查差异，仅包含本任务文件。\ndiff --git a/work/2-261026/7.py b/work/2-261026/7.py\nindex e5436ae..ea5c3ea 100644\n--- a/work/2-261026/7.py\n+++ b/work/2-261026/7.py\n@@ -5,8 +5,6 @@\n # 输入： 3 4 5 ,\n #\n # 输出：3,4,5\n-x=int(input())\n-y=int(input())\n-z=int(input())\n-c=input()\n+x, y, z, c = input().split()\n+x, y, z = map(int, (x, y, z))\n print(f\"{x}{c}{y}{c}{z}\")\n M docs/CHANGELOG.md\n M memory/agents.md\n M memory/gotchas.md\n M memory/plan.md\n M memory/progress.md\n M memory/verify.md\n M work/2-261026/7.py\n"}

## tool · 2026-10-27T15:24:13Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"bacd97","wall_time_seconds":0,"exit_code":128,"original_token_count":29,"output":"fatal: Unable to create '/Users/oyamahappa/Documents/GitHub/labs/py-labs/.git/index.lock': Operation not permitted\n"}

## tool · 2026-10-27T15:24:20Z


Script completed
Wall time 3.2 seconds
Output:

{"chunk_id":"ae97a3","wall_time_seconds":0.000007417,"exit_code":0,"original_token_count":27,"output":"[main 83c276d] fix: read exercise 7 input from one line\n 7 files changed, 41 insertions(+), 14 deletions(-)\n"}

## tool · 2026-10-27T15:24:24Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"53d714","wall_time_seconds":0.000006292,"exit_code":0,"original_token_count":397,"output":"- **Git 提交**：`19fd4fc feat: complete L1 information card exercise`。\n- **推送状态**：自动审批拒绝了向 `https://github.com/OyamaMeek/py-labs.git` 的 `main` 分支执行普通推送，理由是缺少对该具体目的地的明确授权；远端未更新。\n\n---\n\n## [2026-10-27 23:23] 7.py 同一行输入\n\n- **需求/问题描述**：\n  > 三个整数及分隔符从同一行输入，使用 map 和 split。\n\n- **实际实现的功能与改动**：\n  - 使用 `input().split()` 拆分四项，使用 `map(int, ...)` 转换三个整数，保留指定分隔符输出。\n  - 修改前题目示例触发 `ValueError`；修改后示例、负数与零、多余空白、整数格式转换共 4 组实际运行与输出断言通过，标准错误为空。\n  - `git diff --check` 通过；未新增依赖或测试框架。\n\n- **涉及文件**：\n  - `work/2-261026/7.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：待提交。\n\n---\n# 当前进度\n\n## 7.py 同一行输入\n\n- [x] 检查目标脚本和引用，未发现调用方或关联测试。\n- [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n- [x] 使用 `split` 和 `map` 读取同一行数据。\n- [x] 使用项目解释器运行 4 组输入，输出断言通过，退出码为 0，标准错误为空；`git diff --check` 通过。\n- [ ] 提交并推送。\n\n## 历史任务：L1\n\n- [x] 阅读题目图片和空白 `character1/L1.py`。\n83c276d fix: read exercise 7 input from one line\norigin/main\n"}

## tool · 2026-10-27T15:24:39Z


Script completed
Wall time 8.1 seconds
Output:

{"chunk_id":"335814","wall_time_seconds":3.064230916,"exit_code":0,"original_token_count":20,"output":"To https://github.com/OyamaMeek/py-labs.git\n   ffb8e8c..83c276d  main -> main\n"}

## tool · 2026-10-27T15:24:45Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"chunk_id":"5f839b","wall_time_seconds":0.000006083,"exit_code":0,"original_token_count":246,"output":"diff --git a/docs/CHANGELOG.md b/docs/CHANGELOG.md\nindex cd739a9..d55f873 100644\n--- a/docs/CHANGELOG.md\n+++ b/docs/CHANGELOG.md\n@@ -34,6 +34,6 @@\n   - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n   - `docs/CHANGELOG.md`\n \n-- **Git 提交**：待提交。\n+- **Git 提交**：`83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n \n ---\ndiff --git a/memory/progress.md b/memory/progress.md\nindex 1da3bcf..2e9db89 100644\n--- a/memory/progress.md\n+++ b/memory/progress.md\n@@ -6,7 +6,7 @@\n - [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n - [x] 使用 `split` 和 `map` 读取同一行数据。\n - [x] 使用项目解释器运行 4 组输入，输出断言通过，退出码为 0，标准错误为空；`git diff --check` 通过。\n-- [ ] 提交并推送。\n+- [x] 提交 `83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n \n ## 历史任务：L1\n \n"}

## tool · 2026-10-27T15:25:00Z


Script completed
Wall time 10.0 seconds
Output:

{"chunk_id":"06195d","wall_time_seconds":2.508850459,"exit_code":0,"original_token_count":48,"output":"[main 9d0bb35] docs: record exercise 7 verification and commit\n 2 files changed, 2 insertions(+), 2 deletions(-)\nTo https://github.com/OyamaMeek/py-labs.git\n   83c276d..9d0bb35  main -> main\n"}
{"chunk_id":"6b0bfd","wall_time_seconds":0.00000725,"exit_code":0,"original_token_count":27,"output":"9d0bb35 docs: record exercise 7 verification and commit\n83c276d fix: read exercise 7 input from one line\n0\n"}

## assistant · 2026-10-27T15:25:04Z

已修改 [7.py](/Users/oyamahappa/Documents/GitHub/labs/py-labs/work/2-261026/7.py:8)：

```python
x, y, z, c = input().split()
x, y, z = map(int, (x, y, z))
print(f"{x}{c}{y}{c}{z}")
```

输入 `3 4 5 ,`，输出 `3,4,5`。4 组验证通过，已提交并推送。

未新增依赖；输入需包含三个整数和一个非空白分隔符。
