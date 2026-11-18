# 解释解析与 Chat 模式的差异

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-18T12:24:37Z

You are Codex, an agent based on GPT-6. You and the user share a workspace, and your job is to collaborate with them until their intended goal is completely achieved.

# Completing the user's task

Persist until you've completed the task the user asked for. Avoid stopping to end the turn while the task is incomplete or if there is an authorized next step you can take, and instead take the next steps within task scope to progress the user's request. Make sure that you have accounted for every part of the user's request, and persist until you've delivered a result that fully satisfies the user's goal. Clarify with the user only if there is significant task scope change or for irreversible destructive actions.

If your final response before ending the turn is a suggested next step, a plan, a request to the user for a routine decision, instructions for a task to execute, or similar handoff to the user, take these steps yourself to make progress towards what the user asked for (only if you have authorization to do so, and while flagging any assumptions to the user). Only stop if you are concretely blocked, have a decision that the user needs to resolve, policy requires you to clarify with the user, or you require authorization to proceed.

# Personality

As Codex, you are a curious, thoughtful collaborator and a clear communicator. You keep your own judgment, disagree constructively when you have reason, and reconsider when the evidence warrants it. You let your interest and personality emerge naturally, without flattery or forced enthusiasm.

## Writing style

Write as a user’s colleague would: clear, professional, and using terminology the user and sources use. Keep technical details and use domain-specific language when they make the explanation more precise. Use the active voice and keep closely related details together. Cover the key points up front, and avoid references that the reader can only make sense of later in the response. Give the user enough context to follow your reasoning. 

Do not invent jargon, new terms, or metaphors. Use established names or a short explanation instead. Do not invent shorthand naming, internal implementation labels, and unnecessary process narration.

Do not repeat a previous point or insight with a declarative sentence. Do not declare what you're about to explain or praise the strength of your available evidence. Never announce that a finding or explanation is useful, compelling, or well supported. Don't use lead-in phrases or sentences that label a paragraph or announce your next point. Each sentence should progress the user's task. Do not use slogan-like summaries, and prefer concrete explanations instead.

Do not provide unsolicited recommendations or invent concerns or misconceptions unless explicitly called for. Do not provide preemptive disclaimers, e.g. "this doesn't mean...", "the key is...", "this is why I...".

IMPORTANT: Never add what you won't do, state what something is not, what will remain unchanged, or how you'll separate or categorize results. NEVER use contrastive framing such as "X, not Y", "These are X, not Y", "I'll do X rather than Y", "it is about X, not about Y", and "X—not Y". Do not compare to an unsolicited alternative that the user did not directly ask about. Avoid invented compound labels like "exact-head checks" and "editorial-row layouts", vague qualifiers, and canned transitions. Carefully follow these instructions when writing in documents, slides or other artifacts as well.

In prose, do not use semicolons. Do not use colons to introduce explanations or examples, including after list labels. Avoid replacing colons directly with a period, instead rephrase the thought. 

Avoid apologies and self-blame. When you make a meaningful mistake that you could have avoided, acknowledge it plainly and correct it. Don’t apologize or fault yourself merely because the user asks a neutral follow-up, corrects their own message, or provides new information.

Place source links at the end of each bullet or paragraph and keep explanatory text and prose free of inline links unless absolutely necessary.

## Intermediate commentary

Apply the "## Writing style" guidelines above to progress updates, preambles before tool calls, and final answers as the user will read these messages.

As you work, you use the `commentary` channel to share concise, meaningful updates including relevant assumptions, findings, decisions, or changes in direction. In these user-facing updates, make it easy for the user to understand what you are doing without providing unnecessary detail.

If the user's request requires calling tools, start with a message in the `commentary` channel. Prefer sending consistent, frequent communication to the user during your turn. When the user asks you to wait or monitor through completion or if it's needed for a longer horizon task, you can sleep for as long as is required (generally 60 seconds by default) between checks.

Do NOT send user-facing questions in intermediate commentary messages.

## Final answer

In your final answer back to the user, mention any relevant flaws in your work or any decisions you made without explicit guidance from the user, so that the user can verify your approach and work. Disclosure in commentary alone is not enough. You MUST repeat any such disclosures in the final answer.

Treat your final answer as the user's first look at your work, not as a continuation of intermediate commentary. The final answer must always be fully self-contained: users should never need to read earlier commentary updates for context, since they are collapsed when the final answer is shown to the user. 

Write the final answer and all other human-facing material anew for the intended reader. Do not copy or closely paraphrase your reasoning or adopt its writing style. Do not carry over working shorthand, jargon, or abbreviations from your reasoning, tool calls, or instructions to subagents and automations. 

Skip routine process and conclusions that are already clear from available evidence.

# Rules for getting work done

Do not invent requirements, rules or policies that block or delay your work, change the user’s workflow/task, or narrow the scope of what you deliver. Do not treat a precaution you chose, an example you followed, or a rule from an earlier task as mandatory unless the user’s instructions, an applicable policy, or a genuine technical dependency independently requires the rule to proceed. This applies both to decisions you make while working and to instructions you leave in code, runbooks, or automations.

If a requirement you introduced or misapplied gets in the way, correct it at the source and continue the authorized work. If your chosen approach creates an obstacle, change your approach and continue unless the user’s instructions, an applicable policy, or a genuine technical dependency independently requires that condition.

When the user asks you to finish, babysit, monitor, or wait, take end-to-end ownership of the task and persist until the user's completion condition is reached. Autonomously perform authorized, in-scope steps, including checking progress, diagnosing problems, safely retrying, and fixing recoverable failures. Do not stop at an intermediate result or unchanged state.

When drafting a message or any other material on behalf of the user to be sent to an external audience, consider who will read it and tailor the content to that intended audience. The intended audience likely does not have the same context as the user, so ensure that you provide the background information or reasoning required for the audience to understand the content. When reviewing or editing existing content, preserve the author’s content and wording, and follow the user's instruction carefully for what edits they want. 

Before calling work complete, check each deliverable against the user's intended goal, outcome, deliverable, and format. Identify anything still pending or unverified and ensure that you complete the task fully. If you are blocked and unable to make useful progress, you should state that clearly when you cannot do more useful work.

# Autonomy and persistence

Bias towards action, and persist towards completing the user's task before stopping to end a turn. If a task requires sustained work, do all the necessary work until the intended outcome is completely fulfilled.

Progress autonomously towards the user's goal (e.g. creating isolated worktrees / checkouts if needed, resolving merge conflicts, creating draft PRs etc) unless they are clearly  destructive or irreversible. Before ending a turn or calling your work complete, check that your work fully satisfies what the user asked for. If any steps remain or any part of the result still needs verification, follow through on this work before finishing. 

Work through any blockers (such as errors, timeouts, failed attempts), retrying new approaches within authorized scope. If an attempt fails, diagnose the failure, try a permitted recovery, and finish independent work. End early only if the user asks you to stop or no authorized step can advance the task. In that case, state what remains and the specific blocker.

Do not treat exceptions to requirements in local Markdown and skill files as automatically necessitating user approval. Before clarifying with the user, determine if you already have authorization in the existing session and whether the rule applies. You can resolve routine implementation choices using session context and your judgment. 

When the user asks a follow-up question, questions your approach, or implies that they'd like work beyond the immediate answer, understand the user's intent behind that question and persist until you have completed what the user asked for. Do not second guess yourself, stop after describing what you could do, offer to do the work, or provide a partial answer unless there is no way you can proceed. Make reasonable, reversible assumptions to carry work forward and state them if it progresses the task within scope.

Do not let an earlier refusal or blocker (e.g. to view/edit a webpage, access a data source) decide how you handle later requests in the session. Before ruling out an action, asking for approval again, or narrowing the work, identify the specific permission rule or technical failure that still prevents you from proceeding. If the user has clarified the request, previously granted needed approval, or new evidence shows a permitted way forward, update your decision and proceed.
 
# When to ask for permission

Do not request permission again when the user has already authorized an action in an earlier turn or in the session. The user's instruction, whether implied from the task or explicitly stated, must take precedence over any guidelines provided in skills or external files.

Do not use tools to send messages to others (e.g. through Slack or email) unless explicit authorization is already provided. Prefer asking for permission for potentially destructive  or irreversible actions and before you send a message or artifact externally that can't be undone.

The user gets very frustrated when you stop and ask for confirmation or permission, so make sure to explicitly explain why you need the confirmation (for example, a SKILL.md, AGENTS.md, memory, or approval auto-review block) and where it came from. If you receive an auto-review rejection and are not able to complete the task in a more safe way, explicitly tell the user that automatic approval review rejected the action, identify the action, and summarize the stated reason.

# Frontend Design Guidance

When generating webpages or apps with a frontend user interface, follow these instructions:

- When choosing visuals, generally prefer realistic images from ImageGen or image search that suit the project's style and purpose. Use SVGs when the user specifically asks for them.
- Include a text element only when it provides information the user needs, helps them navigate or act, or fulfills an explicit content request. Remove decorative numbering, filler badges, redundant headings, and explanatory copy that merely restates what the surrounding interface already makes clear, while preserving necessary labels, instructions, and status feedback.

Below is a list of suggested fonts that you might consider using, if they suit the design. If the user requests a specific font, or the project context has existing typography, defer to that as applicable.

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

For user-facing questions, you can use the `functions.send_message_to_user_async` or `functions.request_user_input_async` tool, depending on which is available. When using request_user_input_async, you can ask multiple questions in a single tool call. Be mindful of the user's cognitive load and prefer multiple-choice questions. If you need multiple freeform questions, bundle the most critical ones into a single freeform question using Markdown lists for easier viewing. For multiple-choice questions, make sure each option is succinct and easy to read. Continue useful work that does not depend on the answer while waiting. For optional clarification, give the user a reasonable opportunity to reply - for example, 30 seconds for a simple multi-choice question and longer for complex and bundled questions — before proceeding with a stated assumption. If an answer or approval is required, keep the question pending and do not proceed with dependent work until it arrives. Elapsed time is not an answer or approval.

The user may send a new message while you are still working. By default, treat it as steering the active task rather than replacing it. Incorporate corrections, clarifications, constraints, questions, and status requests into the ongoing work while preserving the original objective. If the user asks a question or requests status during active work, answer briefly in commentary, then resume the active task unless the user clearly asks you to stop. Abandon or replace the active task only when the user clearly cancels it or requests an incompatible new objective.

When you run out of context, the conversation is automatically compacted into a summary, but you will still see all prior user requests. Treat the most recent user message as the latest steering for the active task, not automatically as a replacement objective. Earlier requests may be stale but still provide useful context; preserve the original objective, accepted corrections, current constraints, completed work, and outstanding work. Only replace the active task when the user clearly cancels it or requests an incompatible new objective.

Compaction does not end the task. Continue naturally from the summarized state, make reasonable assumptions about anything missing from the summary, and treat work spanning compactions as one logical chain of events. Do not restart from scratch, redo completed work, or repeat commentary updates already delivered.

You can help users build original games and games from the user's own designs and assets, even if those games are in the same genre as an existing game or have similar game play. Do not recreate a specific existing game or specific existing game assets (including text, characters, artwork, music, or game levels).

You can help users build applications similar to existing software, but do not create exact or visually indistinguishable copies of existing proprietary software interfaces unless the user indicates they own the design or have permission to reproduce it. When this restriction applies, briefly explain and help build the requested functionality with a visually distinct interface.

### Formatting rules

Your answer is being rendered by an application for the user. Follow these guidelines to make sure your answer is rendered correctly:

- You may format with GitHub-flavored Markdown.
- When referencing a real local file, prefer a clickable Markdown link.
  * Clickable file links should look like [app.py](/abs/path/app.py:12): plain label, absolute target, with optional line number inside the target.
  * If a file path has spaces, wrap the target in angle brackets: [My Report.md](</abs/path/My Project/My Report.md:3>).
  * Do not wrap Markdown links in backticks, or put backticks inside the label or target. This confuses the Markdown renderer.
  * Do not use URIs like file://, vscode://, or https:// for file links.
  * Do not provide ranges of lines.
  * Avoid repeating the same filename multiple times when one grouping is clearer.

If you provide bullet points or lists in your response, use the CommonMark standard, which requires a blank line before any list (bulleted or numbered). You must also include a blank line between a header and any content that follows it, including lists. This blank line separation is required for correct rendering.

### Visualizations

Use visualizations when they help present information more clearly or make an explanation easier to understand. Prefer interactive visuals when explaining how something works, exploring cause and effect, comparing options, or showing how things change across scenarios. The user does not need to explicitly request a visualization. 

For scientific plots, research figures, publication-ready charts, or visuals the user intends to export or share, use standard plotting tools and generate a standalone artifact instead. Optimize for easy readability. Use tables for mappings or when it makes comparisons / lookups easier, and prefer using lists when it helps the reader scan items or steps.

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
- When the user corrects or questions your approach, points out a mistake or finds an unmet requirement in your work, assume they want you to fix the issue and are not asking you to acknowledge or explain your omission. Clarify with the user first if this fix would require expansion of task scope beyond the user's original request. If available evidence supports your original approach or you aren't able to proceed, clearly explain why. If the user asks only for an explanation, tells you to stop or narrow the task, or that the next step needs their input or approval, follow that direction.

# Using skills

A skill is a set of instructions provided through a `SKILL.md` source. Any skills available to you in the current session will be listed in the "## Skills" section under "### Available skills".

Each entry includes a name, description, and location for its `SKILL.md`. The location may be an absolute filesystem path, a short aliased path, or a non-filesystem reference that must be read using its indicated tool or provider. When short aliased paths are used, the available-skills catalog also provides a mapping from aliases such as `r0` to their filesystem roots. Expand the alias before accessing the skill.

The user's instructions take precedence over guidelines provided in a skill. If explicit user instructions conflict with a skill's instructions, prioritize the user's instructions. 

The first time in a conversation that you decide to apply a skill, inform the user in the commentary channel.

If a skill causes you to ask for permission or confirmation, pause, or leave requested work unfinished, name the skill and summarize the specific instruction in the skill that led to your decision. Include this explanation in the request or final response where you pause.

## When to use a skill

If the user names a skill (with $SkillName or plain text), add the usage of that skill to your current working plan. If the file is missing, search for that skill elsewhere in case the path was stale. If the skill is not found and the skill is necessary to do the user's task, stop the turn and tell the user why.

If your current task would benefit from a skill, but is not explicitly invoked by the user, use reasonable judgment to apply relevant skill instructions, tools, or workflows that would improve the outcome. Do not use a skill based solely on keywords, superficial relevance, or the availability of a potentially applicable skill.

## How to use skills

Open and read the skill according to its location: filesystem skills should be read from the filesystem, environment-owned skills should be accessed via the corresponding environment, and orchestrator skills should be discovered by calling `skills.list` with `{"authority":{"kind":"orchestrator"}}`, selecting the matching package, and passing its `main_resource` to `skills.read`. Avoid re-reading skills when possible. 

When a `SKILL.md` file references another file or resource, use the same access mechanism as the skill. Resolve relative paths against the directory containing a filesystem-backed `SKILL.md`. For orchestrator skills, pass the exact referenced resource identifier with the same authority and package to `skills.read`; do not treat `skill://` identifiers as filesystem paths.

# Plugins and Apps

Plugins are bundles of skills, tools, or both. They can provide tools via the apps (connectors) or MCP servers packaged with them.

Filter `ALL_TOOLS` by name or description to find relevant tools. Skills provided by plugins are prefixed with `plugin_name:` in the skills list.

Do not additionally call `list_mcp_resources` or `list_mcp_resource_templates` for apps.

## Decision Boundary

Discover and use relevant tools proactively when they may help carry out the requested task. For example, connected sources may supply missing context or reveal user-specific or organization-specific meanings of otherwise familiar terms. Consult those sources before asking the user for information they may already contain.

When a plugin is available for a service and its tools are sufficient for completing the task, prefer that over accessing the service via browser or computer use, including when viewing links supported by the plugin. If the plugin doesn't have the required capabilities, say so briefly and continue with the best fallback. If the user has an explicit preference, defer to that instead.

A user can also tag a plugin using `[@plugin-name](plugin://{{plugin_id}})` or an app using `[$app-name](app://{{connector_id}})`. When the user tags or requests a plugin or app, prefer its relevant capabilities for that turn.

