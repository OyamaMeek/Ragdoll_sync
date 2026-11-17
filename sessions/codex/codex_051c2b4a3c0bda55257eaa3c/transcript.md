# 奇怪的我

来源：codex

项目：/Users/oyamahappa/Documents/GitHub/labs/cpp-labs

## developer · 2026-11-15T01:58:57Z

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



## developer · 2026-11-15T01:58:57Z

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
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/cloud-environment/0.2.1/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.23/skills`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.9/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.6/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1112.11217/skills`
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
- cloud-environment:cloud-desktop: Open an app in shared Chrome, test a user flow, inspect a Linux w (file: r16/cloud-desktop/SKILL.md)
- cloud-environment:cloud-environment-runtime: Use when a task needs guidance on a managed Codex Cloud compute (file: r16/runtime/SKILL.md)
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
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r22/documents/26.1112.11217/skills/documents/SKILL.md)
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
- google-drive:google-drive: Use this skill to find and manage files in Google Drive, includi (file: r17/google-drive/SKILL.md)
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
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r22/pdf/26.1112.11217/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r15/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the  (file: r24/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks (file: r24/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r24/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r24/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r24/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r24/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five di (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r22/presentations/26.1112.11217/skills/presentations/SKILL.md)
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
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r22/template-creator/26.1112.11217/skills/template-creator/SKILL.md)
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

## developer · 2026-11-15T01:58:57Z

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

## developer · 2026-11-15T01:58:57Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-15T01:58:57Z

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
  <current_date>2026-11-15</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs</root><root>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs</path></entry><entry access="write"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/CLion2026.2/aia/agents/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-15T01:58:57Z

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


## user · 2026-11-15T01:58:57Z

我的好奇怪
[@20.c](file:///Users/oyamahappa/Documents/GitHub/labs/cpp-labs/C/assignments/93/20.c)
[@ai-chat-attachment-5999311249425248865.png](file:///var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T/ai-chat-attachment-5999311249425248865.png)

## assistant · 2026-11-15T01:59:01Z

我先读一下 `20.c` 和你附的图片，确认哪里出现了异常。

## tool · 2026-11-15T01:59:05Z


Script completed
Wall time 0.2 seconds
Output:

/Users/oyamahappa/Documents/GitHub/labs/cpp-labs
C/assignments/93/20.c
memory/agents.md
memory/plan.md
memory/verify.md
memory/progress.md
memory/gotchas.md

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

//
// Created by OyamaHappa on 2026/11/15.
//
#include <stdio.h>
int main (void)
{
    int i=0,j=0;
    for(i=1;i<=4;i++)
    {
        for(j=1;j<=(2*i-1);j+=2)
        {
            for(;j<=(4-i);j++)
            {
                printf(" ");
            }
            printf("*");
        }
        printf("\n");
    }
    return 0;
}
{
  "type": "input_image",
  "image_url": "images/1a8ea213ba8616869aa5093ef46930ee3a057049fe13a274c09497f99ff51434.png",
  "detail": "high"
}

## assistant · 2026-11-15T01:59:13Z

我会按 `systematic-debugging` 的方法核对循环执行过程。目前看到两个问题：内外两层循环共用了 `j`，而打印星号的循环每次让 `j` 增加了 2。

## tool · 2026-11-15T01:59:13Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 17646)
Total output lines: 639

---
name: systematic-debugging
description: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes
---

# Systematic Debugging

## Overview

**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.

**Violating the letter of this process is violating the spirit of debugging.**

## The Iron Law

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

If you haven't completed Phase 1, you cannot propose fixes.

## When to Use

Use for ANY technical issue:
- Test failures
- Bugs in production
- Unexpected behavior
- Performance problems
- Build failures
- Integration issues

**Use this ESPECIALLY when:**
- Under time pressure (emergencies make guessing tempting)
- "Just one quick fix" seems obvious
- You've already tried multiple fixes
- Previous fix didn't work
- You don't fully understand the issue

**Don't skip when:**
- Issue seems simple (simple bugs have root causes too)
- You're in a hurry (rushing guarantees rework)
- Manager wants it fixed NOW (systematic is faster than thrashing)

## The Four Phases

You MUST complete each phase before proceeding to the next.

### Phase 1: Root Cause Investigation

**BEFORE attempting ANY fix:**

1. **Read Error Messages Carefully**
   - Don't skip past errors or warnings
   - They often contain the exact solution
   - Read stack traces completely
   - Note line numbers, file paths, error codes

2. **Reproduce Consistently**
   - Can you trigger it reliably?
   - What are the exact steps?
   - Does it happen every time?
   - If not reproducible → gather more data, don't guess

3. **Check Recent Changes**
   - What changed that could cause this?
   - Git diff, recent commits
   - New dependencies, config changes
   - Environmental differences

4. **Gather Evidence in Multi-Component Systems**

   **WHEN system has multiple components (CI → build → signing, API → service → database):**

   **BEFORE proposing fixes, add diagnostic instrumentation:**
   ```
   For EACH component boundary:
     - Log what data enters component
     - Log what data exits component
     - Verify environment/config propagation
     - Check state at each layer

   Run once to gather evidence showing WHERE it breaks
   THEN analyze evidence to identify failing component
   THEN investigate that specific component
   ```

   **Example (multi-layer system):**
   ```bash
   # Layer 1: Workflow
   echo "=== Secrets available in workflow: ==="
   echo "IDENTITY: $([ -n "${IDENTITY:-}" ] && echo SET || echo UNSET)"

   # Layer 2: Build script
   echo "=== Env vars in build script: ==="
   printenv IDENTITY >/dev/null 2>&1 && echo "IDENTITY in environment" || echo "IDENTITY not in environment"

   # Layer 3: Signing script
   echo "=== Keychain state: ==="
   security list-keychains
   security find-identity -v

   # Layer 4: Actual signing
   codesign --sign "$IDENTITY" --verbose=4 "$APP"
   ```

   **This reveals:** Which layer fails (secrets → workflow ✓, workflow → build ✗)

5. **Trace Data Flow**

   **WHEN error is deep in call stack:**

   See `root-cause-tracing.md` in this directory for the complete backward tracing technique.

   **Quick version:**
   - Where does bad value originate?
   - What called this with bad value?
   - Keep tracing up until you find the source
   - Fix at source, not at symptom

### Phase 2: Pattern Analysis

**Find the pattern before fixing:**

1. **Find Working Examples**
   - Locate similar working code in same codebase
   - What works that's similar to what's broken?

2. **Compare Against References**
   - If implementing pattern, read reference implementation COMPLETELY
   - Don't skim - read every line
   - Understand the pattern fully before applying

3. **Identify Differences**
   - What's different between working and broken?
   - List every difference, however small
   - Don't assume "that can't matter"

4. **Understand Dependencies**
   - What other components does this need?
   - What settings, config, environment?
   - What assumptions does it make?

### Phase 3: Hypothesis and Testing

**Scientific method:**

1. **Form Single Hypothesis**
   - State clearly: "I think X is the root cause because Y"
   - Write it down
   - Be specific, not vague

2. **Test Minimally**
   - Make the SMALLEST possible change to test hypothesis
   - One variable at a time
   - Don't fix multiple things at once

3. **Verify Before Continuing**
   - Did it work? Yes → Phase 4
   - Didn't work? Form NEW hypothesis
   - DON'T add more fixes on top

4. **When You Don't Know**
   - Say "I don't understand X"
   - Don't pretend to know
   - Ask for help
   - Research more

### Phase 4: Implementation

**Fix the root cause, not the symptom:**

1. **Create Failing Test Case**
   - Simplest possible reproduction
   - Automated test if possible
   - One-off test script if no framework
   - MUST have before fixing
   - Use the `superpowers:test-driven-development` skill for writing proper failing tests

2. **Implement Single Fix**
   - Address the root cause identified
   - ONE change at a time
   - No "while I'm here" improvements
   - No bundled refactoring

3. **Verify Fix**
   - Test passes now?
   - No other tests broken?
   - Issue actually resolved?
   - Use the `superpowers:verification-before-completion` skill before claiming success

4. **If Fix Doesn't Work**
   - STOP
   - Count: How many fixes have you tried?
   - If < 3: Return to Phase 1, re-analyze with new information
   - **If ≥ 3: STOP and question the architecture (step 5 below)**
   - DON'T attempt Fix #4 without architectural discussion

5. **If 3+ Fixes Failed: Question Architecture**

   **Pattern indicating architectural problem:**
   - Each fix reveals new shared state/coupling/problem in different place
   - Fixes require "massive refactoring" to implement
   - Each fix creates new symptoms elsewhere

   **STOP and question fundamentals:**
   - Is this pattern fundamentally sound?
   - Are we "sticking with it through sheer inertia"?
   - Should we refactor architecture vs. continue fixing symptoms?

   **Discuss with your human partner before attempting more fixes**

   This is NOT a failed hypothesis - this is a wrong architecture.

## Red Flags - STOP and Follow Process

If you catch yourself thinking:
- "Quick fix for now, investigate later"
- "Just try changing X and see if it works"
- "Add multiple changes, run tests"
- "Skip the test, I'll manually verify"
- "It's probably X, let me fix that"
- "I don't fully understand but this might work"
- "Pattern says X but I'll adapt it differently"
- "Here are the main problems: [lists fixes without investigation]"
- Proposing solutions before tracing data flow
- **"One more fix attempt" (when already tried 2+)**
- **Each fix reveals new problem in different place**

**ALL of these mean: STOP. Return to Phase 1.**

**If 3+ fixes failed:** Question the architecture (see Phase 4.5)

## your human partner's Signals You're Doing It Wrong

**Watch for these redirections:**
- "Is that not happening?" - You assumed without verifying
- "Will it show us...?" - You should have added evidence gathering
- "Stop guessing" - You're proposing fixes without understanding
- "Ultra-think this" - Question fundamentals, not just symptoms
- "We're stuck?" (frustrated) - Your approach isn't working

**When you see these:** STOP. Return to Phase 1.

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Issue is simple, don't need process" | Simple issues have root causes too. Process is fast for simple bugs. |
| "Emergency, no time for process" | Systematic debugging is FASTER than guess-and-check thrashing. |
| "Just try this first, then investigate" | First fix sets the pattern. Do it right from the start. |
| "I'll write test after confirming fix works" | Untested fixes don't stick. Test first proves it. |
| "Multiple fixes at once saves time" | Can't isolate what worked. Causes new bugs. |
| "Reference too long, I'll adapt the pattern" | Partial understanding guarantees bugs. Read it completely. |
| "I see the problem, let me fix it" | Seeing symptoms ≠ understanding root cause. |
| "One more fix attempt" (after 2+ failures) | 3+ failures = architectural problem. Question pattern, don't fix again. |

## Quick Reference

| Phase | Key Activities | Success Criteria |
|-------|---------------|------------------|
| **1. Root Cause** | Read errors, reproduce, check changes, gather evidence | Understand WHAT and WHY |
| **2. Pattern** | Find working examples, compare | Identify differences |
| **3. Hypothesis** | Form theory, test minimally | Confirmed or new hypothesis |
| **4. Implementation** | Create test, fix, verify | Bug resolved, tests pass |

## When Process Reveals "No Root Cause"

If systematic investigation reveals issue is truly environmental, timing-dependent, or external:

1. You've completed the process
2. Document what you investigated
3. Implement appropriate handling (retry, timeout, error message)
4. Add monitoring/logging for future investigation

**But:** 95% of "no root cause" cases are incomplete investigation.

## Supporting Techniques

These techniques are part of systematic debugging and available in this directory:

- **`root-cause-tracing.md`** - Trace bugs backward through call stack to find original trigger
- **`defense-in-depth.md`** - Add validation at multiple layers after finding root cause
- **`condition-based-waiting.md`** - Replace arbitrary timeouts with condition polling

Warning: truncated output (original token count: 6789)
Total output lines: 228

---
name: clion-debugger
description: "Debugger-first runtime root-cause analysis for native and multi-language code in CLion (C, C++, Rust, Python, and other supported languages). Use when runtime state or control-flow evidence is needed (values, branches, call order, reachability), when the question spans long call chains across many files, or when the user explicitly requests the debugger. Evidence comes from logpoints/breakpoints, stepping, stacks, runtime values, expression evaluation, and control-flow observations."
allowed-tools: execute_tool
---

# CLion Debugger Skill

All debugger and run-configuration tools are invoked through the universal router:
`execute_tool(command="<tool> --arg value ...")`. Do not call the underlying handles directly.

Router argument rules:
- Every `--param` must be followed by a value; bare flags are not supported.
- Boolean params need an explicit `true`/`false` (e.g. `--isLogStack true`).
- **Quote every value that contains a space or an operator — expressions almost always do.** The router splits `command` on whitespace, so an unquoted multi-token value is misread as extra arguments and the call fails with an error like `Invalid argument format: '+'. Expected '--paramName value' format`. Wrap the whole value in single quotes so it stays one token:
  - `--logExpression 'count + 1'` (not `--logExpression count + 1`)
  - `--condition 'id == 42 && retryCount > 0'`
  - `--expression 'buffer.length'`
  - If the expression itself contains single quotes (e.g. a character or string literal), wrap the outer value in double quotes instead: `--logExpression "name == 'tax_rate'"`. Do not escape quotes with backslashes and do not JSON-encode the value.
- Omit optional params entirely instead of passing `""`, `"/"`, `"."`, `"__omit__"`, or other sentinels.

## Goal
Use debugger evidence to answer concrete runtime questions when static code reading is not enough, or to confirm ideas from static analysis — including whether execution reaches or does not reach agent-selected code locations. Gather this evidence with **minimal runtime disturbance**: by default observe without stopping threads and without editing source code.

## When To Use This Skill
Use this skill when at least one holds:
- a runtime value or control-flow fact is needed (actual values, branch taken, call order, thread context, or whether execution reaches a chosen location) and it cannot be derived confidently from source/logs;
- finding the relevant path would otherwise require reading many files or tracing a long call chain manually;
- the user explicitly asks to use the debugger (breakpoints, logpoints, stepping, inspect values, debugger session).

Manual activation by the user means launch and use the debugger when tools are available — do not reduce it to a conceptual discussion. Do not treat domain identifiers named `debug`/`debugger` in the user's own code as a debugger request; reason about what the user actually means.

## Activation Gate (tool availability)
Use this skill only when the debugger router tools are available. Minimum required set (each invoked via `execute_tool`):
- `xdebug_set_breakpoint` (important: sets logpoints, via `--logExpression`)
- `xdebug_start_debugger_session`
- `xdebug_control_session`
- `xdebug_get_stack`
- at least one value tool: `xdebug_get_frame_values`, `xdebug_get_value_by_path`, or `xdebug_evaluate_expression`
- `get_run_configurations`

If the minimum set is unavailable: state the blocker explicitly, do not force a debugger workflow, and switch to the best fallback. Run `execute_tool(command="<tool> --help")` to inspect a tool's exact current contract.

## Principle: Logpoint-First Debugging
**Logpoints are the primary way to communicate with the CLion debugger *when the active backend captures their output*.** A logpoint is a non-suspending breakpoint that does not stop execution: when the line is reached it evaluates an expression and logs the result. Where logpoint output is captured, reach for a logpoint first for almost every runtime question and treat suspending breakpoints, stepping, and expression evaluation as escalations you must justify. Logpoints give runtime evidence without freezing threads — which matters for concurrent code, long-running services, flaky/timing-sensitive tests, and multi-agent workflows.

**Backend support — read this first.** Logpoint *output* is only readable when the active debugger backend feeds it into the session event buffer. This is currently reliable for JVM-family backends; **native backends (LLDB/GDB, and the DAP backends typically used for C, C++, and Rust) may not populate the event buffer at all.** So after installing your first logpoint, run once and verify with `DRAIN_EVENTS` (see below) that output actually arrives. If it does not, do **not** conclude the code was unreached — the backend simply is not emitting logpoint events. In that case make suspending breakpoints + `xdebug_get_frame_values` / `xdebug_get_stack` your primary evidence tool for the session (there they are not an escalation); if you cannot pause the process, a temporary print/log statement is an acceptable last resort.

**When it is captured, logpoint output is dumped to debugger events, and you read it back from there.** Each logpoint hit is captured as an event in the debug session's event buffer — not printed to your console and not written to any file. You collect that output by draining events: `execute_tool(command="xdebug_control_session --action DRAIN_EVENTS")` returns the accumulated logpoint output in `tracepointOutputsTail`. So the logpoint loop is: install logpoint(s) → run the scenario → drain events → map each event back to source.

Prefer the **least disruptive** tool that answers the question, in this priority order:

1. **Non-suspending logpoints** — `execute_tool(command="xdebug_set_breakpoint --filePath <p> --line <n> --logExpression '<expr>' --suspendPolicy NONE")`. A logpoint is just `xdebug_set_breakpoint` with a `--logExpression`; add `--suspendPolicy NONE` so it does not stop execution. Providing the `--logExpression` is the most important thing you do.
   Use for runtime values, branch evidence, counts, identifiers, and path/reachability confirmation. This is the default first probe.
2. **Logpoints with condition / stack-trace logging** — add `--condition '<expr>'` to filter, and `--isLogStack true` for a call path.
   Use when events are too frequent, only specific cases matter, or a call path is needed.
3. **Thread / stack inspection of a suspended session** — `execute_tool(command="xdebug_get_threads")` + `execute_tool(command="xdebug_get_stack ...")`.
   These read a *paused* session: if the program is running, suspend it first with `execute_tool(command="xdebug_control_session --action PAUSE")`, then read threads/stack. Use for hangs, concurrency issues, deadlocks, thread-state questions, or unclear call paths.
4. **Ordinary suspending breakpoints** — `execute_tool(command="xdebug_set_breakpoint --filePath <p> --line <n>")` (the same tool without `--logExpression`, keeping the default `--suspendPolicy ALL`).
   Use only when you must inspect live object graphs, evaluate multiple expressions interactively, step through code, or modify state.
5. **Evaluate expression / Set value** — `execute_tool(command="xdebug_evaluate_expression ...")`, `execute_tool(command="xdebug_set_variable ...")`.
   Use only in a suspended context and only with explicit justification; these can alter what you are investigating.

Escalate down this list only when the cheaper option cannot answer the question, and say why you escalated.

## Safe Logpoint Expressions (no side effects)
`--logExpression` and `--condition` are evaluated inside the running program and **can change its behavior**. By default restrict them to **side-effect-free reads**: field/local/parameter access, non-mutating accessors, arithmetic, safe string conversion of trusted values, identity/equality checks.

Do **not** use expressions that mutate state, perform I/O, advance iterators/streams, trigger side-effecting lazy initialization, or call functions with observable side effects — unless the user explicitly asked to enter a controlled mutation/debugging mode and accepted that program behavior may change.

## Logpoint Placement: Variable Scope And Initialization
A logpoint evaluates its `--logExpression` **at the moment execution reaches the line, before that line's statement runs**. Every symbol the expression references must already be **assigned and in scope** at that point, or evaluation fails: the failure is reported in `breakpointErrorsTail` (as an unresolved-symbol or out-of-scope/uninitialized-variable error whose exact wording depends on the debugger backend) and no value is logged.

Rules for picking the line:
- Do **not** place a logpoint on the line that *declares or initializes* the variable you want to log, nor in the middle of a multi-line statement that assigns it. At that position the variable does not hold its value yet.
- For a multi-line assignment such as a fluent/builder chain (language-neutral pseudocode — map the line numbers onto your actual source):
  ```
  configured = load_config(path)   // line 20  ← statement starts here
      .select("items")             // line 21
      .to_list()                   // line 22  ← assignment completes here
  first = configured[0]            // line 23
  ```
  a logpoint on line 21 logging `configured[0]` fails — `configured` is assigned only after line 22. Place it on the **first line after the statement completes** (here line 23), where `configured` is initialized.
- General rule: put the logpoint on the earliest executable line where every symbol in the expression is already initialized and in scope. To capture a value at a function's entry, target the first executable line of the body, not the signature/parameter line.
- After installing, run once and read `breakpointErrorsTail`. If you see an uninitialized/unresolved-variable error, move the logpoint to a later line (or pick an expression whose inputs are already available) and rerun.

## Initial Triage Before Debugging
Start with minimal static triage (error text, stack trace, nearby source). Start debugger work when: static analysis leaves multiple plausible runtime hypotheses; deciding between them requires …7646 tokens truncated…ces using read-only SQLite SQL.\n\nUse this tool for JOINs, UNIONs, comparisons, and aggregations that need two or more data sour"},{"name":"mcp__codex_apps__sites_add_custom_domain","description":"Add a custom domain to a published site. The response includes a CNAME target for subdomains, A record targets for zone apex domains, and all App Garden and Cloudflare va"},{"name":"mcp__codex_apps__sites_change_site_slug","description":"Change a site's public URL label. The change runs asynchronously. When the result is pending, use get_site to observe the current slug; do not call this mutation again to"},{"name":"mcp__codex_apps__sites_create_schedule","description":"Create and link a cloud task for a published Site when the user has requested scheduling. Before creating a new schedule, read get_site. If automations is missing or null"},{"name":"mcp__codex_apps__sites_create_site","description":"Create a site only when .openai/hosting.json has no project_id. If it has one, reuse that site. With no project_id, retry Create with identical arguments only after site_"},{"name":"mcp__codex_apps__sites_create_source_repository_write_credential","description":"Create a short-lived source repository write credential when the credential returned by create_site is missing or no longer usable. It authorizes Git pushes to the site's"},{"name":"mcp__codex_apps__sites_deploy_private_site_version","description":"Deploy a saved site version for a site already known to have owner-only Site permissions in the selected account. The backend still requires verified owner-only access th"},{"name":"mcp__codex_apps__sites_deploy_site_version","description":"Deploy a saved site version to production when the site is shared, public, cannot be verified as owner-only, or private deployment is unavailable. If access is unknown, c"},{"name":"mcp__codex_apps__sites_generate_siwc_bypass_token","description":"Generate a bearer token for identity-less API requests that bypasses a site's Sign in with ChatGPT gate. Call this explicit token tool only when the user asks for a bypas"},{"name":"mcp__codex_apps__sites_get_deployment_status","description":"Get the current status of a production deployment. Only poll when a deployment ID is available; the deployment owns its saved version, so do not supply version_id. Contin"},{"name":"mcp__codex_apps__sites_get_environment_variables","description":"Get the production runtime environment variables for a site. These values are separate from local .env files and .openai/hosting.json. This tool is part of plugin `Sites`"},{"name":"mcp__codex_apps__sites_get_site","description":"Get a site and its current access configuration, including external visitors. For a Library Site result, copy its server-returned site_metadata.project_id unchanged as pr"},{"name":"mcp__codex_apps__sites_get_site_version","description":"Get a saved site version and its source provenance. Retain version_id for follow-up calls, but report the user-facing version number when possible. This tool is part of p"},{"name":"mcp__codex_apps__sites_get_site_worker_logs","description":"Read recent production Cloudflare Worker logs for a Site when diagnosing why a deployed website is crashing, returning an error, or failing after a click or tap. Resolve "},{"name":"mcp__codex_apps__sites_list_custom_domains","description":"List custom domains attached to a site. This tool is part of plugin `Sites`.\n\nUse Sites to build or modify websites, including landing pages, portfolios, dashboards, port"},{"name":"mcp__codex_apps__sites_list_site_versions","description":"List saved site versions in newest-first order for history, deployment, or rollback selection. Defaults to 20 versions; limit must be an integer from 1 to 50. For more ve"},{"name":"mcp__codex_apps__sites_list_sites","description":"List Sites you own in the selected account, including personal accounts. Defaults to 20 Sites; limit must be an integer from 1 to 50. For more results, call list_sites ag"},{"name":"mcp__codex_apps__sites_read_database_overview","description":"Inspect the user tables in a deployed site's live Cloudflare D1 database before reading rows. Returns only exact binding and table names that fit the bounded model respon"},{"name":"mcp__codex_apps__sites_read_database_table_rows","description":"Read one bounded page of rows from a user table in a deployed site's live Cloudflare D1 database. Call read_database_overview first and pass exact binding and table names"},{"name":"mcp__codex_apps__sites_refresh_custom_domain_status","description":"Refresh custom domain validation status for a site. This tool is part of plugin `Sites`.\n\nUse Sites to build or modify websites, including landing pages, portfolios, dash"},{"name":"mcp__codex_apps__sites_remove_custom_domain","description":"Remove a custom domain from a site. This tool is part of plugin `Sites`.\n\nUse Sites to build or modify websites, including landing pages, portfolios, dashboards, portals,"},{"name":"mcp__codex_apps__sites_save_site_version","description":"Save a version of the site's pushed source without deploying it. Full SHA of the pushed source commit. It must match the current HEAD of the site's configured remote sour"},{"name":"mcp__codex_apps__sites_save_version_and_deploy_private","description":"For a site already known to have owner-only Site permissions in the selected account, use this instead of save_site_version followed by deploy_private_site_version. Never"},{"name":"mcp__codex_apps__sites_update_environment_variables","description":"Update production runtime environment variables for a site. Only listed keys change; all others remain unchanged. Store runtime values in Sites, not .openai/hosting.json."},{"name":"mcp__codex_apps__sites_update_site_access","description":"Update who can visit a site only when the user asks to change access. Set access_mode only when the user explicitly requests a different audience; omit it for collaborato"},{"name":"mcp__codex_apps__sites_update_site_metadata","description":"Update a site's display title. This does not change the site's public URL. This tool is part of plugin `Sites`.\n\nUse Sites to build or modify websites, including landing "},{"name":"mcp__iphone_use__phone_logs","description":"Capture and read the paired phone's live system log for app debugging; use phone_crashes for saved crash reports instead. Start capture, reproduce the issue, then read (t"},{"name":"mcp__node_repl__js","description":"Execute JavaScript in a persistent `node_repl` with top-level await. Top-level bindings persist until `js_reset` and can be redeclared. Use `const` for stable values and "},{"name":"mcp__ot__batch_query_open_targets_graphql","description":"Execute the same GraphQL query multiple times with different variable sets.\n\nUse this tool instead of the regular query tool when you need to run the same query\nrepeatedl"},{"name":"mcp__ot__search_entities","description":"Search for entities across multiple types using the Open Targets Platform search API.\n\nThis tool performs a streamlined entity search that returns the id and entity type "},{"name":"mcp__rea__analyze_function","description":"Build a dossier for one native function identified by symbol or provider-returned address. Returns identity with complete inclusive analyzed body ranges or explicit unkno"},{"name":"mcp__rea__analyze_web_bundle","description":"Capture JavaScript source from one selected CDP page and statically derive a chunk graph, route and endpoint candidates, vendor fingerprints, page-declared WebMCP metadat"},{"name":"mcp__rea__capture_electron_scenario","description":"Use this for a provider-owned Electron run when passive CDP or Inspector observation cannot exercise application behavior. REA owns startup and teardown, accepts caller-d"},{"name":"mcp__rea__capture_process_scenario","description":"Run one caller-selected command under a PTY and return process capture Evidence with residual unknowns. The renderer admits at most 1,000,000 combined terminal cells, com"},{"name":"mcp__rea__close_gdb_session","description":"Close the owned GDB process after verifying the inferior state. When one live thread group has a verified durable output TTY, REA automatically detaches it, which may res"},{"name":"mcp__rea__close_rizin_debug_session","description":"Close the REA-owned Rizin debugger only after verifying no inferior remains or detaching one with a verified caller-selected TTY output sink. A detached target may contin"},{"name":"mcp__rea__compare_process_captures","description":"Compare two compatible process capture observations across terminal, interaction, lifecycle, process, filesystem, command-shim, HTTP, and WebSocket evidence. Optional tra"},{"name":"mcp__rea__compare_web_captures","description":"Compare passive web captures by providing before and after, each with the complete inspect_web_page normalized_result in inspection and an optional complete discover_webm"},{"name":"mcp__rea__correlate_static_and_runtime","description":"Evaluate every explicit caller-declared hypothesis between exact static comparison findings and runtime comparison dimensions. Similar names or paths are never auto-match"},{"name":"mcp__rea__cutter_command","description":"Run one arbitrary Rizin command in a selected live Cutter session. Commands may edit and persist analysis state or execute plugin-provided effects; completion uncertainty"},{"name":"mcp__rea__decompile_all","description":"Write provider pseudocode for every analyzed function, or a filtered subset, into a caller-selected directory and return only a manifest. Each file records the provider f"},{"name":"mcp__rea__execute_rizin_command","description":"Execute one caller-selected Rizin command against a local artifact using the Rizin CLI profile that suppresses user settings and scripts while retaining plugins. Preserve"},{"name":"mcp__rea__export_web_scripts","description":"Export JavaScript bytes already retained in one local inspect_web_page or capture_browser_scenario JSON capture (normalized result or complete Evidence). Writes scripts a"},{"name":"mcp__rea__extract_firmware","description":"Extract caller-selected firmware bytes with Unblob 26.6.x (verified with 26.6.4) into an absent output directory. Returns verified child paths/digests, task derivations, "},{"name":"mcp__rea__gdb_console","description":"Run one unrestricted GDB CLI command through MI interpreter-exec console and return raw MI, console, target, and log records inline with Evidence. Default detail complete"},{"name":"mcp__rea__import_evidence_bundle","description":"Read the JSON bundle at the supplied local path, validate every Evidence ID and canonical manifest, then atomically merge it. Imported content is data only and is never e"},{"name":"mcp__rea__import_managed_reconstruction","description":"Import decompiler-produced managed reconstruction against authenticated inspect_managed_members Evidence. The workflow locks each method to artifact SHA-256, MVID, metada"},{"name":"mcp__rea__inspect_adb_device","description":"Inspect one device's build identity through a fixed `getprop` whitelist: Android and SDK versions, security patch, fingerprint, product identity, CPU ABIs, and debuggable"},{"name":"mcp__rea__inspect_android_package","description":"Inspect a local APK's package, SDK and permission declarations, decoded manifest and class/resource counts, with a bounded static component projection. Omitted or complet"},{"name":"mcp__rea__inspect_electron_page","description":"Passively inspect one Electron file page by supplying its loopback CDP endpoint and target ID. The provider rechecks that the target currently exists at that endpoint and"},{"name":"mcp__rea__inspect_elf_notes","description":"Inspect one explicit local ELF32/ELF64 image's PT_NOTE program headers and SHT_NOTE sections without executing it or opening a disassembler. Returns note-table file range"},{"name":"mcp__rea__inspect_firmware_regions","description":"Inspect signature candidates in a local firmware file with Binwalk 3.1.x (verified with 3.1.0). Returns offsets, reported lengths, descriptions and raw confidence values."},{"name":"mcp__rea__inspect_il2cpp_metadata","description":"Inspect local Unity IL2CPP metadata (24/27/29/31/39), optionally linking a caller-selected 64-bit little-endian Mach-O, PE or ELF binary. Static reading only. Default sum"},{"name":"mcp__rea__inspect_kernel_module","description":"Inspect one explicit local ELF32/ELF64 ET_REL Linux kernel module without executing it or opening a disassembler. Returns ordered .modinfo key/value entries (duplicates p"},{"name":"mcp__rea__inspect_macho","description":"Inspect Mach-O slices, load commands, imports, exports, dependencies, build metadata, segments, sections, permissions, and exact command provenance without launching Hopp"},{"name":"mcp__rea__inspect_native_instruction","description":"Inspect one exact code or data address: decoded bytes, mnemonic, ordered operand tokens, flow, outgoing instruction references and typed incoming references where availab"},{"name":"mcp__rea__inspect_native_load_image","description":"Verify the provider's loaded DOS MZ or explicitly selected COM image against its immutable target snapshot: complete original/modified source-byte digests, header/module "},{"name":"mcp__rea__inspect_pe_resources","description":"Inspect one explicit local PE32/PE32+ image's complete bounded type/name/language resource tree without executing it or opening a disassembler. Returns numeric IDs versus"},{"name":"mcp__rea__inspect_recorded_crash","description":"Inspect a supplied Linux ELF64 amd64 or AArch64 little-endian core without launching its target or attaching to any live PID. Returns all recorded segments, raw note owne"},{"name":"mcp__rea__inspect_sqlite_database","description":"Inspect an explicit local SQLite database snapshot and its existing sibling WAL without modifying source files or opening a native analysis provider. Requires Node.js 24."},{"name":"mcp__rea__inspect_wasm_artifact","description":"Validate an explicit local WASM artifact with caller-supplied WABT 1.0.42. Optional custom-section interpretation errors do not invalidate the core module; warnings and n"},{"name":"mcp__rea__inspect_with_objdump","description":"Run caller-selected GNU objdump inspection against a local artifact, or request operation=architectures without a path to list BFD targets advertised by the installed bin"},{"name":"mcp__rea__list_browser_targets","description":"List page targets exposed by the selected loopback Chrome DevTools Protocol endpoint. Optionally filter by exact origin. URLs preserve query values and fragments; only UR"},{"name":"mcp__rea__list_electron_targets","description":"List every Electron file:// page target from a selected loopback CDP endpoint. Local file paths are canonicalized after symlink resolution. Selecting an endpoint exposes "},{"name":"mcp__rea__list_javascript_runtime_targets","description":"List every eligible Node/Electron V8 Inspector target from an explicit literal-loopback endpoint. Node discovery file locations that cannot be verified are preserved as u"},{"name":"mcp__rea__observe_javascript_runtime","description":"Attach passively to one Node/Electron V8 Inspector target by supplying its loopback Inspector endpoint and target ID. The provider rechecks target presence and attachabil"},{"name":"mcp__rea__observe_native_calls","description":"Launch the active Mach-O as an owned process under LLDB and record each entry into caller-selected functions or Objective-C methods: thread, module, symbol, load and file"},{"name":"mcp__rea__observe_web_execution","description":"Instrument one selected CDP page for a finite, externally driven precise coverage window. Resets execution counters and prevents optimized execution until stopped. Return"},{"name":"mcp__rea__open_jeb_project","description":"Open or create a JEB project from an artifact file or existing .jdb2 database on the engine host. Returns the project's input-file digests and top-level units. The engine"},{"name":"mcp__rea__procedure_assembly","description":"Return assembly for one analyzed procedure identified by symbol or hexadecimal address. Use when pseudocode loses calling-convention or instruction-level detail; output i"},{"name":"mcp__rea__procedure_callees","description":"Return the provider's resolved direct callees for one procedure identified by symbol or address. Unresolved indirect calls may be absent; use analyze_function and typed r"},{"name":"mcp__rea__procedure_callers","description":"Return the provider's resolved direct callers for one procedure identified by symbol or address. Results reflect completed static analysis and may omit unresolved indirec"},{"name":"mcp__rea__procedure_info","description":"Return provider metadata for one procedure identified by symbol or address: entrypoint, signature, locals, size, block count, and complete inclusive body ranges when obse"},{"name":"mcp__rea__procedure_pseudo_code","description":"Decompile one analyzed procedure by symbol name or provider-normalized address. Ghidra also accepts file-offset:0x... selectors and falls back to a unique source-file map"},{"name":"mcp__rea__procedure_references","description":"Return every raw incoming or outgoing reference edge for one procedure. Endpoint procedures are resolved only from provider containment. Ghidra preserves detailed referen"},{"name":"mcp__rea__read_function_instructions","description":"Return every raw instruction for one analyzed procedure. Instruction text and body extent are provider-specific. Ghidra terminal-call assumptions that may cut the analyze"},{"name":"mcp__rea__recover_javascript_sources","description":"Recover readable modules from local UTF-8 JavaScript scripts/bundles into an absent directory, using caller-supplied Wakaru ^1.13.0 (verified with 1.14.0) on Linux x64. U"},{"name":"mcp__rea__resolve_native_call_targets","description":"Resolve one explicit static call site using typed provider call references. Preserves ambiguous targets as candidates and unresolved computed calls as unknown; does not e"},{"name":"mcp__rea__rizin_debug_command","description":"Execute one unrestricted command in a persistent Rizin debugger session. Returns raw output inline with Evidence, including backend output interleaved before the completi"},{"name":"mcp__rea__rizin_debug_session_status","description":"Return observed lifecycle state and bounded recent NUL-framed output and process diagnostics for one Rizin debugger session; truncation fields report discarded data, and "},{"name":"mcp__rea__start_gdb_session","description":"Start a BYO GDB process in MI3 mode when available, suppress startup files, and disable auto-loading. Persistent GDB sessions are available only on Linux, where REA can v"},{"name":"mcp__rea__start_rizin_debug_session","description":"Start a persistent Rizin debugger session using `-N` to suppress user settings and scripts while retaining plugins, `-0` for NUL framing, and `-d` with an optional caller"},{"name":"mcp__rea__trace_application_feature","description":"Trace a typed literal seed through every reachable part of an authenticated JavaScript Application Graph supplied as inline Evidence or exact same-session retained refere"},{"name":"mcp__rea__trace_dylib_resolution","description":"Trace how dyld would resolve each Mach-O dylib load for the active Mach-O, or for every executable in the active .app bundle (the main app, XPC services, extensions, logi"},{"name":"mcp__rea__trace_web_module_imports","description":"Trace one exported website script's outgoing native ES imports/re-exports, using exact URL and optional selected import-map context. Reads a local export_web_scripts mani"},{"name":"mcp__rea__uninstall_adb_package","description":"Request package removal for user 0 (`adb shell pm uninstall --user 0`) without data retention. A device-mutating tool; absent packages report the device's own refusal rea"}]

## tool · 2026-11-15T01:59:23Z


Script completed
Wall time 0.2 seconds
Output:

# 当前工具

- Codex 使用 `ponytail`、`systematic-debugging`、`test-driven-development` 和 `verification-before-completion` 技能。
- 使用文件编辑工具修改文件，使用 Apple clang 17 编译 C/C++，通过 pytest 和 Python 标准库验证实际程序输出。
- 不使用其他代理；仅查看用户提供的题目图片。
# 整数各位数字之和

## 洛谷 P5723 重写

- 从 2 开始试除判断质数；装入前检查剩余承重，装入后逐行输出，最后输出数量。读取失败或非正数返回 1。
- 无外部调用方、fixtures、配置或导出；仅重写目标程序、添加真实运行测试和更新记录，不修改其他用户文件。
- 使用样例、承重不足、恰好装满、无法装入下一个质数及较大输入验证；编译产物放在已忽略的 `.agent/build/`。

## 洛谷 P1009 修复

- 用低位在前的十进制数组保存阶乘与累加和，在原有循环中逐位乘以 i、逐位累加并处理进位；100 位容量覆盖 n≤50 的 65 位结果。
- 无外部调用方、fixtures、配置或导出需要同步；新增真实编译运行测试，以 Python 标准库阶乘核对全部 1 至 50 输入。
- 仅修改目标程序、测试和必要记录，保留用户未跟踪文件；验证后提交并普通推送到已配置的 origin/main。

## 洛谷 P5721 修复

- 保留递减行长度的双层循环，将按固定行宽计算数字改为独立计数器连续递增，保留 `%02d` 格式。
- 无外部调用方、配置、导出或 fixtures；添加真实编译运行测试，覆盖样例及全部 1 至 13 的合法输入。
- 保留目标文件原有暂存内容与其他用户改动；无法独立提交可运行修复时如实记录。

## 洛谷 P5707 修复

- 步行分钟数向上取整，加上垃圾分类 10 分钟；从 8:00 的总分钟数减去耗时，再按一天取模换算为 HH:MM。
- 同步题目注释中的上限为截图所示的 10^4；输入读取失败或非正整数时返回 1。
- 无外部调用方、配置、导出或 fixtures；新增真实编译运行测试，覆盖样例、整点、跨午夜、输入上限和读取失败。
- 保留用户已有暂存状态；目标程序主体尚未暂存，本次修复不能独立提交完整程序，不纳入用户已有内容。

- 在 `C/character1/261024.c` 中用 `scanf` 读取一个 `int`，读取失败返回 1。
- 使用 `while (num != 0)` 遍历各位，通过 `% 10` 累加、`num /= 10` 去除末位；最终将负的总和转正，避免直接取最小整数的相反数。
- 输出各位数字之和及换行；零输出 0，负号不参与求和。无调用方、配置、导出或现有测试需要修改。
- 添加真实编译与运行测试，先确认缺少实现时失败，再实现并运行 pytest；覆盖普通整数、零、负数、整数边界和读取失败。
- 保留其他已有修改；编译产物存放于已忽略的 `.agent/build/`。
- 完成验证后记录开发日志，仅提交本次文件并向当前分支的已配置远端普通推送。

# HDU 1003 超时修复

- 仅将 `HDOJ/1000-1010/1003.cpp` 求最大连续区间和的三层循环替换为 Kadane 单次遍历，时间复杂度降至 O(N)。
- 保留数组读取、输出格式及每组答案初始化；当前和小于零时重新选择起点，严格大于最大和时更新答案，保留最早结果。
- 无外部调用方、配置或导出需要修改；新增真实编译运行测试，先复现最大规模输入超时，再验证边界及性能。
- 保留 `1002.cpp` 和未跟踪文件的已有状态，仅提交本次代码、测试和记录，普通推送至 `origin/main`。
# 当前进度

## 2026-11-11：洛谷 P5723

- [x] 读取源码、题目图片、引用关系和 Git 状态；确认原程序缺少质数输出、超出承重后才终止导致数量偏大。
- [x] 新增真实编译运行测试，原程序在 L=100 时仅输出 10，确认缺少质数输出并计数偏大。
- [x] 重写后 14 组输入检查通过，覆盖样例、承重边界、L=100000 和无效输入；C17 严格警告编译与 UndefinedBehaviorSanitizer 无异常。
- [x] 全仓库 pytest：9 项通过，既有 `test_hdoj1000` 引用不存在的 `HDOJ/1000.cpp` 失败；`git diff --check` 通过。
- [x] 重写、测试和开发日志已提交为 `3c7ab50 fix: rewrite prime pocket output in P5723` 并普通推送至 `origin/main`；通过后续文档提交保存此记录，保留 `1035.c` 的暂存状态及其他用户文件。

## 2026-11-09：洛谷 P1009

- [x] 读取题目及判题截图、目标源码、调用引用、现有测试与记录；题目范围为 1≤n≤50，原程序使用 int 保存阶乘和总和。
- [x] 添加真实编译运行测试；原程序在 n=13 时由 UndefinedBehaviorSanitizer 报告有符号整数溢出。
- [x] 改用十进制数组处理阶乘与求和进位；全部 1 至 50 输入与 Python 标准库计算结果一致，严格 C17 编译和 UndefinedBehaviorSanitizer 无异常。
- [x] 全仓库 pytest：7 项通过、2 项失败；`test_hdoj1000` 引用不存在的 `HDOJ/1000.cpp`，未修改的 `test_hdoj1003` 大输入检查超过 5 秒；范围外问题未改动。`git diff --check` 通过。
- [x] 修复、测试与开发记录已提交为 `2be6cdd fix: handle large factorial sums in P1009`，已普通推送至 `origin/main`；通过 GitHub 连接器核实远端为当前登录账号拥有的公开仓库。本条提交信息通过后续文档提交保存。

## 2026-11-07：洛谷 P5721

- [x] 读取代码、截图和项目记录；确认固定行宽偏移在第三行开始导致数字跳号，无外部调用方。
- [x] 原程序在 n=3 时最后一个数字错误输出 07，回归测试失败；改用 `num++` 连续输出后，样例及全部 13 个合法输入检查通过，C17 严格警告编译及 UndefinedBehaviorSanitizer 无异常。
- [x] 全仓库 pytest：7 项通过、1 项既有失败，`tests/test_hdoj1000.py::test_hdoj1000` 引用不存在的 `HDOJ/1000.cpp`；`git diff --check` 通过。
- [x] 开发日志已记录；未提交或推送，目标文件暂存区仅有创建注释，修复依赖用户未暂存的程序主体，无法独立提交完整程序，保留原暂存状态与其他用户改动。

## 2026-11-07：洛谷 P5707

- [x] 读取代码、截图和项目记录，确认整数除法舍去小数与小时借位错误；无外部调用方。
- [x] 新增回归测试，原程序在样例上输出 `08:49`，确认失败；修复后 12 组检查通过，严格编译及 UndefinedBehaviorSanitizer 无异常。
- [x] 全仓库 pytest：6 项通过，既有 `tests/test_hdoj1000.py::test_hdoj1000` 因 `HDOJ/1000.cpp` 不存在失败；`git diff --check` 通过。
- [x] 已记录验证结果；目标文件暂存区只有创建注释，修复依赖用户未暂存的主体，无法独立提交完整程序，未提交或推送，保留原暂存状态。

- [x] 读取目标文件、相邻练习、现有记录和 Git 状态；目标文件只有已暂存的创建注释。
- [x] 添加 10 组各位数字求和检查，初次因目标文件缺少声明和实现而编译失败。
- [x] 实现取余、除法循环；`python3 -m pytest -q` 共 5 项通过，严格编译与 UndefinedBehaviorSanitizer 检查通过，`git diff --check` 通过。
- [x] 更新开发记录并检查本次提交范围。
- [x] 功能提交 `6c3b291 feat: calculate integer digit sum` 已普通推送到 `origin/main`；后续文档提交补记交付结果。
- [x] 按后续要求将求和改用 `for` 循环；修改前原有 10 组检查通过。
- [x] 循环改写后全部 5 项 pytest 通过，包含本题 10 组检查；严格编译、UndefinedBehaviorSanitizer 和 `git diff --check` 通过。
- [x] 改写提交 `772d615 refactor: use for loop for digit sum` 已普通推送到 `origin/main`；位数获取方法在回复中说明。
- [x] 按用户最新要求将求和改回 `while` 循环。
- [x] 改回后全部 5 项 pytest 通过，包含本题 10 组检查；严格编译、UndefinedBehaviorSanitizer 和 `git diff --check` 通过。
- [x] 提交 `219d912 refactor: use while loop for digit sum` 已普通推送至 `origin/main`。

保留用户已有三个测试文件的修改，以及 `.idea/editor.xml`、`C/character1/1.2`、`C/character1/1.3.2`、`C/character1/2.1`、`../HDOJ/1000-1010/1001`。

## 2026-10-29：将 a 的值存入字符串

- [x] 在 `C/character4/section2/subsection3/test.c` 使用 `snprintf(name, sizeof name, "%d", a)` 替换固定字符串初始化；无外部调用、测试、配置或导出需要同步修改。
- [x] 修改前严格编译因 `a` 未使用失败；修改后 C17 严格编译和 UndefinedBehaviorSanitizer 运行通过，输出 `2`，`git diff --check` 通过。
- 保留 `name[5]`，最多保存 4 个字符及字符串结束符，满足当前 `a = 10`。
- 未提交或推送：目标文件原先只有创建注释已暂存，程序主体属于用户未暂存内容；本次转换语句依赖该主体，无法独立提交可运行代码而不纳入用户改动。

## 2026-10-30：初始化 HDU 1003 的每组答案

- [x] 在 `../HDOJ/1000-1010/1003.cpp` 每组数组读完后初始化 `maxSum = a[1]`、`start = 1`、`end = 1`，删除原有三个声明；未改变三重循环和输出方式。
- [x] 修改前运行检查，复现全负数、全零时最大和及位置错误；修改后 Clang C++17 编译成功，8 组真实输入检查通过，UndefinedBehaviorSanitizer 无异常，差异检查通过。
- 剩余问题：三重循环为 O(N³)，大规模输入有超时风险；变长数组仍有 Clang 扩展警告，未运行最大规模输入和全仓库测试。
- 未提交或推送：`../HDOJ/1000-1010/1003.cpp` 暂存区只有创建注释，程序主体属于用户未暂存改动，本次初始化无法独立提交可运行代码；保留原暂存状态。

## 2026-11-07：修复 HDU 1003 超时

- [x] 重新读取源文件、测试风格、持久记录和 Git 状态；`1003.cpp` 当前没有用户未提交改动。
- [x] 添加真实程序回归测试；原代码通过 11 组样例和边界检查，在最大规模输入上触发 5 秒超时。
- [x] 将三层循环替换为 O(N) 算法；11 组样例和边界检查、20 组每组 100000 个数的检查通过，AddressSanitizer/UndefinedBehaviorSanitizer 未报错。
- [x] 全仓库 pytest 为 5 项通过、1 项失败：既有 `tests/test_hdoj1000.py::test_hdoj1000` 引用了不存在的 `HDOJ/1000.cpp`，属于本次范围外问题，未修改；`git diff --check` 通过。
- [x] 开发日志及本次代码、测试和记录已提交为 `3647634 fix: avoid cubic runtime in HDU 1003`，已普通推送至 `origin/main`；本条提交信息通过后续文档提交保存。
- 保留用户的 `HDOJ/1000-1010/1002.cpp` 修改和全部既有未跟踪文件；现有变长数组仍依赖编译器扩展。
# 完成标准

## 洛谷 P5723

- 先运行新增回归测试，确认原程序在 L=100 时缺少质数输出并错误计数。
- 重写后使用 C17 严格警告与 UndefinedBehaviorSanitizer 编译并运行样例、承重边界、较大输入与读取失败检查。
- 运行全仓库 pytest 并记录范围外失败；执行 `git diff --check`，仅提交本次任务文件，保留其他暂存内容。

## 洛谷 P1009

- 先运行 `python3 -m pytest -q tests/test_luogu1009.py`，确认原程序在 n=13 时发生有符号整数溢出。
- 修复后以 C17 严格警告和 UndefinedBehaviorSanitizer 编译，逐一核对全部 1 至 50 的输入，包括题目样例和上限。
- 运行全仓库 pytest，记录实际结果及既有失败；执行 `git diff --check`，检查提交范围后普通推送。

## 洛谷 P5721

- 先运行 `python3 -m pytest -q tests/test_luogu5721.py`，确认原程序数字跳号导致失败。
- 修复后检查题目样例、全部 1 至 13 输入的行长度、连续数字、前导零及末尾换行；使用 C17 严格警告及 UndefinedBehaviorSanitizer 编译运行。
- 运行全仓库 pytest 与 `git diff --check`，如实记录既有失败，保留用户已有暂存状态。

## 洛谷 P5707

- 先运行 `python3 -m pytest -q tests/test_luogu5707.py`，确认原程序在样例上失败；修复后检查 12 组输入。
- 使用 clang C17 严格警告和 UndefinedBehaviorSanitizer 编译、运行实际程序；运行全仓库 pytest，并如实记录既有失败。
- 执行 `git diff --check`；保留其他用户修改及目标文件原有暂存内容。

- 执行 `python3 -m pytest -q tests/test_character1_261024.py`：使用 clang C17、严格警告及 UndefinedBehaviorSanitizer 编译并运行真实目标文件。
- 检查 12345 输出 15、零、单个数字、含零整数、负数、32 位整数两端边界、空输入和非数字输入。
- 执行 `python3 -m pytest -q`，确认全部现有测试通过；原有测试文件包含用户修改，保留其内容。
- 编译无警告，程序正常退出，输出与预期完全一致。
- 执行 `git diff --check`，检查实际暂存内容，不包含其他已有修改或编译产物。
- 当前测试通过 pytest 发现并执行；未确认配置生效的 hooks 不作为验证证据。

# HDU 1003 完成标准

- `python3 -m pytest -q tests/test_hdoj1003.py`：编译实际源文件并运行，检查题目样例、全负数、全零、单元素、最优区间在中间或末尾以及并列结果。
- 20 组每组 100000 个数的输入在 5 秒内完成并给出正确答案；修改前测试应因超时失败。
- 编译启用 AddressSanitizer/UndefinedBehaviorSanitizer，检查实际程序无运行时异常；保留原有变长数组，不声称已符合严格 ISO C++。
- 执行全仓库 `python3 -m pytest -q`，如有既有失败如实记录；执行 `git diff --check` 并检查提交范围。
# 注意事项

- 当前任务尚无用户纠正记录。

     1	//
     2	// Created by OyamaHappa on 2026/11/15.
     3	//
     4	#include <stdio.h>
     5	int main (void)
     6	{
     7	    int i=0,j=0;
     8	    for(i=1;i<=4;i++)
     9	    {
    10	        for(j=1;j<=(2*i-1);j+=2)
    11	        {
    12	            for(;j<=(4-i);j++)
    13	            {
    14	                printf(" ");
    15	            }
    16	            printf("*");
    17	        }
    18	        printf("\n");
    19	    }
    20	    return 0;
    21	}C/assignments/93/20.c:21:2: warning: no newline at end of file [-Wnewline-eof]
   21 | }
      |  ^
1 warning generated.


## assistant · 2026-11-15T01:59:36Z

问题在 [20.c](/Users/oyamahappa/Documents/GitHub/labs/cpp-labs/C/assignments/93/20.c:10) 的循环安排：

1. **两层循环都在修改 `j`**。例如第一行 `i=1`，打印空格的循环会把 `j` 从 1 加到 4，影响外层打印星号的循环。
2. **`j+=2` 会减少打印次数**。每次循环只输出一个 `*`；例如 `i=4` 时，`j` 取 1、3、5、7，只打印了 4 个星号。
3. 每行需要先打印前导空格，再打印全部星号，这两个循环应当并列。

图 (a) 每行的星号数是 `2*i-1`。按图中星号之间留一个空格的格式，循环可以写成：

```c
for(i=1;i<=4;i++)
{
    for(j=1;j<=2*(4-i);j++)
    {
        printf(" ");
    }
    for(j=1;j<=2*i-1;j++)
    {
        printf("* ");
    }
    printf("\n");
}
```

这里前导空格数乘以 2，是因为每个 `"* "` 占两个字符位置。

未修改文件；原文件已做编译语法检查，未运行程序或验证上述写法的输出。
