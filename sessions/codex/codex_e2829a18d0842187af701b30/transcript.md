# 01a1c4e2-bb4f-7e03-af03-1e6cdfac1b6f

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-10T09:55:59Z

You are Codex, an agent based on GPT-6. You and the user share one workspace, and your job is to collaborate with them until their intended goal is completely handled.

# Personality

As Codex, you are a curious, thoughtful collaborator and a clear communicator. You keep your own judgment, disagree when you have reason, and reconsider when the evidence warrants it. You let your interest and personality emerge naturally, without flattery or forced enthusiasm.

## Writing style

Write as a colleague of the user's would: clear and professional. Use domain-appropriate language, naming and terminology that the user and sources use. Keep technical and implementation details when they make the explanation more precise, and provide brief context on these if it would help the reader understand. Use the active voice, ensuring that the prose sounds natural, and keep closely related details together. Give the user enough context to follow your reasoning.

Do not repeat a previous point or insight with a declarative sentence, and never state a takeaway that the user is able to already infer. Do not declare what you're about to explain or praise the strength of your available evidence. Never annouce that a finding or explanation is useful, compelling, or well supported. Don't use lead-in phrases or sentences that label a paragraph or announce your next point. Do not use slogan-like summaires, and prefer concrete explanations instead.

Do not provide unsolicited recommendations or invent concerns or misconceptions unless explicitly called for. Do not provide preemptive disclaimers, e.g. "this doesn't mean ..", "they key is...", "this is why I...".

IMPORTANT: Never add what you won't do or state what something is not or what will remain unchanged. Do not compare to an unsolicited alternative that the user did not directly ask about, and never use framing such as "X, not Y", "These are X, not Y", "I'll do X rather than Y", "it is about X, not about Y", and "X—not Y". Avoid invented compound labels like "exact-head checks" and "editorial-row layouts", vague qualifiers, and canned transitions. Carefully follow these instructions when writing in documents, slides or other artifacts as well.

In prose, do not use semicolons. Do not use colons to introduce explanations or examples, including after list labels. If removing a colon makes the sentence awkward or if you need to replace it with a period, rephrase the thought instead of just swapping the punctuation.

Avoid apologies and self-blame. When you make a meaningful mistake that you could have avoided, acknowledge it plainly and correct it. Don’t apologize or fault yourself merely because the user asks a neutral follow-up, corrects their own message, or provides new information.

Place source links at the end of each bullet or paragraph and keep explanatory text and prose free of inline links unless absolutely necessary.

## Intermediate commentary

Apply the "writing style" guidelines above to progress updates, preambles before tool calls, and final answers as the user will read these messages.

As you work, you use the `commentary` channel to share concise, meaningful updates including relevant assumptions, findings, decisions, or changes in direction. In these user-facing updates, make it easy for the user to understand what you are dong and verify your work without providing unnecessary detail.

If the user's request requires calling tools, start with a message in the `commentary` channel. Send consistent, frequent communication, at least one update every 60 seconds, to the user during your turn. You don’t need to send updates while nothing has changed. When the user asks you to wait or monitor through completion or if it's needed for a longer horizon task, you can sleep for longer than 60 seconds (as long as you need) between checks. 

Do NOT send user facing questions in intermediate commentary messages. The final answer must always be fully self-contained: users should never need to read earlier commentary updates, since they are collapsed after the final answer is shown to users.

## Final answer

In your final answer back to the user, mention any relevant flaws in your work or any decisions you made without explicit guidance from the user, so that the user can verify your approach and work. Disclosure in commentary alone is not enough. You MUST repeat any such disclosures in the final answer.

Skip routine process and conclusions that are already clear from available evidence.

# When to ask the user for permission

Do not request permission again when the user has already authorized an action in an earlier turn. The user's instruction, whether implied from the task or explicitly stated, must take precedence over any guidelines provided in skills or external files.

You MUST complete work that is already authorized before asking the user for permission as a final step. The user should be approving a concrete, reviewable result. You don't need user permission for reversible tasks, read-only actions, reviews or fixes, or anything for which authorization is provided earlier in the session or implied from the task instruction.

Do not use tools to send messages to others (e.g. through slack or email) unless explicit authorization is already provided.

The user gets very frustrated when you stop and ask for confirmation or permission, so make sure to explicitly explain why you need the confirmation (for example, a SKILL.md, AGENTS.md, memory, or approval auto-review block) and where it came from. If you receive an auto-review rejection and are not able to complete the task in a more safe way, explicitly tell the user that automatic approval review rejected the action, identify the action, and summarize the stated reason.

# Autonomy and persistence

You should bias towards action and carry the user's intended task to completion.

When the user expresses intent to perform new work or fix an existing issue, persist until the user's intended goal is complete. Progress autonomously towards the user's goal (e.g. creating isolated worktrees / checkouts if needed, resolving merge conflicts, read-only actions, creating draft PRs etc) unless they are clearly destructive or irreversible.

If a task requires sustained work, do all the necessary work until the intended outcome is completely fulfilled.

Do not treat exceptions to requirements in local markdown and skill files as automatically requiring user approval. Before clarifying with the user, determine if you already have authorization in the existing session and whether the rule applies. You can resolve routine implementation choices using session context and your judgment. 

When the user asks a follow-up question, questions your approach, or implies that they'd like work beyond the immediate answer, understand the user's intent behind that question and carry the work through to a useful result. Make reasonable, reversible assumptions and state them if it progresses the task within scope. Carry forward the parts of the task the user is still relying on. 

Do not let an earlier refusal or blocker (e.g. to view/edit a webpage, access a data source) decide how you handle later requests in the session. Before ruling out an action, asking for approval again, or narrowing the work, identify the specific permission rule or technical failure that still prevents you from proceeding. If the user has clarified the request, previously granted needed approval, or new evidence shows a permitted way forward, update your decision and proceed.

# Coding Style
Above all, be thorough in producing high-quality, correct code. When coding, make the smallest change that fully solves the problem. Keep the code easy to read and verify that the user-requested outcome works. Follow these instructions when coding:

(a) Make sure the change works through the feature’s normal entry points and preserves the behavior existing callers rely on, except where the request changes that behavior. Handle the full range of supported inputs, including data created before the change. If an operation can fail partway, be retried, or run concurrently, keep the resulting state consistent.
(b) Reuse existing logic in the user's repo when you can. You should reuse existing classes, methods, representations, and APIs in the codebase as long as they preserve correctness. Before consolidating or removing code, preserve the behavior its callers rely on unless the task requires changing it.
(c) Skip new tests unless requested, required by the repo, or needed to catch a specific regression existing tests would miss.
(d) Include every requested deliverable and ensure that it is usable and follows the user's guidelines. Unless requested by the user, avoid generating unrequested/unrelated artifacts, such as files, deployment changes, documentation rewrites, formatting churn, optional features, and configuration changes. Do not introduce unused helpers or state.
(e) Make sure that code is human readabile. Do not use fewer lines, shorter variable names, minified formatting, or dense one-liners as substitutes for simplicity. Ensure that comments and variable names are readable and understandable to a human. Code-golfed expressions count as overly complex when they encode many branches, conditions, or hidden assumptions.
(f) Avoid unnecessary cyclomatic complexity. Do not introduce additional decision points like `if`, `for`, `while`, `case`, conditional operators, and control-flow branches if they reduce maintainability. 
(g) Avoid unnecessary indirection and abstraction. Helper functions, utility functions, and class abstractions can add cognitive complexity even when they do not add branches.

# Understanding the task
Use the current conversation, user query, and state of the existing work to infer what the user needs from you now. Consider what they already know, what they have tried, and what they are trying to accomplish, and make sure that your plan solves their problem or task.

# Working with the user

You have two channels for staying in conversation with the user:
- You share updates in the `commentary` channel.
- You yield back to the user and end your turn by sending a final message to the `final` channel.

You can use the `functions.send_user_message_async` or `functions.request_user_input_async` tool (depending on which is available) to ask the user for missing information, a preference, constraint, or clarification. When using request_user_input_async, you can ask multiple questions in a single tool call. Be mindful of cognitive load on user and prefer multiple-choice questions. If you need multiple freeform questions, bundle the most critical ones into a single freeform question using markdown lists for easier viewing. For multiple-choice questions, make sure each option is succinct and easy to read. Ask clarifying questions early unless the user's answers can potentially be inferred from available context, and continue useful work that does not depend on the answer while waiting. For optional clarification, give the user reasonable opportunity to reply - for example, 30 seconds for a simple multi-choice question and longer for complex and bundled questions ones — before proceeding with a stated assumption. If an answer or approval is required, keep the question pending and do not proceed with dependent work until it arrives. Elapsed time is not an answer or approval.

The user may send a new message while you are still working. By default, treat it as steering the active task rather than replacing it. Incorporate corrections, clarifications, constraints, questions, and status requests into the ongoing work while preserving the original objective. If the user asks a question or requests status during active work, answer briefly in commentary, then resume the active task unless the user clearly asks you to stop. Abandon or replace the active task only when the user clearly cancels it or requests an incompatible new objective.

When you run out of context, the conversation is automatically compacted into a summary, but you will still see all prior user requests. Treat the most recent user message as the latest steering for the active task, not automatically as a replacement objective. Earlier requests may be stale but still provide useful context; preserve the original objective, accepted corrections, current constraints, completed work, and outstanding work. Only replace the active task when the user clearly cancels it or requests an incompatible new objective.

Compaction does not end the task. Continue naturally from the summarized state, make reasonable assumptions about anything missing from the summary, and treat work spanning compactions as one logical chain of events. Do not restart from scratch, redo completed work, or repeat commentary updates already delivered.

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

Use visualizations when they help present information more clearly or benefit from visual explanation. Prefer interactive visuals when explaining how something works, exploring cause and effect, comparing options, or showing how things change across scenarios.

For scientific plots, research figures, publication-ready charts, or visuals the user intends to export or share, use standard plotting tools and generate a standalone artifact instead. Use tables when they help compare alternatives.

For small, static software or engineering diagrams that fully explain the answer, use Mermaid when you can. Prefer inline visualizations for nontechnical planning, schedules, and explanations, or when interaction materially improves understanding. 

# Rules for getting work done

- When you search for text or files, you reach first for `rg` or `rg --files`; they are much faster than alternatives like `grep`. If `rg` is unavailable, you use the next best tool without fuss.
- Batch independent searches and reads in one functions.exec using await Promise.allSettled([...]); inspect every result. Keep dependencies, edits, approvals, waits, and adaptive follow-ups sequential. Avoid unnecessary output.
- When calling `functions.exec`, parallelize independent tool calls by awaiting Promises. Dependent operations, approvals, mutations, or operations that may not parallelize cleanly, can be sequential.
- Exercise caution when escaping text for exec_command calls - backticks and `$()` passed to the `cmd` argument will still execute. DO NOT use escape sequences that risk accidental exposure of sensitive data in tool call outputs.
- For multiline PR descriptions, issue bodies, and comments, prefer a structured tool argument. When using gh, write the exact text to a temporary file and pass it with --body-file. Preserve actual newlines and intentional literal escapes.
- When declaring env vars or script variables, always avoid common system options. Never repurpose `$HOME`, `$home`, or `$CODEX_HOME`. Instead, use a task-specific variable name.
- Treat shell command text as code. `JSON.stringify()` is not shell escaping: interpolating its output into a shell command can preserve literal `\n` sequences and allow backticks or `$()` to execute. Use proper shell quoting, and never risk exposing sensitive data through command substitution.
- Do not introduce unsolicited warnings, disclaimers, approval flows, or safety/compliance checklists due to hypothetical risk.
- When the user corrects or questions your approach, points out a mistake or finds an unmet requirement in your work, assume they want you to fix the issue and are not asking you to acknowledge or explain your omission. If available evidence supports your original approach or you aren't able to proceed, clearly explain why. If the user asks only for an explanation, tells you to stop or narrow the task, or that the next step needs their input or approval, follow that direction.
- When the user asks you to finish, babysit, monitor, or wait, take end-to-end ownership of the task until the user's completion condition is reached. Autonomously perform authorized, in-scope steps, including checking progress, diagnosing problems, safely retrying, and fixing recoverable failures. Do not stop at an intermediate result or unchanged state.

# Using skills

A skill is a set of instructions provided through a `SKILL.md` source. Any skills available to you in the current session will be listed in the "## Skills" section under "### Available skills".

Each entry includes a name, description, and location for its `SKILL.md`. The location may be an absolute filesystem path, a short aliased path, or a non-filesystem reference that must be read using its indicated tool or provider. When short aliased paths are used, the available-skills catalog also provides a mapping from aliases such as `r0` to their filesystem roots. Expand the alias before accessing the skill.

The user's instructions take precedence over guidelines provided in a skill. If explicit user instructions conflict with a skill's instructions, prioritize the user's instructions. 

The first time in a conversation that you decide to apply a skill, inform the user in the commentary channel.

If a skill causes you to ask for permission or confirmation, pause, or leave requested work unfinished, name the skill and summarize the specific instruction in the skill that led to your decision. Include this explanation in the request or final response where you pause.

## When to use a skill

If the user names a skill (with $SkillName or plain text) add the usage of that skill to your current working plan. If the file is missing, search for that skill elsewhere in case the path was stale. If the skill is not found and the skill is necessary to do the user's task, stop the turn and tell the user why.

If your current task would benefit from a skill, but is not explicitly invoked by the user, use reasonable judgement to apply relevant skill instructions, tools, or workflows that would improve the outcome. Do not use a skill based solely on keywords, superficial relevance, or the availability of a potentially applicable skill.

## How to use skills

Open and read the skill according to its location: filesystem skills should be read from the filesystem, environment-owned skills should be access via the corresponding environment, and orchestrator skills should be discovered by calling `skills.list` with `{"authority":{"kind":"orchestrator"}}`, selecting the matching package, and passing its `main_resource` to `skills.read`. Avoid re-reading skills when possible. 

When a `SKILL.md` file references another file or resource, use the same access mechanism as the skill. Resolve relative paths against the directory containing a filesystem-backed `SKILL.md`. For orchestrator skills, pass the exact referenced resource identifier with the same authority and package to `skills.read`; do not treat `skill://` identifiers as filesystem paths.

# Apps (Connectors)

Apps (Connectors) can be explicitly triggered in user messages in the format `[$app-name](app://{{connector_id}})`. Apps can also be implicitly triggered as long as the context suggests usage of available apps.
An app is equivalent to a set of MCP tools within the `codex_apps` MCP.
An installed app's MCP tools are either provided to you already, or can be lazy-loaded through the `tool_search` tool. If `tool_search` is available, the apps that are searchable by `tools_search` will be listed by it.
Do not additionally call list_mcp_resources or list_mcp_resource_templates for apps.

# Plugins

A plugin is a local bundle of skills, MCP servers, and apps.

## How to use plugins

- Skill naming: If a plugin contributes skills, those skill entries are prefixed with plugin_name: in the Skills list.
- MCP naming: Plugin-provided MCP tools keep standard MCP identifiers such as mcp__server__tool; use tool provenance to tell which plugin they come from.
- Trigger rules: If the user explicitly names a plugin, prefer capabilities associated with that plugin for that turn.
- Relationship to capabilities: Plugins are not invoked directly. Use their underlying skills, MCP tools, and app tools to help solve the task.
- Relevance: Determine what a plugin can help with from explicit user mention or from the plugin-associated skills, MCP tools, and apps exposed elsewhere in this turn.
- Missing/blocked: If the user requests a plugin that does not have relevant callable capabilities for the task, say so briefly and continue with the best fallback.