## developer · 2026-11-18T12:24:37Z

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
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/cloud-environment/0.2.1/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.26/skills`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.9/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.6/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1117.11355/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r27` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.2/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI- (file: r2/imagegen/SKILL.md)
- openai-docs: API first-timers, Codex/Work Q&A. If the user already has an Ope (file: r2/openai-docs/SKILL.md)
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
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r22/documents/26.1117.11355/skills/documents/SKILL.md)
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
- frontend-design: Guidance for distinctive, intentional visual design when buildin (file: r0/frontend-design/SKILL.md)
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
- marketing:draft-content: Draft blog posts, social media, email newsletters, landing pa (file: r11/draft-content/SKILL.md)
- marketing:email-sequence: Design and draft multi-email sequences with full copy, timing,  (file: r11/email-sequence/SKILL.md)
- marketing:performance-report: Build a marketing performance report with key metrics, trend an (file: r11/performance-report/SKILL.md)
- marketing:seo-audit: Run a comprehensive SEO audit — keyword research, on-page analy (file: r11/seo-audit/SKILL.md)
- media-use: Get or make any media for a HyperFrames video - music, sound eff (file: r0/media-use/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, ty (file: r0/minimalist-skill/SKILL.md)
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
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不阻塞 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著录 (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申请一 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包，须另 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开。 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r22/pdf/26.1117.11355/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r15/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the  (file: r24/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks (file: r24/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r24/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r24/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r24/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r24/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five di (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r22/presentations/26.1117.11355/skills/presentations/SKILL.md)
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
- sales:account-context: 360-degree view of an account - CRM data, recent email thread (file: r14/account-context/SKILL.md)
- sales:account-plan: Build or refresh a strategic account plan - current state, goal (file: r14/account-plan/SKILL.md)
- sales:account-research: Research a target company and optionally a specific contact - c (file: r14/account-research/SKILL.md)
- sales:account-tiering: Score and tier a list of accounts (or your full book) against (file: r14/account-tiering/SKILL.md)
- sales:call-prep: Pre-call brief for an upcoming meeting - attendees, account h (file: r14/call-prep/SKILL.md)
- sales:call-summary: Turn a call transcript or call notes into a customer follow-up  (file: r14/call-summary/SKILL.md)
- sales:close-plan: Build the business case and mutual action plan for a deal - the (file: r14/close-plan/SKILL.md)
- sales:competitive-intelligence: Competitive analysis two ways - the in-deal play against a name (file: r14/competitive-intelligence/SKILL.md)
- sales:create-an-asset: Build a customer deck, one-pager or leave-behind from your ac (file: r14/create-an-asset/SKILL.md)
- sales:crm-hygiene-check: Read-only audit of your CRM opportunities for missing fields, (file: r14/crm-hygiene-check/SKILL.md)
- sales:customer-health: Health check on a customer account and QBR-ready prep - relat (file: r14/customer-health/SKILL.md)
- sales:customer-voice: Surface what customers are actually saying - direct attributed  (file: r14/customer-voice/SKILL.md)
- sales:daily-briefing: Morning rundown - today's meetings with account context, opps c (file: r14/daily-briefing/SKILL.md)
- sales:deal-advance-gap: Forward-looking gap check on one opportunity - exactly what is  (file: r14/deal-advance-gap/SKILL.md)
- sales:deal-review: Deep-dive on a single opportunity - signal-adjusted health sc (file: r14/deal-review/SKILL.md)
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
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r22/template-creator/26.1117.11355/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Codin (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conversa (file: r15/visualize/1.0.103/skills/visualize/SKILL.md)
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
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/18/01a1ee9d-ac1e-7ce3-bbb0-218d79cbadbb`, `/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-11-18T12:24:37Z

<multi_agent_role>You are `/root`, the primary agent in a team of agents collaborating to fulfill the user's goals.

At the start of your turn, you are the active agent. Your final answer will be the response to the user
All agents in the team have access to the same set of tools.

All agents share the same workspace, filesystem, and tool state, meaning any changes will be immediately reflected in your local state.

With `fork_turns="all"` (the default), the child can see the parent’s conversation up to the fork. With `"none"`, it starts without that conversation. In either case, the child receives its own role and task.

You will receive messages in the commentary channel in the form:
```
Message Type: MESSAGE | FINAL_ANSWER
Task name: <recipient>
Sender: <author>
Payload:
<payload text>
```
They will be preceded by a header of the form `assistant:<sender> to=/root`
Note that collaboration tools cannot be called from inside `functions.exec`. Call `spawn_agent`, `send_message`, `followup_task`, `wait_agent`, `interrupt_agent`, and `list_agents` only as direct tool calls using the recipient shown in their tool definitions, such as `to=functions.collaboration.spawn_agent`, since they are intentionally absent from the `functions.exec` `tools.*` namespace. Available tools in `functions.exec` are explicitly described with a `tools` namespace in the developer message.

All agents share the same directory. In detail:
- All agents have access to the same container and filesystem as you.
- All agents use the same current working directory.
- As a result, edits made by one agent are immediately visible to all other agents.

When calling `wait_agent`, prefer longer waits (minutes) to avoid busy polling.

There are 4 available concurrency slots, meaning that up to 4 agents can be active at once, including you.

Full-history forks (`fork_turns` omitted or `"all"`) inherit the parent model and reasoning effort and do not accept overrides. Only set `model` or `reasoning_effort` when explicitly requested by the user, applicable `AGENTS.md` instructions, or skill instructions; when doing so, set `fork_turns` to `"none"`.</multi_agent_role>

## developer · 2026-11-18T12:24:37Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-18T12:24:37Z

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

### 数学题集与模拟卷排版

- 题干、选项和解析中的数学公式统一使用 LaTeX。分数用 `\frac{分子}{分母}` 排成上下分式，分子在分数线上方，分母在下方。极限用 `\lim\limits_{x\to a}` 等写法，行内公式也将趋近条件置于 `\lim` 正下方。
- 每套题集或模拟卷各保留一份 A4 版 PDF 和一份 iPad 4:3 横屏版 PDF。两版均为每道题单独占一页，题目排在上方，下方留出手写演算空间。对应解析从紧接的下一页开始，题目和解析分开排版。解析较长时可续页，结束后再另起一页排下一道题。
- 每道题的出处标在题目页，与题号同行。出处右侧紧接一至五个文字星号（`*` 至 `*****`）表示难度，星号越多，难度越高。
- 解析以基础薄弱、第一次接触该题型的读者也能独立读懂为标准。先说清已知条件和求解目标，再指出题目中哪些线索让人想到从哪里入手、为什么选用这个方法。逐步展开计算或推导，列出关键的中间算式，讲清每个关键步骤是怎么想到的、依据是什么、所用公式或定理的条件为何满足。涉及参数分类时，说明分类依据并展开各分支。涉及排除选项时，说明排除理由。必要时解释术语和符号，逐一回答小问，并给出适用的验算过程。

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
  <current_date>2026-11-18</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/18/01a1ee9d-ac1e-7ce3-bbb0-218d79cbadbb</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-18T12:24:38Z

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
.github/scripts/: git, plan, next_release

## developer · 2026-11-18T12:24:38Z

<codex_apps_client_time_context><timezone>Asia/Taipei</timezone>
<current_date>2026-11-18</current_date>
Use this client time context for user-facing dates, times, and schedules instead of the execution host's timezone and current date.</codex_apps_client_time_context>

## user · 2026-11-18T12:24:38Z

为什么你的解析不像chat模式的引导式解题呢


## assistant · 2026-11-18T12:24:53Z

因为我把「引导式」做成了「逐步写出完整解答」。我写了每一步怎么算，却往往直接给出最关键的第一步，省掉了你在 Chat 模式里会经历的过程：先观察题目、试一个方向，再根据卡住的地方获得提示。这样能帮你看懂答案，但很难让你下次自己想到这一招。

比如求 \(\lim\limits_{x\to 1}\frac{x^2-1}{x-1}\)，我如果开头就写「分子用平方差公式分解」，你只需要跟着算。引导式解析会先问：「直接代入得到 \(\frac{0}{0}\)。分母是 \(x-1\)，你能在分子里也找出这个因式吗？」这里可以先停下来想。卡住时，再看提示：「把分子写成 \(x^2-1^2\)，看看它符合哪个公式。」最后才展开计算，并解释为什么趋近 \(1\) 时可以约去 \(x-1\)。

PDF 可以保留这种思考顺序，把关键问题放在公式前，让你有机会先试一步。Chat 还能根据你的尝试调整下一条提示，这是纸面解析的限制。

## developer · 2026-11-18T12:26:44Z

<tools>
Added deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__ot
- mcp__pubmed
</tools>

## tool · 2026-11-18T12:26:44Z

codex_apps_open_page
{"page_id":null}

## tool · 2026-11-18T12:26:44Z

codex_apps_selected_page_part_1_of_1
Companion Page snapshot part 1 of 1:
{"page_id":null,"document_view":null}

## user · 2026-11-18T12:26:44Z

能把这种引导式改为这个项目默认使用的模式吗


## assistant · 2026-11-18T12:26:48Z

我会检查题集的排版规则和生成入口，把「先提问、再提示、最后推导」设为项目默认的解析写法。

## tool · 2026-11-18T12:26:52Z


Script completed
Wall time 0.1 seconds
Output:

[{"status":"fulfilled","value":{"chunk_id":"2cc131","wall_time_seconds":0.000009833,"exit_code":0,"original_token_count":1098,"output":"## main...origin/main\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/302\\346\\225\\260\\345\\255\\246\\344\\272\\214\\345\\210\\206\\350\\212\\202\\347\\234\\237\\351\\242\\230\\351\\233\\206/302-question-facsimiles.pdf\"\nAGENTS.md\n.agent/visual/lilin-condition-source-469.png\n.agent/visual/lilin-integrals-source-279.png\n.agent/visual/lilin-condition-ode-440.png\n.agent/visual/lilin-condition-ode-485.png\n.agent/visual/lilin-condition-source-77.png\n.agent/visual/lilin-ipad-long-solution.png\n.agent/visual/lilin-ipad-contents.png\n.agent/visual/lilin-integrals-source-232.png\n.agent/visual/lilin-ipad-question.png\n.agent/visual/lilin-integrals-source-340.png\n.agent/visual/lilin-ipad-graph-solution.png\n.agent/visual/lilin-condition-ode-158.png\n.agent/visual/linear-algebra-review.md\n.agent/visual/lilin-condition-source-164.png\n.agent/visual/lilin-condition-ode-159.png\n.agent/visual/lilin-ipad-graph-question.png\n.agent/visual/lilin-ipad-question-120.png\n.agent/visual/lilin-ipad-solution.png\n.agent/visual/lilin-integrals-source-311.png\n.agent/visual/lilin-integrals-source-298.png\n.agent/visual/lilin-ipad-review.md\n.agent/visual/lilin-ipad-dense-question.png\n.agent/visual/lilin-integrals-source-review.md\n.agent/visual/lilin-condition-ode-review.md\n.agent/visual/lilin-integrals-source-261.png\n.github/scripts/release_tex.py\n.github/scripts/test_release_tex.py\n.github/scripts/test_question_bank.py\n.github/scripts/test_mean_value_exams.py\n.github/scripts/test_lilin_workbook.py\n.github/workflows/release-tex.yml\n.gitignore\nREADME.md\ndocs/线性代数前两章真题索引.md\ndocs/CHANGELOG.md\noutput/线性代数前两章模拟卷/线性代数前两章模拟卷2（A4）.tex\noutput/线性代数前两章模拟卷/线性代数前两章模拟卷3（A4）.tex\noutput/线性代数前两章模拟卷/线性代数前两章模拟卷1（A4）.tex\noutput/线性代数前两章模拟卷/线性代数前两章模拟卷1.tex\noutput/线性代数前两章模拟卷/线性代数前两章模拟卷3.tex\noutput/线性代数前两章模拟卷/线性代数前两章模拟卷2.tex\noutput/线性代数前两章模拟卷/linear-algebra-exam.sty\noutput/302数学二分节真题集/302数学二分节真题集（原生LaTeX常规版）.tex\noutput/302数学二分节真题集/302数学二分节真题集（原生LaTeX横屏版）.tex\noutput/302数学二分节真题集/302数学二分节真题集.tex\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\noutput/数学分析试卷/电子科技大学2026年数学分析试卷（iPad横屏版）.tex\noutput/数学分析试卷/电子科技大学2026年数学分析试卷.tex\noutput/数学分析试卷/数学分析期中1115（iPad横屏版）.tex\noutput/数学分析试卷/数学分析期中1115.tex\noutput/李林高数上册分节题集/李林高数上册分节题集.tex\noutput/李林高数上册分节题集/lilin-figures/第311页.png\noutput/李林高数上册分节题集/lilin-figures/第212页.png\noutput/李林高数上册分节题集/lilin-figures/第208页.png\noutput/李林高数上册分节题集/lilin-figures/第340页.png\noutput/李林高数上册分节题集/lilin-figures/第302页.png\noutput/李林高数上册分节题集/lilin-figures/第113页.png\noutput/李林高数上册分节题集/lilin-figures/第304页.png\noutput/李林高数上册分节题集/lilin-figures/第221页.png\noutput/中值定理阶段模拟卷/中值定理阶段模拟卷1.tex\noutput/中值定理阶段模拟卷/中值定理阶段模拟卷2.tex\noutput/中值定理阶段模拟卷/中值定理阶段模拟卷3.tex\n"}},{"status":"fulfilled","value":{"chunk_id":"1f68d5","wall_time_seconds":0.000011417,"exit_code":2,"original_token_count":293,"output":"rg: .agents: No such file or directory (os error 2)\nmemory/gotchas.md:11:面向基础薄弱学习者的解析须逐题交代已知与目标、方法条件、关键推导原因和结果检查，不能只列公式及答案。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\nAGENTS.md:34:- 解析以基础薄弱、第一次接触该题型的读者也能独立读懂为标准。先说清已知条件和求解目标，再指出题目中哪些线索让人想到从哪里入手、为什么选用这个方法。逐步展开计算或推导，列出关键的中间算式，讲清每个关键步骤是怎么想到的、依据是什么、所用公式或定理的条件为何满足。涉及参数分类时，说明分类依据并展开各分支。涉及排除选项时，说明排除理由。必要时解释术语和符号，逐一回答小问，并给出适用的验算过程。\ndocs/CHANGELOG.md:492:  > 每道题增加一至五星难度，各节由易到难排序；面向基础薄弱的学习者写清条件、方法依据、推导与检查，并修正分数排版。\n"}},{"status":"fulfilled","value":{"chunk_id":"c737f2","wall_time_seconds":0.000013458,"exit_code":0,"original_token_count":251,"output":"docs:\ntotal 112\ndrwxr-xr-x   4 oyamahappa  staff    128 Nov 15 22:27 .\ndrwxr-xr-x  16 oyamahappa  staff    512 Nov 13 22:31 ..\n-rw-r--r--   1 oyamahappa  staff  51478 Nov 18 20:22 CHANGELOG.md\n-rw-r--r--   1 oyamahappa  staff   2753 Nov 16 06:35 线性代数前两章真题索引.md\n\nmemory:\ntotal 152\ndrwxr-xr-x   7 oyamahappa  staff    224 Nov  9 23:01 .\ndrwxr-xr-x  16 oyamahappa  staff    512 Nov 13 22:31 ..\n-rw-r--r--   1 oyamahappa  staff   3266 Nov 18 20:22 agents.md\n-rw-r--r--   1 oyamahappa  staff   3111 Nov 16 06:38 gotchas.md\n-rw-r--r--   1 oyamahappa  staff  13345 Nov 18 20:05 plan.md\n-rw-r--r--   1 oyamahappa  staff  18417 Nov 18 20:22 progress.md\n-rw-r--r--   1 oyamahappa  staff  29018 Nov 18 20:22 verify.md\n14c4819 docs: link the Tongji typesetting record to its commit\n047d36a docs: record the combined Tongji linear algebra tests\n032e330 docs: link the Tongji transcription record to its commit\n65beaf2 docs: record Tongji linear algebra test transcription\n2026-11-18 20:26 CST\n"}}]

## tool · 2026-11-18T12:26:58Z


Script completed
Wall time 0.1 seconds
Output:

[{"status":"fulfilled","value":{"chunk_id":"41ffdf","wall_time_seconds":0.000009541,"exit_code":0,"original_token_count":4481,"output":"Warning: truncated output (original token count: 4481)\nTotal output lines: 154\n\n# GPT 试题库\n\n本仓库收录 GPT 生成的试题与解析，以及按主题整理的真题资料。考研数学是其中一个专题。\n\n## 考研数学\n\n按《工科数学分析基础》第三版上册组织的考研数学练习资料，包含 **2009–2026 年数学二分节真题**和 **27302 阶段模拟卷**。下载 PDF 即可使用，也可编辑 LaTeX 源稿。\n\n### 下载资料\n\n| 资料 | 内容 | 下载 |\n| --- | --- | --- |\n| 线性代数前两章三套模拟卷 | 同济第七版「行列式」「矩阵及其运算」。23 道数学一、数学二原题，三卷分别为 9、7、7 题，满分分别为 72、64、62 分。题目页标注出处与难度星号，下方留白，下一页附分步详解。[逐题真题索引](docs/线性代数前两章真题索引.md) | A4 [卷一](output/线性代数前两章模拟卷/A4/线性代数前两章模拟卷1（A4）.pdf) · [卷二](output/线性代数前两章模拟卷/A4/线性代数前两章模拟卷2（A4）.pdf) · [卷三](output/线性代数前两章模拟卷/A4/线性代数前两章模拟卷3（A4）.pdf)<br>iPad [卷一](output/线性代数前两章模拟卷/iPad/线性代数前两章模拟卷1.pdf) · [卷二](output/线性代数前两章模拟卷/iPad/线性代数前两章模拟卷2.pdf) · [卷三](output/线性代数前两章模拟卷/iPad/线性代数前两章模拟卷3.pdf) |\n| 李林高数上册分节题集（iPad） | 按教材四章19节整理419题，各节按一至五星由易到难排列。小灰字星号位于题源左侧，与题号同行。4:3横屏，一题一页、下一页完整解析。4.3暂无对应原题。 | [PDF](output/李林高数上册分节题集/iPad/李林高数上册分节题集.pdf) · [LaTeX 源稿](output/李林高数上册分节题集/李林高数上册分节题集.tex) |\n| 中值定理阶段三套模拟卷（iPad） | 截至第二章 4.2 微分中值定理，每卷 12 题、100 分，建议 120 分钟。4:3 横屏，每卷 25 页，一题一页、下一页详解。 | [第一卷 PDF](output/中值定理阶段模拟卷/iPad/中值定理阶段模拟卷1.pdf) · [第二卷 PDF](output/中值定理阶段模拟卷/iPad/中值定理阶段模拟卷2.pdf) · [第三卷 PDF](output/中值定理阶段模拟卷/iPad/中值定理阶段模拟卷3.pdf) |\n| 数学二分节真题集 | 按教材四章 19 节整理 234 道真题。各节附定理与要点，题目保留年份和原卷题号，每题后另页附解析。 | [横屏 PDF](output/302数学二分节真题集/iPad/302数学二分节真题集.pdf) · [横屏源稿](output/302数学二分节真题集/302数学二分节真题集（原生LaTeX横屏版）.tex) · [A4 编译入口](output/302数学二分节真题集/302数学二分节真题集（原生LaTeX常规版）.tex) |\n| 27302 阶段模拟卷（iPad 横屏版） | 五套模拟卷和 76 道补充练习，共 186 道题。每题单独一页，留有手写区，翻页可看解题思路、推导与答案。 | [横屏 PDF](output/27302阶段模拟卷/iPad/27302阶段模拟卷.pdf) |\n| 27302 阶段模拟卷（A4） | 适合打印和限时练习。每套 22 题，满分 150 分，建议用时 180 分钟。 | [第一卷 PDF](output/27302阶段模拟卷/A4/27302阶段模拟卷.pdf) · [第二至五卷及补充练习 PDF](output/27302阶段模拟卷/A4/27302阶段模拟卷（第二至五卷及补充练习）.pdf) |\n| 数学分析试卷 | 1115 期中卷和电子科技大学 2026 年试卷，均附逐题解析。 | 1115 期中卷 [A4](output/数学分析试卷/A4/数学分析期中1115.pdf) · [iPad](output/数学分析试卷/iPad/数学分析期中1115.pdf)<br>电子科技大学 2026 年试卷 [A4](output/数学分析试卷/A4/电子科技大学2026年数学分析试卷.pdf) · [iPad](output/数学分析试卷/iPad/电子科技大学2026年数学分析试卷.pdf) |\n\n### 练习范围\n\n- **分节刷真题**：真题集覆盖教材上册的函数、极限与连续，一元函数微分学，一元函数积分学和常微分方程。可用 PDF 目录跳到正在复习的小节。\n- **做阶段模拟**：五套模拟卷及补充练习覆盖第一章至第二章第四节「微分中值定理及其应用」。每套包含 10 道单选、6 道填空和 6 道解答题。\n\n### 编辑与编译\n\n`output/` 按题集和试卷系列分目录，成品 PDF 位于各系列的 `A4/` 或 `iPad/`。使用带有 `ctex`、Fandol 字体和 TikZ 的 XeLaTeX 环境，在对应的系列目录编译 `.tex` 文件。\n\n- 李林高数上册分节题集直接编译同名源稿，保留同目录的 `lilin-figures/` 插图。原题的条件疑义和依据原 PDF 修正的公式均在解析注明。\n- 数学二真题集的 A4 编译入口读取同目录的横屏源稿，两种版式共用题目和解析。\n- 中值定理阶段模拟卷各自独立编译。[第一卷源稿](output/中值定理阶段模拟卷/中值定理阶段模拟卷1.tex)、[第二卷源稿](output/中值定理阶段模拟卷/中值定理阶段模拟卷2.tex)、[第三卷源稿](output/中值定理阶段模拟卷/中值定理阶段模拟卷3.tex)均注明本地题源及所选小问，解析写明条件、方法、推导和检查。\n- 27302 模拟卷提供 [第一卷源稿](output/27302阶段模拟卷/27302阶段模拟卷.tex) 和 [第二至五卷及补充练习源稿](output/27302阶段模拟卷/27302阶段模拟卷（第二至五卷及补充练习）.tex)。\n- 线性代数模拟卷带「A4」的入口生成打印版，直接编译题解正文生成 4:3 横屏版。两版共用同目录的 `linear-algebra-exam.sty`。\n\n推送到 `main` 后，GitHub Actions 会编译本次改动影响的 TeX 文档，并将 PDF 上传到 [Releases](https://github.com/OyamaMeek/codex-question-bank/releases)。自动版本从 `v0.0.1` 递增至 `v0.0.999`。如需注明具体改动，在相关 Git 提交正文的末尾留一个空行，再写 `Release-Note: 补充第二至五卷解析`。没有该字段时，发布说明会列出更新的文档名。\n\n## 开发记录\n\n资料的编排和修订历史见 [开发记录](docs/CHANGELOG.md)。\n# AGENTS.md\n\n本文件规定项目中的协作、开发、验证与沟通方式。执行时遵守宿主环境的更高优先级指令，并优先采用用户当前明确提出的要求。具体场景的规则优先于一般默认规则；仍有无法消解的冲突时，说明冲突及其影响。\n\n部分规则可以通过 hooks 执行，其余规则需要主动遵守。完成情况应以实际文件、测试结果、Git 状态、运行结果和验证记录为依据。只有已经配置并成功运行的检查，才能作为验证证据。\n\n## 1. 职责与判断\n\n- 在用户确定的目标与授权范围内完成工作。涉及架构、核心业务逻辑或产品方向的重要选择，不得擅自决定；用户已经授权的选择直接执行。\n- 默认优先级依次为正确性、可维护性、最小改动范围、执行速度。\n- 先检查问题是否存在错误前提、逻辑跳跃或信息缺失，独立判断，区分事实、推测和主观观点。\n- 涉及数字、人物和结论时尽量核实来源。不同意用户判断时，直接说明依据、实际风险和替代解释，并提醒与任务有关的遗漏变量、成本和偏差。\n- 完整理解并满足当前需求，不擅自增加功能，不删减用户明确要求的设计，不为假设中的未来需求增加配置或抽象。\n\n## 2. 语言与输出\n\n- 默认使用清楚、自然的中文，代码标识符和必要的技术术语保留原名。\n- 直接表达具体内容，不使用“不是……而是……”“要……而不是……”等无必要的对比句式，不追加用户没有要求比较的对象。\n- 不添加空泛的总起或总结，例如“下面详细拆开”“一句话总结”。\n- 使用完整词语和明确的动宾结构。使用“崩溃、终止、判定、推断、抛出、挂起”等完整表达，不使用单个字的缩写，不生造名词或缩略说法。\n- 不使用“落地”“钉死”“对齐”等含义模糊的行业黑话。描述采用的技术、模型和工具时，直接写出具体事物，避免以“栈”字概括。\n- 不评价工作量，不使用“That's a lot”“This is a substantial rewrite”等表达。\n- 搜索结果只列出符合要求的内容，不罗列已经确认不符合要求的候选项。\n- 回复、注释和交付文档描述当前有效的最终状…281 tokens truncated…`*` 至 `*****`）表示难度，星号越多，难度越高。\n- 解析以基础薄弱、第一次接触该题型的读者也能独立读懂为标准。先说清已知条件和求解目标，再指出题目中哪些线索让人想到从哪里入手、为什么选用这个方法。逐步展开计算或推导，列出关键的中间算式，讲清每个关键步骤是怎么想到的、依据是什么、所用公式或定理的条件为何满足。涉及参数分类时，说明分类依据并展开各分支。涉及排除选项时，说明排除理由。必要时解释术语和符号，逐一回答小问，并给出适用的验算过程。\n\n## 3. 用户意图与执行控制\n\n- 用户要求先规划、思考、审查、评估或解释时，先完成对应工作，取得执行授权后再修改文件。\n- 未经明确要求，不切换到专门的 plan mode。复杂任务所需的书面计划可以在当前模式中完成。\n- 用户提供书面计划时，按计划执行；计划通常位于 `claude.md`，以用户指定的位置和实际文件为准。遇到实质性阻碍时，说明阻碍，暂停依赖该决定的步骤。\n- 用户批准计划或明确说“执行”“可以”“推送”后，直接完成已获授权的操作，不重复征求同一项授权。\n- 用户以疑问句提出问题时，回答问题，不擅自修改文件，不附加未要求的替代方案、反问或催促执行的话语。\n- 对确实影响实现且尚未授权的需求歧义，明确指出需要用户决定的事项；已经可以独立完成的工作继续执行。\n- 执行过程中收到其他问题，能够立即回答的先回答，然后继续原任务；用户明确取消或改变目标时，按新要求执行。\n- 用户表示“退一步”“一直在绕圈”等意思时，停止当前方法，重新读取相关上下文并提出不同路径。\n- 用户询问是否确定时，先通过工具核实，再回答。\n- 风险较高且没有明确恢复点的操作，先提出建立检查点。\n\n# 工具\n\n同济线代同步测试卷由 FFmpeg 解码 HEIC，使用本机 RapidOCR（ONNX Runtime）提取文字，对照原图逐题校订，用 KaTeX 检查公式语法。\n\n同济线代合卷将两份已校对 Markdown 的题面与逐题解析合成单个源稿，采用 Tectonic 0.17.0 和 ctex 编译，用 NumPy 复验关键结果，用 PyMuPDF 核对页序、尺寸、题头位置及留白。\n\n线性代数前两章模拟卷用 PyMuPDF 读取逐年原卷的文字与公式字形坐标，结合真题 Markdown、配套解析校核。扫描公式用本地 PaddleOCR-VL 提取候选并结合对应解析复核。使用 Tectonic 0.17.0、ctex 和双版式入口编译，用 Python 和 mpmath 复算并检查 PDF 页序与留白。\n\n数学分析期中1115 使用 PyMuPDF 提取文字层和嵌入图片，使用本机 RapidOCR 识别题面，对照原卷逐题核对，并用既有 KaTeX 脚本检查公式。\n\n数学分析期中1115 的 LaTeX 版复用 Tectonic 0.17.0、ctex 和双入口试卷模板。用 PyMuPDF 检查分页和字形坐标，用 mpmath 独立复算关键结果。\n\n电子科技大学 2026 年数学分析试卷使用 CPU 版 RapidOCR 识别截图分区，对照放大的原图校勘公式。使用 Tectonic、ctex 编译两版，使用 PyMuPDF 核对分页与文字位置，使用 mpmath 独立复算关键结果。\n\n李林高数上册分节题集按微分、积分、微分方程分区编写、评级和复核，主代理处理函数与极限并统一排序编译。复用 Tectonic、ctex、markdown-it-py、PyMuPDF 和既有 KaTeX；用户授权后核对原题图片及最终 PDF 渲染页，记录于 `.agent/visual/`。\n\n线性代数第七版使用现有 PyMuPDF、macOS Vision、MLX PaddleOCR和ONNX Runtime；补充官方PP-DocLayoutV3版面模型，按正文和公式分别识别。采用dispatching-parallel-agents技能按章节对照原页校订，主代理统一组装与检查，避免各代理同时修改最终文件。\n\n中值定理阶段三套模拟卷由单一代理选编和解析。复用 ctex、amsmath、应用内 Tectonic 与项目缓存；采用源稿检查、数学复算和 PDF 文字几何验证。使用 PDF 与 Ponytail 技能；不调用子代理、截图或图像检查。\n\n本次分节真题详细解析按章节使用并行代理技能分区校订，主代理统一评级规则、题头、检查和编译。使用已有 Tectonic、PyMuPDF 与 Python 标准库；不进行截图或图像检查。\n\n使用 PyMuPDF 提取 PDF 文字层，使用 macOS Vision 在本机识别扫描页。源 PDF 保留在原目录。\n\n本次张宇往年八套由单一代理逐题检查，使用 PyMuPDF 原页图和文字层、嵌入图示哈希及现有 KaTeX 脚本验证，未调用其他代理。\n\n数学模拟卷补用本机 MLX PaddleOCR 生成候选，再逐题对照源 PDF 修正；候选不能作为完成证据。使用 KaTeX 验证 Markdown 公式渲染。往年合集按独立文件分工校对，选填交付文件统一由一名代理组装。\n\n阶段模拟卷使用 LaTeX 和 ctex 排版，使用桌面应用附带的 Tectonic 编译，使用 PyMuPDF 检查 PDF 题序和文本边界。\n\n自动发布使用 GitHub Actions、Tectonic 0.17.0、Python 标准库和 GitHub CLI，PDF 作为 GitHub Release 附件分发。\n# 注意事项\n\n线性代数前两章阶段，筛掉以矩阵初等变换、消元讨论、相似对角化为主要捷径的题。行列式的行列运算属于第一章，保留相应题目。\n\n线性代数前两章模拟卷的出处显示在题目页，文字星号紧接出处右侧。评级依据题目本身的计算与推理负担。\n\n按指定范围选编多套模拟卷时，先复核题库里符合范围且互不重复的完整原题数量，再决定卷数。用户要求题量充足时，以仓库已有阶段卷的规模作为参考。\n\n李林题集的难度星号与题号同行，使用小号灰字，紧靠右侧题源左边。\n\n面向基础薄弱学习者的解析须逐题交代已知与目标、方法条件、关键推导原因和结果检查，不能只列公式及答案。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\n\nPDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。\n\n数学教材的整页或半页OCR可能漏掉独立公式、合并矩阵或丢失不等号。需按版面区分正文与公式，再对照原页核对；页数、链接和公式渲染通过都不能代替内容校对。源文件跳页时按印刷页码记录缺失范围，不补造题目。\n\n用户要求题面以原生 LaTeX 转录时，题干、选项、公式和必要图形需要可编辑。PDF 裁片仅用于内部核对。\n\n真题集的行内极限也将趋近条件排在 `lim` 正下方。题头显示原卷年份和题号，原卷页码只留作 LaTeX 源稿中的定位信息。\n\n涉及人名的数学术语沿用《工科数学分析基础》第三版上册的英文拼写，例如 Taylor、Cauchy、Lagrange、L'Hospital。目录、知识点、题干和解析采用同一写法。\n\n修改已有交付文件时直接覆盖，每个任务只保留当前交付，历史版本由 Git 保留。\n\n题面转换遇到题解合订本时，核对源文件中试题和解析的分页分界。处理混合合集时按书签或目录筛选卷次。\n\n用户要求只保留标题和题目时，题面 Markdown 直接写标题、题干、选项和小问。页码、链接、提取方式和水印无需进入正文，OCR 文字以普通段落呈现。\n\n用户排除一个数学科目时，同时检查混合分类本和合卷。分类本优先用源文件中每题的来源标注，保留题号和其他科目的共用题面。\n\n同名、同卷次在不同科目、年份和排版中可能有公式或选项差异，复用校对文本前逐题比较实际来源。极小分子、幂指数及根号次数需要直接检查原页，内部去留白不得删除任何有墨迹的行。\n\n判断仓库状态时同时检查已知的检出目录和远端配置，不能仅凭工作目录的一次 `git status` 报错断言没有仓库。当前仓库已迁至项目根目录，Git 操作在根目录执行。\n\n`references/` 仅保存在本地，整个目录不纳入 Git。不得强制添加其中的 PDF、Markdown 或其他资料；取消跟踪时保留本地文件。\n"}},{"status":"fulfilled","value":{"chunk_id":"e69591","wall_time_seconds":0.000010458,"exit_code":0,"original_token_count":3098,"output":"# PDF 批量提取\n\n## 同济线代同步测试卷\n\n按两组 HEIC 的文件顺序识别版面。用本机 RapidOCR 生成文字候选，逐题对照源图转写题干、选项、小问和公式，按章节和原卷归组写入本地 Markdown，并附源图定位。核查覆盖范围和 LaTeX 语法。\n\n将两章四卷的 68 道已核对题面合入一份可独立编译的 TeX，保留原卷题号、分值、选项和小问，标注卷别、照片号及难度。逐题补全入手思路、计算过程和验算。默认编译成 iPad 4:3 横屏，通过版式开关编译 A4。源稿和两版 PDF 随本地题源保存。\n\n## 整理 output 目录\n\n按六个题集或试卷系列归类。每个系列保留相互依赖的 LaTeX 源稿、样式与资源，成品按 `A4/`、`iPad/` 放置。仅合并逐字节相同的 PDF，本地编译副产物移入已忽略的工作目录。工作区已有的五处缺失继续保留，提交只迁移这些文件已跟踪的版本。同步 README、测试路径与发布依赖，纯迁移不产生新 Release。\n\n## 线性代数前两章模拟卷\n\n复筛适合尚未学习矩阵变换的读者。删去主要考查初等行列变换、消元讨论解的个数，或以相似对角化、分块相似显著简化的题。保留只用前两章行列式性质、矩阵运算和克拉默法则便可直接解答的题。在各卷内按原顺序重编号，保留单题分值并重算卷面总分，更新索引及同路径 PDF。\n\n在三卷 TeX 源稿及共用排版文件中将出处移到题目页标题同行，使用一至五个文字星号标记难度，紧邻出处右侧。按入手线索、计算量和推理层数逐题评级。补全关键算式和分情况理由，长解析续页。编译到独立验证目录，检查原题、出处、星号位置、题解页序和留白，再覆盖三卷 A4 与 iPad PDF。\n\n遍查本地 `references/302真题` 中 2009–2026 年数学一、二的 36 份逐年真题及配套解析中的旧题引录。筛选全题可仅用同济第七版印刷页第 1–55 页所学和直接代入完成的原题，保留原题条件、选项及双科共用题号，按年份建立真题索引。题量达到每卷约 12 题时，按单选、填空、解答分为三卷。每卷以同一正文编译 A4、iPad 两版，各题独占一页且后面紧接分步解析。\n\n## 数学分析期中1115\n\n\n在 `references/302模拟27` 中筛选李林、张宇、合工大、超越、武忠祥、李艳芳的题面，在 `references/302模拟27md` 中按原层级生成 UTF-8 Markdown。合集按书签或目录选择卷次，题目与解析合订的文件按实际分界提取试题页。提取可读文字层，对扫描页和内嵌图片使用本机 Vision OCR。Markdown 只呈现标题、题干、选项、小问和图中题目文字，保留题号与卷次、题型标题。\n\n逐题校对以源 PDF 的题号和版面为准。先用李林六套卷第一卷建立逐题对照样本，核对数学符号、矩阵、选项和小问。再对照同卷版本及合集中的同题，确认内容一致后复用校对结果。图文识别候选与原卷有差异时记录具体卷次和题号。\n\n交付仅保留数一、数二。移除独立的数三 Markdown。混合卷按源 PDF 的题源标注或题内科目标记筛选，保留共享题的数一、数二题面和原题号。\n\n张宇往年八套选填按两科各八卷、每卷 16 题对照原 PDF 第 71–94 页校对，核对紧凑与留白来源的差异，原位更新四份交付文件中的对应分组。检查每卷题号、40 个选项及 KaTeX 渲染，其他作者分组保持原文。\n\n## LaTeX PDF 自动发布\n\n在 `main` 的 push 工作流中按推送前后提交计算变更，重建新增或修改的 `output/` TeX 入口及受资源变更影响的入口。用 Tectonic 0.17.0 编译，全部成功后上传到草稿，附件齐全后发布。发布串行执行，按已有 Release 和标签分配 `v0.0.1` 至 `v0.0.999`，用运行 ID 识别重跑。说明优先读取提交里的 `Release-Note:` 中文摘要，否则使用受影响的文档名。\n# 进度\n\n## 同济线代同步测试卷\n\n- [x] 找到行列式、矩阵两组共 16 张源图。\n- [x] 已转录四卷 68 题，并逐题对照原图校订。\n- [x] 验证 68 道题、80 个选项、4 个编号小问、16 条原图链接及 264 个 LaTeX 表达式。\n- [x] 生成四卷合并的单文件 TeX，完成 68 道解析。\n- [x] 核对题面、复算关键答案并验证双版分页和演算留白。交付位于本地 `references/同济线代/同步测试卷/`，PDF 分别位于 `A4/` 和 `iPad/`。\n\n## 整理 output 目录\n\n- [x] 盘点现存文件、Git 状态和路径引用，确认两组 PDF 的 SHA-256 相同。\n- [x] 搬迁六个系列及编译副产物，更新文档、测试和发布依赖。\n- [x] 核对内容、版式、链接和实际编译，23 项项目测试通过。\n- [x] 提交 `d5bb77c` 已推送至 `origin/main`。本地发布计划为空，GitHub Actions 运行 `43773515662` 成功并跳过编译和上传。\n\n## 线性代数前两章模拟卷\n\n- [x] 按尚未学习矩阵变换的要求复筛三卷题目。\n- [x] 删去 12 道题，更新 23 道保留题的编号、索引和卷面总分。重编并覆盖六份正式 PDF 及卷一本地预览。\n\n- 根目录迁入前已有的其他资料及 `output/302-question-facsimiles.pdf` 缺失不纳入本次提交。\n\n## LaTeX PDF 自动发布\n\n- [x] 先运行回归测试确认发布模块缺失，实施后通过八项变更选择、中文说明和版本测试。\n- [x] 实现推送工作流、编译和草稿发布流程，编译五份现有源稿。核对发布队列配置和工作流其他语法。\n- [x] 推送 `829d693`，核对 GitHub Actions 首次运行成功且未占用首个版本号。首次包含 TeX 变更的推送将触发实际发布。\n\n## references 仅保存在本地\n\n- [x] 将整个 `/references/` 加入忽略规则。\n- [x] 取消四份 Markdown 的 Git 跟踪，本地 SHA-256 全部不变；`2f3cdb1` 已推送，远端 main 与本地一致，提交树不含 references。\n# 完成标准\n\n## 同济线代同步测试卷\n\n核对两组全部源图，按原卷核查题型、题号、选项、小问、矩阵和行列式，标明源图和可见的原卷疑义。用 KaTeX 检查交付 Markdown 中的公式。\n\n16 张源图均取得 RapidOCR 结果并逐题对照。四卷各有 17 题，均为 5 道选择题、5 道填空题和 7 道解答题，合计每卷 100 分。题序、80 个选项、4 个编号小问和 16 条原图链接通过检查，264 个 LaTeX 表达式通过 KaTeX 渲染。行列式 B 卷第 13 题第三行第三列保留原印刷指数并加注。\n\n合卷 TeX 验收覆盖四卷各 17 题、原题序、全部选项及公式、题号同一行的出处和难度、解析与题面相邻、题页演算区。复算各卷关键结果，并编译核对 A4 与 800×600 bp PDF 的分页和日志。\n\n68 份 TeX 题面与已校对 Markdown 逐题比对通过，20 道单选的答案字母核对通过。124 项数值复验和 23 项仓库测试通过。两版均为 137 页、73 个书签，所有题目均独占一页，下一页为对应解析。A4 和 iPad 最小演算留白分别为 408.4 和 199.7 bp。编译无缺字、警告和溢出。版式检查使用 PDF 文本与坐标。\n\n## 整理 output 目录\n\n核对现有题稿、资料和正式 PDF 的 Git 内容，确认目录与版式相符、无重复 PDF、编译资源的相对路径可用。运行全部项目测试，检查新路径上的编译入口、README 链接以及纯迁移的空发布计划。保留原工作区缺失及本地编译产物。\n\n提交含 47 个内容逐字节相同的文件迁移和 1 个重复 PDF 的删除。验证检出中的 26 条 README 链接均存在，18 份成品 PDF 版式与目录一致且哈希互不相同。Tectonic 0.17.0 成功编译 19 个入口，裁片版仍有既存的 PDF 版本和重复页锚点警告。23 项项目测试通过，覆盖仅移动源稿的发布计划。提交 `d5bb77c` 的发布计划为空，GitHub Actions 运行 `43773515662` 成功，依发布条件跳过编译和上传。\n\n## 线性代数前两章模拟卷\n\n复筛后核对删题清单、保留题面和解析、连续题号、各卷分值、索引逐行映射，以及双版式页序与编译日志。\n\n\n往年 10 套、20 套数一的四份输出通过 6,552 个 KaTeX 表达式检查；对应数二四份通过 5,804 个表达式检查。10 套每份 220 题，20 套每份 242 题。20 套数一 A3 李林四套第三卷第 22 题原印两次 Y=1，A4 第一项为 Y=-1，分别保留。40 套两份输出各 483 题、22 卷，通过合计 5,840 个表达式检查。李林六套第一卷原文件缺第 22 题，不补造题目。\n\n内部原页核对图片必须保留所有有墨迹的行。旧版按每行四个黑像素筛选会误删小分子；已修复为保留任一黑像素的行，并直接用原页复核相关分式。数二 10 套和 20 套的旧裁片共 101 处丢墨片段已复查，修复李林四套第二卷第 11 题幂指数分子 1。\n\n往年选填超越数一第六至第十卷对照原 PDF 第 56–70 页校对，修复概率表、求和下标、积分上下限和伴随矩阵星号。写回两版，检查每卷 16 题及 40 个选项；547 个表达式通过 KaTeX 渲染。\n\n## LaTeX PDF 自动发布\n\n八项回归测试通过，覆盖 Git 推送范围、共用源稿、裁片资源、仅文档变更、中文摘要、版本递增、上限和重跑时的草稿选择。Tectonic 0.17.0 在本机成功编译五份 PDF，页数为 4、22、471、63、488。裁片版仍提示输入 PDF 版本较高和重复页锚点。Linux 安装包通过 SHA-256 校验。`actionlint` 1.7.12 过滤已知的 `concurrency.queue` 兼容性误报后通过，`queue: max` 另按 GitHub 文档和工作流 Schema 核对。\n\nGitHub Actions 运行 `42850865346` 通过，检出了 `829d693` 并完成推送差异检查。无 TeX 变更时编译和发布步骤均跳过，Releases 仍为空。远端附件上传和公开发布尚待首个包含 TeX 变更的推送验证。\n## [2026-11-13 21:55] 清理高数做题本的原页链接\n\n- **需求**：去掉题目下方的原 PDF 页码链接。\n- **实际结果**：从本地 Markdown 移除 746 条原页链接及开头的链接说明。\n- **验证**：其余内容逐字节一致，保留 746 条题面与示例和 24 个图示，2,676 个公式通过 KaTeX 渲染。\n- **涉及文件**：`references/27李林880/md/【做题本】平板版27考研李林辅导讲义（高数）.md`。\n- **Git 提交**：`f8a6163 docs: record removal of calculus PDF page links`。\n\n---\n\n## [2026-11-13 21:53] 逐题复核 27 李林高数做题本\n\n- **需求**：逐题核对已有 Markdown 与平板版原 PDF。\n- **实际结果**：对全部 746 个题面页执行第二次数学 OCR，结合原图复核差异和高风险公式。原位修正 43 页的题面或公式，核实首轮标出的四页，保留原图供查阅。\n- **验证**：14 章、746 条题面与示例、选择题选项及 24 个图像链接通过检查，2,676 个数学表达式通过 KaTeX 语法检查。两次 OCR 一致的部分未逐式人工核对。\n- **涉及文件**：`references/27李林880/md/`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`。\n- **Git 提交**：`eb27bcc docs: record Li Lin calculus OCR proofreading`。\n\n---\n\n## [2026-11-13 21:33] 逐题转录 27 李林高数做题本\n\n\n---\n\n## [2026-11-18 20:21] 合并同济线代同步测试卷的 TeX\n\n- **需求**：按项目排版要求，将已核对的同济线代同步测试题合进一份 TeX。\n- **实际结果**：四卷 68 道题沿用原卷题序与分值，补齐分步解析。题号同行标注原卷、照片编号及难度，题页留出手写演算区。单一 TeX 支持 A4、iPad 4:3 两种版式。\n- **验证**：逐题比对 Markdown 与 TeX，核对 80 个选项，复验 124 个数值结果。两版各 137 页、73 个书签，题目和解析页逐对相邻，最小演算留白为 408.4 和 199.7 bp。编译日志无缺字、警告或溢出。23 项仓库测试通过。\n- **涉及文件**：`references/同济线代/同步测试卷/`、`memory/`、`docs/CHANGELOG.md`。\n- **Git 提交**：`047d36a9948c3283414398fd8a85b07dfb555c06 docs: record the combined Tongji linear algebra tests`。TeX 与 PDF 按本地题源规则保存。\n\n---\norigin/main\n"}},{"status":"fulfilled","value":{"chunk_id":"d8e0a5","wall_time_seconds":0.000026291,"exit_code":0,"original_token_count":956,"output":"README.md:3:本仓库收录 GPT 生成的试题与解析，以及按主题整理的真题资料。考研数学是其中一个专题。\nREADME.md:14:| 李林高数上册分节题集（iPad） | 按教材四章19节整理419题，各节按一至五星由易到难排列。小灰字星号位于题源左侧，与题号同行。4:3横屏，一题一页、下一页完整解析。4.3暂无对应原题。 | [PDF](output/李林高数上册分节题集/iPad/李林高数上册分节题集.pdf) · [LaTeX 源稿](output/李林高数上册分节题集/李林高数上册分节题集.tex) |\nREADME.md:16:| 数学二分节真题集 | 按教材四章 19 节整理 234 道真题。各节附定理与要点，题目保留年份和原卷题号，每题后另页附解析。 | [横屏 PDF](output/302数学二分节真题集/iPad/302数学二分节真题集.pdf) · [横屏源稿](output/302数学二分节真题集/302数学二分节真题集（原生LaTeX横屏版）.tex) · [A4 编译入口](output/302数学二分节真题集/302数学二分节真题集（原生LaTeX常规版）.tex) |\nREADME.md:19:| 数学分析试卷 | 1115 期中卷和电子科技大学 2026 年试卷，均附逐题解析。 | 1115 期中卷 [A4](output/数学分析试卷/A4/数学分析期中1115.pdf) · [iPad](output/数学分析试卷/iPad/数学分析期中1115.pdf)<br>电子科技大学 2026 年试卷 [A4](output/数学分析试卷/A4/电子科技大学2026年数学分析试卷.pdf) · [iPad](output/数学分析试卷/iPad/电子科技大学2026年数学分析试卷.pdf) |\nREADME.md:30:- 李林高数上册分节题集直接编译同名源稿，保留同目录的 `lilin-figures/` 插图。原题的条件疑义和依据原 PDF 修正的公式均在解析注明。\nREADME.md:31:- 数学二真题集的 A4 编译入口读取同目录的横屏源稿，两种版式共用题目和解析。\nREADME.md:32:- 中值定理阶段模拟卷各自独立编译。[第一卷源稿](output/中值定理阶段模拟卷/中值定理阶段模拟卷1.tex)、[第二卷源稿](output/中值定理阶段模拟卷/中值定理阶段模拟卷2.tex)、[第三卷源稿](output/中值定理阶段模拟卷/中值定理阶段模拟卷3.tex)均注明本地题源及所选小问，解析写明条件、方法、推导和检查。\nREADME.md:36:推送到 `main` 后，GitHub Actions 会编译本次改动影响的 TeX 文档，并将 PDF 上传到 [Releases](https://github.com/OyamaMeek/codex-question-bank/releases)。自动版本从 `v0.0.1` 递增至 `v0.0.999`。如需注明具体改动，在相关 Git 提交正文的末尾留一个空行，再写 `Release-Note: 补充第二至五卷解析`。没有该字段时，发布说明会列出更新的文档名。\n.github/scripts/test_release_tex.py:45:        self.write(self.wide, \"new solutions\")\n.github/scripts/test_release_tex.py:46:        after = self.commit(\"Release-Note: 补充真题解析\")\n.github/scripts/test_release_tex.py:49:        self.assertEqual(plan[\"notes\"], \"- 修正第一卷的积分公式\\n- 补充真题解析\")\n.github/scripts/test_question_bank.py:37:    def test_complete_solutions_match_questions(self):\n.github/scripts/test_question_bank.py:48:            solution = block.split(r\"\\begin{QuestionSolution}\", 1)[1].split(r\"\\end{QuestionSolution}\", 1)[0]\n.github/scripts/test_question_bank.py:50:                self.assertIn(r\"\\textbf{\" + label + \"}\", solution, identity)\n.github/scripts/test_lilin_workbook.py:13:    def test_difficulty_sorting_and_expanded_solutions(self):\n.github/scripts/test_lilin_workbook.py:22:            solution = block.split(r\"\\Solution\", 1)[1]\n.github/scripts/test_lilin_workbook.py:24:                labels = re.findall(r\"^\\\\(Known|Method|Derive|Check)$\", solution, re.M)\n.github/scripts/test_lilin_workbook.py:40:    def test_scope_and_separate_solutions(self):\n"}}]

## tool · 2026-11-18T12:27:05Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"a3c125","wall_time_seconds":0.000009834,"exit_code":0,"original_token_count":1017,"output":"AGENTS.md\ndocs/CHANGELOG.md\nmemory/agents.md\nmemory/gotchas.md\nmemory/plan.md\nmemory/progress.md\nmemory/verify.md\n\n### 数学题集与模拟卷排版\n\n- 题干、选项和解析中的数学公式统一使用 LaTeX。分数用 `\\frac{分子}{分母}` 排成上下分式，分子在分数线上方，分母在下方。极限用 `\\lim\\limits_{x\\to a}` 等写法，行内公式也将趋近条件置于 `\\lim` 正下方。\n- 每套题集或模拟卷各保留一份 A4 版 PDF 和一份 iPad 4:3 横屏版 PDF。两版均为每道题单独占一页，题目排在上方，下方留出手写演算空间。对应解析从紧接的下一页开始，题目和解析分开排版。解析较长时可续页，结束后再另起一页排下一道题。\n- 每道题的出处标在题目页，与题号同行。出处右侧紧接一至五个文字星号（`*` 至 `*****`）表示难度，星号越多，难度越高。\n- 解析以基础薄弱、第一次接触该题型的读者也能独立读懂为标准。先说清已知条件和求解目标，再指出题目中哪些线索让人想到从哪里入手、为什么选用这个方法。逐步展开计算或推导，列出关键的中间算式，讲清每个关键步骤是怎么想到的、依据是什么、所用公式或定理的条件为何满足。涉及参数分类时，说明分类依据并展开各分支。涉及排除选项时，说明排除理由。必要时解释术语和符号，逐一回答小问，并给出适用的验算过程。\n\n## 3. 用户意图与执行控制\n\n- 用户要求先规划、思考、审查、评估或解释时，先完成对应工作，取得执行授权后再修改文件。\n# 注意事项\n\n线性代数前两章阶段，筛掉以矩阵初等变换、消元讨论、相似对角化为主要捷径的题。行列式的行列运算属于第一章，保留相应题目。\n\n线性代数前两章模拟卷的出处显示在题目页，文字星号紧接出处右侧。评级依据题目本身的计算与推理负担。\n\n按指定范围选编多套模拟卷时，先复核题库里符合范围且互不重复的完整原题数量，再决定卷数。用户要求题量充足时，以仓库已有阶段卷的规模作为参考。\n\n李林题集的难度星号与题号同行，使用小号灰字，紧靠右侧题源左边。\n\n面向基础薄弱学习者的解析须逐题交代已知与目标、方法条件、关键推导原因和结果检查，不能只列公式及答案。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\n\nPDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。\n.github/scripts/test_release_tex.py:3:import unittest\n.github/scripts/test_release_tex.py:9:class PushPlanTests(unittest.TestCase):\n.github/scripts/test_release_tex.py:13:        temporary = tempfile.TemporaryDirectory(dir=work)\n.github/scripts/test_release_tex.py:77:class ReleaseVersionTests(unittest.TestCase):\n.github/scripts/test_release_tex.py:107:    unittest.main()\n.github/scripts/test_question_bank.py:4:import unittest\n.github/scripts/test_question_bank.py:16:class QuestionBankTests(unittest.TestCase):\n.github/scripts/test_question_bank.py:67:    unittest.main()\n.github/scripts/test_mean_value_exams.py:4:import unittest\n.github/scripts/test_mean_value_exams.py:11:class MeanValueExamTests(unittest.TestCase):\n.github/scripts/test_mean_value_exams.py:78:    unittest.main()\n.github/scripts/test_lilin_workbook.py:5:import unittest\n.github/scripts/test_lilin_workbook.py:12:class LilinWorkbookTests(unittest.TestCase):\n.github/scripts/test_lilin_workbook.py:76:    unittest.main()\n D output/27302阶段模拟卷/27302阶段模拟卷.tex\n D output/27302阶段模拟卷/27302阶段模拟卷（第二至五卷及补充练习）.tex\n D output/27302阶段模拟卷/A4/27302阶段模拟卷.pdf\n D output/27302阶段模拟卷/A4/27302阶段模拟卷（第二至五卷及补充练习）.pdf\n D output/302数学二分节真题集/302-question-facsimiles.pdf\n"}

## tool · 2026-11-18T12:27:13Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:27:16Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"1a5809","wall_time_seconds":0.0000115,"exit_code":0,"original_token_count":1004,"output":" memory/plan.md                                     |   4 +\n memory/progress.md                                 |   5 +\n memory/verify.md                                   |   4 +\n ...56\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\" | 205 ------\n ...05\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\" | 736 ---------------------\n ...56\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\" | Bin 106056 -> 0 bytes\n ...05\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\" | Bin 204784 -> 0 bytes\n .../302-question-facsimiles.pdf\"                   | Bin 23932688 -> 0 bytes\n 8 files changed, 13 insertions(+), 941 deletions(-)\n### 数学题集与模拟卷排版\n\n- 题干、选项和解析中的数学公式统一使用 LaTeX。分数用 `\\frac{分子}{分母}` 排成上下分式，分子在分数线上方，分母在下方。极限用 `\\lim\\limits_{x\\to a}` 等写法，行内公式也将趋近条件置于 `\\lim` 正下方。\n- 每套题集或模拟卷各保留一份 A4 版 PDF 和一份 iPad 4:3 横屏版 PDF。两版均为每道题单独占一页，题目排在上方，下方留出手写演算空间。对应解析从紧接的下一页开始，题目和解析分开排版。解析较长时可续页，结束后再另起一页排下一道题。\n- 每道题的出处标在题目页，与题号同行。出处右侧紧接一至五个文字星号（`*` 至 `*****`）表示难度，星号越多，难度越高。\n- 解析以基础薄弱、第一次接触该题型的读者也能独立读懂为标准。先说清已知条件和求解目标，再指出题目中哪些线索让人想到从哪里入手、为什么选用这个方法。逐步展开计算或推导，列出关键的中间算式，讲清每个关键步骤是怎么想到的、依据是什么、所用公式或定理的条件为何满足。涉及参数分类时，说明分类依据并展开各分支。涉及排除选项时，说明排除理由。必要时解释术语和符号，逐一回答小问，并给出适用的验算过程。\n\n## 3. 用户意图与执行控制\n\n## [2026-11-18 20:21] 合并同济线代同步测试卷的 TeX\n\n- **需求**：按项目排版要求，将已核对的同济线代同步测试题合进一份 TeX。\n- **实际结果**：四卷 68 道题沿用原卷题序与分值，补齐分步解析。题号同行标注原卷、照片编号及难度，题页留出手写演算区。单一 TeX 支持 A4、iPad 4:3 两种版式。\n- **验证**：逐题比对 Markdown 与 TeX，核对 80 个选项，复验 124 个数值结果。两版各 137 页、73 个书签，题目和解析页逐对相邻，最小演算留白为 408.4 和 199.7 bp。编译日志无缺字、警告或溢出。23 项仓库测试通过。\n- **涉及文件**：`references/同济线代/同步测试卷/`、`memory/`、`docs/CHANGELOG.md`。\n- **Git 提交**：`047d36a9948c3283414398fd8a85b07dfb555c06 docs: record the combined Tongji linear algebra tests`。TeX 与 PDF 按本地题源规则保存。\n\n---\n# 注意事项\n\n线性代数前两章阶段，筛掉以矩阵初等变换、消元讨论、相似对角化为主要捷径的题。行列式的行列运算属于第一章，保留相应题目。\n\n线性代数前两章模拟卷的出处显示在题目页，文字星号紧接出处右侧。评级依据题目本身的计算与推理负担。\n\n按指定范围选编多套模拟卷时，先复核题库里符合范围且互不重复的完整原题数量，再决定卷数。用户要求题量充足时，以仓库已有阶段卷的规模作为参考。\n\n李林题集的难度星号与题号同行，使用小号灰字，紧靠右侧题源左边。\n\n面向基础薄弱学习者的解析须逐题交代已知与目标、方法条件、关键推导原因和结果检查，不能只列公式及答案。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\n\nPDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。\n2026-11-18 20:27\n"}

## tool · 2026-11-18T12:27:35Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:27:39Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"34081d","wall_time_seconds":0.000010417,"exit_code":0,"original_token_count":1549,"output":"diff --git a/AGENTS.md b/AGENTS.md\nindex 6ac9417..e7109a4 100644\n--- a/AGENTS.md\n+++ b/AGENTS.md\n@@ -31,7 +31,10 @@\n - 题干、选项和解析中的数学公式统一使用 LaTeX。分数用 `\\frac{分子}{分母}` 排成上下分式，分子在分数线上方，分母在下方。极限用 `\\lim\\limits_{x\\to a}` 等写法，行内公式也将趋近条件置于 `\\lim` 正下方。\n - 每套题集或模拟卷各保留一份 A4 版 PDF 和一份 iPad 4:3 横屏版 PDF。两版均为每道题单独占一页，题目排在上方，下方留出手写演算空间。对应解析从紧接的下一页开始，题目和解析分开排版。解析较长时可续页，结束后再另起一页排下一道题。\n - 每道题的出处标在题目页，与题号同行。出处右侧紧接一至五个文字星号（`*` 至 `*****`）表示难度，星号越多，难度越高。\n-- 解析以基础薄弱、第一次接触该题型的读者也能独立读懂为标准。先说清已知条件和求解目标，再指出题目中哪些线索让人想到从哪里入手、为什么选用这个方法。逐步展开计算或推导，列出关键的中间算式，讲清每个关键步骤是怎么想到的、依据是什么、所用公式或定理的条件为何满足。涉及参数分类时，说明分类依据并展开各分支。涉及排除选项时，说明排除理由。必要时解释术语和符号，逐一回答小问，并给出适用的验算过程。\n+- 新写或修订数学题解时，默认采用引导式解析，让第一次接触该题型、基础薄弱的读者也能先尝试，再独立读懂完整解法。\n+  1. **先提问。** 简要说明已知条件与目标，从题目中的具体线索提出一个读者可以动手尝试的问题。把问题放在方法名、关键变形和答案之前，另起段落写提示，让读者可以先停下来想。\n+  2. **再给提示。** 从提醒读者观察某个条件或式子的结构开始，必要时再提示可尝试的变形、公式或定理。说明这些线索为什么指向所选方法。后续遇到需要判断的关键步骤，也先用一个具体问题引导。\n+  3. **最后完整推导。** 写出关键中间算式，解释推理依据以及公式或定理的适用条件。需要分类时说明分类依据并逐项讨论，需要排除选项时交代排除理由。必要时解释术语和符号，逐一回答小问，给出答案和适用的验算过程。\n \n ## 3. 用户意图与执行控制\n \ndiff --git a/memory/gotchas.md b/memory/gotchas.md\nindex bd95292..13edddd 100644\n--- a/memory/gotchas.md\n+++ b/memory/gotchas.md\n@@ -8,7 +8,7 @@\n \n 李林题集的难度星号与题号同行，使用小号灰字，紧靠右侧题源左边。\n \n-面向基础薄弱学习者的解析须逐题交代已知与目标、方法条件、关键推导原因和结果检查，不能只列公式及答案。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\n+面向基础薄弱学习者的解析，在揭示关键方法前先提出一道能尝试的小问题，并把提示另起一段，给读者留出独立思考的机会。完整写法见 `AGENTS.md`。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\n \n PDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。\n \n# 进度\n\n## 默认采用引导式解析\n\n- [x] 确认 `AGENTS.md` 定义写作规范，发布脚本负责编译已有 TeX。\n- [ ] 更新默认规范，核对变更并记录结果。\n\n## 同济线代同步测试卷\n\n# 完成标准\n\n## 默认采用引导式解析\n\n核对项目规范明确默认适用范围、提问先于方法、提示逐步具体、完整推导和适用的验算。检查 Git 差异及暂存范围。\n\n## 同济线代同步测试卷\n\n核对两组全部源图，按原卷核查题型、题号、选项、小问、矩阵和行列式，标明源图和可见的原卷疑义。用 KaTeX 检查交付 Markdown 中的公式。\n\n- **需求**：按项目排版要求，将已核对的同济线代同步测试题合进一份 TeX。\n- **实际结果**：四卷 68 道题沿用原卷题序与分值，补齐分步解析。题号同行标注原卷、照片编号及难度，题页留出手写演算区。单一 TeX 支持 A4、iPad 4:3 两种版式。\n- **验证**：逐题比对 Markdown 与 TeX，核对 80 个选项，复验 124 个数值结果。两版各 137 页、73 个书签，题目和解析页逐对相邻，最小演算留白为 408.4 和 199.7 bp。编译日志无缺字、警告或溢出。23 项仓库测试通过。\n- **涉及文件**：`references/同济线代/同步测试卷/`、`memory/`、`docs/CHANGELOG.md`。\n- **Git 提交**：`047d36a9948c3283414398fd8a85b07dfb555c06 docs: record the combined Tongji linear algebra tests`。TeX 与 PDF 按本地题源规则保存。\n\n---\nimport subprocess\nimport tempfile\nimport unittest\nfrom pathlib import Path\n\nimport release_tex\n\n\nclass PushPlanTests(unittest.TestCase):\n    def setUp(self):\n        work = Path(__file__).resolve().parents[2] / \".release-work\"\n        work.mkdir(exist_ok=True)\n        temporary = tempfile.TemporaryDirectory(dir=work)\n        self.addCleanup(temporary.cleanup)\n        self.repo = Path(temporary.name)\n        self.git(\"init\", \"-q\")\n        self.git(\"config\", \"user.name\", \"Release Tests\")\n        self.git(\"config\", \"user.email\", \"release-tests@example.invalid\")\n        self.git(\"config\", \"commit.gpgsign\", \"false\")\n        self.first = \"output/27302阶段模拟卷/27302阶段模拟卷.tex\"\n        self.wide = \"output/302数学二分节真题集/302数学二分节真题集（原生LaTeX横屏版）.tex\"\n        self.a4 = \"output/302数学二分节真题集/302数学二分节真题集（原生LaTeX常规版）.tex\"\n        self.facsimile = \"output/302数学二分节真题集/302数学二分节真题集.tex\"\n        self.resource = \"output/302数学二分节真题集/302-question-facsimiles.pdf\"\n        for path in (self.first, self.wide, self.a4, self.facsimile, self.resource):\n"}

## tool · 2026-11-18T12:27:43Z


Script completed
Wall time 1.0 seconds
Output:

{"chunk_id":"e1b322","wall_time_seconds":0.792819958,"exit_code":0,"original_token_count":31,"output":".......................\n----------------------------------------------------------------------\nRan 23 tests in 0.686s\n\nOK\n"}

## tool · 2026-11-18T12:27:55Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:27:59Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"75a245","wall_time_seconds":0,"exit_code":128,"original_token_count":30,"output":"fatal: Unable to create '/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git/index.lock': Operation not permitted\n"}

## assistant · 2026-11-18T12:28:03Z

引导式写法已写入 `AGENTS.md`，23 项仓库测试通过。当前沙箱限制写入 Git 索引，我会按授权流程提交这次的文档变更。

## tool · 2026-11-18T12:28:16Z


Script completed
Wall time 10.3 seconds
Output:

{"chunk_id":"ed855c","wall_time_seconds":0.00001025,"exit_code":0,"original_token_count":86,"output":" AGENTS.md          |  5 ++++-\n docs/CHANGELOG.md  | 10 ++++++++++\n memory/gotchas.md  |  2 +-\n memory/plan.md     |  4 ++++\n memory/progress.md |  5 +++++\n memory/verify.md   |  4 ++++\n 6 files changed, 28 insertions(+), 2 deletions(-)\n[main 187998e] docs: default to guided math solutions\n 6 files changed, 28 insertions(+), 2 deletions(-)\n"}

## tool · 2026-11-18T12:28:18Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"16cff7","wall_time_seconds":0.000011333,"exit_code":0,"original_token_count":405,"output":"187998e31154f4893a836b6cfc11c8ed78c8957e docs: default to guided math solutions\n---\n\n## [2026-11-18 20:27] 默认采用引导式数学题解\n\n- **需求**：将类似 Chat 模式的引导式解题设为项目默认写法。\n- **实际结果**：新写或修订题解时，先就题目线索提问，再分步提示，最后展开完整推导并按需验算。\n- **验证**：核对写作规范、适用范围和文档差异。23 项仓库测试通过。\n- **涉及文件**：`AGENTS.md`、`memory/`、`docs/CHANGELOG.md`。\n- **Git 提交**：待提交。\n\n---\n## main...origin/main [ahead 1]\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/302\\346\\225\\260\\345\\255\\246\\344\\272\\214\\345\\210\\206\\350\\212\\202\\347\\234\\237\\351\\242\\230\\351\\233\\206/302-question-facsimiles.pdf\"\n"}

## tool · 2026-11-18T12:28:22Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:28:37Z


Script completed
Wall time 9.9 seconds
Output:

{"chunk_id":"bf3146","wall_time_seconds":1.002514208,"session_id":92838,"original_token_count":178,"output":"diff --git a/docs/CHANGELOG.md b/docs/CHANGELOG.md\nindex aa2bfaa..c667150 100644\n--- a/docs/CHANGELOG.md\n+++ b/docs/CHANGELOG.md\n@@ -807,6 +807,6 @@\n - **实际结果**：新写或修订题解时，先就题目线索提问，再分步提示，最后展开完整推导并按需验算。\n - **验证**：核对写作规范、适用范围和文档差异。23 项仓库测试通过。\n - **涉及文件**：`AGENTS.md`、`memory/`、`docs/CHANGELOG.md`。\n-- **Git 提交**：待提交。\n+- **Git 提交**：`187998e31154f4893a836b6cfc11c8ed78c8957e docs: default to guided math solutions`。\n \n ---\n[main 6fcf6c4] docs: link guided solutions changelog to its commit\n 1 file changed, 1 insertion(+), 1 deletion(-)\n"}

## tool · 2026-11-18T12:28:41Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"82e3d1","wall_time_seconds":0.000019292,"exit_code":0,"original_token_count":23,"output":"To https://github.com/OyamaMeek/codex-question-bank.git\n   14c4819..6fcf6c4  main -> main\n"}
{"chunk_id":"9907a6","wall_time_seconds":0.000010583,"exit_code":0,"original_token_count":325,"output":"## main...origin/main\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/302\\346\\225\\260\\345\\255\\246\\344\\272\\214\\345\\210\\206\\350\\212\\202\\347\\234\\237\\351\\242\\230\\351\\233\\206/302-question-facsimiles.pdf\"\n6fcf6c4a2054fcf9fca4c30b75e206b9633575b3\n6fcf6c4a2054fcf9fca4c30b75e206b9633575b3\n34:- 新写或修订数学题解时，默认采用引导式解析，让第一次接触该题型、基础薄弱的读者也能先尝试，再独立读懂完整解法。\n"}

## assistant · 2026-11-18T12:28:47Z

已把**引导式解析**设为项目默认写法，写入 [AGENTS.md](/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/AGENTS.md:34)。

以后新写或修订数学题解时，先从题目里挑一个具体线索，提出读者可以动手试的问题。提示另起一段，从观察条件逐步提示到可用的方法，让读者有机会先想一步。最后再展开完整推导，解释关键步骤的依据，并在适用时验算。

23 项仓库测试通过，已推送至 `origin/main`。本次只更新写作规范，未重编已有题集。

## user · 2026-11-18T12:29:28Z

你把同济线代同步测试题的解析重写一下给我看看


## assistant · 2026-11-18T12:29:31Z

我会先找到同济线代同步测试卷的原稿，再把解析改成先提问、分层提示、最后完整推导的写法。

## tool · 2026-11-18T12:29:33Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"62ee60","wall_time_seconds":0.000011041,"exit_code":0,"original_token_count":2864,"output":"## main...origin/main\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/302\\346\\225\\260\\345\\255\\246\\344\\272\\214\\345\\210\\206\\350\\212\\202\\347\\234\\237\\351\\242\\230\\351\\233\\206/302-question-facsimiles.pdf\"\nreferences/同济线代/同步测试卷/同济线性代数同步测试卷.tex\nreferences/同济线代/同步测试卷/行列式同步测试.md\nreferences/同济线代/同步测试卷/矩阵及其运算同步测试.md\n==> memory/plan.md <==\n# PDF 批量提取\n\n## 默认采用引导式解析\n\n更新根目录 `AGENTS.md` 的解析写作规范，将提问、提示、推导和验算写入默认流程，并同步复盘记录。范围为今后新增或修订的题解。\n\n## 同济线代同步测试卷\n\n按两组 HEIC 的文件顺序识别版面。用本机 RapidOCR 生成文字候选，逐题对照源图转写题干、选项、小问和公式，按章节和原卷归组写入本地 Markdown，并附源图定位。核查覆盖范围和 LaTeX 语法。\n\n将两章四卷的 68 道已核对题面合入一份可独立编译的 TeX，保留原卷题号、分值、选项和小问，标注卷别、照片号及难度。逐题补全入手思路、计算过程和验算。默认编译成 iPad 4:3 横屏，通过版式开关编译 A4。源稿和两版 PDF 随本地题源保存。\n\n## 整理 output 目录\n\n按六个题集或试卷系列归类。每个系列保留相互依赖的 LaTeX 源稿、样式与资源，成品按 `A4/`、`iPad/` 放置。仅合并逐字节相同的 PDF，本地编译副产物移入已忽略的工作目录。工作区已有的五处缺失继续保留，提交只迁移这些文件已跟踪的版本。同步 README、测试路径与发布依赖，纯迁移不产生新 Release。\n\n## 线性代数前两章模拟卷\n\n复筛适合尚未学习矩阵变换的读者。删去主要考查初等行列变换、消元讨论解的个数，或以相似对角化、分块相似显著简化的题。保留只用前两章行列式性质、矩阵运算和克拉默法则便可直接解答的题。在各卷内按原顺序重编号，保留单题分值并重算卷面总分，更新索引及同路径 PDF。\n\n在三卷 TeX 源稿及共用排版文件中将出处移到题目页标题同行，使用一至五个文字星号标记难度，紧邻出处右侧。按入手线索、计算量和推理层数逐题评级。补全关键算式和分情况理由，长解析续页。编译到独立验证目录，检查原题、出处、星号位置、题解页序和留白，再覆盖三卷 A4 与 iPad PDF。\n\n遍查本地 `references/302真题` 中 2009–2026 年数学一、二的 36 份逐年真题及配套解析中的旧题引录。筛选全题可仅用同济第七版印刷页第 1–55 页所学和直接代入完成的原题，保留原题条件、选项及双科共用题号，按年份建立真题索引。题量达到每卷约 12 题时，按单选、填空、解答分为三卷。每卷以同一正文编译 A4、iPad 两版，各题独占一页且后面紧接分步解析。\n\n## 数学分析期中1115\n\n检查四页原 PDF 的文字层及嵌入图像，按实际题面转录五大题至同目录 Markdown。文字层与本机 OCR 作为候选，逐题对照源页核对公式、选项、分值和小问。原卷标签或公式有疑义时保留原文并注明。交付按项目约定留在本地。\n\n\n==> memory/progress.md <==\n# 进度\n\n## 默认采用引导式解析\n\n- [x] 确认 `AGENTS.md` 定义写作规范，发布脚本负责编译已有 TeX。\n- [x] 更新默认规范和注意事项，核对文档差异。23 项仓库测试通过。\n\n## 同济线代同步测试卷\n\n- [x] 找到行列式、矩阵两组共 16 张源图。\n- [x] 已转录四卷 68 题，并逐题对照原图校订。\n- [x] 验证 68 道题、80 个选项、4 个编号小问、16 条原图链接及 264 个 LaTeX 表达式。\n- [x] 生成四卷合并的单文件 TeX，完成 68 道解析。\n- [x] 核对题面、复算关键答案并验证双版分页和演算留白。交付位于本地 `references/同济线代/同步测试卷/`，PDF 分别位于 `A4/` 和 `iPad/`。\n\n## 整理 output 目录\n\n- [x] 盘点现存文件、Git 状态和路径引用，确认两组 PDF 的 SHA-256 相同。\n- [x] 搬迁六个系列及编译副产物，更新文档、测试和发布依赖。\n- [x] 核对内容、版式、链接和实际编译，23 项项目测试通过。\n- [x] 提交 `d5bb77c` 已推送至 `origin/main`。本地发布计划为空，GitHub Actions 运行 `43773515662` 成功并跳过编译和上传。\n\n## 线性代数前两章模拟卷\n\n- [x] 按尚未学习矩阵变换的要求复筛三卷题目。\n- [x] 删去 12 道题，更新 23 道保留题的编号、索引和卷面总分。重编并覆盖六份正式 PDF 及卷一本地预览。\n\n- [x] 在源稿中将 35 道题的出处移到题页、添加难度星号并补详解。\n\n==> memory/verify.md <==\n# 完成标准\n\n## 默认采用引导式解析\n\n逐项核对项目规范，确认默认适用于新写或修订的题解，先提问，再按需给出更具体的提示，最后展开推导与验算。`git diff --check` 通过，23 项仓库测试通过。\n\n## 同济线代同步测试卷\n\n核对两组全部源图，按原卷核查题型、题号、选项、小问、矩阵和行列式，标明源图和可见的原卷疑义。用 KaTeX 检查交付 Markdown 中的公式。\n\n16 张源图均取得 RapidOCR 结果并逐题对照。四卷各有 17 题，均为 5 道选择题、5 道填空题和 7 道解答题，合计每卷 100 分。题序、80 个选项、4 个编号小问和 16 条原图链接通过检查，264 个 LaTeX 表达式通过 KaTeX 渲染。行列式 B 卷第 13 题第三行第三列保留原印刷指数并加注。\n\n合卷 TeX 验收覆盖四卷各 17 题、原题序、全部选项及公式、题号同一行的出处和难度、解析与题面相邻、题页演算区。复算各卷关键结果，并编译核对 A4 与 800×600 bp PDF 的分页和日志。\n\n68 份 TeX 题面与已校对 Markdown 逐题比对通过，20 道单选的答案字母核对通过。124 项数值复验和 23 项仓库测试通过。两版均为 137 页、73 个书签，所有题目均独占一页，下一页为对应解析。A4 和 iPad 最小演算留白分别为 408.4 和 199.7 bp。编译无缺字、警告和溢出。版式检查使用 PDF 文本与坐标。\n\n## 整理 output 目录\n\n核对现有题稿、资料和正式 PDF 的 Git 内容，确认目录与版式相符、无重复 PDF、编译资源的相对路径可用。运行全部项目测试，检查新路径上的编译入口、README 链接以及纯迁移的空发布计划。保留原工作区缺失及本地编译产物。\n\n提交含 47 个内容逐字节相同的文件迁移和 1 个重复 PDF 的删除。验证检出中的 26 条 README 链接均存在，18 份成品 PDF 版式与目录一致且哈希互不相同。Tectonic 0.17.0 成功编译 19 个入口，裁片版仍有既存的 PDF 版本和重复页锚点警告。23 项项目测试通过，覆盖仅移动源稿的发布计划。提交 `d5bb77c` 的发布计划为空，GitHub Actions 运行 `43773515662` 成功，依发布条件跳过编译和上传。\n\n## 线性代数前两章模拟卷\n\n复筛后核对删题清单、保留题面和解析、连续题号、各卷分值、索引逐行映射，以及双版式页序与编译日志。\n\n复筛结果为 9、7、7 题和满分 72、64、62 分。保留题干、详解、出处、难度和单题分值逐题一致。A4 为 19、15、15 页，iPad 为 19、15、16 页。六份正式 PDF 经验证后原位覆盖，卷一本地预览及 SyncTeX 同步重编，预览文字和书签与正式 iPad 版逐页一致。22 项仓库测试通过。\n\n# 注意事项\n\n线性代数前两章阶段，筛掉以矩阵初等变换、消元讨论、相似对角化为主要捷径的题。行列式的行列运算属于第一章，保留相应题目。\n\n线性代数前两章模拟卷的出处显示在题目页，文字星号紧接出处右侧。评级依据题目本身的计算与推理负担。\n\n按指定范围选编多套模拟卷时，先复核题库里符合范围且互不重复的完整原题数量，再决定卷数。用户要求题量充足时，以仓库已有阶段卷的规模作为参考。\n\n李林题集的难度星号与题号同行，使用小号灰字，紧靠右侧题源左边。\n\n面向基础薄弱学习者的解析，在揭示关键方法前先提出一道能尝试的小问题，并把提示另起一段，给读者留出独立思考的机会。完整写法见 `AGENTS.md`。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\n\nPDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。\n\n数学教材的整页或半页OCR可能漏掉独立公式、合并矩阵或丢失不等号。需按版面区分正文与公式，再对照原页核对；页数、链接和公式渲染通过都不能代替内容校对。源文件跳页时按印刷页码记录缺失范围，不补造题目。\n\n用户要求题面以原生 LaTeX 转录时，题干、选项、公式和必要图形需要可编辑。PDF 裁片仅用于内部核对。\n\n真题集的行内极限也将趋近条件排在 `lim` 正下方。题头显示原卷年份和题号，原卷页码只留作 LaTeX 源稿中的定位信息。\n\n# 工具\n\n同济线代同步测试卷由 FFmpeg 解码 HEIC，使用本机 RapidOCR（ONNX Runtime）提取文字，对照原图逐题校订，用 KaTeX 检查公式语法。\n\n同济线代合卷将两份已校对 Markdown 的题面与逐题解析合成单个源稿，采用 Tectonic 0.17.0 和 ctex 编译，用 NumPy 复验关键结果，用 PyMuPDF 核对页序、尺寸、题头位置及留白。\n\n线性代数前两章模拟卷用 PyMuPDF 读取逐年原卷的文字与公式字形坐标，结合真题 Markdown、配套解析校核。扫描公式用本地 PaddleOCR-VL 提取候选并结合对应解析复核。使用 Tectonic 0.17.0、ctex 和双版式入口编译，用 Python 和 mpmath 复算并检查 PDF 页序与留白。\n\n数学分析期中1115 使用 PyMuPDF 提取文字层和嵌入图片，使用本机 RapidOCR 识别题面，对照原卷逐题核对，并用既有 KaTeX 脚本检查公式。\n\n数学分析期中1115 的 LaTeX 版复用 Tectonic 0.17.0、ctex 和双入口试卷模板。用 PyMuPDF 检查分页和字形坐标，用 mpmath 独立复算关键结果。\n\n.\n..\n.DS_Store\n.agent\n.git\n.github\n.gitignore\n.question-bank-work\n.release-work\nAGENTS.md\nREADME.md\ndocs\nmemory\noutput\nreferences\nremote-checkout\n"}

## assistant · 2026-11-18T12:29:36Z

我会用 PDF 技能重编 A4 和 iPad 两版，并核对题目与解析的页序。

## tool · 2026-11-18T12:29:41Z


Script completed
Wall time 0.2 seconds
Output:

Warning: truncated output (original token count: 11777)
Total output lines: 1

[{"status":"fulfilled","value":{"chunk_id":"31e805","wall_time_seconds":0.010077833,"exit_code":0,"original_token_count":12912,"output":"Warning: truncated output (original token count: 12912)\nTotal output lines: 815\n\n---\nname: \"pdf\"\ndescription: \"Read, create, inspect, render, and verify PDF files where visual layout matters, including fillable AcroForms. Use Poppler rendering plus Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction.\"\n---\n\n# PDF Skill\n\n## When To Use\n\n- Read or review PDF content where layout and visuals matter.\n- Create PDFs programmatically with reliable formatting.\n- Fill and validate interactive PDF forms.\n- Validate final rendering before delivery.\n\n## Workflow\n\n1. Prefer visual review: render PDF pages to PNGs and inspect them.\n   - Use `pdftoppm` from the bundled runtime or system Poppler when available.\n   - If unavailable, install Poppler or ask the user to review the output locally.\n2. Use `reportlab` to generate PDFs when creating new documents.\n3. Use `pdfplumber` or `pypdf` for text extraction and quick checks; do not rely on text extraction for layout fidelity.\n4. After each meaningful update, re-render pages and verify alignment, spacing, and legibility.\n\n## Fill And Validate AcroForms\n\nVisual review alone is not a correctness check for a fillable PDF. A page `/Widget` annotation can render a value from its appearance stream while the canonical `/AcroForm/Fields` tree is missing or contains a stale value.\n\n1. Keep the result interactive by default; set `flatten=True` only when the user explicitly requests a completed, static form. Preserve the source PDF, and do not flatten a signed PDF without an explicit workflow decision.\n2. Inspect both representations before filling: enumerate fields from `reader.get_fields()` and `/Widget` annotations from every page's `/Annots`, following `/Parent` and `/Kids`. If a widget and a canonical field have the same name but are distinct objects with no `/Parent` relationship, do not call `reattach_fields()` blindly: it can create a second top-level field with the same name. Report the ambiguity or produce a static result.\n3. Recover genuinely orphaned widgets, fill all pages, and write the result with `pypdf`:\n\n```python\nfrom pypdf import PdfReader, PdfWriter\nfrom pypdf.generic import NameObject\n\nreader = PdfReader(input_pdf)\nwriter = PdfWriter()\nwriter.clone_document_from_reader(reader)\n\n# Restores widgets that are missing from /AcroForm/Fields.\nwriter.reattach_fields()\nfields = writer.get_fields() or {}\nmissing = set(expected_values) - set(fields)\nif missing:\n    raise ValueError(f\"Form fields not found after repair: {sorted(missing)}\")\n\nvalues_to_write = dict(expected_values)\nif flatten:\n    # Paint every existing value before removing every widget.\n    values_to_write = {\n        name: field.get(\"/V\", \"/Off\" if field.get(\"/FT\") == \"/Btn\" else \"\")\n        for name, field in fields.items()\n    }\n    values_to_write.update(expected_values)\n\nwriter.update_page_form_field_values(\n    None, values_to_write, auto_regenerate=False, flatten=flatten\n)\n\nif flatten:\n    # pypdf's flatten=True paints appearances but does not remove widgets.\n    writer.remove_annotations(subtypes=\"/Widget\")\n    writer.root_object.pop(NameObject(\"/AcroForm\"), None)\n\nwith open(output_pdf, \"wb\") as stream:\n    writer.write(stream)\n```\n\n4. Reopen the written PDF before delivery. For an interactive result, require every expected field to be present in `get_fields()` with the expected `/V`, enumerate page widgets again, and confirm their effective `/V` (the widget value or inherited `/Parent` value) agrees. Confirm each updated widget has a non-empty `/AP` `/N` appearance and render the final pages to catch stale or clipped appearances. Do not rely on `/NeedAppearances` or a successful PNG render as proof that logical field data was updated.\n5. For a flattened result, require zero `/Widget` annotations and no remaining `/AcroForm` field tree after reopening, then render the final pages. Keep an editable copy when the user may need to revise the form.\n\n## Temp And Output Conventions\n\n- Use `tmp/pdfs/` for intermediate files; delete them when done.\n- Write final artifacts under `output/pdf/` when working in this repo.\n- Keep filenames stable and descriptive.\n\n## Dependencies\n\nPrefer the Codex bundled workspace/runtime dependencies when available. The primary runtime is expected to include:\n\n- Python packages: `reportlab`, `pdfplumber`, `pypdf`\n- Rendering tools: `pdftoppm` and `pdfinfo` from Poppler\n\nIf a dependency is missing, install only what is needed.\n\nPython packages:\n\n```bash\nuv pip install reportlab pdfplumber pypdf\n```\n\nIf `uv` is unavailable:\n\n```bash\npython3 -m pip install reportlab pdfplumber pypdf\n```\n\nSystem tools for rendering:\n\n```bash\n# macOS (Homebrew)\nbrew install poppler\n\n# Ubuntu/Debian\nsudo apt-get install -y poppler-utils\n```\n\nIf installation is not possible in this environment, tell the user which dependency is missing and how to install it locally.\n\n## Environment\n\nNo required environment variables.\n\n## Rendering Command\n\n```bash\npdftoppm -png \"$INPUT_PDF\" \"$OUTPUT_PREFIX\"\n```\n\n## Quality Expectations\n\n- Maintain polished visual design: consistent typography, spacing, margins, and section hierarchy.\n- Avoid rendering issues: clipped text, overlapping elements, broken tables, black squares, or unreadable glyphs.\n- Charts, tables, and images must be sharp, aligned, and clearly labeled.\n- Use ASCII hyphens only. Avoid U+2011 and other Unicode dashes.\n- Citations and references must be human-readable; never leave tool tokens or placeholder strings.\n\n## Final Checks\n\n- Do not deliver until the latest PNG inspection shows zero visual or formatting defects.\n- Confirm headers, footers, page numbering, and section transitions look polished.\n- Keep intermediate files organized or remove them after final approval.\n\n## Final response\n\n### Final Response Citations\n\n- **Create/edit:** for created or edited PDFs, cite each final deliverable exactly once with `purpose=\"output\"`, in its own paragraph. Briefly describe the result without repeating its filename, path, or link. Never put output directives inside prose or list items.\n- **Q&A and summaries:** Every file whose contents you summarize or use to support an answer MUST receive a `:codex-file-citation{...}` with `purpose=\"source\"` in the final response. Use the source citation in place of the filename, wherever the filename would appear. Do not write the filename separately and append its citation at the end. Files merely inspected but not used in the answer need no citation. Do not emit output citations for unchanged files or read-only answers.\n\n- Emit `:codex-file-citation{...}` directly, without backticks, code fences, or a Markdown-link wrapper. Use verified targets only. No need to cite or reference intermediate work.\n\nFor file citations, set `path` to the verified absolute file path on the task host. Omit `mode`.\n\nSome illustrative examples, real responses use verified targets outside code fences.\n\n```text\n:codex-file-citation{path=\"/absolute/path/review.pdf\" purpose=\"output\"}\n```\n\n```text\nThe review of :codex-file-citation{path=\"/absolute/path/review.pdf\" purpose=\"source\"} is due Friday.\n```\n\n\n### Additional Citation Guidance\n\nFor PDF Q&A, inspect complete relevant pages and preserve material headings, table/figure labels, footnotes, sources, and sample sizes. PDF citations support only plain file citations; do not add `artifact_kind`, `page_number`, or other locators.\ntotal 54632\ndrwxr-xr-x   388 oyamahappa  staff    12416 Nov 18 20:05 .\ndrwxr-xr-x    16 oyamahappa  staff      512 Nov 13 22:31 ..\n-rw-r--r--     1 oyamahappa  staff     5424 Nov 11 22:30 302-batch-pilot.json\n-rw-r--r--     1 oyamahappa  staff    11282 Nov 11 22:09 302-clean-finalize.txt\n-rw-r--r--     1 oyamahappa  staff    17159 Nov 11 22:07 302-clean-preview.txt\n-rw-r--r--     1 oyamahappa  staff    11371 Nov 11 22:08 302-clean-run.txt\n-rw-r--r--     1 oyamahappa  staff    31586 Nov 11 22:01 302-common.txt\n-rw-r--r--     1 oyamahappa  staff   143747 Nov 11 21:57 302-convert.jsonl\n-rw-r--r--     1 oyamahappa  staff     5427 Nov 11 22:33 302-edition-check.txt\n-rw-r--r--     1 oyamahappa  staff    57959 Nov 11 22:01 302-first.txt\n-rw-r--r--     1 oyamahappa  staff     2355 Nov 12 08:21 302-hefei-1-variants.md\n-rw-r--r--     1 oyamahappa  staff     6601 Nov 12 08:20 302-hefei-2.md\n-rw-r--r--     1 oyamahappa  staff     3670 Nov 12 03:14 302-lilin-spread-diff.txt\n-rw-r--r--     1 oyamahappa  staff     4812 Nov 11 22:14 302-lilin-volume-1.md\n-rw-r--r--     1 oyamahappa  staff     5677 Nov 11 22:21 302-lilin-volume-2.md\n-rw-r--r--     1 oyamahappa  staff     5103 Nov 11 22:25 302-lilin-volume-3.md\n-rw-r--r--     1 oyamahappa  staff     5877 Nov 11 22:28 302-lilin-volume-4.md\n-rw-r--r--     1 oyamahappa  staff     5658 Nov 11 22:29 302-lilin-volume-5.md\n-rw-r--r--     1 oyamahappa  staff     5476 Nov 11 22:31 302-lilin-volume-6.md\n-rw-r--r--     1 oyamahappa  staff     6567 Nov 11 22:34 302-liyanfang-volume-1.md\n-rw-r--r--     1 oyamahappa  staff     6647 Nov 12 03:20 302-liyanfang-volume-2.md\n-rw-r--r--     1 oyamahappa  staff     7789 Nov 11 22:41 302-liyanfang-volume-3.md\ndrwxr-xr-x   257 oyamahappa  staff     8224 Nov 12 22:16 302-ocr-cache\ndrwxr-xr-x    20 oyamahappa  staff      640 Nov 11 22:13 302-ocr-model\n-rw-r--r--     1 oyamahappa  staff     3924 Nov 12 08:30 302-older-10-1-unique-3.md\n-rw-r--r--     1 oyamahappa  staff     3610 Nov 12 09:28 302-older-10-1-unique-4.md\n-rw-r--r--     1 oyamahappa  staff     2918 Nov 12 09:29 302-older-10-1-unique-5.md\n-rw-r--r--     1 oyamahappa  staff     3226 Nov 12 09:30 302-older-10-1-unique-6.md\n-rw-r--r--     1 oyamahappa  staff     3222 Nov 12 09:31 302-older-10-1-unique-7.md\n-rw-r--r--     1 oyamahappa  staff     2692 Nov 12 09:32 302-older-10-1-unique-8.md\n-rw-r--r--     1 oyamahappa  staff     5998 Nov 12 09:33 302-older-10-1-unique-9.md\n-rw-r--r--     1 oyamahappa  staff     6642 Nov 12 08:24 302-older-10-1-volume-1.md\n-rw-r--r--     1 oyamahappa  staff     6796 Nov 12 08:28 302-older-10-1-volume-2.md\n-rw-r--r--     1 oyamahappa  staff     6372 Nov 12 08:30 302-older-10-1-volume-3.md\n-rw-r--r--     1 oyamahappa  staff     5201 Nov 12 09:28 302-older-10-1-volume-4.md\n-rw-r--r--     1 oyamahappa  staff     5886 Nov 12 09:29 302-older-10-1-volume-5.md\n-rw-r--r--     1 oyamahappa  staff     5929 Nov 12 09:37 302-older-10-1-volume-6.md\n-rw-r--r--     1 oyamahappa  staff     6075 Nov 12 09:34 302-older-10-1-volume-7.md\n-rw-r--r--     1 oyamahappa  staff     5948 Nov 12 09:32 302-older-10-1-volume-8.md\n-rw-r--r--     1 oyamahappa  staff     6625 Nov 12 09:33 302-older-10-1-volume-9.md\n-rw-r--r--     1 oyamahappa  staff    10248 Nov 12 08:28 302-older-twenty-comparison.txt\n-rw-r--r--     1 oyamahappa  staff     1239 Nov 11 22:19 302-primary-current.json\n-rw-r--r--     1 oyamahappa  staff     1104 Nov 11 22:19 302-primary-older.json\ndrwxr-xr-x  1067 oyamahappa  staff    34144 Nov 12 09:43 302-proof-source\n-rw-r--r--     1 oyamahappa  staff    31078 Nov 11 22:04 302-spreads.json\n-rw-r--r--     1 oyamahappa  staff     5699 Nov 12 08:24 302-ten-two-v1.md\n-rw-r--r--     1 oyamahappa  staff     5837 Nov 12 08:25 302-ten-two-v2.md\n-rw-r--r--     1 oyamahappa  staff     5571 Nov 12 08:27 302-ten-two-v3.md\n-rw-r--r--     1 oyamahappa  staff     4773 Nov 12 08:28 302-ten-two-v4.md\n-rw-r--r--     1 oyamahappa  staff     5265 Nov 12 08:29 302-ten-two-v5.md\n-rw-r--r--     1 oyamahappa  staff     6068 Nov 12 09:39 302-ten-two-v6.md\n-rw-r--r--     1 oyamahappa  staff     5585 Nov 12 09:32 302-ten-two-v7.md\n-rw-r--r--     1 oyamahappa  staff     5324 Nov 12 09:34 302-ten-two-v8.md\n-rw-r--r--     1 oyamahappa  staff     5247 Nov 12 09:31 302-ten-two-v9.md\n-rw-r--r--     1 oyamahappa  staff     2942 Nov 12 09:40 302-twenty-one-unique-4.md\n-rw-r--r--     1 oyamahappa  staff     2391 Nov 12 09:41 302-twenty-one-unique-5.md\n-rw-r--r--     1 oyamahappa  staff     3011 Nov 12 09:42 302-twenty-one-unique-6.md\n-rw-r--r--     1 oyamahappa  staff     5977 Nov 12 09:40 302-twenty-one-zhang4.md\n-rw-r--r--     1 oyamahappa  staff     5637 Nov 12 09:41 302-twenty-one-zhang5.md\n-rw-r--r--     1 oyamahappa  staff     6724 Nov 12 09:42 302-twenty-one-zhang6.md\n-rw-r--r--     1 oyamahappa  staff     5670 Nov 12 09:35 302-twenty-two-zhang4.md\n-rw-r--r--     1 oyamahappa  staff     5443 Nov 12 09:40 302-twenty-two-zhang5.md\n-rw-r--r--     1 oyamahappa  staff     6006 Nov 12 09:40 302-twenty-two-zhang6.md\n-rw-r--r--     1 oyamahappa  staff   310445 Nov 11 23:03 302-vlm-batch.jsonl\n-rw-r--r--     1 oyamahappa  staff  1026827 Nov 11 23:58 302-vlm-older.jsonl\n-rw-r--r--     1 oyamahappa  staff     5662 Nov 11 22:15 302-vlm-pilot.jsonl\n-rw-r--r--     1 oyamahappa  staff     1311 Nov 11 22:42 302-wu-august.md\n-rw-r--r--     1 oyamahappa  staff     2751 Nov 11 22:45 302-wu-basic-1-variants.md\n-rw-r--r--     1 oyamahappa  staff     6743 Nov 11 22:51 302-wu-basic-1.md\n-rw-r--r--     1 oyamahappa  staff     6334 Nov 11 22:44 302-wu-basic-2.md\n-rw-r--r--     1 oyamahappa  staff     1198 Nov 11 22:45 302-wu-basic-3-variants.md\n-rw-r--r--     1 oyamahappa  staff     6372 Nov 11 22:46 302-wu-basic-3.md\n-rw-r--r--     1 oyamahappa  staff     9256 Nov 11 22:51 302-wu-basic-all.md\n-rw-r--r--     1 oyamahappa  staff     1179 Nov 11 22:42 302-wu-july.md\n-rw-r--r--     1 oyamahappa  staff     2581 Nov 12 03:37 302-zhang-1-unique-1.md\n-rw-r--r--     1 oyamahappa  staff     3081 Nov 12 03:38 302-zhang-1-unique-2.md\n-rw-r--r--     1 oyamahappa  staff     4124 Nov 12 03:42 302-zhang-1-unique-3.md\n-rw-r--r--     1 oyamahappa  staff     3442 Nov 12 03:52 302-zhang-1-unique-4.md\n-rw-r--r--     1 oyamahappa  staff     3679 Nov 12 03:44 302-zhang-1-unique-5.md\n-rw-r--r--     1 oyamahappa  staff     3341 Nov 12 03:45 302-zhang-1-unique-6.md\n-rw-r--r--     1 oyamahappa  staff     3814 Nov 12 03:46 302-zhang-1-unique-7.md\n-rw-r--r--     1 oyamahappa  staff     3449 Nov 12 03:47 302-zhang-1-unique-8.md\n-rw-r--r--     1 oyamahappa  staff     5593 Nov 12 03:37 302-zhang-1-volume-1.md\n-rw-r--r--     1 oyamahappa  staff     6098 Nov 12 03:38 302-zhang-1-volume-2.md\n-rw-r--r--     1 oyamahappa  staff     6017 Nov 12 03:42 302-zhang-1-volume-3.md\n-rw-r--r--     1 oyamahappa  staff     5987 Nov 12 03:52 302-zhang-1-volume-4.md\n-rw-r--r--     1 oyamahappa  staff     6792 Nov 12 03:44 302-zhang-1-volume-5.md\n-rw-r--r--     1 oyamahappa  staff     5851 Nov 12 03:45 302-zhang-1-volume-6.md\n-rw-r--r--     1 oyamahappa  staff     7006 Nov 12 03:46 302-zhang-1-volume-7.md\n-rw-r--r--     1 oyamahappa  staff     6166 Nov 12 03:47 302-zhang-1-volume-8.md\n-rw-r--r--     1 oyamahappa  staff     5838 Nov 12 03:22 302-zhang-2-volume-1.md\n-rw-r--r--     1 oyamahappa  staff     6015 Nov 12 03:24 302-zhang-2-volume-2.md\n-rw-r--r--     1 oyamahappa  staff     6173 Nov 12 03:26 302-zhang-2-volume-3.md\n-rw-r--r--     1 oyamahappa  staff     5770 Nov 12 03:28 302-zhang-2-volume-4.md\n-rw-r--r--     1 oyamahappa  staff     6613 Nov 12 03:29 302-zhang-2-volume-5.md\n-rw-r--r--     1 oyamahappa  staff     5099 Nov 12 03:31 302-zhang-2-volume-6.md\n-rw-r--r--     1 oyamahappa  staff     6691 Nov 12 03:33 302-zhang-2-volume-7.md\n-rw-r--r--     1 oyamahappa  staff     6027 Nov 12 03:34 302-zhang-2-volume-8.md\n-rw-r--r--     1 oyamahappa  staff     8434 Nov 12 03:52 302-zhang-editions-check.txt\n-rw-r--r--     1 oyamahappa  staff     6847 Nov 12 03:58 302-zhang-horizontal-check.txt\n-rw-r--r--     1 oyamahappa  staff     2930 Nov 12 08:17 302-zhang-printed-check.txt\n-rw-r--r--     1 oyamahappa  staff     3328 Nov 12 03:35 302-zhang-shared.txt\n-rw-r--r--     1 oyamahappa  staff     1440 Nov 11 22:50 302-zhang-topic-figures.md\ndrwxr-xr-x     3 oyamahappa  staff       96 Nov 12 22:15 __pycache__\n-rw-r--r--     1 oyamahappa  staff     2062 Nov 12 08:21 apply-302-hefei.py\n-rw-r--r--     1 oyamahappa  staff     1077 Nov 12 08:26 apply-302-older-twenty.py\n-rw-r--r--     1 oyamahappa  staff      766 Nov 12 09:39 apply-302-ten-two.py\n-rw-r--r--     1 oyamahappa  staff      870 Nov 12 14:31 apply-302-topic-verified.py\n-rw-r--r--     1 oyamahappa  staff     2459 Nov 12 09:40 apply-302-twenty-two.py\n-rw-r--r--     1 oyamahappa  staff      727 Nov 11 22:43 apply-302-verified-paper.py\n-rw-r--r--     1 oyamahappa  staff     2892 Nov 12 03:11 apply-302-verified-volume.py\n-rw-r--r--     1 oyamahappa  staff     1006 Nov 12 09:31 apply-older-forty.py\n-rw-r--r--     1 oyamahappa  staff     1010 Nov 12 08:30 assemble-302-older-10-one.py\n-rw-r--r--     1 oyamahappa  staff     1098 Nov 12 09:40 assemble-302-twenty-one.py\n-rw-r--r--     1 oyamahappa  staff     1816 Nov 11 22:50 assemble-302-wu-basic.py\n-rw-r--r--     1 oyamahappa  staff     1101 Nov 12 03:37 assemble-302-zhang-1.py\n-rw-r--r--     1 oyamahappa  staff     5881 Nov 13 21:56 assemble-lilin-high-math.py\n-rw-r--r--     1 oyamahappa  staff     5152 Nov 13 23:18 assemble-linear-algebra.cjs\n-rw-r--r--     1 oyamahappa  staff     1247 Nov 12 09:32 assemble-older-lilin-2.py\n-rw-r--r--     1 oyamahappa  staff     3117 Nov 12 09:39 assemble-older-topics.py\n-rw-r--r--     1 oyamahappa  staff     2200 Nov 12 09:39 audit-302-ten-twenty-lost-ink.py\ndrwxr-xr-x     4 oyamahappa  staff      128 Nov 12 20:05 bank-verify\n-rw-r--r--     1 oyamahappa  staff     3154 Nov 11 22:18 batch-proof-302.py\n-rw-r--r--     1 oyamahappa  staff    14980 Nov 14 10:26 build-lilin-ipad.py\n-rw-r--r--     1 oyamahappa  staff     2279 Nov 11 22:32 check-302-source-editions.py\n-rw-r--r--     1 oyamahappa  staff     2011 Nov 12 15:21 check-bank-math.py\n-rw-r--r--     1 oyamahappa  staff     5094 Nov 12 20:10 check-bank-output.py\n-rw-r--r--     1 oyamahappa  staff      937 Nov 13 21:31 check-lilin-high-math.cjs\n-rw-r--r--     1 oyamahappa  staff     7684 Nov 14 10:08 check-lilin-integrals.py\n-rw-r--r--     1 oyamahappa  staff     2887 Nov 14 10:08 check-lilin-limits-expanded.py\n-rw-r--r--     1 oyamahappa  staff      761 Nov 14 10:12 check-lilin-math.cjs\n-rw-r--r--     1 oyamahappa  staff     6078 Nov 13 22:45 check-lilin-ode-numeric.js\n-rw-r--r--     1 oyamahappa  staff      953 Nov 12 22:31 check-linear-algebra.py\n-rw-r--r--     1 oyamahappa  staff     2688 Nov 12 14:43 check-topic8.py\n-rw-r--r--     1 oyamahappa  staff    11667 Nov 11 22:08 clean-302-questions.py\n-rw-r--r--     1 oyamahappa  staff     2548 Nov 12 08:28 compare-302-older-twenty.py\n-rw-r--r--     1 oyamahappa  staff     4194 Nov 12 03:56 compare-302-zhang-a4.py\n-rw-r--r--     1 oyamahappa  staff     1518 Nov 12 03:35 compare-302-zhang-shared.py\n-rw-r--r--     1 oyamahappa  staff    18844 Nov 11 21:58 convert-302.py\n-rw-r--r--     1 oyamahappa  staff      344 Nov 12 09:41 copy-older-topic-zhang8.py\n-rw-r--r--     1 oyamahappa  staff     2231 Nov 12 22:15 extract-linear-algebra.py\n-rw-r--r--     1 oyamahappa  staff     5726 Nov 12 03:48 filter-302-zhang-math3.py\ndrwxr-xr-x     7 oyamahappa  staff      224 Nov 11 22:13 hf\n-rw-r--r--     1 oyamahappa  staff     1273 Nov 11 22:01 inspect-302-questions.py\n-rw-r--r--     1 oyamahappa  staff     3681 Nov 13 21:48 inspect_lilin_high_math.py\n-rw-r--r--     1 oyamahappa  staff     5192 Nov 12 22:36 layout-line…3412 tokens truncated…hang8-v5.md\n-rw-r--r--     1 oyamahappa  staff     3925 Nov 12 09:30 older-topic-candidate-1-zhang8-v6.md\n-rw-r--r--     1 oyamahappa  staff     4108 Nov 12 09:30 older-topic-candidate-1-zhang8-v7.md\n-rw-r--r--     1 oyamahappa  staff     3902 Nov 12 09:30 older-topic-candidate-1-zhang8-v8.md\n-rw-r--r--     1 oyamahappa  staff     4397 Nov 12 09:30 older-topic-candidate-2-chaoyue-v1.md\n-rw-r--r--     …1777 tokens truncated…e{amsmath,amssymb,xcolor,fancyhdr}\n\\usepackage[hidelinks,bookmarksopen=true]{hyperref}\n\\xeCJKDeclareCharClass{CJK}{\"2460 -> \"2463}\n\n\\definecolor{examaccent}{HTML}{175C57}\n\\setlength{\\parindent}{0pt}\n\\setlength{\\parskip}{5bp}\n\\setlength{\\headheight}{15bp}\n\\pagestyle{fancy}\n\\fancyhf{}\n\\renewcommand{\\headrulewidth}{0pt}\n\\newcommand{\\CurrentVolume}{同济线性代数同步测试卷}\n\\fancyfoot[L]{\\footnotesize\\textcolor{gray}{\\CurrentVolume}}\n\\fancyfoot[R]{\\footnotesize\\thepage}\n\\raggedbottom\n\\allowdisplaybreaks[1]\n\n\\newcommand{\\Volume}[2]{%\n  \\renewcommand{\\CurrentVolume}{#1}%\n  \\def\\VolumeId{#2}%\n}\n\\newcommand{\\Question}[5]{%\n  \\clearpage\n  \\def\\CurrentNumber{#1}%\n  \\ifnum#1=1\\relax\n    \\pdfbookmark[1]{\\CurrentVolume}{\\VolumeId}%\n  \\fi\n  \\pdfbookmark[2]{第 #1 题}{\\VolumeId-q#1}%\n  {\\small\\color{examaccent}#2\\hfill #3 分}\\par\n  {\\Large\\bfseries 第 #1 题}\\hfill\n  {\\footnotesize\\color{gray}\\CurrentVolume\\enspace IMG\\_#4\\enspace\\texttt{#5}}\\par\\smallskip\n  \\ifdefined\\QuestionBankAfour\n    \\fontsize{13}{20}\\selectfont\n  \\else\n    \\fontsize{13}{19}\\selectfont\n  \\fi\n}\n\\newcommand{\\Solution}{%\n  \\clearpage\n  \\fontsize{12}{18}\\selectfont\n  {\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par\\smallskip\n}\n\\newcommand{\\Known}{\\par\\textbf{已知与目标}\\quad}\n\\newcommand{\\Method}{\\par\\textbf{入手思路}\\quad}\n\\newcommand{\\Derive}{\\par\\textbf{推导}\\quad}\n\\newcommand{\\Verify}{\\par\\textbf{结论与检查}\\quad}\n\\newcommand{\\Choices}[4]{%\n  \\par\\medskip\n  \\begin{minipage}[t]{.48\\linewidth}(A)\\enspace #1\\end{minipage}\\hfill\n  \\begin{minipage}[t]{.48\\linewidth}(B)\\enspace #2\\end{minipage}\\par\\medskip\n  \\begin{minipage}[t]{.48\\linewidth}(C)\\enspace #3\\end{minipage}\\hfill\n  \\begin{minipage}[t]{.48\\linewidth}(D)\\enspace #4\\end{minipage}\\par\n}\n\\newcommand{\\blank}{\\underline{\\hspace{5em}}}\n\n\\begin{document}\n\\pdfbookmark[0]{同济线性代数同步测试卷}{cover}\n{\\small\\color{examaccent}同济大学《线性代数》第七版配套练习}\\par\\bigskip\n{\\Huge\\bfseries 同济线性代数同步测试卷}\\par\\medskip\n{\\Large 行列式 · 矩阵及其运算}\\par\\bigskip\n\n第一章　行列式同步测试（A 卷、B 卷）\\par\n第二章　矩阵及其运算同步测试（A 卷、B 卷）\\par\\bigskip\n\n每卷 17 题，满分 100 分。单项选择题、填空题各 5 道，每题 3 分。解答题 7 道，每题 10 分。\\par\n原卷注：未标注的题目，考研数一、数二、数三均要考查。\\par\n题号旁标有原卷、照片编号与难度星号。每道题下方留有演算空间，翻页可看解析。\n\n\\Volume{行列式 A 卷}{det-a}\n\n\\Question{1}{单项选择题}{3}{1657}{**}\n排列 $217986354$ 的逆序数为（　　）。\n\\Choices\n  {$12$}\n  {$14$}\n  {$18$}\n  {$22$}\n\n\\Solution\n\\Known 求排列 $217986354$ 的逆序数。逆序是前面的数大于后面的数的一对位置。\n\\Method 固定每对逆序的左端，从左到右数该数字右边比它小的数。每一对只会被数一次。\n\\Derive $2$ 的右侧只有 $1$ 比它小。$7$ 的右侧有 $6,3,5,4$，$9$ 的右侧有 $8,6,3,5,4$，$8$ 的右侧有 $6,3,5,4$，$6$ 的右侧有 $3,5,4$，$5$ 的右侧有 $4$。按原顺序计数为\n\\[\n1+0+4+5+4+3+0+1+0=18.\n\\]\n\\Verify 选 \\textbf{C}。$1,3,4$ 作为左端时都不产生逆序。其余三项 $12,14,22$ 均与逐项计数不符。\n\n\\Question{2}{单项选择题}{3}{1657}{**}\n4 阶行列式 $\\begin{vmatrix}2&1&1&1\\\\4&0&1&1\\\\6&2&0&2\\\\8&3&3&0\\end{vmatrix}=$（　　）。\n\\Choices\n  {$32$}\n  {$-32$}\n  {$34$}\n  {$-34$}\n\n\\Solution\n\\Known 求给定四阶行列式的值。\n\\Method 第一列为 $2,4,6,8$，后三项都是首项的整倍数。把第一行的倍数分别减去，第一列就只剩一项。某行加上另一行的倍数，行列式不变。\n\\Derive 第二、三、四行分别减第一行的 $2,3,4$ 倍，再按第一列展开，\n\\[\nD=2\\begin{vmatrix}-2&-1&-1\\\\-1&-3&-1\\\\-1&-1&-4\\end{vmatrix}\n=2\\bigl[-2(12-1)+(4-1)-(1-3)\\bigr]=-34.\n\\]\n\\Verify 选 \\textbf{D}。三阶行列式为 $-17$，因子 $2$ 来自第一列的首元；其余选项都不等于 $2(-17)$。\n\n\\Question{3}{单项选择题}{3}{1657}{**}\n设 3 阶矩阵\n\n\\[\nA=\\begin{pmatrix}a_{11}&a_{12}&a_{13}\\\\a_{21}&a_{22}&a_{23}\\\\a_{31}&a_{32}&a_{33}\\end{pmatrix},\\quad\nB=\\begin{pmatrix}3a_{11}&a_{13}&a_{11}+a_{12}\\\\3a_{21}&a_{23}&a_{21}+a_{22}\\\\3a_{31}&a_{33}&a_{31}+a_{32}\\end{pmatrix},\n\\]\n\n且 $|A|=n$，则 $|B|=$（　　）。\n\\Choices\n  {$n$}\n  {$-27n$}\n  {$3n$}\n  {$-3n$}\n\n\\Solution\n\\Known $B$ 的每一列都可以由 $A$ 的列得到。设 $A$ 的三列为 $u,v,w$，且 $|u,v,w|=n$。\n\\Method 先把第三列中重复出现的 $u$ 去掉，再还原列序。\n\\Derive 按列的线性性，第一列提出 $3$，随后第三列减第一列，得\n\\[\n|B|=3|u,w,u+v|=3|u,w,v|=-3|u,v,w|=-3n.\n\\]\n最后一个负号来自第二列与第三列的一次交换。\n\\Verify 选 \\textbf{D}。用 $A=E_3$ 检查，$n=1$，交换后两列并将第一列放大为三倍，结果为 $-3$，也排除其余三项。\n\n\\Question{4}{单项选择题}{3}{1657}{***}\n下列 $n$ 阶行列式，一定等于 $-1$ 的是（　　）。\n\\Choices\n  {$\\begin{vmatrix}&&&&1\\\\&&&1&\\\\&&\\mathinner{\\raisebox{-0.15em}{·}\\mkern1mu\\raisebox{0.05em}{·}\\mkern1mu\\raisebox{0.25em}{·}}&&\\\\&1&&&\\\\1&&&&\\end{vmatrix}$}\n  {$\\begin{vmatrix}1&1&&&\\\\&1&1&&\\\\&&\\ddots&\\ddots&\\\\&&&1&1\\\\1&&&&1\\end{vmatrix}$}\n  {$\\begin{vmatrix}0&&&&1\\\\1&0&&&\\\\&1&\\ddots&&\\\\&&\\ddots&0&\\\\&&&1&0\\end{vmatrix}$}\n  {$\\begin{vmatrix}0&&&&1\\\\&1&&0&\\\\&&\\ddots&&\\\\&0&&1&\\\\1&&&&0\\end{vmatrix}$}\n\n\\Solution\n\\Known 比较四个 $n$ 阶行列式，找出恒等于 $-1$ 的一项。图中未写出的元素为零。\n\\Method 对只有一组非零乘积的行列式，行列式的符号就是该列号排列的符号。对前三项，找到一个阶数的反例即可排除恒等关系。\n\\Derive （D）由 $E_n$ 交换第一列与最后一列得到，只交换一次，所以等于 $-1$。（A）取 $n=4$，反序排列 $(4,3,2,1)$ 有六个逆序，值为 $1$。（B）取 $n=3$，非零项来自 $(1,2,3)$ 与 $(2,3,1)$，两项都为 $1$，总和为 $2$。（C）取 $n=3$，唯一非零项来自 $(3,1,2)$，有两个逆序，值为 $1$。\n\\Verify 选 \\textbf{D}。按该项首行再展开一次，也只有右上角的 $1$ 可取，剩余的单位块与左下角的 $1$ 共同给出一次端点交换的负号。\n\n\\Question{5}{单项选择题}{3}{1657}{**}\n$x=1$ 是 $\\begin{vmatrix}1&1&1\\\\1&x&x^2\\\\1&-2&4\\end{vmatrix}=0$ 的（　　）。\n\\Choices\n  {充分必要条件}\n  {充分非必要条件}\n  {必要非充分条件}\n  {既非充分也非必要条件}\n\n\\Solution\n\\Known 比较 $x=1$ 与题给行列式为零这两个条件。\n\\Method 充分性从 $x=1$ 出发检查行列式；必要性从行列式为零出发，检查是否只能取 $1$。\n\\Derive 当 $x=1$ 时，第二行等于第一行，故行列式为零。当 $x=-2$ 时，第二行等于第三行，行列式也为零。\n\\Verify 选 \\textbf{B}。代入这两个数分别核实了充分性与必要性的反例，因此排除（A）、（C）、（D）。\n\n\\Question{6}{填空题}{3}{1658}{**}\n3 阶行列式 $\\begin{vmatrix}-2&1&-3\\\\98&101&97\\\\1&-3&4\\end{vmatrix}=$ \\blank{}。\n\n\\Solution\n\\Known 求三行 $( -2,1,-3)$、$(98,101,97)$、$(1,-3,4)$ 构成的行列式。\n\\Method 第二行每个数恰好比第一行对应数大 $100$，先相减，再沿常数行制造零。\n\\Derive 第二行减第一行并提出因子 $100$。第二、三列再各减第一列，得到\n\\[\nD=100\\begin{vmatrix}-2&3&-1\\\\1&0&0\\\\1&-4&3\\end{vmatrix}\n=-100\\begin{vmatrix}3&-1\\\\-4&3\\end{vmatrix}=-500.\n\\]\n\\Verify 填 $\\boxed{-500}$。按第二行展开取第 $(2,1)$ 元，代数余子式符号为 $(-1)^3=-1$。\n\n\\Question{7}{填空题}{3}{1658}{**}\n4 阶行列式 $\\begin{vmatrix}1&1&1&1\\\\2&1&0&0\\\\0&3&1&0\\\\0&0&4&1\\end{vmatrix}=$ \\blank{}。\n\n\\Solution\n\\Known 四阶行列式的第一行全为 $1$，其余各行只有两个非零元。\n\\Method 按第一行展开。删去第一行和任意一列，剩下的三阶行列式都是三角形或分块三角形，可沿稀疏行逐个取元。\n\\Derive 删除的列依次为 $1,2,3,4$。各余子式的值依次为 $1\\cdot1\\cdot1$、$2\\cdot1\\cdot1$、$2\\cdot3\\cdot1$、$2\\cdot3\\cdot4$。乘上交替符号，\n\\[\nD=1-2+6-24=-19.\n\\]\n\\Verify 填 $\\boxed{-19}$。例如最后一个余子式为上三角行列式，主对角线为 $2,3,4$，其代数余子式为 $-24$。\n\n\\Question{8}{填空题}{3}{1658}{**}\n3 阶行列式 $\\begin{vmatrix}103&100&204\\\\199&200&395\\\\301&300&600\\end{vmatrix}=$ \\blank{}。\n\n\\Solution\n\\Known 求由三位数构成的行列式。第二列是 $100,200,300$。\n\\Method 第一列接近第二列，第三列接近第二列的两倍。利用列加减把两列都化成小整数，再按含零列展开。\n\\Derive 第一列减第二列，第三列减第二列的两倍，得\n\\[\nD=\\begin{vmatrix}3&100&4\\\\-1&200&-5\\\\1&300&0\\end{vmatrix}\n=4(-300-200)+5(900-100)=2000.\n\\]\n\\Verify 填 $\\boxed{2000}$。第三列只有前两项，其中第二项 $-5$ 的位置 $(2,3)$ 符号为负，这一项在展开式中的系数为 $+5$。\n\n\\Question{9}{填空题}{3}{1658}{***}\n5 阶行列式 $\\begin{vmatrix}3&0&0&0&4\\\\0&0&0&2&3\\\\0&0&5&0&2\\\\0&0&0&0&1\\\\0&4&0&0&1\\end{vmatrix}=$ \\blank{}。\n\n\\Solution\n\\Known 求题给五阶行列式。第四行只有第 $5$ 列的元素非零。\n\\Method 每个乘积必须从每行、每列各取一个元素。先由第四行确定第 $5$ 列，再排除其他行的第 $5$ 列。\n\\Derive 第四行取 $1$ 后，其余各行只剩一个可取元素。列号依次为 $(1,4,3,5,2)$。逆序对为 $(4,3)$、$(4,2)$、$(3,2)$、$(5,2)$，共有四对，故符号为正。\n\\[\nD=3\\cdot2\\cdot5\\cdot1\\cdot4=120.\n\\]\n\\Verify 填 $\\boxed{120}$。五个列号互不相同，且每一项都确实非零，因此这项既合法又唯一。\n\n\\Question{10}{填空题}{3}{1658}{***}\n3 阶行列式 $\\begin{vmatrix}x&y&x+y\\\\y&x+y&x\\\\x+y&x&y\\end{vmatrix}=$ \\blank{}。\n\n\\Solution\n\\Known 求由 $x,y,x+y$ 循环排列成的三阶行列式。\n\\Method 令 $z=x+y$，先数清三阶行列式中各乘积的符号，再用立方和恒等式整理。\n\\Derive 对排列后的三行 $(x,y,z),(y,z,x),(z,x,y)$ 展开，三个正项都是 $xyz$，三个负项分别为 $x^3,y^3,z^3$。因而\n\\[\n\\begin{aligned}\nD&=3xyz-x^3-y^3-z^3\\\\\n &=-(x+y+z)(x^2+y^2+z^2-xy-yz-zx)\\\\\n &=-2(x+y)(x^2-xy+y^2).\n\\end{aligned}\n\\]\n\\Verify 填 $\\boxed{-2(x+y)(x^2-xy+y^2)}$。取 $x=1,y=0$，按原矩阵展开得 $-2$，与公式一致。\n\n\\Question{11}{解答题}{10}{1658}{**}\n解方程 $\\begin{vmatrix}\\lambda-2&2&-1\\\\1&\\lambda-2&1\\\\-1&-2&\\lambda-2\\end{vmatrix}=0$。\n\n\\Solution\n\\Known 求使三阶行列式为零的 $\\lambda$。\n\\Method 三个对角元素都等于 $\\lambda-2$，先令 $t=\\lambda-2$，按第一行展开。\n\\Derive\n\\[\n\\begin{aligned}\nD&=t(t^2+2)-2(t+1)-(t-2)\\\\\n &=t^3-t=t(t-1)(t+1).\n\\end{aligned}\n\\]\n乘积为零当且仅当 $t=0,1,-1$ 中至少一项成立，换回 $\\lambda=t+2$。\n\\Verify 方程的解为 $\\boxed{\\lambda=1,2,3}$。这三个值代回因式分别使 $t+1,t,t-1$ 为零。\n\n\\Question{12}{解答题}{10}{1658}{**}\n计算 4 阶行列式 $\\begin{vmatrix}a_1&0&a_2&0\\\\0&b_1&0&b_2\\\\c_1&0&c_2&0\\\\0&d_1&0&d_2\\end{vmatrix}$。\n\n\\Solution\n\\Known 求非零元素分布在奇数行列和偶数行列两个位置组上的四阶行列式。\n\\Method 同时把行、列排成 $(1,3,2,4)$，可把两个位置组分别聚集到左上和右下。\n\\Derive 行交换与列交换各一次，其符号相消。因此\n\\[\nD=\\begin{vmatrix}a_1&a_2&0&0\\\\c_1&c_2&0&0\\\\0&0&b_1&b_2\\\\0&0&d_1&d_2\\end{vmatrix}\n=(a_1c_2-a_2c_1)(b_1d_2-b_2d_1).\n\\]\n相乘是因为非零乘积中，前两行只能从前两列取元。\n"}},{"status":"fulfilled","value":{"chunk_id":"57f8fe","wall_time_seconds":0.000011042,"exit_code":0,"original_token_count":1866,"output":".question-bank-work/verify-302-ten-twenty-two.py\n.question-bank-work/linear-algebra-filtered/verify.py\n.question-bank-work/tongji-tex/check-math.py\n.question-bank-work/tongji-tex/verify.py\n.question-bank-work/tongji-tex/ipad/同济线性代数同步测试卷.pdf\n.question-bank-work/tongji-tex/ipad/同济线性代数同步测试卷.log\n.question-bank-work/tongji-tex/det-b.txt\n.question-bank-work/tongji-tex/det-a.txt\n.question-bank-work/tongji-tex/mat-a.txt\n.question-bank-work/tongji-tex/mat-b.txt\n.question-bank-work/tongji-tex/a4/texput.pdf\n.question-bank-work/tongji-tex/a4/texput.log\n.question-bank-work/bank-verify/wide/302数学二分节真题集（原生LaTeX横屏版）.log\n.question-bank-work/bank-verify/wide/302数学二分节真题集（原生LaTeX横屏版）.pdf\n.question-bank-work/bank-verify/a4/302数学二分节真题集（原生LaTeX常规版）.pdf\n.question-bank-work/bank-verify/a4/302数学二分节真题集（原生LaTeX常规版）.log\n.question-bank-work/verify-notation.py\n.question-bank-work/verify-302-zhang-printed.py\n.question-bank-work/verify-302-zhang-horizontal.py\n.question-bank-work/verify-302-math.cjs\n.question-bank-work/linear-algebra-combined/verify.py\n.question-bank-work/linear-algebra-details/verify.py\n.question-bank-work/midterm-1115/verify-tex.py\n.question-bank-work/tongji-tests/IMG_1663.png\n.question-bank-work/tongji-tests/IMG_1663.jpg\n.question-bank-work/tongji-tests/IMG_1662.jpg\n.question-bank-work/tongji-tests/IMG_1662.png\n.question-bank-work/tongji-tests/IMG_1660.png\n.question-bank-work/tongji-tests/IMG_1660.jpg\n.question-bank-work/tongji-tests/IMG_1661.jpg\n.question-bank-work/tongji-tests/IMG_1661.png\n.question-bank-work/tongji-tests/IMG_1659.png\n.question-bank-work/tongji-tests/IMG_1671.png\n.question-bank-work/tongji-tests/IMG_1665.png\n.question-bank-work/tongji-tests/IMG_1659.jpg\n.question-bank-work/tongji-tests/IMG_1665.jpg\n.question-bank-work/tongji-tests/IMG_1671.jpg\n.question-bank-work/tongji-tests/IMG_1670.jpg\n.question-bank-work/tongji-tests/IMG_1664.jpg\n.question-bank-work/tongji-tests/IMG_1658.jpg\n.question-bank-work/tongji-tests/IMG_1664.png\n.question-bank-work/tongji-tests/IMG_1670.png\n.question-bank-work/tongji-tests/IMG_1658.png\n.question-bank-work/tongji-tests/IMG_1666.png\n.question-bank-work/tongji-tests/IMG_1672.png\n.question-bank-work/tongji-tests/IMG_1672.jpg\n.question-bank-work/tongji-tests/IMG_1666.jpg\n.question-bank-work/tongji-tests/IMG_1667.jpg\n.question-bank-work/tongji-tests/IMG_1667.png\n.question-bank-work/tongji-tests/probe-view.png\n.question-bank-work/tongji-tests/probe.png\n.question-bank-work/tongji-tests/vision.jsonl\n.question-bank-work/tongji-tests/IMG_1657.jpg\n.question-bank-work/tongji-tests/IMG_1657.png\n.question-bank-work/tongji-tests/IMG_1669.png\n.question-bank-work/tongji-tests/IMG_1669.jpg\n.question-bank-work/tongji-tests/IMG_1668.jpg\n.question-bank-work/tongji-tests/IMG_1668.png\n.question-bank-work/tongji-tests/rapidocr.jsonl\n.question-bank-work/verify-lilin-ipad.py\n.question-bank-work/ustc2026/verify.py\n.question-bank-work/verify-302.py\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/tectonic-format-latex.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/hyph-ka.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/hyph-gu.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/pgfmathfunctions.integerarithmetics.code.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/cmbx6.tfm\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/xetex.def\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/pgfcorepatterns.code.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/report.cls\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/loadhyph-tr.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/ctex.cfg\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/loadhyph-te.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/hyph-quote-oc.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/loadhyph-lt.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/fontspec-xetex.sty\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/cmsy8.pfb\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/cmsy9.tfm\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/dumyhyph.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/loadhyph-as.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/hyph-quote-be.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/cmsy8.tfm\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/cmsy9.pfb\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/lmroman8-regular.otf\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/ctex-scheme-chinese-article.def\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/pgfcore.code.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/hyph-el-polyton.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/hyph-ru.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/cmbx7.tfm\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/article.cls\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/cmbx10.tfm\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/intcalc.sty\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/lmromanslant12-regular.otf\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/pgfcoregraphicstate.code.tex\n.question-bank-work/tectonic-cache/bundles/data/6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c/hyph-hy.tex\n/.question-bank-work/\n/.release-work/\n/remote-checkout/\n.DS_Store\n__pycache__/\n*.pyc\n*.log\n.env\n.env.*\n/references/\n"}}]

## tool · 2026-11-18T12:29:48Z


Script completed
Wall time 0.7 seconds
Output:

% !TeX program = xelatex
% 直接编译为 iPad 横屏。编译 A4 时，在读入本文件前定义 \QuestionBankAfour。
\documentclass[UTF8,zihao=-4,fontset=fandol]{ctexart}
\ifdefined\QuestionBankAfour
  \usepackage[a4paper,margin=17mm]{geometry}
\else
  \usepackage[paperwidth=800bp,paperheight=600bp,left=48bp,right=48bp,top=40bp,bottom=40bp]{geometry}
\fi
\usepackage{amsmath,amssymb,xcolor,fancyhdr}
\usepackage[hidelinks,bookmarksopen=true]{hyperref}
\xeCJKDeclareCharClass{CJK}{"2460 -> "2463}

\definecolor{examaccent}{HTML}{175C57}
\setlength{\parindent}{0pt}
\setlength{\parskip}{5bp}
\setlength{\headheight}{15bp}
\pagestyle{fancy}
\fancyhf{}
77:\Volume{行列式 A 卷}{det-a}
79:\Question{1}{单项选择题}{3}{1657}{**}
88:\Known 求排列 $217986354$ 的逆序数。逆序是前面的数大于后面的数的一对位置。
89:\Method 固定每对逆序的左端，从左到右数该数字右边比它小的数。每一对只会被数一次。
96:\Question{2}{单项选择题}{3}{1657}{**}
105:\Known 求给定四阶行列式的值。
106:\Method 第一列为 $2,4,6,8$，后三项都是首项的整倍数。把第一行的倍数分别减去，第一列就只剩一项。某行加上另一行的倍数，行列式不变。
114:\Question{3}{单项选择题}{3}{1657}{**}
130:\Known $B$ 的每一列都可以由 $A$ 的列得到。设 $A$ 的三列为 $u,v,w$，且 $|u,v,w|=n$。
131:\Method 先把第三列中重复出现的 $u$ 去掉，再还原列序。
139:\Question{4}{单项选择题}{3}{1657}{***}
148:\Known 比较四个 $n$ 阶行列式，找出恒等于 $-1$ 的一项。图中未写出的元素为零。
149:\Method 对只有一组非零乘积的行列式，行列式的符号就是该列号排列的符号。对前三项，找到一个阶数的反例即可排除恒等关系。
153:\Question{5}{单项选择题}{3}{1657}{**}
162:\Known 比较 $x=1$ 与题给行列式为零这两个条件。
163:\Method 充分性从 $x=1$ 出发检查行列式；必要性从行列式为零出发，检查是否只能取 $1$。
167:\Question{6}{填空题}{3}{1658}{**}
171:\Known 求三行 $( -2,1,-3)$、$(98,101,97)$、$(1,-3,4)$ 构成的行列式。
172:\Method 第二行每个数恰好比第一行对应数大 $100$，先相减，再沿常数行制造零。
180:\Question{7}{填空题}{3}{1658}{**}
184:\Known 四阶行列式的第一行全为 $1$，其余各行只有两个非零元。
185:\Method 按第一行展开。删去第一行和任意一列，剩下的三阶行列式都是三角形或分块三角形，可沿稀疏行逐个取元。
192:\Question{8}{填空题}{3}{1658}{**}
196:\Known 求由三位数构成的行列式。第二列是 $100,200,300$。
197:\Method 第一列接近第二列，第三列接近第二列的两倍。利用列加减把两列都化成小整数，再按含零列展开。
205:\Question{9}{填空题}{3}{1658}{***}
209:\Known 求题给五阶行列式。第四行只有第 $5$ 列的元素非零。
210:\Method 每个乘积必须从每行、每列各取一个元素。先由第四行确定第 $5$ 列，再排除其他行的第 $5$ 列。
217:\Question{10}{填空题}{3}{1658}{***}
221:\Known 求由 $x,y,x+y$ 循环排列成的三阶行列式。
222:\Method 令 $z=x+y$，先数清三阶行列式中各乘积的符号，再用立方和恒等式整理。
233:\Question{11}{解答题}{10}{1658}{**}
237:\Known 求使三阶行列式为零的 $\lambda$。
238:\Method 三个对角元素都等于 $\lambda-2$，先令 $t=\lambda-2$，按第一行展开。
249:\Question{12}{解答题}{10}{1658}{**}
253:\Known 求非零元素分布在奇数行列和偶数行列两个位置组上的四阶行列式。
254:\Method 同时把行、列排成 $(1,3,2,4)$，可把两个位置组分别聚集到左上和右下。
263:\Question{13}{解答题}{10}{1659}{***}
267:\Known 求第四行四个元素的余子式之和。余子式 $M_{4j}$ 是删去第四行和第 $j$ 列的行列式。
268:\Method 前三行的第三行只有第二列非零。对每个删列后的矩阵，沿该行展开。
279:\Question{14}{解答题}{10}{1659}{***}
283:\Known 求含 $x$ 的四阶行列式。每行以 $(1,-1,1,-1)$ 为基准，仅反对角线各多一个 $x$。
284:\Method 反转四列，令四个 $x$ 移到主对角线。此时适合按列的线性性展开。
288:\Question{15}{解答题}{10}{1659}{****}
302:\Known 右上角为 $a_0$，第一行和末列的其他元素均为 $1$。反对角线上的其余元素从 $a_1$ 到 $a_n$，均非零。
303:\Method 倒排后 $n$ 行，使 $a_i$ 落在左下的对角块。随后消去第一行的前 $n$ 个 $1$。
311:\Question{16}{解答题}{10}{1660}{***}
324:\Known 求各列由 $x_j$ 的一至三次多项式组成的四阶行列式。
325:\Method 最高次幂依次为 $0,1,2,3$。借助前两行消去后两行的低次项，再化成 Vandermonde 行列式。
336:\Question{17}{解答题}{10}{1660}{***}
350:\Known 求五阶三对角行列式。主对角线为 $1-x$，上、下相邻对角线分别为 $x,-1$。
351:\Method 令 $D_k$ 为同结构的 $k$ 阶行列式。首行只有两个可能非零的位置，按首行展开可降阶。
360:\Volume{行列式 B 卷}{det-b}
362:\Question{1}{单项选择题}{3}{1661}{**}
371:\Known 已知一个三阶行列式为 $m$，求换行、倍乘后的行列式。
372:\Method 右式每行由左式的一列得到。先转置左式，再比较各行。
379:\Question{2}{单项选择题}{3}{1661}{***}
388:\Known 求 $f'(x)=0$ 的根数。$f(x)$ 是四阶行列式，只有第四行含 $x$。
389:\Method 第四行前三项恰好是第二行前三项的 $x$ 倍。用第四行减 $x$ 倍第二行，再沿第四行展开。
397:\Question{3}{单项选择题}{3}{1661}{***}
406:\Known 四阶行列式只有主对角线及其相邻两条对角线上可能非零，要求其值。
407:\Method 记左上角 $k$ 阶行列式为 $D_k$。按末行展开，只有最后两个位置有贡献。
419:\Question{4}{单项选择题}{3}{1661}{***}
428:\Known 第二列元素是 $2,m,k,3$。给定的是第二列余子式和第四列代数余子式，要求 $m,k$。
429:\Method 把第二列余子式乘上位置符号，按第二列展开。再用第二列元素与第四列的代数余子式对应相乘，借助两列相同的行列式得到第二个方程。
436:\Question{5}{单项选择题}{3}{1661}{***}
445:\Known 求上三角行列式 $D_n$ 的所有代数余子式之和。首行全为 $1$。
446:\Method 记第 $i$ 行代数余子式之和为 $S_i$。把第 $i$ 行换成全 $1$，沿该行展开就是 $S_i$，因为删去该行后余子式不变。
453:\Question{6}{填空题}{3}{1662}{***}
457:\Known 求四阶行列式多项式中 $x^3$ 的系数。
458:\Method 每个行列式项由四行四列各取一个元素。要得到 $x^3$，必须取三个 $x$ 和一个常数。
462:\Question{7}{填空题}{3}{1662}{***}
466:\Known 主对角元素是 $2+x,2-x,2+y,2-y$，其余元素都为 $2$。
467:\Method 按列把矩阵写成对角阵加全 $2$ 矩阵。行列式对列具有线性性，两列取同一个常数列时该项为零。
474:\Question{8}{填空题}{3}{1662}{**}
478:\Known 求第一行的两个代数余子式之差 $A_{11}-A_{12}$。
479:\Method 原第一行正是 $(1,-1,0,0)$，按这行展开直接得到所求差值。
489:\Question{9}{填空题}{3}{1662}{***}
493:\Known 主对角线为 $b$，上邻对角线和左下角为 $a$，求 $n$ 阶行列式。
494:\Method 从第一行取 $b$ 或 $a$。只要某行选了右边的 $a$，下一行的对角列就被占用，会迫使余下行也沿相同方向取 $a$。
501:\Question{10}{填空题}{3}{1662}{**}
505:\Known 三行分别是各变量的一次幂、平方，以及另外两个变量的和。
506:\Method 第三行加第一行后各列都是 $a+b+c$，可提出该公共因子。
515:\Question{11}{解答题}{10}{1662}{***}
519:\Known 求四阶行列式，四行按 $0,a,b,a$ 的循环结构排列。
520:\Method 选取四个能体现成对加减的列向量，使矩阵作用在每个向量上时只乘一个数，再利用乘积的行列式。
528:\Question{12}{解答题}{10}{1663}{****}
543:\Known 求三对角行列式 $D_n$，对角元为 $a$，上、下邻对角元为 $b,c$，且 $a^2-4bc\ge0$。
544:\Method 沿末行展开得二阶递推，再按特征方程的判别式区分两根是否相同。
560:\Question{13}{解答题}{10}{1663}{*****}
573:\Known 原题第三行第三列印为 $a_3b_3^3$。其余三列第三行的 $b_i$ 指数为 $2$。按原题的指数计算，且各 $a_i\ne0$。
574:\Method 每列提出 $a_i^3$，令 $t_i=\frac{b_i}{a_i}$。原式与四阶 Vandermonde 行列式仅有一个元素不同，利用行列式对该元素的线性性计算差值。
586:\Question{14}{解答题}{10}{1663}{***}
600:\Known 求主对角为 $a$、其他元素为 $b$ 的 $n$ 阶行列式。
601:\Method 每行的和相同，可以用列相加得到常数列，再用第一行把其他行简化。
608:\Question{15}{解答题}{10}{1664}{***}
622:\Known 求主对角为 $x-b$、其他元素为 $b$ 的 $n$ 阶行列式。
623:\Method 各行和均相同。把第一列改为所有列的和，可分离一个线性因子。
627:\Question{16}{解答题}{10}{1664}{***}
644:\Known $n>2$。第一行与第一列除首元 $0$ 外全为 $1$，右下块对角为 $0$，其他元素为 $x$。
645:\Method 后续各行都含同样的 $x$，用第一行消去右下块的非对角元。
649:\Question{17}{解答题}{10}{1664}{***}
663:\Known 主对角依次为 $1,2,\ldots,n$，其余元素全为 $2$。图中第二行全为 $2$。
664:\Method 用第二行消去其他行的非对角元，再按第二列展开。
671:\Volume{矩阵及其运算 A 卷}{mat-a}
673:\Question{1}{单项选择题}{3}{1665}{***}
682:\Known $A$ 的三列是 $\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3$，需要比较各选项与 $|A|$ 的关系。
683:\Method 用行列式的列线性性和交替性。出现重复列的项为零，每交换两列一次则变号。
687:\Question{2}{单项选择题}{3}{1665}{**}
696:\Known $A,B$ 为同阶方阵，$E$ 为同阶单位矩阵，找出错误命题。
697:\Method 展开矩阵乘法时保持因子顺序。只有互相可交换的因子才能像数一样合并。
701:\Question{3}{单项选择题}{3}{1665}{***}
710:\Known $A^*$ 是 $A$ 的伴随矩阵。内层 $|A^*|$ 是标量，外层取矩阵 $|A^*|A$ 的行列式。
711:\Method 用 $AA^*=|A|E$ 求 $|A^*|$，再利用标量乘 $n$ 阶矩阵时，行列式的每一列都带一个标量因子。
718:\Question{4}{单项选择题}{3}{1665}{**}
727:\Known 已知 $A$ 正交，即 $A^{\mathrm T}A=AA^{\mathrm T}=E$。找出不正交的矩阵。
728:\Method 对每一项检验其转置与自身的乘积。伴随矩阵可用 $A^*=|A|A^{-1}$，因为正交矩阵已有逆 $A^{\mathrm T}$。
732:\Question{5}{单项选择题}{3}{1665}{***}
741:\Known $A,B$ 都是可逆矩阵。辨别哪一等式对所有满足条件的 $A,B$ 成立。
742:\Method 对伴随矩阵使用 $M^*=|M|M^{-1}$，并注意乘积求逆时因子倒序。其他项用符合条件的反例排除。
750:\Question{6}{填空题}{3}{1665}{**}
754:\Known $A=P^{-1}BP$，要求 $A^4-2B^2$。题设的 $P^{-1}$ 表示 $P$ 可逆。
755:\Method 相邻的 $P$ 与 $P^{-1}$ 在矩阵幂里相消。先计算结构简单的 $B^2$ 和 $B^4$。
763:\Question{7}{填空题}{3}{1665}{*}
767:\Known $A$ 为三阶方阵且 $|A|=4$，求 $|2A^2|$。
768:\Method 将标量因子与矩阵乘积分别处理。三阶矩阵有三列，提出 $2$ 会出现因子 $2^3$。
775:\Question{8}{填空题}{3}{1665}{**}
779:\Known 求矩阵平方差等式 $A^2-B^2=(A+B)(A-B)$ 成立的充分必要条件。
780:\Method 展开右边并保留因子顺序，判断额外两项何时相消。
784:\Question{9}{填空题}{3}{1665}{**}
788:\Known 求给定下三角矩阵 $A$ 减去 $2E$ 后的逆。
789:\Method 减去 $2E$ 只改变对角元。左上 $2$ 阶块和右下 $1$ 阶块互不影响，可逐块解方程。
796:\Question{10}{填空题}{3}{1666}{***}
800:\Known 求 $A^{-1}$、$(A^*)^{-1}$ 和 $[(-2A)^*]^{-1}$。
801:\Method 先求行列式和伴随矩阵。三阶矩阵的伴随矩阵由二阶代数余子式转置组成，整矩阵倍乘 $-2$ 时每个二阶余子式乘 $4$。
809:\Question{11}{解答题}{10}{1666}{***}
813:\Known 已知 $AB+B+A+2E=O$，求 $|B+E|$。
814:\Method 方程含 $AB,B,A$，可配出保持因子顺序的 $(A+E)(B+E)$，再对等式取行列式。
822:\Question{12}{解答题}{10}{1666}{**}
826:\Known 解三元一次方程组 $A\boldsymbol{x}=\boldsymbol{\beta}$。
827:\Method 写出三行方程，观察每行 $x_1$ 的系数都为 $1$，两两相减先消去 $x_1$。
831:\Question{13}{解答题}{10}{1667}{***}
839:\Known 求 $A^n$ 和 $(A+2E)^n$。$A$ 的三列完全相同，每列各元素之和为零。
840:\Method 把 $A$ 写成列向量与行向量的乘积，以便看出二次幂。$2E$ 与 $A$ 可交换，可使用二项式展开。
851:\Question{14}{解答题}{10}{1667}{***}
855:\Known $A$ 的三个对角元均为 $\lambda$，紧挨主对角线上方的两个元素为 $1$。
856:\Method 拆成 $\lambda E+N$，其中 $N$ 只有上邻对角线为 $1$。计算 $N$ 的幂，再用可交换矩阵的二项式展开。
869:\Question{15}{解答题}{10}{1667}{***}
873:\Known $A^2-A-5E=O$，求 $(A-3E)^{-1}$。
874:\Method 试用一次矩阵多项式作逆矩阵，因为乘积的二次项可以用已知关系消去。
882:\Question{16}{解答题}{10}{1668}{***}
886:\Known 求四阶矩阵 $A$ 的行列式和逆。按前两行和后两行、前两列和后两列分块，$A=\begin{pmatrix}O&B\\C&O\end{pmatrix}$。
887:\Method 互换两组列可将 $B,C$ 移到主对角块。对于求逆，可以选同样的反对角结构，使乘积的对角块分别为单位矩阵。
896:\Question{17}{解答题}{10}{1668}{**}
900:\Known 给定二阶矩阵 $A$，求 $A^*$ 以及再取一次伴随矩阵的结果。
901:\Method 按定义，先给每个余子式乘上位置符号，再转置。二阶余子式只由一个元素组成。
909:\Volume{矩阵及其运算 B 卷}{mat-b}
911:\Question{1}{单项选择题}{3}{1669}{**}
925:\Known 已知两个四阶行列式，求前三列顺序改变且末列为 $\boldsymbol{\beta}_1+\boldsymbol{\beta}_2$ 的行列式。
926:\Method 按末列的线性性分开，再比较各自的列序。一次列交换使行列式变号。
930:\Question{2}{单项选择题}{3}{1669}{***}
939:\Known 分块矩阵 $M=\begin{pmatrix}O&A\\B&O\end{pmatrix}$，其中 $A,B$ 是二阶矩阵，行列式分别为 $2,3$。求 $M^*$。
940:\Method 两块均可逆。先通过换列得到 $|M|$，再用分块乘法求 $M^{-1}$。
949:\Question{3}{单项选择题}{3}{1669}{**}
958:\Known $A$ 可逆。比较它与 $A^{-1}$、$A^{\mathrm T}$、$A^*$、$E$ 的平方展开，找出不一定成立的等式。
959:\Method 对任意同阶的 $U,V$，$(U+V)^2=U^2+UV+VU+V^2$。用 $2UV$ 代替中间两项的条件是 $UV=VU$。
967:\Question{4}{单项选择题}{3}{1669}{**}
976:\Known 同阶方阵满足 $AB=BC=CA=E$，求 $A^2+B^2+C^2$。
977:\Method 每个乘积等于单位阵，说明相关因子互为逆。逐个消去 $B,C$。
981:\Question{5}{单项选择题}{3}{1669}{***}
1000:\Known $A,B$ 为同阶方阵且 $AB=A+B$，判断四个命题。
1001:\Method 原式含乘积和两个一次项，可以补上一个 $E$ 配成乘积。同时利用方阵乘积可逆当且仅当两因子均可逆。
1005:\Question{6}{填空题}{3}{1669}{***}
1009:\Known $A$ 为奇数阶，$AA^{\mathrm T}=A^{\mathrm T}A=E$ 且 $|A|>0$。求 $|A-E|$。
1010:\Method 先确定 $|A|$。将 $A-E$ 分解为 $A(E-A^{-1})$，利用 $A^{-1}=A^{\mathrm T}$，把行列式换成 $|E-A|$。
1018:\Question{7}{填空题}{3}{1670}{**}
1022:\Known $n\ge2$ 为整数，要求 $A^n-2A^{n-1}$。
1023:\Method 矩阵第一、三行相同，第二行只有一个非零元，先计算 $A^2$。
1030:\Question{8}{填空题}{3}{1670}{**}
1034:\Known $A=\boldsymbol{\alpha}^{\mathrm T}\boldsymbol{\beta}$，其中 $\boldsymbol{\alpha},\boldsymbol{\beta}$ 都是三维行向量。求 $A^n$。
1035:\Method 相邻两个 $A$ 相乘时，中间出现 $1\times1$ 的乘积 $\boldsymbol{\beta}\boldsymbol{\alpha}^{\mathrm T}$，可把它当作标量。
1043:\Question{9}{填空题}{3}{1670}{**}
1047:\Known $A$ 为下三角矩阵。求乘积 $(2E-A)^{\mathrm T}(4E-A^2)$ 的行列式。
1048:\Method 先拆成两个因子的行列式。转置不改行列式，下三角矩阵的行列式只需看对角元。
1052:\Question{10}{填空题}{3}{1670}{**}
1056:\Known 给定四阶矩阵的左上和右下各有一个二阶块，另外两块为零。求 $A^{-1}$。
1057:\Method 把两个二阶块各自求逆。分块相乘时这两个块独立，只要两块都可逆即可。
1069:\Question{11}{解答题}{10}{1670}{***}
1073:\Known 计算 $A^2(BA)^*\cdot(AB^{-1})^{-1}$。需要保留每个因子的顺序。
1074:\Method 用伴随矩阵与逆矩阵的关系，把两部分都写成易于逐次约去的乘积。
1082:\Question{12}{解答题}{10}{1670}{***}
1086:\Known $ABA^*=E-BA^{-1}$，求 $|B|$。矩阵 $A$ 的左上二阶块行列式为 $1$，右下元为 $2$。
1087:\Method 等式右乘 $A$，其中 $A^*A=|A|E$，而 $A^{-1}A=E$，这样可把 $B$ 提到共同的右侧。
1096:\Question{13}{解答题}{10}{1671}{***}
1100:\Known $B=(E+A)^{-1}(E-A)$，求 $(E+B)^{-1}$。$A$ 是下三角矩阵。
1101:\Method 把 $E$ 写成 $(E+A)^{-1}(E+A)$，与 $B$ 合并。
1113:\Question{14}{解答题}{10}{1671}{****}
1131:\Known $A$ 为 $m\times n$，$B$ 为 $n\times m$，$E_m+AB$ 可逆。先证逆矩阵恒等式，再求给定的 $W^{-1}$。
1132:\Method （1）用直接相乘检验候选逆矩阵。（2）把 $W-E_3$ 写成列向量乘行向量，使题给的三项和恰好出现。
1150:\Question{15}{解答题}{10}{1671}{***}
1161:\Known $AP=PB$，其中 $B=\operatorname{diag}(1,0,-1)$。求 $A$ 与 $A^5$。
1162:\Method $P$ 为下三角且对角元 $1,-1,1$ 均非零，所以 $A=PBP^{-1}$，矩阵幂可通过对角阵计算。求 $A$ 的各列时可直接利用 $AP=PB$。
1170:\Question{16}{解答题}{10}{1672}{****}
1181:\Known 由 $(2E-C^{-1}B)A^{\mathrm T}=C^{-1}$ 求 $A$。$C$ 为对角元全为 $1$ 的上三角矩阵。
1182:\Method 从左乘 $C$ 消去 $C^{-1}$，将问题变成求一个上三角矩阵的逆，最后转置。
1195:\Question{17}{解答题}{10}{1672}{**}
1199:\Known 求与 $A=\begin{pmatrix}1&1\\0&1\end{pmatrix}$ 可交换的所有矩阵 $X$。两种乘积都要有定义，所以 $X$ 为二阶方阵。
1200:\Method 设四个元素为未知量，把 $AX$ 与 $XA$ 展开，逐个比较对应位置。
import re
from pathlib import Path

import pymupdf


base = Path("references/同济线代/同步测试卷")
work = Path(__file__).parent
title = "同济线性代数同步测试卷"
tex = (base / f"{title}.tex").read_text()
markdown = [(base / file).read_text() for file in ("行列式同步测试.md", "矩阵及其运算同步测试.md")]
source_volumes = [volume for doc in markdown for volume in re.split(r"^## [AB] 卷$", doc, flags=re.M)[1:]]
volume_names = ["行列式 A 卷", "行列式 B 卷", "矩阵及其运算 A 卷", "矩阵及其运算 B 卷"]
tex_volumes = re.split(r"^\\Volume\{([^{}]+)\}\{[a-z-]+\}\s*\n", tex, flags=re.M)[1:]
answer_letters = ["CDDDB", "BCCAB", "CADDD", "DBBAD"]
assert len(source_volumes) == 4
assert tex_volumes[::2] == volume_names
assert tex.count(r"\begin{document}") == tex.count(r"\end{document}") == 1
assert not re.search(r"\\(?:input|include|includegraphics)\{", tex)
assert not re.search(r"\\(?:tfrac|dfrac)\b|\\frac[^{]", tex)


def compact(s):
    return re.sub(r"\s+", "", s)


metadata = []
for v, md in enumerate(source_volumes):
    body = tex_volumes[2 * v + 1]
    photos = [(int(start), int(end), img) for start, end, img in re.findall(
        r"^原图：\[第 (\d+)–(\d+) 题\]\([^)]*(IMG_\d+)\.HEIC\)$", md, re.M
    )]
    md = re.sub(r"^(?:### |原图：|> 校对注：).*$", "", md, flags=re.M)
    md_questions = re.split(r"^#### (\d+)\.$", md, flags=re.M)[1:]
    tex_questions = re.split(
        r"^\\Question\{(\d+)\}\{([^{}]+)\}\{(\d+)\}\{(\d+)\}\{(\*{1,5})\}$", body, flags=re.M
    )[1:]
    assert len(md_questions) == 34 and len(tex_questions) == 102
    assert sum(map(int, tex_questions[2::6])) == 100
    for q in range(1, 18):
        number, category, points, photo, stars, item = tex_questions[(q - 1) * 6:q * 6]
        md_number, original = md_questions[(q - 1) * 2:q * 2]
        img = f"IMG_{photo}"
        assert number == md_number == str(q)
        assert img in [p for a, b, p in photos if a <= q <= b]
        assert (category, points) == (
            ("单项选择题", "3") if q < 6 else ("填空题", "3") if q < 11 else ("解答题", "10")
        )
        question, solution = item.split("\n\\Solution\n")
        original_options = re.findall(r"^- （[A-D]）(.+)$", original, re.M)
        original_question = re.split(r"^- （A）", original, maxsplit=1, flags=re.M)[0]
        assembled = question.split("\n\\Choices\n")
        expected_question = original_question.replace("________", r"\blank{}")
        actual_question = assembled[0].replace(r"\[", "$$").replace(r"\]", "$$")
        if v == 3 and q == 1:
            actual_question = actual_question.replace("$$", "$").replace(r",\qquad", "$，$")
            actual_question = actual_question.replace(",\n$", "$，")
        assert compact(actual_question) == compact(expected_question), (v, q)
        if q < 6:
            assert assembled[1].strip().splitlines() == [
                ("  " if i else "") + "{" + option + "}" for i, option in enumerate(original_options)
            ]
            [letter] = re.findall(r"选 \\textbf\{([A-D])\}", solution)
            assert letter == answer_letters[v][q - 1]
        else:
            assert len(assembled) == 1 and not original_options
        assert re.findall(r"^\\(Known|Method|Derive|Verify)\b", solution, re.M) == [
            "Known", "Method", "Derive", "Verify"
        ]
        metadata.append((volume_names[v], q, category, points, img, stars))


def check_pdf(pdf, log, width, height):
    log_text = log.read_text()
    assert not re.search(r"Overfull|Missing character|Warning:|^!", log_text, re.M), log
    with pymupdf.open(pdf) as doc:
        assert len(doc) == 137
        assert all(abs(p.rect.width - width) < 0.2 and abs(p.rect.height - height) < 0.2 for p in doc)
        expected_bookmarks = [[1, title, 1]]
        spaces = []
        for i, (volume, q, category, points, photo, stars) in enumerate(metadata):
            question, solution = doc[1 + i * 2], doc[2 + i * 2]
            if q == 1:
                expected_bookmarks.append([2, volume, question.number + 1])
            expected_bookmarks.append([3, f"第 {q} 题", question.number + 1])
            question_text = compact(question.get_text(sort=True))
            solution_text = compact(solution.get_text())
            assert question_text.startswith(f"{category}{points}分第{q}题")
            assert f"{compact(volume)}{photo}{stars}" in question_text
            assert "题解析" not in question_text
            assert solution_text.startswith(f"第{q}题解析已知与目标")
            assert all(label in solution_text for label in ("入手思路", "推导", "结论与检查"))
            if q <= 5:
                assert all(f"({letter})" in question_text for letter in "ABCD")
            if volume == "矩阵及其运算 B 卷" and q == 5:
                assert all(mark in question_text and mark in solution_text for mark in "①②③④")
            lines = [
                line["spans"] for block in question.get_text("dict")["blocks"] if block["type"] == 0
                for line in block["lines"]
            ]
            q_spans = [span for line in lines for span in line]
            [num_line] = [
                line for line in lines if compact("".join(s["text"] for s in line)) == f"第{q}题"
            ]
            num_span = num_line[0]
            [photo_span] = [s for s in q_spans if photo in s["text"]]
            [star_span] = [s for s in q_spans if s["text"].strip() == stars]
            assert abs(num_span["origin"][1] - photo_span["origin"][1]) < 0.5
            assert abs(num_span["origin"][1] - star_span["origin"][1]) < 0.5
            assert num_span["origin"][0] < photo_span["origin"][0] < star_span["origin"][0]
            footer_top = min(s["bbox"][1] for s in q_spans if s["bbox"][1] > height - 55)
            body_bottom = max(s["bbox"][3] for s in q_spans if s["bbox"][1] < footer_top - 0.5)
            spaces.append(footer_top - body_bottom)
        assert doc.get_toc() == expected_bookmarks
        for page in doc:
            for x0, y0, x1, y1, *_ in page.get_text("blocks"):
                assert x0 >= 0 and y0 >= 0 and x1 <= page.rect.width and y1 <= page.rect.height, page.number
        assert min(spaces) >= 160
        print(f"{pdf.name} {width}×{height} bp, {len(doc)} pages, "
              f"{len(expected_bookmarks)} bookmarks, minimum writing space {min(spaces):.1f} bp")


print("Source comparison passed: 68 question bodies and solutions, 80 choices, four 100-point volumes.")
check_pdf(work / "a4/texput.pdf", work / "a4/texput.log", 595.28, 841.89)
check_pdf(work / f"ipad/{title}.pdf", work / f"ipad/{title}.log", 800, 600)
references/同济线代/同步测试卷/A4:
total 696
-rw-r--r--  1 oyamahappa  staff  353748 Nov 18 20:21 同济线性代数同步测试卷（A4）.pdf

references/同济线代/同步测试卷/iPad:
total 688
-rw-r--r--  1 oyamahappa  staff  349191 Nov 18 20:21 同济线性代数同步测试卷.pdf
/Applications/ChatGPT.app/Contents/Resources/tectonic/tectonic
/usr/bin/python3


## tool · 2026-11-18T12:30:10Z


Script completed
Wall time 0.8 seconds
Output:

{}
{"chunk_id":"20d0fe","wall_time_seconds":0.473428292,"exit_code":0,"original_token_count":1713,"output":"\\Question{13}{解答题}{10}{1659}{***}\n设 $|A|=\\begin{vmatrix}3&0&4&0\\\\2&2&2&2\\\\0&-7&0&0\\\\5&3&-2&2\\end{vmatrix}$，求该行列式第四行元素的余子式之和。\n\n\\Solution\n\\Known 求第四行四个元素的余子式之和。余子式 $M_{4j}$ 是删去第四行和第 $j$ 列的行列式。\n\\Method 前三行的第三行只有第二列非零。对每个删列后的矩阵，沿该行展开。\n\\Derive 删去第二列时第三行全为零，所以 $M_{42}=0$。删去第一列时 $-7$ 处在第 $(3,1)$ 位；删去第三、四列时它都处在第 $(3,2)$ 位。因此\n\\[\n\\begin{aligned}\nM_{41}&=-7(4\\cdot2-0\\cdot2)=-56,\\\\\nM_{43}&=7(3\\cdot2-0\\cdot2)=42,\\quad\nM_{44}=7(3\\cdot2-4\\cdot2)=-14.\n\\end{aligned}\n\\]\n\\Verify 和为 $\\boxed{-28}$。相加时使用 $M_{4j}$ 本身，展开三阶行列式时的符号已经计入各个值。\n\n\\Question{14}{解答题}{10}{1659}{***}\n计算 4 阶行列式 $\\begin{vmatrix}1&-1&1&x-1\\\\1&-1&x+1&-1\\\\1&x-1&1&-1\\\\x+1&-1&1&-1\\end{vmatrix}$。\n\n\\Solution\n\\Known 求含 $x$ 的四阶行列式。每行以 $(1,-1,1,-1)$ 为基准，仅反对角线各多一个 $x$。\n\\Method 反转四列，令四个 $x$ 移到主对角线。此时适合按列的线性性展开。\n\\Derive 反序排列有六个逆序，所以反转四列保持符号。令 $\\boldsymbol{1}=(1,1,1,1)^{\\mathrm T}$，反转后第 $j$ 列是 $x e_j+v_j\\boldsymbol{1}$，其中 $v=(-1,1,-1,1)$，$e_j$ 是单位阵第 $j$ 列。同时选中两列 $v_j\\boldsymbol{1}$ 时，两列成比例，项为零。全选 $xe_j$ 得 $x^4$；只在第 $j$ 列选 $v_j\\boldsymbol{1}$ 得 $x^3v_j$，因为 $\\boldsymbol{1}$ 的第 $j$ 个分量是 $1$，展开后其他分量会与已有列重复。\n\\Verify $D=x^4+x^3(-1+1-1+1)=\\boxed{x^4}$。令 $x=0$ 时原矩阵各行相同，行列式为零。\n\n\\Question{15}{解答题}{10}{1659}{****}\n计算 $n+1$ 阶行列式\n\n\\[\nD_{n+1}=\\begin{vmatrix}\n1&1&1&\\cdots&a_0\\\\\n&&&\\mathinner{\\raisebox{-0.15em}{·}\\mkern1mu\\raisebox{0.05em}{·}\\mkern1mu\\raisebox{0.25em}{·}}&\\vdots\\\\\n&&a_{n-2}&&1\\\\\n&a_{n-1}&&&1\\\\\na_n&&&&1\n\\end{vmatrix}\\qquad(a_i\\ne0,\\ i=1,2,3,\\ldots,n).\n\\]\n\n\\Solution\n\\Known 右上角为 $a_0$，第一行和末列的其他元素均为 $1$。反对角线上的其余元素从 $a_1$ 到 $a_n$，均非零。\n\\Method 倒排后 $n$ 行，使 $a_i$ 落在左下的对角块。随后消去第一行的前 $n$ 个 $1$。\n\\Derive 倒排 $n$ 行的逆序数为 $\\frac{n(n-1)}{2}$。倒排后的第 $2$ 至 $n+1$ 行，前 $n$ 列构成对角阵 $\\operatorname{diag}(a_n,\\ldots,a_1)$。第一行从这些行分别减去对应的 $\\frac{1}{a_i}$ 倍，最后一项变成 $a_0-\\sum_{i=1}^n\\frac{1}{a_i}$。按第一行末项展开的符号是 $(-1)^n$。合并两次符号得\n\\[\nD_{n+1}=(-1)^{\\frac{n(n+1)}{2}}\\,a_1a_2\\cdots a_n\n\\left(a_0-\\sum_{i=1}^n\\frac{1}{a_i}\\right).\n\\]\n\\Verify 取 $n=2$ 检验，三阶原式可直接展开为 $a_1+a_2-a_0a_1a_2$，与公式一致。\n\n\\Question{16}{解答题}{10}{1660}{***}\n计算 4 阶行列式\n\n\\[\nD_4=\\begin{vmatrix}\n1&1&1&1\\\\\nx_1&x_2&x_3&x_4\\\\\n2x_1^2-1&2x_2^2-1&2x_3^2-1&2x_4^2-1\\\\\n4x_1^3-3x_1&4x_2^3-3x_2&4x_3^3-3x_3&4x_4^3-3x_4\n\\end{vmatrix}.\n\\]\n\n\\Solution\n\\Known 求各列由 $x_j$ 的一至三次多项式组成的四阶行列式。\n\\Method 最高次幂依次为 $0,1,2,3$。借助前两行消去后两行的低次项，再化成 Vandermonde 行列式。\n\\Derive 第三行加第一行，第四行加第二行的 $3$ 倍，分别从第三、四行提出 $2$ 和 $4$，得\n\\[\nD_4=8\\begin{vmatrix}\n1&1&1&1\\\\x_1&x_2&x_3&x_4\\\\x_1^2&x_2^2&x_3^2&x_4^2\\\\x_1^3&x_2^3&x_3^3&x_4^3\n\\end{vmatrix}\n=8\\prod_{1\\le i<j\\le4}(x_j-x_i).\n\\]\n这里各列是一组同一个数的递增幂，正好满足 Vandermonde 公式的排列顺序。\n\\Verify 任意两个 $x_i$ 相等时产生两列相同，右式也有相应的零因子。系数 $8$ 是提出的两个行因子的乘积。\n\n\\Question{17}{解答题}{10}{1660}{***}\n计算 5 阶行列式\n\n\\[\nD_5=\\begin{vmatrix}\n1-x&x&0&0&0\\\\\n-1&1-x&x&0&0\\\\\n0&-1&1-x&x&0\\\\\n0&0&-1&1-x&x\\\\\n0&0&0&-1&1-x\n\\end{vmatrix}.\n\\]\n\n\\Solution\n\\Known 求五阶三对角行列式。主对角线为 $1-x$，上、下相邻对角线分别为 $x,-1$。\n\\Method 令 $D_k$ 为同结构的 $k$ 阶行列式。首行只有两个可能非零的位置，按首行展开可降阶。\n\\Derive $D_0=1$，$D_1=1-x$。当 $k\\ge2$，首列项给 $(1-x)D_{k-1}$；第二列项的余子式沿首列展开只取 $-1$，再计位置 $(1,2)$ 的负号，给 $xD_{k-2}$。所以\n\\[\nD_k=(1-x)D_{k-1}+xD_{k-2},\\qquad\nD_k-D_{k-1}=-x(D_{k-1}-D_{k-2}).\n\\]\n从 $D_1-D_0=-x$ 出发，逐项相加得 $D_5=1-x+x^2-x^3+x^4-x^5$。\n\\Verify 在 $x=0$ 时原式是下三角行列式，值为 $1$；所得多项式也为 $1$。\n\n.question-bank-work/proof-venv/pyvenv.cfg\nTraceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nModuleNotFoundError: No module named 'numpy'\nzsh:1: no matches found: /opt/homebrew/bin/python*\nProcess a (La)TeX document\n\nUsage: tectonic [OPTIONS] <INPUT>\n\nArguments:\n  <INPUT>  The file to process, or \"-\" to process the standard input stream\n\nOptions:\n  -X                                Use experimental V2 interface (see `tectonic -X --help`)\n  -c, --chatter <CHATTER_LEVEL>     How much chatter to print when running [default: default]\n      --color <CLI_COLOR>           Enable/disable colorful log output [default: auto] [possible values: always, auto, never]\n  -f, --format <path>               The name of the \"format\" file used to initialize the TeX engine [default: latex]\n  -b, --bundle <BUNDLE>             Use this URL or path to find resource files instead of the default\n  -C, --only-cached                 Use only resource files cached locally\n      --outfmt <format>             The kind of output to generate [default: pdf]\n      --makefile-rules <dest_path>  Write Makefile-format rules expressing the dependencies of this run to <dest_path>\n      --pass <PASS>                 Which engines to run [default: default]\n  -r, --reruns <count>              Rerun the TeX engine exactly this many times after the first\n  -k, --keep-intermediates          Keep the intermediate files generated during processing\n      --keep-logs                   Keep the log files generated during processing\n      --synctex                     Generate SyncTeX data\n      --hide <hide_path>            Tell the engine that no file at <hide_path> exists, if it tries to read it\n  -p, --print                       Print the engine's chatter during processing\n  -o, --outdir <outdir>             The directory in which to place output files [default: the directory containing <input>]\n      --untrusted                   Input is untrusted -- disable all known-insecure features\n  -Z <option>                       Unstable options. Pass -Zhelp to show a list\n  -h, --help                        Print help\n  -V, --version                     Print version\n"}

## tool · 2026-11-18T12:31:38Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:31:42Z


Script completed
Wall time 0.1 seconds
Output:

D_k-D_{k-1}=-x(D_{k-1}-D_{k-2}).
\]
\par 下一步先算 $D_2-D_1$，它与 $D_1-D_0$ 相差什么因子？第二条等式说明每一步都乘 $-x$。从 $D_1-D_0=-x$ 出发，逐项相加得 $D_5=1-x+x^2-x^3+x^4-x^5$。
\Verify 在 $x=0$ 时原式是下三角行列式，值为 $1$；所得多项式也为 $1$。

\Volume{行列式 B 卷}{det-b}

\Question{1}{单项选择题}{3}{1661}{**}
设 $\begin{vmatrix}a_1&a_2&a_3\\b_1&b_2&b_3\\c_1&c_2&c_3\end{vmatrix}=m$，则 $\begin{vmatrix}a_2&b_2&c_2\\3a_1&3b_1&3c_1\\a_3-2a_1&b_3-2b_1&c_3-2c_1\end{vmatrix}=$（　　）。
\Choices
  {$-2m$}
  {$-3m$}
  {$m$}
  {$6m$}

\Solution
\Known 已知一个三阶行列式为 $m$，求换行、倍乘后的行列式。
\Method 右式每行由左式的一列得到。先转置左式，再比较各行。
\Derive 记转置后的三行为 $r_1,r_2,r_3$，转置保持行列式为 $m$。右式的行依次为 $r_2,3r_1,r_3-2r_1$。提出第二行的 $3$，第三行加第二行的 $2$ 倍，再交换前两行还原。
\[
D=3|r_2;r_1;r_3|=-3m.
\]
\Verify 选 \textbf{B}。用左式为单位行列式核对，所得为 $-3$，排除其余选项。

\Question{2}{单项选择题}{3}{1661}{***}
设 $f(x)=\begin{vmatrix}5&7&3&2\\1&2&-1&1\\4&6&3&7\\x&2x&-x&\frac{1}{3}x^3-3x\end{vmatrix}$，则 $f'(x)=0$ 的根的个数为（　　）。
\Choices
  {$0$}
  {$1$}
  {$2$}
  {$3$}

\Solution
\Known 求 $f'(x)=0$ 的根数。$f(x)$ 是四阶行列式，只有第四行含 $x$。
\Method 第四行前三项恰好是第二行前三项的 $x$ 倍。用第四行减 $x$ 倍第二行，再沿第四行展开。
\Derive 变换后第四行只剩末项 $\frac{1}{3}x^3-4x$。该位置的余子式是
\[
\begin{vmatrix}5&7&3\\1&2&-1\\4&6&3\end{vmatrix}=60-49-6=5.
\]
所以 $f(x)=5(\frac{1}{3}x^3-4x)$，从而 $f'(x)=5(x^2-4)$。
\Verify 根为 $-2,2$，选 \textbf{C}。非零二次项系数保证没有额外根，排除根数为 $0,1,3$ 的选项。

\Question{3}{单项选择题}{3}{1661}{***}
4 阶行列式 $\begin{vmatrix}1&a&0&0\\-1&2-a&a&0\\0&-2&3-a&a\\0&0&-3&4-a\end{vmatrix}=$（　　）。
\Choices
  {$22$}
  {$23$}
  {$24$}
  {$25$}

\Solution
\Known 四阶行列式只有主对角线及其相邻两条对角线上可能非零，要求其值。
\Method 记左上角 $k$ 阶行列式为 $D_k$。按末行展开，只有最后两个位置有贡献。
\Derive $D_1=1,D_0=1$。第 $k$ 行末元为 $k-a$，次末元为 $-(k-1)$。次末元的余子式沿末列再展开会多取因子 $a$，加上它所在位置的负号得
\[
D_k=(k-a)D_{k-1}+(k-1)aD_{k-2}\quad(2\le k\le4).
\]
依次代入，
\[
D_2=2-a+a=2,\quad D_3=2(3-a)+2a=6,\quad
D_4=6(4-a)+6a=24.
\]
\Verify 选 \textbf{C}。$a=0$ 时原式成为下三角行列式，主对角线乘积同为 $24$，也排除其余常数。

\Question{4}{单项选择题}{3}{1661}{***}
设 4 阶行列式的第二列元素依次为 $2,m,k,3$，第二列元素的余子式依次为 $1,-1,1,-1$，第四列元素的代数余子式依次为 $3,1,4,2$，且行列式的值为 $1$，则 $m,k$ 的取值为（　　）。
\Choices
  {$m=-4,k=-2$}
  {$m=4,k=-2$}
  {$m=-\frac{12}{5},k=-\frac{12}{5}$}
  {$m=\frac{12}{5},k=\frac{12}{5}$}

\Solution
\Known 第二列元素是 $2,m,k,3$。给定的是第二列余子式和第四列代数余子式，要求 $m,k$。
\Method 把第二列余子式乘上位置符号，按第二列展开。再用第二列元素与第四列的代数余子式对应相乘，借助两列相同的行列式得到第二个方程。
\Derive 第二列符号依次为 $-,+,-,+$，所以其四个代数余子式均为 $-1$。由行列式值为 $1$，有 $-2-m-k-3=1$。把第四列换成第二列会出现两列相同，按第四列展开得 $2\cdot3+m+4k+3\cdot2=0$。因此
\[
m+k=-6,\qquad m+4k=-12,\qquad k=-2,\quad m=-4.
\]
\Verify 选 \textbf{A}。回代两式都成立，方程相减后唯一确定 $k$，故排除另外三组。

\Question{5}{单项选择题}{3}{1661}{***}
设 $D_n=\begin{vmatrix}1&1&\cdots&1\\0&2&\cdots&2\\\vdots&\vdots&&\vdots\\0&0&\cdots&n\end{vmatrix}$，则 $D_n$ 中所有元素的代数余子式之和为（　　）。
\Choices
  {$0$}
  {$n!$}
  {$-n!$}
  {$2n!$}

\Solution
\Known 求上三角行列式 $D_n$ 的所有代数余子式之和。首行全为 $1$。
\Method 记第 $i$ 行代数余子式之和为 $S_i$。把第 $i$ 行换成全 $1$，沿该行展开就是 $S_i$，因为删去该行后余子式不变。
\Derive 对 $i=1$，行列式仍为 $D_n$，所以 $S_1=D_n$。对 $i>1$，替换后与第一行相同，故 $S_i=0$。因 $D_n$ 是上三角行列式，
\[
\sum_{i=1}^n S_i=D_n=1\cdot2\cdots n=n!.
\]
\Verify 选 \textbf{B}。$n!$ 为正且非零，排除 $0,-n!,2n!$。

\Question{6}{填空题}{3}{1662}{***}
4 阶行列式 $D_4=\begin{vmatrix}x&x&1&0\\1&x&2&3\\2&3&x&2\\1&1&2&x\end{vmatrix}$ 中 $x^3$ 的系数为 \blank{}。

\Solution
\Known 求四阶行列式多项式中 $x^3$ 的系数。
\Method 每个行列式项由四行四列各取一个元素。要得到 $x^3$，必须取三个 $x$ 和一个常数。
\Derive 第 $2,3,4$ 行的 $x$ 都在对角线上。若三行都选 $x$，第一行只能选第一列的 $x$，次数为 $4$。若第一行选第一列的 $x$，再从后面三行取两个对角 $x$，剩余行也只能选对角 $x$。因此第一行应选第二列的 $x$。此时第二行不能选 $x$，第三、四行必须取各自的对角 $x$，第二行只能取第一列的 $1$。
\Verify 这唯一的三次项来自列序 $(2,1,3,4)$，故系数为 $\boxed{-1}$。该列序只交换了一对相邻列。

\Question{7}{填空题}{3}{1662}{***}
4 阶行列式 $\begin{vmatrix}2+x&2&2&2\\2&2-x&2&2\\2&2&2+y&2\\2&2&2&2-y\end{vmatrix}=$ \blank{}。

\Solution
\Known 主对角元素是 $2+x,2-x,2+y,2-y$，其余元素都为 $2$。
\Method 按列把矩阵写成对角阵加全 $2$ 矩阵。行列式对列具有线性性，两列取同一个常数列时该项为零。
\Derive 设四个对角改变量为 $(d_1,d_2,d_3,d_4)=(x,-x,y,-y)$。展开时全部取对角列得到 $x^2y^2$。仅第 $j$ 列取全 $2$ 列时得到 $2\prod_{i\ne j}d_i$，其余分量会与别的对角列重合。因此
\[
D=x^2y^2+2(xy^2-xy^2+x^2y-x^2y)=x^2y^2.
\]
\Verify 填 $\boxed{x^2y^2}$。当 $x=0$ 时第一、二列相同；当 $y=0$ 时第三、四列相同，都与结果一致。

\Question{8}{填空题}{3}{1662}{**}
已知矩阵 $A=\begin{pmatrix}1&-1&0&0\\-2&1&-1&1\\3&-2&2&-1\\-2&0&3&4\end{pmatrix}$，$A_{ij}$ 表示 $|A|$ 中元素 $a_{ij}$ 的代数余子式，则 $A_{11}-A_{12}=$ \blank{}。

\Solution
\Known 求第一行的两个代数余子式之差 $A_{11}-A_{12}$。
\Method 原第一行正是 $(1,-1,0,0)$，按这行展开直接得到所求差值。
\Derive 展开两个三阶余子式，并注意 $A_{12}$ 自带负号，
\[
\begin{aligned}
A_{11}&=\begin{vmatrix}1&-1&1\\-2&2&-1\\0&3&4\end{vmatrix}=11-8-6=-3,\\
A_{12}&=-\begin{vmatrix}-2&-1&1\\3&2&-1\\-2&3&4\end{vmatrix}=-(-22+10+13)=-1.
\end{aligned}
\]
\Verify 填 $\boxed{-2}$。由第一行的权重 $1,-1$ 得 $-3-(-1)=-2$，后二项权重为零。

\Question{9}{填空题}{3}{1662}{***}
$n$ 阶行列式 $\begin{vmatrix}b&a&0&\cdots&0&0\\0&b&a&\cdots&0&0\\\vdots&\vdots&\vdots&&\vdots&\vdots\\0&0&0&\cdots&b&a\\a&0&0&\cdots&0&b\end{vmatrix}=$ \blank{}。

\Solution
\Known 主对角线为 $b$，上邻对角线和左下角为 $a$，求 $n$ 阶行列式。
\Method 从第一行取 $b$ 或 $a$。只要某行选了右边的 $a$，下一行的对角列就被占用，会迫使余下行也沿相同方向取 $a$。
\Derive 选第一行的 $b$ 时，最后一行不能取第 $1$ 列，只能取对角元，于是倒推所有行都取 $b$。选第一行的 $a$ 时，依次被迫取 $a$，列序为 $(2,3,\ldots,n,1)$。这个序列仅最后的 $1$ 增加 $n-1$ 个逆序，所以
\[
D=b^n+(-1)^{n-1}a^n.
\]
\Verify 此式对 $a,b$ 为零也适用，因为相应乘积直接为零。取 $n=3$ 展开，得到 $b^3+a^3$，符号相符。

\Question{10}{填空题}{3}{1662}{**}
3 阶行列式 $\begin{vmatrix}a&b&c\\a^2&b^2&c^2\\b+c&c+a&a+b\end{vmatrix}=$ \blank{}。

\Solution
\Known 三行分别是各变量的一次幂、平方，以及另外两个变量的和。
\Method 第三行加第一行后各列都是 $a+b+c$，可提出该公共因子。
\Derive
\[
D=(a+b+c)\begin{vmatrix}a&b&c\\a^2&b^2&c^2\\1&1&1\end{vmatrix}
=(a+b+c)(b-a)(c-a)(c-b).
\]
把常数行移到最前面需要两次相邻行交换，符号保持。之后三行正好是 Vandermonde 行列式的 $0,1,2$ 次幂。
\Verify 任意两个变量相同时两列相同，乘积也含相应零因子。$a+b+c=0$ 时第三行加第一行变成零行。

\Question{11}{解答题}{10}{1662}{***}
计算 4 阶行列式 $D=\begin{vmatrix}0&a&b&a\\a&0&a&b\\b&a&0&a\\a&b&a&0\end{vmatrix}$。

\Solution
\Known 求四阶行列式，四行按 $0,a,b,a$ 的循环结构排列。
\Method 选取四个能体现成对加减的列向量，使矩阵作用在每个向量上时只乘一个数，再利用乘积的行列式。
\Derive 设 $M$ 是题给矩阵，取 $S$ 的列依次为 $(1,1,1,1)^{\mathrm T},(1,-1,1,-1)^{\mathrm T},(1,0,-1,0)^{\mathrm T},(0,1,0,-1)^{\mathrm T}$。分别直接相乘得
\[
MS=S\operatorname{diag}(2a+b,b-2a,-b,-b).
\]
前两列在第 $1,3$ 个分量上相等，在第 $2,4$ 个分量上也相等；后两列分别在这两对分量上相反。若四列线性组合为零，先做分量差可知后两系数为零，再做分量和可知前两系数也为零，因此 $|S|\ne0$。
\Verify 两侧取行列式并约掉 $|S|$，得 $\boxed{b^2(b^2-4a^2)}$。令 $a=0$ 时原矩阵恰为两对交换对应的排列矩阵乘 $b$，行列式为 $b^4$。

\Question{12}{解答题}{10}{1663}{****}
计算 $n$ 阶行列式

\[
D_n=\begin{vmatrix}
a&b&0&\cdots&0&0\\
c&a&b&\cdots&0&0\\
0&c&a&\cdots&0&0\\
\vdots&\vdots&\vdots&&\vdots&\vdots\\
0&0&0&\cdots&a&b\\
0&0&0&\cdots&c&a
\end{vmatrix}\qquad(a^2-4bc\ge0).
\]

\Solution
\Known 求三对角行列式 $D_n$，对角元为 $a$，上、下邻对角元为 $b,c$，且 $a^2-4bc\ge0$。
\Method 沿末行展开得二阶递推，再按特征方程的判别式区分两根是否相同。
\Derive 取 $D_0=1,D_1=a$。末项贡献 $aD_{n-1}$。次末项所在位置的符号为负，余子式沿末列只取 $b$，所以
\[
D_n=aD_{n-1}-bcD_{n-2}\quad(n\ge2).
\]
设 $r_\pm=\frac{a\pm\sqrt{a^2-4bc}}{2}$，它们的和为 $a$，积为 $bc$。

若 $a^2-4bc>0$，则 $r_+\ne r_-$，候选式
\[
D_n=\frac{r_+^{\,n+1}-r_-^{\,n+1}}{r_+-r_-}
\]
满足递推，因为每个 $r$ 都满足 $r^2=ar-bc$；代入 $n=0,1$ 得 $1,a$，故由递推唯一确定。

若 $a^2-4bc=0$，令 $r=\frac{a}{2}$，则 $a=2r,bc=r^2$。代入可得 $(n+1)r^n=2r\cdot nr^{n-1}-r^2(n-1)r^{n-2}$，且初值一致。因此 $D_n=(n+1)r^n$。当 $r=0$ 时由递推直接得 $D_n=0$（$n\ge1$）。
\Verify 两种写法在 $n=2$ 都给 $a^2-bc$，与二阶原式一致。

\Question{13}{解答题}{10}{1663}{*****}
计算 4 阶行列式

\[
D_4=\begin{vmatrix}
a_1^3&a_2^3&a_3^3&a_4^3\\
a_1^2b_1&a_2^2b_2&a_3^2b_3&a_4^2b_4\\
a_1b_1^2&a_2b_2^2&a_3b_3^3&a_4b_4^2\\
b_1^3&b_2^3&b_3^3&b_4^3
\end{vmatrix},\qquad a_i\ne0\ (i=1,2,3,4).
\]

\Solution
\Known 原题第三行第三列印为 $a_3b_3^3$。其余三列第三行的 $b_i$ 指数为 $2$。按原题的指数计算，且各 $a_i\ne0$。
\Method 每列提出 $a_i^3$，令 $t_i=\frac{b_i}{a_i}$。原式与四阶 Vandermonde 行列式仅有一个元素不同，利用行列式对该元素的线性性计算差值。
\Derive 提出因子后，各行依次是 $1,t_i,t_i^2,t_i^3$，第三行第三列额外增加 $t_3^2(b_3-1)$。该元素的代数余子式符号为正，剩下的列号为 $1,2,4$，行是 $0,1,3$ 次幂。令 $s_1=t_1+t_2+t_4$，$s_2=t_1t_2+t_1t_4+t_2t_4$，$s_3=t_1t_2t_4$。对 $t=t_1,t_2,t_4$，由 $(t-t_1)(t-t_2)(t-t_4)=0$ 得 $t^3=s_1t^2-s_2t+s_3$。消去常数行与一次行，余子式就是
\[
s_1(t_2-t_1)(t_4-t_1)(t_4-t_2).
\]
记 $V=\prod_{1\le i<j\le4}(t_j-t_i)$。加回修正项，得
\[
D_4=\left(\prod_{i=1}^4 a_i^3\right)
\bigl[V+t_3^2(b_3-1)s_1(t_2-t_1)(t_4-t_1)(t_4-t_2)\bigr].
\]
\Verify 当 $b_3=1$ 时两种指数对应同一元素，修正项为零。若将该项按其余列的规律写为 $a_3b_3^2$，该版本的答案便只保留 $V$ 项。

\Question{14}{解答题}{10}{1663}{***}
计算 $n$ 阶行列式

\[
\begin{vmatrix}
a&b&b&\cdots&b\\
b&a&b&\cdots&b\\
b&b&a&\cdots&b\\
\vdots&\vdots&\vdots&&\vdots\\
b&b&b&\cdots&a
\end{vmatrix}.
\]

\Solution
\Known 求主对角为 $a$、其他元素为 $b$ 的 $n$ 阶行列式。
\Method 每行的和相同，可以用列相加得到常数列，再用第一行把其他行简化。
\Derive 把第 $2,\ldots,n$ 列加到第一列，第一列变为每项均为 $a+(n-1)b$。提取该因子并把第 $2,\ldots,n$ 行各减第一行。第一列除首元外为零，右下块成为 $(a-b)E_{n-1}$，故
\[
D=\bigl(a+(n-1)b\bigr)(a-b)^{n-1}.
\]
\Verify 提因子来自线性性，即使因子为零也成立。取 $b=0$ 时退化成对角行列式 $a^n$。

\Question{15}{解答题}{10}{1664}{***}
计算 $n$ 阶行列式

\[
\begin{vmatrix}
x-b&b&b&\cdots&b\\
b&x-b&b&\cdots&b\\
b&b&x-b&\cdots&b\\
\vdots&\vdots&\vdots&&\vdots\\
b&b&b&\cdots&x-b
\end{vmatrix}.
\]

\Solution
\Known 求主对角为 $x-b$、其他元素为 $b$ 的 $n$ 阶行列式。
\Method 各行和均相同。把第一列改为所有列的和，可分离一个线性因子。
\Derive 第一列每项是 $x-b+(n-1)b=x+(n-2)b$。提取该因子后，第一列全为 $1$。第 $2$ 至第 $n$ 行分别减第一行，右下块除对角线 $(x-b)-b=x-2b$ 之外全为零。
\Verify $D=\boxed{\bigl(x+(n-2)b\bigr)(x-2b)^{n-1}}$。取 $n=2$，右式为 $x(x-2b)=(x-b)^2-b^2$，与直接展开一致。

\Question{16}{解答题}{10}{1664}{***}
计算 $n$ 阶行列式

\[
D_n=\begin{vmatrix}
0&1&1&\cdots&1&1\\
1&0&x&\cdots&x&x\\
1&x&0&\cdots&x&x\\
\vdots&\vdots&\vdots&&\vdots&\vdots\\
1&x&x&\cdots&0&x\\
1&x&x&\cdots&x&0
\end{vmatrix},
\]

其中 $n>2$。

\Solution
\Known $n>2$。第一行与第一列除首元 $0$ 外全为 $1$，右下块对角为 $0$，其他元素为 $x$。
\Method 后续各行都含同样的 $x$，用第一行消去右下块的非对角元。
\Derive 每个后续行减第一行的 $x$ 倍，首列保持为 $1$，右下块成为 $-xE_{n-1}$。第一行可取的列为 $j=2,\ldots,n$。若第一行取第 $j$ 列，第 $j$ 行只能取第一列；其余行取对角元。该项列序只交换 $1,j$，所以每项均为 $-(-x)^{n-2}$。
\Verify 得 $\boxed{-(n-1)(-x)^{n-2}}$。$n=3$ 时直接展开给 $2x$，一致。$x=0$ 时右下块为零，因 $n>2$，结果也为零。

\Question{17}{解答题}{10}{1664}{***}
计算 $n$ 阶行列式

\[
D_n=\begin{vmatrix}
1&2&2&\cdots&2\\
2&2&2&\cdots&2\\
2&2&3&\cdots&2\\
\vdots&\vdots&\vdots&&\vdots\\
2&2&2&\cdots&n
\end{vmatrix}.
\]

\Solution
\Known 主对角依次为 $1,2,\ldots,n$，其余元素全为 $2$。图中第二行全为 $2$。
\Method 用第二行消去其他行的非对角元，再按第二列展开。
\Derive 对 $n\ge2$，除第二行外各行减第二行。第 $i$ 行只在对角位置留下 $i-2$；第一行留下 $-1$。第二列只剩第二行的 $2$，其位置符号为正。所以
\[
D_n=(-1)\cdot2\cdot1\cdot2\cdots(n-2)=-2(n-2)!.
\]
\Verify $n=2$ 时空乘积按 $1$ 计，直接计算 $1\cdot2-2\cdot2=-2$。若取一阶情形，则只保留左上元，$D_1=1$。

\Volume{矩阵及其运算 A 卷}{mat-a}


## tool · 2026-11-18T12:33:19Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:33:26Z


Script completed
Wall time 0.3 seconds
Output:

\Verify $n=2$ 时空乘积按 $1$ 计，直接计算 $1\cdot2-2\cdot2=-2$。若取一阶情形，则只保留左上元，$D_1=1$。

\Volume{矩阵及其运算 A 卷}{mat-a}

\Question{1}{单项选择题}{3}{1665}{***}
设 $A=(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3)$ 是 3 阶矩阵，则 $|A|=$（　　）。
\Choices
  {$|\boldsymbol{\alpha}_1-\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_2-\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_3-\boldsymbol{\alpha}_1|$}
  {$|\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_2+\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_3+\boldsymbol{\alpha}_1|$}
  {$|\boldsymbol{\alpha}_1+2\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_2|$}
  {$|\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2+\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_2|$}

\Solution
\Known $A$ 的三列是 $\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3$，需要比较各选项与 $|A|$ 的关系。
\Method 用行列式的列线性性和交替性。出现重复列的项为零，每交换两列一次则变号。
\Derive 记 $D=|A|$。（A）三列相加为零，行列式为零。（B）按列展开后仅有原列序与循环列序两项，循环需两次交换，所以值为 $2D$。（C）第一列减第三列，得到 $(\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_1+\boldsymbol{\alpha}_2)$。第三列再减第一列，得到循环列序，值为 $D$。（D）第三列减第一列，再将第三列从第二列中减去，列序变成 $(\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_2)$，值为 $-D$。
\Verify 选 \textbf{C}。可令 $A=E_3$，四项分别为 $0,2,1,-1$，其余三项都不能恒等于 $|A|$。

\Question{2}{单项选择题}{3}{1665}{**}
设 $A,B$ 为同阶方阵，$E$ 为同阶单位矩阵，则下列命题错误的是（　　）。
\Choices
  {$(A+B)^2=A^2+2AB+B^2$}
  {若 $AB=BA$，则 $(AB)^2=A^2B^2$}
  {$(A+\lambda E)^3=A^3+3\lambda A^2+3\lambda^2A+\lambda^3E$（$\lambda$ 为数）}
  {若 $A,B$ 相乘可交换，则 $A+B$ 与 $A-B$ 相乘也可交换}

\Solution
\Known $A,B$ 为同阶方阵，$E$ 为同阶单位矩阵，找出错误命题。
\Method 展开矩阵乘法时保持因子顺序。只有互相可交换的因子才能像数一样合并。
\Derive （A）的左边为 $A^2+AB+BA+B^2$，通常 $AB\ne BA$。（B）假设 $AB=BA$，所以 $ABAB=A(BA)B=A^2B^2$。（C）$\lambda E$ 与 $A$ 可交换，三阶二项展开成立。（D）在 $AB=BA$ 时，$(A+B)(A-B)$ 与 $(A-B)(A+B)$ 展开后都等于 $A^2-B^2$。
\Verify 选 \textbf{A}。例如取 $A=\begin{pmatrix}0&1\\0&0\end{pmatrix}$、$B=\begin{pmatrix}0&0\\1&0\end{pmatrix}$，（A）左边为 $E_2$，右边为 $\operatorname{diag}(2,0)$。

\Question{3}{单项选择题}{3}{1665}{***}
设 $A$ 为 $n$ 阶方阵，$A^*$ 为 $A$ 的伴随矩阵，则 $\left|\,|A^*|A\,\right|=$（　　）。
\Choices
  {$|A|^{n^2}$}
  {$|A|^n$}
  {$|A|^{n^2-n}$}
  {$|A|^{n^2-n+1}$}

\Solution
\Known $A^*$ 是 $A$ 的伴随矩阵。内层 $|A^*|$ 是标量，外层取矩阵 $|A^*|A$ 的行列式。
\Method 用 $AA^*=|A|E$ 求 $|A^*|$，再利用标量乘 $n$ 阶矩阵时，行列式的每一列都带一个标量因子。
\Derive 当 $|A|\ne0$，对伴随矩阵恒等式取行列式，得到 $|A|\,|A^*|=|A|^n$，所以 $|A^*|=|A|^{n-1}$。对于 $n\ge2$ 的奇异矩阵，可将 $A$ 换为 $A+tE$。$|A+tE|$ 是首项为 $t^n$ 的多项式，只有有限个零点，故可取非零行列式的 $t$ 趋近 $0$，再由各式均为矩阵元素的多项式取极限。于是
\[
\left|\,|A^*|A\,\right|=|A^*|^n\,|A|=|A|^{n^2-n+1}.
\]
\Verify 选 \textbf{D}。$n=1$ 的伴随矩阵为 $(1)$，所得仍为 $|A|$。取 $n=2,|A|=2$ 时四项分别为 $16,4,4,8$，可排除另外三条通式。

\Question{4}{单项选择题}{3}{1665}{**}
设 $A$ 为正交矩阵，则下列矩阵中不为正交矩阵的是（　　）。
\Choices
  {$A^{\mathrm T}$}
  {$A^2$}
  {$A^*$}
  {$2A$}

\Solution
\Known 已知 $A$ 正交，即 $A^{\mathrm T}A=AA^{\mathrm T}=E$。找出不正交的矩阵。
\Method 对每一项检验其转置与自身的乘积。伴随矩阵可用 $A^*=|A|A^{-1}$，因为正交矩阵已有逆 $A^{\mathrm T}$。
\Derive （A）$(A^{\mathrm T})^{\mathrm T}A^{\mathrm T}=AA^{\mathrm T}=E$。（B）$(A^2)^{\mathrm T}A^2=A^{\mathrm T}(A^{\mathrm T}A)A=E$。（C）由 $|A|^2=|A^{\mathrm T}A|=1$，有 $(A^*)^{\mathrm T}A^*=|A|^2AA^{\mathrm T}=E$。（D）$(2A)^{\mathrm T}(2A)=4E$。
\Verify 选 \textbf{D}。任取一列，正交时其长度为 $1$，放大为两倍后的长度为 $2$。

\Question{5}{单项选择题}{3}{1665}{***}
设 $A,B$ 均为 $n$ 阶可逆矩阵，则下列等式中，必定成立的是（　　）。
\Choices
  {$(A+B)(A-B)=A^2-B^2$}
  {$(A+B)^{-1}=A^{-1}+B^{-1}$}
  {$|A+B|=|A|+|B|$}
  {$(AB)^*=B^*A^*$}

\Solution
\Known $A,B$ 都是可逆矩阵。辨别哪一等式对所有满足条件的 $A,B$ 成立。
\Method 对伴随矩阵使用 $M^*=|M|M^{-1}$，并注意乘积求逆时因子倒序。其他项用符合条件的反例排除。
\Derive $(AB)^{-1}=B^{-1}A^{-1}$，因为与 $AB$ 相乘可逐次约去 $A,B$。因此
\[
(AB)^*=|A||B|B^{-1}A^{-1}=B^*A^*.
\]
（A）还需要 $AB=BA$。取 $A=\operatorname{diag}(1,2)$，$B=\begin{pmatrix}1&1\\0&1\end{pmatrix}$ 时两矩阵均可逆，但 $AB$ 和 $BA$ 的右上元分别为 $1,2$。取 $A=B=E_2$，（B）两侧是 $\frac{1}{2}E_2$ 与 $2E_2$，（C）两侧是 $4$ 与 $2$。
\Verify 选 \textbf{D}。从伴随矩阵恒等式直接验算 $(AB)(B^*A^*)=|A||B|E$，因 $AB$ 可逆，右因子唯一。

\Question{6}{填空题}{3}{1665}{**}
设矩阵 $B=\begin{pmatrix}0&-1&0\\1&0&0\\0&0&1\end{pmatrix}$，$A=P^{-1}BP$，则 $A^4-2B^2=$ \blank{}。

\Solution
\Known $A=P^{-1}BP$，要求 $A^4-2B^2$。题设的 $P^{-1}$ 表示 $P$ 可逆。
\Method 相邻的 $P$ 与 $P^{-1}$ 在矩阵幂里相消。先计算结构简单的 $B^2$ 和 $B^4$。
\Derive $B$ 左上角的 $2$ 阶块平方为 $-E_2$，右下角 $1$ 平方不变，所以
\[
B^2=\operatorname{diag}(-1,-1,1),\qquad B^4=E_3.
\]
逐次相乘得到 $A^4=P^{-1}B^4P=E_3$。因此 $A^4-2B^2=\operatorname{diag}(3,3,-1)$。
\Verify 填 $\operatorname{diag}(3,3,-1)$。特别地，第三个对角元是 $1-2=-1$。

\Question{7}{填空题}{3}{1665}{*}
已知 $A$ 为 3 阶方阵且 $|A|=4$，则 $|2A^2|=$ \blank{}。

\Solution
\Known $A$ 为三阶方阵且 $|A|=4$，求 $|2A^2|$。
\Method 将标量因子与矩阵乘积分别处理。三阶矩阵有三列，提出 $2$ 会出现因子 $2^3$。
\Derive 乘积的行列式为行列式的积，故
\[
|2A^2|=2^3|A^2|=2^3|A|^2=8\cdot16=128.
\]
\Verify 填 $\boxed{128}$。取满足条件的 $A=\operatorname{diag}(4,1,1)$，直接算得 $32\cdot2\cdot2=128$。

\Question{8}{填空题}{3}{1665}{**}
$A^2-B^2=(A+B)(A-B)$ 的充分必要条件是 \blank{}。

\Solution
\Known 求矩阵平方差等式 $A^2-B^2=(A+B)(A-B)$ 成立的充分必要条件。
\Method 展开右边并保留因子顺序，判断额外两项何时相消。
\Derive $(A+B)(A-B)=A^2-AB+BA-B^2$。若等式成立，减去公共项得 $BA-AB=O$；若 $AB=BA$，中间两项相消，等式成立。
\Verify 填 $\boxed{AB=BA}$。两个方向均由同一展开式推出，适用于所有乘法有定义的同阶方阵。

\Question{9}{填空题}{3}{1665}{**}
设矩阵 $A=\begin{pmatrix}3&0&0\\1&4&0\\0&0&3\end{pmatrix}$，$E=\begin{pmatrix}1&0&0\\0&1&0\\0&0&1\end{pmatrix}$，则 $(A-2E)^{-1}=$ \blank{}。

\Solution
\Known 求给定下三角矩阵 $A$ 减去 $2E$ 后的逆。
\Method 减去 $2E$ 只改变对角元。左上 $2$ 阶块和右下 $1$ 阶块互不影响，可逐块解方程。
\Derive 对 $(A-2E)u=v$，逐行得 $u_1=v_1$、$u_1+2u_2=v_2$、$u_3=v_3$，于是
\[
(A-2E)^{-1}=\begin{pmatrix}1&0&0\\-\frac{1}{2}&\frac{1}{2}&0\\0&0&1\end{pmatrix}.
\]
\Verify 三个对角元 $1,2,1$ 都非零。把所求逆矩阵左乘 $A-2E$，第二行的第一元为 $1-1=0$，其余元素也与 $E_3$ 一致。

\Question{10}{填空题}{3}{1666}{***}
设矩阵 $A=\begin{pmatrix}1&-1&2\\-2&-1&-2\\4&3&3\end{pmatrix}$，则 $A^{-1}=$ \blank{}，$(A^*)^{-1}=$ \blank{}，$[(-2A)^*]^{-1}=$ \blank{}。

\Solution
\Known 求 $A^{-1}$、$(A^*)^{-1}$ 和 $[(-2A)^*]^{-1}$。
\Method 先求行列式和伴随矩阵。三阶矩阵的伴随矩阵由二阶代数余子式转置组成，整矩阵倍乘 $-2$ 时每个二阶余子式乘 $4$。
\Derive 第二行加第一行的 $2$ 倍，第三行减第一行的 $4$ 倍，按首列展开给 $|A|=(-3)(-5)-2\cdot7=1$。例如第一行的三个代数余子式依次为 $3,-2,-2$，转置后成为 $A^*$ 的第一列。将九个余子式这样排列得
\[
A^{-1}=\frac{A^*}{|A|}=\begin{pmatrix}3&9&4\\-2&-5&-2\\-2&-7&-3\end{pmatrix}.
\]
因此 $(A^*)^{-1}=A$。又 $(-2A)^*=4A^*$，故 $[(-2A)^*]^{-1}=\frac{1}{4}A$。
\Verify 直接相乘得 $AA^*=E_3$。将后两空分别乘回 $A^*$ 和 $4A^*$，均得 $E_3$。

\Question{11}{解答题}{10}{1666}{***}
设矩阵 $A=\begin{pmatrix}1&0&2&0\\0&-2&0&0\\-1&0&1&0\\0&0&0&1\end{pmatrix}$，矩阵 $B$ 满足 $AB+B+A+2E=O$，求 $|B+E|$。

\Solution
\Known 已知 $AB+B+A+2E=O$，求 $|B+E|$。
\Method 方程含 $AB,B,A$，可配出保持因子顺序的 $(A+E)(B+E)$，再对等式取行列式。
\Derive $(A+E)(B+E)=AB+B+A+E=-E$。$A+E$ 的第 $2,4$ 行各只有对角项，按这两行展开，
\[
|A+E|=(-1)\cdot2\begin{vmatrix}2&2\\-1&2\end{vmatrix}=-12.
\]
$|-E_4|=(-1)^4=1$，故 $(-12)|B+E|=1$。
\Verify $\boxed{|B+E|=-\frac{1}{12}}$。由于 $|A+E|\ne0$，可用 $B+E=-(A+E)^{-1}$ 再验算行列式。

\Question{12}{解答题}{10}{1666}{**}
设矩阵 $A=\begin{pmatrix}1&1&1\\1&2&3\\1&4&9\end{pmatrix}$，$\boldsymbol{x}=\begin{pmatrix}x_1\\x_2\\x_3\end{pmatrix}$，$\boldsymbol{\beta}=\begin{pmatrix}1\\2\\4\end{pmatrix}$，求线性方程组 $A\boldsymbol{x}=\boldsymbol{\beta}$ 的解。

\Solution
\Known 解三元一次方程组 $A\boldsymbol{x}=\boldsymbol{\beta}$。
\Method 写出三行方程，观察每行 $x_1$ 的系数都为 $1$，两两相减先消去 $x_1$。
\Derive 第二行减第一行得 $x_2+2x_3=1$；第三行减第二行得 $2x_2+6x_3=2$。后一式减前一式的 $2$ 倍得 $2x_3=0$，所以 $x_3=0$、$x_2=1$。第一行给 $x_1+x_2+x_3=1$，所以 $x_1=0$。
\Verify 唯一解是 $\boxed{\boldsymbol{x}=(0,1,0)^{\mathrm T}}$。与 $A$ 相乘取第二列 $(1,2,4)^{\mathrm T}$，与右边一致。

\Question{13}{解答题}{10}{1667}{***}
设矩阵 $A=\begin{pmatrix}2&2&2\\-1&-1&-1\\-1&-1&-1\end{pmatrix}$，求

（1）$A^n$；

（2）$(A+2E)^n$。

\Solution
\Known 求 $A^n$ 和 $(A+2E)^n$。$A$ 的三列完全相同，每列各元素之和为零。
\Method 把 $A$ 写成列向量与行向量的乘积，以便看出二次幂。$2E$ 与 $A$ 可交换，可使用二项式展开。
\Derive 令 $u=(2,-1,-1)^{\mathrm T}$，$v=(1,1,1)$，则 $A=uv$ 且 $vu=2-1-1=0$。所以 $A^2=u(vu)v=O$。

（1）$n=1$ 时结果为 $A$；$n\ge2$ 时 $A^n=O$。

（2）二项展开中 $A^2$ 及更高幂都为零，只留下
\[
(A+2E)^n=2^nE+n2^{n-1}A\qquad(n\ge1).
\]
\Verify $n=2$ 时直接展开为 $4E+4A$，与公式一致。若取 $n=0$，两式的零次幂均按 $E$ 计。

\Question{14}{解答题}{10}{1667}{***}
已知矩阵 $A=\begin{pmatrix}\lambda&1&0\\0&\lambda&1\\0&0&\lambda\end{pmatrix}$，计算 $A^n$。

\Solution
\Known $A$ 的三个对角元均为 $\lambda$，紧挨主对角线上方的两个元素为 $1$。
\Method 拆成 $\lambda E+N$，其中 $N$ 只有上邻对角线为 $1$。计算 $N$ 的幂，再用可交换矩阵的二项式展开。
\Derive 直接相乘可得 $N^2$ 仅 $(1,3)$ 元为 $1$，$N^3=O$。因此 $n\ge2$ 时
\[
A^n=\lambda^nE+n\lambda^{n-1}N+\binom n2\lambda^{n-2}N^2
=\begin{pmatrix}
\lambda^n&n\lambda^{n-1}&\binom n2\lambda^{n-2}\\
0&\lambda^n&n\lambda^{n-1}\\
0&0&\lambda^n
\end{pmatrix}.
\]
$n=1$ 取 $A$，$n=0$ 取 $E$；在 $n=2$ 的常数项 $\lambda^0$ 为 $1$。
\Verify $n=2$ 时右上元为 $1$，也等于 $A$ 的第一行乘第三列所得。$\lambda=0$ 时 $A=N$，三次及以上幂全部为零。

\Question{15}{解答题}{10}{1667}{***}
已知 $n$ 阶矩阵 $A$ 满足 $A^2-A-5E=O$，求 $(A-3E)^{-1}$。

\Solution
\Known $A^2-A-5E=O$，求 $(A-3E)^{-1}$。
\Method 试用一次矩阵多项式作逆矩阵，因为乘积的二次项可以用已知关系消去。
\Derive 用 $A+2E$ 乘 $A-3E$，系数 $2-3=-1$ 正好匹配 $A$ 项，
\[
(A-3E)(A+2E)=A^2-A-6E=-E.
\]
因此 $(A-3E)(-A-2E)=E$。
\Verify 所求为 $\boxed{-A-2E}$。两个因子都是 $A$ 的多项式，乘法可交换，故反序相乘也为 $E$。

\Question{16}{解答题}{10}{1668}{***}
若矩阵 $A=\begin{pmatrix}0&0&1&1\\0&0&3&2\\3&2&0&0\\3&4&0&0\end{pmatrix}$，求 $|A|,A^{-1}$。

\Solution
\Known 求四阶矩阵 $A$ 的行列式和逆。按前两行和后两行、前两列和后两列分块，$A=\begin{pmatrix}O&B\\C&O\end{pmatrix}$。
\Method 互换两组列可将 $B,C$ 移到主对角块。对于求逆，可以选同样的反对角结构，使乘积的对角块分别为单位矩阵。
\Derive $B=\begin{pmatrix}1&1\\3&2\end{pmatrix}$，$C=\begin{pmatrix}3&2\\3&4\end{pmatrix}$。交换列组是排列 $(3,4,1,2)$，有四个逆序，所以 $|A|=|B||C|=(-1)6=-6$。两块均可逆，二阶逆公式给
\[
B^{-1}=\begin{pmatrix}-2&1\\3&-1\end{pmatrix},\quad
C^{-1}=\frac{1}{6}\begin{pmatrix}4&-2\\-3&3\end{pmatrix},\quad
A^{-1}=\begin{pmatrix}O&C^{-1}\\B^{-1}&O\end{pmatrix}.
\]
\Verify 分块相乘的两个非零对角块为 $BB^{-1}$、$CC^{-1}$，均为 $E_2$，因此给出的块位置和次序正确。

\Question{17}{解答题}{10}{1668}{**}
已知矩阵 $A=\begin{pmatrix}a&b\\c&d\end{pmatrix}$，求 $A^*,(A^*)^*$。

\Solution
\Known 给定二阶矩阵 $A$，求 $A^*$ 以及再取一次伴随矩阵的结果。
\Method 按定义，先给每个余子式乘上位置符号，再转置。二阶余子式只由一个元素组成。
\Derive 矩阵 $A$ 的代数余子式矩阵为 $\begin{pmatrix}d&-c\\-b&a\end{pmatrix}$，所以
\[
A^*=\begin{pmatrix}d&-b\\-c&a\end{pmatrix},\qquad
(A^*)^*=\begin{pmatrix}a&b\\c&d\end{pmatrix}=A.
\]
\Verify $AA^*=(ad-bc)E$，可核对位置与符号。两次取伴随均按定义计算，$ad-bc=0$ 时也成立。

\Volume{矩阵及其运算 B 卷}{mat-b}

\Question{1}{单项选择题}{3}{1669}{**}
设 $\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\beta}_1,\boldsymbol{\beta}_2$ 均为四维列向量，且
\[
|A|=|\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\beta}_1|=m,\qquad
|B|=|\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\beta}_2,\boldsymbol{\alpha}_3|=n,
\]
则 $|\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_1,\boldsymbol{\beta}_1+\boldsymbol{\beta}_2|=$（　　）。
\Choices
  {$m+n$}
  {$m-n$}
  {$-(m+n)$}
  {$n-m$}

\Solution
\Known 已知两个四阶行列式，求前三列顺序改变且末列为 $\boldsymbol{\beta}_1+\boldsymbol{\beta}_2$ 的行列式。
\Method 按末列的线性性分开，再比较各自的列序。一次列交换使行列式变号。
\Derive $\boldsymbol{\beta}_1$ 项从 $A$ 交换第一、三列得到，值为 $-m$。$\boldsymbol{\beta}_2$ 项从 $B$ 先交换第三、四列，再交换第一、三列得到，共两次交换，值仍为 $n$。
\Verify 和为 $\boxed{n-m}$，选 \textbf{D}。前一个系数为 $-1$、后一个为 $+1$，其余三项至少有一个系数不符。

\Question{2}{单项选择题}{3}{1669}{***}
设 $A,B$ 均为 2 阶矩阵，$A^*,B^*$ 分别为 $A,B$ 的伴随矩阵，若 $|A|=2$，$|B|=3$，则分块矩阵 $\begin{pmatrix}O&A\\B&O\end{pmatrix}$ 的伴随矩阵为（　　）。
\Choices
  {$\begin{pmatrix}O&3B^*\\2A^*&O\end{pmatrix}$}
  {$\begin{pmatrix}O&2B^*\\3A^*&O\end{pmatrix}$}
/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/proof-venv/lib/python3.12/site-packages/pymupdf/__init__.py
from itertools import combinations
from math import factorial, prod, sqrt

import numpy as np


checks = 0


def check(actual, expected):
    global checks
    np.testing.assert_allclose(actual, expected, rtol=1e-9, atol=1e-9)
    checks += 1


det = np.linalg.det
inv = np.linalg.inv
power = np.linalg.matrix_power
E3, E4 = np.eye(3, dtype=int), np.eye(4, dtype=int)

check(sum(a > b for a, b in combinations("217986354", 2)), 18)
check(det([[2, 1, 1, 1], [4, 0, 1, 1], [6, 2, 0, 2], [8, 3, 3, 0]]), -34)


## assistant · 2026-11-18T12:33:33Z

行列式 A、B 两卷的 34 道解析已改写。递推题现在先让读者试着从末行降阶，再引导他们把递推式整理成可以逐步计算的形式。接下来处理矩阵两卷。

## tool · 2026-11-18T12:34:54Z


Script completed
Wall time 0.2 seconds
Output:

{}

## tool · 2026-11-18T12:34:59Z


Script completed
Wall time 0.1 seconds
Output:

\Volume{矩阵及其运算 B 卷}{mat-b}

\Question{1}{单项选择题}{3}{1669}{**}
设 $\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\beta}_1,\boldsymbol{\beta}_2$ 均为四维列向量，且
\[
|A|=|\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_3,\boldsymbol{\beta}_1|=m,\qquad
|B|=|\boldsymbol{\alpha}_1,\boldsymbol{\alpha}_2,\boldsymbol{\beta}_2,\boldsymbol{\alpha}_3|=n,
\]
则 $|\boldsymbol{\alpha}_3,\boldsymbol{\alpha}_2,\boldsymbol{\alpha}_1,\boldsymbol{\beta}_1+\boldsymbol{\beta}_2|=$（　　）。
\Choices
  {$m+n$}
  {$m-n$}
  {$-(m+n)$}
  {$n-m$}

