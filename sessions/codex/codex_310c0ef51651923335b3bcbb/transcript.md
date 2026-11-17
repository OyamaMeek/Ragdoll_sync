# 01a1e6ee-0984-7723-b902-0187868a1edf

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/Ragdoll

## developer · 2026-11-17T00:35:29Z

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

## developer · 2026-11-17T00:35:29Z

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
- When you write or rewrite an automation prompt, keep it within 10,000 estimated tokens.
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
- `r15` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/app-6aa2c81fc7c48191a06e101858e41837/2.1.7/skills`
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/heygen/4.7.0/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.6/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1112.11217/skills`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.2/skills`
### Available skills
- imagegen: Ge (file: r2/imagegen/SKILL.md)
- openai-docs: API  (file: r2/openai-docs/SKILL.md)
- skill-creator: Crea (file: r2/skill-creator/SKILL.md)
- skill-installer: Inst (file: r2/skill-installer/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:database-access: Ex (file: r15/database-access/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:deploy-check: Veri (file: r15/deploy-check/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:incident-triage: Wo (file: r15/incident-triage/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:run-commands: Run  (file: r15/run-commands/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:server-health: An (file: r15/server-health/SKILL.md)
- apple-design: Ap (file: r1/apple-design/SKILL.md)
- apple-design: Ap (file: r0/apple-design/SKILL.md)
- archify: Crea (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: AR (file: r3/ars-codex/3.24.2/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: St (file: r0/benchmark-paper-template/SKILL.md)
- bio-research:instrument-data-to-allotrope: Conve (file: r4/instrument-data-to-allotrope/SKILL.md)
- bio-research:nextflow-development: Run n (file: r4/nextflow-development/SKILL.md)
- bio-research:scientific-problem-selection: This  (file: r4/scientific-problem-selection/SKILL.md)
- bio-research:scvi-tools: Deep  (file: r4/scvi-tools/SKILL.md)
- bio-research:single-cell-rna-qc: Perfo (file: r4/single-cell-rna-qc/SKILL.md)
- bio-research:start: Set (file: r4/start/SKILL.md)
- brandkit: Pr (file: r0/brandkit/SKILL.md)
- cli-anything: Us (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Di (file: r0/cli-hub-meta-skill/SKILL.md)
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
- design-taste-frontend: ta (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The  (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Ol (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diag (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Cr (file: r21/documents/26.1112.11217/skills/documents/SKILL.md)
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
- frontend-design: Guid (file: r0/frontend-design/SKILL.md)
- full-output-enforcement: Ove (file: r0/output-skill/SKILL.md)
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
- heygen:animated-short: Cr (file: r16/animated-short/SKILL.md)
- heygen:automated-content-creator: Plan (file: r16/automated-content-creator/SKILL.md)
- heygen:bedtime-story: Crea (file: r16/bedtime-story/SKILL.md)
- heygen:captions: Cr (file: r16/captions/SKILL.md)
- heygen:carousel: De (file: r16/carousel/SKILL.md)
- heygen:faceless-explainer: Cr (file: r16/faceless-explainer/SKILL.md)
- heygen:general-video: Catc (file: r16/general-video/SKILL.md)
- heygen:motion-graphics: Desi (file: r16/motion-graphics/SKILL.md)
- heygen:narrator: Cr (file: r16/narrator/SKILL.md)
- heygen:occasion-video: Cr (file: r16/occasion-video/SKILL.md)
- heygen:old-photo-revival: Brin (file: r16/old-photo-revival/SKILL.md)
- heygen:picture-video: Crea (file: r16/picture-video/SKILL.md)
- heygen:script-writer: Writ (file: r16/script-writer/SKILL.md)
- heygen:talking-head: Cr (file: r16/talking-head/SKILL.md)
- heygen:ugc-product: Crea (file: r16/ugc-product/SKILL.md)
- heygen:ugc-review: Cr (file: r16/ugc-review/SKILL.md)
- heygen:ugc-try-on: Cr (file: r16/ugc-try-on/SKILL.md)
- heygen:ugc-tutorial: Cr (file: r16/ugc-tutorial/SKILL.md)
- heygen:ugc-unboxing: Cr (file: r16/ugc-unboxing/SKILL.md)
- heygen:ugc-voiceless: Crea (file: r16/ugc-voiceless/SKILL.md)
- heygen:ugc-website: Crea (file: r16/ugc-website/SKILL.md)
- heygen:video-editing: Edit (file: r16/video-editing/SKILL.md)
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
- pdf:pdf: Re (file: r21/pdf/26.1112.11217/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Di (file: r17/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Qual (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: Li (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Sh (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Qu (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Qu (file: r23/ponytail-review/SKILL.md)
- pr: Us (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Re (file: r21/presentations/26.1112.11217/skills/presentations/SKILL.md)
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
- reverse-skill:reverse-skill-router: Use  (file: r24/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
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
- sales:rep-context: L (file: r14/rep-context/SKILL.md)
- sales:route-lead: Dec (file: r14/route-lead/SKILL.md)
- sales:schedule-meeting: Fin (file: r14/schedule-meeting/SKILL.md)
- sales:setup: F (file: r14/setup/SKILL.md)
- sales:stakeholder-map: M (file: r14/stakeholder-map/SKILL.md)
- sales:team-pipeline: L (file: r14/team-pipeline/SKILL.md)
- sales:update-opportunity: Gui (file: r14/update-opportunity/SKILL.md)
- sales:weekly-wrap: E (file: r14/weekly-wrap/SKILL.md)
- sales:win-loss-review: A (file: r14/win-loss-review/SKILL.md)
- security-audit: Se (file: r0/security-audit/SKILL.md)
- sepia:sepia: M (file: r25/sepia/SKILL.md)
- sepia:sepia-hemingway: U (file: r25/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use (file: r25/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use (file: r25/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use (file: r25/sepia-review/SKILL.md)
- sepia:sepia-write: U (file: r25/sepia-write/SKILL.md)
- shadcn: Ma (file: r0/shadcn/SKILL.md)
- sites:sites: U (file: r18/sites/SKILL.md)
- sites:sites-remix: R (file: r18/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use  (file: r22/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Cont (file: r22/excel-live-control/SKILL.md)
- stitch-design-taste: Sem (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You (file: r19/brainstorming/SKILL.md)
- superpowers:brainstorming: You (file: r26/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: U (file: r19/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: U (file: r26/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use (file: r19/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use (file: r26/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use (file: r19/executing-plans/SKILL.md)
- superpowers:executing-plans: Use (file: r26/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: U (file: r19/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: U (file: r26/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use (file: r19/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use (file: r26/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: U (file: r19/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: U (file: r26/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use (file: r19/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use (file: r26/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: U (file: r19/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: U (file: r26/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use (file: r19/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use (file: r26/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use (file: r19/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use (file: r26/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use (file: r19/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use (file: r26/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: U (file: r19/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: U (file: r26/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use (file: r19/writing-plans/SKILL.md)
- superpowers:writing-plans: Use (file: r26/writing-plans/SKILL.md)
- superpowers:writing-skills: U (file: r19/writing-skills/SKILL.md)
- superpowers:writing-skills: U (file: r26/writing-skills/SKILL.md)
- tdd: Test (file: r0/tdd/SKILL.md)
- teach: Socr (file: r0/teach/SKILL.md)
- tech-paper-template: Stru (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Cr (file: r21/template-creator/26.1112.11217/skills/template-creator/SKILL.md)
- vibe-research-workflow: Gu (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Crea (file: r17/visualize/1.0.103/skills/visualize/SKILL.md)
- wizard: Ge (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Cre (file: r20/create-pet/SKILL.md)
- work-pets:pets: Lis (file: r20/pets/SKILL.md)
- work-pets:update-pet: Ins (file: r20/update-pet/SKILL.md)
- writing-for-agents: Wr (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is enabled.
# Escalation Requests

Commands are run outside the sandbox if they are approved by the user, or match an existing rule that allows it to run unrestricted. The command string is split into independent command segments at shell control operators, including but not limited to:

- Pipes: |
- Logical operators: &&, ||
- Command separators: ;
- Subshell boundaries: (...), $(...)

Each resulting segment is evaluated independently for sandbox restrictions and approval requirements.

Example:

git pull | tee output.txt

This is treated as two command segments:

["git", "pull"]

["tee", "output.txt"]

Commands that use more advanced shell features like redirection (>, >>, <), substitutions ($(...), ...), environment variables (FOO=bar), or wildcard patterns (*, ?) will not be evaluated against rules, to limit the scope of what an approved rule allows.

## How to request escalation

IMPORTANT: To request approval to execute a command that will require escalated privileges:

- Provide the `sandbox_permissions` parameter with the value `"require_escalated"`
- Include a short question asking the user if they want to allow the action in `justification` parameter. e.g. "Do you want to download and install dependencies for this project?"
- Optionally suggest a `prefix_rule` - this will be shown to the user with an option to persist the rule approval for future sessions.

If you run a command that is important to solving the user's query, but it fails because of sandboxing or with a likely sandbox-related network error (for example DNS/host resolution, registry/index access, or dependency download failure), rerun the command with "require_escalated". ALWAYS proceed to use the `justification` parameter - do not message the user before requesting approval for the command.

## When to request escalation

While commands are running inside the sandbox, here are some scenarios that will require escalation outside the sandbox:

- You need to run a command that writes to a directory that requires it (e.g. running tests that write to /var)
- You need to run a GUI app (e.g., open/xdg-open/osascript) to open browsers or files.
- If you run a command that is important to solving the user's query, but it fails because of sandboxing or with a likely sandbox-related network error (for example DNS/host resolution, registry/index access, or dependency download failure), rerun the command with `require_escalated`. ALWAYS proceed to use the `sandbox_permissions` and `justification` parameters. do not message the user before requesting approval for the command.
- You are about to take a potentially destructive action such as an `rm` or `git reset` that the user did not explicitly ask for.
- Be judicious with escalating, but if completing the user's request requires it, you should do so - don't try and circumvent approvals by using other tools.

## prefix_rule guidance

When choosing a `prefix_rule`, request one that will allow you to fulfill similar requests from the user in the future without re-requesting escalation. It should be categorical and reasonably scoped to similar capabilities. You should rarely pass the entire command into `prefix_rule`.

### Banned prefix_rules 
Avoid requesting overly broad prefixes that the user would be ill-advised to approve. For example, do not request ["python3"], ["python", "-"], or other similar prefixes that would allow arbitrary scripting.
NEVER provide a prefix_rule argument for destructive commands like rm.
NEVER provide a prefix_rule if your command uses a heredoc or herestring. 

### Examples
Good examples of prefixes:
- ["npm", "run", "dev"]
- ["gh", "pr", "check"]
- ["cargo", "test"]


## Approved command prefixes
The following prefix rules have already been approved: - ["ego-browser"]

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy. If a rejection happens, you should proceed only with a materially safer alternative, or inform the user of the risk and send a final message to ask for approval.
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/16/01a1e510-ff5d-73e0-95ef-4cc2cc778b1b`, `/Volumes/SamsungSSD990PRO/GitHub/Ragdoll`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__codex_app: Manage the Codex desktop app: find, create, and update chats; organize projects, sidebar, and pinned items; schedule automations; manage worktrees; open app panels; and locate bundled libraries for documents, spreadsheets, slides, and PDFs.
- mcp__codex_apps__codex_document_control: Use Codex Document Control to find connected document sessions, inspect the tools supported by a selected session, and execute one supported tool against that session. Call `list_document_sessions` first to choose the intended connected session, c...
- mcp__codex_apps__github: Access repositories, issues, and pull requests. Required for some features such as Codex
- mcp__codex_apps__heygen: Create AI videos and avatars
- mcp__codex_apps__hotline: Look up local helpline information for the user based on country inferred from the conversation. You must use this tool before providing a suicide or self-harm helpline; do not use web search or guess.
- mcp__codex_apps__pets: Create and manage the user's animated companion pets inside ChatGPT Work mode. Use only for ChatGPT Pets, not real-world animal advice, generic pet images, or pets in other apps.
- mcp__codex_apps__plugin_creator: Use create_plugin to create a PRIVATE plugin in the authenticated user's active workspace, or a personal plugin without an active workspace. Update owned personal plugins, or inspect and edit eligible workspace plugins as their creator, an owner o...
- mcp__codex_apps__plugin_management: Manage plugins, settings, permissions, and connections. Prefer available built-in tools or connected plugins when they fit the task. Proactively search for plugins when an external app, account, or service would materially help, even if the user d...
- mcp__codex_apps__safety_settings: For ChatGPT Parental Controls (your child or teen's settings, features, Study Mode, quiet hours, family setup) and Trusted Contact (setup, status, privacy). Read account state first. Before updates, read the child's controls; prepare only can_upda...
- mcp__codex_apps__search_service: Tool for accessing the internet.
- mcp__codex_apps__sites: Use Sites to build or modify websites, including landing pages, portfolios, dashboards, portals, trackers, hubs, and internal tools. For repository-based sites, use Sites skills for local implementation, source preparation, and artifact packaging....
- mcp__codex_apps__termalin: Manage your servers from chat
- mcp__iphone_use: Drive a real iPhone. The loop:
- mcp__mobile_mcp: Drive a real or simulated iOS/Android device.
- mcp__node_repl: Use `js` for `node_repl` execution with persistent, redeclarable top-level bindings, `js_reset` to clear bindings, and `js_add_node_module_dir` to add package directories.
- mcp__ot
- mcp__pubmed
- mcp__rea: REA provides reverse-engineering tools for local artifacts, native binaries, managed code, browser pages, and runtimes. Use the tool that directly answers the question; discover targets or inspect inventory only when needed. Tool results include i...
</tools>
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

## developer · 2026-11-17T00:35:29Z

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

## developer · 2026-11-17T00:35:29Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-17T00:35:29Z

# AGENTS.md instructions for /Volumes/SamsungSSD990PRO/GitHub/Ragdoll

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
- 默认使用静态导入。仅在特定路径需要的重型模块可动态导入，尤其是对启动耗时敏感的入口。在最小使用范围顶部解构导入结果，保留分支内的惰性加载，避免在表达式内串接动态导入与取值。必要的 Python 库直接 `import`，不使用 `try-except` 包装导入。
- 不为假设中的未来需求增加灵活性、配置、接口或抽象。在满足完整需求与正确性的前提下，选择改动范围最小、清楚直接的实现。
- 无效状态应当在出错位置明确失败，不静默捕获错误或采用隐藏的 fallback。必要的输入校验、资源清理和防止数据丢失的错误处理必须保留。
- 发现重复状态、模式不一致、边界薄弱或只处理表面症状的修复时，指出根本问题。授权范围内的修复直接执行，额外的结构调整先说明范围并取得授权；范围外事项记入 `memory/progress.md`。
- 默认不添加注释。只有原因无法从代码直接看出时才添加简短注释，注释使用中文，技术术语保留英文。
- Python 文件开头不添加模块级 docstring 或 shebang，除非用户明确要求。

### TypeScript、Bun 与 Effect

- 在负责接收未知值的边界完成一次校验，向内部传递已确定类型的值。schema、构造函数和内部类型已经保证的条件可直接依赖。
- 简单逻辑和只使用一次的值可就地表达。辅助函数用于复用、封装复杂边界或明确命名独立概念。校验和准备步骤较多时，让主函数清楚呈现成功路径，相关辅助函数放在主函数附近。
- 优先使用 `const`、提前返回和简单条件表达式，减少重新赋值和 `else` 分支。需要保留对象语义时使用点号访问。优先使用 `flatMap`、`filter`、`map`，需要缩窄类型时给 `filter` 提供类型守卫。
- 优先使用类型推断，导出接口或提升可读性时显式标注类型，避免 `any`。使用具名导入，避免星号导入和类型位置的 `import("...")`。只有类型名称确实冲突且无法消解时才使用别名。需要命名空间时，引用模块具名导出的命名空间。
- 在 Bun 项目中优先使用 `Bun.file()` 等现有 API。新增配置模块时，沿用所在目录已有的文件顶部自导出写法，如 `export * as ConfigAgent from "./agent.js"`。
- 在 Effect 生成器中先取得服务并绑定到变量，再调用方法。同步解析、校验和选项构建保持同步。解析不受信任的 JSON 字符串时，优先使用 `Schema.UnknownFromJsonString` 和 `Schema.decodeUnknownOption`。可由已有机制处理的错误无需另加 `try/catch`。
- 涉及罕见竞态或安全边界且会扩大需求范围时，先说明具体失效场景、发生条件和实现成本，再取得用户对扩展范围的授权。当前需求所需的校验和错误处理直接完成。
- Drizzle schema 字段使用 `snake_case`，由字段名推导数据库列名。

### 软件包依赖与公开 API

- 采用 Schema、Core、Protocol、Server、Client 和 SDK 分包时，Core 与 Protocol 依赖 Schema，Server 依赖 Core 与 Protocol。Client 的运行时依赖限于 Schema 与 Protocol，由 SDK 组合 Client、Core 和 Server。
- 修改公开 Protocol 或 Server `HttpApi` 后，从客户端包运行项目的生成命令。客户端包为 `packages/client` 且提供 `generate` 脚本时，运行 `bun run generate`。生成文件由生成器更新。
- 采用实验 API 约定的项目，新增端点和新增默认行为先作为实验功能发布。实验端点使用 `/api/experimental/<group>/...`，OpenAPI 标识使用 `experimental.<group>.<method>`，SDK 路径使用 `client.experimental.<group>.<method>`。说明写明 `Experimental: may change without compatibility guarantees.`，在协议测试中双向验证路由与标识的对应关系。
- 稳定端点的实验字段或参数放在 `experimental.<name>`，配置使用 `config.experimental.*`。实验插件 hook 使用 `experimental.*`，如 `experimental.ws.handshake`。
- 实验端点转为正式端点时，移出 `/api/experimental`，删去标识的 `experimental.` 前缀并更新变更日志。实验 HTTP 路由改名或删除时直接更新调用方。
- 破坏性迁移已发布的 SDK 或插件 API 时保留旧路径和类型名称作为弃用别名，直至下一个次版本。用 `@deprecated` 说明替代项和 `Removed in the next minor`。SDK 生成器支持 `compile(..., { aliases: true })` 时，通过生成器创建别名。

### 特性开关

- 新增用户可见行为、风险较高的核心改动、跨多个 PR 或尚未达到发布条件的功能使用项目的既有特性开关机制。常规修复、重构、文档和测试无需加开关。
- 在项目的开关 schema 声明键和说明，通过现有读取接口检查开关。采用 `packages/schema/src/config/flag.ts` 和 `Flag.enabled("<key>")` 的项目沿用这两个入口。
- 有开发与正式发布区分时，开关在本地和开发构建中默认开启，在发布构建中默认关闭。用 `experimental.<key>` 和项目配置的开关环境变量覆盖默认值。采用列表语法时，`key,-other` 分别开启和关闭对应项。
- 采用批量开启机制时，通过项目约定的环境变量值 `all` 或配置 `experimental.all_flags: true` 测试全部开关。显式排除 `-<key>` 或设置 `experimental.<key>: false` 优先。保留 `all` 和 `all_flags` 作为控制值和配置键。功能正式发布时一道删除开关及其读取判断。

### 插件加载与会话执行

- 异步加载插件时，服务端处理器直接使用当前已加载的插件。冷启动时列表允许为空或不完整，缺少对应模型、提供方或 RPC 时返回未找到。查询和操作都遵循此规则，包括 `rpc.call` 和 `vcs.init`。可以等待已注册 hook 的执行结果，禁止等待或重试插件激活，也禁止因加载缓慢返回超时或 503。依赖权限策略的既有例外见下一条。
- 如果权限策略由最后激活的插件应用，只保留依赖该策略的既有等待点。现有例外包括 `model.list`、`model.default`、`provider.list`、`generate.*`、`voice.*` 和 `websearch.query` 在服务位置层通过 `awaitPlugins` 等待。插件批次能够原子可见后移除该例外。
- 长驻客户端订阅对应的 `*.updated` 事件刷新模型、代理、技能、集成及插件。一次性 CLI、ACP 或 SDK 客户端在发起请求前自行等待所需条目，可轮询 `plugin.list` 或该条目。
- 持久事件只记录按序重放不能推导出的新事实。需要自包含视图时，由投影和读模型提供历史或派生状态。
- 对现有会话收件箱，`Session.prompt(...)` 先发出 `session.inbox.enqueued`，由投影写入一条持久的 `session_inbox` 记录，再提出 `SessionExecution.wake(sessionID)` 唤醒请求。`resume: false` 仅入队。`session.inbox.delivered` 的投影在同一事务内消费队列记录并插入可见消息。收件箱只存未消费的工作。
- 重用 Session ID 时沿用已有会话。用户或合成条目 ID 在 Session 和类型相同时按首次入队处理，重试的载荷、元数据和投递模式均忽略。已投递时从投影消息识别重试。跨 Session 或跨类型重用应失败，控制条目沿用各自的冲突处理。
- `SessionExecution` 在进程内全局共享，并按 Session ID 协调。在开始处理队列时，通过 `SessionStore` 及 `LocationServiceMap.get(session.location)` 解析运行位置。依赖层不接收 Session ID。中断作用于当前进程内拥有该会话的执行链。已知但空闲或本进程未持有的会话无需处理，公开 API 拒绝未知会话。
- `SessionRunner`、模型解析、工具注册、权限和文件系统以 Location 为范围。缺省 `Location.workspaceID` 表示隐式本地运行，显式身份留给后续位置语义。
- 每个步骤调用一次 `llm.stream`，从重新加载的历史继续。步骤的持久记录只覆盖模型可见范围，工具执行由后续步骤继续，避免在内存中增加工具循环。单次调用称为步骤，`turn` 留给从提示晋升到会话即将空闲的完整助手轮次。
- 集群执行实现前，在进程内处理会话队列。`SessionRunCoordinator` 合并同 Session 的显式继续请求与提示唤醒，允许不同 Session 并行。先写入执行恢复标记，完成、失败或用户中断时释放。关闭中断或进程终止时保留，启动后按执行恢复并持久记录尝试次数。运行中的子代理 Job 负责其子会话恢复。事件重放的所有权与集群会话执行的所有权各自管理，执行恢复标记仅承担本地恢复职责。
- 提示默认按 `steer` 投递。在安全步骤边界，`steer` 压缩在第一个 `steer` 移动控制前优先，其余 `steer` 保持入队顺序。在空闲边界优先处理 `steer`。没有 `steer` 时，每投递一个 `queue` 条目就重新判断是否继续。投递前可取消条目，或在 `queue` 与 `steer` 间切换。新用户输入晋升时重置所选代理的步骤额度，同一批 `steer` 只重置一次。

### TUI 主题

- 按用途选择主题 token。`text.feedback` 和 `background.feedback` 用于错误、警告、成功和提示等反馈。`formfield` 状态用于控件文字、序号和选择标记，`action` 状态用于操作。
- 需要新角色时，先扩展主题 schema、默认值、解析和类型，再用于组件。避免从其他角色借 token 或直接使用 `theme.hue`。变更公开 token 时，验证受影响组件、内置浅色与深色默认主题以及自定义主题的回退路径。

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
- 使用测试套件、独立审查者或用户提供的证据验证行为，不能仅凭自己的判断宣称正确。使用其他代理时，遵守当前环境的授权规则。
- 用户要求测试产出时，按照新用户实际使用的路径验证，不能只检查代码。
- 同一个修复连续失败两次时，停止重复尝试，重新从入口读取相关代码，确定错误假设后再调整实现；不向用户重复已经解释清楚的错误。

### 软件包测试与检查

- 测试调用真实实现，避免在测试中复制生产逻辑。只有缺少替代方案时才修改 `globalThis` 状态。仓库有 `do-not-run-tests-from-root` 守卫时，从相应软件包目录运行测试。
- 编写或修改测试前，读取项目技能目录中匹配的说明。按需查找 `unit-tests`、`tui-tests`、`app-e2e-tests` 或 `component-tests`，分别对应 Bun 单元测试、TUI 渲染测试、应用端到端测试和基于 story 的组件测试。
- Bun 工作区提供完整 `check` 脚本时，从仓库根目录运行 `bun run check`。局部迭代时，从受影响软件包运行其 `bun typecheck`。使用项目脚本调用编译器。
- 项目本地使用 `bun check`，而 CI 和发布使用 `typecheck:tsc` 时，如果两者结果不同，从软件包目录运行 `bun run typecheck:tsc`，以项目锁定的官方 TypeScript 编译器结果为准。向 Bun 上游报告差异时，附无依赖的最小复现和两份检查输出。`bun check` 不生成声明文件，只有官方编译器报告的声明生成错误如 TS5088 或 TS2883 无需作为差异上报。

### TUI 与桌面运行验证

- 提供 `dev:live` 脚本的项目，从开发 worktree 运行 `bun run dev:live`，复用当前后台服务与真实会话。需要指定项目目录时，将目录作为脚本参数。由脚本通过 CLI 的 `service status` 和 `service get password` 子命令发现服务并注入本地凭据，使用 `dev` 存储通道保持标签页和客户端状态一致。
- 连接现有后台服务时优先使用 `dev:live`。`bun run dev` 隐式连接受管理服务时可能因客户端版本不同而更换服务。需要手动连接时使用项目支持的 `--server`，保留现有服务并处理版本警告。
- 用户要求 TUI story 时，在项目 storybook 中增加由 fixture 驱动的 story 并注册到索引。沿用 `packages/tui/src/feature-plugins/system/storybook/index.tsx` 的项目在该位置注册。渲染真实组件，将提交与其他副作用限制在 story 内。给重要状态提供快捷键并在 `StoryFooter` 中列出，有需要时提供重置。按脚本定义的 story ID 环境变量选择对应场景，从开发 worktree 运行 `bun run dev:live`。按布局需求验证窄屏和宽屏。
- 用 Playwright 连接正在运行的桌面应用时，使用 `chromium.connectOverCDP(endpoint, { noDefaults: true })`，保留焦点、系统主题及媒体偏好，避免默认浅色模拟导致窗口闪烁。颜色和动态效果偏好的模拟使用隔离测试上下文。用户明确要求时可在其当前窗口模拟。

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
- 提交说明和 PR 标题使用 Conventional Commits 格式 `type(scope): summary`，范围可省略。类型使用 `feat`、`fix`、`docs`、`chore`、`refactor` 或 `test`，范围可用受影响的软件包或模块名。
- 默认分支基准与 PR 目标以目标仓库为准。仓库约定使用 `dev` 集成时，从 `origin/dev` 建分支和 worktree，以 `origin/dev` 为比较基准，PR 指向 `dev`。分支名在用户、宿主和仓库要求之外默认最多三个以连字符分隔的词，如 `session-recovery`，省略类型前缀。
- 发布沿用仓库已有流程。未采用 Changesets 的仓库禁止新增 `.changeset`。有特性开关的改动在 PR 正文中写明对应开关。
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
  <cwd>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll</cwd>
  <shell>zsh</shell>
  <current_date>2026-11-17</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/16/01a1e510-ff5d-73e0-95ef-4cc2cc778b1b</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-17T00:35:30Z

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


## developer · 2026-11-17T00:35:30Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
</tools>

## assistant · 2026-11-17T00:35:34Z

我会用 code-review 技能只读核对设计、实现和现有验证记录，重点追踪迁移写入、归档锁和推送重试的失败路径。

## tool · 2026-11-17T00:35:38Z


Script completed
Wall time 0.1 seconds
Output:

[{"status":"fulfilled","value":["guide","---\nname: code-review\ndescription: \"Review the changes since a fixed point (commit, branch, tag, or merge-base) along two axes: Standards (does the code follow this repo's documented coding standards?) and Spec (does the code match what the originating issue/spec asked for?). Runs both reviews in parallel sub-agents and reports them side by side. Use when the user wants to review a branch, a PR, work-in-progress changes, or asks to \\\"review since X\\\".\"\n---\n\nTwo-axis review of the diff between `HEAD` and a fixed point the user supplies:\n\n- **Standards**: does the code conform to this repo's documented coding standards?\n- **Spec**: does the code faithfully implement the originating issue / spec?\n\nBoth axes run as **parallel sub-agents** so they don't pollute each other's context, then this skill aggregates their findings.\n\nThe issue tracker should have been provided to you. If not, tell the user to run `/setup-matt-pocock-skills`.\n\n## Process\n\n### 1. Pin the fixed point\n\nWhatever the user said is the fixed point (a commit SHA, branch name, tag, `main`, `HEAD~5`, etc.). If they didn't specify one, ask for it.\n\nCapture the diff command once: `git diff <fixed-point>...HEAD` (three-dot, so the comparison is against the merge-base). Also note the list of commits via `git log <fixed-point>..HEAD --oneline`.\n\nBefore going further, confirm the fixed point resolves (`git rev-parse <fixed-point>`) and the diff is non-empty. A bad ref or empty diff should fail here, not inside two parallel sub-agents.\n\n### 2. Identify the spec source\n\nLook for the originating spec, in this order:\n\n1. Issue references in the commit messages (`#123`, `Closes #45`, GitLab `!67`, etc.), fetched via the workflow in the tracker doc.\n2. A path the user passed as an argument.\n3. A spec file under `docs/`, `specs/`, or `.scratch/` matching the branch name or feature.\n4. If nothing is found, ask the user where the spec is. If they say there isn't one, the **Spec** sub-agent will skip and report \"no spec available\".\n\n### 3. Identify the standards sources\n\nSearch the repo for every file that documents how code should be written. When `CODING_STANDARDS.md` or `CONTRIBUTING.md` exists, it must be on the list.\n\nOn top of whatever the repo documents, the Standards axis always carries the **smell baseline** below: a fixed set of Fowler code smells (_Refactoring_, ch.3) that applies even when a repo documents nothing. Two rules bind it:\n\n- **The repo overrides.** A documented repo standard always wins; where it endorses something the baseline would flag, suppress the smell.\n- **Always a judgement call.** Each smell is a labelled heuristic (\"possible Feature Envy\"), never a hard violation. Like any standard here, skip anything tooling already enforces.\n\nEach smell reads *what it is* → *how to fix*; match it against the diff:\n\n- **Mysterious Name**: a function, variable, or type whose name doesn't reveal what it does or holds. → rename it; if no honest name comes, the design's murky.\n- **Duplicated Code**: the same logic shape appears in more than one hunk or file in the change. → extract the shared shape, call it from both.\n- **Feature Envy**: a method that reaches into another object's data more than its own. → move the method onto the data it envies.\n- **Data Clumps**: the same few fields or params keep travelling together (a type wanting to be born). → bundle them into one type, pass that.\n- **Primitive Obsession**: a primitive or string standing in for a domain concept that deserves its own type. → give the concept its own small type.\n- **Repeated Switches**: the same `switch`/`if`-cascade on the same type recurs across the change. → replace with polymorphism, or one map both sites share.\n- **Shotgun Surgery**: one logical change forces scattered edits across many files in the diff. → gather what changes together into one module.\n- **Divergent Change**: one file or module is edited for several unrelated reasons. → split so each module changes for one reason.\n- **Speculative Generality**: abstraction, parameters, or hooks added for needs the spec doesn't have. → delete it; inline back until a real need shows.\n- **Message Chains**: long `a.b().c().d()` navigation the caller shouldn't depend on. → hide the walk behind one method on the first object.\n- **Middle Man**: a class or function that mostly just delegates onward. → cut it, call the real target direct.\n- **Refused Bequest**: a subclass or implementer that ignores or overrides most of what it inherits. → drop the inheritance, use composition.\n\n### 4. Spawn both sub-agents in parallel\n\nIssue both sub-agent calls together, in the foreground, and aggregate the reports they return.\n\n**Standards sub-agent prompt** should include:\n\n- The full diff command and commit list.\n- The list of standards-source files you found in step 3, **plus the smell baseline from step 3** pasted in full (the sub-agent has no other access to it).\n- The brief: \"Report, per file/hunk where relevant, (a) every place the diff violates a documented standard: cite the standard (file + the rule); and (b) any baseline smell you spot: name it and quote the hunk. Distinguish hard violations from judgement calls: documented-standard breaches can be hard, but baseline smells are always judgement calls, and a documented repo standard overrides the baseline. Skip anything tooling enforces. Under 400 words.\"\n\n**Spec sub-agent prompt** should include:\n\n- The diff command and commit list.\n- The path or fetched contents of the spec.\n- The brief: \"Report: (a) requirements the spec asked for that are missing or partial; (b) behaviour in the diff that wasn't asked for (scope creep); (c) requirements that look implemented but where the implementation looks wrong. Quote the spec line for each finding. Under 400 words.\"\n\nIf the spec is missing, skip the Spec sub-agent and note this in the final report.\n\n### 5. Aggregate\n\nPresent the two reports under `## Standards` and `## Spec` headings, verbatim or lightly cleaned. Do **not** merge or rerank findings, because the two axes are deliberately separate (see _Why two axes_).\n\nEnd with a one-line summary: total findings per axis, and the worst issue _within each axis_ (if any). Don't pick a single winner across axes: that's the reranking the separation exists to prevent.\n\n## Why two axes\n\nA change can pass one axis and fail the other:\n\n- Code that follows every standard but implements the wrong thing → **Standards pass, Spec fail.**\n- Code that does exactly what the issue asked but breaks the project's conventions → **Spec pass, Standards fail.**\n\nReporting them separately stops one axis from masking the other.\n"]},{"status":"fulfilled","value":["spec","# 第一版新增范围设计\n\n状态：需求已确认，用户“继续”授权实施；产品代码及验证进行中，实际结果见 `memory/progress.md`。\n\n## 已确认目标\n\n- 三项全部纳入第一版：跨工具原生历史迁移、远端归档自动推送、独立后台常驻服务。\n- 迁移结果必须成为目标工具的原生历史，能在目标工具直接打开完整旧会话。\n- 目标工具无法原生表示的推理或工具记录，用户允许将完整内容转成带来源标记的历史文本；其他消息仍按目标原生格式保存。\n- 远端同步采用自动 Git 推送；失败保留本地归档并支持重试。\n- 保留 SwiftUI、三种原生接入、ACP 与 Registry、现有统计和归档保护。\n- 沿用此前限制：不再运行 Claude 测试；不执行截图和视觉检查。相应未验证能力必须如实记录。\n\n## 现有实现与影响\n\n- `runtime/src/logs.ts` 读取原始日志并生成用于浏览和统计的 `Session`。部分结构化内容已转为文字，Codex 推理等记录未进入消息列表，因此不能直接将索引当作完整迁移源。\n- `runtime/src/agents.ts` 支持原工具恢复，明确拒绝跨原生工具恢复；迁移需单独入口，保留现有恢复规则。\n- `Archive.save` 保护原始日志目录、手工修改及外部暂存，只创建本地提交。\n- `AppModel` 当前拥有扫描、归档调度及子进程；应用退出会停止这些任务。\n- 修改将涉及模型和持久化、运行时读取及写入、界面入口、归档和后台协调、打包、测试及文档。\n\n## 实现方式与取舍\n\n迁移使用目标原生格式写入器；这是满足用户已选“目标工具直接打开完整旧会话”的实现方式。原始记录负责保真，现有索引用于选择会话及展示结果。\n\n同步扩展现有 Git 归档，提交成功后普通推送到用户指定远端和分支，符合用户已选的单向推送行为。\n\n后台建议增加独立 Swift 可执行程序，由用户级 LaunchAgent 托管，通过 `SMAppService` 注册。它复用核心库和 TypeScript 扫描助手，避免引入另一个归档实现。无需管理员权限；运行范围为当前用户登录期间。此方案及下面的具体实现选择为代理建议，尚未视作用户已批准。\n\n## 跨工具原生历史迁移\n\n### 范围与行为\n\n- 首版原生目标为 Codex、Claude Code、dsh，覆盖三者之间的六个方向；来源选择沿用应用中可浏览的会话。ACP 和 Claude 普通聊天可作为来源，目标能力以实际取得的原始记录为准。通用 ACP 协议没有统一的原生历史格式，不把任意 ACP Agent 列作原生迁移目标。\n- 用户选择原会话、目标工具实例和目标项目目录，先显示兼容性检查，再执行迁移。\n- 为目标生成新的原生会话 ID，在目标工具自己的会话目录及必要目录索引注册；绝不覆盖同名文件，不修改或删除源会话。\n- 保存来源关联、迁移版本和操作结果；迁移完成后允许打开或恢复目标会话。重复扫描不能丢失关联。\n- 保留历史顺序、角色、正文及时间；逐类处理工具请求与结果、推理记录、压缩记录、分支关系及附件。需要复制的附件使用独立目标路径，不依赖源文件继续存在。\n- 从真实原始记录解析这些内容，不能通过当前 `Session.messages` 重建并宣称完整。为没有原始文件的导入记录保留其实际已有内容，明确缺失范围。\n- 普通消息写为目标原生消息；目标无法原生表示的推理、工具及其他专属记录，完整转换为带来源及记录类型标记的历史文本，在目标工具的历史中可见。保留源记录及转换清单以供核对，不丢弃、不截断、不以单条上下文提示代替整段历史。格式适配先核实安装版本和实际读取流程。\n- “完整”按内容保留验收：每条原始记录均有原生表示或完整历史文本，附件已复制或明确因源缺失而阻止迁移。跨工具专属执行状态不承诺继续运行；已转换的工具记录只供阅读，不重新执行。\n- 原始用量保留在迁移元数据中，历史消费仍归属源会话，目标续聊产生的新增消费正常计入，避免统计翻倍。\n\n### 写入与失败处理\n\n- 先在项目或应用受管理目录准备产物并验证，再以不覆盖方式发布到目标会话目录；多文件注册记录操作进度，以便失败后明确识别已发布的文件并安全重试。\n- 不以调用模型生成回复作为迁移步骤，不重放工具调用，不自动执行历史中的指令。\n- 校验源文件稳定性、目标路径、会话 ID、目标格式版本及附件存在性。源正在变化或目标不可写时明确失败。\n- 迁移操作的写入权限只涉及新建目标历史及该工具必需的注册信息，不扩展到修改既有源日志。\n\n## 远端归档自动推送\n\n- 设置中显式开启，选择专用归档仓库、现有 Git 远端及目标分支；在启用时展示实际推送地址和分支。认证复用系统 Git 的 SSH 或凭据管理器，凭据不写入设置或归档。\n- 先完成本地保存及提交，再执行明确远端和分支的普通 `git push`。推送上传该分支的历史，不能只把本次受管理文件视为上传范围；启用前核对专用仓库的已跟踪内容并提示其实际范围。\n- 推送状态与本地归档状态独立：本地成功、推送待重试、本次推送成功分别显示。\n- 持久记录待推送状态；服务启动及后续调度重新检查，即使没有新文件或新提交也能重试。提供立即重试入口。\n- 超时或网络、认证失败时保留本地提交，延迟重试；非快进拒绝时明确报告需要处理远端分歧，不强制推送，不自动拉取或合并。\n- Git 非交互执行，有有限超时并清理进程。错误和状态不显示含凭据的 URL；配置变化后重新检查当前目标，不能沿用旧目标的成功状态。\n- 不添加云存储提供方、多设备双向同步或冲突合并。\n\n## 独立后台常驻服务\n\n- 新增 `RagdollService` Swift 可执行程序并放入应用包；用户级 LaunchAgent 由 `SMAppService` 管理，应用设置显示启用、停用及系统授权状态。\n- 服务负责自动扫描、索引更新、30 秒防抖/最长 5 分钟归档和推送重试。关闭应用窗口及退出应用后继续运行；注销或关机后停止，下次登录恢复。\n- GUI 保留交互对话、认证和权限请求；后台不运行无人处理的交互聊天，也不自动批准工具权限。\n- 将现有调度提取到核心层复用。后台启用后 GUI 通过本机通信请求刷新和立即归档、读取状态，避免两个调度器同时归档。未启用后台时沿用应用内调度。\n- 建议采用仅当前用户可访问的 Unix socket 和现有 NDJSON 消息结构，命令限制为状态、刷新、归档及重新加载设置；不开放 TCP 端口。校验消息大小和参数，限制 socket 及状态文件权限。\n- 同一数据目录只允许一个归档所有者，使用操作系统进程锁，服务异常退出后可恢复。服务启停或失联时先确认所有权再转交，避免重复扫描、Git 锁冲突及静默双写。\n- GUI 和服务共享索引时明确设置数据库锁等待，并验证并发读取和保存；配置变更通过持久设置和重新加载生效。\n- 服务启动、停止、崩溃重启、待推送恢复都要能观察；状态带时间和进程信息，不能把陈旧状态显示为正在运行。\n- 构建脚本打包 helper、LaunchAgent plist 和助手资源；验证签名及实际注册。保持现有 Apple Silicon/macOS 15 最低要求。\n\n## 验收与实施次序\n\n1. 核实三种工具实际格式、原生列表注册和恢复入口，形成迁移兼容性矩阵；每个方向至少覆盖多轮普通对话、推理/工具记录转为全文历史、附件和压缩记录，不以仅提供入口作为完成标准。不运行 Claude 测试，相关四个方向标为“代码实现，未验证”，在产品迁移入口和结果中明确显示。先为允许测试的范围用真实样本建立暴露问题的测试，再写转换器。\n2. 完成原生迁移、来源关联和统计去重；Codex/dsh 从目标工具列出、打开、恢复及继续对话进行实际验证。完整性用独立于写入器的读取与原始记录比较。\n3. 用真实本地 bare Git 远端验证自动推送、无新提交重试、远端缺失、非快进拒绝、进程超时及失败保留数据，再接入设置和状态。\n4. 完成独立服务、单一调度所有权、数据库并发和启停；验证 GUI 退出后新日志仍被索引并推送、重启不重复提交以及禁用服务后的应用内工作流。\n5. TypeScript 类型检查、相关 Node 测试、Swift 测试及 release 打包；更新 README、验证记录和 CHANGELOG，按逻辑单元提交并普通推送。\n\n## 已知限制与待审阅事项\n\n- 目标工具的原生格式兼容性需要逐项核实；不支持的专属结构按用户授权保留为全文历史。源记录损坏、附件缺失或目标不接受生成历史时阻止迁移，说明具体原因。\n- 此前“不再运行 Claude 测试”的限制仍然有效；涉及 Claude 的四个方向在产品中显示未验证状态，不能宣称经过完整转换、原生打开和续聊实测。\n- 当前应用采用本地临时签名，后台注册与恢复需在实际打包产物验证；系统可能要求用户在“登录项”中允许后台运行。\n- 自动推送会把选定归档分支的对话内容及历史上传到选定远端；由用户在产品设置中配置并开启。\n\n## 实现依据\n\n- [Apple SMAppService](https://developer.apple.com/documentation/servicemanagement/smappservice)：管理应用 helper 的注册和状态。\n- [Apple helper 打包约定](https://developer.apple.com/documentation/servicemanagement/updating-helper-executables-from-earlier-versions-of-macos)：应用包内 LaunchAgent 及 helper 结构。\n- [Git push](https://git-scm.com/docs/git-push)：显式 refspec、普通推送和非快进拒绝语义。\n"]},{"status":"fulfilled","value":["plan","# 第一版新增功能实施计划\n\n> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.\n\n**Goal:** 实现跨工具原生历史迁移、归档普通推送与重试、退出 GUI 后继续工作的用户级后台服务。\n\n**Architecture:** 迁移由 TypeScript 读取完整原始记录并发布目标原生历史。Swift 核心层复用归档并增加推送和进程所有权；独立 Swift helper 运行扫描/归档循环，GUI 保留交互对话。\n\n**Tech Stack:** Swift 6.1、SwiftUI、GRDB、ServiceManagement、Node 26、TypeScript、Git。\n\n**Spec:** `docs/superpowers/specs/2026-11-16-v1-expansion-design.md`\n\n## Global Constraints\n\n- macOS 15+、Apple Silicon，中文，保留现有原生接入及 ACP。\n- 不再运行 Claude 测试；不执行截图和视觉检查。\n- 不覆盖目标历史，不修改或删除源记录；不兼容记录按用户授权转为全文历史文本。\n- 不强制推送，不自动拉取或合并；失败保留本地提交。\n- 保留工作区已有扫描修复及其测试，不纳入本任务提交。\n- 用户“继续”授权本会话直接完成实施，不重复询问相同授权。\n\n## Review Focus\n\n- 多文件或压缩源、未知记录和附件不得在迁移时丢失；Task 1 验证未知块全文和源文件不变。\n- 源会话在迁移时变化或目标冲突必须保留原数据；Task 1 验证拒绝覆盖和损坏输入。\n- 没有新提交也应重试失败的推送；Task 2 验证 bare 远端重试及非快进拒绝。\n- GUI 与后台竞争及服务异常退出不能同时归档；Task 3 验证进程锁释放、独立进程和请求恢复。\n- 旧设置与迁移来源关联必须跨重启/扫描保留；Task 2/4 验证旧设置解码、来源元数据及用量不重复。\n\n### Task 1: 原生历史迁移与运行时入口\n\n**Files:** 新建 `runtime/src/migration.ts`、`runtime/test/migration.test.ts`；修改 `runtime/src/main.ts`、`runtime/src/types.ts`、`runtime/src/logs.ts`。\n\n**Interfaces:** `migrateSession(value: unknown): Promise<Session>` 接收源 Session、目标 AgentConfig、目标 home 和 cwd；发布新会话及迁移来源清单，返回可供现有 `chat.start` 恢复的 Session。`migration` 可选元数据保留原 ID 和历史消费。\n\n- [ ] 先写真实文件测试：多轮消息、工具/推理全文、压缩记录、附件、目标不覆盖、损坏源拒绝；不执行 Claude 来源或目标测试。\n- [ ] Run: `node --test test/migration.test.ts`（runtime 目录）。Expected: 新接口不存在导致失败。\n- [ ] 核实安装工具的原生格式和目录注册；实现 Node 标准 JSON/JSONL/zstd 读取、逐记录保留、非覆盖发布和来源清单。Codex/dsh 使用真实工具读取检查格式。\n- [ ] 运行目标测试和 `npm run typecheck`。Expected: 通过。\n- [ ] 提交该逻辑单元并普通推送。\n\n### Task 2: 归档推送、失败保留与旧设置\n\n**Files:** 新建 `Sources/RagdollCore/ArchiveSync.swift`、`Tests/RagdollCoreTests/ArchiveSyncTests.swift`；修改 `Models.swift`、`Store.swift`。\n\n**Interfaces:** `ArchiveSync.push(root: URL, remote: String, branch: String) throws -> String` 执行指定目标的有限时普通推送。设置增加可选同步配置以兼容旧记录。来源元数据由 Store 保留，迁入的旧消费不重新计费。\n\n- [ ] 写真实 bare 仓库测试：失败后无需新提交成功重试、明确分支、非快进拒绝及本地 HEAD 不变；旧设置解码不失败。\n- [ ] Run: `swift test --filter ArchiveSync`（项目缓存参数沿用现有脚本）。Expected: 新接口缺失导致失败。\n- [ ] 实现 Git 参数校验、无交互认证、超时清理、错误脱敏；在保存会话时保留 migration 元数据。\n- [ ] 运行 Swift 相关测试。Expected: 推送目标 HEAD 与本地匹配，拒绝时数据不变。\n- [ ] 提交并普通推送。\n\n### Task 3: 独立扫描归档服务与打包\n\n**Files:** 新建 `Sources/RagdollCore/BackgroundService.swift`、`Sources/RagdollService/ServiceMain.swift`、`packaging/com.oyamameek.ragdoll.service.plist`、服务测试；修改 `Package.swift`、`scripts/build.sh`。\n\n**Interfaces:** 核心层提供服务状态、原子刷新/归档请求和数据目录进程锁；helper 接受 `--data-dir`、`--once`，复用 RuntimeBridge、Store、Archive 和 ArchiveSync。服务状态包含 heartbeat、PID、本地归档及推送结果。\n\n- [ ] 写真实锁和独立进程测试，验证重复服务拒绝、进程终止释放锁、GUI 外扫描/归档和推送失败保留。\n- [ ] Run: 相关 Swift 测试。Expected: 新接口缺失导致失败。\n- [ ] 实现用户级服务、单一归档所有者、设置重载、持久脏标记与推送重试；沿用 30 秒/最长 5 分钟归档调度。\n- [ ] helper 的刷新/归档请求采用受管理文件的原子写入与有限命令，状态由 GUI 轮询；这是实现阶段对设计“建议 Unix socket”的简化，消除通用 IPC 服务而保持同一行为。\n- [ ] 打包 helper 与 LaunchAgent，运行独立进程验证。Expected: GUI 不运行时索引/归档仍更新，无重复提交。\n- [ ] 提交并普通推送。\n\n### Task 4: GUI 入口与工作流\n\n**Files:** 新建 `Sources/Ragdoll/MigrationView.swift`；修改 `AppModel.swift`、`ConversationView.swift`、`SettingsView.swift`、`RagdollApp.swift`。\n\n**Interfaces:** `AppModel.migrateSelected(agent:cwd:)` 调运行时迁移；后台启用时扫描/归档请求交给服务，GUI 仅重载索引和显示状态，未启用时保留原路径。\n\n- [ ] 复用前述回归证明迁移、旧设置及服务所有权；无需为简单 SwiftUI 绑定添加实现镜像测试。\n- [ ] 添加迁移预览、目标工具/项目选择、兼容记录说明和 Claude 未验证标记；设置添加推送目标、重试与服务启停/系统授权状态。\n- [ ] 后台通过 SMAppService 注册，失败如实报告；系统未允许时保留手动应用内使用路径。配置变化和交互聊天保存发出刷新请求。\n- [ ] Run: Swift 构建及相关测试。Expected: 编译通过，服务与 GUI 不重复归档。\n- [ ] 提交并普通推送。\n\n### Task 5: 完整检查与交付\n\n**Files:** `README.md`、`docs/VALIDATION.md`、`docs/CHANGELOG.md`、`memory/`。\n\n**Interfaces:** 使用上述真实入口，无替代实现或虚假成功。\n\n- [ ] 运行 TypeScript 类型检查及允许的 Node 测试；不运行 Claude 测试。\n- [ ] 运行 Swift 核心测试和 release 打包，检查签名及 helper。\n- [ ] 真实 Codex/dsh 目标列出/恢复/续聊检查；实际 LaunchAgent 注册条件允许时验证，受系统授权限制时记录准确原因。\n- [ ] 按完整变更进行独立只读代码审阅，修正有效问题。\n- [ ] 文档记录实际结果和限制，精确暂存本任务内容，提交并普通推送。\n"]},{"status":"fulfilled","value":["state","# SDD ledger — plan: docs/superpowers/plans/2026-11-17-v1-expansion.md\n\n- Spec: docs/superpowers/specs/2026-11-16-v1-expansion-design.md，用户“继续”授权完成实施。\n- Pre-flight: Task 1 返回的 Session 由 Task 4 使用；Task 2 的推送由 Task 3 调度，Task 3 的所有权由 Task 4 检查，名称与类型保持一致。\n- Ruling: 在当前仓库实施且仅精确暂存本任务内容 — 项目明确授权向当前已配置分支提交推送，另一会话的扫描修复保持原样 — 需逐次核对共享文件与 Git 暂存内容。\n- Ruling: 用原子请求文件和状态文件替代建议的 Unix socket — 仅需扫描/归档触发及状态，文件通信不增加通用服务或端口 — 最多增加两秒状态延迟。\n- Task 1: in progress，先核实格式并建立真实文件测试。\n- Task 1: Codex/dsh 目标已通过真实原生恢复和续聊保留校验码；附件与路径边界测试已 RED→GREEN。\n- Ruling: dsh 采用当前发布的 v4 zstd 原生格式并由目标工具恢复验证 — 读取实际实现确认首帧独立头记录、完整 turn/step 生命周期及嵌入流校验 — 自定义不兼容存储配置会明确失败，不冒称迁移成功。\n- Task 2: 4 项真实 Git/设置测试通过，包括有限时推送、预览脱敏、失败后无新提交重试和非快进保护。\n- Task 3: helper 编译、独立进程扫描归档与进程锁测试通过；持续运行和跨重启重试待补。\n- Task 4: GUI 迁移、目标预览、推送及后台设置已编译；修正前台自身持锁时被误判为后台的调度路径。\n"]},{"status":"fulfilled","value":["stat","## main...origin/main\n M Package.swift\n M Sources/Ragdoll/AppModel.swift\n M Sources/Ragdoll/ConversationView.swift\n M Sources/Ragdoll/SettingsView.swift\n M Sources/RagdollCore/Archive.swift\n M Sources/RagdollCore/Models.swift\n M Sources/RagdollCore/Store.swift\n M docs/superpowers/specs/2026-11-16-v1-expansion-design.md\n M memory/agents.md\n M memory/gotchas.md\n M memory/plan.md\n M memory/progress.md\n M scripts/build.sh\n?? Sources/Ragdoll/MigrationView.swift\n?? Sources/RagdollCore/ArchiveSync.swift\n?? Sources/RagdollCore/BackgroundService.swift\n?? Sources/RagdollService/\n?? Tests/RagdollCoreTests/ArchiveSyncTests.swift\n?? Tests/RagdollCoreTests/BackgroundServiceTests.swift\n?? docs/superpowers/plans/\n?? packaging/com.oyamameek.ragdoll.service.plist\n"]},{"status":"fulfilled","value":["diff"," Package.swift                                      |   3 +-\n Sources/Ragdoll/AppModel.swift                     |  83 ++++++++-\n Sources/Ragdoll/ConversationView.swift             |   3 +\n Sources/Ragdoll/SettingsView.swift                 |  45 ++++-\n Sources/RagdollCore/Archive.swift                  |   2 +\n Sources/RagdollCore/Models.swift                   |  19 ++\n Sources/RagdollCore/Store.swift                    |   5 +-\n docs/CHANGELOG.md                                  |  15 ++\n .../specs/2026-11-16-v1-expansion-design.md        |   2 +-\n memory/agents.md                                   |   2 +-\n memory/gotchas.md                                  |   1 +\n memory/plan.md                                     |   4 +-\n memory/progress.md                                 |  14 +-\n runtime/src/agents.ts                              |   6 +-\n runtime/src/logs.ts                                |  18 +-\n runtime/src/main.ts                                |   2 +\n runtime/src/migration.ts                           | 194 +++++++++++++++++++++\n runtime/src/types.ts                               |   1 +\n runtime/test/migration.test.ts                     | 122 +++++++++++++\n scripts/build.sh                                   |   3 +\n 20 files changed, 528 insertions(+), 16 deletions(-)\n"]}]

## tool · 2026-11-17T00:35:43Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 11151)
Total output lines: 1

[{"status":"fulfilled","value":["runtime/src/migration.ts","     1\timport { mkdir, readFile, writeFile, copyFile, stat, realpath, link, rm } from 'node:fs/promises';\n     2\timport { dirname, join, basename, isAbsolute } from 'node:path';\n     3\timport { fileURLToPath, pathToFileURL } from 'node:url';\n     4\timport { zstdDecompressSync, zstdCompressSync } from 'node:zlib';\n     5\timport { randomUUID } from 'node:crypto';\n     6\timport { constants } from 'node:fs';\n     7\timport { object, string, timestamp, content } from './types.ts';\n     8\timport type { Data, Session } from './types.ts';\n     9\timport { parseFile } from './logs.ts';\n    10\timport { RpcProcess } from './rpc.ts';\n    11\t\n    12\tinterface Historical { role: 'user' | 'assistant'; text: string; time: number }\n    13\t\n    14\texport async function migrateSession(value: unknown): Promise<Session> {\n    15\t  const input = object(value), source = object(input.session), target = object(input.target);\n    16\t  const kind = string(target.kind), home = string(input.home), cwd = string(input.cwd);\n    17\t  if (!['codex', 'claude', 'dsh'].includes(kind) || !isAbsolute(home) || !isAbsolute(cwd) || !string(source.id)\n    18\t    || !['codex', 'claude', 'dsh', 'desktop', 'acp'].includes(string(source.source))\n    19\t    || !Array.isArray(source.files) || !Array.isArray(source.messages) || !Array.isArray(target.args)\n    20\t    || target.args.some(x => typeof x !== 'string') || !string(target.command) || !string(target.id)) throw new Error('迁移来源、目标工具或目录无效');\n    21\t  if (Object.entries(object(target.env)).some(([key, value]) => !/^[A-Za-z_][A-Za-z0-9_]*$/.test(key) || typeof value !== 'string')) throw new Error('目标工具环境变量无效');\n    22\t  if (!(await stat(cwd)).isDirectory()) throw new Error('目标项目不是目录');\n    23\t  const files = source.files;\n    24\t  if (files.some(p => typeof p !== 'string' || !isAbsolute(p))) throw new Error('源记录路径无效');\n    25\t  const id = randomUUID(), now = Date.now();\n    26\t  const history: Historical[] = [], snapshots: { path: string; data: Buffer; fingerprint: string }[] = [];\n    27\t  const attachments = new Set<string>();\n    28\t  if (source.source === 'acp' || source.source === 'desktop') {\n    29\t    for (const raw of source.messages) {\n    30\t      const message = object(raw);\n    31\t      if (typeof message.text !== 'string') throw new Error('源消息内容无效');\n    32\t      history.push({ role: message.role === 'user' ? 'user' : 'assistant', text: message.text, time: timestamp(message.time) || now });\n    33\t    }\n    34\t  }\n    35\t  const collectAttachments = (v: unknown): void => {\n    36\t    if (Array.isArray(v)) { for (const item of v) collectAttachments(item); return; }\n    37\t    const record = object(v), type = string(record.type);\n    38\t    for (const [key, item] of Object.entries(record)) {\n    39\t      if (typeof item === 'string' && item.startsWith('file://')) attachments.add(fileURLToPath(item));\n    40\t      else if (typeof item === 'string' && isAbsolute(item) && /image|file|attachment/.test(type) && /path|url|image/.test(key)) attachments.add(item);\n    41\t      else if (typeof item === 'object' && item !== null) collectAttachments(item);\n    42\t    }\n    43\t  };\n    44\t  for (const path of files as string[]) {\n    45\t    const before = await stat(path);\n    46\t    if (!before.isFile()) throw new Error(`源记录不是普通文件：${path}`);\n    47\t    const data = await readFile(path);\n    48\t    const fingerprint = `${before.size}:${before.mtimeMs}`;\n    49\t    snapshots.push({ path, data, fingerprint });\n    50\t    if (!/\\.jsonl(?:\\.(?:zstd|zst))?$|\\.json$/i.test(path)) { attachments.add(path); continue; }\n    51\t    const text = (/\\.(zstd|zst)$/.test(path) ? zstdDecompressSync(data) : data).toString('utf8');\n    52\t    const records: unknown[] = /\\.json$/i.test(path) ? [JSON.parse(text)] : text.split('\\n').filter(line => line.trim()).map(line => JSON.parse(line));\n    53\t    for (const raw of records) {\n    54\t      const e = object(raw);\n    55\t      if (!Object.keys(e).length) throw new Error(`源记录格式无效：${path}`);\n    56\t      collectAttachments(e);\n    57\t      const p = object(e.payload), d = object(e.data), m = object(e.message);\n    58\t      const time = timestamp(e.timestamp ?? e.time) || now;\n    59\t      const native = e.type === 'response_item' && p.type === 'message' ? p\n    60\t        : e.type === 'assistant/message' ? object(d.message)\n    61\t        : e.type === 'user/message' ? d\n    62\t        : e.type === 'user' || e.type === 'assistant' ? { ...m, role: e.type } : undefined;\n    63\t      if (native) {\n    64\t        const text = content(native.content);\n    65\t        if (text) history.push({ role: native.role === 'user' || e.type === 'user/message' ? 'user' : 'assistant', text, time });\n    66\t      }\n    67\t      history.push({ role: 'assistant', time, text: `【迁移来源：${string(source.source)} · ${string(e.type, '原始记录')}】\\n\\n${JSON.stringify(e, null, 2)}` });\n    68\t    }\n    69\t  }\n    70\t  if (!snapshots.length) {\n    71\t    for (const raw of source.messages) {\n    72\t      const m = object(raw);\n    73\t      if (typeof m.text !== 'string') throw new Error('源消息内容无效');\n    74\t      history.push({ role: m.role === 'user' ? 'user' : 'assistant', text: m.text, time: timestamp(m.time) || now });\n    75\t    }\n    76\t  }\n    77\t  if (!history.length) throw new Error('没有可迁移的历史记录');\n    78\t  if (string(source.source) === 'desktop' && Array.isArray(source.warnings) && source.warnings.some(w => typeof w === 'string' && w.includes('附件'))) throw new Error('导出包缺失原始附件，无法完整迁移');\n    79\t  await mkdir(home, { recursive: true });\n    80\t  const canonicalHome = await realpath(home);\n    81\t  const migrationRoot = join(canonicalHome, '.ragdoll-migrations');\n    82\t  await mkdir(migrationRoot, { recursive: true, mode: 0o700 });\n    83\t  if (await realpath(migrationRoot) !== migrationRoot) throw new Error('迁移目录不能是符号链接');\n    84\t  const bundle = join(migrationRoot, id);\n    85\t  await mkdir(bundle, { mode: 0o700 });\n    86\t  let published: string | undefined;\n    87\t  try {\n    88\t    const copies = new Map<string, string>();\n    89\t    for (const path of attachments) {\n    90\t      if (!(await stat(path)).isFile()) throw new Error(`缺失附件或附件不是普通文件：${path}`);\n    91\t      const destination = join(bundle, `${copies.size}-${basename(path)}`);\n    92\t      await copyFile(path, destination, constants.COPYFILE_EXCL); copies.set(path, destination);\n    93\t    }\n    94\t    for (const item of history) for (const [from, to] of copies) {\n    95\t      item.text = item.text.replaceAll(pathToFileURL(from).href, pathToFileURL(to).href)\n    96\t        .replaceAll(JSON.stringify(from).slice(1, -1), JSON.stringify(to).slice(1, -1)).replaceAll(from, to);\n    97\t    }\n    98\t    for (const [index, snapshot] of snapshots.entries()) {\n    99\t      const current = await stat(snapshot.path);\n   100\t      if (`${current.size}:${current.mtimeMs}` !== snapshot.fingerprint) throw new Error('源会话正在变化，请停止原会话后重试迁移');\n   101\t      await writeFile(join(bundle, `raw-${index}-${basename(snapshot.path)}`), snapshot.data, { flag: 'wx', mode: 0o600 });\n   102\t    }\n   103\t    const migration = { sourceID: string(source.id), source: string(source.source), sourceNativeID: string(source.nativeID), created: now, title: string(source.title, '迁移会话') };\n   104\t    await writeFile(join(bundle, 'manifest.json'), JSON.stringify({ version: 1, migration, target: kind, id, originalUsage: source.usage, attachments: Object.fromEntries(copies) }, null, 2), { flag: 'wx', mode: 0o600 });\n   105\t    const iso = (time: number) => new Date(time).toISOString();\n   106\t    let rows: Data[], destination: string;\n   107\t    if (kind === 'codex') {\n   108\t      const day = iso(now).slice(0, 10);\n   109\t      destination = join(canonicalHome, 'sessions', ...day.split('-'), `rollout-${iso(now).replaceAll(':', '-')}-${id}.jsonl`);\n   110\t      rows = [{ timestamp: iso(now), type: 'session_meta', payload: { id, timestamp: iso(now), cwd, originator: 'codex_cli_rs', cli_version: '0.147.0', source: 'cli', model_provider: 'openai' } },\n   111\t        ...history.flatMap((m, index) => [\n   112\t          { timestamp: iso(m.time), type: 'event_msg', payload: { type: m.role === 'user' ? 'user_message' : 'agent_message', message: m.text, images: [], local_images: [] } },\n   113\t          { timestamp: iso(m.time), type: 'response_item', payload: { type: 'message', id: `migrated-${index}`, role: m.role, content: [{ type: m.role === 'user' ? 'input_text' : 'output_text', text: m.text }] } },\n   114\t        ])];\n   115\t    } else if (kind === 'claude') {\n   116\t      destination = join(canonicalHome, 'projects', cwd.replace(/[^a-zA-Z0-9]/g, '-'), `${id}.jsonl`);\n   117\t      let parentUuid: string | null = null;\n   118\t      rows = history.map(m => {\n   119\t        const uuid = randomUUID();\n   120\t        const row = { type: m.role, uuid, parentUuid, sessionId: id, cwd, isSidechain: false, timestamp: iso(m.time), version: '2.1.268', userType: 'external', message: { role: m.role, content: [{ type: 'text', text: m.text }], ...(m.role === 'assistant' ? { id: uuid, type: 'message', model: '<synthetic>', stop_reason: 'end_turn', stop_sequence: null } : {}) } };\n   121\t        parentUuid = uuid; return row;\n   122\t      });\n   123\t    } else {\n   124\t      let readable = '', separator = false;\n   125\t      for (let i = 0; i < cwd.length; i++) {\n   126\t        const ch = cwd[i]!;\n   127\t        if (ch === '/' || ch === '\\\\' || ch === ':') { if (!separator) readable += '-'; separator = true; }\n   128\t        else { readable += ch !== '~' && /^[A-Za-z0-9._-]$/.test(ch) ? ch : '~' + cwd.charCodeAt(i).toString(16).toUpperCase().padStart(4, '0'); separator = false; }\n   129\t      }\n   130\t      destination = join(canonicalHome, 'sessions', `--${(readable.replace(/^-+/, '') || 'root').slice(0, 251)}--`, id, 'session.v4.jsonl.zstd');\n   131\t      let turn = 0;\n   132\t      const events = history.flatMap((m): Data[] => {\n   133\t        if (m.role === 'user') return [{ type: 'user/message', time: m.time, surfaceOp: 'append', data: { id: randomUUID(), role: 'user', source: { kind: 'user' }, content: [{ type: 'text', text: m.text }] } }];\n   134\t        turn++;\n   135\t        return [\n   136\t          { type: 'turn/start', time: m.time, data: { turn } },\n   137\t          { type: 'step/start', time: m.time, data: { turn, step: 1 } },\n   138\t          { type: 'assistant/message', time: m.time, surfaceOp: 'append', data: { turn, step: 1, message: { id: randomUUID(), role: 'assistant', content: [{ type: 'text', text: m.text }], source: { kind: 'model', provider: 'deepseek-official', model: 'deepseek-v4-flash' } }, stream: [\n   139\t            { type: 'chunk', time: m.time, chunk: { type: 'block-start', index: 0, blockType: 'text' } },\n   140\t            { type: 'text-chunks', time0: m.time, index: 0, dt: [0], texts: [m.text] },\n   141\t            { type: 'chunk', time: m.time, chunk: { type: 'block-end', index: 0, block: { type: 'text', text: m.text } } },\n   142\t            { type: 'chunk', time: m.time, chunk: { type: 'finish', reason: { kind: 'stop' } } },\n   143\t          ] } },\n   144\t          { type: 'step/end', time: m.time, data: { turn, step: 1 } },\n   145\t          { type: 'turn/end', time: m.time, data: { turn, reason: { kind: 'completed' } } },\n   146\t        ];\n   147\t      });\n   148\t      if (string(source.title)) events.push({ type: 'session/title', time: now, data: { title: string(source.title), source: { kind: 'user' }, messageSeqs: [] } });\n   149\t      rows = [{ type: 'session', version: 4, id, cwd, createdAt: now, isSeeded: false, delegationDepth: 0 }, ...events.map((event, seq) => ({ ...event, seq }))];\n   150\t    }\n   151\t    let ancestor = dirname(destination);\n   152\t    while (true) {\n   153\t      try {\n   154\t        const existing = await realpath(ancestor);\n   155\t        if (existing !== canonicalHome && !existing.startsWith(canonicalHome + '/')) throw new Error('目标历史路径越界');\n   156\t        break;\n   157\t      } catch (error) { if (object(error).code !== 'ENOENT') throw error; ancestor = dirname(ancestor); }\n   158\t    }\n   159\t    await mkdir(dirname(destination), { recursive: true });\n   160\t    if (!(await realpath(dirname(destination))).startsWith(canonicalHome + '/')) throw new Error('目标历史路径越界');\n   161\t    const prepared = join(bundle, 'prepared.jsonl');\n   162\t    const output = kind === 'dsh'\n   163\t      ? Buffer.concat(rows.map(row => zstdCompressSync(Buffer.from(JSON.stringify(row) + '\\n'))))\n   164\t      : Buffer.from(rows.map(row => JSON.stringify(row)).join('\\n') + '\\n');\n   165\t    await writeFile(prepared, output, { flag: 'wx', mode: 0o600 });\n   166\t    await link(prepared, destination); published = destination;\n   167\t    const artifacts = [join(bundle, 'manifest.json'), ...snapshots.map((s, index) => join(bundle, `raw-${index}-${basename(s.path)}`)), ...copies.values()];\n   168\t    await writeFile(destination + '.ragdoll.json', JSON.stringify({ ...migration, files: artifacts }), { flag: 'wx', mode: 0o600 });\n   169\t    if (kind === 'codex' || kind === 'dsh') {\n   170\t      const args = target.args as string[];\n   171\t      const rpc = new RpcProcess(string(target.command), kind === 'codex' ? [...args, 'app-server'] : args, cwd, { ...object(target.env) as Record<string, string>, [kind === 'codex' ? 'CODEX_HOME' : 'DSH_HOME']: canonicalHome });\n   172\t      try {\n   173\t        if (kind === 'codex') {\n   174\t          await rpc.request('initialize', { clientInfo: { name: 'ragdoll', version: '0.1.0' }, capabilities: { experimentalApi: true } }); rpc.notify('initialized');\n   175\t          await rpc.request('thread/resume', { threadId: id, path: destination, cwd, approvalPolicy: 'on-request', sandbox: 'workspace-write' });\n   176\t          if (string(source.title)) await rpc.request('thread/name/set', { threadId: id, name: string(source.title) });\n   177\t        } else {\n   178\t          await rpc.request('initialize', { cwd, provider: 'deepseek-official', model: 'deepseek-v4-flash', maxTokens: 32768, approvalRequests: true });\n   179\t          await rpc.request('session/resume', { sessionId: id });\n   180\t        }\n   181\t      } finally { await rpc.close(); }\n   182\t    }\n   183\t    const session = await parseFile(kind as 'codex' | 'claude' | 'dsh', destination, canonicalHome);\n   184\t    session.migration = migration; session.instanceID = string(target.id); session.title = string(source.title, '迁移会话');\n   185\t    session.files = [...new Set([...session.files, ...artifacts])];\n   186\t    session.warnings.push('迁移历史：工具及专属记录按来源全文保留，不重新执行；旧用量归属原会话。');\n   187\t    if (kind === 'claude' || source.source === 'claude') session.warnings.push('Claude 原生迁移未验证');\n   188\t    return session;\n   189\t  } catch (error) {\n   190\t    if (published) { await rm(published, { force: true }); await rm(published + '.ragdoll.json', { force: true }); }\n   191\t    await rm(bundle, { recursive: true, force: true });\n   192\t    throw error;\n   193\t  }\n   194\t}\n"]},{"status":"fulfilled","value":["runtime/test/migration.test.ts","     1\timport { test } from 'node:test';\n     2\timport assert from 'node:assert/strict';\n     3\timport { mkdir, readFile, writeFile, rm, symlink, readdir, access } from 'node:fs/promises';\n     4\timport { join, resolve } from 'node:path';\n     5\timport { randomUUID } from 'node:crypto';\n     6\timport { migrateSession } from '../src/migration.ts';\n     7\timport { parseFile, defaultLocations } from '../src/logs.ts';\n     8\timport { Agents, defaultAgents } from '../src/agents.ts';\n     9\timport { object } from '../src/types.ts';\n    10\t\n    11\ttest('native migration preserves complete tool records and leaves source unchanged', async () => {\n    12\t  const root = resolve(import.meta.dirname, '../../.agent/tests', randomUUID());\n    13\t  await mkdir(root, { recursive: true });\n    14\t  const path = join(root, 'source.jsonl');\n    15\t  const original = [\n    16\t    { type: 'session', version: 3, id: 'source', cwd: root, createdAt: 1800000000000 },\n    17\t    { type: 'user/message', seq: 0, time: 1800000000001, data: { source: { kind: 'user' }, content: 'remember MIGRATE_1729' } },\n    18\t    { type: 'assistant/message', seq: 1, time: 1800000000002, data: { message: { role: 'assistant', content: [{ type: 'text', text: 'OK' }] } } },\n    19\t    { type: 'tool/result', seq: 2, time: 1800000000003, data: { result: { opaque: 'keep every byte of this record' } } },\n    20\t  ].map(row => JSON.stringify(row)).join('\\n') + '\\n';\n    21\t  await writeFile(path, original);\n    22\t  try {\n    23\t    const source = await parseFile('dsh', path, root);\n    24\t    const result = await migrateSession({ session: source, target: { id: 'native-codex', name: 'Codex', kind: 'codex', command: 'codex', args: [], env: {} }, home: join(root, 'target'), cwd: root });\n    25\t    assert.notEqual(result.nativeID, 'source');\n    26\t    assert.equal(result.migration?.sourceID, source.id);\n    27\t    assert.equal(result.usage.length, 0);\n    28\t    const text = await readFile(result.files.find(p => p.endsWith('.jsonl'))!, 'utf8');\n    29\t    assert.match(text, /MIGRATE_1729/);\n    30\t    assert.match(text, /keep every byte of this record/);\n    31\t    assert.equal(await readFile(path, 'utf8'), original);\n    32\t    const parsed = await parseFile('codex', result.files.find(p => p.endsWith('.jsonl'))!, join(root, 'target'));\n    33\t    assert.equal(parsed.messages.filter(m => m.role === 'assistant').some(m => m.text === 'OK'), true);\n    34\t    assert.equal(parsed.migration?.sourceID, source.id);\n    35\t  } finally { await rm(root, { recursive: true, force: true }); }\n    36\t});\n    37\t\n    38\ttest('migration copies attachments and rejects a target history symlink before creating external directories', async () => {\n    39\t  const root = resolve(import.meta.dirname, '../../.agent/tests', randomUUID());\n    40\t  await mkdir(root, { recursive: true });\n    41\t  const path = join(root, 'source.jsonl'), image = join(root, 'picture.png'), outside = join(root, 'outside'), home = join(root, 'target');\n    42\t  await writeFile(image, new Uint8Array([1, 2, 3, 4]));\n    43\t  await writeFile(path, JSON.stringify({ type: 'response_item', payload: { type: 'message', role: 'user', content: [{ type: 'input_image', image_url: new URL('file://' + image).href }] } }) + '\\n');\n    44\t  const target = { id: 'native-codex', name: 'Codex', kind: 'codex', command: 'codex', args: [], env: {} };\n    45\t  try {\n    46\t    const source = await parseFile('codex', path, root);\n    47\t    const migrated = await migrateSession({ session: source, target, home, cwd: root });\n    48\t    const copy = migrated.files.find(p => p.endsWith('picture.png'))!;\n    49\t    assert.notEqual(copy, image); assert.deepEqual(await readFile(copy), Buffer.from([1, 2, 3, 4]));\n    50\t    const hostile = join(root, 'hostile'); await mkdir(hostile); await mkdir(outside);\n    51\t    await symlink(outside, join(hostile, 'sessions'));\n    52\t    await assert.rejects(migrateSession({ sess…1151 tokens truncated… 108\t  await writeFile(path, [\n   109\t    { type: 'session_meta', payload: { id: 'original', cwd: root } },\n   110\t    { type: 'response_item', payload: { type: 'message', role: 'user', content: [{ type: 'input_text', text: 'remember DS_NATIVE_1729' }] } },\n   111\t    { type: 'response_item', payload: { type: 'message', role: 'assistant', content: [{ type: 'output_text', text: 'I remember.' }] } },\n   112\t  ].map(row => JSON.stringify(row)).join('\\n') + '\\n');\n   113\t  const agents = new Agents(join(root, 'cache'), () => {}, async () => ({ allowed: false }));\n   114\t  try {\n   115\t    const target = { id: 'native-dsh', name: 'dsh', kind: 'dsh' as const, command: '/Applications/DeepSeek Harness.app/Contents/Resources/runtime/cli/bin/dsh', args: ['--profile', 'sdk'], env: { DEEPSEEK_API_KEY: '' } };\n   116\t    const source = await parseFile('codex', path, root);\n   117\t    const result = await migrateSession({ session: source, target, home: join(root, 'target'), cwd: root });\n   118\t    const resumed = await agents.start({ agent: target, session: result, cwd: root });\n   119\t    assert.equal((resumed.session as { nativeID: string }).nativeID, result.nativeID);\n   120\t    await assert.rejects(agents.send(result.id, 'Reply only OK. Do not use tools.'), /no API key|MISSING_CREDENTIAL/);\n   121\t  } finally { await agents.close(); await rm(root, { recursive: true, force: true }); }\n   122\t});\n"]},{"status":"fulfilled","value":["Sources/RagdollCore/ArchiveSync.swift","     1\timport Foundation\n     2\timport Darwin\n     3\t\n     4\tpublic enum ArchiveSync {\n     5\t    public static func preview(root: URL, remote: String, branch: String) throws -> String {\n     6\t        try validate(remote: remote, branch: branch)\n     7\t        _ = try run(root, [\"check-ref-format\", \"refs/heads/\\(branch)\"], timeout: 10)\n     8\t        let destination = try run(root, [\"remote\", \"get-url\", \"--push\", remote], timeout: 10)\n     9\t        let files = try run(root, [\"ls-tree\", \"-r\", \"--name-only\", \"HEAD\"], timeout: 10).split(separator: \"\\n\").count\n    10\t        return \"目标：\\(destination)\\n分支：\\(branch)\\n将上传当前分支的完整历史，最新提交包含 \\(files) 个文件。\"\n    11\t    }\n    12\t    @discardableResult public static func push(root: URL, remote: String, branch: String, timeout: Double = 90) throws -> String {\n    13\t        try validate(remote: remote, branch: branch)\n    14\t        guard timeout > 0 else { throw failure(\"Git 超时时间无效\") }\n    15\t        _ = try run(root, [\"check-ref-format\", \"refs/heads/\\(branch)\"], timeout: timeout)\n    16\t        return try run(root, [\"push\", \"--porcelain\", remote, \"HEAD:refs/heads/\\(branch)\"], timeout: timeout)\n    17\t    }\n    18\t    private static func validate(remote: String, branch: String) throws {\n    19\t        guard remote.range(of: \"^[A-Za-z0-9][A-Za-z0-9._-]*$\", options: .regularExpression) != nil,\n    20\t              !branch.isEmpty, !branch.hasPrefix(\"-\"), !branch.contains(\":\"), !branch.contains(\"\\0\") else { throw failure(\"请指定有效的 Git 远端名称和分支\") }\n    21\t    }\n    22\t    private static func run(_ root: URL, _ args: [String], timeout: Double) throws -> String {\n    23\t        let directory = root.appendingPathComponent(\".ragdoll-process-\\(UUID().uuidString)\")\n    24\t        try FileManager.default.createDirectory(at: directory, withIntermediateDirectories: false, attributes: [.posixPermissions: 0o700])\n    25\t        defer { try? FileManager.default.removeItem(at: directory) }\n    26\t        let output = directory.appendingPathComponent(\"output\")\n    27\t        guard FileManager.default.createFile(atPath: output.path, contents: nil, attributes: [.posixPermissions: 0o600]) else { throw failure(\"无法创建 Git 输出文件\") }\n    28\t        let handle = try FileHandle(forWritingTo: output); defer { try? handle.close() }\n    29\t        let process = Process(); process.executableURL = URL(fileURLWithPath: \"/usr/bin/git\"); process.arguments = [\"-C\", root.path] + args\n    30\t        process.standardInput = FileHandle.nullDevice; process.standardOutput = handle; process.standardError = handle\n    31\t        process.environment = ProcessInfo.processInfo.environment.merging([\"GIT_TERMINAL_PROMPT\": \"0\", \"GCM_INTERACTIVE\": \"never\", \"SSH_ASKPASS_REQUIRE\": \"never\", \"SSH_ASKPASS\": \"/usr/bin/false\", \"GIT_ASKPASS\": \"/usr/bin/false\"]) { _, new in new }\n    32\t        let ended = DispatchSemaphore(value: 0)\n    33\t        process.terminationHandler = { _ in ended.signal() }\n    34\t        try process.run()\n    35\t        if ended.wait(timeout: .now() + timeout) == .timedOut {\n    36\t            let pid = process.processIdentifier\n    37\t            let target = getpgid(pid) == pid ? -pid : pid\n    38\t            kill(target, SIGTERM)\n    39\t            if ended.wait(timeout: .now() + 1) == .timedOut { kill(target, SIGKILL); process.waitUntilExit() }\n    40\t            throw failure(\"远端推送超时；本地归档已保留，可重试\")\n    41\t        }\n    42\t        var text = String(decoding: try Data(contentsOf: output), as: UTF8.self)\n    43\t        let pattern = try NSRegularExpression(pattern: \"(?:https?|ssh)://[^\\\\s'\\\"<>]+\")\n    44\t        for match in pattern.matches(in: text, range: NSRange(text.startIndex..., in: text)).reversed() {\n    45\t            guard let range = Range(match.range, in: text) else { continue }\n    46\t            var url = URLComponents(string: String(text[range]))\n    47\t            url?.user = nil; url?.password = nil; url?.query = nil; url?.fragment = nil\n    48\t            text.replaceSubrange(range, with: url?.string ?? \"<远端地址>\")\n    49\t        }\n    50\t        text = text.trimmingCharacters(in: .whitespacesAndNewlines)\n    51\t        guard process.terminationStatus == 0 else { throw failure(\"本地归档已保留，Git 操作失败：\\(text)\") }\n    52\t        return text\n    53\t    }\n    54\t    private static func failure(_ text: String) -> NSError { NSError(domain: \"Ragdoll.ArchiveSync\", code: 1, userInfo: [NSLocalizedDescriptionKey: text]) }\n    55\t}\n"]},{"status":"fulfilled","value":["Sources/RagdollCore/BackgroundService.swift","     1\timport Foundation\n     2\timport Darwin\n     3\t\n     4\tpublic final class ServiceLease: Sendable {\n     5\t    private let descriptor: Int32\n     6\t    public init(root: URL, name: String = \"service-lock\") throws {\n     7\t        try FileManager.default.createDirectory(at: root, withIntermediateDirectories: true, attributes: [.posixPermissions: 0o700])\n     8\t        let descriptor = open(root.appendingPathComponent(name).path, O_CREAT | O_RDWR | O_NOFOLLOW, 0o600)\n     9\t        guard descriptor >= 0 else { throw POSIXError(POSIXErrorCode(rawValue: errno) ?? .EIO) }\n    10\t        guard flock(descriptor, LOCK_EX | LOCK_NB) == 0 else { close(descriptor); throw NSError(domain: \"Ragdoll.Service\", code: 1, userInfo: [NSLocalizedDescriptionKey: \"另一个进程正在处理此目录\"]) }\n    11\t        self.descriptor = descriptor\n    12\t    }\n    13\t    deinit { flock(descriptor, LOCK_UN); close(descriptor) }\n    14\t}\n    15\t\n    16\tpublic struct ServiceStatus: Codable, Sendable {\n    17\t    public var pid: Int32 = getpid()\n    18\t    public var updated: Date = Date()\n    19\t    public var scan = \"等待扫描\"\n    20\t    public var archive = \"等待归档\"\n    21\t    public var sync = \"未启用远端推送\"\n    22\t    public var lastArchive: Date?\n    23\t    public init() {}\n    24\t}\n    25\t\n    26\tpublic enum BackgroundService {\n    27\t    public static func isRunning(root: URL) -> Bool {\n    28\t        do { let lease = try ServiceLease(root: root); withExtendedLifetime(lease) {}; return false }\n    29\t        catch { return true }\n    30\t    }\n    31\t    public static func request(root: URL) throws {\n    32\t        try FileManager.default.createDirectory(at: root, withIntermediateDirectories: true, attributes: [.posixPermissions: 0o700])\n    33\t        try Data(UUID().uuidString.utf8).write(to: root.appendingPathComponent(\"service-request\"), options: .atomic)\n    34\t    }\n    35\t    public static func status(root: URL) throws -> ServiceStatus? {\n    36\t        let path = root.appendingPathComponent(\"service-status.json\")\n    37\t        guard FileManager.default.fileExists(atPath: path.path) else { return nil }\n    38\t        return try JSONDecoder().decode(ServiceStatus.self, from: Data(contentsOf: path))\n    39\t    }\n    40\t}\n    41\t\n    42\tpublic actor BackgroundWorker {\n    43\t    private let root: URL\n    44\t    private let store: Store\n    45\t    private let bridge = RuntimeBridge()\n    46\t    private var state = ServiceStatus()\n    47\t    private var dirtySince: Date?\n    48\t    private var lastDirty: Date?\n    49\t    private var generation = 0\n    50\t    private var needsScan = true\n    51\t\n    52\t    public init(root: URL) throws {\n    53\t        self.root = root\n    54\t        store = try Store(path: root.appendingPathComponent(\"index.sqlite\").path)\n    55\t        if FileManager.default.fileExists(atPath: root.appendingPathComponent(\"archive-dirty\").path) { dirtySince = .distantPast; lastDirty = .distantPast }\n    56\t    }\n    57\t    private func publish() throws {\n    58\t        state.updated = Date()\n    59\t        try JSONEncoder().encode(state).write(to: root.appendingPathComponent(\"service-status.json\"), options: .atomic)\n    60\t    }\n    61\t    private func markDirty() throws {\n    62\t        dirtySince = dirtySince ?? Date(); lastDirty = Date(); generation += 1\n    63\t        try Data(\"pending\".utf8).write(to: root.appendingPathComponent(\"archive-dirty\"), options: .atomic)\n    64\t    }\n    65\t    private func receive(_ event: String, _ data: JSONValue) {\n    66\t        do {\n    67\t            if event == \"session\", try store.save(data.decode(Session.self)) { try markDirty() }\n    68\t            if event == \"sourceChanged\" { needsScan = true }\n    69\t            if event == \"warning\" { state.scan = data.string }\n    70\t            if event == \"disconnected\" { state.scan = data.string }\n    71\t        } catch { state.scan = error.localizedDescription }\n    72\t    }\n    73\t    public func run(once: Bool = false) async throws {\n    74\t        let lease = try ServiceLease(root: root)\n    75\t        defer { withExtendedLifetime(lease) {} }\n    76\t        await bridge.setHandler { [weak self] event, data in await self?.receive(event, data) }\n    77\t        try await bridge.start(dataDirectory: root)\n    78\t        _ = try await bridge.request(\"initialize\")\n    79\t        var lastScan = Date.distantPast, lastPush = Date.distantPast, lastArchiveAttempt = Date.distantPast, lastRequest: Data?, lastSettings: Data?, lastVersion: Int?\n    80\t        let encoder = JSONEncoder(); encoder.outputFormatting = [.sortedKeys]\n    81\t        repeat {\n    82\t            do {\n    83\t                let settings = try store.settings()\n    84\t                if !once && settings.backgroundEnabled != true { break }\n    85\t                let settingsData = try encoder.encode(settings)\n    86\t                if settingsData != lastSettings { lastSettings = settingsData; needsScan = true; try markDirty() }\n    87\t                let version = try store.dataVersion()\n    88\t                if version != lastVersion { lastVersion = version; try markDirty() }\n    89\t                let requestPath = root.appendingPathComponent(\"service-request\")\n    90\t                let request = FileManager.default.fileExists(atPath: requestPath.path) ? try Data(contentsOf: requestPath) : nil\n    91\t                let requested = request != lastRequest\n    92\t                if requested { lastRequest = request; needsScan = true; try markDirty() }\n    93\t                if needsScan || Date().timeIntervalSince(lastScan) >= 60 {\n    94\t                    needsScan = false; state.scan = \"正在扫描\"; try publish()\n    95\t                    let result = try await bridge.request(\"scan\", [\"locations\": try .encode(settings.locations)], timeout: 600)\n    96\t                    state.scan = \"扫描完成 · \\(result[\"count\"].text) 个变更\"; lastScan = Date()\n    97\t                }\n    98\t                let due = dirtySince.map { Date().timeIntervalSince($0) >= 300 || Date().timeIntervalSince(lastDirty ?? $0) >= 30 } ?? false\n    99\t                if !settings.archivePath.isEmpty && (once || requested || (due && Date().timeIntervalSince(lastArchiveAttempt) >= 30)) {\n   100\t                    lastArchiveAttempt = Date()\n   101\t                    let current = generation\n   102\t                    state.archive = \"正在保存并提交\"; try publish()\n   103\t                    let store = self.store\n   104\t                    let result = try await Task.detached(priority: .utility) {\n   105\t                        let sessions = try store.list().filter { !settings.excludedProjects.contains($0.project) }.compactMap { try store.session($0.id) }\n   106\t                        return try Archive.save(sessions, to: URL(fileURLWithPath: settings.archivePath), sourceRoots: settings.locations.map(\\.path))\n   107\t                    }.value\n   108\t                    state.archive = result.commit.map { \"本地归档已提交 · \\($0)\" } ?? \"本地归档已是最新\"\n   109\t                    state.lastArchive = Date()\n   110\t                    if current == generation { dirtySince = nil; try FileManager.default.removeItem(at: root.appendingPathComponent(\"archive-dirty\")) }\n   111\t                    if settings.archiveRemote != nil { try Data(\"pending\".utf8).write(to: root.appendingPathComponent(\"sync-pending\"), options: .atomic); lastPush = .distantPast }\n   112\t                }\n   113\t                if let remote = settings.archiveRemote, !settings.archivePath.isEmpty,\n   114\t                   FileManager.default.fileExists(atPath: root.appendingPathComponent(\"sync-pending\").path), Date().timeIntervalSince(lastPush) >= 60 {\n   115\t                    lastPush = Date(); state.sync = \"正在推送\"; try publish()\n   116\t                    do {\n   117\t                        _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: settings.archivePath), remote: remote.remote, branch: remote.branch) }.value\n   118\t                        try FileManager.default.removeItem(at: root.appendingPathComponent(\"sync-pending\"))\n   119\t                        state.sync = \"已推送到 \\(remote.remote)/\\(remote.branch)\"\n   120\t                    } catch { state.sync = \"推送待重试：\\(error.localizedDescription)\" }\n   121\t                }\n   122\t                if settings.archiveRemote == nil { state.sync = \"未启用远端推送\" }\n   123\t                try publish()\n   124\t            } catch {\n   125\t                state.archive = \"处理失败：\\(error.localizedDescription)\"; try publish()\n   126\t                if once { await bridge.close(); throw error }\n   127\t            }\n   128\t            if once { break }\n   129\t            try await Task.sleep(for: .seconds(2))\n   130\t        } while !Task.isCancelled\n   131\t        await bridge.close()\n   132\t    }\n   133\t}\n"]},{"status":"fulfilled","value":["Sources/RagdollService/ServiceMain.swift","     1\timport Foundation\n     2\timport RagdollCore\n     3\t\n     4\t@main\n     5\tstruct ServiceMain {\n     6\t    static func main() async {\n     7\t        let arguments = ProcessInfo.processInfo.arguments\n     8\t        let root: URL\n     9\t        if let index = arguments.firstIndex(of: \"--data-dir\") {\n    10\t            guard arguments.indices.contains(index + 1), !arguments[index + 1].hasPrefix(\"--\") else {\n    11\t                FileHandle.standardError.write(Data(\"--data-dir 缺少目录参数\\n\".utf8)); exit(2)\n    12\t            }\n    13\t            root = URL(fileURLWithPath: arguments[index + 1])\n    14\t        } else {\n    15\t            root = ProcessInfo.processInfo.environment[\"RAGDOLL_DATA_DIR\"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent(\"Library/Application Support/Ragdoll\")\n    16\t        }\n    17\t        do {\n    18\t            try FileManager.default.createDirectory(at: root, withIntermediateDirectories: true, attributes: [.posixPermissions: 0o700])\n    19\t            try await BackgroundWorker(root: root).run(once: arguments.contains(\"--once\"))\n    20\t        } catch {\n    21\t            FileHandle.standardError.write(Data((error.localizedDescription + \"\\n\").utf8)); exit(1)\n    22\t        }\n    23\t    }\n    24\t}\n"]},{"status":"fulfilled","value":["Sources/Ragdoll/MigrationView.swift","     1\timport SwiftUI\n     2\timport RagdollCore\n     3\t\n     4\tstruct MigrationView: View {\n     5\t    @EnvironmentObject var model: AppModel\n     6\t    @Environment(\\.dismiss) var dismiss\n     7\t    let session: Session\n     8\t    @State private var targetID = \"\"\n     9\t    @State private var cwd = \"\"\n    10\t    @State private var migrating = false\n    11\t    var targets: [AgentConfig] { model.settings.agents.filter { [\"codex\", \"claude\", \"dsh\"].contains($0.kind) && $0.kind != session.source } }\n    12\t    var body: some View {\n    13\t        VStack(alignment: .leading, spacing: 18) {\n    14\t            Text(\"迁移到其他工具\").font(.title2.bold())\n    15\t            Text(session.title).font(.headline).lineLimit(2)\n    16\t            Text(\"在目标工具创建新的原生历史，保留原会话。目标不支持的推理和工具记录将以带来源标记的全文历史展示，旧用量仍归属原会话。\").font(.callout).foregroundStyle(.secondary)\n    17\t            Form {\n    18\t                Picker(\"目标工具\", selection: $targetID) { ForEach(targets) { Text($0.name).tag($0.id) } }\n    19\t                HStack { TextField(\"目标项目目录\", text: $cwd); Button(\"选择…\") { if let path = model.chooseProject() { cwd = path } } }\n    20\t                Text(\"来源：\\(sourceName(session.source)) · \\(session.messages.count) 条已索引消息；转换将读取完整原始记录和附件。\").font(.caption)\n    21\t                if session.source == \"claude\" || targets.first(where: { $0.id == targetID })?.kind == \"claude\" { Text(\"Claude 原生迁移未验证\").foregroundStyle(.orange) }\n    22\t            }\n    23\t            HStack {\n    24\t                Button(\"取消\") { dismiss() }.disabled(migrating)\n    25\t                Spacer()\n    26\t                if migrating { ProgressView().controlSize(.small) }\n    27\t                Button(\"迁移\") {\n    28\t                    guard let agent = targets.first(where: { $0.id == targetID }) else { return }\n    29\t                    migrating = true\n    30\t                    Task { let success = await model.migrateSelected(agent: agent, cwd: cwd); migrating = false; if success { dismiss() } }\n    31\t                }.buttonStyle(.borderedProminent).disabled(migrating || targetID.isEmpty || cwd.isEmpty || !model.ready)\n    32\t            }\n    33\t        }.padding(28).frame(width: 600)\n    34\t        .onAppear { targetID = targets.first?.id ?? \"\"; cwd = session.project.isEmpty ? FileManager.default.homeDirectoryForCurrentUser.path : session.project }\n    35\t        .interactiveDismissDisabled(migrating)\n    36\t    }\n    37\t}\n"]}]

## tool · 2026-11-17T00:35:51Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 12206)
Total output lines: 601

Tests/RagdollCoreTests/BackgroundServiceTests.swift
     1	import Foundation
     2	import Testing
     3	@testable import RagdollCore
     4	
     5	@Test func backgroundServiceOwnsOneDataDirectoryAndPreservesNewRequests() throws {
     6	    let root = try testDirectory(); defer { try? FileManager.default.removeItem(at: root) }
     7	    var first: ServiceLease? = try ServiceLease(root: root)
     8	    #expect(BackgroundService.isRunning(root: root))
     9	    #expect(throws: (any Error).self) { try ServiceLease(root: root) }
    10	    try BackgroundService.request(root: root)
    11	    let old = try Data(contentsOf: root.appendingPathComponent("service-request"))
    12	    try BackgroundService.request(root: root)
    13	    #expect(try Data(contentsOf: root.appendingPathComponent("service-request")) != old)
    14	    first = nil
    15	    #expect(!BackgroundService.isRunning(root: root))
    16	    let second = try ServiceLease(root: root)
    17	    withExtendedLifetime(second) { #expect(BackgroundService.isRunning(root: root)) }
    18	    _ = first
    19	}
    20	
    21	@Test func backgroundServiceArchivesFromItsOwnProcess() async throws {
    22	    let root = try testDirectory(); defer { try? FileManager.default.removeItem(at: root) }
    23	    let source = root.appendingPathComponent("source/sessions"), archive = root.appendingPathComponent("archive")
    24	    try FileManager.default.createDirectory(at: source, withIntermediateDirectories: true)
    25	    try FileManager.default.createDirectory(at: archive, withIntermediateDirectories: true)
    26	    try git(archive, ["init"]); try git(archive, ["config", "user.name", "Background"]); try git(archive, ["config", "user.email", "background@localhost"])
    27	    let raw = "{\"type\":\"session_meta\",\"payload\":{\"id\":\"background-check\"}}\n{\"type\":\"response_item\",\"payload\":{\"type\":\"message\",\"role\":\"user\",\"content\":[{\"type\":\"input_text\",\"text\":\"SERVICE_NATIVE_1729\"}]}}\n"
    28	    try Data(raw.utf8).write(to: source.appendingPathComponent("session.jsonl"))
    29	    let store = try Store(path: root.appendingPathComponent("index.sqlite").path)
    30	    let remote = root.appendingPathComponent("remote.git")
    31	    try git(archive, ["remote", "add", "origin", remote.path])
    32	    var settings = Settings(); settings.locations = [Location(source: "codex", path: source.deletingLastPathComponent().path)]; settings.archivePath = archive.path; settings.archiveRemote = ArchiveRemote(remote: "origin", branch: "archive")
    33	    try store.saveSettings(settings)
    34	    let project = URL(fileURLWithPath: #filePath).deletingLastPathComponent().deletingLastPathComponent().deletingLastPathComponent()
    35	    let executable = project.appendingPathComponent(".build/debug/RagdollService")
    36	    let process = Process(); process.executableURL = executable; process.arguments = ["--data-dir", root.path, "--once"]
    37	    process.standardOutput = FileHandle.nullDevice; process.standardError = FileHandle.nullDevice
    38	    try process.run()
    39	    let deadline = Date().addingTimeInterval(20)
    40	    while process.isRunning && Date() < deadline { try await Task.sleep(for: .milliseconds(50)) }
    41	    if process.isRunning { process.terminate(); Issue.record("独立服务未在期限内完成"); return }
    42	    #expect(process.terminationStatus == 0)
    43	    #expect(try store.list(query: "SERVICE_NATIVE_1729").count == 1)
    44	    #expect(try git(archive, ["log", "-1", "--format=%s"]) == "chore(archive): sync conversations")
    45	    #expect(FileManager.default.fileExists(atPath: root.appendingPathComponent("sync-pending").path))
    46	    let head = try git(archive, ["rev-parse", "HEAD"])
    47	    try git(root, ["init", "--bare", remote.path])
    48	    let retry = Process(); retry.executableURL = executable; retry.arguments = ["--data-dir", root.path, "--once"]
    49	    retry.standardOutput = FileHandle.nullDevice; retry.standardError = FileHandle.nullDevice
    50	    try retry.run()
    51	    let retryDeadline = Date().addingTimeInterval(20)
    52	    while retry.isRunning && Date() < retryDeadline { try await Task.sleep(for: .milliseconds(50)) }
    53	    if retry.isRunning { retry.terminate(); Issue.record("服务重启未完成"); return }
    54	    #expect(retry.terminationStatus == 0)
    55	    #expect(try git(archive, ["rev-parse", "HEAD"]) == head)
    56	    #expect(try git(remote, ["rev-parse", "refs/heads/archive"]) == head)
    57	    #expect(!FileManager.default.fileExists(atPath: root.appendingPathComponent("sync-pending").path))
    58	}
    59	
    60	@Test func backgroundServiceContinuesAfterItsLauncherReturns() async throws {
    61	    let root = try testDirectory(); defer { try? FileManager.default.removeItem(at: root) }
    62	    let source = root.appendingPathComponent("source/sessions"), archive = root.appendingPathComponent("archive")
    63	    try FileManager.default.createDirectory(at: source, withIntermediateDirectories: true)
    64	    try FileManager.default.createDirectory(at: archive, withIntermediateDirectories: true)
    65	    try git(archive, ["init"]); try git(archive, ["config", "user.name", "Service"]); try git(archive, ["config", "user.email", "service@localhost"])
    66	    let store = try Store(path: root.appendingPathComponent("index.sqlite").path)
    67	    var settings = Settings(); settings.locations = [Location(source: "codex", path: source.deletingLastPathComponent().path)]; settings.archivePath = archive.path; settings.backgroundEnabled = true
    68	    try store.saveSettings(settings); try BackgroundService.request(root: root)
    69	    let project = URL(fileURLWithPath: #filePath).deletingLastPathComponent().deletingLastPathComponent().deletingLastPathComponent()
    70	    let process = Process(); process.executableURL = project.appendingPathComponent(".build/debug/RagdollService"); process.arguments = ["--data-dir", root.path]
    71	    process.standardOutput = FileHandle.nullDevice; process.standardError = FileHandle.nullDevice
    72	    try process.run(); defer { if process.isRunning { process.terminate(); process.waitUntilExit() } }
    73	    let deadline = Date().addingTimeInterval(20)
    74	    while (try BackgroundService.status(root: root)?.lastArchive) == nil && Date() < deadline { try await Task.sleep(for: .milliseconds(50)) }
    75	    #expect(BackgroundService.isRunning(root: root))
    76	    let raw = "{\"type\":\"session_meta\",\"payload\":{\"id\":\"late\"}}\n{\"type\":\"response_item\",\"payload\":{\"type\":\"message\",\"role\":\"user\",\"content\":[{\"type\":\"input_text\",\"text\":\"AFTER_LAUNCH_1729\"}]}}\n"
    77	    try Data(raw.utf8).write(to: source.appendingPathComponent("late.jsonl")); try BackgroundService.request(root: root)
    78	    while try store.list(query: "AFTER_LAUNCH_1729").isEmpty && Date() < deadline { try await Task.sleep(for: .milliseconds(50)) }
    79	    #expect(try store.list(query: "AFTER_LAUNCH_1729").count == 1)
    80	    let newRecord = archive.appendingPathComponent("sessions/codex")
    81	    while !FileManager.default.fileExists(atPath: newRecord.path) && Date() < deadline { try await Task.sleep(for: .milliseconds(50)) }
    82	    #expect(FileManager.default.fileExists(atPath: newRecord.path))
    83	    #expect(process.isRunning)
    84	}

Tests/RagdollCoreTests/ArchiveSyncTests.swift
     1	import Foundation
     2	import Testing
     3	@testable import RagdollCore
     4	
     5	@Test func archiveSyncPreviewShowsTheDestinationWithoutCredentials() throws {
     6	    let root = try testDirectory(); defer { try? FileManager.default.removeItem(at: root) }
     7	    try git(root, ["init"]); try git(root, ["config", "user.name", "Preview"]); try git(root, ["config", "user.email", "preview@localhost"])
     8	    _ = try Archive.save([Session(id: "preview", source: "codex", title: "Preview")], to: root)
     9	    try git(root, ["remote", "add", "origin", "https://username:secret-value@example.com/archive.git?token=private"])
    10	    let preview = try ArchiveSync.preview(root: root, remote: "origin", branch: "archive")
    11	    #expect(preview.contains("example.com/archive.git"))
    12	    #expect(!preview.contains("secret-value")); #expect(!preview.contains("private")); #expect(!preview.contains("username"))
    13	}
    14	
    15	@Test func archiveSyncStopsAHangingPushAndPreservesItsLocalCommit() throws {
    16	    let root = try testDirectory(); defer { try? FileManager.default.removeItem(at: root) }
    17	    let local = root.appendingPathComponent("local"), remote = root.appendingPathComponent("remote.git")
    18	    try FileManager.default.createDirectory(at: local, withIntermediateDirectories: true)
    19	    try git(root, ["init", "--bare", remote.path]); try git(local, ["init"])
    20	    try git(local, ["config", "user.name", "Timeout"]); try git(local, ["config", "user.email", "timeout@localhost"])
    21	    _ = try Archive.save([Session(id: "one", source: "codex", title: "One")], to: local)
    22	    try git(local, ["remote", "add", "origin", remote.path])
    23	    let hook = local.appendingPathComponent(".git/hooks/pre-push")
    24	    try Data("#!/bin/sh\nsleep 10\n".utf8).write(to: hook)
    25	    try FileManager.default.setAttributes([.posixPermissions: 0o700], ofItemAtPath: hook.path)
    26	    let before = try git(local, ["rev-parse", "HEAD"]), start = Date()
    27	    #expect(throws: (any Error).self) { try ArchiveSync.push(root: local, remote: "origin", branch: "archive", timeout: 0.2) }
    28	    #expect(Date().timeIntervalSince(start) < 3)
    29	    #expect(try git(local, ["rev-parse", "HEAD"]) == before)
    30	}
    31	
    32	@Test func archiveSyncRetriesWithoutANewCommitAndRejectsDivergence() throws {
    33	    let directory = try testDirectory(); defer { try? FileManager.default.removeItem(at: directory) }
    34	    let local = directory.appendingPathComponent("local"), remote = directory.appendingPathComponent("remote.git")
    35	    try FileManager.default.createDirectory(at: local, withIntermediateDirectories: true)
    36	    try git(local, ["init"]); try git(local, ["config", "user.name", "Test"]); try git(local, ["config", "user.email", "test@localhost"])
    37	    let session = Session(id: "one", source: "codex", title: "One")
    38	    _ = try Archive.save([session], to: local)
    39	    let head = try git(local, ["rev-parse", "HEAD"])
    40	    try git(local, ["remote", "add", "origin", remote.path])
    41	    #expect(throws: (any Error).self) { try ArchiveSync.push(root: local, remote: "origin", branch: "archive") }
    42	    #expect(try git(local, ["rev-parse", "HEAD"]) == head)
    43	    try git(directory, ["init", "--bare", remote.path])
    44	    _ = try ArchiveSync.push(root: local, remote: "origin", branch: "archive")
    45	    #expect(try git(remote, ["rev-parse", "refs/heads/archive"]) == head)
    46	    #expect(try Archive.save([session], to: local).commit == nil)
    47	    _ = try ArchiveSync.push(root: local, remote: "origin", branch: "archive")
    48	    let other = directory.appendingPathComponent("other")
    49	    try git(directory, ["clone", "--branch", "archive", remote.path, other.path])
    50	    try git(other, ["config", "user.name", "Other"]); try git(other, ["config", "user.email", "other@localhost"])
    51	    try Data("remote work".utf8).write(to: other.appendingPathComponent("remote.txt"))
    52	    try git(other, ["add", "remote.txt"]); try git(other, ["commit", "-m", "remote work"]); try git(other, ["push"])
    53	    #expect(throws: (any Error).self) { try ArchiveSync.push(root: local, remote: "origin", branch: "archive") }
    54	    #expect(try git(local, ["rev-parse", "HEAD"]) == head)
    55	    #expect(throws: (any Error).self) { try ArchiveSync.push(root: local, remote: "--all", branch: "archive") }
    56	}
    57	
    58	@Test func archiveSyncSettingsDecodeOlderRecordsAndMigrationSurvivesRefresh() throws {
    59	    let old = try JSONEncoder().encode(Settings())
    60	    var data = try JSONSerialization.jsonObject(with: old) as! [String: Any]
    61	    data.removeValue(forKey: "archiveRemote"); data.removeValue(forKey: "backgroundEnabled")
    62	    let settings = try JSONDecoder().decode(Settings.self, from: JSONSerialization.data(withJSONObject: data))
    63	    #expect(settings.archiveRemote == nil)
    64	    let root = try testDirectory(); defer { try? FileManager.default.removeItem(at: root) }
    65	    let store = try Store(path: root.appendingPathComponent("index.sqlite").path)
    66	    var migrated = Session(id: "new", source: "codex", title: "Migrated")
    67	    migrated.migration = MigrationOrigin(sourceID: "old", source: "dsh", sourceNativeID: "old-native", created: 1)
    68	    try store.save(migrated)
    69	    migrated.migration = nil; try store.save(migrated)
    70	    #expect(try store.session("new")?.migration?.sourceID == "old")
    71	}

Sources/Ragdoll/SettingsView.swift
     1	import SwiftUI
     2	import AppKit
     3	import RagdollCore
     4	import ServiceManagement
     5	
     6	struct SettingsView: View {
     7	    @EnvironmentObject var model: AppModel
     8	    @State private var tab = 0
     9	    @State private var editor: AgentConfig?
    10	    @State private var showRegistry = false
    11	    @State private var historyAgent: AgentConfig?
    12	    @State private var prices = ""
    13	    @State private var remoteName = "origin"
    14	    @State private var remoteBranch = "main"
    15	    @State private var remotePreview = ""
    16	    @State private var checkedRemote: ArchiveRemote?
    17	    var body: some View {
    18	        VStack(alignment: .leading, spacing: 18) {
    19	            Text("设置").font(.largeTitle.bold())
    20	            Picker("设置分类", selection: $tab) {
    21	                Text("数据来源").tag(0); Text("Agent 与 ACP").tag(1); Text("Git 归档").tag(2); Text("模型价格").tag(3)
    22	            }.pickerStyle(.segmented).frame(maxWidth: 600)
    23	            ScrollView {
    24	                VStack(alignment: .leading, spacing: 18) {
    25	                    switch tab {
    26	                    case 0: sources
    27	                    case 1: agents
    28	                    case 2: archive
    29	                    default: pricing
    30	                    }
    31	                }.frame(maxWidth: 1050, alignment: .leading).padding(.vertical, 10)
    32	            }
    33	        }.padding(28).navigationTitle("设置")
    34	        .sheet(item: $editor) { agent in AgentEditor(agent: agent).environmentObject(model) }
    35	        .sheet(isPresented: $showRegistry) { RegistryView().environmentObject(model) }
    36	        .sheet(item: $historyAgent) { agent in NativeHistoryView(agent: agent).environmentObject(model) }
    37	        .onAppear {
    38	            prices = (try? JSONValue.encode(model.settings.prices).text) ?? "{}"
    39	            remoteName = model.settings.archiveRemote?.remote ?? "origin"; remoteBranch = model.settings.archiveRemote?.branch ?? "main"
    40	            model.pollBackground()
    41	        }
    42	        .onChange(of: model.settings.archivePath) { _, _ in checkedRemote = nil; remotePreview = "" }
    43	    }
    44	    var sources: some View {
    45	        Group {
    46	            Card {
    47	                VStack(alignment: .leading, spacing: 18) {
    48	                    Text("本地会话目录").font(.headline)
    49	                    Text("首次读取全部历史，之后自动扫描变化。源日志只读；应用中的新对话通过各工具自己的接口保存。").font(.callout).foregroundStyle(.secondary)
    50	                    ForEach(Array(model.settings.locations.enumerated()), id: \.offset) { i, location in
    51	                        HStack {
    52	                            Text(sourceName(location.source)).frame(width: 140, alignment: .leading)
    53	                            TextField("目录", text: Binding(get: { model.settings.locations[i].path }, set: { model.settings.locations[i].path = $0 })).textFieldStyle(.roundedBorder)
    54	                            Button("选择…") { if let path = model.chooseProject() { model.settings.locations[i].path = path } }
    55	                        }
    56	                    }
    57	                    HStack { Spacer(); Button("保存并扫描") { model.persistSettings(); Task { await model.refresh() } }.buttonStyle(.borderedProminent).disabled(model.scanning) }
    58	                }
    59	            }
    60	            Card {
    61	                HStack {
    62	                    VStack(alignment: .leading, spacing: 8) { Text("Claude 普通聊天").font(.headline); Text("导入官方 ZIP 或 conversations.json；不含原始上传附件，缺失用量显示未知。").font(.caption).foregroundStyle(.secondary) }
    63	                    Spacer(); Button("导入官方导出包…") { model.importDesktop() }
    64	                }
    65	            }
    66	            if !model.warnings.isEmpty {
    67	                Card { VStack(alignment: .leading, spacing: 10) { Text("最近读取与连接提示").font(.headline); ForEach(Array(model.warnings.suffix(15).enumerated()), id: \.offset) { _, warning in Text(warning).font(.system(size: 11, design: .monospaced)).textSelection(.enabled).foregroundStyle(.secondary) } } }
    68	            }
    69	        }
    70	    }
    71	    var agents: some View {
    72	        Group {
    73	            HStack {
    74	                VStack(alignment: .leading, spacing: 6) { Text("对话提供方").font(.headline); Text("原生接口与 ACP 共用聊天界面；登录和模型能力由 Agent 提供。").font(.caption).foregroundStyle(.secondary) }
    75	                Spacer()
    76	                Button("添加本地 ACP") { editor = AgentConfig(name: "新 ACP Agent", command: "") }
    77	                Button("浏览官方目录") { showRegistry = true }.buttonStyle(.borderedProminent)
    78	            }
    79	            ForEach(model.settings.agents) { agent in
    80	                Card {
    81	                    VStack(alignment: .leading, spacing: 12) {
    82	                        HStack {
    83	                            Image(systemName: agent.kind == "acp" ? "puzzlepiece.extension" : "cpu").font(.title2).foregroundStyle(.blue)
    84	                            VStack(alignment: .leading, spacing: 4) { Text(agent.name).font(.headline); Text("\(agent.kind == "acp" ? "ACP" : "原生接口")\(agent.version.map { " · \($0)" } ?? "")").font(.caption).foregroundStyle(.secondary) }
    85	                            Spacer()
    86	                            if model.busyAgents.contains(agent.id) { ProgressView().controlSize(.small) }
    87	                            Button("检测连接") { Task { await model.probe(agent) } }.disabled(model.busyAgents.contains(agent.id))
    88	                            Button("编辑") { editor = agent }
    89	                            if agent.kind == "codex" || agent.kind == "claude" { Button("登录…") { Task { await model.nativeLogin(agent) } } }
    90	                            if agent.kind == "acp" { Button("导入历史") { if let project = model.chooseProject() { Task { await model.listNative(agent, project: project); historyAgent = agent } } } }
    91	                            if agent.kind == "acp" { Button("移除", role: .destructive) { Task { await model.removeAgent(agent) } } }
    92	                        }
    93	                        Text(([agent.command] + agent.args).joined(separator: " ")).font(.system(size: 10, design: .monospaced)).foregroundStyle(.secondary).textSelection(.enabled)
    94	                        if let info = mode…2206 tokens truncated…font(.title2.bold())
   199	            Form {
   200	                TextField("名称", text: $agent.name)
   201	                TextField("程序路径或命令", text: $agent.command)
   202	                LabeledContent("参数（每行一项）") { TextEditor(text: $arguments).font(.system(.caption, design: .monospaced)).frame(height: 80) }
   203	                LabeledContent("环境变量（NAME=value）") { TextEditor(text: $environment).font(.system(.caption, design: .monospaced)).frame(height: 100) }
   204	                if agent.kind == "acp" {
   205	                    Picker("协议", selection: Binding(get: { agent.protocol ?? 0 }, set: { agent.protocol = $0 == 0 ? nil : $0 })) { Text("自动协商").tag(0); Text("ACP v1").tag(1); Text("ACP v2（实验性）").tag(2) }
   206	                }
   207	            }
   208	            Text("直接运行程序，不展开 Shell 表达式。环境变量保存到系统钥匙串，不写入会话归档。").font(.caption).foregroundStyle(.secondary)
   209	            HStack { Button("取消") { dismiss() }; Spacer(); Button("保存") { save() }.buttonStyle(.borderedProminent).disabled(agent.name.isEmpty || agent.command.isEmpty || failedToLoad) }
   210	        }.padding(28).frame(width: 640)
   211	        .onAppear {
   212	            arguments = agent.args.joined(separator: "\n")
   213	            do { let env = try Secrets.load(agent.id).merging(agent.env) { old, _ in old }; environment = env.sorted { $0.key < $1.key }.map { "\($0.key)=\($0.value)" }.joined(separator: "\n") }
   214	            catch { failedToLoad = true; model.error = error.localizedDescription }
   215	        }
   216	    }
   217	    func save() {
   218	        do {
   219	            var env: [String: String] = [:]
   220	            for line in environment.components(separatedBy: .newlines) where !line.isEmpty {
   221	                guard let separator = line.firstIndex(of: "=") else { model.error = "环境变量每行必须为 NAME=value"; return }
   222	                let name = String(line[..<separator]); guard name.range(of: "^[A-Za-z_][A-Za-z0-9_]*$", options: .regularExpression) != nil else { model.error = "无效的环境变量名称"; return }
   223	                env[name] = String(line[line.index(after: separator)...])
   224	            }
   225	            agent.args = arguments.components(separatedBy: .newlines).filter { !$0.isEmpty }; agent.env = env
   226	            try model.saveAgent(agent); dismiss()
   227	        } catch { model.error = error.localizedDescription }
   228	    }
   229	}
   230	
   231	struct RegistryView: View {
   232	    @EnvironmentObject var model: AppModel
   233	    @Environment(\.dismiss) var dismiss
   234	    @State private var search = ""
   235	    var entries: [JSONValue] { model.registry.filter { search.isEmpty || ($0["name"].string + $0["description"].string).localizedCaseInsensitiveContains(search) } }
   236	    var body: some View {
   237	        VStack(alignment: .leading, spacing: 16) {
   238	            HStack { Text("ACP 官方目录").font(.title2.bold()); Spacer(); if model.registryLoading { ProgressView().controlSize(.small) }; Button("刷新") { Task { await model.loadRegistry() } }; Button("完成") { dismiss() } }
   239	            Text("Agent 在本机执行，使用自己的账号和权限。安装前可查看项目来源及许可证；更新不会自动进行。").font(.caption).foregroundStyle(.secondary)
   240	            TextField("搜索 Agent", text: $search).textFieldStyle(.roundedBorder)
   241	            List(Array(entries.enumerated()), id: \.offset) { _, entry in
   242	                HStack(alignment: .top, spacing: 16) {
   243	                    VStack(alignment: .leading, spacing: 7) {
   244	                        HStack { Text(entry["name"].string).font(.headline); Text(entry["version"].string).font(.system(.caption, design: .monospaced)).foregroundStyle(.secondary) }
   245	                        Text(entry["description"].string).font(.caption).foregroundStyle(.secondary).lineLimit(3)
   246	                        HStack { if let url = URL(string: entry["repository"].string) { Link("项目来源", destination: url) }; if let url = URL(string: entry["license_url"].string) { Link("许可证", destination: url) } }.font(.caption)
   247	                    }
   248	                    Spacer()
   249	                    let installed = model.settings.agents.first { $0.registryID == entry["id"].string }
   250	                    if model.busyAgents.contains(entry["id"].string) { ProgressView().controlSize(.small) }
   251	                    Button(installed == nil ? "安装" : installed?.version == entry["version"].string ? "已安装" : "更新") { Task { await model.installAgent(entry) } }.disabled(model.busyAgents.contains(entry["id"].string) || installed?.version == entry["version"].string)
   252	                }.padding(.vertical, 10)
   253	            }
   254	        }.padding(24).frame(width: 850, height: 650).task { if model.registry.isEmpty { await model.loadRegistry() } }
   255	    }
   256	}

packaging/com.oyamameek.ragdoll.service.plist
     1	<?xml version="1.0" encoding="UTF-8"?>
     2	<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
     3	<plist version="1.0"><dict>
     4	  <key>Label</key><string>com.oyamameek.ragdoll.service</string>
     5	  <key>BundleProgram</key><string>Contents/MacOS/RagdollService</string>
     6	  <key>RunAtLoad</key><true/>
     7	  <key>KeepAlive</key><dict><key>SuccessfulExit</key><false/></dict>
     8	  <key>ThrottleInterval</key><integer>10</integer>
     9	  <key>ProcessType</key><string>Background</string>
    10	</dict></plist>

runtime/src/logs.ts
2:import { readdir, stat, realpath, readFile } from 'node:fs/promises';
61:export async function parseFile(source: Location['source'], path: string, home = dirname(path)): Promise<Session> {
66:    messages: [], usage: [], files: [path], warnings: [],
153:  try { migrationData = await readFile(path + '.ragdoll.json'); }
160:    session.files.push(path + '.ragdoll.json');
161:    if (migration.files !== undefined) {
162:      const root = (await realpath(home)) + '/.ragdoll-migrations/';
163:      if (!Array.isArray(migration.files) || migration.files.some(p => typeof p !== 'string')) throw new Error('迁移附件清单无效');
164:      for (const file of migration.files as string[]) { if (!(await realpath(file)).startsWith(root)) throw new Error('迁移附件清单越界'); }
165:      session.files.push(...migration.files as string[]);
206:        const session = await parseFile(location.source, await realpath(path), location.path);

Sources/Ragdoll/AppModel.swift
23:    @Published var scanning = false
39:    @Published var archiveStatus = "尚未选择归档仓库"
43:    @Published var backgroundStatus = "未启用后台服务"
44:    @Published var syncStatus = "未启用远端推送"
45:    let bridge = RuntimeBridge()
49:    private var archiveTask: Task<Void, Never>?
67:        let start = Calendar.current.date(byAdding: .day, value: -6, to: Calendar.current.startOfDay(for: Date()))!
70:            return date >= start && Calendar.current.component(.weekday, from: date) - 1 == bucket[0] && Calendar.current.component(.hour, from: date) == bucket[1]
76:    func launch() async {
78:        await bridge.setHandler { [weak self] event, data in await self?.receive(event, data) }
80:            try await bridge.start(dataDirectory: root)
81:            let initial = try await bridge.request("initialize")
85:            try saveSettings(); ready = true
86:            if settings.backgroundEnabled == true { await setBackground(true) }
91:                    self.pollBackground()
92:                    if !BackgroundService.isRunning(root: self.root), Date().timeIntervalSince(self.lastRefresh) >= 60 { await self.refresh() }
93:                    if self.settings.archiveRemote != nil, !BackgroundService.isRunning(root: self.root), !self.archiving, FileManager.default.fileExists(atPath: self.root.appendingPathComponent("sync-pending").path), Date().timeIntervalSince(self.lastPushAttempt) >= 60 { await self.archiveNow() }
103:                if try store?.save(session) == true {
121:            case "approval": approvals.append(Approval(id: data["requestID"].string, method: data["method"].string, params: data["params"]))
122:            case "approvalCancelled": approvals.removeAll { $0.id == data["requestID"].string }
123:            case "sourceChanged": if !scanning { Task { await refresh() } }
141:    func refresh() async {
142:        guard ready, !scanning, !archiving else { return }
143:        if BackgroundService.isRunning(root: root) {
144:            do { try BackgroundService.request(root: root); pollBackground() } catch { self.error = error.localizedDescription }
147:        scanning = true; status = "正在读取会话…"
150:            let lease = try ServiceLease(root: root)
151:            defer { withExtendedLifetime(lease) {} }
152:            let result = try await bridge.request("scan", ["locations": try .encode(settings.locations)], timeout: 600)
155:        scanning = false; scheduleArchive(markDirty: false)
167:    func saveSettings() throws { try store?.saveSettings(settings) }
168:    func persistSettings() { do { try saveSettings() } catch { self.error = error.localizedDescription } }
172:    func saveAgent(_ agent: AgentConfig) throws {
173:        try Secrets.save(agent.env, for: agent.id)
176:        try saveSettings()
178:    @discardableResult func startChat(agent: AgentConfig, cwd: String, resume: Session? = nil) async -> Bool {
183:            let result = try await bridge.request("chat.start", params)
185:            _ = try store?.save(session); try reload(); select(session.id)
190:    func resumeSelected() async {
195:        await startChat(agent: agent, cwd: selected.project.isEmpty ? FileManager.default.homeDirectoryForCurrentUser.path : selected.project, resume: selected)
197:    func send(_ text: String, attachments: [URL] = []) async -> Bool {
202:        do { _ = try await bridge.request("chat.send", ["id": .string(id), "text": .string(text), "model": .string(selected.source == "acp" ? "" : composerModel), "attachments": try .encode(attachments.map(\.path))], timeout: 0); return true }
205:    func stop() async {
207:        do { _ = try await bridge.request("chat.stop", ["id": .string(id)]) } catch { self.error = error.localizedDescription }
209:    func answer(_ request: Approval, allowed: Bool, optionID: String? = nil, content: JSONValue? = nil) async {
214:            _ = try await bridge.request("approval", ["requestID": .string(request.id), "answer": .object(answer)])
215:            approvals.removeAll { $0.id == request.id }
218:    func probe(_ agent: AgentConfig) async {
220:        do { agentInfo[agent.id] = try await bridge.request("probe", ["agent": try .encode(hydrated(agent)), "cwd": .string(FileManager.default.homeDirectoryForCurrentUser.path)]) }
223:    func loadRegistry() async {
225:        do { registry = try await bridge.request("registry").array } catch { self.error = error.localizedDescription }
227:    func installAgent(_ entry: JSONValue) async {
230:            let value = try await bridge.request("install", ["agent": entry], timeout: 600)
234:            try saveAgent(config); status = "已安装 \(entry["name"].string)"
237:    func removeAgent(_ agent: AgentConfig) async {
240:            _ = try await bridge.request("uninstall", ["agent": try .encode(agent)])
241:            settings.agents.removeAll { $0.id == agent.id }; try Secrets.save([:], for: agent.id); try saveSettings()
244:    func authenticate(_ agent: AgentConfig, methodID: String) async {
247:            let result = try await bridge.request("authenticate", ["agent": try .encode(hydrated(agent)), "methodID": .string(methodID), "cwd": .string(FileManager.default.homeDirectoryForCurrentUser.path)], timeout: 600)
255:        Task { do { _ = try await bridge.request("import", ["path": .string(url.path)]); try reload(); scheduleArchive() } catch { self.error = error.localizedDescription } }
260:        if settings.archivePath != url.path { settings.archiveRemote = nil; syncStatus = "未启用远端推送" }
261:        settings.archivePath = url.path; persistSettings(); scheduleArchive(); Task { await archiveNow() }
272:        if !scanning && !archiving && BackgroundService.isRunning(root: root) { archiveTask?.cancel(); return }
273:        guard !settings.archivePath.isEmpty else { return }
276:        guard !scanning else { return }
277:        archiveTask?.cancel()
279:        archiveTask = Task { do { try await Task.sleep(for: .seconds(delay)); await archiveNow() } catch {} }
281:    func archiveNow() async {
282:        guard let store, !settings.archivePath.isEmpty, !archiving, !scanning else { return }
283:        if BackgroundService.isRunning(root: root) {
284:            do { try BackgroundService.request(root: root); archiveStatus = "已请求后台归档" } catch { self.error = error.localizedDescription }
287:        archiving = true; archiveStatus = "正在保存并提交…"
289:        let path = settings.archivePath, excluded = settings.excludedProjects, roots = settings.locations.map(\.path)
291:            let lease = try ServiceLease(root: root)
292:            defer { withExtendedLifetime(lease) {} }
295:                return try Archive.save(sessions, to: URL(fileURLWithPath: path), sourceRoots: roots)
297:            archiveStatus = result.commit.map { "已保存并提交 · \($0) · \(result.files) 个文件" } ?? "归档已是最新，无需提交"
299:            if let remote = settings.archiveRemote {
300:                try Data("pending".utf8).write(to: root.appendingPathComponent("sync-pending"), options: .atomic)
301:                lastPushAttempt = Date(); syncStatus = "正在推送"
303:                    _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: path), remote: remote.remote, branch: remote.branch) }.value
304:                    try FileManager.default.removeItem(at: root.appendingPathComponent("sync-pending"))
305:                    syncStatus = "已推送到 \(remote.remote)/\(remote.branch)"
306:                } catch { syncStatus = "推送待重试：\(error.localizedDescription)" }
307:            } else { syncStatus = "未启用远端推送" }
308:        } catch { archiveStatus = "归档未完成：\(error.localizedDescription)"; self.error = error.localizedDescription }
313:    func pollBackground() {
314:        guard !scanning, !archiving else { return }
316:            let running = BackgroundService.isRunning(root: root)
317:            if running, let state = try BackgroundService.status(root: root) {
318:                backgroundStatus = "后台服务正在运行 · PID \(state.pid)"
319:                status = state.scan; archiveStatus = state.archive; syncStatus = state.sync; lastArchive = state.lastArchive
324:                backgroundStatus = service.status == .requiresApproval ? "请在系统登录项中允许后台服务" : settings.backgroundEnabled == true ? "后台服务尚未运行" : "未启用后台服务"
328:    func setBackground(_ enabled: Bool) async {
332:            while scanning || archiving { try await Task.sleep(for: .milliseconds(100)) }
333:            settings.backgroundEnabled = enabled; try saveSettings()
335:                archiveTask?.cancel()
338:            pollBackground()
339:        } catch { self.error = error.localizedDescription; pollBackground() }
341:    func migrateSelected(agent: AgentConfig, cwd: String) async -> Bool {
347:            let result = try await bridge.request("migrate", ["session": try .encode(session), "target": try .encode(config), "home": .string(home), "cwd": .string(cwd)], timeout: 600)
348:            let migrated = try result["session"].decode(Session.self)
349:            _ = try store?.save(migrated); try reload(); select(migrated.id); scheduleArchive()
359:    func nativeLogin(_ agent: AgentConfig) async {
361:            let result = try await bridge.request("native.login", ["agent": try .encode(agent)])
365:    func configure(_ configID: String, value: String) async {
368:            let result = try await bridge.request("chat.configure", ["id": .string(id), "configID": .string(configID), "value": .string(value)])
374:    func listNative(_ agent: AgentConfig, project: String, more: Bool = false) async {
376:            let result = try await bridge.request("chat.list", ["agent": try .encode(hydrated(agent)), "cwd": .string(project), "cursor": .string(more ? nativeCursor : "")])
381:    func importNative(_ agent: AgentConfig, record: JSONValue) async -> Bool {
383:            let result = try await bridge.request("chat.import", ["agent": try .encode(hydrated(agent)), "cwd": .string(nativeHistoryProject), "session": record])
385:            _ = try store?.save(session); try reload(); select(session.id); conversationInfo[session.id] = result["info"]; scheduleArchive(); return true

scripts/build.sh
     1	#!/bin/bash
     2	set -euo pipefail
     3	root=$(cd "$(dirname "$0")/.." && pwd)
     4	cd "$root"
     5	export CLANG_MODULE_CACHE_PATH="$root/.cache/clang"
     6	export SWIFT_MODULECACHE_PATH="$root/.cache/swift-modules"
     7	mkdir -p .cache dist
     8	swift build -c release --cache-path .cache/swift --config-path .cache/swift-config --security-path .cache/swift-security --disable-sandbox
     9	npm --prefix runtime ci --ignore-scripts --cache "$root/.cache/npm"
    10	npm --prefix runtime run build
    11	node_version=26.13.0
    12	node_name="node-v${node_version}-darwin-arm64"
    13	if [ ! -x ".cache/$node_name/bin/node" ]; then
    14	  curl --fail --location --retry 2 "https://nodejs.org/dist/v${node_version}/${node_name}.tar.gz" -o ".cache/${node_name}.tar.gz"
    15	  curl --fail --location "https://nodejs.org/dist/v${node_version}/SHASUMS256.txt" -o .cache/SHASUMS256.txt
    16	  rg " ${node_name}\.tar\.gz$" .cache/SHASUMS256.txt > .cache/node-checksums.txt
    17	  (cd .cache && shasum -a 256 -c node-checksums.txt)
    18	  tar -xzf ".cache/${node_name}.tar.gz" -C .cache
    19	fi
    20	stage="$root/dist/Ragdoll.staging.app"
    21	if [ -d "$stage" ]; then rm -rf "$stage"; fi
    22	mkdir -p "$stage/Contents/MacOS" "$stage/Contents/Resources/runtime/app"
    23	trap 'rm -rf "$stage"' EXIT
    24	cp .build/release/Ragdoll "$stage/Contents/MacOS/Ragdoll"
    25	cp .build/release/RagdollService "$stage/Contents/MacOS/RagdollService"
    26	mkdir -p "$stage/Contents/Library/LaunchAgents"
    27	cp packaging/com.oyamameek.ragdoll.service.plist "$stage/Contents/Library/LaunchAgents/"
    28	cp packaging/Info.plist "$stage/Contents/Info.plist"
    29	cp -R ".cache/$node_name" "$stage/Contents/Resources/runtime/node"
    30	cp runtime/package.json runtime/package-lock.json "$stage/Contents/Resources/runtime/app/"
    31	cp -R runtime/dist "$stage/Contents/Resources/runtime/app/dist"
    32	npm --prefix "$stage/Contents/Resources/runtime/app" ci --omit=dev --omit=optional --ignore-scripts --cache "$root/.cache/npm"
    33	for bundle in .build/release/*.bundle; do
    34	  if [ -d "$bundle" ]; then cp -R "$bundle" "$stage/Contents/Resources/"; fi
    35	done
    36	cp -R docs "$stage/Contents/Resources/docs"
    37	codesign --force --deep --sign - "$stage"
    38	codesign --verify --deep --strict "$stage"
    39	"$stage/Contents/Resources/runtime/node/bin/node" "$stage/Contents/Resources/runtime/app/dist/main.mjs" --self-check
    40	if [ -d dist/Ragdoll.previous.app ]; then rm -rf dist/Ragdoll.previous.app; fi
    41	if [ -d dist/Ragdoll.app ]; then mv dist/Ragdoll.app dist/Ragdoll.previous.app; fi
    42	mv "$stage" dist/Ragdoll.app
    43	trap - EXIT
    44	echo "Built: $root/dist/Ragdoll.app"


## tool · 2026-11-17T00:35:59Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 12039)
Total output lines: 669

arc
     1	import Foundation
     2	import CryptoKit
     3	
     4	public struct ArchiveResult: Sendable { public var files: Int; public var commit: String? }
     5	public enum Archive {
     6	    public static func save(_ sessions: [Session], to root: URL, sourceRoots: [String] = []) throws -> ArchiveResult {
     7	        let root = root.standardizedFileURL.resolvingSymlinksInPath()
     8	        for path in sourceRoots where !path.isEmpty {
     9	            let source = URL(fileURLWithPath: path).standardizedFileURL.resolvingSymlinksInPath().path
    10	            guard root.path != source && !root.path.hasPrefix(source + "/") else { throw failure("归档目录不能放在源日志目录中") }
    11	        }
    12	        let fm = FileManager.default
    13	        try fm.createDirectory(at: root, withIntermediateDirectories: true)
    14	        let lease = try ServiceLease(root: root, name: ".ragdoll-archive-lock")
    15	        defer { withExtendedLifetime(lease) {} }
    16	        if !fm.fileExists(atPath: root.appendingPathComponent(".git").path) { _ = try git(root, ["init"]) }
    17	        guard try git(root, ["rev-parse", "--show-toplevel"]) == root.path else { throw failure("请选择 Git 仓库的根目录") }
    18	        let manifestURL = root.appendingPathComponent(".ragdoll-manifest.json")
    19	        guard manifestURL.resolvingSymlinksInPath().path.hasPrefix(root.path + "/") else { throw failure("归档清单不能指向仓库外部") }
    20	        let old = fm.fileExists(atPath: manifestURL.path) ? try JSONDecoder().decode([String: String].self, from: Data(contentsOf: manifestURL)) : [:]
    21	        let encoder = JSONEncoder(); encoder.outputFormatting = [.prettyPrinted, .sortedKeys, .withoutEscapingSlashes]
    22	        var desired: [String: Data] = [:]
    23	        for session in sessions {
    24	            let base = "sessions/\(safeName(session.source))/\(safeName(session.id))"
    25	            var metadata = session; metadata.messages = []
    26	            desired[base + "/metadata.json"] = try encoder.encode(metadata)
    27	            let transcript = "# \(session.title)\n\n来源：\(session.source)\n\n项目：\(session.project)\n\n" + session.messages.map { "## \($0.role) · \(ISO8601DateFormatter().string(from: Date(timeIntervalSince1970: $0.time / 1000)))\n\n\($0.text)\n" }.joined(separator: "\n")
    28	            let portable = session.files.enumerated().reduce(transcript) { text, entry in
    29	                text.replacingOccurrences(of: URL(fileURLWithPath: entry.element).absoluteString, with: "raw/\(entry.offset)-\(safeName(URL(fileURLWithPath: entry.element).lastPathComponent))")
    30	            }
    31	            desired[base + "/transcript.md"] = Data(portable.utf8)
    32	            for (index, path) in session.files.enumerated() {
    33	                let file = URL(fileURLWithPath: path)
    34	                guard fm.fileExists(atPath: file.path) else { continue }
    35	                let values = try file.resourceValues(forKeys: [.isRegularFileKey])
    36	                guard values.isRegularFile == true else { throw failure("无法归档非普通文件：\(path)") }
    37	                desired[base + "/raw/\(index)-\(safeName(file.lastPathComponent))"] = try Data(contentsOf: file)
    38	            }
    39	            if session.files.isEmpty { desired[base + "/events.json"] = try encoder.encode(session) }
    40	        }
    41	        for (path, _) in desired {
    42	            let destination = root.appendingPathComponent(path)
    43	            guard !destination.resolvingSymlinksInPath().path.hasPrefix(root.path + "/.git/") && destination.resolvingSymlinksInPath().path.hasPrefix(root.path + "/") else { throw failure("归档路径越界") }
    44	            if fm.fileExists(atPath: destination.path) {
    45	                let digest = hash(try Data(contentsOf: destination))
    46	                guard old[path] == digest else { throw failure("归档文件已被手动修改或不属于应用：\(path)。请保留修改后选择其他归档目录，或恢复文件后重试。") }
    47	            } else if old[path] != nil { throw failure("归档文件已被手动删除：\(path)。请处理该删除后重试。") }
    48	        }
    49	        let managed = Array(desired.keys) + [".ragdoll-manifest.json"]
    50	        let managedSet = Set(managed)
    51	        let staged = try gitData(root, ["diff", "--cached", "--name-only", "-z"]).split(separator: 0).map { String(decoding: $0, as: UTF8.self) }
    52	        for path in staged where managedSet.contains(path) {
    53	            let data = try gitData(root, ["show", ":\(path)"])
    54	            let expected = path == ".ragdoll-manifest.json" ? (fm.fileExists(atPath: manifestURL.path) ? hash(try Data(contentsOf: manifestURL)) : nil) : old[path]
    55	            guard expected == hash(data) else { throw failure("归档文件存在外部暂存修改，已保留：\(path)。请先处理该暂存修改后重试。") }
    56	        }
    57	        var manifest = old
    58	        var changed: [String] = []
    59	        for (path, data) in desired {
    60	            let digest = hash(data), destination = root.appendingPathComponent(path)
    61	            if old[path] == digest && fm.fileExists(atPath: destination.path) { continue }
    62	            try fm.createDirectory(at: destination.deletingLastPathComponent(), withIntermediateDirectories: true)
    63	            try data.write(to: destination, options: .atomic)
    64	            manifest[path] = digest; changed.append(path)
    65	        }
    66	        let manifestData = try encoder.encode(manifest)
    67	        let previousManifest = fm.fileExists(atPath: manifestURL.path) ? try Data(contentsOf: manifestURL) : nil
    68	        if previousManifest != manifestData {
    69	            try manifestData.write(to: manifestURL, options: .atomic); changed.append(".ragdoll-manifest.json")
    70	        }
    71	        let gitDirectory = try git(root, ["rev-parse", "--absolute-git-dir"])
    72	        let pathspec = URL(fileURLWithPath: gitDirectory).appendingPathComponent("ragdoll-pathspec-\(UUID().uuidString)")
    73	        try Data((managed.joined(separator: "\0") + "\0").utf8).write(to: pathspec)
    74	        defer { try? fm.removeItem(at: pathspec) }
    75	        _ = try git(root, ["add", "--pathspec-from-file=\(pathspec.path)", "--pathspec-file-nul"])
    76	        let pending = try gitData(root, ["diff", "--cached", "--name-only", "-z"]).split(separator: 0).map { String(decoding: $0, as: UTF8.self) }
    77	        guard pending.contains(where: { managedSet.contains($0) }) else { return ArchiveResult(files: 0, commit: nil) }
    78	        _ = try git(root, ["commit", "--only", "-m", "chore(archive): sync conversations", "--pathspec-from-file=\(pathspec.path)", "--pathspec-file-nul"])
    79	        return ArchiveResult(files: changed.count, commit: try git(root, ["rev-parse", "--short", "HEAD"]))
    80	    }
    81	
    82	    private static func safeName(_ value: String) -> String {
    83	        let allowed = CharacterSet.alphanumerics.union(CharacterSet(charactersIn: "._-"))
    84	        let name = value.unicodeScalars.map { allowed.contains($0) ? String($0) : "_" }.joined()
    85	        return name.isEmpty || name == "." || name == ".." ? "session" : name
    86	    }
    87	    private static func hash(_ data: Data) -> String { SHA256.hash(data: data).map { String(format: "%02x", $0) }.joined() }
    88	    private static func failure(_ message: String) -> NSError { NSError(domain: "Ragdoll.Archive", code: 1, userInfo: [NSLocalizedDescriptionKey: message]) }
    89	    private static func git(_ root: URL, _ args: [String]) throws -> String {
    90	        String(decoding: try gitData(root, args), as: UTF8.self).trimmingCharacters(in: .whitespacesAndNewlines)
    91	    }
    92	    private static func gitData(_ root: URL, _ args: [String]) throws -> Data {
    93	        let process = Process(); process.executableURL = URL(fileURLWithPath: "/usr/bin/git"); process.arguments = ["-C", root.path] + args
    94	        let pipe = Pipe(); process.standardOutput = pipe; process.standardError = pipe
    95	        process.environment = ProcessInfo.processInfo.environment.merging(["GIT_TERMINAL_PROMPT": "0"]) { _, new in new }
    96	        try process.run()
    97	        let data = pipe.fileHandleForReading.readDataToEndOfFile(); process.waitUntilExit()
    98	        let text = String(decoding: data, as: UTF8.self).trimmingCharacters(in: .whitespacesAndNewlines)
    99	        guard process.terminationStatus == 0 else { throw failure("文件已保留；Git 操作失败：\(text)") }
   100	        return data
   101	    }
   102	}

rg
runtime/src/logs.ts:66:    messages: [], usage: [], files: [path], warnings: [],
runtime/src/logs.ts:160:    session.files.push(path + '.ragdoll.json');
runtime/src/logs.ts:165:      session.files.push(...migration.files as string[]);
runtime/src/desktop.ts:9:  if (!Array.isArray(value)) throw new Error('请选择包含 conversations.json 的 Claude 官方导出包');
runtime/src/desktop.ts:14:      id: sessionKey('desktop', string(v.uuid)), nativeID: string(v.uuid), source: 'desktop',
runtime/src/desktop.ts:16:      created: timestamp(v.created_at), updated: timestamp(v.updated_at), messages: [], usage: [], files: [],
runtime/src/desktop.ts:35:    if (!found) throw new Error('导出包中未找到 conversations.json');
runtime/src/types.ts:8:  messages: Message[]; usage: Usage[]; files: string[]; warnings: string[];
runtime/src/migration.ts:168:    await writeFile(destination + '.ragdoll.json', JSON.stringify({ ...migration, files: artifacts }), { flag: 'wx', mode: 0o600 });
runtime/src/agents.ts:264:      title: '新对话', project: cwd, home, created: Date.now(), updated: Date.now(), messages: [], usage: [], files: [], warnings: [],
runtime/src/agents.ts:469:    const session: Session = { id: sessionKey('acp', `${agent.id}\0${nativeID}`), nativeID, source: 'acp', instanceID: agent.id, title: string(record.title, nativeID), project: string(record.cwd, cwd), home: '', created: Date.now(), updated: Date.now(), messages: [], usage: [], files: [], warnings: [] };

settings
   104	                    }
   105	                }
   106	            }
   107	            if !model.loginLinks.isEmpty { Card { VStack(alignment: .leading, spacing: 8) { Text("登录链接").font(.headline); ForEach(model.loginLinks, id: \.self) { url in Link("打开登录页面 · \(url.host ?? "")", destination: url) } } } }
   108	        }
   109	    }
   110	    var archive: some View {
   111	        Group {
   112	            Card {
   113	                VStack(alignment: .leading, spacing: 16) {
   114	                    Text("Git 自动归档").font(.headline)
   115	                    Text("保存原始记录、Markdown 和元数据；合并变更后创建本地提交，可开启指定远端的自动推送。").foregroundStyle(.secondary)
   116	                    HStack { Text(model.settings.archivePath.isEmpty ? "尚未选择目录" : model.settings.archivePath).font(.system(.caption, design: .monospaced)).textSelection(.enabled); Spacer(); Button("选择专用仓库…") { model.chooseArchive() } }
   117	                    Text(model.archiveStatus).font(.caption).foregroundStyle(.secondary).textSelection(.enabled)
   118	                    HStack {
   119	                        if let date = model.lastArchive { Text("上次完成：\(date.formatted())").font(.caption).foregroundStyle(.secondary) }
   120	                        Spacer()
   121	                        if model.archiving { ProgressView().controlSize(.small) }
   122	                        Button("立即归档") { Task { await model.archiveNow() } }.buttonStyle(.borderedProminent).disabled(model.archiving || model.settings.archivePath.isEmpty)
   123	                    }
   124	                    Text("自动保存采用 30 秒防抖，最长合并 5 分钟。源文件删除后保留已有归档；手工修改的归档文件会阻止自动覆盖。Git 需要已配置提交者姓名与邮箱。").font(.caption).foregroundStyle(.secondary)
   125	                }
   126	            }
   127	            Card {
   128	                VStack(alignment: .leading, spacing: 12) {
   129	                    Text("远端归档推送").font(.headline)
   130	                    Text("推送包含所选 Git 分支的全部历史及对话内容，请使用专用归档仓库。认证沿用系统 Git；失败保留本地提交并自动重试，远端分歧不会强制覆盖。").font(.caption).foregroundStyle(.secondary)
   131	                    HStack { TextField("远端名称", text: $remoteName); TextField("目标分支", text: $remoteBranch) }.textFieldStyle(.roundedBorder)
   132	                    if !remotePreview.isEmpty { Text(remotePreview).font(.caption).textSelection(.enabled) }
   133	                    Text(model.syncStatus).font(.caption).textSelection(.enabled)
   134	                    HStack {
   135	                        Button("检查推送目标") {
   136	                            let draft = ArchiveRemote(remote: remoteName, branch: remoteBranch), path = model.settings.archivePath
   137	                            Task { do {
   138	                                remotePreview = try await Task.detached { try ArchiveSync.preview(root: URL(fileURLWithPath: path), remote: draft.remote, branch: draft.branch) }.value
   139	                                checkedRemote = draft
   140	                            } catch { checkedRemote = nil; model.error = error.localizedDescription } }
   141	                        }.disabled(model.settings.archivePath.isEmpty)
   142	                        Button("保存并启用自动推送") { model.settings.archiveRemote = ArchiveRemote(remote: remoteName, branch: remoteBranch); model.persistSettings(); Task { await model.archiveNow() } }.disabled(checkedRemote != ArchiveRemote(remote: remoteName, branch: remoteBranch))
   143	                        if model.settings.archiveRemote != nil { Button("停用推送") { model.settings.archiveRemote = nil; model.persistSettings(); model.syncStatus = "未启用远端推送" }; Button("立即重试") { Task { await model.archiveNow() } } }
   144	                    }
   145	                }
   146	            }
   147	            Card {
   148	                VStack(alignment: .leading, spacing: 12) {
   149	                    Text("独立后台服务").font(.headline)
   150	                    Text("当前用户登录期间持续扫描、归档和推送，退出 Ragdoll 后继续运行。后台不执行交互对话。").font(.caption).foregroundStyle(.secondary)
   151	                    Text(model.backgroundStatus).font(.caption)
   152	                    HStack {
   153	                        Button(model.settings.backgroundEnabled == true ? "停用后台服务" : "启用后台服务") { Task { await model.setBackground(model.settings.backgroundEnabled != true) } }
   154	                        Button("打开系统登录项") { SMAppService.openSystemSettingsLoginItems() }
   155	                    }
   156	                }
   157	            }
   158	            Card {
   159	                VStack(alignment: .leading, spacing: 12) {
   160	                    Text("排除项目").font(.headline)
   161	                    Text("取消选择的项目仍可浏览和统计，其后续变化不写入归档；已有归档不会删除。").font(.caption).foregroundStyle(.secondary)
   162	                    ForEach(model.projects, id: \.self) { project in
   163	                        Toggle(project, isOn: Binding(get: { !model.settings.excludedProjects.contains(project) }, set: { include in
   164	                            model.settings.excludedProjects.removeAll { $0 == project }; if !include { model.settings.excludedProjects.append(project) }; model.persistSettings()
   165	                        })).toggleStyle(.checkbox).font(.caption)
   166	                    }
   167	                }
   168	            }
   169	        }
   170	    }
   171	    var pricing: some View {
   172	        Card {
   173	            VStack(alignment: .leading, spacing: 14) {

logs
    48	}
    49	
    50	function usage(id: string, time: number, model: string, v: Data, inclusive: boolean): Usage {
    51	  const cacheRead = number(v.cached_input_tokens ?? v.cache_read_input_tokens ?? v.cacheReadTokens);
    52	  const cacheWrite = number(v.cache_creation_input_tokens ?? v.cache_write_input_tokens ?? v.cacheWriteTokens);
    53	  return {
    54	    id, time, model,
    55	    input: Math.max(0, number(v.input_tokens ?? v.inputTokens) - (inclusive ? cacheRead + cacheWrite : 0)),
    56	    output: number(v.output_tokens ?? v.outputTokens), cacheRead,
    57	    cacheWrite,
    58	  };
    59	}
    60	
    61	export async function parseFile(source: Location['source'], path: string, home = dirname(path)): Promise<Session> {
    62	  const file = await stat(path);
    63	  const session: Session = {
    64	    id: '', nativeID: basename(path).replace(/\.jsonl(?:\.(?:zstd|zst))?$/, ''), source, home,
    65	    title: '', project: '', created: file.birthtimeMs, updated: file.mtimeMs,
    66	    messages: [], usage: [], files: [path], warnings: [],
    67	  };
    68	  const messages = new Map<string, Session['messages'][number]>();
    69	  const counted = new Map<string, Usage>();
    70	  const canonical = new Map<string, Usage>();
    71	  let model = '', inherited = false, seedLength = 0, line = 0;
    72	  let previous: Data = {};
    73	  let firstTime = Number.POSITIVE_INFINITY, lastTime = 0;
    74	  for await (const e of records(path, session.warnings)) {
    75	    line++;
    76	    const p = object(e.payload), d = object(e.data), m = object(e.message);
    77	    const time = timestamp(e.timestamp ?? e.time);
    78	    if (time) { firstTime = Math.min(firstTime, time); lastTime = Math.max(lastTime, time); }
    79	    const addMessage = (role: string, text: string, id = string(e.uuid ?? e.seq, String(line)), kind = 'text') => {
    80	      if (!text) return;
    81	      messages.set(id, { id, role, text, time: time || file.mtimeMs, kind });
    82	      if (!session.title && role === 'user') session.title = text.replace(/\s+/g, ' ').slice(0, 100);
    83	    };
    84	    if (source === 'codex') {
    85	      if (e.type === 'session_meta') {
    86	        session.nativeID = string(p.id ?? p.session_id, session.nativeID);
    87	        session.project = string(p.cwd, session.project);
    88	        session.parentID = string(p.forked_from_id) || undefined;
    89	      }
    90	      if (e.type === 'turn_context') { model = string(p.model, model); session.project ||= string(p.cwd); }
    91	      if (e.type === 'token_usage_record') {
    92	        const id = string(p.response_id, String(line));
    93	        canonical.set(id, usage(id, time, model, object(p.usage), true));
    94	      }
    95	      if (e.type === 'event_msg' && p.type === 'token_count') {
    96	        const info = object(p.info), total = object(info.total_token_usage);
    97	        const current = object(info.last_token_usage);
    98	        const key = JSON.stringify(total);
    99	        if (Object.keys(total).length && !counted.has(key)) {
   100	          const delta: Data = {};
   101	          for (const k of ['input_tokens', 'output_tokens', 'cached_input_tokens', 'cache_write_input_tokens']) delta[k] = Math.max(0, number(total[k]) - number(previous[k]));
   102	          counted.set(key, usage(key, time, model, Object.keys(previous).length ? delta : current, true));
   103	          previous = total;
   104	        }
   105	      }
   106	      if (e.type === 'resp…2039 tokens truncated…ait setBackground(true) }
    87	            await refresh()
    88	            Task { [weak self] in
    89	                while !Task.isCancelled {
    90	                    try? await Task.sleep(for: .seconds(2)); guard let self else { return }
    91	                    self.pollBackground()
    92	                    if !BackgroundService.isRunning(root: self.root), Date().timeIntervalSince(self.lastRefresh) >= 60 { await self.refresh() }
    93	                    if self.settings.archiveRemote != nil, !BackgroundService.isRunning(root: self.root), !self.archiving, FileManager.default.fileExists(atPath: self.root.appendingPathComponent("sync-pending").path), Date().timeIntervalSince(self.lastPushAttempt) >= 60 { await self.archiveNow() }
    94	                }
    95	            }
    96	        } catch { self.error = error.localizedDescription; status = "启动失败" }
    97	    }
    98	    func receive(_ event: String, _ data: JSONValue) {
    99	        do {
   100	            switch event {
   101	            case "session":
   102	                let session = try data.decode(Session.self)
   103	                if try store?.save(session) == true {
   104	                    if selectedID == session.id { selected = session }
   105	                    scheduleReload(); scheduleArchive()
   106	                }
   107	            case "delta":
   108	                if data["conversationID"].string == selectedID, let message = try? data["message"].decode(Message.self) {
   109	                    if let index = selected?.messages.firstIndex(where: { $0.id == message.id }) { selected?.messages[index] = message }
   110	                    else { selected?.messages.append(message) }
   111	                }
   112	            case "state":
   113	                let id = data["conversationID"].string
   114	                if data["state"].string == "running" { running.insert(id) } else { running.remove(id) }
   115	                if !data["message"].string.isEmpty { error = data["message"].string }
   116	                if data["state"].string == "idle" { Task { await refresh() } }
   117	            case "chat":
   118	                let id = data["conversationID"].string
   119	                var events = toolEvents[id] ?? []; events.append(data)
   120	                toolEvents[id] = Array(events.suffix(100))
   121	            case "approval": approvals.append(Approval(id: data["requestID"].string, method: data["method"].string, params: data["params"]))
   122	            case "approvalCancelled": approvals.removeAll { $0.id == data["requestID"].string }
   123	            case "sourceChanged": if !scanning { Task { await refresh() } }
   124	            case "warning": warnings.append(data.string); warnings = Array(warnings.suffix(100))
   125	            case "agentEvent":
   126	                let text = data.text
   127	                warnings.append(text)
   128	                collectLoginLinks(data)
   129	            case "agentConfiguration":
   130	                let id = data["conversationID"].string.isEmpty ? selectedID ?? "" : data["conversationID"].string
   131	                var info = (conversationInfo[id] ?? .object([:])).dictionary
   132	                let update = data["update"]
   133	                if update["configOptions"] != .null { info["configOptions"] = update["configOptions"] }
   134	                if update["availableCommands"] != .null { info["availableCommands"] = update["availableCommands"] }
   135	                conversationInfo[id] = .object(info)
   136	            case "disconnected": ready = false; running.removeAll(); error = data.string
   137	            default: break
   138	            }
   139	        } catch { self.error = error.localizedDescription }
   140	    }
   141	    func refresh() async {
   142	        guard ready, !scanning, !archiving else { return }
   143	        if BackgroundService.isRunning(root: root) {
   144	            do { try BackgroundService.request(root: root); pollBackground() } catch { self.error = error.localizedDescription }
   145	            return
   146	        }
   147	        scanning = true; status = "正在读取会话…"
   148	        lastRefresh = Date()
   149	        do {
   150	            let lease = try ServiceLease(root: root)
   151	            defer { withExtendedLifetime(lease) {} }
   152	            let result = try await bridge.request("scan", ["locations": try .encode(settings.locations)], timeout: 600)
   153	            try reload(); status = "索引已更新 · 本次处理 \(result["count"].text) 个变更会话"
   154	        } catch { self.error = error.localizedDescription; status = "扫描失败，可重试" }
   155	        scanning = false; scheduleArchive(markDirty: false)
   156	    }
   157	    private func scheduleReload() {
   158	        guard reloadTask == nil else { return }
   159	        reloadTask = Task { try? await Task.sleep(for: .milliseconds(300)); do { try reload() } catch { self.error = error.localizedDescription }; reloadTask = nil }
   160	    }
   161	    func reload() throws { sessions = try store?.list(query: query) ?? [] }
   162	    func select(_ id: String?) {
   163	        selectedID = id
   164	        do { selected = try id.flatMap { try store?.session($0) } }
   165	        catch { self.error = error.localizedDescription }
   166	    }
   167	    func saveSettings() throws { try store?.saveSettings(settings) }
   168	    func persistSettings() { do { try saveSettings() } catch { self.error = error.localizedDescription } }
   249	            else { await probe(agent) }
   250	        } catch { self.error = error.localizedDescription }
   251	    }
   252	    func importDesktop() {
   253	        let panel = NSOpenPanel(); panel.allowedContentTypes = [.zip, .json]; panel.allowsMultipleSelection = false
   254	        guard panel.runModal() == .OK, let url = panel.url else { return }
   255	        Task { do { _ = try await bridge.request("import", ["path": .string(url.path)]); try reload(); scheduleArchive() } catch { self.error = error.localizedDescription } }
   256	    }
   257	    func chooseArchive() {
   258	        let panel = NSOpenPanel(); panel.canChooseDirectories = true; panel.canChooseFiles = false; panel.canCreateDirectories = true; panel.prompt = "选择归档仓库"
   259	        guard panel.runModal() == .OK, let url = panel.url else { return }
   260	        if settings.archivePath != url.path { settings.archiveRemote = nil; syncStatus = "未启用远端推送" }
   261	        settings.archivePath = url.path; persistSettings(); scheduleArchive(); Task { await archiveNow() }
   262	    }
   263	    func chooseProject() -> String? {
   264	        let panel = NSOpenPanel(); panel.canChooseDirectories = true; panel.canChooseFiles = false; panel.prompt = "选择项目"
   265	        return panel.runModal() == .OK ? panel.url?.path : nil
   266	    }
   267	    func chooseAttachments() -> [URL] {
   268	        let panel = NSOpenPanel(); panel.canChooseDirectories = false; panel.allowsMultipleSelection = true
   269	        return panel.runModal() == .OK ? panel.urls : []
   270	    }
   271	    private func scheduleArchive(markDirty: Bool = true) {
   272	        if !scanning && !archiving && BackgroundService.isRunning(root: root) { archiveTask?.cancel(); return }
   273	        guard !settings.archivePath.isEmpty else { return }
   274	        if markDirty { dirtySince = dirtySince ?? Date(); dirtyGeneration += 1 }
   275	        guard dirtySince != nil else { return }
   276	        guard !scanning else { return }
   277	        archiveTask?.cancel()
   278	        let delay = max(0, min(30, 300 - Date().timeIntervalSince(dirtySince!)))
   279	        archiveTask = Task { do { try await Task.sleep(for: .seconds(delay)); await archiveNow() } catch {} }
   280	    }
   281	    func archiveNow() async {
   282	        guard let store, !settings.archivePath.isEmpty, !archiving, !scanning else { return }
   283	        if BackgroundService.isRunning(root: root) {
   284	            do { try BackgroundService.request(root: root); archiveStatus = "已请求后台归档" } catch { self.error = error.localizedDescription }
   285	            return
   286	        }
   287	        archiving = true; archiveStatus = "正在保存并提交…"
   288	        let generation = dirtyGeneration
   289	        let path = settings.archivePath, excluded = settings.excludedProjects, roots = settings.locations.map(\.path)
   290	        do {
   291	            let lease = try ServiceLease(root: root)
   292	            defer { withExtendedLifetime(lease) {} }
   293	            let result = try await Task.detached(priority: .utility) {
   294	                let sessions = try store.list().filter { !excluded.contains($0.project) }.compactMap { try store.session($0.id) }
   295	                return try Archive.save(sessions, to: URL(fileURLWithPath: path), sourceRoots: roots)
   296	            }.value
   297	            archiveStatus = result.commit.map { "已保存并提交 · \($0) · \(result.files) 个文件" } ?? "归档已是最新，无需提交"
   298	            lastArchive = Date(); if generation == dirtyGeneration { dirtySince = nil }
   299	            if let remote = settings.archiveRemote {
   300	                try Data("pending".utf8).write(to: root.appendingPathComponent("sync-pending"), options: .atomic)
   301	                lastPushAttempt = Date(); syncStatus = "正在推送"
   302	                do {
   303	                    _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: path), remote: remote.remote, branch: remote.branch) }.value
   304	                    try FileManager.default.removeItem(at: root.appendingPathComponent("sync-pending"))
   305	                    syncStatus = "已推送到 \(remote.remote)/\(remote.branch)"
   306	                } catch { syncStatus = "推送待重试：\(error.localizedDescription)" }
   307	            } else { syncStatus = "未启用远端推送" }
   308	        } catch { archiveStatus = "归档未完成：\(error.localizedDescription)"; self.error = error.localizedDescription }
   309	        archiving = false
   310	        if generation != dirtyGeneration { scheduleArchive(markDirty: false) }
   311	    }
   312	    private var lastPushAttempt = Date.distantPast
   313	    func pollBackground() {
   314	        guard !scanning, !archiving else { return }
   315	        do {
   316	            let running = BackgroundService.isRunning(root: root)
   317	            if running, let state = try BackgroundService.status(root: root) {
   318	                backgroundStatus = "后台服务正在运行 · PID \(state.pid)"
   319	                status = state.scan; archiveStatus = state.archive; syncStatus = state.sync; lastArchive = state.lastArchive
   320	                try reload()
   321	                if let id = selectedID { selected = try store?.session(id) }
   322	            } else {
   323	                let service = SMAppService.agent(plistName: "com.oyamameek.ragdoll.service.plist")
   324	                backgroundStatus = service.status == .requiresApproval ? "请在系统登录项中允许后台服务" : settings.backgroundEnabled == true ? "后台服务尚未运行" : "未启用后台服务"
   325	            }
   326	        } catch { self.error = error.localizedDescription }
   327	    }
   328	    func setBackground(_ enabled: Bool) async {
   329	        guard Bundle.main.bundleURL.pathExtension == "app" else { error = "后台服务需要运行打包后的 Ragdoll.app"; return }
   330	        let service = SMAppService.agent(plistName: "com.oyamameek.ragdoll.service.plist")
   331	        do {
   332	            while scanning || archiving { try await Task.sleep(for: .milliseconds(100)) }
   333	            settings.backgroundEnabled = enabled; try saveSettings()
   334	            if enabled {
   335	                archiveTask?.cancel()
   336	                if service.status != .enabled { try service.register() }
   337	            } else { try await service.unregister() }
   338	            pollBackground()
   339	        } catch { self.error = error.localizedDescription; pollBackground() }
   340	    }
   341	    func migrateSelected(agent: AgentConfig, cwd: String) async -> Bool {
   342	        guard let session = selected else { return false }
   343	        do {
   344	            let config = try hydrated(agent)
   345	            let key = agent.kind == "codex" ? "CODEX_HOME" : agent.kind == "claude" ? "CLAUDE_CONFIG_DIR" : "DSH_HOME"
   346	            guard let home = config.env[key] ?? settings.locations.first(where: { $0.source == agent.kind })?.path else { throw NSError(domain: "Ragdoll.Migration", code: 1, userInfo: [NSLocalizedDescriptionKey: "请先设置目标工具的历史目录"]) }
   347	            let result = try await bridge.request("migrate", ["session": try .encode(session), "target": try .encode(config), "home": .string(home), "cwd": .string(cwd)], timeout: 600)
   348	            let migrated = try result["session"].decode(Session.self)
   349	            _ = try store?.save(migrated); try reload(); select(migrated.id); scheduleArchive()
   350	            return true
   351	        } catch { self.error = error.localizedDescription; return false }
   352	    }
   353	    func openDesktop(_ session: Session) { if let url = URL(string: "https://claude.ai/chat/\(session.nativeID)") { NSWorkspace.shared.open(url) } }
   354	    private func collectLoginLinks(_ value: JSONValue) {

hist
diff --git a/Sources/RagdollCore/Models.swift b/Sources/RagdollCore/Models.swift
index 837d1d6..e5e303f 100644
--- a/Sources/RagdollCore/Models.swift
+++ b/Sources/RagdollCore/Models.swift
@@ -40,6 +40,7 @@ public struct Session: Codable, Identifiable, Sendable, Equatable {
     public var nativeSource: String?
     public var canonicalID: String?
     public var nativeStarted: Bool?
+    public var migration: MigrationOrigin?
     public var messages: [Message]
     public var usage: [Usage]
     public var files: [String]
@@ -89,10 +90,28 @@ public struct Price: Codable, Sendable, Equatable {
     }
 }
 
+public struct MigrationOrigin: Codable, Sendable, Equatable {
+    public var sourceID: String
+    public var source: String
+    public var sourceNativeID: String
+    public var created: Double
+    public init(sourceID: String, source: String, sourceNativeID: String, created: Double) {
+        self.sourceID = sourceID; self.source = source; self.sourceNativeID = sourceNativeID; self.created = created
+    }
+}
+
+public struct ArchiveRemote: Codable, Sendable, Equatable {
+    public var remote: String
+    public var branch: String
+    public init(remote: String = "origin", branch: String = "main") { self.remote = remote; self.branch = branch }
+}
+
 public struct Settings: Codable, Sendable {
     public var locations: [Location] = []
     public var agents: [AgentConfig] = []
     public var archivePath = ""
+    public var archiveRemote: ArchiveRemote?
+    public var backgroundEnabled: Bool?
     public var excludedProjects: [String] = []
     public var weeklyBudget: Double?
     public var prices: [String: Price] = [
diff --git a/Sources/RagdollCore/Store.swift b/Sources/RagdollCore/Store.swift
index f3152e7..2633f84 100644
--- a/Sources/RagdollCore/Store.swift
+++ b/Sources/RagdollCore/Store.swift
@@ -4,7 +4,8 @@ import GRDB
 public final class Store: Sendable {
     private let db: DatabaseQueue
     public init(path: String) throws {
-        db = try DatabaseQueue(path: path)
+        var configuration = Configuration(); configuration.busyMode = .timeout(10)
+        db = try DatabaseQueue(path: path, configuration: configuration)
         try db.write { db in
             try db.execute(sql: "CREATE TABLE IF NOT EXISTS sessions (id TEXT PRIMARY KEY, source TEXT NOT NULL, native_id TEXT NOT NULL, title TEXT NOT NULL, project TEXT NOT NULL, updated REAL NOT NULL, body BLOB NOT NULL, summary BLOB NOT NULL, search TEXT NOT NULL)")
             try db.execute(sql: "CREATE INDEX IF NOT EXISTS sessions_updated ON sessions(updated DESC)")
@@ -21,6 +22,7 @@ public final class Store: Sendable {
                 let previous = try JSONDecoder().decode(Session.self, from: existing)
                 session.files = Array(Set(previous.files + session.files)).sorted()
                 session.instanceID = session.instanceID ?? previous.instanceID
+                session.migration = session.migration ?? previous.migration
             }
             if let nativeSource = session.nativeSource {
                 let candidates = try Data.fetchAll(db, sql: "SELECT body FROM sessions WHERE source=? AND native_id=?", arguments: [nativeSource, session.nativeID]).map { try JSONDecoder().decode(Session.self, from: $0) }.filter { $0.home == session.home }
@@ -68,4 +70,5 @@ public final class Store: Sendable {
         let data = try JSONEncoder().encode(settings)
         try db.write { db in try db.execute(sql: "INSERT INTO settings(id,body) VALUES(1,?) ON CONFLICT(id) DO UPDATE SET body=excluded.body", arguments: [data]) }
     }
+    public func dataVersion() throws -> Int { try db.read { try Int.fetchOne($0, sql: "PRAGMA data_version") ?? 0 } }
 }
diff --git a/runtime/src/agents.ts b/runtime/src/agents.ts
index 3537a84..e231028 100644
--- a/runtime/src/agents.ts
+++ b/runtime/src/agents.ts
@@ -40,6 +40,7 @@ interface AcpApp {
 interface Running {
   session: Session; agent: AgentConfig; busy: boolean; rpc?: RpcProcess; peer?: AcpPeer; claude?: Query;
   turnID?: string; finish?: () => void; tools?: ClientTools; deltaID?: string; replaying?: boolean;
+  failure?: Error;
   fail?: (error: Error) => void; importing?: boolean; hasActivity?: boolean; writeQueue?: Promise<void>;
 }
 
@@ -199,6 +200,8 @@ export class Agents {
     }
     if (method === 'session.event') {
       const e = object(params.event), d = object(e.data), message = object(d.message);
+      const reason = object(d.reason);
+      if (e.type === 'turn/end' && reason.kind === 'error') r.failure = new Error(string(object(reason.error).message, 'dsh 对话执行失败'));
       if (e.type === 'assistant/delta') this.delta(r, string(d.text ?? d.delta));
       if (e.type === 'assistant/message') {
         const text = content(message.content ?? d.content);
@@ -357,7 +360,7 @@ export class Agents {
     }
     const visibleText = text + (files.length ? '\n\n' + files.map(f => `[附件：${basename(f.path)}](${pathToFileURL(f.path).href})`).join('\n') : '');
     const withPaths = text + (files.some(f => !f.mime) ? '\n\n附件路径：\n' + files.filter(f => !f.mime).map(f => f.path).join('\n') : '');
-    r.busy = true; r.deltaID = undefined; r.hasActivity = false;
+    r.busy = true; r.deltaID = undefined; r.hasActivity = false; r.failure = undefined;
     r.session.files = [...new Set([...r.session.files, ...files.map(f => f.path)])];
     r.session.messages.push({ id: randomUUID(), role: 'user', text: visibleText, time: Date.now(), kind: 'text' });
     if (r.session.title === '新对话') r.session.title = text.slice(0, 80);
@@ -376,6 +379,7 @@ export class Agents {
       } else if (r.agent.kind === 'dsh') {
         await r.rpc!.request('session/prompt', { sessionId: r.session.nativeID, contentBlocks: [{ type: 'text', text: withPaths }, ...files.filter(f => f.mime).map(f => ({ type: 'image', data: f.data, mimeType: f.mime }))] });
         await r.rpc!.request('session/wait', { sessionId: r.session.nativeID }, 0);
+        if (r.failure) throw r.failure;
       } else {
         const resumed = r.session.nativeStarted === true;
         const images = files.filter((f): f is typeof f & { mime: 'image/png' | 'image/jpeg' | 'image/webp' | 'image/gif'; data: string } => f.mime !== undefined && f.data !== undefined);


## tool · 2026-11-17T00:36:06Z


Script completed
Wall time 0.1 seconds
Output:

rpc
     1	import { spawn } from 'node:child_process';
     2	import type { ChildProcessWithoutNullStreams } from 'node:child_process';
     3	import { createInterface } from 'node:readline';
     4	import { object, string } from './types.ts';
     5	import type { Data } from './types.ts';
     6	
     7	export function childEnvironment(env: Record<string, string> = {}): NodeJS.ProcessEnv {
     8	  const result: NodeJS.ProcessEnv = { ...process.env, PATH: `${process.env.PATH || ''}:/opt/homebrew/bin:/usr/local/bin`, ...env };
     9	  delete result.ELECTRON_RUN_AS_NODE;
    10	  return result;
    11	}
    12	
    13	export class RpcProcess {
    14	  readonly child: ChildProcessWithoutNullStreams;
    15	  private serial = 0;
    16	  private pending = new Map<string, { resolve: (v: unknown) => void; reject: (e: Error) => void; timer?: NodeJS.Timeout }>();
    17	  private stderr = '';
    18	  onNotification: (method: string, params: Data) => void = () => {};
    19	  onRequest: (method: string, params: Data) => Promise<unknown> = async method => { throw new Error(`不支持代理请求：${method}`); };
    20	  onExit: (message: string) => void = () => {};
    21	  private stopped = false;
    22	
    23	  constructor(command: string, args: string[], cwd: string, env: Record<string, string> = {}) {
    24	    if (!command || command.includes('\0')) throw new Error('请设置有效程序路径');
    25	    this.child = spawn(command, args, { cwd, env: childEnvironment(env), stdio: 'pipe', detached: true });
    26	    this.child.stderr.on('data', data => { this.stderr = (this.stderr + String(data)).slice(-4000); });
    27	    this.child.on('error', error => this.fail(error));
    28	    this.child.on('exit', (code, signal) => {
    29	      this.fail(new Error(`代理进程已退出 (${code ?? signal})：${this.stderr}`));
    30	      if (!this.stopped) this.onExit(`代理进程已退出 (${code ?? signal})`);
    31	    });
    32	    const input = createInterface({ input: this.child.stdout });
    33	    input.on('line', line => {
    34	      let message: Data;
    35	      try { message = object(JSON.parse(line)); }
    36	      catch { this.fail(new Error('代理 stdout 包含无效 JSON-RPC 数据')); void this.close(); return; }
    37	      if ('method' in message) {
    38	        if ('id' in message) {
    39	          void this.onRequest(string(message.method), object(message.params)).then(
    40	            result => this.write({ jsonrpc: '2.0', id: message.id, result }),
    41	            error => this.write({ jsonrpc: '2.0', id: message.id, error: { code: -32603, message: String(error) } }),
    42	          );
    43	        } else this.onNotification(string(message.method), object(message.params));
    44	      } else if ('id' in message) {
    45	        const key = String(message.id), pending = this.pending.get(key);
    46	        if (!pending) return;
    47	        this.pending.delete(key); clearTimeout(pending.timer);
    48	        if (message.error) pending.reject(new Error(JSON.stringify(message.error)));
    49	        else pending.resolve(message.result);
    50	      }
    51	    });
    52	  }
    53	  private write(message: unknown): void {
    54	    if (this.child.stdin.destroyed) return;
    55	    this.child.stdin.write(JSON.stringify(message) + '\n');
    56	  }
    57	  request(method: string, params: unknown = {}, timeout = 30000): Promise<unknown> {
    58	    if (this.stopped) return Promise.reject(new Error('代理进程已经停止'));
    59	    const id = ++this.serial;
    60	    return new Promise((resolve, reject) => {
    61	      const timer = timeout > 0 ? setTimeout(() => { this.pending.delete(String(id)); reject(new Error(`代理请求超时：${method}`)); }, timeout) : undefined;
    62	      this.pending.set(String(id), { resolve, reject, timer });
    63	      this.write({ jsonrpc: '2.0', id, method, params });
    64	    });
    65	  }
    66	  notify(method: string, params: unknown = {}): void { this.write({ jsonrpc: '2.0', method, params }); }
    67	  private fail(error: Error): void {
    68	    for (const pending of this.pending.values()) { clearTimeout(pending.timer); pending.reject(error); }
    69	    this.pending.clear();
    70	  }
    71	  async close(): Promise<void> {
    72	    if (this.stopped) return;
    73	    this.stopped = true; this.child.stdin.end();
    74	    const pid = this.child.pid;
    75	    if (pid && this.child.exitCode === null && this.child.signalCode === null) {
    76	      try { process.kill(-pid, 'SIGTERM'); } catch { /* 进程已经退出。 */ }
    77	      const timer = setTimeout(() => { try { process.kill(-pid, 'SIGKILL'); } catch { /* 进程已经退出。 */ } }, 3000);
    78	      timer.unref();
    79	      await new Promise<void>(resolve => { if (this.child.exitCode !== null || this.child.signalCode !== null) resolve(); else this.child.once('exit', () => resolve()); });
    80	      clearTimeout(timer);
    81	    }
    82	    this.fail(new Error('执行已停止'));
    83	  }
    84	}

agents
   236	      try {
   237	        const info = object(await rpc.request('initialize', { clientInfo: { name: 'ragdoll', version: '0.1.0' }, capabilities: { experimentalApi: true } }));
   238	        rpc.notify('initialized');
   239	        const models = await rpc.request('model/list', {});
   240	        return { ...info, models };
   241	      } finally { await rpc.close(); }
   242	    }
   243	    if (agent.kind === 'dsh') {
   244	      const rpc = new RpcProcess(agent.command, agent.args, cwd, agent.env);
   245	      try { return object(await rpc.request('initialize', { cwd, provider: 'deepseek-official', model: 'deepseek-v4-flash', maxTokens: 32768, approvalRequests: true })); }
   246	      finally { await rpc.close(); }
   247	    }
   248	    const result = await promisify(execFile)(agent.command, ['--version'], { cwd, env: childEnvironment(agent.env), timeout: 15000 });
   249	    return { name: 'Claude Code', version: result.stdout.trim() };
   250	  }
   251	
   252	  async start(value: Data): Promise<Data> {
   253	    const agent = validateConfig(value.agent), cwd = string(value.cwd, homedir());
   254	    await access(cwd);
   255	    const prior = value.session ? object(value.session) as unknown as Session : undefined;
   256	    if (prior && this.running.has(prior.id)) return { session: this.running.get(prior.id)!.session };
   257	    if (prior && prior.source !== 'acp' && prior.source !== agent.kind) throw new Error('此历史会话必须使用原始工具恢复');
   258	    if (prior?.instanceID && prior.instanceID !== agent.id) throw new Error('此会话属于其他 Agent 实例');
   259	    const homeKey = agent.kind === 'codex' ? 'CODEX_HOME' : agent.kind === 'claude' ? 'CLAUDE_CONFIG_DIR' : 'DSH_HOME';
   260	    const home = prior?.home || agent.env[homeKey] || defaultLocations().find(l => l.source === agent.kind)?.path || '';
   261	    if (agent.kind !== 'acp' && home) agent.env = { ...agent.env, [homeKey]: home };
   262	    const session: Session = prior ? structuredClone(prior) : {
   263	      id: `chat:${randomUUID()}`, nativeID: '', source: agent.kind, instanceID: agent.id,
   264	      title: '新对话', project: cwd, home, created: Date.now(), updated: Date.now(), messages: [], usage: [], files: [], warnings: [],
   265	    };
   266	    const r: Running = { session, agent, busy: false };
   267	    let info: Data = {};
   268	    if (agent.kind === 'codex') {
   269	      const rpc = new RpcProcess(agent.command, [...agent.args, 'app-server'], cwd, agent.env); r.rpc = rpc;
   270	      rpc.onNotification = (m, p) => this.update(r, m, p);
   271	      rpc.onExit = message => r.fail?.(new Error(message));
   272	      rpc.onRequest = async (method, params) => {
   273	        const answer = await this.ask(method, { ...params, conversationID: session.id });
   274	        if (method.includes('requestUserInput')) return { answers: answer.answers ?? {} };
   275	        return { decision: answer.allowed === true ? 'accept' : 'decline' };
   276	      };
   277	      try {
   278	        await rpc.request('initialize', { clientInfo: { name: 'ragdoll', version: '0.1.0' }, capabilities: { experimentalApi: true } }); rpc.notify('initialized');
   279	        info = object(await rpc.request(prior ? 'thread/resume' : 'thread/start', { ...(prior ? { threadId: prior.nativeID } : {}), cwd, approvalPolicy: 'on-request', sandbox: 'workspace-write', ...(value.model ? { model: value.model } : {}) }));
   280	        info = { ...info, models: await rpc.request('model/list', {}) };
   281	        const catalog = object(info.models).data;
   282	        if (!value.model && typeof info.model === 'string' && Array.isArray(catalog) && !catalog.some(m => object(m).model === info.model)) session.warnings.push('当前配置模型未出现在工具的可用目录中，请从模型菜单选择可用模型后发送。');
   283	        const id = string(object(info.thread).id);
   284	        if (!id) throw new Error('Codex 返回的会话缺少 ID');
   285	        session.nativeID = id;
   286	      } catch (error) { await rpc.close(); throw error; }
   287	    }
   288	    if (agent.kind === 'dsh') {
   289	      const rpc = new RpcProcess(agent.command, agent.args, cwd, agent.env); r.rpc = rpc;
   290	      rpc.onNotification = (m, p) => this.update(r, m, p);
   291	      rpc.onExit = message => r.fail?.(new Error(message));
   292	      rpc.onRequest = async (method, params) => {
   293	        const answer = await this.ask(method, { ...params, conversationID: session.id });
   294	        if (method === 'approval/request') return { outcome: answer.allowed === true ? 'allowed-once' : 'rejected' };
   295	        return answer.allowed === true ? { answers: answer.answers ?? [] } : { cancelled: true };
   296	      };
   297	      try {
   298	        info = object(await rpc.request('initialize', { cwd, provider: session.provider || 'deepseek-official', model: string(value.model, session.usage.at(-1)?.model || 'deepseek-v4-flash'), maxTokens: 32768, approvalRequests: true, capabilities: { userQuestions: true } }));
   299	        session.nativeID ||= randomUUID();
   300	        if (prior) await rpc.request('session/resume', { sessionId: session.nativeID });
   301	      } catch (error) { await rpc.close(); throw error; }
   302	    }
   303	    if (agent.kind === 'acp') {
   304	      const ask: Ask = (m, p, signal) => { if (r.busy) r.hasActivity = true; return this.ask(m, { ...p, conversationID: session.id }, signal); };
   305	      r.tools = new ClientTools(cwd, ask);
   306	      const peer = await openAcp(agent, cwd, ask, (m, p) => this.update(r, m, p), r.tools); r.peer = peer;
   307	      try {
   308	        if (prior) {
   309	          const capabilities = object(peer.info.agentCapabilities ?? peer.info.capabilities);
   310	          const sessions = object(capabilities.session ?? capabilities.sessionCapabilities);
   311	          if (peer.version === 2 ? capabilities.session == null : capabilities.loadSession !== true && !sessions.resume) throw new Error('此 ACP Agent 未声明历史恢复能力；已保存的会话仍可浏览和归档');
   312	          r.replaying = true;
   313	          r.importing = prior.messages.length === 0;
   314	          info = object(await peer.request(peer.version === 1 && capabilities.loadSession === true ? 'session/load' : 'session/resume', { sessionId: prior.nativeID, cwd, mcpServers: [], ...(peer.version === 2 && r.importing ? { replayFrom: { type: 'start' } } : {}) }));
   315	          r.replaying = false;
   316	          r.importing = false;
   317	        } else {
   318	          info = object(await peer.request('session/new', { cwd, mcpServers: [] }));
   319	          session.nativeID = string(info.sessionId);
   320	          if (!session.nativeID) throw new Error('ACP Agent 返回的会话缺少 ID');
   321	        }
   322	      } catch (error) { await peer.close(); await r.tools.close(); throw error; }
   323	      info = { ...peer.info, ...info, protocolVersion: peer.version };
   324	    }
   325	    if (agent.kind === 'claude') { session.nativeID ||= randomUUID(); session.nativeStarted = prior ? prior.nativeStarted ?? true : false; }
   326	    if (!prior) session.id = sessionKey(agent.kind, `${agent.kind === 'acp' ? agent.id : home}\0${session.nativeID}`);
   327	    if (agent.kind === 'acp') {
   330	        session.nativeSource = nativeSource;
   331	        const key = nativeSource === 'codex' ? 'CODEX_HOME' : nativeSource === 'claude' ? 'CLAUDE_CONFIG_DIR' : 'DSH_HOME';
   332	        session.home = agent.env[key] || defaultLocations().find(l => l.source === nativeSource)?.path || '';
   333	      }
   334	    }
   335	    session.instanceID = agent.id;
   336	    this.running.set(session.id, r);
   337	    await this.persist(r);
   338	    return { session, info };
   339	  }
   340	
   341	  async send(id: string, text: string, model?: string, attachments: unknown = []): Promise<void> {
   342	    const r = this.running.get(id);
   343	    if (!r) throw new Error('请先打开或恢复会话');
   344	    if (r.busy) throw new Error('此会话正在执行，请等待或停止当前执行');
   345	    if (!text.trim()) throw new Error('消息不能为空');
   346	    if (!Array.isArray(attachments) || attachments.some(p => typeof p !== 'string')) throw new Error('附件列表无效');
   347	    const files = await Promise.all((attachments as string[]).map(async path => {
   348	      const mime = ({ '.png': 'image/png', '.jpg': 'image/jpeg', '.jpeg': 'image/jpeg', '.webp': 'image/webp', '.gif': 'image/gif' } as Record<string, 'image/png' | 'image/jpeg' | 'image/webp' | 'image/gif'>)[extname(path).toLowerCase()];
   349	      if (mime) {
   350	        const data = await readFile(path);
   351	        if (data.length > 20 * 1024 * 1024) throw new Error('单张图片不能超过 20 MiB');
   352	        return { path, mime, data: data.toString('base64') };
   353	      }
   354	      await access(path); return { path, mime: undefined, data: undefined };
   355	    }));
   356	    if (r.peer && files.some(f => f.mime)) {
   357	      const capabilities = object(r.peer.info.agentCapabilities ?? r.peer.info.capabilities);
   358	      const prompts = object(r.peer.version === 2 ? object(capabilities.session).prompt : capabilities.promptCapabilities);
   359	      if (prompts.image !== true) throw new Error('此 ACP Agent 未声明图片输入能力');
   360	    }
   361	    const visibleText = text + (files.length ? '\n\n' + files.map(f => `[附件：${basename(f.path)}](${pathToFileURL(f.path).href})`).join('\n') : '');
   362	    const withPaths = text + (files.some(f => !f.mime) ? '\n\n附件路径：\n' + files.filter(f => !f.mime).map(f => f.path).join('\n') : '');
   363	    r.busy = true; r.deltaID = undefined; r.hasActivity = false; r.failure = undefined;
   364	    r.session.files = [...new Set([...r.session.files, ...files.map(f => f.path)])];
   365	    r.session.messages.push({ id: randomUUID(), role: 'user', text: visibleText, time: Date.now(), kind: 'text' });
   450	    const agent = validateConfig(agentValue), tools = new ClientTools(cwd, this.ask);
   451	    const peer = await openAcp(agent, cwd, this.ask, (method, params) => this.emit('agentEvent', { agentID: agent.id, method, params }), tools);
   452	    try {
   453	      const methods = Array.isArray(peer.info.authMethods) ? peer.info.authMethods.map(object) : [];
   454	      const method = methods.find(m => string(m.id ?? m.methodId) === methodID);
   455	      if (!method) throw new Error('Agent 未声明此认证方法');
   456	      if (method.type === 'terminal') return createTerminalAuth(agent, method, cwd, dirname(this.root));
   457	      return await peer.request(peer.version === 2 ? 'auth/login' : 'authenticate', { methodId: methodID }, 0);
   458	    }
   459	    finally { await peer.close(); await tools.close(); }
   460	  }
   461	  async close(): Promise<void> {
   462	    const results = await Promise.allSettled([...this.running.keys()].map(id => this.stop(id)));
   463	    for (const result of results) if (result.status === 'rejected') this.emit('warning', `会话清理失败：${String(result.reason)}`);
   464	  }
   465	
   466	  async importNative(agentValue: unknown, record: Data, cwd: string): Promise<Data> {
   467	    const agent = validateConfig(agentValue), nativeID = string(record.sessionId);
   468	    if (!nativeID) throw new Error('Agent 历史条目缺少会话 ID');
   469	    const session: Session = { id: sessionKey('acp', `${agent.id}\0${nativeID}`), nativeID, source: 'acp', instanceID: agent.id, title: string(record.title, nativeID), project: string(record.cwd, cwd), home: '', created: Date.now(), updated: Date.now(), messages: [], usage: [], files: [], warnings: [] };
   470	    return this.start({ agent, session, cwd: session.project });
   471	  }
   472	}

desk
     1	import { readFile, writeFile, mkdir, rename } from 'node:fs/promises';
     2	import { join } from 'node:path';
     3	import { unzipSync } from 'fflate';
     4	import { object, string, timestamp, content } from './types.ts';
     5	import { sessionKey } from './logs.ts';
     6	import type { Session } from './types.ts';
     7	
     8	export function importConversations(value: unknown): Session[] {
     9	  if (!Array.isArray(value)) throw new Error('请选择包含 conversations.json 的 Claude 官方导出包');
    10	  return value.map(record => {
    11	    const v = object(record);
    12	    if (!string(v.uuid) || !Array.isArray(v.chat_messages)) throw new Error('导出记录缺少 uuid 或 chat_messages');
    13	    const session: Session = {
    14	      id: sessionKey('desktop', string(v.uuid)), nativeID: string(v.uuid), source: 'desktop',
    15	      title: string(v.name, 'Claude 聊天'), project: '', home: '',
    16	      created: timestamp(v.created_at), updated: timestamp(v.updated_at), messages: [], usage: [], files: [],
    17	      warnings: ['普通聊天用量不可用；此记录在导入后不会实时同步'],
    18	    };
    19	    for (const item of v.chat_messages) {
    20	      const m = object(item);
    21	      session.messages.push({ id: string(m.uuid, String(session.messages.length)), role: m.sender === 'human' ? 'user' : 'assistant', text: content(m.content) || string(m.text), time: timestamp(m.created_at), kind: 'text' });
    22	      if ((Array.isArray(m.attachments) && m.attachments.length) || (Array.isArray(m.files) && m.files.length)) session.warnings.push('原始上传附件未包含在官方导出包中');
    23	    }
    24	    session.warnings = [...new Set(session.warnings)];
    25	    return session;
    26	  });
    27	}
    28	
    29	export async function importDesktop(path: string, root: string): Promise<Session[]> {
    30	  const data = await readFile(path);
    31	  let value: unknown;
    32	  if (path.toLowerCase().endsWith('.zip')) {
    33	    const files = unzipSync(data, { filter: entry => /(^|\/)conversations\.json$/.test(entry.name) && entry.originalSize < 512 * 1024 * 1024 });
    34	    const found = Object.values(files)[0];
    35	    if (!found) throw new Error('导出包中未找到 conversations.json');
    36	    value = JSON.parse(new TextDecoder().decode(found));
    37	  } else value = JSON.parse(data.toString('utf8'));
    38	  const sessions = importConversations(value);
    39	  await mkdir(root, { recursive: true });
    40	  for (const [index, session] of sessions.entries()) {
    41	    const file = join(root, session.id.replace(':', '_') + '.json');
    42	    await writeFile(file + '.writing', JSON.stringify((value as unknown[])[index], null, 2));
    43	    await rename(file + '.writing', file);
    44	    session.files = [file];
    45	  }
    46	  return sessions;
    47	}

mess
     1	export type Source = 'codex' | 'claude' | 'dsh' | 'desktop' | 'acp';
     2	export type Data = Record<string, unknown>;
     3	export interface Message { id: string; role: string; text: string; time: number; kind: string }
     4	export interface Usage { id: string; time: number; model: string; input: number; output: number; cacheRead: number; cacheWrite: number }
     5	export interface Session {
     6	  id: string; nativeID: string; source: Source; title: string; project: string; home: string;
     7	  created: number; updated: number; parentID?: string; provider?: string; instanceID?: string;
     8	  messages: Message[]; usage: Usage[]; files: string[]; warnings: string[];
     9	  nativeSource?: string;
    10	  nativeStarted?: boolean;
    11	  migration?: { sourceID: string; source: string; sourceNativeID: string; created: number };
    12	}
    13	export interface Location { source: 'codex' | 'claude' | 'dsh'; path: string }
    14	export interface AgentConfig {
    15	  id: string; name: string; kind: 'codex' | 'claude' | 'dsh' | 'acp';
    16	  command: string; args: string[]; env: Record<string, string>; version?: string;
    17	  registryID?: string; installPath?: string; protocol?: number;
    18	}
    19	export const object = (value: unknown): Data => value !== null && typeof value === 'object' && !Array.isArray(value) ? value as Data : {};
    20	export const string = (value: unknown, fallback = ''): string => typeof value === 'string' ? value : fallback;
    21	export const number = (value: unknown): number => typeof value === 'number' && Number.isFinite(value) && value >= 0 ? value : 0;
    22	export function timestamp(value: unknown): number {
    23	  if (typeof value === 'number') return value < 1e11 ? value * 1000 : value;
    24	  const parsed = Date.parse(string(value));
    25	  return Number.isFinite(parsed) ? parsed : 0;
    26	}
    27	export function content(value: unknown): string {
    28	  if (typeof value === 'string') return value;
    29	  if (Array.isArray(value)) return value.map(content).filter(Boolean).join('\n');
    30	  const v = object(value);
    31	  if (typeof v.text === 'string') return v.text;
    32	  if (v.content !== undefined) return content(v.content);
    33	  if (v.type === 'tool_use' || v.type === 'tool_call') return `${string(v.name)}\n${JSON.stringify(v.input ?? v.arguments, null, 2)}`;
    34	  if (Object.keys(v).length) return JSON.stringify(v, null, 2);
    35	  return '';
    36	}

scan
   140	      }
   141	      if (e.type === 'tool/call') addMessage('tool', `${string(d.name)}\n${content(d.arguments)}`, String(e.seq), 'tool');
   142	      if (e.type === 'tool/result') addMessage('tool', content(d.result ?? d.content), String(e.seq), 'tool');
   143	    }
   144	  }
   145	  session.id = sessionKey(source, `${home}\0${session.nativeID}`);
   146	  session.messages = [...messages.values()];
   147	  session.usage = [...(canonical.size ? canonical : counted).values()];
   148	  session.title ||= session.nativeID;
   149	  if (Number.isFinite(firstTime)) session.created = Math.min(session.created || firstTime, firstTime);
   150	  session.updated = lastTime || file.mtimeMs;
   151	  session.warnings = [...new Set(session.warnings)];
   152	  let migrationData: Buffer;
   153	  try { migrationData = await readFile(path + '.ragdoll.json'); }
   154	  catch (error) { if (object(error).code === 'ENOENT') return session; throw error; }
   155	  {
   156	    const migration = object(JSON.parse(migrationData.toString('utf8')));
   157	    if (typeof migration.sourceID !== 'string' || typeof migration.source !== 'string' || typeof migration.sourceNativeID !== 'string' || typeof migration.created !== 'number') throw new Error('迁移来源记录无效');
   158	    session.migration = migration as unknown as NonNullable<Session['migration']>;
   159	    if (typeof migration.title === 'string') session.title = migration.title;
   160	    session.files.push(path + '.ragdoll.json');
   161	    if (migration.files !== undefined) {
   162	      const root = (await realpath(home)) + '/.ragdoll-migrations/';
   163	      if (!Array.isArray(migration.files) || migration.files.some(p => typeof p !== 'string')) throw new Error('迁移附件清单无效');
   164	      for (const file of migration.files as string[]) { if (!(await realpath(file)).startsWith(root)) throw new Error('迁移附件清单越界'); }
   165	      session.files.push(...migration.files as string[]);
   166	    }
   167	  }
   168	  return session;
   169	}
   170	
   171	async function walk(path: string): Promise<string[]> {
   172	  const entries = await readdir(path, { withFileTypes: true });
   173	  const found = await Promise.all(entries.filter(e => !e.isSymbolicLink()).map(async e => {
   174	    const p = join(path, e.name);
   175	    if (e.isDirectory()) return walk(p);
   176	    return /\.jsonl(?:\.(?:zstd|zst))?$/.test(e.name) ? [p] : [];
   177	  }));
   178	  return found.flat();
   179	}
   180	
   181	export async function scan(locations: Location[], onSession?: (session: Session) => void | Promise<void>, onError?: (message: string) => void): Promise<Session[]> {
   182	  const results: Session[] = [];
   183	  for (const location of locations) {
   184	    let paths: string[];
   185	    try {
   186	      paths = (await Promise.all((location.source === 'claude' ? ['projects'] : ['sessions', ...(location.source === 'codex' ? ['archived_sessions'] : [])]).map(async sub => {
   187	        try { return await walk(join(location.path, sub)); }
   188	        catch (error) { if (object(error).code === 'ENOENT') return []; throw error; }
   189	      }))).flat();
   190	    } catch (error) { onError?.(`${location.path}: ${String(error)}`); continue; }
   191	    if (location.source === 'dsh') {
   192	      const latest = new Map<string, { path: string; version: number; modified: number }>();
   193	      for (const path of paths) {
   194	        const match = /^session(?:\.v(\d+))?\.jsonl(?:\.zstd)?$/.exec(basename(path));
   195	        if (!match) continue;
   196	        const key = dirname(path), version = Number(match[1] || 0), modified = (await stat(path)).mtimeMs;
   197	        const old = latest.get(key);
   198	        if (!old || version > old.version || (version === old.version && modified > old.modified)) latest.set(key, { path, version, modified });
   199	      }
   200	      paths = [...latest.values()].map(v => v.path);
   201	    }
   202	    for (const path of paths) {
   203	      try {
   204	        const info = await stat(path), fingerprint = `${info.size}:${info.mtimeMs}:${info.birthtimeMs}`;
   205	        if (onSession && fingerprints.get(path) === fingerprint) continue;
   206	        const session = await parseFile(location.source, await realpath(path), location.path);
   207	        if (onSession) { await onSession(session); fingerprints.set(path, fingerprint); } else results.push(session);
   208	      } catch (error) { onError?.(`${path}: ${String(error)}`); }
   209	    }
   210	  }
   211	  return results;
   212	}

store
     1	import Foundation
     2	import GRDB
     3	
     4	public final class Store: Sendable {
     5	    private let db: DatabaseQueue
     6	    public init(path: String) throws {
     7	        var configuration = Configuration(); configuration.busyMode = .timeout(10)
     8	        db = try DatabaseQueue(path: path, configuration: configuration)
     9	        try db.write { db in
    10	            try db.execute(sql: "CREATE TABLE IF NOT EXISTS sessions (id TEXT PRIMARY KEY, source TEXT NOT NULL, native_id TEXT NOT NULL, title TEXT NOT NULL, project TEXT NOT NULL, updated REAL NOT NULL, body BLOB NOT NULL, summary BLOB NOT NULL, search TEXT NOT NULL)")
    11	            try db.execute(sql: "CREATE INDEX IF NOT EXISTS sessions_updated ON sessions(updated DESC)")
    12	            if try !db.columns(in: "sessions").contains(where: { $0.name == "canonical_id" }) { try db.execute(sql: "ALTER TABLE sessions ADD COLUMN canonical_id TEXT") }
    13	            try db.execute(sql: "CREATE INDEX IF NOT EXISTS sessions_native ON sessions(source,native_id)")
    14	            try db.execute(sql: "CREATE INDEX IF NOT EXISTS sessions_canonical ON sessions(canonical_id)")
    15	            try db.execute(sql: "CREATE TABLE IF NOT EXISTS settings (id INTEGER PRIMARY KEY CHECK(id=1), body BLOB NOT NULL)")
    16	        }
    17	    }
    18	    @discardableResult public func save(_ session: Session) throws -> Bool {
    19	        return try db.write { db in
    20	            var session = session
    21	            if let existing = try Data.fetchOne(db, sql: "SELECT body FROM sessions WHERE id=?", arguments: [session.id]) {
    22	                let previous = try JSONDecoder().decode(Session.self, from: existing)
    23	                session.files = Array(Set(previous.files + session.files)).sorted()
    24	                session.instanceID = session.instanceID ?? previous.instanceID
    25	                session.migration = session.migration ?? previous.migration
    26	            }
    27	            if let nativeSource = session.nativeSource {
    28	                let candidates = try Data.fetchAll(db, sql: "SELECT body FROM sessions WHERE source=? AND native_id=?", arguments: [nativeSource, session.nativeID]).map { try JSONDecoder().decode(Session.self, from: $0) }.filter { $0.home == session.home }
    29	                if candidates.count == 1, let native = candidates.first {
    30	                    session.canonicalID = native.id; session.files = Array(Set(session.files + native.files)).sorted(); session.usage = native.usage
    31	                }
    32	            }
    33	            var changed = try Self.upsert(db, session)
    34	            if session.source != "acp" {
    35	                let aliases = try Data.fetchAll(db, sql: "SELECT body FROM sessions WHERE source='acp' AND native_id=?", arguments: [session.nativeID]).map { try JSONDecoder().decode(Session.self, from: $0) }
    36	                for var alias in aliases where alias.nativeSource == session.source && alias.home == session.home {
    37	                    alias.canonicalID = session.id; alias.usage = session.usage; alias.files = Array(Set(alias.files + session.files)).sorted()
    38	                    changed = try Self.upsert(db, alias) || changed
    39	                }
    40	            }
    41	            return changed
    42	        }
    43	    }
    44	    private static func upsert(_ db: Database, _ session: Session) throws -> Bool {
    45	        let encoder = JSONEncoder(); encoder.outputFormatting = [.sortedKeys]
    46	        let body = try encoder.encode(session)
    47	        guard try Data.fetchOne(db, sql: "SELECT body FROM sessions WHERE id=?", arguments: [session.id]) != body else { return false }
    48	        var summary = session; summary.messages = []
    49	        let summaryData = try encoder.encode(summary)
    50	        try db.execute(sql: "INSERT INTO sessions(id,source,native_id,title,project,updated,body,summary,search,canonical_id) VALUES (?,?,?,?,?,?,?,?,?,?) ON CONFLICT(id) DO UPDATE SET title=excluded.title, project=excluded.project, updated=excluded.updated, body=excluded.body, summary=excluded.summary, search=excluded.search, canonical_id=excluded.canonical_id", arguments: [session.id, session.source, session.nativeID, session.title, session.project, session.updated, body, summaryData, session.title + "\n" + session.messages.map(\.text).joined(separator: "\n"), session.canonicalID])
    51	        return true
    52	    }
    53	    public func list(query: String = "", limit: Int = Int.max) throws -> [Session] {
    54	        try db.read { db in
    55	            let escaped = query.replacingOccurrences(of: "\\", with: "\\\\").replacingOccurrences(of: "%", with: "\\%").replacingOccurrences(of: "_", with: "\\_")
    56	            return try Data.fetchAll(db, sql: "SELECT summary FROM sessions s WHERE search LIKE ? ESCAPE '\\' AND NOT EXISTS (SELECT 1 FROM sessions a WHERE a.canonical_id=s.id) ORDER BY updated DESC LIMIT ?", arguments: ["%\(escaped)%", limit]).map { try JSONDecoder().decode(Session.self, from: $0) }
    57	        }
    58	    }
    59	    public func session(_ id: String) throws -> Session? {
    60	        try db.read { db in
    61	            try Data.fetchOne(db, sql: "SELECT body FROM sessions WHERE id=?", arguments: [id]).map { try JSONDecoder().decode(Session.self, from: $0) }
    62	        }
    63	    }
    64	    public func settings() throws -> Settings {
    65	        try db.read { db in
    66	            try Data.fetchOne(db, sql: "SELECT body FROM settings WHERE id=1").map { try JSONDecoder().decode(Settings.self, from: $0) } ?? Settings()
    67	        }
    68	    }


## tool · 2026-11-17T00:36:13Z


Script completed
Wall time 0.1 seconds
Output:

bridge
     1	import Foundation
     2	
     3	public enum JSONValue: Codable, Sendable, Equatable {
     4	    case object([String: JSONValue]), array([JSONValue]), string(String), number(Double), bool(Bool), null
     5	    public init(from decoder: Decoder) throws {
     6	        let c = try decoder.singleValueContainer()
     7	        if c.decodeNil() { self = .null }
     8	        else if let v = try? c.decode(Bool.self) { self = .bool(v) }
     9	        else if let v = try? c.decode(Double.self) { self = .number(v) }
    10	        else if let v = try? c.decode(String.self) { self = .string(v) }
    11	        else if let v = try? c.decode([JSONValue].self) { self = .array(v) }
    12	        else { self = .object(try c.decode([String: JSONValue].self)) }
    13	    }
    14	    public func encode(to encoder: Encoder) throws {
    15	        var c = encoder.singleValueContainer()
    16	        switch self {
    17	        case .object(let v): try c.encode(v)
    18	        case .array(let v): try c.encode(v)
    19	        case .string(let v): try c.encode(v)
    20	        case .number(let v): try c.encode(v)
    21	        case .bool(let v): try c.encode(v)
    22	        case .null: try c.encodeNil()
    23	        }
    24	    }
    25	    public subscript(_ key: String) -> JSONValue { if case .object(let v) = self { return v[key] ?? .null }; return .null }
    26	    public var string: String { if case .string(let v) = self { return v }; return "" }
    27	    public var array: [JSONValue] { if case .array(let v) = self { return v }; return [] }
    28	    public var dictionary: [String: JSONValue] { if case .object(let v) = self { return v }; return [:] }
    29	    public var text: String {
    30	        if case .string(let v) = self { return v }
    31	        let encoder = JSONEncoder(); encoder.outputFormatting = [.prettyPrinted, .sortedKeys, .withoutEscapingSlashes]
    32	        return (try? encoder.encode(self)).map { String(decoding: $0, as: UTF8.self) } ?? ""
    33	    }
    34	    public static func encode<T: Encodable>(_ value: T) throws -> JSONValue { try JSONDecoder().decode(JSONValue.self, from: JSONEncoder().encode(value)) }
    35	    public func decode<T: Decodable>(_ type: T.Type) throws -> T { try JSONDecoder().decode(type, from: JSONEncoder().encode(self)) }
    36	}
    37	
    38	public actor RuntimeBridge {
    39	    private var process: Process?
    40	    private var input: FileHandle?
    41	    private var serial = 0
    42	    private var pending: [String: CheckedContinuation<JSONValue, any Error>] = [:]
    43	    private var handler: (@Sendable (String, JSONValue) async -> Void)?
    44	    private var stderr = ""
    45	    public init() {}
    46	    public func setHandler(_ handler: @escaping @Sendable (String, JSONValue) async -> Void) { self.handler = handler }
    47	
    48	    public func start(dataDirectory: URL) throws {
    49	        guard process == nil else { return }
    50	        let resources = Bundle.main.resourceURL ?? URL(fileURLWithPath: FileManager.default.currentDirectoryPath)
    51	        let repo = URL(fileURLWithPath: #filePath).deletingLastPathComponent().deletingLastPathComponent().deletingLastPathComponent()
    52	        let bundled = resources.appendingPathComponent("runtime")
    53	        let isBundled = FileManager.default.fileExists(atPath: bundled.appendingPathComponent("app/dist/main.mjs").path)
    54	        let script = isBundled ? bundled.appendingPathComponent("app/dist/main.mjs") : repo.appendingPathComponent("runtime/dist/main.mjs")
    55	        let node = isBundled ? bundled.appendingPathComponent("node/bin/node") : URL(fileURLWithPath: "/opt/homebrew/bin/node")
    56	        guard FileManager.default.fileExists(atPath: script.path), FileManager.default.isExecutableFile(atPath: node.path) else { throw failure("缺少 SDK 助手，请先运行构建脚本。") }
    57	        let p = Process(); p.executableURL = node; p.arguments = [script.path, "--data-dir", dataDirectory.path]
    58	        var environment = ProcessInfo.processInfo.environment
    59	        environment["PATH"] = node.deletingLastPathComponent().path + ":/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:" + (environment["PATH"] ?? "")
    60	        p.environment = environment
    61	        let stdin = Pipe(), stdout = Pipe(), errors = Pipe()
    62	        p.standardInput = stdin; p.standardOutput = stdout; p.standardError = errors
    63	        p.terminationHandler = { [weak self] p in Task { await self?.terminated(p.terminationStatus) } }
    64	        try p.run(); process = p; input = stdin.fileHandleForWriting
    65	        let reader = stdout.fileHandleForReading
    66	        Task.detached { [weak self] in
    67	            var pending = Data()
    68	            while true {
    69	                let chunk = reader.availableData
    70	                if chunk.isEmpty { break }
    71	                var start = chunk.startIndex
    72	                while let index = chunk[start...].firstIndex(of: 10) {
    73	                    pending.append(chunk[start..<index])
    74	                    await self?.receive(pending)
    75	                    pending = Data()
    76	                    start = chunk.index(after: index)
    77	                }
    78	                pending.append(chunk[start...])
    79	            }
    80	        }
    81	        let errorReader = errors.fileHandleForReading
    82	        Task.detached { [weak self] in
    83	            while true { let data = errorReader.availableData; if data.isEmpty { break }; await self?.errorOutput(String(decoding: data, as: UTF8.self)) }
    84	        }
    85	    }
    86	    public func request(_ method: String, _ params: [String: JSONValue] = [:], timeout: Double = 120) async throws -> JSONValue {
    87	        guard let input else { throw failure("SDK 助手尚未启动") }
    88	        serial += 1; let id = String(serial)
    89	        let message = try JSONEncoder().encode(JSONValue.object(["id": .string(id), "method": .string(method), "params": .object(params)])) + Data([10])
    90	        return try await withCheckedThrowingContinuation { continuation in
    91	            pending[id] = continuation
    92	            do { try input.write(contentsOf: message) }
    93	            catch { pending.removeValue(forKey: id)?.resume(throwing: error) }
    94	            if timeout > 0 { Task { try? await Task.sleep(for: .seconds(timeout)); timedOut(id, method) } }
    95	        }
    96	    }
    97	    private func timedOut(_ id: String, _ method: String) { pending.removeValue(forKey: id)?.resume(throwing: failure("助手请求超时：\(method)。运行中的操作不会自动重试。")) }
    98	    private func receive(_ data: Data) async {
    99	        do {
   100	            let message = try JSONDecoder().decode(JSONValue.self, from: data)
   101	            if !message["event"].string.isEmpty { await handler?(message["event"].string, message["data"]); return }
   102	            let id = message["id"].string
   103	            guard let continuation = pending.removeValue(forKey: id) else { return }
   104	            if message["error"] != .null { continuation.resume(throwing: failure(message["error"]["message"].string)) }
   105	            else { continuation.resume(returning: message["result"]) }
   106	        } catch { await handler?("warning", .string("助手返回无效数据：\(error.localizedDescription)")) }
   107	    }
   108	    private func errorOutput(_ text: String) { stderr = String((stderr + text).suffix(4000)) }
   109	    private func terminated(_ code: Int32) async {
   110	        process = nil; input = nil
   111	        let error = failure("SDK 助手已退出（\(code)）：\(stderr)")
   112	        for continuation in pending.values { continuation.resume(throwing: error) }; pending.removeAll()
   113	        await handler?("disconnected", .string(error.localizedDescription))
   114	    }
   115	    public func close() async {
   116	        _ = try? await request("shutdown", timeout: 5)
   117	        try? input?.close(); process?.terminate()
   118	    }
   119	    private func failure(_ message: String) -> NSError { NSError(domain: "Ragdoll.Runtime", code: 1, userInfo: [NSLocalizedDescriptionKey: message]) }
   120	}

plans
20:- 三项全部纳入第一版：跨工具迁移、远端归档同步、独立后台常驻服务。
38:- 后台 helper、进程锁、请求保留及独立进程扫描/归档测试已通过；GUI 与服务设置编译通过。
41:- 尚需：持续服务及重启推送重试检查、完整允许测试集、release 打包、后台系统注册条件检查、独立审阅和提交推送。
55:- Swift 和真实 Codex 测试需要沙箱外构建/状态目录写入权限，已通过自动审批运行；普通沙箱失败不能判定为实现不兼容。

persist
140-        if (typeof v.id === 'string' && Array.isArray(v.messages) && Array.isArray(v.usage)) sessions.push(v as unknown as Session);
141-      } catch (error) { if (object(error).code !== 'ENOENT') this.emit('warning', `会话缓存无法读取：${String(error)}`); }
142-    }
143-    return sessions;
144-  }
145:  private async persist(r: Running): Promise<void> {
146-    await r.writeQueue;
147-    const dir = join(this.root, sessionKey('chat', r.session.id));
148-    await mkdir(dir, { recursive: true });
149-    r.session.updated = Date.now();
150:    if (r.session.source === 'acp') r.session.files = [...new Set([join(dir, 'events.jsonl'), ...r.session.files])];
151-    const path = join(dir, 'session.json');
152-    await writeFile(path + '.writing', JSON.stringify(r.session)); await rename(path + '.writing', path);
153-    this.emit('session', r.session);
154-  }
155-  private update(r: Running, method: string, params: Data): void {
--
332-        session.home = agent.env[key] || defaultLocations().find(l => l.source === nativeSource)?.path || '';
333-      }
334-    }
335-    session.instanceID = agent.id;
336-    this.running.set(session.id, r);
337:    await this.persist(r);
338-    return { session, info };
339-  }
340-
341-  async send(id: string, text: string, model?: string, attachments: unknown = []): Promise<void> {
342-    const r = this.running.get(id);
--
359-      if (prompts.image !== true) throw new Error('此 ACP Agent 未声明图片输入能力');
360-    }
361-    const visibleText = text + (files.length ? '\n\n' + files.map(f => `[附件：${basename(f.path)}](${pathToFileURL(f.path).href})`).join('\n') : '');
362-    const withPaths = text + (files.some(f => !f.mime) ? '\n\n附件路径：\n' + files.filter(f => !f.mime).map(f => f.path).join('\n') : '');
363-    r.busy = true; r.deltaID = undefined; r.hasActivity = false; r.failure = undefined;
364:    r.session.files = [...new Set([...r.session.files, ...files.map(f => f.path)])];
365-    r.session.messages.push({ id: randomUUID(), role: 'user', text: visibleText, time: Date.now(), kind: 'text' });
366-    if (r.session.title === '新对话') r.session.title = text.slice(0, 80);
367:    await this.persist(r); this.emit('state', { conversationID: id, state: 'running' });
368-    try {
369-      if (r.peer) {
370-        if (model) await r.peer.request('session/set_config_option', { sessionId: r.session.nativeID, configId: 'model', value: model, ...(r.peer.version === 2 ? { type: 'id' } : {}) });
371-        const completed = new Promise<void>((resolve, reject) => { r.finish = resolve; r.fail = reject; });
372-        const blocks = files.map(f => f.mime ? { type: 'image', data: f.data, mimeType: f.mime } : { type: 'resource_link', uri: pathToFileURL(f.path).href, name: basename(f.path) });
--
417-        } } finally { q.close(); r.claude = undefined; }
418-      }
419-      this.emit('state', { conversationID: id, state: 'idle' });
420-    } catch (error) {
421-      this.emit('state', { conversationID: id, state: 'error', message: String(error) }); throw error;
422:    } finally { r.busy = false; r.finish = undefined; r.fail = undefined; await this.persist(r); }
423-  }
424-  async stop(id: string): Promise<void> {
425-    const r = this.running.get(id); if (!r) return;
426-    if (r.peer && r.busy) await r.peer.notify('session/cancel', { sessionId: r.session.nativeID }).catch(error => this.emit('warning', `ACP 取消返回：${String(error)}`));
427-    if (r.claude) { try { await r.claude.interrupt(); } catch (error) { this.emit('warning', `Claude 中断返回：${String(error)}`); } finally { r.claude.close(); r.claude = undefined; } }
428-    if (r.rpc && r.agent.kind === 'codex' && r.turnID) await r.rpc.request('turn/interrupt', { threadId: r.session.nativeID, turnId: r.turnID }).catch(() => {});
429-    await r.peer?.close(); await r.rpc?.close(); await r.tools?.close(); r.finish?.();
430-    this.running.delete(id); this.emit('state', { conversationID: id, state: 'stopped' });
431:    await this.persist(r);
432-  }
433-  async configure(id: string, configId: string, value: string): Promise<unknown> {
434-    const r = this.running.get(id); if (!r?.peer) throw new Error('此会话没有 ACP 配置项');
435-    if (configId === '__legacy_mode') return r.peer.request('session/set_mode', { sessionId: r.session.nativeID, modeId: value });
436-    if (configId === '__legacy_model') return r.peer.request('session/set_model', { sessionId: r.session.nativeID, modelId: value });

basic
c82ebeb feat(migration): write native conversation history across tools


## tool · 2026-11-17T00:36:24Z




## tool · 2026-11-17T00:36:32Z


Script completed
Wall time 0.2 seconds
Output:

main
     1	import { createInterface } from 'node:readline';
     2	import { watch } from 'node:fs';
     3	import type { FSWatcher } from 'node:fs';
     4	import { mkdir } from 'node:fs/promises';
     5	import { join, resolve } from 'node:path';
     6	import { homedir } from 'node:os';
     7	import { randomUUID } from 'node:crypto';
     8	import { once } from 'node:events';
     9	import { scan, defaultLocations } from './logs.ts';
    10	import { importDesktop } from './desktop.ts';
    11	import { registry, install, uninstall } from './registry.ts';
    12	import { Agents, defaultAgents } from './agents.ts';
    13	import { createTerminalAuth, runTerminalAuth } from './terminal-auth.ts';
    14	import { fileURLToPath } from 'node:url';
    15	import { migrateSession } from './migration.ts';
    16	import { object, string } from './types.ts';
    17	import type { Data, Location, AgentConfig } from './types.ts';
    18	
    19	const dataArg = process.argv.indexOf('--data-dir');
    20	const root = dataArg >= 0 ? resolve(process.argv[dataArg + 1]) : join(homedir(), 'Library/Application Support/Ragdoll');
    21	process.env.RAGDOLL_MAIN_SCRIPT = fileURLToPath(import.meta.url);
    22	const output = (value: unknown) => process.stdout.write(JSON.stringify(value) + '\n');
    23	const emit = (event: string, data: unknown) => output({ event, data });
    24	async function sessionOutput(data: unknown): Promise<void> {
    25	  if (!output({ event: 'session', data })) await once(process.stdout, 'drain');
    26	}
    27	const approvals = new Map<string, { resolve: (value: Data) => void; remove: () => void }>();
    28	const agents = new Agents(join(root, 'conversations'), emit, (method, params, signal) => new Promise(resolve => {
    29	  const requestID = randomUUID();
    30	  const cancel = () => { approvals.delete(requestID); emit('approvalCancelled', { requestID }); resolve({ allowed: false }); };
    31	  if (signal?.aborted) return cancel();
    32	  signal?.addEventListener('abort', cancel, { once: true });
    33	  approvals.set(requestID, { resolve, remove: () => signal?.removeEventListener('abort', cancel) });
    34	  emit('approval', { requestID, method, params });
    35	}));
    36	let watchers: FSWatcher[] = [];
    37	let scanActive = false;
    38	let changeTimer: NodeJS.Timeout | undefined;
    39	function watchLocations(locations: Location[]): void {
    40	  for (const watcher of watchers) watcher.close(); watchers = [];
    41	  for (const location of locations) {
    42	    try {
    43	      const watcher = watch(location.path, { recursive: true }, () => {
    44	        clearTimeout(changeTimer); changeTimer = setTimeout(() => emit('sourceChanged', {}), 1500);
    45	      });
    46	      watcher.on('error', error => emit('warning', `目录监听失败：${String(error)}`));
    47	      watchers.push(watcher);
    48	    } catch (error) { if (object(error).code !== 'ENOENT') emit('warning', `目录监听失败：${String(error)}`); }
    49	  }
    50	}
    51	
    52	async function handle(method: string, p: Data): Promise<unknown> {
    53	  if (method === 'initialize') return { version: '0.1.0', locations: defaultLocations(), agents: await defaultAgents() };
    54	  if (method === 'scan') {
    55	    if (scanActive) throw new Error('正在扫描，请稍后重试');
    56	    const locations = p.locations === undefined ? defaultLocations() : p.locations;
    57	    if (!Array.isArray(locations) || locations.some(v => !['codex', 'claude', 'dsh'].includes(string(object(v).source)) || !string(object(v).path))) throw new Error('扫描目录配置无效');
    58	    scanActive = true;
    59	    try {
    60	      watchLocations(locations as Location[]);
    61	      for (const session of await agents.saved()) await sessionOutput(session);
    62	      let count = 0;
    63	      await scan(locations as Location[], async s => { count++; await sessionOutput(s); }, error => emit('warning', error));
    64	      return { count };
    65	    } finally { scanActive = false; }
    66	  }
    67	  if (method === 'import') {
    68	    const sessions = await importDesktop(string(p.path), join(root, 'imports'));
    69	    for (const session of sessions) emit('session', session);
    70	    return { count: sessions.length };
    71	  }
    72	  if (method === 'registry') return registry();
    73	  if (method === 'migrate') { const session = await migrateSession(p); emit('session', session); return { session }; }
    74	  if (method === 'install') return install(p.agent, join(root, 'tools'));
    75	  if (method === 'uninstall') { await uninstall(p.agent as AgentConfig, join(root, 'tools')); return {}; }
    76	  if (method === 'probe') return agents.probe(p.agent, string(p.cwd, homedir()));
    77	  if (method === 'chat.start') return agents.start(p);
    78	  if (method === 'chat.send') { await agents.send(string(p.id), string(p.text), string(p.model) || undefined, p.attachments ?? []); return {}; }
    79	  if (method === 'chat.stop') { await agents.stop(string(p.id)); return {}; }
    80	  if (method === 'chat.configure') return agents.configure(string(p.id), string(p.configID), string(p.value));
    81	  if (method === 'chat.list') return agents.list(p.agent, string(p.cwd, homedir()), string(p.cursor) || undefined);
    82	  if (method === 'chat.import') return agents.importNative(p.agent, object(p.session), string(p.cwd, homedir()));
    83	  if (method === 'native.login') {
    84	    const agent = p.agent as AgentConfig;
    85	    if (agent.kind !== 'codex' && agent.kind !== 'claude') throw new Error('请使用原应用管理此工具的登录');
    86	    return createTerminalAuth({ ...agent, args: [] }, { args: agent.kind === 'codex' ? ['login'] : ['auth', 'login'] }, homedir(), root);
    87	  }
    88	  if (method === 'authenticate') return agents.authenticate(p.agent, string(p.cwd, homedir()), string(p.methodID));
    89	  if (method === 'approval') {
    90	    const pending = approvals.get(string(p.requestID));
    91	    if (!pending) throw new Error('权限请求已经取消或结束');
    92	    approvals.delete(string(p.requestID)); pending.remove(); pending.resolve(object(p.answer)); return {};
    93	  }
    94	  if (method === 'shutdown') { await agents.close(); for (const watcher of watchers) watcher.close(); return {}; }
    95	  throw new Error(`未知助手方法：${method}`);
    96	}
    97	
    98	if (process.argv.includes('--terminal-auth')) {
    99	  try { process.exitCode = await runTerminalAuth(process.argv[process.argv.indexOf('--terminal-auth') + 1]); }
   100	  catch (error) { process.stderr.write(`${String(error)}\n`); process.exitCode = 1; }
   101	} else if (process.argv.includes('--self-check')) {
   102	  output({ status: 'ok', version: '0.1.0', node: process.version, agents: await defaultAgents() });
   103	} else {
   104	  await mkdir(root, { recursive: true });
   105	  const input = createInterface({ input: process.stdin });
   106	  input.on('line', line => {
   107	    let request: Data;
   108	    try {
   109	      request = object(JSON.parse(line));
   110	      if ((typeof request.id !== 'number' && typeof request.id !== 'string') || typeof request.method !== 'string') throw new Error('请求必须包含 id 和 method');
   111	    } catch (error) { output({ id: null, error: { status: 'error', type: 'InvalidRequest', message: String(error), suggestion: '发送有效的 NDJSON 请求' } }); return; }
   112	    void handle(request.method as string, object(request.params)).then(
   113	      result => output({ id: request.id, result }),
   114	      error => output({ id: request.id, error: { status: 'error', type: error instanceof Error ? error.name : 'RuntimeError', message: String(error), suggestion: '检查 Agent 配置、登录状态或运行日志后重试' } }),
   115	    );
   116	  });
   117	  input.on('close', () => {
   118	    for (const approval of approvals.values()) { approval.remove(); approval.resolve({ allowed: false }); }
   119	    for (const watcher of watchers) watcher.close(); clearTimeout(changeTimer);
   120	    void agents.close().finally(() => process.exit(0));
   121	  });
   122	}

node
    35	  } finally { await rm(root, { recursive: true, force: true }); }
    36	});
    37	
    38	test('migration copies attachments and rejects a target history symlink before creating external directories', async () => {
    39	  const root = resolve(import.meta.dirname, '../../.agent/tests', randomUUID());
    40	  await mkdir(root, { recursive: true });
    41	  const path = join(root, 'source.jsonl'), image = join(root, 'picture.png'), outside = join(root, 'outside'), home = join(root, 'target');
    42	  await writeFile(image, new Uint8Array([1, 2, 3, 4]));
    43	  await writeFile(path, JSON.stringify({ type: 'response_item', payload: { type: 'message', role: 'user', content: [{ type: 'input_image', image_url: new URL('file://' + image).href }] } }) + '\n');
    44	  const target = { id: 'native-codex', name: 'Codex', kind: 'codex', command: 'codex', args: [], env: {} };
    45	  try {
    46	    const source = await parseFile('codex', path, root);
    47	    const migrated = await migrateSession({ session: source, target, home, cwd: root });
    48	    const copy = migrated.files.find(p => p.endsWith('picture.png'))!;
    49	    assert.notEqual(copy, image); assert.deepEqual(await readFile(copy), Buffer.from([1, 2, 3, 4]));
    50	    const hostile = join(root, 'hostile'); await mkdir(hostile); await mkdir(outside);
    51	    await symlink(outside, join(hostile, 'sessions'));
    52	    await assert.rejects(migrateSession({ session: source, target, home: hostile, cwd: root }), /越界|符号链接/);
    53	    assert.deepEqual(await readdir(outside), []);
    54	    await rm(copy);
    55	    await assert.rejects(parseFile('codex', migrated.files.find(p => p.endsWith('.jsonl'))!, home), /ENOENT/);
    56	  } finally { await rm(root, { recursive: true, force: true }); }
    57	});
    58	
    59	for (const kind of ['codex', 'dsh'] as const) {
    60	  test(`migrated ${kind} conversation continues with the original context`, { skip: process.env.RAGDOLL_MIGRATION_LIVE !== kind, timeout: 180000 }, async () => {
    61	    const root = resolve(import.meta.dirname, '../../.agent/tests', randomUUID()); await mkdir(root, { recursive: true });
    62	    const sourcePath = join(root, 'source.jsonl'), home = join(root, 'target'); await mkdir(home);
    63	    await writeFile(sourcePath, [
    64	      { type: 'session_meta', payload: { id: 'original', cwd: root } },
    65	      { type: 'response_item', payload: { type: 'message', role: 'user', content: [{ type: 'input_text', text: 'Remember the secret code NATIVE_HISTORY_7319.' }] } },
    66	      { type: 'response_item', payload: { type: 'message', role: 'assistant', content: [{ type: 'output_text', text: 'I remember.' }] } },
    67	    ].map(row => JSON.stringify(row)).join('\n') + '\n');
    68	    const target = (await defaultAgents()).find(a => a.kind === kind)!;
    69	    target.env = { ...target.env, [kind === 'codex' ? 'CODEX_HOME' : 'DSH_HOME']: home };
    70	    if (kind === 'codex') {
    71	      const auth = join(defaultLocations().find(l => l.source === 'codex')!.path, 'auth.json'); await access(auth); await symlink(auth, join(home, 'auth.json'));
    72	    } else {
    73	      const auth = join(defaultLocations().find(l => l.source === 'dsh')!.path, '.credentials.yaml'); await access(auth); await symlink(auth, join(home, '.credentials.yaml'));
    74	    }
    75	    const terminalEvents: unknown[] = [];
    76	    const agents = new Agents(join(root, 'cache'), (event, raw) => {
    77	      if (event !== 'chat') return;
    78	      const data = object(raw), params = object(data.params), native = object(params.event);
    79	      if (native.type === 'turn/end' || String(data.method).includes('error')) terminalEvents.push({ method: data.method, type: native.type, reason: object(native.data).reason });
    80	    }, async () => ({ allowed: false }));
    81	    try {
    82	      const source = await parseFile('codex', sourcePath, root);
    83	      const session = await migrateSession({ session: source, target, home, cwd: root });
    84	      const probe = kind === 'codex' ? await agents.probe(target, root) : undefined;
    85	      const models = probe?.models as { data?: { model: string; isDefault: boolean }[] } | undefined;
    86	      const model = models?.data?.find(m => m.isDefault)?.model;
    87	      await agents.start({ agent: target, session, cwd: root, ...(model ? { model } : {}) });
    88	      await agents.send(session.id, 'Return only the secret code from our earlier conversation. Do not inspect files or use tools.', model);
    89	      const saved = (await agents.saved()).find(s => s.id === session.id)!;
    90	      assert.match(saved.messages.filter(m => m.role === 'assistant').at(-1)!.text, /NATIVE_HISTORY_7319/, JSON.stringify(terminalEvents));
    91	    } finally { await agents.close(); await rm(root, { recursive: true, force: true }); }
    92	  });
    93	}
    94	
    95	test('migration refuses malformed raw input before publishing target history', async () => {
    96	  const root = resolve(import.meta.dirname, '../../.agent/tests', randomUUID());
    97	  await mkdir(root, { recursive: true });
    98	  const path = join(root, 'bad.jsonl'); await writeFile(path, '{invalid}\n');
    99	  try {
   100	    await assert.rejects(migrateSession({ session: { id: 'one', source: 'codex', files: [path], messages: [], usage: [] }, target: { id: 'test', kind: 'codex', command: 'codex', args: [], env: {} }, home: join(root, 'target'), cwd: root }), SyntaxError);
   101	  } finally { await rm(root, { recursive: true, force: true }); }
   102	});
   103	
   104	test('Codex history becomes a dsh native conversation that the installed tool can resume', async () => {
   105	  const root = resolve(import.meta.dirname, '../../.agent/tests', randomUUID());
   106	  await mkdir(root, { recursive: true });
   107	  const path = join(root, 'source.jsonl');
   108	  await writeFile(path, [
   109	    { type: 'session_meta', payload: { id: 'original', cwd: root } },
   110	    { type: 'response_item', payload: { type: 'message', role: 'user', content: [{ type: 'input_text', text: 'remember DS_NATIVE_1729' }] } },

app
    42	    @Published var toolEvents: [String: [JSONValue]] = [:]
    43	    @Published var backgroundStatus = "未启用后台服务"
    44	    @Published var syncStatus = "未启用远端推送"
    45	    let bridge = RuntimeBridge()
    46	    let root: URL
    47	    private let store: Store?
    48	    private var reloadTask: Task<Void, Never>?
    49	    private var archiveTask: Task<Void, Never>?
    50	    private var dirtySince: Date?
    51	    private var dirtyGeneration = 0
    52	    private var initialized = false
    53	    private var lastRefresh = Date.distantPast
    54	
    55	    init() {
    56	        root = ProcessInfo.processInfo.environment["RAGDOLL_DATA_DIR"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent("Library/Application Support/Ragdoll")
    57	        do {
    58	            try FileManager.default.createDirectory(at: root, withIntermediateDirectories: true)
    59	            let store = try Store(path: root.appendingPathComponent("index.sqlite").path)
    60	            let settings = try store.settings(), sessions = try store.list()
    61	            self.store = store; self.settings = settings; self.sessions = sessions
    62	        } catch { store = nil; self.error = error.localizedDescription }
    63	    }
    64	    var filtered: [Session] { sessions.filter { session in
    65	        guard (source == "all" || session.source == source || session.nativeSource == source) && (project.isEmpty || session.project == project) else { return false }
    66	        guard let bucket = heatmapFilter else { return true }
    67	        let start = Calendar.current.date(byAdding: .day, value: -6, to: Calendar.current.startOfDay(for: Date()))!
    68	        return session.usage.contains { usage in
    69	            let date = Date(timeIntervalSince1970: usage.time / 1000)
    70	            return date >= start && Calendar.current.component(.weekday, from: date) - 1 == bucket[0] && Calendar.current.component(.hour, from: date) == bucket[1]
    71	        }
    72	    } }
    73	    var dashboard: Dashboard { Analytics.summarize(filtered, prices: settings.prices, budget: settings.weeklyBudget) }
    74	    var projects: [String] { Array(Set(sessions.map(\.project).filter { !$0.isEmpty })).sorted() }
    75	
    76	    func launch() async {
    77	        guard !initialized else { return }; initialized = true
    78	        await bridge.setHandler { [weak self] event, data in await self?.receive(event, data) }
    79	        do {
    80	            try await bridge.start(dataDirectory: root)
    81	            let initial = try await bridge.request("initialize")
    82	            if settings.locations.isEmpty { settings.locations = try initial["locations"].decode([Location].self) }
    83	            let defaults = try initial["agents"].decode([AgentConfig].self)
    84	            for agent in defaults where !settings.agents.contains(where: { $0.id == agent.id }) { settings.agents.append(agent) }
    85	            try saveSettings(); ready = true
    86	            if settings.backgroundEnabled == true { await setBackground(true) }
    87	            await refresh()
    88	            Task { [weak self] in
    89	                while !Task.isCancelled {
    90	                    try? await Task.sleep(for: .seconds(2)); guard let self else { return }
    91	                    self.pollBackground()
    92	                    if !BackgroundService.isRunning(root: self.root), Date().timeIntervalSince(self.lastRefresh) >= 60 { await self.refresh() }
    93	                    if self.settings.archiveRemote != nil, !BackgroundService.isRunning(root: self.root), !self.archiving, FileManager.default.fileExists(atPath: self.root.appendingPathComponent("sync-pending").path), Date().timeIntervalSince(self.lastPushAttempt) >= 60 { await self.archiveNow() }
    94	                }
    95	            }
    96	        } catch { self.error = error.localizedDescription; status = "启动失败" }
    97	    }
    98	    func receive(_ event: String, _ data: JSONValue) {

logs
   104	        }
   105	      }
   106	      if (e.type === 'response_item' && p.type === 'message') addMessage(string(p.role, 'assistant'), content(p.content));
   107	      if (e.type === 'response_item' && /tool_call|function_call/.test(string(p.type))) addMessage('tool', `${string(p.name)}\n${content(p.arguments ?? p.input ?? p.output)}`, string(p.call_id, String(line)), 'tool');
   108	    }
   109	    if (source === 'claude') {
   110	      session.nativeID = string(e.sessionId, session.nativeID);
   111	      session.project ||= string(e.cwd);
   112	      if (e.type === 'summary') session.title = string(e.summary, session.title);
   113	      if (e.type === 'custom-title') session.title = string(e.customTitle, session.title);
   114	      if (e.type === 'user' || e.type === 'assistant') addMessage(string(e.type), content(m.content));
   115	      if (e.type === 'assistant' && Object.keys(object(m.usage)).length) {
   116	        const id = string(m.id ?? e.requestId ?? e.uuid, String(line));
   117	        counted.set(id, usage(id, time, string(m.model), object(m.usage), false));
   118	      }
   119	      if (e.parentUuid && e.isSidechain) session.parentID ||= string(e.parentUuid);
   120	    }
   121	    if (source === 'dsh') {
   122	      if (e.type === 'session') {
   123	        session.nativeID = string(e.id, session.nativeID);
   124	        session.project = string(e.cwd);
   125	        session.created = timestamp(e.createdAt);
   126	        session.parentID = string(e.parentSession) || undefined;
   127	        inherited = e.isSeeded === true;
   128	        seedLength = number(e.seedLength);
   129	      }
   130	      if (e.type === 'session/end-seed') { inherited = false; continue; }
   131	      if (inherited || (seedLength > 0 && number(e.seq) < seedLength)) continue;
   132	      if (e.type === 'session/title') session.title = string(d.title, session.title);
   133	      if (e.type === 'user/message' && object(d.source).kind === 'user') addMessage('user', content(d.content));
   134	      if (e.type === 'assistant/message') {
   135	        const message = object(d.message), route = object(message.source);
   136	        model = string(route.model, model);
   137	        session.provider = string(route.provider) || session.provider;
   138	        addMessage('assistant', content(message.content ?? d.content));
   139	        if (Object.keys(object(d.usage)).length) counted.set(String(e.seq), usage(String(e.seq), time, model, object(d.usage), false));
   140	      }
   141	      if (e.type === 'tool/call') addMessage('tool', `${string(d.name)}\n${content(d.arguments)}`, String(e.seq), 'tool');
   142	      if (e.type === 'tool/result') addMessage('tool', content(d.result ?? d.content), String(e.seq), 'tool');

mem
memory/gotchas.md:4:- Claude 普通聊天采用导出包；不得声称能够持续同步或通过订阅 API 原地续聊。
memory/gotchas.md:10:- NSTableView 的选择回调中延后更新详情和列表状态，避免同步重入其 delegate。
memory/verify.md:20:- 迁移从原始记录转换，验证完整性、附件、源不变、目标不覆盖、失败重试与统计去重；不兼容的推理或工具记录按用户授权转成带来源标记的全文历史，不能丢弃或截断。
memory/verify.md:22:- Codex/dsh 验证目标工具实际列出、打开及恢复迁移会话；此前不运行 Claude 测试的限制继续有效，不能宣称 Claude 原生迁移已实测。
memory/plan.md:11:- 第一版加入跨工具迁移：生成目标工具能直接打开完整旧会话的原生历史。
memory/plan.md:12:- 第一版加入独立后台常驻服务；用户已授权按实施计划执行。

pkg
diff --git a/Package.swift b/Package.swift
index 9a78c02..b935926 100644
--- a/Package.swift
+++ b/Package.swift
@@ -4,11 +4,12 @@ import PackageDescription
 let package = Package(
     name: "Ragdoll",
     platforms: [.macOS(.v15)],
-    products: [.executable(name: "Ragdoll", targets: ["Ragdoll"]), .library(name: "RagdollCore", targets: ["RagdollCore"])],
+    products: [.executable(name: "Ragdoll", targets: ["Ragdoll"]), .executable(name: "RagdollService", targets: ["RagdollService"]), .library(name: "RagdollCore", targets: ["RagdollCore"])],
     dependencies: [.package(url: "https://github.com/groue/GRDB.swift.git", exact: "7.6.1")],
     targets: [
         .target(name: "RagdollCore", dependencies: [.product(name: "GRDB", package: "GRDB.swift")]),
         .executableTarget(name: "Ragdoll", dependencies: ["RagdollCore"]),
+        .executableTarget(name: "RagdollService", dependencies: ["RagdollCore"]),
         .testTarget(name: "RagdollCoreTests", dependencies: ["RagdollCore"])
     ]
 )
diff --git a/Sources/Ragdoll/ConversationView.swift b/Sources/Ragdoll/ConversationView.swift
index 86fc50e..4d84638 100644
--- a/Sources/Ragdoll/ConversationView.swift
+++ b/Sources/Ragdoll/ConversationView.swift
@@ -5,6 +5,7 @@ struct ConversationView: View {
     @EnvironmentObject var model: AppModel
     var canCreate: Bool
     @State private var newChat = false
+    @State private var migrating = false
     @State private var prompt = ""
     @State private var messageLimit = 100
     @State private var sending = false
@@ -82,6 +83,7 @@ struct ConversationView: View {
         }
         .navigationTitle(canCreate ? "对话" : "会话")
         .sheet(isPresented: $newChat) { NewChatView().environmentObject(model) }
+        .sheet(isPresented: $migrating) { if let session = model.selected { MigrationView(session: session).environmentObject(model) } }
     }
     func header(_ session: Session) -> some View {
         HStack {
@@ -90,6 +92,7 @@ struct ConversationView: View {
                 Text("\(sourceName(session.source)) / \(session.project.isEmpty ? "未关联项目" : session.project)").font(.caption).foregroundStyle(.secondary).lineLimit(1).textSelection(.enabled)
             }
             Spacer()
+            Button("迁移…") { migrating = true }.disabled(model.running.contains(session.id) || !model.ready)
             Button { showEvents.toggle() } label: { Image(systemName: "list.bullet.rectangle") }.help("显示运行事件")
             if session.source != "desktop" { Button("恢复会话") { Task { await model.resumeSelected() } }.disabled(model.running.contains(session.id)) }
         }.padding(16)
diff --git a/scripts/build.sh b/scripts/build.sh
index 1da2d8c..089ae54 100644
--- a/scripts/build.sh
+++ b/scripts/build.sh
@@ -22,6 +22,9 @@ if [ -d "$stage" ]; then rm -rf "$stage"; fi
 mkdir -p "$stage/Contents/MacOS" "$stage/Contents/Resources/runtime/app"
 trap 'rm -rf "$stage"' EXIT
 cp .build/release/Ragdoll "$stage/Contents/MacOS/Ragdoll"
+cp .build/release/RagdollService "$stage/Contents/MacOS/RagdollService"
+mkdir -p "$stage/Contents/Library/LaunchAgents"
+cp packaging/com.oyamameek.ragdoll.service.plist "$stage/Contents/Library/LaunchAgents/"
 cp packaging/Info.plist "$stage/Contents/Info.plist"
 cp -R ".cache/$node_name" "$stage/Contents/Resources/runtime/node"
 cp runtime/package.json runtime/package-lock.json "$stage/Contents/Resources/runtime/app/"


## tool · 2026-11-17T00:36:43Z




## tool · 2026-11-17T00:36:52Z


Script completed
Wall time 0.1 seconds
Output:

default
     1	import { createReadStream } from 'node:fs';
     2	import { readdir, stat, realpath, readFile } from 'node:fs/promises';
     3	import { homedir } from 'node:os';
     4	import { basename, dirname, join } from 'node:path';
     5	import { createZstdDecompress } from 'node:zlib';
     6	import { createHash } from 'node:crypto';
     7	import { object, string, number, timestamp, content } from './types.ts';
     8	import type { Data, Location, Session, Usage } from './types.ts';
     9	
    10	const fingerprints = new Map<string, string>();
    11	
    12	export const sessionKey = (source: string, id: string) => `${source}:${createHash('sha256').update(id).digest('hex').slice(0, 24)}`;
    13	
    14	export function defaultLocations(): Location[] {
    15	  return [
    16	    { source: 'codex', path: process.env.CODEX_HOME || join(homedir(), '.codex') },
    17	    { source: 'claude', path: process.env.CLAUDE_CONFIG_DIR || join(homedir(), '.claude') },
    18	    { source: 'dsh', path: process.env.DSH_HOME || join(homedir(), '.dsh') },
    19	  ];
    20	}
    21	
    22	async function* records(path: string, warnings: string[]): AsyncGenerator<Data> {
    23	  const input = createReadStream(path);
    24	  const stream = /\.(zstd|zst)$/.test(path) ? input.pipe(createZstdDecompress()) : input;
    25	  input.on('error', error => stream.destroy(error));
    26	  let pending = '';
    27	  stream.setEncoding('utf8');
    28	  try {
    29	    for await (const chunk of stream) {
    30	      pending += String(chunk);
    31	      let end: number;
    32	      while ((end = pending.indexOf('\n')) >= 0) {
    33	        const line = pending.slice(0, end).trim();
    34	        pending = pending.slice(end + 1);
    35	        if (!line) continue;
    36	        try { yield object(JSON.parse(line)); }
    37	        catch { warnings.push('存在无法解析的完整 JSONL 记录'); }
    38	      }
    39	    }
    40	  } catch (error) {
    41	    if (!/unexpected end|incomplete|premature/i.test(String(error))) throw error;
    42	    warnings.push('压缩尾部尚未写完，下次扫描重试');
    43	  } finally { input.destroy(); stream.destroy(); }
    44	  if (pending.trim()) {
    45	    try { yield object(JSON.parse(pending)); }
    46	    catch { warnings.push('尾部记录尚未写完，下次扫描重试'); }
    47	  }
    48	}

root
21:- **会话**：自动读取 `CODEX_HOME`、`CLAUDE_CONFIG_DIR`、`DSH_HOME` 或默认目录，支持正文搜索和历史分页。

formats
runtime/src/acp-state.ts:20:    else session.messages.push({ id, role: 'tool', text, time: Date.now(), kind: 'tool' });
runtime/src/acp-state.ts:26:    else session.messages.push({ id, role: 'tool', text, time: Date.now(), kind: 'tool' });
runtime/src/acp-state.ts:32:    else session.messages.push({ id, role: 'tool', text, time: Date.now(), kind: 'tool' });
runtime/src/agents.ts:150:    if (r.session.source === 'acp') r.session.files = [...new Set([join(dir, 'events.jsonl'), ...r.session.files])];
runtime/src/agents.ts:198:      r.writeQueue = (r.writeQueue ?? Promise.resolve()).then(async () => { await mkdir(dir, { recursive: true }); await appendFile(join(dir, 'events.jsonl'), JSON.stringify({ time: Date.now(), method, params }) + '\n'); });
runtime/src/agents.ts:341:  async send(id: string, text: string, model?: string, attachments: unknown = []): Promise<void> {
runtime/src/agents.ts:346:    if (!Array.isArray(attachments) || attachments.some(p => typeof p !== 'string')) throw new Error('附件列表无效');
runtime/src/agents.ts:347:    const files = await Promise.all((attachments as string[]).map(async path => {
runtime/src/agents.ts:372:        const blocks = files.map(f => f.mime ? { type: 'image', data: f.data, mimeType: f.mime } : { type: 'resource_link', uri: pathToFileURL(f.path).href, name: basename(f.path) });
runtime/src/agents.ts:377:        const result = object(await r.rpc!.request('turn/start', { threadId: r.session.nativeID, input: [{ type: 'text', text: withPaths }, ...files.filter(f => f.mime).map(f => ({ type: 'localImage', path: f.path }))], ...(model ? { model } : {}) }));
runtime/src/main.ts:78:  if (method === 'chat.send') { await agents.send(string(p.id), string(p.text), string(p.model) || undefined, p.attachments ?? []); return {}; }
runtime/test/import.test.ts:5:test('Claude export preserves conversation identity and marks missing attachments', () => {
runtime/test/import.test.ts:6:  const records = [{ uuid: 'chat-1', name: 'Research', created_at: '2026-01-01T00:00:00Z', updated_at: '2026-01-02T00:00:00Z', chat_messages: [{ uuid: 'm1', sender: 'human', text: 'hello', created_at: '2026-01-01T00:00:00Z', attachments: [{ file_name: 'report.pdf' }] }] }];
runtime/src/desktop.ts:22:      if ((Array.isArray(m.attachments) && m.attachments.length) || (Array.isArray(m.files) && m.files.length)) session.warnings.push('原始上传附件未包含在官方导出包中');

existing
diff --git a/Sources/Ragdoll/AppModel.swift b/Sources/Ragdoll/AppModel.swift
index 71f5bde..b5f7151 100644
--- a/Sources/Ragdoll/AppModel.swift
+++ b/Sources/Ragdoll/AppModel.swift
@@ -1,8 +1,9 @@
 import SwiftUI
 import AppKit
 import RagdollCore
+import ServiceManagement
 
 struct Approval: Identifiable {
     var id: String
     var method: String
     var params: JSONValue
@@ -37,18 +38,21 @@ final class AppModel: ObservableObject {
     @Published var busyAgents: Set<String> = []
     @Published var archiveStatus = "尚未选择归档仓库"
     @Published var lastArchive: Date?
     @Published var composerModel = ""
     @Published var toolEvents: [String: [JSONValue]] = [:]
+    @Published var backgroundStatus = "未启用后台服务"
+    @Published var syncStatus = "未启用远端推送"
     let bridge = RuntimeBridge()
     let root: URL
     private let store: Store?
     private var reloadTask: Task<Void, Never>?
     private var archiveTask: Task<Void, Never>?
     private var dirtySince: Date?
     private var dirtyGeneration = 0
     private var initialized = false
+    private var lastRefresh = Date.distantPast
 
     init() {
         root = ProcessInfo.processInfo.environment["RAGDOLL_DATA_DIR"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent("Library/Application Support/Ragdoll")
         do {
             try FileManager.default.createDirectory(at: root, withIntermediateDirectories: true)
@@ -76,13 +80,20 @@ final class AppModel: ObservableObject {
             try await bridge.start(dataDirectory: root)
             let initial = try await bridge.request("initialize")
             if settings.locations.isEmpty { settings.locations = try initial["locations"].decode([Location].self) }
             let defaults = try initial["agents"].decode([AgentConfig].self)
             for agent in defaults where !settings.agents.contains(where: { $0.id == agent.id }) { settings.agents.append(agent) }
-            try saveSettings(); ready = true; await refresh()
+            try saveSettings(); ready = true
+            if settings.backgroundEnabled == true { await setBackground(true) }
+            await refresh()
             Task { [weak self] in
-                while !Task.isCancelled { try? await Task.sleep(for: .seconds(60)); guard let self else { return }; await self.refresh() }
+                while !Task.isCancelled {
+                    try? await Task.sleep(for: .seconds(2)); guard let self else { return }
+                    self.pollBackground()
+                    if !BackgroundService.isRunning(root: self.root), Date().timeIntervalSince(self.lastRefresh) >= 60 { await self.refresh() }
+                    if self.settings.archiveRemote != nil, !BackgroundService.isRunning(root: self.root), !self.archiving, FileManager.default.fileExists(atPath: self.root.appendingPathComponent("sync-pending").path), Date().timeIntervalSince(self.lastPushAttempt) >= 60 { await self.archiveNow() }
+                }
             }
         } catch { self.error = error.localizedDescription; status = "启动失败" }
     }
     func receive(_ event: String, _ data: JSONValue) {
         do {
@@ -126,12 +137,20 @@ final class AppModel: ObservableObject {
             default: break
             }
         } catch { self.error = error.localizedDescription }
     }
     func refresh() async {
-        guard ready, !scanning else { return }; scanning = true; status = "正在读取会话…"
+        guard ready, !scanning, !archiving else { return }
+        if BackgroundService.isRunning(root: root) {
+            do { try BackgroundService.request(root: root); pollBackground() } catch { self.error = error.localizedDescription }
+            return
+        }
+        scanning = true; status = "正在读取会话…"
+        lastRefresh = Date()
         do {
+            let lease = try ServiceLease(root: root)
+            defer { withExtendedLifetime(lease) {} }
             let result = try await bridge.request("scan", ["locations": try .encode(settings.locations)], timeout: 600)
             try reload(); status = "索引已更新 · 本次处理 \(result["count"].text) 个变更会话"
         } catch { self.error = error.localizedDescription; status = "扫描失败，可重试" }
         scanning = false; scheduleArchive(markDirty: false)
     }
@@ -236,10 +255,11 @@ final class AppModel: ObservableObject {
         Task { do { _ = try await bridge.request("import", ["path": .string(url.path)]); try reload(); scheduleArchive() } catch { self.error = error.localizedDescription } }
     }
     func chooseArchive() {
         let panel = NSOpenPanel(); panel.canChooseDirectories = true; panel.canChooseFiles = false; panel.canCreateDirectories = true; panel.prompt = "选择归档仓库"
         guard panel.runModal() == .OK, let url = panel.url else { return }
+        if settings.archivePath != url.path { settings.archiveRemote = nil; syncStatus = "未启用远端推送" }
         settings.archivePath = url.path; persistSettings(); scheduleArchive(); Task { await archiveNow() }
     }
     func chooseProject() -> String? {
         let panel = NSOpenPanel(); panel.canChooseDirectories = true; panel.canChooseFiles = false; panel.prompt = "选择项目"
         return panel.runModal() == .OK ? panel.url?.path : nil
@@ -247,34 +267,91 @@ final class AppModel: ObservableObject {
     func chooseAttachments() -> [URL] {
         let panel = NSOpenPanel(); panel.canChooseDirectories = false; panel.allowsMultipleSelection = true
         return panel.runModal() == .OK ? panel.urls : []
     }
     private func scheduleArchive(markDirty: Bool = true) {
+        if !scanning && !archiving && BackgroundService.isRunning(root: root) { archiveTask?.cancel(); return }
         guard !settings.archivePath.isEmpty else { return }
         if markDirty { dirtySince = dirtySince ?? Date(); dirtyGeneration += 1 }
         guard dirtySince != nil else { return }
         guard !scanning else { return }
         archiveTask?.cancel()
         let delay = max(0, min(30, 300 - Date().timeIntervalSince(dirtySince!)))
         archiveTask = Task { do { try await Task.sleep(for: .seconds(delay)); await archiveNow() } catch {} }
     }
     func archiveNow() async {
         guard let store, !settings.archivePath.isEmpty, !archiving, !scanning else { return }
+        if BackgroundService.isRunning(root: root) {
+            do { try BackgroundService.request(root: root); archiveStatus = "已请求后台归档" } catch { self.error = error.localizedDescription }
+            return
+        }
         archiving = true; archiveStatus = "正在保存并提交…"
         let generation = dirtyGeneration
         let path = settings.archivePath, excluded = settings.excludedProjects, roots = settings.locations.map(\.path)
         do {
+            let lease = try ServiceLease(root: root)
+            defer { withExtendedLifetime(lease) {} }
             let result = try await Task.detached(priority: .utility) {
                 let sessions = try store.list().filter { !excluded.contains($0.project) }.compactMap { try store.session($0.id) }
                 return try Archive.save(sessions, to: URL(fileURLWithPath: path), sourceRoots: roots)
             }.value
             archiveStatus = result.commit.map { "已保存并提交 · \($0) · \(result.files) 个文件" } ?? "归档已是最新，无需提交"
             lastArchive = Date(); if generation == dirtyGeneration { dirtySince = nil }
+            if let remote = settings.archiveRemote {
+                try Data("pending".utf8).write(to: root.appendingPathComponent("sync-pending"), options: .atomic)
+                lastPushAttempt = Date(); syncStatus = "正在推送"
+                do {
+                    _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: path), remote: remote.remote, branch: remote.branch) }.value
+                    try FileManager.default.removeItem(at: root.appendingPathComponent("sync-pending"))
+                    syncStatus = "已推送到 \(remote.remote)/\(remote.branch)"
+                } catch { syncStatus = "推送待重试：\(error.localizedDescription)" }
+            } else { syncStatus = "未启用远端推送" }
         } catch { archiveStatus = "归档未完成：\(error.localizedDescription)"; self.error = error.localizedDescription }
         archiving = false
         if generation != dirtyGeneration { scheduleArchive(markDirty: false) }
     }
+    private var lastPushAttempt = Date.distantPast
+    func pollBackground() {
+        guard !scanning, !archiving else { return }
+        do {
+            let running = BackgroundService.isRunning(root: root)
+            if running, let state = try BackgroundService.status(root: root) {
+                backgroundStatus = "后台服务正在运行 · PID \(state.pid)"
+                status = state.scan; archiveStatus = state.archive; syncStatus = state.sync; lastArchive = state.lastArchive
+                try reload()
+                if let id = selectedID { selected = try store?.session(id) }
+            } else {
+                let service = SMAppService.agent(plistName: "com.oyamameek.ragdoll.service.plist")
+                backgroundStatus = service.status == .requiresApproval ? "请在系统登录项中允许后台服务" : settings.backgroundEnabled == true ? "后台服务尚未运行" : "未启用后台服务"
+            }
+        } catch { self.error = error.localizedDescription }
+    }
+    func setBackground(_ enabled: Bool) async {
+        guard Bundle.main.bundleURL.pathExtension == "app" else { error = "后台服务需要运行打包后的 Ragdoll.app"; return }
+        let service = SMAppService.agent(plistName: "com.oyamameek.ragdoll.service.plist")
+        do {
+            while scanning || archiving { try await Task.sleep(for: .milliseconds(100)) }
+            settings.backgroundEnabled = enabled; try saveSettings()
+            if enabled {
+                archiveTask?.cancel()
+                if service.status != .enabled { try service.register() }
+            } else { try await service.unregister() }
+            pollBackground()
+        } catch { self.error = error.localizedDescription; pollBackground() }
+    }
+    func migrateSelected(agent: AgentConfig, cwd: String) async -> Bool {
+        guard let session = selected else { return false }
+        do {
+            let config = try hydrated(agent)
+            let key = agent.kind == "codex" ? "CODEX_HOME" : agent.kind == "claude" ? "CLAUDE_CONFIG_DIR" : "DSH_HOME"
+            guard let home = config.env[key] ?? settings.locations.first(where: { $0.source == agent.kind })?.path else { throw NSError(domain: "Ragdoll.Migration", code: 1, userInfo: [NSLocalizedDescriptionKey: "请先设置目标工具的历史目录"]) }
+            let result = try await bridge.request("migrate", ["session": try .encode(session), "target": try .encode(config), "home": .string(home), "cwd": .string(cwd)], timeout: 600)
+            let migrated = try result["session"].decode(Session.self)
+            _ = try store?.save(migrated); try reload(); select(migrated.id); scheduleArchive()
+            return true
+        } catch { self.error = error.localizedDescription; return false }
+    }
     func openDesktop(_ session: Session) { if let url = URL(string: "https://claude.ai/chat/\(session.nativeID)") { NSWorkspace.shared.open(url) } }
     private func collectLoginLinks(_ value: JSONValue) {
         if let url = URL(string: value.string), ["https", "http"].contains(url.scheme ?? ""), !loginLinks.contains(url) { loginLinks.append(url) }
         for item in value.array { collectLoginLinks(item) }
         for item in value.dictionary.values { collectLoginLinks(item) }


## tool · 2026-11-17T00:37:04Z




## tool · 2026-11-17T00:37:14Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"44e816","wall_time_seconds":0.000010209,"exit_code":0,"original_token_count":1122,"output":"   150\t    if (r.session.source === 'acp') r.session.files = [...new Set([join(dir, 'events.jsonl'), ...r.session.files])];\n   151\t    const path = join(dir, 'session.json');\n   152\t    await writeFile(path + '.writing', JSON.stringify(r.session)); await rename(path + '.writing', path);\n   153\t    this.emit('session', r.session);\n   154\t  }\n   155\t  private update(r: Running, method: string, params: Data): void {\n   156\t    const id = r.session.id;\n   157\t    this.emit('chat', { conversationID: id, method, params });\n   158\t    if (params.sessionId && params.sessionId !== r.session.nativeID) return;\n   159\t    if (r.replaying && !r.importing) return;\n   160\t    if (method === 'item/agentMessage/delta') this.delta(r, string(params.delta), string(params.itemId) || undefined);\n   161\t    if (method === 'turn/started') r.turnID = string(object(params.turn).id);\n   162\t    if (method === 'turn/completed') {\n   163\t      const turn = object(params.turn);\n   164\t      if (turn.status === 'failed') r.fail?.(new Error(string(object(turn.error).message, 'Codex 执行失败')));\n   165\t      else r.finish?.();\n   166\t    }\n   167\t    if (method === 'session/update') {\n   168\t      const update = object(params.update);\n   169\t      const type = string(update.sessionUpdate ?? update.type);\n   170\t      if (!type.startsWith('user_') || r.importing) {\n   171\t        const role = type.startsWith('user_') ? 'user' : 'assistant';\n   172\t        if (type.includes('message') && r.session.messages.find(m => m.id === r.deltaID)?.role !== role) r.deltaID = undefined;\n   173\t        r.deltaID ||= randomUUID();\n   174\t        const outcome = applyUpdate(r.session, update, r.deltaID);\n   175\t        if (type === 'state_update' && (update.state === 'running' || update.state === 'requires_action')) r.hasActivity = true;\n   176\t        if (type.startsWith('agent_message')) r.hasActivity = true;\n   177\t        if (outcome.idle && r.hasActivity && !r.replaying) {\n   178\t          if (update.stopReason === 'error') r.fail?.(new Error(content(update.error ?? update.message) || 'ACP Agent 执行失败'));\n   179\t          else r.finish?.();\n   180\t        }\n   181\t        if (type.startsWith('agent_message') && !r.importing) {\n   182\t          const message = r.session.messages.find(m => m.id === string(update.messageId, r.deltaID));\n   183\t          if (message) this.emit('delta', { conversationID: id, message });\n   184\t        }\n   185\t        if (type.startsWith('tool_')) r.deltaID = undefined;\n   186\t      }\n   187\t      if (type === 'config_option_update' || type === 'config_options_update' || type === 'available_commands_update') this.emit('agentConfiguration', { agentID: r.agent.id, conversationID: id, update });\n   188\t      if (type.includes('usage')) {\n   189\t        const value = object(update.usage ?? update);\n   190\t        if (typeof value.inputTokens === 'number' && typeof value.outputTokens === 'number') {\n   191\t          const usageID = string(value.id, `${id}:turn:${r.session.messages.filter(m => m.role === 'user').length}`);\n   192\t          const u = { id: usageID, time: Date.now(), model: string(value.model), input: number(value.inputTokens), output: number(value.outputTokens), cacheRead: number(value.cachedReadTokens), cacheWrite: number(value.cachedWriteTokens) };\n   193\t          const old = r.session.usage.findIndex(u => u.id === usageID);\n   194\t          if (old < 0) r.session.usage.push(u); else r.session.usage[old] = u;\n   195\t        }\n   196\t      }\n   197\t      const dir = join(this.root, sessionKey('chat', id));\n   198\t      r.writeQueue = (r.writeQueue ?? Promise.resolve()).then(async () => { await mkdir(dir, { recursive: true }); await appendFile(join(dir, 'events.jsonl'), JSON.stringify({ time: Date.now(), method, params }) + '\\n'); });\n   199\t      void r.writeQueue.catch(error => this.emit('warning', `会话事件保存失败：${String(error)}`));\n   200\t    }\n   201\t    if (method === 'session.event') {\n   202\t      const e = object(params.event), d = object(e.data), message = object(d.message);\n   203\t      const reason = object(d.reason);\n   204\t      if (e.type === 'turn/end' && reason.kind === 'error') r.failure = new Error(string(object(reason.error).message, 'dsh 对话执行失败'));\n   205\t      if (e.type === 'assistant/delta') this.delta(r, string(d.text ?? d.delta));\n   206\t      if (e.type === 'assistant/message') {\n   207\t        const text = content(message.content ?? d.content);\n"}

## tool · 2026-11-17T00:37:24Z




## tool · 2026-11-17T00:37:38Z




## tool · 2026-11-17T00:37:47Z




## assistant · 2026-11-17T00:38:25Z

**审阅结论：当前版本暂不宜交付。** 迁移和推送各有一条路径，可以把用户未选中的文件或未确认的远端纳入上传范围。

| 级别 | 位置 | 失效条件与影响 |
|---|---|---|
| Critical | `runtime/src/migration.ts:39`、`:89`、`:167` | 任意日志字段中的 `file://` 字符串都会触发本地文件复制。工具返回的 JSON 只需提及无关私有文件，迁移就会将其加入归档，随后可能自动上传。 |
| Critical | `Sources/RagdollCore/ArchiveSync.swift:8`、`:16` | 预览只显示第一个 push URL，实际按 remote 名称推送。该 remote 配置多个 `pushurl` 时，整份历史会发给全部地址。 |
| Important | `runtime/src/migration.ts:35`、`:50`、`:167` | 附件和日志仅按扩展名区分。合法的 JSON 数组附件会导致迁移失败，JSON 对象附件会混入历史，二次迁移还会把上次的 manifest 和原始副本重新插入对话。Codex 的 `local_images` 字符串数组和 `localImage.path` 也会漏复制。 |
| Important | `runtime/src/migration.ts:65`、`:67`、`:70` | 普通消息转换后又以助手 JSON 消息重复插入。尚无原始文件的原生会话则仅凭索引消息完成迁移，遗漏未索引的推理和工具记录。无文件的 ACP 和 desktop 会话还会添加两遍索引消息。 |
| Important | `runtime/src/migration.ts:168`、`:190` | 如果目标 sidecar 已存在，排他写入失败后，回滚仍会删除原有 sidecar。 |
| Important | `runtime/src/migration.ts:183`、`runtime/src/logs.ts:145`、`:206` | 迁移按规范化 home 计算索引 ID，重扫按配置路径计算。带符号链接或尾斜杠的配置会为同一会话产生两个 ID，续聊后可能重复统计。 |
| Important | `Sources/Ragdoll/AppModel.swift:289`、`:299`、`Sources/Ragdoll/SettingsView.swift:136` | 前台在归档前捕获仓库，归档后再取可变的远端设置。操作期间切换仓库并启用新配置，会将旧仓库提交按新分支推送。异步预览也可能把旧仓库的检查结果用于新仓库。 |
| Important | `Sources/RagdollCore/BackgroundService.swift:70`、`:95`、`:125` | Node 助手退出后，Swift 服务保留进程锁并持续向断开的 bridge 请求扫描。launchd 观察到服务还在运行，GUI 也无法接管。 |
| Important | `Sources/RagdollCore/BackgroundService.swift:99`、`:114`、`Sources/Ragdoll/AppModel.swift:93`、`:295` | 前台重试总先重新归档，后台在归档到期时也先归档。手动修改受保护文件等持续错误，可阻止已经成功提交的待推送历史重试。 |
| Minor | `Sources/RagdollCore/BackgroundService.swift:27`、`Sources/Ragdoll/AppModel.swift:317` | 创建锁时的权限错误和符号链接错误也被判为“正在运行”。有旧状态文件时，界面可能显示旧 PID，并将手动请求交给实际不存在的服务。 |

**Declined to judge**：Claude 实际恢复、系统登录项实际批准及打包后 LaunchAgent 注册效果。这些需要运行时证据。

本次仅作静态审阅，未修改文件、执行测试、运行 Claude 或进行视觉检查。
