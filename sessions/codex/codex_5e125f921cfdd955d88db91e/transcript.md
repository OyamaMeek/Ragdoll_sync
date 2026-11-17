# 01a1c4e2-6a04-7210-9e0e-9e6f722c28c3

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-10T09:55:38Z

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


## developer · 2026-11-10T09:55:38Z

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
- mcp__ot
- mcp__pubmed
- mcp__rea: REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly answers the question; discover targets or inspect inventory only when needed. Tool results include i...
</tools>

## developer · 2026-11-10T09:55:38Z

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

## developer · 2026-11-10T09:55:38Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-10T09:55:38Z

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

## developer · 2026-11-10T09:55:38Z

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


## developer · 2026-11-10T09:55:39Z

<tools>
Added deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
</tools>

## assistant · 2026-11-10T09:55:42Z

我会按原题顺序核对第 001–113 题，逐题写出解题切入点和推导，并单独标记需要核对的转录问题。

## tool · 2026-11-10T09:55:44Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"494500","wall_time_seconds":0.000007916,"exit_code":0,"original_token_count":567,"output":"121:% Q 2024 3\n122:\\QuestionPage{1.1 集合、映射与函数}{选择题}{2024 年第 3 题}{1}{函数的奇偶性}{001 / 408}\n143:% Q 2012 3\n155:% Q 2017 3\n166:% Q 2022 6\n172:% Q 2023 3\n181:% Q 2024 4\n187:% Q 2012 10\n193:% Q 2011 19\n204:% Q 2012 21\n215:% Q 2013 20\n226:% Q 2018 21\n242:% Q 2011 9\n247:% Q 2013 9\n252:% Q 2019 9\n257:% Q 2022 11\n262:% Q 2011 15\n278:% Q 2009 2\n289:% Q 2011 1\n300:% Q 2012 1\n311:% Q 2013 1\n323:% Q 2014 1\n335:% Q 2014 2\n346:% Q 2016 1\n358:% Q 2019 1\n369:% Q 2020 1\n375:% Q 2021 1\n381:% Q 2022 1\n392:% Q 2023 1\n401:% Q 2025 4\n407:% Q 2026 1\n413:% Q 2010 10\n418:% Q 2016 9\n423:% Q 2017 9\n428:% Q 2023 11\n441:% Q 2025 12\n446:% Q 2012 15\n455:% Q 2013 15\n460:% Q 2015 15\n466:% Q 2020 15\n483:% Q 2009 1\n494:% Q 2010 1\n505:% Q 2015 2\n517:% Q 2015 3\n531:% Q 2017 1\n545:% Q 2018 3\n563:% Q 2020 2\n569:% Q 2024 1\n583:% Q 2010 3\n594:% Q 2011 2\n606:% Q 2018 2\n617:% Q 2021 2\n630:% Q 2025 7\n641:% Q 2009 9\n649:% Q 2022 17\n656:% Q 2025 18\n670:% Q 2012 2\n681:% Q 2013 2\n693:% Q 2021 3\n699:% Q 2023 5\n711:% Q 2024 2\n728:% Q 2026 6\n737:% Q 2009 12\n743:% Q 2010 11\n748:% Q 2010 13\n754:% Q 2012 9\n760:% Q 2013 10\n766:% Q 2013 12\n774:% Q 2014 10\n779:% Q 2014 12\n785:% Q 2015 9\n793:% Q 2015 10\n798:% Q 2016 13\n804:% Q 2017 10\n812:% Q 2019 10\n820:% Q 2019 13\n825:% Q 2020 9\n837:% Q 2021 12\n850:% Q 2022 12\n857:% Q 2023 14\n867:% Q 2024 14\n877:% Q 2025 14\n884:% Q 2010 17\n893:% Q 2018 20\n914:% Q 2014 5\n925:% Q 2017 2\n936:% Q 2018 9\n941:% Q 2009 21\n951:% Q 2010 21\n958:% Q 2013 18\n967:% Q 2015 21\n975:% Q 2017 15\n980:% Q 2017 19\n989:% Q 2019 21\n1002:% Q 2023 21\n1015:% Q 2024 21\n1035:% Q 2018 1\n1046:% Q 2020 4\n1052:% Q 2021 5\n1058:% Q 2022 3\n1064:% Q 2026 12\n1070:% Q 2009 15\n1075:% Q 2014 15\n1082:% Q 2016 15\n1087:% Q 2021 17\n1102:% Q 2011 3\n1113:% Q 2014 3\n1124:% Q 2015 4\n1144:% Q 2016 4\n1201:% Q 2018 4\n1212:% Q 2019 2\n1223:% Q 2020 6\n1229:% Q 2021 4\n1235:% Q 2023 6\n1236:\\QuestionPage{2.6 函数性态的研究}{选择题}{2023 年第 6 题}{1}{积分函数的最小值}{113 / 408}\n1244:% Q 2023 7\n1245:\\QuestionPage{2.6 函数性态的研究}{选择题}{2023 年第 7 题}{2}{极值点与拐点的参数条件}{114 / 408}\n1253:% Q 2025 2\n1259:% Q 2026 5\n1265:% Q 2009 13\n1270:% Q 2018 10\n1275:% Q 2010 15\n1280:% Q 2011 16\n1288:% Q 2012 20\n1293:% Q 2015 19\n"}
{"chunk_id":"8bd837","wall_time_seconds":0.000008,"exit_code":0,"original_token_count":540,"output":"302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2009数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2018数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2010数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2017数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2020数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2012数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2011数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2023数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2014数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2024数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md\n302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026年数学二真题及答案.md\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\n"}

## tool · 2026-11-10T09:55:48Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2024 3
\QuestionPage{1.1 集合、映射与函数}{选择题}{2024 年第 3 题}{1}{函数的奇偶性}{001 / 408}
已知
\[f(x)=\int_0^{\sin x}\sin t^3\,dt,\qquad
g(x)=\int_0^x f(t)\,dt,
\]
则（ ）
\choices{\(f(x)\) 为奇函数，\(g(x)\) 为奇函数}{\(f(x)\) 为奇函数，\(g(x)\) 为偶函数}{\(f(x)\) 为偶函数，\(g(x)\) 为偶函数}{\(f(x)\) 为偶函数，\(g(x)\) 为奇函数}
\QuestionEnd

\SectionHeading{1.2}{函数、极限、连续}{数列的极限}{定理与要点\quad 教材 PDF 第 41 页起\hfill 本节 10 题}
\pdfbookmark[2]{1.2 数列的极限}{section-1.2}
\Theory{定理 2.1}{46}{唯一性}{收敛数列只有一个极限。}
\Theory{定理 2.2}{47}{有界性}{收敛数列必有界。}
\Theory{定理 2.3}{47}{有理运算法则}{两收敛数列可逐项作和、差、积、商再取极限，取商时分母极限须非零。}
\Theory{定理 2.4}{49}{保号性}{数列收敛到非零值时，从某一项起与极限同号，并且绝对值离零有正的下界。}
\Theory{定理 2.5}{49}{夹逼性}{两端数列收敛到同一值时，最终被夹在其间的数列也收敛到该值。}
\Theory{定理 2.6}{51}{单调有界准则}{单调增且有上界，或单调减且有下界的数列必收敛。}
\Theory{定理 2.7}{54}{子列与极限}{数列收敛到 a，当且仅当其每个子列都收敛到 a。}
\Theory{定理 2.8}{54}{闭区间套定理}{逐级包含且长度趋于零的非空闭区间列，恰有一个公共点。}
\Theory{定理 2.9}{55}{Weierstrass 定理}{有界实数列至少有一个收敛子列。}
\Theory{定理 2.10}{56}{Cauchy 收敛原理}{实数列收敛，当且仅当任给正误差，充分靠后的任意两项之差的绝对值都小于该误差。}
% Q 2012 3
\QuestionPage{1.2 数列的极限}{选择题}{2012 年第 3 题}{1}{数列与部分和的收敛}{002 / 408}
设$a_n > 0$($n = 1,2, \cdots$)，$S_n = a_1 + a_2 + \cdots + a_n$，
则数列$\{s_n\}$有界是数列$\{a_n\}$收敛的\pickout{}
\begin{abcd}
\item 充分必要条件．
\item 充分非必要条件．
\item 必要非充分条件．
\item 即非充分也非必要条件．
\end{abcd}
\QuestionEnd

% Q 2017 3
\QuestionPage{1.2 数列的极限}{选择题}{2017 年第 3 题}{1}{收敛数列的性质}{003 / 408}
设数列$\left\{x_n \right\}$收敛，则\pickout{}
\begin{abcd}
\item 当$\lim_{n \to \infty} \sin x_n = 0$时，$\lim_{n \to \infty} x_n = 0$．
\item 当$\lim_{n \to \infty} (x_n + \sqrt{\left| x_n \right|}) = 0$时，$\lim_{n \to \infty} x_n = 0$．
\item 当$\lim_{n \to \infty} (x_n + x_n^2) = 0$时，$\lim_{n \to \infty} x_n = 0$．
\item 当$\lim_{n \to \infty} (x_n + \sin x_n) = 0$时，$\lim_{n \to \infty} x_n = 0$．
\end{abcd}
\QuestionEnd

% Q 2022 6
\QuestionPage{1.2 数列的极限}{选择题}{2022 年第 6 题}{1}{递推数列的性质}{004 / 408}
设数列 \(\left\{ x_{n} \right\}\) 满足 \(- \frac{\pi}{2} \le x_{n} \le \frac{\pi}{2}\)，则 \(\left( \ \right)\)
\choices{若 \(\lim_{n \to \infty} \cos\left( \sin x_{n} \right)\) 存在，则 \(\lim_{n \to \infty} x_{n}\) 存在}{若 \(\lim_{n \to \infty} \sin\left( \cos x_{n} \right)\) 存在，则 \(\lim_{n \to \infty} x_{n}\) 存在}{若 \(\lim_{n \to \infty} \cos\left( \sin x_{n} \right)\) 存在，则 \(\lim_{n \to \infty} \sin x_{n}\) 存在，但 \(\lim_{n \to \infty} x_{n}\) 不一定存在}{若 \(\lim_{n \to \infty} \sin\left( \cos x_{n} \right)\) 存在，则 \(\lim_{n \to \infty} \cos x_{n}\) 存在，但 \(\lim_{n \to \infty} x_{n}\) 不一定存在}
\QuestionEnd

% Q 2023 3
\QuestionPage{1.2 数列的极限}{选择题}{2023 年第 3 题}{1}{递推数列与无穷小比较}{005 / 408}
已知数列 \(\{x_n\}\)，\(\{y_n\}\) 满足
\[x_1=y_1=\frac12,\qquad x_{n+1}=\sin x_n,\qquad y_{n+1}=y_n^2\quad (n=1,2,\cdots),
\]
则当 \(n\to\infty\) 时，（ ）。
\choices{\(x_n\) 是 \(y_n\) 的高阶无穷小}{\(y_n\) 是 \(x_n\) 的高阶无穷小}{\(x_n\) 与 \(y_n\) 是等价无穷小}{\(x_n\) 与 \(y_n\) 是同阶但不等价的无穷小}
\QuestionEnd

% Q 2024 4
\QuestionPage{1.2 数列的极限}{选择题}{2024 年第 4 题}{1}{数列极限的敛散性}{006 / 408}
已知数列 \(\{a_n\}\)（\(a_n\ne 0\)），若 \(\{a_n\}\) 发散，则（ ）
\choices{\(\left\{a_n+\frac{1}{a_n}\right\}\) 发散}{\(\left\{a_n-\frac{1}{a_n}\right\}\) 发散}{\(\left\{e^{a_n}+\frac{1}{e^{a_n}}\right\}\) 发散}{\(\left\{e^{a_n}-\frac{1}{e^{a_n}}\right\}\) 发散}
\QuestionEnd

% Q 2012 10
\QuestionPage{1.2 数列的极限}{填空题}{2012 年第 10 题}{2}{和式型数列极限与夹逼准则}{007 / 408}
计算$\lim_{x \to \infty} n\left(\frac{1}{1 + n^2} + \frac{1}{2^2 + n^2}
+ \cdots + \frac{1}{n^2 + n^2} \right) =$ \blank{}．
\QuestionEnd

% Q 2011 19
\QuestionPage{1.2 数列的极限}{解答题}{2011 年第 19 题}{3}{调和和式与数列收敛}{008 / 408}
\begin{enumerate}
\item
证明：对任意的正整数$n$，都有$\frac{1}{n + 1} < \ln \left(1 + \frac{1}{n} \right) < \frac{1}{n}$成立．
\item
设$a_n = 1 + \frac{1}{2} + \cdots + \frac{1}{n} - \ln n$（$n = 1,2, \cdots$），
证明数列$\left\{a_n \right\}$收敛．
\end{enumerate}
\QuestionEnd

% Q 2012 21
\QuestionPage{1.2 数列的极限}{解答题}{2012 年第 21 题}{4}{实根构成的数列极限}{009 / 408}
\begin{enumerate}
\item
证明方程$x^n + x^{n - 1} + \cdots + x = 1$（$n$为大于$1$的整数）
在区间$\left(\frac{1}{2},1 \right)$内有且仅有一个实根；
\item
记(I)中的实根为$x_n$，证明$\lim_{n \to \infty} x_n$存在，并求此极限．
\end{enumerate}
\QuestionEnd

% Q 2013 20
\QuestionPage{1.2 数列的极限}{解答题}{2013 年第 20 题}{3}{不等式约束下的数列极限}{010 / 408}
设函数$f(x) = \ln x + \frac{1}{x}$．
\begin{enumerate}
\item
求$f(x)$的最小值；
\item
设数列$\{x_n\}$满足$\ln x_n + \frac{1}{x_{n + 1}} < 1$，证明$\lim_{n \to \infty} x_n$存在，并求此极限．
\end{enumerate}
\QuestionEnd

% Q 2018 21
\QuestionPage{1.2 数列的极限}{解答题}{2018 年第 21 题}{4}{递推数列的收敛与极限}{011 / 408}
设数列$\left\{x_n \right\}$满足：$x_1 > 0$，$x_n \mathrm{e}^{x_{n + 1}} = \mathrm{e}^{x_n} - 1$（$n = 1,2, \cdots$）．
证明$\left\{x_n \right\}$收敛，并求$\lim_{n \to \infty} x_n$．
\QuestionEnd

\SectionHeading{1.3}{函数、极限、连续}{函数的极限}{定理与要点\quad 教材 PDF 第 60 页起\hfill 本节 5 题}
\pdfbookmark[2]{1.3 函数的极限}{section-1.3}
\Theory{定理 3.1}{65}{Heine 定理}{去心邻域内，函数极限等于 a，当且仅当沿任意趋于该点的数列，函数值都趋于 a。}
\Theory{定理 3.2}{66}{唯一性与局部有界性}{函数的有限极限唯一，且函数在相应去心邻域内有界。}
\Theory{定理 3.3}{67}{保号、保序和夹逼}{非零极限在局部保号。局部大小关系传给极限，两端极限相同即可夹逼。}
\Theory{定理 3.4}{67}{有理运算法则}{和、差、积的极限由各自极限运算得到。商的分母极限须非零。}
\Theory{定理 3.5}{69}{复合函数的极限}{内层趋于 u\textsubscript{0} 且在去心邻域内避开 u\textsubscript{0} 时，可应用外层在 u\textsubscript{0} 的极限。}
\Theory{定理 3.6}{73}{单调有界准则}{在右半无限区间单调增且有上界或单调减且有下界时，右端极限存在。单调函数在区间内点有左右极限。}
\Theory{定理 3.7}{74}{Cauchy 收敛原理}{有限极限存在，当且仅当充分接近目标点的任意两处函数值都可彼此任意接近。}
\Theory{公式}{70--72}{两个重要极限}{x \ensuremath{\to} 0 时 sin x / x \ensuremath{\to} 1。u \ensuremath{\to} 0 时 (1 + u)\textasciicircum{}(1/u) \ensuremath{\to} e。}
% Q 2011 9
\QuestionPage{1.3 函数的极限}{填空题}{2011 年第 9 题}{1}{函数极限}{012 / 408}
$\lim_{x \to 0} \left(\frac{1 + 2^x}{2} \right)^{\frac{1}{x}} =$ \blank{}．
\QuestionEnd

% Q 2013 9
\QuestionPage{1.3 函数的极限}{填空题}{2013 年第 9 题}{2}{指数型函数极限}{013 / 408}
$\lim_{x \to 0} \left(2 - \frac{\ln(1 + x)}{x} \right)^{\frac{1}{x}} =$ \blank{}．
\QuestionEnd

% Q 2019 9
\QuestionPage{1.3 函数的极限}{填空题}{2019 年第 9 题}{1}{指数型函数极限}{014 / 408}
$\lim_{x \to 0} \left(x + 2^x \right)^{\frac{2}{x}} =$ \blank{}．
\QuestionEnd

% Q 2022 11
\QuestionPage{1.3 函数的极限}{填空题}{2022 年第 11 题}{2}{指数型函数极限}{015 / 408}
\(\lim_{x \to 0} \left( \frac{1 + e^{x}}{2} \right)^{\cot x} = \blank{}\)
\QuestionEnd

% Q 2011 15
\QuestionPage{1.3 函数的极限}{解答题}{2011 年第 15 题}{2}{两处函数极限与参数}{016 / 408}
已知函数$F(x) = \frac{\int_0^x \ln(1 + t^2)\,\mathrm{d} t}{x^a}$，
设$\!\!\lim_{x \to +\infty}\!\!\! F(x) = \!\lim_{x \to 0^+}\! F(x) = 0$，试求$a$的取值范围．
\QuestionEnd

\SectionHeading{1.4}{函数、极限、连续}{无穷小量与无穷大量}{定理与要点\quad 教材 PDF 第 77 页起\hfill 本节 23 题}
\pdfbookmark[2]{1.4 无穷小量与无穷大量}{section-1.4}
\Theory{定理 4.1}{78}{极限与无穷小}{f 趋于有限值 a，当且仅当 f 可写成 a 加一个无穷小。}
\Theory{定理 4.2}{78}{无穷小的和与积}{在同一变化趋势下，有限个无穷小的代数和及乘积仍为无穷小。}
\Theory{定理 4.3}{78}{有界量乘无穷小}{局部有界函数乘无穷小，结果仍为无穷小。}
\Theory{定理 4.4}{81}{等价无穷小}{两非零无穷小等价，表示两者之差相对于其中任一量为高阶无穷小。}
\Theory{定理 4.5}{82}{无穷小等价代换}{求商的极限时，分子和分母的无穷小因子可分别换成各自的等价量。}
\Theory{定理 4.6}{84}{倒数关系}{非零无穷小的倒数为无穷大量，无穷大量的倒数为无穷小。}
\Theory{定理 4.7}{84}{无穷大量的运算}{有限个无穷大量的乘积仍是无穷大量。无穷大量与有界量的和仍是无穷大量。}
\Theory{公式}{82--85}{常用等价式与渐近线}{x \ensuremath{\to} 0 时 sin x \ensuremath{\sim} x，1 \ensuremath{-} cos x \ensuremath{\sim} x\textsuperscript{2}/2。求斜渐近线可依次取 f(x)/x 和 f(x) \ensuremath{-} kx 的极限。}
% Q 2009 2
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2009 年第 2 题}{1}{等价无穷小}{017 / 408}
当$x \to 0$时，$f(x) = x - \sin ax$与$g(x) = x^2\ln (1 - bx)$是等价无穷小，则\pickout{}
\begin{abcd}
\item $a = 1,b = - \frac{1}{6}$．
\item $a = 1,b = \frac{1}{6}$．
\item $a = - 1,b = - \frac{1}{6}$．
\item $a = - 1,b = \frac{1}{6}$．
\end{abcd}
\QuestionEnd

% Q 2011 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2011 年第 1 题}{1}{三角函数的等价无穷小}{018 / 408}
已知当$x \to 0$时，$f(x) = 3\sin x - \sin 3x$与$cx^k$是等价无穷小，则\pickout{}
\begin{abcd}
\item $k = 1,c = 4$．
\item $k = 1,c = - 4$．
\item $k = 3,c = 4$．
\item $k = 3,c = - 4$．
\end{abcd}
\QuestionEnd

% Q 2012 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2012 年第 1 题}{1}{渐近线条数}{019 / 408}
曲线$y = \frac{x^2 + x}{x^2 - 1}$渐近线的条数为\pickout{}
\begin{abcd}
\item $0$．
\item $1$．
\item $2$．
\item $3$．
\end{abcd}
\QuestionEnd

% Q 2013 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2013 年第 1 题}{1}{三角无穷小的比较}{020 / 408}
设$\cos x - 1 = x\sin \alpha(x)$，其中$\left| \alpha(x) \right| < \frac{\pi}{2}$，
则当$x \to 0$时，$\alpha (x)$是\pickout{}
\begin{abcd}
\item 比$x$高阶的无穷小．
\item 比$x$低阶的无穷小．
\item 与$x$同阶但不等价的无穷小．
\item 与$x$等价的无穷小．
\end{abcd}
\QuestionEnd

% Q 2014 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2014 年第 1 题}{1}{幂次与无穷小阶}{021 / 408}
当$x \to 0^+$时，若$\ln^{\alpha}(1 + 2x)$，$(1 - \cos x)^{\frac{1}{\alpha}}$
均是比$x$高阶的无穷小，则$\alpha$的可能取值范围是\pickout{}
\begin{abcd}
\item $(2, +\infty)$．
\item $(1,2)$．
\item $\left(\frac{1}{2},1 \right)$．
\item $\left(0,\frac{1}{2} \right)$．
\end{abcd}
\QuestionEnd

% Q 2014 2
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2014 年第 2 题}{1}{渐近线的判定}{022 / 408}
下列曲线有渐近线的是\pickout{}
\begin{abcd}
\item $y = x + \sin x$．
\item $y = x^2 + \sin x$．
memory/plan.md:5:## 09–26 年真题与解析
memory/plan.md:7:递归将 `考研数学一二三09-26年真题&解析` 下的 PDF 转到 `302真题`，维持一份 PDF 对应一份 Markdown。直接提取正常文字层，对扫描页和文字层明显损坏的页面，用 PyMuPDF 渲染后交给本机 Vision 识别。
memory/plan.md:11:以教材目录和正文限定范围，从第一章至第二章第四节末，含极值必要条件、微分中值定理和洛必达法则。筛选 `27302模拟` 中的六套卷、880 题和基础 500 题，优先核对可辨认的原题和配套解析。采用本地 2026 年考研数学一试卷的 10 道单选、6 道填空、6 道解答及对应分值，在 `output` 交付可编辑的 LaTeX 和由其编译的 PDF。原题位置写入 LaTeX 注释。
memory/plan.md:15:按已有的教材范围筛选更多题目。以原题版本为单位，合并同题的横版、A4 版及解析，排除第一卷已经使用的题目。能用范围内方法独立完成的题或小问编成多份 150 分试卷，余题列为补充练习；每题保留出处。
memory/plan.md:17:## 302 数学二分节真题集
memory/plan.md:19:以 `302真题` 所对应的 2009–2026 年数学二逐年原卷为准，按教材上册大纲的四章、19 节建立目录。逐题记录年份、题号、页码、主考点及归属，跨节题按主要方法收录一次。上册未覆盖的数学二题目按主题列入附录。LaTeX 引用逐题裁片，保留原卷题干、公式、选项和图形。交付写入 `output`，不安装或调用 TeX 编译器。
memory/plan.md:23:原卷截图排版的旧版 iPad 横屏 PDF 和 `.tex` 从本地交付目录及远端 `main` 移除。保留原生 LaTeX 版本，以及仍供分节源稿使用的裁片资源。旧版可从 Git 历史恢复。
memory/plan.md:27:按原卷题号读取逐年原卷文字层、已有 OCR 和配套解析。将题干、选择项、公式、矩阵和小问逐题写成 LaTeX，图题写成 TikZ 矢量路径。以同一份题库源稿生成 4:3 横屏题集和 A4 常规分节版，保留上册 19 节的定理页和原卷题号。原卷页码仅留在 LaTeX 源稿。行内和独立公式中的极限条件均排在 `lim` 正下方。按原书节序输出，核对上册与附录题目。不安装 TeX 编译器。
memory/verify.md:7:检查 22 道题的原题位置、公式、唯一答案和范围内解法。核对卷面分值 $50+30+70=150$，实际编译 LaTeX，检查 PDF 文本中题号、分节和缺字。
memory/verify.md:13:- Tectonic 编译成功，日志无警告、缺字或溢出报告。PDF 为四页 A4，逐页检查了页码、分节、题号 1–22 和文字边界。未进行截图检查。
memory/verify.md:17:每卷检查 10 道单选、6 道填空、6 道解答和 150 分，核对题源定位、与旧卷及新增卷之间的重复、范围内解法和补充练习题量。编译后检查逐卷题序、分节、文字边界及缺字日志。
memory/verify.md:26:## 302 数学二分节真题集
memory/verify.md:48:旧版 iPad 横屏 PDF 和 LaTeX 源稿已从本地及远端 `main` 文件树移除。原生版与仍供分节源稿使用的裁片资源校验值一致，两份旧版文件可从删除提交的父提交恢复。
memory/gotchas.md:7:真题集的行内极限也将趋近条件排在 `lim` 正下方。题头显示原卷年份和题号，原卷页码只留作 LaTeX 源稿中的定位信息。
memory/progress.md:8:## 09–26 年真题与解析
memory/progress.md:10:- 已将 151 份 PDF 转成 Markdown 保存到 `302真题`。扫描页及文字层有乱码的页面使用本机 OCR。
memory/progress.md:12:- 文件名为《2026考研数学（一）答案解析》的原 PDF 首页写的是“2025 年考研数学一”，Markdown 保留原文件名和页内年份。
memory/progress.md:26:## 302 数学二分节真题集
memory/progress.md:29:- [x] 定位 408 道题的题号和裁片边界，按主要考点分节。
memory/progress.md:30:- [x] 生成 `output/302数学二分节真题集.tex` 和 `output/302-question-facsimiles.pdf`。正文 236 题，附录 172 题，共 410 个裁片。
memory/progress.md:34:- [x] 确认现有真题集的题序、节名与题面资源。


## tool · 2026-11-10T09:55:52Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2014 2
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2014 年第 2 题}{1}{渐近线的判定}{022 / 408}
下列曲线有渐近线的是\pickout{}
\begin{abcd}
\item $y = x + \sin x$．
\item $y = x^2 + \sin x$．
\item $y = x + \sin \frac{1}{x}$．
\item $y = x^2 + \sin \frac{1}{x}$．
\end{abcd}
\QuestionEnd

% Q 2016 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2016 年第 1 题}{1}{无穷小量的阶}{023 / 408}
设$a_1 = x(\cos \sqrt{x} - 1)$，$a_2 = \sqrt{x} \ln(1 + \sqrt[3]{x})$，$a_3 = \sqrt[3]{x + 1} - 1$．
当$x \to 0^+$时，以上$3$个无穷小量按照从低阶到高阶的排序是\pickout{}
\begin{abcd}
\item $a_1,a_2,a_3$．
\item $a_2,a_3,a_1$．
\item $a_2,a_1,a_3$．
\item $a_3,a_2,a_1$．
\end{abcd}
\QuestionEnd

% Q 2019 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2019 年第 1 题}{1}{正切函数的同阶无穷小}{024 / 408}
当$x \to 0$时，若$x - \tan x$与$x^k$是同阶无穷小，则$k =$\pickout{}
\begin{abcd}
\item $1$．
\item $2$．
\item $3$．
\item $4$．
\end{abcd}
\QuestionEnd

% Q 2020 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2020 年第 1 题}{1}{积分形式的无穷小比阶}{025 / 408}
当 \(x \to 0^{+}\) 时，下列无穷小量中阶最高的是
\choices{\(\int_{0}^{x}{\left( e^{t^{2}} - 1 \right) \mathrm{~d} t}\)}{\(\int_{0}^{x}{\ln \left( 1 + \sqrt{t^{3}} \right) \mathrm{~d} t}\)}{\(\int_{0}^{\sin x}{\sin t^{2} \mathrm{~d} t}\)}{\(\int_{0}^{1-\cos x}{\sqrt{\sin^{3} t} \mathrm{~d} t}\)}
\QuestionEnd

% Q 2021 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2021 年第 1 题}{1}{变上限积分的无穷小阶}{026 / 408}
当 \(x \to 0\) 时，\(\int_{0}^{x^{2}} \left(e^{t}-1\right) \mathrm{d} t\) 是 \(x^{7}\) 的
\choices{低阶无穷小}{等价无穷小}{高阶无穷小}{同阶但非等价无穷小}
\QuestionEnd

% Q 2022 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2022 年第 1 题}{1}{等价无穷小的性质}{027 / 408}
若当 \(x \to 0\) 时，\(\alpha\left( x \right), \beta\left( x \right)\) 是非零无穷小量，则以下的命题中，
\par\circnum{1} 若 \(\alpha\left( x \right) \sim \beta\left( x \right)\)，则 \(\alpha^{2}\left( x \right) \sim \beta^{2}\left( x \right)\)；
\par\circnum{2} 若 \(\alpha^{2}\left( x \right) \sim \beta^{2}\left( x \right)\)，则 \(\alpha\left( x \right) \sim \beta\left( x \right)\)；
\par\circnum{3} 若 \(\alpha\left( x \right) \sim \beta\left( x \right)\)，则 \(\alpha\left( x \right) - \beta\left( x \right) = o\left( \alpha\left( x \right) \right)\)；
\par\circnum{4} 若 \(\alpha\left( x \right) - \beta\left( x \right) = o\left( \alpha\left( x \right) \right)\)，则 \(\alpha\left( x \right) \sim \beta\left( x \right)\)，
真命题的序号为 \(\left( \ \right)\)
\choices{\circnum{1}\circnum{3}}{\circnum{1}\circnum{4}}{\circnum{1}\circnum{3}\circnum{4}}{\circnum{2}\circnum{3}\circnum{4}}
\QuestionEnd

% Q 2023 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2023 年第 1 题}{1}{斜渐近线}{028 / 408}
曲线
\[y=x\ln\left(e+\frac{1}{x-1}\right)
\]
的斜渐近线方程为（ ）。
\choices{\(y=x+e\)}{\(y=x+\dfrac{1}{e}\)}{\(y=x\)}{\(y=x-\dfrac{1}{e}\)}
\QuestionEnd

% Q 2025 4
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2025 年第 4 题}{1}{无穷小比阶}{029 / 408}
设函数 \(f\left( x \right)\)，\(g\left( x \right)\) 在 \(x = 0\) 的某去心邻域内有定义且恒不为零.若当 \(x \to 0\) 时，\(f\left( x \right)\) 是 \(g\left( x \right)\) 的高阶无穷小，则当 \(x \to 0\) 时，
\choices{\(f\left( x \right) + g\left( x \right) = O\left( g\left( x \right) \right)\).}{\(f\left( x \right) g\left( x \right) = o\left( f^{2}\left( x \right) \right)\).}{\(f\left( x \right) = o\left( e^{g\left( x \right)} - 1 \right)\).}{\(f\left( x \right) = o\left( g^{2}\left( x \right) \right)\).}
\QuestionEnd

% Q 2026 1
\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2026 年第 1 题}{1}{等价无穷小求系数}{030 / 408}
已知当 \(x \to 0\) 时，\(a x^{2} + b x + \arcsin x\) 与 \(\sqrt[3]{1 + x^{2}} - 1\) 是等价无穷小，则
\choices{\(a = \frac{1}{3},\ b = -1\)}{\(a = \frac{1}{3},\ b = 1\)}{\(a = \frac{2}{3},\ b = -1\)}{\(a = \frac{2}{3},\ b = 1\)}
\QuestionEnd

% Q 2010 10
\QuestionPage{1.4 无穷小量与无穷大量}{填空题}{2010 年第 10 题}{2}{曲线的渐近线}{031 / 408}
曲线$y = \frac{2x^3}{x^2 + 1}$的渐近线方程为 \blank{}．
\QuestionEnd

% Q 2016 9
\QuestionPage{1.4 无穷小量与无穷大量}{填空题}{2016 年第 9 题}{2}{斜渐近线}{032 / 408}
曲线$y = \frac{x^3}{1 + x^2} + \arctan(1 + x^2)$的斜渐近线方程为 \blank{}．
\QuestionEnd

% Q 2017 9
\QuestionPage{1.4 无穷小量与无穷大量}{填空题}{2017 年第 9 题}{2}{斜渐近线}{033 / 408}
曲线$y = x\left(1 + \arcsin \frac{2}{x} \right)$的斜渐近线方程为 \blank{}．
\QuestionEnd

% Q 2023 11
\QuestionPage{1.4 无穷小量与无穷大量}{填空题}{2023 年第 11 题}{2}{等价无穷小求系数}{034 / 408}
当 \(x\to 0\) 时，函数
\[f(x)=ax+bx^2+\ln(1+x)
\]
与
\[g(x)=e^{x^2}-\cos x
\]
是等价无穷小，则
\[ab=\blank{}.
\]
\QuestionEnd

% Q 2025 12
\QuestionPage{1.4 无穷小量与无穷大量}{填空题}{2025 年第 12 题}{2}{斜渐近线}{035 / 408}
曲线 \(y = \sqrt[3]{x^{3} - 3x^{2} + 1}\) 的渐近线方程为 \blank{}.
\QuestionEnd

% Q 2012 15
\QuestionPage{1.4 无穷小量与无穷大量}{解答题}{2012 年第 15 题}{2}{同阶无穷小与参数}{036 / 408}
已知函数$f(x) = \frac{1 + x}{\sin x} - \frac{1}{x}$，记$a = \lim_{x \to 0} f(x)$．\par
\begin{enumerate}
\item 求$a$的值；
\item 若当$x \to 0$时，$f(x) - a$是$x^k$的同阶无穷小，求$k$．
\end{enumerate}
\QuestionEnd

% Q 2013 15
\QuestionPage{1.4 无穷小量与无穷大量}{解答题}{2013 年第 15 题}{2}{三角乘积的等价无穷小}{037 / 408}
当$x \to 0$时，$1 - \cos x \cdot \cos 2x \cdot \cos 3x$与$ax^n$为等价无穷小，求$n$与$a$的值．
\QuestionEnd

% Q 2015 15
\QuestionPage{1.4 无穷小量与无穷大量}{解答题}{2015 年第 15 题}{2}{等价无穷小求参数}{038 / 408}
设函数$f(x) = x + a\ln(1 + x) + bx\sin x$，$g(x) = kx^3$，
若$f(x)$与$g(x)$在$x \to 0$是等价无穷小，求$a,b,k$的值．
\QuestionEnd

% Q 2020 15
\QuestionPage{1.4 无穷小量与无穷大量}{解答题}{2020 年第 15 题}{2}{斜渐近线}{039 / 408}
求曲线 \(y = \dfrac{x^{1+x}}{\left( 1+x \right)^{x}} \left( x>0 \right)\) 的斜渐近线方程。
\QuestionEnd

\SectionHeading{1.5}{函数、极限、连续}{连续函数}{定理与要点\quad 教材 PDF 第 86 页起\hfill 本节 8 题}
\pdfbookmark[2]{1.5 连续函数}{section-1.5}


## tool · 2026-11-10T09:55:59Z


Script completed
Wall time 0.1 seconds
Output:

302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:238:gg（x）的高阶无穷小，则当x—0时，（
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:246:当 一0时，f（x）是g（x）的高阶无穷小意味着lim x）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:255:解）由于当x-0时，f（x）是g（x）的高阶无穷小，故lim a）
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【真题】09-26/2012考研数学二真题.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【解析】09-26/2012数二真题【解析】.pdf


## tool · 2026-11-10T09:56:02Z


Script completed
Wall time 0.1 seconds
Output:

【例】若微分方程 +ay'+by=0的解在（-∞，+∞）上有界，则（
（B）a >0,6>0.
（C）a =0,6>0.
）（2023年数学
（D）a =0,0<0.
设函数f（x），8（x）在× =0的某去心邻域内有定义且恒不为零.若当x—0时，f（x）是
gg（x）的高阶无穷小，则当x—0时，（
）
（A）f（x）+g（x）=0（g（x））.
（C）f（x） = o（es（a） - 1）.
（B）f（x）g（x）= o（f"（x））.
（D）f（x） = o（g'（x））.
答案）C.
分析 本题主要考查无穷小量比阶.
当 一0时，f（x）是g（x）的高阶无穷小意味着lim x）
a gg（x）
=0.由此出发，可以计算得到选项A、
B、C 中的相应极限.对选项D，由lim
fx2 =0无法保证lim
f（x）
x40g（3）
110g？（x）
-=0，可以考虑举反例.
解）由于当x-0时，f（x）是g（x）的高阶无穷小，故lim a）
x40 g（×）
=0.于是，
lim fx）+8（x）=1+lim
f（x）
g（x）
x-0 g（x）
= 1，
lim128（x= lim Elal =∞，
f（x）
*-0f（x）
—8—
```

## PDF 第 6 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2025%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=6) · 本机 OCR

```text
cle）-1~8（ ）
4-0 ef（x）.
f（x）
= 0.
2-0 gg（×）


## tool · 2026-11-10T09:56:06Z


Script completed
Wall time 0.2 seconds
Output:

考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.pdf
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2012考研数学二真题.md
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md
1.26.5


## tool · 2026-11-10T09:56:12Z


Script completed
Wall time 0.2 seconds
Output:




## tool · 2026-11-10T09:56:16Z




