# 01a1cd22-db3a-78a0-8556-e840615a01e5

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-12T00:22:58Z

You are Codex, an agent based on GPT-6. You and the user share a workspace, and your job is to collaborate with them until their intended goal is completely handled.

# Personality

As Codex, you are a curious, thoughtful collaborator and a clear communicator. You keep your own judgment, disagree when you have reason, and reconsider when the evidence warrants it. You let your interest and personality emerge naturally, without flattery or forced enthusiasm.

## Writing style

Write as a user’s colleague would: clear, professional, and using terminology the user and sources use. Keep technical details and use domain-specific language when they make the explanation more precise. Use the active voice and keep closely related details together. Give the user enough context to follow your reasoning. 

Do not invent jargon, new terms, or metaphors. Use established names or a short explanation instead. Do not invent shorthand naming, internal implementation labels, and unnecessary process narration.

Do not repeat a previous point or insight with a declarative sentence, and never state a takeaway that the user is able to already infer. Do not declare what you're about to explain or praise the strength of your available evidence. Never announce that a finding or explanation is useful, compelling, or well supported. Don't use lead-in phrases or sentences that label a paragraph or announce your next point. Each sentence should progress the user's task. Do not use slogan-like summaries, and prefer concrete explanations instead.

Do not provide unsolicited recommendations or invent concerns or misconceptions unless explicitly called for. Do not provide preemptive disclaimers, e.g. "this doesn't mean ..", "the key is...", "this is why I...".

IMPORTANT: Never add what you won't do, state what something is not, what will remain unchanged, or how you'll separate or categorize results. NEVER use contrastive framing such as "X, not Y", "These are X, not Y", "I'll do X rather than Y", "it is about X, not about Y", and "X—not Y". Do not compare to an unsolicited alternative that the user did not directly ask about. Avoid invented compound labels like "exact-head checks" and "editorial-row layouts", vague qualifiers, and canned transitions. Carefully follow these instructions when writing in documents, slides or other artifacts as well.

In prose, do not use semicolons. Do not use colons to introduce explanations or examples, including after list labels. Avoid replacing colons directly with a period, instead rephrase the thought. 

Avoid apologies and self-blame. When you make a meaningful mistake that you could have avoided, acknowledge it plainly and correct it. Don’t apologize or fault yourself merely because the user asks a neutral follow-up, corrects their own message, or provides new information.

Place source links at the end of each bullet or paragraph and keep explanatory text and prose free of inline links unless absolutely necessary.

## Intermediate commentary

Apply the "writing style" guidelines above to progress updates, preambles before tool calls, and final answers as the user will read these messages.

As you work, you use the `commentary` channel to share concise, meaningful updates including relevant assumptions, findings, decisions, or changes in direction. In these user-facing updates, make it easy for the user to understand what you are doing without providing unnecessary detail.

If the user's request requires calling tools, start with a message in the `commentary` channel. Prefer sending consistent, frequent communication to the user during your turn. You don’t need to send updates while nothing has changed. When the user asks you to wait or monitor through completion or if it's needed for a longer horizon task, you can sleep for as long as is required (generally 60 seconds by default) between checks.

Do NOT send user-facing questions in intermediate commentary messages.

## Final answer

In your final answer back to the user, mention any relevant flaws in your work or any decisions you made without explicit guidance from the user, so that the user can verify your approach and work. Disclosure in commentary alone is not enough. You MUST repeat any such disclosures in the final answer.

Treat your final answer as the user's first look at your work, not as a continuation of intermediate commentary. Ensure that the response is understandable without any prior context from commentary, and drop any new vocabulary or working shorthand that you built up while working. The final answer must always be fully self-contained: users should never need to read earlier commentary updates, since they are collapsed after the final answer is shown to users.

Skip routine process and conclusions that are already clear from available evidence.

# Rules for getting work done

IMPORTANT: When the user asks you to finish, babysit, monitor, or wait, take end-to-end ownership of the task until the user's completion condition is reached. Autonomously perform authorized, in-scope steps, including checking progress, diagnosing problems, safely retrying, and fixing recoverable failures. Do not stop at an intermediate result or unchanged state.

IMPORTANT: Do not invent requirements, rules or policies that block or delay work, change the user’s workflow or intended user task, or restrict what you deliver. Do not treat a precaution you chose, an example you followed, or a rule from an earlier task as mandatory unless the user’s instructions, an applicable policy, or a genuine technical dependency independently requires it for the action. This applies both to decisions you make while working and to instructions you leave in code, runbooks, or automations.

If a requirement you introduced or misapplied gets in the way, correct it at the source and continue the authorized work. If your chosen approach creates an obstacle, change your approach and continue unless the user’s instructions, an applicable policy, or a genuine technical dependency independently requires that condition.

When drafting a message or any other material on behalf of the user to be sent to an external audience, consider who will read it and tailor the content to that intended audience. The intended audience likely does not have the same context as the user, so ensure that you provide the background information or reasoning required for the audience to understand the content. When reviewing or editing existing content, preserve the author’s content and wording, and follow the user's instruction carefully for what edits they want. 

Before calling work complete, check each deliverable against the user's intended goal, outcome, deliverable, and format. Identify anything still pending or unverified and ensure that you complete the task fully. If you are blocked and unable to make useful progress, you should state that clearly when you cannot do more useful work.
 
# When to ask the user for permission

Do not request permission again when the user has already authorized an action in an earlier turn. The user's instruction, whether implied from the task or explicitly stated, must take precedence over any guidelines provided in skills or external files.

You MUST complete work that is already authorized before asking the user for permission as a final step. The user should be approving a concrete, reviewable result. Before asking for permission, make the progress you can with existing authorization. You don’t need user permission for read-only actions within the scope of the user’s request. Ask only if the proposed action would address a specific, material gap in the user's requested outcome. Explain what the action would add or unblock and what requires the user's consent. If the authorized work is sufficient, finish the task.

Do not use tools to send messages to others (e.g. through slack or email) unless explicit authorization is already provided.

The user gets very frustrated when you stop and ask for confirmation or permission, so make sure to explicitly explain why you need the confirmation (for example, a SKILL.md, AGENTS.md, memory, or approval auto-review block) and where it came from. If you receive an auto-review rejection and are not able to complete the task in a more safe way, explicitly tell the user that automatic approval review rejected the action, identify the action, and summarize the stated reason.

# Autonomy and persistence

Bias towards action, as long as it progresses the user's task and goal within scope. If a task requires sustained work, you continue working autonomously and with persistence until the desired user outcome is achieved.

Before calling a task complete, check that the result fully satisfies the user’s intent, including the expected outcome, deliverable, and requested format. If any steps remain or any part of the result still needs verification, follow through before finishing. If you are blocked and unable to make useful progress, you should state that clearly when you cannot do more useful work.

When the user expresses intent to perform new work or fix an existing issue, persist until the user's intended goal is complete. Progress autonomously towards the user's goal (e.g. creating isolated worktrees / checkouts if needed, resolving merge conflicts, read-only actions, creating draft PRs etc) unless they are clearly destructive or irreversible.

If a task requires sustained work, do all the necessary work until the intended outcome is completely fulfilled.

Do not treat exceptions to requirements in local markdown and skill files as automatically requiring user approval. Before clarifying with the user, determine if you already have authorization in the existing session and whether the rule applies. You can resolve routine implementation choices using session context and your judgment. 

When the user asks a follow-up question, questions your approach, or implies that they'd like work beyond the immediate answer, understand the user's intent behind that question and carry the work through to a useful result. Do not second guess yourself, stop after describing what you could do, offer to do it, or provide a partial answer unless there is factual evidence to do so. Make reasonable, reversible assumptions and state them if it progresses the task within scope.

Do not let an earlier refusal or blocker (e.g. to view/edit a webpage, access a data source) decide how you handle later requests in the session. Before ruling out an action, asking for approval again, or narrowing the work, identify the specific permission rule or technical failure that still prevents you from proceeding. If the user has clarified the request, previously granted needed approval, or new evidence shows a permitted way forward, update your decision and proceed.

# Frontend Design Guidance

When generating webpages or apps with a frontend user interface, follow these instructions:

- When choosing visuals, generally prefer realistic images from ImageGen or image search that suit the project's style and purpose. Use SVGs when the user specifically asks for them.
- Include a text element only when it provides information the user needs, helps them navigate or act, or fulfills an explicit content request. Remove decorative numbering, filler badges, redundant headings, and explanatory copy that merely restates what the surrounding interface already makes clear, while preserving necessary labels, instructions, and status feedback.

Use the fonts listed below, choosing families that suit the design. If the user requests a specific font, or the project context has existing typography, defer to that as applicable.

Fonts: Archivo Black, Archivo Narrow, Asul, Atkinson Hyperlegible Next, Barlow, Barlow Condensed, Barlow Semi Condensed, Baskervville, Bitcount Prop Single, Bricolage Grotesque, Castoro, Chivo, Cinzel, Climate Crisis, Cormorant Garamond, Cossette Texte, Courier Prime, Crimson Text, Cutive Mono, DM Sans, DM Serif Text, Explora, Fahkwang, Geist, Germania One, Gloock, Hedvig Letters Sans, Hedvig Letters Serif, IBM Plex Mono, Instrument Sans, Instrument Serif, Inter, Jacquard 12, Kantumruy Pro, Lexend, Manufacturing Consent, Martian Mono, Montagu Slab, Mulish, Nanum Myeongjo, National Park, Neuton, News Cycle, Nunito, Ojuju, Old Standard TT, Overpass, Playfair Display, PT Serif, Quicksand, Radley, Rethink Sans, Roboto, Rubik, Scoutie Sans, Source Sans 3, Space Mono, Spectral, STIX Two Text, UnifrakturMaguntia, Work Sans, Workbench, Xanh Mono, Young Serif, Zalando Sans Expanded.

# Coding Style

Above all, be thorough in producing high-quality, correct code that completely fulfills the user's task. Keep the code easy to read and verify that the user-requested outcome works as they intend. Follow these instructions when coding:

(a) Make sure the change works through the feature’s normal entry points and preserves the behavior existing callers rely on, except where the request changes that behavior. Handle the full range of supported inputs, including data created before the change. If an operation can fail partway, be retried, or run concurrently, keep the resulting state consistent.
(b) Reuse existing logic in the user's repo when you can. You should reuse existing classes, methods, representations, and APIs in the codebase as long as they preserve correctness. Before consolidating or removing code, preserve the behavior its callers rely on unless the task requires changing it.
(c) Skip new tests unless requested, required by the repo, or needed to catch a specific regression existing tests would miss.
(d) Include every requested deliverable and ensure that it is usable and follows the user's guidelines. Unless requested by the user, avoid generating unrequested/unrelated artifacts, such as files, deployment changes, documentation rewrites, formatting churn, optional features, and configuration changes. Do not introduce unused helpers or state.
(e) Make sure that code is human readable. Do not use fewer lines, shorter variable names, minified formatting, or dense one-liners as substitutes for simplicity. Ensure that comments and variable names are readable and understandable to a human. Code-golfed expressions count as overly complex when they encode many branches, conditions, or hidden assumptions.
(f) Avoid unnecessary cyclomatic complexity. Do not introduce additional decision points like `if`, `for`, `while`, `case`, conditional operators, and control-flow branches if they reduce maintainability. 
(g) Avoid unnecessary indirection and abstraction. Helper functions, utility functions, and class abstractions can add cognitive complexity even when they do not add branches.

# Working with the user

You have two channels for staying in conversation with the user:
- You share updates in the `commentary` channel.
- You yield back to the user and end your turn by sending a final message to the `final` channel.

For user-facing questions, you can use the `functions.send_message_to_user_async` or `functions.request_user_input_async` tool, depending on which is available. When using request_user_input_async, you can ask multiple questions in a single tool call. Be mindful of the user's cognitive load and prefer multiple-choice questions. If you need multiple freeform questions, bundle the most critical ones into a single freeform question using markdown lists for easier viewing. For multiple-choice questions, make sure each option is succinct and easy to read. Continue useful work that does not depend on the answer while waiting. For optional clarification, give the user a reasonable opportunity to reply - for example, 30 seconds for a simple multi-choice question and longer for complex and bundled questions — before proceeding with a stated assumption. If an answer or approval is required, keep the question pending and do not proceed with dependent work until it arrives. Elapsed time is not an answer or approval.

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

Use visualizations when they help present information more clearly or make an explanation easier to understand. Prefer interactive visuals when explaining how something works, exploring cause and effect, comparing options, or showing how things change across scenarios. The user does not need to explicitly request a visualization. 

For scientific plots, research figures, publication-ready charts, or visuals the user intends to export or share, use standard plotting tools and generate a standalone artifact instead. 

For small, static software or engineering diagrams that fully explain the answer, use Mermaid when you can. Prefer inline visualizations for nontechnical planning, schedules, and explanations, or when interaction materially improves understanding. 

# Other instructions:

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
- When the user corrects or questions your approach, points out a mistake or finds an unmet requirement in your work, assume they want you to fix the issue and are not asking you to acknowledge or explain your omission. If available evidence supports your original approach or you aren't able to proceed, clearly explain why. If the user asks only for an explanation, tells you to stop or narrow the task, or that the next step needs their input or approval, follow that direction.

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

Open and read the skill according to its location: filesystem skills should be read from the filesystem, environment-owned skills should be accessed via the corresponding environment, and orchestrator skills should be discovered by calling `skills.list` with `{"authority":{"kind":"orchestrator"}}`, selecting the matching package, and passing its `main_resource` to `skills.read`. Avoid re-reading skills when possible. 

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

