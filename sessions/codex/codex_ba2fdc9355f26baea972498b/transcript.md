# 01a1c4e2-949b-7631-815a-9c59d3611253

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-10T09:55:49Z

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


## developer · 2026-11-10T09:55:49Z

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
- mcp__ot
- mcp__rea: REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly answers the question; discover targets or inspect inventory only when needed. Tool results include i...
</tools>

## developer · 2026-11-10T09:55:49Z

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

## developer · 2026-11-10T09:55:49Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-10T09:55:49Z

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

## developer · 2026-11-10T09:55:49Z

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


## developer · 2026-11-10T09:55:49Z

<tools>
Added deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__pubmed
</tools>

## assistant · 2026-11-10T09:55:53Z

我先核对第 114–234 题的题序和原题，再分批写出推导。遇到影响解答的题面歧义会单独标记。

## tool · 2026-11-10T09:55:55Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"6b718c","wall_time_seconds":0.000008459,"exit_code":0,"original_token_count":247,"output":"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank\n.\n..\n.DS_Store\n.gitignore\n.question-bank-work\n27302模拟\n27李林880做题本（先保存后打开）\n302真题\nAGENTS.md\ndocs\nmemory\noutput\nremote-checkout\n工科数学分析基础第三版 上册（含大纲）.md\n考研数学一二三09-26年真题&解析\n1245:\\QuestionPage{2.6 函数性态的研究}{选择题}{2023 年第 7 题}{2}{极值点与拐点的参数条件}{114 / 408}\n2989:\\QuestionPage{4.2 高阶线性微分方程}{解答题}{2024 年第 18 题}{3}{欧拉方程与定积分}{234 / 408}\ntotal 48\ndrwxr-xr-x   7 oyamahappa  staff   224 Nov  9 23:01 .\ndrwxr-xr-x  15 oyamahappa  staff   480 Nov 10 13:18 ..\n-rw-r--r--   1 oyamahappa  staff   269 Nov 10 07:59 agents.md\n-rw-r--r--   1 oyamahappa  staff   518 Nov 10 13:05 gotchas.md\n-rw-r--r--   1 oyamahappa  staff  2974 Nov 10 13:32 plan.md\n-rw-r--r--   1 oyamahappa  staff  3228 Nov 10 13:35 progress.md\n-rw-r--r--   1 oyamahappa  staff  5985 Nov 10 13:35 verify.md\n"}
{"chunk_id":"8a7c9b","wall_time_seconds":0.000009,"exit_code":0,"original_token_count":798,"output":"---\nname: using-superpowers\ndescription: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions\n---\n\n<SUBAGENT-STOP>\nIf you were dispatched as a subagent to execute a specific task, ignore this skill.\n</SUBAGENT-STOP>\n\n<EXTREMELY-IMPORTANT>\nIf you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.\n\nIF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.\n\nThis is not negotiable. You cannot rationalize your way out of this.\n</EXTREMELY-IMPORTANT>\n\n## The Rule\n\n**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.\n\n**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.\n\nThen announce \"Using [skill] to [purpose]\" and follow the skill exactly. If it has a checklist, create a todo per item.\n\n## Skill Priority\n\nWhen multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.\n\n- \"Let's build X\" → superpowers:brainstorming first, then implementation skills.\n- \"Fix this bug\" → superpowers:systematic-debugging first, then domain skills.\n\n## Red Flags\n\nThese thoughts mean STOP—you're rationalizing:\n\n| Thought | Reality |\n|---------|---------|\n| \"This is just a simple question\" | Questions are tasks. Check for skills. |\n| \"I need more context first\" | Skill check comes BEFORE clarifying questions. |\n| \"Let me explore the codebase first\" | Skills tell you HOW to explore. Check first. |\n| \"I can check git/files quickly\" | Files lack conversation context. Check for skills. |\n| \"Let me gather information first\" | Skills tell you HOW to gather information. |\n| \"This doesn't need a formal skill\" | If a skill exists, use it. |\n| \"I remember this skill\" | Skills evolve. Read current version. |\n| \"This doesn't count as a task\" | Action = task. Check for skills. |\n| \"The skill is overkill\" | Simple things become complex. Use it. |\n| \"I'll just do this one thing first\" | Check BEFORE doing anything. |\n| \"This feels productive\" | Undisciplined action wastes time. Skills prevent this. |\n| \"I know what that means\" | Knowing the concept ≠ using the skill. Invoke it. |\n\n## Platform Adaptation\n\nIf your harness appears here, read its reference file for special instructions:\n\n- Claude Code: `references/claude-code-tools.md`\n- Codex: `references/codex-tools.md`\n- Pi: `references/pi-tools.md`\n- Antigravity: `references/antigravity-tools.md`\n- Hermes Agent: `references/hermes-tools.md`\n- Muse: `references/muse-tools.md`\n\n## User Instructions\n\nUser instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.\n"}

## tool · 2026-11-10T09:55:58Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 11983)
Total output lines: 440

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

## 302 数学二旧版 iPad 横屏版

原卷截图排版的旧版 iPad 横屏 PDF 和 `.tex` 从本地交付目录及远端 `main` 移除。保留原生 LaTeX 版本，以及仍供分节源稿使用的裁片资源。旧版可从 Git 历史恢复。

## 302 数学二原生 LaTeX 题面

按原卷题号读取逐年原卷文字层、已有 OCR 和配套解析。将题干、选择项、公式、矩阵和小问逐题写成 LaTeX，图题写成 TikZ 矢量路径。以同一份题库源稿生成 4:3 横屏题集和 A4 常规分节版，保留上册 19 节的定理页和原卷题号。原卷页码仅留在 LaTeX 源稿。行内和独立公式中的极限条件均排在 `lim` 正下方。按原书节序输出，核对上册与附录题目。不安装 TeX 编译器。

横屏版和 A4 常规版将年份、题号与知识点排在同一行，用小号灰字显示。交付覆盖现有文件，历史版本由 Git 保留。

## 27302 阶段模拟卷 iPad 版

从现有两份 LaTeX 源稿提取五套模拟卷和补充练习。保留各卷原题号、分值、选项、公式和小问。使用 800 × 600 点横向页面，每页上方排一道题，下方留白。用 PDF 书签定位各卷和补充练习。
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

- [x] 交叉核对 880 题、基础 500 题、辅导讲义和六套卷，按原题和小问去重。
- [x] 新增第二至第五卷，每卷 22 道，另有 76 道补充练习。逐题标记题源。
- [x] 编译并检查各卷题型、分值、分页和文字边界。扩充版 LaTeX 和 22 页 A4 PDF 已放入 `output`，其中第 17–22 页为补充练习。

## 302 数学二分节真题集

- [x] 核定 18 份数学二原卷与上册 19 节。
- [x] 定位 408 道题的题号和裁片边界，按主要考点分节。
- [x] 生成 `output/302数学二分节真题集.tex` 和 `output/302-question-facsimiles.pdf`。正文 236 题，附录 172 题，共 410 个裁片。

## 302 数学二 iPad 横屏版

- [x] 确认现有真题集的题序、节名与题面资源。
- [x] 核对 19 节的 85 条编号定理，连同常用性质和公式整理为 113 条。
- [x] 生成 432 页横屏 PDF 和 LaTeX，完成题页、写字区、目录链接和资源引用检查。
- [x] 删除旧版 iPad 横屏 PDF 和 `.tex`，核对远端分支内容。

## 302 数学二原生 LaTeX 题面

- [x] 完成 2009–2026 年 408 道题的原生 LaTeX 转录及题号复核，题面图形写成 10 幅 TikZ 矢量图。
- [x] 按上册 19 节收录 234 题，附录收录 174 题。修正两道二重积分换序题的分组。
- [x] 编译并验证 432 页 iPad 横屏 PDF。验证 A4 常规入口共用同一份题库，编译得到 89 页。
- [x] 在共用 LaTeX 源稿中调整 `lim` 的条件位置，并从两种版式的题头去掉原卷 PDF 页码。
- [x] 重新编译横屏版和 A4 版，核对极限公式、题头和横屏版分页。
- [x] 统一横屏版和 A4 常规版的题头，编译并核对 408 道题的题头样式，再覆盖现有文件。

## 27302 阶段模拟卷 iPad 版

- [x] 找到两份源稿，确认包含五套模拟卷和补充练习。
- [x] 提取并编译 186 道题的横屏 PDF。
- [x] 核对逐题内容、页序、留白和书签。
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
- 第三卷选择题依次为 A、D、B、C、D、C、A、C、C、A。填空题依次为 $0$、$1/a_1$、$1$、$1$、$a^2b$、$-1/(3\mathrm e)$。
- 第四卷选择题依次为 C、B、B、B、C、C、C、C、C、B。填空题依次为 $(1/8,4)$、$1/3$、$1/12$、$-99!$、$-2$、$-1/2$。
- 第五卷选择题依次为 C、C、A、B、B、B、D、D、C、C。填空题依次为 $1$、$-1/24$、$(2/3,3)$、$3$、$1/\pi$、$1$。
- 数值抽查覆盖数列和式、乘积极限、三角无穷小和指数差极限。Tectonic 编译成功，日志无缺字或溢出报告。检查了 22 页 A4 的题号、页码、文字边界和五个 PDF 书签。未进行截图检查。

## 302 数学二分节真题集

核对 2009–2026 年的 408 个年份与题号组合，包含 156 道选择题、108 道填空题、144 道解答题。正文 19 节，逐节检查章节名称、题型分组和题号顺序。410 个题面裁片引用各出现一次，所有裁片页均通过边界、非空和原裁片墨迹量比对。对题号执行本机 OCR 复核，并对调整过的边界复查。2009 年第 6 题和 2010 年第 8 题保留跨页续题。

完成 LaTeX 结构及资源引用检查。本次未进行 TeX 编译，未发现独立安装的编译器。

## 302 数学二 iPad 横屏版

核对 PDF 每页为 4:3 横屏、408 道题各占一页、题面完整、作答区留白且目录跳转有效。核对 19 节的定理编号和教材 PDF 页码，以及 LaTeX 与 PDF 的题序和题面引用。采用 PDF 几何和文字检查，不安装 TeX。

确认 432 页全部为 800 × 600 点。408 道题各占一页，410 个裁片按原比例嵌入，裁片非空且与原题面墨迹量一致至检查容差。逐题检查题面下方固定区域为空白，两道跨页题的两个裁片都在各自同一页。核对 85 条编号定理与教材 PDF 页码，验证 29 个书签、894 个内部链接以及 LaTeX 的 408 个题页和 410 个裁片引用。未编译 LaTeX，未做截图检查。

## 302 数学二原生 LaTeX 题面

与教材目录核对正文 19 节的节名、顺序和教材起始页。核对 408 道题的唯一题号、题型、数学定界符和原卷页码标记，沿用 85 条编号定理和 28 条其他要点。用本机应用自带的 Tectonic 编译，两版均无缺字或溢出警告。

横屏 PDF 为 432 页，页宽和页高分别为 800 和 600 点。验证 408 道题逐题单页、文字可提取、最短作答区 102.2 点、455 个有效内部链接及 28 个书签。六页图题包含可验证的矢量路径，所有页面无嵌入图片。A4 入口编译为 89 页，验证纸张尺寸、408 道题的顺序和内部链接。未安装编译器，未做截图检查。

两版通过 Tectonic 编译，日志无缺字、溢出和警告。2017 年第 3 题的 8 个趋近条件的字形均位于 `lim` 正下方。408 道题题序一致，题头未提取到原卷 PDF 页码，教材页码仍可提取。横屏版为 432 页，一题一页，保留 28 个书签和 455 个有效内部链接。A4 版为 89 页。未进行截图检查。

Tectonic 编译成功，日志无缺字、溢出和警告。逐题核对两版共 408 道题的标题、知识点基线、字号和灰色值。两版仍未显示原卷 PDF 页码，2017 年第 3 题的 8 个极限条件仍在 `lim` 正下方。横屏版 432 页，A4 常规版 89 页，内部链接均有效。未进行截图检查。

旧版 iPad 横屏 PDF 和 LaTeX 源稿已从本地及远端 `main` 文件树移除。原生版与仍供分节源稿使用的裁片资源校验值一致，两份旧版文件可从删除提交的父提交恢复。

## 27302 阶段模拟卷 iPad 版

Tectonic 编译成功，最终日志无缺字、警告或溢出。186 页的题号和题面文字逐题与原版核对。页面尺寸均为 800 × 600 点，题面下方至少留白 375 点。六个书签分别跳转到第 1、23、45、67、89、111 页。未进行截图或 iPad 实机验证。
# 注意事项

PDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。

用户要求题面以原生 LaTeX 转录时，题干、选项、公式和必要图形需要可编辑。PDF 裁片仅用于内部核对。

真题集的行内极限也将趋近条件排在 `lim` 正下方。题头显示原卷年份和题号，原卷页码只留作 LaTeX 源稿中的定位信息。

修改已有交付文件时直接覆盖，每个任务只保留当前交付，历史版本由 Git 保留。
\QuestionEnd

% Q 2023 7
\QuestionPage{2.6 函数性态的研究}{选择题}{2023 年第 7 题}{2}{极值点与拐点的参数条件}{114 / 408}
设函数
\[f(x)=(x^2+a)e^x,
\]
若 \(f(x)\) 没有极值点，但曲线 \(y=f(x)\) 有拐点，则 \(a\) 的取值范围是（ ）。
\choices{\([0,1)\)}{\([1,+\infty)\)}{\([1,2)\)}{\([2,+\infty)\)}
\QuestionEnd

% Q 2025 2
\QuestionPage{2.6 函数性态的研究}{选择题}{2025 年第 2 题}{1}{极值点和拐点的定义}{115 / 408}
已知函数 \(f\left( x \right) = \int_{0}^{x} e^{t^{2}} \sin t \mathrm{~d} t\)，\(g\left( x \right) = \int_{0}^{x} e^{t^{2}} \sin t \mathrm{~d} t \cdot \sin^{2} x\)，则
\choices{\(x = 0\) 是 \(f\left( x \right)\) 的极值点，也是 \(g\left( x \right)\) 的极值点.}{\(x = 0\) 是 \(f\left( x \right)\) 的极值点，\(\left( 0, 0 \right)\) 是曲线 \(y = g\left( x \right)\) 的拐点.}{\(x = 0\) 是 \(f\left( x \right)\) 的极值点，\(\left( 0, 0 \right)\) 是曲线 \(y = f\left( x \right)\) 的拐点.}{\(\left( 0, 0 \right)\) 是曲线 \(y = f\left( x \right)\) 的极值点，也是曲线 \(y = g\left( x \right)\) 的拐点.}
\QuestionEnd

% Q 2026 5
\QuestionPage{2.6 函数性态的研究}{选择题}{2026 年第 5 题}{1}{单调性、极值与凹凸性}{116 / 408}
设函数 \(f(x)\) 在区间 \([-1,1]\) 上有定义，则
\choices{当 \(f(x)\) 在 \((-1,0)\) 单调递减、在 \((0,1)\) 单调递增时，\(f(0)\) 是极小值}{当 \(f(0)\) 是极小值时，\(f(x)\) 在 \((-1,0)\) 单调递减、在 \((0,1)\) 单调递增}{当 \(f(x)\) 的图形在 \([-1,1]\) 上是凹的时，\(\dfrac{f(x)-f(1)}{x-1}\) 在 \([-1,1)\) 上单调递增}{当 \(\dfrac{f(x)-f(1)}{x-1}\) 在 \([-1,1)\) 上单调递增时，\(f(x)\) 的图形在 \([-1,1]\) 上是凹的}
\QuestionEnd

% Q 2009 13
\QuestionPage{2.6 函数性态的研究}{填空题}{2009 年第 13 题}{2}{区间最值}{117 / 408}
函数$y = x^{2x}$在区间$(0,1]$上的最小值为 \blank{}．
\QuestionEnd

% Q 2018 10
\QuestionPage{2.6 函数性态的研究}{填空题}{2018 年第 10 题}{2}{拐点及其切线}{118 / 408}
曲线$y = x^2 + 2\ln x$在其拐点处的切线方程是 \blank{}．
\QuestionEnd

% Q 2010 15
\QuestionPage{2.6 函数性态的研究}{解答题}{2010 年第 15 题}{2}{变上限积分的单调性与极值}{119 / 408}
求函数$f(x) = \int_1^{x^2} \left(x^2 - t \right) \mathrm{e}^{- t^2} \,\mathrm{d} t$的单调区间与极值．
\QuestionEnd

% Q 2011 16
\QuestionPage{2.6 函数性态的研究}{解答题}{2011 年第 16 题}{2}{参数曲线的极值和拐点}{120 / 408}
设函数$y = y(x)$由参数方程$\begin{cases}
  x = \frac{1}{3}t^3 + t + \frac{1}{3}, \\
  y = \frac{1}{3}t^3 - t + \frac{1}{3},
\end{cases}$确定，求$y = y(x)$的极值和曲线$y = y(x)$的凹凸区间及拐点．
\QuestionEnd

% Q 2012 20
\QuestionPage{2.6 函数性态的研究}{解答题}{2012 年第 20 题}{3}{用函数性态证明不等式}{121 / 408}
证明：$x\ln \frac{1 + x}{1 - x} + \cos x \ge 1 + \frac{x^2}{2}$（$- 1 < x < 1$）．
\QuestionEnd

% Q 2015 19
\QuestionPage{2.6 函数性态的研究}{解答题}{2015 年第 19 题}{3}{函数零点的个数}{122 / 408}
已知函数$f(x) = \int_x^1 \sqrt{1 + t^2} \,\mathrm{d} t + \int_1^{x^2} \sqrt{1 + t} \,\mathrm{d} t$，求$f(x)$的零点个数．
\QuestionEnd

% Q 2016 16
\QuestionPage{2.6 函数性态的研究}{解答题}{2016 年第 16 题}{2}{含绝对值的积分与最小值}{123 / 408}
设函数$f(x) = \int_0^1 \left| t^2 - x^2 \right|\,\mathrm{d} t$（$x > 0$），求$f'(x)$并求$f(x)$的最小值．
\QuestionEnd

% Q 2017 18
\QuestionPage{2.6 函数性态的研究}{解答题}{2017 年第 18 题}{3}{隐函数的极值}{124 / 408}
已知函数$y(x)$由方程$x^3 + y^3 - 3x + 3y - 2 = 0$确定，求$y(x)$的极值．
\QuestionEnd

% Q 2018 18
\QuestionPage{2.6 函数性态的研究}{解答题}{2018 年第 18 题}{3}{构造函数证明不等式}{125 / 408}
已知常数$k \ge \ln 2 - 1$，证明：$(x - 1)\left(x - \ln^2 x + 2k\ln x - 1 \right) \ge 0$．
\QuestionEnd

% Q 2019 15
\QuestionPage{2.6 函数性态的研究}{解答题}{2019 年第 15 题}{2}{求导与函数极值}{126 / 408}
已知函数$f(x) = \begin{cases}
     x^{2x}, & x > 0, \\
  x\mathrm{e}^x + 1, & x \le 0.
\end{cases}$求$f'(x)$，并求函数$f(x)$的极值．
\QuestionEnd

% Q 2021 18
\QuestionPage{2.6 函数性态的研究}{解答题}{2021 年第 18 题}{3}{凹凸区间与渐近线}{127 / 408}
已知
\[f(x)=\frac{x|x|}{1+x},
\]
求 \(f(x)\) 的凹凸性及渐近线。
\QuestionEnd

% Q 2022 21
\QuestionPage{2.6 函数性态的研究}{解答题}{2022 年第 21 题}{4}{二阶导数与凹凸性}{128 / 408}
设函数 \(f\left( x \right)\) 在 \(\left( -\infty,+\infty \right)\) 上有二阶连续导数，证明：
\(f^{\prime\prime}\left( x \right) \ge 0\)
的充分必要条件是对任意不同的实数 \(a,b\)，都有
\[f\left( \frac{a+b}{2} \right) \le \frac{1}{b-a}\int_{a}^{b} f\left( x \right) \mathrm{~d}x\]
成立.
\QuestionEnd

% Q 2025 21
\QuestionPage{2.6 函数性态的研究}{解答题}{2025 年第 21 题}{3}{导函数单调与函数凹凸性}{129 / 408}
（本题满分 12 分）
设函数 \(f\left( x \right)\) 在区间 \(\left( a, b \right)\) 内可导，证明：导函数 \(f^{\prime}\left( x \right)\) 在 \(\left( a, b \right)\) 内严格单调递增的充分必要条件是：对 \(\left( a, b \right)\) 内任意的 \(x_{1}\)，\(x_{2}\)，\(x_{3}\)，当 \(x_{1} < x_{2} < x_{3}\) 时，有

\(\frac{f\left( x_{2} \right) - f\left( x_{1} \right)}{x_{2} - x_{1}} < \frac{f\left( x_{3} \right) - f\left( x_{2} \right)}{x_{3} - x_{2}}\).
\QuestionEnd

