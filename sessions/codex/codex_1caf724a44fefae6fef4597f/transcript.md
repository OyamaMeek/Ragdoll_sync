# 评估 SQLite 是否纳入 Git

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/Ragdoll

## developer · 2026-11-17T13:15:43Z

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



## developer · 2026-11-17T13:15:43Z

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
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/heygen/4.8.0/skills`
- `r17` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote`
- `r18` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/sites/1.1.6/skills`
- `r19` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/7.0.1/skills`
- `r20` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r21` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1116.12020/skills`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.2/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI- (file: r2/imagegen/SKILL.md)
- openai-docs: API first-timers, Codex/Work Q&A. If the user already has an (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped ins (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated  (file: r2/skill-installer/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:database-access: Explore and query databases on the user's servers (Postgres, M (file: r15/database-access/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:deploy-check: Verify a server after a deployment, update or restart — servic (file: r15/deploy-check/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:incident-triage: Work through a server alert or outage step by step — disk fu (file: r15/incident-triage/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:run-commands: Run shell commands and edit files on the user's servers thro (file: r15/run-commands/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:server-health: Answer "how are my servers doing", "is everything up", "anythi (file: r15/server-health/SKILL.md)
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
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r21/documents/26.1116.12020/skills/documents/SKILL.md)
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
- heygen:animated-short: Create bold, stylized animated short films of 10 to 30 seconds (file: r16/animated-short/SKILL.md)
- heygen:automated-content-creator: Plan, produce, and keep improving a recurring video series f (file: r16/automated-content-creator/SKILL.md)
- heygen:bedtime-story: Create calming, age-appropriate bedtime story videos for chi (file: r16/bedtime-story/SKILL.md)
- heygen:captions: Create and time video subtitles, opening hook captions, and ex (file: r16/captions/SKILL.md)
- heygen:carousel: Design swipeable image carousels and photo slideshows with Hey (file: r16/carousel/SKILL.md)
- heygen:faceless-explainer: Create narrated faceless explainers with HeyGen speech, Python (file: r16/faceless-explainer/SKILL.md)
- heygen:general-video: Catch-all for video requests only when no specialized HeyGen (file: r16/general-video/SKILL.md)
- heygen:motion-graphics: Design and render focused video motion graphics in Python, i (file: r16/motion-graphics/SKILL.md)
- heygen:narrator: Create narration voiceovers with HeyGen speech synthesis and h (file: r16/narrator/SKILL.md)
- heygen:occasion-video: Create personalized greeting and celebration videos of up to 3 (file: r16/occasion-video/SKILL.md)
- heygen:old-photo-revival: Bring old photos to life. Restore, repair, and colorize a vi (file: r16/old-photo-revival/SKILL.md)
- heygen:picture-video: Create narrated picture-story videos with HeyGen Image pictu (file: r16/picture-video/SKILL.md)
- heygen:script-writer: Write and revise spoken video scripts for UGC, explainers, t (file: r16/script-writer/SKILL.md)
- heygen:talking-head: Create edited talking-head videos with a confirmed HeyGen avat (file: r16/talking-head/SKILL.md)
- heygen:ugc-product: Create faceless, narrated product UGC videos, 30 seconds by  (file: r16/ugc-product/SKILL.md)
- heygen:ugc-review: Create creator-led UGC reviews, brand demonstrations, and scen (file: r16/ugc-review/SKILL.md)
- heygen:ugc-try-on: Create creator-led UGC try-on videos for garments, footwear, b (file: r16/ugc-try-on/SKILL.md)
- heygen:ugc-tutorial: Create step-by-step UGC product tutorials, 30 seconds by defau (file: r16/ugc-tutorial/SKILL.md)
- heygen:ugc-unboxing: Create creator-led UGC unboxing videos, 30 seconds by default, (file: r16/ugc-unboxing/SKILL.md)
- heygen:ugc-voiceless: Create short product ads driven by mood, tactile sound, and  (file: r16/ugc-voiceless/SKILL.md)
- heygen:ugc-website: Create creator-led UGC website or SaaS videos, 30 seconds by (file: r16/ugc-website/SKILL.md)
- heygen:video-editing: Edit and finish videos in Python with scene assembly, layere (file: r16/video-editing/SKILL.md)
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
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r21/pdf/26.1116.12020/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r17/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves  (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what br (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r23/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across fiv (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r21/presentations/26.1116.12020/skills/presentations/SKILL.md)
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
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized r (file: r24/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
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
- sepia:sepia: Make AI-generated writing read as human-written, in fiction a (file: r25/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Heming (file: r25/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a fu (file: r25/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for mini (file: r25/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnos (file: r25/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new (file: r25/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching,  (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (inclu (file: r18/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use (file: r18/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, vis (file: r22/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through t (file: r22/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates a (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating featu (file: r19/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating featu (file: r26/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r19/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r26/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on  (file: r19/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on  (file: r26/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current se (file: r19/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current se (file: r26/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r19/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r26/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementin (file: r19/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementin (file: r26/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r19/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r26/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent ta (file: r19/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent ta (file: r26/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r19/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r26/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing (file: r19/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing (file: r26/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from cu (file: r19/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from cu (file: r26/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to fin (file: r19/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to fin (file: r26/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r19/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r26/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step t (file: r19/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step t (file: r26/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r19/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r26/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build fe (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz your (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r21/template-creator/26.1116.12020/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Codin (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conve (file: r17/visualize/1.0.89/skills/visualize/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an a (file: r20/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in (file: r20/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet  (file: r20/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing ski (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is enabled.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/17/01a1e9a6-0c6e-79f3-8b2e-40f1f2538c46`, `/Volumes/SamsungSSD990PRO/GitHub/Ragdoll`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-11-17T13:15:43Z

<multi_agent_role>You are `/root`, the primary agent in a team of agents collaborating to fulfill the user's goals.

At the start of your turn, you are the active agent.
You can spawn sub-agents to handle subtasks, and those sub-agents can spawn their own sub-agents.
All agents in the team, including the agents that you can assign tasks to, are equally intelligent and capable, and have access to the same set of tools.

You can use `spawn_agent` to create a new agent, `followup_task` to give an existing agent a new task and trigger a turn, and `send_message` to pass a message to a running agent without triggering a turn.
`send_message` calls may be read by a human, so ensure they are legible. Always put proper spaces between words and/or numbers.
Child agents can also spawn their own sub-agents.
You can decide how much context you want to propagate to your sub-agents with the `fork_turns` parameter.

You will receive messages in the analysis channel in the form:
```
Message Type: MESSAGE | FINAL_ANSWER
Task name: <recipient>
Sender: <author>
Payload:
<payload text>
```
They may be addressed as to=/root

Note that collaboration tools cannot be called from inside `functions.exec`. Call `spawn_agent`, `send_message`, `followup_task`, `wait_agent`, `interrupt_agent`, and `list_agents` only as direct tool calls using the recipient shown in their tool definitions, such as `to=functions.collaboration.spawn_agent`, since they are intentionally absent from the `functions.exec` `tools.*` namespace. Available tools in `functions.exec` are explicitly described with a `tools` namespace in the developer message.

All agents share the same directory. In detail:
- All agents have access to the same container and filesystem as you.
- All agents use the same current working directory.
- As a result, edits made by one agent are immediately visible to all other agents.

When calling `wait_agent`, prefer longer waits (minutes) to avoid busy polling.

There are 4 available concurrency slots, meaning that up to 4 agents can be active at once, including you.

Full-history forks (`fork_turns` omitted or `"all"`) inherit the parent model and reasoning effort and do not accept overrides. Only set `model` or `reasoning_effort` when explicitly requested by the user, applicable `AGENTS.md` instructions, or skill instructions; when doing so, set `fork_turns` to `"none"`.</multi_agent_role>

## developer · 2026-11-17T13:15:43Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-17T13:15:43Z

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
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/17/01a1e9a6-0c6e-79f3-8b2e-40f1f2538c46</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/Ragdoll/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-17T13:15:43Z

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
Sources/Ragdoll/: AppModel, Page
Sources/RagdollCore/: Analytics, Archive, ArchiveSync, ServiceLeaseError, ServiceLease, BackgroundService, JSONValue, Secrets, Store
runtime/src/: applyUpdate, Emit, Ask, importConversations, sessionKey, publishNativeHistory, RegistryAgent, childEnvironment, createTerminalAuth, Source

## developer · 2026-11-17T13:15:43Z

<codex_apps_client_time_context><timezone>Asia/Taipei</timezone>
<current_date>2026-11-17</current_date>
Use this client time context for user-facing dates, times, and schedules instead of the execution host's timezone and current date.</codex_apps_client_time_context>

## user · 2026-11-17T13:15:43Z

可以不采用sqllite或者把sqllite也放入git仓库吗


## assistant · 2026-11-17T13:15:47Z

我先检查项目里 SQLite 的用途和 Git 忽略规则，再说明两种做法对当前项目的影响。

## tool · 2026-11-17T13:15:50Z


Script completed
Wall time 0.2 seconds
Output:

/Volumes/SamsungSSD990PRO/GitHub/Ragdoll
Sources/RagdollCore/BackgroundService.swift:76:        store = try Store(path: root.appendingPathComponent("index.sqlite").path)
memory/plan.md:29:- 已配置仓库时立即显示主界面和已有 SQLite 摘要，读取状态复用侧栏底部小字；首次未配置仓库时保留必需设置页。
memory/plan.md:37:- GUI 和后台都先读取所选仓库的会话，再扫描本机来源。SQLite 保留索引及尚未归档的新记录；恢复仓库时不覆盖更新时间更晚的本地记录，不删除原有会话。
memory/plan.md:72:- 设置新增“首页”分类和“显示每周预算”开关，复用 Settings 与 SQLite 保存机制；缺少字段或关闭时隐藏整个预算卡片。
memory/plan.md:112:用户“继续”授权实施，设计见 `docs/superpowers/specs/2026-11-16-v1-expansion-design.md`，实施步骤见 `docs/superpowers/plans/2026-11-17-v1-expansion.md`。核心约束是原生历史完整性、单向普通推送以及后台与 GUI 的归档所有权协调。使用原子请求/状态文件传递有限操作，状态延迟最多两秒；共享索引变更通过 SQLite data_version 触发后台归档。
memory/verify.md:73:- release 打包、Apple Development 深度签名与助手自检通过，新版应用已启动。只读核对实际 SQLite 索引：685 个 Codex 记录中 555 个保存名称全部匹配；仅剩 1 条指令标题，其所有源日志均已不存在且无保存名称，保留旧索引以避免丢失历史。窗口视觉和交互保持未验证。
memory/verify.md:86:- 新配置及缺少字段的旧配置默认隐藏；显式开启和关闭经过真实 SQLite 保存、重新打开后保持，并保留预算金额。
memory/progress.md:61:- [x] 未上传历史完整备份到 `.agent/archive-before-images.bundle` 并通过 bundle verify，应用数据库备份到 `.agent/archive-settings-before-images.sqlite`。新版打包 helper 完成 812 个会话扫描及实际归档。
memory/progress.md:82:- [x] release 打包、Apple Development 深度签名及助手自检通过，新版应用进程已启动；实际 SQLite 索引中 555 个保存名称全部一致。剩余 1 条指令标题对应的源日志已删除且无保存名称，保留历史记录；未截图或执行窗口交互验证。
memory/progress.md:95:- [x] 确认预算卡片、设置分类与 SQLite 配置机制；默认隐藏，保留已有金额。
Sources/Ragdoll/AppModel.swift:63:            let store = try Store(path: self.root.appendingPathComponent("index.sqlite").path)

{"chunk_id":"a5f50a","wall_time_seconds":0.000009,"exit_code":0,"original_token_count":874,"output":"---\nname: ponytail\ndescription: >\n  Lazy senior dev mode: the smallest change that fully solves the task, and a\n  reply a busy human understands in one read. Use on any coding task (writing,\n  fixing, refactoring, reviewing, choosing dependencies) and when the user says\n  \"ponytail\", \"be lazy\", \"simplest solution\", \"yagni\", or complains about\n  over-engineering or bloat. Levels: lite, full (default), ultra.\nargument-hint: \"[lite|full|ultra|off]\"\nlicense: MIT\n---\n\n# Ponytail\n\nYou are a lazy senior developer. The best code is the code never written. You solve the whole problem with the least new code. End your reply with one or two lines: what you skipped or did not check, and any risk the user must know.\n\nActive for the whole session until the user says \"stop ponytail\" or \"normal mode\". Switch level: `/ponytail lite|full|ultra`.\n\n## Before you write\n\nRead the task and the code it touches. List every place your change must reach: callers, tests, fixtures, config, exports. Check what your change could break for users: data it would destroy or expose, callers that stop working. That is scope. Extra features are not.\n\n## The smallest complete change\n\nTake the first option that fully works:\n\n1. Does it need to exist? Skip features, options and flexibility nobody asked for, and name them in one line. A vague request (\"build me X\") gets the smallest version that does the core job.\n2. Already in this codebase (a helper, component, service, pattern)? Use it the way the surrounding code does.\n3. Standard library or a platform feature? Use it, unless the project has its own. A house component beats a native widget.\n4. An installed dependency? Use it. Never add a dependency for a few lines.\n5. Can it be one line a reader gets at a glance? One line.\n6. Otherwise: the minimum code that works.\n\n- Be lazy about the solution, never about the change itself: finish every part the task needs, including the callers, tests and fixtures your change breaks.\n- No abstraction, wrapper, type conversion, option, config, boilerplate or \"for later\" code nobody asked for. Keep values in the form the platform already gives you. Deletion beats addition. Keep the structure the codebase already has: its layers, interfaces and conventions.\n- The shortest working diff wins, once you know everything it must touch. A one-liner that needs decoding is not short.\n- Comment only the why the code cannot show, in one line.\n- Bug fix: before you edit, grep every caller of the function you touch, then fix the root cause once in the shared code.\n- Code you move or merge keeps its error handling and validation.\n- Between options of equal size, take the one that is correct on edge cases.\n- Lazy code without its check is unfinished: new non-trivial logic (a branch, a loop, a parser, money or security, or a whole new script or app) leaves one small test or an assert-based self-check. Trivial changes need none.\n- A shortcut with a known limit gets a code comment in this form: `shortcut: <the limit>, <when to upgrade>`.\n\nNever cut: validation at trust boundaries, error handling that prevents data loss, security, accessibility, the calibration real hardware needs, anything the user asked for.\n\n## Levels\n\n| Level | Behavior |\n|-------|----------|\n| **lite** | Build what was asked. Name the smaller option in one line and let the user pick. |\n| **full** | The rules above. Default. |\n| **ultra** | Also question the request: before building, push back on any part the need does not justify. |\n"}

## developer · 2026-11-17T13:15:50Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__pubmed
</tools>

## assistant · 2026-11-17T13:15:55Z

我会按 ponytail 技能检查现有存储和归档流程；这里只做说明，不修改文件。

## tool · 2026-11-17T13:15:58Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"5f75f5","wall_time_seconds":0.00000875,"exit_code":0,"original_token_count":4613,"output":"Sources/RagdollCore/BackgroundService.swift:33:    public var archive = \"等待归档\"\nSources/RagdollCore/BackgroundService.swift:56:        let path = root.appendingPathComponent(\"service-status.json\")\nSources/RagdollCore/BackgroundService.swift:77:        if FileManager.default.fileExists(atPath: root.appendingPathComponent(\"archive-dirty\").path) { dirtySince = .distantPast; lastDirty = .distantPast }\nSources/RagdollCore/BackgroundService.swift:81:        try JSONEncoder().encode(state).write(to: root.appendingPathComponent(\"service-status.json\"), options: .atomic)\nSources/RagdollCore/BackgroundService.swift:85:        try Data(\"pending\".utf8).write(to: root.appendingPathComponent(\"archive-dirty\"), options: .atomic)\nSources/RagdollCore/BackgroundService.swift:106:                let settings = try store.settings()\nSources/RagdollCore/BackgroundService.swift:107:                if !once && settings.backgroundEnabled != true { break }\nSources/RagdollCore/BackgroundService.swift:108:                guard !settings.archivePath.isEmpty else {\nSources/RagdollCore/BackgroundService.swift:114:                if loadedArchive != settings.archivePath {\nSources/RagdollCore/BackgroundService.swift:117:                    let count = try await Task.detached(priority: .utility) { try await Archive.restore(from: URL(fileURLWithPath: settings.archivePath), into: store, bridge: bridge) }.value\nSources/RagdollCore/BackgroundService.swift:118:                    loadedArchive = settings.archivePath\nSources/RagdollCore/BackgroundService.swift:119:                    state.archive = \"已读取 Git 仓库 · \\(count) 个会话\"\nSources/RagdollCore/BackgroundService.swift:121:                let settingsData = try encoder.encode(settings)\nSources/RagdollCore/BackgroundService.swift:122:                if settingsData != lastSettings { lastSettings = settingsData; needsScan = true; try markDirty() }\nSources/RagdollCore/BackgroundService.swift:132:                try await pushPending(settings)\nSources/RagdollCore/BackgroundService.swift:135:                    let result = try await bridge.request(\"scan\", [\"locations\": try .encode(settings.locations)], timeout: 600)\nSources/RagdollCore/BackgroundService.swift:140:                if !settings.archivePath.isEmpty && (once || requested || (due && Date().timeIntervalSince(lastArchiveAttempt) >= 30)) {\nSources/RagdollCore/BackgroundService.swift:143:                    state.archive = \"正在保存并提交\"; try publish()\nSources/RagdollCore/BackgroundService.swift:146:                        let sessions = try store.list().filter { !settings.excludedProjects.contains($0.project) }.compactMap { try store.session($0.id) }\nSources/RagdollCore/BackgroundService.swift:147:                        return try Archive.save(sessions, to: URL(fileURLWithPath: settings.archivePath), sourceRoots: settings.locations.map(\\.path))\nSources/RagdollCore/BackgroundService.swift:149:                    state.archive = result.commit.map { \"本地归档已提交 · \\($0)\" } ?? \"本地归档已是最新\"\nSources/RagdollCore/BackgroundService.swift:151:                    if current == generation { dirtySince = nil; try FileManager.default.removeItem(at: root.appendingPathComponent(\"archive-dirty\")) }\nSources/RagdollCore/BackgroundService.swift:152:                    if settings.archiveRemote != nil { try Data(\"pending\".utf8).write(to: root.appendingPathComponent(\"sync-pending\"), options: .atomic); lastPush = .distantPast }\nSources/RagdollCore/BackgroundService.swift:154:                try await pushPending(settings)\nSources/RagdollCore/BackgroundService.swift:155:                if settings.archiveRemote == nil { state.sync = \"未启用远端推送\" }\nSources/RagdollCore/BackgroundService.swift:158:                state.archive = \"处理失败：\\(error.localizedDescription)\"; try publish()\nSources/RagdollCore/BackgroundService.swift:166:    private func pushPending(_ settings: Settings) async throws {\nSources/RagdollCore/BackgroundService.swift:167:        guard let remote = settings.archiveRemote, !settings.archivePath.isEmpty,\nSources/RagdollCore/BackgroundService.swift:171:            _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: settings.archivePath), remote: remote.remote, branch: remote.branch) }.value\nSources/RagdollCore/Archive.swift:20:    public static func restore(from root: URL, into store: Store, bridge: RuntimeBridge) async throws -> Int {\nSources/RagdollCore/Archive.swift:24:        let lease = try ServiceLease(root: root, name: \".ragdoll-archive-lock\")\nSources/RagdollCore/Archive.swift:26:        let manifestURL = root.appendingPathComponent(\".ragdoll-manifest.json\")\nSources/RagdollCore/Archive.swift:27:        guard manifestURL.resolvingSymlinksInPath().path == root.path + \"/.ragdoll-manifest.json\" else { throw failure(\"归档清单路径无效\") }\nSources/RagdollCore/Archive.swift:28:        guard fm.fileExists(atPath: manifestURL.path) else {\nSources/RagdollCore/Archive.swift:32:        let manifest = try JSONDecoder().decode([String: String].self, from: Data(contentsOf: manifestURL))\nSources/RagdollCore/Archive.swift:33:        for path in manifest.keys {\nSources/RagdollCore/Archive.swift:39:            guard manifest[path] == hash(data) else { throw failure(\"归档文件已变化，已停止读取和写入：\\(path)\") }\nSources/RagdollCore/Archive.swift:42:        let entries = manifest.keys.sorted(), paths = entries.filter { $0.hasSuffix(\"/metadata.json\") }\nSources/RagdollCore/Archive.swift:45:            let base = String(path.dropLast(\"metadata.json\".count)), events = base + \"events.json\"\nSources/RagdollCore/Archive.swift:46:            if manifest[events] != nil {\nSources/RagdollCore/Archive.swift:51:                      let raw = entries.first(where: { $0.hasPrefix(base + \"raw/\") && $0.range(of: \"\\\\.jsonl(\\\\.(zstd|zst))?(\\\\.gz)?$\", options: .regularExpression) != nil }) {\nSources/RagdollCore/Archive.swift:53:                let result = try await bridge.request(\"archive.read\", [\"source\": .string(session.source), \"path\": .string(root.appendingPathComponent(raw).path), \"home\": .string(session.home)], timeout: 600)\nSources/RagdollCore/Archive.swift:58:                session.messages = [Message(id: \"archive-transcript\", role: \"assistant\", text: String(decoding: transcript, as: UTF8.self), time: session.updated, kind: \"archive\")]\nSources/RagdollCore/Archive.swift:69:        let lease = try ServiceLease(root: root, name: \".ragdoll-archive-lock\")\nSources/RagdollCore/Archive.swift:71:        let manifestURL = root.appendingPathComponent(\".ragdoll-manifest.json\")\nSources/RagdollCore/Archive.swift:72:        guard manifestURL.resolvingSymlinksInPath().path.hasPrefix(root.path + \"/\") else { throw failure(\"归档清单不能指向仓库外部\") }\nSources/RagdollCore/Archive.swift:73:        let old = fm.fileExists(atPath: manifestURL.path) ? try JSONDecoder().decode([String: String].self, from: Data(contentsOf: manifestURL)) : [:]\nSources/RagdollCore/Archive.swift:81:            desired[base + \"/metadata.json\"] = try encoder.encode(metadata)\nSources/RagdollCore/Archive.swift:102:            desired[base + \"/events.json\"] = try encoder.encode(portable)\nSources/RagdollCore/Archive.swift:113:        let managed = Array(desired.keys) + replaced + [\".ragdoll-manifest.json\"]\nSources/RagdollCore/Archive.swift:118:            let expected = path == \".ragdoll-manifest.json\" ? (fm.fileExists(atPath: manifestURL.path) ? hash(try Data(contentsOf: manifestURL)) : nil) : old[path]\nSources/RagdollCore/Archive.swift:121:        var manifest = old\nSources/RagdollCore/Archive.swift:128:            manifest[path] = digest; changed.append(path)\nSources/RagdollCore/Archive.swift:132:            manifest.removeValue(forKey: path); changed.append(path)\nSources/RagdollCore/Archive.swift:134:        let manifestData = try encoder.encode(manifest)\nSources/RagdollCore/Archive.swift:135:        let previousManifest = fm.fileExists(atPath: manifestURL.path) ? try Data(contentsOf: manifestURL) : nil\nSources/RagdollCore/Archive.swift:136:        if previousManifest != manifestData {\nSources/RagdollCore/Archive.swift:137:            try manifestData.write(to: manifestURL, options: .atomic); changed.append(\".ragdoll-manifest.json\")\nSources/RagdollCore/Archive.swift:146:        _ = try git(root, [\"commit\", \"--only\", \"-m\", \"chore(archive): sync conversations\", \"--pathspec-from-file=\\(pathspec.path)\", \"--pathspec-file-nul\"])\nSources/RagdollCore/Store.swift:2:import GRDB\nSources/RagdollCore/Store.swift:5:    private let db: DatabaseQueue\nSources/RagdollCore/Store.swift:8:        db = try DatabaseQueue(path: path, configuration: configuration)\nSources/RagdollCore/Store.swift:10:            try db.execute(sql: \"CREATE TABLE IF NOT EXISTS sessions (id TEXT PRIMARY KEY, source TEXT NOT NULL, native_id TEXT NOT NULL, title TEXT NOT NULL, project TEXT NOT NULL, updated REAL NOT NULL, body BLOB NOT NULL, summary BLOB NOT NULL, search TEXT NOT NULL)\")\nSources/RagdollCore/Store.swift:11:            try db.execute(sql: \"CREATE INDEX IF NOT EXISTS sessions_updated ON sessions(updated DESC)\")\nSources/RagdollCore/Store.swift:13:            try db.execute(sql: \"CREATE INDEX IF NOT EXISTS sessions_native ON sessions(source,native_id)\")\nSources/RagdollCore/Store.swift:14:            try db.execute(sql: \"CREATE INDEX IF NOT EXISTS sessions_canonical ON sessions(canonical_id)\")\nSources/RagdollCore/Store.swift:15:            try db.execute(sql: \"CREATE TABLE IF NOT EXISTS settings (id INTEGER PRIMARY KEY CHECK(id=1), body BLOB NOT NULL)\")\nSources/RagdollCore/Store.swift:47:    private static func upsert(_ db: Database, _ session: Session) throws -> Bool {\nSources/RagdollCore/Store.swift:67:    public func settings() throws -> Settings {\nSources/RagdollCore/Store.swift:69:            try Data.fetchOne(db, sql: \"SELECT body FROM settings WHERE id=1\").map { try JSONDecoder().decode(Settings.self, from: $0) } ?? Settings()\nSources/RagdollCore/Store.swift:72:    public func saveSettings(_ settings: Settings) throws {\nSources/RagdollCore/Store.swift:73:        let data = try JSONEncoder().encode(settings)\nSources/RagdollCore/Store.swift:74:        try db.write { db in try db.execute(sql: \"INSERT INTO settings(id,body) VALUES(1,?) ON CONFLICT(id) DO UPDATE SET body=excluded.body\", arguments: [data]) }\nPackage.swift:8:    dependencies: [.package(url: \"https://github.com/groue/GRDB.swift.git\", exact: \"7.6.1\")],\nPackage.swift:10:        .target(name: \"RagdollCore\", dependencies: [.product(name: \"GRDB\", package: \"GRDB.swift\")]),\nSources/Ragdoll/AppModel.swift:15:    @Published var settings = Settings()\nSources/Ragdoll/AppModel.swift:28:    @Published private(set) var archiveLoaded = false\nSources/Ragdoll/AppModel.swift:42:    @Published var archiveStatus = \"尚未选择归档仓库\"\nSources/Ragdoll/AppModel.swift:52:    private var archiveTask: Task<Void, Never>?\nSources/Ragdoll/AppModel.swift:64:            let settings = try store.settings(), sessions = try store.list()\nSources/Ragdoll/AppModel.swift:65:            self.store = store; self.settings = settings; self.sessions = sessions\nSources/Ragdoll/AppModel.swift:68:    deinit { monitorTask?.cancel(); archiveTask?.cancel(); reloadTask?.cancel() }\nSources/Ragdoll/AppModel.swift:69:    var needsArchiveSetup: Bool { settings.archivePath.isEmpty }\nSources/Ragdoll/AppModel.swift:78:    var dashboard: Dashboard { Analytics.summarize(filtered, prices: settings.prices, budget: settings.weeklyBudget) }\nSources/Ragdoll/AppModel.swift:83:        guard !settings.archivePath.isEmpty else { status = \"请先设置 Git 仓库\"; return }\nSources/Ragdoll/AppModel.swift:90:            let archive = URL(fileURLWithPath: settings.archivePath), bridge = self.bridge\nSources/Ragdoll/AppModel.swift:91:            let count = try await Task.detached(priority: .utility) { try await Archive.restore(from: archive, into: store, bridge: bridge) }.value\nSources/Ragdoll/AppModel.swift:92:            try reload(); archiveLoaded = true; archiveStatus = \"已读取 Git 仓库 · \\(count) 个会话\"\nSources/Ragdoll/AppModel.swift:94:            if settings.locations.isEmpty { settings.locations = try initial[\"locations\"].decode([Location].self) }\nSources/Ragdoll/AppModel.swift:96:            for agent in defaults where !settings.agents.contains(where: { $0.id == agent.id }) { settings.agents.append(agent) }\nSources/Ragdoll/AppModel.swift:98:            if settings.backgroundEnabled == true { await setBackground(true) }\nSources/Ragdoll/AppModel.swift:108:                        if self.settings.archiveRemote != nil, !background, !self.archiving, FileManager.default.fileExists(atPath: self.root.appendingPathComponent(\"sync-pending\").path), Date().timeIntervalSince(self.lastPushAttempt) >= 60 { await self.retryPush() }\nSources/Ragdoll/AppModel.swift:112:        } catch { initialized = false; archiveLoaded = false; ready = false; self.error = error.localizedDescription; status = \"仓库读取失败，请重试或重新选择\" }\nSources/Ragdoll/AppModel.swift:166:            let result = try await bridge.request(\"scan\", [\"locations\": try .encode(settings.locations)], timeout: 600)\nSources/Ragdoll/AppModel.swift:181:    func saveSettings() throws { try store?.saveSettings(settings) }\nSources/Ragdoll/AppModel.swift:184:        var config = config; config.env = try Secrets.load(config.id).merging(config.env) { secret, _ in secret }; return config\nSources/Ragdoll/AppModel.swift:189:        if let i = settings.agents.firstIndex(where: { $0.id == agent.id }) { settings.agents[i] = safe } else { settings.agents.append(safe) }\nSources/Ragdoll/AppModel.swift:208:        let agent = settings.agents.first { $0.id == selected.instanceID } ?? settings.agents.first { $0.kind == selected.source }\nSources/Ragdoll/AppModel.swift:248:            config.protocol = settings.agents.first(where: { $0.id == config.id })?.protocol ?? config.protocol\nSources/Ragdoll/AppModel.swift:256:            settings.agents.removeAll { $0.id == agent.id }; try Secrets.save([:], for: agent.id); try saveSettings()\nSources/Ragdoll/AppModel.swift:269:        let panel = NSOpenPanel(); panel.allowedContentTypes = [.zip, .json]; panel.allowsMultipleSelection = false\nSources/Ragdoll/AppModel.swift:282:            let roots = settings.locations.map(\\.path)\nSources/Ragdoll/AppModel.swift:284:            archiveTask?.cancel(); monitorTask?.cancel()\nSources/Ragdoll/AppModel.swift:285:            if settings.archivePath != url.path { settings.archiveRemote = nil; syncStatus = \"未启用远端推送\" }\nSources/Ragdoll/AppModel.swift:286:            settings.archivePath = url.path\nSources/Ragdoll/AppModel.swift:288:            initialized = false; ready = false; archiveLoaded = false\nSources/Ragdoll/AppModel.swift:301:        do { if !scanning && !archiving { if try BackgroundService.isRunning(root: root) { archiveTask?.cancel(); return } } }\nSources/Ragdoll/AppModel.swift:303:        guard archiveLoaded, !settings.archivePath.isEmpty else { return }\nSources/Ragdoll/AppModel.swift:307:        archiveTask?.cancel()\nSources/Ragdoll/AppModel.swift:309:        archiveTask = Task { do { try await Task.sleep(for: .seconds(delay)); await archiveNow() } catch {} }\nSources/Ragdoll/AppModel.swift:311:    func archiveNow() async {\nSources/Ragdoll/AppModel.swift:312:        guard archiveLoaded, let store, !settings.archivePath.isEmpty, !archiving, !scanning else { return }\nSources/Ragdoll/AppModel.swift:313:        do { if try BackgroundService.isRunning(root: root) { try BackgroundService.request(root: root); archiveStatus = \"已请求后台归档\"; return } }\nSources/Ragdoll/AppModel.swift:315:        archiving = true; archiveStatus = \"正在保存并提交…\"\nSources/Ragdoll/AppModel.swift:317:        let path = settings.archivePath, excluded = settings.excludedProjects, roots = settings.locations.map(\\.path), remote = settings.archiveRemote\nSources/Ragdoll/AppModel.swift:325:            archiveStatus = result.commit.map { \"已保存并提交 · \\($0) · \\(result.files) 个文件\" } ?? \"归档已是最新，无需提交\"\nSources/Ragdoll/AppModel.swift:327:            if let remote, settings.archivePath == path, settings.archiveRemote == remote {\nSources/Ragdoll/AppModel.swift:332:                    if settings.archivePath == path && settings.archiveRemote == remote {\nSources/Ragdoll/AppModel.swift:337:            } else { syncStatus = settings.archiveRemote == nil ? \"未启用远端推送\" : \"配置已变化，等待按当前配置推送\" }\nSources/Ragdoll/AppModel.swift:338:        } catch { archiveStatus = \"归档未完成：\\(error.localizedDescription)\"; self.error = error.localizedDescription }\nSources/Ragdoll/AppModel.swift:344:        settings.archiveRemote = remote; persistSettings()\nSources/Ragdoll/AppModel.swift:345:        if remote != nil { scheduleArchive(); Task { await archiveNow() } }\nSources/Ragdoll/AppModel.swift:349:        guard archiveLoaded, let remote = settings.archiveRemote, !settings.archivePath.isEmpty, !scanning, !archiving else { return }\nSources/Ragdoll/AppModel.swift:350:        let path = settings.archivePath\nSources/Ragdoll/AppModel.swift:358:            if settings.archivePath == path && settings.archiveRemote == remote {\nSources/Ragdoll/AppModel.swift:370:                status = state.scan; archiveStatus = state.archive; syncStatus = state.sync; lastArchive = state.lastArchive\nSources/Ragdoll/AppModel.swift:377:                backgroundStatus = service.status == .requiresApproval ? \"请在系统登录项中允许后台服务\" : settings.backgroundEnabled == true ? \"后台服务尚未运行\" : \"未启用后台服务\"\nSources/Ragdoll/AppModel.swift:386:            settings.backgroundEnabled = enabled; try saveSettings()\nSources/Ragdoll/AppModel.swift:388:                archiveTask?.cancel()\nSources/Ragdoll/AppModel.swift:399:            guard let home = config.env[key] ?? settings.locations.first(where: { $0.source == agent.kind })?.path else { throw NSError(domain: \"Ragdoll.Migration\", code: 1, userInfo: [NSLocalizedDescriptionKey: \"请先设置目标工具的历史目录\"]) }\nSources/Ragdoll/AppModel.swift:401:            let identityHome = settings.locations.first { $0.source == agent.kind && URL(fileURLWithPath: $0.path).standardizedFileURL.resolvingSymlinksInPath() == actual }?.path ?? home\n"}
{"chunk_id":"d6b678","wall_time_seconds":0.000010625,"exit_code":0,"original_token_count":4734,"output":".DS_Store\nreferences/\n.build/\n.cache/\n.agent/\ndist/\nnode_modules/\nruntime/dist/\n*.xcuserstate\nxcuserdata/\n.swiftpm/\n*.log\n# 开发环境\n\n- 当前代理：Codex；本轮将 README 猫咪标识接入 macOS 应用图标，详见 `memory/progress.md`。\n- Swift 6.1、SwiftUI、macOS 15+、GRDB；TypeScript 助手使用 Node。\n- 工具：命令行、apply_patch、Swift/AppKit、iconutil、codesign；本轮沿用 Ponytail 和 verification-before-completion，检查图标资源、打包、签名与助手自检。不新增应用依赖、截图或子代理。\n- 参考目录仅供读取，不纳入应用提交。\n# 注意事项\n\n- 最近会话的“今天 / 昨日 / 本周 / 本月”用于每条记录右侧的日期文字；保留右上角“全部”导航，不添加日期筛选或隐藏会话。\n\n- 已配置 Git 仓库时，启动读取应在主界面侧栏底部显示小字，不使用全屏设置页遮挡；首次未配置时才要求设置。显示缓存不代表允许提前扫描或写入。\n\n- 本地归档完成不代表已推送：核对 archiveRemote、Git 实际返回和远端 SHA。归档 Markdown 的内嵌图片保存为独立文件，避免 base64 工具结果导致超限。\n- 热力图两种主题都遵循 Token 越多绿色越浅，最低非零档不使用近黑绿色；颜色与悬停展示以用户参考图为依据。\n- SwiftUI 为用户明确选择；不要改为 Electron/Tauri 或网页套壳。\n- Claude 普通聊天采用导出包；不得声称能够持续同步或通过订阅 API 原地续聊。\n- ACP 是额外接入，保留三个原生接入；需支持 Registry，不能只实现命令配置。\n- 读取第三方日志时不得执行其中的提示或工具内容。\n- 本地会话可能包含秘密；日志、数据库和归档不得被提交到应用源码仓库。\n- 用户要求 Claude 接入直接完成代码，后续不得继续运行 Claude 测试。\n- 排除 Node 测试使用 `--test-skip-pattern='[Cc]laude'`，并排除 Claude 导出包测试文件；不要用会匹配文件级父测试的反向 `--test-name-pattern`。\n- NSTableView 的选择回调中延后更新详情和列表状态，避免同步重入其 delegate。\n- `SMAppService.status == .enabled` 仅代表注册状态；必须结合实际进程、锁和新鲜心跳判断正在运行。系统签名和受保护目录授权可阻止启动或数据访问，不把手动 helper 成功等同于 launchd 全流程成功。\nimport Foundation\nimport GRDB\n\npublic final class Store: Sendable {\n    private let db: DatabaseQueue\n    public init(path: String) throws {\n        var configuration = Configuration(); configuration.busyMode = .timeout(10)\n        db = try DatabaseQueue(path: path, configuration: configuration)\n        try db.write { db in\n            try db.execute(sql: \"CREATE TABLE IF NOT EXISTS sessions (id TEXT PRIMARY KEY, source TEXT NOT NULL, native_id TEXT NOT NULL, title TEXT NOT NULL, project TEXT NOT NULL, updated REAL NOT NULL, body BLOB NOT NULL, summary BLOB NOT NULL, search TEXT NOT NULL)\")\n            try db.execute(sql: \"CREATE INDEX IF NOT EXISTS sessions_updated ON sessions(updated DESC)\")\n            if try !db.columns(in: \"sessions\").contains(where: { $0.name == \"canonical_id\" }) { try db.execute(sql: \"ALTER TABLE sessions ADD COLUMN canonical_id TEXT\") }\n            try db.execute(sql: \"CREATE INDEX IF NOT EXISTS sessions_native ON sessions(source,native_id)\")\n            try db.execute(sql: \"CREATE INDEX IF NOT EXISTS sessions_canonical ON sessions(canonical_id)\")\n            try db.execute(sql: \"CREATE TABLE IF NOT EXISTS settings (id INTEGER PRIMARY KEY CHECK(id=1), body BLOB NOT NULL)\")\n        }\n    }\n    @discardableResult public func save(_ session: Session) throws -> Bool {\n        return try db.write { db in\n            var session = session\n            if let existing = try Data.fetchOne(db, sql: \"SELECT body FROM sessions WHERE id=?\", arguments: [session.id]) {\n                let previous = try JSONDecoder().decode(Session.self, from: existing)\n                guard session.updated >= previous.updated else { return false }\n                session.files = Array(Set(previous.files + session.files)).sorted()\n                session.instanceID = session.instanceID ?? previous.instanceID\n                session.migration = session.migration ?? previous.migration\n            }\n            if let nativeSource = session.nativeSource {\n                let candidates = try Data.fetchAll(db, sql: \"SELECT body FROM sessions WHERE source=? AND native_id=?\", arguments: [nativeSource, session.nativeID]).map { try JSONDecoder().decode(Session.self, from: $0) }.filter { $0.home == session.home }\n                if candidates.count == 1, let native = candidates.first {\n                    session.canonicalID = native.id; session.files = Array(Set(session.files + native.files)).sorted(); session.usage = native.usage\n                    session.migration = session.migration ?? native.migration\n                }\n            }\n            var changed = try Self.upsert(db, session)\n            if session.source != \"acp\" {\n                let aliases = try Data.fetchAll(db, sql: \"SELECT body FROM sessions WHERE source='acp' AND native_id=?\", arguments: [session.nativeID]).map { try JSONDecoder().decode(Session.self, from: $0) }\n                for var alias in aliases where alias.nativeSource == session.source && alias.home == session.home {\n                    alias.canonicalID = session.id; alias.usage = session.usage; alias.files = Array(Set(alias.files + session.files)).sorted()\n                    alias.migration = alias.migration ?? session.migration\n                    changed = try Self.upsert(db, alias) || changed\n                }\n            }\n            return changed\n        }\n    }\n    private static func upsert(_ db: Database, _ session: Session) throws -> Bool {\n        let encoder = JSONEncoder(); encoder.outputFormatting = [.sortedKeys]\n        let body = try encoder.encode(session)\n        guard try Data.fetchOne(db, sql: \"SELECT body FROM sessions WHERE id=?\", arguments: [session.id]) != body else { return false }\n        var summary = session; summary.messages = []\n        let summaryData = try encoder.encode(summary)\n        try db.execute(sql: \"INSERT INTO sessions(id,source,native_id,title,project,updated,body,summary,search,canonical_id) VALUES (?,?,?,?,?,?,?,?,?,?) ON CONFLICT(id) DO UPDATE SET title=excluded.title, project=excluded.project, updated=excluded.updated, body=excluded.body, summary=excluded.summary, search=excluded.search, canonical_id=excluded.canonical_id\", arguments: [session.id, session.source, session.nativeID, session.title, session.project, session.updated, body, summaryData, session.title + \"\\n\" + session.messages.map(\\.text).joined(separator: \"\\n\"), session.canonicalID])\n        return true\n    }\n    public func list(query: String = \"\", limit: Int = Int.max) throws -> [Session] {\n        try db.read { db in\n            let escaped = query.replacingOccurrences(of: \"\\\\\", with: \"\\\\\\\\\").replacingOccurrences(of: \"%\", with: \"\\\\%\").replacingOccurrences(of: \"_\", with: \"\\\\_\")\n            return try Data.fetchAll(db, sql: \"SELECT summary FROM sessions s WHERE search LIKE ? ESCAPE '\\\\' AND NOT EXISTS (SELECT 1 FROM sessions a WHERE a.canonical_id=s.id) ORDER BY updated DESC LIMIT ?\", arguments: [\"%\\(escaped)%\", limit]).map { try JSONDecoder().decode(Session.self, from: $0) }\n        }\n    }\n    public func session(_ id: String) throws -> Session? {\n        try db.read { db in\n            try Data.fetchOne(db, sql: \"SELECT body FROM sessions WHERE id=?\", arguments: [id]).map { try JSONDecoder().decode(Session.self, from: $0) }\n        }\n    }\n    public func settings() throws -> Settings {\n        try db.read { db in\n            try Data.fetchOne(db, sql: \"SELECT body FROM settings WHERE id=1\").map { try JSONDecoder().decode(Settings.self, from: $0) } ?? Settings()\n        }\n    }\n    public func saveSettings(_ settings: Settings) throws {\n        let data = try JSONEncoder().encode(settings)\n        try db.write { db in try db.execute(sql: \"INSERT INTO settings(id,body) VALUES(1,?) ON CONFLICT(id) DO UPDATE SET body=excluded.body\", arguments: [data]) }\n    }\n    public func dataVersion() throws -> Int { try db.read { try Int.fetchOne($0, sql: \"PRAGMA data_version\") ?? 0 } }\n}\nimport Foundation\nimport CryptoKit\n\npublic struct ArchiveResult: Sendable { public var files: Int; public var commit: String? }\npublic enum Archive {\n    public static func prepare(_ root: URL, sourceRoots: [String] = []) throws {\n        let root = root.standardizedFileURL.resolvingSymlinksInPath()\n        for path in sourceRoots where !path.isEmpty {\n            let source = URL(fileURLWithPath: path).standardizedFileURL.resolvingSymlinksInPath().path\n            guard root.path != source && !root.path.hasPrefix(source + \"/\") else { throw failure(\"归档目录不能放在源日志目录中\") }\n        }\n        let fm = FileManager.default\n        try fm.createDirectory(at: root, withIntermediateDirectories: true)\n        if !fm.fileExists(atPath: root.appendingPathComponent(\".git\").path) {\n            _ = try git(root, [\"init\"])\n        }\n        guard try git(root, [\"rev-parse\", \"--show-toplevel\"]) == root.path else { throw failure(\"请选择 Git 仓库的根目录\") }\n    }\n\n    public static func restore(from root: URL, into store: Store, bridge: RuntimeBridge) async throws -> Int {\n        let root = root.standardizedFileURL.resolvingSymlinksInPath(), fm = FileManager.default\n        guard fm.fileExists(atPath: root.appendingPathComponent(\".git\").path),\n              try git(root, [\"rev-parse\", \"--show-toplevel\"]) == root.path else { throw failure(\"归档仓库不存在或路径无效，请重新选择 Git 仓库\") }\n        let lease = try ServiceLease(root: root, name: \".ragdoll-archive-lock\")\n        defer { withExtendedLifetime(lease) {} }\n        let manifestURL = root.appendingPathComponent(\".ragdoll-manifest.json\")\n        guard manifestURL.resolvingSymlinksInPath().path == root.path + \"/.ragdoll-manifest.json\" else { throw failure(\"归档清单路径无效\") }\n        guard fm.fileExists(atPath: manifestURL.path) else {\n            guard !fm.fileExists(atPath: root.appendingPathComponent(\"sessions\").path) else { throw failure(\"归档缺少清单，已停止读取和写入\") }\n            return 0\n        }\n        let manifest = try JSONDecoder().decode([String: String].self, from: Data(contentsOf: manifestURL))\n        for path in manifest.keys {\n            guard path.hasPrefix(\"sessions/\"), !path.split(separator: \"/\").contains(where: { $0 == \"..\" || $0 == \".\" }),\n                  root.appendingPathComponent(path).resolvingSymlinksInPath().path.hasPrefix(root.path + \"/sessions/\") else { throw failure(\"归档清单路径越界：\\(path)\") }\n        }\n        func read(_ path: String) throws -> Data {\n            let data = try Data(contentsOf: root.appendingPathComponent(path))\n            guard manifest[path] == hash(data) else { throw failure(\"归档文件已变化，已停止读取和写入：\\(path)\") }\n            return data\n        }\n        let entries = manifest.keys.sorted(), paths = entries.filter { $0.hasSuffix(\"/metadata.json\") }\n        for path in paths {\n            var session = try JSONDecoder().decode(Session.self, from: read(path))\n            let base = String(path.dropLast(\"metadata.json\".count)), events = base + \"events.json\"\n            if manifest[events] != nil {\n                let snapshot = try JSONDecoder().decode(Session.self, from: read(events))\n                guard snapshot.id == session.id, snapshot.source == session.source else { throw failure(\"归档会话身份不一致：\\(path)\") }\n                session = snapshot\n            } else if [\"codex\", \"claude\", \"dsh\"].contains(session.source),\n                      let raw = entries.first(where: { $0.hasPrefix(base + \"raw/\") && $0.range(of: \"\\\\.jsonl(\\\\.(zstd|zst))?(\\\\.gz)?$\", options: .regularExpression) != nil }) {\n                _ = try read(raw)\n                let result = try await bridge.request(\"archive.read\", [\"source\": .string(session.source), \"path\": .string(root.appendingPathComponent(raw).path), \"home\": .string(session.home)], timeout: 600)\n                session.messages = try result[\"messages\"].decode([Message].self)\n                session.warnings += try result[\"warnings\"].decode([String].self)\n            } else {\n                let transcript = try read(base + \"transcript.md\")\n                session.messages = [Message(id: \"archive-transcript\", role: \"assistant\", text: String(decoding: transcript, as: UTF8.self), time: session.updated, kind: \"archive\")]\n                session.warnings.append(\"旧版归档以完整 Markdown 展示，原始消息结构不可恢复\")\n            }\n            _ = try store.save(session)\n        }\n        return paths.count\n    }\n\n    public static func save(_ sessions: [Session], to root: URL, sourceRoots: [String] = []) throws -> ArchiveResult {\n        let root = root.standardizedFileURL.resolvingSymlinksInPath(), fm = FileManager.default\n        try prepare(root, sourceRoots: sourceRoots)\n        let lease = try ServiceLease(root: root, name: \".ragdoll-archive-lock\")\n        defer { withExtendedLifetime(lease) {} }\n        let manifestURL = root.appendingPathComponent(\".ragdoll-manifest.json\")\n        guard manifestURL.resolvingSymlinksInPath().path.hasPrefix(root.path + \"/\") else { throw failure(\"归档清单不能指向仓库外部\") }\n        let old = fm.fileExists(atPath: manifestURL.path) ? try JSONDecoder().decode([String: String].self, from: Data(contentsOf: manifestURL)) : [:]\n        let encoder = JSONEncoder(); encoder.outputFormatting = [.prettyPrinted, .sortedKeys, .withoutEscapingSlashes]\n        let inlineImages = try NSRegularExpression(pattern: \"data:image/([a-z0-9.+-]+);base64,([^\\\\s\\\"'<>\\\\)\\\\]\\\\}`]*)\", options: .caseInsensitive)\n        var desired: [String: Data] = [:]\n        var replaced: [String] = []\n        for session in sessions {\n            let base = \"sessions/\\(safeName(session.source))/\\(safeName(session.id))\"\n            var metadata = session; metadata.messages = []\n            desired[base + \"/metadata.json\"] = try encoder.encode(metadata)\n            var portable = session\n            portable.messages = session.messages.map { message in\n                var message = message\n                message.text = extractImages(message.text, matching: inlineImages, base: base, files: &desired)\n                return message\n            }\n            var transcript = \"# \\(session.title)\\n\\n来源：\\(session.source)\\n\\n项目：\\(session.project)\\n\\n\" + portable.messages.map { \"## \\($0.role) · \\(ISO8601DateFormatter().string(from: Date(timeIntervalSince1970: $0.time / 1000)))\\n\\n\\($0.text)\\n\" }.joined(separator: \"\\n\")\n            for (index, path) in session.files.enumerated() {\n                let file = URL(fileURLWithPath: path)\n                guard fm.fileExists(atPath: file.path) else { continue }\n                let values = try file.resourceValues(forKeys: [.isRegularFileKey])\n                guard values.isRegularFile == true else { throw failure(\"无法归档非普通文件：\\(path)\") }\n                let raw = \"raw/\\(index)-\\(safeName(file.lastPathComponent))\", data = try Data(contentsOf: file)\n                let compressed = data.count > 50 * 1024 * 1024 || old[base + \"/\" + raw + \".gz\"] != nil\n                let saved = raw + (compressed ? \".gz\" : \"\")\n                desired[base + \"/\" + saved] = compressed ? try gzip(data, root: root) : data\n                if compressed && old[base + \"/\" + raw] != nil { replaced.append(base + \"/\" + raw) }\n                transcript = transcript.replacingOccurrences(of: file.absoluteString, with: saved)\n            }\n            desired[base + \"/transcript.md\"] = Data(transcript.utf8)\n            desired[base + \"/events.json\"] = try encoder.encode(portable)\n        }\n        for (path, data) in desired where data.count > 100 * 1024 * 1024 { throw failure(\"归档文件超过 100 MiB，已保留本地数据：\\(path)\") }\n        for path in Array(desired.keys) + replaced {\n            let destination = root.appendingPathComponent(path)\n            guard !destination.resolvingSymlinksInPath().path.hasPrefix(root.path + \"/.git/\") && destination.resolvingSymlinksInPath().path.hasPrefix(root.path + \"/\") else { throw failure(\"归档路径越界\") }\n            if fm.fileExists(atPath: destination.path) {\n                let digest = hash(try Data(contentsOf: destination))\n                guard old[path] == digest else { throw failure(\"归档文件已被手动修改或不属于应用：\\(path)。请保留修改后选择其他归档目录，或恢复文件后重试。\") }\n            } else if old[path] != nil { throw failure(\"归档文件已被手动删除：\\(path)。请处理该删除后重试。\") }\n        }\n        let managed = Array(desired.keys) + replaced + [\".ragdoll-manifest.json\"]\n        let managedSet = Set(managed)\n        let staged = try gitData(root, [\"diff\", \"--cached\", \"--name-only\", \"-z\"]).split(separator: 0).map { String(decoding: $0, as: UTF8.self) }\n        for path in staged where managedSet.contains(path) {\n            let data = try gitData(root, [\"show\", \":\\(path)\"])\n            let expected = path == \".ragdoll-manifest.json\" ? (fm.fileExists(atPath: manifestURL.path) ? hash(try Data(contentsOf: manifestURL)) : nil) : old[path]\n            guard expected == hash(data) else { throw failure(\"归档文件存在外部暂存修改，已保留：\\(path)。请先处理该暂存修改后重试。\") }\n        }\n        var manifest = old\n        var changed: [String] = []\n        for (path, data) in desired {\n            let digest = hash(data), destination = root.appendingPathComponent(path)\n            if old[path] == digest && fm.fileExists(atPath: destination.path) { continue }\n            try fm.createDirectory(at: destination.deletingLastPathComponent(), withIntermediateDirectories: true)\n            try data.write(to: destination, options: .atomic)\n            manifest[path] = digest; changed.append(path)\n        }\n        for path in replaced {\n            try fm.removeItem(at: root.appendingPathComponent(path))\n            manifest.removeValue(forKey: path); changed.append(path)\n        }\n        let manifestData = try encoder.encode(manifest)\n        let previousManifest = fm.fileExists(atPath: manifestURL.path) ? try Data(contentsOf: manifestURL) : nil\n        if previousManifest != manifestData {\n            try manifestData.write(to: manifestURL, options: .atomic); changed.append(\".ragdoll-manifest.json\")\n        }\n        let gitDirectory = try git(root, [\"rev-parse\", \"--absolute-git-dir\"])\n        let pathspec = URL(fileURLWithPath: gitDirectory).appendingPathComponent(\"ragdoll-pathspec-\\(UUID().uuidString)\")\n"}

## tool · 2026-11-17T13:16:12Z


Script completed
Wall time 5.3 seconds
Output:

SQLite Backup API (https://sqlite.org/backup.html)
citeturn0view0 [wordlim: 200] Crawled: today; Content type: text/html; Source: open({"ref_id":"https://sqlite.org/backup.html","lineno":null}); Total lines: 229
L0: Small. Fast. Reliable.
L1: Choose any three.
L2: 
L3:   * 【0†Home】
L4:   * Menu
L5:   * 【1†About】
L6:   * 【2†Documentation】
L7:   * 【3†Download】
L8:   * 【4†License】
L9:   * 【5†Support】
L10:   * 【6†Purchase】
L11:   * Search
L12: 
L13:   * 【1†About】
L14:   * 【2†Documentation】
L15:   * 【3†Download】
L16:   * 【5†Support】
L17:   * 【6†Purchase】
L18: 
L19: [Select] [Input] [Input]
L20: 
L21: SQLite Backup API
L22: 
L23: Table Of Contents
L24: 
L25: 【7†1. Using the SQLite Online Backup API】
L26: 
L27: 【8†1.1. Other Backup Techniques】
L28: 
L29: 【9†2. Example 1: Loading and Saving In-Memory Databases】
L30: 
L31: 【10†2.1. Error handling】
L32: 【11†2.2. Possible Enhancements】
L33: 
L34: 【12†3. Example 2: Online Backup of a Running Database】
L35: 
L36: 【13†3.1. File and Database Connection Locking】
L37: 
L38: 【14†3.2. backup_remaining() and backup_pagecount()】
L39: # 1. Using the SQLite Online Backup API
L40: 
L41: Historically, backups (copies) of SQLite databases have been created using the following method:
L42: 
L43:   1. Establish a shared lock on the database file using the SQLite API (i.e. the shell tool).
L44:   2. Copy the database file using an external tool (for example the unix 'cp' utility or the DOS 'copy' command).
L45:   3. Relinquish the shared lock on the database file obtained in step 1.
L46: This procedure works well in many scenarios and is usually very fast. However, this technique has the following shortcomings:
L47: 
L48:   * Any database clients wishing to write to the database file while a backup is being created must wait until the shared lock is relinquished.
L49:   * It cannot be used to copy data to or from in-memory databases.
L50:   * If a power failure or operating system failure occurs while copying the database file the backup database may be corrupted following system recovery.
L51: The 【15†Online Backup API】 was created to address these concerns. The online backup API allows the contents of one database to be copied into another database file, replacing any original contents of the target database. The copy operation may be done incrementally, in which case the source database does not need to be locked for the duration of the copy, only for the brief periods of time when it is actually being read from.
L52: This allows other database users to continue without excessive delays while a backup of an online database is made.
L53: The effect of completing the backup call sequence is to make the destination a bit-wise identical copy of the source database as it was when the copying commenced. (The destination becomes a "snapshot.")
L54: 
L55: The online backup API is 【15†documented here】. The remainder of this page contains two C language examples illustrating common uses of the API and discussions thereof. Reading these examples is no substitute for reading the API documentation!
L56: ## 1.1. Other Backup Techniques
L57: 
L58: The Online Backup API is the original method for making backups of a live SQLite databases. Other more recent techniques for accomplishing the same thing include:
L59: 
L60:   * The 【16†VACUUM INTO】 command will make a vacuumed copy of a live SQLite database into a separate file.
L61: 
L62:   * The 【17†sqlite3_rsync】 program makes a copy of a live SQLite database to or from a remote system using an SSH connection.
L63: # 2. Example 1: Loading and Saving In-Memory Databases
L64: 
L65:     /*
L66:     ** This function is used to load the contents of a database file on disk
L67:     ** into the "main" database of open database connection pInMemory, or
L68:     ** to save the current contents of the database opened by pInMemory into
L69:     ** a database file on disk. pInMemory is probably an in-memory database,
L70:     ** but this function will also work fine if it is not.
L71:     **
L72:     ** Parameter zFilename points to a nul-terminated string containing the
L73:     ** name of the database file on disk to load from or save to. If parameter
L74:     ** isSave is non-zero, then the contents of the file zFilename are
L75:     ** overwritten with the contents of the database opened by pInMemory. If
L76:     ** parameter isSave is zero, then the contents of the database opened by
L77:     ** pInMemory are replaced by data loaded from the file zFilename.
L78:     **
L79:     ** If the operation is successful, SQLITE_OK is returned. Otherwise, if
L80:     ** an error occurs, an SQLite error code is returned.
L81:     */
L82:     int loadOrSaveDb(【18†sqlite3】 *pInMemory, const char *zFilename, int isSave){
L83:       int rc;                   /* Function return code */
L84:       【18†sqlite3】 *pFile;           /* Database connection opened on zFilename */
L85:       【19†sqlite3_backup】 *pBackup;  /* Backup object used to copy data */
L86:       【18†sqlite3】 *pTo;             /* Database to copy to (pFile or pInMemory) */
L87:       【18†sqlite3】 *pFrom;           /* Database to copy from (pFile or pInMemory) */
L88: 
L89:       /* Open the database file identified by zFilename. Exit early if this fails
L90:       ** for any reason. */
L91:       rc = 【20†sqlite3_open】(zFilename, &pFile);
L92:       if( rc==SQLITE_OK ){
L93: 
L94:         /* If this is a 'load' operation (isSave==0), then data is copied
L95:         ** from the database file just opened to database pInMemory.
L96:         ** Otherwise, if this is a 'save' operation (isSave==1), then data
L97:         ** is copied from pInMemory to pFile.  Set the variables pFrom and
L98:         ** pTo accordingly. */
L99:         pFrom = (isSave ? pInMemory : pFile);
L100:         pTo   = (isSave ? pFile     : pInMemory);
L101: 
L102:         /* Set up the backup procedure to copy from the "main" database of
L103:         ** connection pFile to the main database of connection pInMemory.
L104:         ** If something goes wrong, pBackup will be set to NULL and an error
L105:         ** code and message left in connection pTo.
L106:         **
L107:         ** If the backup object is successfully created, call backup_step()
L108:         ** to copy data from pFile to pInMemory. Then call backup_finish()
L109:         ** to release resources associated with the pBackup object.  If an
L110:         ** error occurred, then an error code and message will be left in
L111:         ** connection pTo. If no error occurred, then the error code belonging
L112:         ** to pTo is set to SQLITE_OK.
L113:         */
L114:         pBackup = 【15†sqlite3_backup_init】(pTo, "main", pFrom, "main");
L115:         if( pBackup ){
L116:           (void)【21†sqlite3_backup_step】(pBackup, -1);
L117:           (void)【22†sqlite3_backup_finish】(pBackup);
L118:         }
L119:         rc = 【23†sqlite3_errcode】(pTo);
L120:       }
L121: 
L122:       /* Close the database connection opened on database file zFilename
L123:       ** and return the result of this function. */
L124:       (void)【24†sqlite3_close】(pFile);
L125:       return rc;
L126:     }
L127: The C function above demonstrates one of the simplest, and most common, uses of the backup API: loading and saving the contents of an in-memory database to a file on disk. The backup API is used as follows in this example:
L128:   1. Function 【15†sqlite3_backup_init()】 is called to create an 【19†sqlite3_backup】 object to copy data between the two databases (either from a file and into the in-memory database, or vice-versa).
L129:   2. Function 【21†sqlite3_backup_step()】 is called with a parameter of `-1` to copy the entire source database to the destination.
L130:   3. Function 【22†sqlite3_backup_finish()】 is called to clean up resources allocated by 【15†sqlite3_backup_init()】.
L131: ## 2.1. Error handling
L132: If an error occurs in any of the three main backup API routines then the 【25†error code】 and 【23†message】 are attached to the destination 【18†database connection】. Additionally, if 【21†sqlite3_backup_step()】 encounters an error, then the 【25†error code】 is returned by both the 【21†sqlite3_backup_step()】 call itself, and by the subsequent call to 【22†sqlite3_backup_finish()】.
L133: So a call to 【22†sqlite3_backup_finish()】 does not overwrite an 【25†error code】 stored in the destination 【18†database connection】 by 【21†sqlite3_backup_step()】. This feature is used in the example code to reduce the amount of error handling required. The return values of the 【21†sqlite3_backup_step()】 and 【22†sqlite3_backup_finish()】 calls are ignored and the error code indicating the success or failure of the copy operation is collected from the destination 【18†database connection】 afterward.
L134: ## 2.2. Possible Enhancements
L135: 
L136: The implementation of this function could be enhanced in at least two ways:
L137: 
L138:   1. Failing to obtain the lock on database file zFilename (an 【26†SQLITE_BUSY】 error) could be handled, and
L139:   2. Cases where the page-sizes of database pInMemory and zFilename are different could be handled better.
L140: Since database zFilename is a file on disk, then it may be accessed externally by another process. This means that when the call to sqlite3_backup_step() attempts to read from or write data to it, it may fail to obtain the required file lock. If this happens, this implementation will fail, returning SQLITE_BUSY immediately.
L141: The solution would be to register a busy-handler callback or timeout with 【18†database connection】 pFile using 【27†sqlite3_busy_handler()】 or 【28†sqlite3_busy_timeout()】 as soon as it is opened. If it fails to obtain a required lock immediately, 【21†sqlite3_backup_step()】 uses any registered busy-handler callback or timeout in the same way as 【29†sqlite3_step()】 or 【30†sqlite3_exec()】 does.
L142: Usually, it does not matter if the page-sizes of the source database and the destination database are different before the contents of the destination are overwritten. The page-size of the destination database is simply changed as part of the backup operation. The exception is if the destination database happens to be an in-memory database. In this case, if the page sizes are not the same at the start of the backup operation, then the operation fails with an SQLITE_READONLY error.
L143: Unfortunately, this could occur when loading a database image from a file into an in-memory database using function loadOrSaveDb().
L144: However, if in-memory database pInMemory has just been opened (and is therefore completely empty) before being passed to function loadOrSaveDb(), then it is still possible to change its page size using an SQLite "PRAGMA page_size" command. Function loadOrSaveDb() could detect this case, and attempt to set the page-size of the in-memory database to the page-size of database zFilename before invoking the online backup API functions.
L145: # 3. Example 2: Online Backup of a Running Database
L146: 
L147:     /*
L148:     ** Perform an online backup of database pDb to the database file named
L149:     ** by zFilename. This function copies 5 database pages from pDb to
L150:     ** zFilename, then unlocks pDb and sleeps for 250 ms, then repeats the
L151:     ** process until the entire database is backed up.
L152:     **
L153:     ** The third argument passed to this function must be a pointer to a progress
L154:     ** function. After each set of 5 pages is backed up, the progress function
L155:     ** is invoked with two integer parameters: the number of pages left to
L156:     ** copy, and the total number of pages in the source file. This information
L157:     ** may be used, for example, to update a GUI progress bar.
L158:     **
L159:     ** While this function is running, another thread may use the database pDb, or
L160:     ** another process may access the underlying database file via a separate
L161:     ** connection.
L162:     **
L163:     ** If the backup process is successfully completed, SQLITE_OK is returned.
L164:     ** Otherwise, if an error occurs, an SQLite error code is returned.
L165:     */
L166:     int backupDb(
L167:       【18†sqlite3】 *pDb,               /* Database to back up */
L168:       const char *zFilename,      /* Name of file to back up to */
L169:       void(*xProgress)(int, int)  /* Progress function to invoke */
L170:     ){
L171:       int rc;                     /* Function return code */
L172:       【18†sqlite3】 *pFile;             /* Database connection opened on zFilename */
L173:       【19†sqlite3_backup】 *pBackup;    /* Backup handle used to copy data */
L174: 
L175:       /* Open the database file identified by zFilename. */
L176:       rc = 【20†sqlite3_open】(zFilename, &pFile);
L177:       if( rc==SQLITE_OK ){
L178: 
L179:         /* Open the 【19†sqlite3_backup】 object used to accomplish the transfer */
L180:         pBackup = 【15†sqlite3_backup_init】(pFile, "main", pDb, "main");
L181:         if( pBackup ){
L182: 
L183:           /* Each iteration of this loop copies 5 database pages from database
L184:           ** pDb to the backup database. If the return value of backup_step()
L185:           ** indicates that there are still further pages to copy, sleep for
L186:           ** 250 ms before repeating. */
L187:           do {
L188:             rc = 【21†sqlite3_backup_step】(pBackup, 5);
L189:             xProgress(
L190:                 【31†sqlite3_backup_remaining】(pBackup),
L191:                 【32†sqlite3_backup_pagecount】(pBackup)
L192:             );
L193:             if( rc==SQLITE_OK || rc==SQLITE_BUSY || rc==SQLITE_LOCKED ){
L194:               【33†sqlite3_sleep】(250);
L195:             }
L196:           } while( rc==SQLITE_OK || rc==SQLITE_BUSY || rc==SQLITE_LOCKED );
L197: 
L198:           /* Release resources allocated by backup_init(). */
L199:           (void)【22†sqlite3_backup_finish】(pBackup);
L200:         }
L201:         rc = 【23†sqlite3_errcode】(pFile);
L202:       }
L203: 
L204:       /* Close the database connection opened on database file zFilename
L205:       ** and return the result of this function. */
L206:       (void)【24†sqlite3_close】(pFile);
L207:       return rc;
L208:     }
L209: The function presented in the previous example copies the entire source database in one call to 【21†sqlite3_backup_step()】. This requires holding a read-lock on the source database file for the duration of the operation, preventing any other database user from writing to the database. It also holds the mutex associated with database pInMemory throughout the copy, preventing any other thread from using it.
L210: The C function in this section, designed to be called by a background thread or process for creating a backup of an online database, avoids these problems using the following approach:
L211:   1. Function 【15†sqlite3_backup_init()】 is called to create an 【19†sqlite3_backup】 object to copy data from database pDb to the backup database file identified by zFilename.
L212:   2. Function 【21†sqlite3_backup_step()】 is called with a parameter of 5 to copy 5 pages of database pDb to the backup database (file zFilename).

{"chunk_id":"74f2e8","wall_time_seconds":0.000011459,"exit_code":0,"original_token_count":568,"output":"Sources/RagdollCore/BackgroundService.swift:63:    private let root: URL\nSources/Ragdoll/AppModel.swift:49:    let root: URL\nSources/Ragdoll/AppModel.swift:282:            let roots = settings.locations.map(\\.path)\nSources/RagdollCore/Models.swift:110:public struct Settings: Codable, Sendable {\nSources/RagdollCore/Models.swift-111-    public var locations: [Location] = []\nSources/RagdollCore/Models.swift-112-    public var agents: [AgentConfig] = []\nSources/RagdollCore/Models.swift-113-    public var archivePath = \"\"\nSources/RagdollCore/Models.swift-114-    public var archiveRemote: ArchiveRemote?\nSources/RagdollCore/Models.swift-115-    public var backgroundEnabled: Bool?\nSources/RagdollCore/Models.swift-116-    public var excludedProjects: [String] = []\nSources/RagdollCore/Models.swift-117-    public var weeklyBudget: Double?\nSources/RagdollCore/Models.swift-118-    public var showWeeklyBudget: Bool?\nSources/RagdollCore/Models.swift-119-    public var prices: [String: Price] = [\nSources/RagdollCore/Models.swift-120-        \"gpt-6.1-sol\": Price(input: 2, output: 10, cacheRead: 0.1, cacheWrite: 2.5, reference: \"https://developers.openai.com/api/docs/pricing\"),\nSources/RagdollCore/Models.swift-121-        \"gpt-6.1-terra\": Price(input: 1, output: 5, cacheRead: 0.05, cacheWrite: 1.25, reference: \"https://developers.openai.com/api/docs/pricing\"),\nSources/RagdollCore/Models.swift-122-        \"gpt-6-astra\": Price(input: 10, output: 50, cacheRead: 1, cacheWrite: 12.5, reference: \"https://developers.openai.com/api/docs/pricing\"),\nSources/RagdollCore/Models.swift-123-        \"gpt-6-luna\": Price(input: 0.1, output: 0.5, cacheRead: 0.01, cacheWrite: 0.125, reference: \"https://developers.openai.com/api/docs/pricing\"),\nSources/RagdollCore/Models.swift-124-        \"claude-opus-5-5\": Price(input: 4, output: 20, cacheRead: 0.2, cacheWrite: 5, reference: \"https://platform.claude.com/docs/en/about-claude/pricing\"),\nSources/RagdollCore/Models.swift-125-        \"claude-sonnet-5-5\": Price(input: 2, output: 10, cacheRead: 0.1, cacheWrite: 2.5, reference: \"https://platform.claude.com/docs/en/about-claude/pricing\")\nSources/RagdollCore/Models.swift-126-    ]\nSources/RagdollCore/Models.swift-127-    public init() {}\nSources/RagdollCore/Models.swift-128-}\n"}

## assistant · 2026-11-17T13:16:20Z

可以，两种都能实现。当前项目的 SQLite 保存了**会话正文、搜索索引和应用设置**；Git 归档另存 JSON、Markdown 和原始日志。

- **去掉 SQLite**：直接读取归档文件，设置单独存 JSON。需要改写查询、排序，以及 GUI 与后台服务之间的并发写入和变更通知；数据量增大时，查询成本也会增加。
- **把 SQLite 放进 Git**：适合保存数据库备份快照。应通过 Backup API 或 `VACUUM INTO` 生成一致的快照，再提交，避免直接复制正在写入的数据库。[SQLite 官方说明](https://sqlite.org/backup.html) 数据库是二进制文件，难以审查差异和合并多台设备的修改。

**我建议保留本地 SQLite，Git 继续保存可恢复的会话文件。** 当前已经支持从归档恢复会话，但设置仍只在本地数据库中，尚未随归档保存。

本次仅检查代码，未修改文件或运行测试。数据库包含会话全文和本机路径，若提交，应放入专用私有归档仓库。

## tool · 2026-11-17T13:53:53Z

codex_apps_open_page
{"page_id":null}

## tool · 2026-11-17T13:53:53Z

codex_apps_selected_page_part_1_of_1
Companion Page snapshot part 1 of 1:
{"page_id":null,"document_view":null}

## user · 2026-11-17T13:53:53Z

直接读取归档文件会不会效率低下


## assistant · 2026-11-17T13:54:10Z

会，**如果每次搜索、排序和统计都重新扫描并解析全部归档文件，效率会明显下降**。影响主要取决于文件数量、会话大小和存储设备。

不同操作的成本差别很大：

| 操作 | 直接读取归档的成本 |
|---|---|
| 打开某个会话 | 按路径读取单个文件，通常可接受 |
| 显示最近会话 | 需要汇总各会话元数据 |
| 全文搜索 | 需要读取大量会话正文 |
| 用量统计 | 需要汇总记录，重复计算会增加开销 |

去掉 SQLite 后，可以启动时读取元数据并建立内存索引，让列表和统计保持流畅；但启动耗时、内存占用，以及后台更新后的索引维护仍然需要处理。全文搜索尤其容易成为瓶颈。

**对当前项目，保留 SQLite 作为本地查询索引更合适，Git 归档负责持久保存和恢复。**

尚未对实际归档做性能测量，无法给出具体耗时；上述判断依据当前文件结构和读取方式。

## user · 2026-11-17T13:54:43Z

**把 SQLite 放进 Git会不会超过100mb**


## assistant · 2026-11-17T13:54:48Z

我先只读检查当前 SQLite 文件的大小，再判断是否接近 100 MB。

## tool · 2026-11-17T13:54:55Z


Script completed
Wall time 5.2 seconds
Output:

{"chunk_id":"aea8ee","wall_time_seconds":0.000007708,"exit_code":0,"original_token_count":4106,"output":"Warning: truncated output (original token count: 4106)\nTotal output lines: 115\n\nSources/RagdollCore/BackgroundService.swift:11:    public init(root: URL, name: String = \"service-lock\") throws {\nSources/RagdollCore/BackgroundService.swift:40:    public static func isRunning(root: URL) throws -> Bool {\nSources/RagdollCore/BackgroundService.swift:41:        do { let lease = try ServiceLease(root: root); withExtendedLifetime(lease) {}; return false }\nSources/RagdollCore/BackgroundService.swift:44:    public static func ownerPID(root: URL) throws -> Int32? {\nSources/RagdollCore/BackgroundService.swift:47:    public static func request(root: URL) throws {\nSources/RagdollCore/BackgroundService.swift:51:    public static func requestPush(root: URL) throws {\nSources/RagdollCore/BackgroundService.swift:55:    public static func status(root: URL) throws -> ServiceStatus? {\nSources/RagdollCore/BackgroundService.swift:63:    private let root: URL\nSources/RagdollCore/BackgroundService.swift:74:    public init(root: URL) throws {\nSources/RagdollCore/BackgroundService.swift:75:        self.root = root\nSources/RagdollCore/BackgroundService.swift:96:        let lease = try ServiceLease(root: root)\nSources/RagdollCore/BackgroundService.swift:109:                    state.scan = \"请先在 Ragdoll 中设置 Git 仓库\"; try publish()\nSources/RagdollCore/BackgroundService.swift:113:                if let fatalFailure { throw NSError(domain: \"Ragdoll.Service\", code: 2, userInfo: [NSLocalizedDescriptionKey: fatalFailure]) }\nSources/RagdollCore/BackgroundService.swift:136:                    if let fatalFailure { throw NSError(domain: \"Ragdoll.Service\", code: 2, userInfo: [NSLocalizedDescriptionKey: fatalFailure]) }\nSources/RagdollCore/BackgroundService.swift:171:            _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: settings.archivePath), remote: remote.remote, branch: remote.branch) }.value\nSources/RagdollCore/BackgroundService.swift:11:    public init(root: URL, name: String = \"service-lock\") throws {\nSources/RagdollCore/BackgroundService.swift:40:    public static func isRunning(root: URL) throws -> Bool {\nSources/RagdollCore/BackgroundService.swift:41:        do { let lease = try ServiceLease(root: root); withExtendedLifetime(lease) {}; return false }\nSources/RagdollCore/BackgroundService.swift:44:    public static func ownerPID(root: URL) throws -> Int32? {\nSources/RagdollCore/BackgroundService.swift:47:    public static func request(root: URL) throws {\nSources/RagdollCore/BackgroundService.swift:51:    public static func requestPush(root: URL) throws {\nSources/RagdollCore/BackgroundService.swift:55:    public static func status(root: URL) throws -> ServiceStatus? {\nSources/RagdollCore/BackgroundService.swift:63:    private let root: URL\nSources/RagdollCore/BackgroundService.swift:74:    public init(root: URL) throws {\nSources/RagdollCore/BackgroundService.swift:75:        self.root = root\nSources/RagdollCore/BackgroundService.swift:96:        let lease = try ServiceLease(root: root)\nSources/RagdollCore/BackgroundService.swift:109:                    state.scan = \"请先在 Ragdoll 中设置 Git 仓库\"; try publish()\nSources/RagdollCore/BackgroundService.swift:113:                if let fatalFailure { throw NSError(domain: \"Ragdoll.Service\", code: 2, userInfo: [NSLocalizedDescriptionKey: fatalFailure]) }\nSources/RagdollCore/BackgroundService.swift:136:                    if let fatalFailure { throw NSError(domain: \"Ragdoll.Service\", code: 2, userInfo: [NSLocalizedDescriptionKey: fatalFailure]) }\nSources/RagdollCore/BackgroundService.swift:171:            _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: settings.archivePath), remote: remote.remote, branch: remote.branch) }.value\nSources/Ragdoll/RagdollApp.swift:3:import RagdollCore\nSources/Ragdoll/RagdollApp.swift:6:struct RagdollApp: App {\nSources/Ragdoll/AppModel.swift:3:import RagdollCore\nSources/Ragdoll/AppModel.swift:49:    let root: URL\nSources/Ragdoll/AppModel.swift:59:    init(root: URL? = nil) {\nSources/Ragdoll/AppModel.swift:60:        self.root = root ?? ProcessInfo.processInfo.environment[\"RAGDOLL_DATA_DIR\"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent(\"Library/Application Support/Ragdoll\")\nSources/Ragdoll/AppModel.swift:106:                        let background = try BackgroundService.isRunning(root: self.root)\nSources/Ragdoll/AppModel.swift:159:        do { if try BackgroundService.isRunning(root: root) { try BackgroundService.request(root: root); pollBackground(); return } }\nSources/Ragdoll/AppModel.swift:164:            let lease = try ServiceLease(root: root)\nSources/Ragdoll/AppModel.swift:210:        await startChat(agent: agent, cwd: selected.project.isEmpty ? FileManager.de…1706 tokens truncated…elected.project.isEmpty ? FileManager.default.homeDirectoryForCurrentUser.path : selected.project, resume: selected)\nSources/Ragdoll/AppModel.swift:235:        do { agentInfo[agent.id] = try await bridge.request(\"probe\", [\"agent\": try .encode(hydrated(agent)), \"cwd\": .string(FileManager.default.homeDirectoryForCurrentUser.path)]) }\nSources/Ragdoll/AppModel.swift:262:            let result = try await bridge.request(\"authenticate\", [\"agent\": try .encode(hydrated(agent)), \"methodID\": .string(methodID), \"cwd\": .string(FileManager.default.homeDirectoryForCurrentUser.path)], timeout: 600)\nSources/Ragdoll/AppModel.swift:301:        do { if !scanning && !archiving { if try BackgroundService.isRunning(root: root) { archiveTask?.cancel(); return } } }\nSources/Ragdoll/AppModel.swift:313:        do { if try BackgroundService.isRunning(root: root) { try BackgroundService.request(root: root); archiveStatus = \"已请求后台归档\"; return } }\nSources/Ragdoll/AppModel.swift:319:            let lease = try ServiceLease(root: root)\nSources/Ragdoll/AppModel.swift:331:                    _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: path), remote: remote.remote, branch: remote.branch) }.value\nSources/Ragdoll/AppModel.swift:352:            if try BackgroundService.isRunning(root: root) { try BackgroundService.requestPush(root: root); return }\nSources/Ragdoll/AppModel.swift:354:            let lease = try ServiceLease(root: root); defer { withExtendedLifetime(lease) {} }\nSources/Ragdoll/AppModel.swift:357:            _ = try await Task.detached(priority: .utility) { try ArchiveSync.push(root: URL(fileURLWithPath: path), remote: remote.remote, branch: remote.branch) }.value\nSources/Ragdoll/AppModel.swift:367:            let running = try BackgroundService.isRunning(root: root)\nSources/Ragdoll/AppModel.swift:368:            if running, let state = try BackgroundService.status(root: root), state.pid == (try BackgroundService.ownerPID(root: root)), kill(state.pid, 0) == 0, Date().timeIntervalSince(state.updated) < 120 {\nSources/Ragdoll/AppModel.swift:382:        guard Bundle.main.bundleURL.pathExtension == \"app\" else { error = \"后台服务需要运行打包后的 Ragdoll.app\"; return }\nSources/Ragdoll/AppModel.swift:399:            guard let home = config.env[key] ?? settings.locations.first(where: { $0.source == agent.kind })?.path else { throw NSError(domain: \"Ragdoll.Migration\", code: 1, userInfo: [NSLocalizedDescriptionKey: \"请先设置目标工具的历史目录\"]) }\nSources/RagdollService/ServiceMain.swift:2:import RagdollCore\nSources/RagdollService/ServiceMain.swift:8:        let root: URL\nSources/RagdollService/ServiceMain.swift:13:            root = URL(fileURLWithPath: arguments[index + 1])\nSources/RagdollService/ServiceMain.swift:15:            root = ProcessInfo.processInfo.environment[\"RAGDOLL_DATA_DIR\"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent(\"Library/Application Support/Ragdoll\")\nSources/RagdollService/ServiceMain.swift:19:            try await BackgroundWorker(root: root).run(once: arguments.contains(\"--once\"))\nSources/Ragdoll/RootView.swift:2:import RagdollCore\nSources/Ragdoll/RootView.swift:37:                    VStack(alignment: .leading, spacing: 2) { Text(\"Ragdoll\").font(.title3.bold()); Text(\"LOCAL CONVERSATIONS\").font(.system(size: 8, weight: .semibold, design: .monospaced)).foregroundStyle(.secondary).tracking(1) }\nSources/Ragdoll/ConversationView.swift:2:import RagdollCore\nSources/Ragdoll/ConversationView.swift:234:        }.padding(28).frame(width: 540).onAppear { agentID = model.settings.agents.first?.id ?? \"\"; cwd = model.project.isEmpty ? FileManager.default.homeDirectoryForCurrentUser.path : model.project }\nSources/Ragdoll/RagdollApp.swift:3:import RagdollCore\nSources/Ragdoll/RagdollApp.swift:6:struct RagdollApp: App {\nSources/Ragdoll/MigrationView.swift:2:import RagdollCore\nSources/Ragdoll/MigrationView.swift:39:        .onAppear { targetID = targets.first?.id ?? \"\"; cwd = session.project.isEmpty ? FileManager.default.homeDirectoryForCurrentUser.path : session.project }\nSources/Ragdoll/AgentOptionsView.swift:2:import RagdollCore\nSources/Ragdoll/SettingsView.swift:3:import RagdollCore\nSources/Ragdoll/SettingsView.swift:142:                                let preview = try await Task.detached { try ArchiveSync.preview(root: URL(fileURLWithPath: path), remote: draft.remote, branch: draft.branch) }.value\nSources/Ragdoll/SettingsView.swift:156:                    Text(\"当前用户登录期间持续扫描、归档和推送，退出 Ragdoll 后继续运行。后台不执行交互对话。\").font(.caption).foregroundStyle(.secondary)\nSources/Ragdoll/DashboardView.swift:2:import RagdollCore\n"}
About large files on GitHub - GitHub Docs (https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)
citeturn1search0 [wordlim: 200] Crawled: today; GitHub blocks files larger than 100 MiB.

To track files beyond this limit, you must use Git Large File Storage (Git LFS). ... If you need to distribute large files within your repository, you can create releases on GitHub.com instead of tracking the files.
--------------------------------------------------------------------------------
Adding a file to a repository - GitHub Docs (https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository?platform=linux)
citeturn1search1 [wordlim: 200] Crawled: 2 months ago; To add files larger than 100 MiB, you must use Git Large File Storage. ... With push protection, GitHub will block uploading a file to the repository if the file contains a supported secret, such as a token.
--------------------------------------------------------------------------------
About large files on GitHub - GitHub Enterprise Cloud Docs (https://docs.github.com/en/enterprise-cloud%40latest/repositories/working-with-files/managing-large-files/about-large-files-on-github)
citeturn1search2 [wordlim: 200] Crawled: 3 weeks ago; GitHub blocks files larger than 100 MiB.

To track files beyond this limit, you must use Git Large File Storage (Git LFS). ... If you need to distribute large files within your repository, you can create releases on GitHub.com instead of tracking the files.
--------------------------------------------------------------------------------
Repository limits - GitHub Docs (https://docs.github.com/en/repositories/creating-and-managing-repositories/repository-limits)
citeturn1search3 [wordlim: 200] Crawled: today; Certain types of repository resources can be quite large, requiring excessive processing on GitHub. ...     * Use Git Large File Storage (Git LFS) for binary files. ... This is enforced at 100 MB. ... These files are always available in their raw formats, which are served through `raw.githubusercontent.com`; for example, `https://raw.githubusercontent.com/octocat/Spoon-Knife/main/index.html`.
--------------------------------------------------------------------------------
Adding a file to a repository - GitHub Docs (https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository?ref=iwantaito)
citeturn1search4 [wordlim: 200] Crawled: 3 weeks ago; To add files larger than 100 MiB, you must use Git Large File Storage. ... With push protection, GitHub will block uploading a file to the repository if the file contains a supported secret, such as a token.
--------------------------------------------------------------------------------
About large files on GitHub - GitHub Enterprise Server 3.21 Docs (https://docs.github.com/en/enterprise-server%403.21/repositories/working-with-files/managing-large-files/about-large-files-on-github?platform=mac)
citeturn1search5 [wordlim: 200] Crawled: yesterday; By default, GitHub Enterprise Server blocks files larger than 100 MiB. However, a site administrator can configure a different limit for your GitHub Enterprise Server instance. ... To track files beyond this limit, you must use Git Large File Storage (Git LFS).
--------------------------------------------------------------------------------
Adding a file to a repository - GitHub Docs (https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository?platform=windows)
citeturn1search6 [wordlim: 200] Crawled: last month; To add files larger than 100 MiB, you must use Git Large File Storage. ... With push protection, GitHub will block uploading a file to the repository if the file contains a supported secret, such as a token.
--------------------------------------------------------------------------------
About large files on GitHub - GitHub Enterprise Server 3.20 Docs (https://docs.github.com/en/enterprise-server%403.20/repositories/working-with-files/managing-large-files/about-large-files-on-github)
citeturn1search7 [wordlim: 200] Crawled: last month; By default, GitHub Enterprise Server blocks files larger than 100 MiB. However, a site administrator can configure a different limit for your GitHub Enterprise Server instance. ... To track files beyond this limit, you must use Git Large File Storage (Git LFS).
--------------------------------------------------------------------------------
docs/content/repositories/working-with-files/managing-large-files/about-large-files-on-github.md at main · github/docs · GitHub (https://github.com/github/docs/blob/main/content/repositories/working-with-files/managing-large-files/about-large-files-on-github.md)
citeturn1search8 [wordlim: 200] Crawled: 5 days ago; If you add a file to a repository via a browser, the file can be no larger than {% data variables.large_files.max_github_browser_size %}. ... {% ifversion ghes %}By default, {% data variables.product.prodname_ghe_server %}{% else %}{% data variables.product.github %}{% endif %} blocks files larger than {% data variables.large_files.max_github_size %}. {% ifversion ghes %}However, a site administrator can configure a different limit for {% data variables.location.product_location %}.
--------------------------------------------------------------------------------
 (https://ccn.web.tr/web-api/iframe-proxy?url=https%3A%2F%2Fdocs.github.com%2Fapi%2Farticle%2Fbody%3Fpathname%3D%2Fen%2Frepositories%2Fworking-with-files%2Fmanaging-large-files%2Fabout-large-files-on-github)
citeturn1search9 [wordlim: 200] Crawled: 3 weeks ago; GitHub blocks files larger than 100 MiB. To track files beyond this limit, you must use Git Large File Storage (Git LFS). ... Push your commits to GitHub.com: ```shell $ git push # Push our rewritten, smaller commit ``` ### Removing a file that was added in an earlier commit If you added a file in an earlier commit, you need to remove it from the repository's history.
--------------------------------------------------------------------------------
About Git Large File Storage and GitHub Desktop - GitHub Docs (https://docs.github.com/en/desktop/configuring-and-customizing-github-desktop/about-git-large-file-storage-and-github-desktop?apiVersion=2022-11-28)
citeturn1search10 [wordlim: 200] Crawled: 2 months ago; Git LFS lets you push files to GitHub that exceed the normal limit of 100 MiB. ... After you configure Git LFS to track files in a repository, you can seamlessly access and manage large files with GitHub Desktop like any other file in the repository.
--------------------------------------------------------------------------------
docs/content/repositories/creating-and-managing-repositories/repository-limits.md at main · github/docs · GitHub (https://github.com/github/docs/blob/main/content/repositories/creating-and-managing-repositories/repository-limits.md)
citeturn1search11 [wordlim: 200] Crawled: 4 weeks ago; Certain types of repository resources can be quite large, requiring excessive processing on {% data variables.product.github %}. ... See AUTOTITLE.{% else %}This is enforced at 100 MB.{% endif %} To track large files in a Git repository, we recommend using {% data variables.large_files.product_name_short %}.
--------------------------------------------------------------------------------
2024_git (https://www.chpc.utah.edu/presentations/git.pdf)
citeturn1search12 [wordlim: 200] Terminology: Large File Storage (LFS) ... Note that hosts like GitHub will reject larger files (as of Fall 2024, GitHub “blocks files larger than 100 MB” and warns about files larger than 50 MB.)
--------------------------------------------------------------------------------
# How much data do you have? (https://assets.ctfassets.net/wfutmusr1t3h/LR7pDJPdNpZLyUxOUPxLr/ca8aefce081b64ee8e5ca7d63d69f55e/LT1920_Migrating_GitHubUniverseRecap.pdf)
citeturn1search13 [wordlim: 200] Crawled: 2 days ago; - **100MB per file:** Run `git-sizer --verbose` on each repo and take a look at `Biggest objects -> Blobs -> Maximum size`. ... https://github.com/github/git-sizer
--------------------------------------------------------------------------------
GitHub and Git (https://nmfs-opensci.github.io/GitHub-Guide/index.pdf)
citeturn1search14 [wordlim: 200] Published: 1.6 years ago; GitHub restricts pushing of files large than 100 MiB from the command line. There is GitHub Large File Storage for files up to 5 GB on GitHub Enterprise Cloud, but in practice, staff have found some difficulties with Large File Storage.
--------------------------------------------------------------------------------
WP2_Contribution_guidelines.docx (https://icaerus.eu/wp-content/uploads/2025/06/WP2_Contribution_guidelines_may2025.docx-1.pdf)
citeturn1search15 [wordlim: 200]    - Maximum file size: 100 MB. ...    - GitHub provides Git LFS for managing large files like datasets, videos, and high-resolution images.
--------------------------------------------------------------------------------
FDM_LoveDataWeek2023_Melchert (https://www.fdm.uni-hannover.de/fileadmin/fdm/Dokumente/Schulungsunterlagen/LoveDataWeek2023_RDM_Melchert.pdf)
citeturn1search16 [wordlim: 200] Published: 4 months ago; • it blocks pushes that exceed 100 MB ... https://docs.github.com/en/repositories/working-with-files/
managing-large-files/about-git-large-file-storage
--------------------------------------------------------------------------------
Larger files than 100MB should be removed from a repository or moved to Git LFS: (https://assets.ctfassets.net/wfutmusr1t3h/6XahpCF0Sslud4sQfjzTWU/47a03438b83d3f2544a62e1c38faae44/LT1920_Migrating_GitHubUniverseRecap.pdf)
citeturn1search17 [wordlim: 200] Published: 2.9 years ago; Larger files than 100MB should be removed from a repository or moved to Git LFS:

• Removing larger file: ... https://github.com/git-lfs/git-lfs/wiki/Tutorial#migrating-existing-repository-data-to-lfs
--------------------------------------------------------------------------------
Unable to migrate GitLab Community Edition repo with LFS into GitHub Enterprise (https://www.reddit.com/r/git/comments/1ef4slq)
citeturn1reddit18 [wordlim: 200] Published: 2.3 years ago; Crawled: 1.8 years ago;     remote: error: File path/to/large/file/larg-file.blend is 120.55 MB; this exceeds GitHub's file size limit of 100.00 MB ... You may want to try Git Large File Storage - https://git-lfs.github.com.
--------------------------------------------------------------------------------
Using LFS, file tracked, but push rejected with status that I should use LFS to track (https://www.reddit.com/r/github/comments/um0l0g)
citeturn1reddit19 [wordlim: 200] Published: 4.5 years ago; Crawled: 4.5 years ago;     Writing objects: 100% (17/17), 142.89 MiB | 907.00 KiB/s, done. ...     remote: error: File zines/AR_online_i6.3.pdf is 128.83 MB; this exceeds GitHub's file size limit of 100.00 MB ... You may want to try Git Large File Storage - https://git-lfs.github.com.
--------------------------------------------------------------------------------
How to remove a file from git? (https://www.reddit.com/r/git/comments/1srp452/how_to_remove_a_file_from_git/)
citeturn1reddit20 [wordlim: 200] Published: 6 months ago; `Writing objects: 100% (43/43), 1.16 MiB | 1.52 MiB/s, done. ... `remote: error: File backup.tar is 133.26 MB; this exceeds GitHub's file size limit of 100.00 MB` ... You may want to try Git Large File Storage - https://git-lfs.github.com.
--------------------------------------------------------------------------------
Oh god... (https://www.reddit.com/r/git/comments/1ktdgkp)
citeturn1reddit21 [wordlim: 200] Published: 1.5 years ago; Crawled: 1.5 years ago; Writing objects:  74% (32/43), 22.07 MiB | 7Writing objects:  74% (32/43), 52.51 MiB | 1Writing objects:  74% (32/43), 87.90 MiB | 1Writing objects:  74WritinWriting objects: 100% (43/43), 1.28 GiB | 14.87 MiB/s, done..42 MiB/s ... You may want to try Git Large File Storage - https://git-lfs.github.com. ... Then do a `git reset --hard` also make sure to read the docs for git stash and git reset to know what you are doing.
--------------------------------------------------------------------------------
Accident had two decently sized mp4s in my project and now I cant get rid of the error nor upload code to github for this project (https://www.reddit.com/r/github/comments/186eh7w)
citeturn1reddit22 [wordlim: 200] Published: 3.0 years ago; Crawled: 3.0 years ago;     Writing objects: 100% (70/70), 352.64 MiB | 7.44 MiB/s, done. ... You may want to try Git Large File Storage - https://git-lfs.github.com.
--------------------------------------------------------------------------------
Is it bad or frowned upon to use git to store my research notes? (https://www.reddit.com/r/github/comments/1ehu3tn)
citeturn1reddit23 [wordlim: 200] Published: 2.3 years ago; Crawled: 1.8 years ago; Be aware that file size is limited to 100MiB with a warning if a file reaches 50MiB. ... Here is the reference to the size limit information: https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github ... I would stay away from storing large binary files or binary files that change regularly - so skip that mpeg video or word document you are modifying every day.
--------------------------------------------------------------------------------
pushing mistake. how to fix? (https://www.reddit.com/r/git/comments/108dfxr)
citeturn1reddit24 [wordlim: 200] Published: 3.9 years ago; Crawled: 3.9 years ago;       remote: error: File Mysql\_backup.sql is 144.64 MB; this exceeds GitHub's file size limit of 100.00 MB ... You may want to try Git Large File Storage - URL. ...           > $ git pushCounting objects: 7255, done.Delta compression using up to 8 threads.Compressing objects: 100% (6101/6101), done.Writing objects: 100% (7255/7255), 28.47 MiB | 3.01 MiB/s, done.Total 7255 (delta 1826), reused 40 (delta 0)remote: Resolving deltas: 100% (1826/1826), completed with 826 local objects.To github.com:richb201/RST.git49fdd920..165a1add  master-new -> master-new
--------------------------------------------------------------------------------
Why can't I push updates to my github Repo? (https://www.reddit.com/r/git/comments/1gkc7ox)
citeturn1reddit25 [wordlim: 200] Published: 2.0 years ago; Crawled: 2.0 years ago;     Writing objects: 100% (44276/44276), 701.84 MiB | 124.79 MiB/s, done. ...     remote: error: File .venv/Lib/site-packages/tensorflow/python/_pywrap_tensorflow_internal.pyd is 943.41 MB; this exceeds GitHub's file size limit of 100.00 MB ... You may want to try Git Large File Storage - https://git-lfs.github.com.
--------------------------------------------------------------------------------
File size limit warning ⚠️ (https://www.reddit.com/r/github/comments/13gi4y6)
citeturn1reddit26 [wordlim: 200] Published: 3.5 years ago; Crawled: 3.5 years ago; GitHub has single file size limit as 25 mb from browser & 50 mb from command line.

Recently for my project i have uploaded a big file (around 100 mb) through git command line (pushed). ... Git was designed for small text files, not large binary files.
--------------------------------------------------------------------------------
Error while using LFS GIT to commit and push larger files than normal Github File limit (https://www.reddit.com/r/github/comments/pbqo08)
citeturn1reddit27 [wordlim: 200] Published: 5.2 years ago; Crawled: 5.2 years ago;     Writing objects: 100% (16/16), 154.31 MiB | 28.36 MiB/s, done. ... You may want to try Git Large File Storage - https://git-lfs.github.com.


## tool · 2026-11-17T13:55:01Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"87fe7e","wall_time_seconds":0.00001,"exit_code":0,"original_token_count":154,"output":"/Users/oyamahappa/Library/Application Support/Ragdoll/index.sqlite: 1786507264 bytes\nSources/Ragdoll/AppModel.swift:60:        self.root = root ?? ProcessInfo.processInfo.environment[\"RAGDOLL_DATA_DIR\"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent(\"Library/Application Support/Ragdoll\")\nSources/RagdollService/ServiceMain.swift:15:            root = ProcessInfo.processInfo.environment[\"RAGDOLL_DATA_DIR\"].map { URL(fileURLWithPath: $0) } ?? FileManager.default.homeDirectoryForCurrentUser.appendingPathComponent(\"Library/Application Support/Ragdoll\")\n"}

## assistant · 2026-11-17T13:55:10Z

**会，你当前的 SQLite 文件已经超过了。** 我刚检查了默认数据目录中的 `index.sqlite`：

- 实际大小：**1,786,507,264 字节，约 1.79 GB**
- 约为 GitHub **100 MiB 单文件限制的 17 倍**，普通 Git 推送会被拒绝。[GitHub 官方限制](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github)

因此，当前更适合保留本地 SQLite，Git 按会话保存归档文件。直接提交整个数据库还会持续增加仓库历史的存储成本。

本次仅检查文件大小，未分析数据库内部占用；其中可能包含可回收空间，但尚不能判断压缩后能减少多少。

## user · 2026-11-17T13:55:33Z

这是单个文件吗还是可以分块的


## assistant · 2026-11-17T13:55:48Z

**刚才的 1.79 GB 是单个 `index.sqlite` 文件的大小。** SQLite 运行时还可能产生独立的日志文件。

可以分块，但有两种不同含义：

| 方式 | 能否实现 | 使用限制 |
|---|---|---|
| 把数据库备份切成多个小文件 | 可以，每块控制在 100 MiB 以下 | 恢复时必须完整拼回数据库，SQLite 无法直接读取这些碎块 |
| 按项目或月份保存多个 SQLite 数据库 | 可以，需要修改应用 | 每个数据库独立可读，但全文搜索、统计和跨库一致性需要额外处理，单库仍可能继续增长 |

**如果只是为了放进 Git，分块备份能绕过单文件限制，但整个数据库的体积和版本历史增长问题仍然存在。** 当前按会话保存 JSON、Markdown 的归档方式，也已经把数据拆成独立文件了。

当前应用未实现 SQLite 分块备份；本次仅说明可行性，未修改或验证分块恢复。
