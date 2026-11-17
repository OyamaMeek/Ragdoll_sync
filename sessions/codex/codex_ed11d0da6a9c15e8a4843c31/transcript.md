# 01a1b563-65a8-7d80-8d6f-e86837f2e463

来源：codex

项目：/Users/oyamahappa/Documents/Agent/Codex

## developer · 2026-11-07T09:42:36Z

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



## developer · 2026-11-07T09:42:36Z

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
- google-drive:google-drive: Use connected Google Drive as the single entrypoint for Drive, D (file: r17/google-drive/SKILL.md)
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

## developer · 2026-11-07T09:42:36Z

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

## developer · 2026-11-07T09:42:36Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-07T09:42:36Z

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

## developer · 2026-11-07T09:42:36Z

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


## developer · 2026-11-07T09:42:36Z

<tools>
Added deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
</tools>

## assistant · 2026-11-07T09:42:40Z

妹妹，我会检查九行标准动画的静态形态和 GIF 帧序列，重点核对跳跃升空、行走交替、朝向及各行动作语义。


## tool · 2026-11-07T09:42:44Z


Script completed
Wall time 0.1 seconds
Output:

-rw-r--r--  1 oyamahappa  staff  441230 Nov  7 17:42 .agent/clawd-pet/qa/contact-sheet.png
-rw-r--r--  1 oyamahappa  staff   46847 Nov  7 17:42 .agent/clawd-pet/qa/previews/failed.gif
-rw-r--r--  1 oyamahappa  staff   38540 Nov  7 17:42 .agent/clawd-pet/qa/previews/idle.gif
-rw-r--r--  1 oyamahappa  staff   28135 Nov  7 17:42 .agent/clawd-pet/qa/previews/jumping.gif
-rw-r--r--  1 oyamahappa  staff   38144 Nov  7 17:42 .agent/clawd-pet/qa/previews/review.gif
-rw-r--r--  1 oyamahappa  staff   53632 Nov  7 17:42 .agent/clawd-pet/qa/previews/running-left.gif
-rw-r--r--  1 oyamahappa  staff   53810 Nov  7 17:42 .agent/clawd-pet/qa/previews/running-right.gif
-rw-r--r--  1 oyamahappa  staff   35996 Nov  7 17:42 .agent/clawd-pet/qa/previews/running.gif
-rw-r--r--  1 oyamahappa  staff   31056 Nov  7 17:42 .agent/clawd-pet/qa/previews/waiting.gif
-rw-r--r--  1 oyamahappa  staff   19710 Nov  7 17:42 .agent/clawd-pet/qa/previews/waving.gif
-rw-r--r--  1 oyamahappa  staff   25240 Nov  7 17:42 .agent/clawd-pet/qa/review.json

