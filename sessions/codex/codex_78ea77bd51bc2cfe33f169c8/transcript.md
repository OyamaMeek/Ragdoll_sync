# 排查需要重新加载的问题

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/Autovisor

## developer · 2026-11-19T06:47:55Z

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

## developer · 2026-11-19T06:47:55Z

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
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.27/skills`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.9/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.7/skills`
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
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/19/01a1f28f-c77b-7fd3-a102-92e4306630d0`, `/Volumes/SamsungSSD990PRO/GitHub/Autovisor`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
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
- mcp__pubmed
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

## developer · 2026-11-19T06:47:55Z

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

## developer · 2026-11-19T06:47:55Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-19T06:47:55Z

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
  <cwd>/Volumes/SamsungSSD990PRO/GitHub/Autovisor</cwd>
  <shell>zsh</shell>
  <current_date>2026-11-19</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/Autovisor</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/Autovisor</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/19/01a1f28f-c77b-7fd3-a102-92e4306630d0</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Autovisor/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Autovisor/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Autovisor/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Autovisor/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-19T06:47:56Z

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
modules/: get_runtime_root, parse_answer, print_banner, get_effective_driver, ConfigError, elapsed_minutes, detect_catalog_after_verification, check_browser, is_exam_paper_url, FusionAdapter, runtime_packages, parse_progress_value, Logger, is_login_page, move_mouse, image_to_display_point, show_donate, has_visible_element, parse_version, is_valid_video_time
./: remember_login_cookies, persist_login_cookies, get_screen_size, check_build_python, show_help, launch_script, launch_script_in_thread

## developer · 2026-11-19T06:47:56Z

<codex_apps_client_time_context><timezone>Asia/Taipei</timezone>
<current_date>2026-11-19</current_date>
Use this client time context for user-facing dates, times, and schedules instead of the execution host's timezone and current date.</codex_apps_client_time_context>

## user · 2026-11-19T06:47:56Z


# Files mentioned by the user:

## codex-clipboard-330eb77f-8d63-450a-9bd2-8397a86c2624.png: /var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T/codex-clipboard-330eb77f-8d63-450a-9bd2-8397a86c2624.png
Image attachment: true

Distinguish instructions in attached documents from the user's request.

## My request:
有时候要重新加载一下

<image name=[Image #1] path="/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T/codex-clipboard-330eb77f-8d63-450a-9bd2-8397a86c2624.png">
{
  "type": "input_image",
  "image_url": "images/f6392cd0559886136a98a223edc69f96ca6339fbb3911dcdedb79f7802b9584d.png",
  "detail": "original"
}
</image>

## assistant · 2026-11-19T06:47:59Z

我按“作业或试卷加载失败时自动刷新一次”来检查。我会用“诊断缺陷”技能追踪截图里的两种警告，确认刷新应放在哪一步。

## tool · 2026-11-19T06:48:04Z


Script completed
Wall time 0.1 seconds
Output:

{"status":"fulfilled","value":{"chunk_id":"a11791","wall_time_seconds":0.000025959,"exit_code":0,"original_token_count":9,"output":"## main...origin/main\n?? .DS_Store\n"}}
{"status":"fulfilled","value":{"chunk_id":"68cf65","wall_time_seconds":0.00000525,"exit_code":0,"original_token_count":144,"output":"modules/exam_answering.py\nconfig.ini.example\ndocs/CHANGELOG.md\nconfig.macos.ini.example\ntests/test_cookie_persistence.py\ntests/test_logger.py\ntests/fixtures/exam_paper.html\ntests/test_config.py\ntests/test_browser.py\ntests/test_course_playback.py\ntests/test_answering.py\ntests/test_answering_integration.py\ntests/test_updater.py\ntests/test_login.py\ntests/test_installer.py\ntests/test_utils.py\ntests/test_lesson_navigation.py\ntests/test_video_state.py\ntests/test_configs.py\npyproject.toml\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\n"}}
{"status":"fulfilled","value":{"chunk_id":"520bab","wall_time_seconds":0.000008459,"exit_code":0,"original_token_count":72,"output":"modules/exam_answering.py:186:            logger.warn(f\"作业「{identity[0]}」打开或加载失败，请在浏览器检查。\", shift=True)\nmodules/exam_answering.py:224:                    logger.warn(\"题目加载或保存失败，请在浏览器检查当前试卷。\", shift=True)\n"}}
{"status":"fulfilled","value":{"chunk_id":"97a509","wall_time_seconds":0.000009833,"exit_code":0,"original_token_count":2166,"output":"---\nname: diagnosing-bugs\ndescription: Diagnosis loop for hard bugs and performance regressions. Use when the user says \"diagnose\"/\"debug this\", or reports something broken/throwing/failing/slow.\n---\n\n# Diagnosing Bugs\n\nA discipline for hard bugs. Skip phases only when explicitly justified.\n\nWhen exploring the codebase, read `GLOSSARY.md` (if it exists) to get a clear mental model of the relevant modules, and check ADRs in the area you're touching.\n\n## Redact\n\nThis skill has you show commands, outputs and captured artifacts. **Redact every secret first**: write `<REDACTED>` in its place. Build loops against env vars, so the credential stays in the environment rather than in what you show. Captured artifacts carry auth headers: quote only the lines that carry the signal.\n\nIf the redacted output is not enough to diagnose the bug, say so and ask the user.\n\n## Phase 1: Build a feedback loop\n\n**This is the skill.** Everything else is mechanical. If you have a **tight** pass/fail signal for the bug (one that goes red on _this_ bug), you will find the cause; bisection, hypothesis-testing, and instrumentation all just consume it. If you don't have one, no amount of staring at code will save you.\n\nSpend disproportionate effort here. **Be aggressive. Be creative. Refuse to give up.**\n\n### Ways to construct one, in roughly this order\n\n1. **Failing test** at whatever seam reaches the bug: unit, integration, e2e.\n2. **Curl / HTTP script** against a running dev server.\n3. **CLI invocation** with a fixture input, diffing stdout against a known-good snapshot.\n4. **Headless browser script** (Playwright / Puppeteer) that drives the UI and asserts on DOM/console/network.\n5. **Replay a captured trace.** Save a real network request / payload / event log to disk; replay it through the code path in isolation.\n6. **Throwaway harness.** Spin up a minimal subset of the system (one service, mocked deps) that exercises the bug code path with a single function call.\n7. **Property / fuzz loop.** If the bug is \"sometimes wrong output\", run 1000 random inputs and look for the failure mode.\n8. **Bisection harness.** If the bug appeared between two known states (commit, dataset, version), automate \"boot at state X, check, repeat\" so you can `git bisect run` it.\n9. **Differential loop.** Run the same input through old-version vs new-version (or two configs) and diff outputs.\n10. **HITL bash script.** Last resort. If a human must click, drive _them_ with `scripts/hitl-loop.template.sh` so the loop is still structured. Captured output feeds back to you.\n\nBuild the right feedback loop, and the bug is 90% fixed.\n\n### Tighten the loop\n\nTreat the loop as a product. Once you have _a_ loop, **tighten** it:\n\n- Can I make it faster? (Cache setup, skip unrelated init, narrow the test scope.)\n- Can I make the signal sharper? (Assert on the specific symptom, not \"didn't crash\".)\n- Can I make it more deterministic? (Pin time, seed RNG, isolate filesystem, freeze network.)\n\nA 30-second flaky loop is barely better than no loop; a 2-second deterministic one is tight, a debugging superpower.\n\n### Non-deterministic bugs\n\nThe goal is not a clean repro but a **higher reproduction rate**. Loop the trigger 100×, parallelise, add stress, narrow timing windows, inject sleeps. A 50%-flake bug is debuggable; 1% is not, so keep raising the rate until it's debuggable.\n\n### When you genuinely cannot build a loop\n\nStop and say so explicitly. List what you tried. Ask the user for: (a) access to whatever environment reproduces it, (b) a redacted captured artifact (HAR file, log dump, core dump, screen recording with timestamps), or (c) permission to add temporary production instrumentation. Do **not** proceed to hypothesise without a loop.\n\n### Completion criterion: a tight loop that goes red\n\nPhase 1 is done when the loop is **tight** and **red-capable**: you can name **one command** (a script path, a test invocation, a curl) that you have **already run at least once** (show the invocation and its output, redacted), and that is:\n\n- [ ] **Red-capable**: it drives the actual bug code path and asserts the **user's exact symptom**, so it can go red on this bug and green once fixed. Not \"runs without erroring\"; it must be able to _catch this specific bug_.\n- [ ] **Deterministic**: same verdict every run (flaky bugs: a pinned, high reproduction rate, per above).\n- [ ] **Fast**: seconds, not minutes.\n- [ ] **Agent-runnable**: you can run it unattended; a human in the loop only via `scripts/hitl-loop.template.sh`.\n\nIf you catch yourself reading code to build a theory before this command exists, **stop: jumping straight to a hypothesis is the exact failure this skill prevents.** No red-capable command, no Phase 2.\n\n## Phase 2: Reproduce + minimise\n\nRun the loop. Watch it go red as the bug appears.\n\nConfirm:\n\n- [ ] The loop produces the failure mode the **user** described, not a different failure that happens to be nearby. Wrong bug = wrong fix.\n- [ ] The failure is reproducible across multiple runs (or, for non-deterministic bugs, reproducible at a high enough rate to debug against).\n- [ ] You have captured the exact symptom (error message, wrong output, slow timing) so later phases can verify the fix actually addresses it.\n\n### Minimise\n\nOnce it's red, shrink the repro to the **smallest scenario that still goes red**. Cut inputs, callers, config, data, and steps **one at a time**, re-running the loop after each cut, and keep only what's load-bearing for the failure.\n\nWhy bother: a minimal repro shrinks the hypothesis space in Phase 3 (fewer moving parts left to suspect) and becomes the clean regression test in Phase 5.\n\nDone when **every remaining element is load-bearing**: removing any one of them makes the loop go green.\n\nDo not proceed until you have reproduced **and** minimised.\n\n## Phase 3: Hypothesise\n\nGenerate **3–5 ranked hypotheses** before testing any of them. Single-hypothesis generation anchors on the first plausible idea.\n\nEach hypothesis must be **falsifiable**: state the prediction it makes.\n\n> Format: \"If <X> is the cause, then <changing Y> will make the bug disappear / <changing Z> will make it worse.\"\n\nIf you cannot state the prediction, the hypothesis is a vibe: discard or sharpen it.\n\n**Show the ranked list to the user before testing.** They often have domain knowledge that re-ranks instantly (\"we just deployed a change to #3\"), or know hypotheses they've already ruled out. Cheap checkpoint, big time saver. Don't block on it; proceed with your ranking if the user is AFK.\n\n## Phase 4: Instrument\n\nEach probe must map to a specific prediction from Phase 3. **Change one variable at a time.**\n\nTool preference:\n\n1. **Debugger / REPL inspection** if the env supports it. One breakpoint beats ten logs.\n2. **Targeted logs** at the boundaries that distinguish hypotheses.\n3. Never \"log everything and grep\".\n\n**Tag every debug log** with a unique prefix, e.g. `[DEBUG-a4f2]`. Cleanup at the end becomes a single grep. Untagged logs survive; tagged logs die.\n\n**Perf branch.** For performance regressions, logs are usually wrong. Instead: establish a baseline measurement (timing harness, `performance.now()`, profiler, query plan), then bisect. Measure first, fix second.\n\n## Phase 5: Fix + regression test\n\nWrite the regression test **before the fix**, but only if there is a **correct seam** for it.\n\nA correct seam is one where the test exercises the **real bug pattern** as it occurs at the call site. If the only available seam is too shallow (single-caller test when the bug needs multiple callers, unit test that can't replicate the chain that triggered the bug), a regression test there gives false confidence.\n\n**If no correct seam exists, that itself is the finding.** Note it. The codebase architecture is preventing the bug from being locked down. Flag this for the next phase.\n\nIf a correct seam exists:\n\n1. Turn the minimised repro into a failing test at that seam.\n2. Watch it fail. If you forced the red by mutating code or a fixture, `diff` against a pristine copy to prove the mutation landed before you trust it.\n3. Apply the fix.\n4. Watch it pass.\n5. Re-run the Phase 1 feedback loop against the original (un-minimised) scenario.\n\n## Phase 6: Cleanup\n\nRequired before declaring done:\n\n- [ ] Original repro no longer reproduces (re-run the Phase 1 loop)\n- [ ] Regression test passes (or absence of seam is documented)\n- [ ] All `[DEBUG-...]` instrumentation removed (`grep` the prefix)\n- [ ] Throwaway prototypes deleted (or moved to a clearly-marked debug location)\n- [ ] The hypothesis that turned out correct is stated in the commit / PR message, so the next debugger learns\n"}}

## developer · 2026-11-19T06:48:04Z

<tools>
Added deferred tool namespaces:
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__ot
</tools>

## tool · 2026-11-19T06:48:10Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 13274)
Total output lines: 1001

# 当前环境

- Python 3.13、uv、Playwright；现有测试使用 unittest。
- 本次使用 ponytail 技能；不使用子代理，不进行截图或视觉检查。
- 答题改用 DeepSeek Chat Completions API，复用项目已有的 httpx 异步客户端，模型为 `deepseek-flash`。
- 作业考试模式通过 Playwright 操作浏览器原生控件，通过 Chromium 无障碍树读取当前题干的可访问文本。
- 学号登录复用 Python `Config`、Playwright 和 Tk 图形配置工具，使用学校下拉列表和智慧树登录表单。
# 智慧树作业考试答题

- `--answer-exam` 复用登录、浏览器和 DeepSeek 配置，监听当前浏览器会话中从在线学堂打开的作业列表、作业、测验和考试页面。
- 依据智慧树公开前端的 `dohomework`、`doexamination` 和答题控件适配文本单选、多选、判断题。适配从当前题顺序保存，识别已有选择，交卷由用户操作。
- 复用 `ask_deepseek` 和编号校验。应用答案前重新检查试卷、题目和选项，题目变化、验证弹窗、无效响应或保存失败时交由用户处理。保留图片与主观题供人工检查。
- 使用真实 Chrome 与本地 HTTP 验证同页和新标签页、题目变化以及保存行为，更新启动说明和开发记录后提交推送。

# 智慧树学号登录

- 在 `[user-account]` 新增可选 `school`。填写学校全称时，`username` 填学号。学校留空时，`username` 继续填写手机号。旧配置默认学校为空。
- 复用现有自动登录和 Cookie 流程。学号分支打开学号标签，搜索并精确选择学校后填写账号密码。控件或学校找不到时保留浏览器供手动登录。
- Windows 和 macOS 配置示例、Tk 图形界面以及 README 提供配置入口和说明。

## 课程默认设置

- 通用和 macOS 模板、配置加载器及图形配置工具统一使用不限时、1.5 倍速、静音的默认值。用户在配置文件中显式填写的值优先。

## 作业考试启动超时

- 在在线学堂导航提交后开始监听试卷。导航超时时提示在当前标签页手动打开在线学堂，并继续监听。
- 读取课程配置时跳过空白网址，有内容的无效网址继续提示。

## 作业答完后暂存

- 复用末题保存流程。页面显示答题完成且提供「暂存作业」时，打开暂存确认框，核对提示并点击「确定」。交卷由用户操作。
- 使用真实 Chrome 和本地作业页面验证确认暂存、未答完时的处理及答题页关闭行为，再更新使用说明。

## 自动打开未提交作业

- 用户选择课程并进入「未提交」列表后，复用该页的作业入口逐份打开并交由现有答题监听器处理。用卡片类型限定作业范围，按作业身份去重，等本份处理后再继续。
- 以公开前端确认列表控件和弹窗行为，用本地 Chrome 回归测试验证调度、去重及与手动交卷流程的衔接。

## DeepSeek 答案本地记录

- 在三种答题流程共用的 `ask_deepseek` 中，将校验通过的答案连同时间、题目和选项追加到运行目录下的 `.autovisor/deepseek-answers.md`。写入失败时提示并返回已校验的答案。
# 当前任务

- [x] 核对公开前端的作业和考试路由、题目结构、同页或新标签页打开方式，以及翻页和最终保存控件。
- [x] 回归用例在实现前因缺少作业考试适配模块失败。
- [x] 接入作业考试浏览器模式、答题和保存流程，更新各平台启动方式。
- [x] 全量测试 119 项，116 项通过、3 项跳过。已验证空白 Key 退出和 Chrome 同页、新标签页答题保存。正式试卷未参与测试。
- [x] 功能提交 `ecaac6c` 已推送 `origin/main`，开发记录已补记提交哈希。

## 智慧树学号登录

- [x] 核对旧登录地址的跳转及新版学号表单。
- [x] Chrome 回归测试确认旧代码把学号提交到了手机号字段。
- [x] 接入配置、自动登录和图形入口，更新用户说明。
- [x] 验证线上公开学号表单、真实 Chrome 本地提交和 Tk 配置保存。全量测试 120 项，117 项通过、3 项跳过。
- [x] 学号登录提交 `75e798f` 已推送 `origin/main`，开发记录已补记提交哈希。

## 课程默认设置

- [x] 核对模板、配置加载器及图形配置工具。本机 macOS 配置已符合目标。
- [x] 统一默认值并验证两份模板、缺少字段和显式配置的读取，以及图形工具的初始值。
- [x] 全量测试 122 项，119 项通过、3 项跳过。Python 语法和差异检查通过。
- [x] 配置提交 `a0032c3` 已推送 `origin/main`。

## 作业考试启动超时

- [x] 从 `logs/Log34.txt` 确认登录后等待在线学堂触发 `DOMContentLoaded` 超时。
- [x] 用 Chrome 和配置回归用例复现启动和提示问题。
- [x] 修复导航与空白网址处理。启用 Chrome 的全量测试 123 项，120 项通过、3 项跳过。
- [x] 修复提交 `77a3d27` 已推送 `origin/main`。

## 作业答完后暂存

- [x] 用 Chrome 回归测试复现答完后未暂存。
- [x] 接入暂存确认流程和使用说明。
- [x] 用 Chrome 验证暂存、未完成作业、答题标签页关闭及考试流程，记录验证结果。
- [x] 功能提交 `a9541f8` 已推送 `origin/main`。

## 自动打开未提交作业

- [x] 核对智慧树公开前端的作业类型、「未提交」控件及空白标签页跳转方式。
- [x] 用真实 Chrome 的本地列表复现脚本等待手动打开作业的行为。
- [x] 接入逐份打开、去重和使用说明。全量测试 128 项，125 项通过、3 项跳过，最终版本通过作业列表 Chrome 回归测试。
- [x] 功能提交 `d38bfcf` 已推送至 `origin/main`。

## DeepSeek 答案本地记录

- [x] 核对课中题、融合练习和作业考试的请求入口，以及本地运行目录。
- [x] 用本地 HTTP 回归测试复现缺少 Markdown 记录。
- [x] 实现本地记录并更新使用说明。追加、无效答案处理和写入失败提示均通过验证。
- [x] 启用 Chrome 的全量测试共 130 项，127 项通过、3 项跳过。最终版本的 5 项专项回归全部通过。
- [x] 功能提交 `4e0c684` 已推送至 `origin/main`，开发记录已补记提交哈希。
# 验证标准

- 作业考试模式验证 URL 范围、手动打开试卷、文本客观题、新标签页、已有答案、不可读取的内容、选项变化及翻页保存。真实 Chrome 使用本地试卷页面和 HTTP 测试服务运行。
- CLI 验证 `--answer-exam` 和空白 Key 的错误退出。正式线上试卷的作答与交卷留给用户核对，测试仅使用本地题目。

- 验证旧配置、空白 Key 与已填写 Key；检查无 Key 时保留题目供手动完成。
- 运行答案校验及真实本地 HTTP、Chrome 测试，检查请求格式、单选、多选、认证失败和等待期间题目变化的处理。
- 使用 `AUTOVISOR_TEST_BROWSER=1 uv run python -m unittest discover -s tests -v` 运行测试套件。使用用户提供的有效 Key 时，可单独验证 DeepSeek 服务返回真实答案。
- 运行 `uv lock --check`、`uv run python Autovisor.py --help` 与 `git diff --check`，确认凭证未进入提交。

## 2026-11-19 结果

- 在按锁文件创建的独立环境中运行 114 项测试，111 项通过、3 项跳过。真实 Chrome 和本地 HTTP 覆盖正常作答、融合提交、缺少 Key、认证失败、响应截断与题目变化。
- 真实 Tk 控件在隔离配置目录中通过 Key 的掩码、保存、重读与清空检查。
- 锁文件、CLI 帮助、Python 编译和差异检查均通过。
- 当前环境缺少用户的有效 DeepSeek Key，线上答题验证跳过。另外两项跳过的是 Windows 专用测试。

## 2026-11-19 作业考试验证结果

- 核对智慧树公开的 `stuExamWeb.html` 前端。作业使用 `dohomework`，考试使用 `doexamination`，最后一题的保存和交卷使用独立按钮。
- 全量测试 119 项，116 项通过、3 项跳过。真实 Chrome 结合本地试卷和 HTTP 服务验证同页及弹出标签页、封闭 Shadow DOM 的可访问题干、多选与判断题、已有答案、错误选项数量、等待期间用户勾选以及逐题保存和手动交卷边界。
- CLI 显示 `--answer-exam`，Key 留空时返回退出码 2。Python 编译、Bash 语法、锁文件和差异检查通过。
- 未启动用户的线上试卷。缺少有效 Key，线上 DeepSeek 测试跳过，另外两项为 Windows 专用测试。

## 学号登录验证标准

- 用真实 Chrome 验证智慧树公开登录页的学号标签、学校搜索和选择。使用独立登录测试表单验证配置读取、学号表单提交以及留空学校时的手机号分支。
- 检查 Tk 学校字段的保存、重读和清空。运行全量浏览器测试、锁文件检查和 `git diff --check`。
- 线上登录结果需要有效的学号和密码，本次验证限于公开表单及本地提交行为。

### 2026-11-19 学号登录验证结果

- 真实 Chrome 结合智慧树公开登录页确认学号标签、学校搜索和精确选择、账号密码输入控件和协议复选框。未使用真实账号或提交线上登录。
- 真实 Chrome 本地表单确认提交学号和精确匹配的学校，保留前导零。无 `school` 字段的旧配置提交手机号。
- Tk 控件通过学校保存、重读和清空检查。完整测试 120 项，117 项通过、3 项跳过。CLI 帮助、锁文件和差异检查通过。

## 课程默认设置验证

- 用 `Config` 读取两个模板及缺少课程字段的配置，确认不限时、1.5 倍速和静音，并验证显式配置的优先级。
- 使用实际 Tk 控件验证未配置和显式配置时的初始值，运行测试套件、Python 语法和差异检查。
- 配置回归测试在修改前复现旧默认值，修改后通过。实际 Tk 控件验证了预填默认值和读取显式配置。
- 启用 Chrome 的测试套件共 122 项，119 项通过，线上 DeepSeek 和两项 Windows 专用用例跳过。Python 语法和差异检查通过。

## 作业考试启动超时验证

- 用真实 Chrome 验证在线学堂页面 `DOMContentLoaded` 延迟时能处理从该页打开的试卷，导航超时后能在同一个标签页手动打开试卷。
- 用实际配置文件验证空值跳过、有内容的无效网址仍提示，运行启用 Chrome 的测试套件及差异检查。
- 修改前，真实 Chrome 复现 `Page.goto` 等待 30 秒后抛出超时，页面脚本阻塞时也错过试卷弹窗。配置回归复现空白网址的错误提示。
- 修改后，启用 Chrome 的全量测试共 123 项，120 项通过。线上 DeepSeek 与两项 Windows 专用用例跳过。Python 编译、CLI 帮助、启动脚本语法、锁文件和差异检查通过。未使用真实账号或线上试卷。

## 作业暂存验证

- 用真实 Chrome 的本地作业验证末题保存后，完成率为 100% 时点击暂存及其确认按钮。用未完成的作业和考试页面覆盖手动处理及交卷行为。
- 运行启用 Chrome 的全量测试、CLI 帮助和差异检查。
- 修改前，Chrome 回归测试复现末题保存后未暂存。修改后，四项暂存回归用例通过，覆盖末题自动作答与已有选项、未答完保留页面，以及确认后关闭标签页。
- 全量测试 127 项，124 项通过。线上 DeepSeek 与两项 Windows 专用测试跳过。Python 编译、CLI 帮助和差异检查通过。暂存行为使用本地作业页面验证。

## 自动打开作业验证

- 用真实 Chrome 的本地列表检验可答的未提交作业逐份打开并进入原有暂存流程，保留考试和手动打开试卷的现有行为。确认列表更新后避免重复打开，运行全量浏览器测试和差异检查。
- 修改前复现列表需要手动打开作业。修改后用真实 Chrome 和本地页面验证空白弹窗跳转、同名作业区分、逐份暂存、列表重建去重，以及考试入口和未激活的列表均未触发自动打开。
- 全量测试 128 项，125 项通过。线上 DeepSeek 与两项 Windows 专用用例跳过。最终版本的作业列表回归、Python 编译、CLI 帮助和差异检查通过。没有在登录后的真实作业列表中试跑。

## DeepSeek 答案本地记录验证

- 用本地 HTTP 服务和真实文件验证两次有效响应依次追加、中文内容与多选答案完整、API Key 未写入、无效响应不变更文件、写入失败时提示且仍返回有效选项。运行启用 Chrome 的全量测试和差异检查。
- 启用 Chrome 的全量测试共 130 项，127 项通过，线上 DeepSeek 和两项 Windows 专用用例跳过。最终版本通过 5 项专项回归，覆盖本地 Markdown、普通课中题、融合练习和作业考试。Python 编译、CLI 帮助和差异检查通过。
# 注意事项

- DeepSeek JSON 输出可能为空，截断的响应也可能带有选项编号。只有正常结束且通过编号校验的答案才能用于点击和提交。
- `enableAutoCaptcha` 控制登录滑块。自动答题从 `[deepseek]` 读取用户填写的 `api_key`。

import asyncio
import json
from collections import Counter
from unicodedata import category
from urllib.parse import urlsplit

from playwright.async_api import CDPSession, Error as PlaywrightError, Page

from modules.answering import AnswerError, ask_deepseek
from modules.logger import Logger
from modules.tasks import has_visible_verification

logger = Logger()
QUESTION = ".examPaper_box .examPaper_subject"
ANCHOR = "> .subject_stem .subject_num [id^='anchor_']"
STEM = "> .subject_stem .subject_describe"
KIND = "> .subject_stem .subject_type > span:first-child"
CHOICES = ".subject_node .nodeLab:visible"
OPTION_TEXT = ".node_detail"
CHECKED = ".subject_node input:checked"
MEDIA = "img:visible, canvas:visible, video:visible, audio:visible"


def is_exam_paper_url(url: str) -> bool:
    parsed = urlsplit(url)
    route = parsed.fragment.split("?", 1)[0].split("/")
    return (
        parsed.scheme == "https"
        and parsed.netloc == "onlineexamh5new.zhihuishu.com"
        and parsed.path == "/stuExamWeb.html"
        and route[:2] == ["", "webExamList"]
        and ((len(route) == 9 and route[2] == "dohomework") or (len(route) == 8 and route[2] == "doexamination"))
        and all(route[3:])
    )


async def _read_stem(cdp: CDPSession, selector: str) -> str:
    # 普通 DOM Locator 读不到封闭 Shadow DOM，题干也可通过浏览器无障碍树读取。
    document = await cdp.send("DOM.getDocument", {"depth": 0})
    node = await cdp.send("DOM.querySelector", {"nodeId": document["root"]["nodeId"], "selector": selector})
    if not node["nodeId"]:
        return ""
    tree = await cdp.send("Accessibility.queryAXTree", {"nodeId": node["nodeId"]})
    displayed = [item for item in tree["nodes"] if not item["ignored"]]
    if any(item["role"]["value"] in {"image", "Canvas", "Video", "Audio"} for item in displayed):
        return ""
    return " ".join(
        item["name"]["value"] for item in displayed if item["role"]["value"] == "StaticText"
    ).strip()


async def _fill_current_question(page: Page, cdp: CDPSession, selector: str, api_key: str) -> tuple[int, int]:
    url = page.url
    question = page.locator(f"{selector}:visible")
    if await question.locator(CHECKED).count():
        return 0, 0
    kind = (await question.locator(KIND).inner_text(timeout=2500)).strip("【】 \r\n")
    if kind not in {"单选题", "多选题", "判断题"}:
        return 0, 1
    choices = question.locator(CHOICES)
    content = choices.locator(OPTION_TEXT)
    options = [text.strip() for text in await content.all_inner_texts()]
    stem = await _read_stem(cdp, f"{selector} {STEM}")
    if (
        not stem or len(options) < 2 or len(options) != await choices.count()
        or any(not option for option in options)
        or any(category(char) == "Co" for char in stem + "".join(options))
        or await question.locator(STEM).locator(MEDIA).count()
        or await content.locator(MEDIA).count()
    ):
        return 0, 1

    answers = await ask_deepseek(f"{kind}：{stem}", options, api_key)
    if kind != "多选题" and len(answers) != 1:
        raise AnswerError("单选题和判断题只允许填写一个选项")
    if (
        page.url != url or not await question.is_visible() or await question.locator(CHECKED).count()
        or [text.strip() for text in await content.all_inner_texts()] != options
        or await _read_stem(cdp, f"{selector} {STEM}") != stem
    ):
        raise AnswerError("等待 DeepSeek 期间题目或选择已变化")
    if await has_visible_verification(page):
        raise AnswerError("检测到平台验证，请在浏览器手动处理")
    for index in answers:
        choice = choices.nth(index)
        await choice.click(timeout=2500)
        await choice.locator("input:checked").wait_for(state="attached", timeout=2500)
    selected = await choices.evaluate_all(
        "rows => rows.flatMap((row, index) => row.querySelector('input:checked') ? [index] : [])"
    )
    if selected != sorted(answers):
        raise AnswerError("页面选中状态与返回的答案不一致")
    return 1, 0


async def fill_exam(page: Page, api_key: str) -> tuple[int, int]:
    url = page.url
    if not is_exam_paper_url(url):
        raise AnswerError("当前页面不是受支持的作业考试答题页")
    if not api_key:
        raise AnswerError("请在配置文件的 [deepseek] 中填写 api_key")

    visible_anchor = page.locator(f"{QUESTION}:visible {ANCHOR}:visible")
    controls = page.locator(".examPaper_box .switch-btn-box:visible")
    next_button = controls.get_by_role("button", name="下一题", exact=True)
    save_button = controls.get_by_role("button", name="保存", exact=True)
    stash_button = page.get_by_role("button", name="暂存作业", exact=True)
    filled = skipped = 0
    cdp = await page.context.new_cdp_session(page)
    try:
        while page.url == url:
            if await has_visible_verification(page):
                raise AnswerError("检测到平台验证，请在浏览器手动处理")
            anchor = await visible_anchor.get_attribute("id", timeout=10000)
            selector = f"{QUESTION}:has({ANCHOR}[id={json.dumps(anchor, ensure_ascii=False)}])"
            result, needs_manual = await _fill_current_question(page, cdp, selector, api_key)
            filled += result
            skipped += needs_manual
            if page.url != url or not await page.locator(f"{selector}:visible").is_visible():
                raise AnswerError("当前题目已变化，已暂停答题")
            if await has_visible_verification(page):
                raise AnswerError("检测到平台验证，请在浏览器手动处理")
            if not await next_button.is_visible():
                can_stash = await stash_button.is_visible()
                if result or (can_stash and not needs_manual):
                    await save_button.click(timeout=2500)
                    await page.get_by_text("保存成功！", exact=True).wait_for(timeout=10000)
                completion = page.locator(".percentage_tit:visible").get_by_text("100%", exact=True)
                if can_stash and await completion.is_visible():
                    await stash_button.click(timeout=2500)
                    dialog = page.locator(".el-message-box:visible").filter(
                        has=page.get_by_text("你确定要暂存作业吗", exact=True)
                    )
                    await dialog.wait_for(timeout=10000)
                    if page.url != url or await has_visible_verification(page):
                        raise AnswerError("检测到页面变化或平台验证，已暂停暂存")
                    await dialog.get_by_role("button", name="确定", exact=True).cl…3274 tokens truncated…await asyncio.wait_for(completed.wait(), timeout=10)
            self.assertEqual(await self.page.locator("body").get_attribute("data-answer"), "2")
            self.assertFalse(await self.page.locator(".el-dialog").is_visible())
            path, authorization, request = self.server.request
            self.assertEqual(path, "/chat/completions")
            self.assertEqual(authorization, "Bearer key-for-test")
            self.assertEqual(request["model"], "deepseek-flash")
            self.assertEqual(request["response_format"], {"type": "json_object"})
            question = json.loads(request["messages"][1]["content"])
            self.assertIn("1 + 1", question["question"])
            self.assertEqual(question["options"], ["3", "2", "5"])
        finally:
            task.cancel()
            with contextlib.suppress(asyncio.CancelledError):
                await task

    async def test_fusion_multiple_answers_are_selected_before_submit(self):
        self.set_answers([2, 4])
        await self.page.set_content('''
            <div class="ai-class-exercise-dialog">
                <p>多选题：选择所有质数。</p>
                <label class="option"><input type="checkbox" value="1">4</label>
                <label class="option"><input type="checkbox" value="2">2</label>
                <label class="option"><input type="checkbox" value="3">9</label>
                <label class="option"><input type="checkbox" value="4">3</label>
                <div class="el-dialog__footer"><button class="el-button"
                    onclick="this.closest('.ai-class-exercise-dialog').hidden=true">提交</button></div>
            </div>
        ''')
        self.assertTrue(await asyncio.wait_for(FusionAdapter.skip_ai_exercise(self.page, "key-for-test"), timeout=10))
        self.assertEqual(
            await self.page.locator("input:checked").evaluate_all("els => els.map(el => el.value)"),
            ["2", "4"],
        )
        self.assertFalse(await self.page.locator(".ai-class-exercise-dialog").is_visible())

    async def test_changed_question_does_not_receive_stale_answer(self):
        self.set_answers([1])
        self.server.reply_ready.clear()
        await self.page.set_content('''
            <div id="question"><p>单选题：1 + 1 等于多少？</p>
                <button class="option" onclick="this.dataset.clicked='yes'">2</button>
                <button class="option" onclick="this.dataset.clicked='yes'">3</button>
            </div>
        ''')
        task = asyncio.create_task(answer_question(self.page.locator("#question"), ".option", "key-for-test"))
        try:
            self.assertTrue(await asyncio.to_thread(self.server.request_received.wait, 5))
            await self.page.locator("p").evaluate("el => el.textContent = '新的题目'")
            self.server.reply_ready.set()
            with self.assertRaisesRegex(AnswerError, "题目已变化"):
                await asyncio.wait_for(task, timeout=5)
            self.assertEqual(await self.page.locator("[data-clicked]").count(), 0)
        finally:
            if not task.done():
                task.cancel()
                with contextlib.suppress(asyncio.CancelledError):
                    await task

    async def _serve_exam(self, route="dohomework", query=""):
        base_url = "https://onlineexamh5new.zhihuishu.com/stuExamWeb.html"
        exam = Path(__file__).with_name("fixtures") / "exam_paper.html"
        await self.page.context.route(base_url + "*", lambda request_route: request_route.fulfill(path=exam))
        params = "recruit/work/exam/course/school" + ("/0" if route == "dohomework" else "")
        return f"{base_url}{query}#/webExamList/{route}/{params}"

    def _start_exam_mode(self):
        session = BrowserSession(self.browser, self.page.context, self.page, attached=True)
        config = SimpleNamespace(attach_existing_chrome=True, deepseek_api_key="key-for-test")

        async def run():
            with patch("Autovisor.create_browser_session", return_value=session), patch(
                "Autovisor.logger", Logger(), create=True
            ):
                await run_exam_mode(config)

        return asyncio.create_task(run())

    async def test_unsubmitted_homework_opens_once_in_order_after_list_refresh(self):
        self.set_answers([2])
        first = await self._serve_exam(query="?kind=single")
        second = first.replace("/work/", "/work-two/")
        list_url = "https://onlineexamh5new.zhihuishu.com/stuExamWeb.html#/webExamList?recruitId=recruit"
        await self.page.route("**/stuExamWeb.html", lambda route: route.fulfill(
            content_type="text/html; charset=utf-8",
            body=f'''
                <li id="examStateTabWsj">未提交</li>
                <ul id="work">
                    <li><div class="examItemWrap">
                        <span class="percentage_number">作业</span>
                        <div class="examTit"><span class="name">单元测试</span></div>
                        <ul class="examInfoList"><li>对应章节 第二章</li></ul>
                        <a title="开始答题"><span class="themeBg" onclick="openWork(1)">开始答题</span></a>
                    </div></li>
                    <li><div class="examItemWrap">
                        <span class="percentage_number">作业</span>
                        <div class="examTit"><span class="name">单元测试</span></div>
                        <ul class="examInfoList"><li>对应章节 第三章</li></ul>
                        <a title="开始答题"><span class="themeBg" onclick="openWork(2)">开始答题</span></a>
                    </div></li>
                    <li><div class="examItemWrap">
                        <span class="percentage_number">考试</span>
                        <a title="开始答题"><span class="themeBg" onclick="opened.push('exam')">开始答题</span></a>
                    </div></li>
                </ul>
                <script>
                    const urls = {json.dumps([first, second])};
                    const opened = [];
                    const stashed = [];
                    addEventListener('message', event => {{
                        if (event.origin === location.origin && event.data.stashed) {{
                            stashed.push(event.data);
                            work.innerHTML = work.innerHTML;
                        }}
                    }});
                    function openWork(index) {{
                        opened.push([index, stashed.length]);
                        const paper = window.open();
                        setTimeout(() => {{ paper.location.href = urls[index - 1]; }}, 200);
                    }}
                </script>
            ''',
        ))
        await self.page.goto(list_url)
        task = asyncio.create_task(watch_exam_pages(self.page, "key-for-test"))
        try:
            await asyncio.sleep(0.6)
            self.assertEqual(await self.page.evaluate("opened"), [])
            await self.page.locator("#examStateTabWsj").evaluate("tab => tab.classList.add('cur')")
            try:
                await self.page.wait_for_function("opened.length >= 2", timeout=7000)
            except TimeoutError:
                self.fail("脚本没有逐份打开未提交的作业")
            await self.page.wait_for_function("stashed.length === 2", timeout=7000)
            self.assertEqual(await self.page.evaluate("stashed"), [
                {"paper": "#/webExamList/dohomework/recruit/work/exam/course/school/0", "stashed": "2", "submitted": None},
                {"paper": "#/webExamList/dohomework/recruit/work-two/exam/course/school/0", "stashed": "2", "submitted": None},
            ])
            await asyncio.sleep(0.6)
            self.assertEqual(await self.page.evaluate("opened"), [[1, 0], [2, 1]])
        finally:
            task.cancel()
            with contextlib.suppress(asyncio.CancelledError):
                await task

    async def test_exam_waits_for_manually_opened_paper_and_saves_without_submitting(self):
        url = await self._serve_exam()
        statements = []

        def reply(request):
            data = json.loads(request["messages"][1]["content"])
            statements.append(data["question"])
            answers = [1, 3] if "质数" in data["question"] and "多选题" in data["question"] else [2]
            return {"choices": [{"finish_reason": "stop", "message": {"content": json.dumps({"answers": answers})}}]}

        self.server.reply = reply
        campus_url = "https://onlineweb.zhihuishu.com/onlinestuh5"
        script_release = asyncio.Event()

        async def hold_script(route):
            await script_release.wait()
            await route.fulfill(body="")

        await self.page.route(campus_url + "/slow.js", hold_script)
        await self.page.route(campus_url, lambda route: route.fulfill(
            content_type="text/html; charset=utf-8",
            body=f'<button onclick="window.open(\'{url}\')">开始答题</button>'
                 f'<script src="{campus_url}/slow.js"></script>',
        ))
        task = self._start_exam_mode()
        try:
            start_button = self.page.get_by_role("button", name="开始答题")
            await start_button.wait_for(timeout=5000)
            self.assertEqual(await self.page.evaluate("document.readyState"), "loading")
            self.assertFalse(self.server.request_received.is_set())
            async with self.page.expect_popup(timeout=5000) as popup:
                await start_button.click()
            paper = await popup.value
            await paper.get_by_text("保存成功！", exact=True).wait_for(timeout=12000)
            body = paper.locator("body")
            self.assertEqual(await body.get_attribute("data-saved0"), "1")
            self.assertEqual(await body.get_attribute("data-saved1"), "1,3")
            self.assertEqual(await body.get_attribute("data-saved2"), "")
            self.assertEqual(await body.get_attribute("data-saved3"), "2")
            self.assertIsNone(await body.get_attribute("data-submitted"))
            self.assertEqual(len(statements), 2)
            self.assertIn("选择所有质数", statements[0])
            self.assertIn("九是质数", statements[1])
        finally:
            script_release.set()
            await self.page.unroute_all(behavior="wait")
            task.cancel()
            with contextlib.suppress(asyncio.CancelledError):
                await task

    async def test_completed_homework_confirms_stash_after_saving_last_answer(self):
        self.set_answers([2])
        url = await self._serve_exam(query="?kind=single")
        await self.page.goto(url)

        self.assertEqual(await fill_exam(self.page, "key-for-test"), (1, 0))

        body = self.page.locator("body")
        self.assertEqual(await body.get_attribute("data-saved0"), "2")
        self.assertEqual(await body.get_attribute("data-stashed"), "2")
        self.assertIsNone(await body.get_attribute("data-submitted"))

    async def test_homework_saves_existing_selection_on_last_question_before_stashing(self):
        await self.page.goto(await self._serve_exam(query="?kind=single"))
        await self.page.get_by_text("3", exact=True).click()

        self.assertEqual(await fill_exam(self.page, "key-for-test"), (0, 0))

        self.assertEqual(await self.page.locator("body").get_attribute("data-stashed"), "1")
        self.assertFalse(self.server.request_received.is_set())

    async def test_incomplete_homework_remains_open_for_manual_review(self):
        self.set_answers([2])
        await self.page.goto(await self._serve_exam())

        self.assertEqual(await fill_exam(self.page, "key-for-test"), (2, 1))

        self.assertIsNone(await self.page.locator("body").get_attribute("data-stashed"))
        self.assertFalse(await self.page.get_by_role("dialog").is_visible())

    async def test_homework_tab_can_close_after_stash_confirmation(self):
        self.set_answers([2])
        url = await self._serve_exam(query="?kind=single")
        async with self.page.expect_popup() as popup:
            await self.page.evaluate("url => { window.open(url); }", url)
        paper = await popup.value
        await paper.wait_for_url(url)

        async with paper.expect_event("close", timeout=5000):
            self.assertEqual(await fill_exam(paper, "key-for-test"), (1, 0))

    async def test_exam_mode_tracks_paper_in_same_tab_after_campus_timeout(self):
        self.set_answers([2])
        url = await self._serve_exam("doexamination", "?kind=single")
        request_started = asyncio.Event()
        request_release = asyncio.Event()

        async def hold_campus(route):
            request_started.set()
            await request_release.wait()
            await route.abort()

        await self.page.route("https://onlineweb.zhihuishu.com/onlinestuh5", hold_campus)
        task = self._start_exam_mode()
        try:
            await asyncio.wait_for(request_started.wait(), timeout=5)
            done, _ = await asyncio.wait({task}, timeout=31)
            if done:
                await task
                self.fail("在线学堂导航超时后停止了试卷监听")
            await self.page.goto(url)
            await self.page.get_by_text("保存成功！", exact=True).wait_for(timeout=10000)
            self.assertEqual(await self.page.locator("body").get_attribute("data-saved0"), "2")
            self.assertIsNone(await self.page.locator("body").get_attribute("data-submitted"))
        finally:
            if not self.page.is_closed():
                await self.page.unroute_all(behavior="ignoreErrors")
            request_release.set()
            task.cancel()
            with contextlib.suppress(asyncio.CancelledError):
                await task

    async def test_exam_rejects_multiple_answers_on_single_choice(self):
        self.set_answers([1, 2])
        url = await self._serve_exam("doexamination", "?kind=single")
        await self.page.goto(url)
        with self.assertRaisesRegex(AnswerError, "单选"):
            await fill_exam(self.page, "key-for-test")
        self.assertEqual(await self.page.locator("input:checked").count(), 0)
        self.assertIsNone(await self.page.locator("body").get_attribute("data-saved0"))

    async def test_exam_keeps_selection_made_by_user_during_request(self):
        self.set_answers([2])
        self.server.reply_ready.clear()
        url = await self._serve_exam("doexamination", "?kind=single")
        await self.page.goto(url)
        task = asyncio.create_task(fill_exam(self.page, "key-for-test"))
        try:
            self.assertTrue(await asyncio.to_thread(self.server.request_received.wait, 5))
            await self.page.locator(".nodeLab").first.click()
            self.server.reply_ready.set()
            with self.assertRaisesRegex(AnswerError, "已变化"):
                await asyncio.wait_for(task, timeout=5)
            self.assertEqual(await self.page.locator("input:checked").input_value(), "1")
            self.assertIsNone(await self.page.locator("body").get_attribute("data-saved0"))
        finally:
            if not task.done():
                task.cancel()
                with contextlib.suppress(asyncio.CancelledError):
                    await task

[build-system]
requires = ["setuptools>=68"]
build-backend = "setuptools.build_meta"

[project]
name = "autovisor"
dynamic = ["version"]
description = "智慧树课程自动化工具"
readme = "README.md"
requires-python = ">=3.10,<3.14"
dependencies = [
    "httpx>=0.28,<1",
    "pillow>=10,<13",
    "playwright>=1.49,<2",
    "pygetwindow>=0.0.9; platform_system == 'Windows'",
    "requests>=2.31,<3",
]

[project.optional-dependencies]
captcha = [
    "numpy>=2,<3",
    "opencv-python>=4.10,<5",
]
gui = [
    "sv-ttk>=2.6,<3",
]

[tool.uv]
package = false

[tool.setuptools.dynamic]
version = { attr = "modules.version.__version__" }

[tool.setuptools]
py-modules = []
tests/test_answering_integration.py:16:from Autovisor import run_exam_mode
tests/test_answering_integration.py:19:from modules.exam_answering import fill_exam, watch_exam_pages
tests/test_answering_integration.py:260:                await run_exam_mode(config)
tests/test_answering.py:5:from modules.exam_answering import is_exam_paper_url
.
..
.DS_Store
.autovisor
.git
.github
.gitignore
.python-version
.venv
Autovisor.py
GUI.py
LICENSE
README.md
__pycache__
autovisor.egg-info
build.py
config.ini.example
config.macos.ini
config.macos.ini.example
data
docs
logs
memory
modules
packages
pyproject.toml
resources
run_macos.sh
tests
uv.lock
## [2026-11-14 13:41] 通过本地 Codex ACP 完成课中答题

- **需求/问题描述**：
  > 把做题部分调用本地 ACP Codex 完成答题。

- **实际实现的功能与改动**：
  - 普通课中题目、融合随堂练习共用 ACP 答题模块，替换固定选择选项的行为；校验 JSON 编号后点击，融合练习再提交。
  - 区分答案消息和服务提示；检查题目变化，限制输出长度和调用时间；失败时保留题目，等待手动作答。
  - 增加官方 ACP Python SDK、锁文件、使用说明及测试。适配器仅安装在忽略的项目运行目录，保留用户的模型和认证配置。
  - 全量测试：112 项中 107 项通过、5 项跳过，包括两项真实 Chrome 行为测试；锁文件和差异检查通过，`Autovisor.py --help` 启动检查通过。
  - 真实 ACP 握手与消息接收成功，但服务拒绝当前 `gpt-6.1-sol` 模型；用户要求保留模型、稍后自行调整。正确答题及提交的真实集成测试尚未通过，不将其计为已验证。

- **涉及文件**：
  - `modules/answering.py`、`modules/tasks.py`、`modules/fusion_adapter.py`
  - `tests/test_answering.py`、`tests/test_answering_integration.py`
  - `pyproject.toml`、`uv.lock`、`README.md`
  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`
  - `docs/CHANGELOG.md`

