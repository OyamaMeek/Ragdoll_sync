# 01a1b569-b16b-7ae0-a78e-1483bd2ca702

来源：codex

项目：/Users/oyamahappa/Documents/Agent/Codex

## developer · 2026-11-07T09:49:29Z

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


## developer · 2026-11-07T09:49:29Z

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
- When the user asks to create, fork, inspect, continue, hand off, pin, archive, unarchive, permanently delete, rename, or otherwise manage Codex threads, search for the relevant thread tool first: `create_thread`, `fork_thread`, `list_threads`, `list_archived_threads`, `read_thread`, `wait_threads`, `send_message_to_thread`, `handoff_thread`, `set_thread_archived`, `delete_thread`, or `set_thread_title`.
- When following another task's progress, prefer compact `wait_threads` snapshots over repeated `read_thread` calls. Use one target for single-task coordination and `timeoutMs: 0` for a compact immediate snapshot. `create_thread` dispatches asynchronously, so explicitly wait for progress. Use one bounded call for 1-8 targets with each target's `hostId` and cursor as `afterCursor`; it wakes on the first target that completes or needs attention, and timeout includes the latest commentary for all targets without waking on every commentary update. An up-to-date cursor suppresses already-delivered final text. Separate waits from one task may run serially. Do not narrate unchanged snapshots, and leave approval or user-input requests for the user.
- Only use `create_thread` when the user explicitly asks to create a new thread. Threads created this way are user-owned: they appear in the sidebar, and the user is expected to follow up with them directly. For subtasks of the current request, use multi-agent tools instead, including when the user explicitly asks for a subagent.
- After a successful `create_thread` call, emit `::created-thread{threadId="..."}` for a created thread or `::created-thread{clientThreadId="..."}` for queued worktree setup on its own line in your final response.

### Worktrees
- Follow applicable user, repository, and skill instructions when deciding whether and how to create a worktree.
- Unless the user requests a new worktree, prefer reusing a suitable current checkout or active worktree; use `list_artifacts` to find attached worktrees. An existing worktree's name need not match the new task.
- Use `create_worktree` for new worktrees. If the tool is deferred, look it up before running Git.

- For worktrees created with `create_worktree`, use `archive_worktree` when they are no longer needed. Use `restore_worktree` to recover archived work.

### Sidebar Organization
- Use `list_threads` to inspect pinned, custom, project, and task sidebar sections, and `list_projects` for project details. Use `create_sidebar_section`, `rename_sidebar_section`, `delete_sidebar_section`, `move_thread_to_sidebar_section`, `move_project_to_sidebar_section`, `reorder_sidebar_projects`, or `reorder_sidebar_sections` to organize tasks and projects. Moving an item into the pinned section pins it.

### Inline Code Comments
- Use the ::code-comment{...} directive when you need to attach feedback directly to specific code lines.
- Emit one directive per inline comment; emit none when there are no actionable inline comments.
- Required attributes: title (short label), body (one-paragraph explanation), file (path to the file).
- Optional attributes: start, end (1-based line numbers), priority (0-3).
- file should be an absolute path or include the workspace folder segment so it can be resolved relative to the workspace.
- Keep line ranges tight; end defaults to start.
- Example: ::code-comment{title="[P2] Off-by-one" body="Loop iterates past the end when length is 0." file="/path/to/foo.ts" start=10 end=11 priority=2}

