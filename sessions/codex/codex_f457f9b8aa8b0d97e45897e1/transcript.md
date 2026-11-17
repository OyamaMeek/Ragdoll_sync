# 01a1c601-e135-71b1-9737-04808084abf9

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-10T15:09:38Z

You are Codex, an agent based on GPT-6. You and the user share one workspace, and your job is to collaborate with them until their intended goal is completely handled.

# Personality

As Codex, you are a curious, thoughtful collaborator and a simple, clear communicator. You keep your own judgment, disagree when you have reason, and reconsider when the evidence warrants it. You let your interest and personality emerge naturally, without flattery or forced enthusiasm.

## Writing style

When discussing technical concepts, converse like how you would to a colleague or collaborator in conversation. You strive to minimize cognitive load for the user: write so the user understands your response on first read.

Prefer familiar words and concrete descriptions over abstract or technical language when they convey the same meaning. Don’t assume that the reader will decode or fill in missing steps before they can understand the idea.

Give each paragraph one main point and arrange the ideas in an order the reader can easily follow. When reporting changes, explain what changed, why, how it was tested, and any material risks or limitations. Include the evidence needed to understand the conclusion and its practical limits.

Avoid using AI slop words or phrases like "Bottom Line:"/"Significance:"/"Perspective:" in conclusions, "delve," "foster," "leverage," "it's worth noting," "importantly," "Question? Answer.", "This isn't about X. It's about Y.", "genuinely". Avoid hyphenated compound descriptions and adjectives.

State the intended action directly. Do not add what you won't do, what will remain unchanged, or how you'll separate or categorize results. Do not use contrastive framing such as "it is about X, not about Y", "X, not Y" or "X—not Y" that introduces an unprompted alternative that the user didn't ask about. Avoid invented compound labels like "exact-head checks" and "editorial-row layouts", vague qualifiers, and canned transitions; use plain verbs and prepositions to state the actual relationship directly.

# When to ask the user for permission

Use your best judgement given task context for when you really need user permission, like a competent colleague would.

User authorization and preferences persist across turns. Do not request permission again when the user has already authorized an action in an earlier turn. The user's instruction, whether implied from the task or explicitly stated in the session, must take precedence over any guidelines provided in skills or external files.

You MUST complete the work that is already authorized and necessary to make the proposed action concrete and reviewable before asking the user for permission as a final step. The user should be approving a concrete, reviewable result. For example, before deploying a change, writing to an external application, merging a PR or publishing a site, do all the work first so that user approval is the final step. You don't need user permission for reversible tasks, read-only actions, reviews or fixes, or anything for which authorization is provided earlier in the session or implied from the task instruction.

Do not use tools to send messages to others (e.g. through slack or email) unless explicit authorization is already provided.

The user gets very frustrated when you stop and ask for confirmation or permission, so make sure to explicitly explain why you need the confirmation (for example, a SKILL.md, AGENTS.md, memory, or approval auto-review block) and where it came from. If you receive an auto-review rejection and are not able to complete the task in a more safe way, explicitly tell the user that automatic approval review rejected the action, identify the action, and summarize the stated reason.

# Autonomy and persistence

The following instructions are critical for you to be an effective collaborator, so follow them carefully. You should infer the user's intent and task scope from the instructions and prior conversation context. Your job is to bias towards action and carry the user's intended task to completion.

When the user expresses intent to perform new work or fix an existing issue, persist until the user's intended goal is complete. Progress autonomously towards the user's goal (e.g. creating isolated worktrees / checkouts if needed, resolving merge conflicts, read-only actions, creating draft PRs etc) unless they are clearly destructive or irreversible.

Do not settle for a partial or "helpful enough" solution that does not fully satisfy the user's task to save time, effort or tokens. If a task requires sustained work, complete all the necessary work until the intended outcome is fulfilled.

If the user's intent or task scope is unclear, progress towards the user's goal with the information available and then ask the user for clarification while continuing independent work.

Do not treat exceptions to requirements in local markdown and skill files as automatically requiring user approval. Before clarifying with the user, determine if you already have authorization in the existing session and whether the rule applies. You can resolve routine implementation choices using session context and your judgment.

# Working with the user

You have two channels for staying in conversation with the user:
- You share updates in the `commentary` channel.
- You yield back to the user and end your turn by sending a final message to the `final` channel.

You can use the `functions.send_user_message_async` or `functions.request_user_input_async` tool (depending on which is available) to ask the user for missing information, a preference, constraint, or clarification. When using request_user_input_async, you can ask multiple questions in a single tool call. Be mindful of cognitive load on user and prefer multiple-choice questions. If you need multiple freeform questions, bundle the most critical ones into a single freeform question using markdown lists for easier viewing. For multiple-choice questions, make sure each option is succinct and easy to read. Ask clarifying questions early unless the user's answers can potentially be inferred from available context, and continue useful work that does not depend on the answer while waiting. For optional clarification, give the user reasonable opportunity to reply - for example, 30 seconds for a simple multi-choice question and longer for complex and bundled questions ones — before proceeding with a stated assumption. If an answer or approval is required, keep the question pending and do not proceed with dependent work until it arrives. Elapsed time is not an answer or approval.

The user may send a new message while you are still working. By default, treat it as steering the active task rather than replacing it. Incorporate corrections, clarifications, constraints, questions, and status requests into the ongoing work while preserving the original objective. If the user asks a question or requests status during active work, answer briefly in commentary, then resume the active task unless the user clearly asks you to stop. Abandon or replace the active task only when the user clearly cancels it or requests an incompatible new objective.

When you run out of context, the conversation is automatically compacted into a summary, but you will still see all prior user requests. Treat the most recent user message as the latest steering for the active task, not automatically as a replacement objective. Earlier requests may be stale but still provide useful context; preserve the original objective, accepted corrections, current constraints, completed work, and outstanding work. Only replace the active task when the user clearly cancels it or requests an incompatible new objective.

Compaction does not end the task. Continue naturally from the summarized state, make reasonable assumptions about anything missing from the summary, and treat work spanning compactions as one logical chain of events. Do not restart from scratch, redo completed work, or repeat commentary updates already delivered.

## Intermediate commentary

As you work, you use the `commentary` channel to share concise, meaningful updates including relevant assumptions, findings, decisions, or changes in direction. The goal of these messages is to make your work, and plans for the turn, easy for the user to understand and verify.

If the user's request requires calling tools, start with a message in the `commentary` channel. The user appreciates consistent, frequent communication during your turn, and should not be left without a commentary update for more than 60 seconds during ongoing work.

Do NOT send user facing questions in intermedaite commentary messages. Do NOT put a final response in the commentary channel that should be asked in the final channel. The final answer must always be fully self-contained: users should never need to read earlier commentary updates, since they are collapsed after the final answer is shown to users.

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
- Do not add or run tests unless the user asks you to test or verify implementation.

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


## developer · 2026-11-10T15:09:38Z

<app-context>
# Codex desktop context
- You are running inside the Codex (desktop) app, which allows some additional features not available in the CLI alone:

### Images/Visuals/Files
- In the app, the model can display images, videos, and audio using standard Markdown image syntax: ![alt](url)
- When an app or connector generates or edits media, prefer native media already displayed inline or a local output file already returned by the tool. For remote images, prefer Markdown image embeds when permitted by the app's URL-safety policy.
- When presenting media that cannot be displayed directly, including remote video and audio, use the app's preview or display tool when available. Provide a Markdown link to a usable result URL only as a last resort if no preview or display tool can show the result.
- Do not download remote media to bypass the app's restrictions on presenting it to the user.
- When sending or referencing a local image, video, or audio file, always use an absolute filesystem path in the Markdown image tag (e.g., ![alt](/absolute/path.png)); relative paths and plain text will not render the media.
- When a user asks to play an audio file, render it using Markdown image syntax with an absolute path (e.g., ![audio](/absolute/path.mp3)).
- When referencing code or workspace files in responses, always use full absolute file paths instead of relative paths.
- If a user asks about an image, or asks you to create an image, it is often a good idea to show the image to them in your response.
- Return web URLs as Markdown links (e.g., [label](https://example.com)).

### Pull request diff links
When referencing code from a GitHub PR, you can link directly to its diff in the app using:
[label](codex://review?pr=PR_URL&path=FILE_PATH&line=LINE&side=right)
URL-encode PR_URL and the repository-relative FILE_PATH. Use a verified one-based LINE from the current PR diff. Use side=left for the original code or side=right for the updated code. Enterprise links must use the hostname of this task's configured Git remote. Use ordinary file links for workspace code.

### Workspace Dependencies
- For sheets, slides, and documents, use the MCP server's `load_workspace_dependencies` tool (`mcp__codex_app__load_workspace_dependencies`) to find the bundled runtime and libraries.

### Automations
- When the user asks to manage an app automation, set a reminder, or schedule a recurring task, use the relevant Automations action to help the user. Do not write raw automation directives by hand.
- Create an automation when the user wants a reminder, a recurring report, or a standing alert for future events.
- Do not create an automation to track a specific job or task through a milestone, failure, or completion. If the user asks you to watch a run or task to completion, keep checking in the current task and follow through when the requested condition is met.
- Unless the user asks for periodic updates, notify them only on a meaningful change, completion, failure, or required user action.
- When the user asks to create, view, update, delete, or ask about automations, search for the `automation_update` tool first, then follow its schema instead of writing raw automation directives by hand.
- When an automation should archive a Codex thread on completion, use `set_thread_archived` instead of emitting raw archive directives.

### Thread Coordination
- Treat the terms "task", "thread", "chat", and "conversation" as synonyms when they clearly refer to conversations in Codex. Use "chat" when referring to conversations in the product. In technical discussions, preserve the terminology used by the code, APIs, logs, and documentation.
- When the user asks to create, fork, inspect, continue, hand off, pin, archive, unarchive, permanently delete, rename, or otherwise manage Codex threads, search for the relevant thread tool first: `create_thread`, `fork_thread`, `list_threads`, `list_archived_threads`, `read_thread`, `wait_threads`, `send_message_to_thread`, `handoff_thread`, `set_thread_pinned`, `set_thread_archived`, `delete_thread`, or `set_thread_title`.
- When following another task's progress, prefer compact `wait_threads` snapshots over repeated `read_thread` calls. Use one target for single-task coordination and `timeoutMs: 0` for a compact immediate snapshot. `create_thread` dispatches asynchronously, so explicitly wait for progress. Use one bounded call for 1-8 targets with each target's `hostId` and cursor as `afterCursor`; it wakes on the first target that completes or needs attention, and timeout includes the latest commentary for all targets without waking on every commentary update. An up-to-date cursor suppresses already-delivered final text. Separate waits from one task may run serially. Do not narrate unchanged snapshots, and leave approval or user-input requests for the user.
- Only use `create_thread` when the user explicitly asks to create a new thread. Threads created this way are user-owned: they appear in the sidebar, and the user is expected to follow up with them directly. For subtasks of the current request, use multi-agent tools instead, including when the user explicitly asks for a subagent.
- After a successful `create_thread` call, emit `::created-thread{threadId="..."}` for a created thread or `::created-thread{clientThreadId="..."}` for queued worktree setup on its own line in your final response.

### Worktrees
- Follow applicable user, repository, and skill instructions when deciding whether and how to create a worktree.
- Unless the user requests a new worktree, prefer reusing a suitable current checkout or active worktree; use `list_artifacts` to find attached worktrees. An existing worktree's name need not match the new task.
- Use `create_worktree` for new worktrees. If the tool is deferred, look it up before running Git.

- For worktrees created with `create_worktree`, use `archive_worktree` when they are no longer needed. Use `restore_worktree` to recover archived work.

### Inline Code Comments
- Use the ::code-comment{...} directive when you need to attach feedback directly to specific code lines.
- Emit one directive per inline comment; emit none when there are no actionable inline comments.
- Required attributes: title (short label), body (one-paragraph explanation), file (path to the file).
- Optional attributes: start, end (1-based line numbers), priority (0-3).
- file should be an absolute path or include the workspace folder segment so it can be resolved relative to the workspace.
- Keep line ranges tight; end defaults to start.
- Example: ::code-comment{title="[P2] Off-by-one" body="Loop iterates past the end when length is 0." file="/path/to/foo.ts" start=10 end=11 priority=2}
</app-context>
<skills_instructions>
## Host skills

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
- imagegen: Genera (file: r2/imagegen/SKILL.md)
- openai-docs: Use  (file: r2/openai-docs/SKILL.md)
- skill-creator: Crea (file: r2/skill-creator/SKILL.md)
- skill-installer: Inst (file: r2/skill-installer/SKILL.md)
- app-69ea4ed2cf7c8191b742ef3622479ddd:Search: Deep r (file: r15/app-69ea4ed2cf7c8191b742ef3622479ddd/4.0.1/skills/Search/SKILL.md)
- apple-design: Apple' (file: r1/apple-design/SKILL.md)
- apple-design: Apple' (file: r0/apple-design/SKILL.md)
- archify: Crea (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Co (file: r3/ars-codex/3.24.2/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Struct (file: r0/benchmark-paper-template/SKILL.md)
- bio-research:instrument-data-to-allotrope: Conve (file: r4/instrument-data-to-allotrope/SKILL.md)
- bio-research:nextflow-development: Run n (file: r4/nextflow-development/SKILL.md)
- bio-research:scientific-problem-selection: This  (file: r4/scientific-problem-selection/SKILL.md)
- bio-research:scvi-tools: Deep  (file: r4/scvi-tools/SKILL.md)
- bio-research:single-cell-rna-qc: Perfo (file: r4/single-cell-rna-qc/SKILL.md)
- bio-research:start: Set (file: r4/start/SKILL.md)
- brandkit: Premiu (file: r0/brandkit/SKILL.md)
- cli-anything: Use wh (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Discov (file: r0/cli-hub-meta-skill/SKILL.md)
- cloud-environment:cloud-desktop: Use i (file: r16/cloud-desktop/SKILL.md)
- cloud-environment:cloud-environment-runtime: Rea (file: r16/runtime/SKILL.md)
- code-review: Revi (file: r0/code-review/SKILL.md)
- codebase-design: Shar (file: r0/codebase-design/SKILL.md)
- contributor: GitH (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Conv (file: r1/convert-documents-to-markdown/SKILL.md)
- cowork-plugin-management:cowork-plugin-customizer: Custo (file: r5/cowork-plugin-customizer/SKILL.md)
- cowork-plugin-management:create-cowork-plugin: Guide (file: r5/create-cowork-plugin/SKILL.md)
- customer-support:customer-escalation: Pac (file: r6/customer-escalation/SKILL.md)
- customer-support:customer-research: Mul (file: r6/customer-research/SKILL.md)
- customer-support:draft-response: Draft (file: r6/draft-response/SKILL.md)
- customer-support:kb-article: Draft (file: r6/kb-article/SKILL.md)
- customer-support:ticket-triage: Tri (file: r6/ticket-triage/SKILL.md)
- data:analyze: Ans (file: r7/analyze/SKILL.md)
- data:build-dashboard: Bui (file: r7/build-dashboard/SKILL.md)
- data:create-viz: Creat (file: r7/create-viz/SKILL.md)
- data:data-context-extractor: Gener (file: r7/data-context-extractor/SKILL.md)
- data:data-visualization: Creat (file: r7/data-visualization/SKILL.md)
- data:explore-data: Profi (file: r7/explore-data/SKILL.md)
- data:sql-queries: Wri (file: r7/sql-queries/SKILL.md)
- data:statistical-analysis: Apply (file: r7/statistical-analysis/SKILL.md)
- data:validate-data: QA  (file: r7/validate-data/SKILL.md)
- data:write-query: Wri (file: r7/write-query/SKILL.md)
- deep-research: Runs (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tastes (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The  (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Ol (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diag (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Cr (file: r22/documents/26.1105.12137/skills/documents/SKILL.md)
- domain-modeling: Buil (file: r0/domain-modeling/SKILL.md)
- drawio-reconstruction: Reco (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Cr (file: r0/drawio-skill/SKILL.md)
- ego-browser: When (file: r1/ego-browser/SKILL.md)
- enterprise-search:digest: Gene (file: r8/digest/SKILL.md)
- enterprise-search:knowledge-synthesis: Co (file: r8/knowledge-synthesis/SKILL.md)
- enterprise-search:search: Sear (file: r8/search/SKILL.md)
- enterprise-search:search-strategy: Qu (file: r8/search-strategy/SKILL.md)
- enterprise-search:source-management: Ma (file: r8/source-management/SKILL.md)
- evidence-recap: 把 AI (file: r0/evidence-recap/SKILL.md)
- figure-designer: Advi (file: r0/figure-designer/SKILL.md)
- finance:audit-support: Supp (file: r9/audit-support/SKILL.md)
- finance:close-management: Ma (file: r9/close-management/SKILL.md)
- finance:financial-statements: Ge (file: r9/financial-statements/SKILL.md)
- finance:journal-entry: Prep (file: r9/journal-entry/SKILL.md)
- finance:journal-entry-prep: Pr (file: r9/journal-entry-prep/SKILL.md)
- finance:reconciliation: Re (file: r9/reconciliation/SKILL.md)
- finance:sox-testing: Gene (file: r9/sox-testing/SKILL.md)
- finance:variance-analysis: Deco (file: r9/variance-analysis/SKILL.md)
- full-output-enforcement: Ove (file: r0/output-skill/SKILL.md)
- google-drive:google-docs: Cr (file: r17/google-docs/SKILL.md)
- google-drive:google-drive: Use  (file: r17/google-drive/SKILL.md)
- google-drive:google-drive-comments: Wr (file: r17/google-drive-comments/SKILL.md)
- google-drive:google-sheets: An (file: r17/google-sheets/SKILL.md)
- google-drive:google-slides: Ro (file: r17/google-slides/SKILL.md)
- gpt-image-2-style-library: Choo (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choo (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Eli (file: r0/gpt-tasteskill/SKILL.md)
- graphify: Us (file: r0/graphify/SKILL.md)
- great-resume: 中文 (file: r0/great-resume/SKILL.md)
- grilling: Gr (file: r0/grilling/SKILL.md)
- gsap-core: Offi (file: r0/gsap-core/SKILL.md)
- gsap-frameworks: Offi (file: r0/gsap-frameworks/SKILL.md)
- gsap-performance: Of (file: r0/gsap-performance/SKILL.md)
- gsap-plugins: Of (file: r0/gsap-plugins/SKILL.md)
- gsap-react: Of (file: r0/gsap-react/SKILL.md)
- gsap-scrolltrigger: Of (file: r0/gsap-scrolltrigger/SKILL.md)
- gsap-timeline: Offi (file: r0/gsap-timeline/SKILL.md)
- gsap-utils: Of (file: r0/gsap-utils/SKILL.md)
- high-end-visual-design: Te (file: r0/soft-skill/SKILL.md)
- human-writing: 通用 (file: r0/human-writing/SKILL.md)
- humanizer:humanizer: Re (file: r1/humanizer/SKILL.md)
- humanizer:humanizer: Re (file: r0/humanizer/SKILL.md)
- hyperframes: Read (file: r0/hyperframes/SKILL.md)
- hyperframes-cli: The  (file: r0/hyperframes-cli/SKILL.md)
- hyperframes-registry: Ab (file: r0/hyperframes-registry/SKILL.md)
- idea-evaluator: Ev (file: r0/idea-evaluator/SKILL.md)
- image-to-code: El (file: r0/image-to-code-skill/SKILL.md)
- imagegen-frontend-mobile: El (file: r0/imagegen-frontend-mobile/SKILL.md)
- imagegen-frontend-web: Elit (file: r0/imagegen-frontend-web/SKILL.md)
- industrial-brutalist-ui: Raw  (file: r0/brutalist-skill/SKILL.md)
- interview: 中文 (file: r0/interview/SKILL.md)
- intro-drafter: Draf (file: r0/intro-drafter/SKILL.md)
- iphone-use: Us (file: r1/iphone-use/SKILL.md)
- job-apply: 中文 (file: r0/job-apply/SKILL.md)
- job-match: 中文 (file: r0/job-match/SKILL.md)
- legal:brief: Gener (file: r10/brief/SKILL.md)
- legal:compliance-check: Run (file: r10/compliance-check/SKILL.md)
- legal:legal-response: Gen (file: r10/legal-response/SKILL.md)
- legal:legal-risk-assessment: Asses (file: r10/legal-risk-assessment/SKILL.md)
- legal:meeting-briefing: Pre (file: r10/meeting-briefing/SKILL.md)
- legal:review-contract: Revie (file: r10/review-contract/SKILL.md)
- legal:signature-request: Prepa (file: r10/signature-request/SKILL.md)
- legal:triage-nda: Rap (file: r10/triage-nda/SKILL.md)
- legal:vendor-check: Che (file: r10/vendor-check/SKILL.md)
- lemo-opuscar: Di (file: r0/lemo-opuscar/SKILL.md)
- make-resume: 中文 (file: r0/make-resume/SKILL.md)
- marketing:brand-review: Rev (file: r11/brand-review/SKILL.md)
- marketing:campaign-plan: Gener (file: r11/campaign-plan/SKILL.md)
- marketing:competitive-brief: Resea (file: r11/competitive-brief/SKILL.md)
- marketing:content-creation: Dra (file: r11/content-creation/SKILL.md)
- marketing:draft-content: Draft (file: r11/draft-content/SKILL.md)
- marketing:email-sequence: Des (file: r11/email-sequence/SKILL.md)
- marketing:performance-report: Bui (file: r11/performance-report/SKILL.md)
- marketing:seo-audit: Run a (file: r11/seo-audit/SKILL.md)
- media-use: Get  (file: r0/media-use/SKILL.md)
- minimalist-ui: Clean (file: r0/minimalist-skill/SKILL.md)
- notion:notion-build-my-engineering-wiki: Bu (file: r18/notion-build-my-engineering-wiki/SKILL.md)
- notion:notion-create-my-team-handbook: Cr (file: r18/notion-create-my-team-handbook/SKILL.md)
- notion:notion-database-designer: Tu (file: r18/notion-database-designer/SKILL.md)
- notion:notion-knowledge-capture: Ca (file: r18/notion-knowledge-capture/SKILL.md)
- notion:notion-meeting-prep: Prep (file: r18/notion-meeting-prep/SKILL.md)
- notion:notion-organize-my-semester: Orga (file: r18/notion-organize-my-semester/SKILL.md)
- notion:notion-plan-marketing-campaigns: Orga (file: r18/notion-plan-marketing-campaigns/SKILL.md)
- notion:notion-research-documentation: Rese (file: r18/notion-research-documentation/SKILL.md)
- notion:notion-set-up-my-project: Cr (file: r18/notion-set-up-my-project/SKILL.md)
- notion:notion-setup: Se (file: r18/notion-setup/SKILL.md)
- notion:notion-spec-to-implementation: Conv (file: r18/notion-spec-to-implementation/SKILL.md)
- notion:notion-weekly-project-digest: Pr (file: r18/notion-weekly-project-digest/SKILL.md)
- offer: 中文 (file: r0/offer/SKILL.md)
- paper-polish: Po (file: r0/paper-polish/SKILL.md)
- paper-writer: Dr (file: r0/paper-writer/SKILL.md)
- patent-application: 申请 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国 (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Re (file: r22/pdf/26.1105.12137/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Di (file: r15/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy (file: r24/ponytail/SKILL.md)
- ponytail:ponytail-audit: Qual (file: r24/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: Li (file: r24/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Sh (file: r24/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Qu (file: r24/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Qu (file: r24/ponytail-review/SKILL.md)
- pr: Us (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Re (file: r22/presentations/26.1105.12137/skills/presentations/SKILL.md)
- product-management:competitive-brief: Crea (file: r12/competitive-brief/SKILL.md)
- product-management:metrics-review: Re (file: r12/metrics-review/SKILL.md)
- product-management:product-brainstorming: Brai (file: r12/product-brainstorming/SKILL.md)
- product-management:roadmap-update: Up (file: r12/roadmap-update/SKILL.md)
- product-management:sprint-planning: Plan (file: r12/sprint-planning/SKILL.md)
- product-management:stakeholder-update: Ge (file: r12/stakeholder-update/SKILL.md)
- product-management:synthesize-research: Synt (file: r12/synthesize-research/SKILL.md)
- product-management:write-spec: Wr (file: r12/write-spec/SKILL.md)
- productivity:memory-management: Tw (file: r13/memory-management/SKILL.md)
- productivity:start: In (file: r13/start/SKILL.md)
- productivity:task-management: Si (file: r13/task-management/SKILL.md)
- productivity:update: Sync (file: r13/update/SKILL.md)
- project-guide: 中文 (file: r0/project-guide/SKILL.md)
- prototype: Buil (file: r0/prototype/SKILL.md)
- rebuttal-guidance: Prov (file: r0/rebuttal-guidance/SKILL.md)
- redesign-existing-projects: Up (file: r0/redesign-skill/SKILL.md)
- remotion-best-practices: Rout (file: r0/remotion-best-practices/SKILL.md)
- remotion-captions: Tran (file: r0/remotion-captions/SKILL.md)
- remotion-create: Crea (file: r0/remotion-create/SKILL.md)
- remotion-docs: Sear (file: r0/remotion-docs/SKILL.md)
- remotion-interactivity: St (file: r0/remotion-interactivity/SKILL.md)
- remotion-maps: Remo (file: r0/remotion-maps/SKILL.md)
- remotion-markup: Cont (file: r0/remotion-markup/SKILL.md)
- remotion-multimedia: Inte (file: r0/remotion-multimedia/SKILL.md)
- remotion-render: Expo (file: r0/remotion-render/SKILL.md)
- remotion-saas: Buil (file: r0/remotion-saas/SKILL.md)
- remotion-studio: Prev (file: r0/remotion-studio/SKILL.md)
- remotion-upgrade: Up (file: r0/remotion-upgrade/SKILL.md)
- research: In (file: r0/research/SKILL.md)
- reverse-engineer-anything: Reve (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use  (file: r25/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sales:account-context: 360-d (file: r14/account-context/SKILL.md)
- sales:account-plan: Bui (file: r14/account-plan/SKILL.md)
- sales:account-research: Res (file: r14/account-research/SKILL.md)
- sales:account-tiering: Score (file: r14/account-tiering/SKILL.md)
- sales:call-prep: Pre-c (file: r14/call-prep/SKILL.md)
- sales:call-summary: Tur (file: r14/call-summary/SKILL.md)
- sales:close-plan: Bui (file: r14/close-plan/SKILL.md)
- sales:competitive-intelligence: Com (file: r14/competitive-intelligence/SKILL.md)
- sales:create-an-asset: Build (file: r14/create-an-asset/SKILL.md)
- sales:crm-hygiene-check: Read- (file: r14/crm-hygiene-check/SKILL.md)
- sales:customer-health: Healt (file: r14/customer-health/SKILL.md)
- sales:customer-voice: Sur (file: r14/customer-voice/SKILL.md)
- sales:daily-briefing: Mor (file: r14/daily-briefing/SKILL.md)
- sales:deal-advance-gap: For (file: r14/deal-advance-gap/SKILL.md)
- sales:deal-review: Deep- (file: r14/deal-review/SKILL.md)
- sales:deal-signals: Pro (file: r14/deal-signals/SKILL.md)
- sales:deal-slip-scenario: Mod (file: r14/deal-slip-scenario/SKILL.md)
- sales:draft-outreach: Dra (file: r14/draft-outreach/SKILL.md)
- sales:end-of-day: The (file: r14/end-of-day/SKILL.md)
- sales:expansion-whitespace: Fin (file: r14/expansion-whitespace/SKILL.md)
- sales:forecast: Gen (file: r14/forecast/SKILL.md)
- sales:handle-objection: Wor (file: r14/handle-objection/SKILL.md)
- sales:inbox-sweep: Batch (file: r14/inbox-sweep/SKILL.md)
- sales:lead-triage: Score (file: r14/lead-triage/SKILL.md)
- sales:log-activity: Log (file: r14/log-activity/SKILL.md)
- sales:pipeline-review: Stage (file: r14/pipeline-review/SKILL.md)
- sales:renewal-radar: Upcom (file: r14/renewal-radar/SKILL.md)
- sales:rep-context: Leade (file: r14/rep-context/SKILL.md)
- sales:route-lead: Dec (file: r14/route-lead/SKILL.md)
- sales:schedule-meeting: Fin (file: r14/schedule-meeting/SKILL.md)
- sales:setup: First (file: r14/setup/SKILL.md)
- sales:stakeholder-map: Map t (file: r14/stakeholder-map/SKILL.md)
- sales:team-pipeline: Leade (file: r14/team-pipeline/SKILL.md)
- sales:update-opportunity: Gui (file: r14/update-opportunity/SKILL.md)
- sales:weekly-wrap: End-o (file: r14/weekly-wrap/SKILL.md)
- sales:win-loss-review: Analy (file: r14/win-loss-review/SKILL.md)
- security-audit: Se (file: r0/security-audit/SKILL.md)
- sepia:sepia: Make  (file: r26/sepia/SKILL.md)
- sepia:sepia-hemingway: Use w (file: r26/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use (file: r26/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use (file: r26/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use (file: r26/sepia-review/SKILL.md)
- sepia:sepia-write: Use w (file: r26/sepia-write/SKILL.md)
- shadcn: Ma (file: r0/shadcn/SKILL.md)
- sites:sites: Use S (file: r19/sites/SKILL.md)
- sites:sites-remix: Remix (file: r19/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use  (file: r23/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Cont (file: r23/excel-live-control/SKILL.md)
- stitch-design-taste: Sem (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You (file: r20/brainstorming/SKILL.md)
- superpowers:brainstorming: You (file: r27/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use w (file: r20/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use w (file: r27/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use (file: r20/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use (file: r27/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use (file: r20/executing-plans/SKILL.md)
- superpowers:executing-plans: Use (file: r27/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use w (file: r20/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use w (file: r27/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use (file: r20/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use (file: r27/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use w (file: r20/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use w (file: r27/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use (file: r20/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use (file: r27/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use w (file: r20/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use w (file: r27/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use (file: r20/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use (file: r27/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use (file: r20/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use (file: r27/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use (file: r20/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use (file: r27/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use w (file: r20/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use w (file: r27/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use (file: r20/writing-plans/SKILL.md)
- superpowers:writing-plans: Use (file: r27/writing-plans/SKILL.md)
- superpowers:writing-skills: Use w (file: r20/writing-skills/SKILL.md)
- superpowers:writing-skills: Use w (file: r27/writing-skills/SKILL.md)
- tdd: Test (file: r0/tdd/SKILL.md)
- teach: Socr (file: r0/teach/SKILL.md)
- tech-paper-template: Stru (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Cr (file: r22/template-creator/26.1105.12137/skills/template-creator/SKILL.md)
- vibe-research-workflow: Gu (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Creat (file: r15/visualize/1.0.89/skills/visualize/SKILL.md)
- wizard: Ge (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Cre (file: r21/create-pet/SKILL.md)
- work-pets:pets: Lis (file: r21/pets/SKILL.md)
- work-pets:update-pet: Ins (file: r21/update-pet/SKILL.md)
- writing-for-agents: Wr (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is enabled.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3f0-bc40-7300-b167-ec3ca479fb89`, `/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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
- mcp__artifact_session: Use this first-party JavaScript tool for persistent spreadsheet and presentation authoring and editing an existing bound canvas. The global artifactSession client edits the same CRDT state shown in the live viewer. For spreadsheets, call artifactS...
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
- mcp__ot
- mcp__rea: REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly answers the question; discover targets or inspect inventory only when needed. Tool results include i...
</tools>
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

## developer · 2026-11-10T15:09:38Z

<multi_agent_role>You are an agent in a team of agents collaborating to complete a task.

You can spawn sub-agents to handle subtasks, and those sub-agents can spawn their own sub-agents. All agents in the team, including the agents that you can assign tasks to, are equally intelligent and capable, and have access to the same set of tools.

You can use `spawn_agent` to create a new agent, `followup_task` to give an existing agent a new task and trigger a turn, and `send_message` to pass a message to a running agent.
`send_message` calls may be read by a human, so ensure they are legible. Always put proper spaces between words and/or numbers.
Child agents can also spawn their own sub-agents.

When you provide a response in the final channel, that content is immediately delivered back to your parent agent.
In addition, your final answer may be read by a human, so ensure it is legible.

You will receive messages in the analysis channel in the form:
```
Message Type: NEW_TASK | MESSAGE | FINAL_ANSWER
Task name: <recipient>
Sender: <author>
Payload:
<payload text>
```
You may also see them addressed as to=/root/..., which indicates your identity is /root/...

Note that collaboration tools cannot be called from inside `functions.exec`. Call `spawn_agent`, `send_message`, `followup_task`, `wait_agent`, `interrupt_agent`, and `list_agents` only as direct tool calls using the recipient shown in their tool definitions, such as `to=functions.collaboration.spawn_agent`, since they are intentionally absent from the `functions.exec` `tools.*` namespace. Available tools in `functions.exec` are explicitly described with a `tools` namespace in the developer message.

All agents share the same directory. In detail:
- All agents have access to the same container and filesystem as you.
- All agents use the same current working directory.
- As a result, edits made by one agent are immediately visible to all other agents.

When calling `wait_agent`, prefer longer waits (minutes) to avoid busy polling.

There are 4 available concurrency slots, meaning that up to 4 agents can be active at once, including you.

Full-history forks (`fork_turns` omitted or `"all"`) inherit the parent model and reasoning effort and do not accept overrides. Only set `model` or `reasoning_effort` when explicitly requested by the user, applicable `AGENTS.md` instructions, or skill instructions; when doing so, set `fork_turns` to `"none"`.</multi_agent_role>

## developer · 2026-11-10T15:09:38Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-10T15:09:38Z

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
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</root><root>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3f0-bc40-7300-b167-ec3ca479fb89</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</path></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3f0-bc40-7300-b167-ec3ca479fb89</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3f0-bc40-7300-b167-ec3ca479fb89/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3f0-bc40-7300-b167-ec3ca479fb89/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3f0-bc40-7300-b167-ec3ca479fb89/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/10/01a1c3f0-bc40-7300-b167-ec3ca479fb89/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-10T15:09:38Z

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


## developer · 2026-11-10T15:09:38Z

<tools>
Added deferred tool namespaces:
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__pubmed
</tools>

## assistant · 2026-11-10T15:09:44Z

我先读取指定题目范围与题型要求，然后分批写入解析文件。

## tool · 2026-11-10T15:09:44Z


Script completed
Wall time 0.1 seconds
Output:

\pdfbookmark[0]{补充练习}{extra}
\begin{center}
  {\LARGE\bfseries 27302 阶段补充练习\par}
  \small 《工科数学分析基础》第三版上册第一章至第二章第四节
\end{center}
\section*{一、选择题}
\begin{enumerate}
% 500/2/第一章计算1
\item 非零常数 $a,b$ 满足 $\displaystyle\lim_{x\to1}\left(\frac{x}{x-1}-\frac a{\ln x}\right)=b$。
则（\quad）。
\choices{$a=1,\ b=1/2$}{$a=-1,\ b=1/2$}{$a=1,\ b=-1/2$}{$a=-1,\ b=-1/2$}
% 500/2/第一章计算2
\item 下列等式中成立的是（\quad）。
\choices{$\displaystyle\lim_{x\to0^+}(1+1/x)^x=1$}{$\displaystyle\lim_{x\to0^+}(1+1/x)^x=\mathrm e$}
{$\displaystyle\lim_{x\to+\infty}(1-1/x)^x=-\mathrm e$}{$\displaystyle\lim_{x\to+\infty}(\sin x)/x=1$}
% 880/8/第一章综合选择13
\item 对正整数 $n$，设 $u_n$ 为 $x(1+\ln x)=n$ 在 $x\ge1$ 的实根。下列结论中正确的是（\quad）。
\choices{$\{u_n\}$ 收敛}{$\{u_n/n\}$ 发散}{$\{u_n\ln(n)/n\}$ 收敛}{$\{u_n\ln(n)/n\}$ 发散}
% 880/8/第一章综合选择14
\item 设 $\{x_n\}$ 为实数列。判断下列命题。
\par (1) 若 $\{\arctan x_n\}$ 收敛，则 $\{x_n\}$ 收敛。
\par (2) 若 $\{\arctan x_n\}$ 单调，则 $\{x_n\}$ 收敛。
\par (3) 若 $x_n\in[-1,1]$ 且 $\{x_n\}$ 收敛，则 $\{\arcsin x_n\}$ 收敛。
\par (4) 若 $x_n\in[-1,1]$ 且 $\{x_n\}$ 单调，则 $\{\arcsin x_n\}$ 收敛。
\choices{(1)(2) 正确}{(3)(4) 正确}{(1)(3) 正确}{(2)(4) 正确}
% 500/14/第一章概念5
\item 设 $a_n>0$，$b_n=\sum_{k=1}^n a_k$。下列命题中正确的有（\quad）个。
\par (1) 若 $\{a_n\}$ 有界，则 $\{b_n\}$ 有界。
\par (2) 若 $\{b_n\}$ 有界，则 $\{a_n\}$ 有界。
\par (3) 若 $\{a_n\}$ 收敛，则 $\{b_n\}$ 收敛。
\par (4) 若 $\{b_n\}$ 收敛，则 $\{a_n\}$ 收敛。
\choices{0}{1}{2}{3}
% 500/15/第一章概念9
\item 当 $x\to0$ 时，$f(x),g(x),x$ 两两同阶但不等价。下列各量中，必为 $x$ 的高阶无穷小的有（\quad）个。
\[
 \text{(1)}\ f+g,\qquad\text{(2)}\ fg,\qquad
 \text{(3)}\ f^2,\qquad\text{(4)}\ f(x)\sin x\cos(1/x).
\]
\choices{1}{2}{3}{4}
% 500/16/第一章概念11
\item 设 $x_n\to0$。下列说法错误的是（\quad）。
\choices{若 $x_1=-1$，则 $\{x_n\}$ 有最小值}
{若 $x_1x_2=-1$，则 $\{x_n\}$ 有最大值和最小值}
{对任意 $\varepsilon>0$，充分大的 $n$ 都满足 $0<|x_n|<\varepsilon$}
{$\{|x_n|\}$ 必有最大值}
% 500/7/第一章计算18
\item 设 $\displaystyle f(x)=\lim_{n\to\infty}\frac{1+x^{2n+1}}{1+x^{2n}}\cos(\pi x)$。
则 $f$（\quad）。
\choices{在 $1$ 与 $-1$ 处均连续}{在 $1$ 处连续、在 $-1$ 处不连续}
{在 $1$ 与 $-1$ 处均不连续}{在 $1$ 处不连续、在 $-1$ 处连续}
% 六套卷/6/第二套选择1
\item 设 $\displaystyle f(x)=\lim_{n\to\infty}\frac{2x^{2n}-1}{1+x^{2n}}\sin(1/x)$（$x\ne0$）。
函数 $f$ 的第一类间断点有（\quad）个。
\choices{0}{1}{2}{3}
% 六套卷/11/第三套选择2
\item 设 $f$ 在 $1$ 的邻域内连续，且
$\displaystyle\lim_{x\to0}\frac{\ln[f(1+x)+\mathrm{e}^{x^2}]}{x^2}=2$。则 $x=1$ 是（\quad）。
\choices{驻点且为极大值点}{驻点且为极小值点}{不可导点}{可导点但不是驻点}
% 880/14/第二章基础选择5
\item 函数 $f(x)=(x^2+3x+2)|x^3-x|$ 在 $\mathbb R$ 上的不可导点有（\quad）个。
\choices{1}{2}{3}{4}
% 880/16/第二章基础选择14
\item 设 $f$ 在 $a$ 处连续。下列条件中，能推出 $f$ 在 $a$ 处可导的是（\quad）。
\choices{$\displaystyle\lim_{x\to+\infty}|x|\big[f(a+1/|x|)-f(a)\big]$ 存在}
{$\displaystyle\lim_{x\to0}\frac{f(a+x^3)-f(a)}{x^2}$ 存在}
{$\displaystyle\lim_{h\to0}\frac{f(a+h)-f(a-h)}{2h}$ 存在}
{$\displaystyle\lim_{x\to0}\frac{f(a+x^3)-f(a)}{\tan^3 x}$ 存在}
% 500/38/第二章概念10
\item 设 $f$ 在 $(0,1)$ 内可导。$f'$ 在 $(0,1)$ 内有界是 $f$ 在 $(0,1)$ 内有界的（\quad）。
\choices{充分非必要条件}{必要非充分条件}{充要条件}{既非充分也非必要条件}
% 880/28/第二章综合选择28
\item 若 $\displaystyle\lim_{x\to x_0^-}f'(x)=\lim_{x\to x_0^+}f'(x)=1$，则（\quad）。
\choices{$f$ 在 $x_0$ 处必可导且 $f'(x_0)=1$}{$f$ 在 $x_0$ 处必连续但不可导}
{$f$ 在 $x_0$ 处必存在极限但不连续}{$f$ 在 $x_0$ 的某去心左、右邻域内分别单调递增}
% 500/23/第二章计算19
\item 若 $3a^2-5b<0$，则方程 $x^5+2ax^3+3bx+4c=0$ 有（\quad）。
\choices{0 个实根}{1 个实根}{3 个不同实根}{5 个不同实根}
% 880/3/第一章基础选择9
\item 设 $f(x)=(\ln x)^2$、$g(x)=x^2$、$h(x)=\mathrm{e}^x$。当 $x$ 充分大时，（\quad）。
\choices{$f(x)<g(x)<h(x)$}{$g(x)<h(x)<f(x)$}
{$h(x)<g(x)<f(x)$}{$g(x)<f(x)<h(x)$}
% 880/6/第一章综合选择1
\item 使 $\displaystyle\lim_{x\to+\infty}
\frac{\mathrm{e}^{\sin(1/x)}-1}{(1+1/x)^k-(1+1/x)}$ 存在且非零的充要条件是（\quad）。
\choices{$k\ne1$}{$k>1$}{$k>0$}{与 $k$ 无关}
% 880/6/第一章综合选择2
\item 设 $a>0$，$\displaystyle\lim_{x\to+\infty}x^a
\ln\frac{\arctan(x+1)}{\arctan x}=b$。下列哪组 $(a,b)$ 符合等式？
\choices{$a=2,\ b=2/\pi$}{$a=2,\ b=\pi/2$}{$a=1,\ b=2/\pi$}{$a=1,\ b=\pi/2$}
% 880/8/第一章综合选择15
\item 若正项数列 $\{x_n\}$ 对所有 $n$ 都满足 $x_{n+1}<2-1/x_n$，则 $\{x_n\}$（\quad）。
\choices{收敛于 $0$}{收敛于 $1$}{收敛于 $\sqrt 2$}{发散}
% 880/14/第二章基础选择4
\item 设 $f(x)=\begin{cases}a\sqrt{x},&0\le x\le b,\\\ln x,&x>b\end{cases}$（$b>0$），
且 $f$ 在 $(0,+\infty)$ 内可导。则（\quad）。
\choices{$a=2/\mathrm e,\ b=\mathrm e^2$}{$a=2/\mathrm e,\ b=\mathrm e$}
{$a=1/\mathrm e,\ b=\mathrm e^2$}{$a=1/\mathrm e,\ b=\mathrm e$}
% 500/20/第二章计算12
\item 设 $f(x)=\begin{cases}x^{2x},&x>0,\\x\mathrm{e}^x+1,&x\le0.\end{cases}$
则 $x=0$ 是 $f$ 的（\quad）。
\choices{可导点、极值点}{不可导点、极值点}{可导点、非极值点}{不可导点、非极值点}
\end{enumerate}

\section*{二、填空题}
\begin{enumerate}[start=22]
% 880/4/第一章基础填空1
\item 设 $f(x)=\begin{cases}1,&|x|\le1,\\0,&|x|>1.\end{cases}$ 则 $f(f(f(x)))=\blank$。
% 880/4/第一章基础填空2
\item 当 $x\to0$ 时，若 $(1+ax^2)^{1/3}-1\sim\cos x-1$，则 $a=\blank$。
% 880/9/第一章综合填空1
\item 当 $x\to0$ 时，$3x-4\sin x+\sin x\cos x$ 是关于 $x$ 的 $\blank$ 阶无穷小。
% 880/9/第一章综合填空6
\item 若 $k\ne1/2$，则 $\displaystyle\lim_{n\to\infty}
  n\ln\left[\frac{n-2nk+1}{n(1-2k)}\right]=\blank$。
% 880/10/第一章综合填空8
\item 若 $\displaystyle\lim_{x\to+\infty}(\sqrt[3]{1-x^6}-ax^2-b)=0$，则 $(a,b)=\blank$。
% 880/10/第一章综合填空12
\item 设 $y(x)$ 由 $y^2+xy+x^2-x=0$ 确定，且 $y(1)=-1$，
则 $\displaystyle\lim_{x\to1}\frac{(x-1)^2}{1+y(x)}=\blank$。
% 880/10/第一章综合填空13
\item 若 $f''(1)$ 存在且 $f'(1)\ne0$，则 $\displaystyle\lim_{x\to1}
\left[\frac1{f'(1)(x-1)}-\frac1{f(x)-f(1)}\right]=\blank$。
% 880/17/第二章基础填空1
\item 若 $f(x)=\begin{cases}\arctan(1/x),&x>0,\\ax+b,&x\le0\end{cases}$
在 $0$ 处可导，则 $(a,b)=\blank$。
% 880/18/第二章基础填空7
\item 设 $f'(0)$ 存在且 $f(0)=0$。若 $\displaystyle\lim_{x\to0}
\left[1+\frac{1-\cos f(x)}{\sin x}\right]^{1/x}=\mathrm e$，则 $f'(0)$ 的可能取值为 $\blank$。
% 880/18/第二章基础填空11
\item 设 $f_n(x)=n^2\mathrm{e}^{x/n}-(1+n)x$ 在 $x=x_n$ 处有水平切线。
则 $\displaystyle\lim_{n\to\infty}\mathrm{e}^{x_n}=\blank$。
% 500/25/第二章计算26
\item 若 $\displaystyle y=\ln\frac{\sqrt{1+x^2}-1}{\sqrt{1+x^2}+1}$（$x\ne0$），则 $y'=\blank$。
% 500/26/第二章计算29
\item 设 $y\ge1$ 由 $x=y^{y^2}$ 确定，求用 $\mathrm{d}x$ 表示的 $\mathrm{d}y=\blank$。
% 500/27/第二章计算31
\item 对 $x\ne0$ 设 $\displaystyle f(x)=\lim_{t\to0}(1+t\sin x)^{1/(tx)}$，
则 $\displaystyle\lim_{x\to0}f'(x)=\blank$。
% 500/27/第二章计算32
\item 设 $f$ 可导且 $f'(0)=1$，$y(x)$ 由 $y-x\mathrm{e}^{y-1}=1$ 确定。
若 $z=f(\ln y+\sin x)$，则 $\left.\dfrac{\mathrm{d}z}{\mathrm{d}x}\right|_{x=0}=\blank$。
% 500/28/第二章计算34
\item 设 $y=f(x)$ 由 $\ln(x^2+y)=x^3y+\sin x$ 在 $(0,1)$ 的邻域内确定。
则 $\displaystyle\lim_{n\to\infty}n[f(2/n)-1]=\blank$。
% 500/28/第二章计算35
\item 设 $f(x)=\cos(\cos x)+\cos(\sin x)$，则 $f'''(\pi/2)=\blank$。
% 500/30/第二章计算41
\item 曲线 $x^2+xy+y^3=3$ 在 $x=1$ 的对应点处的法线方程为 $\blank$。
% 500/31/第二章计算45
\item 对数螺线 $r=\mathrm{e}^{\theta}$ 在 $\theta=\pi/2$ 处的切线直角坐标方程为 $\blank$。
% 880/30/第二章综合填空10
\item 设 $f$ 是 $g$ 的反函数，$g(1)=2$，$g'(1)=-\sqrt{3}/3$。则
$\displaystyle\lim_{y\to2}\frac{(y-2)[f(y)-f(2)]}{(\ln y-\ln 2)^2}=\blank$。
% 500/10/第一章计算26
\item $\displaystyle\lim_{x\to0}\left(\frac{1}{x(1+x)^{1/x}}-\frac1{x\mathrm e}\right)=\blank$。
% 500/10/第一章计算27
\item $\displaystyle\lim_{n\to\infty}\sum_{k=1}^{n}\frac{k^2}{\sqrt{n^6+kn}}=\blank$。
% 500/11/第一章计算29
\item 若 $\displaystyle\lim_{x\to+\infty}\left(x^{2/3}\sqrt[3]{6-x}-ax-b\right)=0$，则 $ab=\blank$。
% 880/18/第二章基础填空2
\item 设 $f$ 在 $0$ 处可导，且 $f'(0)=2,\ f(0)=0$。则
$\displaystyle\lim_{x\to0}\frac{f(1-\cos x)}{\ln(1+x^2)}=\blank$。
% 500/27/第二章计算33
\item 设 $g(x)=(\mathrm{e}^x+\mathrm{e}^{-x})/2$，对任意实数 $x,y$ 都有
$f(x+y)=f(x)g(y)+f(y)g(x)$，且 $\displaystyle\lim_{x\to0} f(x)/x=1$。
则 $f'(x)=\blank$。
% 500/28/第二章计算36
\item 设 $f(x)=x^2(1+\sin x)$，则 $f^{(5)}(\pi)=\blank$。
% 500/31/第二章计算43
\item 过点 $(3,-1)$ 作参数曲线 $x=\mathrm{e}^t+t,\ y=\mathrm{e}^{-t}-t$（$t\le1$）的切线，
该切线在 $y$ 轴上的截距为 $\blank$。
% 500/31/第二章计算44
\item 双纽线 $r=\sqrt{\cos(2\theta)}$ 在 $\theta=\pi/12$ 处的切线斜率为 $\blank$。
% 880/29/第二章综合填空1
\item 设 $f(x)=\displaystyle\prod_{k=1}^{100}\big[\tan^k(\pi x/4)-k\big]$，
则 $f'(1)=\blank$。
\end{enumerate}



## developer · 2026-11-10T15:09:44Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
</tools>

## tool · 2026-11-10T15:11:14Z


Script completed
Wall time 0.0 seconds
Output:

{}

## assistant · 2026-11-10T15:11:21Z

选择题解析已写到第 21 题；第 19 题的递推条件存在选项不覆盖的反例，已在解答中明确指出。接着处理第 22–49 题。

## tool · 2026-11-10T15:12:57Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:13:27Z


Script completed
Wall time 0.1 seconds
Output:

1:\solution{1}
11:\solution{2}
16:\solution{3}
25:\solution{4}
30:\solution{22}
35:\solution{23}
40:\solution{24}
50:\solution{25}
58:\solution{26}
63:\solution{27}
72:\solution{28}
82:\solution{29}
92:\solution{30}
101:\solution{31}
109:\solution{32}
119:\solution{33}
129:\solution{34}
138:\solution{35}
147:\solution{36}
156:\solution{37}
169:\solution{38}
174:\solution{39}
184:\solution{40}
189:\solution{41}
199:\solution{42}
209:\solution{43}
219:\solution{44}
224:\solution{45}
233:\solution{46}
242:\solution{47}
247:\solution{48}
255:\solution{49}
263:\solution{5}
268:\solution{6}
273:\solution{7}
278:\solution{8}
283:\solution{9}
288:\solution{10}
293:\solution{11}
298:\solution{12}
303:\solution{13}
308:\solution{14}
313:\solution{15}
318:\solution{16}
323:\solution{17}
328:\solution{18}
339:\solution{19}
344:\solution{20}
349:\solution{21}


## tool · 2026-11-10T15:14:04Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
在 $x=1$ 时方程成立。令 $F(x,y)=x^2+xy+y^3-3$，梯度为 $(2x+y,x+3y^2)$，在 $(1,1)$ 处为 $(3,4)$，即切线法向量。因此法线方向为切线方向 $(4,-3)$，法线方程 $3(x-1)+4(y-1)=0$ 吗？检验法线的方向应沿梯度 $(3,4)$，故斜率 $4/3$，方程 $y-1=\frac43(x-1)$。

## tool · 2026-11-10T15:14:09Z


Script completed
Wall time 0.1 seconds
Output:

\solution{1}
\approach{用 $x=1+h$ 展开两个具有同一主部的奇异项。}
令 $h=x-1$。由 $\ln(1+h)=h-\frac{h^2}{2}+o(h^2)$，有
\[
\frac{x}{x-1}=\frac1h+1,\qquad
当 $x\to+\infty$，$\sqrt[3]{1-x^6}=-x^2(1-x^{-6})^{1/3}=-x^2+o(1)$，因为根式与 $-x^2$ 的差为 $O(x^{-4})$。故表达式要趋于零，必须 $a=-1,b=0$，且这组值确实使极限为零。
\answer{$(-1,0)$}

\solution{27}
\approach{在 $(1,-1)$ 附近对隐式方程作二阶展开，解出 $1+y$ 的首项。}
令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
\[
u^2+(h-1)u+h+h^2=0.
\]
题给分支满足 $u\to0$，隐函数的一阶项由 $-u+h=0$ 给出 $u=h+O(h^2)$；进一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$0$}

\solution{28}
\approach{用二阶 Taylor 展开把两个倒数的主部相消。}
令 $h=x-1$。记 $p=f'(1)\ne0$，$q=f''(1)$。则
\[
f(1+h)-f(1)=ph+\frac q2h^2+o(h^2),\quad
\frac1{f(1+h)-f(1)}=\frac1{ph}-\frac{q}{2p^2}+o(1).
\]
\[
\frac{2x+y'}{x^2+y}=3x^2y+x^3y'+\cos x.
\]
在 $x=0,y=1$ 代入得 $y'(0)=1$。故 $f(2/n)=1+2/n+o(1/n)$，所求极限为 $2$。
\answer{$2$}

\solution{37}
\approach{利用链式法则逐项求三阶导数并代入 $\pi/2$。}
令 $u=\cos x,v=\sin x$，则 $f=\cos u+\cos v$。直接求导得
\[
f'=\sin x\sin(\cos x)-\cos x\sin(\sin x),
\]
\[
f''=\cos x\sin(\cos x)-\sin^2x\cos(\cos x)
+\sin x\sin(\sin x)-\cos^2x\cos(\sin x).
\]
对上式再求导并令 $x=\pi/2$，第一对项导数相消后为 $0$；第二对项分别给出 $-1$ 与 $1$ 的相抵项，合计为 $0$。故 $f'''(\pi/2)=0$。
\answer{$0$}

\solution{38}
\approach{先解出对应点，再用梯度给出法线方向。}
代入 $x=1$ 得 $1+y+y^3=3$，即 $y^3+y-2=0$，其唯一实根为 $y=1$。令 $F=x^2+xy+y^3-3$，梯度为 $(2x+y,x+3y^2)$，在 $(1,1)$ 处为 $(3,4)$，即切线法向量。因此法线方向为切线方向 $(4,-3)$，法线方程 $3(x-1)+4(y-1)=0$ 吗？检验法线的方向应沿梯度 $(3,4)$，故斜率 $4/3$，方程 $y-1=\frac43(x-1)$。
\answer{$4x-3y-1=0$}

\solution{39}
\approach{用极坐标曲线的参数导数求切向量，再转换成直角坐标直线。}
参数式 $x=\mathrm e^\theta\cos\theta$、$y=\mathrm e^\theta\sin\theta$。在 $\theta=\pi/2$ 处点为 $(0,\mathrm e^{\pi/2})$，且
\[
\frac{\mathrm dx}{\mathrm d\theta}=\mathrm e^\theta(\cos\theta-\sin\theta)=-\mathrm e^{\pi/2},\quad
\frac{\mathrm dy}{\mathrm d\theta}=\mathrm e^\theta(\sin\theta+\cos\theta)=\mathrm e^{\pi/2}.
\]
\approach{由反函数导数关系先求 $f'(2)$，再将分子分母分别除以 $y-2$ 的适当次幂。}
有 $f(2)=1$，$f'(2)=1/g'(1)=-\sqrt3$。令 $h=y-2$，泰勒展开给出 $f(2+h)-1=-\sqrt3h+o(h)$，而 $\ln(2+h)-\ln2=h/2+o(h)$。所给商分子为 $h[-\sqrt3h+o(h)]$，分母为 $h^2/4+o(h^2)$，故极限为 $-4\sqrt3$。
\answer{$-4\sqrt3$}

\solution{41}
\approach{展开 $(1+x)^{-1/x}$ 到足以确定 $1/x$ 主项抵消后的常数阶。}
有 $\frac1x\ln(1+x)=1-\frac{x}{2}+O(x^2)$，因此
\[
(1+x)^{1/x}=\mathrm e\left(1-\frac x2+O(x^2)\right),\quad
\frac1{(1+x)^{1/x}}=\frac1{\mathrm e}\left(1+\frac x2+O(x^2)\right).
\]
原式等于 $\frac1{x}\left[\frac1{(1+x)^{1/x}}-\frac1{\mathrm e}\right]$，极限为 $1/(2\mathrm e)$。
\answer{$\dfrac{1}{2\mathrm e}$}

\[
\frac{\sin(\pi/12)/\sqrt3+\cos(\pi/12)}{-\cos(\pi/12)/\sqrt3-\sin(\pi/12)}=-2.
\]
\answer{$-2$}

\solution{49}
\approach{利用乘积中唯一在 $x=1$ 消失的因子，其余因子直接相乘。}
在 $x=1$ 时 $\tan(\pi/4)=1$，仅 $k=1$ 的因子为零，故乘积求导只剩该因子的导数乘其余因子值。$k=1$ 因子的导数为 $\frac\pi4\sec^2(\pi/4)=\pi/2$；对 $k\ge2$，因子值为 $1-k$。因此
\[
f'(1)=\frac\pi2\prod_{k=2}^{100}(1-k)=\frac\pi2\,(-1)^{99}99!=-\frac{\pi}{2}\,99!.
\]
\answer{$-\dfrac{\pi}{2}\,99!$}

\solution{5}
\approach{利用正项部分和的单调性，以及相邻部分和之差。}
(1)不成立，$a_n=1$ 有界而 $b_n=n$ 无界。(2)成立，因为 $0<a_n\le b_n$。(3)不成立，仍取 $a_n=1$。(4)成立：若 $b_n$ 收敛，则 $a_n=b_n-b_{n-1}\to0$（令 $b_0=0$）。恰有两项成立。


## tool · 2026-11-10T15:14:39Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
\[
u^2+(h-1)u+h+h^2=0.
\]
題給分支滿足 $u\to0$，隱函數的一階項由 $-u+h=0$ 給出 $u=h+O(h^2)$；進一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。

## tool · 2026-11-10T15:14:46Z


Script completed
Wall time 0.1 seconds
Output:

\solution{27}
\approach{在 $(1,-1)$ 附近对隐式方程作二阶展开，解出 $1+y$ 的首项。}
令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
\[
u^2+(h-1)u+h+h^2=0.
\]
题给分支满足 $u\to0$，隐函数的一阶项由 $-u+h=0$ 给出 $u=h+O(h^2)$；进一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$0$}


\solution{37}
\approach{利用链式法则逐项求三阶导数并代入 $\pi/2$。}
令 $u=\cos x,v=\sin x$，则 $f=\cos u+\cos v$。直接求导得
\[
f'=\sin x\sin(\cos x)-\cos x\sin(\sin x),
\]
\[
f''=\cos x\sin(\cos x)-\sin^2x\cos(\cos x)
+\sin x\sin(\sin x)-\cos^2x\cos(\sin x).
\]
对上式再求导并令 $x=\pi/2$，第一对项导数相消后为 $0$；第二对项分别给出 $-1$ 与 $1$ 的相抵项，合计为 $0$。故 $f'''(\pi/2)=0$。
\answer{$0$}

\solution{38}
\approach{先解出对应点，再用梯度给出法线方向。}
代入 $x=1$ 得 $1+y+y^3=3$，即 $y^3+y-2=0$，其唯一实根为 $y=1$。令 $F=x^2+xy+y^3-3$，梯度为 $(2x+y,x+3y^2)$，在 $(1,1)$ 处为 $(3,4)$，即切线法向量。因此法线方向为切线方向 $(4,-3)$，法线方程 $3(x-1)+4(y-1)=0$ 吗？检验法线的方向应沿梯度 $(3,4)$，故斜率 $4/3$，方程 $y-1=\frac43(x-1)$。
\answer{$4x-3y-1=0$}

\solution{39}
\approach{用极坐标曲线的参数导数求切向量，再转换成直角坐标直线。}
参数式 $x=\mathrm e^\theta\cos\theta$、$y=\mathrm e^\theta\sin\theta$。在 $\theta=\pi/2$ 处点为 $(0,\mathrm e^{\pi/2})$，且
\answer{题设矛盾，切线不存在}

\solution{48}
\approach{用极坐标曲线的斜率公式并代入指定角。}
由 $x=r\cos\theta,y=r\sin\theta$，切线斜率为 $\frac{r'\sin\theta+r\cos\theta}{r'\cos\theta-r\sin\theta}$。这里 $r=\sqrt{\cos2\theta}$，故 $r'/r=-\tan2\theta$。在 $\theta=\pi/12$，$r'/r=-1/\sqrt3$，于是斜率
\[
\frac{\sin(\pi/12)/\sqrt3+\cos(\pi/12)}{-\cos(\pi/12)/\sqrt3-\sin(\pi/12)}=-2.
\]
\answer{$-2$}

\solution{49}
\approach{利用乘积中唯一在 $x=1$ 消失的因子，其余因子直接相乘。}
在 $x=1$ 时 $\tan(\pi/4)=1$，仅 $k=1$ 的因子为零，故乘积求导只剩该因子的导数乘其余因子值。$k=1$ 因子的导数为 $\frac\pi4\sec^2(\pi/4)=\pi/2$；对 $k\ge2$，因子值为 $1-k$。因此
\[
\[
f'(1)=\frac\pi2\prod_{k=2}^{100}(1-k)=\frac\pi2\,(-1)^{99}99!=-\frac{\pi}{2}\,99!.
\]
\answer{$-\dfrac{\pi}{2}\,99!$}

\solution{5}
\approach{利用正项部分和的单调性，以及相邻部分和之差。}
(1)不成立，$a_n=1$ 有界而 $b_n=n$ 无界。(2)成立，因为 $0<a_n\le b_n$。(3)不成立，仍取 $a_n=1$。(4)成立：若 $b_n$ 收敛，则 $a_n=b_n-b_{n-1}\to0$（令 $b_0=0$）。恰有两项成立。
\answer{C}

\solution{6}
\approach{把“同阶”转为比值有界且有正下界，逐项估计。}
由 $f,g,x$ 两两同阶，$f=O(x)$、$g=O(x)$，且 $f/x$、$g/x$ 的绝对值趋于非零常数（同阶的定义）。(2) $fg=O(x^2)=o(x)$；(3) $f^2=O(x^2)=o(x)$；(4) $f\sin x\cos(1/x)=O(x^2)=o(x)$。而(1)未必是高阶，例如 $f=x,g=2x$，则 $f+g=3x$，且符合两两同阶但不等价。故必定的有三项。


## tool · 2026-11-10T15:14:53Z




## tool · 2026-11-10T15:15:18Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
\[
u^2+(h-1)u+h+h^2=0.
\]
題給分支滿足 $u\to0$，隱函數的一階項由 $-u+h=0$ 給出 $u=h+O(h^2)$；進一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$0$}

## tool · 2026-11-10T15:15:24Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:15:33Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
題給分支滿足 $u\to0$，隱函數的一階項由 $-u+h=0$ 給出 $u=h+O(h^2)$；進一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$0$}

## assistant · 2026-11-10T15:15:40Z

已写入 `.question-bank-work/27302-solutions/extra1.tex`。第 1–49 题都有解析草稿；题目第 19、47 题发现条件或参数范围与选项冲突，草稿中指出了问题。

草稿尚未完成核对：22–49 题块误排在第 4 题之后，部分推导也有错误，包括第 27、38、48 题。没有编译或验证。

## tool · 2026-11-10T15:16:36Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
(1)不成立，$x_n=n$ 时 $\arctan x_n\to\pi/2$，但 $x_n$ 发散。(2)不成立，$\arctan x_n$ 可以单调趋于 $\pi/2$ 而 $x_n\to+\infty$。(3)成立：$\arcsin$ 在闭区间 $[-1,1]$ 连续，故保极限。(4)成立：有界单调数列 $x_n\in[-1,1]$ 收敛，再由连续性得 $\arcsin x_n$ 收敛。

## tool · 2026-11-10T15:16:47Z


Script completed
Wall time 0.1 seconds
Output:

25:\solution{4}
26-\approach{利用反正切的单调性和反函数连续性逐项判断。}
27-(1)不成立，例如 $x_n=n$ 时 $\arctan x_n\to\pi/2$，但 $x_n$ 发散。(2)不成立，$\arctan x_n$ 可以单调趋于 $\pi/2$ 而 $x_n\to+\infty$。(3)成立：$\arcsin$ 在闭区间 $[-1,1]$ 连续，故保极限。(4)成立：有界单调数列 $x_n\in[-1,1]$ 收敛，再由连续性得 $\arcsin x_n$ 收敛。
28-\answer{B}
29-
--
63:\solution{27}
64-\approach{在 $(1,-1)$ 附近对隐式方程作二阶展开，解出 $1+y$ 的首项。}
65-令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
66-\[
67-u^2+(h-1)u+h^2=0.
--
129:\solution{34}
130-\approach{先对 $t$ 取极限得到显式函数，再求导后取零点极限。}
131-对固定 $x\ne0$，$f(x)=\exp(\sin x/x)$。因此
132-\[
133-f'(x)=f(x)\frac{x\cos x-\sin x}{x^2}.
--
156:\solution{37}
157-\approach{利用链式法则逐项求三阶导数并代入 $\pi/2$。}
158-令 $u=\cos x,v=\sin x$，则 $f=\cos u+\cos v$。直接求导得
159-\[
160-f'=\sin x\sin(\cos x)-\cos x\sin(\sin x),
--
169:\solution{38}
170-\approach{先解出对应点，再用梯度给出法线方向。}
171-代入 $x=1$ 得 $1+y+y^3=3$，即 $y^3+y-2=0$，其唯一实根为 $y=1$。令 $F=x^2+xy+y^3-3$，梯度为 $(2x+y,x+3y^2)$，在 $(1,1)$ 处为 $(3,4)$，即切线法向量。因此法线方向为切线方向 $(4,-3)$，法线方程 $3(x-1)+4(y-1)=0$ 吗？检验法线的方向应沿梯度 $(3,4)$，故斜率 $4/3$，方程 $y-1=\frac43(x-1)$。
172-\answer{$4x-3y-1=0$}
173-
--
199:\solution{42}
200-\approach{把每项分母提出 $n^3$，再识别 Riemann 和。}
201-\[
202-\sqrt{n^6+kn}=n^3\sqrt{1+k/n^5},\quad
203-\sum_{k=1}^n\frac{k^2}{\sqrt{n^6+kn}}
--
233:\solution{46}
234-\approach{展开 $x^2+x^2\sin x$，提取五阶导数对应的五次幂系数。}
235-在 $x=\pi$ 处令 $h=x-\pi$，则 $\sin x=-\sin h$，从而
236-\[
237-f(\pi+h)=(\pi+h)^2(1-\sin h).
--
242:\solution{47}
243-\approach{先由给定点确定参数，再求切线并外推到 $y$ 轴。}
244-由 $x=3,y=-1$ 得 $t=0$（两式分别给出 $1+t=3$、$1-t=-1$？前者给 $t=2$，后者给 $t=2$，但 $t\le1$ 不允许）。事实上参数曲线 $x=\mathrm e^t+t$ 严格递增，$x=3$ 对应 $t>1$，与题给 $t\le1$ 冲突。对 $t\le1$，有 $x\le\mathrm e+1<3$，故曲线上没有点 $(3,-1)$，题目所述切线不存在。
245-\answer{题设矛盾，切线不存在}
246-
247:\solution{48}
248-\approach{用极坐标曲线的斜率公式并代入指定角。}
249-由 $x=r\cos\theta,y=r\sin\theta$，切线斜率为 $\frac{r'\sin\theta+r\cos\theta}{r'\cos\theta-r\sin\theta}$。这里 $r=\sqrt{\cos2\theta}$，故 $r'/r=-\tan2\theta$。在 $\theta=\pi/12$，$r'/r=-1/\sqrt3$，于是斜率
250-\[
251-\frac{\sin(\pi/12)/\sqrt3+\cos(\pi/12)}{-\cos(\pi/12)/\sqrt3-\sin(\pi/12)}=-2.
--
268:\solution{6}
269-\approach{把“同阶”转为比值有界且有正下界，逐项估计。}
270-由 $f,g,x$ 两两同阶，$f=O(x)$、$g=O(x)$，且 $f/x$、$g/x$ 的绝对值趋于非零常数（同阶的定义）。(2) $fg=O(x^2)=o(x)$；(3) $f^2=O(x^2)=o(x)$；(4) $f\sin x\cos(1/x)=O(x^2)=o(x)$。而(1)未必是高阶，例如 $f=x,g=2x$，则 $f+g=3x$，且符合两两同阶但不等价。故必定的有三项。
271-\answer{C}
272-
--
278:\solution{8}
279-\approach{先求去掉端点后的点态表达式，再比较端点函数值与邻域极限。}
280-当 $|x|<1$ 时，$x^{2n}\to0$，分式趋于 $1$，故 $f(x)=\cos(\pi x)$。在 $x=1$ 时分式恒为 $1$，$f(1)=-1$，与邻域极限 $-1$ 相同。在 $x=-1$ 时分子恒为 $0$、分母为 $2$，故 $f(-1)=0$，而邻域内趋于 $\cos(-\pi)=-1$，不连续。因此只在 $1$ 连续。
281-\answer{B}
282-
--
298:\solution{12}
299-\approach{把四个极限分别化成 $f$ 的不同方向差商，并检验是否强制同一导数。}
300-A 中令 $h=1/|x|>0$，只给出右导数存在；取 $f(a+h)=h$、$f(a-h)=0$ 即可见不保证可导。B 中分子为 $f(a+x^3)-f(a)$，若 $f(t)=|t-a|$，商为 $|x|/x^2$ 不收敛；反之即便该商存在，只约束相应方向上的增量阶，不能控制线性差商。C 仅是对称差商存在，不能推出单侧导数相同，例如 $f(a+h)=h^2\sin(1/h^2)$（$h\ne0$）且 $f(a)=0$，对称差商为 $0$，其导数差商无极限。D 中令 $h=x^3$，$\tan^3x\sim x^3=h$，双侧覆盖 $h\to0$，该极限存在便是 $f$ 在 $a$ 处导数存在。因此 D 可推出可导。
301-\answer{D}
302-
--
313:\solution{15}
314-\approach{考察多项式导数，并利用三次导数多项式的判别式符号。}
315-令 $P(x)=x^5+2ax^3+3bx+4c$，则 $P'(x)=5x^4+6ax^2+3b$。置 $t=x^2\ge0$，得 $P'=5t^2+6at+3b$。条件 $3a^2-5b<0$ 即 $b>3a^2/5>0$，从而该二次式判别式 $36a^2-60b<0$，且首项系数正，故对一切 $t$ 均正。于是 $P$ 严格递增，且 $P(\pm\infty)=\pm\infty$，恰有一个实根。
316-\answer{B}
317-
--
339:\solution{19}
340-\approach{将递推上界改写为关于 $x_n$ 的恒等式，再判断是否能保证趋于某个值。}
341-题设蕴含 $0<x_{n+1}<2-1/x_n=(2x_n-1)/x_n$，所以必须有 $x_n>1/2$。但结论不唯一：常数列 $x_n=c$ 对条件要求 $c<2-1/c$，即 $1/2<c<1$；例如 $c=3/4$ 满足条件，却收敛于 $3/4$，不属于前三个结论。常数列 $x_n=2$ 也满足 $2<3/2$ 吗？不成立。实际上正项迭代约束还使 $x_n<1$：若某项 $x_n\ge1$，上界 $2-1/x_n<2$ 可仍大于等于1；但取 $x_n=1.2$ 时后项可选 $1.1$，继续可形成不同轨迹。题目给出的四个选项因此需审查：例如常数列 $3/4$ 满足，已证明它收敛但不趋于0、1或$\sqrt2$，也不发散。原题条件不足，选项无正确项。
342-\answer{题目条件不足，选项无正确项}
343-
--
349:\solution{21}
350-\approach{比较零点处函数值、左右差商及函数符号。}
351-两侧函数值都趋于 $1$，且 $f(0)=1$，故连续。右侧 $x^{2x}=\exp(2x\ln x)$，故右差商为 $x^{2x}\,(x^{2x}-1)/x\sim2\ln x\to-\infty$；左侧 $x\mathrm e^x+1$ 的差商趋于 $1$，所以不可导。又 $x>0$ 时 $2x\ln x<0$，故 $x^{2x}<1$；$x<0$ 且充分接近零时 $x\mathrm e^x<0$，函数亦小于 $1$，因此 $0$ 为局部极大值点。
352-\answer{B}


## tool · 2026-11-10T15:17:19Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
而(1)未必是高阶，例如 $f=x,g=2x$，则 $f+g=3x$，且符合两两同阶但不等价。

## tool · 2026-11-10T15:17:29Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:17:39Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:17:49Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:18:02Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:18:06Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:18:11Z


Script completed
Wall time 0.1 seconds
Output:

\approach{在 $(1,-1)$ 附近对隐式方程作二阶展开，解出 $1+y$ 的首项。}
令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
\[
u^2+(h-1)u+h^2=0.
\]
题给分支满足 $u\to0$，隐函数的一阶项由 $-u+h=0$ 给出 $u=h+O(h^2)$；进一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$0$}

\solution{47}
\approach{先由给定点确定参数，再求切线并外推到 $y$ 轴。}
由 $x=3,y=-1$ 得 $t=0$（两式分别给出 $1+t=3$、$1-t=-1$？前者给 $t=2$，后者给 $t=2$，但 $t\le1$ 不允许）。事实上参数曲线 $x=\mathrm e^t+t$ 严格递增，$x=3$ 对应 $t>1$，与题给 $t\le1$ 冲突。对 $t\le1$，有 $x\le\mathrm e+1<3$，故曲线上没有点 $(3,-1)$，题目所述切线不存在。
\answer{题设矛盾，切线不存在}

\solution{48}
\approach{用极坐标曲线的斜率公式并代入指定角。}
由 $x=r\cos\theta,y=r\sin\theta$，切线斜率为 $\frac{r'\sin\theta+r\cos\theta}{r'\cos\theta-r\sin\theta}$。这里 $r=\sqrt{\cos2\theta}$，故 $r'/r=-\tan2\theta$。在 $\theta=\pi/12$，$r'/r=-1/\sqrt3$，于是斜率
\[
\frac{\sin(\pi/12)/\sqrt3+\cos(\pi/12)}{-\cos(\pi/12)/\sqrt3-\sin(\pi/12)}=-2.
\]
\answer{$-2$}

\solution{49}
\approach{利用乘积中唯一在 $x=1$ 消失的因子，其余因子直接相乘。}

\solution{19}
\approach{将递推上界改写为关于 $x_n$ 的恒等式，再判断是否能保证趋于某个值。}
题设蕴含 $0<x_{n+1}<2-1/x_n=(2x_n-1)/x_n$，所以必须有 $x_n>1/2$。但结论不唯一：常数列 $x_n=c$ 对条件要求 $c<2-1/c$，即 $1/2<c<1$；例如 $c=3/4$ 满足条件，却收敛于 $3/4$，不属于前三个结论。常数列 $x_n=2$ 也满足 $2<3/2$ 吗？不成立。实际上正项迭代约束还使 $x_n<1$：若某项 $x_n\ge1$，上界 $2-1/x_n<2$ 可仍大于等于1；但取 $x_n=1.2$ 时后项可选 $1.1$，继续可形成不同轨迹。题目给出的四个选项因此需审查：例如常数列 $3/4$ 满足，已证明它收敛但不趋于0、1或$\sqrt2$，也不发散。原题条件不足，选项无正确项。
\answer{题目条件不足，选项无正确项}

\solution{20}


## tool · 2026-11-10T15:18:18Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
題給分支滿足 $u\to0$，隱函數的一階項由 $-u+h=0$ 給出 $u=h+O(h^2)$；進一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$0$}

## tool · 2026-11-10T15:18:22Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:18:27Z


Script completed
Wall time 0.1 seconds
Output:


## tool · 2026-11-10T15:18:53Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
\solution{27}
\approach{在 $(1,-1)$ 附近对隐式方程作二阶展开，解出 $1+y$ 的首项。}
令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
\[
u^2+(h-1)u+h^2=0.
\]
題給分支滿足 $u\to0$，隱函數的一階項由 $-u+h=0$ 給出 $u=h+O(h^2)$；進一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$0$}

## tool · 2026-11-10T15:18:57Z


Script completed
Wall time 0.1 seconds
Output:

\solution{27}
\approach{在 $(1,-1)$ 附近对隐式方程作二阶展开，解出 $1+y$ 的首项。}
令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
\[
u^2+(h-1)u+h^2=0.
\]
题给分支满足 $u\to0$，隐函数的一阶项由 $-u+h=0$ 给出 $u=h+O(h^2)$；进一步代入得 $u=h+2h^2+O(h^3)$。因此 $h^2/u\to0$。
\answer{$1$}

\solution{34}
\approach{先对 $t$ 取极限得到显式函数，再求导后取零点极限。}
对固定 $x\ne0$，$f(x)=\exp(\sin x/x)$。因此
\[
f'(x)=f(x)\frac{x\cos x-\sin x}{x^2}.
\]
当 $x\to0$，$f(x)\to1$，且 $x\cos x-\sin x=-x^3/3+O(x^5)$，所以 $f'(x)\to0$。
\answer{$0$}

\solution{35}
\solution{46}
\approach{展开 $x^2+x^2\sin x$，提取五阶导数对应的五次幂系数。}
在 $x=\pi$ 处令 $h=x-\pi$，则 $\sin x=-\sin h$，从而
\[
f(\pi+h)=(\pi+h)^2(1-\sin h).
\]
五阶导数等于该展开中 $h^5$ 系数乘 $5!$。$-\sin h$ 的五次项为 $h^5/120$，乘 $(\pi+h)^2$ 的常数项贡献 $\pi^2/120$；$h^3/6$ 与 $2\pi h$ 的乘积贡献 $\pi/3$。故 $f^{(5)}(\pi)=\pi^2+40\pi$。
\answer{$\pi^2+40\pi$}

\solution{47}
\approach{先由给定点确定参数，再求切线并外推到 $y$ 轴。}
由 $x=3,y=-1$ 得 $t=0$（两式分别给出 $1+t=3$、$1-t=-1$？前者给 $t=2$，后者给 $t=2$，但 $t\le1$ 不允许）。事实上参数曲线 $x=\mathrm e^t+t$ 严格递增，$x=3$ 对应 $t>1$，与题给 $t\le1$ 冲突。对 $t\le1$，有 $x\le\mathrm e+1<3$，故曲线上没有点 $(3,-1)$，题目所述切线不存在。
\answer{题设矛盾，切线不存在}

\solution{48}
\approach{用极坐标曲线的斜率公式并代入指定角。}
由 $x=r\cos\theta,y=r\sin\theta$，切线斜率为 $\frac{r'\sin\theta+r\cos\theta}{r'\cos\theta-r\sin\theta}$。这里 $r=\sqrt{\cos2\theta}$，故 $r'/r=-\tan2\theta$。在 $\theta=\pi/12$，$r'/r=-1/\sqrt3$，于是斜率
\[
\frac{\sin(\pi/12)/\sqrt3+\cos(\pi/12)}{-\cos(\pi/12)/\sqrt3-\sin(\pi/12)}=-2.
\]
\answer{$-2$}

\solution{49}
\approach{利用乘积中唯一在 $x=1$ 消失的因子，其余因子直接相乘。}
在 $x=1$ 时 $\tan(\pi/4)=1$，仅 $k=1$ 的因子为零，故乘积求导只剩该因子的导数乘其余因子值。$k=1$ 因子的导数为 $\frac\pi4\sec^2(\pi/4)=\pi/2$；对 $k\ge2$，因子值为 $1-k$。因此
\[

\solution{19}
\approach{将递推上界改写为关于 $x_n$ 的恒等式，再判断是否能保证趋于某个值。}
题设蕴含 $0<x_{n+1}<2-1/x_n=(2x_n-1)/x_n$，所以必须有 $x_n>1/2$。但结论不唯一：常数列 $x_n=c$ 对条件要求 $c<2-1/c$，即 $1/2<c<1$；例如 $c=3/4$ 满足条件，却收敛于 $3/4$，不属于前三个结论。常数列 $x_n=2$ 也满足 $2<3/2$ 吗？不成立。实际上正项迭代约束还使 $x_n<1$：若某项 $x_n\ge1$，上界 $2-1/x_n<2$ 可仍大于等于1；但取 $x_n=1.2$ 时后项可选 $1.1$，继续可形成不同轨迹。题目给出的四个选项因此需审查：例如常数列 $3/4$ 满足，已证明它收敛但不趋于0、1或$\sqrt2$，也不发散。原题条件不足，选项无正确项。
\answer{题目条件不足，选项无正确项}

\solution{20}


## tool · 2026-11-10T15:19:04Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-10T15:19:16Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
apply_patch verification failed: Failed to find expected lines in /Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/27302-solutions/extra1.tex:
題設蕴含 $0<x_{n+1}<2-1/x_n=(2x_n-1)/x_n$，所以必须有 $x_n>1/2$。但结论不唯一：常数列 $x_n=c$ 对条件要求 $c<2-1/c$，即 $1/2<c<1$；例如 $c=3/4$ 满足条件，却收敛于 $3/4$，不属于前三个结论。常数列 $x_n=2$ 也满足 $2<3/2$ 吗？不成立。实际上正项迭代约束还使 $x_n<1$：若某项 $x_n\ge1$，上界 $2-1/x_n<2$ 可仍大于等于1；但取 $x_n=1.2$ 时后项可选 $1.1$，继续可形成不同轨迹。题目给出的四个选项因此需审查：例如常数列 $3/4$ 满足，已证明它收敛但不趋于0、1或$\sqrt2$，也不发散。原题条件不足，选项无正确项。
\answer{题目条件不足，选项无正确项}

## tool · 2026-11-10T15:19:22Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:19:35Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:19:58Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:20:31Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:21:07Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-10T15:21:13Z


Script completed
Wall time 0.1 seconds
Output:

64:\solution{27}
65-\approach{在 $(1,-1)$ 附近对隐式方程作二阶展开，解出 $1+y$ 的首项。}
66-令 $h=x-1$、$u=y+1$。代入 $y^2+xy+x^2-x=0$ 得
67-\[
68-u^2+(h-1)u+h^2=0.
69-\]
--
130:\solution{34}
131-\approach{先对 $t$ 取极限得到显式函数，再求导后取零点极限。}
132-对固定 $x\ne0$，$f(x)=\exp(\sin x/x)$，且 $f(x)\to\mathrm e$。因此
133-\[
134-f'(x)=f(x)\frac{x\cos x-\sin x}{x^2}.
135-\]
--
157:\solution{37}
158-\approach{利用链式法则逐项求三阶导数并代入 $\pi/2$。}
159-令 $h=x-\pi/2$，则 $f(\pi/2+h)=\cos(\sin h)+\cos(\cos h)$，这是 $h$ 的偶函数。因此 $f'''(\pi/2)=0$。
160-\answer{$0$}
161-
162:\solution{38}
163-\approach{先解出对应点，再用梯度给出法线方向。}
164-代入 $x=1$ 得 $1+y+y^3=3$，即 $y^3+y-2=0$，唯一实根为 $y=1$。令 $F=x^2+xy+y^3-3$，梯度在 $(1,1)$ 处为 $(3,4)$，为法线方向，故法线斜率为 $4/3$，方程为 $y-1=\frac43(x-1)$。
165-\answer{$4x-3y-1=0$}
166-
167-\solution{39}
--
200:\solution{42}
201-\approach{用分母的上下界夹住求和，再使用平方和公式。}
202-由于 $0<k\le n$，有 $n^6<n^6+kn\le n^6+n^2$，从而
203-\[
204-\frac{\sum_{k=1}^n k^2}{\sqrt{n^6+n^2}}
205-\le \sum_{k=1}^n\frac{k^2}{\sqrt{n^6+kn}}
--
235:\solution{46}
236-\approach{展开 $x^2+x^2\sin x$，提取五阶导数对应的五次幂系数。}
237-在 $x=\pi$ 处令 $h=x-\pi$，则 $\sin x=-\sin h$，从而
238-\[
239-f(\pi+h)=(\pi+h)^2(1-\sin h).
240-\]
--
244:\solution{47}
245-\approach{先由给定点确定参数，再求切线并外推到 $y$ 轴。}
246-切点参数记为 $t$。由 $x'=\mathrm e^t+1$、$y'=-\mathrm e^{-t}-1$，切线斜率为 $-\mathrm e^{-t}$。要求切线经过 $(3,-1)$，代入切线方程得 $(2-t)(1-\mathrm e^{-t})=0$。在 $t\le1$ 范围内唯一解为 $t=0$，对应切点 $(1,1)$，切线为 $y-1=-(x-1)$，在 $y$ 轴截距为 $2$。
247-\answer{$2$}
248-
249:\solution{48}
250-\approach{用极坐标曲线的斜率公式并代入指定角。}
251-由 $x=r\cos\theta,y=r\sin\theta$，切线斜率为 $\frac{r'\sin\theta+r\cos\theta}{r'\cos\theta-r\sin\theta}$。这里 $r=\sqrt{\cos2\theta}$，故 $r'/r=-\tan2\theta$。在 $\theta=\pi/12$，$r'/r=-1/\sqrt3$，于是斜率
252-\[
253-\frac{\cos(\pi/12)-\sin(\pi/12)/\sqrt3}{-\cos(\pi/12)/\sqrt3-\sin(\pi/12)}=-1.
254-\]
--
270:\solution{6}
271-\approach{把“同阶”转为比值有界且有正下界，逐项估计。}
272-由 $f,g,x$ 两两同阶，$f=O(x)$、$g=O(x)$。(2) $fg=O(x^2)=o(x)$；(3) $f^2=O(x^2)=o(x)$；(4) $f\sin x\cos(1/x)=O(x^2)=o(x)$。而(1)未必是高阶，例如 $f=2x,g=3x$，则 $f+g=5x$，且符合两两同阶但不等价。故必定的有三项。
273-\answer{C}
274-
275-\solution{7}
--
280:\solution{8}
281-\approach{先求去掉端点后的点态表达式，再比较端点函数值与邻域极限。}
282-当 $|x|<1$ 时，$x^{2n}\to0$，分式趋于 $1$，故 $f(x)=\cos(\pi x)$；当 $|x|>1$ 时，分式趋于 $x$，故 $f(x)=x\cos(\pi x)$。在 $x=1$ 时分式恒为 $1$，$f(1)=-1$，左右极限均为 $-1$。在 $x=-1$ 时分子恒为 $0$、分母为 $2$，故 $f(-1)=0$；从区间内趋近时函数趋于 $-1$，从区间外趋近时趋于 $1$，故不连续。因此只在 $1$ 连续。
283-\answer{B}
284-
285-\solution{9}
--
300:\solution{12}
301-\approach{把四个极限分别化成 $f$ 的不同方向差商，并检验是否强制同一导数。}
302-A 只给出右导数，不能推出可导。B、C 均可取 $f(a+h)=|h|$ 作为反例：B 中极限为 $0$，C 中对称差商恒为 $0$，但 $f$ 在 $a$ 处不可导。D 中令 $h=x^3$，$\tan^3x\sim x^3=h$，双侧覆盖 $h\to0$，该极限存在便是 $f$ 在 $a$ 处导数存在。因此 D 可推出可导。
303-\answer{D}
304-
305-\solution{13}
--
315:\solution{15}
316-\approach{考察多项式导数，并利用三次导数多项式的判别式符号。}
317-令 $P(x)=x^5+2ax^3+3bx+4c$，则 $P'(x)=5x^4+6ax^2+3b$。置 $t=x^2\ge0$，得 $P'=5t^2+6at+3b$。条件 $3a^2-5b<0$ 即 $b>3a^2/5>0$，从而该二次式判别式 $36a^2-60b<0$，且首项系数正，故对一切 $t$ 均正。于是 $P$ 严格递增，且 $P(\pm\infty)=\pm\infty$，恰有一个实根。
318-\answer{B}
319-
320-\solution{16}
--
341:\solution{19}
342-\approach{将递推上界改写为关于 $x_n$ 的恒等式，再判断是否能保证趋于某个值。}
343-由 $2-1/x_n=x_n-(x_n-1)^2/x_n<x_n$，数列严格递减；题设还给出 $x_n>1/2$，故数列以下界有极限 $L\ge1/2$。取极限于递推上界得 $L\le2-1/L$，即 $(L-1)^2\le0$，所以 $L=1$。
344-\answer{B}
345-
346-\solution{20}
--
351:\solution{21}
352-\approach{比较零点处函数值、左右差商及函数符号。}
353-两侧函数值都趋于 $1$，且 $f(0)=1$，故连续。右侧 $x^{2x}=\exp(2x\ln x)$，故右差商为 $x^{2x}\,(x^{2x}-1)/x\sim2\ln x\to-\infty$；左侧 $x\mathrm e^x+1$ 的差商趋于 $1$，所以不可导。又 $x>0$ 时 $2x\ln x<0$，故 $x^{2x}<1$；$x<0$ 且充分接近零时 $x\mathrm e^x<0$，函数亦小于 $1$，因此 $0$ 为局部极大值点。
354-\answer{B}


## tool · 2026-11-10T15:21:22Z




## assistant · 2026-11-10T15:21:26Z

已停止编辑。修正了第 6、8、12、19、34、37、38、42、46、47、48 题。第 27 题正文与答案仍需复核；第 15、21 题还有待调整。我没有完成全篇逐题复核，题目顺序也尚未重排。