\Solution
\Known 已知两个四阶行列式，求前三列顺序改变且末列为 $\boldsymbol{\beta}_1+\boldsymbol{\beta}_2$ 的行列式。
\Method 按末列的线性性分开，再比较各自的列序。一次列交换使行列式变号。
\Derive $\boldsymbol{\beta}_1$ 项从 $A$ 交换第一、三列得到，值为 $-m$。$\boldsymbol{\beta}_2$ 项从 $B$ 先交换第三、四列，再交换第一、三列得到，共两次交换，值仍为 $n$。
\Verify 和为 $\boxed{n-m}$，选 \textbf{D}。前一个系数为 $-1$、后一个为 $+1$，其余三项至少有一个系数不符。

\Question{2}{单项选择题}{3}{1669}{***}
设 $A,B$ 均为 2 阶矩阵，$A^*,B^*$ 分别为 $A,B$ 的伴随矩阵，若 $|A|=2$，$|B|=3$，则分块矩阵 $\begin{pmatrix}O&A\\B&O\end{pmatrix}$ 的伴随矩阵为（　　）。
\Choices
  {$\begin{pmatrix}O&3B^*\\2A^*&O\end{pmatrix}$}
  {$\begin{pmatrix}O&2B^*\\3A^*&O\end{pmatrix}$}
  {$\begin{pmatrix}O&3A^*\\2B^*&O\end{pmatrix}$}
  {$\begin{pmatrix}O&2A^*\\3B^*&O\end{pmatrix}$}