### Git
- Branch prefix: `codex/`. Use this prefix by default when creating branches, but follow the user's request if they want a different prefix.
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
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/07/01a1b55b-3702-7c32-8099-1f95fc6d6c56`, `/Users/oyamahappa/Documents/Agent/Codex`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-11-07T09:49:29Z

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

## developer · 2026-11-07T09:49:29Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-07T09:49:29Z

# AGENTS.md instructions for /Users/oyamahappa/Documents/Agent/Codex

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

- 每次回答都先称呼用户为“妹妹”，再回复正文。
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
- 先做出能从头到尾跑通的最小版本，再逐步添加能力，最终完成全部已约定功能。不要为了尚未完成的复杂设计拆掉现有可用功能。
- 做架构选择时考虑后续维护，不采用明知很快需要推倒的临时方案。
- 设计方案前，查看成熟产品怎样解决同类问题；适合当前需求时，沿用已经验证过的做法。
- 默认提供一个能够满足需求的方案。确实需要多个方案时，应当分别说明成立条件，不机械地排列“稳妥”和“激进”选项。
- 完整设计可以分成小范围的执行步骤；每次完成一个可以独立验证的纵向功能切片，最终交付全部已约定功能。
- 避免把广泛重构混入功能开发。每个执行阶段原则上控制在约五个文件内，纯机械修改除外。
- 较大的独立工作区域分别实施和验证。

## 6. 代码与依赖

- 先遵循项目现有的命名、结构和风格，再考虑引入新模式。导出的函数和类使用清楚、可区分的名称。
- 保持组件职责清楚，相关代码放在合适的位置。
- 优先复用已有代码、标准库、平台能力和已经安装的依赖。成熟且维护良好的库能降低复杂度或提高可靠性时，优先使用；没有明确理由，不重写常见功能，不采用复杂绕行方案。
- 写新实现或添加新依赖前，先检查项目已有依赖的文档、类型和现成能力。
- 成熟文件格式使用标准库或成熟的第三方库解析，不自行编写字符串或字节解析器。
- 默认使用静态导入，只有确实需要运行时加载时才采用动态导入。必要的 Python 库直接 `import`，不使用 `try-except` 包装导入。
- 选择能满足当前需求的最简单实现，不为尚未出现的需求增加抽象、配置、接口或间接层。在满足完整需求与正确性的前提下，选择改动范围最小、清楚直接的实现。
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

- 本项目的远端仓库仅保留 `context/`、`docs/`、`memory/` 与根目录 `AGENTS.md`，仅对这些协作文档进行 Git 管理和推送。除非用户另行明确授权，不扩大上述范围。
- 用户交给助手处理的任务输入、源码、配置、测试、生成产物及其他范围外文件均只在本地处理，不暂存新增或修改内容、不提交、不推送；本地 `.gitignore` 采用上述保留范围，防止任务文件重新进入提交。
- 完成一个独立的逻辑单元，且适用的验证通过后，仅对上述允许范围内的本次改动创建原子化提交。
- 提交说明严格遵循 Conventional Commits，例如 `feat:`、`fix:`、`refactor:`、`test:`、`docs:`。
- 只暂存本次改动涉及的文件，禁止执行 `git add .`。文件包含用户已有修改时，检查并仅暂存本次修改对应的部分。
- 提交前检查内容，不提交 `.env`、API Keys、密钥、临时调试文件或 `.log` 文件。
- 用户已授权上述协作文档自动推送：推送前检查暂存文件及全部待推送提交，确认本次将上传的新增和修改均在上述允许范围内，范围外仅可包含用户授权的取消跟踪删除记录，再向当前分支已经配置的远端执行普通 `git push`，无需再次征求用户同意。若待推送提交含范围外新增或修改，停止推送并说明阻碍。不强制推送，不擅自更换远端或目标分支。
- 用户已授权从远端当前分支删除上述范围外的既有文件：仅通过 `git rm --cached` 取消跟踪、提交删除记录并普通推送，保留工作区现有文件；此前已缺失的文件保持缺失。不改写提交历史，历史版本仍可访问。
- 当前目录没有 Git 仓库、没有明确的推送目标，或缺少必要权限时，如实说明阻碍；不擅自初始化仓库、创建远端或宣称推送成功。
- Git 操作仍然遵守文件修改与恢复限制。

## 12. 开发记录

每次完成用户交付的任务时，在 `docs/CHANGELOG.md` 追加开发记录；文件不存在则创建，仅与本次允许范围内的协作文档一起提交，任务文件保留在本地；经用户授权的范围外取消跟踪删除记录可一并提交。
- 每次任务新增或更新的 `context/` 对话归档必须与对应的 `docs/CHANGELOG.md` 记录一并提交，并在提交后推送到当前分支已配置的远端。

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

## 工作空间清理与日志保留

- 用户会在任务结束后手动删除本工作空间中用过的文件。后续任务将这些历史任务文件的缺失视为正常清理，不报错、不追查、不反复确认，也不自动恢复或重新生成，直接继续当前任务。
- Git 状态中与当前任务无关的文件删除保持原样，不因这些删除阻塞工作，也不将其混入当前任务的提交。
- 持续保留 `docs/CHANGELOG.md`，每次完成任务后追加需求、实际改动、验证结果和 Git 提交信息，并提交、推送到已配置的 GitHub 远端。
- 历史任务文件已被删除不影响日志保留与上传；日志只记录实际发生的工作，不要求为补齐旧任务而重建文件。
- 每次任务结束前，将本次会话截至归档时的用户与助手可见消息按原顺序保存为 `context/YYYY/MM/DD/HH-mm-ss/对话.md`，目录使用本地时间；不收录系统或开发者指令、内部推理和工具输出。

</INSTRUCTIONS>
<environment_context>
  <cwd>/Users/oyamahappa/Documents/Agent/Codex</cwd>
  <shell>zsh</shell>
  <current_date>2026-11-07</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/Agent/Codex</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/Agent/Codex</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/07/01a1b55b-3702-7c32-8099-1f95fc6d6c56</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-07T09:49:29Z

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


## developer · 2026-11-07T09:49:29Z

<tools>
Added deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__pubmed
</tools>

## tool · 2026-11-07T09:49:34Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 10027)
Total output lines: 948

Warning: truncated output (original token count: 11275)
Total output lines: 988

---
name: "imagegen"
description: "Generate or edit raster images when the task benefits from AI-created bitmap visuals such as photos, illustrations, textures, sprites, mockups, or transparent-background cutouts. Use when Codex should create a brand-new image, transform an existing image, or derive visual variants from references, and the output should be a bitmap asset rather than repo-native code or vector. Do not use when the task is better handled by editing existing SVG/vector/code-native assets, extending an established icon or logo system, or building the visual directly in HTML/CSS/canvas."
---

# Image Generation Skill

Generates or edits images for the current project (for example website assets, game assets, UI mockups, product mockups, wireframes, logo design, photorealistic images, or infographics).

## Top-level modes and rules

This skill has exactly two top-level modes:

- **Default built-in tool mode (preferred):** built-in `image_gen` tool for image generation, editing, and transparent-image requests. Does not require `OPENAI_API_KEY`.
- **Fallback CLI mode:** `scripts/image_gen.py` CLI. Use when the user explicitly asks for or confirms the CLI/API/model path. Requires `OPENAI_API_KEY`.

Within CLI fallback, the CLI exposes three subcommands:

- `generate`
- `edit`
- `generate-batch`

Rules:
- Use the built-in `image_gen` tool by default for normal image generation and editing requests.
- Do not switch to CLI fallback for ordinary quality, size, or file-path control.
- For transparent images, ask built-in `image_gen` for a transparent background and preserve the generated alpha.
- Never silently switch from built-in `image_gen` or CLI `gpt-image-2` to CLI `gpt-image-1.5`; ask the user first unless they explicitly requested `gpt-image-1.5`.
- The word `batch` by itself does not mean CLI fallback. If the user asks for many assets or says to batch-generate assets without explicitly asking for CLI/API/model controls, stay on the built-in path and issue one built-in call per requested asset or variant.
- If the built-in tool fails or is unavailable, tell the user the CLI fallback exists and that it requires `OPENAI_API_KEY`. Proceed only if the user explicitly asks for that fallback.
- If the user explicitly asks for CLI mode, use the bundled `scripts/image_gen.py` workflow. Do not create one-off SDK runners.
- Never modify `scripts/image_gen.py`. If something is missing, ask the user before doing anything else.

Built-in save-path policy:
- In built-in tool mode, Codex saves generated images under `$CODEX_HOME/*` by default.
- Do not describe or rely on OS temp as the default built-in destination.
- Do not describe or rely on a destination-path argument (if any) on the built-in `image_gen` tool. If a specific location is needed, generate first and then move or copy the selected output from `$CODEX_HOME/generated_images/...`.
- Save-path precedence in built-in mode:
  1. If the user names a destination, move or copy the selected output there.
  2. If the image is meant for the current project, move or copy the final selected image into the workspace before finishing.
  3. If the image is only for preview or brainstorming, render it inline; the underlying file can remain at the default `$CODEX_HOME/*` path.
- Never leave a project-referenced asset only at the default `$CODEX_HOME/*` path.
- Do not overwrite an existing asset unless the user explicitly asked for replacement; otherwise create a sibling versioned filename such as `hero-v2.png` or `item-icon-edited.png`.

Shared prompt guidance for both modes lives in `references/prompting.md` and `references/sample-prompts.md`.

Fallback-only docs/resources for CLI mode:
- `references/cli.md`
- `references/image-api.md`
- `references/codex-network.md`
- `scripts/image_gen.py`

## When to use
- Generate a new image (concept art, product shot, cover, website hero)
- Generate a new image using one or more reference images for style, composition, or mood
- Edit an existing image (inpainting, lighting or weather transformations, background replacement, object removal, compositing, transparent background)
- Produce many assets or variants for one task

## When not to use
- Extending or matching an existing SVG/vector icon set, logo system, or illustration library inside the repo
- Creating simple shapes, diagrams, wireframes, or icons that are better produced directly in SVG, HTML/CSS, or canvas
- Making a small project-local asset edit when the source file already exists in an editable native format
- Any task where the user clearly wants deterministic code-native output instead of a generated bitmap

## Decision tree

Think about two separate questions:

1. **Intent:** is this a new image or an edit of an existing image?
2. **Execution strategy:** is this one asset or many assets/variants?

Intent:
- If the user wants to modify an existing image while preserving parts of it, treat the request as **edit**.
- If the user provides images only as references for style, composition, mood, or subject guidance, treat the request as **generate**.
- If the user provides no images, treat the request as **generate**.

Built-in edit semantics:
- Built-in edit mode is for images already visible in the conversation context, such as attached images or images generated earlier in the thread.
- If the user wants to edit a local image file with the built-in tool, first load it with built-in `view_image` tool so the image is visible in the conversation context, then proceed with the built-in edit flow.
- Do not promise arbitrary filesystem-path editing through the built-in tool.
- If a local file still needs direct file-path control, masks, or other explicit CLI-only parameters, use the explicit CLI fallback only when the user asks for it.
- For edits, preserve invariants aggressively and save non-destructively by default.

Execution strategy:
- In the built-in default path, produce many assets or variants by issuing one `image_gen` call per requested asset or variant.
- In the CLI fallback path, use the CLI `generate-batch` subcommand only when the user explicitly chose CLI mode and needs many prompts/assets.
- For many distinct assets, do not use `n` as a substitute for separate prompts. `n` is for variants of one prompt; distinct assets need distinct built-in calls or distinct CLI `generate-batch` jobs.

Assume the user wants a new image unless they clearly ask to change an existing one.

## Workflow
1. Decide the top-level mode: built-in by default, including transparent-output requests; fallback CLI only if explicitly requested or confirmed.
2. Decide the intent: `generate` or `edit`.
3. Decide whether the output is preview-only or meant to be consumed by the current project.
4. Decide the execution strategy: single asset vs repeated built-in calls vs CLI `generate-batch`.
5. Collect inputs up front: prompt(s), exact text (verbatim), constraints/avoid list, and any input images.
6. For every input image, label its role explicitly:
   - reference image
   - edit target
   - supporting insert/style/compositing input
7. If the edit target is only on the local filesystem and you are staying on the built-in path, inspect it with `view_image` first so the image is available in conversation context.
8. If the user asked for a photo, illustration, sprite, product image, banner, or other explicitly raster-style asset, use `image_gen` rather than substituting SVG/HTML/CSS placeholders. If the request is for an icon, logo, or UI graphic that should match existing repo-native SVG/vector/code assets, prefer editing those directly instead.
9. Augment the prompt based on specificity:
   - If the user's prompt is already specific and detailed, normalize it into a clear spec without adding creative requirements.
   - If the user's prompt is generic, add tasteful augmentation only when it materially improves output quality.
10. Use the built-in `image_gen` tool by default.
11. For transparent-output requests, ask built-in `image_gen` for a transparent background and preserve the generated alpha channel.
12. Inspect outputs and validate: subject, style, composition, text accuracy, and invariants/avoid items.
13. Iterate with a single targeted change, then re-check.
14. For preview-only work, render the image inline; the underlying file may remain at the default `$CODEX_HOME/generated_images/...` path.
15. For project-bound work, move or copy the selected artifact into the workspace and update any consuming code or references. Never leave a project-referenced asset only at the default `$CODEX_HOME/generated_images/...` path.
16. For batches or multi-asset requests, persist every requested deliverable final in the workspace unless the user explicitly asked to keep outputs preview-only. Discarded variants do not need to be kept unless requested.
17. If the user explicitly chooses or confirms the CLI fallback, then use the fallback-only docs for model, quality, size, `input_fidelity`, masks, output format, output paths, and network setup.
18. Always report the final saved path(s) for any workspace-bound asset(s), plus the final prompt or prompt set and whether the built-in tool or fallback CLI mode was used.

## Transparent image requests

Ask built-in `image_gen` for a genuinely transparent background and preserve its alpha.

## Prompt augmentation

Reformat user prompts into a structured, production-oriented spec. Make the user's goal clearer and more actionable, but do not blindly add detail.

Treat this as prompt-shaping guidance, not a closed schema. Use only the lines that help, and add a short extra labeled line when it materially improves clarity.

### Specificity policy

Use the user's prompt specificity to decide how much augmentation is appropriate:

- If the prompt is already specific and detailed, preserve that specificity and only normalize/structure it.
- If the prompt is generic, you may add tasteful augmentation when it will materially improve the result.

Allowed augmentations:
- composition or framing hints
- polish level or intended-use hints
- practical layout guidance
- reasonable scene concreteness that supports the stated request

Not allowed augmentations:
- extra characters or objects that are not implied by the request
- brand names, slogans, palettes, or narrative beats that are not implied
- arbitrary side-specific placement unless the surrounding layout supports it

## Use-case taxonomy (exact slugs)

Classify each request into one of these buckets and keep the slug consistent across prompts and references.

Generate:
- photorealistic-natural — candid/editorial lifestyle scenes with real texture and natural lighting.
- product-mockup — product/packaging shots, catalog imagery, merch concepts.
- ui-mockup — app/web interface mockups and wireframes; specify the desired fidelity.
- infographic-diagram — diagrams/infographics with structured layout and text.
- scientific-educational — classroom explainers, scientific diagrams, and learning visuals with required labels and accuracy constraints.
- ads-marketing — campaign concepts and ad creatives with audience, brand position, scene, and exact tagline/copy.
- productivity-visual — slide, chart, workflow, and data-heavy business visuals.
- logo-brand — logo/mark exploration, vector-friendly.
- illustration-story — comics, children’s book art, narrative scenes.
- stylized-concept — style-driven concept art, 3D/stylized renders.
- historical-scene — period-accurate/world-knowledge scenes.

Edit:
- text-localization — translate/replace in-image text, preserve layout.
- identity-preserve — try-on, person-in-scene; lock face/body/pose.
- precise-object-edit — remove/replace a specific element (including interior swaps).
- lighting-weather — time-of-day/season/atmosphere changes only.
- background-extraction — transparent background / clean cutout. Ask built-in `image_gen` for actual transparency.
- style-transfer — apply reference style while changing subject/scene.
- compositing — multi-image insert/merge with matched lighting/perspective.
- sketch-to-render — drawing/line art to photoreal render.

## Shared prompt schema

Use the following labeled spec as shared prompt scaffolding for both top-level modes:

```text
Use case: <taxonomy slug>
Asset type: <where the asset will be used>
Primary request: <user's main prompt>
Input images: <Image 1: role; Image 2: role> (optional)
Scene/backdrop: <environment>
Subject: <main subject>
Style/medium: <photo/illustration/3D/etc>
Composition/framing: <wide/close/top-down; placement>
Lighting/mood: <lighting + mood>
Color palette: <palette notes>
Materials/textures: <surface details>
Text (verbatim): "<exact text>"
Constraints: <must keep/must avoid>
Avoid: <negative constraints>
```

Notes:
- `Asset type` and `Input images` are prompt scaffolding, not dedicated CLI flags.
- `Scene/backdrop` refers to the visual setting. It is not the same as the fallback CLI `background` parameter, which controls output transparency behavior.
- Fallback-only execution notes such as `Quality:`, `Input fidelity:`, masks, output format, and output paths belong in the CLI path only. Do not treat them as built-in `image_gen` tool arguments.

Augmentation rules:
- Keep it short.
- Add only the details needed to improve the prompt materially.
- For edits, explicitly list invariants (`change only X; keep Y unchanged`).
- If any critical detail is missing and blocks success, ask a question; otherwise proceed.

## Examples

### Generation example (hero image)
```text
Use case: product-mockup
Asset type: landing page hero
Primary request: a minimal hero image of a ceramic coffee mug
Style/medium: clean product photography
Composition/framing: wide composition with usable negative space for page copy if needed
Lighting/mood: soft studio lighting
Constraints: no logos, no text, no watermark
```

### Edit example (invariants)
```text
Use case: precise-object-edit
Asset type: product photo background replacement
Primary request: replace only the background with a warm sunset gradient
Constraints: change only the background; keep the product and its edges unchanged; no text; no watermark
```

## Prompting best practices
- Structure prompt as scene/backdrop -> subject -> details -> constraints.
- Include intended use (ad, UI mock, infographic) to set the mode and polish level.
- Use camera/composition language for photorealism.
- Only use SVG/vector stand-ins when the user explicitly asked for vector output or a non-image placeholder.
- Quote exact text and specify typography + placement.
- For tricky words, spell them letter-by-letter and require verbatim rendering.
- For multi-image inputs, reference images by index and describe how they should be used.
- For edits, repeat invariants every iteration to reduce drift.
- Iterate with single-change follow-ups.
- If the prompt is generic, add only the extra detail that will materially help.
- If the prompt is already detailed, normalize it instead of expanding it.
- For CLI fallback only, see `references/cli.md` and `references/image-api.md` for model, `quality`, `input_fidelity`, masks, output format, and output-path guidance.
- For transparent images, ask built-in `image_gen` for actual transparency and preserve its alpha.

More principles shared by both modes: `references/prompting.md`.
Copy/paste specs shared by both modes: `references/sample-prompts.md`.

## Guidance by asset type
Asset-type templates (website assets, game assets, wireframes, logo) are consolidated in `references/sample-prompts.md`.

## gpt-image-2 guidance for CLI fallback

The fallback CLI defaults to `gpt-image-2`.

- Use `gpt-image-2` for new CLI/API workflows unless the user confirms a different model.
- CLI `gpt-image-2` does not support `background=transparent`; ask before using `gpt-image-1.5` unless the user explicitly requested that model.
- `gpt-image-2` always uses high fidelity for image inputs; do not set `input_fidelity` with this model.
- `gpt-image-2` supports `quality` values `low`, `medium`, `high`, and `auto`.
- Use `quality low` for fast drafts, thumbnails, and quick iterations. Use `medium`, `high`, or `auto` for final assets, dense text, diagrams, identity-sensitive edits, or high-resolution outputs.
- Square images are typically fastest to generate. Use `1024x1024` for fast square drafts.
- If the user asks for 4K-style output, use `3840x2160` for landscape or `2160x3840` for portrait.
- `gpt-image-2` size may be `auto` or `WIDTHxHEIGHT` if all constraints hold: max edge `<= 3840px`, both edges multiples of `16px`, long-to-short ratio `<= 3:1`, total pixels between `655,360` and `8,294,400`.

Popular `gpt-image-2` sizes:
- `1024x1024` square
- `1536x1024` landscape
- `1024x1536` portrait
- `2048x2048` 2K square
- `2048x1152` 2K landscape
- `3840x2160` 4K landscape
- `2160x3840` 4K portrait
- `auto`

## Fallback CLI mode only

### Temp and output conventions
These conventions apply only to the CLI fallback. They do not describe built-in `image_gen` output behavior.
- Use `tmp/imagegen/` for intermediate files (for example JSONL batches); delete them when done.
- Write final artifacts under `output/imagegen/`.
- Use `--out` or `--out-dir` to control output paths; keep filenames stable and descriptive.

### Dependencies
Prefer `uv` for dependency management in this repo.

Required Python package:
```bash
uv pip install openai
```

Optional for image inspection and downscaling:
```bash
uv pip install pillow
```

Portability note:
- If you are using the installed skill outside this repo, install dependencies into that environment with its package manager.
- In uv-managed environments, `uv pip install ...` remains the preferred path.

### Environment
- `OPENAI_API_KEY` must be set for live API calls.
- Do not ask the user for `OPENAI_API_KEY` when using the built-in `image_gen` tool.
- Never ask the user to paste the full key in chat. Ask them to set it locally and confirm when ready.

If the key is missing, give the user these steps:
1. Create an API key in the OpenAI platform UI: https://platform.openai.com/api-keys
2. Set `OPENAI_API_KEY` as an environment variable in their system.
3. Offer to guide them through setting the environment variable for their OS/shell if needed.

If installation is not possible in this environment, tell the user which dependency is missing and how to install it into their active environment.

### Script-mode notes
- CLI commands + examples: `references/cli.md`
- API parameter quick reference: `references/image-api.md`
- Network approvals / sandbox settings for CLI mode: `references/codex-network.md`

## Reference map
- `references/prompting.md`: shared prompting principles for both modes.
- `references/sample-prompts.md`: shared copy/paste prompt recipes for both modes.
- `references/cli.md`: fallback-only CLI usage via `scripts/image_gen.py`.
- `references/image-api.md`: fallback-only API/CLI parameter reference.
- `references/codex-network.md`: fallback-only network/sandbox troubleshooting for CLI mode.
- `scripts/image_gen.py`: fallback-only CLI implementation. Use only when the user explicitly chooses or confirms CLI mode.
Create one horizontal look-direction strip for Codex pet `clawd`, atlas row 10.

Use the attached canonical base, completed standard contact sheet, layout guide, and approved four-cardinal strip for identity, scale, registration, spacing, direction semantics, and cross-row continuity. Read `qa/look-mechanics.md` and follow its pet-specific movement and eye/prop mechanics. The approved cardinal strip and completed coherent row 9 are authoritative. Use the cardinals for direction meaning and row 9 for cross-row identity, scale, registration, and continuity.

COHERENT SYNTHESIS LOCK: produce one unified eight-pose row. Do not paste, tile, or independently restyle individual cells. Every final cell must be drawn …27 tokens truncated…同时存在水平和垂直位移。保留双眼可读，近水平朝向可压窄远侧眼，但不隐藏整张脸。157.5至180及337.5至000只移动一步，不发生翻面或突然复位。注视幅度必须在192×208成品尺寸可识别，所有方向均与中立正面区分。
{
  "schema_version": 1,
  "created_at": "2026-11-07T09:35:15.825386+00:00",
  "run_dir": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet",
  "primary_generation_skill": "$imagegen",
  "jobs": [
    {
      "id": "base",
      "kind": "base-pet",
      "status": "complete",
      "prompt_file": "prompts/base-pet.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        }
      ],
      "output_path": "decoded/base.png",
      "depends_on": [],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "source_path": "decoded/base.png"
    },
    {
      "id": "idle",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/idle.md",
      "retry_prompt_file": "prompts/row-retries/idle.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/idle.png",
          "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/idle.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "no deterministic derivation is configured for this state"
      },
      "mirror_policy": {},
      "source_path": "decoded/idle.png"
    },
    {
      "id": "running-right",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/running-right.md",
      "retry_prompt_file": "prompts/row-retries/running-right.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/running-right.png",
          "role": "layout guide for 8 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/running-right.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "no deterministic derivation is configured for this state"
      },
      "mirror_policy": {},
      "source_path": "decoded/running-right.png"
    },
    {
      "id": "running-left",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/running-left.md",
      "retry_prompt_file": "prompts/row-retries/running-left.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/running-left.png",
          "role": "layout guide for 8 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        },
        {
          "path": "decoded/running-right.png",
          "role": "rightward gait reference for leftward row decision"
        }
      ],
      "output_path": "decoded/running-left.png",
      "depends_on": [
        "base",
        "running-right"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base",
        "running-right"
      ],
      "derivation_policy": {
        "may_derive": true,
        "may_derive_from": "running-right",
        "derivation": "framewise-horizontal-mirror-preserving-order",
        "requires_explicit_approval": true,
        "fallback_generation_skill": "$imagegen"
      },
      "mirror_policy": {
        "may_derive": true,
        "may_derive_from": "running-right",
        "derivation": "framewise-horizontal-mirror-preserving-order",
        "requires_explicit_approval": true,
        "fallback_generation_skill": "$imagegen"
      },
      "source_path": "decoded/running-right.png",
      "derived_from": "running-right",
      "completed_at": "2026-11-07T09:38:32.701932+00:00",
      "metadata": {
        "width": 2172,
        "height": 724,
        "mode": "RGBA",
        "format": "PNG"
      },
      "mirror_decision": {
        "approved": true,
        "approved_at": "2026-11-07T09:38:32.701932+00:00",
        "note": "Pixel Clawd has no held prop, text or directional marking; frame-local mirroring preserves identity and gait order. Side shading flips consistently with the side view.",
        "transform": "framewise-horizontal-mirror-preserving-order"
      }
    },
    {
      "id": "waving",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/waving.md",
      "retry_prompt_file": "prompts/row-retries/waving.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/waving.png",
          "role": "layout guide for 4 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/waving.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "state requires its own generated animation semantics"
      },
      "mirror_policy": {},
      "source_path": "decoded/waving.png"
    },
    {
      "id": "jumping",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/jumping.md",
      "retry_prompt_file": "prompts/row-retries/jumping.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/jumping.png",
          "role": "layout guide for 5 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/jumping.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "state requires its own generated animation semantics"
      },
      "mirror_policy": {},
      "source_path": "decoded/jumping.png",
      "extraction_note": "stable-slots preserves source jump height; auto component centering erases vertical displacement",
      "qa_note": "Revised lower jump; 33px ascent, row-wide registration and independent motion QA passed"
    },
    {
      "id": "failed",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/failed.md",
      "retry_prompt_file": "prompts/row-retries/failed.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/failed.png",
          "role": "layout guide for 8 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/failed.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "state requires its own generated animation semantics"
      },
      "mirror_policy": {},
      "source_path": "decoded/failed.png"
    },
    {
      "id": "waiting",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/waiting.md",
      "retry_prompt_file": "prompts/row-retries/waiting.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/waiting.png",
          "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/waiting.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "state requires its own generated animation semantics"
      },
      "mirror_policy": {},
      "source_path": "decoded/waiting.png"
    },
    {
      "id": "running",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/running.md",
      "retry_prompt_file": "prompts/row-retries/running.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/running.png",
          "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/running.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "state requires its own generated animation semantics"
      },
      "mirror_policy": {},
      "source_path": "decoded/running.png"
    },
    {
      "id": "review",
      "kind": "row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/review.md",
      "retry_prompt_file": "prompts/row-retries/review.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/review.png",
          "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        }
      ],
      "output_path": "decoded/review.png",
      "depends_on": [
        "base"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "parallelizable_after": [
        "base"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "state requires its own generated animation semantics"
      },
      "mirror_policy": {},
      "source_path": "decoded/review.png"
    },
    {
      "id": "look-cardinals",
      "kind": "look-cardinal-strip",
      "status": "complete",
      "prompt_file": "prompts/look-cardinals.md",
      "repair_prompt_files": {
        "000": "prompts/look-anchor-repairs/000.md",
        "090": "prompts/look-anchor-repairs/090.md",
        "180": "prompts/look-anchor-repairs/180.md",
        "270": "prompts/look-anchor-repairs/270.md"
      },
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/look-cardinals.png",
          "role": "layout guide for four cardinal slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        },
        {
          "path": "qa/contact-sheet.png",
          "role": "approved standard-row identity, scale, and baseline reference"
        }
      ],
      "output_path": "decoded/look-cardinals.png",
      "extracted_output_paths": [
        "decoded/look-anchors/000.png",
        "decoded/look-anchors/090.png",
        "decoded/look-anchors/180.png",
        "decoded/look-anchors/270.png"
      ],
      "approved_strip_path": "decoded/look-anchors-approved.png",
      "depends_on": [
        "idle",
        "running-right",
        "running-left",
        "waving",
        "jumping",
        "failed",
        "waiting",
        "running",
        "review"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "look_mechanics_file": "qa/look-mechanics.md",
      "directions": [
        "000",
        "090",
        "180",
        "270"
      ],
      "packaging_eligible": false,
      "parallelizable_after": [
        "idle",
        "running-right",
        "running-left",
        "waving",
        "jumping",
        "failed",
        "waiting",
        "running",
        "review"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "cardinal directions require grounded pet-specific generation"
      },
      "source_path": "decoded/look-cardinals.png",
      "qa_note": "Four extracted cardinals approved: printed eyes visibly high, screen-right, low, screen-left; fixed feet and original eye design"
    },
    {
      "id": "look-row-9",
      "kind": "look-row-strip",
      "status": "complete",
      "prompt_file": "prompts/rows/look-row-9.md",
      "retry_prompt_file": "prompts/row-retries/look-row-9.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/look-row-9.png",
          "role": "layout guide for 8 direction slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        },
        {
          "path": "qa/contact-sheet.png",
          "role": "approved standard-row identity, scale, and baseline reference"
        },
        {
          "path": "decoded/look-anchors-approved.png",
          "role": "approved cardinal reference strip in order 000 up, 090 screen-right, 180 down, 270 screen-left; interpolate intermediate directions evenly"
        }
      ],
      "output_path": "decoded/look-row-9.png",
      "depends_on": [
        "look-cardinals"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "look_mechanics_file": "qa/look-mechanics.md",
      "directions": [
        "000",
        "022.5",
        "045",
        "067.5",
        "090",
        "112.5",
        "135",
        "157.5"
      ],
      "parallelizable_after": [
        "look-cardinals"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "look directions require grounded pet-specific generation"
      },
      "coherent_synthesis_required": true,
      "individual_cell_packaging_allowed": false,
      "packaging_eligible": true,
      "source_path": "decoded/look-row-9.png",
      "qa_note": "Registered eight cells pass edges; eyes progress from high centered to screen-right then lower-right; fixed feet, consistent identity and no reversals. 022.5 is subtle but both axes remain readable."
    },
    {
      "id": "look-row-10",
      "kind": "look-row-strip",
      "status": "pending",
      "prompt_file": "prompts/rows/look-row-10.md",
      "retry_prompt_file": "prompts/row-retries/look-row-10.md",
      "input_images": [
        {
          "path": "references/reference-01.png",
          "role": "pet reference"
        },
        {
          "path": "references/layout-guides/look-row-10.png",
          "role": "layout guide for 8 direction slots; use for spacing only, do not copy guide lines"
        },
        {
          "path": "references/canonical-base.png",
          "role": "canonical identity reference"
        },
        {
          "path": "qa/contact-sheet.png",
          "role": "approved standard-row identity, scale, and baseline reference"
        },
        {
          "path": "decoded/look-anchors-approved.png",
          "role": "approved cardinal reference strip in order 000 up, 090 screen-right, 180 down, 270 screen-left; interpolate intermediate directions evenly"
        },
        {
          "path": "decoded/look-row-9.png",
          "role": "completed first half of the clockwise look loop for row 10 continuity"
        }
      ],
      "output_path": "decoded/look-row-10.png",
      "depends_on": [
        "look-cardinals",
        "look-row-9"
      ],
      "generation_skill": "$imagegen",
      "requires_grounded_generation": true,
      "allow_prompt_only_generation": false,
      "identity_reference_paths": [
        "references/canonical-base.png"
      ],
      "look_mechanics_file": "qa/look-mechanics.md",
      "directions": [
        "180",
        "202.5",
        "225",
        "247.5",
        "270",
        "292.5",
        "315",
        "337.5"
      ],
      "parallelizable_after": [
        "look-cardinals",
        "look-row-9"
      ],
      "derivation_policy": {
        "may_derive": false,
        "reason": "look directions require grounded pet-specific generation"
      },
      "coherent_synthesis_required": true,
      "individual_cell_packaging_allowed": false,
      "packaging_eligible": true
    }
  ]
}


## tool · 2026-11-07T09:49:40Z


Script completed
Wall time 0.1 seconds
Output:

Create one horizontal look-direction strip for Codex pet `clawd`, atlas row 10.

Use the attached canonical base, completed standard contact sheet, layout guide, and approved four-cardinal strip for identity, scale, registration, spacing, direction semantics, and cross-row continuity. Read `qa/look-mechanics.md` and follow its pet-specific movement and eye/prop mechanics. The approved cardinal strip and completed coherent row 9 are authoritative. Use the cardinals for direction meaning and row 9 for cross-row identity, scale, registration, and continuity.

COHERENT SYNTHESIS LOCK: produce one unified eight-pose row. Do not paste, tile, or independently restyle individual cells. Every final cell must be drawn together with the same face construction, body proportions, line/render quality, lighting, materials, scale, baseline, and registration.

Output exactly 8 complete full-body frames in this exact left-to-right order: 180, 202.5, 225, 247.5, 270, 292.5, 315, 337.5. Degrees are clockwise: 000 is up, 090 right, 180 down, and 270 left. Neutral/front is not part of this row.

DIRECTION TARGETS — use these to shape the coherent row, not as pixel-level landmark gates:

1. `180`: vertical DOWN; no horizontal requirement.
2. `202.5`: horizontal SCREEN-LEFT and vertical DOWN.
3. `225`: horizontal SCREEN-LEFT and vertical DOWN.
4. `247.5`: horizontal SCREEN-LEFT and vertical DOWN.
5. `270`: horizontal SCREEN-LEFT; no vertical requirement.
6. `292.5`: horizontal SCREEN-LEFT and vertical UP.
7. `315`: horizontal SCREEN-LEFT and vertical UP.
8. `337.5`: horizontal SCREEN-LEFT and vertical UP.

Cardinals must be unmistakable. Intermediate poses should broadly occupy the intended quadrant and advance naturally through the ordered loop. Minor pupil, nose, eyelid, or aiming-feature deviations are acceptable when the overall direction, continuity, identity, and motion remain coherent. Do not deform the character merely to make every intermediate axis independently obvious.

SCREEN-COORDINATE LOCK: screen-left means the viewer's left image edge, never the character's own left. The row should travel naturally through the left half of the loop. Near-vertical 202.5 and 337.5 may have subtle horizontal cues; prioritize a coherent arc over exact pupil or nose placement.

HARD LAYOUT AND CONTINUITY CONTRACT — DETERMINISTIC REGISTRATION: draw exactly eight separated pose groups in left-to-right direction order. Keep enough chroma-only space between neighboring poses that each complete pose can be detected without cutting through foreground. Approximate the guide's equal spacing, but do not distort a pose merely to hit an exact source-canvas coordinate; deterministic assembly will crop the eight ordered groups, then apply one shared scale and baseline.

Use the same body height, head size, baseline, and planted-body position across the generated family. Never overlap neighboring poses, merge two poses into one connected group, crop foreground at the outer canvas edge, or resize one pose independently.

Keep the feet, base, or lower torso planted at the same coordinates across all eight frames. Express direction through the eyes, face, head, upper body, and physically appropriate prop movement, not by moving, rotating, or rescaling the entire sprite.

Place one centered pose in each invisible equal-width slot on flat pure blue #0000FF. Change only the natural parts needed to express gaze: eyes, eyelids, head, face, neck, upper body, appendages, and constrained prop follow-through. Keep identity, silhouette, materials, palette, markings, and props consistent.

ROW-BOUNDARY LOCK: 180 must continue directly from row 9's 157.5, matching its body size, baseline, planted anchor, expression, and construction. 337.5 must be one even 22.5-degree step before 000: nearly up-facing while remaining on the overall left-hand arc. Do not distort pupils, nose, or body geometry merely to exaggerate the subtle horizontal component.

PRE-RETURN CHECK: reject this result if it does not contain eight separated pose groups in the required order; neighboring poses overlap; foreground is cropped at the outer canvas edge; any frame changes sprite scale, body or head size, baseline, or planted-body position; the row visibly reverses into the wrong half of the loop; or 180 does not continue from 157.5 or 337.5 does not flow evenly into 000. Minor intermediate pupil or nose deviations are not rejection reasons. Exact cell cropping, resizing, and recentering happen deterministically after generation.

Do not rotate, skew, or tilt the whole sprite to fake gaze. Do not add replacement/googly eyes, labels, degree text, arrows, clocks, grids, shadows, glows, scenery, detached effects, or chroma-key colors inside the pet.
# Clawd注视机制

Clawd为单块矩形像素身体，两只暗色矩形眼睛直接画在身体表面，没有眼白、瞳孔、鼻子或独立头部。四只脚与下半身保持原地锚定，两只手不挥动、不携带道具。

注视由整对矩形眼睛在身体表面的水平与竖直位移主导，上半身表面轻微向目标方向转向，保持矩形身体、固定比例及像素网格。不得增加眼白或圆眼，不得旋转整个角色，不得改变脚的注册位置。印刷式眼睛可沿原表面移动，这是本角色自然的注意方向表达。

- 000向上：眼睛明显升至身体上部，额头留白缩小，身体顶部稍显可见，双眼水平居中。
- 090向画面右侧：眼睛整体移至身体右半部，左侧留白明显增大，上半身朝右轻微转向，眼睛保持中间高度。
- 180向下：眼睛明显降至身体下部，额头留白增大，双眼水平居中；脚与身体下缘保持稳定。
- 270向画面左侧：与090在屏幕坐标中相反，眼睛整体移至身体左半部，右侧留白增大。

每22.5度按相同节奏插值，所有斜方向都必须同时存在水平和垂直位移。保留双眼可读，近水平朝向可压窄远侧眼，但不隐藏整张脸。157.5至180及337.5至000只移动一步，不发生翻面或突然复位。注视幅度必须在192×208成品尺寸可识别，所有方向均与中立正面区分。
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/canonical-base.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/failed.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/idle.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/jumping.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/look-cardinals.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/look-row-10.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/look-row-9.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/review.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/running-left.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/running-right.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/running.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/waiting.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/layout-guides/waving.png
/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/references/reference-01.png


## tool · 2026-11-07T09:49:45Z


Script completed
Wall time 0.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/64f0ca531768973e613e6b005f9cafd6869ca81eeca05198529ffcd39b46b5dc.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/6d67d00f341f39f1535fd37776b19b366e4e78ee38f7ef002d368ecb1d765c40.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/29d3a5a473daebc1d3f4717c1ee3e21f6b904c7d19ba23ca2f954b560d26169b.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c27b0e5f1950c7be6ede8a749dfd840c5b3111e66467b1d0ad47c5362ccde9e7.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/7cc4cd3a4eb18d42777ce1d942ca0235c47d7550c54a8d521f26494ea1c76de3.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/f7cb6bf461e21f354feaeae42a64f0207d998ca2e183203c28332f821ad36a35.png",
  "detail": "high"
}

## developer · 2026-11-07T09:49:45Z

<image_resize_notice>
Image 1 of 6 in the preceding tool output was resized from 1920x1440 to 1824x1368 pixels.
Image 6 of 6 in the preceding tool output was resized from 2172x724 to 2048x683 pixels.
</image_resize_notice>

## tool · 2026-11-07T09:50:01Z


Script failed
Wall time 0.0 seconds
Output:

Script error:
`referenced_image_paths` must contain at most 5 paths

## tool · 2026-11-07T09:50:37Z


Script completed
Wall time 18.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/45b064d5683664f866d390de0246f2099b4ea2b212d703bbc01246a46c9df2dc.png",
  "detail": "high"
}
Generated images are saved to /Users/oyamahappa/.codex/generated_images/01a1b569-b16b-7ae0-a78e-1483bd2ca702 as /Users/oyamahappa/.codex/generated_images/01a1b569-b16b-7ae0-a78e-1483bd2ca702/exec-16c27189-3b31-45e5-b386-f9613ca8d956.png by default.
If you need to use a generated image at another path, copy it and leave the original in place unless the user explicitly asks you to delete it.
The generated image is already displayed to the user. There is no need to render it in the final response as a Markdown image or file link.

## developer · 2026-11-07T09:50:37Z

<image_resize_notice>
Image 1 of 1 in the preceding tool output was resized from 2172x724 to 2048x683 pixels.
</image_resize_notice>

## assistant · 2026-11-07T09:50:47Z

selected_source: /Users/oyamahappa/.codex/generated_images/01a1b569-b16b-7ae0-a78e-1483bd2ca702/exec-16c27189-3b31-45e5-b386-f9613ca8d956.png  
qa_note: One coherent strip with eight separated full-body poses on pure blue. The eyes progress from low centered through leftward to high-left; feet and baseline stay fixed, with no extra facial features or effects. Final up-left steps look subtle and similar to each other, so review against row 9 before approval.
