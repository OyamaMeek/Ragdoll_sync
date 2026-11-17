# 是否应该填写 key

来源：codex

项目：/Users/oyamahappa/Documents/GitHub/labs/py-labs

## developer · 2026-11-17T08:28:33Z

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



## developer · 2026-11-17T08:28:33Z

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
- `r15` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/app-6aa2c81fc7c48191a06e101858e41837/2.1.7/skills`
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/heygen/4.8.0/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.6/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1116.12020/skills`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.2/skills`
- `r27` = `/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.agents/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI- (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, setti (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped ins (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated  (file: r2/skill-installer/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:database-access: Explore and query databases on the user's servers (Postgres, M (file: r15/database-access/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:deploy-check: Verify a server after a deployment, update or restart — servic (file: r15/deploy-check/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:incident-triage: Work through a server alert or outage step by step — disk fu (file: r15/incident-triage/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:run-commands: Run shell commands and edit files on the user's servers thro (file: r15/run-commands/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:server-health: Answer "how are my servers doing", "is everything up", "anythi (file: r15/server-health/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motio (file: r1/apple-design/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motio (file: r0/apple-design/SKILL.md)
- archify: Create polished, validated architecture, workflow, sequence, (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Codex research, writing, manuscript review, study screenin (file: r3/ars-codex/3.24.2/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Structures Benchmark and Evaluation papers using the five-pill (file: r0/benchmark-paper-template/SKILL.md)
- bio-research:instrument-data-to-allotrope: Convert laboratory instrument output files (PDF, CSV, Excel,  (file: r4/instrument-data-to-allotrope/SKILL.md)
- bio-research:nextflow-development: Run nf-core bioinformatics pipelines (rnaseq, sarek, atacseq) (file: r4/nextflow-development/SKILL.md)
- bio-research:scientific-problem-selection: This skill should be used when scientists need help with rese (file: r4/scientific-problem-selection/SKILL.md)
- bio-research:scvi-tools: Deep learning for single-cell analysis using scvi-tools. This (file: r4/scvi-tools/SKILL.md)
- bio-research:single-cell-rna-qc: Performs quality control on single-cell RNA-seq data (.h5ad o (file: r4/single-cell-rna-qc/SKILL.md)
- bio-research:start: Set up your bio-research environment and explore available  (file: r4/start/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end (file: r0/brandkit/SKILL.md)
- cli-anything: Use when the user wants Codex to build, refine, test, validate (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Discover agent-native CLIs for professional software. Access t (file: r0/cli-hub-meta-skill/SKILL.md)
- code-review: Review the changes since a fixed point (commit, branch, tag, (file: r0/code-review/SKILL.md)
- code-search: Instructions for MCP code search tools. Use when you need t (file: r27/code-search/SKILL.md)
- codebase-design: Shared vocabulary for designing deep modules. Use when the u (file: r0/codebase-design/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准 (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Convert Word (.doc, .docx), PowerPoint (.ppt, .pptx), Excel  (file: r1/convert-documents-to-markdown/SKILL.md)
- cowork-plugin-management:cowork-plugin-customizer: Customize a Claude Code plugin for a specific organization's  (file: r5/cowork-plugin-customizer/SKILL.md)
- cowork-plugin-management:create-cowork-plugin: Guide users through creating a new plugin from scratch in a c (file: r5/create-cowork-plugin/SKILL.md)
- customer-support:customer-escalation: Package an escalation for engineering, product, or leadersh (file: r6/customer-escalation/SKILL.md)
- customer-support:customer-research: Multi-source research on a customer question or topic with  (file: r6/customer-research/SKILL.md)
- customer-support:draft-response: Draft a professional customer-facing response tailored to the (file: r6/draft-response/SKILL.md)
- customer-support:kb-article: Draft a knowledge base article from a resolved issue or commo (file: r6/kb-article/SKILL.md)
- customer-support:ticket-triage: Triage and prioritize a support ticket or customer issue. U (file: r6/ticket-triage/SKILL.md)
- data:analyze: Answer data questions -- from quick lookups to full analyse (file: r7/analyze/SKILL.md)
- data:build-dashboard: Build an interactive HTML dashboard with charts, filters, a (file: r7/build-dashboard/SKILL.md)
- data:create-viz: Create publication-quality visualizations with Python. Use wh (file: r7/create-viz/SKILL.md)
- data:data-context-extractor: Generate or improve a company-specific data analysis skill by (file: r7/data-context-extractor/SKILL.md)
- data:data-visualization: Create effective data visualizations with Python (matplotlib, (file: r7/data-visualization/SKILL.md)
- data:explore-data: Profile and explore a dataset to understand its shape, qualit (file: r7/explore-data/SKILL.md)
- data:sql-queries: Write correct, performant SQL across all major data warehou (file: r7/sql-queries/SKILL.md)
- data:statistical-analysis: Apply statistical methods including descriptive stats, trend  (file: r7/statistical-analysis/SKILL.md)
- data:validate-data: QA an analysis before sharing -- methodology, accuracy, and (file: r7/validate-data/SKILL.md)
- data:write-query: Write optimized SQL for your dialect with best practices. U (file: r7/write-query/SKILL.md)
- deep-research: Runs a deep, survey-grade literature investigation on a rese (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects dependin (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-dri (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diagnosis loop for hard bugs and performance regressions. Us (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r21/documents/26.1116.12020/skills/documents/SKILL.md)
- domain-modeling: Build and sharpen a project's domain model. Use when discuss (file: r0/domain-modeling/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable D (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it  (file: r1/ego-browser/SKILL.md)
- enterprise-search:digest: Generate a daily or weekly digest of activity across all con (file: r8/digest/SKILL.md)
- enterprise-search:knowledge-synthesis: Combines search results from multiple sources into coherent, d (file: r8/knowledge-synthesis/SKILL.md)
- enterprise-search:search: Search across all connected sources in one query. Trigger wi (file: r8/search/SKILL.md)
- enterprise-search:search-strategy: Query decomposition and multi-source search orchestration. Bre (file: r8/search-strategy/SKILL.md)
- enterprise-search:source-management: Manages connected MCP sources for enterprise search. Detects a (file: r8/source-management/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用 (file: r0/evidence-recap/SKILL.md)
- figure-designer: Advises on the design of the three core figures in a technic (file: r0/figure-designer/SKILL.md)
- finance:audit-support: Support SOX 404 compliance with control testing methodology, (file: r9/audit-support/SKILL.md)
- finance:close-management: Manage the month-end close process with task sequencing, depen (file: r9/close-management/SKILL.md)
- finance:financial-statements: Generate financial statements (income statement, balance sheet (file: r9/financial-statements/SKILL.md)
- finance:journal-entry: Prepare journal entries with proper debits, credits, and sup (file: r9/journal-entry/SKILL.md)
- finance:journal-entry-prep: Prepare journal entries with proper debits, credits, and suppo (file: r9/journal-entry-prep/SKILL.md)
- finance:reconciliation: Reconcile accounts by comparing GL balances to subledgers, ban (file: r9/reconciliation/SKILL.md)
- finance:sox-testing: Generate SOX sample selections, testing workpapers, and cont (file: r9/sox-testing/SKILL.md)
- finance:variance-analysis: Decompose financial variances into drivers with narrative ex (file: r9/variance-analysis/SKILL.md)
- frontend-design: Guidance for distinctive, intentional visual design when bui (file: r0/frontend-design/SKILL.md)
- full-output-enforcement: Overrides default LLM truncation behavior. Enforces complet (file: r0/output-skill/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Elite UX/UI & Advanced GSAP Motion Engineer. Enforces Pytho (file: r0/gpt-tasteskill/SKILL.md)
- graphify: Use for any question about a codebase, its architecture, file  (file: r0/graphify/SKILL.md)
- great-resume: 中文求职经历提升技能：根据目标岗位把真实经历重组为岗位定位、简历要点、项目亮点和 HR 开场白；当用户输入“/great-r (file: r0/great-resume/SKILL.md)
- grilling: Grill the user relentlessly about a plan, decision, or idea. U (file: r0/grilling/SKILL.md)
- gsap-core: Official GSAP skill for the core API — gsap.to(), from(), from (file: r0/gsap-core/SKILL.md)
- gsap-frameworks: Official GSAP skill for Vue, Svelte, and other non-React fra (file: r0/gsap-frameworks/SKILL.md)
- gsap-performance: Official GSAP skill for performance — prefer transforms, avo (file: r0/gsap-performance/SKILL.md)
- gsap-plugins: Official GSAP skill for GSAP plugins — registration, ScrollT (file: r0/gsap-plugins/SKILL.md)
- gsap-react: Official GSAP skill for React — useGSAP hook, refs, gsap.con (file: r0/gsap-react/SKILL.md)
- gsap-scrolltrigger: Official GSAP skill for ScrollTrigger — scroll-linked animat (file: r0/gsap-scrolltrigger/SKILL.md)
- gsap-timeline: Official GSAP skill for timelines — gsap.timeline(), position  (file: r0/gsap-timeline/SKILL.md)
- gsap-utils: Official GSAP skill for gsap.utils — clamp, mapRange, normal (file: r0/gsap-utils/SKILL.md)
- heygen:animated-short: Create bold, stylized animated short films of 10 to 30 seconds (file: r16/animated-short/SKILL.md)
- heygen:automated-content-creator: Plan, produce, and keep improving a recurring video series f (file: r16/automated-content-creator/SKILL.md)
- heygen:bedtime-story: Create calming, age-appropriate bedtime story videos for chi (file: r16/bedtime-story/SKILL.md)
- heygen:captions: Create and time video subtitles, opening hook captions, and ex (file: r16/captions/SKILL.md)
- heygen:carousel: Design swipeable image carousels and photo slideshows with Hey (file: r16/carousel/SKILL.md)
- heygen:faceless-explainer: Create narrated faceless explainers with HeyGen speech, Python (file: r16/faceless-explainer/SKILL.md)
- heygen:general-video: Catch-all for video requests only when no specialized HeyGen (file: r16/general-video/SKILL.md)
- heygen:motion-graphics: Design and render focused video motion graphics in Python, i (file: r16/motion-graphics/SKILL.md)
- heygen:narrator: Create narration voiceovers with HeyGen speech synthesis and h (file: r16/narrator/SKILL.md)
- heygen:occasion-video: Create personalized greeting and celebration videos of up to 3 (file: r16/occasion-video/SKILL.md)
- heygen:old-photo-revival: Bring old photos to life. Restore, repair, and colorize a vi (file: r16/old-photo-revival/SKILL.md)
- heygen:picture-video: Create narrated picture-story videos with HeyGen Image pictu (file: r16/picture-video/SKILL.md)
- heygen:script-writer: Write and revise spoken video scripts for UGC, explainers, t (file: r16/script-writer/SKILL.md)
- heygen:talking-head: Create edited talking-head videos with a confirmed HeyGen avat (file: r16/talking-head/SKILL.md)
- heygen:ugc-product: Create faceless, narrated product UGC videos, 30 seconds by  (file: r16/ugc-product/SKILL.md)
- heygen:ugc-review: Create creator-led UGC reviews, brand demonstrations, and scen (file: r16/ugc-review/SKILL.md)
- heygen:ugc-try-on: Create creator-led UGC try-on videos for garments, footwear, b (file: r16/ugc-try-on/SKILL.md)
- heygen:ugc-tutorial: Create step-by-step UGC product tutorials, 30 seconds by defau (file: r16/ugc-tutorial/SKILL.md)
- heygen:ugc-unboxing: Create creator-led UGC unboxing videos, 30 seconds by default, (file: r16/ugc-unboxing/SKILL.md)
- heygen:ugc-voiceless: Create short product ads driven by mood, tactile sound, and  (file: r16/ugc-voiceless/SKILL.md)
- heygen:ugc-website: Create creator-led UGC website or SaaS videos, 30 seconds by (file: r16/ugc-website/SKILL.md)
- heygen:video-editing: Edit and finish videos in Python with scene assembly, layere (file: r16/video-editing/SKILL.md)
- high-end-visual-design: Teaches the AI to design like a high-end agency. Defines the e (file: r0/soft-skill/SKILL.md)
- human-writing: 通用中文创作与改稿 Skill。用于知乎回答、论坛长帖、公众号文章、博客、评论、人物故事、历史叙事、新闻与行业解读、科普 (file: r0/human-writing/SKILL.md)
- humanizer:humanizer: Rewrite AI-sounding text so it reads like the writer without c (file: r1/humanizer/SKILL.md)
- humanizer:humanizer: Rewrite AI-sounding text so it reads like the writer without c (file: r0/humanizer/SKILL.md)
- hyperframes: Read first to make, edit, animate or render any video with H (file: r0/hyperframes/SKILL.md)
- hyperframes-cli: The HyperFrames CLI by job - scaffold, check, look at frames (file: r0/hyperframes-cli/SKILL.md)
- hyperframes-registry: About 450 ready-made HyperFrames blocks and components install (file: r0/hyperframes-registry/SKILL.md)
- idea-evaluator: Evaluates a preliminary research idea against a five-dimension (file: r0/idea-evaluator/SKILL.md)
- image-to-code: Elite website image-to-code skill for Codex. For visually impo (file: r0/image-to-code-skill/SKILL.md)
- imagegen-frontend-mobile: Elite mobile app image-generation skill for creating premium,  (file: r0/imagegen-frontend-mobile/SKILL.md)
- imagegen-frontend-web: Elite frontend image-direction skill for generating premium, (file: r0/imagegen-frontend-web/SKILL.md)
- industrial-brutalist-ui: Raw mechanical interfaces fusing Swiss typographic print wit (file: r0/brutalist-skill/SKILL.md)
- interview: 中文简历与目标岗位驱动的面试预测、模拟追问和复练技能：提取需要验证的经历 Claim，按面试轮次建立问题与评分契约，通过 (file: r0/interview/SKILL.md)
- intro-drafter: Drafts the Introduction prose for a technical paper, guided  (file: r0/intro-drafter/SKILL.md)
- iphone-use: Use when a task needs a real iPhone — operating iOS apps tha (file: r1/iphone-use/SKILL.md)
- job-apply: 中文求职申请自动填写技能：使用浏览器读取用户确认的简历资料，逐项填写招聘网站申请表并核对结果；当用户输入“/job-appl (file: r0/job-apply/SKILL.md)
- job-match: 中文岗位匹配分析技能：对照目标 JD 与用户已确认的简历、经历或主张—证据账本，区分已匹配、证据不足和真实缺口，生成可解 (file: r0/job-match/SKILL.md)
- jupyter: Create, inspect, edit, and execute Jupyter .ipynb notebooks (file: r27/jupyter/SKILL.md)
- legal:brief: Generate contextual briefings for legal work — daily summar (file: r10/brief/SKILL.md)
- legal:compliance-check: Run a compliance check on a proposed action, product featur (file: r10/compliance-check/SKILL.md)
- legal:legal-response: Generate a response to a common legal inquiry using configu (file: r10/legal-response/SKILL.md)
- legal:legal-risk-assessment: Assess and classify legal risks using a severity-by-likelihoo (file: r10/legal-risk-assessment/SKILL.md)
- legal:meeting-briefing: Prepare structured briefings for meetings with legal releva (file: r10/meeting-briefing/SKILL.md)
- legal:review-contract: Review a contract against your organization's negotiation pla (file: r10/review-contract/SKILL.md)
- legal:signature-request: Prepare and route a document for e-signature — run a pre-si (file: r10/signature-request/SKILL.md)
- legal:triage-nda: Rapidly triage an incoming NDA and classify it as GREEN (st (file: r10/triage-nda/SKILL.md)
- legal:vendor-check: Check the status of existing agreements with a vendor acros (file: r10/vendor-check/SKILL.md)
- lemo-opuscar: Direct and produce a short film made entirely in code, in one  (file: r0/lemo-opuscar/SKILL.md)
- make-resume: 中文可编辑简历制作技能：默认基于 ASu 单栏高密度技术简历模板，根据用户经历制作或复刻可编辑 HTML/PDF；用户也 (file: r0/make-resume/SKILL.md)
- marketing:brand-review: Review content against your brand voice, style guide, and m (file: r11/brand-review/SKILL.md)
- marketing:campaign-plan: Generate a full campaign brief with objectives, audience, mes (file: r11/campaign-plan/SKILL.md)
- marketing:competitive-brief: Research competitors and generate a positioning and messaging (file: r11/competitive-brief/SKILL.md)
- marketing:content-creation: Draft marketing content across channels — blog posts, social  (file: r11/content-creation/SKILL.md)
- marketing:draft-content: Draft blog posts, social media, email newsletters, landing pa (file: r11/draft-content/SKILL.md)
- marketing:email-sequence: Design and draft multi-email sequences with full copy, timi (file: r11/email-sequence/SKILL.md)
- marketing:performance-report: Build a marketing performance report with key metrics, tren (file: r11/performance-report/SKILL.md)
- marketing:seo-audit: Run a comprehensive SEO audit — keyword research, on-page a (file: r11/seo-audit/SKILL.md)
- media-use: Get or make any media for a HyperFrames video - music, sound (file: r0/media-use/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, ty (file: r0/minimalist-skill/SKILL.md)
- offer: 中文秋招求职进度管理技能：记录和更新投递、筛选、测评、面试、Offer、拒信及招聘邮件状态，生成可搜索的进度表；当用户 (file: r0/offer/SKILL.md)
- paper-polish: Polishes existing academic prose while preserving the author's (file: r0/paper-polish/SKILL.md)
- paper-writer: Drafts publishable paper prose from the author's own materials (file: r0/paper-writer/SKILL.md)
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著 (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包， (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where  (file: r21/pdf/26.1116.12020/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permiss (file: r17/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves  (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what br (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from  (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands.  (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe (file: r23/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across fiv (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Us (file: r21/presentations/26.1116.12020/skills/presentations/SKILL.md)
- product-management:competitive-brief: Create a competitive analysis brief for one or more competit (file: r12/competitive-brief/SKILL.md)
- product-management:metrics-review: Review and analyze product metrics with trend analysis and (file: r12/metrics-review/SKILL.md)
- product-management:product-brainstorming: Brainstorm product ideas, explore problem spaces, and challe (file: r12/product-brainstorming/SKILL.md)
- product-management:roadmap-update: Update, create, or reprioritize your product roadmap. Use  (file: r12/roadmap-update/SKILL.md)
- product-management:sprint-planning: Plan a sprint — scope work, estimate capacity, set goals,  (file: r12/sprint-planning/SKILL.md)
- product-management:stakeholder-update: Generate a stakeholder update tailored to audience and cad (file: r12/stakeholder-update/SKILL.md)
- product-management:synthesize-research: Synthesize user research from interviews, surveys, and feedb (file: r12/synthesize-research/SKILL.md)
- product-management:write-spec: Write a feature spec or PRD from a problem statement or fe (file: r12/write-spec/SKILL.md)
- productivity:memory-management: Two-tier memory system that makes Claude a true workplace  (file: r13/memory-management/SKILL.md)
- productivity:start: Initialize the productivity system and open the dashboard. (file: r13/start/SKILL.md)
- productivity:task-management: Simple task management using a shared TASKS.md file. Refer (file: r13/task-management/SKILL.md)
- productivity:update: Sync tasks and refresh memory from your current activity. Us (file: r13/update/SKILL.md)
- project-guide: 中文项目导学、源码课程与项目面经技能：基于本地项目仓库、项目描述或技术材料，按需生成源码课程与理解题，或生成 导学-{ (file: r0/project-guide/SKILL.md)
- prototype: Build a throwaway prototype to answer a design question. Use (file: r0/prototype/SKILL.md)
- python-tools: PyCharm environment tools. MUST be consulted before running A (file: r27/python-tools/SKILL.md)
- rebuttal-guidance: Provides actionable peer-review rebuttal guidance (not full  (file: r0/rebuttal-guidance/SKILL.md)
- redesign-existing-projects: Upgrades existing websites and apps to premium quality. Au (file: r0/redesign-skill/SKILL.md)
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
- research: Investigate a question against high-trust primary sources  (file: r0/research/SKILL.md)
- reverse-engineer-anything: Reverse engineer native, managed, Electron/JavaScript, packa (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized r (file: r24/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sales:account-context: 360-degree view of an account - CRM data, recent email thread (file: r14/account-context/SKILL.md)
- sales:account-plan: Build or refresh a strategic account plan - current state,  (file: r14/account-plan/SKILL.md)
- sales:account-research: Research a target company and optionally a specific contact (file: r14/account-research/SKILL.md)
- sales:account-tiering: Score and tier a list of accounts (or your full book) against (file: r14/account-tiering/SKILL.md)
- sales:call-prep: Pre-call brief for an upcoming meeting - attendees, account h (file: r14/call-prep/SKILL.md)
- sales:call-summary: Turn a call transcript or call notes into a customer follow (file: r14/call-summary/SKILL.md)
- sales:close-plan: Build the business case and mutual action plan for a deal - (file: r14/close-plan/SKILL.md)
- sales:competitive-intelligence: Competitive analysis two ways - the in-deal play against a  (file: r14/competitive-intelligence/SKILL.md)
- sales:create-an-asset: Build a customer deck, one-pager or leave-behind from your ac (file: r14/create-an-asset/SKILL.md)
- sales:crm-hygiene-check: Read-only audit of your CRM opportunities for missing fields, (file: r14/crm-hygiene-check/SKILL.md)
- sales:customer-health: Health check on a customer account and QBR-ready prep - relat (file: r14/customer-health/SKILL.md)
- sales:customer-voice: Surface what customers are actually saying - direct attribu (file: r14/customer-voice/SKILL.md)
- sales:daily-briefing: Morning rundown - today's meetings with account context, op (file: r14/daily-briefing/SKILL.md)
- sales:deal-advance-gap: Forward-looking gap check on one opportunity - exactly what (file: r14/deal-advance-gap/SKILL.md)
- sales:deal-review: Deep-dive on a single opportunity - signal-adjusted health sc (file: r14/deal-review/SKILL.md)
- sales:deal-signals: Proactive watch over your book - deals gone quiet, close da (file: r14/deal-signals/SKILL.md)
- sales:deal-slip-scenario: Model what happens to your number if a deal slips, shrinks, (file: r14/deal-slip-scenario/SKILL.md)
- sales:draft-outreach: Draft a personalized outreach email or multi-touch sequence (file: r14/draft-outreach/SKILL.md)
- sales:end-of-day: The closing beat of the day - every call processed or expli (file: r14/end-of-day/SKILL.md)
- sales:expansion-whitespace: Find the expansion whitespace in an account or a book - wha (file: r14/expansion-whitespace/SKILL.md)
- sales:forecast: Generate the commit / best-case / pipeline narrative for a  (file: r14/forecast/SKILL.md)
- sales:handle-objection: Work through a live objection or competitive threat - what' (file: r14/handle-objection/SKILL.md)
- sales:inbox-sweep: Batch-process unread customer emails - classify, prioritize,  (file: r14/inbox-sweep/SKILL.md)
- sales:lead-triage: Score and route an inbound lead, or rank a backlog of leads,  (file: r14/lead-triage/SKILL.md)
- sales:log-activity: Log a call, meeting, or email exchange to the CRM after the (file: r14/log-activity/SKILL.md)
- sales:pipeline-review: Stage-by-stage pipeline health check - coverage, aging, conve (file: r14/pipeline-review/SKILL.md)
- sales:renewal-radar: Upcoming renewals with timing, risk, and uplift potential - a (file: r14/renewal-radar/SKILL.md)
- sales:rep-context: Leader's prep on a single rep before a 1:1 - their pipeline,  (file: r14/rep-context/SKILL.md)
- sales:route-lead: Decide who owns an unrouted lead or opportunity and manage  (file: r14/route-lead/SKILL.md)
- sales:schedule-meeting: Find a time, draft the invite, and book the meeting on Goog (file: r14/schedule-meeting/SKILL.md)
- sales:setup: First-run setup - checks which tools are connected, shows wha (file: r14/setup/SKILL.md)
- sales:stakeholder-map: Map the people in a deal or account - roles, influence, senti (file: r14/stakeholder-map/SKILL.md)
- sales:team-pipeline: Leader view - roll up a team's pipeline by rep and stage, fla (file: r14/team-pipeline/SKILL.md)
- sales:update-opportunity: Guided updates to an opportunity - push the stage, move the (file: r14/update-opportunity/SKILL.md)
- sales:weekly-wrap: End-of-week summary for a rep or leader - what closed, what m (file: r14/weekly-wrap/SKILL.md)
- sales:win-loss-review: Analyze recently closed opportunities to find patterns in wha (file: r14/win-loss-review/SKILL.md)
- security-audit: Security guidance and vulnerability review for codebases,  (file: r0/security-audit/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction a (file: r25/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Heming (file: r25/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a fu (file: r25/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for mini (file: r25/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnos (file: r25/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new (file: r25/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching,  (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (inclu (file: r18/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use (file: r18/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, vis (file: r22/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through t (file: r22/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates a (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating featu (file: r19/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating featu (file: r26/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r19/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r26/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on  (file: r19/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on  (file: r26/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current se (file: r19/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current se (file: r26/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r19/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r26/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementin (file: r19/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementin (file: r26/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r19/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r26/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent ta (file: r19/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent ta (file: r26/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r19/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r26/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing (file: r19/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing (file: r26/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from cu (file: r19/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from cu (file: r26/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to fin (file: r19/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to fin (file: r26/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r19/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r26/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step t (file: r19/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step t (file: r26/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r19/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r26/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build fe (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz  (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-templa (file: r21/template-creator/26.1116.12020/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe C (file: r0/vibe-research-workflow/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human thr (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an a (file: r20/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in (file: r20/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet  (file: r20/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing (file: r0/writing-for-agents/SKILL.md)
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
- Gmail (gmail@openai-curated-remote)
- Google Calendar (google-calendar@openai-curated-remote)
- Google Drive (google-drive@openai-curated-remote)
- Linear (linear@openai-curated-remote)
- Notion (notion@openai-curated-remote)
- OpenAI Developers (openai-developers@openai-curated-remote)
- Outlook Calendar (outlook-calendar@openai-curated-remote)
- Outlook Email (outlook-email@openai-curated-remote)
- SharePoint (sharepoint@openai-curated-remote)
- Slack (slack@openai-curated-remote)
- Teams (teams@openai-curated-remote)
</recommended_plugins>

## developer · 2026-11-17T08:28:33Z

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

## developer · 2026-11-17T08:28:33Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-17T08:28:33Z

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
  <current_date>2026-11-17</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/GitHub/labs/py-labs</root><root>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs</path></entry><entry access="write"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/GitHub/labs/py-labs/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/Library/Caches/JetBrains/PyCharm2026.2/aia/agents/views/codex/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-17T08:28:33Z

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

## user · 2026-11-17T08:28:33Z

这里不应该写key吗
[@8.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/assignments/5-261116/8.py)
[@8.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/assignments/5-261116/8.py)
<context ref="file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/assignments/5-261116/8.py">
{"description":"Byte offsets of selected text in filePath.\nUse these offsets to read selected text if it is required.\nstartOffset is inclusive, endOffset is exclusive.","offsetEncoding":"byte","selections":[{"startOffset":640,"endOffset":645}]}
</context>
[@ai-chat-custom-attachment-temp-file-81ff7713-6007-44ce-a1ca-999674a67c54-10616549146006650262.png](file:///var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T/ai-chat-custom-attachment-temp-file-81ff7713-6007-44ce-a1ca-999674a67c54-10616549146006650262.png)

## assistant · 2026-11-17T08:28:37Z

我先查看选中的代码，确认这里的变量代表什么。

## tool · 2026-11-17T08:28:39Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"2715ae","wall_time_seconds":0.000011583,"exit_code":0,"original_token_count":170,"output":"# 词频统计基础\n# 描述：给定一行英文句子（单词之间用空格分隔），统计每个单词出现的次\n# 数，并按插入顺序输出。\n# 输入格式：一行字符串，由若干英文单词组成，单词之间用单个空格分隔。\n# 输出格式：每行输出 \"单词: 次数\"，按首次出现顺序输出。\n# 样例输入：apple banana apple cherry banana apple\n# 样例输出：apple: 3\n# banana: 2\n# cherry: 1\n\nsentence = input().split()\nword_count = {}\nfor word in sentence:\n    if word in word_count:\n        word_count[word] += 1\n    else:\n        word_count[word] = 1\n\nfor word, count in word_count.items():\n    print(f\"{word}: {count}\")\n"}
{"chunk_id":"e5431c","wall_time_seconds":0.000015417,"exit_code":0,"original_token_count":798,"output":"---\nname: using-superpowers\ndescription: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions\n---\n\n<SUBAGENT-STOP>\nIf you were dispatched as a subagent to execute a specific task, ignore this skill.\n</SUBAGENT-STOP>\n\n<EXTREMELY-IMPORTANT>\nIf you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.\n\nIF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.\n\nThis is not negotiable. You cannot rationalize your way out of this.\n</EXTREMELY-IMPORTANT>\n\n## The Rule\n\n**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.\n\n**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.\n\nThen announce \"Using [skill] to [purpose]\" and follow the skill exactly. If it has a checklist, create a todo per item.\n\n## Skill Priority\n\nWhen multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.\n\n- \"Let's build X\" → superpowers:brainstorming first, then implementation skills.\n- \"Fix this bug\" → superpowers:systematic-debugging first, then domain skills.\n\n## Red Flags\n\nThese thoughts mean STOP—you're rationalizing:\n\n| Thought | Reality |\n|---------|---------|\n| \"This is just a simple question\" | Questions are tasks. Check for skills. |\n| \"I need more context first\" | Skill check comes BEFORE clarifying questions. |\n| \"Let me explore the codebase first\" | Skills tell you HOW to explore. Check first. |\n| \"I can check git/files quickly\" | Files lack conversation context. Check for skills. |\n| \"Let me gather information first\" | Skills tell you HOW to gather information. |\n| \"This doesn't need a formal skill\" | If a skill exists, use it. |\n| \"I remember this skill\" | Skills evolve. Read current version. |\n| \"This doesn't count as a task\" | Action = task. Check for skills. |\n| \"The skill is overkill\" | Simple things become complex. Use it. |\n| \"I'll just do this one thing first\" | Check BEFORE doing anything. |\n| \"This feels productive\" | Undisciplined action wastes time. Skills prevent this. |\n| \"I know what that means\" | Knowing the concept ≠ using the skill. Invoke it. |\n\n## Platform Adaptation\n\nIf your harness appears here, read its reference file for special instructions:\n\n- Claude Code: `references/claude-code-tools.md`\n- Codex: `references/codex-tools.md`\n- Pi: `references/pi-tools.md`\n- Antigravity: `references/antigravity-tools.md`\n- Hermes Agent: `references/hermes-tools.md`\n- Muse: `references/muse-tools.md`\n\n## User Instructions\n\nUser instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.\n"}

## tool · 2026-11-17T08:28:52Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"d2e9f0","wall_time_seconds":0.000008625,"exit_code":0,"original_token_count":2,"output":"items"}

## assistant · 2026-11-17T08:29:06Z

这里用 **`items()`** 是对的，因为循环需要同时取出“单词”和“次数”：

```python
for word, count in word_count.items():
```

例如字典为 `{"apple": 3}`，`items()` 会提供 `("apple", 3)`，分别赋给 `word` 和 `count`。

如果只需要键，可以写：

```python
for word in word_count:
```

也可以用 `word_count.keys()`，注意是 **`keys()`**，没有 `key()` 这个字典方法。

未修改文件，也未运行程序；以上根据代码说明。

## user · 2026-11-17T08:30:24Z

改成key吧
[@8.py](file:///Users/oyamahappa/Documents/GitHub/labs/py-labs/assignments/5-261116/8.py)

## assistant · 2026-11-17T08:30:28Z

我会改成用 `key` 遍历字典的键，再通过 `word_count[key]` 读取次数，并验证样例输出。

## tool · 2026-11-17T08:30:45Z


Script completed
Wall time 1.8 seconds
Output:

Warning: truncated output (original token count: 20800)
Total output lines: 5

[{"name":"apply_patch","description":"The `apply_patch` tool can be used to edit files. This is a FREEFORM tool, so do not wrap the p"},{"name":"exec_command","description":"Runs a command in a PTY, returning output or a session ID for ongoing interaction.\n\nexec tool d"},{"name":"image_gen__imagegen","description":"The `image_gen.imagegen` tool enables image generation from descriptions and editing of existin"},{"name":"list_mcp_resource_templates","description":"Lists resource templates provided by MCP servers. Parameterized resource templates allow server"},{"name":"list_mcp_resources","description":"Lists resources provided by MCP servers. Resources allow servers to share data that provides co"},{"name":"mcp__chembl__drug_search","description":"Search for approved drugs and clinical candidates by therapeutic indication.\n\nPURPOSE: Find dru"},{"name":"mcp__chembl__get_admet","description":"Retrieve ADMET-related molecular properties for drug-likeness assessment.\n\nIMPORTANT: ChEMBL pr"},{"name":"mcp__codex_apps__github_add_review_to_pr","description":"Add a review to a GitHub pull request. review is required for REQUEST_CHANGES and COMMENT event"},{"name":"mcp__codex_apps__github_compare_commits","description":"Compare two commits/refs and return per-file stats plus compare metadata. This is a thin wrappe"},{"name":"mcp__codex_apps__github_create_file","description":"Create a new UTF-8 text file through GitHub's contents API. Returns only the resulting commit S"},{"name":"mcp__codex_apps__github_delete_file","description":"Delete a file through GitHub's contents API. Returns only the resulting commit SHA. Docs: https"},{"name":"mcp__codex_apps__github_download_user_content","description":"Download a GitHub private user image attachment URL. Use this only for private-user-images.gith"},{"name":"mcp__codex_apps__github_download_workflow_artifact","description":"Download a GitHub Actions workflow artifact ZIP archive. GitHub serves this endpoint through a "},{"name":"mcp__codex_apps__github_fetch","description":"Fetch approved public GitHub repository resources and repository files. Supports repositories, "},{"name":"mcp__codex_apps__github_fetch_file","description":"Fetch file content by repository path, using the default branch when ref is omitted. This tool "},{"name":"mcp__codex_apps__github_fetch_issue","description":"Fetch a GitHub issue. You must populate exactly one of `repository_full_name`, `repository_id`,"},{"name":"mcp__codex_apps__github_fetch_pr_file_patch","description":"Fetch the patch for one validated changed file in an accessible pull request. Call `list_pr_cha"},{"name":"mcp__codex_apps__github_fetch_pr_patch","description":"Fetch the patch for a GitHub pull request across all changed-file pages. This tool is part of p"},{"name":"mcp__codex_apps__github_get_pr_info","description":"Get metadata (title, description, refs, and status) for a pull request. This action does *not* "},{"name":"mcp__codex_apps__github_get_profile","description":"Retrieve the GitHub profile for the authenticated user. This tool is part of plugin `GitHub`.\n\n"},{"name":"mcp__codex_apps__github_get_repo","description":"Retrieve metadata for a GitHub repository. You must populate exactly one of `repository_full_na"},{"name":"mcp__codex_apps__github_list_pr_changed_filenames","description":"List changed filenames for a PR across all paginated file-list pages. This tool is part of plug"},{"name":"mcp__codex_apps__github_search","description":"Search GitHub files and return matching excerpts when available. Provide a plain string query, "},{"name":"mcp__codex_apps__github_search_installed_repositories_streaming","description":"Search for a repository (not a file) by name or description. To search for a file, use `search`"},{"name":"mcp__codex_apps__github_search_repositories","description":"Search for a repository (not a file) by name or description. To search for a file, use `search`"},{"name":"mcp__codex_apps__github_update_file","description":"Replace a UTF-8 text file through GitHub's contents API. Returns the resulting commit SHA and c"},{"name":"mcp__codex_apps__heygen_clone_voice","description":"Before calling this tool, identify the selected recording(s) and explain that HeyGen will proce"},{"name":"mcp__codex_apps__heygen_complete_asset_batch","description":"Finalizes every uploaded file in a batch once all PUTs return 200. Files are ingested independe"},{"name":"mcp__codex_apps__heygen_convert_speech","description":"Speech to speech: re-voice a recording in an ACTIVE instant voice the workspace owns (from list"},{"name":"mcp__codex_apps__heygen_create_ai_clipping","description":"Submit a source video and return a job id immediately. The job runs asynchronously and produces"},{"name":"mcp__codex_apps__heygen_create_asset_upload_batch","description":"Returns up to 100 presigned upload URLs in one call. PUT each file to its `upload_url` with the"},{"name":"mcp__codex_apps__heygen_create_background_removal","description":"Remove the background from a video: returns a job id at once; poll get_background_removal until"},{"name":"mcp__codex_apps__heygen_create_brand_kit","description":"Creates a brand kit by importing logos, colors and fonts from a public website; by calling it y"},{"name":"mcp__codex_apps__heygen_create_conversation_video","description":"Video of two people talking to each other: interview, podcast, conversation or dialogue between"},{"name":"mcp__codex_apps__heygen_create_digital_twin","description":"Create a reusable digital twin from video footage of a person speaking. Requires their consent:"},{"name":"mcp__codex_apps__heygen_create_filler_word_removal","description":"Submits a video for filler-word removal and returns a job id. The job cuts filler words and lon"},{"name":"mcp__codex_apps__heygen_create_folder","description":"Creates a folder at the root or inside `parent_id`. Pass its `folder_id` to create_video_from_a"},{"name":"mcp__codex_apps__heygen_create_image","description":"Generate images from a text prompt, or edit images: with referenceImages, the prompt says how t"},{"name":"mcp__codex_apps__heygen_create_lipsync","description":"Replaces the audio on an existing video and re-animates the speaker's lip movements to match th"},{"name":"mcp__codex_apps__heygen_create_lipsync_batch","description":"Submits up to 100 lipsync payloads as one batch, and items run independently. Returns 202 with "},{"name":"mcp__codex_apps__heygen_create_look_remix","description":"Remix a person's look: generate one to five portraits that keep the person's identity, with hey"},{"name":"mcp__codex_apps__heygen_create_photo_avatar","description":"Create a photo avatar from one image of a person. Use create_digital_twin for speaking video fo"},{"name":"mcp__codex_apps__heygen_create_professional_voice","description":"Before calling this tool, identify the selected recording(s) and explain that HeyGen will proce"},{"name":"mcp__codex_apps__heygen_create_prompt_avatar","description":"Create an AI avatar from a text description. Use create_photo_avatar for an existing photo or c"},{"name":"mcp__codex_apps__heygen_create_video_from_avatar","description":"Creates a direct talking-avatar video from a specific HeyGen avatar. This is the Avatar Video r"},{"name":"mcp__codex_apps__heygen_create_video_from_cinematic_avatar","description":"Create a Cinematic Avatar video: a 4–15 second clip of one to three avatar looks driven by a na"},{"name":"mcp__codex_apps__heygen_create_video_from_image","description":"Create a talking video by animating one image of a person, with lip movements synced to a scrip"},{"name":"mcp__codex_apps__heygen_create_video_from_studio","description":"Create a single video by composing an ordered list of whole-frame scenes.\n\nThe server owns layo"},{"name":"mcp__codex_apps__heygen_create_video_translation","description":"Before calling this tool, identify the source video(s) and target language(s). Explain that Hey"},{"name":"mcp__codex_apps__heygen_delete_lipsync","description":"Permanently deletes a lipsync job and its associated files. This action cannot be undone. This "},{"name":"mcp__codex_apps__heygen_delete_video","description":"Permanently deletes a video and its associated files. This action cannot be undone. This tool i"},{"name":"mcp__codex_apps__heygen_delete_video_translation","description":"Permanently deletes a video translation and its associated files. This action cannot be undone."},{"name":"mcp__codex_apps__heygen_design_voice","description":"Design a new HeyGen voice from a description of its age, tone, accent and speaking style, in on"},{"name":"mcp__codex_apps__heygen_get_asset","description":"Returns metadata for an asset in the caller's workspace — including owner, upload timestamp, fi"},{"name":"mcp__codex_apps__heygen_get_current_user","description":"Returns the authenticated user's profile, remaining credits or balance, and billing details. Th"},{"name":"mcp__codex_apps__heygen_image_to_video","description":"Animate a first-frame image with a prompt. Optionally supply endImage to guide the ending. Outp"},{"name":"mcp__codex_apps__heygen_import_asset_from_chat","description":"Import a file the user already attached to ChatGPT into their HeyGen workspace. Prefer this too"},{"name":"mcp__codex_apps__heygen_open_asset_library","description":"For a file already attached in chat that the user wants to use in HeyGen, if import_asset_from_"},{"name":"mcp__codex_apps__heygen_reference_to_video","description":"Generate a clip guided by reference images, videos or audio. Supply at least one reference in r"},{"name":"mcp__codex_apps__heygen_show_video","description":"Display a validated or newly created HeyGen video in the inline, self-updating player.\n\nFor \"sh"},{"name":"mcp__codex_apps__heygen_submit_feedback","description":"Submit concise product feedback to HeyGen after the user gives\nfeedback or you observe a meanin"},{"name":"mcp__codex_apps__heygen_text_to_video","description":"Generate a HeyGen Video 1 clip from a text prompt. Use it for visual productions of 30 seconds "},{"name":"mcp__codex_apps__heygen_track_skill_activation","description":"Record that you activated a HeyGen plugin skill, for product\nanalytics. Call this once per skil"},{"name":"mcp__codex_apps__heygen_track_skill_completion","description":"Record that a HeyGen plugin skill you tracked with track_skill_activation\nhas finished, for pro"},{"name":"mcp__codex_apps__pets_create_pet","description":"Consume a completed prepare_pet_upload session by its upload_session_id, validate the sprite sh"},{"name":"mcp__codex_apps__pets_prepare_pet_upload","description":"Prepare a user-scoped ChatGPT pet sprite-sheet upload. First call validate_pet_spritesheet and "},{"name":"mcp__codex_apps__pets_update_pet","description":"Update the name, description, sprite sheet, or any combination for one owned custom ChatGPT pet"},{"name":"mcp__codex_apps__pets_validate_pet_spritesheet","description":"Validate a ChatGPT pet PNG or WebP before creating an upload session. Pass its absolute local p"},{"name":"mcp__codex_apps__plugin_creator_create_plugin","description":"Create one PRIVATE plugin from a generated ZIP or gzip-compressed tar archive. Uses the authent"},{"name":"mcp__codex_apps__plugin_creator_get_owned_plugin_archive","description":"Get a short-lived download URL for the complete archive of an eligible owned personal plugin or"},{"name":"mcp__codex_apps__plugin_creator_get_plugin_files","description":"Get metadata and list files from an editable plugin's current release by its exact backend ID. "},{"name":"mcp__codex_apps__plugin_creator_get_plugin_metadata","description":"Get metadata for an editable plugin by its exact backend ID, without downloading its archive. H"},{"name":"mcp__codex_apps__plugin_creator_get_plugin_sharing","description":"Read the complete plugin sharing audience and discoverability before or after sharing.\n\nUse cre"},{"name":"mcp__codex_apps__plugin_creator_list_owned_personal_plugins","description":"List eligible private personal plugins with USER scope created by the current user. Requires a "},{"name":"mcp__codex_apps__plugin_creator_list_plugin_releases","description":"List attached releases of an eligible owned personal plugin or workspace plugin using the same "},{"name":"mcp__codex_apps__plugin_creator_share_plugin","description":"Share a plugin, including a Dot-created MCP plugin, with explicitly requested users in the acti"},{"name":"mcp__codex_apps__plugin_creator_update_plugin","description":"Update an owned personal plugin or an eligible workspace plugin from a host-uploaded ZIP or tar"},{"name":"mcp__codex_apps__plugin_management_search_plugins","description":"Search available plugins when the user explicitly requests a plugin or provider, or when their "},{"name":"mcp__codex_apps__sites_add_custom_domain","description":"Add a custom domain to a published site. The response includes a CNAME target for subdomains, A"},{"name":"mcp__codex_apps__sites_change_site_slug","description":"Change a site's public URL label. The change runs asynchronously. When the result is pending, u"},{"name":"mcp__codex_apps__sites_create_schedule","description":"Create and link a cloud task for a published Site when the user has requested scheduling. Befor"},{"name":"mcp__codex_apps__sites_create_site","description":"Create a site only when .openai/hosting.json has no project_id. If it has one, reuse that site."},{"name":"mcp__codex_apps__sites_create_source_repository_write_credential","description":"Create a short-lived source repository write credential when the credential returned by create_"},{"name":"mcp__codex_apps__sites_deploy_private_site_version","description":"Deploy a saved site version for a site already known to have owner-only Site permissions in the"},{"name":"mcp__codex_apps__sites_deploy_site_version","description":"Deploy a saved site version to production when the site is shared, public, cannot be verified a"},{"name":"mcp__codex_apps__sites_generate_siwc_bypass_token","description":"Generate a bearer token for identity-less API requests that bypasses a site's Sign in with Chat"},{"name":"mcp__codex_apps__sites_get_deployment_status","description":"Get the current status of a production deployment. Only poll when a deployment ID is available;"},{"name":"mcp__codex_apps__sites_get_environment_variables","description":"Get the production runtime environment variables for a site. These values are separate from loc"},{"name":"mcp__codex_apps__sites_get_site","description":"Get a site and its current access configuration, including external visitors. For a Library Sit"},{"name":"mcp__codex_apps__sites_get_site_version","description":"Get a saved site version and its source provenance. Retain version_id for follow-up calls, but "},{"name":"mcp__codex_apps__sites_get_site_worker_logs","description":"Read recent production Cloudflare Worker logs for a Site when diagnosing why a deployed website"},{"name":"mcp__codex_apps__sites_list_custom_domains","description":"List custom domains attached to a site. This tool is part of plugin `Sites`.\n\nUse Sites to buil"},{"name":"mcp__codex_apps__sites_list_site_versions","description":"List saved site versions in newest-first order for history, deployment, or rollback selection. "},{"name":"mcp__codex_apps__sites_list_sites","description":"List Sites you own in the selected account, including personal accounts. Defaults to 20 Sites; "},{"name":"mcp__codex_apps__sites_read_database_overview","description":"Inspect the user tables in a deployed site's live Cloudflare D1 database before reading rows. R"},{"name":"mcp__codex_apps__sites_read_database_table_rows","description":"Read one bounded page of rows from a user table in a deployed site's live Cloudflare D1 databas"},{"name":"mcp__codex_apps__sites_refresh_custom_domain_status","description":"Refresh custom domain validation status for a site. This tool is part of plugin `Sites`.\n\nUse S"},{"name":"mcp__codex_apps__sites_remove_custom_domain","description":"Remove a custom domain from a site. This tool is part of plugin `Sites`.\n\nUse Sites to build or"},{"name":"mcp__codex_apps__sites_save_site_version","description":"Save a version of the site's pushed source without deploying it. Full SHA of the pushed source "},{"name":"mcp__codex_apps__sites_save_version_and_deploy_private","description":"For a site already known to have owner-only Site permissions in the selected account, use this "},{"name":"mcp__codex_apps__sites_update_environment_variables","description":"Update production runtime environment variables for a site. Only listed keys change; all others"},{"name":"mcp__codex_apps__sites_update_site_access","description":"Update who can visit a site only when the user asks to change access. Set access_mode only when"},{"name":"mcp__codex_apps__sites_update_site_metadata","description":"Update a site's display title. This does not change the site's public URL. This tool is part of"},{"name":"mcp__codex_apps__termalin_alerts_list","description":"What Termalin's monitoring says is wrong with the user's servers right now (disk filling up, me"},{"name":"mcp__codex_apps__termalin_backup_create","description":"Make an encrypted backup of one of the user's servers now, through Termalin's backup job for th"},{"name":"mcp__codex_apps__termalin_backup_job_create","description":"Propose a new encrypted backup job for one of the user's servers: folders and/or databases, how"},{"name":"mcp__codex_apps__termalin_backup_list","description":"The backup jobs and recent archives of one of the user's servers: what each job covers (folders"},{"name":"mcp__codex_apps__termalin_data_query","description":"Run a database query on one of your servers — passwordless. It executes the engine's own client"},{"name":"mcp__codex_apps__termalin_data_schema","description":"Describe one table of a database on one of your servers: its columns with type, whether they ca"},{"name":"mcp__codex_apps__termalin_data_tables","description":"List the tables / collections / keys of a database on one of your servers — passwordless, over "},{"name":"mcp__codex_apps__termalin_desktop_click","description":"Click on a desktop session at a point of the last screenshot. The user started this desktop ses"},{"name":"mcp__codex_apps__termalin_desktop_key","description":"Press a key or a key combination on a desktop session: \"enter\", \"esc\", \"tab\", \"ctrl+s\", \"alt+ta"},{"name":"mcp__codex_apps__termalin_desktop_list","description":"List the remote desktop sessions (Windows over RDP, Linux or Mac over VNC) open for AI in Terma"},{"name":"mcp__codex_apps__termalin_desktop_move","description":"Move the mouse pointer on a desktop session (e.g. to show a tooltip). The user started this des"},{"name":"mcp__codex_apps__termalin_desktop_open","description":"Open a remote desktop the user saved for AI in Termalin (see `desktops` in desktop_list). Signs"},{"name":"mcp__codex_apps__termalin_desktop_screenshot","description":"Take a screenshot of a desktop session (JPEG). Returns the picture and its size; the coordinate"},{"name":"mcp__codex_apps__termalin_desktop_scroll","description":"Scroll with the mouse wheel at a point of a desktop session: dy > 0 scrolls down, dy < 0 up, in"},{"name":"mcp__codex_apps__termalin_desktop_type","description":"Type text on a desktop session, where the keyboard focus is (click a field first). Up to 500 ch"},{"name":"mcp__codex_apps__termalin_desktop_wait","description":"Wait until the screen of a desktop session changes since your last screenshot (or until the tim"},{"name":"mcp__codex_apps__termalin_generate_password","description":"Generate a strong random password — handy when creating a user or setting a password on a serve"},{"name":"mcp__codex_apps__termalin_hosts_list","description":"List the servers reachable through Termalin (your tunnel agents). Returns id, name, whether the"},{"name":"mcp__cod…10800 tokens truncated… (base plus every split, as `pm path` reports) fro"},{"name":"mcp__rea__push_adb_file","description":"Push one local file to an absolute device path. If the destination is an existing directory, ad"},{"name":"mcp__rea__read_adb_logcat","description":"Read a bounded dump of the device log (`logcat -d -t`) for one buffer, optionally restricted to"},{"name":"mcp__rea__read_adb_setting","description":"Read one settings value (`settings get`) from the system, secure, or global namespace. Absent k"},{"name":"mcp__rea__read_bytes","description":"Read analyzed bytes from one provider-normalized virtual address. The hexadecimal payload repor"},{"name":"mcp__rea__read_function_instructions","description":"Return every raw instruction for one analyzed procedure. Instruction text and body extent are p"},{"name":"mcp__rea__reconcile_javascript_runtime","description":"Reconcile verified static JavaScript application graphs with existing passive web/Electron CDP,"},{"name":"mcp__rea__record_unknown","description":"Create one deterministic residual unknown and immutable mutation evidence. Validates all eviden"},{"name":"mcp__rea__recover_javascript_sources","description":"Recover readable modules from local UTF-8 JavaScript scripts/bundles into an absent directory, "},{"name":"mcp__rea__resolve_adb_packages","description":"Find installed packages by case-insensitive substring of the package name (e.g. `whatsapp` → `c"},{"name":"mcp__rea__resolve_containing_procedure","description":"Resolve an arbitrary address, including an interior instruction or exact external entry, to its"},{"name":"mcp__rea__resolve_native_call_targets","description":"Resolve one explicit static call site using typed provider call references. Preserves ambiguous"},{"name":"mcp__rea__resume_frida_session","description":"Resume the process created by a paused Frida spawn session. Attached processes are already runn"},{"name":"mcp__rea__rizin_debug_command","description":"Execute one unrestricted command in a persistent Rizin debugger session. Returns raw output inl"},{"name":"mcp__rea__rizin_debug_session_status","description":"Return observed lifecycle state and bounded recent NUL-framed output and process diagnostics fo"},{"name":"mcp__rea__search_android_classes","description":"Search complete top-level decompiler class-name rows in an explicit local APK by case-sensitive"},{"name":"mcp__rea__search_bytes","description":"Find masked byte signatures in initialized analyzed memory. Hex byte pairs and ?? wildcards are"},{"name":"mcp__rea__search_procedures","description":"Search every analyzed procedure name using literal matching by default or regex when requested."},{"name":"mcp__rea__search_strings","description":"Search every provider-reported string object or candidate using literal matching by default or "},{"name":"mcp__rea__set_address_name","description":"Assign an analyst name to one mapped hexadecimal address and report whether the native edit suc"},{"name":"mcp__rea__set_addresses_names","description":"Assign analyst names to multiple mapped addresses in one call and return per-address edit/readb"},{"name":"mcp__rea__set_bookmark","description":"Create or update a bookmark at a mapped hexadecimal address and report readback success. Omit n"},{"name":"mcp__rea__set_comment","description":"Write a regular analysis comment at a hexadecimal address and return whether readback matched. "},{"name":"mcp__rea__set_inline_comment","description":"Write an inline instruction comment at a hexadecimal address and return whether readback matche"},{"name":"mcp__rea__start_adb_activity","description":"Start an intent with `am start -W`: one action, optional data URI, optional explicit component,"},{"name":"mcp__rea__start_adb_app","description":"Start one installed app's resolved launcher activity with `am start -W -n`. A device-mutating t"},{"name":"mcp__rea__start_frida_session","description":"Attach Frida to one selected process or spawn one selected target. Spawned targets remain pause"},{"name":"mcp__rea__start_gdb_session","description":"Start a BYO GDB process in MI3 mode when available, suppress startup files, and disable auto-lo"},{"name":"mcp__rea__start_rizin_debug_session","description":"Start a persistent Rizin debugger session using `-N` to suppress user settings and scripts whil"},{"name":"mcp__rea__stop_adb_app","description":"Force-stop every process of one package (`am force-stop`), ending a dynamic-analysis run. A dev"},{"name":"mcp__rea__trace_android_references","description":"Trace incoming static using nodes to an exact Android class or selected method overload. The to"},{"name":"mcp__rea__trace_application_feature","description":"Trace a typed literal seed through every reachable part of an authenticated JavaScript Applicat"},{"name":"mcp__rea__trace_call_path","description":"Resolve start and optional goal symbols or addresses to canonical procedure entries, then trace"},{"name":"mcp__rea__trace_dylib_resolution","description":"Trace how dyld would resolve each Mach-O dylib load for the active Mach-O, or for every executa"},{"name":"mcp__rea__trace_feature","description":"Trace the complete literal query, preserving spaces, through every matching string and procedur"},{"name":"mcp__rea__trace_javascript_semantics","description":"Trace static JavaScript data-flow, direct call/return, and closure relations from inline applic"},{"name":"mcp__rea__trace_native_ui_action","description":"Trace one unique compiled UI action, object ID, native symbol or exact function address through"},{"name":"mcp__rea__trace_native_values","description":"Trace a bounded static dependency graph from one explicit native procedure. Includes high-p-cod"},{"name":"mcp__rea__trace_web_module_imports","description":"Trace one exported website script's outgoing native ES imports/re-exports, using exact URL and "},{"name":"mcp__rea__trace_web_source_location","description":"Trace one generated position in an exported website script through an explicitly paired local s"},{"name":"mcp__rea__uninstall_adb_package","description":"Request package removal for user 0 (`adb shell pm uninstall --user 0`) without data retention. "},{"name":"mcp__rea__unload_frida_script","description":"Unload one caller-selected Frida script from a live session. This removes that script's instrum"},{"name":"mcp__rea__unset_bookmark","description":"Remove the bookmark at a mapped hexadecimal address and return whether it is absent. Hopper als"},{"name":"mcp__rea__update_analysis_settings","description":"When REA names an adjustable limit, atomically set or reset its runtime default, then retry onc"},{"name":"mcp__rea__update_unknown","description":"Append one immutable full-state revision and mutation evidence. Requires exact expected_revisio"},{"name":"mcp__rea__verify_managed_native_boundaries","description":"Verify managed P/Invoke/native-boundary declarations against authenticated native export or fun"},{"name":"mcp__rea__verify_reconstruction","description":"Verify a finite typed behavioral and structural specification against a canonical Evidence bund"},{"name":"mcp__rea__verify_unknown_resolution","description":"Revalidate the current residual-unknown head against live bundled evidence, exact authority/con"},{"name":"mcp__rea__xrefs","description":"Return analyzed references to a code or data address. Hopper may default to its current cursor;"},{"name":"view_image","description":"View a local image file from the filesystem when visual inspection is needed. Use this for imag"}]
{"chunk_id":"532eb8","wall_time_seconds":0.000010375,"exit_code":0,"original_token_count":12,"output":"/Users/oyamahappa/Documents/GitHub/labs/py-labs\n"}
{"chunk_id":"948e09","wall_time_seconds":0.00000725,"exit_code":0,"original_token_count":2864,"output":"---\nname: python-tools\ndescription: PyCharm environment tools. MUST be consulted before running ANY Python toolchain command (python, python3, pip, pip3, uv, conda, pytest, ruff, mypy, python -m <module>, etc.) — call get_python_environment first to get the executable and package manager that match PyCharm's configured SDK for the file's module. Also covers configuring an interpreter when none is set up.\nallowed-tools: execute_tool\n---\n\n# PyCharm Environment Tools\n\n> **Mandatory pre-flight:** before running ANY Python command — `python`, `python3`, `pip`, `pip3`, `uv`, `conda`, `pytest`, `ruff`, `mypy`, `python -m <module>`, or anything else that resolves a Python interpreter — call `get_python_environment` on a file inside the target module. Use the returned `executablePath` instead of a bare `python` / `python3`, and the returned `packageManager` to choose the correct install command. Skipping this step silently picks the wrong interpreter (system Python instead of the project's venv, an older minor version, missing packages) and corrupts the project's environment.\n\n> **If `get_python_environment` returns a non-null `noInterpreterConfigured` field, get a proper interpreter before running the Python command.** Branch on the field's content:\n> - Ends with `call configure_python_interpreter with the same --filePath.` → call `configure_python_interpreter`, then re-call `get_python_environment`. Run the Python command using the env info returned by the second call.\n> - Says `PyCharm expects this project to use <tool>, but <tool> is not installed.` (e.g. `uv`, `poetry`, `hatch`) → do NOT call `configure_python_interpreter`. Ask the user to install the named tool first, then re-call `get_python_environment`.\n> - Plain `No Python interpreter configured for: <path>.` (no extra suffix) → PyCharm has no automatic option, but the project also doesn't dictate a specific tool. Set up the env yourself with a sensible default (e.g. `python3 -m venv .venv` in the project root), then re-call `get_python_environment`. The new venv should be detected and the next response will suggest `configure_python_interpreter`; if it still returns plain \"no interpreter\" for some reason, use `.venv/bin/python` directly. Tell the user what you set up.\n>\n> For commands that aren't tied to a specific file (e.g. `pip install`, `pytest` at the project root, or a run configuration that doesn't expose a target file), pass any `.py` file inside the target module as `--filePath` — the interpreter is per-module, not per-file.\n\nTwo tools, used together:\n\n1. **`get_python_environment`** — always call this first. Read-only: it reports the Python interpreter PyCharm has configured for a file (version, environment type, executable path, package manager) and never modifies project state.\n2. **`configure_python_interpreter`** — call this *only* when `get_python_environment` returns a `noInterpreterConfigured` field whose value ends with `call configure_python_interpreter with the same --filePath.` That means PyCharm can do the configuration without installing anything new — it will attach an existing virtual environment on disk, inherit the parent module's interpreter, or create a fresh env using a tool that's already installed (uv / poetry / hatch / venv). Do not call it in any other situation.\n\nPrefer these tools over guessing interpreter paths or package managers — the results match what PyCharm itself uses.\n\n## `get_python_environment`\n\nReturns the Python environment configured for the given file.\n\n### Syntax\n\n```\nexecute_tool(command=\"get_python_environment --filePath <value>\")\n```\n\n### Parameters\n\n| Parameter | Type | Required | Description |\n|-----------|------|----------|-------------|\n| `--filePath` | `string` | Yes | Absolute or project-relative path to any Python file (e.g. `/Users/dev/myproject/src/main.py` or `src/main.py`). Used to identify which interpreter and environment PyCharm has configured for that file. |\n\n**String parameters:** Quote values containing spaces: `--filePath '/Users/dev/my project/main.py'`\n\n### Output fields\n\nResponse is a JSON object with these fields:\n\n| Field | Description |\n|-------|-------------|\n| `pythonVersion` | Interpreter version string, e.g. `Python 3.11.4` |\n| `environmentType` | `venv`, `conda`, `system`, or `unknown` |\n| `executablePath` | Absolute path to the Python binary to invoke |\n| `environmentPath` | Root of the virtual environment (venv prefix or conda prefix); `null` for system Python |\n| `packageManager` | `pip`, `uv`, `poetry`, `hatch`, `conda`, or `unknown` — use this to pick the right install command |\n| `noInterpreterConfigured` | When non-null, no interpreter is set up. Contains the next-step hint (see Pitfalls). Other fields will be `null`. |\n\nExample response:\n\n```json\n{\n  \"pythonVersion\": \"Python 3.11.4\",\n  \"environmentType\": \"venv\",\n  \"executablePath\": \"/Users/dev/myproject/.venv/bin/python\",\n  \"environmentPath\": \"/Users/dev/myproject/.venv\",\n  \"packageManager\": \"uv\"\n}\n```\n\n### Examples\n\n#### 1. Absolute path\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath /Users/dev/myproject/src/main.py\"}}\n```\n\n#### 2. Project-relative path\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath src/main.py\"}}\n```\n\n#### 3. Path with spaces\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"get_python_environment --filePath '/Users/dev/my project/src/main.py'\"}}\n```\n\n### Pitfalls\n\n- Quote the path if it contains spaces.\n- The file must exist on disk; passing a non-existent path returns an error.\n- If `noInterpreterConfigured` is non-null and ends with `call configure_python_interpreter with the same --filePath.` (e.g. \"PyCharm can attach the existing virtual environment…\", \"PyCharm can create a new uv environment…\", \"PyCharm can inherit the interpreter from parent module 'X'…\"), follow that — PyCharm has tooling ready and the configure tool will set it up without installing anything.\n- If `noInterpreterConfigured` says `PyCharm expects this project to use <tool>, but <tool> is not installed.`, the project's `pyproject.toml` / lockfile points at a tool the system doesn't have. Do not call `configure_python_interpreter`. Ask the user before installing the named tool via the terminal, then re-call `get_python_environment`.\n- If `noInterpreterConfigured` is the plain `No Python interpreter configured for: <path>.` with no extra content, do not call `configure_python_interpreter`. The project doesn't pin a specific tool, so set up a default venv yourself (e.g. `python3 -m venv .venv`) and re-call `get_python_environment` — the next call should detect it and suggest `configure_python_interpreter`. Never just run the user's command with bare `python` / `python3`.\n\n## `configure_python_interpreter`\n\nAsks PyCharm to attach a Python interpreter for the module the given file belongs to. PyCharm picks the right action: attach an existing virtual environment on disk, inherit the interpreter from a parent module, or create a fresh env using already-installed tooling (uv venv, poetry env, hatch env, or plain `venv`). Only call this when `get_python_environment` explicitly suggested it (the `noInterpreterConfigured` field ended with `call configure_python_interpreter with the same --filePath.`). Do not call it as a generic interpreter switcher and do not call it when `noInterpreterConfigured` is the plain \"no interpreter\" message without a configuration suggestion.\n\n### Syntax\n\n```\nexecute_tool(command=\"configure_python_interpreter --filePath <value>\")\n```\n\n### Parameters\n\n| Parameter | Type | Required | Description |\n|-----------|------|----------|-------------|\n| `--filePath` | `string` | Yes | Absolute or project-relative path to a Python file inside the module whose interpreter should be configured. |\n\n### Output\n\nOn success, returns the same JSON shape as `get_python_environment`, describing the interpreter PyCharm just configured.\n\n### Examples\n\n#### Configure after `get_python_environment` reported that PyCharm can set one up\n\n```json\n{\"tool\":\"execute_tool\",\"arguments\":{\"command\":\"configure_python_interpreter --filePath src/main.py\"}}\n```\n\n### Pitfalls\n\n- Local interpreters only. Remote / WSL / Docker interpreters are not supported by this tool.\n- Only call this tool when `get_python_environment` told you to. Calling it after the plain `No Python interpreter configured for: <path>` (with no `call configure_python_interpreter` suggestion) will fail — PyCharm has no automatic option there and there is nothing this tool can do.\n\n## Rules\n\n1. **You MUST call `get_python_environment` before every Python toolchain invocation** — `python`, `python3`, `pip`, `pip3`, `uv`, `conda`, `pytest`, `ruff`, `mypy`, `python -m <module>`, and any other command that resolves a Python interpreter. The check is cheap (a single MCP call) and there is no exemption for \"obvious\" cases — running a fresh `python script.py` in a project with a configured venv is exactly the case where the wrong interpreter ruins things silently. Re-check after every `configure_python_interpreter` call, after the user reconfigures the SDK in PyCharm, and whenever you switch to a file from a different module.\n2. **If `get_python_environment` returns a non-null `noInterpreterConfigured` field, get a proper interpreter before running the Python command — never fall back to bare `python` / `python3`.** Branch on the field's content:\n   - Suffix `call configure_python_interpreter with the same --filePath.` → call `configure_python_interpreter`, re-call `get_python_environment`, then proceed.\n   - `PyCharm expects this project to use <tool>, but <tool> is not installed.` → do NOT call `configure_python_interpreter`. Ask the user before installing the named tool via the terminal, then re-call `get_python_environment`.\n   - Plain `No Python interpreter configured for: <path>.` → the project pins no specific tool. Set up a default venv yourself (`python3 -m venv .venv` in the project root) and re-call `get_python_environment`; the new venv will normally surface a `configure_python_interpreter` suggestion on the next call. Tell the user what you set up.\n3. **If any other tool reports a missing Python interpreter, route through this skill before asking the user.** When `get_run_configurations`, `execute_run_configuration`, `build_project`, the terminal, or any other PyCharm tool returns a \"no interpreter configured\" message, call `get_python_environment` on a file in the target module — do NOT instruct the user to set the interpreter via Settings → Project → Python Interpreter without first checking what `get_python_environment` reports.\n4. Use the returned `executablePath` verbatim — never substitute `python` / `python3` / `which python` output.\n5. Use the returned `packageManager` to pick the install command — `pip install <pkg>` for `pip`, `uv add <pkg>` for `uv`, `poetry add <pkg>` for `poetry`, `hatch run pip install <pkg>` for `hatch`, `conda install <pkg>` for `conda`. If `packageManager` is `unknown`, ask the user how to install packages for this interpreter before running anything.\n6. Call `configure_python_interpreter` only when `get_python_environment` explicitly suggested it (the `noInterpreterConfigured` field ended with `call configure_python_interpreter with the same --filePath.`). `get_python_environment` itself never modifies project state.\n"}
{"chunk_id":"0acce4","wall_time_seconds":0.000015083,"exit_code":0,"original_token_count":16,"output":"## main...origin/main\n M assignments/5-261116/8.py\n?? .DS_Store\n"}
{"chunk_id":"dae523","wall_time_seconds":1.339702041,"exit_code":0,"original_token_count":58,"output":"docs/CHANGELOG.md\ncharacter2/section5/subsection5/20261012103558.py\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\nassignments/4-261109/8.py\nassignments/5-261116/8.py\nassignments/3-261102/8.py\n"}

## assistant · 2026-11-17T08:30:54Z

我会使用 `python-tools` 技能确认项目解释器，再运行样例验证。

## tool · 2026-11-17T08:30:56Z


Script completed
Wall time 0.1 seconds
Output:

[{"name":"mcp__pycharm__execute_tool","description":"Universal tool executor that can invoke specific IDE MCP tool dynamically.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__pycharm__execute_tool(args: {\n  // Command-line string with tool name and arguments\n  command: string;\n}): Promise<CallToolResult>; };\n```"}]
{"status":"fulfilled","value":{"chunk_id":"507f11","wall_time_seconds":0.00003475,"exit_code":0,"original_token_count":1364,"output":"# 词频统计基础\n# 描述：给定一行英文句子（单词之间用空格分隔），统计每个单词出现的次\n# 数，并按插入顺序输出。\n# 输入格式：一行字符串，由若干英文单词组成，单词之间用单个空格分隔。\n# 输出格式：每行输出 \"单词: 次数\"，按首次出现顺序输出。\n# 样例输入：apple banana apple cherry banana apple\n# 样例输出：apple: 3\n# banana: 2\n# cherry: 1\n\nsentence = input().split()\nword_count = {}\nfor word in sentence:\n    if word in word_count:\n        word_count[word] += 1\n    else:\n        word_count[word] = 1\n\nfor word, count in word_count.items():\n    print(f\"{word}: {count}\")\n# 协作环境\n\n- 项目：Python 基础练习，当前任务为修复 `assignments/4-261109/8.py` 的正负数统计。\n- 工具：文件编辑工具、Git、PyCharm Python 环境查询、标准库 unittest 和 subprocess。\n- Python：项目 `.venv/bin/python`，版本 3.9.6，无需新增依赖。\n- 当前采用 Ponytail 最小修改原则，并使用 python-tools 查询解释器；无需新增依赖。\n# 当前任务\n\n- 修复 `assignments/4-261109/8.py`：调用 `split()`，使用 `map(int, ...)` 转换整数，移除多余的外层无限循环。\n- 保留当前计数逻辑，按题目从一行读取整数，在首个 0 处终止统计。\n- 先用标准库回归测试复现附件中的 TypeError，再验证样例、零、单一符号、多余空白和结束标志。\n- 未发现调用方、夹具、配置和导出；范围为目标脚本、新增测试、协作记录及日志，不新增依赖。目标脚本已有用户修改，本次修复基于当前内容，提交仅涉及本任务最终状态。\n# 完成标准\n\n- 使用 PyCharm 确认的 Python 3.9.6，通过 subprocess 实际运行 `8.py`，不使用 mock。\n- 修改前确认样例因 split 未调用而抛出 TypeError；修改后 7 组输入逐字符验证输出、退出码和标准错误。\n- 覆盖样例、仅 0、全正数、全负数、额外空白、首个 0 后停止、较大整数。\n- 运行 unittest discover，包含已有乘法表测试；项目无静态检查配置。\n- 执行 `git diff --check`；仅暂存任务文件，保留 `3.py` 和 `.DS_Store` 的已有变化。\n- 未访问判题系统，不能确认远端判题结果。\n# 当前进度\n\n## 8.py 正负数统计\n\n- [x] 阅读代码、附件和已有用户修改，定位 split 未调用、字符串未转整数、外层循环无法结束的问题。\n- [x] 通过 PyCharm 确认项目解释器为 Python 3.9.6。\n- [x] 用样例回归测试复现附件中的 TypeError。\n- [x] 使用 `map(int,input().split())` 和单层循环完成统计，7 组输入检查通过；包括乘法表在内的 3 项测试全部通过，`git diff --check` 通过。\n- [x] 更新开发日志，提交 `63d8ce6 fix: count signed integers from one input line`，已普通推送至 `origin/main`。\n\n## 10.py 乘法表输出\n\n- [x] 阅读题目附件、脚本和引用，确认每行末尾多输出空格。\n- [x] 通过 PyCharm 确认项目解释器为 Python 3.9.6。\n- [x] 运行回归测试，确认修改前因行尾空格失败。\n- [x] 仅修改输出结束符；标准库 unittest 的 2 项测试通过，覆盖样例和全部合法输入 1～9；`git diff --check` 通过。\n- [x] 更新日志，提交 `e724433 fix: remove trailing spaces from multiplication table`，已普通推送至 `origin/main`。\n\n## f-string 详细笔记\n\n- [x] 阅读 `4.py`、现有记录和 Git 状态，核对 Python 官方文档。\n- [x] 通过 PyCharm 确认项目解释器为 Python 3.9.6。\n- [x] 编写 18 节详细笔记，包含输出、常见错误、速查表和 6 道练习及答案。\n- [x] Python 3.9.6 doctest：126 条示例全部通过；原练习 4 组输入输出断言通过；`git diff --check` 通过。\n- [x] 更新开发日志，提交 `51bc3e5 docs: add detailed f-string study notes`，已普通推送至 `origin/main`。\n\n## 7.py 同一行输入\n\n- [x] 检查目标脚本和引用，未发现调用方或关联测试。\n- [x] 修改前输入 `3 4 5 ,`，确认抛出 `ValueError`。\n- [x] 使用 `split` 和 `map` 读取同一行数据。\n- [x] 使用项目解释器运行 4 组输入，输出断言通过，退出码为 0，标准错误为空；`git diff --check` 通过。\n- [x] 提交 `83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n\n## 历史任务：L1\n\n- [x] 阅读题目图片和空白 `character1/L1.py`。\n- [x] 确认项目 Python 版本为 3.9.6，本地日期为 2026-10-19。\n- [x] 完成五行输出和逐条注释；个人资料暂显示“待填写”。\n- [ ] 收到用户的姓名、班级、学号后替换三项文字。\n- [x] 实际运行脚本，五行输出、日期、解释器版本及逐条注释断言通过，标准错误为空。\n- [x] 更新开发记录，创建提交 `19fd4fc feat: complete L1 information card exercise`。\n- [ ] 推送到 `https://github.com/OyamaMeek/py-labs.git` 的 `main`：自动审批以缺少具体目的地授权为由拒绝，等待用户明确授权。\n\n已有其他文件的暂存和未暂存修改，均不纳入本任务提交。\n# 注意事项\n\n- `../assignments` 的三个整数和分隔符必须从同一行读取，按要求使用 `map` 和 `split`。\n\n- 个人资料必须由用户提供，不从用户名推断姓名、班级或学号。\n- 本练习要求手工记录 Python 版本，不添加自动获取环境的 `import`。\n"}}
{"status":"fulfilled","value":{"chunk_id":"bd6598","wall_time_seconds":0.000012667,"exit_code":0,"original_token_count":204,"output":"diff --git a/assignments/5-261116/8.py b/assignments/5-261116/8.py\nindex 32faea2..82c05ec 100644\n--- a/assignments/5-261116/8.py\n+++ b/assignments/5-261116/8.py\n@@ -3,8 +3,18 @@\n # 数，并按插入顺序输出。\n # 输入格式：一行字符串，由若干英文单词组成，单词之间用单个空格分隔。\n # 输出格式：每行输出 \"单词: 次数\"，按首次出现顺序输出。\n-# 样例输入：apple banana apple cherry ba\n-# nana apple\n+# 样例输入：apple banana apple cherry banana apple\n # 样例输出：apple: 3\n # banana: 2\n # cherry: 1\n+\n+sentence = input().split()\n+word_count = {}\n+for word in sentence:\n+    if word in word_count:\n+        word_count[word] += 1\n+    else:\n+        word_count[word] = 1\n+\n+for word, count in word_count.items():\n+    print(f\"{word}: {count}\")\n"}}
{"status":"fulfilled","value":{"chunk_id":"fff301","wall_time_seconds":0.000007458,"exit_code":0,"original_token_count":844,"output":"\n- **涉及文件**：\n  - `../assignments`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`83c276d fix: read exercise 7 input from one line`，已推送至 `origin/main`。\n\n---\n\n## [2026-11-03 17:13] f-string 详细学习笔记\n\n- **需求/问题描述**：\n  > 结合 `../assignments` 整理一份 f-string 的详细笔记。\n\n- **实际实现的功能与改动**：\n  - 新增 18 节中文笔记，逐项解释原题，覆盖常用格式、表达式、转义、调试、动态格式、日期、常见错误、速查表和 6 道练习答案。\n  - 说明两个 `f` 的区别、最小宽度、浮点舍入和中文显示宽度，附 Python 官方文档链接。\n  - Python 3.9.6 doctest：126 条示例全部通过；原练习普通输入、中文、超宽内容和负数共 4 组输入输出断言通过，退出码为 0、标准错误为空。\n  - `git diff --check` 通过；未修改练习脚本，未新增依赖，未执行视觉检查。\n\n- **涉及文件**：\n  - `docs/f-string笔记.md`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`51bc3e5 docs: add detailed f-string study notes`，已推送至 `origin/main`。\n\n---\n\n## [2026-11-09 13:40] 10.py 乘法表行尾空格\n\n- **需求/问题描述**：\n  > 修复 `assignments/4-261109/10.py`，附件显示判题结果为 Wrong Answer。\n\n- **实际实现的功能与改动**：\n  - 修改一行 print 结束符，仅在同一行的算式之间输出空格，保留嵌套循环。\n  - 修改前回归测试复现行尾空格造成的输出差异；修改后 Python 3.9.6 标准库 unittest 的 2 项测试通过，覆盖样例和全部合法输入 1～9，检查行数、分隔符、顺序、乘积、退出码及标准错误。\n  - `git diff --check` 通过；未新增依赖，未访问判题系统，远端判题结果尚未验证。\n\n- **涉及文件**：\n  - `assignments/4-261109/10.py`（+1 / -1）\n  - `tests/test_multiplication_table.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`e724433 fix: remove trailing spaces from multiplication table`，已推送至 `origin/main`。\n\n---\n\n## [2026-11-09 13:44] 8.py 单行正负数统计\n\n- **需求/问题描述**：\n  > 修复 `assignments/4-261109/8.py`，附件显示运行时抛出 TypeError。\n\n- **实际实现的功能与改动**：\n  - 调用 `split()` 并通过 `map(int, ...)` 转换整数，使用单层循环，在首个 0 处停止统计，输出正数和负数个数。\n  - 修改前测试复现附件中的 TypeError；修改后样例、仅 0、全正数、全负数、额外空白、结束标志和较大整数共 7 组实际输入输出检查通过。\n  - Python 3.9.6 标准库 unittest 全部 3 项测试通过，包含已有乘法表测试；`git diff --check` 通过。\n  - 未新增依赖，未访问判题系统，网站判题结果尚未验证。\n\n- **涉及文件**：\n  - `assignments/4-261109/8.py`\n  - `tests/test_sign_counts.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n  - `docs/CHANGELOG.md`\n\n- **Git 提交**：`63d8ce6 fix: count signed integers from one input line`，已推送至 `origin/main`。\n\n---\n"}}
{"status":"fulfilled","value":{"chunk_id":"d62b46","wall_time_seconds":0.000013666,"exit_code":0,"original_token_count":48,"output":"tests/test_sign_counts.py\ntests/test_multiplication_table.py\ncharacter2/section5/subsection5/20261012103558.py\nassignments/4-261109/8.py\nassignments/5-261116/8.py\nassignments/3-261102/8.py\n"}}
{"status":"fulfilled","value":{"chunk_id":"866760","wall_time_seconds":0.000006959,"exit_code":0,"original_token_count":5,"output":"2026-11-17 16:30\n"}}

## tool · 2026-11-17T08:31:22Z


Script completed
Wall time 7.5 seconds
Output:

{"content":[{"type":"text","text":"{\"pythonVersion\":\"Python 3.9.6\",\"environmentType\":\"venv\",\"executablePath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv/bin/python\",\"environmentPath\":\"/Users/oyamahappa/Documents/GitHub/labs/py-labs/.venv\",\"packageManager\":\"pip\"}"}],"isError":false}
{"chunk_id":"d5e0cf","wall_time_seconds":0.000007458,"exit_code":0,"original_token_count":149,"output":"assignments/5-261116/8.py:12:word_count = {}\nassignments/5-261116/8.py:14:    if word in word_count:\nassignments/5-261116/8.py:15:        word_count[word] += 1\nassignments/5-261116/8.py:17:        word_count[word] = 1\nassignments/5-261116/8.py:19:for word, count in word_count.items():\nassignments/3-261102/8.py:15:word_count={}\nassignments/3-261102/8.py:17:    if word in word_count:\nassignments/3-261102/8.py:18:        word_count[word]+=1\nassignments/3-261102/8.py:20:        word_count[word]=1\nassignments/3-261102/8.py:22:sorted_words=sorted(word_count.items(),key=lambda x:(-x[1],x[0]))\n"}