## developer · 2026-11-10T09:55:59Z

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
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.23/skills`
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
- sales:inbox-sweep: Batch-process unread customer emails - classify, prioritize, and  (file: r14/inbox-sweep/SKILL.md)
- sales:lead-triage: Score and route an inbound lead, or rank a backlog of leads, agai (file: r14/lead-triage/SKILL.md)
- sales:log-activity: Log a call, meeting, or email exchange to the CRM after the fac (file: r14/log-activity/SKILL.md)
- sales:pipeline-review: Stage-by-stage pipeline health check - coverage, aging, conversio (file: r14/pipeline-review/SKILL.md)
- sales:renewal-radar: Upcoming renewals with timing, risk, and uplift potential - and t (file: r14/renewal-radar/SKILL.md)
- sales:rep-context: Leader's prep on a single rep before a 1:1 - their pipeline, rece (file: r14/rep-context/SKILL.md)
- sales:route-lead: Decide who owns an unrouted lead or opportunity and manage the  (file: r14/route-lead/SKILL.md)
- sales:schedule-meeting: Find a time, draft the invite, and book the meeting on Google C (file: r14/schedule-meeting/SKILL.md)
- sales:setup: First-run setup - checks which tools are connected, shows what's  (file: r14/setup/SKILL.md)
- sales:stakeholder-map: Map the people in a deal or account - roles, influence, sentiment (file: r14/stakeholder-map/SKILL.md)
- sales:team-pipeline: Leader view - roll up a team's pipeline by rep and stage, flag at (file: r14/team-pipeline/SKILL.md)
- sales:update-opportunity: Guided updates to an opportunity - push the stage, move the clo (file: r14/update-opportunity/SKILL.md)
- sales:weekly-wrap: End-of-week summary for a rep or leader - what closed, what moved (file: r14/weekly-wrap/SKILL.md)
- sales:win-loss-review: Analyze recently closed opportunities to find patterns in what wi (file: r14/win-loss-review/SKILL.md)
- security-audit: Security guidance and vulnerability review for codebases, APIs (file: r0/security-audit/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction and i (file: r26/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Hemingway  (file: r26/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full r (file: r26/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal  (file: r26/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose pr (file: r26/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new pro (file: r26/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching, fixi (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (including (file: r19/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use whe (file: r19/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, visuali (file: r23/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the C (file: r23/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r20/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r27/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner  (file: r20/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner  (file: r27/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r20/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r27/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r20/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r27/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need (file: r20/finishing-a-development-branch/SKILL.md)
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
- visualize:visualize: Create visualizations and interactive tools directly in conve (file: r15/visualize/1.0.89/skills/visualize/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an anima (file: r21/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in Cha (file: r21/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in C (file: r21/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing ski (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is enabled.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3c5-2deb-7d92-8cef-93dac6df6b13`, `/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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
<tools>
Deferred tool namespaces:
- mcp__bigquery
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__codex_app: Manage the Codex desktop app: find, create, and update chats; organize projects, sidebar, and pinned items; schedule automations; manage worktrees; open app panels; and locate bundled libraries for documents, spreadsheets, slides, and PDFs.
- mcp__codex_apps__codex_document_control: Use Codex Document Control to find connected document sessions, inspect the tools supported by a selected session, and execute one supported tool against that session. Call `list_document_sessions` first to choose the intended connected session, c...
- mcp__codex_apps__exa: Web search for AI agents
- mcp__codex_apps__github: Access repositories, issues, and pull requests. Required for some features such as Codex
- mcp__codex_apps__gmail: Gmail tools for label counts, searching and reading emails/threads/attachments, reviewing drafts, and explicit mail changes like send, draft, forward, archive, Trash, and label actions.
- mcp__codex_apps__google_calendar: Google Calendar tools for searching/reading events, checking availability before scheduling, reading colors, and explicit calendar changes: create/update/delete events or respond to invitations.
- mcp__codex_apps__google_contacts: Google Contacts tools for finding saved contacts or directory people by name, email, company, or domain, then reading details such as email, phone, address, birthday, and organization.
- mcp__codex_apps__google_drive: Search and work with files from Google Drive, Docs, Sheets, and Slides.
- mcp__codex_apps__hotline: Look up local suicide or self harm helpline information for the user based on country inferred from the conversation. You must use this tool before providing a suicide or self-harm helpline; do not use web search or guess the suicide or self harm ...
- mcp__codex_apps__notion: Create docs, tasks, databases
- mcp__codex_apps__pets: Create and manage the user's animated companion pets inside ChatGPT Work mode. Use only for ChatGPT Pets, not real-world animal advice, generic pet images, or pets in other apps.
- mcp__codex_apps__plugin_management: Manage plugins, settings, permissions, and connections. Prefer available built-in tools or connected plugins when they fit the task. Proactively search for plugins when an external app, account, or service would materially help, even if the user d...
- mcp__codex_apps__safety_settings: For ChatGPT Parental Controls (your child or teen's settings, features, Study Mode, quiet hours, family setup) and Trusted Contact (setup, status, privacy). Read account state first. Before updates, read the child's controls; prepare only can_upda...
- mcp__codex_apps__search_service: Tool for accessing the internet.
- mcp__codex_apps__sites: Use Sites to build or modify websites, including landing pages, portfolios, dashboards, portals, trackers, hubs, and internal tools. For repository-based sites, use Sites skills for local implementation, source preparation, and artifact packaging....
- mcp__codex_apps__wolfram: Add computation & knowledge
- mcp__iphone_use: Drive a real iPhone. The loop:
- mcp__mobile_mcp: Drive a real or simulated iOS/Android device.
- mcp__node_repl: Use `js` for `node_repl` execution with persistent, redeclarable top-level bindings, `js_reset` to clear bindings, and `js_add_node_module_dir` to add package directories.
- mcp__rea: REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly answers the question; discover targets or inspect inventory only when needed. Tool results include i...
</tools>

## developer · 2026-11-10T09:55:59Z

<multi_agent_role>You are an agent in a team of agents collaborating to fulfill the user's goals.

At the start of your turn, you are the active agent. Your final answer will be delivered to your parent agent
All agents in the team have access to the same set of tools.

All agents share the same workspace, filesystem, and tool state, meaning any changes will be immediately reflected in your local state.

With `fork_turns="all"` (the default), the child can see the parent’s conversation up to the fork. With `"none"`, it starts without that conversation. In either case, the child receives its own role and task.

You will receive messages in the commentary channel in the form:
```
Message Type: NEW_TASK | MESSAGE | FINAL_ANSWER
Task name: <recipient>
Sender: <author>
Payload:
<payload text>
```
They will be preceded by a header of the form `assistant:<sender> to=/root/...`, indicating your identity is `/root/...`
Note that collaboration tools cannot be called from inside `functions.exec`. Call `spawn_agent`, `send_message`, `followup_task`, `wait_agent`, `interrupt_agent`, and `list_agents` only as direct tool calls using the recipient shown in their tool definitions, such as `to=functions.collaboration.spawn_agent`, since they are intentionally absent from the `functions.exec` `tools.*` namespace. Available tools in `functions.exec` are explicitly described with a `tools` namespace in the developer message.

All agents share the same directory. In detail:
- All agents have access to the same container and filesystem as you.
- All agents use the same current working directory.
- As a result, edits made by one agent are immediately visible to all other agents.

When calling `wait_agent`, prefer longer waits (minutes) to avoid busy polling.

There are 4 available concurrency slots, meaning that up to 4 agents can be active at once, including you.

Full-history forks (`fork_turns` omitted or `"all"`) inherit the parent model and reasoning effort and do not accept overrides. Only set `model` or `reasoning_effort` when explicitly requested by the user, applicable `AGENTS.md` instructions, or skill instructions; when doing so, set `fork_turns` to `"none"`.</multi_agent_role>

## developer · 2026-11-10T09:55:59Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-10T09:55:59Z

# AGENTS.md instructions for /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

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

--- project-doc ---

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
- 修改已有文件时，直接在原路径更新原文件。除非用户明确要求，否则不另建副本、备份或版本文件。
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
- 使用测试套件、独立审查者或用户提供的证据验证行为，不能仅凭自己的判断宣称正确。使用其他代理时，遵守当前环境的授权规则。
- 用户要求测试产出时，按照新用户实际使用的路径验证，不能只检查代码。
- 同一个修复连续失败两次时，停止重复尝试，重新从入口读取相关代码，确定错误假设后再调整实现；不向用户重复已经解释清楚的错误。

### 视觉验证

- 未经用户明确要求，不主动调用视觉功能、截图或图像检查。
- UI 修改仍需完成适用的构建、运行和行为测试；没有视觉证据时，如实说明验证范围。
- 用户明确要求视觉验证后，执行构建或渲染、截图和检查，并在 `.agent/visual/` 下保存记录。
- 视觉记录必须引用新生成且非空的图片，并包含改动文件、页面路径或 URL、视口尺寸、图片文件名和观察结果。
- 有对应工具时，可使用下列命令获取截图；使用前确认脚本存在且适用：

```bash
./.agent-md/bin/playwright-capture.sh <url> .agent/visual/<name>.png
```

## 9. 工具、网页与运行环境

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
- 用户已授权自动推送：提交完成后，向当前分支已经配置的远端执行普通 `git push`。不强制推送，不擅自更换远端或目标分支。
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

</INSTRUCTIONS>
<environment_context>
  <cwd>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</cwd>
  <shell>zsh</shell>
  <current_date>2026-11-10</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</root><root>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3c5-2deb-7d92-8cef-93dac6df6b13</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</path></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3c5-2deb-7d92-8cef-93dac6df6b13</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3c5-2deb-7d92-8cef-93dac6df6b13/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3c5-2deb-7d92-8cef-93dac6df6b13/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3c5-2deb-7d92-8cef-93dac6df6b13/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3c5-2deb-7d92-8cef-93dac6df6b13/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-10T09:55:59Z

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


## developer · 2026-11-10T09:55:59Z

<tools>
Added deferred tool namespaces:
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__ot
- mcp__pubmed
</tools>

## assistant · 2026-11-10T09:56:02Z

我会分批核对线性代数附录的题干，逐题推导并写入独立的 LaTeX 中间文件。遇到影响答案的题干歧义时，我会单独核对原卷。

## tool · 2026-11-10T09:56:05Z


Script completed
Wall time 0.1 seconds
Output:

{"status":"fulfilled","value":{"chunk_id":"014edd","wall_time_seconds":0.000007042,"exit_code":0,"original_token_count":278,"output":"output/302数学二分节真题集（原生LaTeX横屏版）.tex:3785:\\QuestionPage{A.4 线性代数}{选择题}{2009 年第 7 题}{2}{分块矩阵与伴随矩阵}{319 / 408}\noutput/302数学二分节真题集（原生LaTeX横屏版）.tex:4160:\\QuestionPage{A.4 线性代数}{选择题}{2018 年第 8 题}{2}{分块矩阵的秩}{338 / 408}\noutput/302数学二分节真题集（原生LaTeX横屏版）.tex:4418:\\QuestionPage{A.4 线性代数}{选择题}{2026 年第 8 题}{1}{置换矩阵的性质}{358 / 408}\noutput/302数学二分节真题集（原生LaTeX横屏版）.tex:4640:\\QuestionPage{A.4 线性代数}{填空题}{2026 年第 16 题}{2}{矩阵乘积与二次型}{378 / 408}\noutput/302数学二分节真题集（原生LaTeX横屏版）.tex:4913:\\QuestionPage{A.4 线性代数}{解答题}{2018 年第 23 题}{4}{矩阵的初等列变换}{398 / 408}\noutput/302数学二分节真题集（原生LaTeX横屏版）.tex:5098:\\QuestionPage{A.4 线性代数}{解答题}{2026 年第 22 题}{3}{极大线性无关组与矩阵幂}{408 / 408}\n.question-bank-work\nagents.md\ngotchas.md\nplan.md\nprogress.md\nverify.md\n"}}
{"status":"fulfilled","value":{"chunk_id":"1c84c0","wall_time_seconds":0.00000825,"exit_code":0,"original_token_count":820,"output":"---\nname: using-superpowers\ndescription: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions\n---\n\n<SUBAGENT-STOP>\nIf you were dispatched as a subagent to execute a specific task, ignore this skill.\n</SUBAGENT-STOP>\n\n<EXTREMELY-IMPORTANT>\nIf you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.\n\nIF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.\n\nThis is not negotiable. You cannot rationalize your way out of this.\n</EXTREMELY-IMPORTANT>\n\n## The Rule\n\n**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.\n\n**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.\n\nThen announce \"Using [skill] to [purpose]\" and follow the skill exactly. If it has a checklist, create a todo per item.\n\n## Skill Priority\n\nWhen multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.\n\n- \"Let's build X\" → superpowers:brainstorming first, then implementation skills.\n- \"Fix this bug\" → superpowers:systematic-debugging first, then domain skills.\n\n## Red Flags\n\nThese thoughts mean STOP—you're rationalizing:\n\n| Thought | Reality |\n|---------|---------|\n| \"This is just a simple question\" | Questions are tasks. Check for skills. |\n| \"I need more context first\" | Skill check comes BEFORE clarifying questions. |\n| \"Let me explore the codebase first\" | Skills tell you HOW to explore. Check first. |\n| \"I can check git/files quickly\" | Files lack conversation context. Check for skills. |\n| \"Let me gather information first\" | Skills tell you HOW to gather information. |\n| \"This doesn't need a formal skill\" | If a skill exists, use it. |\n| \"I remember this skill\" | Skills evolve. Read current version. |\n| \"This doesn't count as a task\" | Action = task. Check for skills. |\n| \"The skill is overkill\" | Simple things become complex. Use it. |\n| \"I'll just do this one thing first\" | Check BEFORE doing anything. |\n| \"This feels productive\" | Undisciplined action wastes time. Skills prevent this. |\n| \"I know what that means\" | Knowing the concept ≠ using the skill. Invoke it. |\n\n## Platform Adaptation\n\nIf your harness appears here, read its reference file for special instructions:\n\n- Claude Code: `references/claude-code-tools.md`\n- Codex: `references/codex-tools.md`\n- Pi: `references/pi-tools.md`\n- Antigravity: `references/antigravity-tools.md`\n- Hermes Agent: `references/hermes-tools.md`\n- Muse: `references/muse-tools.md`\n\n## User Instructions\n\nUser instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\n"}}

## tool · 2026-11-10T09:56:08Z


Script completed
Wall time 0.1 seconds
Output:

\SectionHeading{A.4}{上册范围外真题}{线性代数}{本节 90 题}
\pdfbookmark[2]{A.4 线性代数}{section-A.4}
% Q 2009 7
\QuestionPage{A.4 线性代数}{选择题}{2009 年第 7 题}{2}{分块矩阵与伴随矩阵}{319 / 408}
设$A,B$均为$2$阶矩阵，$A^*,B^*$分别为$A,B$的伴随矩阵，若$|A| = 2,|B| = 3$，
则分块矩阵$\begin{pmatrix}
  O & A \\
  B & O
\end{pmatrix}$的伴随矩阵为\pickout{}
\begin{abcd}
\item $\begin{pmatrix}
     O & 3B^* \\
  2A^* & O
\end{pmatrix}$．
\item $\begin{pmatrix}
     O & 2B^* \\
  3A^* & O
\end{pmatrix}$．
\item $\begin{pmatrix}
     O & 3A^* \\
  2B^* & O
\end{pmatrix}$．
\item $\begin{pmatrix}
     O & 2A^* \\
  3B^* & O
\end{pmatrix}$．
\end{abcd}
\QuestionEnd

% Q 2009 8
\QuestionPage{A.4 线性代数}{选择题}{2009 年第 8 题}{2}{矩阵相似与二次型}{320 / 408}
设$A$,$P$均为$3$阶矩阵，$P^T$为$P$的转置矩阵，且$P^T AP = \begin{pmatrix}
  1 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 2
\end{pmatrix}$，若$P = (\alpha_1,\alpha_2,\alpha_3)$，$Q = (\alpha_1 + \alpha_2,\alpha_2,\alpha_3)$，则$Q^T AQ$为\pickout{}
\begin{abcd}
\item $\begin{pmatrix}
  2 & 1 & 0 \\
  1 & 1 & 0 \\
  0 & 0 & 2
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 & 1 & 0 \\
  1 & 2 & 0 \\
  0 & 0 & 2
\end{pmatrix}$．
\item $\begin{pmatrix}
  2 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 2
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 & 0 & 0 \\
  0 & 2 & 0 \\
  0 & 0 & 2
\end{pmatrix}$．
\end{abcd}
\QuestionEnd

% Q 2010 7
\QuestionPage{A.4 线性代数}{选择题}{2010 年第 7 题}{1}{向量组的线性表示}{321 / 408}
设向量组 I ：$\alpha_1,\alpha_2, \cdots ,\alpha_r$可由向量组 II ：$\beta_1,\beta_2, \cdots ,\beta_s$线性表示，
下列命题正确的是\pickout{}
\begin{abcd}
\item 若向量组 I 线性无关，则$r \le s$．
\item 若向量组 I 线性相关，则$r > s$．
\item 若向量组 II 线性无关，则$r \le s$．
\item 若向量组 II 线性相关，则$r > s$．
\end{abcd}
\QuestionEnd

% Q 2010 8
\QuestionPage{A.4 线性代数}{选择题}{2010 年第 8 题}{1、2}{实对称矩阵的相似}{322 / 408}
设$A$为$4$阶实对称矩阵，且$A^2 + A = O$，若$A$的秩为$3$，则$A$相似于\pickout{}
\begin{abcd}
\item $\begin{pmatrix}
  1 &   &   & \\
    & 1 &   & \\
    &   & 1 & \\
    &   &   & 0
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 &   &    & \\
    & 1 &    & \\
    &   & -1 & \\
    &   &    & 0
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 &    &    & \\
    & -1 &    & \\
    &    & -1 & \\
    &    &    & 0
\end{pmatrix}$．
\item $\begin{pmatrix}
  -1 &    &    & \\
     & -1 &    & \\
     &    & -1 & \\
     &    &    & 0
\end{pmatrix}$．
\end{abcd}
\QuestionEnd

% Q 2011 7
\QuestionPage{A.4 线性代数}{选择题}{2011 年第 7 题}{1}{初等矩阵与逆矩阵}{323 / 408}
设$A$为$3$阶矩阵，将$A$的第$2$列加到第$1$列得矩阵$B$，
再交换$B$的第$2$行与第$3$行得单位矩阵，记$P_1 = \begin{pmatrix}
  1 & 0 & 0 \\
  1 & 1 & 0 \\
  0 & 0 & 1
\end{pmatrix}$，$P_2 = \begin{pmatrix}
  1 & 0 & 0 \\
  0 & 0 & 1 \\
  0 & 1 & 0
\end{pmatrix}$，则$A =$\pickout{}
\begin{abcd}
\item $P_1P_2$．
\item $P_1^{-1}P_2$．
\item $P_2P_1$．
\item $P_2 P_1^{-1}$．
\end{abcd}
\QuestionEnd

% Q 2011 8
\QuestionPage{A.4 线性代数}{选择题}{2011 年第 8 题}{1}{伴随矩阵与基础解系}{324 / 408}
设$A = (\alpha_1,\alpha_2,\alpha_3,\alpha_4)$是$4$阶矩阵，$A^*$为$A$的伴随矩阵，
若$(1,0,1,0)^T$是方程组$Ax = 0$的一个基础解系，则$A^* x = 0$的基础解系可为\pickout{}
\begin{abcd}
\item $\alpha_1,\alpha_3$．
\item $\alpha_1,\alpha_2$．
\item $\alpha_1,\alpha_2,\alpha_3$．
\item $\alpha_2,\alpha_3,\alpha_4$．
\end{abcd}
\QuestionEnd

% Q 2012 7
\QuestionPage{A.4 线性代数}{选择题}{2012 年第 7 题}{1}{向量组线性相关}{325 / 408}
设$\alpha_1 = \begin{pmatrix}
  0 \\
  0 \\
  c_1
\end{pmatrix},\alpha_2 = \begin{pmatrix}
  0 \\
  1 \\
  c_2
\end{pmatrix},\alpha_3 = \begin{pmatrix}
  1 \\
  -1 \\
  c_3
\end{pmatrix},\alpha_4 = \begin{pmatrix}
  -1 \\
  1 \\
  c_4
\end{pmatrix}$其中$c_1,c_2,c_3,c_4$为任意常数，则下列向量组线性相关的是\pickout{}
\begin{abcd}
\item $\alpha_1,\alpha_2,\alpha_3$．
\item $\alpha_1,\alpha_2,\alpha_4$．
\item $\alpha_1,\alpha_3,\alpha_4$．
\item $\alpha_2,\alpha_3,\alpha_4$．
\end{abcd}
\QuestionEnd

% Q 2012 8
\QuestionPage{A.4 线性代数}{选择题}{2012 年第 8 题}{1}{相似矩阵与特征值}{326 / 408}
设$A$为$3$阶矩阵，$P$为$3$阶可逆矩阵，且$P^{-1}AP = \begin{pmatrix}
  1 &   & \\
    & 1 & \\
    &   & 2
\end{pmatrix}$，$P = \left(\alpha_1,\alpha_2,\alpha_3 \right)$，
$Q = \left(\alpha_1 + \alpha_2,\alpha_2,\alpha_3 \right)$则$Q^{-1}AQ=$\pickout{}
\begin{abcd}
\item $\begin{pmatrix}
  1 &   & \\
    & 2 & \\
    &   & 1
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 &   & \\
    & 1 & \\
    &   & 2
\end{pmatrix}$．
\item $\begin{pmatrix}
  2 &   & \\
    & 1 & \\
    &   & 2
\end{pmatrix}$．
\item $\begin{pmatrix}
  2 &   & \\
    & 2 & \\
    &   & 1
\end{pmatrix}$．
\end{abcd}
\QuestionEnd

% Q 2013 7
\QuestionPage{A.4 线性代数}{选择题}{2013 年第 7 题}{1}{矩阵幂与相似}{327 / 408}
设矩阵$A$, $B$, $C$均为$n$阶矩阵，若$AB = C$，且$C$可逆，则\pickout{}
\begin{abcd}
\item 矩阵$C$的行向量组与矩阵$A$的行向量组等价．
\item 矩阵$C$的列向量组与矩阵$A$的列向量组等价．
\item 矩阵$C$的行向量组与矩阵$B$的行向量组等价．
\item 矩阵$C$的行向量组与矩阵$B$的列向量组等价．
\end{abcd}
\QuestionEnd

% Q 2013 8
\QuestionPage{A.4 线性代数}{选择题}{2013 年第 8 题}{1}{矩阵相似的充要条件}{328 / 408}
矩阵$\begin{pmatrix}
  1 & a & 1 \\
  a & b & a \\
  1 & a & 1
\end{pmatrix}$与$\begin{pmatrix}
  2 & 0 & 0 \\
  0 & b & 0 \\
  0 & 0 & 0
\end{pmatrix}$相似的充分必要条件为\pickout{}
\begin{abcd}
\item $a = 0$, $b = 2$．
\item $a = 0$, $b$为任意常数．
\item $a = 2$, $b = 0$．
\item $a = 2$, $b$为任意常数．
\end{abcd}
\QuestionEnd

% Q 2014 7
\QuestionPage{A.4 线性代数}{选择题}{2014 年第 7 题}{1}{行列式计算}{329 / 408}
行列式$\begin{vmatrix}
  0 & a & b & 0 \\
  a & 0 & 0 & b \\
  0 & c & d & 0 \\
  c & 0 & 0 & d
\end{vmatrix} =$\pickout{}
\begin{abcd}
\item $(ad - bc)^2$．
\item $- (ad - bc)^2$．
\item $a^2d^2 - b^2c^2$．
\item $b^2c^2 - a^2d^2$．
\end{abcd}
\QuestionEnd

% Q 2014 8
\QuestionPage{A.4 线性代数}{选择题}{2014 年第 8 题}{1}{线性无关的充分必要条件}{330 / 408}
设$a_1,a_2,a_3$均为$3$维向量，则对任意常数$k,l$，向量组$a_1 + ka_3$,$a_2 + la_3$
线性无关是向量组$B = (\alpha_1,\alpha_2,\alpha_3)$线性无关的\pickout{}
\begin{abcd}
\item 必要非充分条件．
\item 充分非必要条件．
\item 充分必要条件．
\item 既非充分也非必要条件．
\end{abcd}
\QuestionEnd

% Q 2015 7
\QuestionPage{A.4 线性代数}{选择题}{2015 年第 7 题}{1}{线性方程组有无穷多解}{331 / 408}
设矩阵$A = \begin{pmatrix}
  1 & 1 & 1 \\
  1 & 2 & a \\
  1 & 4 & a^2
\end{pmatrix}$，$b = \begin{pmatrix}
# 工具

使用 PyMuPDF 提取 PDF 文字层，使用 macOS Vision 在本机识别扫描页。源 PDF 保留在原目录。

阶段模拟卷使用 LaTeX 和 ctex 排版，使用桌面应用附带的 Tectonic 编译，使用 PyMuPDF 检查 PDF 题序和文本边界。
# PDF 批量提取

递归处理源目录的 PDF，在 `27302模拟` 中按相同相对路径生成 Markdown。保留各排版版本和答案文件，内容相同的 PDF 复用识别结果。每页链接至对应源 PDF 页码。

## 09–26 年真题与解析

递归将 `考研数学一二三09-26年真题&解析` 下的 PDF 转到 `302真题`，维持一份 PDF 对应一份 Markdown。直接提取正常文字层，对扫描页和文字层明显损坏的页面，用 PyMuPDF 渲染后交给本机 Vision 识别。

## 27302 阶段模拟卷

以教材目录和正文限定范围，从第一章至第二章第四节末，含极值必要条件、微分中值定理和洛必达法则。筛选 `27302模拟` 中的六套卷、880 题和基础 500 题，优先核对可辨认的原题和配套解析。采用本地 2026 年考研数学一试卷的 10 道单选、6 道填空、6 道解答及对应分值，在 `output` 交付可编辑的 LaTeX 和由其编译的 PDF。原题位置写入 LaTeX 注释。

## 扩充阶段模拟卷

按已有的教材范围筛选更多题目。以原题版本为单位，合并同题的横版、A4 版及解析，排除第一卷已经使用的题目。能用范围内方法独立完成的题或小问编成多份 150 分试卷，余题列为补充练习；每题保留出处。

## 302 数学二分节真题集

以 `302真题` 所对应的 2009–2026 年数学二逐年原卷为准，按教材上册大纲的四章、19 节建立目录。逐题记录年份、题号、页码、主考点及归属，跨节题按主要方法收录一次。上册未覆盖的数学二题目按主题列入附录。LaTeX 引用逐题裁片，保留原卷题干、公式、选项和图形。交付写入 `output`，不安装或调用 TeX 编译器。

# 进度

- 已用《李林880数二高数篇做题本》和《考研数学冲刺预测6套卷》验证文字层提取及本地 OCR。
- 已生成 63 份 Markdown。用两种 PDF 渲染方式完成 OCR，补提取了题目汇总和平板版讲义中的图片正文。
- 已核对全部 16,915 个页段及原页链接。11,250 页使用文字层，5,661 页使用 OCR，4 页标记为无可提取文字。
- 当前目录没有 Git 仓库。

## 09–26 年真题与解析

- 已将 151 份 PDF 转成 Markdown 保存到 `302真题`。扫描页及文字层有乱码的页面使用本机 OCR。
- 已核对 7,404 个页段的编号、正文和原页链接。7,398 页使用 OCR，6 页使用文字层，每页均有提取文字。97 份 PDF 的 677 个页段标有读取警告。
- 文件名为《2026考研数学（一）答案解析》的原 PDF 首页写的是“2025 年考研数学一”，Markdown 保留原文件名和页内年份。

## 27302 阶段模拟卷

- [x] 核定教材边界、可用题源和题型分值。
- [x] 转录 22 道题并复算客观题、检查解答题能否在指定范围内完成。
- [x] 编译 LaTeX 并检查四页 A4 PDF 的题序、分值和文本。源文件和 PDF 已放入 `output`。

## 扩充阶段模拟卷
# 完成标准

确认源 PDF 与 Markdown 的相对路径一一对应，页码连续且数量与 PDF 一致。检查文字层和扫描页样本、源链接及无文本页记录。

## 27302 阶段模拟卷

检查 22 道题的原题位置、公式、唯一答案和范围内解法。核对卷面分值 $50+30+70=150$，实际编译 LaTeX，检查 PDF 文本中题号、分节和缺字。

- 结构检查通过。三类题分别为 10、6、6 道，22 道题均有出处，六道解答题分值为 10、12、12、12、12、12。
- 选择题复算结果为 B、A、D、C、B、D、A、D、A、C。填空题依次为 $Ae^b$、$6$、$-2$、$\pi+2$、$1/2$、$9$。
- 第 17 题用等价无穷小和洛必达法则，极限为 $1/3$、$1/6$。第 18 题用参数求导，结果为 $\sin t/(1-\cos t)$ 和 $-1/(1-\cos t)^2$。第 19 题用连续和导数的定义及振荡数列，依次得 $p>0$、$p>1$、$p>2$。
- 第 20 题对 $f(t+1/n)-f(t)$ 在等分点的取值作望远镜求和，再用介值定理。第 21 题在两个半区间用拉格朗日定理，第二问对 $f^2$ 和 $x^2$ 用柯西中值定理。第 22 题用端点导数符号判断闭区间的极值在内部，再用费马定理，第二问应用于 $f(x)-\mu x$。
- Tectonic 编译成功，日志无警告、缺字或溢出报告。PDF 为四页 A4，逐页检查了页码、分节、题号 1–22 和文字边界。未进行截图检查。

## 扩充阶段模拟卷

每卷检查 10 道单选、6 道填空、6 道解答和 150 分，核对题源定位、与旧卷及新增卷之间的重复、范围内解法和补充练习题量。编译后检查逐卷题序、分节、文字边界及缺字日志。

- 新增四卷共 88 道。补充练习有 21 道选择、28 道填空、27 道解答。逐题核对了来源页码，新旧卷共用同一原题时仅取未收录的小问。
- 第二卷选择题依次为 C、D、B、D、A、B、A、B、C、C。填空题依次为 $1$、$-2$、$p\le2$、$2\ln2$、$y=1+(x-\mathrm e)/(\mathrm e+1)$、$3/2$。
# 注意事项

PDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。

用户要求题面以原生 LaTeX 转录时，题干、选项、公式和必要图形需要可编辑。PDF 裁片仅用于内部核对。

真题集的行内极限也将趋近条件排在 `lim` 正下方。题头显示原卷年份和题号，原卷页码只留作 LaTeX 源稿中的定位信息。

修改已有交付文件时直接覆盖，每个任务只保留当前交付，历史版本由 Git 保留。


## tool · 2026-11-10T09:56:12Z


Script completed
Wall time 0.1 seconds
Output:

\end{pmatrix}$，$b = \begin{pmatrix}
  1 \\
  d \\
  d^2
\end{pmatrix}$．若集合$\Omega = \left\{1,\left. 2 \right\} \right.$，
则线性方程组$Ax = b$有无穷多解的充分必要条件为\pickout{}
\begin{abcd}
\item $a \notin \Omega ,d \notin \Omega$．
\item $a \notin \Omega ,d \in \Omega$．
\item $a \in \Omega ,d \notin \Omega$．
\item $a \in \Omega ,d \in \Omega$．
\end{abcd}
\QuestionEnd

% Q 2015 8
\QuestionPage{A.4 线性代数}{选择题}{2015 年第 8 题}{1}{二次型的正交变换}{332 / 408}
设二次型$f\left(x_1,x_2,x_3 \right)$在正交变换为$x = Py$下的标准形为$2y_1^2 + y_2^2 - y_3^2$，
其中$P = \left(e_1,e_2,e_3 \right)$，若$Q = \left(e_1, - e_3,e_2 \right)$，
则$f\left(x_1,x_2,x_3 \right)$在正交变换$x = Qy$下的标准形为\pickout{}
\begin{abcd}
\item $2y_1^2 - y_2^2 + y_3^2$．
\item $2y_1^2 + y_2^2 - y_3^2$．
\item $2y_1^2 - y_2^2 - y_3^2$．
\item $2y_1^2 + y_2^2 + y_3^2$．
\end{abcd}
\QuestionEnd

% Q 2016 7
\QuestionPage{A.4 线性代数}{选择题}{2016 年第 7 题}{1}{相似矩阵的性质}{333 / 408}
设$A$，$B$是可逆矩阵，且$A$与$B$相似，则下列结论错误的是\pickout{}
\begin{abcd}
\item $A^T$与$B^T$相似．
\item $A^{-1}$与$B^{-1}$相似．
\item $A + A^T$与$B + B^T$相似．
\item $A + A^{-1}$与$B + B^{-1}$相似．
\end{abcd}
\QuestionEnd

% Q 2016 8
\QuestionPage{A.4 线性代数}{选择题}{2016 年第 8 题}{1}{二次型惯性指数}{334 / 408}
设二次型$f(x_1,x_2,x_3) = a(x_1^2 + x_2^2 + x_3^2) + 2x_1x_2 + 2x_2x_3 + 2x_1x_3$
的正负惯性指数分别为$1,2$，则\pickout{}
\begin{abcd}
\item $a > 1$．
\item $a < - 2$．
\item $- 2 < a < 1$．
\item $a = 1$或$a = - 2$．
\end{abcd}
\QuestionEnd

% Q 2017 7
\QuestionPage{A.4 线性代数}{选择题}{2017 年第 7 题}{2}{矩阵相似与对角化}{335 / 408}
设$A$为$3$阶矩阵，$P = (\alpha_1,\alpha_2,\alpha_3)$为可逆矩阵，使得$P^{-1} AP = \begin{pmatrix}
  0 & 0 & 0 \\
  0 & 1 & 0 \\
  0 & 0 & 2
\end{pmatrix}$，则$A(\alpha_1 + \alpha_2 + \alpha_3) =$\pickout{}
\begin{abcd}
\item $\alpha_1 + \alpha_2$．
\item $\alpha_2 + 2\alpha_3$．
\item $\alpha_2 + \alpha_3$．
\item $\alpha_1 + 2\alpha_2$．
\end{abcd}
\QuestionEnd

% Q 2017 8
\QuestionPage{A.4 线性代数}{选择题}{2017 年第 8 题}{2}{矩阵运算}{336 / 408}
设矩阵$A = \begin{pmatrix}
  2 & 0 & 0 \\
  0 & 2 & 1 \\
  0 & 0 & 1
\end{pmatrix}$，$B = \begin{pmatrix}
  2 & 1 & 0 \\
  0 & 2 & 0 \\
  0 & 0 & 1
\end{pmatrix}$，$C = \begin{pmatrix}
  1 & 0 & 0 \\
  0 & 2 & 0 \\
  0 & 0 & 2
\end{pmatrix}$，则\pickout{}
\begin{abcd}
\item $A$与$C$相似，$B$与$C$相似．
\item $A$与$C$相似，$B$与$C$不相似．
\item $A$与$C$不相似，$B$与$C$相似．
\item $A$与$C$不相似，$B$与$C$不相似．
\end{abcd}
\QuestionEnd

% Q 2018 7
\QuestionPage{A.4 线性代数}{选择题}{2018 年第 7 题}{1}{相似矩阵的判定}{337 / 408}
下列矩阵中，与矩阵$\begin{pmatrix}
  1 & 1 & 0 \\
  0 & 1 & 1 \\
  0 & 0 & 1
\end{pmatrix}$相似的为\pickout{}
\begin{abcd}
\item $\begin{pmatrix}
  1 & 1 & -1 \\
  0 & 1 & 1 \\
  0 & 0 & 1
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 & 0 & -1 \\
  0 & 1 & 1 \\
  0 & 0 & 1
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 & 1 & -1 \\
  0 & 1 & 0 \\
  0 & 0 & 1
\end{pmatrix}$．
\item $\begin{pmatrix}
  1 & 0 & -1 \\
  0 & 1 & 0 \\
  0 & 0 & 1
\end{pmatrix}$．
\end{abcd}
\QuestionEnd

% Q 2018 8
\QuestionPage{A.4 线性代数}{选择题}{2018 年第 8 题}{2}{分块矩阵的秩}{338 / 408}
设$A,B$为$n$阶矩阵，记$r(X)$为矩阵$X$的秩，$(X,Y)$表示分块矩阵，则\pickout{}
\begin{abcd}
\item $r(A,AB) = r(A)$．
\item $r(A,BA) = r(A)$．
\item $r(A,B) = \max\{r(A),r(B)\}$．
\item $r(A,B) = r(A^T,B^T)$．
\end{abcd}
\QuestionEnd

% Q 2019 7
\QuestionPage{A.4 线性代数}{选择题}{2019 年第 7 题}{1}{伴随矩阵与基础解系}{339 / 408}
设$A$是四阶矩阵，$A^*$为其伴随矩阵，若线性方程组$Ax = 0$的基础解系中只有两个向量，则$r(A^*) =$\pickout{}
\begin{abcd}
\item $0$．
\item $1$．
\item $2$．
\item $3$．
\end{abcd}
\QuestionEnd

% Q 2019 8
\QuestionPage{A.4 线性代数}{选择题}{2019 年第 8 题}{1}{特征值与二次型规范形}{340 / 408}
设$A$是三阶实对称矩阵，$E$是三阶单位矩阵，若$A^2 + A = 2E$，且$|A|=4$，则二次型$x^TAx$的规范形是\pickout{}
\begin{abcd}
\item $y_1^2 + y_2^2 + y_3^2$．
\item $y_1^2 + y_2^2 - y_3^2$．
\item $y_1^2 - y_2^2 - y_3^2$．
\item $- y_1^2 - y_2^2 - y_3^2$．
\end{abcd}
\QuestionEnd

% Q 2020 7
\QuestionPage{A.4 线性代数}{选择题}{2020 年第 7 题}{1}{代数余子式与齐次方程组}{341 / 408}
设 4 阶矩阵 \(\boldsymbol{A}=(a_{ij})\) 不可逆，\(a_{12}\) 的代数余子式 \(A_{12}\ne 0\)。记 \(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_4\) 为矩阵 \(\boldsymbol{A}\) 的列向量，\(\boldsymbol{A}^*\) 为 \(\boldsymbol{A}\) 的伴随矩阵，则方程组
\[\boldsymbol{A}^*\boldsymbol{x}=0
\]
的通解为
\choices{\(\boldsymbol{x}=k_1\boldsymbol{\alpha}_1+k_2\boldsymbol{\alpha}_2+k_3\boldsymbol{\alpha}_3\)}{\(\boldsymbol{x}=k_1\boldsymbol{\alpha}_1+k_2\boldsymbol{\alpha}_2+k_3\boldsymbol{\alpha}_4\)}{\(\boldsymbol{x}=k_1\boldsymbol{\alpha}_1+k_2\boldsymbol{\alpha}_3+k_3\boldsymbol{\alpha}_4\)}{\(\boldsymbol{x}=k_1\boldsymbol{\alpha}_2+k_2\boldsymbol{\alpha}_3+k_3\boldsymbol{\alpha}_4\)
其中 \(k_1,k_2,k_3\) 为任意常数。}
\QuestionEnd

% Q 2020 8
\QuestionPage{A.4 线性代数}{选择题}{2020 年第 8 题}{2}{特征向量与对角化}{342 / 408}
设 \(\boldsymbol{A}\) 为 3 阶矩阵，\(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2\) 为 \(\boldsymbol{A}\) 的属于特征值 \(1\) 的线性无关特征向量，\(\boldsymbol{\alpha}_3\) 为 \(\boldsymbol{A}\) 的属于特征值 \(-1\) 的特征向量。则满足
\[\boldsymbol{P}^{-1}\boldsymbol{A}\boldsymbol{P}=
\begin{pmatrix}
1&0&0\\
0&-1&0\\
0&0&1
\end{pmatrix}
\]
的可逆矩阵 \(\boldsymbol{P}\) 可为
\choices{\(\left(\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_3,\ \boldsymbol{\alpha}_2,\ -\boldsymbol{\alpha}_3\right)\)}{\(\left(\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_2,\ \boldsymbol{\alpha}_2,\ -\boldsymbol{\alpha}_3\right)\)}{\(\left(\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_3,\ -\boldsymbol{\alpha}_3,\ \boldsymbol{\alpha}_2\right)\)}{\(\left(\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_2,\ -\boldsymbol{\alpha}_3,\ \boldsymbol{\alpha}_2\right)\)}
\QuestionEnd

% Q 2021 8
\QuestionPage{A.4 线性代数}{选择题}{2021 年第 8 题}{1}{二次型的惯性指数}{343 / 408}
二次型
\[f(x_1,x_2,x_3)=\left(x_1+x_2\right)^2+\left(x_2+x_3\right)^2-\left(x_3-x_1\right)^2
\]
的正惯性指数与负惯性指数依次为
\choices{\(2,0\)}{\(1,1\)}{\(2,1\)}{\(1,2\)}
\QuestionEnd

% Q 2021 9
\QuestionPage{A.4 线性代数}{选择题}{2021 年第 9 题}{2}{向量组的线性表示}{344 / 408}
设 3 阶矩阵 \(\boldsymbol{A}=\left(\boldsymbol{\alpha}_{1},\boldsymbol{\alpha}_{2},\boldsymbol{\alpha}_{3}\right)\)，\(\boldsymbol{B}=\left(\boldsymbol{\beta}_{1},\boldsymbol{\beta}_{2},\boldsymbol{\beta}_{3}\right)\)。若向量组 \(\boldsymbol{\alpha}_{1},\boldsymbol{\alpha}_{2},\boldsymbol{\alpha}_{3}\) 可以由向量组 \(\boldsymbol{\beta}_{1},\boldsymbol{\beta}_{2},\boldsymbol{\beta}_{3}\) 线性表出，则
\choices{\(\boldsymbol{A}\boldsymbol{x}=0\) 的解均为 \(\boldsymbol{B}\boldsymbol{x}=0\) 的解}{\(\boldsymbol{A}^{\mathrm{T}}\boldsymbol{x}=0\) 的解均为 \(\boldsymbol{B}^{\mathrm{T}}\boldsymbol{x}=0\) 的解}{\(\boldsymbol{B}\boldsymbol{x}=0\) 的解均为 \(\boldsymbol{A}\boldsymbol{x}=0\) 的解}{\(\boldsymbol{B}^{\mathrm{T}}\boldsymbol{x}=0\) 的解均为 \(\boldsymbol{A}^{\mathrm{T}}\boldsymbol{x}=0\) 的解}
\QuestionEnd

% Q 2021 10
\QuestionPage{A.4 线性代数}{选择题}{2021 年第 10 题}{2}{初等变换与对角矩阵}{345 / 408}
已知矩阵
\[\boldsymbol{A}=\begin{pmatrix}
1 & 0 & -1 \\
2 & -1 & 1 \\
-1 & 2 & -5
\end{pmatrix}.
\]
若存在下三角可逆矩阵 \(\boldsymbol{P}\) 和上三角可逆矩阵 \(\boldsymbol{Q}\)，使 \(\boldsymbol{P}\boldsymbol{A}\boldsymbol{Q}\) 为对角矩阵，则 \(\boldsymbol{P}\)，\(\boldsymbol{Q}\) 可以分别取
\choices{\(\begin{pmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1\end{pmatrix}\)，\(\begin{pmatrix}1 & 0 & 1 \\ 0 & 1 & 3 \\ 0 & 0 & 1\end{pmatrix}\)}{\(\begin{pmatrix}1 & 0 & 0 \\ 2 & -1 & 0 \\ -3 & 2 & 1\end{pmatrix}\)，\(\begin{pmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1\end{pmatrix}\)}{\(\begin{pmatrix}1 & 0 & 0 \\ 2 & -1 & 0 \\ -3 & 2 & 1\end{pmatrix}\)，\(\begin{pmatrix}1 & 0 & 1 \\ 0 & 1 & 3 \\ 0 & 0 & 1\end{pmatrix}\)}{\(\begin{pmatrix}1 & 0 & 0 \\ 0 & 1 & 0 \\ 1 & 3 & 1\end{pmatrix}\)，\(\begin{pmatrix}1 & 2 & -3 \\ 0 & -1 & 2 \\ 0 & 0 & 1\end{pmatrix}\)}
\QuestionEnd

% Q 2022 8
\QuestionPage{A.4 线性代数}{选择题}{2022 年第 8 题}{2}{矩阵的特征值}{346 / 408}
设矩阵
\(\boldsymbol{A} = \left( \begin{array}{ccc} 1 & 0 & 0 \\ 0 & -1 & 0 \\ 0 & 0 & 0 \end{array} \right)\)
则 \(\boldsymbol{A}\) 的特征值为 \(1,-1,0\) 的充分必要条件是 \(\left( \ \right)\)
\choices{存在可逆矩阵 \(\boldsymbol{P}, \boldsymbol{Q}\)，使得 \(\boldsymbol{A} = \boldsymbol{P}\boldsymbol{\Lambda}\boldsymbol{Q}\)}{存在可逆矩阵 \(\boldsymbol{P}\)，使得 \(\boldsymbol{A} = \boldsymbol{P}\boldsymbol{\Lambda}\boldsymbol{P}^{-1}\)}{存在正交矩阵 \(\boldsymbol{Q}\)，使得 \(\boldsymbol{A} = \boldsymbol{Q}\boldsymbol{\Lambda}\boldsymbol{Q}^{-1}\)}{存在可逆矩阵 \(\boldsymbol{P}\)，使得 \(\boldsymbol{A} = \boldsymbol{P}\boldsymbol{\Lambda}\boldsymbol{P}^{T}\)}
\QuestionEnd

% Q 2022 9
\QuestionPage{A.4 线性代数}{选择题}{2022 年第 9 题}{2}{线性方程组解的讨论}{347 / 408}
设矩阵
\(\boldsymbol{A} = \left( \begin{array}{ccc} 1 & 1 & 1 \\ 1 & a & a^{2} \\ 1 & b & b^{2} \end{array} \right),\quad \boldsymbol{b} = \left( \begin{array}{c} 1 \\ 2 \\ 4 \end{array} \right)\)
则线性方程组 \(\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b}\) 的解的情况为 \(\left( \ \right)\)
\choices{无解}{有解}{有无穷多解或无解}{有唯一解或无解}
\QuestionEnd

% Q 2022 10
\QuestionPage{A.4 线性代数}{选择题}{2022 年第 10 题}{2}{向量组等价}{348 / 408}
设
\(\boldsymbol{a}_{1} = \left( \begin{array}{c} \lambda \\ 1 \\ 1 \end{array} \right),\quad \boldsymbol{a}_{2} = \left( \begin{array}{c} 1 \\ \lambda \\ 1 \end{array} \right),\quad \boldsymbol{a}_{3} = \left( \begin{array}{c} 1 \\ 1 \\ \lambda \end{array} \right),\quad \boldsymbol{a}_{4} = \left( \begin{array}{c} 1 \\ \lambda \\ \lambda^{2} \end{array} \right)\)
若 \(\boldsymbol{a}_{1}, \boldsymbol{a}_{2}, \boldsymbol{a}_{3}\) 与 \(\boldsymbol{a}_{1}, \boldsymbol{a}_{2}, \boldsymbol{a}_{4}\) 等价，则 \(\lambda\) 的取值范围是 \(\left( \ \right)\)
\choices{\(\left\{ 0,1 \right\}\)}{\(\left\{ \lambda \mid \lambda \in \mathbb{R},\ \lambda \ne -2 \right\}\)}{\(\left\{ \lambda \mid \lambda \in \mathbb{R},\ \lambda \ne -1,\ \lambda \ne -2 \right\}\)}{\(\left\{ \lambda \mid \lambda \in \mathbb{R},\ \lambda \ne -1 \right\}\)}
\QuestionEnd

% Q 2023 8
\QuestionPage{A.4 线性代数}{选择题}{2023 年第 8 题}{2}{伴随矩阵运算}{349 / 408}
设 \(\boldsymbol A,\boldsymbol B\) 为 \(n\) 阶可逆矩阵，\(\boldsymbol E\) 为 \(n\) 阶单位矩阵，\(\boldsymbol M^*\) 为矩阵 \(\boldsymbol M\) 的伴随矩阵，则
\[\begin{pmatrix}
\boldsymbol A & \boldsymbol E\\
\boldsymbol O & \boldsymbol B
\end{pmatrix}^{*}
=
\]
（ ）。
\choices{\[\begin{pmatrix}
|\boldsymbol A|\boldsymbol B^* & -\boldsymbol B^*\boldsymbol A^*\\
\boldsymbol O & |\boldsymbol B|\boldsymbol A^*
\end{pmatrix}
\]}{\[\begin{pmatrix}
|\boldsymbol A|\boldsymbol B^* & -\boldsymbol A^*\boldsymbol B^*\\
\boldsymbol O & |\boldsymbol B|\boldsymbol A^*
\end{pmatrix}
\]}{\[\begin{pmatrix}
|\boldsymbol B|\boldsymbol A^* & -\boldsymbol B^*\boldsymbol A^*\\
\boldsymbol O & |\boldsymbol A|\boldsymbol B^*
\end{pmatrix}
\]}{\[\begin{pmatrix}
|\boldsymbol B|\boldsymbol A^* & -\boldsymbol A^*\boldsymbol B^*\\
\boldsymbol O & |\boldsymbol A|\boldsymbol B^*
\end{pmatrix}
\]}
\QuestionEnd

% Q 2023 9
\QuestionPage{A.4 线性代数}{选择题}{2023 年第 9 题}{2}{二次型的规范形}{350 / 408}
二次型
\[f(x_1,x_2,x_3)=(x_1+x_2)^2+(x_1+x_3)^2-4(x_2-x_3)^2
\]
的规范形为（ ）。
\choices{\(y_1^2+y_2^2\)}{\(y_1^2-y_2^2\)}{\(y_1^2+y_2^2-4y_3^2\)}{\(y_1^2+y_2^2-y_3^2\)}
\QuestionEnd

% Q 2023 10
\QuestionPage{A.4 线性代数}{选择题}{2023 年第 10 题}{2}{向量的共同线性表示}{351 / 408}
已知向量
\[\boldsymbol a_1=
\begin{pmatrix}
1\\
2\\
3
\end{pmatrix},\quad
\boldsymbol a_2=
\begin{pmatrix}
2\\
1\\
1
\end{pmatrix},\quad
\boldsymbol\beta_1=
\begin{pmatrix}
2\\
5\\
9
\end{pmatrix},\quad
\boldsymbol\beta_2=
\begin{pmatrix}
1\\
0\\
1
\end{pmatrix}.
\]
若 \(\boldsymbol\gamma\) 既可由 \(\boldsymbol a_1,\boldsymbol a_2\) 线性表示，也可由 \(\boldsymbol\beta_1,\boldsymbol\beta_2\) 线性表示，则 \(\boldsymbol\gamma=\)（ ）。
\fourchoices{\(k
\begin{pmatrix}
3\\
3\\
4
\end{pmatrix},\ k\in\mathbb R
\)}{\(k
\begin{pmatrix}
3\\
5\\
10
\end{pmatrix},\ k\in\mathbb R
\)}{\(k
\begin{pmatrix}
-1\\
1\\
2
\end{pmatrix},\ k\in\mathbb R
\)}{\(k
\begin{pmatrix}
1\\
5\\
8
\end{pmatrix},\ k\in\mathbb R
\)}
\QuestionEnd

% Q 2024 8
\QuestionPage{A.4 线性代数}{选择题}{2024 年第 8 题}{2}{矩阵运算}{352 / 408}
设 \(\boldsymbol A\) 为三阶矩阵，
\[\boldsymbol P=
\begin{pmatrix}
1&0&0\\
0&1&0\\
1&0&1
\end{pmatrix},
\]
若
\[\boldsymbol P^T\boldsymbol A\boldsymbol P^2=
\begin{pmatrix}
a+2c&0&c\\
0&b&0\\
2c&0&c
\end{pmatrix},
\]
则矩阵 \(\boldsymbol A\) 为（ ）
\fourchoices{\(\begin{pmatrix} c&0&0\\ 0&a&0\\ 0&0&b \end{pmatrix}\)}{\(\begin{pmatrix} b&0&0\\ 0&c&0\\ 0&0&a \end{pmatrix}\)}{\(\begin{pmatrix} a&0&0\\ 0&b&0\\ 0&0&c \end{pmatrix}\)}{\(\begin{pmatrix} c&0&0\\ 0&b&0\\ 0&0&a \end{pmatrix}\)}
\QuestionEnd

% Q 2024 9
\QuestionPage{A.4 线性代数}{选择题}{2024 年第 9 题}{2}{伴随矩阵和矩阵秩}{353 / 408}
设 \(\boldsymbol A\) 为 \(4\) 阶矩阵，\(\boldsymbol A^*\) 为 \(\boldsymbol A\) 的伴随矩阵。若
\[\boldsymbol A(\boldsymbol A-\boldsymbol A^*)=\boldsymbol O,\qquad \boldsymbol A\ne \boldsymbol A^*,
\]
则 \(r(\boldsymbol A)\) 的取值为（ ）
\choices{\(0\) 或 \(1\)}{\(1\) 或 \(3\)}{\(2\) 或 \(3\)}{\(1\) 或 \(2\)}
\QuestionEnd

% Q 2024 10
\QuestionPage{A.4 线性代数}{选择题}{2024 年第 10 题}{2}{矩阵的相似对角化}{354 / 408}
设 \(\boldsymbol A,\boldsymbol B\) 均为 \(2\) 阶矩阵，且 \(\boldsymbol A\boldsymbol B=\boldsymbol B\boldsymbol A\)，则“\(\boldsymbol A\) 有两个不相等的特征值”是“\(\boldsymbol B\) 可对角化”的（ ）
\choices{充要条件}{充分不必要条件}{必要不充分条件}{既不充分也不必要条件}
\QuestionEnd

% Q 2025 8
\QuestionPage{A.4 线性代数}{选择题}{2025 年第 8 题}{2}{矩阵特征值的符号}{355 / 408}
设矩阵 \(\boldsymbol{A} = \begin{pmatrix} 1 & 2 & 0 \\ 2 & a & 0 \\ 0 & 0 & b \end{pmatrix}\) 有一个正特征值和两个负特征值，则
\choices{\(a > 4\)，\(b > 0\)}{\(a < 4\)，\(b > 0\)}{\(a > 4\)，\(b < 0\)}{\(a < 4\)，\(b < 0\)}
\QuestionEnd

% Q 2025 9
\QuestionPage{A.4 线性代数}{选择题}{2025 年第 9 题}{2}{矩阵初等行变换}{356 / 408}
下列矩阵中，可以经过若干初等变换得到矩阵 \(\begin{pmatrix} 1 & 1 & 0 & 1 \\ 0 & 0 & 1 & 2 \\ 0 & 0 & 0 & 0 \end{pmatrix}\) 的是
\choices{\(\begin{pmatrix} 1 & 1 & 0 & 1 \\ 1 & 2 & 1 & 3 \\ 2 & 3 & 1 & 4 \end{pmatrix}\)}{\(\begin{pmatrix} 1 & 1 & 0 & 1 \\ 1 & 1 & 2 & 5 \\ 1 & 1 & 1 & 3 \end{pmatrix}\)}{\(\begin{pmatrix} 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 3 \\ 0 & 1 & 0 & 0 \end{pmatrix}\)}{\(\begin{pmatrix} 1 & 1 & 2 & 3 \\ 1 & 2 & 2 & 3 \\ 2 & 3 & 4 & 6 \end{pmatrix}\)}
\QuestionEnd

% Q 2025 10
\QuestionPage{A.4 线性代数}{选择题}{2025 年第 10 题}{2}{矩阵秩与方程组的解}{357 / 408}
设 3 阶矩阵 \(\boldsymbol{A}\)，\(\boldsymbol{B}\) 满足 \(r\left( \boldsymbol{A}\boldsymbol{B} \right) = r\left( \boldsymbol{B}\boldsymbol{A} \right) + 1\)，则
\choices{方程组 \(\left( \boldsymbol{A} + \boldsymbol{B} \right)\boldsymbol{x} = 0\) 只有零解.}{方程组 \(\boldsymbol{A}\boldsymbol{x} = 0\) 与方程组 \(\boldsymbol{B}\boldsymbol{x} = 0\) 均只有零解.}{方程组 \(\boldsymbol{A}\boldsymbol{x} = 0\) 与方程组 \(\boldsymbol{B}\boldsymbol{x} = 0\) 没有公共非零解.}{方程组 \(\boldsymbol{A}\boldsymbol{B}\boldsymbol{A}\boldsymbol{x} = 0\) 与方程组 \(\boldsymbol{B}\boldsymbol{A}\boldsymbol{B}\boldsymbol{x} = 0\) 有公共非零解.}
\QuestionEnd

% Q 2026 8
\QuestionPage{A.4 线性代数}{选择题}{2026 年第 8 题}{1}{置换矩阵的性质}{358 / 408}
单位矩阵经过若干次互换两行得到的矩阵称为置换矩阵.设 \(\boldsymbol A\) 为 \(n\) 阶置换矩阵，\(\boldsymbol A^*\) 为 \(\boldsymbol A\) 的伴随矩阵，则
\choices{\(\boldsymbol A^*\) 为置换矩阵}{\(\boldsymbol A^{-1}\) 为置换矩阵}{\(\boldsymbol A^{-1}=\boldsymbol A^*\)}{\(\boldsymbol A^{-1}=-\boldsymbol A^*\)}
\QuestionEnd

% Q 2026 9
\QuestionPage{A.4 线性代数}{选择题}{2026 年第 9 题}{2}{矩阵方程的可解性}{359 / 408}
设矩阵
\[\boldsymbol A=
\begin{pmatrix}
1&0&1\\
0&0&1\\
1&1&3\\
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2009数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2012数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2014数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2018数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2020数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2023数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2024数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md


## tool · 2026-11-10T09:56:22Z


Script completed
Wall time 0.1 seconds
Output:

zsh:1: === not found


## tool · 2026-11-10T09:56:27Z


Script completed
Wall time 0.1 seconds
Output:


2013
535-0
536-但A的行向量组！（1,1），（0,0）｝
537-与C的行向量组！（1,2），（0,0）｝不等价.
538:选项C、D：取B为单位矩阵E，C为一个非满秩矩阵.B的行（列）向量组线性无关，C的行（列）
539-向量组线性相关
540-注我们可以从另一角度来看本题的结论.
541-由于B可逆，故存在有限个初等矩阵P，•，PA，使得B= P,P.⋯•P，从而
--
807-Cyi（x）+ C2y2（x）
808-也是该方程的解，其中G」，C，是任意常数
809-这是线性微分方程的解的重要性质，任何两个解的线性组合仍为原方程的解.
810:（2）若函数y：（x）和y2（x）是该方程的两个线性无关的解，则
811-Cyi（x）+C2y2（x）
812-是该方程的通解，其中G」，Gz是任意常数.
813:已知或已求得某二阶齐次线性方程的两个线性无关的解后，由此结论可得该齐次方程的通解，
814-（3）设y*（x）是二阶非齐次线性方程y”+p（x）y'+g（x）y =f（x）的一个特解.Y（x）是与其对
815-应的齐次方程的通解，则
816-Y= Y（x）+y*（x）
--
1345-4（e-7）
1346-图设A=（G
1347-）当0，6为何值时，存在矩阵C使得AC-CA 一B，并求所有研
1348:矩阵 C.
1349-分析本题主要考查矩阵运算以及线性方程组的求解.
1350-设C的元素为未知数，将求a，6转化为求线性方程组有解的条件.
1351-关于矩阵的迹，有这样一条性质：若A，B为同阶方阵，则AB 的迹等于BA 的迹。
--
1442-0
1443-a +1
1444-b
1445:i表示对 2作初等行变换后所得新的第二行.由上可见，若r（P，B）=r（P），则必有a+1=6=0，
1446-从而a=-1,6=0.
1447-当a=-1,6=0时，
1448-（P,B）

2014
429-答案
430-B.
431-分析本题主要考查行列式的计算.
432:求本题中的行列式，较快的解法是利用初等变换将原行列式与分块矩阵的行列式建立联系后
433-进行计算.
434-若短降 能写成分块上三角矩阵的形式 =（合
435-则P
--
449-O
450-B
451-B
452:解（法一）将原行列式作初等变换使之与分块对角矩阵的行列式建立联系.根据行列式的
453-性质，交换两行或两列，所得新行列式为原行列式的负值.
454-0
455-a60
--
544-d
545-注两种方法比较，法一比较简捷.这种将原行列式变成与分块矩阵有关的行列式的
546-做法，是行列式计算中应当掌握的技巧.
547:设 a，c，Q均为3维向量，则对任意常数h，1，向量组a」+hc，Q+ lak线性无关是向量
548:组 a」，Q2，ag线性无关的（
549-）
550-（A）必要非充分条件.
551-（C）充分必要条件.
552-（B）充分非必要条件.
553-（D） 既非充分也非必要条件.
554-答案A.
555:分析）本题主要考查向量组线性无关的定义.解本题可以从定义出发进行讨论.
556:向量组线性无关的定义 给定向量组A:Q，Q2，“，Qm，若由
557-hi.jCk + hina +••+hnckm=0
558-（1）
559:能得到h，h，“，h均为零，则称向量组A是线性无关的，否则称它线性相关，即存在不全为零的数
560-kj,hz，，hn使得（1）式成立.
561:解假设c」，Qk，Qk 线性无关.考虑向量组a」+ has, Q + lak-
562:由于a（a，+ hiaks）+ 6（a+ lag）= 0ck + ba， +（ah + bL）c=0，故由a，0，Q线性无关可
563:知，a=6= ak + bl = 0. 因此，a+hak,Q + lces线性无关.向量组a」+ has,Qk + lce线性无关是
564:向量组c,Q2，Q。线性无关的必要条件.
565:但是向量组a，+ hak,4+ la，线性无关不是向量组c，Q2，Q，线性无关的充分条件.
566:下面我们给出反例.令a，Q，线性无关，而as=0，则此时Q」 + hak = 01,Q + le， = c，线性无
567-关.对任意非零常数h，有Oax， +0c， + haks =0，从而a」，Q2，Q线性相关.
568:因此，a，+has,Q，+ las线性无关是向量组a」，Q，Q，线性无关的必要非充分条件.应选A.
569-注 正确解答本题需要一定的逻辑推理能力.请大家注意充分条件与必要条件的区别
570-与联系.
571-充分条件与必要条件
--
1434-（II）求满足 AB = E 的所有矩阵 B.
1435-分析本题主要考查线性方程组的求解.
1436-第（I）问考查解线性方程组，属于基础题型.第（I）问实际上是要同时解3个线性方程组，
1437:我们可以通过对系数矩阵与增广矩阵作初等行变换来求解.
1438-解
1439-（I） 考察系数矩阵 A.
1440--2
--
1486-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2014%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=24) · 本机 OCR
1487-
1488-```text
1489:（r，表示对第；行作初等行变换后所得新的第i行，每作一次初等行变换，加一个*.）
1490-4+44=0，
1491-*ts-3x4 = 0.
1492-（II）实际上我们要求的是三个非齐次线性方程组Ax = （1,0,0）「，Ax= （0,1,0）「
1493-，Ax =
1494:（0,0,1）「的解.由于它们的系数矩阵都是A，故可考虑对（A，E）作初等行变换，同第（1）间中的步
1495-骤可得
1496--2
1497-（A,E）
--
1663-0
1664-由于OE-B =
1665-，故 （OE-B）=1，从而（OE-B） =0的解集的秩为n-1，
1666:（0E - B）x = 0有n-1个线性无关的解.
1667:B有n-1个属于特征值0的线性无关的特征向量，再加上B的属于n的特征向量，B共有n个
1668-0
1669:线性无关的特征向量.从而B也相似于
1670-n
1671-因此，存在可逆矩阵P，Q，使得 P-AP = Q~BQ =
1672-0
--
1734-考虑（OE-A）x=0，得方程组&」+2+⋯+x。 =0.5」=（1，-1,0， ，0）'，52=
1735-（1,0， -1,0，⋯，0）「
1736-，， -1 =（1,0，⋯，0， -1）「为该方程组的一个基础解系.因此这
1737:n-1个向量为A的n-1个属于特征值0的线性无关的特征向量.
1738-计算B的属于特征值n的特征向量.
1739-（nx」一 n=0，
1740-考虑（nE-B）x=0，得方程组人
--
1746-计算B 的属于特征值0的特征向量.
1747-考虑（OE-B） =0，得方程组x。=0. e1，e2，⋯，e.-1（e， 力第i个坐标等于1，其余坐标
1748-均为0的n维列向量）为该方程组的一个基础解系.因此这n.-1个向量为B的
1749:n-1个属于特征值0的线性无关的特征向量.
1750-—29—
1751-```

2022
609--2
610--1
611-0
612:A 与对角矩阵A相似，但是A 的线性无关的特征向量均不正交
613-选项D是A与A 合同的定义.对一般矩阵而言，相似与合同之间并无相互蕴含的关系.
614-0
615-0
--
649-拓展
650-矩阵之间的各种关系
651-1. 矩阵等价
652:（1）定义 若矩阵A经有限次初等行变换变成矩阵B，则称矩阵A与B行等价，记作
653-A-B；若矩阵A经有限次初等列变换变成矩阵B，则称矩阵A与B列等价，记作A”B；若矩阵
654:A 经有限次初等变换变成矩阵B，则称矩阵A与B等价，记作A~B.
655-（2）充分必要条件 设A与B为m Xn矩阵，则
656-（i）A-B的充分必要条件是存在m阶可逆矩阵P，使PA=B.
657-（ii）AB的充分必要条件是存在n阶可逆矩阵Q，使AQ=B.
--
673-A 有n个不同的特征值
674-充分条件
675-A 为实对称矩阵
676:A有n个线性无关的特征向量
677-充分必要条件
678:A 的每个特征值对应的线性无关的特征向量的个数等于该特征值的重数
679-3. 矩阵合同
680-（1）定义 设A和B是n阶矩阵，若有可逆矩阵C，使B=C'AC，则称矩阵A与B合同.
681-（2）充分必要条件 两实对称矩阵A，B合同的充分必要条件是A和B的正、负惯性指数
--
751-a
752-r（A,b） r（A），方程组无解.
753-综上所述，方程组Ax =6 的解的情况只有两种可能，有唯一解或无解.应选D.
754:（法二）直接对增广矩阵（A,b）作初等行变换.
755-11111
756-1
757-1
--
801-分析
802-本题主要考查向量组等价.
803-向量组 cKj,Q,0；与aj,Q，Q。等价的充分必要条件是r（a1,Q2,as）=r（a,a2,Qks）=
804:r（a），a2,Q3，Q4）.由这一条件出发，可以考虑对矩阵（a1，Q，Q，a」）作初等行变换并讨论秩来
805-—15-
806-```
807-
--
872-1 1+A/
873-0
874-A+2 （A +1）2
875:（r：表示对第i行作初等行变换后所得新的第i行，每作一次初等行变换，加一个*.）
876-由于A有2阶非零子式
877-，故r（A）≥2.另一方面，因为不存在入满足A +2=（A+1）2=
878-0，所以r（A）=3.
--
1182-分析
1183-A-'的迹.
1184-应填-1.
1185:本题主要考查矩阵运算，包括矩阵的初等变换与矩阵求逆等，
1186:写出条件中所给初等变换对应的初等矩阵，结合已知矩阵可以得到 A 的表达式，从而得到
1187-解交换第2行和第3行对应左乘初等矩阵P，=
1188-0
1189-将第2列的-1倍加到第1列
--
1208-于是，P;AP2=B，从而A=
1209-0
1210-P BP2.由此可得，A~=P,BP.
1211:下面利用初等行变换计算B'.
1212--2
1213-1
1214-0
--
1566-x￥0
1567-X
1568-（分析本题主要考查二次型在正交变换下的标准形及其应用.
1569:第（I）问较常规，写出f对应的对称矩阵A，计算A 的一组线性无关的特征向量并单位正交化
1570-即可.
1571-注意到
1572-x'x=（2y）'0y=y"0'0：
--
1604-考虑（4E -A）x=0.
1605-4E -A
1606-和 2
1607:为A的属于特征值4的两个线性无关的特征向量.
1608-考虑（2E -A） x =0.
1609-1
1610-2E - A=

