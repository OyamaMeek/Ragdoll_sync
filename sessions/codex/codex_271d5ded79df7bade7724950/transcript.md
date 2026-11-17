# 01a1d7c4-8e85-7a50-901e-9d3ae77a00bc

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-14T01:55:52Z

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



## developer · 2026-11-14T01:55:52Z

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
- mcp__bigquery
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

## developer · 2026-11-14T01:55:52Z

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

## developer · 2026-11-14T01:55:52Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-14T01:55:52Z

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

## developer · 2026-11-14T01:55:53Z

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


## tool · 2026-11-14T01:55:56Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 11878)
Total output lines: 560

     559 .question-bank-work/lilin-ipad-derivatives.txt
@@ 533 2.1
先把分子两项分别除以 $x^3$。出现 $f(x)$ 与 $f(x^3)$ 时，把它们写成导数定义的差商，因为 $f(0)=0$。
\[
\frac{x^2f(x)-2f(x^3)}{x^3}=\frac{f(x)-f(0)}x-2\frac{f(x^3)-f(0)}{x^3}.
\]
当 $x\to0$ 时，$x^3$ 也从两侧趋于 $0$。两个差商均趋于 $f'(0)$，所以原极限是 $-f'(0)$。
@@ 537 2.1
公切线给出两条信息。曲线经过 $(1,0)$，故 $f(1)=0$。两条切线斜率相等，故 $f'(1)=2\cdot1-1=1$。

令 $u_n=\frac{n}{n+2}$。因 $u_n-1=-\frac{2}{n+2}$，把原式拆成一个差商和一个可以直接取极限的因子：
\[
n f(u_n)=\frac{f(u_n)-f(1)}{u_n-1}\cdot\frac{-2n}{n+2}\longrightarrow 1\cdot(-2)=-2.
\]
$u_n$ 从左侧趋于 $1$，在 $1$ 处可导足以保证这一侧的差商也趋于 $1$。
@@ 541 2.5
指数 $\frac1x$ 的绝对值越来越大，底数趋于 $1$。先取对数，把乘方变成乘积。由于 $f(x)$ 在 $0$ 可导，连续性与 $f(x)=x\cdot\frac{f(x)}x\to0$ 给出 $f(0)=0$，进而 $f'(0)=0$。

二阶 Taylor 公式给出 $f(x)=2x^2+o(x^2)$，这里 $\frac{o(x^2)}{x^2}\to0$。令 $u=\frac{f(x)}x$。底数 $1+u$ 在零点附近为正，且 $\ln(1+u)\sim u$，因此
\[
\frac{\ln(1+u)}x=\frac{\ln(1+u)}{u}\cdot\frac{f(x)}{x^2}\longrightarrow 2.
\]
取指数，原极限为 $\mathrm e^2$。
@@ 545 2.1
题设只给一个点的导数，直接展开差商最有效。因为 $\frac{f(x)-f(0)}x\to f'(0)>0$，在充分小的去心邻域内，该差商为正。若 $x>0$，乘以 $x$ 得 $f(x)>f(0)$。若 $x<0$，乘以 $x$ 后不等号反向，得 $f(x)<f(0)$。故选 C，D 错误。

差商只比较 $x$ 与 $0$。要判断单调性，还得比较同一侧的任意两点。例取 $f(x)=x+2x^2\sin(\frac1x)$、$f(0)=0$。其 $f'(0)=1$，但非零处的 $f'(x)=1+4x\sin(\frac1x)-2\cos(\frac1x)$ 在两侧均反复变号，排除 A、B。
@@ 557 2.1
先记住一个事实：若商趋于有限值而分母趋于零，分子就是这二者的乘积，必趋于零。A 的分子趋于 $f(0)$，所以 $f(0)=0$。B 的分子趋于 $2f(0)$，结论相同。C 先由 A 得 $f(0)=0$，此时题给极限正是导数定义。

D 用的是对称差商，两侧函数值可能互相抵消。取 $f(x)=|x|$，对称差商恒为零，但 $\frac{f(x)-f(0)}x=\frac{|x|}{x}$ 的右极限为 $1$、左极限为 $-1$。故 D 错误。
@@ 569 2.1
增量 $\Delta y$ 就是 $y(x+\Delta x)-y(x)$。导数是增量比的极限，故把等式除以 $\Delta x$：
\[
\frac{\Delta y}{\Delta x}=\frac{y}{1+x^2}+\frac{\alpha}{\Delta x}.
\]
“比 $\Delta x$ 高阶”表示右边第二项趋于零。取极限得 $\frac{\mathrm dy}{\mathrm dx}=\frac{y}{1+x^2}$，代入 $x=0$、$y=\pi$，结果为 $\pi$。
@@ 573 2.3
“增量的线性主部”就是 $\mathrm dy=y'(x)\Delta x$，意思是只保留关于 $\Delta x$ 的一次项。对 $y=f(x^2)$ 先对外层求导，再乘里层 $x^2$ 的导数 $2x$，所以 $y'=2xf'(x^2)$。

代入 $x=-1$ 和 $\Delta x=-0.1$，得 $0.1=(-2)f'(1)\cdot(-0.1)=0.2f'(1)$。因此 $f'(1)=0.5$，选 D。
@@ 585 2.1
左支在 $x=0$ 给出 $f(0)=0$，所以要检验的导数差商就是 $\frac{f(x)}x$。右侧利用 $1-\cos x=2\sin^2\frac{x}{2}$ 和 $|\sin u|\leq |u|$，得到
\[
0\leq\frac{1-\cos x}{x^{\frac32}}\leq\frac{\sqrt{x}}2\longrightarrow0.
\]
左侧的差商为 $xg(x)$。若 $|g(x)|\leq M$，其绝对值至多是 $M|x|$，也趋于零。左右导数相等，所以 $f'(0)=0$，选 D。可导同时保证了 $f$ 在零点连续。
@@ 597 2.1
导数条件提供了 $\frac{f(u)-f(0)}u\to2$。分子里恰好有 $u=1-\cos x$，所以乘除同一个 $u$，把已知差商分离出来：
\[
\frac{f(1-\cos x)}{\ln(1+x^2)}=\frac{f(u)-f(0)}u\cdot\frac{1-\cos x}{x^2}\cdot\frac{x^2}{\ln(1+x^2)}.
\]
第二项由 $1-\cos x=2\sin^2\frac{x}{2}$ 得极限 $\frac12$，第三项由 $\ln(1+t)\sim t$ 得极限 $1$。三项相乘，填 $1$。
@@ 601 2.5
左支告诉我们 $f(0)=b$、左导数为 $a$。要配出右支在零点的常数项与一次项，先把分子的 $g(x)$ 和 $\cos x$ 都展开到二阶，因为后面还要除以 $x$。
\[
g(x)=1+2x+\frac52x^2+o(x^2),\qquad \cos x=1-\frac12x^2+o(x^2).
\]
相减并除以 $x$，得到右支 $2+3x+o(x)$。右极限是 $2$，连续性要求 $b=2$。以此值计算右导数：$\frac{f(x)-2}{x}=3+o(1)\to3$。故令 $a=3$ 才能让左右导数相等，且 $f'(0)=3$。
@@ 605 2.2
乘积在 $0$ 处只有第一因子 $\mathrm e^x-1$ 为零。令剩下的因子之积为 $G(x)$，用乘积法则可知 $f'(0)=\mathrm e^0G(0)+(\mathrm e^0-1)G'(0)=G(0)$。因此
\[
f'(0)=(1-2)(1-3)\cdots(1-n)=(-1)^{n-1}(n-1)!.
\]
若 $n=1$，函数就只有 $\mathrm e^x-1$，直接求导得 $1$，也与公式一致。
@@ 609 2.1
周期为 $5$，所以先在 $x=1$ 找函数值和斜率，再把切线平移到 $x=6$。让题设等式里的 $x\to0$，左边趋于 $-2f(1)$，右边趋于 $0$，故 $f(1)=0$。

令 $u=\sin x$。在 $1$ 处可导，故 $f(1+u)=f(1)+u f'(1)+o(u)$，$f(1-u)=f(1)-u f'(1)+o(u)$。把这两式代回题设并除以 $x$，由 $\frac{\sin x}{x}\to1$ 得 $4f'(1)=8$。故 $f(6)=0$、$f'(6)=2$，切线为 $y=2(x-6)$。
@@ 613 2.5
令 $u=x^{\frac23}=|x|^{\frac23}$。分子 $\mathrm e^u-1-u$ 已经减去了指数函数展开式的常数项和一次项，因此首项是 $\frac12u^2$。由于 $f(0)=0$，
\[
\frac{f(x)-f(0)}x=\left(\frac12+o(1)\right)\frac{|x|^{\frac43}}x.
\]
最后一项的绝对值是 $|x|^{\frac13}$，两边都趋于零，所以 $f'(0)=0$。保留外层函数的抵消，可直接避开在 $0$ 处对 $|x|^{\frac23}$ 求导。
@@ 619 2.2
按 $t$ 的正负去绝对值。若 $t>0$，则 $x=t$、$y=t\ln(1+t)$。若 $-1<t<0$，则 $x=3t$、$y=-t\ln(1+t)$。由乘积与链式法则，
\[
f'(x)=\begin{cases}
\ln(1+x)+\frac{x}{1+x},&x>0,\\
-\frac13\left[\ln(1+\frac x3)+\frac{x}{3+x}\right],&-3<x<0.
\end{cases}
\]
在 $0$ 处用定义。因 $y(0)=0$，右差商是 $\ln(1+t)$，左差商是 $-\frac13\ln(1+t)$，均趋于零，故 $f'(0)=0$。上面两支的导函数也都趋于 $0$，这就证明了 $f'$ 连续。
@@ 623 2.1
绝对值里的 $\ln(1+x)$ 在 $0$ 的两侧异号。把差商拆开：
\[
\frac{F(x)-F(0)}x=\frac{f(x)-f(0)}x-f(x)\frac{|\ln(1+x)|}{x}.
\]
$\frac{\ln(1+x)}x\to1$，因此含绝对值的比值右极限为 $1$、左极限为 $-1$。$f$ 可导所以连续，两个单侧导数分别是 $f'(0)-f(0)$ 和 $f'(0)+f(0)$。这两个数相等当且仅当 $f(0)=0$，选 A。
@@ 635 2.1
先按 $f(a)$ 是否为零分开。若 $f(a)\ne0$，连续性保证 $f$ 在 $a$ 附近与 $f(a)$ 同号，所以 $|f|$ 在附近等于 $f$ 或 $-f$，均可导。

若 $f(a)=0$，令 $h=x-a$。$|f|$ 的差商等于 $\frac{|h|}{h}\left|\frac{f(a+h)-f(a)}{h}\right|$，右导数为 $|f'(a)|$，左导数为 $-|f'(a)|$。只有 $f'(a)=0$ 时它们相等。因此不可导当且仅当 $f(a)=0$ 且 $f'(a)\ne0$，选 B。
@@ 647 2.2
去掉绝对值后，$f(x)$ 在 $x\geq0$ 时等于 $2x^5$，在 $x<0$ 时恒等于 $0$。每次求导右支的幂次降一阶，左支一直为零。用导数定义逐次计算，在前四次求导时，右差商仍含 $x$ 的正整数次幂，左右导数均为零，故 $f^{(j)}(0)=0$，$j=1,2,3,4$。

此时 $f^{(4)}(x)=240x$（$x>0$），而左支为 $0$。第五阶的右差商是 $240$，左差商是 $0$，故第五阶导数不存在。最高阶为 $4$，选 C。
@@ 659 2.1
绝对值只有在内部为零时才可能形成尖点。$x^3-x=x(x-1)(x+1)$，候选点是 $-1,0,1$。外部因子 $x^2-x-2=(x+1)(x-2)$，所以在 $-1$ 同时为零。差商在该点化为 $(x-2)|x^3-x|\to0$，故可导。