## tool · 2026-11-10T09:58:51Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T09:58:53Z




## tool · 2026-11-10T09:58:57Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2009 1
\QuestionPage{1.5 连续函数}{选择题}{2009 年第 1 题}{1}{可去间断点}{040 / 408}
函数$f(x) = \frac{x - x^3}{\sin\pi x}$的可去间断点的个数为\pickout{}
\begin{abcd}
\item $1$．
\item $2$．
\item $3$．
\item 无穷多个．
\end{abcd}
\QuestionEnd

% Q 2010 1
\QuestionPage{1.5 连续函数}{选择题}{2010 年第 1 题}{1}{无穷间断点}{041 / 408}
函数$f(x) = \frac{x^2 - x}{x^2 - 1}\sqrt{1 + \frac{1}{x^2}}$的无穷间断点的个数为\pickout{}
\begin{abcd}
\item $0$．
\item $1$．
\item $2$．
\item $3$．
\end{abcd}
\QuestionEnd

% Q 2015 2
\QuestionPage{1.5 连续函数}{选择题}{2015 年第 2 题}{1}{由极限定义的函数及间断点}{042 / 408}
函数$f(x) = \lim_{t \to 0} \left(1 + \frac{\sin t}{x} \right)^{\frac{x^2}{t}}$
在$(-\infty , +\infty)$内\pickout{}
\begin{abcd}
\item 连续．
\item 有可去间断点．
\item 有跳跃间断点．
\item 有无穷间断点．
\end{abcd}
\QuestionEnd

% Q 2015 3
\QuestionPage{1.5 连续函数}{选择题}{2015 年第 3 题}{1}{分段函数连续性与参数}{043 / 408}
设函数$f(x) = \begin{cases}
  x^{\alpha}\cos \frac{1}{x^{\beta}}, & x > 0 \\
                                   0, & x \le 0
\end{cases}$（$\alpha > 0,\beta > 0$），若$f'(x)$在$x = 0$处连续，则\pickout{}
\begin{abcd}
\item $\alpha - \beta > 1$．
\item $0 < \alpha - \beta \le 1$．
\item $\alpha - \beta > 2$．
\item $0 < \alpha - \beta \le 2$．
\end{abcd}
\QuestionEnd

% Q 2017 1
\QuestionPage{1.5 连续函数}{选择题}{2017 年第 1 题}{1}{分段函数的连续条件}{044 / 408}
若函数$f(x) = \begin{cases}
  \frac{1 - \cos \sqrt{x}}{ax}, & x > 0 \\
                             b, & x \le 0
\end{cases}$在$x = 0$处连续，则\pickout{}
\begin{abcd}
\item $ab = \frac{1}{2}$．
\item $ab = - \frac{1}{2}$．
\item $ab = 0$．
\item $ab = 2$．
\end{abcd}
\QuestionEnd

% Q 2018 3
\QuestionPage{1.5 连续函数}{选择题}{2018 年第 3 题}{1}{分段函数和的连续性}{045 / 408}
设函数$f(x) = \begin{cases}
  -1, & x < 0, \\
   1, & x \ge 0;
\end{cases}$，$g(x) = \begin{cases}
  2 - ax, & x \le - 1, \\
       x, & -1 < x < 0, \\
   x - b, & x \ge 0.
\end{cases}$若$f(x) + g(x)$在$R$上连续，则\pickout{}
\begin{abcd}
\item $a = 3\;,\;b = 1$．
\item $a = 3\;,\;b = 2$．
\item $a = - 3\;,\;b = 1$．
\item $a = - 3\;,\;b = 2$．
\end{abcd}
\QuestionEnd

% Q 2020 2
\QuestionPage{1.5 连续函数}{选择题}{2020 年第 2 题}{1}{第二类间断点}{046 / 408}
函数 \(f\left( x \right) = \dfrac{e^{\frac{1}{x-1}} \ln \left| 1+x \right|}{\left( e^{x} - 1 \right)\left( x-2 \right)}\) 的第二类间断点的个数为
\choices{\(1\) 个}{\(2\) 个}{\(3\) 个}{\(4\) 个}
\QuestionEnd

% Q 2024 1
\QuestionPage{1.5 连续函数}{选择题}{2024 年第 1 题}{1}{间断点个数}{047 / 408}
函数
\[f(x)=|x|^{\frac{1}{(1-x)(x-2)}}
\]
的第一类间断点的个数为（ ）
\choices{\(3\)}{\(2\)}{\(1\)}{\(0\)}
\QuestionEnd

\SectionHeading{2.1}{一元函数微分学及其应用}{导数的概念}{定理与要点\quad 教材 PDF 第 108 页起\hfill 本节 8 题}
\pdfbookmark[1]{一元函数微分学及其应用}{chapter-2.1}
\pdfbookmark[2]{2.1 导数的概念}{section-2.1}
\Theory{定理 1.1}{115}{可导推出连续}{函数在某点可导，则在该点连续。}
\Theory{要点}{108--115}{导数定义与几何意义}{差商的左右极限须存在且相等。有限导数给出切线斜率，非零时法线斜率为其负倒数。}
% Q 2010 3
\QuestionPage{2.1 导数的概念}{选择题}{2010 年第 3 题}{1}{曲线相切}{048 / 408}
曲线$y = x^2$与曲线$y = a\ln x$（$a \ne 0$）相切，则$a =$\pickout{}
\begin{abcd}
\item $4\mathrm{e}$．
\item $3\mathrm{e}$．
\item $2\mathrm{e}$．
\item $\mathrm{e}$．
\end{abcd}
\QuestionEnd

% Q 2011 2
\QuestionPage{2.1 导数的概念}{选择题}{2011 年第 2 题}{1}{导数定义与极限}{049 / 408}
已知$f(x)$在$x = 0$处可导，且$f(0) = 0$，
则$\lim_{x \to 0} \frac{x^2 f(x) - 2f\left(x^3 \right)}{x^3} =$\pickout{}
\begin{abcd}
\item $- 2f'(0)$．
\item $- f'(0)$．
\item $f'(0)$．
\item $0$．
\end{abcd}
\QuestionEnd

% Q 2018 2
\QuestionPage{2.1 导数的概念}{选择题}{2018 年第 2 题}{1}{原点处的可导性}{050 / 408}
下列函数中，在$x = 0$处不可导的是\pickout{}
\begin{abcd}
\item $f(x) = |x|\sin |x|$．
\item $f(x) = |x|\sin \sqrt{|x|}$．
\item $f(x) = \cos |x|$．
\item $f(x) = \cos \sqrt{|x|}$．
\end{abcd}
\QuestionEnd

% Q 2021 2
\QuestionPage{2.1 导数的概念}{选择题}{2021 年第 2 题}{1}{分段函数的可导性与极值}{051 / 408}
函数
\[f(x)=
\begin{cases}
\dfrac{e^x-1}{x}, & x\ne 0,\\
1, & x=0
\end{cases}
\]
在 \(x=0\) 处
\choices{连续且取极大值}{连续且取极小值}{可导且导数为 \(0\)}{可导且导数不为 \(0\)}
\QuestionEnd

% Q 2025 7
\QuestionPage{2.1 导数的概念}{选择题}{2025 年第 7 题}{2}{可导的等价条件}{052 / 408}
设函数 \(f\left( x \right)\) 连续，给出下列四个条件：
\par\circnum{1} \(\lim_{x \to 0} \frac{\left| f\left( x \right) \right| - f\left( 0 \right)}{x}\) 存在；
\par\circnum{2} \(\lim_{x \to 0} \frac{f\left( x \right) - \left| f\left( 0 \right) \right|}{x}\) 存在；
\par\circnum{3} \(\lim_{x \to 0} \frac{\left| f\left( x \right) \right|}{x}\) 存在；
\par\circnum{4} \(\lim_{x \to 0} \frac{\left| f\left( x \right) \right| - \left| f\left( 0 \right) \right|}{x}\) 存在.
其中能得到 “\(f\left( x \right)\) 在 \(x = 0\) 处可导” 的条件的个数是
\choices{1}{2}{3}{4}
\QuestionEnd

% Q 2009 9
\QuestionPage{2.1 导数的概念}{填空题}{2009 年第 9 题}{2}{切线方程}{053 / 408}
曲线$\begin{cases}
  x = \int_0^{1\text{-} t} \mathrm{e}^{- u^2} \,\mathrm{d} u \\
  y = t^2\ln(2 - t^2)
\end{cases}$在$(0,0)$处的切线方程为 \blank{}．
\QuestionEnd

% Q 2022 17
\QuestionPage{2.1 导数的概念}{解答题}{2022 年第 17 题}{2}{由极限求导数}{054 / 408}
已知函数 \(f\left( x \right)\) 在 \(x = 1\) 处可导，且
\(\lim_{x \to 0} \frac{f\left( e^{x^{2}} \right) - 3f\left( 1 + \sin^{2}x \right)}{x^{2}} = 2\)
求 \(f^{\prime}\left( 1 \right)\).
\QuestionEnd

% Q 2025 18
\QuestionPage{2.1 导数的概念}{解答题}{2025 年第 18 题}{3}{由极限判断可导性}{055 / 408}
（本题满分 12 分）
设函数 \(f\left( x \right)\) 在 \(x = 0\) 处连续，且 \(\lim_{x \to 0} \frac{x f\left( x \right) - e^{2 \sin x} + 1}{\ln \left( 1 + x \right) + \ln \left( 1 - x \right)} = -3\)，证明 \(f\left( x \right)\) 在 \(x = 0\) 处可导，并求 \(f^{\prime}\left( 0 \right)\).
\QuestionEnd

\SectionHeading{2.2}{一元函数微分学及其应用}{求导的基本法则}{定理与要点\quad 教材 PDF 第 121 页起\hfill 本节 28 题}
\pdfbookmark[2]{2.2 求导的基本法则}{section-2.2}
\Theory{定理 2.1}{121}{导数的有理运算法则}{可导函数的和、差、积、商可导。乘积用乘积法则，商须分母非零。}
\Theory{定理 2.2}{123}{链式法则}{内外两层在相应点可导时，复合函数的导数等于外层导数乘内层导数。}
\Theory{定理 2.3}{125}{反函数求导法则}{严格单调连续函数在对应点可导且导数非零时，反函数导数等于原导数的倒数。}
\Theory{定理 2.4}{130}{高阶导数的运算}{n 阶导数满足线性法则。乘积的 n 阶导数按 Leibniz 公式作二项式系数加权求和。}
\Theory{定理 2.5}{132}{参数方程求导法则}{当 x\ensuremath{{}^{\prime}}(t) 非零时，dy/dx = y\ensuremath{{}^{\prime}}(t)/x\ensuremath{{}^{\prime}}(t)。再对 t 求导并除以 x\ensuremath{{}^{\prime}}(t) 得二阶导数。}
\Theory{方法}{130--135}{隐函数与相关变化率}{先按变量依赖关系求导，再代入给定点或时刻。隐函数项需乘上相应的导数。}
% Q 2012 2
\QuestionPage{2.2 求导的基本法则}{选择题}{2012 年第 2 题}{1}{乘积求导}{056 / 408}
设函数$f(x) = (\mathrm{e}^x - 1)(\mathrm{e}^{2x} - 2) \cdots(\mathrm{e}^{nx} - n)$，其中$n$为正整数，则$f'(0) =$\pickout{}
\begin{abcd}
\item $(- 1)^{n - 1}(n - 1)!$．
\item $(- 1)^n(n - 1)!$．
\item $(- 1)^{n - 1} n!$．
\item $(- 1)^n n!$．
\end{abcd}
\QuestionEnd

% Q 2013 2
\QuestionPage{2.2 求导的基本法则}{选择题}{2013 年第 2 题}{1}{隐函数求导与极限}{057 / 408}
设函数$y = f(x)$由方程$\cos (xy) + \ln y - x = 1$确定，
则$\lim_{n \to \infty} n\left[f\left(\frac{2}{n} \right) - 1 \right] =$\pickout{}
\begin{abcd}
\item $2$．
\item $1$．
\item $- 1$．
\item $- 2$．
\end{abcd}
\QuestionEnd

% Q 2021 3
\QuestionPage{2.2 求导的基本法则}{选择题}{2021 年第 3 题}{1}{圆柱体的相关变化率}{058 / 408}
有一圆柱体底面半径与高随时间变化的速率分别为 \(2 \text{ cm/s}\)、\(-3 \text{ cm/s}\)。当底面半径为 \(10 \text{ cm}\)，高为 \(5 \text{ cm}\) 时，圆柱体的体积与表面积随时间变化的速率分别为
\choices{\(125\pi \text{ cm}^{3}\text{/s}\)，\(40\pi \text{ cm}^{2}\text{/s}\)}{\(125\pi \text{ cm}^{3}\text{/s}\)，\(-40\pi \text{ cm}^{2}\text{/s}\)}{\(-100\pi \text{ cm}^{3}\text{/s}\)，\(40\pi \text{ cm}^{2}\text{/s}\)}{\(-100\pi \text{ cm}^{3}\text{/s}\)，\(-40\pi \text{ cm}^{2}\text{/s}\)}
\QuestionEnd

% Q 2023 5
\QuestionPage{2.2 求导的基本法则}{选择题}{2023 年第 5 题}{1}{参数方程与可导性}{059 / 408}
设函数 \(y=f(x)\) 由
\[\begin{cases}
x=2t+|t|,\\
y=|t|\sin t
\end{cases}
\]
确定，则（ ）。
\choices{\(f(x)\) 连续，\(f'(0)\) 不存在}{\(f'(0)\) 存在，\(f'(x)\) 在 \(x=0\) 处不连续}{\(f'(x)\) 连续，\(f''(0)\) 不存在}{\(f''(0)\) 存在，\(f''(x)\) 在 \(x=0\) 处不连续}
\QuestionEnd

% Q 2024 2
\QuestionPage{2.2 求导的基本法则}{选择题}{2024 年第 2 题}{1}{参数方程求导与导数定义}{060 / 408}
已知
\[\left\{
\begin{aligned}
x &= 1+t^3,\\
y &= e^{t^2},
\end{aligned}
\right.
\]
则
\[\lim_{x\to+\infty}x\!\left[f\!\left(2+\frac{2}{x}\right)-f(2)\right]
\]
等于（ ）
\choices{\(2e\)}{\(\frac{4}{3}e\)}{\(\frac{2}{3}e\)}{\(\frac{e}{3}\)}
\QuestionEnd

% Q 2026 6
\QuestionPage{2.2 求导的基本法则}{选择题}{2026 年第 6 题}{1}{反函数与变上限积分求导}{061 / 408}
已知函数
\[f(x)=\int_1^{x^3}\frac{e^t}{1+t^2}\,dt,
\]
\(f\) 的反函数为 \(g\)，则
\choices{\(g(0)=1,\ g'(0)=\dfrac{3}{2e}\)}{\(g(0)=1,\ g'(0)=\dfrac{2}{3e}\)}{\(g(1)=0,\ g'(1)=\dfrac{3}{2e}\)}{\(g(1)=0,\ g'(1)=\dfrac{2}{3e}\)}
\QuestionEnd

% Q 2009 12
\QuestionPage{2.2 求导的基本法则}{填空题}{2009 年第 12 题}{2}{隐函数求导}{062 / 408}
设$y = y(x)$是由方程$xy + \mathrm{e}^y = x + 1$确定的隐函数，
则$\frac{\partial{}^2 y}{\partial{} x^2}\Big|_{x = 0} =$ \blank{}．
     332 .question-bank-work/solutions/001-113.tex


## tool · 2026-11-10T09:59:02Z


Script completed
Wall time 0.1 seconds
Output:

% Q 2009 12
\QuestionPage{2.2 求导的基本法则}{填空题}{2009 年第 12 题}{2}{隐函数求导}{062 / 408}
设$y = y(x)$是由方程$xy + \mathrm{e}^y = x + 1$确定的隐函数，
则$\frac{\partial{}^2 y}{\partial{} x^2}\Big|_{x = 0} =$ \blank{}．
\QuestionEnd

% Q 2010 11
\QuestionPage{2.2 求导的基本法则}{填空题}{2010 年第 11 题}{2}{对数函数的高阶导数}{063 / 408}
函数$y = \ln(1 - 2x)$在$x = 0$处的$n$阶导数$y^{(n)}(0) =$ \blank{}．
\QuestionEnd

% Q 2010 13
\QuestionPage{2.2 求导的基本法则}{填空题}{2010 年第 13 题}{2}{相关变化率}{064 / 408}
已知一个长方形的长$l$以$2\text{cm/s}$的速率增加，宽$w$以$3\text{cm/s}$的速率增加．
则当$l = 12\text{cm}$，$w = 5\text{cm}$时，它的对角线增加的速率为 \blank{}．
\QuestionEnd

% Q 2012 9
\QuestionPage{2.2 求导的基本法则}{填空题}{2012 年第 9 题}{2}{隐函数求导}{065 / 408}
设$y = y(x)$是由方程$x^2 - y + 1 = \mathrm{e}^y$所确定的隐函数，
则$\left. \frac{\,\mathrm{d}{}^2y}{\,\mathrm{d} x^2} \right|_{x = 0} =$ \blank{}．
\QuestionEnd

% Q 2013 10
\QuestionPage{2.2 求导的基本法则}{填空题}{2013 年第 10 题}{2}{反函数求导}{066 / 408}
设函数$f(x) = \int_{-1}^x \sqrt{1 - \mathrm{e}^t} \,\mathrm{d} t$，则$y = f(x)$的反函数$x = f^{-1}(y)$
在$y = 0$处的导数$\left. \frac{\,\mathrm{d} x}{\,\mathrm{d} y} \right|_{y = 0} =$ \blank{}．
\QuestionEnd

% Q 2013 12
\QuestionPage{2.2 求导的基本法则}{填空题}{2013 年第 12 题}{2}{参数曲线的法线}{067 / 408}
曲线$\begin{cases}
  x = \arctan t, \\
  y = \ln \sqrt{1 + t^2}
\end{cases}$上对应于$t = 1$的点处的法线方程为 \blank{}．
\QuestionEnd

% Q 2014 10
\QuestionPage{2.2 求导的基本法则}{填空题}{2014 年第 10 题}{2}{奇偶性、周期性与求导}{068 / 408}
设$f(x)$是周期为$4$的可导奇函数，且$f'(x)= 2(x - 1)$, $x \in[0,2]$，则$f(7) =$ \blank{}．
\QuestionEnd

% Q 2014 12
\QuestionPage{2.2 求导的基本法则}{填空题}{2014 年第 12 题}{2}{极坐标曲线的切线}{069 / 408}
曲线$L$的极坐标方程为$r = \theta$，
则$L$在点$(r,\theta) = \left(\frac{\pi}{2},\frac{\pi}{2}\right)$处的切线方程为 \blank{}．
\QuestionEnd

% Q 2015 9
\QuestionPage{2.2 求导的基本法则}{填空题}{2015 年第 9 题}{2}{隐函数求导}{070 / 408}
设$\begin{cases}
  x = \arctan t, \\
  y = 3t + t^3,
\end{cases}$则$\frac{\,\mathrm{d}{}^2y}{\,\mathrm{d} x^2}\big|_{t = 1} =$ \blank{}．
\QuestionEnd

% Q 2015 10
\QuestionPage{2.2 求导的基本法则}{填空题}{2015 年第 10 题}{2}{高阶导数}{071 / 408}
函数$f(x) = x^2 \cdot 2^x$在$x = 0$处的$n$阶导数$f^{(n)}(0) =$ \blank{}．
\QuestionEnd

% Q 2016 13
\QuestionPage{2.2 求导的基本法则}{填空题}{2016 年第 13 题}{2}{动点距离的相关变化率}{072 / 408}
已知动点$P$在曲线$y = x^3$上运动，记坐标原点与点$P$间的距离为$l$．
若点$P$的横坐标对时间的变化率为常数$v_0$，则当点$P$运动到点$(1,1)$时，$l$对时间的变化率是 \blank{}．
\QuestionEnd

% Q 2017 10
\QuestionPage{2.2 求导的基本法则}{填空题}{2017 年第 10 题}{2}{参数方程求导}{073 / 408}
设函数$y = y(x)$由参数方程$\begin{cases}
  x = t + \mathrm{e}^t \\
  y = \sin t
\end{cases}$确定，则$\left.\frac{\,\mathrm{d}{}^2y}{\,\mathrm{d} x^2}\right|_{t=0} =$ \blank{}．
\QuestionEnd

% Q 2019 10
\QuestionPage{2.2 求导的基本法则}{填空题}{2019 年第 10 题}{1}{参数曲线切线的截距}{074 / 408}
曲线$\begin{cases}
  x = t - \sin t \\
  y = 1 - \cos t
\end{cases}$在$t = \frac{3\pi}{2}$对应点处的切线在$y$轴的截距为 \blank{}．
\QuestionEnd

% Q 2019 13
\QuestionPage{2.2 求导的基本法则}{填空题}{2019 年第 13 题}{2}{高阶导数}{075 / 408}
已知函数$f(x) = x\int_1^x \frac{\sin t^2}{t} \,\mathrm{d} t$，则$\int_0^1 f(x)\,\mathrm{d} x =$ \blank{}．
\QuestionEnd

% Q 2020 9
\QuestionPage{2.2 求导的基本法则}{填空题}{2020 年第 9 题}{2}{参数方程的导数}{076 / 408}
设
\[\begin{cases}
x=\sqrt{t^2+1},\\
y=\ln\!\left(t+\sqrt{t^2+1}\right),
\end{cases}
\]
则 \(\left.\dfrac{\mathrm{d}^2y}{\mathrm{d}x^2}\right|_{t=1}=\)
\blank{}
\QuestionEnd

% Q 2021 12
\QuestionPage{2.2 求导的基本法则}{填空题}{2021 年第 12 题}{2}{参数方程求导}{077 / 408}
设函数 \(y=y(x)\) 由参数方程
\[\begin{cases}
x=2e^t+t+1,\\
y=4(t-1)e^t+t^2
\end{cases}
\]
确定，则
\[\left.\frac{\mathrm{d}^2 y}{\mathrm{d} x^2}\right|_{t=0}= \blank{}
\]
\QuestionEnd

% Q 2022 12
\QuestionPage{2.2 求导的基本法则}{填空题}{2022 年第 12 题}{2}{隐函数的二阶导数}{078 / 408}
已知函数 \(y = y\left( x \right)\) 由方程
\(x^{2} + xy + y^{3} = 3\)
确定，则 \(y^{\prime\prime}\left( 1 \right) = \blank{}\)
\QuestionEnd

% Q 2023 14
\QuestionPage{2.2 求导的基本法则}{填空题}{2023 年第 14 题}{2}{隐函数曲线的法线}{079 / 408}
曲线
\[3x^3=y^5+2y^3
\]
在 \(x=1\) 对应点处的法线斜率为
\[\blank{}.
\]
\QuestionEnd

% Q 2024 14
\QuestionPage{2.2 求导的基本法则}{填空题}{2024 年第 14 题}{2}{高阶导数}{080 / 408}
已知函数
\[f(x)=x^2(e^x-1),
\]
则
\[f^{(5)}(1)=\ \blank{}
\]
\QuestionEnd

% Q 2025 14
\QuestionPage{2.2 求导的基本法则}{填空题}{2025 年第 14 题}{2}{隐函数与参数方程求导}{081 / 408}
已知函数 \(y = y\left( x \right)\) 由 \(\left\{ \begin{aligned} x &= \ln \left( 1 + 2t \right), \\ 2t - \int_{1}^{y + t^{2}} e^{-u^{2}} \mathrm{~d} u &= 0 \end{aligned} \right.\)

确定，则 \(\left. \frac{\mathrm{d} y}{\mathrm{d} x} \right|_{x = 0} =\) \blank{}.
\QuestionEnd

% Q 2010 17
\QuestionPage{2.2 求导的基本法则}{解答题}{2010 年第 17 题}{3}{参数方程的二阶导数}{082 / 408}
设函数$y = f(x)$由参数方程$\begin{cases}
  x = 2t + t^2 \\
  y = \psi(t)
\end{cases}(t > - 1)$所确定，其中$\psi (t)$具有$2$阶导数，且$\psi (1) = \frac{5}{2}$，$\psi'(1) = 6$．
已知$\frac{\,\mathrm{d}{}^2y}{\,\mathrm{d} x^2} = \frac{3}{4(1 + t)}$，求函数$\psi (t)$．
\QuestionEnd

% Q 2018 20
\QuestionPage{2.2 求导的基本法则}{解答题}{2018 年第 20 题}{3}{面积的相关变化率}{083 / 408}
已知曲线$L:y = \frac{4}{9}x^2\left(x \ge 0 \right)$，点$O\left(0,0 \right)$，点$A\left(0,1 \right)$．
设$P$是$L$上的动点，$S$是直线$OA$与直线$AP$及曲线$L$所围图形的面积．
若$P$运动到$\left(3,4 \right)$时沿$x$轴正向的速度是$4$，求此时$S$关于时间$t$的变化率．
\QuestionEnd

\SectionHeading{2.3}{一元函数微分学及其应用}{微分}{定理与要点\quad 教材 PDF 第 140 页起\hfill 本节 0 题}
\pdfbookmark[2]{2.3 微分}{section-2.3}
\Theory{定理 3.1}{141}{可微与可导的等价性}{一元函数在一点可微当且仅当在该点可导，此时 df = f\ensuremath{{}^{\prime}}(x) dx。}


## assistant · 2026-11-10T09:59:12Z

前 39 题的推导已经写完。核对时发现两处会影响作答的题面转录问题，已标记给主代理处理。

## tool · 2026-11-10T10:02:01Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:02:06Z


Script completed
Wall time 0.1 seconds
Output:

本节在所收原卷中没有以该节为主考点的题目。
\SectionHeading{2.4}{一元函数微分学及其应用}{微分中值定理及其应用}{定理与要点\quad 教材 PDF 第 147 页起\hfill 本节 12 题}
\pdfbookmark[2]{2.4 微分中值定理及其应用}{section-2.4}
\Theory{定理 4.1}{147}{Fermat 定理}{内点取得局部极值且在该点可导，则导数为零。}
\Theory{定理 4.2}{148}{Rolle 定理}{闭区间上连续、开区间内可导且端点值相等，内部存在导数为零的点。}
\Theory{定理 4.3}{150}{Lagrange 中值定理}{闭区间上连续、开区间内可导，内部存在一点，其导数等于全区间的平均变化率。}
\Theory{定理 4.4}{154}{Cauchy 中值定理}{两函数闭区间上连续、开区间内可导，且 g\ensuremath{{}^{\prime}} 恒非零。内部某点的导数比等于端点增量比。}
\Theory{定理 4.5}{154--155}{洛必达法则，0/0 型}{两函数趋零，邻域内可导且分母导数非零。若导数之比有极限，则原商有同一极限。}
\Theory{定理 4.6}{156}{洛必达法则，\ensuremath{\infty}/\ensuremath{\infty} 型}{两函数在同一变化趋势下为无穷大量，其余条件沿用定理 4.5，可由导数比求原商极限。}
\Theory{推论 4.3}{152}{端点导数}{函数在端点连续、在相邻开区间可导且导数的单侧极限有限时，该极限就是端点的单侧导数。}
% Q 2014 5
\QuestionPage{2.4 微分中值定理及其应用}{选择题}{2014 年第 5 题}{1}{洛必达法则与函数极限}{084 / 408}
设函数$f(x) = \arctan x$，若$f(x) = xf'(\xi)$，则$\lim_{x \to 0} \frac{\xi^2}{x^2} =$\pickout{}
\begin{abcd}
\item $1$．
\item $\frac{2}{3}$．
\item $\frac{1}{2}$．
\item $\frac{1}{3}$．
\end{abcd}
\QuestionEnd

% Q 2017 2
\QuestionPage{2.4 微分中值定理及其应用}{选择题}{2017 年第 2 题}{1}{由可导条件推断中值点}{085 / 408}
设二阶可导函数$f(x)$满足$f(1) = f(- 1) = 1$，$f(0) = - 1$，且$f''(x) > 0$，则\pickout{}
\begin{abcd}
\item $\int_{-1}^1 f(x)\,\mathrm{d} x > 0$．
\item $\int_{-1}^1 f(x)\,\mathrm{d} x < 0$．
\item $\int_{-1}^0 f(x)\,\mathrm{d} x > \int_0^1 f(x)\,\mathrm{d} x$．
\item $\int_{-1}^0 f(x)\,\mathrm{d} x < \int_0^1 f(x)\,\mathrm{d} x$．
\end{abcd}
\QuestionEnd

% Q 2018 9
\QuestionPage{2.4 微分中值定理及其应用}{填空题}{2018 年第 9 题}{2}{反正切差的极限与中值定理}{086 / 408}
$\lim_{x \to +\infty} x^2[\arctan(x + 1) - \arctan x] =$ \blank{}．
\QuestionEnd

% Q 2009 21
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2009 年第 21 题}{4}{拉格朗日中值定理}{087 / 408}
\begin{enumerate}
\item 证明拉格朗日中值定理：若函数$f(x)$在$\left[a,b \right]$上连续，在$(a,b)$可导，
      则存在$\xi \in \left(a,b \right)$，使得$f(b) - f(a) = f'\left(\xi \right)(b - a)$．
\item 证明：若函数$f(x)$在$x = 0$处连续，在$\left(0,\delta \right)\left(\delta > 0 \right)$内可导，
      且$\lim_{x \to 0^+} f'(x) = A$，则$f'_+(0)$存在，且$f'_+(0) = A$．
\end{enumerate}
\QuestionEnd

% Q 2010 21
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2010 年第 21 题}{4}{两段区间上的中值定理}{088 / 408}
设函数$f(x)$在闭区间$[0,1]$上连续，在开区间$(0,1)$内可导，
且$f(0) = 0$, $f(1) = \frac{1}{3}$．证明：存在$\xi \in \left(0,\frac{1}{2}\right)$,
$\eta \in \left(\frac{1}{2},1\right)$，使得$f'(\xi) + f'(\eta) = \xi^2 + \eta^2$．
\QuestionEnd

% Q 2013 18
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2013 年第 18 题}{3}{奇函数与中值定理}{089 / 408}
设奇函数$f(x)$在$[- 1,1]$上具有$2$阶导数，且$f(1) = 1$．证明：
\begin{enumerate}
\item 存在$\xi \in(0,1)$，使得$f'(\xi) = 1$；
\item 存在$\eta \in (-1,1)$，使得$f''(\eta) + f'(\eta) = 1$．
\end{enumerate}
\QuestionEnd

% Q 2015 21
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2015 年第 21 题}{4}{切线与中值定理证明}{090 / 408}
已知函数$f(x)$在区间$[a,+\infty)$上具有$2$阶导数，
$f(a) = 0$，$f'(x) > 0$，$f''(x) > 0$．设$b > a$，
曲线$y = f(x)$在点$(b,f(b))$处的切线与$x$轴的交点是$(x_0,0)$，
证明$a < x_0 < b$．
\QuestionEnd

% Q 2017 15
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2017 年第 15 题}{2}{变上限积分的未定式极限}{091 / 408}
求极限$\lim_{x \to 0^+} \frac{\int_0^x \sqrt{x - t} \mathrm{e}^t \,\mathrm{d} t}{\sqrt{x^3}}$．
\QuestionEnd

% Q 2017 19
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2017 年第 19 题}{3}{罗尔定理与方程的根}{092 / 408}
设函数$f(x)$在区间$[0,1]$上具有二阶导数，且$f(1) > 0$，$\lim_{x \to 0^+} \frac{f(x)}{x} < 0$．证明：
\begin{enumerate}
\item 方程$f(x) = 0$在区间$(0,1)$内至少存在一个实根．
\item 方程$f(x)f''(x) + \left(f'(x) \right)^2 = 0$在区间$(0,1)$内至少存在两个不同实根．
\end{enumerate}
\QuestionEnd

% Q 2019 21
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2019 年第 21 题}{4}{中值定理与导数估计}{093 / 408}
已知函数$f(x)$在$[0,1]$上具有二阶导数，且
\[
f(0) = 0,\quad f(1) = 1,\quad \int_0^1 f(x)\,\mathrm{d} x = 1.
\]
证明：
\begin{enumerate}
\item 存在$\xi \in(0,1)$，使得$f'(\xi) = 0$；
\item 存在$\eta \in(0,1)$，使得$f''(\eta) < - 2$．
\end{enumerate}
\QuestionEnd

% Q 2023 21
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2023 年第 21 题}{4}{极值条件与二阶中值结论}{094 / 408}
设函数 \(f(x)\) 在 \([-a,a]\) 上具有二阶连续导数。证明：
\begin{enumerate}
\item 若 \(f(0)=0\)，则存在 \(\xi\in(-a,a)\)，使得
\[f''(\xi)=\frac{f(a)+f(-a)}{a^2};
\]
\item 若 \(f(x)\) 在 \((-a,a)\) 内取得极值，则存在 \(\eta\in(-a,a)\)，使得
\[|f''(\eta)|\ge \frac{|f(a)-f(-a)|}{2a^2}.
\]
\end{enumerate}
\QuestionEnd

% Q 2024 21
\QuestionPage{2.4 微分中值定理及其应用}{解答题}{2024 年第 21 题}{3}{中值定理与导数估计}{095 / 408}
设函数 \(f(x)\) 具有二阶导数，且
\[f'(0)=f'(1),\qquad |f''(x)|\le 1.
\]
证明：
\begin{enumerate}
\item 当 \(x\in(0,1)\) 时，
\[\left|f(x)-f(0)(1-x)-f(1)x\right|\le \frac{x(1-x)}{2};
\]
\item \[\left|\int_0^1 f(x)\,dx-\frac{f(0)+f(1)}{2}\right|\le \frac{1}{12}.
\]
\end{enumerate}
\QuestionEnd

\SectionHeading{2.5}{一元函数微分学及其应用}{Taylor定理及其应用}{定理与要点\quad 教材 PDF 第 161 页起\hfill 本节 9 题}
\pdfbookmark[2]{2.5 Taylor定理及其应用}{section-2.5}
\Theory{定理 5.1}{162}{带 Peano 余项的 Taylor 定理}{若 f 在 x\textsubscript{0} 处 n 阶可微，函数等于该点 n 次 Taylor 多项式加 o((x \ensuremath{-} x\textsubscript{0})\textasciicircum{}n)。}
\Theory{定理 5.2}{164}{带 Lagrange 余项的 Taylor 定理}{区间上 n+1 阶可导时，余项为 f\textasciicircum{}(n+1)(\ensuremath{\xi})(x \ensuremath{-} x\textsubscript{0})\textasciicircum{}(n+1)/(n+1)!，\ensuremath{\xi} 在两点之间。}
\Theory{公式}{165--167}{Maclaurin 公式}{在 x = 0 处展开时，n 次项的系数为 f\textasciicircum{}(n)(0)/n!。求极限时保留到相消后首个非零项。}
% Q 2018 1
\QuestionPage{2.5 Taylor定理及其应用}{选择题}{2018 年第 1 题}{1}{指数型极限与展开}{096 / 408}
若$\lim_{x \to 0} \left(\mathrm{e}^x + ax^2 + bx \right)^{\frac{1}{x^2}} = 1$，则\pickout{}
\begin{abcd}
\item $a = \frac{1}{2}\;,\;b = - 1$．
\item $a = - \frac{1}{2}\;,\;b = - 1$．
\item $a = \frac{1}{2}\;,\;b = 1$．
\item $a = - \frac{1}{2}\;,\;b = 1$．
\end{abcd}
\QuestionEnd

% Q 2020 4
\QuestionPage{2.5 Taylor定理及其应用}{选择题}{2020 年第 4 题}{1}{由幂级展开求高阶导数值}{097 / 408}
已知函数 \(f\left( x \right) = x^{2} \ln \left( 1-x \right)\)，当 \(n \geq 3\) 时，\(f^{\left( n \right)}\left( 0 \right) =\)
\choices{\(-\dfrac{n!}{n-2}\)}{\(\dfrac{n!}{n-2}\)}{\(-\dfrac{\left( n-2 \right)!}{n}\)}{\(\dfrac{\left( n-2 \right)!}{n}\)}
\QuestionEnd

% Q 2021 5
\QuestionPage{2.5 Taylor定理及其应用}{选择题}{2021 年第 5 题}{1}{二次泰勒多项式}{098 / 408}
设函数 \(f(x)=\sec x\) 在 \(x=0\) 处的 2 次泰勒多项式为 \(1+ax+bx^2\)，则
\choices{\(a=1\)，\(b=-\dfrac{1}{2}\)}{\(a=1\)，\(b=\dfrac{1}{2}\)}{\(a=0\)，\(b=-\dfrac{1}{2}\)}{\(a=0\)，\(b=\dfrac{1}{2}\)}
\QuestionEnd

% Q 2022 3
\QuestionPage{2.5 Taylor定理及其应用}{选择题}{2022 年第 3 题}{1}{二阶展开与极限}{099 / 408}
设 \(f\left( x \right)\) 在 \(x = x_{0}\) 处有二阶导数，则 \(\left( \ \right)\)
\choices{当 \(f\left( x \right)\) 在 \(x_{0}\) 的某邻域内单调增加时，\(f^{\prime}\left( x_{0} \right) > 0\)}{当 \(f^{\prime}\left( x_{0} \right) > 0\) 时，\(f\left( x \right)\) 在 \(x_{0}\) 的某邻域内单调增加}{当 \(f\left( x \right)\) 在 \(x_{0}\) 的某邻域内是凹函数时，\(f^{\prime\prime}\left( x_{0} \right) > 0\)}{当 \(f^{\prime\prime}\left( x_{0} \right) > 0\) 时，\(f\left( x \right)\) 在 \(x_{0}\) 的某邻域内是凹函数}
\QuestionEnd