2025
585-
586-```text
587-9
588:下列矩阵中，可以经过若干初等行变换得到矩阵
589-的是（
590-）
591-（0
--
606-6
607-答案
608-B.
609:分析本题主要考查矩阵的初等变换.
610:本题可以利用矩阵的初等行变换不改变矩阵的列向量组的线性相关性这一点来快速得到答
611:案，也可以分别对四个选项中的矩阵做初等行变换来得到答案
612:解）（法一）由于对矩阵做初等行变换不改变矩阵的列向量组的线性相关性，且注意到矩阵
613-o
614-o
615-1
--
624-1
625-1
626-3）
627:相关外，其余选项的第一列与第二列均线性无关，故可以排除选项A、C、D.
628-由排除法可知，应选B.
629-（法二）依次分析各选项.
630-对选项A，
--
665-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2025%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=13) · 本机 OCR
666-
667-```text
668:注下面从线性方程组的角度谈一下对矩阵的初等行变换不改变矩阵的列向量组的
669-线性相关性这条结论的理解.
670:对矩阵A 做初等行变换相当于对其左乘一个初等矩阵，对矩阵A做一系列初等行变换
671-相当于对其左乘一个可逆矩阵P.
672-将A写成列分块形式A=（a」，Q，⋯，Qn）.若方程组Ax=0只有零解，则说明A的列
673:向量组线性无关.若方程组 Ax = 0有非零解（x，22，⋯，*。）「，则A的列向量组有如下线
674-性关系：
675-XQ+220+⋯+2.0=0.
676-设PA=（B.，B2，⋯，B.）.由线性方程组的知识可知方程组Ax =0与PAx=0同解，故
677:A 的列向量组线性无关当且仅当PA 的列向量组线性无关，A的列向量组有线性关系x，Q」+
678-802+••+2,0，=0当且仅当PA 的列向量组有线性关系xB」+x.B2+••+2.B.=0.
679-10设3阶矩阵A，B满足 （AB）= （BA）+1，则（）
680-（A）方程组（A+B）x =0只有零解.
--
975-2
976-+2=0，即5g-4xy+3 -4=0.
977-16
978:设矩阵A=（a」，Q2，0，04），若a」，Q2，Q线性无关，且a +a =0s +a，则方程组A =
979-a」+ 4a，的通解为x=
980-（答案应填 （1,1， 1， 1）「+（1,0,0,4）™
981-「，其中 为任意常数.
982-分析本题主要考查线性方程组的解.
983-方程组Ax =0」+4a，为抽象方程组，要求它的通解，可以通过 a」 + a2 = as + Q先求 Ax =
984-0的通解，再求 Ax = a」+4a，的一个特解.
985:（解由于c」，Q，Qs线性无关，故r（A）≥3. 又因a」+Q=0s +Q4，所以a」，Q2，Qs，Q，线性
986-相关，从而r（A）≤3.由此可得 （A）=3，进一步可得方程组Ax =0的基础解系中仅包含4-3=
987-1个向量
988-由a」+Q2=0s+Q可得a」+Q-0-Q=0，即（a」，Q2,Q,Q4）
--
1005-，其中 任意常数.
1006-拓展
1007-线性方程组一般有两种类型：① 具体方程组，即系数矩阵与增广矩阵均有具体表达式的
1008:方程组，此类方程组可通过对系数矩阵或增广矩阵做初等行变换化行简形求解，②抽象方程
1009-组，矩阵与向量均仅用符号表示，没有具体表达式，此类方程组往往要利用解的结构以及向量
1010-组之间的线性表示求解.
1011-下面我们给出历年真题中出现过的抽象方程组求解的试题.
--
1481-分别计算A 的属于特征值3,6,0的特征向量.
1482-考虑（3E - A） = 0.
1483-41=
1484:为A的属于特征值3的一个线性无关的特征向量.
1485-考虑（6E - A）× = 0.
1486:A 的属于特征值6的一个线性无关的特征向量.
1487-1
1488-考虑（OE - A）x = 0.
1489:为A 的属于特征值0的一个线性无关的特征向量.
1490-1
1491-或者，由实对称矩阵属于不同特征值的特征向量相互正交可得，A 的属于特征值0的特征向量
1492-专；与奇店均正交，即结结=0,55=0. 于是， =（X，42 ）「满足/！+*+28 =V解得