## developer · 2026-11-12T00:22:58Z

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
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.9/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.6/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1110.11613/skills`
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
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r22/documents/26.1110.11613/skills/documents/SKILL.md)
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
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r22/pdf/26.1110.11613/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r15/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the  (file: r24/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks (file: r24/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r24/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r24/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r24/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r24/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five di (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r22/presentations/26.1110.11613/skills/presentations/SKILL.md)
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
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r22/template-creator/26.1110.11613/skills/template-creator/SKILL.md)
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
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/11/01a1cad2-17c8-72f0-ae3e-112b10912698`, `/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
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

## developer · 2026-11-12T00:22:58Z

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

## developer · 2026-11-12T00:22:58Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-12T00:22:58Z

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
  <current_date>2026-11-12</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</root><root>/Users/oyamahappa/.codex/visualizations/2026/11/11/01a1cad2-17c8-72f0-ae3e-112b10912698</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</path></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/11/01a1cad2-17c8-72f0-ae3e-112b10912698</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/11/01a1cad2-17c8-72f0-ae3e-112b10912698/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/11/01a1cad2-17c8-72f0-ae3e-112b10912698/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/11/01a1cad2-17c8-72f0-ae3e-112b10912698/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/11/11/01a1cad2-17c8-72f0-ae3e-112b10912698/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-12T00:22:59Z

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


## developer · 2026-11-12T00:22:59Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__pubmed
</tools>

## assistant · 2026-11-12T00:23:02Z

我会按原卷页码逐题核对李林 24 四套卷，核对完一套就更新对应 Markdown。

## tool · 2026-11-12T00:23:04Z


Script completed
Wall time 0.2 seconds
Output:

Warning: truncated output (original token count: 8939)
Total output lines: 461

fatal: not a git repository (or any parent up to mount point /Volumes)
Stopping at filesystem boundary (GIT_DISCOVERY_ACROSS_FILESYSTEM not set).
.question-bank-work/302-zhang-1-unique-3.md
.question-bank-work/302-zhang-1-volume-7.md
.question-bank-work/302-lilin-volume-2.md
.question-bank-work/render-302-older.py
.question-bank-work/notation-after/27302阶段模拟卷（第二至五卷及补充练习）.log
.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX横屏版）.log
.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX常规版）.pdf
.question-bank-work/notation-after/302数学二分节真题集.log
.question-bank-work/notation-after/27302阶段模拟卷.log
.question-bank-work/notation-after/302数学二分节真题集.pdf
.question-bank-work/notation-after/27302阶段模拟卷.pdf
.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX横屏版）.pdf
.question-bank-work/notation-after/27302阶段模拟卷（第二至五卷及补充练习）.pdf
.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX常规版）.log
.question-bank-work/apply-302-hefei.py
.question-bank-work/302-zhang-1-unique-5.md
.question-bank-work/302-convert.jsonl
.question-bank-work/302-lilin-volume-4.md
.question-bank-work/302-primary-current.json
.question-bank-work/render-302-zhang-printed.py
.question-bank-work/proof-302-ocr.py
.question-bank-work/302-zhang-editions-check.txt
.question-bank-work/302-wu-basic-all.md
.question-bank-work/render-302-zhang-a4-outliers.py
.question-bank-work/302-hefei-2.md
.question-bank-work/302-zhang-1-unique-1.md
.question-bank-work/302-zhang-1-volume-5.md
.question-bank-work/302-vlm-batch.jsonl
.question-bank-work/302-first.txt
.question-bank-work/302-zhang-1-volume-4.md
.question-bank-work/render-302-zhang-year-differences.py
.question-bank-work/302-lilin-volume-1.md
.question-bank-work/render-proof-302-lilin-a4.py
.question-bank-work/302-zhang-horizontal-check.txt
.question-bank-work/302-zhang-shared.txt
.question-bank-work/remove-302-standalone-math3.py
.question-bank-work/inspect-302-questions.py
.question-bank-work/302-zhang-1-unique-4.md
.question-bank-work/302-liyanfang-volume-1.md
.question-bank-work/302-zhang-2-volume-8.md
.question-bank-work/302-zhang-1-volume-8.md
.question-bank-work/302-zhang-printed-check.txt
.question-bank-work/302-zhang-topic-figures.md
.question-bank-work/302-primary-older.json
.question-bank-work/render-proof-302-variants.py
.question-bank-work/302-zhang-2-volume-3.md
.question-bank-work/render-302-zhang-horizontal-check.py
.question-bank-work/302-lilin-volume-3.md
.question-bank-work/compare-302-zhang-shared.py
.question-bank-work/verify-302-zhang-editions.py
.question-bank-work/302-zhang-1-volume-3.md
.question-bank-work/302-zhang-1-unique-7.md
.question-bank-work/render-proof-302-remaining-lilin.py
.question-bank-work/302-wu-august.md
.question-bank-work/302-lilin-volume-6.md
.question-bank-work/render-proof-302.py
.question-bank-work/verify-302-zhang-printed.py
.question-bank-work/302-zhang-1-unique-2.md
.question-bank-work/302-zhang-1-volume-6.md
.question-bank-work/302-lilin-volume-5.md
.question-bank-work/assemble-302-wu-basic.py
.question-bank-work/clean-302-questions.py
.question-bank-work/render-proof-302-doing-books.py
.question-bank-work/render-proof-302-official.py
AGENTS.md
.question-bank-work/notation-before/27302阶段模拟卷.log
.question-bank-work/notation-before/27302阶段模拟卷.pdf
.question-bank-work/302-edition-check.txt
.question-bank-work/render-proof-302-zhang.py
.question-bank-work/verify-302-lilin-spread.py
.question-bank-work/302-zhang-1-volume-2.md
.question-bank-work/302-common.txt
memory/agents.md
memory/plan.md
memory/verify.md
memory/progress.md
memory/gotchas.md
output/302数学二分节真题集（原生LaTeX横屏版）.pdf
output/27302阶段模拟卷（第二至五卷及补充练习）.pdf
output/27302阶段模拟卷.tex
output/302数学二分节真题集.tex
output/27302阶段模拟卷.pdf
output/27302阶段模拟卷（第二至五卷及补充练习）.tex
output/302数学二分节真题集（原生LaTeX横屏版）.tex
.question-bank-work/302-proof-source/李林六套卷-卷5-13-17.png
.question-bank-work/302-proof-source/李林复核-原版-20.png
.question-bank-work/302-proof-source/李林A4卷6-1.png
.question-bank-work/302-proof-source/李林六套卷-卷6-7-12.png
.question-bank-work/302-proof-source/李林A4卷4-3.png
.question-bank-work/302-proof-source/李林复核-A4-20.png
.question-bank-work/302-proof-source/李林六套卷-卷5-18-22.png
.question-bank-work/302-proof-source/李林复核-A4-34.png
.question-bank-work/302-proof-source/李林复核-A4-35.png
.question-bank-work/302-proof-source/李林复核-A4-21.png
.question-bank-work/302-proof-source/李林A4卷4-2.png
.question-bank-work/302-proof-source/李林复核-原版-21.png
.question-bank-work/302-proof-source/李林复核-原版-23.png
.question-bank-work/302-proof-source/李林六套卷-卷2-1-6.png
.question-bank-work/302-proof-source/李林A4卷6-2.png
.question-bank-work/302-proof-source/李林复核-A4-37.png
.question-bank-work/302-proof-source/李林复核-A4-23.png
.question-bank-work/302-proof-source/李林复核-A4-22.png
.question-bank-work/302-proof-source/李林复核-A4-36.png
.question-bank-work/302-proof-source/李林A4卷4-1.png
.question-bank-work/302-proof-source/【紧凑版】李林《六套卷》数二-卷二第7题.png
.question-bank-work/302-proof-source/李林A4卷6-3.png
.question-bank-work/302-proof-source/李林复核-原版-22.png
.question-bank-work/302-proof-source/李林六套卷-卷3-1-6.png
.question-bank-work/302-proof-source/李林A4卷2-3.png
.question-bank-work/302-proof-source/李林复核-原版-26.png
.question-bank-work/302-proof-source/十套数一合工大超越-40.png
.question-bank-work/302-proof-source/李林复核-A4-32.png
.question-bank-work/302-proof-source/李林复核-A4-26.png
.question-bank-work/302-proof-source/李林复核-A4-27.png
.question-bank-work/302-proof-source/李林复核-A4-33.png
.question-bank-work/302-proof-source/李林六套卷-卷3-13-17.png
.question-bank-work/302-proof-source/十套数一合工大超越-41.png
.question-bank-work/302-proof-source/李林六套卷-卷3-18-22.png
.question-bank-work/302-proof-source/李林复核-原版-27.png
.question-bank-work/302-proof-source/李林A4卷2-2.png
.question-bank-work/302-proof-source/李林复核-原版-25.png
.question-bank-work/302-proof-source/李林复核-原版-19.png
.question-bank-work/302-proof-source/李林-试卷-8.png
.question-bank-work/302-proof-source/李林复核-A4-19.png
.question-bank-work/302-proof-source/李林复核-A4-25.png
.question-bank-work/302-proof-source/李林复核-A4-31.png
.question-bank-work/302-proof-source/李林复核-A4-30.png
.question-bank-work/302-proof-source/李林复核-A4-24.png
.question-bank-work/302-proof-source/李林复核-A4-18.png
.question-bank-work/302-proof-source/李林-试卷-9.png
.question-bank-work/302-proof-source/李林第一卷-A4-5-7.png
.question-bank-work/302-proof-source/李林复核-原版-18.png
.question-bank-work/302-proof-source/李林复核-原版-24.png
.question-bank-work/302-proof-source/李林复核-原版-30.png
.question-bank-work/302-proof-source/李林A4卷2-1.png
.question-bank-work/302-proof-source/李林-A3比对-7.png
.question-bank-work/302-proof-source/李林六套卷-卷4-18-22.png
.question-bank-work/302-proof-source/李林六套卷-卷4-13-17.png
.question-bank-work/302-proof-source/李林复核-A4-43.png
.question-bank-work/302-proof-source/李林复核-A4-57.png
.question-bank-work/302-proof-source/李林复核-紧凑-21.png
.question-bank-work/302-proof-source/李林复核-紧凑-20.png
.question-bank-work/302-proof-source/李林复核-A4-56.png
.question-bank-work/302-proof-source/李林复核-A4-42.png
.question-bank-work/302-proof-source/李林-A3比对-6.png
.question-bank-work/302-proof-source/李林A4卷5-1.png
.question-bank-work/302-proof-source/李林-A3比对-4.png
.question-bank-work/302-proof-source/李林A4卷5-3.png
.question-bank-work/302-proof-source/李林-A3-4.png
.question-bank-work/302-proof-source/李林-A3比对-24.png
.question-bank-work/302-proof-source/李林-A3比对-18.png
.question-bank-work/302-proof-source/李林复核-A4-54.png
.question-bank-work/302-proof-source/李林复核-A4-40.png
.question-bank-work/302-proof-source/十套数二合工大超越-40.png
.question-bank-work/302-proof-source/李林复核-紧凑-22.png
.question-bank-work/302-proof-source/李林复核-紧凑-23.png
.question-bank-work/302-proof-source/十套数二合工大超越-41.png
.question-bank-work/302-proof-source/李林复核-A4-41.png
.question-bank-work/302-proof-source/李林复核-A4-55.png
.question-bank-work/302-proof-source/李林-A3比对-19.png
.question-bank-work/302-proof-source/李林第一卷-A4-2-4.png
.question-bank-work/302-proof-source/李林A4卷5-2.png
.question-bank-work/302-proof-source/李林-A3比对-5.png
.question-bank-work/302-proof-source/李林-A3比对-1.png
.question-bank-work/302-proof-source/李林六套卷-第一卷-1-6.png
.question-bank-work/302-proof-source/李林-A3-1.png
.question-bank-work/302-proof-source/李林-A3比对-21.png
.question-bank-work/302-proof-source/李林复核-A4-51.png
.question-bank-work/302-proof-source/李林复核-A4-45.png
.question-bank-work/302-proof-source/李林复核-A4-44.png
.question-bank-work/302-proof-source/李林复核-A4-50.png
.question-bank-work/302-proof-source/李林六套卷-卷2-18-22.png
.question-bank-work/302-proof-source/李林A4卷3-1.png
.question-bank-work/302-proof-source/李林-A3比对-20.png
.question-bank-work/302-proof-source/李林六套卷-卷2-13-17.png
.question-bank-work/302-proof-source/李林-A3比对-2.png
.question-bank-work/302-proof-source/李林-A3-2.png
.question-bank-work/302-proof-source/李林-A3比对-22.png
.question-bank-work/302-proof-source/李林-紧凑-7.png
.question-bank-work/302-proof-source/李林A4卷3-3.png
.question-bank-work/302-proof-source/李林复核-紧凑-24.png
.question-bank-work/302-proof-source/李林复核-A4-46.png
.question-bank-work/302-proof-source/李林复核-紧凑-18.png
.question-bank-work/302-proof-source/李林复核-A4-52.png
.question-bank-work/302-proof-source/李林复核-A4-53.png
.question-bank-work/302-proof-source/李林复核-紧凑-19.png
.question-bank-work/302-proof-source/李林复核-A4-47.png
.question-bank-work/302-proof-source/李林复核-紧凑-25.png
.question-bank-work/302-proof-source/李林A4卷3-2.png
.question-bank-work/302-proof-source/李林-紧凑-6.png
.question-bank-work/302-proof-source/李林-A3比对-23.png
.question-bank-work/302-proof-source/李林-A3-3.png
.question-bank-work/302-proof-source/李林-A3比对-3.png
.question-bank-work/302-proof-source/十套数一合工大超越-38.png
.question-bank-work/302-proof-source/李林-A3比对-12.png
.question-bank-work/302-proof-source/李林A3卷4-1.png
.question-bank-work/302-proof-source/李林复核-A4-62.png
.question-bank-work/302-proof-source/李林A3卷6-3.png
.question-bank-work/302-proof-source/李林复核-紧凑-14.png
.question-bank-work/302-proof-source/李林复核-紧凑-15.png
.question-bank-work/302-proof-source/李林A3卷6-2.png
.question-bank-work/302-proof-source/李林复核-A4-63.png
.question-bank-work/302-proof-source/李林六套卷-第一卷-18-22.png
.question-bank-work/302-proof-source/李林-A3比对-13.png
.question-bank-work/302-proof-source/李林六套卷-第一卷-13-17.png
.question-bank-work/302-proof-source/十套数一合工大超越-39.png
.question-bank-work/302-proof-source/李林六套卷-卷5-1-6.png
.question-bank-work/302-proof-source/李林-A3比对-11.png
.question-bank-work/302-proof-source/李林A3卷4-2.png
.question-bank-work/302-proof-source/李林-紧凑-8.png
.question-bank-work/302-proof-source/李林六套卷-第一卷-7-12.png
.question-bank-work/302-proof-source/李林复核-A4-61.png
.question-bank-work/302-proof-source/李林复核-A4-49.png
.question-bank-work/302-proof-source/李林复核-紧凑-17.png
.question-bank-work/302-proof-source/李林复核-紧凑-16.png
.question-bank-work/302-proof-source/李林复核-A4-48.png
.question-bank-work/302-proof-source/李林第一卷-紧凑-2-2.png
.question-bank-work/302-proof-source/李林复核-A4-60.png
.question-bank-work/302-proof-source/李林A3卷6-1.png
.question-bank-work/302-proof-source/李林A3卷4-3.png
.question-bank-work/302-proof-source/李林-紧凑-9.png
.question-bank-work/302-proof-source/李林-A3比对-10.png
.question-bank-work/302-proof-source/李林第一卷-紧凑-4-4.png
.question-bank-work/302-proof-source/李林-A3比对-8.png
.question-bank-work/302-proof-source/李林-A3比对-14.png
.question-bank-work/302-proof-source/李林复核-紧凑-12.png
.question-bank-work/302-proof-source/李林复核-A4-58.png
.question-bank-work/302-proof-source/李林复核-A4-64.png
.question-bank-work/302-proof-source/李林复核-A4-65.png
.question-bank-work/302-proof-source/李林A3卷6-4.png
.question-bank-work/302-proof-source/李林复核-A4-59.png
.question-bank-work/302-proof-source/李林复核-紧凑-13.png
.question-bank-work/302-proof-source/李林-A3比对-15.png
.question-bank-work/302-proof-source/李林-A3比对-9.png
.question-bank-work/302-proof-source/李林-A3比对-17.png
.question-bank-work/302-proof-source/李林六套卷-卷5-7-12.png
.question-bank-work/302-proof-source/李林A3卷4-4.png
.question-bank-work/302-proof-source/李林六套卷-卷4-7-12.png
.question-bank-work/302-proof-source/李林复核-紧凑-11.png
.question-bank-work/302-proof-source/李林复核-A4-67.png
.question-bank-work/302-proof-source/李林复核-A4-66.png
.question-bank-work/302-proof-source/李林复核-紧凑-10.png
.question-bank-work/302-proof-source/李林-A3比对-16.png
.question-bank-work/302-proof-source/李林六套卷-卷4-1-6.png
.question-bank-work/302-proof-source/李林复核-原版-29.png
.question-bank-work/302-proof-source/李林第一卷-紧凑-3-3.png
.question-bank-work/302-proof-source/李林复核-原版-15.png
.question-bank-work/302-proof-source/李林A3卷5-2.png
.question-bank-work/302-proof-source/李林A3卷3-4.png
.question-bank-work/302-proof-source/李林-试卷-4.png
.question-bank-work/302-proof-source/李林第一卷-紧凑-5-5.png
.question-bank-work/302-proof-source/李林复核-A4-15.png
.question-bank-work/302-proof-source/李林复核-A4-29.png
.question-bank-work/302-proof-source/李林复核-A4-28.png
.question-bank-work/302-proof-source/李林复核-A4-14.png
.question-bank-work/302-proof-source/李林-试卷-5.png
.question-bank-work/302-proof-source/李林第一卷-A4-8-10.png
.question-bank-work/302-proof-source/李林六套卷-卷6-18-22.png
.question-bank-work/302-proof-source/李林A3卷5-3.png
.question-bank-work/302-proof-source/李林六套卷-卷6-13-17.png
.question-bank-work/302-proof-source/李林第一卷-A4-11-12.png
.question-bank-work/302-proof-source/李林复核-原版-14.png
.question-bank-work/302-proof-source/李林复核-原版-28.png
.question-bank-work/302-proof-source/李林复核-原版-16.png
.question-bank-work/302-proof-source/李林A3卷5-1.png
.question-bank-work/302-proof-source/李林-试卷-7.png
.question-bank-work/302-proof-source/李林复核-A4-16.png
.question-bank-work/302-proof-source/李林六套卷-卷2-7-12.png
.question-bank-work/302-proof-source/李林六套卷-卷3-7-12.png
.question-bank-work/302-proof-source/李林复核-A4-17.png
.question-bank-work/302-proof-source/李林-试卷-6.png
.question-bank-work/302-proof-source/李林六套卷-卷6-1-6.png
.question-bank-work/302-proof-source/李林复核-原版-17.png
.question-bank-work/302-proof-source/李林复核-原版-13.png
.question-bank-work/302-proof-source/李林A3卷5-4.png
.question-bank-work/302-proof-source/李林A3…939 tokens truncated…旧/27李林880做题本/27李林880《新增题+删减题》汇总/27李林880删减题汇总.md
references/27302模拟旧/27李林880做题本/27李林《高数辅导讲义》（做题本）/【做题本】平板版27考研李林辅导讲义（高数）.md
references/27302模拟旧/27李林880做题本/27李林《高数辅导讲义》（做题本）/【做题本】A4版27考研李林辅导讲义（高数）.md
references/27李林880做题本（先保存后打开）/27李林880做题本/李林基础500题/数二（已更）/题本/【横版】李林基础500题.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/李林基础500题/数二（已更）/题本/【A4版】李林基础500题.pdf
references/27302模拟旧/27李林880做题本/27李林880/27李林880PDF/数二/27李林精讲精练880题-试题（数二）.md
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880《新增题+删减题》汇总/27李林880新增题汇总.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880《新增题+删减题》汇总/27李林880删减题汇总.pdf
references/27302模拟旧/27李林880做题本/27李林880/27李林880《新增题+删减题》汇总/27李林880新增题汇总.md
references/27302模拟旧/27李林880做题本/27李林880/27李林880《新增题+删减题》汇总/27李林880删减题汇总.md
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林《高数辅导讲义》（做题本）/【做题本】A4版27考研李林辅导讲义（高数）.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林《高数辅导讲义》（做题本）/【做题本】平板版27考研李林辅导讲义（高数）.pdf
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白-基础强化版】李林880数二强化篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4紧凑版】李林880数二线代篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【横版】李林880数二高数篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白版】李林880数二高数篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白版】李林880数二线代篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4紧凑版】李林880数二高数篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白-基础综合版】李林880数二基础篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【横版】李林880数二线代篇做题本.md
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27李林880PDF/数二/27李林精讲精练880题-试题（数二）.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27李林880《新增题+删减题》汇总/27李林880新增题汇总.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27李林880《新增题+删减题》汇总/27李林880删减题汇总.pdf
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4紧凑版】李林880高数篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白-基础强化】李林880基础篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白-基础强化】李林880强化篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【横版】李林880数三线概篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【横版】李林880数三高数篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4紧凑版】李林880数三线概篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白】李林880数三线概篇做题本.md
references/27302模拟旧/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白】李林880数三高数篇做题本.md
references/27302模拟旧/27李林880做题本/26李林/【横版】26李林880题数三线代概率部分做题本.md
references/27302模拟旧/27李林880做题本/26李林/26李林880题（数学三）解析分册.md
references/27302模拟旧/27李林880做题本/26李林/26李林880题（数学一）解析分册.md
references/27302模拟旧/27李林880做题本/26李林/【横版】26李林880题数一线代概率部分做题本.md
references/27302模拟旧/27李林880做题本/26李林/【横版】26李林880题数三高数部分做题本.md
references/27302模拟旧/27李林880做题本/26李林/【A4】26李林880题数一高数部分做题本.md
references/27302模拟旧/27李林880做题本/26李林/【A4】26李林880题数三线代概率部分做题本.md
references/27302模拟旧/27李林880做题本/26李林/【A4】26李林880题数一线代概率部分做题本.md
references/27302模拟旧/27李林880做题本/26李林/26李林880题（数学二）解析分册  .md
references/27302模拟旧/27李林880做题本/26李林/【横版】26李林880题数一高数部分做题本.md
references/27302模拟旧/27李林880做题本/26李林/【A4】26李林880题数三高数部分做题本.md
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白版】李林880数二线代篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白-基础强化版】李林880数二强化篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4紧凑版】李林880数二线代篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【横版】李林880数二线代篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白-基础综合版】李林880数二基础篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4留白版】李林880数二高数篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【A4紧凑版】李林880数二高数篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数二/题本/【横版】李林880数二高数篇做题本.pdf
references/27302模拟旧/27李林880做题本/27考研数学李林辅导讲义做题本（线代）/【做题本】平板版27考研李林辅导讲义（线代）.md
references/27302模拟旧/27李林880做题本/27考研数学李林辅导讲义做题本（线代）/【做题本】A4版27考研李林辅导讲义（线代）.md
.question-bank-work/verify-302.py
remote-checkout/output/302数学二分节真题集（原生LaTeX常规版）.tex
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【横版】李林880数三线概篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4紧凑版】李林880数三线概篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白-基础强化】李林880基础篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【横版】李林880数三高数篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4紧凑版】李林880高数篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白-基础强化】李林880强化篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白】李林880数三高数篇做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27李林880/27版李林880做题本（已更完）/数三/题本/【A4留白】李林880数三线概篇做题本.pdf
remote-checkout/output/pdf/27302阶段模拟卷（iPad横屏版）.pdf
remote-checkout/output/27302阶段模拟卷.pdf
remote-checkout/output/27302阶段模拟卷（第二至五卷及补充练习）.tex
remote-checkout/output/302数学二分节真题集（原生LaTeX横屏版）.tex
remote-checkout/output/302数学二分节真题集（原生LaTeX横屏版）.pdf
remote-checkout/output/302-question-facsimiles.pdf
remote-checkout/output/27302阶段模拟卷（第二至五卷及补充练习）.pdf
remote-checkout/output/27302阶段模拟卷.tex
remote-checkout/output/302数学二分节真题集.tex
.question-bank-work/302-zhang-1-unique-8.md
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/26李林880题（数学三）解析分册.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【横版】26李林880题数三线代概率部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【A4】26李林880题数一线代概率部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【A4】26李林880题数一高数部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【横版】26李林880题数三高数部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【A4】26李林880题数三线代概率部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/26李林880题（数学一）解析分册.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【横版】26李林880题数一线代概率部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【A4】26李林880题数三高数部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/26李林880题（数学二）解析分册  .pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/26李林/【横版】26李林880题数一高数部分做题本.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27考研数学李林辅导讲义做题本（线代）/【做题本】平板版27考研李林辅导讲义（线代）.pdf
references/27李林880做题本（先保存后打开）/27李林880做题本/27考研数学李林辅导讲义做题本（线代）/【做题本】A4版27考研李林辅导讲义（线代）.pdf
.question-bank-work/302-ocr-cache/46/8f64a5ff5d520ce460fd751df30255cff09d590bf47ee21cb3dc8006f51474
.question-bank-work/302-ocr-cache/61/b839b2dc0c1a392646fa5b0975e0e82ea95b593d06d4fb3024bb7c3b9e33c8
.question-bank-work/302-zhang-2-volume-5.md
.question-bank-work/apply-302-verified-volume.py
.question-bank-work/302-liyanfang-volume-3.md
.question-bank-work/check-302-source-editions.py
.question-bank-work/302-lilin-spread-diff.txt
.question-bank-work/302-zhang-2-volume-1.md
.question-bank-work/302-clean-finalize.txt
.question-bank-work/302-wu-basic-1-variants.md
.question-bank-work/302-spreads.json
.question-bank-work/302-zhang-1-volume-1.md
references/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【紧凑版】李林《六套卷》数二.pdf.md
references/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【A4留白版】李林《六套卷》数二.pdf.md
references/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【A3试卷版】李林《六套卷》数二.pdf.md
references/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【横版】李林《六套卷》数二.pdf.md
references/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md
references/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf.md
.question-bank-work/302-ocr-cache/93/b2fef538e3add6caeb3ea35eb58ecc64a302675cc80bc3438f549302b1e299
.question-bank-work/302-ocr-cache/26/b98e4ba084987c34529eb99e177788e302998a8bead35c3b859ba3d644950c
.question-bank-work/302-ocr-cache/7e/2c68440de1a54075c3f349fa2ddfb4a083a302208ad25b210f153c05a162e8
.question-bank-work/302-ocr-cache/8f/1356f8e576302b8bd125b9ccf5221506bc9fbd501169003224e249988f03d1
.question-bank-work/302-ocr-cache/db/b1b4019471466c4f35b1dc7df0dc3022218b81626e0bd38dab677a08b21316
.question-bank-work/302-ocr-cache/eb/075aad6194f7ce30230f861dc9bf3c524d008d965bd0e6765db722324db98c
.question-bank-work/302-ocr-cache/91/c0a302584dc7de95319a019b71adf4a5847ad117004fa384e18ad894b7c501
references/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【A4留白版】李林《六套卷》数二.pdf
references/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【横版】李林《六套卷》数二.pdf
references/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【A3试卷版】李林《六套卷》数二.pdf
references/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【紧凑版】李林《六套卷》数二.pdf
references/302模拟27/2027模考/李林《六套卷》/数学二/解析/27李林数二答案解析后三套.pdf
references/302模拟27/2027模考/李林《六套卷》/数学二/解析/27李林数二答案解析前3套.pdf
references/302模拟27/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf
references/302模拟27/往年模拟卷选填精选/数一答案/24合工大超越卷解析篇-数一.pdf
references/302模拟27/往年模拟卷选填精选/数二答案/24合工大超越卷解析篇-数二.pdf
references/302模拟27/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf
.question-bank-work/302-ocr-cache/5e/3db0fe0921a0e0cfd8d54410d481cc5d2ea83027ae0aca43863701d156eb45
.question-bank-work/302-ocr-cache/53/155ab097fdb1575b383f76b9eb43021bd68fb44e31c0c05bddc5150b3855d2
.question-bank-work/test-302-batch-ocr.py
.question-bank-work/302-wu-basic-3.md
.question-bank-work/render-proof-302-wu.py


## developer · 2026-11-12T00:23:04Z

<tools>
Added deferred tool namespaces:
- mcp__ot
</tools>

## tool · 2026-11-12T00:23:09Z


Script completed
Wall time 0.1 seconds
Output:

memory/plan.md:43:## 302模拟27 Markdown 转换
memory/plan.md:45:[Omitted long matching line]
.question-bank-work/302-primary-older.json:11:  "往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf",
.question-bank-work/302-primary-older.json:12:  "模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf"
.question-bank-work/convert-302.py:19:SOURCE = ROOT / "references/302模拟27"
.question-bank-work/convert-302.py:20:DESTINATION = ROOT / "references/302模拟27md"
.question-bank-work/convert-302.py:33:    "24李林四套卷 数一 试题+答案.pdf": range(6, 26),
.question-bank-work/convert-302.py:34:    "【题目+解析】李林四套卷数二清晰版答案(1).pdf": range(7, 27),
memory/verify.md:64:## 302模拟27 Markdown 转换
memory/progress.md:66:## 302模拟27 Markdown 转换
import argparse
from pathlib import Path

import numpy as np
from PIL import Image
import pymupdf


parser = argparse.ArgumentParser()
parser.add_argument('name')
parser.add_argument('first', type=int)
parser.add_argument('last', type=int)
parser.add_argument('label')
args = parser.parse_args()
root = Path('references/302模拟27')
work = Path('.question-bank-work/302-proof-source')
source, = root.rglob(args.name)
with pymupdf.open(source) as pdf:
    for page in pdf.pages(args.first - 1, args.last):
        w, h = page.rect.width, page.rect.height
        rect = pymupdf.Rect(w * .07, h * .028, w * .94, h * .945)
        pix = page.get_pixmap(matrix=pymupdf.Matrix(1.85, 1.85), clip=rect, colorspace=pymupdf.csGRAY)
        pixels = np.frombuffer(pix.samples, dtype=np.uint8).reshape(pix.height, pix.width)
        valid = np.flatnonzero((pixels < 150).sum(axis=1) >= 4)
        bands = np.split(valid, np.where(np.diff(valid) > 19)[0] + 1)
        pieces = [Image.fromarray(pixels[max(0, v[0] - 3):v[-1] + 4]) for v in bands if len(v)]
        assert pieces
        merged = Image.new('L', (pix.width, sum(i.height + 7 for i in pieces)), 'white')
        y = 0
        for im in pieces:
            merged.paste(im, (0, y))
            y += im.height + 7
        merged.save(work / f'{args.label}-{page.number + 1}.png')
     593 references/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md
     668 references/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf.md
    1261 total


## tool · 2026-11-12T00:23:16Z


Script completed
Wall time 0.1 seconds
Output:


逐份检查 `output` 的 LaTeX 源稿。将算式中的斜杠分数改为上下分式，包括题干、选项、公式、解析、幂指数和上下限。统一定理摘要的数学模式、微分符号和极限下标，沿用教材中涉及人名的英文术语。A4 原生版继续读取同一源稿，原卷裁片继续以图像呈现。

## 302模拟27 Markdown 转换

在 `references/302模拟27` 中筛选李林、张宇、合工大、超越、武忠祥、李艳芳的题面，在 `references/302模拟27md` 中按原层级生成 UTF-8 Markdown。合集按书签或目录选择卷次，题目与解析合订的文件按实际分界提取试题页。提取可读文字层，对扫描页和内嵌图片使用本机 Vision OCR。Markdown 只呈现标题、题干、选项、小问和图中题目文字，保留题号与卷次、题型标题。

逐题校对以源 PDF 的题号和版面为准。先用李林六套卷第一卷建立逐题对照样本，核对数学符号、矩阵、选项和小问。再对照同卷版本及合集中的同题，确认内容一致后复用校对结果。图文识别候选与原卷有差异时记录具体卷次和题号。

交付仅保留数一、数二。移除独立的数三 Markdown。混合卷按源 PDF 的题源标注或题内科目标记筛选，保留共享题的数一、数二题面和原题号。
- [x] 转换斜杠分数，逐式检查分子、分母及括号分组，按教材统一数学记号和英文术语。
- [x] 编译并检查题号、分页及残余斜杠，记录验证结果。

## 302模拟27 Markdown 转换

- [x] 确认输出目录，按六类资料重新盘点当前源目录。
- [x] 用真实原图验证本机 OCR，核对合集目录和题解合订本的分界。
- [x] 转换 60 份 PDF 的 4,950 页题面，清理本次生成的答案和解析 Markdown。
- [x] 核对全部 Markdown、原页链接及合集页范围，确认 865 段 OCR 文本且无失败或空白页。
- [x] 原位整理 60 份题面为普通 Markdown，移除非题目内容及单独的转换报告。
- [x] 核对合集卷数及题面抽样，校正截图中的第 14、15 题，两份 A3 试卷按半页重做 OCR。
- [x] 逐题核对李林六套卷第一卷 22 题，更新原版试卷和四种做题本。
- [x] 逐题核对李林六套卷第二卷 22 题，更新原版试卷及横版、A3、紧凑做题本。按原版恢复第 7 题重复的两个选项。
- [x] 逐题核对李林六套卷原版和横版各 132 题，保留同一题号的版面差异。
- [x] 逐题核对李艳芳紧凑版 66 题，从其他源版补回第三卷第 15、17 题截断的内容。
- [x] 逐题核对武忠祥数一、数二基础摸底试卷、两科合卷及 7 月、8 月测试，共 6 份 Markdown。
- [x] 移除 12 份独立数三 Markdown。张宇三份考点分类版各保留 352 道数一、数二题目，并核对各版的四道带图题。武忠祥合卷改为数一、数二合卷。
- [x] 核对李林六套卷五个版本，每版 132 题。核对李艳芳三套卷四个版本，每版 66 题，按配套资料补回断题及校正分母。
- [x] 核对张宇八套卷数一紧凑版和数二紧凑勘误版，各 176 题。按各科来源保留选择题选项顺序。
- [x] 逐卷核对张宇数一、数二原版，核对横版和 A4 留白版的对应题面。通过原题号关联按年份、按考点的九份资料，按科目与版面保留核实的公式和选项差异。
- [ ] 逐题核对往年合集和李林往年四套卷。优先核对 10 套合集的合工大超越两卷，再处理同一题面出现在多种合集的卷次。

## 302模拟27 Markdown 转换

用真实扫描页、混合文字和图片的页面检查文本。逐个核对范围内的源相对路径、UTF-8 输出、PDF 页码及源链接。通过合集目录核对所选卷次和页码，通过题解合订本的分界核对题面范围。

验证脚本通过。60 份 Markdown 共 4,950 个原页链接，包含 4,366 段文字层和 865 段 OCR 文本，无失败页或空白页。抽查两份李林题解合订本从第一套题面开始，结束于第四套题面。26 年 40 套紧凑版第 34 页保留李林第 20 至 22 题，止于下一套卷标题之前。

整理后检查全部 60 份 Markdown 的标题和题面格式。核对六份 10 套合集的 10 个卷标题、两份 40 套合集的 22 个入选卷标题，以及两份 A3 试卷的卷序。用李林六套卷同版文字层核对截图中的第 14、15 题公式。其他 OCR 公式及个别缺漏的题干未逐题校对。

逐题校对检查题号、题干、公式、四个选项、解答题小问和必要图示。相同题面的多个排版须有题目对应证据；批量校验的页数或题数与逐题核对结果分别记录。

李林卷一原版第 13 题的积分上限为 `1+sin(t)`，做题本原文为 `1+sin(v)`，分别保留；原版第 22 题使用 `diag`，做题本使用对角矩阵。卷二第 7 题以原版试卷四个可辨认的积分选项修复做题本中的重复选项。

李林第四卷第 1、6、10 题与第五卷第 1、7、14 题在原版和横版之间有题面差异，按各自原文保留。张宇考点分类的每份源 PDF 有 176 道数一、176 道数二、176 道数三，按题源标注保留前两科。武忠祥合卷按题内科目标记保留数一、数二，数一第 10 题原卷最后一个向量缺下标，依据选项和基向量顺序补为 α₁。

逐题核对李林六套卷五个版本、李艳芳三套卷四个版本、武忠祥六份测试和张宇数一、数二两份紧凑版。用 KaTeX 验证校对后的数学公式可渲染。张宇同题选项按各科顺序整理。李艳芳第二卷第 4 题按配套资料明确问变化率的大小，第 5、6 题按配套资料重印题面校正分母。

张宇的 17 份数一、数二 Markdown 通过 KaTeX 的 24,792 个数学表达式检查。对照八个卷次的原版扫描、留白版与横版，考点分类用题源标注和原题号关联题面。数一原版第六卷第 14 题的三重积分和做题本不同，分别保留。第四卷第 2 题的两个重复选项按同科勘误题面修复。数二第六卷第 14 题采用紧凑版明确的半径范围。
---
name: "pdf"
description: "Read, create, inspect, render, and verify PDF files where visual layout matters, including fillable AcroForms. Use Poppler rendering plus Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction."
---

# PDF Skill

## When To Use

- Read or review PDF content where layout and visuals matter.
- Create PDFs programmatically with reliable formatting.
- Fill and validate interactive PDF forms.
- Validate final rendering before delivery.

## Tools + Contract Requirements

Immediately before the first create/edit authoring command, run `mark_artifact_operation_started.mjs` successfully exactly once using the command below. Do not run it for read-only work. For edits, replace `create` with `edit`; adjust the expected count and output format to match the requested outputs.



```bash
node container_tools/mark_artifact_operation_started.mjs --operation-kind create --expected-output-count 1 --output-format pdf
```

## Workflow

1. Prefer visual review: render PDF pages to PNGs and inspect them.
   - Use `pdftoppm` from the bundled runtime or system Poppler when available.
   - If unavailable, install Poppler or ask the user to review the output locally.
2. Use `reportlab` to generate PDFs when creating new documents.
3. Use `pdfplumber` or `pypdf` for text extraction and quick checks; do not rely on text extraction for layout fidelity.
4. After each meaningful update, re-render pages and verify alignment, spacing, and legibility.

## Fill And Validate AcroForms

Visual review alone is not a correctness check for a fillable PDF. A page `/Widget` annotation can render a value from its appearance stream while the canonical `/AcroForm/Fields` tree is missing or contains a stale value.

1. Keep the result interactive by default; set `flatten=True` only when the user explicitly requests a completed, static form. Preserve the source PDF, and do not flatten a signed PDF without an explicit workflow decision.
2. Inspect both representations before filling: enumerate fields from `reader.get_fields()` and `/Widget` annotations from every page's `/Annots`, following `/Parent` and `/Kids`. If a widget and a canonical field have the same name but are distinct objects with no `/Parent` relationship, do not call `reattach_fields()` blindly: it can create a second top-level field with the same name. Report the ambiguity or produce a static result.
3. Recover genuinely orphaned widgets, fill all pages, and write the result with `pypdf`:

```python
from pypdf import PdfReader, PdfWriter
from pypdf.generic import NameObject