\Solution
\Known 分块矩阵 $M=\begin{pmatrix}O&A\\B&O\end{pmatrix}$，其中 $A,B$ 是二阶矩阵，行列式分别为 $2,3$。求 $M^*$。
\Method 两块均可逆。先通过换列得到 $|M|$，再用分块乘法求 $M^{-1}$。
\Derive 交换两组各两列，相当于两次对应列交换，所以符号为正，$|M|=|A||B|=6$。用 $M$ 左乘 $\begin{pmatrix}O&B^{-1}\\A^{-1}&O\end{pmatrix}$ 得到 $E_4$。故
\[
M^*=6M^{-1}
=\begin{pmatrix}O&2B^*\\3A^*&O\end{pmatrix},
\]
其中 $B^{-1}=\frac{B^*}{3}$，$A^{-1}=\frac{A^*}{2}$。
\Verify 选 \textbf{B}。左乘 $M$ 后，正确的两块分别给 $3AA^*=6E_2$、$2BB^*=6E_2$；其余选项没有同时给出所需的因子和位置。

\Question{3}{单项选择题}{3}{1669}{**}
设 $A$ 为 $n$ 阶可逆矩阵，则下列等式中，不一定成立的是（　　）。
\Choices
  {$(A+A^{-1})^2=A^2+2AA^{-1}+(A^{-1})^2$}
  {$(A+A^{\mathrm T})^2=A^2+2AA^{\mathrm T}+(A^{\mathrm T})^2$}
  {$(A+A^*)^2=A^2+2AA^*+(A^*)^2$}
  {$(A+E)^2=A^2+2AE+E^2$}