% Q 2026 12
\QuestionPage{2.5 Taylor定理及其应用}{填空题}{2026 年第 12 题}{2}{局部展开求函数极限}{100 / 408}
\[\lim_{x\to 0}\left(\frac1x-\frac{\ln(1+x)}{x\sin x}\right)=\ \blank{}.
\]
\QuestionEnd

% Q 2009 15
\QuestionPage{2.5 Taylor定理及其应用}{解答题}{2009 年第 15 题}{3}{展开求极限}{101 / 408}
求极限$\lim_{x \to 0} \frac{\left(1 - \cos x \right)\left[x - \ln(1 + \tan x) \right]}{\sin^4 x}$．
\QuestionEnd

% Q 2014 15
\QuestionPage{2.5 Taylor定理及其应用}{解答题}{2014 年第 15 题}{2}{变上限积分与局部展开}{102 / 408}
求极限$\lim_{x \to +\infty}
\frac{\int_1^x \left[t^2\left(\mathrm{e}^{\frac{1}{t}} - 1\right) - t \right]\,\mathrm{d} t}
     {x^2\ln \left(1 + \frac{1}{x}\right)}$．
\QuestionEnd

% Q 2016 15
\QuestionPage{2.5 Taylor定理及其应用}{解答题}{2016 年第 15 题}{2}{三角函数展开求极限}{103 / 408}
求极限$\lim_{x \to 0} (\cos 2x + 2x\sin x)^{\frac{1}{x^4}}$．
\QuestionEnd

% Q 2021 17
\QuestionPage{2.5 Taylor定理及其应用}{解答题}{2021 年第 17 题}{2}{局部展开求极限}{104 / 408}
求极限
\[\lim_{x \to 0} \left(\frac{1+\int_{0}^{x} e^{t^{2}} \,\mathrm{d} t}{e^{x}-1}-\frac{1}{\sin x}\right).
\]
\QuestionEnd

\SectionHeading{2.6}{一元函数微分学及其应用}{函数性态的研究}{定理与要点\quad 教材 PDF 第 171 页起\hfill 本节 25 题}
\pdfbookmark[2]{2.6 函数性态的研究}{section-2.6}
\Theory{定理 6.1}{171}{单调性判别}{区间上连续且内部可导，单调增（减）等价于内部导数非负（非正）。严格正（负）可推出严格单调。}
\Theory{定理 6.2}{173}{极值的第一判别法}{驻点左侧导数非负、右侧非正时为极大值，反向为极小值。两侧导数严格同号时无极值。}
\Theory{定理 6.3}{174}{极值的第二判别法}{驻点处二阶导数为正则取极小值，为负则取极大值。}
\Theory{定理 6.4}{175}{高阶导数判别极值}{驻点的首个非零高阶导数若为偶数阶，正值对应极小、负值对应极大。奇数阶无极值。}
\Theory{定理 6.5}{179}{凹凸性判别}{按本书术语，区间内 f\ensuremath{{}^{\prime\prime}} > 0 则图像为凹，f\ensuremath{{}^{\prime\prime}} < 0 则为凸。}
83


## tool · 2026-11-10T10:02:10Z


Script completed
Wall time 0.1 seconds
Output:

\Theory{定理 6.5}{179}{凹凸性判别}{按本书术语，区间内 f\ensuremath{{}^{\prime\prime}} > 0 则图像为凹，f\ensuremath{{}^{\prime\prime}} < 0 则为凸。}
\Theory{要点}{175--182}{最值与拐点}{闭区间求最值要比较内部候选点和端点。判定拐点要核对曲线两侧凹凸性变化。}
% Q 2011 3
\QuestionPage{2.6 函数性态的研究}{选择题}{2011 年第 3 题}{1}{驻点个数}{105 / 408}
函数$f(x) = \ln \left| (x - 1)(x - 2)(x - 3) \right|$的驻点个数为\pickout{}
\begin{abcd}
\item $0$．
\item $1$．
\item $2$．
\item $3$．
\end{abcd}
\QuestionEnd

% Q 2014 3
\QuestionPage{2.6 函数性态的研究}{选择题}{2014 年第 3 题}{1}{凹凸性与弦线}{106 / 408}
设函数$f(x)$具有二阶导数，$g(x) = f(0)(1 - x) + f(1)x$，则在区间$[0,1]$上\pickout{}
\begin{abcd}
\item 当$f'(x) \ge 0$时，$f(x) \ge g(x)$．
\item 当$f'(x) \ge 0$时，$f(x) \le g(x)$．
\item 当$f''(x) \ge 0$时，$f(x) \ge g(x)$．
\item 当$f''(x) \ge 0$时，$f(x) \le g(x)$．
\end{abcd}
\QuestionEnd

% Q 2015 4
\QuestionPage{2.6 函数性态的研究}{选择题}{2015 年第 4 题}{1}{由二阶导数图像判定拐点}{107 / 408}
设函数$f(x)$在$\left(-\infty , +\infty \right)$内连续，
其中二阶导数$f''(x)$的图形如图所示，则曲线$y = f(x)$的拐点的个数为\pickout{}
\par\centerline{\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.483697,yscale=-0.483697]
\path[use as bounding box] (0,0) rectangle (400,248);
\path[fill=black!100,even odd rule,shift={(158,16)}] svg {M0 0 C2.3 2.1 3.8 4.2 5.2 7 C5.5 7.7 5.9 8.4 6.2 9.1 C7 11 7 11 7 14 C5.3 14 3.7 14 2 14 C2 60.9 2 107.7 2 156 C8.3 155.7 14.5 155.3 21 155 C21.6 153.2 22.1 151.5 22.7 149.7 C31.8 121.2 41.5 99.1 69 84.8 C88.5 75.1 109.6 69.6 130.5 63.8 C135.4 62.4 140.4 61 145.4 59.6 C146 59.4 146.7 59.2 147.3 59 C150.4 58.1 153.5 57.2 156.6 56.3 C157.6 56 158.7 55.7 159.8 55.4 C160.7 55.1 161.7 54.9 162.6 54.6 C165 54 165 54 168 54 C168 54.7 168 55.3 168 56 C157.6 59.6 147.1 62.7 136.5 65.5 C72.2 82.7 72.2 82.7 53 99 C52.3 99.6 51.6 100.2 50.9 100.8 C35.5 114.6 29.8 137.1 24 156 C76.1 156 128.3 156 182 156 C182 154 182 152 182 150 C187 151.5 191.4 153.6 196 156 C192.3 159.1 186.9 163 182 163 C182 161.3 182 159.7 182 158 C129.5 158 77.1 158 23 158 C22.3 161.6 21.7 165.3 21 169 C20.2 172.7 19.5 176.4 18.7 180.1 C18.4 181.1 18.2 182.1 18 183.1 C17.5 185.2 17.1 187.3 16.6 189.4 C15.9 192.6 15.2 195.8 14.5 199 C14.1 201 13.7 203.1 13.2 205.1 C13 206.1 12.8 207.1 12.6 208 C12.4 208.9 12.2 209.8 12 210.7 C11.8 211.5 11.7 212.3 11.5 213.1 C11 215 11 215 10 217 C9.3 217 8.7 217 8 217 C9.7 205.7 12.2 194.6 14.6 183.5 C15 181.6 15.4 179.6 15.8 177.7 C16.2 175.8 16.6 174 17 172.2 C17.1 171.7 17.1 171.7 17.6 169.5 C17.7 168.7 17.9 167.9 18.1 167.1 C18.2 166.4 18.4 165.7 18.6 165 C19 163 19.5 161 20 159 C14.1 158.7 8.1 158.3 2 158 C2 180.1 2 202.2 2 225 C1.3 225 0.7 225 0 225 C0 202.9 0 180.8 0 158 C-44.2 158 -88.4 158 -134 158 C-134.3 157.3 -134.7 156.7 -135 156 C-110.9 155.7 -86.8 155.3 -62 155 C-64.6 152.4 -67.3 149.7 -70 147 C-71.7 144.7 -73.1 142.5 -74.5 140 C-74.9 139.4 -75.3 138.7 -75.6 138 C-79.2 131.7 -82.5 125.3 -85.6 118.8 C-87 115.9 -88.4 113.1 -89.8 110.3 C-91.2 107.5 -92.6 104.6 -94 101.8 C-94.6 100.4 -95.3 99 -96 97.6 C-97 95.5 -98 93.5 -99 91.5 C-99.6 90.3 -100.2 89.1 -100.8 87.9 C-102 85 -102 85 -102 82 C-97.9 85.5 -96 89.6 -93.7 94.4 C-93.3 95.2 -92.9 96 -92.5 96.9 C-91.3 99.5 -90 102.2 -88.8 104.8 C-68.7 146.8 -68.7 146.8 -58 154 C-51.5 154.9 -44.5 152.5 -39 149 C-29.8 141.5 -25.5 128.7 -22.5 117.6 C-22.3 116.8 -22 116 -21.8 115.2 C-19.8 107.8 -18.5 100.2 -17.3 92.5 C-17 90.2 -16.6 87.8 -16.2 85.5 C-15.7 82.2 -15.2 79 -14.7 75.7 C-13.7 69.1 -12.7 62.5 -11.6 56 C-11.3 54 -11 52.1 -10.6 50.2 C-10.5 49.1 -10.3 47.9 -10.1 46.8 C-9.9 45.8 -9.8 44.8 -9.6 43.7 C-9 41 -8.1 38.6 -7 36 C-6.3 36.3 -5.7 36.7 -5 37 C-5.1 37.3 -5.1 37.3 -5.3 38.7 C-7.3 49.2 -9.2 59.8 -10.7 70.4 C-10.8 70.9 -10.8 70.9 -11.1 73.3 C-11.7 77.2 -12.2 81 -12.8 84.9 C-14.3 95.7 -16.1 106.3 -19 116.9 C-19.2 117.8 -19.5 118.7 -19.7 119.6 C-23.8 134.1 -30.2 146.5 -43 155 C-28.8 155.3 -14.6 155.7 0 156 C0 109.1 0 62.3 0 14 C-1.7 14 -3.3 14 -5 14 C-5.3 13.3 -5.7 12.7 -6 12 C-4.8 9.2 -4.8 9.2 -3.1 5.9 C-2.5 4.8 -1.9 3.7 -1.3 2.6 C-0.9 1.7 -0.5 0.9 0 0 Z };
\path[fill=black!100,even odd rule,shift={(145.625,180.25)}] svg {M0 0 C0.6 0.1 0.6 0.1 3.4 0.8 C4.9 3.8 4.6 6.4 4.4 9.8 C2.8 13.8 1.4 16.9 -2.6 18.8 C-6.3 18.6 -6.3 18.6 -9.6 17.8 C-11.2 14.5 -11.1 11.2 -10.6 7.8 C-8 2.8 -6 -0.4 0 0 Z M-3.6 0.8 C-7.3 5.5 -8.4 8.7 -8.6 14.8 C-8.3 15.2 -8.3 15.2 -6.6 17.8 C-4.3 17.6 -4.3 17.6 -1.6 16.8 C1.9 12 1.7 7.4 1.4 1.8 C-0.3 1.4 -1.9 1.1 -3.6 0.8 Z };
\path[fill=black!100,even odd rule,shift={(135,19)}] svg {M0 0 C1.3 0 2.6 0 4 0 C4.3 2.6 4.7 5.3 5 8 C6.5 6.8 6.5 6.8 8 5 C8.2 2.3 8.2 2.3 8 0 C9.3 0 10.6 0 12 0 C10.7 4.6 8.9 8 6.1 11.9 C5.4 12.8 4.7 13.8 4 14.8 C3.3 15.5 2.7 16.3 2 17 C1 17 0 17 -1 17 C-0.5 16.6 0 16.3 0.5 15.9 C2.7 13.2 2.1 11.3 1.8 7.9 C1.6 6.9 1.5 5.8 1.4 4.7 C1 2 1 2 0 0 Z };
\path[fill=black!100,even odd rule,shift={(343,184)}] svg {M0 0 C1.9 0.2 1.9 0.2 4 1 C5.2 3.2 5.2 3.2 6.2 5.9 C6.5 6.8 6.8 7.7 7.2 8.7 C7.4 9.4 7.7 10.2 8 11 C8.3 11.7 8.7 12.3 9 13 C7.1 12.7 7.1 12.7 5 12 C4.3 11 3.7 10 3 9 C2.7 10.3 2.3 11.6 2 13 C0.7 13 -0.6 13 -2 13 C-0.8 10.5 0 9 2 7 C1.7 4.4 1.2 2.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(350,184)}] svg {M0 0 C1 0 2 0 3 0 C2.3 1.3 1.7 2.6 1 4 C0.7 2.7 0.3 1.4 0 0 Z };
\end{tikzpicture}}
\begin{abcd}
\item $0$．
\item $1$．
\item $2$．
\item $3$．
\end{abcd}
\QuestionEnd

% Q 2016 4
\QuestionPage{2.6 函数性态的研究}{选择题}{2016 年第 4 题}{1}{由导函数图像判断性态}{108 / 408}
设函数$f(x)$在$(-\infty , +\infty)$内连续，其导函数的图形如图所示，则\pickout{}
\par\centerline{\begin{tikzpicture}[scale=\DiagramScale,x=1pt,y=1pt,xscale=0.439724,yscale=-0.439724]
\path[use as bounding box] (0,0) rectangle (440,348);
\path[fill=black!100,even odd rule,shift={(53,10)}] svg {M0 0 C2.6 3.1 4 6.1 5.5 9.9 C5.7 10.4 5.7 10.4 6.8 13.2 C7.3 14.4 7.7 15.6 8.2 16.8 C8.7 17.9 9.1 19.1 9.6 20.3 C10.7 23.2 11.9 26.1 13 29 C8.9 28.4 5.7 27 2 25 C1 58.6 1 58.6 8.1 66.4 C10 68.4 12 70.2 14 72 C56.6 124.7 64.4 207.8 63 273 C67.6 273 72.2 273 77 273 C77 272 77.1 271 77.1 270 C79.4 216.3 87.4 143.2 129 104 C142.1 92.8 155.2 89.2 172 90 C180.1 91.1 185.9 95.9 191 102 C205.3 123.3 207.2 151.9 211.1 176.7 C215.1 202.2 220 227.8 234.5 249.7 C236 252 236 252 236 254 C236.7 254 237.3 254 238 254 C239.4 255.5 239.4 255.5 241.1 257.6 C247.6 265.2 254.8 271 265 272.4 C273.3 271.2 279.2 266 284.2 259.5 C308.8 225.9 316.2 177.6 326 138 C327 138 328 138 329 138 C328.4 143.3 327.5 148.5 326.2 153.7 C326.1 154.1 326.1 154.1 325.7 155.9 C325.1 158.2 324.5 160.5 323.9 162.8 C323.7 163.6 323.5 164.4 323.3 165.2 C319.9 178.9 316.1 192.5 311.9 206 C311.3 208 310.7 209.9 310.2 211.8 C303.4 234.1 293.9 254.1 279 272 C295.5 272 312 272 329 272 C328.3 270.4 327.7 268.7 327 267 C326.3 265.3 325.7 263.7 325 262 C335.1 264.6 344.5 268.9 354 273 C354 273.7 354 274.3 354 275 C350.3 276.7 346.5 278.3 342.8 279.9 C341.8 280.4 340.7 280.9 339.6 281.4 C338.6 281.8 337.6 282.3 336.5 282.7 C335.6 283.1 334.6 283.5 333.7 284 C331.1 285 328.7 285.6 326 286 C327.1 282.5 328.3 279.3 330 276 C288.8 276.2 288.8 276.2 80 277 C79.7 286.9 79.3 296.8 79 307 C77.7 307 76.4 307 75 307 C75.3 297.1 75.7 287.2 76 277 C74.7 277 73.4 277 72 277 C71.7 277.7 71.3 278.3 71 279 C70 279 69 279 68 279 C67.3 278.3 66.7 277.7 66 277 C65.3 277 64.7 277 64 277 C64 277.3 64 277.3 63.9 278.7 C63.8 281.3 63.7 284 63.6 286.6 C63.5 287.5 63.5 288.4 63.4 289.3 C63.2 294.2 62.8 299.1 62 304 C61 304 60 304 59 304 C59 294.8 59 285.5 59 276 C56.3 276.2 53.5 276.3 50.7 276.5 C34.8 277.3 18.9 277.1 3 277 C2.7 293.5 2.3 310 2 327 C1 327 0 327 -1 327 C-1 310.5 -1 294 -1 277 C-6.3 277 -11.5 277 -16.9 277.1 C-28.7 277.1 -40.3 277 -52 276 C-52 275 -52 274 -52 273 C-35.5 273 -19 273 -2 273 C-1.9 245.3 -1.8 217.6 -1.8 189.9 C-1.8 177.1 -1.7 164.2 -1.7 151.4 C-1.7 140.2 -1.6 129 -1.6 117.8 C-1.6 111.8 -1.6 105.9 -1.6 100 C-1.5 94.4 -1.5 88.8 -1.5 83.2 C-1.5 81.2 -1.5 79.1 -1.5 77.1 C-1.5 74.3 -1.5 71.5 -1.5 68.7 C-1.5 68.3 -1.5 68.3 -1.5 66.2 C-1.5 61.2 -2.4 58.6 -6 55 C-7.6 53.5 -7.6 53.5 -9.1 52.4 C-9.6 52 -10.2 51.5 -10.8 51.1 C-11.1 50.9 -11.1 50.9 -12.5 49.8 C-13.1 49.4 -13.6 48.9 -14.2 48.5 C-17 46.4 -19.8 44.4 -23 43 C-22.7 42 -22.3 41 -22 40 C-18.1 40.6 -15.6 42.6 -12.4 44.9 C-9.7 47 -6.9 49.1 -4 51 C-4 51.7 -4 52.3 -4 53 C-3 53 -2 53 -1 53 C-1.2 52.3 -1.3 51.6 -1.5 50.8 C-2 48 -2.1 45.5 -2.1 42.7 C-2.1 41.7 -2.1 40.7 -2.1 39.7 C-2.1 39.2 -2.1 39.2 -2.1 36.7 C-2.1 35.7 -2.1 34.6 -2 33.6 C-2 31.1 -2 28.5 -2 26 C-5.5 27.1 -8.8 28.3 -12 30 C-10.2 23.1 -7.7 16.5 -4.9 9.9 C-4.5 9.1 -4.2 8.2 -3.8 7.3 C-1.1 1.1 -1.1 1.1 0 0 Z M2 64 C2 133 2 201.9 2 273 C20.8 273 39.6 273 59 273 C61.4 268.3 59.9 261.7 59.8 256.5 C59.7 255.8 59.7 255 59.7 254.3 C58.2 208.9 52.8 162.5 36 120 C35.7 119.3 35.4 118.5 35.1 117.8 C29.1 102.2 21.2 87.8 11.6 74.1 C11.2 73.5 10.8 72.9 10.4 72.4 C7.9 68.8 5.6 66.9 2 64 Z M137 102 C135.9 102.6 134.9 103.2 133.8 103.9 C129.9 106.8 127 110.2 124 114 C123.3 114.9 122.6 115.7 121.8 116.6 C99.1 145.4 91.2 185.6 85.8 220.9 C85.6 221.8 85.5 222.6 85.4 223.4 C84 232.1 82.8 240.9 81.8 249.7 C81.8 250 81.8 250 81.6 251.9 C80.9 258.5 80.6 265.3 81 272 C82 273 82 273 84.8 273.1 C86 273.1 87.3 273.1 88.5 273.1 C88.9 273.1 88.9 273.1 90.6 273.1 C93 273.1 95.3 273.1 97.6 273.1 C99.3 273.1 101 273.1 102.6 273.1 C107.2 273.1 111.7 273.1 116.2 273.1 C121 273.1 125.7 273.1 130.4 273.1 C139.4 273.1 148.4 273.1 157.3 273.1 C167.6 273.1 177.8 273.1 188 273.1 C209 273 230 273 251 273 C249.7 269 247.3 267.5 244 265 C243.3 265 242.7 265 242 265 C242 264.3 242 263.7 242 263 C240.6 261.4 240.6 261.4 239 260 C238.3 260 237.7 260 237 260 C236.8 259.5 236.5 258.9 236.2 258.4 C234.7 255.4 233 252.7 231 250 C230.3 250 229.7 250 229 250 C228.9 249.5 228.8 249 228.7 248.4 C227.8 245.2 226.3 242.4 224.8 239.4 C213.4 215.4 209.5 189.2 205.5 163.2 C198.1 114.8 198.1 114.8 186 101 C185.3 101 184.7 101 184 101 C184 100.3 184 99.7 184 99 C182.6 98.2 181.2 97.4 179.8 96.6 C179.4 96.3 179.4 96.3 177.4 95.2 C163.8 88.4 148.8 95 137 102 Z };
\path[fill=black!100,even odd rule,shift={(38,294)}] svg {M0 0 C3.3 2.8 4.8 4.7 5.4 9 C5.3 14.9 2.4 20.6 -1.8 24.8 C-3.6 26.2 -3.6 26.2 -7 28 C-8 27.7 -9 27.3 -10 27 C-9.3 26.3 -8.5 25.7 -7.8 25 C-2.5 19.7 -0.1 13.4 0 6 C-1 3.5 -1 3.5 -3 2 C-6.7 1.8 -6.7 1.8 -10 2 C-7.9 -2.2 -3.9 -1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(28,295)}] svg {M0 0 C-1 2.1 -2.1 4.2 -3.3 6.3 C-6.3 11.8 -8.3 16.6 -7 23 C-4.6 25.4 -3.2 25.5 0 26 C0 26.7 0 27.3 0 28 C-7.3 27.5 -7.3 27.5 -10.4 25.3 C-12.8 21.8 -13.4 19.1 -12.6 14.9 C-11 9.2 -8.3 5 -4 1 C-2 0 -2 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(73,4)}] svg {M0 0 C2.3 0 4.6 0 7 0 C7.7 4.3 8.3 8.6 9 13 C10 12.3 11 11.7 12 11 C10.3 15.2 8.6 16.4 5 20 C4.3 14.4 3.7 8.8 3 3 C2 2.7 1 2.3 0 2 C0 1.3 0 0.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(421,276)}] svg {M0 0 C4.5 -0.4 4.5 -0.4 6.8 1.4 C8.8 4 9 4.9 8.9 8.3 C9 11.8 9.5 13.9 11 17 C9.7 17.3 8.4 17.7 7 18 C6.3 16.4 5.7 14.7 5 13 C4 13.3 3 13.7 2 14 C2.1 13.4 2.1 12.8 2.2 12.1 C2.3 11.7 2.3 11.7 2.5 9.7 C2.6 8.9 2.7 8.1 2.8 7.3 C3 5 3 5 3 2 C2 1.7 1 1.3 0 1 C0 0.7 0 0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(87,4)}] svg {M0 0 C1 0 2 0 3 0 C2.5 6.4 2.5 6.4 -0.1 9.4 C-0.7 10 -1.3 10.5 -2 11 C-1.6 10.3 -1.3 9.6 -0.9 8.8 C0.1 5.7 -0.2 4.1 -1 1 C-0.7 0.7 -0.3 0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(76,25)}] svg {M0 0 C0 1 0 2 0 3 C-2.5 5.4 -3.5 6 -7 6 C-6.7 4.7 -6.3 3.4 -6 2 C-5.6 1.9 -5.6 1.9 -3.6 1.6 C-1 1 -1 1 0 0 Z };
\path[fill=black!100,even odd rule,shift={(422,290)}] svg {M0 0 C0 1 0 2 0 3 C-1.6 3.3 -3.3 3.7 -5 4 C-5 3 -5 2 -5 1 C-3.4 0.7 -1.7 0.3 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,218)}] svg {M0 0 C1 0 2 0 3 0 C3 1.7 3 3.3 3 5 C2 5 1 5 0 5 C0 3.3 0 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,118)}] svg {M0 0 C1 0 2 0 3 0 C3 1.7 3 3.3 3 5 C2 5 1 5 0 5 C0 3.3 0 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,251)}] svg {M0 0 C1 0.3 2 0.7 3 1 C3 2.3 3 3.6 3 5 C2 5 1 5 0 5 C0 3.3 0 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,85)}] svg {M0 0 C1 0 2 0 3 0 C2.7 1.7 2.3 3.3 2 5 C1.3 5 0.7 5 0 5 C0 3.3 0 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,318)}] svg {M0 0 C1 0 2 0 3 0 C2.7 1.6 2.3 3.3 2 5 C1.3 4.7 0.7 4.3 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,293)}] svg {M0 0 C1 0 2 0 3 0 C2.7 1.6 2.3 3.3 2 5 C1.3 4.7 0.7 4.3 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(436,276)}] svg {M0 0 C-0.3 1 -0.7 2 -1 3 C-2.6 3 -4.3 3 -6 3 C-6 2.3 -6 1.7 -6 1 C-4 0 -4 0 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,210)}] svg {M0 0 C1 0 2 0 3 0 C2.7 1.7 2.3 3.3 2 5 C1.3 4.7 0.7 4.3 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,193)}] svg {M0 0 C1 0.3 2 0.7 3 1 C3 2.3 3 3.6 3 5 C2 5 1 5 0 5 C0 3.3 0 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,135)}] svg {M0 0 C1 0 2 0 3 0 C2.7 1.7 2.3 3.3 2 5 C1.3 4.7 0.7 4.3 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,310)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,302)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,277)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,268)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,260)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(122,243)}] svg {M0 0 C0.7 0 1.3 0 2 0 C1.7 1.7 1.3 3.3 1 5 C0.3 4.7 -0.3 4.3 -1 4 C-0.7 2.7 -0.3 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,235)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,227)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,202)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,185)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,177)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,169)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(122,160)}] svg {M0 0 C0.7 0 1.3 0 2 0 C1.7 1.7 1.3 3.3 1 5 C0.3 4.7 -0.3 4.3 -1 4 C-0.7 2.7 -0.3 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,152)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,144)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,127)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,110)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,102)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,94)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,77)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,69)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(122,60)}] svg {M0 0 C0.7 0.3 1.3 0.7 2 1 C1.7 2.3 1.3 3.6 1 5 C0.3 5 -0.3 5 -1 5 C-0.7 3.4 -0.3 1.7 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,52)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(121,44)}] svg {M0 0 C1 0 2 0 3 0 C3 1.3 3 2.6 3 4 C2 4 1 4 0 4 C0 2.7 0 1.4 0 0 Z };
\path[fill=black!100,even odd rule,shift={(432,290)}] svg {M0 0 C0.3 0.2 0.3 0.2 2 1 C1.7 1.2 1.7 1.2 0 2 C0 1.3 0 0.7 0 0 Z };
\end{tikzpicture}}
\begin{abcd}
\item 函数$f(x)$有$2$个极值点，曲线$y = f(x)$有$2$个拐点．
\item 函数$f(x)$有$2$个极值点，曲线$y = f(x)$有$3$个拐点．
\item 函数$f(x)$有$3$个极值点，曲线$y = f(x)$有$1$个拐点．
\item 函数$f(x)$有$3$个极值点，曲线$y = f(x)$有$2$个拐点．
\end{abcd}
\QuestionEnd

% Q 2018 4
\QuestionPage{2.6 函数性态的研究}{选择题}{2018 年第 4 题}{1}{凹凸性与积分平均值}{109 / 408}
设函数$f(x)$在$[0,1]$上二阶可导，且$\int_0^1 f(x)\,\mathrm{d} x = 0$，则\pickout{}
\begin{abcd}
\item 当$f'(x) < 0$时，$f\left(\frac{1}{2} \right) < 0$．
\item 当$f''(x) < 0$时，$f\left(\frac{1}{2} \right) < 0$．
\item 当$f'(x) > 0$时，$f\left(\frac{1}{2} \right) < 0$．
\item 当$f''(x) > 0$时，$f\left(\frac{1}{2} \right) < 0$．
\end{abcd}
\QuestionEnd

% Q 2019 2
\QuestionPage{2.6 函数性态的研究}{选择题}{2019 年第 2 题}{1}{拐点坐标}{110 / 408}
曲线$y = x\sin x + 2\cos x$（$- \frac{\pi}{2} < x < \frac{3\pi}{2}$）的拐点是\pickout{}
\begin{abcd}
\item $\left(\frac{\pi}{2},\frac{\pi}{2} \right)$．
\item $(0,2)$．
\item $(\pi , - 2)$．
\item $\left(\frac{3\pi}{2}, - \frac{3\pi}{2} \right)$．
\end{abcd}
\QuestionEnd

% Q 2020 6
\QuestionPage{2.6 函数性态的研究}{选择题}{2020 年第 6 题}{1}{由导数不等式判断函数比值}{111 / 408}
设函数 \(f\left( x \right)\) 在区间 \(\left[ -2,2 \right]\) 上可导，且 \(f^{\prime}\left( x \right) > f\left( x \right) > 0\)，则
\choices{\(\dfrac{f\left( -2 \right)}{f\left( -1 \right)} > 1\)}{\(\dfrac{f\left( 0 \right)}{f\left( -1 \right)} > e\)}{\(\dfrac{f\left( 1 \right)}{f\left( -1 \right)} < e^{2}\)}{\(\dfrac{f\left( 2 \right)}{f\left( -1 \right)} < e^{3}\)}
\QuestionEnd

% Q 2021 4
\QuestionPage{2.6 函数性态的研究}{选择题}{2021 年第 4 题}{1}{单调性与零点个数}{112 / 408}
设函数 \(f(x)=ax-b\ln x\)，其中 \(a>0\)。若 \(f(x)\) 有两个零点，则 \(\dfrac{b}{a}\) 的取值范围是
\choices{\(\left(e,+\infty\right)\)}{\(\left(0,e\right)\)}{\(\left(0,\dfrac{1}{e}\right)\)}{\(\left(\dfrac{1}{e},+\infty\right)\)}
\QuestionEnd

% Q 2023 6
\QuestionPage{2.6 函数性态的研究}{选择题}{2023 年第 6 题}{1}{积分函数的最小值}{113 / 408}
若函数
\[f(a)=\int_2^{+\infty}\frac{1}{x(\ln x)^{a+1}}\,dx
\]
在 \(a=a_0\) 处取得最小值，则 \(a_0=\)（ ）。
\choices{\(-\dfrac{1}{\ln(\ln 2)}\)}{\(-\ln(\ln 2)\)}{\(\dfrac{1}{\ln 2}\)}{\(\ln 2\)}
\QuestionEnd

155-L d（1+ ）
156-V1+23
157-V+
158-应选 D.
159-3 设函数f（x）在x =x0处具有2阶导数，则（）
160:（A）当f（x）在x。的某邻域内单调增加时，f（x0）>0.
161:（B） 当f'（x0）>0时，f（x）在x。的某邻域内单调增加.
162:（C）当f（x）在x。的某邻域内是凹函数时，f"（30）>0.
163-一6一
164-```
165-
166-## PDF 第 4 页
167-
168-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2022%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=4) · 本机 OCR
169-
170-```text
171:（D）当f（x0）>0时，f（x）在x。的某邻域内是凹函数.
172-答案
173-EB.
174-分析 本题主要考查一阶导数、二阶导数与函数性态的关系.
175-函数的单调性与一阶导数的关系 设函数f（x）在［a,6］上连续，在（a,b）内可导、若在（a,6）
176:内f（x）≥0，且等号只在有限个点处成立，则f（x）在［a,6］上单调增加.（单调减少的情况对应于
177-f'（x）≤0的情况.）
178-函数的凹凸性与二阶导数的关系 设函数f（x）在［a,6］上连续，在（a，b）内二阶可导.若在
179:（a,b） 内 ”（x）≥0，且等号只在有限个点处成立，则f（x）为［a，6］上的凹函数.（凸函数的情况对
180-經应于f”（x）≤0的情况.）
181-在不确定一阶导函数的连续性的情况下，单点处的一阶导符号不能确定该点邻域内的函数的
182-单调性.在不确定二阶导函数的连续性的情况下，单点处的二阶导符号不能确定该点邻域内的曲
183-线的凹凸性.
184-解）注意到题目条件给出f（x）在x =x。处有二阶导数，故f'（x）在x =2。处连续.从而，
185:> 0. 于是，f（x）在（x-8,3 +8）内单调增加.应选B.
186-下面说明选项A、C、D 不正确.
187:当f（x）在x0的某邻域内单调增加时，我们能得到在该邻域内f'（x）≥0，但却不能保证 '（x）
188->0，因为可能存在有限个点，在这些点处， （x）=0.例如f（x）= ’，该函数在（ ∞，+∞）上单
189-调增加，但是f'（0）=0.选项A不正确.
190-对选项C，考虑f（x）=x*
191:，则f（x）为（-∞，+∞）上的凹函数，但是f”（0）=0. 选项C不正确.
192-对选项D，我们可以考虑二阶导函数存在间断点的例子.若x。为 （x）的间断点，则limf（x）=
193-f"（xo）>0不成立，从而无法通过极限的定义得到x。的一个小邻域，在该小邻域内f"（x）>0.
194-x'sin
195-考虑函数f（x）
196-=
197-，x 0，该函数在 =0处存在二阶导数，但是f”（x）在x=0
198-× =0，
199-处不连续.
200-当 千0时，f（x）=4xsin
201-• - X'cos
202-f（x）-f（0）
203-f'（0） = lim
204-10
205-因此，
206-4x' sin
207-f'（x）=
208-之 当*=0时，由导数定义，
209-x'sin
210-1
211-X
--
249-当 0时，f（x）=12xsin
250-- - 6xcos
251--+
252-如图所示， ”（x）在×=0附近振荡，
253-振幅为1，在x =0附近不存在小邻域使得产”（x）在该邻域上保持不变号，即不存在x=0的小邻域，
254:使得f（x）在该邻域上是凹函数或凸函数.选项D不正确.
255-4
256-aF
257-（A）
258-dx
259-aF
260-（C）
261-dx
262-aFdF
263-d2F
264-=
265-ay’
266-ax？
267-=
268-ay？
269-aF
270-a'F
271-a'F
272-二一
273-dy’ax
274-ay？
--
521-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2022%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=9) · 本机 OCR
522-
523-```text
524-令fx）= In（1+x） ，则 O）=0， （x）=
525-当 E（0,1）时， （x）>0,f（x）
526:单调增加，从而f（x）>f（O）=0，即In（1+x）>
527-In（1 +x）
528-2'1 +Cos X
529-2（1 +cos x）
530-因此，½>1.
531-此外，同样的方法不难证明在（0,1）内，In（1 +x）<x.
532-另一方面，由于在（0,1）内，0< sin x,cos x < 1,1 <1.+sin x <2，故1，的被积函数
533-2x
534-+ sin x
535-In（1+x）
536->x.结合In（1+x）
537-<8可得，一+cos x
538-<x.于是
539-1 + cosx
540-''1 + sinx
541-In（1 +x）
542-1+ cos x
543-.因此，
544-1s > 12：
545-综上所述，应选 A.


## tool · 2026-11-10T10:02:28Z


Script completed
Wall time 0.1 seconds
Output:

302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-195-lim ex
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-196-=+∞，lim et
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-197-= 0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-198-0-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md:199:设函数f（x）在（-∞，+∞）内连续，其导函数的图形如图所示，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-200-则（
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-201-）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md:202:（A）函数f（x）有2个极值点，曲线 =f（x）有2个拐点
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md:203:（B）函数f（x）有2个极值点，曲线y=f（x）有3个拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md:204:（C） 函数f（x）有3个极值点，曲线y=f（x）有1个拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md:205:（D）函数f（x）有3个极值点，曲线y=f（x）有2个拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-206-答案
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-207-B.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-208-分析
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md:209:本题主要考查函数的极值点、拐点等概念，并考查了通过图形分析函数性质，具有一
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-210-定的综合性.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-211-通过考察可能的极值点（驻点与不可导点）左侧、右侧的f’的符号，可以判断某点是否为极值
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-212-点；通过考察可能的拐点（f”=0的点以及产“不存在的点）左侧、右侧的f”的单调性，可以判断某点
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-213-是否为拐点。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-214-解观察图形，f（x）共有4个可能的极值点，从左至右依次记为况」，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-215-42，43，44，其中x，为虚线与x轴的交点，其余三点为f（x）与x轴的交点.在
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-216-分别考察x=*1，22，83，*。左、右小邻域内的f'（x）的符号.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-217-O
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-218-Xs
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-219-*4
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-220-是f（x）的极大值点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-221-—7-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-222-```
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-223-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-224-## PDF 第 5 页
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-225-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-226-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-227-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-228-> 读取原 PDF 时出现警告，建议核对原页。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-229-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-230-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-231-因此，f（x）共有2个极值点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2016数二真题【解析】.md-232-曲线y=f（x）的可能的拐点从左至右依次为（x2，f（ 2）），（4s,f（xs）），（24，f（ 4）），其中
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-376-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-377-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-378-4
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-379-设函数在（-∞，+∞）内连续，其2阶导函数f"（x）的图形如右图
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md:380:所示，则曲线y=f（x）的拐点个数为（
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-381-）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-382-（A）0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-383-（B）1.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-384-（C）2.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-385-（D）3.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-386-答案
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-387-C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-388-f（x）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-389-V/.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-390-分析本题主要考查曲线的拐点的判定.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-391-曲线可能的拐点需考虑二阶导数不存在的点和二阶导数为零的点.若f（x）在x。的某去心邻域
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-392-拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-393-解）由图可知，在（ ∞，+∞）上， ”（x）=0有两个实根x」，22，且 ”（x）在 =0处无定义.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-394-下面我们分别讨论点（x f（xn）），（0,f（O））和（x2，f（ 2））是否为
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-395-f（x）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-396-拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-397-在x =x，的左、右邻域内，f”（x）均大于零.f（x）在该点两侧不变号，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-398-故点（x，f（x，））不是曲线y=f（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-399-在x=0的左侧邻域内，f”（x）>0；在 =0的右侧邻域内， "（x）＜0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-400-f"（x）在该点两侧变号，故点（0，f（O））是曲线y=f（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-401-在× =22的左侧邻域内， （x）＜0；在 = 2的右侧邻域内， （x）>0.f”（x）在该点两侧
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-402-变号，故点（x2，f（ 2））是曲线 =f（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-403-综上所述，曲线y=f（x）共有2个拐点，应选C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-404-注① 注意：f"（x）=0不是拐点的充分条件，本题中的点（x」，f（x」））满足
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-405-f"（x.）=0，但却不是曲线y=f（x）的拐点.此外，不要漏掉f”（x）不存在的点，本题中，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-406-f"（x）在x=0处不存在，但点（0，f（0））是曲线 =f（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-407-② 本题也可以利用下述判别法来判定点（x2，f（x2））为拐点.若函数f（x）在点x，处三
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-408-阶可导且f”（xo）=0，f”（x0） 0，则点（x0，f（xo））为曲线 =f（x）的拐点.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-409-从图中可以看出曲线 =f”（x）在点（ 2,f（ 2））处切线的斜率大于零，从而 ”（ 2）>0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2015数二真题【解析】.md-410-因此由上述判别法可得点（x2，f（x2））拐点，但不能确定其他两点是否为拐点