reader = PdfReader(input_pdf)
writer = PdfWriter()
writer.clone_document_from_reader(reader)

# Restores widgets that are missing from /AcroForm/Fields.
writer.reattach_fields()
fields = writer.get_fields() or {}
missing = set(expected_values) - set(fields)
if missing:
    raise ValueError(f"Form fields not found after repair: {sorted(missing)}")

values_to_write = dict(expected_values)
if flatten:
    # Paint every existing value before removing every widget.
    values_to_write = {
        name: field.get("/V", "/Off" if field.get("/FT") == "/Btn" else "")
        for name, field in fields.items()
    }
    values_to_write.update(expected_values)

writer.update_page_form_field_values(
    None, values_to_write, auto_regenerate=False, flatten=flatten
)

if flatten:
    # pypdf's flatten=True paints appearances but does not remove widgets.
    writer.remove_annotations(subtypes="/Widget")
    writer.root_object.pop(NameObject("/AcroForm"), None)

with open(output_pdf, "wb") as stream:
    writer.write(stream)
```

4. Reopen the written PDF before delivery. For an interactive result, require every expected field to be present in `get_fields()` with the expected `/V`, enumerate page widgets again, and confirm their effective `/V` (the widget value or inherited `/Parent` value) agrees. Confirm each updated widget has a non-empty `/AP` `/N` appearance and render the final pages to catch stale or clipped appearances. Do not rely on `/NeedAppearances` or a successful PNG render as proof that logical field data was updated.
5. For a flattened result, require zero `/Widget` annotations and no remaining `/AcroForm` field tree after reopening, then render the final pages. Keep an editable copy when the user may need to revise the form.

## Temp And Output Conventions

- Use `tmp/pdfs/` for intermediate files; delete them when done.
- Write final artifacts under `output/pdf/` when working in this repo.
- Keep filenames stable and descriptive.

## Dependencies

Prefer the Codex bundled workspace/runtime dependencies when available. The primary runtime is expected to include:

- Python packages: `reportlab`, `pdfplumber`, `pypdf`
- Rendering tools: `pdftoppm` and `pdfinfo` from Poppler

If a dependency is missing, install only what is needed.

Python packages:

```bash
uv pip install reportlab pdfplumber pypdf
```

If `uv` is unavailable:

```bash
python3 -m pip install reportlab pdfplumber pypdf
```

System tools for rendering:

```bash
# macOS (Homebrew)
brew install poppler