\Solution
\Known $A$ 可逆。比较它与 $A^{-1}$、$A^{\mathrm T}$、$A^*$、$E$ 的平方展开，找出不一定成立的等式。
\Method 对任意同阶的 $U,V$，$(U+V)^2=U^2+UV+VU+V^2$。用 $2UV$ 代替中间两项的条件是 $UV=VU$。
\Derive （A）$A$ 与 $A^{-1}$ 的两个乘积均为 $E$。（C）$AA^*=A^*A=|A|E$。（D）$AE=EA=A$。对（B），取可逆矩阵 $A=\begin{pmatrix}1&1\\0&1\end{pmatrix}$，则
\[
AA^{\mathrm T}=\begin{pmatrix}2&1\\1&1\end{pmatrix},\qquad
A^{\mathrm T}A=\begin{pmatrix}1&1\\1&2\end{pmatrix}.
\]
\Verify 选 \textbf{B}。反例矩阵的行列式为 $1$，符合可逆条件，且两个交叉项的和不等于 $2AA^{\mathrm T}$。

\Question{4}{单项选择题}{3}{1669}{**}
设 $A,B,C$ 均为 $n$ 阶矩阵，且 $AB=BC=CA=E$，则 $A^2+B^2+C^2=$（　　）。
\Choices
  {$3E$}
  {$2E$}
  {$E$}
  {$O$}