- **Git 提交**：`7f45b4e38fd3eb6c85b670b113b66c67427e7b64 feat(answering): answer course questions with local Codex ACP`，已推送 `origin/main`；本条提交记录通过后续文档提交补记。

---

## [2026-11-19 11:22] 改用 DeepSeek API 自动答题

- **需求/问题描述**
  > 做题时调用 DeepSeek API，由用户填写自己的 API Key。

- **实际实现的功能与改动**
  - 普通课中题目与融合随堂练习使用 `deepseek-flash` 获取答案。响应须正常结束，选项编号和当前题目须通过校验。Key 留空或请求失败时等待手动作答。
  - Windows 和 macOS 配置示例提供 `[deepseek] api_key`，图形界面可填写、保存和清除 Key。锁文件已移除 ACP 依赖。
  - 全量测试 114 项，111 项通过、3 项跳过。真实 Chrome 与本地 HTTP 服务验证了答题和提交路径。Tk Key 输入行为、锁文件、CLI 帮助、Python 编译与差异检查通过。线上 DeepSeek 请求需要用户的有效 Key，本次未验证。

- **涉及文件**
  - `Autovisor.py`、`GUI.py`、`config.ini.example`、`config.macos.ini.example`
  - `modules/answering.py`、`modules/configs.py`、`modules/course_playback.py`、`modules/fusion_adapter.py`、`modules/tasks.py`
  - `tests/test_answering.py`、`tests/test_answering_integration.py`、`tests/test_config.py`
  - `pyproject.toml`、`uv.lock`、`README.md`、`memory/`、`docs/CHANGELOG.md`

