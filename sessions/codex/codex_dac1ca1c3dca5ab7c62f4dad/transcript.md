# 01a1d7c4-c7da-7b61-9648-07ba9d6b5020

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-14T01:56:05Z

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



## developer · 2026-11-14T01:56:05Z

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
- When the user asks to create, fork, inspect, continue, hand off, pin, archive, unarchive, permanently delete, rename, or otherwise manage Codex threads, search for the relevant thread tool first: `create_thread`, `fork_thread`, `list_threads`, `list_archived_threads`, `read_thread`, `wait_threads`, `send_message_to_thread`, `handoff_thread`, `set_thread_pinned`, `set_thread_archived`, `delete_thread`, or `set_thread_title`.
- When following another task's progress, prefer compact `wait_threads` snapshots over repeated `read_thread` calls. Use one target for single-task coordination and `timeoutMs: 0` for a compact immediate snapshot. `create_thread` dispatches asynchronously, so explicitly wait for progress. Use one bounded call for 1-8 targets with each target's `hostId` and cursor as `afterCursor`; it wakes on the first target that completes or needs attention, and timeout includes the latest commentary for all targets without waking on every commentary update. An up-to-date cursor suppresses already-delivered final text. Separate waits from one task may run serially. Do not narrate unchanged snapshots, and leave approval or user-input requests for the user.
- Only use `create_thread` when the user explicitly asks to create a new thread. Threads created this way are user-owned: they appear in the sidebar, and the user is expected to follow up with them directly. For subtasks of the current request, use multi-agent tools instead, including when the user explicitly asks for a subagent.
- After a successful `create_thread` call, emit `::created-thread{threadId="..."}` for a created thread or `::created-thread{clientThreadId="..."}` for queued worktree setup on its own line in your final response.

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
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Googl (file: r21/documents/26.1112.11217/skills/documents/SKILL.md)
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
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r21/pdf/26.1112.11217/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r17/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves  (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what br (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r23/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across fiv (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r21/presentations/26.1112.11217/skills/presentations/SKILL.md)
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
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r21/template-creator/26.1112.11217/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Codin (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conv (file: r17/visualize/1.0.103/skills/visualize/SKILL.md)
- wizard: Generate an interactive bash wizard that walks a human through (file: r0/wizard/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an anima (file: r20/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in Cha (file: r20/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in C (file: r20/update-pet/SKILL.md)
- writing-for-agents: Writing documents for agents. Use when creating or editing ski (file: r0/writing-for-agents/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is enabled.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/11/13/01a1d539-370b-75a0-87b0-e1683efd760a`, `/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-11-14T01:56:05Z

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

## developer · 2026-11-14T01:56:05Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-14T01:56:05Z

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
  <current_date>2026-11-14</current_date>
  <timezone>Asia/Taipei</timezone>
  <filesystem><workspace_roots><root>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/11/13/01a1d539-370b-75a0-87b0-e1683efd760a</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.git</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.agents</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.codex</path></entry><entry access="read"><path>/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-11-14T01:56:05Z

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


## developer · 2026-11-14T01:56:05Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__pubmed
</tools>

## tool · 2026-11-14T01:56:09Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"4a374a","wall_time_seconds":0.000012375,"exit_code":0,"original_token_count":1660,"output":"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank\n     998 .question-bank-work/lilin-ipad-integrals.txt\n@@ 1466 3.2\n遇到分段的被积函数，先看分段点是否会使面积突然跳跃。对 $0<x<1$，直接积分得 $g(x)=\\frac{x^3}{6}+\\frac x2$。对 $1\\leq x<2$，将积分在 $1$ 处分开：\n\\[\ng(x)=\\int_0^1 f(u)\\,du+\\int_1^x\\frac{u-1}{3}\\,du=\\frac23+\\frac{(x-1)^2}{6}.\n\\]\n第一个式子在 $x\\to1^-$ 时趋于 $\\frac23$，第二个式子给出 $g(1)=\\frac23$ 且右极限相同。因此 $g$ 在整个区间连续，选 \\textbf{D}。$f$ 在 $1$ 处跳变只影响 $g$ 的斜率，积分累积的面积依然连续。\n@@ 1480 3.2\n先分开判断连续性和奇偶性。第一类间断意味着 $0$ 的左右极限有限。结合其余各点连续，$f$ 在每个有限闭区间有界且可积。因此对附近的 $x,y$，取共同上界 $|f|\\le M$，有 $|g(y)-g(x)|=|\\int_x^y f(t)\\,dt|\\le M|y-x|$，得到 $g$ 连续。\n\n判断奇偶性就将 $-x$ 代入。令 $t=-u$，$dt=-du$，同时利用 $f(-u)=-f(u)$，\n\\[\ng(-x)=-\\int_0^x f(-u)\\,du=\\int_0^x f(u)\\,du=g(x).\n\\]\n因此 $g$ 是连续的偶函数，选 \\textbf{B}。\n@@ 1492 3.2\n题目给的是 $f'$ 在 $e^x$ 处的值。要找 $f'(u)$，先把 $e^x$ 整体看成新变量 $u$，于是 $u>0$、$x=\\ln u$、$e^{-x}=\\frac1u$。这给出 $f'(u)=\\frac{\\ln u}{u}$。分子 $\\ln u$ 的导数恰是 $\\frac1u$，因此\n\\[\nf(u)=\\frac12(\\ln u)^2+C.\n\\]\n代入 $f(1)=0$，由 $\\ln1=0$ 得 $C=0$。填 $\\frac12(\\ln x)^2$，适用 $x>0$。将 $e^x$ 代回导数，可恢复 $x e^{-x}$。\n@@ 1496 3.3\n设 $F(t)=\\frac{\\sin t}{t}$，则 $F'(t)=f(t)$。看到 $f(ax)$ 时，想到将 $F$ 中的自变量换成 $ax$。链式法则给出 $\\frac{d}{dx}F(ax)=a f(ax)$，因此要乘 $\\frac1{a^2}$ 才会得到题目的 $\\frac{f(ax)}a$。所以\n\\[\n\\int \\frac{f(ax)}a\\,dx=\\frac{1}{a^2}F(ax)+C=\\frac{\\sin ax}{a^3x}+C.\n\\]\n选 \\textbf{A}。外部出现的两个 $a$ 分别来自题目的除数和抵消链式求导，第三个 $a$ 来自 $F(ax)$ 自身的分母。\n@@ 1508 3.2\n\\TextCorrection{将积分写为 $I=\\int \\max\\{x^3,x^2,1\\}\\,dx$，最大值是被积函数。}\n先比较三个数。$x<-1$ 时，$x^2>1$ 且 $x^3<0$。$-1\\le x\\le1$ 时，$x^2\\le1$ 且 $x^3\\le1$。$x>1$ 时，$x^3>x^2>1$。分别对 $x^2,1,x^3$ 积分，然后令三个表达式在连接点取同一个值，才能得到全实轴上的原函数。\n\\[\nI=C+\\begin{cases}\n\\frac{x^3}{3}-\\frac23,&x<-1,\\\\\nx,&-1\\le x\\le1,\\\\\n\\frac{x^4}{4}+\\frac34,&x>1.\n\\end{cases}\n\\]\n两处左右值分别都是 $-1+C,1+C$，两边导数也都为 $1$，所以连接点同样可导。\n@@ 1512 3.3\n分母能分解为 $(x+1)(x^2-x+1)$，其中二次因式配方后恒正。先按因式拆分，乘回分母比较系数可得\n\\[\n\\frac{2x^2-x-1}{x^3+1}=\\frac{2}{3(x+1)}+\\frac{2(2x-1)-3}{3(x^2-x+1)}.\n\\]\n二次式的导数是 $2x-1$，对应对数。剩下的常数分子用配方 $(x-\\frac12)^2+\\frac34$，对应反正切。因此\n\\[\nI=\\frac23\\ln|x+1|+\\frac23\\ln(x^2-x+1)\n-\\frac{2}{\\sqrt3}\\arctan\\frac{2x-1}{\\sqrt3}+C .\n\\]\n在 $x=-1$ 两侧的区间上，积分常数可各自选取。\n@@ 1518 3.3\n每小问先找被积式中可以连同导数一起替换的部分。\n\n(1) $u=1+2\\ln x$ 时 $du=\\frac2x\\,dx$，得到 $\\frac12\\ln|1+2\\ln x|+C$。\n\n(2) 分子分母同乘 $e^{-x}$，令 $u=1+e^{-x}$，则分子 $e^{-x}dx=-du$，得到 $-\\ln(1+e^{-x})+C$。\n\n(3) 写成 $(1+\\tan^2 x)\\sec^2 x\\,dx$，令 $u=\\tan x$，积分 $1+u^2$，得 $\\tan x+\\frac{\\tan^3 x}{3}+C$。\n\n(4) $d(\\sin^2 x)=\\sin 2x\\,dx$。令 $u=\\sin^2 x$ 后积分 $\\frac1{1+u^2}$，得 $\\arctan(\\sin^2 x)+C$。\n\n(5) 看见 $xe^x$ 及其导数的因子 $x+1$，令 $u=xe^x$。原式变为 $\\frac{du}{u(1+u)}$。拆成 $\\frac1u-\\frac1{1+u}$，得 $\\ln\\left|\\frac{xe^x}{1+xe^x}\\right|+C$。\n\n(6) $d(\\ln\\tan x)=\\frac{2}{\\sin 2x}\\,dx$，故结果是 $\\frac14(\\ln\\tan x)^2+C$。各式在原被积函数有定义的区间上使用。\n@@ 1526 3.3\n(1) 两个根号指数的分母是 $2,3$，取 $u=x^{\\frac16}$ 同时消去。被积式化成 $\\frac{6u^3}{u+1}\\,du$。用多项式除法后结果为 $6[\\frac{u^3}{3}-\\frac{u^2}{2}+u-\\ln(1+u)]+C$。\n\n(2) 令 $u=\\sqrt{1+\\frac1x}$，则 $\\frac{dx}{x}=-\\frac{2u}{u^2-1}\\,du$。原式变为 $-2[1+\\frac1{u^2-1}]\\,du$，拆分两个一次因式，得 $-2u-\\ln\\left|\\frac{u-1}{u+1}\\right|+C$。\n\n(3) 根号内的导数含 $x$，取 $u=\\sqrt{4-x^2}$ 后，$\\frac{dx}{x\\sqrt{4-x^2}}=-\\frac{du}{4-u^2}$，得 $\\frac14\\ln\\left|\\frac{2-u}{2+u}\\right|+C$。\n\n(4) $u=\\sqrt{e^x-1}$，$e^x=1+u^2$ 给出 $\\frac{dx}{u}=\\frac{2du}{1+u^2}$，结果 $2\\arctan u+C$。\n\n(5) 令 $v=x+1$，根号为 $R=\\sqrt{2v^2+3}$，分子为 $v-3$。$dR=\\frac{2v}{R}\\,dv$ 处理第一项。第二项利用 $\\frac{d}{dv}\\ln(\\sqrt2v+R)=\\frac{\\sqrt2}{R}$。相加得 $\\frac R2-\\frac3{\\sqrt2}\\ln(\\sqrt2v+R)+C$。\n@@ 1534 3.3\n(1) 选 $u=x+1$，$dv=e^{3x}dx$。分部积分后 $du=dx$ 降为常数，得到 $\\frac{(x+1)e^{3x}}3-\\frac{e^{3x}}9+C$。\n\n(2) 选 $u=(\\ln x)^2$，$dv=x^{-2}dx$。得到 $-\\frac{(\\ln x)^2}{x}+2\\int\\frac{\\ln x}{x^2}\\,dx$。再用 $u=\\ln x$ 分部一次，结果 $-\\frac{(\\ln x)^2+2\\ln x+2}{x}+C$。\n\n(3) 先令 $t=\\ln x$，原式为 $\\int e^t\\sin t\\,dt$。两次分部后有 $I=e^t\\sin t-e^t\\cos t-I$，所以 $I=\\frac x2[\\sin(\\ln x)-\\cos(\\ln x)]+C$。\n\n(4) 令 $t=\\arcsin x$，得到 $\\int t^2\\cos t\\,dt$。先分部得 $t^2\\sin t-2\\int t\\sin t\\,dt$，再分部得 $t^2\\sin t+2t\\cos t-2\\sin t$。结果为 $x(\\arcsin x)^2+2\\sqrt{1-x^2}\\arcsin x-2x+C$。\n@@ 1542 3.3\n(1) 分子是分母导数，结果 $\\ln|x^2+3x-10|+C$。\n\n(2) 展开得 $(\\tan x+1)^2=\\sec^2 x+2\\tan x$，认出乘积求导，结果 $e^{2x}\\tan x+C$。\n\n(3) 写成 $\\frac12[\\frac1{x^2-\\sqrt2 x+1}+\\frac1{x^2+\\sqrt2 x+1}]$，因为两个分母的乘积为 $x^4+1$。配方后得 $\\frac1{\\sqrt2}[\\arctan(\\sqrt2 x-1)+\\arctan(\\sqrt2 x+1)]+C$。\n\n(4) 分子 $x$ 可以写成 $(1+x)-1$，对应 $\\frac{d}{dx}(\\frac{e^x}{1+x})=\\frac{xe^x}{(1+x)^2}$，故原函数为 $\\frac{e^x}{1+x}+C$。\n\n(5) $\\frac1{1+\\cos x}$ 是 $\\tan\\frac x2$ 的导数，$\\frac{\\sin x}{1+\\cos x}=\\tan\\frac x2$。两项正好拼出乘积导数，结果 $x\\tan\\frac x2+C$。\n\n(6) 原分式是 $\\frac{2}{1+\\sin x-\\cos x}-1$。令 $t=\\tan\\frac x2$，第一项化为 $\\frac{2}{t(t+1)}dt$。拆分后结果 $2\\ln\\left|\\frac{\\sin\\frac x2}{\\sin\\frac x2+\\cos\\frac x2}\\right|-x+C$。\n@@ 1552 3.3\n分母有两个二重因式，原式是偶函数，因此把两处二阶项配成和，把一次项配成差。通分比较分子得\n\\[\n\\frac{2x^2+1}{(x^2-1)^2}\n=\\frac34\\left(\\frac1{(x-1)^2}+\\frac1{(x+1)^2}\\right)\n+\\frac14\\left(\\frac1{x-1}-\\frac1{x+1}\\right).\n\\]\n二阶项积分给出负倒数，一次项积分给出对数。合并得到\n"}

## tool · 2026-11-14T01:56:12Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 17196)
Total output lines: 1

{"chunk_id":"2fde37","wall_time_seconds":0.000010959,"exit_code":0,"original_token_count":16277,"output":"@@ 1466 3.2\n遇到分段的被积函数，先看分段点是否会使面积突然跳跃。对 $0<x<1$，直接积分得 $g(x)=\\frac{x^3}{6}+\\frac x2$。对 $1\\leq x<2$，将积分在 $1$ 处分开：\n\\[\ng(x)=\\int_0^1 f(u)\\,du+\\int_1^x\\frac{u-1}{3}\\,du=\\frac23+\\frac{(x-1)^2}{6}.\n\\]\n第一个式子在 $x\\to1^-$ 时趋于 $\\frac23$，第二个式子给出 $g(1)=\\frac23$ 且右极限相同。因此 $g$ 在整个区间连续，选 \\textbf{D}。$f$ 在 $1$ 处跳变只影响 $g$ 的斜率，积分累积的面积依然连续。\n@@ 1480 3.2\n先分开判断连续性和奇偶性。第一类间断意味着 $0$ 的左右极限有限。结合其余各点连续，$f$ 在每个有限闭区间有界且可积。因此对附近的 $x,y$，取共同上界 $|f|\\le M$，有 $|g(y)-g(x)|=|\\int_x^y f(t)\\,dt|\\le M|y-x|$，得到 $g$ 连续。\n\n判断奇偶性就将 $-x$ 代入。令 $t=-u$，$dt=-du$，同时利用 $f(-u)=-f(u)$，\n\\[\ng(-x)=-\\int_0^x f(-u)\\,du=\\int_0^x f(u)\\,du=g(x).\n\\]\n因此 $g$ 是连续的偶函数，选 \\textbf{B}。\n@@ 1492 3.2\n题目给的是 $f'$ 在 $e^x$ 处的值。要找 $f'(u)$，先把 $e^x$ 整体看成新变量 $u$，于是 $u>0$、$x=\\ln u$、$e^{-x}=\\frac1u$。这给出 $f'(u)=\\frac{\\ln u}{u}$。分子 $\\ln u$ 的导数恰是 $\\frac1u$，因此\n\\[\nf(u)=\\frac12(\\ln u)^2+C.\n\\]\n代入 $f(1)=0$，由 $\\ln1=0$ 得 $C=0$。填 $\\frac12(\\ln x)^2$，适用 $x>0$。将 $e^x$ 代回导数，可恢复 $x e^{-x}$。\n@@ 1496 3.3\n设 $F(t)=\\frac{\\sin t}{t}$，则 $F'(t)=f(t)$。看到 $f(ax)$ 时，想到将 $F$ 中的自变量换成 $ax$。链式法则给出 $\\frac{d}{dx}F(ax)=a f(ax)$，因此要乘 $\\frac1{a^2}$ 才会得到题目的 $\\frac{f(ax)}a$。所以\n\\[\n\\int \\frac{f(ax)}a\\,dx=\\frac{1}{a^2}F(ax)+C=\\frac{\\sin ax}{a^3x}+C.\n\\]\n选 \\textbf{A}。外部出现的两个 $a$ 分别来自题目的除数和抵消链式求导，第三个 $a$ 来自 $F(ax)$ 自身的分母。\n@@ 1508 3.2\n\\TextCorrection{将积分写为 $I=\\int \\max\\{x^3,x^2,1\\}\\,dx$，最大值是被积函数。}\n先比较三个数。$x<-1$ 时，$x^2>1$ 且 $x^3<0$。$-1\\le x\\le1$ 时，$x^2\\le1$ 且 $x^3\\le1$。$x>1$ 时，$x^3>x^2>1$。分别对 $x^2,1,x^3$ 积分，然后令三个表达式在连接点取同一个值，才能得到全实轴上的原函数。\n\\[\nI=C+\\begin{cases}\n\\frac{x^3}{3}-\\frac23,&x<-1,\\\\\nx,&-1\\le x\\le1,\\\\\n\\frac{x^4}{4}+\\frac34,&x>1.\n\\end{cases}\n\\]\n两处左右值分别都是 $-1+C,1+C$，两边导数也都为 $1$，所以连接点同样可导。\n@@ 1512 3.3\n分母能分解为 $(x+1)(x^2-x+1)$，其中二次因式配方后恒正。先按因式拆分，乘回分母比较系数可得\n\\[\n\\frac{2x^2-x-1}{x^3+1}=\\frac{2}{3(x+1)}+\\frac{2(2x-1)-3}{3(x^2-x+1)}.\n\\]\n二次式的导数是 $2x-1$，对应对数。剩下的常数分子用配方 $(x-\\frac12)^2+\\frac34$，对应反正切。因此\n\\[\nI=\\frac23\\ln|x+1|+\\frac23\\ln(x^2-x+1)\n-\\frac{2}{\\sqrt3}\\arctan\\frac{2x-1}{\\sqrt3}+C .\n\\]\n在 $x=-1$ 两侧的区间上，积分常数可各自选取。\n@@ 1518 3.3\n每小问先找被积式中可以连同导数一起替换的部分。\n\n(1) $u=1+2\\ln x$ 时 $du=\\frac2x\\,dx$，得到 $\\frac12\\ln|1+2\\ln x|+C$。\n\n(2) 分子分母同乘 $e^{-x}$，令 $u=1+e^{-x}$，则分子 $e^{-x}dx=-du$，得到 $-\\ln(1+e^{-x})+C$。\n\n(3) 写成 $(1+\\tan^2 x)\\sec^2 x\\,dx$，令 $u=\\tan x$，积分 $1+u^2$，得 $\\tan x+\\frac{\\tan^3 x}{3}+C$。\n\n(4) $d(\\sin^2 x)=\\sin 2x\\,dx$。令 $u=\\sin^2 x$ 后积分 $\\frac1{1+u^2}$，得 $\\arctan(\\sin^2 x)+C$。\n\n(5) 看见 $xe^x$ 及其导数的因子 $x+1$，令 $u=xe^x$。原式变为 $\\frac{du}{u(1+u)}$。拆成 $\\frac1u-\\frac1{1+u}$，得 $\\ln\\left|\\frac{xe^x}{1+xe^x}\\right|+C$。\n\n(6) $d(\\ln\\tan x)=\\frac{2}{\\sin 2x}\\,dx$，故结果是 $\\frac14(\\ln\\tan x)^2+C$。各式在原被积函数有定义的区间上使用。\n@@ 1526 3.3\n(1) 两个根号指数的分母是 $2,3$，取 $u=x^{\\frac16}$ 同时消去。被积式化成 $\\frac{6u^3}{u+1}\\,du$。用多项式除法后结果为 $6[\\frac{u^3}{3}-\\frac{u^2}{2}+u-\\ln(1+u)]+C$。\n\n(2) 令 $u=\\sqrt{1+\\frac1x}$，则 $\\frac{dx}{x}=-\\frac{2u}{u^2-1}\\,du$。原式变为 $-2[1+\\frac1{u^2-1}]\\,du$，拆分两个一次因式，得 $-2u-\\ln\\left|\\frac{u-1}{u+1}\\right|+C$。\n\n(3) 根号内的导数含 $x$，取 $u=\\sqrt{4-x^2}$ 后，$\\frac{dx}{x\\sqrt{4-x^2}}=-\\frac{du}{4-u^2}$，得 $\\frac14\\ln\\left|\\frac{2-u}{2+u}\\right|+C$。\n\n(4) $u=\\sqrt{e^x-1}$，$e^x=1+u^2$ 给出 $\\frac{dx}{u}=\\frac{2du}{1+u^2}$，结果 $2\\arctan u+C$。\n\n(5) 令 $v=x+1$，根号为 $R=\\sqrt{2v^2+3}$，分子为 $v-3$。$dR=\\frac{2v}{R}\\,dv$ 处理第一项。第二项利用 $\\frac{d}{dv}\\ln(\\sqrt2v+R)=\\frac{\\sqrt2}{R}$。相加得 $\\frac R2-\\frac3{\\sqrt2}\\ln(\\sqrt2v+R)+C$。\n@@ 1534 3.3\n(1) 选 $u=x+1$，$dv=e^{3x}dx$。分部积分后 $du=dx$ 降为常数，得到 $\\frac{(x+1)e^{3x}}3-\\frac{e^{3x}}9+C$。\n\n(2) 选 $u=(\\ln x)^2$，$dv=x^{-2}dx$。得到 $-\\frac{(\\ln x)^2}{x}+2\\int\\frac{\\ln x}{x^2}\\,dx$。再用 $u=\\ln x$ 分部一次，结果 $-\\frac{(\\ln x)^2+2\\ln x+2}{x}+C$。\n\n(3) 先令 $t=\\ln x$，原式为 $\\int e^t\\sin t\\,dt$。两次分部后有 $I=e^t\\sin t-e^t\\cos t-I$，所以 $I=\\frac x2[\\sin(\\ln x)-\\cos(\\ln x)]+C$。\n\n(4) 令 $t=\\arcsin x$，得到 $\\int t^2\\cos t\\,dt$。先分部得 $t^2\\sin t-2\\int t\\sin t\\,dt$，再分部得 $t^2\\sin t+2t\\cos t-2\\sin t$。结果为 $x(\\arcsin x)^2+2\\sqrt{1-x^2}\\arcsin x-2x+C$。\n@@ 1542 3.3\n(1) 分子是分母导数，结果 $\\ln|x^2+3x-10|+C$。\n\n(2) 展开得 $(\\tan x+1)^2=\\sec^2 x+2\\tan x$，认出乘积求导，结果 $e^{2x}\\tan x+C$。\n\n(3) 写成 $\\frac12[\\frac1{x^2-\\sqrt2 x+1}+\\frac1{x^2+\\sqrt2 x+1}]$，因为两个分母的乘积为 $x^4+1$。配方后得 $\\frac1{\\sqrt2}[\\arctan(\\sqrt2 x-1)+\\arctan(\\sqrt2 x+1)]+C$。\n\n(4) 分子 $x$ 可以写成 $(1+x)-1$，对应 $\\frac{d}{dx}(\\frac{e^x}{1+x})=\\frac{xe^x}{(1+x)^2}$，故原函数为 $\\frac{e^x}{1+x}+C$。\n\n(5) $\\frac1{1+\\cos x}$ 是 $\\tan\\frac x2$ 的导数，$\\frac{\\sin x}{1+\\cos x}=\\tan\\frac x2$。两项正好拼出乘积导数，结果 $x\\tan\\frac x2+C$。\n\n(6) 原分式是 $\\frac{2}{1+\\sin x-\\cos x}-1$。令 $t=\\tan\\frac x2$，第一项化为 $\\frac{2}{t(t+1)}dt$。拆分后结果 $2\\ln\\left|\\frac{\\sin\\frac x2}{\\sin\\frac x2+\\cos\\frac x2}\\right|-x+C$。\n@@ 1552 3.3\n分母有两个二重因式，原式是偶函数，因此把两处二阶项配成和，把一次项配成差。通分比较分子得\n\\[\n\\frac{2x^2+1}{(x^2-1)^2}\n=\\frac34\\left(\\frac1{(x-1)^2}+\\frac1{(x+1)^2}\\right)\n+\\frac14\\left(\\frac1{x-1}-\\frac1{x+1}\\right).\n\\]\n二阶项积分给出负倒数，一次项积分给出对数。合并得到\n\\[\nI=-\\frac{3x}{2(x^2-1)}+\\frac14\\ln\\left|\\frac{x-1}{x+1}\\right|+C .\n\\]\n检查时先将第一项拆回两个倒数，再分别求导即可恢复上式。\n@@ 1556 3.3\n分子次数高于分母，先做除法，得 $x-\\frac{x}{x^3+1}$。接着把分母分为 $(x+1)q$，其中 $q=x^2-x+1$。通分核对可得\n\\[\n\\frac{x}{x^3+1}=-\\frac1{3(x+1)}+\\frac{2x-1}{6q}+\\frac1{2q}.\n\\]\n三项依次用一次式积分、$q'/q$ 型积分和二次式配方积分。留意原式对整个余项取负，最终\n\\[\nI=\\frac{x^2}{2}+\\frac13\\ln|x+1|-\\frac16\\ln q\n-\\frac1{\\sqrt3}\\arctan\\frac{2x-1}{\\sqrt3}+C.\n\\]\n@@ 1560 3.3\n反函数看起来不容易直接积分。把 $x=f(t)$，那么 $f^{-1}(x)=t$，换元后 $\\int f^{-1}(x)\\,dx=\\int t f'(t)\\,dt$。这个乘积适合分部积分，让 $t$ 求导、$f'(t)$ 积分，于是\n\\[\n\\int t f'(t)\\,dt=t f(t)-F(t)+C.\n\\]\n将 $t$ 换回去，答案为 $x f^{-1}(x)-F(f^{-1}(x))+C$。即便反函数在某点不可导，该式仍是原函数。设 $t_0=f^{-1}(x_0)$，其增量减去 $t_0(x-x_0)$ 等于 $\\int_{t_0}^t[f(t)-f(s)]\\,ds$，绝对值至多为 $|t-t_0||x-x_0|$。除以 $|x-x_0|$ 后趋于零。\n@@ 1565 3.3\n看到 $fF$ 且 $f=F'$，应想到 $\\frac{d}{dx}(F^2)=2FF'$，所以 $(F^2)'=\\frac{xe^x}{(1+x)^2}$。右式正好是 $\\frac{e^x}{1+x}$ 的导数，因为商求导后分子是 $e^x(1+x)-e^x=xe^x$。积分得到\n\\[\nF(x)^2=\\frac{e^x}{1+x}+C.\n\\]\n代入 $F(0)=1$ 得 $C=0$。由 $F>0$ 取正平方根，即 $F=e^{\\frac x2}(1+x)^{-\\frac12}$。再求导得到\n\\[\nf(x)=\\frac{x e^{\\frac x2}}{2(1+x)^{\\frac32}},\\qquad x\\ge0.\n\\]\n两式相乘可恢复题给的乘积。\n@@ 1569 3.3\n目标里有 $f'$，条件只给 $F$。通过两次分部，把 $f'$ 积成 $f$ 再积成 $F$，同时多项式每次降一次：\n\\[\nI=x^3f(x)-3\\int x^2 f(x)\\,dx\n=x^3f(x)-3x^2F(x)+6\\int xF(x)\\,dx.\n\\]\n最后一项因 $xF(x)=\\sin x$ 变得容易，且 $f=F'=\\frac{x\\cos x-\\sin x}{x^2}$。所以\n\\[\nI=x^2\\cos x-4x\\sin x-6\\cos x+C.\n\\]\n若将 $F$ 按极限连续延拓至 $0$，这个原函数也可以在 $0$ 处使用。\n@@ 1573 3.2\n不定积分等式说明右边是左边被积函数的原函数，先对 $x$ 求导得 $f'(x^3)=3x^2$。这一步直接对原函数求导，无需对 $f'(x^3)$ 再求导。立方函数可以取任意实数，因此令 $t=x^3$，得到 $f'(t)=3(\\sqrt[3]t)^2$。\n\n由于 $\\frac{d}{dt}(\\sqrt[3]t)^5=\\frac53(\\sqrt[3]t)^2$，积分后\n\\[\nf(x)=\\frac95(\\sqrt[3]x)^5+C_1.\n\\]\n在 $x=0$，用差商可验证导数为 $0$，和题给关系一致。\n@@ 1577 3.2\n令 $t=\\ln x$。当 $0<x\\le1$ 时 $t\\le0$，$f'(t)=1$；当 $x>1$ 时 $t>0$，$f'(t)=e^t$。因此分别得到 $t+C_1$ 和 $e^t+C_2$。$f$ 在 $t=0$ 可导，必须连续，所以 $C_1=1+C_2$。令 $C=C_1$，还原变量后得\n\\[\nf(\\ln x)=\\begin{cases}\n\\ln x+C,&0<x\\le1,\\\\\nx-1+C,&x>1.\n\\end{cases}\n\\]\n在连接点，两侧关于 $t$ 的导数都等于 $1$，也符合条件。\n@@ 1583 3.3\n(I) 配方 $x(4-x)=4-(x-2)^2$，用反正弦原函数，得 $\\arcsin\\frac{x-2}{2}+C$。\n\n(II) 指数 $x+\\frac1x$ 的导数就是前面的括号，故为 $e^{x+\\frac1x}+C$。\n\n(III) 配方 $x(x+2)=(x+1)^2-1$。令 $u=x+1$，$\\ln|u+\\sqrt{u^2-1}|$ 的导数为 $\\frac1{\\sqrt{u^2-1}}$。故结果 $\\ln|x+1+\\sqrt{x(x+2)}|+C$。\n\n(IV) $u=1+x^3$，$x^5dx=\\frac{u-1}{3}du$，积分两项幂函数，得 $\\frac{u^{\\frac53}}5-\\frac{u^{\\frac23}}2+C$，分数次幂按实立方根理解。\n\n(V) $u=\\sqrt{\\sin x}$ 后化成 $\\frac{2du}{1-u^4}=[\\frac1{1-u^2}+\\frac1{1+u^2}]du$，故为 $\\frac12\\ln|\\frac{1+u}{1-u}|+\\arctan u+C$。\n\n(VI) $u=e^x$ 可约掉一个 $e^x$，得到 $\\frac{u^2+1}{u^4+1}du$。分母分解成 $(u^2-\\sqrt2u+1)(u^2+\\sqrt2u+1)$，分式等于两个因式倒数之和的一半。配方后得 $\\frac1{\\sqrt2}[\\arctan(\\sqrt2u-1)+\\arctan(\\sqrt2u+1)]+C$。\n@@ 1588 3.3\n(I) 令 $u=\\arctan\\sqrt x$，则 $du=\\frac{dx}{2(1+x)\\sqrt x}$。原式是 $2u\\,du$，得 $(\\arctan\\sqrt x)^2+C$。\n\n(II) 令 $x=2\\sin t$、$t=\\arcsin\\frac x2$，得到 $16\\sin^2t\\cos^2t\\,dt=2(1-\\cos4t)\\,dt$，结果为 $2t-\\frac12\\sin4t+C$。\n\n(III) 分子拆成 $(2x+2)-1$，第一项是分母导数，第二项把分母配成 $(x+1)^2+4$。结果 $\\ln(x^2+2x+5)-\\frac12\\arctan\\frac{x+1}{2}+C$。\n\n(IV) 令 $u=\\sqrt{4+x^2}$，则 $du=\\frac{x}{u}dx$，余下的 $x^2=u^2-4$。积分得 $\\frac{u^3}{3}-4u+C$。\n\n(V) 根号取作新变量 $u=\\sqrt{\\frac{1-x}{1+x}}$，解出 $x=\\frac{1-u^2}{1+u^2}$。原式化为 $-\\frac{4u^2}{(1-u^2)^2}du$。把它写成 $-2[\\frac{d}{du}(\\frac{u}{1-u^2})-\\frac1{1-u^2}]du$，积分得 $-\\frac{2u}{1-u^2}+\\ln|\\frac{1+u}{1-u}|+C$。\n@@ 1595 3.3\n(I) 先把分式拆成 $1-\\frac1{1+\\sin x}$。注意对 $\\frac{\\cos x}{1+\\sin x}$ 用商求导时，分子化成 $-\\sin x(1+\\sin x)-\\cos^2 x=-(1+\\sin x)$。因此答案为 $x+\\frac{\\cos x}{1+\\sin x}+C$。\n\n(II) 把 $\\tan x$ 写成 $\\frac{\\sin x}{\\cos x}$，原式为 $\\frac{\\cos x}{\\cos x+2\\sin x}dx$。分母的导数为 $2\\cos x-\\sin x$，而 $5\\cos x=2(2\\cos x-\\sin x)+(\\cos x+2\\sin x)$。所以\n\\[\nI=\\frac25\\ln|\\cos x+2\\sin x|+\\frac x5+C .\n\\]\n这两个结果分别在原被积函数有定义的区间上成立。\n@@ 1600 3.3\n已知等式右边是 $xf(x)$ 的原函数，先求导得 $xf(x)=\\frac1{\\sqrt{1-x^2}}$。因此在题意可成立的区间 $-1<x<1$、$x\\ne0$ 上，$\\frac1{f(x)}=x\\sqrt{1-x^2}$。\n\n看到根号内的 $1-x^2$，旁边恰好有 $x\\,dx$，令 $u=1-x^2$，得到 $du=-2x\\,dx$，所以\n\\[\nI=-\\frac12\\int\\sqrt u\\,du=-\\frac13(1-x^2)^{\\frac32}+C.\n\\]\n对结果求导，指数带下来的因子与内层导数 $-2x$ 相乘，恢复 $x\\sqrt{1-x^2}$。\n@@ 1604 3.3\n先令 $u=x^2-1$，得到 $f(u)=\\ln\\frac{u+1}{u-1}$。按原等式的实数定义域，$x^2>2$，所以 $u>1$。因此\n\\[\n\\ln\\frac{\\varphi(x)+1}{\\varphi(x)-1}=\\ln x\n\\ \\Longrightarrow\\ \\varphi(x)+1=x(\\varphi(x)-1).\n\\]\n解出 $\\varphi(x)=\\frac{x+1}{x-1}=1+\\frac2{x-1}$。这一解满足 $\\varphi(x)>1$ 当且仅当 $x>1$。因此 $I=x+2\\ln(x-1)+C$。这里先解出 $\\varphi$，才能确定该积什么函数以及对数在哪个区间有意义。\n@@ 1608 3.3\n把等式中的 $\\ln x$ 看成新变量 $u$，得到 $f(u)=e^{-u}\\ln(1+e^u)$。积分时令 $t=e^u$，便得到 $\\int\\frac{\\ln(1+t)}{t^2}\\,dt$。对数求导后变成简单分式，适合分部：\n\\[\n-\\frac{\\ln(1+t)}t+\\int\\frac{dt}{t(1+t)}\n=-\\frac{\\ln(1+t)}t+\\ln t-\\ln(1+t)+C .\n\\]\n最后把 $t=e^x$ 代回，得 $x-(1+e^{-x})\\ln(1+e^x)+C$。求导时来自最后两个因子的常数项抵消，剩下 $e^{-x}\\ln(1+e^x)$。\n@@ 1612 3.3\n(I) 试设原函数为 $e^x R(x)$。取 $R(x)=\\frac{x-2}{x+2}$，则 $R+R'=\\frac{x^2}{(x+2)^2}$。故为 $\\frac{(x-2)e^x}{x+2}+C$。\n\n(II) 取 $u=\\ln x$、$dv=\\frac{dx}{(1-x)^2}$，得到 $\\frac{\\ln x}{1-x}-\\int\\frac{dx}{x(1-x)}$。拆分后为 $\\frac{\\ln x}{1-x}-\\ln x+\\ln|1-x|+C$。\n\n(III) 令 $t=\\sqrt{1+e^x}$，此时 $\\frac{e^x}{\\sqrt{1+e^x}}dx=2dt$。分部得 $2xt-2\\int t\\,dx$，再用 $dx=\\frac{2t}{t^2-1}dt$，结果 $2xt-4t-2\\ln|\\frac{t-1}{t+1}|+C$。\n\n(IV) 拆出 $\\frac1{x^2(1+x^2)}=\\frac1{x^2}-\\frac1{1+x^2}$。前一项对 $\\arctan x$ 分部，后一项直接换元。结果 $-\\frac{\\arctan x}{x}-\\frac12(\\arctan x)^2+\\ln|x|-\\frac12\\ln(1+x^2)+C$。\n\n(V) 取 $u=\\arctan\\sqrt x$、$dv=dx$。分部后剩下 $\\int\\frac{\\sqrt x}{2(1+x)}dx$，用 $t=\\sqrt x$ 化成 $\\int(1-\\frac1{1+t^2})dt$，故为 $(x+1)\\arctan\\sqrt x-\\sqrt x+C$。\n\n(VI) 令 $t=\\sqrt{e^x-1}$，得到 $\\int2t(1+t^2)\\arctan t\\,dt$。用 $u=\\arctan t$、$v=\\frac12(1+t^2)^2$ 分部，结果 $\\frac12(1+t^2)^2\\arctan t-\\frac t2-\\frac{t^3}{6}+C$。\n@@ 1619 3.2\n绝对值在 $x=0$ 改变写法。$x<0$ 时 $e^{-|x|}=e^x$，原函数是 $e^x+C_1$；$x>0$ 时 $e^{-|x|}=e^{-x}$，原函数是 $-e^{-x}+C_2$。要在全实轴得到可导的原函数，两边必须在 $0$ 连续。因此 $1+C_1=-1+C_2$。用公共的函数值 $C$ 表示，\n\\[\nI=C+\\begin{cases}e^x-1,&x<0,\\\\1-e^{-x},&x\\ge0.\\end{cases}\n\\]\n两侧导数在 $0$ 均趋于 $1$，而且连接处的差商也趋于 $1$，正好等于被积函数在 $0$ 的值。\n@@ 1623 3.3\n分母是 $x-1$ 的高次幂，直接令 $u=x-1$，使分子也用 $u$ 表示。$x^2=(u+1)^2=u^2+2u+1$，除以 $u^{100}$ 后得到 $u^{-98}+2u^{-99}+u^{-100}$。逐项使用幂函数积分公式，\n\\[\nI=-\\frac1{97(x-1)^{97}}-\\frac1{49(x-1)^{98}}-\\frac1{99(x-1)^{99}}+C.\n\\]\n三项求导后分子分别是 $1,2,1$，通分恢复 $(u+1)^2$。$x=1$ 两侧的常数可分别选取。\n@@ 1629 3.3\n积分区间以 $0$ 为中心，因此可以把每个 $x$ 和它的对称点 $-x$ 配成一对。具体地，设 $t=-x$，则 $dx=-dt$。$x$ 从 $-a$ 到 $a$ 时，$t$ 从 $a$ 到 $-a$，所以\n\\[\n\\int_{-a}^{a}f(-x)\\,dx=-\\int_a^{-a}f(t)\\,dt=\\int_{-a}^a f(t)\\,dt.\n\\]\n将原积分与这份同值的积分相加，左边变成原积分的两倍。利用积分的线性，再除以 $2$，便得所证。特别地，如果 $f$ 是奇函数，被加起来的两项处处相消。\n@@ 1636 3.1\n积分区间长为 $\\frac\\pi4$。如果能找出被积函数的最大、最小值，再乘区间长度，就能得到上下界。设 $h(x)=\\frac{\\sin x}{x}$，求导得\n\\[\nh'(x)=\\frac{x\\cos x-\\sin x}{x^2}.\n\\]\n令 $u(x)=x\\cos x-\\sin x$，有 $u(0)=0$ 且 $u'(x)=-x\\sin x<0$，因此 $h'<0$。两个端点值分别为 $\\frac{2\\sqrt2}{\\pi}$ 与 $\\frac2\\pi$。内部各点严格介于二者之间，乘区间长度 $\\frac\\pi4$ 即得 $\\frac12<I<\\frac{\\sqrt2}{2}$。\n@@ 1640 3.3\n(1) 对 $|x|>1$，$\\ln|x+\\sqrt{x^2-1}|$ 的导数是 $\\frac1{\\sqrt{x^2-1}}$。两端代入得 $\\ln(\\frac{\\sqrt2-1}{2-\\sqrt3})=\\ln[(\\sqrt2-1)(2+\\sqrt3)]$。\n\n(2) 令 $u=x-1$，根号变成 $\\sqrt{1-u^2}$，另一个因子变成 $\\frac32+\\frac u2$。奇函数项在 $[-1,1]$ 上积分为零，余下 $\\frac32$ 倍单位上半圆面积，得 $\\frac{3\\pi}4$。\n\n(3) 令 $t=\\arcsin x$ 消去根号，积分变为 $\\int_0^{\\frac\\pi2}t\\sin^2t\\,dt$。用 $\\sin^2t=\\frac{1-\\cos2t}2$，再分部算出 $\\int_0^{\\frac\\pi2}t\\cos2t\\,dt=-\\frac12$，所以答案 $\\frac{\\pi^2}{16}+\\frac14$。换元可先在 $x<1$ 的截断区间进行，再取上限趋于 $1$。\n\n(4) 令 $t=\\sqrt x$。因为 $\\sin(\\arctan t)=\\frac{t}{\\sqrt{1+t^2}}$，原反正弦等于 $\\arctan t$。分部得 $\\left[t^2\\arctan t-t+\\arctan t\\right]_0^{\\sqrt3}=\\frac{4\\pi}3-\\sqrt3$。\n@@ 1648 3.3\n两被积函数只把正弦和余弦互换，而 $x\\mapsto\\frac\\pi2-x$ 正好能作这个交换，积分区间仍相同。故两个积分相等，设共同值为 $I$。\n\n将两式相加，分子变成 $\\sin^3x+\\cos^3x$。利用立方和分解，恰好消掉分母：\n\\[\n2I=\\int_0^{\\frac\\pi2}(1-\\sin x\\cos x)\\,dx\n=\\frac\\pi2-\\frac12.\n\\]\n所以两个积分都等于 $\\frac\\pi4-\\frac14$。整个区间内 $\\sin x+\\cos x>0$，约分有效。\n@@ 1652 3.3\n题目只直接给了 $(0,\\pi)$ 上的 $f$，遇到 $x$ 在后面的区间就用题给递推每次减去 $\\pi$。当 $\\pi<x<2\\pi$，$f(x)=x-\\pi+\\sin x$。当 $2\\pi<x<3\\pi$，再代一次得到\n\\[\nf(x)=x-2\\pi+\\sin(x-\\pi)+\\sin x=x-2\\pi .\n\\]\n有限个端点的取值不改变积分。于是\n\\[\nI=\\int_\\pi^{2\\pi}(x-\\pi+\\sin x)\\,dx+\n\\int_{2\\pi}^{3\\pi}(x-2\\pi)\\,dx\n=\\frac{\\pi^2}2-2+\\frac{\\pi^2}2=\\pi^2-2.\n\\]\n@@ 1656 3.3\n已知 $[0,2]$ 上的积分，所求区间 $[1,3]$ 和它重叠一半。先分开重叠和新增部分，得到\n\\[\n\\int_1^3f(x)\\,dx-\\int_0^2f(x)\\,dx\n=\\int_2^3f(x)\\,dx-\\int_0^1f(x)\\,dx.\n\\]\n在第一项令 $x=t+2$，使两个区间都变为 $[0,1]$。此时题给关系 $f(t+2)-f(t)=t$ 正好能用，差等于 $\\int_0^1t\\,dt=\\frac12$。已知第二个总积分为零，所以所求为 $\\frac12$。\n@@ 1660 3.3\n积分含 $f''$ 而题目给了函数值和切线。想到分部积分，因为可以先把 $f''$ 积成 $f'$，再用端点值消去剩下的积分。切线斜率给出 $f'(2)=5$，过原点给出 $f(0)=0$，曲线上的点给出 $f(2)=4$。\n\\[\nI=[xf'(x)]_0^2-\\int_0^2f'(x)\\,dx\n=2f'(2)-[f(2)-f(0)]=10-4=6.\n\\]\n虽然 $f'(0)$ 没有给出，端点项中它乘以 $0$，因此无需再求。\n@@ 1664 3.3\n\\TextCorrection{按原页平方位于 $(x-1)$ 后的写法，将自变量括号明确为 $f'(x)=\\arcsin((x-1)^2)$。}\n只知道 $f'$ 时，不急着把它积成完整的 $f$。分部时用 $v=x-1$，令上端点 $v(1)=0$，下端点又有 $f(0)=0$，于是\n\\[\nI=\\int_0^1(1-x)f'(x)\\,dx\n=\\int_0^1(1-x)\\arcsin((1-x)^2)\\,dx.\n\\]\n令 $u=(1-x)^2$，因为 $du=-2(1-x)dx$，原积分化为 $\\frac12\\int_0^1\\arcsin u\\,du$。其原函数为 $u\\arcsin u+\\sqrt{1-u^2}$，两端代入得 $\\frac\\pi4-\\frac12$。\n@@ 1668 3.3\n分母 $\\pi-t$ …7196 tokens truncated…)e^{-x}]_0^R\\to1$，收敛。\n\nB 用 $u=x^2$，得到 $\\frac12\\int_0^{R^2}e^{-u}du\\to\\frac12$，收敛。\n\nC 用 $u=\\arctan x$，得到 $\\frac12(\\arctan R)^2\\to\\frac{\\pi^2}{8}$，收敛。\n\nD 的原函数为 $\\frac12\\ln(1+x^2)$，在 $R\\to+\\infty$ 时趋于 $+\\infty$，所以发散，选 \\textbf{D}。前三项不仅有有限极限，还给出了各自的积分值。\n@@ 2012 3.1\n把每项提取 $\\frac1n$，原和式变为 $\\sum_{i=1}^n\\frac1n\\,\\frac{e^{i/n}}{1+e^{2i/n}}$。这对应把 $[0,1]$ 等分成 $n$ 份，每段长度为 $\\frac1n$，取右端点 $\\frac in$ 的 Riemann 和。被积函数连续，所以极限为\n\\[\n\\int_0^1\\frac{e^x}{1+e^{2x}}dx.\n\\]\n令 $u=e^x$，$du=e^x dx$，上下限变为 $1,e$，所得积分为 $\\int_1^e\\frac{du}{1+u^2}=\\arctan e-\\frac\\pi4$。识别步长和取样点后，数列极限就变成定积分计算。\n@@ 2016 3.2\n式子同时在上限和被积函数内含 $x$，直接求导容易多出难处理的项。这里 $x^2-t^2$ 的微分正好含 $t\\,dt$，先令 $u=x^2-t^2$。两端由 $x^2$ 变到 $0$，故\n\\[\n\\int_0^x t f(x^2-t^2)\\,dt\n=-\\frac12\\int_{x^2}^0 f(u)\\,du\n=\\frac12\\int_0^{x^2}f(u)\\,du .\n\\]\n接着用微积分基本定理和链式法则，导数为 $\\frac12 f(x^2)\\cdot2x=x f(x^2)$。这个换元对负 $x$ 也成立，积分方向已由上下限处理。\n@@ 2020 3.2\n让被积函数中的乘积 $xu$ 变成一个变量。对 $x>0$，令 $t=xu$、$dt=x\\,du$，得到\n\\[\ny=\\int_0^{2x}\\sqrt{12-t^2}\\,dt.\n\\]\n原被积函数是实数要求 $0\\le x\\le\\sqrt3$。在内部 $0<x<\\sqrt3$，微积分基本定理给出 $y'=2\\sqrt{12-4x^2}=4\\sqrt{3-x^2}$。\n\n在左端点 $x=0$，原式给出 $y(0)=0$，上面的积分表示也成立，右导数为 $4\\sqrt3$。在右端点 $x=\\sqrt3$，左导数为 $0$。端点应按单侧导数理解，因为实数函数在区间外没有定义。\n@@ 2024 3.2\n求关于 $s$ 的导数时把 $t>0$ 当作固定参数。先令 $u=tx$，则 $du=t\\,dx$，外部的因子 $t$ 正好消去微分的分母，上限 $\\frac st$ 正好变成 $s$。因此\n\\[\nI(s,t)=\\int_0^s f(u)\\,du .\n\\]\n这个表达式已与 $t$ 无关。由 $f$ 连续，微积分基本定理直接给出 $\\frac{dI}{ds}=f(s)$。也可直接用变上限求导，得到 $t f(t\\frac st)\\cdot\\frac1t$，两处 $t$ 相消后相同。\n@@ 2030 3.2\n未知的 $f$ 出现在 $x-t$ 中，先把它的自变量变成积分变量。令 $u=x-t$，得\n\\[\n\\int_0^x t f(x-t)dt\n=\\int_0^x(x-u)f(u)du\n=x\\int_0^x f(u)du-\\int_0^x u f(u)du .\n\\]\n对两边求导时，前一项给出 $\\int_0^x f(u)du+xf(x)$，后一项给出 $xf(x)$，两项恰好抵消，剩下 $\\int_0^x f(u)du=\\sin x$。取 $x=\\frac\\pi2$，便得所求积分为 $1$。若继续求导还可得到 $f(x)=\\cos x$，代回也能核对。\n@@ 2034 3.2\n分子中的 $e^u du$ 是 $e^u$ 的微分。令 $v=e^u-e^{x^2}+1$，上下限变为 $2-e^{x^2},1$。再令 $h=e^{x^2}-1$、$w=1-v$，分子变为 $\\int_0^h f(1-w)dw$。\n\n由 $f(1)=0,f'(1)=2$，有 $f(1-w)=-2w+o(w)$，因此分子为 $-h^2+o(h^2)$。这里误差可在 $0\\le w\\le h$ 上一致估计后积分。由于 $h\\sim x^2$，分子主项为 $-x^4$。分母中 $\\ln(\\cos x)=\\ln[1-(1-\\cos x)]\\sim-(1-\\cos x)\\sim-\\frac{x^2}{2}$，所以分母主项为 $-\\frac{x^4}{2}$。比值极限为 $2$。\n@@ 2038 3.2\n积分中的变量 $x$ 只是求和的哑变量，可以改名为 $t$，将它的值记为常数 $C=\\int_0^1 f(t)dt$。于是 $f(x)=\\frac1{1+x^2}+Cx^3$。对等式两边在 $[0,1]$ 上积分，得到\n\\[\nC=\\int_0^1\\frac{dx}{1+x^2}+C\\int_0^1 x^3dx\n=\\frac\\pi4+\\frac C4.\n\\]\n解得 $C=\\frac\\pi3$。代回得到 $f(x)=\\frac1{1+x^2}+\\frac\\pi3x^3$。最后再积一次，可得其 $[0,1]$ 上积分确为 $\\frac\\pi3$，满足常数的定义。\n@@ 2042 3.5\n(I) 积分区间 $[-1,1]$ 关于 $0$ 对称，先检查各项的奇偶性。分母只含 $x^2$，换成 $-x$ 后不变，而 $\\sin(-x)=-\\sin x$，所以\n\\[\n\\int_{-1}^1\\frac{\\sin x}{1+\\sqrt{1-x^2}}\\,dx=0.\n\\]\n这可以通过负半段令 $x=-t$ 来核对，负半段恰好是正半段的相反数。余下的分子是 $2x^2$，想到用平方差 $1-(\\sqrt{1-x^2})^2=x^2$ 消去分母的根号。于是\n\\[\n\\frac{2x^2}{1+\\sqrt{1-x^2}}=2(1-\\sqrt{1-x^2}),\\qquad\nI_1=2\\int_{-1}^1 1\\,dx-2\\int_{-1}^1\\sqrt{1-x^2}\\,dx.\n\\]\n第一个积分等于区间长度 $2$。第二个积分的曲线满足 $x^2+y^2=1$、$y\\ge0$，所围面积是半径 $1$ 的上半圆面积 $\\frac\\pi2$。所以 $I_1=2\\cdot2-2\\cdot\\frac\\pi2=4-\\pi$。\n\n(II) 根号下的 $1-\\sin2x$ 可以配成一个完全平方，因为\n\\[\n(\\sin x-\\cos x)^2=\\sin^2x+\\cos^2x-2\\sin x\\cos x=1-\\sin2x.\n\\]\n因此被积函数是 $|\\sin x-\\cos x|$。平方根取非负值，所以必须保留绝对值。这个函数的周期是 $\\pi$，因为 $x$ 增加 $\\pi$ 后括号内整体变号，绝对值不变。当 $n$ 为正整数时，$[0,n\\pi]$ 包含 $n$ 个完整周期，每一段的积分相同。\n\n先计算 $[0,\\pi]$。其中 $\\sin x-\\cos x$ 在 $\\frac\\pi4$ 处为零，在左段为负、右段为正，所以\n\\[\n\\begin{aligned}\nJ&=\\int_0^{\\frac\\pi4}(\\cos x-\\sin x)\\,dx+\n\\int_{\\frac\\pi4}^{\\pi}(\\sin x-\\cos x)\\,dx\\\\\n&=[\\sin x+\\cos x]_0^{\\frac\\pi4}\n+[-\\cos x-\\sin x]_{\\frac\\pi4}^{\\pi}\\\\\n&=(\\sqrt2-1)+(1+\\sqrt2)=2\\sqrt2.\n\\end{aligned}\n\\]\n累加 $n$ 段，得到 $I_2=nJ=2\\sqrt2\\,n$。\n\n(III) 根号内是 $1-x^2$，其导数含 $x$，恰好与分子的 $x\\,dx$ 配合，故令 $u=\\sqrt{1-x^2}$。平方后有 $u^2=1-x^2$，微分得 $2u\\,du=-2x\\,dx$，即 $x\\,dx=-u\\,du$。另外，$2-x^2=1+u^2$。代入后，分子中的 $u$ 与分母的根号 $u$ 相消，只剩下\n\\[\n\\frac{x\\,dx}{(2-x^2)\\sqrt{1-x^2}}=-\\frac{du}{1+u^2}.\n\\]\n原积分在 $x=1$ 处有奇性，先把上限取为 $b<1$。$x=0$ 时 $u=1$，$x=b$ 时 $u=\\sqrt{1-b^2}$，因此\n\\[\n\\int_0^b\\frac{x\\,dx}{(2-x^2)\\sqrt{1-x^2}}\n=-\\int_1^{\\sqrt{1-b^2}}\\frac{du}{1+u^2}\n=\\arctan1-\\arctan\\sqrt{1-b^2}.\n\\]\n令 $b\\to1^-$，第二项趋于 $0$，得到 $I_3=\\frac\\pi4$。这个有限极限也证明反常积分收敛。\n\n(IV) 记 $J=\\int_0^{\\frac\\pi2}\\ln(\\sin x)\\,dx$。先检查反常端点 $0$。由 $\\frac{\\sin x}{x}\\to1$，有\n\\[\n\\ln(\\sin x)=\\ln x+\\ln\\frac{\\sin x}{x},\\qquad\n\\ln\\frac{\\sin x}{x}\\longrightarrow0.\n\\]\n后面的修正项在 $0$ 附近有界，而 $\\int_\\varepsilon^\\delta\\ln x\\,dx=[x\\ln x-x]_\\varepsilon^\\delta$ 在 $\\varepsilon\\to0^+$ 时有有限极限，因为 $\\varepsilon\\ln\\varepsilon\\to0$。所以 $J$ 收敛，以下的拆分、换元和相加都有依据。\n\n直接求 $\\ln\\sin x$ 的原函数困难，看到区间端点为 $0,\\frac\\pi2$，可想到用 $x=\\frac\\pi2-t$ 将正弦换成余弦。此时 $dx=-dt$，上下限依次为 $\\frac\\pi2,0$，翻转上下限后得到\n\\[\nJ=\\int_0^{\\frac\\pi2}\\ln(\\cos t)\\,dt.\n\\]\n将两份相等的积分相加。区间内部正弦、余弦都为正，故对数可以合并，再用 $\\sin x\\cos x=\\frac12\\sin2x$：\n\\[\n2J=\\int_0^{\\frac\\pi2}\\ln(\\sin x\\cos x)\\,dx\n=\\int_0^{\\frac\\pi2}\\ln(\\sin2x)\\,dx-\\frac\\pi2\\ln2.\n\\]\n设这里的新积分为 $K$。令 $u=2x$，则 $dx=\\frac12du$，上下限变为 $0,\\pi$，所以\n\\[\nK=\\frac12\\left[\\int_0^{\\frac\\pi2}\\ln(\\sin u)\\,du+\n\\int_{\\frac\\pi2}^{\\pi}\\ln(\\sin u)\\,du\\right].\n\\]\n前一项就是 $J$。后一项令 $v=\\pi-u$，利用 $\\sin(\\pi-v)=\\sin v$，也得到 $J$。因此 $K=\\frac12(J+J)=J$。代回得到 $2J=J-\\frac\\pi2\\ln2$，移项即得 $I_4=J=-\\frac\\pi2\\ln2$。\n\n(V) 分母含 $1+\\cos2x$，先用二倍角公式 $1+\\cos2x=2\\cos^2x$，得到\n\\[\nI_5=\\frac12\\int_0^{\\frac\\pi4}x\\sec^2x\\,dx.\n\\]\n这里 $x$ 求导后会变成 $1$，而 $\\sec^2x$ 容易积分为 $\\tan x$，适合分部积分。取 $U=x$、$dV=\\sec^2x\\,dx$，则 $dU=dx$、$V=\\tan x$，从而\n\\[\nI_5=\\frac12[x\\tan x]_0^{\\frac\\pi4}\n-\\frac12\\int_0^{\\frac\\pi4}\\tan x\\,dx.\n\\]\n因 $\\frac{d}{dx}\\ln(\\cos x)=-\\tan x$，余下积分为 $[-\\ln(\\cos x)]_0^{\\frac\\pi4}=\\frac12\\ln2$。端点项为 $\\frac\\pi4\\cdot1-0=\\frac\\pi4$，故 $I_5=\\frac\\pi8-\\frac{\\ln2}{4}$。\n\n(VI) 指数为 $h(x)=x+\\frac1x$，求导得到 $h'(x)=1-\\frac1{x^2}$。指数函数求导时会出现这个因子，但题目中的因子为 $1+x-\\frac1x$。其中 $x-\\frac1x=xh'(x)$，余下的 $1$ 提示再乘一个 $x$，利用乘积法则产生它：\n\\[\n\\frac{d}{dx}\\bigl(xe^{h(x)}\\bigr)\n=e^{h(x)}+xe^{h(x)}h'(x)\n=\\left(1+x-\\frac1x\\right)e^{x+\\frac1x}.\n\\]\n所以原函数为 $xe^{x+\\frac1x}$。积分区间内 $x>0$，该原函数处处可导。两个端点的指数相同，$2+\\frac12=\\frac12+2=\\frac52$，因此\n\\[\nI_6=\\left[xe^{x+\\frac1x}\\right]_{\\frac12}^2\n=2e^{\\frac52}-\\frac12e^{\\frac52}\n=\\frac32e^{\\frac52}.\n\\]\n\n(VII) 被积式有两层对数，先从内层 $\\ln|x|$ 入手，因为分母中恰好有它的导数 $\\frac1x$。令 $u=\\ln|x|$，则 $du=\\frac{dx}{x}$。原区间中 $x<0$，$|x|$ 从 $e$ 变到 $\\sqrt e$，所以 $u$ 从 $1$ 变到 $\\frac12$。这时 $u>0$，外层的 $\\ln u$ 也有定义。代换后\n\\[\nI_7=\\int_1^{\\frac12}\\frac{\\ln u}{u}\\,du.\n\\]\n再令 $v=\\ln u$，则 $dv=\\frac{du}{u}$，上下限从 $1,\\frac12$ 变成 $0,-\\ln2$，所以\n\\[\nI_7=\\int_0^{-\\ln2}v\\,dv\n=\\left[\\frac{v^2}{2}\\right]_0^{-\\ln2}\n=\\frac12(\\ln2)^2.\n\\]\n两次换元都已经保留相应的积分方向，无需另加负号。原区间上分子、分母都为负，被积函数为正，与结果一致。\n\n(VIII) 分数指数 $\\frac32$ 表示先开平方再取三次幂。对负 $x$，$\\sqrt{x^2}$ 也取非负值，因此\n\\[\n(x^2)^{\\frac32}=(\\sqrt{x^2})^3=|x|^3.\n\\]\n$|x|^3$ 是偶函数，在 $[-1,0]$ 与 $[0,1]$ 上的积分相同。只算正半段再乘 $2$：\n\\[\nI_8=2\\int_0^1x^3\\,dx\n=2\\left[\\frac{x^4}{4}\\right]_0^1\n=2\\left(\\frac14-0\\right)=\\frac12.\n\\]\n@@ 2047 3.1\n每项提取 $\\frac1n$ 后，原和为\n\\[\nS_n=\\frac1n\\sum_{i=1}^n\\frac1{1+(\\frac in)^2+\\frac1{n^2}}.\n\\]\n先去掉随 $n$ 变化的 $\\frac1{n^2}$，记 $T_n=\\frac1n\\sum_{i=1}^n\\frac1{1+(\\frac in)^2}$。两项分式作差，分母都至少为 $1$，所以 $0\\le T_n-S_n\\le\\frac1{n^2}$，误差趋于零。$T_n$ 是连续函数 $\\frac1{1+x^2}$ 在 $[0,1]$ 上的右端点 Riemann 和，因此 $T_n\\to\\int_0^1\\frac{dx}{1+x^2}=\\frac\\pi4$。由误差估计，$S_n$ 的极限也为 $\\frac\\pi4$。\n@@ 2051 3.3\n在 $0<x<1$，$x^{n+1}<x^n$，且 $\\sqrt{1-x^2}>0$，因此对两边积分得 $a_{n+1}<a_n$，即严格单调减少。\n\n为得到间隔两项的关系，注意 $(1-x^2)^{\\frac32}$ 的导数含 $x\\sqrt{1-x^2}$。把整个乘积 $x^{n-1}(1-x^2)^{\\frac32}$ 求导再从 $0$ 积到 $1$。当 $n\\ge2$ 时两个端点都为零，故\n\\[\n0=(n-1)\\int_0^1x^{n-2}(1-x^2)^{\\frac32}dx-3a_n.\n\\]\n将积分中的 $(1-x^2)^{\\frac32}$ 写成 $(1-x^2)\\sqrt{1-x^2}$，该积分正是 $a_{n-2}-a_n$。于是 $(n-1)a_{n-2}=(n+2)a_n$，得到题设递推式。\n@@ 2055 3.3\n(I) 记左边为 $J$，令 $x=\\pi-u$。因为 $\\sin(\\pi-u)=\\sin u$，得 $J=\\int_0^\\pi(\\pi-u)f(\\sin u)du$。与原式相加，得到 $2J=\\pi\\int_0^\\pi f(\\sin x)dx$。\n\n(II) 取 $f(u)=u^n$，得到 $I=\\frac\\pi2 B_n$，其中 $B_n=\\int_0^\\pi\\sin^n x\\,dx$。对 $\\sin^{n-1}x\\sin x$ 分部，端点项为零，\n\\[\nB_n=(n-1)\\int_0^\\pi\\sin^{n-2}x\\cos^2x\\,dx\n=(n-1)(B_{n-2}-B_n).\n\\]\n所以 $B_n=\\frac{n-1}{n}B_{n-2}$。从 $B_0=\\pi,B_1=2$ 向下递推可得\n\\[\nI=\\begin{cases}\n\\frac{\\pi^2}{2}\\frac{1\\cdot3\\cdots(2m-1)}{2\\cdot4\\cdots2m},&n=2m,\\\\\n\\pi\\frac{2\\cdot4\\cdots2m}{1\\cdot3\\cdots(2m+1)},&n=2m+1.\n\\end{cases}\n\\]\n当 $m=0$ 时空乘积取 $1$，包括 $n=0,1$ 的情况。\n@@ 2061 3.3\n$y$ 在此题是参数，积分变量是 $x$。由 $|y|<1$，绝对值在积分内部的 $x=y$ 处分两段。在左段 $|x-y|=y-x$，右段等于 $x-y$，所以\n\\[\nI=\\int_{-1}^{y}(y-x)e^x dx+\\int_y^1(x-y)e^x dx.\n\\]\n分别作一次分部，或对候选乘积求导，可以得到两个原函数 $(y-x+1)e^x$、$(x-y-1)e^x$。代入端点后，\n\\[\nI=e^y-(y+2)e^{-1}-ye+e^y\n=2e^y-ye-(y+2)e^{-1}.\n\\]\n例如 $y=0$ 时得 $2-\\frac2e>0$，与原被积函数非负一致。\n@@ 2065 3.2\n出现 $x\\int_0^x f$ 的端点值，可以想到对这个乘积求导。记 $F(x)=\\int_0^x f(t)dt$，则 $(xF(x))'=F(x)+xf(x)$。由于 $f$ 单调增加，$0\\le t\\le x$ 时 $f(t)\\le f(x)$，对 $t$ 积分得 $F(x)\\le xf(x)$。因此\n\\[\n(xF(x))'\\le2xf(x).\n\\]\n从 $a$ 到 $b$ 积分，得 $bF(b)-aF(a)\\le2\\int_a^bxf(x)dx$，两边除以 $2$ 就是目标。这个比较只乘了正的长度 $x$，无需额外假设 $f$ 的正负。\n@@ 2069 3.2\n先由 $f'>0$、$f(0)=0$ 得 $f(x)>0$，$x>0$。记 $F(x)=\\int_0^x f(t)dt$，要让积分的平方出现，想到 $(F^2)'=2Ff$。因此只需比较 $f^3$ 与 $2Ff$，即比较 $f^2$ 与 $2F$。\n\n设 $H(x)=2F(x)-f(x)^2$。有 $H(0)=0$，而\n\\[\nH'(x)=2f(x)[1-f'(x)]>0,\\qquad 0<x<1.\n\\]\n由中值定理，$H(x)>0$。乘以正的 $f(x)$，得到 $f(x)^3<2F(x)f(x)$。对 $[0,1]$ 积分，右边是 $[F(x)^2]_0^1$，于是 $\\int_0^1 f(x)^3dx<[\\int_0^1 f(x)dx]^2$。条件 $f'<1$ 正是保证严格不等式的一步。\n@@ 2073 3.1\n条件给了导数的最大绝对值，先用 Lagrange 中值定理把它变成函数值的界。对每个 $x\\in(a,b]$，存在 $\\xi$ 在 $a,x$ 之间，使 $f(x)-f(a)=f'(\\xi)(x-a)$。由 $f(a)=0$，得到 $|f(x)|\\le M(x-a)$。\n\n接着两边积分，\n\\[\n\\int_a^b|f(x)|dx\\le M\\int_a^b(x-a)dx=\\frac M2(b-a)^2 .\n\\]\n题设分母 $(b-a)^2$ 为正，将它除到左边并乘以 $2$ 就得到结论。这里使用绝对值后上界始终非负，允许 $f$ 在区间内变号。\n@@ 2078 3.1\n右边是「区间长度乘以中点处的函数值」。为了让中点自然出现，在 $c=\\frac a2$ 处作切线。由 $f''>0$，$f'$ 严格增加，曲线位于这条切线上方。具体地，对 $x>c$，中值定理给出的斜率大于 $f'(c)$；对 $x<c$，斜率小于 $f'(c)$，但乘上负的 $x-c$ 后方向反转。因此两种情况都有\n\\[\nf(x)\\ge f(c)+f'(c)(x-c).\n\\]\n积分后 $\\int_0^a(x-c)dx=0$，切线的倾斜部分相消，留下 $\\int_0^a f(x)dx\\ge af(c)$，即所证。由于 $f''>0$，当 $x\\ne c$ 实际为严格大于。\n@@ 2082 3.1\n设区间中点为 $c=\\frac{a+b}{2}$。$f''>0$ 保证 $f'$ 严格增加。用中值定理可得曲线在中点的切线上方，\n\\[\nf(x)\\ge f(c)+f'(c)(x-c),\\qquad a\\le x\\le b.\n\\]\n理由是 $x>c$ 时，割线斜率至少为 $f'(c)$；$x<c$ 时割线斜率至多为 $f'(c)$，乘负的横坐标增量后又得到同一方向的不等式。两边积分，线性项关于中点奇对称，所以积分为零。得 $\\int_a^b f(x)dx\\ge(b-a)f(c)$。除以正数 $b-a$，便得题设结论。\n@@ 2087 3.5\n(I) 将根号配成 $\\sqrt{(x-1)^2-1}$。倒数代换 $u=\\frac1{x-1}$ 同时降低分母幂并把无穷上限化为有限端点。$dx=-\\frac{du}{u^2}$，原积分变为\n\\[\n\\int_0^1\\frac{u^3}{\\sqrt{1-u^2}}du.\n\\]\n再令 $v=1-u^2$，变为 $\\frac12\\int_0^1(1-v)v^{-\\frac12}dv=\\frac12(2-\\frac23)=\\frac23$。$v^{-\\frac12}$ 在 $0$ 可积，说明反常端点收敛。\n\n(II) 根号内 $(x-1)(3-x)=1-(x-2)^2$。先把端点截去，再用反正弦原函数 $\\arcsin(x-2)$，最后两端分别趋于 $\\pm1$，得到 $\\frac\\pi2-(-\\frac\\pi2)=\\pi$。两端的单侧积分均收敛，才能相加。\n@@ 2093 skip\n该题以参数曲线的弧长积分公式为核心。教材上册第三章第四节正文未讲授弧长公式，本次按教材明确教学范围暂不收录。\n@@ 2097 3.5\n面积要累加每段的正面积，故为 $A=\\int_0^{+\\infty}e^{-x}|\\sin x|dx$。若直接积 $e^{-x}\\sin x$，横轴下方的面积会被扣除。\n\n在第 $k$ 段 $[k\\pi,(k+1)\\pi]$ 令 $x=k\\pi+u$，则 $|\\sin x|=\\sin u$、$0\\le u\\le\\pi$，所以这段面积为 $e^{-k\\pi}J$，其中\n\\[\nJ=\\int_0^\\pi e^{-u}\\sin u\\,du\n=\\left[-\\frac{e^{-u}(\\sin u+\\cos u)}2\\right]_0^\\pi\n=\\frac{1+e^{-\\pi}}2.\n\\]\n先累加前 $N$ 段，用有限等比和得到 $J\\frac{1-e^{-N\\pi}}{1-e^{-\\pi}}$，令 $N\\to+\\infty$，得到 $A=\\frac{e^\\pi+1}{2(e^\\pi-1)}$。\n@@ 2101 3.4\n圆的方程写为 $(x-1)^2+y^2\\le1$。直线与圆交于 $(0,0),(1,1)$，满足 $y\\ge x$ 的部分只能位于 $0\\le x\\le1$，其上下边界为 $\\sqrt{2x-x^2}$ 和 $x$。\n\n绕竖直线 $x=2$，用竖条圆柱壳。半径为 $2-x$，高度为 $\\sqrt{2x-x^2}-x$，所以\n\\[\n\\frac{V}{2\\pi}=\\int_0^1(2-x)\\sqrt{2x-x^2}dx-\\int_0^1(2x-x^2)dx.\n\\]\n第二项为 $\\frac23$。第一项令 $u=x-1$，得 $\\int_{-1}^0(1-u)\\sqrt{1-u^2}du=\\frac\\pi4+\\frac13$，分别是单位圆四分之一面积和幂函数换元积分。相减再乘 $2\\pi$，得 $V=\\frac{\\pi^2}2-\\frac{2\\pi}3$。\n@@ 2105 3.4\n按几何题中 $a$ 是正半径，$b>a$ 保证整个圆位于横轴上方。对固定 $x\\in[-a,a]$，上下边界为 $y=b\\pm\\sqrt{a^2-x^2}$。旋转后得到圆环，其外半径为较大的纵坐标，内半径为较小的纵坐标。因此\n\\[\nV=\\pi\\int_{-a}^a\\big[(b+\\sqrt{a^2-x^2})^2-(b-\\sqrt{a^2-x^2})^2\\big]dx\n=4\\pi b\\int_{-a}^a\\sqrt{a^2-x^2}dx .\n\\]\n最后一个积分为半径 $a$ 的上半圆面积 $\\frac{\\pi a^2}2$，所以 $V=2\\pi^2a^2b$。先作平方差能使两个根式平方与 $b^2$ 全部抵消。\n@@ 2109 3.4\n由 $ax^2=1-x^2$，交点横坐标为 $c=\\frac1{\\sqrt{a+1}}$，纵坐标为 $ac^2$。过原点的直线斜率为 $ac$，所以直线方程 $y=acx$。在 $0<x<c$，直线高于 $ax^2$，旋转截面是圆环，故\n\\[\nV(a)=\\pi\\int_0^c[(acx)^2-(ax^2)^2]dx\n=\\frac{2\\pi a^2}{15(a+1)^{\\frac52}}.\n\\]\n此时 $a$ 才是待优化的变量。求导可将正因子提出，得到\n\\[\nV'(a)=\\frac{\\pi a(4-a)}{15(a+1)^{\\frac72}}.\n\\]\n所以 $0<a<4$ 时递增，$a>4$ 时递减，全局最大值在 $a=4$ 取得，为 $V_{\\max}=\\frac{32\\pi}{375\\sqrt5}$。两端 $a\\to0^+$、$a\\to+\\infty$ 的体积均趋于零。\n@@ 2113 3.4\n由原图，容器底部为 $y=-1$，顶部为 $y=2$。水平截面在 $y=\\frac12$ 处换边界。半径平方在下部为 $1-y^2$，上部为 $2y-y^2$。\n\n(I) 按圆盘体积累加，\n\\[\nV=\\pi\\int_{-1}^{\\frac12}(1-y^2)dy+\n\\pi\\int_{\\frac12}^2(2y-y^2)dy\n=\\pi\\left(\\frac98+\\frac98\\right)=\\frac{9\\pi}4.\n\\]\n(II) 记水密度为 $\\rho$、重力加速度为 $g$。高度 $y$ 处厚 $dy$ 的水层需提升 $2-y$，故功为重力乘提升高度。于是\n\\[\nW=\\rho g\\pi\\left[\\int_{-1}^{\\frac12}(2-y)(1-y^2)dy+\n\\int_{\\frac12}^2(2-y)(2y-y^2)dy\\right].\n\\]\n两个积分分别是 $\\frac{153}{64}$ 和 $\\frac{63}{64}$，所以 $W=\\frac{27\\pi\\rho g}{8}$。题干未指定 $\\rho,g$ 及长度单位，保留一般式。若坐标以米计且取 $\\rho=1000,g=10$，则为 $33750\\pi\\ \\mathrm J$。\n@@ 2124 3.2\n(I) 绝对值在 $t=x$ 处换号，先拆成 $g(x)=\\int_{-a}^x(x-t)f(t)dt+\\int_x^a(t-x)f(t)dt$。逐项求导，端点项都乘以零，得\n\\[\ng'(x)=\\int_{-a}^x f(t)dt-\\int_x^a f(t)dt,\\qquad g''(x)=2f(x)>0 .\n\\]\n按教材术语，二阶导数为正称图像凹，即图像位于弦下方，故(I)成立。\n\n(II) $f$ 为偶函数，两边的积分在 $x=0$ 相等，所以 $g'(0)=0$。又因 $g''>0$，$g'$ 严格增加，故 $g$ 在 $0$ 左侧递减、右侧递增，最小值是 $g(0)=2\\int_0^a t f(t)dt$。\n\n(III) 若该关系对任意 $a>0$ 成立，则 $2\\int_0^a t f(t)dt=f(a)-a^2-1$。令 $a\\to0^+$ 得 $f(0)=1$。对 $a$ 求导得 $f'(a)-2af(a)=2a$，即 $[(f(a)+1)e^{-a^2}]'=0$。由初值常数为 $2$，故 $f(a)=2e^{a^2}-1$；用偶性延伸到所有实数。它为正且可代回核对。若关系仅针对某个固定的 $a$，题设只有一条积分约束，无法唯一确定整个 $f$。\n"}

## tool · 2026-11-14T01:56:18Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"db46a0","wall_time_seconds":0.000010917,"exit_code":0,"original_token_count":2340,"output":"@@ 1466 3.2\n@@ 1480 3.2\n@@ 1492 3.2\n@@ 1496 3.3\n@@ 1508 3.2\n@@ 1512 3.3\n@@ 1518 3.3\n@@ 1526 3.3\n@@ 1534 3.3\n@@ 1542 3.3\n@@ 1552 3.3\n@@ 1556 3.3\n@@ 1560 3.3\n@@ 1565 3.3\n@@ 1569 3.3\n@@ 1573 3.2\n@@ 1577 3.2\n@@ 1583 3.3\n@@ 1588 3.3\n@@ 1595 3.3\n@@ 1600 3.3\n@@ 1604 3.3\n@@ 1608 3.3\n@@ 1612 3.3\n@@ 1619 3.2\n@@ 1623 3.3\n@@ 1629 3.3\n@@ 1636 3.1\n@@ 1640 3.3\n@@ 1648 3.3\n@@ 1652 3.3\n@@ 1656 3.3\n@@ 1660 3.3\n@@ 1664 3.3\n@@ 1668 3.3\n@@ 1672 3.5\n@@ 1676 3.3\n@@ 1680 3.3\n@@ 1684 3.3\n@@ 1688 3.3\n@@ 1692 3.2\n@@ 1696 3.3\n@@ 1704 3.3\n@@ 1708 3.2\n@@ 1712 3.3\n@@ 1718 3.2\n@@ 1722 3.2\n@@ 1726 3.2\n@@ 1730 3.2\n@@ 1734 3.2\n@@ 1738 3.2\n@@ 1742 2.5\n@@ 1746 3.1\n@@ 1752 3.1\n@@ 1756 3.3\n@@ 1760 1.2\n@@ 1764 3.5\n@@ 1776 3.1\n@@ 1788 3.1\n@@ 1792 3.1\n@@ 1800 3.3\n@@ 1808 3.2\n@@ 1812 2.5\n@@ 1820 3.1\n@@ 1824 3.3\n@@ 1832 3.3\n@@ 1842 3.5\n@@ 1846 3.5\n@@ 1850 3.5\n@@ 1856 3.5\n@@ 1868 3.5\n@@ 1874 3.5\n@@ 1878 3.5\n@@ 1882 3.5\n@@ 1886 3.4\n@@ 1897 3.4\n@@ 1905 3.4\n@@ 1916 3.5\n@@ 1920 skip\n@@ 1924 3.4\n@@ 1928 skip\n@@ 1932 3.4\n@@ 1936 3.4\n@@ 1940 3.4\n@@ 1946 3.4\n@@ 1960 3.1\n@@ 1972 3.2\n@@ 1984 3.1\n@@ 1998 3.5\n@@ 2012 3.1\n@@ 2016 3.2\n@@ 2020 3.2\n@@ 2024 3.2\n@@ 2030 3.2\n@@ 2034 3.2\n@@ 2038 3.2\n@@ 2042 3.5\n@@ 2047 3.1\n@@ 2051 3.3\n@@ 2055 3.3\n@@ 2061 3.3\n@@ 2065 3.2\n@@ 2069 3.2\n@@ 2073 3.1\n@@ 2078 3.1\n@@ 2082 3.1\n@@ 2087 3.5\n@@ 2093 skip\n@@ 2097 3.5\n@@ 2101 3.4\n@@ 2105 3.4\n@@ 2109 3.4\n@@ 2113 3.4\n@@ 2124 3.2\n5280:% SOURCE line=1466 pdf_page=228 section=3.2\n5773:% SOURCE line=2124 pdf_page=341 section=3.2\n5943:% SOURCE line=1518 pdf_page=234 section=3.3\n5973:% SOURCE line=1526 pdf_page=235 section=3.3\n6162:% SOURCE line=1583 pdf_page=245 section=3.3\n6186:% SOURCE line=1588 pdf_page=246 section=3.3\n6286:% SOURCE line=1612 pdf_page=251 section=3.3\nimport json\nimport math\nimport re\nfrom pathlib import Path\n\nfrom scipy.integrate import quad\n\n\ndef integral(function, lower, upper):\n    return quad(function, lower, upper, epsabs=1e-10, epsrel=1e-10)[0]\n\n\nsource_path = Path(\n    \"references/27李林880/md/【做题本】平板版27考研李林辅导讲义（高数）.md\"\n)\nsolution_path = Path(\".question-bank-work/lilin-ipad-integrals.txt\")\nsource_lines = source_path.read_text().splitlines()\nexpected_lines = {\n    number\n    for number, line in enumerate(source_lines, 1)\n    if 1462 <= number <= 2134 and line.startswith(\"#### \")\n}\nsolutions = solution_path.read_text()\nwritten_lines = [\n    int(number) for number in re.findall(r\"^@@ (\\d+) \", solutions, re.MULTILINE)\n]\nassert set(written_lines) == expected_lines\nassert len(written_lines) == len(expected_lines) == 114\n\nchunks = re.split(r\"^@@ (\\d+) (\\S+)\\n\", solutions, flags=re.MULTILINE)\nfor index in range(1, len(chunks), 3):\n    source_line, section, solution = chunks[index : index + 3]\n    assert solution.count(\"$\") % 2 == 0, source_line\n    assert solution.count(r\"\\[\") == solution.count(r\"\\]\"), source_line\n\nderivative_cases = [\n    (\n        \"1512\",\n        lambda x: (\n            2 * math.log(abs(x + 1)) / 3\n            + 2 * math.log(x * x - x + 1) / 3\n            - 2 * math.atan((2 * x - 1) / math.sqrt(3)) / math.sqrt(3)\n        ),\n        lambda x: (2 * x * x - x - 1) / (x**3 + 1),\n        (0.2, 2.0, -2.0),\n    ),\n    (\n        \"1526-2\",\n        lambda x: (\n            -2 * math.sqrt(1 + 1 / x)\n            - math.log(\n                abs(\n                    (math.sqrt(1 + 1 / x) - 1)\n                    / (math.sqrt(1 + 1 / x) + 1)\n                )\n            )\n        ),\n        lambda x: math.sqrt((1 + x) / x) / x,\n        (0.5, 2.0, -2.0),\n    ),\n    (\n        \"1526-3\",\n        lambda x: math.log(\n            abs(\n                (2 - math.sqrt(4 - x * x))\n                / (2 + math.sqrt(4 - x * x))\n            )\n        )\n        / 4,\n        lambda x: 1 / (x * math.sqrt(4 - x * x)),\n        (0.5, -0.5, 1.5),\n    ),\n    (\n        \"1552\",\n        lambda x: (\n            -3 * x / (2 * (x * x - 1))\n            + math.log(abs((x - 1) / (x + 1))) / 4\n        ),\n        lambda x: (2 * x * x + 1) / (x * x - 1) ** 2,\n        (0.2, 2.0, -2.0),\n    ),\n    (\n        \"1556\",\n        lambda x: (\n            x * x / 2\n            + math.log(abs(x + 1)) / 3\n            - math.log(x * x - x + 1) / 6\n            - math.atan((2 * x - 1) / math.sqrt(3)) / math.sqrt(3)\n        ),\n        lambda x: x**4 / (x**3 + 1),\n        (0.2, 2.0, -2.0),\n    ),\n    (\n        \"1569\",\n        lambda x: (\n            x * x * math.cos(x) - 4 * x * math.sin(x) - 6 * math.cos(x)\n        ),\n        lambda x: -x * x * math.sin(x) - 2 * x * math.cos(x) + 2 * math.sin(x),\n        (0.2, 1.0, 2.0),\n    ),\n    (\n        \"1588-5\",\n        lambda x: (\n            -2 * math.sqrt((1 - x) / (1 + x)) / (1 - (1 - x) / (1 + x))\n            + math.log(\n                abs(\n                    (1 + math.sqrt((1 - x) / (1 + x)))\n                    / (1 - math.sqrt((1 - x) / (1 + x)))\n                )\n            )\n        ),\n        lambda x: math.sqrt((1 - x) / (1 + x)) / x**2,\n        (0.2, 0.5, -0.5),\n    ),\n    (\n        \"1612-4\",\n        lambda x: (\n            -math.atan(x) / x\n            - math.atan(x) ** 2 / 2\n            + math.log(abs(x))\n            - math.log(1 + x * x) / 2\n        ),\n        lambda x: math.atan(x) / (x * x * (1 + x * x)),\n        (0.2, 2.0, -2.0),\n    ),\n]\nstep = 1e-5\nderivative_errors = []\nfor question, primitive, function, points in derivative_cases:\n    for point in points:\n        derivative = (primitive(point + step) - primitive(point - step)) / (2 * step)\n        error = abs(derivative - function(point))\n        assert error < 2e-6, (question, point, error)\n        derivative_errors.append(error)\n\nintegral_cases = [\n    (\n        \"1640-1\",\n        integral(lambda x: 1 / math.sqrt(x * x - 1), -2, -math.sqrt(2)),\n        math.log((math.sqrt(2) - 1) * (2 + math.sqrt(3))),\n    ),\n    (\n        \"1640-3\",\n        integral(lambda x: x * math.sin(x) ** 2, 0, math.pi / 2),\n        math.pi**2 / 16 + 0.25,\n    ),\n    (\n        \"1676\",\n        integral(lambda x: math.sin(x) * math.cos(x) / (x + 1), 0, math.pi / 2),\n        0.25\n        + 1 / (2 * (math.pi + 2))\n        - integral(lambda x: math.cos(x) / (x + 2) ** 2, 0, math.pi) / 2,\n    ),\n    (\n        \"1905-volume\",\n        2\n        * math.pi\n        * (\n            integral(lambda x: (math.e - x) * x / math.e, 0, math.e)\n            - integral(lambda x: (math.e - x) * math.log(x), 1, math.e)\n        ),\n        2 * math.pi * (5 * math.e**2 / 12 - math.e + 0.25),\n    ),\n    (\n        \"1916\",\n        math.pi\n        * sum(\n            integral(\n                lambda x: math.exp(-2 * x) * math.sin(x),\n                2 * number * math.pi,\n                (2 * number + 1) * math.pi,\n            )\n            for number in range(4)\n        ),\n        math.pi / (5 * (1 - math.exp(-2 * math.pi))),\n    ),\n    (\"1940\", 4 / (8 / 3 + 8 / 15), 5 / 4),\n    (\n        \"2101\",\n        2\n        * math.pi\n        * integral(lambda x: (2 - x) * (math.sqrt(2 * x - x * x) - x), 0, 1),\n        math.pi**2 / 2 - 2 * math.pi / 3,\n    ),\n    (\n        \"2113-volume\",\n        integral(lambda y: 1 - y * y, -1, 0.5)\n        + integral(lambda y: 2 * y - y * y, 0.5, 2),\n        9 / 4,\n    ),\n    (\n        \"2113-work\",\n        integral(lambda y: (2 - y) * (1 - y * y), -1, 0.5)\n        + integral(lambda y: (2 - y) * (2 * y - y * y), 0.5, 2),\n        27 / 8,\n    ),\n    (\n        \"2042-I\",\n        integral(\n            lambda x: (2 * x * x + math.sin(x)) / (1 + math.sqrt(1 - x * x)),\n            -1,\n            1,\n        ),\n        4 - math.pi,\n    ),\n    (\n        \"2042-II\",\n        integral(lambda x: math.cos(x) - math.sin(x), 0, math.pi / 4)\n        + integral(lambda x: math.sin(x) - math.cos(x), math.pi / 4, math.pi),\n        2 * math.sqrt(2),\n    ),\n    (\n        \"2042-III\",\n        integral(lambda x: x / ((2 - x * x) * math.sqrt(1 - x * x)), 0, 1),\n        math.pi / 4,\n    ),\n    (\n        \"2042-IV\",\n        integral(lambda x: math.log(math.sin(x)), 0, math.pi / 2),\n        -math.pi * math.log(2) / 2,\n    ),\n    (\n        \"2042-V\",\n        integral(lambda x: x / (1 + math.cos(2 * x)), 0, math.pi / 4),\n        math.pi / 8 - math.log(2) / 4,\n    ),\n    (\n        \"2042-VI\",\n        integral(lambda x: (1 + x - 1 / x) * math.exp(x + 1 / x), 0.5, 2),\n        3 * math.exp(2.5) / 2,\n    ),\n    (\n        \"2042-VII\",\n        integral(\n            lambda x: math.log(math.log(abs(x))) / (x * math.log(abs(x))),\n            -math.e,\n            -math.sqrt(math.e),\n        ),\n        math.log(2) ** 2 / 2,\n    ),\n    (\n        \"2042-VIII\",\n        integral(lambda x: (x * x) ** 1.5, -1, 1),\n        0.5,\n    ),\n]\nintegral_errors = []\nfor question, calculated, expected in integral_cases:\n    error = abs(calculated - expected)\n    assert error < 1e-8, (question, calculated, expected)\n    integral_errors.append(error)\n\nprint(\n    json.dumps(\n        {\n            \"status\": \"passed\",\n            \"type\": \"mathematical-verification\",\n            \"message\": \"题号、数学环境与选定数值复算通过\",\n            \"suggestion\": \"结合最终编译和视觉检查交付\",\n            \"source_entries\": len(expected_lines),\n            \"derivative_checks\": len(derivative_errors),\n            \"integral_checks\": len(integral_errors),\n            \"max_derivative_error\": max(derivative_errors),\n            \"max_integral_error\": max(integral_errors),\n        },\n        ensure_ascii=False,\n        indent=2,\n    )\n)\n"}

## tool · 2026-11-14T01:56:25Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"a8660b","wall_time_seconds":0.000010458,"exit_code":127,"original_token_count":9,"output":"zsh:1: command not found: python\n"}

## tool · 2026-11-14T01:56:33Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"b70c4b","wall_time_seconds":0.000009916,"exit_code":0,"original_token_count":4315,"output":"% SOURCE line=1466 pdf_page=228 section=3.2\n\n\\Question{247}{第5章 · 例题第1组 · 例 1}\n\n设 $g(x)=\\int_{0}^{x}f(u)du$，其中 $f(x)=\\left\\{\\begin{aligned}&\\frac{1}{2}(x^{2}+1),&0\\leqslant x<1,\\\\&\\frac{1}{3}(x-1),&1\\leqslant x\\leqslant2,\\end{aligned}\\right.$ 则$g(x)$在$(0,2)$内().\n\n\\textbf{A.} 无界\n\n\\textbf{B.} 单调减少\n\n\\textbf{C.} 不连续\n\n\\textbf{D.} 连续\n\n\\vfill\n\n\\Solution\n\n遇到分段的被积函数，先看分段点是否会使面积突然跳跃。对 $0<x<1$，直接积分得 $g(x)=\\frac{x^3}{6}+\\frac x2$。对 $1\\leq x<2$，将积分在 $1$ 处分开：\n\\[\ng(x)=\\int_0^1 f(u)\\,du+\\int_1^x\\frac{u-1}{3}\\,du=\\frac23+\\frac{(x-1)^2}{6}.\n\\]\n第一个式子在 $x\\to1^-$ 时趋于 $\\frac23$，第二个式子给出 $g(1)=\\frac23$ 且右极限相同。因此 $g$ 在整个区间连续，选 \\textbf{D}。$f$ 在 $1$ 处跳变只影响 $g$ 的斜率，积分累积的面积依然连续。\n\n\\clearpage\n\n% SOURCE line=1480 pdf_page=229 section=3.2\n\n\\Question{248}{第5章 · 例题第1组 · 例 2}\n\n设 $f(x)$ 是奇函数，除 x=0 外，$f(x)$ 处处连续，x=0 是 $f(x)$ 的第一类间断点，则 $\\int_{0}^{x}f(t)dt$ 是（）.\n\n\\textbf{A.} 连续的奇函数\n\n\\textbf{B.} 连续的偶函数\n\n\\textbf{C.} 在 x=0 处间断的奇函数\n\n\\textbf{D.} 在 x=0 处间断的偶函数\n\n\\vfill\n\n\\Solution\n\n先分开判断连续性和奇偶性。第一类间断意味着 $0$ 的左右极限有限。结合其余各点连续，$f$ 在每个有限闭区间有界且可积。因此对附近的 $x,y$，取共同上界 $|f|\\le M$，有 $|g(y)-g(x)|=|\\int_x^y f(t)\\,dt|\\le M|y-x|$，得到 $g$ 连续。\n\n判断奇偶性就将 $-x$ 代入。令 $t=-u$，$dt=-du$，同时利用 $f(-u)=-f(u)$，\n\\[\ng(-x)=-\\int_0^x f(-u)\\,du=\\int_0^x f(u)\\,du=g(x).\n\\]\n因此 $g$ 是连续的偶函数，选 \\textbf{B}。\n\n\\clearpage\n\n% SOURCE line=1492 pdf_page=230 section=3.2\n\n\\Question{249}{第5章 · 例题第1组 · 例 3}\n\n已知 $f'(e^x) = x e^{-x}$，且 $f(1) = 0$，则 $f(x) =$ \\underline{\\hspace{4em}}.\n\n\\vfill\n\n\\Solution\n\n题目给的是 $f'$ 在 $e^x$ 处的值。要找 $f'(u)$，先把 $e^x$ 整体看成新变量 $u$，于是 $u>0$、$x=\\ln u$、$e^{-x}=\\frac1u$。这给出 $f'(u)=\\frac{\\ln u}{u}$。分子 $\\ln u$ 的导数恰是 $\\frac1u$，因此\n\\[\nf(u)=\\frac12(\\ln u)^2+C.\n\\]\n代入 $f(1)=0$，由 $\\ln1=0$ 得 $C=0$。填 $\\frac12(\\ln x)^2$，适用 $x>0$。将 $e^x$ 代回导数，可恢复 $x e^{-x}$。\n\n\\clearpage\n\n% SOURCE line=1508 pdf_page=232 section=3.2\n\n\\Question{250}{第5章 · 例题第1组 · 例 5}\n\n计算 $I=\\int\\max\\{x^{3},x^{2},1\\}dx$.\n\n\\vfill\n\n\\Solution\n\n\\TextCorrection{将积分写为 $I=\\int \\max\\{x^3,x^2,1\\}\\,dx$，最大值是被积函数。}\n先比较三个数。$x<-1$ 时，$x^2>1$ 且 $x^3<0$。$-1\\le x\\le1$ 时，$x^2\\le1$ 且 $x^3\\le1$。$x>1$ 时，$x^3>x^2>1$。分别对 $x^2,1,x^3$ 积分，然后令三个表达式在连接点取同一个值，才能得到全实轴上的原函数。\n\\[\nI=C+\\begin{cases}\n\\frac{x^3}{3}-\\frac23,&x<-1,\\\\\nx,&-1\\le x\\le1,\\\\\n\\frac{x^4}{4}+\\frac34,&x>1.\n\\end{cases}\n\\]\n两处左右值分别都是 $-1+C,1+C$，两边导数也都为 $1$，所以连接点同样可导。\n\n\\clearpage\n\n% SOURCE line=1573 pdf_page=243 section=3.2\n\n\\Question{251}{第5章 · 例题第2组 · 例 10}\n\n已知$\\int f'(x^{3})dx = x^{3} + C$，求 $f(x)$.\n\n\\vfill\n\n\\Solution\n\n不定积分等式说明右边是左边被积函数的原函数，先对 $x$ 求导得 $f'(x^3)=3x^2$。这一步直接对原函数求导，无需对 $f'(x^3)$ 再求导。立方函数可以取任意实数，因此令 $t=x^3$，得到 $f'(t)=3(\\sqrt[3]t)^2$。\n\n由于 $\\frac{d}{dt}(\\sqrt[3]t)^5=\\frac53(\\sqrt[3]t)^2$，积分后\n\\[\nf(x)=\\frac95(\\sqrt[3]x)^5+C_1.\n\\]\n在 $x=0$，用差商可验证导数为 $0$，和题给关系一致。\n\n\\clearpage\n\n% SOURCE line=1577 pdf_page=244 section=3.2\n\n\\Question{252}{第5章 · 例题第2组 · 例 11}\n\n设 $f'(\\ln x) = \\begin{cases} 1, & 0 < x \\leqslant 1, \\\\ x, & x > 1, \\end{cases}$ 求 $f(\\ln x)$.\n\n\\vfill\n\n\\Solution\n\n令 $t=\\ln x$。当 $0<x\\le1$ 时 $t\\le0$，$f'(t)=1$；当 $x>1$ 时 $t>0$，$f'(t)=e^t$。因此分别得到 $t+C_1$ 和 $e^t+C_2$。$f$ 在 $t=0$ 可导，必须连续，所以 $C_1=1+C_2$。令 $C=C_1$，还原变量后得\n\\[\nf(\\ln x)=\\begin{cases}\n\\ln x+C,&0<x\\le1,\\\\\nx-1+C,&x>1.\n\\end{cases}\n\\]\n在连接点，两侧关于 $t$ 的导数都等于 $1$，也符合条件。\n\n\\clearpage\n\n% SOURCE line=1496 pdf_page=231 section=3.3\n\n\\Question{277}{第5章 · 例题第1组 · 例 4}\n\n设$\\frac{\\sin x}{x}$ 是 $f(x)$ 的一个原函数，$a \\neq 0$，则$\\int \\frac{f(ax)}{a} \\, dx = (\\quad)$.\n\n\\textbf{A.} $\\frac{\\sin ax}{a^{3}x} + C$\n\n\\textbf{B.} $\\frac{\\sin ax}{a^{2}x} + C$\n\n\\textbf{C.} $\\frac{\\sin ax}{ax} + C$\n\n\\textbf{D.} $\\frac{\\sin ax}{x} + C$\n\n\\vfill\n\n\\Solution\n\n设 $F(t)=\\frac{\\sin t}{t}$，则 $F'(t)=f(t)$。看到 $f(ax)$ 时，想到将 $F$ 中的自变量换成 $ax$。链式法则给出 $\\frac{d}{dx}F(ax)=a f(ax)$，因此要乘 $\\frac1{a^2}$ 才会得到题目的 $\\frac{f(ax)}a$。所以\n\\[\n\\int \\frac{f(ax)}a\\,dx=\\frac{1}{a^2}F(ax)+C=\\frac{\\sin ax}{a^3x}+C.\n\\]\n选 \\textbf{A}。外部出现的两个 $a$ 分别来自题目的除数和抵消链式求导，第三个 $a$ 来自 $F(ax)$ 自身的分母。\n\n\\clearpage\n\n% SOURCE line=1512 pdf_page=233 section=3.3\n\n\\Question{278}{第5章 · 例题第1组 · 示例}\n\n计算积分 $I=\\int\\frac{2x^{2}-x-1}{x^{3}+1}dx$.\n\n\\vfill\n\n\\Solution\n\n分母能分解为 $(x+1)(x^2-x+1)$，其中二次因式配方后恒正。先按因式拆分，乘回分母比较系数可得\n\\[\n\\frac{2x^2-x-1}{x^3+1}=\\frac{2}{3(x+1)}+\\frac{2(2x-1)-3}{3(x^2-x+1)}.\n\\]\n二次式的导数是 $2x-1$，对应对数。剩下的常数分子用配方 $(x-\\frac12)^2+\\frac34$，对应反正切。因此\n\\[\nI=\\frac23\\ln|x+1|+\\frac23\\ln(x^2-x+1)\n-\\frac{2}{\\sqrt3}\\arctan\\frac{2x-1}{\\sqrt3}+C .\n\\]\n在 $x=-1$ 两侧的区间上，积分常数可各自选取。\n\n\\clearpage\n\n% SOURCE line=1518 pdf_page=234 section=3.3\n\n\\Question{279}{第5章 · 例题第2组 · 例 1}\n\n计算下列不定积分：\n\n(1) $\\int \\frac{dx}{x(1+2\\ln x)};$ (2) $\\int \\frac{dx}{1+e^x};$ (3) $\\int \\frac{dx}{\\cos^4 x};$\n\n(4) $\\int \\frac{\\sin 2x}{1+\\sin^4 x}dx;$ (5) $\\int \\frac{x+1}{x(1+x e^x)}dx;$ (6) $\\int \\frac{\\ln(\\tan x)}{\\sin 2x}dx.$\n\n\\vfill\n\n\\Solution\n\n每小问先找被积式中可以连同导数一起替换的部分。\n\n(1) $u=1+2\\ln x$ 时 $du=\\frac2x\\,dx$，得到 $\\frac12\\ln|1+2\\ln x|+C$。\n\n(2) 分子分母同乘 $e^{-x}$，令 $u=1+e^{-x}$，则分子 $e^{-x}dx=-du$，得到 $-\\ln(1+e^{-x})+C$。\n\n(3) 写成 $(1+\\tan^2 x)\\sec^2 x\\,dx$，令 $u=\\tan x$，积分 $1+u^2$，得 $\\tan x+\\frac{\\tan^3 x}{3}+C$。\n\n(4) $d(\\sin^2 x)=\\sin 2x\\,dx$。令 $u=\\sin^2 x$ 后积分 $\\frac1{1+u^2}$，得 $\\arctan(\\sin^2 x)+C$。\n\n(5) 看见 $xe^x$ 及其导数的因子 $x+1$，令 $u=xe^x$。原式变为 $\\frac{du}{u(1+u)}$。拆成 $\\frac1u-\\frac1{1+u}$，得 $\\ln\\left|\\frac{xe^x}{1+xe^x}\\right|+C$。\n\n(6) $d(\\ln\\tan x)=\\frac{2}{\\sin 2x}\\,dx$，故结果是 $\\frac14(\\ln\\tan x)^2+C$。各式在原被积函数有定义的区间上使用。\n\n\\clearpage\n\n% SOURCE line=1526 pdf_page=235 section=3.3\n\n\\Question{280}{第5章 · 例题第2组 · 例 2}\n\n计算下列不定积分：\n\n(1) $\\int \\frac{\\mathrm{d}x}{\\sqrt{x} + \\sqrt[3]{x}}$; (2) $\\int \\frac{1}{x} \\sqrt{\\frac{1 + x}{x}} \\mathrm{d}x$; (3) $\\int \\frac{\\mathrm{d}x}{x \\sqrt{4 - x^2}}$;\n\n(4) $\\int \\frac{\\mathrm{d}x}{\\sqrt{\\mathrm{e}^x - 1}}$; (5) $\\int \\frac{x - 2}{\\sqrt{2x^2 + 4x + 5}} \\mathrm{d}x$.\n\n\\vfill\n\n\\Solution\n\n(1) 两个根号指数的分母是 $2,3$，取 $u=x^{\\frac16}$ 同时消去。被积式化成 $\\frac{6u^3}{u+1}\\,du$。用多项式除法后结果为 $6[\\frac{u^3}{3}-\\frac{u^2}{2}+u-\\ln(1+u)]+C$。\n\n(2) 令 $u=\\sqrt{1+\\frac1x}$，则 $\\frac{dx}{x}=-\\frac{2u}{u^2-1}\\,du$。原式变为 $-2[1+\\frac1{u^2-1}]\\,du$，拆分两个一次因式，得 $-2u-\\ln\\left|\\frac{u-1}{u+1}\\right|+C$。\n\n(3) 根号内的导数含 $x$，取 $u=\\sqrt{4-x^2}$ 后，$\\frac{dx}{x\\sqrt{4-x^2}}=-\\frac{du}{4-u^2}$，得 $\\frac14\\ln\\left|\\frac{2-u}{2+u}\\right|+C$。\n\n(4) $u=\\sqrt{e^x-1}$，$e^x=1+u^2$ 给出 $\\frac{dx}{u}=\\frac{2du}{1+u^2}$，结果 $2\\arctan u+C$。\n\n(5) 令 $v=x+1$，根号为 $R=\\sqrt{2v^2+3}$，分子为 $v-3$。$dR=\\frac{2v}{R}\\,dv$ 处理第一项。第二项利用 $\\frac{d}{dv}\\ln(\\sqrt2v+R)=\\frac{\\sqrt2}{R}$。相加得 $\\frac R2-\\frac3{\\sqrt2}\\ln(\\sqrt2v+R)+C$。\n\n\\clearpage\n\n% SOURCE line=1534 pdf_page=236 section=3.3\n\n\\Question{281}{第5章 · 例题第2组 · 例 3}\n\n计算下列不定积分：\n\n(1) $\\int(x+1)\\mathrm{e}^{3x}dx$; (2) $\\int\\frac{\\ln^{2}x}{x^{2}}dx$;\n\n(3) $\\int\\sin(\\ln x)dx$; (4) $\\int(\\arcsin x)^{2}dx$.\n\n\\vfill\n\n\\Solution\n\n(1) 选 $u=x+1$，$dv=e^{3x}dx$。分部积分后 $du=dx$ 降为常数，得到 $\\frac{(x+1)e^{3x}}3-\\frac{e^{3x}}9+C$。\n\n(2) 选 $u=(\\ln x)^2$，$dv=x^{-2}dx$。得到 $-\\frac{(\\ln x)^2}{x}+2\\int\\frac{\\ln x}{x^2}\\,dx$。再用 $u=\\ln x$ 分部一次，结果 $-\\frac{(\\ln x)^2+2\\ln x+2}{x}+C$。\n\n(3) 先令 $t=\\ln x$，原式为 $\\int e^t\\sin t\\,dt$。两次分部后有 $I=e^t\\sin t-e^t\\cos t-I$，所以 $I=\\frac x2[\\sin(\\ln x)-\\cos(\\ln x)]+C$。\n\n(4) 令 $t=\\arcsin x$，得到 $\\int t^2\\cos t\\,dt$。先分部得 $t^2\\sin t-2\\int t\\sin t\\,dt$，再分部得 $t^2\\sin t+2t\\cos t-2\\sin t$。结果为 $x(\\arcsin x)^2+2\\sqrt{1-x^2}\\arcsin x-2x+C$。\n\n\\clearpage\n\n% SOURCE line=1542 pdf_page=237 section=3.3\n\n\\Question{282}{第5章 · 例题第2组 · 例 4}\n\n计算下列不定积分：\n\n(1) $\\int \\frac{2x+3}{x^{2}+3x-10}dx$; (2) $\\int e^{2x}(\\tan x+1)^{2}dx$;\n\n(3) $\\int \\frac{x^{2}+1}{x^{4}+1}dx$; (4) $\\int \\frac{x e^{x}}{(1+x)^{2}}dx$;\n\n(5) $\\int \\frac{x+\\sin x}{1+\\cos x}dx$; (6) $\\int \\frac{1-\\sin x+\\cos x}{1+\\sin x-\\cos x}dx$.\n\n\\vfill\n\n\\Solution\n\n(1) 分子是分母导数，结果 $\\ln|x^2+3x-10|+C$。\n\n(2) 展开得 $(\\tan x+1)^2=\\sec^2 x+2\\tan x$，认出乘积求导，结果 $e^{2x}\\tan x+C$。\n\n(3) 写成 $\\frac12[\\frac1{x^2-\\sqrt2 x+1}+\\frac1{x^2+\\sqrt2 x+1}]$，因为两个分母的乘积为 $x^4+1$。配方后得 $\\frac1{\\sqrt2}[\\arctan(\\sqrt2 x-1)+\\arctan(\\sqrt2 x+1)]+C$。\n\n(4) 分子 $x$ 可以写成 $(1+x)-1$，对应 $\\frac{d}{dx}(\\frac{e^x}{1+x})=\\frac{xe^x}{(1+x)^2}$，故原函数为 $\\frac{e^x}{1+x}+C$。\n\n(5) $\\frac1{1+\\cos x}$ 是 $\\tan\\frac x2$ 的导数，$\\frac{\\sin x}{1+\\cos x}=\\tan\\frac x2$。两项正好拼出乘积导数，结果 $x\\tan\\frac x2+C$。\n\n(6) 原分式是 $\\frac{2}{1+\\sin x-\\cos x}-1$。令 $t=\\tan\\frac x2$，第一项化为 $\\frac{2}{t(t+1)}dt$。拆分后结果 $2\\ln\\left|\\frac{\\sin\\frac x2}{\\sin\\frac x2+\\cos\\frac x2}\\right|-x+C$。\n\n\\clearpage\n\n% SOURCE line=1552 pdf_page=238 section=3.3\n\n\\Question{283}{第5章 · 例题第2组 · 例 5}\n\n计算 $I=\\int\\frac{2x^{2}+1}{(x^{2}-1)^{2}}dx$.\n\n\\vfill\n\n\\Solution\n\n分母有两个二重因式，原式是偶函数，因此把两处二阶项配成和，把一次项配成差。通分比较分子得\n\\[\n\\frac{2x^2+1}{(x^2-1)^2}\n=\\frac34\\left(\\frac1{(x-1)^2}+\\frac1{(x+1)^2}\\right)\n+\\frac14\\left(\\frac1{x-1}-\\frac1{x+1}\\right).\n\\]\n二阶项积分给出负倒数，一次项积分给出对数。合并得到\n\\[\nI=-\\frac{3x}{2(x^2-1)}+\\frac14\\ln\\left|\\frac{x-1}{x+1}\\right|+C .\n\\]\n检查时先将第一项拆回两个倒数，再分别求导即可恢复上式。\n\n\\clearpage\n\n% SOURCE line=1556 pdf_page=239 section=3.3\n\n\\Question{284}{第5章 · 例题第2组 · 例 6}\n\n计算 $I=\\int\\frac{x^{4}}{x^{3}+1}\\,\\mathrm{d}x$.\n\n\\vfill\n\n\\Solution\n\n分子次数高于分母，先做除法，得 $x-\\frac{x}{x^3+1}$。接着把分母分为 $(x+1)q$，其中 $q=x^2-x+1$。通分核对可得\n\\[\n\\frac{x}{x^3+1}=-\\frac1{3(x+1)}+\\frac{2x-1}{6q}+\\frac1{2q}.\n\\]\n三项依次用一次式积分、$\\frac{q'}q$ 型积分和二次式配方积分。留意原式对整个余项取负，最终\n\\[\nI=\\frac{x^2}{2}+\\frac13\\ln|x+1|-\\frac16\\ln q\n-\\frac1{\\sqrt3}\\arctan\\frac{2x-1}{\\sqrt3}+C.\n\\]\n\n\\clearpage\n\n% SOURCE line=1560 pdf_page=240 section=3.3\n\n\\Question{285}{第5章 · 例题第2组 · 例 7}\n\n设 $f(x)$ 是严格单调的可导函数, $f^{-1}(x)$ 是其反函数, 若 $\\int f(x)dx = F(x) + C$, 求 $I=\\int f^{-1}(x)dx$.\n\n\\vfill\n\n\\Solution\n\n反函数看起来不容易直接积分。把 $x=f(t)$，那么 $f^{-1}(x)=t$，换元后 $\\int f^{-1}(x)\\,dx=\\int t f'(t)\\,dt$。这个乘积适合分部积分，让 $t$ 求导、$f'(t)$ 积分，于是\n\\[\n\\int t f'(t)\\,dt=t f(t)-F(t)+C.\n\\]\n将 $t$ 换回去，答案为 $x f^{-1}(x)-F(f^{-1}(x))+C$。即便反函数在某点不可导，该式仍是原函数。设 $t_0=f^{-1}(x_0)$，其增量减去 $t_0(x-x_0)$ 等于 $\\int_{t_0}^t[f(t)-f(s)]\\,ds$，绝对值至多为 $|t-t_0||x-x_0|$。除以 $|x-x_0|$ 后趋于零。\n\n\\clearpage\n\n% SOURCE line=1565 pdf_page=241 section=3.3\n\n\\Question{286}{第5章 · 例题第2组 · 例 8}\n\n设 $F(x)$ 为 $f(x)$ 的原函数，当 $x \\geqslant 0$ 时，$f(x)F(x) = \\frac{x \\mathrm{e}^{x}}{2(1 + x)^{2}}$，已知 $F(0) = 1, F(x) > 0$，求 $f(x)$.\n\n\\vfill\n\n\\Solution\n\n看到 $fF$ 且 $f=F'$，应想到 $\\frac{d}{dx}(F^2)=2FF'$，所以 $(F^2)'=\\frac{xe^x}{(1+x)^2}$。右式正好是 $\\frac{e^x}{1+x}$ 的导数，因为商求导后分子是 $e^x(1+x)-e^x=xe^x$。积分得到\n\\[\nF(x)^2=\\frac{e^x}{1+x}+C.\n\\]\n代入 $F(0)=1$ 得 $C=0$。由 $F>0$ 取正平方根，即 $F=e^{\\frac x2}(1+x)^{-\\frac12}$。再求导得到\n\\[\nf(x)=\\frac{x e^{\\frac x2}}{2(1+x)^{\\frac32}},\\qquad x\\ge0.\n\\]\n两式相乘可恢复题给的乘积。\n\n\\clearpage\n\n% SOURCE line=1569 pdf_page=242 section=3.3\n\n\\Question{287}{第5章 · 例题第2组 · 例 9}\n\n设 $f(x)$ 的一个原函数 $F(x)=\\frac{\\sin x}{x}$，求 $\\mathrm{I}=\\int x^{3}f'(x)dx$.\n\n\\vfill\n\n\\Solution\n\n目标里有 $f'$，条件只给 $F$。通过两次分部，把 $f'$ 积成 $f$ 再积成 $F$，同时多项式每次降一次：\n\\[\nI=x^3f(x)-3\\int x^2 f(x)\\,dx\n=x^3f(x)-3x^2F(x)+6\\int xF(x)\\,dx.\n\\]\n最后一项因 $xF(x)=\\sin x$ 变得容易，且 $f=F'=\\frac{x\\cos x-\\sin x}{x^2}$。所以\n\\[\nI=x^2\\cos x-4x\\sin x-6\\cos x+C.\n\\]\n若将 $F$ 按极限连续延拓至 $0$，这个原函数也可以在 $0$ 处使用。\n\n\\clearpage\n\n% SOURCE line=1583 pdf_page=245 section=3.3\n\n\\Question{288}{第5章 · 解答题 · 第 1 题}\n\n求下列不定积分： (I) $\\int \\frac{\\mathrm{d}x}{\\sqrt{x(4-x)}};$ (II) $\\int \\left(1 - \\frac{1}{x^2}\\right)e^{x + \\frac{1}{x}} \\mathrm{d}x;$ (III) $\\int \\frac{\\mathrm{d}x}{\\sqrt{x(x+2)}};$ (IV) $\\int \\frac{x^{5}}{\\sqrt[3]{1+x^{3}}} \\mathrm{d}x;$ (V) $\\int \\frac{\\mathrm{d}x}{\\sqrt{\\sin x} \\cos x};$ (VI) $\\int \\frac{e^{3x} + e^{x}}{e^{4x} + 1} \\mathrm{d}x.$\n\n\\vfill\n\n\\Solution\n\n(I) 配方 $x(4-x)=4-(x-2)^2$，用反正弦原函数，得 $\\arcsin\\frac{x-2}{2}+C$。\n\n(II) 指数 $x+\\frac1x$ 的导数就是前面的括号，故为 $e^{x+\\frac1x}+C$。\n\n(III) 配方 $x(x+2)=(x+1)^2-1$。令 $u=x+1$，$\\ln|u+\\sqrt{u^2-1}|$ 的导数为 $\\frac1{\\sqrt{u^2-1}}$。故结果 $\\ln|x+1+\\sqrt{x(x+2)}|+C$。\n\n(IV) $u=1+x^3$，$x^5dx=\\frac{u-1}{3}du$，积分两项幂函数，得 $\\frac{u^{\\frac53}}5-\\frac{u^{\\frac23}}2+C$，分数次幂按实立方根理解。\n\n(V) $u=\\sqrt{\\sin x}$ 后化成 $\\frac{2du}{1-u^4}=[\\frac1{1-u^2}+\\frac1{1+u^2}]du$，故为 $\\frac12\\ln|\\frac{1+u}{1-u}|+\\arctan u+C$。\n\n(VI) $u=e^x$ 可约掉一个 $e^x$，得到 $\\frac{u^2+1}{u^4+1}du$。分母分解成 $(u^2-\\sqrt2u+1)(u^2+\\sqrt2u+1)$，分式等于两个因式倒数之和的一半。配方后得 $\\frac1{\\sqrt2}[\\arctan(\\sqrt2u-1)+\\arctan(\\sqrt2u+1)]+C$。\n\n\\clearpage\n\n% SOURCE line=1588 pdf_page=246 section=3.3\n\n\\Question{289}{第5章 · 解答题 · 第 2 题}\n\n求下列不定积分： (I) $\\int \\frac{\\arctan\\sqrt{x}}{(1+x)\\sqrt{x}}dx$; (II) $\\int x^2\\sqrt{4-x^2}dx$; (III) $\\int \\frac{2x+1}{x^2+2x+5}dx$; (IV) $\\int \\frac{x^3}{\\sqrt{4+x^2}}dx$; (V) $\\int \\frac{1}{x^2}\\sqrt{\\frac{1-x}{1+x}}dx$;\n\n\\vfill\n\n\\Solution\n\n(I) 令 $u=\\arctan\\sqrt x$，则 $du=\\frac{dx}{2(1+x)\\sqrt x}$。原式是 $2u\\,du$，得 $(\\arctan\\sqrt x)^2+C$。\n\n(II) 令 $x=2\\sin t$、$t=\\arcsin\\frac x2$，得到 $16\\sin^2t\\cos^2t\\,dt=2(1-\\cos4t)\\,dt$，结果为 $2t-\\frac12\\sin4t+C$。\n\n(III) 分子拆成 $(2x+2)-1$，第一项是分母导数，第二项把分母配成 $(x+1)^2+4$。结果 $\\ln(x^2+2x+5)-\\frac12\\arctan\\frac{x+1}{2}+C$。\n\n(IV) 令 $u=\\sqrt{4+x^2}$，则 $du=\\frac{x}{u}dx$，余下的 $x^2=u^2-4$。积分得 $\\frac{u^3}{3}-4u+C$。\n\n(V) 根号取作新变量 $u=\\sqrt{\\frac{1-x}{1+x}}$，解出 $x=\\frac{1-u^2}{1+u^2}$。原式化为 $-\\frac{4u^2}{(1-u^2)^2}du$。把它写成 $-2[\\frac{d}{du}(\\frac{u}{1-u^2})-\\frac1{1-u^2}]du$，积分得 $-\\frac{2u}{1-u^2}+\\ln|\\frac{1+u}{1-u}|+C$。\n\n\\clearpage\n\n% SOURCE line=1595 pdf_page=247 section=3.3\n\n\\Question{290}{第5章 · 解答题 · 第 3 题}\n\n求下列不定积分： (I) $\\int \\frac{\\sin x}{\\sin x + 1} dx$; (II) $\\int \\frac{dx}{1 + 2\\tan x}$.\n\n\\vfill\n\n\\Solution\n\n(I) 先把分式拆成 $1-\\frac1{1+\\sin x}$。注意对 $\\frac{\\cos x}{1+\\sin x}$ 用商求导时，分子化成 $-\\sin x(1+\\sin x)-\\cos^2 x=-(1+\\sin x)$。因此答案为 $x+\\frac{\\cos x}{1+\\sin x}+C$。\n\n(II) 把 $\\tan x$ 写成 $\\frac{\\sin x}{\\cos x}$，原式为 $\\frac{\\cos x}{\\cos x+2\\sin x}dx$。分母的导数为 $2\\cos x-\\sin x$，而 $5\\cos x=2(2\\cos x-\\sin x)+(\\cos x+2\\sin x)$。所以\n\\[\nI=\\frac25\\ln|\\cos x+2\\sin x|+\\frac x5+C .\n\\]\n这两个结果分别在原被积函数有定义的区间上成立。\n\n\\clearpage\n\n"}

## tool · 2026-11-14T01:58:28Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T01:58:35Z




## tool · 2026-11-14T01:58:41Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"f3b604","wall_time_seconds":0.000011042,"exit_code":0,"original_token_count":3984,"output":"@@ 1600 3.3\n已知等式右边是 $xf(x)$ 的原函数，先求导得 $xf(x)=\\frac1{\\sqrt{1-x^2}}$。因此在题意可成立的区间 $-1<x<1$、$x\\ne0$ 上，$\\frac1{f(x)}=x\\sqrt{1-x^2}$。\n\n看到根号内的 $1-x^2$，旁边恰好有 $x\\,dx$，令 $u=1-x^2$，得到 $du=-2x\\,dx$，所以\n\\[\nI=-\\frac12\\int\\sqrt u\\,du=-\\frac13(1-x^2)^{\\frac32}+C.\n\\]\n对结果求导，指数带下来的因子与内层导数 $-2x$ 相乘，恢复 $x\\sqrt{1-x^2}$。\n@@ 1604 3.3\n先令 $u=x^2-1$，得到 $f(u)=\\ln\\frac{u+1}{u-1}$。按原等式的实数定义域，$x^2>2$，所以 $u>1$。因此\n\\[\n\\ln\\frac{\\varphi(x)+1}{\\varphi(x)-1}=\\ln x\n\\ \\Longrightarrow\\ \\varphi(x)+1=x(\\varphi(x)-1).\n\\]\n解出 $\\varphi(x)=\\frac{x+1}{x-1}=1+\\frac2{x-1}$。这一解满足 $\\varphi(x)>1$ 当且仅当 $x>1$。因此 $I=x+2\\ln(x-1)+C$。这里先解出 $\\varphi$，才能确定该积什么函数以及对数在哪个区间有意义。\n@@ 1608 3.3\n把等式中的 $\\ln x$ 看成新变量 $u$，得到 $f(u)=e^{-u}\\ln(1+e^u)$。积分时令 $t=e^u$，便得到 $\\int\\frac{\\ln(1+t)}{t^2}\\,dt$。对数求导后变成简单分式，适合分部：\n\\[\n-\\frac{\\ln(1+t)}t+\\int\\frac{dt}{t(1+t)}\n=-\\frac{\\ln(1+t)}t+\\ln t-\\ln(1+t)+C .\n\\]\n最后把 $t=e^x$ 代回，得 $x-(1+e^{-x})\\ln(1+e^x)+C$。求导时来自最后两个因子的常数项抵消，剩下 $e^{-x}\\ln(1+e^x)$。\n@@ 1612 3.3\n(I) 试设原函数为 $e^x R(x)$。取 $R(x)=\\frac{x-2}{x+2}$，则 $R+R'=\\frac{x^2}{(x+2)^2}$。故为 $\\frac{(x-2)e^x}{x+2}+C$。\n\n(II) 取 $u=\\ln x$、$dv=\\frac{dx}{(1-x)^2}$，得到 $\\frac{\\ln x}{1-x}-\\int\\frac{dx}{x(1-x)}$。拆分后为 $\\frac{\\ln x}{1-x}-\\ln x+\\ln|1-x|+C$。\n\n(III) 令 $t=\\sqrt{1+e^x}$，此时 $\\frac{e^x}{\\sqrt{1+e^x}}dx=2dt$。分部得 $2xt-2\\int t\\,dx$，再用 $dx=\\frac{2t}{t^2-1}dt$，结果 $2xt-4t-2\\ln|\\frac{t-1}{t+1}|+C$。\n\n(IV) 拆出 $\\frac1{x^2(1+x^2)}=\\frac1{x^2}-\\frac1{1+x^2}$。前一项对 $\\arctan x$ 分部，后一项直接换元。结果 $-\\frac{\\arctan x}{x}-\\frac12(\\arctan x)^2+\\ln|x|-\\frac12\\ln(1+x^2)+C$。\n\n(V) 取 $u=\\arctan\\sqrt x$、$dv=dx$。分部后剩下 $\\int\\frac{\\sqrt x}{2(1+x)}dx$，用 $t=\\sqrt x$ 化成 $\\int(1-\\frac1{1+t^2})dt$，故为 $(x+1)\\arctan\\sqrt x-\\sqrt x+C$。\n\n(VI) 令 $t=\\sqrt{e^x-1}$，得到 $\\int2t(1+t^2)\\arctan t\\,dt$。用 $u=\\arctan t$、$v=\\frac12(1+t^2)^2$ 分部，结果 $\\frac12(1+t^2)^2\\arctan t-\\frac t2-\\frac{t^3}{6}+C$。\n@@ 1619 3.2\n绝对值在 $x=0$ 改变写法。$x<0$ 时 $e^{-|x|}=e^x$，原函数是 $e^x+C_1$；$x>0$ 时 $e^{-|x|}=e^{-x}$，原函数是 $-e^{-x}+C_2$。要在全实轴得到可导的原函数，两边必须在 $0$ 连续。因此 $1+C_1=-1+C_2$。用公共的函数值 $C$ 表示，\n\\[\nI=C+\\begin{cases}e^x-1,&x<0,\\\\1-e^{-x},&x\\ge0.\\end{cases}\n\\]\n两侧导数在 $0$ 均趋于 $1$，而且连接处的差商也趋于 $1$，正好等于被积函数在 $0$ 的值。\n@@ 1623 3.3\n分母是 $x-1$ 的高次幂，直接令 $u=x-1$，使分子也用 $u$ 表示。$x^2=(u+1)^2=u^2+2u+1$，除以 $u^{100}$ 后得到 $u^{-98}+2u^{-99}+u^{-100}$。逐项使用幂函数积分公式，\n\\[\nI=-\\frac1{97(x-1)^{97}}-\\frac1{49(x-1)^{98}}-\\frac1{99(x-1)^{99}}+C.\n\\]\n三项求导后分子分别是 $1,2,1$，通分恢复 $(u+1)^2$。$x=1$ 两侧的常数可分别选取。\n@@ 1629 3.3\n积分区间以 $0$ 为中心，因此可以把每个 $x$ 和它的对称点 $-x$ 配成一对。具体地，设 $t=-x$，则 $dx=-dt$。$x$ 从 $-a$ 到 $a$ 时，$t$ 从 $a$ 到 $-a$，所以\n\\[\n\\int_{-a}^{a}f(-x)\\,dx=-\\int_a^{-a}f(t)\\,dt=\\int_{-a}^a f(t)\\,dt.\n\\]\n将原积分与这份同值的积分相加，左边变成原积分的两倍。利用积分的线性，再除以 $2$，便得所证。特别地，如果 $f$ 是奇函数，被加起来的两项处处相消。\n@@ 1636 3.1\n积分区间长为 $\\frac\\pi4$。如果能找出被积函数的最大、最小值，再乘区间长度，就能得到上下界。设 $h(x)=\\frac{\\sin x}{x}$，求导得\n\\[\nh'(x)=\\frac{x\\cos x-\\sin x}{x^2}.\n\\]\n令 $u(x)=x\\cos x-\\sin x$，有 $u(0)=0$ 且 $u'(x)=-x\\sin x<0$，因此 $h'<0$。两个端点值分别为 $\\frac{2\\sqrt2}{\\pi}$ 与 $\\frac2\\pi$。内部各点严格介于二者之间，乘区间长度 $\\frac\\pi4$ 即得 $\\frac12<I<\\frac{\\sqrt2}{2}$。\n@@ 1640 3.3\n(1) 对 $|x|>1$，$\\ln|x+\\sqrt{x^2-1}|$ 的导数是 $\\frac1{\\sqrt{x^2-1}}$。两端代入得 $\\ln(\\frac{\\sqrt2-1}{2-\\sqrt3})=\\ln[(\\sqrt2-1)(2+\\sqrt3)]$。\n\n(2) 令 $u=x-1$，根号变成 $\\sqrt{1-u^2}$，另一个因子变成 $\\frac32+\\frac u2$。奇函数项在 $[-1,1]$ 上积分为零，余下 $\\frac32$ 倍单位上半圆面积，得 $\\frac{3\\pi}4$。\n\n(3) 令 $t=\\arcsin x$ 消去根号，积分变为 $\\int_0^{\\frac\\pi2}t\\sin^2t\\,dt$。用 $\\sin^2t=\\frac{1-\\cos2t}2$，再分部算出 $\\int_0^{\\frac\\pi2}t\\cos2t\\,dt=-\\frac12$，所以答案 $\\frac{\\pi^2}{16}+\\frac14$。换元可先在 $x<1$ 的截断区间进行，再取上限趋于 $1$。\n\n(4) 令 $t=\\sqrt x$。因为 $\\sin(\\arctan t)=\\frac{t}{\\sqrt{1+t^2}}$，原反正弦等于 $\\arctan t$。分部得 $\\left[t^2\\arctan t-t+\\arctan t\\right]_0^{\\sqrt3}=\\frac{4\\pi}3-\\sqrt3$。\n@@ 1648 3.3\n两被积函数只把正弦和余弦互换，而 $x\\mapsto\\frac\\pi2-x$ 正好能作这个交换，积分区间仍相同。故两个积分相等，设共同值为 $I$。\n\n将两式相加，分子变成 $\\sin^3x+\\cos^3x$。利用立方和分解，恰好消掉分母：\n\\[\n2I=\\int_0^{\\frac\\pi2}(1-\\sin x\\cos x)\\,dx\n=\\frac\\pi2-\\frac12.\n\\]\n所以两个积分都等于 $\\frac\\pi4-\\frac14$。整个区间内 $\\sin x+\\cos x>0$，约分有效。\n@@ 1652 3.3\n题目只直接给了 $(0,\\pi)$ 上的 $f$，遇到 $x$ 在后面的区间就用题给递推每次减去 $\\pi$。当 $\\pi<x<2\\pi$，$f(x)=x-\\pi+\\sin x$。当 $2\\pi<x<3\\pi$，再代一次得到\n\\[\nf(x)=x-2\\pi+\\sin(x-\\pi)+\\sin x=x-2\\pi .\n\\]\n有限个端点的取值不改变积分。于是\n\\[\nI=\\int_\\pi^{2\\pi}(x-\\pi+\\sin x)\\,dx+\n\\int_{2\\pi}^{3\\pi}(x-2\\pi)\\,dx\n=\\frac{\\pi^2}2-2+\\frac{\\pi^2}2=\\pi^2-2.\n\\]\n@@ 1656 3.3\n已知 $[0,2]$ 上的积分，所求区间 $[1,3]$ 和它重叠一半。先分开重叠和新增部分，得到\n\\[\n\\int_1^3f(x)\\,dx-\\int_0^2f(x)\\,dx\n=\\int_2^3f(x)\\,dx-\\int_0^1f(x)\\,dx.\n\\]\n在第一项令 $x=t+2$，使两个区间都变为 $[0,1]$。此时题给关系 $f(t+2)-f(t)=t$ 正好能用，差等于 $\\int_0^1t\\,dt=\\frac12$。已知第二个总积分为零，所以所求为 $\\frac12$。\n@@ 1660 3.3\n积分含 $f''$ 而题目给了函数值和切线。想到分部积分，因为可以先把 $f''$ 积成 $f'$，再用端点值消去剩下的积分。切线斜率给出 $f'(2)=5$，过原点给出 $f(0)=0$，曲线上的点给出 $f(2)=4$。\n\\[\nI=[xf'(x)]_0^2-\\int_0^2f'(x)\\,dx\n=2f'(2)-[f(2)-f(0)]=10-4=6.\n\\]\n虽然 $f'(0)$ 没有给出，端点项中它乘以 $0$，因此无需再求。\n@@ 1664 3.3\n\\TextCorrection{按原页平方位于 $(x-1)$ 后的写法，将自变量括号明确为 $f'(x)=\\arcsin((x-1)^2)$。}\n只知道 $f'$ 时，不急着把它积成完整的 $f$。分部时用 $v=x-1$，令上端点 $v(1)=0$，下端点又有 $f(0)=0$，于是\n\\[\nI=\\int_0^1(1-x)f'(x)\\,dx\n=\\int_0^1(1-x)\\arcsin((1-x)^2)\\,dx.\n\\]\n令 $u=(1-x)^2$，因为 $du=-2(1-x)dx$，原积分化为 $\\frac12\\int_0^1\\arcsin u\\,du$。其原函数为 $u\\arcsin u+\\sqrt{1-u^2}$，两端代入得 $\\frac\\pi4-\\frac12$。\n@@ 1668 3.3\n分母 $\\pi-t$ 在右端点为零，但令 $u=\\pi-t$ 后，$\\frac{\\sin t}{\\pi-t}=\\frac{\\sin u}{u}\\to1$，可以连续延拓。这样便能用微积分基本定理得到 $f'(x)=\\frac{\\sin x}{\\pi-x}$。\n\n发现分母是 $\\pi-x$ 时，分部积分可选择 $v=x-\\pi$ 来抵消它。这一选择还让上端点乘以零，下端点 $f(0)=0$，所以\n\\[\nI=[(x-\\pi)f(x)]_0^\\pi-\\int_0^\\pi(x-\\pi)f'(x)\\,dx\n=\\int_0^\\pi\\sin x\\,dx=2.\n\\]\n@@ 1672 3.5\n先处理 $0$ 处的反常性。$\\frac{\\ln(1+t)}t\\to1$，故 $f$ 在 $0$ 附近有界，乘上 $\\frac1{\\sqrt x}$ 仍可积。先从 $\\varepsilon>0$ 开始分部，用 $v=2\\sqrt x$。当 $\\varepsilon\\to0^+$ 时端点积趋于零，且 $f(1)=0$，于是\n\\[\nI=-2\\int_0^1\\frac{\\ln(1+x)}{\\sqrt x}\\,dx\n=-4\\int_0^1\\ln(1+u^2)\\,du,\\qquad u=\\sqrt x.\n\\]\n再分部，$\\int_0^1\\ln(1+u^2)\\,du=\\ln2-2\\int_0^1(1-\\frac1{1+u^2})\\,du=\\ln2-2+\\frac\\pi2$。因此 $I=8-2\\pi-4\\ln2$。它为负，与 $f(x)<0$ 一致。\n@@ 1676 3.3\n给出的 $A$ 含 $\\cos x$，所求分子 $\\sin x\\cos x$ 可先改成 $\\frac12\\sin2x$。再令 $u=2x$，积分上下限变为 $0,\\pi$，分母也变为与已知一致的 $u+2$：\n\\[\nI=\\frac12\\int_0^\\pi \\frac{\\sin u}{u+2}\\,du .\n\\]\n要使 $\\sin u$ 变成 $\\cos u$，用分部积分，取 $dv=\\sin u\\,du$、$v=-\\cos u$，得\n\\[\nI=\\frac12\\left[-\\frac{\\cos u}{u+2}\\right]_0^\\pi-\n\\frac12\\int_0^\\pi\\frac{\\cos u}{(u+2)^2}\\,du\n=\\frac14+\\frac{1}{2(\\pi+2)}-\\frac A2.\n\\]\n@@ 1680 3.3\n要比较两个积分，先让变量和区间相同。令 $x=\\sin t$，得到 $a_n=\\int_0^{\\frac\\pi2}\\sin^n t\\cos^2t\\,dt=b_n-b_{n+2}$。接着对 $b_{n+2}=\\int\\sin^{n+1}t\\sin t\\,dt$ 分部，用 $v=-\\cos t$。两端乘积为零，故\n\\[\nb_{n+2}=(n+1)\\int_0^{\\frac\\pi2}\\sin^n t\\cos^2t\\,dt=(n+1)a_n.\n\\]\n合起来得 $b_n=(n+2)a_n$。$b_n>0$，故 $\\frac{a_n}{b_n}=\\frac1{n+2}\\to0$。换元和分部的作用是得到精确比值，避免对两个都趋小的量直接估计。\n@@ 1684 3.3\n分母为偶函数，$x\\cos x$ 为奇函数，奇函数部分在对称区间积分为零。剩下 $2x^2$ 恰与分母的根式共轭，因为\n\\[\nx^2=(1+\\sqrt{1-x^2})(1-\\sqrt{1-x^2}).\n\\]\n原式化为 $2\\int_{-1}^1(1-\\sqrt{1-x^2})\\,dx$。根式的图像是单位圆上半圆，其面积为 $\\frac\\pi2$；常数 $1$ 的积分为 $2$。因此 $I=4-\\pi$。分母在全区间至少为 $1$，约分不引入例外。\n@@ 1688 3.3\n直接积分含指数与三角的分式很复杂，但区间对称，可以把 $x$ 与 $-x$ 的贡献配对。设 $h(x)=\\frac{1}{1+e^{-x}}$，通分得 $h(x)+h(-x)=1$。又因 $\\cos^2(-x)=\\cos^2x$，所以\n\\[\n2I=\\int_{-\\frac\\pi2}^{\\frac\\pi2}\\cos^2x[h(x)+h(-x)]\\,dx\n=\\int_{-\\frac\\pi2}^{\\frac\\pi2}\\cos^2x\\,dx=\\frac\\pi2.\n\\]\n最后一步用 $\\cos^2x=\\frac{1+\\cos2x}{2}$，余弦项端点差为零。答案为 $\\frac\\pi4$。\n@@ 1692 3.2\n分别看两个变上限积分的奇偶性。第一项的被积函数 $f(t)\\cos t$ 是奇函数，令 $t=-u$ 后，换元的负号与奇函数的负号抵消，所以这项是偶函数。第二项被积函数 $\\frac1{1+t^2}$ 是偶函数，换元时只有一个负号，故这项是奇函数。第二项在 $x=1$ 处等于 $\\arctan1=\\frac\\pi4$，第一项在 $x=1$ 和 $x=-1$ 都等于 $\\pi-\\frac\\pi4=\\frac{3\\pi}4$。于是 $F(-1)=\\frac{3\\pi}4-\\frac\\pi4=\\frac\\pi2$。\n@@ 1696 3.3\n(1) 将负半段用 $x=-t$ 改写成正半段。由于 $g$ 为偶函数，两半合并后得到\n\\[\n\\int_{-a}^a f(x)g(x)\\,dx=\\int_0^a[f(t)+f(-t)]g(t)\\,dt=A\\int_0^a g(t)\\,dt.\n\\]\n(2) 取 $g(x)=|\\sin x|$，$f(x)=\\arctan e^x$。两个反正切的自变量互为倒数且都为正，因此 $\\arctan e^x+\\arctan e^{-x}=\\frac\\pi2$。例如对左边求导得零，在 $x=0$ 取值为 $\\frac\\pi2$。于是\n\\[\nI=\\frac\\pi2\\int_0^{\\frac\\pi2}\\sin x\\,dx=\\frac\\pi2.\n\\]\n@@ 1704 3.3\n先令 $u=x-1$，积分区间变为 $[-1,1]$，然后在分段点 $0$ 处分开。正半段积分为 $\\int_0^1\\frac{du}{1+u}=\\ln2$。负半段因 $\\frac1{1+e^u}=1-\\frac{e^u}{1+e^u}$，原函数为 $u-\\ln(1+e^u)$。故\n\\[\nI=[u-\\ln(1+e^u)]_{-1}^0+\\ln2\n=1+\\ln(1+e^{-1})=\\ln(1+e).\n\\]\n在 $u=0$ 处具体采用哪一段的函数值，不改变积分的值。\n@@ 1708 3.2\n绝对值的换号点在 $t=x$，但该点只有在 $0<x<1$ 时位于积分区间内部。此时\n\\[\nf(x)=\\int_0^x(x^2-t^2)\\,dt+\\int_x^1(t^2-x^2)\\,dt\n=\\frac43x^3-x^2+\\frac13.\n\\]\n若 $x\\ge1$，整个区间都取 $x^2-t^2$，故 $f(x)=x^2-\\frac13$。求导分别得到 $2x(2x-1)$ 和 $2x$，两式在 $1$ 给出相同导数 $2$。于是 $f$ 在 $(0,\\frac12)$ 递减、在 $(\\frac12,+\\infty)$ 递增，最小值为 $f(\\frac12)=\\frac14$。\n@@ 1712 3.3\n先整理内层 $\\ln\\frac1x=-\\ln x$，余弦为偶函数，原函数等于 $\\cos(\\ln x)$。求导取绝对值，得 $\\frac{|\\sin(\\ln x)|}{x}$。正好有 $\\frac{dx}{x}=dt$，令 $t=\\ln x$ 后\n\\[\nI=\\int_{-2n\\pi}^{0}|\\sin t|\\,dt.\n\\]\n$|\\sin t|$ 的周期为 $\\pi$，每个完整周期的积分都是 $\\int_0^\\pi\\sin t\\,dt=2$。区间包含 $2n$ 个完整周期，因此 $I=4n$。\n@@ 1718 3.2\n两个积分的区间都缩到 $0$，可以分别用「区间的有向长度乘以被积函数在 $0$ 的极限」估计。具体地，被积函数连续延拓后，积分中值定理给出 $\\alpha(x)=5x A_x$、$\\beta(x)=\\sin x B_x$，其中 $A_x$、$B_x$ 是对应小区间内的函数值。\n\n由重要极限，$A_x\\to1$。另一方面，$\\ln((1+t)^{\\frac1t})=\\frac{\\ln(1+t)}t\\to1$，所以 $B_x\\to e$。因此\n\\[\n\\lim_{x\\to0}\\frac{\\alpha(x)}{\\beta(x)}\n=\\lim_{x\\to0}5\\frac{x}{\\sin x}\\frac{A_x}{B_x}=\\frac5e .\n\\]\n若 $x<0$，两个积分的有向长度均为负，公式同样适用。\n@@ 1722 3.2\n变量 $x^2$ 同时出现在上限和被积式。先设 $u=x^2$，写 $H(u)=u\\int_1^u e^{-t^2}dt-\\int_1^u t e^{-t^2}dt$。对 $u$ 求导时，两个上限带来的项恰好抵消，剩下 $H'(u)=\\int_1^u e^{-t^2}dt$。因此\n\\[\nf'(x)=2x\\int_1^{x^2}e^{-t^2}dt .\n\\]\n被积函数恒正，积分符号与 $x^2-1$ 相同。按 $-1,0,1$ 划分，导数符号依次为负、正、负、正。递增区间是 $(-1,0),(1,+\\infty)$，递减区间是 $(-\\infty,-1),(0,1)$。两处最小值 $f(\\pm1)=0$，局部极大值 $f(0)=\\int_0^1t e^{-t^2}dt=\\frac{1-e^{-1}}2$。\n@@ 1726 3.2\n发现 $x^2-t^2$ 的微分包含 $t\\,dt$，令 $u=x^2-t^2$。$t=0$ 对应 $u=x^2$，$t=x$ 对应 $u=0$，故对正负 $x$ 都有 $F(x)=\\frac12\\int_0^{x^2} f(u)\\,du$。\n\n$f(0)=0$、$f'(0)=1$ 意味着 $f(u)=u+o(u)$。给定 $\\varepsilon>0$，当 $x^2$ 足够小时，整个积分区间都有 $|f(u)-u|\\le\\varepsilon u$。积分误差至多为 $\\frac{\\varepsilon x^4}{4}$，而主项 $\\frac12\\int_0^{x^2}u\\,du=\\frac{x^4}{4}$。所以所求极限是 $\\frac14$。\n@@ 1730 3.2\n两个积分都在 $0$ 附近取 $f$ 的值。把 $t=xu$，就能同时消掉区间长度和分子额外的 $x-t$：\n\\[\n\\frac{\\int_0^x(x-t)f(t)dt}{x\\int_0^x f(x-t)dt}\n=\\frac{\\int_0^1 (1-u)f(xu)du}{\\int_0^1 f(x(1-u))du}.\n\\]\n虽然 $u$ 在整个 $[0,1]$ 内变化，$|xu|$、$|x(1-u)|$ 都不超过 $|x|$，故由连续性可将其中的 $f$ 用 $f(0)$ 逼近，误差在整个区间一致趋于零。分子趋于 $\\frac12 f(0)$，分母趋于非零的 $f(0)$，极限为 $\\frac12$。\n@@ 1734 3.2\n当 $x\\ne0$，用 $u=xt$ 把 $x$ 移到上限，得到 $F(x)=\\frac1x\\int_0^x f(u)\\,du$。按商求导，\n\\[\nF'(x)=\\frac{f(x)}x-\\frac1{x^2}\\int_0^x f(u)\\,du .\n\\]\n在 $0$ 处用定义。条件与连续性给出 $f(0)=0$，且 $f(u)=Au+o(u)$。对小区间内的误差用 $|f(u)-Au|\\le\\varepsilon |u|$ 估计，有 $\\int_0^x f(u)\\,du=\\frac A2x^2+o(x^2)$。因此 $F(0)=0$，差商给出 $F'(0)=\\frac A2$。前面 $x\\ne0$ 的公式趋于 $A-\\frac A2=\\frac A2$，所以 $F'$ 在 $0$ 连续。\n@@ 1738 3.2\n未知函数出现在积分上限中，可以对等式求导来消掉积分。由于 $g$ 是 $f$ 的反函数，$g(f(x))=x$。微积分基本定理与链式法则给出\n\\[\nx f'(x)=\\frac{x}{x+\\sqrt{a^2-x^2}},\\qquad 0<x<a .\n\\]\n除以 $x$，再用 $f(0)=0$ 得 $f(a)=\\int_0^a \\frac{dx}{x+\\sqrt{a^2-x^2}}$。令 $x=a\\sin t$，所得积分为 $\\int_0^{\\frac\\pi2}\\frac{\\cos t}{\\sin t+\\cos t}dt$。对称换元 $t\\mapsto\\frac\\pi2-t$ 给出一个相等、分子为 $\\sin t$ 的积分。相加后被积函数为 $1$，所以 $f(a)=\\frac\\pi4$。\n@@ 1742 2.5\n\\TextCorrection{按原页平方位于 $(u-t)$ 后的写法，将题干明确写成 $\\sin((u-t)^2)$。}\n先在内层令 $s=u-t$，于是内层为 $u^3-3\\int_0^u\\sin(s^2)ds$。分母为 $x^8$，先找分子八次项。Taylor 展开给出 $\\sin(s^2)=s^2-\\frac{s^6}{6}+O(s^{10})$。首项积分后正好抵消 $u^3$，所以\n\\[\nu^3-3\\int_0^u\\sin(s^2)\\,ds\n=\\frac{u^7}{14}+O(|u|^{11}).\n\\]\n再积一次得到分子 $\\frac{x^8}{112}+O(|x|^{12})$，故极限为 $\\frac1{112}$。展开时先看清正弦的自变量是 $(u-t)^2$，再逐层积分；分母的八次幂提示前面的低次项将相消。\n"}
{"chunk_id":"ac79da","wall_time_seconds":0.000017375,"exit_code":0,"original_token_count":1906,"output":"% SOURCE line=1742 pdf_page=279 section=2.5\n\n\\Question{186}{第6章 · 例题第2组 · 例 7}\n\n求$\\lim_{x\\to0}\\frac{\\int_{0}^{x}\\mathrm{d}u\\int_{0}^{u}[u^{2}-3\\sin((u-t)^{2})]\\mathrm{d}t}{x^{8}}$.\n\n\\vfill\n\n\n% SOURCE line=1636 pdf_page=255 section=3.1\n\n\\Question{226}{第6章 · 例题第1组 · 例 1}\n\n证明:不等式$\\frac{1}{2}<\\int_{\\frac{\\pi}{4}}^{\\frac{\\pi}{2}}\\frac{\\sin x}{x}dx<\\frac{\\sqrt{2}}{2}$.\n\n\\vfill\n\n\n% SOURCE line=1746 pdf_page=280 section=3.1\n\n\\Question{227}{第6章 · 例题第2组 · 例 8}\n\n求$\\lim_{t\\to0^{+}}\\frac{1}{1-\\mathrm{e}^{-t^{2}}}\\int_{0}^{t}\\mathrm{d}x\\int_{t}^{x}\\mathrm{e}^{-(x-y)^{2}}\\mathrm{d}y$.\n\n\\vfill\n\n\n% SOURCE line=1619 pdf_page=252 section=3.2\n\n\\Question{253}{第5章 · 解答题 · 第 8 题}\n\n求 $I = \\int e^{-|x|} \\, dx$.\n\n\\vfill\n\n\n% SOURCE line=1692 pdf_page=268 section=3.2\n\n\\Question{254}{第6章 · 例题第1组 · 例 14}\n\n设 $f(x)$ 为连续的奇函数，$F(x)=\\int_{0}^{x}f(t)\\cos tdt+\\int_{0}^{x}\\frac{dt}{1+t^{2}}$，且 $F(1)=\\pi$，求 $F(-1)$.\n\n\\vfill\n\n\n% SOURCE line=1708 pdf_page=271 section=3.2\n\n\\Question{255}{第6章 · 例题第1组 · 例 17}\n\n设 $f(x)=\\int_{0}^{1}\\left|t^{2}-x^{2}\\right|\\mathrm{d}t(x>0)$，求 $f'(x)$ 的表达式和 $f(x)$ 的最小值.\n\n\\vfill\n\n\n% SOURCE line=1718 pdf_page=273 section=3.2\n\n\\Question{256}{第6章 · 例题第2组 · 例 1}\n\n设 $\\alpha(x)=\\int_{0}^{5x}\\frac{\\sin t}{t}dt,\\beta(x)=\\int_{0}^{\\sin x}(1+t)^{\\frac{1}{t}}dt$ ，求 $\\lim_{x\\to0}\\frac{\\alpha(x)}{\\beta(x)}$\n\n\\vfill\n\n\n% SOURCE line=1722 pdf_page=274 section=3.2\n\n\\Question{257}{第6章 · 例题第2组 · 例 2}\n\n求 $f(x)=\\int_{1}^{x^{2}}(x^{2}-t)e^{-t^{2}}dt$ 的单调区间和极值.\n\n\\vfill\n\n\n% SOURCE line=1726 pdf_page=275 section=3.2\n\n\\Question{258}{第6章 · 例题第2组 · 例 3}\n\n设 $F(x)=\\int_{0}^{x}tf(x^{2}-t^{2})dt$，其中 $f(x)$ 在 x=0 的某邻域内连续，且 $f(0)=0,f'(0)=1$，求 $\\lim_{x\\to0}\\frac{F(x)}{x^{4}}$.\n\n\\vfill\n\n\n% SOURCE line=1730 pdf_page=276 section=3.2\n\n\\Question{259}{第6章 · 例题第2组 · 例 4}\n\n设 $f(x)$ 连续，且 $f(0) \\neq 0$，求 $\\lim_{x \\to 0} \\frac{\\int_{0}^{x}(x-t)f(t)dt}{x\\int_{0}^{x} f(x-t)dt}$.\n\n\\vfill\n\n\n% SOURCE line=1734 pdf_page=277 section=3.2\n\n\\Question{260}{第6章 · 例题第2组 · 例 5}\n\n设 $f(x)$ 连续, $F(x)=\\int_{0}^{1}f(xt)dt$, 且 $\\lim_{x\\to0}\\frac{f(x)}{x}=A$, 求 $F'(x)$, 并讨论 $F'(x)$ 在 x=0 处的连续性.\n\n\\vfill\n\n\n% SOURCE line=1738 pdf_page=278 section=3.2\n\n\\Question{261}{第6章 · 例题第2组 · 例 6}\n\n设 $f(x)$ 在 $[0,+\\infty)$ 上可导，$f(0)=0$，且 $f(x)$ 的反函数为 $g(x)$。若 $\\int_{0}^{f(x)} g(t)dt = \\int_{0}^{x}\\frac{t}{t+\\sqrt{a^{2}-t^{2}}}dt (a>0)$，求 $f(a)$。\n\n\\vfill\n\n\n% SOURCE line=1600 pdf_page=248 section=3.3\n\n\\Question{291}{第5章 · 解答题 · 第 4 题}\n\n设 $\\int x f(x) \\, \\mathrm{d}x = \\arcsin x + C$ (C 为任意常数)，计算 $I = \\int \\frac{1}{f(x)} \\, \\mathrm{d}x$.\n\n\\vfill\n\n\n% SOURCE line=1604 pdf_page=249 section=3.3\n\n\\Question{292}{第5章 · 解答题 · 第 5 题}\n\n设 $f(x^{2}-1)=\\ln\\frac{x^{2}}{x^{2}-2}$，且 $f[\\varphi(x)]=\\ln x$，求 $I=\\int\\varphi(x)\\mathrm{d}x$.\n\n\\vfill\n\n\n% SOURCE line=1608 pdf_page=250 section=3.3\n\n\\Question{293}{第5章 · 解答题 · 第 6 题}\n\n设 $f(\\ln x) = \\frac{\\ln(1+x)}{x}$，求 $I=\\int f(x)dx$.\n\n\\vfill\n\n\n% SOURCE line=1612 pdf_page=251 section=3.3\n\n\\Question{294}{第5章 · 解答题 · 第 7 题}\n\n求下列不定积分: (I) $\\int \\frac{x^{2} e^{x}}{(x+2)^{2}} dx$; (II) $\\int \\frac{\\ln x}{(1-x)^{2}} dx$; (III) $\\int \\frac{x e^{x}}{\\sqrt{1+e^{x}}} dx$; (IV) $\\int \\frac{\\arctan x}{x^{2}(1+x^{2})} dx$; (V) $\\int \\arctan \\sqrt{x} dx$; (VI) $\\int e^{2x} \\arctan \\sqrt{e^{x}-1} dx$.\n\n\\vfill\n\n\n% SOURCE line=1623 pdf_page=253 section=3.3\n\n\\Question{295}{第5章 · 解答题 · 第 9 题}\n\n计算 $I=\\int\\frac{x^{2}}{(x-1)^{100}}dx$.\n\n\\vfill\n\n\n% SOURCE line=1629 pdf_page=254 section=3.3\n\n\\Question{296}{第6章 · 示例 · 示例}\n\n证明： $\\int_{-a}^{a}f(x)dx=\\frac{1}{2}\\int_{-a}^{a}[f(x)+f(-x)]dx$\n\n\\vfill\n\n\n% SOURCE line=1640 pdf_page=256 section=3.3\n\n\\Question{297}{第6章 · 例题第1组 · 例 2}\n\n计算下列定积分：\n\n(1) $\\int_{-2}^{-\\sqrt{2}}\\frac{\\mathrm{d}x}{\\sqrt{x^{2}-1}}$; (2) $\\int_{0}^{2}\\left(1+\\frac{x}{2}\\right)\\sqrt{2x-x^{2}}\\mathrm{d}x$;\n\n(3) $\\int_{0}^{1}\\frac{x^{2}\\arcsin x}{\\sqrt{1-x^{2}}}\\mathrm{d}x$; (4) $\\int_{0}^{3}\\arcsin\\sqrt{\\frac{x}{1+x}}\\mathrm{d}x$.\n\n\\vfill\n\n\n% SOURCE line=1648 pdf_page=257 section=3.3\n\n\\Question{298}{第6章 · 例题第1组 · 例 3}\n\n证明：$\\int_{0}^{\\frac{\\pi}{2}}\\frac{\\sin^{3}x}{\\sin x+\\cos x}dx=\\int_{0}^{\\frac{\\pi}{2}}\\frac{\\cos^{3}x}{\\sin x+\\cos x}dx$，并求其值.\n\n\\vfill\n\n\n% SOURCE line=1652 pdf_page=258 section=3.3\n\n\\Question{299}{第6章 · 例题第1组 · 例 4}\n\n设 $f(x)$ 在 $(-\\infty,+\\infty)$ 内满足 $f(x)=f(x-\\pi)+\\sin x$，且 $f(x)=x,x\\in(0,\\pi)$，求 $I=\\int_{\\pi}^{3\\pi}f(x)dx$.\n\n\\vfill\n\n\n% SOURCE line=1656 pdf_page=259 section=3.3\n\n\\Question{300}{第6章 · 例题第1组 · 例 5}\n\n设连续函数 $f(x)$ 满足 $f(x+2)-f(x)=x$, $\\int_{0}^{2}f(x)dx=0$, 求 $\\int_{1}^{3}f(x)dx$.\n\n\\vfill\n\n\n% SOURCE line=1660 pdf_page=260 section=3.3\n\n\\Question{301}{第6章 · 例题第1组 · 例 6}\n\n设过原点的曲线 $y = f(x)$ 在其上一点 $(2,4)$ 处的切线方程为 $y = 5x - 6$，且 $f''(x)$ 连续，计算 $\\mathrm{I} = \\int_{0}^{2} x f''(x) \\, dx$.\n\n\\vfill\n\n\n% SOURCE line=1664 pdf_page=261 section=3.3\n\n\\Question{302}{第6章 · 例题第1组 · 例 7}\n\n设 $f'(x) = \\arcsin((x-1)^2)$，且 $f(0) = 0$，求 $I = \\int_0^1 f(x) \\, dx$。\n\n\\vfill\n\n\n% SOURCE line=1668 pdf_page=262 section=3.3\n\n\\Question{303}{第6章 · 例题第1组 · 例 8}\n\n设 $f(x)=\\int_{0}^{x}\\frac{\\sin t}{\\pi-t}dt$，求 $I=\\int_{0}^{\\pi}f(x)dx$。\n\n\\vfill\n\n\n% SOURCE line=1676 pdf_page=264 section=3.3\n\n\\Question{304}{第6章 · 例题第1组 · 例 10}\n\n设$\\int_{0}^{\\pi}\\frac{\\cos x}{(x+2)^{2}}$dx=A，计算$I=\\int_{0}^{\\frac{\\pi}{2}}\\frac{\\sin x\\cos x}{x+1}$dx.\n\n\\vfill\n\n\n% SOURCE line=1680 pdf_page=265 section=3.3\n\n\\Question{305}{第6章 · 例题第1组 · 例 11}\n\n设 $a_{n}=\\int_{0}^{1}x^{n}\\sqrt{1-x^{2}}dx$, $b_{n}=\\int_{0}^{\\frac{\\pi}{2}}\\sin^{n}tdt$ ($n=1,2,\\cdots$)，证明：$\\lim_{n\\to\\infty}\\frac{a_{n}}{b_{n}}=0$\n\n\\vfill\n\n\n% SOURCE line=1684 pdf_page=266 section=3.3\n\n\\Question{306}{第6章 · 例题第1组 · 例 12}\n\n计算 $I=\\int_{-1}^{1}\\frac{2x^{2}+x\\cos x}{1+\\sqrt{1-x^{2}}}$ dx.\n\n\\vfill\n\n\n% SOURCE line=1688 pdf_page=267 section=3.3\n\n\\Question{307}{第6章 · 例题第1组 · 例 13}\n\n计算 $I=\\int_{-\\frac{\\pi}{2}}^{\\frac{\\pi}{2}}\\frac{\\cos^{2}x}{1+e^{-x}}dx$.\n\n\\vfill\n\n\n% SOURCE line=1696 pdf_page=269 section=3.3\n\n\\Question{308}{第6章 · 例题第1组 · 例 15}\n\n设 $f(x), g(x)$ 在 $[-a, a]$ ($a > 0$) 上连续，$g(x)$ 为偶函数，且 $f(x) + f(-x) = A$ ($A$ 为常数).\n\n(1) 证明：$\\int_{-a}^{a}f(x)g(x)dx = A\\int_{0}^{a}g(x)dx;$\n\n(2) 利用(1) 的结论计算 $I=\\int_{-\\frac{\\pi}{2}}^{\\frac{\\pi}{2}}|\\sin x|\\arctan e^{x}dx$.\n\n\\vfill\n\n\n% SOURCE line=1704 pdf_page=270 section=3.3\n\n\\Question{309}{第6章 · 例题第1组 · 例 16}\n\n求 $I=\\int_{0}^{2}f(x-1)dx$，其中 $f(x)=\\left\\{\\begin{aligned}&\\frac{1}{1+x},&x\\geqslant0,\\\\&\\frac{1}{1+e^{x}},&x<0.\\end{aligned}\\right.$\n\n\\vfill\n\n\n% SOURCE line=1712 pdf_page=272 section=3.3\n\n\\Question{310}{第6章 · 例题第1组 · 例 18}\n\n求 $I=\\int_{e^{-2n\\pi}}^{1}\\left|\\frac{d}{dx}\\cos\\left(\\ln\\frac{1}{x}\\right)\\right|dx,n$ 为正整数.\n\n\\vfill\n\n\n% SOURCE line=1672 pdf_page=263 section=3.5\n\n\\Question{336}{第6章 · 例题第1组 · 例 9}\n\n设 $f(x)=\\int_{1}^{x}\\frac{\\ln(t+1)}{t}dt$，求 $I=\\int_{0}^{1}\\frac{f(x)}{\\sqrt{x}}dx$.\n\n\\vfill\n\n\n"}

## tool · 2026-11-14T02:00:34Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T02:00:40Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"2934c7","wall_time_seconds":0.000009541,"exit_code":0,"original_token_count":2838,"output":"@@ 1692 3.2\n分别看两个变上限积分的奇偶性。第一项的被积函数 $f(t)\\cos t$ 是奇函数，令 $t=-u$ 后，换元的负号与奇函数的负号抵消，所以这项是偶函数。第二项被积函数 $\\frac1{1+t^2}$ 是偶函数，换元时只有一个负号，故这项是奇函数。第二项在 $x=1$ 处等于 $\\arctan1=\\frac\\pi4$，第一项在 $x=1$ 和 $x=-1$ 都等于 $\\pi-\\frac\\pi4=\\frac{3\\pi}4$。于是 $F(-1)=\\frac{3\\pi}4-\\frac\\pi4=\\frac\\pi2$。\n@@ 1696 3.3\n(1) 将负半段用 $x=-t$ 改写成正半段。由于 $g$ 为偶函数，两半合并后得到\n\\[\n\\int_{-a}^a f(x)g(x)\\,dx=\\int_0^a[f(t)+f(-t)]g(t)\\,dt=A\\int_0^a g(t)\\,dt.\n\\]\n(2) 取 $g(x)=|\\sin x|$，$f(x)=\\arctan e^x$。两个反正切的自变量互为倒数且都为正，因此 $\\arctan e^x+\\arctan e^{-x}=\\frac\\pi2$。例如对左边求导得零，在 $x=0$ 取值为 $\\frac\\pi2$。于是\n\\[\nI=\\frac\\pi2\\int_0^{\\frac\\pi2}\\sin x\\,dx=\\frac\\pi2.\n\\]\n@@ 1704 3.3\n先令 $u=x-1$，积分区间变为 $[-1,1]$，然后在分段点 $0$ 处分开。正半段积分为 $\\int_0^1\\frac{du}{1+u}=\\ln2$。负半段因 $\\frac1{1+e^u}=1-\\frac{e^u}{1+e^u}$，原函数为 $u-\\ln(1+e^u)$。故\n\\[\nI=[u-\\ln(1+e^u)]_{-1}^0+\\ln2\n=1+\\ln(1+e^{-1})=\\ln(1+e).\n\\]\n在 $u=0$ 处具体采用哪一段的函数值，不改变积分的值。\n@@ 1708 3.2\n绝对值的换号点在 $t=x$，但该点只有在 $0<x<1$ 时位于积分区间内部。此时\n\\[\nf(x)=\\int_0^x(x^2-t^2)\\,dt+\\int_x^1(t^2-x^2)\\,dt\n=\\frac43x^3-x^2+\\frac13.\n\\]\n若 $x\\ge1$，整个区间都取 $x^2-t^2$，故 $f(x)=x^2-\\frac13$。求导分别得到 $2x(2x-1)$ 和 $2x$，两式在 $1$ 给出相同导数 $2$。于是 $f$ 在 $(0,\\frac12)$ 递减、在 $(\\frac12,+\\infty)$ 递增，最小值为 $f(\\frac12)=\\frac14$。\n@@ 1712 3.3\n先整理内层 $\\ln\\frac1x=-\\ln x$，余弦为偶函数，原函数等于 $\\cos(\\ln x)$。求导取绝对值，得 $\\frac{|\\sin(\\ln x)|}{x}$。正好有 $\\frac{dx}{x}=dt$，令 $t=\\ln x$ 后\n\\[\nI=\\int_{-2n\\pi}^{0}|\\sin t|\\,dt.\n\\]\n$|\\sin t|$ 的周期为 $\\pi$，每个完整周期的积分都是 $\\int_0^\\pi\\sin t\\,dt=2$。区间包含 $2n$ 个完整周期，因此 $I=4n$。\n@@ 1718 3.2\n两个积分的区间都缩到 $0$，可以分别用「区间的有向长度乘以被积函数在 $0$ 的极限」估计。具体地，被积函数连续延拓后，积分中值定理给出 $\\alpha(x)=5x A_x$、$\\beta(x)=\\sin x B_x$，其中 $A_x$、$B_x$ 是对应小区间内的函数值。\n\n由重要极限，$A_x\\to1$。另一方面，$\\ln((1+t)^{\\frac1t})=\\frac{\\ln(1+t)}t\\to1$，所以 $B_x\\to e$。因此\n\\[\n\\lim_{x\\to0}\\frac{\\alpha(x)}{\\beta(x)}\n=\\lim_{x\\to0}5\\frac{x}{\\sin x}\\frac{A_x}{B_x}=\\frac5e .\n\\]\n若 $x<0$，两个积分的有向长度均为负，公式同样适用。\n@@ 1722 3.2\n变量 $x^2$ 同时出现在上限和被积式。先设 $u=x^2$，写 $H(u)=u\\int_1^u e^{-t^2}dt-\\int_1^u t e^{-t^2}dt$。对 $u$ 求导时，两个上限带来的项恰好抵消，剩下 $H'(u)=\\int_1^u e^{-t^2}dt$。因此\n\\[\nf'(x)=2x\\int_1^{x^2}e^{-t^2}dt .\n\\]\n被积函数恒正，积分符号与 $x^2-1$ 相同。按 $-1,0,1$ 划分，导数符号依次为负、正、负、正。递增区间是 $(-1,0),(1,+\\infty)$，递减区间是 $(-\\infty,-1),(0,1)$。两处最小值 $f(\\pm1)=0$，局部极大值 $f(0)=\\int_0^1t e^{-t^2}dt=\\frac{1-e^{-1}}2$。\n@@ 1726 3.2\n发现 $x^2-t^2$ 的微分包含 $t\\,dt$，令 $u=x^2-t^2$。$t=0$ 对应 $u=x^2$，$t=x$ 对应 $u=0$，故对正负 $x$ 都有 $F(x)=\\frac12\\int_0^{x^2} f(u)\\,du$。\n\n$f(0)=0$、$f'(0)=1$ 意味着 $f(u)=u+o(u)$。给定 $\\varepsilon>0$，当 $x^2$ 足够小时，整个积分区间都有 $|f(u)-u|\\le\\varepsilon u$。积分误差至多为 $\\frac{\\varepsilon x^4}{4}$，而主项 $\\frac12\\int_0^{x^2}u\\,du=\\frac{x^4}{4}$。所以所求极限是 $\\frac14$。\n@@ 1730 3.2\n两个积分都在 $0$ 附近取 $f$ 的值。把 $t=xu$，就能同时消掉区间长度和分子额外的 $x-t$：\n\\[\n\\frac{\\int_0^x(x-t)f(t)dt}{x\\int_0^x f(x-t)dt}\n=\\frac{\\int_0^1 (1-u)f(xu)du}{\\int_0^1 f(x(1-u))du}.\n\\]\n虽然 $u$ 在整个 $[0,1]$ 内变化，$|xu|$、$|x(1-u)|$ 都不超过 $|x|$，故由连续性可将其中的 $f$ 用 $f(0)$ 逼近，误差在整个区间一致趋于零。分子趋于 $\\frac12 f(0)$，分母趋于非零的 $f(0)$，极限为 $\\frac12$。\n@@ 1734 3.2\n当 $x\\ne0$，用 $u=xt$ 把 $x$ 移到上限，得到 $F(x)=\\frac1x\\int_0^x f(u)\\,du$。按商求导，\n\\[\nF'(x)=\\frac{f(x)}x-\\frac1{x^2}\\int_0^x f(u)\\,du .\n\\]\n在 $0$ 处用定义。条件与连续性给出 $f(0)=0$，且 $f(u)=Au+o(u)$。对小区间内的误差用 $|f(u)-Au|\\le\\varepsilon |u|$ 估计，有 $\\int_0^x f(u)\\,du=\\frac A2x^2+o(x^2)$。因此 $F(0)=0$，差商给出 $F'(0)=\\frac A2$。前面 $x\\ne0$ 的公式趋于 $A-\\frac A2=\\frac A2$，所以 $F'$ 在 $0$ 连续。\n@@ 1738 3.2\n未知函数出现在积分上限中，可以对等式求导来消掉积分。由于 $g$ 是 $f$ 的反函数，$g(f(x))=x$。微积分基本定理与链式法则给出\n\\[\nx f'(x)=\\frac{x}{x+\\sqrt{a^2-x^2}},\\qquad 0<x<a .\n\\]\n除以 $x$，再用 $f(0)=0$ 得 $f(a)=\\int_0^a \\frac{dx}{x+\\sqrt{a^2-x^2}}$。令 $x=a\\sin t$，所得积分为 $\\int_0^{\\frac\\pi2}\\frac{\\cos t}{\\sin t+\\cos t}dt$。对称换元 $t\\mapsto\\frac\\pi2-t$ 给出一个相等、分子为 $\\sin t$ 的积分。相加后被积函数为 $1$，所以 $f(a)=\\frac\\pi4$。\n@@ 1742 2.5\n\\TextCorrection{按原页平方位于 $(u-t)$ 后的写法，将题干明确写成 $\\sin((u-t)^2)$。}\n先在内层令 $s=u-t$，于是内层为 $u^3-3\\int_0^u\\sin(s^2)ds$。分母为 $x^8$，先找分子八次项。Taylor 展开给出 $\\sin(s^2)=s^2-\\frac{s^6}{6}+O(s^{10})$。首项积分后正好抵消 $u^3$，所以\n\\[\nu^3-3\\int_0^u\\sin(s^2)\\,ds\n=\\frac{u^7}{14}+O(|u|^{11}).\n\\]\n再积一次得到分子 $\\frac{x^8}{112}+O(|x|^{12})$，故极限为 $\\frac1{112}$。展开时先看清正弦的自变量是 $(u-t)^2$，再逐层积分；分母的八次幂提示前面的低次项将相消。\n@@ 1746 3.1\n先留意内积分下限 $t$ 大于上限 $x$，因此带负号。对 $0\\le x\\le y\\le t$，有 $0\\le(y-x)^2\\le t^2$，从而 $e^{-t^2}\\le e^{-(x-y)^2}\\le1$。翻转内积分方向后，再乘回负号得\n\\[\n-\\frac{t^2}{2}\\le\n\\int_0^t dx\\int_t^x e^{-(x-y)^2}\\,dy\n\\le -e^{-t^2}\\frac{t^2}{2},\n\\]\n这里 $\\int_0^t(t-x)\\,dx=\\frac{t^2}2$。分母 $1-e^{-t^2}>0$ 且与 $t^2$ 等价，两个端点除以分母都趋于 $-\\frac12$。由夹逼准则即得答案。只用一元积分的逐次估计。\n@@ 1752 3.1\n把要证的式子移项并拆开 $[0,b]$，目标等价于\n\\[\n(b-a)\\int_0^a f(x)\\,dx \\ \\ge\\ a\\int_a^b f(x)\\,dx .\n\\]\n左右各自除以 $a(b-a)>0$ 后，恰好比较前后两个区间的平均值。由单调减少，前半段每个函数值至少为 $f(a)$，所以左边积分至少为 $a f(a)$。后半段每个函数值至多为 $f(a)$，所以右边积分至多为 $(b-a)f(a)$。分别乘回正的区间长度就得到不等式。这一思路对负值函数同样成立。\n@@ 1756 3.3\n看到 $gf'$ 和 $fg'$，想到乘积导数 $(fg)'=f'g+fg'$。为配成相同区间，把第二个积分在 $a$ 处分开。左边于是化为\n\\[\n[f(x)g(x)]_0^a+\\int_a^1 f(x)g'(x)\\,dx\n= f(a)g(a)+\\int_a^1 f(x)g'(x)\\,dx .\n\\]\n$f'\\ge0$ 保证 $x\\ge a$ 时 $f(x)\\ge f(a)$，且 $g'\\ge0$，所以末项至少为 $f(a)\\int_a^1g'(x)\\,dx=f(a)[g(1)-g(a)]$。与前项相加得到 $f(a)g(1)$。证明不需要假定 $g$ 为正。\n@@ 1760 1.2\n证明数列收敛，可以同时找单调性和下界。相邻两项相减，只剩一项和一个单位区间积分：\n\\[\na_{n+1}-a_n=f(n+1)-\\int_n^{n+1}f(x)\\,dx\\le0,\n\\]\n因为在 $[n,n+1]$ 上，$f(x)\\ge f(n+1)$。要找下界，将 $\\int_1^n f(x)\\,dx$ 按整数拆开。在 $[k,k+1]$ 上 $f(x)\\le f(k)$，于是 $\\int_1^n f(x)\\,dx\\le\\sum_{k=1}^{n-1} f(k)$。所以 $a_n\\ge f(n)\\ge0$。由单调有界准则，$a_n$ 有有限极限。\n@@ 1764 3.5\n先看收敛性。$x\\to0^+$ 时，$\\ln(\\sin x)=\\ln x+\\ln(\\frac{\\sin x}{x})$，第二项趋于零，而 $\\ln x$ 的反常积分收敛，因为 $x\\ln x-x\\to0$。同理 $\\ln(\\cot x)=\\ln(\\cos x)-\\ln(\\sin x)$ 也可积。\n\n在 $0<x<\\frac\\pi4$ 上，$0<\\sin x<\\cos x<1$，因此 $a<c<0$。此外 $\\cot x>1$，所以 $b>0$。合并得到 $a<c<b$，选 \\textbf{B}。可以先在 $[\\varepsilon,\\frac\\pi4]$ 比较，再令 $\\varepsilon\\to0^+$。\n@@ 1776 3.1\n正弦函数每隔 $\\pi$ 变号。将三段都平移到 $[0,\\pi]$，设\n\\[\nJ_k=\\int_0^\\pi e^{(x+k\\pi)^2}\\sin x\\,dx,\\qquad k=0,1,2 .\n\\]\n因 $x$ 在正半轴且 $\\sin x$ 在内部为正，随 $k$ 增大被积式严格增大，所以 $0<J_0<J_1<J_2$。原积分依次为 $I_1=J_0$、$I_2=J_0-J_1$、$I_3=J_0-J_1+J_2$。这样 $I_2<I_1$，且 $I_3-I_1=J_2-J_1>0$，即 $I_2<I_1<I_3$，选 \\textbf{D}。\n@@ 1788 3.1\n两个端点的函数值都是零。$|f'|\\le M$ 的意思是，离哪个端点较近，就能从哪个端点得到更好的界。对 $0,x$ 用 Lagrange 中值定理得 $|f(x)|\\le Mx$，对 $x,1$ 使用则得 $|f(x)|\\le M(1-x)$。取较小者，再积分：\n\\[\n\\left|\\int_0^1 f(x)\\,dx\\right|\n\\le M\\left(\\int_0^{\\frac12}x\\,dx+\\int_{\\frac12}^1(1-x)\\,dx\\right)\n=M\\left(\\frac18+\\frac18\\right)=\\frac M4 .\n\\]\n只使用一个端点时上界为 $\\frac M2$，取最近端点正好让估计更紧。\n@@ 1792 3.1\n(1) $|\\cos t|$ 的周期为 $\\pi$。一个周期内，把 $[\\frac\\pi2,\\pi]$ 的负余弦取相反数，总积分为 $2$，故 $s(n\\pi)=2n$。$s$ 随 $x$ 严格增加，因为任何非零长度区间里都有一段 $|\\cos t|>0$。于是 $2n\\le s(x)<2(n+1)$。\n\n(2) 取 $n$ 为满足 $n\\pi\\le x<(n+1)\\pi$ 的整数。把分子、分母分别用上述界估计，有\n\\[\n\\frac{2n}{(n+1)\\pi}\\le\\frac{s(x)}x\\le\\frac{2(n+1)}{n\\pi}.\n\\]\n$x\\to+\\infty$ 时 $n\\to+\\infty$，两端都趋于 $\\frac2\\pi$，由夹逼准则得到该极限。\n@@ 1800 3.3\n(1) 设左边为 $J$。令 $x=\\pi-u$，因 $\\sin(\\pi-u)=\\sin u$，得 $J=\\int_0^\\pi(\\pi-u)f(\\sin u)du$。与原式相加，两个一次因子之和恒为 $\\pi$，得所证。\n\n(2) 令 $C=\\int_{-\\pi}^{\\pi}f(t)\\sin t\\,dt$，它与自由变量 $x$ 无关。代入 $f(t)=\\frac{t}{1+\\cos^2t}+C$，常数项乘奇函数积分为零，另一项是偶函数，故\n\\[\nC=2\\int_0^\\pi t\\frac{\\sin t}{1+\\cos^2t}\\,dt\n=\\pi\\int_0^\\pi\\frac{\\sin t}{2-\\sin^2 t}\\,dt .\n\\]\n第二步用(1)，因为 $\\frac{\\sin t}{1+\\cos^2 t}$ 仅取决于 $\\sin t$。再令 $u=\\cos t$，得 $C=\\pi\\int_{-1}^1\\frac{du}{1+u^2}=\\frac{\\pi^2}2$。所以 $f(x)=\\frac{x}{1+\\cos^2x}+\\frac{\\pi^2}2$。\n@@ 1808 3.2\n周期性的定义是比较 $g(x+2)$ 与 $g(x)$。相减后，\n\\[\ng(x+2)-g(x)=2\\int_x^{x+2} f(t)\\,dt-2\\int_0^2 f(t)\\,dt.\n\\]\n要证明两个积分相等，只需令 $H(x)=\\int_x^{x+2}f(t)\\,dt$。由微积分基本定理，$H'(x)=f(x+2)-f(x)=0$，故 $H(x)$ 为常数，等于 $H(0)$。代回得 $g(x+2)=g(x)$，所以 $2$ 是 $g$ 的一个周期。题目无需确定最小正周期。\n@@ 1812 2.5\n(1) 一阶 Maclaurin 公式围绕 $0$ 展开。因为 $f(0)=0$，\n\\[\nf(x)=f'(0)x+\\frac12 f''(\\xi_x)x^2,\n\\]\n其中 $\\xi_x$ 在 $0$ 与 $x$ 之间。$x=0$ 时两边同为零。\n\n(2) 一次项是奇函数，在 $[-a,a]$ 上积分为零。注意 $\\xi_x$ 可能随 $x$ 变，先用 $f''$ 在闭区间的最小值 $m$、最大值 $M$ 夹住余项。因为 $x^2\\ge0$，\n\\[\n\\frac{ma^3}{3}\\le\\int_{-a}^a f(x)\\,dx\\le\\frac{Ma^3}{3}.\n\\]\n因此 $\\frac3{a^3}\\int_{-a}^a f(x)\\,dx$ 介于 $m,M$ 之间。$f''$ 连续，由介值定理可在某点 $\\eta$ 取到这个数，得结论。\n"}
{"chunk_id":"c7456f","wall_time_seconds":0.00001475,"exit_code":0,"original_token_count":901,"output":"% SOURCE line=1760 pdf_page=283 section=1.2\n\n\\Question{23}{第6章 · 例题第3组 · 例 3}\n\n设 $f(x)$ 是 $[0,+\\infty)$ 上单调减少且非负的连续函数，$a_{n}=\\sum_{k=1}^{n}f(k)-\\int_{1}^{n}f(x)dx$，证明：$\\lim_{n\\to\\infty}a_{n}$ 存在.\n\n\\vfill\n\n\n% SOURCE line=1812 pdf_page=290 section=2.5\n\n\\Question{187}{第6章 · 例题第3组 · 例 10}\n\n设 $f(x)$ 在 $[-a,a]$ ($a>0$) 上有二阶连续导数，且 $f(0)=0$.\n\n(1) 写出 $f(x)$ 带拉格朗日余项的一阶麦克劳林公式;\n\n(2) 证明: 至少存在一点 $\\eta \\in [-a, a]$, 使得 $a^{3} f''(\\eta) = 3 \\int_{-a}^{a} f(x) dx$.\n\n\\vfill\n\n\n% SOURCE line=1746 pdf_page=280 section=3.1\n\n\\Question{227}{第6章 · 例题第2组 · 例 8}\n\n求$\\lim_{t\\to0^{+}}\\frac{1}{1-\\mathrm{e}^{-t^{2}}}\\int_{0}^{t}\\mathrm{d}x\\int_{t}^{x}\\mathrm{e}^{-(x-y)^{2}}\\mathrm{d}y$.\n\n\\vfill\n\n\n% SOURCE line=1752 pdf_page=281 section=3.1\n\n\\Question{228}{第6章 · 例题第3组 · 例 1}\n\n设 $f(x)$ 在 $[0,+\\infty)$ 上连续且单调减少，证明：当 0 < a < b 时，有 $a \\int_{0}^{b} f(x) \\, dx \\leqslant b \\int_{0}^{a} f(x) \\, dx$.\n\n\\vfill\n\n\n% SOURCE line=1776 pdf_page=285 section=3.1\n\n\\Question{229}{第6章 · 例题第3组 · 例 5}\n\n设 $I_{k}=\\int_{0}^{k\\pi}e^{x^{2}}\\sin x\\,dx$ ($k=1,2,3$)，则（）.\n\n\\textbf{A.} $I_{1}<I_{2}<I_{3}$\n\n\\textbf{B.} $I_{3}<I_{2}<I_{1}$\n\n\\textbf{C.} $I_{2}<I_{3}<I_{1}$\n\n\\textbf{D.} $I_{2}<I_{1}<I_{3}$\n\n\\vfill\n\n\n% SOURCE line=1788 pdf_page=286 section=3.1\n\n\\Question{230}{第6章 · 例题第3组 · 例 6}\n\n设 $f(x)$ 在 $[0,1]$ 上有连续导数，且 $f(0)=f(1)=0$，证明：$\\left|\\int_{0}^{1}f(x)dx\\right|\\leqslant\\frac{M}{4}$，其中 $M=\\max_{0\\leqslant x\\leqslant1}\\left\\{\\left|f'(x)\\right|\\right\\}$.\n\n\\vfill\n\n\n% SOURCE line=1792 pdf_page=287 section=3.1\n\n\\Question{231}{第6章 · 例题第3组 · 例 7}\n\n设 $s(x)=\\int_{0}^{x}\\left|\\cos t\\right|\\mathrm{d}t.$\n\n(1) 当 n 为正整数，且 $n\\pi \\leqslant x < (n+1)\\pi$ 时，证明：$2n \\leqslant s(x) < 2(n+1)$.\n\n(2) 求 $\\lim_{x \\to +\\infty} \\frac{s(x)}{x}$.\n\n\\vfill\n\n\n% SOURCE line=1820 pdf_page=291 section=3.1\n\n\\Question{232}{第6章 · 例题第3组 · 例 11}\n\n设 $f(x)$ 在 $[0,\\pi]$ 上连续，且 $\\int_{0}^{\\pi}f(x)dx=\\int_{0}^{\\pi}f(x)\\cos xdx=0$，证明：在 $(0,\\pi)$ 内至少存在两个不同的点 $\\xi_{1},\\xi_{2}$，使得 $f(\\xi_{1})=f(\\xi_{2})=0$。\n\n\\vfill\n\n\n% SOURCE line=1808 pdf_page=289 section=3.2\n\n\\Question{262}{第6章 · 例题第3组 · 例 9}\n\n设 $f(x)$ 是以2为周期的连续函数，证明：$g(x)=\\int_{0}^{x}2f(t)dt-x\\int_{0}^{2}f(t)dt$ 以2为周期.\n\n\\vfill\n\n\n% SOURCE line=1756 pdf_page=282 section=3.3\n\n\\Question{311}{第6章 · 例题第3组 · 例 2}\n\n设 $f(x)$ 和 $g(x)$ 在 $[0,1]$ 上有连续导数，且 $f(0)=0, f'(x)\\geqslant0, g'(x)\\geqslant0$，证明：对任意 $a\\in[0,1]$，有 $\\int_{0}^{a}g(x)f'(x)dx+\\int_{0}^{1}f(x)g'(x)dx\\geqslant f(a)g(1)$.\n\n\\vfill\n\n\n% SOURCE line=1800 pdf_page=288 section=3.3\n\n\\Question{312}{第6章 · 例题第3组 · 例 8}\n\n设 $f(x)$ 在 $[-\\pi, \\pi]$ 上连续.\n\n(1) 证明: $\\int_{0}^{\\pi} x f(\\sin x) dx = \\frac{\\pi}{2} \\int_{0}^{\\pi} f(\\sin x) dx$.\n\n(2) 若 $f(x)=\\frac{x}{1+\\cos^{2}x}+\\int_{-\\pi}^{\\pi}f(x)\\sin x dx$，利用(1)的结论，求 $f(x)$.\n\n\\vfill\n\n\n% SOURCE line=1764 pdf_page=284 section=3.5\n\n\\Question{337}{第6章 · 例题第3组 · 例 4}\n\n设 $a=\\int_{0}^{\\frac{\\pi}{4}}\\ln(\\sin x)dx$, $b=\\int_{0}^{\\frac{\\pi}{4}}\\ln(\\cot x)dx$, $c=\\int_{0}^{\\frac{\\pi}{4}}\\ln(\\cos x)dx$, 则 a, b, c 的大小关系为().\n\n\\textbf{A.} $a < b < c$\n\n\\textbf{B.} a < c < b\n\n\\textbf{C.} b < a < c\n\n\\textbf{D.} c < b < a\n\n\\vfill\n\n\n"}

## tool · 2026-11-14T02:02:06Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T02:02:10Z




## tool · 2026-11-14T02:02:17Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"262c0d","wall_time_seconds":0.000010375,"exit_code":0,"original_token_count":2913,"output":"@@ 1820 3.1\n若 $f$ 在内部处处为零，结论直接成立。否则，第一条积分为零迫使 $f$ 在内部既取正值也取负值。由连续性，至少有一个零点。假设只有一个零点 $\\xi$，则 $f$ 在 $\\xi$ 两侧符号相反，且每一侧都不变号。\n\n为了与 $f$ 一同在 $\\xi$ 换号，构造 $h(x)=\\cos x-\\cos\\xi$。因余弦在 $(0,\\pi)$ 严格递减，$h$ 左正右负。因此 $f(x)h(x)$ 在两侧同号且均非零，积分不可能为零。然而两条已知积分关系给出 $\\int_0^\\pi f(x)h(x)dx=0$，矛盾，所以至少有两个不同的内部零点。\n@@ 1824 3.3\n(1) 周期性与偶性给出 $f(kT-x)=f(-x)=f(x)$。在积分中令 $x=kT-u$，再与原式相加，得到\n\\[\n2\\int_0^{kT}x f(x)\\,dx=kT\\int_0^{kT} f(x)\\,dx .\n\\]\n右边的积分由 $k$ 个完整周期组成，每段都等于 $\\int_0^T f(x)\\,dx$，所以得到所证的系数 $\\frac{k^2T}{2}$。\n\n(2) 取 $f(x)=|\\sin x|$，它是偶函数，周期为 $\\pi$。其一个周期的积分为 $\\int_0^\\pi\\sin x\\,dx=2$，代入 $T=\\pi,k=n$ 得 $I=n^2\\pi$。\n@@ 1832 3.3\n(1) 目标是把 $f$ 变成 $f''$。反过来从右侧积分做两次分部，使 $f''$ 每次降低一阶。设 $w(x)=x(x-1)$，有 $w(0)=w(1)=0$。第一次分部的边界项 $[wf']_0^1$ 消失，第二次的 $[w'f]_0^1$ 因 $f$ 两端为零也消失。故 $\\int_0^1 w f''=\\int_0^1w''f=2\\int_0^1f$。\n\n(2) 对等式取绝对值，将 $|f''|$ 换成上界 $M$。由于 $|w(x)|=x(1-x)$，\n\\[\n\\left|\\int_0^1 f(x)\\,dx\\right|\\le\n\\frac M2\\int_0^1x(1-x)\\,dx=\\frac M{12}.\n\\]\n@@ 1842 3.5\n左边是重要极限的变形。对幂取对数得 $ax\\ln(1+\\frac1x)\\to a$，故左边为 $e^a$。右边是无穷区间上的积分，先从有限的 $b$ 积到 $a$。对 $t e^t$ 分部，原函数为 $(t-1)e^t$。当 $b\\to-\\infty$，$(b-1)e^b\\to0$，因此右边为 $(a-1)e^a$。\n\n等式两边除以始终为正的 $e^a$，得 $1=a-1$，所以 $a=2$。代回，两边都等于 $e^2$。\n@@ 1846 3.5\n已知的是分母一次幂的积分，所求分母二次幂。分部积分时让 $\\frac1{x^2}$ 积成 $-\\frac1x$，就能降低分母次数。先在 $[\\varepsilon,R]$ 上计算，\n\\[\n\\int_\\varepsilon^R\\frac{\\sin^2 x}{x^2}\\,dx\n=\\left[-\\frac{\\sin^2x}{x}\\right]_\\varepsilon^R\n+\\int_\\varepsilon^R\\frac{\\sin 2x}{x}\\,dx .\n\\]\n$R\\to+\\infty$ 时分子有界，边界项趋于零。$\\varepsilon\\to0^+$ 时 $\\sin^2\\varepsilon$ 约为 $\\varepsilon^2$，边界项也趋于零。最后令 $u=2x$，$\\frac{dx}{x}=\\frac{du}{u}$，所求正好等于给出的 $\\frac\\pi2$。\n@@ 1850 3.5\n(1) 上限为无穷大。对 $x\\ge1$，$0<\\frac1{x^2\\sqrt{1+x}}\\le\\frac1{x^{\\frac52}}$。右边的幂积分收敛，因为指数 $\\frac52>1$。用比较准则得原积分收敛。\n\n(2) 这里的问题在 $x=0$。对 $x>0$，$\\ln(1+x)\\le x$，这可由 $x-\\ln(1+x)$ 在 $0$ 处为零且导数非负看出。所以 $\\frac1{\\ln(1+x)}\\ge\\frac1x$。而 $\\int_\\varepsilon^1\\frac{dx}{x}=-\\ln\\varepsilon\\to+\\infty$，比较得原积分发散至 $+\\infty$。\n@@ 1856 3.5\n逐项在有限区间求原函数，再检查无穷端。\n\nA 的原函数为 $\\frac12\\ln(1+x^2)$。$[0,+\\infty)$ 上已发散，整轴积分也发散。奇函数两边对称抵消只会得到主值。\n\nB 的原函数为 $\\frac12(\\ln x)^2$，趋于无穷。C 的原函数为 $\\ln\\ln x$，同样趋于无穷。\n\nD 的原函数为 $-(x+1)e^{-x}$，在 $+\\infty$ 趋于 $0$。因此积分等于 $3e^{-2}$，为有限值，选 \\textbf{D}。\n@@ 1868 3.5\n\\TextCorrection{对照原页，第一问的根号写成 $\\sqrt{|x-x^2|}$，删除 OCR 多出的 $1$。}\n(1) 先在唯一的奇点 $1$ 处分开。左边 $|x-x^2|=x(1-x)$，令 $x=\\sin^2 t$ 后被积式为 $2dt$，$t$ 从 $\\frac\\pi4$ 到 $\\frac\\pi2$，得到 $\\frac\\pi2$。右边 $|x-x^2|=x(x-1)$，令 $u=\\sqrt{x-1}$ 后化成 $\\int_0^{\\frac1{\\sqrt2}}\\frac{2}{\\sqrt{1+u^2}}du$，得 $2\\ln(\\frac{1+\\sqrt3}{\\sqrt2})=\\ln(2+\\sqrt3)$。两段都收敛，总值 $\\frac\\pi2+\\ln(2+\\sqrt3)$。\n\n(2) 同样令 $u=\\sqrt{x-1}$，上下限变为 $0,+\\infty$，积分化为 $\\int_0^{+\\infty}\\frac{2}{1+u^2}du=2(\\frac\\pi2-0)=\\pi$。这个换元同时化解了下端点的根号奇性。\n@@ 1874 3.5\n将未知的积分记作 $I$。右边是关于这个常数的线性式，因此把等式两边都对 $x$ 积分，就能解出 $I$。第一项的积分为 $\\frac\\pi2$。第二项令 $u=e^{-x}$，得\n\\[\n\\int_0^{+\\infty}\\frac{e^{-x}}{1+e^x}dx\n=\\int_0^1\\frac{u}{1+u}du=1-\\ln2 .\n\\]\n两项均收敛，可以分别积分。于是 $I=\\frac\\pi2-I(1-\\ln2)$，整理得 $I=\\frac{\\pi}{2(2-\\ln2)}$。$2-\\ln2>0$，方程有唯一解。\n@@ 1878 3.5\n先合并被积式为 $\\frac{(a-b)x+b}{x(2x+b)}$。若 $a\\ne b$，用它乘 $x$ 后极限是非零的 $\\frac{a-b}{2}$，所以尾部与常数倍的 $\\frac1x$ 同号且同阶，积分发散。题目给出有限值，必须 $a=b$。\n\n此时被积式拆为 $\\frac1x-\\frac2{2x+b}$，先积到 $R$ 再令 $R\\to+\\infty$，得到\n\\[\n\\lim_{R\\to+\\infty}[\\ln x-\\ln(2x+b)]_1^R=\\ln(1+\\frac b2).\n\\]\n令它等于 $1$，得到 $a=b=2(e-1)$，满足 $b>0$，且在积分区间分母不为零。\n@@ 1882 3.5\n先检查分母。若 $a\\le-2$，则 $2x+a$ 在区间内或端点为零，且 $a\\ne0$，出现一阶极点，积分发散。故只考虑 $a>-2$。把分式拆开，正好得到两个对数导数：\n\\[\n\\frac{a}{x(2x+a)}=\\frac1x-\\frac2{2x+a}.\n\\]\n积分到 $R$，合并成 $\\ln\\frac{x}{2x+a}$ 再代入端点。$R\\to+\\infty$ 时 $\\frac{R}{2R+a}\\to\\frac12$，所以积分为 $\\ln(1+\\frac a2)$。由 $\\ln(1+\\frac a2)=\\ln2$，得到 $a=2$。\n@@ 1886 3.4\n按图示取 $0\\le a<b$、$f(x)\\ge0$。绕 $y$ 轴旋转时，竖直小条形成薄圆柱壳。它的半径约为 $x$，圆周长为 $2\\pi x$，高度为 $f(x)$，厚度为 $dx$，因此体积微元为 $dV=2\\pi x f(x)\\,dx$。把从 $a$ 到 $b$ 的薄壳体积累加，得到\n\\[\nV=2\\pi\\int_a^b x f(x)\\,dx.\n\\]\n圆柱壳也可看作内外半径为 $x,x+dx$ 的圆环柱，其底面积 $\\pi[(x+dx)^2-x^2]=2\\pi x\\,dx+\\pi(dx)^2$，后一项在积分极限中不贡献。若曲线在横轴下方且区间仍在同一侧，壳高改取 $|f(x)|$。\n@@ 1897 3.4\n(1) 两曲线交于 $x=0,k$。先取 $0<k<1$，在 $[0,k]$ 直线较高，在 $[k,1]$ 抛物线较高，所以\n\\[\nS_1+S_2=\\int_0^k(kx-x^2)\\,dx+\\int_k^1(x^2-kx)\\,dx\n=\\frac13-\\frac k2+\\frac{k^3}3.\n\\]\n对 $k$ 求导得 $k^2-\\frac12$，在 $0<k<\\frac1{\\sqrt2}$ 为负，在 $\\frac1{\\sqrt2}<k<1$ 为正，故最小点为 $k=\\frac1{\\sqrt2}$，最小面积 $\\frac13-\\frac1{3\\sqrt2}$。还需检查题设允许的 $k\\le0$。这时 $S_1=-\\frac{k^3}6$，$S_2=\\frac13-\\frac k2$，总和至少为 $\\frac13$，更大。\n\n(2) 所求是两块图形的并集旋转。各处半径都是相应纵坐标，取大半径平方减小半径平方：\n\\[\nV=\\pi\\int_0^k(k^2x^2-x^4)\\,dx+\\pi\\int_k^1(x^4-k^2x^2)\\,dx\n=\\pi\\left(\\frac15-\\frac{k^2}3+\\frac{4k^5}{15}\\right).\n\\]\n代入最小点 $k=\\frac1{\\sqrt2}$，得 $V=\\frac{\\pi(1+\\sqrt2)}{30}$。\n@@ 1905 3.4\n设切点横坐标为 $c$。切线为 $y=\\ln c+\\frac{x-c}{c}$，通过原点给出 $\\ln c-1=0$，所以 $c=e$、切线为 $y=\\frac xe$。\n\n(1) $0\\le x\\le1$ 时图形夹在切线和横轴之间。$1\\le x\\le e$ 时夹在切线和对数曲线之间，因此\n\\[\nA=\\int_0^e\\frac xe\\,dx-\\int_1^e\\ln x\\,dx\n=\\frac e2-[x\\ln x-x]_1^e=\\frac e2-1 .\n\\]\n(2) 绕竖直线 $x=e$，用壳法时半径为 $e-x$。以完整切线下方的图形减去对数曲线下方的图形，得\n\\[\n\\frac{V}{2\\pi}=\\int_0^e(e-x)\\frac xe\\,dx-\\int_1^e(e-x)\\ln x\\,dx.\n\\]\n第一项为 $\\frac{e^2}6$。第二项分别对 $\\ln x$ 和 $x\\ln x$ 分部，得 $-\\frac{e^2}4+e-\\frac14$。所以 $V=2\\pi(\\frac{5e^2}{12}-e+\\frac14)$。\n@@ 1916 3.5\n平方根要求 $\\sin x\\ge0$，因此实数曲线只存在于各段 $[2k\\pi,(2k+1)\\pi]$，$k=0,1,\\ldots$。每一段与横轴之间的图形绕横轴形成旋转体，截面面积为 $\\pi y^2=\\pi e^{-2x}\\sin x$。\n\n第一段体积除以 $\\pi$ 为\n\\[\nJ=\\int_0^\\pi e^{-2x}\\sin x\\,dx\n=\\left[-\\frac{e^{-2x}(2\\sin x+\\cos x)}5\\right]_0^\\pi\n=\\frac{1+e^{-2\\pi}}5.\n\\]\n第 $k$ 段通过平移 $x=2k\\pi+u$，其体积等于 $\\pi J e^{-4k\\pi}$。前 $N$ 段的体积用有限等比数列公式相加，令 $N\\to+\\infty$，得到 $V=\\frac{\\pi J}{1-e^{-4\\pi}}=\\frac{\\pi}{5(1-e^{-2\\pi})}$。\n@@ 1920 skip\n该题以一般曲线弧长和椭圆周长的积分公式为核心。教材上册第三章第四节正文未讲授弧长公式，本次按教材明确教学范围暂不收录。\n@@ 1924 3.4\n$x'(t)=a(1-\\cos t)\\ge0$，所以参数从 $0$ 走到 $2\\pi$ 时不会倒行，可以直接把 $dx=a(1-\\cos t)dt$ 代入体积积分。\n\n绕 $x$ 轴用圆盘，得到 $V_x=\\pi a^3\\int_0^{2\\pi}(1-\\cos t)^3dt$。展开后，$\\cos t,\\cos^3t$ 在一个整周期积分为零，$\\int_0^{2\\pi}\\cos^2t\\,dt=\\pi$，故 $V_x=5\\pi^2a^3$。\n\n绕 $y$ 轴用壳法，得到\n\\[\nV_y=2\\pi a^3\\int_0^{2\\pi}(t-\\sin t)(1-\\cos t)^2dt.\n\\]\n设 $w(t)=(1-\\cos t)^2$，它满足 $w(2\\pi-t)=w(t)$。换元相加可得 $\\int_0^{2\\pi}tw(t)dt=\\pi\\int_0^{2\\pi}w(t)dt=3\\pi^2$。另有 $\\int_0^{2\\pi}\\sin t\\,w(t)dt=[\\frac{(1-\\cos t)^3}3]_0^{2\\pi}=0$。所以 $V_y=6\\pi^3a^3$。\n@@ 1928 skip\n该题求旋转曲面表面积，需要弧长微元与旋转曲面面积公式。教材上册第三章第四节明确讲授的几何应用为面积与体积，本次暂不收录。\n@@ 1932 3.4\n把容器口所在水平面设为深度 $z=0$，向下为正。深度为 $z$ 的水层，到球心的竖直距离是 $z$，由球面方程得截面半径平方为 $R^2-z^2$。厚度为 $dz$ 的水层体积约为 $\\pi(R^2-z^2)dz$，重力为这个体积乘 $\\rho g$。\n\n这一层水要提升 $z$，故所需功的微元是 $dW=\\rho g\\pi z(R^2-z^2)dz$。对全部深度累加，\n\\[\nW=\\rho g\\pi\\int_0^R z(R^2-z^2)\\,dz\n=\\rho g\\pi\\left[\\frac{R^2z^2}2-\\frac{z^4}4\\right]_0^R\n=\\frac{\\rho g\\pi R^4}{4}=2500\\pi R^4\\ \\mathrm{J}.\n\\]\n此处 $R$ 用米。每层水仅提升到容器口，给出了克服重力的最小功。\n@@ 1936 3.4\n质心是以各小段质量为权重的平均位置。位置 $x$ 附近长度 $dx$ 的小段质量为 $dm=\\rho(x)dx$，它对原点的质量矩为 $x\\,dm$。所以先分别求总质量和质量矩，\n\\[\nM=\\int_0^1(-x^2+2x+1)dx=\\frac53,\\qquad\nJ=\\int_0^1(-x^3+2x^2+x)dx=\\frac{11}{12}.\n\\]\n再相除，得到 $\\bar x=\\frac JM=\\frac{11}{20}$。密度在 $[0,1]$ 上递增，右端更重，结果比均匀细棒的中点 $\\frac12$ 稍靠右，且位于棒内。\n@@ 1940 3.4\n按图中标注取水平坐标 $y$，竖直向下的深度为 $z$。矩形半宽为 $1$，下方抛物线的顶点深度为 $h+1$、两端在 $(\\pm1,h)$，故它的方程为 $z=h+1-y^2$。深度 $z$ 处的下部宽度是 $2\\sqrt{h+1-z}$。\n\n水压强为 $\\rho gz$。水平薄条两端的深度相同，压力微元为压强乘宽度再乘 $dz$。于是\n\\[\nF_{\\rm 矩}=\\rho g\\int_0^h2z\\,dz=\\rho gh^2,\\quad\nF_{\\rm 下}=2\\rho g\\int_h^{h+1}z\\sqrt{h+1-z}\\,dz.\n\\]\n第二个积分令 $u=h+1-z$，得到 $F_{\\rm 下}=2\\rho g[\\frac{2(h+1)}3-\\frac25]=\\rho g(\\frac{4h}3+\\frac8{15})$。由比值 $\\frac{F_{\\rm 矩}}{F_{\\rm 下}}=\\frac54$ 得 $3h^2-5h-2=0$，两根为 $2,-\\frac13$。高度为正，故 $h=2\\ \\mathrm m$。\n@@ 1946 3.4\n质点移动到 $(x,0)$ 时，与 $Q$ 的距离为 $r=\\sqrt{x^2+1}$。两者都是单位质量，引力大小为 $\\frac{G}{r^2}$，方向沿着从 $P$ 指向 $Q$ 的连线。\n\n做功只计算力在移动方向上的分量。引力的水平分量朝负 $x$ 方向，其大小还要乘方向因子 $\\frac{x}{r}$，所以为 $\\frac{Gx}{(x^2+1)^{\\frac32}}$。为克服该引力，外力沿正 $x$ 方向做功，因此\n\\[\nW=\\int_0^l\\frac{Gx}{(x^2+1)^{\\frac32}}\\,dx\n=G\\left(1-\\frac1{\\sqrt{1+l^2}}\\right).\n\\]\n对应 \\textbf{B}。因子 $\\frac{x}{r}$ 来自方向投影，仅用引力大小会把竖直方向的力也计入水平功。\n"}
{"chunk_id":"eed209","wall_time_seconds":0.000008667,"exit_code":0,"original_token_count":1607,"output":"% SOURCE line=1820 pdf_page=291 section=3.1\n\n\\Question{232}{第6章 · 例题第3组 · 例 11}\n\n设 $f(x)$ 在 $[0,\\pi]$ 上连续，且 $\\int_{0}^{\\pi}f(x)dx=\\int_{0}^{\\pi}f(x)\\cos xdx=0$，证明：在 $(0,\\pi)$ 内至少存在两个不同的点 $\\xi_{1},\\xi_{2}$，使得 $f(\\xi_{1})=f(\\xi_{2})=0$。\n\n\\vfill\n\n\n% SOURCE line=1824 pdf_page=292 section=3.3\n\n\\Question{313}{第6章 · 例题第3组 · 例 12}\n\n设 $f(x)$ 连续, $f(x+T)=f(x)$, T>0, 且 $f(-x)=f(x)$.\n\n(1) 证明: $\\int_{0}^{kT} x f(x) dx = \\frac{k^{2}T}{2} \\int_{0}^{T} f(x) dx$ (k 为正整数).\n\n(2) 利用(1)的结论, 求 $I=\\int_{0}^{n\\pi}x|\\sin x|$ dx.\n\n\\vfill\n\n\n% SOURCE line=1832 pdf_page=293 section=3.3\n\n\\Question{314}{第6章 · 例题第3组 · 例 13}\n\n设 $f''(x)$ 在 $[0,1]$ 上连续，且 $f(0)=f(1)=0$，记 $M=\\max_{0\\leq x\\leq1}\\{|f''(x)|\\}$，证明：\n\n(1)$\\int_{0}^{1}f(x)dx=\\frac{1}{2}\\int_{0}^{1}x(x-1)f''(x)dx;$\n\n(2)$\\left|\\int_{0}^{1}f(x)dx\\right|\\leqslant\\frac{M}{12}.$\n\n\\vfill\n\n\n% SOURCE line=1886 pdf_page=302 section=3.4\n\n\\Question{320}{第6章 · 例题第4组 · 示例}\n\n如图 6-4 所示，求由直线 $x = a, x = b, x$ 轴，曲线 $y = f(x)$ 所围成的图形绕 y 轴旋转一周所得旋转体的体积. y O a x x+dx b x 图6-4\n\n\\par\\smallskip\\includegraphics[width=170bp,height=135bp,keepaspectratio]{lilin-figures/第302页.png}\n\n\\vfill\n\n\n% SOURCE line=1897 pdf_page=303 section=3.4\n\n\\Question{321}{第6章 · 例题第5组 · 例 1}\n\n设直线 y=kx 与曲线 $y=x^{2}$ 所围图形的面积为 $S_{1}$，它们与直线 x=1 所围图形的面积为 $S_{2}$，且 k < 1.\n\n(1) 确定 k 的值, 使得 $S_{1} + S_{2}$ 取得最小值, 并求最小值.\n\n(2) 求该最小值所对应的图形绕 x 轴旋转一周所得旋转体的体积.\n\n\\vfill\n\n\n% SOURCE line=1905 pdf_page=304 section=3.4\n\n\\Question{322}{第6章 · 例题第5组 · 例 2}\n\n过坐标原点作曲线 $y = \\ln x$ 的切线，该切线与曲线 $y = \\ln x$ 及 x 轴围成平面图形 D，如图 6-10 所示。求：\n\n(1) D 的面积 A.\n\n(2) D 绕直线 x = e 旋转一周所得旋转体的体积. 图6-10\n\n\\par\\smallskip\\includegraphics[width=390bp,height=135bp,keepaspectratio]{lilin-figures/第304页.png}\n\n\\vfill\n\n\n% SOURCE line=1924 pdf_page=307 section=3.4\n\n\\Question{323}{第6章 · 例题第5组 · 例 5}\n\n求由摆线 $x = a(t - \\sin t)$, $y = a(1 - \\cos t)(a > 0)$ 的一拱 $(0 \\leqslant t \\leqslant 2\\pi)$ 及 x 轴所围图形分别绕 x 轴，y 轴旋转一周所得旋转体的体积.\n\n\\vfill\n\n\n% SOURCE line=1932 pdf_page=309 section=3.4\n\n\\Question{324}{第6章 · 例题第5组 · 例 7}\n\n一个半球形容器，其半径为R。容器中盛满水，将容器中的水全部抽出容器口，至少需要做功多少？（设水的密度为$\\rho=1\\times10^{3}\\ \\frac{\\mathrm{kg}}{\\mathrm m^3}$，重力加速度$g=10\\ \\frac{\\mathrm m}{\\mathrm s^2}$）\n\n\\vfill\n\n\n% SOURCE line=1936 pdf_page=310 section=3.4\n\n\\Question{325}{第6章 · 例题第5组 · 例 8}\n\n一根长度为1的细棒位于x轴的区间[0,1]上，其线密度$\\rho(x)=-x^{2}+2x+1$，求该细棒的质心坐标$\\overrightarrow{x}$.\n\n\\vfill\n\n\n% SOURCE line=1940 pdf_page=311 section=3.4\n\n\\Question{326}{第6章 · 例题第5组 · 例 9}\n\n某闸门的形状与大小如图6-14所示，其中l为对称轴。闸门的上部为矩形ABCD，下部由二次抛物线与线段AB组成，当水面与闸门的上端相平时，欲使闸门矩形部分承受的水压力与闸门下部承受的水压力之比为5:4，问闸门矩形部分的高h应为多少米？\n\n\\par\\smallskip\\includegraphics[width=390bp,height=135bp,keepaspectratio]{lilin-figures/第311页.png}\n\n\\vfill\n\n\n% SOURCE line=1946 pdf_page=312 section=3.4\n\n\\Question{327}{第6章 · 例题第5组 · 例 10}\n\n设单位质点 P, Q 分别位于点 (0,0) 和点 (0,1) 处, P 从点 (0,0) 出发沿 x 轴正向移动, 记 G 为引力常量, 则当质点 P 移动到点 (l,0) 时, 克服质点 Q 的引力所做的功为 ( ).\n\n\\textbf{A.} $\\int_{0}^{l}\\frac{G}{x^{2}+1}dx$\n\n\\textbf{B.} $\\int_{0}^{l}\\frac{Gx}{(x^{2}+1)^{\\frac{3}{2}}}dx$\n\n\\textbf{C.} $\\int_{0}^{l}\\frac{G}{(x^{2}+1)^{\\frac{3}{2}}}dx$\n\n\\textbf{D.} $\\int_{0}^{l}\\frac{G(x+1)}{(x^{2}+1)^{\\frac{3}{2}}}dx$\n\n\\vfill\n\n\n% SOURCE line=1842 pdf_page=294 section=3.5\n\n\\Question{338}{第6章 · 例题第4组 · 例 1}\n\n设$\\lim_{x\\to\\infty}\\left(\\frac{1+x}{x}\\right)^{ax}=\\int_{-\\infty}^{a}t\\mathrm{e}^{t}dt$，则a=\\underline{\\hspace{4em}}。\n\n\\vfill\n\n\n% SOURCE line=1846 pdf_page=295 section=3.5\n\n\\Question{339}{第6章 · 例题第4组 · 例 2}\n\n已知$\\int_{0}^{+\\infty}\\frac{\\sin x}{x}dx=\\frac{\\pi}{2}$，求$\\int_{0}^{+\\infty}\\frac{\\sin^{2}x}{x^{2}}dx$。\n\n\\vfill\n\n\n% SOURCE line=1850 pdf_page=296 section=3.5\n\n\\Question{340}{第6章 · 例题第4组 · 例 3}\n\n判别下列反常积分的敛散性：\n\n(1)$\\int_{1}^{+\\infty}\\frac{\\mathrm{d}x}{x^{2}\\sqrt{1+x}}$; (2)$\\int_{0}^{1}\\frac{\\mathrm{d}x}{\\ln(1+x)}$.\n\n\\vfill\n\n\n% SOURCE line=1856 pdf_page=297 section=3.5\n\n\\Question{341}{第6章 · 例题第4组 · 例 4}\n\n下列反常积分收敛的是( ).\n\n\\textbf{A.} $\\int_{-\\infty}^{+\\infty}\\frac{x}{1+x^{2}}\\mathrm{d}x$\n\n\\textbf{B.} $\\int_{2}^{+\\infty}\\frac{\\ln x}{x}\\mathrm{d}x$\n\n\\textbf{C.} $\\int_{2}^{+\\infty}\\frac{\\mathrm{d}x}{x\\ln x}$\n\n\\textbf{D.} $\\int_{2}^{+\\infty}\\frac{x}{\\mathrm{e}^{x}}\\mathrm{d}x$\n\n\\vfill\n\n\n% SOURCE line=1868 pdf_page=298 section=3.5\n\n\\Question{342}{第6章 · 例题第4组 · 例 5}\n\n计算下列积分：\n\n(1) $I=\\int_{\\frac{1}{2}}^{\\frac{3}{2}} \\frac{\\mathrm{d}x}{\\sqrt{|x-x^2|}};$ (2) $I=\\int_{1}^{+\\infty} \\frac{\\mathrm{d}x}{x \\sqrt{x-1}}.$\n\n\\vfill\n\n\n% SOURCE line=1874 pdf_page=299 section=3.5\n\n\\Question{343}{第6章 · 例题第4组 · 例 6}\n\n设$\\int_{0}^{+\\infty}f(x)dx$收敛，且$f(x)=\\frac{1}{1+x^{2}}-\\frac{e^{-x}}{1+e^{x}}\\int_{0}^{+\\infty}f(x)dx$，求$\\int_{0}^{+\\infty}f(x)dx$。\n\n\\vfill\n\n\n% SOURCE line=1878 pdf_page=300 section=3.5\n\n\\Question{344}{第6章 · 例题第4组 · 例 7}\n\n已知$\\int_{1}^{+\\infty}\\left(\\frac{2x^{2}+ax+b}{2x^{2}+bx}-1\\right)dx=1(b>0)$，求a，b的值.\n\n\\vfill\n\n\n% SOURCE line=1882 pdf_page=301 section=3.5\n\n\\Question{345}{第6章 · 例题第4组 · 例 8}\n\n设$\\int_{1}^{+\\infty}\\frac{a}{x(2x+a)}\\mathrm{d}x=\\ln2$，则a=\\underline{\\hspace{4em}}。\n\n\\vfill\n\n\n% SOURCE line=1916 pdf_page=305 section=3.5\n\n\\Question{346}{第6章 · 例题第5组 · 例 3}\n\n求曲线 $y = e^{-x} \\sqrt{\\sin x}$ ($x \\geqslant 0$) 绕 x 轴旋转一周所得旋转体的体积 V.\n\n\\vfill\n\n\n"}

## tool · 2026-11-14T02:03:37Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-14T02:03:43Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"08c7de","wall_time_seconds":0.000011375,"exit_code":0,"original_token_count":1317,"output":"@@ 1960 3.1\n在 $0<x\\le\\frac\\pi4$，有 $\\tan x>x$，所以逐点比较得到 $M>N$ 且 $N<\\frac\\pi4<1$。还需要判断 $M$ 与 $1$ 的关系。\n\n设 $h(x)=\\frac{\\tan x}{x}$。其导数的符号等于 $x-\\sin x\\cos x$ 的符号。后者在 $0$ 为零，导数为 $1-\\cos2x>0$，故 $h$ 严格增加，且 $h(\\frac\\pi4)=\\frac4\\pi$。于是\n\\[\nM=\\int_0^{\\frac\\pi4}h(x)\\,dx\n<\\frac\\pi4\\cdot\\frac4\\pi=1 .\n\\]\n综合得到 $1>M>N$，选 \\textbf{B}。两个被积函数在 $0$ 都可按极限补成 $1$。\n@@ 1972 3.2\n当 $x\\to0$ 时，第一被积函数在 $0$ 的极限是 $1$，第二被积函数在 $0$ 的极限是 $e$。用积分中值定理，或用连续性一致估计小区间上的函数值，得到\n\\[\n\\alpha(x)=2x[1+o(1)],\\qquad\n\\beta(x)=\\sin x[e+o(1)] .\n\\]\n所以 $\\frac{\\alpha(x)}{\\beta(x)}\\to\\frac2e$。这个极限为有限的非零数，说明两者是同阶无穷小。只有比值极限为 $1$ 才是等价无穷小，而 $\\frac2e\\ne1$，所以选 \\textbf{D}。\n@@ 1984 3.1\n三个量分别是曲线下方的面积、以右端高度作出的矩形面积、以两端高度作出的梯形面积。因为 $f'<0$，内部 $x$ 都满足 $f(x)>f(b)$，积分得 $S_1>S_2$。\n\n又因 $f''>0$，$f'$ 严格增加，曲线位于两个端点连成的弦下方。因此\n\\[\nf(x)<\\frac{b-x}{b-a}f(a)+\\frac{x-a}{b-a}f(b),\\qquad a<x<b .\n\\]\n两边积分，右边两个线性权重的积分均为 $\\frac{b-a}{2}$，得到 $S_1<S_3$。所以 $S_2<S_1<S_3$，选 \\textbf{B}。\n@@ 1998 3.5\n先对各项积到有限的上限 $R$，然后令 $R\\to+\\infty$。\n\nA 对 $x e^{-x}$ 分部，得到 $[-(x+1)e^{-x}]_0^R\\to1$，收敛。\n\nB 用 $u=x^2$，得到 $\\frac12\\int_0^{R^2}e^{-u}du\\to\\frac12$，收敛。\n\nC 用 $u=\\arctan x$，得到 $\\frac12(\\arctan R)^2\\to\\frac{\\pi^2}{8}$，收敛。\n\nD 的原函数为 $\\frac12\\ln(1+x^2)$，在 $R\\to+\\infty$ 时趋于 $+\\infty$，所以发散，选 \\textbf{D}。前三项不仅有有限极限，还给出了各自的积分值。\n@@ 2012 3.1\n把每项提取 $\\frac1n$，原和式变为 $\\sum_{i=1}^n\\frac1n\\,\\frac{e^{i/n}}{1+e^{2i/n}}$。这对应把 $[0,1]$ 等分成 $n$ 份，每段长度为 $\\frac1n$，取右端点 $\\frac in$ 的 Riemann 和。被积函数连续，所以极限为\n\\[\n\\int_0^1\\frac{e^x}{1+e^{2x}}dx.\n\\]\n令 $u=e^x$，$du=e^x dx$，上下限变为 $1,e$，所得积分为 $\\int_1^e\\frac{du}{1+u^2}=\\arctan e-\\frac\\pi4$。识别步长和取样点后，数列极限就变成定积分计算。\n@@ 2016 3.2\n式子同时在上限和被积函数内含 $x$，直接求导容易多出难处理的项。这里 $x^2-t^2$ 的微分正好含 $t\\,dt$，先令 $u=x^2-t^2$。两端由 $x^2$ 变到 $0$，故\n\\[\n\\int_0^x t f(x^2-t^2)\\,dt\n=-\\frac12\\int_{x^2}^0 f(u)\\,du\n=\\frac12\\int_0^{x^2}f(u)\\,du .\n\\]\n接着用微积分基本定理和链式法则，导数为 $\\frac12 f(x^2)\\cdot2x=x f(x^2)$。这个换元对负 $x$ 也成立，积分方向已由上下限处理。\n@@ 2020 3.2\n让被积函数中的乘积 $xu$ 变成一个变量。对 $x>0$，令 $t=xu$、$dt=x\\,du$，得到\n\\[\ny=\\int_0^{2x}\\sqrt{12-t^2}\\,dt.\n\\]\n原被积函数是实数要求 $0\\le x\\le\\sqrt3$。在内部 $0<x<\\sqrt3$，微积分基本定理给出 $y'=2\\sqrt{12-4x^2}=4\\sqrt{3-x^2}$。\n\n在左端点 $x=0$，原式给出 $y(0)=0$，上面的积分表示也成立，右导数为 $4\\sqrt3$。在右端点 $x=\\sqrt3$，左导数为 $0$。端点应按单侧导数理解，因为实数函数在区间外没有定义。\n@@ 2024 3.2\n求关于 $s$ 的导数时把 $t>0$ 当作固定参数。先令 $u=tx$，则 $du=t\\,dx$，外部的因子 $t$ 正好消去微分的分母，上限 $\\frac st$ 正好变成 $s$。因此\n\\[\nI(s,t)=\\int_0^s f(u)\\,du .\n\\]\n这个表达式已与 $t$ 无关。由 $f$ 连续，微积分基本定理直接给出 $\\frac{dI}{ds}=f(s)$。也可直接用变上限求导，得到 $t f(t\\frac st)\\cdot\\frac1t$，两处 $t$ 相消后相同。\n@@ 2030 3.2\n未知的 $f$ 出现在 $x-t$ 中，先把它的自变量变成积分变量。令 $u=x-t$，得\n\\[\n\\int_0^x t f(x-t)dt\n=\\int_0^x(x-u)f(u)du\n=x\\int_0^x f(u)du-\\int_0^x u f(u)du .\n\\]\n对两边求导时，前一项给出 $\\int_0^x f(u)du+xf(x)$，后一项给出 $xf(x)$，两项恰好抵消，剩下 $\\int_0^x f(u)du=\\sin x$。取 $x=\\frac\\pi2$，便得所求积分为 $1$。若继续求导还可得到 $f(x)=\\cos x$，代回也能核对。\n@@ 2034 3.2\n分子中的 $e^u du$ 是 $e^u$ 的微分。令 $v=e^u-e^{x^2}+1$，上下限变为 $2-e^{x^2},1$。再令 $h=e^{x^2}-1$、$w=1-v$，分子变为 $\\int_0^h f(1-w)dw$。\n\n由 $f(1)=0,f'(1)=2$，有 $f(1-w)=-2w+o(w)$，因此分子为 $-h^2+o(h^2)$。这里误差可在 $0\\le w\\le h$ 上一致估计后积分。由于 $h\\sim x^2$，分子主项为 $-x^4$。分母中 $\\ln(\\cos x)=\\ln[1-(1-\\cos x)]\\sim-(1-\\cos x)\\sim-\\frac{x^2}{2}$，所以分母主项为 $-\\frac{x^4}{2}$。比值极限为 $2$。\n@@ 2038 3.2\n积分中的变量 $x$ 只是求和的哑变量，可以改名为 $t$，将它的值记为常数 $C=\\int_0^1 f(t)dt$。于是 $f(x)=\\frac1{1+x^2}+Cx^3$。对等式两边在 $[0,1]$ 上积分，得到\n\\[\nC=\\int_0^1\\frac{dx}{1+x^2}+C\\int_0^1 x^3dx\n=\\frac\\pi4+\\frac C4.\n\\]\n解得 $C=\\frac\\pi3$。代回得到 $f(x)=\\frac1{1+x^2}+\\frac\\pi3x^3$。最后再积一次，可得其 $[0,1]$ 上积分确为 $\\frac\\pi3$，满足常数的定义。\n"}
{"chunk_id":"244ffe","wall_time_seconds":0.000009375,"exit_code":0,"original_token_count":2022,"output":"% SOURCE line=1960 pdf_page=313 section=3.1\n\n\\Question{233}{第6章 · 选择题 · 第 1 题}\n\n设 $M=\\int_{0}^{\\frac{\\pi}{4}}\\frac{\\tan x}{x}dx$，$N=\\int_{0}^{\\frac{\\pi}{4}}\\frac{x}{\\tan x}dx$，则( )。\n\n\\textbf{A.} M > N > 1\n\n\\textbf{B.} 1 > M > N\n\n\\textbf{C.} N > M > 1\n\n\\textbf{D.} 1 > N > M\n\n\\vfill\n\n\n% SOURCE line=1984 pdf_page=315 section=3.1\n\n\\Question{234}{第6章 · 选择题 · 第 3 题}\n\n设在 $[a, b]$ 上，$f(x) > 0$，$f'(x) < 0$，$f''(x) > 0$，记 $S_{1}=\\int_{a}^{b}f(x)dx,\\quad S_{2}=f(b)(b-a),\\quad S_{3}=\\frac{1}{2}[f(a)+f(b)](b-a),$ 则（）.\n\n\\textbf{A.} $S_{1}<S_{2}<S_{3}$\n\n\\textbf{B.} $S_{2}<S_{1}<S_{3}$\n\n\\textbf{C.} $S_{3}<S_{1}<S_{2}$\n\n\\textbf{D.} $S_{2}<S_{3}<S_{1}$\n\n\\vfill\n\n\n% SOURCE line=2012 pdf_page=317 section=3.1\n\n\\Question{235}{第6章 · 填空题 · 第 1 题}\n\n$\\lim_{n \\to \\infty} \\sum_{i=1}^{n} \\frac{e^{\\frac{i}{n}}}{n + n e^{\\frac{2i}{n}}} =$ \\underline{\\hspace{4em}}.\n\n\\vfill\n\n\n% SOURCE line=2047 pdf_page=325 section=3.1\n\n\\Question{236}{第6章 · 解答题 · 第 5 题}\n\n求 $\\lim_{n \\to \\infty} \\sum_{i=1}^{n} \\frac{1}{n + \\frac{i^2 + 1}{n}}$.\n\n\\vfill\n\n\n% SOURCE line=2073 pdf_page=331 section=3.1\n\n\\Question{237}{第6章 · 解答题 · 第 11 题}\n\n设 $f(x)$ 在 $[a,b]$ 上有连续导数, $f(a)=0$ ，证明： $\\frac{2}{(b-a)^{2}}\\int_{a}^{b}\\left|f(x)\\right|\\mathrm{d}x\\leqslant M,\\quad M=\\max_{x\\in\\left[a,b\\right]}\\left|f'(x)\\right|.$\n\n\\vfill\n\n\n% SOURCE line=2078 pdf_page=332 section=3.1\n\n\\Question{238}{第6章 · 解答题 · 第 12 题}\n\n设 $f(x)$ 是 $[0,a]$ 上的正值函数，且 $f''(x) > 0$，$a > 0$，证明：$\\int_{0}^{a}f(x)dx \\geqslant af\\left(\\frac{a}{2}\\right)$.\n\n\\vfill\n\n\n% SOURCE line=2082 pdf_page=333 section=3.1\n\n\\Question{239}{第6章 · 解答题 · 第 13 题}\n\n设 $f''(x) > 0, x \\in [a, b]$，证明： $f\\left(\\frac{a+b}{2}\\right)\\leqslant\\frac{1}{b-a}\\int_{a}^{b}f(x)dx$\n\n\\vfill\n\n\n% SOURCE line=1972 pdf_page=314 section=3.2\n\n\\Question{263}{第6章 · 选择题 · 第 2 题}\n\n设 $\\alpha(x)=\\int_{0}^{2x}\\frac{\\sin t}{t}dt,\\beta(x)=\\int_{0}^{\\sin x}(1+t)^{\\frac{1}{t}}dt$ ，则当 $x\\to0$ 时，$\\alpha(x)$ 是 $\\beta(x)$ 的（）.\n\n\\textbf{A.} 等价无穷小\n\n\\textbf{B.} 低阶无穷小\n\n\\textbf{C.} 高阶无穷小\n\n\\textbf{D.} 同阶但非等价无穷小\n\n\\vfill\n\n\n% SOURCE line=2016 pdf_page=318 section=3.2\n\n\\Question{264}{第6章 · 填空题 · 第 2 题}\n\n设 $f(x)$ 连续，则 $\\frac{\\mathrm{d}}{\\mathrm{d}x}\\int_{0}^{x} t f\\left(x^{2}-t^{2}\\right) \\mathrm{d}t =$ \\underline{\\hspace{4em}}.\n\n\\vfill\n\n\n% SOURCE line=2020 pdf_page=319 section=3.2\n\n\\Question{265}{第6章 · 填空题 · 第 3 题}\n\n设 $y=\\int_{0}^{2}x\\sqrt{12-x^{2}u^{2}}\\mathrm{d}u(x\\geqslant0)$，则 $y'=\\_\\_\\_\\_\\_\\_$.\n\n\\vfill\n\n\n% SOURCE line=2024 pdf_page=320 section=3.2\n\n\\Question{266}{第6章 · 填空题 · 第 4 题}\n\n设 $f(x)$ 为已知连续函数，$I(s,t)=t\\int_{0}^{\\frac{s}{t}}f(tx)dx$，其中 $t>0,s>0$，则 $\\frac{dI}{ds}=$ \\underline{\\hspace{4em}}.\n\n\\vfill\n\n\n% SOURCE line=2030 pdf_page=321 section=3.2\n\n\\Question{267}{第6章 · 解答题 · 第 1 题}\n\n设 $f(x)$ 连续，且 $\\int_{0}^{x}tf(x-t)dt = 1 - \\cos x$，求 $I = \\int_{0}^{\\frac{\\pi}{2}}f(x)dx$.\n\n\\vfill\n\n\n% SOURCE line=2034 pdf_page=322 section=3.2\n\n\\Question{268}{第6章 · 解答题 · 第 2 题}\n\n设 $f(1) = 0, f'(1) = 2$，求 $\\lim_{x \\to 0} \\frac{\\int_{0}^{x^2} e^u f(e^u - e^{x^2} + 1) \\, du}{x^2 \\ln (\\cos x)}$.\n\n\\vfill\n\n\n% SOURCE line=2038 pdf_page=323 section=3.2\n\n\\Question{269}{第6章 · 解答题 · 第 3 题}\n\n设 $f(x)=\\frac{1}{1+x^{2}}+x^{3}\\int_{0}^{1}f(x)dx$ ，求 $f(x)$ 的表达式.\n\n\\vfill\n\n\n% SOURCE line=2065 pdf_page=329 section=3.2\n\n\\Question{270}{第6章 · 解答题 · 第 9 题}\n\n设 $f(x)$ 在 $[0,+\\infty)$ 上连续且单调增加，证明：当 b > a > 0 时，有 $\\int_{a}^{b} x f(x) \\, dx \\geqslant \\frac{1}{2} \\left[ b \\int_{0}^{b} f(x) \\, dx - a \\int_{0}^{a} f(x) \\, dx \\right]$.\n\n\\vfill\n\n\n% SOURCE line=2069 pdf_page=330 section=3.2\n\n\\Question{271}{第6章 · 解答题 · 第 10 题}\n\n设 $f(x)$ 在 $[0,1]$ 上可导，$f(0)=0,0<f'(x)<1$ ，证明：$\\left[\\int_{0}^{1}f(x)dx\\right]^{2}>\\int_{0}^{1}f^{3}(x)dx$\n\n\\vfill\n\n\n% SOURCE line=2124 pdf_page=341 section=3.2\n\n\\Question{272}{第6章 · 解答题 · 第 21 题}\n\n设 $f(t)$ 在 $(-\\infty, +\\infty)$ 内是可导的正值函数，且 $f(-t) = f(t)$，令 $g(x)=\\int_{-a}^{a}\\left|x-t\\right|f(t)dt,\\quad-a\\leqslant x\\leqslant a(a>0).$\n\n（I）证明：$g(x)$ 是凹函数；\n\n（II）求 $g(x)$ 的最小值；\n\n（III）当 $g(x)$ 的最小值为 $f(a)-a^{2}-1$ 时，求 $f(t)$.\n\n\\vfill\n\n\n% SOURCE line=2051 pdf_page=326 section=3.3\n\n\\Question{315}{第6章 · 解答题 · 第 6 题}\n\n设 $a_{n}=\\int_{0}^{1}x^{n}\\sqrt{1-x^{2}}\\mathrm{d}x$ ($n=0,1,2,\\cdots$)，证明：$\\{a_{n}\\}$ 单调减少，且 $a_{n}=\\frac{n-1}{n+2}a_{n-2}$ ($n=2,3,\\cdots$).\n\n\\vfill\n\n\n% SOURCE line=2055 pdf_page=327 section=3.3\n\n\\Question{316}{第6章 · 解答题 · 第 7 题}\n\n(I)证明:$\\int_{0}^{\\pi}xf(\\sin x)dx=\\frac{\\pi}{2}\\int_{0}^{\\pi}f(\\sin x)dx$;\n\n（II）求$I=\\int_{0}^{\\pi}x\\sin^{n}x\\,dx$\n\n\\vfill\n\n\n% SOURCE line=2061 pdf_page=328 section=3.3\n\n\\Question{317}{第6章 · 解答题 · 第 8 题}\n\n求 $I=\\int_{-1}^{1}|x-y|\\,\\mathrm{e}^{x}\\,\\mathrm{d}x(|y|<1)$.\n\n\\vfill\n\n\n% SOURCE line=2101 pdf_page=337 section=3.4\n\n\\Question{328}{第6章 · 解答题 · 第 17 题}\n\n设平面图形D由$x^{2}+y^{2}\\leqslant2x$与$y\\geqslant x$所围，求图形D绕直线x=2旋转一周所得旋转体的体积.\n\n\\vfill\n\n\n% SOURCE line=2105 pdf_page=338 section=3.4\n\n\\Question{329}{第6章 · 解答题 · 第 18 题}\n\n求圆域 $x^{2}+(y-b)^{2} \\leqslant a^{2}(b>a)$ 绕 x 轴旋转一周所得旋转体的体积.\n\n\\vfill\n\n\n% SOURCE line=2109 pdf_page=339 section=3.4\n\n\\Question{330}{第6章 · 解答题 · 第 19 题}\n\n设曲线 $y = ax^{2} (a > 0, x \\geqslant 0)$ 与 $y = 1 - x^{2}$ 交于点 A，过原点 O 与点 A 的直线与 $y = ax^{2}$ 围成一个平面图形，问 a 为何值时，该图形绕 x 轴旋转所得旋转体的体积最大？最大体积是多少？\n\n\\vfill\n\n\n% SOURCE line=2113 pdf_page=340 section=3.4\n\n\\Question{331}{第6章 · 解答题 · 第 20 题}\n\n(仅数学一、数学二要求)设一容器的内侧是由图6-15中曲线绕y轴旋转一周而成的曲面，该曲线由$x^{2}+y^{2}=2y(y\\geqslant\\frac{1}{2})$与$x^{2}+y^{2}=1(y\\leqslant\\frac{1}{2})$连接而成.\n\n（I）求容器的容积；\n\n（II）若将容器内盛满的水从容器顶全部抽出，至少需要做多少功？ 图6-15\n\n\\par\\smallskip\\includegraphics[width=170bp,height=135bp,keepaspectratio]{lilin-figures/第340页.png}\n\n\\vfill\n\n\n% SOURCE line=1998 pdf_page=316 section=3.5\n\n\\Question{347}{第6章 · 选择题 · 第 4 题}\n\n下列反常积分发散的是( ).\n\n\\textbf{A.} $\\int_{0}^{+\\infty}x\\mathrm{e}^{-x}\\mathrm{d}x$\n\n\\textbf{B.} $\\int_{0}^{+\\infty}x\\mathrm{e}^{-x^{2}}\\mathrm{d}x$\n\n\\textbf{C.} $\\int_{0}^{+\\infty}\\frac{\\arctan x}{1+x^{2}}\\mathrm{d}x$\n\n\\textbf{D.} $\\int_{0}^{+\\infty}\\frac{x}{1+x^{2}}\\mathrm{d}x$\n\n\\vfill\n\n\n% SOURCE line=2042 pdf_page=324 section=3.5\n\n\\Question{348}{第6章 · 解答题 · 第 4 题}\n\n求下列积分: (I) $\\int_{-1}^{1}\\frac{2x^{2}+\\sin x}{1+\\sqrt{1-x^{2}}}\\mathrm{d}x;$ (II) $\\int_{0}^{n\\pi}\\sqrt{1-\\sin2x}\\mathrm{d}x;$ (III) $\\int_{0}^{1}\\frac{x\\mathrm{d}x}{(2-x^{2})\\sqrt{1-x^{2}}};$\n\n(IV) $\\int_{0}^{\\frac{\\pi}{2}}\\ln(\\sin x)\\mathrm{d}x;$ (V) $\\int_{0}^{\\frac{\\pi}{4}}\\frac{x}{1+\\cos2x}\\mathrm{d}x;$ (VI) $\\int_{\\frac{1}{2}}^{2}\\left(1+x-\\frac{1}{x}\\right)\\mathrm{e}^{x+\\frac{1}{x}}\\mathrm{d}x;$\n\n(VII) $\\int_{-\\mathrm{e}}^{-\\sqrt{\\mathrm{e}}}\\frac{\\ln\\ln|x|}{x\\ln|x|}\\mathrm{d}x;$ (VIII) $\\int_{-1}^{1}(x^{2})^{\\frac{3}{2}}\\mathrm{d}x.$\n\n\\vfill\n\n\n% SOURCE line=2087 pdf_page=334 section=3.5\n\n\\Question{349}{第6章 · 解答题 · 第 14 题}\n\n计算反常积分：\n\n(I)$\\int_{2}^{+\\infty}\\frac{\\mathrm{d}x}{(x-1)^4\\sqrt{x^2-2x}}$; (II)$\\int_{1}^{3}\\frac{dx}{\\sqrt{(x-1)(3-x)}}$.\n\n\\vfill\n\n\n% SOURCE line=2097 pdf_page=336 section=3.5\n\n\\Question{350}{第6章 · 解答题 · 第 16 题}\n\n求曲线 $y = e^{-x} \\sin x \\, (x \\geqslant 0)$ 与 x 轴所围图形的面积.\n\n\\vfill\n\n\n"}

## tool · 2026-11-14T02:04:39Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-14T02:04:43Z




## tool · 2026-11-14T02:04:48Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"20f89b","wall_time_seconds":0.000011375,"exit_code":0,"original_token_count":2105,"output":"@@ 2055 3.3\n(I) 记左边为 $J$，令 $x=\\pi-u$。因为 $\\sin(\\pi-u)=\\sin u$，得 $J=\\int_0^\\pi(\\pi-u)f(\\sin u)du$。与原式相加，得到 $2J=\\pi\\int_0^\\pi f(\\sin x)dx$。\n\n(II) 取 $f(u)=u^n$，得到 $I=\\frac\\pi2 B_n$，其中 $B_n=\\int_0^\\pi\\sin^n x\\,dx$。对 $\\sin^{n-1}x\\sin x$ 分部，端点项为零，\n\\[\nB_n=(n-1)\\int_0^\\pi\\sin^{n-2}x\\cos^2x\\,dx\n=(n-1)(B_{n-2}-B_n).\n\\]\n所以 $B_n=\\frac{n-1}{n}B_{n-2}$。从 $B_0=\\pi,B_1=2$ 向下递推可得\n\\[\nI=\\begin{cases}\n\\frac{\\pi^2}{2}\\frac{1\\cdot3\\cdots(2m-1)}{2\\cdot4\\cdots2m},&n=2m,\\\\\n\\pi\\frac{2\\cdot4\\cdots2m}{1\\cdot3\\cdots(2m+1)},&n=2m+1.\n\\end{cases}\n\\]\n当 $m=0$ 时空乘积取 $1$，包括 $n=0,1$ 的情况。\n@@ 2061 3.3\n$y$ 在此题是参数，积分变量是 $x$。由 $|y|<1$，绝对值在积分内部的 $x=y$ 处分两段。在左段 $|x-y|=y-x$，右段等于 $x-y$，所以\n\\[\nI=\\int_{-1}^{y}(y-x)e^x dx+\\int_y^1(x-y)e^x dx.\n\\]\n分别作一次分部，或对候选乘积求导，可以得到两个原函数 $(y-x+1)e^x$、$(x-y-1)e^x$。代入端点后，\n\\[\nI=e^y-(y+2)e^{-1}-ye+e^y\n=2e^y-ye-(y+2)e^{-1}.\n\\]\n例如 $y=0$ 时得 $2-\\frac2e>0$，与原被积函数非负一致。\n@@ 2065 3.2\n出现 $x\\int_0^x f$ 的端点值，可以想到对这个乘积求导。记 $F(x)=\\int_0^x f(t)dt$，则 $(xF(x))'=F(x)+xf(x)$。由于 $f$ 单调增加，$0\\le t\\le x$ 时 $f(t)\\le f(x)$，对 $t$ 积分得 $F(x)\\le xf(x)$。因此\n\\[\n(xF(x))'\\le2xf(x).\n\\]\n从 $a$ 到 $b$ 积分，得 $bF(b)-aF(a)\\le2\\int_a^bxf(x)dx$，两边除以 $2$ 就是目标。这个比较只乘了正的长度 $x$，无需额外假设 $f$ 的正负。\n@@ 2069 3.2\n先由 $f'>0$、$f(0)=0$ 得 $f(x)>0$，$x>0$。记 $F(x)=\\int_0^x f(t)dt$，要让积分的平方出现，想到 $(F^2)'=2Ff$。因此只需比较 $f^3$ 与 $2Ff$，即比较 $f^2$ 与 $2F$。\n\n设 $H(x)=2F(x)-f(x)^2$。有 $H(0)=0$，而\n\\[\nH'(x)=2f(x)[1-f'(x)]>0,\\qquad 0<x<1.\n\\]\n由中值定理，$H(x)>0$。乘以正的 $f(x)$，得到 $f(x)^3<2F(x)f(x)$。对 $[0,1]$ 积分，右边是 $[F(x)^2]_0^1$，于是 $\\int_0^1 f(x)^3dx<[\\int_0^1 f(x)dx]^2$。条件 $f'<1$ 正是保证严格不等式的一步。\n@@ 2073 3.1\n条件给了导数的最大绝对值，先用 Lagrange 中值定理把它变成函数值的界。对每个 $x\\in(a,b]$，存在 $\\xi$ 在 $a,x$ 之间，使 $f(x)-f(a)=f'(\\xi)(x-a)$。由 $f(a)=0$，得到 $|f(x)|\\le M(x-a)$。\n\n接着两边积分，\n\\[\n\\int_a^b|f(x)|dx\\le M\\int_a^b(x-a)dx=\\frac M2(b-a)^2 .\n\\]\n题设分母 $(b-a)^2$ 为正，将它除到左边并乘以 $2$ 就得到结论。这里使用绝对值后上界始终非负，允许 $f$ 在区间内变号。\n@@ 2078 3.1\n右边是「区间长度乘以中点处的函数值」。为了让中点自然出现，在 $c=\\frac a2$ 处作切线。由 $f''>0$，$f'$ 严格增加，曲线位于这条切线上方。具体地，对 $x>c$，中值定理给出的斜率大于 $f'(c)$；对 $x<c$，斜率小于 $f'(c)$，但乘上负的 $x-c$ 后方向反转。因此两种情况都有\n\\[\nf(x)\\ge f(c)+f'(c)(x-c).\n\\]\n积分后 $\\int_0^a(x-c)dx=0$，切线的倾斜部分相消，留下 $\\int_0^a f(x)dx\\ge af(c)$，即所证。由于 $f''>0$，当 $x\\ne c$ 实际为严格大于。\n@@ 2082 3.1\n设区间中点为 $c=\\frac{a+b}{2}$。$f''>0$ 保证 $f'$ 严格增加。用中值定理可得曲线在中点的切线上方，\n\\[\nf(x)\\ge f(c)+f'(c)(x-c),\\qquad a\\le x\\le b.\n\\]\n理由是 $x>c$ 时，割线斜率至少为 $f'(c)$；$x<c$ 时割线斜率至多为 $f'(c)$，乘负的横坐标增量后又得到同一方向的不等式。两边积分，线性项关于中点奇对称，所以积分为零。得 $\\int_a^b f(x)dx\\ge(b-a)f(c)$。除以正数 $b-a$，便得题设结论。\n@@ 2087 3.5\n(I) 将根号配成 $\\sqrt{(x-1)^2-1}$。倒数代换 $u=\\frac1{x-1}$ 同时降低分母幂并把无穷上限化为有限端点。$dx=-\\frac{du}{u^2}$，原积分变为\n\\[\n\\int_0^1\\frac{u^3}{\\sqrt{1-u^2}}du.\n\\]\n再令 $v=1-u^2$，变为 $\\frac12\\int_0^1(1-v)v^{-\\frac12}dv=\\frac12(2-\\frac23)=\\frac23$。$v^{-\\frac12}$ 在 $0$ 可积，说明反常端点收敛。\n\n(II) 根号内 $(x-1)(3-x)=1-(x-2)^2$。先把端点截去，再用反正弦原函数 $\\arcsin(x-2)$，最后两端分别趋于 $\\pm1$，得到 $\\frac\\pi2-(-\\frac\\pi2)=\\pi$。两端的单侧积分均收敛，才能相加。\n@@ 2093 skip\n该题以参数曲线的弧长积分公式为核心。教材上册第三章第四节正文未讲授弧长公式，本次按教材明确教学范围暂不收录。\n@@ 2097 3.5\n面积要累加每段的正面积，故为 $A=\\int_0^{+\\infty}e^{-x}|\\sin x|dx$。若直接积 $e^{-x}\\sin x$，横轴下方的面积会被扣除。\n\n在第 $k$ 段 $[k\\pi,(k+1)\\pi]$ 令 $x=k\\pi+u$，则 $|\\sin x|=\\sin u$、$0\\le u\\le\\pi$，所以这段面积为 $e^{-k\\pi}J$，其中\n\\[\nJ=\\int_0^\\pi e^{-u}\\sin u\\,du\n=\\left[-\\frac{e^{-u}(\\sin u+\\cos u)}2\\right]_0^\\pi\n=\\frac{1+e^{-\\pi}}2.\n\\]\n先累加前 $N$ 段，用有限等比和得到 $J\\frac{1-e^{-N\\pi}}{1-e^{-\\pi}}$，令 $N\\to+\\infty$，得到 $A=\\frac{e^\\pi+1}{2(e^\\pi-1)}$。\n@@ 2101 3.4\n圆的方程写为 $(x-1)^2+y^2\\le1$。直线与圆交于 $(0,0),(1,1)$，满足 $y\\ge x$ 的部分只能位于 $0\\le x\\le1$，其上下边界为 $\\sqrt{2x-x^2}$ 和 $x$。\n\n绕竖直线 $x=2$，用竖条圆柱壳。半径为 $2-x$，高度为 $\\sqrt{2x-x^2}-x$，所以\n\\[\n\\frac{V}{2\\pi}=\\int_0^1(2-x)\\sqrt{2x-x^2}dx-\\int_0^1(2x-x^2)dx.\n\\]\n第二项为 $\\frac23$。第一项令 $u=x-1$，得 $\\int_{-1}^0(1-u)\\sqrt{1-u^2}du=\\frac\\pi4+\\frac13$，分别是单位圆四分之一面积和幂函数换元积分。相减再乘 $2\\pi$，得 $V=\\frac{\\pi^2}2-\\frac{2\\pi}3$。\n@@ 2105 3.4\n按几何题中 $a$ 是正半径，$b>a$ 保证整个圆位于横轴上方。对固定 $x\\in[-a,a]$，上下边界为 $y=b\\pm\\sqrt{a^2-x^2}$。旋转后得到圆环，其外半径为较大的纵坐标，内半径为较小的纵坐标。因此\n\\[\nV=\\pi\\int_{-a}^a\\big[(b+\\sqrt{a^2-x^2})^2-(b-\\sqrt{a^2-x^2})^2\\big]dx\n=4\\pi b\\int_{-a}^a\\sqrt{a^2-x^2}dx .\n\\]\n最后一个积分为半径 $a$ 的上半圆面积 $\\frac{\\pi a^2}2$，所以 $V=2\\pi^2a^2b$。先作平方差能使两个根式平方与 $b^2$ 全部抵消。\n@@ 2109 3.4\n由 $ax^2=1-x^2$，交点横坐标为 $c=\\frac1{\\sqrt{a+1}}$，纵坐标为 $ac^2$。过原点的直线斜率为 $ac$，所以直线方程 $y=acx$。在 $0<x<c$，直线高于 $ax^2$，旋转截面是圆环，故\n\\[\nV(a)=\\pi\\int_0^c[(acx)^2-(ax^2)^2]dx\n=\\frac{2\\pi a^2}{15(a+1)^{\\frac52}}.\n\\]\n此时 $a$ 才是待优化的变量。求导可将正因子提出，得到\n\\[\nV'(a)=\\frac{\\pi a(4-a)}{15(a+1)^{\\frac72}}.\n\\]\n所以 $0<a<4$ 时递增，$a>4$ 时递减，全局最大值在 $a=4$ 取得，为 $V_{\\max}=\\frac{32\\pi}{375\\sqrt5}$。两端 $a\\to0^+$、$a\\to+\\infty$ 的体积均趋于零。\n@@ 2113 3.4\n由原图，容器底部为 $y=-1$，顶部为 $y=2$。水平截面在 $y=\\frac12$ 处换边界。半径平方在下部为 $1-y^2$，上部为 $2y-y^2$。\n\n(I) 按圆盘体积累加，\n\\[\nV=\\pi\\int_{-1}^{\\frac12}(1-y^2)dy+\n\\pi\\int_{\\frac12}^2(2y-y^2)dy\n=\\pi\\left(\\frac98+\\frac98\\right)=\\frac{9\\pi}4.\n\\]\n(II) 记水密度为 $\\rho$、重力加速度为 $g$。高度 $y$ 处厚 $dy$ 的水层需提升 $2-y$，故功为重力乘提升高度。于是\n\\[\nW=\\rho g\\pi\\left[\\int_{-1}^{\\frac12}(2-y)(1-y^2)dy+\n\\int_{\\frac12}^2(2-y)(2y-y^2)dy\\right].\n\\]\n两个积分分别是 $\\frac{153}{64}$ 和 $\\frac{63}{64}$，所以 $W=\\frac{27\\pi\\rho g}{8}$。题干未指定 $\\rho,g$ 及长度单位，保留一般式。若坐标以米计且取 $\\rho=1000,g=10$，则为 $33750\\pi\\ \\mathrm J$。\n@@ 2124 3.2\n(I) 绝对值在 $t=x$ 处换号，先拆成 $g(x)=\\int_{-a}^x(x-t)f(t)dt+\\int_x^a(t-x)f(t)dt$。逐项求导，端点项都乘以零，得\n\\[\ng'(x)=\\int_{-a}^x f(t)dt-\\int_x^a f(t)dt,\\qquad g''(x)=2f(x)>0 .\n\\]\n按教材术语，二阶导数为正称图像凹，即图像位于弦下方，故(I)成立。\n\n(II) $f$ 为偶函数，两边的积分在 $x=0$ 相等，所以 $g'(0)=0$。又因 $g''>0$，$g'$ 严格增加，故 $g$ 在 $0$ 左侧递减、右侧递增，最小值是 $g(0)=2\\int_0^a t f(t)dt$。\n\n(III) 若该关系对任意 $a>0$ 成立，则 $2\\int_0^a t f(t)dt=f(a)-a^2-1$。令 $a\\to0^+$ 得 $f(0)=1$。对 $a$ 求导得 $f'(a)-2af(a)=2a$，即 $[(f(a)+1)e^{-a^2}]'=0$。由初值常数为 $2$，故 $f(a)=2e^{a^2}-1$；用偶性延伸到所有实数。它为正且可代回核对。若关系仅针对某个固定的 $a$，题设只有一条积分约束，无法唯一确定整个 $f$。\n"}

## tool · 2026-11-14T02:05:53Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-14T02:06:03Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"8075a1","wall_time_seconds":0.000012041,"exit_code":0,"original_token_count":587,"output":"entries 114\ngrades Counter({'3': 66, '2': 37, '4': 5, '1': 3, '0': 3})\nslashes [(144, \"四问答案如上。(2) 求导时令 $P=(\\\\ln x)^2+2\\\\ln x+2$，有 $[-P/x]'=(P-xP')/x^2=(\\\\ln x)^2/x^2$。(4) 两个含 $\\\\arcsin x$ 的交叉项抵消。对数题要求 $x>0$，(4) 内部 $|x|<1$。\"), (193, \"三项依次用一次式积分、$q'/q$ 型积分和二次式配方积分。留意原式对整个余项取负，最终\"), (229, '$f(x)=\\\\frac{xe^{x/2}}{2(1+x)^{3/2}}$，此处指数均按实数幂理解。$Ff$ 恢复题设，$F(0)=1$、$F>0$；不能任取负平方根。'), (297, '(I) 求导为 $[4-(x-2)^2]^{-1/2}$；(II) 用链式法则直接恢复原式；(IV) 求导得 $(1+x^3)^{-1/3}x^5$。(V) $du=\\\\frac{\\\\cos x}{2\\\\sqrt{\\\\sin x}}dx$，从而分母转换为 $1-u^4$，要求 $\\\\sin x>0,\\\\cos x\\\\ne0$；(VI) 两个二次因式都恒正。各答案中的代换变量均按本问定义代回。'), (433, '证明 $\\\\int_{\\\\pi/4}^{\\\\pi/2}\\\\frac{\\\\sin x}{x}dx$ 的两个严格界。'), (564, '$I=8-2\\\\pi-4\\\\ln2<0$。$f$ 在 $[0,1]$ 有界，故绝对值由常数倍 $x^{-1/2}$ 控制；下端点的 $2\\\\sqrt\\\\varepsilon f(\\\\varepsilon)$ 趋于零。'), (691, '两个变上限积分分别含 $\\\\frac{\\\\sin t}t$ 与 $(1+t)^{1/t}$，求它们在 $0$ 的比值极限。'), (1045, '(1) $\\\\frac\\\\pi2+\\\\ln(2+\\\\sqrt3)$；(2) $\\\\pi$。第一问两侧在 $1$ 都是常数倍 $|x-1|^{-1/2}$，分别收敛；第二问换元在截断区间先执行，再取 $u\\\\to0^+, +\\\\infty$，所得反正切极限有限。'), (1242, \"选 B，$W=G(1-\\\\frac1{\\\\sqrt{1+l^2}})$。$W(0)=0$ 且 $W'(l)=\\\\frac{Gl}{(1+l^2)^{3/2}}$ 为水平阻力；$l\\\\to+\\\\infty$ 时功趋于 $G$。\"), (1307, '求 $\\\\sum_{i=1}^n\\\\frac{e^{i/n}}{n+ne^{2i/n}}$ 在 $n\\\\to\\\\infty$ 的极限。'), (1311, '把每项提取 $\\\\frac1n$，原和式变为 $\\\\sum_{i=1}^n\\\\frac1n\\\\,\\\\frac{e^{i/n}}{1+e^{2i/n}}$。这对应把 $[0,1]$ 等分成 $n$ 份，每段长度为 $\\\\frac1n$，取右端点 $\\\\frac in$ 的 Riemann 和。被积函数连续，所以极限为'), (1350, '$I(s,t)=t\\\\int_0^{s/t}f(tx)dx$，$s,t>0$，$f$ 连续，求对 $s$ 的导数。'), (1671, '(I) $\\\\frac23$；(II) $\\\\pi$。第一问在 $u=0$ 附近为 $O(u^3)$、在 $u=1$ 附近为常数倍 $(1-u)^{-1/2}$，均可积；第二问在任一端也为常数倍端点距离的负二分之一次幂，分别收敛。')]\nbadformats []\n"}
{"chunk_id":"b1b4c5","wall_time_seconds":0.000010583,"exit_code":1,"original_token_count":62,"output":"Traceback (most recent call last):\n  File \"/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank/.question-bank-work/check-lilin-integrals.py\", line 6, in <module>\n    from scipy.integrate import quad\nModuleNotFoundError: No module named 'scipy'\n"}

## tool · 2026-11-14T02:06:07Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"5486ba","wall_time_seconds":0.000015459,"exit_code":0,"original_token_count":2433,"output":".\n..\n302-batch-pilot.json\n302-clean-finalize.txt\n302-clean-preview.txt\n302-clean-run.txt\n302-common.txt\n302-convert.jsonl\n302-edition-check.txt\n302-first.txt\n302-hefei-1-variants.md\n302-hefei-2.md\n302-lilin-spread-diff.txt\n302-lilin-volume-1.md\n302-lilin-volume-2.md\n302-lilin-volume-3.md\n302-lilin-volume-4.md\n302-lilin-volume-5.md\n302-lilin-volume-6.md\n302-liyanfang-volume-1.md\n302-liyanfang-volume-2.md\n302-liyanfang-volume-3.md\n302-ocr-cache\n302-ocr-model\n302-older-10-1-unique-3.md\n302-older-10-1-unique-4.md\n302-older-10-1-unique-5.md\n302-older-10-1-unique-6.md\n302-older-10-1-unique-7.md\n302-older-10-1-unique-8.md\n302-older-10-1-unique-9.md\n302-older-10-1-volume-1.md\n302-older-10-1-volume-2.md\n302-older-10-1-volume-3.md\n302-older-10-1-volume-4.md\n302-older-10-1-volume-5.md\n302-older-10-1-volume-6.md\n302-older-10-1-volume-7.md\n302-older-10-1-volume-8.md\n302-older-10-1-volume-9.md\n302-older-twenty-comparison.txt\n302-primary-current.json\n302-primary-older.json\n302-proof-source\n302-spreads.json\n302-ten-two-v1.md\n302-ten-two-v2.md\n302-ten-two-v3.md\n302-ten-two-v4.md\n302-ten-two-v5.md\n302-ten-two-v6.md\n302-ten-two-v7.md\n302-ten-two-v8.md\n302-ten-two-v9.md\n302-twenty-one-unique-4.md\n302-twenty-one-unique-5.md\n302-twenty-one-unique-6.md\n302-twenty-one-zhang4.md\n302-twenty-one-zhang5.md\n302-twenty-one-zhang6.md\n302-twenty-two-zhang4.md\n302-twenty-two-zhang5.md\n302-twenty-two-zhang6.md\n302-vlm-batch.jsonl\n302-vlm-older.jsonl\n302-vlm-pilot.jsonl\n302-wu-august.md\n302-wu-basic-1-variants.md\n302-wu-basic-1.md\n302-wu-basic-2.md\n302-wu-basic-3-variants.md\n302-wu-basic-3.md\n302-wu-basic-all.md\n302-wu-july.md\n302-zhang-1-unique-1.md\n302-zhang-1-unique-2.md\n302-zhang-1-unique-3.md\n302-zhang-1-unique-4.md\n302-zhang-1-unique-5.md\n302-zhang-1-unique-6.md\n302-zhang-1-unique-7.md\n302-zhang-1-unique-8.md\n302-zhang-1-volume-1.md\n302-zhang-1-volume-2.md\n302-zhang-1-volume-3.md\n302-zhang-1-volume-4.md\n302-zhang-1-volume-5.md\n302-zhang-1-volume-6.md\n302-zhang-1-volume-7.md\n302-zhang-1-volume-8.md\n302-zhang-2-volume-1.md\n302-zhang-2-volume-2.md\n302-zhang-2-volume-3.md\n302-zhang-2-volume-4.md\n302-zhang-2-volume-5.md\n302-zhang-2-volume-6.md\n302-zhang-2-volume-7.md\n302-zhang-2-volume-8.md\n302-zhang-editions-check.txt\n302-zhang-horizontal-check.txt\n302-zhang-printed-check.txt\n302-zhang-shared.txt\n302-zhang-topic-figures.md\n__pycache__\napply-302-hefei.py\napply-302-older-twenty.py\napply-302-ten-two.py\napply-302-topic-verified.py\napply-302-twenty-two.py\napply-302-verified-paper.py\napply-302-verified-volume.py\napply-older-forty.py\nassemble-302-older-10-one.py\nassemble-302-twenty-one.py\nassemble-302-wu-basic.py\nassemble-302-zhang-1.py\nassemble-lilin-high-math.py\nassemble-linear-algebra.cjs\nassemble-older-lilin-2.py\nassemble-older-topics.py\naudit-302-ten-twenty-lost-ink.py\nbank-verify\nbatch-proof-302.py\nbuild-lilin-ipad.py\ncheck-302-source-editions.py\ncheck-bank-math.py\ncheck-bank-output.py\ncheck-lilin-high-math.cjs\ncheck-lilin-integrals.py\ncheck-lilin-ode-numeric.js\ncheck-linear-algebra.py\ncheck-topic8.py\nclean-302-questions.py\ncompare-302-older-twenty.py\ncompare-302-zhang-a4.py\ncompare-302-zhang-shared.py\nconvert-302.py\ncopy-older-topic-zhang8.py\nextract-linear-algebra.py\nfilter-302-zhang-math3.py\nhf\ninspect-302-questions.py\ninspect_lilin_high_math.py\nlayout-linear-algebra.py\nlilin-hash-stage.patch\nlilin-high-math-edits.json\nlilin-high-math-fast-sample.jsonl\nlilin-high-math-final.jsonl\nlilin-high-math-formula-crops.json\nlilin-high-math-formulas.jsonl\nlilin-high-math-ocr.jsonl\nlilin-high-math-proof.jsonl\nlilin-high-math-retry.jsonl\nlilin-high-math-sample.jsonl\nlilin-high-math-vision.jsonl\nlilin-ipad-derivatives.txt\nlilin-ipad-integrals.txt\nlilin-ipad-limits.txt\nlilin-ipad-manifest.json\nlilin-ipad-ode.txt\nlilin-ipad-verification.json\nlilin-memory-stage.patch\nlilin-proof-002-014.png\nlilin-proof-015-022.png\nlilin-proof-023-036.png\nlilin-proof-064-089.png\nlilin-proof-091-127.png\nlilin-proof-128-158.png\nlilin-proof-171-208.png\nlilin-proof-194-228.png\nlilin-proof-220-246.png\nlilin-proof-245-260.png\nlilin-proof-265-307.png\nlilin-proof-309-353.png\nlilin-proof-334-384.png\nlilin-proof-345-395.png\nlilin-proof-397-443.png\nlilin-proof-429-455.png\nlilin-proof-466-505.png\nlilin-proof-506-541.png\nlilin-proof-534-585.png\nlilin-proof-545-608.png\nlilin-proof-571-606.png\nlilin-proof-617-653.png\nlilin-proof-630-683.png\nlilin-proof-643-718.png\nlilin-proof-665-747.png\nlilin-proof-698-708.png\nlilin-proof-710-746.png\nlilin-proof-diff.py\nlilin-proof-early.png\nlilin-proof-final.png\nlilin-proof-images.py\nlilin-proof-marked.png\nlilin-proof-vision.py\nlinear-algebra-final-math.log\nlinear-algebra-ocr-report.json\nlinear-algebra-proof\nlinear-algebra-review-ocr.jsonl\nlinear-algebra-source-14.png\nnotation-after\nnotation-before\nnpm\nocr-302\nocr-302-spreads.py\nocr-302.swift\nocr-lilin-high-math.py\nolder-forty-candidates.py\nolder-forty-early-1.md\nolder-forty-early-2.md\nolder-forty-early-3.md\nolder-forty-early-4.md\nolder-forty-early-5.md\nolder-forty-early-6.md\nolder-forty-early-7.md\nolder-forty-early-8.md\nolder-forty-lilin-1.md\nolder-forty-lilin-2.md\nolder-forty-lilin-3.md\nolder-forty-lilin-4.md\nolder-forty-lilin-5.md\nolder-forty-lilin-6.md\nolder-forty-zhang-1.md\nolder-forty-zhang-2.md\nolder-forty-zhang-3.md\nolder-forty-zhang-4.md\nolder-forty-zhang-5.md\nolder-forty-zhang-6.md\nolder-forty-zhang-7.md\nolder-forty-zhang-8.md\nolder-lilin-1-v1.md\nolder-lilin-1-v2.md\nolder-lilin-1-v3.md\nolder-lilin-1-v4.md\nolder-lilin-2-v1.md\nolder-lilin-2-v2.md\nolder-lilin-2-v3.md\nolder-lilin-2-v4.md\nolder-lilin-crop.py\nolder-topic-1-chaoyue-v10.md\nolder-topic-1-chaoyue-v2.md\nolder-topic-1-chaoyue-v6.md\nolder-topic-1-chaoyue-v7.md\nolder-topic-1-chaoyue-v8.md\nolder-topic-1-chaoyue-v9.md\nolder-topic-1-lilin-v1.md\nolder-topic-1-lilin-v2.md\nolder-topic-1-lilin-v3.md\nolder-topic-1-lilin-v4.md\nolder-topic-1-zhang4-v1.md\nolder-topic-1-zhang4-v2.md\nolder-topic-1-zhang4-v3.md\nolder-topic-1-zhang4-v4.md\nolder-topic-1-zhang8-v1.md\nolder-topic-1-zhang8-v2.md\nolder-topic-1-zhang8-v3.md\nolder-topic-1-zhang8-v4.md\nolder-topic-1-zhang8-v5.md\nolder-topic-1-zhang8-v6.md\nolder-topic-1-zhang8-v7.md\nolder-topic-1-zhang8-v8.md\nolder-topic-2-chaoyue-v1.md\nolder-topic-2-chaoyue-v2.md\nolder-topic-2-chaoyue-v3.md\nolder-topic-2-lilin-v1.md\nolder-topic-2-lilin-v2.md\nolder-topic-2-lilin-v3.md\nolder-topic-2-lilin-v4.md\nolder-topic-2-zhang4-v1.md\nolder-topic-2-zhang4-v2.md\nolder-topic-2-zhang4-v3.md\nolder-topic-2-zhang4-v4.md\nolder-topic-2-zhang8-v1.md\nolder-topic-2-zhang8-v2.md\nolder-topic-2-zhang8-v3.md\nolder-topic-2-zhang8-v4.md\nolder-topic-2-zhang8-v5.md\nolder-topic-2-zhang8-v6.md\nolder-topic-2-zhang8-v7.md\nolder-topic-2-zhang8-v8.md\nolder-topic-candidate-1-chaoyue-v1.md\nolder-topic-candidate-1-chaoyue-v10.md\nolder-topic-candidate-1-chaoyue-v2.md\nolder-topic-candidate-1-chaoyue-v3.md\nolder-topic-candidate-1-chaoyue-v4.md\nolder-topic-candidate-1-chaoyue-v5.md\nolder-topic-candidate-1-chaoyue-v6.md\nolder-topic-candidate-1-chaoyue-v7.md\nolder-topic-candidate-1-chaoyue-v8.md\nolder-topic-candidate-1-chaoyue-v9.md\nolder-topic-candidate-1-lilin-v1.md\nolder-topic-candidate-1-lilin-v2.md\nolder-topic-candidate-1-lilin-v3.md\nolder-topic-candidate-1-lilin-v4.md\nolder-topic-candidate-1-zhang4-v1.md\nolder-topic-candidate-1-zhang4-v2.md\nolder-topic-candidate-1-zhang4-v3.md\nolder-topic-candidate-1-zhang4-v4.md\nolder-topic-candidate-1-zhang8-v1.md\nolder-topic-candidate-1-zhang8-v2.md\nolder-topic-candidate-1-zhang8-v3.md\nolder-topic-candidate-1-zhang8-v4.md\nolder-topic-candidate-1-zhang8-v5.md\nolder-topic-candidate-1-zhang8-v6.md\nolder-topic-candidate-1-zhang8-v7.md\nolder-topic-candidate-1-zhang8-v8.md\nolder-topic-candidate-2-chaoyue-v1.md\nolder-topic-candidate-2-chaoyue-v10.md\nolder-topic-candidate-2-chaoyue-v2.md\nolder-topic-candidate-2-chaoyue-v3.md\nolder-topic-candidate-2-chaoyue-v4.md\nolder-topic-candidate-2-chaoyue-v5.md\nolder-topic-candidate-2-chaoyue-v6.md\nolder-topic-candidate-2-chaoyue-v7.md\nolder-topic-candidate-2-chaoyue-v8.md\nolder-topic-candidate-2-chaoyue-v9.md\nolder-topic-candidate-2-lilin-v1.md\nolder-topic-candidate-2-lilin-v2.md\nolder-topic-candidate-2-lilin-v3.md\nolder-topic-candidate-2-lilin-v4.md\nolder-topic-candidate-2-zhang4-v1.md\nolder-topic-candidate-2-zhang4-v2.md\nolder-topic-candidate-2-zhang4-v3.md\nolder-topic-candidate-2-zhang4-v4.md\nolder-topic-candidate-2-zhang8-v1.md\nolder-topic-candidate-2-zhang8-v2.md\nolder-topic-candidate-2-zhang8-v3.md\nolder-topic-candidate-2-zhang8-v4.md\nolder-topic-candidate-2-zhang8-v5.md\nolder-topic-candidate-2-zhang8-v6.md\nolder-topic-candidate-2-zhang8-v7.md\nolder-topic-candidate-2-zhang8-v8.md\nprepare-older-forty-early.py\nprepare-older-topic-candidates.py\nproof-302-ocr.py\nproof-katex\nproof-linear-algebra.py\nproof-venv\npycache\nremove-302-standalone-math3.py\nrender-302-older.py\nrender-302-zhang-a4-outliers.py\nrender-302-zhang-horizontal-check.py\nrender-302-zhang-printed.py\nrender-302-zhang-year-differences.py\nrender-proof-302-doing-books.py\nrender-proof-302-lilin-a4.py\nrender-proof-302-official.py\nrender-proof-302-remaining-lilin.py\nrender-proof-302-variants.py\nrender-proof-302-wu.py\nrender-proof-302-zhang.py\nrender-proof-302.py\nswift-cache\ntectonic-cache\ntest-302-batch-ocr.py\ntopic8-other-sections.json\nuv\nverify-302-lilin-spread.py\nverify-302-math.cjs\nverify-302-ten-twenty-two.py\nverify-302-zhang-editions.py\nverify-302-zhang-horizontal.py\nverify-302-zhang-printed.py\nverify-302.py\nverify-lilin-ipad.py\nverify-mean-value.py\nverify-notation.py\nvision-lilin-high-math.py\n中值定理阶段模拟卷1.log\n中值定理阶段模拟卷1.pdf\n中值定理阶段模拟卷2.log\n中值定理阶段模拟卷2.pdf\n中值定理阶段模拟卷3.log\n中值定理阶段模拟卷3.pdf\n李林高数上册分节题集.log\n李林高数上册分节题集.pdf\n444\n"}

## tool · 2026-11-14T02:06:11Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"5d029a","wall_time_seconds":0.015799041,"exit_code":0,"original_token_count":2,"output":"1.18.1\n"}

## tool · 2026-11-14T02:06:55Z


Script completed
Wall time 0.8 seconds
Output:

{}
{"chunk_id":"33de6e","wall_time_seconds":0.575332541,"exit_code":0,"original_token_count":91,"output":"{\n  \"status\": \"passed\",\n  \"type\": \"mathematical-verification\",\n  \"message\": \"题号、数学环境与选定数值复算通过\",\n  \"suggestion\": \"结合最终编译和视觉检查交付\",\n  \"source_entries\": 114,\n  \"derivative_checks\": 24,\n  \"integral_checks\": 17,\n  \"max_derivative_error\": 5.8356707910434125e-08,\n  \"max_integral_error\": 1.1535217225855376e-13\n}\n"}

## tool · 2026-11-14T02:07:18Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"6b66ff","wall_time_seconds":0.000011375,"exit_code":1,"original_token_count":30,"output":"Traceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nModuleNotFoundError: No module named 'sympy'\n"}
{"chunk_id":"d3c4e7","wall_time_seconds":0.000009042,"exit_code":0,"original_token_count":64,"output":"{'entries': 114, 'included': 111, 'macro_lines': 444, 'grades': {'2': 37, '3': 66, '1': 3, '4': 5, '0': 3}, 'sections': {'3.2': 26, '3.3': 41, '3.1': 14, '3.5': 15, '2.5': 2, '1.2': 1, '3.4': 12, 'skip': 3}, 'braces': 'balanced', 'fractions': 'passed'}\n"}

## tool · 2026-11-14T02:07:25Z




## tool · 2026-11-14T02:07:50Z


Script completed
Wall time 0.5 seconds
Output:

{"chunk_id":"b49b0f","wall_time_seconds":0.30555425,"exit_code":0,"original_token_count":17,"output":"{'extra_derivative_cases': 11, 'max_error': 7.324190143265241e-10}\n"}

## tool · 2026-11-14T02:07:55Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"4937b5","wall_time_seconds":0.000020583,"exit_code":0,"original_token_count":1347,"output":"@@ 1534 3.3 3\n\\Known\n四个乘积或复合函数积分，目标为全部原函数。\n\\Method\n多项式或对数求导能降次，适合分部；对数中的 $x$ 及反三角函数可先换元，再分部。\n\\Derive\n(1) 选 $u=x+1$、$dv=e^{3x}dx$，则 $du=dx,v=\\frac13e^{3x}$。因此 $I=\\frac{(x+1)e^{3x}}3-\\frac13\\int e^{3x}dx=\\frac{(x+1)e^{3x}}3-\\frac{e^{3x}}9+C$。\n\n(2) 选 $u=(\\ln x)^2$，$dv=x^{-2}dx$。得到 $-\\frac{(\\ln x)^2}{x}+2\\int\\frac{\\ln x}{x^2}\\,dx$。再用 $u=\\ln x$ 分部一次，结果 $-\\frac{(\\ln x)^2+2\\ln x+2}{x}+C$。\n\n(3) 先令 $t=\\ln x$，$dx=e^tdt$。设 $I=\\int e^t\\sin tdt$，第一次分部得 $I=e^t\\sin t-\\int e^t\\cos tdt$；余项分部得 $\\int e^t\\cos tdt=e^t\\cos t+I$。故 $2I=e^t(\\sin t-\\cos t)$，结果为 $\\frac x2[\\sin(\\ln x)-\\cos(\\ln x)]+C$。\n\n(4) 令 $t=\\arcsin x$，得到 $\\int t^2\\cos t\\,dt$。先分部得 $t^2\\sin t-2\\int t\\sin t\\,dt$，再分部得 $t^2\\sin t+2t\\cos t-2\\sin t$。结果为 $x(\\arcsin x)^2+2\\sqrt{1-x^2}\\arcsin x-2x+C$。\n\\Check\n四问答案如上。(2) 求导时令 $P=(\\ln x)^2+2\\ln x+2$，有 $[-\\frac Px]'=\\frac{P-xP'}{x^2}=\\frac{(\\ln x)^2}{x^2}$。(4) 两个含 $\\arcsin x$ 的交叉项抵消。对数题要求 $x>0$，(4) 内部 $|x|<1$。\n@@ 1542 3.3 3\n\\Known\n六个不定积分，包含分母导数、乘积导数、二次因式分解与三角有理式。\n\\Method\n先识别直接求导能得到的结构；剩余有理式用分解，三角分式用半角代换。\n\\Derive\n(1) 令 $u=x^2+3x-10$，$du=(2x+3)dx$，原积分为 $\\int\\frac{du}u=\\ln|x^2+3x-10|+C$。\n\n(2) 展开得 $(\\tan x+1)^2=\\sec^2 x+2\\tan x$。由 $(e^{2x}\\tan x)'=e^{2x}\\sec^2 x+2e^{2x}\\tan x$，故原函数为 $e^{2x}\\tan x+C$。\n\n(3) 写成 $\\frac12[\\frac1{x^2-\\sqrt2 x+1}+\\frac1{x^2+\\sqrt2 x+1}]$，因为两个分母的乘积为 $x^4+1$。配方后得 $\\frac1{\\sqrt2}[\\arctan(\\sqrt2 x-1)+\\arctan(\\sqrt2 x+1)]+C$。\n\n(4) 分子 $x$ 可以写成 $(1+x)-1$，对应 $\\frac{d}{dx}(\\frac{e^x}{1+x})=\\frac{xe^x}{(1+x)^2}$，故原函数为 $\\frac{e^x}{1+x}+C$。\n\n(5) $\\frac1{1+\\cos x}$ 是 $\\tan\\frac x2$ 的导数，$\\frac{\\sin x}{1+\\cos x}=\\tan\\frac x2$。两项正好拼出乘积导数，结果 $x\\tan\\frac x2+C$。\n\n(6) 原分式是 $\\frac{2}{1+\\sin x-\\cos x}-1$。令 $t=\\tan\\frac x2$，用 $\\sin x=\\frac{2t}{1+t^2},\\cos x=\\frac{1-t^2}{1+t^2},dx=\\frac{2dt}{1+t^2}$，第一项化为 $\\frac{2}{t(t+1)}dt=2(\\frac1t-\\frac1{t+1})dt$。积分得 $2\\ln|\\frac t{t+1}|-x+C$，即 $2\\ln\\left|\\frac{\\sin\\frac x2}{\\sin\\frac x2+\\cos\\frac x2}\\right|-x+C$。\n\\Check\n答案逐问如上。(3) 两个反正切导数分别为对应二次式倒数的一半，通分得原分式。(5) 乘积求导为 $\\tan\\frac x2+\\frac{x}{1+\\cos x}$。(6) 半角参数无定义处可用最后表达式延拓；所有答案只在原式连续区间内使用。\n@@ 1583 3.3 3\n\\Known\n六个不定积分，逐问求原函数并保留实数定义域。\n\\Method\n二次根式先配方，复合函数找内层导数，根号与指数用换元转为有理式。\n\\Derive\n(I) 配方 $x(4-x)=4-(x-2)^2$，用反正弦原函数，得 $\\arcsin\\frac{x-2}{2}+C$。\n\n(II) 指数 $x+\\frac1x$ 的导数就是前面的括号，故为 $e^{x+\\frac1x}+C$。\n\n(III) 配方 $x(x+2)=(x+1)^2-1$。令 $u=x+1$，$\\ln|u+\\sqrt{u^2-1}|$ 的导数为 $\\frac1{\\sqrt{u^2-1}}$。故结果 $\\ln|x+1+\\sqrt{x(x+2)}|+C$。\n\n(IV) $u=1+x^3$，$x^5dx=\\frac{u-1}{3}du$，积分两项幂函数，得 $\\frac{u^{\\frac53}}5-\\frac{u^{\\frac23}}2+C$，分数次幂按实立方根理解。\n\n(V) $u=\\sqrt{\\sin x}$ 后化成 $\\frac{2du}{1-u^4}=[\\frac1{1-u^2}+\\frac1{1+u^2}]du$，故为 $\\frac12\\ln|\\frac{1+u}{1-u}|+\\arctan u+C$。\n\n(VI) $u=e^x$ 可约掉一个 $e^x$，得到 $\\frac{u^2+1}{u^4+1}du$。分母分解成 $(u^2-\\sqrt2u+1)(u^2+\\sqrt2u+1)$，分式等于两个因式倒数之和的一半。配方后得 $\\frac1{\\sqrt2}[\\arctan(\\sqrt2u-1)+\\arctan(\\sqrt2u+1)]+C$。\n\\Check\n(I) 求导为 $[4-(x-2)^2]^{-\\frac12}$；(II) 用链式法则直接恢复原式；(IV) 求导得 $(1+x^3)^{-\\frac13}x^5$。(V) $du=\\frac{\\cos x}{2\\sqrt{\\sin x}}dx$，从而分母转换为 $1-u^4$，要求 $\\sin x>0,\\cos x\\ne0$；(VI) 两个二次因式都恒正。各答案中的代换变量均按本问定义代回。\n@@ 1588 3.3 3\n\\Known\n五个不定积分，含反三角、圆形根式与分式根式。\n\\Method\n反三角复合式找导数；$4-x^2$ 用三角代换，其余根号可整体换元降低次数。\n\\Derive\n(I) 令 $u=\\arctan\\sqrt x$，则 $du=\\frac{dx}{2(1+x)\\sqrt x}$。原式是 $2u\\,du$，得 $(\\arctan\\sqrt x)^2+C$。\n\n(II) 令 $x=2\\sin t$、$t=\\arcsin\\frac x2$，得到 $16\\sin^2t\\cos^2t\\,dt=2(1-\\cos4t)\\,dt$，结果为 $2t-\\frac12\\sin4t+C$。\n\n(III) 分子拆成 $(2x+2)-1$，第一项是分母导数，第二项把分母配成 $(x+1)^2+4$。结果 $\\ln(x^2+2x+5)-\\frac12\\arctan\\frac{x+1}{2}+C$。\n\n(IV) 令 $u=\\sqrt{4+x^2}$，则 $du=\\frac{x}{u}dx$，余下的 $x^2=u^2-4$。积分得 $\\frac{u^3}{3}-4u+C$。\n\n(V) 根号取作新变量 $u=\\sqrt{\\frac{1-x}{1+x}}$，解出 $x=\\frac{1-u^2}{1+u^2}$。原式化为 $-\\frac{4u^2}{(1-u^2)^2}du$。把它写成 $-2[\\frac{d}{du}(\\frac{u}{1-u^2})-\\frac1{1-u^2}]du$，积分得 $-\\frac{2u}{1-u^2}+\\ln|\\frac{1+u}{1-u}|+C$。\n\\Check\n(II) 最终可写为 $2\\arcsin\\frac x2-\\frac{x(2-x^2)\\sqrt{4-x^2}}4+C$；(IV) 代回 $u=\\sqrt{4+x^2}$，求导得 $\\frac{x}{u}(u^2-4)=\\frac{x^3}u$。(V) $-1<x<1,x\\ne0$，需代回 $u=\\sqrt{\\frac{1-x}{1+x}}$，对数的绝对值不能删去。\n"}

## tool · 2026-11-14T02:08:49Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T02:09:05Z


Script completed
Wall time 0.6 seconds
Output:

{"chunk_id":"909a7b","wall_time_seconds":0.2783365,"exit_code":0,"original_token_count":91,"output":"{\n  \"status\": \"passed\",\n  \"type\": \"mathematical-verification\",\n  \"message\": \"题号、数学环境与选定数值复算通过\",\n  \"suggestion\": \"结合最终编译和视觉检查交付\",\n  \"source_entries\": 114,\n  \"derivative_checks\": 24,\n  \"integral_checks\": 17,\n  \"max_derivative_error\": 5.8356707910434125e-08,\n  \"max_integral_error\": 1.1535217225855376e-13\n}\n"}
{"chunk_id":"80dd9e","wall_time_seconds":0.000008542,"exit_code":0,"original_token_count":13,"output":"114 entries, 111 included, 444 macro lines; passed\n"}
{"chunk_id":"deda39","wall_time_seconds":0.000008,"exit_code":0,"original_token_count":2338,"output":"@@ 197 1.4 3\n\\Known\n两问要求按渐近阶数确定指数参数 $n$；第二问还需辨明它是否被限制为整数。\n\\Method\n先求每个表达式的首个非零幂次。等价无穷小要求阶数相同且系数比为 $1$，高阶无穷小则要求商趋于零；参数的定义域也必须说明。\n\\Derive\n（1）先提取外层指数差 $\\mathrm e^{\\tan x}-\\mathrm e^x=\\mathrm e^x(\\mathrm e^{\\tan x-x}-1)\\sim\\tan x-x$。再用\n\\[\n\\tan x-x=\\frac{\\sin x-x\\cos x}{\\cos x}\\sim\\frac{x^3}{3}.\n\\]\n分子的系数来自 $\\sin x=x-\\frac{x^3}6+o(x^3)$ 与 $x\\cos x=x-\\frac{x^3}2+o(x^3)$。故 $n=3$。\n\n（2）先在 $x>0$ 一侧讨论实数 $n$。若 $n\\le0$，$\\sin(x^n)$ 不会让 $x\\sin(x^n)$ 成为比 $x^2$ 高阶的量，因此需 $n>0$。此时 $(1-\\cos x)\\ln(1+x^2)\\sim\\frac{x^4}2$，$x\\sin(x^n)\\sim x^{n+1}$，$\\mathrm e^{x^2}-1\\sim x^2$。幂的指数越大，小量消失越快，所以需 $4>n+1>2$，即 $1<n<3$。若补充 $n$ 为整数，才得到唯一的 $n=2$。原题未写整数条件；允许非整数时还要按 $x^n$ 的实数定义域解释双侧趋近。\n\\Check\n第一问 $n=3$；第二问在正侧实数幂解释下 $1<n<3$，若限整数才是 $n=2$。原题没有整数条件时不能只保留 $2$，双侧幂的实数定义也应另作约定。\n\n@@ 332 1.5 3\n\\Known\n$f$ 连续且非零，$g$ 有间断点，要求判断和、差、商及复合函数能否必有间断点。\n\\Method\n对“必有”的断言，可假设新函数连续并用代数关系还原 $g$，推出矛盾；对“不一定”则给具体反例。商还必须检查分母与实际定义域。\n\\Derive\n（1）必有。若 $f\\pm g$ 在 $g$ 的某个间断点 $c$ 连续，则用它减去连续的 $f$ 可推出 $g$ 在 $c$ 连续，矛盾。\n\n（2）必有。若 $\\frac gf$ 在 $c$ 连续，乘以连续的 $f$ 又会推出 $g$ 连续。$f$ 处处非零，保证商有定义。\n\n（3）若商在全实轴有定义，即 $g$ 处处非零，则必有间断点。反设 $h=\\frac fg$ 在 $g$ 的间断点 $c$ 连续，因为 $h(c)\\ne0$，倒数 $\\frac1h$ 在该点连续，从而 $g=f\\frac1h$ 连续，矛盾。原条件未排除 $g$ 的零点，因此仍需说明商的定义域。教材定义5.2要求某个单侧邻域内有定义：例如 $f\\equiv1$，$g$ 在有理数处为 $1$、无理数处为 $0$，则商仅在有理数上有定义，任何点都缺少完整单侧邻域，不能按该定义判为间断点。可去缺点在教材中仍算间断点。\n\n（4）不一定。取 $f\\equiv1$，即使 $g$ 有跳跃，复合函数也恒为 $1$。\n\\Check\n和差与 $\\frac gf$ 必有相应间断；$\\frac fg$ 的论证需商在相应邻域有定义。复合函数可为常值。可去缺点仍属于间断点，不能仅从约分后的延拓判断原函数连续。\n\n@@ 478 2.5 3\n\\Known\n四个小问依次涉及负无穷远根式、基本幂极限的偏差、指数差、以及二阶差的比值。\n\\Method\n每问先识别抵消来源：负方向要用 $|x|$ 提取根式；幂式取对数保留下一阶；指数差用中值定理；根式差用共轭。这样所有小问都能化为明确的主项比值。\n\\Derive\n（I）$x$ 为负，分子分母同除 $|x|=-x$。两个根式分别化为 $\\sqrt{4+\\frac1x-\\frac1{x^2}}$、$\\sqrt{1+\\frac{\\sin x}{x^2}}$，其余两项化为 $-1-\\frac1x$。故极限为 $\\frac{2-1}{1}=1$。\n\n（II）先改写幂：$(1+x)^{\\frac1x}=\\mathrm e^{1+u}$，其中 $u=\\frac{\\ln(1+x)}x-1=-\\frac x2+o(x)$。因此分子 $\\mathrm e(\\mathrm e^u-1)\\sim-\\frac{\\mathrm e x}{2}$，除以 $\\sin x\\sim x$ 得 $-\\frac{\\mathrm e}{2}$。\n\n（III）由中值定理，分子为 $\\mathrm e^\\xi(\\tan x-x)$，其中 $\\xi$ 介于 $x$ 与 $\\tan x$ 之间，所以 $\\xi\\to0$。而 $\\tan x-x=\\frac{\\sin x-x\\cos x}{\\cos x}$，约去相同因子后得极限 $1$。\n\n（IV）分子 $x-\\ln(1+x)\\sim\\frac{x^2}2$。分母乘共轭式后为 $\\frac{x\\sin x+(1-\\cos x)}{\\sqrt{1+x\\sin x}+\\sqrt{\\cos x}}\\sim\\frac{3x^2}{4}$。两者相除得 $\\frac23$。\n\\Check\n四问依次为 $1,-\\frac{\\mathrm e}2,1,\\frac23$。第II问底数幂的极限是 $\\mathrm e$，但题目计算的是偏离 $\\mathrm e$ 后除以 $\\sin x$ 的极限，不能把前者直接作为答案。\n\n@@ 488 1.3 3\n\\Known\n六问分别含三角趋近点、根式差、二阶比值、有限指数平均的幂、反正切差以及无穷远幂。\n\\Method\n把非零趋近点或无穷远换成零点；根式有理化，幂式先取对数，函数值差用中值定理。每个换元都先写清新变量与原变量的关系。\n\\Derive\n（I）令 $t=\\frac\\pi4-x\\to0$，则 $2x=\\frac\\pi2-2t$，所以 $\\tan2x=\\cot2t$。在去心邻域，\n\\[\n\\tan2x\\tan\\left(\\frac\\pi4-x\\right)\n=\\frac{\\cos2t}{\\sin2t}\\frac{\\sin t}{\\cos t}\n=\\frac{\\cos2t}{2\\cos^2t}\\longrightarrow\\frac12.\n\\]\n约去 $\\sin t$ 合法，因为只在充分接近零且非零的 $t$ 上求极限。\n\n（II）两个根式都趋于 $1$，因此先分别减 $1$，再有理化：\n\\[\n\\frac{\\sqrt{1+x}+\\sqrt{1-x}-2}{x}\n=\\frac1{\\sqrt{1+x}+1}-\\frac1{\\sqrt{1-x}+1}\\longrightarrow\\frac12-\\frac12=0.\n\\]\n注意第二个有理化的分子是 $-x$，所以两项之间是减号。\n\n（III）分子、分母都除以 $x^2$。利用 $1-\\cos2x=2\\sin^2x$，分子变为 $5-4(\\frac{\\sin x}x)^2\\to1$。分母变为 $3x+4\\frac{\\sin(x^2)}{x^2}\\to4$。分母极限非零，故商趋于 $\\frac14$。原题的 $\\sin x^2$ 表示 $\\sin(x^2)$，这里两处小自变量不可混淆。\n\n（IV）将底数减去 $1$ 记为 $u=\\frac1n\\sum_{k=1}^n(\\mathrm e^{kx}-1)$。因为 $n$ 固定，有限项的极限可相加，得到\n\\[\n\\frac ux=\\frac1n\\sum_{k=1}^n k\\frac{\\mathrm e^{kx}-1}{kx}\n\\longrightarrow\\frac1n\\sum_{k=1}^n k=\\frac{n+1}2.\n\\]\n底数在零点附近为正，故设原幂为 $Y$，有 $\\ln Y=\\frac{\\ln(1+u)}u\\frac ux\\to\\frac{n+1}2$。原极限为 $\\mathrm e^{\\frac{n+1}2}$。\n\n（V）对 $\\arctan t$ 在 $\\frac1{x+1}$ 与 $\\frac1x$ 之间应用 Lagrange 定理。存在其中的 $\\xi$ 使两函数值之差等于\n\\[\n\\frac1{1+\\xi^2}\\left(\\frac1x-\\frac1{x+1}\\right)\n=\\frac1{1+\\xi^2}\\frac1{x(x+1)}.\n\\]\n乘题中的 $x^2$ 后得到 $\\frac1{1+\\xi^2}\\frac{x}{x+1}$。两端都趋于 $0$，所以 $\\xi\\to0$；另一个因子趋于 $1$，结果为 $1$。\n\n（VI）令 $t=\\frac1x\\to0$，指数 $x^2=\\frac1{t^2}$，底数为 $1+u$，其中 $u=t^2+\\cos t-1$。由 $\\frac{1-\\cos t}{t^2}\\to\\frac12$ 得\n\\[\n\\frac u{t^2}=1-\\frac{1-\\cos t}{t^2}\\longrightarrow\\frac12,\n\\qquad\n\\ln Y=\\frac{\\ln(1+u)}u\\cdot\\frac u{t^2}\\longrightarrow\\frac12.\n\\]\n最后还原指数，得到 $\\mathrm e^{\\frac12}$。\n\\Check\n六问依次为 $\\frac12,0,\\frac14,\\mathrm e^{\\frac{n+1}2},1,\\sqrt{\\mathrm e}$。第IV问的 $n$ 是固定整数，不能在求 $x$ 的极限时再让它无穷大；第V问须检查中间点趋于零。\n\n@@ 1236 2.4 5\n\\Known\n$f$ 二阶可导，$f(x_0)=f(1)=0$，先证明目标一阶组合有两个不同零点，再在额外符号条件下证明 $f''$ 有内部零点。\n\\Method\n第一问把组合看作 $(xf)'$，利用三个辅助函数零点作两次 Rolle。第二问先制造 $f''$ 的负值点，再用右侧正值点围出 $f'$ 的内部最小点；这条路径不需要擅自增加 $f''$ 连续的假设。\n\\Derive\n（I）令 $F(x)=xf(x)$，则 $F(0)=F(x_0)=F(1)=0$。分别在 $[0,x_0]$ 与 $[x_0,1]$ 用 Rolle 定理，得到 $\\xi_1\\in(0,x_0)$、$\\xi_2\\in(x_0,1)$，且 $F'(\\xi_i)=\\xi_i f'(\\xi_i)+f(\\xi_i)=0$。两点在不同区间，保证不相等。\n\n（II）在 $[0,x_0]$ 上用 Lagrange 定理，得 $u\\in(0,x_0)$ 满足 $f'(u)=\\frac{-f(0)}{x_0}>0$。在 $[x_0,1]$ 上用 Rolle 定理，得 $v\\in(x_0,1)$ 满足 $f'(v)=0$。再对 $f'$ 在 $[u,v]$ 用 Lagrange 定理，找到 $w\\in(u,v)$，使 $f''(w)=\\frac{-f'(u)}{v-u}<0$。\n\n取 $z\\in(v,1)$，则 $w<z$ 且 $f''(z)>0$。连续函数 $f'$ 在 $[w,z]$ 取得最小值。因为 $f''(w)<0$，从 $w$ 向右走一小段会使 $f'$ 更小，所以最小值不在 $w$。因为 $f''(z)>0$，从 $z$ 向左走一小段也会使 $f'$ 更小，所以最小值也不在 $z$。因此最小值取在某个内点 $\\eta$，由 Fermat 定理得 $(f')'(\\eta)=f''(\\eta)=0$。这个证明无需假设 $f''$ 连续。\n\\Check\n第一问的两个点分居 $x_0$ 两侧，故不同。第二问的 $\\eta$ 是 $f'$ 的内部极小值点，Fermat 定理给 $f''(\\eta)=0$；仅由 $f''$ 一正一负而直接使用介值定理，会遗漏它未必连续的条件问题。\n\n@@ 1244 3.3 4\n\\Known\n$f(0)=f(1)=0$ 且二阶导数连续，设 $M=\\max_{[0,1]}|f''|$，需证明整个区间上 $|f'|\\le\\frac M2$。\n\\Method\n直接用某个 Rolle 点只易得到界 $M$。利用 $f'$ 的积分平均值为零，把每个 $f'(x)$ 写成它与全区间导数值之差的积分，再用二阶导数界控制这些差值，可得到更好的常数。\n\\Derive\n因为 $f(1)-f(0)=0$，微积分基本公式给出 $\\int_0^1 f'(t)\\,\\mathrm dt=0$。因此对固定 $x\\in[0,1]$，\n\\[\nf'(x)=\\int_0^1[f'(x)-f'(t)]\\,\\mathrm dt.\n\\]\n由 Lagrange 定理和 $|f''|\\le M$，有 $|f'(x)-f'(t)|\\le M|x-t|$。积分并用三角不等式，得到\n\\[\n|f'(x)|\\le M\\int_0^1|x-t|\\,\\mathrm dt\n=\\frac M2[x^2+(1-x)^2]\\le\\frac M2.\n\\]\n最后一步用 $x^2+(1-x)^2=1-2x(1-x)\\le1$。这个估计在两端也成立；$M=0$ 时表示 $f'$ 恒为零，同样包含在证明中。\n\\Check\n对每个 $x\\in[0,1]$ 均有 $|f'(x)|\\le\\frac M2$。取 $f(x)=\\frac M2x(x-1)$ 可在两端取得等号，说明系数 $\\frac12$ 不能统一缩小；$M=0$ 时原函数恒为零，也满足结论。\n\n"}

## tool · 2026-11-14T02:09:11Z




## tool · 2026-11-14T02:09:15Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"77df08","wall_time_seconds":0.000008792,"exit_code":0,"original_token_count":659,"output":"% SOURCE line=488 pdf_page=74 section=1.3\n\n\\Question{34}{第1章 · 解答题 · 第 3 题}\n\n求下列极限：\n\n（I）$\\lim_{x\\to\\frac{\\pi}{4}}\\tan2x\\cdot\\tan\\left(\\frac{\\pi}{4}-x\\right)$； （II）$\\lim_{x\\to0}\\frac{\\sqrt{1+x}+\\sqrt{1-x}-2}{x}$；\n\n（III）$\\lim_{x\\to0}\\frac{5x^{2}-2(1-\\cos2x)}{3x^{3}+4\\sin x^{2}};\\quad$ （IV）$\\lim_{x\\to0}\\left(\\frac{\\mathrm{e}^{x}+\\mathrm{e}^{2x}+\\cdots+\\mathrm{e}^{nx}}{n}\\right)^{\\frac{1}{x}}$；\n\n（V）$\\lim_{x\\to\\infty}x^{2}\\left(\\arctan\\frac{1}{x}-\\arctan\\frac{1}{1+x}\\right)$； （VI）$\\lim_{x\\to\\infty}\\left(\\frac{1}{x^{2}}+\\cos\\frac{1}{x}\\right)^{x^{2}}$。\n\n\\vfill\n\n\n% SOURCE line=197 pdf_page=31 section=1.4\n\n\\Question{42}{第1章 · 例题第2组 · 例 17}\n\n（1）当$x\\to0$时，$(e^{\\tan x}-e^{x})$与$x^{n}$是同阶无穷小，求$n$；\n\n(2) 当 $x \\to 0$ 时，$(1 - \\cos x) \\ln(1 + x^{2})$ 是比 $x \\sin x^{n}$ 高阶的无穷小，而 $x \\sin x^{n}$ 是比 $(e^{x^{2}} - 1)$ 高阶的无穷小，求 n.\n\n\\vfill\n\n\n% SOURCE line=332 pdf_page=52 section=1.5\n\n\\Question{52}{第1章 · 例题第4组 · 例 1}\n\n设 $f(x)$ 和 $g(x)$ 在 $(-\\infty,+\\infty)$ 内有定义，$f(x)$ 为连续函数，且 $f(x) \\neq 0$，$g(x)$ 有间断点，讨论下列函数是否必有间断点：\n\n(1)$f(x)\\pm g(x)$; (2)$\\frac{g(x)}{f(x)}$; (3)$\\frac{f(x)}{g(x)}$; (4)$f[g(x)]$.\n\n\\vfill\n\n\n% SOURCE line=1236 pdf_page=196 section=2.4\n\n\\Question{161}{第3章 · 解答题 · 第 25 题}\n\n设 $f(x)$ 在 $[0,1]$ 上有二阶导数，且 $f(1)=0$，方程 $f(x)=0$ 在 $(0,1)$ 内有实根 $x_{0}$。\n\n（I）证明：存在 $\\xi_{1}\\neq\\xi_{2}\\in(0,1)$，使得 $\\xi_{1}f^{\\prime}\\left(\\xi_{1}\\right)+f\\left(\\xi_{1}\\right)=\\xi_{2}f^{\\prime}\\left(\\xi_{2}\\right)+f\\left(\\xi_{2}\\right)=0;$\n\n（II）证明：若 $f(0)<0$ ，且 $\\forall x\\in(x_{0},1)$，有 $f^{\\prime\\prime}(x)>0$ ，则存在一点 $\\eta\\in(0,1)$，使得 $f^{\\prime\\prime}(\\eta)=0$ 。\n\n\\vfill\n\n\n% SOURCE line=478 pdf_page=72 section=2.5\n\n\\Question{168}{第1章 · 解答题 · 第 1 题}\n\n求下列极限：\n\n（I）$\\lim_{x\\to-\\infty}\\frac{\\sqrt{4x^{2}+x-1}+x+1}{\\sqrt{x^{2}+\\sin x}}$; （II）$\\lim_{x\\to0}\\frac{(1+x)^{\\frac{1}{x}}-\\mathrm{e}}{\\sin x}$; （III）$\\lim_{x\\to0}\\frac{\\mathrm{e}^{\\tan x}-\\mathrm{e}^{x}}{\\sin x-x\\cos x}$; （IV）$\\lim_{x\\to0}\\frac{x-\\ln(1+x)}{\\sqrt{1+x\\sin x}-\\sqrt{\\cos x}}$.\n\n\\vfill\n\n\n% SOURCE line=1244 pdf_page=197 section=3.3\n\n\\Question{276}{第3章 · 解答题 · 第 26 题}\n\n设 $f(x)$ 有二阶连续导数, $f(0) = f(1) = 0$, 证明: 当 $x \\in [0,1]$ 时, 有 $\\left|f'(x)\\right| \\leqslant \\frac{1}{2}M$, 其中 $M = \\max_{x \\in [0,1]} \\{\\left|f''(x)\\right|\\}$.\n\n\\vfill\n\n\n"}

## tool · 2026-11-14T02:09:30Z




## assistant · 2026-11-14T02:09:38Z

已冻结积分文件，仅修改 `.question-bank-work/lilin-ipad-integrals.txt`。

- 保留114条，111收录均有1–5难度评分及四个独立宏，共444宏行。
- 扩写换元、分部、反常收敛、几何切片及针对性检查，保留2042八问完整推导。
- 结构与题号检查通过；35个导数检查点、17项积分复算通过。
- 保留1600零点条件、1604已知分支、2055整数参数、2124参数量词的疑义说明。
- 指定六条交叉复核完成，具体补充建议已发消息；未编辑其他文件。

未执行汇总编译、视觉检查及Git操作。风险主要为上述原题条件歧义，须在最终题集中保留说明。