\SectionHeading{3.1}{一元函数积分学及其应用}{定积分的概念、存在条件与性质}{定理与要点\quad 教材 PDF 第 189 页起\hfill 本节 11 题}
\pdfbookmark[1]{一元函数积分学及其应用}{chapter-3.1}
\pdfbookmark[2]{3.1 定积分的概念、存在条件与性质}{section-3.1}
\Theory{定理 1.1}{195}{可积的充要条件}{有界函数可积，当且仅当分割足够细时，各小区间的振幅乘区间长度之和可任意小。}
\Theory{定理 1.2}{196}{连续函数可积}{闭区间上的连续函数黎曼可积。}
\Theory{定理 1.3}{196}{有限间断点及单调情形}{有界函数若只有有限个第一类间断点，或在闭区间上单调，则可积。}
\Theory{性质 1.1--1.5}{197--199}{定积分的性质}{积分具有线性、保序、绝对值估计和区间可加性。可积函数的乘积仍可积。}
\Theory{性质 1.6}{199}{积分中值定理}{f 连续、g 可积且不变号，则存在 \ensuremath{\xi}，使 \ensuremath{\int} f g = f(\ensuremath{\xi}) \ensuremath{\int} g。}
\Theory{推论 1.2}{200}{积分平均值}{取权函数恒为 1，连续函数的积分平均值等于该闭区间某一点的函数值。}
\Theory{方法}{192--195}{从和式识别定积分}{把和式写成取样函数值乘小区间长度，再找分割的区间和取样点。}
% Q 2012 4
\QuestionPage{3.1 定积分的概念、存在条件与性质}{选择…1983 tokens truncated… 226.7 183.3 226.7 C181.1 226.7 179 226.7 176.8 226.7 C173.7 226.7 170.6 226.7 167.5 226.7 C166.6 226.6 165.7 226.6 164.8 226.6 C160.1 226.6 157.5 226.7 154 230 C151 229.8 148.8 229.5 146.2 228 C143.2 226.7 140.8 226.8 137.5 226.8 C137.2 226.8 137.2 226.8 135.5 226.8 C133.4 226.8 131.3 226.8 129.2 226.8 C127.7 226.8 126.2 226.8 124.7 226.8 C120.9 226.8 117 226.8 113.1 226.9 C109.2 226.9 105.2 226.9 101.3 226.9 C93.5 226.9 85.8 227 78 227 C77.9 227.6 77.7 228.2 77.6 228.8 C77.4 229.6 77.3 230.4 77.1 231.3 C76.9 232 76.8 232.8 76.6 233.6 C75.7 237.3 74.1 240.5 72.4 243.9 C72.1 244.6 71.7 245.3 71.4 246 C59.2 269 35.7 282.7 13.2 294.1 C12.4 294.5 11.6 294.9 10.8 295.3 C5.3 298 5.3 298 3 298 C3 320.4 3 342.9 3 366 C1.7 365.7 0.4 365.3 -1 365 C-1 319.5 -1 273.9 -1 227 C-44.2 227 -87.5 227 -132 227 C-132 225.7 -132 224.4 -132 223 C-113.5 223 -95 223 -76 223 C-76 220 -76 217.1 -76 214 C-75 214 -74 214 -73 214 C-73 217 -73 219.9 -73 223 C-49.2 223 -25.5 223 -1 223 C-1 200.6 -1 178.1 -1 155 C-2 154.7 -3 154.3 -4 154 C-4.3 153.3 -4.7 152.7 -5 152 C-28.4 152 -51.9 152 -76 152 C-75.7 150.7 -75.3 149.4 -75 148 C-67.3 146.9 -59.9 146.9 -52.1 147 C-50.1 147 -48.1 147 -46.1 147 C-41.2 147.1 -36.3 147.1 -31.4 147.2 C-28.7 147.2 -25.9 147.2 -23.2 147.2 C-20.6 147.3 -18 147.3 -15.4 147.3 C-14.2 147.3 -13 147.3 -11.8 147.3 C-11.3 147.3 -11.3 147.3 -8.7 147.4 C-5.5 146.9 -4.3 146.2 -2 144 C-1.5 141.8 -1.5 141.8 -1.5 139.1 C-1.5 138.1 -1.5 137.1 -1.4 136.1 C-1.4 135.5 -1.4 135.5 -1.5 132.7 C-1.4 132.2 -1.4 132.2 -1.4 129.2 C-1.4 125.4 -1.4 121.5 -1.4 117.7 C-1.4 115 -1.4 112.3 -1.3 109.7 C-1.3 103.4 -1.3 97.1 -1.3 90.8 C-1.3 83.6 -1.2 76.4 -1.2 69.3 C-1.1 54.5 -1 39.8 -1 25 C-1.3 25.1 -1.3 25.1 -2.7 25.9 C-3.4 26.2 -4.1 26.6 -4.9 27 C-5.6 27.4 -6.3 27.7 -7.1 28.1 C-9 29 -9 29 -11 29 C-10.4 25.2 -9.2 21.8 -7.7 18.3 C-7.3 17.2 -6.8 16.1 -6.4 15 C-5.9 13.9 -5.4 12.8 -4.9 11.7 C-4.5 10.6 -4 9.4 -3.5 8.3 C-2.3 5.5 -1.2 2.8 0 0 Z M0 147 C-0.7 148.3 -1.3 149.6 -2 151 C-1.5 151.3 -1.5 151.3 1 153 C2 152.3 3 151.7 4 151 C3.3 149.7 2.7 148.4 2 147 C1.3 147 0.7 147 0 147 Z M150 221 C149.7 222 149.3 223 149 224 C149.3 224.7 149.7 225.3 150 226 C151.6 225.7 153.3 225.3 155 225 C154.7 223.7 154.3 222.4 154 221 C152.7 221 151.4 221 150 221 Z M3 227 C2.4 240.7 1.8 254.3 1.9 268 C1.9 270.7 1.9 273.4 1.9 276.1 C1.9 277.9 1.9 279.7 1.9 281.4 C1.9 282.2 1.9 283 1.9 283.9 C1.9 287.4 2 290.6 3 294 C9 292.2 14.5 290 20.1 287 C20.8 286.6 21.5 286.2 22.3 285.8 C34.2 279.3 45.4 271.6 55 262 C55.8 261.2 56.6 260.4 57.4 259.6 C65.6 250.9 74 239.5 74 227 C50.6 227 27.1 227 3 227 Z };
\path[fill=black!100,even odd rule,shift={(284.875,235.625)}] svg {M0 0 C2.9 0.1 4.1 0.3 6.7 1.9 C8.4 4.9 8.4 7 7.7 10.3 C6.8 13.6 5.3 15.7 3.1 18.4 C2.5 18.4 1.8 18.4 1.1 18.4 C0.8 19 0.5 19.7 0.2 20.3 C-0.9 22.4 -0.9 22.4 -1.9 23.4 C1.8 23.4 5.4 23.4 9.1 23.4 C8.8 24.2 8.8 24.2 7.1 28.4 C2.2 28.4 -2.8 28.4 -7.9 28.4 C-6.1 24.9 -4.5 22.3 -1.9 19.4 C-1.2 19.4 -0.6 19.4 0.1 19.4 C0.4 18.6 0.7 17.8 1.1 16.9 C2.1 14.4 2.1 14.4 3.1 13.4 C3.4 6.8 3.4 6.8 2.1 4.4 C-4.6 5.2 -4.6 5.2 -6.9 6.4 C-5.9 1.7 -5.1 0.5 0 0 Z };
\path[fill=black!100,even odd rule,shift={(114.875,56.625)}] svg {M0 0 C3 0.1 4 0.3 6.6 2 C8.7 5.3 8.8 6.6 8.1 10.4 C5.5 15.3 2.3 19.7 -1.9 23.4 C1.8 23.4 5.4 23.4 9.1 23.4 C8.8 24.7 8.5 26 8.1 27.4 C2.8 28.1 -2.5 28.5 -7.9 28.4 C-6.1 24.4 -3.5 21.6 -0.5 18.4 C2.8 14.4 3.5 11.5 3.1 6.4 C2.8 5.7 2.5 5.1 2.1 4.4 C-3.5 4.1 -3.5 4.1 -6.9 6.4 C-5.9 1.7 -5.1 0.5 0 0 Z };
\path[fill=black!100,even odd rule,shift={(365,236)}] svg {M0 0 C1.4 2.2 1.4 2.2 2 5 C1.6 6 1.3 7 0.9 8.1 C0.6 9 0.3 10 0 11 C1 12.3 2 13.7 3 15 C2.9 19 2.6 21.2 0.1 24.4 C-3.7 27.3 -6.3 27.3 -11 27 C-11.7 26 -12.3 25 -13 24 C-9.3 22.8 -6.8 23.4 -3 24 C-1 21 -1 21 -1.1 18.6 C-2.3 15.2 -4.1 14 -7 12 C-6.7 11.7 -6.7 11.7 -5 10.3 C-3 8 -3 8 -2.8 5.2 C-2.8 4.9 -2.8 4.9 -3 3 C-5.8 2 -6.9 2 -9.8 2.9 C-10.1 3.1 -10.1 3.1 -12 4 C-9.6 -0.7 -9.6 -0.7 -7.1 -1.9 C-4.2 -2 -2.5 -1.5 0 0 Z };
\path[fill=black!100,even odd rule,shift={(171,0)}] svg {M0 0 C3 0 6 0 9 0 C9 3 9 3 7.6 4.8 C3.5 10.5 3.6 19.2 4.6 25.9 C5.6 30.4 7.1 33.5 10 37 C5.9 35.5 3.3 32.6 1 29 C-1.7 21.7 -1.6 14.3 1.6 7.1 C2 6.1 2.5 5 3 4 C3 3 3 2 3 1 C2 0.7 1 0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(169,1)}] svg {M0 0 C0.7 0.3 1.3 0.7 2 1 C0.7 4 -0.6 6.9 -2 10 C-1.3 10.3 -0.7 10.7 0 11 C-0.3 11.2 -0.3 11.2 -2 12 C-2.8 14.5 -3.6 17 -4.3 19.6 C-6.1 25.7 -7.8 31 -12 36 C-15.3 37 -15.3 37 -18 37 C-18 35.7 -18 34.4 -18 33 C-17.3 33 -16.7 33 -16 33 C-16 33.7 -16 34.3 -16 35 C-15.5 34.8 -15.5 34.8 -13 34 C-9.9 26.7 -8.3 18.8 -7 11 C-7.7 10.7 -8.3 10.3 -9 10 C-8.3 9.3 -7.5 8.6 -6.8 7.8 C-4.3 5.3 -2.1 2.8 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,295)}] svg {M0 0 C0 8.6 0 17.2 0 26 C0.7 26 1.3 26 2 26 C2 26.7 2 27.3 2 28 C-0.3 28 -2.6 28 -5 28 C-5.3 27.3 -5.7 26.7 -6 26 C-5.3 26 -4.7 26 -4 26 C-4 18.4 -4 10.8 -4 3 C-5 2.7 -6 2.3 -7 2 C-4.4 0.5 -3.1 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(115,234)}] svg {M0 0 C7.4 -0.5 7.4 -0.5 10.4 1.9 C12.8 5.1 13.5 7.5 13.4 11.6 C12.5 17 9.3 22.1 5.1 25.6 C3.2 26.7 3.2 26.7 0 28 C-0.7 27.7 -1.3 27.3 -2 27 C-0.6 25.5 -0.6 25.5 1 24 C1.7 24 2.3 24 3 24 C3.3 23.3 3.5 22.6 3.8 21.9 C4.7 19.8 5.6 17.7 6.6 15.6 C8.1 11.7 8.5 9.1 8 5 C6.9 3.1 6.9 3.1 5 2 C1.8 1.8 1.8 1.8 -1 2 C-0.7 1.3 -0.3 0.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(114,235)}] svg {M0 0 C0 0.7 0 1.3 0 2 C-0.8 2.7 -1.5 3.4 -2.3 4.1 C-6.5 8.6 -7.8 12.8 -8.3 18.8 C-8 22 -8 22 -6 25 C-3.4 25.7 -3.4 25.7 -1 26 C-1 26.3 -1 26.7 -1 27 C-7.3 27.4 -7.3 27.4 -10.4 25.7 C-13.4 22.5 -13.5 18.7 -13.4 14.5 C-12.5 9.1 -9 4.7 -5 1.2 C-3 0 -3 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(203,1)}] svg {M0 0 C4.7 1.9 7.1 5.1 9.2 9.6 C10.9 17.1 10.9 23.6 7.2 30.3 C5.9 32.1 4.6 33.5 3 35 C2.3 34.7 1.7 34.3 1 34 C1.5 33.3 1.9 32.5 2.4 31.8 C6.3 25 6.1 15.9 4.4 8.4 C3.3 5.3 1.8 2.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(155,137)}] svg {M0 0 C0 8.9 0 17.8 0 27 C1 27.3 2 27.7 3 28 C-2.6 29.1 -2.6 29.1 -6 28 C-5.3 27.3 -4.7 26.7 -4 26 C-3.8 23.8 -3.8 23.8 -3.8 21 C-3.8 20 -3.8 19 -3.8 18 C-3.8 17 -3.9 15.9 -3.9 14.9 C-3.9 13.8 -3.9 12.8 -3.9 11.7 C-3.9 9.1 -4 6.6 -4 4 C-4.7 3.7 -5.3 3.3 -6 3 C-1.1 0 -1.1 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(69,234)}] svg {M0 0 C1.3 9 1.1 17.9 1 27 C1.7 27.3 2.3 27.7 3 28 C0 28 -2.9 28 -6 28 C-5.3 27.3 -4.7 26.7 -4 26 C-3.7 23.8 -3.7 23.8 -3.7 21.1 C-3.7 20.1 -3.7 19.1 -3.7 18.1 C-3.7 17.1 -3.7 16.1 -3.8 15 C-3.7 14 -3.7 13 -3.7 11.9 C-3.7 11.4 -3.7 11.4 -3.7 8.9 C-3.7 8 -3.7 7.1 -3.7 6.2 C-4 4 -4 4 -6 2 C-2.2 0 -2.2 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(217,238)}] svg {M0 0 C0 0.7 0 1.5 0.1 2.3 C0.2 5.6 0.3 9 0.4 12.4 C0.4 13.6 0.4 14.7 0.5 15.9 C0.5 17.1 0.5 18.2 0.6 19.3 C0.6 20.4 0.6 21.4 0.7 22.5 C1 25 1 25 3 27 C0 27 -2.9 27 -6 27 C-5.3 26.3 -4.7 25.7 -4 25 C-3.8 22.8 -3.8 22.8 -3.8 20 C-3.8 19 -3.8 18 -3.8 17 C-3.8 16 -3.9 14.9 -3.9 13.9 C-3.9 12.8 -3.9 11.8 -3.9 10.7 C-3.9 8.1 -4 5.6 -4 3 C-5 2.7 -6 2.3 -7 2 C-4 0 -4 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(428,217)}] svg {M0 0 C2.2 1.9 2.2 1.9 4 4 C4.8 3.3 5.6 2.7 6.4 2 C9 0 9 0 11 0 C11 1 11 2 11 3 C10.6 3.1 10.6 3.1 8.6 3.6 C6 5 6 5 5.1 7.9 C5 10.6 5.1 12.5 6 15 C7 15 8 15 9 15 C8.3 16.3 7.7 17.6 7 19 C5.7 18.7 4.4 18.3 3 18 C2.8 17.2 2.8 17.2 2 13 C1 13.3 0 13.7 -1 14 C-0.8 12.9 -0.6 11.9 -0.4 10.8 C-0 7.1 0.1 5.9 -2 3 C-2.7 2.3 -3.3 1.7 -4 1 C-2.2 0.2 -2.2 0.2 0 0 Z };
\path[fill=black!100,even odd rule,shift={(185,11)}] svg {M0 0 C2 0 4 0 6 0 C6.3 1.3 6.7 2.6 7 4 C7.7 4 8.3 4 9 4 C9.3 7.6 9.7 11.3 10 15 C11.3 14.3 12.6 13.7 14 13 C13.2 14.9 13.2 14.9 12 17 C9.9 17.8 9.9 17.8 8 18 C6 15 6 15 6 12 C5.3 12 4.7 12 4 12 C4 11.4 3.9 10.8 3.9 10.1 C3.8 9.3 3.8 8.5 3.7 7.7 C3.6 6.9 3.6 6.1 3.5 5.3 C2.9 2.6 2 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(38,246)}] svg {M0 0 C5.6 0 11.2 0 17 0 C17 0.7 17 1.3 17 2 C11.4 2 5.8 2 0 2 C0 1.3 0 0.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(89,307)}] svg {M0 0 C5.9 0 11.9 0 18 0 C18 0.3 18 0.7 18 1 C12.1 1 6.1 1 0 1 C0 0.7 0 0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(188,23)}] svg {M0 0 C0 3 0 3 -1.2 4.7 C-3 6 -3 6 -7 6 C-6.7 5 -6.3 4 -6 3 C-4.1 2.4 -4.1 2.4 -2 2 C-1.3 1.3 -0.7 0.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(426,231)}] svg {M0 0 C0 1 0 2 0 3 C-0.7 3.7 -1.3 4.3 -2 5 C-4.1 4.6 -4.1 4.6 -6 4 C-6 3.3 -6 2.7 -6 2 C-5.6 1.9 -5.6 1.9 -3.6 1.6 C-1 1 -1 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(57,190)}] svg {M0 0 C1 0 2 0 3 0 C3 1.7 3 3.3 3 5 C2 5 1 5 0 5 C0 3.3 0 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,156)}] svg {M0 0 C1 0.3 2 0.7 3 1 C2.7 2.3 2.3 3.6 2 5 C1 4.7 0 4.3 -1 4 C-0.7 2.7 -0.3 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(196,11)}] svg {M0 0 C1.7 0 3.3 0 5 0 C4.7 1 4.3 2 4 3 C2 3.3 0 3.7 -2 4 C-1.3 2.7 -0.7 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(283,124)}] svg {M0 0 C1.3 0 2.6 0 4 0 C3.7 1.3 3.3 2.6 3 4 C2 3.7 1 3.3 0 3 C0 2 0 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,115)}] svg {M0 0 C1 0.3 2 0.7 3 1 C2.7 2.3 2.3 3.6 2 5 C1 4.3 0 3.7 -1 3 C-0.7 2 -0.3 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,82)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C1.7 3.7 0.4 3.3 -1 3 C-0.7 2 -0.3 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,206)}] svg {M0 0 C1 0.3 2 0.7 3 1 C2.7 2.3 2.3 3.6 2 5 C1.3 5 0.7 5 0 5 C-0.6 3.1 -0.6 3.1 -1 1 C-0.7 0.7 -0.3 0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,198)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C-0.3 3 -0.7 2 -1 1 C-0.7 0.7 -0.3 0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,165)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C1.7 3.7 0.4 3.3 -1 3 C-0.7 2 -0.3 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(57,207)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(57,199)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,190)}] svg {M0 0 C1 0 2 0 3 0 C2.7 1.3 2.3 2.6 2 4 C1 3.7 0 3.3 -1 3 C-0.7 2 -0.3 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(283,182)}] svg {M0 0 C1.3 0 2.6 0 4 0 C3.7 1.3 3.3 2.6 3 4 C2.3 4 1.7 4 1 4 C0.7 2.7 0.3 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(57,182)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(57,174)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,173)}] svg {M0 0 C1 0.3 2 0.7 3 1 C3 2 3 3 3 4 C1.7 3.7 0.4 3.3 -1 3 C-0.7 2 -0.3 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(58,165)}] svg {M0 0 C0.7 0.3 1.3 0.7 2 1 C2 2.3 2 3.6 2 5 C1 4.7 0 4.3 -1 4 C-0.7 2.7 -0.3 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(57,157)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,107)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,99)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,90)}] svg {M0 0 C1 0.3 2 0.7 3 1 C3 2 3 3 3 4 C2 4.3 1 4.7 0 5 C0 3.3 0 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,148)}] svg {M0 0 C1 0.3 2 0.7 3 1 C3 2 3 3 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,140)}] svg {M0 0 C1 0.3 2 0.7 3 1 C3 2 3 3 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(284,132)}] svg {M0 0 C1 0.3 2 0.7 3 1 C2.7 2 2.3 3 2 4 C1 3.7 0 3.3 -1 3 C-0.7 2 -0.3 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(306,94)}] svg {M0 0 C0.7 0.3 0.7 0.3 4 2 C2.7 1.7 1.4 1.3 0 1 C0 0.7 0 0.3 0 0 Z };
\end{tikzpicture}}
则函数$F(x) = \int_0^x f(t)\,\mathrm{d} t$的图形为\pickout{}