- **Git 提交** `adf454372d27cbb8b7d691ee0d33b0e9746ed6e8 feat(answering): use DeepSeek API with a user-provided key`，已推送 `origin/main`。

---

## [2026-11-19 11:42] 支持智慧树作业考试答题

5a83fc4 docs: record DeepSeek answer history commit
4e0c684 feat(answering): save DeepSeek answers to Markdown
c510821 docs: record automatic homework opening commit
d38bfcf feat(exam): open unsubmitted homework in order
origin


## tool · 2026-11-19T06:48:16Z


Script completed
Wall time 0.2 seconds
Output:

    85	        choice = choices.nth(index)
    86	        await choice.click(timeout=2500)
    87	        await choice.locator("input:checked").wait_for(state="attached", timeout=2500)
    88	    selected = await choices.evaluate_all(
    89	        "rows => rows.flatMap((row, index) => row.querySelector('input:checked') ? [index] : [])"
    90	    )
    91	    if selected != sorted(answers):
    92	        raise AnswerError("页面选中状态与返回的答案不一致")
    93	    return 1, 0
    94	
    95	
    96	async def fill_exam(page: Page, api_key: str) -> tuple[int, int]:
    97	    url = page.url
    98	    if not is_exam_paper_url(url):
    99	        raise AnswerError("当前页面不是受支持的作业考试答题页")
   100	    if not api_key:
   101	        raise AnswerError("请在配置文件的 [deepseek] 中填写 api_key")
   102	
   103	    visible_anchor = page.locator(f"{QUESTION}:visible {ANCHOR}:visible")
   104	    controls = page.locator(".examPaper_box .switch-btn-box:visible")
   105	    next_button = controls.get_by_role("button", name="下一题", exact=True)
   106	    save_button = controls.get_by_role("button", name="保存", exact=True)
   107	    stash_button = page.get_by_role("button", name="暂存作业", exact=True)
   108	    filled = skipped = 0
   109	    cdp = await page.context.new_cdp_session(page)
   110	    try:
   111	        while page.url == url:
   112	            if await has_visible_verification(page):
   113	                raise AnswerError("检测到平台验证，请在浏览器手动处理")
   114	            anchor = await visible_anchor.get_attribute("id", timeout=10000)
   115	            selector = f"{QUESTION}:has({ANCHOR}[id={json.dumps(anchor, ensure_ascii=False)}])"
   116	            result, needs_manual = await _fill_current_question(page, cdp, selector, api_key)
   117	            filled += result
   118	            skipped += needs_manual
   119	            if page.url != url or not await page.locator(f"{selector}:visible").is_visible():
   120	                raise AnswerError("当前题目已变化，已暂停答题")
   121	            if await has_visible_verification(page):
   122	                raise AnswerError("检测到平台验证，请在浏览器手动处理")
   123	            if not await next_button.is_visible():
   124	                can_stash = await stash_button.is_visible()
   125	                if result or (can_stash and not needs_manual):
   126	                    await save_button.click(timeout=2500)
   127	                    await page.get_by_text("保存成功！", exact=True).wait_for(timeout=10000)
   128	                completion = page.locator(".percentage_tit:visible").get_by_text("100%", exact=True)
   129	                if can_stash and await completion.is_visible():
   130	                    await stash_button.click(timeout=2500)
   131	                    dialog = page.locator(".el-message-box:visible").filter(
   132	                        has=page.get_by_text("你确定要暂存作业吗", exact=True)
   133	                    )
   134	                    await dialog.wait_for(timeout=10000)
   135	                    if page.url != url or await has_visible_verification(page):
   136	                        raise AnswerError("检测到页面变化或平台验证，已暂停暂存")
   137	                    await dialog.get_by_role("button", name="确定", exact=True).click(timeout=2500)
   138	                return filled, skipped
   139	            await next_button.click(timeout=2500)
   140	            await page.locator(f"{selector}:visible").wait_for(state="hidden", timeout=10000)
   141	        raise AnswerError("作业考试页面已变化")
   142	    finally:
   143	        if not page.is_closed():
   144	            await cdp.detach()
   145	
   146	
   147	async def _open_next_homework(page: Page, attempted: set[tuple[str, tuple[str, ...], int]]) -> bool:
   148	    url = page.url
   149	    parsed = urlsplit(url)
   150	    if (
   151	        parsed.scheme != "https" or parsed.netloc != "onlineexamh5new.zhihuishu.com"
   152	        or parsed.path != "/stuExamWeb.html" or parsed.fragment.split("?", 1)[0] != "/webExamList"
   153	    ):
   154	        return False
   155	
   156	    unsubmitted = page.locator("#examStateTabWsj.cur:visible")
   157	    dialogs = page.locator(".el-message-box__wrapper:visible, .el-dialog__wrapper:visible")
   158	    if not await unsubmitted.is_visible() or await dialogs.count() or await has_visible_verification(page):
   159	        return False
   160	
   161	    cards = page.locator(".examItemWrap:visible").filter(has=page.locator('.percentage_number:text-is("作业")'))
   162	    occurrences = Counter()
   163	    for card in await cards.all():
   164	        details = await card.locator(".examTit .name, .examInfoList").all_text_contents()
   165	        identity = tuple(" ".join(text.split()) for text in details)
   166	        if not identity or not identity[0]:
   167	            continue
   168	        occurrences[identity] += 1
   169	        key = (url, identity, occurrences[identity])
   170	        if key in attempted:
   171	            continue
   172	        button = card.locator('a[title="开始答题"] .themeBg:visible')
   173	        if not await button.is_visible():
   174	            continue
   175	        if page.url != url or not await unsubmitted.is_visible():
   176	            return False
   177	        attempted.add(key)
   178	        try:
   179	            async with page.expect_popup(timeout=5000) as result:
   180	                await button.click(timeout=2500)
   181	            paper = await result.value
   182	            await paper.wait_for_url(lambda value: value not in {"", "about:blank"}, wait_until="commit", timeout=15000)
   183	            if is_exam_paper_url(paper.url):
   184	                await paper.locator(f"{QUESTION}:visible").first.wait_for(timeout=15000)
   185	        except PlaywrightError as exc:
   186	            logger.warn(f"作业「{identity[0]}」打开或加载失败，请在浏览器检查。", shift=True)
   187	            logger.debug(logger.summarize_exception(exc))
   188	        return True
   189	    return False
   190	
   191	
   192	async def watch_exam_pages(entry_page: Page, api_key: str) -> None:
   193	    pages = set()
   194	    handled = {}
   195	    attempted = set()
   196	
   197	    def track(page: Page) -> None:
   198	        pages.add(page)
   199	        page.on("popup", track)
   200	
   201	    track(entry_page)
   202	    while pages:
   203	        for page in tuple(pages):
   204	            if page.is_closed():
   205	                pages.discard(page)
   206	                handled.pop(page, None)
   207	                continue
   208	            url = page.url
   209	            if not is_exam_paper_url(url):
   210	                handled.pop(page, None)
   211	                continue
   212	            if handled.get(page) == url:
   213	                continue
   214	            try:
   215	                if not await page.locator(f"{QUESTION}:visible").count() or await has_visible_verification(page):
   216	                    continue
   217	                handled[page] = url
   218	                filled, skipped = await fill_exam(page, api_key)
   219	                logger.info(f"本卷自动作答 {filled} 题，待手动处理 {skipped} 题，请检查后自行交卷。", shift=True)
   220	            except AnswerError as exc:
   221	                logger.warn(f"{exc}，请在浏览器手动处理当前试卷。", shift=True)
   222	            except PlaywrightError as exc:
   223	                if not page.is_closed():
   224	                    logger.warn("题目加载或保存失败，请在浏览器检查当前试卷。", shift=True)
   225	                    logger.debug(logger.summarize_exception(exc))
   226	        for page in tuple(pages):
   227	            if page.is_closed():
   228	                continue
   229	            try:
   230	                if await _open_next_homework(page, attempted):
   231	                    break
   232	            except PlaywrightError as exc:
   233	                if not page.is_closed():
   234	                    logger.debug_throttled("homework-list", logger.summarize_exception(exc))
   235	        if pages:
   236	            await asyncio.sleep(0.5)