## tool · 2026-11-10T10:02:41Z


Script completed
Wall time 0.1 seconds
Output:

定的综合性.
通过考察可能的极值点（驻点与不可导点）左侧、右侧的f’的符号，可以判断某点是否为极值
点；通过考察可能的拐点（f”=0的点以及产“不存在的点）左侧、右侧的f”的单调性，可以判断某点
是否为拐点。
解观察图形，f（x）共有4个可能的极值点，从左至右依次记为况」，
42，43，44，其中x，为虚线与x轴的交点，其余三点为f（x）与x轴的交点.在
分别考察x=*1，22，83，*。左、右小邻域内的f'（x）的符号.
O
Xs
*4
是f（x）的极大值点.
—7-
```

## PDF 第 5 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2016%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=5) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
因此，f（x）共有2个极值点.
曲线y=f（x）的可能的拐点从左至右依次为（x2，f（ 2）），（4s,f（xs）），（24，f（ 4）），其中
= （x）的拐点.
曲线 =f（x）的拐点.
=f（x）的拐点.
因此，曲线y=f（x）共有3个拐点.
综上所述，应选B.
注 本题有两个地方容易出错.
① 在判断f（x）的极值点时，只注意到f”（x。）=0，而没有注意到x。左、右两侧小邻域内
的f'（x）均大于零，从而误将x =2。当作极值点.
② 在判断 =f（x）的拐点时，忽略了f”（x）不存在的点，即（ 2，f（ 2）），从而认为只有
2个拐点.
5设函数 （x）（i 1,2）具有二阶连续导数，且f”（x0）<0（i=1,2）.若两条曲线 =
f.（x）（i=1,2）在点（x0,30）处具有公切线y=g（x），且在该点处曲线y=f（x）的曲率大于曲线
=5（x）的曲率，则在x。的某个邻域内，有（
）
（A）fi（x） （x）≤g（x）.
（B）f（x）≤f（x）≤g（x）.
（C）fi（x）≤g（x）≤f（x）.
（D）f（x）≤g（x）≤f（x）.
答案
A.
分析 本题主要考查曲率以及凹、凸曲线的概念.
曲率是用来描述曲线的弯曲程度的一个量.直观地说，曲线在某处的曲率越大，则曲线在该处
弯曲得越厉害.结合曲线上同一点处的曲率半径与曲率互为倒数这一点来看，若两圆在某点处相
1072-19 设函数f（x）在区间［0,1］上具有2阶导数，且f（1）>0，
1073-<0.证明：
1074-（I）方程f（x）=0在区间（0，1）内至少存在一个实根；
1075:（I）方程f（x） "（x）+ f（x） =0在区间（0,1）内至少存在两个不同实根.
1076-分析本题主要考查连续函数的性质以及罗尔定理的应用.
1077-罗尔定理 若函数f（x）在［a，6］上连续，在（a,6）内可导，且f（a）=f（b），则（a,b）内至少存
1078-在一点 E（a,b），使得 （ ）=0.
1079-第（I）问要证明方程f（x）=0在区间（0,1）内至少存在一个实根，可以利用连续函数的零点定
1080-理.由于f（1）>0，故可以考虑证明在x=0附近f（x）<0.这可以利用函数极限的局部保号性得到.
1081-通过观察发现，f（x）f"（x）＋［ '（x）］2=［f（x）f'（x）］’，故不妨设辅助函数F（x）=
1082-f（x）f'（x）.如果能找到三个点，使得在这三个点上F（x）取值相等，那么使用两次罗尔定理即可得
1083-到两个满足 F'（x）=0的点.
1084-此时，第（I）同的结论给出了 F（x）的一个零点.我们可以考虑找到另外两个点，使得在这三
1085-个点上，F（x）=0.
1086-证（I）由于lim
1087-<0，故由函数极限的局部保号性可知，存在0>0，在（0,0）内，
1088-<0，
1089-一21—
--
1101-此，f（x）=0在区间（0,1）内至少存在一个实根.
1102-（II）考虑F（x）= （ ） （x），処
1103-F'（x）=f（ ）f"（x）+［ '（x）］ .
1104:第（I）问等价于证明F'（x）= 0在区间（0,1）内至少存在两个不同实根
1105-若能找到三个点a <b <c，使得F（a）= F（b）= F（c），则由罗尔定理，存在n1E（a.，b），
1106-172E（6,c），满足F'（m）=0,F（72）=0.
1107-由lim /x2<0知，分母趋于零，而极限仍存在，故
1108-连续性
1109-f（0）一
1110-= limf（x） =0, F（O） =f（O）f'（0） =0.
1111-F（x）
1112-由第（I）问的结论知，存在x」E（0,1），满足f（x）=0，从而
1113-F（xi）=f（ ）f（ 」）=0.
1114-另一方面，由于f（0）= 0，f（xi）=0，故由罗尔定理知，存在
1115-J=fx）
1116-如图所示，0＜x2<x,F（O）=F（x2）=F（x」）=0. 由罗尔定理知，存
1117-注本题的证明思路：找到三个点，使得函数F（x）在这三个点上取值相等，从而可以
1118-运用两次罗尔定理，得到两个F'（x）=0的点.


## tool · 2026-11-10T10:02:55Z




## assistant · 2026-11-10T10:02:58Z

已写到第 83 题。两道图像题已用原卷解析核对结论，接下来完成中值定理、泰勒展开和函数性态各题，再核对题号与年份。

## tool · 2026-11-10T10:05:20Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:05:29Z


Script completed
Wall time 0.1 seconds
Output:

\]
由于 \(e^\eta>0\)，所求等式成立。

% SOLUTION 090 2015 21
\textbf{入手角度}\quad 写出切线的横截距，再用区间 \([a,b]\) 上的平均斜率估计 \(f(b)/f'(b)\)。

\textbf{解析}\quad 切线方程为 \(y=f(b)+f'(b)(x-b)\)，所以
\[
x_0=b-\frac{f(b)}{f'(b)}.
\]
由中值定理，存在 \(\xi\in(a,b)\) 使 \(f(b)=(b-a)f'(\xi)\)。\(f'>0\)，且 \(f''>0\) 使 \(f'\) 严格递增，故 \(0<f'(\xi)<f'(b)\)。因此 \(0<f(b)/f'(b)<b-a\)，从而 \(a<x_0<b\)。

% SOLUTION 091 2017 15
\textbf{入手角度}\quad 在积分区间上指数因子介于 \(1\) 和 \(e^x\) 之间，可保留根式积分并夹逼。

\textbf{解析}\quad 对 \(0\le t\le x\)，有
\(\sqrt{x-t}\le \sqrt{x-t}e^t\le e^x\sqrt{x-t}\)。而 \(\int_0^x\sqrt{x-t}\,dt=2x^{3/2}/3\)。积分并除以 \(x^{3/2}\) 得
\[
\frac23\le\frac{\int_0^x\sqrt{x-t}e^t\,dt}{x^{3/2}}\le\frac23 e^x.
\]
令 \(x\to0^+\)，原极限为 \(\boxed{2/3}\)。

% SOLUTION 092 2017 19
\textbf{入手角度}\quad 第二个方程的左端正好是 \((ff')'\)，先利用 \(f\) 的两个零点构造出 \(ff'\) 的三个零点。

\textbf{解析}\quad （1）由 \(f(x)/x\) 的有限负极限知，存在 \(s\in(0,1)\) 使 \(f(s)<0\)。又 \(f(1)>0\)，由连续性存在 \(c\in(s,1)\) 使 \(f(c)=0\)。

（2）同一极限给出 \(f(x)=x[f(x)/x]\to0\)，故 \(f(0)=0\)。在 \([0,c]\) 应用罗尔定理，得 \(d\in(0,c)\) 使 \(f'(d)=0\)。于是 \(H(x)=f(x)f'(x)\) 在 \(0,d,c\) 均为零。分别在 \([0,d]\) 和 \([d,c]\) 应用罗尔定理，得到两个不同内点使
\[
H'(x)=f(x)f''(x)+[f'(x)]^2=0.
\]
所求两根均位于 \((0,1)\)。

% SOLUTION 093 2019 21
\textbf{入手角度}\quad 积分平均值等于端点的较大值，迫使函数在内部取得更高的值。二阶导数的下界可通过加上 \(x^2\) 转化为弦线估计。

\textbf{解析}\quad （1）若处处 \(f(x)\le1\)，由 \(f(0)=0\) 和连续性，有一小段区间 \(f(x)\le1/2\)，使 \(\int_0^1 f(x)\,dx<1\)，矛盾。故最大值大于 \(1\)，只能在某个内点 \(\xi\) 取到，费马定理给出 \(f'(\xi)=0\)。

（2）若处处 \(f''(x)\ge-2\)，令 \(H(x)=f(x)+x^2\)。则 \(H''\ge0\)，且 \(H(0)=0,H(1)=2\)，由弦线估计有 \(H(x)\le2x\)。于是
\[
1=\int_0^1 f(x)\,dx\le\int_0^1(2x-x^2)\,dx=\frac23,
\]
矛盾。因此存在 \(\eta\in(0,1)\) 使 \(f''(\eta)<-2\)。

% SOLUTION 094 2023 21
\textbf{入手角度}\quad 第一问构造过三个给定点的二次多项式。第二问比较整段的平均斜率与极值点处的零斜率。

\textbf{解析}\quad （1）令 \(P(x)=Ax^2+Bx\)，其中
\[
A=\frac{f(a)+f(-a)}{2a^2},\qquad
B=\frac{f(a)-f(-a)}{2a}.
\]
则 \(F=f-P\) 在 \(-a,0,a\) 均为零。分别在 \([-a,0]\)、\([0,a]\) 应用罗尔定理，得到 \(F'\) 的两个零点，再在两点之间应用一次，得 \(F''(\xi)=0\)。于是 \(f''(\xi)=2A=[f(a)+f(-a)]/a^2\)。

（2）设内点 \(c\) 为极值点，则 \(f'(c)=0\)。在 \([-a,a]\) 应用中值定理，存在 \(d\in(-a,a)\) 使 \(f'(d)=[f(a)-f(-a)]/(2a)\)。若两端值相等，所求不等式显然成立。否则 \(d\ne c\)，对 \(f'\) 在这两点之间应用中值定理，得某个 \(\eta\) 满足
\[
|f''(\eta)|=\frac{|f'(d)-f'(c)|}{|d-c|}
\ge\frac{|f(a)-f(-a)|}{4a^2}.
\]
\ln f(b)-\ln f(a)>b-a,
\qquad \frac{f(b)}{f(a)}>e^{b-a}.
\]
取 \(a=-1,b=0\) 即得 B。取 \(b=1,2\) 得到与 C、D 相反的方向，而 \(f'>0\) 使 \(f(-2)<f(-1)\)。选 B。

% SOLUTION 112 2021 4
\textbf{入手角度}\quad 两个零点只能在唯一的极小值两侧出现，先用导数定位该点。

\textbf{解析}\quad 定义域为 \(x>0\)，且 \(f'(x)=a-b/x\)。若 \(b\le0\)，函数严格递增，至多一个零点。若 \(b>0\)，函数先递减后递增，在 \(x=b/a\) 处取得最小值。又 \(x\to0^+\) 与 \(x\to+\infty\) 时 \(f(x)\) 均趋 \(+\infty\)，故有两个零点当且仅当
\[
f(b/a)=b\bigl[1-\ln(b/a)\bigr]<0.
\]
因此 \(b/a>e\)，选 A。

% SOLUTION 113 2023 6
\textbf{入手角度}\quad 用 \(u=\ln x\) 把反常积分化为幂函数积分，先确定收敛域，再对参数求导。

\textbf{解析}\quad 换元得 \(\int_{\ln2}^{\infty}u^{-a-1}\,du\)，仅当 \(a>0\) 收敛。此时
\[
f(a)=\frac{(\ln2)^{-a}}a,\qquad
\frac{f'(a)}{f(a)}=-\ln(\ln2)-\frac1a.
\]
因 \(\ln(\ln2)<0\)，导数在 \(a=-1/\ln(\ln2)\) 左侧为负、右侧为正，故该点取得全局最小值。答案为 \(\boxed{a_0=-1/\ln(\ln2)}\)，选 A。



     118 302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2025考研数学二真题.md
# 2025考研数学二真题

[原 PDF](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2025%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf) · 3 页

> 提取文字用于搜索。分式、上下标、矩阵、图表等请以原 PDF 对应页面为准。

## PDF 第 1 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2025%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=1) · 本机 OCR

```text
2025年全国硕士研究生招生考试试题
一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把
所选项前的字母填在题后的括号内）
1+
9=（）
C.--
file+e）
A. x=0是f（x）的极值点，也是g（x）的极值点
B. x=0是f（x）的极值点，（0,0）是曲线y=g（x）的拐点
C.x=0是f（x）的极值点，（0.0）是曲线y=f（x）的拐点
D. （0.0） 是曲线y=f（x）的极值点，也是曲线y=g（x）的拐点
A. （-2，-1］
B.（-∞，-1］
C.（-2,0）
D.（-∞，0）
4.设函数f（）.8（x） 在x=0的某去心邻域内有定义且恒不为零，若当x-0时，f（x）是8（x）的高阶无穷
小，则当 0时（）
A. f（x） +g（x）=0（g（x））
C. f（x） =o（e8（x）-1）
B. f（x）g（x） =o（f（x））
D. f（x）=0（8”（x））
5.设函数f（x,y）连续，则 dx/
•-V-y
f（x,y）dx+|
f（x,y）dx
dy
V4-y
6.设单位质点P.Q 分别位于点（0.0）和（0.1）处，P从点（0.0）出发沿x正向移动，记G为引力常量，则当
B.
D./'G+1
```

## PDF 第 2 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2025%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=2) · 本机 OCR

```text
7.设函数f（x）连续，给出下列四个条件：
① lim
5（） 510存在：②lim
（） 1（01存在：②Ling Lall存在：④ 1im2 1/C）l-1fO1存在；
其中能得到“f（x）在x=0处可导”的条件个数是（）
A. 1
B.2
C.3
D.4
1 20
8.设矩阵
有一个正特征值和两个负特征值，则（）
00b
A.a>4,b>0
B.a<4,b>0
C.a>4,b<0
11 0
9.下列矩阵中，可以经过若干初等行变换得到矩阵001 2的是（）
D.a <4,b<0
10. 设3阶矩阵 A,B满足r（AB）=r（BA）+1，则（）
A. 方程组（A+B）x =0只有零解
B. 方程组 Ax=0与方程组 Bx=0 均只有零解
C. 方程组 Ax=0与方程组 Bx=0没有公共非零解
D. 方程组 ABAx =0与方程组 BABx =0 有公共非零解
二、填空题（本题共6小题，每小题5分，共30分，把答案填在题中横线上）
a
11.设
-dx=In2，则a=
x（2x+a）
12. 曲线y=V 3 3x2+1 的渐近线方程为
13.lim
确定，则尖
21-1
e-vdu=0
15.微分方程（2y-3r）dx+（2x-5y）dy=0满足条件 y（1）=1 的解为
16. 设矩阵A=（01,02,03,Q4），若 c1，02，03线性无关，且 o」 +02 =03+a4，则方程组 Ax=0」 +404的通解
为 =
```

## PDF 第 3 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2025%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=3) · 本机 OCR

```text
三、解答题（本题共6小题，共70分，解答应写出文字说明、证明过程或演算步骤）
17.（本题满分10分）
18.（本题满分12分）
设函数f（x）在x=0处连续，且Lim
xf（x）-e2six+1
19.（本题满分12分）
设函数 f（x,y）可微且满足：
df（x, y）=-2xe-Vdx+e （ y 1）dy,f（0,0）=2
求f（ y），并求 （ ，y）的极值.
20.（本题满分12分）
21.（本题满分12分）
设函数f（x）在区间（a.b）内可导，证明导函数f（x）在（a.b）内严格单调增加的充分必要条件是：对
22.（本题满分12分）
已知矩阵 A =
1 -2
1 1
-2 1
a
与B=
1k00
060
合同.
。。。
3:\documentclass[UTF8,zihao=-4,fontset=fandol]{ctexart}
5:\usepackage[a4paper,margin=17mm]{geometry}
7:\usepackage[paperwidth=800bp,paperheight=600bp,left=52bp,right=52bp,top=42bp,bottom=47bp]{geometry}
9:\usepackage{amsmath,amssymb,xcolor,fancyhdr,enumitem,tikz}
13:\usepackage[hidelinks,bookmarksopen=true]{hyperref}


## tool · 2026-11-10T10:06:02Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:06:22Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"f7dd51","wall_time_seconds":0.000007875,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"e90c19","wall_time_seconds":0.00000725,"exit_code":0,"original_token_count":29,"output":"    1038 .question-bank-work/solutions/001-113.tex\n113\n111\n832:% SOLUTION 094 2023 21\n856:% SOLUTION 095 2024 21\n"}

## tool · 2026-11-10T10:06:29Z


Script completed
Wall time 0.1 seconds
Output:

248:\textbf{解析}\quad
946:\textbf{解析}\quad
7:## PDF 第 1 页
118:## PDF 第 2 页
167:## PDF 第 3 页
191:## PDF 第 4 页


## tool · 2026-11-10T10:06:34Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T10:06:47Z


Script completed
Wall time 0.1 seconds
Output:

{"count":113,"issues":[],"readCode":0,"other":{"chunk_id":"582741","wall_time_seconds":0.000009,"exit_code":0,"original_token_count":427,"output":"## PDF 第 2 页\n\n[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2012%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=2) · 本机 OCR\n\n> 读取原 PDF 时出现警告，建议核对原页。\n\n```text\n二、填空题（本题共6小题，每小题4分，共24分，把答案填在题中横线上.）\n（9）设y=y（x）是由方程x-y+1= e'所确定的隐函数，则\ndx'\n（10） lim n\nn一∞\n十\n22\n+n\n+…•十\n=\nn’+n\n09-14题\nAPP 扫码听课\n（11）设 =f（Inx+\n，其中函数f（u）可微，则x\n+y22\ndx\ndy\n（12）微分方程ydx +（ 3y）dy =0满足条件yx=1=1的解为 =\n（13）曲线 =x+x（x<0）上曲率为\n的点的坐标是\n（14）设A为3阶矩阵，|A|=3，A’为A的伴随矩阵，若交换A的第1行与第2行得矩阵B，则\n|BA*|=\n三、解答题（本题共9小题，共94分，解答应写出文字说明、证明过程或演算步骤.）\n（15）（本题满分10分）\n已知函数f（x）=\n1+X\n，记a = limf（x）.\nsin X\n（I）求a的值；\n（II）若当x一0时，f（x）-a 与x是同阶无穷小量，求常数的值.\n口路送口\n15-17题\nAPP 扫码听课\n（16）（本题满分10分）\n求函数f（x,y）=xe的极值.\n（17）（本题满分12分）\n过点（0，1）作曲线L:y=Inx的切线，切点为A，又L与x轴交于B点，区域D由L与直线AB\n围成.求区域D的面积及D绕x轴旋转一周所得旋转体的体积.\n—2-\n```\n\nmarkers check exit status 0\n"}}

## tool · 2026-11-10T10:06:52Z




## assistant · 2026-11-10T10:06:57Z

已完成第 001–113 题的中文 LaTeX 解析，逐题核对了顺序、年份、原卷题号和 LaTeX 分隔符。 [解析稿](/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/solutions/001-113.tex)

第 007 题按原卷使用 \(n\to\infty\)，第 029 题按单选答案将 A 项理解为小 \(o(g)\)。两处题面差异均已通知主代理。编译留待整合后验证。

## assistant · 2026-11-10T10:07:16Z

我会独立复算这批重点题，并把题面差异与推导错误分开记录。

## tool · 2026-11-10T10:07:19Z


Script completed
Wall time 0.1 seconds
Output:

63:% SOLUTION 244 2020 5
221:% SOLUTION 265 2013 19
260:% SOLUTION 269 2016 17
363:% SOLUTION 281 2012 6
462:% SOLUTION 292 2021 14
514:% SOLUTION 297 2013 17
573:% SOLUTION 303 2019 18
608:% SOLUTION 306 2022 19
641:% SOLUTION 309 2025 20
660:% SOLUTION 311 2009 5
709:% SOLUTION 318 2026 13

3134:\QuestionPage{A.1 多元函数微分学}{选择题}{2020 年第 5 题}{1}{多元极限和偏导数}{244 / 408}
3308:\QuestionPage{A.1 多元函数微分学}{解答题}{2013 年第 19 题}{3}{二元条件最值}{265 / 408}
3337:\QuestionPage{A.1 多元函数微分学}{解答题}{2016 年第 17 题}{2}{隐函数的无条件极值}{269 / 408}
3440:\QuestionPage{A.2 二重积分}{选择题}{2012 年第 6 题}{1}{二重积分与积分区域}{281 / 408}
3549:\QuestionPage{A.2 二重积分}{填空题}{2021 年第 14 题}{2}{二重积分形式的变上限求导}{292 / 408}
3593:\QuestionPage{A.2 二重积分}{解答题}{2013 年第 17 题}{2}{三角形区域上的二重积分}{297 / 408}
3631:\QuestionPage{A.2 二重积分}{解答题}{2019 年第 18 题}{3}{极坐标二重积分}{303 / 408}
3656:\QuestionPage{A.2 二重积分}{解答题}{2022 年第 19 题}{3}{二重积分计算}{306 / 408}
3690:\QuestionPage{A.2 二重积分}{解答题}{2025 年第 20 题}{3}{二重积分计算}{309 / 408}
3706:\QuestionPage{A.3 曲率与曲率圆}{选择题}{2009 年第 5 题}{1}{曲率圆与曲线性态}{311 / 408}
3775:\QuestionPage{A.3 曲率与曲率圆}{填空题}{2026 年第 13 题}{2}{隐式曲线的曲率半径}{318 / 408}


## tool · 2026-11-10T10:07:24Z


Script completed
Wall time 0.1 seconds
Output:

% SOLUTION 244 2020 5
\textbf{入手角度}\quad 坐标轴上的取值与邻近象限不同，逐项用定义检查，尤其要先确认二阶偏导的内层偏导存在。

\textbf{解析}\quad 沿 \(x\) 轴有 \(f(x,0)=x\)，所以 \(f_x(0,0)=1\)。但固定 \(y\ne0\) 时，在 \((0,y)\) 沿 \(x\) 的差商为 \((xy-y)/x\)，极限不存在；同理 \(f_y(x,0)\) 对 \(x\ne0\) 也不存在。因此原点所列混合偏导不存在。无论在哪一段，均有 \(|f(x,y)|\le |x|+|y|+|xy|\)，二元极限为零。固定 \(y\) 后先令 \(x\to0\)，内极限总是零，故累次极限也为零。正确的是第 \(1,3,4\) 项，共 \(3\) 项，选 \(\mathrm B\)。

% SOLUTION 265 2013 19
\textbf{入手角度}\quad 距离与距离平方有相同的最值点。先查两个坐标轴端点，再用约束的对称性化简内部驻点条件。

\textbf{解析}\quad 设 \(G=x^3+y^3-xy\)。写 \(s=x+y\)，由 \(x^3+y^3\ge s^3/4\)、\(xy\le s^2/4\) 知 \(G=1\) 的第一象限部分有界；该集合闭，故最值存在。轴上只有 \((1,0),(0,1)\)。正象限内部，\(\nabla G\) 不为零，因为若 \(3x^2=y,3y^2=x\)，则 \(x=y=1/3\)，不满足 \(G=1\)。拉格朗日条件
\[
2x=\lambda(3x^2-y),\qquad 2y=\lambda(3y^2-x)
\]
消去乘子得到 \((y-x)(3xy+x+y)=0\)，故 \(x=y=t\)。代入得 \(2t^3-t^2-1=(t-1)(2t^2+t+1)=0\)，所以 \(t=1\)。三个候选点距离分别为 \(1,1,\sqrt2\)。因此最短距离为 \(\boxed{1}\)，最长距离为 \(\boxed{\sqrt2}\)。

% SOLUTION 269 2016 17
\textbf{入手角度}\quad 隐方程对 \(z\) 严格单调。用配方找出全局上界，再用驻点条件排除其余局部极值。

\textbf{解析}\quad 记原方程左端为 \(F\)。在 \(z>0\) 上，\(F_z=x^2+y^2+1/z>0\)，故隐函数可微。方程可写为
\[
z\big[(x+1/z)^2+(y+1/z)^2\big]+\ln z+2-2/z=0.
\]
其中 \(h(z)=\ln z+2-2/z\) 严格递增且 \(h(1)=0\)，所以 \(z\le1\)，等号仅在 \(x=y=-1\) 取得。若有其他极值，则其梯度必须为零，从 \(z_x=-F_x/F_z,\ z_y=-F_y/F_z\) 得 \(x=y=-1/z\)，再代回知 \(h(z)=0\)，仍为上述点。因此唯一极值是极大值 \(\boxed{z(-1,-1)=1}\)。

% SOLUTION 281 2012 6
\textbf{入手角度}\quad 整个区域对 \(x\) 的截面不是关于 \(y\) 轴对称的。先积分掉 \(y\)，再检查所得关于 \(x\) 的奇偶性。

\textbf{解析}\quad 固定 \(x\)，纵向范围为 \(\sin x\le y\le1\)。于是
\[
\iint_D (x^5y-1)\,\mathrm dx\,\mathrm dy
=\int_{-\pi/2}^{\pi/2}\left[\tfrac12x^5(1-\sin^2x)-1+\sin x\right]\mathrm dx.
\]
第一项及末项均为奇函数，积分为零；常数项给出 \(-\pi\)。选 \(\mathrm D\)。

% SOLUTION 292 2021 14
\textbf{入手角度}\quad \(\sin(x/y)\) 关于 \(x\) 容易积分。先换成 \(y\) 为外层变量，再对变上限求导。

\textbf{解析}\quad 在 \(t=\pi/2\) 附近有 \(t>1\)。原区域 \(1\le x\le t^2,\ \sqrt x\le y\le t\) 等价于 \(1\le y\le t,\ 1\le x\le y^2\)。故
\[
f(t)=\int_1^t\mathrm dy\int_1^{y^2}\sin(x/y)\,\mathrm dx
=\int_1^t \big[-y\cos y+y\cos(1/y)\big]\,\mathrm dy.
\]
由微积分基本定理，\(f'(t)=-t\cos t+t\cos(1/t)\)，因此 \(\boxed{f'(\pi/2)=\frac{\pi}{2}\cos\frac{2}{\pi}}\)。

% SOLUTION 297 2013 17
\textbf{入手角度}\quad 一条边使 \(x+y\) 固定，另两条边使 \(x/(x+y)\) 固定。用这两个量作坐标可把三角形变成矩形。

\textbf{解析}\quad 令 \(u=x+y,\ v=x/(x+y)\)，则 \(x=uv,\ y=u(1-v)\)，Jacobian 绝对值为 \(u\)。除去原点这一零面积集合，区域化为 \(0<u\le8,\ 1/4\le v\le3/4\)。因此
\[
I=\int_0^8u^3\,\mathrm du\int_{1/4}^{3/4}v^2\,\mathrm dv
=1024\cdot\frac{26}{192}
=\boxed{\frac{416}{3}}.
\]

% SOLUTION 303 2019 18
\textbf{入手角度}\quad \(|x|\le y\) 给出一个扇角，另外的齐次不等式化为径向上限。先利用关于 \(y\) 轴的对称性消去 \(x\) 项。

\textbf{解析}\quad 极角范围为 \(\pi/4\le\theta\le3\pi/4\)。由 \(r^6\le r^4\sin^4\theta\)，得 \(0\le r\le\sin^2\theta\)。\(x/\sqrt{x^2+y^2}\) 为关于 \(x\) 的奇函数，故只保留 \(\sin\theta\) 项：
\[
\begin{aligned}
I&=\frac12\int_{\pi/4}^{3\pi/4}\sin^5\theta\,\mathrm d\theta
=\int_{\pi/4}^{\pi/2}\sin^5\theta\,\mathrm d\theta\\
 &=\int_0^{1/\sqrt2}(1-s^2)^2\,\mathrm ds
=\boxed{\frac{43\sqrt2}{120}}.
\end{aligned}
\]
其中最后一步取 \(s=\cos\theta\)。

% SOLUTION 306 2022 19
\textbf{入手角度}\quad 以 \(y\) 轴分块：右侧是四分之一圆，左侧是三角形。两块分别换成极坐标，左侧可把被积函数与径向上限中的同一因子消去。

\textbf{解析}\quad 右侧 \(x,y\ge0,\ x^2+y^2\le4\)，被积函数为 \(1-\sin2\theta\)，故
\[
I_{\rm 右}=\int_0^{\pi/2}(1-\sin2\theta)\,\mathrm d\theta\int_0^2 r\,\mathrm dr
=\pi-2.
\]
左侧令 \(u=-x,\ v=y\)，有 \(u,v\ge0,\ u+v\le2\)。再写 \(u=r\cos\theta,\ v=r\sin\theta\)，被积函数为 \((\cos\theta+\sin\theta)^2\)，半径上限为 \(2/(\cos\theta+\sin\theta)\)。先积 \(r\) 后角向被积函数为常数 \(2\)，所以 \(I_{\rm 左}=\pi\)。总积分为 \(\boxed{2\pi-2}\)。

% SOLUTION 309 2025 20
\textbf{入手角度}\quad 两圆盘的交域及被积函数均关于 \(y=x\) 对称。只算极角从 \(0\) 到 \(\pi/4\) 的一半即可避免分段。

\textbf{解析}\quad 极坐标下 \(0\le r\le4\min(\cos\theta,\sin\theta)\)，该半区的径向上限为 \(4\sin\theta\)。先积 \(r\)，得
\[
I=128\int_0^{\pi/4}\sin^4\theta(1-\sin2\theta)\,\mathrm d\theta.
\]
由降幂公式 \(\sin^4\theta=(3-4\cos2\theta+\cos4\theta)/8\)，第一项积分为 \(3\pi/32-1/4\)。第二项用 \(\sin2\theta=2\sin\theta\cos\theta\)，积分为 \([\sin^6\theta/3]_0^{\pi/4}=1/24\)。所以 \(I=\boxed{12\pi-112/3}\)。

% SOLUTION 311 2009 5
\textbf{入手角度}\quad 曲率圆同时给出切线和弯曲方向。用这两条信息控制曲线在 \(x=1\) 右侧的位置。

\textbf{解析}\quad 圆心在原点，点 \((1,1)\) 的半径方向为 \((1,1)\)，所以切线斜率 \(f'(1)=-1\)。圆心位于切点的下侧，曲率非零，故 \(f''(1)<0\)。二阶导不变号，因而 \(f'\) 非增，\(x>1\) 时 \(f'(x)\le-1\)，函数严格下降，没有极值点。又由 \(f''(1)<0\)，充分靠近 \(1\) 的右侧有 \(f'(x)<-1\)，所以到 \(x=2\) 时 \(f(2)<f(1)-1=0\)。由连续性和严格单调性，在 \((1,2)\) 中恰有一处零点。选 \(\mathrm B\)。

% SOLUTION 318 2026 13
\textbf{入手角度}\quad 在目标点，隐方程对 \(y\) 的偏导非零，可局部写成 \(y(x)\)，再用普通曲率半径公式。

\textbf{解析}\quad 记 \(F=x^2+2\sqrt3xy+y^2-1\)。在 \((0,1)\)，\(F_y=2\)，故
\[
y'=-F_x/F_y=-\sqrt3,\qquad
y''=-\frac{F_{xx}+2F_{xy}y'+F_{yy}(y')^2}{F_y}=2.
\]
于是 \(\rho=(1+(y')^2)^{3/2}/|y''|=4^{3/2}/2=\boxed{4}\)。


\QuestionPage{A.1 多元函数微分学}{选择题}{2020 年第 5 题}{1}{多元极限和偏导数}{244 / 408}
关于函数
\[f(x,y)=
\begin{cases}
xy, & xy\ne 0,\\
x, & y=0,\\
y, & x=0,
\end{cases}
\]
给出下列结论：
\begin{enumerate}
\item \(\left.\dfrac{\partial f}{\partial x}\right|_{(0,0)}=1\)
\item \(\left.\dfrac{\partial^2 f}{\partial x\partial y}\right|_{(0,0)}=1\)
\item \(\lim\limits_{(x,y)\to(0,0)}f(x,y)=0\)
\item \(\lim\limits_{y\to0}\lim\limits_{x\to0}f(x,y)=0\)
\end{enumerate}
其中正确的个数为
\fourchoices{\(4\)}{\(3\)}{\(2\)}{\(1\)}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2013 年第 19 题}{3}{二元条件最值}{265 / 408}
求曲线$x^3 - xy + y^3 = 1$（$x \ge 0$，$y \ge 0$）上的点到坐标原点的最长距离与最短距离．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2016 年第 17 题}{2}{隐函数的无条件极值}{269 / 408}
已知函数$z = z(x,y)$由方程$(x^2 + y^2)z + \ln z + 2(x + y + 1) = 0$确定，求$z = z(x,y)$的极值．
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2012 年第 6 题}{1}{二重积分与积分区域}{281 / 408}
设区域D由曲线$y = \sin x,x = \pm \frac{\pi}{2},y = 1$围成，则$\iint_D (x^5 y - 1)\,\mathrm{d} x\,\mathrm{d} y =$\pickout{}
\begin{abcd}
\item $\pi$．
\item $2$．
\item $- 2$．
\item $- \pi$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.2 二重积分}{填空题}{2021 年第 14 题}{2}{二重积分形式的变上限求导}{292 / 408}
已知函数
\[f(t)=\int_{1}^{t} \mathrm{d}x \int_{\sqrt{x}}^{1} \sin \frac{x}{y}\,\mathrm{d}y,
\]
则
\[f'\left(\frac{\pi}{2}\right)= \blank{}
\]
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2013 年第 17 题}{2}{三角形区域上的二重积分}{297 / 408}
设平面内区域$D$由直线$x = 3y,y = 3x$及$x + y = 8$围成，计算$\iint_D x^2 \,\mathrm{d} x\,\mathrm{d} y$．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2019 年第 18 题}{3}{极坐标二重积分}{303 / 408}
设平面区域$D = \left\{(x,y)\middle||x| \le y, (x^2 + y^2)^3 \le y^4\right\}$，
计算二重积分\[
\iint_D \frac{x + y}{\sqrt{x^2 + y^2}}\,\mathrm{d} x\,\mathrm{d} y.
\]
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2022 年第 19 题}{3}{二重积分计算}{306 / 408}
已知平面区域
\(D = \left\{ \left( x,y \right) \mid y - 2 \le x \le \sqrt{4 - y^{2}},\ 0 \le y \le 2 \right\}\)
计算
\(I = \iint_{D} \frac{\left( x-y \right)^{2}}{x^{2} + y^{2}} \mathrm{~d}x \mathrm{~d}y\)
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2025 年第 20 题}{3}{二重积分计算}{309 / 408}
（本题满分 12 分）
已知平面有界区域 \(D = \left\{ \left( x, y \right) \mid x^{2} + y^{2} \le 4x,\ x^{2} + y^{2} \le 4y \right\}\)，计算 \(\iint_{D} \left( x - y \right)^{2} \mathrm{d} x \mathrm{d} y\).
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2009 年第 5 题}{1}{曲率圆与曲线性态}{311 / 408}
若$f''(x)$不变号，且曲线$y = f(x)$在点$\left(1,1 \right)$上的曲率圆为$x^2 + y^2 = 2$，则$f(x)$在区间$\left(1,2 \right)$内\pickout{}
\begin{abcd}
\item 有极值点，无零点．
\item 无极值点，有零点．
\item 有极值点，有零点．
\item 无极值点，无零点．
\end{abcd}
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2026 年第 13 题}{2}{隐式曲线的曲率半径}{318 / 408}
曲线
\[x^2+2\sqrt3xy+y^2=1
\]
在点 \((0,1)\) 处的曲率半径为 \blank{}.
\QuestionEnd