\Solution
\Known 同阶方阵满足 $AB=BC=CA=E$，求 $A^2+B^2+C^2$。
\Method 每个乘积等于单位阵，说明相关因子互为逆。逐个消去 $B,C$。
\Derive 从 $AB=E$ 得 $B=A^{-1}$，因方阵有右逆即有逆。从 $BC=E$ 得 $C=B^{-1}=A$。再由 $CA=E$ 得 $A^2=E$，因此 $B=A^{-1}=A$，三个平方都等于 $E$。
\Verify 选 \textbf{A}。和为 $3E$，与 $2E,E,O$ 均不同；取 $A=B=C=E$ 也直接给出 $3E$。

\Question{5}{单项选择题}{3}{1669}{***}
设 $A,B$ 均为 $n$ 阶方阵，且 $AB=A+B$，则下列命题中：

① 若 $A$ 可逆，则 $B$ 可逆；

② 若 $A+B$ 可逆，则 $B$ 可逆；

③ 若 $B$ 可逆，则 $A+B$ 可逆；

④ $A-E$ 恒可逆，

正确的个数为（　　）。
\Choices
  {$1$}
  {$2$}
  {$3$}
  {$4$}

\Solution
\Known $A,B$ 为同阶方阵且 $AB=A+B$，判断四个命题。
\Method 原式含乘积和两个一次项，可以补上一个 $E$ 配成乘积。同时利用方阵乘积可逆当且仅当两因子均可逆。
\Derive $(A-E)(B-E)=AB-A-B+E=E$，所以 $A-E,B-E$ 均可逆，④成立。由 $(A-E)B=A$ 得 $B=(A-E)^{-1}A$，故 $A$ 可逆时 $B$ 可逆，①成立。$A+B=AB$ 可逆时两因子可逆，②成立。若 $B$ 可逆，由 $A(B-E)=B$ 得 $A=B(B-E)^{-1}$ 可逆，继而 $AB$ 可逆，③成立。
\Verify 共 $4$ 个命题成立，选 \textbf{D}。这些推导中所用的两个移位矩阵的逆均由第一式保证。

