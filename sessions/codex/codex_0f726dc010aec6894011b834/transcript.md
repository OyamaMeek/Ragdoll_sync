# 制作三张高数模拟卷

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-12T13:04:13Z

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



## developer · 2026-11-12T13:04:13Z

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
- `r22` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1111.10930/skills`
- `r23` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.3/skills`
- `r24` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r25` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.13.0/skills`
- `r26` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.2/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI- (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, settings, (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped instruc (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list (file: r2/skill-installer/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:database-access: Explore and query databases on the user's servers (Postgres, M (file: r15/database-access/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:deploy-check: Verify a server after a deployment, update or restart — servic (file: r15/deploy-check/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:incident-triage: Work through a server alert or outage step by step — disk full,  (file: r15/incident-triage/SKILL.md)
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
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r21/documents/26.1111.10930/skills/documents/SKILL.md)
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
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r21/pdf/26.1111.10930/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r17/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves  (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what br (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r23/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across fiv (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r21/presentations/26.1111.10930/skills/presentations/SKILL.md)
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
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full r (file: r25/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal  (file: r25/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose pr (file: r25/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new (file: r25/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching,  (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (inclu (file: r18/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use (file: r18/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, vis (file: r22/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through t (file: r22/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r19/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r26/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r19/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human part (file: r26/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r19/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r26/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r19/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r26/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r19/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you  (file: r26/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing su (file: r19/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing su (file: r26/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r19/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or be (file: r26/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks  (file: r19/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks  (file: r26/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r19/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected be (file: r26/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing imp (file: r19/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing imp (file: r26/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from curren (file: r19/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from curren (file: r26/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find an (file: r19/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find an (file: r26/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r19/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing,  (file: r26/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, (file: r19/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, (file: r26/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r19/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or ver (file: r26/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build fe (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz your (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r21/template-creator/26.1111.10930/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Codin (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conve (file: r17/visualize/1.0.89/skills/visualize/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an anima (file: r20/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in Cha (file: r20/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in C (file: r20/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing ski (file: r0/writing-for-agents/SKILL.md)
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
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/12/01a1cfdb-c864-76b1-a3e1-808cf1c7e0f1`, `/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-11-12T13:04:13Z

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

## developer · 2026-11-12T13:04:13Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-12T13:04:13Z

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
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/12/01a1cfdb-c864-76b1-a3e1-808cf1c7e0f1</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-12T13:04:13Z

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

## developer · 2026-11-12T13:04:13Z

<codex_apps_client_time_context><timezone>Asia/Taipei</timezone>
<current_date>2026-11-12</current_date>
Use this client time context for user-facing dates, times, and schedules instead of the execution host's timezone and current date.</codex_apps_client_time_context>

## user · 2026-11-12T13:04:14Z

使用references/302模拟27md里面的试题 参考工科数学分析基础第三版 上册（含大纲）到中值微分定理为考试范围 出3张模拟卷 题目选用稍微有难度的但不要超纲 格式使用latex语法分数要写成分子在分数线上面的 lim的内容要写到lim下面 排版采用适配iPad的4:3 一面一道题 下面留空 下一页写这道题的解析 解析和题目不要出现在同一页解析要以一名耐心、严谨的理科教师提供

- 使用清楚、自然的中文，面向基础薄弱的学习者；必要术语首次出现时解释含义，不使用贬低学习者的措辞。
- 先说明已知什么、要求什么，再说明准备使用的规律、适用条件和解题方向。
- 每个关键步骤交代“为什么可以这样做”，展示必要的推导、代入、计算和单位，不跳过影响理解的中间关系。
- 优先寻找可以减少计算的分析方法，如对称性、守恒关系、比例、整体分析、图像、特殊值和极限检验；仅在适用时使用。
- 默认给出一个清楚、可靠的完整解法。其他解法确有价值时，再解释它们的适用条件与优势，不为凑数量重复计算。
- 多问问题分别作答，说明各问之间的关系；结论带上必要的单位、方向、取值范围、限制条件及近似精度。
- 完成后检查代回原条件是否成立，以及符号、量纲、数量级、边界情况和增根问题；按题目类型选择相关检查。
- 区分题目事实、推导结论与额外假设。涉及需要外部核实的事实或数据时，查阅可靠来源并附链接，不编造出处。


## assistant · 2026-11-12T13:04:18Z

我会先读取题库、教材和大纲，核定考试范围，再选编三张模拟卷。每题单独一页，下一页给出完整解析，按 iPad 4:3 横向页面排版。


## tool · 2026-11-12T13:04:21Z


Script completed
Wall time 0.2 seconds
Output:

[{"name":"mcp__codex_app__load_workspace_dependencies","description":"Locate the configured bundled workspace dependency runtime paths for this local desktop thread, including Node.js, Python, and useful libraries for working with spreadsheets, slide decks, Word documents, and PDFs. This is read-only and takes no arguments. This tool is part of plugin `codex-app-tools`.\n\nManage the Codex desktop app: find, create, and update chats; organize projects, sidebar, and pinned items; schedule automations; manage worktrees; open app panels; and locate bundled libraries for documents, spreadsheets, slides, and PDFs.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_app__load_workspace_dependencies(args: {}): Promise<CallToolResult>; };\n```"}]
{"chunk_id":"f8b072","wall_time_seconds":0.000009292,"exit_code":0,"original_token_count":137,"output":"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank\nAGENTS.md\n.gitignore\ndocs/CHANGELOG.md\noutput/iPad/302数学二分节真题集.pdf\noutput/iPad/27302阶段模拟卷.pdf\noutput/302数学二分节真题集（原生LaTeX常规版）.tex\noutput/pdf/27302阶段模拟卷（iPad横屏版）.pdf\noutput/302数学二分节真题集（原生LaTeX横屏版）.tex\noutput/302数学二分节真题集（原生LaTeX横屏版）.pdf\noutput/302数学二分节真题集.tex\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\n"}
{"chunk_id":"105632","wall_time_seconds":0.000011792,"exit_code":0,"original_token_count":2827,"output":"---\nname: \"pdf\"\ndescription: \"Read, create, inspect, render, and verify PDF files where visual layout matters, including fillable AcroForms. Use Poppler rendering plus Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction.\"\n---\n\n# PDF Skill\n\n## When To Use\n\n- Read or review PDF content where layout and visuals matter.\n- Create PDFs programmatically with reliable formatting.\n- Fill and validate interactive PDF forms.\n- Validate final rendering before delivery.\n\n## Tools + Contract Requirements\n\nImmediately before the first create/edit authoring command, run `mark_artifact_operation_started.mjs` successfully exactly once using the command below. Do not run it for read-only work. For edits, replace `create` with `edit`; adjust the expected count and output format to match the requested outputs.\n\n\n\n```bash\nnode container_tools/mark_artifact_operation_started.mjs --operation-kind create --expected-output-count 1 --output-format pdf\n```\n\n## Workflow\n\n1. Prefer visual review: render PDF pages to PNGs and inspect them.\n   - Use `pdftoppm` from the bundled runtime or system Poppler when available.\n   - If unavailable, install Poppler or ask the user to review the output locally.\n2. Use `reportlab` to generate PDFs when creating new documents.\n3. Use `pdfplumber` or `pypdf` for text extraction and quick checks; do not rely on text extraction for layout fidelity.\n4. After each meaningful update, re-render pages and verify alignment, spacing, and legibility.\n\n## Fill And Validate AcroForms\n\nVisual review alone is not a correctness check for a fillable PDF. A page `/Widget` annotation can render a value from its appearance stream while the canonical `/AcroForm/Fields` tree is missing or contains a stale value.\n\n1. Keep the result interactive by default; set `flatten=True` only when the user explicitly requests a completed, static form. Preserve the source PDF, and do not flatten a signed PDF without an explicit workflow decision.\n2. Inspect both representations before filling: enumerate fields from `reader.get_fields()` and `/Widget` annotations from every page's `/Annots`, following `/Parent` and `/Kids`. If a widget and a canonical field have the same name but are distinct objects with no `/Parent` relationship, do not call `reattach_fields()` blindly: it can create a second top-level field with the same name. Report the ambiguity or produce a static result.\n3. Recover genuinely orphaned widgets, fill all pages, and write the result with `pypdf`:\n\n```python\nfrom pypdf import PdfReader, PdfWriter\nfrom pypdf.generic import NameObject\n\nreader = PdfReader(input_pdf)\nwriter = PdfWriter()\nwriter.clone_document_from_reader(reader)\n\n# Restores widgets that are missing from /AcroForm/Fields.\nwriter.reattach_fields()\nfields = writer.get_fields() or {}\nmissing = set(expected_values) - set(fields)\nif missing:\n    raise ValueError(f\"Form fields not found after repair: {sorted(missing)}\")\n\nvalues_to_write = dict(expected_values)\nif flatten:\n    # Paint every existing value before removing every widget.\n    values_to_write = {\n        name: field.get(\"/V\", \"/Off\" if field.get(\"/FT\") == \"/Btn\" else \"\")\n        for name, field in fields.items()\n    }\n    values_to_write.update(expected_values)\n\nwriter.update_page_form_field_values(\n    None, values_to_write, auto_regenerate=False, flatten=flatten\n)\n\nif flatten:\n    # pypdf's flatten=True paints appearances but does not remove widgets.\n    writer.remove_annotations(subtypes=\"/Widget\")\n    writer.root_object.pop(NameObject(\"/AcroForm\"), None)\n\nwith open(output_pdf, \"wb\") as stream:\n    writer.write(stream)\n```\n\n4. Reopen the written PDF before delivery. For an interactive result, require every expected field to be present in `get_fields()` with the expected `/V`, enumerate page widgets again, and confirm their effective `/V` (the widget value or inherited `/Parent` value) agrees. Confirm each updated widget has a non-empty `/AP` `/N` appearance and render the final pages to catch stale or clipped appearances. Do not rely on `/NeedAppearances` or a successful PNG render as proof that logical field data was updated.\n5. For a flattened result, require zero `/Widget` annotations and no remaining `/AcroForm` field tree after reopening, then render the final pages. Keep an editable copy when the user may need to revise the form.\n\n## Temp And Output Conventions\n\n- Use `tmp/pdfs/` for intermediate files; delete them when done.\n- Write final artifacts under `output/pdf/` when working in this repo.\n- Keep filenames stable and descriptive.\n\n## Dependencies\n\nPrefer the Codex bundled workspace/runtime dependencies when available. The primary runtime is expected to include:\n\n- Python packages: `reportlab`, `pdfplumber`, `pypdf`\n- Rendering tools: `pdftoppm` and `pdfinfo` from Poppler\n\nIf a dependency is missing, install only what is needed.\n\nPython packages:\n\n```bash\nuv pip install reportlab pdfplumber pypdf\n```\n\nIf `uv` is unavailable:\n\n```bash\npython3 -m pip install reportlab pdfplumber pypdf\n```\n\nSystem tools for rendering:\n\n```bash\n# macOS (Homebrew)\nbrew install poppler\n\n# Ubuntu/Debian\nsudo apt-get install -y poppler-utils\n```\n\nIf installation is not possible in this environment, tell the user which dependency is missing and how to install it locally.\n\n## Environment\n\nNo required environment variables.\n\n## Rendering Command\n\n```bash\npdftoppm -png \"$INPUT_PDF\" \"$OUTPUT_PREFIX\"\n```\n\n## Quality Expectations\n\n- Maintain polished visual design: consistent typography, spacing, margins, and section hierarchy.\n- Avoid rendering issues: clipped text, overlapping elements, broken tables, black squares, or unreadable glyphs.\n- Charts, tables, and images must be sharp, aligned, and clearly labeled.\n- Use ASCII hyphens only. Avoid U+2011 and other Unicode dashes.\n- Citations and references must be human-readable; never leave tool tokens or placeholder strings.\n\n## Final Checks\n\n- Do not deliver until the latest PNG inspection shows zero visual or formatting defects.\n- Confirm headers, footers, page numbering, and section transitions look polished.\n- Keep intermediate files organized or remove them after final approval.\n\n## Final response\n\n### Final Response Citations\n\n- **Create/edit:** for created or edited PDFs, cite each final deliverable exactly once with `purpose=\"output\"`, in its own paragraph. Briefly describe the result without repeating its filename, path, or link. Never put output directives inside prose or list items.\n- **Q&A and summaries:** Every file whose contents you summarize or use to support an answer MUST receive a `:codex-file-citation{...}` with `purpose=\"source\"` in the final response. Use the source citation in place of the filename, wherever the filename would appear. Do not write the filename separately and append its citation at the end. Files merely inspected but not used in the answer need no citation. Do not emit output citations for unchanged files or read-only answers.\n\n- Emit `:codex-file-citation{...}` directly, without backticks, code fences, or a Markdown-link wrapper. Use verified targets only. No need to cite or reference intermediate work.\n\nFor file citations, set `path` to the verified absolute file path on the task host. Omit `mode`.\n\nSome illustrative examples, real responses use verified targets outside code fences.\n\n```text\n:codex-file-citation{path=\"/absolute/path/review.pdf\" purpose=\"output\"}\n```\n\n```text\nThe review of :codex-file-citation{path=\"/absolute/path/review.pdf\" purpose=\"source\"} is due Friday.\n```\n\n\n### Additional Citation Guidance\n\nFor PDF Q&A, inspect complete relevant pages and preserve material headings, table/figure labels, footnotes, sources, and sample sizes. PDF citations support only plain file citations; do not add `artifact_kind`, `page_number`, or other locators.\n---\nname: ponytail\ndescription: >\n  Lazy senior dev mode: the smallest change that fully solves the task, and a\n  reply a busy human understands in one read. Use on any coding task (writing,\n  fixing, refactoring, reviewing, choosing dependencies) and when the user says\n  \"ponytail\", \"be lazy\", \"simplest solution\", \"yagni\", or complains about\n  over-engineering or bloat. Levels: lite, full (default), ultra.\nargument-hint: \"[lite|full|ultra|off]\"\nlicense: MIT\n---\n\n# Ponytail\n\nYou are a lazy senior developer. The best code is the code never written. You solve the whole problem with the least new code. End your reply with one or two lines: what you skipped or did not check, and any risk the user must know.\n\nActive for the whole session until the user says \"stop ponytail\" or \"normal mode\". Switch level: `/ponytail lite|full|ultra`.\n\n## Before you write\n\nRead the task and the code it touches. List every place your change must reach: callers, tests, fixtures, config, exports. Check what your change could break for users: data it would destroy or expose, callers that stop working. That is scope. Extra features are not.\n\n## The smallest complete change\n\nTake the first option that fully works:\n\n1. Does it need to exist? Skip features, options and flexibility nobody asked for, and name them in one line. A vague request (\"build me X\") gets the smallest version that does the core job.\n2. Already in this codebase (a helper, component, service, pattern)? Use it the way the surrounding code does.\n3. Standard library or a platform feature? Use it, unless the project has its own. A house component beats a native widget.\n4. An installed dependency? Use it. Never add a dependency for a few lines.\n5. Can it be one line a reader gets at a glance? One line.\n6. Otherwise: the minimum code that works.\n\n- Be lazy about the solution, never about the change itself: finish every part the task needs, including the callers, tests and fixtures your change breaks.\n- No abstraction, wrapper, type conversion, option, config, boilerplate or \"for later\" code nobody asked for. Keep values in the form the platform already gives you. Deletion beats addition. Keep the structure the codebase already has: its layers, interfaces and conventions.\n- The shortest working diff wins, once you know everything it must touch. A one-liner that needs decoding is not short.\n- Comment only the why the code cannot show, in one line.\n- Bug fix: before you edit, grep every caller of the function you touch, then fix the root cause once in the shared code.\n- Code you move or merge keeps its error handling and validation.\n- Between options of equal size, take the one that is correct on edge cases.\n- Lazy code without its check is unfinished: new non-trivial logic (a branch, a loop, a parser, money or security, or a whole new script or app) leaves one small test or an assert-based self-check. Trivial changes need none.\n- A shortcut with a known limit gets a code comment in this form: `shortcut: <the limit>, <when to upgrade>`.\n\nNever cut: validation at trust boundaries, error handling that prevents data loss, security, accessibility, the calibration real hardware needs, anything the user asked for.\n\n## Levels\n\n| Level | Behavior |\n|-------|----------|\n| **lite** | Build what was asked. Name the smaller option in one line and let the user pick. |\n| **full** | The rules above. Default. |\n| **ultra** | Also question the request: before building, push back on any part the need does not justify. |\n"}

## developer · 2026-11-12T13:04:21Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__ot
- mcp__pubmed
</tools>

## tool · 2026-11-12T13:04:27Z


Script completed
Wall time 0.2 seconds
Output:

{"i":0,"result":{"status":"fulfilled","value":{"chunk_id":"ef0bd6","wall_time_seconds":0.000009958,"exit_code":0,"original_token_count":271,"output":" D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D output/302-question-facsimiles.pdf\n?? \"output/iPad/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n* main 87e8b36 [origin/main] docs: record math question bank delivery commit\n.github/scripts/release_tex.py\n.github/scripts/test_release_tex.py\n.github/scripts/test_question_bank.py\n.github/workflows/release-tex.yml\n.gitignore\nREADME.md\ndocs/CHANGELOG.md\nmemory/agents.md\nmemory/plan.md\nmemory/verify.md\nmemory/progress.md\nmemory/gotchas.md\n"}}}
{"i":1,"result":{"status":"fulfilled","value":{"chunk_id":"58b3e7","wall_time_seconds":0.000009,"exit_code":0,"original_token_count":10209,"output":"Warning: truncated output (original token count: 10209)\nTotal output lines: 424\n\n# 工具\n\n本次分节真题详细解析按章节使用并行代理技能分区校订，主代理统一评级规则、题头、检查和编译。使用已有 Tectonic、PyMuPDF 与 Python 标准库；不进行截图或图像检查。\n\n使用 PyMuPDF 提取 PDF 文字层，使用 macOS Vision 在本机识别扫描页。源 PDF 保留在原目录。\n\n本次张宇往年八套由单一代理逐题检查，使用 PyMuPDF 原页图和文字层、嵌入图示哈希及现有 KaTeX 脚本验证，未调用其他代理。\n\n数学模拟卷补用本机 MLX PaddleOCR 生成候选，再逐题对照源 PDF 修正；候选不能作为完成证据。使用 KaTeX 验证 Markdown 公式渲染。往年合集按独立文件分工校对，选填交付文件统一由一名代理组装。\n\n阶段模拟卷使用 LaTeX 和 ctex 排版，使用桌面应用附带的 Tectonic 编译，使用 PyMuPDF 检查 PDF 题序和文本边界。\n\n自动发布使用 GitHub Actions、Tectonic 0.17.0、Python 标准库和 GitHub CLI，PDF 作为 GitHub Release 附件分发。\n# PDF 批量提取\n\n## 当前任务：分节真题难度与详细解析\n\n原位更新 234 题共用的原生 LaTeX 源稿和横屏 PDF（含现有 iPad 交付路径）；A4 入口同步编译验证。不改原卷题号、题面和节归属。每题增加 1–5 个文字 `*`，依据知识要求、推理层数、计算量和易错点评级，各节按难度稳定升序。解析依次交代已知与目标、方法及条件、完整推导、结论与检查，首次用到的必要术语作通俗解释。统一算式中的上下分式，检查紧缩分式与指数中的除法。\n\n按第一章、第二章、第三章、第四章分区校订；各区仅修改所属题目。汇总后核对题目集合、解析对应、难度顺序、公式结构，编译两种版式并检查日志、PDF 文本与内容边界。不进行未授权的截图或图像检查。完成后提交并普通推送当前 origin/main。\n\n递归处理源目录的 PDF，在 `27302模拟` 中按相同相对路径生成 Markdown。保留各排版版本和答案文件，内容相同的 PDF 复用识别结果。每页链接至对应源 PDF 页码。\n\n## 09–26 年真题与解析\n\n递归将 `考研数学一二三09-26年真题&解析` 下的 PDF 转到 `302真题`，维持一份 PDF 对应一份 Markdown。直接提取正常文字层，对扫描页和文字层明显损坏的页面，用 PyMuPDF 渲染后交给本机 Vision 识别。\n\n## 27302 阶段模拟卷\n\n以教材目录和正文限定范围，从第一章至第二章第四节末，含极值必要条件、微分中值定理和洛必达法则。筛选 `27302模拟` 中的六套卷、880 题和基础 500 题，优先核对可辨认的原题和配套解析。采用本地 2026 年考研数学一试卷的 10 道单选、6 道填空、6 道解答及对应分值，在 `output` 交付可编辑的 LaTeX 和由其编译的 PDF。原题位置写入 LaTeX 注释。\n\n## 扩充阶段模拟卷\n\n按已有的教材范围筛选更多题目。以原题版本为单位，合并同题的横版、A4 版及解析，排除第一卷已经使用的题目。能用范围内方法独立完成的题或小问编成多份 150 分试卷，余题列为补充练习；每题保留出处。\n\n## 302 数学二分节真题集\n\n以 `302真题` 所对应的 2009–2026 年数学二逐年原卷为准，按教材上册大纲的四章、19 节建立目录。逐题记录年份、题号、页码、主考点及归属，跨节题按主要方法收录一次。上册未覆盖的数学二题目按主题列入附录。LaTeX 引用逐题裁片，保留原卷题干、公式、选项和图形。交付写入 `output`，不安装或调用 TeX 编译器。\n\n## 302 数学二旧版 iPad 横屏版\n\n原卷截图排版的旧版 iPad 横屏 PDF 和 `.tex` 从本地交付目录及远端 `main` 移除。保留原生 LaTeX 版本，以及仍供分节源稿使用的裁片资源。旧版可从 Git 历史恢复。\n\n## 302 数学二原生 LaTeX 题面\n\n按原卷题号读取逐年原卷文字层、已有 OCR 和配套解析。将题干、选择项、公式、矩阵和小问逐题写成 LaTeX，图题写成 TikZ 矢量路径。以同一份题库源稿生成 4:3 横屏题集和 A4 常规分节版，保留上册 19 节的定理页和原卷题号。原卷页码仅留在 LaTeX 源稿。行内和独立公式中的极限条件均排在 `lim` 正下方。按原书节序输出。不安装 TeX 编译器。\n\n横屏版和 A4 常规版将年份、题号与知识点排在同一行，用小号灰字显示。交付覆盖现有文件，历史版本由 Git 保留。\n\n按《工科数学分析基础》第三版上册目录收录四章 19 节对应的 234 道题。每份解析写出入手角度、推导步骤和答案，解答题覆盖全部小问。两版共用同一份题库源稿，每道题结束后翻页进入本题解析，解析结束后再翻页进入下一题。原位更新横屏 PDF，使用已有 A4 入口编译验证。\n\n## 27302 阶段模拟卷 iPad 版\n\n从现有两份 LaTeX 源稿提取五套模拟卷和补充练习。保留各卷原题号、分值、选项、公式和小问。使用 800 × 600 点横向页面，每页上方排一道题，下方留白。用 PDF 书签定位各卷和补充练习。\n\n为 186 道题分别写入手角度、完整推导和答案。保留现有题面页，在每道题后插入对应解析页，再进入下一道题。原位更新 iPad PDF 并调整原有卷级书签。\n\n## LaTeX 分数与数学记号\n\n逐份检查 `output` 的 LaTeX 源稿。将算式中的斜杠分数改为上下分式，包括题干、选项、公式、解析、幂指数和上下限。统一定理摘要的数学模式、微分符号和极限下标，沿用教材中涉及人名的英文术语。A4 原生版继续读取同一源稿，原卷裁片继续以图像呈现。\n\n## 302模拟27 Markdown 转换\n\n在 `references/302模拟27` 中筛选李林、张宇、合工大、超越、武忠祥、李艳芳的题面，在 `references/302模拟27md` 中按原层级生成 UTF-8 Markdown。合集按书签或目录选择卷次，题目与解析合订的文件按实际分界提取试题页。提取可读文字层，对扫描页和内嵌图片使用本机 Vision OCR。Markdown 只呈现标题、题干、选项、小问和图中题目文字，保留题号与卷次、题型标题。\n\n逐题校对以源 PDF 的题号和版面为准。先用李林六套卷第一卷建立逐题对照样本，核对数学符号、矩阵、选项和小问。再对照同卷版本及合集中的同题，确认内容一致后复用校对结果。图文识别候选与原卷有差异时记录具体卷次和题号。\n\n交付仅保留数一、数二。移除独立的数三 Markdown。混合卷按源 PDF 的题源标注或题内科目标记筛选，保留共享题的数一、数二题面和原题号。\n\n张宇往年八套选填按两科各八卷、每卷 16 题对照原 PDF 第 71–94 页校对，核对紧凑与留白来源的差异，原位更新四份交付文件中的对应分组。检查每卷题号、40 个选项及 KaTeX 渲染，其他作者分组保持原文。\n\n## LaTeX PDF 自动发布\n\n在 `main` 的 push 工作流中按推送前后提交计算变更，重建新增或修改的 `output/` TeX 入口及受资源变更影响的入口。用 Tectonic 0.17.0 编译，全部成功后上传到草稿，附件齐全后发布。发布串行执行，按已有 Release 和标签分配 `v0.0.1` 至 `v0.0.999`，用运行 ID 识别重跑。说明优先读取提交里的 `Release-Note:` 中文摘要，否则使用受影响的文档名。\n# 进度\n\n## 当前任务：分节真题难度与详细解析\n\n- [x] 核实共用源稿有 234 题、19 节，两种版式共用题库；Git 初始存在裁片 PDF 删除及未跟踪 iPad 目录。\n- [x] 234 题逐题补充四部分解析、难度与上下分式；中断时未完成移动的 2023 年第 5 题、2019 年第 13 题已按原题恢复并扩写。\n- [x] 完成全部节内稳定排序，同星保留原序，题头用计数器连续编号。星级 1–5 依次为 6、110、88、29、1 题。\n- [x] 与任务开始前 HEAD 对照 234 份题面，题干、选项、图形内容均保持原文；第四章独立复核完成，48 项计算检查通过。\n- [x] 五项回归检查通过；横屏 488 页、A4 471 页编译成功，日志无缺字、警告或溢出。逐题检查题头、解析、星级、下一页开始、23 个书签及页面边界，并用字形和分数线坐标检查上下分式。已覆盖现有横屏及 iPad PDF，未做截图或实机验证。\n- [x] 题集及验证记录已提交为 `a8e4665` 并普通推送至 `origin/main`。任务开始前的裁片 PDF 删除及另一份未跟踪 iPad 模拟卷均保持原状态；提交哈希补记另作后续文档提交。\n\n- 已用《李林880数二高数篇做题本》和《考研数学冲刺预测6套卷》验证文字层提取及本地 OCR。\n- 已生成 63 份 Markdown。用两种 PDF 渲染方式完成 OCR，补提取了题目汇总和平板版讲义中的图片正文。\n- 已核对全部 16,915 个页段及原页链接。11,250 页使用文字层，5,661 页使用 OCR，4 页标记为无可提取文字。\n- Git 仓库位于项目根目录，沿用 `origin` 的 `main`；元数据由原 `remote-checkout/.git` 迁入。\n\n## 09–26 年真题与解析\n\n- 已将 151 份 PDF 转成 Markdown 保存到 `302真题`。扫描页及文字层有乱码的页面使用本机 OCR。\n- 已核对 7,404 个页段的编号、正文和原页链接。7,398 页使用 OCR，6 页使用文字层，每页均有提取文字。97 份 PDF 的 677 个页段标有读取警告。\n- 文件名为《2026考研数学（一）答案解析》的原 PDF 首页写的是“2025 年考研数学一”，Markdown 保留原文件名和页内年份。\n\n## 27302 阶段模拟卷\n\n- [x] 核定教材边界、可用题源和题型分值。\n- [x] 转录 22 道题并复算客观题、检查解答题能否在指定范围内完成。\n- [x] 编译 LaTeX 并检查四页 A4 PDF 的题序、分值和文本。源文件和 PDF 已放入 `output`。\n\n## 扩充阶段模拟卷\n\n- [x] 交叉核对 880 题、基础 500 题、辅导讲义和六套卷，按原题和小问去重。\n- [x] 新增第二至第五卷，每卷 22 道，另有 76 道补充练习。逐题标记题源。\n- [x] 编译并检查各卷题型、分值、分页和文字边界。扩充版 LaTeX 和 22 页 A4 PDF 已放入 `output`，其中第 17–22 页为补充练习。\n\n## 302 数学二分节真题集\n\n- [x] 核定 18 份数学二原卷与上册 19 节。\n- [x] 定位 408 道题的题号和裁片边界，按主要考点分节。\n- [x] 生成 `output/302数学二分节真题集.tex` 和 `output/302-question-facsimiles.pdf`。正文 236 题，附录 172 题，共 410 个裁片。\n\n## 302 数学二 iPad 横屏版\n\n- [x] 确认现有真题集的题序、节名与题面资源。\n- [x] 核对 19 节的 85 条编号定理，连同常用性质和公式整理为 113 条。\n- [x] 生成 432 页横屏 PDF 和 LaTeX，完成题页、写字区、目录链接和资源引用检查。\n- [x] 删除旧版 iPad 横屏 PDF 和 `.tex`，核对远端分支内容。\n\n## 302 数学二原生 LaTeX 题面\n\n- [x] 完成 2009–2026 年 408 道题的原生 LaTeX 转录及题号复核，题面图形写成 10 幅 TikZ 矢量图。\n- [x] 按上册 19 节收录 234 题，附录收录 174 题。修正两道二重积分换序题的分组。\n- [x] 编译并验证 432 页 iPad 横屏 PDF。验证 A4 常规入口共用同一份题库，编译得到 89 页。\n- [x] 在共用 LaTeX 源稿中调整 `lim` 的条件位置，并从两种版式的题头去掉原卷 PDF 页码。\n- [x] 重新编译横屏版和 A4 版，核对极限公式、题头和横屏版分页。\n- [x] 统一横屏版和 A4 常规版的题头，编译并核对 408 道题的题头样式，再覆盖现有文件。\n- [x] 按题号分组完成 408 道解析，核对选择题答案表及若干题目的条件和推导。\n- [x] 将解析并入现有 LaTeX，编译横屏版和 A4 版，核对全部题目与解析的分页和对应关系。\n- [x] 按上册目录保留 234 道题及解析，移除超出上册范围的四个分组并更新目录和总题数。\n- [x] 编译两版，核对 19 节及逐题分页后原位更新 PDF。\n\n## 27302 阶段模拟卷 iPad 版\n\n- [x] 找到两份源稿，确认包含五套模拟卷和补充练习。\n- [x] 提取并编译 186 道题的横屏 PDF。\n- [x] 核对逐题内容、页序、留白和书签。\n- [x] 撰写并逐组核对 186 份解析。\n- [x] 编译解析并与题页交错合并，核对全书对应关系。\n\n## LaTeX 分数与数学记号\n\n- [x] 盘点五份源稿，确认共用入口、原卷裁片和可编辑公式的范围。\n- [x] 转换斜杠分数，逐式检查分子、分母及括号分组，按教材统一数学记号和英文术语。\n- [x] 编译并检查题号、分页及残余斜杠，记录验证结果。\n\n## 302模拟27 Markdown 转换\n\n- [x] 确认输出目录，…3709 tokens truncated…编辑算式无斜杠分数。核对两种原生版的 234 道题、逐题解析和内部跳转，通过 PDF 字形坐标确认 2012 年第 10 题解析中的分数上下排列。裁片版编译使用 Git 副本中的原卷资源，编译器提示 PDF 版本和重复页锚点。未做截图检查。\n\n## 302模拟27 Markdown 转换\n\n用真实扫描页、混合文字和图片的页面检查文本。逐个核对范围内的源相对路径、UTF-8 输出、PDF 页码及源链接。通过合集目录核对所选卷次和页码，通过题解合订本的分界核对题面范围。\n\n验证脚本通过。60 份 Markdown 共 4,950 个原页链接，包含 4,366 段文字层和 865 段 OCR 文本，无失败页或空白页。抽查两份李林题解合订本从第一套题面开始，结束于第四套题面。26 年 40 套紧凑版第 34 页保留李林第 20 至 22 题，止于下一套卷标题之前。\n\n整理后检查全部 60 份 Markdown 的标题和题面格式。核对六份 10 套合集的 10 个卷标题、两份 40 套合集的 22 个入选卷标题，以及两份 A3 试卷的卷序。用李林六套卷同版文字层核对截图中的第 14、15 题公式。其他 OCR 公式及个别缺漏的题干未逐题校对。\n\n逐题校对检查题号、题干、公式、四个选项、解答题小问和必要图示。相同题面的多个排版须有题目对应证据；批量校验的页数或题数与逐题核对结果分别记录。\n\n李林卷一原版第 13 题的积分上限为 `1+sin(t)`，做题本原文为 `1+sin(v)`，分别保留；原版第 22 题使用 `diag`，做题本使用对角矩阵。卷二第 7 题以原版试卷四个可辨认的积分选项修复做题本中的重复选项。\n\n李林第四卷第 1、6、10 题与第五卷第 1、7、14 题在原版和横版之间有题面差异，按各自原文保留。张宇考点分类的每份源 PDF 有 176 道数一、176 道数二、176 道数三，按题源标注保留前两科。武忠祥合卷按题内科目标记保留数一、数二，数一第 10 题原卷最后一个向量缺下标，依据选项和基向量顺序补为 α₁。\n\n逐题核对李林六套卷五个版本、李艳芳三套卷四个版本、武忠祥六份测试和张宇数一、数二两份紧凑版。用 KaTeX 验证校对后的数学公式可渲染。张宇同题选项按各科顺序整理。李艳芳第二卷第 4 题按配套资料明确问变化率的大小，第 5、6 题按配套资料重印题面校正分母。\n\n张宇的 17 份数一、数二 Markdown 通过 KaTeX 的 24,792 个数学表达式检查。对照八个卷次的原版扫描、留白版与横版，考点分类用题源标注和原题号关联题面。数一原版第六卷第 14 题的三重积分和做题本不同，分别保留。第四卷第 2 题的两个重复选项按同科勘误题面修复。数二第六卷第 14 题采用紧凑版明确的半径范围。\n\n往年 10 套、20 套数一的四份输出通过 6,552 个 KaTeX 表达式检查；对应数二四份通过 5,804 个表达式检查。10 套每份 220 题，20 套每份 242 题。20 套数一 A3 李林四套第三卷第 22 题原印两次 Y=1，A4 第一项为 Y=-1，分别保留。40 套两份输出各 483 题、22 卷，通过合计 5,840 个表达式检查。李林六套第一卷原文件缺第 22 题，不补造题目。\n\n内部原页核对图片必须保留所有有墨迹的行。旧版按每行四个黑像素筛选会误删小分子；已修复为保留任一黑像素的行，并直接用原页复核相关分式。数二 10 套和 20 套的旧裁片共 101 处丢墨片段已复查，修复李林四套第二卷第 11 题幂指数分子 1。\n\n往年选填超越数一第六至第十卷对照原 PDF 第 56–70 页校对，修复概率表、求和下标、积分上下限和伴随矩阵星号。写回两版，检查每卷 16 题及 40 个选项；547 个表达式通过 KaTeX 渲染。\n\n## LaTeX PDF 自动发布\n\n八项回归测试通过，覆盖 Git 推送范围、共用源稿、裁片资源、仅文档变更、中文摘要、版本递增、上限和重跑时的草稿选择。Tectonic 0.17.0 在本机成功编译五份 PDF，页数为 4、22、471、63、488。裁片版仍提示输入 PDF 版本较高和重复页锚点。Linux 安装包通过 SHA-256 校验。`actionlint` 1.7.12 过滤已知的 `concurrency.queue` 兼容性误报后通过，`queue: max` 另按 GitHub 文档和工作流 Schema 核对。\n\nGitHub Actions 运行 `42850865346` 通过，检出了 `829d693` 并完成推送差异检查。无 TeX 变更时编译和发布步骤均跳过，Releases 仍为空。远端附件上传和公开发布尚待首个包含 TeX 变更的推送验证。\n# 注意事项\n\n面向基础薄弱学习者的解析须逐题交代已知与目标、方法条件、关键推导原因和结果检查，不能只列公式及答案。难度采用文字 `*`，各节从易到难。检查分数时同时覆盖斜杠、紧缩分式、幂指数和积分上下限，确保上下分式清楚可读。\n\nPDF 文字层及通用 OCR 可能丢失公式结构。通过原页链接保留核对入口。\n\n用户要求题面以原生 LaTeX 转录时，题干、选项、公式和必要图形需要可编辑。PDF 裁片仅用于内部核对。\n\n真题集的行内极限也将趋近条件排在 `lim` 正下方。题头显示原卷年份和题号，原卷页码只留作 LaTeX 源稿中的定位信息。\n\n涉及人名的数学术语沿用《工科数学分析基础》第三版上册的英文拼写，例如 Taylor、Cauchy、Lagrange、L'Hospital。目录、知识点、题干和解析采用同一写法。\n\n修改已有交付文件时直接覆盖，每个任务只保留当前交付，历史版本由 Git 保留。\n\n题面转换遇到题解合订本时，核对源文件中试题和解析的分页分界。处理混合合集时按书签或目录筛选卷次。\n\n用户要求只保留标题和题目时，题面 Markdown 直接写标题、题干、选项和小问。页码、链接、提取方式和水印无需进入正文，OCR 文字以普通段落呈现。\n\n用户排除一个数学科目时，同时检查混合分类本和合卷。分类本优先用源文件中每题的来源标注，保留题号和其他科目的共用题面。\n\n同名、同卷次在不同科目、年份和排版中可能有公式或选项差异，复用校对文本前逐题比较实际来源。极小分子、幂指数及根号次数需要直接检查原页，内部去留白不得删除任何有墨迹的行。\n\n判断仓库状态时同时检查已知的检出目录和远端配置，不能仅凭工作目录的一次 `git status` 报错断言没有仓库。当前仓库已迁至项目根目录，Git 操作在根目录执行。\n\n`references/` 仅保存在本地，整个目录不纳入 Git。不得强制添加其中的 PDF、Markdown 或其他资料；取消跟踪时保留本地文件。\n/.question-bank-work/\n/.release-work/\n/remote-checkout/\n.DS_Store\n__pycache__/\n*.pyc\n*.log\n.env\n.env.*\n/references/\n- **实际实现的功能与改动**：\n  - 对照两科紧凑版第 71–94 页，逐题校对 256 题，原位更新紧凑及留白两种版式的题面。\n  - 修正分段函数漏项、积分限、单侧极限、向量与矩阵分量、导数阶数及概率选项上划线，补全图题文字描述，保留各科原选项顺序及来源写法。\n  - 两科留白版第 140–187 页与紧凑版的正文文字层一致，嵌入图示数据哈希一致。四份 Markdown 各有 128 道张宇八套题及 320 个选项，逐卷与校对稿一致，其他作者分组哈希未变；1463 个独立数学表达式通过 KaTeX 检查，无警告。\n  - 未独立复算全部答案，未继续其他作者的校对。\n- **涉及文件**：\n  - `references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf.md`\n  - `references/302模拟27md/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf.md`\n  - `references/302模拟27md/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf.md`\n  - `references/302模拟27md/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf.md`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n- **Git 提交**：`937f7e5c052370e37fede71c2825f7bf7a663416 chore: manage project at repository root and save proofread exams`，已推送至 `origin/main`。\n\n---\n\n## [2026-11-11 22:08] 精简 302模拟27 题面 Markdown\n\n- **需求/问题描述**：\n  > 题面 Markdown 只保留标题和题目。\n\n- **实际实现的功能与改动**：\n  - 原位整理 60 份题面。保留卷次、题型、题号、题干、选项和小问，去掉页码、原页链接、OCR 标签、代码框、封面目录、考试说明和水印。移除单独的转换报告。\n  - 用同版文字层核对李林六套卷截图中第 14、15 题的公式。两份 A3 试卷分半页 OCR，按原题序合并。检查 60 份文件格式及合集卷数。\n\n- **涉及文件**：\n  - `references/302模拟27md/`（原位更新 60 份题面 Markdown）\n  - `memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n\n- **Git 提交**：当前工作目录没有 Git 仓库，未提交。\n\n---\n\n## [2026-11-12 14:51] 在项目根目录管理 Git 仓库\n\n- **需求/问题描述**：\n  > 将当前目录设置为 Git 仓库，按既有规则提交并自动推送校对结果。\n- **实际实现的功能与改动**：\n  - 将 remote-checkout/.git 迁至项目根目录，保留历史、origin 和 main，移入既有 README 和 GitHub Actions。迁移前工作区干净，HEAD 与远端均为 64700e1。\n  - 合并两处开发及验证记录，记录正确仓库位置，加入缓存、原始 PDF、环境文件与日志的忽略规则。\n  - 将四份包含张宇八套校对结果的选填 Markdown、项目规则与相关记录纳入提交。其他既有资料及缺失的裁片 PDF 不纳入本次提交。\n  - 复查题面结构和 1463 个数学表达式；发布脚本与工作流保持原内容。\n- **涉及文件**：\n  - `.gitignore`、`AGENTS.md`、`docs/CHANGELOG.md`、`memory/` 的五份记录。\n  - `references/302模拟27md/往年模拟卷选填精选/` 的数一、数二紧凑及留白四份 Markdown。\n- **Git 提交**：`937f7e5c052370e37fede71c2825f7bf7a663416 chore: manage project at repository root and save proofread exams`，已通过远端引用核对推送成功；本条哈希补记由后续文档提交保存。\n\n---\n\n## [2026-11-12 14:54] 停止跟踪 references 目录\n\n- **需求/问题描述**：\n  > references 不纳入 Git。\n- **实际实现的功能与改动**：\n  - 将整个 `/references/` 加入 `.gitignore`，取消四份已跟踪 Markdown 的索引记录，保留本地资料。\n  - 对比取消跟踪前后的文件 SHA-256，检查忽略规则和索引中没有 references 文件。\n- **涉及文件**：\n  - `.gitignore`、`memory/gotchas.md`、`memory/progress.md`、`docs/CHANGELOG.md`。\n  - `references/302模拟27md/往年模拟卷选填精选/` 中四份 Markdown（取消跟踪）。\n- **Git 提交**：`2f3cdb1fc6bfee1600df49d5f96d5601c93435d8 chore: keep references local and untracked`，已推送并核对远端 main；哈希补记由后续文档提交保存。\n\n---\n\n## [2026-11-12 20:13] 为数学二分节真题增加难度及详细解析\n\n- **需求/问题描述**：\n  > 每道题增加一至五星难度，各节由易到难排序；面向基础薄弱的学习者写清条件、方法依据、推导与检查，并修正分数排版。\n- **实际实现的功能与改动**：\n  - 为全部 234 题增加文字星级，同难度保留原先后次序，显示题序连续，原卷年份、题号及小节归属保留。\n  - 逐题扩写已知与目标、方法与条件、推导、结论与检查，补足初次使用的必要术语解释、关键计算、各小问及适用条件；清除紧缩分式和斜杠分数，修正括号命令和缺字。\n  - 234 份题干、选项和图形与修改前完全一致。五项回归检查通过，第四章独立复核及 48 项数值检查通过。\n  - 横屏和 A4 共用源稿编译成功，分别为 488 页、471 页，日志无缺字、警告或溢出。两版均核对 234 道题和解析、逐题星级、解析分页、23 个书签及文字边界；抽查字形坐标确认上下分式。覆盖现有横屏及 iPad PDF；未进行截图或实机验证。\n- **涉及文件**：\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.tex`\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.pdf`\n  - `output/iPad/302数学二分节真题集.pdf`\n  - `.github/scripts/test_question_bank.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n- **Git 提交**：`a8e46659df271d2027e6a038826fe477b28d00a6 feat: grade math questions and expand step-by-step solutions`，已推送至 `origin/main`；本条哈希补记由后续文档提交保存。\n\n---\n"}}}
{"i":2,"result":{"status":"fulfilled","value":{"content":[{"type":"text","text":"Workspace dependencies are available for this local desktop thread.\n\n### Workspace Dependencies\nUse these bundled paths for sheets, slides, documents, PDFs, images, or browser automation:\n- Bundle version: `26.1111.10930`\n- Git executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/fallback/git`\n- Node.js executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node`\n- Node.js packages: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/node_modules`\n- pnpm executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/fallback/pnpm`\n- Python executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/bin/python3`\n- Python packages: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python`\n- Override binaries: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/override`\n- Fallback binaries: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/fallback`"}],"isError":false}}}

## assistant · 2026-11-12T13:04:32Z

我会沿用项目已有的原生 LaTeX 和 PDF 工具，保留可编辑源稿。当前工作区有几份模拟卷文件的删除或移动，我会保留这些状态，另建本次三卷的交付文件。


## tool · 2026-11-12T13:04:35Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"45640c","wall_time_seconds":0.000018292,"exit_code":0,"original_token_count":2868,"output":"references/考研数学一二三09-26年真题&解析/考研数学答题卡（新大纲）.pdf\nreferences/工科数学分析基础第三版 上册（含大纲）.md\nreferences/27302模拟旧/27李林6套卷/数二/做题本/【横版】27李林六套卷做题本.md\nreferences/27302模拟旧/27李林6套卷/数二/做题本/【A4紧凑】27李林六套卷做题本.md\nreferences/27302模拟旧/27李林6套卷/数二/做题本/【A4留白】27李林六套卷做题本.md\nreferences/27302模拟旧/27李林6套卷/数二/考研数学冲刺预测6套卷.md\nreferences/27李林880做题本（先保存后打开）/27李林6套卷/数二/做题本/【A4留白】27李林六套卷做题本.pdf\nreferences/27李林880做题本（先保存后打开）/27李林6套卷/数二/做题本/【横版】27李林六套卷做题本.pdf\nreferences/27李林880做题本（先保存后打开）/27李林6套卷/数二/做题本/【A4紧凑】27李林六套卷做题本.pdf\nreferences/27李林880做题本（先保存后打开）/27李林6套卷/数二/考研数学冲刺预测6套卷.pdf\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【紧凑版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【A4留白版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【A3试卷版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【横版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\nreferences/302真题/考研数学答题卡（新大纲）.md\nreferences/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md\nreferences/302模拟27/模拟卷20套整理合集PDF（可高清打印）/数一答案/【解析】张宇四套卷数一答案.pdf\nreferences/302模拟27/模拟卷20套整理合集PDF（可高清打印）/数二答案/【解析】张宇四套卷数二答案.pdf\nreferences/302模拟27/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf\nreferences/302模拟27/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf\nreferences/302模拟27/往年模拟卷选填精选/数一答案/24张宇四套卷答案-数一.pdf\nreferences/302模拟27/模拟卷40套整理合集PDF（可高清打印）（仅数二）/答案/8-【解析】26周洋鑫四套卷.pdf\nreferences/302模拟27/模拟卷40套整理合集PDF（可高清打印）（仅数二）/答案/1-【解析】26张宇四套卷.pdf\nreferences/302模拟27/往年模拟卷选填精选/数二答案/24张宇四套卷答案-数二.pdf\nreferences/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【A4留白版】李林《六套卷》数二.pdf\nreferences/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【横版】李林《六套卷》数二.pdf\nreferences/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【A3试卷版】李林《六套卷》数二.pdf\nreferences/302模拟27/2027模考/李林《六套卷》/数学二/做题本/【紧凑版】李林《六套卷》数二.pdf\nreferences/302模拟27/2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf\n% !TeX program = xelatex\n% 数学题面为原生 LaTeX。图题为内嵌 TikZ 路径。\n\\documentclass[UTF8,zihao=-4,fontset=fandol]{ctexart}\n\\ifdefined\\QuestionBankAfour\n\\usepackage[a4paper,margin=17mm]{geometry}\n\\else\n\\usepackage[paperwidth=800bp,paperheight=600bp,left=52bp,right=52bp,top=42bp,bottom=47bp]{geometry}\n\\fi\n\\usepackage{amsmath,amssymb,xcolor,fancyhdr,enumitem,tikz}\n\\usetikzlibrary{svg.path}\n\\DeclareMathOperator{\\arcsec}{arcsec}\n\\renewcommand{\\lim}{\\operatorname*{lim}\\limits}\n\\usepackage[hidelinks,bookmarksopen=true]{hyperref}\n\\definecolor{ink}{HTML}{192635}\n\\definecolor{muted}{HTML}{45566A}\n\\definecolor{accent}{HTML}{175C57}\n\\setlength{\\parindent}{0pt}\n\\setlength{\\headheight}{15bp}\n\\pagestyle{fancy}\n\\fancyhf{}\n\\renewcommand{\\headrulewidth}{0pt}\n\\fancyfoot[L]{\\small\\textcolor{muted}{\\hyperlink{contents}{返回目录}}}\n\\fancyfoot[R]{\\small\\textcolor{muted}{\\thepage}}\n\\raggedbottom\n\\newcommand{\\SectionHeading}[4]{%\n  \\clearpage\\hypertarget{sec-#1}{}%\n  {\\small\\textcolor{accent}{#2\\hfill 第 #1 节}}\\par\\medskip\n  {\\LARGE\\bfseries #3}\\par\\smallskip\n  {\\small\\textcolor{muted}{#4}}\\par\\bigskip}\n\\newcommand{\\Theory}[4]{%\n  {\\small\\textcolor{accent}{#1}\\quad\\textbf{#3}\\hfill\\textcolor{muted}{教材 PDF 第 #2 页}}\\par\n  {\\small #4}\\par\\smallskip}\n\\newcommand{\\blank}{\\underline{\\hspace{5em}}}\n\\newcommand{\\pickout}{\\hfill（\\hspace{1.4em}）}\n\\newcommand{\\circnum}[1]{\\textcircled{\\scriptsize #1}}\n\\setlist[enumerate,1]{label=\\textup{(\\arabic*)}}\n\\newenvironment{abcd}{\\begin{enumerate}[label=\\textup{(\\Alph*)},leftmargin=2.3em,itemsep=1pt,topsep=4pt,parsep=1pt]}{\\end{enumerate}}\n\\newcommand{\\choices}[4]{%\n  \\begin{abcd}\n    \\item #1\n    \\item #2\n    \\item #3\n    \\item #4\n  \\end{abcd}}\n\\newcommand{\\graphchoice}[2]{\\begin{minipage}[t]{.235\\linewidth}\\centering\\textup{(#1)}\\par #2\\end{minipage}}\n\\newcommand{\\fourchoices}[4]{%\n  \\par\\smallskip\\noindent\n  \\graphchoice{A}{#1}\\hfill\\graphchoice{B}{#2}\\hfill\\graphchoice{C}{#3}\\hfill\\graphchoice{D}{#4}\\par}\n\\newcommand{\\widechoice}[2]{\\begin{minipage}[t]{.48\\linewidth}\\raggedright\\textup{(#1)}\\enspace #2\\end{minipage}}\n\\newcommand{\\twochoices}[4]{%\n  \\par\\medskip\\noindent\\widechoice{A}{#1}\\hfill\\widechoice{B}{#2}\\par\n  \\medskip\\noindent\\widechoice{C}{#3}\\hfill\\widechoice{D}{#4}\\par}\n\\newcounter{BankQuestion}\n\\ifdefined\\QuestionBankAfour\n\\newcommand{\\DiagramScale}{.85}\n\\newcommand{\\BankFormat}{A4 纵向}\n\\newcommand{\\BankSubtitle}{分节练习版}\n\\newcommand{\\QuestionPage}[7]{%\n  \\stepcounter{BankQuestion}%\n  \\par\\noindent\\begin{minipage}{\\linewidth}\n  \\raggedright\n  {\\small\\textcolor{black!60}{#3\\quad #5\\quad 难度 #7}\\hfill\\textcolor{accent}{#2}}\\par\\smallskip}\n\\newcommand{\\QuestionEnd}{\\end{minipage}\\par\\medskip}\n\\else\n\\newcommand{\\DiagramScale}{1}\n\\newcommand{\\BankFormat}{4:3 横屏}\n\\newcommand{\\BankSubtitle}{iPad 手写练习版}\n\\newcommand{\\QuestionPage}[7]{%\n  \\clearpage\n  \\stepcounter{BankQuestion}%\n  {\\small\\textcolor{accent}{#1\\hfill #2}}\\par\\medskip\n  {\\small\\textcolor{black!60}{#3\\quad #5\\quad 难度 #7\\hfill \\arabic{BankQuestion} / 234}}\\par\\vspace{9bp}}\n\\newcommand{\\QuestionEnd}{}\n\\fi\n\\newenvironment{QuestionSolution}[1]{%\n  \\clearpage\n  {\\small\\textcolor{black!60}{本题解析\\quad #1}}\\par\\medskip\n}{\\par\\clearpage}\n\\begin{document}\n\\hypertarget{contents}{}\n{\\small\\textcolor{accent}{302\\quad 全国硕士研究生招生考试\\hfill \\BankFormat}}\\par\\bigskip\n{\\huge\\bfseries 数学二分节真题集}\\par\\smallskip\n{\\large \\BankSubtitle}\\par\\smallskip\n{\\small 2009--2026 年\\quad 234 题\\quad 上册 19 节}\\par\\smallskip\n{\\small 点击目录进入对应小节。每道题的解析在下一页。}\\par\\bigskip\n{\\small 难度用 1--5 个 * 表示：* 直接应用，** 常规推算，*** 综合分析，**** 多步推理，***** 较难综合。各节由易到难，同难度保留原顺序。评级供学习安排参考。}\\par\\medskip\n\n\\begin{minipage}[t]{0.48\\linewidth}\n\\medskip\\textbf{函数、极限、连续}\\par\n{\\small\\hyperlink{sec-1.1}{1.1\\quad 集合、映射与函数}\\hfill 1 题}\\par\n{\\small\\hyperlink{sec-1.2}{1.2\\quad 数列的极限}\\hfill 10 题}\\par\n{\\small\\hyperlink{sec-1.3}{1.3\\quad 函数的极限}\\hfill 5 题}\\par\n{\\small\\hyperlink{sec-1.4}{1.4\\quad 无穷小量与无穷大量}\\hfill 23 题}\\par\n{\\small\\hyperlink{sec-1.5}{1.5\\quad 连续函数}\\hfill 8 题}\\par\n\\medskip\\textbf{一元函数微分学及其应用}\\par\n{\\small\\hyperlink{sec-2.1}{2.1\\quad 导数的概念}\\hfill 8 题}\\par\n{\\small\\hyperlink{sec-2.2}{2.2\\quad 求导的基本法则}\\hfill 28 题}\\par\n{\\small\\hyperlink{sec-2.3}{2.3\\quad 微分}\\hfill 0 题}\\par\n{\\small\\hyperlink{sec-2.4}{2.4\\quad 微分中值定理及其应用}\\hfill 12 题}\\par\n{\\small\\hyperlink{sec-2.5}{2.5\\quad Taylor定理及其应用}\\hfill 9 题}\\par\nimport hashlib\nfrom pathlib import Path\nimport re\nimport unittest\n\n\nSOURCE = Path(__file__).resolve().parents[2] / \"output/302数学二分节真题集（原生LaTeX横屏版）.tex\"\nCOUNTS = [1, 10, 5, 23, 8, 8, 28, 0, 12, 9, 25, 11, 11, 12, 25, 13, 17, 16, 0]\nHEAD = re.compile(\n    r\"\\\\QuestionPage\\{([^{}]+)\\}\\{([^{}]+)\\}\\{(\\d+) 年第 (\\d+) 题\\}\"\n    r\"\\{(\\d+(?:、\\d+)*)\\}\\{([^{}]+)\\}\\{(\\d+) / 234\\}\\{(\\*{1,5})\\}\"\n)\n\n\nclass QuestionBankTests(unittest.TestCase):\n    @classmethod\n    def setUpClass(cls):\n        cls.source = SOURCE.read_text()\n        cls.sections = re.split(r\"(?=^\\\\SectionHeading\\{)\", cls.source, flags=re.M)[1:]\n\n    def test_question_identity_and_section_counts(self):\n        identities = re.findall(r\"^% Q (\\d+) (\\d+)$\", self.source, re.M)\n        self.assertEqual(len(identities), 234)\n        self.assertEqual(len(set(identities)), 234)\n        self.assertEqual(hashlib.sha256(str(sorted(identities)).encode()).hexdigest(),\n                         \"b201d7886afc28e8454c0aad1e060a7dc4c552f94eeb9347d55294a8a7e715ff\")\n        self.assertEqual([len(re.findall(r\"^% Q \", s, re.M)) for s in self.sections], COUNTS)\n\n    def test_ratings_and_stable_section_order(self):\n        self.assertEqual(len(HEAD.findall(self.source)), 234)\n        for section in self.sections:\n            heads = HEAD.findall(section)\n            order = [(len(h[7]), int(h[6])) for h in heads]\n            self.assertEqual(order, sorted(order), section.splitlines()[0])\n\n    def test_complete_solutions_match_questions(self):\n        blocks = re.split(r\"^% Q \", self.source, flags=re.M)[1:]\n        for block in blocks:\n            identity = block.splitlines()[0]\n            year, number = identity.split()\n            header = HEAD.search(block)\n            self.assertIsNotNone(header, identity)\n            self.assertEqual(header.group(3, 4), (year, number), identity)\n            self.assertEqual(block.count(r\"\\begin{QuestionSolution}\"), 1, identity)\n            self.assertEqual(block.count(r\"\\end{QuestionSolution}\"), 1, identity)\n            self.assertIn(r\"\\begin{QuestionSolution}{\" + f\"{year} 年第 {number} 题\" + \"}\", block)\n            solution = block.split(r\"\\begin{QuestionSolution}\", 1)[1].split(r\"\\end{QuestionSolution}\", 1)[0]\n            for label in (\"已知与目标\", \"方法与条件\", \"推导\", \"结论与检查\"):\n                self.assertIn(r\"\\textbf{\" + label + \"}\", solution, identity)\n\n    def test_readable_stacked_fractions(self):\n        self.assertFalse(r\"\\tfrac\" in self.source, \"源稿仍有紧缩分式\")\n        self.assertNotRegex(self.source, r\"[¼½¾⅐-⅞]\")\n        for line in self.source.splitlines():\n            if (line.startswith(\"%\") or line.startswith(r\"\\QuestionPage{\")\n                    or \"svg\" in line or r\"\\arabic{BankQuestion}\" in line):\n                continue\n            self.assertNotIn(\"/\", line, line[:160])\n\n    def test_delimiter_commands(self):\n        self.assertFalse(re.search(r\"(?<!\\\\)\\b(?:left|right)\\s*\\(\", self.source),\n                         \"公式括号命令缺少反斜杠\")\n\n\nif __name__ == \"__main__\":\n    unittest.main()\n"}
{"chunk_id":"a7f9a2","wall_time_seconds":0.000008167,"exit_code":0,"original_token_count":558999,"output":"Warning: truncated output (original token count: 558999)\n... 1187418 bytes omitted ...\n\n.question-bank-work/compare-302-older-twenty.py\n.question-bank-work/check-bank-math.py\n.question-bank-work/assemble-older-lilin-2.py\n.question-bank-work/filter-302-zhang-math3.py\n.question-bank-work/verify-302-ten-twenty-two.py\n.question-bank-work/older-lilin-crop.py\n.question-bank-work/audit-302-ten-twenty-lost-ink.py\n.question-bank-work/render-proof-302-variants.py\n.question-bank-work/render-302-zhang-horizontal-check.py\n.question-bank-work/assemble-302-zhang-1.py\n.question-bank-work/copy-older-topic-zhang8.py\n.question-bank-work/batch-proof-302.py\n.question-bank-work/render-302-older.py\n.question-bank-work/prepare-older-forty-early.py\n.question-bank-work/ocr-302-spreads.py\n.question-bank-work/verify-302-zhang-printed.py\n.question-bank-work/assemble-older-topics.py\n.question-bank-work/verify-302-zhang-horizontal.py\n.question-bank-work/render-proof-302-wu.py\n.question-bank-work/test-302-batch-ocr.py\n.question-bank-work/prepare-older-topic-candidates.py\n.question-bank-work/apply-302-hefei.py\n.question-bank-work/render-302-zhang-printed.py\n.question-bank-work/proof-302-ocr.py\n.question-bank-work/render-302-zhang-a4-outliers.py\n.question-bank-work/apply-302-older-twenty.py\n.question-bank-work/older-forty-candidates.py\n.question-bank-work/render-302-zhang-year-differences.py\n.question-bank-work/apply-302-twenty-two.py\n.question-bank-work/remove-302-standalone-math3.py\n.question-bank-work/assemble-302-twenty-one.py\n.question-bank-work/302-ocr-model/configuration_paddleocr_vl.py\n.question-bank-work/302-ocr-model/processing_paddleocr_vl.py\n.question-bank-work/302-ocr-model/image_processing_paddleocr_vl.py\n.question-bank-work/302-ocr-model/modeling_paddleocr_vl.py\n.question-bank-work/compare-302-zhang-a4.py\n.question-bank-work/check-topic8.py\n.question-bank-work/apply-older-forty.py\n.question-bank-work/assemble-302-older-10-one.py\n.question-bank-work/compare-302-zhang-shared.py\n.question-bank-work/render-proof-302-lilin-a4.py\n.question-bank-work/inspect-302-questions.py\n.question-bank-work/proof-katex/node_modules/katex/src/fonts/generate_fonts.py\n.question-bank-work/assemble-302-wu-basic.py\n.question-bank-work/clean-302-questions.py\n.question-bank-work/render-proof-302-doing-books.py\n.question-bank-work/render-proof-302-official.py\n.question-bank-work/verify-302.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/_sounddevice_data/__init__.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/uts46data.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/__main__.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/codec.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/cli.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/core.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/__init__.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/idnadata.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/compat.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/package_data.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/__main__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/filter.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/plugin.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/regexopt.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/lexer.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/unistring.py\n.question-bank-work/uv/archive-v0/O-KoQNiVMdfeKHR7/idna/intranges.py\n.question-bank-work/proof-katex/node_modules/katex/src/metrics/format_json.py\n.question-bank-work/proof-katex/node_modules/katex/src/metrics/extract_tfms.py\n.question-bank-work/proof-katex/node_modules/katex/src/metrics/parse_tfm.py\n.question-bank-work/proof-katex/node_modules/katex/src/metrics/extract_ttfs.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/stata_light.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/nord.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/arduino.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/algol.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/trac.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/night_owl.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/perldoc.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/rrt.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/autumn.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/manni.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/rainbow_dash.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/abap.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/fruity.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/lightbulb.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/murphy.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/_mapping.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/coffee.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/borland.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/vim.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/stata_dark.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/lovelace.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/paraiso_light.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/default.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/vs.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/dracula.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/emacs.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/bw.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/zenburn.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/igor.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/lilypond.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/colorful.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/native.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/gh_dark.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/algol_nu.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/solarized.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/paraiso_dark.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/staroffice.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/friendly.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/tango.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/monokai.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/gruvbox.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/xcode.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/inkpot.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/onedark.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/pastie.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/friendly_grayscale.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/material.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/styles/sas.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/latex.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/groff.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/_mapping.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/pangomarkup.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/bbcode.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/svg.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/rtf.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/terminal256.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/formatters/img.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/pygments/for…257652 tokens truncated…/做题本/【横版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/.DS_Store\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数一/【横版】27张宇八套卷做题本数一.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数一/【紧凑版】27张宇八套卷做题本数一.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数一/【竖版】27张宇八套卷做题本数一.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\n# 完成标准\n\n## 当前任务：分节真题难度与详细解析\n\n- 234 个原卷年份与题号组合保持一致，各题保留原小节、题干、选项、图形和全部小问；234 份解析与题目一一对应。\n- 题头均有 1–5 个文字 `*`，各节难度非递减；同难度保留原顺序；显示题序连续。\n- 每份解析包含条件与目标、方法依据、必要中间计算、明确结论和针对性检查；逐题校订，客观结构检查不能替代数学正确性检查。\n- 数学算式不使用斜杠分数、Unicode 分数字符或紧缩的 `\\tfrac`；分子分母及指数分组正确。\n- 横屏和 A4 实际编译成功，无缺字或内容溢出；检查 PDF 234 个题头、解析对应与难度顺序、书签和文字边界。未授权视觉检查，不截图。\n- 保留用户已有的裁片 PDF 删除及 iPad 目录其他内容，只提交任务相关文件。\n\n2026-11-12 验证结果：五项源稿回归检查通过，234 份题面与任务开始前 HEAD 完全一致，题号集合、小节题量及解析对应正确。星级 1–5 分别为 6、110、88、29、1 题，各节稳定升序。234 份解析均含已知与目标、方法与条件、推导、结论与检查；算式没有斜杠分数、Unicode 分数或紧缩分式。\n\nTectonic 0.17.0 使用既有缓存编译：横屏 488 页、A4 471 页，日志无缺字、警告或溢出。两份 PDF 均核对 234 个题头、234 个解析入口及 23 个书签；星级与源稿逐题一致，解析从题目下一页开始，文字均在页面内。用 2017 年第 10 题解析的字形坐标和分数线确认分子在上、分母在下。现有横屏及 iPad PDF 均由本次横屏编译结果覆盖。第四章 33 题经独立代理复核，选定方程、初值及面积、体积、弧长、冷却时间通过 48 项数值检查。未做截图或 iPad 实机检查。\n\n本次张宇八套：两科各八卷、每卷 16 题及 40 个选项；对照源 PDF 逐题核对，不以候选文件存在或公式渲染成功代替原页校对。四份交付文件只更新张宇八套分组。\n\n2026-11-12 已对照两科紧凑版第 71–94 页逐题校对 256 题。修正分段函数、积分限、单侧极限、向量与矩阵分量、微分阶数、补事件及条件概率，补全数二卷二第 3 题的容器与四幅曲线描述。留白版第 140–187 页去除页脚和空白后的文字与紧凑版一致，数一 3 幅、数二 5 幅图示的图片数据哈希一致。原 PDF 自身的选项及公式写法按来源保留。\n\n`.question-bank-work/check-topic8.py after` 通过：四份交付文件各有八卷、128 题和 320 个选项，逐卷等于校对稿；张宇八套以外的分组哈希与修改前一致。16 份校对稿合计 1463 个数学表达式通过 `verify-302-math.cjs`，无警告。题面校对未包括独立复算全部答案。\n\n确认源 PDF 与 Markdown 的相对路径一一对应，页码连续且数量与 PDF 一致。检查文字层和扫描页样本、源链接及无文本页记录。\n\n## 27302 阶段模拟卷\n\n检查 22 道题的原题位置、公式、唯一答案和范围内解法。核对卷面分值 $50+30+70=150$，实际编译 LaTeX，检查 PDF 文本中题号、分节和缺字。\n\n- 结构检查通过。三类题分别为 10、6、6 道，22 道题均有出处，六道解答题分值为 10、12、12、12、12、12。\n- 选择题复算结果为 B、A、D、C、B、D、A、D、A、C。填空题依次为 $Ae^b$、$6$、$-2$、$\\pi+2$、$1/2$、$9$。\n- 第 17 题用等价无穷小和洛必达法则，极限为 $1/3$、$1/6$。第 18 题用参数求导，结果为 $\\sin t/(1-\\cos t)$ 和 $-1/(1-\\cos t)^2$。第 19 题用连续和导数的定义及振荡数列，依次得 $p>0$、$p>1$、$p>2$。\n- 第 20 题对 $f(t+1/n)-f(t)$ 在等分点的取值作望远镜求和，再用介值定理。第 21 题在两个半区间用拉格朗日定理，第二问对 $f^2$ 和 $x^2$ 用柯西中值定理。第 22 题用端点导数符号判断闭区间的极值在内部，再用费马定理，第二问应用于 $f(x)-\\mu x$。\n- Tectonic 编译成功，日志无警告、缺字或溢出报告。PDF 为四页 A4，逐页检查了页码、分节、题号 1–22 和文字边界。未进行截图检查。\n\n## 扩充阶段模拟卷\n\n每卷检查 10 道单选、6 道填空、6 道解答和 150 分，核对题源定位、与旧卷及新增卷之间的重复、范围内解法和补充练习题量。编译后检查逐卷题序、分节、文字边界及缺字日志。\n\n- 新增四卷共 88 道。补充练习有 21 道选择、28 道填空、27 道解答。逐题核对了来源页码，新旧卷共用同一原题时仅取未收录的小问。\n- 第二卷选择题依次为 C、D、B、D、A、B、A、B、C、C。填空题依次为 $1$、$-2$、$p\\le2$、$2\\ln2$、$y=1+(x-\\mathrm e)/(\\mathrm e+1)$、$3/2$。\n- 第三卷选择题依次为 A、D、B、C、D、C、A、C、C、A。填空题依次为 $0$、$1/a_1$、$1$、$1$、$a^2b$、$-1/(3\\mathrm e)$。\n- 第四卷选择题依次为 C、B、B、B、C、C、C、C、C、B。填空题依次为 $(1/8,4)$、$1/3$、$1/12$、$-99!$、$-2$、$-1/2$。\n- 第五卷选择题依次为 C、C、A、B、B、B、D、D、C、C。填空题依次为 $1$、$-1/24$、$(2/3,3)$、$3$、$1/\\pi$、$1$。\n- 数值抽查覆盖数列和式、乘积极限、三角无穷小和指数差极限。Tectonic 编译成功，日志无缺字或溢出报告。检查了 22 页 A4 的题号、页码、文字边界和五个 PDF 书签。未进行截图检查。\n\n## 302 数学二分节真题集\n\n核对 2009–2026 年的 408 个年份与题号组合，包含 156 道选择题、108 道填空题、144 道解答题。正文 19 节，逐节检查章节名称、题型分组和题号顺序。410 个题面裁片引用各出现一次，所有裁片页均通过边界、非空和原裁片墨迹量比对。对题号执行本机 OCR 复核，并对调整过的边界复查。2009 年第 6 题和 2010 年第 8 题保留跨页续题。\n\n完成 LaTeX 结构及资源引用检查。本次未进行 TeX 编译，未发现独立安装的编译器。\n\n## 302 数学二 iPad 横屏版\n\n核对 PDF 每页为 4:3 横屏、408 道题各占一页、题面完整、作答区留白且目录跳转有效。核对 19 节的定理编号和教材 PDF 页码，以及 LaTeX 与 PDF 的题序和题面引用。采用 PDF 几何和文字检查，不安装 TeX。\n\n确认 432 页全部为 800 × 600 点。408 道题各占一页，410 个裁片按原比例嵌入，裁片非空且与原题面墨迹量一致至检查容差。逐题检查题面下方固定区域为空白，两道跨页题的两个裁片都在各自同一页。核对 85 条编号定理与教材 PDF 页码，验证 29 个书签、894 个内部链接以及 LaTeX 的 408 个题页和 410 个裁片引用。未编译 LaTeX，未做截图检查。\n\n## 302 数学二原生 LaTeX 题面\n\n与教材目录核对正文 19 节的节名、顺序和教材起始页。核对 408 道题的唯一题号、题型、数学定界符和原卷页码标记，沿用 85 条编号定理和 28 条其他要点。用本机应用自带的 Tectonic 编译，两版均无缺字或溢出警告。\n\n横屏 PDF 为 432 页，页宽和页高分别为 800 和 600 点。验证 408 道题逐题单页、文字可提取、最短作答区 102.2 点、455 个有效内部链接及 28 个书签。六页图题包含可验证的矢量路径，所有页面无嵌入图片。A4 入口编译为 89 页，验证纸张尺寸、408 道题的顺序和内部链接。未安装编译器，未做截图检查。\n\n两版通过 Tectonic 编译，日志无缺字、溢出和警告。2017 年第 3 题的 8 个趋近条件的字形均位于 `lim` 正下方。408 道题题序一致，题头未提取到原卷 PDF 页码，教材页码仍可提取。横屏版为 432 页，一题一页，保留 28 个书签和 455 个有效内部链接。A4 版为 89 页。未进行截图检查。\n\nTectonic 编译成功，日志无缺字、溢出和警告。逐题核对两版共 408 道题的标题、知识点基线、字号和灰色值。两版仍未显示原卷 PDF 页码，2017 年第 3 题的 8 个极限条件仍在 `lim` 正下方。横屏版 432 页，A4 常规版 89 页，内部链接均有效。未进行截图检查。\n"}

## tool · 2026-11-12T13:04:43Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"bb06e3","wall_time_seconds":0.000010708,"exit_code":0,"original_token_count":5808,"output":"# 工科数学分析基础第三版 上册（含大纲）\n\n[原始 PDF](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf) · 共 390 页\n\n> 本文由扫描 PDF 逐页自动识别。公式、图表与版式可通过各页链接回查原文。\n\n## 大纲\n\n- [封面](#pdf-page-1)\n- [书名](#pdf-page-3)\n- [版权](#pdf-page-4)\n- [前言](#pdf-page-5)\n- [目录](#pdf-page-13)\n- [绪论](#pdf-page-18)\n- [第一章 函数、极限、连续](#pdf-page-24)\n    - [第一节 集合、映射与函数](#pdf-page-24)\n        - [1.1 集合及其运算](#pdf-page-24)\n        - [1.2 实数集的完备性与确界存在定理](#pdf-page-27)\n        - [1.3 映射与函数的概念](#pdf-page-29)\n        - [1.4 线性函数的基本属性](#pdf-page-33)\n        - [1.5 复合映射与复合函数](#pdf-page-35)\n        - [1.6 逆映射与反函数](#pdf-page-36)\n        - [1.7 初等函数与双曲函数](#pdf-page-37)\n        - [习题1.1](#pdf-page-38)\n    - [第二节 数列的极限](#pdf-page-41)\n        - [2.1 数列极限的概念](#pdf-page-41)\n        - [2.2 收敛数列的性质](#pdf-page-46)\n        - [2.3 数列收敛性的判别准则](#pdf-page-50)\n        - [习题1.2](#pdf-page-58)\n    - [第三节 函数的极限](#pdf-page-60)\n        - [3.1 函数极限的概念](#pdf-page-60)\n        - [3.2 函数极限的性质](#pdf-page-66)\n        - [3.3 两个重要极限](#pdf-page-70)\n        - [3.4 函数极限的存在准则](#pdf-page-73)\n        - [习题1.3](#pdf-page-75)\n    - [第四节 无穷小量与无穷大量](#pdf-page-77)\n        - [4.1 无穷小量的概念与性质](#pdf-page-77)\n        - [4.2 无穷小的比较](#pdf-page-79)\n        - [4.3 无穷小的等价代换](#pdf-page-82)\n        - [4.4 无穷大量](#pdf-page-83)\n        - [习题1.4](#pdf-page-85)\n    - [第五节 连续函数](#pdf-page-86)\n        - [5.1 函数的连续性概念与间断点的分类](#pdf-page-86)\n        - [5.2 连续函数的运算性质与初等函数的连续性](#pdf-page-90)\n        - [5.3 闭区间上连续函数的性质](#pdf-page-94)\n        - [5.4 函数的一致连续性](#pdf-page-98)\n        - [*5.5 一维空间R上的压缩映射原理与迭代法](#pdf-page-101)\n        - [习题1.5](#pdf-page-102)\n    - [第1章习题](#pdf-page-104)\n    - [综合练习题](#pdf-page-106)\n- [第二章 一元函数微分学及其应用](#pdf-page-108)\n    - [第一节 导数的概念](#pdf-page-108)\n        - [1.1 导数的定义](#pdf-page-108)\n        - [1.2 导数的几何意义](#pdf-page-113)\n        - [1.3 可导与连续的关系](#pdf-page-115)\n        - [1.4 导数在科学技术中的含义——变化率](#pdf-page-116)\n        - [习题2.1](#pdf-page-119)\n    - [第二节 求导的基本法则](#pdf-page-121)\n        - [2.1 函数和、差、积、商的求导法则](#pdf-page-121)\n        - [2.2 复合函数的求导法则](#pdf-page-123)\n        - [2.3 反函数的求导法则](#pdf-page-125)\n        - [2.4 初等函数的求导问题](#pdf-page-127)\n        - [2.5 高阶导数](#pdf-page-128)\n        - [2.6 隐函数求导法](#pdf-page-130)\n        - [2.7 由参数方程确定的函数的求导法则](#pdf-page-132)\n        - [2.8 相关变化率问题](#pdf-page-134)\n        - [习题2.2](#pdf-page-136)\n    - [第三节 微分](#pdf-page-140)\n        - [3.1 微分的概念](#pdf-page-141)\n        - [3.2 微分的运算法则](#pdf-page-143)\n        - [3.3 高阶微分](#pdf-page-144)\n        - [3.4 微分在近似计算中的应用](#pdf-page-144)\n        - [习题2.3](#pdf-page-145)\n    - [第四节 微分中值定理及其应用](#pdf-page-147)\n        - [4.1 函数的极值及其必要条件](#pdf-page-147)\n        - [4.2 微分中值定理](#pdf-page-148)\n        - [4.3 L’Hospital法则](#pdf-page-154)\n        - [习题2.4](#pdf-page-159)\n    - [第五节 Taylor定理及其应用](#pdf-page-161)\n        - [5.1 Taylor定理](#pdf-page-162)\n        - [5.2 几个初等函数的Maclaurin公式](#pdf-page-165)\n        - [5.3 Taylor公式的应用](#pdf-page-167)\n        - [习题2.5](#pdf-page-170)\n    - [第六节 函数性态的研究](#pdf-page-171)\n        - [6.1 函数的单调性](#pdf-page-171)\n        - [6.2 函数的极值](#pdf-page-173)\n        - [6.3 函数的最大（小）值](#pdf-page-175)\n        - [6.4 函数图像的凹凸性与拐点](#pdf-page-178)\n        - [习题2.6](#pdf-page-182)\n    - [第2章习题](#pdf-page-185)\n    - [综合练习题](#pdf-page-187)\n- [第三章 一元函数积分学及其应用](#pdf-page-189)\n    - [第一节 定积分的概念、存在条件与性质](#pdf-page-189)\n        - [1.1 定积分问题举例](#pdf-page-189)\n        - [1.2 定积分的定义](#pdf-page-192)\n        - [1.3 定积分的存在条件](#pdf-page-195)\n        - [1.4 定积分的性质](#pdf-page-197)\n        - [习题3.1](#pdf-page-201)\n    - [第二节 微积分基本公式与基本定理](#pdf-page-203)\n        - [2.1 微积分基本公式](#pdf-page-203)\n        - [2.2 微积分基本定理](#pdf-page-206)\n        - [2.3 不定积分](#pdf-page-209)\n        - [习题3.2](#pdf-page-211)\n    - [第三节 两种基本积分法](#pdf-page-214)\n        - [3.1 换元积分法](#pdf-page-214)\n        - [3.2 分部积分法](#pdf-page-225)\n        - [3.3 初等函数的积分问题](#pdf-page-230)\n        - [习题3.3](#pdf-page-230)\n    - [第四节 定积分的应用](#pdf-page-233)\n        - [4.1 建立积分表达式的微元法](#pdf-page-234)\n        - [4.2 定积分在几何中的应用举例](#pdf-page-235)\n        - [4.3 定积分在物理中的应用举例](#pdf-page-239)\n        - [习题3.4](#pdf-page-242)\n    - [第五节 反常积分](#pdf-page-244)\n        - [5.1 无穷区间上的积分](#pdf-page-244)\n        - [5.2 无界函数的积分](#pdf-page-247)\n        - [5.3 无穷区间上积分的审敛准则](#pdf-page-250)\n        - [5.4 无界函数积分的审敛准则](#pdf-page-253)\n        - [5.5 Γ函数](#pdf-page-255)\n        - [习题3.5](#pdf-page-256)\n    - [第3章习题](#pdf-page-258)\n    - [综合练习题](#pdf-page-261)\n- [第四章 常微分方程](#pdf-page-262)\n    - [第一节 几类简单的微分方程](#pdf-page-262)\n        - [1.1 几个基本概念](#pdf-page-263)\n        - [1.2 可分离变量的一阶微分方程](#pdf-page-266)\n        - [1.3 一阶线性微分方程](#pdf-page-267)\n        - [1.4 可用变量代换法求解的一阶微分方程](#pdf-page-270)\n        - [1.5 可降阶的高阶微分方程](#pdf-page-274)\n        - [1.6 微分方程应用举例](#pdf-page-277)\n        - [习题4.1](#pdf-page-282)\n    - [第二节 高阶线性微分方程](#pdf-page-284)\n        - [2.1 高阶线性微分方程举例](#pdf-page-284)\n        - [2.2 线性微分方程解的结构](#pdf-page-287)\n        - [2.3 高阶常系数线性齐次微分方程的解法](#pdf-page-294)\n        - [2.4 高阶常系数线性非齐次微分方程的解法](#pdf-page-299)\n        - [2.5 高阶变系数线性微分方程的求解问题](#pdf-page-307)\n        - [习题4.2](#pdf-page-308)\n    - [*第三节 线性微分方程组](#pdf-page-310)\n        - [3.1 线性微分方程组的基本概念](#pdf-page-310)\n        - [3.2 线性微分方程组解的结构](#pdf-page-312)\n        - [3.3 常系数线性齐次微分方程组的求解方法](#pdf-page-319)\n        - [3.4 常系数线性非齐次微分方程组的求解](#pdf-page-329)\n        - [3.5 微分方程组应用举例](#pdf-page-330)\n        - [习题4.3](#pdf-page-335)\n    - [第4章习题](#pdf-page-337)\n    - [综合练习题](#pdf-page-339)\n- [附录](#pdf-page-340)\n    - [附录1 函数的参数表示与极坐标表示](#pdf-page-340)\n    - [附录2 常见曲线及其方程](#pdf-page-344)\n    - [附录3 常用的三角函数公式](#pdf-page-351)\n    - [附录4 反三角函数定义及其图形](#pdf-page-352)\n    - [附录5 复数及其运算](#pdf-page-355)\n    - [附录6 简明积分表](#pdf-page-357)\n- [部分习题答案与提示](#pdf-page-364)\n- [参考文献](#pdf-page-389)\n\n<a id=\"pdf-page-1\"></a>\n\n## PDF 第 1 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=1)\n\n面向21世纪课程教材\nTextbook Series for 21st Century\n\n工科数学分析基础\n\n第三版 上册\n\n• 王绵森 马知恩 主编\n\n高等教育出版社\n\n<a id=\"pdf-page-2\"></a>\n\n## PDF 第 2 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=2)\n\n第一版荣获2002年全国普通高等学校优秀教材一等奖\n\n数字课程网站\n网址：http://abook.hep.com.cn/48216\nhttp://abook.hep.edu.cn/48216\n数字课程账号 使用说明详见书内数字课程说明页\n\nISBN 978-7-04-048216-4\n9 787040 482164 >\n定价 47.20元\n\n<a id=\"pdf-page-3\"></a>\n\n## PDF 第 3 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=3)\n\n面向21世纪课程教材\nTextbook Series for 21st Century\n\n51:- [第二章 一元函数微分学及其应用](#pdf-page-108)\n62:        - [2.4 初等函数的求导问题](#pdf-page-127)\n74:    - [第四节 微分中值定理及其应用](#pdf-page-147)\n76:        - [4.2 微分中值定理](#pdf-page-148)\n77:        - [4.3 L’Hospital法则](#pdf-page-154)\n78:        - [习题2.4](#pdf-page-159)\n79:    - [第五节 Taylor定理及其应用](#pdf-page-161)\n80:        - [5.1 Taylor定理](#pdf-page-162)\n82:        - [5.3 Taylor公式的应用](#pdf-page-167)\n104:    - [第三节 两种基本积分法](#pdf-page-214)\n105:        - [3.1 换元积分法](#pdf-page-214)\n110:        - [4.1 建立积分表达式的微元法](#pdf-page-234)\n114:    - [第五节 反常积分](#pdf-page-244)\n115:        - [5.1 无穷区间上的积分](#pdf-page-244)\n129:        - [1.5 可降阶的高阶微分方程](#pdf-page-274)\n132:    - [第二节 高阶线性微分方程](#pdf-page-284)\n133:        - [2.1 高阶线性微分方程举例](#pdf-page-284)\n135:        - [2.3 高阶常系数线性齐次微分方程的解法](#pdf-page-294)\n136:        - [2.4 高阶常系数线性非齐次微分方程的解法](#pdf-page-299)\n378:2. 注意分析、代数、几何内容的有机结合，相互渗透。本书在多元函数微积分和微分方程组部分，加强了向量和矩阵的运用，充分利用向量、矩阵和线性代数中其他知识来表述分析中的有关内容。例如，用Jacobi矩阵来表示Rn到Rm的多元向量值函数的微分；利用梯度、Hesse矩阵来表示多元函数Taylor公式中的有关系数；利用向量和矩阵研究微分方程组；运用向量值函数的微分来研究曲线与曲面；将第二型线面积分与向量场的研究密切结合等。这种处理方法，不但符合现代数学的发展趋势，也可以更好地满足现代科技对数学用法的要求，有利于改变在后继课程中学生不习惯于运用向量和矩阵的状况，培养学生综合运用数学知识的能力。\n390:4. 加强数学应用能力的培养。本书在讲解数学内容的同时，力求突出在解决实际问题中有重要应用的数学思想方法，揭示重要数学概念和方法的本质。例如，在绪论中强调且贯穿全书的微积分基本思想方法；微分中的局部线性化思想；Taylor公式和无穷级数中的逼近思想；极值问题中的最优化思想；积分应用中的微元法以及贯穿全书的变换思想和方法等。本书除保存了一些几何、物理方面的例子外，增加了不少诸如在工程、生态、人口、经济、医学甚至日常生活方面的例题和习题，注意了应用问题的趣味性，以增强对读者的吸引力。此外，还配备了一些综合练习题，有的需要上机计算，使读者从建立模型，寻求方法到问题解决的全过程受到初步的训练。\n478:第二章 一元函数微分学及其应用 ····· 91\n491:2.4 初等函数的求导问题 ····· 110\n514:第四节 微分中值定理及其应用 ····· 130\n516:4.2 微分中值定理 ····· 131\n517:4.3 L'Hospital法则 ····· 137\n518:习题2.4 ····· 142\n520:第五节 Taylor定理及其应用 ····· 144\n521:5.1 Taylor定理 ····· 145\n523:5.3 Taylor公式的应用 ····· 150\n583:综合练习题 ····· 244\n609:2.4 高阶常系数线性非齐次微分方程的解法 ····· 282\n729:才能求得；后者像例2中那样，需要通过“分”“匀”“合”“精”四个步骤，用一个“和式极限”（0.4）式才能求得。前者就是将在第二章中研究的导数问题，后者则是第三章中讨论的积分问题.\n1555:例2.4 求 $\\lim_{n \\to \\infty} \\frac{1^2 + 2^2 + \\cdots + n^2}{n^3}$.\n1571:解 由于待求极限数列的通项是 $n$ 项之和,当 $n \\to \\infty$ 时,就是无限多项之和,不能直接利用有理运算法则(1).对于这种情况,可类似于例2.4,先设法求出 $n$ 项之和,再用法则(1).本例中,利用将每一项写成两项之差,可得\n1584:定理2.4（保号性）设 $\\lim_{n \\to \\infty} a_n = a, a \\neq 0$，则 $\\exists N \\in \\mathbf{N}_+$，使得 $\\forall n > N, a_n$ 与 $a$ 同号. 并且，若 $a > 0$（或 $a < 0$），则 $\\exists N \\in \\mathbf{N}_+$，使得 $\\forall n > N$，恒有 $a_n \\geq q > 0$（或 $a_n \\leq q < 0$).\n1612:想一想：定理 2.4 的证明中，为什么取 $\\varepsilon=\\frac{a}{2}$？$\\varepsilon$ 可以取其他数吗？\n1626:(2) 由于该数列的通项是 $n$ 项之和，并且难以直接求得该和，不能利用例 2.4 和例 2.6 中的方法，所以利用不等式放、缩技巧，易得\n1740:$$e = 2.718281828459045\\cdots.$$\n1914:二维码 1.2.4 无界数列、发散数列和无穷大数列之间的关系.\n2137:例 3.2 用定义验证 $\\lim_{x\\to 2}\\frac{x^2-4}{x-2}=4.$\n2141:$$\\left|\\frac{x^2-4}{x-2}-4\\right|=|x-2|<\\varepsilon,$$\n2143:只要取 $\\delta=\\varepsilon$ 就行了.因此,当 $0<|x-2|<\\delta$ 时,就有 $\\left|\\frac{x^2-4}{x-2}-4\\right|<\\varepsilon$.由定义知 $\\lim_{x\\to 2}\\frac{x^2-4}{x-2}=4.$\n2145:例 3.3 用定义验证: $\\lim_{x\\to 2}\\frac{x-2}{x^2-4}=\\frac{1}{4}.$\n2401:下面介绍微积分中两个常用的重要极限公式，它们不但可以用来求一些更复杂函数的极限，而且是第二章中建立一些重要导数公式的基础，读者应当牢记并能熟练地运用它们。\n# 考研数学冲刺预测6套卷\n\n## 第一套\n\n### 选择题\n\n1\\. 当 $x\\to0$ 时，$ax+bx^2+\\ln(1+x)$ 与 $\\mathrm{e}^{x^2}-\\cos x$ 是等价无穷小，则下列选项正确的是（　）。\n\nA. $a=-1,b=2$  \nB. $a=-1,b=-2$  \nC. $a=1,b=2$  \nD. $a=1,b=-2$\n\n2\\. 设 $a,b,k$ 均为不为零的常数，则 $\\lim_{x\\to a}\\frac{f(x)-b}{x-a}=k$ 是 $\\lim_{x\\to a}\\frac{\\mathrm{e}^{f(x)}-\\mathrm{e}^b}{x-a}=k\\mathrm{e}^b$ 的（　）。\n\nA. 充分非必要条件  \nB. 必要非充分条件  \nC. 充分必要条件  \nD. 既非充分又非必要条件\n\n3\\. 设 $\\mathrm{e}<x_1<x_2$，则下列不等式成立的是（　）。\n\n① $x_2\\ln x_2>x_1\\ln x_1$。  \n② $x_1\\ln x_2<x_2\\ln x_1$。  \n③ $x_2\\ln x_2<x_1\\ln x_1$。  \n④ $x_1\\ln x_2>x_2\\ln x_1$。\n\nA. ②③  \nB. ①②  \nC. ①④  \nD. ③④\n\n4\\. 设 $f(\\alpha)=\\lim_{x\\to0}\\frac{(1+x)^\\alpha-1}{x^\\alpha}$ 有界，$\\alpha\\in\\mathbb{R}$，则 $\\alpha$ 的取值范围为（　）。\n\nA. $(-\\infty,0)$  \nB. $(-\\infty,1]$  \nC. $(-\\infty,1)$  \nD. $(-\\infty,0]$\n\n5\\. 设 $\\int_0^{\\frac{\\pi}{2}}(\\mathrm{e}^{\\cos x}+\\mathrm{e}^{\\sin x})\\,\\mathrm{d}x\\le a$，则下列四个选项中 $a$ 最小可取（　）。\n\nA. $\\pi\\mathrm{e}^{\\sqrt{2}}$  \nB. $\\mathrm{e}^{\\frac{\\sqrt{2}}2}$  \nC. $\\pi\\mathrm{e}^{\\frac{\\sqrt{2}}2}$  \nD. $2\\mathrm{e}^{\\sqrt{2}}$\n\n6\\. 设连续函数 $f(x,y)$ 满足 $\\lim_{(x,y)\\to(1,0)}\\frac{f(x,y)-x+2y+2}{\\sqrt{(x-1)^2+y^2}}=0$，则 $\\lim_{u\\to0}\\frac{f(1+3u,0)-f(1,2u)}{u}=$（　）。\n\nA. $1$  \nB. $3$  \nC. $5$  \nD. $7$\n\n7\\. 设 $y=y(x)$ 满足 $y''+4y'+4y=0$，$y(0)=0$，且 $\\int_0^{+\\infty}y(x)\\,\\mathrm{d}x=\\frac14$，则 $y(x)$ 的极大值为（　）。\n\nA. $2\\mathrm{e}$  \nB. $\\frac{1}{2\\mathrm{e}}$  \nC. $\\mathrm{e}$  \nD. $\\frac{1}{\\mathrm{e}}$\n\n8\\. 设 $A$ 为 $4$ 阶实矩阵，则 $r(A)-r(A^2)$ 取值不可能为（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $3$\n\n9\\. 设 $A$ 是 $3$ 阶实对称矩阵，$r(A)=1$，$\\alpha=(-1,1,1)^T$ 满足 $(A-2E)\\alpha=0$，则方程组 $AX=0$ 的基础解系为（　）。\n\nA. $(1,1,0)^T,(1,-1,0)^T$  \nB. $(1,1,0)^T,(1,0,1)^T$  \nC. $(1,1,0)^T,(1,1,1)^T$  \nD. $(1,1,0)^T,(1,0,-1)^T$\n\n10\\. 设 $A$ 为 $3$ 阶实矩阵，则下列选项中能推出 $A$ 必有特征值 $1$ 的是（　）。\n\nA. $2$ 是 $A+A^{-1}$ 的一个特征值  \nB. $2$ 是 $A+A^T$ 的一个特征值  \nC. $2$ 是 $A+A^*$ 的一个特征值  \nD. $2$ 是 $A+A^2$ 的一个特征值\n\n### 填空题\n\n11\\. 设 $f(x)$ 在 $x=1$ 处连续，$\\lim_{x\\to1}\\frac{f(x)-5x+2}{\\ln x}=1$，则 $f'(1)=$ ______。\n\n12\\. 已知 $f(x)=\\ln x-a\\sqrt{x}$（$a>0$）在 $x\\in(0,+\\infty)$ 内有唯一零点，则 $a=$ ______。\n\n13\\. 已知 $y=\\int_1^{1+\\sin t}\\left(1+\\mathrm{e}^{\\frac1s}\\right)\\,\\mathrm{d}s$，其中 $t=t(x)$ 由 $\\begin{cases}x=\\cos 2v,\\\\t=\\sin v\\end{cases}$ 确定，则 $\\frac{\\mathrm{d}y}{\\mathrm{d}x}=$ ______。\n\n14\\. 设反常积分 $I=\\int_0^{+\\infty}\\frac{\\arctan x}{x^a(2+x^3)}\\,\\mathrm{d}x$ 收敛，则 $a$ 的取值范围为 ______。\n\n15\\. 双纽线 $r^2=a^2\\cos 2\\theta$（$a>0$）绕极轴旋转一周所得旋转曲面的面积为 ______。\n\n16\\. 设 $3$ 阶行列式 $|A|=1$，将矩阵 $A$ 的第 $1$ 列加到第 $2$ 列得到 $B$，$A^*$ 是 $A$ 的伴随矩阵，则 $|A^*+B^{-1}|=$ ______。\n\n### 解答题\n\n17\\.（本题满分 10 分）设 $f''(x)$ 在 $x=0$ 处连续，$f'(0)=0$，$f''(0)=1$，求 $\\lim_{x\\to0}\\frac{\\int_0^x\\{f(t)-f[\\ln(1+t)]\\}\\,\\mathrm{d}t}{x^4}$。\n\n18\\.（本题满分 12 分）设 $x\\ge0$，$y\\ge0$，有 $(x^2+y^2)\\mathrm{e}^{-x-y}\\le k\\mathrm{e}^{-2}$，求 $k$ 的最小值。\n\n19\\.（本题满分 12 分）设 $D=\\{(x,y)\\mid2y\\le x^2+y^2\\le2x,\\ y\\ge0\\}$，计算 $I=\\iint_D\\ln\\left(1+\\frac{xy}{x^2+y^2}\\right)\\,\\mathrm{d}x\\,\\mathrm{d}y$。\n\n20\\.（本题满分 12 分）设非负函数 $y=f(x)$（$x\\ge0$）满足 $xf''(x)-f'(x)=-2$，且曲线 $y=f(x)$ 过原点，其与直线 $x=1,y=0$ 围成平面区域 $D$ 的面积为 $2$，求 $y=f(x)$ 及 $D$ 绕 $y$ 轴旋转一周所得旋转体的体积。\n\n21\\.（本题满分 12 分）设 $f(x)$ 在 $(-\\infty,+\\infty)$ 内有二阶连续导数，且对 $\\forall x,y\\in(-\\infty,+\\infty)$，有 $f\\left(\\frac{x+y}{2}\\right)\\le\\frac{f(x)+f(y)}{2}$。\n\n（I）证明：对 $\\forall x\\in(-\\infty,+\\infty)$，有 $f''(x)\\ge0$。  \n（II）若 $f(x)$ 在 $[-1,1]$ 上为非负偶函数，证明：$\\int_{-1}^1f(x)\\,\\mathrm{d}x\\le f(0)+f(1)$。\n\n22\\.（本题满分 12 分）设 $A=\\begin{pmatrix}1&-\\frac12&-\\frac12\\\\1&-\\frac12&-\\frac12\\\\-2&1&1\\end{pmatrix}$。\n\n（I）求一个正交矩阵 $Q=(\\alpha_1,\\alpha_2,\\alpha_3)$，使 $Q^{-1}A^TAQ=\\operatorname{diag}(\\lambda_1,\\lambda_2,\\lambda_3)$，其中 $\\lambda_1\\ge\\lambda_2\\ge\\lambda_3$ 为 $A^TA$ 的特征值。  \n（II）在第（I）问的基础上，若 $P=(\\beta_1,\\beta_2,\\beta_3)$ 为正交矩阵，且 $\\beta_1=\\frac{1}{\\sqrt{\\lambda_1}}A\\alpha_1$，求 $(P^{-1}AQ)^8$。\n\n## 第二套\n\n### 选择题\n\n1\\. 设 $f(x)=\\lim_{n\\to\\infty}\\frac{2x^{2n}-1}{x^{2n}+1}\\sin\\frac1x$，则 $f(x)$ 的第一类间断点的个数为（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $3$\n\n2\\. 设正值函数 $f(x)$ 在 $[0,+\\infty)$ 上有一阶连续的导数，且 $\\lim_{x\\to+\\infty}[f(x)+f'(x)]=0$，则 $y=f(x)$ 一定有渐近线（　）。\n\nA. $y=0$  \nB. $y=\\mathrm{e}$  \nC. $x=0$  \nD. $x=\\mathrm{e}$\n\n3\\. 设 $y=f(x)$ 由 $\\begin{cases}x=2t-|t|,\\\\y=t|\\mathrm{e}^t-1|\\end{cases}$ 确定，则在 $x=0$ 处（　）。\n\nA. $f'(x)$ 不存在  \nB. $f'(x)$ 存在但不连续  \nC. $f'(x)$ 连续但不可导  \nD. $f''(x)$ 存在\n\n4\\. 设 $f(x)$ 在 $x=0$ 处有三阶导数，且 $\\lim_{x\\to0}\\frac{f'(x)}{x^2}=1$，则（　）。\n\nA. $f(0)$ 是 $f(x)$ 的极小值  \nB. $f(0)$ 是 $f(x)$ 的极大值  \nC. $(0,f(0))$ 是 $y=f(x)$ 的拐点  \nD. $(0,f(0))$ 不是 $y=f(x)$ 的拐点\n\n5\\. 设反常积分 $I=\\int_0^{+\\infty}\\left(\\frac{ax}{1+x^2}-\\frac{1}{1+2x}\\right)\\,\\mathrm{d}x$ 收敛，则（　）。\n\nA. $I=\\ln\\frac12$  \nB. $I=\\frac12\\ln2$  \nC. $I=-\\ln\\frac12$  \nD. $I=-\\frac12\\ln2$\n\n6\\. 设 $u=u(x,y)$ 有二阶连续偏导数，且 $\\frac{\\partial^2u}{\\partial x^2}-\\frac{\\partial^2u}{\\partial y^2}+a\\left(\\frac{\\partial u}{\\partial x}+\\frac{\\partial u}{\\partial y}\\right)=0$（$a\\ne0$），若 $u(x,y)=v(x,y)\\mathrm{e}^{\\alpha x+\\beta y}$，使得 $\\frac{\\partial^2v}{\\partial x^2}-\\frac{\\partial^2v}{\\partial y^2}=0$，则（　）。\n\nA. $\\alpha=\\frac a2,\\beta=\\frac a2$  \nB. $\\alpha=-\\frac a2,\\beta=\\frac a2$  \nC. $\\alpha=\\frac a2,\\beta=-\\frac a2$  \nD. $\\alpha=-\\frac a2,\\beta=-\\frac a2$\n\n7\\. 设 $f(x,y)$ 连续，则 $I=\\int_0^{\\frac{\\pi}{2}}\\mathrm{d}\\theta\\int_0^{\\sqrt{\\sin2\\theta}}f(\\theta,r)r\\,\\mathrm{d}r=$（　）。\n\nA. $\\int_0^1\\mathrm{d}r\\int_{\\frac12\\arcsin r^2}^{\\frac{\\pi}{2}-\\frac12\\arcsin r^2}f(\\theta,r)r\\,\\mathrm{d}\\theta$  \nB. $\\int_0^1\\mathrm{d}r\\int_{\\frac12\\arcsin r^2}^{-\\frac12\\arcsin r^2}f(\\theta,r)r\\,\\mathrm{d}\\theta$  \nC. $\\int_0^1\\mathrm{d}r\\int_{-\\frac12\\arcsin r^2}^{\\frac12\\arcsin r^2}f(\\theta,r)r\\,\\mathrm{d}\\theta$  \nD. $\\int_0^1\\mathrm{d}r\\int_{\\frac12\\arcsin r^2}^{\\pi-\\frac12\\arcsin r^2}f(\\theta,r)r\\,\\mathrm{d}\\theta$\n\n8\\. 设向量 $\\boldsymbol\\beta=(a,1,1)^T$ 可由向量组 $\\boldsymbol\\alpha_1=(b,0,1)^T$，$\\boldsymbol\\alpha_2=(1,b-1,1)^T$，$\\boldsymbol\\alpha_3=(1,0,b)^T$ 线性表示，且表示法不唯一，则（　）。\n\nA. $a=-2,b=1$  \nB. $a=-2,b=-1$  \nC. $a=2,b=1$  \nD. $a=2,b=-1$\n\n9\\. 设 $3$ 阶矩阵 $A$ 相似于 $B=\\begin{pmatrix}\\lambda_0&1&0\\\\0&\\lambda_0&0\\\\0&0&\\lambda_0\\end{pmatrix}$，其中 $\\lambda_0$ 是 $A$ 的 $3$ 重特征值，下列命题中正确的个数为（　）。\n\n① $A-\\lambda_0E$ 的非零列向量是 $A$ 属于 $\\lambda_0$ 的特征向量。  \n② $r(A-\\lambda_0E)=1$。  \n③ $r[(A-\\lambda_0E)^2]=0$。  \n④ $r[(A-\\lambda_0E)^3]=0$。\n\nA. $1$  \nB. $2$  \nC. $3$  \nD. $4$\n\n10\\. 设 $A$ 是 $3$ 阶矩阵，$3$ 维列向量 $\\boldsymbol\\alpha$ 不是方程组 $A^2X=0$ 的解，$A\\boldsymbol\\alpha$ 是方程组 $A^2X=0$ 的解，则下列选项正确的是（　）。\n\nA. $\\boldsymbol\\alpha,A\\boldsymbol\\alpha$ 线性相关  \nB. $\\boldsymbol\\alpha,A^2\\boldsymbol\\alpha$ 线性相关  \nC. $A\\boldsymbol\\alpha,A^2\\boldsymbol\\alpha$ 线性相关  \nD. $A\\boldsymbol\\alpha,A^2\\boldsymbol\\alpha$ 线性无关\n\n### 填空题\n\n11\\. 设 $y=f(x)$ 由 $\\int_1^{x+y}\\mathrm{e}^{-t^2}\\,\\mathrm{d}t=x+\\int_0^x x\\sin t^2\\,\\mathrm{d}t$ 确定，则 $\\lim_{n\\to\\infty}n\\left[f\\left(\\frac2n\\right)-1\\right]=$ ______。\n\n12\\. 函数 $f(x)=\\frac{\\mathrm{e}^x(1+\\sin x)}{1+\\cos x}$ 在区间 $\\left[0,\\frac{\\pi}{2}\\right]$ 上的平均值为 ______。\n\n"}
{"chunk_id":"6416c6","wall_time_seconds":0.000011,"exit_code":0,"original_token_count":1638,"output":"ls: /Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/pdf/26.1111.10930/container_tools: No such file or directory\n.github/scripts/release_tex.py:77:        subprocess.run([\"tectonic\", \"--untrusted\", \"--outdir\", str(destination), \"--\", source.name],\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数一_估分10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数一_精编10套模拟卷.pdf.md\nreferences/302模拟27md/2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\nreferences/302模拟27md/2027模考/李艳芳《三套卷》/数学二/【A3试卷版】李艳芳三套卷做题本 .pdf.md\nreferences/302模拟27md/2027模考/李艳芳《三套卷》/数学二/【横版】李艳芳三套卷做题本 .pdf.md\nreferences/302模拟27md/2027模考/李艳芳《三套卷》/数学二/【A4留白版】李艳芳三套卷做题本 .pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数二/27张宇八套卷（数二）.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数二/【横版】数二张宇八套卷.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数二/【A4留白】张宇八套卷-数二（已勘误）.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数一/【A4留白】张宇八套卷.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数一/【横版】数一张宇八套卷.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数一/27张宇八套卷（数一）.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张宇八套卷/数一/【紧凑】张宇八套卷.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按考点/【紧凑版】27张宇八套卷考点分类【数一、数二】.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按考点/【横版】27张宇八套卷【数一、数二】.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按考点/【竖版】27张宇八套卷【数一、数二】.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数二/【竖版】27张宇八套卷做题本数二.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数二/【横版】27张宇八套卷做题本数二.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数二/【紧凑版】27张宇八套卷做题本数二.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数一/【横版】27张宇八套卷做题本数一.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数一/【紧凑版】27张宇八套卷做题本数一.pdf.md\nreferences/302模拟27md/2027模考/张宇《八套卷》/张八考点分类版/按年份/数一/【竖版】27张宇八套卷做题本数一.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【紧凑版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【A4留白版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【A3试卷版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/做题本/【横版】李林《六套卷》数二.pdf.md\nreferences/302模拟27md/2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\nreferences/302模拟27md/2027模考/武忠祥/27考研基础摸底测试（高数、线代）/27考研基础摸底测试（高数、线代）数二.pdf.md\nreferences/302模拟27md/2027模考/武忠祥/27考研基础摸底测试（高数、线代）/27考研基础摸底测试（高数、线代）数一.pdf.md\nreferences/302模拟27md/2027模考/武忠祥/武老师7月摸底测验/【紧凑版】武老师7月摸底小测验.pdf.md\nreferences/302模拟27md/2027模考/武忠祥/武老师7月摸底测验/【A4留白】武老师7月摸底小测验.pdf.md\nreferences/302模拟27md/2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\nreferences/302模拟27md/2027模考/武忠祥/27考研基础摸底测试（高数、线代）数一、数二合卷/27考研基础摸底测试（高数、线代）数一、数二合卷.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/数一答案/24李林四套卷 数一 试题+答案.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf.md\nreferences/302模拟27md/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A3数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A3数一模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A4数一模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/数二答案/【题目+解析】李林四套卷数二清晰版答案(1).pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A4数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷40套整理合集PDF（可高清打印）（仅数二）/试卷/【A4留白】26模拟卷数学二40套精选.pdf.md\nreferences/302模拟27md/模拟卷40套整理合集PDF（可高清打印）（仅数二）/试卷/【紧凑版】26模拟卷数学二40套精选.pdf.md\n"}

## tool · 2026-11-12T13:04:59Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"443970","wall_time_seconds":0.0000115,"exit_code":0,"original_token_count":3948,"output":"3:## 第一套\n7:1\\. 当 $x\\to0$ 时，$ax+bx^2+\\ln(1+x)$ 与 $\\mathrm{e}^{x^2}-\\cos x$ 是等价无穷小，则下列选项正确的是（　）。\n14:2\\. 设 $a,b,k$ 均为不为零的常数，则 $\\lim_{x\\to a}\\frac{f(x)-b}{x-a}=k$ 是 $\\lim_{x\\to a}\\frac{\\mathrm{e}^{f(x)}-\\mathrm{e}^b}{x-a}=k\\mathrm{e}^b$ 的（　）。\n21:3\\. 设 $\\mathrm{e}<x_1<x_2$，则下列不等式成立的是（　）。\n33:4\\. 设 $f(\\alpha)=\\lim_{x\\to0}\\frac{(1+x)^\\alpha-1}{x^\\alpha}$ 有界，$\\alpha\\in\\mathbb{R}$，则 $\\alpha$ 的取值范围为（　）。\n84:11\\. 设 $f(x)$ 在 $x=1$ 处连续，$\\lim_{x\\to1}\\frac{f(x)-5x+2}{\\ln x}=1$，则 $f'(1)=$ ______。\n86:12\\. 已知 $f(x)=\\ln x-a\\sqrt{x}$（$a>0$）在 $x\\in(0,+\\infty)$ 内有唯一零点，则 $a=$ ______。\n88:13\\. 已知 $y=\\int_1^{1+\\sin t}\\left(1+\\mathrm{e}^{\\frac1s}\\right)\\,\\mathrm{d}s$，其中 $t=t(x)$ 由 $\\begin{cases}x=\\cos 2v,\\\\t=\\sin v\\end{cases}$ 确定，则 $\\frac{\\mathrm{d}y}{\\mathrm{d}x}=$ ______。\n98:17\\.（本题满分 10 分）设 $f''(x)$ 在 $x=0$ 处连续，$f'(0)=0$，$f''(0)=1$，求 $\\lim_{x\\to0}\\frac{\\int_0^x\\{f(t)-f[\\ln(1+t)]\\}\\,\\mathrm{d}t}{x^4}$。\n106:21\\.（本题满分 12 分）设 $f(x)$ 在 $(-\\infty,+\\infty)$ 内有二阶连续导数，且对 $\\forall x,y\\in(-\\infty,+\\infty)$，有 $f\\left(\\frac{x+y}{2}\\right)\\le\\frac{f(x)+f(y)}{2}$。\n116:## 第二套\n120:1\\. 设 $f(x)=\\lim_{n\\to\\infty}\\frac{2x^{2n}-1}{x^{2n}+1}\\sin\\frac1x$，则 $f(x)$ 的第一类间断点的个数为（　）。\n127:2\\. 设正值函数 $f(x)$ 在 $[0,+\\infty)$ 上有一阶连续的导数，且 $\\lim_{x\\to+\\infty}[f(x)+f'(x)]=0$，则 $y=f(x)$ 一定有渐近线（　）。\n134:3\\. 设 $y=f(x)$ 由 $\\begin{cases}x=2t-|t|,\\\\y=t|\\mathrm{e}^t-1|\\end{cases}$ 确定，则在 $x=0$ 处（　）。\n141:4\\. 设 $f(x)$ 在 $x=0$ 处有三阶导数，且 $\\lim_{x\\to0}\\frac{f'(x)}{x^2}=1$，则（　）。\n197:11\\. 设 $y=f(x)$ 由 $\\int_1^{x+y}\\mathrm{e}^{-t^2}\\,\\mathrm{d}t=x+\\int_0^x x\\sin t^2\\,\\mathrm{d}t$ 确定，则 $\\lim_{n\\to\\infty}n\\left[f\\left(\\frac2n\\right)-1\\right]=$ ______。\n199:12\\. 函数 $f(x)=\\frac{\\mathrm{e}^x(1+\\sin x)}{1+\\cos x}$ 在区间 $\\left[0,\\frac{\\pi}{2}\\right]$ 上的平均值为 ______。\n201:13\\. 设二阶常系数线性齐次微分方程 $y''+ay'+by=0$ 的通解为 $y=(C_1+C_2x)\\mathrm{e}^x$，则微分方程 $y''+ay'+by=x$ 满足 $y(0)=2,y'(0)=0$ 的特解为 $y=$ ______。\n211:17\\.（本题满分 10 分）设 $f(x)$ 连续，且 $\\lim_{x\\to1}\\frac{f(x)}{x-1}=2$，求 $\\lim_{x\\to0}\\frac{\\int_0^{x^2}\\mathrm{e}^uf\\left(\\mathrm{e}^u-\\mathrm{e}^{x^2}+1\\right)\\,\\mathrm{d}u}{x^2\\ln(\\cos x)}$。\n222:21\\.（本题满分 12 分）设 $f(x)$ 在 $(-\\infty,+\\infty)$ 内二阶可导，且对任意 $h$，有 $f(x+h)+f(x-h)-2f(x)\\ge0$。\n232:## 第三套\n236:1\\. 当 $x\\to0$ 时，$1-\\cos(\\sin x)-\\frac12\\ln(1+x^2)$ 是关于 $x$ 的（　）。\n243:2\\. 设 $f(x)$ 在 $x=1$ 的某邻域内连续，且 $\\lim_{x\\to0}\\frac{\\ln[f(x+1)+\\mathrm{e}^{x^2}]}{x^2}=2$，则 $x=1$ 是 $f(x)$ 的（　）。\n250:3\\. 函数 $f(x)=\\frac{x^2-x}{|x|(x^2-1)}\\mathrm{e}^{\\frac{1}{x-2}}$ 的无穷间断点的个数为（　）。\n257:4\\. 设 $f(x)$ 有二阶连续导数，且 $\\lim_{x\\to0}\\frac{f(x)}x=0$，当 $x>0$ 时满足 $xf''(x)+\\mathrm{e}^{f(x)}\\le6\\ln(1+x)$，则（　）。\n308:11\\. 设 $y=y(x)$ 由 $\\begin{cases}x=\\int_0^t2\\cos(t-s)^2\\,\\mathrm{d}s,\\\\y=x\\sin y+\\mathrm{e}^{2t}\\end{cases}$ 确定，则 $\\left.\\frac{\\mathrm{d}y}{\\mathrm{d}x}\\right|_{t=0}=$ ______。\n310:12\\. $\\lim_{x\\to0}\\frac{\\int_0^x\\left(\\sin t+t^2\\cos\\frac1t\\right)\\,\\mathrm{d}t}{(2+\\sin x)\\int_0^x\\ln(1+t)\\,\\mathrm{d}t}=$ ______。\n312:13\\. 设函数 $f(x)=x^3+3ax^2-ax-1$ 在 $x\\in(-\\infty,+\\infty)$ 内没有极值，则 $a$ 的取值范围为 ______。\n322:17\\.（本题满分 10 分）问是否存在常数 $k$，使得 $x\\to0$ 时，$\\int_0^{2x}|t-x|\\sin t\\,\\mathrm{d}t$ 与 $k|x|^3$ 是等价无穷小？若存在，求 $k$ 的值；若不存在，请说明理由。\n336:21\\.（本题满分 12 分）设 $f(x)$ 满足 $(1-x)f'(x)+nf(x)=n(1-x)^{n+1}$（$n$ 为正整数），且 $f(0)=0$。\n347:## 第四套\n351:1\\. 设常数 $a,b$ 使得 $\\lim_{x\\to+\\infty}(x\\arctan x-ax-b)=0$，则（　）。\n358:2\\. 已知反常积分 $\\int_0^{+\\infty}\\frac{\\mathrm{e}^x-1}{x^\\alpha\\cdot\\mathrm{e}^x}\\,\\mathrm{d}x$ 收敛，则下列选项正确的是（　）。\n365:3\\. $f(x)=\\begin{cases}2^x,&x\\le0,\\\\\\cos x+x^2,&x>0,\\end{cases}$ 的一个原函数为（　）。\n372:4\\. 设 $f(x)$ 在 $[0,1]$ 上有连续的导数，且 $f(0)=0,f(1)=1$，则下列选项正确的是（　）。\n428:11\\. 曲线 $x=2y-y^2$ 上各点处的曲率的最大值为 ______。\n430:12\\. 设 $f(x)=\\ln\\sqrt{\\frac{1-x}{1+x}}$，则 $f^{(2n+1)}(0)=$ ______。\n432:13\\. $\\int_0^1\\mathrm{d}y\\int_0^{1-\\sqrt{2y-y^2}}\\frac1{\\sqrt{2-x}}\\,\\mathrm{d}x=$ ______。\n442:17\\.（本题满分 10 分）设 $F(x)=\\frac{\\int_0^{x^2}\\ln(1+t^2)\\,\\mathrm{d}t}{x^\\alpha}$，且 $\\lim_{x\\to+\\infty}F(x)=\\lim_{x\\to0^+}F(x)=0$，求 $\\alpha$ 的取值范围。\n453:21\\.（本题满分 12 分）经过曲线 $y=y(x)$（$y$ 不为常函数）上点 $P(x,y)$ 作 $x$ 轴垂线交于点 $M(x,0)$，曲线上点 $P(x,y)$ 处的切线为 $l$，已知点 $M$ 到切线 $l$ 的距离等于 $1$，且 $y(0)=1$。\n463:## 第五套\n467:1\\. 设 $f(x),g(x)$ 均是连续函数，当 $x\\to0$ 时，$f(x)$ 和 $g(x)$ 都与 $x$ 是等价无穷小，$F(x)=\\int_1^2xf(xt)\\,\\mathrm{d}t$，$G(x)=\\int_0^x g(2x-t)\\,\\mathrm{d}t$。则当 $x\\to0$ 时，$F(x)$ 是 $G(x)$ 的（　）。\n474:2\\. 设 $f(x)$ 为连续函数，且 $\\lim_{x\\to1}\\frac{f(2x-1)}{x-1}=2$，则 $\\lim_{x\\to0}\\frac{f[(1+\\sin x)^2]-f(1+\\sin x)}x=$（　）。\n481:3\\. 设可导函数 $y=f(x)$ 在 $[a,b]$ 上严格单调递增，$g(y)$ 是 $f(x)$ 的反函数，则 $\\int_a^b f(x)\\,\\mathrm{d}x+\\int_{f(a)}^{f(b)}g(y)\\,\\mathrm{d}y=$（　）。\n488:4\\. 设积分 $\\int_1^{+\\infty}\\frac{\\arctan(x-1)}{(x-1)^p}\\,\\mathrm{d}x$ 收敛，则下列选项正确的是（　）。\n539:11\\. 设 $\\lim_{x\\to\\infty}\\left(\\frac{ax^2}{1+x}-bx-1\\right)=\\lim_{x\\to\\infty}[f(x+1)-f(x)]$，且 $\\lim_{x\\to\\infty}f'(x)=0$，则曲线 $y=\\frac{ax^2}{1+x}$ 的斜渐近线方程为 ______。\n541:12\\. 设函数 $f(x,y)=\\begin{cases}(x^2+y^2)^a\\sin\\frac{1}{x^2+y^2},&(x,y)\\ne(0,0),\\\\0,&(x,y)=(0,0),\\end{cases}$ 在点 $(0,0)$ 处可微，则 $a$ 的取值范围为 ______。\n543:13\\. 设 $f(x)$ 可导，且对任意的 $t$，都有 $\\lim_{x\\to t}\\frac{xf(t)-tf(x)}{x-t}=t^2\\mathrm{e}^t$，则 $f(x)=$ ______。\n553:17\\.（本题满分 10 分）设 $f(x)=\\int_x^{x^2}\\left(1+\\frac1{2t}\\right)^t\\sin\\frac1{\\sqrt{t}}\\,\\mathrm{d}t$（$x>0$），求 $\\lim_{n\\to\\infty}f(n)\\sin\\frac1n$。\n568:21\\.（本题满分 12 分）设二阶线性微分方程 $(1-x^2)\\frac{\\mathrm{d}^2y}{\\mathrm{d}x^2}+\\left(2\\sqrt{1-x^2}-x\\right)\\frac{\\mathrm{d}y}{\\mathrm{d}x}+y=2x$。\n578:## 第六套\n582:1\\. 已知 $\\lim_{x\\to+\\infty}\\frac1{x^a}\\int_0^{x^2}\\sqrt{1+t^4}\\,\\mathrm{d}t=b$，其中 $a$ 为大于零的常数，$b$ 为非零常数，则（　）。\n589:2\\. 已知曲线 $y=ax(b-x)$（$a>0,b>0$）与 $xy=1$ 在第一象限内有公切线，两曲线在切点相交，则 $y=ax(b-x)$ 与 $x$ 轴在第一象限围成图形的面积为（　）。\n596:3\\. 设 $F(x,y)=\\frac{x-y}{\\sqrt{1+x^2}}\\mathrm{e}^{x+f(x)y}$，其中 $f(x)$ 连续，且 $\\lim_{x\\to1}f(x)=1$，则 $F'_x(1,1)+F'_y(1,1)=$（　）。\n603:4\\. 设反常积分 $I=\\int_3^{+\\infty}\\frac{\\mathrm{d}x}{(x-1)(\\ln x)^a}$（$a>0$）收敛，则 $a$ 的取值范围为（　）。\n659:11\\. 曲线 $y=\\int_0^x\\sqrt{\\sin t}\\,\\mathrm{d}t$ 在 $x\\in[0,\\pi]$ 上的弧长为 ______。\n661:12\\. 设摆线 $\\begin{cases}x=t-\\sin t,\\\\y=1-\\cos t,\\end{cases}\\quad t\\in(0,2\\pi)$，则该曲线的最小曲率为 ______。\n663:13\\. 设 $D=\\left\\{(\\theta,r)\\mid\\arctan\\frac14\\le\\theta\\le\\frac\\pi4,\\frac1{\\sqrt{\\sin\\theta\\cos\\theta}}\\le r\\le\\frac2{\\cos\\theta}\\right\\}$，则 $I=\\iint_Dr^3\\cos^2\\theta\\,\\mathrm{d}\\theta\\,\\mathrm{d}r=$ ______。\n673:17\\.（本题满分 10 分）已知当 $x\\to0$ 时，$a\\sin x+bx^2+\\ln(1-2x+x^2)$ 与 $1-\\mathrm{e}^{5x^2}$ 是等价无穷小，求 $a,b$ 的值。\n684:21\\.（本题满分 12 分）设 $f(x)$ 在 $[-1,1]$ 上有连续的二阶导数。\n# 27考研基础摸底测试（高数、线代）数二\n\n### 选择题\n\n1\\. 当 $x\\to0$ 时，$f(x)=x-\\sin ax$ 与 $g(x)=x^2\\ln(1-bx)$ 是等价无穷小，则（　）。\n\nA. $a=1,\\ b=-\\frac16$\n\nB. $a=1,\\ b=\\frac16$\n\nC. $a=-1,\\ b=-\\frac16$\n\nD. $a=-1,\\ b=\\frac16$\n\n2\\. 函数 $f(x)=\\frac{x-x^3}{\\sin\\pi x}$ 的可去间断点的个数为（　）。\n\nA. $1$\n\nB. $2$\n\nC. $3$\n\nD. 无穷多个\n\n3\\. 使不等式 $\\int_1^x\\frac{\\sin t}{t}\\,\\mathrm dt>\\ln x$ 成立的 $x$ 的范围是（　）。\n\nA. $(0,1)$\n\nB. $\\left(1,\\frac\\pi2\\right)$\n\nC. $\\left(\\frac\\pi2,\\pi\\right)$\n\nD. $(\\pi,+\\infty)$\n\n4\\. 若 $f''(x)$ 不变号，且曲线 $y=f(x)$ 在点 $(1,1)$ 上的曲率圆为 $x^2+y^2=2$，则函数 $f(x)$ 在区间 $(1,2)$ 内（　）。\n\nA. 有极值点，无零点\n\nB. 无极值点，有零点\n\nC. 有极值点，有零点\n\nD. 无极值点，无零点\n\n5\\. 设函数 $y=f(x)$ 在区间 $[-1,3]$ 上的图形为：$-1\\le x<0$ 时为高度 $1$ 的水平线段，$x$ 从 $0$ 到 $2$ 时，曲线从 $(0,-1)$ 上升，经过 $(1,0)$ 到达 $(2,2)$，$2$ 右侧至 $3$ 为 $x$ 轴上的线段。则函数 $F(x)=\\int_0^x f(t)\\,\\mathrm dt$ 的图形为（　）。\n\nA. 左侧为从 $(-1,1)$ 下降到原点的直线段，右侧曲线在 $x=1$ 处取负的最小值，上升到 $x=2$ 后在正高度处保持水平。\n\nB. 左侧为从 $(-1,-1)$ 上升到原点的直线段，右侧曲线在 $x=1$ 处取负的最小值，上升到 $x=2$ 时跳至横轴，随后沿横轴延伸。\n\nC. 左侧为从 $(-1,0)$ 上升到 $(0,1)$ 的直线段，右侧曲线在 $x=1$ 附近取正的最小值，上升到 $x=2$ 后在正高度处保持水平。\n\nD. 左侧为从 $(-1,-1)$ 上升到原点的直线段，右侧曲线在 $x=1$ 处取负的最小值，上升到 $x=2$ 后在正高度处保持水平。\n\n6\\. 设函数 $z=f(x,y)$ 的全微分为 $\\mathrm dz=x\\,\\mathrm dx+y\\,\\mathrm dy$，则点 $(0,0)$（　）。\n\nA. 不是 $f(x,y)$ 的连续点\n\nB. 不是 $f(x,y)$ 的极值点\n\nC. 是 $f(x,y)$ 的极大值点\n\nD. 是 $f(x,y)$ 的极小值点\n\n7\\. 正方形 $\\{(x,y)\\mid |x|\\le1,\\ |y|\\le1\\}$ 被其对角线划分为四个区域 $D_k$（$k=1,2,3,4$），图中 $D_1,D_2,D_3,D_4$ 分别在原点的上、左、下、右侧。设 $I_k=\\iint_{D_k}y\\cos x\\,\\mathrm dx\\,\\mathrm dy$，则 $\\max_{1\\le k\\le4}\\{I_k\\}=$（　）。\n\nA. $I_1$\n\nB. $I_2$\n\nC. $I_3$\n\nD. $I_4$\n\n8\\. 设函数 $f(x,y)$ 连续，则\n\n$$\n\\int_1^2\\mathrm dx\\int_x^2 f(x,y)\\,\\mathrm dy\n+\\int_1^2\\mathrm dy\\int_y^{4-y} f(x,y)\\,\\mathrm dx=\n$$\n\nA. $\\int_1^2\\mathrm dx\\int_1^{4-x} f(x,y)\\,\\mathrm dy$\n\nB. $\\int_1^2\\mathrm dx\\int_x^{4-x} f(x,y)\\,\\mathrm dy$\n\nC. $\\int_1^2\\mathrm dy\\int_1^{4-y} f(x,y)\\,\\mathrm dx$\n\nD. $\\int_1^2\\mathrm dy\\int_y^2 f(x,y)\\,\\mathrm dx$\n\n9\\. 设 $\\boldsymbol A,\\boldsymbol B$ 均为 2 阶矩阵，$\\boldsymbol A^*,\\boldsymbol B^*$ 分别为 $\\boldsymbol A,\\boldsymbol B$ 的伴随矩阵。若 $|\\boldsymbol A|=2$，$|\\boldsymbol B|=3$，则分块矩阵 $\\begin{pmatrix}\\boldsymbol O&\\boldsymbol A\\\\\\boldsymbol B&\\boldsymbol O\\end{pmatrix}$ 的伴随矩阵为（　）。\n\nA. $\\begin{pmatrix}\\boldsymbol O&3\\boldsymbol B^*\\\\2\\boldsymbol A^*&\\boldsymbol O\\end{pmatrix}$\n\nB. $\\begin{pmatrix}\\boldsymbol O&2\\boldsymbol B^*\\\\3\\boldsymbol A^*&\\boldsymbol O\\end{pmatrix}$\n\nC. $\\begin{pmatrix}\\boldsymbol O&3\\boldsymbol A^*\\\\2\\boldsymbol B^*&\\boldsymbol O\\end{pmatrix}$\n\nD. $\\begin{pmatrix}\\boldsymbol O&2\\boldsymbol A^*\\\\3\\boldsymbol B^*&\\boldsymbol O\\end{pmatrix}$\n\n10\\. 设 $\\boldsymbol A,\\boldsymbol P$ 均为 3 阶矩阵，$\\boldsymbol P^T$ 为 $\\boldsymbol P$ 的转置矩阵，且 $\\boldsymbol P^T\\boldsymbol A\\boldsymbol P=\\begin{pmatrix}1&0&0\\\\0&1&0\\\\0&0&2\\end{pmatrix}$。若 $\\boldsymbol P=(\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\boldsymbol\\alpha_3)$，$\\boldsymbol Q=(\\boldsymbol\\alpha_1+\\boldsymbol\\alpha_2,\\boldsymbol\\alpha_2,\\boldsymbol\\alpha_3)$，则 $\\boldsymbol Q^T\\boldsymbol A\\boldsymbol Q$ 为（　）。\n\nA. $\\begin{pmatrix}2&1&0\\\\1&1&0\\\\0&0&2\\end{pmatrix}$\n\nB. $\\begin{pmatrix}1&1&0\\\\1&2&0\\\\0&0&2\\end{pmatrix}$\n\nC. $\\begin{pmatrix}2&0&0\\\\0&1&0\\\\0&0&2\\end{pmatrix}$\n\nD. $\\begin{pmatrix}1&0&0\\\\0&2&0\\\\0&0&2\\end{pmatrix}$\n\n### 填空题\n\n11\\. 设 $y=y(x)$ 是由方程 $xy+e^y=x+1$ 确定的隐函数，则 $\\left.\\frac{\\mathrm d^2y}{\\mathrm dx^2}\\right|_{x=0}=$ ______。\n\n12\\. 曲线 $\\begin{cases}x=\\int_0^{1-t}e^{-u^2}\\,\\mathrm du,\\\\ y=t^2\\ln(2-t^2)\\end{cases}$ 在 $(0,0)$ 处的切线方程为 ______。\n\n13\\. 函数 $y=x^{2x}$ 在区间 $(0,1]$ 上的最小值为 ______。\n\n14\\. 已知 $\\int_{-\\infty}^{+\\infty}e^{k|x|}\\,\\mathrm dx=1$，则 $k=$ ______。\n\n15\\. $\\lim_{n\\to\\infty}\\int_0^1e^{-x}\\sin nx\\,\\mathrm dx=$ ______。\n\n16\\. 设 $\\boldsymbol\\alpha,\\boldsymbol\\beta$ 为 3 维列向量，$\\boldsymbol\\beta^T$ 为 $\\boldsymbol\\beta$ 的转置。若矩阵 $\\boldsymbol\\alpha\\boldsymbol\\beta^T$ 相似于 $\\begin{pmatrix}2&0&0\\\\0&0&0\\\\0&0&0\\end{pmatrix}$，则 $\\boldsymbol\\beta^T\\boldsymbol\\alpha=$ ______。\n\n### 解答题\n\n17\\. （10 分）求极限 $\\lim_{x\\to0}\\frac{(1-\\cos x)[x-\\ln(1+\\tan x)]}{\\sin^4 x}$。\n\n18\\. （12 分）设非负函数 $y=y(x)$（$x\\ge0$）满足微分方程 $xy''-y'+2=0$。当曲线 $y=y(x)$ 过原点时，其与直线 $x=1$ 及 $y=0$ 围成平面区域 $D$ 的面积为 $2$。求 $D$ 绕 $y$ 轴旋转所得旋转体体积。\n\n19\\. （12 分）设 $y=y(x)$ 是区间 $(-\\pi,\\pi)$ 内过 $\\left(-\\frac{\\pi}{\\sqrt2},\\frac{\\pi}{\\sqrt2}\\right)$ 的光滑曲线。当 $-\\pi<x<0$ 时，曲线上任一点处的法线都过原点；当 $0\\le x<\\pi$ 时，函数 $y(x)$ 满足 $y''+y+x=0$。求 $y(x)$ 的表达式。\n\n20\\. （12 分）计算二重积分 $\\iint_D(x-y)\\,\\mathrm dx\\,\\mathrm dy$，其中 $D=\\{(x,y)\\mid(x-1)^2+(y-1)^2\\le2,\\ y\\ge x\\}$。\n\n21\\. （12 分）设\n\n$$\n\\boldsymbol A=\\begin{pmatrix}1&-1&-1\\\\-1&1&1\\\\0&-4&-2\\end{pmatrix},\n\\quad \\boldsymbol\\xi_1=\\begin{pmatrix}-1\\\\1\\\\-2\\end{pmatrix}.\n$$\n\n（I）求满足 $\\boldsymbol A\\boldsymbol\\xi_2=\\boldsymbol\\xi_1$，$\\boldsymbol A^2\\boldsymbol\\xi_3=\\boldsymbol\\xi_1$ 的所有向量 $\\boldsymbol\\xi_2,\\boldsymbol\\xi_3$；\n\n（II）对（I）中的任意向量 $\\boldsymbol\\xi_2,\\boldsymbol\\xi_3$，证明 $\\boldsymbol\\xi_1,\\boldsymbol\\xi_2,\\boldsymbol\\xi_3$ 线性无关。\n\n22\\. （12 分）设二次型\n\n$$\nf(x_1,x_2,x_3)=ax_1^2+ax_2^2+(a-1)x_3^2+2x_1x_3-2x_2x_3.\n$$\n\n（I）求二次型 $f$ 的矩阵的所有特征值；\n\n（II）若二次型 $f$ 的规范形为 $y_1^2+y_2^2$，求 $a$ 的值。\n# 【紧凑版】武老师7月摸底小测验\n\n1\\. 曲线 $y=\\frac{1}{x^2}+\\ln(1+e^x)$ 的渐近线条数为（　）。\n\nA. $0$\n\nB. $1$\n\nC. $2$\n\nD. $3$\n\n2\\. 设 $D=\\{(x,y)\\mid x^2+y^2\\le 2x+2y\\}$，则 $\\iint_D(x+y^2)\\,\\mathrm d\\sigma=$（　）。\n\nA. $3\\pi$\n\nB. $\\left(2+\\frac{2\\sqrt 2}{3}\\right)\\pi$\n\nC. $\\left(4+\\frac{2\\sqrt 2}{3}\\right)\\pi$\n\nD. $5\\pi$\n\n3\\. 设 $f(x)$ 连续且 $f(x)=1+\\int_0^x f^3(t)\\,\\mathrm dt$，则 $f^{(n)}(0)=$ ______。\n\n4\\. 设 $V(a)$ 是由曲线 $y=xe^{-x}$（$x\\ge 0$）、$y=0$、$x=a$ 所围图形绕 $Ox$ 轴旋转一周的立体的体积，则 $\\lim_{a\\to+\\infty}V(a)=$ ______。\n\n5\\. 已知 $y_1=\\cos 2x-\\frac14x\\cos 2x$、$y_2=\\sin 2x-\\frac14x\\cos 2x$ 是某二阶常系数非齐次微分方程的两个解，$y_3=\\cos 2x$ 是它所对应的齐次方程的一个解，则该微分方程是 ______。\n\n6\\. 已知 $y_1=\\cos 2x-\\frac14x\\cos 2x$、$y_2=\\sin 2x-\\frac14x\\cos 2x$ 是某二阶常系数非齐次微分方程的两个解，$y_3=\\cos 2x$ 是它所对应的齐次方程的一个解，则该微分方程是 ______。\n\n7\\. 计算二重积分\n\n$$\n\\iint_D \\left[3x^2\\ln\\left(y+\\sqrt{1+y^2}\\right)+6x+9+y^2\\right]\\,\\mathrm d\\sigma,\n$$\n\n其中区域 $D=\\{(x,y)\\mid x^2+y^2\\le 2x\\}$。\n"}
{"chunk_id":"964fe3","wall_time_seconds":0.000017541,"exit_code":0,"original_token_count":2787,"output":"3:## 卷一\n7:1\\. 曲线 $y=(x+2)e^{1/x}$ 的渐近线的条数为（　）。\n14:2\\. 设函数 $f(x)$ 可导，$F(x)=f(x)[1-|\\ln(1+x)|]$，则（　）。\n21:3\\. 设线性无关的函数 $y_1,y_2,y_3$ 都是二阶非齐次线性微分方程 $y''+p(x)y'+q(x)y=f(x)$ 的解，$C_1,C_2$ 是任意常数，则该非齐次方程的通解是（　）。\n28:4\\. 设 $u=f(x^2,y^2,xyz)$，函数 $z=g(x,y)$ 由方程 $\\int_{e^{xy}}^z\\varphi(e^{xy}+z-t)\\,\\mathrm dt=xyz$ 确定，其中 $f$ 可微，$\\varphi$ 连续，且满足 $\\varphi(z)-xy\\ne0$，则 $x\\frac{\\partial u}{\\partial x}-y\\frac{\\partial u}{\\partial y}=$（　）。\n79:11\\. $\\lim_{x\\to0}\\left(\\frac{e^x-1}{\\sin x}\\right)^{\\cot x}=$ ______。\n81:12\\. $\\int\\sqrt{\\frac{e^x-1}{e^x+1}}\\,\\mathrm dx=$ ______。\n83:13\\. 设连续函数 $y=f(x)$ 在区间 $[0,2]$ 上满足 $f(x)+f(2-x)=0$，则 $\\int_0^\\pi f(1+\\cos x)\\,\\mathrm dx=$ ______。\n93:17\\.（本题满分 10 分）求函数 $f(x,y)=(y-x)(y-x^2)$ 的极值。\n104:21\\.（本题满分 12 分）已知平面区域 $D=\\{(x,y)\\mid |y|\\le x\\le\\pi-|y|\\}$，计算 $\\iint_D\\sin(x+y)\\,\\mathrm dx\\,\\mathrm dy$。\n111:## 卷二\n115:1\\. 设函数 $f(x)$ 有二阶连续导数，$\\lim_{x\\to0}\\frac{f(x)}{\\int_0^{x^2}\\frac{\\sin t}{t}\\,\\mathrm dt}=-1$，则（　）。\n122:2\\. 已知函数 $f(x,y)=\\frac{e^y}{y-x}$，则（　）。\n129:3\\. 设数列 $\\{a_n\\}$ 满足 $\\lim_{n\\to\\infty}(a_{n+1}-a_n)=0$，下面结论中正确的是（　）。\n136:4\\. 曲线 $y=\\int_0^x xte^{-t^2}\\,\\mathrm dt$ 的渐近线条数为（　）。\n194:11\\. $\\int_1^{+\\infty}\\frac{\\ln x}{(1+x)^2}\\,\\mathrm dx=$ ______。\n196:12\\. 曲线 $\\begin{cases}x=\\frac{2t+t^2}{1+t^3},\\\\y=\\frac{2t-t^2}{1+t^3}\\end{cases}$ 在 $t=1$ 对应点处的法线方程为 ______。\n198:13\\. 设连续单增函数 $f(x)$ 满足 $\\int_{+\\infty}^{x}\\frac{\\mathrm dt}{f(t)}\\cdot\\int_{-\\infty}^{x}f(t)\\,\\mathrm dt=-1$ 且 $f(0)=1$，则 $f(x)=$ ______。\n225:17\\.（本题满分 10 分）求 $\\lim_{x\\to0}\\left(1+\\frac1{x^2}-\\frac1{x^3}\\ln\\frac{2+x}{2-x}\\right)$。\n244:21\\.（本题满分 12 分）设函数 $f(x)$ 在 $[0,+\\infty)$ 上连续，且满足\n257:## 卷三\n261:1\\. 设 $f(x)=\\int_0^{|\\sin x|}e^{t^2}\\,\\mathrm dt$，$g(x)=\\int_0^{|x|}\\sin t^2\\,\\mathrm dt$，则在 $(-\\pi,\\pi)$ 内（　）。\n268:2\\. 设函数 $f(x)$ 在 $[-\\pi,\\pi]$ 上连续，当 $F(a)=\\int_{-\\pi}^{\\pi}[f(x)-a\\cos nx]^2\\,\\mathrm dx$（$n\\in\\mathbb N_+$）取得极小值时，$a=$（　）。\n275:3\\. 设 $p>0$，$\\int_2^{+\\infty}\\frac{\\mathrm dx}{(\\ln x)^{(\\ln x)^p}}$ 收敛，则 $p$ 的取值范围是（　）。\n282:4\\. 设函数 $u=u(x,y)$ 具有二阶连续偏导数，函数 $F(s,t)$ 具有一阶连续偏导数，且 $\\left(\\frac{\\partial F}{\\partial s}\\right)^2+\\left(\\frac{\\partial F}{\\partial t}\\right)^2\\ne0$，$F\\left(\\frac{\\partial u}{\\partial x},\\frac{\\partial u}{\\partial y}\\right)=0$，则有（　）。\n339:11\\. 已知函数 $f(x)=\\int_1^{x^2}\\frac{\\sin t}{1+t}\\,\\mathrm dt$（$0<x<\\sqrt\\pi$），$f$ 的反函数为 $g$，则 $g'(0)=$ ______。\n341:12\\. 已知 $\\int_{-\\infty}^{+\\infty}(|x|+ax)e^{-x}\\,\\mathrm dx=2$，则 $a$ 的取值范围是 ______。\n343:13\\. 设 $f(x)=\\int_1^{2x}\\ln(t^2-1)\\,\\mathrm dt$（$x>\\frac12$），则当 $n>1$ 时，$f^{(n)}(x)=$ ______。\n353:17\\.（本题满分 10 分）求 $\\int\\frac{2x^2+2x+13}{(x-2)(1+x^2)^2}\\,\\mathrm dx$。\n364:21\\.（本题满分 12 分）设平面区域 $D$ 由 $x$ 轴、$y=x$、$\\sqrt x+\\sqrt y=1$ 及 $\\sqrt x+\\sqrt y=2$ 所围成，计算 $\\iint_D\\frac{(\\sqrt x+\\sqrt y)^4}{x^2}\\,\\mathrm dx\\,\\mathrm dy$。\n372:## 卷四\n376:1\\. 设 $z=f(x,y)$ 具有二阶连续偏导数，$x=u$，$y^2=v-u^2$。以 $u,v$ 为新的自变量变换方程 $y\\frac{\\partial z}{\\partial x}-x\\frac{\\partial z}{\\partial y}=0$（$y\\ne0$），得到（　）。\n383:2\\. 已知 $f(x)=e^{|x|}$，则 $f(x)$ 的原函数为（　）。\n390:3\\. 以 $y=x$ 与 $y=xe^{-2x}$ 为特解的最低阶常系数齐次线性微分方程为（　）。\n397:4\\. 已知 $F(x,y,z)=f(\\pi y-\\sqrt2z)-e^{2x-z}$，其中 $f$ 可微。若 $aF'_x+bF'_y+cF'_z=0$，则 $(a,b,c)$ 可以是（　）。\n455:11\\. $\\int_{1/2}^{3/4}\\frac{\\arcsin\\sqrt x}{\\sqrt{x(1-x)}}\\,\\mathrm dx=$ ______。\n457:12\\. 设非负连续函数 $f(x)$ 满足 $f(x)\\int_0^1 f(t)\\,\\mathrm dt=2x^2$，则 $f(x)$ 在区间 $[0,2]$ 上的平均值是 ______。\n459:13\\. $\\lim_{x\\to0}\\frac1{x^2}\\left(\\frac1{x^2+1}-\\cos x\\right)=$ ______。\n469:17\\.（本题满分 10 分）设函数 $y(x)$ 是微分方程 $y'+\\frac1{2\\sqrt x}y=\\frac{\\sqrt x}2+1$ 满足 $y(1)=2$ 的解，求曲线 $y=y(x)$ 的渐近线。\n480:21\\.（本题满分 12 分）设 $D=\\{(x,y)\\mid x^2+y^2\\le2(x+y)\\}$，计算 $\\iint_D(x^2+x+y)\\,\\mathrm dx\\,\\mathrm dy$。\n487:## 卷五\n491:1\\. 设 $g(x)$ 在 $x=0$ 的某邻域内连续，$f(x)$ 具有一阶连续导数，且满足 $\\lim_{x\\to0}\\frac{g(x)}x=-3$，$f'(x)=\\ln(1+x^2)-x\\int_0^1g(xt)\\,\\mathrm dt$，则（　）。\n498:2\\. 设 $f(x,y)=\\begin{cases}x\\cos\\frac1y+y\\cos\\frac1x,&xy\\ne0,\\\\0,&xy=0,\\end{cases}$ 考察以下三个结论。\n511:3\\. 设函数 $f(x)$ 在区间 $[a,b]$ 上可积，考察以下四个结论。\n525:4\\. 设 $D$ 是由 $x^2+y^2=ax$ 与 $x^2+y^2=ay$（$a>0$）所围成的位于第一象限的平面有界区域，$f(x,y)$ 是 $D$ 上的连续函数，则 $\\iint_D f(x,y)\\,\\mathrm dx\\,\\mathrm dy=$（　）。\n576:11\\. $\\lim_{x\\to0}\\frac1x\\left(\\frac{\\sqrt{1+x^2}}{\\sin x}-\\cot x\\right)=$ ______。\n578:12\\. 曲线 $\\begin{cases}x=\\int_0^t e^{-u^2}\\,\\mathrm du,\\\\y=te^{-t^2}+\\int_0^t e^{-u^2}\\,\\mathrm du\\end{cases}$ 在其拐点处的法线方程为 ______。\n580:13\\. 设 $y(x)$ 是微分方程 $xy'-y=-9x^4+6x^2$（$x>0$）满足条件 $y(1)=3$ 的解，则曲线 $y=y(x)$ 的凹区间为 ______。\n590:17\\.（本题满分 10 分）设\n610:21\\.（本题满分 12 分）设函数 $p_1(x),p_2(x)$ 连续，$y_1(x),y_2(x)$ 是二阶齐次线性微分方程 $y''+p_1(x)y'+p_2(x)y=0$ 的两个线性无关的解，记 $W(x)=y_1y_2'-y_2y_1'$。证明：\n622:## 卷六\n626:1\\. $\\lim_{n\\to\\infty}\\frac1n\\sum_{i=1}^n\\int_1^{i/n}\\frac{\\sin x}{x}\\,\\mathrm dx=$（　）。\n633:2\\. 设函数 $f(x)$ 与 $g(x)$ 满足 $f(x_0)=g(x_0)$，$f'(x_0)<g'(x_0)$，则必存在 $\\delta>0$，使得（　）。\n640:3\\. 设方程 $y''+ay'+y=(x+1)e^{bx}$ 的每一个解 $y=y(x)$ 在区间 $[0,+\\infty)$ 上均有界，则实数 $a,b$ 满足（　）。\n647:4\\. 若\n709:11\\. $\\lim_{x\\to0}\\left(\\frac{2+x}{\\sin x}-\\frac2x\\right)=$ ______。\n711:12\\. 设可微函数 $f(x)$ 及其反函数 $g(x)$ 满足关系式 $\\int_1^{f(x)}g(t)\\,\\mathrm dt=\\frac13(x^{3/2}-8)$（$x>0$），则 $f(x)=$ ______。\n713:13\\. 若 $\\begin{cases}x=\\ln t,\\\\y=e^{t^2},\\end{cases}$ 则 $\\left.\\frac{\\mathrm d^2y}{\\mathrm dx^2}\\right|_{t=1}=$ ______。\n723:17\\.（本题满分 10 分）求曲线 $y=\\frac{1+\\int_0^{1/x}e^{t^2}\\,\\mathrm dt}{1-e^{1/x}}$（$x>0$）的斜渐近线。\n737:21\\.（本题满分 12 分）已知可微函数 $f(u,v)$ 满足\n753:## 卷七\n757:1\\. 曲线 $y=\\frac{e^x+1}{2e^x-1}$（　）。\n764:2\\. 若二元函数 $f(x,y)$ 与 $g(x,y)$ 在点 $P_0(x_0,y_0)$ 的某邻域内有定义，$f(x,y)$ 在点 $P_0$ 处可微且 $f(x_0,y_0)=0$，$g(x,y)$ 在点 $P_0$ 处连续但不可微。考察下列 4 个函数。\n780:3\\. 反常积分 ① $\\int_0^{+\\infty}\\frac{|\\sin x|}{\\sqrt{x^3}}\\,\\mathrm dx$、② $\\int_0^{+\\infty}\\frac{1}{1+\\sqrt x|\\sin x|}\\,\\mathrm dx$ 的敛散性为（　）。\n787:4\\. 设平面 $D$ 是由曲线 $y=\\ln x$、直线 $x=1$、$y=1$ 围成的第一象限的有界区域，记 $D$ 绕 $x$ 轴与绕 $y=1$ 旋转一周所得旋转体体积分别为 $V_1,V_2$，则（　）。\n844:11\\. $\\int\\frac{e^x(1-x)}{(x-e^x)^2}\\,\\mathrm dx=$ ______。\n846:12\\. 如果曲线 $y=e^x+ax^3$ 有拐点，则 $a$ 的取值范围为 ______。\n848:13\\. 质点在第一象限沿曲线 $y=x^{3/2}$ 远离原点。已知质点与原点的距离以 $11\\,\\mathrm{cm/s}$ 的变化率增加，则当质点运动到 $x=3\\,\\mathrm{cm}$ 时的水平速度为 ______。\n858:17\\.（本题满分 10 分）设 $f(x)$ 在 $x=0$ 的某邻域内连续，在 $x=0$ 处可导，且 $f(0)=0$，\n891:21\\.（本题满分 12 分）设函数 $f(x)$ 在 $[0,2]$ 上连续，在 $(0,2)$ 内二阶可导，$f''(x)>0$，且 $f(0)=1,f'(1)=0$。又曲线 $y=f(x)$ 上任一点 $(x,y)$ 处的曲率半径恒等于 $1$，$D$ 是由 $y=f(x)$ 与 $y=1$ 所围成的平面有界区域。\n901:## 卷八\n905:1\\. 设函数 $f(x)$ 在区间 $(-1,1)$ 内有定义，且在点 $x=0$ 处连续。考察以下结论。\n918:2\\. 三元方程 $e^{z+1}+xy+yz+zx=0$ 在点 $(1,1,-1)$ 的某个邻域内必能确定的隐函数为（　）。\n925:3\\. 设函数 $f(x)$ 在 $(0,+\\infty)$ 上可导，给出下列命题。\n939:4\\. 已知函数 $f(x),g(x)$ 可导，且 $f'(x)>0$，$g'(x)<0$，则（　）。\n990:11\\. 设 $f'(a)=1$，其中 $a>0$，则 $\\lim_{x\\to a}\\frac{x[f(x)-f(a)]}{\\ln x-\\ln a}=$ ______。\n992:12\\. 设 $y=e^{3x}+xe^{2x}+1$ 与 $y=e^{3x}-1$ 是某三阶常系数非齐次线性微分方程的两个特解，则该微分方程为 ______。\n994:13\\. 函数 $f(x)=\\int_0^x\\frac1{1-\\sin t}\\,\\mathrm dt$ 在区间 $\\left[-\\frac\\pi4,\\frac\\pi4\\right]$ 上的取值范围为 ______。\n1004:17\\.（本题满分 10 分）已知函数 $f(x)$ 在 $x=0$ 处具有一阶导数，且 $\\lim_{x\\to0}\\frac{xf(x)+e^{x^2}\\sin x}{x^2}=1$。求曲线 $y=f(x)$ 在 $x=0$ 处的切线方程。\n1018:21\\.（本题满分 12 分）已知曲线 $L\\colon y=y(x)$ 位于 $x$ 轴上方区域，$y(x)$ 二阶可导，且 $L$ 上任一点 $P$ 处的法线与 $x$ 轴相交，其交点记为 $Q$。点 $P$ 处的曲率半径始终等于线段 $PQ$ 的长，并且 $L$ 在点 $(0,1)$ 处的切线与 $y$ 轴垂直。\n/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/pdf/26.1111.10930/skills/pdf/container_tools/mark_artifact_operation_started.mjs\n/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1111.10930/skills/spreadsheets/container_tools/mark_artifact_operation_started.mjs\n/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/documents/26.1111.10930/skills/documents/container_tools/mark_artifact_operation_started.mjs\n/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/presentations/26.1111.10930/skills/presentations/container_tools/mark_artifact_operation_started.mjs\nrg: .release-work: IO error for operation on .release-work: No such file or directory (os error 2)\n302-batch-pilot.json\n302-clean-finalize.txt\n302-clean-preview.txt\n302-clean-run.txt\n302-common.txt\n302-convert.jsonl\n302-edition-check.txt\n302-first.txt\n302-hefei-1-variants.md\n302-hefei-2.md\n302-lilin-spread-diff.txt\n302-lilin-volume-1.md\n302-lilin-volume-2.md\n302-lilin-volume-3.md\n302-lilin-volume-4.md\n302-lilin-volume-5.md\n302-lilin-volume-6.md\n302-liyanfang-volume-1.md\n302-liyanfang-volume-2.md\n302-liyanfang-volume-3.md\n302-ocr-cache\n302-ocr-model\n302-older-10-1-unique-3.md\n302-older-10-1-unique-4.md\n302-older-10-1-unique-5.md\n302-older-10-1-unique-6.md\n302-older-10-1-unique-7.md\n302-older-10-1-unique-8.md\n302-older-10-1-unique-9.md\n302-older-10-1-volume-1.md\n302-older-10-1-volume-2.md\n302-older-10-1-volume-3.md\n302-older-10-1-volume-4.md\n302-older-10-1-volume-5.md\n302-older-10-1-volume-6.md\n"}

## assistant · 2026-11-12T13:05:05Z

教材将 L’Hospital 法则列在微分中值定理之后。我会把范围控制在第一章至第二章第四节的中值定理，解析也只用这一范围内的方法。每卷按 100 分、12 道题编排，包含选择、填空、计算与证明题；题源和删改情况会逐题注明。


## tool · 2026-11-12T13:05:12Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"bc7173","wall_time_seconds":0.000011375,"exit_code":0,"original_token_count":4734,"output":"## 第四套\n\n### 选择题\n\n1\\. 设常数 $a,b$ 使得 $\\lim_{x\\to+\\infty}(x\\arctan x-ax-b)=0$，则（　）。\n\nA. $a=\\pi,b=1$  \nB. $a=\\frac\\pi2,b=-1$  \nC. $a=\\pi,b=-1$  \nD. $a=\\frac\\pi2,b=1$\n\n2\\. 已知反常积分 $\\int_0^{+\\infty}\\frac{\\mathrm{e}^x-1}{x^\\alpha\\cdot\\mathrm{e}^x}\\,\\mathrm{d}x$ 收敛，则下列选项正确的是（　）。\n\nA. $0<\\alpha\\le1$  \nB. $1<\\alpha\\le2$  \nC. $1<\\alpha<2$  \nD. $0<\\alpha<1$\n\n3\\. $f(x)=\\begin{cases}2^x,&x\\le0,\\\\\\cos x+x^2,&x>0,\\end{cases}$ 的一个原函数为（　）。\n\nA. $F(x)=\\begin{cases}\\frac{2^x}{\\ln2}+1,&x\\le0,\\\\\\sin x+\\frac{x^3}3+\\frac1{\\ln2},&x>0\\end{cases}$  \nB. $F(x)=\\begin{cases}\\frac{2^x}{\\ln2}+1,&x\\le0,\\\\\\sin x+\\frac{x^3}3+\\frac1{\\ln2}+2,&x>0\\end{cases}$  \nC. $F(x)=\\begin{cases}\\frac{2^x}{\\ln2},&x\\le0,\\\\\\sin x+\\frac{x^3}3+\\frac1{\\ln2},&x>0\\end{cases}$  \nD. $F(x)=\\begin{cases}\\frac{2^x}{\\ln2},&x\\le0,\\\\\\sin x+\\frac{x^3}3,&x>0\\end{cases}$\n\n4\\. 设 $f(x)$ 在 $[0,1]$ 上有连续的导数，且 $f(0)=0,f(1)=1$，则下列选项正确的是（　）。\n\nA. $\\int_0^1|f'(x)-f(x)|\\,\\mathrm{d}x\\ge\\mathrm{e}$  \nB. $\\int_0^1|f'(x)-f(x)|\\,\\mathrm{d}x\\ge\\frac1{\\mathrm{e}}$  \nC. $\\int_0^1|f'(x)-f(x)|\\,\\mathrm{d}x\\le2$  \nD. $\\int_0^1|f'(x)-f(x)|\\,\\mathrm{d}x\\le\\frac2{\\mathrm{e}}$\n\n5\\. 设 $a>0$，当 $x\\in(1,+\\infty)$ 时，$\\ln x\\le x^a$，则 $a$ 的取值范围为（　）。\n\nA. $(0,\\mathrm{e}]$  \nB. $\\left(0,\\frac1{\\mathrm{e}}\\right)$  \nC. $[\\mathrm{e},+\\infty)$  \nD. $\\left[\\frac1{\\mathrm{e}},+\\infty\\right)$\n\n6\\. 设 $f(x,y)$ 的全微分为 $\\mathrm{d}f(x,y)=\\frac{axy^2}{(x^2+y^2)^2}\\,\\mathrm{d}x+\\frac{-4yx^b}{(x^2+y^2)^2}\\,\\mathrm{d}y$（$x>0,y>0$），$f(x,y)$ 有二阶连续偏导数，则 $\\left.\\mathrm{d}f\\right|_{(1,1)}=$（　）。\n\nA. $\\mathrm{d}x-\\mathrm{d}y$  \nB. $\\mathrm{d}x+\\mathrm{d}y$  \nC. $2\\mathrm{d}x-\\mathrm{d}y$  \nD. $-2\\mathrm{d}x-\\mathrm{d}y$\n\n7\\. 设数列 $\\{x_n\\}$ 与 $\\{y_n\\}$ 满足 $x_0=1$，$x_n=x_{n-1}+\\cos x_{n-1}$，且 $x_n+y_n=\\frac\\pi2$（$n=1,2,\\ldots$），则 $\\lim_{n\\to\\infty}\\frac{y_{n+1}}{\\left(\\frac\\pi2-x_n\\right)^3}=$（　）。\n17\\.（本题满分 10 分）已知当 $x\\to0$ 时，$a\\sin x+bx^2+\\ln(1-2x+x^2)$ 与 $1-\\mathrm{e}^{5x^2}$ 是等价无穷小，求 $a,b$ 的值。\n\n18\\.（本题满分 12 分）设 $f(x,y)=\\begin{cases}(x^2+y^2+a\\sqrt{|x|}+b)\\frac{\\sin(xy^2)}{x^2+y^4},&(x,y)\\ne0,\\\\0,&(x,y)=0\\end{cases}$ 在点 $(0,0)$ 处可微，求 $a,b$ 的值。\n\n19\\.（本题满分 12 分）设 $D=\\{(x,y)\\mid0\\le x\\le1,\\ 1\\le y\\le2\\}$。计算 $I=\\iint_D x^y\\sin\\left(\\ln\\frac1x\\right)\\,\\mathrm{d}x\\,\\mathrm{d}y$。\n\n20\\.（本题满分 12 分）设 $f(x)$ 在 $(0,+\\infty)$ 内有定义，$f'(1)=1$，对任意的正数 $x,y$ 满足 $f(xy)=\\frac{f(x)}y+\\frac{f(y)}x$。\n\n（I）求 $f(x)$。  \n（II）求 $y=f(x)$ 的极值与拐点。\n\n21\\.（本题满分 12 分）设 $f(x)$ 在 $[-1,1]$ 上有连续的二阶导数。\n\n（I）证明：存在 $\\xi\\in[-1,1]$，使得 $\\int_{-1}^1xf(x)\\,\\mathrm{d}x=\\frac13[2f'(\\xi)+\\xi f''(\\xi)]$。  \n（II）证明：若 $f(x)$ 在 $(-1,1)$ 内取得极值，则存在一点 $\\eta\\in(-1,1)$，使得 $|2f'(\\eta)+\\eta f''(\\eta)|\\ge\\frac12|f(1)-f(-1)|$。\n\n22\\.（本题满分 12 分）设 $A=\\begin{pmatrix}0&1&0\\\\1&0&2\\\\1&-1&2\\end{pmatrix}$。\n\n（I）求 $3$ 阶可逆矩阵 $P$ 与 $Q$，使得 $PAQ=\\begin{pmatrix}1&0&0\\\\0&1&0\\\\0&0&0\\end{pmatrix}$。  \n（II）在第（I）问的基础上，若记 $B=(QP)^{-1}$，且 $A=BC$，求一个可逆矩阵 $T$ 及对角矩阵 $\\Lambda$，使得 $T^{-1}(C+E)^2T=\\Lambda$。\n# 【紧凑】张宇八套卷-数二（已勘误）\n\n## 卷一\n\n### 选择题\n\n1\\. 曲线 $y=(x+2)e^{1/x}$ 的渐近线的条数为（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $3$\n\n2\\. 设函数 $f(x)$ 可导，$F(x)=f(x)[1-|\\ln(1+x)|]$，则（　）。\n\nA. $F(x)$ 在 $x=0$ 处不可导。  \nB. 当 $F(x)$ 在 $x=0$ 处可导时，$f(0)=0$。  \nC. 当 $F(x)$ 在 $x=0$ 处可导时，$f(0)=1$。  \nD. $F'(0)=f'(0)$。\n\n3\\. 设线性无关的函数 $y_1,y_2,y_3$ 都是二阶非齐次线性微分方程 $y''+p(x)y'+q(x)y=f(x)$ 的解，$C_1,C_2$ 是任意常数，则该非齐次方程的通解是（　）。\n\nA. $C_1y_1+C_2y_2+y_3$  \n3\\. 设数列 $\\{a_n\\}$ 满足 $\\lim_{n\\to\\infty}(a_{n+1}-a_n)=0$，下面结论中正确的是（　）。\n\nA. 若 $\\{a_n\\}$ 是单调的，则 $\\{a_n\\}$ 必收敛。  \nB. 若 $\\{a_n\\}$ 是有界的，则 $\\{a_n\\}$ 必收敛。  \nC. 若 $\\{a_{2n}\\}$ 单调增加，而 $\\{a_{2n+1}\\}$ 单调减少，则 $\\{a_n\\}$ 必收敛。  \nD. 若 $\\{a_n\\}$ 与 $\\{a_{2n+1}\\}$ 均是单调增加的，则 $\\{a_n\\}$ 必收敛。\n\n4\\. 曲线 $y=\\int_0^x xte^{-t^2}\\,\\mathrm dt$ 的渐近线条数为（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $3$\n\n5\\. 设 $M=\\int_{-\\pi/2}^{\\pi/2}\\left(\\frac{\\sin^3x}{1+x^2}\\cos^4x+1\\right)\\,\\mathrm dx$，$N=\\int_{-\\pi/2}^{\\pi/2}\\left(\\ln\\frac{4+x}{4-x}+\\cos^3x\\right)\\,\\mathrm dx$，$P=\\int_{-\\pi/2}^{\\pi/2}(e^{x^2}\\sin x-2)\\,\\mathrm dx$，则（　）。\n17\\.（本题满分 10 分）设\n\n$$\ng(x)=\\begin{cases}f'(0),&x=0,\\\\\\frac{f(x)}x,&x\\ne0.\\end{cases}\n$$\n\n证明：\n\n（1）若 $f(0)=0$，$f''(0)$ 存在，则有 $g'(0)=\\frac12f''(0)$。  \n（2）若 $f(0)=0$，且 $f(x)$ 在 $(-\\infty,+\\infty)$ 上有连续的二阶导数，则 $g'(x)$ 在 $(-\\infty,+\\infty)$ 上连续。\n\n18\\.（本题满分 12 分）设平面光滑曲线 $L$ 位于 $x$ 轴上方并经过点 $M(1,2)$，并且具有如下性质：从原点到此曲线上任意一点的法线的距离等于该点到 $x$ 轴的距离。求此曲线方程，并求该方程确定的函数 $y=y(x)$ 的极值。\n\n19\\.（本题满分 12 分）设函数 $f(x)$ 在 $[0,1]$ 上有一阶连续导数，$M=\\max_{0\\le x\\le1}\\{|f(x)|\\}$，$f(0)=f(1)=0$，证明：\n\n（1）$\\left[\\int_0^x f'(t)\\,\\mathrm dt\\right]^2\\le x\\int_0^x[f'(t)]^2\\,\\mathrm dt$，$x\\in[0,1]$；  \n（2）$\\sqrt{\\int_0^1[f'(t)]^2\\,\\mathrm dt}\\ge2M$。\n\n20\\.（本题满分 12 分）设平面区域 $D=\\{(x,y)\\mid x^2+y^2\\le1\\}$，计算 $I=\\iint_D\\left|x^2+y^2-\\frac{\\sqrt2}2(x+y)\\right|\\,\\mathrm d\\sigma$。\n\n21\\.（本题满分 12 分）设函数 $p_1(x),p_2(x)$ 连续，$y_1(x),y_2(x)$ 是二阶齐次线性微分方程 $y''+p_1(x)y'+p_2(x)y=0$ 的两个线性无关的解，记 $W(x)=y_1y_2'-y_2y_1'$。证明：\n2\\. 设函数 $f(x)$ 与 $g(x)$ 满足 $f(x_0)=g(x_0)$，$f'(x_0)<g'(x_0)$，则必存在 $\\delta>0$，使得（　）。\n\nA. 当 $x\\in(x_0-\\delta,x_0)\\cup(x_0,x_0+\\delta)$ 时，有 $f(x)<g(x)$。  \nB. 当 $x\\in(x_0-\\delta,x_0)\\cup(x_0,x_0+\\delta)$ 时，有 $f(x)>g(x)$。  \nC. 当 $x\\in(x_0-\\delta,x_0)$ 时，有 $f(x)<g(x)$；当 $x\\in(x_0,x_0+\\delta)$ 时，有 $f(x)>g(x)$。  \nD. 当 $x\\in(x_0-\\delta,x_0)$ 时，有 $f(x)>g(x)$；当 $x\\in(x_0,x_0+\\delta)$ 时，有 $f(x)<g(x)$。\n\n3\\. 设方程 $y''+ay'+y=(x+1)e^{bx}$ 的每一个解 $y=y(x)$ 在区间 $[0,+\\infty)$ 上均有界，则实数 $a,b$ 满足（　）。\n17\\.（本题满分 10 分）设 $f(x)$ 在 $x=0$ 的某邻域内连续，在 $x=0$ 处可导，且 $f(0)=0$，\n\n$$\ng(x)=\\begin{cases}\\frac1{x^2}\\int_0^xtf(t)\\,\\mathrm dt,&x\\ne0,\\\\0,&x=0.\\end{cases}\n$$\n\n证明 $g(x)$ 在 $x=0$ 处可导且 $g'(x)$ 在 $x=0$ 处连续。\n\n18\\.（本题满分 12 分）设函数 $f(x)$ 满足 $f(x)=-f(x-1)$，$x\\in[0,1]$，且 $f(x)$ 在 $[-1,1]$ 上可导。\n\n（1）证明 $\\int_{-1}^1f(x)\\,\\mathrm dx=0$。  \n（2）设 $F(x)=(1-x^2)\\int_0^1f(x)\\,\\mathrm dx+\\int_1^xf(t)\\,\\mathrm dt$，证明存在 $\\xi\\in(-1,1)$，使得 $F''(\\xi)=0$。\n\n19\\.（本题满分 12 分）设 $z(x,y)$ 在 $xOy$ 平面上的任一有界区域 $D$ 内存在连续偏导数，且\n\n$$\n\\iint_D\\left[\\left(\\frac{\\partial z}{\\partial x}\\right)^2+x^2z^2\\right]\\,\\mathrm dx\\,\\mathrm dy\n=2\\iint_D xz\\frac{\\partial z}{\\partial x}\\,\\mathrm dx\\,\\mathrm dy,\\quad z(0,y)=y^2,\n$$\n\n求 $z(x,y)$ 的表达式。\n1\\. 设函数 $f(x)$ 在区间 $(-1,1)$ 内有定义，且在点 $x=0$ 处连续。考察以下结论。\n\n① 当 $\\lim_{x\\to0}\\frac{f(x)}{\\sqrt[3]x}=0$ 时，$f(x)$ 在点 $x=0$ 处可导。  \n② 当 $\\lim_{x\\to0}\\frac{f(x)}{x^2}=0$ 时，$f(x)$ 在点 $x=0$ 处可导。  \n③ 当 $f(x)$ 在点 $x=0$ 处可导时，$\\lim_{x\\to0}\\frac{f(x)}{\\sqrt[3]x}=0$。\n\n所有正确结论的序号为（　）。\n\nA. ①  \nB. ②  \nC. ②③  \nD. ①②\n\n2\\. 三元方程 $e^{z+1}+xy+yz+zx=0$ 在点 $(1,1,-1)$ 的某个邻域内必能确定的隐函数为（　）。\n3\\. 设函数 $f(x)$ 在 $(0,+\\infty)$ 上可导，给出下列命题。\n\n① 若曲线 $y=f(x)$ 有水平渐近线 $y=1$，则 $\\lim_{x\\to+\\infty}f'(x)=0$。  \n② 若曲线 $y=f(x)$ 有斜渐近线 $y=x$，则 $\\lim_{x\\to+\\infty}f'(x)=1$。  \n③ 若 $\\lim_{x\\to+\\infty}\\frac{f(x)}x=1$，则曲线 $y=f(x)$ 的斜渐近线斜率为 $1$。  \n④ 若曲线 $y=f(x)$ 的斜渐近线斜率为 $1$，则 $\\lim_{x\\to+\\infty}\\frac{f(x)}x=1$。\n\n正确命题的个数为（　）。\n\nA. $1$  \nB. $2$  \nC. $3$  \nD. $4$\n\n4\\. 已知函数 $f(x),g(x)$ 可导，且 $f'(x)>0$，$g'(x)<0$，则（　）。\n\nA. $\\int_{-1}^0 f(x)g(x)\\,\\mathrm dx>\\int_0^1 f(x)g(x)\\,\\mathrm dx$  \nB. $\\int_{-1}^0 |f(x)g(x)|\\,\\mathrm dx>\\int_0^1 |f(x)g(x)|\\,\\mathrm dx$  \nC. $\\int_{-1}^0 f[g(x)]\\,\\mathrm dx>\\int_0^1 f[g(x)]\\,\\mathrm dx$  \nD. $\\int_{-1}^0 g[f(x)]\\,\\mathrm dx>\\int_0^1 g[g(x)]\\,\\mathrm dx$\n\n5\\. 设数列 $\\{a_n\\}$ 满足 $a_1>2$，$a_{n+1}=a_n-\\frac{a_n-3}{a_n-2}$（$n=1,2,3,\\ldots$），则（　）。\n\nA. $\\{a_n\\}$ 收敛于大于 $3$ 的数。  \nB. $\\{a_n\\}$ 收敛于 $3$。  \nC. $\\{a_n\\}$ 发散。  \nD. $\\{a_n\\}$ 的敛散性与 $a_1$ 有关。\n\n6\\. 设函数 $f(x)$ 在 $x=0$ 的某邻域内有定义，且 $\\lim_{x\\to0}\\frac{x-f(x)}{\\sin x}=1$，则（　）。\n\nA. $f(0)=0$  \n17\\.（本题满分 10 分）已知函数 $f(x)$ 在 $x=0$ 处具有一阶导数，且 $\\lim_{x\\to0}\\frac{xf(x)+e^{x^2}\\sin x}{x^2}=1$。求曲线 $y=f(x)$ 在 $x=0$ 处的切线方程。\n\n18\\.（本题满分 12 分）求 $f(x,y)=e^{x+y}\\left(y+\\frac{x^3}3\\right)$ 的极值。\n\n19\\.（本题满分 12 分）已知函数 $f(x,y)$ 二阶偏导数连续，任给 $x,y$，均有 $f(x+1,y)=f(x,y)$，$f(x,y+1)=f(x,y)$，且 $\\iint_D\\{[f'_x(x,y)]^2+[f'_y(x,y)]^2\\}\\,\\mathrm d\\sigma=a$，其中 $D=\\{(x,y)\\mid-1\\le x\\le1,\\ -1\\le y\\le1\\}$。\n\n（I）计算 $I=\\iint_D f(x,y)[f''_{xx}(x,y)+f''_{yy}(x,y)]\\,\\mathrm d\\sigma$。  \n（II）若 $I\\ge0$，证明 $\\mathrm d[f(x,y)]=0$。\n\n20\\.（本题满分 12 分）设由曲线 $y=y(x)=\\lim_{a\\to-\\infty}\\frac{x}{1+x^2-2e^{ax}}$ 和直线 $y=\\frac12x$ 围成的平面图形为 $D$。\n\n（I）求 $D$ 的面积 $S$。  \n（II）求 $D$ 绕 $y$ 轴旋转一周所围成的旋转体的体积 $V$。\n\n21\\.（本题满分 12 分）已知曲线 $L\\colon y=y(x)$ 位于 $x$ 轴上方区域，$y(x)$ 二阶可导，且 $L$ 上任一点 $P$ 处的法线与 $x$ 轴相交，其交点记为 $Q$。点 $P$ 处的曲率半径始终等于线段 $PQ$ 的长，并且 $L$ 在点 $(0,1)$ 处的切线与 $y$ 轴垂直。\n# 【紧凑版】李艳芳三套卷做题本\n\n## 卷一\n\n### 选择题\n\n1\\. 若 $\\lim_{x\\to\\infty}x^2\\left(2a-ax\\sin\\frac1x-b\\cos\\frac1x\\right)=\\frac12$，则（　）。\n\nA. $a=\\frac34,b=\\frac34$  \nB. $a=\\frac34,b=\\frac43$  \nC. $a=\\frac43,b=\\frac34$  \nD. $a=\\frac43,b=\\frac43$\n\n2\\. 若曲线 $y=\\frac{x^5}{20}-\\frac{x^4}4+\\frac{x^3}3+C_1x+C_2$ 的三个拐点位于同一条直线上，则（　）。\n\nA. 必有 $C_1=-\\frac2{15},C_2=0$。  \nB. 必有 $C_1=\\frac{13}{15},C_2=1$。  \nC. 不存在这样的 $C_1,C_2$。  \nD. 任意的 $C_1,C_2$ 均满足要求。\n\n3\\. 记 $I_1=\\int_0^{\\frac12}\\frac{1}{\\sqrt{4-x+x^2}}\\,\\mathrm{d}x$，$I_2=\\int_0^1\\frac{x}{\\sqrt{4-x^2+x^3}}\\,\\mathrm{d}x$，$I_3=\\int_0^1\\frac{\\mathrm{e}^x-1}{\\sqrt{4-x^2+x^4}}\\,\\mathrm{d}x$，则 $I_1,I_2,I_3$ 的大小关系是（　）。\n\nA. $I_1<I_2<I_3$  \nB. $I_2<I_1<I_3$  \nC. $I_1<I_3<I_2$  \nD. $I_2<I_3<I_1$\n\n4\\. 设 $ab>0$，若数 $k$ 满足对任意的 $x$，$a^2\\sec^2x+b^2\\csc^2x\\ge k$ 均成立，则 $k$ 的最大值为（　）。\n\nA. $(a+b)^2$  \nB. $(a-b)^2$  \nC. $a^2+b^2$  \nD. $a^2-b^2$\n\n5\\. 设函数 $f(x)$ 在 $(-\\infty,+\\infty)$ 内有定义，且对于任意的 $x,y$，都有 $f(x+y)=f(x)f(y)$，已知 $f(0)\\ne0,f'(0)=a\\ne0$，则（　）。\n\nA. $f(x)$ 单调增加。  \nB. $f(x)$ 单调减少。  \nC. $f(x)$ 为凹函数。  \nD. $f(x)$ 为凸函数。\n\n6\\. 设函数 $f(x,y)=\\begin{cases}\\left(\\frac1{x^2+y^2}\\right)^{|x|+|y|},&(x,y)\\ne(0,0),\\\\1,&(x,y)=(0,0),\\end{cases}$ 则下列说法中，正确的是（　）。\n\nA. $f(x,y)$ 在点 $(0,0)$ 处的二重极限不存在。  \nB. $f(x,y)$ 在点 $(0,0)$ 处的二重极限存在，但在该点处不连续。  \nC. $f(x,y)$ 在点 $(0,0)$ 处连续但不可微。  \nD. $f(x,y)$ 在点 $(0,0)$ 处可微。\n\n7\\. 设区域 $D=\\{(x,y)\\mid0\\le x\\le\\pi,0\\le y\\le\\pi\\}$，则 $\\iint_D(\\sin^2x+\\cos^2y)(x+y)\\,\\mathrm{d}x\\,\\mathrm{d}y=$（　）。\n\nA. $\\pi^3\\lim_{n\\to\\infty}\\sum_{i=1}^n\\frac{i}{n^2}$  \nB. $\\pi^3\\lim_{n\\to\\infty}\\sum_{i=1}^{2n}\\frac{i}{n^2}$  \nC. $\\frac{\\pi^3}{2}\\lim_{n\\to\\infty}\\sum_{i=1}^{2n}\\sum_{j=1}^i\\frac{i+j}{n^3}$  \nD. $\\frac{\\pi^3}{4}\\lim_{n\\to\\infty}\\sum_{i=1}^{2n}\\sum_{j=1}^i\\frac{i+j}{n^3}$\n\n8\\. 设向量 $\\boldsymbol\\beta$ 可由向量组 $\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_t$（$t\\ge2$）线性表示，但不能由向量组 $\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_{t-1}$ 线性表示，则下列说法中，正确的是（　）。\n\nA. $r(\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_{t-1})=t$  \nB. $r(\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_{t-1},\\boldsymbol\\alpha_t)=t$  \nC. $r(\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_t)=r(\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_{t-1})$  \nD. $r(\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_t,\\boldsymbol\\beta)=r(\\boldsymbol\\alpha_1,\\boldsymbol\\alpha_2,\\ldots,\\boldsymbol\\alpha_{t-1},\\boldsymbol\\beta)$\n\n9\\. 设 $a,b,c$ 均为非零常数，矩阵 $A=\\begin{pmatrix}1&a&a^2\\\\1&b&b^2\\\\1&c&c^2\\end{pmatrix}$，向量 $\\begin{pmatrix}1\\\\2\\\\1\\end{pmatrix}$ 是方程组 $A\\boldsymbol{x}=\\begin{pmatrix}0\\\\0\\\\1\\end{pmatrix}$ 的一个解，则（　）。\n\nA. 方程组 $A\\boldsymbol{x}=(1,0,0)^T$ 有解。  \nB. 方程组 $A\\boldsymbol{x}=(0,1,0)^T$ 有解。  \nC. 方程组 $A\\boldsymbol{x}=(1,1,0)^T$ 有解。  \nD. 方程组 $A\\boldsymbol{x}=0$ 的基础解系中包含两个向量。\n\n10\\. 设 $\\boldsymbol\\alpha,\\boldsymbol\\beta$ 为相互正交的 $3$ 维非零列向量，则下列命题中，正确的是（　）。\n\n① $\\boldsymbol\\alpha\\boldsymbol\\beta^T$ 不能相似对角化。  \n② $\\boldsymbol\\alpha\\boldsymbol\\beta^T$ 能相似对角化。  \n③ $\\boldsymbol\\alpha\\boldsymbol\\beta^T$ 与 $\\boldsymbol\\alpha\\boldsymbol\\beta^T+\\boldsymbol\\beta\\boldsymbol\\alpha^T$ 没有公共的特征向量。  \n④ $\\boldsymbol\\alpha\\boldsymbol\\beta^T$ 与 $\\boldsymbol\\alpha\\boldsymbol\\beta^T+\\boldsymbol\\beta\\boldsymbol\\alpha^T$ 有公共的特征向量。\n\nA. ①③  \nB. ①④  \nC. ②③  \nD. ②④\n\n### 填空题\n\n11\\. 设函数 $f(x)$ 可导，已知曲线 $y=\\arccos\\frac1x-\\frac{2\\pi}3$ 与曲线 $y=f(x)$ 在点 $(-2,0)$ 处相切，且 $f(x)$ 满足 $f(x)+f(-x)=-\\frac\\pi3$，则曲线 $y=f(x)$ 在点 $(2,f(2))$ 处的切线方程为 $y=$ ______。\n\n12\\. 设可导函数 $f(x)$ 满足 $f(x)=x+\\int_0^xf'(t)\\sin t\\,\\mathrm{d}t$，则 $f(x)=$ ______。\n\n13\\. 曲线 $|\\ln x|+|\\ln y|=1$ 所围成图形绕 $x$ 轴旋转一周所得旋转体的体积 $V=$ ______。\n\n14\\. 设 $p$ 为常数，若反常积分 $\\int_0^{\\frac\\pi2}\\frac{\\tan x}{(1-\\sin x)^{1-p}\\sin^p x}\\,\\mathrm{d}x$ 收敛，则 $p$ 的取值范围是 ______。\n\n15\\. 设函数 $z=z(x,y)$ 由方程 $z^3-3xy\\sin z=1$ 所确定，则 $\\left.\\frac{\\partial^2z}{\\partial x\\partial y}\\right|_{(0,0)}=$ ______。\n\n16\\. 已知二次型 $f(x_1,x_2,x_3)=x_1^2-2x_2^2+bx_3^2-4x_1x_2+4x_1x_3+2ax_2x_3$ 可经正交变换化为标准形 $-7y_1^2-by_2^2-by_3^2$，记二次型 $f$ 对应的对称矩阵为 $(a_{ij})_{3\\times3}$，$a_{11}$ 的代数余子式 $A_{11}$ 等于 $-12$，则 $ab=$ ______。\n\n### 解答题\n\n17\\.（本题满分 10 分）设函数 $f(x)$ 满足当 $0<x\\le1$ 时，$f(x)=(1-\\cos x)^{\\sin\\pi x}$，而对其他 $x$，满足 $f(x)+k=\\frac12f(x-1)$。已知 $f(x)$ 在 $x=1$ 处连续。\n\n① 求常数 $k$。  \n② $f(x)$ 在 $x=0$ 处是否连续？\n\n18\\.（本题满分 12 分）设区域 $D$ 是由抛物线 $x=y^2$ 与折线 $x=|y|$ 围成的平面有界区域，函数 $f(x,y)=x+[y]\\cos y\\iint_D f(x,y)\\,\\mathrm{d}x\\,\\mathrm{d}y$，其中 $[y]$ 表示不超过 $y$ 的最大整数，求 $f(x,y)$ 的表达式。\n\n19\\.（本题满分 12 分）设函数 $f(x)$ 满足微分方程 $y''+2y'-2y=\\mathrm{e}^x\\cos x$，且 $f(0)=0,f'(0)=\\frac14$，求 $\\int_0^{2\\pi}\\max\\{f(x),0\\}\\,\\mathrm{d}x$。\n\n20\\.（本题满分 12 分）求函数 $f(x,y)=x(y+1)\\mathrm{e}^{xy-x^2}$ 的极值。\n\n21\\.（本题满分 12 分）设函数 $f(x)$ 在 $[0,1]$ 上连续，$\\int_0^1xf(x)\\,\\mathrm{d}x=0$，$\\int_0^1x^2f(x)\\,\\mathrm{d}x=-1$。\n\n① 求 $\\int_0^1x(1-x)f(x)\\,\\mathrm{d}x$。  \n② 证明：$\\max_{0\\le x\\le1}f(x)>6$。\n\n22\\.（本题满分 12 分）设可相似对角化的 $3$ 阶矩阵 $A$ 的特征值为 $2,-1,-1$。已知 $\\boldsymbol\\alpha=(1,1,0)^T$ 是 $A^T$ 的属于特征值 $2$ 的一个特征向量，且 $\\boldsymbol\\alpha$ 也是 $A$ 的一个特征向量。\n\n① 求矩阵 $A$。  \n② 求可逆线性变换 $\\boldsymbol{x}=P\\boldsymbol{y}$，将二次型 $f(\\boldsymbol{x})=\\boldsymbol{x}^T(A+A^T)\\boldsymbol{x}$ 化为规范形。\n\n## 卷二\n\n### 选择题\n\n1\\. 若 $\\lim_{x\\to0}\\frac{\\tan x+xf(x)}{x^3}=\\frac23$，则当 $x\\to0$ 时，与 $f(x)+1$ 等价的无穷小量为（　）。\n\nA. $\\cos x-1$  \n# 8月强化突击测试\n\n1\\. 设函数 $f(x)$ 连续，给出下列四个条件\n\n（1）$\\lim_{x\\to0}\\frac{|f(x)|-f(0)}{x}$ 存在；\n\n（2）$\\lim_{x\\to0}\\frac{f(x)-|f(0)|}{x}$ 存在；\n\n（3）$\\lim_{x\\to0}\\frac{|f(x)|}{x}$ 存在；\n\n（4）$\\lim_{x\\to0}\\frac{|f(x)|-|f(0)|}{x}$ 存在。\n\n其中能得到“$f(x)$ 在 $x=0$ 处可导”的条件个数是 ______。\n\n2\\. 设 $f(x)$ 在点 $x=a$ 处可导，则函数 $|f(x)|$ 在点 $x=a$ 处不可导的充分条件是（　）。\n\nA. $f(a)=0$，且 $f'(a)=0$\n\nB. $f(a)=0$，且 $f'(a)\\ne0$\n\nC. $f(a)>0$，且 $f'(a)>0$\n\nD. $f(a)<0$，且 $f'(a)<0$\n\n3\\. 设函数 $f(x)$ 在 $x=0$ 处连续，且\n\n$$\n\\lim_{x\\to0}\\frac{xf(x)-e^{2\\sin x}+1}{\\ln(1+x)+\\ln(1-x)}=-3,\n$$\n\n证明 $f(x)$ 在 $x=0$ 处可导，并求 $f'(0)$。\n\n4\\. 设函数 $f(x)$ 在 $[-a,a]$ 内有 2 阶连续导数，证明：\n\n（1）若 $f(0)=0$，则存在 $\\xi\\in(-a,a)$，使得 $f''(\\xi)=\\frac{1}{a^2}[f(a)+f(-a)]$；\n\n（2）若 $f(x)$ 在 $(-a,a)$ 内取得极值，则存在 $\\eta\\in(-a,a)$，使得 $|f''(\\eta)|\\ge\\frac{1}{2a^2}|f(a)-f(-a)|$。\n\n5\\. 设函数 $f(x)$ 具有 2 阶导数，且 $f'(0)=f'(1)$，$|f''(x)|\\le1$，证明：\n\n（I）当 $x\\in(0,1)$ 时，$\\left|f(x)-f(0)(1-x)-f(1)x\\right|\\le\\frac{x(1-x)}2$；\n\n（II）$\\left|\\int_0^1 f(x)\\,\\mathrm dx-\\frac{f(0)+f(1)}2\\right|\\le\\frac1{12}$。\n"}
{"chunk_id":"446146","wall_time_seconds":0.000010791,"exit_code":0,"original_token_count":2244,"output":"proof-katex\ntectonic-cache\nJxrDecApp\nheif-convert\npdfinfo\npdftoppm\nsoffice\nrg: /Applications/Codex.app: IO error for operation on /Applications/Codex.app: No such file or directory (os error 2)\n# GPT 试题库\n\n本仓库收录 GPT 生成的试题与解析，以及按主题整理的真题资料。考研数学是其中一个专题。\n\n## 考研数学\n\n按《工科数学分析基础》第三版上册组织的考研数学练习资料，包含 **2009–2026 年数学二分节真题**和 **27302 阶段模拟卷**。下载 PDF 即可使用，也可编辑 LaTeX 源稿。\n\n### 下载资料\n\n| 资料 | 内容 | 下载 |\n| --- | --- | --- |\n| 数学二分节真题集 | 按教材四章 19 节整理 234 道真题。各节附定理与要点，题目保留年份和原卷题号，每题后另页附解析。 | [横屏 PDF](output/302数学二分节真题集（原生LaTeX横屏版）.pdf) · [横屏源稿](output/302数学二分节真题集（原生LaTeX横屏版）.tex) · [A4 编译入口](output/302数学二分节真题集（原生LaTeX常规版）.tex) |\n| 27302 阶段模拟卷（iPad 横屏版） | 五套模拟卷和 76 道补充练习，共 186 道题。每题单独一页，留有手写区，翻页可看解题思路、推导与答案。 | [横屏 PDF](output/pdf/27302阶段模拟卷（iPad横屏版）.pdf) |\n| 27302 阶段模拟卷（A4） | 适合打印和限时练习。每套 22 题，满分 150 分，建议用时 180 分钟。 | [第一卷 PDF](output/27302阶段模拟卷.pdf) · [第二至五卷及补充练习 PDF](output/27302阶段模拟卷（第二至五卷及补充练习）.pdf) |\n\n### 练习范围\n\n- **分节刷真题**：真题集覆盖教材上册的函数、极限与连续，一元函数微分学，一元函数积分学和常微分方程。可用 PDF 目录跳到正在复习的小节。\n- **做阶段模拟**：五套模拟卷及补充练习覆盖第一章至第二章第四节「微分中值定理及其应用」。每套包含 10 道单选、6 道填空和 6 道解答题。\n\n### 编辑与编译\n\nLaTeX 源文件位于 `output/`。使用带有 `ctex`、Fandol 字体和 TikZ 的 XeLaTeX 环境，在该目录编译所需的 `.tex` 文件。\n\n- 数学二真题集的 A4 编译入口读取同目录的横屏源稿，两种版式共用题目和解析。\n- 27302 模拟卷提供 [第一卷源稿](output/27302阶段模拟卷.tex) 和 [第二至五卷及补充练习源稿](output/27302阶段模拟卷（第二至五卷及补充练习）.tex)。\n\n推送到 `main` 后，GitHub Actions 会编译本次改动影响的 TeX 文档，并将 PDF 上传到 [Releases](https://github.com/OyamaMeek/codex-question-bank/releases)。自动版本从 `v0.0.1` 递增至 `v0.0.999`。如需注明具体改动，在相关 Git 提交正文的末尾留一个空行，再写 `Release-Note: 补充第二至五卷解析`。没有该字段时，发布说明会列出更新的文档名。\n\n## 开发记录\n\n资料的编排和修订历史见 [开发记录](docs/CHANGELOG.md)。\nimport math\n\n\ndef integral(function, lower, upper, intervals=20000):\n    assert intervals % 2 == 0\n    step = (upper - lower) / intervals\n    total = function(lower) + function(upper)\n    total += 4 * sum(function(lower + i * step) for i in range(1, intervals, 2))\n    total += 2 * sum(function(lower + i * step) for i in range(2, intervals, 2))\n    return step * total / 3\n\n\nchecks = 0\n\n\ndef close(actual, expected, tolerance=1e-8):\n    global checks\n    assert math.isclose(actual, expected, rel_tol=tolerance, abs_tol=tolerance), (actual, expected)\n    checks += 1\n\n\nfor x in (0.2, 0.7, 1.0, 1.4, 2.0):\n    close(math.exp(-x) * (math.cos(x) - math.sin(x))\n          + math.exp(-x) * math.sin(x), math.exp(-x) * math.cos(x))\n    close(math.sqrt(x) + (x - 3 * x) / (2 * math.sqrt(x)), 0)\n    close(x * 6 - (2 + 6 * x) + 2, 0)\n    close(2 * x * (x / 2 - 1 / (2 * x))\n          - 4 * (x * x / 4 - math.log(x) / 2), 2 * math.log(x) - 1)\n    close(x * 2 * x**5 - 6 * (1 + x**6 / 3), -6)\n    close(x**2 * (12 * x) + x * 6 * x**2 - 9 * 2 * x**3, 0)\n    close(x * (2 - math.log(x)) - x * (1 - math.log(x)), x)\n\nfor x in (2.1, 2.5, 3.0, 4.0, 7.0):\n    derivative = -x**2 / (x - 2)\n    second = -x * (x - 4) / (x - 2)**2\n    close(x**2 * second - 2 * x * derivative - derivative**2, 0)\n\nclose(11 - 3**2 / 2 - 2 * 3 - 4 * math.log(3 - 2), 0.5)\nclose(-3**2 / (3 - 2), -9)\nclose(integral(lambda x: 2 * x + 3 * x**2, 0, 1), 2)\nclose(2 * math.pi * integral(lambda x: x * (2 * x + 3 * x**2), 0, 1), 17 * math.pi / 6)\nclose(math.pi * integral(lambda x: x * math.exp(x*x), 1, 2),\n      math.pi * (math.exp(4) - math.e) / 2)\nclose(integral(lambda x: math.hypot(1, (x - 1/x) / 2), 1, math.e), (math.e**2 + 1) / 4)\nclose(integral(lambda x: 2 * x**3 * math.sqrt(max(0, 4 - x*x)), 1, 2),\n      22 * math.sqrt(3) / 5, 1e-6)\nclose(20 + 100 * math.exp(-math.log(10) * 60 / 30), 21)\nprint({\"status\": \"passed\", \"checks\": checks,\n       \"scope\": \"第四章选定解的原方程残差、初值、面积、体积、弧长及冷却时间\"})\n<a id=\"pdf-page-122\"></a>\n\n## PDF 第 122 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=122)\n\n已知 $v$ 在 $x$ 可导，由定理 1.1, $v$ 在 $x$ 必连续，故 $\\lim_{\\Delta x \\to 0} v(x + \\Delta x) = v(x)$，因而\n$$(uv)'(x) = u'(x)v(x) + u(x)v'(x).$$\n\n(3) 设 $y = \\frac{1}{v(x)}$，则\n$$\\Delta y = \\frac{1}{v(x + \\Delta x)} - \\frac{1}{v(x)} = -\\frac{v(x + \\Delta x) - v(x)}{v(x)v(x + \\Delta x)} = -\\frac{\\Delta v}{v(x)v(x + \\Delta x)}.$$\n与(2)中类似，可知 $\\lim_{\\Delta x \\to 0} v(x + \\Delta x) = v(x)$，注意到 $v(x) \\neq 0$，从而\n$$\\left(\\frac{1}{v}\\right)'(x) = \\lim_{\\Delta x \\to 0} \\frac{\\Delta y}{\\Delta x} = -\\lim_{\\Delta x \\to 0} \\frac{\\Delta v}{\\Delta x} \\frac{1}{v(x)v(x + \\Delta x)} = -\\frac{v'(x)}{v^2(x)}.$$\n再由(2)得\n$$\\left(\\frac{u}{v}\\right)'(x) = u'(x) \\frac{1}{v(x)} + u(x)\\left(\\frac{1}{v}\\right)'(x)\n= \\frac{u'(x)}{v(x)} - \\frac{u(x)v'(x)}{v^2(x)} = \\frac{u'(x)v(x) - u(x)v'(x)}{v^2(x)}.$$\n\n定理中的(1)与(2)可以推广到有限个函数的情形，并且容易得到导数运算的线性法则：\n$$(\\alpha u + \\beta v)'(x) = \\alpha u'(x) + \\beta v'(x)$$\n\n（$\\alpha, \\beta \\in \\mathbf{R}$ 为常数）。\n\n例 2.1 已知 $y = 2^x + \\sqrt{x}\\ln x$，求 $\\frac{\\mathrm{d}y}{\\mathrm{d}x}$.\n\n解 根据定理 2.1 的(1)，(2)及习题 2.1(A)的第1题得\n$$\\frac{\\mathrm{d}y}{\\mathrm{d}x} = (2^x)' + (\\sqrt{x})'\\ln x + \\sqrt{x}(\\ln x)' = 2^x\\ln 2 + \\frac{\\ln x}{2\\sqrt{x}} + \\frac{1}{\\sqrt{x}}.$$\n\n例 2.2 求正切函数 $y = \\tan x$ 和余切函数 $y = \\cot x$ 的导数.\n\n解 根据两个函数商的求导法则，我们有\n$$(\\tan x)' = \\left(\\frac{\\sin x}{\\cos x}\\right)' = \\frac{(\\sin x)'\\cos x - \\sin x(\\cos x)'}{\\cos^2 x}\n= \\frac{\\cos^2 x + \\sin^2 x}{\\cos^2 x} = \\sec^2 x,$$\n故得正切函数的导数公式\n$$(\\tan x)' = \\sec^2 x \\left(x \\neq (2k + 1) \\frac{\\pi}{2}, k \\in \\mathbf{Z}\\right).$$\n\n**页边注**\n\n注：利用已证的（2）中的结果将（3）的证明简化为只要证明 $y=\\frac{1}{v(x)}$ 可导，且 $\\left(\\frac{1}{v}\\right)'(x)=-\\frac{v'(x)}{v^{2}(x)}$，而后者的证明只要利用导数定义。\n\n想一想：为什么（1）与（2）的结论仅对有限个函数成立？\n\n<a id=\"pdf-page-123\"></a>\n\n## PDF 第 123 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=123)\n\n类似可得余切函数的导数公式\n\n$(\\cot x)' = -\\csc^2 x (x \\neq k\\pi, k \\in \\mathbf{Z}).$\n\n例2.3 求正割函数 $y = \\sec x$ 和余割函数 $y = \\csc x$ 的导数.\n\n解 根据定理2.1，我们有\n\n$(\\sec x)' = \\left(\\frac{1}{\\cos x}\\right)' = -\\frac{(\\cos x)'}{\\cos^2 x} = \\frac{\\sin x}{\\cos^2 x} = \\sec x \\tan x,$\n\n故得正割函数的导数公式\n\n$(\\sec x)' = \\sec x \\tan x \\left(x \\neq (2k + 1) \\frac{\\pi}{2}, k \\in \\mathbf{Z}\\right).$\n\n类似可得余割函数的导数公式\n\n$(\\csc x)' = -\\csc x \\cot x (x \\neq k\\pi, k \\in \\mathbf{Z}).$\n\n2.2 复合函数的求导法则\n\n定理2.2（链式法则）设函数 $u = g(x)$ 在 $x$ 处可导，函数 $y = f(u)$ 在与 $x$ 相对应的 $u$ 处可导，则复合函数 $y = f[g(x)]$ 在 $x$ 处可导，并且\n\n$\\frac{dy}{dx} = f'(u) g'(x)$ 或 $\\frac{dy}{dx} = \\frac{dy}{du} \\cdot \\frac{du}{dx}$. (2.1)\n\n证 由于函数 $y = f(u)$ 在 $u$ 处可导，由(1.10)式,\n\n$\\frac{\\Delta y}{\\Delta u} = f'(u) + \\alpha(\\Delta u)$ （其中 $\\lim_{\\Delta u \\to 0} \\alpha(\\Delta u) = 0$）。\n\n若 $\\Delta u \\neq 0$，则\n\n$\\Delta y = f'(u) \\Delta u + \\alpha(\\Delta u) \\Delta u;$ (2.2)\n\n若 $\\Delta u = 0$，则 $\\alpha(\\Delta u)$ 无意义.由于此时 $\\Delta y = f(u + \\Delta u) - f(u) = 0$，为使(2.2)式当 $\\Delta u = 0$ 时也成立，规定当 $\\Delta u = 0$ 时，$\\alpha(\\Delta u) = 0$，从而知无论 $\\Delta u$ 是否为0，(2.2)式都成立.于是\n\n"}

## tool · 2026-11-12T13:05:21Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"3b9f46","wall_time_seconds":0.000010541,"exit_code":0,"original_token_count":1303,"output":"1\\. 设 $f(x)=\\lim_{n\\to\\infty}\\frac{2x^{2n}-1}{x^{2n}+1}\\sin\\frac1x$，则 $f(x)$ 的第一类间断点的个数为（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $3$\n\n2\\. 设正值函数 $f(x)$ 在 $[0,+\\infty)$ 上有一阶连续的导数，且 $\\lim_{x\\to+\\infty}[f(x)+f'(x)]=0$，则 $y=f(x)$ 一定有渐近线（　）。\n\nA. $y=0$  \nB. $y=\\mathrm{e}$  \nC. $x=0$  \nD. $x=\\mathrm{e}$\n\n3\\. 设 $y=f(x)$ 由 $\\begin{cases}x=2t-|t|,\\\\y=t|\\mathrm{e}^t-1|\\end{cases}$ 确定，则在 $x=0$ 处（　）。\n\nA. $f'(x)$ 不存在  \nB. $f'(x)$ 存在但不连续  \nC. $f'(x)$ 连续但不可导  \nD. $f''(x)$ 存在\n\n4\\. 设 $f(x)$ 在 $x=0$ 处有三阶导数，且 $\\lim_{x\\to0}\\frac{f'(x)}{x^2}=1$，则（　）。\n\nA. $f(0)$ 是 $f(x)$ 的极小值  \n\n（I）求 $a,b,\\lambda$ 的值。  \n（II）求正交变换 $X=QY$，将二次型 $g(x_1,x_2,x_3)=X^T(A-A^*)X$ 化为标准形。\n\n## 第三套\n\n### 选择题\n\n1\\. 当 $x\\to0$ 时，$1-\\cos(\\sin x)-\\frac12\\ln(1+x^2)$ 是关于 $x$ 的（　）。\n\nA. 一阶无穷小量  \nB. 二阶无穷小量  \nC. 三阶无穷小量  \nD. 四阶无穷小量\n\n2\\. 设 $f(x)$ 在 $x=1$ 的某邻域内连续，且 $\\lim_{x\\to0}\\frac{\\ln[f(x+1)+\\mathrm{e}^{x^2}]}{x^2}=2$，则 $x=1$ 是 $f(x)$ 的（　）。\n\nA. 驻点且为极大值点  \nB. 驻点且为极小值点  \nC. 不可导点  \nD. 可导点但不是驻点\n\n3\\. 函数 $f(x)=\\frac{x^2-x}{|x|(x^2-1)}\\mathrm{e}^{\\frac{1}{x-2}}$ 的无穷间断点的个数为（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $3$\n\n4\\. 设 $f(x)$ 有二阶连续导数，且 $\\lim_{x\\to0}\\frac{f(x)}x=0$，当 $x>0$ 时满足 $xf''(x)+\\mathrm{e}^{f(x)}\\le6\\ln(1+x)$，则（　）。\n\n\n### 选择题\n\n1\\. 若 $\\lim_{x\\to0}\\frac{\\tan x+xf(x)}{x^3}=\\frac23$，则当 $x\\to0$ 时，与 $f(x)+1$ 等价的无穷小量为（　）。\n\nA. $\\cos x-1$  \nB. $\\ln\\left(1+\\frac x3\\right)$  \nC. $1-\\mathrm{e}^{x^2}$  \nD. $\\sqrt[3]{x^2+1}-1$\n\n2\\. 设函数 $f(x)$ 二阶可导，$g(x)$ 是 $f(x)$ 的反函数，$y(x)=g(\\cos x)$，$f(1)=0$，$f'(1)=-\\frac12$，$f''(1)=\\frac12$，则 $y'\\left(\\frac\\pi2\\right),y''\\left(\\frac\\pi2\\right)$ 分别为（　）。\n\nA. $2,2$  \nB. $2,4$  \nC. $-2,2$  \nD. $-2,4$\n\n3\\. 设函数 $f(x)$ 为二阶可导的正值函数，满足 $f''(x)f(x)-\\frac12[f'(x)]^2>0$，则对任意不同的非负 $x_1,x_2$，有（　）。\n\nA. $\\sqrt{f(x_1)}+\\sqrt{f(x_2)}<2f\\left(\\sqrt{\\frac{x_1+x_2}{2}}\\right)$  \nB. $\\sqrt{f(x_1)}+\\sqrt{f(x_2)}>2f\\left(\\sqrt{\\frac{x_1+x_2}{2}}\\right)$  \nC. $\\sqrt{f(x_1)}+\\sqrt{f(x_2)}<2\\sqrt{f\\left(\\frac{x_1+x_2}{2}\\right)}$  \nD. $\\sqrt{f(x_1)}+\\sqrt{f(x_2)}>2\\sqrt{f\\left(\\frac{x_1+x_2}{2}\\right)}$\n\n4\\. 设动点 $P$ 从原点出发以匀速 $v_0$ 沿 $x$ 轴正向运动，点 $A$ 为 $y$ 轴正半轴上的定点，坐标为 $(0,a)$，记 $\\angle APO=\\alpha$，$AP$ 的长为 $l$，则 $\\alpha$ 关于时间的变化率的大小为（　）。\n19\\.（本题满分 12 分）设 $\\varphi(t)$ 是 $[0,+\\infty)$ 上的非负函数，且 $\\varphi(0)=0$，函数 $u=u(x,y)$ 由方程 $u(x,y)=y+x\\varphi(u)$ 确定，已知 $2u''_{xx}-\\varphi(u)u''_{xy}-\\varphi^2(u)u''_{yy}=\\left[\\frac{u}{1-x\\varphi'(u)}\\right]^2$，求 $\\varphi(t)$ 的表达式。\n\n20\\.（本题满分 12 分）设曲线 $y=y(x)$（$-1\\le x<0$）过点 $P(-1,0)$，$y(x)$ 单调增加，曲线上任意一点 $M$ 处的切线与 $y$ 轴相交于点 $T$。若对任意一点 $M$，曲线弧段 $PM$ 的长度均等于点 $T$ 到原点的距离的一半，且曲线与 $x$ 轴在点 $P$ 处相切。求曲线 $y=y(x)$ 的方程。\n\n21\\.（本题满分 12 分）设函数 $f(x)$ 在 $[0,1]$ 上三阶可导，且 $f(0)=f(1)$，$f(x)$ 在 $x=c$（$0<c<1$）处取得极值。已知对任意 $x\\in(0,1)$，都有 $1\\le |f''(x)|\\le4$。\n\n① 证明：$\\frac13\\le c\\le\\frac23$。  \n② 证明：存在 $\\xi\\in(0,1)$，使得 $|f'''(\\xi)|\\ge\\frac{3|2c-1|}{c^3+(1-c)^3}$。\n\n22\\.（本题满分 12 分）已知矩阵 $A$ 满足 $\\begin{pmatrix}0&0&1\\\\0&1&0\\\\1&0&0\\end{pmatrix}^{2027}A\\begin{pmatrix}0&1&0\\\\0&0&1\\\\1&0&0\\end{pmatrix}^{2027}=\\begin{pmatrix}0&2&2\\\\1&1&2\\\\-1&2&3\\end{pmatrix}$，求矩阵 $A$，并判断 $A$ 是否能相似对角化。\n\n## 卷三\n\n### 选择题\n\n1\\. 设 $c\\ne0$，函数 $f(x)=\\begin{cases}\\frac{\\int_0^{x^2}\\tan\\frac{t}{t+1}\\,\\mathrm{d}t}{x^k},&x>0,\\\\c,&x=0\\end{cases}$ 在 $x=0$ 处连续，则（　）。\n\nA. $k=2,c=\\frac12$  \nB. $k=4,c=\\frac12$  \nC. $k=2,c=1$  \nD. $k=4,c=1$\n\n2\\. 曲线 $y=\\frac{\\mathrm{e}^{\\frac1x}\\arctan x}{x(1-\\mathrm{e}^{\\frac1x})}$ 的渐近线的条数为（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $3$\n\n3\\. 设函数 $f(x)=\\frac{g(x)}{h(x)}$，且 $\\frac{g'(x)}{g(x)}=x$，$\\frac{h'(x)}{h(x)}=\\frac1x$，则 $f(x)$ 满足的微分方程为（　）。\n\nA. $y'=y\\left(x-\\frac1x\\right)$  \nB. $y'=y\\left(x+\\frac1x\\right)$  \nC. $y'=\\frac{x-\\frac1x}{y}$  \nD. $y'=\\frac{x+\\frac1x}{y}$\n74:    - [第四节 微分中值定理及其应用](#pdf-page-147)\n75:        - [4.1 函数的极值及其必要条件](#pdf-page-147)\n76:        - [4.2 微分中值定理](#pdf-page-148)\n5335:<a id=\"pdf-page-147\"></a>\n5368:<a id=\"pdf-page-148\"></a>\n5407:<a id=\"pdf-page-149\"></a>\n5430:<a id=\"pdf-page-150\"></a>\n5468:<a id=\"pdf-page-151\"></a>\n5511:<a id=\"pdf-page-152\"></a>\n5545:<a id=\"pdf-page-153\"></a>\n"}
{"chunk_id":"ca5c1d","wall_time_seconds":0.000009792,"exit_code":0,"original_token_count":362,"output":"bundles\nformats\n1Password 7.app\nAdobe Acrobat DC\nAdobe Acrobat.app\nAdobe Activation Tool.app\nAdobe Creative Cloud\nAdsPower Global.app\nAirBattery.app\nAirCard.app\nAlDente.app\nAmphetamine.app\nArc.app\nBaiduNetdisk_mac.app\nBurp Suite.app\nCC Switch.app\nCLion.app\nChatGPT.app\nClaude.app\nCleanMyMac_5.app\nCodex Computer Use.app\nCodex Tools.app\nCowabunga Lite.app\nCursor.app\nDeepSeek Harness.app\nDingTalk.app\nDownie 4.app\nEudic.app\nFineTune.app\nGemini.app\nGeoGebra Calculator Suite.app\nGitKraken.app\nGo2Shell.app\nGoodnotes.app\nGoogle Chrome.app\nHappaTools.app\nHex Fiend.app\nHopper Disassembler v4.app\nIINA.app\nIntelliJ IDEA.app\nItsycal.app\nMicrosoft Excel.app\nMicrosoft PowerPoint.app\nMicrosoft Word.app\nMinerU.app\nMp3tag.app\nNagram.app\nNeatDownloadManager.app\nNotability: 笔记, PDF.app\nNotion.app\nNutstore.app\nOCS Desktop.app\nObsidian.app\nParallels Desktop.app\nPermute 3.app\nPlistEdit Pro.app\nPyCharm.app\nQQ.app\nQiuChenAppStore.app\nQuantumult X.app\nQuark.app\nQuarkCloudDrive.app\nSafari.app\nScripting.app\nSourcetree.app\nSpeedtest.app\nSurge.app\nT3 Code (Beta).app\nTelegram.app\nTermius.app\nTestFlight.app\nThe Unarchiver.app\nThings3.app\nTor Browser.app\nTypora.app\nUURemote.app\nUtilities\nVisual Studio Code.app\nVorssaint.app\nWake.app\nWeChat.app\nWebStorm.app\nXcode.app\naDrive.app\naTrust.app\nego lite.app\ni4Tools.app\niMazing.app\niShot.app\niTerm.app\nmacOS Assistant.app\nmagpie.app\nrednote.app\n企业微信.app\n哔哩哔哩.app\n学习通.app\n小白羊云盘.app\n"}

## tool · 2026-11-12T13:06:43Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"8eb4ba","wall_time_seconds":0.0000115,"exit_code":0,"original_token_count":4797,"output":"import hashlib\nimport json\nimport os\nimport re\nimport subprocess\nimport sys\nfrom pathlib import Path\nfrom urllib.parse import urlencode\n\n\nWIDE_SOURCE = \"output/302数学二分节真题集（原生LaTeX横屏版）.tex\"\nDEPENDENTS = {\n    WIDE_SOURCE: \"output/302数学二分节真题集（原生LaTeX常规版）.tex\",\n    \"output/302-question-facsimiles.pdf\": \"output/302数学二分节真题集.tex\",\n}\nASSET_NAMES = {\n    WIDE_SOURCE: \"math-ii-past-exams-landscape.pdf\",\n    DEPENDENTS[WIDE_SOURCE]: \"math-ii-past-exams-a4.pdf\",\n    DEPENDENTS[\"output/302-question-facsimiles.pdf\"]: \"math-ii-past-exams-facsimile.pdf\",\n    \"output/27302阶段模拟卷.tex\": \"27302-mock-exam-1.pdf\",\n    \"output/27302阶段模拟卷（第二至五卷及补充练习）.tex\": \"27302-mock-exams-2-5.pdf\",\n}\nVERSION = re.compile(r\"v0\\.0\\.([1-9][0-9]*)\")\n\n\ndef git(repo, *args):\n    return subprocess.check_output([\"git\", *args], cwd=repo, encoding=\"utf-8\")\n\n\ndef plan(repo, before, after):\n    tracked = set(git(repo, \"ls-tree\", \"-rz\", \"--name-only\", after, \"--\", \"output/\").split(\"\\0\"))\n    initial = before == \"0\" * 40\n    changed = tracked if initial else set(git(\n        repo, \"diff\", \"--no-renames\", \"--name-only\", \"-z\", before, after, \"--\", \"output/\"\n    ).split(\"\\0\"))\n    affected = changed | {DEPENDENTS[path] for path in changed & DEPENDENTS.keys()}\n    files = sorted(path for path in affected & tracked if path.endswith(\".tex\"))\n    if not files:\n        return {\"files\": [], \"notes\": \"\"}\n\n    inputs = set(files) | {path for path, entry in DEPENDENTS.items() if entry in files}\n    commits = after if initial else f\"{before}..{after}\"\n    summaries = git(repo, \"log\", \"--reverse\", \"--format=%(trailers:key=Release-Note,valueonly,unfold)\",\n                    commits, \"--\", *sorted(changed & inputs)).splitlines()\n    notes = \"\\n\".join(f\"- {line}\" for line in dict.fromkeys(line.strip() for line in summaries if line.strip()))\n    if not notes:\n        titles = \"、\".join(f\"《{Path(path).stem}》\" for path in files)\n        notes = f\"更新{titles}的 PDF。\"\n    return {\"files\": files, \"notes\": notes}\n\n\ndef next_release(releases, tags, run_id):\n    versions = [release for release in releases if VERSION.fullmatch(release[\"tag_name\"])]\n    marker = f\"\\n\\n<!-- latex-release-run: {run_id} -->\"\n    for release in versions:\n        if (release[\"body\"] or \"\").endswith(marker):\n            return (release[\"tag_name\"], release[\"id\"]) if release[\"draft\"] else (None, None)\n\n    for release in versions:\n        if release[\"draft\"]:\n            raise ValueError(f\"{release['tag_name']} 仍是草稿，请先重跑对应的发布任务。\")\n\n    latest = max((int(VERSION.fullmatch(release[\"tag_name\"])[1]) for release in versions), default=0)\n    if latest >= 999:\n        raise ValueError(\"已达到 v0.0.999，后续版本须经用户批准。\")\n    tag = f\"v0.0.{latest + 1}\"\n    if tag in tags:\n        raise ValueError(f\"标签 {tag} 已存在，但没有对应的 Release。\")\n    return tag, None\n\n\ndef compile_pdfs(files, destination):\n    destination.mkdir()\n    for name in files:\n        source = Path(name)\n        asset = destination / asset_name(name)\n        subprocess.run([\"tectonic\", \"--untrusted\", \"--outdir\", str(destination), \"--\", source.name],\n                       cwd=source.parent, check=True)\n        pdf = destination / source.with_suffix(\".pdf\").name\n        if not pdf.is_file() or pdf.stat().st_size == 0:\n            raise ValueError(f\"未生成 PDF：{source}\")\n        pdf.rename(asset)\n\n\ndef asset_name(source):\n    if source in ASSET_NAMES:\n        return ASSET_NAMES[source]\n    return f\"document-{hashlib.sha256(source.encode()).hexdigest()[:12]}.pdf\"\n\n\ndef github(endpoint, *args):\n    response = subprocess.check_output([\"gh\", \"api\", endpoint, *args], encoding=\"utf-8\")\n    return json.loads(response) if response else None\n\n\ndef publish(release_plan, directory):\n    repository = os.environ[\"GITHUB_REPOSITORY\"]\n    run_id = os.environ[\"GITHUB_RUN_ID\"]\n    endpoint = f\"repos/{repository}/releases\"\n    releases = github(f\"{endpoint}?per_page=100\", \"--paginate\", \"--slurp\")\n2\\. 设 $f(x)$ 为连续函数，且 $\\lim_{x\\to1}\\frac{f(2x-1)}{x-1}=2$，则 $\\lim_{x\\to0}\\frac{f[(1+\\sin x)^2]-f(1+\\sin x)}x=$（　）。\n\nA. $0$  \nB. $2$  \nC. $1$  \nD. $-1$\n\n3\\. 设可导函数 $y=f(x)$ 在 $[a,b]$ 上严格单调递增，$g(y)$ 是 $f(x)$ 的反函数，则 $\\int_a^b f(x)\\,\\mathrm{d}x+\\int_{f(a)}^{f(b)}g(y)\\,\\mathrm{d}y=$（　）。\n<a id=\"pdf-page-147\"></a>\n\n## PDF 第 147 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=147)\n\n11. 求下列函数 $y$ 关于自变量 $x$ 的二阶微分：\n(1) $y = \\frac{\\sin x}{x}$;\n(2) $xy + y^2 = 1$.\n\n(B)\n\n1. 有人说“若 $y = f(x)$ 在点 $x_0$ 可导，则当 $\\Delta x \\to 0$ 时，该函数在点 $x_0$ 的微分 $dy$ 是 $\\Delta x$ 的同阶无穷小。”这种说法是否正确？为什么？\n\n2. 证明：函数 $f: U(x_0) \\to R$ 在 $x_0$ 处可微（可导）的充要条件是存在一个关于 $\\Delta x$ 的线性函数 $L(\\Delta x) = \\alpha \\Delta x$，使\n$$\\lim_{\\Delta x \\to 0} \\frac{|f(x_0 + \\Delta x) - f(x_0) - L(\\Delta x)|}{|\\Delta x|} = 0.$$\n\n第四节 微分中值定理及其应用\n\n我们知道，函数的导数反映了函数在一点附近的局部变化性态，为了利用导数研究函数在某一个区间上整体的变化性态，就需要建立函数在区间上的改变量与导数之间的联系，这就是本节将介绍的几个微分中值定理。微分中值定理在函数的导数与函数在区间上的变化（函数的改变量）之间搭建了一座桥梁，使我们能用导数去研究函数的在一个区间上的某些性态，是利用导数进一步解决函数的许多理论和应用问题的理论基础。\n\n4.1 函数的极值及其必要条件\n\n设有函数 $f: I \\to R, x_0 \\in I$，若 $\\exists \\delta > 0$，使得 $\\forall x \\in U(x_0, \\delta) \\subseteq I$，恒有 $f(x) \\geq f(x_0)$ ($\\leq f(x_0)$），则称 $f$ 在 $x_0$ 取得极小（大）值 $f(x_0)$。$f$ 的极小值与极大值统称为 $f$ 的极值，使 $f$ 取得极值的点 $x_0$ 称为 $f$ 的极值点。\n\n在图 2.12 中，函数 $f$ 在 $x_1, x_3$ 与 $x_5$ 分别取得极大值 $f(x_1), f(x_3)$ 与 $f(x_5)$，在 $x_2$ 与 $x_4$ 分别取得极小值 $f(x_2)$ 与 $f(x_4)$。\n\n应当注意函数的极大（小）值与最大（小）值的区别。函数的极值是就一点的邻域来说的，是局部性概念；而最值（最大、最小值的简称）是对整个区间而言的，是整体性概念。函数在区间 $I$ 内部取得的最值一定是极值，反过来不一定成立。而且同一个函数的极小值有可能大于极大值，在图 2.12 中，极小值 $f(x_4)$ 大于极大值 $f(x_1)$。\n\n设函数 $f$ 在 $(a, b)$ 内可导，从图 2.12 易见，曲线 $y = f(x)$ 上与 $f$ 的极值点 $x_1, x_2, x_3, x_4, x_5$ 相对应的点处有水平切线，受这个事实的启发得到下面的定理。\n\n定理 4.1 (Fermat 定理) 若函数 $f: (a, b) \\to R$ 在 $x_0 \\in (a, b)$ 处取得极值，且 $f$ 在\n\n<a id=\"pdf-page-148\"></a>\n\n## PDF 第 148 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=148)\n\n证 不妨设 $f$ 在 $x_0$ 处取极大值(若 $f$ 在 $x_0$ 处取极小值证法类似), 则\n$\\exists \\delta > 0$, 使得 $\\forall x \\in \\mathring{U}(x_0, \\delta) \\subseteq (a, b)$, 恒有 $f(x) \\leq f(x_0)$.\n若 $x \\in (x_0 - \\delta, x_0)$, 则\n$$\\frac{f(x) - f(x_0)}{x - x_0} \\geq 0,$$\n从而由极限的保号性有\n$$f'_- (x_0) = \\lim_{x \\to x_0} \\frac{f(x) - f(x_0)}{x - x_0} \\geq 0;$$\n若 $x \\in (x_0, x_0 + \\delta)$, 则\n$$\\frac{f(x) - f(x_0)}{x - x_0} \\leq 0,$$\n从而有\n$$f'_+ (x_0) = \\lim_{x \\to x_0} \\frac{f(x) - f(x_0)}{x - x_0} \\leq 0.$$\n由于 $f(x)$ 在 $x_0$ 处可导, 故必有 $f'_- (x_0) = f'_+ (x_0) = f'_- (x_0) = 0.$\n\n4.2 微分中值定理\n\n微分中值定理包括 Rolle 定理、Lagrange 定理与 Cauchy 定理, 下面先介绍 Rolle 定理.\n\nRolle 定理也是受一个简单的几何事实的启发得到的. 设函数 $f$ 在 $[a, b]$ 上连续, 在区间的两个端点处函数值相等. 若曲线 $y = f(x)$ 上与 $(a, b)$ 内任一点 $x$ 相对应的点处都有切线存在, 但无与 $x$ 轴垂直的切线, 则由图 2.13 可见, 该曲线上至少有一点具有水平切线.\n\n定理 4.2 (Rolle 定理) 若函数 $f: [a, b] \\to \\mathbb{R}$ 满足下列条件:\n(1) $f$ 在 $[a, b]$ 上连续; (2) $f$ 在 $(a, b)$ 内可导;\n(3) $f(a) = f(b)$,\n则至少存在一点 $\\xi \\in (a, b)$, 使 $f'(\\xi) = 0.$\n\n注意: 为了利用 $f$ 在 $x_0$ 处取极大值且可导这两个已知条件来证明 $f'_- (x_0) = 0$, 自然应当用导数的定义, 但由于直接用导数定义很难得出此结论, 所以我们转而证明 $f$ 在 $x_0$ 的左导数 $f'_- (x_0) \\geq 0$, 右导数 $f'_+ (x_0) \\leq 0$, 由于 $f$ 在 $x_0$ 处可导, 所以必有 $f'_- (x_0) = 0.$\n\n想一想:\n试举例说明 $f'_- (x_0) = 0$ 只是在 $x_0$ 处可导函数 $f$ 在 $x_0$ 取得极值的必要条件而不是充分条件.\n\n图 2.13\n\n想一想:\n说明将 Rolle 定理中的条件 (1) 与 (2) 换成 “$f$ 在闭区间 $[a, b]$ 上可导”, 定理的结论仍然成立, 试问条件 (1) 与 (2) 换成后者好吗? 有什么缺陷?\n\n<a id=\"pdf-page-149\"></a>\n\n## PDF 第 149 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=149)\n\n证 根据定理4.1, 只要证明 $f$ 在区间 $(a,b)$ 内有极值点就行了. 由已知, $f$ 在 $[a,b]$ 上连续, 故由闭区间上连续函数最大(小)值定理, 必存在 $x_1,x_2 \\in [a,b]$, 使\n$$f(x_1) = \\max_{x \\in [a,b]} f(x) = M, \\quad f(x_2) = \\min_{x \\in [a,b]} f(x) = m.$$\n若 $M = m$, 则 $f$ 在 $[a,b]$ 上为常数, 因此对于 $(a,b)$ 中每个点都可作为 $\\xi$, 使 $f'(\\xi) = 0$.\n若 $M \\neq m$, 则 $M$ 与 $m$ 中至少有一个不等于 $f(a)$, 不妨设 $M \\neq f(a)$ (若 $m \\neq f(a)$, 可类似地证明). 由条件(3)知, $M \\neq f(b)$, 最大值 $M$ 只能被 $f$ 在 $(a,b)$ 内的点 $x_1$ 取得, 故 $x_1$ 也是 $f$ 的极值点. 由定理4.1, $f'(x_1) = 0$.\n由定理4.2 立即可得\n推论4.1 可微函数 $f$ 的任意两个零点之间至少有导函数 $f'$ 的一个零点.\n例4.1 证明方程 $x^3 + 2x + 1 = 0$ 在区间 $(-1,0)$ 内有且只有一个实根.\n证 设 $f(x) = x^3 + 2x + 1$, 则 $f(-1) = -2 < 0, f(0) = 1 > 0$. 根据连续函数的零点定理, 在 $(-1,0)$ 内 $f$ 至少有一个零点, 即方程 $x^3 + 2x + 1 = 0$ 在 $(-1,0)$ 内至少有一个根, 设其为 $x_1$. 下面证明该方程在 $(-1,0)$ 内只有一个根. 若它还有一个根 $x_2$, 则由推论4.1, 在 $x_1$ 与 $x_2$ 之间至少有一点 $\\xi$, 使 $f'(\\xi) = 0$. 然后, $f'(x) = 3x^2 + 2 > 0$, 即 $f'$ 在 $(-1,0)$ 内没有零点, 从而得到矛盾. 所以, 在 $(-1,0)$ 内该方程有且仅有一个实根.\n例4.2 证明: 若函数 $f: [0,1] \\rightarrow \\mathbf{R}$ 在 $[0,1]$ 上连续, 在 $(0,1)$ 内可导, 并且 $f(1) = 0$, 则至少存在一个 $c \\in (0,1)$, 使\n$$f'(c) = -\\frac{f(c)}{c}.$$\n证 先作一简单的分析. 为了证明结论成立, 由于 $c \\neq 0$, 只要证明 $cf'(c) + f(c) = 0$ 就行了. 又因为\n$$cf'(c) + f(c) = [xf(x)]'|_{x=c},$$\n所以只要证明 $F(x) = xf(x)$ 满足 Rolle 定理条件就行了. 显然, $F$ 在 $[0,1]$ 上连续, 在 $(0,1)$ 内可导, 又 $F(0) = F(1) = 0$, 根据 Rolle 定理, 至少存在一点 $c \\in (0,1)$, 使 $F'(c) = 0$. 又 $F'(x) = xf'(x) + f(x)$, 故结论成立.\n注: 证明例4.2的关键在于通过将要证明的等式变形和分析, 构造满足 Rolle 定理条件的辅助函数\n$$F(x) = xf(x).$$\n注意: Rolle 定理的三个条件中只要有一个不满足, 都不能保证定理的结论成立. 例如, 在图2.14的 $(a), (b)$ 与 $(c)$ 中, 分别画出了不满足条件(1), (2)与(3)之一的三个函数的图像, 显然, 这三个函数都不存在使定理结论成立的 $\\xi$.\n\n<a id=\"pdf-page-150\"></a>\n\n## PDF 第 150 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=150)\n\n在图 2.14 的 (c) 中, 由于 $f(a) \\neq f(b)$, 曲线 $y=f(x)$ 上没有一点的切线平行于 $x$ 轴. 但是, 不难看到, 曲线上至少有一点 (如点 $P_1$ 或 $P_2$) 处的切线平行于弦 $AB$. 由于弦 $AB$ 的斜率是 $\\frac{f(b)-f(a)}{b-a}$, 该曲线在点 $P_1$ 与 $P_2$ 处切线的斜率为 $f'(\\xi)$, 故有\n\n$$\\frac{f(b)-f(a)}{b-a}=f'(\\xi), \\quad \\xi \\in(a,b).$$\n\n图 2.14\n\n由此, 我们得到下面的重要定理:\n\n定理 4.3 (Lagrange 定理) 若函数 $f:[a,b] \\to \\mathbf{R}$ 满足下列条件:\n\n(1) $f$ 在 $[a,b]$ 上连续; (2) $f$ 在 $(a,b)$ 内可导, 则至少存在一点 $\\xi \\in(a,b)$, 使\n\n$$f(b)-f(a)=f'(\\xi)(b-a).$$\n\n(4.1)\n\n分析 为了证明结论成立, 由于 $b-a \\neq 0$, 只要证明至少存在一点 $\\xi$, 使\n\n$$\\frac{f(b)-f(a)}{b-a}-f'(\\xi)=0$$\n\n就行了. 又因为\n\n$$\\frac{f(b)-f(a)}{b-a}-f'(\\xi)=\\left[\\frac{f(b)-f(a)}{b-a}x-f(x)\\right]'|_{x=\\xi},$$\n\n所以, 只要证明 $F(x)=\\frac{f(b)-f(a)}{b-a}x-f(x)$ 在 $[a,b]$ 上满足 Rolle 定理的条件就行了.\n\n证 作辅助函数\n\n$$F(x)=\\frac{f(b)-f(a)}{b-a}x-f(x).$$\n\n显然, 函数 $F$ 满足 Rolle 定理的条件 (1) 与 (2). 又\n\n<a id=\"pdf-page-151\"></a>\n\n## PDF 第 151 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=151)\n\n$F(a) = \\frac{f(b) - f(a)}{b - a} a - f(a) = \\frac{af(b) - bf(a)}{b - a},$\n$F(b) = \\frac{f(b) - f(a)}{b - a} b - f(b) = \\frac{af(b) - bf(a)}{b - a},$\n\n故 $F(a) = F(b)$. 由 Rolle 定理，至少存在一点 $\\xi \\in (a,b)$, 使 $F'(\\xi) = 0$, 即\n$\\frac{f(b) - f(a)}{b - a} - f'(\\xi) = 0,$\n\n从而有 $f(b) - f(a) = f'(\\xi)(b - a)$.\n\n证明定理 4.3 的辅助函数的选取不是唯一的. 事实上, 由于\n$\\left[f(x) - f(a) - \\frac{f(b) - f(a)}{b - a}(x - a)\\right]' \\bigg|_{x = \\xi} = f'(\\xi) - \\frac{f(b) - f(a)}{b - a},$\n\n因此, 也可用\n$F(x) = f(x) - \\left[f(a) + \\frac{f(b) - f(a)}{b - a}(x - a)\\right]$\n\n作为辅助函数. 而且此函数就是曲线 $y = f(x)$ 与弦 $AB$ 方程之差, 显然满足 Rolle 定理的条件.\n\n在 Lagrange 定理中, 若 $f(a) = f(b)$, 则有 $f'(\\xi) = 0$. 因此, Rolle 定理是 Lagrange 定理的特例, 而 Lagrange 定理是 Rolle 定理的推广.\n\n公式 (4.1) 称为 Lagrange 公式. 将两边同乘 -1 得\n$f(a) - f(b) = f'(\\xi)(a - b),$\n\n这就是说, 无论是 $a < b$ 还是 $a > b$, Lagrange 公式均成立.\n\nLagrange 公式还可以写成其他形式. 由于 $\\xi \\in (a,b)$, 所以 $0 < \\frac{\\xi - a}{b - a} < 1$. 令 $\\theta = \\frac{\\xi - a}{b - a}$, 则 $\\xi = a + \\theta(b - a)$, 于是有\n$f(b) - f(a) = f'[a + \\theta(b - a)](b - a) \\quad (0 < \\theta < 1).$ (4.2)\n\n如果取 $a = x, b = x + \\Delta x$, Lagrange 公式又可写成\n$f(x + \\Delta x) - f(x) = f'(x + \\theta \\Delta x)\\Delta x \\quad (0 < \\theta < 1),$ (4.3)\n\n常称 (4.3) 式为有限改变量公式. 它建立了函数 $y = f(x)$ 在区间上的改变量与导数之间的关系, 使我们能够用导数研究函数在区间上的变化性态.\n\n推论 4.2 设 $f: I \\rightarrow R$ 在 $I$ 上连续, 在 $I$ 内可导, 则在 $I$ 内 $f'(x) \\equiv 0$ 的充要条件为\n\n**页边注**\n\n注：定理4.3的证明思路也是将要证明的等式（4.1）变形，构造一个满足Rolle定理条件的辅助函数，关键在于如何构造符合要求的辅助函数.通过将要证明的结论变形、分析是常用的一种方法，称为分析法，另一种是几何法，定理 4.3证明之后给出的另一个辅助函数就是受几何上的启示构造出来的.\n\n<a id=\"pdf-page-152\"></a>\n\n## PDF 第 152 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=152)\n\n证 充分性是显然的，下面证明必要性.\n任取 $x_1, x_2 \\in I$, 在闭区间 $[x_1, x_2]$ 上对 $f$ 应用 Lagrange 定理, 存在 $\\xi \\in (x_1, x_2) \\subseteq (a, b)$, 使\n$$f(x_2) - f(x_1) = f'(\\xi)(x_2 - x_1) = 0,$$\n因此, $f(x_1) = f(x_2)$. 由 $x_1, x_2$ 的任意性知 $f$ 在 $I$ 上是常数.\n\n推论 4.3 设函数 $f$ 在 $[x_0, b)$ (或 $(a, x_0]$) 上连续, 在 $(x_0, b)$ (或 $(a, x_0)$) 内可导, 且 $\\lim_{x \\to x_0^+} f'(x) = A$ (或 $\\lim_{x \\to x_0^-} f'(x) = A$), 则\n\n$f'_+ (x_0) = \\lim_{x \\to x_0^+} f'(x) = A$ (或 $f'_- (x_0) = \\lim_{x \\to x_0^-} f'(x) = A$),\n其中 $A$ 为有限或无限.\n\n证 根据公式 (4.3), 我们有\n$$\\frac{f(x_0 + \\Delta x) - f(x_0)}{\\Delta x} = f'(x_0 + \\theta \\Delta x) \\quad (0 < \\theta < 1).$$\n\n所以\n$$f'_+ (x_0) = \\lim_{\\Delta x \\to 0^+} \\frac{f(x_0 + \\Delta x) - f(x_0)}{\\Delta x} = \\lim_{\\Delta x \\to 0^+} f'(x_0 + \\theta \\Delta x) = A.$$\n\n同样, 可证明关于左导数的结论.\n\n前面曾经指出, 在研究分段函数的可导性时, 对于使函数有不同表达式的子区间的分界点处的可导性, 通常需要利用导数的定义来讨论. 但是, 如果函数满足推论 4.3 的条件, 那么, 利用该推论研究分界点处的可导性比用导数定义更为简便, 下面举一个例子来说明.\n\n例 4.3 设\n$$f(x) = \\begin{cases} x^2, & x < 0, \\\\ 0, & x = 0, \\\\ x \\sin x, & x > 0, \\end{cases}$$\n\n求 $f'(x)$.\n\n解 当 $x < 0$ 时, $f'(x) = 2x$; 当 $x > 0$ 时, $f'(x) = \\sin x + x \\cos x$. 由于 $\\lim_{x \\to 0^-} f'(x) = \\lim_{x \\to 0^-} 2x = 0$, $\\lim_{x \\to 0^+} f'(x) = \\lim_{x \\to 0^+} (\\sin x + x \\cos x) = 0$, 在区间 $[0, b)$ ($b > 0$) 与 $(a, 0]$ ($a < 0$) 上分别应用推论 4.3, 则有\n$$f'_+ (0) = \\lim_{x \\to 0^+} f'(x) = 0, \\quad f'_- (0) = \\lim_{x \\to 0^-} f'(x) = 0.$$\n\n<a id=\"pdf-page-153\"></a>\n\n## PDF 第 153 页\n\n[查看原页](%E5%B7%A5%E7%A7%91%E6%95%B0%E5%AD%A6%E5%88%86%E6%9E%90%E5%9F%BA%E7%A1%80%E7%AC%AC%E4%B8%89%E7%89%88%20%E4%B8%8A%E5%86%8C%EF%BC%88%E5%90%AB%E5%A4%A7%E7%BA%B2%EF%BC%89.pdf#page=153)\n\n故\n$$f'(x) = \\begin{cases} 2x, & x < 0, \\\\ 0, & x = 0, \\\\ \\sin x + x\\cos x, & x > 0. \\end{cases}$$\n\nLagrange 定理是最常用的一个微分中值定理，具有重要的理论和应用价值. 下面举例说明它在证明不等式、判断方程根的存在性等方面的应用.\n\n例 4.4 证明: 当 $x > 0$ 时,\n\n$$\\frac{x}{1+x} < \\ln(1+x) < x.$$\n\n证 由于 $\\ln(1+x) = \\ln(1+x) - \\ln 1$, 所以为了证明本题中的不等式, 只要取 $f(t) = \\ln(1+t)$ 为辅助函数, 并对该函数在 $[0,x]$ 上应用 Lagrange 定理. 容易验证 $f(t)$ 在 $[0,x]$ 上满足 Lagrange 定理的条件, 因而至少存在一点 $\\xi \\in (0,x)$, 使\n\n$$f(x) - f(0) = f'(\\xi)(x - 0),$$\n\n即\n\n$$\\ln(1+x) = \\frac{x}{1+\\xi}.$$\n\n又因为 $\\xi \\in (0,x)$, 故有\n"}

## tool · 2026-11-12T13:06:51Z


Script completed
Wall time 1.4 seconds
Output:

{"chunk_id":"500e0e","wall_time_seconds":1.002402625,"session_id":45434,"original_token_count":0,"output":""}
{"chunk_id":"10a0c1","wall_time_seconds":0.038183041,"exit_code":0,"original_token_count":0,"output":""}

## tool · 2026-11-12T13:07:14Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"a8f9bf","wall_time_seconds":0.000011083,"exit_code":1,"original_token_count":1274,"output":"# PDF 批量提取\n\n## 当前任务：分节真题难度与详细解析\n\n原位更新 234 题共用的原生 LaTeX 源稿和横屏 PDF（含现有 iPad 交付路径）；A4 入口同步编译验证。不改原卷题号、题面和节归属。每题增加 1–5 个文字 `*`，依据知识要求、推理层数、计算量和易错点评级，各节按难度稳定升序。解析依次交代已知与目标、方法及条件、完整推导、结论与检查，首次用到的必要术语作通俗解释。统一算式中的上下分式，检查紧缩分式与指数中的除法。\n\n按第一章、第二章、第三章、第四章分区校订；各区仅修改所属题目。汇总后核对题目集合、解析对应、难度顺序、公式结构，编译两种版式并检查日志、PDF 文本与内容边界。不进行未授权的截图或图像检查。完成后提交并普通推送当前 origin/main。\n\n递归处理源目录的 PDF，在 `27302模拟` 中按相同相对路径生成 Markdown。保留各排版版本和答案文件，内容相同的 PDF 复用识别结果。每页链接至对应源 PDF 页码。\n\n## 09–26 年真题与解析\n\n递归将 `考研数学一二三09-26年真题&解析` 下的 PDF 转到 `302真题`，维持一份 PDF 对应一份 Markdown。直接提取正常文字层，对扫描页和文字层明显损坏的页面，用 PyMuPDF 渲染后交给本机 Vision 识别。\n\n# 进度\n\n## 当前任务：分节真题难度与详细解析\n\n- [x] 核实共用源稿有 234 题、19 节，两种版式共用题库；Git 初始存在裁片 PDF 删除及未跟踪 iPad 目录。\n- [x] 234 题逐题补充四部分解析、难度与上下分式；中断时未完成移动的 2023 年第 5 题、2019 年第 13 题已按原题恢复并扩写。\n- [x] 完成全部节内稳定排序，同星保留原序，题头用计数器连续编号。星级 1–5 依次为 6、110、88、29、1 题。\n- [x] 与任务开始前 HEAD 对照 234 份题面，题干、选项、图形内容均保持原文；第四章独立复核完成，48 项计算检查通过。\n- [x] 五项回归检查通过；横屏 488 页、A4 471 页编译成功，日志无缺字、警告或溢出。逐题检查题头、解析、星级、下一页开始、23 个书签及页面边界，并用字形和分数线坐标检查上下分式。已覆盖现有横屏及 iPad PDF，未做截图或实机验证。\n- [x] 题集及验证记录已提交为 `a8e4665` 并普通推送至 `origin/main`。任务开始前的裁片 PDF 删除及另一份未跟踪 iPad 模拟卷均保持原状态；提交哈希补记另作后续文档提交。\n\n- 已用《李林880数二高数篇做题本》和《考研数学冲刺预测6套卷》验证文字层提取及本地 OCR。\n- 已生成 63 份 Markdown。用两种 PDF 渲染方式完成 OCR，补提取了题目汇总和平板版讲义中的图片正文。\n- 已核对全部 16,915 个页段及原页链接。11,250 页使用文字层，5,661 页使用 OCR，4 页标记为无可提取文字。\n# 工具\n\n本次分节真题详细解析按章节使用并行代理技能分区校订，主代理统一评级规则、题头、检查和编译。使用已有 Tectonic、PyMuPDF 与 Python 标准库；不进行截图或图像检查。\n\n使用 PyMuPDF 提取 PDF 文字层，使用 macOS Vision 在本机识别扫描页。源 PDF 保留在原目录。\n\n本次张宇往年八套由单一代理逐题检查，使用 PyMuPDF 原页图和文字层、嵌入图示哈希及现有 KaTeX 脚本验证，未调用其他代理。\n\n数学模拟卷补用本机 MLX PaddleOCR 生成候选，再逐题对照源 PDF 修正；候选不能作为完成证据。使用 KaTeX 验证 Markdown 公式渲染。往年合集按独立文件分工校对，选填交付文件统一由一名代理组装。\n\n阶段模拟卷使用 LaTeX 和 ctex 排版，使用桌面应用附带的 Tectonic 编译，使用 PyMuPDF 检查 PDF 题序和文本边界。\n\n自动发布使用 GitHub Actions、Tectonic 0.17.0、Python 标准库和 GitHub CLI，PDF 作为 GitHub Release 附件分发。\n# 完成标准\n\n## 当前任务：分节真题难度与详细解析\n\n- 234 个原卷年份与题号组合保持一致，各题保留原小节、题干、选项、图形和全部小问；234 份解析与题目一一对应。\n- 题头均有 1–5 个文字 `*`，各节难度非递减；同难度保留原顺序；显示题序连续。\n- 每份解析包含条件与目标、方法依据、必要中间计算、明确结论和针对性检查；逐题校订，客观结构检查不能替代数学正确性检查。\n- 数学算式不使用斜杠分数、Unicode 分数字符或紧缩的 `\\tfrac`；分子分母及指数分组正确。\n- 横屏和 A4 实际编译成功，无缺字或内容溢出；检查 PDF 234 个题头、解析对应与难度顺序、书签和文字边界。未授权视觉检查，不截图。\n- 保留用户已有的裁片 PDF 删除及 iPad 目录其他内容，只提交任务相关文件。\nTraceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nModuleNotFoundError: No module named 'fitz'\n"}
{"chunk_id":"affd9c","wall_time_seconds":0.000021,"exit_code":0,"original_token_count":16,"output":"/Applications/ChatGPT.app/Contents/Resources/tectonic/tectonic\n"}

## tool · 2026-11-12T13:07:48Z


Script completed
Wall time 0.6 seconds
Output:

{"chunk_id":"08ebb6","wall_time_seconds":0.141646875,"exit_code":0,"original_token_count":585,"output":"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/proof-venv/lib/python3.12/site-packages/fitz/__init__.py:17: FutureWarning: The `fitz` API is deprecated and will be removed in future. Use `import pymupdf` instead.\n  warnings.warn(\nTraceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nModuleNotFoundError: No module named 'mpmath'\nProcess a (La)TeX document\n\nUsage: tectonic [OPTIONS] <INPUT>\n\nArguments:\n  <INPUT>  The file to process, or \"-\" to process the standard input stream\n\nOptions:\n  -X                                Use experimental V2 interface (see `tectonic -X --help`)\n  -c, --chatter <CHATTER_LEVEL>     How much chatter to print when running [default: default]\n      --color <CLI_COLOR>           Enable/disable colorful log output [default: auto] [possible values: always, auto, never]\n  -f, --format <path>               The name of the \"format\" file used to initialize the TeX engine [default: latex]\n  -b, --bundle <BUNDLE>             Use this URL or path to find resource files instead of the default\n  -C, --only-cached                 Use only resource files cached locally\n      --outfmt <format>             The kind of output to generate [default: pdf]\n      --makefile-rules <dest_path>  Write Makefile-format rules expressing the dependencies of this run to <dest_path>\n      --pass <PASS>                 Which engines to run [default: default]\n  -r, --reruns <count>              Rerun the TeX engine exactly this many times after the first\n  -k, --keep-intermediates          Keep the intermediate files generated during processing\n      --keep-logs                   Keep the log files generated during processing\n      --synctex                     Generate SyncTeX data\n      --hide <hide_path>            Tell the engine that no file at <hide_path> exists, if it tries to read it\n  -p, --print                       Print the engine's chatter during processing\n  -o, --outdir <outdir>             The directory in which to place output files [default: the directory containing <input>]\n      --untrusted                   Input is untrusted -- disable all known-insecure features\n  -Z <option>                       Unstable options. Pass -Zhelp to show a list\n  -h, --help                        Print help\n  -V, --version                     Print version\n"}
{}
{"chunk_id":"76cc94","wall_time_seconds":0.015676833,"exit_code":1,"original_token_count":962,"output":"\n======================================================================\nERROR: test_three_complete_papers (__main__.MeanValueExamTests) (path='中值定理阶段模拟卷1.tex')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.github/scripts/test_mean_value_exams.py\", line 14, in test_three_complete_papers\n    source = path.read_text()\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1256, in read_text\n    with self.open(mode='r', encoding=encoding, errors=errors) as f:\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1242, in open\n    return io.open(self, mode, buffering, encoding, errors, newline,\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1110, in _opener\n    return self._accessor.open(self, flags, mode)\nFileNotFoundError: [Errno 2] No such file or directory: '/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷1.tex'\n\n======================================================================\nERROR: test_three_complete_papers (__main__.MeanValueExamTests) (path='中值定理阶段模拟卷2.tex')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.github/scripts/test_mean_value_exams.py\", line 14, in test_three_complete_papers\n    source = path.read_text()\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1256, in read_text\n    with self.open(mode='r', encoding=encoding, errors=errors) as f:\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1242, in open\n    return io.open(self, mode, buffering, encoding, errors, newline,\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1110, in _opener\n    return self._accessor.open(self, flags, mode)\nFileNotFoundError: [Errno 2] No such file or directory: '/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷2.tex'\n\n======================================================================\nERROR: test_three_complete_papers (__main__.MeanValueExamTests) (path='中值定理阶段模拟卷3.tex')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.github/scripts/test_mean_value_exams.py\", line 14, in test_three_complete_papers\n    source = path.read_text()\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1256, in read_text\n    with self.open(mode='r', encoding=encoding, errors=errors) as f:\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1242, in open\n    return io.open(self, mode, buffering, encoding, errors, newline,\n  File \"/Applications/Xcode.app/Contents/Developer/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/pathlib.py\", line 1110, in _opener\n    return self._accessor.open(self, flags, mode)\nFileNotFoundError: [Errno 2] No such file or directory: '/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷3.tex'\n\n----------------------------------------------------------------------\nRan 1 test in 0.002s\n\nFAILED (errors=3)\n"}

## assistant · 2026-11-12T13:07:57Z

已选定三卷共 36 题，重点覆盖极限、连续与可导的关系、复合及隐函数求导、中值定理证明。部分原题会改成解答题或只保留范围内的小问，并注明改动；需要处理高阶小量的题，会直接用 Cauchy 中值定理推导。


## tool · 2026-11-12T13:10:21Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-12T13:10:28Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"32ff56","wall_time_seconds":0,"exit_code":101,"original_token_count":850,"output":"2:% 题源根目录：references/302模拟27md/\n3:% 武忠祥基础：2027模考/武忠祥/27考研基础摸底测试（高数、线代）/27考研基础摸底测试（高数、线代）数二.pdf.md\n4:% 武忠祥8月：2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\n5:% 李林：2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\n6:% 张宇：2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\n7:% 李艳芳：2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\n24:\\newcommand{\\Question}[4]{\\clearpage\\def\\CurrentNumber{#1}\\def\\CurrentSource{#4}\\pdfbookmark[1]{第#1题}{q#1}{\\small\\color{accent}模拟卷 1\\hfill #2 · #3 分}\\par{\\Large\\bfseries 第 #1 题}\\par\\medskip\\fontsize{14}{22}\\selectfont}\n25:\\newcommand{\\Solution}{\\clearpage\\fontsize{12}{18}\\selectfont{\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par{\\footnotesize\\color{gray}题源：\\CurrentSource}\\par\\smallskip}\n45:题目选自本地 \\texttt{references/302模拟27md}，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。\n47:\\Question{1}{单项选择}{5}{武忠祥基础摸底测试数二，第 1 题；原题}\n50:\\Solution\n62:于是两式比值趋于 $\\frac{1/6}{-b}$。其中分子 $1/6$ 表示 $\\frac16$，故 $-b=\\frac16$。\n65:\\Question{2}{单项选择}{5}{武忠祥基础摸底测试数二，第 2 题；原题}\n68:\\Solution\n83:\\Question{3}{单项选择}{5}{张宇八套卷数二，卷一第 2 题；原题}\n86:\\Solution\n100:\\Question{4}{单项选择}{5}{李艳芳三套卷数二，卷二第 2 题；原题}\n107:\\Solution\n127:\\Question{5}{填空}{5}{李林六套卷数二，第一套第 11 题；原题}\n133:\\Solution\n147:\\Question{6}{填空}{5}{李林六套卷数二，第四套第 12 题；明确 n 为非负整数}\n152:\\Solution\n172:\\Question{7}{填空}{5}{张宇八套卷数二，卷六第 13 题；原题}\n177:\\Solution\n182:\\frac{\\mathrm dy}{\\mathrm dx}=\\frac{2t\\mathrm e^{t^2}}{1/t}\n185:上式中的 $1/t$ 即 $\\frac1t$。再对这个一阶导数关于 $x$ 求导，\n195:\\Question{8}{填空}{5}{张宇八套卷数二，卷八第 11 题；原题}\n200:\\Solution\n217:\\Question{9}{解答}{15}{武忠祥基础摸底测试数二，第 17 题；原题，分值重设}\n222:\\Solution\n243:\\Question{10}{解答}{15}{李林六套卷数二，第二套第 3 题；选择题改为分步解答}\n253:\\Solution\n258:f(x)=\\begin{cases}\\frac x3(1-\\mathrm e^{x/3}),&x<0,\\\\x(\\mathrm e^x-1),&x\\ge0.\\end{cases}\n264:f'(x)=\\begin{cases}\\frac13(1-\\mathrm e^{x/3})-\\frac x9\\mathrm e^{x/3},&x<0,\\\\\\mathrm e^x-1+x\\mathrm e^x,&x>0.\\end{cases}\n274:\\Question{11}{解答}{15}{武忠祥8月强化突击测试，第 4 题第（1）问；补充 a>0，分值重设}\n279:\\Solution\n300:\\Question{12}{解答}{15}{武忠祥8月强化突击测试，第 5 题第（I）问；只取不含积分的小问}\n305:\\Solution\nnote: using only cached resource files\n\nthread 'main' (1596117) panicked at src/config.rs:154:18:\ncalled `Result::unwrap()` on an `Err` value: failed to create directory `/Users/oyamahappa/Library/Caches/TectonicProject.Tectonic/bundles/hashes` or one of its parents\n\nCaused by:\n    Operation not permitted (os error 1)\nnote: run with `RUST_BACKTRACE=1` environment variable to display a backtrace\n"}

## tool · 2026-11-12T13:11:06Z


Script completed
Wall time 19.9 seconds
Output:

{}
{"chunk_id":"407761","wall_time_seconds":1.002769292,"session_id":21714,"original_token_count":10,"output":"note: using only cached resource files\n"}

## tool · 2026-11-12T13:13:48Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-12T13:14:19Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"84a279","wall_time_seconds":0.000248583,"exit_code":1,"original_token_count":24,"output":"note: generating format \"latex\"\nerror: failed to open input file \"tectonic-format-latex.tex\"\n"}
{"chunk_id":"94141d","wall_time_seconds":0.000017083,"exit_code":0,"original_token_count":638,"output":"2:% 题源根目录：references/302模拟27md/\n3:% 武忠祥8月：2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\n4:% 李林：2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\n5:% 张宇：2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\n6:% 李艳芳：2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\n19:\\newcommand{\\Question}[4]{\\clearpage\\def\\CurrentNumber{#1}\\def\\CurrentSource{#4}\\pdfbookmark[1]{第#1题}{q#1}{\\small\\color{accent}模拟卷 2\\hfill #2 · #3 分}\\par{\\Large\\bfseries 第 #1 题}\\par\\medskip\\fontsize{14}{22}\\selectfont}\n20:\\newcommand{\\Solution}{\\clearpage\\fontsize{12}{18}\\selectfont{\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par{\\footnotesize\\color{gray}题源：\\CurrentSource}\\par\\smallskip}\n40:题目选自本地 \\texttt{references/302模拟27md}，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。\n42:\\Question{1}{单项选择}{5}{李林六套卷数二，第一套第 2 题；原题}\n53:\\Solution\n69:\\Question{2}{单项选择}{5}{李林六套卷数二，第二套第 1 题；补明定义域 x≠0}\n76:\\Solution\n88:\\Question{3}{单项选择}{5}{张宇八套卷数二，卷六第 2 题；原题}\n91:\\Solution\n105:\\Question{4}{单项选择}{5}{李艳芳三套卷数二，卷一第 1 题；原题}\n112:\\Solution\n127:\\Question{5}{填空}{5}{张宇八套卷数二，卷四第 13 题；原题}\n131:\\Solution\n145:\\Question{6}{填空}{5}{张宇八套卷数二，卷五第 11 题；原题}\n149:\\Solution\n165:\\Question{7}{填空}{5}{李艳芳三套卷数二，卷一第 11 题；原题}\n171:\\Solution\n187:\\Question{8}{填空}{5}{武忠祥8月强化突击测试，第 1 题；原题}\n198:\\Solution\n210:\\Question{9}{解答}{15}{李林六套卷数二，第六套第 17 题；原题，分值重设}\n216:\\Solution\n233:\\Question{10}{解答}{15}{张宇八套卷数二，卷八第 17 题；原题，分值重设}\n239:\\Solution\n259:\\Question{11}{解答}{15}{张宇八套卷数二，卷五第 17 题；原题，分值重设}\n269:\\Solution\n286:\\Question{12}{解答}{15}{武忠祥8月强化突击测试，第 4 题第（2）问；补充 a>0，分值重设}\n291:\\Solution\nhead: .question-bank-work/中值定理阶段模拟卷1.log: No such file or directory\n.question-bank-work/proof-venv/bin/python\n.question-bank-work/proof-venv/bin/python3\n.question-bank-work/proof-venv/bin/python3.12\n"}

## assistant · 2026-11-12T13:14:24Z

前两卷的题目与解析已写入源稿，第三卷正在编排。目前逐题检查了导数、极限系数和定理条件。编译发现现有缓存目录还需确认，接下来会处理编译环境，并检查 PDF 是否严格按“题页—解析页”交替。


## tool · 2026-11-12T13:14:27Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"a4154e","wall_time_seconds":0.000016291,"exit_code":0,"original_token_count":244,"output":"total 0\ndrwxr-xr-x    4 oyamahappa  staff   128 Nov 10 23:30 .\ndrwxr-xr-x  297 oyamahappa  staff  9504 Nov 12 20:05 ..\ndrwxr-xr-x    4 oyamahappa  staff   128 Nov 10 23:30 bundles\ndrwxr-xr-x    3 oyamahappa  staff    96 Nov 10 23:35 formats\ntotal 47760\ndrwxr-xr-x  3 oyamahappa  staff        96 Nov 10 23:35 .\ndrwxr-xr-x  4 oyamahappa  staff       128 Nov 10 23:30 ..\n-rw-------  1 oyamahappa  staff  24451466 Nov 10 23:35 6ffe055852f8faf66c0acbe1a7fb27f87b869a90bad1204f3bf4d9683f597c7c-latex-33.fmt\ntotal 0\ndrwxr-xr-x  4 oyamahappa  staff  128 Nov 10 23:30 .\ndrwxr-xr-x  4 oyamahappa  staff  128 Nov 10 23:30 ..\ndrwxr-xr-x  5 oyamahappa  staff  160 Nov 10 23:30 data\ndrwxr-xr-x  4 oyamahappa  staff  128 Nov 10 23:30 hashes\nls: /Users/oyamahappa/Library/Caches/Tectonic: No such file or directory\ntotal 0\ndrwxr-xr-x   3 oyamahappa  staff    96 Nov 12 21:11 .\ndrwx------+ 92 oyamahappa  staff  2944 Nov 12 21:12 ..\ndrwxr-xr-x   4 oyamahappa  staff   128 Nov 12 21:11 bundles\n"}

## tool · 2026-11-12T13:14:37Z


Script completed
Wall time 3.1 seconds
Output:

{"chunk_id":"0f253b","wall_time_seconds":2.516743666,"exit_code":0,"original_token_count":300,"output":".invalid rule day julian dayi64 is out of range for i32out of range operationinvalid offset hourinvalid offset minuteinvalid offset secondinvalid day time hourinvalid day time minuteinvalid day time second/usr/share/zoneinfo/share/zoneinfo/etc/zoneinfo/usr/share/lib/zoneinfolocaltime/etc/localtimetime zone name must have between 3 and 7 charactersinvalid characters in time zone nameinvalid UTC offsetout of range operationlist of local time types must not be emptyinvalid leap secondextra transition rule is inconsistent with the last transitioninvalid transitioninvalid local time type indexcapacity overflowstream did not contain valid UTF-8a formatting trait implementation returned an error when the underlying stream did notfailed to fill whole bufferTectonicProjectTECTONIC_CACHE_DIRUnable to find standard directories for platform!\ntotal 16\ndrwxr-xr-x  4 oyamahappa  staff  128 Nov 10 23:30 .\ndrwxr-xr-x  4 oyamahappa  staff  128 Nov 10 23:30 ..\n-rw-r--r--  1 oyamahappa  staff   10 Nov 10 23:30 https,58,,47,,47,relay.fullyjustified.net,47,default_bundle_v33.lock\n-rw-r--r--  1 oyamahappa  staff   65 Nov 10 23:30 https,58,,47,,47,relay.fullyjustified.net,47,default_bundle_v33.tar\n2.1\n"}
{"chunk_id":"1424ef","wall_time_seconds":0.273316167,"exit_code":1,"original_token_count":654,"output":"note: using only cached resource files\nnote: Running TeX ...\nerror: 中值定理阶段模拟卷1.tex:29: LaTeX Error: Command \\Check already defined.\n               Or name \\end... illegal, see p.192 of the manual.\n\nSee the LaTeX manual or LaTeX Companion for explanation.\nType  H <return>  for immediate help\nnote: Writing `.question-bank-work/中值定理阶段模拟卷1.log` (15.2607421875 KiB)\nerror: something bad happened inside XeTeX; its output follows:\n\n===============================================================================\n(中值定理阶段模拟卷1.tex\nLaTeX2e <2021-11-15> patch level 1\nL3 programming layer <2022-02-24> (ctexart.cls (ctexbackend.cfg) (expl3.sty\n(l3backend-xetex.def))\nDocument Class: ctexart 2021/12/12 v2.5.8 Chinese adapter for class article (CT\nEX)\n(xparse.sty) (l3keys2e.sty) (ctexhook.sty) (ctexpatch.sty) (fix-cm.sty\n(ts1enc.def)) (ctexopts.cfg) (article.cls\nDocument Class: article 2021/10/04 v1.4n Standard LaTeX document class\n(size12.clo)) (ctex-engine-xetex.def (xeCJK.sty (xtemplate.sty) (fontspec.sty\n(fontspec-xetex.sty (fontenc.sty) (fontspec.cfg))) (xeCJK.cfg))) (zhnumber.sty\n(zhnumber-utf8.cfg)) (ctex-scheme-chinese-article.def (ctex-name-utf8.cfg))\n(ctex-cs4size.clo) (ctex-fontset-fandol.def)) (ctex.cfg) (geometry.sty\n(keyval.sty) (ifvtex.sty (iftex.sty))) (amsmath.sty\nFor additional information on amsmath, use the `?' option.\n(amstext.sty (amsgen.sty)) (amsbsy.sty) (amsopn.sty)) (amssymb.sty\n(amsfonts.sty)) (xcolor.sty (color.cfg) (xetex.def)) (fancyhdr.sty)\n(enumitem.sty) (hyperref.sty (ltxcmds.sty) (pdftexcmds.sty (infwarerr.sty))\n(kvsetkeys.sty) (kvdefinekeys.sty) (pdfescape.sty) (hycolor.sty)\n(letltxmacro.sty) (auxhook.sty) (kvoptions.sty) (pd1enc.def) (intcalc.sty)\n(etexcmds.sty) (puenc.def) (url.sty) (bitset.sty (bigintcalc.sty))\n(atbegshi-ltx.sty)) (hxetex.def (stringenc.sty) (rerunfilecheck.sty\n(atveryend-ltx.sty) (uniquecounter.sty)))\n\n! LaTeX Error: Command \\Check already defined.\n               Or name \\end... illegal, see p.192 of the manual.\n\nSee the LaTeX manual or LaTeX Companion for explanation.\nType  H <return>  for immediate help.\n ...                                              \n                                                  \nl.29 \\newcommand{\\Check}{\\par\\textbf{结论与检查}\\quad}\n                                                 \nNo pages of output.\nTranscript written on 中值定理阶段模拟卷1.log.\n===============================================================================\nerror: the XeTeX engine had an unrecoverable error\ncaused by: halted on potentially-recoverable error as specified\n"}

## tool · 2026-11-12T13:14:51Z


Script completed
Wall time 0.6 seconds
Output:

{"chunk_id":"2cd32a","wall_time_seconds":0.000010958,"exit_code":0,"original_token_count":1125,"output":"% !TeX program = xelatex\n% 题源根目录：references/302模拟27md/\n% 武忠祥基础：2027模考/武忠祥/27考研基础摸底测试（高数、线代）/27考研基础摸底测试（高数、线代）数二.pdf.md\n% 武忠祥8月：2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\n% 李林：2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\n% 张宇：2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\n% 李艳芳：2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\n\\documentclass[UTF8,zihao=-4,fontset=fandol]{ctexart}\n\\usepackage[paperwidth=800bp,paperheight=600bp,left=48bp,right=48bp,top=40bp,bottom=40bp]{geometry}\n\\usepackage{amsmath,amssymb,xcolor,fancyhdr,enumitem}\n\\usepackage[hidelinks,bookmarksopen=true]{hyperref}\n\\renewcommand{\\lim}{\\operatorname*{lim}\\limits}\n\\everymath{\\displaystyle}\n\\definecolor{accent}{HTML}{175C57}\n\\setlength{\\parindent}{0pt}\n\\setlength{\\parskip}{5bp}\n\\setlength{\\headheight}{15bp}\n\\setlength{\\abovedisplayskip}{6bp}\n\\setlength{\\belowdisplayskip}{6bp}\n\\pagestyle{fancy}\\fancyhf{}\\renewcommand{\\headrulewidth}{0pt}\n\\fancyfoot[L]{\\footnotesize\\textcolor{gray}{中值定理阶段模拟卷 1 · 4:3 横屏}}\n\\fancyfoot[R]{\\footnotesize\\thepage}\n\\raggedbottom\n\\newcommand{\\Question}[4]{\\clearpage\\def\\CurrentNumber{#1}\\def\\CurrentSource{#4}\\pdfbookmark[1]{第#1题}{q#1}{\\small\\color{accent}模拟卷 1\\hfill #2 · #3 分}\\par{\\Large\\bfseries 第 #1 题}\\par\\medskip\\fontsize{14}{22}\\selectfont}\n\\newcommand{\\Solution}{\\clearpage\\fontsize{12}{18}\\selectfont{\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par{\\footnotesize\\color{gray}题源：\\CurrentSource}\\par\\smallskip}\n\\newcommand{\\Known}{\\par\\textbf{已知与目标}\\quad}\n\\newcommand{\\Method}{\\par\\textbf{方法与条件}\\quad}\n\\newcommand{\\Derive}{\\par\\textbf{推导}\\quad}\n\\newcommand{\\Check}{\\par\\textbf{结论与检查}\\quad}\n\\newcommand{\\Choices}[4]{\\begin{enumerate}[label=\\textup{(\\Alph*)},leftmargin=2em,itemsep=4bp,topsep=8bp]\\item #1\\item #2\\item #3\\item #4\\end{enumerate}}\n\\newcommand{\\blank}{\\underline{\\hspace{6em}}}\n\\begin{document}\n\\pdfbookmark[0]{模拟卷1}{cover}\n{\\small\\color{accent}工科数学分析基础 · 第三版上册}\\par\\vspace{20bp}\n{\\Huge\\bfseries 阶段模拟卷 1}\\par\\medskip\n% !TeX program = xelatex\n% 题源根目录：references/302模拟27md/\n% 武忠祥8月：2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\n% 李林：2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\n% 张宇：2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\n% 李艳芳：2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\n\\documentclass[UTF8,zihao=-4,fontset=fandol]{ctexart}\n\\usepackage[paperwidth=800bp,paperheight=600bp,left=48bp,right=48bp,top=40bp,bottom=40bp]{geometry}\n\\usepackage{amsmath,amssymb,xcolor,fancyhdr,enumitem}\n\\usepackage[hidelinks,bookmarksopen=true]{hyperref}\n\\renewcommand{\\lim}{\\operatorname*{lim}\\limits}\n\\everymath{\\displaystyle}\n\\definecolor{accent}{HTML}{175C57}\n\\setlength{\\parindent}{0pt}\\setlength{\\parskip}{5bp}\\setlength{\\headheight}{15bp}\n\\setlength{\\abovedisplayskip}{6bp}\\setlength{\\belowdisplayskip}{6bp}\n\\pagestyle{fancy}\\fancyhf{}\\renewcommand{\\headrulewidth}{0pt}\n\\fancyfoot[L]{\\footnotesize\\textcolor{gray}{中值定理阶段模拟卷 2 · 4:3 横屏}}\n\\fancyfoot[R]{\\footnotesize\\thepage}\\raggedbottom\n\\newcommand{\\Question}[4]{\\clearpage\\def\\CurrentNumber{#1}\\def\\CurrentSource{#4}\\pdfbookmark[1]{第#1题}{q#1}{\\small\\color{accent}模拟卷 2\\hfill #2 · #3 分}\\par{\\Large\\bfseries 第 #1 题}\\par\\medskip\\fontsize{14}{22}\\selectfont}\n\\newcommand{\\Solution}{\\clearpage\\fontsize{12}{18}\\selectfont{\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par{\\footnotesize\\color{gray}题源：\\CurrentSource}\\par\\smallskip}\n\\newcommand{\\Known}{\\par\\textbf{已知与目标}\\quad}\n\\newcommand{\\Method}{\\par\\textbf{方法与条件}\\quad}\n\\newcommand{\\Derive}{\\par\\textbf{推导}\\quad}\n\\newcommand{\\Check}{\\par\\textbf{结论与检查}\\quad}\n\\newcommand{\\Choices}[4]{\\begin{enumerate}[label=\\textup{(\\Alph*)},leftmargin=2em,itemsep=4bp,topsep=8bp]\\item #1\\item #2\\item #3\\item #4\\end{enumerate}}\n\\newcommand{\\blank}{\\underline{\\hspace{6em}}}\n\\begin{document}\n\\pdfbookmark[0]{模拟卷2}{cover}\n"}
{}
{"chunk_id":"cc23d6","wall_time_seconds":0.305588125,"exit_code":1,"original_token_count":685,"output":"note: using only cached resource files\nnote: Running TeX ...\nerror: 中值定理阶段模拟卷1.tex:45: Package fontspec Error: The font \"FandolFang-Regular\" cannot be found.\n\nFor immediate help type H <return>\nnote: Writing `.question-bank-work/中值定理阶段模拟卷1.log` (21.6357421875 KiB)\nerror: something bad happened inside XeTeX; its output follows:\n\n===============================================================================\n(中值定理阶段模拟卷1.tex\nLaTeX2e <2021-11-15> patch level 1\nL3 programming layer <2022-02-24> (ctexart.cls (ctexbackend.cfg) (expl3.sty\n(l3backend-xetex.def))\nDocument Class: ctexart 2021/12/12 v2.5.8 Chinese adapter for class article (CT\nEX)\n(xparse.sty) (l3keys2e.sty) (ctexhook.sty) (ctexpatch.sty) (fix-cm.sty\n(ts1enc.def)) (ctexopts.cfg) (article.cls\nDocument Class: article 2021/10/04 v1.4n Standard LaTeX document class\n(size12.clo)) (ctex-engine-xetex.def (xeCJK.sty (xtemplate.sty) (fontspec.sty\n(fontspec-xetex.sty (fontenc.sty) (fontspec.cfg))) (xeCJK.cfg))) (zhnumber.sty\n(zhnumber-utf8.cfg)) (ctex-scheme-chinese-article.def (ctex-name-utf8.cfg))\n(ctex-cs4size.clo) (ctex-fontset-fandol.def)) (ctex.cfg) (geometry.sty\n(keyval.sty) (ifvtex.sty (iftex.sty))) (amsmath.sty\nFor additional information on amsmath, use the `?' option.\n(amstext.sty (amsgen.sty)) (amsbsy.sty) (amsopn.sty)) (amssymb.sty\n(amsfonts.sty)) (xcolor.sty (color.cfg) (xetex.def)) (fancyhdr.sty)\n(enumitem.sty) (hyperref.sty (ltxcmds.sty) (pdftexcmds.sty (infwarerr.sty))\n(kvsetkeys.sty) (kvdefinekeys.sty) (pdfescape.sty) (hycolor.sty)\n(letltxmacro.sty) (auxhook.sty) (kvoptions.sty) (pd1enc.def) (intcalc.sty)\n(etexcmds.sty) (puenc.def) (url.sty) (bitset.sty (bigintcalc.sty))\n(atbegshi-ltx.sty)) (hxetex.def (stringenc.sty) (rerunfilecheck.sty\n(atveryend-ltx.sty) (uniquecounter.sty)))\nNo file 中值定理阶段模拟卷1.aux.\n*geometry* driver: auto-detecting\n*geometry* detected driver: xetex\n(nameref.sty (refcount.sty) (gettitlestring.sty))\n\nPackage hyperref Warning: Rerun to get /PageLabels entry.\n\n\n! Package fontspec Error: The font \"FandolFang-Regular\" cannot be found.\n\nFor immediate help type H <return>.\n ...                                              \n                                                  \nl.45 题目选自本地 \\texttt{references/302模拟27md}\n                                         ，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐...\nNo pages of output.\nTranscript written on 中值定理阶段模拟卷1.log.\n===============================================================================\nerror: the XeTeX engine had an unrecoverable error\ncaused by: halted on potentially-recoverable error as specified\n"}

## tool · 2026-11-12T13:17:34Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-12T13:17:42Z


Script completed
Wall time 1.3 seconds
Output:

{"chunk_id":"d50ba8","wall_time_seconds":0.007866084,"exit_code":0,"original_token_count":1345,"output":"\n======================================================================\nFAIL: test_three_complete_papers (__main__.MeanValueExamTests) (path='中值定理阶段模拟卷1.tex')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.github/scripts/test_mean_value_exams.py\", line 31, in test_three_complete_papers\n    self.assertNotRegex(line, r\"(?<=[0-9a-z)])/+(?=[0-9a-z(])\")\nAssertionError: Regex matched: '/' matches '(?<=[0-9a-z)])/+(?=[0-9a-z(])' in '题目选自本地 references/302模拟27md，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。'\n\n======================================================================\nFAIL: test_three_complete_papers (__main__.MeanValueExamTests) (path='中值定理阶段模拟卷2.tex')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.github/scripts/test_mean_value_exams.py\", line 31, in test_three_complete_papers\n    self.assertNotRegex(line, r\"(?<=[0-9a-z)])/+(?=[0-9a-z(])\")\nAssertionError: Regex matched: '/' matches '(?<=[0-9a-z)])/+(?=[0-9a-z(])' in '题目选自本地 references/302模拟27md，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。'\n\n======================================================================\nFAIL: test_three_complete_papers (__main__.MeanValueExamTests) (path='中值定理阶段模拟卷3.tex')\n----------------------------------------------------------------------\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.github/scripts/test_mean_value_exams.py\", line 31, in test_three_complete_papers\n    self.assertNotRegex(line, r\"(?<=[0-9a-z)])/+(?=[0-9a-z(])\")\nAssertionError: Regex matched: '/' matches '(?<=[0-9a-z)])/+(?=[0-9a-z(])' in '题目选自本地 references/302模拟27md，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。'\n\n----------------------------------------------------------------------\nRan 1 test in 0.001s\n\nFAILED (failures=3)\noutput/中值定理阶段模拟卷1.tex:2:% 题源根目录：references/302模拟27md/\noutput/中值定理阶段模拟卷1.tex:3:% 武忠祥基础：2027模考/武忠祥/27考研基础摸底测试（高数、线代）/27考研基础摸底测试（高数、线代）数二.pdf.md\noutput/中值定理阶段模拟卷1.tex:4:% 武忠祥8月：2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\noutput/中值定理阶段模拟卷1.tex:5:% 李林：2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\noutput/中值定理阶段模拟卷1.tex:6:% 张宇：2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\noutput/中值定理阶段模拟卷1.tex:7:% 李艳芳：2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\noutput/中值定理阶段模拟卷1.tex:45:题目选自本地 references/302模拟27md，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。\noutput/中值定理阶段模拟卷3.tex:2:% 题源根目录：references/302模拟27md/\noutput/中值定理阶段模拟卷3.tex:3:% 武忠祥基础：2027模考/武忠祥/27考研基础摸底测试（高数、线代）/27考研基础摸底测试（高数、线代）数二.pdf.md\noutput/中值定理阶段模拟卷3.tex:4:% 武忠祥8月：2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\noutput/中值定理阶段模拟卷3.tex:5:% 李林：2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\noutput/中值定理阶段模拟卷3.tex:6:% 张宇：2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\noutput/中值定理阶段模拟卷3.tex:7:% 李艳芳：2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\noutput/中值定理阶段模拟卷3.tex:41:题目选自本地 references/302模拟27md，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。\noutput/中值定理阶段模拟卷2.tex:2:% 题源根目录：references/302模拟27md/\noutput/中值定理阶段模拟卷2.tex:3:% 武忠祥8月：2027模考/武忠祥/武老师8月突击强化测试/8月强化突击测试.pdf.md\noutput/中值定理阶段模拟卷2.tex:4:% 李林：2027模考/李林《六套卷》/数学二/试卷/考研数学冲刺预测6套卷.pdf.md\noutput/中值定理阶段模拟卷2.tex:5:% 张宇：2027模考/张宇《八套卷》/张宇八套卷/数二/【紧凑】张宇八套卷-数二（已勘误）.pdf.md\noutput/中值定理阶段模拟卷2.tex:6:% 李艳芳：2027模考/李艳芳《三套卷》/数学二/【紧凑版】李艳芳三套卷做题本 .pdf.md\noutput/中值定理阶段模拟卷2.tex:40:题目选自本地 references/302模拟27md，具体作者、卷次与原题号见各题解析。改题型、增设任务或只取原题小问均逐题标注。\n"}
{"paper":1,"result":{"status":"fulfilled","value":{"chunk_id":"511a45","wall_time_seconds":1.002304666,"session_id":90772,"original_token_count":41,"output":"note: using only cached resource files\nnote: Running TeX ...\nnote: Rerunning TeX because \"中值定理阶段模拟卷1.aux\" changed ...\nnote: Running xdvipdfmx ...\n"}}}
{"paper":2,"result":{"status":"fulfilled","value":{"chunk_id":"26ef56","wall_time_seconds":1.000566084,"session_id":6263,"original_token_count":2703,"output":"Warning: truncated output (original token count: 2703)\nTotal output lines: 98\n\nnote: using only cached resource files\nnote: Running TeX ...\nwarning: 中值定理阶段模拟卷2.tex:76: \nMissing character: There is no ��� (U+2260) in font [lmroman9-regular]:mapping=tex-text;!\nwarning: could not represent character \"≠\" (0x2260) in font \"[lmroman9-regular]:mapping=tex-text;\"\nwarning:   you may need to load the `fontspec` package and use (e.g.) \\setmainfont to\nwarning:   choose a different font that covers the unrepresentable character(s)\nwarning: 中值定理阶段模拟卷2.tex:191: \nMissing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:191: Missing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:191: Missing character: There is no ��� (U+2460) in font [lmroman10-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman10-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:191: Missing character: There is no ��� (U+2460) in font [lmroman7-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman7-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:192: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:192: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:192: Missing character: There is no ��� (U+2461) in font [lmroman10-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman10-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:192: Missing character: There is no ��� (U+2461) in font [lmroman7-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman7-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:193: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:193: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:193: Missing character: There …1203 tokens truncated…ar]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:193: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:193: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:193: Missing character: There is no ��� (U+2462) in font [lmroman10-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman10-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:193: Missing character: There is no ��� (U+2462) in font [lmroman7-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman7-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:194: Missing character: There is no ��� (U+2463) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"④\" (0x2463) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:194: Missing character: There is no ��� (U+2463) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"④\" (0x2463) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:194: Missing character: There is no ��� (U+2463) in font [lmroman10-regular]:mapping=tex-text;!\nwarning: could not represent character \"④\" (0x2463) in font \"[lmroman10-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:194: Missing character: There is no ��� (U+2463) in font [lmroman7-regular]:mapping=tex-text;!\nwarning: could not represent character \"④\" (0x2463) in font \"[lmroman7-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:201: \nMissing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:203: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:205: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷2.tex:207: Missing character: There is no ��� (U+2463) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"④\" (0x2463) in font \"[lmroman12-regular]:mapping=tex-text;\"\nnote: Running xdvipdfmx ...\n"}}}
{"paper":3,"result":{"status":"fulfilled","value":{"chunk_id":"83b77f","wall_time_seconds":1.0021155,"session_id":16944,"original_token_count":2093,"output":"Warning: truncated output (original token count: 2093)\nTotal output lines: 78\n\nnote: using only cached resource files\nnote: Running TeX ...\nwarning: 中值定理阶段模拟卷3.tex:108: \nMissing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning:   you may need to load the `fontspec` package and use (e.g.) \\setmainfont to\nwarning:   choose a different font that covers the unrepresentable character(s)\nwarning: 中值定理阶段模拟卷3.tex:110: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:112: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:119: \nMissing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:119: Missing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:121: Missing character:…593 tokens truncated…:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:115: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:119: \nMissing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:119: Missing character: There is no ��� (U+2460) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:121: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:125: Missing character: There is no ��� (U+2461) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"②\" (0x2461) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:127: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:127: Missing character: There is no ��� (U+2462) in font [lmroman12-regular]:mapping=tex-text;!\nwarning: could not represent character \"③\" (0x2462) in font \"[lmroman12-regular]:mapping=tex-text;\"\nwarning: 中值定理阶段模拟卷3.tex:269: \nMissing character: There is no ��� (U+2460) in font [lmroman9-regular]:mapping=tex-text;!\nwarning: could not represent character \"①\" (0x2460) in font \"[lmroman9-regular]:mapping=tex-text;\"\nnote: Running xdvipdfmx ...\n"}}}

## tool · 2026-11-12T13:17:52Z


Script completed
Wall time 0.2 seconds
Output:

{"status":"fulfilled","value":{"chunk_id":"ec3e09","wall_time_seconds":0.000021,"exit_code":1,"original_token_count":183,"output":"warning: Tectonic unable to generate PK font \"cmr9.pfb\" (dpi 600) on-the-fly\nwarning: Could not locate a virtual/physical font for TFM \"cmr9\".\nwarning: >> This font is mapped to a physical font \"cmr9.pfb\".\nwarning: >> Please check if kpathsea library can find this font: cmr9.pfb\nnote: Writing `.question-bank-work/中值定理阶段模拟卷1.log` (21.9853515625 KiB)\nerror: something bad happened inside xdvipdfmx; its output follows:\n\n===============================================================================\n\n===============================================================================\nerror: the xdvipdfmx engine had an unrecoverable error\ncaused by: Cannot proceed without .vf or \"physical\" font for PDF output...\n"}}
{"status":"fulfilled","value":{"chunk_id":"63e96a","wall_time_seconds":0.000007791,"exit_code":1,"original_token_count":184,"output":"warning: Tectonic unable to generate PK font \"cmmi9.pfb\" (dpi 600) on-the-fly\nwarning: Could not locate a virtual/physical font for TFM \"cmmi9\".\nnote: Writing `.question-bank-work/中值定理阶段模拟卷2.log` (23.8681640625 KiB)\nwarning: >> This font is mapped to a physical font \"cmmi9.pfb\".\nwarning: >> Please check if kpathsea library can find this font: cmmi9.pfb\nerror: something bad happened inside xdvipdfmx; its output follows:\n\n===============================================================================\n\n===============================================================================\nerror: the xdvipdfmx engine had an unrecoverable error\ncaused by: Cannot proceed without .vf or \"physical\" font for PDF output...\n"}}
{"status":"fulfilled","value":{"chunk_id":"6e9f66","wall_time_seconds":0.00000825,"exit_code":1,"original_token_count":184,"output":"warning: Tectonic unable to generate PK font \"cmmi9.pfb\" (dpi 600) on-the-fly\nwarning: Could not locate a virtual/physical font for TFM \"cmmi9\".\nwarning: >> This font is mapped to a physical font \"cmmi9.pfb\".\nwarning: >> Please check if kpathsea library can find this font: cmmi9.pfb\nnote: Writing `.question-bank-work/中值定理阶段模拟卷3.log` (23.4228515625 KiB)\nerror: something bad happened inside xdvipdfmx; its output follows:\n\n===============================================================================\n\n===============================================================================\nerror: the xdvipdfmx engine had an unrecoverable error\ncaused by: Cannot proceed without .vf or \"physical\" font for PDF output...\n"}}
{"chunk_id":"fe8f30","wall_time_seconds":0.000009791,"exit_code":0,"original_token_count":1321,"output":"\\Question{8}{填空}{5}{武忠祥8月强化突击测试，第 1 题；原题}\n设函数 $f(x)$ 连续，给出四个条件：\n\\[\n\\begin{aligned}\n&\\text{① }\\lim_{x\\to0}\\frac{|f(x)|-f(0)}x\\text{ 存在；}\\qquad\n\\text{② }\\lim_{x\\to0}\\frac{f(x)-|f(0)|}x\\text{ 存在；}\\\\[6bp]\n&\\text{③ }\\lim_{x\\to0}\\frac{|f(x)|}x\\text{ 存在；}\\qquad\n\\text{④ }\\lim_{x\\to0}\\frac{|f(x)|-|f(0)|}x\\text{ 存在。}\n\\end{aligned}\n\\]\n这里“存在”均指有限极限存在。其中能推出“$f$ 在 $0$ 处可导”的条件个数是\\blank。\n\\Solution\n\\Known 分别判断四个条件，每次只使用其中一个，以及共同的连续条件。\n\\Method 先记录一个事实：若 $\\lim_{x\\to0}\\frac{|f(x)|}x=L$ 为有限数，则右侧比值非负、左侧非正，故 $L=0$。于是 $\\left|\\frac{f(x)}x\\right|\\to0$，且连续性给出 $f(0)=0$，从而 $f'(0)=0$。\n\\Derive ① 有限极限要求 $|f(0)|-f(0)=0$，所以 $f(0)\\ge0$。若 $f(0)>0$，连续性保证附近 $f(x)>0$，条件中的差商就是导数差商；若 $f(0)=0$，使用上述事实。\n\n② 有限极限要求 $f(0)=|f(0)|$，于是分子正是 $f(x)-f(0)$，直接得到导数存在。\n\n③ 正好满足上述事实，故 $f'(0)=0$。\n\n④ 若 $f(0)>0$，附近 $|f(x)|=f(x)$；若 $f(0)<0$，附近 $|f(x)|=-f(x)$。两种情况都把给定差商变成导数差商或其相反数。若 $f(0)=0$，再使用上述事实。\n\\Check 填 $\\boxed{4}$。关键是双侧极限；只给单侧极限时，“非负、非正迫使极限为零”的论证不能直接使用。\n\n\\Question{9}{解答}{15}{李林六套卷数二，第六套第 17 题；原题，分值重设}\n\n\\Question{4}{单项选择}{5}{张宇八套卷数二，卷八第 1 题；原题}\n设 $f(x)$ 在 $(-1,1)$ 内有定义，且在 $0$ 处连续。考察以下结论：\n\n① 若 $\\lim_{x\\to0}\\frac{f(x)}{\\sqrt[3]x}=0$，则 $f$ 在 $0$ 处可导。\n\n② 若 $\\lim_{x\\to0}\\frac{f(x)}{x^2}=0$，则 $f$ 在 $0$ 处可导。\n\n③ 若 $f$ 在 $0$ 处可导，则 $\\lim_{x\\to0}\\frac{f(x)}{\\sqrt[3]x}=0$。\n\n所有正确结论的序号为（\\quad）。\n\\Choices{①}{②}{②③}{①②}\n\\Solution\n\\Known 三个命题都涉及导数与小量的关系，需要分别验证，不能擅自添加 $f(0)=0$。\n\\Method 正确命题用导数定义证明；错误命题用满足前提但不满足结论的函数，即反例，进行排除。\n\\Derive ① 取 $f(x)=|x|^{\\frac23}$。有 $\\frac{f(x)}{\\sqrt[3]x}\\to0$，但 $\\frac{f(x)-f(0)}x$ 的右侧趋于 $+\\infty$、左侧趋于 $-\\infty$，故不可导。① 错误。\n\n② 给定条件推出 $f(x)\\to0$，连续性给出 $f(0)=0$。于是\n\\[\n\\frac{f(x)-f(0)}x=x\\frac{f(x)}{x^2}\\to0,\n\\]\n故 $f'(0)=0$。② 正确。\n\n③ 取 $f(x)\\equiv1$，函数处处可导，但 $\\frac1{\\sqrt[3]x}$ 不趋于 $0$。③ 错误。\n\\Check 选 \\textbf{B}。两个反例在整个 $(-1,1)$ 内都有定义且在 $0$ 连续；原题确实没有给出 $f(0)=0$，这一条件不能自行补入。\n\n\\Question{5}{填空}{5}{张宇八套卷数二，卷六第 11 题；原题}\n\\[\n设 $f$ 在 $[0,1]$ 上三阶可导，$f(0)=f(1)$，并在 $x=c$（$0<c<1$）处取得极值。已知对任意 $x\\in(0,1)$，\n\\[\n1\\le|f''(x)|\\le4.\n\\]\n证明：$\\frac13\\le c\\le\\frac23$。\n\\Solution\n\\Known 极值点在内部，故 Fermat 定理给出 $f'(c)=0$；两个端点函数值相同。\n\\Method 用 Rolle 定理把端点到极值点的函数增量写成二阶导数乘距离平方，再比较两侧距离。三阶可导保证 $f''$ 在内部连续；它不能在不经过零的情况下改变符号。\n\\Derive 因 $|f''|\\ge1$，所以 $f''$ 符号固定。必要时把 $f$ 换成 $-f$，可设 $1\\le f''\\le4$。\nfrom pathlib import Path\nimport re\nimport unittest\n\n\nROOT = Path(__file__).resolve().parents[2]\nFILES = [ROOT / f\"output/中值定理阶段模拟卷{number}.tex\" for number in (1, 2, 3)]\n\n\nclass MeanValueExamTests(unittest.TestCase):\n    def test_three_complete_papers(self):\n        for path in FILES:\n            with self.subTest(path=path.name):\n                source = path.read_text()\n                questions = re.findall(r\"^\\\\Question\\{(\\d+)\\}\\{([^}]+)\\}\\{(\\d+)\\}\\{([^}]+)\\}\", source, re.M)\n                self.assertEqual([int(q[0]) for q in questions], list(range(1, 13)))\n                self.assertEqual([q[1] for q in questions], [\"单项选择\"] * 4 + [\"填空\"] * 4 + [\"解答\"] * 4)\n                self.assertEqual(sum(int(q[2]) for q in questions), 100)\n                blocks = re.split(r\"^\\\\Question\\{\", source, flags=re.M)[1:]\n                for block in blocks:\n                    self.assertEqual(block.count(r\"\\Solution\"), 1)\n                    for label in (r\"\\Known\", r\"\\Method\", r\"\\Derive\", r\"\\Check\"):\n                        self.assertEqual(block.count(label), 1)\n                self.assertEqual(source.count(r\"\\Choices{\"), 4)\n                self.assertIn(\"paperwidth=800bp,paperheight=600bp\", source)\n                self.assertIn(r\"\\operatorname*{lim}\\limits\", source)\n                self.assertNotIn(r\"\\tfrac\", source)\n                self.assertNotIn(r\"\\int\", source)\n                for line in source.splitlines():\n                    if not line.startswith(\"%\"):\n                        self.assertNotRegex(line, r\"(?<=[0-9a-z)])/+(?=[0-9a-z(])\")\n\n\nif __name__ == \"__main__\":\n    unittest.main()\n"}

## tool · 2026-11-12T13:18:41Z


Script completed
Wall time 1.3 seconds
Output:

{}
{"chunk_id":"c9d79e","wall_time_seconds":1.001988583,"session_id":88521,"original_token_count":38,"output":"note: Running TeX ...\nnote: Rerunning TeX because \"中值定理阶段模拟卷1.aux\" changed ...\nnote: Running xdvipdfmx ...\nnote: downloading cmr9.pfb\n"}

## tool · 2026-11-12T13:19:27Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"3e0b5e","wall_time_seconds":0.000015875,"exit_code":0,"original_token_count":80,"output":"note: downloading cmsy9.pfb\nnote: downloading cmmi9.pfb\nnote: Writing `.question-bank-work/中值定理阶段模拟卷1.pdf` (200.142578125 KiB)\nnote: Writing `.question-bank-work/中值定理阶段模拟卷1.log` (21.9853515625 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}
{"chunk_id":"272b2e","wall_time_seconds":0.189860833,"exit_code":0,"original_token_count":190,"output":".\n----------------------------------------------------------------------\nRan 1 test in 0.002s\n\nOK\n中值定理阶段模拟卷1.pdf 25 [(1, ['工科数学分析基础·第三版上册']), (2, ['模拟卷1']), (3, ['第1 题解析']), (4, ['模拟卷1']), (5, ['第2 题解析']), (6, ['模拟卷1']), (7, ['第3 题解析']), (8, ['模拟卷1']), (9, ['第4 题解析']), (10, ['模拟卷1']), (11, ['第5 题解析']), (12, ['模拟卷1']), (13, ['第6 题解析']), (14, ['模拟卷1']), (15, ['第7 题解析']), (16, ['模拟卷1']), (17, ['第8 题解析']), (18, ['模拟卷1']), (19, ['第9 题解析']), (20, ['模拟卷1']), (21, ['第10 题解析']), (22, ['模拟卷1']), (23, ['第11 题解析']), (24, ['模拟卷1']), (25, ['第12 题解析'])]\n"}

## assistant · 2026-11-12T13:19:33Z

三卷内容已完成。第一卷已成功编译为 25 页，文字检查确认了 12 组“题页—解析页”，没有多出的续页。接下来会编译其余两卷，复核关键极限与证明，并检查手写留白、分式和极限下标的位置。


## tool · 2026-11-12T13:19:36Z


Script completed
Wall time 1.3 seconds
Output:

{"paper":2,"result":{"status":"fulfilled","value":{"chunk_id":"3dd440","wall_time_seconds":0.973685875,"exit_code":0,"original_token_count":96,"output":"note: Running TeX ...\nnote: Rerunning TeX because \"中值定理阶段模拟卷2.out\" changed ...\nnote: Running xdvipdfmx ...\nnote: Writing `.question-bank-work/中值定理阶段模拟卷2.pdf` (211.2734375 KiB)\nnote: Writing `.question-bank-work/中值定理阶段模拟卷2.log` (21.986328125 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}}}
{"paper":3,"result":{"status":"fulfilled","value":{"chunk_id":"4b2d0c","wall_time_seconds":0.973285917,"exit_code":0,"original_token_count":97,"output":"note: Running TeX ...\nnote: Rerunning TeX because \"中值定理阶段模拟卷3.out\" changed ...\nnote: Running xdvipdfmx ...\nnote: Writing `.question-bank-work/中值定理阶段模拟卷3.pdf` (207.173828125 KiB)\nnote: Writing `.question-bank-work/中值定理阶段模拟卷3.log` (21.986328125 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}}}
{"chunk_id":"dd3f45","wall_time_seconds":0.000010375,"exit_code":0,"original_token_count":1283,"output":"from pathlib import Path\nimport re\nimport unittest\n\n\nROOT = Path(__file__).resolve().parents[2]\nFILES = [ROOT / f\"output/中值定理阶段模拟卷{number}.tex\" for number in (1, 2, 3)]\n\n\nclass MeanValueExamTests(unittest.TestCase):\n    def test_three_complete_papers(self):\n        for path in FILES:\n            with self.subTest(path=path.name):\n                source = path.read_text()\n                questions = re.findall(r\"^\\\\Question\\{(\\d+)\\}\\{([^}]+)\\}\\{(\\d+)\\}\\{([^}]+)\\}\", source, re.M)\n                self.assertEqual([int(q[0]) for q in questions], list(range(1, 13)))\n                self.assertEqual([q[1] for q in questions], [\"单项选择\"] * 4 + [\"填空\"] * 4 + [\"解答\"] * 4)\n                self.assertEqual(sum(int(q[2]) for q in questions), 100)\n                blocks = re.split(r\"^\\\\Question\\{\", source, flags=re.M)[1:]\n                for block in blocks:\n                    self.assertEqual(block.count(r\"\\Solution\"), 1)\n                    for label in (r\"\\Known\", r\"\\Method\", r\"\\Derive\", r\"\\Check\"):\n                        self.assertEqual(block.count(label), 1)\n                self.assertEqual(source.count(r\"\\Choices{\"), 4)\n                self.assertIn(\"paperwidth=800bp,paperheight=600bp\", source)\n                self.assertIn(r\"\\operatorname*{lim}\\limits\", source)\n                self.assertNotIn(r\"\\tfrac\", source)\n                self.assertNotIn(r\"\\int\", source)\n                for line in source.splitlines():\n                    if not line.startswith(\"%\") and \"references/\" not in line:\n                        self.assertNotRegex(line, r\"(?<=[0-9a-z)])/+(?=[0-9a-z(])\")\n\n\nif __name__ == \"__main__\":\n    unittest.main()\n# 完成标准\n\n## 当前任务：中值定理阶段三套模拟卷\n\n每卷 12 题：选择 4×5 分、填空 4×5 分、解答 4×15 分，总分 100；共 36 题且无跨卷原题重复。逐题注明 `302模拟27md` 中的作者、卷次、题号和改动；解法只用第一章至 2.4.2。三份 PDF 各 25 页（封面 1 页、12 对题解页），全部 800×600 bp；每题下方至少 200 bp 空白，解析只出现在紧邻下一页，所有正文在边界内。公式统一上下分式、lim 下置条件。逐题复算并用数值和反例补验关键极限及命题，编译日志无缺字和溢出。不进行未授权截图或图像检查；不宣称实机验证。\n\n## 当前任务：分节真题难度与详细解析\n\n- 234 个原卷年份与题号组合保持一致，各题保留原小节、题干、选项、图形和全部小问；234 份解析与题目一一对应。\n- 题头均有 1–5 个文字 `*`，各节难度非递减；同难度保留原顺序；显示题序连续。\n- 每份解析包含条件与目标、方法依据、必要中间计算、明确结论和针对性检查；逐题校订，客观结构检查不能替代数学正确性检查。\n- 数学算式不使用斜杠分数、Unicode 分数字符或紧缩的 `\\tfrac`；分子分母及指数分组正确。\n- 横屏和 A4 实际编译成功，无缺字或内容溢出；检查 PDF 234 个题头、解析对应与难度顺序、书签和文字边界。未授权视觉检查，不截图。\n- 保留用户已有的裁片 PDF 删除及 iPad 目录其他内容，只提交任务相关文件。\n\n2026-11-12 验证结果：五项源稿回归检查通过，234 份题面与任务开始前 HEAD 完全一致，题号集合、小节题量及解析对应正确。星级 1–5 分别为 6、110、88、29、1 题，各节稳定升序。234 份解析均含已知与目标、方法与条件、推导、结论与检查；算式没有斜杠分数、Unicode 分数或紧缩分式。\n\nTectonic 0.17.0 使用既有缓存编译：横屏 488 页、A4 471 页，日志无缺字、警告或溢出。两份 PDF 均核对 234 个题头、234 个解析入口及 23 个书签；星级与源稿逐题一致，解析从题目下一页开始，文字均在页面内。用 2017 年第 10 题解析的字形坐标和分数线确认分子在上、分母在下。现有横屏及 iPad PDF 均由本次横屏编译结果覆盖。第四章 33 题经独立代理复核，选定方程、初值及面积、体积、弧长、冷却时间通过 48 项数值检查。未做截图或 iPad 实机检查。\n\n本次张宇八套：两科各八卷、每卷 16 题及 40 个选项；对照源 PDF 逐题核对，不以候选文件存在或公式渲染成功代替原页校对。四份交付文件只更新张宇八套分组。\n\n memory/agents.md                                   |   2 +\n memory/plan.md                                     |   6 +\n memory/progress.md                                 |   8 +\n memory/verify.md                                   |   4 +\n ...56\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\" | Bin 106056 -> 0 bytes\n ...56\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\" | 205 ------\n ...05\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\" | Bin 204784 -> 0 bytes\n ...05\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\" | 736 ---------------------\n output/302-question-facsimiles.pdf                 | Bin 23932688 -> 0 bytes\n 9 files changed, 20 insertions(+), 941 deletions(-)\n2026-11-12 21:19 CST\n"}

## tool · 2026-11-12T13:20:29Z


Script completed
Wall time 0.5 seconds
Output:

{}
{"chunk_id":"fb0a57","wall_time_seconds":0.301091542,"exit_code":1,"original_token_count":108,"output":"....\n----------------------------------------------------------------------\nRan 4 tests in 0.008s\n\nOK\nTraceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/verify-mean-value.py\", line 31, in <module>\n    assert bottom <= 360, (number, question, \"作答区不足200bp\", bottom)\n           ^^^^^^^^^^^^^\nAssertionError: (1, 4, '作答区不足200bp', 360.64410400390625)\n"}

## tool · 2026-11-12T13:20:40Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"b4bc1e","wall_time_seconds":0.074046167,"exit_code":0,"original_token_count":907,"output":"[(1, 25, [(1, 275.3), (2, 280.5), (3, 280.3), (4, 199.4), (5, 370.7), (6, 393.7), (7, 355.6), (8, 396.1), (9, 395.2), (10, 276.0), (11, 384.2), (12, 384.2)]), (2, 25, [(1, 158.2), (2, 216.8), (3, 280.3), (4, 207.2), (5, 396.1), (6, 396.1), (7, 353.3), (8, 324.0), (9, 370.7), (10, 353.3), (11, 277.3), (12, 384.2)]), (3, 25, [(1, 240.4), (2, 280.3), (3, 280.3), (4, 138.8), (5, 396.1), (6, 393.7), (7, 380.8), (8, 396.1), (9, 370.7), (10, 353.3), (11, 343.7), (12, 371.0)])]\n\\pagestyle{fancy}\\fancyhf{}\\renewcommand{\\headrulewidth}{0pt}\n\\fancyfoot[L]{\\footnotesize\\textcolor{gray}{中值定理阶段模拟卷 1 · 4:3 横屏}}\n\\fancyfoot[R]{\\footnotesize\\thepage}\n\\raggedbottom\n\\newcommand{\\Question}[4]{\\clearpage\\def\\CurrentNumber{#1}\\def\\CurrentSource{#4}\\pdfbookmark[1]{第#1题}{q#1}{\\small\\color{accent}模拟卷 1\\hfill #2 · #3 分}\\par{\\Large\\bfseries 第 #1 题}\\par\\medskip\\fontsize{14}{22}\\selectfont}\n\\newcommand{\\Solution}{\\clearpage\\fontsize{12}{18}\\selectfont{\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par{\\footnotesize\\color{gray}题源：\\CurrentSource}\\par\\smallskip}\n\\newcommand{\\Known}{\\par\\textbf{已知与目标}\\quad}\n\\newcommand{\\Method}{\\par\\textbf{方法与条件}\\quad}\n\\newcommand{\\Derive}{\\par\\textbf{推导}\\quad}\n\\renewcommand{\\Check}{\\par\\textbf{结论与检查}\\quad}\n\\newcommand{\\Choices}[4]{\\begin{enumerate}[label=\\textup{(\\Alph*)},leftmargin=2em,itemsep=4bp,topsep=8bp]\\item #1\\item #2\\item #3\\item #4\\end{enumerate}}\n\\newcommand{\\blank}{\\underline{\\hspace{6em}}}\n\\begin{document}\n\\pdfbookmark[0]{模拟卷1}{cover}\n\\fancyfoot[L]{\\footnotesize\\textcolor{gray}{中值定理阶段模拟卷 2 · 4:3 横屏}}\n\\fancyfoot[R]{\\footnotesize\\thepage}\\raggedbottom\n\\newcommand{\\Question}[4]{\\clearpage\\def\\CurrentNumber{#1}\\def\\CurrentSource{#4}\\pdfbookmark[1]{第#1题}{q#1}{\\small\\color{accent}模拟卷 2\\hfill #2 · #3 分}\\par{\\Large\\bfseries 第 #1 题}\\par\\medskip\\fontsize{14}{22}\\selectfont}\n\\newcommand{\\Solution}{\\clearpage\\fontsize{12}{18}\\selectfont{\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par{\\footnotesize\\color{gray}题源：\\CurrentSource}\\par\\smallskip}\n\\newcommand{\\Known}{\\par\\textbf{已知与目标}\\quad}\n\\newcommand{\\Method}{\\par\\textbf{方法与条件}\\quad}\n\\newcommand{\\Derive}{\\par\\textbf{推导}\\quad}\n\\renewcommand{\\Check}{\\par\\textbf{结论与检查}\\quad}\n\\newcommand{\\Choices}[4]{\\begin{enumerate}[label=\\textup{(\\Alph*)},leftmargin=2em,itemsep=4bp,topsep=8bp]\\item #1\\item #2\\item #3\\item #4\\end{enumerate}}\n\\newcommand{\\blank}{\\underline{\\hspace{6em}}}\n\\begin{document}\n\\pdfbookmark[0]{模拟卷2}{cover}\n\\pagestyle{fancy}\\fancyhf{}\\renewcommand{\\headrulewidth}{0pt}\n\\fancyfoot[L]{\\footnotesize\\textcolor{gray}{中值定理阶段模拟卷 3 · 4:3 横屏}}\n\\fancyfoot[R]{\\footnotesize\\thepage}\\raggedbottom\n\\newcommand{\\Question}[4]{\\clearpage\\def\\CurrentNumber{#1}\\def\\CurrentSource{#4}\\pdfbookmark[1]{第#1题}{q#1}{\\small\\color{accent}模拟卷 3\\hfill #2 · #3 分}\\par{\\Large\\bfseries 第 #1 题}\\par\\medskip\\fontsize{14}{22}\\selectfont}\n\\newcommand{\\Solution}{\\clearpage\\fontsize{12}{18}\\selectfont{\\large\\bfseries 第 \\CurrentNumber\\ 题解析}\\par{\\footnotesize\\color{gray}题源：\\CurrentSource}\\par\\smallskip}\n\\newcommand{\\Known}{\\par\\textbf{已知与目标}\\quad}\n\\newcommand{\\Method}{\\par\\textbf{方法与条件}\\quad}\n\\newcommand{\\Derive}{\\par\\textbf{推导}\\quad}\n\\renewcommand{\\Check}{\\par\\textbf{结论与检查}\\quad}\n\\newcommand{\\Choices}[4]{\\begin{enumerate}[label=\\textup{(\\Alph*)},leftmargin=2em,itemsep=4bp,topsep=8bp]\\item #1\\item #2\\item #3\\item #4\\end{enumerate}}\n\\newcommand{\\blank}{\\underline{\\hspace{6em}}}\n\\begin{document}\n"}

## tool · 2026-11-12T13:21:26Z


Script completed
Wall time 1.3 seconds
Output:

{}
{"paper":1,"result":{"status":"fulfilled","value":{"chunk_id":"4642be","wall_time_seconds":1.001770708,"session_id":44980,"original_token_count":41,"output":"note: using only cached resource files\nnote: Running TeX ...\nnote: Rerunning TeX because \"中值定理阶段模拟卷1.out\" changed ...\nnote: Running xdvipdfmx ...\n"}}}
{"paper":2,"result":{"status":"fulfilled","value":{"chunk_id":"c4d3cb","wall_time_seconds":1.001822667,"session_id":80936,"original_token_count":41,"output":"note: using only cached resource files\nnote: Running TeX ...\nnote: Rerunning TeX because \"中值定理阶段模拟卷2.aux\" changed ...\nnote: Running xdvipdfmx ...\n"}}}
{"paper":3,"result":{"status":"fulfilled","value":{"chunk_id":"622572","wall_time_seconds":1.002197125,"session_id":46483,"original_token_count":41,"output":"note: using only cached resource files\nnote: Running TeX ...\nnote: Rerunning TeX because \"中值定理阶段模拟卷3.out\" changed ...\nnote: Running xdvipdfmx ...\n"}}}

## tool · 2026-11-12T13:21:47Z


Script completed
Wall time 0.3 seconds
Output:

{"status":"fulfilled","value":{"chunk_id":"3cf102","wall_time_seconds":0.000026916,"exit_code":0,"original_token_count":66,"output":"note: Writing `.question-bank-work/中值定理阶段模拟卷1.pdf` (199.8173828125 KiB)\nnote: Writing `.question-bank-work/中值定理阶段模拟卷1.log` (21.9853515625 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}}
{"status":"fulfilled","value":{"chunk_id":"f24490","wall_time_seconds":0.0000055,"exit_code":0,"original_token_count":66,"output":"note: Writing `.question-bank-work/中值定理阶段模拟卷2.pdf` (210.7470703125 KiB)\nnote: Writing `.question-bank-work/中值定理阶段模拟卷2.log` (21.986328125 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}}
{"status":"fulfilled","value":{"chunk_id":"ae2354","wall_time_seconds":0.000006167,"exit_code":0,"original_token_count":66,"output":"note: Writing `.question-bank-work/中值定理阶段模拟卷3.log` (21.9853515625 KiB)\nnote: Writing `.question-bank-work/中值定理阶段模拟卷3.pdf` (206.0068359375 KiB)\nnote: Skipped writing 2 intermediate files (use --keep-intermediates to keep them)\n"}}
{"chunk_id":"7b632e","wall_time_seconds":0.120061209,"exit_code":0,"original_token_count":764,"output":"Traceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/verify-mean-value.py\", line 20, in <module>\n    assert all(span[\"bbox\"][0] >= 45 and span[\"bbox\"][2] <= 755\n           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^\nAssertionError: (1, 20)\n[(48.0, 46.53700637817383, 88.24647521972656, 57.099998474121094, '模拟卷1', 0, 0, 0), (701.2535400390625, 46.53700637817383, 738.0035400390625, 57.099998474121094, '填空·5', 0, 1, 0), (741.5000610351562, 46.600006103515625, 752.0000610351562, 57.099998474121094, '分', 0, 1, 1), (48.0, 67.4726333618164, 82.88398742675781, 86.80461883544922, '第8', 1, 0, 0), (89.63398742675781, 67.4726333618164, 107.63397979736328, 85.47261810302734, '题', 1, 0, 1), (48.0, 111.62525177001953, 73.2174301147461, 125.8305435180664, '设f', 2, 0, 0), (74.71548461914062, 109.2138442993164, 95.72098541259766, 125.8305435180664, '′(a)', 2, 0, 1), (99.5844955444336, 111.88284301757812, 110.19869232177734, 125.8305435180664, '=', 2, 0, 2), (114.07615661621094, 111.62525177001953, 174.4902801513672, 125.8305435180664, '1，其中a', 2, 0, 3), (178.35379028320312, 111.88284301757812, 188.96798706054688, 125.8305435180664, '>', 2, 0, 4), (192.86102294921875, 111.62525177001953, 227.58489990234375, 125.8305435180664, '0，则', 2, 0, 5), (292.7270812988281, 140.0347900390625, 311.6959533691406, 153.98248291015625, 'lim', 3, 0, 0), (291.69244384765625, 151.83456420898438, 312.7259216308594, 161.77821350097656, 'x→a', 3, 1, 0), (316.25067138671875, 130.9403533935547, 354.3977966308594, 144.88804626464844, 'x[f(x)', 4, 0, 0), (357.5082092285156, 130.68275451660156, 401.23681640625, 144.88804626464844, '−f(a)]', 4, 0, 1), (329.06170654296875, 149.6022186279297, 340.4430236816406, 163.54991149902344, 'ln', 5, 0, 0), (342.7676086425781, 149.94349670410156, 350.52252197265625, 163.8911895751953, 'x', 5, 0, 1), (353.6278381347656, 149.6022186279297, 378.9568786621094, 163.6335906982422, '−ln', 5, 0, 2), (381.2814636230469, 149.94349670410156, 388.4505920410156, 163.8911895751953, 'a', 5, 0, 3), (406.3313903808594, 140.37606811523438, 416.9455871582031, 154.32376098632812, '=', 5, 1, 0), (504.51397705078125, 140.37606811523438, 508.2937927246094, 154.32376098632812, '.', 5, 2, 0), (48.0, 585.6787719726562, 136.71287536621094, 594.7327270507812, '中值定理阶段模拟卷1', 6, 0, 0), (139.79986572265625, 585.6787719726562, 160.62583923339844, 594.7327270507812, '·4:3', 6, 0, 1), (163.7128448486328, 585.7327270507812, 181.7128143310547, 594.7327270507812, '横屏', 6, 0, 2), (742.748046875, 585.6787719726562, 752.0, 594.6787109375, '16', 6, 1, 0)]\n[(Rect(316.25067138671875, 147.78970336914062, 401.26153564453125, 147.78970336914062), [('l', Point(316.25067138671875, 147.78970336914062), Point(401.26153564453125, 147.78970336914062))]), (Rect(420.82781982421875, 153.229248046875, 504.51397705078125, 153.229248046875), [('l', Point(420.82781982421875, 153.229248046875), Point(504.51397705078125, 153.229248046875))])]\n"}

## tool · 2026-11-12T13:21:57Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"d54b7e","wall_time_seconds":0.015595625,"exit_code":0,"original_token_count":492,"output":"[(1, 20, '（', (39.15721130371094, 236.30841064453125, 53.10490798950195, 250.256103515625)), (1, 20, '（', (39.1572265625, 269.8016357421875, 53.104923248291016, 283.74932861328125)), (1, 21, '（', (40.42042541503906, 275.28656005859375, 52.37559509277344, 287.2417297363281)), (2, 17, '（', (40.42047882080078, 236.61302185058594, 52.375648498535156, 248.5681915283203)), (2, 17, '（', (40.420501708984375, 264.9256286621094, 52.37567138671875, 276.88079833984375)), (2, 17, '（', (40.420501708984375, 293.2382507324219, 52.37567138671875, 305.19342041015625)), (2, 17, '，', (748.3179931640625, 293.2382507324219, 760.2731323242188, 305.19342041015625)), (2, 22, '（', (39.15718078613281, 234.9554901123047, 53.10487747192383, 248.90318298339844)), (2, 22, '（', (39.15716552734375, 268.4486999511719, 53.104862213134766, 282.3963928222656)), (2, 23, '（', (40.42041015625, 305.6847839355469, 52.375579833984375, 317.63995361328125)), (2, 23, '。', (747.744140625, 305.68475341796875, 759.6992797851562, 317.6399230957031)), (3, 8, '（', (39.15715026855469, 145.1184539794922, 53.1048469543457, 159.06614685058594)), (3, 8, '（', (39.15715026855469, 183.9824676513672, 53.1048469543457, 197.93016052246094)), (3, 8, '（', (39.15715026855469, 219.8865203857422, 53.1048469543457, 233.83421325683594)), (3, 9, '（', (40.42041015625, 189.98776245117188, 52.375579833984375, 201.94293212890625)), (3, 9, '（', (40.42045593261719, 288.8359680175781, 52.37562561035156, 300.7911376953125))]\n[(1, [(1, 350.3), (2, 355.2), (3, 355.2), (4, 274.3), (5, 370.7), (6, 393.7), (7, 355.6), (8, 396.1), (9, 395.2), (10, 276.0), (11, 384.2), (12, 384.2)]), (2, [(1, 233.2), (2, 291.8), (3, 355.2), (4, 282.2), (5, 396.1), (6, 396.1), (7, 353.3), (8, 324.0), (9, 370.7), (10, 353.3), (11, 277.3), (12, 384.2)]), (3, [(1, 303.4), (2, 355.2), (3, 355.2), (4, 213.7), (5, 396.1), (6, 393.7), (7, 380.8), (8, 396.1), (9, 370.7), (10, 353.3), (11, 343.7), (12, 371.0)])]\n"}

## assistant · 2026-11-12T13:22:28Z

三卷均已编译为 25 页，关键极限、参数求导、函数关系和数列递推的数值检查已通过。页面坐标检查发现少数选择题留白较少，现已将选项改为两列；36 个题页的下方均保留了至少约 214 点的手写空间。


## tool · 2026-11-12T13:22:38Z


Script completed
Wall time 1.5 seconds
Output:

{"chunk_id":"5c8894","wall_time_seconds":0.000011458,"exit_code":0,"original_token_count":1374,"output":"from pathlib import Path\nimport json\nimport re\nimport pymupdf\n\n\nroot = Path(__file__).resolve().parents[1]\nreports = []\nfor number in (1, 2, 3):\n    path = root / f\".question-bank-work/中值定理阶段模拟卷{number}.pdf\"\n    document = pymupdf.open(path)\n    assert len(document) == 25, (number, len(document))\n    assert len(document.get_toc()) == 13\n    blanks = []\n    for index, page in enumerate(document):\n        assert abs(page.rect.width-800) < 0.01 and abs(page.rect.height-600) < 0.01\n        content = re.sub(r\"\\s+\", \"\", page.get_text())\n        spans = [span for block in page.get_text(\"dict\")[\"blocks\"] if \"lines\" in block\n                 for line in block[\"lines\"] for span in line[\"spans\"]]\n        assert all(span[\"bbox\"][0] >= 45 and span[\"bbox\"][2] <= 755\n                   and span[\"bbox\"][1] >= 30 and span[\"bbox\"][3] < 595 for span in spans), (number, index+1)\n        assert \"\\ufffd\" not in content\n        if index == 0:\n            continue\n        question = (index+1)//2\n        if index % 2:\n            assert f\"第{question}题\" in content and \"解析\" not in content\n            body = [span for span in spans if span[\"bbox\"][1] < 560]\n            bottom = max(span[\"bbox\"][3] for span in body)\n            blanks.append(round(560-bottom, 1))\n            assert bottom <= 360, (number, question, \"作答区不足200bp\", bottom)\n        else:\n            assert f\"第{question}题解析\" in content\n            for label in (\"已知与目标\", \"方法与条件\", \"推导\", \"结论与检查\"):\n                assert label in content, (number, question, label)\n    log = path.with_suffix(\".log\").read_text()\n    assert not re.search(r\"Overfull|Underfull|Missing character|Warning\", log), number\n    reports.append({\"paper\": number, \"pages\": len(document), \"size\": [800, 600],\n                    \"minimum_writing_space_bp\": min(blanks), \"bookmarks\": len(document.get_toc())})\nprint(json.dumps({\"status\": \"passed\", \"papers\": reports}, ensure_ascii=False, indent=2))\n# 进度\n\n## 当前任务：中值定理阶段三套模拟卷\n\n- [x] 核对教材目录和第 147–153 页中值定理正文；明确截止 4.2，筛选本地题源。\n- [x] 确认现有 Git 删除及未跟踪 iPad 模拟卷，保留用户当前状态。\n- [ ] 完成三卷共 36 题及逐题解析、原题定位和范围检查。\n- [ ] 编译三份 PDF，检查题解交替、页面比例、留白、文字边界、数学结果。\n- [ ] 更新开发记录与资料入口，提交并普通推送。\n\n## 当前任务：分节真题难度与详细解析\n\n- [x] 核实共用源稿有 234 题、19 节，两种版式共用题库；Git 初始存在裁片 PDF 删除及未跟踪 iPad 目录。\n- [x] 234 题逐题补充四部分解析、难度与上下分式；中断时未完成移动的 2023 年第 5 题、2019 年第 13 题已按原题恢复并扩写。\n- [x] 完成全部节内稳定排序，同星保留原序，题头用计数器连续编号。星级 1–5 依次为 6、110、88、29、1 题。\n- [x] 与任务开始前 HEAD 对照 234 份题面，题干、选项、图形内容均保持原文；第四章独立复核完成，48 项计算检查通过。\n- [x] 五项回归检查通过；横屏 488 页、A4 471 页编译成功，日志无缺字、警告或溢出。逐题检查题头、解析、星级、下一页开始、23 个书签及页面边界，并用字形和分数线坐标检查上下分式。已覆盖现有横屏及 iPad PDF，未做截图或实机验证。\n- [x] 题集及验证记录已提交为 `a8e4665` 并普通推送至 `origin/main`。任务开始前的裁片 PDF 删除及另一份未跟踪 iPad 模拟卷均保持原状态；提交哈希补记另作后续文档提交。\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.tex`\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.pdf`\n  - `output/iPad/302数学二分节真题集.pdf`\n  - `.github/scripts/test_question_bank.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n- **Git 提交**：`a8e46659df271d2027e6a038826fe477b28d00a6 feat: grade math questions and expand step-by-step solutions`，已推送至 `origin/main`；本条哈希补记由后续文档提交保存。\n\n---\n M memory/agents.md\n M memory/plan.md\n M memory/progress.md\n M memory/verify.md\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D output/302-question-facsimiles.pdf\n?? .github/scripts/test_mean_value_exams.py\n?? \"output/iPad/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n?? \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2671.tex\"\n?? \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2672.tex\"\n?? \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2673.tex\"\n"}
{}
{"chunk_id":"79b163","wall_time_seconds":1.160438458,"exit_code":0,"original_token_count":216,"output":"{\n  \"status\": \"passed\",\n  \"papers\": [\n    {\n      \"paper\": 1,\n      \"pages\": 25,\n      \"size\": [\n        800,\n        600\n      ],\n      \"minimum_writing_space_bp\": 274.3,\n      \"bookmarks\": 13,\n      \"sampled_lower_limits\": 1,\n      \"sampled_stacked_fractions\": 1\n    },\n    {\n      \"paper\": 2,\n      \"pages\": 25,\n      \"size\": [\n        800,\n        600\n      ],\n      \"minimum_writing_space_bp\": 233.2,\n      \"bookmarks\": 13,\n      \"sampled_lower_limits\": 2,\n      \"sampled_stacked_fractions\": 2\n    },\n    {\n      \"paper\": 3,\n      \"pages\": 25,\n      \"size\": [\n        800,\n        600\n      ],\n      \"minimum_writing_space_bp\": 213.7,\n      \"bookmarks\": 13,\n      \"sampled_lower_limits\": 1,\n      \"sampled_stacked_fractions\": 1\n    }\n  ]\n}\n.................\n----------------------------------------------------------------------\nRan 17 tests in 0.663s\n\nOK\n"}

## tool · 2026-11-12T13:23:16Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"50714a","wall_time_seconds":0.000014041,"exit_code":0,"original_token_count":1705,"output":"# GPT 试题库\n\n本仓库收录 GPT 生成的试题与解析，以及按主题整理的真题资料。考研数学是其中一个专题。\n\n## 考研数学\n\n按《工科数学分析基础》第三版上册组织的考研数学练习资料，包含 **2009–2026 年数学二分节真题**和 **27302 阶段模拟卷**。下载 PDF 即可使用，也可编辑 LaTeX 源稿。\n\n### 下载资料\n\n| 资料 | 内容 | 下载 |\n| --- | --- | --- |\n| 数学二分节真题集 | 按教材四章 19 节整理 234 道真题。各节附定理与要点，题目保留年份和原卷题号，每题后另页附解析。 | [横屏 PDF](output/302数学二分节真题集（原生LaTeX横屏版）.pdf) · [横屏源稿](output/302数学二分节真题集（原生LaTeX横屏版）.tex) · [A4 编译入口](output/302数学二分节真题集（原生LaTeX常规版）.tex) |\n| 27302 阶段模拟卷（iPad 横屏版） | 五套模拟卷和 76 道补充练习，共 186 道题。每题单独一页，留有手写区，翻页可看解题思路、推导与答案。 | [横屏 PDF](output/pdf/27302阶段模拟卷（iPad横屏版）.pdf) |\n| 27302 阶段模拟卷（A4） | 适合打印和限时练习。每套 22 题，满分 150 分，建议用时 180 分钟。 | [第一卷 PDF](output/27302阶段模拟卷.pdf) · [第二至五卷及补充练习 PDF](output/27302阶段模拟卷（第二至五卷及补充练习）.pdf) |\n\n### 练习范围\n\n- **分节刷真题**：真题集覆盖教材上册的函数、极限与连续，一元函数微分学，一元函数积分学和常微分方程。可用 PDF 目录跳到正在复习的小节。\n- **做阶段模拟**：五套模拟卷及补充练习覆盖第一章至第二章第四节「微分中值定理及其应用」。每套包含 10 道单选、6 道填空和 6 道解答题。\n\n### 编辑与编译\n\nLaTeX 源文件位于 `output/`。使用带有 `ctex`、Fandol 字体和 TikZ 的 XeLaTeX 环境，在该目录编译所需的 `.tex` 文件。\n\n- 数学二真题集的 A4 编译入口读取同目录的横屏源稿，两种版式共用题目和解析。\n- 27302 模拟卷提供 [第一卷源稿](output/27302阶段模拟卷.tex) 和 [第二至五卷及补充练习源稿](output/27302阶段模拟卷（第二至五卷及补充练习）.tex)。\n\n推送到 `main` 后，GitHub Actions 会编译本次改动影响的 TeX 文档，并将 PDF 上传到 [Releases](https://github.com/OyamaMeek/codex-question-bank/releases)。自动版本从 `v0.0.1` 递增至 `v0.0.999`。如需注明具体改动，在相关 Git 提交正文的末尾留一个空行，再写 `Release-Note: 补充第二至五卷解析`。没有该字段时，发布说明会列出更新的文档名。\n\n## 开发记录\n\n资料的编排和修订历史见 [开发记录](docs/CHANGELOG.md)。\n## [2026-11-12 20:13] 为数学二分节真题增加难度及详细解析\n\n- **需求/问题描述**：\n  > 每道题增加一至五星难度，各节由易到难排序；面向基础薄弱的学习者写清条件、方法依据、推导与检查，并修正分数排版。\n- **实际实现的功能与改动**：\n  - 为全部 234 题增加文字星级，同难度保留原先后次序，显示题序连续，原卷年份、题号及小节归属保留。\n  - 逐题扩写已知与目标、方法与条件、推导、结论与检查，补足初次使用的必要术语解释、关键计算、各小问及适用条件；清除紧缩分式和斜杠分数，修正括号命令和缺字。\n  - 234 份题干、选项和图形与修改前完全一致。五项回归检查通过，第四章独立复核及 48 项数值检查通过。\n  - 横屏和 A4 共用源稿编译成功，分别为 488 页、471 页，日志无缺字、警告或溢出。两版均核对 234 道题和解析、逐题星级、解析分页、23 个书签及文字边界；抽查字形坐标确认上下分式。覆盖现有横屏及 iPad PDF；未进行截图或实机验证。\n- **涉及文件**：\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.tex`\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.pdf`\n  - `output/iPad/302数学二分节真题集.pdf`\n  - `.github/scripts/test_question_bank.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n- **Git 提交**：`a8e46659df271d2027e6a038826fe477b28d00a6 feat: grade math questions and expand step-by-step solutions`，已推送至 `origin/main`；本条哈希补记由后续文档提交保存。\n\n---\n# 进度\n\n## 当前任务：中值定理阶段三套模拟卷\n\n- [x] 核对教材目录和第 147–153 页中值定理正文；明确截止 4.2，筛选本地题源。\n- [x] 确认现有 Git 删除及未跟踪 iPad 模拟卷，保留用户当前状态。\n- [ ] 完成三卷共 36 题及逐题解析、原题定位和范围检查。\n- [ ] 编译三份 PDF，检查题解交替、页面比例、留白、文字边界、数学结果。\n- [ ] 更新开发记录与资料入口，提交并普通推送。\n\n## 当前任务：分节真题难度与详细解析\n\n- [x] 核实共用源稿有 234 题、19 节，两种版式共用题库；Git 初始存在裁片 PDF 删除及未跟踪 iPad 目录。\n- [x] 234 题逐题补充四部分解析、难度与上下分式；中断时未完成移动的 2023 年第 5 题、2019 年第 13 题已按原题恢复并扩写。\n- [x] 完成全部节内稳定排序，同星保留原序，题头用计数器连续编号。星级 1–5 依次为 6、110、88、29、1 题。\n# 完成标准\n\n## 当前任务：中值定理阶段三套模拟卷\n\n每卷 12 题：选择 4×5 分、填空 4×5 分、解答 4×15 分，总分 100；共 36 题且无跨卷原题重复。逐题注明 `302模拟27md` 中的作者、卷次、题号和改动；解法只用第一章至 2.4.2。三份 PDF 各 25 页（封面 1 页、12 对题解页），全部 800×600 bp；每题下方至少 200 bp 空白，解析只出现在紧邻下一页，所有正文在边界内。公式统一上下分式、lim 下置条件。逐题复算并用数值和反例补验关键极限及命题，编译日志无缺字和溢出。不进行未授权截图或图像检查；不宣称实机验证。\n\n## 当前任务：分节真题难度与详细解析\n\n- 234 个原卷年份与题号组合保持一致，各题保留原小节、题干、选项、图形和全部小问；234 份解析与题目一一对应。\n- 题头均有 1–5 个文字 `*`，各节难度非递减；同难度保留原顺序；显示题序连续。\n- 每份解析包含条件与目标、方法依据、必要中间计算、明确结论和针对性检查；逐题校订，客观结构检查不能替代数学正确性检查。\n- 数学算式不使用斜杠分数、Unicode 分数字符或紧缩的 `\\tfrac`；分子分母及指数分组正确。\n2026-11-12 21:23\n"}
{"chunk_id":"27ae81","wall_time_seconds":0.000010125,"exit_code":0,"original_token_count":0,"output":""}

## tool · 2026-11-12T13:24:15Z


Script completed
Wall time 1.1 seconds
Output:

{}
{"chunk_id":"c8f583","wall_time_seconds":0.747018,"exit_code":0,"original_token_count":38,"output":".................\n----------------------------------------------------------------------\nRan 17 tests in 0.511s\n\nOK\n[(1, True), (2, True), (3, True)]\n"}

## tool · 2026-11-12T13:24:27Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"2b3c7d","wall_time_seconds":0,"exit_code":128,"original_token_count":30,"output":"fatal: Unable to create '/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git/index.lock': Operation not permitted\n"}
{"chunk_id":"d65d2d","wall_time_seconds":0.000016166,"exit_code":0,"original_token_count":1249,"output":"origin\thttps://github.com/OyamaMeek/codex-question-bank.git (fetch)\norigin\thttps://github.com/OyamaMeek/codex-question-bank.git (push)\n- **实际实现的功能与改动**：\n  - 为全部 234 题增加文字星级，同难度保留原先后次序，显示题序连续，原卷年份、题号及小节归属保留。\n  - 逐题扩写已知与目标、方法与条件、推导、结论与检查，补足初次使用的必要术语解释、关键计算、各小问及适用条件；清除紧缩分式和斜杠分数，修正括号命令和缺字。\n  - 234 份题干、选项和图形与修改前完全一致。五项回归检查通过，第四章独立复核及 48 项数值检查通过。\n  - 横屏和 A4 共用源稿编译成功，分别为 488 页、471 页，日志无缺字、警告或溢出。两版均核对 234 道题和解析、逐题星级、解析分页、23 个书签及文字边界；抽查字形坐标确认上下分式。覆盖现有横屏及 iPad PDF；未进行截图或实机验证。\n- **涉及文件**：\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.tex`\n  - `output/302数学二分节真题集（原生LaTeX横屏版）.pdf`\n  - `output/iPad/302数学二分节真题集.pdf`\n  - `.github/scripts/test_question_bank.py`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`、`memory/gotchas.md`\n- **Git 提交**：`a8e46659df271d2027e6a038826fe477b28d00a6 feat: grade math questions and expand step-by-step solutions`，已推送至 `origin/main`；本条哈希补记由后续文档提交保存。\n\n---\n\n## [2026-11-12 21:23] 编写中值定理阶段三套模拟卷\n\n- **需求/问题描述**：\n  > 使用 302模拟27md 中的试题，参考教材上册大纲，截至微分中值定理编成三套稍有难度的模拟卷。采用 LaTeX、上下分式、lim 下置条件，适配 iPad 4:3 横屏，一题一页并留白，下一页提供耐心、严谨的详细解析。\n- **实际实现的功能与改动**：\n  - 选编李林、张宇、李艳芳、武忠祥的 36 道题或独立小问；每卷 4 道选择、4 道填空、4 道解答，共 100 分，建议 120 分钟。逐题记录作者、卷次、原题号及改编情况。\n  - 按教材第一章至第二章 4.2 确定范围，使用导数定义、极限性质和中值定理完成推导。每份解析包括已知与目标、方法与条件、推导、结论与检查，证明逐项说明定理条件。\n  - 交付三份独立可编辑 LaTeX 和三份 800×600 bp PDF，每份 25 页，题页与解析页严格交替。题页最少留白分别为 274.3、233.2、213.7 bp；各卷均有 13 个导航书签。\n  - Tectonic 编译全部通过，最终日志无缺字、警告或溢出；17 项回归测试通过，覆盖题解结构、关键极限、参数导数、函数关系与数列递推。检查全部页数、题序、题解对应和文字边界，抽查 lim 条件及上下分式的 PDF 坐标。未进行截图或 iPad 实机检查。\n  - 保留任务开始前的旧模拟卷文件删除、裁片 PDF 删除及未跟踪 iPad 模拟卷，不将其纳入本次提交。\n- **涉及文件**：\n  - `output/中值定理阶段模拟卷1.tex`、`output/中值定理阶段模拟卷1.pdf`\n  - `output/中值定理阶段模拟卷2.tex`、`output/中值定理阶段模拟卷2.pdf`\n  - `output/中值定理阶段模拟卷3.tex`、`output/中值定理阶段模拟卷3.pdf`\n  - `.github/scripts/test_mean_value_exams.py`、`README.md`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n- **Git 提交**：待提交；编译和验证已完成。\n\n---\n# 进度\n\n## 当前任务：中值定理阶段三套模拟卷\n\n- [x] 核对教材目录和第 147–153 页中值定理正文；明确截止 4.2，筛选本地题源。\n- [x] 确认现有 Git 删除及未跟踪 iPad 模拟卷，保留用户当前状态。\n- [x] 完成三卷共 36 题及逐题解析，注明作者、卷次、题号、所选小问和改题型情况；所有方法截至教材 2.4.2。\n- [x] 三份 PDF 均为 25 页、800×600 bp，12 对题解页紧邻交替；各卷最少手写留白 274.3、233.2、213.7 bp，各有 13 个书签，日志无缺字或溢出。抽查 4 个 lim 下标与 4 个上下分式的坐标。\n- [x] 17 项项目回归测试通过（新增 4 项），包含关键极限双侧数值检验、参数二阶导数、函数关系和 8 个不同初值的数列递推；逐题解析同步复算。\n- [x] 三份 PDF 已保存至 `output/`，资料入口及开发记录已更新；未做截图或 iPad 实机验证。\n- [ ] 提交并普通推送当前 `origin/main`，补记实际提交哈希。\n\n## 当前任务：分节真题难度与详细解析\n\n- [x] 核实共用源稿有 234 题、19 节，两种版式共用题库；Git 初始存在裁片 PDF 删除及未跟踪 iPad 目录。\n- [x] 234 题逐题补充四部分解析、难度与上下分式；中断时未完成移动的 2023 年第 5 题、2019 年第 13 题已按原题恢复并扩写。\n"}

## tool · 2026-11-12T13:34:52Z


Script running with cell ID g4:35
Wall time 31.0 seconds
Output:


## tool · 2026-11-12T13:34:58Z


Script completed
Wall time 0.0 seconds
Output:

{"chunk_id":"4501af","wall_time_seconds":0.000041666,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"cac2e7","wall_time_seconds":0.00001225,"exit_code":0,"original_token_count":451,"output":" .github/scripts/test_mean_value_exams.py           |  78 +++++\n README.md                                          |   2 +\n docs/CHANGELOG.md                                  |  20 ++\n memory/agents.md                                   |   2 +\n memory/plan.md                                     |   6 +\n memory/progress.md                                 |  10 +\n memory/verify.md                                   |   8 +\n ...6\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2671.pdf\" | Bin 0 -> 204613 bytes\n ...6\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2671.tex\" | 321 +++++++++++++++++++++\n ...6\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2672.pdf\" | Bin 0 -> 215805 bytes\n ...6\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2672.tex\" | 309 ++++++++++++++++++++\n ...6\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2673.pdf\" | Bin 0 -> 210951 bytes\n ...6\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2673.tex\" | 313 ++++++++++++++++++++\n 13 files changed, 1069 insertions(+)\n.github/scripts/test_mean_value_exams.py\nREADME.md\ndocs/CHANGELOG.md\nmemory/agents.md\nmemory/plan.md\nmemory/progress.md\nmemory/verify.md\n\"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2671.pdf\"\n\"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2671.tex\"\n\"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2672.pdf\"\n\"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2672.tex\"\n\"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2673.pdf\"\n\"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2673.tex\"\n"}

## assistant · 2026-11-12T13:35:03Z

三卷 PDF 和 LaTeX 源稿已保存，17 项回归测试及 PDF 分页、留白和公式坐标检查全部通过。范围截至教材第二章 4.2。现在按项目规则提交并推送本次文件，原有删除和移动不纳入提交。


## tool · 2026-11-12T13:35:10Z


Script completed
Wall time 3.5 seconds
Output:

{"chunk_id":"fc5638","wall_time_seconds":0.000030458,"exit_code":0,"original_token_count":257,"output":"[main 763b2e2] feat: add three mean-value theorem mock exams for iPad\n 13 files changed, 1069 insertions(+)\n create mode 100644 .github/scripts/test_mean_value_exams.py\n create mode 100644 \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2671.pdf\"\n create mode 100644 \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2671.tex\"\n create mode 100644 \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2672.pdf\"\n create mode 100644 \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2672.tex\"\n create mode 100644 \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2673.pdf\"\n create mode 100644 \"output/\\344\\270\\255\\345\\200\\274\\345\\256\\232\\347\\220\\206\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\2673.tex\"\n"}
{"chunk_id":"4622ed","wall_time_seconds":0.000014209,"exit_code":0,"original_token_count":587,"output":"763b2e294e7c7396e975a405689fe7bb09301c00\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D output/302-question-facsimiles.pdf\n?? \"output/iPad/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n  - `output/中值定理阶段模拟卷1.tex`、`output/中值定理阶段模拟卷1.pdf`\n  - `output/中值定理阶段模拟卷2.tex`、`output/中值定理阶段模拟卷2.pdf`\n  - `output/中值定理阶段模拟卷3.tex`、`output/中值定理阶段模拟卷3.pdf`\n  - `.github/scripts/test_mean_value_exams.py`、`README.md`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n- **Git 提交**：待提交；编译和验证已完成。\n\n---\n# 进度\n\n## 当前任务：中值定理阶段三套模拟卷\n\n- [x] 核对教材目录和第 147–153 页中值定理正文；明确截止 4.2，筛选本地题源。\n- [x] 确认现有 Git 删除及未跟踪 iPad 模拟卷，保留用户当前状态。\n- [x] 完成三卷共 36 题及逐题解析，注明作者、卷次、题号、所选小问和改题型情况；所有方法截至教材 2.4.2。\n- [x] 三份 PDF 均为 25 页、800×600 bp，12 对题解页紧邻交替；各卷最少手写留白 274.3、233.2、213.7 bp，各有 13 个书签，日志无缺字或溢出。抽查 4 个 lim 下标与 4 个上下分式的坐标。\n- [x] 17 项项目回归测试通过（新增 4 项），包含关键极限双侧数值检验、参数二阶导数、函数关系和 8 个不同初值的数列递推；逐题解析同步复算。\n- [x] 三份 PDF 已保存至 `output/`，资料入口及开发记录已更新；未做截图或 iPad 实机验证。\n- [ ] 提交并普通推送当前 `origin/main`，补记实际提交哈希。\n\n## 当前任务：分节真题难度与详细解析\n\n"}

## tool · 2026-11-12T13:35:33Z


Script completed
Wall time 18.1 seconds
Output:

{"chunk_id":"fa7b3f","wall_time_seconds":1.00147175,"session_id":33041,"original_token_count":0,"output":""}

## tool · 2026-11-12T13:35:37Z


Script completed
Wall time 0.0 seconds
Output:

{"chunk_id":"b23b6c","wall_time_seconds":0.0000105,"exit_code":0,"original_token_count":23,"output":"To https://github.com/OyamaMeek/codex-question-bank.git\n   87e8b36..763b2e2  main -> main\n"}

## tool · 2026-11-12T13:35:57Z


Script completed
Wall time 6.2 seconds
Output:

{"chunk_id":"f8490e","wall_time_seconds":0.000008708,"exit_code":0,"original_token_count":399,"output":"  - `output/中值定理阶段模拟卷1.tex`、`output/中值定理阶段模拟卷1.pdf`\n  - `output/中值定理阶段模拟卷2.tex`、`output/中值定理阶段模拟卷2.pdf`\n  - `output/中值定理阶段模拟卷3.tex`、`output/中值定理阶段模拟卷3.pdf`\n  - `.github/scripts/test_mean_value_exams.py`、`README.md`\n  - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n- **Git 提交**：待提交；编译和验证已完成。\n\n---\n# 进度\n\n## 当前任务：中值定理阶段三套模拟卷\n\n- [x] 核对教材目录和第 147–153 页中值定理正文；明确截止 4.2，筛选本地题源。\n- [x] 确认现有 Git 删除及未跟踪 iPad 模拟卷，保留用户当前状态。\n- [x] 完成三卷共 36 题及逐题解析，注明作者、卷次、题号、所选小问和改题型情况；所有方法截至教材 2.4.2。\n- [x] 三份 PDF 均为 25 页、800×600 bp，12 对题解页紧邻交替；各卷最少手写留白 274.3、233.2、213.7 bp，各有 13 个书签，日志无缺字或溢出。抽查 4 个 lim 下标与 4 个上下分式的坐标。\n- [x] 17 项项目回归测试通过（新增 4 项），包含关键极限双侧数值检验、参数二阶导数、函数关系和 8 个不同初值的数列递推；逐题解析同步复算。\n- [x] 三份 PDF 已保存至 `output/`，资料入口及开发记录已更新；未做截图或 iPad 实机验证。\n- [ ] 提交并普通推送当前 `origin/main`，补记实际提交哈希。\n\n763b2e294e7c7396e975a405689fe7bb09301c00\n763b2e294e7c7396e975a405689fe7bb09301c00\n"}
{}
{"chunk_id":"33a78d","wall_time_seconds":0.000008791,"exit_code":0,"original_token_count":435,"output":"diff --git a/docs/CHANGELOG.md b/docs/CHANGELOG.md\nindex 5f52bfb..8a6b208 100644\n--- a/docs/CHANGELOG.md\n+++ b/docs/CHANGELOG.md\n@@ -491,6 +491,6 @@\n   - `output/中值定理阶段模拟卷3.tex`、`output/中值定理阶段模拟卷3.pdf`\n   - `.github/scripts/test_mean_value_exams.py`、`README.md`\n   - `memory/agents.md`、`memory/plan.md`、`memory/progress.md`、`memory/verify.md`\n-- **Git 提交**：待提交；编译和验证已完成。\n+- **Git 提交**：`763b2e294e7c7396e975a405689fe7bb09301c00 feat: add three mean-value theorem mock exams for iPad`，已普通推送至 `origin/main`；本条实际哈希通过后续文档提交保存。\n \n ---\ndiff --git a/memory/progress.md b/memory/progress.md\nindex cfed64f..bb96ec6 100644\n--- a/memory/progress.md\n+++ b/memory/progress.md\n@@ -8,7 +8,7 @@\n - [x] 三份 PDF 均为 25 页、800×600 bp，12 对题解页紧邻交替；各卷最少手写留白 274.3、233.2、213.7 bp，各有 13 个书签，日志无缺字或溢出。抽查 4 个 lim 下标与 4 个上下分式的坐标。\n - [x] 17 项项目回归测试通过（新增 4 项），包含关键极限双侧数值检验、参数二阶导数、函数关系和 8 个不同初值的数列递推；逐题解析同步复算。\n - [x] 三份 PDF 已保存至 `output/`，资料入口及开发记录已更新；未做截图或 iPad 实机验证。\n-- [ ] 提交并普通推送当前 `origin/main`，补记实际提交哈希。\n+- [x] 交付已提交为 `763b2e2`，普通推送至当前 `origin/main` 成功；实际哈希已补入开发记录，补记通过后续文档提交保存。任务开始前的五个删除和一份未跟踪 iPad 模拟卷保持原状态。\n \n ## 当前任务：分节真题难度与详细解析\n \n"}
{"chunk_id":"3ff67d","wall_time_seconds":0.000011084,"exit_code":0,"original_token_count":54,"output":" docs/CHANGELOG.md  | 2 +-\n memory/progress.md | 2 +-\n 2 files changed, 2 insertions(+), 2 deletions(-)\n[main d16343b] docs: record mean-value exam delivery commit\n 2 files changed, 2 insertions(+), 2 deletions(-)\n"}
{"chunk_id":"f3355c","wall_time_seconds":1.001852458,"session_id":46469,"original_token_count":0,"output":""}

## tool · 2026-11-12T13:36:04Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"11d706","wall_time_seconds":0.000017833,"exit_code":0,"original_token_count":23,"output":"To https://github.com/OyamaMeek/codex-question-bank.git\n   763b2e2..d16343b  main -> main\n"}
{"chunk_id":"870383","wall_time_seconds":0.000009333,"exit_code":0,"original_token_count":373,"output":" D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.tex\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.pdf\"\n D \"output/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267\\357\\274\\210\\347\\254\\254\\344\\272\\214\\350\\207\\263\\344\\272\\224\\345\\215\\267\\345\\217\\212\\350\\241\\245\\345\\205\\205\\347\\273\\203\\344\\271\\240\\357\\274\\211.tex\"\n D output/302-question-facsimiles.pdf\n?? \"output/iPad/27302\\351\\230\\266\\346\\256\\265\\346\\250\\241\\346\\213\\237\\345\\215\\267.pdf\"\nd16343b23b7bab0de2357e3c5401c6f33017e9fa\nd16343b23b7bab0de2357e3c5401c6f33017e9fa\nd16343b docs: record mean-value exam delivery commit\n763b2e2 feat: add three mean-value theorem mock exams for iPad\n-rw-r--r--  1 oyamahappa  staff   200K Nov 12 21:23 output/中值定理阶段模拟卷1.pdf\n-rw-r--r--  1 oyamahappa  staff    16K Nov 12 21:21 output/中值定理阶段模拟卷1.tex\n-rw-r--r--  1 oyamahappa  staff   211K Nov 12 21:23 output/中值定理阶段模拟卷2.pdf\n-rw-r--r--  1 oyamahappa  staff    17K Nov 12 21:21 output/中值定理阶段模拟卷2.tex\n-rw-r--r--  1 oyamahappa  staff   206K Nov 12 21:23 output/中值定理阶段模拟卷3.pdf\n-rw-r--r--  1 oyamahappa  staff    17K Nov 12 21:21 output/中值定理阶段模拟卷3.tex\n"}

## assistant · 2026-11-12T13:36:20Z

已完成三卷，共 36 题。每卷 **100 分、25 页**，范围截至教材第二章 4.2 微分中值定理。采用 **4:3 横屏、一题一页、下方留白、次页详解**，分数上下排列，极限条件置于 lim 下方。

:codex-file-citation{path="/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷1.pdf" purpose="output"}

:codex-file-citation{path="/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷2.pdf" purpose="output"}

:codex-file-citation{path="/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷3.pdf" purpose="output"}

可编辑 LaTeX：[卷一](/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷1.tex) · [卷二](/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷2.tex) · [卷三](/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/output/中值定理阶段模拟卷3.tex)。

已通过编译、分页检查和 17 项回归测试，并已提交推送。未做截图或 iPad 实机检查。