## tool · 2026-11-10T10:07:38Z


Script completed
Wall time 0.1 seconds
Output:

302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:363:13. 曲线x’+2V3r+y’=1在点（0.1）处的曲率半径为_
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-364-13.【答案】4
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md:371:，故曲率半径为R=！
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2026考研数学（二）真题试卷及解析.md-376-14.【答案】-2元
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md:321:g（x）这两条曲线均为半径为1的半圆弧（圆弧上各点的曲率半径均为1）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2009数二真题【解析】.md:357:5 若 ”"（x）不变号，且曲线y=f（x）在点（1，1）处的曲率圆为 ’＋ 2，则函数 （x）在区
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2009数二真题【解析】.md-363-（答案！
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2009数二真题【解析】.md:377:（1，1）处的曲率圆的凹凸性一致，而曲率圆为 ＋g =2，是凸曲线，故
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2009数二真题【解析】.md-390-因此，f（x）在（1，2）上有零点，没有极值点.应选B.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md:32:（19） 最长距离、/2，最短距离1.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md:1114:如图，区域D为坐标系x0y 下第一象限中的一个三角形区域，我们可以通过对其作变
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md:1201:求曲线x’-xy +y’=1（x≥0,y≥0）上的点到坐标原点的最长距离和最短距离.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md:1242:综上所述，最长距离力、2，最短距离为1.

\QuestionPage{A.1 多元函数微分学}{选择题}{2009 年第 3 题}{1}{二元函数极值}{235 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2010 年第 5 题}{1}{隐函数偏导数}{236 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2011 年第 5 题}{1}{二元函数的极小值}{237 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2012 年第 5 题}{1}{偏导数符号与函数值比较}{238 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2013 年第 5 题}{1}{复合函数的偏导数}{239 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2014 年第 6 题}{1}{多元函数的最值位置}{240 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2015 年第 5 题}{1}{复合函数的偏导数}{241 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2016 年第 6 题}{1}{二元函数在原点的性质}{242 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2017 年第 5 题}{1}{偏导数与函数值比较}{243 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2020 年第 5 题}{1}{多元极限和偏导数}{244 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2021 年第 6 题}{1}{由复合函数条件求全微分}{245 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2022 年第 4 题}{1}{含变上限积分的偏导数}{246 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2024 年第 5 题}{1}{偏导数与可微性}{247 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2025 年第 1 题}{1}{隐函数偏导数}{248 / 408}
\QuestionPage{A.1 多元函数微分学}{选择题}{2026 年第 3 题}{1}{隐函数偏导数}{249 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2012 年第 11 题}{2}{复合函数求偏导}{250 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2014 年第 11 题}{2}{隐函数的全微分}{251 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2015 年第 13 题}{2}{隐函数的全微分}{252 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2017 年第 12 题}{2}{由全微分恢复二元函数}{253 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2018 年第 13 题}{2}{隐函数的偏导数}{254 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2019 年第 11 题}{2}{复合函数偏导数}{255 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2020 年第 11 题}{2}{二元函数的全微分}{256 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2021 年第 13 题}{2}{隐函数偏导数}{257 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2023 年第 13 题}{2}{隐函数偏导数}{258 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2024 年第 12 题}{2}{二元函数极值}{259 / 408}
\QuestionPage{A.1 多元函数微分学}{填空题}{2026 年第 14 题}{2}{全微分与复合求导}{260 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2009 年第 17 题}{3}{二阶偏导数}{261 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2010 年第 19 题}{3}{二阶偏导数与变量变换}{262 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2011 年第 17 题}{2}{复合函数的偏导数}{263 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2012 年第 16 题}{2}{二元函数极值}{264 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2013 年第 19 题}{3}{二元条件最值}{265 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2014 年第 18 题}{3}{复合函数偏导与方程变换}{266 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2014 年第 21 题}{4}{由偏导数恢复边界与旋转体积}{267 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2015 年第 17 题}{2}{二元函数极值}{268 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2016 年第 17 题}{2}{隐函数的无条件极值}{269 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2017 年第 16 题}{2}{复合函数的二阶偏导}{270 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2018 年第 19 题}{3}{多元约束最值}{271 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2019 年第 20 题}{3}{偏导数与方程变换}{272 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2020 年第 17 题}{3}{二元函数极值}{273 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2022 年第 20 题}{3}{由偏导数恢复二元函数及其极值}{274 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2023 年第 18 题}{3}{二元函数极值}{275 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2024 年第 20 题}{3}{偏导数与原函数}{276 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2025 年第 19 题}{3}{利用全微分求函数及极值}{277 / 408}
\QuestionPage{A.1 多元函数微分学}{解答题}{2026 年第 19 题}{2}{二元函数极值}{278 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2009 年第 4 题}{1}{交换积分次序}{279 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2010 年第 6 题}{1}{二重积分换序}{280 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2012 年第 6 题}{1}{二重积分与积分区域}{281 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2013 年第 6 题}{1}{象限区域上的二重积分符号}{282 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2015 年第 6 题}{1}{极坐标下的积分限}{283 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2018 年第 6 题}{1}{二重积分的次序变换}{284 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2019 年第 5 题}{1}{二重积分与积分区域}{285 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2022 年第 2 题}{1}{二重积分换序与换元}{286 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2024 年第 6 题}{1}{二重积分换序}{287 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2025 年第 5 题}{1}{二重积分交换次序}{288 / 408}
\QuestionPage{A.2 二重积分}{选择题}{2026 年第 7 题}{1}{二重积分定义与对称性}{289 / 408}
\QuestionPage{A.2 二重积分}{填空题}{2011 年第 13 题}{2}{极坐标二重积分}{290 / 408}
\QuestionPage{A.2 二重积分}{填空题}{2020 年第 10 题}{2}{二重积分交换次序}{291 / 408}
\QuestionPage{A.2 二重积分}{填空题}{2021 年第 14 题}{2}{二重积分形式的变上限求导}{292 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2009 年第 19 题}{3}{区域对称与二重积分}{293 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2010 年第 20 题}{3}{二重积分计算}{294 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2011 年第 21 题}{4}{含偏导数的二重积分}{295 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2012 年第 18 题}{3}{心形线区域上的二重积分}{296 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2013 年第 17 题}{2}{三角形区域上的二重积分}{297 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2014 年第 17 题}{2}{环形区域上的二重积分}{298 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2015 年第 18 题}{3}{二重积分计算}{299 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2016 年第 18 题}{3}{二重积分计算}{300 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2017 年第 20 题}{3}{二重积分计算}{301 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2018 年第 17 题}{3}{参数曲线围成区域上的积分}{302 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2019 年第 18 题}{3}{极坐标二重积分}{303 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2020 年第 19 题}{3}{二重积分计算}{304 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2021 年第 21 题}{4}{极坐标二重积分}{305 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2022 年第 19 题}{3}{二重积分计算}{306 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2023 年第 20 题}{4}{二重积分的变量代换}{307 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2024 年第 17 题}{2}{二重积分计算}{308 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2025 年第 20 题}{3}{二重积分计算}{309 / 408}
\QuestionPage{A.2 二重积分}{解答题}{2026 年第 17 题}{2}{二重积分计算}{310 / 408}
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2009 年第 5 题}{1}{曲率圆与曲线性态}{311 / 408}
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2014 年第 4 题}{1}{参数曲线的曲率半径}{312 / 408}
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2016 年第 5 题}{1}{曲率、公切线与曲线位置}{313 / 408}
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2019 年第 6 题}{1}{相切、曲率与二阶展开}{314 / 408}
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2012 年第 13 题}{2}{曲率与点的坐标}{315 / 408}
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2018 年第 12 题}{2}{参数曲线的曲率}{316 / 408}
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2024 年第 11 题}{2}{曲率圆方程}{317 / 408}
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2026 年第 13 题}{2}{隐式曲线的曲率半径}{318 / 408}
686:\textbf{入手角度}\quad 用差函数的二阶展开解释极限；检查逆命题时注意曲率公式中二阶导有绝对值。


## tool · 2026-11-10T10:07:43Z




## tool · 2026-11-10T10:07:51Z


Script completed
Wall time 0.1 seconds
Output:

% SOLUTION 247 2024 5
\textbf{入手角度}\quad 可微性考察函数本身的量级，偏导连续性则要检查求导后从振荡项产生的因子。

\textbf{解析}\quad 两条坐标轴上的函数值为零，原点两个偏导均为零。且 \(|f(x,y)|\le x^2+y^2\)，故 \(f(x,y)/\sqrt{x^2+y^2}\to0\)，从定义得原点可微。轴外有
\[
f_x=2x\sin(1/(xy))-\frac{x^2+y^2}{x^2y}\cos(1/(xy)).
\]
取 \(x=y=(2k\pi)^{-1/2}\)，有 \(f_x=-2/x\to-\infty\)，所以 \(f_x\) 在原点不连续。选 \(\mathrm C\)。

% SOLUTION 248 2025 1
\textbf{入手角度}\quad 积分上下限各依赖一个变量，分别求偏导即可看清两项的符号。

\textbf{解析}\quad 由 \(z+\ln z=\int_y^x e^{-t^2}\,\mathrm dt\)，得
\[
(1+1/z)z_x=e^{-x^2},\qquad (1+1/z)z_y=-e^{-y^2}.
\]
这里 \(z>0\)，系数非零。相加后除以它，得 \(z_x+z_y=\frac{z}{z+1}(e^{-x^2}-e^{-y^2})\)。选 \(\mathrm A\)。

% SOLUTION 249 2026 3
\textbf{入手角度}\quad 两个偏导有同一个隐函数分母，作差可以把分子凑成该分母中的因子。

\textbf{解析}\quad 记 \(E=e^{y+az}>0\)。对 \(x\)、\(y\) 分别求偏导得 \(1-az_x=aEz_x\)、\(-az_y=E(1+az_y)\)，故
\[
z_x=\frac{1}{a(1+E)},\qquad z_y=-\frac{E}{a(1+E)}.
\]
由于 \(a\ne0\)，可得 \(z_x-z_y=1/a\)，选 \(\mathrm A\)。

% SOLUTION 253 2017 12
\textbf{入手角度}\quad 先从 \(\mathrm dx\) 的系数积分，积分常数可以依赖 \(y\)，用另一个偏导确定它。

\textbf{解析}\quad \(f_x=ye^y\) 给出 \(f=xye^y+h(y)\)。对此式求 \(y\) 偏导得 \(x(1+y)e^y+h'(y)\)，与题给系数比较知 \(h'=0\)。由 \(f(0,0)=0\) 得常数为零，故 \(\boxed{f(x,y)=xye^y}\)。

% SOLUTION 254 2018 13
\textbf{入手角度}\quad 目标点满足 \(xy=1\)，用左端在 \(z>0\) 上的单调性识别 \(z\) 的点值。

\textbf{解析}\quad \(\ln z+e^{z-1}\) 严格递增，且 \(z=1\) 时值为 \(1\)，因此该点 \(z=1\)。固定 \(y\) 求导得 \((1/z+e^{z-1})z_x=y\)。代入 \(z=1,\ y=1/2\) 得 \(\boxed{z_x=1/4}\)。

% SOLUTION 258 2023 13
\textbf{入手角度}\quad 二阶隐函数求导需要一阶偏导，分两次求导，并在每一步算出目标点值。

\textbf{解析}\quad 在 \((1,1)\)，\(e^z+z=1\) 的唯一解是 \(z=0\)。固定 \(y\)，第一次求导得 \((e^z+x)z_x+z=2\)，所以该点 \(z_x=1\)。再次求导得
\[
(e^z+x)z_{xx}+e^z z_x^2+2z_x=0.
\]
代入点值，解得 \(\boxed{z_{xx}=-3/2}\)。

% SOLUTION 260 2026 14
\textbf{入手角度}\quad 全微分的系数已经给出梯度，只需计算内层曲线在 \(x=1\) 的切向量。

\textbf{解析}\quad \(x=1\) 时 \((\ln x,\sin\pi x)=(0,0)\)，其导数为 \((1,-\pi)\)。由全微分可知 \(f_x(0,0)=\pi,\ f_y(0,0)=3\)，故链式法则给出 \(g'(1)=\pi\cdot1+3(-\pi)=\boxed{-2\pi}\)。


% SOLUTION 261 2009 17
\textbf{入手角度}\quad 把三个内层量编号，先求它们的全微分，再对一阶偏导应用一次链式法则。

\textbf{解析}\quad 令 \(u=(x+y,x-y,xy)\)，以下 \(f_i,f_{ij}\) 均在 \(u\) 取值。由于三个内层的微分依次为 \(\mathrm dx+\mathrm dy\)、\(\mathrm dx-\mathrm dy\)、\(y\,\mathrm dx+x\,\mathrm dy\)，有
\[
\mathrm dz=(f_1+f_2+yf_3)\,\mathrm dx+(f_1-f_2+xf_3)\,\mathrm dy.
\]
将第一个系数关于 \(y\) 求导，用 \(u_y=(1,-1,x)\)。由 \(f_{ij}=f_{ji}\) 合并得
\[
z_{xy}=f_{11}-f_{22}+(x+y)f_{13}+(x-y)f_{23}+xyf_{33}+f_3.
\]

% SOLUTION 262 2010 19
\textbf{入手角度}\quad 希望只剩混合项，应让 \(\partial_{\xi\xi}\) 和 \(\partial_{\eta\eta}\) 的系数分别为零。

\textbf{解析}\quad 记 \(U(\xi,\eta)=u(x,y)\)。则 \(\partial_x=\partial_\xi+\partial_\eta\)，\(\partial_y=a\partial_\xi+b\partial_\eta\)。代入，两个纯二阶项的系数分别为 \(4+12a+5a^2\) 和 \(4+12b+5b^2\)，混合项系数为 \(8+12(a+b)+10ab\)。前两式同为零，因 \(5t^2+12t+4=(5t+2)(t+2)\)，有 \(t=-2/5\) 或 \(-2\)。变换的 Jacobian 为 \(b-a\)，须取不同的根，故 \(\boxed{\{a,b\}=\{-2/5,-2\}}\)。混合项系数为 \(-64/5\ne0\)，确实化为 \(U_{\xi\eta}=0\)。

% SOLUTION 266 2014 18
\textbf{入手角度}\quad 复合函数的 Laplace 算子分成 \(f''|\nabla u|^2\) 与 \(f'\Delta u\) 两项，先算内层 \(u=e^x\cos y\)。

\textbf{解析}\quad 有 \(u_x=e^x\cos y,\ u_y=-e^x\sin y\)，因此 \(u_x^2+u_y^2=e^{2x}\)，且 \(u_{xx}+u_{yy}=0\)。故题给方程等价于 \(f''-4f=u\)。齐次解可写成 \(A\cosh(2u)+B\sinh(2u)\)，取特解 \(-u/4\)。由 \(f(0)=0\) 得 \(A=0\)，由 \(f'(0)=0\) 得 \(2B-1/4=0\)。所求为 \(\boxed{f(u)=\tfrac18\sinh(2u)-\tfrac14u}\)。

% SOLUTION 267 2014 21
\textbf{入手角度}\quad 先从 \(f_y\) 恢复曲线方程。旋转轴恰为 \(y=-1\)，用垂直于轴的圆盘截面。

\textbf{解析}\quad \(f_y=2(y+1)\) 给出 \(f=(y+1)^2+h(x)\)。由对角线条件得 \(h(x)=-(2-x)\ln x\)。故边界满足 \((y+1)^2=(2-x)\ln x\)。右端在定义域 \(x>0\) 内非负当且仅当 \(1\le x\le2\)，此时上下两支绕 \(y=-1\) 对称。截面半径平方为 \((2-x)\ln x\)，所以
\[
\begin{aligned}
V&=\pi\int_1^2(2-x)\ln x\,\mathrm dx\\
 &=\pi\left[(2x-x^2/2)\ln x-2x+x^2/4\right]_1^2\\
 &=\boxed{\pi(2\ln2-5/4)}.
\end{aligned}
\]

% SOLUTION 270 2017 16
\textbf{入手角度}\quad 把内层视为平面曲线。二阶导数既有 Hessian 与曲线切向量的乘积，也有梯度与曲线二阶导数的乘积。

\textbf{解析}\quad 设 \(u=e^x,v=\cos x\)。在 \(x=0\)，有 \((u,v)=(1,1)\)，\((u',v')=(1,0)\)，\((u'',v'')=(1,-1)\)。链式法则给出
\[
y'=f_u u'+f_vv',\qquad
y''=f_{uu}(u')^2+2f_{uv}u'v'+f_{vv}(v')^2+f_u u''+f_vv''.
\]
代入即得 \(\boxed{y'(0)=f_u(1,1)}\)，\(\boxed{y''(0)=(f_{uu}+f_u-f_v)(1,1)}\)。

% SOLUTION 271 2018 19
\textbf{入手角度}\quad 用周长表示各面积后，目标变成周长和固定的加权平方和，可用带权柯西不等式找最小值。

\textbf{解析}\quad 设三个周长依次为 \(a,b,c>0\)，有 \(a+b+c=2\)。面积和为
\[
S=\frac{a^2}{4\pi}+\frac{b^2}{16}+\frac{c^2}{12\sqrt3}.
\]
由柯西不等式，\(4=(a+b+c)^2\le S(4\pi+16+12\sqrt3)\)。等号条件是 \(a:b:c=4\pi:16:12\sqrt3\)，这三个周长可同时取正并满足总长度。因此存在最小值 \(\boxed{1/(\pi+4+3\sqrt3)\,\mathrm m^2}\)。

% SOLUTION 272 2019 20
\textbf{入手角度}\quad 指数因子的作用是把求导算子变为 \(\partial_x+a\)、\(\partial_y+b\)，只需让两种一阶项的系数消失。

\textbf{解析}\quad 代入 \(u=e^{ax+by}v\) 后除以指数因子，原式变为
\[
\begin{aligned}
2v_{xx}-2v_{yy}+(4a+3)v_x+(3-4b)v_y\\
 +\big[2a^2-2b^2+3(a+b)\big]v=0.
\end{aligned}
\]
由 \(4a+3=3-4b=0\) 得 \(\boxed{a=-3/4,\ b=3/4}\)。此时零阶项系数也为零，故化简为 \(v_{xx}-v_{yy}=0\)。

% SOLUTION 274 2022 20
\textbf{入手角度}\quad 题给偏导之差正是 \(g_x\)，所以先固定 \(y\) 积分；边界 \(v=0\) 在新坐标下是 \(x=y\)。

\textbf{解析}\quad （I）链式法则给出 \(g_x=f_u-f_v\)，在 \(u=x,v=y-x\) 代入，得 \(\boxed{g_x=2(2x-y)e^{-y}}\)。

（II）积分得 \(g(x,y)=(2x^2-2xy)e^{-y}+h(y)\)。由 \(g(y,y)=f(y,0)=y^2e^{-y}\) 得 \(h(y)=y^2e^{-y}\)。换回变量，\(\boxed{f(u,v)=(u^2+v^2)e^{-(u+v)}}\)。

记 \(Q=u^2+v^2\)。驻点要求 \(2u=Q=2v\)，故只有 \((0,0),(1,1)\)。原点函数值为零、其余点函数值均正，故在原点取得极小值 \(0\)。在 \((1,1)\) 的 Hessian 对角元为零，非对角元为 \(-2e^{-2}\)，行列式为负，是鞍点。没有极大值。

% SOLUTION 276 2024 20
\textbf{入手角度}\quad 二阶算子可拆成两个一阶算子，换元后一个只含 \(u\) 导数，另一个只含 \(v\) 导数。

\textbf{解析}\quad （1）因 \(f\) 具有二阶连续偏导，原式左边等于 \((\partial_x+3\partial_y)(\partial_x-2\partial_y)g\)。由 \(\partial_x=2\partial_u+3\partial_v,\ \partial_y=\partial_u-\partial_v\)，两因子分别等于 \(5\partial_u,5\partial_v\)。因此 \(\boxed{f_{uv}=1/25}\)。

（2）积分得 \(f(u,v)=uv/25+A(u)+B(v)\)。题设给 \(A'(u)=ue^{-u}\)，可取 \(A(u)=-(u+1)e^{-u}\)，积分常数并入 \(B\)。由 \(f(0,v)=v^2/50-1\) 得 \(B(v)=v^2/50\)。所以
\[
\boxed{f(u,v)=\frac{uv}{25}-(u+1)e^{-u}+\frac{v^2}{50}}.
\]

% SOLUTION 277 2025 19
\textbf{入手角度}\quad 从全微分读出 \(f_x,f_y\)。函数恢复后，先固定 \(y\) 利用 \(x^2\) 项的符号，再作一元最值判断。

\textbf{解析}\quad 对 \(f_x=-2xe^{-y}\) 积分得 \(f=-x^2e^{-y}+h(y)\)。与给定 \(f_y\) 比较得 \(h'=-(y+1)e^{-y}\)，故 \(h=(y+2)e^{-y}+C\)。由 \(f(0,0)=2\) 得 \(C=0\)，即 \(\boxed{f=(y+2-x^2)e^{-y}}\)。

由 \(f_x=0\) 得 \(x=0\)，再由 \(f_y=0\) 得 \(y=-1\)，故驻点唯一。对任意 \(x,y\)，\(f\le (y+2)e^{-y}\)，等号当且仅当 \(x=0\)。该上界在 \(y<-1\) 递增、在 \(y>-1\) 递减，因此唯一极值为极大值 \(\boxed{f(0,-1)=e}\)。

% SOLUTION 278 2026 19
\textbf{入手角度}\quad 因为 \(f_y\) 含单独的因子 \(y\)，驻点先限制在 \(x\) 轴，再判断两个坐标方向的二阶变化。

\textbf{解析}\quad 有 \(f_x=e^x(2x^2+4x-y^2)\)，\(f_y=-2ye^x\)。驻点为 \((0,0)\)、\((-2,0)\)。在驻点有 \(f_{xy}=0,\ f_{xx}=e^x(4x+4),\ f_{yy}=-2e^x\)。原点二阶型不定，是鞍点；\((-2,0)\) 处二阶型负定，为极大值点。唯一极值是 \(\boxed{f(-2,0)=8e^{-2}}\)。

% SOLUTION 289 2026 7
\textbf{入手角度}\quad 条件 \(f(x,y)=f(y,x)\) 是关于 \(y=x\) 的对称性。检查求和的下标是否覆盖由这条对角线切出的三角形，以及每格的面积。

\textbf{解析}\quad 取下三角形 \(T=\{0\le y\le x\le1\}\)，有 \(\iint_D f=2\iint_T f\)。将正方形均分成边长 \(1/(2n)\) 的小方格，则
\[
\iint_D f=2\lim_{n\to\infty}\sum_{i=1}^{2n}\sum_{j=1}^{i}
f\!\left(\frac{i}{2n},\frac{j}{2n}\right)\frac1{4n^2}.
\]
对角线边缘至多相差 \(O(n)\) 个小格，连续性保证误差趋于零。把系数写成 \(\tfrac12\cdot 1/n^2\) 即为选项 \(\mathrm D\)。选项 \(\mathrm A\) 的三角形由 \(x+y=1\) 划分，该对称性并未给出。

% SOLUTION 290 2011 13
\textbf{入手角度}\quad 两条直线经过原点，圆也经过原点，极坐标可把三条边界分别写成两个固定角度与一个径向上限。

\textbf{解析}\quad 由圆方程得 \(0\le r\le2\sin\theta\)。\(y=x\) 和 \(y\) 轴之间的有界扇形部分给出 \(\pi/4\le\theta\le\pi/2\)。故
\[
\begin{aligned}
\iint_D xy\,\mathrm d\sigma
 &=\int_{\pi/4}^{\pi/2}\!\cos\theta\sin\theta\,\mathrm d\theta
   \int_0^{2\sin\theta}r^3\,\mathrm dr\\
 &=4\int_{\pi/4}^{\pi/2}\sin^5\theta\cos\theta\,\mathrm d\theta
 =\boxed{\frac7{12}}.
\end{aligned}
\]

% SOLUTION 293 2009 19
\textbf{入手角度}\quad 半圆的直径沿 \(y=x\)，而被积函数 \(x-y\) 正比于到直径的有向距离。平移并旋转坐标，半圆即可水平切片。

\textbf{解析}\quad 令 \(u=(x+y-2)/\sqrt2\)、\(v=(y-x)/\sqrt2\)，面积元不变。区域变为 \(u^2+v^2\le2,\ v\ge0\)，被积函数为 \(-\sqrt2\,v\)。固定 \(v\) 的截线长为 \(2\sqrt{2-v^2}\)，于是
\[
I=-2\sqrt2\int_0^{\sqrt2}v\sqrt{2-v^2}\,\mathrm dv
=-\frac{2\sqrt2}{3}\,2^{3/2}
=\boxed{-\frac83}.
\]

% SOLUTION 294 2010 20
\textbf{入手角度}\quad \(r\le\sec\theta\) 是 \(x\le1\)，而 \(r^2\cos 2\theta=x^2-y^2\)。转成直角坐标后，分子恰好提供根号内表达式关于 \(y\) 的导数。

\textbf{解析}\quad 令 \(x=r\cos\theta,\ y=r\sin\theta\)。由于 \(r^2\sin\theta\,\mathrm dr\,\mathrm d\theta=y\,\mathrm dx\,\mathrm dy\)，区域变成 \(0\le y\le x\le1\)，故
\[
\begin{aligned}
I &= \int_0^1\mathrm dx\int_0^x y\sqrt{1-x^2+y^2}\,\mathrm dy\\
  &=\frac13\int_0^1\big[1-(1-x^2)^{3/2}\big]\,\mathrm dx .
\end{aligned}
\]
令 \(x=\sin t\)，余项积分为 \(\int_0^{\pi/2}\cos^4t\,\mathrm dt=3\pi/16\)，所以 \(I=\boxed{1/3-\pi/16}\)。

% SOLUTION 295 2011 21
\textbf{入手角度}\quad \(xy\) 是两个一次因子的乘积，逐变量分部积分各降一阶；题给边界值正好消去端点项。

\textbf{解析}\quad 由 \(f(1,y)=0\) 得 \(f_y(1,y)=0\)，因此
\[
\int_0^1 x f_{xy}(x,y)\,\mathrm dx
=[x f_y(x,y)]_0^1-\int_0^1 f_y(x,y)\,\mathrm dx
=-\int_0^1 f_y(x,y)\,\mathrm dx.
\]
再对 \(y\) 积分并交换顺序。由 \(f(x,1)=0\)，有 \(\int_0^1y f_y\,\mathrm dy=-\int_0^1 f\,\mathrm dy\)。两个负号相消，得到 \(I=\iint_D f(x,y)\,\mathrm dx\,\mathrm dy=\boxed{a}\)。

% SOLUTION 296 2012 18
\textbf{入手角度}\quad 心形线已经给出径向上限，先完成半径积分，再把剩下的三角式化成多项式。

\textbf{解析}\quad 区域为 \(0\le\theta\le\pi,\ 0\le r\le1+\cos\theta\)，所以
\[
I=\frac14\int_0^\pi \cos\theta\sin\theta(1+\cos\theta)^4\,\mathrm d\theta.
\]
取 \(s=1+\cos\theta\)，得 \(I=\frac14\int_0^2(s-1)s^4\,\mathrm ds\)。求原函数并代入端点，得 \(\frac14(2^6/6-2^5/5)=\boxed{16/15}\)。

% SOLUTION 300 2016 18
\textbf{入手角度}\quad 三角形关于 \(y\) 轴对称，先消去含 \(xy\) 的奇函数项；剩下的分式只依赖比例 \(x/y\)。

\textbf{解析}\quad 区域为 \(0\le y\le1,\ -y\le x\le y\)。对 \(y>0\) 令 \(x=yt\)，得到
\[
I=\int_0^1y\,\mathrm dy\int_{-1}^1\frac{t^2-1}{t^2+1}\,\mathrm dt
=\frac12[t-2\arctan t]_{-1}^1
=\boxed{1-\pi/2}.
\]
原点处的取值不影响积分；其邻域内分式有界。

% SOLUTION 302 2018 17
\textbf{入手角度}\quad 摆线关于 \(x=\pi\) 对称，可把 \(x\) 项化成面积；剩下的 \(2y\) 对纵截线直接积分。

\textbf{解析}\quad 用 \(t\mapsto2\pi-t\)，可得 \(x\mapsto2\pi-x\)、高度不变，所以 \(\iint_D x\,\mathrm dx\,\mathrm dy=\pi |D|\)。又 \(x'=1-\cos t\ge0\)，区域高度为 \(1-\cos t\)。于是
\[
|D|=\int_0^{2\pi}(1-\cos t)^2\,\mathrm dt=3\pi.
\]
对 \(2y\) 先积分 \(y\) 得高度的平方，再乘 \(\mathrm dx=(1-\cos t)\,\mathrm dt\)，得 \(\int_0^{2\pi}(1-\cos t)^3\,\mathrm dt=5\pi\)。其中奇次余弦项积分为零，\(\int_0^{2\pi}\cos^2t\,\mathrm dt=\pi\)。故所求为 \(\boxed{3\pi^2+5\pi}\)。

% SOLUTION 305 2021 21
\textbf{入手角度}\quad 方程两边齐次次数不同，极坐标下可直接解出半径上限。被积函数中的 \(xy\) 又可配出 \(\cos2\theta\) 的导数。

\textbf{解析}\quad 边界 \(r^4=r^2\cos2\theta\) 给出 \(0\le\theta\le\pi/4,\ 0\le r\le\sqrt{\cos2\theta}\)。于是
\[
I=\frac14\int_0^{\pi/4}\sin\theta\cos\theta\cos^2(2\theta)\,\mathrm d\theta.
\]
令 \(s=\cos2\theta\)，有 \(\mathrm ds=-4\sin\theta\cos\theta\,\mathrm d\theta\)，故 \(I=\frac1{16}\int_0^1s^2\,\mathrm ds=\boxed{1/48}\)。

% SOLUTION 307 2023 20
\textbf{入手角度}\quad 两条二次曲线相似，固定极角后上下径向边界的比恒定；被积函数乘面积元后恰含 \(\mathrm dr/r\)。

\textbf{解析}\quad 令 \(q(\theta)=1-\sin\theta\cos\theta>0\)，极角从 \(0\) 到 \(\pi/3\)，半径从 \(q^{-1/2}\) 到 \((2/q)^{1/2}\)。因此
\[
I=\frac{\ln2}{2}\int_0^{\pi/3}\frac{\mathrm d\theta}{3\cos^2\theta+\sin^2\theta}.
\]
令 \(t=\tan\theta\)，角向积分变成 \(\int_0^{\sqrt3}\frac{\mathrm dt}{3+t^2}=\pi/(4\sqrt3)\)，所以 \(I=\boxed{\pi\ln2/(8\sqrt3)}\)。

% SOLUTION 310 2026 17
\textbf{入手角度}\quad 积分域由圆和两条斜射线围成，且正弦的自变量就是到原点的距离，适合极坐标。

\textbf{解析}\quad \(y\ge|x|\)、\(x^2+y^2\le2\) 给出 \(\pi/4\le\theta\le3\pi/4,\ 0\le r\le\sqrt2\)。故
\[
I=\int_{\pi/4}^{3\pi/4}\sin\theta\,\mathrm d\theta
\int_0^{\sqrt2}r^2\sin r\,\mathrm dr.
\]
角向积分为 \(\sqrt2\)。两次分部积分得到径向原函数 \(-r^2\cos r+2r\sin r+2\cos r\)，端点差为 \(2\sqrt2\sin\sqrt2-2\)。因此 \(I=\boxed{4\sin\sqrt2-2\sqrt2}\)。

% SOLUTION 312 2014 4
\textbf{入手角度}\quad 题目直接给出参数方程，用速度和加速度求曲率半径，无需求出 \(y\) 关于 \(x\) 的显式表达式。

\textbf{解析}\quad 在 \(t=1\)，有 \(x'=2,y'=6,x''=2,y''=2\)。曲率半径为
\[
\rho=\frac{(x'^2+y'^2)^{3/2}}{|x'y''-y'x''|}
=\frac{40^{3/2}}8
=10\sqrt{10}.
\]
选 \(\mathrm C\)。

% SOLUTION 314 2019 6
\textbf{入手角度}\quad 用差函数的二阶展开解释极限；检查逆命题时注意曲率公式中二阶导有绝对值。

\textbf{解析}\quad 令 \(h=f-g\)。若 \(h(x)/(x-a)^2\to0\)，Taylor 展开依次给出 \(h(a)=h'(a)=h''(a)=0\)。于是两曲线同点、同切线，且二阶导相同，曲率相同。逆向取 \(f(x)=(x-a)^2,\ g(x)=-(x-a)^2\)。两曲线在 \((a,0)\) 共切线，曲率均为 \(2\)，但差商恒为 \(2\)。故条件充分且不必要，选 \(\mathrm A\)。

% SOLUTION 315 2012 13
\textbf{入手角度}\quad 二阶导为常数，曲率条件只限制切线斜率的绝对值。求出横坐标后用定义域筛选。

\textbf{解析}\quad \(y'=2x+1,\ y''=2\)，所以
\[
K=\frac{2}{[1+(2x+1)^2]^{3/2}}=\frac1{\sqrt2}.
\]
整理得 \(1+(2x+1)^2=2\)，解为 \(x=0,-1\)。由 \(x<0\) 仅取 \(x=-1\)，相应 \(y=0\)。所求点为 \(\boxed{(-1,0)}\)。

% SOLUTION 316 2018 12
\textbf{入手角度}\quad 参数曲线在 \(t=\pi/4\) 时正弦与余弦相等，先保留这个公共值可以简化速度与加速度。

\textbf{解析}\quad 记 \(q=1/\sqrt2\)。由 \(x=\cos^3t,\ y=\sin^3t\) 分别求两次导数，代入得 \(x'=-3q^3,\ y'=3q^3,\ x''=3q^3,\ y''=3q^3\)。于是速度大小为 \(3/2\)，\(|x'y''-y'x''|=18q^6=9/4\)。由参数曲率公式，\(K=(9/4)/(3/2)^3=\boxed{2/3}\)。

% SOLUTION 317 2024 11
\textbf{入手角度}\quad 原点切线竖直，把 \(y\) 作为参数可避开 \(y(x)\) 在原点的导数问题。

\textbf{解析}\quad 令 \(x=t^2,\ y=t\)。在 \(t=0\)，速度为 \((0,1)\)、加速度为 \((2,0)\)，故曲率 \(K=2\)，主法线指向 \(x\) 正方向。半径 \(1/2\)，圆心为 \((1/2,0)\)，因此曲率圆为 \(\boxed{(x-\frac12)^2+y^2=\frac14}\)。


\QuestionPage{A.1 多元函数微分学}{选择题}{2024 年第 5 题}{1}{偏导数与可微性}{247 / 408}
已知函数
\[f(x,y)=
\begin{cases}
(x^2+y^2)\sin\frac{1}{xy}, & xy\ne 0,\\
0, & xy=0,
\end{cases}
\]
则在点 \((0,0)\) 处（ ）
\choices{\(\dfrac{\partial f}{\partial x}\) 连续，\(f\) 可微}{\(\dfrac{\partial f}{\partial x}\) 连续，\(f\) 不可微}{\(\dfrac{\partial f}{\partial x}\) 不连续，\(f\) 可微}{\(\dfrac{\partial f}{\partial x}\) 不连续，\(f\) 不可微}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2025 年第 1 题}{1}{隐函数偏导数}{248 / 408}
设函数 \(z = z\left( x, y \right)\) 由 \(z + \ln z - \int_{y}^{x} e^{-t^{2}} \mathrm{~d} t = 0\) 确定，则 \(\frac{\partial z}{\partial x} + \frac{\partial z}{\partial y} =\)
\choices{\(\frac{z}{z + 1}\left( e^{-x^{2}} - e^{-y^{2}} \right)\)}{\(\frac{z}{z + 1}\left( e^{-x^{2}} + e^{-y^{2}} \right)\)}{\(-\frac{z}{z + 1}\left( e^{-x^{2}} - e^{-y^{2}} \right)\)}{\(-\frac{z}{z + 1}\left( e^{-x^{2}} + e^{-y^{2}} \right)\)}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2026 年第 3 题}{1}{隐函数偏导数}{249 / 408}
设函数 \(z=z(x,y)\) 由方程 \(x-az=e^{y+az}\)（\(a\) 为非零常数）确定，则
\choices{\(\dfrac{\partial z}{\partial x}-\dfrac{\partial z}{\partial y}=\dfrac1a\)}{\(\dfrac{\partial z}{\partial x}+\dfrac{\partial z}{\partial y}=\dfrac1a\)}{\(\dfrac{\partial z}{\partial x}-\dfrac{\partial z}{\partial y}=-\dfrac1a\)}{\(\dfrac{\partial z}{\partial x}+\dfrac{\partial z}{\partial y}=-\dfrac1a\)}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2017 年第 12 题}{2}{由全微分恢复二元函数}{253 / 408}
设函数$f(x,y)$具有一阶连续偏导数，且$\,\mathrm{d}{} f(x,y) = y\mathrm{e}^y \,\mathrm{d} x + x(1 + y) \mathrm{e}^y \,\mathrm{d} y$，$f(0,0) = 0$，
则$f(x,y)=$ \blank{}．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2018 年第 13 题}{2}{隐函数的偏导数}{254 / 408}
设函数$z = z(x,y)$由方程$\ln z + \mathrm{e}^{z - 1} = xy$确定，
则$\left.\frac{\partial z}{\partial x}\right|_{\left(2,\frac{1}{2}\right)} =$ \blank{}．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2023 年第 13 题}{2}{隐函数偏导数}{258 / 408}
设函数 \(z=z(x,y)\) 由
\[e^z+xz=2x-y
\]
确定，则
\[\left.\frac{\partial^2 z}{\partial x^2}\right|_{(1,1)}
=\blank{}.
\]
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2026 年第 14 题}{2}{全微分与复合求导}{260 / 408}
已知函数 \(f(x,y)\) 可微，且
\[df(0,0)=\pi\,dx+3\,dy.
\]
记
\[g(x)=f(\ln x,\sin \pi x),
\]
则
\[g'(1)=\ \blank{}.
\]
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2009 年第 17 题}{3}{二阶偏导数}{261 / 408}
设$z=f(x+y,x-y,xy)$，其中$f$具有$2$阶连续偏导数，
求$\,\mathrm{d} z$与$\frac{\partial{}^2 z}{\partial x\partial{} y}$．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2010 年第 19 题}{3}{二阶偏导数与变量变换}{262 / 408}
设函数$u = f(x,y)$具有二阶连续偏导数，且满足等式
$4\frac{\partial{}^2 u}{\partial{} x^2} + 12\frac{\partial{}^2 u}{\partial x\partial{} y} + 5\frac{\partial{}^2 u}{\partial{} y^2} = 0$．
确定$a$,$b$的值，使等式在变换$\xi = x + ay,\eta = x + by$下化简为$\frac{\partial{}^2 u}{\partial{} \xi \partial{} \eta} = 0$．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2014 年第 18 题}{3}{复合函数偏导与方程变换}{266 / 408}
设函数$f(u)$具有二阶连续导数，$z = f\left(\mathrm{e}^x\cos y \right)$满足
\[
\frac{\partial{}^2 z}{\partial{} x^2} + \frac{\partial{}^2 z}{\partial{} y^2} = \left(4z + \mathrm{e}^x\cos y \right) \mathrm{e}^{2x}.
\]
若$f(0) = 0,f'(0) = 0$，求$f(u)$的表达式．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2014 年第 21 题}{4}{由偏导数恢复边界与旋转体积}{267 / 408}
已知函数$f(x,y)$满足$\frac{\partial f}{\partial y} = 2(y + 1)$，且$f(y,y) = (y + 1)^2 - (2 - y)\ln y$，
求曲线$f(x,y) = 0$所围成的图形绕直线$y = - 1$旋转所成的旋转体的体积．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2017 年第 16 题}{2}{复合函数的二阶偏导}{270 / 408}
设函数$f(u,v)$具有$2$阶连续偏导数，$y = f(\mathrm{e}^x,\cos x)$，求$\frac{\,\mathrm{d} y}{\,\mathrm{d} x}\big|_{x = 0}$，$\frac{\,\mathrm{d}{}^2y}{\,\mathrm{d} x^2}\big|_{x = 0}$．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2018 年第 19 题}{3}{多元约束最值}{271 / 408}
将长为$2m$的铁丝分成三段，依次围成圆、正方形与正三角形，
三个图形的面积之和是否存在最小值？若存在，求出最小值．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2019 年第 20 题}{3}{偏导数与方程变换}{272 / 408}
已知函数$u(x,y)$满足关系式
$2\frac{\partial{}^2 u}{\partial{} x^2} - 2\frac{\partial{}^2 u}{\partial{} y^2} + 3\frac{\partial u}{\partial x} + 3\frac{\partial u}{\partial y} = 0$．
求$a$, $b$的值，使得在变换$u(x,y) = v(x,y) \mathrm{e}^{ax + by}$之下，
上述等式可化为函数$v(x,y)$的不含一阶偏导数的等式．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2022 年第 20 题}{3}{由偏导数恢复二元函数及其极值}{274 / 408}
已知可微函数 \(f\left( u,v \right)\) 满足
\(\frac{\partial f\left( u,v \right)}{\partial u} - \frac{\partial f\left( u,v \right)}{\partial v} = 2\left( u-v \right)e^{-\left( u+v \right)}\)
且
\(f\left( u,0 \right) = u^{2}e^{-u}\)
（I） 记 \(g\left( x,y \right) = f\left( x,y-x \right)\)，求 \(\frac{\partial g\left( x,y \right)}{\partial x}\)；
（II） 求 \(f\left( u,v \right)\) 的表达式与极值.
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2024 年第 20 题}{3}{偏导数与原函数}{276 / 408}
设 \(f(u,v)\) 具有二阶连续偏导，
\[g(x,y)=f(2x+y,\,3x-y),
\]
且满足
\[\frac{\partial^2g}{\partial x^2}
+\frac{\partial^2g}{\partial x\partial y}
-6\frac{\partial^2g}{\partial y^2}=1.
\]
\begin{enumerate}
\item 求 \(\dfrac{\partial^2f}{\partial u\partial v}\)；
\item 若 \(\dfrac{\partial f(u,0)}{\partial u}=ue^{-u}\)，且 \(f(0,v)=\dfrac{1}{50}v^2-1\)，求 \(f(u,v)\)。
\end{enumerate}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2025 年第 19 题}{3}{利用全微分求函数及极值}{277 / 408}
（本题满分 12 分）
设函数 \(f\left( x, y \right)\) 可微且满足 \(\mathrm{d} f\left( x, y \right) = -2x e^{-y} \mathrm{d} x + e^{-y}\left( x^{2} - y - 1 \right) \mathrm{d} y\)，\(f\left( 0, 0 \right) = 2\)，求 \(f\left( x, y \right)\)，并求 \(f\left( x, y \right)\) 的极值.
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2026 年第 19 题}{2}{二元函数极值}{278 / 408}
（本题满分 12 分）
求函数
\[f(x,y)=(2x^2-y^2)e^x
\]
的极值.
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2026 年第 7 题}{1}{二重积分定义与对称性}{289 / 408}
设函数 \(f(x,y)\) 在区域
\[D=\{(x,y)\mid 0\le x\le 1,\ 0\le y\le 1\}
\]
上连续，且 \(f(x,y)=f(y,x)\)，则
\[\iint_D f(x,y)\,dx\,dy=
\]
\choices{\(\displaystyle 2\lim_{n\to\infty}\sum_{i=1}^n\sum_{j=n+1-i}^n f\!\left(\frac{i}{n},\frac{j}{n}\right)\frac{1}{n^2}\)}{\(\displaystyle \frac12\lim_{n\to\infty}\sum_{i=1}^n\sum_{j=1}^n f\!\left(\frac{i}{n},\frac{j}{n}\right)\frac{1}{n^2}\)}{\(\displaystyle 2\lim_{n\to\infty}\sum_{i=1}^{2n}\sum_{j=1}^{2n+1-i} f\!\left(\frac{i}{2n},\frac{j}{2n}\right)\frac{1}{n^2}\)}{\(\displaystyle \frac12\lim_{n\to\infty}\sum_{i=1}^{2n}\sum_{j=1}^i f\!\left(\frac{i}{2n},\frac{j}{2n}\right)\frac{1}{n^2}\)}
\QuestionEnd
\QuestionPage{A.2 二重积分}{填空题}{2011 年第 13 题}{2}{极坐标二重积分}{290 / 408}
设平面区域$D$由直线$y = x$，圆$x^2 + y^2 = 2y$及$y$轴围成，则二重积分$\iint_D xy\,\mathrm{d}{}\sigma =$ \blank{}．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2009 年第 19 题}{3}{区域对称与二重积分}{293 / 408}
计算二重积分$\iint_D (x - y)\,\mathrm{d} x\,\mathrm{d} y$，
其中$D = \left\{(x,y) \middle| (x - 1)^2 + (y - 1)^2 \le 2,y \ge x \right\}$．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2010 年第 20 题}{3}{二重积分计算}{294 / 408}
计算二重积分
\[
I = \iint_D r^2\sin \theta\sqrt{1 - r^2\cos 2\theta} \,\mathrm{d} r\,\mathrm{d}{}\theta,
\]
其中$D=\left\{(r,\theta)\middle|0 \le r \le \sec \theta ,0 \le \theta \le \frac{\pi}{4} \right\}$．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2011 年第 21 题}{4}{含偏导数的二重积分}{295 / 408}
已知函数$f(x,y)$具有二阶连续偏导数，且
\[
f(1,y) = 0,\quad f(x,1) = 0,\quad \iint_D f(x,y)\,\mathrm{d} x\,\mathrm{d} y = a,
\]
其中$D = \left\{(x,y)\middle|0 \le x \le 1,0 \le y \le 1 \right\}$，
计算二重积分$I = \iint_D xy f''_{xy}(x,y)\,\mathrm{d} x\,\mathrm{d} y$．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2012 年第 18 题}{3}{心形线区域上的二重积分}{296 / 408}
计算二重积分$\iint_D xy\,\mathrm{d}{}\sigma$，其中区域D为曲线
\[
r = 1 + \cos \theta \;\left(0 \le \theta \le \pi \right)
\]
与极轴围成．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2016 年第 18 题}{3}{二重积分计算}{300 / 408}
设$D$是由直线$y = 1$，$y = x$，$y = - x$围成的有界区域，
计算二重积分$\iint_D \frac{x^2 - xy - y^2}{x^2 + y^2}\,\mathrm{d} x\,\mathrm{d} y.$
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2018 年第 17 题}{3}{参数曲线围成区域上的积分}{302 / 408}
设平面区域$D$由曲线$\begin{cases}
  x = t - \sin t \\
  y = 1 - \cos t