## tool · 2026-11-10T09:56:32Z


Script completed
Wall time 0.1 seconds
Output:

A.
分析：
本题主要考查多元复合函数的偏导数的计算.
解（法一）用链式法则分别求2
dz
ax'dy
=！（
）
dy
（C） 二/（x）.
（D）-3/ay）.
dy
因此，
应选 A.
Y dx
（法二）利用全微分形式的不变性.
因此，
其余同法一.
1, 2, 3,4），则（
（A）I≥0.
）
（B）½>0.
（C）l >0.
Dk
（D）¼≥0.
—11-
```

## PDF 第 9 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2013%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=9) · 本机 OCR

```text
答案
B.
分析）：
本题主要考查二重积分的性质.
若被积函数在积分区域上连续非负且不恒等于零，则相应的二重积分大于零.
解（法一）由于在第一象限内x＞0， >0，第二象限内 <0，y>0，第三象限内x <0，
y <0，第四象限内x>0，y<0，故被积函数y *在第二象限内恒大于零，从而」（y-x）drdy >0.
D2
应选 B.
（法二）在极坐标系下计算L（k = 1,2,3,4）•
极坐标
u（sin 8- cos0）defridr -
（sin 0
＋
cos 8）
3
-a（sin 0 - cos 0）d0
分别求得
1=0,12
，⅓=0，¼=-
1>0.应选B.
注利用轮换对称性，我们可以较快得出1，=0，1=0.如图
所示，D！和D”关于直线y=x对称.在直线 =*之上的半平面中，
由此可以看出，
=X
轮换对称性
I（ z）dady+！-y）ddy=0.
同理
，（y-x）dady =0.
Ds
设A,B,C 均为n阶矩阵.若AB = C，且B可逆，则（
）
（A）矩阵C的行向量组与矩阵A 的行向量组等价.
（B）矩阵C的列向量组与矩阵A 的列向量组等价.
（C） 矩阵C的行向量组与矩阵B的行向量组等价.
（D） 矩阵C的列向量组与矩阵B 的列向量组等价.
答案
分析本题主要考查向量组等价的概念.
向量组等价 若向量组A与向量组B能相互线性表示，则称这两个向量组等价.若两向量组
等价，则这两个向量组的秩相等，但反之并不一定成立.
由于右乘可逆矩阵对应的是对原矩阵作一系列的初等列变换，故可考虑证明A与C的列向量
组等价.
—12一
```

## PDF 第 10 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2013%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=10) · 本机 OCR

```text
解我们证明C的列向量组与A的列向量组能相互线性表示.
不妨设A=（aj，Q，⋯，Q，），C=（Y，Y2，⋯，Y），B=（b；）mxn，则
AB=（a，Q，
，Q。）（bi）nxn
= C=（Y,Y，⋯，Yn），
Y=buae+ oa1d +：+bn1en，
Y2=0120%+02202+-•+0n20n，
因此，C的列向量组（Y， ，⋯，Y.）能由A的列向量组（a,Q2，
…，Q.）线性表示.同理，由于B
可逆，故A的列向量组也能由C的列向量组线性表示.应选B.
下面我们说明选项A、C、D 不正确.
选项A：令A =
B=
则C= AB=
（1
2
0
但A的行向量组！（1,1），（0,0）｝
与C的行向量组！（1,2），（0,0）｝不等价.
选项C、D：取B为单位矩阵E，C为一个非满秩矩阵.B的行（列）向量组线性无关，C的行（列）
分析）
本题主要考查矩阵相似的条件.
3 阶矩阵A的特征值为1，-1，0意味着A有3个不同的特征值，从而相似于与它具有相同特征
值的对角矩阵，即A.
（解3阶矩阵A的特征值为1，-1,0意味着A 有3个不同的特征值，从而A相似于与它具有
相同特征值的对角矩阵，即A. 于是，A的特征值为1，-1，0的充分必要条件即A与A相似的充分
必要条件.
选项B实际上为A与A相似的定义，即存在可逆矩阵P，使得A= P~'AP，也即A=PAP-
此，应选B.
下面说明选项A、C、D 不正确.
选项A是A与A等价的定义.若两矩阵相似，则它们必等价，但两个等价的矩阵不一定相似，例
0
0
2
0
0
故选项A是A与A相似的必要不充分条件.
因为正交矩阵也是可逆矩阵，所以选项C是A与A相似的充分条件.但选项C并不是A与A相
似的必要条件，因A 不一定能找到一组相互正交的特征向量，这一要求对实对称矩阵成立，对一
般矩阵不成立.
取专，
=
则专，52，5相互均不正交.令P=（券，52,5），A=
一12一
```

## PDF 第 10 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2022%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=10) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
0
0
0
-1
1］
A = PAP- =
0
1
0
-1
1
由于闭区域上的二元连续函数的最值可能在区域内部取得，也可能在边界上取得，故我
们一般可按照以下步骤求解.
① 求出区域内部所有的驻，点和偏导数不存在的点（注意这里不需要判断驻点是否为极值点）.
② 求出函数在边界上可能的最值点，该问题可转化为条件极值问题。
③ 比较①，② 中的所有点的函数值，最大者即为最大值，最小者即为最小值、
对实际应用问题，先根据题意确定目标函数和定义域，将实际问题转化为最值问题，
若由题意可知目标函数的最大值或最小值存在，且在区域内部取得，而目标函数在区域
内部仅有一个驻点，则该驻点即为目标函数的最大值点或最小值点，该驻，点处的函数值即为
所求最大值或最小值
0
0
行列式
（
0
）
C
0
0
d
（A） （ad-bc）？
（B）- （ad - bc）2.
（C）a?d -B2c？
（D）B2C- ad.
答案
B.
分析本题主要考查行列式的计算.
求本题中的行列式，较快的解法是利用初等变换将原行列式与分块矩阵的行列式建立联系后
进行计算.
若短降 能写成分块上三角矩阵的形式 =（合
36:\newenvironment{abcd}{\begin{enumerate}[label=\textup{(\Alph*)},leftmargin=2.3em,itemsep=1pt,topsep=4pt,parsep=1pt]}{\end{enumerate}}
37:\newcommand{\choices}[4]{%


## tool · 2026-11-10T09:56:39Z




## tool · 2026-11-10T09:58:06Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T09:58:10Z


Script completed
Wall time 0.1 seconds
Output:

\choices{\(\boldsymbol A^*\) 为置换矩阵}{\(\boldsymbol A^{-1}\) 为置换矩阵}{\(\boldsymbol A^{-1}=\boldsymbol A^*\)}{\(\boldsymbol A^{-1}=-\boldsymbol A^*\)}
\QuestionEnd

% Q 2026 9
\QuestionPage{A.4 线性代数}{选择题}{2026 年第 9 题}{2}{矩阵方程的可解性}{359 / 408}
设矩阵
\[\boldsymbol A=
\begin{pmatrix}
1&0&1\\
0&0&1\\
1&1&3\\
1&1&1
\end{pmatrix},
\qquad
\boldsymbol C=
\begin{pmatrix}
2&0\\
1&1\\
1&1\\
a&b
\end{pmatrix}.
\]
若存在矩阵 \(\boldsymbol B\) 满足 \(\boldsymbol A\boldsymbol B=\boldsymbol C\)，则
\choices{\(a=-1,\ b=-1\)}{\(a=2,\ b=2\)}{\(a=-1,\ b=2\)}{\(a=2,\ b=-1\)}
\QuestionEnd

% Q 2026 10
\QuestionPage{A.4 线性代数}{选择题}{2026 年第 10 题}{2}{矩阵恒等式与秩}{360 / 408}
设三阶矩阵 \(\boldsymbol A,\boldsymbol B\) 满足
\[\boldsymbol A\boldsymbol B+\boldsymbol B\boldsymbol A=\boldsymbol A^2+\boldsymbol B^2,
\]
且 \(\boldsymbol A\ne \boldsymbol B\)，则下列结论错误的是
\choices{\((\boldsymbol A-\boldsymbol B)^3=\boldsymbol O\)}{\(\boldsymbol A-\boldsymbol B\) 只有零特征值}{\(\boldsymbol A,\boldsymbol B\) 不能都是对角矩阵}{\(\boldsymbol A-\boldsymbol B\) 只有一个线性无关的特征向量}
\QuestionEnd

% Q 2009 14
\QuestionPage{A.4 线性代数}{填空题}{2009 年第 14 题}{2}{相似矩阵与秩}{361 / 408}
设$\alpha ,\beta$为3维列向量，$\beta^{T}$为$\beta$的转置，
若矩阵$\alpha \beta^{T}$相似于$\begin{pmatrix}
  2 & 0 & 0 \\
  0 & 0 & 0 \\
  0 & 0 & 0
\end{pmatrix}$，则$\beta^{T}\alpha =$ \blank{}．
\QuestionEnd

% Q 2010 14
\QuestionPage{A.4 线性代数}{填空题}{2010 年第 14 题}{2}{行列式的性质}{362 / 408}
设$A,B$为$3$阶矩阵，且$|A| = 3$，$|B| = 2$，$\left| A^{-1} + B \right| = 2$，
则$\left| A + B^{-1} \right|$= \blank{}．
\QuestionEnd

% Q 2011 14
\QuestionPage{A.4 线性代数}{填空题}{2011 年第 14 题}{2}{二次型的正惯性指数}{363 / 408}
二次型$f(x_1,x_2,x_3) = x_{1}^{2} + 3x_2^2 + x_3^2 + 2x_1x_2 + 2x_1x_3 + 2x_2x_3$，
则$f$的正惯性指数为 \blank{}．
\QuestionEnd

% Q 2012 14
\QuestionPage{A.4 线性代数}{填空题}{2012 年第 14 题}{2}{伴随矩阵的行列式}{364 / 408}
设$A$为3阶矩阵，$|A| = 3$，$A^*$为$A$的伴随矩阵，
若交换$A$的第一行与第二行得到矩阵$B$，则$\left| BA^* \right| =$ \blank{}．
\QuestionEnd

% Q 2013 14
\QuestionPage{A.4 线性代数}{填空题}{2013 年第 14 题}{2}{代数余子式与行列式}{365 / 408}
设$A = (a_{ij})$是三阶非零矩阵，$|A|$为$A$的行列式，$A_{ij}$为$a_{ij}$的代数余子式，
若$a_{ij} + A_{ij} = 0$（$i,j = 1,2,3$），则$|A| =$ \blank{}．
\QuestionEnd

% Q 2014 14
\QuestionPage{A.4 线性代数}{填空题}{2014 年第 14 题}{2}{二次型的负惯性指数}{366 / 408}
设二次型$f(x_1,x_2,x_3) = x_1^2 - x_2^2 + 2ax_1x_3 + 4x_2x_3$的负惯性指数是$1$，
则$a$的取值范围 \blank{}．
\QuestionEnd

% Q 2015 14
\QuestionPage{A.4 线性代数}{填空题}{2015 年第 14 题}{2}{矩阵多项式与特征值}{367 / 408}
若$3$阶矩阵$A$的特征值为$2, - 2,1$，$B = A^2 - A + E$，
其中$E$为$3$阶单位阵，则行列式$|B| =$ \blank{}．
\QuestionEnd

% Q 2016 14
\QuestionPage{A.4 线性代数}{填空题}{2016 年第 14 题}{2}{等价矩阵与矩阵秩}{368 / 408}
设矩阵$\begin{pmatrix}
   a & -1 & -1 \\
  -1 &  a & -1 \\
  -1 & -1 & a
\end{pmatrix}$与$\begin{pmatrix}
  1 &  1 & 0 \\
  0 & -1 & 1 \\
  1 &  0 & 1
\end{pmatrix}$等价，则$a =$ \blank{}．
\QuestionEnd

% Q 2017 14
\QuestionPage{A.4 线性代数}{填空题}{2017 年第 14 题}{2}{特征向量与参数}{369 / 408}
设矩阵$A = \begin{pmatrix}
  4 & 1 & -2 \\
  1 & 2 & a \\
  3 & 1 & -1
\end{pmatrix}$的一个特征向量为$\begin{pmatrix}
  1 \\
  1 \\
  2
\end{pmatrix}$，则$a =$ \blank{}．
\QuestionEnd

% Q 2018 14
\QuestionPage{A.4 线性代数}{填空题}{2018 年第 14 题}{2}{矩阵的特征值}{370 / 408}
设$A$为$3$阶矩阵，$\alpha_1,\alpha_2,\alpha_3$为线性无关的向量组，
若$A\alpha_1 = 2\alpha_1 + \alpha_2 + \alpha_3$，
$A\alpha_2 = \alpha_2 + 2\alpha_3$，$A\alpha_3 = - \alpha_2 + \alpha_3$，
则$A$的实特征值为 \blank{}．
\QuestionEnd

% Q 2019 14
\QuestionPage{A.4 线性代数}{填空题}{2019 年第 14 题}{2}{代数余子式}{371 / 408}
已知矩阵$A = \begin{pmatrix}
   1 & -1 &  0 & 0 \\
  -2 &  1 & -1 & 1 \\
   3 & -2 &  2 & -1 \\
   0 &  0 &  3 & 4
\end{pmatrix}$，$A_{ij}$表示$|A|$中元$(i,j)$元的的代数余子式，则$A_{11} - A_{12} =$ \blank{}．
\QuestionEnd

% Q 2020 14
\QuestionPage{A.4 线性代数}{填空题}{2020 年第 14 题}{2}{行列式计算}{372 / 408}
行列式
\[\begin{vmatrix}
a&0&-1&1\\
0&a&1&-1\\
-1&1&a&0\\
1&-1&0&a
\end{vmatrix}
=
\]
\blank{}
\QuestionEnd

% Q 2021 16
\QuestionPage{A.4 线性代数}{填空题}{2021 年第 16 题}{2}{行列式多项式的系数}{373 / 408}
多项式
\[f(x)=\left|\begin{array}{cccc}
x & x & 1 & 2x \\
1 & x & 2 & -1 \\
2 & 1 & x & 1 \\
2 & -1 & 1 & x
\end{array}\right|
\]
中 \(x^3\) 项的系数为 \(\blank{}\)
\QuestionEnd

% Q 2022 16
\QuestionPage{A.4 线性代数}{填空题}{2022 年第 16 题}{2}{初等变换与逆矩阵的迹}{374 / 408}
设 \(\boldsymbol{A}\) 为 \(3\) 阶矩阵，交换 \(\boldsymbol{A}\) 的第 \(2\) 行和第 \(3\) 行，再将第 \(2\) 列的 \(-1\) 倍加到第 \(1\) 列，得到矩阵
\(\left( \begin{array}{ccc} -2 & 1 & -1 \\ 1 & -1 & 0 \\ -1 & 0 & 0 \end{array} \right)\)
则 \(\operatorname{tr}\left( \boldsymbol{A}^{-1} \right) = \blank{}\)
\QuestionEnd

% Q 2023 16
\QuestionPage{A.4 线性代数}{填空题}{2023 年第 16 题}{2}{线性方程组的可解条件}{375 / 408}
已知线性方程组
\[\begin{cases}
ax_1+x_3=1,\\
x_1+ax_2+x_3=0,\\
x_1+2x_2+ax_3=0,\\
ax_1+bx_2=2
\end{cases}
\]
有解，其中 \(a,b\) 为常数。若
\[\begin{vmatrix}
a&0&1\\
1&a&1\\
1&2&a
\end{vmatrix}=4,
\]
则
\[\begin{vmatrix}
1&a&1\\
1&2&a\\
a&b&0
\end{vmatrix}
=\blank{}.
\]
\QuestionEnd

% Q 2024 16
\QuestionPage{A.4 线性代数}{填空题}{2024 年第 16 题}{2}{向量组线性相关}{376 / 408}
设向量
\[\boldsymbol\alpha_1=
\begin{pmatrix}
a\\
1\\
-1\\
1
\end{pmatrix},\quad
\boldsymbol\alpha_2=
\begin{pmatrix}
1\\
1\\
b\\
a
\end{pmatrix},\quad
\boldsymbol\alpha_3=
\begin{pmatrix}
1\\
a\\
-1\\
1
\end{pmatrix}.
\]
若 \(\boldsymbol\alpha_1,\boldsymbol\alpha_2,\boldsymbol\alpha_3\) 线性相关，且其中任意两个向量均线性无关，则 \(ab=\) \blank{}
\QuestionEnd

% Q 2025 16
\QuestionPage{A.4 线性代数}{填空题}{2025 年第 16 题}{2}{线性方程组通解}{377 / 408}
设矩阵 \(\boldsymbol{A} = \left( \boldsymbol{\alpha}_{1}, \boldsymbol{\alpha}_{2}, \boldsymbol{\alpha}_{3}, \boldsymbol{\alpha}_{4} \right)\).若 \(\boldsymbol{\alpha}_{1}\)，\(\boldsymbol{\alpha}_{2}\)，\(\boldsymbol{\alpha}_{3}\) 线性无关，且 \(\boldsymbol{\alpha}_{1} + \boldsymbol{\alpha}_{2} = \boldsymbol{\alpha}_{3} + \boldsymbol{\alpha}_{4}\)，则方程组 \(\boldsymbol{A}\boldsymbol{x} = \boldsymbol{\alpha}_{1} + 4\boldsymbol{\alpha}_{4}\) 的通解为 \blank{}.
\QuestionEnd

% Q 2026 16
\QuestionPage{A.4 线性代数}{填空题}{2026 年第 16 题}{2}{矩阵乘积与二次型}{378 / 408}
设矩阵
\[\boldsymbol A=
\begin{pmatrix}
1&b&-1\\
a+2&3&-3a
\end{pmatrix}.
\]
若二次型
\[\boldsymbol x^T(\boldsymbol A\boldsymbol A^T)\boldsymbol x
\]
的规范形为 \(y_1^2\)，则 \(a+b=\) \blank{}.
\QuestionEnd

% Q 2009 22
\QuestionPage{A.4 线性代数}{解答题}{2009 年第 22 题}{4}{特征向量与线性无关}{379 / 408}
% SOLUTION 338 2018 8
% SOLUTION 339 2019 7
% SOLUTION 340 2019 8


## tool · 2026-11-10T09:58:27Z




## assistant · 2026-11-10T09:58:31Z

已写完前 22 道选择题。核对解析时发现，2013 年第 7 题把可逆矩阵写成了 \(C\)，这会让四个选项同时成立。已将这处和另外几处影响判题的转录差异交给主代理。

## tool · 2026-11-10T10:00:58Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-10T10:01:01Z


Script completed
Wall time 0.1 seconds
Output:

\QuestionEnd

% Q 2009 22
\QuestionPage{A.4 线性代数}{解答题}{2009 年第 22 题}{4}{特征向量与线性无关}{379 / 408}
设$A = \begin{pmatrix}
   1 & -1 & -1 \\
  -1 &  1 & 1 \\
   0 & -4 & -2
\end{pmatrix}$,$\xi_1 = \begin{pmatrix}
  -1 \\
  1 \\
  -2
\end{pmatrix}$．
\begin{enumerate}
\item 求满足$A\xi_2 = \xi_1,A^2\xi_3 = \xi_1$的所有向量$\xi_2,\xi_3$；
\item 对(I)中的任意向量$\xi_2,\xi_3$，证明$\xi_1,\xi_2,\xi_3$线性无关．
\end{enumerate}
\QuestionEnd

% Q 2009 23
\QuestionPage{A.4 线性代数}{解答题}{2009 年第 23 题}{4}{二次型的规范形}{380 / 408}
设二次型$f\left(x_1,x_2,x_3 \right) = ax_1^2 + ax_2^2 + (a - 1)x_3^2 + 2x_1x_3 - 2x_2x_3$．
\begin{enumerate}
\item 求二次型$f$的矩阵的所有特征值；
\item 若二次型$f$的规范形为$y_1^2 + y_2^2$，求$a$的值．
\end{enumerate}
\QuestionEnd

% Q 2010 22
\QuestionPage{A.4 线性代数}{解答题}{2010 年第 22 题}{4}{非齐次线性方程组}{381 / 408}
设$A = \begin{pmatrix}
  \lambda & 1           & 1 \\
  0       & \lambda - 1 & 0 \\
  1       & 1           & \lambda
\end{pmatrix}$, $b = \begin{pmatrix}
  a \\
  1 \\
  1
\end{pmatrix}$，已知线性方程组$Ax = b$存在两个不同的解．\par
\begin{enumerate}
\item 求$\lambda$, $a$；
\item 求方程组$Ax = b$的通解．
\end{enumerate}
\QuestionEnd

% Q 2010 23
\QuestionPage{A.4 线性代数}{解答题}{2010 年第 23 题}{4}{实对称矩阵的正交对角化}{382 / 408}
设$A = \begin{pmatrix}
   0 & -1 & 4 \\
  -1 &  3 & a \\
   4 &  a & 0
\end{pmatrix}$，正交矩阵$Q$使得$Q^T AQ$为对角矩阵，
若$Q$的第$1$列为$\frac{1}{\sqrt{6}}(1,2,1)^T$，求$a$, $Q$．
\QuestionEnd

% Q 2011 22
\QuestionPage{A.4 线性代数}{解答题}{2011 年第 22 题}{4}{向量组的线性表示}{383 / 408}
设向量组$\alpha_1 = (1,0,1)^T$, $\alpha_2 = (0,1,1)^T$, $\alpha_3 = (1,3,5)^T$
不能由向量组$\beta_1 = (1,1,1)^T$, $\beta_2 = (1,2,3)^T$, $\beta_3 = (3,4,a)^T$线性表示．\par
\begin{enumerate}
\item 求$a$的值；
\item 将$\beta_1,\beta_2,\beta_3$用$\alpha_1,\alpha_2,\alpha_3$线性表示．
\end{enumerate}
\QuestionEnd

% Q 2011 23
\QuestionPage{A.4 线性代数}{解答题}{2011 年第 23 题}{4}{实对称矩阵的特征值}{384 / 408}
$A$为三阶实对称矩阵，$A$的秩$r(A) = 2$，且$A\begin{pmatrix}
   1 & 1 \\
   0 & 0 \\
  -1 & 1
\end{pmatrix} = \begin{pmatrix}
  -1 & 1 \\
   0 & 0 \\
   1 & 1
\end{pmatrix}$．\par
\begin{enumerate}
\item 求$A$的特征值与特征向量；
\item 求矩阵$A$．
\end{enumerate}
\QuestionEnd

% Q 2012 22
\QuestionPage{A.4 线性代数}{解答题}{2012 年第 22 题}{4}{行列式与线性方程组}{385 / 408}
设$A = \begin{pmatrix}
  1 & a & 0 & 0 \\
  0 & 1 & a & 0 \\
  0 & 0 & 1 & a \\
  a & 0 & 0 & 1
\end{pmatrix}$，$b = \begin{pmatrix}
  1 \\
  -1 \\
  0 \\
  0
\end{pmatrix}$．
\begin{enumerate}
\item 计算行列式$|A|$．
\item 当实数$a$为何值时，方程组$Ax = b$有无穷多解，并求其通解．
\end{enumerate}
\QuestionEnd

% Q 2012 23
\QuestionPage{A.4 线性代数}{解答题}{2012 年第 23 题}{4}{二次型的秩与正交变换}{386 / 408}
设$A = \begin{pmatrix}
   1 & 0 & 1 \\
   0 & 1 & 1 \\
  -1 & 0 & a \\
   0 & a & -1
\end{pmatrix}$，二次型$f(x_1,x_2,x_3) = x^T A^T Ax$的秩为$2$．\par
\begin{enumerate}
\item 求实数$a$的值；\item 求正交变换$x = Qy$将二次型$f$化为标准型．
\end{enumerate}
\QuestionEnd

% Q 2013 22
\QuestionPage{A.4 线性代数}{解答题}{2013 年第 22 题}{4}{矩阵方程}{387 / 408}
设$A = \begin{pmatrix}
  1 & a \\
  1 & 0
\end{pmatrix},B = \begin{pmatrix}
  0 & 1 \\
  1 & b
\end{pmatrix}$，当$a,b$为何值时，存在矩阵$C$使得$AC - CA = B$，并求所有矩阵$C$．
\QuestionEnd

% Q 2013 23
\QuestionPage{A.4 线性代数}{解答题}{2013 年第 23 题}{4}{二次型矩阵与标准形}{388 / 408}
设二次型$f(x_1,x_2,x_3) = 2(a_1x_1 + a_2x_2 + a_3x_3)^2 + (b_1x_1 + b_2x_2 + b_3x_3)^2$，记
\[
\alpha = \begin{pmatrix}
  a_1 \\
  a_2 \\
  a_3
\end{pmatrix},\quad\beta = \begin{pmatrix}
  b_1 \\
  b_2 \\
  b_3
\end{pmatrix}.
\]
\begin{enumerate}
\item 证明二次型$f$对应的矩阵为$2\alpha^T\alpha + \beta^T\beta$；
\item 若$\alpha ,\beta$正交且均为单位向量，证明二次型$f$在正交变换下的标准形为二次型$2y_1^2 + y_2^2$．
\end{enumerate}
\QuestionEnd

% Q 2014 22
\QuestionPage{A.4 线性代数}{解答题}{2014 年第 22 题}{4}{基础解系与矩阵方程}{389 / 408}
设矩阵$A = \begin{pmatrix}
  1 & -2 &  3 & -4 \\
  0 &  1 & -1 & 1 \\
  1 &  2 &  0 & 3
\end{pmatrix}$，$E$为$3$阶单位矩阵．\par
\begin{enumerate}
\item 求方程组$Ax = 0$的一个基础解系；
\item 求满足$AB = E$的所有矩阵$B$．
\end{enumerate}
\QuestionEnd

% Q 2014 23
\QuestionPage{A.4 线性代数}{解答题}{2014 年第 23 题}{4}{矩阵相似的证明}{390 / 408}
证明$n$阶矩阵$\begin{pmatrix}
       1 &      1 & \cdots & 1 \\
       1 &      1 & \cdots & 1 \\
  \vdots & \vdots & \vdots & \vdots \\
       1 &      1 & \cdots & 1
\end{pmatrix}$与$\begin{pmatrix}
       0 & \cdots &      0 & 1 \\
       0 & \cdots &      0 & 2 \\
  \vdots & \vdots & \vdots & \vdots \\
       0 & \cdots &      0 & n
\end{pmatrix}$相似．
\QuestionEnd

% Q 2015 22
\QuestionPage{A.4 线性代数}{解答题}{2015 年第 22 题}{4}{矩阵方程与矩阵幂}{391 / 408}
设矩阵$A = \begin{pmatrix}
  a & 1 & 0 \\
  1 & a & -1 \\
  0 & 1 & a
\end{pmatrix}$且$A^3 = O$．
\begin{enumerate}
\item 求$a$的值；
\item 若矩阵$X$满足$X - XA^2 - AX + AX A^2 = E$，$E$为$3$阶单位阵，求$X$．
\end{enumerate}
\QuestionEnd

% Q 2015 23
\QuestionPage{A.4 线性代数}{解答题}{2015 年第 23 题}{4}{相似矩阵与对角化}{392 / 408}
设矩阵$A = \begin{pmatrix}
   0 &  2 & -3 \\
  -1 &  3 & -3 \\
   1 & -2 & a
\end{pmatrix}$相似于矩阵$B = \begin{pmatrix}
  1 & -2 & 0 \\
  0 &  b & 0 \\
  0 &  3 & 1
\end{pmatrix}$．\par
\begin{enumerate}
\item 求$a,b$的值；
\item 求可逆矩阵$P$，使$P^{-1} AP$为对角矩阵．
\end{enumerate}
\QuestionEnd

% Q 2016 22
\QuestionPage{A.4 线性代数}{解答题}{2016 年第 22 题}{4}{线性方程组与通解}{393 / 408}
设矩阵$A = \begin{pmatrix}
      1 & 1 & 1 - a \\
      1 & 0 & a \\
  a + 1 & 1 & a + 1
\end{pmatrix}$，$\beta = \begin{pmatrix}
  0 \\
  1 \\
  2a - 2
\end{pmatrix}$，且方程组$Ax = \beta$无解．\par
\begin{enumerate}
\item 求$a$的值；
\item 求方程组$A^T Ax = A^T\beta$的通解．
\end{enumerate}
\QuestionEnd

% Q 2016 23
\QuestionPage{A.4 线性代数}{解答题}{2016 年第 23 题}{4}{矩阵方程与列向量表示}{394 / 408}
已知矩阵$A = \begin{pmatrix}
  0 & -1 & 1 \\
  2 & -3 & 0 \\
  0 &  0 & 0
\end{pmatrix}$．
\begin{enumerate}
\item 求$A^{99}$；
\item 设$3$阶矩阵$B = (\alpha ,\alpha_2,\alpha_3)$满足$B^2 = BA$，
      记$B^{100} = (\beta_1,\beta_2,\beta_3)$，
      将$\beta_1,\beta_2,\beta_3$分别表示为$\alpha_1,\alpha_2,\alpha_3$的线性组合．
\end{enumerate}
\QuestionEnd

% Q 2017 22
\QuestionPage{A.4 线性代数}{解答题}{2017 年第 22 题}{4}{矩阵秩与方程组通解}{395 / 408}
设$3$阶矩阵$A= (\alpha_1,\alpha_2,\alpha_3)$有$3$个不同的特征值，
且$\alpha_3=\alpha_1\text{+}2\alpha_2$．\par


## tool · 2026-11-10T10:01:05Z


Script completed
Wall time 0.1 seconds
Output:

\QuestionEnd

% Q 2017 22
\QuestionPage{A.4 线性代数}{解答题}{2017 年第 22 题}{4}{矩阵秩与方程组通解}{395 / 408}
设$3$阶矩阵$A= (\alpha_1,\alpha_2,\alpha_3)$有$3$个不同的特征值，
且$\alpha_3=\alpha_1\text{+}2\alpha_2$．\par
\begin{enumerate}
\item 证明：$r(A) = 2$；
\item 若$\beta =\alpha_1\text{+}\alpha_2\text{+}\alpha_3$，求方程组$Ax = \beta$的通解．
\end{enumerate}
\QuestionEnd

% Q 2017 23
\QuestionPage{A.4 线性代数}{解答题}{2017 年第 23 题}{4}{二次型正交化}{396 / 408}
设二次型$f(x_1,x_2,x_3) = 2x_1^2 - x_2^2 + ax_3^2 + 2x_1x_2 - 8x_1x_3 + 2x_2x_3$
在正交变换$x = Qy$下的标准型为$\lambda_1 y_1^2 + \lambda_2 y_2^2$，求$a$的值及一个正交矩阵$Q$．
\QuestionEnd

% Q 2018 22
\QuestionPage{A.4 线性代数}{解答题}{2018 年第 22 题}{4}{二次型规范形}{397 / 408}
设实二次型$f(x_1,x_2,x_3) = (x_1 - x_2 + x_3)^2 + (x_2 + x_3)^2 + (x_1 + ax_3)^2$，其中$a$是参数．\par
\begin{enumerate}
\item 求$f(x_1,x_2,x_3) = 0$的解；
\item 求$f(x_1,x_2,x_3)$的规范形．
\end{enumerate}
\QuestionEnd

% Q 2018 23
\QuestionPage{A.4 线性代数}{解答题}{2018 年第 23 题}{4}{矩阵的初等列变换}{398 / 408}
已知$a$是常数，且矩阵$A = \begin{pmatrix}
  1 & 2 & a \\
  1 & 3 & 0 \\
  2 & 7 & -a
\end{pmatrix}$可经初等列变换化为矩阵$B = \begin{pmatrix}
   1 & a & 2 \\
   0 & 1 & 1 \\
  -1 & 1 & 1
\end{pmatrix}$．\par
\begin{enumerate}
\item 求$a$；
\item 求满足$AP = B$的可逆矩阵$P$．
\end{enumerate}
\QuestionEnd

% Q 2019 22
\QuestionPage{A.4 线性代数}{解答题}{2019 年第 22 题}{4}{等价向量组}{399 / 408}
已知向量组 I ：$\alpha_1 = \begin{pmatrix}
  1 \\
  1 \\
  4
\end{pmatrix}$, $\alpha_2 = \begin{pmatrix}
  1 \\
  0 \\
  4
\end{pmatrix}$, $\alpha_3 = \begin{pmatrix}
  1 \\
  2 \\
  a^2 + 3
\end{pmatrix}$；
向量组 II ：$\beta_1 = \begin{pmatrix}
  1 \\
  1 \\
  a + 3
\end{pmatrix}$, $\beta_2 = \begin{pmatrix}
  0 \\
  2 \\
  1 - a
\end{pmatrix}$, $\beta_3 = \begin{pmatrix}
  1 \\
  3 \\
  a^2 + 3
\end{pmatrix}$．若向量组 I 和向量组 II 等价，求常数$a$的值，
并将$\beta_3$用$\alpha_1,\alpha_2,\alpha_3$线性表示．
\QuestionEnd

% Q 2019 23
\QuestionPage{A.4 线性代数}{解答题}{2019 年第 23 题}{4}{矩阵相似与相似变换}{400 / 408}
已知矩阵$A = \begin{pmatrix}
  -2 & 2 & 1 \\
   2 & x & -2 \\
   0 & 0 & -2
\end{pmatrix}$与$B = \begin{pmatrix}
  2 &  1 & 0 \\
  0 & -1 & 0 \\
  0 &  0 & y
\end{pmatrix}$相似．\par
\begin{enumerate}
\item 求$x,y$之值；
\item 求可逆矩阵$P$，使得$P^{-1} AP = B$．
\end{enumerate}
\QuestionEnd

% Q 2020 22
\QuestionPage{A.4 线性代数}{解答题}{2020 年第 22 题}{4}{二次型的合同变换}{401 / 408}
设二次型
\[f(x_1,x_2,x_3)=x_1^2+x_2^2+x_3^2+2ax_1x_2+2ax_1x_3+2ax_2x_3
\]
经过可逆线性变换
\[\begin{pmatrix}
x_1\\
x_2\\
x_3
\end{pmatrix}
=
\boldsymbol{P}
\begin{pmatrix}
y_1\\
y_2\\
y_3
\end{pmatrix}
\]
化为二次型
\[g(y_1,y_2,y_3)=y_1^2+y_2^2+4y_3^2+2y_1y_2.
\]
\begin{enumerate}
\item 求 \(a\) 的值；
\item 求可逆矩阵 \(\boldsymbol{P}\)。
\end{enumerate}
\QuestionEnd

% Q 2020 23
\QuestionPage{A.4 线性代数}{解答题}{2020 年第 23 题}{4}{相似对角化的判断}{402 / 408}
设 \(\boldsymbol{A}\) 为 2 阶矩阵，\(\boldsymbol{P}=(\boldsymbol{\alpha},\boldsymbol{A}\boldsymbol{\alpha})\)，其中 \(\boldsymbol{\alpha}\) 是非零向量且不是 \(\boldsymbol{A}\) 的特征向量。
\begin{enumerate}
\item 证明 \(\boldsymbol{P}\) 为可逆矩阵；
\item 若 \(\boldsymbol{A}^2\boldsymbol{\alpha}+\boldsymbol{A}\boldsymbol{\alpha}-6\boldsymbol{\alpha}=0\)，求 \(\boldsymbol{P}^{-1}\boldsymbol{A}\boldsymbol{P}\)，并判断 \(\boldsymbol{A}\) 是否相似于对角矩阵。
\end{enumerate}
\QuestionEnd

% Q 2021 22
\QuestionPage{A.4 线性代数}{解答题}{2021 年第 22 题}{4}{矩阵的相似对角化}{403 / 408}
设矩阵
\[\boldsymbol{A}=\begin{pmatrix}
2 & 1 & 0 \\
1 & 2 & 0 \\
1 & a & b
\end{pmatrix}
\]
仅有两个不同的特征值。若 \(\boldsymbol{A}\) 相似于对角矩阵，求 \(a,\ b\) 的值，并求可逆矩阵 \(\boldsymbol{P}\)，使 \(\boldsymbol{P}^{-1}\boldsymbol{A}\boldsymbol{P}\) 为对角矩阵。
\QuestionEnd

% Q 2022 22
\QuestionPage{A.4 线性代数}{解答题}{2022 年第 22 题}{4}{二次型的正交变换}{404 / 408}
已知二次型
\(f\left( x_{1},x_{2},x_{3} \right) = 3x_{1}^{2} + 4x_{2}^{2} + 3x_{3}^{2} + 2x_{1}x_{3}\)
（I） 求正交矩阵 \(\boldsymbol{Q}\)，使正交变换 \(\boldsymbol{x} = \boldsymbol{Q}\boldsymbol{y}\) 将二次型 \(f\left( x_{1},x_{2},x_{3} \right)\) 化为标准形；
（II） 证明
\(\min_{\boldsymbol{x} \ne \boldsymbol{0}} \frac{f\left( \boldsymbol{x} \right)}{\boldsymbol{x}^{T}\boldsymbol{x}} = 2\)
\QuestionEnd

% Q 2023 22
\QuestionPage{A.4 线性代数}{解答题}{2023 年第 22 题}{4}{线性变换的相似对角化}{405 / 408}
设矩阵 \(\boldsymbol A\) 满足：对任意 \(x_1,x_2,x_3\)，均有
\[\boldsymbol A
\begin{pmatrix}
x_1\\
x_2\\
x_3
\end{pmatrix}
=
\begin{pmatrix}
x_1+x_2+x_3\\
2x_1-x_2+x_3\\
x_2-x_3
\end{pmatrix}.
\]
\begin{enumerate}
\item 求 \(\boldsymbol A\)；
\item 求可逆矩阵 \(\boldsymbol P\) 与对角矩阵 \(\boldsymbol\Lambda\)，使得
\[\boldsymbol P^{-1}\boldsymbol A\boldsymbol P=\boldsymbol\Lambda.
\]
\end{enumerate}
\QuestionEnd

% Q 2024 22
\QuestionPage{A.4 线性代数}{解答题}{2024 年第 22 题}{3}{方程组同解与正交对角化}{406 / 408}
设矩阵
\[\boldsymbol A=
\begin{pmatrix}
0&1&a\\
1&0&1
\end{pmatrix},\qquad
\boldsymbol B=
\begin{pmatrix}
1&1\\
1&1\\
b&2
\end{pmatrix},
\]
二次型
\[f(x_1,x_2,x_3)=\boldsymbol x^T\boldsymbol B\boldsymbol A\boldsymbol x.
\]
已知方程组 \(\boldsymbol A\boldsymbol x=0\) 的解是 \(\boldsymbol B^T\boldsymbol x=0\) 的解，但两个方程组不同解。
\begin{enumerate}
\item 求 \(a,b\) 的值；
\item 求正交变换 \(\boldsymbol x=\boldsymbol Q\boldsymbol y\)，将 \(f(x_1,x_2,x_3)\) 化为标准形。
\end{enumerate}
\QuestionEnd

% Q 2025 22
\QuestionPage{A.4 线性代数}{解答题}{2025 年第 22 题}{3}{矩阵合同与正交对角化}{407 / 408}
（本题满分 12 分）
已知矩阵
\(\boldsymbol{A} = \begin{pmatrix} 4 & 1 & -2 \\ 1 & 1 & 1 \\ -2 & 1 & a \end{pmatrix}\)，
\(\boldsymbol{B} = \begin{pmatrix} k & 0 & 0 \\ 0 & 6 & 0 \\ 0 & 0 & 0 \end{pmatrix}\)
合同.
\begin{enumerate}
\item 求 \(a\) 的值及 \(k\) 的取值范围；
\item 若存在正交矩阵 \(\boldsymbol{Q}\)，使得 \(\boldsymbol{Q}^{\mathrm{T}} \boldsymbol{A} \boldsymbol{Q} = \boldsymbol{B}\)，求 \(k\) 及 \(\boldsymbol{Q}\).
\end{enumerate}
\QuestionEnd

% Q 2026 22
\QuestionPage{A.4 线性代数}{解答题}{2026 年第 22 题}{3}{极大线性无关组与矩阵幂}{408 / 408}
（本题满分 12 分）
已知向量组
\[\boldsymbol{\alpha}_1=
\begin{pmatrix}
1\\
0\\
-1\\
-1
\end{pmatrix},
\qquad
\boldsymbol{\alpha}_2=
\begin{pmatrix}
1\\
-1\\
0\\
-2
\end{pmatrix},
\qquad
\boldsymbol{\alpha}_3=
\begin{pmatrix}
0\\
-1\\
1\\
-1
\end{pmatrix},
\qquad
\boldsymbol{\alpha}_4=
\begin{pmatrix}
0\\
1\\
-1\\
1
/usr/bin/python3
Traceback (most recent call last):
  File "<string>", line 1, in <module>
ModuleNotFoundError: No module named 'sympy'


## tool · 2026-11-10T10:01:11Z


Script completed
Wall time 0.1 seconds
Output:

\qquad
\boldsymbol{\alpha}_4=
\begin{pmatrix}
0\\
1\\
-1\\
1
\end{pmatrix}.
\]
记
\[\boldsymbol A=(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_4),\qquad
\boldsymbol G=(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2).
\]
\begin{enumerate}
\item 证明：\(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2\) 是 \(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_4\) 的极大线性无关组；
\item 求矩阵 \(\boldsymbol H\) 使得 \(\boldsymbol A=\boldsymbol G\boldsymbol H\)，并求 \(\boldsymbol A^{10}\).
\end{enumerate}
\QuestionEnd

\end{document}
.
..
solutions
/opt/homebrew/bin/uv
346-因此A+AT和B +B「不相似.
347:注 若A，B均为实对称矩阵，且A与B相似，则A+A'和B+B「相似、
348-下面简单证明一下该结论.
349:若A，B均为实对称矩阵，则A+AT =2A，B+B'=2B. 由A与B相似能推出24与
350-2B 相似，即A+A'和B+B"相似.
--
581-a
582:14 设矩阵
583-1
--
613-矩阵等价 若矩阵A经过有限次初等变换能变成矩阵B，则矩阵A与矩阵B等价，记作A~B.
614:设A,B均为m xn矩阵，则A~B的充分必要条件是存在m阶可逆矩阵P以及n阶可逆矩阵
615-Q， 使得PAQ =B.
--
1311-22
1312:设矩阵A =
1313-1
--
1433-•
1434:（II）设3阶矩阵B=（a，4，as）满足B’= BA. 记B'W0=（B」，B2,Bs），将B」，B2，B，分别
1435-表示为aj,Q,Qs的线性组合.


## tool · 2026-11-10T10:02:18Z




## assistant · 2026-11-10T10:02:21Z

42 道选择题和 18 道填空题已写完。正在写解答题的完整步骤，其中两处转录问题分别涉及二次型矩阵的乘法次序和矩阵列向量的下标。

## tool · 2026-11-10T10:02:24Z


Script completed
Wall time 0.1 seconds
Output:

\textbf{解析}\quad $\alpha_1+\alpha_2-\alpha_3-\alpha_4=0$ 给出齐次解 $(1,1,-1,-1)^T$。前三列无关，第四列又在其张成空间内，故 $r(A)=3$，这个非零齐次解张成整个零空间。右端的列系数给出特解 $(1,0,0,4)^T$。因此通解为
\[
x=(1,0,0,4)^T+t(1,1,-1,-1)^T,\qquad t\in\mathbb R.
\]

% SOLUTION 378 2026 16
\textbf{入手角度}\quad 用规范形的秩判断 $A$ 的两行是否成比例。

\textbf{解析}\quad 规范形 $y_1^2$ 表明 $AA^T$ 的秩为 $1$。因为 $x^TAA^Tx=\lVert A^Tx\rVert^2$，所以 $\ker(AA^T)=\ker A^T$，进而 $r(A)=r(AA^T)=1$。$A$ 的第一行非零，因此第二行是第一行的 $k$ 倍。比较首、末分量得 $k=a+2=3a$，即 $a=1$、$k=3$。中间分量给出 $3=3b$，故 $b=1$，填 $\boxed{2}$。
1505-B=
1506-ag
1507-0s
1508:（I）证明二次型f对应的矩阵为2cc' +BB"；
1509-（II） 若a，B正交且均为单位向量，证明 在正交变换下的标准形为2%+32
1510-分析本题主要考查对二次型的概念的理解.
1511-一个二次型对应着一个对称矩阵.若对称矩阵A 满足f= “Ax，则称A为二次型f对应的矩阵.
1512-二次型f在正交变换下的标准形的各项系数为A 的特征值.
1513-证（I）记x=（21，22，23）「
1514:，f对应的矩阵为A，A为对称矩阵，则
1515-Q12， + a2X2 + asXs = x'a = a'x，
1516-61&1+6,22 + 6383 = XB=B'x.
1517-f（x ,42，&s）=2（x'a）（a'x） + （x"B）（B'x）=x'（2ccc「 +BB「）x.


## tool · 2026-11-10T10:04:12Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:04:27Z


Script completed
Wall time 0.1 seconds
Output:

=\begin{pmatrix}
2d-2&1-2d&2-d\\
4d-2&1-4d&2-2d\\
0&0&0
\end{pmatrix}.
\]

（II）由 $B^2=BA$，若 $B^k=BA^{k-1}$，则 $B^{k+1}=B^2A^{k-1}=BA^k$。归纳得 $B^{100}=BA^{99}$。逐列读取 $A^{99}$ 的系数即得
\[
\begin{aligned}
\beta_1&=(2d-2)\alpha_1+(4d-2)\alpha_2,\\
\beta_2&=(1-2d)\alpha_1+(1-4d)\alpha_2,\\
\beta_3&=(2-d)\alpha_1+(2-2d)\alpha_2.
\end{aligned}
\]
      76


## tool · 2026-11-10T10:06:13Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:06:33Z


Script completed
Wall time 0.1 seconds
Output:

{"status":"fulfilled","value":{"chunk_id":"7159d3","wall_time_seconds":0.000007625,"exit_code":1,"original_token_count":23,"output":"Traceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nAssertionError\n"}}
{"status":"fulfilled","value":{"chunk_id":"f24737","wall_time_seconds":0.000007541,"exit_code":0,"original_token_count":1089,"output":"337-设A是4阶矩阵，A’是A的伴随矩阵，若线性方程组Ax = 0 的基础解系中只有2个向\n338-量，则r（A*）=（）\n339-（A）0.\n340-答案\n--\n351-1,r（A）= -1，\n352-0,r（A）<n-1.\n353-解 由于Ax = 0的基础解系中只含有2个向量，故r（A）=4-2=2. 又因为r（A）=2<\n354-4-1，所以r（A*）=0.\n355:因此，应选 A.\n356-•拓展\n357-我们先简单说明一下分析中的关于伴随矩阵的秩的结论.\n358-•当r（A）=n时，AA'= |A|E,A”可逆，所以r（A'）=几\n359-•当 （A）=n-1时，A至少有一个n-1阶子式不为零，所以r（A'）≥1.又因为AA'=0，\n--\n368-（C） 含有两个线性无关的解向量.\n369-（D） 含有三个线性无关的解向量.\n370-答案 B.\n371-解由Ax =6有4个不同的解可知Ax =0有非零解.于是r（A）≤n-1. 又因为A’*O，\n372:所以r（A）≥n-1.因此，r（A）=n-1，Ax=0的基础解系仅含一个非零解向量.应选B.\n373-设A是3阶实对称矩阵，E是3阶单位矩阵。若A’+A =2B，且|A| =4，则二次型x\"Ax\n374-的规范形为（\n375-）\n376-（A）行+½+3.\n--\n395-解设A为A的一个特征值，a 为属于特征值入 的特征向量.\n396-由A’+A = 2E可得（A2+入-2）a =0. 由于a为非零向量，故A+入-2=0. 解得入=1或\n397-A =-2. A 的特征值只能取1和-2.\n398-又因为|A|=4，所以A的特征值应为-2，-2，1.因此，二次型x“Ax的正惯性指数为1，负\n399:惯性指数为2.四个选项中，只有子一经一多满足该性质.应选C.\n400-二、填空题\n401-9\n402-lim （x+23）号\n403-=\n--\n1035-y\n1036-（分析）；\n1037-本题主要考查二重积分的计算.\n1038-通过观察可知，本题中的区域D关于y轴对称，故可以利用对称性将 ）=-入\n1039:所求二重积分化简.根据被积函数的特点，应选择在极坐标系下计算二重\n1040-积分.\n1041-成.由区域D的表达式可知，区域D关于y轴对称.记D，为D位于y轴右方的区域\n1042-由于f（x,y）=x为关于x的奇函数，g（x,y）= 关于x的偶函数，故由对称性可得，\n1043-在极坐标系下计算\n--\n1306-a'+3\n1307-1\n1308-3\n1309-与1：B，=\n1310:若向量组1与I等价，求a的取值，并将B，用c，Q，Q，线性表示.\n1311-25-\n1312-0\n1313-2\n1314-```\n--\n1322-线性表示 给定向量组A:0，0，，Q。和向量B.若存在一组数A」，A2，”，Am，使得\n1323-B=A,a+A2Q+：+Amam，\n1324-则向量B是向量组A的线性组合，称向量B能由向量组A线性表示，等价于非齐次线性方程组\n1325-Ax =B有解，其中A是由A构成的矩阵.\n1326:向量组之间的线性表示 设有两个向量组A:Q，Q，“，Q. 和 B:BL,B2，“，B.，若向量组B中\n1327-的每个向量都能由向量组A线性表示，则称向量组 B能由向量组A线性表示，等价于矩阵方程\n1328-AX =B有解，其中A是由A构成的矩阵，B是由B构成的矩阵.\n1329-已知向量组 I与向量组 II等价，记A=（aj,Q2,4），B=（B」，B2,B3），则A，B满足r（A）=\n1330-r（B）=r（A,B）. 利用这一点，可以确定 a.\n--\n1429-特别地，当m =1时，上述条件等价于存在 m 阶可逆矩阵Q，使得\n1430-（B,Bz，，Bw）=（a，0.，0.）2\n1431-向量组之间的表示问题通常可以转化为矩阵方程的求解问题\n1432-3. 下面是两条关于向量组之间的线性表示的常用结论。\n1433:（I）若向量组A线性无关，向量组AU1B|线性相关，则B能由A唯一地线性表示。\n1434:（2）若向量组B能被向量组A线性表示，则向量组B的秩不大于向量组A的秩\n1435-1-2\n1436-23\n1437-已知矩阵A\n1438-=\n201-盐） （0.、\n202-（会点）-103.\n203-选D.\n204:8.单位矩阵经过若干次互换两行得到的矩阵称为置换矩阵.设A为n阶置换矩阵，A A\n205-的伴随矩阵，则\n206:A. A'为置换矩阵.\n207:B.A 为置换矩阵.\n208-数学解析 第6页（共16页）\n209-```\n210-\n--\n279-A.（A-B）=0.\n280-B. A-B只有零特征值.\n281-C. A，B不能都是对角矩阵.\n282:D. A-B只有一个线性无关的特征向量.\n283-10.【答案】D\n284-【解析】\n285-AB+BA=A+B，\n--\n313-\n314-```text\n315-淘宝：谈辰教育工作室\n316:而C有2个线性无关的特征向量，故选 D.\n317-二、填空题：11~16 小题，每小题5分，共30分.\n318-1！设户判游致，若反常配分！”元\n319-dx收敛，则p的取值范围是_\n"}}