\noindent
\graphchoice{A}{%
\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.290994,yscale=-0.290994]
\path[use as bounding box] (0,0) rectangle (440,266);
\path[fill=black!100,even odd rule,shift={(166,1)}] svg {M0 0 C0.7 0 1.3 0 2 0 C5 7.3 7.9 14.5 11 22 C10.5 22.2 10.5 22.2 8 23 C6 22 4 21 2 20 C2 47.4 2 74.8 2 103 C4 103 6 103 8 103 C8 104 8 105 8 106 C6.3 106.3 4.7 106.7 3 107 C2.7 126.8 2.3 146.6 2 167 C22.5 167 42.9 167 64 167 C64 165.3 64 163.7 64 162 C65 162.3 66 162.7 67 163 C67 164.3 67 165.6 67 167 C81.2 167 95.4 167 110 167 C110.7 165.3 111.3 163.7 112 162 C112.6 160.8 113.3 159.5 113.9 158.3 C114.3 157.6 114.7 156.9 115 156.2 C115.4 155.5 115.8 154.8 116.2 154.1 C120.3 146.4 124.1 138.7 128 131 C149.4 131 170.9 131 193 131 C193 132 193 133 193 134 C172.2 134.3 151.4 134.7 130 135 C128.2 138.6 128.2 138.6 119 157 C118.2 158.5 118.2 158.5 114 166 C118.6 166 123.2 166 128 166 C128.3 164.7 128.7 163.4 129 162 C130 162.3 131 162.7 132 163 C132 164.3 132 165.6 132 167 C152.1 166.7 172.3 166.3 193 166 C193.3 164.7 193.7 163.4 194 162 C194.7 162 195.3 162 196 162 C196.3 163.3 196.7 164.6 197 166 C208.6 166 220.1 166 232 166 C231 164.3 230 162.7 229 161 C229 160.3 229 159.7 229 159 C234 159.8 238.6 161.6 243.2 163.4 C244.1 163.7 244.9 164 245.8 164.3 C246.2 164.4 246.2 164.4 248.1 165.2 C248.5 165.3 248.5 165.3 250.3 166 C252 167 252 167 253 170 C252.2 170.3 251.4 170.6 250.5 171 C243.6 173.6 236.8 176.2 230 179 C229.7 178.3 229.3 177.7 229 177 C230.1 174.5 231.6 172.3 233 170 C217.3 169.7 201.6 169.5 185.9 169.4 C178.6 169.4 171.3 169.3 164 169.1 C157.7 169 151.3 168.9 145 168.9 C141.6 168.9 138.2 168.9 134.9 168.8 C114.4 168.2 114.4 168.2 108.7 172.9 C104.9 177.4 102.3 182.4 100 187.8 C97.9 192.5 94.3 196.2 91 200 C90.3 200.9 89.6 201.7 88.8 202.6 C83 209.5 76.2 216.2 67 218 C61.6 217.6 57.3 216.1 52.6 213.7 C51.9 213.3 51.2 213 50.5 212.6 C33.8 203.9 19.7 190.3 5.9 177.6 C4 176 4 176 2 175 C2 194.1 2 213.3 2 233 C4 233 6 233 8 233 C8 234 8 235 8 236 C6 236 4 236 2 236 C2 242.3 2 248.5 2 255 C1 255 0 255 -1 255 C-1 226.9 -1 198.9 -1 170 C-29.7 170 -58.4 170 -88 170 C-88 169 -88 168 -88 167 C-80.7 166.7 -73.5 166.3 -66 166 C-65.7 164.7 -65.3 163.4 -65 162 C-64.3 162 -63.7 162 -63 162 C-62.8 162.7 -62.8 162.7 -62 166 C-43.8 166 -25.7 166 -7 166 C-9.9 162.4 -12.7 159.2 -16 156 C-16.8 155.2 -17.7 154.3 -18.6 153.4 C-19.5 152.6 -20.4 151.7 -21.3 150.8 C-22.8 149.3 -24.3 147.7 -25.8 146.2 C-26.9 145.2 -27.9 144.2 -28.9 143.2 C-34.3 137.8 -39.7 132.4 -44.6 126.6 C-46 125 -47.4 123.6 -48.9 122.1 C-51 120 -51 120 -51 118 C-51.7 118 -52.3 118 -53 118 C-54.6 116.3 -56 114.5 -57.5 112.6 C-61.9 107.1 -61.9 107.1 -64 105 C-64 104 -64 103 -64 102 C-60.1 103.6 -57.9 106 -55.2 109.1 C-54.7 109.6 -54.7 109.6 -52.5 112.1 C-51.7 113.1 -50.9 114 -50 115 C-49.3 115.8 -48.7 116.5 -48 117.3 C-45.4 120.2 -42.8 123.2 -40.4 126.2 C-38 129 -35.6 131.4 -33 134 C-31.9 135.1 -30.7 136.3 -29.6 137.4 C-29.3 137.7 -29.3 137.7 -27.7 139.3 C-19.1 147.9 -10.6 156.4 -2 165 C-1.9 150.7 -1.7 136.3 -1.6 122 C-1.5 115.3 -1.5 108.6 -1.4 102 C-0.9 44.5 -0.9 44.5 -1 21 C-1.8 21.3 -2.5 21.7 -3.3 22 C-6 23 -6 23 -9 23 C-6.5 15.1 -3.3 7.6 0 0 Z M4 170 C5.6 173.3 6.4 174.6 8.9 176.9 C9.4 177.4 10 178 10.6 178.5 C11.2 179.1 11.8 179.6 12.4 180.2 C13.1 180.8 13.7 181.3 14.3 181.9 C50.8 215 50.8 215 66.8 215 C78.9 212.9 87.9 200.5 94.6 191.1 C96.5 188.4 98.2 185.7 100 183 C100.7 181.9 101.4 180.9 102.1 179.8 C107 172.3 107 172.3 107 170 C73 170 39 170 4 170 Z };
\path[fill=black!100,even odd rule,shift={(188,2)}] svg {M0 0 C5.6 0 11.2 0 17 0 C16.7 1.7 16.3 3.3 16 5 C15.3 5 14.7 5 14 5 C14 4 14 3 14 2 C11.4 2 8.7 2 6 2 C5 4.6 4 7.3 3 10 C5.3 9.3 7.6 8.7 10 8 C9.7 10 9.3 12 9 14 C6.7 13.7 4.4 13.3 2 13 C1.8 14.5 1.7 16 1.5 17.4 C1.4 18.3 1.3 19.1 1.2 19.9 C1 22 1 22 1 23 C-1.6 23 -4.3 23 -7 23 C-6.6 22.5 -6.1 21.9 -5.6 21.4 C-3.7 18.6 -2.8 15.9 -1.8 12.6 C-1.5 11.5 -1.1 10.4 -0.8 9.3 C0 6 0 6 0 0 Z };
\path[fill=black!100,even odd rule,shift={(28,114)}] svg {M0 0 C0.7 0 1.3 0 2 0 C2.2 0.7 2.4 1.3 2.6 2 C3.5 5 4.5 7.9 5.4 10.9 C5.5 11.4 5.5 11.4 6.3 14 C6.5 14.5 6.5 14.5 7.3 17 C7.6 17.9 7.8 18.8 8.1 19.8 C9 22 9 22 11 24 C8.4 24 5.7 24 3 24 C3.3 23 3.7 22 4 21 C3.1 18.3 3.1 18.3 2 16 C0.4 16 -1.3 16 -3 16 C-3.7 18 -4.4 20 -5 22 C-4.7 22.7 -4.3 23.3 -4 24 C-6 24 -8 24 -10 24 C-9 23.7 -8 23.3 -7 23 C-6.5 21 -6.1 18.9 -5.7 16.9 C-4.3 11.1 -2.1 5.6 0 0 Z M-1 7 C-1.7 9.3 -2.3 11.6 -3 14 C-1.4 14 0.3 14 2 14 C1.6 11.1 1.6 11.1 1 8 C0.3 7.7 -0.3 7.3 -1 7 Z };
\path[fill=black!100,even odd rule,shift={(299,179)}] svg {M0 0 C1.9 1.1 1.9 1.1 3 3 C3.6 6.9 3.2 8.7 1.2 12.1 C0.5 13.1 -0.3 14 -1 15 C-1.6 15.8 -2.2 16.6 -2.8 17.4 C-3.2 17.9 -3.6 18.4 -4 19 C-1.4 19 1.3 19 4 19 C3.7 20.3 3.3 21.6 3 23 C-1.3 23 -5.6 23 -10 23 C-4 15 -4 15 -2.3 12.9 C-0.5 10.2 -0.7 8.2 -1 5 C-2 4 -2 4 -4.4 3.9 C-7 4 -7 4 -9 5 C-8.6 3.1 -8.6 3.1 -8 1 C-5.2 -0.4 -3.1 -0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(363,178)}] svg {M0 0 C1.9 2.1 1.9 2.1 3 5 C2.7 7 2.4 9 2 11 C2.7 12.3 3.3 13.7 4 15 C3.8 17.7 3.3 19.4 1.9 21.8 C-1.2 23.8 -4.3 23.7 -8 24 C-8.3 23 -8.7 22 -9 21 C-6.4 21 -3.7 21 -1 21 C-0.3 18.7 -0.3 18.7 0 16 C-1.3 14.3 -1.3 14.3 -3 13 C-3.7 12.3 -4.3 11.7 -5 11 C-4 10.3 -3 9.7 -2 9 C-1.8 6.4 -1.8 6.4 -2 4 C-4 4 -6 4 -8 4 C-7.7 3 -7.3 2 -7 1 C-4.4 -0.3 -2.9 -0.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(150,177)}] svg {M0 0 C3.1 -0.2 5.4 -0.3 8.3 1 C10.9 4.1 11.3 7.1 11 11 C9.4 16.3 6.8 20.1 2 23 C-0.8 23.8 -0.8 23.8 -3 24 C-1.3 22.3 0.3 20.7 2.1 19.2 C6.5 14.1 6.3 8.4 6 2 C3.7 2 1.4 2 -1 2 C-0.7 1.3 -0.3 0.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(149,178)}] svg {M0 0 C-1.5 3.1 -3.2 6 -5 9 C-6.6 12.2 -6.5 15.5 -6 19 C-4 21.5 -4 21.5 -2 23 C-5.6 22.8 -7.4 22.6 -9.9 19.9 C-11.3 16 -11.2 12.9 -10 9 C-7.9 5.1 -5 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(234,181)}] svg {M0 0 C0.3 7.6 0.7 15.2 1 23 C-1 23 -3 23 -5 23 C-4.7 22.3 -4.3 21.7 -4 21 C-3.9 19.6 -3.9 18.3 -3.9 16.9 C-3.9 16.1 -3.9 15.3 -3.9 14.5 C-3.9 14.1 -3.9 14.1 -3.9 12 C-3.9 11.2 -3.9 10.3 -3.9 9.5 C-3.9 8.7 -3.9 7.9 -3.9 7.1 C-3.9 6.3 -3.9 5.6 -3.9 4.8 C-4 3 -4 3 -5 1 C-3 0 -3 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(231,1)}] svg {M0 0 C4.1 3.1 6.4 4.9 8 10 C8.9 17.1 8.4 22.3 4 28 C1.8 29.4 1.8 29.4 0 30 C0.5 29.3 0.9 28.5 1.4 27.8 C4.6 22.2 4.5 16.3 4 10 C3.2 7.4 2.3 5.4 1 3 C0.7 2 0.3 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(156,94)}] svg {M0 0 C0 0.6 0.1 1.3 0.1 1.9 C0.2 4.7 0.3 7.5 0.4 10.4 C0.5 11.4 0.5 12.3 0.6 13.4 C0.6 14.3 0.6 15.2 0.7 16.2 C0.7 17.1 0.8 17.9 0.8 18.8 C1 21 1 21 2 23 C-0.3 23 -2.6 23 -5 23 C-4.3 22.7 -3.7 22.3 -3 22 C-3 15.7 -3 9.5 -3 3 C-3.7 2.7 -4.3 2.3 -5 2 C-2 0 -2 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(209,3)}] svg {M0 0 C0.7 0.3 1.3 0.7 2 1 C1.7 1.6 1.4 2.1 1 2.7 C-2.6 10.8 -0.7 19 2 27 C-1.4 25.9 -1.6 25.5 -3.2 22.5 C-5.3 17.9 -5.9 13.9 -5 9 C-3.8 5.8 -2.4 2.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(107,181)}] svg {M0 0 C0.3 7.6 0.7 15.2 1 23 C-1 23 -3 23 -5 23 C-4.3 22.7 -3.7 22.3 -3 22 C-3 15.7 -3 9.5 -3 3 C-3.7 2.7 -4.3 2.3 -5 2 C-2 0 -2 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(426,163)}] svg {M0 0 C1.6 0 3.3 0 5 0 C5.3 1 5.7 2 6 3 C6.6 2.5 7.2 2 7.8 1.5 C10 0 10 0 14 0 C14 0.7 14 1.3 14 2 C13.6 2.1 13.6 2.1 11.6 2.8 C10.7 3.2 9.9 3.6 9 4 C7.8 7.6 8.5 8.6 10 12 C10.7 11.7 11.3 11.3 12 11 C11.3 12.3 10.7 13.6 10 15 C8.1 14.7 8.1 14.7 6 14 C4 11 4 11 4 8 C2.4 2.4 2.4 2.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(216,10)}] svg {M0 0 C2.4 -0.1 2.4 -0.1 5 0 C5.7 0.7 6.3 1.3 7 2 C7.7 1.3 8.3 0.7 9 0 C10.3 0 11.6 0 13 0 C13 0.7 13 1.3 13 2 C11.3 2.7 9.7 3.3 8 4 C8 6.6 8 9.3 8 12 C9 12.3 10 12.7 11 13 C10.3 13.3 10.3 13.3 7 15 C6.3 13.7 5.7 12.4 5 11 C4 11.3 3 11.7 2 12 C2.2 10.9 2.4 9.8 2.6 8.7 C3 5 3 5 2 2 C1.3 1.3 0.7 0.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(7,113)}] svg {M0 0 C0 3 0 3 -1.4 5.8 C-4.1 11.4 -4.4 16.1 -2.7 22 C-1.5 25.3 0.2 28.1 2 31 C-2.2 29.5 -3.8 26.8 -6 23 C-8.1 17.7 -7.4 12.4 -5.2 7.2 C-3.8 4.3 -2.4 2.2 0 0 Z };


## tool · 2026-11-10T09:57:33Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T09:57:38Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2012 4
\QuestionPage{3.1 定积分的概念、存在条件与性质}{选择题}{2012 年第 4 题}{1}{定积分比较}{130 / 408}
设$I_k = \int_0^{k\pi} \mathrm{e}^{x^{2}} \sin x\,\mathrm{d} x$（$k = 1,2,3$），则有\pickout{}
\begin{abcd}
\item $I_1 < I_2 < I_3$．
\item $I_3 < I_2 < I_1$．
\item $I_2 < I_3 < I_1$．
\item $I_2 < I_1 < I_3$．
\end{abcd}
\QuestionEnd
% Q 2018 5
\QuestionPage{3.1 定积分的概念、存在条件与性质}{选择题}{2018 年第 5 题}{1}{定积分估计与比较}{131 / 408}
设$M = \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \frac{\left(1 + x \right)^2}{1 + x^2}\,\mathrm{d} x$,
  $N = \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \frac{1 + x}{\mathrm{e}^x}\,\mathrm{d} x$,
  $K = \int_{-\frac{\pi}{2}}^{\frac{\pi}{2}} \left(1 + \sqrt{\cos x}\right)\,\mathrm{d} x$，
则\pickout{}
\begin{abcd}
\item $M > N > K$．
\item $M > K > N$．
\item $K > M > N$．
\item $K > N > M$．
\end{abcd}
\QuestionEnd
% Q 2021 7
\QuestionPage{3.1 定积分的概念、存在条件与性质}{选择题}{2021 年第 7 题}{1}{定积分与黎曼和}{132 / 408}
设函数 \(f(x)\) 在区间 \(\left[0,1\right]\) 上连续，则
\[\int_{0}^{1} f(x)\,\mathrm{d}x=
\]
\choices{\(\lim_{n \to \infty}\sum_{k=1}^{n} f\left(\dfrac{2k-1}{2n}\right)\dfrac{1}{2n}\)}{\(\lim_{n \to \infty}\sum_{k=1}^{n} f\left(\dfrac{2k-1}{2n}\right)\dfrac{1}{n}\)}{\(\lim_{n \to \infty}\sum_{k=1}^{2n} f\left(\dfrac{k-1}{2n}\right)\dfrac{1}{n}\)}{\(\lim_{n \to \infty}\sum_{k=1}^{2n} f\left(\dfrac{k}{2n}\right)\dfrac{2}{n}\)}
\QuestionEnd
% Q 2022 7
\QuestionPage{3.1 定积分的概念、存在条件与性质}{选择题}{2022 年第 7 题}{2}{比较定积分大小}{133 / 408}
若
\(I_{1} = \int_{0}^{1} \frac{x}{2\left( 1 + \cos x \right)} \mathrm{~d}x,\quad I_{2} = \int_{0}^{1} \frac{\ln\left( 1 + x \right)}{1 + \cos x} \mathrm{~d}x,\quad I_{3} = \int_{0}^{1} \frac{2x}{1 + \sin x} \mathrm{~d}x\)
则 \(\left( \ \right)\)
\choices{\(I_{1} < I_{2} < I_{3}\)}{\(I_{2} < I_{1} < I_{3}\)}{\(I_{1} < I_{3} < I_{2}\)}{\(I_{3} < I_{2} < I_{1}\)}
\QuestionEnd
% Q 2016 10
\QuestionPage{3.1 定积分的概念、存在条件与性质}{填空题}{2016 年第 10 题}{2}{三角和式极限}{134 / 408}
极限$\lim_{n \to \infty} \frac{1}{n^2}\left(\sin\frac{1}{n} + 2\sin\frac{2}{n}
+ \cdots + n\sin\frac{n}{n}\right) =$ \blank{}．
\QuestionEnd
% Q 2024 15
\QuestionPage{3.1 定积分的概念、存在条件与性质}{填空题}{2024 年第 15 题}{2}{速度的积分平均值}{135 / 408}
某物体以速度
\[v(t)=t+k\sin\pi t
\]
做直线运动。若它从 \(t=0\) 到 \(t=3\) 的平均速度是 \(\dfrac52\)，则 \(k=\) \blank{}
\QuestionEnd
% Q 2025 13
\QuestionPage{3.1 定积分的概念、存在条件与性质}{填空题}{2025 年第 13 题}{2}{和式极限与定积分定义}{136 / 408}
\(\lim_{n \to \infty} \frac{1}{n^{2}} \left[ \ln \frac{1}{n} + 2 \ln \frac{2}{n} + \cdots + \left( n - 1 \right) \ln \frac{n - 1}{n} \right] =\) \blank{}.
\QuestionEnd
% Q 2026 15
\QuestionPage{3.1 定积分的概念、存在条件与性质}{填空题}{2026 年第 15 题}{2}{函数的积分平均值}{137 / 408}
函数
\[f(x)=\ln(2+x)
\]
在区间 \([0,2]\) 上的平均值为 \blank{}.
\QuestionEnd
% Q 2010 16
\QuestionPage{3.1 定积分的概念、存在条件与性质}{解答题}{2010 年第 16 题}{2}{积分比较与数列极限}{138 / 408}
\begin{enumerate}
\item
比较$\int_0^1 |\ln t|[\ln(1+t)]^n\,\mathrm{d} t$
与$\int_0^1 t^n |\ln t|\,\mathrm{d} t$（$n=1,2,\cdots$）的大小，说明理由；
\item
记$u_n = \int_0^1 |\ln t|[\ln(1+t)]^n\,\mathrm{d} t$（$n=1,2,\cdots$），求极限$\lim_{n\to\infty} u_n$．
\end{enumerate}
\QuestionEnd
% Q 2014 19
\QuestionPage{3.1 定积分的概念、存在条件与性质}{解答题}{2014 年第 19 题}{3}{定积分保序与比较}{139 / 408}
设函数$f(x),g(x)$在区间$[a.b]$上连续，且$f(x)$单调增加，$0 \le g(x) \le 1$，证明：
\begin{enumerate}
\item $0 \le \int_a^x g(t)\,\mathrm{d} t \le x - a$，$x \in [a,b]$；
\item $\int_a^{a + \int_a^b g(t)\,\mathrm{d} t} f(x)\,\mathrm{d} x \le \int_a^b f(x)g(x)\,\mathrm{d} x$．
\end{enumerate}
\QuestionEnd
% Q 2020 20
\QuestionPage{3.1 定积分的概念、存在条件与性质}{解答题}{2020 年第 20 题}{3}{积分中值定理}{140 / 408}
设函数 \(f\left( x \right)=\int_{1}^{x}{e^{t^{2}} \mathrm{~d} t}\)。
\begin{enumerate}
\item 证明：存在 \(\xi \in \left( 1,2 \right)\)，使得 \(f\left( \xi \right)=\left( 2-\xi \right)e^{\xi^{2}}\)；
\item 证明：存在 \(\eta \in \left( 1,2 \right)\)，使得 \(f\left( 2 \right)=\ln 2 \cdot \eta e^{\eta^{2}}\)。
\end{enumerate}
\QuestionEnd
% Q 2009 6
\QuestionPage{3.2 微积分基本公式与基本定理}{选择题}{2009 年第 6 题}{1、2}{变上限积分的图像}{141 / 408}
设函数$y = f(x)$在区间$\left[- 1,3 \right]$上的图形为
\par\centerline{\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.439724,yscale=-0.439724]
\end{tikzpicture}}
则函数$F(x) = \int_0^x f(t)\,\mathrm{d} t$的图形为\pickout{}

\noindent
\graphchoice{A}{%
\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.290994,yscale=-0.290994]
\end{tikzpicture}
}
\hfill
\graphchoice{B}{%
\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.290994,yscale=-0.290994]
\end{tikzpicture}
}
\hfill
\graphchoice{C}{%
\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.290994,yscale=-0.290994]
\end{tikzpicture}
}
\hfill
\graphchoice{D}{%
\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.290994,yscale=-0.290994]
\end{tikzpicture}
}
\QuestionEnd
% Q 2013 3
\QuestionPage{3.2 微积分基本公式与基本定理}{选择题}{2013 年第 3 题}{1}{变上限积分的连续性与可导性}{142 / 408}
设函数$f(x) = \begin{cases}
  \sin x, & 0 \le x < \pi , \\
       2, & \pi \le x \le 2\pi ,
\end{cases}$ $F(x) = \int_0^x f(t) \,\mathrm{d} t$，则\pickout{}
\begin{abcd}
\item $x = \pi$是函数$F(x)$的跳跃间断点．
\item $x = \pi$是函数$F(x)$的可去间断点．
\item $F(x)$在$x = \pi$处连续但不可导．
\item $F(x)$在$x = \pi$处可导．
\end{abcd}
\QuestionEnd
% Q 2016 2
\QuestionPage{3.2 微积分基本公式与基本定理}{选择题}{2016 年第 2 题}{1}{分段函数的原函数}{143 / 408}
已知函数$f(x) = \begin{cases}
  2(x - 1), & x < 1, \\
     \ln x, & x \ge 1,
\end{cases}$，则$f(x)$的一个原函数是\pickout{}
\begin{abcd}
\item $F(x) = \begin{cases}
                 (x - 1)^2, & x < 1 \\
  x\left(\ln x - 1 \right), & x \ge 1
\end{cases}$．
\item $F(x) = \begin{cases}
                     (x - 1)^2, & x < 1 \\
  x\left(\ln x + 1 \right) - 1, & x \ge 1
\end{cases}$．
\item $F(x) = \begin{cases}
                     (x - 1)^2, & x < 1 \\
  x\left(\ln x + 1 \right) + 1, & x \ge 1
\end{cases}$．
\item $F(x) = \begin{cases}
                     (x - 1)^2, & x < 1 \\
  x\left(\ln x - 1 \right) + 1, & x \ge 1
\end{cases}$．
\end{abcd}
\QuestionEnd
% Q 2023 2
\QuestionPage{3.2 微积分基本公式与基本定理}{选择题}{2023 年第 2 题}{1}{分段函数的原函数}{144 / 408}
函数
\[f(x)=
\begin{cases}
\dfrac{1}{\sqrt{1+x^2}}, & x\le 0,\\[0.6em]
(x+1)\cos x, & x>0
\end{cases}
\]
的一个原函数为（ ）。
\twochoices{\(F(x)=
\begin{cases}
\ln\left(\sqrt{1+x^2}-x\right), & x\le 0,\\
(x+1)\cos x-\sin x, & x>0
\end{cases}
\)}{\(F(x)=
\begin{cases}
\ln\left(\sqrt{1+x^2}-x\right)+1, & x\le 0,\\
(x+1)\cos x-\sin x, & x>0
\end{cases}
\)}{\(F(x)=
\begin{cases}
\ln\left(\sqrt{1+x^2}+x\right), & x\le 0,\\
(x+1)\sin x+\cos x, & x>0
\end{cases}
\)}{\(F(x)=
\begin{cases}
\ln\left(\sqrt{1+x^2}+x\right)+1, & x\le 0,\\
(x+1)\sin x+\cos x, & x>0
\end{cases}
\)}
\QuestionEnd
% Q 2015 11
\QuestionPage{3.2 微积分基本公式与基本定理}{填空题}{2015 年第 11 题}{2}{变上限积分求导}{145 / 408}
设$f(x)$连续，$\varphi (x) = \int_0^{x^2} x f(t)\,\mathrm{d} t$，
若$\varphi (1) = 1$，$\varphi'(1) = 5$，则$f(1) =$ \blank{}．
\QuestionEnd
% Q 2016 12
\QuestionPage{3.2 微积分基本公式与基本定理}{填空题}{2016 年第 12 题}{2}{变上限积分与高阶导数}{146 / 408}
已知函数$f(x)$在$(-\infty,+\infty)$上连续，且$f(x) = (x + 1)^2 + 2\int_0^x f(t) \,\mathrm{d} t$，
则当$n \ge 2$时，$f^{(n)}(0) =$ \blank{}．
\QuestionEnd
% Q 2023 15
\QuestionPage{3.2 微积分基本公式与基本定理}{填空题}{2023 年第 15 题}{2}{积分关系求函数值}{147 / 408}
设连续函数 \(f(x)\) 满足
\[f(x+2)-f(x)=x,\qquad \int_0^2 f(x)\,dx=0,
\]
则
\[\int_1^3 f(x)\,dx=\blank{}.
\]
\QuestionEnd
% Q 2016 21
\QuestionPage{3.2 微积分基本公式与基本定理}{解答题}{2016 年第 21 题}{4}{原函数、平均值与零点}{148 / 408}
已知$f(x)$在$\left[0,\frac{3\pi}{2} \right]$上连续，
在$\left(0,\frac{3\pi}{2} \right)$内是函数$\frac{\cos x}{2x - 3\pi}$的一个原函数$f(0) = 0$．
\begin{enumerate}
\item 求$f(x)$在区间$\left[0,\frac{3\pi}{2} \right]$上的平均值；
\item 证明$f(x)$在区间$\left(0,\frac{3\pi}{2} \right)$内存在唯一零点．
\end{enumerate}
\QuestionEnd
% Q 2018 16
\QuestionPage{3.2 微积分基本公式与基本定理}{解答题}{2018 年第 16 题}{2}{变上限积分与平均值}{149 / 408}
已知连续函数$f(x)$满足$\int_0^x f(t)\,\mathrm{d} t + \int_0^x tf(x - t)\,\mathrm{d} t = ax^2$．
\begin{enumerate}
\item 求$f(x)$；
\item 若$f(x)$在区间$[0,1]$上的平均值为$1$，求$a$的值．
\end{enumerate}
\QuestionEnd
% Q 2020 16
\QuestionPage{3.2 微积分基本公式与基本定理}{解答题}{2020 年第 16 题}{2}{变上限积分求导与连续性}{150 / 408}
已知函数 \(f\left( x \right)\) 连续且 \(\lim\limits_{x\to 0}{\dfrac{f\left( x \right)}{x}} = 1\)，\(g\left( x \right)=\int_{0}^{1}{f\left( xt \right) \mathrm{~d} t}\)，求 \(g^{\prime}\left( x \right)\)，并证明 \(g^{\prime}\left( x \right)\) 在 \(x=0\) 处连续。
\QuestionEnd
% Q 2026 18
\QuestionPage{3.2 微积分基本公式与基本定理}{解答题}{2026 年第 18 题}{2}{变上限积分的导数与连续性}{151 / 408}
（本题满分 12 分）
已知函数 \(g(x)\) 连续.设
\[f(x)=\int_0^{x^2} g(xt)\,dt,
\]
求 \(f'(x)\) 的表达式，并判断 \(f'(x)\) 在 \(x=0\) 处的连续性.
\QuestionEnd
% Q 2011 6
\QuestionPage{3.3 两种基本积分法}{选择题}{2011 年第 6 题}{1}{定积分的对称换元}{152 / 408}
设$I = \int_{0}^{\frac{\pi}{4}}\ln\sin x\,\mathrm{d} x$，$J = \int_{0}^{\frac{\pi}{4}}\ln\cot x\,\mathrm{d} x$，
$K = \int_{0}^{\frac{\pi}{4}}\ln\cos x\,\mathrm{d} x$，则$I,\;J,\;K$的大小关系是\pickout{}
\begin{abcd}
\item $I < J < K$．
\item $I < K < J$．
\item $J < I < K$．
\item $K < J < I$．
\end{abcd}
\QuestionEnd
% Q 2020 3
\QuestionPage{3.3 两种基本积分法}{选择题}{2020 年第 3 题}{1}{反三角函数的换元积分}{153 / 408}
\(\int_{0}^{1}{\dfrac{\arcsin \sqrt{x}}{\sqrt{x\left( 1-x \right)}} \mathrm{~d} x} =\)
\choices{\(\dfrac{\pi^{2}}{4}\)}{\(\dfrac{\pi^{2}}{8}\)}{\(\dfrac{\pi}{4}\)}{\(\dfrac{\pi}{8}\)}
\QuestionEnd
2009数二真题【解析】.md
2010数二真题【解析】.md
2011数二真题【解析】.md
2012数二真题【解析】.md
2013数二真题【解析】.md
2014数二真题【解析】.md
2015数二真题【解析】.md
2016数二真题【解析】.md
2017数二真题【解析】.md
2018数二真题【解析】.md
2019数二真题【解析】.md
2020数二真题【解析】.md
2021数二真题【解析】.md
2022数二真题【解析】.md
2023数二真题【解析】.md
2024数二真题【解析】.md
2025数二真题【解析】.md
2026年数学二真题及答案.md
2026考研数学（二）真题试卷及解析.md


## tool · 2026-11-10T09:57:42Z


Script completed
Wall time 0.1 seconds
Output:

403-## PDF 第 7 页
404-
405-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2009%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=7) · 本机 OCR
406-
407-```text
408-系，结合曲率计算公式K=
409-［1+（g'）2］号
410-率半径为 2），可计算得 "（1）=2.再由 ”＜0可知 （1）= 2.
411-台（这是因为曲
412:改函数 =f（x）在区间L-1，3」上的图形如图所不，则函数
413:F（x） =f（t）dt的图形为（
414-）
415-AF（x）
416-AF（x）
417-418）
418-（A）
419-（B）
420--1
421-23
422-F（x）
423-½N⑦2 328
424-F（x）
425-（C）
426-（D）
427--1
428-答案
429-D.
430-分析
431:本题主要考查对变上限积分函数的理解.
432-若f（x）在区间［a,b］上可积，则积分上限的函数F（x） ）d在［a，6］上连续.
433-若f（x）在区间［a，b］上连续，则积分上限的函数P（z）=「Kt）d在［a，6.］上可导，且导数为
434-当 为左（右）端点时，可导指右（左）可导，F'（x）应为F！（x）（F！（x））
435-f（x）是一个分段连续函数，我们可以通过计算f（x）的定积分得到F（x）在某些特殊点的值，从
436-而借助排除法得到结果.
437-解（法一）我们可以从f（x）出发具体分析F（x）的性质.
438:因为f（x）分段连续，所以由变上限积分函数的性质可知，在［-1,0），（0,2），（2，3］上，均
439-有F'（x）=f（x）.
440-① 由于f（x）在［-1,3］上有界且只有两个间断点，故f（x）可积、又因为F（x）= t）d，所
441-以F（x）连续
442-② 在［-1,0）上，f（x）>0，故F（x）单调增加；在（0， 1）上，f（x）<0，故F（x）单调减少；在
443-（1, 2）上，f（x）>0，故F（x）单调增加；在（2，3］上，f（x）=0，故F（x）为常函数.
444-③F（O）= e）d=0.在［-1,11上，F（x）均小于等于零，
445-一10—
446-```
447-
448-## PDF 第 8 页
449-
450-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2009%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=8) · 本机 OCR
451-
452-> 读取原 PDF 时出现警告，建议核对原页。
453-
454-```text
455-④f（1）= 0,x=1为F（x）的驻点及极小值点.
456:同时满足以上要求的图形只有选项D.应选 D.
457:（法二）通过图形考察f（x）在［-1，0）上的性质，可知当* E［-1,0）时，f（x）=1，故
458-F（-1） =
459-1dx =-1，
460-F（O） =51dx=0，
461-从而可排除选项 A 和选项C.
462-又由于f（x）在［-1，3］上有界且只有两个间断点，f（x）在［-1，3］上可积，而F（x）=
463-lrc）d，故F（x）必连续，从而可以排除选项B.
464-综上所述，应选 D.
465-注 也许在解图像题时，有些同学会把积分值与“面积”相联系，将非负函数在区间
466-［a,6］上的积分值对应该函数图像与x= a，x =6以及x轴围成的面积（面积始终是正
467-值），与F（x）的含义（F（x）可能为负值）混淆.
468:F（x）=ft）de是一个变上限积分，也就是说，它的上限x是变动的，可能大于零，也可
469-能小于零.若f（t）非负，则当x>0时，F（x）>0,F（x）的值对应面积；当x<0时，F（x）的
470-值对应的是面积的负值.
471-O
472-B
473-A
474-设A，B均为2阶方阵，A’，B*分别为A，B的伴随矩阵.若|A|-=2，1B|=3，则分块矩阵
475-的伴随矩阵为（）
476-3B*
477-O
\textbf{入手角度}\quad 用拉格朗日中值定理把相邻割线斜率化为导数值，反向用割线趋于切线。

\textbf{解析}\quad 若 \(f'\) 严格递增，任取 \(x_1<x_2<x_3\)，两段割线的斜率分别是 \(f'(\xi_1),f'(\xi_2)\)，其中 \(x_1<\xi_1<x_2<\xi_2<x_3\)，故前者严格小于后者。

反之，固定任意 \(u<v\)。分别把条件用在 \(u-\varepsilon<u<v\) 与 \(u<v<v+\varepsilon\)，再令 \(\varepsilon\to0^+\)，得
\[
f'(u)\le\frac{f(v)-f(u)}{v-u}\le f'(v).
\]
所以 \(f'\) 非减。若某对 \(u<v\) 满足 \(f'(u)=f'(v)\)，则 \(f'\) 在 \([u,v]\) 上为常数。由中值定理，区间内任意两点间的割线斜率均相等，这与条件中的严格不等式矛盾。因此 \(f'\) 严格递增。



## tool · 2026-11-10T09:57:54Z




## assistant · 2026-11-10T09:57:57Z

第 114–129 题的推导已写入中间稿。2009 年第 6 题的图像选项已用配套解析复核，选 D。

## tool · 2026-11-10T09:59:50Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T09:59:56Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2009 11
\QuestionPage{3.3 两种基本积分法}{填空题}{2009 年第 11 题}{2}{含参数积分与分部积分}{154 / 408}
$\lim_{n \to \infty} \int_{0}^{1} \mathrm{e}^{- x}\sin nx\,\mathrm{d} x =$ \blank{}．
\QuestionEnd
% Q 2017 11
\QuestionPage{3.3 两种基本积分法}{填空题}{2017 年第 11 题}{2}{定积分计算}{155 / 408}
$\int_0^{+\infty} \frac{\ln(1 + x)}{(1 + x)^2}\,\mathrm{d} x =$ \blank{}．
\QuestionEnd
% Q 2017 13
\QuestionPage{3.3 两种基本积分法}{填空题}{2017 年第 13 题}{2}{三角函数的定积分}{156 / 408}
$\int_0^1 \,\mathrm{d} y \int_y^1 \frac{\tan x}{x}\,\mathrm{d} x =$ \blank{}．
\QuestionEnd
% Q 2018 11
\QuestionPage{3.3 两种基本积分法}{填空题}{2018 年第 11 题}{2}{有理函数的积分}{157 / 408}
$\int_5^{+\infty} \frac{1}{x^2 - 4x + 3}\,\mathrm{d} x =$ \blank{}．
\QuestionEnd
% Q 2022 13
\QuestionPage{3.3 两种基本积分法}{填空题}{2022 年第 13 题}{2}{有理函数的定积分}{158 / 408}
\(\int_{0}^{1} \frac{2x + 3}{x^{2} - x + 1} \mathrm{~d}x = \blank{}\)
\QuestionEnd
% Q 2009 16
\QuestionPage{3.3 两种基本积分法}{解答题}{2009 年第 16 题}{3}{对数函数的不定积分}{159 / 408}
计算不定积分$\int \ln \left(1 + \sqrt{\frac{1 + x}{x}} \right)\,\mathrm{d} x$（$x > 0$）．
\QuestionEnd
% Q 2017 17
\QuestionPage{3.3 两种基本积分法}{解答题}{2017 年第 17 题}{3}{不定积分计算}{160 / 408}
求$\lim_{n \to \infty} \sum_{k = 1}^n \frac{k}{n^2} \ln \left(1 + \frac{k}{n} \right)$．
\QuestionEnd
% Q 2018 15
\QuestionPage{3.3 两种基本积分法}{解答题}{2018 年第 15 题}{2}{换元与分部积分}{161 / 408}
求不定积分$\int \mathrm{e}^{2x}\arctan \sqrt{\mathrm{e}^x - 1} \,\mathrm{d} x$．
\QuestionEnd
% Q 2019 16
\QuestionPage{3.3 两种基本积分法}{解答题}{2019 年第 16 题}{2}{不定积分计算}{162 / 408}
求不定积分$\int \frac{3x + 6}{(x - 1)^2(x^2 + x + 1)}\,\mathrm{d} x$．
\QuestionEnd
% Q 2025 17
\QuestionPage{3.3 两种基本积分法}{解答题}{2025 年第 17 题}{3}{定积分计算}{163 / 408}
（本题满分 10 分）
计算 \(\int_{0}^{1} \frac{1}{\left( x + 1 \right)\left( x^{2} - 2x + 2 \right)} \mathrm{~d} x\).
\QuestionEnd
% Q 2017 6
\QuestionPage{3.4 定积分的应用}{选择题}{2017 年第 6 题}{1}{速度图像与追及距离}{164 / 408}
甲、乙两人赛跑，计时开始时，甲在乙前方$10$（单位：m）处，
图中实线表示甲的速度曲线$v = v_1(t)$（单位：m/s），虚线表示乙的速度$v = v_2(t)$，
三块阴影部分面积的数值依次为$10$、$20$、$3$，计时开始后乙追上甲的时刻记为$t_0$（单位：s），
则\pickout{}
\par\centerline{\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.439724,yscale=-0.439724]
\end{tikzpicture}}
\begin{abcd}
\item $t_0 = 10$．
\item $15 < t_0 < 20$．
\item $t_0 = 25$．
\item $t_0 > 25$．
\end{abcd}
\QuestionEnd
% Q 2025 6
\QuestionPage{3.4 定积分的应用}{选择题}{2025 年第 6 题}{1}{克服引力做功}{165 / 408}
设单位质点 \(P\)，\(Q\) 分别位于点 \(\left( 0, 0 \right)\) 和 \(\left( 0, 1 \right)\) 处，\(P\) 从点 \(\left( 0, 0 \right)\) 出发沿 \(x\) 轴正向移动，记 \(G\) 为引力常量，则当质点 \(P\) 移动到点 \(\left( 1, 0 \right)\) 时，克服质点 \(Q\) 的引力所做的功为
\choices{\(\int_{0}^{1} \frac{G}{x^{2} + 1} \mathrm{~d} x\)}{\(\int_{0}^{1} \frac{Gx}{\left( x^{2} + 1 \right)^{\frac{3}{2}}} \mathrm{~d} x\)}{\(\int_{0}^{1} \frac{G}{\left( x^{2} + 1 \right)^{\frac{3}{2}}} \mathrm{~d} x\)}{\(\int_{0}^{1} \frac{G\left( x + 1 \right)}{\left( x^{2} + 1 \right)^{\frac{3}{2}}} \mathrm{~d} x\)}
\QuestionEnd
% Q 2026 4
\QuestionPage{3.4 定积分的应用}{选择题}{2026 年第 4 题}{1}{连续分布质点的引力}{166 / 408}
设线密度为 \(1\) 的细直棒两端点分别位于 \((-1,0)\) 和 \((1,0)\)，质量为 \(m\) 的质点位于 \((0,1)\)，\(G\) 为引力常量，则该细直棒对该质点的引力大小为
\choices{\(\displaystyle \int_0^1 \frac{2Gmx}{(x^2+1)^{1/2}}\,dx\)}{\(\displaystyle \int_0^1 \frac{2Gm}{(x^2+1)^{1/2}}\,dx\)}{\(\displaystyle \int_0^1 \frac{2Gmx}{(x^2+1)^{3/2}}\,dx\)}{\(\displaystyle \int_0^1 \frac{2Gm}{(x^2+1)^{3/2}}\,dx\)}
\QuestionEnd
% Q 2010 12
\QuestionPage{3.4 定积分的应用}{填空题}{2010 年第 12 题}{2}{极坐标曲线弧长}{167 / 408}
当$0 \le \theta \le \pi$时，对数螺线$r = \mathrm{e}^{\theta}$的弧长为 \blank{}．
\QuestionEnd
% Q 2011 11
\QuestionPage{3.4 定积分的应用}{填空题}{2011 年第 11 题}{1}{平面曲线弧长}{168 / 408}
曲线$y = \int_0^x \tan t\,\mathrm{d} t$（$0 \le x \le \frac{\pi}{4}$）的弧长$s =$ \blank{}．
\QuestionEnd
% Q 2013 11
\QuestionPage{3.4 定积分的应用}{填空题}{2013 年第 11 题}{2}{极坐标曲线围成的面积}{169 / 408}
设封闭曲线$L$的极坐标方程为$r = \cos 3\theta$（$- \frac{\pi}{6} \le \theta \le \frac{\pi}{6}$），
则$L$所围成的平面图形的面积为 \blank{}．
\QuestionEnd
% Q 2014 13
\QuestionPage{3.4 定积分的应用}{填空题}{2014 年第 13 题}{2}{细棒的质心}{170 / 408}
一根长为$1$的细棒位于$x$轴的区间$[0,1]$上，若其线密度$\rho (x) = - x^2 + 2x + 1$，
则该细棒的质心坐标$\overline{x} =$ \blank{}．
\QuestionEnd
% Q 2019 12
\QuestionPage{3.4 定积分的应用}{填空题}{2019 年第 12 题}{2}{对数曲线的弧长}{171 / 408}
曲线$y = \ln \cos x$（$0 \le x \le \frac{\pi}{6}$）的弧长为 \blank{}．
\QuestionEnd
% Q 2020 12
\QuestionPage{3.4 定积分的应用}{填空题}{2020 年第 12 题}{2}{水压力的微元法}{172 / 408}
斜边长为 \(2a\) 的等腰直角三角形平板铅直地沉没在水中，且斜边与水面相齐。记重力加速度为 \(g\)，水的密度为 \(\rho\)，则该平板一侧所受的水压力为
\blank{}
\QuestionEnd
% Q 2022 15
\QuestionPage{3.4 定积分的应用}{填空题}{2022 年第 15 题}{2}{极坐标曲线围成的面积}{173 / 408}
已知曲线 \(L\) 的极坐标方程为
\(r = \sin 3\theta \quad \left( 0 \le \theta \le \frac{\pi}{3} \right)\)
则 \(L\) 围成的有界区域的面积为 \(\blank{}\)
\QuestionEnd
% Q 2023 12
\QuestionPage{3.4 定积分的应用}{填空题}{2023 年第 12 题}{2}{由积分表示的曲线弧长}{174 / 408}
曲线
\[y=\int_{-\sqrt3}^{x}\sqrt{3-t^2}\,dt
\]
的弧长为
\[\blank{}.
\]
\QuestionEnd
% Q 2010 18
\QuestionPage{3.4 定积分的应用}{解答题}{2010 年第 18 题}{3}{液体质量的积分模型}{175 / 408}
一个高为$l$的柱体形贮油罐，底面是长轴为$2a$，短轴为$2b$的椭圆．
现将贮油罐平放，当油罐中油面高度为$\frac{3}{2}b$时（如图），计算油的质量．
\par\centerline{\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.439724,yscale=-0.439724]
\end{tikzpicture}}
（长度单位为$\text{m}$，质量单位为$\text{kg}$，油的密度为常数$\rho\text{kg/m}^3$）
\QuestionEnd
% Q 2011 20
\QuestionPage{3.4 定积分的应用}{解答题}{2011 年第 20 题}{3}{旋转体容积与抽水做功}{176 / 408}
一容器的内侧是由图中曲线绕$y$轴旋转一周而成的曲面，
该曲线由$x^2 + y^2 = 2y$（$y \ge \frac{1}{2}$）与$x^2 + y^2 = 1$（$y \le \frac{1}{2}$）连接而成．
\par\centerline{\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.439724,yscale=-0.439724]
\end{tikzpicture}}
\begin{enumerate}
\item 求容器的容积；
\item 若将容器内盛满的水从容器顶部全部抽出，至少需要做多少功？
\end{enumerate}
（长度单位：$\text{m}$，重力加速度为$g\text{m/s}^2$，水的密度为$10^3\text{kg/m}^3$．）
\QuestionEnd
% Q 2012 17
\QuestionPage{3.4 定积分的应用}{解答题}{2012 年第 17 题}{2}{切线围成的面积与旋转体积}{177 / 408}
过$(0,1)$点作曲线$L:\;y = \ln x$的切线，切点为$A$，又$L$与$x$轴交于$B$点，区域$D$由$L$与直线$AB$围成，
求区域$D$的面积及$D$绕$x$轴旋转一周所得旋转体的体积．
\QuestionEnd
% Q 2013 16
\QuestionPage{3.4 定积分的应用}{解答题}{2013 年第 16 题}{2}{两个旋转体的体积关系}{178 / 408}
设$D$是由曲线$y = x^{\frac{1}{3}}$，直线$x = a$（$a > 0$）及$x$轴所围成的平面图形，
$V_x$，$V_y$分别是$D$绕$x$轴，$y$轴旋转一周所得旋转体的体积，若$V_y = 10V_x$，求$a$的值．
\QuestionEnd
\textbf{解析}\quad 由 \(x=\sin^2u\) 得 \(\mathrm{d}x=2\sin u\cos u\,\mathrm{d}u\)，而 \(\sqrt{x(1-x)}=\sin u\cos u\)（\(0<u<\pi/2\)）。在内区间换元再取端点极限，原积分化为
\[
2\int_0^{\pi/2}u\,\mathrm{d}u=\frac{\pi^2}{4},
\]
故选 A。




## tool · 2026-11-10T10:00:00Z


Script completed
Wall time 0.1 seconds
Output:

302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1008-p=el+［B3（t+1）elad+C］= （t+1）（3t+C），
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1009-其中C为待定常数.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1010-由女（1）=6得，p（1）=2（3+C）=6，得C=0.从而 （ ） 3 ＋3 。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1011-对 （t）积分，得
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1012-代入少（1）=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1013-之，得C'=0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1014-因此，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1015-山（t= +一
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1016-2 （ >-1）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md:1017:18 一个高为1的柱体形贮油罐，底面是长轴为2a，短轴为26的
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md:1018:椭圆.现将贮油罐平放，当油罐中油面高度》-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1019-时（如图），计算油的
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1020-质量.（长度单位m，质量单位力kg，油的密度为常量p，单位
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1021-力kg/m？）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1022-2a
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1023-分析本题是一道应用题，实际上考查求平面区域面积.平面区域为椭圆的一部分，可以利
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1024-用定积分计算其面积，也可以利用二重积分计算其面积，下面我们给出两种不同的解法，请大家比
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1025-较它们的区别.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md:1026:解以贮油罐的底面中心为原点，*轴方向平行于地面方向建立直角坐标系xOy，则平放时贮
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md:1027:油罐底面所对应的椭圆方程为”
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1028-2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1029-Q
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1030-B2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1031-= 1.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md:1032:由于油的密度为常量，贮油罐为柱体，故油的质量m=pV =pLS，其中1为柱体的高，S为底面油
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1033-面的面积.因此，要求油的质量，只需求出平放时油面的面积S.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1034-设油面所占区域为D. 下面用两种方法来求D的面积.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1035-（法一）利用定积分计算区域D的面积.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1036-记D'为D在x≥0的半平面上的部分.由于区域D关于y轴对
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1037-點+水
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1038-A
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1039-D
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1040-称，故D的面积是D’的面积的2倍.如图所示， ’ ，其中 ！
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md-1041--0
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-288-P1.0）-f（0.0） =9（2.g2）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-289-•1>0,f（0,1）-f（0.0）=9 ，2）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-290-•1 <0，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-291-x= ，y=0
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-292-×=0,y=n
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-293-其中0<<1,0≤n≤1.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-294-甲，乙两人赛跑，计时开始时，甲在乙前方10（单位：m）处，图中，实线表示甲的速度曲线
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-295-=2」（t）（单位：m s），虚线表示乙的速度曲线 = （t），三块
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-296-A v（m/s）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md:297:阴影部分面积的数值依次为10,20，3.计时开始后乙追上甲的
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-298-时刻记为t。（单位：s），则（
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-299-）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-300-（A）to=10.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-301-（C）to = 25.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-302-（B）15 <to <20.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-303-（D）to >25.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-304-答案
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-305-O
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-306-5
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-310-25
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-311-30~t（S）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-312-分析本题主要考查定积分的物理意义，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-313-根据定积分的物理意义，速度曲线2=2（t）与t=a，t =6以及t轴所围成的区域面积为时刻
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-314-a 到时刻6这段时间内所跑过的路程.两条速度曲线所围成的区域面积为路程差的绝对值.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-315-解）根据定积分的物理意义，从0s到10s这段时间内，实线位于虚线之上，于是甲跑过的路
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-316-程比乙跑过的路程多10m；从10s到25s这段时间内，虚线位于实线之上，于是乙跑过的路程比甲
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-317-跑过的路程多20 m.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-318-由于在计时开始时，甲领先乙10m，故到25s时，甲与乙之间的距离为10+10-20=0（m），即
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md:319:乙追上甲.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-320-因此，应选 C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-321-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-322-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-323-## PDF 第 7 页
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-324-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-325-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-326-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-327-> 读取原 PDF 时出现警告，建议核对原页。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md-328-
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1180-= In（1+
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1181--|
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1182-，是因为，通过计算发现，当×=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1183-'1+X
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1184-1 +n’
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1185-1+n
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1186-20
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1187-一容器的内侧是由图中曲线绕y轴旋转一周而成的曲面，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1188-（I）求容器的容积；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md:1189:（II）若将容器内盛满的水从容器顶部全部抽出，至少需要做
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1190-多少功？
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1191-（长度单位：m，重力加速度为gm/s’，水的密度为10°kg/m2）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1192-分析本题主要考查旋转体的体积的计算以及变力做功问
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1193-题.这两个问题都是定积分的应用.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1194-第（I）问求旋转体的体积，可利用旋转体体积的计算公式.解决第（I）问中变力做功问题的
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1195-关键是正确写出做功的微元.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1196-×2+y=2y
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1197-：y=2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1198-dy
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1199-D，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1200-X
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1201-O
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1202-D
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1203-x2+y2=1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1204--T
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1205-（b）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md:1206:解）（I）如图（a）所示，旋转体可看作由图中阴影区域绕y轴旋转一周所得，由两部分组成，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1207-V =V+V.V，是由区域D，绕y轴旋转而成的旋转体的体积，½是由区域D，绕y轴旋转而成的旋
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1208-转体的体积.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1209-线可取为x =V2y ，1日1 ：2」
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1210-因此，该容器的容积为2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1211--（m’）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1212-一23-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1213-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1214-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1215-## PDF 第 21 页
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1216-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1217-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1218-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1219-> 读取原 PDF 时出现警告，建议核对原页。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1220-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1221-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md:1222:（I）用元素法，取图（b）中阴影部分的小薄片为做功的元素.该小薄片近似于高为dy的圆柱
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1223-为r（y）=v2 -g.小薄片提升的高度近似为2-夕，克服该小薄片形状的水的重力所做功为
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1224-dW = pgr［r（y）］（2 -y）dy.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1225-因此，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1226-W=J.pgT［r（y）］'（2-ydy=pg™LJ！
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1227--」（1 ）（2-ydy +（2 -g）（2-y）dy-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1228-由于
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1229-故
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1230-= PET（4g*-4g -9g +19g）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md-1231-27
/usr/bin/python3


## tool · 2026-11-10T10:00:25Z




## assistant · 2026-11-10T10:00:28Z

第 130–153 题的推导已完成。我也核对了赛跑题的阴影区间和符号，乙在 25 秒时首次追上甲。

## tool · 2026-11-10T10:02:22Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:02:28Z


Script completed
Wall time 0.1 seconds
Output:

% SOLUTION 149 2018 16
% SOLUTION 150 2020 16
% SOLUTION 151 2026 18
% SOLUTION 152 2011 6
% SOLUTION 153 2020 3
% SOLUTION 154 2009 11
% SOLUTION 155 2017 11
% SOLUTION 156 2017 13
% SOLUTION 157 2018 11
% SOLUTION 158 2022 13
% SOLUTION 159 2009 16
% SOLUTION 160 2017 17
% SOLUTION 161 2018 15
% SOLUTION 162 2019 16
% SOLUTION 163 2025 17
% SOLUTION 164 2017 6
% SOLUTION 165 2025 6
% SOLUTION 166 2026 4
% SOLUTION 167 2010 12
% SOLUTION 168 2011 11
% SOLUTION 169 2013 11
% SOLUTION 170 2014 13
% SOLUTION 171 2019 12
% SOLUTION 172 2020 12
% SOLUTION 173 2022 15
% SOLUTION 174 2023 12
% SOLUTION 175 2010 18
% SOLUTION 176 2011 20
% SOLUTION 177 2012 17
% SOLUTION 178 2013 16
% Q 2013 21
\QuestionPage{3.4 定积分的应用}{解答题}{2013 年第 21 题}{4}{弧长与平面图形的形心}{179 / 408}
设曲线$L$的方程为$y = \frac{1}{4}x^2 - \frac{1}{2}\ln x$（$1 \le x \le \mathrm{e}$）．
\begin{enumerate}
\item 求$L$的弧长；
\item 设$D$是由曲线$L$，直线$x = 1,x = \mathrm{e}$及$x$轴所围平面图形，求$D$的形心的横坐标．
\end{enumerate}
\QuestionEnd
% Q 2014 20
\QuestionPage{3.4 定积分的应用}{解答题}{2014 年第 20 题}{3}{递推函数围成的面积}{180 / 408}
设函数$f(x) = \frac{x}{1 + x}$，$x \in [0,1]$．定义函数列
\[
f_1(x) = f(x),\quad f_2(x) = f(f_1(x)),\quad \cdots,\quad f_n(x) = f(f_{n - 1}(x)), \cdots
\]
设$S_n$是曲线$y = f_n(x)$，直线$x = 1$, $y = 0$所围平面图形的面积．求极限$\lim_{n \to \infty} nS_n$．
\QuestionEnd
% Q 2015 16
\QuestionPage{3.4 定积分的应用}{解答题}{2015 年第 16 题}{2}{旋转体积的比值}{181 / 408}
设$A > 0$，$D$是由曲线段$y = A\sin x$（$0 \le x \le \frac{\pi}{2}$）
及直线$y = 0$，$x = \frac{\pi}{2}$所围成的平面区域，
$V_1$，$V_2$分别表示$D$绕$x$轴与绕$y$轴旋转成旋转体的体积，若$V_1 = V_2$，求$A$的值．
\QuestionEnd
% Q 2016 20
\QuestionPage{3.4 定积分的应用}{解答题}{2016 年第 20 题}{3}{旋转体积和表面积}{182 / 408}
设$D$是由曲线$y = \sqrt{1 - x^2}$（$0 \le x \le 1$）与$\begin{cases}
  x = \cos^3 t \\
  y = \sin^3 t
\end{cases}$（$0 \le t \le \frac{\pi}{2}$）围成的平面区域，求$D$绕$x$轴旋转一周所得旋转体的体积和表面积．
\QuestionEnd
% Q 2019 19
\QuestionPage{3.4 定积分的应用}{解答题}{2019 年第 19 题}{3}{分段面积与极限}{183 / 408}
设$n$是正整数，记$S_n$为曲线$y = \mathrm{e}^{- x}\sin x$（$0 \le x \le n\pi$）
与$x$轴所围成图形的面积，求$S_n$，并求$\lim_{n \to \infty} S_n$．
\QuestionEnd
% Q 2020 18
\QuestionPage{3.4 定积分的应用}{解答题}{2020 年第 18 题}{3}{函数关系与旋转体积}{184 / 408}
设函数 \(f\left( x \right)\) 的定义域为 \(\left( 0,+\infty \right)\) 且满足
\[2f\left( x \right)+x^{2}f\left( \dfrac{1}{x} \right)=\dfrac{x^{2}+2x}{\sqrt{1+x^{2}}}
\]
求 \(f\left( x \right)\)，并求曲线 \(y=f\left( x \right)\)，\(y=\dfrac{1}{2}\)，\(y=\dfrac{\sqrt{3}}{2}\) 及 \(y\) 轴所围图形绕 \(x\) 轴旋转所成旋转体的体积。
\QuestionEnd
% Q 2021 19
\QuestionPage{3.4 定积分的应用}{解答题}{2021 年第 19 题}{3}{弧长与旋转曲面面积}{185 / 408}
\(f(x)\) 满足
\[\int \frac{f(x)}{\sqrt{x}} \,\mathrm{d}x=\frac{1}{6}x^{2}-x+C,
\]
\(L\) 为曲线 \(y=f(x)\)，其中 \(4 \le x \le 9\)。\(L\) 的弧长为 \(s\)，\(L\) 绕 \(x\) 轴旋转一周所形成的曲面的面积为 \(A\)，求 \(s\) 和 \(A\)。
\QuestionEnd
% Q 2023 19
\QuestionPage{3.4 定积分的应用}{解答题}{2023 年第 19 题}{3}{无界区域的面积与旋转体积}{186 / 408}
已知平面区域
\[D=\left\{(x,y)\mid 0\le y\le \frac{1}{x\sqrt{1+x^2}},\ x\ge 1\right\}.
\]
\begin{enumerate}
\item 求 \(D\) 的面积；
\item 求 \(D\) 绕 \(x\) 轴旋转所成旋转体的体积。
\end{enumerate}
\QuestionEnd
% Q 2024 19
\QuestionPage{3.4 定积分的应用}{解答题}{2024 年第 19 题}{3}{旋转体积及其最大值}{187 / 408}
设 \(t>0\)，曲线
\[y=\sqrt{x}e^{-x}
\]
与直线 \(x=t,\ x=2t\) 及 \(x\) 轴所围平面图形绕 \(x\) 轴旋转所得的旋转体体积为 \(V(t)\)，求 \(V(t)\) 的最大值。
\QuestionEnd
% Q 2026 20
\QuestionPage{3.4 定积分的应用}{解答题}{2026 年第 20 题}{2}{拐点与无界旋转体积}{188 / 408}
（本题满分 12 分）
已知 \(M(x_0,y_0)\) 是曲线
\[y=\frac{1}{1+x^2}\qquad (x\ge 0)
\]
的拐点，\(O\) 为原点.记 \(D\) 是第一象限中以曲线
\[y=\frac{1}{1+x^2}\qquad (x\ge x_0),
\]
线段 \(OM\) 及 \(x\) 正半轴为边界的无界区域，求 \(D\) 绕 \(x\) 轴旋转所成旋转体的体积.
\QuestionEnd
% Q 2010 4
\QuestionPage{3.5 反常积分}{选择题}{2010 年第 4 题}{1}{反常积分审敛}{189 / 408}
设$m,n$是正整数，则反常积分$\int_0^1 \frac{\sqrt[m]{\ln^2(1 - x)}}{\sqrt[n]{x}}\,\mathrm{d} x$的收敛性\pickout{}
\begin{abcd}
\item 仅与$m$的取值有关．
\item 仅与$n$的取值有关．
\item 与$m,n$取值都有关．
\item 与$m,n$取值都无关．
\end{abcd}
\QuestionEnd
% Q 2013 4
\QuestionPage{3.5 反常积分}{选择题}{2013 年第 4 题}{1}{分段函数的反常积分}{190 / 408}
设函数$f(x) =\begin{cases}
  \frac{1}{(x - 1)^{\alpha - 1}}, & 1 < x < \mathrm{e}, \\
   \frac{1}{x\ln^{\alpha + 1} x}, & x \ge \mathrm{e},
\end{cases}$若反常积分$\int_1^{+\infty} f(x) \,\mathrm{d} x$收敛，则\pickout{}
\begin{abcd}
\item $\alpha < - 2$．
\item $\alpha > 2$．
\item $- 2 < \alpha < 0$．
\item $0 < \alpha < 2$．
\end{abcd}
\QuestionEnd
% Q 2015 1
\QuestionPage{3.5 反常积分}{选择题}{2015 年第 1 题}{1}{反常积分的收敛判别}{191 / 408}
下列反常积分收敛的是\pickout{}
\begin{abcd}
\item $\int_2^{+\infty} \frac{1}{\sqrt{x}}\,\mathrm{d} x$．
\item $\int_2^{+\infty} \frac{\ln x}{x}\,\mathrm{d} x$．
\item $\int_2^{+\infty} \frac{1}{x\ln x}\,\mathrm{d} x$．
\item $\int_2^{+\infty} \frac{x}{\mathrm{e}^x}\,\mathrm{d} x$．
\end{abcd}
\QuestionEnd
% Q 2016 3
\QuestionPage{3.5 反常积分}{选择题}{2016 年第 3 题}{1}{反常积分敛散性}{192 / 408}
反常积分\circnum{1}$\int_{-\infty}^0 \frac{1}{x^2}\mathrm{e}^{\frac{1}{x}} \,\mathrm{d} x$，
\par\circnum{2}$\int_0^{\text{+}\infty} \frac{1}{x^2}\mathrm{e}^{\frac{1}{x}} \,\mathrm{d} x$的敛散性为\pickout{}
\begin{abcd}
\item \circnum{1}收敛，\circnum{2}收敛．
\item \circnum{1}收敛，\circnum{2}发散．
\item \circnum{1}发散，\circnum{2}收敛．
\item \circnum{1}发散，\circnum{2}发散．
\end{abcd}
\QuestionEnd
% Q 2019 3
\QuestionPage{3.5 反常积分}{选择题}{2019 年第 3 题}{1}{反常积分审敛}{193 / 408}
下列反常积分发散的是\pickout{}
\begin{abcd}
\item $\int_0^{+\infty} x\mathrm{e}^{- x} \,\mathrm{d} x$．
\item $\int_0^{+\infty} x\mathrm{e}^{- x^2} \,\mathrm{d} x$．
\item $\int_0^{+\infty} \frac{\arctan x}{1 + x^2}\,\mathrm{d} x$．
\item $\int_0^{+\infty} \frac{x}{1 + x^2}\,\mathrm{d} x$．
\end{abcd}
\QuestionEnd
% Q 2022 5
\QuestionPage{3.5 反常积分}{选择题}{2022 年第 5 题}{1}{反常积分的收敛参数}{194 / 408}
设 \(p\) 为常数，若反常积分
\(\int_{0}^{1} \frac{\ln x}{x^{p}\left( 1-x \right)^{1-p}} \mathrm{~d}x\)
收敛，则 \(p\) 的取值范围是 \(\left( \ \right)\)
\choices{\(\left( -1,1 \right)\)}{\(\left( -1,2 \right)\)}{\(\left( -\infty,1 \right)\)}{\(\left( -\infty,2 \right)\)}
\QuestionEnd
% Q 2024 7
\QuestionPage{3.5 反常积分}{选择题}{2024 年第 7 题}{1}{非负函数的反常积分审敛}{195 / 408}
设非负函数 \(f(x)\) 在 \([0,+\infty)\) 上连续，给出三个命题：
\begin{enumerate}
\item 若 \(\int_0^{+\infty}f^2(x)\,dx\) 收敛，则 \(\int_0^{+\infty}f(x)\,dx\) 收敛；
\item 若存在 \(p>1\)，使极限 \(\lim_{x\to+\infty}x^p f(x)\) 存在，则 \(\int_0^{+\infty}f(x)\,dx\) 收敛；
\item 若 \(\int_0^{+\infty}f(x)\,dx\) 收敛，则存在 \(p>1\)，使极限 \(\lim_{x\to+\infty}x^p f(x)\) 存在。
\end{enumerate}
其中正确命题的个数是（ ）
\choices{\(0\)}{\(1\)}{\(2\)}{\(3\)}
\QuestionEnd
% Q 2009 10
\QuestionPage{3.5 反常积分}{填空题}{2009 年第 10 题}{2}{反常积分求参数}{196 / 408}
已知$\int_{-\infty}^{+\infty}\mathrm{e}^{k|x|}\,\mathrm{d} x = 1$，则$k=$ \blank{}．
\QuestionEnd
% Q 2011 12
\QuestionPage{3.5 反常积分}{填空题}{2011 年第 12 题}{2}{无穷区间上的积分}{197 / 408}
设函数$f(x) = \begin{cases}
  \lambda \mathrm{e}^{- \lambda x}, & x > 0, \\
                         0, & x \le 0,
\end{cases}$ $\lambda > 0$，则$\int_{-\infty}^{+\infty} xf(x)\,\mathrm{d} x =$ \blank{}．
\QuestionEnd
% Q 2014 9
\QuestionPage{3.5 反常积分}{填空题}{2014 年第 9 题}{2}{无穷区间上的反常积分}{198 / 408}
$\int_{-\infty}^{1} \frac{1}{x^2 + 2x + 5}\,\mathrm{d} x =$ \blank{}．
\QuestionEnd
% Q 2021 11
\QuestionPage{3.5 反常积分}{填空题}{2021 年第 11 题}{2}{无穷区间上的积分}{199 / 408}
\[\int_{-\infty}^{+\infty} |x|3^{-x^2}\,\mathrm{d}x= \blank{}
\]
\QuestionEnd
% Q 2025 11
\QuestionPage{3.5 反常积分}{填空题}{2025 年第 11 题}{2}{反常积分求参数}{200 / 408}
设 \(\int_{1}^{+\infty} \frac{a}{x\left( 2x + a \right)} \mathrm{~d} x = \ln 2\)，则 \(a =\) \blank{}.
\QuestionEnd


## tool · 2026-11-10T10:02:51Z




## assistant · 2026-11-10T10:02:54Z

已写到第 178 题。油罐题和抽水题都已核对原解析中的截面与高度，抽水功也用截面对称性复算了一遍。

## tool · 2026-11-10T10:04:48Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:04:53Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2026 11
\QuestionPage{3.5 反常积分}{填空题}{2026 年第 11 题}{2}{反常积分的收敛参数}{201 / 408}
设 \(p\) 为常数，若反常积分
\[\int_0^{+\infty}\frac{\arctan x}{x^p(x+1)}\,dx
\]
收敛，则 \(p\) 的取值范围是 \blank{}.
\QuestionEnd
% Q 2010 2
\QuestionPage{4.1 几类简单的微分方程}{选择题}{2010 年第 2 题}{1}{一阶线性方程解的关系}{202 / 408}
设$y_1,y_2$是一阶线性非齐次微分方程$y' + p(x)y = q(x)$的两个特解，
若常数$\lambda ,\mu$使$\lambda y_1 + \mu y_2$是该方程的解，
$\lambda y_1 - \mu y_2$是该方程对应的齐次方程的解，则\pickout{}
\begin{abcd}
\item $\lambda = \frac{1}{2},\mu = \frac{1}{2}$．
\item $\lambda = - \frac{1}{2},\mu = - \frac{1}{2}$．
\item $\lambda = \frac{2}{3},\mu = \frac{1}{3}$．
\item $\lambda = \frac{2}{3},\mu = \frac{2}{3}$．
\end{abcd}
\QuestionEnd
% Q 2011 10
\QuestionPage{4.1 几类简单的微分方程}{填空题}{2011 年第 10 题}{1}{一阶线性方程初值问题}{203 / 408}
微分方程$y' + y = \mathrm{e}^{- x}\cos x$满足条件$y(0) = 0$的解为$y =$ \blank{}．
\QuestionEnd
% Q 2012 12
\QuestionPage{4.1 几类简单的微分方程}{填空题}{2012 年第 12 题}{2}{一阶微分方程初值问题}{204 / 408}
微分方程$y\,\mathrm{d} x + (x - 3y^2)\,\mathrm{d} y = 0$满足初始条件$y|_{x = 1}$=1的解为$y =$ \blank{}．
\QuestionEnd
% Q 2016 11
\QuestionPage{4.1 几类简单的微分方程}{填空题}{2016 年第 11 题}{2}{由特解确定一阶线性方程}{205 / 408}
以$y = x^2 - \mathrm{e}^x$和$y = x^2$为特解的一阶非齐次线性微分方程为 \blank{}．
\QuestionEnd
% Q 2024 13
\QuestionPage{4.1 几类简单的微分方程}{填空题}{2024 年第 13 题}{2}{一阶微分方程}{206 / 408}
微分方程
\[y'=\frac{1}{(x+y)^2}
\]
满足初始条件 \(y(1)=0\) 的解为 \blank{}
\QuestionEnd
% Q 2025 15
\QuestionPage{4.1 几类简单的微分方程}{填空题}{2025 年第 15 题}{2}{一阶微分方程初值问题}{207 / 408}
微分方程 \(\left( 2y - 3x \right) \mathrm{d} x + \left( 2x - 5y \right) \mathrm{d} y = 0\) 满足条件 \(y\left( 1 \right) = 1\) 的解为 \blank{}.
\QuestionEnd
% Q 2009 18
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2009 年第 18 题}{3}{降阶方程与旋转体积}{208 / 408}
设非负函数$y = y(x)$（$x \ge 0$）满足微分方程$xy'' - y' + 2 = 0$，
当曲线$y = y(x)$过原点时，其与直线$x = 1$及$y = 0$围成平面区域$D$的面积为$2$，
求$D$绕$y$轴旋转所得旋转体体积．
\QuestionEnd
% Q 2011 18
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2011 年第 18 题}{3}{由切线倾角建立微分方程}{209 / 408}
设函数$y(x)$具有二阶导数，且曲线$l:y = y(x)$与直线$y = x$相切于原点，
记$\alpha$为曲线$l$在点$(x,y)$处切线的倾角，若$\frac{\,\mathrm{d}{}\alpha}{\,\mathrm{d} x} = \frac{\,\mathrm{d} y}{\,\mathrm{d} x}$，求$y(x)$的表达式．
\QuestionEnd
% Q 2014 16
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2014 年第 16 题}{2}{可分离变量方程与极值}{210 / 408}
已知函数$y = y(x)$满足微分方程$x^2 + y^2 y' = 1 - y'$，且$y(2) = 0$，求$y(x)$的极大值和极小值．
\QuestionEnd
% Q 2015 20
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2015 年第 20 题}{3}{牛顿冷却模型}{211 / 408}
已知高温物体置于低温介质中，任一时刻该物体温度对时间的变化率与该时刻物体和介质的温差成正比，
现将一初始温度为$120^{\circ}C$的物体在$20^{\circ}C$的恒温介质中冷却，$30$min后该物体降至$30^{\circ}C$，
若要将该物体的温度继续降至$21^{\circ}C$，还需冷却多长时间？
\QuestionEnd
% Q 2017 21
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2017 年第 21 题}{4}{由切线和法线条件建立方程}{212 / 408}
设$y(x)$是区间$\left(0,\frac{3}{2} \right)$内的可导函数，且$y(1) = 0$．
点$P$是曲线$L:y = y(x)$上的任意一点．$L$在$P$处的切线与$y$轴相交于点$\left(0,Y_p\right)$，
法线与$x$轴相交于点$\left(X_p,0 \right)$，若$X_p = Y_p$，求$L$上点的坐标$(x,y)$满足的方程．
\QuestionEnd
% Q 2019 17
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2019 年第 17 题}{2}{一阶线性方程与旋转体积}{213 / 408}
设函数$y(x)$是微分方程$y'-xy=\frac{1}{2\sqrt{x}}\mathrm{e}^{\frac{x^2}{2}}$满足条件$y(1)=\sqrt{\mathrm{e}}$的特解．
\begin{enumerate}
\item 求$y(x)$的表达式；
\item 设平面区域$D = \{(x,y)|1 \le x \le 2,0 \le y \le y(x)\}$，
      求$D$绕$x$轴旋转一周所形成的旋转体的体积．
\end{enumerate}
\QuestionEnd
% Q 2020 21
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2020 年第 21 题}{4}{由面积比建立微分方程}{214 / 408}
设函数 \(f\left( x \right)\) 可导，且 \(f^{\prime}\left( x \right)>0\)，曲线 \(y=f\left( x \right)\left( x\geq 0 \right)\) 经过坐标原点 \(O\)。\(M\) 为其上任意一点，点 \(M\) 处的切线与 \(x\) 轴交于点 \(T\)，又 \(MP\) 垂直 \(x\) 轴于点 \(P\)。已知由曲线 \(y=f\left( x \right)\)、直线 \(MP\) 以及 \(x\) 轴所围图形的面积与 \(\triangle MTP\) 的面积之比恒为 \(3:2\)，求满足上述条件的曲线方程。
\QuestionEnd
% Q 2021 20
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2021 年第 20 题}{3}{一阶方程与距离最值}{215 / 408}
函数 \(y=y(x)\) 的微分方程
\[xy'-6y=-6,
\]
满足 \(y\left(\sqrt{3}\right)=10\)。
\begin{enumerate}
\item 求 \(y(x)\)；
\item \(P\) 为曲线 \(y=y(x)\) 上的一点，曲线在点 \(P\) 的法线在 \(y\) 轴上的截距为 \(I_y\)。为使 \(I_y\) 最小，求 \(P\) 的坐标。
\end{enumerate}
\QuestionEnd
% Q 2022 18
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2022 年第 18 题}{3}{一阶方程与曲线弧长}{216 / 408}
设函数 \(y\left( x \right)\) 是微分方程
\(2x y^{\prime} - 4y = 2\ln x - 1\)
的满足条件
\(y\left( 1 \right) = \frac{1}{4}\)
的解，求曲线 \(y = y\left( x \right)\) 在 \(\left[ 1,e \right]\) 上的弧长.
\QuestionEnd
% Q 2023 17
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2023 年第 17 题}{3}{由切线截距建立一阶方程}{217 / 408}
设曲线 \(\boldsymbol L:y=y(x)\)（\(x>e\)）经过点 \((e^2,0)\)，且 \(\boldsymbol L\) 上任一点 \(P(x,y)\) 到 \(y\) 轴的距离等于该点处切线在 \(y\) 轴上的截距。
\begin{enumerate}
\item 求 \(y(x)\)；
\item 在 \(\boldsymbol L\) 上求一点，使该点处的切线与两坐标轴所围三角形的面积最小，并求此最小面积。
\end{enumerate}
\QuestionEnd
% Q 2026 21
\QuestionPage{4.1 几类简单的微分方程}{解答题}{2026 年第 21 题}{2}{二阶微分方程降阶}{218 / 408}
（本题满分 12 分）
求微分方程
\[x^2y''-2xy'-(y')^2=0\qquad (x>2)
\]
满足条件
\[y\big|_{x=3}=\frac12,\qquad y'\big|_{x=3}=-9
\]
的解.
\QuestionEnd
\frac{a}{x(2x+a)}=\frac1x-\frac{2}{2x+a},\qquad
\int_1^\infty \frac{a}{x(2x+a)}\,\mathrm{d}x
=\left[\ln\frac{x}{2x+a}\right]_1^\infty
=\ln\frac{2+a}{2}.
\]
由题设，\((2+a)/2=2\)，所以 \(a=\boxed{2}\)。




## tool · 2026-11-10T10:05:23Z


Script completed
Wall time 0.1 seconds
Output:

1469-```text
1470-如图（b）所示，同理可得由曲线x=4（g），直线 =0， =6以及 轴所围成的曲边梯形
1471-=（x）
1472-X=$0）
1473-As
1474-Q
1475-Ax
1476-（a）
1477-（b）
1478-20
1479-设函数y=y（x）（ >0）满足微分方程xy’ 6y= 6，且满足y（ 3）= 10.
1480-（I）求y（x）；
1481:（II）P为曲线y=y（x）上的一点，曲线y=y（x）在点P的法线在y轴上截距为1p，为使1，最
1482-小，求尸的坐标
1483-（分析 本题综合考查微分方程求解与一元函数最值问题.
1484-y（x）的表达式可通过解微分方程得到.根据导数的几何意义，可找到曲线y=y（x）在点P（x,y）
1485-处的切线斜率，从而可得点P处的法线方程.1p可写为关于点P的横坐标x的一元函数，求其最小值
1486-点，即可得点P的坐标.
1487-解（I）整理 xy’ 6y= 6得，
1488-92 =-
1489-由求解公式，可得
1490-d+C」=x［/（-6xd+c］ =x（x+C）=ca+1.
1491-代入y（ 3）=10，可得10=1+C（/3）。
1492-°，即10 =1 +27C. 解得C =
1493-因此， （ ）
1448-由罗尔定理，存在 E（1,2），使得G'（5）=0，即
1449-因此，存在 （1,2），使得f（ ）=（2 ）e
1450-由柯西中值定理，存在n= （1,2），使得
1451-f（2） -f（1）
1452-8（2）-8i:f（2
1453-g'（m）
1454-由于f（1）= 0,g（1）= 0,g（2）=In 2，故（1）式可化为
1455-1f（2）
1456-In 2
1457-（1）
1458--，即f（2） = In2•ne”
1459-21设函数f（x）可导，且 （x）>0.曲线 （ ）（ ≥0）经过坐标原点O，其上任意一点M
1460:处的切线与x轴交于T，又MP垂直x轴于点P.已知由曲线y=f（x），直线MP 以及x轴所围图形
1461:的面积与 AMTP 的面积之比恒为3：2，求满足上述条件的曲线的方程.
1462-分析本题综合考查了导数的几何应用、定积分的几何应用与微分方程.
1463:本题中，分别写出两个平面图形的面积的表达式，利用面积之比恒为3：2建立微分方程，解微
1464-分方程可得所求曲线方程.
1465-解点M,T,P 如图所示.
1466-=f（）
1467:计算 AMTP 的面积
1468-曲线y=f（x）上任意一点 M（x，f（x））处的切线方程为
1469-f（x）
1470-令Y=0，可得点T的横坐标为X=x
1471-24
1472-```
1473-
1474-## PDF 第 22 页
1475-
1476-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2020%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=22) · 本机 OCR
1477-
1478-```text
1479:由于 =f（x）（ ≥0）过原点，且 （x）>0，故点M的纵坐标f（x）>0.MP=f（ ），
1480-fx）
1481-f（x）
1482-f（x）
1483:，于是，SLMTP =
1484-f（x）
1485:-IMPI 1TPI=•J（x）．
1486-TP=
1487-f（x）
1488-［f（x） ］2
1489-f'（x）
1490-=
1491-2f'（x）
1492:由定积分的几何意义可得，曲边三角形 OMP的面积S=St）d.
1493:由曲边三角形 OMP 的面积与 AMTP 的面积之比恒3:2可知
1494-4l,8t）d=3L/（z）12
1495-f'（x）
1496-Jft）d
1497-［f（x） 卫2
1498-=
1499-2f（x）
1500-之，即
1501-（1）
1502-对（1）式两端同时求导可得，
1503-［f"（x）］
1504-整理可得2［f'（x）］ =3f（x）f"（x），即2（y'） =3yy”.
1505-，即3y
516-应填0.
517-分析本题主要考查多元复合函数的偏导数的计算.
518-（解）利用链式法则，
519-ax
520-=f'（Inx+
521-L）
522-因此，
523:12微分方程ydx +（x-3y ）dy =0满足条件ylx=1 =1 的解为y=-
524-答案
525-应填 v死.
526-分析）本题主要考查一阶非齐次线性微分方程的解法.
527-我们可以将原方程转化为一阶非齐次线性微分方程，然后利用求解公式直接计算该方程的通
528-解，最后代人初始条件求得初值问题的解.
529-（） 紧理原微分方程。码票+产=3以，这是一个以y为自变題：为因变顧的一阶非齐改线性
530-微分方程.