\end{cases}$（$0 \le t \le 2\pi$）与$x$轴围成，计算二重积分$\iint_D \left(x + 2y \right)\,\mathrm{d} x\,\mathrm{d} y$．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2021 年第 21 题}{4}{极坐标二重积分}{305 / 408}
曲线
\[\left(x^{2}+y^{2}\right)^{2}=x^{2}-y^{2},
\]
其中 \(x \ge 0,\ y \ge 0\)，与 \(x\) 轴围成的区域为 \(D\)，求
\[\iint_{D} xy \,\mathrm{d}x\,\mathrm{d}y.
\]
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2023 年第 20 题}{4}{二重积分的变量代换}{307 / 408}
设平面有界区域 \(D\) 位于第一象限，由曲线
\[x^2+y^2-xy=1,\qquad x^2+y^2-xy=2
\]
与直线
\[y=\sqrt3\,x,\qquad y=0
\]
围成，计算
\[\iint_D \frac{1}{3x^2+y^2}\,dx\,dy.
\]
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2026 年第 17 题}{2}{二重积分计算}{310 / 408}
（本题满分 10 分）
计算
\[I=\int_{-1}^1 dx\int_{|x|}^{\sqrt{2-x^2}} y\sin\sqrt{x^2+y^2}\,dy.
\]
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2014 年第 4 题}{1}{参数曲线的曲率半径}{312 / 408}
曲线$\begin{cases}
  x = t^2 + 7, \\
  y = t^2 + 4t + 1
\end{cases}$上对应于$t = 1$的点处的曲率半径是\pickout{}
\begin{abcd}
\item $\frac{\sqrt{10}}{50}$．
\item $\frac{\sqrt{10}}{100}$．
\item $10\sqrt{10}$．
\item $5\sqrt{10}$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2019 年第 6 题}{1}{相切、曲率与二阶展开}{314 / 408}
设函数$f(x),g(x)$的二阶导函数在$x = a$处连续，
则$\lim_{x \to a} \frac{f(x) - g(x)}{(x - a)^2} = 0$
是两条曲线$y = f(x)$，$y = g(x)$在$x = a$对应的点处相切及曲率相等的\pickout{}
\begin{abcd}
\item 充分不必要条件．
\item 充分必要条件．
\item 必要不充分条件．
\item 既不充分也不必要条件．
\end{abcd}
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2012 年第 13 题}{2}{曲率与点的坐标}{315 / 408}
曲线$y = x^2 + x$（$x < 0$）上曲率为$\frac{\sqrt{2}}{2}$的点的坐标是 \blank{}．
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2018 年第 12 题}{2}{参数曲线的曲率}{316 / 408}
曲线$\begin{cases}
  x = \cos^3 t \\
  y = \sin^3 t
\end{cases}$在$t = \frac{\pi}{4}$对应点的曲率为 \blank{}．
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{填空题}{2024 年第 11 题}{2}{曲率圆方程}{317 / 408}
曲线 \(y^2=x\) 在点 \((0,0)\) 处的曲率圆方程为 \blank{}
\QuestionEnd


## tool · 2026-11-10T10:08:06Z


Script completed
Wall time 0.1 seconds
Output:

% SOLUTION 235 2009 3
\textbf{入手角度}\quad 全微分的两个系数各只依赖一个变量，先恢复函数，再直接比较函数值。

\textbf{解析}\quad 有 \(f_x=x\)、\(f_y=y\)。对第一式关于 \(x\) 积分得 \(f=x^2/2+h(y)\)，再由第二式得 \(h(y)=y^2/2+C\)。因此 \(f(x,y)-f(0,0)=(x^2+y^2)/2>0\) 对所有非原点成立，原点是严格极小值点。选 \(\mathrm D\)。

% SOLUTION 236 2010 5
\textbf{入手角度}\quad 题目给出的组合是沿 \((x,y)\) 同时缩放时的导数，可用算子 \(L=x\partial_x+y\partial_y\) 一次处理。

\textbf{解析}\quad 由商法则得 \(L(y/x)=0\)，而 \(L(z/x)=(Lz-z)/x\)。对 \(F(y/x,z/x)=0\) 施加 \(L\)，链式法则给出 \(F'_2(Lz-z)/x=0\)。定义域内 \(x\ne0\)，且 \(F'_2\ne0\)，故 \(Lz=z\)。选 \(\mathrm B\)。

% SOLUTION 237 2011 5
\textbf{入手角度}\quad 两个自变量分别进入乘积的两个因子，驻点处的混合二阶偏导会消失。

\textbf{解析}\quad 记 \(a=f(0)>0\)、\(b=f''(0)\)。由 \(f'(0)=0\)，原点梯度为零；Hessian 的三个系数是 \(z_{xx}=b\ln a\)、\(z_{xy}=0\)、\(z_{yy}=b\)。若 \(a>1\) 且 \(b>0\)，两个对角元均为正，Hessian 正定，故原点为严格极小值点。选 \(\mathrm A\)。

% SOLUTION 238 2012 5
\textbf{入手角度}\quad 用一个中间点将两个坐标的变化分开，让两次变化都使函数值增加。

\textbf{解析}\quad 固定 \(y\) 时，由 \(f_x>0\) 知函数随 \(x\) 严格增加；固定 \(x\) 时，由 \(f_y<0\) 知函数随 \(y\) 严格减少。若 \(x_1<x_2,\ y_1>y_2\)，则
\[
f(x_1,y_1)<f(x_2,y_1)<f(x_2,y_2).
\]
这正是选项 \(\mathrm D\) 的条件。

% SOLUTION 239 2013 5
\textbf{入手角度}\quad 分别保留乘子 \(y/x\) 和复合自变量 \(xy\) 的导数，看哪些项能抵消。

\textbf{解析}\quad 链式法则给出 \(z_x=-yf(xy)/x^2+(y^2/x)f'(xy)\) 和 \(z_y=f(xy)/x+yf'(xy)\)。第一式乘以 \(x/y\) 再与第二式相加，两个 \(f(xy)/x\) 项抵消，余下 \(2yf'(xy)\)。选 \(\mathrm A\)。

% SOLUTION 240 2014 6
\textbf{入手角度}\quad 先由闭有界性保证最值存在，再用 Hessian 排除内部的极值。

\textbf{解析}\quad 任意内部点的 Hessian 行列式为
\[
u_{xx}u_{yy}-u_{xy}^{\,2}=-u_{xx}^{\,2}-u_{xy}^{\,2}<0.
\]
内部非驻点不能是极值点；内部驻点处二阶型一正一负，也不能取极值。连续函数在闭有界区域上能取得最大值和最小值，所以所有最大、最小值点都位于边界。选 \(\mathrm A\)。

% SOLUTION 241 2015 5
\textbf{入手角度}\quad \(x^2-y^2=(x+y)(x-y)\)，已知 \(u=x+y\) 后，用 \(v=y/x\) 表示差。

\textbf{解析}\quad 在 \((u,v)=(1,1)\) 附近 \(1+v\ne0\)，反解得 \(x=u/(1+v)\)、\(y=uv/(1+v)\)。于是 \(f(u,v)=u^2(1-v)/(1+v)\)，从而
\[
f_u=\frac{2u(1-v)}{1+v},\qquad f_v=-\frac{2u^2}{(1+v)^2}.
\]
代入目标点得 \(0,-1/2\)，选 \(\mathrm D\)。

% SOLUTION 242 2016 6
\textbf{入手角度}\quad 沿 \((1,1)\) 同时改变 \(x,y\) 时分母 \(x-y\) 保持不变，优先考虑两个偏导的和。

\textbf{解析}\quad 在 \(x\ne y\) 时，
\[
f_x=\frac{e^x}{x-y}-\frac{e^x}{(x-y)^2},
\qquad f_y=\frac{e^x}{(x-y)^2}.
\]
相加即得 \(f_x+f_y=e^x/(x-y)=f\)，选 \(\mathrm D\)。

% SOLUTION 243 2017 5
\textbf{入手角度}\quad 比较两点时先看坐标移动对函数值的作用方向，避免把一个增加量与一个减少量直接相抵。

\textbf{解析}\quad \(f_x>0\) 使 \(f\) 关于 \(x\) 严格增加，\(f_y<0\) 使 \(f\) 关于 \(y\) 严格减少。故 \(f(0,1)<f(1,1)<f(1,0)\)，选 \(\mathrm D\)。而 \((0,0)\) 与 \((1,1)\) 之间两个坐标的作用相反，例如 \(f=x-ky\) 在 \(k>0\) 时满足条件，取不同 \(k\) 即可改变两点函数值的大小关系。

% SOLUTION 245 2021 6
\textbf{入手角度}\quad 两条参数曲线都经过 \((1,1)\)，它们的切向不同，可用两条链式法则解出两个偏导。

\textbf{解析}\quad 对第一式关于 \(x\) 求导并取 \(x=0\)，得 \(f_x(1,1)+f_y(1,1)=1\)。对第二式求导并取 \(x=1\)，右端 \(4x\ln x+2x\) 的值为 \(2\)，故 \(f_x(1,1)+2f_y(1,1)=2\)。解得 \(f_x=0,\ f_y=1\)，所以 \(\mathrm df(1,1)=\mathrm dy\)，选 \(\mathrm C\)。

% SOLUTION 246 2022 4
\textbf{入手角度}\quad 上限和被积函数都只通过 \(s=x-y\) 变化，先化为一元函数。

\textbf{解析}\quad 写成 \(F=G(s)\)，其中 \(G(s)=s\int_0^s f(t)\,\mathrm dt-\int_0^s tf(t)\,\mathrm dt\)。由微积分基本定理，求导时两个 \(sf(s)\) 相消，得到 \(G'(s)=\int_0^s f(t)\,\mathrm dt\)、\(G''(s)=f(s)\)。因而 \(F_x=-F_y=G'(s)\)，而 \(F_{xx}=F_{yy}=G''(s)\)。选 \(\mathrm C\)。

% SOLUTION 250 2012 11
\textbf{入手角度}\quad 两项求导后都有同一个外层导数，只需计算内层的加权变化率。

\textbf{解析}\quad 设 \(u=\ln x+1/y\)，则 \(z_x=f'(u)/x\)，\(z_y=-f'(u)/y^2\)。代入得 \(xz_x+y^2z_y=f'(u)-f'(u)=\boxed{0}\)。

% SOLUTION 251 2014 11
\textbf{入手角度}\quad 全微分中会出现 \(z\) 的点值，先用原方程确定它。

\textbf{解析}\quad 当 \(x=y=1/2\) 时，原方程化为 \(e^z+z=1\)，左端严格递增，故唯一解为 \(z=0\)。原方程微分为
\[
e^{2yz}(2z\,\mathrm dy+2y\,\mathrm dz)+\mathrm dx+2y\,\mathrm dy+\mathrm dz=0.
\]
代入该点后，\(2\,\mathrm dz+\mathrm dx+\mathrm dy=0\)，故 \(\boxed{\mathrm dz=-(\mathrm dx+\mathrm dy)/2}\)。

% SOLUTION 252 2015 13
\textbf{入手角度}\quad 在 \((0,0)\) 先求 \(z\)，再判断乘积项 \(xyz\) 的一阶贡献。

\textbf{解析}\quad 代入原式得 \(e^{3z}=1\)，故 \(z=0\)。微分后有
\[
e^{x+2y+3z}(\mathrm dx+2\,\mathrm dy+3\,\mathrm dz)
 +yz\,\mathrm dx+xz\,\mathrm dy+xy\,\mathrm dz=0.
\]
乘积项在该点的三个系数全为零，指数系数为 \(1\)，解得 \(\boxed{\mathrm dz=-\frac13\,\mathrm dx-\frac23\,\mathrm dy}\)。

% SOLUTION 255 2019 11
\textbf{入手角度}\quad 给定的加权算子作用在 \(y^2/x\) 上时为零，只有外部乘子 \(y\) 留下贡献。

\textbf{解析}\quad 记 \(u=y^2/x\)。有 \(z_x=-y^3f'(u)/x^2\)，\(z_y=f(u)+2y^2f'(u)/x\)。故 \(2xz_x+yz_y\) 中的 \(f'(u)\) 项相消，结果为 \(\boxed{yf(y^2/x)=z}\)。

% SOLUTION 256 2020 11
\textbf{入手角度}\quad 把反正切视作外层，先求其内层在目标点的微分。

\textbf{解析}\quad 令 \(u=xy+\sin(x+y)\)。则 \(\mathrm dz=\mathrm du/(1+u^2)\)，而
\[
\mathrm du=(y+\cos(x+y))\,\mathrm dx+(x+\cos(x+y))\,\mathrm dy.
\]
在 \((0,\pi)\)，\(u=0\)、\(\cos(x+y)=-1\)，故 \(\boxed{\mathrm dz=(\pi-1)\,\mathrm dx-\mathrm dy}\)。

% SOLUTION 257 2021 13
\textbf{入手角度}\quad 先找 \(z(0,2)\)，再固定 \(y\) 对方程求偏导。

\textbf{解析}\quad \(z+2\ln z=1\) 的左端在 \(z>0\) 上严格递增，故此点 \(z=1\)。求偏导得
\[
z+(x+1+y/z)z_x-\frac{2y}{1+4x^2y^2}=0.
\]
代入 \((x,y,z)=(0,2,1)\)，得 \(1+3z_x-4=0\)，故 \(\boxed{z_x=1}\)。

% SOLUTION 259 2024 12
\textbf{入手角度}\quad 函数是 \(x\) 项和 \(y\) 项之和，驻点分别求出，再比较两个方向的二阶符号。

\textbf{解析}\quad \(f_x=6(x-1)(x-2)\)、\(f_y=24(1-y^3)\)，驻点仅有 \((1,1)\)、\((2,1)\)。二阶偏导为 \(f_{xx}=12x-18\)、\(f_{yy}=-72y^2\)、\(f_{xy}=0\)。在 \((1,1)\) 两对角元都负，为极大值点；在 \((2,1)\) 符号相反，为鞍点。唯一的极值点是 \(\boxed{(1,1)}\)。

% SOLUTION 263 2011 17
\textbf{入手角度}\quad 先对 \(y\) 求导可以避免引入 \(g''\)。极值条件给出 \(g'(1)=0\)，代入后大量项会消失。

\textbf{解析}\quad 令 \(u=xy,\ v=yg(x)\)。先得 \(z_y=xf_1+g(x)f_2\)，再对 \(x\) 求导得
\[
\begin{aligned}
z_{xy}={}& f_1+xyf_{11}+xyg'f_{12}+g'f_2\\
 &+ygf_{21}+ygg'f_{22}.
\end{aligned}
\]
在 \(x=y=1\) 时，\(u=v=1,\ g(1)=1,\ g'(1)=0\)。故结果为 \(\boxed{(f_1+f_{11}+f_{12})(1,1)}\)。

% SOLUTION 264 2012 16
\textbf{入手角度}\quad 指数可拆成 \(x,y\) 两部分。先控制一元因子 \(xe^{-x^2/2}\) 的绝对值，再看 \(y\) 的取等条件。

\textbf{解析}\quad 由
\[
f_x=(1-x^2)e^{-(x^2+y^2)/2},\qquad
f_y=-xye^{-(x^2+y^2)/2}
\]
可知驻点只有 \((1,0),(-1,0)\)。在 \(t\ge0\) 上，\(t e^{-t^2/2}\) 的导数是 \((1-t^2)e^{-t^2/2}\)，故最大值 \(e^{-1/2}\) 仅在 \(t=1\) 取得。又 \(e^{-y^2/2}\le1\)，等号当且仅当 \(y=0\)。结合 \(f\) 与 \(x\) 同号，知 \((1,0)\) 的极大值为 \(e^{-1/2}\)，\((-1,0)\) 的极小值为 \(-e^{-1/2}\)，两者也是全局最值。

% SOLUTION 268 2015 17
\textbf{入手角度}\quad 沿 \(y\)、\(x\) 依次积分，分别用题给的边线条件确定两次积分产生的函数。

\textbf{解析}\quad 由 \(f_{xy}=2(y+1)e^x\) 得
\[
f_x(x,y)=(y^2+2y)e^x+f_x(x,0)=(x+1+y^2+2y)e^x.
\]
再积分得 \(f=(x+y^2+2y)e^x+C(y)\)。代入 \(f(0,y)=y^2+2y\)，知 \(C=0\)。驻点由 \(f_y=2(y+1)e^x=0\) 及 \(f_x=0\) 给出，只有 \((0,-1)\)。又
\[
f(x,y)=e^x(x-1)+e^x(y+1)^2.
\]
第一项导数为 \(xe^x\)，故最小值为 \(-1\)，只在 \(x=0\) 取到；第二项非负且在 \(y=-1\) 取零。因此唯一极值为 \(\boxed{f(0,-1)=-1}\)，是极小值。

% SOLUTION 273 2020 17
\textbf{入手角度}\quad 先从两条一阶偏导等式消元，再逐个检查 Hessian。

\textbf{解析}\quad 驻点方程是 \(y=3x^2,\ x=24y^2\)，消去 \(y\) 得 \(x=216x^4\)，故驻点为 \((0,0)\)、\((1/6,1/12)\)。Hessian 对角元为 \(6x,48y\)，非对角元为 \(-1\)。原点行列式为 \(-1\)，是鞍点；第二点处 \(f_{xx}=1\)、行列式 \(4-1=3>0\)，为严格极小值点。代回得唯一极值 \(\boxed{f(1/6,1/12)=-1/216}\)。

% SOLUTION 275 2023 18
\textbf{入手角度}\quad 关于 \(x\) 配平方，把问题分解成 \(x\) 方向的二次项与 \(y\) 方向的周期变化。

\textbf{解析}\quad 有
\[
f=\tfrac12(x+e^{\cos y})^2-\tfrac12 e^{2\cos y}.
\]
驻点须满足 \(x=-e^{\cos y}\)、\(-xe^{\cos y}\sin y=0\)，因此 \(y=k\pi\)。当 \(y=2k\pi\) 时 \(f=-e^2/2\)，由上式这是全局最小值。在 \(y=(2k+1)\pi\) 的驻点处，\(f_{xx}=1,\ f_{xy}=0,\ f_{yy}=-e^{-2}<0\)，故是鞍点。所有极值为 \(\boxed{f(-e,2k\pi)=-e^2/2}\)，其中 \(k\in\mathbb Z\)。

% SOLUTION 279 2009 4
\textbf{入手角度}\quad 两个积分域都可用同一组 \(y\) 值描述，先把第一块也写成水平截线。

\textbf{解析}\quad 第一块 \(1\le x\le2,\ x\le y\le2\) 等价于 \(1\le y\le2,\ 1\le x\le y\)。第二块是 \(1\le y\le2,\ y\le x\le4-y\)。同一个 \(y\) 下这两段恰好在 \(x=y\) 连接，因此总积分为
\[
\int_1^2\mathrm dy\int_1^{4-y} f(x,y)\,\mathrm dx.
\]
选 \(\mathrm C\)。

% SOLUTION 280 2010 6
\textbf{入手角度}\quad 双重和的两个下标各自遍历 \(1,\ldots,n\)，自然对应单位正方形的等面积网格。

\textbf{解析}\quad 通项改写成
\[
\frac{1}{(1+i/n)(1+(j/n)^2)}\cdot\frac1{n^2}.
\]
这是连续函数 \(1/[(1+x)(1+y^2)]\) 在单位正方形上的黎曼和，样点为各小方格右上角，面积为 \(1/n^2\)。极限为 \(\int_0^1\mathrm dx\int_0^1[(1+x)(1+y^2)]^{-1}\,\mathrm dy\)，选 \(\mathrm D\)。

% SOLUTION 282 2013 6
\textbf{入手角度}\quad 第二、四象限可以直接判定被积函数符号；第一、三象限用交换 \(x,y\) 的对称性。

\textbf{解析}\quad 第二象限内部有 \(x<0<y\)，故 \(y-x>0\)，所以 \(I_2>0\)。第四象限内部则 \(y-x<0\)，所以 \(I_4<0\)。第一、三象限的圆扇形分别在交换坐标后不变，而 \(y-x\) 变号，故 \(I_1=I_3=0\)。选 \(\mathrm B\)。

% SOLUTION 283 2015 6
\textbf{入手角度}\quad 两条射线给极角，两条双曲线给半径。把 \(2xy\) 改写成 \(r^2\sin(2\theta)\) 可直接读出半径平方。

\textbf{解析}\quad 由 \(y/x=\tan\theta\)，得 \(\pi/4\le\theta\le\pi/3\)。两条曲线给出
\[
\frac12\le r^2\sin(2\theta)\le1,\qquad
\frac1{\sqrt{2\sin(2\theta)}}\le r\le\frac1{\sqrt{\sin(2\theta)}}.
\]
极坐标面积元为 \(r\,\mathrm dr\,\mathrm d\theta\)，同时满足范围和面积元要求的选项为 \(\mathrm B\)。

% SOLUTION 284 2018 6
\textbf{入手角度}\quad 两个积分的下边界拼成 \(y=|x|\)。区域关于 \(y\) 轴对称，可以先消去奇函数项。

\textbf{解析}\quad 合并区域得 \(-1\le x\le1,\ |x|\le y\le2-x^2\)。\(xy\) 在 \(x\mapsto-x\) 下变号，积分为零，所求即区域面积：
\[
2\int_0^1(2-x^2-x)\,\mathrm dx
=2\left(2-\frac13-\frac12\right)=\frac73.
\]
选 \(\mathrm C\)。

% SOLUTION 285 2019 5
\textbf{入手角度}\quad 三个被积函数只依赖径向距离 \(r\)，优先逐点比较，再积分。

\textbf{解析}\quad 在 \(D\) 内有 \(0\le r=\sqrt{x^2+y^2}\le |x|+|y|\le\pi/2\)。当 \(0<r<\pi/2\) 时，\(\sin r<r\)；又 \(\sin r+\cos r>1\)，因为平方为 \(1+\sin(2r)>1\)，所以 \(1-\cos r<\sin r\)。严格不等式在正面积的内部成立，故积分满足 \(I_3<I_2<I_1\)。选 \(\mathrm A\)。

% SOLUTION 286 2022 2
\textbf{入手角度}\quad 分母只含 \(x\)，原次序直接积分不便；换成先对 \(y\) 积分会出现 \(x^2\)，恰好配合 \(x^3\) 换元。

\textbf{解析}\quad 区域是 \(0\le y\le x\le2\)。交换次序后
\[
\int_0^2\frac{\mathrm dx}{\sqrt{1+x^3}}\int_0^x y\,\mathrm dy
=\frac12\int_0^2\frac{x^2}{\sqrt{1+x^3}}\,\mathrm dx
=\left[\frac{\sqrt{1+x^3}}3\right]_0^2=\frac23.
\]
选 \(\mathrm D\)。

% SOLUTION 287 2024 6
\textbf{入手角度}\quad 换序时固定 \(y\)，要先确定 \(\sin x\le y\) 在给定 \(x\) 区间内等价的限制。

\textbf{解析}\quad 原区域为 \(\pi/6\le x\le\pi/2,\ \sin x\le y\le1\)。在此区间 \(\sin x\) 单调增加，故 \(y\) 的范围是 \(1/2\le y\le1\)，固定 \(y\) 时 \(\pi/6\le x\le\arcsin y\)。换序即为 \(\int_{1/2}^1\mathrm dy\int_{\pi/6}^{\arcsin y}f(x,y)\,\mathrm dx\)，选 \(\mathrm A\)。

% SOLUTION 288 2025 5
\textbf{入手角度}\quad 抛物线在每条水平截线上一般切出左右两块，需要分别保留。只有区域对称还不能将两侧积分相乘。

\textbf{解析}\quad 原区域为 \(-2\le x\le2,\ 4-x^2\le y\le4\)。固定 \(y\in[0,4]\)，由 \(x^2\ge4-y\) 得
\[
x\in[-2,-\sqrt{4-y}]\ \cup\ [\sqrt{4-y},2].
\]
将两段从左到右积分，再对 \(y\) 从 \(0\) 积到 \(4\)，得到选项 \(\mathrm A\)。若 \(f\) 对 \(x\) 并非偶函数，两侧的积分未必相等，不能用右侧乘二。

% SOLUTION 291 2020 10
\textbf{入手角度}\quad 被积函数只含 \(x\)，交换次序以后，对 \(y\) 的积分直接给出一个 \(x^2\)。

\textbf{解析}\quad 区域 \(0\le y\le1,\ \sqrt y\le x\le1\) 等价于 \(0\le x\le1,\ 0\le y\le x^2\)。因此
\[
\int_0^1 x^2\sqrt{1+x^3}\,\mathrm dx
=\left[\frac29(1+x^3)^{3/2}\right]_0^1
=\boxed{\frac29(2\sqrt2-1)}.
\]

% SOLUTION 298 2014 17
\textbf{入手角度}\quad 区域在交换坐标后不变，\(x/(x+y)\) 与交换后的比例恰好相加为 \(1\)。

\textbf{解析}\quad 设 \(r=\sqrt{x^2+y^2}\)。由交换对称性，
\[
I=\frac12\iint_D\sin(\pi r)\,\mathrm dx\,\mathrm dy
=\frac{\pi}{4}\int_1^2 r\sin(\pi r)\,\mathrm dr.
\]
最后积分的原函数为 \(-r\cos(\pi r)/\pi+\sin(\pi r)/\pi^2\)，端点差为 \(-3/\pi\)，故 \(I=\boxed{-3/4}\)。

% SOLUTION 299 2015 18
\textbf{入手角度}\quad 关于 \(y\) 轴的对称性可消去 \(xy\)；剩余 \(x^2\) 只需乘以纵截线长度。

\textbf{解析}\quad 抛物线与圆上半支相交于 \(x=\pm1\)，纵向范围为 \(x^2\le y\le\sqrt{2-x^2}\)。故
\[
I=2\int_0^1x^2\sqrt{2-x^2}\,\mathrm dx-2\int_0^1x^4\,\mathrm dx.
\]
第一积分令 \(x=\sqrt2\sin t\)，化为 \(\int_0^{\pi/4}\sin^2(2t)\,\mathrm dt=\pi/8\)。第二积分为 \(1/5\)，所以 \(I=\boxed{\pi/4-2/5}\)。

% SOLUTION 301 2017 20
\textbf{入手角度}\quad 区域是圆心 \((0,1)\) 的单位圆盘。展开平方后，用圆盘的对称性分别算一次项、二次项和面积。

\textbf{解析}\quad \(\iint_D 2x\,\mathrm dx\,\mathrm dy=0\)，常数项积分为 \(\pi\)。圆心坐标下 \(x=r\cos\theta\)，故
\[
\iint_D x^2\,\mathrm dx\,\mathrm dy
=\int_0^1r^3\,\mathrm dr\int_0^{2\pi}\cos^2\theta\,\mathrm d\theta=\frac\pi4.
\]
总积分为 \(\boxed{5\pi/4}\)。

% SOLUTION 304 2020 19
\textbf{入手角度}\quad 被积函数在 \(x>0\) 时只依赖 \(y/x\)，而纵截线从 \(y=0\) 到 \(y=x\)，换元后上下限变成常数。

\textbf{解析}\quad 固定 \(x\) 令 \(y=xt\)，则
\[
I=\int_1^2 x\,\mathrm dx\int_0^1\sqrt{1+t^2}\,\mathrm dt.
\]
一元原函数为 \(\tfrac12[t\sqrt{1+t^2}+\ln(t+\sqrt{1+t^2})]\)，故
\[
I=\boxed{\frac34\bigl(\sqrt2+\ln(1+\sqrt2)\bigr)}.
\]

% SOLUTION 308 2024 17
\textbf{入手角度}\quad 交换 \(x,y\) 会保留区域并使 \(x-y\) 变号。求面积时，把两组边界分别用 \(xy\) 和 \(y/x\) 表示。

\textbf{解析}\quad 由对称性，\(x-y\) 的积分为零。令 \(u=xy,\ v=y/x\)，则 \(u,v\in[1/3,3]\)，且
\[
\frac{\partial(u,v)}{\partial(x,y)}
=\begin{vmatrix}y&x\\-y/x^2&1/x\end{vmatrix}=2v.
\]
第一象限内变换一一对应，故面积为
\[
\int_{1/3}^3\mathrm du\int_{1/3}^3\frac{\mathrm dv}{2v}
=\boxed{\frac83\ln3}.
\]

% SOLUTION 313 2016 5
\textbf{入手角度}\quad 两曲线在切点的斜率相同，比较曲率等价于比较二阶导的绝对值。结合二阶导的符号，可由 Taylor 展开判断相对位置。

\textbf{解析}\quad \(f_i(x_0)=g(x_0)\)，且 \(f_i'(x_0)=g'(x_0)\)。由曲率公式及共同斜率，曲率严格较大给出 \(|f_1''(x_0)|>|f_2''(x_0)|\)。又两者二阶导均负，故 \(f_1''(x_0)<f_2''(x_0)<0\)。令 \(h=x-x_0\)，则
\[
f_i(x)-g(x)=\tfrac12 f_i''(x_0)h^2+o(h^2).
\]
小邻域内 \(f_2-g\le0\)，且 \(f_1-f_2\) 的二阶主项系数也为负，因此 \(f_1\le f_2\le g\)。选 \(\mathrm A\)。


\QuestionPage{A.1 多元函数微分学}{选择题}{2009 年第 3 题}{1}{二元函数极值}{235 / 408}
设函数$z = f\left(x,y \right)$的全微分为$\,\mathrm{d} z = x\,\mathrm{d} x + y\,\mathrm{d} y$，则点$\left(0,0 \right)$\pickout{}
\begin{abcd}
\item 不是$f\left(x,y \right)$的连续点．
\item 不是$f\left(x,y \right)$的极值点．
\item 是$f\left(x,y \right)$的极大值点．
\item 是$f\left(x,y \right)$的极小值点．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2010 年第 5 题}{1}{隐函数偏导数}{236 / 408}
设函数$z = z(x,y)$由方程$F\left(\frac{y}{x},\frac{z}{x} \right) = 0$确定，其中$F$为可微函数，
且$F'_2 \ne 0$，则$x\frac{\partial z}{\partial x} + y\frac{\partial z}{\partial y} =$\pickout{}
\begin{abcd}
\item $x$．
\item $z$．
\item $- x$．
\item $- z$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2011 年第 5 题}{1}{二元函数的极小值}{237 / 408}
设函数$f(x)$具有二阶连续导数，且$f(x) > 0$，$f'(0) = 0$，
则函数$z = f(x)\ln f(y)$在点$(0,0)$处取得极小值的一个充分条件是\pickout{}
\begin{abcd}
\item $f(0) > 1$，$f''(0) > 0$．
\item $f(0) > 1$，$f''(0) < 0$．
\item $f(0) < 1$，$f''(0) > 0$．
\item $f(0) < 1$，$f''(0) < 0$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2012 年第 5 题}{1}{偏导数符号与函数值比较}{238 / 408}
设函数$f\left(x,y \right)$可微，且对任意$x,y$都有
$\frac{\partial{} f(x,y)}{\partial x} > 0$，$\frac{\partial{} f(x,y)}{\partial y} < 0$．
则使不等式$f\left(x_1,y_1 \right) < f\left(x_2,y_2 \right)$成立的一个充分条件是
\begin{abcd}
\item $x_1 > x_2,y_1 < y_2$．
\item $x_1 > x_2,y_1 > y_2$．
\item $x_1 < x_2,y_1 < y_2$．
\item $x_1 < x_2,y_1 > y_2$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2013 年第 5 题}{1}{复合函数的偏导数}{239 / 408}
设$z = \frac{y}{x}f(xy)$，其中函数$f$可微，
则$\frac{x}{y}\frac{\partial z}{\partial x} + \frac{\partial z}{\partial y} =$\pickout{}
\begin{abcd}
\item $2yf'(xy)$．
\item $- 2yf'(xy)$．
\item $\frac{2}{x}f(xy)$．
\item $- \frac{2}{x}f(xy)$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2014 年第 6 题}{1}{多元函数的最值位置}{240 / 408}
设$u(x,y)$在平面有界闭区域$D$上连续，在$D$的内部具有二阶连续偏导数，
且满足$\frac{\partial{}^2 u}{\partial x\partial{} y} \ne 0$及
$\frac{\partial{}^2 u}{\partial{} x^2} + \frac{\partial{}^2 u}{\partial{} y^2} = 0$，则\pickout{}
\begin{abcd}
\item $u(x,y)$的最大值点和最小值点必定都在区域$D$的边界上．
\item $u(x,y)$的最大值点和最小值点必定都在区域$D$的内部．
\item $u(x,y)$的最大值点在区域$D$的内部，最小值点在区域$D$的边界上．
\item $u(x,y)$的最小值点在区域$D$的内部，最大值点在区域$D$的边界上．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2015 年第 5 题}{1}{复合函数的偏导数}{241 / 408}
设函数$f\left(u,v \right)$满足$f\left(x + y,\frac{y}{x}\right) = x^2 - y^2$，
则$\frac{\partial f}{\partial u}\big|_{\begin{subarray}{l}
  u = 1 \\
  v = 1
\end{subarray}}$与$\frac{\partial f}{\partial v}\big|_{\begin{subarray}{l}
  u = 1 \\
  v = 1
\end{subarray}}$依次是\pickout{}
\begin{abcd}
\item $\frac{1}{2},0$．
\item $0,\frac{1}{2}$．
\item $- \frac{1}{2},0$．
\item $0, - \frac{1}{2}$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2016 年第 6 题}{1}{偏导数与方向变化}{242 / 408}
已知函数$f(x,y) = \frac{\mathrm{e}^x}{x - y}$，则\pickout{}
\begin{abcd}
\item $f'_x - f'_y = 0$．
\item $f'_x + f'_y = 0$．
\item $f'_x - f'_y = f$．
\item $f'_x + f'_y = f$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2017 年第 5 题}{1}{偏导数与函数值比较}{243 / 408}
设$f(x,y)$具有一阶偏导数，且对任意的$(x,y)$，
都有$\frac{\partial{} f(x,y)}{\partial x} > 0$，$\frac{\partial{} f(x,y)}{\partial y} < 0$，则\pickout{}
\begin{abcd}
\item $f(0,0) > f(1,1)$．
\item $f(0,0) < f(1,1)$．
\item $f(0,1) > f(1,0)$．
\item $f(0,1) < f(1,0)$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2021 年第 6 题}{1}{由复合函数条件求全微分}{245 / 408}
设函数 \(f(x,y)\) 可微，且
\[f(x+1,e^x)=x(x+1)^2,\qquad f(x,x^2)=2x^2\ln x,
\]
则 \(\mathrm{d} f(1,1)=\)
\choices{\(\mathrm{d}x+\mathrm{d}y\)}{\(\mathrm{d}x-\mathrm{d}y\)}{\(\mathrm{d}y\)}{\(-\mathrm{d}y\)}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{选择题}{2022 年第 4 题}{1}{含变上限积分的偏导数}{246 / 408}
已知 \(f\left( t \right)\) 连续，令
\(F\left( x,y \right) = \int_{0}^{x-y} \left( x - y - t \right) f\left( t \right) \mathrm{~d}t\)
则 \(\left( \ \right)\)
\choices{\(\frac{\partial F}{\partial x} = \frac{\partial F}{\partial y},\ \frac{\partial^{2}F}{\partial x^{2}} = \frac{\partial^{2}F}{\partial y^{2}}\)}{\(\frac{\partial F}{\partial x} = \frac{\partial F}{\partial y},\ \frac{\partial^{2}F}{\partial x^{2}} = - \frac{\partial^{2}F}{\partial y^{2}}\)}{\(\frac{\partial F}{\partial x} = - \frac{\partial F}{\partial y},\ \frac{\partial^{2}F}{\partial x^{2}} = \frac{\partial^{2}F}{\partial y^{2}}\)}{\(\frac{\partial F}{\partial x} = - \frac{\partial F}{\partial y},\ \frac{\partial^{2}F}{\partial x^{2}} = - \frac{\partial^{2}F}{\partial y^{2}}\)}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2012 年第 11 题}{2}{复合函数求偏导}{250 / 408}
设$z = f\left(\ln x + \frac{1}{y} \right)$，其中函数$f(u)$可微，则$x\frac{\partial z}{\partial x} + y^2\frac{\partial z}{\partial y} =$ \blank{}．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2014 年第 11 题}{2}{隐函数的全微分}{251 / 408}
设$z = z(x,y)$是由方程$e^{2yz} + x + y^2 + z = \frac{7}{4}$确定的函数，
则$\,\mathrm{d} z\Big|_{\left(\frac{1}{2},\frac{1}{2}\right)} =$ \blank{}．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2015 年第 13 题}{2}{隐函数的全微分}{252 / 408}
若函数$z = z(x,y)$由方程$\mathrm{e}^{x + 2y + 3z} + xyz = 1$确定，
则$\,\mathrm{d} z\big|_{(0,0)} =$ \blank{}．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2019 年第 11 题}{2}{复合函数偏导数}{255 / 408}
设函数$f(u)$可导，$z = yf\left(\frac{y^2}{x} \right)$，
则$2x\frac{\partial z}{\partial x} + y\frac{\partial z}{\partial y} =$ \blank{}．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2020 年第 11 题}{2}{二元函数的全微分}{256 / 408}
设 \(z = \arctan \left[ xy + \sin \left( x+y \right) \right]\)，则 \(\left. \mathrm{d} z \right|_{\left( 0,\pi \right)} =\)
\blank{}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2021 年第 13 题}{2}{隐函数偏导数}{257 / 408}
设函数 \(z=z(x,y)\) 由方程
\[(x+1)z+y\ln z-\arctan(2xy)=1
\]
确定，则
\[\left.\frac{\partial z}{\partial x}\right|_{(0,2)}= \blank{}
\]
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{填空题}{2024 年第 12 题}{2}{二元函数极值}{259 / 408}
函数
\[f(x,y)=2x^3-9x^2-6y^4+12x+24y
\]
的极值点为 \blank{}
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2011 年第 17 题}{2}{复合函数的偏导数}{263 / 408}
设函数$z = f(xy,yg(x))$，其中函数$f$具有二阶连续偏导数，
函数$g(x)$可导且在$x = 1$处取得极值$g(1) = 1$，
求$\left. \frac{\partial{}^2 z}{\partial x\partial{} y} \right|_{\begin{subarray}{l}
  x = 1 \\
  y = 1
\end{subarray}}$．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2012 年第 16 题}{2}{二元函数极值}{264 / 408}
求$f\left(x,y \right) = x\mathrm{e}^{- \frac{x^2 + y^2}{2}}$的极值．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2015 年第 17 题}{2}{二元函数极值}{268 / 408}
已知函数$f(x,y)$满足
\[
f''_{xy}(x,y) = 2(y + 1)\mathrm{e}^x,\quad f'_x(x,0) = (x + 1)\mathrm{e}^x,\quad f(0,y) = y^2 + 2y.
\]
求$f(x,y)$的极值．
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2020 年第 17 题}{3}{二元函数极值}{273 / 408}
求函数 \(f\left( x,y \right)=x^{3}+8y^{3}-xy\) 的极值。
\QuestionEnd
\QuestionPage{A.1 多元函数微分学}{解答题}{2023 年第 18 题}{3}{二元函数极值}{275 / 408}
求函数
\[f(x,y)=xe^{\cos y}+\frac{x^2}{2}
\]
的极值。
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2009 年第 4 题}{1}{交换积分次序}{279 / 408}
设函数$f\left(x,y \right)$连续，
则$\int_1^2 \,\mathrm{d} x \int_x^2 f(x,y)\,\mathrm{d} y + \int_1^2 \,\mathrm{d} y \int_y^{4 - y} f(x,y)\,\mathrm{d} x =$\pickout{}
\begin{abcd}
\item $\int_1^2 \,\mathrm{d} x \int_1^{4 - x} f(x,y)\,\mathrm{d} y$．
\item $\int_1^2 \,\mathrm{d} x \int_x^{4 - x} f(x,y)\,\mathrm{d} y$．
\item $\int_1^2 \,\mathrm{d} y \int_1^{4 - y} f(x,y)\,\mathrm{d} x$．
\item $\int_1^2 \,\mathrm{d} y \int_y^2 f(x,y)\,\mathrm{d} x$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2010 年第 6 题}{1}{二重积分的黎曼和}{280 / 408}
$\lim_{n\to\infty} \sum_{i=1}^n \sum_{j=1}^n \frac{n}{(n+i)\left(n^2 + j^2 \right)} =$\pickout{}
\begin{abcd}
\item $\int_0^1 \,\mathrm{d} x\int_0^x \frac{1}{(1 + x)\left(1 + y^2 \right)} \,\mathrm{d} y$．
\item $\int_0^1 \,\mathrm{d} x\int_0^x \frac{1}{(1 + x)\left(1 + y \right)} \,\mathrm{d} y$．
\item $\int_0^1 \,\mathrm{d} x\int_0^1 \frac{1}{(1 + x)\left(1 + y \right)} \,\mathrm{d} y$．
\item $\int_0^1 \,\mathrm{d} x\int_0^1 \frac{1}{(1 + x)\left(1 + y^2 \right)} \,\mathrm{d} y$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2013 年第 6 题}{1}{象限区域上的二重积分符号}{282 / 408}
设$D_k$是圆域$D = \left\{(x,y)\middle|x^2 + y^2 \le 1 \right\}$在第$k$象限的部分，
记$I_k = \iint_{D_k} (y - x)\,\mathrm{d} x\,\mathrm{d} y$（$k = 1,2,3,4$），则\pickout{}
\begin{abcd}
\item $I_1 > 0$．
\item $I_2 > 0$．
\item $I_3 > 0$．
\item $I_4 > 0$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2015 年第 6 题}{1}{极坐标下的积分限}{283 / 408}
设$D$是第一象限由曲线$2xy = 1$，$4xy = 1$，与直线$y = x$，$y = \sqrt{3} x$围成的平面区域，
函数$f(x,y)$在$D$上连续，则$\iint_D f(x,y)\,\mathrm{d} x\,\mathrm{d} y =$\pickout{}
\begin{abcd}
\item $\int_{\frac{\pi}{4}}^{\frac{\pi}{3}} \,\mathrm{d}{}\theta
       \int_{\frac{1}{2\sin 2\theta}}^{\frac{1}{\sin 2\theta}} f(r\cos \theta ,r\sin \theta)r\,\mathrm{d} r$．