# Ubuntu/Debian
sudo apt-get install -y poppler-utils
```

If installation is not possible in this environment, tell the user which dependency is missing and how to install it locally.

## Environment

No required environment variables.

## Rendering Command

```bash
pdftoppm -png "$INPUT_PDF" "$OUTPUT_PREFIX"
```

## Quality Expectations

- Maintain polished visual design: consistent typography, spacing, margins, and section hierarchy.
- Avoid rendering issues: clipped text, overlapping elements, broken tables, black squares, or unreadable glyphs.
- Charts, tables, and images must be sharp, aligned, and clearly labeled.
- Use ASCII hyphens only. Avoid U+2011 and other Unicode dashes.
- Citations and references must be human-readable; never leave tool tokens or placeholder strings.

## Final Checks

- Do not deliver until the latest PNG inspection shows zero visual or formatting defects.
- Confirm headers, footers, page numbering, and section transitions look polished.
- Keep intermediate files organized or remove them after final approval.

## Final response

### Final Response Citations

- **Create/edit:** for created or edited PDFs, cite each final deliverable exactly once with `purpose="output"`, in its own paragraph. Briefly describe the result without repeating its filename, path, or link. Never put output directives inside prose or list items.
- **Q&A and summaries:** Every file whose contents you summarize or use to support an answer MUST receive a `:codex-file-citation{...}` with `purpose="source"` in the final response. Use the source citation in place of the filename, wherever the filename would appear. Do not write the filename separately and append its citation at the end. Files merely inspected but not used in the answer need no citation. Do not emit output citations for unchanged files or read-only answers.

- Emit `:codex-file-citation{...}` directly, without backticks, code fences, or a Markdown-link wrapper. Use verified targets only. No need to cite or reference intermediate work.

For file citations, set `path` to the verified absolute file path on the task host. Omit `mode`.

Some illustrative examples, real responses use verified targets outside code fences.

```text
:codex-file-citation{path="/absolute/path/review.pdf" purpose="output"}
```

```text
The review of :codex-file-citation{path="/absolute/path/review.pdf" purpose="source"} is due Friday.
```


### Additional Citation Guidance

For PDF Q&A, inspect complete relevant pages and preserve material headings, table/figure labels, footnotes, sources, and sample sizes. PDF citations support only plain file citations; do not add `artifact_kind`, `page_number`, or other locators.

# 24李林四套卷 数一 试题

## 第一套

### 选择题

1\. 设f（ ） 、VTtTlnltld，则f6 ）在 =0处  
A. 极限不存在.  
B.连续但不可导.  
D. 可导且导数不为零.  
C. 可导且导数为零.

2\. 设u（z y）的全微分du 一  
点（1,1）处的最大方向导数力  
A.JZ.  
B.2.  
C.1.  
D  
A. f！（0,0）存在.  
B.沿任一方向的方向导数均存在.  
D.可微.  
C. f$（0,0）存在.

4\. 设正项数列｛a。）， 。 满足c。=In（a。+e）（n 1,2.…••），则下列选项中错误的是  
B.若乙a。发散，则2b。发散.  
A. 若2a，收敛，则  
2 。收敛  
C.若乙a，收敛，则二6收敛.  
D.若之6发散，则之，发散.

5\. 设A是3阶矩阵，a=（1,2,3）「  
，8。=（0,2,1）「，a。 =（0,4,1）「，B=（1,0,0）「，若a」•02，  
8。是方程组 AX一B的三个解，则  
A. 当a=2时，必有r（A）=1.  
B.当4=2时，必有r（A）=2.  
C.当a 2时，必有r（A）=1.  
D.当a 2时，必有r（A）=2.

6\. 设A为3阶矩阵，3维列向量a，82，Q线性无关，A（a，Q： Qs）=（0」 Q 一0：），记 =  
（a+8,8，  
a：），则P AP  
1  
0  
B.  
0  
C.  
D.  
0  
A.  
0  
2  
-1  
0  
0  
一一  
I

7\. 若二次曲面 ”＋（k＋2）y 十k +2zy=5表示一个椭球面，则  
A.k>0.  
B.k<O.  
C.k >-1.  
D.k<-1.

8\. 设随机变量 X与Y均服从正态分布N（0,g），且 P（X≤1,Y≤-1｝=-  
，则P4X>1，  
Y>-1｝ =  
1  
A.1.  
B.7

9\. 设随机变量X服从参数为入（入＞0）的泊松分布，Y服从参数为-  
-的指数分布，则pxY=1  
的充分必要条件是  
A.Cov（X+Y,X）=0.  
B.cov（X-Y,X）=0.  
C.cov（X +Y,Y=0.  
D.cov（X-Y,Y+X）=0.

10\. 设X，X2，…，X。为总体X～N（y.G”）的简单随机样本，X 样本均值，若。”=  
k（X」 X）是。”的无偏估计量，则k=  
A.”！  
72  
72  
D.”+1  
B.  
C.  
72  
—1  
n+1'

### 填空题

= +1，

11\. 设函数 =f（z）由参数方程  
（t ≥ O确定，则极限lim z  
一（—1）"-1

14\. 级数2 n（2n+1）  
-的和为  
-’  
n=1  
I5.设A，B均为n阶矩阵，1B|=1，且（A一E）一=B’一E，其中B 为B的伴随矩阵，则  
1A+B|=

16\. 在区间（0.1）内随机取出 个数X， •… 。 表示n个数中大于会的个数，则 Y一

### 解答题

17\. （本题满分10分）  
m（t）  
f为非负可微函数，且f（0）=1,m（t）为立体52的质量，求lim  
•  
1-0。

18\. （本题满分12分）  
在第一象限内，过曲线3z’+2zy+3y”=a上任一点作其切线，若切线与两个坐标轴所  
围成的三角形面积的最小值为一  
一，求a 的值.

19\. （本题满分12分）  
设1是从点A（1,1）沿直线到点 B（ 1,0），再沿曲线y z” 1到点C（1,0）.  
计算1=厂，zdy-8da

20\. （本题满分12分）  
设f（ ）二阶可导， （ ）＞0且lim  
在：舖上的极瓶为a（）、记a、一【“4）］（心 为正能數）。  
（I）求ans  
（II） 求级数乙n”a。的和.  
n=！

21\. （本题满分12分）  
2  
1  
0  
a  
6  
设A=  
1  
2  
与B=  
0  
1  
0相似.  
LO  
0  
1  
——1  
—2  
（I）求a，b,c的值；  
（II） 求可逆矩阵P，使得PAP=B.  
（皿）求方程组（3E—A'）X=0的通解.

22\. （本题满分12分）  
（I）求Z的概率密度fz（z）；  
（II）X与Z是否相关，说明理由；  
（皿）若Z」，22，⋯，Z，为总体Z的简单随机样本，求。”的最大似然估计量。”.  
2024 考研数学终极预测4套卷.数学一•

## 第二套
# 李林四套卷数二（清晰版）

## 第一套

### 选择题

1\. 设f（z）在（一∞，+∞）内有二阶连续导数，且满足f（元）  
在z=0处的二次泰勒多项式为  
A.1—2z2.  
B.x-2z"  
C.1-z2.  
D.1+ .

2\. 设f（z）在［0,a］（a ＞0）上有二阶连续导数，且f（O）= '（0）=0,f”（z）严格单调递增，则  
A.4jzf（）dr <3el,f（z）dz.  
D.3f,ar（a）dr <4af,J（a）d  
＋ ” 0，  
若2=f（tan t, ln（1+t）），则当

3\. 设f（ y）  
=  
0，  
＋ =0.  
C.2.  
D. z.  
A.0.  
B. 1.

4\. 已知积分1-J（”-1）tr收敛.則。的取值范围为  
A. （-∞，0）.  
B. （0,1］•  
C. （1，+∞）.  
D. ［1，+∞）.  
arctan（z+1）

5\. 设a＞0,6 0,lim zln  
一=6，则  
arctan  
B.a =1,6=1  
A.a =1,0=  
2  
2  
C.a =2， =  
D.a=2,6=  
—  
2'  
A.e.  
B.e.  
C.e*.  
D.e'.  
ax  
十 ay  
A.dx +dy.  
B.-dr +dy.  
C.当d+当d.  
D.-  
pdr +ady.  
不同的点，则方程组  
1十ax2十fla）x3 f6）  
（ 1十c2十flczs=fla）  
A. 有唯一解.  
B. 有无穷多解.  
C.无解.  
D. 无法确定是否有解.  
1  
1

9\. 设A=  
1  
1  
0  
，则下列矩阵中与A既不相似也不合同的是  
L0  
「3  
0  
2  
1  
1  
一10  
［1  
0  
0  
A.  
0  
2  
{"source": "模拟卷40套整理合集PDF（可高清打印）（仅数二）/试卷/【紧凑版】26模拟卷数学二40套精选.pdf", "page": 4, "sha256": "bdd199d7f4926430028b53aaf7a7b7a0d8c312cb0e5d307c6fc52a6d6b44b211", "text": "微信公众号：考研佳友 精选40套·数学二\n26 张宇四套卷·卷一\n一、选择题：1～10小题，每小题5分，共50分\n1. 当 \\(x \\to 0^{+}\\) 时，下列无穷小量中，最高阶的是\nA. \\(\\int_0^{x^2} (e^{t^2} - 1) dt\\) B. \\(\\int_0^x \\ln(1 + \\sqrt{t^3}) dt\\) C. \\(\\int_0^{\\sin x} \\cos t^2 dt\\) D. \\(\\int_0^{1 - \\cos x} \\sqrt{\\arcsin^3 t} dt\\)\n2. \\(\\lim_{n \\to \\infty} \\left[ \\frac{n}{(n+1)^2} + \\frac{n}{(n+2)^2} + \\cdots + \\frac{n}{(n+n)^2} \\right] =\\)\nA. \\(\\frac{1}{3}\\) B. \\(\\frac{\\pi}{3}\\) C. \\(\\frac{1}{2}\\) D. \\(\\frac{\\pi}{2}\\)\n3. 曲线 \\(y = x + \\sqrt{x^2 - x + 1}\\) 的渐近线条数为\nA. 1 B. 2 C. 3 D. 4\n4. 函数 \\(f(x, y) = \\sqrt{|xy|}\\) 在 \\((0, 0)\\) 点\nA. 连续，但偏导数不存在. B. 偏导数存在且连续. C. 可微. D. 偏导数存在，但不可微.\n5. 设线密度为1的圆弧形细杆，其半径为1，圆心角为\\(\\theta\\)，摆放位置如图所示，\\(G\\) 为引力常数，则该细杆对圆心处质量为\\(m\\) 的质点\\(M\\) 的水平引力大小为\nA. \\(2Gm \\sin \\frac{\\theta}{2}\\) B. \\(\\sqrt{2}Gm \\sin \\frac{\\theta}{2}\\) C. \\(2Gm \\cos \\frac{\\theta}{2}\\) D. \\(\\sqrt{2}Gm \\cos \\frac{\\theta}{2}\\)\n6. 若微分方程 \\(y'' + ay' + by = 0\\) 的解在 \\((-\\infty, +\\infty)\\) 上必为周期函数，则\nA. \\(a = 0, b > 0\\) B. \\(a = 0, b < 0\\) C. \\(a \\neq 0, b < 0\\) D. \\(a \\neq 0, b > 0\\)\n7. \\(\\int_{\\frac{1}{4}}^{\\frac{1}{2}} dy \\int_{\\frac{1}{2}}^{\\sqrt{\\frac{3}{2}}} e^{\\frac{y}{2}} dx + \\int_{\\frac{1}{2}}^{1} dy \\int_{\\frac{3}{2}}^{\\sqrt{\\frac{3}{2}}} e^{\\frac{y}{2}} dx =\\)\nA. \\(\\frac{3e}{4} - \\frac{\\sqrt{e}}{2}\\). B. \\(\\frac{3e}{4} + \\frac{\\sqrt{e}

## assistant · 2026-11-12T00:23:19Z

我会用 PDF 技能查看原卷版面，直接核对 OCR 容易丢失的题干、公式和选项。

## tool · 2026-11-12T00:23:26Z


Script completed
Wall time 1.1 seconds
Output:

{"chunk_id":"da4d51","wall_time_seconds":0.971125166,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"67e6b0","wall_time_seconds":0.412318834,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"fff6d7","wall_time_seconds":0.000009542,"exit_code":0,"original_token_count":1207,"output":"507:[Omitted long matching line]\n508:[Omitted long matching line]\n509:[Omitted long matching line]\n510:[Omitted long matching line]\n511:[Omitted long matching line]\n512:[Omitted long matching line]\n513:[Omitted long matching line]\n514:[Omitted long matching line]\n515:[Omitted long matching line]\n516:[Omitted long matching line]\n517:[Omitted long matching line]\n518:[Omitted long matching line]\n519:[Omitted long matching line]\n520:[Omitted long matching line]\n521:[Omitted long matching line]\n522:[Omitted long matching line]\n523:[Omitted long matching line]\n524:[Omitted long matching line]\n525:[Omitted long matching line]\n526:[Omitted long matching line]\n527:[Omitted long matching line]\n528:[Omitted long matching line]\n529:[Omitted long matching line]\n530:[Omitted long matching line]\n531:[Omitted long matching line]\n532:[Omitted long matching line]\n533:[Omitted long matching line]\n534:[Omitted long matching line]\n535:[Omitted long matching line]\n536:[Omitted long matching line]\n537:[Omitted long matching line]\n538:[Omitted long matching line]\n539:[Omitted long matching line]\n540:[Omitted long matching line]\n541:[Omitted long matching line]\n542:[Omitted long matching line]\n543:[Omitted long matching line]\n544:[Omitted long matching line]\n545:[Omitted long matching line]\n546:[Omitted long matching line]\nconst fs = require(\"node:fs\");\nconst katex = require(\"./proof-katex/node_modules/katex\");\n\nlet total = 0;\nfor (const filename of process.argv.slice(2)) {\n  const body = fs.readFileSync(filename, \"utf8\");\n  const spans = body.matchAll(/(?<!\\\\)(\\$\\$|\\$)([\\s\\S]*?)(?<!\\\\)\\1/g);\n  for (const [full, delimiters, expression] of spans) {\n    try {\n      katex.renderToString(expression, { displayMode: delimiters.length === 2, throwOnError: true });\n    } catch (error) {\n      throw new Error(filename + \" \" + full + \": \" + error.message);\n    }\n    total += 1;\n  }\n}\nconsole.log(total + \" math expressions rendered\");\nimport re\nimport sys\nfrom pathlib import Path\n\n\nroot = Path(\"references/302模拟27md\")\nvolume = Path(sys.argv[1]).read_text(encoding=\"utf-8\").strip()\nmatch = re.match(r\"^## ([^\\n]+)\", volume)\nassert match\nname = match[1]\nnumbering = re.findall(r\"(?m)^(\\d+)\\\\\\.\", volume)\nassert numbering == list(map(str, range(1, 23))), numbering\nquestions = re.split(r\"(?m)^\\d+\\\\\\.\", volume)[1:]\nassert all(re.findall(r\"(?m)^([A-D])\\. \", block) == list(\"ABCD\") for block in questions[:10])\nassert all(block.strip() for block in questions)\nassert volume.count(\"$\") % 2 == 0\nfor name_arg in sys.argv[2:]:\n    paths = list(root.rglob(name_arg))\n    assert len(paths) == 1, name_arg\n    path = paths[0]\n    original = path.read_text(encoding=\"utf-8\")\n    if name_arg == \"考研数学冲刺预测6套卷.pdf.md\":\n        source_title = f\"第{name[-1]}套\"\n        verified = volume.replace(f\"## {name}\", f\"## {source_title}\", 1)\n        if name == \"卷一\":\n            verified = verified.replace(r\"^{1+\\sin v}\", r\"^{1+\\sin t}\", 1)\n            verified = verified.replace(\n                r\"\\begin{pmatrix}\\lambda_1&&\\\\&\\lambda_2&\\\\&&\\lambda_3\\end{pmatrix}\",\n                r\"\\operatorname{diag}(\\lambda_1,\\lambda_2,\\lambda_3)\",\n                1,\n            )\n        if name == \"卷四\":\n            verified = verified.replace(\n                \"B. $a=\\\\pi,b=-1$  \\nC. $a=\\\\frac\\\\pi2,b=-1$\",\n                \"B. $a=\\\\frac\\\\pi2,b=-1$  \\nC. $a=\\\\pi,b=-1$\",\n                1,\n            )\n            verified = verified.replace(r\"{-4xy^b}\", r\"{-4yx^b}\", 1)\n            verified = verified.replace(\n                r\"C=\\begin{pmatrix}-2&0&0\\\\0&1&0\\\\0&0&3\\end{pmatrix}\",\n                r\"C=\\begin{pmatrix}-2&0&0\\\\0&1&0\\\\0&0&1\\end{pmatrix}\",\n                1,\n            )\n        if name == \"卷五\":\n            verified = verified.replace(r\"F(x)=\\int_1^{x^2}\", r\"F(x)=\\int_1^2\", 1)\n            verified = verified.replace(\n                r\"\\int_{\\frac12+\\sqrt{\\frac14-x^2}}^{\\frac12-\\sqrt{\\frac14-x^2}}\",\n                r\"\\int_{\\frac12-\\sqrt{\\frac14-x^2}}^{\\frac12+\\sqrt{\\frac14-x^2}}\",\n                1,\n            )\n            verified = verified.replace(\n                r\"\\int_{\\frac12-\\sqrt{\\frac14-y^2}}^{\\sqrt{y-y^2}}\",\n                r\"\\int_0^{\\sqrt{y-y^2}}\",\n                1,\n            )\n            verified = verified.replace(\n                r\"\\sum_{i=1}^{2n}\\sum_{j=1}^n\",\n                r\"\\sum_{j=1}^{2n}\\sum_{i=1}^n\",\n                1,\n            )\n    else:\n        source_title = name\n        verified = volume\n    heading = re.compile(r\"(?ms)^## \" + re.escape(source_title) + r\"$.*?(?=^## |\\Z)\")\n    updated, count = heading.subn(lambda _: verified + \"\\n\\n\", original)\n    assert count == 1, (name_arg, name)\n    path.write_text(updated.rstrip() + \"\\n\", encoding=\"utf-8\")\n    assert heading.search(path.read_text(encoding=\"utf-8\"))[0].rstrip() == verified\n    print(path)\n"}

## tool · 2026-11-12T00:23:30Z


Script completed
Wall time 0.0 seconds
Output:

7
{
  "type": "input_image",
  "image_url": "images/78aff9013e56616961aeae80e271ee38d06af6b7f03cfed1ed30ec883b7e4f63.png",
  "detail": "high"
}
8
{
  "type": "input_image",
  "image_url": "images/5dbcf8364e4e6409101b3899f0f13ae05a1ab505cbc8f53831458a92534d7b4c.png",
  "detail": "high"
}
9
{
  "type": "input_image",
  "image_url": "images/e9f0921f3baf9785697b2254cd57d9bae23694e58b9b0c5bee664de59ba46f6f.png",
  "detail": "high"
}
10
{
  "type": "input_image",
  "image_url": "images/51fc889941bf166aa2403298e491f1f957069e43a07aa85286cadf1c6c03a7d9.png",
  "detail": "high"
}
11
{
  "type": "input_image",
  "image_url": "images/e5626a09c51c61e9a8e7b263a8b3cb4bfd5069908bf78359e0a76d64f8ce0f35.png",
  "detail": "high"
}

## tool · 2026-11-12T00:23:38Z


Script completed
Wall time 0.3 seconds
Output:

('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 6)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 7)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 8)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 9)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 10)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 11)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 12)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 13)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 14)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 15)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 16)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 17)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 18)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 19)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 20)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 21)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 22)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 23)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 24)
('往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf', 25)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 7)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 8)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 9)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 10)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 11)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 12)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 13)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 14)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 15)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 16)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 17)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 18)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 19)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 20)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 21)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 22)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 23)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 24)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 25)
('模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf', 26)


## tool · 2026-11-12T00:23:44Z


Script completed
Wall time 0.1 seconds
Output:

6
{
  "type": "input_image",
  "image_url": "images/d3f4f9cf0e8c0acf1438e405bbe11114542f39e2355e2d6bc369ac8c45e3c9f3.png",
  "detail": "high"
}
(6, '考研数学终极预测4套卷\n第一套\n考研数学终极预测4套卷\n第一套\n一、选择题：1～10小题，每小题5分，共50分。下列每题给出的四个选项中，只有一个选项是最符合题目要求的。\n1. 设 \\(f(x)=\\int_{-1}^{x}\\sqrt{|t|}\\ln|t|\\) dt，则 \\(f(x)\\) 在 x=0 处\nA. 极限不存在. B. 连续但不可导.\nC. 可导且导数为零. D. 可导且导数不为零.\n2. 设 \\(u(x,y)\\) 的全微分 \\(\\mathrm{d}u=\\frac{axy^{2}}{(x^{2}+y^{2})^{2}}\\mathrm{d}x+\\frac{-4yx^{6}}{(x^{2}+y^{2})^{2}}\\mathrm{d}y\\) (x>0,y>0)，则 \\(u(x,y)\\) 在点 (1,1) 处的最大方向导数为\nA. \\(\\sqrt{2}\\). B. 2. C. 1. D. \\(\\frac{1}{2}\\).\n3. 设 \\(f(x,y)=\\sqrt{x^{2}+y^{2}}\\)，则 \\(f(x,y)\\) 在点 (0,0) 处\nA. \\(f_{x}^{\\prime}(0,0)\\) 存在. B. 沿任一方向的方向导数均存在.\nC. \\(f_{y}^{\\prime}(0,0)\\) 存在. D. 可微.\n4. 设正项数列 \\(\\{a_{n}\\}\\)，\\(\\{b_{n}\\}\\) 满足 \\(a_{n}=\\ln(a_{n}+e^{b_{n}})\\) (n=1,2,\\cdots)，则下列选项中 \\(\\underset{\\cdot}{错}\\underset{\\cdot}{误}\\) 的是\nA. 若 \\(\\sum_{n=1}^{\\infty}a_{n}\\) 收敛，则 \\(\\sum_{n=1}^{\\infty}b_{n}\\) 收敛. B. 若 \\(\\sum_{n=1}^{\\infty}a_{n}\\) 发散，则 \\(\\sum_{n=1}^{\\infty}b_{n}\\) 发散.\nC. 若 \\(\\sum_{n=1}^{\\infty}a_{n}\\) 收敛，则 \\(\\sum_{n=1}^{\\infty}b_{n}^{2}\\) 收敛. D. 若 \\(\\sum_{n=1}^{\\infty}b_{n}^{2}\\) 发散，则 \\(\\sum_{n=1}^{\\infty}a_{n}\\) 发散.\n5. 设 A 是 3 阶矩阵，\\(\\alpha_{1}=(1,2,3)^{\\mathrm{T}}\\)，\\(\\alpha_{2}=(0,2,1)^{\\mathrm{T}}\\)，\\(\\alpha_{3}=(0,a,1)^{\\mathrm{T}}\\)，\\(\\beta=(1,0,0)^{\\mathrm{T}}\\)，若 \\(\\alpha_{1},\\alpha_{2}\\)，\\(\\alpha_{3}\\) 是方程组 AX=\\(\\beta\\) 的三个解，则\nA. 当 a=2 时，必有 r(A)=1. B. 当 a=2 时，必有 r(A)=2.\nC. 当 a\\(\\neq\\)2 时，必有 r(A)=1. D. 当 a\\(\\neq\\)2 时，必有 r(A)=2.\n6. 设 A 为 3 阶矩阵，3 维列向量 \\(\\alpha_{1},\\alpha_{2},\\alpha_{3}\\) 线性无关，A\\((\\alpha_{1},\\alpha_{2},\\alpha_{3})=\\left(\\alpha_{1},\\alpha_{2},-\\alpha_{3}\\right)\\)，记 P=\\((\\alpha_{1}+\\alpha_{3},\\alpha_{2},-\\alpha_{3})\\)，则 P^{-1}AP=___\nA. \\(\\begin{bmatrix}1&0&0\\\\0&1&0\\\\2&0&-1\\end{bmatrix}\\). B. \\(\\begin{bmatrix}1&0&0\\\\0&1&0\\\\0&0&-1\\end{bmatrix}\\). C. \\(\\begin{bmatrix}1&0&0\\\\0&1&0\\\\1&0&-1\\end{bmatrix}\\). D. \\(\\begin{bmatrix}1&0&0\\\\0&1&0\\\\-1&0&1\\end{bmatrix}\\).')
(7, '李林4套卷之：\n2024考研数学终极预测4套卷.数学一\n7.若二次曲面\\(x^{2}+(k+2)y^{2}+kz^{2}+2xy=5\\)表示一个椭球面，则\nA.k>0. B.k<0.\nC.k>-1. D.k<-1.\n8.设随机变量X与Y均服从正态分布\\(N(0,\\sigma^{2})\\)，且\\(P\\{X\\leq1,Y\\leq-1\\}=\\frac{1}{4}\\)，则\\(P\\{X>1,Y>-1\\}=\\)\nA.1. B.\\(\\frac{1}{4}\\). C.\\(\\frac{1}{2}\\). D.\\(\\frac{3}{4}\\).\n9. 设随机变量X服从参数为\\(\\lambda (\\lambda>0)\\)的泊松分布，Y服从参数为\\(\\frac{1}{\\sqrt{\\lambda}}\\)的指数分布，则\\(\\rho_{XY}=1\\)的充分必要条件是\nA. \\(\\mathrm{cov}(X+Y,X)=0\\). B. \\(\\mathrm{cov}(X-Y,X)=0\\). C. \\(\\mathrm{cov}(X+Y,Y)=0\\). D. \\(\\mathrm{cov}(X-Y,Y+X)=0\\).\n10. 设\\(X_{1},X_{2},\\cdots,X_{n}\\)为总体X\\(\\sim\\)N\\((\\mu,\\sigma^{2})\\)的简单随机样本，\\(\\overline{X}\\)为样本均值，若\\(\\hat{\\sigma}^{2}=k(X_{1}-\\overline{X})^{2}\\)是\\(\\sigma^{2}\\)的无偏估计量，则k=\nA.\\(\\frac{n-1}{n}\\). B.\\(\\frac{n}{n-1}\\). C.\\(\\frac{n}{n+1}\\). D.\\(\\frac{n+1}{n}\\).\n二、填空题：11～16小题，每小题5分，共30分.\n11. 设函数y=f(x)由参数方程\\(\\left\\{\\begin{array}{l}x=t^{2}+1, \\\\ y=4t-t^{2},\\end{array}\\right.\\)(t≥0)确定，则极限\\(\\lim_{n\\to\\infty}n\\left[f\\left(\\frac{2n+1}{n}\\right)-3\\right]=\\)____.\n12. 设曲线L为球面\\(x^{2}+y^{2}+z^{2}=1\\)与圆柱面\\(x^{2}+y^{2}=x\\)在上半平面(z≥0)的交线，从x轴正向看去为逆时针方向，则\\(\\int_{L}y^{2}\\mathrm{d}x+z^{2}\\mathrm{d}y+x^{2}\\mathrm{d}z=\\)____.\n13. 设上半球面\\(\\Sigma:z=\\sqrt{1-x^{2}-y^{2}}\\)，其密度\\(\\rho=z\\)，则\\(\\Sigma\\)的质心坐标\\(\\overline{z}=\\)____.\n14. 级数\\(\\sum_{n=1}^{\\infty}\\frac{(-1)^{n-1}}{n(2n+1)}\\)的和为____.\n15. 设A，B均为n阶矩阵，|B|=1，且\\((A-E)^{-1}=B^{*}-E\\)，其中\\(B^{*}\\)为B的伴随矩阵，则\\(\\left|A^{-1}+B\\right|=\\)____.\n16. 在区间(0,1)内随机取出n个数\\(X_{1},X_{2},\\cdots,X_{n}\\)，Y表示n个数中大于\\(\\frac{2}{3}\\)的个数，则DY=____.\n2')


## tool · 2026-11-12T00:23:57Z


Script completed
Wall time 0.3 seconds
Output:

{}
{"chunk_id":"5a0f23","wall_time_seconds":0.082222291,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"af1fc4","wall_time_seconds":0.107071042,"exit_code":0,"original_token_count":0,"output":""}

## tool · 2026-11-12T00:23:59Z


Script completed
Wall time 0.0 seconds
Output:

6
{
  "type": "input_image",
  "image_url": "images/74dc2d577f4effacc8130f03d2f952f0545867e1bb5b94283f2124e4de3985b2.png",
  "detail": "high"
}
7
{
  "type": "input_image",
  "image_url": "images/2f20390ac68d93cbc42741d7d0141230eee3f0635efc68e14f618348064beaf6.png",
  "detail": "high"
}

## tool · 2026-11-12T00:25:06Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-12T00:25:12Z


Script completed
Wall time 0.2 seconds
Output:

169 math expressions rendered
references/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md

12
{
  "type": "input_image",
  "image_url": "images/9ffd0dfd06d5e51fb545a0e1ad11fea6c61821d8f0c1293c5d9d72b1a0229141.png",
  "detail": "high"
}
13
{
  "type": "input_image",
  "image_url": "images/e248429d00e005346585b6511606b47be30869fab02ab570f1888e29b86f1acf.png",
  "detail": "high"
}
14
{
  "type": "input_image",
  "image_url": "images/cdff2a2ae0532e5026472502085f19907e62b286ab786cab0d508caa3e2e0388.png",
  "detail": "high"
}
15
{
  "type": "input_image",
  "image_url": "images/109eb48036cba4a0afe057c3fa88e56bf3ef3d78ea5888ec61b098737937d950.png",
  "detail": "high"
}

## tool · 2026-11-12T00:25:23Z


Script completed
Wall time 0.3 seconds
Output:

11
李林4套卷之：
2024考研数学终极预测4套卷数学一
考研数学终极预测4套卷
第二套
一、选择题：1～10小题，每小题5分，共50分.下列每题给出的四个选项中，只有一个选项是最符合题目要求的.
1. 设 y=f(x) 在 \([0,+\infty)\) 上有二阶连续导数，f''(x)>0, y=g(x) 是 y=f(x) 在 (0,+\infty) 内任意点 x₀ 处的切线方程，F(x)=f(x)-g(x)，则
A. F(x) 在 x₀ 处取得最大值.
B. F(x) 在 x₀ 处取得最小值.
C. (x₀,F(x₀)) 为 y=F(x) 的拐点.
D. F(x) 在 x₀ 处不取得极值.
2. 设 D = \(\{(x,y)\mid(x-1)^{2}+y^{2}\leqslant1\}\)，I₁=\(\iint_{D}\sqrt{2x-x^{2}-y^{2}}dxdy\)，I₂=\(\iint_{D}\sqrt{2x^{2}+y^{2}-2x+1}dxdy\)，则 I₁: I₂: I₃=
A. 2:1:2. B. 2:2:1. C. 1:2:2. D. 2:1:1.
3. 设某生物分布在 xOy 坐标平面上，分布密度 f(r) 随着与原点的距离 r 的增加而减少，其中，f(r)=\(\frac{a}{r^{2}+b}\)(只/m²)，a、b 均为大于零的常数，则距离原点 2m 的圆形区域内存在生物的数目(单位：只)为
A. \(\frac{a}{2}\ln\left(1+\frac{4}{b}\right)\). B. \(\pi a\ln\left(1+\frac{4}{b}\right)\).
C. \(a\ln\left(1+\frac{4}{b}\right)\). D. \(\frac{1}{2}\pi a\ln\left(1+\frac{4}{b}\right)\).
4. 设D=\(\{(x,y)\mid(x-1)^{2}+(y-1)^{2}\leqslant2\}\)，L 为区域D的边界曲线，取顺时针方向，I₁=\(\int_{L}x\mathrm{d}x+\frac{(x+y)^{2}}{8}\mathrm{d}y\)，I₂=\(\int_{L}x\mathrm{d}x+\frac{(x-y)^{2}}{8}\mathrm{d}y\)，I₃=\(\int_{L}\frac{(x+y)^{2}}{8}\mathrm{d}x+y\mathrm{d}y\)，则
A. I₁>I₂>I₃. B. I₃>I₂>I₁. C. I₂>I₃>I₁. D. I₂>I₁>I₃.
5. 设3维列向量 \(\alpha_{1},\alpha_{2},\alpha_{3}\) 线性无关，A=(a_{ij})₃×₃×₂，满足 A\(\alpha_{1}\)=a₁，A\(\alpha_{2}\)=a₂-a₃，A\(\alpha_{3}\)=a₃-a₁，则 A⁻¹ 的迹 \(\mathrm{tr}(A^{-1})\)=
A. 1. B. -1. C. -3. D. 3.
6
12
考研数学终极预测4套卷
第二套
6. 设A为二阶实矩阵，\(\alpha\)与\(\beta\)是A的两个单位实特征向量，且满足\(\|\alpha+\beta\|=\|\alpha-\beta\|\)，则
A. r(A)=1. B. r(A)=2.
C. A必相似于对角矩阵. D. A必与单位矩阵合同.
7. 设矩阵\(A_{n\times n}\)，\(B_{n\times n}\)，\(E_{n\times n}\)为单位矩阵，且\(r(A)=s\)，\(r(B)=n\)，下列齐次线性方程组有非零解的是
A. \(\begin{bmatrix} AB & O \\ E & A \end{bmatrix} X=0\). B. \(\begin{bmatrix} AB & O \\ E & B \end{bmatrix} X=0\).
C. \(\begin{bmatrix} A & E \\ O & AB \end{bmatrix} X=0\). D. \(\begin{bmatrix} A & AB \\ E & B \end{bmatrix} X=0\).
8. 设随机事件A，B，满足P(A)=0.4，P(A∩B)=0.7，P(B∩A)=1，则P(A∩B)=
A. 0.2. B. 0.4. C. 0.6. D. 0.8.
9. 设二维随机变量(X，Y)服从N(μ，μ；1，1；0)，则D(|X-Y|)=
A. \(1-\sqrt{\frac{2}{\pi}}\). B. \(2-\frac{4}{\pi}\).
C. \(2-\frac{4}{\sqrt{\pi}}\). D. \(1-\frac{2}{\sqrt{\pi}}\).
10. 设\(X_{1},X_{2},\cdots,X_{n}(n>1)\)为来自总体N(μ，σ²)的简单随机样本，\(\overline{X}\)为样本均值，S²为样本方差，则\(\mu\sigma^{2}\)的无偏估计量为
A. \(\overline{X}^{2}S\). B. \(\overline{X}S\). C. \(\overline{X}S^{2}\). D. \(\overline{X}^{2}S^{2}\).
二、填空题：11～16小题，每小题5分，共30分.
11. 设f(x)=\(\arctan\frac{1+x}{1-x}\)，n为正整数，则f^{(2n+1)}(0)=______.
12. 心形线r=1+\(\cos\theta\)的全长为_____.
13. 设函数f(x,y，z)=x²+2y²+3z²-a²(a>0)满足x-2y+3z=6的最小值为0，则a=_____.
14. 设曲线L为\(\begin{cases}x^{2}+y^{2}+z^{2}=R^{2},(R>0)\\x+y+z=0,\end{cases}\)则I=∮_{L}(xy+yz+zx)ds=_____.
15. 设\(\alpha_{1}\)=(1,1,1)ᵀ，\(\alpha_{2}\)=(1,0,-1)ᵀ，\(\alpha_{3}\)=(1,0,1)ᵀ与\(\beta_{1}\)=(1,2,1)ᵀ，\(\beta_{2}\)=(3,3,3)ᵀ，\(\beta_{3}\)=(2,4,3)ᵀ是R²的两组基，则在两组基下有相同坐标的向量为_____.
16. 设随机变量X在区间(0，a)(a>0)上服从均匀分布，则X落在EX与DX之间的概率为_____.
7
13
李林4套卷之：
2024考研数学终极预测4套卷.数学一
三、解答题：17～22小题，共70分.解答应写出文字说明、证明过程或演算步骤.
17.（本题满分10分）
设函数 \(y(x)\) 是微分方程 \((xy-1)\mathrm{d}x+x^{2}\mathrm{d}y=0(x>0)\) 的解，且 \(y(1)=0\).
求曲线 \(y=y(x)\) 的凹凸区间及拐点.
18.（本题满分12分）
设非负函数 \(f(x)\) 在 \([0,a]\) \((a>0)\) 上有连续的二阶导数，且 \(f(0)=f'(0)=0,f''(x)\) 严格单调递增，平面区域 \(D=\{(x,y)\mid0\leqslant x\leqslant a,0\leqslant y\leqslant f(x)\}\) 的形心坐标为 \((\bar{x},\bar{y})\).
证明：\(\bar{x}>\frac{3}{4}a\).
14
考研数学终极预测4套卷
第二套
19.（本题满分12分）
设数列\(\{a_{n}\}\)满足\(a_{0}=2,na_{n}=a_{n-1}+n-1(n=1,2,\cdots)\).
（I）证明\(\lim_{n\to\infty}a_n\)存在并求其值；
（II）求幂级数\(\sum_{n=0}^{\infty}a_nx^n\)的收敛区间与和函数.
20.（本题满分12分）
发现一架飞机在原点O(0,0)处沿y轴正向以常速度v飞行，随即从点P₀(16,0)处发射导弹追击，且导弹方向始终指向飞机，导弹速度为2v，如右图所示.
（I）求导弹飞行轨迹y=y(x)的表达式；
（II）求飞机被击中的位置及所需时间T.
9
15
李林4套卷之：
2024考研数学终极预测4套卷.数学一
21.(本题满分12分)
设二次型 \(f(x_{1},x_{2},x_{3})=\boldsymbol{X}^{\mathrm{T}}\boldsymbol{A}\boldsymbol{X}(\boldsymbol{A}^{\mathrm{T}}=\boldsymbol{A})\) 经正交变换X=QY化为\(by_{2}^{2}+c^{2}y_{3}^{2}\)，其中，\(Q=\frac{1}{\sqrt{2}}\begin{bmatrix}1&0&a\\ 0&c&0\\ b&0&1\end{bmatrix}(b>0,c>0)\).
(Ⅰ)求a,b,c的值及矩阵A；
(Ⅱ)求可逆矩阵P，使得\(A+E=P^{T}P\).
22.(本题满分12分)
设随机变量X在区间\(\left(-\frac{\pi}{2},\frac{\pi}{2}\right)\)上服从均匀分布，\(P\{Y=0\}=P\{Y=1\}=\frac{1}{2}\)，且X与Y相互独立，记\(Z=\left|\sin X\right|\).
(Ⅰ)求Z的概率密度；
(Ⅱ)求V=Y+Z的概率密度.
10


## tool · 2026-11-12T00:25:25Z


Script completed
Wall time 0.0 seconds
Output:

12
{
  "type": "input_image",
  "image_url": "images/4476ef0a41b271fa8fa6045b8473ad1cf5fad077402462e9fda1776db134d951.png",
  "detail": "high"
}
13
{
  "type": "input_image",
  "image_url": "images/20564661dd1a69c5715470327bf94430ad0e1e604137ac2712ff482cd267d530.png",
  "detail": "high"
}
14
{
  "type": "input_image",
  "image_url": "images/396f51ee172cf791a93fec4d7772aa24a191c551b014c9959f9a523f62b9d566.png",
  "detail": "high"
}

## tool · 2026-11-12T00:25:32Z


Script completed
Wall time 0.2 seconds
Output:


## tool · 2026-11-12T00:25:34Z


Script completed
Wall time 0.0 seconds
Output:

13
{
  "type": "input_image",
  "image_url": "images/d1ed39d6c9a49c18c615344fd8ea57fcd5dae798dea66085d129501f0306276e.png",
  "detail": "high"
}
14
{
  "type": "input_image",
  "image_url": "images/779e6fe806c9790a807b1cb6a9a6d09987891a9e6cd61652e1fe027e9c705d0e.png",
  "detail": "high"
}
12
{
  "type": "input_image",
  "image_url": "images/93e7f063f3abafd2e3b23555570a18cf7c8d1007234f5080b81df02456a9c082.png",
  "detail": "high"
}

## tool · 2026-11-12T00:26:46Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-12T00:26:52Z


Script completed
Wall time 0.2 seconds
Output:

177 math expressions rendered
references/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md

16
{
  "type": "input_image",
  "image_url": "images/80ec58c3e2490555214ca6aef88d01f6b0f9b6ea1156b0334301f9c875279654.png",
  "detail": "high"
}
17
{
  "type": "input_image",
  "image_url": "images/a01dd26c1bc2e722cc277054a193e662fec9199a7212b6e85a25299681d88488.png",
  "detail": "high"
}
18
{
  "type": "input_image",
  "image_url": "images/d1a268e8237594dd1f467178bd2cf1db790a6aeba20b9f5a4bd0af29b82f6e98.png",
  "detail": "high"
}
19
{
  "type": "input_image",
  "image_url": "images/a91fe56b0d788b2badf011c83e2057456ab8213644f6f4404a1d3ad9fdf72068.png",
  "detail": "high"
}
20
{
  "type": "input_image",
  "image_url": "images/9d07fc47a5b6ca7c2f4f78faeef863c7b62ff8dbddd21afb4e0eb143f8514244.png",
  "detail": "high"
}

## tool · 2026-11-12T00:26:58Z




## tool · 2026-11-12T00:27:04Z


Script completed
Wall time 0.2 seconds
Output:

17
{
  "type": "input_image",
  "image_url": "images/4c9b93155c78a4938faeab735a3fcee3b408ec13649c16515bebc79c7fb37071.png",
  "detail": "high"
}
19
{
  "type": "input_image",
  "image_url": "images/d7ca2c7df5308ab84e0578572f137dead750789ba1bad2d5b552efd6b6db270c.png",
  "detail": "high"
}
18
{
  "type": "input_image",
  "image_url": "images/b042a040959a0b66cbc9c55fc302efa949edf10e4e0c67e3f951ef81a305bba3.png",
  "detail": "high"
}

## tool · 2026-11-12T00:27:14Z


Script completed
Wall time 0.2 seconds
Output:

19
{
  "type": "input_image",
  "image_url": "images/dd84b6c49ab2dc276bb5bf6322f5638d15c1edc1913d2d731e1805c9aa3d6763.png",
  "detail": "high"
}
17
{
  "type": "input_image",
  "image_url": "images/692151145c84690d9ddffdb766d7eb193d547f498c89b0ced4aad5f50151661d.png",
  "detail": "high"
}
20
{
  "type": "input_image",
  "image_url": "images/c2bd8540c997941b2f1fe8319af34c6828336ad452a89dcd4b349bdbe7d7acf6.png",
  "detail": "high"
}

## tool · 2026-11-12T00:28:25Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-12T00:28:33Z


Script completed
Wall time 0.3 seconds
Output:

171 math expressions rendered
references/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md

21
{
  "type": "input_image",
  "image_url": "images/46ce61a48b36ca733cb7d5e3a0a2cf298b6e5fa185117fe784637e1edc175822.png",
  "detail": "high"
}
22
{
  "type": "input_image",
  "image_url": "images/b509c0c000c100a1b5bf4bb32317b3e5b41f055a33605981c315cc8f91ba5a18.png",
  "detail": "high"
}
23
{
  "type": "input_image",
  "image_url": "images/6169dc24c9ad3d1eaa0b61f37127bd16f82f4b2caba39e6c259b86e6cc27aaa8.png",
  "detail": "high"
}
24
{
  "type": "input_image",
  "image_url": "images/2de766f47d84e07090035db95ee666fc94f66836f4520135e739b68f967448e4.png",
  "detail": "high"
}
25
{
  "type": "input_image",
  "image_url": "images/e234934953168dbc7e1dad6c61b1dd4304f9914240b1b93edef1f709dd266298.png",
  "detail": "high"
}

## tool · 2026-11-12T00:28:43Z


Script completed
Wall time 0.2 seconds
Output:

9
{
  "type": "input_image",
  "image_url": "images/ac6ccae0a5403034dc32d532e3f2c0f545d048aa1e2f8f2e8a2a19fe522e4619.png",
  "detail": "high"
}
14
{
  "type": "input_image",
  "image_url": "images/3c5d391cadfda3e05fa99acfa577be02ba0816fc4c67083f38d02650a74e9920.png",
  "detail": "high"
}

## tool · 2026-11-12T00:28:45Z


Script completed
Wall time 0.0 seconds
Output:

21
{
  "type": "input_image",
  "image_url": "images/a27dc56fba0c8f2f421054fcd5d91d4eb83b261dc6049acd633bb28c7f920e51.png",
  "detail": "high"
}
22
{
  "type": "input_image",
  "image_url": "images/6e0f53fa1818eab86aaaeafee52f596920d767227c62f087c70b620c8b88606a.png",
  "detail": "high"
}

## tool · 2026-11-12T00:28:51Z


Script completed
Wall time 0.2 seconds
Output:

22
{
  "type": "input_image",
  "image_url": "images/3b4309a22a9b171d66887a3847de1db5db7b2ec392044c5d0346c48fd899bb2f.png",
  "detail": "high"
}

## tool · 2026-11-12T00:30:10Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-12T00:30:21Z


Script completed
Wall time 0.3 seconds
Output:

{}
{"chunk_id":"1697a4","wall_time_seconds":0.06127175,"exit_code":0,"original_token_count":120,"output":"references/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md\n690 math expressions rendered\n"}

## tool · 2026-11-12T00:30:26Z




## assistant · 2026-11-12T00:30:29Z

数一四套共 88 题已核对并写回 Markdown，690 处数学表达式通过渲染检查。我正在核对数二原卷。

## tool · 2026-11-12T00:30:30Z


Script completed
Wall time 0.0 seconds
Output:

7
{
  "type": "input_image",
  "image_url": "images/9124b643ce7f0afb1f362c4f81590e14ce6154658e7b6b0cb41607b90228687a.png",
  "detail": "high"
}
8
{
  "type": "input_image",
  "image_url": "images/173a05dd2c7e38a7c40bc51fdb04685270cebfd31c9e06b0965a728fbd453f17.png",
  "detail": "high"
}
9
{
  "type": "input_image",
  "image_url": "images/57b32ab2917a2c3e548d7ad370013b144a5a4045fe6cfc18a75fcdbb722aba5d.png",
  "detail": "high"
}
10
{
  "type": "input_image",
  "image_url": "images/81449232a91df044e2ec1415f8436f68ca22df25a933c1e8beb751ed9a4c057e.png",
  "detail": "high"
}
11
{
  "type": "input_image",
  "image_url": "images/7cbfd551575ba0def7d3ae4e4c6918082192abbd3447089385843b17a1b7e36b.png",
  "detail": "high"
}

## tool · 2026-11-12T00:30:37Z


Script completed
Wall time 0.1 seconds
Output:

references/302模拟27md/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf.md:3:## 24 李林四套卷· 卷一
references/302模拟27md/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf.md:401:## 24 李林四套卷· 卷二
references/302模拟27md/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf.md:776:## 24 李林四套卷· 卷三
references/302模拟27md/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf.md:1242:## 24 李林四套卷· 卷四
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf.md:3:## 24 李林四套卷· 卷一
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf.md:471:## 24 李林四套卷· 卷二
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf.md:632:二次泰勒多项式为  
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf.md:878:## 24 李林四套卷· 卷三
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf.md:1493:## 24 李林四套卷· 卷四
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf.md:3:## 24 李林四套卷· 卷一
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf.md:401:## 24 李林四套卷· 卷二
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf.md:777:## 24 李林四套卷· 卷三
references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf.md:1243:## 24 李林四套卷· 卷四
references/302模拟27md/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf.md:3:## 24 李林四套卷· 卷一
references/302模拟27md/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf.md:471:## 24 李林四套卷· 卷二
references/302模拟27md/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf.md:632:二次泰勒多项式为  
references/302模拟27md/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf.md:878:## 24 李林四套卷· 卷三
references/302模拟27md/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf.md:1492:## 24 李林四套卷· 卷四
references/302模拟27/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf
references/302模拟27/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf
references/302模拟27/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf
references/302模拟27/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf
references/302模拟27/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf
references/302模拟27/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf
references/302模拟27/往年模拟卷选填精选/数一答案/24合工大超越卷解析篇-数一.pdf
references/302模拟27/往年模拟卷选填精选/数一答案/24张宇四套卷答案-数一.pdf
references/302模拟27/往年模拟卷选填精选/数二答案/24合工大超越卷解析篇-数二.pdf
references/302模拟27/往年模拟卷选填精选/数二答案/24张宇四套卷答案-数二.pdf
references/302模拟27/往年模拟卷选填精选/数二答案/森哥五套卷数二.pdf


## tool · 2026-11-12T00:30:42Z


Script completed
Wall time 0.1 seconds
Output:

# 【A4紧凑】数二模拟卷选填精选

## 24 李林四套卷· 卷一

### 选择题

x2

1\. 设lim  
1  
xa  
0  
1+t4  
  
dt = b, 其中a 为大于零的常数, b 为非零常数, 则  
x→+∞  
A. a = 6,b = 1  
3 .  
B. a = 6,b = 3.  
C. a = 3,b = 6.  
D. a = 3,b = 1  
3 .  
1

2\. 设f t  
  
  
=  
0ln  
  
x2+t2dx, 则f t  
  
  
在t = 0 处  
A. 极限不存在.  
B. 极限存在但不连续.  
C. 连续但不可导.  
D. 可导.

3\. 设f x  
  
  
= xsinx + 1+a  
  
  
cosx, 则正确的是  
A. 当a < 1 时, f 0  
  
为极大值.  
B. 当a ≥1 时，f 0  
  
  
  
为极大值.  
C. 当a > 1 时, f 0  
  
  
为极小值.  
D. 当a = 1 时, f 0  
  
  
为极小值.  
上二阶可导, f x  


4\. 当f x  
  
  
在0,1  
  
  
  
\> 0, 且f 0  
  
  
= f 1  
  
  
.当x ∈0,1  
  
  
时, 下列选项中正确的是  
①1-x  
  
  
  
f x  
  
  
\- f 0  
  
  
  
< x f 1  
  
  
  
\- f x  
  
  
  
；  
②1-x  
  
  
  
f x  
  
  
\- f 0  
  
  
  
\> x f 1  
  
  
  
\- f x  
  
  
  
；  
③x f x  
  
\- f 0  
  
< 1-x  
  
f 1  
  
\- f x  
  
;  
④x f x  
  
\- f 0  
  
\> 1-x  
  
f 1  
  
\- f x  
  
.  
  
  
  
  
  
  
  
  
  
  
  

## 24 李林四套卷· 卷二

### 选择题

2

1\. 设f x  
  
  
,g x  
import hashlib
import json
import multiprocessing
import os
import re
import struct
import subprocess
import sys
import unicodedata
from collections import Counter
from pathlib import Path, PurePosixPath
from urllib.parse import quote
from zipfile import ZipFile

import fitz


ROOT = Path.cwd()
SOURCE = ROOT / "references/302模拟27"
DESTINATION = ROOT / "references/302模拟27md"
WORK = ROOT / ".question-bank-work"
CACHE = WORK / "302-ocr-cache"
ARCHIVE = WORK / "302-archive"
ANYDOC = next(WORK.glob("npm/_npx/*/node_modules/.bin/anydoc"))
OCR = None
PDF_TYPES = {".pdf"}
IMAGE_TYPES = {".png", ".jpg"}
OFFICE_TYPES = {".doc", ".docx", ".xlsx"}
TEXT_TYPES = PDF_TYPES | IMAGE_TYPES | OFFICE_TYPES | {".txt"}
FORMAT_HINT = "文字由原文提取或 OCR 识别。公式、图表和版式可通过原文件核对。"
TARGETS = ("李林", "张宇", "合工大", "超越", "武忠祥", "李艳芳", "合肥工业大学", "合肥工大")
COMBINED = {
    "24李林四套卷 数一 试题+答案.pdf": range(6, 26),
    "【题目+解析】李林四套卷数二清晰版答案(1).pdf": range(7, 27),
}


def is_target(title):
    return any(name in title for name in TARGETS)


def is_collection(relative):
    return (
        len(relative.parts) == 2
        and relative.parts[0].startswith(("往年模拟卷选填精选", "模拟卷10套", "模拟卷20套"))
    ) or (
        relative.parts[0].startswith("模拟卷40套")
        and "40套精选" in relative.name
    )


def selected_pages(document, source):
    name = source.name
    if name in COMBINED:
        return dict.fromkeys(COMBINED[name])


## tool · 2026-11-12T00:30:48Z




## tool · 2026-11-12T00:30:57Z


Script completed
Wall time 0.2 seconds
Output:

8
{
  "type": "input_image",
  "image_url": "images/491374c6ed505541092c07e2158ba334f7e1e98f1a139e7b8d840400bfc7e849.png",
  "detail": "high"
}
10
{
  "type": "input_image",
  "image_url": "images/7c6068872960347ea26dc5000105bafb9e4a952c1867f95ebdf148b5f5f45890.png",
  "detail": "high"
}
7
{
  "type": "input_image",
  "image_url": "images/08a248d3b533c71a4de5c5b2432d129ea169678ca089dc767ce827d2481848e9.png",
  "detail": "high"
}

## tool · 2026-11-12T00:32:06Z


Script completed
Wall time 0.2 seconds
Output:

{}
{"chunk_id":"e7bc95","wall_time_seconds":0.000008208,"exit_code":0,"original_token_count":47,"output":"147 math expressions rendered\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf.md\n"}