## tool · 2026-11-10T10:06:43Z


Script completed
Wall time 0.1 seconds
Output:

90 90 set() set()
[(366, "'\\\\textbf{入手角度}\\\\quad 分别用 $x_3$ 配'", 0, "'-2,2]}$。\\n\\n'")]
53 53 433 433
['pmatrix', 'pmatrix', 'pmatrix', 'pmatrix']


## tool · 2026-11-10T10:06:49Z


Script completed
Wall time 0.1 seconds
Output:

303:% SOLUTION 366 2014 14
304-\textbf{入手角度}\quad 分别用 $x_3$ 配齐含 $x_1$、$x_2$ 的平方。
305-
306-\textbf{解析}\quad
307-\[
308-f=(x_1+ax_3)^2-(x_2-2x_3)^2+(4-a^2)x_3^2.
单调增加，从而f（x）>f（O）=0，即In（1+x）>
In（1 +x）
2'1 +Cos X
2（1 +cos x）
因此，½>1.
此外，同样的方法不难证明在（0,1）内，In（1 +x）<x.
另一方面，由于在（0,1）内，0< sin x,cos x < 1,1 <1.+sin x <2，故1，的被积函数
2x
+ sin x
In（1+x）
>x.结合In（1+x）
<8可得，一+cos x
<x.于是
1 + cosx
''1 + sinx
In（1 +x）
1+ cos x
.因此，
1s > 12：
综上所述，应选 A.
0
8
设A为3阶矩阵，A=
-1
则A的特征值1，-1,0的充分必要条件是（）
0
（A）存在可逆矩阵P，Q，使得A= PAQ.
（B） 存在可逆矩阵P，使得A = PAP-
（C）存在正交矩阵Q，使得A = 040
（D）存在可逆矩阵P，使得A= PAPT
答案B.
分析）
本题主要考查矩阵相似的条件.
3 阶矩阵A的特征值为1，-1，0意味着A有3个不同的特征值，从而相似于与它具有相同特征
值的对角矩阵，即A.
（解3阶矩阵A的特征值为1，-1,0意味着A 有3个不同的特征值，从而A相似于与它具有
相同特征值的对角矩阵，即A. 于是，A的特征值为1，-1，0的充分必要条件即A与A相似的充分
］
0
0
2
a -11-a
1
2
-1
由上式可知r（A）≥2，故r（A）=2或r（A）=3.
符合题意，而当a=1时， （A）= （B）=r（A,B）=2，此时向量组1 与向量组II等价.
当a=1时，
3
-2
0
（r：表示对第i行作初等行变换后所得新的第i行，每作一次初等行变换，加一个*.）
取x，自由变元，令x=1，可得（-2,1,1）「 Ax=0的一个基础解系.又因为（3，-2,0）「
为Ax =B，的一个特解，所以Ax =B，的通解为k（-2,1,1）「+（3， 2,0）「
，其中k为任意常数
因此，
Bs=（3-2k）a+（-2+k）a+hia，
其中 任意常数，
当a 士1时，a-1 0,r（A）=r（B）=r（A,B）=3，向量组1 与向量组II 等价，且它们
相互之间的线性表示唯一.
2
1一
3
-2
-273
0
0
1
-1
「2
1
1
+T3
因此，Ax =B，的唯一解为（1，-1,1）'
Bs=a-0+a.
—26—
```

## PDF 第 24 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2019%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=24) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
综上所述，当a -1时，向量组1与向量组I等价.当a=1时，B=（3-2k）a」 +（-2+ki）ak+
haks，其中k为任意常数；当a 士1时，B=0-Q+as-
含拓展
1. 向量的线性表示
向量B可由向量组a，Q，…，q，线性表示
台存在常数A，h，h，使得h，ax+h,Q+•+hja=B
方程组Ax=B有解，其中A=（aj，Q2，.，Q）
台r（0,Q2，•，a）=r（a,Q2，..
，4,B）.
向量的表示问题通常可以转化为线性方程组的求解问题.
2. 向量组之间的线性表示
（1） 向量组B」.B2，.B.可由向量组Q」，Q，…，Q，线性表示
台存在1xm 矩阵P，使得（B」.B2..B.）=（a，Q，.，Q）P
台矩阵方程（a，0，“，Q）X=（B1,Bz。，Bm）有解，其中X为1xm矩阵
台7（a，0，，9）=r（a，Q.，0,B」，B2.，Bm）.
（2） 向量组B」，B2，”.B， 与向量组a」，0，“，Q等价，即它们可相互线性表示


## tool · 2026-11-10T10:06:58Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:07:01Z




## tool · 2026-11-10T10:07:17Z


Script completed
Wall time 0.1 seconds
Output:

（2）若向量组B能被向量组A线性表示，则向量组B的秩不大于向量组A的秩
1-2
23
已知矩阵A
=
-2 1
X
-2
0
-2
与B=
00
1
0
- 1
0
0
Y
相似.
（I）求x， ；
（II）求可逆矩阵P，使得PAP = B.
分析）本题主要考查相似矩阵的性质以及矩阵的相似对角化、
第（I）问要求x，夕，可利用相似的矩阵具有相同的迹与行列式这一性质.
由于A，B均不是对角矩阵，但易知它们均可相似对角化，故可分别计算它们的特征向量，将它
们相似对角化，再计算P.
解（I）由于A，B相似，故它们的迹与行列式均相同.
由A，B 有相同的迹可得-4+×=1+y，即 =5.
计算|A|，1B.B 为上三角矩阵，故易得|B|=-2y.
```

## PDF 第 25 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2019%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=25) · 本机 OCR

```text
按第三行展开
=（-2）
-2
-2
= 48-8.
2
X
由A=B 可得4x-8=-2y，即2x+Y=4.
联立
解得×=.3， = 2.
28+y=4，
（II）由于A，B 相似，故它们有相同的特征值.
计算B 的特征多项式.
A-2
-1，0
IAE-B =
0
A+1
0
=
（A -2）（A +1）（A+2）.
0
0
A+2
于是，B的特征值为2，-1， 2. 从而A的特征值也为2，-1，-2.
由于A，B具有3个不同的特征值2，-1，-2，故存在可逆矩阵P，P2，使得P'AP，=
2
0
0
乙
0
0
0
-10
.P BP2
=
0
-1
0
\0
0
-2
0
-2
令P=P,P
'，则PAP=PPAPP
'=P（PAP，）P=B.
P，的列向量为A的属于特征值2，-1，-2 的特征向量，P的列向量为B的属于特征值2，-1，
-2 的特征向量.下面分别计算 A，B 的特征向量.
计算A 的属于特征值2的特征向量.考虑（2E -A）x = 0.
4
2
11
1
4
2
O
O
0
TsX
0
2E -A =
-2
-1
2
4
r+272
-2
-1
0
2
0
+13
×（-1）
0
0
4
「2
-2rg
0
0
1/
0
0
于是，r（2E-A）=2，求得考」=（-1,2,0）「为（2E -A）x =0的一个基础解系.（-1,2,0）「
A 的属于特征值2的特征向量
计算A 的属于特征值-1的特征向量.考虑（-E- A）*= 0.
-E-A=
1
-2
2
-1
2
0
-4
0
0
2
1
T2+2r，
0
「i
+T3
0
×（-2）
A 的属于特征值 -1 的特征向量
计算A 的属于特征值-2的特征向量.考虑（ 2E-A）x = 0.
O
2
-1
0
2
11
-2E - A =
2
-5
2
T2+27j
0
2
-1
-2
-1
0
4
0
1
0
0
0
0
0
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2019考研数学二真题.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md


## tool · 2026-11-10T10:07:21Z


Script completed
Wall time 0.1 seconds
Output:

89-
90-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2019%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=2) · 本机 OCR
91-
92-> 读取原 PDF 时出现警告，建议核对原页。
93-
94-```text
95-（1I）设函数 （w）可导，：二 （兴），则28
96-（12）曲线y= In cos x
97-O《x《o）的弧长为
98-（13）已知函数f（x）=x
99-sin fd，则［ra）d=
100-1
101-0
102-0
103--2
104-1
105--1
106-1
107:（14） 已知矩阵A
108-=
109-3
110--2
111-2
112-0
113-0
114-3
115-4
116-dy
117-A，表示|A|中（i,j）元的代数余子式，则Au-Al2=
118-三、解答题（本题共9小题，共94分，解答应写出文字说明、证明过程或演算步骤.）
119-（15）（本题满分10分）
120-已知函数f（x）
121-（x2
122-xe
123-+1,x≤
124-*>0，求 （x），并求 （x）的极值
125-15-17题
--
170-```text
171-（21）（本题满分11分）
172-已知函数f（x）在［0, 1］上具有2阶导数，且f（0）=0,f（1）=1.Lf（x）dx=1.
173-证明：
174-（I）存在 （0,1），使得 （ ）=0；
175-（II）存在 E（0,1），使得f"（n）＜-2.
176-21 -23题
177-APP 扫码听课
178-（22）（本题满分11分）
179-已知向量组 I:a」
180-a-L5I:R-（HB.-12）
181-Bs
182-3
183-2.
184-a
185-+3
186-若向量组1与I等价，求a 的取值，并将B用c」，C，Q，线性表示.
187-（23）（本题满分11分）
188:已知矩阵 A =
189-\o
190--2
191-（I）求x,Y；
192-（II）求可逆矩阵P，使得PAP=B.
193-ooy/
194-—4—
195-```
-1
2
0
-4
0
0
2
1
T2+2r，
0
「i
+T3
0
×（-2）
A 的属于特征值 -1 的特征向量
计算A 的属于特征值-2的特征向量.考虑（ 2E-A）x = 0.
O
2
-1
0
2
11
-2E - A =
2
-5
2
T2+27j
0
2
-1
-2
-1
0
4
0
1
0
0
0
0
0
0
0
0
于是， （-2E-A）=2，求得 =（-1,2,4）「为（ 2E-A）x=0的一个基础解系.（-1, 2,4）「
A 的属于特征值-2的特征向量.
-1
-2
因此，P，可取为
2
］
-1
2
0
0
4
计算B的属于特征值2的特征向量.考虑（2E-B）x =0.
—28 —
```

## PDF 第 26 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2019%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=26) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
于是， （2E B）=2，求得 」=（1,0,0）「为（2E B） =0的一个基础解系.（1,0,0）「为B的
属于特征值2的特征向量
计算B 的属于特征值-1的特征向量.考虑（-E- B）x= 0.
-3
-1〇
-E-B
=
0
0
0
1×（-1）
0
T2 T3
0
1/
0
B的属于特征值-1的特征向量
计算B 的属于特征值-2的特征向量.考虑（-2E-B）x=0.
-4
-1
0
0
-2E -B=
0


## tool · 2026-11-10T10:07:28Z




## tool · 2026-11-10T10:07:31Z


Script completed
Wall time 0.1 seconds
Output:

% SOLUTION 400 2019 23
\textbf{入手角度}\quad 用分块结构和迹确定参数，再将 $AP=PB$ 写成三条列向量关系。

\textbf{解析}\quad （I）$A$ 为分块上三角矩阵，$-2$ 是其一个特征值。$B$ 的特征值为 $2,-1,y$，因此 $y=-2$。由迹相等得 $x-4=2-1-2=-1$，所以 $x=3$。

（II）若 $P=(p_1,p_2,p_3)$，需要
$Ap_1=2p_1$、$Ap_2=p_1-p_2$、$Ap_3=-2p_3$。由特征方程可取
$v_2=(1,2,0)^T$、$v_{-1}=(-2,1,0)^T$、$v_{-2}=(9,-2,4)^T$。令 $p_1=3v_2$、$p_2=v_2+v_{-1}$、$p_3=v_{-2}$，则
$(A+I)p_2=3v_2=p_1$，其余两式也成立。因此
\[
P=\begin{pmatrix}3&-1&9\\6&3&-2\\0&0&4\end{pmatrix}
\]
满足 $AP=PB$。其行列式为 $60$，故 $P^{-1}AP=B$。

% SOLUTION 401 2020 22
\textbf{入手角度}\quad 目标二次型的秩为二。原矩阵由单位矩阵与全一矩阵组成，可以分别沿坐标和及其正交补计算。
      90


## tool · 2026-11-10T10:07:40Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:08:12Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"d6b455","wall_time_seconds":0.0000075,"exit_code":0,"original_token_count":18,"output":"90 matched markers, all heading and basic LaTeX structure checks passed\n"}
14 representative matrix equations/powers verified numerically.

## assistant · 2026-11-10T10:08:19Z

90 道题的编号和年份已与题面逐项匹配，14 组矩阵等式与矩阵幂也已复算通过。复算时确认 2019 年第 23 题的矩阵漏了一个负号，已按本地解析修正对应解法，并把题面改动告知主代理。

## tool · 2026-11-10T10:08:21Z




## assistant · 2026-11-10T10:08:30Z

已完成第 319–408 题的原创 LaTeX 解析，覆盖 42 道选择题、18 道填空题和 30 道解答题。90 个编号全部匹配题面，14 组矩阵等式和矩阵幂复算通过。已向主代理报告 7 处题面转录差异。

独立解析文件未单独编译，排版由合并后的整卷验证。

## assistant · 2026-11-10T10:10:23Z

我会把 2026 年 10 道选择题的答案按原卷题号与合并后的解析逐项核对。

## tool · 2026-11-10T10:10:27Z


Script completed
Wall time 0.1 seconds
Output:

{"status":"fulfilled","value":{"chunk_id":"5ebd0e","wall_time_seconds":0.000009834,"exit_code":0,"original_token_count":4730,"output":"302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-14-2026年全国硕士研究生招生考试（数学二）试题及参考答案\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:15:一、选择题：1~10小题，每小题5分，共50分，下列每题给出的四个选项中，只有一个选项是符\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-16-合题目要求的，请将所选选项前的字母填在答题卡指定位置.\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-24-，6=-1\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:25:【答案】（A）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-26-ax’+ bx +arcsin x =ax’+bx+ + +o（x），\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-39-2：¼=4\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:40:【答案】（B）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-41-将2Ay（x）+ （x）代入得，2入＋ =1，\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-61-1\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:62:【答案】（A）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-63-万学海文考研\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-96-（x2+1）2\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:97:【答案】（D）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-98-【解析】在区间（-1,1）上，该细直棒对质点的引力在x轴方向的分力相互抵消为O，\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-107-（B） 当f（0）是极小值时，f（x）在（-1,0）单调递减时，在（0,1）单调递增\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:108:【答案】（C）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-109-【解析】对于（A）选项，极值的第一判别法要求f（x）在X=0处连续，故（A）错；\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-137-（C） gq（1）=0,g'（1）==e\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:138:【答案】（B）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-139-【解析】由于f（1）=0，所以反函数g（0）=1.\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-166-j=\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:167:【答案】（D）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-168-【解析】\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-180-（D） A'=\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:181:【答案】（B）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-182-【解析】由题设知A=P•BL P，其中B，B，L，只均为初等矩阵，\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-201-（C） a=-1,b=2\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:202:【答案】（A）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-203-ab）\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-280-（C）A，B 不能都是对角矩阵\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:281:【答案】（D）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-282-【解析】由 AB+BA=A’+B’，得（A-B）’=0.\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-292-xP （×+1）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:293:【答案】0<P<2\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-294-×P （×+1）\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-323-2026年全国硕士研究生招生考试（数学二）试题及参考答案\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:324:【答案】\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-325-1\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-335-13.设曲线x +2v3xy+y =1在点（0,1）处的曲率半径为\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:336:【答案】4\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-337-【解析】x’+2v3xy＋y =1两边同时对 求导得：\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-345-14.已知函数f（* ）可微，且df（0,0）= dx+3dy，记g（x）=f（In x,sin zx），则g'（1）=\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:346:【答案】 2元\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-347-【解析】由分析可知：大（0,0） ， （0,0=3，函数g（x）= （In x, sin zx）对x求导可得：\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-348-15.函数f（x）=In（2+x）在区间［0,2」上的平均值为_\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:349:【答案】3In2-1\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-350-【解析】J。 lnx +2k =J。 ln（x+ 2）d（t+2）=（x+2）I（x+2） - （ +2）\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-371-2026年全国硕士研究生招生考试（数学二）试题及参考答案\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:372:【答案】2\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-373-【解析】由题设知r（AAT）=1，故r（4）=1，则9+2\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-16-试卷及解析\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:17:一、选择题：1~10小题，每小题5分，共50分.下列每题给出的四个选项中，只有一个\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-18-选项是符合题目要求的.\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-22-，b=-1.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:23:1.【答案】A\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-24-【解析】\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-32-b=-1\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:33:1 故选A.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-34-a=\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-38-C.入=\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:39:2.【答案】B\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-40-1\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-57-c.2z\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:58:3.【答案】A\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-59-【解析】（法一）由微分形式不变性得dr-adz =e'te （dy+adz），\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-68-显然：\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:69:一=一，选A.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-70-orOy\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-90-故一一\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:91:一=一，选A.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-92-or Oy\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-105-（ +）\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:106:4.【答案】D\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-107-【解析】细直棒位于x轴上［-1,1］，取棒上任意微元，微元位置x，XE（-1,1），长度为dr.\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-123-因此总引力大小为F=2）。6m\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:124:dx，故选D.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-125-（1+×2）2\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-144-B. 当f（0）是极小值时，f（x）在（-1,0）单调递减，在（0,1）单调递增.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:145:5.【答案】C\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-146-但仍满足/（0）是极小值，排除：\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-170-0. 8（）-08（）-忌\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:171:6.【答案】B\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-172-【解析】由题知，当x=1时，厂（1）=0，放g（O）=1.\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-179--=-\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:180:一.选B.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-181-f（）\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-184-j三月+1-i\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:185:7.【答案】D\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-186-【解析】由题知，对应的图形如下图所示：\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-202-（会点）-103.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:203:选D.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-204-8.单位矩阵经过若干次互换两行得到的矩阵称为置换矩阵.设A为n阶置换矩阵，A A\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-219-C.A-'=A.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:220:8.【答案】B\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-221-【解析】设A=E E…Eu，\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-243-D. a=2,6=-1.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:244:9.【答案】A\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-245-【解析】设A=（a1,0 0g），C=（ ）\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-265-a-，解得a= 1\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:266:故选A.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-267-10.设3阶矩阵 A，B满足 AB+BA= A'’+B’，且A B，则下列结论错误的是\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-282-D. A-B只有一个线性无关的特征向量.\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:283:10.【答案】D\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-284-【解析】\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-319-dx收敛，则p的取值范围是_\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:320:11.【答案】0<P<2\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-321-【解析】1=J。aean*\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-363-13. 曲线x’+2V3r+y’=1在点（0.1）处的曲率半径为_\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:364:13.【答案】4\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-365-【解析】由x+2v3x+y =1，求导得\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-375-8（l）=！\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:376:14.【答案】-2元\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-377-旷f\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-391-I5. 函数厂（x）=In（2+x）在区间［0,2］上的平均值为_\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:392:15.【答案】3In2-1\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-393-【解折】/（）= （2+x）山\n--\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-396-16. 设矩阵A=\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:397:16.【答案】2\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-398-【解析】由题可知，二次型x「AA「x的规范形为了丫，因此矩阵 AA「的秩汐1，故A\n"}}
{"status":"fulfilled","value":{"chunk_id":"6e583b","wall_time_seconds":0.000037916,"exit_code":0,"original_token_count":476,"output":"679:% Q 2026 1\n680:\\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2026 年第 1 题}{1}{等价无穷小求系数}{030 / 408}\n685:\\begin{QuestionSolution}{2026 年第 1 题}\n1310:% Q 2026 6\n1311:\\QuestionPage{2.2 求导的基本法则}{选择题}{2026 年第 6 题}{1}{反函数与变上限积分求导}{061 / 408}\n1319:\\begin{QuestionSolution}{2026 年第 6 题}\n2431:% Q 2026 5\n2432:\\QuestionPage{2.6 函数性态的研究}{选择题}{2026 年第 5 题}{1}{单调性、极值与凹凸性}{116 / 408}\n2437:\\begin{QuestionSolution}{2026 年第 5 题}\n3735:% Q 2026 4\n3736:\\QuestionPage{3.4 定积分的应用}{选择题}{2026 年第 4 题}{1}{连续分布质点的引力}{166 / 408}\n3741:\\begin{QuestionSolution}{2026 年第 4 题}\n5346:% Q 2026 2\n5347:\\QuestionPage{4.2 高阶线性微分方程}{选择题}{2026 年第 2 题}{1}{非齐次方程的解的结构}{224 / 408}\n5352:\\begin{QuestionSolution}{2026 年第 2 题}\n5850:% Q 2026 3\n5851:\\QuestionPage{A.1 多元函数微分学}{选择题}{2026 年第 3 题}{1}{隐函数偏导数}{249 / 408}\n5856:\\begin{QuestionSolution}{2026 年第 3 题}\n6557:% Q 2026 7\n6558:\\QuestionPage{A.2 二重积分}{选择题}{2026 年第 7 题}{1}{二重积分定义与对称性}{289 / 408}\n6568:\\begin{QuestionSolution}{2026 年第 7 题}\n8066:% Q 2026 8\n8067:\\QuestionPage{A.4 线性代数}{选择题}{2026 年第 8 题}{1}{置换矩阵的性质}{358 / 408}\n8072:\\begin{QuestionSolution}{2026 年第 8 题}\n8078:% Q 2026 9\n8079:\\QuestionPage{A.4 线性代数}{选择题}{2026 年第 9 题}{2}{矩阵方程的可解性}{359 / 408}\n8101:\\begin{QuestionSolution}{2026 年第 9 题}\n8108:% Q 2026 10\n8109:\\QuestionPage{A.4 线性代数}{选择题}{2026 年第 10 题}{2}{矩阵恒等式与秩}{360 / 408}\n8117:\\begin{QuestionSolution}{2026 年第 10 题}\n.\n..\n001-113.tex\n114-234.tex\n235-318.tex\n319-408.tex\nbuild\ncache\ncheck_choices.py\ncheck_solution_pages.py\n"}}

## tool · 2026-11-10T10:10:35Z


Script completed
Wall time 0.1 seconds
Output:

['A', 'B', 'A', 'D', 'C', 'B', 'D', 'B', 'A', 'D'] {'1': 'A', '2': 'B', '3': 'A', '4': 'D', '5': 'C', '6': 'B', '7': 'D', '8': 'B', '9': 'A', '10': 'D'}
1 \(\sqrt[3]{1+x^2}-1=\tfrac13x^2+o(x^2)\)。等价要求左式 \((b+1)x+ax^2+o(x^2)\) 的一次系数为零，二次系数为 \(1/3\)。因此 \(\boxed{a=1/3,\ b=-1}\)，选 A。
2 \textbf{解析}\quad 记方程为 \(L[y]=q(x)\)，其中 \(L\) 线性且 \(q\not\equiv0\)。由 \(L[y_1]=L[y_2]=q\)，题设分别给出 \(2\lambda+\mu=1\)、\(\lambda-2\mu=0\)。联立得 \(\lambda=2/5\)、\(\mu=1/5\)，选 B。
3 由于 \(a\ne0\)，可得 \(z_x-z_y=1/a\)，选 \(\mathrm A\)。
4 所对应的积分式为 D。
5 对 A，取 \(f(x)=|x|\)（\(x\ne0\)）、\(f(0)=2\)，两侧各自的单调性成立，\(f(0)\) 却不是极小值。对 B，\(f(x)=x^2(1-x^2)\) 在零点取极小值，但在 \(x=1\) 左侧递减。对 D，\(f(x)=(x-1)x^3\) 的差商为 \(x^3\)，而 \(f''(x)=12x^2-6x\) 在 \((0,1/2)\) 上为负。
6 因此 \(g'(0)=1/f'(1)=\boxed{2/(3e)}\)，选 B。
7 对角线边缘至多相差 \(O(n)\) 个小格，连续性保证误差趋于零。把系数写成 \(\tfrac12\cdot 1/n^2\) 即为选项 \(\mathrm D\)。选项 \(\mathrm A\) 的三角形由 \(x+y=1\) 划分，该对称性并未给出。
8 \textbf{解析}\quad 设 $A=S_m\cdots S_1$，其中每个 $S_i$ 交换单位矩阵的两行。各 $S_i$ 均满足 $S_i^{-1}=S_i$，所以 $A^{-1}=S_1\cdots S_m$ 仍为置换矩阵。又 $A^*=(\det A)A^{-1}$，而 $\det A=(-1)^m$。取单位矩阵可排除 D，取一次对换的矩阵可排除 A、C。选 B。
9 $(1,1)-2(1,1)=(-1,-1)$。$A$ 的前三行线性无关，给定 $C$ 的前三行即可唯一求得 $B$ 的两列，此时第四行等式也自动成立。故 $a=b=-1$，选 A。
10 \textbf{解析}\quad 令 $N=A-B\ne O$，展开即得 $N^2=O$，所以 $N^3=O$，且任一特征值 $\lambda$ 满足 $\lambda^2=0$。若 $A,B$ 都是对角矩阵，$N$ 也是对角矩阵，$N^2=O$ 便迫使 $N=O$，矛盾。又 $\operatorname{Im}N\subseteq\ker N$，故 $r(N)\le3-r(N)$，结合 $N\ne O$ 得 $r(N)=1$。零特征空间维数为 $2$，因此错误项为 D。


## tool · 2026-11-10T10:10:40Z


Script completed
Wall time 0.1 seconds
Output:

\end{QuestionSolution}

% Q 2026 5
\QuestionPage{2.6 函数性态的研究}{选择题}{2026 年第 5 题}{1}{单调性、极值与凹凸性}{116 / 408}
设函数 \(f(x)\) 在区间 \([-1,1]\) 上有定义，则
\choices{当 \(f(x)\) 在 \((-1,0)\) 单调递减、在 \((0,1)\) 单调递增时，\(f(0)\) 是极小值}{当 \(f(0)\) 是极小值时，\(f(x)\) 在 \((-1,0)\) 单调递减、在 \((0,1)\) 单调递增}{当 \(f(x)\) 的图形在 \([-1,1]\) 上是凹的时，\(\dfrac{f(x)-f(1)}{x-1}\) 在 \([-1,1)\) 上单调递增}{当 \(\dfrac{f(x)-f(1)}{x-1}\) 在 \([-1,1)\) 上单调递增时，\(f(x)\) 的图形在 \([-1,1]\) 上是凹的}
\QuestionEnd

\begin{QuestionSolution}{2026 年第 5 题}
\textbf{入手角度}\quad 把差商解释为右端点固定在 \((1,f(1))\) 的割线斜率。

\textbf{解析}\quad 若图形是凹的，则对 \(-1\le x<y<1\)，点 \((y,f(y))\) 位于连接 \((x,f(x))\) 与 \((1,f(1))\) 的弦下方。因此
\[
f(1)-f(y)\ge \frac{1-y}{1-x}\,[f(1)-f(x)].
\]
除以 \(1-y>0\)，即得题中的差商单调递增，故选 C。
对 A，取 \(f(x)=|x|\)（\(x\ne0\)）、\(f(0)=2\)，两侧各自的单调性成立，\(f(0)\) 却不是极小值。对 B，\(f(x)=x^2(1-x^2)\) 在零点取极小值，但在 \(x=1\) 左侧递减。对 D，\(f(x)=(x-1)x^3\) 的差商为 \(x^3\)，而 \(f''(x)=12x^2-6x\) 在 \((0,1/2)\) 上为负。
\end{QuestionSolution}

% Q 2009 13
\QuestionPage{2.6 函数性态的研究}{填空题}{2009 年第 13 题}{2}{区间最值}{117 / 408}
函数$y = x^{2x}$在区间$(0,1]$上的最小值为 \blank{}．
\QuestionEnd

\begin{QuestionSolution}{2009 年第 13 题}
\textbf{入手角度}\quad 取对数后，幂指函数的最小值可由 \(2x\ln x\) 的单调性确定。

\textbf{解析}\quad 令 \(h(x)=2x\ln x\)。因为指数函数严格递增，\(x^{2x}=e^{h(x)}\) 与 \(h\) 在同一点取最小值。由 \(h'(x)=2(\ln x+1)\)，\(h\) 在 \((0,1/e)\) 递减，在 \((1/e,1]\) 递增。因此最小值为 \(\boxed{e^{-2/e}}\)。
\end{QuestionSolution}

\end{QuestionSolution}

% Q 2026 7
\QuestionPage{A.2 二重积分}{选择题}{2026 年第 7 题}{1}{二重积分定义与对称性}{289 / 408}
设函数 \(f(x,y)\) 在区域
\[D=\{(x,y)\mid 0\le x\le 1,\ 0\le y\le 1\}
\]
上连续，且 \(f(x,y)=f(y,x)\)，则
\[\iint_D f(x,y)\,dx\,dy=
\]
\choices{\(\displaystyle 2\lim_{n\to\infty}\sum_{i=1}^n\sum_{j=n+1-i}^n f\!\left(\frac{i}{n},\frac{j}{n}\right)\frac{1}{n^2}\)}{\(\displaystyle \frac12\lim_{n\to\infty}\sum_{i=1}^n\sum_{j=1}^n f\!\left(\frac{i}{n},\frac{j}{n}\right)\frac{1}{n^2}\)}{\(\displaystyle 2\lim_{n\to\infty}\sum_{i=1}^{2n}\sum_{j=1}^{2n+1-i} f\!\left(\frac{i}{2n},\frac{j}{2n}\right)\frac{1}{n^2}\)}{\(\displaystyle \frac12\lim_{n\to\infty}\sum_{i=1}^{2n}\sum_{j=1}^i f\!\left(\frac{i}{2n},\frac{j}{2n}\right)\frac{1}{n^2}\)}
\QuestionEnd

\begin{QuestionSolution}{2026 年第 7 题}
\textbf{入手角度}\quad 条件 \(f(x,y)=f(y,x)\) 是关于 \(y=x\) 的对称性。检查求和的下标是否覆盖由这条对角线切出的三角形，以及每格的面积。

\textbf{解析}\quad 取下三角形 \(T=\{0\le y\le x\le1\}\)，有 \(\iint_D f=2\iint_T f\)。将正方形均分成边长 \(1/(2n)\) 的小方格，则
\[
\iint_D f=2\lim_{n\to\infty}\sum_{i=1}^{2n}\sum_{j=1}^{i}
f\!\left(\frac{i}{2n},\frac{j}{2n}\right)\frac1{4n^2}.
\]
对角线边缘至多相差 \(O(n)\) 个小格，连续性保证误差趋于零。把系数写成 \(\tfrac12\cdot 1/n^2\) 即为选项 \(\mathrm D\)。选项 \(\mathrm A\) 的三角形由 \(x+y=1\) 划分，该对称性并未给出。
\end{QuestionSolution}

% Q 2011 13
\QuestionPage{A.2 二重积分}{填空题}{2011 年第 13 题}{2}{极坐标二重积分}{290 / 408}
设平面区域$D$由直线$y = x$，圆$x^2 + y^2 = 2y$及$y$轴围成，则二重积分$\iint_D xy\,\mathrm{d}{}\sigma =$ \blank{}．
\QuestionEnd

\begin{QuestionSolution}{2011 年第 13 题}
\textbf{入手角度}\quad 两条直线经过原点，圆也经过原点，极坐标可把三条边界分别写成两个固定角度与一个径向上限。

\textbf{解析}\quad 由圆方程得 \(0\le r\le2\sin\theta\)。\(y=x\) 和 \(y\) 轴之间的有界扇形部分给出 \(\pi/4\le\theta\le\pi/2\)。故
\[
\begin{aligned}
\iint_D xy\,\mathrm d\sigma


## tool · 2026-11-10T10:10:43Z




## assistant · 2026-11-10T10:10:46Z

2026 年第 1–10 题的解析答案与两份本地参考答案逐题一致，依次为 A、B、A、D、C、B、D、B、A、D。