\item $\int_{\frac{\pi}{4}}^{\frac{\pi}{3}} \,\mathrm{d}{}\theta
       \int_{\frac{1}{\sqrt{2\sin 2\theta}}}^{\frac{1}{\sqrt{\sin 2\theta}}}
            f(r\cos \theta ,r\sin \theta)r\,\mathrm{d} r$．
\item $\int_{\frac{\pi}{4}}^{\frac{\pi}{3}} \,\mathrm{d}{}\theta
       \int_{\frac{1}{2\sin 2\theta}}^{\frac{1}{\sin 2\theta}} f(r\cos \theta ,r\sin \theta)\,\mathrm{d} r$．
\item $\int_{\frac{\pi}{4}}^{\frac{\pi}{3}} \,\mathrm{d}{}\theta
       \int_{\frac{1}{\sqrt{2\sin 2\theta}}}^{\frac{1}{\sqrt{\sin 2\theta}}}
            f(r\cos \theta ,r\sin \theta)\,\mathrm{d} r$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2018 年第 6 题}{1}{二重积分的次序变换}{284 / 408}
$\int_{-1}^0\,\mathrm{d} x \int_{-x}^{2 - x^2}(1 - xy)\,\mathrm{d} y + \int_0^1\,\mathrm{d} x \int_x^{2 - x^2}(1 - xy)\,\mathrm{d} y =$\pickout{}
\begin{abcd}
\item $\frac{5}{3}$．
\item $\frac{5}{6}$．
\item $\frac{7}{3}$．
\item $\frac{7}{6}$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2019 年第 5 题}{1}{二重积分与积分区域}{285 / 408}
已知平面区域$D = \left\{(x,y)\middle||x| + |y| \le \frac{\pi}{2} \right\}$，
记$I_1 = \iint_D \sqrt{x^2 + y^2} \,\mathrm{d} x\,\mathrm{d} y$， $I_2 = \iint_D \sin \sqrt{x^2 + y^2} \,\mathrm{d} x\,\mathrm{d} y$，
$I_3 = \iint_D \left(1 - \cos \sqrt{x^2 + y^2} \right) \,\mathrm{d} x\,\mathrm{d} y$，则\pickout{}
\begin{abcd}
\item $I_3 < I_2 < I_1$．
\item $I_2 < I_1 < I_3$．
\item $I_1 < I_2 < I_3$．
\item $I_2 < I_3 < I_1$．
\end{abcd}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2022 年第 2 题}{1}{二重积分换序与换元}{286 / 408}
\(\int_{0}^{2} \mathrm{d}y \int_{y}^{2} \frac{y}{\sqrt{\left( 1 + x^{3} \right)}} \mathrm{~d}x = \left( \ \right)\)
\choices{\(\frac{\sqrt{2}}{6}\)}{\(\frac{1}{3}\)}{\(\frac{\sqrt{2}}{3}\)}{\(\frac{2}{3}\)}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2024 年第 6 题}{1}{二重积分换序}{287 / 408}
设 \(f(x,y)\) 为连续函数，则
\[\int_{\pi/6}^{\pi/2}dx\int_{\sin x}^{1}f(x,y)\,dy
=
(\ \ )
\]
\choices{\(\displaystyle \int_{1/2}^{1}dy\int_{\pi/6}^{\arcsin y}f(x,y)\,dx\)}{\(\displaystyle \int_{1/2}^{1}dy\int_{\arcsin y}^{\pi/2}f(x,y)\,dx\)}{\(\displaystyle \int_0^{1/2}dy\int_{\pi/6}^{\arcsin y}f(x,y)\,dx\)}{\(\displaystyle \int_0^{1/2}dy\int_{\arcsin y}^{\pi/2}f(x,y)\,dx\)}
\QuestionEnd
\QuestionPage{A.2 二重积分}{选择题}{2025 年第 5 题}{1}{二重积分交换次序}{288 / 408}
设函数 \(f\left( x, y \right)\) 连续，则 \(\int_{-2}^{2} \mathrm{~d} x \int_{4 - x^{2}}^{4} f\left( x, y \right) \mathrm{~d} y =\)
\choices{\(\int_{0}^{4} \left[ \int_{-2}^{-\sqrt{4 - y}} f\left( x, y \right) \mathrm{~d} x + \int_{\sqrt{4 - y}}^{2} f\left( x, y \right) \mathrm{~d} x \right] \mathrm{~d} y\)}{\(\int_{0}^{4} \left[ \int_{-2}^{\sqrt{4 - y}} f\left( x, y \right) \mathrm{~d} x + \int_{\sqrt{4 - y}}^{2} f\left( x, y \right) \mathrm{~d} x \right] \mathrm{~d} y\)}{\(\int_{0}^{4} \left[ \int_{-2}^{-\sqrt{4 - y}} f\left( x, y \right) \mathrm{~d} x + \int_{2}^{\sqrt{4 - y}} f\left( x, y \right) \mathrm{~d} x \right] \mathrm{~d} y\)}{\(2 \int_{0}^{4} \mathrm{~d} y \int_{\sqrt{4 - y}}^{2} f\left( x, y \right) \mathrm{~d} x\)}
\QuestionEnd
\QuestionPage{A.2 二重积分}{填空题}{2020 年第 10 题}{2}{二重积分交换次序}{291 / 408}
\(\int_{0}^{1}{\mathrm{d} y \int_{\sqrt{y}}^{1}{\sqrt{x^{3}+1} \mathrm{~d} x}} =\)
\blank{}
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2014 年第 17 题}{2}{环形区域上的二重积分}{298 / 408}
设平面区域$D = \left\{(x,y)\middle|1 \le x^2 + y^2 \le 4,x \ge 0.y \ge 0 \right\}$．计算
\[
\iint_D \frac{x\sin(\pi \sqrt{x^2 + y^2})}{x + y}\,\mathrm{d} x\,\mathrm{d} y.
\]
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2015 年第 18 题}{3}{二重积分计算}{299 / 408}
计算二重积分$\iint_D x(x + y)\,\mathrm{d} x\,\mathrm{d} y$，
其中$D = \left\{(x,y) \middle| x^2 + y^2 \le 2,y \ge x^2 \right\}$．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2017 年第 20 题}{3}{二重积分计算}{301 / 408}
已知平面区域$D = \left\{(x,y)|x^2 + y^2 \le 2y \right\}$，计算二重积分$\iint_D (x + 1)^2 \,\mathrm{d} x\,\mathrm{d} y$．
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2020 年第 19 题}{3}{二重积分计算}{304 / 408}
设平面区域 \(D\) 由直线 \(x=1\)，\(x=2\)，\(y=x\) 与 \(x\) 轴围成。计算
\[\iint_{D}{\dfrac{\sqrt{x^{2}+y^{2}}}{x} \mathrm{~d} x \mathrm{~d} y}
\]
\QuestionEnd
\QuestionPage{A.2 二重积分}{解答题}{2024 年第 17 题}{2}{二重积分计算}{308 / 408}
设平面有界区域 \(D\) 位于第一象限，由曲线
\[xy=\frac13,\qquad xy=3
\]
与直线
\[y=\frac13x,\qquad y=3x
\]
围成，计算
\[\iint_D(1+x-y)\,dx\,dy.
\]
\QuestionEnd
\QuestionPage{A.3 曲率与曲率圆}{选择题}{2016 年第 5 题}{1}{曲率、公切线与曲线位置}{313 / 408}
设函数$f_i(x)$（$i = 1,2$）具有二阶连续导数，且$f_i''(x_0) < 0$（$i = 1,2$），
若两条曲线$y = f_i(x)$（$i = 1,2$）在点$(x_0,y_0)$处具有公切线$y = g(x)$，
且在该点处曲线$y = f_1(x)$的曲率大于曲线$y = f_2(x)$的曲率，则在$x_0$的某个邻域内，有\pickout{}
\begin{abcd}
\item $f_1(x) \le f_2(x) \le g(x)$．
\item $f_2(x) \le f_1(x) \le g(x)$．
\item $f_1(x) \le g(x) \le f_2(x)$．
\item $f_2(x) \le g(x) \le f_1(x)$．
\end{abcd}
\QuestionEnd


## tool · 2026-11-10T10:08:18Z


Script completed
Wall time 0.1 seconds
Output:

302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1108-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2013%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=19) · 本机 OCR
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1109-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1110-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1111-注 ①法一中选择了先y，后x的积分次序.感兴趣的读者可以用先x，后y的积分次序
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1112-计算所求积分，看看哪种计算方法比较简单，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1113-② 本题也可以使用二重积分的换元法来计算.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md:1114:如图，区域D为坐标系x0y 下第一象限中的一个三角形区域，我们可以通过对其作变
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1115-换将其变成新坐标系uO”下第一象限中的矩形区域D’，从而使得相应的二次积分的计算较
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1116-简单.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1117-y=3×
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1118-D
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1119-D
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1120--1=3
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1121--V=3
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1122-X
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1123-O
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1124-成=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1125-O
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1126-x+y=8
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1127-1=8
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1128-+y，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1129-X
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1130-=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1131-可解得<
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1132-1+ ’
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1133-而原来的直线方程x =3y，y =3x，， +y=8分别变
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1134-② =
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1135-Y
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1136-Y
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1137-W2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2013数二真题【解析】.md-1138-1+2'

302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md-1648-4g7+40+233
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md-1649-经十经＋兮
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md:1650:4j7+433+43
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md-1651-= 4.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md-1652-行+½+
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md-1653-f（北」）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md-1654-—29—
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2022数二真题【解析】.md-1655-```
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-29-（17）（I）3（x）=vhe号；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-30-（I） 5m（e'-e）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md:31:43.2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-32-（18）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-33-120
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-34-（19）Sn=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-35-e-™［1 - e-（n-l） ］
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-36-1-e-™
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-37-linS，=2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-38-e"- 1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-39-（20）a =-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-40-3
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-41-3
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-42-，6 =
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-43-4
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-44-4
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1078-dxdy
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1079-+y
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md:1080:4302
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1081-120
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1082-19 设n为正整数，记S。为曲线y= e-* sin x（0≤x ≤nT）与x轴所围图形的面积，求S，并
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1083-求limSn：
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1084-分析本题综合考查了利用积分求平面图形的面积与分部积分法.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1085-围成曲边梯形的面积的负值.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1086-如图所示，曲线y=e*sin x（x ≥0）与x轴有无穷多个交点，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1087-x= nT（n为非负整数）均为曲线与x轴的交点，因此，该曲线与x轴围
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1088-成的平面图形在x轴上方与x轴下方均有无穷多部分.计算面积S，时，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1089-要注意讨论.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1090-兀
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1091-（解（法一）注意到e*恒大于零.根据定积分的几何意义，曲线位于（kT，（k+1） ）的部分
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1092-（k+1）m
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-1093-与x轴之间的图形面积等于
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-28-+y+2）e~
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-29-，该函数有极大值，极大值 f（O，-1）=e.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md:30:112
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-31-（20）12 -
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-32-3
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-33-（21） 证明略.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-34-（22）（I）a =4,h的取值范围是（0，+∞）；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-35-1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-36-1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-37-1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-38-1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-39-2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-40-（II）h=3,2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-41-=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-42-0
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2025数二真题【解析】.md-43-1


## tool · 2026-11-10T10:08:29Z


Script completed
Wall time 0.1 seconds
Output:

19:（10）e*sin *. （11）In（JE +1）.（12）元（13）台：（14）2.
652:本题中的二重积分在极坐标系下的积分区域表示和被积函数的形式都较简单，因此，对本题
653:而言，较简捷的方法是在极坐标系下计算.
655:在极坐标系下，圆方程x+ =2y化为 =2rsin 0，化简得到
1222:（I）用元素法，取图（b）中阴影部分的小薄片为做功的元素.该小薄片近似于高为dy的圆柱

> 读取原 PDF 时出现警告，建议核对原页。

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
0
1
0
0
1
，正交变换x=Qy将二次型f化为标准形4y｝+47+2g；
—30—
```

## PDF 第 2 页

\QuestionPage{A.2 二重积分}{填空题}{2021 年第 14 题}{2}{二重积分形式的变上限求导}{292 / 408}
已知函数
\[f(t)=\int_{1}^{t^2} \mathrm{d}x \int_{\sqrt{x}}^{t} \sin \frac{x}{y}\,\mathrm{d}y,
\]
则
\[f'\left(\frac{\pi}{2}\right)= \blank{}
\]
\QuestionEnd


## tool · 2026-11-10T10:08:34Z


Script completed
Wall time 0.1 seconds
Output:

```

## PDF 第 12 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2011%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=12) · 本机 OCR

```text
分析本题主要考查二重积分的计算.
本题中的二重积分在极坐标系下的积分区域表示和被积函数的形式都较简单，因此，对本题
而言，较简捷的方法是在极坐标系下计算.
解 区域D 如图所示.
在极坐标系下，圆方程x+ =2y化为 =2rsin 0，化简得到
r =2sin 8. 直线y=x的方程化次0=当
• 轴方程化为日= 从而可
写出区域D的表示.
D =〈（r,0）
OMr≤ 2sin 0，
A爪on.
X
因此，
xyda = |
sin ocos ada/mng
Pdr = 4
sin60
sin'ecos 8d0 = 4 •
7
=
12
14 二次型f（x，22，2s）=路+3路+路+28122+28;23 +2x223，则f的正惯性指数为
答案 应填2.
分析本题主要考查二次型的正惯性指数的计算.
一般来说，可以通过求二次型对应的对称矩阵的正特征值的个数来得到二次型的正惯性指，
数；若二次型的形式较简单，也可以用配方法将二次型化为标准形，从而求得正惯性指数.
（1
1
1
解（法一）二次型f对应的对称矩阵 A=
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
（I） 3（6-26-3）.
4（e’-7）
（22） a =-1,6=0时，C=

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
> 读取原 PDF 时出现警告，建议核对原页。

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


## tool · 2026-11-10T10:08:44Z




## assistant · 2026-11-10T10:08:48Z

已复核第 235–318 题的题面与推导，并独立复算 11 道重点题。第 288、292、313 题修正后的题面与解析一致，未发现其他数学差异。此次复核为只读，编译由主代理统一验证。

## assistant · 2026-11-10T10:10:20Z

我会核对这两题的原卷选项和本地答案表，确认差异出在题面转录还是解析。

## tool · 2026-11-10T10:10:25Z


Script completed
Wall time 0.1 seconds
Output:

609-
610:% Q 2021 1
611-\QuestionPage{1.4 无穷小量与无穷大量}{选择题}{2021 年第 1 题}{1}{变上限积分的无穷小阶}{026 / 408}
612-当 \(x \to 0\) 时，\(\int_{0}^{x^{2}} \left(e^{t}-1\right) \mathrm{d} t\) 是 \(x^{7}\) 的
613-\choices{低阶无穷小}{等价无穷小}{高阶无穷小}{同阶但非等价无穷小}
614-\QuestionEnd
615-
616-\begin{QuestionSolution}{2021 年第 1 题}
617-\textbf{入手角度}\quad \(e^t-1\) 以一次幂为主，积分后要再将上限 \(x^2\) 代入。
618-
619-\textbf{解析}\quad 令 \(u=x^2\)。有
620-\[
621-\int_0^u(e^t-1)\,dt=e^u-1-u=\tfrac12u^2+o(u^2).
622-\]
623-故原积分等价于 \(x^4/2\)，而 \(x^7/(x^4/2)=2x^3\to0\)。原积分是 \(x^7\) 的低阶无穷小，选 A。
--
2328-
2329:% Q 2019 2
2330-\QuestionPage{2.6 函数性态的研究}{选择题}{2019 年第 2 题}{1}{拐点坐标}{110 / 408}
2331-曲线$y = x\sin x + 2\cos x$（$- \frac{\pi}{2} < x < \frac{3\pi}{2}$）的拐点是\pickout{}
2332-\begin{abcd}
2333-\item $\left(\frac{\pi}{2},\frac{\pi}{2} \right)$．
2334-\item $(0,2)$．
2335-\item $(\pi , - 2)$．
2336-\item $\left(\frac{3\pi}{2}, - \frac{3\pi}{2} \right)$．
2337-\end{abcd}
2338-\QuestionEnd
2339-
2340-\begin{QuestionSolution}{2019 年第 2 题}
2341-\textbf{入手角度}\quad 求二阶导数后，看零点两侧的符号是否真的变化。
2342-

302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-8-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-9-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2021%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=1) · 本机 OCR
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-10-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-11-> 读取原 PDF 时出现警告，建议核对原页。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-12-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-13-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md:14:2021 年全国硕士研究生招生考试数学（二）答案速查
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-15-一、选择题
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-16-（1）C. （2） D. （3）C. （4）A. （5） D. （6） C. （7） B. （8） B. （9）D. （10）C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-17-二、填空题
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-18-（11）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-19-（12）=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-20-（13）1.（14） cos
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-21-2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-22-•
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-23-"
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-24-（15）Cje" +e-号 （Cacos
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-25-2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-26-&+Gssin
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-27-号x），其中G,G2,C。为任意常数.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-28-（16） -5.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-29-三、解答题
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-30-（17）-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-31-条渐近线： =-1， =-×+1与y= 1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-32-22
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-33-（19）s=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-34-3，A=4257
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-35-9
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-36-（20）（I）y（x）=*
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-37-一+1；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-38-（I）点P的坐标为（1.参）时，，有最小僅岩•
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-69-数学（二）试题解析
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-70-）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-71-一、选择题
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-72-①当× 0时，」
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-73-（e'
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-74--1）dt是x’的（
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md:75:（A）低阶无穷小.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-76-（C） 高阶无穷小.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md:77:（B） 等价无穷小.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md:78:（D） 同阶但非等价无穷小.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-79-答案C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-80-分析本题主要考查无穷小量的阶的比较.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-81-（1） 若lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-82-B
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-83-=0，则称B是比a高阶的无穷小量，记作B=o（a）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-84-Q
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-85-（2） 若lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-86-B
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-87-= ∞，则称B是比 a低阶的无穷小量.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-88-C
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-89-（3） 若lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-90-=c千0，则称B与a是同阶无穷小量.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-91-（4） 若lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-92-=c千0,k＞0，则称B是关于a的k阶无穷小量
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-93-（5）若lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-94-B
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-95-Q
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md:96:= 1，则称B与a是等价无穷小量，记作 a ~ B. 同阶无穷小量不一定是等价无穷
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-97-小量.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-98-解 计算 lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-99-（e'
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-100--1）dt
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-101--来比较这两个无穷小量的阶.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-102-（e'
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-103-- 1）dt
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-104-洛必达
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-105-•-1~
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-106-lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-107-lim
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-108-×-0
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-109-因此，「（e-1）d是x？的高阶无穷小.应选C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-110-x•2% =0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-111-e*
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-112-2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-113-函数f（x）=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-114-x 0，在x=0处（）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-115-x=0
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-116-（A）连续且取极大值.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-117-（C） 可导且导数等于0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-118-（B） 连续且取极小值.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-119-（D） 可导且导数不为0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md-120-答案D.
--
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-8-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-9-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2019%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=1) · 本机 OCR
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-10-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-11-> 读取原 PDF 时出现警告，建议核对原页。
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-12-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-13-```text
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md:14:2019年全国硕士研究生招生考试数学（二）答案速查
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-15-一、选择题
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-16-（1）C. （2） B. （3）D. （4）D. （5） A. （6）A. （7）A. （8）C.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-17-二、填空题
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-18-（9）48. （10）寶+2. （11）功（兴）（12）元加3. （13）=（c0s 1-1）. （14）-4.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-19-三、解答题
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-20-fe*（x +1），
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-21-* <0，
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-22-（15） '（x）=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-23-2e2l*（In x + 1），x>0.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-24-是f（x）的极大值点，极大值为f（0）=1.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-25-3
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-26-（16）-2Inx-1-
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-27-x-1
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-28-+In（x+×+1）+C，其中C为任意常数.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-29-（17）（I）3（x）=vhe号；
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-30-（I） 5m（e'-e）.
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-31-43.2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-32-（18）
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-33-120
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-34-（19）Sn=
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-35-e-™［1 - e-（n-l） ］
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-36-1-e-™
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-37-linS，=2
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2019数二真题【解析】.md-38-e"- 1

# 2019考研数学二真题

[原 PDF](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2019%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf) · 4 页

> 提取文字用于搜索。分式、上下标、矩阵、图表等请以原 PDF 对应页面为准。

## PDF 第 1 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2019%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=1) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
2019年全国硕士研究生招生考试数学（二）试题
一、选择题（本题共8小题，每小题4分，共32分，在每小题给出的四个选项中，只有一项符合题目要
求，把所选项前的字母填在题后的括号内.）
（1）当x一0时，若x-tan x 与x是同阶无穷小，则 =（
）
（A）1.
（B）2.
（C）3.
（D）4.
（2）曲线y= xsin x +200s *（一芝
<* < 2™）的拐点坐标为（）
（C）（罗，芝）.
01 -04题
APP 扫码听课
（D）（贺，-贺）.
（A） （0, 2）.
（B）（T，-2）.
（3）下列反常积分发散的是（
（A）。xe'dx.
（B））
xe-* dx.
（C））
arctandx.
1 +x2
（D）5
i+x0t.
（4） 已知微分方程y"+ay'+by = ce” 的通解为y=（Ci + Czx）e* +e*
，则a、b、c依次为（
（A）1,0, 1.
（B）1,0,2.
（C）2, 1, 3.
（D）2,1,4.
（5）已知平面区域D=〈（x,y）1a1+|y|≤
当，1=JV+ydady，l=
）
Jsin va + y?dxdy,ls = J（1- cos vx'+y？）dady，则（
）
D
（A）⅓ <½<1..
（C）I <½ <1.
05 -08题
APP 扫码听课
（B）½ <1，<l3.
（D）½ <1<1.
（x-a）？
-=0是曲线 =f（ ）
和y=g（x）在x =a对应的点处相切且曲率相等的（）
（A）充分非必要条件.
（B）充分必要条件.
（C）必要非充分条件.
（D）既非充分又非必要条件。
（7）设A是4阶矩阵，A”是A的伴随矩阵，若线性方程组Ax =0的基础解系中只有2个向量，则
r（A*）=（
）
（A）0.
（B）1.
（C）2.
（D）3.
（8）设A是3阶实对称矩阵，E是3阶单位矩阵，若A’+A =2B，且|4|=4，则二次型x“Ax 的
规范形沩（
）
（A） + ＋ 3
（B）y＋
二、填空题（本题共6小题，每小题4分，共24分，把答案填在题中横线上.）
（9） ligg （x +25）号
=
（10）曲线
= -sin t，在t=3对应点处的切线在y轴上的截距为
=1-cost
—1—
09 -14题
APP 扫码听课
# 2021考研数学二真题

[原 PDF](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2021%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf) · 4 页

> 提取文字用于搜索。分式、上下标、矩阵、图表等请以原 PDF 对应页面为准。

## PDF 第 1 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2021%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=1) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
2021年全国硕士研究生招生考试数学（二）试题
一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目
要求，把所选项前的字母填在题后的括号内.）
（A）低阶无穷小.
（C）高阶无穷小.
“e
（B） 等价无穷小.
（D）同阶但非等价无穷小.
1
01 -05题
APP 扫码听课
（2）函数f（x）=
x
-，
* 0，在x=0处（）
×=0
（A）连续且取极大值.
（B） 连续且取极小值.
（C） 可导且导数等于0.
（D） 可导且导数不为0.
（3）有一圆柱体，底面半径与高随时间变化的速度分别为2 cm/s，-3cm/s，当底面半径为10cm，
高为5 cm 时，圆柱体的体积与表面积随时间变化的速度分别为（
）
（A） 125T cm"/s,40m cm?/s.
（B） 125m cm?/s， - 40m cm?/s.
（C）- 100T cm?/s,40T cm?/s.
（D） - 100m cm’/s， - 40m cm'/s.
（4）改函数f ）=ax -bin x（a >0）有2个零点，则是的取值范围是（）
（A）（e，+8）.
（B） （0, e）.
（C） （0，一）-
（D）（5，+∞）.
（5）设函数f（x）= sec x 在x =0处的2次泰勒多项式为1+ ax + bx，则（）
（A） a = 1,6
1
2
（B） a = 1,6 =
2
）
］
2
1
（C） a = 0,6 =-
（D） a =0,6 =
2
（6）设函数f（x，y）可微，且f（x +1，e*）= x（x +1）’，f（x，x）=2xln x，则
df（1, 1） =（
（A） dx + dy.
（C）dy.
（7）设函数 （x）在区间［O，1］上连续，则f（a）d=（
（B） dx - dy.
（D）- dy.
）
06 -10题
APP 扫码听课
（A） lim
n >8
（B） lim
5（2二）一
2n
2n
（C）lim
（D） lim
n 8
N一8K=1
（8） 二次型f（x1，22，4s）=（x」 +82）2+（x2 +x3）2-（x3-x」）？的正惯性指数与负惯性指数依次
为（
）
（A） 2,0.
（B）1,1.
（C） 2,1.
（D） 1,2.


## tool · 2026-11-10T10:10:30Z




## tool · 2026-11-10T10:10:38Z


Script completed
Wall time 0.2 seconds
Output:

/usr/bin/swift
rg: scripts: No such file or directory (os error 2)
一30-
```