在 $0,1$，外部因子的值都为 $-2$。设 $p(x)=x^3-x$，则 $p'(0)=-1$，$p'(1)=2$。在任一零点 $a$，$\frac{|p(x)|}{|x-a|}\to|p'(a)|$，故原函数的左右差商分别趋于 $2|p'(a)|$ 和 $-2|p'(a)|$。两点均不可导，共 $2$ 个，选 B。
@@ 673 2.2
底数和指数都含 $x$，先取自然对数，把指数放到乘积中。底数 $1+x^2>0$，故 $\ln y=(\arctan x)\ln(1+x^2)$。对两边求导，左边由链式法则成为 $\frac{y'}y$，右边用乘积法则：
\[
\frac{y'}y=\frac{\ln(1+x^2)}{1+x^2}+\frac{2x\arctan x}{1+x^2}.
\]
乘回 $y$，得到 $\displaystyle y'=(1+x^2)^{\arctan x}\frac{\ln(1+x^2)+2x\arctan x}{1+x^2}$。在 $x=0$，括号中两项都为零，故斜率为零。
@@ 677 2.2
原式说明 $x=\mathrm e^{y-f(y)}>0$，所以可取对数，得到 $\ln x=y-f(y)$。把 $y$ 看作 $x$ 的函数，求导得 $\frac1x=(1-f'(y))y'$。令 $A=1-f'(y)\ne0$，则 $y'=\frac1{xA}$。

第二次求导时 $A$ 随 $y$、进而随 $x$ 变化，所以 $A'=-f''(y)y'$。分开对 $x^{-1}$ 和 $A^{-1}$ 求导，得到
\[
y''=-\frac{1}{x^2A}+\frac{f''(y)y'}{xA^2}=\frac{f''(y)-A^2}{x^2A^3},\qquad A=1-f'(y).
\]
@@ 681 2.3
要求的是微分，所以目标是先求该点的 $y'$，再乘 $\mathrm dx$。令 $x=0$，原式给出 $y=1$。两边对 $x$ 求导，左边按复合函数处理：
\[
2^{xy}\ln 2\,(y+xy')=1+y'.
\]
在 $(0,1)$ 处，左边只剩 $\ln 2$，故 $y'=\ln2-1$，从而 $\left.\mathrm dy\right|_{x=0}=(\ln2-1)\,\mathrm dx$。
@@ 685 2.2
只求一个点的二阶导数，可先定位该点，再逐次求导并代入，省去写复杂的通式。令 $x=0$，得 $\mathrm e^{y(0)}=1$，所以 $y(0)=0$。

第一次求导得 $y+(x+\mathrm e^y)y'=1$，代入 $(0,0)$ 得 $y'(0)=1$。第二次求导时，$x+\mathrm e^y$ 也随 $x$ 变动，因此
\[
2y'+\mathrm e^y(y')^2+(x+\mathrm e^y)y''=0.
\]
在 $0$ 处代入 $y=0,y'=1$，得 $2+1+y''(0)=0$，故 $y''(0)=-3$。
@@ 689 2.2
令 $u=\frac{3x-2}{3x+2}$。复合函数的导数为 $f'(u)u'$。求 $x=0$ 处的导数时，外层导数应在 $u(0)=-1$ 处计算。
\[
u'=\frac{3(3x+2)-3(3x-2)}{(3x+2)^2}=\frac{12}{(3x+2)^2},\qquad u'(0)=3.
\]
于是 $y'(0)=\arctan((-1)^2)\cdot3=\frac{3\pi}{4}$。
@@ 693 2.2
虽然题目给出的是 $y$ 与 $t$ 的隐式关系，仍然可以把 $t$ 当作共同参数。第二个等式对 $t$ 求导，记 $y_t=\frac{\mathrm dy}{\mathrm dt}$，有
\[
2y_t-y^2-2tyy_t+\mathrm e^t=0,\qquad x_t=\frac{1}{1+t^2}.
\]
移项后除以 $x_t$，得 $\displaystyle\frac{\mathrm dy}{\mathrm dx}=\frac{(1+t^2)(y^2-\mathrm e^t)}{2(1-ty)}$，适用于 $1-ty\ne0$ 的点。此处分母是求解 $y_t$ 时的系数，求导公式须在它非零处使用。
@@ 697 3.2
先求关于参数 $t$ 的导数。变上限积分的导数等于把上限代入被积函数，所以 $y_t=\ln(1+t^2)$，而 $x_t=-\mathrm e^{-t}$。故一阶导数为 $y_x=-\mathrm e^t\ln(1+t^2)$。

二阶导数要求的是 $y_x$ 对 $x$ 的变化率。先对 $t$ 求导，再除以 $x_t$：
\[
y_{xx}=\frac{-\mathrm e^t[\ln(1+t^2)+\frac{2t}{1+t^2}]}{-\mathrm e^{-t}}=\mathrm e^{2t}\left[\ln(1+t^2)+\frac{2t}{1+t^2}\right].
\]
代入 $t=0$，两项都为零，结果为 $0$。
@@ 701 2.2
设反函数为 $g$，则 $f(g(x))=x$。因为 $f'(u)=a\mathrm e^u>0$，原函数严格递增，反函数在值域内存在并可导。对恒等式求导：$f'(g(x))g'(x)=1$，所以 $g'(x)=\frac1a\mathrm e^{-g(x)}$。

再求一次导数时指数 $-g(x)$ 也要乘它的导数 $-g'(x)$。于是
\[
g''(x)=-\frac1a\mathrm e^{-g(x)}g'(x)=-\frac{1}{a^2\mathrm e^{2g(x)}}.
\]
也可写成 $-\frac1{(x-C)^2}$，其中 $f(u)=a\mathrm e^u+C$。
@@ 705 2.2
输入和输出在反函数里互换，所以 $f(a)=3$ 对应 $g(3)=a$。将 $f(g(x))=x$ 求导一次，得 $f'(g(x))g'(x)=1$，故 $g'(3)=1$。

继续使用乘积与链式法则，得 $f''(g(x))(g'(x))^2+f'(g(x))g''(x)=0$。代入 $x=3$，得到 $2\cdot1^2+1\cdot g''(3)=0$，所以 $g''(3)=-2$。原函数在 $a$ 处的导数为 $1$，求反函数导数时分母非零。
@@ 709 2.2
原函数三支分别严格递增，接合值为 $-1,8$，所以可以按这两个输出值把反函数分段。第一支解出平方根时取负号，因为原输入小于 $-1$。交换自变量和函数值后得
\[
g(x)=\begin{cases}-\sqrt{\frac{1-x}{2}},&x<-1,\\ \sqrt[3]{x},&-1\leq x\leq8,\\ \frac{x+16}{12},&x>8.\end{cases}
\]
两处接合值相等，故没有间断点。在 $-1$，左、右导数分别为 $\frac14,\frac13$，故不可导。在 $0$，差商为 $\frac{1}{|x|^{\frac23}}$，无有限极限，也不可导。在 $8$，两侧导数都是 $\frac1{12}$，可导。其他点由各支直接求导，均可导。
@@ 717 2.2
用乘积的高阶求导公式。因为 $x^2$ 在 $0$ 处的值和一阶导数都为零，三阶及更高阶导数也恒为零，代入 $x=0$ 后，只有恰好对 $x^2$ 求两次导数的项留下：
\[
f^{(n)}(0)=\binom n2\cdot2\,\left.\frac{\mathrm d^{n-2}}{\mathrm dx^{n-2}}\ln(1+x)\right|_{x=0}.
\]
对数从一阶导数 $(1+x)^{-1}$ 开始连续求导，每次把负指数乘下来。其 $m$ 阶导数在 $0$ 处为 $(-1)^{m-1}(m-1)!$。令 $m=n-2$，得到 $\displaystyle f^{(n)}(0)=(-1)^{n-3}\frac{n!}{n-2}$。
@@ 721 2.2
试求前几阶，观察重复出现的因子。$f'=f^2$，$f''=2ff'=2f^3$，$f'''=6f^2f'=6f^4$。每求导一次，原来的幂次乘到前面，而 $f'=f^2$ 又使总幂次增加一。

由此猜测 $f^{(n)}(x)=n![f(x)]^{n+1}$。$n=1$ 时是已知条件。若第 $n$ 阶成立，则
\[
f^{(n+1)}=n!(n+1)f^nf'=(n+1)!f^{n+2}.
\]
所以归纳结论对所有正整数 $n$ 成立，$f(x)=0$ 的点也无需另外除以 $f$。
@@ 725 2.2
先改成以 $\theta$ 为参数的直角坐标：$x=(1-\cos\theta)\cos\theta$、$y=(1-\cos\theta)\sin\theta$。在 $\theta=\frac\pi6$，有
\[
x_0=\frac{2\sqrt3-3}{4},\qquad y_0=\frac{2-\sqrt3}{4}.
\]
令 $r=1-\cos\theta$，则 $x_\theta=r'\cos\theta-r\sin\theta$，$y_\theta=r'\sin\theta+r\cos\theta$。代入 $r'=\frac12$，得两式都等于 $\frac{\sqrt3-1}{2}\ne0$。故切线斜率为 $1$，与它垂直的法线斜率为 $-1$。

切线为 $y-y_0=x-x_0$，法线为 $y-y_0=-(x-x_0)$。
@@ 729 2.2
横坐标、纵坐标和距离都随时间 $t$ 变化，题目给的是 $\frac{\mathrm dx}{\mathrm dt}=30$。由 $9y=4x^2$ 对 $t$ 求导，得 $9\frac{\mathrm dy}{\mathrm dt}=8x\frac{\mathrm dx}{\mathrm dt}$，在 $x=3$ 处 $\frac{\mathrm dy}{\mathrm dt}=80$。

原点到动点的距离满足 $s^2=x^2+y^2$。对 $t$ 求导，并约去系数 $2$，得 $s\frac{\mathrm ds}{\mathrm dt}=x\frac{\mathrm dx}{\mathrm dt}+y\frac{\mathrm dy}{\mathrm dt}$。在 $(3,4)$ 处，$s=5$，所以 $\frac{\mathrm ds}{\mathrm dt}=\frac{3\cdot30+4\cdot80}{5}=82$ 厘米每秒。正号表示点正在远离原点。
@@ 740 2.1
函数在 $0$ 可导，等价于左、右差商有相同的有限极限。因为 $F(0)=f(0)$，
\[
\frac{F(x)-F(0)}x=\frac{f(x)-f(0)}x+f(x)\frac{|\sin x|}{x}.
\]
由 $\frac{\sin x}x\to1$，第二项的右极限为 $f(0)$，左极限为 $-f(0)$。第一项的两侧均趋于 $f'(0)$。所以两侧导数相等恰在 $f(0)=0$ 时成立，选 A。
@@ 752 2.1
逐项计算差商 $\frac{f(x)-f(0)}x$。A 和 B 的 $f(0)=0$，约去绝对值后差商的绝对值分别为 $|\sin|x||$ 和 $\left|\sin\sqrt{|x|}\right|$，两者都趋于零。C 中 $\cos|x|=\cos x$，导数在 $0$ 处为零。

D 在 $0$ 处的函数值为 $1$。令 $u=\sqrt{|x|}$，用 $\cos u-1\sim-\frac12u^2$，差商等于 $\frac{\cos u-1}{u^2}\frac{|x|}x$。右侧趋于 $-\frac12$，左侧趋于 $\frac12$，故不可导，选 D。
@@ 764 2.1
题设保证在 $0$ 可导，尚需证明在 $1$ 可导，直接在 $1$ 写差商。由 $f(1+h)=2f(h)$，令 $h=0$ 还有 $f(1)=2f(0)$，故
\[
\frac{f(1+h)-f(1)}h=2\frac{f(h)-f(0)}h\longrightarrow 2f'(0)=6.
\]
因此 $f'(1)$ 存在且等于 $6$，选 C。
@@ 776 2.1
两条曲线相切有两个条件：同一个横坐标处高度相同，切线斜率也相同。设切点横坐标为 $a>0$，则
\[
ka^2=\ln a,\qquad 2ka=\frac1a.
\]
第二式给出 $ka^2=\frac12$，代入第一式得 $a=\mathrm e^{\frac12}$。再解得 $k=\frac1{2\mathrm e}$，选 B。此时两条曲线在 $a$ 的高度均为 $\frac12$，斜率均为 $\frac1a$，确实满足相切条件。
@@ 788 2.1
B 中令 $u=-h$。当 $h$ 双侧趋于零，$u$ 同样双侧趋于零，且 $\frac{f(x_0)-f(x_0-h)}h=\frac{f(x_0+u)-f(x_0)}u$。这正是导数定义，因此选 B。

A、C 令 $u=\frac1h$ 后，分别只检查右导数和左导数。D 使用对称差商。取 $f(x)=|x-x_0|$，A、C、D 中的极限都存在，分别为 $1,-1,0$，但真正的导数因左右不同而不存在。这同时排除三个选项。
@@ 800 2.2
左侧函数恒为零，所以若 $f'$ 在 $0$ 连续，必有 $f'(0)=0$。右侧求导时，内层 $x^{-\beta}$ 还要再求导，得到
\[
f'(x)=\alpha x^{\alpha-1}\cos(x^{-\beta})+\beta x^{\alpha-\beta-1}\sin(x^{-\beta}).
\]
第二项的幂次更低。令 $x=(\frac\pi2+2k\pi)^{-\frac1\beta}\to0^+$，则余弦为零、正弦为 $1$。要让导数沿这串点趋于零，必须 $\alpha-\beta-1>0$。此时 $\alpha>1$，右差商 $x^{\alpha-1}\cos(x^{-\beta})\to0$，且导函数上式的两项都趋于零，确实连续。因此选 A。
@@ 812 2.1
要把题设极限变成标准差商 $\frac{f(u)}u$，还要确保 $u$ 能从两侧遍历零点附近。B 令 $u=1-\mathrm e^h$，在 $0$ 附近一一对应且遍历两侧，$\frac uh\to-1$，于是 $\frac{f(u)}u$ 有限收敛恰等价于 $\frac{f(u)}h$ 有限收敛，选 B。

A 只看 $u\geq0$。C 中 $h-\sin h$ 是三阶小量，除以 $h^2$ 会抹掉差商的跳变。取 $f(x)=|x|$，A、C 的极限都存在，导数却不存在。D 取 $f(x)=1$（$x\ne0$）、$f(0)=0$，D 恒为零但函数在 $0$ 不连续。
@@ 826 2.1
切线在 $(1,1)$ 的斜率为 $f'(1)=n$，所以切线方程是 $y-1=n(x-1)$。令 $y=0$ 求与横轴的交点，得 $\xi_n=1-\frac1n$。
\[
f(\xi_n)=\left(1-\frac1n\right)^n\longrightarrow\mathrm e^{-1}.
\]
最后一步可取对数核实：$n\ln(1-\frac1n)\to-1$。所以填 $\frac1{\mathrm e}$。
@@ 830 2.2
去绝对值后，函数在 $x\geq0$ 等于 $2x^3$，在 $x<0$ 等于 $0$。分段多项式只需要检查交界 $0$。第一阶和第二阶的右差商分别为 $2x^2$ 和 $6x$，都趋于零，左差商恒为零，因此 $f'(0)=f''(0)=0$。

第二阶导数在 $x>0$ 等于 $12x$，在 $x<0$ 等于 $0$。它在零点的右差商为 $12$、左差商为 $0$，故 $f'''(0)$ 不存在。全定义域上可求的最高阶数为 $2$。
@@ 834 2.2
把恰好在 $x=2$ 为零的因子 $(x-2)$ 单独提出，令其他因子之积为 $G(x)$。乘积求导给出 $f'(2)=G(2)+(2-2)G'(2)=G(2)$。代入剩余因子，
\[
G(2)=(2-1)(2-3)(2-4)\cdots(2-100)=(-1)^{98}\,98!=98!.
\]
数负号时从 $-1$ 到 $-98$ 一共 $98$ 个，所以结果为正。
@@ 838 2.2
分母有两个线性因子，先拆成部分分式，以免反复用商法则：
\[
f(x)=\frac1{(2-x)(3-x)}=\frac1{2-x}-\frac1{3-x}.
\]
求 $\frac1{a-x}$ 的导数时，幂函数带来的负号与内层导数 $-1$ 抵消。每求导一次分母幂次加一，并把旧幂次乘到分子。故其 $n$ 阶导数是 $\frac{n!}{(a-x)^{n+1}}$，代入 $x=0$ 得
\[
f^{(n)}(0)=n!\left(\frac1{2^{n+1}}-\frac1{3^{n+1}}\right).
\]
@@ 842 2.1
公切线意味着 $f(1)=0$，并且 $f'(1)$ 等于 $x^2-x$ 在 $1$ 处的导数 $1$。要使用这两个条件，就在原式中凑出以 $1$ 为基点的差商。令 $v_n=\frac{n}{n+2}$，则 $v_n-1=-\frac2{n+2}$，
\[
n f(v_n)=\frac{f(v_n)-f(1)}{v_n-1}\,n(v_n-1)\longrightarrow 1\cdot(-2)=-2.
\]
所以填 $-2$。
@@ 846 2.2
把极坐标改为参数方程：$x=r\cos\theta$、$y=r\sin\theta$。在 $\theta=\frac\pi6$，$r=1-\frac{\sqrt3}2$，所以 $(x_0,y_0)=(\frac{2\sqrt3-3}{4},\frac{2-\sqrt3}{4})$。

用乘积求导得到 $x_\theta=r'\cos\theta-r\sin\theta$，$y_\theta=r'\sin\theta+r\cos\theta$。代入 $r'=\sin\theta=\frac12$，二者均为 $\frac{\sqrt3-1}{2}$。横坐标导数非零，切线斜率可用 $\frac{y_\theta}{x_\theta}=1$，故切线为 $y-y_0=x-x_0$，即 $y=x+\frac{5-3\sqrt3}{4}$。
@@ 850 2.2
先找过点与切线斜率。$t=1$ 时点为 $(\frac\pi4,\frac12\ln2)$。将 $y=\ln\sqrt{1+t^2}$ 写成 $\frac12\ln(1+t^2)$，可得
\[
\frac{\mathrm dx}{\mathrm dt}=\frac1{1+t^2},\qquad \frac{\mathrm dy}{\mathrm dt}=\frac{t}{1+t^2}.
\]
两式相除，切线斜率为 $t$，在 $t=1$ 等于 $1$。法线与切线垂直，所以斜率为 $-1$。所求方程是 $y-\frac12\ln2=-…1878 tokens truncated…。$x<0$ 时 $f(x)=-x\mathrm e^x$，导数为 $-(1+x)\mathrm e^x$。$x>0$ 时 $f(x)=x\mathrm e^x$，导数为 $(1+x)\mathrm e^x$。指数恒正，故函数在 $(-2,-1)$ 递增、$(-1,0)$ 递减、$(0,1)$ 递增。

区间内部的极大值为 $f(-1)=\frac1{\mathrm e}$，极小值为 $f(0)=0$，零点不可导也照样可以取极值。求闭区间最值还要比较两个端点：$f(-2)=\frac2{\mathrm e^2}$，$f(1)=\mathrm e$。于是最大值为 $\mathrm e$，在 $x=1$ 取得。最小值为 $0$，在 $x=0$ 取得。
@@ 1280 2.6
极限 $\frac{f''(x)}{|x|}\to1$ 保证充分靠近零点且 $x\ne0$ 时，该比值为正。$|x|>0$，因此这一区域内 $f''(x)>0$。这说明 $f'$ 在零点的两侧递增。

又因 $f'(0)=0$，左边的 $f'(x)<0$，右边的 $f'(x)>0$。可用中值定理严格核实：$f'(x)-f'(0)=f''(c)x$，其中 $c$ 介于 $0$ 与 $x$，符号恰与 $x$ 相同。于是 $f$ 先减后增，$f(0)$ 是极小值，选 B。两侧 $f''$ 都为正，凹凸没有改变，因此此点不是拐点。
@@ 1292 2.6
先设 $p=f'(0)$。代入方程得 $f''(0)=-\frac12p^2$。若 $p\ne0$，函数在零点的斜率非零，故不是极值点。此时 $f''(0)<0$，且由方程 $f''=\frac12[3x-(f')^2]$ 知 $f''$ 连续，附近两侧都为负，也不是拐点。

若 $p=0$，则 $f''(0)=0$。对方程求导，得 $2f'''+2f'f''=3$，所以 $f'''(0)=\frac32$。于是 $f''(x)=\frac32x+o(x)$，两侧异号，$(0,f(0))$ 是拐点。同时 $f'(x)=\frac34x^2+o(x^2)>0$，两侧同为递增，所以仍不是极值点。

结论是 $x=0$ 总不是极值点，是否为拐点取决于 $f'(0)$，恰在 $f'(0)=0$ 时为拐点。
@@ 1296 2.6
导数为 $f'(x)=kx^2-1$，唯一正驻点是 $x=\frac1{\sqrt k}$。当 $k\geq1$ 时，有 $\frac1k\leq\frac1{\sqrt k}$，整个区间上导数非正，函数递减，所以最大值一定在 $x=0$ 取得，选 D。

为核实其余选项，若 $0<k<1$，驻点位于区间内部，函数先减后增，最大值需比较端点 $f(0)=0$ 与 $f(\frac1k)=\frac{1-3k}{3k^2}$。当 $k<\frac13$ 时后者较大，当 $k>\frac13$ 时前者较大。因此 A、B 对全部 $0<k<1$ 均不成立。$k=1$ 时 $f(1)=-\frac23<0$，也直接排除了 C。
@@ 1308 2.6
隐函数的极值点若可导，应满足 $y'=0$。对原方程求导并整理，得到 $y'=\frac{x-y}{3y^2-2y+x}$。因此候选点满足 $x=y$。代回原方程，得
\[
2y^3-y^2-1=(y-1)(2y^2+y+1)=0.
\]
二次因子的判别式为 $1-8<0$，所以唯一实候选点是 $(1,1)$。此处分母为 $2\ne0$，导数公式有效。对商再求导，在 $y'=0$ 的候选点只剩 $y''=\frac{1}{3y^2-2y+x}=\frac12>0$。因此这是极小值点，所求极小值是 $1$。

还能用原方程检查整体范围。配方得 $(x-y)^2=(y-1)(2y^2+y+1)$，左侧非负，右侧的二次因子恒正，故曲线上所有实点都有 $y\geq1$。在 $(1,1)$ 确实达到 $1$，也核实了这个最小值。
@@ 1312 2.6
图中画的是 $f'$，它的正负决定原函数的升降。从左向右读图，$f'$ 在 $x_1$ 由正变负，所以 $f$ 在 $x_1$ 由增变减，有极大值。在 $x_2$ 由负变正，有极小值。

还要检查 $x=0$。此点的 $f'$ 虽然没有给出，但左侧导数为正、右侧导数为负，且题设保证 $f$ 连续。因此 $f$ 在零点由增变减，零点也是极大值点。最后在 $x_3$，$f'$ 由负变正，又产生一个极小值点。

合计两个极小值点 $x_2,x_3$，两个极大值点 $x_1,0$，选 C。查极值时，导数不存在的连续接合点也需要检查。
@@ 1328 2.6
对于负数，$x^{\frac23}$ 表示 $\sqrt[3]{x^2}$。在 $x\ne0$ 处连续求导，得 $f'(x)=\frac53x^{-\frac13}(x-2)$，$f''(x)=\frac{10(x+1)}{9x^{\frac43}}$。分母始终为正，所以二阶导数的符号完全由 $x+1$ 决定。

在 $(-\infty,-1)$，$f''<0$，图像向下弯曲。在 $(-1,0)$ 和 $(0,+\infty)$，$f''>0$，图像向上弯曲。$x=-1$ 两侧凹凸改变，且曲线连续，代入得拐点 $(-1,-6)$。

$x=0$ 处导数不存在，需另外检查两侧凹凸。两侧二阶导数都为正，所以凹凸没有改变，零点不是拐点。凹凸区间也须在该尖点处分开。
@@ 1332 2.6
拐点要检查二阶导数在两侧是否变号。设 $a=f''(0)\ne0$，由 $f(0)=f'(0)=0$，有 $f(x)=\frac12ax^2+o(x^2)$、$f'(x)=ax+o(x)$、$f''(x)=a+o(1)$。

对 $F$ 用乘积法则求两次导数，得到
\[
F''(x)=(1-\mathrm e^{2x})f''(x)-4\mathrm e^{2x}f'(x)-4\mathrm e^{2x}f(x).
\]
由于 $1-\mathrm e^{2x}=-2x+o(x)$，代入各项后得到 $F''(x)=-6ax+o(x)$。于是 $\frac{F''(x)}x\to-6a\ne0$，在零点两侧 $F''$ 的符号相反。$F$ 连续且 $F(0)=0$，故 $(0,0)$ 是拐点。
@@ 1336 2.6
$g(x)$ 是连接 $(0,f(0))$ 与 $(1,f(1))$ 的直线。要比较曲线与这条弦，取任意 $0<x<1$，分别在 $[0,x]$ 和 $[x,1]$ 使用 Lagrange 中值定理，得
\[
\frac{f(x)-f(0)}x=f'(u),\qquad \frac{f(1)-f(x)}{1-x}=f'(v),\quad 0<u<x<v<1.
\]
若 $f''\geq0$，则 $f'$ 单调不减，所以第一个分式不超过第二个。乘以正数 $x(1-x)$ 并移项，得到 $f(x)\leq(1-x)f(0)+xf(1)=g(x)$。两个端点取等，故选 D。

只给 $f'\geq0$ 无法确定曲线位于弦的哪一侧。例如 $x^2$ 位于弦下方，$2x-x^2$ 位于弦上方，均在 $[0,1]$ 递增。
@@ 1348 2.6
判断两条曲线谁是谁的导数，可以对照“函数的极值点对应导函数的零点”。先看 $L_2$，它先下降、到最低点后再上升。恰在它的最低点对应横坐标处，$L_1$ 从负值穿过横轴变成正值，所以 $L_1$ 是 $L_2$ 的导函数。

再看 $L_3$，它先升、后降、再升，依次有一个极大值和一个极小值。这两点分别对应 $L_2$ 从正到负、从负到正穿过横轴的位置。因此 $L_2$ 是 $L_3$ 的导函数。

导数关系串起来为 $L_3\to L_2\to L_1$，所以 $L_1$ 对应 $f''$、$L_2$ 对应 $f'$、$L_3$ 对应 $f$，选 C。
@@ 1363 skip
本题要求曲率、曲率半径及曲率圆，这些概念不在教材上册十九节范围内。
@@ 1368 skip
本题依赖曲率圆给出的一阶和二阶导数信息，曲率圆不在教材上册范围内。
@@ 1380 skip
本题专门计算曲率圆，教材上册未介绍曲率，暂不收录。
@@ 1384 2.6
把左边记作 $H(x)$。三次函数在负无穷趋于负无穷，在正无穷趋于正无穷。求导得 $H'(x)=6(x-1)(x-2)$，所以先增、后减、再增，局部最高点在 $1$，最低点在 $2$。

算出 $H(1)=k+5$、$H(2)=k+4$。若最高点在横轴上方、最低点在横轴下方，三个单调区间各穿轴一次，所以 $-5<k<-4$ 时有三个不同实根。

$k=-5$ 或 $k=-4$ 时，某个极值点恰在横轴上，产生一个重根，另有一个不同实根，合计两个。其余情况下两个极值都在横轴同侧，只有最左段或最右段穿轴，合计一个实根。
@@ 1388 2.6
令 $H(x)=k\arctan x-x$。函数为奇函数，$x=0$ 总是一个根，所以只需研究正半轴。其导数为 $H'(x)=\frac{k}{1+x^2}-1$。

若 $k\leq1$，对 $x>0$ 总有 $H'(x)<0$。从 $H(0)=0$ 开始严格下降，因此正半轴无根，利用奇性，负半轴也无根，只有一个根 $0$。

若 $k>1$，导数在 $0<x<\sqrt{k-1}$ 为正，在 $x>\sqrt{k-1}$ 为负。函数从零先升至正的最大值，再严格下降到负无穷。由连续性与严格单调性，下降段恰有一个正根，其相反数是唯一负根。加上零点，共三个不同实根。
@@ 1392 2.6
因为 $x>0$，将方程解出参数 $a$，得到 $a=H(x)=\frac1x-\frac1{x^3}$。现在问题变成水平线 $y=a$ 与这条曲线有几个交点。

求导得 $H'(x)=\frac{3-x^2}{x^4}$。所以 $H$ 在 $(0,\sqrt3)$ 递增，在 $(\sqrt3,+\infty)$ 递减。左端趋于负无穷，右端从正侧趋于 $0$，而最大值为 $H(\sqrt3)=\frac{2}{3\sqrt3}$。

要让递增段和递减段各与水平线交一次，水平线必须严格位于 $0$ 与最大值之间。因此 $0<a<\frac{2}{3\sqrt3}$。取等于最大值时仅有切触点，取 $a=0$ 时右侧极限没有实际达到，均只有一个根。
@@ 1396 2.6
先查定义域的有限断点 $x=0$。对数项趋于 $\ln2$，而 $\frac1x$ 无界，所以 $x=0$ 是竖直渐近线。

当 $x\to-\infty$，$\frac1x\to0$ 且 $\ln(1+\mathrm e^x)\to0$，因此 $y=0$ 是这一端的水平渐近线。

当 $x\to+\infty$，从对数中提出 $\mathrm e^x$，得 $\ln(1+\mathrm e^x)=x+\ln(1+\mathrm e^{-x})$，从而 $y-x=\frac1x+\ln(1+\mathrm e^{-x})\to0$。所以 $y=x$ 是这一端的斜渐近线。共得到三条渐近线。
@@ 1402 2.6
原方程两边都是偶函数，正根与负根成对出现，先看 $x\geq0$。当 $x\geq1$ 时，左边至少为 $2$，右边至多为 $1$，所以无解。

在 $[0,1]$，令 $H(x)=x^{\frac14}+x^{\frac12}-\cos x$。端点值 $H(0)=-1<0$，$H(1)=2-\cos1>0$，连续性保证至少有一个根。对 $0<x<1$，有 $H'(x)=\frac1{4x^{\frac34}}+\frac1{2\sqrt{x}}+\sin x>0$，所以函数严格递增，只能有一个根。

该根不等于零，取它的相反数又得到唯一负根。故共两个不同实根，选 C。
@@ 1414 2.6
先根据 $f'$ 的正负数极值点。在 $x_1$，导数由正变负，原函数有极大值。在 $x_3$，导数由负变正，有极小值。$x_2$ 左右导数都为负，$x_5$ 左右导数都为正，这两点不产生极值。因此极值点共有两个。

再根据 $f'$ 的升降找拐点。$f'$ 下降时 $f''<0$，上升时 $f''>0$。图中 $f'$ 在 $x_2$ 由下降转为上升，在 $x_4$ 由上升转为下降，在 $x_5$ 又由下降转为上升，因此这三处凹凸改变。题设保证 $f$ 连续，即使 $x_2$ 处没有导数，仍能成为拐点。

合计两个极值点、三个拐点，选 B。
@@ 1428 2.6
先约分以分清真正的无穷间断点和可去间断点。除 $x=\pm1$ 外，$y=\frac{x(x+1)}{(x-1)(x+1)}=\frac{x}{x-1}=1+\frac1{x-1}$。

在 $x=1$ 附近，$\frac1{x-1}$ 无界，因此 $x=1$ 是竖直渐近线。在 $x=-1$ 附近，约分后的式子趋于 $\frac12$，原曲线只少了一个点，不产生渐近线。两端无穷远处 $\frac1{x-1}\to0$，所以水平渐近线为 $y=1$。共两条，选 C。
@@ 1442 2.6
定义域为 $x\ne\pm1$。先求一阶导数并通分，得 $y'=\frac{x^2(x^2-3)}{(x^2-1)^2}$。分母正，$x^2$ 非负，所以符号由 $x^2-3$ 决定。

递增区间为 $(-\infty,-\sqrt3)$、$(\sqrt3,+\infty)$。递减区间为 $(-\sqrt3,-1)$、$(-1,1)$、$(1,\sqrt3)$。其中 $x=0$ 仅使导数瞬间等于零，左右同为递减。极大值在 $x=-\sqrt3$，为 $-\frac{3\sqrt3}{2}$；极小值在 $x=\sqrt3$，为 $\frac{3\sqrt3}{2}$。

二阶导数为 $y''=\frac{2x(x^2+3)}{(x^2-1)^3}$。在 $(-\infty,-1)$、$(0,1)$ 为负，图像向下弯曲；在 $(-1,0)$、$(1,+\infty)$ 为正，图像向上弯曲。零点两侧凹凸改变，拐点为 $(0,0)$。$\pm1$ 不在定义域内，不能作拐点。
@@ 1446 2.6
先令 $t=\frac ba>1$，把含两个参数的不等式化成只含一个变量的 $\ln t>\frac{2(t-1)}{t+1}$。比较两个表达式时，可以研究它们的差。

设 $H(t)=\ln t-\frac{2(t-1)}{t+1}$。显然 $H(1)=0$，而
\[
H'(t)=\frac1t-\frac4{(t+1)^2}=\frac{(t-1)^2}{t(t+1)^2}>0\quad(t>1).
\]
所以从 $1$ 往右，$H$ 严格增加，$H(t)>H(1)=0$。将 $t=\frac ba$ 代回，即得到题目中的严格不等式。
@@ 1450 2.6
对 $x>0$ 写成 $f(x)=\mathrm e^{\frac{\ln x}{x}}$。初等函数在正半轴连续。在 $x\to0^+$ 时，$\frac{\ln x}{x}\to-\infty$，故 $f(x)\to0=f(0)$，所以在定义域 $[0,+\infty)$ 上处处连续，端点按右连续理解。

对正半轴用链式法则，得 $f'(x)=x^{\frac1x}\frac{1-\ln x}{x^2}$。除 $1-\ln x$ 外其余因子均为正，故在 $(0,\mathrm e)$ 递增，在 $(\mathrm e,+\infty)$ 递减。$x=\mathrm e$ 处取得极大值，也是最大值 $\mathrm e^{\frac1{\mathrm e}}$；内部没有极小值，端点 $x=0$ 取得全域最小值 $0$。

无穷远处 $\frac{\ln x}{x}\to0$，所以 $f(x)\to1$，渐近线为 $y=1$。有限端点的函数值有限，没有竖直渐近线。
@@ 1454 2.6
两个幂的底数和指数不同，先取自然对数，比较 $\mathrm e\ln\pi$ 与 $\pi$，再除以正数 $\mathrm e\pi$，就变成比较 $\frac{\ln\pi}{\pi}$ 与 $\frac1{\mathrm e}$。

令 $H(x)=\frac{\ln x}{x}$，其导数为 $H'(x)=\frac{1-\ln x}{x^2}$。当 $x>\mathrm e$ 时导数为负，所以 $H$ 在这一段严格递减。因为 $\pi>\mathrm e$，有 $H(\pi)<H(\mathrm e)=\frac1{\mathrm e}$。乘回正数并取指数，得到 $\pi^{\mathrm e}<\mathrm e^\pi$。
@@ 1458 2.6
左边 $\ln a$ 要有定义，先要求 $a>0$。再研究右边 $H(x)=\frac{\ln x}{x}$ 在正半轴能取到哪些值。其导数为 $H'(x)=\frac{1-\ln x}{x^2}$，在 $(0,\mathrm e)$ 为正，在 $(\mathrm e,+\infty)$ 为负，所以最大值在 $x=\mathrm e$ 取得，为 $\frac1{\mathrm e}$。

同时 $H(x)$ 在 $x\to0^+$ 时趋于负无穷，且在 $(0,\mathrm e]$ 连续递增，因此值域正好是 $(-\infty,\frac1{\mathrm e}]$。方程有解当且仅当 $\ln a\leq\frac1{\mathrm e}$，即 $0<a\leq\mathrm e^{\frac1{\mathrm e}}$。
@@ 2137 skip
该题的年复利提款需要无穷级数求和，属于教材上册未覆盖的无穷级数范围。
@@ 2141 skip
差分方程不在教材上册的常微分方程范围内。
@@ 2147 skip
本题只要求生产函数的经济弹性，教材上册未定义该概念，且题目没有给出定义。
@@ 2151 2.6
需求弹性 $E_d=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$，描述价格上涨百分之一时需求量下降百分之几。负号使通常递减的需求对应正弹性。因为 $Q=100-5P$，$Q'=-5$，所以 $E_d=\frac{5P}{100-5P}=\frac{P}{20-P}$。

销售收入等于单价乘销量，$R=PQ$。用乘积法则得 $R'=Q+PQ'=Q(1-E_d)$。当 $E_d>1$ 时，$R'<0$，所以降低价格会增加收入。解 $\frac{P}{20-P}>1$，分母在已知区间为正，得到 $10<P<20$。

也可直接核实 $R(P)=100P-5P^2$、$R'(P)=100-10P$，在上述区间确为负。
@@ 2159 4.1
需求弹性的定义是 $\eta=-\frac{P}{Q}Q'$。代入后得 $\frac{Q'}Q=-\frac1{120-P}$。分离变量并积分，得到 $\ln Q=\ln(120-P)+C$，即 $Q=A(120-P)$，其中 $0<P<120$。最大需求量在价格降至零时取得，因此 $120A=1200$，$A=10$，故 $Q=1200-10P$。

“边际收益”指多卖一件时收入大约增加多少，计算的是 $\frac{\mathrm dR}{\mathrm dQ}$。把单价写成销量的函数，$P=120-\frac Q{10}$，收入为 $R=PQ=120Q-\frac{Q^2}{10}$，故边际收益为 $120-\frac Q5$。

价格为 $100$ 万元时，销量 $Q=200$，边际收益是 $80$ 万元每件，即在该销量附近每多售一件，收入约增加 $80$ 万元。
@@ 2167 2.6
设价格可写成销量的函数 $P=P(Q)$，利润为 $\Pi(Q)=P(Q)Q-C(Q)$。边际成本指 $MC=C'(Q)$，需求弹性为 $\eta=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$。因此 $P'(Q)=-\frac{P}{\eta Q}$。

内点利润最大时，导数必须为零：$\Pi'=P+QP'-MC=P(1-\frac1\eta)-MC=0$。当 $\eta\ne1$ 时，解得定价模型 $P=\frac{MC}{1-\frac1\eta}$。这给出最优内点的必要条件，具体题中还需检查确为最大值。

（2）由 $Q=40-P$ 得 $P=40-Q$，故 $\Pi=(40-Q)Q-(1600+Q^2)=40Q-2Q^2-1600$。其导数为 $40-4Q$，二阶导数为 $-4<0$，所以 $Q=10$ 时利润最大，价格为 $P=30$。此时 $MC=20$、$\eta=\frac PQ=3$，代入模型也得到 $30$。
@@ 2175 skip
差分方程属于离散递推内容，教材上册未覆盖。
@@ 2179 skip
本题直接确定差分方程的系数，超出教材上册的微分方程范围。
@@ 2183 skip
差分方程的通解不在教材上册范围内。
@@ 2189 2.6
平均成本是每件分摊的总成本，故目标函数为 $A(x)=\frac{C(x)}x=\frac{100}{x}+18-\frac{40}{\sqrt{x}}$，其中 $x>0$。求导并把分母统一成正数 $x^2$，得到
\[
A'(x)=-\frac{100}{x^2}+\frac{20}{x^{\frac32}}=\frac{20(\sqrt{x}-5)}{x^2}.
\]
当 $0<x<25$ 时导数为负，$x>25$ 时为正，所以平均成本先减后增，在 $x=25$ 取得全域最小值。日产量应为 $25$ 件。代入可查平均成本为 $\frac{100}{25}+18-\frac{40}{5}=14$ 百元每件。
@@ 2193 4.1
先用弹性恢复需求函数。$E_d=-\frac{P}{Q}Q'$ 给出 $\frac{Q'}Q=-\frac{2P}{256-P^2}$。积分得 $Q=A(256-P^2)$，代入 $P=10,Q=156$ 得 $A=1$，所以 $Q=256-P^2$，有效价格区间为 $0<P<16$。

利润是销售收入减成本。以 $P$ 为自变量，$\Pi(P)=(P-4)(256-P^2)-2000$。求导得 $\Pi'=256+8P-3P^2=-3(P-\frac{32}{3})(P+8)$。因此在有效区间内，利润先增后减，唯一最大值点为 $P=\frac{32}{3}$。

对应日产量为 $Q=256-(\frac{32}{3})^2=\frac{1280}{9}$ 件，约 $142.22$ 件。这是连续模型的最优值。若实际日产量限整数，比较邻近的 $142$ 与 $143$ 件，$142$ 件的利润较高，取 $142$ 件。
@@ 2197 2.2
单价为 $P$、销量为 $Q(P)$ 时，总收益为 $R(P)=P Q(P)$。需求弹性的定义是 $\eta=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$，其中负号使价格升高、销量降低的需求对应正值。

因为两个乘数都随 $P$ 变化，要用乘积法则。计算得
\[
\frac{\mathrm dR}{\mathrm dP}=Q+P\frac{\mathrm dQ}{\mathrm dP}=Q\left(1+\frac P Q\frac{\mathrm dQ}{\mathrm dP}\right)=Q(1-\eta).
\]
代入题给表达式还可写成 $\frac{\mathrm dR}{\mathrm dP}=Q\frac{192-3P^2}{192-P^2}$。题目所要证明的恒等式直接来自收入定义与乘积求导法则。
@@ 2201 4.1
把需求弹性写成定义，$-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}=P\ln3$。在正价格处约去 $P$，得 $\frac{Q'}Q=-\ln3$。这是可以分离变量的一阶微分方程。

两边积分，得到 $\ln Q=-P\ln3+C$，所以 $Q=A\mathrm e^{-P\ln3}=A\cdot3^{-P}$。价格越低，需求越大，最大需求量是价格趋于零时的 $A$。题给最大需求为 $1500$，所以 $Q(P)=1500\cdot3^{-P}$，$P\geq0$。

检查 $Q'=-Q\ln3$，代回弹性定义得 $P\ln3$，与已知一致。
@@ 2205 2.3
收入等于单价乘需求量，$R(P)=P Q(P)$，用乘积法则得 $R'=Q+PQ'$。本题没有写明符号 $\xi_P$ 的定义，计算时须说明约定。

若采用需求价格弹性的正值约定 $\xi_P=-\frac{P}{Q}Q'$，则 $R'=Q(1-\xi_P)=10000\times0.8=8000$。由微分估计，价格增加 $1$ 元，收入约增加 $8000$ 元。

若 $\xi_P$ 采用一般函数的有符号弹性定义 $\xi_P=\frac{P}{Q}Q'$，则 $R'=Q(1+\xi_P)=12000$，收入约增加 $12000$ 元。两种符号定义相差一个负号，需与原讲义的定义核对。两者都是当前价格处的微分估计；题面未给完整需求函数，无法确定涨价一元后的精确收入差额。
@@ 2209 2.6
连续复利的折现因子是 $\mathrm e^{-rt}$。因此 $t$ 年后的收入折算到现在，现值为 $V(t)=R_0\mathrm e^{\frac25\sqrt t-rt}$，$t\geq0$。指数函数严格递增，只需使指数 $H(t)=\frac25\sqrt t-rt$ 最大。

在通常的正利率 $r>0$ 下，$H'(t)=\frac1{5\sqrt t}-r$。它在 $t<\frac1{25r^2}$ 时为正，在更大时为负，因此最优窖陈时间为 $t_*=\frac1{25r^2}$ 年，最大现值为 $R_0\mathrm e^{\frac1{25r}}$。

当 $r=0.06=\frac3{50}$，$t_*=\frac{100}{9}$ 年，约 $11.11$ 年。若 $r\leq0$，指数始终上升，没有有限的最优售出时间。
@@ 2213 2.3
收入为 $R(P)=P(100-5P)$，导数为 $R'(P)=100-10P$。在 $P=3$ 时导数为正，涨价增加收入；在 $P=12$ 时为负，涨价减少收入。

若用微分估计相对变化，$\frac{\mathrm dR}{R}=\frac{20-2P}{20-P}\frac{\mathrm dP}{P}$。因此（I）约增加 $\frac{14}{17}\times8.5\%=7\%$；（II）约减少 $\frac12\times5\%=2.5\%$。

本题给出了完整需求函数，还能求精确幅度。若涨价比例为 $\varepsilon$，直接把新价格 $P(1+\varepsilon)$ 代入收入函数，得到 $\frac{\Delta R}{R}=\frac{20-2P}{20-P}\varepsilon-\frac{P}{20-P}\varepsilon^2$。代入（I）的 $P=3,\varepsilon=0.085$，精确增加 $6.8725\%$；代入（II）的 $P=12,\varepsilon=0.05$，精确减少 $2.875\%$。微分估计忽略了这个二次项。
@@ 2221 skip
该题要求差分方程通解，超出教材上册的范围。


## tool · 2026-11-14T01:56:04Z


Script completed
Wall time 0.2 seconds
Output:

.question-bank-work/lilin-ipad-derivatives.txt:1:@@ 533 2.1
.question-bank-work/lilin-ipad-derivatives.txt:7:@@ 537 2.1
.question-bank-work/lilin-ipad-derivatives.txt:15:@@ 541 2.5
.question-bank-work/lilin-ipad-derivatives.txt:23:@@ 545 2.1
.question-bank-work/lilin-ipad-derivatives.txt:27:@@ 557 2.1
.question-bank-work/lilin-ipad-derivatives.txt:31:@@ 569 2.1
.question-bank-work/lilin-ipad-derivatives.txt:37:@@ 573 2.3
.question-bank-work/lilin-ipad-derivatives.txt:41:@@ 585 2.1
.question-bank-work/lilin-ipad-derivatives.txt:47:@@ 597 2.1
.question-bank-work/lilin-ipad-derivatives.txt:53:@@ 601 2.5
.question-bank-work/lilin-ipad-derivatives.txt:59:@@ 605 2.2
.question-bank-work/lilin-ipad-derivatives.txt:65:@@ 609 2.1
.question-bank-work/lilin-ipad-derivatives.txt:69:@@ 613 2.5
.question-bank-work/lilin-ipad-derivatives.txt:75:@@ 619 2.2
.question-bank-work/lilin-ipad-derivatives.txt:84:@@ 623 2.1
.question-bank-work/lilin-ipad-derivatives.txt:90:@@ 635 2.1
.question-bank-work/lilin-ipad-derivatives.txt:94:@@ 647 2.2
.question-bank-work/lilin-ipad-derivatives.txt:98:@@ 659 2.1
.question-bank-work/lilin-ipad-derivatives.txt:102:@@ 673 2.2
.question-bank-work/lilin-ipad-derivatives.txt:108:@@ 677 2.2
.question-bank-work/lilin-ipad-derivatives.txt:115:@@ 681 2.3
.question-bank-work/lilin-ipad-derivatives.txt:121:@@ 685 2.2
.question-bank-work/lilin-ipad-derivatives.txt:129:@@ 689 2.2
.question-bank-work/lilin-ipad-derivatives.txt:135:@@ 693 2.2
.question-bank-work/lilin-ipad-derivatives.txt:141:@@ 697 3.2
.question-bank-work/lilin-ipad-derivatives.txt:149:@@ 701 2.2
.question-bank-work/lilin-ipad-derivatives.txt:157:@@ 705 2.2
.question-bank-work/lilin-ipad-derivatives.txt:161:@@ 709 2.2
.question-bank-work/lilin-ipad-derivatives.txt:167:@@ 717 2.2
.question-bank-work/lilin-ipad-derivatives.txt:173:@@ 721 2.2
.question-bank-work/lilin-ipad-derivatives.txt:181:@@ 725 2.2
.question-bank-work/lilin-ipad-derivatives.txt:189:@@ 729 2.2
.question-bank-work/lilin-ipad-derivatives.txt:193:@@ 740 2.1
.question-bank-work/lilin-ipad-derivatives.txt:199:@@ 752 2.1
.question-bank-work/lilin-ipad-derivatives.txt:203:@@ 764 2.1
.question-bank-work/lilin-ipad-derivatives.txt:209:@@ 776 2.1
.question-bank-work/lilin-ipad-derivatives.txt:215:@@ 788 2.1
.question-bank-work/lilin-ipad-derivatives.txt:219:@@ 800 2.2
.question-bank-work/lilin-ipad-derivatives.txt:225:@@ 812 2.1
.question-bank-work/lilin-ipad-derivatives.txt:229:@@ 826 2.1
.question-bank-work/lilin-ipad-derivatives.txt:235:@@ 830 2.2
.question-bank-work/lilin-ipad-derivatives.txt:239:@@ 834 2.2
.question-bank-work/lilin-ipad-derivatives.txt:245:@@ 838 2.2
.question-bank-work/lilin-ipad-derivatives.txt:254:@@ 842 2.1
.question-bank-work/lilin-ipad-derivatives.txt:260:@@ 846 2.2
.question-bank-work/lilin-ipad-derivatives.txt:264:@@ 850 2.2
.question-bank-work/lilin-ipad-derivatives.txt:270:@@ 856 2.2
.question-bank-work/lilin-ipad-derivatives.txt:282:@@ 866 2.2
.question-bank-work/lilin-ipad-derivatives.txt:288:@@ 876 2.2
.question-bank-work/lilin-ipad-derivatives.txt:294:@@ 880 2.1
.question-bank-work/lilin-ipad-derivatives.txt:302:@@ 884 2.5
.question-bank-work/lilin-ipad-derivatives.txt:310:@@ 892 2.1
.question-bank-work/lilin-ipad-derivatives.txt:314:@@ 896 2.2
.question-bank-work/lilin-ipad-derivatives.txt:318:@@ 1250 2.6
.question-bank-work/lilin-ipad-derivatives.txt:324:@@ 1256 2.6
.question-bank-work/lilin-ipad-derivatives.txt:332:@@ 1264 2.6
.question-bank-work/lilin-ipad-derivatives.txt:336:@@ 1268 2.6
.question-bank-work/lilin-ipad-derivatives.txt:344:@@ 1272 2.6
.question-bank-work/lilin-ipad-derivatives.txt:350:@@ 1276 2.6
.question-bank-work/lilin-ipad-derivatives.txt:354:@@ 1280 2.6
.question-bank-work/lilin-ipad-derivatives.txt:358:@@ 1292 2.6
.question-bank-work/lilin-ipad-derivatives.txt:364:@@ 1296 2.6
.question-bank-work/lilin-ipad-derivatives.txt:368:@@ 1308 2.6
.question-bank-work/lilin-ipad-derivatives.txt:376:@@ 1312 2.6
.question-bank-work/lilin-ipad-derivatives.txt:382:@@ 1328 2.6
.question-bank-work/lilin-ipad-derivatives.txt:388:@@ 1332 2.6
.question-bank-work/lilin-ipad-derivatives.txt:396:@@ 1336 2.6
.question-bank-work/lilin-ipad-derivatives.txt:404:@@ 1348 2.6
.question-bank-work/lilin-ipad-derivatives.txt:410:@@ 1363 skip
.question-bank-work/lilin-ipad-derivatives.txt:412:@@ 1368 skip
.question-bank-work/lilin-ipad-derivatives.txt:414:@@ 1380 skip
.question-bank-work/lilin-ipad-derivatives.txt:416:@@ 1384 2.6
.question-bank-work/lilin-ipad-derivatives.txt:422:@@ 1388 2.6
.question-bank-work/lilin-ipad-derivatives.txt:428:@@ 1392 2.6
.question-bank-work/lilin-ipad-derivatives.txt:434:@@ 1396 2.6
.question-bank-work/lilin-ipad-derivatives.txt:440:@@ 1402 2.6
.question-bank-work/lilin-ipad-derivatives.txt:446:@@ 1414 2.6
.question-bank-work/lilin-ipad-derivatives.txt:452:@@ 1428 2.6
.question-bank-work/lilin-ipad-derivatives.txt:456:@@ 1442 2.6
.question-bank-work/lilin-ipad-derivatives.txt:462:@@ 1446 2.6
.question-bank-work/lilin-ipad-derivatives.txt:470:@@ 1450 2.6
.question-bank-work/lilin-ipad-derivatives.txt:476:@@ 1454 2.6
.question-bank-work/lilin-ipad-derivatives.txt:480:@@ 1458 2.6
.question-bank-work/lilin-ipad-derivatives.txt:484:@@ 2137 skip
.question-bank-work/lilin-ipad-derivatives.txt:486:@@ 2141 skip
.question-bank-work/lilin-ipad-derivatives.txt:488:@@ 2147 skip
.question-bank-work/lilin-ipad-derivatives.txt:490:@@ 2151 2.6
.question-bank-work/lilin-ipad-derivatives.txt:496:@@ 2159 4.1
.question-bank-work/lilin-ipad-derivatives.txt:502:@@ 2167 2.6
.question-bank-work/lilin-ipad-derivatives.txt:508:@@ 2175 skip
.question-bank-work/lilin-ipad-derivatives.txt:510:@@ 2179 skip
.question-bank-work/lilin-ipad-derivatives.txt:512:@@ 2183 skip
.question-bank-work/lilin-ipad-derivatives.txt:514:@@ 2189 2.6
.question-bank-work/lilin-ipad-derivatives.txt:520:@@ 2193 4.1
.question-bank-work/lilin-ipad-derivatives.txt:526:@@ 2197 2.2
.question-bank-work/lilin-ipad-derivatives.txt:534:@@ 2201 4.1
.question-bank-work/lilin-ipad-derivatives.txt:540:@@ 2205 2.3
.question-bank-work/lilin-ipad-derivatives.txt:546:@@ 2209 2.6
.question-bank-work/lilin-ipad-derivatives.txt:552:@@ 2213 2.3
.question-bank-work/lilin-ipad-derivatives.txt:558:@@ 2221 skip
output/李林高数上册分节题集.tex:1496:% SOURCE line=533 pdf_page=82 section=2.1
output/李林高数上册分节题集.tex:1514:% SOURCE line=537 pdf_page=83 section=2.1
output/李林高数上册分节题集.tex:1534:% SOURCE line=545 pdf_page=85 section=2.1
output/李林高数上册分节题集.tex:1558:% SOURCE line=557 pdf_page=86 section=2.1
output/李林高数上册分节题集.tex:1582:% SOURCE line=569 pdf_page=87 section=2.1
output/李林高数上册分节题集.tex:1600:% SOURCE line=585 pdf_page=89 section=2.1
output/李林高数上册分节题集.tex:1626:% SOURCE line=597 pdf_page=90 section=2.1
output/李林高数上册分节题集.tex:1644:% SOURCE line=609 pdf_page=93 section=2.1
output/李林高数上册分节题集.tex:1660:% SOURCE line=623 pdf_page=96 section=2.1
output/李林高数上册分节题集.tex:1686:% SOURCE line=635 pdf_page=97 section=2.1
output/李林高数上册分节题集.tex:1710:% SOURCE line=659 pdf_page=99 section=2.1
output/李林高数上册分节题集.tex:1734:% SOURCE line=740 pdf_page=114 section=2.1
output/李林高数上册分节题集.tex:1760:% SOURCE line=752 pdf_page=115 section=2.1
output/李林高数上册分节题集.tex:1784:% SOURCE line=764 pdf_page=116 section=2.1
output/李林高数上册分节题集.tex:1810:% SOURCE line=776 pdf_page=117 section=2.1
output/李林高数上册分节题集.tex:1836:% SOURCE line=788 pdf_page=118 section=2.1
output/李林高数上册分节题集.tex:1860:% SOURCE line=812 pdf_page=120 section=2.1
output/李林高数上册分节题集.tex:1884:% SOURCE line=826 pdf_page=121 section=2.1
output/李林高数上册分节题集.tex:1902:% SOURCE line=842 pdf_page=125 section=2.1
output/李林高数上册分节题集.tex:2012:% SOURCE line=605 pdf_page=92 section=2.2
output/李林高数上册分节题集.tex:2030:% SOURCE line=619 pdf_page=95 section=2.2
output/李林高数上册分节题集.tex:2051:% SOURCE line=647 pdf_page=98 section=2.2
output/李林高数上册分节题集.tex:2075:% SOURCE line=673 pdf_page=100 section=2.2
output/李林高数上册分节题集.tex:2093:% SOURCE line=677 pdf_page=101 section=2.2
output/李林高数上册分节题集.tex:2112:% SOURCE line=685 pdf_page=103 section=2.2
output/李林高数上册分节题集.tex:2132:% SOURCE line=689 pdf_page=104 section=2.2
output/李林高数上册分节题集.tex:2150:% SOURCE line=693 pdf_page=105 section=2.2
output/李林高数上册分节题集.tex:2168:% SOURCE line=701 pdf_page=107 section=2.2
output/李林高数上册分节题集.tex:2188:% SOURCE line=705 pdf_page=108 section=2.2
output/李林高数上册分节题集.tex:2204:% SOURCE line=709 pdf_page=109 section=2.2
output/李林高数上册分节题集.tex:2226:% SOURCE line=717 pdf_page=110 section=2.2
output/李林高数上册分节题集.tex:2244:% SOURCE line=721 pdf_page=111 section=2.2
output/李林高数上册分节题集.tex:2264:% SOURCE line=725 pdf_page=112 section=2.2
output/李林高数上册分节题集.tex:2284:% SOURCE line=729 pdf_page=113 section=2.2
output/李林高数上册分节题集.tex:2302:% SOURCE line=800 pdf_page=119 section=2.2
output/李林高数上册分节题集.tex:2328:% SOURCE line=830 pdf_page=122 section=2.2
output/李林高数上册分节题集.tex:2344:% SOURCE line=834 pdf_page=123 section=2.2
output/李林高数上册分节题集.tex:2362:% SOURCE line=838 pdf_page=124 section=2.2
output/李林高数上册分节题集.tex:2383:% SOURCE line=846 pdf_page=126 section=2.2
output/李林高数上册分节题集.tex:2399:% SOURCE line=850 pdf_page=127 section=2.2
output/李林高数上册分节题集.tex:2606:% SOURCE line=573 pdf_page=88 section=2.3
output/李林高数上册分节题集.tex:2630:% SOURCE line=681 pdf_page=102 section=2.3
output/李林高数上册分节题集.tex:3634:% SOURCE line=541 pdf_page=84 section=2.5
output/李林高数上册分节题集.tex:3654:% SOURCE line=601 pdf_page=91 section=2.5
output/李林高数上册分节题集.tex:3672:% SOURCE line=613 pdf_page=94 section=2.5
output/李林高数上册分节题集.tex:5185:% SOURCE line=697 pdf_page=106 section=3.2

1:@@ 533 2.1
7:@@ 537 2.1
15:@@ 541 2.5
23:@@ 545 2.1
27:@@ 557 2.1
31:@@ 569 2.1
37:@@ 573 2.3
41:@@ 585 2.1
47:@@ 597 2.1
53:@@ 601 2.5
59:@@ 605 2.2
65:@@ 609 2.1
69:@@ 613 2.5
75:@@ 619 2.2
84:@@ 623 2.1
90:@@ 635 2.1
94:@@ 647 2.2
98:@@ 659 2.1
102:@@ 673 2.2
108:@@ 677 2.2
115:@@ 681 2.3
121:@@ 685 2.2
129:@@ 689 2.2
135:@@ 693 2.2
141:@@ 697 3.2
149:@@ 701 2.2
157:@@ 705 2.2
161:@@ 709 2.2
167:@@ 717 2.2
173:@@ 721 2.2
181:@@ 725 2.2
189:@@ 729 2.2
193:@@ 740 2.1
199:@@ 752 2.1
203:@@ 764 2.1
209:@@ 776 2.1
215:@@ 788 2.1
219:@@ 800 2.2
225:@@ 812 2.1
229:@@ 826 2.1
235:@@ 830 2.2
239:@@ 834 2.2
245:@@ 838 2.2
254:@@ 842 2.1
260:@@ 846 2.2
264:@@ 850 2.2
270:@@ 856 2.2
282:@@ 866 2.2
288:@@ 876 2.2
294:@@ 880 2.1
302:@@ 884 2.5
310:@@ 892 2.1
314:@@ 896 2.2
318:@@ 1250 2.6
324:@@ 1256 2.6
332:@@ 1264 2.6
336:@@ 1268 2.6
344:@@ 1272 2.6
350:@@ 1276 2.6
354:@@ 1280 2.6
358:@@ 1292 2.6
364:@@ 1296 2.6
368:@@ 1308 2.6
376:@@ 1312 2.6
382:@@ 1328 2.6
388:@@ 1332 2.6
396:@@ 1336 2.6
404:@@ 1348 2.6
410:@@ 1363 skip
412:@@ 1368 skip
414:@@ 1380 skip
416:@@ 1384 2.6
422:@@ 1388 2.6
428:@@ 1392 2.6
434:@@ 1396 2.6
440:@@ 1402 2.6
446:@@ 1414 2.6
452:@@ 1428 2.6
456:@@ 1442 2.6
462:@@ 1446 2.6
470:@@ 1450 2.6
476:@@ 1454 2.6
480:@@ 1458 2.6
484:@@ 2137 skip
486:@@ 2141 skip
488:@@ 2147 skip
490:@@ 2151 2.6
496:@@ 2159 4.1
502:@@ 2167 2.6
508:@@ 2175 skip
510:@@ 2179 skip
512:@@ 2183 skip
514:@@ 2189 2.6
520:@@ 2193 4.1
526:@@ 2197 2.2
534:@@ 2201 4.1
540:@@ 2205 2.3
546:@@ 2209 2.6
552:@@ 2213 2.3
558:@@ 2221 skip


% !TeX program = xelatex
\documentclass[UTF8,zihao=-4,fontset=fandol]{ctexart}
\usepackage[paperwidth=800bp,paperheight=600bp,left=44bp,right=44bp,top=38bp,bottom=38bp,headsep=16bp,footskip=14bp]{geometry}
\usepackage{amsmath,amssymb,xcolor,fancyhdr,graphicx}
\usepackage[hidelinks,bookmarksopen=true]{hyperref}
\renewcommand{\lim}{\operatorname*{lim}\limits}
\everymath{\displaystyle}
\definecolor{accent}{HTML}{175C57}
\setlength{\parindent}{0pt}
\setlength{\parskip}{6bp}
\setlength{\headheight}{14bp}
\setlength{\abovedisplayskip}{6bp}
\setlength{\belowdisplayskip}{6bp}
\setlength{\emergencystretch}{3em}
\pagestyle{fancy}
\fancyhf{}
\renewcommand{\headrulewidth}{0pt}
\fancyfoot[L]{\footnotesize\color{gray}李林高数 · 上册分节题集 · 4:3 横屏}
\fancyfoot[R]{\footnotesize\thepage}
\raggedbottom
\newcommand{\SectionHeading}[2]{\fancyhead[L]{}\def\CurrentSection{#1\quad #2}
  \hypertarget{s#1}{}\pdfbookmark[1]{#1 #2}{s#1}}
\newcommand{\Question}[2]{\fancyhead[L]{}
  \def\CurrentNumber{#1}\def\CurrentSource{#2}
  {\small\color{accent}\CurrentSection}\par
  {\Large\bfseries 第 #1 题}\hfill{\footnotesize\color{gray}#2}\par\medskip
  \fontsize{13}{23}\selectfont}
\newcommand{\Solution}{\clearpage
  \fancyhead[L]{\footnotesize\color{gray}第 \CurrentNumber\ 题解析}
  \fontsize{12}{20}\selectfont
  {\Large\bfseries 第 \CurrentNumber\ 题解析}\par\medskip}
\newcommand{\TextCorrection}[1]{\par{\small\color{accent}\textbf{题面核对}\quad #1}\par}
\begin{document}


\pdfbookmark[0]{目录}{contents}

{\LARGE\bfseries 李林高数上册分节题集}\par

{\small 按《工科数学分析基础》第三版上册目录编排。题目页下方留空，翻页看对应解析。}

\par{\small 分式采用上下结构，极限条件置于运算符下方。跨节题按主要解法收录一次。}

\par{\small 题源沿用讲义原章、组别和题号。题面存在条件冲突时，解析明确给出结论及依据。}

\par\smallskip\begingroup\setlength{\parskip}{0.5bp}\fontsize{10.8}{12}\selectfont

\par\smallskip\textbf{第1章 函数、极限、连续}

\par\hyperlink{s1.1}{1.1\quad 集合、映射与函数}\hfill 7 题

\par\hyperlink{s1.2}{1.2\quad 数列的极限}\hfill 16 题

\par\hyperlink{s1.3}{1.3\quad 函数的极限}\hfill 12 题

\par\hyperlink{s1.4}{1.4\quad 无穷小量与无穷大量}\hfill 16 题

\par\hyperlink{s1.5}{1.5\quad 连续函数}\hfill 14 题

\par\smallskip\textbf{第2章 一元函数微分学及其应用}

\par\hyperlink{s2.1}{2.1\quad 导数的概念}\hfill 21 题

\par\hyperlink{s2.2}{2.2\quad 求导的基本法则}\hfill 32 题

\par\hyperlink{s2.3}{2.3\quad 微分}\hfill 4 题

\par\hyperlink{s2.4}{2.4\quad 微分中值定理及其应用}\hfill 39 题

\par\hyperlink{s2.5}{2.5\quad Taylor定理及其应用}\hfill 26 题

\par\hyperlink{s2.6}{2.6\quad 函数性态的研究}\hfill 35 题

\par\smallskip\textbf{第3章 一元函数积分学及其应用}

\par\hyperlink{s3.1}{3.1\quad 定积分的概念、存在条件与性质}\hfill 17 题

\par\hyperlink{s3.2}{3.2\quad 微积分基本公式与基本定理}\hfill 33 题



## tool · 2026-11-14T01:56:09Z


Script completed
Wall time 0.1 seconds
Output:

% SOURCE line=533 pdf_page=82 section=2.1

\Question{66}{第2章 · 例题第1组 · 例 1}

设 $f(x)$ 在 x=0 处可导，$f(0)=0$，求 $\lim_{x\to0}\frac{x^2f(x)-2f(x^3)}{x^3}$.

\vfill

\Solution
% SOURCE line=537 pdf_page=83 section=2.1

\Question{67}{第2章 · 例题第1组 · 例 2}

设 $y = f(x)$ 与 $y = x^{2} - x$ 在点 $(1,0)$ 处有公切线，求 $\lim_{n \to \infty} n f\left(\frac{n}{n+2}\right)$.

\vfill

\Solution
% SOURCE line=545 pdf_page=85 section=2.1

\Question{68}{第2章 · 例题第1组 · 例 4}

设 $f(x)$ 是连续函数，且 $f'(0) > 0$，则存在 $\delta > 0$，使得（）.

\textbf{A.} $f(x)$ 在 $(0,\delta)$ 内单调增加

\textbf{B.} $f(x)$ 在 $(-\delta,0)$ 内单调减少

\textbf{C.} 对任意 $x\in(0,\delta)$，有 $f(x)>f(0)$

\textbf{D.} 对任意 $x\in(-\delta,0)$，有 $f(x)>f(0)$

\vfill

\Solution
% SOURCE line=557 pdf_page=86 section=2.1

\Question{69}{第2章 · 例题第1组 · 例 5}

设 $f(x)$ 在 x=0 处连续，则下列错误的是（ ）。

\textbf{A.} 若 $\lim_{x\to0}\frac{f(x)}{x}$ 存在，则 $f(0)=0$

\textbf{B.} 若 $\lim_{x\to0}\frac{f(x)+f(-x)}{x}$ 存在，则 $f(0)=0$

\textbf{C.} 若 $\lim_{x\to0}\frac{f(x)}{x}$ 存在，则 $f'(0)$ 存在

\textbf{D.} 若 $\lim_{x\to0}\frac{f(x)-f(-x)}{x}$ 存在，则 $f'(0)$ 存在

\vfill

\Solution
% SOURCE line=569 pdf_page=87 section=2.1

\Question{70}{第2章 · 例题第1组 · 例 6}

设 $y=y(x)$ 在 x 处的增量为 $\Delta y=\frac{y\Delta x}{1+x^{2}}+\alpha$，当 $\Delta x\to0$ 时，$\alpha$ 是 $\Delta x$ 的高阶无穷小，求 $\frac{dy}{dx}\bigg|_{\substack{x=0\\y=\pi}}$.

\vfill

\Solution
% SOURCE line=585 pdf_page=89 section=2.1

\Question{71}{第2章 · 例题第1组 · 例 8}

设 $f(x)=\left\{\begin{aligned}&\frac{1-\cos x}{\sqrt{x}},&x>0,\\&x^{2}g(x),&x\leqslant0,\end{aligned}\right.$ 其中 $g(x)$ 是有界函数，则 $f(0)$ 在 x=0 处（ ）。

\textbf{A.} 极限不存在

\textbf{B.} 极限存在，但不连续

\textbf{C.} 连续，但不可导

\textbf{D.} 可导

\vfill

\Solution
% SOURCE line=597 pdf_page=90 section=2.1

\Question{72}{第2章 · 例题第1组 · 例 9}

设 $f(x)$ 在 x=0 处可导，且 $f^{\prime}(0)=2, f(0)=0$，则 $\lim_{x\to0}\frac{f(1-\cos x)}{\ln(1+x^2)}=$ \underline{\hspace{4em}}.

\vfill

\Solution
% SOURCE line=609 pdf_page=93 section=2.1

\Question{73}{第2章 · 例题第1组 · 例 12}

已知 $f(x)$ 是周期为5的连续函数，在 x=0 的某邻域内满足 $f(1+\sin x)-3f(1-\sin x)=8x+\alpha(x)$，其中 $\alpha(x)$ 是当 $x\to0$ 时比 x 高阶的无穷小，且 $f(x)$ 在 x=1 处可导，求曲线 $y=f(x)$ 在点 $(6,f(6))$ 处的切线方程.

\vfill

\Solution
% SOURCE line=623 pdf_page=96 section=2.1

\Question{74}{第2章 · 例题第1组 · 例 15}

设 $f(x)$ 可导, $F(x) = f(x)[1 - \left|\ln(1 + x)\right|]$, 则 $f(0) = 0$ 是 $F(x)$ 在 x = 0 处可导的().

\textbf{A.} 充分必要条件

\textbf{B.} 充分但非必要条件

\textbf{C.} 必要但非充分条件

\textbf{D.} 既非充分也非必要条件

\vfill

\Solution
% SOURCE line=635 pdf_page=97 section=2.1

\Question{75}{第2章 · 例题第1组 · 例 16}

设 $f(x)$ 在 x = a 处可导，则 $\left|f(x)\right|$ 在 x = a 处不可导的充分必要条件是（ ）。

\textbf{A.} $f(a) = 0$ 且 $f'(a) = 0$

\textbf{B.} $f(a) = 0$ 且 $f'(a) \neq 0$

\textbf{C.} $f(a) > 0$ 且 $f'(a) > 0$

\textbf{D.} $f(a) < 0$ 且 $f'(a) < 0$

\vfill

\Solution
% SOURCE line=659 pdf_page=99 section=2.1

\Question{76}{第2章 · 例题第1组 · 例 18}

$f(x)=(x^{2}-x-2)\mid x^{3}-x\mid$ 不可导点的个数为( )。

\textbf{A.} 3

\textbf{B.} 2

\textbf{C.} 1

\textbf{D.} 0

\vfill

\Solution
% SOURCE line=605 pdf_page=92 section=2.2

\Question{89}{第2章 · 例题第1组 · 例 11}

设 $f(x) = (\mathrm{e}^{x} - 1)(\mathrm{e}^{2x} - 2)\cdots(\mathrm{e}^{nx} - n)$ (n 为正整数)，求 $f'(0)$.

\vfill

\Solution
% SOURCE line=619 pdf_page=95 section=2.2

\Question{90}{第2章 · 例题第1组 · 例 14}

设 $y = f(x)$ 由 $\left\{\begin{aligned}x = 2t - |t|,\\ y = |t| \ln(1 + t)\end{aligned}\right.$ 确定，求 $f'(x)$，并证明 $f'(x)$ 在 x = 0 处连续.

\vfill

\Solution
% SOURCE line=647 pdf_page=98 section=2.2

\Question{91}{第2章 · 例题第1组 · 例 17}

设 $f(x)=x^{5}+x^{4}\mid x\mid$，使 $f^{(n)}(0)$ 存在的最高阶数 n 为（）.

\textbf{A.} 2

\textbf{B.} 3

\textbf{C.} 4

\textbf{D.} 5

\vfill

\Solution
% SOURCE line=673 pdf_page=100 section=2.2

\Question{92}{第2章 · 例题第2组 · 例 1}

设 $y = \left(1 + x^{2}\right)^{\arctan x}$，求 $y'$.

\vfill

\Solution
% SOURCE line=677 pdf_page=101 section=2.2

\Question{93}{第2章 · 例题第2组 · 例 2}

设 $y = y(x)$ 由方程 $x e^{f(y)} = e^{y}$ 确定，$f$ 有二阶导数且 $f' \neq 1$，求 $\frac{d^2 y}{dx^2}$.

\vfill

\Solution
% SOURCE line=573 pdf_page=88 section=2.3

\Question{119}{第2章 · 例题第1组 · 例 7}

设函数 $f(u)$ 可导, $y = f(x^{2})$, 当自变量 x 在 x = -1 处取得增量 $\Delta x = -0.1$ 时, 相应的函数增量 $\Delta y$ 的线性主部为 0.1, 则 $f'(1) = (\quad)$.

\textbf{A.} 1

\textbf{B.} 0.1

\textbf{C.} 0.2

\textbf{D.} 0.5

\vfill

\Solution
% SOURCE line=541 pdf_page=84 section=2.5

\Question{169}{第2章 · 例题第1组 · 例 3}

设 $f(x)$ 在 x=0 的某邻域内有定义，且 $\lim_{x\to0}\frac{f(x)}{x}=0, f''(0)=4$，求 $\lim_{x\to0}\left[1+\frac{f(x)}{x}\right]^{\frac{1}{x}}$。

\vfill

\Solution
% SOURCE line=601 pdf_page=91 section=2.5

\Question{170}{第2章 · 例题第1组 · 例 10}

设 $f(x)=\left\{\begin{aligned}&\frac{g(x)-\cos x}{x},&x>0,\\&ax+b,&x\leqslant0,\end{aligned}\right.$ 且 $g''(0)=5,g'(0)=2,g(0)=1$ ,确定 a,b 的值，使得 $f(x)$ 在 x=0 处可导，并求 $f'(0)$.

\vfill

\Solution
% SOURCE line=613 pdf_page=94 section=2.5

\Question{171}{第2章 · 例题第1组 · 例 13}

设 $f(x)=\mathrm{e}^{x^{\frac{2}{3}}}-1-x^{\frac{2}{3}}$，求 $f'(0)$.

\vfill

\Solution

@@ 856 2.2
（I）把原式看成三个因子的积：$\mathrm e^x$、$\sin x$、$(1+x^2)^{-\frac12}$，依次只对其中一个求导。合并得 $y'=\frac{\mathrm e^x(\sin x+\cos x)}{\sqrt{1+x^2}}-\frac{x\mathrm e^x\sin x}{(1+x^2)^{\frac32}}$。

（II）底数和指数都变化，先取对数。由 $\ln y=\sqrt{x}\ln(1+x^2)$，用乘积法则得 $y'=y\left[\frac{\ln(1+x^2)}{2\sqrt{x}}+\frac{2x\sqrt{x}}{1+x^2}\right]$。

（III）$x=0$ 时 $y=1$。求导得 $(\mathrm e^y+x)y'=-y$，故 $y'(0)=-\frac1{\mathrm e}$。再求导得 $(\mathrm e^y+x)y''+\mathrm e^y(y')^2+2y'=0$，代入得 $y''(0)=\frac1{\mathrm e^2}$。

（IV）对 $x=y^y$ 取对数，得 $\ln x=y\ln y$（$y>0$）。两边微分得 $\mathrm dy=\frac{\mathrm dx}{x(1+\ln y)}$，适用于 $y\ne\mathrm e^{-1}$。

（V）对参数 $t$ 求导，得 $2(1-ty)y_t=y^2-\mathrm e^t$ 和 $x_t=\frac1{1+t^2}$。相除得 $\frac{\mathrm dy}{\mathrm dx}=\frac{(1+t^2)(y^2-\mathrm e^t)}{2(1-ty)}$（$1-ty\ne0$）。

（VI）内层 $u=\frac{3x-2}{3x+2}$ 满足 $u(0)=-1$、$u'(0)=\frac{12}{(3\cdot0+2)^2}=3$。按链式法则结果为 $3\arcsin 1=\frac{3\pi}{2}$。若只采用题给反正弦公式的实数自然定义域，则 $x=0$ 为端点，这个值对应右导数。若要求双侧导数，需要 $f$ 在 $u=-1$ 两侧可导的条件。
@@ 866 2.2
（I）先看每求一次导数发生什么。设当前因子是 $\mathrm e^x\sin(x+\phi)$，求导后变成 $\mathrm e^x[\sin(x+\phi)+\cos(x+\phi)]=\sqrt2\,\mathrm e^x\sin(x+\phi+\frac\pi4)$。因此求导 $n$ 次后，系数乘 $(\sqrt2)^n$，相位增加 $\frac{n\pi}{4}$，得到 $y^{(n)}(x)=2^{\frac n2}\mathrm e^x\sin(x+\frac{n\pi}{4})$。

（II）对 $x^2\ln(1+x)$ 用乘积的高阶求导公式。代入 $x=0$ 后，只留下对 $x^2$ 恰求两次导数的项。$\ln(1+x)$ 八阶导数在 $0$ 处为 $-7!$，故 $y^{(10)}(0)=2\binom{10}{2}(-7!)=-\frac{10!}{8}=-453600$。

（III）先把分式拆开，$\frac{5x-1}{(2x-1)(x+1)}=-\frac{1}{1-2x}+\frac{2}{1+x}$。这两个分式求导时，线性内层每次带出固定系数，分母幂次逐次增加。因此 $f^{(n)}(0)=n![-2^n+2(-1)^n]$。
@@ 876 2.2
等式中有 $f(x)$ 和 $f(\frac1x)$ 两个未知量。把 $x$ 换成 $\frac1x$，两者的位置就交换了，得到联立方程：
\[
af(x)+bf(\frac1x)=\frac cx,\qquad bf(x)+af(\frac1x)=cx.
\]
第一式乘 $a$，第二式乘 $b$，相减消去 $f(\frac1x)$。因为 $a^2-b^2\ne0$，$f(x)=\frac{c}{a^2-b^2}(\frac ax-bx)$。最后按幂函数求导得 $f'(x)=-\frac{c}{a^2-b^2}(\frac a{x^2}+b)$，$x\ne0$。
@@ 880 2.1
由 $f(0)=0,f'(0)=1$ 得 $\frac{f(u)}u\to1$。虽然每项都很小，项数越来越多，所以需要同时控制全部误差。任给 $\varepsilon>0$，当 $0<u<\delta$ 时，$|f(u)-u|\leq\varepsilon u$。

令 $u=\frac{k}{n^2}$，其中 $1\leq k\leq n$。所有这些 $u$ 均不超过 $\frac1n$，所以大 $n$ 下可对每项使用同一个误差界。于是
\[
\left|\sum_{k=1}^{n}f\left(\frac{k}{n^2}\right)-\frac{n+1}{2n}\right|\leq\varepsilon\frac{n+1}{2n}\leq\varepsilon.
\]
这里 $\frac{n+1}{2n}=\sum_{k=1}^{n}\frac{k}{n^2}$。该和趋于 $\frac12$，总误差趋于零，故原极限为 $\frac12$。
@@ 884 2.5
设 $g(x)=f(x)-\mathrm e^{-x}$，则 $g(0)=0$。原分式是 $g$ 在零点的差商，连续要求 $k=g'(0)=f'(0)+1$。

令 $A=g'(0)$、$B=g''(0)$。二阶 Taylor 公式和 $g'$ 在零点可导分别给出 $g(x)=Ax+\frac12Bx^2+o(x^2)$ 与 $g'(x)=A+Bx+o(x)$。第一式表明 $\varphi(x)=A+\frac12Bx+o(x)$，所以 $\varphi'(0)=\frac12B$。对 $x\ne0$ 用商法则：
\[
\varphi'(x)=\frac{xg'(x)-g(x)}{x^2}=\frac12B+o(1).
\]
这就证明 $\varphi'(x)\to\varphi'(0)$。两个展开各自来自已知条件，避免直接对余项求导。
@@ 892 2.1
先因式分解，$x^2+x-2=(x-1)(x+2)$。只有 $1,-2$ 可能因绝对值发生折转。在 $1$ 处，$f(1)=0$，差商为 $|x^2+x-2|\to0$，因为外面的 $(x-1)$ 恰能约去分母，所以可导。

在 $-2$ 处，$f(-2)=0$，差商为 $(x-1)|x-1|\frac{|x+2|}{x+2}$。右侧趋于 $-9$，左侧趋于 $9$，左右不同。故唯一不可导点为 $x=-2$。
@@ 896 2.2
参数在 $0$ 处带绝对值，分别写两支：$t>0$ 时 $x=3t$、$y=9t^2$；$t<0$ 时 $x=t$、$y=t^2$。所以不论哪一支，都有 $y=x^2$。在 $t=0$ 也有 $(x,y)=(0,0)$，于是 $\left.\frac{\mathrm dy}{\mathrm dx}\right|_{t=0}=2\cdot0=0$。

也可以检查两支的差商。$\frac{y-0}{x-0}$ 分别为 $3t$ 和 $t$，均趋于零。这样可以处理 $x(t)$ 自身在 $t=0$ 不可导的情形。
@@ 1250 2.6
分数次幂在零点不可导，找最值时须把这个点与驻点、区间端点一起检查。对 $x\ne0$ 求导，得 $f'(x)=\frac53x^{-\frac13}(x-2)$。因此函数在 $(-2,0)$ 递增，在 $(0,2)$ 递减，在 $(2,3]$ 递增。

各段边界上的值为 $f(0)=0$，$f(2)=-3\sqrt[3]4$，$f(3)=-2\sqrt[3]9$，而 $\lim_{x\to-2^+}f(x)=-7\sqrt[3]4$。所有实际函数值均小于或等于 $0$，所以最大值是 $f(0)=0$。

左端点 $-2$ 未包含。函数在该端附近的值低于后两段的所有值，并从下确界 $-7\sqrt[3]4$ 向上递增，却取不到下确界，所以本题没有最小值。
@@ 1256 2.6
（1）两边均为正，先开平方，把乘方不等式转成 $\ln(1+x)<\frac{x}{\sqrt{1+x}}$。设两边之差为 $H(x)=\frac{x}{\sqrt{1+x}}-\ln(1+x)$，则 $H(0)=0$，且
\[
H'(x)=\frac{(\sqrt{1+x}-1)^2}{2(1+x)^{\frac32}}>0\quad(x>0).
\]
故 $H(x)>0$，平方并乘 $1+x$ 即得原结论。

（2）设 $G(x)=\frac1{\ln(1+x)}-\frac1x$。求导得 $G'(x)=\frac1{x^2}-\frac1{(1+x)\ln^2(1+x)}$，由（1）知导数为负。因此 $0<x<1$ 时，$G(1)<G(x)<G(0^+)$。左端值为 $G(1)=\frac1{\ln2}-1$。利用 $\ln(1+x)=x-\frac12x^2+o(x^2)$，右端极限为 $\frac12$。所以两侧严格不等式都成立。
@@ 1264 2.6
把左侧下界与较简单的 $\frac1b$ 比较。Lagrange 中值定理给出某个 $c\in(a,b)$，使 $\frac{\ln b-\ln a}{b-a}=\frac1c>\frac1b$。又因 $(b-a)^2>0$，$a^2+b^2>2ab$，故 $\frac1b>\frac{2a}{a^2+b^2}$，左侧成立。

右侧令 $t=\frac ba>1$，要证的式子等价于 $\ln t<\sqrt t-\frac1{\sqrt t}$。设 $H(t)=\sqrt t-\frac1{\sqrt t}-\ln t$。有 $H(1)=0$，且 $H'(t)=\frac{(\sqrt t-1)^2}{2t^{\frac32}}>0$，所以 $H(t)>0$。乘回正数 $a(t-1)$，就得所需上界。
@@ 1268 2.6
先取自然对数，目标变成 $x\ln(1+\frac1x)<1<(x+1)\ln(1+\frac1x)$。这样只需要估计一个对数。

对 $\ln u$ 在 $[1,1+t]$ 上用 Lagrange 中值定理，存在 $c\in(1,1+t)$ 使 $\ln(1+t)=\frac tc$。因为 $t>0$，由 $1<c<1+t$ 得
\[
\frac{t}{1+t}<\ln(1+t)<t.
\]
取 $t=\frac1x$，上界乘 $x$，下界乘 $x+1$，得到取对数后的两个严格不等式。指数函数严格递增，取指数即可恢复原结论。
@@ 1272 2.6
先记下定义域为 $x\ne-2$，导数符号表必须在这个断点分开。求导并因式分解，得 $f'(x)=\frac{x^2(x+6)}{(x+2)^3}$。除 $x=0$ 这个不改变符号的零点外，符号由 $x+6$ 和 $x+2$ 决定。

所以 $f$ 在 $(-\infty,-6)$、$(-2,+\infty)$ 递增，在 $(-6,-2)$ 递减。$x=-6$ 处由增变减，是极大值点，极大值 $f(-6)=-\frac{19}{2}$。$x=0$ 两侧均递增，故没有极值，函数也没有其他极小值。

再求导，$f''(x)=\frac{24x}{(x+2)^4}$。在 $(-\infty,-2)$ 和 $(-2,0)$，$f''<0$，图像向下弯曲。在 $(0,+\infty)$，$f''>0$，图像向上弯曲。只有 $x=0$ 两侧凹凸改变且曲线连续，拐点为 $(0,4)$。
@@ 1276 2.6
绝对值在零点改变表达式，所以先分段。$x<0$ 时 $f(x)=-x\mathrm e^x$，导数为 $-(1+x)\mathrm e^x$。$x>0$ 时 $f(x)=x\mathrm e^x$，导数为 $(1+x)\mathrm e^x$。指数恒正，故函数在 $(-2,-1)$ 递增、$(-1,0)$ 递减、$(0,1)$ 递增。

区间内部的极大值为 $f(-1)=\frac1{\mathrm e}$，极小值为 $f(0)=0$，零点不可导也照样可以取极值。求闭区间最值还要比较两个端点：$f(-2)=\frac2{\mathrm e^2}$，$f(1)=\mathrm e$。于是最大值为 $\mathrm e$，在 $x=1$ 取得。最小值为 $0$，在 $x=0$ 取得。
@@ 1280 2.6
极限 $\frac{f''(x)}{|x|}\to1$ 保证充分靠近零点且 $x\ne0$ 时，该比值为正。$|x|>0$，因此这一区域内 $f''(x)>0$。这说明 $f'$ 在零点的两侧递增。

又因 $f'(0)=0$，左边的 $f'(x)<0$，右边的 $f'(x)>0$。可用中值定理严格核实：$f'(x)-f'(0)=f''(c)x$，其中 $c$ 介于 $0$ 与 $x$，符号恰与 $x$ 相同。于是 $f$ 先减后增，$f(0)$ 是极小值，选 B。两侧 $f''$ 都为正，凹凸没有改变，因此此点不是拐点。


## tool · 2026-11-14T01:59:56Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T02:00:01Z




## tool · 2026-11-14T02:00:07Z


Script completed
Wall time 0.1 seconds
Output:

% SOURCE line=740 pdf_page=114 section=2.1

\Question{77}{第2章 · 选择题 · 第 1 题}

设 $f(x)$ 可导, $F(x) = f(x)(1 + |\sin x|)$, 则 $f(0) = 0$ 是 $F(x)$ 在 x = 0 处可导的 ().

\textbf{A.} 充分必要条件

\textbf{B.} 充分非必要条件

\textbf{C.} 必要非充分条件

\textbf{D.} 既非充分也非必要条件

\vfill

\Solution
% SOURCE line=752 pdf_page=115 section=2.1

\Question{78}{第2章 · 选择题 · 第 2 题}

下列函数中，在 x=0 处不可导的是( )。

\textbf{A.} $f(x)=\left|x\right|\sin\left|x\right|$

\textbf{B.} $f(x)=\left|x\right|\sin\sqrt{\left|x\right|}$

\textbf{C.} $f(x)=\cos\left|x\right|$

\textbf{D.} $f(x)=\cos\sqrt{\left|x\right|}$

\vfill

\Solution
% SOURCE line=764 pdf_page=116 section=2.1

\Question{79}{第2章 · 选择题 · 第 3 题}

设 $f(x)$ 对任意 $x \in (-\infty, +\infty)$ 满足 $f(1+x) = 2f(x)$，且 $f'(0) = 3$，则 ( ).

\textbf{A.} $f'(1) = 1$

\textbf{B.} $f'(1) = 2$

\textbf{C.} $f'(1) = 6$

\textbf{D.} $f'(1)$ 不存在

\vfill

\Solution
% SOURCE line=776 pdf_page=117 section=2.1

\Question{80}{第2章 · 选择题 · 第 4 题}

设曲线 $y = kx^{2}$ 与 $y = \ln x$ 相切，则 k = ( ).

\textbf{A.} $\frac{1}{2}$

\textbf{B.} $\frac{1}{2e}$

\textbf{C.} e

\textbf{D.} $\sqrt{e}$

\vfill

\Solution
% SOURCE line=788 pdf_page=118 section=2.1

\Question{81}{第2章 · 选择题 · 第 5 题}

设 $f(x)$ 在 $x = x_0$ 的某邻域内有定义，则 $f(x)$ 在 $x = x_0$ 处可导的一个充分必要条件是（ ）。

\textbf{A.} $\lim_{h \to +\infty} h \left[ f \left( x_0 + \frac{1}{h} \right) - f(x_0) \right]$ 存在

\textbf{B.} $\lim_{h \to 0} \frac{f(x_0) - f(x_0 - h)}{h}$ 存在

\textbf{C.} $\lim_{h \to -\infty} h \left[ f \left( x_0 + \frac{1}{h} \right) - f(x_0) \right]$ 存在

\textbf{D.} $\lim_{h \to 0} \frac{f(x_0 + h) - f(x_0 - h)}{2h}$ 存在

\vfill

\Solution
% SOURCE line=812 pdf_page=120 section=2.1

\Question{82}{第2章 · 选择题 · 第 7 题}

设 $f(0)=0$, 则 $f(x)$ 在 x=0 处可导的充分必要条件为( ).

\textbf{A.} $\lim_{h\to0}\frac{1}{h^2}f(1-\cos h)$存在

\textbf{B.} $\lim_{h\to0}\frac{1}{h}f(1-\mathrm{e}^h)$存在

\textbf{C.} $\lim_{h\to0}\frac{1}{h^2}f(h-\sin h)$存在

\textbf{D.} $\lim_{h\to0}\frac{1}{h}[f(2h)-f(h)]$存在

\vfill

\Solution
% SOURCE line=826 pdf_page=121 section=2.1

\Question{83}{第2章 · 填空题 · 第 1 题}

若 $f(x)=x^{n}$ 过点 (1,1) 的切线与 x 轴的交点为 $(\xi_{n},0)$，则 $\lim_{n\to\infty}f(\xi_n)=$ \underline{\hspace{4em}}.

\vfill

\Solution
% SOURCE line=842 pdf_page=125 section=2.1

\Question{84}{第2章 · 填空题 · 第 5 题}

设曲线 $y = f(x)$ 与 $y = x^2 - x$ 在点 $(1,0)$ 处有公切线，则 $\lim_{n \to \infty} n f \left( \frac{n}{n+2} \right) =$ \underline{\hspace{4em}}.

\vfill

\Solution
% SOURCE line=880 pdf_page=131 section=2.1

\Question{85}{第2章 · 解答题 · 第 4 题}

设 $f(0)=0,f^{\prime}(0)=1$ ，求极限 $\lim_{n\to\infty}\left[f\left(\frac{1}{n^2}\right)+f\left(\frac{2}{n^2}\right)+\cdots+f\left(\frac{n}{n^2}\right)\right]$

\vfill

\Solution
% SOURCE line=892 pdf_page=133 section=2.1

\Question{86}{第2章 · 解答题 · 第 6 题}

求函数 $f(x)=(x-1)\mid x^{2}+x-2\mid$ 的不可导点.

\vfill

\Solution
% SOURCE line=685 pdf_page=103 section=2.2

\Question{94}{第2章 · 例题第2组 · 例 4}

设 $y = y(x)$ 由方程 $xy + e^{y} = x + 1$ 确定，求 $y''(0)$.

\vfill

\Solution
% SOURCE line=689 pdf_page=104 section=2.2

\Question{95}{第2章 · 例题第2组 · 例 5}

已知 $y = f\left(\frac{3x - 2}{3x + 2}\right)$，$f'(x) = \arctan x^2$，求 $\left.\frac{dy}{dx}\right|_{x=0}$。

\vfill

\Solution
% SOURCE line=693 pdf_page=105 section=2.2

\Question{96}{第2章 · 例题第2组 · 例 6}

（数学三不要求）设 $y = y(x)$ 由 $\left\{\begin{aligned}x = &\arctan t,\\ 2y - ty^2 + e^t = 5\end{aligned}\right.$ 确定，求 $\frac{dy}{dx}$.

\vfill

\Solution
% SOURCE line=701 pdf_page=107 section=2.2

\Question{97}{第2章 · 例题第2组 · 例 8}

已知 $f'(x) = a e^{x} (a > 0$ 且为常数)，求 $f(x)$ 的反函数的二阶导数.

\vfill

\Solution
% SOURCE line=705 pdf_page=108 section=2.2

\Question{98}{第2章 · 例题第2组 · 例 9}

设可导函数 $y = f(x)$ 有反函数 $g(x)$，且 $f(a) = 3, f'(a) = 1, f''(a) = 2$，求 $g''(3)$.

\vfill

\Solution
% SOURCE line=709 pdf_page=109 section=2.2

\Question{99}{第2章 · 例题第2组 · 例 10}

设 $f(x)=\left\{\begin{aligned}&1-2x^{2},&x<-1,\\&x^{3},&-1\leqslant x\leqslant2,\\&12x-16,&x>2.\end{aligned}\right.$

(1) 写出 $f(x)$ 的反函数 $g(x)$ 的表达式.

(2)问$g(x)$是否有间断点、不可导点，若有，请指出这些点.

\vfill

\Solution
% SOURCE line=717 pdf_page=110 section=2.2

\Question{100}{第2章 · 例题第2组 · 例 11}

求函数 $f(x)=x^{2}\ln(1+x)$ 在 x=0 处的 n 阶导数 $f^{(n)}(0)(n \geqslant 3)$.

\vfill

\Solution
% SOURCE line=721 pdf_page=111 section=2.2

\Question{101}{第2章 · 例题第2组 · 例 12}

已知函数有任意阶导数，且 $f'(x) = \left[f(x)\right]^2$，求 $f^{(n)}(x)$.

\vfill

\Solution
% SOURCE line=725 pdf_page=112 section=2.2

\Question{102}{第2章 · 例题第2组 · 例 13}

已知曲线的极坐标方程是 $r=1-\cos\theta$，求该曲线上对应于 $\theta=\frac{\pi}{6}$ 处的切线与法线的直角坐标方程.

\vfill

\Solution
% SOURCE line=729 pdf_page=113 section=2.2

\Question{103}{第2章 · 例题第2组 · 例 14}

如图2-1所示，一动点P在曲线$9y=4x^{2}$上运动，P点的横坐标的运动速度为$30\frac{\mathrm{cm}}{\mathrm s}$，当P点经过点(3,4)时，从原点到P点的距离s的变化率是多少？（设坐标轴的单位长为1cm） y O 图2-1

\par\smallskip\includegraphics[width=170bp,height=135bp,keepaspectratio]{lilin-figures/第113页.png}

\vfill

\Solution
% SOURCE line=800 pdf_page=119 section=2.2

\Question{104}{第2章 · 选择题 · 第 6 题}

设 $f(x)=\left\{\begin{aligned}&x^{\alpha}\cdot\cos\frac{1}{x^{\beta}},&x>0,\\&0,&x\leqslant0\end{aligned}\right.$ $(\alpha>0,\beta>0)$，若 $f^{\prime}(x)$ 在 x=0 处连续，则().

\textbf{A.} $\alpha-\beta>1$

\textbf{B.} $0<\alpha-\beta\leq1$

\textbf{C.} $\alpha-\beta>2$

\textbf{D.} $0<\alpha-\beta\leq2$

\vfill

\Solution
% SOURCE line=830 pdf_page=122 section=2.2

\Question{105}{第2章 · 填空题 · 第 2 题}

设 $f(x) = x^{3} + x^{2} \cdot |x|$，则 $f(x)$ 的最高阶导数 n = \underline{\hspace{4em}}.

\vfill

\Solution
% SOURCE line=834 pdf_page=123 section=2.2

\Question{106}{第2章 · 填空题 · 第 3 题}

设 $f(x)=(x-1)(x-2)\cdots(x-100)$，则 $f'(2)=$ \underline{\hspace{4em}}.

\vfill

\Solution
% SOURCE line=838 pdf_page=124 section=2.2

\Question{107}{第2章 · 填空题 · 第 4 题}

设 $f(x)=\frac{1}{x^{2}-5x+6}$，则 $f^{(n)}(0)=$ \underline{\hspace{4em}}.

\vfill

\Solution
% SOURCE line=846 pdf_page=126 section=2.2

\Question{108}{第2章 · 填空题 · 第 6 题}

(仅数学一、数学二要求)已知曲线的极坐标方程为$r=1-\cos\theta$，则该曲线上对应于$\theta=\frac{\pi}{6}$处的切线的直角坐标方程为\_\_\_。

\vfill

\Solution
% SOURCE line=850 pdf_page=127 section=2.2

\Question{109}{第2章 · 填空题 · 第 7 题}

曲线 $\begin{cases} x = \arctan t, \\ y = \ln \sqrt{1+t^2} \end{cases}$ 上对应于 t = 1 点处的法线方程为\_\_\_。

\vfill

\Solution
% SOURCE line=856 pdf_page=128 section=2.2

\Question{110}{第2章 · 解答题 · 第 1 题}

求下列函数的导数或微分： (I) $y = \frac{\mathrm{e}^{x} \sin x}{\sqrt{1 + x^2}}$, 求 $y'$; (II) $y = (1 + x^2)^{\sqrt{x}}$ ($x > 0$), 求 $y'$; (III) 设 $y = y(x)$ 由方程 $e^y + xy = e$ 确定，求 $\left. \frac{d^2 y}{dx^2} \right|_{x=0}$; (IV) 设 $x = y^y$, 求 $dy$; (V) (仅数学一、数学二要求) 设 $y = y(x)$ 由 $\left\{\begin{array}{l} x = \arctan t, \\ 2y - ty^2 = 5 - e^t \end{array}\right.$ 确定，求 $\frac{dy}{dx}$; (VI) 设 $y = f\left(\frac{3x - 2}{3x + 2}\right)$, 且 $f'(x) = \arcsin x^2$, 求 $\left. \frac{dy}{dx} \right|_{x=0}$.

\vfill

\Solution
% SOURCE line=866 pdf_page=129 section=2.2

\Question{111}{第2章 · 解答题 · 第 2 题}

求高阶导数：

（I）设 $y = e^{x} \sin x$，求 $y^{(n)}(x)$；

（II）设 $y = x^{2}\ln(1+x)$，求 $y^{(10)}(0)$

（III）设 $f(x)=\frac{5x-1}{2x^{2}+x-1}$，求 $f^{(n)}(0)$.

\vfill

\Solution
% SOURCE line=876 pdf_page=130 section=2.2

\Question{112}{第2章 · 解答题 · 第 3 题}

设 $f(x)$ 满足 $af(x)+bf\left(\frac{1}{x}\right)=\frac{c}{x}$, $\left|a\right|\neq\left|b\right|$, 求 $f'(x)$.

\vfill

\Solution
% SOURCE line=896 pdf_page=134 section=2.2

\Question{113}{第2章 · 解答题 · 第 7 题}

设 $y = y(x)$ 由 $\left\{\begin{array}{l}x = 2t + |t|, \\ y = 5t^2 + 4t |t\end{array}\right.$ 所确定，求 $\left.\frac{dy}{dx}\right|_{t=0}$.

\vfill

\Solution
% SOURCE line=681 pdf_page=102 section=2.3

\Question{120}{第2章 · 例题第2组 · 例 3}

设 $y = y(x)$ 由方程 $2^{xy} = x + y$ 确定，求 $\mathrm{d}y\big|_{x=0}$.

\vfill

\Solution
% SOURCE line=884 pdf_page=132 section=2.5

\Question{172}{第2章 · 解答题 · 第 5 题}

设 $f(x)$ 二阶可导, $f(0)=1$, $\varphi(x)=\left\{\begin{aligned}&\frac{f(x)-\mathrm{e}^{-x}}{x},&x\neq0,\\&k,&x=0,\end{aligned}\right.$ $\varphi(x)$ 在 x=0 处连续.

(I) 求 k 的值;

（II）证明：$\varphi^{\prime}(x)$ 在 x=0 处连续.

\vfill

\Solution
% SOURCE line=697 pdf_page=106 section=3.2

\Question{242}{第2章 · 例题第2组 · 例 7}

（数学三不要求）设 $y = y(x)$ 由 $\left\{\begin{array}{l}x = e^{-t}, \\ y = \int_{0}^{t} \ln(1 + u^{2}) du\end{array}\right.$ 确定，求 $\left.\frac{d^{2}y}{dx^{2}}\right|_{t=0}$.

\vfill

\Solution

\Method
等式给出 $x>0$，取对数可消去指数；连续两次隐式求导时需保留 $y$ 对 $x$ 的链式因子。
\Derive
由原式得 $x=\mathrm e^{y-f(y)}>0$，故 $\ln x=y-f(y)$。记 $A=1-f'(y)\ne0$，第一次求导得 $\frac1x=Ay'$，从而 $y'=\frac1{xA}$。又因 $A'=-f''(y)y'$，所以
\[
y''=-\frac1{x^2A}+\frac{f''(y)y'}{xA^2}
=\frac{f''(y)-A^2}{x^2A^3}.
\]
\Check
答案为 $\frac{f''(y)-[1-f'(y)]^2}{x^2[1-f'(y)]^3}$。取 $f\equiv0$ 时原式给出 $y=\ln x$，公式化为 $-\frac1{x^2}$，符号一致；$f'\ne1$ 保证分母非零。
@@ 681 2.3
要求的是微分，所以目标是先求该点的 $y'$，再乘 $\mathrm dx$。令 $x=0$，原式给出 $y=1$。两边对 $x$ 求导，左边按复合函数处理：
\[
2^{xy}\ln 2\,(y+xy')=1+y'.
\]
在 $(0,1)$ 处，左边只剩 $\ln 2$，故 $y'=\ln2-1$，从而 $\left.\mathrm dy\right|_{x=0}=(\ln2-1)\,\mathrm dx$。
@@ 685 2.2
只求一个点的二阶导数，可先定位该点，再逐次求导并代入，省去写复杂的通式。令 $x=0$，得 $\mathrm e^{y(0)}=1$，所以 $y(0)=0$。

第一次求导得 $y+(x+\mathrm e^y)y'=1$，代入 $(0,0)$ 得 $y'(0)=1$。第二次求导时，$x+\mathrm e^y$ 也随 $x$ 变动，因此
\[
2y'+\mathrm e^y(y')^2+(x+\mathrm e^y)y''=0.
\]
在 $0$ 处代入 $y=0,y'=1$，得 $2+1+y''(0)=0$，故 $y''(0)=-3$。
@@ 689 2.2
令 $u=\frac{3x-2}{3x+2}$。复合函数的导数为 $f'(u)u'$。求 $x=0$ 处的导数时，外层导数应在 $u(0)=-1$ 处计算。
\[
u'=\frac{3(3x+2)-3(3x-2)}{(3x+2)^2}=\frac{12}{(3x+2)^2},\qquad u'(0)=3.
\]
于是 $y'(0)=\arctan((-1)^2)\cdot3=\frac{3\pi}{4}$。
@@ 693 2.2
虽然题目给出的是 $y$ 与 $t$ 的隐式关系，仍然可以把 $t$ 当作共同参数。第二个等式对 $t$ 求导，记 $y_t=\frac{\mathrm dy}{\mathrm dt}$，有
\[
2y_t-y^2-2tyy_t+\mathrm e^t=0,\qquad x_t=\frac{1}{1+t^2}.
\]
移项后除以 $x_t$，得 $\displaystyle\frac{\mathrm dy}{\mathrm dx}=\frac{(1+t^2)(y^2-\mathrm e^t)}{2(1-ty)}$，适用于 $1-ty\ne0$ 的点。此处分母是求解 $y_t$ 时的系数，求导公式须在它非零处使用。
@@ 697 3.2
先求关于参数 $t$ 的导数。变上限积分的导数等于把上限代入被积函数，所以 $y_t=\ln(1+t^2)$，而 $x_t=-\mathrm e^{-t}$。故一阶导数为 $y_x=-\mathrm e^t\ln(1+t^2)$。

二阶导数要求的是 $y_x$ 对 $x$ 的变化率。先对 $t$ 求导，再除以 $x_t$：
\[
y_{xx}=\frac{-\mathrm e^t[\ln(1+t^2)+\frac{2t}{1+t^2}]}{-\mathrm e^{-t}}=\mathrm e^{2t}\left[\ln(1+t^2)+\frac{2t}{1+t^2}\right].
\]
代入 $t=0$，两项都为零，结果为 $0$。
@@ 701 2.2
设反函数为 $g$，则 $f(g(x))=x$。因为 $f'(u)=a\mathrm e^u>0$，原函数严格递增，反函数在值域内存在并可导。对恒等式求导：$f'(g(x))g'(x)=1$，所以 $g'(x)=\frac1a\mathrm e^{-g(x)}$。

再求一次导数时指数 $-g(x)$ 也要乘它的导数 $-g'(x)$。于是
\[
g''(x)=-\frac1a\mathrm e^{-g(x)}g'(x)=-\frac{1}{a^2\mathrm e^{2g(x)}}.
\]
也可写成 $-\frac1{(x-C)^2}$，其中 $f(u)=a\mathrm e^u+C$。
@@ 705 2.2
输入和输出在反函数里互换，所以 $f(a)=3$ 对应 $g(3)=a$。将 $f(g(x))=x$ 求导一次，得 $f'(g(x))g'(x)=1$，故 $g'(3)=1$。

继续使用乘积与链式法则，得 $f''(g(x))(g'(x))^2+f'(g(x))g''(x)=0$。代入 $x=3$，得到 $2\cdot1^2+1\cdot g''(3)=0$，所以 $g''(3)=-2$。原函数在 $a$ 处的导数为 $1$，求反函数导数时分母非零。
@@ 709 2.2
原函数三支分别严格递增，接合值为 $-1,8$，所以可以按这两个输出值把反函数分段。第一支解出平方根时取负号，因为原输入小于 $-1$。交换自变量和函数值后得
\[
g(x)=\begin{cases}-\sqrt{\frac{1-x}{2}},&x<-1,\\ \sqrt[3]{x},&-1\leq x\leq8,\\ \frac{x+16}{12},&x>8.\end{cases}
\]
两处接合值相等，故没有间断点。在 $-1$，左、右导数分别为 $\frac14,\frac13$，故不可导。在 $0$，差商为 $\frac{1}{|x|^{\frac23}}$，无有限极限，也不可导。在 $8$，两侧导数都是 $\frac1{12}$，可导。其他点由各支直接求导，均可导。
@@ 717 2.2
用乘积的高阶求导公式。因为 $x^2$ 在 $0$ 处的值和一阶导数都为零，三阶及更高阶导数也恒为零，代入 $x=0$ 后，只有恰好对 $x^2$ 求两次导数的项留下：
\[
f^{(n)}(0)=\binom n2\cdot2\,\left.\frac{\mathrm d^{n-2}}{\mathrm dx^{n-2}}\ln(1+x)\right|_{x=0}.
\]
对数从一阶导数 $(1+x)^{-1}$ 开始连续求导，每次把负指数乘下来。其 $m$ 阶导数在 $0$ 处为 $(-1)^{m-1}(m-1)!$。令 $m=n-2$，得到 $\displaystyle f^{(n)}(0)=(-1)^{n-3}\frac{n!}{n-2}$。
@@ 721 2.2
试求前几阶，观察重复出现的因子。$f'=f^2$，$f''=2ff'=2f^3$，$f'''=6f^2f'=6f^4$。每求导一次，原来的幂次乘到前面，而 $f'=f^2$ 又使总幂次增加一。

由此猜测 $f^{(n)}(x)=n![f(x)]^{n+1}$。$n=1$ 时是已知条件。若第 $n$ 阶成立，则
\[
f^{(n+1)}=n!(n+1)f^nf'=(n+1)!f^{n+2}.
\]
所以归纳结论对所有正整数 $n$ 成立，$f(x)=0$ 的点也无需另外除以 $f$。
@@ 725 2.2
先改成以 $\theta$ 为参数的直角坐标：$x=(1-\cos\theta)\cos\theta$、$y=(1-\cos\theta)\sin\theta$。在 $\theta=\frac\pi6$，有
\[
x_0=\frac{2\sqrt3-3}{4},\qquad y_0=\frac{2-\sqrt3}{4}.
\]
令 $r=1-\cos\theta$，则 $x_\theta=r'\cos\theta-r\sin\theta$，$y_\theta=r'\sin\theta+r\cos\theta$。代入 $r'=\frac12$，得两式都等于 $\frac{\sqrt3-1}{2}\ne0$。故切线斜率为 $1$，与它垂直的法线斜率为 $-1$。

切线为 $y-y_0=x-x_0$，法线为 $y-y_0=-(x-x_0)$。
@@ 729 2.2
横坐标、纵坐标和距离都随时间 $t$ 变化，题目给的是 $\frac{\mathrm dx}{\mathrm dt}=30$。由 $9y=4x^2$ 对 $t$ 求导，得 $9\frac{\mathrm dy}{\mathrm dt}=8x\frac{\mathrm dx}{\mathrm dt}$，在 $x=3$ 处 $\frac{\mathrm dy}{\mathrm dt}=80$。

原点到动点的距离满足 $s^2=x^2+y^2$。对 $t$ 求导，并约去系数 $2$，得 $s\frac{\mathrm ds}{\mathrm dt}=x\frac{\mathrm dx}{\mathrm dt}+y\frac{\mathrm dy}{\mathrm dt}$。在 $(3,4)$ 处，$s=5$，所以 $\frac{\mathrm ds}{\mathrm dt}=\frac{3\cdot30+4\cdot80}{5}=82$ 厘米每秒。正号表示点正在远离原点。
@@ 740 2.1
函数在 $0$ 可导，等价于左、右差商有相同的有限极限。因为 $F(0)=f(0)$，
\[
\frac{F(x)-F(0)}x=\frac{f(x)-f(0)}x+f(x)\frac{|\sin x|}{x}.
\]
由 $\frac{\sin x}x\to1$，第二项的右极限为 $f(0)$，左极限为 $-f(0)$。第一项的两侧均趋于 $f'(0)$。所以两侧导数相等恰在 $f(0)=0$ 时成立，选 A。
@@ 752 2.1
逐项计算差商 $\frac{f(x)-f(0)}x$。A 和 B 的 $f(0)=0$，约去绝对值后差商的绝对值分别为 $|\sin|x||$ 和 $\left|\sin\sqrt{|x|}\right|$，两者都趋于零。C 中 $\cos|x|=\cos x$，导数在 $0$ 处为零。

D 在 $0$ 处的函数值为 $1$。令 $u=\sqrt{|x|}$，用 $\cos u-1\sim-\frac12u^2$，差商等于 $\frac{\cos u-1}{u^2}\frac{|x|}x$。右侧趋于 $-\frac12$，左侧趋于 $\frac12$，故不可导，选 D。
@@ 764 2.1
题设保证在 $0$ 可导，尚需证明在 $1$ 可导，直接在 $1$ 写差商。由 $f(1+h)=2f(h)$，令 $h=0$ 还有 $f(1)=2f(0)$，故
\[
\frac{f(1+h)-f(1)}h=2\frac{f(h)-f(0)}h\longrightarrow 2f'(0)=6.
\]
因此 $f'(1)$ 存在且等于 $6$，选 C。
@@ 776 2.1
两条曲线相切有两个条件：同一个横坐标处高度相同，切线斜率也相同。设切点横坐标为 $a>0$，则
\[
ka^2=\ln a,\qquad 2ka=\frac1a.
\]
第二式给出 $ka^2=\frac12$，代入第一式得 $a=\mathrm e^{\frac12}$。再解得 $k=\frac1{2\mathrm e}$，选 B。此时两条曲线在 $a$ 的高度均为 $\frac12$，斜率均为 $\frac1a$，确实满足相切条件。
@@ 788 2.1
B 中令 $u=-h$。当 $h$ 双侧趋于零，$u$ 同样双侧趋于零，且 $\frac{f(x_0)-f(x_0-h)}h=\frac{f(x_0+u)-f(x_0)}u$。这正是导数定义，因此选 B。

A、C 令 $u=\frac1h$ 后，分别只检查右导数和左导数。D 使用对称差商。取 $f(x)=|x-x_0|$，A、C、D 中的极限都存在，分别为 $1,-1,0$，但真正的导数因左右不同而不存在。这同时排除三个选项。
@@ 800 2.2
左侧函数恒为零，所以若 $f'$ 在 $0$ 连续，必有 $f'(0)=0$。右侧求导时，内层 $x^{-\beta}$ 还要再求导，得到
\[
f'(x)=\alpha x^{\alpha-1}\cos(x^{-\beta})+\beta x^{\alpha-\beta-1}\sin(x^{-\beta}).
\]
第二项的幂次更低。令 $x=(\frac\pi2+2k\pi)^{-\frac1\beta}\to0^+$，则余弦为零、正弦为 $1$。要让导数沿这串点趋于零，必须 $\alpha-\beta-1>0$。此时 $\alpha>1$，右差商 $x^{\alpha-1}\cos(x^{-\beta})\to0$，且导函数上式的两项都趋于零，确实连续。因此选 A。
@@ 812 2.1
要把题设极限变成标准差商 $\frac{f(u)}u$，还要确保 $u$ 能从两侧遍历零点附近。B 令 $u=1-\mathrm e^h$，在 $0$ 附近一一对应且遍历两侧，$\frac uh\to-1$，于是 $\frac{f(u)}u$ 有限收敛恰等价于 $\frac{f(u)}h$ 有限收敛，选 B。

A 只看 $u\geq0$。C 中 $h-\sin h$ 是三阶小量，除以 $h^2$ 会抹掉差商的跳变。取 $f(x)=|x|$，A、C 的极限都存在，导数却不存在。D 取 $f(x)=1$（$x\ne0$）、$f(0)=0$，D 恒为零但函数在 $0$ 不连续。
@@ 826 2.1
切线在 $(1,1)$ 的斜率为 $f'(1)=n$，所以切线方程是 $y-1=n(x-1)$。令 $y=0$ 求与横轴的交点，得 $\xi_n=1-\frac1n$。
\[
f(\xi_n)=\left(1-\frac1n\right)^n\longrightarrow\mathrm e^{-1}.
\]
最后一步可取对数核实：$n\ln(1-\frac1n)\to-1$。所以填 $\frac1{\mathrm e}$。
@@ 830 2.2


## tool · 2026-11-14T02:03:52Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T02:04:00Z


Script completed
Wall time 0.1 seconds
Output:

% SOURCE line=1250 pdf_page=198 section=2.6

\Question{192}{第4章 · 示例 · 示例}

求 $f(x) = (x - 5) \sqrt[3]{x^2}$ 在 $(-2, 3]$ 上的最值.

\vfill

\Solution
% SOURCE line=1256 pdf_page=199 section=2.6

\Question{193}{第4章 · 例题第1组 · 例 1}

设 $x \in (0,1)$，证明：

(1)$(1+x)\ln^{2}(1+x)<x^{2}$;

(2)$\frac{1}{\ln2}-1<\frac{1}{\ln(1+x)}-\frac{1}{x}<\frac{1}{2}$

\vfill

\Solution
% SOURCE line=1264 pdf_page=200 section=2.6

\Question{194}{第4章 · 例题第1组 · 例 2}

设 0 < a < b，证明：$\frac{2a}{a^{2}+b^{2}}<\frac{\ln b-\ln a}{b-a}<\frac{1}{\sqrt{ab}}$.

\vfill

\Solution
% SOURCE line=1268 pdf_page=201 section=2.6

\Question{195}{第4章 · 例题第1组 · 例 3}

证明：当x>0时，$\left(1+\frac{1}{x}\right)^{x}<\mathrm{e}<\left(1+\frac{1}{x}\right)^{x+1}$.

\vfill

\Solution
% SOURCE line=1272 pdf_page=202 section=2.6

\Question{196}{第4章 · 例题第1组 · 例 4}

设 $f(x)=\frac{x^{3}}{(2+x)^{2}}+4$，求函数 $f(x)$ 的单调区间和极值，并求曲线 $y=f(x)$ 的凹凸区间和拐点.

\vfill

\Solution
% SOURCE line=1276 pdf_page=203 section=2.6

\Question{197}{第4章 · 例题第1组 · 例 5}

求函数 $f(x) = |x|$ $e^x$ 在 $[-2,1]$ 上的极值与最值.

\vfill

\Solution
% SOURCE line=1280 pdf_page=204 section=2.6

\Question{198}{第4章 · 例题第1组 · 例 6}

设 $f(x)$ 有二阶连续导数，且 $f'(0)=0,\lim_{x\to0}\frac{f''(x)}{|x|}=1$ ，则（）.

\textbf{A.} $f(0)$ 是 $f(x)$ 的极大值

\textbf{B.} $f(0)$ 是 $f(x)$ 的极小值

\textbf{C.} $(0,f(0))$ 是曲线 $y=f(x)$ 的拐点

\textbf{D.} $f(0)$ 不是 $f(x)$ 的极值，$(0,f(0))$ 也不是曲线 $y=f(x)$ 的拐点

\vfill

\Solution
% SOURCE line=1292 pdf_page=205 section=2.6

\Question{199}{第4章 · 例题第1组 · 例 7}

设 $f(x)$ 满足方程 $2f''(x)+\left[f'(x)\right]^2=3x$，问 x=0 是否为 $y=f(x)$ 的极值点？$(0,f(0))$ 是否为曲线 $y=f(x)$ 的拐点？

\vfill

\Solution
% SOURCE line=1296 pdf_page=206 section=2.6

\Question{200}{第4章 · 例题第1组 · 例 8}

设 $k > 0, f(x) = \frac{1}{3} k x^{3} - x, x \in \left[0, \frac{1}{k}\right]$，则()。

\textbf{A.} 当 0 < k < 1 时，$f\left(\frac{1}{k}\right)$ 是 $f(x)$ 的最大值

\textbf{B.} 当 0 < k < 1 时，$f(0)$ 是 $f(x)$ 的最大值

\textbf{C.} 当 $k \geqslant 1$ 时，$f\left(\frac{1}{k}\right)$ 是 $f(x)$ 的最大值

\textbf{D.} 当 $k \geqslant 1$ 时，$f(0)$ 是 $f(x)$ 的最大值

\vfill

\Solution
% SOURCE line=1308 pdf_page=207 section=2.6

\Question{201}{第4章 · 例题第1组 · 例 9}

设 $y = y(x)$ 由方程 $2y^{3} - 2y^{2} + 2xy - x^{2} = 1$ 确定，求 $y = y(x)$ 的极小值.

\vfill

\Solution
% SOURCE line=1312 pdf_page=208 section=2.6

\Question{202}{第4章 · 例题第1组 · 例 10}

设 $f(x)$ 在 $(-\infty, +\infty)$ 内连续，其导函数的图形如图4-2所示，则 $f(x)$ 有（ ）。

\textbf{A.} 一个极小值点和两个极大值点

\textbf{B.} 两个极小值点和一个极大值点

\textbf{C.} 两个极小值点和两个极大值点

\textbf{D.} 三个极小值点和一个极大值点

\par\smallskip\includegraphics[width=390bp,height=135bp,keepaspectratio]{lilin-figures/第208页.png}

\vfill

\Solution
% SOURCE line=1328 pdf_page=209 section=2.6

\Question{203}{第4章 · 例题第2组 · 例 1}

求曲线 $f(x)=(x-5)x^{\frac{2}{3}}$ 的凹凸区间与拐点.

\vfill

\Solution
% SOURCE line=1332 pdf_page=210 section=2.6

\Question{204}{第4章 · 例题第2组 · 例 2}

设 $f(x)$ 在 x=0 处有二阶连续导数，且 $f(0)=f'(0)=0, f''(0)\neq0$ ，证明：$(0,F(0))$ 是曲线 $F(x)=(1-\mathrm{e}^{2x})f(x)$ 的拐点.

\vfill

\Solution
% SOURCE line=1336 pdf_page=211 section=2.6

\Question{205}{第4章 · 例题第2组 · 例 3}

设在定义域内 $f(x)$ 二阶可导, $g(x) = f(0)(1 - x) + f(1)x$, 则在 $[0,1]$ 上().

\textbf{A.} 当 $f'(x) \geqslant 0$ 时, $f(x) \geqslant g(x)$

\textbf{B.} 当 $f'(x) \geqslant 0$ 时, $f(x) \leqslant g(x)$

\textbf{C.} 当 $f''(x) \geqslant 0$ 时, $f(x) \geqslant g(x)$

\textbf{D.} 当 $f''(x) \geqslant 0$ 时, $f(x) \leqslant g(x)$

\vfill

\Solution
% SOURCE line=1348 pdf_page=212 section=2.6

\Question{206}{第4章 · 例题第2组 · 例 4}

设 $f(x)$ 有二阶连续导数, $L_{1}, L_{2}, L_{3}$ (见图4-6) 分别为曲线( ).

\textbf{A.} $y = f(x), y = f'(x), y = f''(x)$

\textbf{B.} $y = f(x), y = f''(x), y = f'(x)$

\textbf{C.} $y = f''(x), y = f'(x), y = f(x)$

\textbf{D.} $y = f'(x), y = f(x), y = f''(x)$ 图4-6

\par\smallskip\includegraphics[width=390bp,height=135bp,keepaspectratio]{lilin-figures/第212页.png}

\vfill

\Solution

@@ 830 2.2
去绝对值后，函数在 $x\geq0$ 等于 $2x^3$，在 $x<0$ 等于 $0$。分段多项式只需要检查交界 $0$。第一阶和第二阶的右差商分别为 $2x^2$ 和 $6x$，都趋于零，左差商恒为零，因此 $f'(0)=f''(0)=0$。

第二阶导数在 $x>0$ 等于 $12x$，在 $x<0$ 等于 $0$。它在零点的右差商为 $12$、左差商为 $0$，故 $f'''(0)$ 不存在。全定义域上可求的最高阶数为 $2$。
@@ 834 2.2
把恰好在 $x=2$ 为零的因子 $(x-2)$ 单独提出，令其他因子之积为 $G(x)$。乘积求导给出 $f'(2)=G(2)+(2-2)G'(2)=G(2)$。代入剩余因子，
\[
G(2)=(2-1)(2-3)(2-4)\cdots(2-100)=(-1)^{98}\,98!=98!.
\]
数负号时从 $-1$ 到 $-98$ 一共 $98$ 个，所以结果为正。
@@ 838 2.2
分母有两个线性因子，先拆成部分分式，以免反复用商法则：
\[
f(x)=\frac1{(2-x)(3-x)}=\frac1{2-x}-\frac1{3-x}.
\]
求 $\frac1{a-x}$ 的导数时，幂函数带来的负号与内层导数 $-1$ 抵消。每求导一次分母幂次加一，并把旧幂次乘到分子。故其 $n$ 阶导数是 $\frac{n!}{(a-x)^{n+1}}$，代入 $x=0$ 得
\[
f^{(n)}(0)=n!\left(\frac1{2^{n+1}}-\frac1{3^{n+1}}\right).
\]
@@ 842 2.1
公切线意味着 $f(1)=0$，并且 $f'(1)$ 等于 $x^2-x$ 在 $1$ 处的导数 $1$。要使用这两个条件，就在原式中凑出以 $1$ 为基点的差商。令 $v_n=\frac{n}{n+2}$，则 $v_n-1=-\frac2{n+2}$，
\[
n f(v_n)=\frac{f(v_n)-f(1)}{v_n-1}\,n(v_n-1)\longrightarrow 1\cdot(-2)=-2.
\]
所以填 $-2$。
@@ 846 2.2
把极坐标改为参数方程：$x=r\cos\theta$、$y=r\sin\theta$。在 $\theta=\frac\pi6$，$r=1-\frac{\sqrt3}2$，所以 $(x_0,y_0)=(\frac{2\sqrt3-3}{4},\frac{2-\sqrt3}{4})$。

用乘积求导得到 $x_\theta=r'\cos\theta-r\sin\theta$，$y_\theta=r'\sin\theta+r\cos\theta$。代入 $r'=\sin\theta=\frac12$，二者均为 $\frac{\sqrt3-1}{2}$。横坐标导数非零，切线斜率可用 $\frac{y_\theta}{x_\theta}=1$，故切线为 $y-y_0=x-x_0$，即 $y=x+\frac{5-3\sqrt3}{4}$。
@@ 850 2.2
先找过点与切线斜率。$t=1$ 时点为 $(\frac\pi4,\frac12\ln2)$。将 $y=\ln\sqrt{1+t^2}$ 写成 $\frac12\ln(1+t^2)$，可得
\[
\frac{\mathrm dx}{\mathrm dt}=\frac1{1+t^2},\qquad \frac{\mathrm dy}{\mathrm dt}=\frac{t}{1+t^2}.
\]
两式相除，切线斜率为 $t$，在 $t=1$ 等于 $1$。法线与切线垂直，所以斜率为 $-1$。所求方程是 $y-\frac12\ln2=-\left(x-\frac\pi4\right)$。
@@ 856 2.2
（I）把原式看成三个因子的积：$\mathrm e^x$、$\sin x$、$(1+x^2)^{-\frac12}$，依次只对其中一个求导。合并得 $y'=\frac{\mathrm e^x(\sin x+\cos x)}{\sqrt{1+x^2}}-\frac{x\mathrm e^x\sin x}{(1+x^2)^{\frac32}}$。

（II）底数和指数都变化，先取对数。由 $\ln y=\sqrt{x}\ln(1+x^2)$，用乘积法则得 $y'=y\left[\frac{\ln(1+x^2)}{2\sqrt{x}}+\frac{2x\sqrt{x}}{1+x^2}\right]$。

（III）$x=0$ 时 $y=1$。求导得 $(\mathrm e^y+x)y'=-y$，故 $y'(0)=-\frac1{\mathrm e}$。再求导得 $(\mathrm e^y+x)y''+\mathrm e^y(y')^2+2y'=0$，代入得 $y''(0)=\frac1{\mathrm e^2}$。

（IV）对 $x=y^y$ 取对数，得 $\ln x=y\ln y$（$y>0$）。两边微分得 $\mathrm dy=\frac{\mathrm dx}{x(1+\ln y)}$，适用于 $y\ne\mathrm e^{-1}$。

（V）对参数 $t$ 求导，得 $2(1-ty)y_t=y^2-\mathrm e^t$ 和 $x_t=\frac1{1+t^2}$。相除得 $\frac{\mathrm dy}{\mathrm dx}=\frac{(1+t^2)(y^2-\mathrm e^t)}{2(1-ty)}$（$1-ty\ne0$）。

（VI）内层 $u=\frac{3x-2}{3x+2}$ 满足 $u(0)=-1$、$u'(0)=\frac{12}{(3\cdot0+2)^2}=3$。按链式法则结果为 $3\arcsin 1=\frac{3\pi}{2}$。若只采用题给反正弦公式的实数自然定义域，则 $x=0$ 为端点，这个值对应右导数。若要求双侧导数，需要 $f$ 在 $u=-1$ 两侧可导的条件。
@@ 866 2.2
（I）先看每求一次导数发生什么。设当前因子是 $\mathrm e^x\sin(x+\phi)$，求导后变成 $\mathrm e^x[\sin(x+\phi)+\cos(x+\phi)]=\sqrt2\,\mathrm e^x\sin(x+\phi+\frac\pi4)$。因此求导 $n$ 次后，系数乘 $(\sqrt2)^n$，相位增加 $\frac{n\pi}{4}$，得到 $y^{(n)}(x)=2^{\frac n2}\mathrm e^x\sin(x+\frac{n\pi}{4})$。

（II）对 $x^2\ln(1+x)$ 用乘积的高阶求导公式。代入 $x=0$ 后，只留下对 $x^2$ 恰求两次导数的项。$\ln(1+x)$ 八阶导数在 $0$ 处为 $-7!$，故 $y^{(10)}(0)=2\binom{10}{2}(-7!)=-\frac{10!}{8}=-453600$。

（III）先把分式拆开，$\frac{5x-1}{(2x-1)(x+1)}=-\frac{1}{1-2x}+\frac{2}{1+x}$。这两个分式求导时，线性内层每次带出固定系数，分母幂次逐次增加。因此 $f^{(n)}(0)=n![-2^n+2(-1)^n]$。
@@ 876 2.2
等式中有 $f(x)$ 和 $f(\frac1x)$ 两个未知量。把 $x$ 换成 $\frac1x$，两者的位置就交换了，得到联立方程：
\[
af(x)+bf(\frac1x)=\frac cx,\qquad bf(x)+af(\frac1x)=cx.
\]
第一式乘 $a$，第二式乘 $b$，相减消去 $f(\frac1x)$。因为 $a^2-b^2\ne0$，$f(x)=\frac{c}{a^2-b^2}(\frac ax-bx)$。最后按幂函数求导得 $f'(x)=-\frac{c}{a^2-b^2}(\frac a{x^2}+b)$，$x\ne0$。
@@ 880 2.1
由 $f(0)=0,f'(0)=1$ 得 $\frac{f(u)}u\to1$。虽然每项都很小，项数越来越多，所以需要同时控制全部误差。任给 $\varepsilon>0$，当 $0<u<\delta$ 时，$|f(u)-u|\leq\varepsilon u$。

令 $u=\frac{k}{n^2}$，其中 $1\leq k\leq n$。所有这些 $u$ 均不超过 $\frac1n$，所以大 $n$ 下可对每项使用同一个误差界。于是
\[
\left|\sum_{k=1}^{n}f\left(\frac{k}{n^2}\right)-\frac{n+1}{2n}\right|\leq\varepsilon\frac{n+1}{2n}\leq\varepsilon.
\]
这里 $\frac{n+1}{2n}=\sum_{k=1}^{n}\frac{k}{n^2}$。该和趋于 $\frac12$，总误差趋于零，故原极限为 $\frac12$。
@@ 884 2.5
设 $g(x)=f(x)-\mathrm e^{-x}$，则 $g(0)=0$。原分式是 $g$ 在零点的差商，连续要求 $k=g'(0)=f'(0)+1$。

令 $A=g'(0)$、$B=g''(0)$。二阶 Taylor 公式和 $g'$ 在零点可导分别给出 $g(x)=Ax+\frac12Bx^2+o(x^2)$ 与 $g'(x)=A+Bx+o(x)$。第一式表明 $\varphi(x)=A+\frac12Bx+o(x)$，所以 $\varphi'(0)=\frac12B$。对 $x\ne0$ 用商法则：
\[
\varphi'(x)=\frac{xg'(x)-g(x)}{x^2}=\frac12B+o(1).
\]
这就证明 $\varphi'(x)\to\varphi'(0)$。两个展开各自来自已知条件，避免直接对余项求导。
@@ 892 2.1
先因式分解，$x^2+x-2=(x-1)(x+2)$。只有 $1,-2$ 可能因绝对值发生折转。在 $1$ 处，$f(1)=0$，差商为 $|x^2+x-2|\to0$，因为外面的 $(x-1)$ 恰能约去分母，所以可导。

在 $-2$ 处，$f(-2)=0$，差商为 $(x-1)|x-1|\frac{|x+2|}{x+2}$。右侧趋于 $-9$，左侧趋于 $9$，左右不同。故唯一不可导点为 $x=-2$。
@@ 896 2.2
参数在 $0$ 处带绝对值，分别写两支：$t>0$ 时 $x=3t$、$y=9t^2$；$t<0$ 时 $x=t$、$y=t^2$。所以不论哪一支，都有 $y=x^2$。在 $t=0$ 也有 $(x,y)=(0,0)$，于是 $\left.\frac{\mathrm dy}{\mathrm dx}\right|_{t=0}=2\cdot0=0$。

也可以检查两支的差商。$\frac{y-0}{x-0}$ 分别为 $3t$ 和 $t$，均趋于零。这样可以处理 $x(t)$ 自身在 $t=0$ 不可导的情形。
@@ 1250 2.6
分数次幂在零点不可导，找最值时须把这个点与驻点、区间端点一起检查。对 $x\ne0$ 求导，得 $f'(x)=\frac53x^{-\frac13}(x-2)$。因此函数在 $(-2,0)$ 递增，在 $(0,2)$ 递减，在 $(2,3]$ 递增。

各段边界上的值为 $f(0)=0$，$f(2)=-3\sqrt[3]4$，$f(3)=-2\sqrt[3]9$，而 $\lim_{x\to-2^+}f(x)=-7\sqrt[3]4$。所有实际函数值均小于或等于 $0$，所以最大值是 $f(0)=0$。

左端点 $-2$ 未包含。函数在该端附近的值低于后两段的所有值，并从下确界 $-7\sqrt[3]4$ 向上递增，却取不到下确界，所以本题没有最小值。
@@ 1256 2.6
（1）两边均为正，先开平方，把乘方不等式转成 $\ln(1+x)<\frac{x}{\sqrt{1+x}}$。设两边之差为 $H(x)=\frac{x}{\sqrt{1+x}}-\ln(1+x)$，则 $H(0)=0$，且
\[
H'(x)=\frac{(\sqrt{1+x}-1)^2}{2(1+x)^{\frac32}}>0\quad(x>0).
\]
故 $H(x)>0$，平方并乘 $1+x$ 即得原结论。

（2）设 $G(x)=\frac1{\ln(1+x)}-\frac1x$。求导得 $G'(x)=\frac1{x^2}-\frac1{(1+x)\ln^2(1+x)}$，由（1）知导数为负。因此 $0<x<1$ 时，$G(1)<G(x)<G(0^+)$。左端值为 $G(1)=\frac1{\ln2}-1$。利用 $\ln(1+x)=x-\frac12x^2+o(x^2)$，右端极限为 $\frac12$。所以两侧严格不等式都成立。
@@ 1264 2.6
把左侧下界与较简单的 $\frac1b$ 比较。Lagrange 中值定理给出某个 $c\in(a,b)$，使 $\frac{\ln b-\ln a}{b-a}=\frac1c>\frac1b$。又因 $(b-a)^2>0$，$a^2+b^2>2ab$，故 $\frac1b>\frac{2a}{a^2+b^2}$，左侧成立。

右侧令 $t=\frac ba>1$，要证的式子等价于 $\ln t<\sqrt t-\frac1{\sqrt t}$。设 $H(t)=\sqrt t-\frac1{\sqrt t}-\ln t$。有 $H(1)=0$，且 $H'(t)=\frac{(\sqrt t-1)^2}{2t^{\frac32}}>0$，所以 $H(t)>0$。乘回正数 $a(t-1)$，就得所需上界。
@@ 1268 2.6
先取自然对数，目标变成 $x\ln(1+\frac1x)<1<(x+1)\ln(1+\frac1x)$。这样只需要估计一个对数。

对 $\ln u$ 在 $[1,1+t]$ 上用 Lagrange 中值定理，存在 $c\in(1,1+t)$ 使 $\ln(1+t)=\frac tc$。因为 $t>0$，由 $1<c<1+t$ 得
\[
\frac{t}{1+t}<\ln(1+t)<t.
\]
取 $t=\frac1x$，上界乘 $x$，下界乘 $x+1$，得到取对数后的两个严格不等式。指数函数严格递增，取指数即可恢复原结论。
@@ 1272 2.6
先记下定义域为 $x\ne-2$，导数符号表必须在这个断点分开。求导并因式分解，得 $f'(x)=\frac{x^2(x+6)}{(x+2)^3}$。除 $x=0$ 这个不改变符号的零点外，符号由 $x+6$ 和 $x+2$ 决定。

所以 $f$ 在 $(-\infty,-6)$、$(-2,+\infty)$ 递增，在 $(-6,-2)$ 递减。$x=-6$ 处由增变减，是极大值点，极大值 $f(-6)=-\frac{19}{2}$。$x=0$ 两侧均递增，故没有极值，函数也没有其他极小值。

再求导，$f''(x)=\frac{24x}{(x+2)^4}$。在 $(-\infty,-2)$ 和 $(-2,0)$，$f''<0$，图像向下弯曲。在 $(0,+\infty)$，$f''>0$，图像向上弯曲。只有 $x=0$ 两侧凹凸改变且曲线连续，拐点为 $(0,4)$。
@@ 1276 2.6
绝对值在零点改变表达式，所以先分段。$x<0$ 时 $f(x)=-x\mathrm e^x$，导数为 $-(1+x)\mathrm e^x$。$x>0$ 时 $f(x)=x\mathrm e^x$，导数为 $(1+x)\mathrm e^x$。指数恒正，故函数在 $(-2,-1)$ 递增、$(-1,0)$ 递减、$(0,1)$ 递增。

区间内部的极大值为 $f(-1)=\frac1{\mathrm e}$，极小值为 $f(0)=0$，零点不可导也照样可以取极值。求闭区间最值还要比较两个端点：$f(-2)=\frac2{\mathrm e^2}$，$f(1)=\mathrm e$。于是最大值为 $\mathrm e$，在 $x=1$ 取得。最小值为 $0$，在 $x=0$ 取得。
@@ 1280 2.6
极限 $\frac{f''(x)}{|x|}\to1$ 保证充分靠近零点且 $x\ne0$ 时，该比值为正。$|x|>0$，因此这一区域内 $f''(x)>0$。这说明 $f'$ 在零点的两侧递增。

又因 $f'(0)=0$，左边的 $f'(x)<0$，右边的 $f'(x)>0$。可用中值定理严格核实：$f'(x)-f'(0)=f''(c)x$，其中 $c$ 介于 $0$ 与 $x$，符号恰与 $x$ 相同。于是 $f$ 先减后增，$f(0)$ 是极小值，选 B。两侧 $f''$ 都为正，凹凸没有改变，因此此点不是拐点。


## tool · 2026-11-14T02:04:05Z




## tool · 2026-11-14T02:08:41Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T02:08:51Z


Script completed
Wall time 0.1 seconds
Output:

@@ 866 2.2 3
\Known
求 $\mathrm e^x\sin x$ 的 $n$ 阶导数、$x^2\ln(1+x)$ 在零点的十阶导数，以及有理函数在零点的 $n$ 阶导数。
\Method
（I）利用求导后的相位规律并归纳；（II）Leibniz 公式在零点只留一项；（III）部分分式分解后逐项高阶求导。
\Derive
（I）对任意常数 $\phi$，
\[
[\mathrm e^x\sin(x+\phi)]'
=\mathrm e^x[\sin(x+\phi)+\cos(x+\phi)]
=\sqrt2\mathrm e^x\sin(x+\phi+\frac\pi4).
\]
从 $n=0$ 开始，每求导一次系数乘 $\sqrt2$，相位加 $\frac\pi4$，由归纳法得 $y^{(n)}=2^{\frac n2}\mathrm e^x\sin(x+\frac{n\pi}4)$。
（II）$x^2$ 在零点的零阶、一阶值为零，高于二阶导数为零，所以仅保留对 $x^2$ 求两次的项：
\[
y^{(10)}(0)=\binom{10}2\cdot2[\ln(1+x)]^{(8)}_{x=0}
=90(-7!)=-453600.
\]
这里对数的 $m$ 阶导数为 $(-1)^{m-1}(m-1)!(1+x)^{-m}$，故八阶在零点为 $-7!$。
（III）因 $2x^2+x-1=(2x-1)(x+1)$，有
\[
f(x)=\frac1{1-2x}+\frac2{1+x}.
\]
第一项的 $n$ 阶导数为 $2^nn!(1-2x)^{-n-1}$，第二项为 $2(-1)^nn!(1+x)^{-n-1}$，故
\[
f^{(n)}(0)=n![2^n+2(-1)^n].
\]
\Check
（I）$n=1$ 恢复 $\mathrm e^x(\sin x+\cos x)$；（II）答案为 $-453600$；（III）取 $n=0$ 得 $3$，与原函数 $f(0)=1$ 不一致，说明该部分分式需按原分子重新核对。

% SOURCE line=2197 pdf_page=353 section=2.2

\Question{115}{第7章 · 解答题 · 第 3 题}

某商品的需求量 $Q = Q(P)$，需求对价格的弹性 $\eta = \frac{2P^{2}}{192 - P^{2}}$，若 R 为总收益函数，证明：$\frac{dR}{dP} = Q(1 - \eta)$.

\vfill

\Solution
% SOURCE line=2205 pdf_page=355 section=2.3

\Question{121}{第7章 · 解答题 · 第 5 题}

设某产品的需求函数 $Q = Q(P)$，其对价格 P 的弹性 $\xi_{P} = 0.2$，当需求量为 10000 件时，价格增加 1 元，问此时会使产品的收益增加多少元？

\vfill

\Solution
% SOURCE line=2213 pdf_page=357 section=2.3

\Question{122}{第7章 · 解答题 · 第 7 题}

设某商品需求函数为 Q = 100 - 5P.

（I）当 P = 3 时，问涨价会使销售收入增加还是减少？若价格上涨幅度为 8.5\%，则对销售收入的影响幅度为多少？

（II）当P=12时，问涨价会使销售收入增加还是减少？若价格上涨幅度为5\%，则对销售收入影响的幅度为多少？

\vfill

\Solution
% SOURCE line=1384 pdf_page=216 section=2.6

\Question{207}{第4章 · 例题第2组 · 例 8}

讨论方程 $2x^{3}-9x^{2}+12x+k=0$ 不同实根的个数.

\vfill

\Solution
% SOURCE line=1388 pdf_page=217 section=2.6

\Question{208}{第4章 · 例题第2组 · 例 9}

求方程 $k \arctan x = x$ 不同实根的个数，其中 k 为参数.

\vfill

\Solution
% SOURCE line=1392 pdf_page=218 section=2.6

\Question{209}{第4章 · 例题第2组 · 例 10}

设方程 $ax+\frac{1}{x^{2}}-1=0$ 在 $(0,+\infty)$ 内有两个不同实根，求 a 的取值范围.

\vfill

\Solution
% SOURCE line=1396 pdf_page=219 section=2.6

\Question{210}{第4章 · 例题第2组 · 例 11}

求曲线 $y=\frac{1}{x}+\ln(1+e^{x})$ 的渐近线方程.

\vfill

\Solution
% SOURCE line=1402 pdf_page=220 section=2.6

\Question{211}{第4章 · 选择题 · 第 1 题}

方程 $\left|x\right|^{\frac{1}{4}}+\left|x\right|^{\frac{1}{2}}=\cos x$ 不同实根的个数为( )。

\textbf{A.} 无实根

\textbf{B.} 有且只有一个实根

\textbf{C.} 有且只有两个实根

\textbf{D.} 无法确定

\vfill

\Solution
% SOURCE line=1414 pdf_page=221 section=2.6

\Question{212}{第4章 · 选择题 · 第 2 题}

设 $f(x)$ 在 $(-\infty, +\infty)$ 内连续，其导函数 $y = f'(x)$ 如图 4-10 所示，则（ ）。

\textbf{A.} $f(x)$ 有两个极值点，$y = f(x)$ 有两个拐点

\textbf{B.} $f(x)$ 有两个极值点，$y = f(x)$ 有三个拐点

\textbf{C.} $f(x)$ 有三个极值点，$y = f(x)$ 有一个拐点

\textbf{D.} $f(x)$ 有三个极值点，$y = f(x)$ 有两个拐点

\par\smallskip\includegraphics[width=390bp,height=135bp,keepaspectratio]{lilin-figures/第221页.png}

\vfill

\Solution
% SOURCE line=1428 pdf_page=222 section=2.6

\Question{213}{第4章 · 选择题 · 第 3 题}

曲线 $y=\frac{x^{2}+x}{x^{2}-1}$ 的渐近线的条数为( ).

\textbf{A.} 0

\textbf{B.} 1

\textbf{C.} 2

\textbf{D.} 3

\vfill

\Solution
% SOURCE line=1442 pdf_page=223 section=2.6

\Question{214}{第4章 · 解答题 · 第 1 题}

求 $y = x + \frac{x}{x^{2}-1}$ 的单调区间、凹凸区间、极值和拐点.

\vfill

\Solution
% SOURCE line=1446 pdf_page=224 section=2.6

\Question{215}{第4章 · 解答题 · 第 2 题}

证明: 不等式 $\ln\frac{b}{a}>\frac{2(b-a)}{b+a}$ (0<a<b).

\vfill

\Solution
% SOURCE line=1450 pdf_page=225 section=2.6

\Question{216}{第4章 · 解答题 · 第 3 题}

设 $y = f(x) = \left\{ \begin{aligned} & \sqrt[x]{x}, & x > 0, \\ & 0, & x = 0, \end{aligned} \right.$ 讨论 $f(x)$ 的连续性，并求 $f(x)$ 的单调区间、极值与渐近线.

\vfill

\Solution
% SOURCE line=1454 pdf_page=226 section=2.6

\Question{217}{第4章 · 解答题 · 第 4 题}

比较$\pi^{e}$与$e^{\pi}$的大小.

\vfill

\Solution
% SOURCE line=1458 pdf_page=227 section=2.6

\Question{218}{第4章 · 解答题 · 第 5 题}

设当 x > 0 时，方程 $\ln a = \frac{\ln x}{x}$ 有实根，求 a 的取值范围.

\vfill

\Solution
% SOURCE line=2151 pdf_page=345 section=2.6

\Question{219}{第7章 · 例题第1组 · 例 2}

设某商品的需求函数为 $Q = 100 - 5P$，其中价格 $P \in (0, 20)$，Q 为需求量。

(1) 求需求量对价格的弹性 $E_{d}(E_{d}>0)$;

(2) 证明：$\frac{dR}{dP}=Q(1-E_{d})$（R 表示收益），并用弹性 $E_{d}$ 说明当价格在何范围内时，降价反而使收益增加.

\vfill

\Solution
% SOURCE line=2167 pdf_page=347 section=2.6

\Question{220}{第7章 · 例题第1组 · 例 4}

为实现利润最大化，厂商需要对某商品确定其定价模型。设 Q 为该商品的需求量，P 为价格，MC 为边际成本，$\eta$ 为需求弹性（$\eta>0$）。

(1) 证明: 定价模型为 $P = \frac{MC}{1 - \frac{1}{\eta}}$;

(2) 若该商品的成本函数为 $C(Q) = 1600 + Q^{2}$，需求函数为 Q = 40 - P，试求由(1)中定价模型确定的此商品价格.

\vfill

\Solution
% SOURCE line=2189 pdf_page=351 section=2.6

\Question{221}{第7章 · 解答题 · 第 1 题}

设某产品在日产量为 x（件）时，其总成本函数为 $C(x)=100+18x-40\sqrt{x}$（百元），求使平均成本为最小的日产量.

\vfill

\Solution
% SOURCE line=2209 pdf_page=356 section=2.6

\Question{222}{第7章 · 解答题 · 第 6 题}

设某酒厂有一批新酿好酒，若现在 $(t=0)$ 出售，总收入为 $R_{0}$，若窑陈起来，按陈酒价格出售，t 年末总收入为 $R=R_{0}e^{\frac{2}{5}\sqrt{t}}$，现设银行年利率为 r，以连续复利计算，求窑陈多少年售出可使总收入现值最大，并求 r=0.06 时，t 的值.

\vfill

\Solution
% SOURCE line=2159 pdf_page=346 section=4.1

\Question{351}{第7章 · 例题第1组 · 例 3}

设某商品的最大需求量为1200件，该商品的需求函数$Q=Q(P)$，需求弹性$\eta=\frac{P}{120-P}(\eta>0)$，P为单价（万元）.

(1) 求需求函数的表达式;

(2) 求 P = 100 万元时的边际收益，并说明其经济意义.

\vfill

\Solution
% SOURCE line=2193 pdf_page=352 section=4.1

\Question{352}{第7章 · 解答题 · 第 2 题}

设某种商品的社会需求量 Q = Q(P)(P 表示价格)，其弹性 $E_{d} = \frac{2P^{2}}{256 - P^{2}}(E_{d} > 0)$，当 P = 10 时，Q = 156，一个工厂生产这种商品，其日总成本函数 $C(Q) = 4Q + 2000$，求该厂日产量 Q 为多少时，总利润最大.

\vfill

\Solution
% SOURCE line=2201 pdf_page=354 section=4.1

\Question{353}{第7章 · 解答题 · 第 4 题}

设某商品的需求量 Q 对价格 P 的弹性为 $P \ln 3$，若商品的市场最大需求量为 1500 件，求需求函数。

\vfill

\Solution


## tool · 2026-11-14T02:09:02Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-14T02:09:11Z


Script completed
Wall time 0.1 seconds
Output:

@@ 1292 2.6
先设 $p=f'(0)$。代入方程得 $f''(0)=-\frac12p^2$。若 $p\ne0$，函数在零点的斜率非零，故不是极值点。此时 $f''(0)<0$，且由方程 $f''=\frac12[3x-(f')^2]$ 知 $f''$ 连续，附近两侧都为负，也不是拐点。

若 $p=0$，则 $f''(0)=0$。对方程求导，得 $2f'''+2f'f''=3$，所以 $f'''(0)=\frac32$。于是 $f''(x)=\frac32x+o(x)$，两侧异号，$(0,f(0))$ 是拐点。同时 $f'(x)=\frac34x^2+o(x^2)>0$，两侧同为递增，所以仍不是极值点。

结论是 $x=0$ 总不是极值点，是否为拐点取决于 $f'(0)$，恰在 $f'(0)=0$ 时为拐点。
@@ 1296 2.6
导数为 $f'(x)=kx^2-1$，唯一正驻点是 $x=\frac1{\sqrt k}$。当 $k\geq1$ 时，有 $\frac1k\leq\frac1{\sqrt k}$，整个区间上导数非正，函数递减，所以最大值一定在 $x=0$ 取得，选 D。

为核实其余选项，若 $0<k<1$，驻点位于区间内部，函数先减后增，最大值需比较端点 $f(0)=0$ 与 $f(\frac1k)=\frac{1-3k}{3k^2}$。当 $k<\frac13$ 时后者较大，当 $k>\frac13$ 时前者较大。因此 A、B 对全部 $0<k<1$ 均不成立。$k=1$ 时 $f(1)=-\frac23<0$，也直接排除了 C。
@@ 1308 2.6
隐函数的极值点若可导，应满足 $y'=0$。对原方程求导并整理，得到 $y'=\frac{x-y}{3y^2-2y+x}$。因此候选点满足 $x=y$。代回原方程，得
\[
2y^3-y^2-1=(y-1)(2y^2+y+1)=0.
\]
二次因子的判别式为 $1-8<0$，所以唯一实候选点是 $(1,1)$。此处分母为 $2\ne0$，导数公式有效。对商再求导，在 $y'=0$ 的候选点只剩 $y''=\frac{1}{3y^2-2y+x}=\frac12>0$。因此这是极小值点，所求极小值是 $1$。

还能用原方程检查整体范围。配方得 $(x-y)^2=(y-1)(2y^2+y+1)$，左侧非负，右侧的二次因子恒正，故曲线上所有实点都有 $y\geq1$。在 $(1,1)$ 确实达到 $1$，也核实了这个最小值。
@@ 1312 2.6
图中画的是 $f'$，它的正负决定原函数的升降。从左向右读图，$f'$ 在 $x_1$ 由正变负，所以 $f$ 在 $x_1$ 由增变减，有极大值。在 $x_2$ 由负变正，有极小值。

还要检查 $x=0$。此点的 $f'$ 虽然没有给出，但左侧导数为正、右侧导数为负，且题设保证 $f$ 连续。因此 $f$ 在零点由增变减，零点也是极大值点。最后在 $x_3$，$f'$ 由负变正，又产生一个极小值点。

合计两个极小值点 $x_2,x_3$，两个极大值点 $x_1,0$，选 C。查极值时，导数不存在的连续接合点也需要检查。
@@ 1328 2.6
对于负数，$x^{\frac23}$ 表示 $\sqrt[3]{x^2}$。在 $x\ne0$ 处连续求导，得 $f'(x)=\frac53x^{-\frac13}(x-2)$，$f''(x)=\frac{10(x+1)}{9x^{\frac43}}$。分母始终为正，所以二阶导数的符号完全由 $x+1$ 决定。

在 $(-\infty,-1)$，$f''<0$，图像向下弯曲。在 $(-1,0)$ 和 $(0,+\infty)$，$f''>0$，图像向上弯曲。$x=-1$ 两侧凹凸改变，且曲线连续，代入得拐点 $(-1,-6)$。

$x=0$ 处导数不存在，需另外检查两侧凹凸。两侧二阶导数都为正，所以凹凸没有改变，零点不是拐点。凹凸区间也须在该尖点处分开。
@@ 1332 2.6
拐点要检查二阶导数在两侧是否变号。设 $a=f''(0)\ne0$，由 $f(0)=f'(0)=0$，有 $f(x)=\frac12ax^2+o(x^2)$、$f'(x)=ax+o(x)$、$f''(x)=a+o(1)$。

对 $F$ 用乘积法则求两次导数，得到
\[
F''(x)=(1-\mathrm e^{2x})f''(x)-4\mathrm e^{2x}f'(x)-4\mathrm e^{2x}f(x).
\]
由于 $1-\mathrm e^{2x}=-2x+o(x)$，代入各项后得到 $F''(x)=-6ax+o(x)$。于是 $\frac{F''(x)}x\to-6a\ne0$，在零点两侧 $F''$ 的符号相反。$F$ 连续且 $F(0)=0$，故 $(0,0)$ 是拐点。
@@ 1336 2.6
$g(x)$ 是连接 $(0,f(0))$ 与 $(1,f(1))$ 的直线。要比较曲线与这条弦，取任意 $0<x<1$，分别在 $[0,x]$ 和 $[x,1]$ 使用 Lagrange 中值定理，得
\[
\frac{f(x)-f(0)}x=f'(u),\qquad \frac{f(1)-f(x)}{1-x}=f'(v),\quad 0<u<x<v<1.
\]
若 $f''\geq0$，则 $f'$ 单调不减，所以第一个分式不超过第二个。乘以正数 $x(1-x)$ 并移项，得到 $f(x)\leq(1-x)f(0)+xf(1)=g(x)$。两个端点取等，故选 D。

只给 $f'\geq0$ 无法确定曲线位于弦的哪一侧。例如 $x^2$ 位于弦下方，$2x-x^2$ 位于弦上方，均在 $[0,1]$ 递增。
@@ 1348 2.6
判断两条曲线谁是谁的导数，可以对照“函数的极值点对应导函数的零点”。先看 $L_2$，它先下降、到最低点后再上升。恰在它的最低点对应横坐标处，$L_1$ 从负值穿过横轴变成正值，所以 $L_1$ 是 $L_2$ 的导函数。

再看 $L_3$，它先升、后降、再升，依次有一个极大值和一个极小值。这两点分别对应 $L_2$ 从正到负、从负到正穿过横轴的位置。因此 $L_2$ 是 $L_3$ 的导函数。

导数关系串起来为 $L_3\to L_2\to L_1$，所以 $L_1$ 对应 $f''$、$L_2$ 对应 $f'$、$L_3$ 对应 $f$，选 C。
@@ 1363 skip
本题要求曲率、曲率半径及曲率圆，这些概念不在教材上册十九节范围内。
@@ 1368 skip
本题依赖曲率圆给出的一阶和二阶导数信息，曲率圆不在教材上册范围内。
@@ 1380 skip
本题专门计算曲率圆，教材上册未介绍曲率，暂不收录。
@@ 1384 2.6
把左边记作 $H(x)$。三次函数在负无穷趋于负无穷，在正无穷趋于正无穷。求导得 $H'(x)=6(x-1)(x-2)$，所以先增、后减、再增，局部最高点在 $1$，最低点在 $2$。

算出 $H(1)=k+5$、$H(2)=k+4$。若最高点在横轴上方、最低点在横轴下方，三个单调区间各穿轴一次，所以 $-5<k<-4$ 时有三个不同实根。

$k=-5$ 或 $k=-4$ 时，某个极值点恰在横轴上，产生一个重根，另有一个不同实根，合计两个。其余情况下两个极值都在横轴同侧，只有最左段或最右段穿轴，合计一个实根。
@@ 1388 2.6
令 $H(x)=k\arctan x-x$。函数为奇函数，$x=0$ 总是一个根，所以只需研究正半轴。其导数为 $H'(x)=\frac{k}{1+x^2}-1$。

若 $k\leq1$，对 $x>0$ 总有 $H'(x)<0$。从 $H(0)=0$ 开始严格下降，因此正半轴无根，利用奇性，负半轴也无根，只有一个根 $0$。

若 $k>1$，导数在 $0<x<\sqrt{k-1}$ 为正，在 $x>\sqrt{k-1}$ 为负。函数从零先升至正的最大值，再严格下降到负无穷。由连续性与严格单调性，下降段恰有一个正根，其相反数是唯一负根。加上零点，共三个不同实根。
@@ 1392 2.6
因为 $x>0$，将方程解出参数 $a$，得到 $a=H(x)=\frac1x-\frac1{x^3}$。现在问题变成水平线 $y=a$ 与这条曲线有几个交点。

求导得 $H'(x)=\frac{3-x^2}{x^4}$。所以 $H$ 在 $(0,\sqrt3)$ 递增，在 $(\sqrt3,+\infty)$ 递减。左端趋于负无穷，右端从正侧趋于 $0$，而最大值为 $H(\sqrt3)=\frac{2}{3\sqrt3}$。

要让递增段和递减段各与水平线交一次，水平线必须严格位于 $0$ 与最大值之间。因此 $0<a<\frac{2}{3\sqrt3}$。取等于最大值时仅有切触点，取 $a=0$ 时右侧极限没有实际达到，均只有一个根。
@@ 1396 2.6
先查定义域的有限断点 $x=0$。对数项趋于 $\ln2$，而 $\frac1x$ 无界，所以 $x=0$ 是竖直渐近线。

当 $x\to-\infty$，$\frac1x\to0$ 且 $\ln(1+\mathrm e^x)\to0$，因此 $y=0$ 是这一端的水平渐近线。

当 $x\to+\infty$，从对数中提出 $\mathrm e^x$，得 $\ln(1+\mathrm e^x)=x+\ln(1+\mathrm e^{-x})$，从而 $y-x=\frac1x+\ln(1+\mathrm e^{-x})\to0$。所以 $y=x$ 是这一端的斜渐近线。共得到三条渐近线。
@@ 1402 2.6
原方程两边都是偶函数，正根与负根成对出现，先看 $x\geq0$。当 $x\geq1$ 时，左边至少为 $2$，右边至多为 $1$，所以无解。

在 $[0,1]$，令 $H(x)=x^{\frac14}+x^{\frac12}-\cos x$。端点值 $H(0)=-1<0$，$H(1)=2-\cos1>0$，连续性保证至少有一个根。对 $0<x<1$，有 $H'(x)=\frac1{4x^{\frac34}}+\frac1{2\sqrt{x}}+\sin x>0$，所以函数严格递增，只能有一个根。

该根不等于零，取它的相反数又得到唯一负根。故共两个不同实根，选 C。
@@ 1414 2.6
先根据 $f'$ 的正负数极值点。在 $x_1$，导数由正变负，原函数有极大值。在 $x_3$，导数由负变正，有极小值。$x_2$ 左右导数都为负，$x_5$ 左右导数都为正，这两点不产生极值。因此极值点共有两个。

再根据 $f'$ 的升降找拐点。$f'$ 下降时 $f''<0$，上升时 $f''>0$。图中 $f'$ 在 $x_2$ 由下降转为上升，在 $x_4$ 由上升转为下降，在 $x_5$ 又由下降转为上升，因此这三处凹凸改变。题设保证 $f$ 连续，即使 $x_2$ 处没有导数，仍能成为拐点。

合计两个极值点、三个拐点，选 B。
@@ 1428 2.6
先约分以分清真正的无穷间断点和可去间断点。除 $x=\pm1$ 外，$y=\frac{x(x+1)}{(x-1)(x+1)}=\frac{x}{x-1}=1+\frac1{x-1}$。

在 $x=1$ 附近，$\frac1{x-1}$ 无界，因此 $x=1$ 是竖直渐近线。在 $x=-1$ 附近，约分后的式子趋于 $\frac12$，原曲线只少了一个点，不产生渐近线。两端无穷远处 $\frac1{x-1}\to0$，所以水平渐近线为 $y=1$。共两条，选 C。
@@ 1442 2.6
定义域为 $x\ne\pm1$。先求一阶导数并通分，得 $y'=\frac{x^2(x^2-3)}{(x^2-1)^2}$。分母正，$x^2$ 非负，所以符号由 $x^2-3$ 决定。

递增区间为 $(-\infty,-\sqrt3)$、$(\sqrt3,+\infty)$。递减区间为 $(-\sqrt3,-1)$、$(-1,1)$、$(1,\sqrt3)$。其中 $x=0$ 仅使导数瞬间等于零，左右同为递减。极大值在 $x=-\sqrt3$，为 $-\frac{3\sqrt3}{2}$；极小值在 $x=\sqrt3$，为 $\frac{3\sqrt3}{2}$。

二阶导数为 $y''=\frac{2x(x^2+3)}{(x^2-1)^3}$。在 $(-\infty,-1)$、$(0,1)$ 为负，图像向下弯曲；在 $(-1,0)$、$(1,+\infty)$ 为正，图像向上弯曲。零点两侧凹凸改变，拐点为 $(0,0)$。$\pm1$ 不在定义域内，不能作拐点。
@@ 1446 2.6
先令 $t=\frac ba>1$，把含两个参数的不等式化成只含一个变量的 $\ln t>\frac{2(t-1)}{t+1}$。比较两个表达式时，可以研究它们的差。

设 $H(t)=\ln t-\frac{2(t-1)}{t+1}$。显然 $H(1)=0$，而
\[
H'(t)=\frac1t-\frac4{(t+1)^2}=\frac{(t-1)^2}{t(t+1)^2}>0\quad(t>1).
\]
所以从 $1$ 往右，$H$ 严格增加，$H(t)>H(1)=0$。将 $t=\frac ba$ 代回，即得到题目中的严格不等式。
@@ 1450 2.6
对 $x>0$ 写成 $f(x)=\mathrm e^{\frac{\ln x}{x}}$。初等函数在正半轴连续。在 $x\to0^+$ 时，$\frac{\ln x}{x}\to-\infty$，故 $f(x)\to0=f(0)$，所以在定义域 $[0,+\infty)$ 上处处连续，端点按右连续理解。

对正半轴用链式法则，得 $f'(x)=x^{\frac1x}\frac{1-\ln x}{x^2}$。除 $1-\ln x$ 外其余因子均为正，故在 $(0,\mathrm e)$ 递增，在 $(\mathrm e,+\infty)$ 递减。$x=\mathrm e$ 处取得极大值，也是最大值 $\mathrm e^{\frac1{\mathrm e}}$；内部没有极小值，端点 $x=0$ 取得全域最小值 $0$。

无穷远处 $\frac{\ln x}{x}\to0$，所以 $f(x)\to1$，渐近线为 $y=1$。有限端点的函数值有限，没有竖直渐近线。
@@ 1454 2.6
两个幂的底数和指数不同，先取自然对数，比较 $\mathrm e\ln\pi$ 与 $\pi$，再除以正数 $\mathrm e\pi$，就变成比较 $\frac{\ln\pi}{\pi}$ 与 $\frac1{\mathrm e}$。

令 $H(x)=\frac{\ln x}{x}$，其导数为 $H'(x)=\frac{1-\ln x}{x^2}$。当 $x>\mathrm e$ 时导数为负，所以 $H$ 在这一段严格递减。因为 $\pi>\mathrm e$，有 $H(\pi)<H(\mathrm e)=\frac1{\mathrm e}$。乘回正数并取指数，得到 $\pi^{\mathrm e}<\mathrm e^\pi$。
@@ 1458 2.6
左边 $\ln a$ 要有定义，先要求 $a>0$。再研究右边 $H(x)=\frac{\ln x}{x}$ 在正半轴能取到哪些值。其导数为 $H'(x)=\frac{1-\ln x}{x^2}$，在 $(0,\mathrm e)$ 为正，在 $(\mathrm e,+\infty)$ 为负，所以最大值在 $x=\mathrm e$ 取得，为 $\frac1{\mathrm e}$。

同时 $H(x)$ 在 $x\to0^+$ 时趋于负无穷，且在 $(0,\mathrm e]$ 连续递增，因此值域正好是 $(-\infty,\frac1{\mathrm e}]$。方程有解当且仅当 $\ln a\leq\frac1{\mathrm e}$，即 $0<a\leq\mathrm e^{\frac1{\mathrm e}}$。
@@ 2137 skip
该题的年复利提款需要无穷级数求和，属于教材上册未覆盖的无穷级数范围。
@@ 2141 skip
差分方程不在教材上册的常微分方程范围内。
@@ 2147 skip
本题只要求生产函数的经济弹性，教材上册未定义该概念，且题目没有给出定义。
@@ 2151 2.6
需求弹性 $E_d=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$，描述价格上涨百分之一时需求量下降百分之几。负号使通常递减的需求对应正弹性。因为 $Q=100-5P$，$Q'=-5$，所以 $E_d=\frac{5P}{100-5P}=\frac{P}{20-P}$。

销售收入等于单价乘销量，$R=PQ$。用乘积法则得 $R'=Q+PQ'=Q(1-E_d)$。当 $E_d>1$ 时，$R'<0$，所以降低价格会增加收入。解 $\frac{P}{20-P}>1$，分母在已知区间为正，得到 $10<P<20$。

也可直接核实 $R(P)=100P-5P^2$、$R'(P)=100-10P$，在上述区间确为负。
@@ 2159 4.1
需求弹性的定义是 $\eta=-\frac{P}{Q}Q'$。代入后得 $\frac{Q'}Q=-\frac1{120-P}$。分离变量并积分，得到 $\ln Q=\ln(120-P)+C$，即 $Q=A(120-P)$，其中 $0<P<120$。最大需求量在价格降至零时取得，因此 $120A=1200$，$A=10$，故 $Q=1200-10P$。

“边际收益”指多卖一件时收入大约增加多少，计算的是 $\frac{\mathrm dR}{\mathrm dQ}$。把单价写成销量的函数，$P=120-\frac Q{10}$，收入为 $R=PQ=120Q-\frac{Q^2}{10}$，故边际收益为 $120-\frac Q5$。

价格为 $100$ 万元时，销量 $Q=200$，边际收益是 $80$ 万元每件，即在该销量附近每多售一件，收入约增加 $80$ 万元。
@@ 2167 2.6
设价格可写成销量的函数 $P=P(Q)$，利润为 $\Pi(Q)=P(Q)Q-C(Q)$。边际成本指 $MC=C'(Q)$，需求弹性为 $\eta=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$。因此 $P'(Q)=-\frac{P}{\eta Q}$。

内点利润最大时，导数必须为零：$\Pi'=P+QP'-MC=P(1-\frac1\eta)-MC=0$。当 $\eta\ne1$ 时，解得定价模型 $P=\frac{MC}{1-\frac1\eta}$。这给出最优内点的必要条件，具体题中还需检查确为最大值。

（2）由 $Q=40-P$ 得 $P=40-Q$，故 $\Pi=(40-Q)Q-(1600+Q^2)=40Q-2Q^2-1600$。其导数为 $40-4Q$，二阶导数为 $-4<0$，所以 $Q=10$ 时利润最大，价格为 $P=30$。此时 $MC=20$、$\eta=\frac PQ=3$，代入模型也得到 $30$。
@@ 2175 skip
差分方程属于离散递推内容，教材上册未覆盖。
@@ 2179 skip
本题直接确定差分方程的系数，超出教材上册的微分方程范围。
@@ 2183 skip
差分方程的通解不在教材上册范围内。
@@ 2189 2.6
平均成本是每件分摊的总成本，故目标函数为 $A(x)=\frac{C(x)}x=\frac{100}{x}+18-\frac{40}{\sqrt{x}}$，其中 $x>0$。求导并把分母统一成正数 $x^2$，得到
\[
A'(x)=-\frac{100}{x^2}+\frac{20}{x^{\frac32}}=\frac{20(\sqrt{x}-5)}{x^2}.
\]
当 $0<x<25$ 时导数为负，$x>25$ 时为正，所以平均成本先减后增，在 $x=25$ 取得全域最小值。日产量应为 $25$ 件。代入可查平均成本为 $\frac{100}{25}+18-\frac{40}{5}=14$ 百元每件。
@@ 2193 4.1
先用弹性恢复需求函数。$E_d=-\frac{P}{Q}Q'$ 给出 $\frac{Q'}Q=-\frac{2P}{256-P^2}$。积分得 $Q=A(256-P^2)$，代入 $P=10,Q=156$ 得 $A=1$，所以 $Q=256-P^2$，有效价格区间为 $0<P<16$。

利润是销售收入减成本。以 $P$ 为自变量，$\Pi(P)=(P-4)(256-P^2)-2000$。求导得 $\Pi'=256+8P-3P^2=-3(P-\frac{32}{3})(P+8)$。因此在有效区间内，利润先增后减，唯一最大值点为 $P=\frac{32}{3}$。

对应日产量为 $Q=256-(\frac{32}{3})^2=\frac{1280}{9}$ 件，约 $142.22$ 件。这是连续模型的最优值。若实际日产量限整数，比较邻近的 $142$ 与 $143$ 件，$142$ 件的利润较高，取 $142$ 件。
@@ 2197 2.2
单价为 $P$、销量为 $Q(P)$ 时，总收益为 $R(P)=P Q(P)$。需求弹性的定义是 $\eta=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$，其中负号使价格升高、销量降低的需求对应正值。

因为两个乘数都随 $P$ 变化，要用乘积法则。计算得
\[
\frac{\mathrm dR}{\mathrm dP}=Q+P\frac{\mathrm dQ}{\mathrm dP}=Q\left(1+\frac P Q\frac{\mathrm dQ}{\mathrm dP}\right)=Q(1-\eta).
\]
代入题给表达式还可写成 $\frac{\mathrm dR}{\mathrm dP}=Q\frac{192-3P^2}{192-P^2}$。题目所要证明的恒等式直接来自收入定义与乘积求导法则。
@@ 2201 4.1
把需求弹性写成定义，$-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}=P\ln3$。在正价格处约去 $P$，得 $\frac{Q'}Q=-\ln3$。这是可以分离变量的一阶微分方程。

两边积分，得到 $\ln Q=-P\ln3+C$，所以 $Q=A\mathrm e^{-P\ln3}=A\cdot3^{-P}$。价格越低，需求越大，最大需求量是价格趋于零时的 $A$。题给最大需求为 $1500$，所以 $Q(P)=1500\cdot3^{-P}$，$P\geq0$。

检查 $Q'=-Q\ln3$，代回弹性定义得 $P\ln3$，与已知一致。
@@ 2205 2.3
收入等于单价乘需求量，$R(P)=P Q(P)$，用乘积法则得 $R'=Q+PQ'$。本题没有写明符号 $\xi_P$ 的定义，计算时须说明约定。

若采用需求价格弹性的正值约定 $\xi_P=-\frac{P}{Q}Q'$，则 $R'=Q(1-\xi_P)=10000\times0.8=8000$。由微分估计，价格增加 $1$ 元，收入约增加 $8000$ 元。

若 $\xi_P$ 采用一般函数的有符号弹性定义 $\xi_P=\frac{P}{Q}Q'$，则 $R'=Q(1+\xi_P)=12000$，收入约增加 $12000$ 元。两种符号定义相差一个负号，需与原讲义的定义核对。两者都是当前价格处的微分估计；题面未给完整需求函数，无法确定涨价一元后的精确收入差额。
@@ 2209 2.6
连续复利的折现因子是 $\mathrm e^{-rt}$。因此 $t$ 年后的收入折算到现在，现值为 $V(t)=R_0\mathrm e^{\frac25\sqrt t-rt}$，$t\geq0$。指数函数严格递增，只需使指数 $H(t)=\frac25\sqrt t-rt$ 最大。

在通常的正利率 $r>0$ 下，$H'(t)=\frac1{5\sqrt t}-r$。它在 $t<\frac1{25r^2}$ 时为正，在更大时为负，因此最优窖陈时间为 $t_*=\frac1{25r^2}$ 年，最大现值为 $R_0\mathrm e^{\frac1{25r}}$。

当 $r=0.06=\frac3{50}$，$t_*=\frac{100}{9}$ 年，约 $11.11$ 年。若 $r\leq0$，指数始终上升，没有有限的最优售出时间。
@@ 2213 2.3
收入为 $R(P)=P(100-5P)$，导数为 $R'(P)=100-10P$。在 $P=3$ 时导数为正，涨价增加收入；在 $P=12$ 时为负，涨价减少收入。

若用微分估计相对变化，$\frac{\mathrm dR}{R}=\frac{20-2P}{20-P}\frac{\mathrm dP}{P}$。因此（I）约增加 $\frac{14}{17}\times8.5\%=7\%$；（II）约减少 $\frac12\times5\%=2.5\%$。

本题给出了完整需求函数，还能求精确幅度。若涨价比例为 $\varepsilon$，直接把新价格 $P(1+\varepsilon)$ 代入收入函数，得到 $\frac{\Delta R}{R}=\frac{20-2P}{20-P}\varepsilon-\frac{P}{20-P}\varepsilon^2$。代入（I）的 $P=3,\varepsilon=0.085$，精确增加 $6.8725\%$；代入（II）的 $P=12,\varepsilon=0.05$，精确减少 $2.875\%$。微分估计忽略了这个二次项。
@@ 2221 skip
该题要求差分方程通解，超出教材上册的范围。

## 第2章 导数与微分

### 例题第1组

#### 例 1

设 $f(x)$ 在 x=0 处可导，$f(0)=0$，求 $\lim_{x\to0}\frac{x^2f(x)-2f(x^3)}{x^3}$.

#### 例 2

设 $y = f(x)$ 与 $y = x^{2} - x$ 在点 $(1,0)$ 处有公切线，求 $\lim_{n \to \infty} n f\left(\frac{n}{n+2}\right)$.

#### 例 3

设 $f(x)$ 在 x=0 的某邻域内有定义，且 $\lim_{x\to0}\frac{f(x)}{x}=0, f''(0)=4$，求 $\lim_{x\to0}\left[1+\frac{f(x)}{x}\right]^{\frac{1}{x}}$。

#### 例 4
#### 第 7 题

曲线 $\begin{cases} x = \arctan t, \\ y = \ln \sqrt{1+t^2} \end{cases}$ 上对应于 t = 1 点处的法线方程为___。

### 解答题

#### 第 1 题

求下列函数的导数或微分：
(I) $y = \frac{\mathrm{e}^{x} \sin x}{\sqrt{1 + x^2}}$, 求 $y'$;
(II) $y = (1 + x^2)^{\sqrt{x}}$ ($x > 0$), 求 $y'$;
(III) 设 $y = y(x)$ 由方程 $e^y + xy = e$ 确定，求 $\left. \frac{d^2 y}{dx^2} \right|_{x=0}$;
(IV) 设 $x = y^y$, 求 $dy$;
(V) (仅数学一、数学二要求) 设 $y = y(x)$ 由 $\left\{\begin{array}{l} x = \arctan t, \\ 2y - ty^2 = 5 - e^t \end{array}\right.$ 确定，求 $\frac{dy}{dx}$;
(VI) 设 $y = f\left(\frac{3x - 2}{3x + 2}\right)$, 且 $f'(x) = \arcsin x^2$, 求 $\left. \frac{dy}{dx} \right|_{x=0}$.

#### 第 2 题

求高阶导数：

（Ⅰ）设 $y = e^{x} \sin x$，求 $y^{(n)}(x)$；

（Ⅱ）设 $y = x^{2}\ln(1+x)$，求 $y^{(10)}(0)$

设某产品在日产量为 x（件）时，其总成本函数为 $C(x)=100+18x-40\sqrt{x}$（百元），求使平均成本为最小的日产量.

#### 第 2 题

设某种商品的社会需求量 Q = Q(P)(P 表示价格)，其弹性 $E_{d} = \frac{2P^{2}}{256 - P^{2}}(E_{d} > 0)$，当 P = 10 时，Q = 156，一个工厂生产这种商品，其日总成本函数 $C(Q) = 4Q + 2000$，求该厂日产量 Q 为多少时，总利润最大.

#### 第 3 题

某商品的需求量 $Q = Q(P)$，需求对价格的弹性 $\eta = \frac{2P^{2}}{192 - P^{2}}$，若 R 为总收益函数，证明：$\frac{dR}{dP} = Q(1 - \eta)$.

#### 第 4 题

设某商品的需求量 Q 对价格 P 的弹性为 $P \ln 3$，若商品的市场最大需求量为 1500 件，求需求函数。

#### 第 5 题

设某产品的需求函数 $Q = Q(P)$，其对价格 P 的弹性 $\xi_{P} = 0.2$，当需求量为 10000 件时，价格增加 1 元，问此时会使产品的收益增加多少元？

#### 第 6 题

设某酒厂有一批新酿好酒，若现在 $(t=0)$ 出售，总收入为 $R_{0}$，若窑陈起来，按陈酒价格出售，t 年末总收入为 $R=R_{0}e^{\frac{2}{5}\sqrt{t}}$，现设银行年利率为 r，以连续复利计算，求窑陈多少年售出可使总收入现值最大，并求 r=0.06 时，t 的值.

#### 第 7 题

设某商品需求函数为 Q = 100 - 5P.

（Ⅰ）当 P = 3 时，问涨价会使销售收入增加还是减少？若价格上涨幅度为 8.5%，则对销售收入的影响幅度为多少？

（Ⅱ）当P=12时，问涨价会使销售收入增加还是减少？若价格上涨幅度为5%，则对销售收入影响的幅度为多少？

#### 第 8 题

求差分方程 $y_{t+1}-2y_t=2^t$ 的通解.


## tool · 2026-11-14T02:13:30Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-14T02:13:35Z




## tool · 2026-11-14T02:16:15Z


Script completed
Wall time 0.1 seconds
Output:

@@ 1458 2.6
左边 $\ln a$ 要有定义，先要求 $a>0$。再研究右边 $H(x)=\frac{\ln x}{x}$ 在正半轴能取到哪些值。其导数为 $H'(x)=\frac{1-\ln x}{x^2}$，在 $(0,\mathrm e)$ 为正，在 $(\mathrm e,+\infty)$ 为负，所以最大值在 $x=\mathrm e$ 取得，为 $\frac1{\mathrm e}$。

同时 $H(x)$ 在 $x\to0^+$ 时趋于负无穷，且在 $(0,\mathrm e]$ 连续递增，因此值域正好是 $(-\infty,\frac1{\mathrm e}]$。方程有解当且仅当 $\ln a\leq\frac1{\mathrm e}$，即 $0<a\leq\mathrm e^{\frac1{\mathrm e}}$。
@@ 2137 skip
该题的年复利提款需要无穷级数求和，属于教材上册未覆盖的无穷级数范围。
@@ 2141 skip
差分方程不在教材上册的常微分方程范围内。
@@ 2147 skip
本题只要求生产函数的经济弹性，教材上册未定义该概念，且题目没有给出定义。
@@ 2151 2.6
需求弹性 $E_d=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$，描述价格上涨百分之一时需求量下降百分之几。负号使通常递减的需求对应正弹性。因为 $Q=100-5P$，$Q'=-5$，所以 $E_d=\frac{5P}{100-5P}=\frac{P}{20-P}$。

销售收入等于单价乘销量，$R=PQ$。用乘积法则得 $R'=Q+PQ'=Q(1-E_d)$。当 $E_d>1$ 时，$R'<0$，所以降低价格会增加收入。解 $\frac{P}{20-P}>1$，分母在已知区间为正，得到 $10<P<20$。

也可直接核实 $R(P)=100P-5P^2$、$R'(P)=100-10P$，在上述区间确为负。
@@ 2159 4.1
需求弹性的定义是 $\eta=-\frac{P}{Q}Q'$。代入后得 $\frac{Q'}Q=-\frac1{120-P}$。分离变量并积分，得到 $\ln Q=\ln(120-P)+C$，即 $Q=A(120-P)$，其中 $0<P<120$。最大需求量在价格降至零时取得，因此 $120A=1200$，$A=10$，故 $Q=1200-10P$。

“边际收益”指多卖一件时收入大约增加多少，计算的是 $\frac{\mathrm dR}{\mathrm dQ}$。把单价写成销量的函数，$P=120-\frac Q{10}$，收入为 $R=PQ=120Q-\frac{Q^2}{10}$，故边际收益为 $120-\frac Q5$。

价格为 $100$ 万元时，销量 $Q=200$，边际收益是 $80$ 万元每件，即在该销量附近每多售一件，收入约增加 $80$ 万元。
@@ 2167 2.6
设价格可写成销量的函数 $P=P(Q)$，利润为 $\Pi(Q)=P(Q)Q-C(Q)$。边际成本指 $MC=C'(Q)$，需求弹性为 $\eta=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$。因此 $P'(Q)=-\frac{P}{\eta Q}$。

内点利润最大时，导数必须为零：$\Pi'=P+QP'-MC=P(1-\frac1\eta)-MC=0$。当 $\eta\ne1$ 时，解得定价模型 $P=\frac{MC}{1-\frac1\eta}$。这给出最优内点的必要条件，具体题中还需检查确为最大值。

（2）由 $Q=40-P$ 得 $P=40-Q$，故 $\Pi=(40-Q)Q-(1600+Q^2)=40Q-2Q^2-1600$。其导数为 $40-4Q$，二阶导数为 $-4<0$，所以 $Q=10$ 时利润最大，价格为 $P=30$。此时 $MC=20$、$\eta=\frac PQ=3$，代入模型也得到 $30$。
@@ 2175 skip
差分方程属于离散递推内容，教材上册未覆盖。
@@ 2179 skip
本题直接确定差分方程的系数，超出教材上册的微分方程范围。
@@ 2183 skip
差分方程的通解不在教材上册范围内。
@@ 2189 2.6
平均成本是每件分摊的总成本，故目标函数为 $A(x)=\frac{C(x)}x=\frac{100}{x}+18-\frac{40}{\sqrt{x}}$，其中 $x>0$。求导并把分母统一成正数 $x^2$，得到
\[
A'(x)=-\frac{100}{x^2}+\frac{20}{x^{\frac32}}=\frac{20(\sqrt{x}-5)}{x^2}.
\]
当 $0<x<25$ 时导数为负，$x>25$ 时为正，所以平均成本先减后增，在 $x=25$ 取得全域最小值。日产量应为 $25$ 件。代入可查平均成本为 $\frac{100}{25}+18-\frac{40}{5}=14$ 百元每件。
@@ 2193 4.1
先用弹性恢复需求函数。$E_d=-\frac{P}{Q}Q'$ 给出 $\frac{Q'}Q=-\frac{2P}{256-P^2}$。积分得 $Q=A(256-P^2)$，代入 $P=10,Q=156$ 得 $A=1$，所以 $Q=256-P^2$，有效价格区间为 $0<P<16$。

利润是销售收入减成本。以 $P$ 为自变量，$\Pi(P)=(P-4)(256-P^2)-2000$。求导得 $\Pi'=256+8P-3P^2=-3(P-\frac{32}{3})(P+8)$。因此在有效区间内，利润先增后减，唯一最大值点为 $P=\frac{32}{3}$。

对应日产量为 $Q=256-(\frac{32}{3})^2=\frac{1280}{9}$ 件，约 $142.22$ 件。这是连续模型的最优值。若实际日产量限整数，比较邻近的 $142$ 与 $143$ 件，$142$ 件的利润较高，取 $142$ 件。
@@ 2197 2.2
单价为 $P$、销量为 $Q(P)$ 时，总收益为 $R(P)=P Q(P)$。需求弹性的定义是 $\eta=-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}$，其中负号使价格升高、销量降低的需求对应正值。

因为两个乘数都随 $P$ 变化，要用乘积法则。计算得
\[
\frac{\mathrm dR}{\mathrm dP}=Q+P\frac{\mathrm dQ}{\mathrm dP}=Q\left(1+\frac P Q\frac{\mathrm dQ}{\mathrm dP}\right)=Q(1-\eta).
\]
代入题给表达式还可写成 $\frac{\mathrm dR}{\mathrm dP}=Q\frac{192-3P^2}{192-P^2}$。题目所要证明的恒等式直接来自收入定义与乘积求导法则。
@@ 2201 4.1
把需求弹性写成定义，$-\frac{P}{Q}\frac{\mathrm dQ}{\mathrm dP}=P\ln3$。在正价格处约去 $P$，得 $\frac{Q'}Q=-\ln3$。这是可以分离变量的一阶微分方程。

两边积分，得到 $\ln Q=-P\ln3+C$，所以 $Q=A\mathrm e^{-P\ln3}=A\cdot3^{-P}$。价格越低，需求越大，最大需求量是价格趋于零时的 $A$。题给最大需求为 $1500$，所以 $Q(P)=1500\cdot3^{-P}$，$P\geq0$。

检查 $Q'=-Q\ln3$，代回弹性定义得 $P\ln3$，与已知一致。
@@ 2205 2.3
收入等于单价乘需求量，$R(P)=P Q(P)$，用乘积法则得 $R'=Q+PQ'$。本题没有写明符号 $\xi_P$ 的定义，计算时须说明约定。

若采用需求价格弹性的正值约定 $\xi_P=-\frac{P}{Q}Q'$，则 $R'=Q(1-\xi_P)=10000\times0.8=8000$。由微分估计，价格增加 $1$ 元，收入约增加 $8000$ 元。

若 $\xi_P$ 采用一般函数的有符号弹性定义 $\xi_P=\frac{P}{Q}Q'$，则 $R'=Q(1+\xi_P)=12000$，收入约增加 $12000$ 元。两种符号定义相差一个负号，需与原讲义的定义核对。两者都是当前价格处的微分估计；题面未给完整需求函数，无法确定涨价一元后的精确收入差额。
@@ 2209 2.6
连续复利的折现因子是 $\mathrm e^{-rt}$。因此 $t$ 年后的收入折算到现在，现值为 $V(t)=R_0\mathrm e^{\frac25\sqrt t-rt}$，$t\geq0$。指数函数严格递增，只需使指数 $H(t)=\frac25\sqrt t-rt$ 最大。

在通常的正利率 $r>0$ 下，$H'(t)=\frac1{5\sqrt t}-r$。它在 $t<\frac1{25r^2}$ 时为正，在更大时为负，因此最优窖陈时间为 $t_*=\frac1{25r^2}$ 年，最大现值为 $R_0\mathrm e^{\frac1{25r}}$。

当 $r=0.06=\frac3{50}$，$t_*=\frac{100}{9}$ 年，约 $11.11$ 年。若 $r\leq0$，指数始终上升，没有有限的最优售出时间。
@@ 2213 2.3
收入为 $R(P)=P(100-5P)$，导数为 $R'(P)=100-10P$。在 $P=3$ 时导数为正，涨价增加收入；在 $P=12$ 时为负，涨价减少收入。

若用微分估计相对变化，$\frac{\mathrm dR}{R}=\frac{20-2P}{20-P}\frac{\mathrm dP}{P}$。因此（I）约增加 $\frac{14}{17}\times8.5\%=7\%$；（II）约减少 $\frac12\times5\%=2.5\%$。

本题给出了完整需求函数，还能求精确幅度。若涨价比例为 $\varepsilon$，直接把新价格 $P(1+\varepsilon)$ 代入收入函数，得到 $\frac{\Delta R}{R}=\frac{20-2P}{20-P}\varepsilon-\frac{P}{20-P}\varepsilon^2$。代入（I）的 $P=3,\varepsilon=0.085$，精确增加 $6.8725\%$；代入（II）的 $P=12,\varepsilon=0.05$，精确减少 $2.875\%$。微分估计忽略了这个二次项。
@@ 2221 skip
该题要求差分方程通解，超出教材上册的范围。

{}

## tool · 2026-11-14T02:16:26Z


Script completed
Wall time 0.1 seconds
Output:

1:@@ 533 2.1 1
2:\Known
4:\Method
6:\Derive
12:\Check
14:@@ 537 2.1 2
15:\Known
17:\Method
19:\Derive
25:\Check
27:@@ 541 2.5 2
28:\Known
30:\Method
32:\Derive
42:\Check
44:@@ 545 2.1 3
45:\Known
47:\Method
49:\Derive
56:\Check
58:@@ 557 2.1 2
59:\Known
61:\Method
63:\Derive
66:\Check
68:@@ 569 2.1 1
69:\Known
71:\Method
73:\Derive
79:\Check
81:@@ 573 2.3 2
82:\Known
84:\Method
86:\Derive
92:\Check
94:@@ 585 2.1 2
95:\Known
97:\Method
99:\Derive
110:\Check
112:@@ 597 2.1 2
113:\Known
115:\Method
117:\Derive
123:第一项趋于 $2$；第二项为 $\frac12(\frac{\sin(x/2)}{x/2})^2$，趋于 $\frac12$；第三项由 $\lim_{t\to0}\frac{\ln(1+t)}t=1$ 趋于 $1$。乘积极限为 $2\cdot\frac12\cdot1=1$。
124:\Check
126:@@ 601 2.5 2
127:\Known
129:\Method
131:\Derive
143:\Check
145:@@ 605 2.2 2
146:\Known
148:\Method
150:\Derive
157:\Check
159:@@ 609 2.1 3
160:\Known
162:\Method
164:\Derive
172:\Check
174:@@ 613 2.5 2
175:\Known
177:\Method
179:\Derive
186:\Check
188:@@ 619 2.2 3
189:\Known
191:\Method
193:\Derive
208:\Check
210:@@ 623 2.1 2
211:\Known
213:\Method
215:\Derive
221:\Check
223:@@ 635 2.1 2
224:\Known
226:\Method
228:\Derive
236:\Check
238:@@ 647 2.2 2
239:\Known
241:\Method
243:\Derive
250:\Check
252:@@ 659 2.1 3
253:\Known
255:\Method
257:\Derive
268:\Check
270:@@ 673 2.2 2
271:\Known
273:\Method
275:\Derive
285:\Check
287:@@ 677 2.2 3
288:\Known
290:\Method
292:\Derive
298:\Check
300:@@ 681 2.3 2
301:\Known
303:\Method
305:\Derive
311:\Check
313:@@ 685 2.2 2
314:\Known
316:\Method
318:\Derive
328:\Check
330:@@ 689 2.2 2
331:\Known
333:\Method
335:\Derive
342:\Check
344:@@ 693 2.2 2
345:\Known
347:\Method
349:\Derive
360:\Check
362:@@ 697 3.2 2
363:\Known
365:\Method
367:\Derive
377:\Check
379:@@ 701 2.2 2
380:\Known
382:\Method
384:\Derive
391:\Check
393:@@ 705 2.2 2
394:\Known
396:\Method
398:\Derive
404:\Check
406:@@ 709 2.2 3
407:\Known
409:\Method
411:\Derive
419:两交界的左右极限分别为 $-1,2$，都等于函数值，故无间断点。$x=-1$ 处左导数为 $\frac1{4\sqrt{(1-x)/2}}|_{x=-1}=\frac14$，右导数为 $\frac1{3x^{\frac23}}|_{x=-1}=\frac13$，不相等。$x=0$ 处差商为 $\frac{\sqrt[3]x}{x}=\frac1{|x|^{\frac23}}\to+\infty$，无有限导数。$x=8$ 两侧导数均为 $\frac1{12}$。各支其余点可直接求导。
420:\Check
422:@@ 717 2.2 2
423:\Known
425:\Method
427:\Derive
437:\Check
439:@@ 721 2.2 3
440:\Known
442:\Method
444:\Derive
451:\Check
453:@@ 725 2.2 3
454:\Known
456:\Method
458:\Derive
471:\Check
473:@@ 729 2.2 2
474:\Known
476:\Method
478:\Derive
484:\Check
486:@@ 740 2.1 2
487:\Known
489:\Method
491:\Derive
497:\Check
499:@@ 752 2.1 2
500:\Known
502:\Method
504:\Derive
511:\Check
513:@@ 764 2.1 1
514:\Known
516:\Method
518:\Derive
525:\Check
527:@@ 776 2.1 2
528:\Known
530:\Method
532:\Derive
538:\Check
540:@@ 788 2.1 2
541:\Known
543:\Method
545:\Derive
553:\Check
555:@@ 800 2.2 3
556:\Known
558:\Method
560:\Derive
568:\Check
570:@@ 812 2.1 3
571:\Known
573:\Method
575:\Derive
583:\Check
585:@@ 826 2.1 2
586:\Known
588:\Method
590:\Derive
595:当 $n\geq2$ 时可取对数，$n\ln(1-\frac1n)=\frac{\ln(1-1/n)}{-1/n}(-1)\to-1$，利用指数连续性得极限为 $\mathrm e^{-1}$。
596:\Check
598:@@ 830 2.2 2
599:\Known
601:\Method
603:\Derive
605:\Check
607:@@ 834 2.2 2
608:\Known
610:\Method
612:\Derive
618:\Check
620:@@ 838 2.2 2
621:\Known
623:\Method
625:\Derive
634:\Check
636:@@ 842 2.1 2
637:\Known
639:\Method
641:\Derive
647:\Check
649:@@ 846 2.2 3
650:\Known
652:\Method
654:\Derive
667:\Check
669:@@ 850 2.2 2
670:\Known
672:\Method
674:\Derive
681:\Check
683:@@ 856 2.2 3
684:\Known
686:\Method
688:\Derive
712:\Check
714:@@ 866 2.2 3
715:\Known
717:\Method
719:\Derive
741:\Check
743:@@ 876 2.2 2
744:\Known
746:\Method
748:\Derive
759:\Check
761:@@ 880 2.1 3
762:\Known
764:\Method
766:\Derive
775:\Check
777:@@ 884 2.5 3
778:\Known
780:\Method
782:\Derive
790:\Check
792:@@ 892 2.1 2
793:\Known
795:\Method
797:\Derive
807:\Check
809:@@ 896 2.2 2
810:\Known
812:\Method
814:\Derive
817:\Check
819:@@ 1250 2.6 3
820:\Known
822:\Method
824:\Derive
832:\Check
834:@@ 1256 2.6 3
835:\Known
837:\Method
839:\Derive
856:\Check
858:@@ 1264 2.6 3
859:\Known
861:\Method
863:\Derive
875:\Check
877:@@ 1268 2.6 2
878:\Known
880:\Method
882:\Derive
891:\Check
893:@@ 1272 2.6 3
894:\Known
896:\Method
898:\Derive
911:\Check
913:@@ 1276 2.6 2
914:\Known
916:\Method
918:\Derive
921:\Check
923:@@ 1280 2.6 2
924:\Known
926:\Method
928:\Derive
934:\Check
936:@@ 1292 2.6 4
937:\Known
939:\Method
941:\Derive
953:\Check
955:@@ 1296 2.6 3
956:\Known
958:\Method
960:\Derive
967:\Check
969:@@ 1308 2.6 3
970:\Known
972:\Method
974:\Derive
985:\Check
987:@@ 1312 2.6 2
988:\Known
990:\Method
992:\Derive
995:\Check
997:@@ 1328 2.6 3
998:\Known
1000:\Method
1002:\Derive
1011:\Check
1013:@@ 1332 2.6 3
1014:\Known
1016:\Method
1018:\Derive
1029:\Check
1031:@@ 1336 2.6 3
1032:\Known
1034:\Method
1036:\Derive
1044:\Check
1046:@@ 1348 2.6 2
1047:\Known
1049:\Method
1051:\Derive
1054:\Check
1056:@@ 1363 skip 0
1058:@@ 1368 skip 0
1060:@@ 1380 skip 0
1062:@@ 1384 2.6 3
1063:\Known
1065:\Method
1067:\Derive
1072:\Check
1074:@@ 1388 2.6 3
1075:\Known
1077:\Method
1079:\Derive
1083:\Check
1085:@@ 1392 2.6 3
1086:\Known
1088:\Method
1090:\Derive
1097:\Check
1099:@@ 1396 2.6 2
1100:\Known
1102:\Method
1104:\Derive
1112:\Check
1114:@@ 1402 2.6 2
1115:\Known
1117:\Method
1119:\Derive
1126:\Check
1128:@@ 1414 2.6 3
1129:\Known
1131:\Method
1133:\Derive
1136:\Check
1138:@@ 1428 2.6 2
1139:\Known
1141:\Method
1143:\Derive
1149:\Check
1151:@@ 1442 2.6 3
1152:\Known
1154:\Method
1156:\Derive
1169:\Check
1171:@@ 1446 2.6 2
1172:\Known
1174:\Method
1176:\Derive
1184:\Check
1186:@@ 1450 2.6 3
1187:\Known
1189:\Method
1191:\Derive
1199:\Check
1201:@@ 1454 2.6 2
1202:\Known
1204:\Method
1206:\Derive
1213:\Check
1215:@@ 1458 2.6 2
1216:\Known
1218:\Method
1220:\Derive
1226:\Check
1228:@@ 2137 skip 0
1230:@@ 2141 skip 0
1232:@@ 2147 skip 0
1234:@@ 2151 2.6 2
1235:\Known
1237:\Method
1239:\Derive
1249:\Check
1251:@@ 2159 4.1 3
1252:\Known
1254:\Method
1256:\Derive
1267:\Check
1269:@@ 2167 2.6 3
1270:\Known
1272:\Method
1274:\Derive
1287:\Check
1288:价格为 $30$。此时 $MC=20,\eta=3$，模型给出 $\frac{20}{1-1/3}=30$。固定成本使最大利润仍可能为负，但不改变给定生产模型下利润最大时的价格。
1289:@@ 2175 skip 0
1291:@@ 2179 skip 0
1293:@@ 2183 skip 0
1295:@@ 2189 2.6 2
1296:\Known
1298:\Method
1300:\Derive
1307:\Check
1309:@@ 2193 4.1 3
1310:\Known
1312:\Method
1314:\Derive
1328:\Check
1330:@@ 2197 2.2 1
1331:\Known
1333:\Method
1335:\Derive
1342:\Check
1344:@@ 2201 4.1 2
1345:\Known
1347:\Method
1349:\Derive
1355:\Check
1357:@@ 2205 2.3 2
1358:\Known
1360:\Method
1362:\Derive
1369:\Check
1371:@@ 2209 2.6 3
1372:\Known
1374:\Method
1376:\Derive
1386:最大现值为 $R_0\mathrm e^{\frac1{25r}}$。当 $r=0.06=\frac3{50}$，$t_*=\frac1{25(3/50)^2}=\frac{100}9\approx11.11$ 年。
1387:\Check
1389:@@ 2213 2.3 3
1390:\Known
1392:\Method
1394:\Derive
1407:\Check
1409:@@ 2221 skip 0

zsh:1: command not found: python


## tool · 2026-11-14T02:17:04Z


Script completed
Wall time 0.1 seconds
Output:

{}
{'total': 100, 'included': 90, 'skip': 10, 'unique': 100, 'difficulty': {'1': 4, '2': 50, '3': 35, '4': 1, '0': 10}}
{142: -1051.8548882115538, 143: -1051.8891487789451}


## tool · 2026-11-14T02:17:11Z




## tool · 2026-11-14T02:17:25Z


Script completed
Wall time 0.1 seconds
Output:

Traceback (most recent call last):
  File "<string>", line 1, in <module>
ModuleNotFoundError: No module named 'sympy'

1:@@ 533 2.1 1
14:@@ 537 2.1 2
27:@@ 541 2.5 2
43:由指数函数连续，原极限为 $\mathrm e^2$。必须先证明 $f(0)=f'(0)=0$，不能只凭二阶导数直接省略 Taylor 公式的前两项。
44:@@ 545 2.1 3
58:@@ 557 2.1 2
68:@@ 569 2.1 1
81:@@ 573 2.3 2
94:@@ 585 2.1 2
112:@@ 597 2.1 2
126:@@ 601 2.5 2
145:@@ 605 2.2 2
159:@@ 609 2.1 3
173:切线为 $y-f(6)=f'(6)(x-6)$，即 $y=2(x-6)$。它经过 $(6,0)$，斜率为 $2$；周期性转移的是局部增量，不能只转移函数值而省略导数依据。
174:@@ 613 2.5 2
188:@@ 619 2.2 3
196:f(x)=\begin{cases}x\ln(1+x),&x\geq0,\\
198:\end{cases}
202:f'(x)=\begin{cases}\ln(1+x)+\frac{x}{1+x},&x>0,\\
205:\end{cases}
210:@@ 623 2.1 2
223:@@ 635 2.1 2
238:@@ 647 2.2 2
246:f^{(j)}(x)=\begin{cases}\frac{2\cdot5!}{(5-j)!}x^{5-j},&x>0,\\0,&x\leq0.
247:\end{cases}
252:@@ 659 2.1 3
270:@@ 673 2.2 2
287:@@ 677 2.2 3
300:@@ 681 2.3 2
313:@@ 685 2.2 2
330:@@ 689 2.2 2
344:@@ 693 2.2 2
362:@@ 697 3.2 2
379:@@ 701 2.2 2
393:@@ 705 2.2 2
406:@@ 709 2.2 3
414:g(x)=\begin{cases}-\sqrt{\frac{1-x}{2}},&x<-1,\\
417:\end{cases}
422:@@ 717 2.2 2
439:@@ 721 2.2 3
452:$f^{(n)}(x)=n![f(x)]^{n+1}$。全程没有除以 $f$，因而 $f$ 为零的点和恒零解也包括在内；不能只观察前三阶就省略归纳证明。
453:@@ 725 2.2 3
473:@@ 729 2.2 2
486:@@ 740 2.1 2
499:@@ 752 2.1 2
513:@@ 764 2.1 1
527:@@ 776 2.1 2
540:@@ 788 2.1 2
555:@@ 800 2.2 3
570:@@ 812 2.1 3
585:@@ 826 2.1 2
598:@@ 830 2.2 2
607:@@ 834 2.2 2
620:@@ 838 2.2 2
636:@@ 842 2.1 2
649:@@ 846 2.2 3
669:@@ 850 2.2 2
683:@@ 856 2.2 3
714:@@ 866 2.2 3
743:@@ 876 2.2 2
761:@@ 880 2.1 3
777:@@ 884 2.5 3
792:@@ 892 2.1 2
809:@@ 896 2.2 2
819:@@ 1250 2.6 3
834:@@ 1256 2.6 3
858:@@ 1264 2.6 3
877:@@ 1268 2.6 2
893:@@ 1272 2.6 3
913:@@ 1276 2.6 2
923:@@ 1280 2.6 2
936:@@ 1292 2.6 4
955:@@ 1296 2.6 3
969:@@ 1308 2.6 3
987:@@ 1312 2.6 2
997:@@ 1328 2.6 3
1013:@@ 1332 2.6 3
1031:@@ 1336 2.6 3
1046:@@ 1348 2.6 2
1056:@@ 1363 skip 0
1058:@@ 1368 skip 0
1060:@@ 1380 skip 0
1062:@@ 1384 2.6 3
1074:@@ 1388 2.6 3
1085:@@ 1392 2.6 3
1099:@@ 1396 2.6 2
1114:@@ 1402 2.6 2
1128:@@ 1414 2.6 3
1138:@@ 1428 2.6 2
1151:@@ 1442 2.6 3
1171:@@ 1446 2.6 2
1186:@@ 1450 2.6 3
1201:@@ 1454 2.6 2
1215:@@ 1458 2.6 2
1228:@@ 2137 skip 0
1230:@@ 2141 skip 0
1232:@@ 2147 skip 0
1234:@@ 2151 2.6 2
1251:@@ 2159 4.1 3
1269:@@ 2167 2.6 3
1289:@@ 2175 skip 0
1291:@@ 2179 skip 0
1293:@@ 2183 skip 0
1295:@@ 2189 2.6 2
1309:@@ 2193 4.1 3
1330:@@ 2197 2.2 1
1344:@@ 2201 4.1 2
1357:@@ 2205 2.3 2
1371:@@ 2209 2.6 3
1389:@@ 2213 2.3 3
1408:两种方法的方向相同：第一问增加，第二问减少。微分答案分别约 $7\%$、约 $2.5\%$，精确幅度分别为 $6.8725\%$、$2.875\%$；差别恰是被微分忽略的二次项。
1409:@@ 2221 skip 0


## tool · 2026-11-14T02:17:42Z


Script completed
Wall time 0.2 seconds
Output:

{'complex_step_derivative_checks': 33, 'passed': 33}


## tool · 2026-11-14T02:17:49Z




## assistant · 2026-11-14T02:17:54Z

已完成并冻结 `.question-bank-work/lilin-ipad-derivatives.txt`：

- 保留100条、90题收录、10条skip。
- 90题均重新编写完整四段解析并评级，所有小问逐项处理。
- 四宏数量与顺序、数学定界符、括号及禁用字符检查通过。
- 33项数值求导核验通过；核实2193整数最优产量为142件。

未编译整体PDF、未新增视觉检查；856(VI)定义域与2205弹性符号疑义已保留说明。