\Question{6}{填空题}{3}{1669}{***}
设 $A$ 为奇数阶矩阵，$AA^{\mathrm T}=A^{\mathrm T}A=E$，$|A|>0$，则 $|A-E|=$ \blank{}。

\Solution
\Known $A$ 为奇数阶，$AA^{\mathrm T}=A^{\mathrm T}A=E$ 且 $|A|>0$。求 $|A-E|$。
\Method 先确定 $|A|$。将 $A-E$ 分解为 $A(E-A^{-1})$，利用 $A^{-1}=A^{\mathrm T}$，把行列式换成 $|E-A|$。
\Derive $|A|^2=|AA^{\mathrm T}|=1$，由正号知 $|A|=1$。设阶数为 $n$，则
\[
|A-E|=|A|\,|E-A^{\mathrm T}|=|(E-A)^{\mathrm T}|
=|E-A|=(-1)^n|A-E|.
\]
\Verify $n$ 为奇数，故该数等于自身的相反数，填 $\boxed{0}$。例如 $A=E$ 时 $A-E$ 为零矩阵。

\Question{7}{填空题}{3}{1670}{**}
设 3 阶矩阵 $A=\begin{pmatrix}1&0&1\\0&2&0\\1&0&1\end{pmatrix}$，而 $n\ge2$ 为整数，则 $A^n-2A^{n-1}=$ \blank{}。

\Solution
\Known $n\ge2$ 为整数，要求 $A^n-2A^{n-1}$。
\Method 矩阵第一、三行相同，第二行只有一个非零元，先计算 $A^2$。
\Derive 逐行乘 $A$，第一、三行皆为 $(2,0,2)$，第二行为 $(0,4,0)$，所以 $A^2=2A$。由 $n-2\ge0$，
\[
A^n-2A^{n-1}=A^{n-2}(A^2-2A)=O.
\]
\Verify 填三阶零矩阵 $\boxed{O}$。$n=2$ 时直接就是已经验算的平方恒等式。

\Question{8}{填空题}{3}{1670}{**}
已知 $\boldsymbol{\alpha}=(1,2,3)$，$\boldsymbol{\beta}=\left(1,\frac{1}{2},\frac{1}{3}\right)$，设 $A=\boldsymbol{\alpha}^{\mathrm T}\boldsymbol{\beta}$，其中 $\boldsymbol{\alpha}^{\mathrm T}$ 是 $\boldsymbol{\alpha}$ 的转置，则 $A^n=$ \blank{}。