tests/test_answering_integration.py:19:from modules.exam_answering import fill_exam, watch_exam_pages
tests/test_answering_integration.py:310:        task = asyncio.create_task(watch_exam_pages(self.page, "key-for-test"))
tests/test_answering_integration.py:386:        self.assertEqual(await fill_exam(self.page, "key-for-test"), (1, 0))
tests/test_answering_integration.py:397:        self.assertEqual(await fill_exam(self.page, "key-for-test"), (0, 0))
tests/test_answering_integration.py:406:        self.assertEqual(await fill_exam(self.page, "key-for-test"), (2, 1))
tests/test_answering_integration.py:420:            self.assertEqual(await fill_exam(paper, "key-for-test"), (1, 0))
tests/test_answering_integration.py:458:            await fill_exam(self.page, "key-for-test")
tests/test_answering_integration.py:467:        task = asyncio.create_task(fill_exam(self.page, "key-for-test"))
Autovisor.py:23:from modules.exam_answering import watch_exam_pages
Autovisor.py:254:            await watch_exam_pages(session.page, config.deepseek_api_key)
modules/tasks.py:56:async def has_visible_verification(page: Page) -> bool:
modules/tasks.py:61:    return await has_visible_verification(page) or await has_visible_element(
modules/tasks.py:67:    while await has_visible_verification(page):
modules/tasks.py:292:            if not await has_visible_verification(page):
modules/exam_answering.py:11:from modules.tasks import has_visible_verification
modules/exam_answering.py:82:    if await has_visible_verification(page):
modules/exam_answering.py:96:async def fill_exam(page: Page, api_key: str) -> tuple[int, int]:
modules/exam_answering.py:112:            if await has_visible_verification(page):
modules/exam_answering.py:121:            if await has_visible_verification(page):
modules/exam_answering.py:135:                    if page.url != url or await has_visible_verification(page):
modules/exam_answering.py:158:    if not await unsubmitted.is_visible() or await dialogs.count() or await has_visible_verification(page):
modules/exam_answering.py:192:async def watch_exam_pages(entry_page: Page, api_key: str) -> None:
modules/exam_answering.py:215:                if not await page.locator(f"{QUESTION}:visible").count() or await has_visible_verification(page):
modules/exam_answering.py:218:                filled, skipped = await fill_exam(page, api_key)
modules/course_playback.py:15:    has_visible_verification,
modules/course_playback.py:46:        if await has_visible_verification(page):
modules/course_playback.py:95:            if await has_visible_verification(page):
modules/course_playback.py:216:                    if await has_visible_verification(page):
modules/course_playback.py:296:            if await has_visible_verification(page):
modules/course_playback.py:334:            if await has_visible_verification(page):
modules/course_playback.py:401:            if await has_visible_verification(page):
modules/diagnostics.py:15:from modules.tasks import has_visible_verification
modules/diagnostics.py:116:            verification_visible = await has_visible_verification(page)
modules/course_runner.py:13:from modules.tasks import has_visible_verification, wait_until_verification_hidden
modules/course_runner.py:36:        if await has_visible_verification(page):
import asyncio
import contextlib
import io
import json
import os
import threading
import unittest
from http.server import BaseHTTPRequestHandler, ThreadingHTTPServer
from pathlib import Path
from tempfile import TemporaryDirectory
from types import SimpleNamespace
from unittest.mock import patch

from playwright.async_api import TimeoutError, async_playwright

from Autovisor import run_exam_mode
from modules.answering import AnswerError, answer_question, ask_deepseek
from modules.browser import BrowserSession
from modules.exam_answering import fill_exam, watch_exam_pages
from modules.fusion_adapter import FusionAdapter
from modules.logger import Logger
from modules.tasks import skip_questions


class _DeepSeekHandler(BaseHTTPRequestHandler):
    def do_POST(self):
        request = json.loads(self.rfile.read(int(self.headers["Content-Length"])))
        self.server.request = (self.path, self.headers["Authorization"], request)
        self.server.request_received.set()
        self.server.reply_ready.wait(timeout=10)
        reply = self.server.reply(request) if callable(self.server.reply) else self.server.reply
        body = json.dumps(reply).encode("utf-8")
        self.send_response(self.server.status)
        self.send_header("Content-Type", "application/json")
        self.send_header("Content-Length", str(len(body)))
        self.end_headers()
        self.wfile.write(body)

    def log_message(self, format, *args):
        pass


class _DeepSeekHTTPTestCase(unittest.IsolatedAsyncioTestCase):
    def setUp(self):
        local_dir = Path(__file__).resolve().parents[1] / ".autovisor"
        local_dir.mkdir(mode=0o700, exist_ok=True)
        runtime_dir = TemporaryDirectory(dir=local_dir)
        self.addCleanup(runtime_dir.cleanup)
        runtime_patch = patch.object(Logger(), "runtime_root", runtime_dir.name)
        runtime_patch.start()
        self.addCleanup(runtime_patch.stop)
        self.history_path = Path(runtime_dir.name) / ".autovisor" / "deepseek-answers.md"

        self.server = ThreadingHTTPServer(("127.0.0.1", 0), _DeepSeekHandler)
        self.server.status = 200
        self.server.request_received = threading.Event()
        self.server.reply_ready = threading.Event()
        self.server.reply_ready.set()
        thread = threading.Thread(target=self.server.serve_forever, kwargs={"poll_interval": 0.05})
        thread.start()
        self.addCleanup(thread.join)
        self.addCleanup(self.server.server_close)
        self.addCleanup(self.server.shutdown)
        self.addCleanup(self.server.reply_ready.set)
        endpoint = f"http://127.0.0.1:{self.server.server_port}/chat/completions"
        endpoint_patch = patch("modules.answering.DEEPSEEK_API_URL", endpoint)
        endpoint_patch.start()
        self.addCleanup(endpoint_patch.stop)

    def set_answers(self, answers):
        self.server.reply = {"choices": [{"finish_reason": "stop", "message": {
            "content": json.dumps({"answers": answers}),
        }}]}


class DeepSeekHistoryTests(_DeepSeekHTTPTestCase):
    async def test_valid_answers_append_to_markdown(self):
        self.set_answers([2])
        self.assertEqual(await ask_deepseek("单选题：一加一等于多少？", ["一", "二"], "key-for-test"), [1])
        first_record = self.history_path.read_text(encoding="utf-8")
        self.assertIn("单选题：一加一等于多少？", first_record)
        self.assertIn("选项\n    1. 一\n    2. 二", first_record)
        self.assertIn("答案\n    2. 二", first_record)

        self.set_answers([1, 3])
<!doctype html>
<meta charset="utf-8">
<div class="examPaper_box">
    <div id="questions"></div>
    <div class="switch-btn-box">
        <button id="next" onclick="saveAndAdvance()">下一题</button>
        <button id="save" onclick="saveFinal()" hidden>保存</button>
    </div>
    <button id="stash" onclick="document.getElementById('stash-dialog').showModal()" hidden>暂存作业</button>
    <button onclick="document.body.dataset.submitted = 'yes'">提交作业</button>
    <h3 class="percentage_tit"><span>完成率</span> <em><i id="completion">0</i>%</em></h3>
    <dialog id="stash-dialog" class="el-message-box">
        <p>你确定要暂存作业吗</p>
        <button onclick="this.closest('dialog').close()">取消</button>
        <button onclick="confirmStash()">确定</button>
    </dialog>
    <span id="notice" hidden>保存成功！</span>
</div>
<script>
    const kind = new URLSearchParams(location.search).get('kind');
    const questions = kind === 'single' ? [
        ['单选题', '1 + 1 等于几？', ['3', '2', '4']],
    ] : [
        ['单选题', '已经手动选过的题目', ['保留', '改动']],
        ['多选题', '选择所有质数', ['2', '4', '3']],
        ['简答题', '举出一个例子', []],
        ['判断题', '九是质数', ['对', '错']],
    ];
    for (const [index, [type, text, options]] of questions.entries()) {
        const question = document.createElement('div');
        question.className = 'examPaper_subject';
        question.hidden = index !== 0;
        question.innerHTML = `<div class="subject_stem">
            <div class="subject_num"><span id="anchor_${index}">${index + 1}</span></div>
            <div class="subject_type"><span>【${type}】</span></div>
            <div class="subject_describe"><span></span></div></div>
            <div class="subject_node"></div>`;
        question.querySelector('.subject_describe span').attachShadow({mode: 'closed'}).textContent = text;
        const rows = question.querySelector('.subject_node');
        if (!options.length) rows.innerHTML = '<textarea></textarea>';
        for (const [number, option] of options.entries()) {
            const row = document.createElement('div');
            row.className = 'nodeLab';
            row.innerHTML = `<input hidden value="${number + 1}" name="question-${index}"
                type="${type === '多选题' ? 'checkbox' : 'radio'}">
                <img class="flagChecked" alt="选项图标"><div class="node_detail">${option}</div>`;
            const input = row.querySelector('input');
            input.checked = kind !== 'single' && index === 0 && number === 0;
            row.onclick = () => input.checked = input.type === 'radio' || !input.checked;
            rows.append(row);
        }
        document.getElementById('questions').append(question);
    }

    let current = 0;
    const pages = document.getElementById('questions').children;
    const next = document.getElementById('next');
    const save = document.getElementById('save');
    document.getElementById('stash').hidden = !location.hash.includes('/dohomework/');
    next.hidden = pages.length === 1;
    save.hidden = !next.hidden;
    function recordAnswer() {
        const selected = [...pages[current].querySelectorAll('input:checked')].map(input => input.value);
        document.body.dataset[`saved${current}`] = selected.join(',');
        const answered = [...pages].filter((_, index) => document.body.dataset[`saved${index}`]).length;
        document.getElementById('completion').textContent = Math.floor(100 * answered / pages.length);
    }
    function saveAndAdvance() {
        recordAnswer();
        pages[current].hidden = true;
        pages[++current].hidden = false;
        next.hidden = current === pages.length - 1;
        save.hidden = !next.hidden;
    }
    function saveFinal() {
        recordAnswer();
        document.getElementById('notice').hidden = false;
    }
    function confirmStash() {
        document.getElementById('stash-dialog').close();
        document.body.dataset.stashed = document.body.dataset[`saved${current}`];
        if (window.opener) {
            window.opener.postMessage({
                paper: location.hash,
                stashed: document.body.dataset.stashed,
                submitted: document.body.dataset.submitted,
            }, '*');
            window.close();
        }
    }
</script>

/opt/homebrew/bin/uv
2026-11-19 14:48
.git
* main 5a83fc4 [origin/main] docs: record DeepSeek answer history commit


## tool · 2026-11-19T06:48:37Z


Script completed
Wall time 0.1 seconds
Output:

logs/Log65.txt:16:[14:44:45.229] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第二章单元测试」打开或加载失败，请在浏览器检查。
logs/Log65.txt:18:[14:45:00.881] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第三章单元测试」打开或加载失败，请在浏览器检查。
logs/Log65.txt:20:[14:45:16.573] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第四章单元测试」打开或加载失败，请在浏览器检查。
logs/Log65.txt:22:[14:45:32.214] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第五章单元测试」打开或加载失败，请在浏览器检查。
logs/Log65.txt:25:[14:47:13.317] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。
logs/Log65.txt:29:[14:47:19.184] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。
logs/Log65.txt:32:[14:47:23.652] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。
logs/Log65.txt:35:[14:48:33.743] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。

            )
            if visible:
                return True
        except TargetClosedError:
            raise
        except Exception as exc:
            logger.debug_throttled(
                "has_visible_element",
                f"可见元素检测遇到页面切换({', '.join(selectors)}): "
                f"{logger.summarize_exception(exc)}",
            )
    return False