## tool · 2026-11-10T10:05:32Z




## tool · 2026-11-10T10:05:37Z


Script completed
Wall time 0.1 seconds
Output:

17-二、填空题
18-（9） 12.
19-（10）e*sin *. （11）In（JE +1）.（12）元（13）台：（14）2.
20-三、解答题
21-（15）1 <a <3.
22-（16）极大值y（-1）=1，极小值，（号）=一号，凹区间（号，+∞），凸区间（-∞，言），拐点
23-（17） f！（1, 1） +f". （1,1） +f2（1,1）-
24-e"
25:（18） y（x） = arcsin
26-V2
27-4
28-（19）（I）证明略；
29-（II）证明略.
30-（20）（1）90
31-“（m'）；
32-（1I） 27×103
33--Tg（J）•
--
978-而不能写成 3y
979-=f1+ H+f12
980-y=1
981-18
982-设函数y（x）具有二阶导数，且曲线1:y=y（x）与直线y=，*相切于原点.记~为曲线1在
983-分析
984-本题是一道关于微分方程在几何上的应用的题目，需要从条件出发构造微分方程，从
985-而求得y（x）的表达式.
986:题目中涉及的变量有3个，x，y，Q. 一方面，利用已知条件dQ =当以及利用直线的倾角a与直
987-线的斜率y之间的关系 tan a =y’，可以建立一个关于~，x的一阶微分方程.另一方面，也可以利
988-用Q与y’的关系，将dQ
989-=当转化为关于y，x的微分方程。
990-一19一
991-```
992-
993-## PDF 第 17 页
994-
--
999-由=当可得，a =y+G，其中G，为待定常数.于是，可以将求y（x）的表达式转化为求c的表
1000-达式.
1001-由导数的几何意义知，
1002-sin a =Cze*，其中Cz为待定常数.
1003-= tan a，故
1004-分离变量得，
1005-da = dx，解得
1006-e*
1007:a（x） = arcsin
1008-12
1009:3（x）= 8（x）-G= arcsin
1010--C」.
1011-12
1012-下面求G」•
1013-由于 a（0）=
1014-因此，
1015-，1（0）=0，故0=
1016--G,G=#
1017:y（x） = arcsin d
1018--—-
1019-4
1020-（法二）由于曲线1： =y（x）在点（x，y）处的切线斜率y’
1021-'，故 tan a = y'， a = arctan y'.
1022-由链式法则可得
1023-''dx
1024-1+（y 又因为g
1025-品，所以
--
1055-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2011%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=18) · 本机 OCR
1056-
1057-```text
1058-Y（×）=
1059-v2
1060-dt
1061-=
1062-e'
1063:dt = arcsin
1064-12
1065-0
1066-e'
1067:= arcsin
1068-—
1069-"
1070-4
1071-注法一的方法在计算上比法二简单许多，它的好处在于直接以a为因变量来构造微
1072-分方程，从而得到的微分方程均为一阶微分方程.
1073-富拓展
1074-本题是微分方程的几何应用题—导数的几何应用.
1075-由于导数与切线斜率、二阶导数与曲率密切相关，故在导数的几何应用中，常见的几何量
20
设函数y=y（x）（ >0）满足微分方程xy’ 6y= 6，且满足y（ 3）= 10.
（I）求y（x）；
（II）P为曲线y=y（x）上的一点，曲线y=y（x）在点P的法线在y轴上截距为1p，为使1，最
小，求尸的坐标
（分析 本题综合考查微分方程求解与一元函数最值问题.
y（x）的表达式可通过解微分方程得到.根据导数的几何意义，可找到曲线y=y（x）在点P（x,y）
处的切线斜率，从而可得点P处的法线方程.1p可写为关于点P的横坐标x的一元函数，求其最小值
点，即可得点P的坐标.
解（I）整理 xy’ 6y= 6得，
92 =-
由求解公式，可得
d+C」=x［/（-6xd+c］ =x（x+C）=ca+1.
代入y（ 3）=10，可得10=1+C（/3）。
°，即10 =1 +27C. 解得C =
因此， （ ）
-+1,3>0.
（I）根据导数的几何意义，曲线y=
+1上的点P（x,y）处的切线斜率为2x’.由同一点处的
切线与法幾相豆垂宜，斛率藥积为一1可得点P处的法线斜率为一之子是，点P处的法幾方群光
令X=0，可得Y=y+
2x
计算Ip（x）•
Y-y=一
205（X-x）.
+1+
20，即Ip（x）=
4+1.
16（x）=（+
+1）=2x°-288
2（x1
-1）
，× ≥0.
% SOLUTION 197 2011 12
% SOLUTION 198 2014 9
% SOLUTION 199 2021 11
% SOLUTION 200 2025 11