{
  "ok": true,
  "frames_root": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames",
  "states": [
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
  "errors": [],
  "warnings": [
    "jumping used extraction method stable-slots; confirm motion playback remains stable and unclipped"
  ],
  "rows": [
    {
      "state": "idle",
      "expected_frames": 6,
      "actual_frames": 6,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/idle/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16589,
          "bbox": [
            5,
            40,
            187,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 224
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/idle/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17147,
          "bbox": [
            6,
            32,
            183,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 373
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/idle/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17297,
          "bbox": [
            6,
            32,
            186,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 476
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/idle/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16597,
          "bbox": [
            5,
            40,
            186,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 272
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/idle/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16303,
          "bbox": [
            9,
            40,
            183,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 219
        },
        {
          "index": 5,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/idle/05.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16364,
          "bbox": [
            9,
            40,
            183,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 300
        }
      ]
    },
    {
      "state": "running-right",
      "expected_frames": 8,
      "actual_frames": 8,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 19198,
          "bbox": [
            6,
            23,
            186,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 353
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18919,
          "bbox": [
            6,
            23,
            185,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 201
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18334,
          "bbox": [
            7,
            23,
            185,
            178
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 162
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18807,
          "bbox": [
            7,
            23,
            185,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 235
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 19098,
          "bbox": [
            6,
            23,
            185,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 177
        },
        {
          "index": 5,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/05.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18930,
          "bbox": [
            6,
            22,
            186,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 279
        },
        {
          "index": 6,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/06.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18990,
          "bbox": [
            6,
            23,
            185,
            178
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 175
        },
        {
          "index": 7,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-right/07.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 19073,
          "bbox": [
            6,
            23,
            186,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 313
        }
      ]
    },
    {
      "state": "running-left",
      "expected_frames": 8,
      "actual_frames": 8,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 19198,
          "bbox": [
            6,
            23,
            186,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 353
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18923,
          "bbox": [
            6,
            23,
            185,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 211
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18334,
          "bbox": [
            7,
            23,
            185,
            178
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 162
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18807,
          "bbox": [
            7,
            23,
            185,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 235
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 19098,
          "bbox": [
            6,
            23,
            185,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 193
        },
        {
          "index": 5,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/05.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18930,
          "bbox": [
            6,
            22,
            186,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 279
        },
        {
          "index": 6,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/06.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 18995,
          "bbox": [
            6,
            23,
            185,
            178
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 177
        },
        {
          "index": 7,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running-left/07.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 19073,
          "bbox": [
            6,
            23,
            186,
            185
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 313
        }
      ]
    },
    {
      "state": "waving",
      "expected_frames": 4,
      "actual_frames": 4,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waving/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15651,
          "bbox": [
            8,
            38,
            184,
            170
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 119
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waving/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15999,
          "bbox": [
            7,
            39,
            185,
            169
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 136
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waving/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16147,
          "bbox": [
            5,
            38,
            187,
            169
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 175
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waving/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15768,
          "bbox": [
            8,
            38,
            184,
            170
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 171
        }
      ]
    },
    {
      "state": "jumping",
      "expected_frames": 5,
      "actual_frames": 5,
      "extraction_method": "stable-slots",
      "ok": true,
      "errors": [],
      "warnings": [
        "jumping used extraction method stable-slots; confirm motion playback remains stable and unclipped"
      ],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/jumping/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16328,
          "bbox": [
            5,
            54,
            186,
            187
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 102
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/jumping/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16213,
          "bbox": [
            5,
            38,
            187,
            170
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 192
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/jumping/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16255,
          "bbox": [
            6,
            20,
            186,
            154
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 172
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/jumping/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16571,
          "bbox": [
            5,
            31,
            186,
            167
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 199
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/jumping/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16439,
          "bbox": [
            5,
            54,
            187,
            187
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 120
        }
      ]
    },
    {
      "state": "failed",
      "expected_frames": 8,
      "actual_frames": 8,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16157,
          "bbox": [
            7,
            33,
            185,
            170
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 299
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15877,
          "bbox": [
            7,
            34,
            185,
            170
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 311
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15051,
          "bbox": [
            6,
            43,
            185,
            170
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 371
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 14688,
          "bbox": [
            7,
            53,
            185,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 387
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 13441,
          "bbox": [
            7,
            64,
            185,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 300
        },
        {
          "index": 5,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/05.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 14937,
          "bbox": [
            6,
            48,
            186,
            175
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 291
        },
        {
          "index": 6,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/06.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15716,
          "bbox": [
            7,
            37,
            185,
            172
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 151
        },
        {
          "index": 7,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/failed/07.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16117,
          "bbox": [
            7,
            33,
            185,
            170
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 195
        }
      ]
    },
    {
      "state": "waiting",
      "expected_frames": 6,
      "actual_frames": 6,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waiting/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17306,
          "bbox": [
            6,
            35,
            186,
            172
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 302
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waiting/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17263,
          "bbox": [
            5,
            35,
            186,
            172
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 279
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waiting/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17174,
          "bbox": [
            6,
            35,
            186,
            172
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 224
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waiting/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17252,
          "bbox": [
            6,
            35,
            186,
            172
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 271
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waiting/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17276,
          "bbox": [
            5,
            35,
            187,
            172
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 307
        },
        {
          "index": 5,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/waiting/05.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17241,
          "bbox": [
            5,
            35,
            187,
            172
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 216
        }
      ]
    },
    {
      "state": "running",
      "expected_frames": 6,
      "actual_frames": 6,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 20781,
          "bbox": [
            6,
            26,
            185,
            181
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 306
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 20787,
          "bbox": [
            6,
            26,
            184,
            181
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 305
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 20876,
          "bbox": [
            5,
            26,
            186,
            181
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 287
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 21146,
          "bbox": [
            5,
            26,
            187,
            181
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 325
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 20885,
          "bbox": [
            6,
            26,
            185,
            181
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 207
        },
        {
          "index": 5,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/running/05.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 20648,
          "bbox": [
            7,
            26,
            185,
            181
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 291
        }
      ]
    },
    {
      "state": "review",
      "expected_frames": 6,
      "actual_frames": 6,
      "extraction_method": null,
      "ok": true,
      "errors": [],
      "warnings": [],
      "frames": [
        {
          "index": 0,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/review/00.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16729,
          "bbox": [
            5,
            39,
            187,
            177
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 273
        },
        {
          "index": 1,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/review/01.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 17032,
          "bbox": [
            8,
            31,
            186,
            177
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 256
        },
        {
          "index": 2,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/review/02.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15912,
          "bbox": [
            6,
            47,
            185,
            177
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 198
        },
        {
          "index": 3,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/review/03.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 15956,
          "bbox": [
            8,
            47,
            186,
            177
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 204
        },
        {
          "index": 4,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/review/04.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16668,
          "bbox": [
            6,
            37,
            184,
            177
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 256
        },
        {
          "index": 5,
          "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/frames/review/05.png",
          "width": 192,
          "height": 208,
          "nontransparent_pixels": 16676,
          "bbox": [
            5,
            39,
            184,
            177
          ],
          "edge_pixels": 0,
          "chroma_adjacent_pixels": 222
        }
      ]
    }
  ]
}

{
  "type": "input_image",
  "image_url": "images/fe7ac0b8b6abc315b0a4335caecdf9e4d520198bcee205d5c6ed99ab74874195.png",
  "detail": "high"
}

## tool · 2026-11-07T09:42:53Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"327be7","wall_time_seconds":0.000008833,"exit_code":1,"original_token_count":30,"output":"Traceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nModuleNotFoundError: No module named 'PIL'\n"}

## tool · 2026-11-07T09:43:00Z


Script completed
Wall time 0.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/9dfa982b2f7090b47bb0b184e080f282818c9e0e90b095d4b029a15c1078b526.png",
  "detail": "high"
}
{"chunk_id":"23b09b","wall_time_seconds":0.000010292,"exit_code":127,"original_token_count":8,"output":"zsh:1: command not found: -v\n"}

## tool · 2026-11-07T09:43:05Z




## tool · 2026-11-07T09:43:07Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"1159fc","wall_time_seconds":0.000018167,"exit_code":0,"original_token_count":15,"output":"/usr/bin/python3\n/opt/homebrew/bin/uv\n/opt/homebrew/bin/uv\n"}

## tool · 2026-11-07T09:43:25Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"0181b8","wall_time_seconds":0.000008583,"exit_code":0,"original_token_count":235,"output":"[{\"state\": \"waiting\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [150, 150, 150, 150, 150, 260]}, {\"state\": \"jumping\", \"size\": [192, 208], \"frames\": 5, \"duration_ms\": [140, 140, 140, 140, 280]}, {\"state\": \"running\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [120, 120, 120, 120, 120, 220]}, {\"state\": \"running-left\", \"size\": [192, 208], \"frames\": 8, \"duration_ms\": [120, 120, 120, 120, 120, 120, 120, 220]}, {\"state\": \"waving\", \"size\": [192, 208], \"frames\": 4, \"duration_ms\": [140, 140, 140, 280]}, {\"state\": \"failed\", \"size\": [192, 208], \"frames\": 8, \"duration_ms\": [140, 140, 140, 140, 140, 140, 140, 240]}, {\"state\": \"review\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [150, 150, 150, 150, 150, 280]}, {\"state\": \"idle\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [280, 110, 110, 140, 140, 320]}, {\"state\": \"running-right\", \"size\": [192, 208], \"frames\": 8, \"duration_ms\": [120, 120, 120, 120, 120, 120, 120, 220]}]\n"}

## tool · 2026-11-07T09:43:39Z


Script completed
Wall time 0.2 seconds
Output:

idle, running-right, running-left
{
  "type": "input_image",
  "image_url": "images/4261e82b60d25f28d80173c31ad4028246afd9a40d03e073cf9c39b846561bd5.png",
  "detail": "high"
}
waving, jumping, failed
{
  "type": "input_image",
  "image_url": "images/dec29bc55802b89c9beae9b43c6b9337e591b452d59868993b00ed0f5bd3ca96.png",
  "detail": "high"
}
waiting, running, review
{
  "type": "input_image",
  "image_url": "images/c9894c2f594e25a8ee2787722dba209076f14027fcef02735af5ca5c641a4c1d.png",
  "detail": "high"
}

## tool · 2026-11-07T09:44:02Z




## assistant · 2026-11-07T09:44:19Z

standard_qa=fail

- 九行动物身份与像素风格一致，完整无裁剪；动作语义成立。行走左右朝向正确且有交替迈腿，idle 有呼吸和眨眼，running 为原地工作，review 有倾身检查。
- jumping 确实升空：首尾脚底 y=187，顶点 y=154，上升33px，尺度基本稳定。
- 基线不一致：idle175、行走185、waving169–170、failed170–175、waiting172、running181、review177、jumping首尾187。切换状态会产生可见上下位移。
- 行走及 running 的身体比 idle 明显偏大，约10–17%，影响状态切换时的尺度一致性。

需修复：第1、2、7行尺度；除第0行参考基线外，第1–8行统一着地基线，并保留 jumping 的33px升空轨迹。

已逐帧检查全部 GIF 及帧时长；未观看实时循环播放，连续播放的节奏感仍需最终确认。

## tool · 2026-11-07T09:45:30Z


Script completed
Wall time 0.1 seconds
Output:

{
  "ok": true,
  "method": "one fixed scale and translation per entire animation row",
  "target_height": 135,
  "target_baseline": 186,
  "rows": [
    {
      "state": "failed",
      "scale": 0.9854014598540146,
      "shift_y": 18.481751824817508,
      "bounds": [
        [
          8,
          51,
          184,
          186
        ],
        [
          8,
          52,
          184,
          186
        ],
        [
          7,
          61,
          184,
          186
        ],
        [
          8,
          71,
          184,
          191
        ],
        [
          8,
          82,
          184,
          191
        ],
        [
          7,
          66,
          185,
          191
        ],
        [
          8,
          55,
          184,
          188
        ],
        [
          8,
          51,
          184,
          186
        ]
      ]
    },
    {
      "state": "idle",
      "scale": 1.0,
      "shift_y": 11.0,
      "bounds": [
        [
          5,
          51,
          187,
          186
        ],
        [
          6,
          43,
          183,
          186
        ],
        [
          6,
          43,
          186,
          186
        ],
        [
          5,
          51,
          186,
          186
        ],
        [
          9,
          51,
          183,
          186
        ],
        [
          9,
          51,
          183,
          186
        ]
      ]
    },
    {
      "state": "jumping",
      "scale": 1.0150375939849625,
      "shift_y": -3.8120300751879768,
      "bounds": [
        [
          4,
          51,
          187,
          186
        ],
        [
          4,
          35,
          188,
          169
        ],
        [
          5,
          16,
          187,
          153
        ],
        [
          4,
          28,
          187,
          166
        ],
        [
          4,
          51,
          188,
          186
        ]
      ]
    },
    {
      "state": "review",
      "scale": 0.9782608695652174,
      "shift_y": 12.84782608695653,
      "bounds": [
        [
          7,
          51,
          185,
          186
        ],
        [
          10,
          43,
          184,
          186
        ],
        [
          8,
          59,
          183,
          186
        ],
        [
          10,
          59,
          184,
          186
        ],
        [
          8,
          49,
          182,
          186
        ],
        [
          7,
          51,
          182,
          186
        ]
      ]
    },
    {
      "state": "running",
      "scale": 0.8709677419354839,
      "shift_y": 28.35483870967741,
      "bounds": [
        [
          19,
          51,
          174,
          186
        ],
        [
          19,
          51,
          173,
          186
        ],
        [
          17,
          51,
          173,
          186
        ],
        [
          17,
          51,
          175,
          186
        ],
        [
          19,
          51,
          174,
          186
        ],
        [
          18,
          51,
          174,
          186
        ]
      ]
    },
    {
      "state": "running-left",
      "scale": 0.8333333333333334,
      "shift_y": 31.833333333333314,
      "bounds": [
        [
          21,
          51,
          171,
          186
        ],
        [
          21,
          51,
          170,
          186
        ],
        [
          22,
          51,
          170,
          180
        ],
        [
          22,
          51,
          170,
          186
        ],
        [
          21,
          51,
          170,
          186
        ],
        [
          21,
          50,
          171,
          186
        ],
        [
          21,
          51,
          170,
          180
        ],
        [
          21,
          51,
          171,
          186
        ]
      ]
    },
    {
      "state": "running-right",
      "scale": 0.8333333333333334,
      "shift_y": 31.833333333333314,
      "bounds": [
        [
          21,
          51,
          171,
          186
        ],
        [
          21,
          51,
          170,
          186
        ],
        [
          22,
          51,
          170,
          180
        ],
        [
          22,
          51,
          170,
          186
        ],
        [
          21,
          51,
          170,
          186
        ],
        [
          21,
          50,
          171,
          186
        ],
        [
          21,
          51,
          170,
          180
        ],
        [
          21,
          51,
          171,
          186
        ]
      ]
    },
    {
      "state": "waiting",
      "scale": 0.9854014598540146,
      "shift_y": 16.510948905109473,
      "bounds": [
        [
          7,
          51,
          185,
          186
        ],
        [
          6,
          51,
          185,
          186
        ],
        [
          7,
          51,
          185,
          186
        ],
        [
          7,
          51,
          185,
          186
        ],
        [
          6,
          51,
          186,
          186
        ],
        [
          6,
          51,
          186,
          186
        ]
      ]
    },
    {
      "state": "waving",
      "scale": 1.0227272727272727,
      "shift_y": 12.136363636363626,
      "bounds": [
        [
          6,
          51,
          186,
          186
        ],
        [
          5,
          52,
          187,
          185
        ],
        [
          3,
          51,
          189,
          185
        ],
        [
          6,
          51,
          186,
          186
        ]
      ]
    }
  ]
}

{
  "type": "input_image",
  "image_url": "images/c27b0e5f1950c7be6ede8a749dfd840c5b3111e66467b1d0ad47c5362ccde9e7.png",
  "detail": "high"
}

## tool · 2026-11-07T09:45:42Z


Script completed
Wall time 0.2 seconds
Output:

idle, running-right, running-left
{
  "type": "input_image",
  "image_url": "images/30b580ba46250766972ef072c45e5a13d6ece74a1cf6e27abd0d22a19d73aa24.png",
  "detail": "high"
}
waving, jumping, failed
{
  "type": "input_image",
  "image_url": "images/989fe45e36d7c9a21b109b8db6719db7664f65794e10cc525a453c70843f0893.png",
  "detail": "high"
}
waiting, running, review
{
  "type": "input_image",
  "image_url": "images/d5b265ddcf0e8bb86b778b804b8bb697a6fadb78fb63fd7e476761b7ebe01786.png",
  "detail": "high"
}

## assistant · 2026-11-07T09:45:52Z

standard_qa=pass

当前版本未发现需修复行。九行身份与风格一致、完整无裁剪；基线与尺度一致，行走交替及朝向正确，jumping 保留33px升空，idle、running、review 动作语义成立。

已逐帧复查全部 GIF；未观看实时循环播放，节奏感未作最终判定。

## developer · 2026-11-07T09:55:49Z

<tools>
Removed deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__ot
- mcp__pubmed
</tools>

## developer · 2026-11-07T09:55:49Z

<tools>
Added deferred tool namespaces:
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__pubmed
</tools>

## tool · 2026-11-07T09:55:56Z


Script completed
Wall time 0.1 seconds
Output:

{
  "ok": true,
  "errors": [],
  "warnings": [],
  "unconfirmed": [],
  "reviewRequired": false,
  "pairs": [
    {
      "pair": "horizontal-1",
      "axis": "horizontal",
      "gate": "review",
      "A": {
        "observed": "screen-right",
        "expected": "screen-right",
        "source_direction": "022.5",
        "pass": true
      },
      "B": {
        "observed": "screen-left",
        "expected": "screen-left",
        "source_direction": "337.5",
        "pass": true
      }
    },
    {
      "pair": "horizontal-2",
      "axis": "horizontal",
      "gate": "review",
      "A": {
        "observed": "screen-left",
        "expected": "screen-left",
        "source_direction": "315",
        "pass": true
      },
      "B": {
        "observed": "screen-right",
        "expected": "screen-right",
        "source_direction": "045",
        "pass": true
      }
    },
    {
      "pair": "horizontal-3",
      "axis": "horizontal",
      "gate": "review",
      "A": {
        "observed": "screen-right",
        "expected": "screen-right",
        "source_direction": "067.5",
        "pass": true
      },
      "B": {
        "observed": "screen-left",
        "expected": "screen-left",
        "source_direction": "292.5",
        "pass": true
      }
    },
    {
      "pair": "horizontal-4",
      "axis": "horizontal",
      "gate": "hard",
      "A": {
        "observed": "screen-right",
        "expected": "screen-right",
        "source_direction": "090",
        "pass": true
      },
      "B": {
        "observed": "screen-left",
        "expected": "screen-left",
        "source_direction": "270",
        "pass": true
      }
    },
    {
      "pair": "horizontal-5",
      "axis": "horizontal",
      "gate": "review",
      "A": {
        "observed": "screen-left",
        "expected": "screen-left",
        "source_direction": "247.5",
        "pass": true
      },
      "B": {
        "observed": "screen-right",
        "expected": "screen-right",
        "source_direction": "112.5",
        "pass": true
      }
    },
    {
      "pair": "horizontal-6",
      "axis": "horizontal",
      "gate": "review",
      "A": {
        "observed": "screen-left",
        "expected": "screen-left",
        "source_direction": "225",
        "pass": true
      },
      "B": {
        "observed": "screen-right",
        "expected": "screen-right",
        "source_direction": "135",
        "pass": true
      }
    },
    {
      "pair": "horizontal-7",
      "axis": "horizontal",
      "gate": "review",
      "A": {
        "observed": "screen-right",
        "expected": "screen-right",
        "source_direction": "157.5",
        "pass": true
      },
      "B": {
        "observed": "screen-left",
        "expected": "screen-left",
        "source_direction": "202.5",
        "pass": true
      }
    },
    {
      "pair": "vertical-1",
      "axis": "vertical",
      "gate": "hard",
      "A": {
        "observed": "down",
        "expected": "down",
        "source_direction": "180",
        "pass": true
      },
      "B": {
        "observed": "up",
        "expected": "up",
        "source_direction": "000",
        "pass": true
      }
    },
    {
      "pair": "vertical-2",
      "axis": "vertical",
      "gate": "review",
      "A": {
        "observed": "up",
        "expected": "up",
        "source_direction": "022.5",
        "pass": true
      },
      "B": {
        "observed": "down",
        "expected": "down",
        "source_direction": "157.5",
        "pass": true
      }
    },
    {
      "pair": "vertical-3",
      "axis": "vertical",
      "gate": "review",
      "A": {
        "observed": "up",
        "expected": "up",
        "source_direction": "045",
        "pass": true
      },
      "B": {
        "observed": "down",
        "expected": "down",
        "source_direction": "135",
        "pass": true
      }
    },
    {
      "pair": "vertical-4",
      "axis": "vertical",
      "gate": "review",
      "A": {
        "observed": "down",
        "expected": "down",
        "source_direction": "112.5",
        "pass": true
      },
      "B": {
        "observed": "up",
        "expected": "up",
        "source_direction": "067.5",
        "pass": true
      }
    },
    {
      "pair": "vertical-5",
      "axis": "vertical",
      "gate": "review",
      "A": {
        "observed": "up",
        "expected": "up",
        "source_direction": "337.5",
        "pass": true
      },
      "B": {
        "observed": "down",
        "expected": "down",
        "source_direction": "202.5",
        "pass": true
      }
    },
    {
      "pair": "vertical-6",
      "axis": "vertical",
      "gate": "review",
      "A": {
        "observed": "up",
        "expected": "up",
        "source_direction": "315",
        "pass": true
      },
      "B": {
        "observed": "down",
        "expected": "down",
        "source_direction": "225",
        "pass": true
      }
    },
    {
      "pair": "vertical-7",
      "axis": "vertical",
      "gate": "review",
      "A": {
        "observed": "down",
        "expected": "down",
        "source_direction": "247.5",
        "pass": true
      },
      "B": {
        "observed": "up",
        "expected": "up",
        "source_direction": "292.5",
        "pass": true
      }
    }
  ]
}
{
  "ok": true,
  "reviewRequired": true,
  "medianDiffPixels": 626.0,
  "warnings": [
    "045 has transparent interior hole rows (y=152, y=154, y=155, y=157, +2 more)",
    "090 has transparent interior hole rows (y=152, y=153, y=154)",
    "135 has transparent interior hole rows (y=152, y=153, y=154, y=155, +3 more)",
    "270 has transparent interior hole rows (y=178)",
    "337.5 has transparent interior hole rows (y=154, y=179, y=180, y=181)",
    "090->112.5 diff is a local outlier (845 pixels vs neighbor average 568)",
    "337.5->000 diff is a local outlier (1316 pixels vs neighbor average 390)"
  ],
  "alphaHoles": [
    {
      "direction": "045",
      "holes": [
        {
          "row": 152,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 154,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 155,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 157,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 158,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 159,
          "transparentPixels": 33,
          "spanPixels": 110
        }
      ]
    },
    {
      "direction": "090",
      "holes": [
        {
          "row": 152,
          "transparentPixels": 33,
          "spanPixels": 112
        },
        {
          "row": 153,
          "transparentPixels": 33,
          "spanPixels": 112
        },
        {
          "row": 154,
          "transparentPixels": 33,
          "spanPixels": 112
        }
      ]
    },
    {
      "direction": "135",
      "holes": [
        {
          "row": 152,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 153,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 154,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 155,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 156,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 175,
          "transparentPixels": 33,
          "spanPixels": 110
        },
        {
          "row": 177,
          "transparentPixels": 33,
          "spanPixels": 110
        }
      ]
    },
    {
      "direction": "270",
      "holes": [
        {
          "row": 178,
          "transparentPixels": 33,
          "spanPixels": 112
        }
      ]
    },
    {
      "direction": "337.5",
      "holes": [
        {
          "row": 154,
          "transparentPixels": 33,
          "spanPixels": 111
        },
        {
          "row": 179,
          "transparentPixels": 33,
          "spanPixels": 112
        },
        {
          "row": 180,
          "transparentPixels": 33,
          "spanPixels": 112
        },
        {
          "row": 181,
          "transparentPixels": 33,
          "spanPixels": 112
        }
      ]
    }
  ],
  "pairs": [
    {
      "from": "000",
      "to": "022.5",
      "firstPixels": 15386,
      "secondPixels": 15408,
      "diffPixels": 505,
      "centerDelta": 0.0,
      "areaRatio": 1.001429871311582
    },
    {
      "from": "022.5",
      "to": "045",
      "firstPixels": 15408,
      "secondPixels": 15358,
      "diffPixels": 574,
      "centerDelta": 0.0,
      "areaRatio": 1.0032556322437818
    },
    {
      "from": "045",
      "to": "067.5",
      "firstPixels": 15358,
      "secondPixels": 15320,
      "diffPixels": 340,
      "centerDelta": 0.0,
      "areaRatio": 1.0024804177545692
    },
    {
      "from": "067.5",
      "to": "090",
      "firstPixels": 15320,
      "secondPixels": 15644,
      "diffPixels": 795,
      "centerDelta": 0.5,
      "areaRatio": 1.021148825065274
    },
    {
      "from": "090",
      "to": "112.5",
      "firstPixels": 15644,
      "secondPixels": 15386,
      "diffPixels": 845,
      "centerDelta": 0.5,
      "areaRatio": 1.0167684908358248
    },
    {
      "from": "112.5",
      "to": "135",
      "firstPixels": 15386,
      "secondPixels": 15437,
      "diffPixels": 340,
      "centerDelta": 0.0,
      "areaRatio": 1.003314701676849
    },
    {
      "from": "135",
      "to": "157.5",
      "firstPixels": 15437,
      "secondPixels": 15451,
      "diffPixels": 823,
      "centerDelta": 1.0,
      "areaRatio": 1.00090691196476
    },
    {
      "from": "157.5",
      "to": "180",
      "firstPixels": 15451,
      "secondPixels": 15289,
      "diffPixels": 940,
      "centerDelta": 1.4142135623730951,
      "areaRatio": 1.0105958532278108
    },
    {
      "from": "180",
      "to": "202.5",
      "firstPixels": 15289,
      "secondPixels": 15286,
      "diffPixels": 603,
      "centerDelta": 1.0,
      "areaRatio": 1.0001962580138688
    },
    {
      "from": "202.5",
      "to": "225",
      "firstPixels": 15286,
      "secondPixels": 15331,
      "diffPixels": 355,
      "centerDelta": 0.0,
      "areaRatio": 1.0029438702080335
    },
    {
      "from": "225",
      "to": "247.5",
      "firstPixels": 15331,
      "secondPixels": 15293,
      "diffPixels": 499,
      "centerDelta": 0.5,
      "areaRatio": 1.002484796965932
    },
    {
      "from": "247.5",
      "to": "270",
      "firstPixels": 15293,
      "secondPixels": 15331,
      "diffPixels": 649,
      "centerDelta": 0.5,
      "areaRatio": 1.002484796965932
    },
    {
      "from": "270",
      "to": "292.5",
      "firstPixels": 15331,
      "secondPixels": 15225,
      "diffPixels": 1023,
      "centerDelta": 1.0,
      "areaRatio": 1.0069622331691297
    },
    {
      "from": "292.5",
      "to": "315",
      "firstPixels": 15225,
      "secondPixels": 15371,
      "diffPixels": 884,
      "centerDelta": 1.0,
      "areaRatio": 1.0095894909688012
    },
    {
      "from": "315",
      "to": "337.5",
      "firstPixels": 15371,
      "secondPixels": 15414,
      "diffPixels": 275,
      "centerDelta": 0.0,
      "areaRatio": 1.002797475766053
    },
    {
      "from": "337.5",
      "to": "000",
      "firstPixels": 15414,
      "secondPixels": 15386,
      "diffPixels": 1316,
      "centerDelta": 1.4142135623730951,
      "areaRatio": 1.0018198362147406
    }
  ]
}
{
  "ok": true,
  "file": "/Users/oyamahappa/Documents/Agent/Codex/.agent/clawd-pet/final/spritesheet-extended.webp",
  "format": "WEBP",
  "mode": "RGBA",
  "columns": 8,
  "rows": 11,
  "sprite_version_number": 2,
  "width": 1536,
  "height": 2288,
  "transparent_rgb_residue_pixels": 0,
  "errors": [],
  "warnings": [],
  "cells": [
    {
      "state": "idle",
      "row": 0,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 16589,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 17147,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 17297,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 16597,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 16303,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 16364,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 16589,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 7,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 13314,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 13052,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 12729,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 13050,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 13208,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 13129,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 13149,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 13227,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 13297,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 13148,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 12777,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 13108,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 13258,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 13155,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 13198,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 13241,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 16337,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 16699,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 16910,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 16457,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 4,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 5,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 6,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 7,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 16730,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 16619,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 16839,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 16984,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 16843,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 5,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 6,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 7,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 15682,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 15416,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 14590,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 14205,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 12968,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 14473,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 15240,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 15641,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 16832,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 16806,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 16754,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 16802,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 16856,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 16821,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 6,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 7,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 15754,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 15761,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 15842,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 16077,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 15849,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 15668,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 6,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 7,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 16068,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 16274,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 15219,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 15264,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 15959,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 16016,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 6,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 7,
      "used": false,
      "nontransparent_pixels": 0,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 15952,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 15937,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 15910,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 15887,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 16134,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 15904,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 15967,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-000-to-157.5",
      "row": 9,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 15982,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 15863,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 15870,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 15939,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 15819,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 15935,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 15771,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 15992,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "look-180-to-337.5",
      "row": 10,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 16004,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    }
  ]
}

{
  "type": "input_image",
  "image_url": "images/e83619f7a4e91d9400006a2ebcc1f427c2b7b16ff45f9cf9b41f68a9b92dc7e4.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/2f9f9ad2cb5d02c0953267a04f230cfed5053b88a69bd41838d99286dc936bee.png",
  "detail": "high"
}

## tool · 2026-11-07T09:56:07Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"a31ef8","wall_time_seconds":0.000008583,"exit_code":0,"original_token_count":405,"output":"[{\"state\": \"waiting\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [150, 150, 150, 150, 150, 260]}, {\"state\": \"jumping\", \"size\": [192, 208], \"frames\": 5, \"duration_ms\": [140, 140, 140, 140, 280]}, {\"state\": \"running\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [120, 120, 120, 120, 120, 220]}, {\"state\": \"look-loop\", \"size\": [192, 208], \"frames\": 16, \"duration_ms\": [180, 180, 180, 180, 180, 180, 180, 180, 180, 180, 180, 180, 180, 180, 180, 180]}, {\"state\": \"running-left\", \"size\": [192, 208], \"frames\": 8, \"duration_ms\": [120, 120, 120, 120, 120, 120, 120, 220]}, {\"state\": \"waving\", \"size\": [192, 208], \"frames\": 4, \"duration_ms\": [140, 140, 140, 280]}, {\"state\": \"failed\", \"size\": [192, 208], \"frames\": 8, \"duration_ms\": [140, 140, 140, 140, 140, 140, 140, 240]}, {\"state\": \"review\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [150, 150, 150, 150, 150, 280]}, {\"state\": \"idle\", \"size\": [192, 208], \"frames\": 6, \"duration_ms\": [280, 110, 110, 140, 140, 320]}, {\"state\": \"idle-jump-idle\", \"size\": [192, 208], \"frames\": 17, \"duration_ms\": [150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150]}, {\"state\": \"all-states\", \"size\": [192, 208], \"frames\": 57, \"duration_ms\": [150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150, 150]}, {\"state\": \"running-right\", \"size\": [192, 208], \"frames\": 8, \"duration_ms\": [120, 120, 120, 120, 120, 120, 120, 220]}]\n"}

## tool · 2026-11-07T09:56:19Z


Script completed
Wall time 0.1 seconds
Output:

idle, running-right, running-left
{
  "type": "input_image",
  "image_url": "images/c8f2ab22b53e4d451f473b100e6309b7e5d9a0100041b694c5eeee641653d86d.png",
  "detail": "high"
}
waving, jumping, failed
{
  "type": "input_image",
  "image_url": "images/9831a5ccc2a5bf5226eb0e5e326700e371c6f36ba2ac93dd3a444e1f3a49b956.png",
  "detail": "high"
}
waiting, running, review
{
  "type": "input_image",
  "image_url": "images/1c69a3c26385f2649c376126fae74b86fcc1d4a66629ba6db1b2be9a6cc3b33f.png",
  "detail": "high"
}

## tool · 2026-11-07T09:56:27Z


Script completed
Wall time 0.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/aae3e3837353fc061be0587c9f58c2a05d9ac045bbc6cbbe20a3b194f223c6b0.png",
  "detail": "high"
}

## tool · 2026-11-07T09:56:55Z


Script completed
Wall time 0.2 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/0bbf072169a0bbe7e41834e0f0089bf7e9b9d148271023f84ccb771d8a1b4323.png",
  "detail": "high"
}

## assistant · 2026-11-07T09:57:32Z

{
  "ok": true,
  "qa_note": "九种标准动作身份、风格与尺寸一致，完整无裁剪，未见额外效果或非动作所需的漂浮。行走朝向及交替迈腿正确，jumping 保留真实升空，idle 有变化，running 表现原地工作，review 表现倾身检查。16方向完整，四个正方向清晰，斜向横纵分量正确。alphaHoles 警告对应脚间天然留白；067.5脚根候选像素经放大检查位于外轮廓转角，未形成身体内部破洞。",
  "limits": [
    "查看了最终图集、方向图和九种动作及look-loop的全部GIF解码帧；未观看实时循环播放，播放节奏未作最终判定。",
    "色键与透明残留采用已通过的确定性验证结果，未以目测覆盖该结果。"
  ],
  "warnings": [
    "090→112.5的眼睛纵向位移较邻近步骤明显，但方向连续，未发生身份、身体位置或尺度突变。",
    "337.5与315较接近，337.5→000的眼睛横向回中步幅较大；主象限正确，可作为角度间距略不均匀的小差异接受。"
  ],
  "directions": [
    {
      "direction": "000",
      "expected": "up",
      "observed": "up",
      "verdict": "pass",
      "reason": "向上特征清晰。",
      "horizontal_evidence": "双眼总体居中，无明显左右偏移。",
      "vertical_evidence": "双眼明确位于面部上方，高于neutral。"
    },
    {
      "direction": "022.5",
      "expected": "up-right",
      "observed": "up-right",
      "verdict": "pass",
      "reason": "具有向上和向右两个分量。",
      "horizontal_evidence": "双眼相对000向屏幕右侧偏移。",
      "vertical_evidence": "双眼维持面部高位。"
    },
    {
      "direction": "045",
      "expected": "up-right",
      "observed": "up-right",
      "verdict": "pass",
      "reason": "右上象限清晰。",
      "horizontal_evidence": "双眼明显处于面部右半部。",
      "vertical_evidence": "双眼位于面部上半部。"
    },
    {
      "direction": "067.5",
      "expected": "up-right",
      "observed": "up-right",
      "verdict": "pass",
      "reason": "向右分量较强，仍保留向上分量。",
      "horizontal_evidence": "双眼靠近右侧轮廓。",
      "vertical_evidence": "双眼高于090，尚未回到水平中位。"
    },
    {
      "direction": "090",
      "expected": "right",
      "observed": "right",
      "verdict": "pass",
      "reason": "正右方向清晰。",
      "horizontal_evidence": "双眼明显靠右。",
      "vertical_evidence": "双眼位于面部纵向中部，介于上下斜向之间。"
    },
    {
      "direction": "112.5",
      "expected": "down-right",
      "observed": "down-right",
      "verdict": "pass",
      "reason": "右下象限正确。",
      "horizontal_evidence": "双眼保持右侧偏移。",
      "vertical_evidence": "双眼低于090，位于面部下半部。"
    },
    {
      "direction": "135",
      "expected": "down-right",
      "observed": "down-right",
      "verdict": "pass",
      "reason": "具有明确的右下分量。",
      "horizontal_evidence": "双眼位于面部右半部。",
      "vertical_evidence": "双眼明显低于neutral及090。"
    },
    {
      "direction": "157.5",
      "expected": "down-right",
      "observed": "down-right",
      "verdict": "pass",
      "reason": "主象限正确，向下程度增加。",
      "horizontal_evidence": "双眼仍处于中心右侧。",
      "vertical_evidence": "双眼接近面部底缘，低于135。"
    },
    {
      "direction": "180",
      "expected": "down",
      "observed": "down",
      "verdict": "pass",
      "reason": "正下方向清晰。",
      "horizontal_evidence": "双眼回到面部中央附近。",
      "vertical_evidence": "双眼明确处于最低一组位置。"
    },
    {
      "direction": "202.5",
      "expected": "down-left",
      "observed": "down-left",
      "verdict": "pass",
      "reason": "左下象限正确。",
      "horizontal_evidence": "双眼相对180向左偏移。",
      "vertical_evidence": "双眼保持面部低位。"
    },
    {
      "direction": "225",
      "expected": "down-left",
      "observed": "down-left",
      "verdict": "pass",
      "reason": "横纵分量均可辨认。",
      "horizontal_evidence": "双眼明显位于面部左半部。",
      "vertical_evidence": "双眼低于270及neutral。"
    },
    {
      "direction": "247.5",
      "expected": "down-left",
      "observed": "down-left",
      "verdict": "pass",
      "reason": "向左分量较强，仍保留向下分量。",
      "horizontal_evidence": "双眼进一步靠近左侧。",
      "vertical_evidence": "双眼仍低于270。"
    },
    {
      "direction": "270",
      "expected": "left",
      "observed": "left",
      "verdict": "pass",
      "reason": "正左方向清晰。",
      "horizontal_evidence": "双眼明确靠左。",
      "vertical_evidence": "双眼回到纵向中部，介于上下斜向之间。"
    },
    {
      "direction": "292.5",
      "expected": "up-left",
      "observed": "up-left",
      "verdict": "pass",
      "reason": "左上象限正确。",
      "horizontal_evidence": "双眼保持明显左侧偏移。",
      "vertical_evidence": "双眼高于270，位于面部上半部。"
    },
    {
      "direction": "315",
      "expected": "up-left",
      "observed": "up-left",
      "verdict": "pass",
      "reason": "左上两个分量清晰。",
      "horizontal_evidence": "双眼位于面部左半部。",
      "vertical_evidence": "双眼接近面部上缘。"
    },
    {
      "direction": "337.5",
      "expected": "up-left",
      "observed": "up-left",
      "verdict": "pass",
      "reason": "主象限正确，与315区别较小。",
      "horizontal_evidence": "双眼仍明显偏左，未出现反向。",
      "vertical_evidence": "双眼保持高位，与000的向上分量衔接。"
    }
  ]
}