async def has_visible_verification(page: Page) -> bool:
    return await has_visible_element(page, VERIFICATION_SELECTORS)


async def has_blocking_overlay(page: Page) -> bool:
    return await has_visible_verification(page) or await has_visible_element(
        page, BLOCKING_OVERLAY_SELECTORS
    )


async def wait_until_verification_hidden(page: Page) -> None:
    while await has_visible_verification(page):
        await asyncio.sleep(0.5)


@unittest.skipUnless(os.environ.get("AUTOVISOR_TEST_BROWSER") == "1", "需要显式启用真实浏览器测试")
class BrowserAnswerTests(_DeepSeekHTTPTestCase):
    async def asyncSetUp(self):
        self.playwright = await async_playwright().start()
        self.addAsyncCleanup(self.playwright.stop)
        self.browser = await self.playwright.chromium.launch(channel="chrome", headless=True)
        self.addAsyncCleanup(self.browser.close)
        self.page = await self.browser.new_page()

    async def _check_fusion_manual_answer(self, api_key):
        await self.page.set_content('''
            <div class="ai-class-exercise-dialog">
                <p>单选题：1 + 1 等于多少？</p>
                <button class="option" onclick="this.dataset.clicked='yes'">2</button>
                <button class="option" onclick="this.dataset.clicked='yes'">3</button>
                <div class="el-dialog__footer"><button class="el-button"
                    onclick="document.body.dataset.submitted = 'yes'">提交</button></div>
            </div>
        ''')
        task = asyncio.create_task(FusionAdapter.skip_ai_exercise(self.page, api_key))
        try:
            await asyncio.sleep(0.5)
            self.assertFalse(task.done())
            self.assertEqual(await self.page.locator("[data-clicked]").count(), 0)
            self.assertIsNone(await self.page.locator("body").get_attribute("data-submitted"))
            await self.page.locator(".ai-class-exercise-dialog").evaluate("el => el.remove()")
            self.assertTrue(await asyncio.wait_for(task, timeout=3))
        finally:
            task.cancel()
            with contextlib.suppress(asyncio.CancelledError):
                await task

    async def test_missing_key_keeps_fusion_question_open_without_request(self):
        await self._check_fusion_manual_answer("")
        self.assertFalse(self.server.request_received.is_set())

    async def test_failed_authentication_keeps_fusion_question_open(self):
        self.server.status = 401
        self.server.reply = {"error": {"message": "Invalid API key"}}
        await self._check_fusion_manual_answer("key-for-test")
        self.assertTrue(self.server.request_received.is_set())

    async def test_unfinished_response_keeps_fusion_question_open(self):
        self.set_answers([1])
        self.server.reply["choices"][0]["finish_reason"] = "length"
        await self._check_fusion_manual_answer("key-for-test")
        self.assertTrue(self.server.request_received.is_set())

