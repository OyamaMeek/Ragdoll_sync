# 01a1e4fb-03ba-7a01-b5d2-a6d393501c49

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/Ragdoll

## developer · 2026-11-16T15:30:22Z

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



## developer · 2026-11-16T15:30:22Z

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
- `r15` = `/Users/oyamahappa/.codex/plugins/cache/openai-bundled`
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/app-6aa2c81fc7c48191a06e101858e41837/2.1.7/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/heygen/4.7.0/skills`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.6/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1112.11217/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r27` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.2/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI- (file: r2/imagegen/SKILL.md)
- openai-docs: API first-timers, Codex/Work Q&A. If the user already has an (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped ins (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated  (file: r2/skill-installer/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:database-access: Explore and query databases on the user's servers (Postgres, M (file: r16/database-access/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:deploy-check: Verify a server after a deployment, update or restart — servic (file: r16/deploy-check/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:incident-triage: Work through a server alert or outage step by step — disk fu (file: r16/incident-triage/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:run-commands: Run shell commands and edit files on the user's servers thro (file: r16/run-commands/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:server-health: Answer "how are my servers doing", "is everything up", "anythi (file: r16/server-health/SKILL.md)
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
- bio-research:start: Set up your bio-research environment and explore available tool (file: r4/start/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end (file: r0/brandkit/SKILL.md)
- cli-anything: Use when the user wants Codex to build, refine, test, validate (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Discover agent-native CLIs for professional software. Access t (file: r0/cli-hub-meta-skill/SKILL.md)
- code-review: Review the changes since a fixed point (commit, branch, tag, (file: r0/code-review/SKILL.md)
- codebase-design: Shared vocabulary for designing deep modules. Use when the u (file: r0/codebase-design/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准备 (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Convert Word (.doc, .docx), PowerPoint (.ppt, .pptx), Excel  (file: r1/convert-documents-to-markdown/SKILL.md)
- cowork-plugin-management:cowork-plugin-customizer: Customize a Claude Code plugin for a specific organization's  (file: r5/cowork-plugin-customizer/SKILL.md)
- cowork-plugin-management:create-cowork-plugin: Guide users through creating a new plugin from scratch in a c (file: r5/create-cowork-plugin/SKILL.md)
- customer-support:customer-escalation: Package an escalation for engineering, product, or leadership w (file: r6/customer-escalation/SKILL.md)
- customer-support:customer-research: Multi-source research on a customer question or topic with sour (file: r6/customer-research/SKILL.md)
- customer-support:draft-response: Draft a professional customer-facing response tailored to the (file: r6/draft-response/SKILL.md)
- customer-support:kb-article: Draft a knowledge base article from a resolved issue or commo (file: r6/kb-article/SKILL.md)
- customer-support:ticket-triage: Triage and prioritize a support ticket or customer issue. Use w (file: r6/ticket-triage/SKILL.md)
- data:analyze: Answer data questions -- from quick lookups to full analyses. U (file: r7/analyze/SKILL.md)
- data:build-dashboard: Build an interactive HTML dashboard with charts, filters, and t (file: r7/build-dashboard/SKILL.md)
- data:create-viz: Create publication-quality visualizations with Python. Use wh (file: r7/create-viz/SKILL.md)
- data:data-context-extractor: Generate or improve a company-specific data analysis skill by (file: r7/data-context-extractor/SKILL.md)
- data:data-visualization: Create effective data visualizations with Python (matplotlib, (file: r7/data-visualization/SKILL.md)
- data:explore-data: Profile and explore a dataset to understand its shape, qualit (file: r7/explore-data/SKILL.md)
- data:sql-queries: Write correct, performant SQL across all major data warehouse d (file: r7/sql-queries/SKILL.md)
- data:statistical-analysis: Apply statistical methods including descriptive stats, trend  (file: r7/statistical-analysis/SKILL.md)
- data:validate-data: QA an analysis before sharing -- methodology, accuracy, and bia (file: r7/validate-data/SKILL.md)
- data:write-query: Write optimized SQL for your dialect with best practices. Use w (file: r7/write-query/SKILL.md)
- deep-research: Runs a deep, survey-grade literature investigation on a rese (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects dependin (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-dri (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diagnosis loop for hard bugs and performance regressions. Us (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r22/documents/26.1112.11217/skills/documents/SKILL.md)
- domain-modeling: Build and sharpen a project's domain model. Use when discuss (file: r0/domain-modeling/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable D (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it  (file: r1/ego-browser/SKILL.md)
- enterprise-search:digest: Generate a daily or weekly digest of activity across all con (file: r8/digest/SKILL.md)
- enterprise-search:knowledge-synthesis: Combines search results from multiple sources into coherent, d (file: r8/knowledge-synthesis/SKILL.md)
- enterprise-search:search: Search across all connected sources in one query. Trigger wi (file: r8/search/SKILL.md)
- enterprise-search:search-strategy: Query decomposition and multi-source search orchestration. Bre (file: r8/search-strategy/SKILL.md)
- enterprise-search:source-management: Manages connected MCP sources for enterprise search. Detects a (file: r8/source-management/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用户 (file: r0/evidence-recap/SKILL.md)
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
- full-output-enforcement: Overrides default LLM truncation behavior. Enforces complete co (file: r0/output-skill/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Elite UX/UI & Advanced GSAP Motion Engineer. Enforces Python-dr (file: r0/gpt-tasteskill/SKILL.md)
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
- heygen:animated-short: Create bold, stylized animated short films of 10 to 30 seconds (file: r17/animated-short/SKILL.md)
- heygen:automated-content-creator: Plan, produce, and keep improving a recurring video series f (file: r17/automated-content-creator/SKILL.md)
- heygen:bedtime-story: Create calming, age-appropriate bedtime story videos for chi (file: r17/bedtime-story/SKILL.md)
- heygen:captions: Create and time video subtitles, opening hook captions, and ex (file: r17/captions/SKILL.md)
- heygen:carousel: Design swipeable image carousels and photo slideshows with Hey (file: r17/carousel/SKILL.md)
- heygen:faceless-explainer: Create narrated faceless explainers with HeyGen speech, Python (file: r17/faceless-explainer/SKILL.md)
- heygen:general-video: Catch-all for video requests only when no specialized HeyGen (file: r17/general-video/SKILL.md)
- heygen:motion-graphics: Design and render focused video motion graphics in Python, i (file: r17/motion-graphics/SKILL.md)
- heygen:narrator: Create narration voiceovers with HeyGen speech synthesis and h (file: r17/narrator/SKILL.md)
- heygen:occasion-video: Create personalized greeting and celebration videos of up to 3 (file: r17/occasion-video/SKILL.md)
- heygen:old-photo-revival: Bring old photos to life. Restore, repair, and colorize a vi (file: r17/old-photo-revival/SKILL.md)
- heygen:picture-video: Create narrated picture-story videos with HeyGen Image pictu (file: r17/picture-video/SKILL.md)
- heygen:script-writer: Write and revise spoken video scripts for UGC, explainers, t (file: r17/script-writer/SKILL.md)
- heygen:talking-head: Create edited talking-head videos with a confirmed HeyGen avat (file: r17/talking-head/SKILL.md)
- heygen:ugc-product: Create faceless, narrated product UGC videos, 30 seconds by  (file: r17/ugc-product/SKILL.md)
- heygen:ugc-review: Create creator-led UGC reviews, brand demonstrations, and scen (file: r17/ugc-review/SKILL.md)
- heygen:ugc-try-on: Create creator-led UGC try-on videos for garments, footwear, b (file: r17/ugc-try-on/SKILL.md)
- heygen:ugc-tutorial: Create step-by-step UGC product tutorials, 30 seconds by defau (file: r17/ugc-tutorial/SKILL.md)
- heygen:ugc-unboxing: Create creator-led UGC unboxing videos, 30 seconds by default, (file: r17/ugc-unboxing/SKILL.md)
- heygen:ugc-voiceless: Create short product ads driven by mood, tactile sound, and  (file: r17/ugc-voiceless/SKILL.md)
- heygen:ugc-website: Create creator-led UGC website or SaaS videos, 30 seconds by (file: r17/ugc-website/SKILL.md)
- heygen:video-editing: Edit and finish videos in Python with scene assembly, layere (file: r17/video-editing/SKILL.md)
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
- legal:brief: Generate contextual briefings for legal work — daily summary, t (file: r10/brief/SKILL.md)
- legal:compliance-check: Run a compliance check on a proposed action, product feature, o (file: r10/compliance-check/SKILL.md)
- legal:legal-response: Generate a response to a common legal inquiry using configured  (file: r10/legal-response/SKILL.md)
- legal:legal-risk-assessment: Assess and classify legal risks using a severity-by-likelihoo (file: r10/legal-risk-assessment/SKILL.md)
- legal:meeting-briefing: Prepare structured briefings for meetings with legal relevance  (file: r10/meeting-briefing/SKILL.md)
- legal:review-contract: Review a contract against your organization's negotiation pla (file: r10/review-contract/SKILL.md)
- legal:signature-request: Prepare and route a document for e-signature — run a pre-signat (file: r10/signature-request/SKILL.md)
- legal:triage-nda: Rapidly triage an incoming NDA and classify it as GREEN (standa (file: r10/triage-nda/SKILL.md)
- legal:vendor-check: Check the status of existing agreements with a vendor across al (file: r10/vendor-check/SKILL.md)
- lemo-opuscar: Direct and produce a short film made entirely in code, in one  (file: r0/lemo-opuscar/SKILL.md)
- make-resume: 中文可编辑简历制作技能：默认基于 ASu 单栏高密度技术简历模板，根据用户经历制作或复刻可编辑 HTML/PDF；用户也 (file: r0/make-resume/SKILL.md)
- marketing:brand-review: Review content against your brand voice, style guide, and messa (file: r11/brand-review/SKILL.md)
- marketing:campaign-plan: Generate a full campaign brief with objectives, audience, mes (file: r11/campaign-plan/SKILL.md)
- marketing:competitive-brief: Research competitors and generate a positioning and messaging (file: r11/competitive-brief/SKILL.md)
- marketing:content-creation: Draft marketing content across channels — blog posts, social  (file: r11/content-creation/SKILL.md)
- marketing:draft-content: Draft blog posts, social media, email newsletters, landing pa (file: r11/draft-content/SKILL.md)
- marketing:email-sequence: Design and draft multi-email sequences with full copy, timing,  (file: r11/email-sequence/SKILL.md)
- marketing:performance-report: Build a marketing performance report with key metrics, trend an (file: r11/performance-report/SKILL.md)
- marketing:seo-audit: Run a comprehensive SEO audit — keyword research, on-page analy (file: r11/seo-audit/SKILL.md)
- media-use: Get or make any media for a HyperFrames video - music, sound (file: r0/media-use/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, ty (file: r0/minimalist-skill/SKILL.md)
- offer: 中文秋招求职进度管理技能：记录和更新投递、筛选、测评、面试、Offer、拒信及招聘邮件状态，生成可搜索的进度表；当用户输 (file: r0/offer/SKILL.md)
- paper-polish: Polishes existing academic prose while preserving the author's (file: r0/paper-polish/SKILL.md)
- paper-writer: Drafts publishable paper prose from the author's own materials (file: r0/paper-writer/SKILL.md)
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不阻塞 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著 (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申请一 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包，须 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开。 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r22/pdf/26.1112.11217/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r18/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves  (file: r24/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what br (file: r24/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r24/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r24/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r24/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r24/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across fiv (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r22/presentations/26.1112.11217/skills/presentations/SKILL.md)
- product-management:competitive-brief: Create a competitive analysis brief for one or more competit (file: r12/competitive-brief/SKILL.md)
- product-management:metrics-review: Review and analyze product metrics with trend analysis and act (file: r12/metrics-review/SKILL.md)
- product-management:product-brainstorming: Brainstorm product ideas, explore problem spaces, and challe (file: r12/product-brainstorming/SKILL.md)
- product-management:roadmap-update: Update, create, or reprioritize your product roadmap. Use when (file: r12/roadmap-update/SKILL.md)
- product-management:sprint-planning: Plan a sprint — scope work, estimate capacity, set goals, and  (file: r12/sprint-planning/SKILL.md)
- product-management:stakeholder-update: Generate a stakeholder update tailored to audience and cadence (file: r12/stakeholder-update/SKILL.md)
- product-management:synthesize-research: Synthesize user research from interviews, surveys, and feedb (file: r12/synthesize-research/SKILL.md)
- product-management:write-spec: Write a feature spec or PRD from a problem statement or featur (file: r12/write-spec/SKILL.md)
- productivity:memory-management: Two-tier memory system that makes Claude a true workplace coll (file: r13/memory-management/SKILL.md)
- productivity:start: Initialize the productivity system and open the dashboard. Use (file: r13/start/SKILL.md)
- productivity:task-management: Simple task management using a shared TASKS.md file. Reference (file: r13/task-management/SKILL.md)
- productivity:update: Sync tasks and refresh memory from your current activity. Us (file: r13/update/SKILL.md)
- project-guide: 中文项目导学、源码课程与项目面经技能：基于本地项目仓库、项目描述或技术材料，按需生成源码课程与理解题，或生成 导学-{简 (file: r0/project-guide/SKILL.md)
- prototype: Build a throwaway prototype to answer a design question. Use (file: r0/prototype/SKILL.md)
- rebuttal-guidance: Provides actionable peer-review rebuttal guidance (not full  (file: r0/rebuttal-guidance/SKILL.md)
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
- reverse-engineer-anything: Reverse engineer native, managed, Electron/JavaScript, packa (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized r (file: r25/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sales:account-context: 360-degree view of an account - CRM data, recent email thread (file: r14/account-context/SKILL.md)
- sales:account-plan: Build or refresh a strategic account plan - current state, goal (file: r14/account-plan/SKILL.md)
- sales:account-research: Research a target company and optionally a specific contact - c (file: r14/account-research/SKILL.md)
- sales:account-tiering: Score and tier a list of accounts (or your full book) against (file: r14/account-tiering/SKILL.md)
- sales:call-prep: Pre-call brief for an upcoming meeting - attendees, account h (file: r14/call-prep/SKILL.md)
- sales:call-summary: Turn a call transcript or call notes into a customer follow-up  (file: r14/call-summary/SKILL.md)
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
- security-audit: Security guidance and vulnerability review for codebases, APIs (file: r0/security-audit/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction a (file: r26/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Heming (file: r26/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a fu (file: r26/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for mini (file: r26/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnos (file: r26/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new (file: r26/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching,  (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (inclu (file: r19/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use (file: r19/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, vis (file: r23/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through t (file: r23/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates a (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating featu (file: r20/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating featu (file: r27/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r20/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r27/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on  (file: r20/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on  (file: r27/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current se (file: r20/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current se (file: r27/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r20/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r27/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementin (file: r20/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementin (file: r27/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r20/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r27/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent ta (file: r20/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent ta (file: r27/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r20/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r27/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing (file: r20/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing (file: r27/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from cu (file: r20/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from cu (file: r27/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to fin (file: r20/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to fin (file: r27/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r20/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r27/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step t (file: r20/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step t (file: r27/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r20/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r27/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build fe (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz your (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r22/template-creator/26.1112.11217/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Codin (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conve (file: r15/visualize/1.0.97/skills/visualize/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an a (file: r21/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in (file: r21/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet  (file: r21/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing ski (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is enabled.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/16/01a1e4a7-a45c-75a0-8f36-90d7b6df6c19`, `/Volumes/SamsungSSD990PRO/GitHub/Ragdoll`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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
- mcp__node_repl: Use `js` for `node_repl` execution with persistent, redeclarable top-level bindings, `js_reset` to clear bindings, and `js_add_node_module_dir` to add package directories.
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

## developer · 2026-11-16T15:30:22Z

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

## developer · 2026-11-16T15:30:22Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-16T15:30:22Z

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
  <current_date>2026-11-16</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/16/01a1e4a7-a45c-75a0-8f36-90d7b6df6c19</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-16T15:30:22Z

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


## developer · 2026-11-16T15:30:23Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
- mcp__mobile_mcp: Drive a real or simulated iOS/Android device.
</tools>

## tool · 2026-11-16T15:30:27Z


Script completed
Wall time 0.1 seconds
Output:

/Volumes/SamsungSSD990PRO/GitHub/Ragdoll
AGENTS.md
Sources/RagdollCore/Store.swift
Sources/RagdollCore/Secrets.swift
Sources/RagdollCore/Models.swift
Sources/RagdollCore/RuntimeBridge.swift
Sources/RagdollCore/Archive.swift
Sources/RagdollCore/Analytics.swift
Sources/Ragdoll/RootView.swift
Sources/Ragdoll/AppModel.swift
Sources/Ragdoll/ConversationView.swift
Sources/Ragdoll/AgentOptionsView.swift
Sources/Ragdoll/SettingsView.swift
Sources/Ragdoll/RagdollApp.swift
Sources/Ragdoll/DashboardView.swift
scripts/build.sh
runtime/src/terminal-auth.ts
runtime/src/client-tools.ts
runtime/src/registry.ts
runtime/src/acp-state.ts
runtime/src/types.ts
runtime/src/agents.ts
runtime/src/rpc.ts
runtime/src/logs.ts
runtime/src/main.ts
runtime/src/desktop.ts
memory/agents.md
memory/plan.md
memory/verify.md
memory/progress.md
memory/gotchas.md


## tool · 2026-11-16T15:30:32Z


Script completed
Wall time 0.1 seconds
Output:

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
# Ragdoll 实施计划

## 已确认需求

- macOS 原生 SwiftUI 应用，Apple Silicon，中文、系统主题。
- 首页：7×24 Token 热力图、成本、项目统计、滚动 168 小时预算及 80%/100% 提醒。
- 全量及增量读取 Codex、Claude Code、dsh；搜索、分页浏览，原生协议续聊。
- 独立“对话”入口，保留原生接入并加入本地 ACP 命令与官方 Registry 的安装、认证、更新、卸载。
- Claude 普通聊天导入官方导出包，续聊打开原聊天。
- 自动归档原始记录、Markdown、元数据及可取得的附件；30 秒防抖、最长 5 分钟，本地 Git 提交，不推送归档。
- 缺失用量/价格显示未知；凭据不进入归档；源日志只读，用户主动对话通过原生工具持久化。

## 结构

- Swift Package：RagdollCore（模型、GRDB、统计、归档）、Ragdoll（SwiftUI 入口及交互）。
- runtime：TypeScript（日志、Codex/Claude/dsh、ACP、Registry）；NDJSON 子进程通信。
- scripts：构建、打包和验证。通过 Swift Package 构建原生 .app，避免依赖额外工程生成器。
- Tests、runtime/test：真实格式样本和真实 Git 仓库验证。

## 执行次序

1. 模型、日志读取、持久索引与浏览。
2. 统计、热力图、预算。
3. 自动 Git 归档及冲突保护。
4. 原生会话恢复、流式输出、权限、停止。
5. ACP 本地与 Registry、安装和认证。
6. Claude 导出包导入、打包、实际运行与最终检查。
# 实施进度

- [x] 初始化工程、真实格式样本与历史读取。
- [x] Swift 索引与会话浏览；完整 SwiftUI 应用已编译。
- [x] 首页、成本和预算；5 项 Swift 核心测试通过。
- [x] Git 全量/增量归档与提交；已验证不带入外部暂存、无空提交、手工修改保护。
- [进行中] 三种原生工具续聊：dsh 真实新建、恢复、两次对话通过；Codex 握手通过，默认模型被账号拒绝；Claude 未登录。
- [进行中] ACP 协议、本地与 Registry：官方 Claude ACP 实际下载安装和协商通过，补充历史导入与动态配置。
- [x] Claude 导出包导入及格式边界；尚无用户官方导出包实测。
- [进行中] 打包、实际运行、静态审查和提交推送。

## 用户最新要求

- Claude 接入完成代码即可，后续不再运行 Claude 测试。真实续聊验证保留未完成状态；不要求用户代为测试。

## 环境事实

- 初始提交 18e3793；main 跟踪 origin/main；仓库原本只有 AGENTS.md。
- macOS 15.7.7，Swift 6.1.2，Xcode 16.4；Node 26.13.0。
- Codex 0.147.0、Claude Code 2.1.268；DeepSeek Harness.app 0.2.1-rc.5，dsh 不在 PATH，但应用包内包含运行入口。
- 没有既存测试、项目技能或构建脚本。

## 实施决定

- 使用 Swift Package 与打包脚本生成 .app；无需用户安装工程生成工具。
- npm 发布的 dsh SDK 客户端早于当前协议；通过 dsh 官方 SDK JSON-RPC 接口直接连接，已用安装的 dsh 验证恢复，删除未使用的旧客户端依赖。
- Swift 和真实 Codex 测试需要沙箱外构建/状态目录写入权限，已通过自动审批运行；普通沙箱失败不能判定为实现不兼容。
- ACP v2 按聚合状态等待完成，不能把 prompt 的入队响应当作对话完成；不将上下文占用量当作消费 Token。


## developer · 2026-11-16T15:30:33Z

<tools>
Added deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__pubmed
</tools>

## tool · 2026-11-16T15:30:37Z


Script completed
Wall time 0.1 seconds
Output:

      63 Sources/RagdollCore/Analytics.swift
      85 Sources/RagdollCore/Archive.swift
     106 Sources/RagdollCore/Models.swift
     117 Sources/RagdollCore/RuntimeBridge.swift
      23 Sources/RagdollCore/Secrets.swift
      71 Sources/RagdollCore/Store.swift
      61 Sources/Ragdoll/AgentOptionsView.swift
     304 Sources/Ragdoll/AppModel.swift
     197 Sources/Ragdoll/ConversationView.swift
     135 Sources/Ragdoll/DashboardView.swift
      21 Sources/Ragdoll/RagdollApp.swift
      61 Sources/Ragdoll/RootView.swift
     215 Sources/Ragdoll/SettingsView.swift
      38 runtime/src/acp-state.ts
     457 runtime/src/agents.ts
      71 runtime/src/client-tools.ts
      47 runtime/src/desktop.ts
     195 runtime/src/logs.ts
     120 runtime/src/main.ts
     173 runtime/src/registry.ts
      84 runtime/src/rpc.ts
      42 runtime/src/terminal-auth.ts
      34 runtime/src/types.ts
      41 scripts/build.sh
    2761 total


## tool · 2026-11-16T15:30:40Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 10508)
Total output lines: 577

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
    14	        if !fm.fileExists(atPath: root.appendingPathComponent(".git").path) { _ = try git(root, ["init"]) }
    15	        guard try git(root, ["rev-parse", "--show-toplevel"]) == root.path else { throw failure("请选择 Git 仓库的根目录") }
    16	        let manifestURL = root.appendingPathComponent(".ragdoll-manifest.json")
    17	        let old = fm.fileExists(atPath: manifestURL.path) ? try JSONDecoder().decode([String: String].self, from: Data(contentsOf: manifestURL)) : [:]
    18	        let encoder = JSONEncoder(); encoder.outputFormatting = [.prettyPrinted, .sortedKeys, .withoutEscapingSlashes]
    19	        var desired: [String: Data] = [:]
    20	        for session in sessions {
    21	            let base = "sessions/\(safeName(session.source))/\(safeName(session.id))"
    22	            var metadata = session; metadata.messages = []
    23	            desired[base + "/metadata.json"] = try encoder.encode(metadata)
    24	            let transcript = "# \(session.title)\n\n来源：\(session.source)\n\n项目：\(session.project)\n\n" + session.messages.map { "## \($0.role) · \(ISO8601DateFormatter().string(from: Date(timeIntervalSince1970: $0.time / 1000)))\n\n\($0.text)\n" }.joined(separator: "\n")
    25	            let portable = session.files.enumerated().reduce(transcript) { text, entry in
    26	                text.replacingOccurrences(of: URL(fileURLWithPath: entry.element).absoluteString, with: "raw/\(entry.offset)-\(safeName(URL(fileURLWithPath: entry.element).lastPathComponent))")
    27	            }
    28	            desired[base + "/transcript.md"] = Data(portable.utf8)
    29	            for (index, path) in session.files.enumerated() {
    30	                let file = URL(fileURLWithPath: path)
    31	                guard fm.fileExists(atPath: file.path) else { continue }
    32	                let values = try file.resourceValues(forKeys: [.isRegularFileKey])
    33	                guard values.isRegularFile == true else { throw failure("无法归档非普通文件：\(path)") }
    34	                desired[base + "/raw/\(index)-\(safeName(file.lastPathComponent))"] = try Data(contentsOf: file)
    35	            }
    36	            if session.files.isEmpty { desired[base + "/events.json"] = try encoder.encode(session) }
    37	        }
    38	        for (path, _) in desired {
    39	            let destination = root.appendingPathComponent(path)
    40	            guard !destination.resolvingSymlinksInPath().path.hasPrefix(root.path + "/.git/") && destination.resolvingSymlinksInPath().path.hasPrefix(root.path + "/") else { throw failure("归档路径越界") }
    41	            if fm.fileExists(atPath: destination.path) {
    42	                let digest = hash(try Data(contentsOf: destination))
    43	                guard old[path] == digest else { throw failure("归档文件已被手动修改或不属于应用：\(path)。请保留修改后选择其他归档目录，或恢复文件后重试。") }
    44	            }
    45	        }
    46	        var manifest = old
    47	        var changed: [String] = []
    48	        for (path, data) in desired {
    49	            let digest = hash(data), destination = root.appendingPathComponent(path)
    50	            if old[path] == digest && fm.fileExists(atPath: destination.path) { continue }
    51	            try fm.createDirectory(at: destination.deletingLastPathComponent(), withIntermediateDirectories: true)
    52	            try data.write(to: destination, options: .atomic)
    53	            manifest[path] = digest; changed.append(path)
    54	        }
    55	        let manifestData = try encoder.encode(manifest)
    56	        let previousManifest = fm.fileExists(atPath: manifestURL.path) ? try Data(contentsOf: manifestURL) : nil
    57	        if previousManifest != manifestData {
    58	            try manifestData.write(to: manifestURL, options: .atomic); changed.append(".ragdoll-manifest.json")
    59	        }
    60	        let managed = Array(manifest.keys) + [".ragdoll-manifest.json"]
    61	        let pending = try git(root, ["status", "--porcelain", "--"] + managed)
    62	        guard !pending.isEmpty else { return ArchiveResult(files: 0, commit: nil) }
    63	        _ = try git(root, ["add", "--"] + managed)
    64	        _ = try git(root, ["commit", "--only", "-m", "chore(archive): sync conversations", "--"] + managed)
    65	        return ArchiveResult(files: changed.count, commit: try git(root, ["rev-parse", "--short", "HEAD"]))
    66	    }
    67	
    68	    private static func safeName(_ value: String) -> String {
    69	        let allowed = CharacterSet.alphanumerics.union(CharacterSet(charactersIn: "._-"))
    70	        let name = value.unicodeScalars.map { allowed.contains($0) ? String($0) : "_" }.joined()
    71	        return name.isEmpty || name == "." || name == ".." ? "session" : name
    72	    }
    73	    private static func hash(_ data: Data) -> String { SHA256.hash(data: data).map { String(format: "%02x", $0) }.joined() }
    74	    private static func failure(_ message: String) -> NSError { NSError(domain: "Ragdoll.Archive", code: 1, userInfo: [NSLocalizedDescriptionKey: message]) }
    75	    private static func git(_ root: URL, _ args: [String]) throws -> String {
    76	        let process = Process(); process.executableURL = URL(fileURLWithPath: "/usr/bin/git"); process.arguments = ["-C", root.path] + args
    77	        let pipe = Pipe(); process.standardOutput = pipe; process.standardError = pipe
    78	        process.environment = ProcessInfo.processInfo.environment.merging(["GIT_TERMINAL_PROMPT": "0"]) { _, new in new }
    79	        try process.run()
    80	        let data = pipe.fileHandleForReading.readDataToEndOfFile(); process.waitUntilExit()
    81	        let text = String(decoding: data, as: UTF8.self).trimmingCharacters(in: .whitespacesAndNewlines)
    82	        guard process.terminationStatus == 0 else { throw failure("文件已保留；Git 操作失败：\(text)") }
    83	        return text
    84	    }
    85	}
     1	import Foundation
     2	import GRDB
     3	
     4	public final class Store: Sendable {
     5	    private let db: DatabaseQueue
     6	    public init(path: String) throws {
     7	        db = try DatabaseQueue(path: path)
     8	        try db.write { db in
     9	            try db.execute(sql: "CREATE TABLE IF NOT EXISTS sessions (id TEXT PRIMARY KEY, source TEXT NOT NULL, native_id TEXT NOT NULL, title TEXT NOT NULL, project TEXT NOT NULL, updated REAL NOT NULL, body BLOB NOT NULL, summary BLOB NOT NULL, search TEXT NOT NULL)")
    10	            try db.execute(sql: "CREATE INDEX IF NOT EXISTS sessions_updated ON sessions(updated DESC)")
    11	            if try !db.columns(in: "sessions").contains(where: { $0.name == "canonical_id" }) { try db.execute(sql: "ALTER TABLE sessions ADD COLUMN canonical_id TEXT") }
    12	            try db.execute(sql: "CREATE INDEX IF NOT EXISTS sessions_native ON sessions(source,native_id)")
    13	            try db.execute(sql: "CREATE INDEX IF NOT EXISTS sessions_canonical ON sessions(canonical_id)")
    14	            try db.execute(sql: "CREATE TABLE IF NOT EXISTS settings (id INTEGER PRIMARY KEY CHECK(id=1), body BLOB NOT NULL)")
    15	        }
    16	    }
    17	    @discardableResult public func save(_ session: Session) throws -> Bool {
    18	        return try db.write { db in
    19	            var session = session
    20	            if let existing = try Data.fetchOne(db, sql: "SELECT body FROM sessions WHERE id=?", arguments: [session.id]) {
    21	                let previous = try JSONDecoder().decode(Session.self, from: existing)
    22	                session.files = Array(Set(previous.files + session.files)).sorted()
    23	                session.instanceID = session.instanceID ?? previous.instanceID
    24	            }
    25	            if let nativeSource = session.nativeSource {
    26	                let candidates = try Data.fetchAll(db, sql: "SELECT body FROM sessions WHERE source=? AND native_id=?", arguments: [nativeSource, session.nativeID]).map { try JSONDecoder().decode(Session.self, from: $0) }.filter { $0.home == session.home }
    27	                if candidates.count == 1, let native = candidates.first {
    28	                    session.canonicalID = native.id; session.files = Array(Set(session.files + native.files)).sorted(); session.usage = native.usage
    29	                }
    30	            }
    31	            var changed = try Self.upsert(db, session)
    32	            if session.source != "acp" {
    33	                let aliases = try Data.fetchAll(db, sql: "SELECT body FROM sessions WHERE source='acp' AND native_id=?", arguments: [session.nativeID]).map { try JSONDecoder().decode(Session.self, from: $0) }
    34	                for var alias in aliases where alias.nativeSource == session.source && alias.home == session.home {
    35	                    alias.canonicalID = session.id; alias.usage = session.usage; alias.files = Array(Set(alias.files + session.files)).sorted()
    36	                    changed = try Self.upsert(db, alias) || changed
    37	                }
    38	            }
    39	            return changed
    40	        }
    41	    }
    42	    private static func upsert(_ db: Database, _ session: Session) throws -> Bool {
    43	        let encoder = JSONEncoder(); encoder.outputFormatting = [.sortedKeys]
    44	        let body = try encoder.encode(session)
    45	        guard try Data.fetchOne(db, sql: "SELECT body FROM sessions WHERE id=?", arguments: [session.id]) != body else { return false }
    46	        var summary = session; summary.messages = []
    47	        let summaryData = try encoder.encode(summary)
    48	        try db.execute(sql: "INSERT INTO sessions(id,source,native_id,title,project,updated,body,summary,search,canonical_id) VALUES (?,?,?,?,?,?,?,?,?,?) ON CONFLICT(id) DO UPDATE SET title=excluded.title, project=excluded.project, updated=excluded.updated, body=excluded.body, summary=excluded.summary, search=excluded.search, canonical_id=excluded.canonical_id", arguments: [session.id, session.source, session.nativeID, session.title, session.project, session.updated, body, summaryData, session.title + "\n" + session.messages.map(\.text).joined(separator: "\n"), session.canonicalID])
    49	        return true
    50	    }
    51	    public func list(query: String = "", limit: Int = 10000) throws -> [Session] {
    52	        try db.read { db in
    53	            let escaped = query.replacingOccurrences(of: "\\", with: "\\\\").replacingOccurrences(of: "%", with: "\\%").replacingOccurrences(of: "_", with: "\\_")
    54	            return try Data.fetchAll(db, sql: "SELECT summary FROM sessions s WHERE search LIKE ? ESCAPE '\\' AND NOT EXISTS (SELECT 1 FROM sessions a WHERE a.canonical_id=s.id) ORDER BY updated DESC LIMIT ?", arguments: ["%\(escaped)%", limit]).map { try JSONDecoder().decode(Session.self, from: $0) }
    55	        }
    56	    }
    57	    public func session(_ id: String) throws -> Session? {
    58	        try db.read { db in
    59	            try Data.fetchOne(db, sql: "SELECT body FROM sessions WHERE id=?", arguments: [id]).map { try JSONDecoder().decode(Session.self, from: $0) }
    60	        }
    61	    }
    62	    public func settings() throws -> Settings {
    63	        try db.read { db in
    64	            try Data.fetchOne(db, sql: "SELECT body FROM settings WHERE id=1").map { try JSONDecoder().decode(Settings.self, from: $0) } ?? Settings()
    65	        }
    66	    }
    67	    public func saveSettings(_ settings: Settings) throws {
    68	        let data = try JSONEncoder().encode(settings)
    69	        try db.write { db in try db.execute(sql: "INSERT INTO settings(id,body) VALUES(1,?) ON CONFLICT(id) DO UPDATE SET body=excluded.body", arguments: [data]) }
    70	    }
    71	}
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
    71	                pending.append(chunk)
    72	                while let index = pending.firstIndex(of: 10) {
    73	                    let line = pending.prefix(upTo: index); pending.removeSubrange(...index)
    74	                    await self?.receive(Data(line))
    75	                }
    76	            }
    77	        }
    78	        let errorReader = errors.fileHandleForReading
    79	        Task.detached { [weak self] in
    80	            while true { let data = errorReader.availableData; if data.isEmpty { break }; await self?.errorOutput(String(decoding: data, as: UTF8.self)) }
    81	        }
    82	    }
    83	    public func request(_ method: String, _ params: [String: JSONValue] = [:], timeout: Double = 120) async throws -> JSONValue {
    84	        guard let input else { throw failure("SDK 助手尚未启动") }
    85	        serial += 1; let id = String(serial)
    86	        let message = try JSONEncoder().encode(JSONValue.object(["id": .string(id), "method": .string(method), "params": .object(params)])) + Data([10])
    87	        return try await withCheckedThrowingContinuation { continuation in
    88	            pending[id] = continuation
    89	            do { try input.write(contentsOf: message) }
    90	            catch { pending.removeValue(forKey: id)?.resume(throwing: error) }
    91	            if timeout > 0 { Task { try? await Task.sleep(for: .seconds(timeout)); timedOut(id, method) } }
    92	        }
    93	    }
    94	    private func timedOut(_ id: String, _ method: String) { pending.removeValue(forKey: id)?.resume(throwing: failure("助手请求超时：\(method)。运行中的操作不会自动重试。")) }
    95	    private func receive(_ data: Data) async {
    96	        do {
    97	            let message = try JSONDecoder().decode(JSONValue.self, from: data)
    98	            if !message["event"].string.isEmpty { await handler?(message["event"].string, message["data"]); return }
    99	            let id = message["id"].string
   100	            guard let continuation = pending.removeValue(forKey: id) else { return }
   101	            if message["error"] != .null { continuation.resume(throwing: failure(message["e…508 tokens truncated…ng] = []
    28	    @Published var approvals: [Approval] = []
    29	    @Published var registry: [JSONValue] = []
    30	    @Published var agentInfo: [String: JSONValue] = [:]
    31	    @Published var conversationInfo: [String: JSONValue] = [:]
    32	    @Published var loginLinks: [URL] = []
    33	    @Published var nativeHistory: [JSONValue] = []
    34	    @Published var nativeCursor = ""
    35	    @Published var nativeHistoryProject = ""
    36	    @Published var registryLoading = false
    37	    @Published var busyAgents: Set<String> = []
    38	    @Published var archiveStatus = "尚未选择归档仓库"
    39	    @Published var lastArchive: Date?
    40	    @Published var composerModel = ""
    41	    @Published var toolEvents: [String: [JSONValue]] = [:]
    42	    let bridge = RuntimeBridge()
    43	    let root: URL
    44	    private let store: Store?
    45	    private var reloadTask: Task<Void, Never>?
    46	    private var archiveTask: Task<Void, Never>?
    47	    private var dirtySince: Date?
    48	    private var initialized = false
    49	
    50	    init() {
    51	        root = ProcessInfo.processInfo.environment["RAGDOLL_DATA_DIR"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent("Library/Application Support/Ragdoll")
    52	        do {
    53	            try FileManager.default.createDirectory(at: root, withIntermediateDirectories: true)
    54	            let store = try Store(path: root.appendingPathComponent("index.sqlite").path)
    55	            let settings = try store.settings(), sessions = try store.list()
    56	            self.store = store; self.settings = settings; self.sessions = sessions
    57	        } catch { store = nil; self.error = error.localizedDescription }
    58	    }
    59	    var filtered: [Session] { sessions.filter { session in
    60	        guard (source == "all" || session.source == source || session.nativeSource == source) && (project.isEmpty || session.project == project) else { return false }
    61	        guard let bucket = heatmapFilter else { return true }
    62	        let start = Calendar.current.date(byAdding: .day, value: -6, to: Calendar.current.startOfDay(for: Date()))!
    63	        return session.usage.contains { usage in
    64	            let date = Date(timeIntervalSince1970: usage.time / 1000)
    65	            return date >= start && Calendar.current.component(.weekday, from: date) - 1 == bucket[0] && Calendar.current.component(.hour, from: date) == bucket[1]
    66	        }
    67	    } }
    68	    var dashboard: Dashboard { Analytics.summarize(filtered, prices: settings.prices, budget: settings.weeklyBudget) }
    69	    var projects: [String] { Array(Set(sessions.map(\.project).filter { !$0.isEmpty })).sorted() }
    70	
    71	    func launch() async {
    72	        guard !initialized else { return }; initialized = true
    73	        await bridge.setHandler { [weak self] event, data in await self?.receive(event, data) }
    74	        do {
    75	            try await bridge.start(dataDirectory: root)
    76	            let initial = try await bridge.request("initialize")
    77	            if settings.locations.isEmpty { settings.locations = try initial["locations"].decode([Location].self) }
    78	            let defaults = try initial["agents"].decode([AgentConfig].self)
    79	            for agent in defaults where !settings.agents.contains(where: { $0.id == agent.id }) { settings.agents.append(agent) }
    80	            try saveSettings(); ready = true; await refresh()
    81	            Task { [weak self] in
    82	                while !Task.isCancelled { try? await Task.sleep(for: .seconds(60)); guard let self else { return }; await self.refresh() }
    83	            }
    84	        } catch { self.error = error.localizedDescription; status = "启动失败" }
    85	    }
    86	    func receive(_ event: String, _ data: JSONValue) {
    87	        do {
    88	            switch event {
    89	            case "session":
    90	                let session = try data.decode(Session.self)
    91	                if try store?.save(session) == true {
    92	                    if selectedID == session.id { selected = session }
    93	                    scheduleReload(); scheduleArchive()
    94	                }
    95	            case "delta":
    96	                if data["conversationID"].string == selectedID, let message = try? data["message"].decode(Message.self) {
    97	                    if let index = selected?.messages.firstIndex(where: { $0.id == message.id }) { selected?.messages[index] = message }
    98	                    else { selected?.messages.append(message) }
    99	                }
   100	            case "state":
   101	                let id = data["conversationID"].string
   102	                if data["state"].string == "running" { running.insert(id) } else { running.remove(id) }
   103	                if !data["message"].string.isEmpty { error = data["message"].string }
   104	                if data["state"].string == "idle" { Task { await refresh() } }
   105	            case "chat":
   106	                let id = data["conversationID"].string
   107	                var events = toolEvents[id] ?? []; events.append(data)
   108	                toolEvents[id] = Array(events.suffix(100))
   109	            case "approval": approvals.append(Approval(id: data["requestID"].string, method: data["method"].string, params: data["params"]))
   110	            case "approvalCancelled": approvals.removeAll { $0.id == data["requestID"].string }
   111	            case "sourceChanged": if !scanning { Task { await refresh() } }
   112	            case "warning": warnings.append(data.string); warnings = Array(warnings.suffix(100))
   113	            case "agentEvent":
   114	                let text = data.text
   115	                warnings.append(text)
   116	                collectLoginLinks(data)
   117	            case "agentConfiguration":
   118	                let id = data["conversationID"].string.isEmpty ? selectedID ?? "" : data["conversationID"].string
   119	                var info = (conversationInfo[id] ?? .object([:])).dictionary
   120	                let update = data["update"]
   121	                if update["configOptions"] != .null { info["configOptions"] = update["configOptions"] }
   122	                if update["availableCommands"] != .null { info["availableCommands"] = update["availableCommands"] }
   123	                conversationInfo[id] = .object(info)
   124	            case "disconnected": ready = false; running.removeAll(); error = data.string
   125	            default: break
   126	            }
   127	        } catch { self.error = error.localizedDescription }
   128	    }
   129	    func refresh() async {
   130	        guard ready, !scanning else { return }; scanning = true; status = "正在读取会话…"
   131	        do {
   132	            let result = try await bridge.request("scan", ["locations": try .encode(settings.locations)], timeout: 600)
   133	            try reload(); status = "索引已更新 · 本次处理 \(result["count"].text) 个变更会话"
   134	        } catch { self.error = error.localizedDescription; status = "扫描失败，可重试" }
   135	        scanning = false; scheduleArchive(markDirty: false)
   136	    }
   137	    private func scheduleReload() {
   138	        guard reloadTask == nil else { return }
   139	        reloadTask = Task { try? await Task.sleep(for: .milliseconds(300)); do { try reload() } catch { self.error = error.localizedDescription }; reloadTask = nil }
   140	    }
   141	    func reload() throws { sessions = try store?.list(query: query) ?? [] }
   142	    func select(_ id: String?) {
   143	        selectedID = id
   144	        do { selected = try id.flatMap { try store?.session($0) } }
   145	        catch { self.error = error.localizedDescription }
   146	    }
   147	    func saveSettings() throws { try store?.saveSettings(settings) }
   148	    func persistSettings() { do { try saveSettings() } catch { self.error = error.localizedDescription } }
   149	    private func hydrated(_ config: AgentConfig) throws -> AgentConfig {
   150	        var config = config; config.env = try Secrets.load(config.id).merging(config.env) { secret, _ in secret }; return config
   151	    }
   152	    func saveAgent(_ agent: AgentConfig) throws {
   153	        try Secrets.save(agent.env, for: agent.id)
   154	        var safe = agent; safe.env = [:]
   155	        if let i = settings.agents.firstIndex(where: { $0.id == agent.id }) { settings.agents[i] = safe } else { settings.agents.append(safe) }
   156	        try saveSettings()
   157	    }
   158	    @discardableResult func startChat(agent: AgentConfig, cwd: String, resume: Session? = nil) async -> Bool {
   159	        do {
   160	            var params: [String: JSONValue] = ["agent": try .encode(hydrated(agent)), "cwd": .string(cwd)]
   161	            if let resume { params["session"] = try .encode(resume) }
   162	            if agent.kind != "acp" && !composerModel.isEmpty { params["model"] = .string(composerModel) }
   163	            let result = try await bridge.request("chat.start", params)
   164	            let session = try result["session"].decode(Session.self)
   165	            _ = try store?.save(session); try reload(); select(session.id); agentInfo[agent.id] = result["info"]; conversationInfo[session.id] = result["info"]
   166	            return true
   167	        } catch { self.error = error.localizedDescription; return false }
   168	    }
   169	    func resumeSelected() async {
   170	        guard let selected else { return }
   171	        if selected.source == "desktop" { openDesktop(selected); return }
   172	        let agent = settings.agents.first { $0.id == selected.instanceID } ?? settings.agents.first { $0.kind == selected.source }
   173	        guard let agent else { error = "请先配置此会话使用的 Agent"; return }
   174	        await startChat(agent: agent, cwd: selected.project.isEmpty ? FileManager.default.homeDirectoryForCurrentUser.path : selected.project, resume: selected)
   175	    }
   176	    func send(_ text: String, attachments: [URL] = []) async -> Bool {
   177	        guard let selected else { return false }
   178	        if selected.source == "desktop" { openDesktop(selected); return false }
   179	        if !running.contains(selected.id) { await resumeSelected() }
   180	        guard let id = self.selected?.id else { return false }
   181	        do { _ = try await bridge.request("chat.send", ["id": .string(id), "text": .string(text), "model": .string(selected.source == "acp" ? "" : composerModel), "attachments": try .encode(attachments.map(\.path))], timeout: 0); return true }
   182	        catch { self.error = error.localizedDescription; running.remove(id); return false }
   183	    }
   184	    func stop() async {
   185	        guard let id = selectedID else { return }
   186	        do { _ = try await bridge.request("chat.stop", ["id": .string(id)]) } catch { self.error = error.localizedDescription }
   187	    }
   188	    func answer(_ request: Approval, allowed: Bool, optionID: String? = nil, content: JSONValue? = nil) async {
   189	        var answer: [String: JSONValue] = ["allowed": .bool(allowed)]
   190	        if let optionID { answer["optionId"] = .string(optionID) }
   191	        if let content { answer.merge(content.dictionary) { _, new in new }; answer["content"] = content }
   192	        do {
   193	            _ = try await bridge.request("approval", ["requestID": .string(request.id), "answer": .object(answer)])
   194	            approvals.removeAll { $0.id == request.id }
   195	        } catch { self.error = error.localizedDescription }
   196	    }
   197	    func probe(_ agent: AgentConfig) async {
   198	        busyAgents.insert(agent.id); defer { busyAgents.remove(agent.id) }
   199	        do { agentInfo[agent.id] = try await bridge.request("probe", ["agent": try .encode(hydrated(agent)), "cwd": .string(FileManager.default.homeDirectoryForCurrentUser.path)]) }
   200	        catch { self.error = error.localizedDescription }
   201	    }
   202	    func loadRegistry() async {
   203	        registryLoading = true; defer { registryLoading = false }
   204	        do { registry = try await bridge.request("registry").array } catch { self.error = error.localizedDescription }
   205	    }
   206	    func installAgent(_ entry: JSONValue) async {
   207	        let id = entry["id"].string; busyAgents.insert(id); defer { busyAgents.remove(id) }
   208	        do {
   209	            let value = try await bridge.request("install", ["agent": entry], timeout: 600)
   210	            try saveAgent(value.decode(AgentConfig.self)); status = "已安装 \(entry["name"].string)" 
   211	        } catch { self.error = error.localizedDescription }
   212	    }
   213	    func removeAgent(_ agent: AgentConfig) async {
   214	        do {
   215	            guard !running.contains(where: { id in sessions.first(where: { $0.id == id })?.instanceID == agent.id }) else { error = "请先停止此 Agent 的运行会话"; return }
   216	            _ = try await bridge.request("uninstall", ["agent": try .encode(agent)])
   217	            settings.agents.removeAll { $0.id == agent.id }; try Secrets.save([:], for: agent.id); try saveSettings()
   218	        } catch { self.error = error.localizedDescription }
   219	    }
   220	    func authenticate(_ agent: AgentConfig, methodID: String) async {
   221	        busyAgents.insert(agent.id); defer { busyAgents.remove(agent.id) }
   222	        do {
   223	            let result = try await bridge.request("authenticate", ["agent": try .encode(hydrated(agent)), "methodID": .string(methodID), "cwd": .string(FileManager.default.homeDirectoryForCurrentUser.path)], timeout: 600)
   224	            if !result["terminalScript"].string.isEmpty { NSWorkspace.shared.open(URL(fileURLWithPath: result["terminalScript"].string)); status = "在终端完成登录后，请检测连接" }
   225	            else { await probe(agent) }
   226	        } catch { self.error = error.localizedDescription }
   227	    }
   228	    func importDesktop() {
   229	        let panel = NSOpenPanel(); panel.allowedContentTypes = [.zip, .json]; panel.allowsMultipleSelection = false
   230	        guard panel.runModal() == .OK, let url = panel.url else { return }
   231	        Task { do { _ = try await bridge.request("import", ["path": .string(url.path)]); try reload(); scheduleArchive() } catch { self.error = error.localizedDescription } }
   232	    }
   233	    func chooseArchive() {
   234	        let panel = NSOpenPanel(); panel.canChooseDirectories = true; panel.canChooseFiles = false; panel.canCreateDirectories = true; panel.prompt = "选择归档仓库"
   235	        guard panel.runModal() == .OK, let url = panel.url else { return }
   236	        settings.archivePath = url.path; persistSettings(); Task { await archiveNow() }
   237	    }
   238	    func chooseProject() -> String? {
   239	        let panel = NSOpenPanel(); panel.canChooseDirectories = true; panel.canChooseFiles = false; panel.prompt = "选择项目"
   240	        return panel.runModal() == .OK ? panel.url?.path : nil
   241	    }
   242	    func chooseAttachments() -> [URL] {
   243	        let panel = NSOpenPanel(); panel.canChooseDirectories = false; panel.allowsMultipleSelection = true
   244	        return panel.runModal() == .OK ? panel.urls : []
   245	    }
   246	    private func scheduleArchive(markDirty: Bool = true) {
   247	        guard !settings.archivePath.isEmpty else { return }
   248	        if markDirty { dirtySince = dirtySince ?? Date() }
   249	        guard dirtySince != nil else { return }
   250	        guard !scanning else { return }
   251	        archiveTask?.cancel()
   252	        let delay = max(0, min(30, 300 - Date().timeIntervalSince(dirtySince!)))
   253	        archiveTask = Task { do { try await Task.sleep(for: .seconds(delay)); await archiveNow() } catch {} }
   254	    }
   255	    func archiveNow() async {
   256	        guard let store, !settings.archivePath.isEmpty, !archiving, !scanning else { return }
   257	        archiving = true; archiveStatus = "正在保存并提交…"
   258	        let path = settings.archivePath, excluded = settings.excludedProjects, roots = settings.locations.map(\.path)
   259	        do {
   260	            let result = try await Task.detached(priority: .utility) {
   261	                let sessions = try store.list().filter { !excluded.contains($0.project) }.compactMap { try store.session($0.id) }
   262	                return try Archive.save(sessions, to: URL(fileURLWithPath: path), sourceRoots: roots)
   263	            }.value
   264	            archiveStatus = result.commit.map { "已保存并提交 · \($0) · \(result.files) 个文件" } ?? "归档已是最新，无需提交"
   265	            lastArchive = Date(); dirtySince = nil
   266	        } catch { archiveStatus = "归档未完成：\(error.localizedDescription)"; self.error = error.localizedDescription }
   267	        archiving = false
   268	    }
   269	    func openDesktop(_ session: Session) { if let url = URL(string: "https://claude.ai/chat/\(session.nativeID)") { NSWorkspace.shared.open(url) } }
   270	    private func collectLoginLinks(_ value: JSONValue) {
   271	        if let url = URL(string: value.string), ["https", "http"].contains(url.scheme ?? ""), !loginLinks.contains(url) { loginLinks.append(url) }
   272	        for item in value.array { collectLoginLinks(item) }
   273	        for item in value.dictionary.values { collectLoginLinks(item) }
   274	    }
   275	    func nativeLogin(_ agent: AgentConfig) async {
   276	        do {
   277	            let result = try await bridge.request("native.login", ["agent": try .encode(agent)])
   278	            NSWorkspace.shared.open(URL(fileURLWithPath: result["terminalScript"].string))
   279	        } catch { self.error = error.localizedDescription }
   280	    }
   281	    func configure(_ configID: String, value: String) async {
   282	        guard let id = selectedID else { return }
   283	        do {
   284	            let result = try await bridge.request("chat.configure", ["id": .string(id), "configID": .string(configID), "value": .string(value)])
   285	            if result["configOptions"] != .null {
   286	                var info = (conversationInfo[id] ?? .object([:])).dictionary; info["configOptions"] = result["configOptions"]; conversationInfo[id] = .object(info)
   287	            }
   288	        } catch { self.error = error.localizedDescription }
   289	    }
   290	    func listNative(_ agent: AgentConfig, project: String, more: Bool = false) async {
   291	        do {
   292	            let result = try await bridge.request("chat.list", ["agent": try .encode(hydrated(agent)), "cwd": .string(project), "cursor": .string(more ? nativeCursor : "")])
   293	            nativeHistory = (more ? nativeHistory : []) + result["sessions"].array
   294	            nativeCursor = result["nextCursor"].string; nativeHistoryProject = project
   295	        } catch { self.error = error.localizedDescription }
   296	    }
   297	    func importNative(_ agent: AgentConfig, record: JSONValue) async -> Bool {
   298	        do {
   299	            let result = try await bridge.request("chat.import", ["agent": try .encode(hydrated(agent)), "cwd": .string(nativeHistoryProject), "session": record])
   300	            let session = try result["session"].decode(Session.self)
   301	            _ = try store?.save(session); try reload(); select(session.id); conversationInfo[session.id] = result["info"]; scheduleArchive(); return true
   302	        } catch { self.error = error.localizedDescription; return false }
   303	    }
   304	}


## tool · 2026-11-16T15:30:43Z


Script completed
Wall time 0.1 seconds
Output:

     1	import { spawn, execFile } from 'node:child_process';
     2	import { promisify } from 'node:util';
     3	import { Readable, Writable } from 'node:stream';
     4	import { mkdir, writeFile, rename, appendFile, readdir, readFile, access } from 'node:fs/promises';
     5	import { join, dirname, extname, basename } from 'node:path';
     6	import { pathToFileURL } from 'node:url';
     7	import { homedir } from 'node:os';
     8	import { randomUUID } from 'node:crypto';
     9	import { query } from '@anthropic-ai/claude-agent-sdk';
    10	import type { Query, SDKUserMessage } from '@anthropic-ai/claude-agent-sdk';
    11	import * as acp from '@agentclientprotocol/sdk';
    12	import * as acp2 from '@agentclientprotocol/sdk/experimental/v2';
    13	import { RpcProcess, childEnvironment } from './rpc.ts';
    14	import { ClientTools } from './client-tools.ts';
    15	import type { Ask } from './client-tools.ts';
    16	import { sessionKey, defaultLocations } from './logs.ts';
    17	import { object, string, content, number } from './types.ts';
    18	import { applyUpdate } from './acp-state.ts';
    19	import { createTerminalAuth } from './terminal-auth.ts';
    20	import type { Data, AgentConfig, Session } from './types.ts';
    21	
    22	export type Emit = (event: string, data: unknown) => void;
    23	interface AcpPeer {
    24	  request: (method: string, params?: unknown, timeout?: number) => Promise<unknown>;
    25	  notify: (method: string, params?: unknown) => Promise<void>;
    26	  close: () => Promise<void>;
    27	  version: number;
    28	  info: Data;
    29	  closed: Promise<void>;
    30	}
    31	interface AcpApp {
    32	  onRequest(method: '*', handler: (ctx: { method: string; params: unknown; signal: AbortSignal }) => Promise<unknown>): unknown;
    33	  onNotification(method: '*', handler: (ctx: { method: string; params: unknown }) => void): unknown;
    34	  connect(stream: acp.Stream): { close(error?: unknown): void; closed: Promise<void>; agent: {
    35	    request<Response = unknown, Params = unknown>(method: string, params?: Params, options?: { signal: AbortSignal }): Promise<Response>;
    36	    notify(method: string, params?: unknown): Promise<void>;
    37	  } };
    38	}
    39	interface Running {
    40	  session: Session; agent: AgentConfig; busy: boolean; rpc?: RpcProcess; peer?: AcpPeer; claude?: Query;
    41	  turnID?: string; finish?: () => void; tools?: ClientTools; deltaID?: string; replaying?: boolean;
    42	  fail?: (error: Error) => void; importing?: boolean; hasActivity?: boolean; writeQueue?: Promise<void>;
    43	}
    44	
    45	export async function defaultAgents(): Promise<AgentConfig[]> {
    46	  const dshBundle = '/Applications/DeepSeek Harness.app/Contents/Resources/runtime/cli/bin/dsh';
    47	  const dsh = await access(dshBundle).then(() => dshBundle, () => 'dsh');
    48	  return [
    49	    { id: 'native-codex', name: 'Codex', kind: 'codex', command: 'codex', args: [], env: {} },
    50	    { id: 'native-claude', name: 'Claude Code', kind: 'claude', command: 'claude', args: [], env: {} },
    51	    { id: 'native-dsh', name: 'DeepSeek Harness', kind: 'dsh', command: dsh, args: ['--profile', 'sdk'], env: {} },
    52	  ];
    53	}
    54	
    55	function validateConfig(value: unknown): AgentConfig {
    56	  const c = object(value);
    57	  if (!string(c.id) || !string(c.command) || !['codex', 'claude', 'dsh', 'acp'].includes(string(c.kind)) || !Array.isArray(c.args) || c.args.some(x => typeof x !== 'string')) throw new Error('Agent 配置无效');
    58	  for (const [name, value] of Object.entries(object(c.env))) if (!/^[a-zA-Z_][a-zA-Z0-9_]*$/.test(name) || typeof value !== 'string') throw new Error('环境变量必须是有效名称和文本值');
    59	  return c as unknown as AgentConfig;
    60	}
    61	
    62	async function openAcp(agent: AgentConfig, cwd: string, ask: Ask, emit: (method: string, params: Data) => void, tools: ClientTools): Promise<AcpPeer> {
    63	  async function connect(version: number): Promise<AcpPeer> {
    64	    const child = spawn(agent.command, agent.args, { cwd, env: childEnvironment(agent.env), stdio: 'pipe', detached: true });
    65	    let stderr = '';
    66	    child.stderr.on('data', data => { stderr = (stderr + String(data)).slice(-3000); });
    67	    const sdk = version === 2 ? acp2 : acp;
    68	    const app = sdk.client({ name: 'Ragdoll' }) as unknown as AcpApp;
    69	    app.onNotification('*', ctx => emit(ctx.method, object(ctx.params)));
    70	    app.onRequest('*', async ctx => {
    71	      const params = object(ctx.params);
    72	      if (ctx.method === 'session/request_permission') {
    73	        const answer = await ask(ctx.method, params, ctx.signal);
    74	        const options = Array.isArray(params.options) ? params.options.map(object) : [];
    75	        const chosen = options.find(o => o.optionId === answer.optionId) ?? options.find(o => answer.allowed === true ? o.kind === 'allow_once' : o.kind === 'reject_once');
    76	        return chosen ? { outcome: { outcome: 'selected', optionId: chosen.optionId } } : { outcome: { outcome: 'cancelled' } };
    77	      }
    78	      if (ctx.method.includes('elicitation')) {
    79	        const answer = await ask(ctx.method, params, ctx.signal);
    80	        return { action: answer.allowed === true ? 'accept' : 'cancel', content: answer.content ?? {} };
    81	      }
    82	      return tools.handle(ctx.method, params, ctx.signal);
    83	    });
    84	    const stream = sdk.ndJsonStream(Writable.toWeb(child.stdin), Readable.toWeb(child.stdout) as ReadableStream<Uint8Array>);
    85	    let mismatch: Error | undefined;
    86	    const readable = stream.readable.pipeThrough(new TransformStream({ transform(message, controller) {
    87	      const result = object(object(message).result);
    88	      if (typeof result.protocolVersion === 'number' && result.protocolVersion !== version) {
    89	        mismatch = new Error(`ACP_PROTOCOL_MISMATCH:${result.protocolVersion}`); controller.error(mismatch); return;
    90	      }
    91	      controller.enqueue(message);
    92	    } }));
    93	    const connection = app.connect({ writable: stream.writable, readable });
    94	    child.on('error', error => connection.close(error));
    95	    child.on('exit', code => connection.close(new Error(`ACP 进程退出 (${code})：${stderr}`)));
    96	    const request = (method: string, params?: unknown, timeout = 30000) => connection.agent.request<unknown, unknown>(method, params, timeout > 0 ? { signal: AbortSignal.timeout(timeout) } : undefined);
    97	    const close = async () => {
    98	      connection.close(); child.stdin.end();
    99	      if (child.pid && child.exitCode === null && child.signalCode === null) {
   100	        const pid = child.pid;
   101	        try { process.kill(-pid, 'SIGTERM'); } catch {}
   102	        const timer = setTimeout(() => { try { process.kill(-pid, 'SIGKILL'); } catch {} }, 3000); timer.unref();
   103	        await new Promise<void>(resolve => { if (child.exitCode !== null || child.signalCode !== null) resolve(); else child.once('exit', () => resolve()); });
   104	        clearTimeout(timer);
   105	      }
   106	    };
   107	    try {
   108	      const info = object(await request('initialize', version === 2
   109	        ? { protocolVersion: 2, info: { name: 'ragdoll', version: '0.1.0' }, capabilities: { auth: { terminal: {} } } }
   110	        : { protocolVersion: 1, clientInfo: { name: 'ragdoll', version: '0.1.0' }, clientCapabilities: { fs: { readTextFile: true, writeTextFile: true }, terminal: true, auth: { terminal: {} } } }));
   111	      if (number(info.protocolVersion) !== version) throw new Error(`ACP_PROTOCOL_MISMATCH:${info.protocolVersion}`);
   112	      return { request, notify: (m, p) => connection.agent.notify(m, p), close, version, info, closed: connection.closed };
   113	    } catch (error) { await close(); throw mismatch ?? error; }
   114	  }
   115	  try { return await connect(agent.protocol ?? 2); }
   116	  catch (error) {
   117	    if (!agent.protocol && /ACP_PROTOCOL_MISMATCH|protocol.?version|unsupported.*version|-32602|-32022/i.test(String(error))) return connect(1);
   118	    throw error;
   119	  }
   120	}
   121	
   122	export class Agents {
   123	  private running = new Map<string, Running>();
   124	  private root: string;
   125	  private emit: Emit;
   126	  private ask: Ask;
   127	  constructor(root: string, emit: Emit, ask: Ask) { this.root = root; this.emit = emit; this.ask = ask; }
   128	
   129	  async saved(): Promise<Session[]> {
   130	    await mkdir(this.root, { recursive: true });
   131	    const entries = await readdir(this.root, { withFileTypes: true });
   132	    const sessions: Session[] = [];
   133	    for (const entry of entries) {
   134	      if (!entry.isDirectory()) continue;
   135	      try {
   136	        const v = object(JSON.parse(await readFile(join(this.root, entry.name, 'session.json'), 'utf8')));
   137	        if (typeof v.id === 'string' && Array.isArray(v.messages) && Array.isArray(v.usage)) sessions.push(v as unknown as Session);
   138	      } catch (error) { if (object(error).code !== 'ENOENT') this.emit('warning', `会话缓存无法读取：${String(error)}`); }
   139	    }
   140	    return sessions;
   141	  }
   142	  private async persist(r: Running): Promise<void> {
   143	    await r.writeQueue;
   144	    const dir = join(this.root, sessionKey('chat', r.session.id));
   145	    await mkdir(dir, { recursive: true });
   146	    r.session.updated = Date.now();
   147	    if (r.session.source === 'acp') r.session.files = [...new Set([join(dir, 'events.jsonl'), ...r.session.files])];
   148	    const path = join(dir, 'session.json');
   149	    await writeFile(path + '.writing', JSON.stringify(r.session)); await rename(path + '.writing', path);
   150	    this.emit('session', r.session);
   151	  }
   152	  private update(r: Running, method: string, params: Data): void {
   153	    const id = r.session.id;
   154	    this.emit('chat', { conversationID: id, method, params });
   155	    if (params.sessionId && params.sessionId !== r.session.nativeID) return;
   156	    if (r.replaying && !r.importing) return;
   157	    if (method === 'item/agentMessage/delta') this.delta(r, string(params.delta), string(params.itemId) || undefined);
   158	    if (method === 'turn/started') r.turnID = string(object(params.turn).id);
   159	    if (method === 'turn/completed') {
   160	      const turn = object(params.turn);
   161	      if (turn.status === 'failed') r.fail?.(new Error(string(object(turn.error).message, 'Codex 执行失败')));
   162	      else r.finish?.();
   163	    }
   164	    if (method === 'session/update') {
   165	      const update = object(params.update);
   166	      const type = string(update.sessionUpdate ?? update.type);
   167	      if (!type.startsWith('user_') || r.importing) {
   168	        const role = type.startsWith('user_') ? 'user' : 'assistant';
   169	        if (type.includes('message') && r.session.messages.find(m => m.id === r.deltaID)?.role !== role) r.deltaID = undefined;
   170	        r.deltaID ||= randomUUID();
   171	        const outcome = applyUpdate(r.session, update, r.deltaID);
   172	        if (type === 'state_update' && update.state === 'running') r.hasActivity = true;
   173	        if (type.startsWith('agent_message')) r.hasActivity = true;
   174	        if (outcome.idle && r.hasActivity && !r.replaying) r.finish?.();
   175	        if (type.startsWith('agent_message') && !r.importing) {
   176	          const message = r.session.messages.find(m => m.id === string(update.messageId, r.deltaID));
   177	          if (message) this.emit('delta', { conversationID: id, message });
   178	        }
   179	        if (type.startsWith('tool_')) r.deltaID = undefined;
   180	      }
   181	      if (type === 'config_option_update' || type === 'config_options_update' || type === 'available_commands_update') this.emit('agentConfiguration', { agentID: r.agent.id, conversationID: id, update });
   182	      if (type.includes('usage')) {
   183	        const value = object(update.usage ?? update);
   184	        if (typeof value.inputTokens === 'number' && typeof value.outputTokens === 'number') {
   185	          const usageID = string(value.id, `${id}:turn:${r.session.messages.filter(m => m.role === 'user').length}`);
   186	          const u = { id: usageID, time: Date.now(), model: string(value.model), input: number(value.inputTokens), output: number(value.outputTokens), cacheRead: number(value.cachedReadTokens), cacheWrite: number(value.cachedWriteTokens) };
   187	          const old = r.session.usage.findIndex(u => u.id === usageID);
   188	          if (old < 0) r.session.usage.push(u); else r.session.usage[old] = u;
   189	        }
   190	      }
   191	      const dir = join(this.root, sessionKey('chat', id));
   192	      r.writeQueue = (r.writeQueue ?? Promise.resolve()).then(async () => { await mkdir(dir, { recursive: true }); await appendFile(join(dir, 'events.jsonl'), JSON.stringify({ time: Date.now(), method, params }) + '\n'); });
   193	      void r.writeQueue.catch(error => this.emit('warning', `会话事件保存失败：${String(error)}`));
   194	    }
   195	    if (method === 'session.event') {
   196	      const e = object(params.event), d = object(e.data), message = object(d.message);
   197	      if (e.type === 'assistant/delta') this.delta(r, string(d.text ?? d.delta));
   198	      if (e.type === 'assistant/message') {
   199	        const text = content(message.content ?? d.content);
   200	        if (text) {
   201	          const existing = r.session.messages.find(m => m.id === r.deltaID);
   202	          if (existing) existing.text = text;
   203	          else r.session.messages.push({ id: randomUUID(), role: 'assistant', text, time: Date.now(), kind: 'text' });
   204	        }
   205	        r.deltaID = undefined;
   206	      }
   207	    }
   208	    if (method === 'session.status' && (params.status === 'idle' || object(params.status).status === 'idle')) r.finish?.();
   209	  }
   210	  private delta(r: Running, text: string, preferredID?: string): void {
   211	    if (!text) return;
   212	    if (preferredID && r.deltaID !== preferredID) r.deltaID = preferredID;
   213	    r.deltaID ||= randomUUID();
   214	    if (!r.session.messages.some(m => m.id === r.deltaID)) r.session.messages.push({ id: r.deltaID, role: 'assistant', text: '', time: Date.now(), kind: 'text' });
   215	    const message = r.session.messages.find(m => m.id === r.deltaID)!; message.text += text;
   216	    this.emit('delta', { conversationID: r.session.id, message });
   217	  }
   218	
   219	  async probe(agentValue: unknown, cwd: string): Promise<Data> {
   220	    const agent = validateConfig(agentValue);
   221	    if (agent.kind === 'acp') {
   222	      const tools = new ClientTools(cwd, this.ask);
   223	      const peer = await openAcp(agent, cwd, this.ask, (m, p) => this.emit('agentEvent', { agentID: agent.id, method: m, params: p }), tools);
   224	      try { return { ...peer.info, protocolVersion: peer.version }; } finally { await peer.close(); tools.close(); }
   225	    }
   226	    if (agent.kind === 'codex') {
   227	      const rpc = new RpcProcess(agent.command, [...agent.args, 'app-server'], cwd, agent.env);
   228	      try {
   229	        const info = object(await rpc.request('initialize', { clientInfo: { name: 'ragdoll', version: '0.1.0' }, capabilities: { experimentalApi: true } }));
   230	        rpc.notify('initialized');
   231	        const models = await rpc.request('model/list', {});
   232	        return { ...info, models };
   233	      } finally { await rpc.close(); }
   234	    }
   235	    if (agent.kind === 'dsh') {
   236	      const rpc = new RpcProcess(agent.command, agent.args, cwd, agent.env);
   237	      try { return object(await rpc.request('initialize', { cwd, provider: 'deepseek-official', model: 'deepseek-v4-flash', maxTokens: 32768, approvalRequests: true })); }
   238	      finally { await rpc.close(); }
   239	    }
   240	    const result = await promisify(execFile)(agent.command, ['--version'], { cwd, env: childEnvironment(agent.env), timeout: 15000 });
   241	    return { name: 'Claude Code', version: result.stdout.trim() };
   242	  }
   243	
   244	  async start(value: Data): Promise<Data> {
   245	    const agent = validateConfig(value.agent), cwd = string(value.cwd, homedir());
   246	    await access(cwd);
   247	    const prior = value.session ? object(value.session) as unknown as Session : undefined;
   248	    if (prior && this.running.has(prior.id)) return { session: this.running.get(prior.id)!.session };
   249	    if (prior && prior.source !== 'acp' && prior.source !== agent.kind) throw new Error('此历史会话必须使用原始工具恢复');
   250	    if (prior?.instanceID && prior.instanceID !== agent.id) throw new Error('此会话属于其他 Agent 实例');
   251	    const homeKey = agent.kind === 'codex' ? 'CODEX_HOME' : agent.kind === 'claude' ? 'CLAUDE_CONFIG_DIR' : 'DSH_HOME';
   252	    const home = prior?.home || agent.env[homeKey] || defaultLocations().find(l => l.source === agent.kind)?.path || '';
   253	    if (agent.kind !== 'acp' && home) agent.env = { ...agent.env, [homeKey]: home };
   254	    const session: Session = prior ? structuredClone(prior) : {
   255	      id: `chat:${randomUUID()}`, nativeID: '', source: agent.kind, instanceID: agent.id,
   256	      title: '新对话', project: cwd, home, created: Date.now(), updated: Date.now(), messages: [], usage: [], files: [], warnings: [],
   257	    };
   258	    const r: Running = { session, agent, busy: false };
   259	    let info: Data = {};
   260	    if (agent.kind === 'codex') {
   261	      const rpc = new RpcProcess(agent.command, [...agent.args, 'app-server'], cwd, agent.env); r.rpc = rpc;
   262	      rpc.onNotification = (m, p) => this.update(r, m, p);
   263	      rpc.onExit = message => r.fail?.(new Error(message));
   264	      rpc.onRequest = async (method, params) => {
   265	        const answer = await this.ask(method, { ...params, conversationID: session.id });
   266	        if (method.includes('requestUserInput')) return { answers: answer.answers ?? {} };
   267	        return { decision: answer.allowed === true ? 'accept' : 'decline' };
   268	      };
   269	      try {
   270	        await rpc.request('initialize', { clientInfo: { name: 'ragdoll', version: '0.1.0' }, capabilities: { experimentalApi: true } }); rpc.notify('initialized');
   271	        info = object(await rpc.request(prior ? 'thread/resume' : 'thread/start', { ...(prior ? { threadId: prior.nativeID } : {}), cwd, approvalPolicy: 'on-request', sandbox: 'workspace-write', ...(value.model ? { model: value.model } : {}) }));
   272	        info = { ...info, models: await rpc.request('model/list', {}) };
   273	        const id = string(object(info.thread).id);
   274	        if (!id) throw new Error('Codex 返回的会话缺少 ID');
   275	        session.nativeID = id;
   276	      } catch (error) { await rpc.close(); throw error; }
   277	    }
   278	    if (agent.kind === 'dsh') {
   279	      const rpc = new RpcProcess(agent.command, agent.args, cwd, agent.env); r.rpc = rpc;
   280	      rpc.onNotification = (m, p) => this.update(r, m, p);
   281	      rpc.onExit = message => r.fail?.(new Error(message));
   282	      rpc.onRequest = async (method, params) => {
   283	        const answer = await this.ask(method, { ...params, conversationID: session.id });
   284	        if (method === 'approval/request') return { outcome: answer.allowed === true ? 'allowed-once' : 'rejected' };
   285	        return answer.allowed === true ? { answers: answer.answers ?? [] } : { cancelled: true };
   286	      };
   287	      try {
   288	        info = object(await rpc.request('initialize', { cwd, provider: session.provider || 'deepseek-official', model: string(value.model, session.usage.at(-1)?.model || 'deepseek-v4-flash'), maxTokens: 32768, approvalRequests: true, capabilities: { userQuestions: true } }));
   289	        session.nativeID ||= randomUUID();
   290	        if (prior) await rpc.request('session/resume', { sessionId: session.nativeID });
   291	      } catch (error) { await rpc.close(); throw error; }
   292	    }
   293	    if (agent.kind === 'acp') {
   294	      const ask: Ask = (m, p, signal) => this.ask(m, { ...p, conversationID: session.id }, signal);
   295	      r.tools = new ClientTools(cwd, ask);
   296	      const peer = await openAcp(agent, cwd, ask, (m, p) => this.update(r, m, p), r.tools); r.peer = peer;
   297	      try {
   298	        if (prior) {
   299	          const capabilities = object(peer.info.agentCapabilities ?? peer.info.capabilities);
   300	          const sessions = object(capabilities.session ?? capabilities.sessionCapabilities);
   301	          if (peer.version === 2 ? capabilities.session == null : capabilities.loadSession !== true && !sessions.resume) throw new Error('此 ACP Agent 未声明历史恢复能力；已保存的会话仍可浏览和归档');
   302	          r.replaying = true;
   303	          r.importing = prior.messages.length === 0;
   304	          info = object(await peer.request(peer.version === 1 && capabilities.loadSession === true ? 'session/load' : 'session/resume', { sessionId: prior.nativeID, cwd, mcpServers: [], ...(peer.version === 2 && r.importing ? { replayFrom: { type: 'start' } } : {}) }));
   305	          r.replaying = false;
   306	          r.importing = false;
   307	        } else {
   308	          info = object(await peer.request('session/new', { cwd, mcpServers: [] }));
   309	          session.nativeID = string(info.sessionId);
   310	          if (!session.nativeID) throw new Error('ACP Agent 返回的会话缺少 ID');
   311	        }
   312	      } catch (error) { await peer.close(); r.tools.close(); throw error; }
   313	      info = { ...peer.info, ...info, protocolVersion: peer.version };
   314	    }
   315	    if (agent.kind === 'claude') session.nativeID ||= randomUUID();
   316	    if (!prior) session.id = sessionKey(agent.kind, `${agent.kind === 'acp' ? agent.id : home}\0${session.nativeID}`);
   317	    if (agent.kind === 'acp') {
   318	      const nativeSource = agent.registryID === 'codex-acp' ? 'codex' : agent.registryID === 'claude-acp' ? 'claude' : /(?:^|\/)dsh$/.test(agent.command) && agent.args.includes('acp') ? 'dsh' : undefined;
   319	      if (nativeSource) {
   320	        session.nativeSource = nativeSource;
   321	        const key = nativeSource === 'codex' ? 'CODEX_HOME' : nativeSource === 'claude' ? 'CLAUDE_CONFIG_DIR' : 'DSH_HOME';
   322	        session.home = agent.env[key] || defaultLocations().find(l => l.source === nativeSource)?.path || '';
   323	      }
   324	    }
   325	    session.instanceID = agent.id;
   326	    this.running.set(session.id, r);
   327	    await this.persist(r);
   328	    return { session, info };
   329	  }
   330	
   331	  async send(id: string, text: string, model?: string, attachments: unknown = []): Promise<void> {
   332	    const r = this.running.get(id);
   333	    if (!r) throw new Error('请先打开或恢复会话');
   334	    if (r.busy) throw new Error('此会话正在执行，请等待或停止当前执行');
   335	    if (!text.trim()) throw new Error('消息不能为空');
   336	    if (!Array.isArray(attachments) || attachments.some(p => typeof p !== 'string')) throw new Error('附件列表无效');
   337	    const files = await Promise.all((attachments as string[]).map(async path => {
   338	      const mime = ({ '.png': 'image/png', '.jpg': 'image/jpeg', '.jpeg': 'image/jpeg', '.webp': 'image/webp', '.gif': 'image/gif' } as Record<string, 'image/png' | 'image/jpeg' | 'image/webp' | 'image/gif'>)[extname(path).toLowerCase()];
   339	      if (mime) {
   340	        const data = await readFile(path);
   341	        if (data.length > 20 * 1024 * 1024) throw new Error('单张图片不能超过 20 MiB');
   342	        return { path, mime, data: data.toString('base64') };
   343	      }
   344	      await access(path); return { path, mime: undefined, data: undefined };
   345	    }));
   346	    if (r.peer && files.some(f => f.mime)) {
   347	      const capabilities = object(r.peer.info.agentCapabilities ?? r.peer.info.capabilities);
   348	      const prompts = object(r.peer.version === 2 ? object(capabilities.session).prompt : capabilities.promptCapabilities);
   349	      if (prompts.image !== true) throw new Error('此 ACP Agent 未声明图片输入能力');
   350	    }
   351	    const visibleText = text + (files.length ? '\n\n' + files.map(f => `[附件：${basename(f.path)}](${pathToFileURL(f.path).href})`).join('\n') : '');
   352	    const withPaths = text + (files.some(f => !f.mime) ? '\n\n附件路径：\n' + files.filter(f => !f.mime).map(f => f.path).join('\n') : '');
   353	    r.busy = true; r.deltaID = undefined; r.hasActivity = false;
   354	    r.session.files = [...new Set([...r.session.files, ...files.map(f => f.path)])];
   355	    r.session.messages.push({ id: randomUUID(), role: 'user', text: visibleText, time: Date.now(), kind: 'text' });
   356	    if (r.session.title === '新对话') r.session.title = text.slice(0, 80);
   357	    await this.persist(r); this.emit('state', { conversationID: id, state: 'running' });
   358	    try {
   359	      if (r.peer) {
   360	        if (model) await r.peer.request('session/set_config_option', { sessionId: r.session.nativeID, configId: 'model', value: model, ...(r.peer.version === 2 ? { type: 'id' } : {}) });
   361	        const completed = new Promise<void>((resolve, reject) => { r.finish = resolve; r.fail = reject; });
   362	        const blocks = files.map(f => f.mime ? { type: 'image', data: f.data, mimeType: f.mime } : { type: 'resource_link', uri: pathToFileURL(f.path).href, name: basename(f.path) });
   363	        await r.peer.request('session/prompt', { sessionId: r.session.nativeID, prompt: [{ type: 'text', text }, ...blocks] }, 0);
   364	        if (r.peer.version === 2) await Promise.race([completed, r.peer.closed.then(() => { throw new Error('ACP 连接中断，运行结果尚未确认'); })]);
   365	      } else if (r.agent.kind === 'codex') {
   366	        const completed = new Promise<void>((resolve, reject) => { r.finish = resolve; r.fail = reject; });
   367	        const result = object(await r.rpc!.request('turn/start', { threadId: r.session.nativeID, input: [{ type: 'text', text: withPaths }, ...files.filter(f => f.mime).map(f => ({ type: 'localImage', path: f.path }))], ...(model ? { model } : {}) }));
   368	        r.turnID = string(object(result.turn).id); await completed;
   369	      } else if (r.agent.kind === 'dsh') {
   370	        await r.rpc!.request('session/prompt', { sessionId: r.session.nativeID, contentBlocks: [{ type: 'text', text: withPaths }, ...files.filter(f => f.mime).map(f => ({ type: 'image', data: f.data, mimeType: f.mime }))] });
   371	        await r.rpc!.request('session/wait', { sessionId: r.session.nativeID }, 0);
   372	      } else {
   373	        const resumed = r.session.messages.some(m => m.role === 'assistant') || r.session.files.length > 0;
   374	        const images = files.filter((f): f is typeof f & { mime: 'image/png' | 'image/jpeg' | 'image/webp' | 'image/gif'; data: string } => f.mime !== undefined && f.data !== undefined);
   375	        async function* input(): AsyncGenerator<SDKUserMessage> {
   376	          yield { type: 'user', session_id: r!.session.nativeID, parent_tool_use_id: null, message: { role: 'user', content: [{ type: 'text', text: withPaths }, ...images.map(f => ({ type: 'image' as const, source: { type: 'base64' as const, media_type: f.mime, data: f.data } }))] } };
   377	        }
   378	        const q = query({ prompt: images.length ? input() : withPaths, options: {
   379	          cwd: r.session.project, pathToClaudeCodeExecutable: r.agent.command, env: { ...childEnvironment(r.agent.env), CLAUDE_CODE_MAX_OUTPUT_TOKENS: '32768' },
   380	          ...(resumed ? { resume: r.session.nativeID } : { sessionId: r.session.nativeID }),
   381	          ...(model ? { model } : {}), maxTurns: 64, includePartialMessages: true, permissionMode: 'default',
   382	          canUseTool: async (name, input, options) => {
   383	            const answer = await this.ask(name, { input, conversationID: id }, options.signal);
   384	            return answer.allowed === true ? { behavior: 'allow', updatedInput: { ...input, ...object(answer.updatedInput) } } : { behavior: 'deny', message: '用户拒绝此次操作' };
   385	          },
   386	        } });
   387	        r.claude = q;
   388	        try { for await (const message of q) {
   389	          const raw = object(message);
   390	          if (raw.type === 'stream_event') {
   391	            const event = object(raw.event), delta = object(event.delta);
   392	            if (delta.type === 'text_delta') this.delta(r, string(delta.text));
   393	          }
   394	          if (raw.type === 'assistant') {
   395	            const m = object(raw.message), text = content(m.content);
   396	            const existing = r.session.messages.find(m => m.id === r.deltaID);
   397	            if (existing) existing.text = text;
   398	            else if (text) r.session.messages.push({ id: randomUUID(), role: 'assistant', text, time: Date.now(), kind: 'text' });
   399	            r.deltaID = undefined;
   400	            const u = object(m.usage);
   401	            if (Object.keys(u).length) r.session.usage.push({ id: string(m.id, randomUUID()), time: Date.now(), model: string(m.model), input: number(u.input_tokens), output: number(u.output_tokens), cacheRead: number(u.cache_read_input_tokens), cacheWrite: number(u.cache_creation_input_tokens) });
   402	          }
   403	          this.emit('chat', { conversationID: id, method: 'claude/message', params: raw });
   404	          if (raw.type === 'result' && raw.is_error === true) throw new Error(string(raw.result, JSON.stringify(raw.errors ?? 'Claude 执行失败')));
   405	        } } finally { q.close(); r.claude = undefined; }
   406	      }
   407	      this.emit('state', { conversationID: id, state: 'idle' });
   408	    } catch (error) {
   409	      this.emit('state', { conversationID: id, state: 'error', message: String(error) }); throw error;
   410	    } finally { r.busy = false; r.finish = undefined; r.fail = undefined; await this.persist(r); }
   411	  }
   412	  async stop(id: string): Promise<void> {
   413	    const r = this.running.get(id); if (!r) return;
   414	    if (r.peer && r.busy) await r.peer.notify('session/cancel', { sessionId: r.session.nativeID });
   415	    if (r.claude) { try { await r.claude.interrupt(); } catch (error) { this.emit('warning', `Claude 中断返回：${String(error)}`); } finally { r.claude.close(); r.claude = undefined; } }
   416	    if (r.rpc && r.agent.kind === 'codex' && r.turnID) await r.rpc.request('turn/interrupt', { threadId: r.session.nativeID, turnId: r.turnID }).catch(() => {});
   417	    await r.peer?.close(); await r.rpc?.close(); r.tools?.close(); r.finish?.();
   418	    this.running.delete(id); this.emit('state', { conversationID: id, state: 'stopped' });
   419	    await this.persist(r);
   420	  }
   421	  async configure(id: string, configId: string, value: string): Promise<unknown> {
   422	    const r = this.running.get(id); if (!r?.peer) throw new Error('此会话没有 ACP 配置项');
   423	    if (configId === '__legacy_mode') return r.peer.request('session/set_mode', { sessionId: r.session.nativeID, modeId: value });
   424	    if (configId === '__legacy_model') return r.peer.request('session/set_model', { sessionId: r.session.nativeID, modelId: value });
   425	    const parsed: string | boolean = value === 'true' ? true : value === 'false' ? false : value;
   426	    return r.peer.request('session/set_config_option', { sessionId: r.session.nativeID, configId, value: parsed, ...(r.peer.version === 2 ? { type: typeof parsed === 'boolean' ? 'boolean' : 'id' } : {}) });
   427	  }
   428	  async list(agentValue: unknown, cwd: string, cursor?: string): Promise<unknown> {
   429	    const agent = validateConfig(agentValue), tools = new ClientTools(cwd, this.ask);
   430	    const peer = await openAcp(agent, cwd, this.ask, () => {}, tools);
   431	    try {
   432	      const caps = object(peer.info.agentCapabilities ?? peer.info.capabilities), session = object(caps.session ?? caps.sessionCapabilities);
   433	      if (peer.version === 2 ? caps.session == null : !session.list) throw new Error('此 Agent 未声明会话列举能力');
   434	      return await peer.request('session/list', { cwd, ...(cursor ? { cursor } : {}) });
   435	    } finally { await peer.close(); tools.close(); }
   436	  }
   437	  async authenticate(agentValue: unknown, cwd: string, methodID: string): Promise<unknown> {
   438	    const agent = validateConfig(agentValue), tools = new ClientTools(cwd, this.ask);
   439	    const peer = await openAcp(agent, cwd, this.ask, (method, params) => this.emit('agentEvent', { agentID: agent.id, method, params }), tools);
   440	    try {
   441	      const methods = Array.isArray(peer.info.authMethods) ? peer.info.authMethods.map(object) : [];
   442	      const method = methods.find(m => string(m.id ?? m.methodId) === methodID);
   443	      if (!method) throw new Error('Agent 未声明此认证方法');
   444	      if (method.type === 'terminal') return createTerminalAuth(agent, method, cwd, dirname(this.root));
   445	      return await peer.request(peer.version === 2 ? 'auth/login' : 'authenticate', { methodId: methodID }, 0);
   446	    }
   447	    finally { await peer.close(); tools.close(); }
   448	  }
   449	  async close(): Promise<void> { for (const id of this.running.keys()) await this.stop(id); }
   450	
   451	  async importNative(agentValue: unknown, record: Data, cwd: string): Promise<Data> {
   452	    const agent = validateConfig(agentValue), nativeID = string(record.sessionId);
   453	    if (!nativeID) throw new Error('Agent 历史条目缺少会话 ID');
   454	    const session: Session = { id: sessionKey('acp', `${agent.id}\0${nativeID}`), nativeID, source: 'acp', instanceID: agent.id, title: string(record.title, nativeID), project: string(record.cwd, cwd), home: '', created: Date.now(), updated: Date.now(), messages: [], usage: [], files: [], warnings: [] };
   455	    return this.start({ agent, session, cwd: session.project });
   456	  }
   457	}


## tool · 2026-11-16T15:30:56Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 10636)
Total output lines: 2

{"i":0,"output":"     1\timport { createInterface } from 'node:readline';\n     2\timport { watch } from 'node:fs';\n     3\timport type { FSWatcher } from 'node:fs';\n     4\timport { mkdir } from 'node:fs/promises';\n     5\timport { join, resolve } from 'node:path';\n     6\timport { homedir } from 'node:os';\n     7\timport { randomUUID } from 'node:crypto';\n     8\timport { once } from 'node:events';\n     9\timport { scan, defaultLocations } from './logs.ts';\n    10\timport { importDesktop } from './desktop.ts';\n    11\timport { registry, install, uninstall } from './registry.ts';\n    12\timport { Agents, defaultAgents } from './agents.ts';\n    13\timport { createTerminalAuth, runTerminalAuth } from './terminal-auth.ts';\n    14\timport { fileURLToPath } from 'node:url';\n    15\timport { object, string } from './types.ts';\n    16\timport type { Data, Location, AgentConfig } from './types.ts';\n    17\t\n    18\tconst dataArg = process.argv.indexOf('--data-dir');\n    19\tconst root = dataArg >= 0 ? resolve(process.argv[dataArg + 1]) : join(homedir(), 'Library/Application Support/Ragdoll');\n    20\tprocess.env.RAGDOLL_MAIN_SCRIPT = fileURLToPath(import.meta.url);\n    21\tconst output = (value: unknown) => process.stdout.write(JSON.stringify(value) + '\\n');\n    22\tconst emit = (event: string, data: unknown) => output({ event, data });\n    23\tasync function sessionOutput(data: unknown): Promise<void> {\n    24\t  if (!output({ event: 'session', data })) await once(process.stdout, 'drain');\n    25\t}\n    26\tconst approvals = new Map<string, { resolve: (value: Data) => void; remove: () => void }>();\n    27\tconst agents = new Agents(join(root, 'conversations'), emit, (method, params, signal) => new Promise(resolve => {\n    28\t  const requestID = randomUUID();\n    29\t  const cancel = () => { approvals.delete(requestID); emit('approvalCancelled', { requestID }); resolve({ allowed: false }); };\n    30\t  if (signal?.aborted) return cancel();\n    31\t  signal?.addEventListener('abort', cancel, { once: true });\n    32\t  approvals.set(requestID, { resolve, remove: () => signal?.removeEventListener('abort', cancel) });\n    33\t  emit('approval', { requestID, method, params });\n    34\t}));\n    35\tlet watchers: FSWatcher[] = [];\n    36\tlet scanActive = false;\n    37\tlet changeTimer: NodeJS.Timeout | undefined;\n    38\tfunction watchLocations(locations: Location[]): void {\n    39\t  for (const watcher of watchers) watcher.close(); watchers = [];\n    40\t  for (const location of locations) {\n    41\t    try {\n    42\t      const watcher = watch(location.path, { recursive: true }, () => {\n    43\t        clearTimeout(changeTimer); changeTimer = setTimeout(() => emit('sourceChanged', {}), 1500);\n    44\t      });\n    45\t      watcher.on('error', error => emit('warning', `目录监听失败：${String(error)}`));\n    46\t      watchers.push(watcher);\n    47\t    } catch (error) { if (object(error).code !== 'ENOENT') emit('warning', `目录监听失败：${String(error)}`); }\n    48\t  }\n    49\t}\n    50\t\n    51\tasync function handle(method: string, p: Data): Promise<unknown> {\n    52\t  if (method === 'initialize') return { version: '0.1.0', locations: defaultLocations(), agents: await defaultAgents() };\n    53\t  if (method === 'scan') {\n    54\t    if (scanActive) throw new Error('正在扫描，请稍后重试');\n    55\t    const locations = p.locations === undefined ? defaultLocations() : p.locations;\n    56\t    if (!Array.isArray(locations) || locations.some(v => !['codex', 'claude', 'dsh'].includes(string(object(v).source)) || !string(object(v).path))) throw new Error('扫描目录配置无效');\n    57\t    scanActive = true;\n    58\t    try {\n    59\t      watchLocations(locations as Location[]);\n    60\t      for (const session of await agents.saved()) await sessionOutput(session);\n    61\t      let count = 0;\n    62\t      await scan(locations as Location[], async s => { count++; await sessionOutput(s); }, error => emit('warning', error));\n    63\t      return { count };\n    64\t    } finally { scanActive = false; }\n    65\t  }\n    66\t  if (method === 'import') {\n    67\t    const sessions = await importDesktop(string(p.path), join(root, 'imports'));\n    68\t    for (const session of sessions) emit('session', session);\n    69\t    return { count: sessions.length };\n    70\t  }\n    71\t  if (method === 'registry') return registry();\n    72\t  if (method === 'install') return install(p.agent, join(root, 'tools'));\n    73\t  if (method === 'uninstall') { await uninstall(p.agent as AgentConfig, join(root, 'tools')); return {}; }\n    74\t  if (method === 'probe') return agents.probe(p.agent, string(p.cwd, homedir()));\n    75\t  if (method === 'chat.start') return agents.start(p);\n    76\t  if (method === 'chat.send') { await agents.send(string(p.id), string(p.text), string(p.model) || undefined, p.attachments ?? []); return {}; }\n    77\t  if (method === 'chat.stop') { await agents.stop(string(p.id)); return {}; }\n    78\t  if (method === 'chat.configure') return agents.configure(string(p.id), string(p.configID), string(p.value));\n    79\t  if (method === 'chat.list') return agents.list(p.agent, string(p.cwd, homedir()), string(p.cursor) || undefined);\n    80\t  if (method === 'chat.import') return agents.importNative(p.agent, object(p.session), string(p.cwd, homedir()));\n    81\t  if (method === 'native.login') {\n    82\t    const agent = p.agent as AgentConfig;\n    83\t    if (agent.kind !== 'codex' && agent.kind !== 'claude') throw new Error('请使用原应用管理此工具的登录');\n    84\t    return createTerminalAuth({ ...agent, args: [] }, { args: agent.kind === 'codex' ? ['login'] : ['auth', 'login'] }, homedir(), root);\n    85\t  }\n    86\t  if (method === 'authenticate') return agents.authenticate(p.agent, string(p.cwd, homedir()), string(p.methodID));\n    87\t  if (method === 'approval') {\n    88\t    const pending = approvals.get(string(p.requestID));\n    89\t    if (!pending) throw new Error('权限请求已经取消或结束');\n    90\t    approvals.delete(string(p.requestID)); pending.remove(); pending.resolve(object(p.answer)); return {};\n    91\t  }\n    92\t  if (method === 'shutdown') { await agents.close(); for (const watcher of watchers) watcher.close(); return {}; }\n    93\t  throw new Error(`未知助手方法：${method}`);\n    94\t}\n    95\t\n    96\tif (process.argv.includes('--terminal-auth')) {\n    97\t  try { process.exitCode = await runTerminalAuth(process.argv[process.argv.indexOf('--terminal-auth') + 1]); }\n    98\t  catch (error) { process.stderr.write(`${String(error)}\\n`); process.exitCode = 1; }\n    99\t} else if (process.argv.includes('--self-check')) {\n   100\t  output({ status: 'ok', version: '0.1.0', node: process.version, agents: await defaultAgents() });\n   101\t} else {\n   102\t  await mkdir(root, { recursive: true });\n   103\t  const input = createInterface({ input: process.stdin });\n   104\t  input.on('line', line => {\n   105\t    let request: Data;\n   106\t    try {\n   107\t      request = object(JSON.parse(line));\n   108\t      if ((typeof request.id !== 'number' && typeof request.id !== 'string') || typeof request.method !== 'string') throw new Error('请求必须包含 id 和 method');\n   109\t    } catch (error) { output({ id: null, error: { status: 'error', type: 'InvalidRequest', message: String(error), suggestion: '发送有效的 NDJSON 请求' } }); return; }\n   110\t    void handle(request.method as string, object(request.params)).then(\n   111\t      result => output({ id: request.id, result }),\n   112\t      error => output({ id: request.id, error: { status: 'error', type: error instanceof Error ? error.name : 'RuntimeError', message: String(error), suggestion: '检查 Agent 配置、登录状态或运行日志后重试' } }),\n   113\t    );\n   114\t  });\n   115\t  input.on('close', () => {\n   116\t    for (const approval of approvals.values()) { approval.remove(); approval.resolve({ allowed: false }); }\n   117\t    for (const watcher of watchers) watcher.close(); clearTimeout(changeTimer);\n   118\t    void agents.close().finally(() => process.exit(0));\n   119\t  });\n   120\t}\n     1\timport { spawn } from 'node:child_process';\n     2\timport type { ChildProcessWithoutNullStreams } from 'node:child_process';\n     3\timport { createInterface } from 'node:readline';\n     4\timport { object, string } from './types.ts';\n     5\timport type { Data } from './types.ts';\n     6\t\n     7\texport function childEnvironment(env: Record<string, string> = {}): NodeJS.ProcessEnv {\n     8\t  const result: NodeJS.ProcessEnv = { ...process.env, PATH: `${process.env.PATH || ''}:/opt/homebrew/bin:/usr/local/bin`, ...env };\n     9\t  delete result.ELECTRON_RUN_AS_NODE;\n    10\t  return result;\n    11\t}\n    12\t\n    13\texport class RpcProcess {\n    14\t  readonly child: ChildProcessWithoutNullStreams;\n    15\t  private serial = 0;\n    16\t  private pending = new Map<string, { resolve: (v: unknown) => void; reject: (e: Error) => void; timer?: NodeJS.Timeout }>();\n    17\t  private stderr = '';\n    18\t  onNotification: (method: string, params: Data) => void = () => {};\n    19\t  onRequest: (method: string, params: Data) => Promise<unknown> = async method => { throw new Error(`不支持代理请求：${method}`); };\n    20\t  onExit: (message: string) => void = () => {};\n    21\t  private stopped = false;\n    22\t\n    23\t  constructor(command: string, args: string[], cwd: string, env: Record<string, string> = {}) {\n    24\t    if (!command || command.includes('\\0')) throw new Error('请设置有效程序路径');\n    25\t    this.child = spawn(command, args, { cwd, env: childEnvironment(env), stdio: 'pipe', detached: true });\n    26\t    this.child.stderr.on('data', data => { this.stderr = (this.stderr + String(data)).slice(-4000); });\n    27\t    this.child.on('error', error => this.fail(error));\n    28\t    this.child.on('exit', (code, signal) => {\n    29\t      this.fail(new Error(`代理进程已退出 (${code ?? signal})：${this.stderr}`));\n    30\t      if (!this.stopped) this.onExit(`代理进程已退出 (${code ?? signal})`);\n    31\t    });\n    32\t    const input = createInterface({ input: this.child.stdout });\n    33\t    input.on('line', line => {\n    34\t      let message: Data;\n    35\t      try { message = object(JSON.parse(line)); }\n    36\t      catch { this.fail(new Error('代理 stdout 包含无效 JSON-RPC 数据')); void this.close(); return; }\n    37\t      if ('method' in message) {\n    38\t        if ('id' in message) {\n    39\t          void this.onRequest(string(message.method), object(message.params)).then(\n    40\t            result => this.write({ jsonrpc: '2.0', id: message.id, result }),\n    41\t            error => this.write({ jsonrpc: '2.0', id: message.id, error: { code: -32603, message: String(error) } }),\n    42\t          );\n    43\t        } else this.onNotification(string(message.method), object(message.params));\n    44\t      } else if ('id' in message) {\n    45\t        const key = String(message.id), pending = this.pending.get(key);\n    46\t        if (!pending) return;\n    47\t        this.pending.delete(key); clearTimeout(pending.timer);\n    48\t        if (message.error) pending.reject(new Error(JSON.stringify(message.error)));\n    49\t        else pending.resolve(message.result);\n    50\t      }\n    51\t    });\n    52\t  }\n    53\t  private write(message: unknown): void {\n    54\t    if (this.child.stdin.destroyed) return;\n    55\t    this.child.stdin.write(JSON.stringify(message) + '\\n');\n    56\t  }\n    57\t  request(method: string, params: unknown = {}, timeout = 30000): Promise<unknown> {\n    58\t    if (this.stopped) return Promise.reject(new Error('代理进程已经停止'));\n    59\t    const id = ++this.serial;\n    60\t    return new Promise((resolve, reject) => {\n    61\t      const timer = timeout > 0 ? setTimeout(() => { this.pending.delete(String(id)); reject(new Error(`代理请求超时：${method}`)); }, timeout) : undefined;\n    62\t      this.pending.set(String(id), { resolve, reject, timer });\n    63\t      this.write({ jsonrpc: '2.0', id, method, params });\n    64\t    });\n    65\t  }\n    66\t  notify(method: string, params: unknown = {}): void { this.write({ jsonrpc: '2.0', method, params }); }\n    67\t  private fail(error: Error): void {\n    68\t    for (const pending of this.pending.values()) { clearTimeout(pending.timer); pending.reject(error); }\n    69\t    this.pending.clear();\n    70\t  }\n    71\t  async close(): Promise<void> {\n    72\t    if (this.stopped) return;\n    73\t    this.stopped = true; this.child.stdin.end();\n    74\t    const pid = this.child.pid;\n    75\t    if (pid && this.child.exitCode === null) {\n    76\t      try { process.kill(-pid, 'SIGTERM'); } catch { /* 进程已经退出。 */ }\n    77\t      const timer = setTimeout(() => { try { process.kill(-pid, 'SIGKILL'); } catch { /* 进程已经退出。 */ } }, 3000);\n    78\t      timer.unref();\n    79\t      await new Promise<void>(resolve => { if (this.child.exitCode !== null) resolve(); else this.child.once('exit', () => resolve()); });\n    80\t      clearTimeout(timer);\n    81\t    }\n    82\t    this.fail(new Error('执行已停止'));\n    83\t  }\n    84\t}\n     1\timport { readFile, writeFile, rename, realpath } from 'node:fs/promises';\n     2\timport { resolve, dirname } from 'node:path';\n     3\timport { spawn } from 'node:child_process';\n     4\timport type { ChildProcessWithoutNullStreams } from 'node:child_process';\n     5\timport { randomUUID } from 'node:crypto';\n     6\timport { object, string, number } from './types.ts';\n     7\timport { childEnvironment } from './rpc.ts';\n     8\timport type { Data } from './types.ts';\n     9\t\n    10\texport type Ask = (method: string, params: Data, signal?: AbortSignal) => Promise<Data>;\n    11\t\n    12\texport class ClientTools {\n    13\t  private terminals = new Map<string, { child: ChildProcessWithoutNullStreams; output: string; done: Promise<unknown>; status?: Data }>();\n    14\t  private cwd: string;\n    15\t  private ask: Ask;\n    16\t  constructor(cwd: string, ask: Ask) { this.cwd = cwd; this.ask = ask; }\n    17\t  private async path(value: unknown): Promise<string> {\n    18\t    if (typeof value !== 'string') throw new Error('缺少文件路径');\n    19\t    const path = resolve(this.cwd, value), root = await realpath(this.cwd);\n    20\t    const target = await realpath(path).catch(async error => { if (object(error).code !== 'ENOENT') throw error; return resolve(await realpath(dirname(path)), path.split('/').at(-1)!); });\n    21\t    if (target !== root && !target.startsWith(root + '/')) throw new Error('文件路径超出当前项目授权范围');\n    22\t    return target;\n    23\t  }\n    24\t  async handle(method: string, p: Data, signal?: AbortSignal): Promise<unknown> {\n    25\t    if (method === 'fs/read_text_file') {\n    26\t      const data = await readFile(await this.path(p.path), 'utf8');\n    27\t      const start = Math.max(0, number(p.line || 1) - 1);\n    28\t      return { content: data.split('\\n').slice(start, p.limit ? start + number(p.limit) : undefined).join('\\n') };\n    29\t    }\n    30\t    if (method === 'fs/write_text_file') {\n    31\t      const path = await this.path(p.path);\n    32\t      if ((await this.ask(method, p, signal)).allowed !== true) throw new Error('用户拒绝写入文件');\n    33\t      if (typeof p.content !== 'string') throw new Error('文件内容必须为文本');\n    34\t      const temp = `${path}.ragdoll-${randomUUID()}`;\n    35\t      await writeFile(temp, p.content); await rename(temp, path); return {};\n    36\t    }\n    37\t    if (method === 'terminal/create') {\n    38\t      const cwd = await this.path(p.cwd ?? this.cwd);\n    39\t      if ((await this.ask(method, p, signal)).allowed !== true) throw new Error('用户拒绝执行命令');\n    40\t      if (typeof p.command !== 'string' || !Array.isArray(p.args ?? []) || (p.args as unknown[] | undefined)?.some(v => typeof v !== 'string')) throw new Error('命令参数无效');\n    41\t      const id = randomUUID();\n    42\t      const env: Record<string, string> = {};\n    43\t      for (const value of Array.isArray(p.env) ? p.env : []) { const pair = object(value); if (typeof pair.name === 'string' && typeof pair.value === 'string') env[pair.name] = pair.value; }\n    44\t      const child = spawn(p.command, p.args as string[] ?? [], { cwd, env: childEnvironment(env), stdio: 'pipe', detached: true });\n    45\t      const entry: { child: ChildProcessWithoutNullStreams; output: string; done: Promise<unknown>; status?: Data } = { child, output: '', done: Promise.resolve() };\n    46\t      const append = (data: Buffer) => { entry.output = (entry.output + data.toString()).slice(-256000); };\n    47\t      child.stdout.on('data', append); child.stderr.on('data', append);\n    48\t      entry.done = new Promise(resolve => {\n    49\t        child.on('error', error => { entry.output += String(error); entry.status = { exitCode: 1 }; resolve(entry.status); });\n    50\t        child.on('exit', (exitCode, signal) => { entry.status = { exitCode, signal }; resolve(entry.status); });\n    51\t      });\n    52\t      this.terminals.set(id, entry); return { terminalId: id };\n    53\t    }\n    54\t    if (method.startsWith('terminal/')) {\n    55\t      const id = string(p.terminalId), entry = this.terminals.get(id);\n    56\t      if (!entry) throw new Error('未知终端');\n    57\t      if (method === 'terminal/output') return { output: entry.output, truncated: entry.output.length >= 256000, exitStatus: entry.status };\n    58\t      if (method === 'terminal/wait_for_exit') return await entry.done;\n    59\t      if (method === 'terminal/kill' || method === 'terminal/release') {\n    60\t        if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }\n    61\t        if (method === 'terminal/release') this.terminals.delete(id);\n    62\t        return {};\n    63\t      }\n    64\t    }\n    65\t    throw new Error(`不支持的客户端方法：${method}`);\n    66\t  }\n    67\t  close(): void {\n    68\t    for (const entry of this.terminals.values()) if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }\n    69\t    this.terminals.clear();\n    70\t  }\n    71\t}\n     1\timport type { Session, Data } from './types.ts';\n     2\timport { object, string, content } from './types.ts';\n     3\t\n     4\texport function applyUpdate(session: Session, update: Data, fallbackID: string): { idle: boolean } {\n     5\t  const type = string(update.sessionUpdate ?? update.type);\n     6\t  if (['agent_message_chunk', 'agent_message', 'user_message_chunk', 'user_message'].includes(type)) {\n     7\t    const id = string(update.messageId, fallbackID), role = type.startsWith('user') ? 'user' : 'assistant';\n     8\t    const existing = session.messages.find(m => m.id === id);\n     9\t    const text = content(update.content);\n    10\t    if (existing) {\n    11\t      if (type.endsWith('chunk')) existing.text += text;\n    12\t      else if ('content' in update) existing.text = text;\n    13\t    } else session.messages.push({ id, role, text, time: Date.now(), kind: 'text' });\n    14\t  }\n    15\t  if (type === 'tool_call' || type === 'tool_call_update') {\n    16\t    const id = string(update.toolCallId, fallbackID);\n    17\t    const existing = session.messages.find(m => m.id === id);\n    18\t    const text = `${string(update.title)}\\n${content(update.content ?? update.rawInput ?? update.rawOutput)}`;\n    19\t    if (existing) { if (text.trim()) e…636 tokens truncated…udes('..')) throw new Error(`不安全的安装路径：${path}`);\n    18\t  return full;\n    19\t}\n    20\t\n    21\texport function pinnedPackage(spec: string, version: string, python: boolean): string {\n    22\t  if (!/^\\d+\\.\\d+\\.\\d+(?:[-.][a-zA-Z0-9.-]+)?$/.test(version)) throw new Error('Registry 缺少有效版本');\n    23\t  if (python) {\n    24\t    const match = /^([a-zA-Z0-9][a-zA-Z0-9._-]*)(?:==([^\\s]+))?$/.exec(spec);\n    25\t    if (!match || (match[2] && match[2] !== version)) throw new Error('Python 包必须使用目录中的精确版本');\n    26\t    return `${match[1]}==${version}`;\n    27\t  }\n    28\t  const match = /^(@[a-z0-9._-]+\\/[a-z0-9._-]+|[a-z0-9._-]+)(?:@([^\\s]+))?$/.exec(spec);\n    29\t  if (!match || (match[2] && match[2] !== version)) throw new Error('npm 包必须使用目录中的精确版本');\n    30\t  return `${match[1]}@${version}`;\n    31\t}\n    32\t\n    33\texport function validateAgent(value: unknown): RegistryAgent {\n    34\t  const v = object(value);\n    35\t  if (!/^[a-z0-9]+(?:-[a-z0-9]+)*$/.test(string(v.id)) || !string(v.name) || !/^\\d+\\.\\d+\\.\\d+/.test(string(v.version)) || !Object.keys(object(v.distribution)).length) throw new Error('无效的 ACP Registry 条目');\n    36\t  return { id: string(v.id), name: string(v.name), version: string(v.version), description: string(v.description), repository: string(v.repository), license: string(v.license), license_url: string(v.license_url), distribution: object(v.distribution) };\n    37\t}\n    38\t\n    39\texport async function registry(): Promise<RegistryAgent[]> {\n    40\t  const response = await fetch(registryURL, { signal: AbortSignal.timeout(30000) });\n    41\t  if (!response.ok) throw new Error(`Registry 请求失败：HTTP ${response.status}`);\n    42\t  const body = object(await response.json());\n    43\t  if (!Array.isArray(body.agents)) throw new Error('Registry 缺少 agents 列表');\n    44\t  return body.agents.map(validateAgent);\n    45\t}\n    46\t\n    47\texport async function extractArchive(data: Uint8Array, url: string, root: string): Promise<void> {\n    48\t  if (/\\.zip(?:\\?|$)/i.test(url)) {\n    49\t    let declared = 0;\n    50\t    const entries = unzipSync(data, { filter: file => { declared += file.originalSize; if (declared > 1024 * 1024 * 1024) throw new Error('解压文件超过 1 GiB'); return true; } });\n    51\t    let total = 0;\n    52\t    for (const [path, bytes] of Object.entries(entries)) {\n    53\t      const full = safePath(root, path);\n    54\t      total += bytes.length;\n    55\t      if (total > 1024 * 1024 * 1024) throw new Error('解压文件超过 1 GiB');\n    56\t      if (path.endsWith('/')) { await mkdir(full, { recursive: true }); continue; }\n    57\t      await mkdir(dirname(full), { recursive: true });\n    58\t      await writeFile(full, bytes, { flag: 'wx' });\n    59\t    }\n    60\t    return;\n    61\t  }\n    62\t  const archive = join(root, '.archive');\n    63\t  await writeFile(archive, data);\n    64\t  let total = 0;\n    65\t  let invalid: Error | undefined;\n    66\t  await listTar({ file: archive, strict: true, onReadEntry: entry => {\n    67\t    if (entry.path === './' || entry.path === '.') return;\n    68\t    try {\n    69\t      safePath(root, entry.path);\n    70\t      if (!['File', 'Directory', 'ExtendedHeader', 'GlobalExtendedHeader'].includes(entry.type)) throw new Error('安装包不允许符号链接或硬链接');\n    71\t      total += entry.size;\n    72\t      if (total > 1024 * 1024 * 1024) throw new Error('解压文件超过 1 GiB');\n    73\t    } catch (error) { invalid = error instanceof Error ? error : new Error(String(error)); }\n    74\t  } });\n    75\t  if (invalid) throw invalid;\n    76\t  await extractTar({ file: archive, cwd: root, strict: true, preservePaths: false });\n    77\t  await rm(archive);\n    78\t}\n    79\t\n    80\tfunction literalArgs(value: unknown): string[] {\n    81\t  if (value === undefined) return [];\n    82\t  if (!Array.isArray(value) || value.some(v => typeof v !== 'string')) throw new Error('Agent 参数必须为字符串数组');\n    83\t  return value as string[];\n    84\t}\n    85\t\n    86\texport async function install(agentValue: unknown, tools: string): Promise<AgentConfig> {\n    87\t  const agent = validateAgent(agentValue);\n    88\t  const parent = safePath(tools, agent.id), target = safePath(parent, agent.version);\n    89\t  const stage = safePath(parent, `.install-${randomUUID()}`);\n    90\t  await mkdir(stage, { recursive: true });\n    91\t  let directTarget = false;\n    92\t  try {\n    93\t    let command: string, args: string[], env: Record<string, string> = {};\n    94\t    const binary = object(object(agent.distribution.binary)['darwin-aarch64']);\n    95\t    if (binary.archive) {\n    96\t      const url = new URL(string(binary.archive));\n    97\t      if (url.protocol !== 'https:') throw new Error('安装包必须使用 HTTPS');\n    98\t      const response = await fetch(url, { signal: AbortSignal.timeout(120000) });\n    99\t      if (!response.ok) throw new Error(`下载失败：HTTP ${response.status}`);\n   100\t      if (!response.body) throw new Error('安装包响应为空');\n   101\t      const reader = response.body.getReader(), chunks: Uint8Array[] = [];\n   102\t      let length = 0;\n   103\t      while (true) {\n   104\t        const chunk = await reader.read(); if (chunk.done) break;\n   105\t        length += chunk.value.length;\n   106\t        if (length > 512 * 1024 * 1024) { await reader.cancel(); throw new Error('安装包超过 512 MiB'); }\n   107\t        chunks.push(chunk.value);\n   108\t      }\n   109\t      const bytes = Buffer.concat(chunks);\n   110\t      if (binary.sha256) {\n   111\t        if (!/^[a-f0-9]{64}$/i.test(string(binary.sha256)) || createHash('sha256').update(bytes).digest('hex') !== string(binary.sha256).toLowerCase()) throw new Error('安装包 SHA-256 校验失败');\n   112\t      }\n   113\t      const archive = /\\.(zip|tar\\.gz|tgz|tar\\.bz2|tbz2)(?:\\?|$)/i.test(url.pathname);\n   114\t      const relative = string(binary.cmd);\n   115\t      safePath(stage, relative);\n   116\t      if (archive) await extractArchive(bytes, url.href, stage);\n   117\t      else { await mkdir(dirname(safePath(stage, relative)), { recursive: true }); await writeFile(safePath(stage, relative), bytes); }\n   118\t      await chmod(safePath(stage, relative), 0o755);\n   119\t      command = safePath(target, relative); args = literalArgs(binary.args);\n   120\t      for (const [key, value] of Object.entries(object(binary.env))) {\n   121\t        if (typeof value !== 'string') throw new Error('Agent 环境变量必须为字符串');\n   122\t        env[key] = value;\n   123\t      }\n   124\t    } else if (agent.distribution.npx) {\n   125\t      const distribution = object(agent.distribution.npx);\n   126\t      const spec = pinnedPackage(string(distribution.package), agent.version, false);\n   127\t      const npm = join(dirname(process.execPath), '../lib/node_modules/npm/bin/npm-cli.js');\n   128\t      const npmExists = await stat(npm).then(() => true, () => false);\n   129\t      const npmCommand = npmExists ? process.execPath : 'npm';\n   130\t      const prefix = npmExists ? [npm] : [];\n   131\t      await exec(npmCommand, [...prefix, 'install', '--prefix', stage, '--cache', join(tools, '.npm-cache'), '--ignore-scripts', '--no-audit', '--no-fund', spec], { timeout: 240000, maxBuffer: 4 * 1024 * 1024 });\n   132\t      const packageName = spec.replace(/@[^@]+$/, '');\n   133\t      const pkg = object(JSON.parse(await readFile(join(stage, 'node_modules', packageName, 'package.json'), 'utf8')));\n   134\t      const bin = typeof pkg.bin === 'string' ? pkg.bin : Object.values(object(pkg.bin))[0];\n   135\t      if (typeof bin !== 'string') throw new Error('npm 包没有可执行入口');\n   136\t      const installed = join('node_modules', packageName, bin);\n   137\t      safePath(stage, installed);\n   138\t      command = process.execPath; args = [safePath(target, installed), ...literalArgs(distribution.args)];\n   139\t    } else if (agent.distribution.uvx) {\n   140\t      const distribution = object(agent.distribution.uvx);\n   141\t      const spec = pinnedPackage(string(distribution.package), agent.version, true);\n   142\t      await mkdir(target); directTarget = true;\n   143\t      const uvEnv = { ...process.env, UV_TOOL_DIR: join(target, 'python-tools'), UV_TOOL_BIN_DIR: join(target, 'bin'), UV_CACHE_DIR: join(tools, '.uv-cache') };\n   144\t      try { await exec('uv', ['tool', 'install', spec], { env: uvEnv, timeout: 240000, maxBuffer: 4 * 1024 * 1024 }); }\n   145\t      catch (error) { if (object(error).code === 'ENOENT') throw new Error('需要安装 uv：请先安装 uv，再重试此 Python Agent'); throw error; }\n   146\t      const entries = await readdir(join(target, 'bin'));\n   147\t      const supplied = literalArgs(distribution.args);\n   148\t      const entry = supplied[0] && entries.includes(supplied[0]) ? supplied.shift()! : entries[0];\n   149\t      if (!entry) throw new Error('Python 包没有可执行入口');\n   150\t      command = safePath(target, `bin/${entry}`); args = supplied;\n   151\t    } else throw new Error('此 Agent 没有适用于 macOS Apple Silicon 的分发包');\n   152\t    const config: AgentConfig = { id: agent.id, name: agent.name, kind: 'acp', command, args, env, version: agent.version, registryID: agent.id, installPath: target };\n   153\t    if (directTarget) {\n   154\t      await writeFile(join(target, 'ragdoll-agent.json'), JSON.stringify(config));\n   155\t      await rm(stage, { recursive: true, force: true }); return config;\n   156\t    }\n   157\t    await writeFile(join(stage, 'ragdoll-agent.json'), JSON.stringify(config));\n   158\t    try { await rename(stage, target); }\n   159\t    catch (error) {\n   160\t      if (object(error).code !== 'ENOTEMPTY' && object(error).code !== 'EEXIST') throw error;\n   161\t      const existing = JSON.parse(await readFile(join(target, 'ragdoll-agent.json'), 'utf8')) as AgentConfig;\n   162\t      await rm(stage, { recursive: true, force: true }); return existing;\n   163\t    }\n   164\t    return config;\n   165\t  } catch (error) { await rm(stage, { recursive: true, force: true }); if (directTarget) await rm(target, { recursive: true, force: true }); throw error; }\n   166\t}\n   167\t\n   168\texport async function uninstall(config: AgentConfig, tools: string): Promise<void> {\n   169\t  if (!config.registryID || !config.installPath) return;\n   170\t  const parent = safePath(tools, config.registryID);\n   171\t  if (!resolve(config.installPath).startsWith(parent + '/')) throw new Error('拒绝删除应用安装目录以外的文件');\n   172\t  await rm(config.installPath, { recursive: true, force: true });\n   173\t}\n     1\timport { readFile, writeFile, mkdir, rename } from 'node:fs/promises';\n     2\timport { join } from 'node:path';\n     3\timport { unzipSync } from 'fflate';\n     4\timport { object, string, timestamp, content } from './types.ts';\n     5\timport { sessionKey } from './logs.ts';\n     6\timport type { Session } from './types.ts';\n     7\t\n     8\texport function importConversations(value: unknown): Session[] {\n     9\t  if (!Array.isArray(value)) throw new Error('请选择包含 conversations.json 的 Claude 官方导出包');\n    10\t  return value.map(record => {\n    11\t    const v = object(record);\n    12\t    if (!string(v.uuid) || !Array.isArray(v.chat_messages)) throw new Error('导出记录缺少 uuid 或 chat_messages');\n    13\t    const session: Session = {\n    14\t      id: sessionKey('desktop', string(v.uuid)), nativeID: string(v.uuid), source: 'desktop',\n    15\t      title: string(v.name, 'Claude 聊天'), project: '', home: '',\n    16\t      created: timestamp(v.created_at), updated: timestamp(v.updated_at), messages: [], usage: [], files: [],\n    17\t      warnings: ['普通聊天用量不可用；此记录在导入后不会实时同步'],\n    18\t    };\n    19\t    for (const item of v.chat_messages) {\n    20\t      const m = object(item);\n    21\t      session.messages.push({ id: string(m.uuid, String(session.messages.length)), role: m.sender === 'human' ? 'user' : 'assistant', text: content(m.content) || string(m.text), time: timestamp(m.created_at), kind: 'text' });\n    22\t      if ((Array.isArray(m.attachments) && m.attachments.length) || (Array.isArray(m.files) && m.files.length)) session.warnings.push('原始上传附件未包含在官方导出包中');\n    23\t    }\n    24\t    session.warnings = [...new Set(session.warnings)];\n    25\t    return session;\n    26\t  });\n    27\t}\n    28\t\n    29\texport async function importDesktop(path: string, root: string): Promise<Session[]> {\n    30\t  const data = await readFile(path);\n    31\t  let value: unknown;\n    32\t  if (path.toLowerCase().endsWith('.zip')) {\n    33\t    const files = unzipSync(data, { filter: entry => /(^|\\/)conversations\\.json$/.test(entry.name) && entry.originalSize < 512 * 1024 * 1024 });\n    34\t    const found = Object.values(files)[0];\n    35\t    if (!found) throw new Error('导出包中未找到 conversations.json');\n    36\t    value = JSON.parse(new TextDecoder().decode(found));\n    37\t  } else value = JSON.parse(data.toString('utf8'));\n    38\t  const sessions = importConversations(value);\n    39\t  await mkdir(root, { recursive: true });\n    40\t  for (const [index, session] of sessions.entries()) {\n    41\t    const file = join(root, session.id.replace(':', '_') + '.json');\n    42\t    await writeFile(file + '.writing', JSON.stringify((value as unknown[])[index], null, 2));\n    43\t    await rename(file + '.writing', file);\n    44\t    session.files = [file];\n    45\t  }\n    46\t  return sessions;\n    47\t}\n     1\timport { mkdir, writeFile, readFile, rm } from 'node:fs/promises';\n     2\timport { join } from 'node:path';\n     3\timport { fileURLToPath } from 'node:url';\n     4\timport { spawn, execFile } from 'node:child_process';\n     5\timport { promisify } from 'node:util';\n     6\timport { randomUUID } from 'node:crypto';\n     7\timport { childEnvironment } from './rpc.ts';\n     8\timport { object, string } from './types.ts';\n     9\timport type { AgentConfig, Data } from './types.ts';\n    10\t\n    11\tconst quote = (value: string) => `'${value.replaceAll(\"'\", \"'\\\\''\")}'`;\n    12\t\n    13\texport async function createTerminalAuth(agent: AgentConfig, method: Data, cwd: string, root: string): Promise<Data> {\n    14\t  if (!Array.isArray(method.args ?? []) || (method.args as unknown[] | undefined)?.some(a => typeof a !== 'string')) throw new Error('终端认证参数无效');\n    15\t  const dir = join(root, 'auth'); await mkdir(dir, { recursive: true });\n    16\t  const path = join(dir, `${randomUUID()}.json`), script = path.replace(/\\.json$/, '.command');\n    17\t  await writeFile(path, JSON.stringify({ agent: { ...agent, env: {} }, method, cwd }), { mode: 0o600 });\n    18\t  const main = process.env.RAGDOLL_MAIN_SCRIPT || fileURLToPath(import.meta.url).replace(/\\/terminal-auth\\.ts$/, '/main.ts');\n    19\t  const command = [process.execPath, main, '--terminal-auth', path].map(quote).join(' ');\n    20\t  await writeFile(script, `#!/bin/sh\\n${command}\\nresult=$?\\nprintf '\\\\n登录进程已结束，退出码：%s\\\\n请返回 Ragdoll 检测连接。\\\\n' \"$result\"\\nexit \"$result\"\\n`, { mode: 0o700 });\n    21\t  return { terminalScript: script };\n    22\t}\n    23\t\n    24\texport async function runTerminalAuth(path: string): Promise<number> {\n    25\t  const value = object(JSON.parse(await readFile(path, 'utf8'))), agent = object(value.agent), method = object(value.method);\n    26\t  let secrets: Record<string, string> = {};\n    27\t  try {\n    28\t    const result = await promisify(execFile)('/usr/bin/security', ['find-generic-password', '-s', 'Ragdoll.AgentEnvironment', '-a', string(agent.id), '-w']);\n    29\t    secrets = JSON.parse(result.stdout.trim()) as Record<string, string>;\n    30\t  } catch (error) { if (object(error).code !== 44) throw new Error('无法从钥匙串读取 Agent 环境变量'); }\n    31\t  const methodEnv: Record<string, string> = {};\n    32\t  if (Array.isArray(method.env)) {\n    33\t    for (const value of method.env) { const v = object(value); if (typeof v.name === 'string' && typeof v.value === 'string') methodEnv[v.name] = v.value; }\n    34\t  } else for (const [key, value] of Object.entries(object(method.env))) if (typeof value === 'string') methodEnv[key] = value;\n    35\t  const args = [...(agent.args as string[] ?? []), ...(method.args as string[] ?? [])];\n    36\t  try {\n    37\t    return await new Promise<number>((resolve, reject) => {\n    38\t      const child = spawn(string(agent.command), args, { cwd: string(value.cwd), stdio: 'inherit', env: childEnvironment({ ...secrets, ...methodEnv }) });\n    39\t      child.on('error', reject); child.on('exit', code => resolve(code ?? 1));\n    40\t    });\n    41\t  } finally { await rm(path, { force: true }); }\n    42\t}\n     1\t#!/bin/bash\n     2\tset -euo pipefail\n     3\troot=$(cd \"$(dirname \"$0\")/..\" && pwd)\n     4\tcd \"$root\"\n     5\texport CLANG_MODULE_CACHE_PATH=\"$root/.cache/clang\"\n     6\texport SWIFT_MODULECACHE_PATH=\"$root/.cache/swift-modules\"\n     7\tmkdir -p .cache dist\n     8\tswift build -c release --cache-path .cache/swift --config-path .cache/swift-config --security-path .cache/swift-security --disable-sandbox\n     9\tnpm --prefix runtime ci --ignore-scripts --cache \"$root/.cache/npm\"\n    10\tnpm --prefix runtime run build\n    11\tnode_version=26.13.0\n    12\tnode_name=\"node-v${node_version}-darwin-arm64\"\n    13\tif [ ! -x \".cache/$node_name/bin/node\" ]; then\n    14\t  curl --fail --location --retry 2 \"https://nodejs.org/dist/v${node_version}/${node_name}.tar.gz\" -o \".cache/${node_name}.tar.gz\"\n    15\t  curl --fail --location \"https://nodejs.org/dist/v${node_version}/SHASUMS256.txt\" -o .cache/SHASUMS256.txt\n    16\t  rg \" ${node_name}\\.tar\\.gz$\" .cache/SHASUMS256.txt > .cache/node-checksums.txt\n    17\t  (cd .cache && shasum -a 256 -c node-checksums.txt)\n    18\t  tar -xzf \".cache/${node_name}.tar.gz\" -C .cache\n    19\tfi\n    20\tstage=\"$root/dist/Ragdoll.staging.app\"\n    21\tif [ -d \"$stage\" ]; then rm -rf \"$stage\"; fi\n    22\tmkdir -p \"$stage/Contents/MacOS\" \"$stage/Contents/Resources/runtime/app\"\n    23\ttrap 'rm -rf \"$stage\"' EXIT\n    24\tcp .build/release/Ragdoll \"$stage/Contents/MacOS/Ragdoll\"\n    25\tcp packaging/Info.plist \"$stage/Contents/Info.plist\"\n    26\tcp -R \".cache/$node_name\" \"$stage/Contents/Resources/runtime/node\"\n    27\tcp runtime/package.json runtime/package-lock.json \"$stage/Contents/Resources/runtime/app/\"\n    28\tcp -R runtime/dist \"$stage/Contents/Resources/runtime/app/dist\"\n    29\tnpm --prefix \"$stage/Contents/Resources/runtime/app\" ci --omit=dev --omit=optional --ignore-scripts --cache \"$root/.cache/npm\"\n    30\tfor bundle in .build/release/*.bundle; do\n    31\t  if [ -d \"$bundle\" ]; then cp -R \"$bundle\" \"$stage/Contents/Resources/\"; fi\n    32\tdone\n    33\tcp -R docs \"$stage/Contents/Resources/docs\"\n    34\tcodesign --force --deep --sign - \"$stage\"\n    35\tcodesign --verify --deep --strict \"$stage\"\n    36\t\"$stage/Contents/Resources/runtime/node/bin/node\" \"$stage/Contents/Resources/runtime/app/dist/main.mjs\" --self-check\n    37\tif [ -d dist/Ragdoll.previous.app ]; then rm -rf dist/Ragdoll.previous.app; fi\n    38\tif [ -d dist/Ragdoll.app ]; then mv dist/Ragdoll.app dist/Ragdoll.previous.app; fi\n    39\tmv \"$stage\" dist/Ragdoll.app\n    40\ttrap - EXIT\n    41\techo \"Built: $root/dist/Ragdoll.app\"\n"}

## tool · 2026-11-16T15:31:00Z


Script completed
Wall time 0.1 seconds
Output:

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
    71	                pending.append(chunk)
    72	                while let index = pending.firstIndex(of: 10) {
    73	                    let line = pending.prefix(upTo: index); pending.removeSubrange(...index)
    74	                    await self?.receive(Data(line))
    75	                }
    76	            }
    77	        }
    78	        let errorReader = errors.fileHandleForReading
    79	        Task.detached { [weak self] in
    80	            while true { let data = errorReader.availableData; if data.isEmpty { break }; await self?.errorOutput(String(decoding: data, as: UTF8.self)) }
    81	        }
    82	    }
    83	    public func request(_ method: String, _ params: [String: JSONValue] = [:], timeout: Double = 120) async throws -> JSONValue {
    84	        guard let input else { throw failure("SDK 助手尚未启动") }
    85	        serial += 1; let id = String(serial)
    86	        let message = try JSONEncoder().encode(JSONValue.object(["id": .string(id), "method": .string(method), "params": .object(params)])) + Data([10])
    87	        return try await withCheckedThrowingContinuation { continuation in
    88	            pending[id] = continuation
    89	            do { try input.write(contentsOf: message) }
    90	            catch { pending.removeValue(forKey: id)?.resume(throwing: error) }
    91	            if timeout > 0 { Task { try? await Task.sleep(for: .seconds(timeout)); timedOut(id, method) } }
    92	        }
    93	    }
    94	    private func timedOut(_ id: String, _ method: String) { pending.removeValue(forKey: id)?.resume(throwing: failure("助手请求超时：\(method)。运行中的操作不会自动重试。")) }
    95	    private func receive(_ data: Data) async {
    96	        do {
    97	            let message = try JSONDecoder().decode(JSONValue.self, from: data)
    98	            if !message["event"].string.isEmpty { await handler?(message["event"].string, message["data"]); return }
    99	            let id = message["id"].string
   100	            guard let continuation = pending.removeValue(forKey: id) else { return }
   101	            if message["error"] != .null { continuation.resume(throwing: failure(message["error"]["message"].string)) }
   102	            else { continuation.resume(returning: message["result"]) }
   103	        } catch { await handler?("warning", .string("助手返回无效数据：\(error.localizedDescription)")) }
   104	    }
   105	    private func errorOutput(_ text: String) { stderr = String((stderr + text).suffix(4000)) }
   106	    private func terminated(_ code: Int32) async {
   107	        process = nil; input = nil
   108	        let error = failure("SDK 助手已退出（\(code)）：\(stderr)")
   109	        for continuation in pending.values { continuation.resume(throwing: error) }; pending.removeAll()
   110	        await handler?("disconnected", .string(error.localizedDescription))
   111	    }
   112	    public func close() async {
   113	        _ = try? await request("shutdown", timeout: 5)
   114	        try? input?.close(); process?.terminate()
   115	    }
   116	    private func failure(_ message: String) -> NSError { NSError(domain: "Ragdoll.Runtime", code: 1, userInfo: [NSLocalizedDescriptionKey: message]) }
   117	}
     1	import SwiftUI
     2	import AppKit
     3	import RagdollCore
     4	
     5	@main
     6	struct RagdollApp: App {
     7	    @StateObject private var model = AppModel()
     8	    var body: some Scene {
     9	        WindowGroup {
    10	            RootView().environmentObject(model).frame(minWidth: 1050, minHeight: 720).task { await model.launch() }
    11	        }
    12	        .defaultSize(width: 1380, height: 900)
    13	        .commands {
    14	            CommandGroup(after: .newItem) {
    15	                Button("导入 Claude 导出包…") { model.importDesktop() }.keyboardShortcut("i", modifiers: [.command, .shift])
    16	                Button("刷新会话") { Task { await model.refresh() } }.keyboardShortcut("r")
    17	                Button("立即归档") { Task { await model.archiveNow() } }.keyboardShortcut("s", modifiers: [.command, .shift])
    18	            }
    19	        }
    20	    }
    21	}
     1	import SwiftUI
     2	import RagdollCore
     3	
     4	struct ConversationView: View {
     5	    @EnvironmentObject var model: AppModel
     6	    var canCreate: Bool
     7	    @State private var newChat = false
     8	    @State private var prompt = ""
     9	    @State private var messageLimit = 100
    10	    @State private var sending = false
    11	    @State private var showEvents = false
    12	    @State private var attachments: [URL] = []
    13	    var body: some View {
    14	        HSplitView {
    15	            VStack(spacing: 0) {
    16	                HStack {
    17	                    Text(canCreate ? "对话" : "历史会话").font(.headline)
    18	                    Spacer()
    19	                    if canCreate { Button { newChat = true } label: { Image(systemName: "square.and.pencil") }.buttonStyle(.plain).help("新建对话") }
    20	                }.padding(16)
    21	                TextField("搜索标题与消息", text: $model.query).textFieldStyle(.roundedBorder).padding(.horizontal, 12).padding(.bottom, 10)
    22	                    .onChange(of: model.query) { _, _ in do { try model.reload() } catch { model.error = error.localizedDescription } }
    23	                HStack {
    24	                    Picker("来源", selection: $model.source) {
    25	                        Text("全部").tag("all")
    26	                        ForEach(["codex", "claude", "dsh", "desktop", "acp"], id: \.self) { Text(sourceName($0)).tag($0) }
    27	                    }.labelsHidden()
    28	                    if !model.project.isEmpty || model.heatmapFilter != nil {
    29	                        Button("清除筛选") { model.project = ""; model.heatmapFilter = nil }.font(.caption)
    30	                    }
    31	                }.padding(.horizontal, 12).padding(.bottom, 8)
    32	                List(selection: Binding(get: { model.selectedID }, set: { model.select($0); messageLimit = 100 })) {
    33	                    ForEach(model.filtered) { session in
    34	                        VStack(alignment: .leading, spacing: 7) {
    35	                            HStack(alignment: .top) {
    36	                                Text(session.title).font(.system(size: 12, weight: .medium)).lineLimit(2)
    37	                                Spacer(minLength: 0)
    38	                                if model.running.contains(session.id) { ProgressView().controlSize(.mini) }
    39	                            }
    40	                            HStack { Text(sourceName(session.source)); Spacer(); Text(compact(session.tokens)) }.font(.system(size: 10)).foregroundStyle(.secondary)
    41	                            Text(session.projectName).font(.system(size: 10)).foregroundStyle(.tertiary).lineLimit(1)
    42	                        }.padding(.vertical, 7).tag(session.id)
    43	                    }
    44	                }.listStyle(.sidebar)
    45	                Text("\(model.filtered.count) 个会话").font(.caption2).foregroundStyle(.secondary).frame(maxWidth: .infinity, alignment: .leading).padding(12)
    46	            }.frame(minWidth: 245, idealWidth: 285, maxWidth: 340)
    47	            if let session = model.selected {
    48	                VStack(spacing: 0) {
    49	                    header(session)
    50	                    Divider()
    51	                    ScrollViewReader { proxy in
    52	                        ScrollView {
    53	                            LazyVStack(alignment: .leading, spacing: 22) {
    54	                                if session.messages.count > messageLimit { Button("加载更早的消息（剩余 \(session.messages.count - messageLimit) 条）") { messageLimit += 100 }.frame(maxWidth: .infinity) }
    55	                                ForEach(Array(session.messages.suffix(messageLimit))) { message in MessageView(message: message).id(message.id) }
    56	                                if session.messages.isEmpty { ContentUnavailableView("尚无消息", systemImage: "bubble.left", description: Text("恢复会话后可在下方输入消息。")) }
    57	                                Color.clear.frame(height: 1).id("bottom")
    58	                            }.padding(26).frame(maxWidth: 1000).frame(maxWidth: .infinity)
    59	                        }
    60	                        .onChange(of: model.selected?.messages.last?.text) { _, _ in if sending { proxy.scrollTo("bottom", anchor: .bottom) } }
    61	                        .onChange(of: model.selectedID) { _, _ in proxy.scrollTo("bottom", anchor: .bottom) }
    62	                    }
    63	                    if showEvents {
    64	                        DisclosureGroup("最近运行事件", isExpanded: .constant(true)) {
    65	                            ScrollView { Text((model.toolEvents[session.id] ?? []).suffix(15).map(\.text).joined(separator: "\n\n")).font(.system(size: 10, design: .monospaced)).textSelection(.enabled).frame(maxWidth: .infinity, alignment: .leading) }.frame(height: 160)
    66	                        }.padding(.horizontal, 20)
    67	                    }
    68	                    if !session.warnings.isEmpty { Text(session.warnings.joined(separator: " · ")).font(.caption2).foregroundStyle(.orange).lineLimit(3).frame(maxWidth: .infinity, alignment: .leading).padding(.horizontal, 20).padding(.vertical, 8) }
    69	                    if session.source == "desktop" {
    70	                        HStack { Text("官方导出记录 · 更新时需重新导入").foregroundStyle(.secondary); Spacer(); Button("打开原聊天") { model.openDesktop(session) } }.padding(20)
    71	                    } else { composer(session) }
    72	                }.frame(minWidth: 550)
    73	            } else {
    74	                VStack(spacing: 18) {
    75	                    Image(systemName: "bubble.left.and.bubble.right").font(.system(size: 40, weight: .ultraLight)).foregroundStyle(.secondary)
    76	                    Text(canCreate ? "开始一段对话" : "选择一个历史会话").font(.title2.weight(.medium))
    77	                    Text(canCreate ? "选择项目和 Agent，使用原生接口或 ACP 开始工作。" : "浏览本地记录，或导入 Claude 官方导出包。").font(.callout).foregroundStyle(.secondary)
    78	                    if canCreate { Button("新建对话") { newChat = true }.buttonStyle(.borderedProminent) }
    79	                    else { Button("导入 Claude 聊天…") { model.importDesktop() } }
    80	                }.frame(maxWidth: .infinity, maxHeight: .infinity)
    81	            }
    82	        }
    83	        .navigationTitle(canCreate ? "对话" : "会话")
    84	        .sheet(isPresented: $newChat) { NewChatView().environmentObject(model) }
    85	    }
    86	    func header(_ session: Session) -> some View {
    87	        HStack {
    88	            VStack(alignment: .leading, spacing: 4) {
    89	                Text(session.title).font(.headline).lineLimit(1)
    90	                Text("\(sourceName(session.source)) / \(session.project.isEmpty ? "未关联项目" : session.project)").font(.caption).foregroundStyle(.secondary).lineLimit(1).textSelection(.enabled)
    91	            }
    92	            Spacer()
    93	            Button { showEvents.toggle() } label: { Image(systemName: "list.bullet.rectangle") }.help("显示运行事件")
    94	            if session.source != "desktop" { Button("恢复会话") { Task { await model.resumeSelected() } }.disabled(model.running.contains(session.id)) }
    95	        }.padding(16)
    96	    }
    97	    func composer(_ session: Session) -> some View {
    98	        VStack(alignment: .leading, spacing: 10) {
    99	            if !attachments.isEmpty {
   100	                HStack { ForEach(attachments, id: \.self) { url in Button { attachments.removeAll { $0 == url } } label: { Label(url.lastPathComponent, systemImage: "xmark.circle").lineLimit(1) }.font(.caption) } }
   101	            }
   102	            ZStack(alignment: .topLeading) {
   103	                if prompt.isEmpty { Text("输入消息，继续此会话…").foregroundStyle(.tertiary).padding(.top, 8).padding(.leading, 5).allowsHitTesting(false) }
   104	                TextEditor(text: $prompt).font(.body).scrollContentBackground(.hidden).frame(minHeight: 65, maxHeight: 150)
   105	            }
   106	            HStack {
   107	                Button { attachments += model.chooseAttachments().filter { !attachments.contains($0) } } label: { Image(systemName: "paperclip") }.buttonStyle(.plain).help("添加附件，图片能力由 Agent 决定")
   108	                Image(systemName: "folder").foregroundStyle(.secondary)
   109	                Text(session.projectName).font(.caption).foregroundStyle(.secondary)
   110	                Spacer()
   111	                AgentOptionsView(session: session, prompt: $prompt)
   112	                if sending || model.running.contains(session.id) {
   113	                    Button { Task { await model.stop(); sending = false } } label: { Image(systemName: "stop.fill") }.help("停止当前执行")
   114	                } else {
   115	                    Button {
   116	                        let text = prompt, files = attachments; prompt = ""; attachments = []; sending = true
   117	                        Task { if !(await model.send(text, attachments: files)) { if prompt.isEmpty { prompt = text }; if attachments.isEmpty { attachments = files } }; sending = false }
   118	                    } label: { Image(systemName: "arrow.up").fontWeight(.semibold).frame(width: 22, height: 22) }.buttonStyle(.borderedProminent).keyboardShortcut(.return, modifiers: .command).disabled(prompt.trimmingCharacters(in: .whitespacesAndNewlines).isEmpty || !model.ready)
   119	                }
   120	            }
   121	        }.padding(14).background(.quaternary.opacity(0.4), in: RoundedRectangle(cornerRadius: 14)).overlay(RoundedRectangle(cornerRadius: 14).stroke(.primary.opacity(0.08))).padding(18)
   122	    }
   123	}
   124	
   125	struct MessageView: View {
   126	    let message: Message
   127	    @State private var expanded = false
   128	    var body: some View {
   129	        VStack(alignment: .leading, spacing: 8) {
   130	            HStack(spacing: 7) {
   131	                Image(systemName: message.role == "user" ? "person.circle" : message.role == "tool" ? "terminal" : "sparkle").foregroundStyle(message.role == "user" ? .blue : .secondary)
   132	                Text(message.role == "user" ? "你" : message.role == "tool" ? "工具" : "助手").font(.caption.weight(.semibold))
   133	                Spacer()
   134	                Text(Date(timeIntervalSince1970: message.time / 1000), style: .time).font(.caption2).foregroundStyle(.tertiary)
   135	            }
   136	            if message.kind == "tool" {
   137	                DisclosureGroup(isExpanded: $expanded) { Text(message.text).font(.system(size: 11, design: .monospaced)).textSelection(.enabled).frame(maxWidth: .infinity, alignment: .leading) } label: { Text(message.text.components(separatedBy: "\n").first ?? "工具输出").lineLimit(1).font(.caption) }
   138	            } else { Text(.init(message.text)).textSelection(.enabled).font(.system(size: 13)).lineSpacing(5).frame(maxWidth: .infinity, alignment: .leading) }
   139	        }.padding(message.role == "user" ? 16 : 0).background(message.role == "user" ? Color.blue.opacity(0.055) : .clear, in: RoundedRectangle(cornerRadius: 12))
   140	    }
   141	}
   142	
   143	struct NewChatView: View {
   144	    @EnvironmentObject var model: AppModel
   145	    @Environment(\.dismiss) var dismiss
   146	    @State private var agentID = ""
   147	    @State private var cwd = ""
   148	    @State private var starting = false
   149	    var body: some View {
   150	        VStack(alignment: .leading, spacing: 22) {
   151	            Text("新建对话").font(.title2.bold())
   152	            Text("选择原生工具或 ACP Agent，在本地项目中开始对话。").foregroundStyle(.secondary)
   153	            Form {
   154	                Picker("Agent", selection: $agentID) {
   155	                    ForEach(model.settings.agents) { agent in Text("\(agent.name) · \(agent.kind == "acp" ? "ACP" : "原生")").tag(agent.id) }
   156	                }
   157	                HStack { TextField("工作目录", text: $cwd); Button("选择…") { if let path = model.chooseProject() { cwd = path } } }
   158	                if model.settings.agents.first(where: { $0.id == agentID })?.kind != "acp" { TextField("模型（留空使用默认值）", text: $model.composerModel) }
   159	                else { Text("创建后可选择 Agent 提供的模型与权限选项").font(.caption).foregroundStyle(.secondary) }
   160	            }
   161	            HStack { Button("取消") { dismiss() }.keyboardShortcut(.cancelAction); Spacer(); if starting { ProgressView().controlSize(.small) }; Button("创建对话") {
   162	                guard let agent = model.settings.agents.first(where: { $0.id == agentID }) else { return }
   163	                starting = true
   164	                Task { let created = await model.startChat(agent: agent, cwd: cwd); starting = false; if created { dismiss() } }
   165	            }.buttonStyle(.borderedProminent).disabled(starting || cwd.isEmpty || agentID.isEmpty) }
   166	        }.padding(28).frame(width: 540).onAppear { agentID = model.settings.agents.first?.id ?? ""; cwd = model.project.isEmpty ? FileManager.default.homeDirectoryForCurrentUser.path : model.project }
   167	        .onChange(of: agentID) { _, _ in model.composerModel = "" }
   168	    }
   169	}
   170	
   171	struct ApprovalView: View {
   172	    @EnvironmentObject var model: AppModel
   173	    let request: Approval
   174	    @State private var response = "{}"
   175	    var body: some View {
   176	        VStack(alignment: .leading, spacing: 16) {
   177	            Label("Agent 请求你的确认", systemImage: "hand.raised").font(.title3.bold())
   178	            Text(request.method).font(.system(.caption, design: .monospaced)).foregroundStyle(.secondary)
   179	            ScrollView { Text(request.params.text).font(.system(size: 11, design: .monospaced)).textSelection(.enabled).frame(maxWidth: .infinity, alignment: .leading) }.frame(maxHeight: 300)
   180	            if request.method.contains("question") || request.method.contains("UserInput") || request.method.contains("AskUserQuestion") || request.method.contains("elicitation") {
   181	                Text("结构化回答（JSON）").font(.caption)
   182	                TextEditor(text: $response).font(.system(size: 11, design: .monospaced)).frame(height: 100).border(.quaternary)
   183	            }
   184	            HStack {
   185	                Button("拒绝", role: .cancel) { Task { await model.answer(request, allowed: false) } }
   186	                Spacer()
   187	                ForEach(Array(request.params["options"].array.enumerated()), id: \.offset) { _, option in
   188	                    Button(option["name"].string) { Task { await model.answer(request, allowed: option["kind"].string.hasPrefix("allow"), optionID: option["optionId"].string) } }
   189	                }
   190	                if request.params["options"].array.isEmpty { Button("允许一次 / 提交回答") {
   191	                    do { let value = try JSONDecoder().decode(JSONValue.self, from: Data(response.utf8)); Task { await model.answer(request, allowed: true, content: value) } }
   192	                    catch { model.error = "回答不是有效 JSON：\(error.localizedDescription)" }
   193	                }.buttonStyle(.borderedProminent) }
   194	            }
   195	        }.padding(24).frame(width: 650).interactiveDismissDisabled()
   196	    }
   197	}
     1	import { createReadStream } from 'node:fs';
     2	import { readdir, stat, realpath } from 'node:fs/promises';
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
   143	    }
   144	  }
   145	  session.id = sessionKey(source, `${home}\0${session.nativeID}`);
   146	  session.messages = [...messages.values()];
   147	  session.usage = [...(canonical.size ? canonical : counted).values()];
   148	  session.title ||= session.nativeID;
   149	  if (Number.isFinite(firstTime)) session.created = Math.min(session.created || firstTime, firstTime);
   150	  session.updated = lastTime || file.mtimeMs;
   151	  session.warnings = [...new Set(session.warnings)];
   152	  return session;
   153	}
   154	
   155	async function walk(path: string): Promise<string[]> {
   156	  const entries = await readdir(path, { withFileTypes: true });
   157	  const found = await Promise.all(entries.filter(e => !e.isSymbolicLink()).map(async e => {
   158	    const p = join(path, e.name);
   159	    if (e.isDirectory()) return walk(p);
   160	    return /\.jsonl(?:\.(?:zstd|zst))?$/.test(e.name) ? [p] : [];
   161	  }));
   162	  return found.flat();
   163	}
   164	
   165	export async function scan(locations: Location[], onSession?: (session: Session) => void | Promise<void>, onError?: (message: string) => void): Promise<Session[]> {
   166	  const results: Session[] = [];
   167	  for (const location of locations) {
   168	    let paths: string[];
   169	    try {
   170	      paths = (await Promise.all((location.source === 'claude' ? ['projects'] : ['sessions', ...(location.source === 'codex' ? ['archived_sessions'] : [])]).map(async sub => {
   171	        try { return await walk(join(location.path, sub)); }
   172	        catch (error) { if (object(error).code === 'ENOENT') return []; throw error; }
   173	      }))).flat();
   174	    } catch (error) { onError?.(`${location.path}: ${String(error)}`); continue; }
   175	    if (location.source === 'dsh') {
   176	      const latest = new Map<string, { path: string; version: number; modified: number }>();
   177	      for (const path of paths) {
   178	        const match = /^session(?:\.v(\d+))?\.jsonl(?:\.zstd)?$/.exec(basename(path));
   179	        if (!match) continue;
   180	        const key = dirname(path), version = Number(match[1] || 0), modified = (await stat(path)).mtimeMs;
   181	        const old = latest.get(key);
   182	        if (!old || version > old.version || (version === old.version && modified > old.modified)) latest.set(key, { path, version, modified });
   183	      }
   184	      paths = [...latest.values()].map(v => v.path);
   185	    }
   186	    for (const path of paths) {
   187	      try {
   188	        const info = await stat(path), fingerprint = `${info.size}:${info.mtimeMs}:${info.birthtimeMs}`;
   189	        if (onSession && fingerprints.get(path) === fingerprint) continue;
   190	        const session = await parseFile(location.source, await realpath(path), location.path);
   191	        if (onSession) { await onSession(session); fingerprints.set(path, fingerprint); } else results.push(session);
   192	      } catch (error) { onError?.(`${path}: ${String(error)}`); }
   193	    }
   194	  }
   195	  return results;
   196	}


## tool · 2026-11-16T15:31:09Z


Script completed
Wall time 0.1 seconds
Output:

     1	import type { Session, Data } from './types.ts';
     2	import { object, string, content } from './types.ts';
     3	
     4	export function applyUpdate(session: Session, update: Data, fallbackID: string): { idle: boolean } {
     5	  const type = string(update.sessionUpdate ?? update.type);
     6	  if (['agent_message_chunk', 'agent_message', 'user_message_chunk', 'user_message'].includes(type)) {
     7	    const id = string(update.messageId, fallbackID), role = type.startsWith('user') ? 'user' : 'assistant';
     8	    const existing = session.messages.find(m => m.id === id);
     9	    const text = content(update.content);
    10	    if (existing) {
    11	      if (type.endsWith('chunk')) existing.text += text;
    12	      else if ('content' in update) existing.text = text;
    13	    } else session.messages.push({ id, role, text, time: Date.now(), kind: 'text' });
    14	  }
    15	  if (type === 'tool_call' || type === 'tool_call_update') {
    16	    const id = string(update.toolCallId, fallbackID);
    17	    const existing = session.messages.find(m => m.id === id);
    18	    const text = `${string(update.title)}\n${content(update.content ?? update.rawInput ?? update.rawOutput)}`;
    19	    if (existing) { if (text.trim()) existing.text = text; }
    20	    else session.messages.push({ id, role: 'tool', text, time: Date.now(), kind: 'tool' });
    21	  }
    22	  if (type === 'terminal_output_chunk') {
    23	    const id = `terminal:${string(update.terminalId, fallbackID)}`, text = string(update.data ?? update.output);
    24	    const existing = session.messages.find(m => m.id === id);
    25	    if (existing) existing.text += text;
    26	    else session.messages.push({ id, role: 'tool', text, time: Date.now(), kind: 'tool' });
    27	  }
    28	  if (type === 'plan_update' || type === 'plan') {
    29	    const id = 'agent:plan', text = content(update.entries ?? update.plan);
    30	    const existing = session.messages.find(m => m.id === id);
    31	    if (existing) existing.text = text;
    32	    else session.messages.push({ id, role: 'tool', text, time: Date.now(), kind: 'tool' });
    33	  }
    34	  if (type === 'session_info_update' && typeof update.title === 'string') session.title = update.title;
    35	  if (type === 'notice') session.warnings = [...new Set([...session.warnings, `${string(update.title)} ${string(update.description)}`])];
    36	  const state = string(update.state ?? object(update.state).type);
    37	  return { idle: type === 'state_update' && state === 'idle' };
    38	}
{
  "name": "ragdoll-runtime",
  "version": "0.1.0",
  "private": true,
  "type": "module",
  "engines": { "node": ">=24.2" },
  "scripts": {
    "test": "node --test test/*.test.ts",
    "typecheck": "tsc --noEmit",
    "build": "esbuild src/main.ts --bundle --platform=node --format=esm --packages=external --outfile=dist/main.mjs"
  },
  "dependencies": {
    "@agentclientprotocol/sdk": "2.7.0",
    "@anthropic-ai/claude-agent-sdk": "0.3.325",
    "fflate": "0.8.3",
    "tar": "7.5.23"
  },
  "devDependencies": {
    "@types/node": "^26.0.0",
    "esbuild": "0.28.2",
    "typescript": "5.9.3"
  }
}
rg: runtime/node_modules/@agentclientprotocol/sdk/dist/experimental/v2: IO error for operation on runtime/node_modules/@agentclientprotocol/sdk/dist/experimental/v2: No such file or directory (os error 2)


## tool · 2026-11-16T15:31:13Z


Script completed
Wall time 0.1 seconds
Output:

runtime/node_modules/@agentclientprotocol/sdk/package.json
runtime/node_modules/@agentclientprotocol/sdk/README.md
runtime/node_modules/@agentclientprotocol/sdk/LICENSE
runtime/node_modules/@agentclientprotocol/sdk/MIGRATION_STABLE_UNSTABLE.md
runtime/node_modules/@agentclientprotocol/sdk/schema/v1/schema.json
runtime/node_modules/@agentclientprotocol/sdk/schema/v1/schema.unstable.json
runtime/node_modules/@agentclientprotocol/sdk/schema/v2/schema.json
runtime/node_modules/@agentclientprotocol/sdk/schema/v2/schema.unstable.json
     1	import Foundation
     2	
     3	public struct Message: Codable, Identifiable, Sendable, Equatable {
     4	    public var id: String
     5	    public var role: String
     6	    public var text: String
     7	    public var time: Double
     8	    public var kind: String
     9	    public init(id: String = UUID().uuidString, role: String, text: String, time: Double = Date().timeIntervalSince1970 * 1000, kind: String = "text") {
    10	        self.id = id; self.role = role; self.text = text; self.time = time; self.kind = kind
    11	    }
    12	}
    13	
    14	public struct Usage: Codable, Identifiable, Sendable, Equatable {
    15	    public var id: String
    16	    public var time: Double
    17	    public var model: String
    18	    public var input: Int
    19	    public var output: Int
    20	    public var cacheRead: Int
    21	    public var cacheWrite: Int
    22	    public var tokens: Int { input + output + cacheRead + cacheWrite }
    23	    public init(id: String = UUID().uuidString, time: Double, model: String, input: Int, output: Int, cacheRead: Int = 0, cacheWrite: Int = 0) {
    24	        self.id = id; self.time = time; self.model = model; self.input = input; self.output = output; self.cacheRead = cacheRead; self.cacheWrite = cacheWrite
    25	    }
    26	}
    27	
    28	public struct Session: Codable, Identifiable, Sendable, Equatable {
    29	    public var id: String
    30	    public var nativeID: String
    31	    public var source: String
    32	    public var title: String
    33	    public var project: String
    34	    public var home: String
    35	    public var created: Double
    36	    public var updated: Double
    37	    public var parentID: String?
    38	    public var provider: String?
    39	    public var instanceID: String?
    40	    public var nativeSource: String?
    41	    public var canonicalID: String?
    42	    public var messages: [Message]
    43	    public var usage: [Usage]
    44	    public var files: [String]
    45	    public var warnings: [String]
    46	    public var tokens: Int { usage.reduce(0) { $0 + $1.tokens } }
    47	    public var projectName: String { project.isEmpty ? "未关联项目" : URL(fileURLWithPath: project).lastPathComponent }
    48	    public init(id: String, nativeID: String? = nil, source: String, title: String, project: String = "", home: String = "", created: Double = Date().timeIntervalSince1970 * 1000, updated: Double? = nil, messages: [Message] = [], usage: [Usage] = [], files: [String] = [], warnings: [String] = []) {
    49	        self.id = id; self.nativeID = nativeID ?? id; self.source = source; self.title = title; self.project = project; self.home = home; self.created = created; self.updated = updated ?? created
    50	        self.messages = messages; self.usage = usage; self.files = files; self.warnings = warnings
    51	    }
    52	}
    53	
    54	public struct Location: Codable, Sendable, Equatable {
    55	    public var source: String
    56	    public var path: String
    57	    public init(source: String, path: String) { self.source = source; self.path = path }
    58	}
    59	
    60	public struct AgentConfig: Codable, Identifiable, Sendable, Equatable {
    61	    public var id: String
    62	    public var name: String
    63	    public var kind: String
    64	    public var command: String
    65	    public var args: [String]
    66	    public var env: [String: String]
    67	    public var version: String?
    68	    public var registryID: String?
    69	    public var installPath: String?
    70	    public var `protocol`: Int?
    71	    public init(id: String = UUID().uuidString, name: String, kind: String = "acp", command: String, args: [String] = [], env: [String: String] = [:]) {
    72	        self.id = id; self.name = name; self.kind = kind; self.command = command; self.args = args; self.env = env
    73	    }
    74	}
    75	
    76	public struct Price: Codable, Sendable, Equatable {
    77	    public var input: Double
    78	    public var output: Double
    79	    public var cacheRead: Double
    80	    public var cacheWrite: Double
    81	    public var reference: String
    82	    public var date: String
    83	    public init(input: Double, output: Double, cacheRead: Double = 0, cacheWrite: Double = 0, reference: String = "用户设置", date: String = "2026-11-16") {
    84	        self.input = input; self.output = output; self.cacheRead = cacheRead; self.cacheWrite = cacheWrite; self.reference = reference; self.date = date
    85	    }
    86	    public func cost(_ usage: Usage) -> Double {
    87	        (Double(usage.input) * input + Double(usage.output) * output + Double(usage.cacheRead) * cacheRead + Double(usage.cacheWrite) * cacheWrite) / 1_000_000
    88	    }
    89	}
    90	
    91	public struct Settings: Codable, Sendable {
    92	    public var locations: [Location] = []
    93	    public var agents: [AgentConfig] = []
    94	    public var archivePath = ""
    95	    public var excludedProjects: [String] = []
    96	    public var weeklyBudget: Double?
    97	    public var prices: [String: Price] = [
    98	        "gpt-6.1-sol": Price(input: 2, output: 10, cacheRead: 0.1, cacheWrite: 2.5, reference: "https://developers.openai.com/api/docs/pricing"),
    99	        "gpt-6.1-terra": Price(input: 1, output: 5, cacheRead: 0.05, cacheWrite: 1.25, reference: "https://developers.openai.com/api/docs/pricing"),
   100	        "gpt-6-astra": Price(input: 10, output: 50, cacheRead: 1, cacheWrite: 12.5, reference: "https://developers.openai.com/api/docs/pricing"),
   101	        "gpt-6-luna": Price(input: 0.1, output: 0.5, cacheRead: 0.01, cacheWrite: 0.125, reference: "https://developers.openai.com/api/docs/pricing"),
   102	        "claude-opus-5-5": Price(input: 4, output: 20, cacheRead: 0.2, cacheWrite: 5, reference: "https://platform.claude.com/docs/en/about-claude/pricing"),
   103	        "claude-sonnet-5-5": Price(input: 2, output: 10, cacheRead: 0.1, cacheWrite: 2.5, reference: "https://platform.claude.com/docs/en/about-claude/pricing")
   104	    ]
   105	    public init() {}
   106	}
     1	import Foundation
     2	
     3	public struct Dashboard: Sendable {
     4	    public var tokens = 0
     5	    public var cost = 0.0
     6	    public var recentCost = 0.0
     7	    public var weeklyCost = 0.0
     8	    public var pricedEvents = 0
     9	    public var events = 0
    10	    public var sessions = 0
    11	    public var missingUsageSessions = 0
    12	    public var heatmap = Array(repeating: Array(repeating: 0, count: 24), count: 7)
    13	    public var projects: [ProjectTotal] = []
    14	    public var alert: String = "none"
    15	}
    16	
    17	public struct ProjectTotal: Identifiable, Sendable {
    18	    public var id: String
    19	    public var tokens: Int
    20	    public var cost: Double
    21	    public var sessions: Int
    22	}
    23	
    24	public enum Analytics {
    25	    public static func summarize(_ sessions: [Session], prices: [String: Price], budget: Double?, now: Date = Date(), calendar: Calendar = .current) -> Dashboard {
    26	        var result = Dashboard()
    27	        result.sessions = sessions.count
    28	        let today = calendar.startOfDay(for: now)
    29	        let start = calendar.date(byAdding: .day, value: -6, to: today)!
    30	        let previousWeek = calendar.date(byAdding: .day, value: -7, to: today)!
    31	        let rollingStart = now.addingTimeInterval(-168 * 3600)
    32	        var projects: [String: ProjectTotal] = [:]
    33	        for session in sessions {
    34	            if session.usage.isEmpty { result.missingUsageSessions += 1 }
    35	            var project = projects[session.project] ?? ProjectTotal(id: session.project, tokens: 0, cost: 0, sessions: 0)
    36	            project.sessions += 1
    37	            for usage in session.usage {
    38	                let date = Date(timeIntervalSince1970: usage.time / 1000)
    39	                guard date <= now else { continue }
    40	                result.events += 1
    41	                result.tokens += usage.tokens
    42	                project.tokens += usage.tokens
    43	                if let price = prices[usage.model] {
    44	                    let cost = price.cost(usage)
    45	                    result.cost += cost; result.pricedEvents += 1; project.cost += cost
    46	                    if date >= rollingStart { result.weeklyCost += cost }
    47	                    if date >= previousWeek && date < today { result.recentCost += cost }
    48	                }
    49	                if date >= start {
    50	                    let weekday = calendar.component(.weekday, from: date) - 1
    51	                    let hour = calendar.component(.hour, from: date)
    52	                    result.heatmap[weekday][hour] += usage.tokens
    53	                }
    54	            }
    55	            projects[session.project] = project
    56	        }
    57	        result.projects = projects.values.sorted { $0.tokens > $1.tokens }
    58	        if let budget, budget > 0 {
    59	            result.alert = result.weeklyCost >= budget ? "exceeded" : result.weeklyCost >= budget * 0.8 ? "warning" : "none"
    60	        }
    61	        return result
    62	    }
    63	}
     1	import SwiftUI
     2	import RagdollCore
     3	
     4	struct DashboardView: View {
     5	    @EnvironmentObject var model: AppModel
     6	    var showSessions: () -> Void
     7	    @State private var budget = ""
     8	    var body: some View {
     9	        let stats = model.dashboard
    10	        ScrollView {
    11	            VStack(alignment: .leading, spacing: 22) {
    12	                HStack(alignment: .bottom) {
    13	                    VStack(alignment: .leading, spacing: 8) {
    14	                        Text("WORKSPACE INSIGHTS").font(.system(size: 10, weight: .semibold, design: .monospaced)).tracking(2).foregroundStyle(.blue)
    15	                        Text("活动概览").font(.system(size: 30, weight: .bold))
    16	                        Text(Date.now.formatted(.dateTime.year().month().day().weekday())).foregroundStyle(.secondary)
    17	                    }
    18	                    Spacer()
    19	                    Picker("来源", selection: $model.source) {
    20	                        Text("全部来源").tag("all")
    21	                        ForEach(["codex", "claude", "dsh", "desktop", "acp"], id: \.self) { Text(sourceName($0)).tag($0) }
    22	                    }.frame(width: 180)
    23	                }
    24	                HStack(spacing: 14) {
    25	                    metric("估算总成本", value: stats.pricedEvents > 0 ? money(stats.cost) : "未知", note: "\(stats.pricedEvents)/\(stats.events) 条用量已定价", icon: "dollarsign.circle")
    26	                    metric("前 7 个完整自然日", value: stats.pricedEvents > 0 ? money(stats.recentCost) : "未知", note: "按本地日期统计", icon: "calendar")
    27	                    metric("总 Token", value: compact(stats.tokens), note: "\(stats.missingUsageSessions) 个会话缺少用量", icon: "chart.bar.xaxis")
    28	                    metric("会话", value: "\(stats.sessions)", note: "本地日志与导入记录", icon: "bubble.left.and.bubble.right")
    29	                }
    30	                Card {
    31	                    HStack(spacing: 20) {
    32	                        VStack(alignment: .leading, spacing: 6) {
    33	                            Text("每周预算").font(.headline)
    34	                            Text(model.settings.weeklyBudget.map { "\(money(stats.weeklyCost)) / \(money($0))" } ?? "尚未设置预算").font(.title3.bold()).monospacedDigit()
    35	                            Text("滚动 168 小时 · 80% 和 100% 提醒").font(.caption).foregroundStyle(.secondary)
    36	                        }
    37	                        Spacer()
    38	                        if let total = model.settings.weeklyBudget, total > 0 {
    39	                            VStack(alignment: .leading) {
    40	                                ProgressView(value: min(stats.weeklyCost / total, 1)).tint(stats.alert == "none" ? .blue : .orange)
    41	                                if stats.alert != "none" { Text(stats.alert == "exceeded" ? "已达到预算" : "已使用超过 80% 预算").font(.caption).foregroundStyle(.orange) }
    42	                            }.frame(maxWidth: 220)
    43	                        }
    44	                        TextField("预算 USD", text: $budget).textFieldStyle(.roundedBorder).frame(width: 110)
    45	                        Button("保存") { saveBudget() }
    46	                        if model.settings.weeklyBudget != nil { Button("清除") { model.settings.weeklyBudget = nil; budget = ""; model.persistSettings() } }
    47	                    }
    48	                }
    49	                Card {
    50	                    VStack(alignment: .leading, spacing: 20) {
    51	                        HStack {
    52	                            VStack(alignment: .leading, spacing: 6) { Text("7 日热力图").font(.headline); Text("按本地星期和小时显示 Token 活跃度").font(.caption).foregroundStyle(.secondary) }
    53	                            Spacer()
    54	                            HStack(spacing: 4) { Text("少").font(.caption2).foregroundStyle(.secondary); ForEach(0..<5) { i in RoundedRectangle(cornerRadius: 3).fill(.blue.opacity(i == 0 ? 0.06 : Double(i) / 4)).frame(width: 12, height: 12) }; Text("多").font(.caption2).foregroundStyle(.secondary) }
    55	                        }
    56	                        heatmap(stats)
    57	                    }
    58	                }
    59	                HStack(alignment: .top, spacing: 18) {
    60	                    Card {
    61	                        VStack(alignment: .leading, spacing: 16) {
    62	                            Text("项目活动").font(.headline)
    63	                            if stats.projects.isEmpty { empty("尚无项目记录", icon: "folder") }
    64	                            ForEach(Array(stats.projects.prefix(8))) { project in
    65	                                Button {
    66	                                    model.project = project.id; showSessions()
    67	                                } label: {
    68	                                    VStack(alignment: .leading, spacing: 8) {
    69	                                        HStack { Image(systemName: "folder").foregroundStyle(.blue); Text(project.id.isEmpty ? "未关联项目" : URL(fileURLWithPath: project.id).lastPathComponent).fontWeight(.medium); Spacer(); Text(compact(project.tokens)).monospacedDigit() }
    70	                                        GeometryReader { geometry in Capsule().fill(.blue.opacity(0.12)).overlay(alignment: .leading) { Capsule().fill(.blue).frame(width: geometry.size.width * Double(project.tokens) / Double(max(stats.projects.first?.tokens ?? 1, 1))) } }.frame(height: 4)
    71	                                        HStack { Text("\(project.sessions) 个会话"); Spacer(); Text(money(project.cost)) }.font(.caption).foregroundStyle(.secondary)
    72	                                    }
    73	                                }.buttonStyle(.plain)
    74	                                if project.id != stats.projects.prefix(8).last?.id { Divider() }
    75	                            }
    76	                        }
    77	                    }
    78	                    Card {
    79	                        VStack(alignment: .leading, spacing: 16) {
    80	                            HStack { Text("最近会话").font(.headline); Spacer(); Button("全部") { showSessions() }.buttonStyle(.plain).foregroundStyle(.blue) }
    81	                            if model.filtered.isEmpty { empty("等待本地会话", icon: "bubble.left") }
    82	                            ForEach(Array(model.filtered.prefix(6))) { session in
    83	                                Button { model.select(session.id); showSessions() } label: {
    84	                                    HStack(alignment: .top, spacing: 10) {
    85	                                        Image(systemName: "bubble.left").foregroundStyle(.secondary).padding(.top, 2)
    86	                                        VStack(alignment: .leading, spacing: 5) { Text(session.title).lineLimit(1); Text("\(sourceName(session.source)) · \(session.projectName)").font(.caption).foregroundStyle(.secondary) }
    87	                                        Spacer()
    88	                                        Text(Date(timeIntervalSince1970: session.updated / 1000), style: .relative).font(.caption2).foregroundStyle(.tertiary)
    89	                                    }
    90	                                }.buttonStyle(.plain)
    91	                                Divider()
    92	                            }
    93	                            HStack { Image(systemName: "externaldrive.badge.checkmark"); Text(model.archiveStatus).lineLimit(2) }.font(.caption).foregroundStyle(.secondary)
    94	                        }
    95	                    }
    96	                }
    97	                Text("成本按当前价格表估算，不代表实际账单。未知价格、不同服务层级、长上下文和缓存时长可能影响结果。").font(.caption).foregroundStyle(.tertiary)
    98	            }.padding(28).frame(maxWidth: 1500)
    99	        }
   100	        .background(Color(nsColor: .windowBackgroundColor))
   101	        .onAppear { budget = model.settings.weeklyBudget.map { String($0) } ?? ""; model.heatmapFilter = nil }
   102	        .navigationTitle("首页")
   103	    }
   104	    func saveBudget() {
   105	        guard let value = Double(budget), value.isFinite, value > 0 else { model.error = "请输入大于零的预算金额"; return }
   106	        model.settings.weeklyBudget = value; model.persistSettings()
   107	    }
   108	    func metric(_ title: String, value: String, note: String, icon: String) -> some View {
   109	        Card { VStack(alignment: .leading, spacing: 12) {
   110	            HStack { Text(title).font(.caption).foregroundStyle(.secondary); Spacer(); Image(systemName: icon).foregroundStyle(.tertiary) }
   111	            Text(value).font(.system(size: 27, weight: .semibold, design: .rounded)).monospacedDigit().lineLimit(1).minimumScaleFactor(0.6)
   112	            Text(note).font(.caption2).foregroundStyle(.secondary)
   113	        } }
   114	    }
   115	    func heatmap(_ stats: Dashboard) -> some View {
   116	        let maximum = max(stats.heatmap.flatMap { $0 }.max() ?? 0, 1)
   117	        let days = ["周日", "周一", "周二", "周三", "周四", "周五", "周六"]
   118	        return Grid(horizontalSpacing: 5, verticalSpacing: 5) {
   119	            GridRow { Text("").frame(width: 35); ForEach(0..<24) { hour in Text(hour % 6 == 0 ? "\(hour):00" : "").font(.system(size: 9, weight: .medium, design: .monospaced)).foregroundStyle(.secondary).frame(maxWidth: .infinity) } }
   120	            ForEach(0..<7) { day in
   121	                GridRow {
   122	                    Text(days[day]).font(.caption2).foregroundStyle(.secondary).frame(width: 35, alignment: .leading)
   123	                    ForEach(0..<24) { hour in
   124	                        let value = stats.heatmap[day][hour]
   125	                        let intensity = value == 0 ? 0.055 : 0.18 + 0.82 * log1p(9 * Double(value) / Double(maximum)) / log(10)
   126	                        Button { model.heatmapFilter = [day, hour]; showSessions() } label: {
   127	                            RoundedRectangle(cornerRadius: 4).fill(.blue.opacity(intensity)).frame(maxWidth: .infinity).frame(height: 25)
   128	                        }.buttonStyle(.plain).help("\(days[day]) \(hour):00 · \(value.formatted()) Token").accessibilityLabel("\(days[day]) \(hour) 点，\(value) Token")
   129	                    }
   130	                }
   131	            }
   132	        }
   133	    }
   134	    func empty(_ title: String, icon: String) -> some View { HStack { Image(systemName: icon); Text(title) }.foregroundStyle(.secondary).frame(maxWidth: .infinity, minHeight: 100) }
   135	}


## tool · 2026-11-16T15:31:20Z




## tool · 2026-11-16T15:31:26Z


Script completed
Wall time 0.1 seconds
Output:

145:                  "title": "RequestPermissionRequest",
149:                      "$ref": "#/$defs/RequestPermissionRequest"
198:    "RequestPermissionRequest": {
2778:                  "title": "PromptResponse",
2782:                      "$ref": "#/$defs/PromptResponse"
2872:            "$ref": "#/$defs/AuthMethod"
3269:    "AuthMethod": {
3284:              "$ref": "#/$defs/AuthMethodTerminal"
3300:              "$ref": "#/$defs/AuthMethodAgent"
3317:                  "$ref": "#/$defs/AuthMethodId"
3355:    "AuthMethodId": {
3380:    "AuthMethodTerminal": {
3388:              "$ref": "#/$defs/AuthMethodId"
3426:    "AuthMethodAgent": {
3434:              "$ref": "#/$defs/AuthMethodId"
4058:      "description": "Response from resuming an existing session.\n\nThe agent MUST send a current `state_update` after any requested history\nreplay and before this response, even without replay. The update reports\nforeground state after resuming. The response alone does not imply `idle`.\n\nSee protocol docs: [Current-State Synchronization](https://agentclientprotocol.com/protocol/v2/session-setup#current-state-synchronization)",
4154:    "PromptResponse": {
4155:      "description": "Response acknowledging that a user prompt was inserted into the ACP conversation.\n\nThis response does not indicate that the prompt was merely received or held, nor that the\nagent has finished processing it.\nProcessing and completion are reported through `state_update` session updates.\n\nInsertion is the logical addition of a user message with a message ID and a position\nrelative to other messages in the ACP conversation.\n\nSee protocol docs: [Prompt Accepted](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#2-prompt-accepted)",
4378:                  "description": "Handles session update notifications from the agent.\n\nThis is a notification endpoint (no response expected) that receives\nupdates about session activity, including message updates, message chunks,\ntool calls, and execution plans.\n\nNote: Clients SHOULD continue accepting tool call updates even after\nsending a `session/cancel` notification, as the agent may send final\nupdates before reporting an idle `state_update` with the cancelled\nstop reason.\n\nSee protocol docs: [Agent Reports Output](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#3-agent-reports-output)",
4550:              "const": "state_update"
4556:              "$ref": "#/$defs/StateUpdate"
4894:                    "const": "state_update"
5347:    "RunningStateUpdate": {
5385:    "IdleStateUpdate": {
5455:          "description": "The user or client chose to stop the work: via `session/cancel`, by\nclosing the session, or through an interaction the agent offers, such\nas a permission option that tells the agent to stop. Work the agent\nstops for its own reasons uses another reason, such as `error` for an\ninternal timeout.\n\nAgents MUST report this stop reason on an idle `state_update` when\ncancellation ends active foreground work, even if aborting causes\nexceptions. Agents MUST catch these errors and report `cancelled`, not\n`error`.",
5570:    "RequiresActionStateUpdate": {
5590:    "UnknownStateUpdate": {
5610:    "StateUpdate": {
5625:              "$ref": "#/$defs/RunningStateUpdate"
5641:              "$ref": "#/$defs/IdleStateUpdate"
5657:              "$ref": "#/$defs/RequiresActionStateUpdate"
5673:              "$ref": "#/$defs/UnknownStateUpdate"
6514:      "description": "Notification that the enclosing parent session created and owns a child session.\n\nLater updates modify the existing association's metadata, not its ownership.\n\nSent on the immediate parent session. The first update for an unknown\n`sessionId` announces the child and MUST be sent\nbefore any live request or notification bearing the child's session ID,\nincluding messages naming it as sender or recipient. Child events are\ndelivered automatically. No separate child load, resume, or subscription is needed.\nUnderstanding this update, registering child sessions, and applying their\noperation restrictions are baseline v2 requirements. No Client capability\nis required.\n\nOnly `sessionId` is required. Other fields have\npatch semantics: omitted fields leave the stored value unchanged, `null`\nclears or unsets the value, and concrete values replace it. A concrete\n`_meta` object instead patches the stored metadata by top-level key. For\n`state`, `null` removes the current state report and leaves activity\nunconfirmed. It does not report idle or cancellation. A child whose capabilities are\nunset permits no Client-initiated session mutations.\n\n`cwd` and `additionalDirectories` report where the Agent placed the child.\nWhile unset, each inherits the immediate parent's effective value.\nThe title and description provide the parent's display metadata for the\nchild. Agents SHOULD mirror known child state changes in the parent's\n`state` using the same `StateUpdate` snapshot as the\nordinary `state_update` notification on the child session. This reports\nchild state, not a separate parent-owned lifecycle. Consumers should\ntreat duplicate reports idempotently.\nCompleting or cancelling work does not end the association: the parent may\nmessage the same child again. Individual messages and their outcomes do not\nchange this association.",
6548:          "description": "The child's current foreground state, mirrored onto its parent association.\n\nOptional and nullable. Omitted means unchanged. `null` removes the\ncurrent report and leaves activity unconfirmed (not idle or cancelled).\nA concrete `StateUpdate` replaces the entire previous snapshot.",
6551:              "$ref": "#/$defs/StateUpdate"
6742:                  "title": "InitializeRequest",
6746:                      "$ref": "#/$defs/InitializeRequest"
6841:                  "title": "PromptRequest",
6845:                      "$ref": "#/$defs/PromptRequest"
6869:    "InitializeRequest": {
6895:              "$ref": "#/$defs/ClientCapabilities"
6910:    "ClientCapabilities": {
7050:              "$ref": "#/$defs/AuthMethodId"
7532:      "description": "Request parameters for closing an active session.\n\nThe Agent MUST cancel any ongoing work related to the session as if `session/cancel`\nwas called, then free the resources associated with the session. Unlike `session/cancel`,\nclosing also stops the session's background work. After the close response, the Agent\nsends no other messages for the session on that connection.\n\nClosing a session that does not exist or is not active SHOULD succeed, and Clients SHOULD\ntreat a `-32002` response as a successful close.\n\nWhen closing cancels active foreground work, the Agent MUST send the final\nupdates for that work and the idle `state_update` with `stopReason: \"cancelled\"`\nbefore responding successfully to `session/close`. Closing an idle session\ndoes not itself require another idle update.\n\nClosing also cancels pending `session/prompt` requests whose messages have not\nbeen inserted, including held prompts. If closing prevents a prompt's user message from being inserted, the\nAgent MUST answer that request with `-32800` (Request Cancelled). If the message\nhas already been inserted, the Agent MUST respond successfully with its\n`messageId`. Prompt responses need not precede the close response.",
7723:    "PromptRequest": {
8142:                  "description": "Cancels a session's foreground work and its prompts not yet inserted.\n\nWork in the latest `background` list is not covered and keeps running. The\nAgent MAY stop background activity it does not list.\n\nUpon receiving this notification, the Agent SHOULD stop all language model\nrequests and all tool call invocations of the cancelled foreground work as soon\nas possible.\n\nThe Agent MUST stop waiting for pending `session/request_permission` requests of\nthe cancelled work and treat them as not approved. It SHOULD cancel each of them\nwith `$/cancel_request`.\n\nAfter all ongoing operations have been successfully aborted and pending\nupdates have been sent, the Agent MUST send an idle `state_update` session\nupdate with the `cancelled` stop reason if cancellation ended active\nforeground work. No additional completion update is required if no\nforeground work was active.\n\nAfter cancellation completes, the Agent SHOULD ignore late answers rather\nthan use them to resume the cancelled work.\n\nAgents MUST catch errors caused by aborting cancelled work and report the\n`cancelled` stop reason, not `error`.\n\nThe Agent MAY send content or tool call updates after receiving\n`session/cancel`, but MUST send them before the idle `state_update` that\nreports cancellation.\n\nSee protocol docs: [Cancellation](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#cancellation)",
148:export declare function archiveSession(_sessionId: string, _options?: SessionMutationOptions): Promise<void>;
724:export declare function deleteSession(_sessionId: string, _options?: SessionMutationOptions): Promise<void>;
902:export declare function forkSession(_sessionId: string, _options?: ForkSessionOptions): Promise<ForkSessionResult>;
929:    /** New session UUID. Resumable via `query({ options: { resume: sessionId } })`. */
930:    sessionId: string;
942:export declare function getSessionInfo(_sessionId: string, _options?: GetSessionInfoOptions): Promise<SDKSessionInfo | undefined>;
972:export declare function getSessionMessages(_sessionId: string, _options?: GetSessionMessagesOptions): Promise<SessionMessage[]>;
1009:export declare function getSubagentMessages(_sessionId: string, _agentId: string, _options?: GetSubagentMessagesOptions): Promise<SessionMessage[]>;
1081:export declare function importSessionToStore(_sessionId: string, _store: SessionStore, _options?: ImportSessionToStoreOptions): Promise<void>;
1127:        sessionId: string;
1134:        sessionId: string;
1242:export declare function listSubagents(_sessionId: string, _options?: ListSubagentsOptions): Promise<string[]>;
2226:    resume?: string;
2232:    sessionId?: string;
2760:     * command: /model <name>, the /config Model row, or enabling fast mode when that promotes the model; picker: an interactive model picker; sdk: headless set_model (SDK, Remote Control, IDE); auto: automatic fallback or other programmatic change; resume: model restored while resuming a session
3469:export declare function renameSession(_sessionId: string, _title: string, _options?: SessionMutationOptions): Promise<void>;
5887:        sessionId: string;
6391:    sessionId: string;
7101:    sessionId: string;
7239:        sessionId: string;
7270:        sessionId: string;
7318:    sessionId: string;
10232:        sessionId: string;
10468:export declare function tagSession(_sessionId: string, _tag: string | null, _options?: SessionMutationOptions): Promise<void>;
10635:export declare function unarchiveSession(_sessionId: string, _options?: SessionMutationOptions): Promise<void>;


## tool · 2026-11-16T15:31:30Z


Script completed
Wall time 0.1 seconds
Output:

{
  "StateUpdate": {
    "description": "A snapshot of the session's aggregate foreground activity.\n\nForeground work is the agent's active response or workflow in the session,\nincluding model processing, tool execution, and waiting for user action needed\nto continue that work. It can start with a prompt or be agent-initiated, for\nexample to pursue an ongoing goal or follow up on a completed background task.\nEither way, the agent MUST report `running` when foreground work starts,\nor `requires_action` if it starts blocked on user action, and `idle` when it\nends. The agent SHOULD include a stop reason on that idle update.\nAgent-initiated work does not require a prompt request or a synthetic user\nmessage.\n\n`running` may precede user-message insertion, for example during a foreground\nhook. It is not acknowledgment of insertion, and rejecting a prompt does not\nitself end foreground work.\n\nBackground activity can continue and emit other `session/update` notifications\nwhile `idle`. Those notifications, including a detached task's progress or\ncompletion, do not by themselves change this state. A permission request only\nwarrants `requires_action` when foreground work is blocked on user action.\n\nThe agent SHOULD report `requires_action` when the foreground workflow as a\nwhole cannot progress without user action, including permissions or elicitations.\nOnce reported, it MUST report `running` when progress resumes, or `idle` when\nwork ends without resuming.\nIf other foreground work can progress, the state remains `running`. Resolving\none of several requests does not itself change the state. Agents SHOULD ignore\nresponses for work that has already ended rather than use them to resume it.\n\nA new session defaults to idle until a state update reports otherwise.\nResume MUST send a current-state snapshot after any replay and before its\nresponse. The snapshot reports foreground state after resuming.\nThe response alone does not imply idle.\nRepeated snapshots are idempotent, not additional work, completions, or usage.\nA repeated state may carry updated information without another state transition.\nThe agent MUST report `idle` when no foreground activity remains. Completing\nan individual activity while other foreground work continues does not require\nan idle boundary. Local commands use the same lifecycle even without model work.\n\nSee protocol docs: [Session States](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#session-states)",
    "anyOf": [
      {
        "description": "Foreground work is in progress.",
        "type": "object",
        "properties": {
          "state": {
            "type": "string",
            "const": "running"
          }
        },
        "required": [
          "state"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/RunningStateUpdate"
          }
        ]
      },
      {
        "description": "No foreground work is active. Background activity may continue.",
        "type": "object",
        "properties": {
          "state": {
            "type": "string",
            "const": "idle"
          }
        },
        "required": [
          "state"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/IdleStateUpdate"
          }
        ]
      },
      {
        "description": "Foreground work is blocked on user action.",
        "type": "object",
        "properties": {
          "state": {
            "type": "string",
            "const": "requires_action"
          }
        },
        "required": [
          "state"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/RequiresActionStateUpdate"
          }
        ]
      },
      {
        "description": "The Agent cannot currently determine foreground activity.\nThis replaces previously confirmed activity without ending the work or session.",
        "type": "object",
        "properties": {
          "state": {
            "type": "string",
            "const": "unknown"
          }
        },
        "required": [
          "state"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/UnknownStateUpdate"
          }
        ]
      },
      {
        "title": "other",
        "description": "Custom or future session state.\n\nValues beginning with `_` are reserved for implementation-specific\nextensions. Unknown values that do not begin with `_` are reserved for\nfuture ACP variants.\n\nUnless the Client advertised support for this state, Agents MUST still\nreport the standard states.\nClients MUST NOT treat an unrecognized state as `idle` or present the\nprevious state as confirmed, and show a generic busy state until a known\nstate arrives.",
        "type": "object",
        "properties": {
          "state": {
            "description": "Custom or future session state.\n\nValues beginning with `_` are reserved for implementation-specific\nextensions. Unknown values that do not begin with `_` are reserved for\nfuture ACP variants.",
            "type": "string"
          }
        },
        "required": [
          "state"
        ],
        "not": {
          "anyOf": [
            {
              "type": "object",
              "properties": {
                "state": {
                  "type": "string",
                  "const": "running"
                }
              },
              "required": [
                "state"
              ]
            },
            {
              "type": "object",
              "properties": {
                "state": {
                  "type": "string",
                  "const": "idle"
                }
              },
              "required": [
                "state"
              ]
            },
            {
              "type": "object",
              "properties": {
                "state": {
                  "type": "string",
                  "const": "requires_action"
                }
              },
              "required": [
                "state"
              ]
            },
            {
              "type": "object",
              "properties": {
                "state": {
                  "type": "string",
                  "const": "unknown"
                }
              },
              "required": [
                "state"
              ]
            }
          ]
        },
        "additionalProperties": true
      }
    ]
  },
  "RunningStateUpdate": {
    "description": "Foreground work is in progress.",
    "type": "object",
    "properties": {
      "background": {
        "description": "Work running independently of foreground work, as a complete snapshot.\n\nOptional. Omitted and `null` are equivalent and mean the Agent is not reporting\nbackground work, not that nothing is running. `[]` means no background work is\nrunning. An Agent that reports background work MUST include it on every state\nupdate for the session. A malformed list is treated as not reported.\n\nSee protocol docs: [Background Work](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#background-work)",
        "type": [
          "array",
          "null"
        ],
        "items": {
          "$ref": "#/$defs/BackgroundWork"
        },
        "x-deserialize-default-on-error": true
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    }
  },
  "IdleStateUpdate": {
    "description": "No foreground work is active. Background activity may continue.\n\nAgents SHOULD include a `stopReason` when the idle transition ends foreground\nwork. An idle update that does not end foreground work need not include one.\nReceivers treat an omitted, `null`, or malformed `stopReason` as the agent not\nreporting one.\nRepeated or resume snapshots may carry the last stop reason for context.\nThey MUST NOT be counted as new completions, cancellations, or additional usage.",
    "type": "object",
    "properties": {
      "background": {
        "description": "Work running independently of foreground work, as a complete snapshot.\n\nOptional. Omitted and `null` are equivalent and mean the Agent is not reporting\nbackground work, not that nothing is running. `[]` means no background work is\nrunning. An Agent that reports background work MUST include it on every state\nupdate for the session. A malformed list is treated as not reported.\n\nSee protocol docs: [Background Work](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#background-work)",
        "type": [
          "array",
          "null"
        ],
        "items": {
          "$ref": "#/$defs/BackgroundWork"
        },
        "x-deserialize-default-on-error": true
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      },
      "stopReason": {
        "description": "Why foreground work stopped. The value selects one of this type's variants, which may add fields of their own.\n\nOptional. Omitted and `null` are equivalent and mean the agent is not reporting a stop reason; a malformed value is treated the same way.\n\nSee protocol docs: [Stop Reasons](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#stop-reasons)",
        "type": [
          "string",
          "null"
        ],
        "x-deserialize-default-on-error": true
      }
    },
    "anyOf": [
      {
        "description": "The active work ended successfully.\nIncludes locally handled commands that required no model call.",
        "type": "object",
        "properties": {
          "stopReason": {
            "type": "string",
            "const": "end_turn"
          }
        },
        "required": [
          "stopReason"
        ]
      },
      {
        "description": "The active work ended because the agent reached the maximum number of tokens.",
        "type": "object",
        "properties": {
          "stopReason": {
            "type": "string",
            "const": "max_tokens"
          }
        },
        "required": [
          "stopReason"
        ]
      },
      {
        "description": "The active work ended because the agent reached the maximum number of\nmodel requests for the foreground work.",
        "type": "object",
        "properties": {
          "stopReason": {
            "type": "string",
            "const": "max_turn_requests"
          }
        },
        "required": [
          "stopReason"
        ]
      },
      {
        "description": "The active work ended because the agent refused to continue.",
        "type": "object",
        "properties": {
          "stopReason": {
            "type": "string",
            "const": "refusal"
          }
        },
        "required": [
          "stopReason"
        ]
      },
      {
        "description": "The user or client chose to stop the work: via `session/cancel`, by\nclosing the session, or through an interaction the agent offers, such\nas a permission option that tells the agent to stop. Work the agent\nstops for its own reasons uses another reason, such as `error` for an\ninternal timeout.\n\nAgents MUST report this stop reason on an idle `state_update` when\ncancellation ends active foreground work, even if aborting causes\nexceptions. Agents MUST catch these errors and report `cancelled`, not\n`error`.",
        "type": "object",
        "properties": {
          "stopReason": {
            "type": "string",
            "const": "cancelled"
          }
        },
        "required": [
          "stopReason"
        ]
      },
      {
        "description": "The active work ended because something failed.\n\nThis includes pre-insertion foreground work. A prompt failure before\ninsertion also requires an error response to `session/prompt`. After\ninsertion, the prompt's response remains successful.",
        "type": "object",
        "properties": {
          "stopReason": {
            "type": "string",
            "const": "error"
          }
        },
        "required": [
          "stopReason"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ErrorStopReason"
          }
        ]
      },
      {
        "title": "other",
        "description": "Custom or future stop reason.\n\nValues beginning with `_` are reserved for implementation-specific\nextensions. Unknown values that do not begin with `_` are reserved for\nfuture ACP variants.",
        "type": "object",
        "properties": {
          "stopReason": {
            "description": "Custom or future stop reason.\n\nValues beginning with `_` are reserved for implementation-specific\nextensions. Unknown values that do not begin with `_` are reserved for\nfuture ACP variants.",
            "type": "string"
          }
        },
        "required": [
          "stopReason"
        ],
        "not": {
          "anyOf": [
            {
              "type": "object",
              "properties": {
                "stopReason": {
                  "type": "string",
                  "const": "end_turn"
                }
              },
              "required": [
                "stopReason"
              ]
            },
            {
              "type": "object",
              "properties": {
                "stopReason": {
                  "type": "string",
                  "const": "max_tokens"
                }
              },
              "required": [
                "stopReason"
              ]
            },
            {
              "type": "object",
              "properties": {
                "stopReason": {
                  "type": "string",
                  "const": "max_turn_requests"
                }
              },
              "required": [
                "stopReason"
              ]
            },
            {
              "type": "object",
              "properties": {
                "stopReason": {
                  "type": "string",
                  "const": "refusal"
                }
              },
              "required": [
                "stopReason"
              ]
            },
            {
              "type": "object",
              "properties": {
                "stopReason": {
                  "type": "string",
                  "const": "cancelled"
                }
              },
              "required": [
                "stopReason"
              ]
            },
            {
              "type": "object",
              "properties": {
                "stopReason": {
                  "type": "string",
                  "const": "error"
                }
              },
              "required": [
                "stopReason"
              ]
            }
          ]
        },
        "additionalProperties": true
      },
      {
        "title": "none",
        "description": "No stop reason: `stopReason` is omitted or `null`.",
        "type": "object",
        "properties": {
          "stopReason": {
            "type": "null"
          }
        }
      }
    ]
  },
  "PromptRequest": {
    "description": "Request parameters for sending a user prompt to the agent.\n\nContains the user's message and any additional context.\n\nSee protocol docs: [User Message](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#1-user-message)",
    "type": "object",
    "properties": {
      "sessionId": {
        "description": "The ID of the session to send this user message to",
        "allOf": [
          {
            "$ref": "#/$defs/SessionId"
          }
        ]
      },
      "prompt": {
        "description": "The blocks of content that compose the user's message.\n\nAs a baseline, the Agent MUST support `text` and `resource_link` content blocks,\nwhile other variants are optionally enabled via `PromptCapabilities`.\n\nThe Client MUST adapt its interface according to `PromptCapabilities`.\n\nThe client MAY include referenced pieces of context as either\n`resource` or `resource_link` content blocks.\n\nWhen available, `resource` is preferred\nas it avoids extra round-trips and allows the message to include\npieces of context from sources the agent may not have access to.\n\nClients MUST NOT send an empty array. Agents MAY reject one with `-32602` without\ninserting it.",
        "type": "array",
        "items": {
          "$ref": "#/$defs/ContentBlock"
        },
        "minItems": 1
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    },
    "required": [
      "sessionId",
      "prompt"
    ],
    "x-side": "agent",
    "x-method": "session/prompt"
  },
  "PromptResponse": {
    "description": "Response acknowledging that a user prompt was inserted into the ACP conversation.\n\nThis response does not indicate that the prompt was merely received or held, nor that the\nagent has finished processing it.\nProcessing and completion are reported through `state_update` session updates.\n\nInsertion is the logical addition of a user message with a message ID and a position\nrelative to other messages in the ACP conversation.\n\nSee protocol docs: [Prompt Accepted](https://agentclientprotocol.com/protocol/v2/prompt-lifecycle#2-prompt-accepted)",
    "type": "object",
    "properties": {
      "messageId": {
        "description": "Identifies the user message inserted into the ACP conversation.\n\nRequired and non-null. Omission and explicit `null` are both invalid.\n\nThe corresponding user-message session update carries this same identifier and may arrive\nbefore or after this response. Agents must echo the message during the live session, but are\nnot required to retain it. If retained and replayed, the message keeps this identifier.",
        "allOf": [
          {
            "$ref": "#/$defs/MessageId"
          }
        ]
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    },
    "required": [
      "messageId"
    ],
    "x-side": "agent",
    "x-method": "session/prompt"
  },
  "ClientCapabilities": {
    "description": "Capabilities supported by the client.\n\nAdvertised during initialization to inform the agent about\navailable features and methods.\n\nSee protocol docs: [Client Capabilities](https://agentclientprotocol.com/protocol/v2/initialization#client-capabilities)",
    "type": "object",
    "properties": {
      "auth": {
        "description": "Authentication capabilities supported by the client.\nDetermines which authentication method types the agent may include\nin its `InitializeResponse`.\n\nOptional. Omitted and `null` are equivalent and mean the client does not advertise any\nauthentication-method extensions.",
        "anyOf": [
          {
            "$ref": "#/$defs/ClientAuthCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "elicitation": {
        "description": "Elicitation capabilities supported by the client.\nDetermines which elicitation modes the agent may use.\n\nOptional. Omitted and `null` are equivalent and mean the client does not advertise\nelicitation support.",
        "anyOf": [
          {
            "$ref": "#/$defs/ElicitationCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    }
  },
  "AuthMethodTerminal": {
    "description": "Terminal-based authentication method.\n\nThe client runs the configured agent program as a separate interactive\nprocess for the user to authenticate via a TUI. Agents MUST advertise this\nmethod only when the client enabled its terminal authentication capability.\nA zero exit status signals success. Any other termination signals failure.\nThe client MUST NOT pass this method to `auth/login`.",
    "type": "object",
    "properties": {
      "methodId": {
        "description": "Unique identifier for this authentication method.",
        "allOf": [
          {
            "$ref": "#/$defs/AuthMethodId"
          }
        ]
      },
      "name": {
        "description": "Human-readable name of the authentication method.",
        "type": "string"
      },
      "description": {
        "description": "Optional human-readable description of this authentication method.\n\nOmitted and `null` are equivalent and mean no description is provided.",
        "type": [
          "string",
          "null"
        ],
        "x-deserialize-default-on-error": true
      },
      "args": {
        "description": "Additional arguments to append to the configured agent invocation for terminal auth.",
        "type": "array",
        "items": {
          "type": "string"
        },
        "x-deserialize-default-on-null": true
      },
      "env": {
        "description": "Additional environment variables to set on the configured agent invocation for terminal auth.\nNames MUST be unique. These values override same-named variables in the\nbase launch configuration.",
        "type": "array",
        "items": {
          "$ref": "#/$defs/EnvVariable"
        },
        "x-deserialize-default-on-null": true
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    },
    "required": [
      "methodId",
      "name"
    ]
  },
  "RequestPermissionRequest": {
    "description": "Request for user permission to proceed with an operation.\n\nSent when the agent needs authorization before performing a sensitive operation.\n\nSee protocol docs: [Requesting Permission](https://agentclientprotocol.com/protocol/v2/tool-calls#requesting-permission)",
    "type": "object",
    "properties": {
      "sessionId": {
        "description": "The session ID for this request.",
        "allOf": [
          {
            "$ref": "#/$defs/SessionId"
          }
        ]
      },
      "title": {
        "description": "Human-readable title for the permission prompt.\n\nThis title is specific to the permission prompt and does not update any\nsubject's displayed title.",
        "type": "string"
      },
      "description": {
        "description": "Optional human-readable explanation of why permission is needed.\n\nThis text is specific to the permission prompt and does not update any\nsubject's displayed content. Omitted and `null` are equivalent and mean no separate\npermission description was provided.",
        "type": [
          "string",
          "null"
        ],
        "x-deserialize-default-on-error": true
      },
      "subject": {
        "description": "Optional structured context about the operation requiring permission.\n\nOmitted and `null` are equivalent and mean no structured subject was provided.",
        "anyOf": [
          {
            "$ref": "#/$defs/RequestPermissionSubject"
          },
          {
            "type": "null"
          }
        ]
      },
      "options": {
        "description": "Available permission options for the user to choose from.\nMust contain at least one option.",
        "type": "array",
        "items": {
          "$ref": "#/$defs/PermissionOption"
        },
        "minItems": 1
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    },
    "required": [
      "sessionId",
      "title",
      "options"
    ],
    "x-side": "client",
    "x-method": "session/request_permission"
  },
  "ContentBlock": {
    "description": "Content blocks represent displayable information in the Agent Client Protocol.\n\nContent blocks appear in:\n- User prompts sent via `session/prompt`\n- Language model output reported through `session/update` notifications as\n  message updates or streamed chunks\n- Progress updates and results from tool calls\n\nThis structure is compatible with the Model Context Protocol (MCP), so agents can\nforward content from MCP tool outputs without transformation.\n\nSee protocol docs: [Content](https://agentclientprotocol.com/protocol/v2/content)",
    "anyOf": [
      {
        "description": "Text content. May be plain text or formatted with Markdown.\n\nAll agents MUST support text content blocks in prompts.\nClients SHOULD render this text as CommonMark and MAY support GitHub Flavored Markdown\nextensions.",
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "const": "text"
          }
        },
        "required": [
          "type"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/TextContent"
          }
        ]
      },
      {
        "description": "Images for visual context or analysis.\n\nRequires the `image` prompt capability when included in prompts.",
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "const": "image"
          }
        },
        "required": [
          "type"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ImageContent"
          }
        ]
      },
      {
        "description": "Audio data for transcription or analysis.\n\nRequires the `audio` prompt capability when included in prompts.",
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "const": "audio"
          }
        },
        "required": [
          "type"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/AudioContent"
          }
        ]
      },
      {
        "description": "References to resources that the receiver may be able to read.\n\nAll agents MUST support resource links in prompts.",
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "const": "resource_link"
          }
        },
        "required": [
          "type"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ResourceLink"
          }
        ]
      },
      {
        "description": "Complete resource contents embedded directly in the message.\n\nPreferred for including context as it avoids extra round-trips.\n\nRequires the `embeddedContext` prompt capability when included in prompts.",
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "const": "resource"
          }
        },
        "required": [
          "type"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/EmbeddedResource"
          }
        ]
      },
      {
        "title": "other",
        "description": "Custom or future content block.\n\nValues beginning with `_` are reserved for implementation-specific\nextensions. Unknown values that do not begin with `_` are reserved for\nfuture ACP variants.\n\nReceivers that do not understand this content block type should preserve\nthe raw payload when storing, replaying, proxying, or forwarding content,\nand otherwise ignore it or display it generically. Agents MUST reject a\n`session/prompt` request with a content block type they do not support\nwith `-32602`.",
        "type": "object",
        "properties": {
          "type": {
            "description": "Custom or future content block type.\n\nValues beginning with `_` are reserved for implementation-specific\nextensions. Unknown values that do not begin with `_` are reserved for\nfuture ACP variants.",
            "type": "string"
          }
        },
        "required": [
          "type"
        ],
        "not": {
          "anyOf": [
            {
              "type": "object",
              "properties": {
                "type": {
                  "type": "string",
                  "const": "text"
                }
              },
              "required": [
                "type"
              ]
            },
            {
              "type": "object",
              "properties": {
                "type": {
                  "type": "string",
                  "const": "image"
                }
              },
              "required": [
                "type"
              ]
            },
            {
              "type": "object",
              "properties": {
                "type": {
                  "type": "string",
                  "const": "audio"
                }
              },
              "required": [
                "type"
              ]
            },
            {
              "type": "object",
              "properties": {
                "type": {
                  "type": "string",
                  "const": "resource_link"
                }
              },
              "required": [
                "type"
              ]
            },
            {
              "type": "object",
              "properties": {
                "type": {
                  "type": "string",
                  "const": "resource"
                }
              },
              "required": [
                "type"
              ]
            }
          ]
        },
        "additionalProperties": true
      }
    ]
  },
  "AgentMessageUpdate": null,
  "AgentMessageChunk": null
}


## tool · 2026-11-16T15:31:36Z


Script completed
Wall time 0.1 seconds
Output:

{
  "description": "A user message has been created or updated.\n\nAgents can send this when they accept or replay a user message. When a\nclient receives another `user_message` update with the same `messageId`,\nfields in the new update patch the previous fields for that message.",
  "type": "object",
  "properties": {
    "sessionUpdate": {
      "type": "string",
      "const": "user_message"
    }
  },
  "required": [
    "sessionUpdate"
  ],
  "allOf": [
    {
      "$ref": "#/$defs/UserMessage"
    }
  ]
}
{
  "description": "An agent message has been created or updated.\n\nAgents can send this in addition to streamed chunks. When a client\nreceives another `agent_message` update with the same `messageId`,\nfields in the new update patch the previous fields for that message.",
  "type": "object",
  "properties": {
    "sessionUpdate": {
      "type": "string",
      "const": "agent_message"
    }
  },
  "required": [
    "sessionUpdate"
  ],
  "allOf": [
    {
      "$ref": "#/$defs/AgentMessage"
    }
  ]
}
{
  "description": "A snapshot of the session's aggregate foreground activity.",
  "type": "object",
  "properties": {
    "sessionUpdate": {
      "type": "string",
      "const": "state_update"
    }
  },
  "required": [
    "sessionUpdate"
  ],
  "allOf": [
    {
      "$ref": "#/$defs/StateUpdate"
    }
  ]
}
{
  "MessageUpdate": null,
  "MessageChunk": null,
  "ConfigOptionValue": null,
  "SessionCapabilities": {
    "description": "Session capabilities supported by the agent.\n\nSupplying `{}` means the agent supports the baseline session methods:\n`session/new`, `session/list`, `session/resume`, `session/close`,\n`session/prompt`, `session/cancel`, and `session/update`.\n\nAgents that support sessions **MAY** support additional session methods,\nprompt content types, and MCP transports by specifying additional\ncapabilities.\n\nSee protocol docs: [Session Capabilities](https://agentclientprotocol.com/protocol/v2/initialization#session-capabilities)",
    "type": "object",
    "properties": {
      "prompt": {
        "description": "Prompt capabilities supported by the agent in `session/prompt` requests.\n\nOptional. Omitted and `null` are equivalent and mean the agent does not advertise any\nprompt extensions beyond the baseline text and resource-link content\nrequired by `session/prompt`.",
        "anyOf": [
          {
            "$ref": "#/$defs/PromptCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "mcp": {
        "description": "MCP capabilities supported by the agent for session lifecycle requests.\n\nOptional. Omitted and `null` are equivalent and mean the agent does not advertise MCP\nserver transport support for sessions.",
        "anyOf": [
          {
            "$ref": "#/$defs/McpCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "delete": {
        "description": "Whether the agent supports `session/delete`.\n\nOptional. Omitted and `null` are equivalent and mean the agent does not advertise support.\nSupplying `{}` means the agent supports deleting sessions from `session/list`.",
        "anyOf": [
          {
            "$ref": "#/$defs/SessionDeleteCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "additionalDirectories": {
        "description": "Whether the agent supports `additionalDirectories` on supported session lifecycle requests.\n\nOptional. Omitted and `null` are equivalent and mean the agent does not advertise support.\nSupplying `{}` means the agent supports `additionalDirectories` on\nsupported session lifecycle requests.\n\nAgents may return `SessionInfo.additionalDirectories` to report the\ncomplete ordered additional-root list associated with a listed session.",
        "anyOf": [
          {
            "$ref": "#/$defs/SessionAdditionalDirectoriesCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "systemPrompt": {
        "description": "Whether the agent supports `systemPrompt` on session lifecycle requests.\n\nOptional. Omitted and `null` are equivalent and mean the agent does not advertise support.\nSupplying `{}` means the agent supports `systemPrompt` in `append` mode.",
        "anyOf": [
          {
            "$ref": "#/$defs/SessionSystemPromptCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    }
  },
  "AgentCapabilities": {
    "description": "Capabilities supported by the agent.\n\nAdvertised during initialization to inform the client about\navailable features and content types.\n\nSee protocol docs: [Agent Capabilities](https://agentclientprotocol.com/protocol/v2/initialization#agent-capabilities)",
    "type": "object",
    "properties": {
      "session": {
        "description": "Session capabilities supported by the agent.\n\nOptional. Omitted and `null` are equivalent and mean the agent does not support the\n`session/*` methods. Supplying `{}` means the agent supports the\nbaseline session methods: `session/new`, `session/list`,\n`session/resume`, `session/close`, `session/prompt`, `session/cancel`,\nand `session/update`.",
        "anyOf": [
          {
            "$ref": "#/$defs/SessionCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "auth": {
        "description": "Authentication-related extension capabilities supported by the agent.\n\nOptional. Omitted and `null` are equivalent and mean the agent does not advertise any\nauthentication-related extensions. This field does not advertise support\nfor `auth/login` or `auth/logout`. Those methods are advertised by a\nnon-empty `authMethods` list in the `initialize` response.",
        "anyOf": [
          {
            "$ref": "#/$defs/AgentAuthCapabilities"
          },
          {
            "type": "null"
          }
        ],
        "x-deserialize-default-on-error": true
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Omitted and `null` are equivalent and mean no metadata.\nImplementations MUST NOT assign meaning to keys they do not recognize.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v2/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    }
  }
}


## tool · 2026-11-16T15:31:45Z




## tool · 2026-11-16T15:32:13Z


Script completed
Wall time 0.1 seconds
Output:

     1	import SwiftUI
     2	import RagdollCore
     3	
     4	enum Page: String, CaseIterable, Identifiable {
     5	    case home = "首页", sessions = "会话", chat = "对话", settings = "设置"
     6	    var id: String { rawValue }
     7	    var icon: String {
     8	        switch self { case .home: "square.grid.2x2"; case .sessions: "clock.arrow.circlepath"; case .chat: "bubble.left.and.bubble.right"; case .settings: "slider.horizontal.3" }
     9	    }
    10	}
    11	
    12	struct RootView: View {
    13	    @EnvironmentObject var model: AppModel
    14	    @State private var page: Page? = .home
    15	    var body: some View {
    16	        NavigationSplitView {
    17	            VStack(alignment: .leading, spacing: 16) {
    18	                HStack(spacing: 10) {
    19	                    Image(systemName: "square.stack.3d.up.fill").font(.title2).foregroundStyle(.blue)
    20	                    VStack(alignment: .leading, spacing: 2) { Text("Ragdoll").font(.title3.bold()); Text("LOCAL CONVERSATIONS").font(.system(size: 8, weight: .semibold, design: .monospaced)).foregroundStyle(.secondary).tracking(1) }
    21	                }.padding(.horizontal, 16).padding(.top, 20)
    22	                List(Page.allCases, selection: $page) { item in Label(item.rawValue, systemImage: item.icon).tag(item).padding(.vertical, 5) }.listStyle(.sidebar)
    23	                VStack(alignment: .leading, spacing: 8) {
    24	                    HStack { Circle().fill(model.ready ? .green : .orange).frame(width: 6, height: 6); Text(model.ready ? "本地运行" : "未连接").font(.caption) }
    25	                    Text(model.status).font(.caption2).foregroundStyle(.secondary).lineLimit(3)
    26	                    Text("\(model.sessions.count) 个会话").font(.caption.monospacedDigit()).foregroundStyle(.secondary)
    27	                }.padding(16)
    28	            }
    29	            .navigationSplitViewColumnWidth(min: 180, ideal: 210, max: 260)
    30	        } detail: {
    31	            Group {
    32	                switch page ?? .home {
    33	                case .home: DashboardView { page = .sessions }
    34	                case .sessions: ConversationView(canCreate: false)
    35	                case .chat: ConversationView(canCreate: true)
    36	                case .settings: SettingsView()
    37	                }
    38	            }
    39	            .toolbar {
    40	                ToolbarItem { if model.scanning { ProgressView().controlSize(.small) } else { Button { Task { await model.refresh() } } label: { Image(systemName: "arrow.clockwise") }.help("刷新本地会话") } }
    41	                ToolbarItem { Button { model.importDesktop() } label: { Image(systemName: "square.and.arrow.down") }.help("导入 Claude 官方导出包") }
    42	            }
    43	        }
    44	        .alert("操作未完成", isPresented: Binding(get: { model.error != nil }, set: { if !$0 { model.error = nil } })) {
    45	            Button("好", role: .cancel) { model.error = nil }
    46	        } message: { Text(model.error ?? "") }
    47	        .sheet(item: Binding(get: { model.approvals.first }, set: { _ in })) { request in ApprovalView(request: request).environmentObject(model) }
    48	    }
    49	}
    50	
    51	struct Card<Content: View>: View {
    52	    @ViewBuilder var content: Content
    53	    var body: some View { content.padding(20).frame(maxWidth: .infinity, alignment: .leading).background(.background, in: RoundedRectangle(cornerRadius: 16)).overlay(RoundedRectangle(cornerRadius: 16).stroke(.primary.opacity(0.07))) }
    54	}
    55	
    56	func sourceName(_ source: String) -> String {
    57	    switch source { case "codex": "Codex"; case "claude": "Claude Code"; case "dsh": "DeepSeek Harness"; case "desktop": "Claude 聊天"; case "acp": "ACP"; default: source }
    58	}
    59	
    60	func compact(_ value: Int) -> String { value.formatted(.number.notation(.compactName)) }
    61	func money(_ value: Double) -> String { value.formatted(.currency(code: "USD")) }
     1	import SwiftUI
     2	import AppKit
     3	import RagdollCore
     4	
     5	struct SettingsView: View {
     6	    @EnvironmentObject var model: AppModel
     7	    @State private var tab = 0
     8	    @State private var editor: AgentConfig?
     9	    @State private var showRegistry = false
    10	    @State private var historyAgent: AgentConfig?
    11	    @State private var prices = ""
    12	    var body: some View {
    13	        VStack(alignment: .leading, spacing: 18) {
    14	            Text("设置").font(.largeTitle.bold())
    15	            Picker("设置分类", selection: $tab) {
    16	                Text("数据来源").tag(0); Text("Agent 与 ACP").tag(1); Text("Git 归档").tag(2); Text("模型价格").tag(3)
    17	            }.pickerStyle(.segmented).frame(maxWidth: 600)
    18	            ScrollView {
    19	                VStack(alignment: .leading, spacing: 18) {
    20	                    switch tab {
    21	                    case 0: sources
    22	                    case 1: agents
    23	                    case 2: archive
    24	                    default: pricing
    25	                    }
    26	                }.frame(maxWidth: 1050, alignment: .leading).padding(.vertical, 10)
    27	            }
    28	        }.padding(28).navigationTitle("设置")
    29	        .sheet(item: $editor) { agent in AgentEditor(agent: agent).environmentObject(model) }
    30	        .sheet(isPresented: $showRegistry) { RegistryView().environmentObject(model) }
    31	        .sheet(item: $historyAgent) { agent in NativeHistoryView(agent: agent).environmentObject(model) }
    32	        .onAppear { prices = (try? JSONValue.encode(model.settings.prices).text) ?? "{}" }
    33	    }
    34	    var sources: some View {
    35	        Group {
    36	            Card {
    37	                VStack(alignment: .leading, spacing: 18) {
    38	                    Text("本地会话目录").font(.headline)
    39	                    Text("首次读取全部历史，之后自动扫描变化。源日志只读；应用中的新对话通过各工具自己的接口保存。").font(.callout).foregroundStyle(.secondary)
    40	                    ForEach(Array(model.settings.locations.enumerated()), id: \.offset) { i, location in
    41	                        HStack {
    42	                            Text(sourceName(location.source)).frame(width: 140, alignment: .leading)
    43	                            TextField("目录", text: Binding(get: { model.settings.locations[i].path }, set: { model.settings.locations[i].path = $0 })).textFieldStyle(.roundedBorder)
    44	                            Button("选择…") { if let path = model.chooseProject() { model.settings.locations[i].path = path } }
    45	                        }
    46	                    }
    47	                    HStack { Spacer(); Button("保存并扫描") { model.persistSettings(); Task { await model.refresh() } }.buttonStyle(.borderedProminent).disabled(model.scanning) }
    48	                }
    49	            }
    50	            Card {
    51	                HStack {
    52	                    VStack(alignment: .leading, spacing: 8) { Text("Claude 普通聊天").font(.headline); Text("导入官方 ZIP 或 conversations.json；不含原始上传附件，缺失用量显示未知。").font(.caption).foregroundStyle(.secondary) }
    53	                    Spacer(); Button("导入官方导出包…") { model.importDesktop() }
    54	                }
    55	            }
    56	            if !model.warnings.isEmpty {
    57	                Card { VStack(alignment: .leading, spacing: 10) { Text("最近读取与连接提示").font(.headline); ForEach(Array(model.warnings.suffix(15).enumerated()), id: \.offset) { _, warning in Text(warning).font(.system(size: 11, design: .monospaced)).textSelection(.enabled).foregroundStyle(.secondary) } } }
    58	            }
    59	        }
    60	    }
    61	    var agents: some View {
    62	        Group {
    63	            HStack {
    64	                VStack(alignment: .leading, spacing: 6) { Text("对话提供方").font(.headline); Text("原生接口与 ACP 共用聊天界面；登录和模型能力由 Agent 提供。").font(.caption).foregroundStyle(.secondary) }
    65	                Spacer()
    66	                Button("添加本地 ACP") { editor = AgentConfig(name: "新 ACP Agent", command: "") }
    67	                Button("浏览官方目录") { showRegistry = true }.buttonStyle(.borderedProminent)
    68	            }
    69	            ForEach(model.settings.agents) { agent in
    70	                Card {
    71	                    VStack(alignment: .leading, spacing: 12) {
    72	                        HStack {
    73	                            Image(systemName: agent.kind == "acp" ? "puzzlepiece.extension" : "cpu").font(.title2).foregroundStyle(.blue)
    74	                            VStack(alignment: .leading, spacing: 4) { Text(agent.name).font(.headline); Text("\(agent.kind == "acp" ? "ACP" : "原生接口")\(agent.version.map { " · \($0)" } ?? "")").font(.caption).foregroundStyle(.secondary) }
    75	                            Spacer()
    76	                            if model.busyAgents.contains(agent.id) { ProgressView().controlSize(.small) }
    77	                            Button("检测连接") { Task { await model.probe(agent) } }.disabled(model.busyAgents.contains(agent.id))
    78	                            Button("编辑") { editor = agent }
    79	                            if agent.kind == "codex" || agent.kind == "claude" { Button("登录…") { Task { await model.nativeLogin(agent) } } }
    80	                            if agent.kind == "acp" { Button("导入历史") { if let project = model.chooseProject() { Task { await model.listNative(agent, project: project); historyAgent = agent } } } }
    81	                            if agent.kind == "acp" { Button("移除", role: .destructive) { Task { await model.removeAgent(agent) } } }
    82	                        }
    83	                        Text(([agent.command] + agent.args).joined(separator: " ")).font(.system(size: 10, design: .monospaced)).foregroundStyle(.secondary).textSelection(.enabled)
    84	                        if let info = model.agentInfo[agent.id] {
    85	                            let methods = info["authMethods"].array.isEmpty ? info["auth"]["methods"].array : info["authMethods"].array
    86	                            if !methods.isEmpty {
    87	                                HStack {
    88	                                    Text("登录：").font(.caption)
    89	                                    ForEach(Array(methods.enumerated()), id: \.offset) { _, method in Button(method["name"].string) { Task { await model.authenticate(agent, methodID: method["methodId"].string.isEmpty ? method["id"].string : method["methodId"].string) } }.disabled(model.busyAgents.contains(agent.id)) }
    90	                                }
    91	                            }
    92	                            DisclosureGroup("连接信息与能力") { Text(info.text).font(.system(size: 10, design: .monospaced)).textSelection(.enabled).frame(maxWidth: .infinity, alignment: .leading) }
    93	                        }
    94	                    }
    95	                }
    96	            }
    97	            if !model.loginLinks.isEmpty { Card { VStack(alignment: .leading, spacing: 8) { Text("登录链接").font(.headline); ForEach(model.loginLinks, id: \.self) { url in Link("打开登录页面 · \(url.host ?? "")", destination: url) } } } }
    98	        }
    99	    }
   100	    var archive: some View {
   101	        Group {
   102	            Card {
   103	                VStack(alignment: .leading, spacing: 16) {
   104	                    Text("Git 自动归档").font(.headline)
   105	                    Text("保存原始记录、Markdown 和元数据；合并变更后创建本地提交。不会推送到远端。").foregroundStyle(.secondary)
   106	                    HStack { Text(model.settings.archivePath.isEmpty ? "尚未选择目录" : model.settings.archivePath).font(.system(.caption, design: .monospaced)).textSelection(.enabled); Spacer(); Button("选择专用仓库…") { model.chooseArchive() } }
   107	                    Text(model.archiveStatus).font(.caption).foregroundStyle(.secondary).textSelection(.enabled)
   108	                    HStack {
   109	                        if let date = model.lastArchive { Text("上次完成：\(date.formatted())").font(.caption).foregroundStyle(.secondary) }
   110	                        Spacer()
   111	                        if model.archiving { ProgressView().controlSize(.small) }
   112	                        Button("立即归档") { Task { await model.archiveNow() } }.buttonStyle(.borderedProminent).disabled(model.archiving || model.settings.archivePath.isEmpty)
   113	                    }
   114	                    Text("自动保存采用 30 秒防抖，最长合并 5 分钟。源文件删除后保留已有归档；手工修改的归档文件会阻止自动覆盖。Git 需要已配置提交者姓名与邮箱。").font(.caption).foregroundStyle(.secondary)
   115	                }
   116	            }
   117	            Card {
   118	                VStack(alignment: .leading, spacing: 12) {
   119	                    Text("排除项目").font(.headline)
   120	                    Text("取消选择的项目仍可浏览和统计，其后续变化不写入归档；已有归档不会删除。").font(.caption).foregroundStyle(.secondary)
   121	                    ForEach(model.projects, id: \.self) { project in
   122	                        Toggle(project, isOn: Binding(get: { !model.settings.excludedProjects.contains(project) }, set: { include in
   123	                            model.settings.excludedProjects.removeAll { $0 == project }; if !include { model.settings.excludedProjects.append(project) }; model.persistSettings()
   124	                        })).toggleStyle(.checkbox).font(.caption)
   125	                    }
   126	                }
   127	            }
   128	        }
   129	    }
   130	    var pricing: some View {
   131	        Card {
   132	            VStack(alignment: .leading, spacing: 14) {
   133	                Text("模型价格（USD / 百万 Token）").font(.headline)
   134	                Text("内置表记录官方标准价格和核实日期。可按实际提供方修正；没有精确匹配的模型显示未知。缓存时长、上下文长度、服务层级和历史调价可能影响估算。").font(.caption).foregroundStyle(.secondary)
   135	                TextEditor(text: $prices).font(.system(size: 11, design: .monospaced)).frame(minHeight: 400).border(.quaternary)
   136	                HStack { Spacer(); Button("保存价格表") {
   137	                    do {
   138	                        let result = try JSONDecoder().decode([String: Price].self, from: Data(prices.utf8))
   139	                        guard result.values.allSatisfy({ [$0.input, $0.output, $0.cacheRead, $0.cacheWrite].allSatisfy { $0.isFinite && $0 >= 0 } }) else { model.error = "价格必须是非负有限数字"; return }
   140	                        model.settings.prices = result; model.persistSettings()
   141	                    } catch { model.error = "价格表无效：\(error.localizedDescription)" }
   142	                }.buttonStyle(.borderedProminent) }
   143	            }
   144	        }
   145	    }
   146	}
   147	
   148	struct AgentEditor: View {
   149	    @EnvironmentObject var model: AppModel
   150	    @Environment(\.dismiss) var dismiss
   151	    @State var agent: AgentConfig
   152	    @State private var arguments = ""
   153	    @State private var environment = ""
   154	    @State private var failedToLoad = false
   155	    var body: some View {
   156	        VStack(alignment: .leading, spacing: 18) {
   157	            Text("配置 \(agent.kind == "acp" ? "ACP Agent" : agent.name)").font(.title2.bold())
   158	            Form {
   159	                TextField("名称", text: $agent.name)
   160	                TextField("程序路径或命令", text: $agent.command)
   161	                LabeledContent("参数（每行一项）") { TextEditor(text: $arguments).font(.system(.caption, design: .monospaced)).frame(height: 80) }
   162	                LabeledContent("环境变量（NAME=value）") { TextEditor(text: $environment).font(.system(.caption, design: .monospaced)).frame(height: 100) }
   163	                if agent.kind == "acp" {
   164	                    Picker("协议", selection: Binding(get: { agent.protocol ?? 0 }, set: { agent.protocol = $0 == 0 ? nil : $0 })) { Text("自动协商").tag(0); Text("ACP v1").tag(1); Text("ACP v2（实验性）").tag(2) }
   165	                }
   166	            }
   167	            Text("直接运行程序，不展开 Shell 表达式。环境变量保存到系统钥匙串，不写入会话归档。").font(.caption).foregroundStyle(.secondary)
   168	            HStack { Button("取消") { dismiss() }; Spacer(); Button("保存") { save() }.buttonStyle(.borderedProminent).disabled(agent.name.isEmpty || agent.command.isEmpty || failedToLoad) }
   169	        }.padding(28).frame(width: 640)
   170	        .onAppear {
   171	            arguments = agent.args.joined(separator: "\n")
   172	            do { let env = try Secrets.load(agent.id).merging(agent.env) { old, _ in old }; environment = env.sorted { $0.key < $1.key }.map { "\($0.key)=\($0.value)" }.joined(separator: "\n") }
   173	            catch { failedToLoad = true; model.error = error.localizedDescription }
   174	        }
   175	    }
   176	    func save() {
   177	        do {
   178	            var env: [String: String] = [:]
   179	            for line in environment.components(separatedBy: .newlines) where !line.isEmpty {
   180	                guard let separator = line.firstIndex(of: "=") else { model.error = "环境变量每行必须为 NAME=value"; return }
   181	                let name = String(line[..<separator]); guard name.range(of: "^[A-Za-z_][A-Za-z0-9_]*$", options: .regularExpression) != nil else { model.error = "无效的环境变量名称"; return }
   182	                env[name] = String(line[line.index(after: separator)...])
   183	            }
   184	            agent.args = arguments.components(separatedBy: .newlines).filter { !$0.isEmpty }; agent.env = env
   185	            try model.saveAgent(agent); dismiss()
   186	        } catch { model.error = error.localizedDescription }
   187	    }
   188	}
   189	
   190	struct RegistryView: View {
   191	    @EnvironmentObject var model: AppModel
   192	    @Environment(\.dismiss) var dismiss
   193	    @State private var search = ""
   194	    var entries: [JSONValue] { model.registry.filter { search.isEmpty || ($0["name"].string + $0["description"].string).localizedCaseInsensitiveContains(search) } }
   195	    var body: some View {
   196	        VStack(alignment: .leading, spacing: 16) {
   197	            HStack { Text("ACP 官方目录").font(.title2.bold()); Spacer(); if model.registryLoading { ProgressView().controlSize(.small) }; Button("刷新") { Task { await model.loadRegistry() } }; Button("完成") { dismiss() } }
   198	            Text("Agent 在本机执行，使用自己的账号和权限。安装前可查看项目来源及许可证；更新不会自动进行。").font(.caption).foregroundStyle(.secondary)
   199	            TextField("搜索 Agent", text: $search).textFieldStyle(.roundedBorder)
   200	            List(Array(entries.enumerated()), id: \.offset) { _, entry in
   201	                HStack(alignment: .top, spacing: 16) {
   202	                    VStack(alignment: .leading, spacing: 7) {
   203	                        HStack { Text(entry["name"].string).font(.headline); Text(entry["version"].string).font(.system(.caption, design: .monospaced)).foregroundStyle(.secondary) }
   204	                        Text(entry["description"].string).font(.caption).foregroundStyle(.secondary).lineLimit(3)
   205	                        HStack { if let url = URL(string: entry["repository"].string) { Link("项目来源", destination: url) }; if let url = URL(string: entry["license_url"].string) { Link("许可证", destination: url) } }.font(.caption)
   206	                    }
   207	                    Spacer()
   208	                    let installed = model.settings.agents.first { $0.registryID == entry["id"].string }
   209	                    if model.busyAgents.contains(entry["id"].string) { ProgressView().controlSize(.small) }
   210	                    Button(installed == nil ? "安装" : installed?.version == entry["version"].string ? "已安装" : "更新") { Task { await model.installAgent(entry) } }.disabled(model.busyAgents.contains(entry["id"].string) || installed?.version == entry["version"].string)
   211	                }.padding(.vertical, 10)
   212	            }
   213	        }.padding(24).frame(width: 850, height: 650).task { if model.registry.isEmpty { await model.loadRegistry() } }
   214	    }
   215	}
     1	export type Source = 'codex' | 'claude' | 'dsh' | 'desktop' | 'acp';
     2	export type Data = Record<string, unknown>;
     3	export interface Message { id: string; role: string; text: string; time: number; kind: string }
     4	export interface Usage { id: string; time: number; model: string; input: number; output: number; cacheRead: number; cacheWrite: number }
     5	export interface Session {
     6	  id: string; nativeID: string; source: Source; title: string; project: string; home: string;
     7	  created: number; updated: number; parentID?: string; provider?: string; instanceID?: string;
     8	  messages: Message[]; usage: Usage[]; files: string[]; warnings: string[];
     9	  nativeSource?: string;
    10	}
    11	export interface Location { source: 'codex' | 'claude' | 'dsh'; path: string }
    12	export interface AgentConfig {
    13	  id: string; name: string; kind: 'codex' | 'claude' | 'dsh' | 'acp';
    14	  command: string; args: string[]; env: Record<string, string>; version?: string;
    15	  registryID?: string; installPath?: string; protocol?: number;
    16	}
    17	export const object = (value: unknown): Data => value !== null && typeof value === 'object' && !Array.isArray(value) ? value as Data : {};
    18	export const string = (value: unknown, fallback = ''): string => typeof value === 'string' ? value : fallback;
    19	export const number = (value: unknown): number => typeof value === 'number' && Number.isFinite(value) && value >= 0 ? value : 0;
    20	export function timestamp(value: unknown): number {
    21	  if (typeof value === 'number') return value < 1e11 ? value * 1000 : value;
    22	  const parsed = Date.parse(string(value));
    23	  return Number.isFinite(parsed) ? parsed : 0;
    24	}
    25	export function content(value: unknown): string {
    26	  if (typeof value === 'string') return value;
    27	  if (Array.isArray(value)) return value.map(content).filter(Boolean).join('\n');
    28	  const v = object(value);
    29	  if (typeof v.text === 'string') return v.text;
    30	  if (v.content !== undefined) return content(v.content);
    31	  if (v.type === 'tool_use' || v.type === 'tool_call') return `${string(v.name)}\n${JSON.stringify(v.input ?? v.arguments, null, 2)}`;
    32	  if (Object.keys(v).length) return JSON.stringify(v, null, 2);
    33	  return '';
    34	}
     1	import SwiftUI
     2	import RagdollCore
     3	
     4	struct AgentOptionsView: View {
     5	    @EnvironmentObject var model: AppModel
     6	    let session: Session
     7	    @Binding var prompt: String
     8	    var info: JSONValue { model.conversationInfo[session.id] ?? .object([:]) }
     9	    var body: some View {
    10	        HStack(spacing: 10) {
    11	            if session.source != "acp" {
    12	                TextField("默认模型", text: $model.composerModel).textFieldStyle(.plain).font(.caption).frame(width: 120)
    13	                if !info["models"]["data"].array.isEmpty {
    14	                    Menu { ForEach(Array(info["models"]["data"].array.enumerated()), id: \.offset) { _, entry in Button(entry["displayName"].string) { model.composerModel = entry["model"].string } } } label: { Image(systemName: "chevron.down") }.menuStyle(.borderlessButton).fixedSize()
    15	                }
    16	            } else {
    17	                Menu("模型与权限") {
    18	                    ForEach(Array(info["configOptions"].array.enumerated()), id: \.offset) { _, option in
    19	                        if option["type"].string == "boolean" {
    20	                            Toggle(option["name"].string, isOn: Binding(get: { option["currentValue"] == .bool(true) }, set: { value in Task { await model.configure(configID(option), value: String(value)) } }))
    21	                        } else {
    22	                            Menu(option["name"].string) {
    23	                                ForEach(Array(values(option).enumerated()), id: \.offset) { _, value in Button(value["name"].string) { Task { await model.configure(configID(option), value: value["value"].string.isEmpty ? value["id"].string : value["value"].string) } } }
    24	                            }
    25	                        }
    26	                    }
    27	                    ForEach(Array(info["models"]["availableModels"].array.enumerated()), id: \.offset) { _, value in Button(value["name"].string) { Task { await model.configure("__legacy_model", value: value["modelId"].string) } } }
    28	                    ForEach(Array(info["modes"]["availableModes"].array.enumerated()), id: \.offset) { _, value in Button(value["name"].string) { Task { await model.configure("__legacy_mode", value: value["id"].string) } } }
    29	                    if info["configOptions"].array.isEmpty && info["models"]["availableModels"].array.isEmpty && info["modes"]["availableModes"].array.isEmpty { Text("Agent 未提供可选配置") }
    30	                }.font(.caption).disabled(model.running.contains(session.id))
    31	                if !info["availableCommands"].array.isEmpty {
    32	                    Menu("命令") { ForEach(Array(info["availableCommands"].array.enumerated()), id: \.offset) { _, command in Button(command["name"].string) { prompt = "/\(command["name"].string) " } } }.font(.caption)
    33	                }
    34	            }
    35	        }
    36	    }
    37	    func configID(_ option: JSONValue) -> String { option["configId"].string.isEmpty ? option["id"].string : option["configId"].string }
    38	    func values(_ option: JSONValue) -> [JSONValue] { option["options"].array.flatMap { value in value["options"].array.isEmpty ? [value] : value["options"].array } }
    39	}
    40	
    41	struct NativeHistoryView: View {
    42	    @EnvironmentObject var model: AppModel
    43	    @Environment(\.dismiss) var dismiss
    44	    let agent: AgentConfig
    45	    @State private var importing: String?
    46	    var body: some View {
    47	        VStack(alignment: .leading, spacing: 16) {
    48	            HStack { Text("导入 \(agent.name) 历史会话").font(.title2.bold()); Spacer(); Button("完成") { dismiss() } }
    49	            Text(model.nativeHistoryProject).font(.caption).foregroundStyle(.secondary)
    50	            List(Array(model.nativeHistory.enumerated()), id: \.offset) { _, entry in
    51	                HStack {
    52	                    VStack(alignment: .leading, spacing: 6) { Text(entry["title"].string.isEmpty ? entry["sessionId"].string : entry["title"].string); Text(entry["cwd"].string).font(.caption).foregroundStyle(.secondary) }
    53	                    Spacer()
    54	                    if importing == entry["sessionId"].string { ProgressView().controlSize(.small) }
    55	                    Button("导入") { importing = entry["sessionId"].string; Task { if await model.importNative(agent, record: entry) { dismiss() }; importing = nil } }.disabled(importing != nil)
    56	                }.padding(.vertical, 8)
    57	            }
    58	            if !model.nativeCursor.isEmpty { Button("加载更多") { Task { await model.listNative(agent, project: model.nativeHistoryProject, more: true) } } }
    59	        }.padding(24).frame(width: 760, height: 560)
    60	    }
    61	}


## tool · 2026-11-16T15:32:41Z




## tool · 2026-11-16T15:32:54Z




## tool · 2026-11-16T15:33:17Z


Script completed
Wall time 0.1 seconds
Output:

{
  "SessionNotification": {
    "description": "Notification containing a session update from the agent.\n\nUsed to stream real-time progress and results during prompt processing.\n\nSee protocol docs: [Agent Reports Output](https://agentclientprotocol.com/protocol/v1/prompt-turn#3-agent-reports-output)",
    "type": "object",
    "properties": {
      "sessionId": {
        "description": "The ID of the session this update pertains to.",
        "allOf": [
          {
            "$ref": "#/$defs/SessionId"
          }
        ]
      },
      "update": {
        "description": "The actual update content.",
        "allOf": [
          {
            "$ref": "#/$defs/SessionUpdate"
          }
        ]
      },
      "_meta": {
        "description": "The _meta property is reserved by ACP to allow clients and agents to attach additional\nmetadata to their interactions. Implementations MUST NOT make assumptions about values at\nthese keys.\n\nSee protocol docs: [Extensibility](https://agentclientprotocol.com/protocol/v1/extensibility)",
        "type": [
          "object",
          "null"
        ],
        "x-deserialize-default-on-error": true,
        "additionalProperties": true
      }
    },
    "required": [
      "sessionId",
      "update"
    ],
    "x-side": "client",
    "x-method": "session/update"
  },
  "SessionUpdate": {
    "description": "Different types of updates that can be sent during session processing.\n\nThese updates provide real-time feedback about the agent's progress.\n\nSee protocol docs: [Agent Reports Output](https://agentclientprotocol.com/protocol/v1/prompt-turn#3-agent-reports-output)",
    "oneOf": [
      {
        "description": "A chunk of the user's message being streamed.",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "user_message_chunk"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ContentChunk"
          }
        ]
      },
      {
        "description": "A chunk of the agent's response being streamed.",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "agent_message_chunk"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ContentChunk"
          }
        ]
      },
      {
        "description": "A chunk of the agent's internal reasoning being streamed.",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "agent_thought_chunk"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ContentChunk"
          }
        ]
      },
      {
        "description": "Notification that a new tool call has been initiated.",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "tool_call"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ToolCall"
          }
        ]
      },
      {
        "description": "Update on the status or results of a tool call.",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "tool_call_update"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ToolCallUpdate"
          }
        ]
      },
      {
        "description": "The agent's execution plan for complex tasks.\nSee protocol docs: [Agent Plan](https://agentclientprotocol.com/protocol/v1/agent-plan)",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "plan"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/Plan"
          }
        ]
      },
      {
        "description": "Available commands are ready or have changed",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "available_commands_update"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/AvailableCommandsUpdate"
          }
        ]
      },
      {
        "description": "The current mode of the session has changed\n\nSee protocol docs: [Session Modes](https://agentclientprotocol.com/protocol/v1/session-modes)",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "current_mode_update"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/CurrentModeUpdate"
          }
        ]
      },
      {
        "description": "Session configuration options have been updated.",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "config_option_update"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/ConfigOptionUpdate"
          }
        ]
      },
      {
        "description": "Session metadata has been updated (title, timestamps, custom metadata)",
        "type": "object",
        "properties": {
          "sessionUpdate": {
            "type": "string",
            "const": "session_info_update"
          }
        },
        "required": [
          "sessionUpdate"
        ],
        "allOf": [
          {
            "$ref": "#/$defs/SessionInfoUpdate"
          }
        ]
runtime/src/client-tools.ts:60:        if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }
runtime/src/client-tools.ts:68:    for (const entry of this.terminals.values()) if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }
runtime/src/rpc.ts:76:      try { process.kill(-pid, 'SIGTERM'); } catch { /* 进程已经退出。 */ }
runtime/src/agents.ts:101:        try { process.kill(-pid, 'SIGTERM'); } catch {}


## tool · 2026-11-16T15:33:37Z


Script completed
Wall time 0.1 seconds
Output:

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
    75	    if (pid && this.child.exitCode === null) {
    76	      try { process.kill(-pid, 'SIGTERM'); } catch { /* 进程已经退出。 */ }
    77	      const timer = setTimeout(() => { try { process.kill(-pid, 'SIGKILL'); } catch { /* 进程已经退出。 */ } }, 3000);
    78	      timer.unref();
    79	      await new Promise<void>(resolve => { if (this.child.exitCode !== null) resolve(); else this.child.once('exit', () => resolve()); });
    80	      clearTimeout(timer);
    81	    }
    82	    this.fail(new Error('执行已停止'));
    83	  }
    84	}
    52	      this.terminals.set(id, entry); return { terminalId: id };
    53	    }
    54	    if (method.startsWith('terminal/')) {
    55	      const id = string(p.terminalId), entry = this.terminals.get(id);
    56	      if (!entry) throw new Error('未知终端');
    57	      if (method === 'terminal/output') return { output: entry.output, truncated: entry.output.length >= 256000, exitStatus: entry.status };
    58	      if (method === 'terminal/wait_for_exit') return await entry.done;
    59	      if (method === 'terminal/kill' || method === 'terminal/release') {
    60	        if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }
    61	        if (method === 'terminal/release') this.terminals.delete(id);
    62	        return {};
    63	      }
    64	    }
    65	    throw new Error(`不支持的客户端方法：${method}`);
    66	  }
    67	  close(): void {
    68	    for (const entry of this.terminals.values()) if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }
    69	    this.terminals.clear();
    70	  }
    71	}
    51	            try fm.createDirectory(at: destination.deletingLastPathComponent(), withIntermediateDirectories: true)
    52	            try data.write(to: destination, options: .atomic)
    53	            manifest[path] = digest; changed.append(path)
    54	        }
    55	        let manifestData = try encoder.encode(manifest)
    56	        let previousManifest = fm.fileExists(atPath: manifestURL.path) ? try Data(contentsOf: manifestURL) : nil
    57	        if previousManifest != manifestData {
    58	            try manifestData.write(to: manifestURL, options: .atomic); changed.append(".ragdoll-manifest.json")
    59	        }
    60	        let managed = Array(manifest.keys) + [".ragdoll-manifest.json"]
    61	        let pending = try git(root, ["status", "--porcelain", "--"] + managed)
    62	        guard !pending.isEmpty else { return ArchiveResult(files: 0, commit: nil) }
    63	        _ = try git(root, ["add", "--"] + managed)
    64	        _ = try git(root, ["commit", "--only", "-m", "chore(archive): sync conversations", "--"] + managed)
    65	        return ArchiveResult(files: changed.count, commit: try git(root, ["rev-parse", "--short", "HEAD"]))
    66	    }
    67	
    68	    private static func safeName(_ value: String) -> String {
    69	        let allowed = CharacterSet.alphanumerics.union(CharacterSet(charactersIn: "._-"))
    70	        let name = value.unicodeScalars.map { allowed.contains($0) ? String($0) : "_" }.joined()
    71	        return name.isEmpty || name == "." || name == ".." ? "session" : name
    72	    }
    73	    private static func hash(_ data: Data) -> String { SHA256.hash(data: data).map { String(format: "%02x", $0) }.joined() }
    74	    private static func failure(_ message: String) -> NSError { NSError(domain: "Ragdoll.Archive", code: 1, userInfo: [NSLocalizedDescriptionKey: message]) }
    75	    private static func git(_ root: URL, _ args: [String]) throws -> String {
    76	        let process = Process(); process.executableURL = URL(fileURLWithPath: "/usr/bin/git"); process.arguments = ["-C", root.path] + args
    77	        let pipe = Pipe(); process.standardOutput = pipe; process.standardError = pipe
    78	        process.environment = ProcessInfo.processInfo.environment.merging(["GIT_TERMINAL_PROMPT": "0"]) { _, new in new }
    79	        try process.run()
    80	        let data = pipe.fileHandleForReading.readDataToEndOfFile(); process.waitUntilExit()
    81	        let text = String(decoding: data, as: UTF8.self).trimmingCharacters(in: .whitespacesAndNewlines)
    82	        guard process.terminationStatus == 0 else { throw failure("文件已保留；Git 操作失败：\(text)") }
    83	        return text
    84	    }
    85	}
   240	        return panel.runModal() == .OK ? panel.url?.path : nil
   241	    }
   242	    func chooseAttachments() -> [URL] {
   243	        let panel = NSOpenPanel(); panel.canChooseDirectories = false; panel.allowsMultipleSelection = true
   244	        return panel.runModal() == .OK ? panel.urls : []
   245	    }
   246	    private func scheduleArchive(markDirty: Bool = true) {
   247	        guard !settings.archivePath.isEmpty else { return }
   248	        if markDirty { dirtySince = dirtySince ?? Date() }
   249	        guard dirtySince != nil else { return }
   250	        guard !scanning else { return }
   251	        archiveTask?.cancel()
   252	        let delay = max(0, min(30, 300 - Date().timeIntervalSince(dirtySince!)))
   253	        archiveTask = Task { do { try await Task.sleep(for: .seconds(delay)); await archiveNow() } catch {} }
   254	    }
   255	    func archiveNow() async {
   256	        guard let store, !settings.archivePath.isEmpty, !archiving, !scanning else { return }
   257	        archiving = true; archiveStatus = "正在保存并提交…"
   258	        let path = settings.archivePath, excluded = settings.excludedProjects, roots = settings.locations.map(\.path)
   259	        do {
   260	            let result = try await Task.detached(priority: .utility) {
   261	                let sessions = try store.list().filter { !excluded.contains($0.project) }.compactMap { try store.session($0.id) }
   262	                return try Archive.save(sessions, to: URL(fileURLWithPath: path), sourceRoots: roots)
   263	            }.value
   264	            archiveStatus = result.commit.map { "已保存并提交 · \($0) · \(result.files) 个文件" } ?? "归档已是最新，无需提交"
   265	            lastArchive = Date(); dirtySince = nil
   266	        } catch { archiveStatus = "归档未完成：\(error.localizedDescription)"; self.error = error.localizedDescription }
   267	        archiving = false
   268	    }
   269	    func openDesktop(_ session: Session) { if let url = URL(string: "https://claude.ai/chat/\(session.nativeID)") { NSWorkspace.shared.open(url) } }
   270	    private func collectLoginLinks(_ value: JSONValue) {
   271	        if let url = URL(string: value.string), ["https", "http"].contains(url.scheme ?? ""), !loginLinks.contains(url) { loginLinks.append(url) }
   272	        for item in value.array { collectLoginLinks(item) }
   273	        for item in value.dictionary.values { collectLoginLinks(item) }
   274	    }
   275	    func nativeLogin(_ agent: AgentConfig) async {
   276	        do {
   277	            let result = try await bridge.request("native.login", ["agent": try .encode(agent)])
   278	            NSWorkspace.shared.open(URL(fileURLWithPath: result["terminalScript"].string))
   279	        } catch { self.error = error.localizedDescription }
   280	    }
   281	    func configure(_ configID: String, value: String) async {
   282	        guard let id = selectedID else { return }
   283	        do {
   284	            let result = try await bridge.request("chat.configure", ["id": .string(id), "configID": .string(configID), "value": .string(value)])
   285	            if result["configOptions"] != .null {
   286	                var info = (conversationInfo[id] ?? .object([:])).dictionary; info["configOptions"] = result["configOptions"]; conversationInfo[id] = .object(info)
   287	            }
   288	        } catch { self.error = error.localizedDescription }
   289	    }
   290	    func listNative(_ agent: AgentConfig, project: String, more: Bool = false) async {
   291	        do {
   292	            let result = try await bridge.request("chat.list", ["agent": try .encode(hydrated(agent)), "cwd": .string(project), "cursor": .string(more ? nativeCursor : "")])
   293	            nativeHistory = (more ? nativeHistory : []) + result["sessions"].array
   294	            nativeCursor = result["nextCursor"].string; nativeHistoryProject = project
   295	        } catch { self.error = error.localizedDescription }
   296	    }
   297	    func importNative(_ agent: AgentConfig, record: JSONValue) async -> Bool {
   298	        do {
   299	            let result = try await bridge.request("chat.import", ["agent": try .encode(hydrated(agent)), "cwd": .string(nativeHistoryProject), "session": record])
   300	            let session = try result["session"].decode(Session.self)
   301	            _ = try store?.save(session); try reload(); select(session.id); conversationInfo[session.id] = result["info"]; scheduleArchive(); return true
   302	        } catch { self.error = error.localizedDescription; return false }
   303	    }
   304	}
    47	        let summaryData = try encoder.encode(summary)
    48	        try db.execute(sql: "INSERT INTO sessions(id,source,native_id,title,project,updated,body,summary,search,canonical_id) VALUES (?,?,?,?,?,?,?,?,?,?) ON CONFLICT(id) DO UPDATE SET title=excluded.title, project=excluded.project, updated=excluded.updated, body=excluded.body, summary=excluded.summary, search=excluded.search, canonical_id=excluded.canonical_id", arguments: [session.id, session.source, session.nativeID, session.title, session.project, session.updated, body, summaryData, session.title + "\n" + session.messages.map(\.text).joined(separator: "\n"), session.canonicalID])
    49	        return true
    50	    }
    51	    public func list(query: String = "", limit: Int = 10000) throws -> [Session] {
    52	        try db.read { db in
    53	            let escaped = query.replacingOccurrences(of: "\\", with: "\\\\").replacingOccurrences(of: "%", with: "\\%").replacingOccurrences(of: "_", with: "\\_")
    54	            return try Data.fetchAll(db, sql: "SELECT summary FROM sessions s WHERE search LIKE ? ESCAPE '\\' AND NOT EXISTS (SELECT 1 FROM sessions a WHERE a.canonical_id=s.id) ORDER BY updated DESC LIMIT ?", arguments: ["%\(escaped)%", limit]).map { try JSONDecoder().decode(Session.self, from: $0) }
    55	        }
    56	    }
    57	    public func session(_ id: String) throws -> Session? {
    58	        try db.read { db in
    59	            try Data.fetchOne(db, sql: "SELECT body FROM sessions WHERE id=?", arguments: [id]).map { try JSONDecoder().decode(Session.self, from: $0) }
    60	        }
    61	    }
    62	    public func settings() throws -> Settings {
    63	        try db.read { db in
    64	            try Data.fetchOne(db, sql: "SELECT body FROM settings WHERE id=1").map { try JSONDecoder().decode(Settings.self, from: $0) } ?? Settings()
    65	        }
    66	    }
    67	    public func saveSettings(_ settings: Settings) throws {
    68	        let data = try JSONEncoder().encode(settings)
    69	        try db.write { db in try db.execute(sql: "INSERT INTO settings(id,body) VALUES(1,?) ON CONFLICT(id) DO UPDATE SET body=excluded.body", arguments: [data]) }
    70	    }
    71	}


## tool · 2026-11-16T15:33:55Z




## tool · 2026-11-16T15:34:26Z




## tool · 2026-11-16T15:34:44Z


Script completed
Wall time 0.1 seconds
Output:

Sources/Ragdoll/AppModel.swift:153:    func saveAgent(_ agent: AgentConfig) throws {
Sources/Ragdoll/AppModel.swift:166:            _ = try store?.save(session); try reload(); select(session.id); agentInfo[agent.id] = result["info"]; conversationInfo[session.id] = result["info"]
Sources/Ragdoll/AppModel.swift:207:    func installAgent(_ entry: JSONValue) async {
Sources/Ragdoll/AppModel.swift:304:            _ = try store?.save(session); try reload(); select(session.id); conversationInfo[session.id] = result["info"]; scheduleArchive(); return true
runtime/src/agents.ts:42:  fail?: (error: Error) => void; importing?: boolean; hasActivity?: boolean; writeQueue?: Promise<void>;
runtime/src/agents.ts:172:        if (type === 'state_update' && (update.state === 'running' || update.state === 'requires_action')) r.hasActivity = true;
runtime/src/agents.ts:173:        if (type.startsWith('agent_message')) r.hasActivity = true;
runtime/src/agents.ts:174:        if (outcome.idle && r.hasActivity && !r.replaying) r.finish?.();
runtime/src/agents.ts:248:    if (prior && this.running.has(prior.id)) return { session: this.running.get(prior.id)!.session };
runtime/src/agents.ts:294:      const ask: Ask = (m, p, signal) => { if (r.busy) r.hasActivity = true; return this.ask(m, { ...p, conversationID: session.id }, signal); };
runtime/src/agents.ts:353:    r.busy = true; r.deltaID = undefined; r.hasActivity = false;
runtime/src/agents.ts:373:        const resumed = r.session.nativeStarted === true;


## tool · 2026-11-16T15:34:51Z


Script completed
Wall time 0.1 seconds
Output:

runtime/src/agents.ts:174:        if (outcome.idle && r.hasActivity && !r.replaying) r.finish?.();
runtime/src/agents.ts:408:      this.emit('state', { conversationID: id, state: 'idle' });
Sources/Ragdoll/AppModel.swift:154:        try Secrets.save(agent.env, for: agent.id)
Sources/Ragdoll/AppModel.swift:211:            try saveAgent(value.decode(AgentConfig.self)); status = "已安装 \(entry["name"].string)" 
Sources/Ragdoll/AppModel.swift:263:                let sessions = try store.list().filter { !excluded.contains($0.project) }.compactMap { try store.session($0.id) }
Sources/Ragdoll/AppModel.swift:267:            lastArchive = Date(); if generation == dirtyGeneration { dirtySince = nil }
Sources/RagdollCore/Store.swift:51:    public func list(query: String = "", limit: Int = Int.max) throws -> [Session] {
Sources/RagdollCore/Archive.swift:46:        let managed = Array(desired.keys) + [".ragdoll-manifest.json"]
Sources/RagdollCore/Archive.swift:69:        _ = try git(root, ["add", "--"] + managed)


## tool · 2026-11-16T15:34:56Z


Script completed
Wall time 0.1 seconds
Output:

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
    14	        if !fm.fileExists(atPath: root.appendingPathComponent(".git").path) { _ = try git(root, ["init"]) }
    15	        guard try git(root, ["rev-parse", "--show-toplevel"]) == root.path else { throw failure("请选择 Git 仓库的根目录") }
    16	        let manifestURL = root.appendingPathComponent(".ragdoll-manifest.json")
    17	        let old = fm.fileExists(atPath: manifestURL.path) ? try JSONDecoder().decode([String: String].self, from: Data(contentsOf: manifestURL)) : [:]
    18	        let encoder = JSONEncoder(); encoder.outputFormatting = [.prettyPrinted, .sortedKeys, .withoutEscapingSlashes]
    19	        var desired: [String: Data] = [:]
    20	        for session in sessions {
    21	            let base = "sessions/\(safeName(session.source))/\(safeName(session.id))"
    22	            var metadata = session; metadata.messages = []
    23	            desired[base + "/metadata.json"] = try encoder.encode(metadata)
    24	            let transcript = "# \(session.title)\n\n来源：\(session.source)\n\n项目：\(session.project)\n\n" + session.messages.map { "## \($0.role) · \(ISO8601DateFormatter().string(from: Date(timeIntervalSince1970: $0.time / 1000)))\n\n\($0.text)\n" }.joined(separator: "\n")
    25	            let portable = session.files.enumerated().reduce(transcript) { text, entry in
    26	                text.replacingOccurrences(of: URL(fileURLWithPath: entry.element).absoluteString, with: "raw/\(entry.offset)-\(safeName(URL(fileURLWithPath: entry.element).lastPathComponent))")
    27	            }
    28	            desired[base + "/transcript.md"] = Data(portable.utf8)
    29	            for (index, path) in session.files.enumerated() {
    30	                let file = URL(fileURLWithPath: path)
    31	                guard fm.fileExists(atPath: file.path) else { continue }
    32	                let values = try file.resourceValues(forKeys: [.isRegularFileKey])
    33	                guard values.isRegularFile == true else { throw failure("无法归档非普通文件：\(path)") }
    34	                desired[base + "/raw/\(index)-\(safeName(file.lastPathComponent))"] = try Data(contentsOf: file)
    35	            }
    36	            if session.files.isEmpty { desired[base + "/events.json"] = try encoder.encode(session) }
    37	        }
    38	        for (path, _) in desired {
    39	            let destination = root.appendingPathComponent(path)
    40	            guard !destination.resolvingSymlinksInPath().path.hasPrefix(root.path + "/.git/") && destination.resolvingSymlinksInPath().path.hasPrefix(root.path + "/") else { throw failure("归档路径越界") }
    41	            if fm.fileExists(atPath: destination.path) {
    42	                let digest = hash(try Data(contentsOf: destination))
    43	                guard old[path] == digest else { throw failure("归档文件已被手动修改或不属于应用：\(path)。请保留修改后选择其他归档目录，或恢复文件后重试。") }
    44	            }
    45	        }
    46	        let managed = Array(desired.keys) + [".ragdoll-manifest.json"]
    47	        let staged = try git(root, ["-c", "core.quotepath=false", "diff", "--cached", "--name-only", "--"] + managed)
    48	        for path in staged.components(separatedBy: .newlines) where !path.isEmpty {
    49	            let data = try gitData(root, ["show", ":\(path)"])
    50	            let expected = path == ".ragdoll-manifest.json" ? (fm.fileExists(atPath: manifestURL.path) ? hash(try Data(contentsOf: manifestURL)) : nil) : old[path]
    51	            guard expected == hash(data) else { throw failure("归档文件存在外部暂存修改，已保留：\(path)。请先处理该暂存修改后重试。") }
    52	        }
    53	        var manifest = old
    54	        var changed: [String] = []
    55	        for (path, data) in desired {
    56	            let digest = hash(data), destination = root.appendingPathComponent(path)
    57	            if old[path] == digest && fm.fileExists(atPath: destination.path) { continue }
    58	            try fm.createDirectory(at: destination.deletingLastPathComponent(), withIntermediateDirectories: true)
    59	            try data.write(to: destination, options: .atomic)
    60	            manifest[path] = digest; changed.append(path)
    61	        }
    62	        let manifestData = try encoder.encode(manifest)
    63	        let previousManifest = fm.fileExists(atPath: manifestURL.path) ? try Data(contentsOf: manifestURL) : nil
    64	        if previousManifest != manifestData {
    65	            try manifestData.write(to: manifestURL, options: .atomic); changed.append(".ragdoll-manifest.json")
    66	        }
    67	        let pending = try git(root, ["status", "--porcelain", "--"] + managed)
    68	        guard !pending.isEmpty else { return ArchiveResult(files: 0, commit: nil) }
    69	        _ = try git(root, ["add", "--"] + managed)
    70	        _ = try git(root, ["commit", "--only", "-m", "chore(archive): sync conversations", "--"] + managed)
    71	        return ArchiveResult(files: changed.count, commit: try git(root, ["rev-parse", "--short", "HEAD"]))
    72	    }
    73	
    74	    private static func safeName(_ value: String) -> String {
    75	        let allowed = CharacterSet.alphanumerics.union(CharacterSet(charactersIn: "._-"))
    76	        let name = value.unicodeScalars.map { allowed.contains($0) ? String($0) : "_" }.joined()
    77	        return name.isEmpty || name == "." || name == ".." ? "session" : name
    78	    }
    79	    private static func hash(_ data: Data) -> String { SHA256.hash(data: data).map { String(format: "%02x", $0) }.joined() }
    80	    private static func failure(_ message: String) -> NSError { NSError(domain: "Ragdoll.Archive", code: 1, userInfo: [NSLocalizedDescriptionKey: message]) }
    81	    private static func git(_ root: URL, _ args: [String]) throws -> String {
    82	        String(decoding: try gitData(root, args), as: UTF8.self).trimmingCharacters(in: .whitespacesAndNewlines)
    83	    }
    84	    private static func gitData(_ root: URL, _ args: [String]) throws -> Data {
    85	        let process = Process(); process.executableURL = URL(fileURLWithPath: "/usr/bin/git"); process.arguments = ["-C", root.path] + args
    86	        let pipe = Pipe(); process.standardOutput = pipe; process.standardError = pipe
    87	        process.environment = ProcessInfo.processInfo.environment.merging(["GIT_TERMINAL_PROMPT": "0"]) { _, new in new }
    88	        try process.run()
    89	        let data = pipe.fileHandleForReading.readDataToEndOfFile(); process.waitUntilExit()
    90	        let text = String(decoding: data, as: UTF8.self).trimmingCharacters(in: .whitespacesAndNewlines)
    91	        guard process.terminationStatus == 0 else { throw failure("文件已保留；Git 操作失败：\(text)") }
    92	        return data
    93	    }
    94	}
   241	        return panel.runModal() == .OK ? panel.url?.path : nil
   242	    }
   243	    func chooseAttachments() -> [URL] {
   244	        let panel = NSOpenPanel(); panel.canChooseDirectories = false; panel.allowsMultipleSelection = true
   245	        return panel.runModal() == .OK ? panel.urls : []
   246	    }
   247	    private func scheduleArchive(markDirty: Bool = true) {
   248	        guard !settings.archivePath.isEmpty else { return }
   249	        if markDirty { dirtySince = dirtySince ?? Date(); dirtyGeneration += 1 }
   250	        guard dirtySince != nil else { return }
   251	        guard !scanning else { return }
   252	        archiveTask?.cancel()
   253	        let delay = max(0, min(30, 300 - Date().timeIntervalSince(dirtySince!)))
   254	        archiveTask = Task { do { try await Task.sleep(for: .seconds(delay)); await archiveNow() } catch {} }
   255	    }
   256	    func archiveNow() async {
   257	        guard let store, !settings.archivePath.isEmpty, !archiving, !scanning else { return }
   258	        archiving = true; archiveStatus = "正在保存并提交…"
   259	        let generation = dirtyGeneration
   260	        let path = settings.archivePath, excluded = settings.excludedProjects, roots = settings.locations.map(\.path)
   261	        do {
   262	            let result = try await Task.detached(priority: .utility) {
   263	                let sessions = try store.list().filter { !excluded.contains($0.project) }.compactMap { try store.session($0.id) }
   264	                return try Archive.save(sessions, to: URL(fileURLWithPath: path), sourceRoots: roots)
   265	            }.value
   266	            archiveStatus = result.commit.map { "已保存并提交 · \($0) · \(result.files) 个文件" } ?? "归档已是最新，无需提交"
   267	            lastArchive = Date(); if generation == dirtyGeneration { dirtySince = nil }
   268	        } catch { archiveStatus = "归档未完成：\(error.localizedDescription)"; self.error = error.localizedDescription }
   269	        archiving = false
   270	        if generation != dirtyGeneration { scheduleArchive(markDirty: false) }
   271	    }
   272	    func openDesktop(_ session: Session) { if let url = URL(string: "https://claude.ai/chat/\(session.nativeID)") { NSWorkspace.shared.open(url) } }
   273	    private func collectLoginLinks(_ value: JSONValue) {
   274	        if let url = URL(string: value.string), ["https", "http"].contains(url.scheme ?? ""), !loginLinks.contains(url) { loginLinks.append(url) }
   275	        for item in value.array { collectLoginLinks(item) }
   276	        for item in value.dictionary.values { collectLoginLinks(item) }
   277	    }
   278	    func nativeLogin(_ agent: AgentConfig) async {
   279	        do {
   280	            let result = try await bridge.request("native.login", ["agent": try .encode(agent)])
   281	            NSWorkspace.shared.open(URL(fileURLWithPath: result["terminalScript"].string))
   282	        } catch { self.error = error.localizedDescription }
   283	    }
   284	    func configure(_ configID: String, value: String) async {
   285	        guard let id = selectedID else { return }
   286	        do {
   287	            let result = try await bridge.request("chat.configure", ["id": .string(id), "configID": .string(configID), "value": .string(value)])
   288	            if result["configOptions"] != .null {
   289	                var info = (conversationInfo[id] ?? .object([:])).dictionary; info["configOptions"] = result["configOptions"]; conversationInfo[id] = .object(info)
   290	            }
   291	        } catch { self.error = error.localizedDescription }
   292	    }
   293	    func listNative(_ agent: AgentConfig, project: String, more: Bool = false) async {
   294	        do {
   295	            let result = try await bridge.request("chat.list", ["agent": try .encode(hydrated(agent)), "cwd": .string(project), "cursor": .string(more ? nativeCursor : "")])
   296	            nativeHistory = (more ? nativeHistory : []) + result["sessions"].array
   297	            nativeCursor = result["nextCursor"].string; nativeHistoryProject = project
   298	        } catch { self.error = error.localizedDescription }
   299	    }
   300	    func importNative(_ agent: AgentConfig, record: JSONValue) async -> Bool {
   301	        do {
   302	            let result = try await bridge.request("chat.import", ["agent": try .encode(hydrated(agent)), "cwd": .string(nativeHistoryProject), "session": record])
   303	            let session = try result["session"].decode(Session.self)
   304	            _ = try store?.save(session); try reload(); select(session.id); conversationInfo[session.id] = result["info"]; scheduleArchive(); return true
   305	        } catch { self.error = error.localizedDescription; return false }
   306	    }
   307	}
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
    45	      const entry: { child: ChildProcessWithoutNullStreams; output: string; done: Promise<unknown>; status?: Data } = { child, output: '', done: Promise.resolve() };
    46	      const append = (data: Buffer) => { entry.output = (entry.output + data.toString()).slice(-256000); };
    47	      child.stdout.on('data', append); child.stderr.on('data', append);
    48	      entry.done = new Promise(resolve => {
    49	        child.on('error', error => { entry.output += String(error); entry.status = { exitCode: 1 }; resolve(entry.status); });
    50	        child.on('exit', (exitCode, signal) => { entry.status = { exitCode, signal }; resolve(entry.status); });
    51	      });
    52	      this.terminals.set(id, entry); return { terminalId: id };
    53	    }
    54	    if (method.startsWith('terminal/')) {
    55	      const id = string(p.terminalId), entry = this.terminals.get(id);
    56	      if (!entry) throw new Error('未知终端');
    57	      if (method === 'terminal/output') return { output: entry.output, truncated: entry.output.length >= 256000, exitStatus: entry.status };
    58	      if (method === 'terminal/wait_for_exit') return await entry.done;
    59	      if (method === 'terminal/kill' || method === 'terminal/release') {
    60	        if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }
    61	        if (method === 'terminal/release') this.terminals.delete(id);
    62	        return {};
    63	      }
    64	    }
    65	    throw new Error(`不支持的客户端方法：${method}`);
    66	  }
    67	  close(): void {
    68	    for (const entry of this.terminals.values()) if (!entry.status && entry.child.pid) { try { process.kill(-entry.child.pid, 'SIGTERM'); } catch {} }
    69	    this.terminals.clear();
    70	  }
    71	}


## tool · 2026-11-16T15:35:04Z




## tool · 2026-11-16T15:35:17Z




## assistant · 2026-11-16T15:35:39Z

当前文件仍有 6 项 P2：

1. **发送消息清空 ACP 配置菜单**：[AppModel.swift:166](/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/Sources/Ragdoll/AppModel.swift:166)。空闲发送会调用恢复；[agents.ts:248](/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/runtime/src/agents.ts:248) 对已打开会话仅返回 `session`，Swift 无条件把 `info` 写成 null，模型、权限和命令菜单随之消失。仅在返回有效 `info` 时更新即可。

2. **更新 Agent 丢失用户环境变量**：[AppModel.swift:211](/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/Sources/Ragdoll/AppModel.swift:211)。Registry 更新调用 `saveAgent`，其中第 154 行将分发包环境变量直接覆盖钥匙串记录，用户 API key、自定义 HOME 等会丢失。更新路径应保留已有环境变量；显式编辑继续按用户提交内容替换。

3. **终端进程停止后继续运行**：[client-tools.ts:60](/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/runtime/src/client-tools.ts:60)、[client-tools.ts:68](/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/runtime/src/client-tools.ts:68)。终端以独立进程组启动，清理仅发送 SIGTERM 后丢弃句柄；忽略 SIGTERM 的命令将继续运行，停止会话或助手退出均无法回收。需要等待退出并在超时后 SIGKILL。

4. **ACP v2 运行错误被当作成功**：[agents.ts:174](/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/runtime/src/agents.ts:174)。已安装 v2 schema 明确允许 `idle + stopReason:error` 表示入队后的工作失败；当前所有 idle 均调用成功完成，随后发送 idle 并返回成功。此终态应调用失败回调并保留错误详情。

5. **大量历史导致 Git 参数长度超限**：[Archive.swift:47](/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/Sources/RagdollCore/Archive.swift:47)、第 67、69、70 行。每条 Git 命令把所有文件路径放进 argv；路径累计超过 macOS ARG_MAX 后，`Process.run()` 将以 E2BIG 失败，全量归档无法完成。使用 pathspec 文件/stdin，或有界分批处理。

6. **首次附件发送问题尚需留意持久状态的时机**：你已改成 `nativeStarted` 判定；确认该字段仅在 Claude 实际创建会话成功后置为 true，失败前不得提前持久化为 true。这项属于刚修改代码的复核事项，未重新运行 Claude 验证。

已静态确认 `dirtyGeneration`、外部暂存 digest 保护、`Store.list Int.max`、`RpcProcess.signalCode` 检查及 `requires_action` 活动判定解决了此前对应问题。

未运行任何测试、应用或截图，也未修改文件；以上结论来自代码和本地安装 SDK schema 的静态核对。