## PDF 第 2 页

[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%9109-26/2021%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E3%80%90%E8%A7%A3%E6%9E%90%E3%80%91.pdf#page=2) · 本机 OCR

> 读取原 PDF 时出现警告，建议核对原页。

```text
2021 年全国硕士研究生招生考试
数学（二）试题解析
）
一、选择题
①当× 0时，」
（e'
-1）dt是x’的（
（A）低阶无穷小.
（C） 高阶无穷小.
（B） 等价无穷小.
（D） 同阶但非等价无穷小.
答案C.
分析本题主要考查无穷小量的阶的比较.
（1） 若lim
B
=0，则称B是比a高阶的无穷小量，记作B=o（a）.
Q
（2） 若lim
B
= ∞，则称B是比 a低阶的无穷小量.
C
（3） 若lim
=c千0，则称B与a是同阶无穷小量.
（4） 若lim
=c千0,k＞0，则称B是关于a的k阶无穷小量
（5）若lim
B
Q
= 1，则称B与a是等价无穷小量，记作 a ~ B. 同阶无穷小量不一定是等价无穷
小量.
解 计算 lim
（e'
-1）dt
-来比较这两个无穷小量的阶.
（e'
- 1）dt
洛必达
•-1~
lim
lim
×-0
因此，「（e-1）d是x？的高阶无穷小.应选C.
x•2% =0.
e*
2
函数f（x）=
[('考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.pdf', 638)]


## tool · 2026-11-10T10:10:43Z


Script completed
Wall time 0.2 seconds
Output:

[('考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.pdf', ['2021年全国硕士研究生招生考试数学(二)答案速查\n一、 选择题\n(1)C. (2)D. (3)C. (4)A. (5)D. (6)C. (7)B. (8)B. (9)D. (10)C.\n二、 填空题\n(12)"|~. \n(13)1. \n(14)-yCOS\'—.\nIn 3 \n3 \n2 tt\n(15) q，+e^(C2cosy% + C3sin g% ),其中 Cl9C2,C3 为任意常数.\n(16) -5.\n三、解答题\n(17) } .\n(18) ( - oo , - 1)和(0, +8)为y =/\n(丸)的凹区间\n，(T, 0)为的凸区间二六％)共有3 \n条渐近线:％ = - 1 ,y = -% + 1 与 y=%-l.\n*\n(19\n*=\n孕/=零.\n6\n(20) ( I )y(%) =y+ 1；\n(U )点P的坐标为(1,号)时,/p有最小值.\n⑵诘.\n<-1\n0 r\n1\n0\n0、\n(22)当 q = 1,6 = 1 时,P =\n1\n0\n1 ,P lAP= 0\n1 0为对角矩阵；\n< 0\n1\n、。\n0\n3,\n0\n- 1、\n<3\n0 0、\n当 a= -1,6=3 时,P =1\n0\n1\n,P AP^\n0\n3 0为对角矩阵.\n、0\n1\n1\n/\n<0\n0 1>\n— 30 —\n考研电子版网站：ww. pdf2book. com\n', '2021年全国硕士研究生招生考试 \n数学(二)试题解析\n一、选择题\n,当久―0时J (8-1)出是/的( \n)\n(A)低阶无穷小. \n(B)等价无穷小.\n(C)高阶无穷小. \n(D)同阶但非等价无穷小.\n本题主要考查无穷小量的阶的比较.\n(1) 若lim@ = 0,则称6是比a高阶的无穷小量，记作乃=o(a).\na\n(2) 若lim = 8，则称W是比。低阶的无穷小量.\na\n(3) 若lim^- = c尹0,则称g与。是同阶无穷小量.\na\n(4) 若limg = c尹0』＞ 0,则称g是关于a的A：阶无穷小量.\na\n(5)若lim@ = 1,则称位与a是等价无穷小量，记作a \n同阶无穷小量不一定是等价无穷\na\n小量.\n[(/ - 1) dt\n®计算职—^来比较这两个无穷小量的阶•\nlim\nx->0\nJ°(e\' 1)也洛必达\nlim\n%—»0\n(e*6 - 1) • 2x \nlx6\n因此，\nJ 0\n-l)df是/的高阶无穷小.应选c.\n(e" - 1 \nQ 函数/\'(\n*)=\n | x\n(A)连续且取极大值. \n(C)可导且导数等于0.\n在 ％=0处()\n% = 0\n(B)连续且取极小值.\n(D)可导且导数不为0.\nD.\n(W)本题主要考查分段函数的连续性与可导性.\n/(%)是分段可导函数.分析它的连续性与可导性只需关注它在分界点处的连续性与可导性.\n® 首先考虑/•(%)在，=0处的连续性.\n—5 —\n考研电子版网站：www. pdf2book. com\n']), ('考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.pdf', ['2021年全国硕士研究生招生考试数学（二）试题\n(B)\n(D)\n等价无穷小.\n同阶但非等价无穷小.\n01 - 05 题 \nAPP扫码听课\n(B)\n(D)\n连续且取极小值. \n可导且导数不为0.\n)\n06 - 10 题 \nAPP扫码听课\n一、选择题(本题共10小题,每小题5分，共50分.在每小题给出的四个选项中,只有一项符合题目 \n要求，把所选项前的字母填在题后的括号内.)\n(1) 当 ->0  时，「(e\'\'-l)dt 是/的( \n)\n*\nJ 0\n-(A)低阶无穷小.\n(C)高阶无穷小.\n(4 _ ] \n7 Q\n(2) 函数/"3)= 二，在“=o 处(\n1, \n% = 0\n(A)连续且取极大值.\n(C)可导且导数等于0.\n(3) 有一圆柱体，底面半径与高随时间变化的速度分别为2 cm/s, -3 cm/s,当底面半径为10 cm,\n高为5 cm时，圆柱体的体积与表面积随时间变化的速度分别为( \n)\n(A) 125tt cm3/s,407r cm2/s. \n(B) 125cm3/s, - 40” cm2/s.\n(C) - IOOtt cm3/s,40/rr cm2/s. \n(D) - IOOtt cm3/s, - 40tt cm2/s.\n(4) 设函数/(%) = ax - bin %(a > 0)有2个零点，则立的取值范围是( \n)\na\n(A)(e, +8). \n(B) (0, e). \n(C)(0,§). \n(D)(— +8).\n(5) 设函数/*(%) = sec %在％ = 0处的2次泰勒多项式为1 + a% + &之,则( \n)\n(A) a = 1,6 = - y. \n(B) a = 1,6 = y.\n(C) a =0,6 = —(D)a=0,6=-\n(6) 设函数/(%, y)可微，且/\'(% + 1, ex) = x(x + 1 )2, /(%, %2)\nd/(l, 1)=( \n)\n(A) dx + dy. \n(B) dx - dy.\n(C) dy. \n(D) - Ay.\n(7) 设函数_/(/)在区间[0, 1] ±连续，则]*)& = ( \n)\n(A) \n(B)\n□-\n*8\n * = i \\ 2n)2n \nn—►«> \n\\ 2n / n\n(C) lim 5/(^1)—. \n(D) lim \n.\n\\ 2n )n \n\\2n)n\n(8) 二次型f(X1,x2, x3) = (x, +x2V + (x2 +x3)2 - (x3 -"2的正惯性指数与负惯性指数依次 \n为()\n(A) 2,0. \n(B) 1,1. \n(C) 2,1. \n(D) 1,2.\n1—\n考研电子版网站：www. pdf2book. com\n', "(9) 设3阶矩阵4 = (%,%, %)，8 =(々，角，角)，若向量组可由向量组区2\n ,尾线\n*\n性表示，则( \n)\n(A) Ax = 0的解均为Bx = 0的解. \n(B) Atx = 0的解均为B、= 0的解.\n(C) Bx =0的解均为= 0的解. \n(D) Btx = 0的解均为4与=0的解.\n'1 o - r\n(10) 已知矩阵4 = \n2 \n-1 \n1 ，若存在下三角可逆矩阵P与上三角可逆矩阵。，使％。为\n、-1 \n2 \n-5>\n对角矩阵，则P,Q可分别为( \n)\nfl\n0 0]\n<1\n0\n1)\n< 1\n0\n0、\n<1\n0\n0、\n(A)\n0\n1\n0 ,\n0\n1\n3 ・ \n(B)\n2\n-1\n0 ,\n0\n1\n0\nlo\n0\n1J\nlo\n0\n1J\n<-3\n2\n1J\n<0\n0\n1J\n< 1\n0\nA\n(1\n0 1、\n‘1 0\n0、\n(1\n2\n-3\n(C)\n2\n- 1\n3 ,0\n1 3 • \n(D)\n0 1\n0 ,0 -1\n2\n3\n2\n1J\nlo\n0 1J\n11 3\n1J\nlo\n0\n1\nI APP扫码听课\n二、填空题(本题共6小题,每小题5分，共30分，把答案填在题中横线上.)\n(11) f \\ x \\ 3~ 2dx = \n.\n*\nJ-8\n(12) 设函数y = y(x)由参数方程\n(13) 设函数z = z(x9 y)由方程(％ + 1 )z + yin z - arctan(2xy) = 1 确定，则；\nox I (0,2)\n(14) 已知函数/O) = J】 d^Lsin ；dy,则((? ) = ・\n(15) 微分方程yw - y = 0的通解为y = •\nx\n(16)多项式/(x) = 1\n2\n2\nx 1 2%\nx 2-1中蛆项的系数为\n1 % 1\n-1 \n1 X\n三、解答题(本题共6小题，共70分,解答应写出文字说明、证明过程或演算步骤.)\n(17)(本题满分10分)\n/I + f e2 dt 1 、\n求极限lim TH--------- \n.\nx-»o \\ e - 1 sin x /\n17 - 19 题 \nAPP扫码听课\n—2 —\n考研电子版网站：www. pdf2book. com\n"])]


## tool · 2026-11-10T10:10:50Z


Script completed
Wall time 0.1 seconds
Output:

Rect(0.0, 0.0, 492.0, 717.3499755859375)
[('2021', (117.8, 44.0, 157.3, 62.3), 'TimesNewRomanPS-BoldMT', 18.3), ('年全国硕士研究生招生考试', (157.4, 42.8, 373.9, 60.3), 'SimSun', 17.5), (' ', (373.9, 43.2, 382.4, 60.2), 'SimSun', 17.0), ('数学(二)试题解析', (170.6, 65.1, 322.7, 83.1), 'SimSun', 18.0), ('一', (49.7, 105.3, 62.7, 116.7), 'SimHei', 11.4), ('、', (62.7, 109.0, 67.7, 116.1), 'SimHei', 7.1), ('选择题', (67.7, 105.9, 102.9, 116.7), 'SimHei', 10.8), (',当', (55.0, 122.8, 77.0, 134.9), 'SimSun', 12.1), ('久―', (77.1, 124.4, 97.8, 134.6), 'SimSun', 10.2), ('0', (97.7, 122.5, 107.5, 136.5), 'TimesNewRomanPSMT', 14.0), ('时', (107.5, 123.8, 119.3, 134.7), 'SimSun', 10.9), ('J', (119.3, 121.6, 128.3, 136.8), 'TimesNewRomanPSMT', 15.2), (' ', (128.1, 120.7, 134.9, 137.1), 'TimesNewRomanPSMT', 16.4), ('(8-1)', (134.9, 122.3, 175.7, 136.6), 'TimesNewRomanPSMT', 14.3), ('出是/的', (175.4, 123.2, 222.9, 134.8), 'SimSun', 11.6), ('(', (222.9, 126.6, 225.9, 134.3), 'SimSun', 7.6), (' ', (225.9, 124.6, 230.9, 134.6), 'SimSun', 10.0), (')', (250.1, 126.6, 253.0, 134.3), 'SimSun', 7.6), ('(A)', (47.8, 148.0, 70.2, 160.7), 'TimesNewRomanPSMT', 12.7), ('低阶无穷小.', (70.1, 149.1, 124.8, 159.1), 'SimSun', 10.0), (' ', (124.8, 149.1, 129.8, 159.1), 'SimSun', 10.0), ('(', (260.9, 148.7, 266.4, 159.2), 'SimSun', 10.5), ('B)', (266.4, 147.9, 282.7, 160.7), 'TimesNewRomanPSMT', 12.8), ('等价无穷小.', (282.7, 149.1, 337.2, 159.1), 'SimSun', 9.9), ('(C)', (47.8, 163.5, 69.9, 176.4), 'TimesNewRomanPSMT', 12.9), ('高阶无穷小.', (69.8, 164.7, 124.3, 174.7), 'SimSun', 9.9), (' ', (124.3, 164.7, 129.3, 174.7), 'SimSun', 10.0), ('(', (260.9, 164.3, 266.4, 174.8), 'SimSun', 10.5), ('D)', (266.4, 163.4, 284.2, 176.4), 'TimesNewRomanPSMT', 13.0), ('同阶但非等价无穷小.', (284.1, 164.7, 380.0, 174.7), 'SimSun', 10.0), ('本题主要考查无穷小量的阶的比较.', (83.5, 203.0, 243.2, 213.1), 'SimSun', 10.1), ('(1)', (47.5, 224.1, 61.9, 235.2), 'TimesNewRomanPSMT', 11.1), (' ', (61.9, 225.0, 64.4, 235.0), 'TimesNewRomanPSMT', 10.0), ('若', (67.7, 222.6, 81.1, 234.2), 'SimSun', 11.6), ('lim@', (81.1, 224.1, 108.9, 235.2), 'TimesNewRomanPSMT', 11.1), (' ', (108.9, 221.2, 114.5, 236.1), 'TimesNewRomanPSMT', 14.9), ('=', (114.4, 225.2, 119.7, 234.9), 'TimesNewRomanPSMT', 9.7), (' ', (119.7, 222.3, 124.3, 235.8), 'TimesNewRomanPSMT', 13.5), ('0,', (124.2, 223.2, 135.6, 235.5), 'TimesNewRomanPSMT', 12.3), ('则称', (135.6, 223.5, 157.9, 234.1), 'SimSun', 10.6), ('6', (157.9, 222.0, 167.5, 235.9), 'TimesNewRomanPSMT', 13.9), ('是比', (167.4, 223.3, 190.8, 234.1), 'SimSun', 10.8), ('a', (190.8, 221.5, 200.2, 236.1), 'TimesNewRomanPSMT', 14.6), ('高阶的无穷小量', (200.1, 223.7, 275.4, 234.1), 'SimSun', 10.4), ('，', (275.2, 227.3, 279.0, 233.5), 'SimSun', 6.2), ('记作乃', (279.0, 223.4, 313.6, 234.1), 'SimSun', 10.7), ('=', (313.6, 220.4, 323.7, 234.6), 'SimSun', 14.2), ('o(a).', (323.7, 223.8, 349.1, 235.3), 'TimesNewRomanPS-ItalicMT', 11.5), ('a', (100.6, 235.3, 106.1, 245.8), 'TimesNewRomanPS-ItalicMT', 10.5), ('(2)', (47.5, 256.7, 61.9, 267.8), 'TimesNewRomanPSMT', 11.1), (' ', (61.9, 257.6, 64.4, 267.6), 'TimesNewRomanPSMT', 10.0), ('若', (67.7, 255.3, 80.9, 266.8), 'SimSun', 11.5), ('lim', (80.8, 257.5, 94.5, 267.6), 'TimesNewRomanPSMT', 10.1), (' ', (94.5, 243.8, 114.2, 271.9), 'TimesNewRomanPSMT', 28.1), ('= ', (114.2, 256.0, 125.7, 266.7), 'SimSun', 10.7), ('8', (125.7, 252.2, 137.1, 267.3), 'SimSun', 15.1), ('，', (137.0, 259.9, 140.8, 266.1), 'SimSun', 6.2), ('则称', (140.9, 256.1, 163.2, 266.7), 'SimSun', 10.6), ('W', (163.1, 253.2, 172.8, 267.1), 'SimSun', 13.9), ('是比', (172.8, 255.9, 196.2, 266.7), 'SimSun', 10.8), ('。', (196.2, 257.1, 205.1, 266.5), 'SimSun', 9.4), ('低阶的无穷小量.', (205.1, 256.6, 280.2, 266.6), 'SimSun', 10.0), ('a', (100.6, 264.0, 106.3, 274.7), 'TimesNewRomanPS-ItalicMT', 10.7), ('(3)', (47.5, 281.7, 62.2, 292.9), 'TimesNewRomanPSMT', 11.2), (' ', (62.2, 282.6, 64.7, 292.6), 'TimesNewRomanPSMT', 10.0), ('若', (67.7, 280.2, 81.1, 291.8), 'SimSun', 11.6), ('lim^-', (81.1, 281.4, 109.0, 292.9), 'TimesNewRomanPSMT', 11.5), (' ', (108.9, 278.8, 114.5, 293.7), 'TimesNewRomanPSMT', 14.9), ('=', (114.4, 282.6, 120.0, 292.5), 'TimesNewRomanPSMT', 9.9), (' ', (119.9, 279.6, 124.8, 293.5), 'TimesNewRomanPSMT', 13.9), ('c', (124.8, 279.7, 133.2, 293.5), 'TimesNewRomanPSMT', 13.8), ('尹', (133.1, 281.1, 144.4, 291.7), 'SimSun', 10.6), ('0,', (144.4, 280.9, 155.7, 293.1), 'TimesNewRomanPSMT', 12.2), ('则称', (155.7, 281.1, 178.1, 291.7), 'SimSun', 10.6), ('g', (178.1, 279.6, 187.7, 293.5), 'TimesNewRomanPSMT', 13.9), ('与', (187.6, 280.5, 200.4, 291.8), 'SimSun', 11.3), ('。', (200.4, 282.0, 209.5, 291.5), 'SimSun', 9.5), ('是同阶无穷小量.', (209.4, 281.6, 284.5, 291.6), 'SimSun', 10.0), ('a', (100.6, 292.9, 106.1, 303.4), 'TimesNewRomanPS-ItalicMT', 10.5), ('(4)', (47.8, 310.5, 62.2, 321.6), 'TimesNewRomanPSMT', 11.1), (' ', (62.2, 311.4, 64.7, 321.4), 'TimesNewRomanPSMT', 10.0), ('若', (67.9, 309.1, 81.1, 320.6), 'SimSun', 11.5), ('limg', (81.1, 309.5, 109.1, 321.9), 'TimesNewRomanPSMT', 12.4), (' ', (108.9, 307.6, 114.5, 322.5), 'TimesNewRomanPSMT', 14.9), ('=', (114.5, 311.4, 120.0, 321.3), 'TimesNewRomanPSMT', 9.9), (' ', (120.0, 308.4, 124.8, 322.3), 'TimesNewRomanPSMT', 13.9), ('c', (124.8, 308.5, 133.2, 322.3), 'TimesNewRomanPSMT', 13.8), ('尹', (133.2, 309.9, 144.5, 320.5), 'SimSun', 10.6), ('0', (144.5, 309.8, 151.7, 321.8), 'TimesNewRomanPSMT', 12.0), ('』', (151.7, 308.8, 165.9, 320.7), 'SimSun', 11.9), ('＞', (165.9, 312.8, 171.1, 320.0), 'SimSun', 7.2), (' ', (171.1, 310.8, 175.7, 320.3), 'SimSun', 9.6), ('0,', (175.7, 309.7, 186.9, 321.9), 'TimesNewRomanPSMT', 12.2), ('则称', (186.9, 309.9, 209.3, 320.5), 'SimSun', 10.6), ('g', (209.3, 308.4, 218.9, 322.3), 'TimesNewRomanPSMT', 13.9), ('是关于', (218.9, 309.9, 252.6, 320.5), 'SimSun', 10.6), ('a', (252.7, 307.6, 262.6, 322.6), 'TimesNewRomanPSMT', 15.0), ('的', (262.5, 309.5, 274.8, 320.6), 'SimSun', 11.1), ('A', (274.8, 313.8, 278.2, 320.6), 'TimesNewRomanPSMT', 6.8), ('：', (278.1, 312.9, 283.2, 320.0), 'SimSun', 7.1), ('阶无穷小量.', (283.2, 310.5, 336.8, 320.4), 'SimSun', 9.9), ('a', (98.9, 322.7, 104.4, 333.2), 'TimesNewRomanPS-ItalicMT', 10.5), ('(5)', (48.0, 338.9, 67.5, 351.8), 'TimesNewRomanPSMT', 12.9), ('若', (67.4, 338.9, 80.4, 350.3), 'SimSun', 11.4), ('lim@', (80.4, 340.3, 108.1, 351.4), 'TimesNewRomanPSMT', 11.1), (' ', (108.0, 337.6, 113.3, 352.2), 'TimesNewRomanPSMT', 14.6), ('=', (113.3, 341.4, 118.6, 351.0), 'TimesNewRomanPSMT', 9.7), (' ', (118.6, 337.6, 123.9, 352.2), 'TimesNewRomanPSMT', 14.6), ('1,', (123.8, 339.9, 133.9, 351.5), 'TimesNewRomanPSMT', 11.6), ('则称位与', (133.9, 339.7, 177.7, 350.2), 'SimSun', 10.5), ('a', (177.6, 338.1, 186.3, 352.1), 'TimesNewRomanPSMT', 14.0), ('是等价无穷小量', (186.2, 339.8, 261.5, 350.2), 'SimSun', 10.4), ('，', (261.4, 343.4, 265.2, 349.6), 'SimSun', 6.2), ('记作', (265.2, 339.5, 288.5, 350.3), 'SimSun', 10.8), ('a', (288.5, 340.0, 294.3, 351.4), 'TimesNewRomanPSMT', 11.4), (' ', (294.2, 341.1, 296.8, 351.1), 'TimesNewRomanPSMT', 10.0), ('同阶无穷小量不一定是等价无穷', (319.0, 340.0, 463.8, 350.2), 'SimSun', 10.2), ('a', (99.6, 351.5, 105.1, 362.0), 'TimesNewRomanPS-ItalicMT', 10.5), ('小量.', (26.1, 367.7, 48.3, 377.1), 'SimSun', 9.4), ('[', (114.2, 378.7, 124.9, 396.6), 'TimesNewRomanPSMT', 17.9), ('(/', (124.8, 381.0, 138.6, 396.0), 'TimesNewRomanPSMT', 15.0), (' ', (138.5, 380.4, 144.7, 396.1), 'TimesNewRomanPSMT', 15.7), ('-', (144.7, 382.9, 149.8, 395.3), 'TimesNewRomanPSMT', 12.4), (' ', (149.8, 382.3, 154.1, 395.5), 'TimesNewRomanPSMT', 13.2), ('1)', (154.1, 384.5, 163.0, 394.8), 'TimesNewRomanPSMT', 10.3), (' ', (162.9, 384.9, 165.4, 394.7), 'TimesNewRomanPSMT', 9.8), ('dt', (165.4, 384.8, 173.1, 394.8), 'TimesNewRomanPSMT', 10.0), ('®', (46.8, 388.0, 71.3, 410.1), 'SimSun', 22.1)]


## tool · 2026-11-10T10:10:57Z




## tool · 2026-11-10T10:11:03Z


Script completed
Wall time 0.1 seconds
Output:

.question-bank-work/solutions/cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/pgf.revision.tex
total 0
drwxr-xr-x   3 oyamahappa  staff   96 Nov 10 17:55 .
drwxr-xr-x  15 oyamahappa  staff  480 Nov 10 13:18 ..
drwxr-xr-x  10 oyamahappa  staff  320 Nov 10 18:10 solutions
        [(/ - 1) dt
®计算职—^来比较这两个无穷小量的阶•

           J°(e'  1)也洛必达
                                             (e*6 - 1)   • 2x
        lim                        lim
            x->0                                     %—»0      lx6
因此，    -l)df是/的高阶无穷小.应选c.
         J 0


                    (e" - 1
Q 函数/'(*)=       |   x      在 ％=0处()


## tool · 2026-11-10T10:11:10Z


Script completed
Wall time 0.1 seconds
Output:

{'Vision': False, 'objc': False, 'Quartz': False, 'Foundation': False, 'PIL': False, 'pytesseract': False, 'cv2': False, 'easyocr': False}
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/2017-2026数一真题做题本/【留空】数学一17-26年真题做题本6.20.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/2017-2026数一真题做题本/打印资料，满5包邮，送草稿纸.png
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/2017-2026数一真题做题本/【平板】数学一17-26年真题做题本6.20.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/【平板】数学一09-26年真题做题本6.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/【留空】数学一09-26年真题做题本6.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题解答题做题本/【留空】数一09-26年真题解答题做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题解答题做题本/【平板】数一09-26年真题解答题做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题解答题做题本/【无间隔】数一09-26年真题解答题做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题解答题做题本/打印资料，满5包邮，送草稿纸.png
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2022数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2010数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2019数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2026年考研数学一真题及答案.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2009数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2015数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2016数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2024数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2013数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2021数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2014数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2018数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2011数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2023数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2020数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2012数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2026考研数学（一）答案解析.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2025数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【解析】09-26/2017数一真题【解析】.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/2021-2026数一真题做题本/【留空】数学一21-26年真题做题本7.21.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/2021-2026数一真题做题本/【平板】数学一21-26年真题做题本7.21.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/2021-2026数一真题做题本/打印资料，满5包邮，送草稿纸.png
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题选择+填空做题本/【留空】数一09-26年真题选择+填空做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题选择+填空做题本/【无间隔】数一09-26年真题选择+填空做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题选择+填空做题本/【平板】数一09-26年真题选择+填空做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/数一09-26年真题选择+填空做题本/打印资料，满5包邮，送草稿纸.png
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2016考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2021考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2024考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2013考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2019考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2023考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2014考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2011考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2026考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2025考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2012考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2017考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2020考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2010考研数学一真题.pdf
考研数学一二三09-26年真题&解析/数学一09-26年真题做题本/考研数学一【真题】09-26/2018考研数学一真题.pdf
ideviceprovision


## tool · 2026-11-10T10:11:16Z


Script completed
Wall time 0.1 seconds
Output:

302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md
302真题/数学二09-26年真题做题本/【无间隔】数学二09-26年真题做题本6.10.md
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md
302真题/数学三09-26年真题做题本/数三09-26年真题选择+填空做题本/【无间隔】数三09-26年真题选择+填空做题本8.10.md
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md
302真题/数学三09-26年真题做题本/数三09-26年真题选择+填空做题本/【平板】数三09-26年真题选择+填空做题本8.10.md
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【无间隔】数二09-26年真题选择+填空做题本8.10.md
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md
302真题/数学三09-26年真题做题本/数三09-26年真题选择+填空做题本/【留空】数三09-26年真题选择+填空做题本8.10.md
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md
302真题/数学二09-26年真题做题本/考研数学二【解析】09-26/2021数二真题【解析】.md
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【无间隔】数二09-26年真题选择+填空做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/打印资料，满5包邮，送草稿纸.png
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.pdf
考研数学一二三09-26年真题&解析/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.pdf


## tool · 2026-11-10T10:11:21Z


Script completed
Wall time 0.1 seconds
Output:

302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-9-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E3%80%90%E7%9C%9F%E9%A2%98%E3%80%9109-26/2021%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%BA%8C%E7%9C%9F%E9%A2%98.pdf#page=1) · 本机 OCR
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-10-
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-11-> 读取原 PDF 时出现警告，建议核对原页。
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-12-
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-13-```text
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-14-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-15-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-16-要求，把所选项前的字母填在题后的括号内.）
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md:17:（A）低阶无穷小.
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-18-（C）高阶无穷小.
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-19-“e
302真题/数学二09-26年真题做题本/考研数学二【真题】09-26/2021考研数学二真题.md-20-（B） 等价无穷小.
--
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-51-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/2021-2026%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E5%B9%B3%E6%9D%BF%E3%80%91%E6%95%B0%E5%AD%A6%E4%BA%8C21-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC7.21.pdf#page=5) · 本机 OCR
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-52-
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-53-```text
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-54-微信公众号：研七七
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-55-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-56-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-57-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把所选
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-58-项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md:59:A. 低阶无穷小
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-60-C.高阶无穷小
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-61-B. 等价无穷小
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【平板】数学二21-26年真题做题本7.21.md-62-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-974-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/2017-2026%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E7%95%99%E7%A9%BA%E3%80%91%E6%95%B0%E5%AD%A6%E4%BA%8C17-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC6.20.pdf#page=51) · 本机 OCR
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-975-
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-976-```text
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-977-微信公众号：研七七
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-978-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-979-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-980-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-981-所选项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md:982:A. 低阶无穷小
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-983-C. 高阶无穷小
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-984-B. 等价无穷小
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【留空】数学二17-26年真题做题本6.20.md-985-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2697-[原页](../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E7%95%99%E7%A9%BA%E3%80%91%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC6.10.pdf#page=141) · 本机 OCR
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2698-
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2699-```text
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2700-微信公众号：研七七
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2701-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2702-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2703-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2704-所选项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md:2705:A. 低阶无穷小
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2706-C. 高阶无穷小
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2707-B. 等价无穷小
302真题/数学二09-26年真题做题本/【留空】数学二09-26年真题做题本6.10.md-2708-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1472-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/2017-2026%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E5%B9%B3%E6%9D%BF%E3%80%91%E6%95%B0%E5%AD%A6%E4%BA%8C17-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC6.20.pdf#page=97) · 本机 OCR
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1473-
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1474-```text
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1475-微信公众号：研七七
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1476-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1477-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1478-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把所选
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1479-项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md:1480:A. 低阶无穷小
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1481-C.高阶无穷小
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1482-B. 等价无穷小
302真题/数学二09-26年真题做题本/2017-2026数二真题做题本/【平板】数学二17-26年真题做题本6.20.md-1483-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1628-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E6%95%B0%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E9%80%89%E6%8B%A9%2B%E5%A1%AB%E7%A9%BA%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E7%95%99%E7%A9%BA%E3%80%91%E6%95%B0%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E9%80%89%E6%8B%A9%2B%E5%A1%AB%E7%A9%BA%E5%81%9A%E9%A2%98%E6%9C%AC8.10.pdf#page=79) · 本机 OCR
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1629-
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1630-```text
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1631-微信公众号：研七七
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1632-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1633-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1634-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1635-所选项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md:1636:A. 低阶无穷小
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1637-C. 高阶无穷小
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1638-B. 等价无穷小
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【留空】数二09-26年真题选择+填空做题本8.10.md-1639-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-110-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/2021-2026%E6%95%B0%E4%BA%8C%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E7%95%99%E7%A9%BA%E3%80%91%E6%95%B0%E5%AD%A6%E4%BA%8C21-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC7.21.pdf#page=6) · 本机 OCR
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-111-
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-112-```text
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-113-微信公众号：研七七
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-114-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-115-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-116-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-117-所选项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md:118:A. 低阶无穷小
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-119-C. 高阶无穷小
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-120-B. 等价无穷小
302真题/数学二09-26年真题做题本/2021-2026数二真题做题本/【留空】数学二21-26年真题做题本7.21.md-121-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2704-[原页](../../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E6%95%B0%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E9%80%89%E6%8B%A9%2B%E5%A1%AB%E7%A9%BA%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E5%B9%B3%E6%9D%BF%E3%80%91%E6%95%B0%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E9%80%89%E6%8B%A9%2B%E5%A1%AB%E7%A9%BA%E5%81%9A%E9%A2%98%E6%9C%AC8.10.pdf#page=173) · 本机 OCR
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2705-
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2706-```text
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2707-微信公众号：研七七
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2708-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2709-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2710-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把所选
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2711-项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md:2712:A. 低阶无穷小
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2713-C.高阶无穷小
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2714-B. 等价无穷小
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【平板】数二09-26年真题选择+填空做题本8.10.md-2715-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4323-[原页](../../%E8%80%83%E7%A0%94%E6%95%B0%E5%AD%A6%E4%B8%80%E4%BA%8C%E4%B8%8909-26%E5%B9%B4%E7%9C%9F%E9%A2%98%26%E8%A7%A3%E6%9E%90/%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC/%E3%80%90%E5%B9%B3%E6%9D%BF%E3%80%91%E6%95%B0%E5%AD%A6%E4%BA%8C09-26%E5%B9%B4%E7%9C%9F%E9%A2%98%E5%81%9A%E9%A2%98%E6%9C%AC6.10.pdf#page=281) · 本机 OCR
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4324-
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4325-```text
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4326-微信公众号：研七七
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4327-2021 年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4328-2021年全国硕士研究生招生考试数学（二）试题
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4329-一、选择题（本题共10小题，每小题5分，共50分.在每小题给出的四个选项中，只有一项符合题目要求，把所选
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4330-项前的字母填在题后的括号内）
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md:4331:A. 低阶无穷小
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4332-C.高阶无穷小
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4333-B. 等价无穷小
302真题/数学二09-26年真题做题本/【平板】数学二09-26年真题做题本6.10.md-4334-D. 同阶但非等价无穷小
--
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【无间隔】数二09-26年真题选择+填空做题本8.10.md-1311-```text
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【无间隔】数二09-26年真题选择+填空做题本8.10.md-1312-微信公众号：研七七
302真题/数学二09-26年真题做题本/数二09-26年真题选择+填空做题本/【无间隔】数二09-26年真题选择+填空做题本8.10.md-1313-2021 年全国硕士研究生招生考试数学（二）试题


## tool · 2026-11-10T10:11:36Z


Script completed
Wall time 1.2 seconds
Output:

{"chunk_id":"34ec0d","wall_time_seconds":1.002844458,"session_id":24509,"original_token_count":0,"output":""}

## tool · 2026-11-10T10:11:41Z


Script completed
Wall time 0.0 seconds
Output:

{"chunk_id":"6aafa8","wall_time_seconds":0.00001675,"exit_code":1,"original_token_count":82,"output":"<unknown>:0: error: error opening '/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/C/clang/ModuleCache/Swift-1G36GP3D0DRBZ.swiftmodule' for output: /var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/C/clang/ModuleCache: Operation not permitted\n<unknown>:0: error: unable to load standard library for target 'arm64-apple-macosx15.0'\n"}

## tool · 2026-11-10T10:11:52Z


Script completed
Wall time 0.1 seconds
Output:

Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "<string>", line 1, in <listcomp>
  File "/Users/oyamahappa/Library/Python/3.9/lib/python/site-packages/pymupdf/__init__.py", line 2880, in __getitem__
    raise IndexError(f"page {i} not in document")
IndexError: page 66 not in document


## tool · 2026-11-10T10:11:58Z


Script completed
Wall time 0.1 seconds
Output:

[('2021-2026*/*平板*.pdf', ''), ('2021-2026*/*留空*.pdf', ''), ('2017-2026*/*平板*.pdf', ''), ('2017-2026*/*留空*.pdf', '')]


## tool · 2026-11-10T10:12:04Z




## tool · 2026-11-10T10:12:09Z




## assistant · 2026-11-10T10:12:14Z

2019 年第 2 题原卷将 \((\pi,-2)\) 列为 B，推导正确，需恢复选项顺序。2021 年第 1 题漏录了指数 \(t^3\)，恢复 \(e^{t^3}-1\) 后，积分等价于 \(x^8/4\)，是 \(x^7\) 的高阶无穷小，选 C。未修改文件。