- Windows 和 macOS 配置示例、Tk 图形界面以及 README 提供配置入口和说明。

## 课程默认设置

- 通用和 macOS 模板、配置加载器及图形配置工具统一使用不限时、1.5 倍速、静音的默认值。用户在配置文件中显式填写的值优先。

## 作业考试启动超时

- 在在线学堂导航提交后开始监听试卷。导航超时时提示在当前标签页手动打开在线学堂，并继续监听。
- 读取课程配置时跳过空白网址，有内容的无效网址继续提示。

## 作业答完后暂存

- 复用末题保存流程。页面显示答题完成且提供「暂存作业」时，打开暂存确认框，核对提示并点击「确定」。交卷由用户操作。
- 使用真实 Chrome 和本地作业页面验证确认暂存、未答完时的处理及答题页关闭行为，再更新使用说明。

## 自动打开未提交作业

- 用户选择课程并进入「未提交」列表后，复用该页的作业入口逐份打开并交由现有答题监听器处理。用卡片类型限定作业范围，按作业身份去重，等本份处理后再继续。
- 以公开前端确认列表控件和弹窗行为，用本地 Chrome 回归测试验证调度、去重及与手动交卷流程的衔接。

## DeepSeek 答案本地记录

- 在三种答题流程共用的 `ask_deepseek` 中，将校验通过的答案连同时间、题目和选项追加到运行目录下的 `.autovisor/deepseek-answers.md`。写入失败时提示并返回已校验的答案。