## assistant · 2026-11-10T10:05:41Z

第 179–200 题的推导已写完。核对 2021 年第 20 题时发现题库漏录了 \(x>0\)，这会影响法线截距最小点的结论，已把原解析的位置交给主稿编辑。

## tool · 2026-11-10T10:07:11Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:07:17Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2011 4
\QuestionPage{4.2 高阶线性微分方程}{选择题}{2011 年第 4 题}{1}{非齐次方程的特解形式}{219 / 408}
微分方程$y'' - \lambda^2 y = \mathrm{e}^{\lambda x} + \mathrm{e}^{- \lambda x}$（$\lambda > 0$）的特解形式为\pickout{}
\begin{abcd}
\item $a(\mathrm{e}^{\lambda x} + \mathrm{e}^{- \lambda x})$．
\item $ax(\mathrm{e}^{\lambda x} + \mathrm{e}^{- \lambda x})$．
\item $x(a\mathrm{e}^{\lambda x} + b\mathrm{e}^{- \lambda x})$．
\item $x^2(a\mathrm{e}^{\lambda x} + b\mathrm{e}^{- \lambda x})$．
\end{abcd}
\QuestionEnd
% Q 2017 4
\QuestionPage{4.2 高阶线性微分方程}{选择题}{2017 年第 4 题}{1}{常系数非齐次方程特解}{220 / 408}
微分方程$y'' - 4y' + 8y = \mathrm{e}^{2x}(1 + \cos 2x)$的特解可设为$y^* =$\pickout{}
\begin{abcd}
\item $A\mathrm{e}^{2x} + \mathrm{e}^{2x}\left(B\cos 2x + C\sin 2x \right)$．
\item $Ax \mathrm{e}^{2x} + \mathrm{e}^{2x}\left(B\cos 2x + C\sin 2x \right)$．
\item $A\mathrm{e}^{2x} + x\mathrm{e}^{2x}\left(B\cos 2x + C\sin 2x \right)$．
\item $Ax \mathrm{e}^{2x} + x\mathrm{e}^{2x}\left(B\cos 2x + C\sin 2x \right)$．
\end{abcd}
\QuestionEnd
% Q 2019 4
\QuestionPage{4.2 高阶线性微分方程}{选择题}{2019 年第 4 题}{1}{由通解确定方程系数}{221 / 408}
已知微分方程$y'' + ay' + by = c\mathrm{e}^x$的通解为$y = (C_1 + C_2 x) \mathrm{e}^{- x} + \mathrm{e}^x$，则$a,b,c$依次为\pickout{}
\begin{abcd}
\item $1,0,1$．
\item $1,0,2$．
\item $2,1,3$．
\item $2,1,4$．
\end{abcd}
\QuestionEnd
% Q 2023 4
\QuestionPage{4.2 高阶线性微分方程}{选择题}{2023 年第 4 题}{1}{常系数方程解的有界性}{222 / 408}
若微分方程
\[y''+ay'+by=0
\]
的解在 \((-\infty,+\infty)\) 上有界，则（ ）。
\choices{\(a<0,\ b>0\)}{\(a>0,\ b>0\)}{\(a=0,\ b>0\)}{\(a=0,\ b<0\)}
\QuestionEnd
% Q 2025 3
\QuestionPage{4.2 高阶线性微分方程}{选择题}{2025 年第 3 题}{1}{常系数方程与反常积分收敛}{223 / 408}
如果对微分方程 \(y^{\prime\prime} - 2a y^{\prime} + \left( a + 2 \right) y = 0\) 的任一解 \(y\left( x \right)\)，反常积分 \(\int_{0}^{+\infty} y\left( x \right) \mathrm{~d} x\) 均收敛，那么 \(a\) 的取值范围是
\choices{\(\left( -2, -1 \right]\)}{\(\left( -\infty, -1 \right]\)}{\(\left( -2, 0 \right)\)}{\(\left( -\infty, 0 \right)\)}
\QuestionEnd
% Q 2026 2
\QuestionPage{4.2 高阶线性微分方程}{选择题}{2026 年第 2 题}{1}{非齐次方程的解的结构}{224 / 408}
设 \(y_1(x),y_2(x)\) 是某二阶非齐次线性微分方程的两个特解.若常数 \(\lambda,\mu\) 使得 \(2\lambda y_1(x)+\mu y_2(x)\) 是该方程的解，\(\lambda y_1(x)-2\mu y_2(x)\) 是该方程对应齐次方程的解，则
\choices{\(\lambda=\frac15,\ \mu=\frac25\)}{\(\lambda=\frac25,\ \mu=\frac15\)}{\(\lambda=\frac14,\ \mu=\frac12\)}{\(\lambda=\frac12,\ \mu=\frac14\)}
\QuestionEnd
% Q 2010 9
\QuestionPage{4.2 高阶线性微分方程}{填空题}{2010 年第 9 题}{2}{三阶常系数齐次方程}{225 / 408}
$3$阶常系数线性齐次微分方程$y''' - 2y'' + y' - 2y = 0$的通解为$y =$ \blank{}．
\QuestionEnd
% Q 2013 13
\QuestionPage{4.2 高阶线性微分方程}{填空题}{2013 年第 13 题}{2}{非齐次方程的特解与初值}{226 / 408}
已知$y_1 = \mathrm{e}^{3x} - x\mathrm{e}^{2x}$，$y_2 = \mathrm{e}^x - x\mathrm{e}^{2x}$，$y_3 = - x\mathrm{e}^{2x}$
是某二阶常系数非齐次线性微分方程的$3$个解，
该方程满足条件$y\big|_{x = 0} = 0$，$y'\big|_{x = 0} = 1$的解为$y =$ \blank{}．
\QuestionEnd
% Q 2015 12
\QuestionPage{4.2 高阶线性微分方程}{填空题}{2015 年第 12 题}{2}{常系数齐次方程与极值条件}{227 / 408}
设函数$y = y(x)$是微分方程$y'' + y' - 2y = 0$的解，且在$x = 0$处$y(x)$取得极值$3$，则$y(x)$= \blank{}．
\QuestionEnd
% Q 2020 13
\QuestionPage{4.2 高阶线性微分方程}{填空题}{2020 年第 13 题}{2}{齐次方程初值问题与积分}{228 / 408}
设 \(y = y\left( x \right)\) 满足 \(y^{\prime\prime} + 2y^{\prime} + y = 0\)，且 \(y\left( 0 \right) = 0\)，\(y^{\prime}\left( 0 \right) = 1\)，则 \(\int_{0}^{+\infty}{y\left( x \right) \mathrm{~d} x} =\)
\blank{}
\QuestionEnd
% Q 2021 15
\QuestionPage{4.2 高阶线性微分方程}{填空题}{2021 年第 15 题}{2}{常系数齐次方程的通解}{229 / 408}
微分方程 \(y'''-y=0\) 的通解
\[y= \blank{}
\]
\QuestionEnd
% Q 2022 14
\QuestionPage{4.2 高阶线性微分方程}{填空题}{2022 年第 14 题}{2}{三阶常系数齐次方程}{230 / 408}
微分方程
\(y^{\prime\prime\prime} - 2y^{\prime\prime} + 5y^{\prime} = 0\)
的通解为 \(y\left( x \right) = \blank{}\)
\QuestionEnd
% Q 2009 20
\QuestionPage{4.2 高阶线性微分方程}{解答题}{2009 年第 20 题}{4}{分段求解微分方程}{231 / 408}
设$y = y(x)$是区间$(- \pi ,\pi)$内过点
$\left(- \frac{\pi}{\sqrt{2}},\frac{\pi}{\sqrt{2}} \right)$的光滑曲线，
当$- \pi < x < 0$时，曲线上任一点处的法线都过原点，
当$0 \le x < \pi$时，函数$y(x)$满足$y'' + y + x = 0$．求$y(x)$的表达式．
\QuestionEnd
% Q 2012 19
\QuestionPage{4.2 高阶线性微分方程}{解答题}{2012 年第 19 题}{3}{常系数方程与积分曲线拐点}{232 / 408}
设函数$f(x)$满足方程$f''(x) + f'(x) - 2f(x) = 0$及$f'(x) + f(x) = 2\mathrm{e}^x$．
\begin{enumerate}
\item 求表达式$f(x)$；
\item 求曲线的拐点$y = f(x^2)\int_0^x f(- t^2)\,\mathrm{d} t$．
\end{enumerate}
\QuestionEnd
% Q 2016 19
\QuestionPage{4.2 高阶线性微分方程}{解答题}{2016 年第 19 题}{3}{二阶变系数线性方程}{233 / 408}
已知$y_1(x) = \mathrm{e}^x$，$y_2(x) = u(x) \mathrm{e}^x$是二阶微分方程$(2x - 1)y^n - (2x + 1)y' + 2y = 0$的解，
若$u(- 1) = e$，$u(0) = - 1$，求$u(x)$，并写出该微分方程的通解．
\QuestionEnd
% Q 2024 18
\QuestionPage{4.2 高阶线性微分方程}{解答题}{2024 年第 18 题}{3}{欧拉方程与定积分}{234 / 408}
设 \(y=y(x)\) 满足方程
\[x^2y''+xy'-9y=0,
\]
且
\[y\big|_{x=1}=2,\qquad y'\big|_{x=1}=6.
\]
\begin{enumerate}
\item 利用变换 \(x=e^t\) 化简方程，并求 \(y(x)\)；
\item 求
\[\int_1^2 y(x)\sqrt{4-x^2}\,dx.
\]
\end{enumerate}
\QuestionEnd
\[
y'=-\frac{x^2}{x-2}=-x-2-\frac4{x-2}.
\]
此式在整个 \(x>2\) 上有定义且不取零。积分得 \(y=-x^2/2-2x-4\ln(x-2)+C_1\)，由 \(y(3)=1/2\) 得 \(C_1=11\)。因此
\[
\boxed{y=11-\frac{x^2}{2}-2x-4\ln(x-2)},\qquad x>2 .
\]
代回可验证方程及两个初值。




## tool · 2026-11-10T10:07:38Z


Script completed
Wall time 0.1 seconds
Output:

1050-注 法二中最后一步计算用到了
1051-d0 = - cot 0 +C. 这是因
1052-sin?e
1053-sin?0
1054-（cot 0）'= - csc?0. 与此同类型的公式还有我们熟悉的（tan O）'= sec?0.
1055-如果对余切函数cot x 不熟悉，那么也可以如下计算.
1056-=1-2
1057-= csc0而
1058-= 1.
1059-19
1060:已知yi（x）=e*，32（x）=u（x）e*是二阶微分方程（2 1） ” （2 +1）y’+2y=0的
1061-两个解.若u（-1）=e,u（O）=-1，求w（x），并写出该微分方程的通解
1062-分析本题综合考查了微分方程的相关知识，包括微分方程的解的概念，用降阶法解微分方
1063-程以及齐次线性微分方程的解的结构等.
1064-原方程是一个二阶线性微分方程，但不是常系数的，由我们学过的解微分方程的知识不能直
1065-接得到该方程的解，因而可以考虑将y2（x）代入原方程得到新的关于w（x）的方程.由于二阶齐次
1066-线性微分方程的通解可以由该方程的两个线性无关的解表示，故在得到w（x）后，可以写出原微分
1067-—21—
1068-```
1069-
1070-## PDF 第 19 页
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-454-20.（本题满分12分）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-455-已知M（xo.1）是曲线y=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:456:I+ （ ≥0）的拐点，Q为坐标原点、记D是第一象限中以
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-457-曲线 =
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-458-I+ （ ≥x），线段OM及x正半轴为这界的无界区域，求D绕x轴旋转所成庭
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-428-20.（本题满分12分）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-429-已知M（xo.2o）是曲线 =
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:430:1+x（*≥0）的拐点，Q为坐标原点，记D是第一象限中以曲线
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-431-i+x（2 ），线段ON 及x正半轴为边界的无界区域，求D绕x轴旋转所成旋转体的体积、
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-432-6x2-2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-433-【解析】 =
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:434:一，拐点坐标为
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-435-（1+x
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-436-（1+×~


## tool · 2026-11-10T10:07:43Z




## tool · 2026-11-10T10:07:47Z


Script completed
Wall time 0.1 seconds
Output:

307-T
308-由于1（平）"
309-= 0，故由夹逼准则可知，lim
310-1=0.
311-1∞ Xn
312-综上所述，当n一∞时，3，是x，的高阶无穷小，应选B.
313-下面证明1xn｝是n一∞时的无穷小.
314-由法一可知，&a+l = sin n= 。一
315-cos 5r 。<xo，于是1 。！单调减少.结合法一中所得结
316:论“对任意正整数n.，*。E（0,1）”可得，1x。｝单调有界，从而lim *。存在，记为a.对
317-Xa+l = sin *，两端取极限可得，Lim *a+l = Lim gin x。 = sin lim &n，即a= sin a，解得a=0.
318-此外，%=（）
319-，lim yn = 0,1ynl 也是n一>∞时的无穷小.
320-4元
321:若微分方程y”+ay'+by = 0的解在（-∞，+∞）上有界，则（
322-）
323-（A）a <0,6>0.
324-（B）a ≥0,6≥0.
325-（C）a =0,6 >0.
326-（D）a =0,6<0.
327-答案）
328-分析）本题主要考查二阶常系数齐次线性微分方程的解.
329-二阶常系数齐次线性微分方程y”+py'+gy = 0（p，q 为常数）通解的求法
330-（1）写出特征方程A+pA + 9 =0；
--
332-（3）根据特征方程两个根的不同情形，按照下述表格写出通解.
333-特征方程A2+pA +9 =0的根
334-微分方程y"+py'+gy=0的通解
335-两个不同实根A」，A2
336-y= Celn + Cze's
337-两个相同实根A」=A2
338-Y= （C1 + Czx）e^H
339-一对共轭复根A12= a 士Bi
340-y= e" （C,cos Bx + Casin Bx）
341:已知条件为给定方程的解在（-∞，+∞）上有界，故我们可以从该方程的解的情况出发，找到
342:有界解对应系数所满足的条件.注意到三种情况下解中都出现了指数函数，而
343-lim
344-A≥0，
345-lim elr =
346-+∞，
347-A≥0，
348-X—-∞
349-+8，
350-A<0，
351-一+∞
--
356-
357-## PDF 第 7 页
358-
359-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2023%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=7) · 本机 OCR
360-
361-> 读取原 PDF 时出现警告，建议核对原页。
362-
363-```text
364-故当A*0时，e'在（-∞，+∞）上均无界.此为本题的解题关键
365:解由于二阶常系数齐次线性微分方程必有零解，而零解为有界解，故微分方程y"+ay’ + by
366:=0必然存在（-∞，+∞）上的有界解.本题实际上是要求此方程的所有解都有界.
367-微分方程g'+ay'+by = 0的特征方程为A+aA +6=0.
368-•若A=a-46>0，则特征方程有两个不同实根A」，A2，从而至少有一个实根非零.此时，微
369-分方程的解为y=Cje'i + Cze'*.
370-取C，=C2=1，则lim （e' +el*）=+∞或lim （e's +elx）=+∞.该解在（-∞，+∞）上
371-无界.
372-• 若A=a’-46 =0，则特征方程有两个相同实根A.此时，微分方程的解为 =（C，+
373-Cz）e'.
374-取C， =0,C2 =1，则lim xe' = ∞ 或lim xe^ = ∞.该解在（-∞，+∞）上无界.
375-•若A=d-46 <0，则特征方程有一对共轭复根A12=士Bi. 此时，微分方程的解为
376-y= e"（Cjcos Bx + Czsin Bx）.
377-当a¥0时，取C，=1,C2=0，所得解y= e"cos Bx 是（-∞，+∞）上的无界函数
378-当~ = 0时，微分方程的解为y=G, cos Bx + Casin Bx. 对任意常数C1,Gz，该解在
379:（-∞， +∞）上均有界，根据求根公式，A12=一2
380-a-46<0可知，6>0.
381-因此，a=0,6>0.应选C.
382-一i，即a =-
383-于是，a=0. 结合
384-5
385-设函数y=f（x）由
386-Jx =21+1t，确定，则（
387-.）
388-y=tsint
146-么a的取值范围是（）
147-（A）（-2，-1］•
148-（B） （-∞，-1］.
149-（C） （-2,0）.
150-（D）（-∞，0）.
151-（答案）c.
152:分析本题主要考查二阶常系数齐次线性微分方程的解与反常积分的敛散性.
153-根据二阶常系数齐次线性微分方程的解的情况，y（x）共有三种可能性：Cje^ +Cze e
154-，（C」+
155-Czx）ed
156-，e"（G;cos Bxi + Casin Bx）.考虑）
157-x（x）dx的敛散性，可归结为考虑店
158-“edx，lse'dx，
--
211-## PDF 第 5 页
212-
213-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2025%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=5) · 本机 OCR
214-
215-```text
216-拓展
217:与微分方程的解有关的综合题，包括与函数性质综合、与反常积分综合等，是近年来一种
218-较新的出题类型. 下面我们给出历年真题中的一些同类题
219-【例】设函数y（x）满足方程 ”+2y'+ky=0，其中0< <1.
220:（I）证明：反常积分。y（x）dx 收敛；
221-（I）若y（0）=1,y'（0）=1，求。 （x）dx的值（2016年数学一试题）
222-答案
223-（I）证明略：（I）≥
224-【例】若函数f（x）满足f（x）+af'（x）+f（x）=0（a>0），f（0）=m,f（0） ，则
225-oflx）d=—（2020年数学一试题）
226-答案 n+am.
--
784-+8
785-11设，
786-x（2x +aJdt= In2，则a=
787-答案
788-应填2.
789-（分析
790:本题主要考查反常积分的计算.
791-要求a的值，只需计算）
792-x（28+a）
793--dx的值，由此可得一个关于a的方程，解该方程即可得a.
794-解 由于
795-2
796-=
--
813-= 2或a
814-= - 6.
815-当a=-6时
816-3-2（%-3
817-x（2x +a）dt=
818-x（x-3）d，此时x=3为被积函数的環点，且
819:由无界函数的反常积分的极限审敛法可得」
820-x（ -3）
821--dx 发散，从而
822-dx 发散.于是，应舍去 a =-6.
823-2（%-3）
824-当a =2时，被积函数在（1，+∞）上没有瑕点.
825-因此，a = 2.


## tool · 2026-11-10T10:09:07Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:09:20Z


Script completed
Wall time 0.1 seconds
Output:

Traceback (most recent call last):
  File "<string>", line 1, in <module>
AssertionError
    1276   64901 .question-bank-work/solutions/114-234.tex
.
..
solutions


## tool · 2026-11-10T10:09:30Z


Script completed
Wall time 0.1 seconds
Output:

121 121 True
paragraph issues []
pair issues []
max line length 304


## tool · 2026-11-10T10:09:34Z




## assistant · 2026-11-10T10:09:38Z

第 114–234 题全部写完，121 个标记已逐条核对题库的序号、年份和原卷题号。中间稿已交给主稿编辑，我继续复查几处计算结果。

## tool · 2026-11-10T10:09:40Z


Script completed
Wall time 0.1 seconds
Output:


----2009----

```text
2009年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）C. （2）A.
二、填空题
（9）y=2%.
三、解答题
（15）
（3）D. （4）C.
（5）B. （6） D.
（7）B. （8） A.
（10） -2. （11）0. （12）-3.
（13）e合.（14）2.
dxdy
17m
（18）
6
8
（19）-
3
V -x
（20）y（x）
=
，