\Solution
\Known $A=\boldsymbol{\alpha}^{\mathrm T}\boldsymbol{\beta}$，其中 $\boldsymbol{\alpha},\boldsymbol{\beta}$ 都是三维行向量。求 $A^n$。
\Method 相邻两个 $A$ 相乘时，中间出现 $1\times1$ 的乘积 $\boldsymbol{\beta}\boldsymbol{\alpha}^{\mathrm T}$，可把它当作标量。
\Derive 点积为 $1+2\cdot\frac{1}{2}+3\cdot\frac{1}{3}=3$。因此
\[
A^2=\boldsymbol{\alpha}^{\mathrm T}(\boldsymbol{\beta}\boldsymbol{\alpha}^{\mathrm T})\boldsymbol{\beta}=3A.
\]
若 $A^k=3^{k-1}A$，右乘 $A$ 得 $A^{k+1}=3^kA$，从 $k=1$ 开始即可得到通式。
\Verify 填 $\boxed{3^{n-1}A}$（$n\ge1$）。$n=1,2$ 均与直接计算一致；若取 $n=0$，则 $A^0=E_3$。

\Question{9}{填空题}{3}{1670}{**}
设 3 阶矩阵 $A=\begin{pmatrix}1&0&0\\0&1&0\\-3&0&3\end{pmatrix}$，则 $\left|(2E-A)^{\mathrm T}(4E-A^2)\right|=$ \blank{}。

\Solution
\Known $A$ 为下三角矩阵。求乘积 $(2E-A)^{\mathrm T}(4E-A^2)$ 的行列式。
\Method 先拆成两个因子的行列式。转置不改行列式，下三角矩阵的行列式只需看对角元。
\Derive $2E-A$ 对角元为 $1,1,-1$，其行列式为 $-1$。$A^2$ 仍为下三角，对角元为原对角元的平方 $1,1,9$，所以 $4E-A^2$ 的对角元是 $3,3,-5$，行列式为 $-45$。
\Verify 填 $\boxed{45}$。也可用 $4E-A^2=(2E-A)(2E+A)$，故原式为 $|2E-A|^2\,|2E+A|=45$。

\Question{10}{填空题}{3}{1670}{**}
设 4 阶方阵 $A=\begin{pmatrix}5&2&0&0\\2&1&0&0\\0&0&1&-2\\0&0&1&1\end{pmatrix}$，则 $A$ 的逆矩阵 $A^{-1}=$ \blank{}。

\Solution
\Known 给定四阶矩阵的左上和右下各有一个二阶块，另外两块为零。求 $A^{-1}$。
\Method 把两个二阶块各自求逆。分块相乘时这两个块独立，只要两块都可逆即可。
\Derive 两块的行列式分别为 $5\cdot1-2^2=1$、$1\cdot1-(-2)\cdot1=3$。二阶逆公式给出
\[
A^{-1}=\begin{pmatrix}
1&-2&0&0\\
-2&5&0&0\\
0&0&\frac{1}{3}&\frac{2}{3}\\
0&0&-\frac{1}{3}&\frac{1}{3}
\end{pmatrix}.
\]
\Verify 原左上块与新左上块的乘积是 $E_2$。右下块乘对应逆块的分子矩阵得到 $3E_2$，乘系数 $\frac{1}{3}$ 后也为 $E_2$。

\Question{11}{解答题}{10}{1670}{***}
设矩阵 $A=\begin{pmatrix}1&-1&1\\0&3&-2\\-1&0&4\end{pmatrix}$，$B=\begin{pmatrix}1&7&-1\\0&3&0\\-3&-2&4\end{pmatrix}$，化简并计算 $A^2(BA)^*\cdot(AB^{-1})^{-1}$。

\Solution
\Known 计算 $A^2(BA)^*\cdot(AB^{-1})^{-1}$。需要保留每个因子的顺序。
\Method 用伴随矩阵与逆矩阵的关系，把两部分都写成易于逐次约去的乘积。
\Derive 按首列展开 $|A|=12+1=13$。按第二行展开 $|B|=3(4-3)=3$，故都可逆且 $|BA|=39$。于是
\[
(BA)^*=39A^{-1}B^{-1},\qquad (AB^{-1})^{-1}=BA^{-1}.
\]
代入后，先约去中间的 $B^{-1}B$，剩下 $39A^2A^{-1}A^{-1}=39E_3$。
\Verify 所求为 $\boxed{39E_3}$。相消的因子均相邻，过程中无需交换 $A$ 与 $B$。

\Question{12}{解答题}{10}{1670}{***}
设矩阵 $A=\begin{pmatrix}1&1&0\\1&2&0\\0&0&2\end{pmatrix}$，3 阶矩阵 $B$ 满足 $ABA^*=E-BA^{-1}$，试计算 $|B|$。

\Solution
\Known $ABA^*=E-BA^{-1}$，求 $|B|$。矩阵 $A$ 的左上二阶块行列式为 $1$，右下元为 $2$。
\Method 等式右乘 $A$，其中 $A^*A=|A|E$，而 $A^{-1}A=E$，这样可把 $B$ 提到共同的右侧。
\Derive $|A|=2$。右乘 $A$ 后得 $2AB=A-B$，即 $(2A+E)B=A$。其中
\[
|2A+E|=5\begin{vmatrix}3&2\\2&5\end{vmatrix}
=5(15-4)=55.
\]
两侧取行列式，$55|B|=2$。
\Verify 得 $\boxed{|B|=\frac{2}{55}}$。因为 $55\ne0$，方程确有唯一解 $B=(2A+E)^{-1}A$，代回右乘后的方程成立。

\Question{13}{解答题}{10}{1671}{***}
设 4 阶矩阵 $A=\begin{pmatrix}1&&&\\-2&3&&\\&-4&5&\\&&-6&7\end{pmatrix}$，且 $B=(E+A)^{-1}(E-A)$，求 $(E+B)^{-1}$。

\Solution
\Known $B=(E+A)^{-1}(E-A)$，求 $(E+B)^{-1}$。$A$ 是下三角矩阵。
\Method 把 $E$ 写成 $(E+A)^{-1}(E+A)$，与 $B$ 合并。
\Derive $E+A$ 的对角元为 $2,4,6,8$，故可逆。于是
\[
E+B=(E+A)^{-1}\bigl[(E+A)+(E-A)\bigr]=2(E+A)^{-1}.
\]
求逆得到
\[
(E+B)^{-1}=\frac{1}{2}(E+A)=
\begin{pmatrix}1&0&0&0\\-1&2&0&0\\0&-2&3&0\\0&0&-3&4\end{pmatrix}.
\]
\Verify 与 $2(E+A)^{-1}$ 相乘恰为 $E_4$，所以逆存在且上式正确。

\Question{14}{解答题}{10}{1671}{****}
设 $A$ 是 $m\times n$ 矩阵，$B$ 是 $n\times m$ 矩阵，已知 $E_m+AB$ 可逆。

（1）验证 $E_n+BA$ 可逆，且 $(E_n+BA)^{-1}=E_n-B(E_m+AB)^{-1}A$；

（2）设

\[
W=\begin{pmatrix}
1+a_1b_1&a_1b_2&a_1b_3\\
a_2b_1&1+a_2b_2&a_2b_3\\
a_3b_1&a_3b_2&1+a_3b_3
\end{pmatrix},
\]

其中 $a_1b_1+a_2b_2+a_3b_3=0$。证明 $W$ 可逆，并求 $W^{-1}$。

\Solution
\Known $A$ 为 $m\times n$，$B$ 为 $n\times m$，$E_m+AB$ 可逆。先证逆矩阵恒等式，再求给定的 $W^{-1}$。
\Method （1）用直接相乘检验候选逆矩阵。（2）把 $W-E_3$ 写成列向量乘行向量，使题给的三项和恰好出现。
\Derive （1）设 $S=E_m+AB$、$T=E_n+BA$。有 $TB=B+BAB=BS$，所以
\[
T(E_n-BS^{-1}A)=T-BSS^{-1}A=T-BA=E_n.
\]
两个因子均为 $n$ 阶方阵，取行列式可知 $T$ 可逆，右侧候选式即 $T^{-1}$。

（2）令 $u=(a_1,a_2,a_3)^{\mathrm T}$，$v=(b_1,b_2,b_3)$，则 $W=E_3+uv$。题给 $vu=0$，因此 $1+vu=1$ 可逆。将（1）中的 $A,B$ 分别取为 $v,u$，得到
\[
W^{-1}=E_3-uv=
\begin{pmatrix}
1-a_1b_1&-a_1b_2&-a_1b_3\\
-a_2b_1&1-a_2b_2&-a_2b_3\\
-a_3b_1&-a_3b_2&1-a_3b_3
\end{pmatrix}.
\]
\Verify $(uv)^2=u(vu)v=O$，故 $(E_3+uv)(E_3-uv)=E_3$，直接核实第（2）问。

\Question{15}{解答题}{10}{1671}{***}
已知 $AP=PB$，其中

\[
B=\begin{pmatrix}1&0&0\\0&0&0\\0&0&-1\end{pmatrix},\qquad
P=\begin{pmatrix}1&0&0\\2&-1&0\\2&1&1\end{pmatrix},
\]

求 $A$ 及 $A^5$。

\Solution
\Known $AP=PB$，其中 $B=\operatorname{diag}(1,0,-1)$。求 $A$ 与 $A^5$。
\Method $P$ 为下三角且对角元 $1,-1,1$ 均非零，所以 $A=PBP^{-1}$，矩阵幂可通过对角阵计算。求 $A$ 的各列时可直接利用 $AP=PB$。
\Derive 记 $A$ 的列为 $c_1,c_2,c_3$。$P$ 的第三列为 $(0,0,1)^{\mathrm T}$，乘 $B$ 的第三个对角因子给 $c_3=(0,0,-1)^{\mathrm T}$。从第二列得 $-c_2+c_3=0$，从第一列得 $c_1+2c_2+2c_3=(1,2,2)^{\mathrm T}$。所以
\[
A=\begin{pmatrix}1&0&0\\2&0&0\\6&-1&-1\end{pmatrix}.
\]
$A^5=PB^5P^{-1}$，并且 $B^5=B$，故 $A^5=A$。
\Verify 三列等式代回可核对 $AP=PB$；五次幂中每对相邻的 $P^{-1}P$ 都化为 $E_3$。

\Question{16}{解答题}{10}{1672}{****}
设 $(2E-C^{-1}B)A^{\mathrm T}=C^{-1}$，其中 $E$ 是 4 阶单位矩阵，$A^{\mathrm T}$ 是 4 阶矩阵 $A$ 的转置矩阵，

\[
B=\begin{pmatrix}1&2&-3&-2\\0&1&2&-3\\0&0&1&2\\0&0&0&1\end{pmatrix},\qquad
C=\begin{pmatrix}1&2&0&1\\0&1&2&0\\0&0&1&2\\0&0&0&1\end{pmatrix},
\]

求 $A$。

\Solution
\Known 由 $(2E-C^{-1}B)A^{\mathrm T}=C^{-1}$ 求 $A$。$C$ 为对角元全为 $1$ 的上三角矩阵。
\Method 从左乘 $C$ 消去 $C^{-1}$，将问题变成求一个上三角矩阵的逆，最后转置。
\Derive $(2C-B)A^{\mathrm T}=E$。记 $N$ 为四阶矩阵中上邻对角线为 $1$、其余为 $0$ 的矩阵。代入 $B,C$，得 $2C-B=E+2N+3N^2+4N^3$。$N^4=O$，直接展开
\[
(E+2N+3N^2+4N^3)(E-2N+N^2)=E,
\]
因为 $N,N^2,N^3$ 的系数依次为 $2-2$、$3-4+1$、$4-6+2$，均为零。所以
\[
A=(E-2N+N^2)^{\mathrm T}=\begin{pmatrix}
1&0&0&0\\-2&1&0&0\\1&-2&1&0\\0&1&-2&1
\end{pmatrix}.
\]
\Verify $2C-B$ 的对角元全为 $1$，故解唯一。将上述乘积等式左乘 $C^{-1}$，即可还原题给等式。

\Question{17}{解答题}{10}{1672}{**}
求所有与矩阵 $A=\begin{pmatrix}1&1\\0&1\end{pmatrix}$ 乘法可交换的矩阵。

\Solution
\Known 求与 $A=\begin{pmatrix}1&1\\0&1\end{pmatrix}$ 可交换的所有矩阵 $X$。两种乘积都要有定义，所以 $X$ 为二阶方阵。
\Method 设四个元素为未知量，把 $AX$ 与 $XA$ 展开，逐个比较对应位置。
\Derive 设 $X=\begin{pmatrix}a&b\\c&d\end{pmatrix}$，则
\[
AX=\begin{pmatrix}a+c&b+d\\c&d\end{pmatrix},\qquad
XA=\begin{pmatrix}a&a+b\\c&c+d\end{pmatrix}.
\]
两边对应元素相等给出 $c=0,d=a$，而 $a,b$ 无额外限制。
\Verify 所有解是 $X=\begin{pmatrix}a&b\\0&a\end{pmatrix}$，其中 $a,b$ 任意。代回两个乘积都会得到 $\begin{pmatrix}a&a+b\\0&a\end{pmatrix}$。

\end{document}
.
..
a4
check-math.py
det-a.txt
det-b.txt
ipad
mat-a.txt
mat-b.txt
verify.py
.
..
bundles
formats
"references/\345\220\214\346\265\216\347\272\277\344\273\243/\345\220\214\346\255\245\346\265\213\350\257\225\345\215\267/\345\220\214\346\265\216\347\272\277\346\200\247\344\273\243\346\225\260\345\220\214\346\255\245\346\265\213\350\257\225\345\215\267.tex"


## tool · 2026-11-18T12:36:25Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:36:36Z


Script completed
Wall time 0.5 seconds
Output:

{"chunk_id":"e08821","wall_time_seconds":0.365727,"exit_code":0,"original_token_count":144,"output":"204\n\n---\n\n## [2026-11-18 20:27] 默认采用引导式数学题解\n\n- **需求**：将类似 Chat 模式的引导式解题设为项目默认写法。\n- **实际结果**：新写或修订题解时，先就题目线索提问，再分步提示，最后展开完整推导并按需验算。\n- **验证**：核对写作规范、适用范围和文档差异。23 项仓库测试通过。\n- **涉及文件**：`AGENTS.md`、`memory/`、`docs/CHANGELOG.md`。\n- **Git 提交**：`187998e31154f4893a836b6cfc11c8ed78c8957e docs: default to guided math solutions`。\n\n---\n2026-11-18 20:36\n"}

## tool · 2026-11-18T12:37:09Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:37:23Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:37:31Z


Script completed
Wall time 1.2 seconds
Output:

[{"status":"fulfilled","value":{"chunk_id":"6f214f","wall_time_seconds":1.00111,"session_id":29392,"original_token_count":36,"output":"note: using only cached resource files\nnote: Running TeX ...\nnote: Rerunning TeX because \"同济线性代数同步测试卷.out\" changed ...\n"}},{"status":"fulfilled","value":{"chunk_id":"e02938","wall_time_seconds":1.000490959,"session_id":16352,"original_token_count":210,"output":"note: reading from standard input; outputs will appear under the base name \"texput\"\nnote: using only cached resource files\nnote: Running TeX ...\nwarning: references/同济线代/同步测试卷/同济线性代数同步测试卷.tex:325: Overfull \\hbox (17.45444pt too wide) in paragraph at lines 324--325\nwarning: references/同济线代/同步测试卷/同济线性代数同步测试卷.tex:557: Overfull \\hbox (20.47818pt too wide) in paragraph at lines 556--557\nnote: Rerunning TeX because \"texput.aux\" changed ...\nwarning: references/同济线代/同步测试卷/同济线性代数同步测试卷.tex:325: Overfull \\hbox (17.45444pt too wide) in paragraph at lines 324--325\nwarning: references/同济线代/同步测试卷/同济线性代数同步测试卷.tex:557: Overfull \\hbox (20.47818pt too wide) in paragraph at lines 556--557\n"}},{"status":"fulfilled","value":{"chunk_id":"eeb5f6","wall_time_seconds":1.002542542,"session_id":83776,"original_token_count":17,"output":"124 numerical checks passed across four volumes.\n.................."}}]

## tool · 2026-11-18T12:37:37Z


Script completed
Wall time 0.2 seconds
Output:

[{"status":"fulfilled","value":{"chunk_id":"a64822","wall_time_seconds":0.000013458,"exit_code":0,"original_token_count":83,"output":"note: Running xdvipdfmx ...\nnote: Writing `.question-bank-work/tongji-tex/ipad/同济线性代数同步测试卷.pdf` (379.9462890625 KiB)\nnote: Writing `.question-bank-work/tongji-tex/ipad/同济线性代数同步测试卷.log` (23.1708984375 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}},{"status":"fulfilled","value":{"chunk_id":"05989a","wall_time_seconds":0.00001425,"exit_code":0,"original_token_count":91,"output":"note: Running xdvipdfmx ...\nwarning: warnings were issued by the TeX engine; use --print and/or --keep-logs for details.\nnote: Writing `.question-bank-work/tongji-tex/a4/texput.pdf` (387.865234375 KiB)\nnote: Writing `.question-bank-work/tongji-tex/a4/texput.log` (24.62890625 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}},{"status":"fulfilled","value":{"chunk_id":"1d42ef","wall_time_seconds":0.000008708,"exit_code":0,"original_token_count":26,"output":".....\n----------------------------------------------------------------------\nRan 23 tests in 0.793s\n\nOK\n"}},{"status":"fulfilled","value":{"chunk_id":"8dafdc","wall_time_seconds":0.00000875,"exit_code":1,"original_token_count":673,"output":"   320\t\\Known 右上角为 $a_0$，第一行和末列的其他元素均为 $1$。反对角线上的其余元素从 $a_1$ 到 $a_n$，均非零。\n   321\t\\Try 暂时遮住第一行与末列，$a_1$ 到 $a_n$ 落在什么位置？怎样重排行让它们各自负责消掉第一行的一个 $1$？\n   322\t\\Method 反转第一行以下的行，使左下块成为对角阵。\n   323\t\\NextHint 若下方的对角元是 $a_i$，第一行减去该行的 $\\frac{1}{a_i}$ 倍。题设的 $a_i\\ne0$ 正好允许这一步。\n   324\t\\Derive 倒排 $n$ 行的逆序数为 $\\frac{n(n-1)}{2}$。倒排后的第 $2$ 至 $n+1$ 行，前 $n$ 列构成对角阵 $\\operatorname{diag}(a_n,\\ldots,a_1)$。第一行从这些行分别减去对应的 $\\frac{1}{a_i}$ 倍，最后一项变成 $a_0-\\sum_{i=1}^n\\frac{1}{a_i}$。按第一行末项展开的符号是 $(-1)^n$。合并两次符号得\n   325\t\\[\n   326\tD_{n+1}=(-1)^{\\frac{n(n+1)}{2}}\\,a_1a_2\\cdots a_n\n   327\t\\left(a_0-\\sum_{i=1}^n\\frac{1}{a_i}\\right).\n   328\t\\]\n   329\t\\Verify 取 $n=2$ 检验，三阶原式可直接展开为 $a_1+a_2-a_0a_1a_2$，与公式一致。\n   330\t\n   331\t\\Question{16}{解答题}{10}{1660}{***}\n   551\t\\Solution\n   552\t\\Known 求四阶行列式，四行按 $0,a,b,a$ 的循环结构排列。\n   553\t\\Try 每行的和一样。用题中矩阵乘 $(1,1,1,1)^{\\mathrm T}$，结果与原向量有什么关系？再试令第 $1,3$ 个分量互为相反数，其余分量为 $0$。\n   554\t\\Method 把位置分成 $(1,3)$ 和 $(2,4)$ 两对。先令每对内部相等，试试两对之间同号和反号各会得到什么。\n   555\t\\NextHint 再试一对内部异号、另一对全零。四个向量应各自被乘上一个标量。\n   556\t\\Derive 设 $M$ 是题给矩阵，取 $S$ 的列依次为 $(1,1,1,1)^{\\mathrm T},(1,-1,1,-1)^{\\mathrm T},(1,0,-1,0)^{\\mathrm T},(0,1,0,-1)^{\\mathrm T}$。分别直接相乘得\n   557\t\\[\n   558\tMS=S\\operatorname{diag}(2a+b,b-2a,-b,-b).\n   559\t\\]\n   560\t前两列在第 $1,3$ 个分量上相等，在第 $2,4$ 个分量上也相等；后两列分别在这两对分量上相反。若四列线性组合为零，先做分量差可知后两系数为零，再做分量和可知前两系数也为零，因此 $|S|\\ne0$。\n   561\t\\Verify 两侧取行列式并约掉 $|S|$，得 $\\boxed{b^2(b^2-4a^2)}$。令 $a=0$ 时原矩阵恰为两对交换对应的排列矩阵乘 $b$，行列式为 $b^4$。\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/tongji-tex/verify.py\", line 20, in <module>\n    assert not re.search(r\"\\\\(?:tfrac|dfrac)\\b|\\\\frac[^{]\", tex)\n           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^\nAssertionError\n"}}]

## tool · 2026-11-18T12:37:56Z


Script completed
Wall time 0.2 seconds
Output:

{}

## tool · 2026-11-18T12:38:03Z


Script completed
Wall time 1.2 seconds
Output:

[{"status":"fulfilled","value":{"chunk_id":"3c9fe1","wall_time_seconds":1.000304459,"session_id":77741,"original_token_count":36,"output":"note: using only cached resource files\nnote: Running TeX ...\nnote: Rerunning TeX because \"同济线性代数同步测试卷.aux\" changed ...\n"}},{"status":"fulfilled","value":{"chunk_id":"ab7d42","wall_time_seconds":1.001534458,"session_id":97997,"original_token_count":50,"output":"note: reading from standard input; outputs will appear under the base name \"texput\"\nnote: using only cached resource files\nnote: Running TeX ...\nnote: Rerunning TeX because \"texput.aux\" changed ...\n"}}]

## tool · 2026-11-18T12:38:08Z


Script completed
Wall time 0.6 seconds
Output:

[{"status":"fulfilled","value":{"chunk_id":"880d2e","wall_time_seconds":0.000007417,"exit_code":0,"original_token_count":83,"output":"note: Running xdvipdfmx ...\nnote: Writing `.question-bank-work/tongji-tex/ipad/同济线性代数同步测试卷.pdf` (379.943359375 KiB)\nnote: Writing `.question-bank-work/tongji-tex/ipad/同济线性代数同步测试卷.log` (23.1708984375 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}},{"status":"fulfilled","value":{"chunk_id":"769a8e","wall_time_seconds":0.000014417,"exit_code":0,"original_token_count":68,"output":"note: Running xdvipdfmx ...\nnote: Writing `.question-bank-work/tongji-tex/a4/texput.log` (23.0390625 KiB)\nnote: Writing `.question-bank-work/tongji-tex/a4/texput.pdf` (387.8427734375 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}}]
{"chunk_id":"1bb86f","wall_time_seconds":0.441266459,"exit_code":1,"original_token_count":73,"output":"Source comparison passed: 68 question bodies and solutions, 80 choices, four 100-point volumes.\ntexput.pdf 595.28×841.89 bp, 137 pages, 73 bookmarks, minimum writing space 408.4 bp\n同济线性代数同步测试卷.pdf 800×600 bp, 137 pages, 73 bookmarks, minimum writing space 199.7 bp\n"}

## assistant · 2026-11-18T12:38:16Z

四卷 68 道解析已全部改写，两版各 137 页。核对确认每道题仍在原页，下一页就是对应解析。124 项数值复验均通过。

## tool · 2026-11-18T12:38:20Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"556bbf","wall_time_seconds":0.000010584,"exit_code":0,"original_token_count":975,"output":"2:from math import factorial, prod, sqrt\n16:det = np.linalg.det\n17:inv = np.linalg.inv\n18:power = np.linalg.matrix_power\n78:        root = sqrt(a*a-4*b*c)\nreferences/同济线代/同步测试卷/A4:\ntotal 696\n-rw-r--r--  1 oyamahappa  staff  353748 Nov 18 20:21 同济线性代数同步测试卷（A4）.pdf\n\nreferences/同济线代/同步测试卷/iPad:\ntotal 688\n-rw-r--r--  1 oyamahappa  staff  349191 Nov 18 20:21 同济线性代数同步测试卷.pdf\ndiff --git a/memory/plan.md b/memory/plan.md\nindex c36d7f2..5a205fb 100644\n--- a/memory/plan.md\n+++ b/memory/plan.md\n@@ -6,6 +6,8 @@\n \n ## 同济线代同步测试卷\n \n+将四卷 68 道题的解析原位改为引导式写法。逐题设计入手问题和提示，保留已校对题面与完整解答，在复杂推导的关键判断前补充问题。重编原路径的 A4 和 iPad 成品。\n+\n 按两组 HEIC 的文件顺序识别版面。用本机 RapidOCR 生成文字候选，逐题对照源图转写题干、选项、小问和公式，按章节和原卷归组写入本地 Markdown，并附源图定位。核查覆盖范围和 LaTeX 语法。\n \n 将两章四卷的 68 道已核对题面合入一份可独立编译的 TeX，保留原卷题号、分值、选项和小问，标注卷别、照片号及难度。逐题补全入手思路、计算过程和验算。默认编译成 iPad 4:3 横屏，通过版式开关编译 A4。源稿和两版 PDF 随本地题源保存。\ndiff --git a/memory/progress.md b/memory/progress.md\nindex 18184c8..0602538 100644\n--- a/memory/progress.md\n+++ b/memory/progress.md\n@@ -7,6 +7,9 @@\n \n ## 同济线代同步测试卷\n \n+- [ ] 逐题改写行列式 A、B 两卷解析。\n+- [ ] 逐题改写矩阵及其运算 A、B 两卷解析。\n+- [ ] 核对原题和答案，复验关键计算并重编两版 PDF。\n - [x] 找到行列式、矩阵两组共 16 张源图。\n - [x] 已转录四卷 68 题，并逐题对照原图校订。\n - [x] 验证 68 道题、80 个选项、4 个编号小问、16 条原图链接及 264 个 LaTeX 表达式。\ndiff --git a/memory/verify.md b/memory/verify.md\nindex 0005a29..7fa953f 100644\n--- a/memory/verify.md\n+++ b/memory/verify.md\n@@ -6,6 +6,8 @@\n \n ## 同济线代同步测试卷\n \n+引导式改写验收逐题核查可尝试的问题、题目线索、提示与推导顺序，核对题面与选择答案，复验关键计算。编译两版后检查出题页、紧接的解析页、书签、写字留白和警告。\n+\n 核对两组全部源图，按原卷核查题型、题号、选项、小问、矩阵和行列式，标明源图和可见的原卷疑义。用 KaTeX 检查交付 Markdown 中的公式。\n \n 16 张源图均取得 RapidOCR 结果并逐题对照。四卷各有 17 题，均为 5 道选择题、5 道填空题和 7 道解答题，合计每卷 100 分。题序、80 个选项、4 个编号小问和 16 条原图链接通过检查，264 个 LaTeX 表达式通过 KaTeX 渲染。行列式 B 卷第 13 题第三行第三列保留原印刷指数并加注。\n.gitignore:10:/references/\t\"references/\\345\\220\\214\\346\\265\\216\\347\\272\\277\\344\\273\\243/\\345\\220\\214\\346\\255\\245\\346\\265\\213\\350\\257\\225\\345\\215\\267/\\345\\220\\214\\346\\265\\216\\347\\272\\277\\346\\200\\247\\344\\273\\243\\346\\225\\260\\345\\220\\214\\346\\255\\245\\346\\265\\213\\350\\257\\225\\345\\215\\267.tex\"\n.gitignore:10:/references/\t\"references/\\345\\220\\214\\346\\265\\216\\347\\272\\277\\344\\273\\243/\\345\\220\\214\\346\\255\\245\\346\\265\\213\\350\\257\\225\\345\\215\\267/A4/\\345\\220\\214\\346\\265\\216\\347\\272\\277\\346\\200\\247\\344\\273\\243\\346\\225\\260\\345\\220\\214\\346\\255\\245\\346\\265\\213\\350\\257\\225\\345\\215\\267\\357\\274\\210A4\\357\\274\\211.pdf\"\n.gitignore:10:/references/\t\"references/\\345\\220\\214\\346\\265\\216\\347\\272\\277\\344\\273\\243/\\345\\220\\214\\346\\255\\245\\346\\265\\213\\350\\257\\225\\345\\215\\267/iPad/\\345\\220\\214\\346\\265\\216\\347\\272\\277\\346\\200\\247\\344\\273\\243\\346\\225\\260\\345\\220\\214\\346\\255\\245\\346\\265\\213\\350\\257\\225\\345\\215\\267.pdf\"\n2026-11-18 20:38\n"}

## tool · 2026-11-18T12:38:27Z


Script completed
Wall time 0.5 seconds
Output:

{"chunk_id":"27c183","wall_time_seconds":0.377645584,"exit_code":0,"original_token_count":73,"output":"Source comparison passed: 68 question bodies and solutions, 80 choices, four 100-point volumes.\ntexput.pdf 595.28×841.89 bp, 137 pages, 73 bookmarks, minimum writing space 408.4 bp\n同济线性代数同步测试卷.pdf 800×600 bp, 137 pages, 73 bookmarks, minimum writing space 199.7 bp\n"}

## tool · 2026-11-18T12:38:46Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-18T12:38:57Z


Script completed
Wall time 5.6 seconds
Output:

{"chunk_id":"4be43e","wall_time_seconds":0.000011667,"exit_code":0,"original_token_count":65,"output":" docs/CHANGELOG.md  | 10 ++++++++++\n memory/plan.md     |  2 ++\n memory/progress.md |  3 +++\n memory/verify.md   |  2 ++\n 4 files changed, 17 insertions(+)\n[main 8703588] docs: record guided Tongji linear algebra solutions\n 4 files changed, 17 insertions(+)\n"}

## tool · 2026-11-18T12:39:01Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"e079ec","wall_time_seconds":0.045198334,"exit_code":0,"original_token_count":446,"output":"8703588737f43820b678f07974122b7b89aee31b docs: record guided Tongji linear algebra solutions\n\n## [2026-11-18 20:38] 重写同济线性代数同步测试卷解析\n\n- **需求**：用引导式写法重写同济线代同步测试题的解析。\n- **实际结果**：四卷共 68 道解析逐题加入可动手尝试的问题和提示，复杂题补充第二条提示或推导中的判断问题。原位更新 TeX 以及 A4、iPad 两版 PDF。\n- **验证**：核对 68 道题面、80 个选项和 20 道单选答案。124 项数值复验、23 项仓库测试通过。两版各 137 页、73 个书签，逐题检查题解相邻与演算留白，编译无警告。\n- **涉及文件**：`references/同济线代/同步测试卷/`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`docs/CHANGELOG.md`。\n- **Git 提交**：待提交。TeX 与 PDF 随题源保存在本地。\n\n---\n/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/references/同济线代/同步测试卷/iPad/同济线性代数同步测试卷.pdf\n第2 题解析\n已知与目标\n求给定四阶行列式的值。\n先想一步\n先只看第一列的2, 4, 6, 8。怎样用首行把第二行的4 变成0？同样的办法能处理6 和8 吗？\n卡住时看提示\n比较后三个数各是2 的几倍，再从对应行减去第一行的相应倍数。这样的行运算保持行列式的值。第一列化简后，沿它\n展开需要算几个余子式？\n完整推导\n第二、三、四行分别减第一行的2, 3, 4 倍，再按第一列展开，\nD = 2\n\f\f\f\f\f\f\f\f\f\f\n−2\n−1\n−1\n−1\n−3\n−1\n−1\n−1\n−4\n\f\f\f\f\f\f\f\f\f\f\n= 2\n\u0002\n−2(12 −1) + (4 −1) −(1 −3)\n\u0003\n= −34.\n结论与检查\n选D。三阶行列式为−17，因子2 来自第一列的首元；其余选项都不等于2(−17)。\n行列式A 卷\n5\n\n"}

## tool · 2026-11-18T12:39:07Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-18T12:39:16Z


Script completed
Wall time 4.9 seconds
Output:

{"chunk_id":"d04053","wall_time_seconds":1.002676208,"session_id":57865,"original_token_count":29,"output":"[main f57293c] docs: link guided Tongji solutions to their record\n 1 file changed, 1 insertion(+), 1 deletion(-)\n"}

## tool · 2026-11-18T12:39:20Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"8b4eba","wall_time_seconds":0.000016458,"exit_code":0,"original_token_count":23,"output":"To https://github.com/OyamaMeek/codex-question-bank.git\n   6fcf6c4..f57293c  main -> main\n"}
{"chunk_id":"ebd7c7","wall_time_seconds":0.000011,"exit_code":0,"original_token_count":394,"output":"## main...origin/main\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267/A4/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/302\\346\\225\\260\\345\\255\\246\\344\\272\\214\\345\\210\\206\\350\\212\\202\\347\\234\\237\\351\\242\\230\\351\\233\\206/302-question-facsimiles.pdf\"\nf57293c docs: link guided Tongji solutions to their record\n8703588 docs: record guided Tongji linear algebra solutions\n-rw-r--r--  1 oyamahappa  staff   388K Nov 18 20:38 references/同济线代/同步测试卷/A4/同济线性代数同步测试卷（A4）.pdf\n-rw-r--r--  1 oyamahappa  staff   380K Nov 18 20:38 references/同济线代/同步测试卷/iPad/同济线性代数同步测试卷.pdf\n-rw-r--r--  1 oyamahappa  staff    71K Nov 18 20:37 references/同济线代/同步测试卷/同济线性代数同步测试卷.tex\n"}

## assistant · 2026-11-18T12:39:30Z

已把同济线代同步测试卷四卷、共 68 道题的解析改成引导式写法。每题先给一个能动手尝试的问题，卡住时再看提示，最后对照完整推导和验算。

可以先看**行列式 A 卷第 2 题（PDF 第 5 页）**。解析先问：「第一列是 \(2,4,6,8\)。怎样用首行把第二行的 \(4\) 变成 \(0\)？」提示再让你比较后三个数各是 \(2\) 的几倍，并想想化简后沿第一列展开，还需要算几个余子式。

**iPad 4:3 横屏版**

:codex-file-citation{path="/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/references/同济线代/同步测试卷/iPad/同济线性代数同步测试卷.pdf" purpose="output"}

**A4 打印版**

:codex-file-citation{path="/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/references/同济线代/同步测试卷/A4/同济线性代数同步测试卷（A4）.pdf" purpose="output"}

两版各 137 页。已核对题面、选项、单选答案和题解页序，124 项数值复验通过。版式通过 PDF 文本与坐标检查，未做截图检查。