- [x] 用 Chrome 回归测试复现答完后未暂存。
- [x] 接入暂存确认流程和使用说明。
- [x] 用 Chrome 验证暂存、未完成作业、答题标签页关闭及考试流程，记录验证结果。
- [x] 功能提交 `a9541f8` 已推送 `origin/main`。

## 自动打开未提交作业

- [x] 核对智慧树公开前端的作业类型、「未提交」控件及空白标签页跳转方式。
- [x] 用真实 Chrome 的本地列表复现脚本等待手动打开作业的行为。
- [x] 接入逐份打开、去重和使用说明。全量测试 128 项，125 项通过、3 项跳过，最终版本通过作业列表 Chrome 回归测试。
- [x] 功能提交 `d38bfcf` 已推送至 `origin/main`。

## DeepSeek 答案本地记录

- [x] 核对课中题、融合练习和作业考试的请求入口，以及本地运行目录。
- [x] 用本地 HTTP 回归测试复现缺少 Markdown 记录。
- [x] 实现本地记录并更新使用说明。追加、无效答案处理和写入失败提示均通过验证。
- [x] 启用 Chrome 的全量测试共 130 项，127 项通过、3 项跳过。最终版本的 5 项专项回归全部通过。
- [x] 功能提交 `4e0c684` 已推送至 `origin/main`，开发记录已补记提交哈希。
- 运行启用 Chrome 的全量测试、CLI 帮助和差异检查。
- 修改前，Chrome 回归测试复现末题保存后未暂存。修改后，四项暂存回归用例通过，覆盖末题自动作答与已有选项、未答完保留页面，以及确认后关闭标签页。
- 全量测试 127 项，124 项通过。线上 DeepSeek 与两项 Windows 专用测试跳过。Python 编译、CLI 帮助和差异检查通过。暂存行为使用本地作业页面验证。