----2010----

```text
2010年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1） B. （2）A. （3）C. （4）D. （5） B. （6）D. （7）A. （8） D.
二、填空题
（9） Gje^ + Cacos x + Cgsin x，其中G」，G2，Gs为任意常数
（10）y =23
（11） - 2"（n -1）！. （12） v2（e™ - 1）.
（13）3 cm/s. （14）3.
三、解答题
（15）单调增加区间为（-1，0）和（1，+∞），单调减少区间为（-∞，-1）和（0，1）；
（16） （I） IIntl［In（1 +t）］"d < e |Int l da（n = 1,2，⋯），理由略；
（I） lin 4=0.
（18） abol（写+順）.
a =-2，
（19）
b
=—
2
或
5
a --，
= -2.
（20）1=

----2011----

```text
2011 年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）C. （2）B. （3） C. （4）C. （5）A. （6）B. （7）D. （8）D.
二、填空题
（9） 12.
（10）e*sin *. （11）In（JE +1）.（12）元（13）台：（14）2.
三、解答题
（15）1 <a <3.
（16）极大值y（-1）=1，极小值，（号）=一号，凹区间（号，+∞），凸区间（-∞，言），拐点
（17） f！（1, 1） +f". （1,1） +f2（1,1）-
e"
（18） y（x） = arcsin
V2
4
（19）（I）证明略；
（II）证明略.
（20）（1）90
“（m'）；
（1I） 27×103
-Tg（J）•
（21） a.
（22）（I）a =5；
（II）B」=20+40-0，B. =0+202，B=5a+ 100-205-

----2012----

```text
2012 年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）C. （2）A. （3） B. （4）D. （5） D. （6）D. （7） C.（8） B.
二、填空题
（9）1. （10）
TT
4
（11）0. （12） v%. （13） （-1, 0）.（14）-27.
三、解答题
（15）（I）a = 1；
（II）k=1.
（16）极大值f（1,0）=e立，极小值f（-1,0）=-e
（17）D的面积为2，旋转体的体 （ 1）、
16
（18）
15
（19）（I）f（x）= e*；
（I）（0,0）.
（20）证明略.
（21）（I）证明略；
（II）证明略，lim w=
1
2

----2013----

```text
2013年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）C. ：（2）A. （3）C.
（4）D. （5）A. （6）B. （7）B. （8） B.
二、填空题
（9） ve.
（10）
e
e
-1
（ （12）x+y=+
-In 2. （13） e" - e* - xe™. （14） -1.
三、解答题
（15）n=2,a=7.
（16） a =707.
（17）背
（18） （I）证明略；
（I）证明略.
（19） 最长距离、/2，最短距离1.
（20） （I）1；
（II）证明略，lim &n =1.
（21） （I）
（e+1）；

----2014----

```text
2014 年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1） B. （2） C. （3）D. （4）C. （5）D. （6）A. （7）B. （8）A.
二、填空题
（9）3
8•（10）1. （11） -5（dx + dy）.（12）-
+ =0.（13）5
（14）［-2,2J
三、解答题
（15）号
（16） 极大值y（1）=1，极小值y（-1）=0.
3
（17）-
4
1
（18）f（u）=
16
~ （19） （1）证明略；
（II）证明略.
1
e
-2u-
16

----2015----

```text
2015年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）D. （2） B. （3） A. （4） C. （5）D. （6） B. （7）D. （8）A.
二、填空题
（9）48.
（10）n（n-1）（In 2）~2. （11）2.（12）2e+e2.（13）-gd-
-dy.
（14）21.
三、解答题
（15） a =-1,6 =-
， =-
2
3
8
（16）
T
（17）极小值f（0，-1）=-1.
（18） "
（19） f（x）在（-∞，+∞）上共有两个零点.
（20） 30 min.
（21）证明略.
（22） （I）a = 0；
3

----2016----

```text
2016年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）B. （2）D. （3） B. （4） B. （5）A. （6）D. （7）C. （8）C.
二、填空题
（9） = +
T
2‘
（12）5•2 -！
• （13）2J22•（14）2.
三、解答题
（15） e.
（16）f'（x）=
（o -2k，0＜* 1，最小值/（）一卡
×≥1.
（17）极大值f（-1，-1）=1.
（18）1-当•
（19） u（x） = - （2x +1）e-*
，原方程的通解为y=hje* -kz（2x +1），其中K，kz为任意常数
18
16
（20）体积
35™，表面积
-T.

----2017----

```text
2017年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1） A. （2） B. （3）D. （4） C. （5） D. （6）C. （7） B. （8） B.
二、填空题
（9）y=×+2.
（10）-
8
（11）1. （12）xye'. （13） - In（cos 1）.（14） - 1.
三、解答题
（15）号
（16）岁
（17）
14
（18） 极大值y（1）=1，极小值y（-1）=0.
（19）（I）证明略；
（II）证明略.
（20）
5t
4
（21） In（a+y）+2arctan炎 =0, x e （0号）.
（22）（1）证明略；
（II） k（1,2， -1）'+（1,1,1）「 线性方程组Ax=B 的通解，其中 为任意常数.
1

----2018----

```text
2018年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）B. （2）D. （3） D. （4）D. （5）C. （6）C. （7）A. （8）A.
二、填空题
（9）1.（10）y = 4x -3.
（1I） 当m2.（12）号
（13）4（14）2.
三、解答题
（15）C“arctan
（16） （I）f（x） = 2a（1-e-*）；
（I）a=
e
2
（17）3 +5T.
（18）证明略.
（19）三个图形的面积之和存在最小值，最小值为
T+4+30
（20） 10.
（21）证明略，lim *，=0.
，其中 为任意常数
（II）当a 2时，f的规范形 f=分+分＋分；当a=2时，f的规范形为 =2+2.
（23）（I）a = 2；
（II）满足 AP = B 的可逆矩阵为

----2019----

```text
2019年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）C. （2） B. （3）D. （4）D. （5） A. （6）A. （7）A. （8）C.
二、填空题
（9）48. （10）寶+2. （11）功（兴）（12）元加3. （13）=（c0s 1-1）. （14）-4.
三、解答题
fe*（x +1），
* <0，
（15） '（x）=
2e2l*（In x + 1），x>0.
是f（x）的极大值点，极大值为f（0）=1.
3
（16）-2Inx-1-
x-1
+In（x+×+1）+C，其中C为任意常数.
（17）（I）3（x）=vhe号；
（I） 5m（e'-e）.
43.2
（18）
120
（19）Sn=
e-™［1 - e-（n-l） ］
1-e-™

----2020----

```text
2020年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）D. （2）C. （3）A. （4）A. （5）B. （6） B. （7）C. （8）D.
二、填空题
（9） -M. （10）gk
-（2.2-1）. （11）（H-I）dx-dy. （12） gpsa.. （13）1. （14）c*-4c.
三、解答题
（15） 斜渐近线方程为y=
e
1
-+
2e'
xf（x）-l flu）du
（16）g'（x） =
*天0，证明略.
× = 0.
（17）极小值/（合，）=-216
（18）f（x）=
＋X
，旋转体体积光信
（19）3
4
-［ +In（+1）］.

----2021----

```text
2021 年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）C. （2） D. （3）C. （4）A. （5） D. （6） C. （7） B. （8） B. （9）D. （10）C.
二、填空题
（11）
（12）=
（13）1.（14） cos
2
•
"
（15）Cje" +e-号 （Cacos
2
&+Gssin
号x），其中G,G2,C。为任意常数.
（16） -5.
三、解答题
（17）-
条渐近线： =-1， =-×+1与y= 1
22
（19）s=
3，A=4257
9
（20）（I）y（x）=*

----2022----

```text
2022 年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）C （2）D.
（3） B. （4） C. （5） A. （6）D. （7） A. （8） B. （9）D.（10）C.
二、填空题
（11）Je.（12）-3
32
（13）83m
（14）G， +e'（Czcos 2x + Cssin 2x），其中Ci，Cz,C；为任意常数.（15）（16）-1.
三、解答题
（17） -1.
（18）
+ 1
4
（19）1= 2T -2.
（20） （1） （4x -2y）e"；
（21）证明略
1
（22） （1）0 =
0
1
~2
（I）证明略.

----2023----

```text
2023年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）B. （2） D. （3） B. （4）C. （5） C. （6） A. （7）C. （8） D. （9） B. （10）D.
二、填空题
（11）-2.（12）当
F+35.（13）-号.（14） -号.（15）元．（16）8.
三、解答题
（17） （T）y（x） = x（2-Inx）；
（I）点（e，号）处的切线与坐标轴所围成的三角形面积最小，最小值为S（e）=。
（18）f（x,y）有极小值，极小值 f（ e,2k ）=
号，其中KEZ
（19） （I）In（+1）；
（I）n（1-采）.
（20）JSmln 2
（21）（1） 证明略；
（II）证明略
1
（22）（1）4 =
2
0
（I）P=
1 1
0

----2024----
2024 年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1） C. （2） B. （3）D. （4）D. （5） C. （6）A. （7） B. （8）C. （9） D. （10） B.
二、填空题
（12）（1,1）.（13）y -arctan（x+y）+ =0.（14）3le.（15）
（16） -4.
三、解答题
（17）当I3.
（II） 22/3
（19） V（t）的最大值为V（In 2） = 64（4In2+3）.
（20）（I）；
（II）f（u,2）=
U0
25
（21）（T）证明略；
（I）证明略.
（22）（T）a = 1,6 =2；
- （u+1）e™".
50
（I）Q=
内正交矩阵，正交变换×=Qy将f（21，22,2s）化标准形 6y7.
—30—
```

## PDF 第 2 页

----2025----
2025年全国硕士研究生招生考试数学（二）答案速查
一、选择题
（1）A. （2） B. （3） C. （4）C. （5）A. （6）B. （7）D. （8）D. （9）B. （10）D.
二、填空题
（11）2.（12） = ×-1.（13）-
1、
4
（14） e.（15） 5g’- 4xy +3x’-4=0.
（16）h（1,1， -1， - 1）'+（1,0,0,4）「
，其中 为任意常数.
三、解答题
3In2 +T
（17）
10
（18）证明略， '（0）=5．
（19）f（ ， ）=（
+y+2）e~
，该函数有极大值，极大值 f（O，-1）=e.
112
（20）12 -
3
（21） 证明略.
（22）（I）a =4,h的取值范围是（0，+∞）；
1
1


## tool · 2026-11-10T10:09:46Z


Script completed
Wall time 0.1 seconds
Output:

97-因此，
98-=-e-y
99-，解得
100-0z
101-+e-P =0.
102-dy
103-eg.
104-2+1
105-0z +
106-dy
107---（e-n -ey）
108-2 +1
109-应选 A.
110-2已知函数f（x）=esin tdi,g（x）=edt • sin’x，则（
111:（A）x =0是f（x）的极值点，也是g（x）的极值点
112:（B）x =0是f（x）的极值点，（0,0）是曲线y=g（x）的拐点.
113:（C）x = 0是f（x）的极值点，（0,0）是曲线 =f（x）的拐点.
114:（D）（0,0）是曲线y=f（x）的拐点，也是曲线y=g（x）的拐点.
115-答案B.
116:分析本题主要考查极值点与拐点的定义.
117-—5—
118-```
119-
120-## PDF 第 3 页
121-
122-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2025%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=3) · 本机 OCR
123-
124-```text
125:根据极值点与拐点的定义，分别计算 （x）， "（x），g（x），g”（ ），并判断它们在 =0附近的
126:符号即可判定x=0是否极值点，点（0,0）是否为拐点.
127-解）先分析f（x）的性质，分别计算f'（x）， ”（x）.根据链式法则，
128-f'（x）= sin xe*
129-f"（x）= 2xsin xe*
130-+ cos xe” = （2xsin s + cos x）e*
131->0，f（x）单调增加.于是， =0是f（x）的极小值点.或者，也可以由 （0）=0， （0）=1>0以
132-及极值的第二充分条件得到x= 0是f（x）的极小值点.
133-当xE（-8,8）时，xsin x ≥0,cos x >0,f"（x）在（ 8,8）内恒大于0， =f（x）是凹曲线.于
134:是，点（0,0）不是曲线 =f（x）的拐点.
135-再分析g（x）的性质，分别计算g'（x），g”（x）.根据链式法则，
136-g'（x） = sin?xe
137-'+2sin xcos.t e’d= sin’te +sin 28ed，
138-8"（x） =2sin xcos xe + 2xsin' xe + sin 2xe+2c0s28）e°dd
139-=2（sin 2x+ xsin2 ）e+2c0s2 ）e’dt.
140-得，g（x）>0,g（x）单调增加，当 E（0,6）时。。edt>0，結合sin 2 >0可得，g'（x）>0,g（x）
141:单调增加.于是，&=0不是g（x）的极值点.
142-当x E （-8.0）时， sin 2x + xsin’x < 0.le"d < 0,cos 24 > 0,g”（x） <0,y =g（x）是凸曲
143-线，当x E （0,8）时， sin 2x + xsin’x>0, edt > 0,cos2x >0,g”（x）>0,y =g（x）是凹曲线.
144:于是，点（0,0）是曲线 =g（x）的拐点.
145-综上所述，应选 B.
146-么a的取值范围是（）
147-（A）（-2，-1］•
148-（B） （-∞，-1］.
149-（C） （-2,0）.
150-（D）（-∞，0）.
151-（答案）c.
152-分析本题主要考查二阶常系数齐次线性微分方程的解与反常积分的敛散性.
153-根据二阶常系数齐次线性微分方程的解的情况，y（x）共有三种可能性：Cje^ +Cze e
154-，（C」+
155-Czx）ed
156-，e"（G;cos Bxi + Casin Bx）.考虑）
157-x（x）dx的敛散性，可归结为考虑店
158-“edx，lse'dx，
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-15-1+
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-16-9=（）
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-17-C.--
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-18-file+e）
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md:19:A. x=0是f（x）的极值点，也是g（x）的极值点
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md:20:B. x=0是f（x）的极值点，（0,0）是曲线y=g（x）的拐点
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md:21:C.x=0是f（x）的极值点，（0.0）是曲线y=f（x）的拐点
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md:22:D. （0.0） 是曲线y=f（x）的极值点，也是曲线y=g（x）的拐点
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-23-A. （-2，-1］
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-24-B.（-∞，-1］
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-25-C.（-2,0）
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md-26-D.（-∞，0）
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-106-dy
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-107---（e-n -ey）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-108-2 +1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-109-应选 A.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:110:2已知函数f（x）=esin tdi,g（x）=edt • sin’x，则（
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:111:（A）x =0是f（x）的极值点，也是g（x）的极值点
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:112:（B）x =0是f（x）的极值点，（0,0）是曲线y=g（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:113:（C）x = 0是f（x）的极值点，（0,0）是曲线 =f（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-114-（D）（0,0）是曲线y=f（x）的拐点，也是曲线y=g（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-115-答案B.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:116:分析本题主要考查极值点与拐点的定义.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-117-—5—
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-118-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-119-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-120-## PDF 第 3 页
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-121-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-122-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2025%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=3) · 本机 OCR
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-123-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-124-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:125:根据极值点与拐点的定义，分别计算 （x）， "（x），g（x），g”（ ），并判断它们在 =0附近的
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:126:符号即可判定x=0是否极值点，点（0,0）是否为拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-127-解）先分析f（x）的性质，分别计算f'（x）， ”（x）.根据链式法则，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:128:f'（x）= sin xe*
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:129:f"（x）= 2xsin xe*
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:130:+ cos xe” = （2xsin s + cos x）e*
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-131->0，f（x）单调增加.于是， =0是f（x）的极小值点.或者，也可以由 （0）=0， （0）=1>0以
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-132-及极值的第二充分条件得到x= 0是f（x）的极小值点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:133:当xE（-8,8）时，xsin x ≥0,cos x >0,f"（x）在（ 8,8）内恒大于0， =f（x）是凹曲线.于
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-134-是，点（0,0）不是曲线 =f（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-135-再分析g（x）的性质，分别计算g'（x），g”（x）.根据链式法则，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:136:g'（x） = sin?xe
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:137:'+2sin xcos.t e’d= sin’te +sin 28ed，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:138:8"（x） =2sin xcos xe + 2xsin' xe + sin 2xe+2c0s28）e°dd
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:139:=2（sin 2x+ xsin2 ）e+2c0s2 ）e’dt.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:140:得，g（x）>0,g（x）单调增加，当 E（0,6）时。。edt>0，結合sin 2 >0可得，g'（x）>0,g（x）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:141:单调增加.于是，&=0不是g（x）的极值点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:142:当x E （-8.0）时， sin 2x + xsin’x < 0.le"d < 0,cos 24 > 0,g”（x） <0,y =g（x）是凸曲
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:143:线，当x E （0,8）时， sin 2x + xsin’x>0, edt > 0,cos2x >0,g”（x）>0,y =g（x）是凹曲线.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-144-于是，点（0,0）是曲线 =g（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-145-综上所述，应选 B.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-146-么a的取值范围是（）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-147-（A）（-2，-1］•
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-152-分析本题主要考查二阶常系数齐次线性微分方程的解与反常积分的敛散性.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-153-根据二阶常系数齐次线性微分方程的解的情况，y（x）共有三种可能性：Cje^ +Cze e
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-154-，（C」+
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-155-Czx）ed
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:156:，e"（G;cos Bxi + Casin Bx）.考虑）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-157-x（x）dx的敛散性，可归结为考虑店
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-158-“edx，lse'dx，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-159-+8
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-160-ecos Budx,J
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:161:e"sin Bxdx 的敛散性.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-162-解微分方程 2ay’+（a+2）y=0的特征方程为 -2a入 +a +2=0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-163-•若A= 4a’-4（a +2）= 4（a-a-2）>0，则特征方程有两个不同实根A」，A2•此时，微
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-164-—6—
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-165-```
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-183-e'dx，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-184-xe'dx收敛当且仅当入<0，故此时对任一解g（x），y（x）dx均收敛当且
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-185-仅当a =-1.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-186-•若A =4（a’ a-2）＜0，则特征方程有一对共轭复根A12=a a’+a+2i Q土B。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:187:此时，微分方程的解为 y（x）= e"（Cj cos Bxt + Casin Bx），其中c= a,B = v-a'+a +2.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:188:由于e"cos Brdk, J。e“sin Bxdx 收敛当且仅当 a < 0（见注），故此时对任一解g（z），
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-189-y（x）d 均收敛当且仅当！-a-2<0，解得aE（-1,0）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-190-a <0，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-191-因此，应选C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:192:由于|e"cos Bx | ≤ e"， leasin Bx| ≤ ea
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-193-，而当a<0时，o“dx收敛，故此时
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-194-e"cos Budx，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:195:e"sin Bxdx 绝对收敛，从而收敛
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:196:当a =0时，由于lim sin Bx.，Lim cos Bx 均不存在，故
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:197:cos Bxdx,J sin Bxdx均发散.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:198:下面说明当Q>0时，厂ecos Bndr， ［e™sin Pds 发散.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-199-由分部配分法可利/e*os Pendke （0c0wy Ber +/AainmRB）、手是。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-200-e"cos Bxdx =
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:201:Rj + p （acos Bx + Bsin Bsx）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-202-248（号-1）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-203-当n 8
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-204-时，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-205-e" cos Bxdx =+ ∞，进一步可得J。e“cos Bxdx发散.同理可得
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:206:esin Bxdx发散
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:207:因此，e"cos Brdx ， ） esin Brdx 收敛当且仅当 a < 0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-208-—7-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-209-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-210-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-211-## PDF 第 5 页
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1163-解分别计算e2：在x=0处的一阶、二阶导数，并写出e2*的带佩亚诺余项的二阶泰勒公
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1164-式.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1165-于是，（e2in ）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1166-（e‘sm *）'= eoi*•2cos x，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:1167:（e2si*）"=2（e2sin*
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:1168:•cos x）'= 2（2e2ain *cos'x - e2in *sin x）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1169-=2，（e2 ）”
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1170-=4.结合e2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1171-= 1可得，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:1172:e2sin s
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1173-= 1+2x +
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1174--+o（x’）=1 +28 +2x2+o（x）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1175-将（1）式代人已知极限可得，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1176--3= lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:1177:xf（x）-e2sin*+1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1178-4f（x）-2×-2x°+o（x）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1179-1ini+x）+ In（1-x） =5
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1180-In（1-x2）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1181-In（1- ）～-
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1274-D，的极坐标表示为D」=〈（7，②）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1275-=J（x-y）'dady + J（g -z）-dady =2/（x-y）drdy.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1276-Di
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1277-Di
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:1278:OMT≤Asin 8,0 ≤0≤g）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1279-Di
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1280-Di
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-1281-=1（1-2si 8cos e）•4
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:1282:4sin8


## tool · 2026-11-10T10:09:52Z




## tool · 2026-11-10T10:10:07Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:10:12Z




## tool · 2026-11-10T10:10:20Z


Script completed
Wall time 0.1 seconds
Output:

792-，即k=-2.
793-注 =c为偶函数，已知收敛性时，可利用对称性得到。d dx=2 cdx.
794-11
795-lim
796:-*sin nxdx =
797--8•
798-答案
799-应填0.
800-分析），
801-本题主要考查定积分与数列极限的计算.对题给类型的积分，一般可采用分部积
802-分法.
803-解
804:（法一）由分部积分法，可得
805-besin nadx= le-d（-cos mx）=-
806-bed（cos nx） =-
807-当x E［0, 1］时，e EL。.1，lcos nx|≤1，从而
808-Tecos nadx
--
817-+1≤3.
818-从而
819-e'*cos nx
820-+e"cos nxdx
821:lim e-'sin nxdx = lim （
822:（法二）记1。=Jesin nxdx.我们可以计算出。的值，再求lim..
823-一15-
824-分子有界
825-=0.
826-```
--
830-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2009%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=13) · 本机 OCR
831-
832-```text
833-n=
834:Je''sin nxdx =-J,sin nad（e""）=-e"sin nx
835:= - e™*sin nx
836-- ne'*cos nx
837-+n,e'cos nxdx
838-整理得，
839:ncos n + sin n
840-e（n'+1）
841-十
842-+ 1
843-因此，
844-lim In = Lim
845-1-8
846-n-8
847:ncos n + sin n
848-e（n
849--+
850-+1）
851-n+1
852-=0.
853:本题的解题关键是使用分部积分法. 法一和法二都使用了分部积分法.不过法一
854:并没有求出 。e*'sin nxdx的具体表达式，而是通过分部积分对原积分进行恒等变形后，对所
855-得表达式进行估计，从而求得lim
856:e"sin nxdx. 这种做法的计算量较小.
857-12设y= （x）是由方程 y+ ＋1确定的隐函数，则”！
858-答案
859-应填-3.
860-分析
--
1050-X一X
1051-= 0.
1052-分析）
1053-本题主要考查不定积分的计算.
1054:一般来说，积分计算有换元积分法和分部积分法两种方法. 解题时要根据被积函数的特点选
1055-择合适的积分方法，有时候还需要两种方法相结合.
1056-常见的变量代换有三角代换，倒代换以及根式代换等.
1057-① fx, Vax +b）da. 设t= Vax+b.
1058-③ f（x, va+&）du.设x=alan t.

```text
万学海文考研
www.wanxue.cn
2026年全国硕士研究生招生考试（数学二）试题及参考答案
一、选择题：1~10小题，每小题5分，共50分，下列每题给出的四个选项中，只有一个选项是符
合题目要求的，请将所选选项前的字母填在答题卡指定位置.
1.己知当×->0时，ax’+bx +arcsin x 与&1+x—1是等价无穷小，则（）
1
（A） a==，6=-1
（B）a= =1
万子
（0）
（C） a=
，6=-1
【答案】（A）
ax’+ bx +arcsin x =ax’+bx+ + +o（x），
又cx’+bx+arcsin x 与¾1+x2-1是当x->0时的等价无穷小，从而a=
二，b+1=0.故选（A）.
2. 设3（x），32（x） 是某2阶非齐次线性微分方程的两个特解，若常数A,4使得22｝（x）+4422（x）是
该方程的解，2y（x）-2432（x）是该方程对应的齐次方程的解，则（）
（A）九==
2
5
1
（B）入=
（C）2=
2
（D）A=
2：¼=4
【答案】（B）
将2Ay（x）+ （x）代入得，2入＋ =1，
解得入=二
1
M’H=
5，故造（B）.
3. 设函数z=2（x,y）由方程x-az =e'tc（a是非零常数）确定，则（）
（A）18
Ox
Oz
Oy
1
a

```text
淘宝：谈辰教育工作室
2026 考研数学（二）真题
试卷及解析
一、选择题：1~10小题，每小题5分，共50分.下列每题给出的四个选项中，只有一个
选项是符合题目要求的.
1.已知当x->0时，ax’+br +arcsinx 与V1+x2-1是等价无穷小，则
B.Q= b=1
C.a-g
，b=-1.
1.【答案】A
【解析】
由于 ax’+bx +arcsin x 与V1+2-1为等价无穷小，則
故<
6+1=0，
1
a=二，
3
解得<
b=-1
1 故选A.
sympy None
fitz ModuleSpec(name='fitz', loader=<_frozen_importlib_external.SourceFileLoader object at 0x10135c4f0>, origin='/Users/oyamahappa/Library/Python/3.9/lib/python/site-packages/fitz/__init__.py', submodule_search_locations=['/Users/oyamahappa/Library/Python/3.9/lib/python/site-packages/fitz'])


## tool · 2026-11-10T10:10:25Z


Script completed
Wall time 0.1 seconds
Output:

考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【真题】09-26/2016考研数学二真题.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/2021-2026数二真题做题本/打印资料，满5包邮，送草稿纸.png
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:94:4. 设线密度为1的细直棒的两个端点分别位于点（-1.0）和点（1.0）处，质量力m的质点位于
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:95:点（0.1）处，G为引力常量，则该细直棒对该质点的引力大小为
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-96-^. j' 2Gms
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-97-Tdx.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-98-E. f-20m
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-99-dr.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-100-（x+）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-101-（ +）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-102-cf,20mE
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-103-（x+1）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-104-0. f. 20m
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-105-（ +）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-106-4.【答案】D
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:107:【解析】细直棒位于x轴上［-1,1］，取棒上任意微元，微元位置x，XE（-1,1），长度为dr.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-108-由万有引力定律，两质点，（微元与质点）的距离为 = +12=V1+ .
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-109-引力微元dF 的大小为dF =G•—
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-110-md mH=C
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-111-mdr
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-112-（I+8？）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-113-X方向：由于棒关于y轴对称（x与一X处的微元，x分量大小相等、方向相反），故
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-114-引力的水平分力为0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-115-Y方向：引力微元的y分最为dF，=dF cosO，其中 cos0
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-116-（0是引力
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-117-VX+1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-118-方向与y轴的夹角）•
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-119-因此，Y方向的引力微元为：dF， =G.Mdx
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-120--- Gmdy
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-121-X+1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-122-最后积分计算总引力，利用对称性，［-1,0］与［0.1］的引力贡献相同。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-123-因此总引力大小为F=2）。6m
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-124-dx，故选D.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-125-（1+×2）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-126-数学解析 第3页（共16页）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-127-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-128-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-129-## PDF 第 4 页
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:142:5.设函数「（x）在区间［一1，刂上有定义，则
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-143-A. 当f（x）在（一10）单调递减，在（0.1）单调递增时，f（0）是极小值.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-144-B. 当f（0）是极小值时，f（x）在（-1,0）单调递减，在（0,1）单调递增.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-145-5.【答案】C
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-146-但仍满足/（0）是极小值，排除：
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-147-对C选项：若f（x）的图形在［-1,1］上是凹的（即凸函数，二阶导数非负或满足凸性定
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-148-1-×2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-149-数学解析 第4页（共16页）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-150-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-151-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-152-## PDF 第 5 页
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-153-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-154-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2026%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%EF%BC%88%E4%BA%8C%EF%BC%89%E7%9C%9F%E9%A2%98%E8%AF%95%E5%8D%B7%E5%8F%8A%E8%A7%A3%E6%9E%90.pdf#page=5) · 本机 OCR
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-155-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-156-> 读取原 PDF 时出现警告，建议核对原页。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-157-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-158-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-159-淘宝：谈辰教育工作室
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-160-不一1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-161-对D选项，取厂（x）=附时，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-162-J（x）-/④
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-163-单增，但f（x）在［-1， 不是凹曲线，排除.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-164-×-1
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:86:4. 设线密度为1的细直棒的两个端点分别位于点（-1,0）和点（1,0）处，质量为m的质点位于点（0,1）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:87:处，G为引力常量，则该细直棒对该质点的引力大小为（）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-88-Tdt
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-89-（x’+1）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-90-（x2+1）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-91-（B）「
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-92-2Gm
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-93-Tds
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-94-（×2+1）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-95-© C 20m
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-96-（x2+1）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-97-【答案】（D）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:98:【解析】在区间（-1,1）上，该细直棒对质点的引力在x轴方向的分力相互抵消为O，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-99-所以只需考虑在 轴方向的分力，当 x＋dx时，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-100-dF，--Cmdas
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-101-（x2+1）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-102-（x+1）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-103-（x+1）2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-104-故选（D）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md:105:5.设函数f（x）在区间［-1,1上有定义，则（）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-106-（A） 当f（x）在（一1,0）单调递减，在（0,1）单调递增时，f（O）是极小值
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-107-（B） 当f（0）是极小值时，f（x）在（-1,0）单调递减时，在（0,1）单调递增
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-108-【答案】（C）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-109-【解析】对于（A）选项，极值的第一判别法要求f（x）在X=0处连续，故（A）错；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-110-对于（B）选项，考虑函数f（x）= cOs10x，该函数在×=0处取到极小值，但是在（-1,0）和（0,1）都
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-111-不是单调函数．故（B）错；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-112-×-1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-113-2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-114-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-115-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-116-## PDF 第 3 页
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-117-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-118-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2026%E5%B9%B4%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98%E5%8F%8A%E7%AD%94%E6%A1%88.pdf#page=3) · 本机 OCR
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-119-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-120-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-121-万学海文考研
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-122-www.wanxue.cn
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-123-2026 年全国硕士研究生招生考试（数学二）试题及参考答案
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-124-是f"（x）=6x+2在x= 两边异号，所以f（x）的凹凸性改变，故（D）错；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-125-在［-1,1）上单调递增，即证对于任意的
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-126-X一1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md-127-根据凹函数的定义：对于任意的x， E［-1,1］， y，AE（0,1），都有


## tool · 2026-11-10T10:10:31Z


Script completed
Wall time 0.1 seconds
Output:

2378-
2379:% Q 2023 6
2380-\QuestionPage{2.6 函数性态的研究}{选择题}{2023 年第 6 题}{1}{积分函数的最小值}{113 / 408}
2381-若函数
2382-\[f(a)=\int_2^{+\infty}\frac{1}{x(\ln x)^{a+1}}\,dx
2383-\]
2384-在 \(a=a_0\) 处取得最小值，则 \(a_0=\)（ ）。
2385-\choices{\(-\dfrac{1}{\ln(\ln 2)}\)}{\(-\ln(\ln 2)\)}{\(\dfrac{1}{\ln 2}\)}{\(\ln 2\)}
2386-\QuestionEnd
2387-
2388-\begin{QuestionSolution}{2023 年第 6 题}
2389-\textbf{入手角度}\quad 用 \(u=\ln x\) 把反常积分化为幂函数积分，先确定收敛域，再对参数求导。
2390-
2391-\textbf{解析}\quad 换元得 \(\int_{\ln2}^{\infty}u^{-a-1}\,du\)，仅当 \(a>0\) 收敛。此时
2392-\[
2393-f(a)=\frac{(\ln2)^{-a}}a,\qquad
2394-\frac{f'(a)}{f(a)}=-\ln(\ln2)-\frac1a.
2395-\]
2396-因 \(\ln(\ln2)<0\)，导数在 \(a=-1/\ln(\ln2)\) 左侧为负、右侧为正，故该点取得全局最小值。答案为 \(\boxed{a_0=-1/\ln(\ln2)}\)，选 A。
453-= lim
454-x-0
455-3c00w）
456-3
457-由于 ”（0） f（0），故 （0）不存在.选项C正确，选项D不正确.
458-综上所述，应选C.
459:6
460-若函数f（a）=
461-1
462-（A）-
463-In（In 2）
464-*（In ）arde 在c =co处取得最小值，则Q=（）
465-（B） - In（In 2）.
466-（C）
467-In 2
468-（D）In2.
469-答案
470-A.
471-分析）本题主要考查反常积分的计算与一元函数的最值问题.
472-f（a）由反常积分给出，计算该反常积分，可以得到f（a）的定义域以及表达式.进一步，计算
473-f'（a），分析f（a）的单调性可得其最小值点.
474-解）当～ =0时，
475-f（a）=5
476-dx =
477-xin x
--
658-X=-A-'B-
659-，从而
660-BX，=0，
661-X；=0，
662-BX4=E.
663-X=B-
664:6
665-E
666-B
667-=
668-（ AB
669-（法二）分别记选项A、B、C、D 中的矩阵为M，，M.，M，M.，记A
670-2,3,4）.若M， =M*，则M,M= |A1|B| E20•
671-观察可得 M,M 与M、M的“第一列”均为（1A！召A）
672-M,M*AIBEzn，
673-MM IABE20
674-E
675-B
676-=M. 考虑MM（i=1，
677-选项A、B均不正确，
678-又因为
679-（1BA
680--B*A*YA
681-A B
682-E
--
1156-b
1157-1
1158-因此，
1159-1
1160-a
1161-2
1162:6
1163-= 8.
1164-0
1165-fax， +%s = 1，
1166-（法二）记方程组/*」+at2+ s
1167-= 0，
1168-X1+2%2 + axs =0，
1169-ax」+bx2=2
1170-的系数矩阵为A，增广矩阵为（A,b）.由方程组有解可
1171-—20
1172-```
1173-
1174-## PDF 第 18 页
1175-
1176-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2023%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=18) · 本机 OCR
1177-
1178-> 读取原 PDF 时出现警告，建议核对原页。
1179-
1180-```text
--
1219-Q
1220-=A 0.
1221-1
1222-2
1223-a
1224-Q
1225:6
1226-0
1227-1
1228-0
1229-1
1230-1
1231-0
1232-0
1233-1
1234-0
1235-a
1236-1
1237-对方程组I使用克拉默法则可得&」
1238-2
1239-a
1240-0
1241-2
1242-4
1243-a
.question-bank-work/solutions/001-113.tex-1027-
.question-bank-work/solutions/001-113.tex:1028:% SOLUTION 113 2023 6
.question-bank-work/solutions/001-113.tex-1029-\textbf{入手角度}\quad 用 \(u=\ln x\) 把反常积分化为幂函数积分，先确定收敛域，再对参数求导。
.question-bank-work/solutions/001-113.tex-1030-
.question-bank-work/solutions/001-113.tex-1031-\textbf{解析}\quad 换元得 \(\int_{\ln2}^{\infty}u^{-a-1}\,du\)，仅当 \(a>0\) 收敛。此时
.question-bank-work/solutions/001-113.tex-1032-\[
.question-bank-work/solutions/001-113.tex-1033-f(a)=\frac{(\ln2)^{-a}}a,\qquad
.question-bank-work/solutions/001-113.tex-1034-\frac{f'(a)}{f(a)}=-\ln(\ln2)-\frac1a.
.question-bank-work/solutions/001-113.tex-1035-\]
.question-bank-work/solutions/001-113.tex-1036-因 \(\ln(\ln2)<0\)，导数在 \(a=-1/\ln(\ln2)\) 左侧为负、右侧为正，故该点取得全局最小值。答案为 \(\boxed{a_0=-1/\ln(\ln2)}\)，选 A。
.question-bank-work/solutions/001-113.tex-1037-
.question-bank-work/solutions/001-113.tex-1038-


## tool · 2026-11-10T10:10:36Z




## tool · 2026-11-10T10:10:44Z


Script completed
Wall time 0.2 seconds
Output:

[('2025考研数学二真题.pdf', [(1, 0), (2, 0), (3, 0)]), ('2025数二真题【解析】.pdf', [(1, 447), (2, 830), (3, 1537), (4, 1853)]), ('2023考研数学二真题.pdf', [(1, 1057), (2, 997), (3, 376), (4, 366)]), ('2023数二真题【解析】.pdf', [(1, 498), (2, 1006), (3, 1367), (4, 1024)])]
[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2023%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=1) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
2023年全国硕士研究生招生考试数学（二）试题
一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目
要求，把所选项前的字母填在题后的括号内.）
（1）曲线y二sbn（e+ - ）的斜渐近线方程为（
）
（A）y=x+e.
（B） =$+
1
€
（C）y=$.
e
01 -05题
APP 扫码听课
（2）函数f（x）=
+x
（x +1）cos x，
31-，原方程的通解为y=hje* -kz（2x +1），其中K，kz为任意常数
32-18
33-16
34-（20）体积
35-35™，表面积
36--T.
37-5
38:（21）（I） 平均值
39-3元；
40-（II）证明略.
41-（22）（I）a = 0；
42-（II）h（0， -1,1）'+（1， -2,0）"
43-，其中h为任意常数.
44-（299 -2
45-1 -299
46-2-298
--
852-是f（x）在（0，+∞）上的最小值点时，我们强调了f（x）的连续
853-性.若f（x）不连续，则×=
854-可能不是最小值点.考虑下面的例子.令g（x）=
855-［（a-号），o<*<二，
856-8（x）在（步，1）和（1，+∞）内均单调增加，在（0，之）内单调减
857-*-g，
858-×≥1.
859-少，但8（一）不是8（x）在（0， + ∞）上的最小值
860:② 在求f！（1）和f：（1）时，我们可以使用2009年第（21）题第（I）问中的结论的推广：
861-若函数f（x）在 =a处连续，在（a,a+8）（8>0）内可导，且limf（x）= A，則 （a）
862-存在，且f！（a）=A.
863-由于f（x）在x=1处连续，且4x-2x和2x 在×=1处均连续，故
864-—18—
865-```
866-
867-## PDF 第 16 页
868-
--
1185--37（好 好）d=3m（号-号）=3m
1186-下面计算S2.
1187-=3升-号（1-1）号。
1188--Wa=
1189-因此，V=3
1190-27 知函数 ）在［o.3上连续，在（0.3g）内是函数
1191-28-3T
1192-的一个原函数，且f（O）=0.
1193:（I）求/x）在区间［o，3］上的平均值；
1194-（I）证明 ）在区间（0.3）内存在唯一零点.
1195-—24—
1196-```
1197-
1198-## PDF 第 22 页
1199-
1200-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2016%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=22) · 本机 OCR
1201-
1202-```text
1203:分析本题综合考查了原函数、函数在区间上的平均值以及积分中值定理等知识
1204-积分中值定理 若函数f（x）在［a，6］上连续，则在［a，6］上至少存在一点专，使得
1205-Jfa）d =fE）（6-a）.
1206-若f（x）≥0，则左端积分所表示的曲边梯形的面积等于以［a，6］
1207-积分中值定理的几何意义
1208-为底，以f（ ）为高的矩形面积.
1209-6-a
1210-一.由积分中值定理可知，f（ ）即f（x）在
1211:［a, 6］上的平均值
1212:要求函数在10，当］上的平均值，可以先根据定义写出平均值的表达式，然后再考虑如何计算。
1213-第（II）问是利用导数来分析函数的零点、单调性等性质的综合问题.由已知条件可知f（x）的
1214-导数f“（x）=28-3元，于是可以利用它来分析f（z）的单调性。
1215-（I）由于f（x）是
1216-2x -3T
1217-的一个原函数，故不妨设 （ ）=10
1218--dt +C. 由f（0） =0
1219-2t-3m
1220-可知，C=0. 于是，f（x）=J。
1221-COS
1222-t
1223--dt.
1224-2t -3元
1225-根据 （ ）在区间［o.習
1226:上的平均值的定义，可知
1227-A=
1228-f（x）dx
1229-3m
1230-2
1231-2t -3m
1232--de） dsx
1233-3m
1234-2


## tool · 2026-11-10T10:10:48Z


Script completed
Wall time 0.2 seconds
Output:

                                                                                                                                             兀父                                                             0                   f(x)                                           ··  f                                                                                                                                  ，解得一＝-
                                            =                                                  e_Y2)                  =                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             的极值点，也是g(x)    的极值点，（0,0)    的极值点，（0,0)                    x,y)     e_Y2). _                                       -',e2025           z( -                     -                                            一无2       =     一无2                     =                          f(x)                                                                                                                                                                                                       是曲线y                          (e  1                                                                            竺＝产，解得扣如如        !!!-扣ay                                                是J(x)  是J(x)  是f(x)
         1 +           1       1           0 0 0         z+  ~(ez             +z    +z        ===
          -                                艾函数z  z  "t一、选择题         (A)   (C)   豆A.    立本题主要考查隐函数的偏导数的计算      对已知方程两端分别关于x                             雹对巳知方程两端关于x                                                                      同理，对已知方程两端关于y                 因此，                       日已知函数  (A)x (B)x (C)x   (D)(O,O) 豆B.   磋湮）本题主要考查极值点与拐点的定义                                                                 扣扣如切的表达式                    整理可得z                           整理可得z                     应选A.
  2023年全国硕士研究生招生考试数学(二)试题


一、选择题(本题共10小题,每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目

  要求，把所选项前的字母填在题后的括号内.)
(1)曲线y = %ln(e +-L-)的斜渐近线方程为(        )
                            \    % - 1  /

    (A)y = x + e.                          (B)y = x
                                                                                                               01 - 05 题
    (C)y = x.                            (D)y = x                APP扫码听课


                 --- ----         先 W 0
  函数 _/■(.)=  71 +2       的一个原函数为(

                  (% + 1 ) COS X,   X > 0

               ln(Jl + x2 - x),       % W 0,   (A)F(%)=
                 [(先 + 1)cos x - sin %,   x > 0.

                    ln( a/1 + x2 - x) + 1,   % W 0,    (B)F(x) =         •
                  (% + 1)cos x 一 sin x,   x > 0.

                    ln( a/1 + x2 + %),       % W 0,    (C)F(x) =         •
                  (x + 1)sin x + cos x,   % > 0.

               ln(Jl + x2 + x)  4- 1,  久W 0,   (D)F(x)=
                  (% + 1)sin x + cos x,    % > 0.
(3)已知数列｛xn \  ,  j yn  | 满足幻== y,x„+1 = sin x„ ,y„+I   y^(n = 1,2,…)，则当 zi 一'8 时,

      (         )
  (A)%n是以的高阶无穷小.            (B)*  是先几的高阶无穷小.
  (C)%„是心的等价无穷小.          (D)%是九的同阶但非等价无穷小.
(4)若微分方程*" + " +奶=0的解在(- 8  , + 8 )上有界，则(         )
   (A)a <0,6 >0.     (B)a >0,6 >0.     (C)a =0,6 >0.     (D)a =0,6 <0.
(5)设函数y =/(x)由确定，则(        )
                                         I*  =         I t    \ sin t
   (A)/(x)连续，尸(0)不存在.         (B)r(0)存在，尸(％)在，=0处不连续.
  (C)广⑴ 连续,r(o)不存在.            (D)/ff(0)存在,_/■"(/)在％ = 0处不连续.
(6)若函数Ha) =   I广+ 8 —-----1     dx 在 a = %处取得最小值，则％ =           )
                              In X)
                                         (C)h?2-   (A)~ ln(ln2)'      (B) -ln(ln2).                          (D)ln 2.     06 - 10 题
                                                         APP扫码听课

                    —1   考研电子版网站：www.pdf2book.com


## tool · 2026-11-10T10:10:54Z




## tool · 2026-11-10T10:11:02Z


Script completed
Wall time 0.1 seconds
Output:

170-11 -16题
171-APP 扫码听课
172-（13）设函数z=z（x，J）由方程（x+1）z +yln z - arctan（2xy） = 1确定，则”
173-（0,2）
174-（14）已知函数 ）二），此sin
175:（15）微分方程y"-y=0的通解为y=
176-X
177-x
178-1
179-X
180-2
--
216-（19）（本题满分12分）
217-设函数f（ ））满足厂比 d
218-6
219-x轴旋转一周所形成的曲面面积为A，求和A.
220-（20）（本题满分12分）
221:设函数y=y（x）（ >0）满足微分方程xy’ 6y = 6，，且满足y（3）= 10.
222-（I）求y（x）；
223-20 -22题
224:（II）P 曲线 = （x）上的一点，曲线 =y（x）在点P的法线在y轴上截距
225-APP 扫码听课
226-为1p，为使1，最小，求P的坐标.
227-一3-
228-```
229-
155--dxdy.
156-D
157-18-20题
158-APP 扫码听课
159-（19）（本题满分10分）
160:已知yi（x）=e*，32（x）=u（x）e*是二阶微分方程（2 -1） （2×+1） ’+2y=0的两个
161-解.若u（-1）= e, u（0）=-1，求u（x），并写出该微分方程的通解.
162-（20）（本题满分11分）
163-设D是由曲线 =v1 （0≤ ≤1）与
164-/x =cosk（o≤1≤”）围成的平面区域，求D绕
165-ly = sin2e


## tool · 2026-11-10T10:11:15Z


Script completed
Wall time 0.1 seconds
Output:

{174: 4.3301184859956265e-09, 177: 9.495089159372583e-09, 182: 3.670885373452393e-08, 184: 6.41257047462318e-10, 185: 2.7271198632661253e-08, 187: 2.23487894857044e-12, 188: 1.0627987379052684e-10, 234: 6.898214133244096e-07}


## tool · 2026-11-10T10:11:20Z




## assistant · 2026-11-10T10:11:28Z

第 114–234 题的 121 份解析已写入 [中间稿](/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/solutions/114-234.tex)。逐题核对了序号、年份和原卷题号，并对八道积分题做了独立数值复算。

已报告三处影响解答的题面转录问题，涉及第 115 题的被积函数、第 215 题的定义域和第 233 题的二阶导数。第 214 题按原解析将导数严格为正的条件用于 \(x>0\)。本中间稿未单独编译。