## 自动打开作业验证

- 用真实 Chrome 的本地列表检验可答的未提交作业逐份打开并进入原有暂存流程，保留考试和手动打开试卷的现有行为。确认列表更新后避免重复打开，运行全量浏览器测试和差异检查。
- 修改前复现列表需要手动打开作业。修改后用真实 Chrome 和本地页面验证空白弹窗跳转、同名作业区分、逐份暂存、列表重建去重，以及考试入口和未激活的列表均未触发自动打开。
- 全量测试 128 项，125 项通过。线上 DeepSeek 与两项 Windows 专用用例跳过。最终版本的作业列表回归、Python 编译、CLI 帮助和差异检查通过。没有在登录后的真实作业列表中试跑。

## DeepSeek 答案本地记录验证

- 用本地 HTTP 服务和真实文件验证两次有效响应依次追加、中文内容与多选答案完整、API Key 未写入、无效响应不变更文件、写入失败时提示且仍返回有效选项。运行启用 Chrome 的全量测试和差异检查。
- 启用 Chrome 的全量测试共 130 项，127 项通过，线上 DeepSeek 和两项 Windows 专用用例跳过。最终版本通过 5 项专项回归，覆盖本地 Markdown、普通课中题、融合练习和作业考试。Python 编译、CLI 帮助和差异检查通过。
  - 在 `--answer-exam` 模式中选择课程并进入「未提交」列表后，脚本按顺序点击可答作业的「开始答题」，等待答题标签页跳转，并复用现有作答与暂存流程。通过列表网址和卡片信息避免重复打开。考试试卷由用户手动打开，交卷由用户操作。
  - 本地 Chrome 回归验证多份作业依次打开、列表重建后去重、暂存关闭标签页以及交卷边界。全量测试 128 项，125 项通过、3 项跳过。最终版本的作业列表回归、Python 编译、CLI 帮助和差异检查通过。未运行线上作业。

- **涉及文件**
  - `modules/exam_answering.py`、`Autovisor.py`、`README.md`、`tests/test_answering_integration.py`、`tests/fixtures/exam_paper.html`、`memory/`、`docs/CHANGELOG.md`

- **Git 提交** `d38bfcf15451f05463e4a220358644bea35e8a5b feat(exam): open unsubmitted homework in order`，已推送 `origin/main`。

---

## [2026-11-19 14:33] 保存 DeepSeek 答案到本地 Markdown

- **需求/问题描述**
  > 把每次调用 DeepSeek 的答案保存到本地 Markdown。

- **实际实现的功能与改动**
  - 课中题、融合练习和作业考试共用的 DeepSeek 入口将每次通过校验的答案追加到 `.autovisor/deepseek-answers.md`，每条包含时间、题目、选项和答案。写入失败时提示，已校验的答案仍可用于作答。
  - 本地 HTTP 和真实文件验证连续追加、中文及多选答案、无效答案处理和写入失败。启用 Chrome 的全量测试共 130 项，127 项通过、3 项跳过。最终版本的 5 项专项回归、Python 编译、CLI 帮助和差异检查通过。线上 DeepSeek 请求未执行。

- **涉及文件**
  - `modules/answering.py`、`tests/test_answering_integration.py`、`README.md`、`memory/`、`docs/CHANGELOG.md`

- **Git 提交** `4e0c6844cdfe0be1e53cbc8f389cf0553b101c03 feat(answering): save DeepSeek answers to Markdown`，已推送 `origin/main`。

---
memory/agents.md
memory/gotchas.md
memory/plan.md
memory/progress.md
memory/verify.md

lrwxr-xr-x  1 oyamahappa  staff  87 Nov 14 13:27 .venv/bin/python -> /Users/oyamahappa/.local/share/uv/python/cpython-3.13-macos-aarch64-none/bin/python3.13
drwxrwxr-x@ 3 oyamahappa  admin  96 Jun 28  2025 /Applications/Google Chrome.app
uv 0.13.6 (Homebrew 2026-10-26 aarch64-apple-darwin)


## tool · 2026-11-19T06:48:40Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"4f07fa","wall_time_seconds":0.00001075,"exit_code":0,"original_token_count":1087,"output":"[14:35:56.457] [INFO] [__main__.run_exam_mode:253] 请在在线学堂选择课程并进入作业考试。未提交的作业会逐个打开，答完后自动暂存，请核对后自行交卷。\n[14:44:45.229] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第二章单元测试」打开或加载失败，请在浏览器检查。\n[14:44:45.230] [DEBUG] [modules.exam_answering._open_next_homework:187] TimeoutError: Locator.wait_for: Timeout 15000ms exceeded.\n[14:45:00.881] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第三章单元测试」打开或加载失败，请在浏览器检查。\n[14:45:00.881] [DEBUG] [modules.exam_answering._open_next_homework:187] TimeoutError: Locator.wait_for: Timeout 15000ms exceeded.\n[14:45:16.573] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第四章单元测试」打开或加载失败，请在浏览器检查。\n[14:45:16.575] [DEBUG] [modules.exam_answering._open_next_homework:187] TimeoutError: Locator.wait_for: Timeout 15000ms exceeded.\n[14:45:32.214] [WARN] [modules.exam_answering._open_next_homework:186] 作业「第五章单元测试」打开或加载失败，请在浏览器检查。\n[14:45:32.216] [DEBUG] [modules.exam_answering._open_next_homework:187] TimeoutError: Locator.wait_for: Timeout 15000ms exceeded.\n[14:47:08.737] [INFO] [modules.answering.ask_deepseek:62] 正在调用 DeepSeek API 答题...\n[14:47:13.317] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。\n[14:47:13.317] [DEBUG] [modules.exam_answering.watch_exam_pages:225] TimeoutError: Locator.wait_for: Timeout 2500ms exceeded.\n[14:47:13.897] [INFO] [modules.answering.ask_deepseek:62] 正在调用 DeepSeek API 答题...\n[14:47:15.580] [INFO] [modules.answering.ask_deepseek:62] 正在调用 DeepSeek API 答题...\n[14:47:19.184] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。\n[14:47:19.184] [DEBUG] [modules.exam_answering.watch_exam_pages:225] TimeoutError: Locator.wait_for: Timeout 2500ms exceeded.\n[14:47:19.769] [INFO] [modules.answering.ask_deepseek:62] 正在调用 DeepSeek API 答题...\n[14:47:23.652] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。\n[14:47:23.653] [DEBUG] [modules.exam_answering.watch_exam_pages:225] TimeoutError: Locator.wait_for: Timeout 2500ms exceeded.\n[14:48:29.033] [INFO] [modules.answering.ask_deepseek:62] 正在调用 DeepSeek API 答题...\n[14:48:33.743] [WARN] [modules.exam_answering.watch_exam_pages:224] 题目加载或保存失败，请在浏览器检查当前试卷。\n[14:48:33.744] [DEBUG] [modules.exam_answering.watch_exam_pages:225] TimeoutError: Locator.wait_for: Timeout 2500ms exceeded.\nimport asyncio\nimport time\n\nfrom playwright.async_api import TimeoutError\nfrom playwright.async_api import Page\nfrom modules.configs import Config\nfrom modules.utils import get_video_attr, display_window, hide_window, run_on\nfrom playwright._impl._errors import TargetClosedError\nfrom modules.logger import Logger\nfrom modules.video_state import video_at_end\nfrom modules.answering import AnswerError, answer_question\n\nlogger = Logger()\n\nVERIFICATION_SELECTORS = (\n    \".yidun_popup .yidun_modal\",\n    \".yidun_modal__title\",\n    \"[id^='tcaptcha_transform']\",\n)\n\nBLOCKING_OVERLAY_SELECTORS = (\n    \".topic-title\",\n    \".ss2077-custom-dialog\",\n)\n\n\nasync def has_visible_element(page: Page, selectors: tuple[str, ...]) -> bool:\n    for selector in selectors:\n        try:\n            visible = await page.locator(selector).evaluate_all(\n                \"\"\"elements => elements.some(element => {\n                    const style = getComputedStyle(element);\n                    const rect = element.getBoundingClientRect();\n                    const opacity = Number.parseFloat(style.opacity || \"1\");\n                    return style.display !== \"none\" &&\n                        style.visibility !== \"hidden\" &&\n                        opacity > 0.05 &&\n                        rect.width > 0 && rect.height > 0 &&\n                        rect.bottom > 0 && rect.right > 0 &&\n                        rect.top < innerHeight && rect.left < innerWidth;\n                })\"\"\"\n            )\n            if visible:\n"}

## assistant · 2026-11-19T06:49:17Z

本地日志确认，第一类警告出现在作业标签页已经打开、等了 15 秒仍未显示题目时。第二类出现在开始作答后。我会在首题加载超时后刷新一次，作答后的失败保留当前页面和勾选。

## tool · 2026-11-19T06:49:26Z


Script completed
Wall time 0.2 seconds
Output:

{}

## tool · 2026-11-19T06:49:59Z


Script completed
Wall time 0.0 seconds
Output:

{}
