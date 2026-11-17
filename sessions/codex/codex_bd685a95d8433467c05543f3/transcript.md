# 01a1cd5d-d5cd-7c23-947f-363f788e9112

来源：codex

项目：/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank

## developer · 2026-11-12T01:27:25Z

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



## developer · 2026-11-12T01:27:25Z

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
- `r16` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/heygen/4.6.0/skills`
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
- imagegen: Generate or edit raster images when the task benefits from AI-crea (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, settings, (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped instruc (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list (file: r2/skill-installer/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:database-access: Explore and query databases on the user's servers (Postgres, MySQL (file: r15/database-access/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:deploy-check: Verify a server after a deployment, update or restart — services u (file: r15/deploy-check/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:incident-triage: Work through a server alert or outage step by step — disk full,  (file: r15/incident-triage/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:run-commands: Run shell commands and edit files on the user's servers through  (file: r15/run-commands/SKILL.md)
- app-6aa2c81fc7c48191a06e101858e41837:server-health: Answer "how are my servers doing", "is everything up", "anything w (file: r15/server-health/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, t (file: r1/apple-design/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, t (file: r0/apple-design/SKILL.md)
- archify: Create polished, validated architecture, workflow, sequence, dat (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Codex research, writing, manuscript review, study screening, a (file: r3/ars-codex/3.24.2/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Structures Benchmark and Evaluation papers using the five-pillar f (file: r0/benchmark-paper-template/SKILL.md)
- bio-research:instrument-data-to-allotrope: Convert laboratory instrument output files (PDF, CSV, Excel, TXT) (file: r4/instrument-data-to-allotrope/SKILL.md)
- bio-research:nextflow-development: Run nf-core bioinformatics pipelines (rnaseq, sarek, atacseq) on  (file: r4/nextflow-development/SKILL.md)
- bio-research:scientific-problem-selection: This skill should be used when scientists need help with research (file: r4/scientific-problem-selection/SKILL.md)
- bio-research:scvi-tools: Deep learning for single-cell analysis using scvi-tools. This ski (file: r4/scvi-tools/SKILL.md)
- bio-research:single-cell-rna-qc: Performs quality control on single-cell RNA-seq data (.h5ad or .h (file: r4/single-cell-rna-qc/SKILL.md)
- bio-research:start: Set up your bio-research environment and explore available tool (file: r4/start/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end bra (file: r0/brandkit/SKILL.md)
- cli-anything: Use when the user wants Codex to build, refine, test, validate, or (file: r0/cli-anything/SKILL.md)
- cli-hub-meta-skill: Discover agent-native CLIs for professional software. Access the l (file: r0/cli-hub-meta-skill/SKILL.md)
- code-review: Review the changes since a fixed point (commit, branch, tag, or  (file: r0/code-review/SKILL.md)
- codebase-design: Shared vocabulary for designing deep modules. Use when the user  (file: r0/codebase-design/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准备最小可 (file: r0/contributor/SKILL.md)
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
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for web (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects depending on (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-driven  (file: r0/taste-skill-v2-experimental/SKILL.md)
- diagnosing-bugs: Diagnosis loop for hard bugs and performance regressions. Use wh (file: r0/diagnosing-bugs/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Google Do (file: r21/documents/26.1111.10930/skills/documents/SKILL.md)
- domain-modeling: Build and sharpen a project's domain model. Use when discussing  (file: r0/domain-modeling/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable Draw. (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable dra (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it to o (file: r1/ego-browser/SKILL.md)
- enterprise-search:digest: Generate a daily or weekly digest of activity across all connect (file: r8/digest/SKILL.md)
- enterprise-search:knowledge-synthesis: Combines search results from multiple sources into coherent, dedup (file: r8/knowledge-synthesis/SKILL.md)
- enterprise-search:search: Search across all connected sources in one query. Trigger with " (file: r8/search/SKILL.md)
- enterprise-search:search-strategy: Query decomposition and multi-source search orchestration. Breaks  (file: r8/search-strategy/SKILL.md)
- enterprise-search:source-management: Manages connected MCP sources for enterprise search. Detects avail (file: r8/source-management/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用户运行 /ev (file: r0/evidence-recap/SKILL.md)
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
- heygen:automated-content-creator: Plan, produce, and keep improving a recurring video series for Y (file: r16/automated-content-creator/SKILL.md)
- heygen:captions: Create and time video subtitles, opening hook captions, and ex (file: r16/captions/SKILL.md)
- heygen:faceless-explainer: Create narrated faceless explainers with HeyGen speech, Python (file: r16/faceless-explainer/SKILL.md)
- heygen:general-video: Catch-all for video requests only when no specialized HeyGen vid (file: r16/general-video/SKILL.md)
- heygen:motion-graphics: Design and render focused video motion graphics in Python, inclu (file: r16/motion-graphics/SKILL.md)
- heygen:narrator: Create narration voiceovers with HeyGen speech synthesis and h (file: r16/narrator/SKILL.md)
- heygen:picture-video: Create narrated picture-story videos with OpenAI native images,  (file: r16/picture-video/SKILL.md)
- heygen:script-writer: Write and revise spoken video scripts for UGC, explainers, talki (file: r16/script-writer/SKILL.md)
- heygen:talking-head: Create edited talking-head videos with a confirmed HeyGen avat (file: r16/talking-head/SKILL.md)
- heygen:ugc-product: Create faceless, narrated product UGC videos, 30 seconds by defa (file: r16/ugc-product/SKILL.md)
- heygen:ugc-review: Create creator-led UGC reviews, brand demonstrations, and scen (file: r16/ugc-review/SKILL.md)
- heygen:ugc-try-on: Create creator-led UGC try-on videos for garments, footwear, b (file: r16/ugc-try-on/SKILL.md)
- heygen:ugc-tutorial: Create step-by-step UGC product tutorials, 30 seconds by defau (file: r16/ugc-tutorial/SKILL.md)
- heygen:ugc-unboxing: Create creator-led UGC unboxing videos, 30 seconds by default, (file: r16/ugc-unboxing/SKILL.md)
- heygen:ugc-voiceless: Create short product ads driven by mood, tactile sound, and visu (file: r16/ugc-voiceless/SKILL.md)
- heygen:ugc-website: Create creator-led UGC website or SaaS videos, 30 seconds by def (file: r16/ugc-website/SKILL.md)
- heygen:video-editing: Edit and finish videos in Python with scene assembly, layered me (file: r16/video-editing/SKILL.md)
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
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visu (file: r21/pdf/26.1111.10930/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions (file: r17/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the  (file: r23/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks (file: r23/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as (file: r23/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the  (file: r23/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One- (file: r23/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, do (file: r23/ponytail-review/SKILL.md)
- pr: Use when writing a PR body. (file: r0/pr/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five di (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use fo (file: r21/presentations/26.1111.10930/skills/presentations/SKILL.md)
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
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized rever (file: r24/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
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
- sepia:sepia: Make AI-generated writing read as human-written, in fiction and i (file: r25/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Hemingway  (file: r25/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full r (file: r25/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal  (file: r25/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose pr (file: r25/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new pro (file: r25/sepia-write/SKILL.md)
- shadcn: Manages shadcn components and projects — adding, searching, fixi (file: r0/shadcn/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (including (file: r18/sites/SKILL.md)
- sites:sites-remix: Remix a Site built with the Sites plugin into a new Site. Use whe (file: r18/sites-remix/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, visuali (file: r22/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the C (file: r22/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r19/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, (file: r26/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner  (file: r19/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner  (file: r26/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r19/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on with (file: r26/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r19/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current sessio (file: r26/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need (file: r19/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need (file: r26/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing su (file: r19/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing su (file: r26/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before (file: r19/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before (file: r26/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks  (file: r19/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks  (file: r26/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavi (file: r19/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavi (file: r26/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing imp (file: r19/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing imp (file: r26/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from curren (file: r19/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from curren (file: r26/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find an (file: r19/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find an (file: r26/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, befo (file: r19/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, befo (file: r26/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, (file: r19/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, (file: r26/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifyi (file: r19/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifyi (file: r26/writing-skills/SKILL.md)
- tdd: Test-driven development. Use when the user wants to build featur (file: r0/tdd/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz your (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a thi (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template s (file: r21/template-creator/26.1111.10930/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Codin (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conversat (file: r17/visualize/1.0.89/skills/visualize/SKILL.md)
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

## developer · 2026-11-12T01:27:25Z

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

## developer · 2026-11-12T01:27:25Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-11-12T01:27:25Z

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

## developer · 2026-11-12T01:27:25Z

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


## developer · 2026-11-12T01:27:25Z

<tools>
Added deferred tool namespaces:
- mcp__bigquery
- mcp__biorxiv: An MCP server for accessing bioRxiv and medRxiv preprint servers.
- mcp__c_trials: An MCP server for accessing ClinicalTrials.gov API v2.
- mcp__chembl: An MCP server for accessing the EMBL-EBI ChEMBL Database v34.
- mcp__mobile_mcp: Drive a real or simulated iOS/Android device.
- mcp__ot
- mcp__pubmed
</tools>

## tool · 2026-11-12T01:27:31Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"af44f4","wall_time_seconds":0.000008125,"exit_code":0,"original_token_count":41207,"output":"Warning: truncated output (original token count: 41207)\nTotal output lines: 1990\n\n/Volumes/SamsungSSD990PRO/GitHub/codex-question-bank\n.question-bank-work/older-forty-zhang-6.md\n.question-bank-work/older-forty-lilin-1.md\n.question-bank-work/302-zhang-1-unique-3.md\n.question-bank-work/302-zhang-1-volume-7.md\n.question-bank-work/302-lilin-volume-2.md\n.question-bank-work/render-302-older.py\n.question-bank-work/notation-after/27302阶段模拟卷（第二至五卷及补充练习）.log\n.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX横屏版）.log\n.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX常规版）.pdf\n.question-bank-work/notation-after/302数学二分节真题集.log\n.question-bank-work/notation-after/27302阶段模拟卷.log\n.question-bank-work/notation-after/302数学二分节真题集.pdf\n.question-bank-work/notation-after/27302阶段模拟卷.pdf\n.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX横屏版）.pdf\n.question-bank-work/notation-after/27302阶段模拟卷（第二至五卷及补充练习）.pdf\n.question-bank-work/notation-after/302数学二分节真题集（原生LaTeX常规版）.log\n.question-bank-work/302-older-twenty-comparison.txt\n.question-bank-work/apply-302-hefei.py\n.question-bank-work/older-forty-lilin-5.md\n.question-bank-work/render-proof-302-doing-books.py\n.question-bank-work/clean-302-questions.py\n.question-bank-work/render-proof-302-official.py\n.question-bank-work/older-lilin-2-v1.md\n.question-bank-work/302-zhang-1-volume-1.md\n.question-bank-work/302-zhang-1-unique-5.md\n.question-bank-work/302-convert.jsonl\n.question-bank-work/302-lilin-volume-4.md\n.question-bank-work/302-primary-current.json\n.question-bank-work/render-302-zhang-printed.py\n.question-bank-work/proof-302-ocr.py\n.question-bank-work/302-zhang-editions-check.txt\n.question-bank-work/older-forty-zhang-4.md\n.question-bank-work/302-wu-basic-all.md\n.question-bank-work/302-ten-two-v2.md\n.question-bank-work/render-302-zhang-a4-outliers.py\n.question-bank-work/older-forty-lilin-3.md\n.question-bank-work/302-hefei-2.md\n.question-bank-work/302-zhang-1-unique-1.md\n.question-bank-work/302-zhang-1-volume-5.md\n.question-bank-work/apply-302-older-twenty.py\n.question-bank-work/older-forty-zhang-5.md\n.question-bank-work/302-ten-two-v3.md\n.question-bank-work/302-vlm-batch.jsonl\n.question-bank-work/older-forty-lilin-2.md\n.question-bank-work/302-first.txt\n.question-bank-work/older-forty-candidates.py\n.question-bank-work/302-zhang-1-volume-4.md\n.question-bank-work/render-302-zhang-year-differences.py\n.question-bank-work/302-lilin-volume-1.md\n.question-bank-work/302-zhang-horizontal-check.txt\n.question-bank-work/older-forty-lilin-6.md\n.question-bank-work/remove-302-standalone-math3.py\n.question-bank-work/older-forty-zhang-1.md\n.question-bank-work/302-zhang-1-unique-4.md\n.question-bank-work/assemble-302-wu-basic.py\n.question-bank-work/302-wu-basic-2.md\n.question-bank-work/ocr-302\n.question-bank-work/convert-302.py\n.question-bank-work/302-liyanfang-volume-2.md\n.question-bank-work/apply-302-verified-paper.py\n.question-bank-work/compare-302-older-twenty.py\n.question-bank-work/302-wu-july.md\n.question-bank-work/302-clean-run.txt\n.question-bank-work/302-ten-two-v6.md\n.question-bank-work/302-batch-pilot.json\n.question-bank-work/302-vlm-pilot.jsonl\n.question-bank-work/ocr-302-spreads.py\n.question-bank-work/assemble-302-zhang-1.py\n.question-bank-work/302-hefei-1-variants.md\n.question-bank-work/older-lilin-1-v4.md\n.question-bank-work/older-lilin-crop.py\n.question-bank-work/batch-proof-302.py\n.question-bank-work/302-zhang-2-volume-4.md\n.question-bank-work/302-zhang-2-volume-6.md\n.question-bank-work/302-clean-preview.txt\n.question-bank-work/302-wu-basic-1.md\n.question-bank-work/filter-302-zhang-math3.py\n.question-bank-work/302-older-10-1-volume-1.md\n.question-bank-work/ocr-302.swift\n.question-bank-work/302-lilin-volume-5.md\n.question-bank-work/older-lilin-1-v1.md\n.question-bank-work/302-lilin-spread-diff.txt\n.question-bank-work/302-zhang-2-volume-1.md\n.question-bank-work/302-clean-finalize.txt\n.question-bank-work/302-wu-basic-1-variants.md\n.question-bank-work/302-spreads.json\n.question-bank-work/older-lilin-1-v3.md\n.question-bank-work/render-proof-302-variants.py\n.question-bank-work/302-zhang-2-volume-3.md\n.question-bank-work/render-302-zhang-horizontal-check.py\n.question-bank-work/302-ten-two-v1.md\n.question-bank-work/older-forty-zhang-7.md\n.question-bank-work/302-zhang-1-unique-2.md\n.question-bank-work/302-zhang-1-volume-6.md\n.question-bank-work/assemble-302-older-10-one.py\n.question-bank-work/302-lilin-volume-3.md\n.question-bank-work/compare-302-zhang-shared.py\n.question-bank-work/render-proof-302-lilin-a4.py\n.question-bank-work/302-zhang-shared.txt\n.question-bank-work/inspect-302-questions.py\n.question-bank-work/302-older-10-1-volume-2.md\n.question-bank-work/302-ten-two-v5.md\n.question-bank-work/302-zhang-1-volume-2.md\n.question-bank-work/302-common.txt\n.question-bank-work/notation-before/27302阶段模拟卷.log\n.question-bank-work/notation-before/27302阶段模拟卷.pdf\n.question-bank-work/302-edition-check.txt\n.question-bank-work/older-forty-lilin-4.md\n.question-bank-work/render-proof-302-zhang.py\n.question-bank-work/older-forty-zhang-3.md\n.question-bank-work/verify-302-lilin-spread.py\n.question-bank-work/302-zhang-1-unique-7.md\n.question-bank-work/render-proof-302-remaining-lilin.py\n.question-bank-work/302-wu-august.md\n.question-bank-work/302-lilin-volume-6.md\n.question-bank-work/302-zhang-2-volume-8.md\n.question-bank-work/302-zhang-printed-check.txt\n.question-bank-work/302-ocr-model/preprocessor_config.json\n.question-bank-work/302-ocr-model/model.safetensors.index.json\n.question-bank-work/302-ocr-model/configuration_paddleocr_vl.py\n.question-bank-work/302-ocr-model/chat_template.jinja\n.question-bank-work/302-ocr-model/README.md\n.question-bank-work/302-ocr-model/generation_config.json\n.question-bank-work/302-ocr-model/processor_config.json\n.question-bank-work/302-ocr-model/tokenizer.json\n.question-bank-work/302-ocr-model/processing_paddleocr_vl.py\n.question-bank-work/302-ocr-model/config.json\n.question-bank-work/302-ocr-model/special_tokens_map.json\n.question-bank-work/302-ocr-model/tokenizer_config.json\n.question-bank-work/302-ocr-model/added_tokens.json\n.question-bank-work/302-ocr-model/image_processing_paddleocr_vl.py\n.question-bank-work/302-ocr-model/modeling_paddleocr_vl.py\n.question-bank-work/302-ocr-model/model.safetensors\n.question-bank-work/302-zhang-1-unique-6.md\n.question-bank-work/compare-302-zhang-a4.py\n.question-bank-work/302-zhang-1-volume-3.md\n.question-bank-work/verify-302-zhang-editions.py\n.question-bank-work/older-forty-zhang-2.md\n.question-bank-work/render-proof-302.py\n.question-bank-work/302-ten-two-v4.md\n.question-bank-work/302-ocr-cache/25/b81d7dded92cad8a847230efdf15e4da1bd9c32cef341f949e11e0a7a7c2ee\n.question-bank-work/302-ocr-cache/25/6b143b2b543e18d5ec724739c04b1d3932cda207218141a86f9edf4aac3d69\n.question-bank-work/302-zhang-2-volume-7.md\n.question-bank-work/302-wu-basic-3-variants.md\n.question-bank-work/302-vlm-older.jsonl\n.question-bank-work/302-older-10-1-volume-3.md\n.question-bank-work/302-zhang-1-unique-8.md\n.question-bank-work/verify-302-zhang-printed.py\n.question-bank-work/302-ocr-cache/22/e8daa084c96650e6f656f1e1cf5ffdaaa77c780c9d81452eb8cdce1ac3a336\n.question-bank-work/302-ocr-cache/22/e43049590ceddc6e3ca5928e4d89728f9e1e7d8180e0c6667729f7ded11e66\n.question-bank-work/302-ocr-cache/22/613d2d127a9c1c415e56b7eb3390a104206ec4558c473c609788ba732549b1\n.question-bank-work/302-ocr-cache/8e/b803bc300c6fefedc19d0541516c65c71776bb4c665d1458ac13ccccec6963\n.question-bank-work/302-ocr-cache/8e/e96632e6f18240b0987c3a99f0c7c8873ae717e5c38036192276cbba5c60fd\n.question-bank-work/302-ocr-cache/14/7bb84f454413e9b2f2bfff90d7e6545b1fa4c3da0028c329a6442b01341195\n.question-bank-work/302-ocr-cache/14/b146a387a4511ad65ea40f251df3acb24bc4ba41a5bbabb483fb3b46f9fb3f\n.question-bank-work/302-ocr-cache/14/5821f2888953970112ba96c94266729abf2dc74033366acf6f8d471661b9b8\n.question-bank-work/302-ocr-cache/14/ac210eac33f0fe338044012729ce7fd54575e1b94e77728e0d95cf7bbd20c1\n.question-bank-work/302-ocr-cache/14/357b0c87d63c023afdfcb448357e1e59b1ad4cc8a5aa2d8a15450dd9acd88f\n.question-bank-work/302-ocr-cache/7a/c5a75d96a651e42aedbc0658df7eadadca115c7b7f8c15a1861763a871105f\n.question-bank-work/302-ocr-cache/7a/730b42b66c85f1ce25ed5fcb871bd423f85d1d1ea866f11ed0d7496c95aa37\n.question-bank-work/302-ocr-cache/7a/b242d190218c6e1352bd456b03f196e3f410209abccfa51ee3307c9686f525\n.question-bank-work/302-ocr-cache/7a/943f33bd3095fd8576c421056427ba27a1fa23332c2b8ff3ba32157325b558\n.question-bank-work/302-ocr-cache/7a/90d9898cfdae2775e9afd917175575156910941b3e7e4a61a0740bdca5dd70\n.question-bank-work/302-ocr-cache/7a/0fced2c40299460e4715227a70b51e923734db760705b4d4ec7ef07794ce7d\n.question-bank-work/verify-302.py\n.question-bank-work/302-ocr-cache/57/2218b45a9cd6e0bd7815d1663ce38eada512ca991719b29475f82405621588\n.question-bank-work/302-ocr-cache/57/b9a5c9c8fb68834f41252d55274882b31ad1c3a7dd77d8f69303a66b972beb\n.question-bank-work/302-ocr-cache/57/016f9f98ca371c604b13cc922d223df30ad639ed1da1df880d5acc46f95ef3\n.question-bank-work/302-ocr-cache/57/7b5a261181116c2451e31141391df82161d83db187a2b72fab6ab9e3643957\n.question-bank-work/302-ocr-cache/57/31144e7c7d44137a3bef74fbb43f06ddfc195b2e3a4f172fd0af627fbd4a45\n.question-bank-work/302-ocr-cache/57/73611f5e58a2ae51936dbeca125a35f881c3f1cbafd2b950b7e274e5ab3811\n.question-bank-work/302-ocr-cache/57/62e968067c7221b81c9cbf1b57c3149863b33a7fef30d36aa5a15b2a2bf3a7\n.question-bank-work/302-ocr-cache/57/9edeef94563ff69f84408df2077305f5a80e3ddbdcd87b5bd3bb9c461559e0\n.question-bank-work/302-ocr-cache/57/766b958ba3d622bf769ccf3911a9e8baa0af64d86767e3285cc4d9b80ce736\n.question-bank-work/302-ocr-cache/7f/fd142906d62f2cb10d869625afef4335ae79c76e7b95c7800bc5a36c666d11\n.question-bank-work/302-ocr-cache/7f/ba68d774d0076f4b50ef7d1b51852db93fe20d14bf85ff06f9e287c0fe905a\n.question-bank-work/302-ocr-cache/7f/a78a69318ba4a3f746c131b2c4774e51bb01402ec38b26db8b2bc20619827e\n.question-bank-work/302-ocr-cache/7f/6eb21fc51ed7f24e44b066e9516801bc49bc04eaa062128b08d3d6396c79f7\n.question-bank-work/302-ocr-cache/7f/ba5f7aa27c54252a9d303d012fd7a4eab5ecd7965f71747a24845a6af867e7\n.question-bank-work/302-ocr-cache/0b/c78e2e31db1820091cbf761b38badd9214151058d7e22ed107a7bc603746fa\n.question-bank-work/302-ocr-cache/0b/fdd5902f067d386576d70392b26d84b2d8eeff079e8a1b7edd6a1a28f4c6a6\n.question-bank-work/302-ocr-cache/0b/aac87d15a0f3d35f7387db6932826834c034e4bacfd48480fa34f9df269752\n.question-bank-work/302-ocr-cache/68/ae372449786eee3e0fabfeb9da68f464332fe8d29e2cbc728785c6880a02a2\n.question-bank-work/302-ocr-cache/68/29fd89e3bdec827590cb73c858c9ce67a5fbf11298c40ad7cc5fd58ecb11fc\n.question-bank-work/302-ocr-cache/50/5827c2036d729fcdfcdf4173170f47098014a887ff34dab42534ec8e02b961\n.question-bank-work/302-ocr-cache/50/a817a0f2177d5d4718abad7fac1dcaf8813997aaa17b1a2e27332553aebb59\n.question-bank-work/302-ocr-cache/50/3971d4688c228ef486af5c46f1add74076e0d4330914215b83edea4df2246d\n.question-bank-work/302-ocr-cache/50/367e3056221c9bdc176014d28b65e9cbe7ca9430104a1b4492a29642226988\n.question-bank-work/302-proof-source/张宇数一原版卷4-整1.png\n.question-bank-work/302-proof-source/李艳芳横版卷3-1.png\n.question-bank-work/302-proof-source/李林六套卷-卷5-13-17.png\n.question-bank-work/302-proof-source/二十套A4数一-10.png\n.question-bank-work/302-proof-source/李林复核-原版-20.png\n.question-bank-work/302-proof-source/老李林数1-细节-22.png\n.question-bank-work/302-proof-source/张宇按年份数一-8-4.png\n.question-bank-work/302-proof-source/李艳芳横版卷1-3.png\n.question-bank-work/302-proof-source/老李林数一-9.png\n.question-bank-work/302-proof-source/李林A4卷6-1.png\n.question-bank-work/302-proof-source/李林六套卷-卷6-7-12.png\n.question-bank-work/302-proof-source/老李林数1-细节-9.png\n.question-bank-work/302-proof-source/李艳芳A3卷1-1.png\n.question-bank-work/302-proof-source/张宇…35207 tokens truncated…9d8032a0a73f0aff9174c95\n.question-bank-work/302-ocr-cache/63/6fb98058712e5d457817cbbdacc9dd61ac4fcd5e2f1a2b65199aa9e50018c2\n.question-bank-work/302-ocr-cache/63/89c9325bcea56159dd6fb7dd9fea357439215f59861b6f673fed1a08d5e59b\n.question-bank-work/302-ocr-cache/63/3f7e2718065412814097a29fccf5be553cd8ef16d1754819871dfa041590ef\n.question-bank-work/302-ocr-cache/63/b749119745e10a742a29a5aa35ae2efa329777b773d61148802f60137a5bb1\n.question-bank-work/302-ocr-cache/97/cf3d0529478c5c3d5ade534dfb5f3f5ff091fc46996feb8897634744a49f9d\n.question-bank-work/302-ocr-cache/97/0ba941dc257ace665defd728fd95fe0b13337f6366dc2fe463b727993c09db\n.question-bank-work/302-ocr-cache/97/892d23941c460d23ad48a22e44a253ef5485e0e026da12689bd94090629484\n.question-bank-work/302-ocr-cache/97/09598c524ef5e341b8dd113d060f212fde2086479d9f5695e109aa0b1c959d\n.question-bank-work/302-ocr-cache/97/716a187e1f2bb4cc1629612a8187881163ed54139fdff52115fc65a2bb8674\n.question-bank-work/302-ocr-cache/55/1c5b48ae2cfaaa350c28587ba162ce9166c240806eefc876da246254762886\n.question-bank-work/302-ocr-cache/55/7868b5f6373c17725a3b8e442e7a9480fc7dd908a645cb53c4631983b5ae86\n.question-bank-work/302-ocr-cache/55/a1825dac957762d91ce29d45086d94f051dc2c22a2641327ef8d0bcdb27704\n.question-bank-work/302-ocr-cache/55/a677b4e9a7f59574e750fc6dcb62f95eabd3d7b34befd8d9c04284e0265843\n.question-bank-work/302-ocr-cache/55/a45ead06f315638748b1894cc86c51f16f7a1d9cccb77a402503efbd4900ac\n.question-bank-work/302-ocr-cache/52/b28c90e8ba831fc2927b68cde18b073ec621e2ed27dc960795b9bd828e7a4e\n.question-bank-work/302-ocr-cache/52/5e5bea98726da7d3e63a4489b246308d3b85f994918af9bb9d7b6b92f68b81\n.question-bank-work/302-ocr-cache/52/12ee7bf72eead2eef78c71eb37868579472c4cf6d6702fafb8052493855a43\n.question-bank-work/302-ocr-cache/52/541b66155054a36f3351611884d4784f3a0f37a6cdccac7f662d1b5e85cc77\n.question-bank-work/302-ocr-cache/52/0dcf984e8362fff3ac1bd6bf66f5c35eb1227aa49836269e92436e195c319d\n.question-bank-work/302-ocr-cache/52/ff133ad3a2aa4b58de0f170819e4c3d5a80b15031a389fb3188eb080477213\n.question-bank-work/302-ocr-cache/99/3dd8bfdf8011e828aef7c39940528528961e6b7e122af43432b0ff2b33fb0a\n.question-bank-work/302-ocr-cache/99/9736bac9e26bb4f97a860284b5dd5f23fccdf86f4b8ffe77cbf04068b8849d\n.question-bank-work/302-ocr-cache/99/deddc47dc31a3d87b300d78f859b95e38c073097a650456a5c84e147321897\n.question-bank-work/302-ocr-cache/99/0226097506a40aa0ce609d985a34367083c46bcd6cb24e53db509b46aa9335\n.question-bank-work/302-ocr-cache/39/2b2fbcddff973cbe1d7f131b12523618bc362e9b0b6fd5b8cf2b9548541b09\n.question-bank-work/302-ocr-cache/39/05ea0b36f8bd178ec28d37def83362ae4d90cfca2fa9fd9edccf0d44ef5fc0\n.question-bank-work/302-ocr-cache/39/81a80142780b13870410f4f36cb6e975b1979f6d9c702f01681f0b7df288b5\n.question-bank-work/302-ocr-cache/39/4ee01f18059d7daa4884eea21fcdcb2efc303dbecf49219fde8b079262955f\n.question-bank-work/uv/archive-v0/5wEwp_Q6ut6wzteA/datasets/packaged_modules/meshfolder/__init__.py\n.question-bank-work/uv/archive-v0/5wEwp_Q6ut6wzteA/datasets/packaged_modules/meshfolder/meshfolder.py\n.question-bank-work/302-ocr-cache/6c/1b9abfbd446ead4631d178d142b7c955007b544936f6ec3fb59d3a71f4793b\n.question-bank-work/302-ocr-cache/6c/a1e4359087f46e37d6c0aa7a9359fad3ce3cd477f5069fb54d7a6f46f3992b\n.question-bank-work/302-ocr-cache/6c/f8430b424f1f6795f77a79c2978e674a4bffe92e9dca40c8bdff4842f23295\n.question-bank-work/302-ocr-cache/b1/e6edf4a3ac5f8770b4866fef6514c8a6a69409fda14adfb4141f57d40cc49e\n.question-bank-work/302-ocr-cache/b1/735be13b9fada0d4c2b6a16195bc1049290ad399fc9cb84057c422eac90aa0\n.question-bank-work/302-ocr-cache/b1/4c468c8f17e292b4556227eb06dee9b5a3708e88b04117323cd9de02a846d7\n.question-bank-work/302-ocr-cache/06/c5905a29182aa8f1d8c7a8fd880c7faa230e66cbb338f88d27db4e63f04e46\n.question-bank-work/302-ocr-cache/06/9294d456577c567f77d651f06ffaa73802c86f24f41401333dda65d2db37eb\n.question-bank-work/302-ocr-cache/06/ea6142d91e37663dafbdcf446075042b547cb3e54a28d6ba2d00d308f9ed0e\n.question-bank-work/302-ocr-cache/06/321637b018c1833be4922873d76368a381f1d1d8601b5c0726687cdb4c6250\n.question-bank-work/302-ocr-cache/06/c4873aedecd7b2bd66eeb84628d041f3437f5e5c402ee5be3d116163d8e399\n.question-bank-work/302-ocr-cache/06/1098f02c9ca5220f77331688ee58a0a49af21475083bd865fd226c280cf216\n.question-bank-work/302-ocr-cache/06/4e5e01ab48a2d91ffcd493963d7917f8cba88a41423a78ebe7405b504a7005\n.question-bank-work/302-ocr-cache/01/132b995db6e3e33a7b6ff7a49ce9e1e61f181c3b7e1725958b428cb382f5b9\n.question-bank-work/302-ocr-cache/6d/3164e014b5abc1cf70d0a3f47d1ca6a955888335a3bee1764f83fceb0a2adf\n.question-bank-work/302-ocr-cache/6d/32d843f7a310eb4e9c19e1199dd5e50018150a256dd32200eb0df296ba59ce\n.question-bank-work/302-ocr-cache/64/fcc554aea58a017e7179b393f9aeac54cf1046e37fdf4d6c188d97ded3469c\n.question-bank-work/302-ocr-cache/64/1613614ea4c4634fa703dbb64fd5646e6e6c965066f3ac5820510bee6bd492\n.question-bank-work/302-ocr-cache/64/f2c5aa50ff9d01864c4298e8f5055a003ce3fc776a67459f513f3ffb9509fa\n.question-bank-work/302-ocr-cache/b8/85efd59d85903e6a355e6c394b7b3d0f9f42b036fd1217a0df8afb916eeb71\n.question-bank-work/302-ocr-cache/b8/b7989346482c7b0a57e52be099f375ab9416c79ca72a32bc878aaabec2e440\n.question-bank-work/302-ocr-cache/b8/8325a169bbf86fdf91dffefefc812f99a821013ba34156e3b47b757234a360\n.question-bank-work/302-ocr-cache/b8/70e2b012c6d4d7b8c2d2094f91c1d2f66563115d98057bd2092d56c1372977\n.question-bank-work/302-ocr-cache/b8/3bff742443bf2e101b2240dcd7747042882b9586f69e67ad782806cab45347\n.question-bank-work/302-ocr-cache/b8/143717cf77bcb385bb697e9894b720a990b43f5849b7d1b7973789ce5bf041\n.question-bank-work/302-ocr-cache/b8/80ac95dae9cb1bac34b90846929423f2846f60f276ca46c9f48f04f35dd8f8\n.question-bank-work/302-ocr-cache/bf/fa5fd4c53574e4839258cb392edfc9befc83f8c9d648fbf77c9cc8aa6ffe29\n.question-bank-work/302-ocr-cache/0a/b5bb3eaef7ba29a82d926e0519984bcb4afe1b542ab4fe83782422e0fc6db8\n.question-bank-work/302-ocr-cache/bf/67376a5d5b633ff36d3ff99d6ed4e54c6f56d64471807bd5045a0a2924355b\n.question-bank-work/302-ocr-cache/0a/b044255f52d566b3dd40ea7b70351e188cc83669b9db75369a120dcaf66080\n.question-bank-work/302-ocr-cache/bf/17a512e146e0e2154df40f30d415bbee1c1be438ddfc7badfb694d353134d6\n.question-bank-work/302-ocr-cache/0a/b67d86bbe14f7b561a5320aa7b07c559478a4cd172af766c88033f70aa1bfd\n.question-bank-work/302-ocr-cache/bf/8f35908166ff2d2dd7faf00171885d4ece3cbbac4b8845da2d843fa23a8ca3\n.question-bank-work/302-ocr-cache/0a/af5fe9bb9a5cb2155b68ef0ec0526b47fca4f2b7b456eef9d23cdaf4527047\n.question-bank-work/302-ocr-cache/a7/39f9abc242af2efefab3d435122d4ac7f127b3c053cc7617e5e34c78410a8f\n.question-bank-work/302-ocr-cache/a7/733f13c8f0d7c127b15ea7c0ea77121f798585edc56464bc4d982699bcda12\n.question-bank-work/302-ocr-cache/a7/63a1c4eaa0416b98b6348f12327d23f19ad9f6eea72bfd059e0e73f71e565b\n.question-bank-work/302-ocr-cache/a0/ac3e48c4a353f0c961f8e9e714efa2e21da16e133eb93c2961790b7f074a44\n.question-bank-work/302-ocr-cache/a0/d0b23a8a2f7e8625c8a1f1b6e45874dcdad4ac66d1ea37fe700c2426417bad\n.question-bank-work/302-ocr-cache/a0/b0a792db1c710a8b57a8867cc101e9097cb28f9dbb50173d055023bd004aa1\n.question-bank-work/302-ocr-cache/a0/4c79d0a99bbab3c234c87a4e06bdf5898459d6fc3e26d8175fc06f18308b85\n.question-bank-work/302-ocr-cache/a0/b959d2fcb82f11066244099b7c5a27a28db64c88106d5155884da0087b8e02\n.question-bank-work/uv/archive-v0/5wEwp_Q6ut6wzteA/datasets/packaged_modules/folder_based_builder/folder_based_builder.py\n.question-bank-work/uv/archive-v0/5wEwp_Q6ut6wzteA/datasets/packaged_modules/folder_based_builder/__init__.py\n.question-bank-work/302-ocr-cache/ba/1f99a7575578ca0b875012f362c5d5879f8dc98a8686214d31f5ee465f3720\n.question-bank-work/302-ocr-cache/ba/21bd43d24eb1f815648a04a263ee2d1b63ed408c0b7a55dd4bdacd14e3b4a5\n.question-bank-work/302-ocr-cache/ba/24f6f103c3f771976080bd81ebc1fcd8885095dcbc4f020e177c1eca8e98f2\n.question-bank-work/302-ocr-cache/ba/aaabc48637f7efbfc30d5dc28e4aff913a5bad0ff042ca4b75de10e87a3deb\n.question-bank-work/302-ocr-cache/ba/0122adfbf668ba1dfffd57b09ff2a107b8277d2eba5927a45750207304cf3f\n.question-bank-work/302-ocr-cache/ba/d928f6addc070aaf7a7f31adb25f1789a12bd1d6abfaefb8b8c6630b0e1f6a\n.question-bank-work/302-ocr-cache/d4/773818cddcfa553d30c335f51e5c07865506360f27adf10f657baecaeffc52\n.question-bank-work/302-ocr-cache/d4/ea45a84b9a92169469e042130a0522d75bbe30fad452f1f460f846870ac529\n.question-bank-work/302-ocr-cache/d4/43a0880a99ed6bf63dc7375cdba1b63c9ef3677cde3af20660ff9a05dc81b2\n.question-bank-work/302-ocr-cache/d4/47067a738780e87c916efaf871497ec5e3c9271c0269610a9d62be509d1f19\n.question-bank-work/302-ocr-cache/d4/9f124c2fae9d56b50c8829f73994459e07cfe56d7946ff4131f783041e6b69\n.question-bank-work/302-ocr-cache/d4/f66565b798a9b09a431e414129b978f501486f1279a6112a54793875c62966\n.question-bank-work/302-ocr-cache/d4/9e86c48eb63a3f2f927eff927977a2077cc693ad6e705e1bcc0d3c6fcf9723\n.question-bank-work/302-ocr-cache/90/0932e24e5dec968ee86e0b43577ab1730eb8318306a005306c8edd67570dcb\n.question-bank-work/302-ocr-cache/90/fa019542a7acd6441035b2626e998580886a1cbd6431ceb4dfde04a8012f56\n.question-bank-work/302-ocr-cache/90/d67b10acf5e20e73299d56fec1d905cd91151a6b9885372b884c5c43f600da\n.question-bank-work/302-ocr-cache/90/bd70acdc79512f2a8d0e7a37e8dc4912f558a5aa55628e172938be21b21c6a\n.question-bank-work/302-ocr-cache/90/1251b6700f53d3a60494a5c03bc419393db02b7f73ec67d2b7087edd3636ad\n.question-bank-work/302-ocr-cache/90/052cff0609e97628e0f2e9e6201eb03f78466507a0fd0c61d2b25647f7528e\n.question-bank-work/302-ocr-cache/90/4863e8cf6d632c2f6bc04c056239212a30cbfb12984294dfaf7b0a1e681694\n.question-bank-work/302-ocr-cache/90/bbc9f5af78f376d2b4c9390bd62a1293dfeb58d2fa5b22743a42aa41c19011\n.question-bank-work/test-302-batch-ocr.py\n.question-bank-work/302-wu-basic-3.md\n.question-bank-work/render-proof-302-wu.py\n.question-bank-work/older-lilin-1-v2.md\n.question-bank-work/verify-302-zhang-horizontal.py\n.question-bank-work/older-forty-zhang-8.md\n.question-bank-work/302-zhang-2-volume-2.md\n.question-bank-work/verify-302-math.cjs\n.question-bank-work/302-liyanfang-volume-1.md\n.question-bank-work/302-zhang-1-volume-8.md\n.question-bank-work/302-zhang-topic-figures.md\n.question-bank-work/302-primary-older.json\n.question-bank-work/302-older-10-1-unique-3.md\n.question-bank-work/proof-venv/lib/python3.12/site-packages/huggingface_hub/__pycache__/_local_folder.cpython-312.pyc\n.question-bank-work/proof-venv/lib/python3.12/site-packages/huggingface_hub/_local_folder.py\n.question-bank-work/uv/archive-v0/Tw71Z78tS8xpoToU/huggingface_hub/_local_folder.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/audiofolder/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/audiofolder/audiofolder.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/meshfolder/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/meshfolder/meshfolder.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/videofolder/videofolder.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/videofolder/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/folder_based_builder/folder_based_builder.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/folder_based_builder/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/pdffolder/pdffolder.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/pdffolder/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/imagefolder/imagefolder.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/imagefolder/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/niftifolder/__init__.py\n.question-bank-work/proof-venv/lib/python3.12/site-packages/datasets/packaged_modules/niftifolder/niftifolder.py\n"}

## tool · 2026-11-12T01:27:36Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"2731de","wall_time_seconds":0.000009084,"exit_code":0,"original_token_count":3164,"output":"import argparse\nfrom pathlib import Path\n\nimport numpy as np\nfrom PIL import Image\nimport pymupdf\n\n\nparser = argparse.ArgumentParser()\nparser.add_argument('name')\nparser.add_argument('first', type=int)\nparser.add_argument('last', type=int)\nparser.add_argument('label')\nargs = parser.parse_args()\nroot = Path('references/302模拟27')\nwork = Path('.question-bank-work/302-proof-source')\nsource, = root.rglob(args.name)\nwith pymupdf.open(source) as pdf:\n    for page in pdf.pages(args.first - 1, args.last):\n        w, h = page.rect.width, page.rect.height\n        rect = pymupdf.Rect(w * .07, h * .028, w * .94, h * .945)\n        pix = page.get_pixmap(matrix=pymupdf.Matrix(1.85, 1.85), clip=rect, colorspace=pymupdf.csGRAY)\n        pixels = np.frombuffer(pix.samples, dtype=np.uint8).reshape(pix.height, pix.width)\n        valid = np.flatnonzero((pixels < 150).sum(axis=1) >= 4)\n        bands = np.split(valid, np.where(np.diff(valid) > 19)[0] + 1)\n        pieces = [Image.fromarray(pixels[max(0, v[0] - 3):v[-1] + 4]) for v in bands if len(v)]\n        assert pieces\n        merged = Image.new('L', (pix.width, sum(i.height + 7 for i in pieces)), 'white')\n        y = 0\n        for im in pieces:\n            merged.paste(im, (0, y))\n            y += im.height + 7\n        merged.save(work / f'{args.label}-{page.number + 1}.png')\nimport argparse\nfrom pathlib import Path\nimport re\n\n\nparser = argparse.ArgumentParser()\nparser.add_argument('paper', type=Path)\nparser.add_argument('subject', choices=['一', '二'])\nparser.add_argument('old_title')\nparser.add_argument('new_title')\nargs = parser.parse_args()\nroot = Path('references/302模拟27md')\npaper = args.paper.read_text(encoding='utf-8').strip()\nheading = paper.splitlines()[0]\nassert heading.startswith('## ')\nassert re.findall(r'(?m)^(\\d+)\\\\\\.', paper) == list(map(str, range(1, 23)))\npaper = paper.replace(heading, f'## {args.new_title}', 1)\npattern = re.compile(r'(?ms)^## ' + re.escape(args.old_title) + r'$.*?(?=^## |\\Z)')\nfor layout in ('A3', 'A4'):\n    path, = root.rglob(f'{layout}数{args.subject}模拟卷精选20套.pdf.md')\n    before = path.read_text(encoding='utf-8')\n    result, count = pattern.subn(lambda m: paper + '\\n\\n', before)\n    assert count == 1, (path, args.old_title)\n    path.write_text(result.rstrip() + '\\n', encoding='utf-8')\n    assert paper in path.read_text(encoding='utf-8')\n    print(path.name, args.new_title, 22)\nCOMPARE A3 一 1 22 [(11, 2, '', '1-'), (12, 5, '-1', '=n0'), (13, 3, 'n=0', ''), (15, 10, '', 'xx001其他μ≤<'), (16, 10, 'xxμ00≤<1其他', ''), (17, 17, '', '111=xxxxxx-e<>gln'), (18, 17, '111xxxxxx=<ln>ge-', ''), (20, 3, '', '111'), (21, 3, '111', '')]\nVOLUME A3 一 1  \nCOMPARE A3 一 2 22 [(1, 6, '1', '-23zy'), (2, 6, 'zxy2-3', ''), (4, 4, '', '2=1i'), (5, 6, '=2i', '110'), (6, 20, '11', '223iiii+b≠=则三条直线ax'), (7, 20, '1=a223biiii+≠0则三条直线x', ''), (15, 4, '', '为最小值'), (16, 7, '为最小值', 'nnk'), (17, 3, 'nnk', '')]\nVOLUME A3 一 2 x1 \nCOMPARE A3 一 3 22 [(2, 21, '', 'ffxx000001则yyy-αα==n是'), (3, 21, 'ffxxyyy00000==n-1αα则是', ''), (5, 3, '', '210'), (6, 3, '120', ''), (10, 1, '', 'π'), (11, 40, 'π', 'xxxx+++3==222222yyy其中zzz是'), (12, 37, 'u==zzzxxxxyyy222222++其中是由', ''), (13, 2, '1+', ''), (18, 1, '', 'y'), (19, 1, 'y', ''), (21, 21, '', '111222xxxxxyy0≤≤≤≤---'), (22, 21, '111222xxxxxyy0≤≤≤≤---', '')]\nVOLUME A3 一 3  \nCOMPARE A3 一 4 22 [(7, 6, '', '110pp-'), (8, 6, '110pp-', ''), (12, 8, '', '=xx00<<π'), (13, 8, 'πxx=<<00', ''), (20, 6, '', '11aaa-'), (21, 6, '11aaa-', '')]\nVOLUME A3 一 4  \nCOMPARE A3 一 5 22 [(1, 9, '+11nnn=22', ''), (3, 6, '', '==0nn1'), (4, 6, 'nn==01', ''), (5, 6, '', '000111'), (6, 6, '111000', ''), (10, 3, '', '10x'), (11, 14, 'x0', '=+2nnnn111--'), (12, 13, 'nnnn=1111--2+', ''), (13, 3, '', 'x2+'), (14, 3, 'x2+', '')]\nVOLUME A3 一 5 +11nnn=22 \nCOMPARE A3 一 6 22 [(1, 1, 'x', ''), (3, 3, '', '=n1'), (4, 3, '=n1', ''), (17, 2, '', '2d'), (18, 2, '2d', ''), (20, 4, '', '1=i3'), (21, 4, '1=i3', '')]\nVOLUME A3 一 6 x \nCOMPARE A3 一 7 22 [(1, 1, '2', ''), (5, 12, '', '00000002111a'), (6, 12, '21110000000a', ''), (8, 24, '', '若=P2111<<<<<00yaxx其他XYb8'), (9, 24, 'XYxxy=a00<<<<<111其他若P2b8', ''), (11, 7, '', 'tt=+x22'), (12, 7, '=xtt22+', '')]\nVOLUME A3 一 7 2 \nCOMPARE A3 一 8 22 [(1, 29, 'ttt0=ddxsinnnyy是关于的阶无穷小则', '+211-'), (2, 8, 'xx22+11-', ''), (4, 6, '', '-11235'), (5, 18, '5', '2223333111-bbbbbb'), (6, 22, 'bbbbbb33333111112222--', ''), (11, 3, '', '2=n'), (12, 3, 'n=2', ''), (19, 36, '', '111112222xxxx++===0dttttt'), (20, 36, '111112222gggttttttt-n++==', '')]\nVOLUME A3 一 8 ttt0=ddxxxsinnnyy2是关于的阶无穷小则 \nCOMPARE A4 一 1 22 [(11, 2, '', '1-'), (12, 5, '-1', '=n0'), (13, 3, 'n=0', ''), (15, 8, '', 'xx01≤θ其他'), (16, 8, 'xx0≤1θ其他', ''), (17, 17, '', '111=xxxxxx-e<>gln'), (18, 17, '111xxxxxx=<ln>ge-', ''), (20, 3, '', '111'), (21, 3, '111', '')]\nVOLUME A4 一 1  \nCOMPARE A4 一 2 22 [(1, 6, '1', '-23zy'), (2, 6, 'zxy2-3', ''), (4, 4, '', '2=1i'), (5, 6, '=2i', '110'), (6, 20, '11', '223iiii+b≠=则三条直线ax'), (7, 20, '1=a223biiii+≠0则三条直线x', ''), (16, 3, '', 'nnk'), (17, 3, 'nnk', '')]\nVOLUME A4 一 2 x1 \nCOMPARE A4 一 3 22 [(2, 21, '', 'ffxx000001则yyy-αα==n是'), (3, 21, 'ffxxyyy00000==n-1αα则是', ''), (5, 3, '', '210'), (6, 3, '120', ''), (7, 19, '一一线直的的过过原原点点条B不D个平面', ''), (8, 19, '', '的的B过过原原点点一一条直线D不个平面'), (10, 1, '', 'π'), (11, 38, 'π', 'xxxx+++3==222222yyy其中zzz是'), (12, 40, 'u===zzzxxxxyyy222222+++其中', ''), (13, 3, '', '11='), (18, 1, '', 'y'), (19, 1, 'y', ''), (21, 12, '', '1222xxxy--≤≤'), (22, 12, '1222xxxy≤≤--', '')]\nVOLUME A4 一 3  \nCOMPARE A4 一 4 22 [(1, 2, '1-', ''), (6, 3, '1-D', ''), (7, 9, '', '111D--0pp'), (8, 6, '110pp-', ''), (12, 10, '', '=1xx000<<π'), (13, 10, 'πxx=<<0001', ''), (20, 6, '', '11aaa-'), (21, 6, '11aaa-', '')]\nVOLUME A4 一 4 1- \nCOMPARE A4 一 5 22 [(1, 9, '+11nnn=22', ''), (2, 22, '', 'xxxx00=2222222yyyy+++≠'), (3, 24, 'xxxxyyyy2222222+++≠0', '=nn1'), (4, 6, 'nn==01', ''), (5, 1, '', '1'), (6, 1, '1', ''), (8, 1, '', 'T'), (9, 1, 'T', ''), (11, 13, '', '=1111+2nnnn--'), (12, 13, 'nnnn=1111--2+', ''), (13, 3, '', 'x2+'), (14, 3, 'x2+', '')]\nVOLUME A4 一 5 +11nnn=22 \nCOMPARE A4 一 6 22 [(1, 8, 'xx=1--yC', ''), (2, 7, '', 'x1--Cy='), (3, 6, '', '==nn11'), (4, 6, '==nn11', ''), (9, 12, '', '为为2样样本本均值S方差'), (10, 12, '2为为样样本本均值S方差', ''), (15, 7, '', '2为样本均值S'), (16, 7, '2为样本均值S', ''), (17, 2, '', '2d'), (18, 2, '2d', ''), (20, 4, '', '1=i3'), (21, 4, '1=i3', '')]\nVOLUME A4 一 6 x \nCOMPARE A4 一 7 22 [(1, 1, '2', ''), (2, 3, '24D', ''), (4, 3, '', 'D24'), (5, 1, '', '2'), (6, 1, '2', ''), (7, 29, 'A=αααααα112233的0必线性关B无X基础', ''), (8, 53, '', 'AB若==αααααα1111122233必线性无'), (9, 24, 'XYxxy=a00<<<<<111其他若P2b8', ''), (11, 7, '', 'tt=+x22'), (12, 7, '=xtt22+', '')]\nVOLUME A4 一 7 2 \nCOMPARE A4 一 8 22 [(1, 2, '', '+x'), (2, 2, 'x+', ''), (4, 1, '', '-'), (5, 21, '', '11111222233333-bbbbbb'), (6, 22, 'bbbbbb33333111112222--', ''), (19, 36, '', '111112222xxxx++===0dttttt'), (20, 36, '111112222gggttttttt-n++==', '')]\nVOLUME A4 一 8  \nCOMPARE A3 二 1 22 [(1, 17, '', '+++++22221nnnnnnn'), (2, 17, 'nnnnnnn++++222', 'xx-'), (3, 6, 'xx+2-1', ''), (12, 2, '', '1-'), (13, 2, '-1', ''), (20, 17, '', '111=xxxxxx<>ge-ln'), (21, 14, 'xxxxxx=<ln>ge-', ''), (22, 3, '111', '')]\nVOLUME A3 二 1  \nCOMPARE A3 二 2 22 [(1, 2, 'x1', ''), (2, 1, '', 'x'), (3, 1, 'x', ''), (5, 6, '', '23zx-y'), (6, 6, 'zxy2-3', ''), (7, 4, '', '12i='), (8, 6, '=2i', '110'), (9, 4, '1110', ''), (10, 11, '', '+++-1111xxx'), (11, 11, 'xxx+++1111-', ''), (12, 2, '', '3x'), (13, 2, 'x3', ''), (15, 11, '', '1=xxx2λ++3a'), (16, 14, 'λxxx1++23=a', 'nnk'), (17, 3, 'nnk', ''), (19, 4, '', '2x4-'), (20, 4, '2x-4', '')]\nVOLUME A3 二 2 x1 \nCOMPARE A3 二 3 22 [(8, 3, '', '210'), (9, 6, '20', 'βββr'), (10, 5, 'βββ1r', ''), (11, 1, '', 'π'), (12, 40, 'π', 'xxxx+++3==222222yyy其中zzz是'), (13, 38, 'u==zzzxxxxyy222222+++其中是由', ''), (14, 7, 'y', 'x=tsin'), (15, 6, '=xsint', ''), (18, 1, '', 'y'), (19, 1, 'y', ''), (21, 15, '', '1111222---00a+3'), (22, 15, '111122200---a+3', '')]\nVOLUME A3 二 3  \nCOMPARE A3 二 4 22 [(4, 1, '', '2'), (5, 1, '2', ''), (14, 2, '', 'x2'), (15, 2, 'x2', ''), (17, 2, '', 'x+'), (18, 2, 'x+', '')]\nVOLUME A3 二 4  \nCOMPARE A3 二 5 22 [(1, 9, '+11nnn=22', ''), (3, 22, '', 'xxx2+aanl1则de-收敛的取值范围为'), (4, 22, '+2elnxxxaa-1d收敛则的取值范围为', ''), (6, 21, '', 'xxxxxn+=则lyyyyyzzz满足d'), (7, 21, 'zzz=xxxxxyyyyy满足+ln则d', ''), (8, 6, '', '000111'), (9, 6, '111000', ''), (10, 3, '', '1x0'), (11, 3, 'x01', ''), (13, 4, '', 'x2+y'), (14, 20, 'yx', '=nnnnnnnl2++11kkkk'), (15, 20, 'lnnnnnnnkkkk=1122+++', ''), (17, 36, '', '111110xxxx-2222nttttttt++'), (18, 36, '111112222gggttttttt-n++==', '')]\nVOLUME A3 二 5 +11nnn=22 \nCOMPARE A3 二 6 22 [(1, 1, 'x', ''), (3, 1, '', 'z'), (4, 1, 'z', ''), (13, 1, '', 'S'), (14, 1, 'S', ''), (17, 2, '', 'yd'), (18, 3, 'yd', 'n'), (19, 28, '', '222+000i≤≤≤≤≤≤θθθθπrrccoo'), (20, 29, '222rrθθθθ000≤≤≤≤≤≤πccooss', ''), (21, 4, '', '1=i3'), (22, 4, '1=i3', '')]\nVOLUME A3 二 6 x \nCOMPARE A3 二 7 22 [(1, 1, '2', ''), (8, 12, '', '00000002111a'), (9, 12, '21110000000a', ''), (12, 6, '', 't=+x22'), (13, 6, '=xt22+', ''), (14, 4, '', '2x+y'), (15, 4, 'x2y+', ''), (21, 12, '', '11122000a--4'), (22, 12, '11122000a--4', '')]\nVOLUME A3 二 7 2 \nCOMPARE A3 二 8 22 [(1, 10, 'tt0d', '+2211-'), (2, 8, 'xx22+11-', ''), (7, 6, '', '11-235'), (8, 18, '5', '2223333111-bbbbbb'), (9, 22, 'bbbbbb33333111112222--', ''), (16, 1, '', '2'), (17, 1, '2', '')]\nVOLUME A3 二 8 tt0dxx \nCOMPARE A4 二 1 22 [(1, 17, '', '+++++22221nnnnnnn'), (2, 17, 'nnnnnnn++++222', 'xx-'), (3, 6, 'xx+2-1', ''), (12, 2, '', '1-'), (13, 2, '-1', ''), (20, 17, '', '111=xxxxxx<>ge-ln'), (21, 14, 'xxxxxx=<ln>ge-', ''), (22, 3, '111', '')]\nVOLUME A4 二 1  \nCOMPARE A4 二 2 22 [(1, 2, 'x1', ''), (2, 1, '', 'x'), (3, 1, 'x', ''), (7, 4, '', '12i='), (8, 6, '=2i', '110'), (9, 4, '1110', ''), (10, 11, '', '+++-1111xxx'), (11, 11, 'xxx+++1111-', ''), (12, 2, '', '3x'), (13, 2, 'x3', ''), (15, 11, '', '1=xxx2λ++3a'), (16, 14, 'λxxx1++23=a', 'nnk'), (17, 3, 'nnk', ''), (19, 4, '', '2x4-'), (20, 4, '2x-4', '')]\nVOLUME A4 二 2 x1 \nCOMPARE A4 二 3 22 [(3, 9, '>>III123D', ''), (4, 9, '', '1DIII2>>3'), (8, 3, '', '210'), (9, 6, '20', 'βββr'), (10, 5, 'βββ1r', ''), (11, 1, '', 'π'), (12, 40, 'π', 'xxxx+++3==222222yyy其中zzz是'), (13, 38, 'u==zzzxxxxyy222222+++其中是由', ''), (14, 7, 'y', 'x=tsin'), (15, 6, '=xsint', ''), (18, 1, '', 'y'), (19, 1, 'y', ''), (21, 15, '', '1111222---00a+3'), (22, 15, '111122200---a+3', '')]\nVOLUME A4 二 3  \nCOMPARE A4 二 4 22 [(1, 2, '1-', ''), (4, 1, '', '2'), (5, 1, '2', ''), (9, 2, '2D', ''), (10, 2, '', '2D'), (14, 2, '', 'x2'), (15, 2, 'x2', ''), (16, 1, '', 'x'), (17, 3, '', '1+x'), (18, 15, '112xx+ttt-d的最小值', ''), (19, 11, '', '12ttt-d的最小值')]\nVOLUME A4 二 4 1- \nCOMPARE A4 二 5 22 [(1, 9, '+11nnn=22', ''), (3, 22, '', 'xxx2+aanl1则de-收敛的取值范围为'), (4, 22, '+2elnxxxaa-1d收敛则的取值范围为', ''), (6, 21, '', 'xxxxxn+=则lyyyyyzzz满足d'), (7, 21, 'zzz=xxxxxyyyyy满足+ln则d', ''), (8, 6, '', '000111'), (9, 6, '111000', ''), (10, 3, '', '1x0'), (11, 3, 'x01', ''), (13, 4, '', 'x2+y'), (14, 20, 'yx', '=nnnnnnnl2++11kkkk'), (15, 20, 'lnnnnnnnkkkk=1122+++', ''), (17, 36, '', '111110xxxx-2222nttttttt++'), (18, 36, '111112222gggttttttt-n++==', '')]\nVOLUME A4 二 5 +11nnn=22 \nCOMPARE A4 二 6 22 [(1, 1, 'x', ''), (3, 1, '', 'z'), (4, 1, 'z', ''), (13, 1, '', 'S'), (14, 1, 'S', ''), (17, 2, '', 'yd'), (18, 3, 'yd', 'n'), (19, 28, '', '222+000i≤≤≤≤≤≤θθθθπrrccoo'), (20, 29, '222rrθθθθ000≤≤≤≤≤≤πccooss', ''), (21, 4, '', '1=i3'), (22, 4, '1=i3', '')]\nVOLUME A4 二 6 x \nCOMPARE A4 二 7 22 [(1, 1, '2', ''), (8, 12, '', '00000002111a'), (9, 12, '21110000000a', ''), (12, 6, '', 't=+x22'), (13, 6, '=xt22+', ''), (14, 4, '', '2x+y'), (15, 8, 'x2y+', '3ααT'), (16, 4, 'αα3T', ''), (21, 12, '', '11122000a--4'), (22, 12, '11122000a--4', '')]\nVOLUME A4 二 7 2 \nCOMPARE A4 二 8 22 [(1, 10, 'tt0d', '+2211-'), (2, 8, 'xx22+11-', ''), (7, 6, '', '11-235'), (8, 18, '5', '2223333111-bbbbbb'), (9, 22, 'bbbbbb33333111112222--', ''), (16, 1, '', '2'), (17, 1, '2', '')]\nVOLUME A4 二 8 tt0dxx \n"}
{"chunk_id":"acf38a","wall_time_seconds":0.000007917,"exit_code":0,"original_token_count":864,"output":"find: 302模拟27md: No such file or directory\n## 卷六· 李林四套卷（2）\n\n### 选择题\n\n1\\. 设 $\\lim_{x\\to\\infty}f'(x)=0$，且 $\\lim_{x\\to\\infty}\\left(\\frac{ax^2}{1+x}-bx-1\\right)=\\lim_{x\\to\\infty}[f(x+1)-f(x)]$，则曲线 $y=\\frac{ax^2}{1+x}$ 的斜渐近线方程为（　）。\n\nA. $y=-x+1$  \nB. $y=x+1$  \nC. $y=-x-1$  \nD. $y=x-1$\n\n2\\. 设可导函数 $f(x)$ 在 $[a,b]$ 上满足 $f(x)>0$，$f'(x)>0$，则 $\\lim_{b\\to a^+}\\frac{\\ln f(b)-\\ln f(a)}{f(b)-f(a)}=$（　）。\n\nA. $f(a)$  \nB. $\\frac1{f(a)}$  \nC. $\\frac1{f'_+(a)}$  \nD. $f'_+(a)$\n\n3\\. 设 $I_1=\\int_0^1\\ln(1+x)\\,\\mathrm dx$，$I_2=\\int_0^1\\frac{\\arctan x}{1+x}\\,\\mathrm dx$，$I_3=\\int_0^1\\sqrt{\\ln(1+x)}\\,\\mathrm dx$，则（　）。\n\nA. $I_3>I_1>I_2$  \nB. $I_3>I_2>I_1$  \nC. $I_1>I_2>I_3$  \nD. $I_2>I_3>I_1$\n\n4\\. 设 $z(x,y)$ 满足 $\\frac{\\partial z}{\\partial x}=\\sin y+\\frac1{1-xy}$，$z(1,y)=\\sin y$，则（　）。\n\nA. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx+\\mathrm dy$  \nB. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx-\\mathrm dy$  \nC. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx+\\frac12\\,\\mathrm dy$  \nD. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx-\\frac12\\,\\mathrm dy$\n\n5\\. 设正项数列 $\\{x_n\\}$ 满足 $x_{n+1}<2-\\frac1{x_n}$（$n=1,2,\\ldots$），则（　）。\n\nA. $\\{x_n\\}$ 收敛于 0。  \nB. $\\{x_n\\}$ 收敛于 1。  \nC. $\\{x_n\\}$ 收敛于 $\\sqrt2$。  \nD. $\\{x_n\\}$ 发散。\n\n6\\. 设 $f(x)$ 在 $[0,4]$ 上有二阶连续导数，在 $xOy$ 坐标系中，三条曲线为 $y=f(x)$，$y=f'(x)$，$y=f''(x)$。如图所示，$L_1$ 单调增加，在 $x=2$ 处穿过 $x$ 轴；$L_2$ 从 $y$ 轴上方下降，在 $x=1$ 处穿过 $x$ 轴，达到极小值后上升，在 $x=3$ 处再次穿过 $x$ 轴；$L_3$ 自 $y$ 轴附近上升，达到极大值后下降，在 $x=2$ 处穿过 $x$ 轴，达到极小值后上升，在 $x=4$ 处再次穿过 $x$ 轴。则 $y=f(x)$ 在 $[0,4]$ 上（　）。\n\nA. 有一个极值点，一个拐点。  \nB. 有一个极值点，两个拐点。  \nC. 有两个极值点，一个拐点。  \nD. 有两个极值点，两个拐点。\n\n7\\. 已知平面上的点 $A(0,1)$ 和抛物线 $x=2\\sqrt y$，动点 $P$ 从坐标原点 $O$ 出发，沿抛物线移动。若直线段 $OA$、$AP$ 和抛物线所围成图形的面积对时间 $t$ 的增大速率为 1，则当 $P$ 移动到点 $(6,9)$ 处时，$P$ 的横坐标的变动速率为（　）。\n\nA. $\\frac12$  \nB. $\\frac13$  \n{\"source\": \"模拟卷40套整理合集PDF（可高清打印）（仅数二）/试卷/【紧凑版】26模拟卷数学二40套精选.pdf\", \"page\": 4, \"sha256\": \"bdd199d7f4926430028b53aaf7a7b7a0d8c312cb0e5d307c6fc52a6d6b44b211\", \"text\": \"微信公众号：考研佳友 精选40套·数学二\\n26 张宇四套卷·卷一\\n一、选择题：1～10小题，每小题5分，共50分\\n1. 当 \\\\(x \\\\to 0^{+}\\\\) 时，下列无穷小量中，最高阶的是\\nA. \\\\(\\\\int_0^{x^2} (e^{t^2} - 1) dt\\\\) B. \\\\(\\\\int_0^x \\\\ln(1 + \\\\sqrt{t^3}) dt\\\\) C. \\\\(\\\\int_0^{\\\\sin x} \\\\cos t^2 dt\\\\) D. \\\\(\\\\int_0^{1 - \\\\cos x} \\\\sqrt{\\\\arcsin^3 t} dt\\\\)\\n2. \\\\(\\\\lim_{n \\\\to \\\\infty} \\\\left[ \\\\frac{n}{(n+1)^2} + \\\\frac{n}{(n+2)^2} + \\\\cdots + \\\\frac{n}{(n+n)^2} \\\\right] =\\\\)\\nA. \\\\(\\\\frac{1}{3}\\\\) B. \\\\(\\\\frac{\\\\pi}{3}\\\\) C. \\\\(\\\\frac{1}{2}\\\\) D. \\\\(\\\\frac{\\\\pi}{2}\\\\)\\n3. 曲线 \\\\(y = x + \\\\sqrt{x^2 - x + 1}\\\\) 的渐近线条数为\\nA. 1 B. 2 C. 3 D. 4\\n4. 函数 \\\\(f(x, y) = \\\\sqrt{|xy|}\\\\) 在 \\\\((0, 0)\\\\) 点\\nA."}

## tool · 2026-11-12T01:27:40Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"75d351","wall_time_seconds":0.000010167,"exit_code":0,"original_token_count":1096,"output":"references/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A4数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A3数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md\nimport re\nimport sys\nfrom pathlib import Path\n\n\nsource = Path(sys.argv[1]).read_text(encoding='utf-8').strip()\nexpected_count = int(sys.argv[2])\nnumbering = re.findall(r'(?m)^(\\d+)\\\\\\.', source)\nassert numbering == list(map(str, range(1, expected_count + 1))), numbering\nassert source.count('$') % 2 == 0\nfor name in sys.argv[3:]:\n    paths = list(Path('references/302模拟27md').rglob(name))\n    assert len(paths) == 1, name\n    path = paths[0]\n    current = path.read_text(encoding='utf-8')\n    title = current.splitlines()[0]\n    assert title.startswith('# ')\n    revised = title + '\\n\\n' + source + '\\n'\n    path.write_text(revised, encoding='utf-8')\n    assert path.read_text(encoding='utf-8') == revised\n    print(path)\nfrom collections import Counter\nfrom pathlib import Path\nimport re\nimport unicodedata\n\nimport pymupdf\n\n\nroot = Path('references/302模拟27')\npattern = re.compile(r'(?m)^\\s*[（(](\\d{1,2})[）)]')\n\n\ndef questions(path):\n    papers = []\n    with pymupdf.open(path) as pdf:\n        volumes = [(title, page) for depth, title, page in pdf.get_toc() if depth == 1]\n        for index, (title, first) in enumerate(volumes[:8]):\n            last = volumes[index + 1][1]\n            content = '\\n'.join(page.get_text() for page in pdf.pages(first - 1, last - 1))\n            content = re.sub(\n                r'(?m)^.*(?:公众号|第\\s*\\d+\\s*页|模拟卷精选\\s*20\\s*套|[一二三]、(?:选择|填空|解答)题|[张李][宇林][四八六]套卷).*$',\n                '', content,\n            )\n            matches = []\n            for m in pattern.finditer(content):\n                if int(m[1]) == len(matches) + 1:\n                    matches.append(m)\n            if len(matches) != 22:\n                print('PARTIAL', path.name, title, [m[1] for m in matches])\n            texts = {}\n            for i, m in enumerate(matches):\n                body = content[m.end():matches[i + 1].start() if i + 1 < len(matches) else len(content)]\n                texts[int(m[1])] = body.strip()\n            papers.append((title, texts))\n    return papers\n\n\ndef chars(text):\n    normalized = unicodedata.normalize('NFKC', text).replace('−', '-')\n    return Counter(c for c in normalized if c.isalnum() or c in '+-=><≠≤≥')\n\n\nfor subject in '一二':\n    ten = questions(next(root.rglob(f'【A4紧凑_带答案】数{subject}_精编10套模拟卷.pdf')))\n    for layout in ['A3', 'A4']:\n        source = next(root.rglob(f'{layout}数{subject}模拟卷精选20套.pdf'))\n        twenty = questions(source)\n        for v, ((oldtitle, old), (title, new)) in enumerate(zip(ten[:8], twenty[:8], strict=True), 1):\n            difference = []\n            for q in old.keys() & new.keys():\n                a, b = chars(old[q]), chars(new[q])\n                delta = sum((a - b).values()) + sum((b - a).values())\n                if delta:\n                    difference.append((q, delta, ''.join((a - b).elements())[:25], ''.join((b - a).elements())[:25]))\n            print('COMPARE', layout, subject, v, len(old.keys() & new.keys()), difference)\n            left = chars(''.join(old.values()))\n            right = chars(''.join(new.values()))\n            print('VOLUME', layout, subject, v, ''.join((left - right).elements()), ''.join((right - left).elements()))\nconst fs = require(\"node:fs\");\nconst katex = require(\"./proof-katex/node_modules/katex\");\n\nlet total = 0;\nfor (const filename of process.argv.slice(2)) {\n  const body = fs.readFileSync(filename, \"utf8\");\n  const spans = body.matchAll(/(?<!\\\\)(\\$\\$|\\$)([\\s\\S]*?)(?<!\\\\)\\1/g);\n  for (const [full, delimiters, expression] of spans) {\n    try {\n      katex.renderToString(expression, { displayMode: delimiters.length === 2, throwOnError: true });\n    } catch (error) {\n      throw new Error(filename + \" \" + full + \": \" + error.message);\n    }\n    total += 1;\n  }\n}\nconsole.log(total + \" math expressions rendered\");\n"}

## tool · 2026-11-12T01:27:44Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"385277","wall_time_seconds":0.000011709,"exit_code":1,"original_token_count":134,"output":"  File \"<string>\", line 1\n    from pathlib import Path; import pymupdf; p=next(Path('references/302模拟27').rglob('【A4紧凑_带答案】数二_精编10套模拟卷.pdf')); d=pymupdf.open(p); print(d.get_toc()); print(p); print('\\n'.join(d[i].get_text() for i in range(25,29))))\n                                                                                                                                                                                                                             ^\nSyntaxError: unmatched ')'\n"}

## tool · 2026-11-12T01:27:51Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"d1e2b9","wall_time_seconds":0.021311667,"exit_code":0,"original_token_count":1548,"output":"[[1, '卷一 · 张宇四套卷（1）', 2], [2, '一、选择题.', 2], [2, '二、填空题.', 3], [2, '三、解答题.', 4], [1, '卷二 · 张宇四套卷（2）', 6], [2, '一、选择题.', 6], [2, '二、填空题.', 7], [2, '三、解答题.', 8], [1, '卷三 · 张宇四套卷（3）', 10], [2, '一、选择题.', 10], [2, '二、填空题.', 11], [2, '三、解答题.', 12], [1, '卷四 · 张宇四套卷（4）', 14], [2, '一、选择题.', 14], [2, '二、填空题.', 15], [2, '三、解答题.', 16], [1, '卷五 · 李林四套卷（1）', 18], [2, '一、选择题.', 18], [2, '二、填空题.', 19], [2, '三、解答题.', 20], [1, '卷六 · 李林四套卷（2）', 22], [2, '一、选择题.', 22], [2, '二、填空题.', 23], [2, '三、解答题.', 24], [1, '卷七 · 李林四套卷（3）', 26], [2, '一、选择题.', 26], [2, '二、填空题.', 27], [2, '三、解答题.', 28], [1, '卷八 · 李林四套卷（4）', 30], [2, '一、选择题.', 30], [2, '二、填空题.', 31], [2, '三、解答题.', 32], [1, '卷九 · 李林六套卷（1）', 34], [2, '一、选择题.', 34], [2, '二、填空题.', 35], [2, '三、解答题.', 36], [1, '卷十 · 合工大超越（1）', 38], [2, '一、选择题.', 38], [2, '二、填空题.', 39], [2, '三、解答题.', 40]]\nreferences/302模拟27/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_精编10套模拟卷.pdf\n卷七· 李林四套卷（3）\n一、选择题.\n(1) 当x →0 时, 1+x\n\n\n2\nx - e2 1-ln 1+x\n\n\n\n\n是关于x 的\nA. 高阶无穷小.\nB. 等价无穷小.\nC. 同阶但非等价无穷小.\nD. 低阶无穷小.\n(2) 设f x\n\n\n在[0, +∞) 上有连续导数, 且f x\n\n\n> 0.当0 < a < x < b 时, 有\nA. a\nx\n0 f\nt\n\n\ndt < x\na\n0 f\n\nt\n\n\ndt.\nB. b\nx\n0 f\nt\n\n\ndt < x\nb\n0 f\n\nt\n\n\ndt.\nC. x\nx\n0 f\nt\n\n\ndt < b\nb\n0 f\n\nt\n\n\ndt.\nD. x\nx\n0 f\nt\n\n\ndt > a\na\n0 f\n\nt\n\n\ndt.\n(3) 设y1 x\n\n\n与y2 x\n\n\n是非齐次微分方程y+ P x\n\n\ny = Q x\n\n\n的两个解.若λy1 x\n\n\n+ μy2 x\n\n\n仍是该方程的\n解, 则eλ3+μ3的最小值为\nA. e-1.\nB. e\n1\n2 .\nC. e\n1\n4 .\nD. e\n1\n3 .\n(4) 下列积分发散的是\nA.\n+∞\n1\ndx\nx3 1+x\n\n.\nB.\n+∞\n0\nx2\n\ne-xdx.\nC.\n+∞\n2\ndx\nxln2x\n\n.\nD.\n+∞\n-∞e x\n\n\nsinxdx.\n(5) 下列结论正确的是\n①若f x\n\n\n在x = a 处连续，且lim\nx→0\nf a+x3\n\n\n- f a\n\n\nx2\n存在，则f a\n\n\n存在.\n②若lim\nn→∞n f a+ 1\nn\n\n\n- f a\n\n\n\n\n\n\n(n 为正整数) 存在，则f a\n\n\n存在.\n③若f x\n\n\n= x-a\n\n\nφ x\n\n\n，其中φ x\n\n\n在x = a 处连续，则f a\n\n\n存在.\n④存在δ > 0, 对∀x ∈a-δ,a+δ\n\n\n, 有f x\n\n\n\n≤L x-a\n\nα, 其中L > 0,α > 1 为常数, 则f a\n\n\n存在.\nA. ①②.\nB. ②③.\nC. ②④.\nD. ③④.\n第25 页，共40 页\n\n(6) 积分\n2\n0d\n\nx\nx\n3x f\n\nx2+y2\n\n\ndy =\nA.\nπ\n3\nπ\n4 d\n\nθ\n2secθ\n0\nf\n\nr\n\n\nrdr.\nB.\nπ\n4\nπ\n3 d\n\nθ\n2secθ\n0\nf\n\nr\n\n\ndr.\nC. -\n2 2\n0\nd\n\nr\nπ\n3\nπ\n4 f\n\nr\n\n\nrdθ -\n4\n2 2d\n\nr\nπ\n3\narccos 2\nr f\n\nr\n\n\nrdθ.\nD.\n2 2\n0\nd\n\nr\nπ\n3\nπ\n4 f\n\nr\n\n\nrdθ +\n4\n2 2d\n\nr\nπ\n3\narccos 2\nr f\n\nr\n\n\nrdθ.\n(7) 设f x\n\n\n=\n1\nx\nx2\nx3\n1\n2\n4\n8\n1\n-1\n1\n-1\n1\n1\n1\n1\n\n\n, 则曲线y = f x\n\n\n在-1,2\n\n\n内存在水平切线的条数为\nA. 0.\nB. 1.\nC. 2.\nD. 3.\n(8) 设A 是m × n 矩阵, 则非齐次线性方程组AX = b 有解的充分必要条件是\nA. r A\n\n\n= r AT\n\n\n= m.\nB. r A\n\n\n= r AT\n\n\n= n.\nC. r AT\n\n\n= r AT\nbT\n\n\n= m.\nD. ATX = 0 与\nAT\nbT\n\n\nX = 0 同解.\n(9) 设A =\n2\n1\n0\n1\n2\n0\n0\n0\na\n\n\n\n\n\n\n\n\n\n\n与B =\n1\n0\n0\n0\n1\n1\n0\n1\n0\n\n\n\n\n\n\n\n\n\n\n合同, 则\nA. a = 0.\nB. a < 0.\nC. a > 0.\nD. a > 1.\n(10) 设4 阶实矩阵A = aij\n\n\n= α1,α2,α3,α4\n\n\n,a11 的代数余子式A11 ≠0, 且A\n\n= 0, 则下列选项正确的\n是\nA. α2,α3,α4 必线性相关.\nB. α1,α2,α3 必线性无关.\nC. A*X = 0 的基础解系为α2,α3,α4.\nD. A*X = 0 的基础解系为α1,α2,α3.\n二、填空题.\n(11) 曲线y = x+1\n\n\nenx-1\n\n\nn>1\n\n\n与x 轴所围图形的面积为_____.\n第26 页，共40 页\n\n(12) 设f t\n\n\n= lim\nn→∞\nn\ni=1\nt-1\nn+ t-1\n\n\ni\n\n\nt-1\nn i\n\nt>1\n\n\n, 则lim\nt→+∞f t\n\n\n= _____.\n(13) 设函数y = y x\n\n\n由\nx=t2+2t\n1\n2 siny-y+t2=1\n\nt>0\n\n\n确定, 则d2y\ndx2 x=3\n= _____.\n(14) 设lim\nx→0\nln 1-2x3\n\n\n+xf x\n\n\nx6\n= 3, 则lim\nx→0\nf x\n\n\n-2x2\nx5\n= _____.\n(15) 设g x\n\n\n连续, g 2\n\n\n= 1,f x,y\n\n\n=\nx2+y2\n0\ntg\n\nx2+y2-t2\n\n\ndt, 则df 1,1\n\n\n= _____.\n(16) 设α 为3 维非零实列向量，E 为3 阶单位矩阵，A = E -\n3\nαTα\nααT，则tr A\n\n\n= _____.\n三、解答题.\n(17) (本题满分10 分) 求极限lim\nx→0\nx\n0d\n\nu\nu\n0 u2-3sin u-t\n\n\n2\n\n\n\ndt\nsinx8\n.\n(18) (本题满分12 分)\n设可导函数y = f x\n\n\n由方程ex-2y - x2y = 1 确定, 计算lim\nx→1+\nsin x-1\n\n\nx-1\n\n\n3\n1\n0 f\n\nt x-1\n\n\ndt.\n(19) (本题满分12 分) 设f x\n\n\n满足f x\n\n\n- f x\n\n\n= πexcosπx,f 0\n\n\n= 0,y = f x\n\n\n在0,n\n\n\n(n 为正整数) 上\n与x 轴所围图形的面积为Sn.\n(I) 求f x\n\n\n;\n(II) 求lim\nn→∞\nSn\nen .\n第27 页，共40 页\n\n(20) (本题满分12 分) 设z = f u,v\n\n\n有二阶连续偏导数，u = x - 2\ny,v = x + 2\ny，且满足\n∂2z\n∂x2 - y ∂2z\n∂y2 - 1\n2\n∂z\n∂y = 12a\na≠0\n\n\n(I) 求∂2z\n∂u∂v ;\n(II) 若∂f u,0\n\n\n∂u\n=-3u2,f 0,v\n\n\n=-v3, 求f u,v\n\n\n的极值.\n(21) (本题满分12 分) 设D =\nx,y\n\n\n∣x2+y2≤1,x≥0,y≥0\n\n\n, 计算I =\nDmax\n\ny+1,\n2\n1+x\n\n\ndxdy.\n(22) (本题满分12 分) 设A =\n2\n1\n0\n1\n2\n0\n0\n0\n1\n\n\n\n\n\n\n\n\n\n\n与B =\na\nb\nc\n0\n1\n0\n-1\n-2\n4\n\n\n\n\n\n\n\n\n\n\n相似.\n(I) 求a,b,c 的值;\n(II) 求可逆矩阵P, 使得P-1AP = B;\n(III) 求可逆矩阵C, 使得A = CTC.\n第28 页，共40 页\n\n"}

## tool · 2026-11-12T01:27:58Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"60689d","wall_time_seconds":0.200035458,"exit_code":0,"original_token_count":0,"output":""}
{"chunk_id":"8417e7","wall_time_seconds":0.000008,"exit_code":0,"original_token_count":385,"output":"## 卷一· 张宇四套卷（1）\n### 选择题\n### 填空题\n### 解答题\n## 卷二· 张宇四套卷（2）\n### 选择题\n### 填空题\n### 解答题\n## 卷三· 张宇四套卷（3）\n### 选择题\n### 填空题\n### 解答题\n## 卷四· 张宇四套卷（4）\n### 选择题\n### 填空题\n### 解答题\n## 卷五· 李林四套卷（1）\n### 选择题\n### 填空题\n### 解答题\n## 卷六· 李林四套卷（2）\n### 选择题\n### 填空题\n### 解答题\n## 卷七· 李林四套卷（3）\n### 选择题\n### 填空题\n### 解答题\n## 卷八· 李林四套卷（4）\n### 选择题\n### 填空题\n### 解答题\n## 卷九· 李林六套卷（1）\n### 选择题\n### 填空题\n### 解答题\n## 卷十· 合工大超越（1）\n### 选择题\n### 填空题\n### 解答题\n## 张宇四套卷· 卷一\n### 选择题\n### 填空题\n### 解答题\n## 张宇四套卷· 卷二\n### 选择题\n### 填空题\n### 解答题\n## 张宇四套卷· 卷三\n### 选择题\n### 填空题\n### 解答题\n## 张宇四套卷· 卷四\n### 选择题\n### 填空题\n### 解答题\n## 李林四套卷· 卷一\n### 选择题\n### 填空题\n### 解答题\n## 李林四套卷· 卷二\n### 选择题\n### 填空题\n### 解答题\n## 李林四套卷· 卷三\n### 选择题\n### 填空题\n### 解答题\n## 李林四套卷· 卷四\n### 选择题\n### 填空题\n### 解答题\n## 张宇八套卷·卷四\n### 选择题\n### 填空题\n### 解答题\n## 张宇八套卷·卷五\n### 选择题\n### 填空题\n### 解答题\n## 张宇八套卷·卷六\n### 选择题\n### 填空题\n### 解答题\n"}

## tool · 2026-11-12T01:28:01Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/45acaaf951df16df37d4f3fb476d722e3cf12e4003435c133b6318171c8e2226.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/97541945e3a4ed6707fad5afc23da97b2cfa77f910bb4ecbf589acaad50667c6.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/cbba93bfb75c5d5dfa127ce4fc84e50c6129bb4bfd3940261bb8fed4ffac0218.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/d83ab8fae25521f7189ed4f8b1ada19ddd9f33030fe8b91736aa111fbffe9558.png",
  "detail": "high"
}

## tool · 2026-11-12T01:28:07Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"0e1a48","wall_time_seconds":0.000024459,"exit_code":0,"original_token_count":1492,"output":"## 卷七· 李林四套卷（3）\n\n### 选择题\n\n2  \nx - e2 1-ln 1+x  \n\n\n(1) 当x →0 时, 1+x  \n  \n  \n  \n  \n  \n是关于x 的  \nA. 高阶无穷小.  \nB. 等价无穷小.  \nC. 同阶但非等价无穷小.  \nD. 低阶无穷小.\n\n(2) 设f x  \n  \n  \n在[0, +∞) 上有连续导数, 且f x  \n  \n  \n\\> 0.当0 < a < x < b 时, 有  \nx  \na  \nx  \nb  \nA. a  \n0 f  \nt  \n  \n  \ndt < x  \n0 f  \n  \nt  \n  \n  \ndt.  \nB. b  \n0 f  \nt  \n  \n  \ndt < x  \n0 f  \n  \nt  \n  \n  \ndt.  \nx  \nb  \nx  \na  \nC. x  \n0 f  \nt  \n  \n  \ndt < b  \n0 f  \n  \nt  \n  \n  \ndt.  \nD. x  \n0 f  \nt  \n  \n  \ndt > a  \n0 f  \n  \nt  \n  \n  \ndt.\n\n(3) 设y1 x  \n  \n是非齐次微分方程y+ P x  \n  \ny = Q x  \n  \n\\+ μy2 x  \n  \n仍是该方程的  \n  \n与y2 x  \n  \n  \n  \n  \n的两个解.若λy1 x  \n  \n  \n  \n解, 则eλ3+μ3的最小值为  \n1  \n2 .  \nC. e  \n1  \n4 .  \nD. e  \n1  \n3 .  \nA. e-1.  \nB. e\n\n(4) 下列积分发散的是  \n+∞  \n+∞  \n+∞  \n+∞  \nA.  \ndx  \nx3 1+x  \n  \n.  \nB.  \n0  \nx2  \n  \ne-xdx.  \nC.  \ndx  \nxln2x  \n  \n.  \nD.  \n-∞e x  \n  \n  \nsinxdx.  \n1  \n2\n\n(5) 下列结论正确的是  \nf a+x3  \n  \n  \n\\- f a  \n  \n  \n①若f x  \n  \n在x = a 处连续，且lim  \nx2  \n存在，则f a  \n  \n存在.  \n  \n  \nx→0  \n②若lim  \nn→∞n f a+ 1  \n  \n  \nn  \n  \n  \n\\- f a  \n  \n  \n  \n(n 为正整数) 存在，则f a  \n  \n存在.  \n  \n  \n③若f x  \n  \n= x-a  \n  \nφ x  \n  \n，其中φ x  \n  \n在x = a 处连续，则f a  \n  \n存在.  \n  \n  \n  \n  \n  \n  \n≤L x-a  \n  \nα, 其中L > 0,α > 1 为常数, 则f a  \n  \n④存在δ > 0, 对∀x ∈a-δ,a+δ  \n  \n  \n, 有f x  \n  \n  \n  \n存在.  \nA. ①②.  \nB. ②③.  \nC. ②④.  \nD. ③④.  \n2  \nx\n\n(6) 积分  \n0d  \n  \nx  \n3x f  \n  \nx2+y2  \n  \n  \ndy =  \nπ  \n3  \n2secθ  \nπ  \n4  \n2secθ  \nπ  \n4 d  \n  \nθ  \n0  \nf  \n  \nr  \n  \nπ  \n3 d  \n  \nθ  \n0  \nf  \n  \nr  \n  \nA.  \n  \nrdr.  \nB.  \n  \ndr.  \n2 2  \nπ  \n3  \n4  \nπ  \n3  \n2 2  \nπ  \n3  \n4  \nπ  \n3  \nC. -  \n0  \nd  \n  \nr  \nπ  \n4 f  \n  \nr  \n  \n  \nrdθ -  \n2 2d  \n  \nr  \nr f  \n  \nr  \n  \n  \nrdθ.  \nD.  \n0  \nd  \n  \nr  \nπ  \n4 f  \n  \nr  \n  \n  \nrdθ +  \n2 2d  \n  \nr  \nr f  \n  \nr  \n  \n  \nrdθ.  \narccos 2  \narccos 2  \n1  \nx  \nx2  \nx3  \n1  \n2  \n4  \n8  \n1  \n-1  \n1  \n-1  \n1  \n1  \n1  \n1  \n  \n\n\n(7) 设f x  \n  \n=  \n, 则曲线y = f x  \n  \n在-1,2  \n  \n  \n  \n  \n内存在水平切线的条数为  \nA. 0.  \nB. 1.  \nC. 2.  \nD. 3.\n\n(8) 设A 是m × n 矩阵, 则非齐次线性方程组AX = b 有解的充分必要条件是  \nA. r A  \n  \n  \n= r AT  \n  \n  \n= m.  \nB. r A  \n  \n  \n= r AT  \n  \n  \n= n.  \n= r AT  \nbT  \n  \n  \n= m.  \nD. ATX = 0 与  \nAT  \nbT  \n  \n  \nC. r AT  \n  \n  \nX = 0 同解.  \n  \n  \n  \n\n\n(9) 设A =  \n  \n  \n  \n2  \n1  \n0  \n1  \n2  \n0  \n0  \n0  \na  \n  \n  \n  \n与B =  \n  \n  \n  \n1  \n0  \n0  \n0  \n1  \n1  \n0  \n1  \n0  \n  \n  \n  \n合同, 则  \n  \n  \n  \n  \nA. a = 0.  \nB. a < 0.  \nC. a > 0.  \nD. a > 1.\n\n(10) 设4 阶实矩阵A = aij  \n  \n  \n= α1,α2,α3,α4  \n  \n  \n,a11 的代数余子式A11 ≠0, 且A  \n  \n= 0, 则下列选项正确的  \n是  \nA. α2,α3,α4 必线性相关.  \nB. α1,α2,α3 必线性无关.  \nC. A*X = 0 的基础解系为α2,α3,α4.  \nD. A*X = 0 的基础解系为α1,α2,α3.\n\n### 填空题\n\n(11) 曲线y = x+1  \n  \n  \nenx-1  \n  \n  \nn>1  \n  \n  \n与x 轴所围图形的面积为_____.  \nn  \nt-1\n\n(12) 设f t  \n  \n  \n= lim  \nn→∞  \n  \n, 则lim  \nt→+∞f t  \n  \n  \n= _____.  \nn i  \n  \nt>1  \n  \nt-1  \ni=1  \ni  \n  \nn+ t-1  \n  \n  \n  \nx=t2+2t\n\n(13) 设函数y = y x  \n  \n1  \n2 siny-y+t2=1  \n  \nt>0  \n  \n确定, 则d2y  \ndx2 x=3  \n= _____.  \n  \n由  \n  \nln 1-2x3  \n  \n  \n+xf x  \n  \n  \nf x  \n  \n  \n-2x2\n\n(14) 设lim  \nx6  \n= 3, 则lim  \nx5  \n= _____.  \nx→0  \nx→0  \nx2+y2\n\n(15) 设g x  \n  \n  \n连续, g 2  \n  \n  \n= 1,f x,y  \n  \n  \n=  \n0  \ntg  \n  \nx2+y2-t2  \n  \n  \ndt, 则df 1,1  \n  \n= _____.  \n\n\n(16) 设α 为3 维非零实列向量，E 为3 阶单位矩阵，A = E -  \n3  \nαTα  \nααT，则tr A  \n  \n  \n= _____.\n\n### 解答题\n\nx  \nu  \n0d  \n  \nu  \n  \ndt  \n0 u2-3sin u-t  \n  \n2  \n  \n  \n\n\n(17) (本题满分10 分) 求极限lim  \nx→0  \nsinx8  \n.\n\n(18) (本题满分12 分)  \n由方程ex-2y - x2y = 1 确定, 计算lim  \nsin x-1  \n  \n  \n1  \n设可导函数y = f x  \n  \n  \n0 f  \n  \nt x-1  \n  \n  \ndt.  \nx→1+  \n3  \nx-1  \n  \n\n\n(19) (本题满分12 分) 设f x  \n  \n  \n满足f x  \n  \n  \n\\- f x  \n  \n  \n= πexcosπx,f 0  \n  \n  \n= 0,y = f x  \n  \n  \n在0,n  \n  \n  \n(n 为正整数) 上  \n与x 轴所围图形的面积为Sn.  \n(I) 求f x  \n  \n  \n;  \nSn  \nen .  \n(II) 求lim  \nn→∞\n\n(20) (本题满分12 分) 设z = f u,v  \n  \n  \n有二阶连续偏导数，u = x - 2  \ny,v = x + 2  \ny，且满足  \n∂2z  \n∂x2 - y ∂2z  \n∂y2 - 1  \n∂z  \n∂y = 12a  \na≠0  \n  \n  \n2  \n(I) 求∂2z  \n∂u∂v ;  \n(II) 若∂f u,0  \n  \n  \n∂u  \n=-3u2,f 0,v  \n  \n  \n=-v3, 求f u,v  \n  \n  \n的极值.  \nDmax  \n  \ny+1,  \n2  \n1+x  \n\n\n(21) (本题满分12 分) 设D =  \nx,y  \n  \n∣x2+y2≤1,x≥0,y≥0  \n  \n  \n  \n, 计算I =  \n  \ndxdy.  \n  \n  \n  \n\n\n(22) (本题满分12 分) 设A =  \n  \n  \n  \n2  \n1  \n0  \n1  \n2  \n0  \n0  \n0  \n1  \n  \n  \n  \n与B =  \n  \n  \n  \na  \nb  \nc  \n0  \n1  \n0  \n-1  \n-2  \n4  \n  \n  \n  \n相似.  \n  \n  \n  \n  \n(I) 求a,b,c 的值;  \n(II) 求可逆矩阵P, 使得P-1AP = B;  \n(III) 求可逆矩阵C, 使得A = CTC.\n\n"}

## tool · 2026-11-12T01:29:10Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-12T01:29:14Z




## tool · 2026-11-12T01:29:21Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/3acfbe089836415580305d5a27a3e43d61f5baf87c255d01edeb852cd91affcc.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/67fd93809629d92ab62906f34a3b4048505a2842d8756e5d9e9865b4e6c0a98c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/16f07167b29f7e38de3087de699394469896025374377d1c9788a9c86ceb0019.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/5efdfb1bbb34ee394166e803f4ea418971e8e28c48c3fc0ab29d21fbfb286b0c.png",
  "detail": "high"
}

## tool · 2026-11-12T01:30:21Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-11-12T01:30:28Z




## tool · 2026-11-12T01:30:33Z


Script completed
Wall time 0.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/f842d162f6273a4a60477297348d218c4d69ced2814eb349eb2ffee738e121a5.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/9e61f7196bb34aa2f8fbf0b66fa8f46970c923d287ad6deea78720c0f953eb8a.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/52957892634a2e1f92637743c6d7352b57d31275df88e14c3a274dd776a258aa.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/a6903f86c23328fa69048bf99fe3ede0e17d33bf9266ed7ab94f06a89ab79ee0.png",
  "detail": "high"
}
{"chunk_id":"1b62e8","wall_time_seconds":0.00001,"exit_code":0,"original_token_count":379,"output":"99:18\\. （12 分）设 $y(x)$ 满足 $4x\\frac{\\mathrm dy^2}{\\mathrm dx^2}+2(1-\\sqrt x)\\frac{\\mathrm dy}{\\mathrm dx}-6y=\\mathrm e^{-\\sqrt x}$。\n119:22\\. （12 分）设实对称矩阵 $A=(a_{ij})_{3\\times3}$ 有二重特征值 1，且 $\\sum_{i=1}^3a_{ij}=0$（$j=1,2,3$）。\n123:（Ⅱ）求可逆矩阵 $P$，使得 $X^T(2E-A)X=\\|PX\\|$。\n.question-bank-work/302-proof-source/老李林数二-22.png\n.question-bank-work/302-proof-source/十套数二合工大超越-38.png\n.question-bank-work/302-proof-source/十套数二合工大超越-39.png\n.question-bank-work/302-proof-source/老李林数二-25.png\n.question-bank-work/302-proof-source/十套数二卷一-5.png\n.question-bank-work/302-proof-source/十套数二卷一-4.png\n.question-bank-work/302-proof-source/数二十套逐题-22.png\n.question-bank-work/302-proof-source/十套数二卷一-3.png\n.question-bank-work/302-proof-source/十套数二卷一-2.png\n.question-bank-work/302-proof-source/数二十套逐题-25.png\n.question-bank-work/302-proof-source/张宇数二A4-21-22.png\n.question-bank-work/302-proof-source/十套数二合工大超越-40.png\n.question-bank-work/302-proof-source/四十套数二卷一-5.png\n.question-bank-work/302-proof-source/十套数二合工大超越-41.png\n.question-bank-work/302-proof-source/张宇按年份数二-2-22.png\n.question-bank-work/302-proof-source/四十套数二卷一-7.png\n.question-bank-work/302-proof-source/四十套数二卷一-6.png\n.question-bank-work/302-proof-source/四十套数二卷一-4.png\n"}

## tool · 2026-11-12T01:30:41Z




## tool · 2026-11-12T01:31:41Z


Script completed
Wall time 0.2 seconds
Output:

{}
{"chunk_id":"aff907","wall_time_seconds":0.00001025,"exit_code":0,"original_token_count":10,"output":"     343\n419 math expressions rendered\n"}

## tool · 2026-11-12T01:31:45Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/7c3546ea2e164dfcbd6aeb9030083cbe2e3123c38bd6718d146a537f31877a05.png",
  "detail": "high"
}

## tool · 2026-11-12T01:31:51Z




## tool · 2026-11-12T01:31:57Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"7a70c1","wall_time_seconds":0.033451042,"exit_code":0,"original_token_count":381,"output":".question-bank-work/apply-302-older-twenty.py\nA4数二模拟卷精选20套.pdf [('张宇四套卷 · 卷一', 2), ('张宇四套卷 · 卷二', 5), ('张宇四套卷 · 卷三', 8), ('张宇四套卷 · 卷四', 11), ('李林四套卷 · 卷一', 14), ('李林四套卷 · 卷二', 17), ('李林四套卷 · 卷三', 20), ('李林四套卷 · 卷四', 23), ('欧几里得三套卷 · 卷一', 26), ('张宇八套卷·卷四', 29), ('张宇八套卷·卷五', 32), ('张宇八套卷·卷六', 35), ('欧几里得三套卷 · 卷二', 38), ('余炳森五套卷 · 卷四', 41), ('余炳森五套卷 · 卷五', 44), ('欧几里得三套卷 · 卷三', 47), ('李擂 · 模拟卷五', 50), ('李擂 · 模拟卷六', 53), ('李擂 · 模拟卷七', 56), ('李擂 · 模拟卷八', 59)]\nA3数二模拟卷精选20套.pdf [('张宇四套卷 · 卷一', 5), ('张宇四套卷 · 卷二', 9), ('张宇四套卷 · 卷三', 13), ('张宇四套卷 · 卷四', 17), ('李林四套卷 · 卷一', 21), ('李林四套卷 · 卷二', 25), ('李林四套卷 · 卷三', 29), ('李林四套卷 · 卷四', 33), ('欧几里得三套卷 · 卷一', 37), ('张宇八套卷·卷四', 41), ('张宇八套卷·卷五', 45), ('张宇八套卷·卷六', 49), ('欧几里得三套卷 · 卷二', 53), ('余炳森五套卷 · 卷四', 57), ('余炳森五套卷 · 卷五', 61), ('欧几里得三套卷 · 卷三', 65), ('李擂 · 模拟卷五', 69), ('李擂 · 模拟卷六', 73), ('李擂 · 模拟卷七', 77), ('李擂 · 模拟卷八', 81)]\n"}

## tool · 2026-11-12T01:32:14Z


Script completed
Wall time 0.8 seconds
Output:

{}
{"chunk_id":"4d3ec9","wall_time_seconds":0.655195708,"exit_code":0,"original_token_count":68,"output":"references/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md\n"}

## tool · 2026-11-12T01:32:18Z




## tool · 2026-11-12T01:32:23Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/df8d29bf7b17a47e8d6b6580da35bb2c5dc7c75fc6d06384decd81f69a48ac2b.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/0a9404cbdc9828abf12a2780eb02483b6db07f727d4a6542703c5f3ef9123737.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/21101e794847fad1b56a91570488dc6d4b741f11709ab0d5ab29b17292870363.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/8f44d9d535c6b684de2f41446f7803cf1fe1251f12c1df7b94b43ea3c9c0db92.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/7e01d13a7fdac9c32b4b505ab95ecdf0815fb33bb502cdb59644c83915de9f6b.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/a9c88fd88133566c84976745584568ba454eecfe0bc9813f77bf54fe1802ef72.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/33a4433c8a489902e0d297c5f9da53f12ffcf99193e9e3d04b443d636d28c0d0.png",
  "detail": "high"
}

## tool · 2026-11-12T01:32:37Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"682b8c","wall_time_seconds":0.000011583,"exit_code":0,"original_token_count":603,"output":"## 卷二· 张宇四套卷（2）\n\n### 选择题\n\n1\\. 函数 $f(x)=\\frac{(\\mathrm e^{\\frac1{x-1}}-1)|x|}{(x+1)\\ln|x-1|}$ 的第一类间断点的个数为（　）。\n\nA. 0  \nB. 1  \nC. 2  \nD. 3\n## 卷四· 张宇四套卷（4）\n\n### 选择题\n\n1\\. 若函数 $f(x)=\\begin{cases}\\frac{1-\\cos\\sqrt x}{a\\ln(1+x)},&x>0,\\\\b,&x\\le0\\end{cases}$ 在 $x=0$ 处连续，则（　）。\n\nA. $ab=\\frac12$  \nB. $ab=-\\frac12$  \nC. $ab=0$  \nD. $ab=2$\n## 卷五· 李林四套卷（1）\n\n### 选择题\n\n1\\. 设 $f(x)$ 在 $(-\\infty,+\\infty)$ 内有二阶连续导数，且满足 $f\\left(\\frac1n\\right)=\\frac{n^2}{n^2+1}$（$n=1,2,\\ldots$），则 $f(x)$ 在 $x=0$ 处的二次泰勒多项式为（　）。\n\nA. $1-2x^2$  \nB. $x-2x^2$  \nC. $1-x^2$  \nD. $1+x-x^2$\n.question-bank-work/302-ten-two-v6.md:47:7\\. 已知平面上的点 $A(0,1)$ 和抛物线 $x=2\\sqrt y$，动点 $P$ 从坐标原点 $O$ 出发，沿抛物线移动。若直线段 $OA$、$AP$ 和抛物线所围成图形的面积对时间 $t$ 的增大速率为 1，则当 $P$ 移动到点 $(6,9)$ 处时，$P$ 的横坐标的变动速率为（　）。\n.question-bank-work/302-ten-two-v6.md:91:17\\. （10 分）设定义在 $(-\\infty,+\\infty)$ 内的连续函数 $f(x)$ 满足\n.question-bank-work/302-ten-two-v6.md:99:18\\. （12 分）设 $y(x)$ 满足 $4x\\frac{\\mathrm dy^2}{\\mathrm dx^2}+2(1-\\sqrt x)\\frac{\\mathrm dy}{\\mathrm dx}-6y=\\mathrm e^{-\\sqrt x}$。\n.question-bank-work/302-ten-two-v6.md:119:22\\. （12 分）设实对称矩阵 $A=(a_{ij})_{3\\times3}$ 有二重特征值 1，且 $\\sum_{i=1}^3a_{ij}=0$（$j=1,2,3$）。\n.question-bank-work/302-ten-two-v5.md:47:7\\. 设 $f(t)$ 可微，$z=xyf\\left(\\frac yx\\right)$ 满足 $x\\frac{\\partial z}{\\partial x}+y\\frac{\\partial z}{\\partial y}=xy\\frac yx$，则 $\\left.\\mathrm dz\\right|_{(1,1)}=$（　）。\n.question-bank-work/302-ten-two-v5.md:101:17\\. （10 分）计算 $\\lim_{x\\to1^-}\\frac{\\pi\\int_0^x[\\ln(1-t)+\\tan\\frac{\\pi}{2}t]\\,\\mathrm dt}{\\ln|\\sin\\pi x|}$。\n.question-bank-work/302-ten-two-v5.md:103:18\\. （12 分）设 $g(t)$ 满足 $g'(t)-g(t)\\ln\\left(1+\\frac1{2t}\\right)=-\\frac{g(t)}{2t+1}$，$g(1)=\\frac32$。$f(x)=\\int_x^{x^2}g(t)\\tan\\frac1{\\sqrt t}\\,\\mathrm dt$（$x>0$）。\n.question-bank-work/302-ten-two-v5.md:127:22\\. （12 分）设 $A=\\begin{bmatrix}0&2&3\\\\2&2&a\\\\2&3&4\\end{bmatrix}$，3 阶实对称矩阵 $B$ 满足 $AB+B=A+E$，$B\\ne E$，其中 $E$ 为单位矩阵，且 $r(A+B)=3$。\n"}
{
  "type": "input_image",
  "image_url": "images/175f4730f9e9d6c4f69bbe9bab6406990c4272995c7c0848e19bfe356c983754.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/1cc7fa744022f445b6967eccc8a8a8f83728802395e8473e73f4e40fafed4b8e.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/e93d643a47c0d9453af85acfab8af0a9451b197c7f46c27d6e90953d7105437e.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c93dc9dd46b974ce89786c5a6d5f1b6ef6876dc2c0482a9df92032d095e139ac.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/767d43240a61c99a017bcee6d605459e65d395051618a78ba8e86d45b2c5edf6.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/4f2a00cef9b7ce895b16976bf947a38dd32593a9dfda6c5cdd365923ca375bd7.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/e95ed773f03d27ef00df28462daf47d2107656138ba821dac560fe1d7f9e3a3c.png",
  "detail": "high"
}

## tool · 2026-11-12T01:32:52Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"chunk_id":"5ecde6","wall_time_seconds":0.000008,"exit_code":0,"original_token_count":68,"output":"references/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md\n"}

## tool · 2026-11-12T01:32:56Z




## tool · 2026-11-12T01:33:01Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/361fed9206f5fb3f34c0826facd52400257f30cbf53985198aef31e1f71c562a.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/d518a309cfe0f85c2d3eac686030899953d169f60cf7e26661b107dfbc92ccef.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/93e2578fa23bc9ecabda88bf7bbf4f68a3b34591f4f1d08d72310054e7fa46b0.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/7c6c518f00ab4723269f0bc78077fc854409b9c16ee4d4094b0b258ac51855ad.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/fe3d31306a524571318cb914c2c032b303eb183d6d0465895953be4712473a9c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c45a45e67bc0ab57a9f484446f07efae6e481279d2f478f3f4d6b3379fce1b18.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/6a96893f5531a95f57c6b13610e834448b789d22726627b3942fe7e3d040f2d8.png",
  "detail": "high"
}

## tool · 2026-11-12T01:33:12Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"1dec5b","wall_time_seconds":0.000011166,"exit_code":0,"original_token_count":4046,"output":"## 卷二· 张宇四套卷（2）\n\n### 选择题\n\n1\\. 函数 $f(x)=\\frac{(\\mathrm e^{\\frac1{x-1}}-1)|x|}{(x+1)\\ln|x-1|}$ 的第一类间断点的个数为（　）。\n\nA. 0  \nB. 1  \nC. 2  \nD. 3\n\n2\\. 已知数列 $\\{x_n\\}$，以下结论：\n\n① 当 $\\lim_{n\\to\\infty}\\cos(\\arctan x_n)$ 存在时，$\\lim_{n\\to\\infty}x_n$ 存在，其中 $-\\infty<x_n<+\\infty$；  \n② 当 $\\lim_{n\\to\\infty}\\cos(\\tan x_n)$ 存在时，$\\lim_{n\\to\\infty}x_n$ 存在，其中 $-\\frac{\\pi}{2}<x_n<\\frac{\\pi}{2}$；  \n③ 当 $\\lim_{n\\to\\infty}\\sin(\\arctan x_n)$ 存在时，$\\lim_{n\\to\\infty}x_n$ 存在，其中 $-\\infty<x_n<+\\infty$；  \n④ 当 $\\lim_{n\\to\\infty}\\sin(\\tan x_n)$ 存在时，$\\lim_{n\\to\\infty}x_n$ 存在，其中 $-\\frac{\\pi}{2}<x_n<\\frac{\\pi}{2}$。\n\n正确结论的个数为（　）。\n\nA. 0  \nB. 1  \nC. 2  \nD. 3\n\n3\\. 设函数 $y=f(x)$ 由 $\\begin{cases}x=2t+|t|,\\\\y=|t|(\\mathrm e^t-1)\\end{cases}$ 确定，则（　）。\n\nA. $f(x)$ 连续，$f'(0)$ 不存在。  \nB. $f'(0)$ 存在，$f'(x)$ 在 $x=0$ 处不连续。  \nC. $f'(x)$ 连续，$f''(0)$ 不存在。  \nD. $f''(0)$ 存在，$f''(x)$ 在 $x=0$ 处不连续。\n\n4\\. 设 $I_1=\\int_0^1\\frac{x}{\\sqrt{1-x^2}}\\,\\mathrm dx$，$I_2=\\int_0^1\\frac{\\cos x}{\\sqrt{1-x^2}}\\,\\mathrm dx$，$I_3=\\int_0^1\\frac{\\sin x}{\\sqrt{1-x^2}}\\,\\mathrm dx$，则（　）。\n\nA. $I_1<I_2<I_3$  \nB. $I_2<I_3<I_1$  \nC. $I_3<I_1<I_2$  \nD. $I_2<I_1<I_3$\n\n5\\. 一个直径为 $20\\,\\mathrm m$ 的倒圆锥形水池，深 $a\\,\\mathrm m$，水密度为 $\\rho\\,\\mathrm{kg/m^3}$，重力加速度为 $g\\,\\mathrm{m/s^2}$，若将盛满的水全部抽出，至少需做功 $75\\rho g\\pi\\,\\mathrm J$，则 $a=$（　）。\n\nA. 15  \nB. 9  \nC. 5  \nD. 3\n\n6\\. 设 $z=z(x,y)$ 是由方程 $\\int_{2x-3y}^z f(2x-3y+z-t)\\,\\mathrm dt=\\sin(2x-3y+z)$ 所确定的函数，其中 $f$ 为大于 1 的连续函数，则（　）。\n\nA. $3\\frac{\\partial z}{\\partial x}+2\\frac{\\partial z}{\\partial y}=0$  \nB. $3\\frac{\\partial z}{\\partial x}-2\\frac{\\partial z}{\\partial y}=0$  \nC. $2\\frac{\\partial z}{\\partial x}+3\\frac{\\partial z}{\\partial y}=0$  \nD. $2\\frac{\\partial z}{\\partial x}-3\\frac{\\partial z}{\\partial y}=0$\n\n7\\. 设 $a$ 与 $b$ 都是常数，若反常积分 $\\int_0^{+\\infty}\\frac{x^a(1-\\mathrm e^{-x})}{(1+x)^b}\\,\\mathrm dx$ 收敛，则 $a$ 与 $b$ 的取值范围为（　）。\n\nA. $a<-2,b>a+1$  \nB. $a>-2,b>a+1$  \nC. $a>-2,b<a+1$  \nD. $a<-2,b<a+1$\n\n8\\. 已知 $\\alpha_1=(1,2)^T$，$\\alpha_2=(a,1)^T$，$x=(x_1,x_2)^T$。若二次型 $f(x_1,x_2)=\\sum_{i=1}^2[\\alpha_i,x]^2$ 正定，其中 $[\\alpha_i,x]$ 表示向量 $\\alpha_i,x$ 的内积（$i=1,2$），则 $a$ 的取值范围是（　）。\n\nA. $\\left(-\\infty,\\frac12\\right)\\cup\\left(\\frac12,+\\infty\\right)$  \nB. $\\left(-\\infty,-\\frac12\\right)\\cup\\left(-\\frac12,+\\infty\\right)$  \nC. $\\left(-\\frac12,\\frac12\\right)$  \nD. $\\left\\{\\frac12\\right\\}$\n\n9\\. 下列矩阵中，可以经过若干次初等行变换得到矩阵 $\\begin{pmatrix}1&1&0&1\\\\0&1&0&0\\\\0&0&0&0\\end{pmatrix}$ 的是（　）。\n\nA. $\\begin{pmatrix}1&1&0&1\\\\1&2&1&3\\\\2&3&1&4\\end{pmatrix}$  \nB. $\\begin{pmatrix}1&1&0&1\\\\1&1&2&5\\\\1&1&1&3\\end{pmatrix}$  \nC. $\\begin{pmatrix}1&0&0&1\\\\0&1&0&3\\\\0&1&0&0\\end{pmatrix}$  \nD. $\\begin{pmatrix}1&1&0&1\\\\1&2&0&1\\\\2&3&0&2\\end{pmatrix}$\n\n10\\. 设 $A$ 为 2 阶方阵，$\\alpha$ 为 2 维非零列向量，且 $\\alpha$ 不是 $A$ 的特征向量，$P=(\\alpha,A\\alpha)$，$A^2\\alpha+A\\alpha-2\\alpha=0$，若矩阵 $B$ 满足 $AP=PB$，则 $B=$（　）。\n\nA. $\\begin{pmatrix}-1&0\\\\1&2\\end{pmatrix}$  \nB. $\\begin{pmatrix}0&2\\\\1&-1\\end{pmatrix}$  \nC. $\\begin{pmatrix}-1&1\\\\0&2\\end{pmatrix}$  \nD. $\\begin{pmatrix}0&1\\\\1&-1\\end{pmatrix}$\n\n### 填空题\n\n11\\. $\\lim_{x\\to+\\infty}x^2\\left[\\left(1+\\frac1{x+1}\\right)^{x+1}-\\left(1+\\frac1x\\right)^x\\right]=$ ______。\n\n12\\. 微分方程 $3(x+y-1)\\,\\mathrm dx+(x+y)\\,\\mathrm dy=0$ 的通解为 ______。\n\n13\\. $\\int\\frac{x^3\\arccos x}{\\sqrt{1-x^2}}\\,\\mathrm dx=$ ______。\n\n14\\. 设连续函数 $f(x)$ 满足 $f(x+1)-f(x)=x^2$，$\\int_0^1 f(x)\\,\\mathrm dx=0$，则 $\\int_1^2 f(x)\\,\\mathrm dx=$ ______。\n\n15\\. 由 $\\begin{cases}x=1-\\cos t,\\\\y=t-\\sin t\\end{cases}$（$0\\le t\\le2\\pi$），$x=0$ 所围成的平面图形 $D$ 的形心横坐标等于 ______。\n\n16\\. 设方程组 $\\begin{cases}\\lambda x_1+x_2+x_3=a,\\\\(\\lambda-1)x_2=1,\\\\x_1+x_2+\\lambda x_3=1\\end{cases}$ 有两个不同的解，则该方程组的通解为 ______。\n\n### 解答题\n\n17\\. （10 分）计算 $\\lim_{n\\to\\infty}\\sum_{k=1}^n\\frac{k}{n^2}\\ln\\left(1+\\frac{k^2}{n^2}\\right)$。\n\n18\\. （12 分）设函数 $f(x)$ 在 $x=0$ 处连续，且\n\n$$\n\\lim_{x\\to0}\\frac{xf(x)-\\mathrm e^{2\\ln(1+x)}+1}{x[(1+x)^{1/x}-\\mathrm e]}=-\\frac2{\\mathrm e},\n$$\n\n证明 $f(x)$ 在 $x=0$ 处可导，并求 $f'(0)$。\n\n19\\. （12 分）设 $f(x)$ 是 $[0,1]$ 上的正值连续函数，证明：\n\n（Ⅰ）存在唯一的 $\\xi\\in(0,1)$，使得 $\\int_0^\\xi f(t)\\,\\mathrm dt=\\int_\\xi^1\\frac1{f(t)}\\,\\mathrm dt$；\n\n（Ⅱ）对任意自然数 $n$（$n\\ge2$），存在唯一的 $x_n\\in(0,1)$，使得 $\\int_{1/n}^{x_n}f(t)\\,\\mathrm dt=\\int_{x_n}^1\\frac1{f(t)}\\,\\mathrm dt$，且 $\\lim_{n\\to\\infty}x_n=\\xi$。\n\n20\\. （12 分）设平面区域 $D=\\{(x,y)\\mid x-2\\le y\\le\\sqrt{4-x^2},\\,0\\le x\\le2\\}$，计算 $I=\\iint_D\\frac{|x-y|}{x^2+y^2}\\,\\mathrm dx\\,\\mathrm dy$。\n\n21\\. （12 分）设过点 $(0,1)$ 的曲线，其上任意点 $P$ 处的切线在 $y$ 轴上的截距等于原点到点 $P$ 的距离，求该曲线方程。\n\n22\\. （12 分）设 4 阶实矩阵 $A$ 与 4 维列向量 $\\alpha,\\beta$ 满足 $A(\\alpha+\\beta)=4\\alpha+3\\beta$，$A(\\alpha-\\beta)=2\\alpha-3\\beta$，$\\alpha,\\beta$ 线性无关。方程组 $Ax=0$ 有两个线性无关的解向量 $\\eta_1,\\eta_2$。\n\n（Ⅰ）证明 $\\alpha,\\beta,\\eta_1,\\eta_2$ 线性无关；\n\n（Ⅱ）判断矩阵 $A$ 与 $\\begin{pmatrix}3&1&0&0\\\\0&3&0&0\\\\0&0&0&0\\\\0&0&0&0\\end{pmatrix}$ 是否相似，并说明理由。\n## 卷三· 张宇四套卷（3）\n\n### 选择题\n\n1\\. 设 $f(x)=\\int_0^x(x-2t)\\mathrm e^{-t^2}\\,\\mathrm dt$（$x\\ge0$），$g(x)=\\int_0^x(x-2t)\\sin t^2\\,\\mathrm dt$，则（　）。\n\nA. $f(x)$ 单调增加，$g(x)$ 是奇函数。  \nB. $f(x)$ 单调增加，$g(x)$ 是偶函数。  \nC. $f(x)$ 单调减少，$g(x)$ 是奇函数。  \nD. $f(x)$ 单调减少，$g(x)$ 是偶函数。\n\n2\\. 设函数 $f(x)$ 在 $[0,1]$ 上二阶可导，则（　）。\n\nA. 当 $f'(x)<0$ 时，$f\\left(\\frac12\\right)<\\int_0^1f(x)\\,\\mathrm dx$。  \nB. 当 $f'(x)>0$ 时，$f\\left(\\frac12\\right)<\\int_0^1f(x)\\,\\mathrm dx$。  \nC. 当 $f''(x)<0$ 时，$f\\left(\\frac13\\right)<\\int_0^1f(x^2)\\,\\mathrm dx$。  \nD. 当 $f''(x)>0$ 时，$f\\left(\\frac13\\right)<\\int_0^1f(x^2)\\,\\mathrm dx$。\n\n3\\. 设 $f'(x)>0$，$f''(x)<0$，$x>0$，对任意的正整数 $n$，记\n\n$$\nI_1=\\frac12[f(n+1)-f(n)],\\quad\nI_2=f(n)-f\\left(\\frac{2n-1}{2}\\right),\\quad\nI_3=f\\left(\\frac{2n+1}{2}\\right)-f(n),\n$$\n\n则（　）。\n\nA. $I_1>I_2>I_3$  \nB. $I_1>I_3>I_2$  \nC. $I_2>I_1>I_3$  \nD. $I_2>I_3>I_1$\n\n4\\. 圆 $r=1$ 之外和圆 $r=\\frac2{\\sqrt3}\\cos\\theta$ 之内的公共部分面积表示为（　）。\n\nA. $\\int_0^{\\pi/6}\\mathrm d\\theta\\int_0^{\\frac2{\\sqrt3}\\cos\\theta}r\\,\\mathrm dr$  \nB. $2\\int_0^{\\pi/6}\\mathrm d\\theta\\int_0^{\\frac2{\\sqrt3}\\cos\\theta}r\\,\\mathrm dr$  \nC. $2\\int_0^{\\pi/6}\\mathrm d\\theta\\int_1^{\\frac2{\\sqrt3}\\cos\\theta}r\\,\\mathrm dr$  \nD. $\\int_0^{\\pi/6}\\mathrm d\\theta\\int_1^{\\frac2{\\sqrt3}\\cos\\theta}r\\,\\mathrm dr$\n\n5\\. 边长为 1 的正方形闸门铅直放置于水中，顶边与水面相平，一条对角线将闸门分成两个三角形区域，则两个三角形区域上所受水压力之比可以为（　）。\n\nA. $\\frac{\\sqrt2}{2}$  \nB. $\\frac{\\sqrt3}{3}$  \nC. $2$  \nD. $\\frac32$\n\n6\\. 已知数列 $\\{x_n\\},\\{y_n\\}$，且 $x_1=y_1=k$，$0<k<1$，$x_{n+1}=x_n^2$，$y_{n+1}=\\sin y_n$（$n=1,2,\\ldots$），则当 $n\\to\\infty$ 时，（　）。\n\nA. $x_n$ 是 $y_n$ 的高阶无穷小。  \nB. $y_n$ 是 $x_n$ 的高阶无穷小。  \nC. $x_n$ 与 $y_n$ 是等价无穷小。  \nD. $x_n$ 与 $y_n$ 是同阶但不等价的无穷小。\n\n7\\. 设 $f(1)=1$，$f'(1)=2$，则 $\\lim_{x\\to1}\\frac{\\ln f[\\cos(x-1)-\\sin(x-1)]}{\\ln x}=$（　）。\n\nA. $-2$  \nB. $2$  \nC. $-\\mathrm e$  \nD. $\\mathrm e$\n\n8\\. 设 $n$ 阶矩阵 $A,B,C$ 满足 $r(ABC)+2n=r(A)+r(B)+r(C)$，则（　）。\n\nA. $r(A)+r(B)+r(C)=r(AB)$  \nB. $r(AB)+n=r(A)+r(B)$  \nC. $r(ABC)>r(A)+r(BC)-n$  \nD. $r(AB)=r(BC)=n$\n\n9\\. 设矩阵 $\\begin{pmatrix}1&2&0\\\\2&a&1\\\\0&1&b\\end{pmatrix}$ 有 2 个正特征值和 1 个负特征值，则（　）。\n\nA. $a>4,b>1$  \nB. $a<4,b>1$  \nC. $(a-4)b>1$  \nD. $(a-4)b<1$\n\n10\\. 设向量组 $B\\colon\\beta_1,\\beta_2,\\ldots,\\beta_r$ 能由向量组 $A\\colon\\alpha_1,\\alpha_2,\\ldots,\\alpha_s$ 线性表示为\n\n$$\n\\begin{pmatrix}\\beta_1\\\\\\beta_2\\\\\\vdots\\\\\\beta_r\\end{pmatrix}\n=P\\begin{pmatrix}\\alpha_1\\\\\\alpha_2\\\\\\vdots\\\\\\alpha_s\\end{pmatrix},\n$$\n\n其中 $P$ 为 $r\\times s$ 矩阵，且向量组 $A$ 线性无关，则向量组 $B$ 线性无关是 $r(P)=r$ 的（　）。\n\nA. 充分非必要条件。  \nB. 必要非充分条件。  \nC. 充分必要条件。  \nD. 既非充分也非必要条件。\n\n### 填空题\n\n11\\. 设 $y=\\tan^n x$（$n\\ge1$）在 $x=\\frac{\\pi}{4}$ 处的切线在 $x$ 轴上的截距为 $x_n$，则 $\\lim_{n\\to\\infty}y(x_n)=$ ______。\n\n12\\. $\\int_{-\\pi}^{\\pi}(x+\\cos x)^3\\,\\mathrm dx=$ ______。\n\n13\\. 设 $u=z\\mathrm e^{x/y}\\sin(x^2+y^2)$，其中 $z=z(x,y)$ 是由方程 $3x^2+2y^2+2z=7$ 确定的隐函数，则 $\\left.\\frac{\\partial u}{\\partial x}\\right|_{(1,1)}=$ ______。\n\n14\\. 曲线 $x=\\int_{-\\sqrt3}^y\\sqrt{3-t^2}\\,\\mathrm dt$ 的弧长为 ______。\n\n15\\. 已知函数 $y=y(x)$ 由 $\\begin{cases}x=\\sin t,\\\\2t-\\int_1^{y+t^2}\\mathrm e^{-u^2}\\,\\mathrm du=0\\end{cases}$ 确定，则 $\\left.\\frac{\\mathrm dy}{\\mathrm dx}\\right|_{t=0}=$ ______。\n\n16\\. 已知 $A,B$ 均为 3 阶方阵，且满足 $ABA+AB^2=-2E$，$\\lambda_1=1,\\lambda_2=-2,\\lambda_3=-1$ 为 $A$ 的三个特征值，则 $|AB+B^2|=$ ______。\n\n### 解答题\n\n17\\. （10 分）求函数 $z=\\cos^2 x+\\cos^2 y$ 在条件 $x-y=\\frac{\\pi}{4}$ 下的极值。\n\n18\\. （12 分）设 $f(x)$ 在 $[0,1]$ 上可导，$F(x)$ 是 $f(x)$ 的一个原函数，且 $F(0)=0$。若 $\\int_0^1f(x)\\,\\mathrm dx=\\int_0^1F(x)\\,\\mathrm dx=0$，证明：\n\n（Ⅰ）$\\int_0^1xf(x)\\,\\mathrm dx=0$；\n\n（Ⅱ）存在 $\\xi\\in(0,1)$，使得 $f'(\\xi)=0$。\n\n19\\. （12 分）设 $u=\\frac{x}{y}$，$v=x$，$w=xz-y$，$z=z(x,y)$ 具有二阶连续偏导数。\n\n（Ⅰ）将函数 $z=z(x,y)$ 的方程 $y\\frac{\\partial^2z}{\\partial y^2}+x\\frac{\\partial^2z}{\\partial x\\partial y}+2\\frac{\\partial z}{\\partial y}=\\frac1x-\\frac{x}{y}$ 化为 $w=w(u,v)$ 的方程；\n\n（Ⅱ）若 $w'_u(u,0)=1$，$w(1,v)=v^2$，求 $w=w(u,v)$ 的表达式。\n\n20\\. （12 分）设 $f(x,y)$ 连续，且 $f(x,y)=\\frac1{\\sqrt{|x^2+y^2-2|+2}}+\\frac1\\pi\\iint_D f(x,y)\\,\\mathrm d\\sigma$，其中 $D=\\{(x,y)\\mid0\\le y\\le\\sqrt{2x-x^2}\\}$，试求 $\\iint_D f(x,y)\\,\\mathrm d\\sigma$。\n\n21\\. （12 分）设一光滑曲线在第一象限内且过坐标原点 $O$，曲线上任意一点 $M$ 处的切线 $MT$ 交 $x$ 轴于点 $T$，$MP\\perp x$ 轴于点 $P$。若三角形 $MPT$ 的面积与曲边三角形 $OMP$ 的面积之比恒为常数 $k$（$k>\\frac12$），且曲线是沿 $x$ 轴正向单调增加的，求该曲线的方程。\n\n22\\. （12 分）设矩阵 $A=\\begin{pmatrix}0&-1&2&0&-1\\\\-1&0&-2&-a&-1\\\\2&1&a+1&2&3\\end{pmatrix}$，$B=\\begin{pmatrix}0&-1\\\\-1&0\\\\2&1\\end{pmatrix}$，$A=BC$。\n\n（Ⅰ）求 $a$ 的值及 $C$；\n\n（Ⅱ）求 $Ax=0$ 的通解。\n## 卷四· 张宇四套卷（4）\n\n### 选择题\n\n1\\. 若函数 $f(x)=\\begin{cases}\\frac{1-\\cos\\sqrt x}{a\\ln(1+x)},&x>0,\\\\b,&x\\le0\\end{cases}$ 在 $x=0$ 处连续，则（　）。\n\nA. $ab=\\frac12$  \nB. $ab=-\\frac12$  \nC. $ab=0$  \nD. $ab=2$\n\n2\\. 某质点作直线运动，在 $t$ 时刻的位移为 $x=t^3$。已知介质的阻力大小与质点速度的平方成正比，比例系数为 $k$（$k>0$），则质点从 $x=0$ 运动到 $x=1$ 克服介质阻力做功的大小为（　）。\n\nA. $\\frac92k$  \nB. $\\frac{13}{6}k$  \nC. $\\frac{27}{7}k$  \nD. $\\frac{13}{7}k$\n\n3\\. 已知函数 $f(x)=\\int_0^x\\mathrm e^{t^2}\\cos t\\,\\mathrm dt$，$g(x)=\\int_0^x\\mathrm e^{t^2}\\cos^2x\\,\\mathrm dt$，则（　）。\n\nA. $x=\\frac{\\pi}{2}$ 是 $f(x)$ 的极值点，$\\left(\\frac{\\pi}{2},f\\left(\\frac{\\pi}{2}\\right)\\right)$ 是曲线 $y=f(x)$ 的拐点。  \nB. $\\left(\\frac{\\pi}{2},f\\left(\\frac{\\pi}{2}\\right)\\right)$ 是曲线 $y=f(x)$ 的拐点，$\\left(\\frac{\\pi}{2},0\\right)$ 是曲线 $y=g(x)$ 的拐点。  \nC. $x=\\frac{\\pi}{2}$ 是 $f(x)$ 的极大值点，是 $g(x)$ 的极大值点。  \nD. $x=\\frac{\\pi}{2}$ 是 $f(x)$ 的极大值点，是 $g(x)$ 的极小值点。\n\n4\\. 已知 $y_1=x\\mathrm e^x+\\mathrm e^{2x}$ 和 $y_2=x\\mathrm e^x+\\mathrm e^{-x}$ 是二阶常系数非齐次线性微分方程的两个解，则此方程为（　）。\n\nA. $y''-y'+2y=\\mathrm e^x+2x\\mathrm e^x$  \nB. $y''-y'-2y=\\mathrm e^x-2x\\mathrm e^x$  \nC. $y''-y'+2y=\\mathrm e^{2x}-\\mathrm e^{-x}$  \nD. $y''-y'-2y=x\\mathrm e^x+\\mathrm e^{2x}$\n\n5\\. 设 $f(x)=\\frac{x^2}{\\mathrm e^x-1}$ 在 $x=0$ 处的 3 次泰勒多项式为 $ax^3+bx^2+cx$，则 $(a,b,c)=$（　）。\n\nA. $\\left(\\frac1{12},-\\frac12,1\\right)$  \nB. $\\left(-\\frac1{12},\\frac12,1\\right)$  \nC. $\\left(\\frac1{12},\\frac12,-1\\right)$  \nD. $\\left(-\\frac1{12},-\\frac12,1\\right)$\n\n6\\. 设 $f(x,y)=\\begin{cases}\\sin x\\cos y,&x\\ne0,\\\\1-\\cos y,&x=0,\\end{cases}$ 则（　）。\n\nA. $f'_x(0,0)=0$  \nB. $\\lim_{x\\to0}\\lim_{y\\to0} f(x,y)=0$  \nC. $f''_{yx}(0,0)=1$  \nD. $f'_y(0,0)=1$\n\n7\\. 设 $D=\\{(x,y)\\mid |x|\\le1,\\,0\\le y\\le2\\}$，则 $\\iint_D\\sqrt{|y-x^2|}\\,\\mathrm d\\sigma=$（　）。\n\nA. $\\frac\\pi2+\\frac53$  \nB. $\\frac\\pi2+\\frac73$  \nC. $\\frac\\pi4+\\frac53$  \nD. $\\frac\\pi4+\\frac73$\n\n8\\. $\\alpha,\\beta$ 是 2 阶实矩阵 $A$ 的两个实特征向量，$\\|\\alpha+\\beta\\|=\\|\\alpha-\\beta\\|$，则矩阵 $A$ 必为（　）。\n\nA. 正定矩阵。  \nB. 正交矩阵。  \nC. 对称矩阵。  \nD. 单位矩阵。\n\n9\\. 二次型 $f(x_1,x_2,x_3)=x_1^2+2x_1x_2+2x_1x_3$ 的符号差（正惯性指数 $-$ 负惯性指数）为（　）。\n\nA. $-1$  \nB. $0$  \nC. $1$  \nD. $2$\n\n10\\. 若矩阵 $A=(a_{ij})_{n\\times n}$，对 $i=1,2,\\ldots,n$，均有 $|a_{ii}|>\\sum_{j\\ne i}|a_{ij}|$，其中 $|a_{ij}|$ 表示元素 $a_{ij}$ 的绝对值，$\\beta$ 为任一 $n$ 维列向量，则（　）。\n\nA. $Ax=0$ 有非零解。  \nB. $Ax=0$ 不一定有非零解。  \nC. $Ax=\\beta$ 不一定有解。  \nD. $Ax=\\beta$ 有唯一解。\n\n### 填空题\n\n11\\. 设函数 $z=z(x,y)$ 由 $\\mathrm e^z+yz=2y-x$ 确定，则 $\\left.\\frac{\\partial^2z}{\\partial y^2}\\right|_{(1,1)}=$ ______。\n\n12\\. 曲线 $y=\\sqrt[3]{x^3-2x^2+1}$ 的斜渐近线方程为 ______。\n\n13\\. 抛物线 $y^2=2x$（$0\\le x\\le h$）绕 $x$ 轴旋转一周所得旋转曲面的面积为 ______。\n\n14\\. 已知函数 $y(x)$ 由方程 $\\int_0^y\\mathrm e^t\\,\\mathrm dt+\\int_0^x\\cos t\\,\\mathrm dt=0$ 确定，则 $\\frac{\\mathrm d^2y}{\\mathrm dx^2}=$ ______。\n\n15\\. 设过点 $(0,1)$ 的曲线 $y=y(x)$ 满足 $y''=x$，且在点 $(0,1)$ 处与直线 $y=\\frac x2+1$ 相切，则该曲线的方程为 ______。\n\n16\\. 设 $\\alpha_1,\\alpha_2,\\alpha_3,\\alpha_4$ 是四元非齐次线性方程组 $Ax=b$ 的 4 个解向量，且 $\\alpha_1+\\alpha_2=(2,4,6,8)^T$，$\\alpha_2+\\alpha_3+\\alpha_4=(3,5,7,9)^T$，$\\alpha_1+2\\alpha_2-\\alpha_3=(2,0,0,2)^T$，若秩 $r(A)=2$，则方程组 $Ax=b$ 的通解是 ______。\n\n### 解答题\n\n17\\. （10 分）计算 $\\int\\frac{x^3+1}{x^4+2x^2+1}\\,\\mathrm dx$。\n\n18\\. （12 分）求函数 $F(x)=\\int_x^{x+1}|t(t^2-1)|\\,\\mathrm dt$ 的最小值。\n\n19\\. （12 分）设 $f(x)$ 在 $[0,1]$ 上具有三阶连续导数，$f'(0)=f''(0)=0$，证明存在 $\\xi,\\eta,\\zeta\\in(0,1)$，使得 $\\mathrm e^\\xi f'''(\\eta)=6\\mathrm e^\\zeta f'(\\xi)$。\n\n20\\. （12 分）求函数 $z=\\mathrm e^{2x+3y}(8x^2-6xy+3y^2)$ 的极值。\n\n21\\. （12 分）已知平面有界区域 $D=\\{(r,\\theta)\\mid r\\le4\\cos\\theta,\\,r\\le4\\sin\\theta\\}$，计算 $\\iint_D r^3(\\sin\\theta-\\cos\\theta)^2\\,\\mathrm dr\\,\\mathrm d\\theta$。\n\n22\\. （12 分）已知矩阵 $A=\\begin{pmatrix}4&1&-2\\\\1&1&1\\\\-2&1&a\\end{pmatrix}$ 与 $B=\\begin{pmatrix}k&0&0\\\\0&6&0\\\\0&0&0\\end{pmatrix}$ 合同但不相似。\n\n（1）求 $a$ 的值及 $k$ 的取值范围；\n\n（2）若存在可逆矩阵 $Q$，使得 $Q^TAQ=B$，求 $Q$。\n"}

## tool · 2026-11-12T01:33:18Z


Script completed
Wall time 0.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/d78e17555a363f2b5f2a4a8b193de0ebf5fa21de6200fa19e52374cc75873dec.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/6f668be56f43742fdaa00306ada0425ef7a960bfb835f0319d1df97ca0346219.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/f1502416689aab1f8de5a625defdfdc5a83ffa9626b6e04ae00b82eb2e55ef5c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/9036fcfea69270b26daf9ece53c7424f19651d731259cdd99ed39a1488622702.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/9e90e44e953037963907e519f5e07f7df057937e34b645264a153a5b09975dc7.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/9743ba942583191c2a9a0b0fadbc3e0b40d72011273256436e0439c42677dab8.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/7de034c4f0cd852f3a2542cc25ae9779c1018f59b8f55b1a816ddb8decfccc24.png",
  "detail": "high"
}
{"chunk_id":"065428","wall_time_seconds":0.0000095,"exit_code":0,"original_token_count":2832,"output":"## 卷五· 李林四套卷（1）\n\n### 选择题\n\n1\\. 设 $f(x)$ 在 $(-\\infty,+\\infty)$ 内有二阶连续导数，且满足 $f\\left(\\frac1n\\right)=\\frac{n^2}{n^2+1}$（$n=1,2,\\ldots$），则 $f(x)$ 在 $x=0$ 处的二次泰勒多项式为（　）。\n\nA. $1-2x^2$  \nB. $x-2x^2$  \nC. $1-x^2$  \nD. $1+x-x^2$\n\n2\\. 设 $f(x)$ 在 $[0,a]$（$a>0$）上有二阶连续导数，且 $f(0)=f'(0)=0$，$f''(x)$ 严格单调递增，则（　）。\n\nA. $4\\int_0^a xf(x)\\,\\mathrm dx<3a\\int_0^a f(x)\\,\\mathrm dx$  \nB. $4\\int_0^a xf(x)\\,\\mathrm dx>3a\\int_0^a f(x)\\,\\mathrm dx$  \nC. $3\\int_0^a xf(x)\\,\\mathrm dx>4a\\int_0^a f(x)\\,\\mathrm dx$  \nD. $3\\int_0^a xf(x)\\,\\mathrm dx<4a\\int_0^a f(x)\\,\\mathrm dx$\n\n3\\. 设 $f(x,y)=\\begin{cases}\\frac{2x|y|}{\\sqrt{x^2+y^2}},&x^2+y^2\\ne0,\\\\0,&x^2+y^2=0.\\end{cases}$ 若 $z=f(\\tan t,\\ln(1+t))$，则 $\\left.\\frac{\\mathrm dz}{\\mathrm dt}\\right|_{t=0}=$（　）。\n\nA. $0$  \nB. $1$  \nC. $2$  \nD. $\\sqrt2$\n\n4\\. 已知积分 $I=\\int_2^{+\\infty}\\left(\\mathrm e^{\\frac{\\ln x}{x^a}}-1\\right)\\,\\mathrm dx$ 收敛，则 $a$ 的取值范围为（　）。\n\nA. $(-\\infty,0)$  \nB. $(0,1]$  \nC. $(1,+\\infty)$  \nD. $[1,+\\infty)$\n\n5\\. 设 $a>0,b\\ne0$，$\\lim_{x\\to+\\infty}x^a\\ln\\frac{\\arctan(x+1)}{\\arctan x}=b$，则（　）。\n\nA. $a=1,b=\\frac{\\pi}{2}$  \nB. $a=1,b=\\frac2\\pi$  \nC. $a=2,b=\\frac{\\pi}{2}$  \nD. $a=2,b=\\frac2\\pi$\n\n6\\. 设方程 $x^n+nx=k$（$n=1,2,\\ldots$）在 $x\\in(0,+\\infty)$ 内的实根为 $x_n$，其中 $k>0$，则 $\\lim_{n\\to\\infty}(1+x_n)^n=$（　）。\n\nA. $\\mathrm e$  \nB. $\\mathrm e^k$  \nC. $\\mathrm e^{-k}$  \nD. $\\mathrm e^{-1}$\n\n7\\. 设 $f(t)$ 可微，$z=xyf\\left(\\frac yx\\right)$ 满足 $x\\frac{\\partial z}{\\partial x}+y\\frac{\\partial z}{\\partial y}=xy\\frac yx$，则 $\\left.\\mathrm dz\\right|_{(1,1)}=$（　）。\n\nA. $\\mathrm dx+\\mathrm dy$  \nB. $-\\mathrm dx+\\mathrm dy$  \nC. $\\frac12\\,\\mathrm dx+\\frac12\\,\\mathrm dy$  \nD. $-\\frac12\\,\\mathrm dx+\\frac12\\,\\mathrm dy$\n\n8\\. 设 $f(x)$ 二阶可导，$f''(x)\\ne0$，$(a,f(a)),(b,f(b)),(c,f(c))$ 为曲线 $y=f(x)$ 上三个不同的点，则方程组\n\n$$\n\\begin{cases}\nx_1+ax_2+f(a)x_3=f(b)\\\\\nx_1+bx_2+f(b)x_3=f(c)\\\\\nx_1+cx_2+f(c)x_3=f(a)\n\\end{cases}\n$$\n\n（　）。\n\nA. 有唯一解。  \nB. 有无穷多解。  \nC. 无解。  \nD. 无法确定是否有解。\n\n9\\. 设 $A=\\begin{bmatrix}1&1&0\\\\1&1&0\\\\0&0&1\\end{bmatrix}$，则下列矩阵中与 $A$ 既不相似也不合同的是（　）。\n\nA. $\\begin{bmatrix}3&0&0\\\\0&2&0\\\\0&0&0\\end{bmatrix}$  \nB. $\\begin{bmatrix}1&2&1\\\\2&5&2\\\\1&2&1\\end{bmatrix}$  \nC. $\\begin{bmatrix}1&-1&0\\\\-1&1&0\\\\0&0&1\\end{bmatrix}$  \nD. $\\begin{bmatrix}1&0&0\\\\0&1&0\\\\0&0&-1\\end{bmatrix}$\n\n10\\. 设 $\\alpha$ 为 3 维单位列向量，$A=E-2\\alpha\\alpha^T$，$E$ 为 3 阶单位矩阵，$A^*$ 是 $A$ 的伴随矩阵，则二次型 $X^TA^*X$ 的规范形为（　）。\n\nA. $y_1^2-y_2^2-y_3^2$  \nB. $y_1^2+y_2^2-y_3^2$  \nC. $y_1^2+y_2^2+y_3^2$  \nD. $-y_1^2-y_2^2-y_3^2$\n\n### 填空题\n\n11\\. 设 $f(x)$ 在 $x=0$ 处连续，且 $\\lim_{x\\to0}[f(x)+\\mathrm e^x]^{1/x}=2$，则 $\\lim_{n\\to\\infty}2nf\\left(\\frac1n\\right)=$ ______。\n\n12\\. 设曲线 $y=\\int_0^{x/n}n\\sqrt{\\sin t}\\,\\mathrm dt$（$n$ 为正整数）在 $[0,n\\pi]$ 上的全长为 $S_n$，则 $\\lim_{n\\to\\infty}\\frac{S_n}{n+1}=$ ______。\n\n13\\. 当 $x\\to0$ 时，微分方程 $(3x^2+2)y''=6xy'$ 的解 $y(x)$ 与 $x$ 是等价无穷小，则 $y(x)=$ ______。\n\n14\\. 设 $y=f(x)$ 由方程 $\\arctan\\frac xy=\\ln\\sqrt{\\frac{x^2+y^2}{2}}+\\frac\\pi4$ 确定，则曲线 $y=f(x)$ 在点 $(1,1)$ 处的曲率半径为 ______。\n\n15\\. $\\lim_{n\\to\\infty}\\sum_{k=1}^n\\left[\\frac{k}{2n^2+k}+\\ln\\left(\\frac{n+k}{n}\\right)^{1/n}\\right]=$ ______。\n\n16\\. 设 3 阶行列式 $|A|=1$，将 $A$ 的第 1 列加到第 2 列得 $B$，则行列式 $|A^{-1}+B^*|=$ ______。\n\n### 解答题\n\n17\\. （10 分）计算 $\\lim_{x\\to1^-}\\frac{\\pi\\int_0^x[\\ln(1-t)+\\tan\\frac{\\pi}{2}t]\\,\\mathrm dt}{\\ln|\\sin\\pi x|}$。\n\n18\\. （12 分）设 $g(t)$ 满足 $g'(t)-g(t)\\ln\\left(1+\\frac1{2t}\\right)=-\\frac{g(t)}{2t+1}$，$g(1)=\\frac32$。$f(x)=\\int_x^{x^2}g(t)\\tan\\frac1{\\sqrt t}\\,\\mathrm dt$（$x>0$）。\n\n（Ⅰ）求 $g(t)$；\n\n（Ⅱ）求 $\\lim_{n\\to\\infty}\\frac{f(n)}{n}$。\n\n19\\. （12 分）设 $D=\\{(x,y)\\mid1\\le x+y\\le2,\\,x\\ge0,\\,y\\ge0\\}$。计算 $I=\\iint_D\\mathrm e^{(x+y)^2}(\\sin^2x+\\cos^2y)\\,\\mathrm dx\\,\\mathrm dy$。\n\n20\\. （12 分）设 $f(x)$ 有二阶连续偏导数，且满足\n\n$$\n\\mathrm df(x,y)=(2ax+2y)\\,\\mathrm dx+(2x+2by)\\,\\mathrm dy,\\qquad f(1,1)=a+b+2.\n$$\n\n（Ⅰ）求 $f(x,y)$；\n\n（Ⅱ）记原点到曲线 $f(x,y)=1$ 上任一点距离为 $d$，若 $d$ 在点 $\\left(\\frac12,-\\frac12\\right)$ 处取得最大值，求 $a,b$ 的值。\n\n21\\. （12 分）设 $f(x)$ 在 $x\\in[0,1]$ 上有二阶连续导数，$f(0)=f(1)$，$0<f(x)<1$，$|f''(x)|<2$。\n\n（Ⅰ）证明当 $x\\in[0,1]$ 时，有 $|f'(x)|<1$；\n\n（Ⅱ）设 $x_0\\in(0,1)$，数列 $\\{x_n\\}$ 满足 $2x_{n+1}=x_n+f(x_n)$（$n=0,1,2,\\ldots$）。证明 $\\lim_{n\\to\\infty}x_n$ 存在。\n\n22\\. （12 分）设 $A=\\begin{bmatrix}0&2&3\\\\2&2&a\\\\2&3&4\\end{bmatrix}$，3 阶实对称矩阵 $B$ 满足 $AB+B=A+E$，$B\\ne E$，其中 $E$ 为单位矩阵，且 $r(A+B)=3$。\n\n（Ⅱ）求 $a$ 的值；\n\n（Ⅱ）求所有满足题干的矩阵 $B$；\n\n（Ⅲ）求可逆矩阵 $P$ 及对角矩阵 $\\Lambda$，使得 $P^{-1}BP=\\Lambda$。\n## 卷六· 李林四套卷（2）\n\n### 选择题\n\n1\\. 设 $\\lim_{x\\to\\infty}f'(x)=0$，且 $\\lim_{x\\to\\infty}\\left(\\frac{ax^2}{1+x}-bx-1\\right)=\\lim_{x\\to\\infty}[f(x+1)-f(x)]$，则曲线 $y=\\frac{ax^2}{1+x}$ 的斜渐近线方程为（　）。\n\nA. $y=-x+1$  \nB. $y=x+1$  \nC. $y=-x-1$  \nD. $y=x-1$\n\n2\\. 设可导函数 $f(x)$ 在 $[a,b]$ 上满足 $f(x)>0$，$f'(x)>0$，则 $\\lim_{b\\to a^+}\\frac{\\ln f(b)-\\ln f(a)}{f(b)-f(a)}=$（　）。\n\nA. $f(a)$  \nB. $\\frac1{f(a)}$  \nC. $\\frac1{f'_+(a)}$  \nD. $f'_+(a)$\n\n3\\. 设 $I_1=\\int_0^1\\ln(1+x)\\,\\mathrm dx$，$I_2=\\int_0^1\\frac{\\arctan x}{1+x}\\,\\mathrm dx$，$I_3=\\int_0^1\\sqrt{\\ln(1+x)}\\,\\mathrm dx$，则（　）。\n\nA. $I_3>I_1>I_2$  \nB. $I_3>I_2>I_1$  \nC. $I_1>I_2>I_3$  \nD. $I_2>I_3>I_1$\n\n4\\. 设 $z(x,y)$ 满足 $\\frac{\\partial z}{\\partial x}=\\sin y+\\frac1{1-xy}$，$z(1,y)=\\sin y$，则（　）。\n\nA. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx+\\mathrm dy$  \nB. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx-\\mathrm dy$  \nC. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx+\\frac12\\,\\mathrm dy$  \nD. $\\left.\\mathrm dz\\right|_{(0,2)}=(1+\\sin2)\\,\\mathrm dx-\\frac12\\,\\mathrm dy$\n\n5\\. 设正项数列 $\\{x_n\\}$ 满足 $x_{n+1}<2-\\frac1{x_n}$（$n=1,2,\\ldots$），则（　）。\n\nA. $\\{x_n\\}$ 收敛于 0。  \nB. $\\{x_n\\}$ 收敛于 1。  \nC. $\\{x_n\\}$ 收敛于 $\\sqrt2$。  \nD. $\\{x_n\\}$ 发散。\n\n6\\. 设 $f(x)$ 在 $[0,4]$ 上有二阶连续导数，在 $xOy$ 坐标系中，三条曲线为 $y=f(x)$，$y=f'(x)$，$y=f''(x)$。如图所示，$L_1$ 单调增加，在 $x=2$ 处穿过 $x$ 轴；$L_2$ 从 $y$ 轴上方下降，在 $x=1$ 处穿过 $x$ 轴，达到极小值后上升，在 $x=3$ 处再次穿过 $x$ 轴；$L_3$ 自 $y$ 轴附近上升，达到极大值后下降，在 $x=2$ 处穿过 $x$ 轴，达到极小值后上升，在 $x=4$ 处再次穿过 $x$ 轴。则 $y=f(x)$ 在 $[0,4]$ 上（　）。\n\nA. 有一个极值点，一个拐点。  \nB. 有一个极值点，两个拐点。  \nC. 有两个极值点，一个拐点。  \nD. 有两个极值点，两个拐点。\n\n7\\. 已知平面上的点 $A(0,1)$ 和抛物线 $x=2\\sqrt y$，动点 $P$ 从坐标原点 $O$ 出发，沿抛物线移动。若直线段 $OA$、$AP$ 和抛物线所围成图形的面积对时间 $t$ 的增大速率为 1，则当 $P$ 移动到点 $(6,9)$ 处时，$P$ 的横坐标的变动速率为（　）。\n\nA. $\\frac12$  \nB. $\\frac13$  \nC. $\\frac14$  \nD. $\\frac15$\n\n8\\. 设 $A$ 为 3 阶矩阵，$\\alpha_1=(1,2,-2)^T$，$\\alpha_2=(2,1,-1)^T$，$\\alpha_3=(1,1,a)^T$（$a\\ne-1$）是非齐次线性方程组 $AX=b$ 的三个解，$A^*$ 是 $A$ 的伴随矩阵，则（　）。\n\nA. $AX=0$ 与 $A^*X=0$ 同解。  \nB. $A^*X=0$ 的解均是 $AX=0$ 的解，但二者不同解。  \nC. $AX=0$ 的解均是 $A^*X=0$ 的解，但二者不同解。  \nD. $AX=0$ 与 $A^*X=0$ 没有非零公共解。\n\n9\\. 设 $A$ 为 2 阶实矩阵，$\\alpha$ 与 $\\beta$ 是 $A$ 的两个单位实特征向量，且满足 $\\|\\alpha+\\beta\\|=\\|\\alpha-\\beta\\|$，则（　）。\n\nA. $r(A)=1$  \nB. $r(A)=2$  \nC. $A$ 必相似于对角矩阵。  \nD. $A$ 必与单位矩阵合同。\n\n10\\. 设 $A,B,C$ 均为 3 阶矩阵，$r(C)=1$，$r(B)=2$，且满足 $(A+E)C=O$，$B(A^T-2E)=O$，则下列矩阵中与 $A$ 相似的是（　）。\n\nA. $\\begin{bmatrix}2&1&0\\\\0&2&1\\\\0&0&1\\end{bmatrix}$  \nB. $\\begin{bmatrix}-1&1&0\\\\0&-1&1\\\\0&0&2\\end{bmatrix}$  \nC. $\\begin{bmatrix}-2&0&0\\\\0&-2&0\\\\0&0&1\\end{bmatrix}$  \nD. $\\begin{bmatrix}-1&0&0\\\\0&2&0\\\\0&0&2\\end{bmatrix}$\n\n### 填空题\n\n11\\. 设 $y=f(x)$ 由方程 $\\mathrm e^y+x=\\mathrm e\\cos(xy)$ 确定，则 $\\lim_{n\\to\\infty}\\left[f\\left(\\frac1n\\right)\\right]^{n(1-\\cos\\frac1n)}=$ ______。\n\n12\\. 设 $x=f(y)$ 是单调可导函数 $y=g(x)$ 的反函数，且 $g(1)=2$，$g'(1)=-\\frac{\\sqrt3}{3}$，则 $\\lim_{y\\to2}(y-2)\\frac{f(y)-f(2)}{(\\ln y-\\ln2)^2}=$ ______。\n\n13\\. 设 $a^2+b^2=1$（$a<0,b>0$），则曲线 $y=x^2+ax$ 与直线 $y=bx$ 所围区域面积的最大值为 ______。\n\n14\\. 设 $y=x\\cos^2x$ 在 $x\\in[0,n\\pi]$（$n=1,2,\\ldots$）上与 $x$ 轴所围图形的面积为 $S_n$，则 $\\lim_{n\\to\\infty}\\frac{S_n}{(n+1)^2}=$ ______。\n\n15\\. $\\lim_{n\\to\\infty}n\\int_0^{2\\pi}\\mathrm e^{-x}\\sin nx\\,\\mathrm dx=$ ______。\n\n16\\. 设 $\\alpha_1,\\alpha_2,\\alpha_3$ 为线性无关的 3 维列向量，$A=(\\alpha_1,\\alpha_2,\\alpha_3)$，交换 $A$ 的第 2 列与第 3 列，再将第 2 列乘以 $(-4)$、第 3 列乘以 $(-1)$ 得 $C$。若 $BA=C$，则 $\\operatorname{tr}(B)=$ ______。\n\n### 解答题\n\n17\\. （10 分）设定义在 $(-\\infty,+\\infty)$ 内的连续函数 $f(x)$ 满足\n\n$$\nf(x)f(y)=f(x+y),\\qquad \\lim_{x\\to0}\\frac{1-f(x)}x=1.\n$$\n\n求 $F(x)=|x|f(x)$ 的极值。\n\n18\\. （12 分）设 $y(x)$ 满足 $4x\\frac{\\mathrm dy^2}{\\mathrm dx^2}+2(1-\\sqrt x)\\frac{\\mathrm dy}{\\mathrm dx}-6y=\\mathrm e^{-\\sqrt x}$。\n\n（Ⅰ）作变换 $x=t^2$（$t>0$），将方程变换成 $y$ 关于 $t$ 的方程；\n\n（Ⅱ）若 $\\lim_{x\\to0^+}y(x)=0$，$\\lim_{x\\to+\\infty}y(x)=0$，求 $y(x)$。\n\n19\\. （12 分）设 $f(x)$ 满足 $f'(x)-\\frac1nf(x)=\\left(1+\\frac1n\\right)x-1-n$，$f(0)=n^2$，$n$ 为正整数。\n\n（Ⅰ）求 $f(x)$；\n\n（Ⅱ）若 $f(x)$ 在点 $x=x_n$ 处取得极小值，求 $\\lim_{n\\to\\infty}x_n^n$。\n\n20\\. （12 分）设 $D=\\left\\{(r,\\theta)\\mid0\\le\\theta\\le\\frac{\\pi}{2},\\,0\\le r\\le2\\cos\\theta,\\,0\\le r\\le\\frac2{\\cos\\theta+\\sin\\theta}\\right\\}$。计算 $I=\\iint_D(\\cos\\theta+\\sin\\theta)r^2\\,\\mathrm d\\theta\\,\\mathrm dr$。\n\n21\\. （12 分）设 $f(x)$ 连续且严格单调递减。\n\n（Ⅰ）证明当 $x\\in(0,1)$ 时，有 $x\\int_0^1 f(t)\\,\\mathrm dt<\\int_0^x f(t)\\,\\mathrm dt<xf(0)$；\n\n（Ⅱ）若 $\\int_0^1 f(t)\\,\\mathrm dt\\ge0$，$f(0)\\le1$，$x_0\\in(0,1)$，$x_n=\\int_0^{x_{n-1}}f(t)\\,\\mathrm dt$（$n=1,2,\\ldots$）。证明 $\\lim_{n\\to\\infty}x_n$ 存在，并求其值。\n\n22\\. （12 分）设实对称矩阵 $A=(a_{ij})_{3\\times3}$ 有二重特征值 1，且 $\\sum_{i=1}^3a_{ij}=0$（$j=1,2,3$）。\n\n（Ⅰ）记 $X=(x_1,x_2,x_3)^T$，求方程 $X^TAX=0$ 的全部解；\n\n（Ⅱ）求可逆矩阵 $P$，使得 $X^T(2E-A)X=\\|PX\\|$。\n"}

## tool · 2026-11-12T01:33:25Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/f3accd139463ec251cb5497ea4480bfbe3e02d07e44bcce0dbaf2fe4ab6a5b26.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/41bd487900775ff96a44739b2f8f1abfb5d68757e233e62016b8ab0dead164fd.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/59e076e28cb1049bb8cbcb2297fd7011e9b667fb65fb89aeb8da9f0568b2f281.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/735587c49a73c81d756963e63976acea65a0d312a311bb85190330e9903bddc0.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/0883ed4f98931a26ab971ac5bc24d400c931f4554fe769e3da51fb04a4fd640e.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/069ea22d10374810cadcb38d8d2e5f510987b4a5f6cb9c5d1117c049df6939a2.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/f817548639544722671c18014157392bf33124f24ecde15182d9c25cd67742d2.png",
  "detail": "high"
}

## tool · 2026-11-12T01:33:32Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/932bbab7cbb98cfa97418355c52539b4fab52c228f1f1ef0ab65b26b12be12cb.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/0f1377b926b49d3fa9f774a821aed173002d990e056a976658df2232f09840b8.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/6fa8196198b6072edb212ca701394bf951ec3987d5b852cac7b011acf669958c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c697ff34440e7463bd76956cb87c7fdeeeca4b39e5a1ecc6231548c43f12e285.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/a91d1f871fda657ad652949587d02c60079ee7d4d793c45d9716d10b6a6b8150.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/22e4a3b3a97196f2b1cf8cb27ed7beadfda85027ecaab6c5388626fbc5c62374.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/0abe49b1459112d0d1f9b7a3835e2dbf630cc51a602592ed1f7fbb60c67c7b44.png",
  "detail": "high"
}

## tool · 2026-11-12T01:33:38Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/02f035c5b4d6e5347d7afac160f428408d466a137f3ceb1c2079cf092a50562e.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/2663cdaa4e56b8b80253716f134b099315ecfbaacf5262572aa8b281d5b64a0c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/2b95f36ad591fca7e88791245df61d509bb9b0b8b17f53c088a400ee18e001de.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c0bbc8761c92066779b616e9af0c75300e9d3a3edd60d1a5e33c46533f51d892.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/28c049f1b54d7f9e71874a5a989497af62d733714645d835ed4ac269afa4efe8.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/8e1b615a4fd5ba1f72b0f333033ce55c9670eb5f2b0dafcfa9f686e4b058ef8f.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/97a7caecd02888617b46864761f42c74eddf8227739eeff737db0755a6291f3b.png",
  "detail": "high"
}

## tool · 2026-11-12T01:33:51Z




## tool · 2026-11-12T01:34:09Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"90bd4a","wall_time_seconds":0.000009583,"exit_code":0,"original_token_count":132,"output":"==> .question-bank-work/older-forty-zhang-4.md <==\n## 26 张宇八套卷·卷四\n\n### 选择题\n\n\n==> .question-bank-work/older-forty-zhang-5.md <==\n## 26 张宇八套卷·卷五\n\n### 选择题\n\n\n==> .question-bank-work/older-forty-zhang-6.md <==\n## 26 张宇八套卷·卷六\n\n### 选择题\n\n## 卷八· 李林四套卷（4）\n\n### 选择题\n\n1\\. 当 $t\\to0^+$ 时，$\\alpha(t)=\\int_0^t\\mathrm dx\\int_x^t\\sin(xy)^2\\,\\mathrm dy$ 是关于 $t$ 的 $n$ 阶无穷小，则 $n=$（　）。\n\nA. 3。  \nB. 4。  \nC. 5。  \nD. 6。\n"}
{}
{"chunk_id":"6aeb5d","wall_time_seconds":0.000008042,"exit_code":0,"original_token_count":124,"output":"references/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A3数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A4数二模拟卷精选20套.pdf.md\n"}

## tool · 2026-11-12T01:34:14Z




## tool · 2026-11-12T01:34:20Z


Script completed
Wall time 0.6 seconds
Output:

{"chunk_id":"4d457f","wall_time_seconds":0.467929125,"exit_code":0,"original_token_count":1432,"output":"## 26 张宇八套卷·卷四\n\n### 选择题\n\n1\\. 设函数 $f(x)$ 在 $x=0$ 的某邻域内有定义，且 $\\lim_{x \\to 0} \\frac{x - f(x)}{\\ln(1 + x)} = 1$，则以下叙述：  \n① $f(0) = 0$；② $\\lim_{x \\to 0} f(x) = f(0)$；③ $\\lim_{x \\to 0} \\frac{f(x)}{x} = 1$；④ 当 $x \\to 0$ 时，$f(x)$ 是 $x$ 的高阶无穷小。  \n正确叙述的个数为  \nA. 1.  \nB. 2.  \nC. 3.  \nD. 4.\n\n2\\. 函数 $f(x, y) = x^{2} + y^{2}$ 在约束条件 $(x-1)^{3} = y^{2}$ 下  \nA. 有最大值，无最小值.  \nB. 无最大值，无最小值.  \nC. 有最大值，有最小值.  \nD. 无最大值，有最小值.\n\n3\\. 设 $f(x)$ 在 $[0,1]$ 上可积，则 $\\lim_{n \\to \\infty} \\sum_{i=0}^{n-1} \\ln \\left[1 + \\frac{1}{n} f\\left(\\frac{i}{n}\\right)\\right] =$  \nA. $\\int_{0}^{1} \\ln \\left[1 + \\frac{f(x)}{n}\\right] dx$.  \nB. $\\int_{0}^{1} \\ln \\left[1 + f(x)\\right] dx$.  \nC. $\\int_{0}^{1} f(x) dx$.  \nD. $\\int_{0}^{1} f^{2}(x) dx$.\n\n4\\. 设函数 $z = z(x, y)$ 由 $z + \\ln z = \\int_{x}^{y} e^{-t^{2}} dt$ 确定，则 $\\frac{\\partial z}{\\partial x} + \\frac{\\partial z}{\\partial y} =$  \nA. $\\frac{z}{z+1} \\left( e^{-x^{2}} - e^{-y^{2}} \\right)$.  \nB. $\\frac{z}{z+1} \\left( e^{-x^{2}} + e^{-y^{2}} \\right)$.  \nC. $-\\frac{z}{z+1} \\left( e^{-x^{2}} - e^{-y^{2}} \\right)$.  \nD. $-\\frac{z}{z+1} \\left( e^{-x^{2}} + e^{-y^{2}} \\right)$.\n\n5\\. 如果对于微分方程 $y'' - (2k - 4)y' + ky = 0$ 的任一解 $y(x)$，反常积分 $\\int_{0}^{+\\infty} y(x) dx$ 均收敛，则 $k$ 的取值范围为  \nA. $(-\\infty, 1]$.  \nB. $(0, 1]$.  \nC. $(-\\infty, 2)$.  \nD. $(0, 2)$.\n\n6\\. 函数 $f(x)$ 在 $x=0$ 的某邻域内有定义，且 $\\lim_{x\\to0}\\frac{f(x)}{x}$ 存在，则 $\\lim_{x\\to0}\\frac{f(x)-f(-x)}{x}$ 是 $\\lim_{x\\to0}\\frac{f(x)}{x}=0$ 的  \nA. 充分必要条件.  \nB. 充分非必要条件.  \nC. 必要非充分条件.  \nD. 既非充分也非必要条件.\n\n7\\. 设函数 $f(x)$ 在 $x=0$ 的去心邻域内有定义且为奇函数，若当 $x\\to0$ 时，$f(x)$ 是比 $x$ 高阶的无穷小，则以下结论正确的个数为  \n① $f'(0)=0$。② $\\lim_{x\\to0}f(x)=0$。③ $f(0)=0$。④ $\\lim_{x\\to0}\\frac{f(x)}{x^2}=0$。  \nA. 1.  \nB. 2.  \nC. 3.  \nD. 4.\n\n8\\. 以下矩阵相似的是  \nA. $\\begin{pmatrix}-1&&\\\\&-1&\\\\&&-1\\end{pmatrix}$ 与 $\\begin{pmatrix}-1 & 1 & 0 \\\\ 0 & -1 & 0 \\\\ 0 & 0 & -1\\end{pmatrix}$。  \nB. $\\begin{pmatrix}1&&\\\\&1&\\\\&&1\\end{pmatrix}$ 与 $\\begin{pmatrix}1 & 1 & 0 \\\\ 0 & 1 & 0 \\\\ 0 & 0 & 1\\end{pmatrix}$。  \nC. $\\begin{pmatrix}1&&\\\\&2&\\\\&&3\\end{pmatrix}$ 与 $\\begin{pmatrix}1 & 1 & 0 \\\\ 0 & 2 & 1 \\\\ 0 & 0 & 3\\end{pmatrix}$。  \nD. $\\begin{pmatrix}1 & 0 & 0 \\\\ 0 & 1 & 0 \\\\ 0 & 0 & 2\\end{pmatrix}$ 与 $\\begin{pmatrix}1 & 1 & 0 \\\\ 0 & 1 & 0 \\\\ 0 & 0 & 2\\end{pmatrix}$。\n\n9\\. 设二次型 $f(x_{1}, x_{2}, x_{3}) = x_{1}^{2} + ax_{2}^{2} + ax_{3}^{2} + 2x_{1}x_{2} + 2x_{1}x_{3}$ 的正负惯性指数分别为 1, 1，则以下结论可能正确的是  \nA. $a > 1$.  \nB. $a < 0$.  \nC. $0 \\leq a \\leq 1$.  \nD. $a = 0$.\n\n10\\. 设 $A, B$ 均为 $n$ 阶矩阵，且 $A \\sim B$，则下列结论中不一定正确的是  \nA. $A$ 与 $B$ 有相同的特征多项式.  \nB. $A$ 与 $B$ 有相同的秩.  \nC. $A$ 与 $B$ 有相同的特征值.  \nD. $A$ 与 $B$ 有相同的特征向量.\n\n### 填空题\n\n11\\. $\\int_{-1}^{1}\\left(x^{2}\\ln\\frac{2-x}{2+x}+\\sin^{2}x\\ln\\frac{1+x}{1-x}\\right)\\mathrm{d}x=\\underline{\\qquad}$。\n\n12\\. 设 $y=y(x)$ 满足 $\\sqrt{1+x^{2}}y'-\\sqrt{1+y^{2}}=0$，且 $y(0)=1$，则 $\\int_{0}^{1}y(x)\\mathrm{d}x=\\underline{\\qquad}$。\n\n13\\. 设函数 $y=y(x)$ 由 $\\begin{cases} x=\\arctan t,\\\\ y=\\ln(1+t^{2}) \\end{cases}$ 确定，则 $\\frac{\\mathrm{d}^{2}y}{\\mathrm{d}x^{2}}=\\underline{\\qquad}$。\n\n14\\. $\\int_{0}^{1}\\mathrm{d}x\\int_{0}^{\\sqrt{x}}y^{2}\\mathrm{e}^{x-y}\\mathrm{d}y=\\underline{\\qquad}$。\n\n15\\. 已知曲线 $y=y(x)$ 在每一点的切线与 $y$ 轴的截距与该点横坐标的平方之比为 $3:1$，则该曲线方程为 $\\underline{\\qquad}$。\n\n16\\. 设 $\\alpha_{1}=\\begin{pmatrix}1\\\\ 0\\\\ 1\\end{pmatrix},\\alpha_{2}=\\begin{pmatrix}0\\\\ 1\\\\ 1\\end{pmatrix},\\alpha_{3}=\\begin{pmatrix}1\\\\ 1\\\\ 0\\end{pmatrix}$，若 $A\\alpha_{1}=\\alpha_{2},A\\alpha_{2}=\\alpha_{3},A\\alpha_{3}=\\alpha_{1}$，则 $A^{3}x=b$ 的解为 $\\underline{\\qquad}$。\n\n### 解答题\n\n17\\. 设 $f'(x)=\\mathrm{e}^{-x^{2}}$,$g(x)=f(x^{2})$，求 $\\int_{0}^{1}g(x)\\mathrm{d}x$。\n\n18\\. 设函数 $f(x)$ 满足 $f(x)+2\\int_{0}^{x}f(t)\\mathrm{d}t=x^{2}$，且 $f(0)=1$。\n\n（1）求 $y=f(x)$ 的表达式；\n\n（2）记由曲线 $y=f(x),x=0,x=1,y=0$ 围成的平面图形面积为 $S$，求 $S$。\n\n19\\. 设函数 $f(x)$ 在 $[a,b]$ 上连续，在 $(a,b)$ 内可导，且 $f(a)=f(b)=0$。证明：\n\n（1）存在一点 $\\xi \\in (a,b)$，使得 $\\int_{a}^{\\xi} f(t)dt = f(\\xi)$；\n\n（2）存在一点 $\\eta \\in (a,b)$，使得 $f'(\\eta) - \\int_{a}^{\\eta} f(t)dt = 0$。\n\n20\\. 设 $f(x,y) = \\mathrm{e}^{x^2 + y^2} - 1$，区域 $D: x^2 + y^2 \\leq 1$，计算 $\\iint_{D} \\left( \\frac{\\partial^2 f}{\\partial x^2} + \\frac{\\partial^2 f}{\\partial y^2} \\right) \\mathrm{d}\\sigma$。\n\n21\\. 设 $z = z(x,y)$ 具有二阶连续偏导数，且 $z = (x - y)\\varphi(x + y)$，其中 $\\varphi$ 二阶可导。\n\n（1）证明：$\\frac{\\partial^2 z}{\\partial x^2} + 2\\frac{\\partial^2 z}{\\partial x \\partial y} + \\frac{\\partial^2 z}{\\partial y^2} = 0$；\n\n（2）若 $\\varphi(0) = 1$，$\\varphi'(0) = 2$，求 $z = z(x,y)$ 的表达式。\n\n22\\. 设 $A = \\begin{pmatrix} 1 & 2 & 3 \\\\ 0 & 1 & 2 \\\\ 1 & 0 & 2 \\end{pmatrix}$，$\\beta = \\begin{pmatrix}4\\\\-1\\\\0\\end{pmatrix}$，$B = \\begin{pmatrix} 2 & 1 & 0 \\\\ -1 & 2 & 1 \\\\ 0 & -1 & 2 \\end{pmatrix}$。\n\n（1）求 $r(A)$ 并求 $Ax = \\beta$ 的通解；\n\n（2）求满足 $(\\boldsymbol{A}\\boldsymbol{B})\\boldsymbol{Y} = \\boldsymbol{B}\\boldsymbol{C}$ 的所有 $\\boldsymbol{Y}$。\n"}

## tool · 2026-11-12T01:34:26Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/7a99e179f8d94820160ccf7c5f0cce0e0fe6b245678aa8c5e6c648556505cda8.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/709c79fc71562cafa6f1a78fb4baaabc8751fa333213095d164696b45417c673.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/bbdc755e4bad3c8d66c9e2d88565aeebaba919d329b87f1bc3b67190da34b699.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/b461719e7bf8c839a14b9df5587206ef738c22d99cbbaebe2a793fc9a2dff8c0.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/f7d4dd565a510c7b934c553bdcc0f2d58adeb99a5930eeed6143d8acf8fef249.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/f3dd013425a20196dc26193d2eb430647f4f5c8ab1d91f6e36be401382fa553a.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/ce87082b709994a14b28f6d1abff54182cfcffc4b911f94ff3bebf709070398e.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c9e63fcb5b267b5dcc536210f42dfb1072c73346e6eb715398c261f2ede35127.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/d6e91ee58641b5133ed101ccc8e34afbfdc9c56b0fbe9da55fe53260e32526fb.png",
  "detail": "high"
}

## tool · 2026-11-12T01:34:35Z




## tool · 2026-11-12T01:34:39Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"082b0e","wall_time_seconds":0.00001125,"exit_code":0,"original_token_count":2864,"output":"## 26 张宇八套卷·卷五\n\n### 选择题\n\n1\\. 设 $f\\left(\\frac{1}{x}\\right)=x+\\sqrt{1+x^2}$（$x\\neq0$），则 $x=0$ 是 $f(x)$ 的  \nA. 连续点.  \nB. 跳跃间断点.  \nC. 可去间断点.  \nD. 第二类间断点.\n\n2\\. 设 $f(x,y)=x^2+y^2(1+x)^3$，则  \nA. 点 $(0,0)$ 是 $f(x,y)$ 的唯一极小值点，也是其最小值点。  \nB. 点 $(0,0)$ 是 $f(x,y)$ 的唯一极大值点，也是其最大值点。  \nC. 点 $(0,0)$ 是 $f(x,y)$ 的唯一极小值点，但不是其最小值点。  \nD. 点 $(0,0)$ 是 $f(x,y)$ 的唯一极大值点，但不是其最大值点。\n\n3\\. 若 $\\{x_n\\}, \\{y_n\\}$ 满足 $\\lim_{n\\to\\infty} x_n y_n = \\infty$，则以下结论：  \n① $\\lim_{n\\to\\infty} x_n = \\infty$ 或 $\\lim_{n\\to\\infty} y_n = \\infty$；  \n② $\\lim_{n\\to\\infty} x_n = \\infty$ 且 $\\lim_{n\\to\\infty} y_n = \\infty$；  \n③ $x_n$ 与 $y_n$ 中一个是无穷大量，另一个是无界量；  \n④ 当 $x_n$ 是非零无穷小量时，$\\lim_{n\\to\\infty} y_n = \\infty$。  \n正确结论的个数为  \nA. 1.  \nB. 2.  \nC. 3.  \nD. 4.\n\n4\\. 设 $p,q$ 为正常数，若 $\\int_0^1 \\frac{1}{x^p |\\ln x|^q}\\,dx$ 收敛，则  \nA. $p<1,\\ q<1$。  \nB. $p>1,\\ q<1$。  \nC. $p<1,\\ q>1$。  \nD. $p>1,\\ q>1$。\n\n5\\. 设函数 $y = f(x)$ 由参数方程 $\\begin{cases} x = t^3 + \\frac{\\pi}{2} - 1, \\\\ y = e^{t^2} \\end{cases}$ 确定，则 $\\lim_{n \\to \\infty} n \\left[ f\\left(\\frac{\\pi}{2} + \\frac{2}{n}\\right) - f\\left(\\frac{\\pi}{2}\\right) \\right] =$  \nA. $2e$。  \nB. $\\frac{4e}{3}$.  \nC. $\\frac{2e}{3}$.  \nD. $\\frac{e}{3}$.\n\n6\\. 设函数 $f(x)=\\int_{0}^{\\sin x} e^{t^2} \\sin t \\, dt$, $g(x)=\\int_{0}^{x} e^{t^2} \\sin^2 x \\, dt$, 则  \nA. $f(x)$ 是奇函数, $g(x)$ 是奇函数.  \nB. $f(x)$ 是偶函数, $g(x)$ 是奇函数.  \nC. $f(x)$ 是偶函数, $g(x)$ 是偶函数.  \nD. $f(x)$ 是奇函数, $g(x)$ 是偶函数.\n\n7\\. 已知数列 $\\{a_n\\}$ 发散, $b_n = a_n e^{a_n}$, 则  \nA. 当 $a_n > 0$ 时, $\\{b_n\\}$ 收敛.  \nB. 当 $a_n < 0$ 时, $\\{b_n\\}$ 收敛.  \nC. 当 $a_n > 0$ 时, $\\{b_n\\}$ 发散.  \nD. 当 $a_n < 0$ 时, $\\{b_n\\}$ 发散.\n\n8\\. 设二次型 $f(x_1, x_2, x_3) = 4x_1^2 + x_2^2 + ax_3^2 + 2x_1x_2 - 4x_1x_3 + 2x_2x_3$ 与 $g(y_1, y_2, y_3) = 2y_1^2 + by_2^2$ 合同, 则  \nA. $a = 3, b > 0$.  \nB. $a = 3, b < 0$.  \nC. $a = 4, b > 0$.  \nD. $a = 4, b < 0$.\n\n9\\. 设 $\\mathbf{A}, \\mathbf{B}$ 为 $n$ 阶矩阵，且 $\\mathbf{A}$ 满足 $\\mathbf{A}^2-\\mathbf{A}=3\\mathbf{E}$，则与 $\\begin{pmatrix} \\mathbf{A} \\\\ \\mathbf{B} \\end{pmatrix} \\mathbf{x} = 0$ 不一定同解的是  \nA. $\\begin{pmatrix} \\mathbf{A} - \\mathbf{B} \\\\ \\mathbf{A} + \\mathbf{AB} \\end{pmatrix} \\mathbf{x} = 0$.  \nB. $\\begin{pmatrix} \\mathbf{A} + \\mathbf{B} \\\\ \\mathbf{A} + \\mathbf{AB} - \\mathbf{B} \\end{pmatrix} \\mathbf{x} = 0$.  \nC. $\\begin{pmatrix} \\mathbf{A} - \\mathbf{B} \\\\ 2\\mathbf{A} + \\mathbf{B} \\end{pmatrix} \\mathbf{x} = 0$.  \nD. $\\begin{pmatrix} \\mathbf{A} + \\mathbf{B} \\\\ \\mathbf{B}\\mathbf{A} + \\mathbf{B}^2 \\end{pmatrix} \\mathbf{x} = 0$.\n\n10\\. 设 $\\mathbf{A} = \\begin{pmatrix} 1 & 0 & a \\\\ b & 2 & 0 \\\\ 0 & c & 3 \\end{pmatrix}$, 其中 $abc = -6$, 则 $\\mathbf{A}$ 的伴随矩阵 $\\mathbf{A}^*$ 有非零特征值  \nA. $-8$。  \nB. $8$。  \nC. $-11$。  \nD. $11$。\n\n### 填空题\n\n11\\. $\\lim_{x \\to 0} \\frac{\\sqrt{1+2x} - \\sqrt[3]{1+3x}}{\\ln(1+x^2)}=\\underline{\\qquad}$。\n\n12\\. 已知函数 $y = y(x)$ 满足 $y' - 2\\sqrt{2}x\\sqrt{y} = 0$，且该曲线的一个拐点的横坐标为 $-2$，则 $y(x)=\\underline{\\qquad}$。\n\n13\\. $\\int_{1}^{+\\infty}\\frac{1}{x(x+2)}\\,dx=\\underline{\\qquad}$。\n\n14\\. 若 $(2ax^3y^3 - 3y^2 + 5)\\,dx+(3x^4y^2 - 2bxy - 4)\\,dy$ 是某函数 $u(x, y)$ 的全微分，则 $u(x,y)=\\underline{\\qquad}$。\n\n15\\. $\\lim_{n \\to \\infty} \\frac{1}{n^3} \\left[ \\ln \\frac{1}{n} + 4\\ln \\frac{2}{n} + \\cdots + (n-1)^2 \\ln \\frac{n-1}{n} \\right]=\\underline{\\qquad}$。\n\n16\\. 设 $A = \\begin{pmatrix} 1 & 1 \\\\ 0 & 1 \\end{pmatrix}$，$B = \\begin{pmatrix} -1 & 1 \\\\ 0 & -1 \\end{pmatrix}$，则 $A^9-B^9=\\underline{\\qquad}$。\n\n### 解答题\n\n17\\. 设平面区域 $D = \\left\\{(x, y) \\mid 0 \\leq y \\leq \\frac{\\sqrt{x^2 - 1}}{x^2}, \\sqrt{2} < x < 2\\right\\}$，求\n\n（1）$D$ 的面积；\n\n（2）$D$ 绕 $x$ 轴旋转一周所成旋转体的体积。\n\n18\\. 设 $y = y(x)$ 满足 $(xy - 1)\\mathrm{d}x + x^2\\mathrm{d}y = 0, x > 0, y(1) = 0$，求\n\n（1）$y = y(x)$ 的表达式；\n\n（2）曲线 $y = y(x)$ 的拐点及渐近线。\n\n19\\. 设函数 $f(x)$ 在 $[a, b]$ 上可导，$c \\in (a, b)$，证明：\n\n（1）存在一点 $\\xi \\in (a, c)$，使得 $f(c) - f(a) = f'(\\xi)(c - a)$；\n\n（2）存在一点 $\\eta \\in (a, b)$，使得 $f(b) - f(a) = f'(\\eta)(b - a)$ 且 $\\eta > \\xi$。\n\n20\\. 计算 $I=\\iint_{D}x^{2}y^{2}\\,dx\\,dy$，其中 $D$ 是由直线 $y=2$、$y=0$、$x=-2$ 及曲线 $x=-\\sqrt{2y-y^{2}}$ 所围成的区域。\n\n21\\. 已知可微函数 $f(u,v)$ 满足 $\\frac{\\partial[f(u,v)]}{\\partial u}+\\frac{\\partial[f(u,v)]}{\\partial v}=6(u+v)-3u^{2}$,\n且 $f(u,0)=3u^{2}-u^{3}$. 记 $g(x,y)=f(x,x-y)$.\n\n（1）计算 $\\frac{\\partial[g(x,y)]}{\\partial x}$;\n\n（2）求 $f(x,y)$ 在有界闭区域 $D=\\{(x,y)|x^{2}+y^{2}\\leq16\\}$ 上的最值.\n\n22\\. 设向量 $\\alpha_{1}=\\begin{pmatrix}1\\\\0\\\\1\\end{pmatrix},\\alpha_{2}=\\begin{pmatrix}0\\\\1\\\\1\\end{pmatrix},\\alpha_{3}=\\begin{pmatrix}1\\\\1\\\\0\\end{pmatrix}$.\n\n（1）将 $\\alpha_{1},\\alpha_{2},\\alpha_{3}$ 化成正交单位向量组 $\\gamma_{1},\\gamma_{2},\\gamma_{3}$；\n\n（2）若 $(\\alpha_{1},\\alpha_{2},\\alpha_{3})=(\\gamma_{1},\\gamma_{2},\\gamma_{3})C$，求 $C$。\n## 26 张宇八套卷·卷六\n\n### 选择题\n\n1\\. $f(x,y)=x^{4}+y^{4}-(x+y)^{2}$ 有  \nA. 2 个极小值点,1个极大值点.  \nB. 1个极小值点,1个极大值点.  \nC. 3个极小值点,无极大值点.  \nD. 2个极小值点,无极大值点.\n\n2\\. 设函数 $f(x,y)$ 连续，且 $f(x,y)=f(y,x)=f(-x,y)$，则 $\\int_{-2}^{2}dx\\int_{\\sqrt{4-x^{2}}}^{2}f(x,y)\\,dy=$  \nA. $\\int_{0}^{2}\\left[\\int_{-2}^{-\\sqrt{4-y^{2}}}f(x,y)dx+\\int_{\\sqrt{4-y^{2}}}^{2}f(x,y)dx\\right]dy.$  \nB. $2\\int_{0}^{2}\\left[\\int_{\\sqrt{4-y^{2}}}^{2}f(x,y)\\,dy\\right]dx.$  \nC. $4\\int_{0}^{\\frac{\\pi}{4}}d\\theta\\int_{2}^{2\\sec\\theta}f(r\\cos\\theta,r\\sin\\theta)rdr.$  \nD. $4\\int_{0}^{\\arctan\\frac{1}{2}}d\\theta\\int_{2}^{2\\sec\\theta}f(r\\cos\\theta,r\\sin\\theta)rdr.$\n\n3\\. 设 $f(x)$ 在 $(0,+\\infty)$ 内可导，$a$ 为常数。对于以下结论：  \n① 若 $\\lim_{x \\to +\\infty} f'(x) = a$，则 $\\lim_{x \\to +\\infty} \\frac{f(x)}{x} = a$；  \n② 若 $\\lim_{x \\to +\\infty} \\frac{f(x)}{x} = a$，则 $\\lim_{x \\to +\\infty} f'(x) = a$。  \n下列说法中正确的是  \nA. ①正确,②错误.  \nB. ①错误,②正确.  \nC. ①与②均正确.  \nD. ①与②均错误.\n\n4\\. 设函数 $f(t)$ 连续, 令 $F(x,y)=\\int_{0}^{y-x}(y-x-t)f(t)dt$, 则  \nA. $\\frac{\\partial F}{\\partial x}=\\frac{\\partial F}{\\partial y},\\frac{\\partial^{2}F}{\\partial x^{2}}=\\frac{\\partial^{2}F}{\\partial y^{2}}$.  \nB. $\\frac{\\partial F}{\\partial x}=\\frac{\\partial F}{\\partial y},\\frac{\\partial^{2}F}{\\partial x^{2}}=-\\frac{\\partial^{2}F}{\\partial y^{2}}$.  \nC. $\\frac{\\partial F}{\\partial x}=-\\frac{\\partial F}{\\partial y},\\frac{\\partial^{2}F}{\\partial x^{2}}=\\frac{\\partial^{2}F}{\\partial y^{2}}$.  \nD. $\\frac{\\partial F}{\\partial x}=-\\frac{\\partial F}{\\partial y},\\frac{\\partial^{2}F}{\\partial x^{2}}=-\\frac{\\partial^{2}F}{\\partial y^{2}}$.\n\n5\\. 曲线 $y = e^{-\\frac{1}{x}} \\sqrt{x^2 - 4x + 1}$ 的渐近线条数为  \nA. 1.  \nB. 2.  \nC. 3.  \nD. 4.\n\n6\\. 直角三角板的斜边长度为1, 将该直角三角板竖直插入水中, 并使其中一个直角边与水面对齐, 当三角板受到水的压力最大时, 其水平直角边长度为  \nA. $\\frac{\\sqrt{3}}{3}$.  \nB. $\\frac{\\sqrt{5}}{5}$.  \nC. $\\frac{\\sqrt{6}}{3}$.  \nD. $\\frac{\\sqrt{2}}{2}$.\n\n7\\. 设 $D$ 为由 $x=0$、$y=0$、$x+y=\\frac{1}{2}$、$x+y=1$ 所围成的区域，$I_{1}=\\iint_{D}\\ln^{7}(x+y)\\mathrm{d}\\sigma$，$I_{2}=\\iint_{D}(x+y)^{7}\\mathrm{d}\\sigma$，$I_{3}=\\iint_{D}\\sin^{7}(x+y)\\mathrm{d}\\sigma$，则  \nA. $I_{1}<I_{2}<I_{3}$.  \nB. $I_{1}<I_{3}<I_{2}$.  \nC. $I_{3}<I_{2}<I_{1}$.  \nD. $I_{3}<I_{1}<I_{2}$.\n\n8\\. 设 $A,B$ 是 $n$ 阶矩阵，$A^*,B^*$ 分别是 $A,B$ 对应的伴随矩阵，则分块矩阵 $C=\\begin{pmatrix} O & A \\\\ B & O \\end{pmatrix}$ 的伴随矩阵 $C^*=$  \nA. $\\begin{pmatrix} O & |A|A^* \\\\ |B|B^* & O \\end{pmatrix}$.  \nB. $\\begin{pmatrix} O & (-1)^n|A|B^* \\\\ (-1)^n|B|A^* & O \\end{pmatrix}$.  \nC. $\\begin{pmatrix} O & |B|A^* \\\\ |A|B^* & O \\end{pmatrix}$.  \nD. $\\begin{pmatrix} O & (-1)^n|B|B^* \\\\ (-1)^n|A|A^* & O \\end{pmatrix}$.\n\n9\\. 设矩阵 $A=\\begin{pmatrix} 1 & -1 & 1 \\\\ -2 & 2 & 1 \\\\ 1 & -1 & k \\end{pmatrix}$，$r((3E-A)^2)<r(3E-A)$，其中 $E$ 是 3 阶单位矩阵，则常数 $k=$  \nA. 3.  \nB. 4.  \nC. 5.  \nD. 6.\n\n10\\. 设 $n$ 阶方阵 $A=(\\alpha_{1},\\alpha_{2},\\cdots,\\alpha_{n})$，$B=(\\beta_{1},\\beta_{2},\\cdots,\\beta_{n})$，$AB=(\\gamma_{1},\\gamma_{2},\\cdots,\\gamma_{n})$，记向量组 I：$\\alpha_{1},\\alpha_{2},\\cdots,\\alpha_{n}$，向量组 II：$\\beta_{1},\\beta_{2},\\cdots,\\beta_{n}$，向量组 III：$\\gamma_{1},\\gamma_{2},\\cdots,\\gamma_{n}$。如果向量组 III 线性相关，则  \nA. 向量组 I 线性相关.  \nB. 向量组 II 线性相关.  \nC. 向量组 I 与 II 都线性相关.  \nD. 向量组 I 与 II 至少有一个线性相关.\n\n### 填空题\n\n11\\. 设 $x \\to 0$ 时，$\\ln\\frac{2+x}{2+\\sin x}$ 与 $x^n$ 为同阶无穷小，则 $n=\\underline{\\qquad}$。\n\n12\\. 使得 $\\ln x \\leq a\\sqrt{x}$ 成立的最小正数 $a$ 为 $\\underline{\\qquad}$。\n\n13\\. 已知 $D = \\{(x,y)\\mid(x-a)^2 + y^2 \\leq a^2, y \\geq 0\\}$，则 $\\iint_D \\sqrt{4a^2 - x^2 - y^2}\\,dx\\,dy=\\underline{\\qquad}$。\n\n14\\. 设 $z = f(u)$ 可导，$u = u(x,y)$ 由方程 $u = \\varphi(u) + \\int_y^x P(t)\\,dt$ 所确定，其中函数 $P$ 连续，$\\varphi$ 有连续导数，且 $\\varphi'(u) \\neq 1$，则 $P(x)\\frac{\\partial z}{\\partial y} + P(y)\\frac{\\partial z}{\\partial x}=\\underline{\\qquad}$。\n\n15\\. $x \\ln x\\,dy = (1 + y + \\ln^2 x)\\,dx$ 满足 $y(e)=1$ 的特解为 $\\underline{\\qquad}$。\n\n16\\. 设 $A$ 是 4 阶矩阵，$A$ 的伴随矩阵 $A^* = \\begin{pmatrix} 1 & 0 & 1 & 0 \\\\ 0 & 2 & 0 & 2 \\\\ 0 & 0 & 1 & 1 \\\\ 0 & 0 & 0 & 4 \\end{pmatrix}$，$\\mathbf{b} = (1,1,1,1)^T$，则方程组 $A\\mathbf{x} = \\mathbf{b}$ 的解为 $\\underline{\\qquad}$。\n\n### 解答题\n\n17\\. 设 $\\lim_{x \\to +\\infty} f(x) = +\\infty$, $\\lim_{x \\to +\\infty} g(x) = +\\infty$, 且 $\\lim_{x \\to +\\infty} \\frac{f(x)}{g(x)} = a > 0$, 计算 $\\lim_{x \\to +\\infty} \\frac{\\ln f(x)}{\\ln g(x)}$.\n\n18\\. 设 $y = y(x)$ 满足微分方程 $(xy' - 2)\\ln x + y = 0, y(e) = 2$.\n\n（1）求 $y = y(x)$ 的表达式及其定义域;\n\n（2）求函数 $y = y(x)$ 的极值.\n\n19\\. 设函数 $f(x)$ 在 $(a,b)$ 上二次可微, 证明: 对任意 $x \\in (a,b)$ 及适当小的正数 $h$ (使 $x + h, x - h \\in (a,b)$), 不等式 $f(x) \\leq \\frac{1}{2}[f(x + h) + f(x - h)]$ 成立的充要条件是 $f''(x) \\geq 0, x \\in (a,b)$.\n\n20\\. 计算 $\\iint_{D}\\ln(xy)\\mathrm{d}x\\mathrm{d}y$，其中 $D=\\{(x,y)\\mid 1\\leq xy\\leq2,x\\leq y\\leq4x,x>0\\}$。\n\n21\\. 过曲线 $\\frac{x^{2}}{4}+y^{2}=1$（$x\\geq0,y\\geq0$）任意点作该曲线的切线，切线夹在两坐标轴之间的部分为 $L$，求 $L$ 的最小长度，以及 $L$ 的长度达到最小时的切点坐标。\n\n22\\. 已知实矩阵 $\\mathbf{A}=\\begin{pmatrix}1&1\\\\1&a\\end{pmatrix}$，$\\mathbf{B}=\\begin{pmatrix}4&b\\\\3&1\\end{pmatrix}$，其中 $a$ 为非负整数，且 $\\mathbf{A}$ 与 $\\mathbf{B}$ 合同。\n\n（1）求 $a,b$ 的值；\n\n（2）求可逆矩阵$\\mathbf{D}$，使得$\\mathbf{A}=\\mathbf{D}^{\\mathrm{T}}\\mathbf{B}\\mathbf{D}$.\n"}

## tool · 2026-11-12T01:34:52Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"fbe73f","wall_time_seconds":0.029412417,"exit_code":0,"original_token_count":0,"output":""}
{
  "type": "input_image",
  "image_url": "images/3a14da6eb4232eecd175189ffe5fb7f397261b1b51d769e3a569fd24ad1e711d.png",
  "detail": "high"
}

## tool · 2026-11-12T01:35:59Z


Script completed
Wall time 0.2 seconds
Output:

{}
{"chunk_id":"8c1352","wall_time_seconds":0.000009459,"exit_code":0,"original_token_count":8,"output":"116 math expressions rendered\n"}

## tool · 2026-11-12T01:36:05Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/bc11661eeaa4161f8eee776c780b5d0ae1d440eec778ad01f07f0165a8dfa504.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/392dad66e21d8195d1df60af3ebd7099d1359b5c849a5454b01ff5c07d493cb0.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/4391b107c51aff571331e632c10b1f130c1cf83eaca8e675d75735c0fe0d47f3.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/2ff4a0a1022a4a173faa4dfc5834817aff775bee1f2d2737598df681bde0259c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/7133c4b836d5d93767ac16f7fd8749f369bf788e9319e819925b3c7c8a92e735.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/06ea0d1db535e26ffc09ce9ccc516da034ee0dc6733c89998a1d356238db2762.png",
  "detail": "high"
}

## tool · 2026-11-12T01:36:10Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/adcd0f5e338c755e098db6868926be56c400b7c554fc96fc624b877bb7aadd70.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c44d4cd0a1702bb647bc1358b83c601b474a43231122d6bac338334eb2654b0c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/456b0e74bddb75ba4b41090d61d407933d0feebb612bbe352971bd7033b489dc.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/972b435cdd7e01488ad5c26f678eef35f23ebc877d7772ce3701de3d960f6e3c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/72dd845dac6c2386d8f1c27951200fdd66cb5028128e280c0c00f2706d189d2e.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/49992126a9cc2e457f8c40735ff66465a975fc13002cc296a8297d2b0b6a4395.png",
  "detail": "high"
}

## tool · 2026-11-12T01:36:30Z




## tool · 2026-11-12T01:36:50Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"b5d1d6","wall_time_seconds":0.000010167,"exit_code":0,"original_token_count":285,"output":"        assert re.findall(r'(?m)^(\\d+)\\\\\\.', paper) == list(map(str, range(1, 23)))\n        pattern = re.compile(r'(?ms)^## ' + re.escape(title) + r'$.*?(?=^## |\\Z)')\n        current, count = pattern.subn(lambda m: paper + '\\n\\n', current)\n        assert count == 1\n    path.write_text(current.rstrip() + '\\n', encoding='utf-8')\n    print(path)\n.question-bank-work/older-forty-zhang-5.md:52:8\\. 设二次型 $f(x_1, x_2, x_3) = 4x_1^2 + x_2^2 + ax_3^2 + 2x_1x_2 - 4x_1x_3 + 2x_2x_3$ 与 $g(y_1, y_2, y_3) = 2y_1^2 + by_2^2$ 合同, 则  \n.question-bank-work/older-forty-zhang-5.md:86:17\\. 设平面区域 $D = \\left\\{(x, y) \\mid 0 \\leq y \\leq \\frac{\\sqrt{x^2 - 1}}{x^2}, \\sqrt{2} < x < 2\\right\\}$，求\n.question-bank-work/older-forty-zhang-6.md:11:2\\. 设函数 $f(x,y)$ 连续，且 $f(x,y)=f(y,x)=f(-x,y)$，则 $\\int_{-2}^{2}dx\\int_{\\sqrt{4-x^{2}}}^{2}f(x,y)\\,dy=$  \n.question-bank-work/older-forty-zhang-6.md:12:A. $\\int_{0}^{2}\\left[\\int_{-2}^{-\\sqrt{4-y^{2}}}f(x,y)dx+\\int_{\\sqrt{4-y^{2}}}^{2}f(x,y)dx\\right]dy.$  \n.question-bank-work/older-forty-zhang-6.md:13:B. $2\\int_{0}^{2}\\left[\\int_{\\sqrt{4-y^{2}}}^{2}f(x,y)\\,dy\\right]dx.$  \n"}
{}
{"chunk_id":"fe9b8a","wall_time_seconds":0.10999175,"exit_code":0,"original_token_count":64,"output":"references/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A3数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A4数二模拟卷精选20套.pdf.md\n5804 math expressions rendered\n"}

## tool · 2026-11-12T01:37:07Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"b084e7","wall_time_seconds":0.000008667,"exit_code":0,"original_token_count":0,"output":""}
{
  "type": "input_image",
  "image_url": "images/13052d0d4c96fefdfbd8de3e7315880df2849260ffea4c9a7401a2cbcea25427.png",
  "detail": "high"
}

## developer · 2026-11-12T01:37:07Z

<image_resize_notice>
Image 1 of 1 in the preceding tool output was resized from 2222x360 to 2048x332 pixels.
</image_resize_notice>

## tool · 2026-11-12T01:37:22Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"fc1f7a","wall_time_seconds":0.00001075,"exit_code":129,"original_token_count":2823,"output":"Warning: truncated output (original token count: 2823)\nTotal output lines: 133\n\n【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md [('卷一· 张宇四套卷（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷二· 张宇四套卷（2）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷三· 张宇四套卷（3）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷四· 张宇四套卷（4）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷五· 李林四套卷（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷六· 李林四套卷（2）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷七· 李林四套卷（3）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷八· 李林四套卷（4）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷九· 李林六套卷（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷十· 合工大超越（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6)]\n【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md [('卷一· 张宇四套卷（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷二· 张宇四套卷（2）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷三· 张宇四套卷（3）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷四· 张宇四套卷（4）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷五· 李林四套卷（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷六· 李林四套卷（2）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷七· 李林四套卷（3）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷八· 李林四套卷（4）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷九· 李林六套卷（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('卷十· 合工大超越（1）', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6)]\nA4数二模拟卷精选20套.pdf.md [('张宇四套卷· 卷一', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇四套卷· 卷二', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇四套卷· 卷三', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇四套卷· 卷四', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷一', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷二', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷三', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷四', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇八套卷·卷四', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇八套卷·卷五', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇八套卷·卷六', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6)]\nA3数二模拟卷精选20套.pdf.md [('张宇四套卷· 卷一', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇四套卷· 卷二', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇四套卷· 卷三', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇四套卷· 卷四', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷一', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷二', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷三', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('李林四套卷· 卷四', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇八套卷·卷四', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇八套卷·卷五', 0), ('选择题', 10), ('填空题', 6), ('解答题', 6), ('张宇八套卷·卷六', 0), ('选择题', 10), ('填空题'…823 tokens truncated…                 break complete rewrite changes into pairs of delete and create\n    -M, --find-renames[=<n>]\n                          detect renames\n    -D, --irreversible-delete\n                          omit the preimage for deletes\n    -C, --find-copies[=<n>]\n                          detect copies\n    --find-copies-harder  use unmodified files as source to find copies\n    --no-renames          disable rename detection\n    --rename-empty        use empty blobs as rename source\n    --follow              continue listing the history of a file beyond renames\n    -l <n>                prevent rename/copy detection if the number of rename/copy targets exceeds given limit\n\nDiff algorithm options\n    --minimal             produce the smallest possible diff\n    -w, --ignore-all-space\n                          ignore whitespace when comparing lines\n    -b, --ignore-space-change\n                          ignore changes in amount of whitespace\n    --ignore-space-at-eol\n                          ignore changes in whitespace at EOL\n    --ignore-cr-at-eol    ignore carrier-return at the end of line\n    --ignore-blank-lines  ignore changes whose lines are all blank\n    -I, --ignore-matching-lines <regex>\n                          ignore changes whose all lines match <regex>\n    --indent-heuristic    heuristic to shift diff hunk boundaries for easy reading\n    --patience            generate diff using the \"patience diff\" algorithm\n    --histogram           generate diff using the \"histogram diff\" algorithm\n    --diff-algorithm <algorithm>\n                          choose a diff algorithm\n    --anchored <text>     generate diff using the \"anchored diff\" algorithm\n    --word-diff[=<mode>]  show word diff, using <mode> to delimit changed words\n    --word-diff-regex <regex>\n                          use <regex> to decide what a word is\n    --color-words[=<regex>]\n                          equivalent to --word-diff=color --word-diff-regex=<regex>\n    --color-moved[=<mode>]\n                          moved lines of code are colored differently\n    --color-moved-ws <mode>\n                          how white spaces are ignored in --color-moved\n\nOther diff options\n    --relative[=<prefix>]\n                          when run from subdir, exclude changes outside and show relative paths\n    -a, --text            treat all files as text\n    -R                    swap two inputs, reverse the diff\n    --exit-code           exit with 1 if there were differences, 0 otherwise\n    --quiet               disable all output of the program\n    --ext-diff            allow an external diff helper to be executed\n    --textconv            run external text conversion filters when comparing binary files\n    --ignore-submodules[=<when>]\n                          ignore changes to submodules in the diff generation\n    --submodule[=<format>]\n                          specify how differences in submodules are shown\n    --ita-invisible-in-index\n                          hide 'git add -N' entries from the index\n    --ita-visible-in-index\n                          treat 'git add -N' entries as real in the index\n    -S <string>           look for differences that change the number of occurrences of the specified string\n    -G <regex>            look for differences that change the number of occurrences of the specified regex\n    --pickaxe-all         show all changes in the changeset with -S or -G\n    --pickaxe-regex       treat <string> in -S as extended POSIX regular expression\n    -O <file>             control the order in which files appear in the output\n    --rotate-to <path>    show the change in the specified path first\n    --skip-to <path>      skip the output to the specified path\n    --find-object <object-id>\n                          look for differences that change the number of occurrences of the specified object\n    --diff-filter [(A|C|D|M|R|T|U|X|B)...[*]]\n                          select files by diff type\n    --output <file>       output to a specific file\n\n"}

## tool · 2026-11-12T01:37:36Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"chunk_id":"79bf9e","wall_time_seconds":0.000009667,"exit_code":0,"original_token_count":55,"output":"【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md 10 220\n【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md 10 220\nA3数二模拟卷精选20套.pdf.md 11 242\nA4数二模拟卷精选20套.pdf.md 11 242\n"}

## tool · 2026-11-12T01:37:51Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"1f4534","wall_time_seconds":0.0160405,"exit_code":0,"original_token_count":14,"output":"Rect(0.0, 0.0, 595.2760009765625, 841.8900146484375)\n"}
{
  "type": "input_image",
  "image_url": "images/358bd27e31c08d903d9c6ec9c40bdc8056042a8bf6210893f9afa9e358edf00e.png",
  "detail": "high"
}

## developer · 2026-11-12T01:37:51Z

<image_resize_notice>
Image 1 of 1 in the preceding tool output was resized from 2222x460 to 2048x424 pixels.
</image_resize_notice>

## tool · 2026-11-12T01:38:04Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"410e8d","wall_time_seconds":0.000007292,"exit_code":0,"original_token_count":24,"output":"[(72.13600158691406, 628.3263549804688, 90.45437622070312, 641.165283203125, '(11)', 77, 0, 0)]\n"}
{
  "type": "input_image",
  "image_url": "images/3bb253106bec4497411758e7dae80424558c00abea922810bf83a0d636bc7388.png",
  "detail": "high"
}

## developer · 2026-11-12T01:38:04Z

<image_resize_notice>
Image 1 of 1 in the preceding tool output was resized from 2222x480 to 2048x442 pixels.
</image_resize_notice>

## tool · 2026-11-12T01:38:15Z




## tool · 2026-11-12T01:38:28Z




## tool · 2026-11-12T01:38:35Z




## tool · 2026-11-12T01:38:48Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"5d3d2c","wall_time_seconds":0.013413541,"exit_code":0,"original_token_count":24,"output":"[(72.13600158691406, 581.8703002929688, 90.83837890625, 594.709228515625, '(18)', 122, 0, 0)]\n"}
{
  "type": "input_image",
  "image_url": "images/2d8f62b892c134bbfaac1d624a7f18a2973ba9f64224931f10a9527d4a725fd8.png",
  "detail": "high"
}

## developer · 2026-11-12T01:38:48Z

<image_resize_notice>
Image 1 of 1 in the preceding tool output was resized from 1786x2526 to 1334x1888 pixels.
</image_resize_notice>

## tool · 2026-11-12T01:38:55Z




## tool · 2026-11-12T01:39:22Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"9a69d8","wall_time_seconds":0.000009625,"exit_code":0,"original_token_count":1051,"output":"import argparse\nfrom pathlib import Path\n\nimport numpy as np\nfrom PIL import Image\nimport pymupdf\n\n\nparser = argparse.ArgumentParser()\nparser.add_argument('name')\nparser.add_argument('first', type=int)\nparser.add_argument('last', type=int)\nparser.add_argument('label')\nargs = parser.parse_args()\nroot = Path('references/302模拟27')\nwork = Path('.question-bank-work/302-proof-source')\nsource, = root.rglob(args.name)\nwith pymupdf.open(source) as pdf:\n    for page in pdf.pages(args.first - 1, args.last):\n        w, h = page.rect.width, page.rect.height\n        rect = pymupdf.Rect(w * .07, h * .028, w * .94, h * .945)\n        pix = page.get_pixmap(matrix=pymupdf.Matrix(1.85, 1.85), clip=rect, colorspace=pymupdf.csGRAY)\n        pixels = np.frombuffer(pix.samples, dtype=np.uint8).reshape(pix.height, pix.width)\n        valid = np.flatnonzero((pixels < 150).any(axis=1))\n        bands = np.split(valid, np.where(np.diff(valid) > 19)[0] + 1)\n        pieces = [Image.fromarray(pixels[max(0, v[0] - 3):v[-1] + 4]) for v in bands if len(v)]\n        assert pieces\n        merged = Image.new('L', (pix.width, sum(i.height + 7 for i in pieces)), 'white')\n        y = 0\n        for im in pieces:\n            merged.paste(im, (0, y))\n            y += im.height + 7\n        merged.save(work / f'{args.label}-{page.number + 1}.png')\nfor layout in ['A3', 'A4']:\n    path, = root.rglob(f'{layout}数二模拟卷精选20套.pdf.md')\n    current = path.read_text(encoding='utf-8')\n    for number, title in enumerate(titles, 2):\n        paper = Path(f'.question-bank-work/302-ten-two-v{number}.md').read_text(encoding='utf-8').strip()\n        paper = paper.replace(paper.splitlines()[0], f'## {title}', 1)\n        if number == 5:\n            assert 'xy\\\\frac yx' in paper\n            paper = paper.replace('xy\\\\frac yx', 'xy\\\\ln\\\\frac yx', 1)\n            if layout == 'A4':\n                assert 'g(1)=\\\\frac32' in paper\n                paper = paper.replace('g(1)=\\\\frac32', 'g(1)=\\\\frac52', 1)\n        assert re.findall(r'(?m)^(\\d+)\\\\\\.', paper) == list(map(str, range(1, 23)))\n        pattern = re.compile(r'(?ms)^## ' + re.escape(title) + r'$.*?(?=^## |\\Z)')\n        current, count = pattern.subn(lambda m: paper + '\\n\\n', current)\n        assert count == 1\n    for volume in [4, 5, 6]:\n        title = '张宇八套卷·卷' + {4: '四', 5: '五', 6: '六'}[volume]\n        if volume == 4:\n            paper = Path('.question-bank-work/302-twenty-two-zhang4.md').read_text(encoding='utf-8').strip()\n        else:\n            paper = Path(f'.question-bank-work/older-forty-zhang-{volume}.md').read_text(encoding='utf-8').strip()\n            paper = paper.replace(paper.splitlines()[0], f'## {title}', 1)\n            if volume == 5:\n                assert '\\\\sqrt{2} < x < 2' in paper\n                paper = paper.replace('\\\\sqrt{2} < x < 2', '\\\\sqrt{2} \\\\leq x \\\\leq 2', 1)\n                assert 'g(y_1, y_2, y_3)' in paper\n                paper = paper.replace('g(y_1, y_2, y_3)', 'g(y_1, y_2)', 1)\n            else:\n                old = '\\\\int_{\\\\sqrt{4-y^{2}}}^{2}f(x,y)dx'\n                assert old in paper\n                paper = paper.replace(old, '\\\\int_{-\\\\sqrt{4-y^{2}}}^{2}f(x,y)dx', 1)\n        assert re.findall(r'(?m)^(\\d+)\\\\\\.', paper) == list(map(str, range(1, 23)))\n        pattern = re.compile(r'(?ms)^## ' + re.escape(title) + r'$.*?(?=^## |\\Z)')\n        current, count = pattern.subn(lambda m: paper + '\\n\\n', current)\n        assert count == 1\n    path.write_text(current.rstrip() + '\\n', encoding='utf-8')\n    print(path)\nfrom pathlib import Path\nimport re\n\n\nroot = Path('references/302模拟27md')\nfor kind in ['精编', '估分']:\n    path, = root.rglob(f'【A4紧凑_带答案】数二_{kind}10套模拟卷.pdf.md')\n    current = path.read_text(encoding='utf-8')\n    for number in [7, 8, 9]:\n        paper = Path(f'.question-bank-work/302-ten-two-v{number}.md').read_text(encoding='utf-8').strip()\n        heading = paper.splitlines()[0]\n        assert re.findall(r'(?m)^(\\d+)\\\\\\.', paper) == list(map(str, range(1, 23)))\n77:11\\. 设 $y=f(x)$ 由方程 $\\mathrm e^y+x=\\mathrm e\\cos(xy)$ 确定，则 $\\lim_{n\\to\\infty}\\left[f\\left(\\frac1n\\right)\\right]^{n(1-\\cos\\frac1n)}=$ ______。\n"}
{}
{"chunk_id":"74a062","wall_time_seconds":0.000008458,"exit_code":0,"original_token_count":124,"output":"references/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷10套整理合集PDF（可高清打印）/【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A3数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A4数二模拟卷精选20套.pdf.md\n"}

## tool · 2026-11-12T01:39:45Z


Script completed
Wall time 0.9 seconds
Output:

{}
{"chunk_id":"99e818","wall_time_seconds":0.712164042,"exit_code":0,"original_token_count":6,"output":"ten 32\ntw3 36\ntw4 33\n"}

## tool · 2026-11-12T01:39:58Z


Script completed
Wall time 0.8 seconds
Output:

{"chunk_id":"12e5fc","wall_time_seconds":0.000010834,"exit_code":0,"original_token_count":261,"output":"                for band in bands:\n                    kept[max(0, band[0]-3):band[-1]+4] = True\n                missing = np.flatnonzero((pixels < 150).any(axis=1) & ~kept)\n                if not len(missing):\n                    continue\n                groups = np.split(missing, np.where(np.diff(missing) > 35)[0] + 1)\n                for group in groups:\n                    crop = Image.fromarray(pixels[max(0, group[0]-35):group[-1]+60])\n                    panel = Image.new('L', (pix.width, crop.height+20), 'white')\n                    ImageDraw.Draw(panel).text((2, 2), f'{tag} p{page.number+1}', fill='black')\n                    panel.paste(crop, (0, 20))\n                    pieces.append(panel)\n    if pieces:\n        result = Image.new('L', (pieces[0].width, sum(p.height+10 for p in pieces)), 'white')\n        y = 0\n        for panel in pieces:\n            result.paste(panel, (0, y))\n            y += panel.height+10\n        result.save(f'.question-bank-work/302-proof-source/lost-ink-{tag}.png')\n    print(tag, len(pieces))\n"}
{}
{"chunk_id":"94129c","wall_time_seconds":0.56291425,"exit_code":0,"original_token_count":6,"output":"ten 32\ntw3 36\ntw4 33\n"}

## tool · 2026-11-12T01:40:08Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"8d462a","wall_time_seconds":0.000016958,"exit_code":0,"original_token_count":262,"output":"        else:\n            paper = Path(f'.question-bank-work/older-forty-zhang-{volume}.md').read_text(encoding='utf-8').strip()\n            paper = paper.replace(paper.splitlines()[0], f'## {title}', 1)\n            if volume == 5:\n                assert '\\\\sqrt{2} < x < 2' in paper\n                paper = paper.replace('\\\\sqrt{2} < x < 2', '\\\\sqrt{2} \\\\leq x \\\\leq 2', 1)\n                assert 'g(y_1, y_2, y_3)' in paper\n                paper = paper.replace('g(y_1, y_2, y_3)', 'g(y_1, y_2)', 1)\n            else:\n                old = '\\\\int_{\\\\sqrt{4-y^{2}}}^{2}f(x,y)dx'\n                assert old in paper\n                paper = paper.replace(old, '\\\\int_{-\\\\sqrt{4-y^{2}}}^{2}f(x,y)dx', 1)\n        assert re.findall(r'(?m)^(\\d+)\\\\\\.', paper) == list(map(str, range(1, 23)))\n        pattern = re.compile(r'(?ms)^## ' + re.escape(title) + r'$.*?(?=^## |\\Z)')\n        current, count = pattern.subn(lambda m: paper + '\\n\\n', current)\n        assert count == 1\n    path.write_text(current.rstrip() + '\\n', encoding='utf-8')\n    print(path)\n"}
{}
{"chunk_id":"1d3116","wall_time_seconds":0.000009084,"exit_code":0,"original_token_count":56,"output":"references/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A3数二模拟卷精选20套.pdf.md\nreferences/302模拟27md/模拟卷20套整理合集PDF（可高清打印）/A4数二模拟卷精选20套.pdf.md\n"}
{
  "type": "input_image",
  "image_url": "images/eb5809e4ed9dcfdea6a265912e36bab2e8cdfba9b46a47d5abc810e93eb0654c.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/d18a6f4b3040a04aa1d98d6f9765794fdbd125e16a06c9acb5a6329c5c35562a.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/6d908b7667dfa957c00e88b277c962c93ebd3518e112c19a0aa7ea3c9a2edca2.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/786d900d94dd96709f19aa5696900afc93c004ac00ea83cb3519c07280dfd8ef.png",
  "detail": "high"
}

## tool · 2026-11-12T01:40:14Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"335762","wall_time_seconds":0.000008625,"exit_code":0,"original_token_count":89,"output":"77:11\\. $\\lim_{x\\to0}\\frac{\\ln\\frac{\\sin x}{x}}{\\int_0^{x^2}(1+t)^{1/t}\\,\\mathrm dt}=$ ______。\n81:13\\. 曲线 $y=x\\mathrm e^{-\\frac1{x+1}}$ 的斜渐近线方程为 ______。\n83:14\\. 设 $f(x)$ 为连续函数，且 $x^2+y^2+z^2=\\int_x^y f(x+y-t)\\,\\mathrm dt$，则 $z\\left(\\frac{\\partial z}{\\partial x}+\\frac{\\partial z}{\\partial y}\\right)=$ ______。\n"}
{
  "type": "input_image",
  "image_url": "images/b496b907e4b7069ad60a9b5c453e54d266864d3b3c00f4a28eb4db1422f10065.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/e049753fa714276b51d0b525c491c4017443e49cb4926ee1e3f5e3b4f43d7cd7.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/e500bd04553dfa737ea171019645d51d0d388809027045b2f83021633d6162a4.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/fc0870ff8bb9087cbccf44b45d96465c7402f6f72a20d41dd65cdebbd86a7994.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/1bede36b3563179f68ab9a07743d2ae997a372308b546cfe83da1804c140ee1f.png",
  "detail": "high"
}

## tool · 2026-11-12T01:40:23Z




## tool · 2026-11-12T01:40:32Z


Script completed
Wall time 0.3 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/d4446788f73949e2db85b558097a687e41c10a0d6877e92257a2ec7d56ec3a5e.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/0084dd7fc35f07a42dc6c8efa9e14b98b9263fe42526121aa5db59c62cfafd39.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/b69d835b5a8c510c7cfb707046a6eb9313f9567e38e8cf3c865d480e10009487.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/c6250328969c2217cde60a17df28f43871a7b1e64a034163bb9c641f92999514.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/3b2a3a6c24937072716bd90e0cbf537dc6d7f3dfb8e497c3255811b1c254d96a.png",
  "detail": "high"
}
{"chunk_id":"a45435","wall_time_seconds":0.14153725,"exit_code":0,"original_token_count":63,"output":"5804 math expressions rendered\n【A4紧凑_带答案】数二_精编10套模拟卷.pdf.md 10 220\n【A4紧凑_带答案】数二_估分10套模拟卷.pdf.md 10 220\nA3数二模拟卷精选20套.pdf.md 11 242\nA4数二模拟卷精选20套.pdf.md 11 242\n"}

## tool · 2026-11-12T01:40:45Z




## tool · 2026-11-12T01:40:51Z




## tool · 2026-11-12T01:40:56Z




## tool · 2026-11-12T01:41:02Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"b6c163","wall_time_seconds":0.0000165,"exit_code":0,"original_token_count":1166,"output":"references/302模拟27/往年模拟卷选填精选\nreferences/302模拟27/往年模拟卷选填精选/【A4留白】数三模拟卷选填精选.pdf\nreferences/302模拟27/往年模拟卷选填精选/【A4留白】数二模拟卷选填精选.pdf\nreferences/302模拟27/往年模拟卷选填精选/数二答案/24合工大超越卷解析篇-数二.pdf\nreferences/302模拟27/往年模拟卷选填精选/【A4紧凑】数二模拟卷选填精选.pdf\nreferences/302模拟27/往年模拟卷选填精选/【A4紧凑】数三模拟卷选填精选.pdf\nreferences/302模拟27/往年模拟卷选填精选/【A4留白】数一模拟卷选填精选.pdf\nreferences/302模拟27/往年模拟卷选填精选/数一答案/24合工大超越卷解析篇-数一.pdf\nreferences/302模拟27/往年模拟卷选填精选/【A4紧凑】数一模拟卷选填精选.pdf\n.question-bank-work/older-topic-2-lilin-v2.md\n.question-bank-work/older-topic-candidate-1-zhang8-v6.md\n.question-bank-work/older-topic-2-zhang4-v1.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v1.md\n.question-bank-work/older-topic-candidate-1-zhang4-v1.md\n.question-bank-work/older-topic-candidate-1-lilin-v3.md\n.question-bank-work/older-topic-candidate-2-zhang4-v4.md\n.question-bank-work/older-topic-2-lilin-v1.md\n.question-bank-work/older-topic-candidate-1-zhang8-v5.md\n.question-bank-work/older-topic-2-zhang4-v2.md\n.question-bank-work/older-topic-1-zhang4-v4.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v2.md\n.question-bank-work/older-topic-candidate-1-zhang4-v2.md\n.question-bank-work/older-topic-candidate-2-zhang8-v3.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v3.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v6.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v7.md\n.question-bank-work/older-topic-candidate-1-lilin-v4.md\n.question-bank-work/older-topic-candidate-2-zhang8-v7.md\n.question-bank-work/older-topic-candidate-1-zhang8-v1.md\n.question-bank-work/older-topic-2-lilin-v4.md\n.question-bank-work/older-topic-candidate-2-zhang4-v1.md\n.question-bank-work/older-topic-candidate-2-zhang8-v6.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v6.md\n.question-bank-work/older-topic-1-zhang4-v1.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v7.md\n.question-bank-work/older-topic-candidate-1-zhang8-v4.md\n.question-bank-work/older-topic-2-zhang4-v3.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v3.md\n.question-bank-work/older-topic-candidate-1-zhang4-v3.md\n.question-bank-work/older-topic-candidate-1-lilin-v1.md\n.question-bank-work/older-topic-candidate-2-zhang8-v2.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v2.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v10.md\n.question-bank-work/older-topic-1-lilin-v1.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v9.md\n.question-bank-work/older-topic-candidate-2-zhang8-v8.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v8.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v10.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v8.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v9.md\n.question-bank-work/older-topic-candidate-2-lilin-v1.md\n.question-bank-work/older-topic-candidate-2-lilin-v4.md\n.question-bank-work/older-topic-candidate-2-lilin-v3.md\n.question-bank-work/assemble-older-topics.py\n.question-bank-work/older-topic-candidate-1-zhang8-v8.md\n.question-bank-work/older-topic-1-lilin-v2.md\n.question-bank-work/older-topic-1-lilin-v4.md\n.question-bank-work/older-topic-2-zhang4-v4.md\n.question-bank-work/prepare-older-topic-candidates.py\n.question-bank-work/older-topic-candidate-2-zhang4-v2.md\n.question-bank-work/older-topic-candidate-1-zhang8-v3.md\n.question-bank-work/older-topic-candidate-1-zhang4-v4.md\n.question-bank-work/older-topic-candidate-2-zhang8-v5.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v5.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v4.md\n.question-bank-work/older-topic-1-zhang4-v2.md\n.question-bank-work/older-topic-candidate-1-zhang8-v7.md\n.question-bank-work/older-topic-2-lilin-v3.md\n.question-bank-work/older-topic-candidate-2-zhang8-v1.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v1.md\n.question-bank-work/older-topic-candidate-1-lilin-v2.md\n.question-bank-work/older-topic-candidate-2-zhang8-v4.md\n.question-bank-work/older-topic-candidate-1-chaoyue-v4.md\n.question-bank-work/older-topic-candidate-2-chaoyue-v5.md\n.question-bank-work/older-topic-1-zhang4-v3.md\n.question-bank-work/older-topic-candidate-2-zhang4-v3.md\n.question-bank-work/older-topic-candidate-1-zhang8-v2.md\n.question-bank-work/older-topic-1-lilin-v3.md\n.question-bank-work/older-topic-candidate-2-lilin-v2.md\n"}

## tool · 2026-11-12T01:41:13Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"cf72aa","wall_time_seconds":0.232774958,"exit_code":0,"original_token_count":1100,"output":"## 24 超越十套卷· 卷一\n\n### 选择题\n\n1\\. 设函数 $f(x)=\\begin{cases}x^2, & x\\leq0, \\\\ \\ln x, & x>0, \\end{cases}$ 则函数 $f(f(x))$ ( ) .\nA. 无极值点  \nB. 有一个极小值点,无极大值点  \nC. 有一个极大值点,无极小值点  \nD. 有一个极小值点和一个极大值点  \n\n2\\. 设有积分 $I_1=\\int_0^1\\frac{\\sin x}{\\sqrt{1-x^2}}dx$, $I_2=\\int_0^1\\frac{\\cos x}{\\sqrt{1-x^2}}dx$, 则下列说法正确的是 ( ) .\nA. $I_1$ 发散, $I_2$ 收敛且 $I_2<1$  \nB. $I_1$ 收敛, $I_2$ 发散且 $I_1<1$  \nC. $I_1,I_2$ 均收敛且 $I_1<1,I_2<1$  \nD. $I_1,I_2$ 均收敛且 $I_1<1,I_2>1$  \n\n3\\. 一长方体的三条棱长分别用 x, y, z 表示, 若 x, z 分别以 $1\\,cm/s$ 和 $2\\,cm/s$ 的速率增加, y 以 $3\\,cm/s$ 的速率减少, 当 $x=1\\,cm, y=z=2\\,cm$ 时, 长方体的体积 V 对对角线长度 l 的变化率分别为 ( ).\nA. $\\frac{2}{3}$  \nB. $-\\frac{2}{3}$  \nC. $-6$  \nD. $6$  \n\n4\\. 设 $a=\\lim_{n \\to \\infty} n \\left[ e-\\left(1+\\frac{1}{n}\\right)^n \\right], b=\\lim_{n \\to \\infty} n \\left[\\frac{e}{\\left(1+\\frac{1}{n}\\right)^n} - 1 \\right]$, 则 ab=().\nA. e  \nB. $\\frac{e}{4}$  \nC. $2e$  \nD. $\\frac{e^2}{4}$  \n\n5\\. 设 $y=f(x)$ 在 $[a,b]$ ($b>a>0$) 上有连续导数, 若 $x=r(\\theta)\\cos\\theta, y=f(x)=r(\\theta)\\sin\\theta$, 且 $a=\\arctan\\frac{f(a)}{a}$, $\\beta=\\arctan\\frac{f(b)}{b}$, 则当 $\\int_a^b f(x)dx=0$ 时, $\\int_a^b r^2(\\theta)d\\theta=(\\quad)$.\nA. $bf(a)-af(b)$  \nB. $af(b)-bf(a)$  \nC. $bf(b)-af(a)$  \nD. $af(a)-bf(b)$  \n\n6\\. 设 $f(x,y)=\\begin{cases}\\frac{x^2y}{x^2+y^2}, & x^2+y^2 \\neq 0, \\\\ 0, & x^2+y^2=0,\\end{cases}$ 则 ( ) .\nA. $f_{xy}^{\\prime\\prime}(0,0),f_{yx}^{\\prime\\prime}(0,0)$ 均存在  \nB. $f_{xy}^{\\prime\\prime}(0,0),f_{yx}^{\\prime\\prime}(0,0)$ 均不存在  \nC. $f_{xy}^{\\prime\\prime}(0,0)$ 存在, $f_{yx}^{\\prime\\prime}(0,0)$ 不存在  \nD. $f_{xy}^{\\prime\\prime}(0,0)$ 不存在, $f_{yx}^{\\prime\\prime}(0,0)$ 存在  \n\n7\\. 设 $f(x,y)$ 具有一阶连续偏导数, 且 $\\frac{\\partial f}{\\partial x} > 0$, $\\frac{\\partial f}{\\partial y} < 0$. $D:0 \\leq x \\leq 1$, $0 \\leq y \\leq 1$, 则二重积分\n$I_{1} = \\iint_{D} f(x,y) d\\sigma, I_{2} = \\iint_{D} f(\\ln(1+x), y) d\\sigma, I_{3} = \\iint_{D} f(x, \\sin y) d\\sigma$ 的大小关系为 ( ).\nA. $I_{1} \\leq I_{2} \\leq I_{3}$  \nB. $I_{1} \\leq I_{3} \\leq I_{2}$  \nC. $I_{2} \\leq I_{1} \\leq I_{3}$  \nD. $I_{3} \\leq I_{2} \\leq I_{1}$  \n\n8\\. 设 $A, B$ 为 3 阶矩阵 $A$ 的伴随矩阵, 先将 $A$ 的第一行与第三行对调得到 $B$, 再将 $B$ 的第二列的一 2 倍加到第一列得到 $E$, 则 $\\left[2A + \\left(A^{*}\\right)^{*}\\right]^{-1} = (\\quad)$.\nA. $\\begin{pmatrix} 0 & 0 & 1 \\\\ 0 & 1 & 2 \\\\ 1 & 0 & 0 \\end{pmatrix}$  \nB. $\\begin{pmatrix} 0 & 0 & 1 \\\\ 0 & 1 & -2 \\\\ 1 & 0 & 0 \\end{pmatrix}$  \nC. $\\begin{pmatrix} 0 & 0 & 1 \\\\ -2 & 1 & 0 \\\\ 1 & 0 & 0 \\end{pmatrix}$  \nD. $\\begin{pmatrix} 0 & 0 & 1 \\\\ 1 & -2 & 0 \\\\ 0 & 1 & 0 \\end{pmatrix}$  \n\n9\\. 设 $A, B$ 为 $n$ 阶可逆的实对称矩阵.\n① $A, B$ 的列向量组具有相同的线性相关性; ② $A, B$ 的行向量组具有相同的线性相关性;\n③ 存在可逆矩阵 $P$, 使 $P^{T} A^{2} P = B^{2}$; ④ 存在可逆矩阵 $P$, 使 $P^{-1} A B P = B A$.\n以上说法正确的个数为 ( ).\nA. 1  \nB. 2  \nC. 3  \nD. 4  \n\n10\\. 设二次型 $f(x_{1}, x_{2}, \\cdots, x_{n}) = \\sum_{i=1}^{m} (a_{i1} x_{1} + a_{i2} x_{2} + \\cdots + a_{ii} x_{n})^{2}$ 的矩阵为 $B$, 记 $A = (a_{ij})_{m \\times n}$, 则当 ( )\n时, 二次型 $f = x^{T} B x$ 为正定二次型.\nA. $r(f) = m$  \nB. $r(f) = n$  \nC. $r(f) = r(A)$  \nD. $m = n$  \n### 填空题\n\n11\\.$\\lim_{n \\to \\infty} \\frac{\\sum_{k=1}^{n} \\frac{1}{k}}{\\ln n} =$ ___.\n\n12\\. 设 $xy = c_{1} e^{x} + c_{2} e^{2x}$ 是某二阶齐次线性微分方程的通解, 则该方程为 ___.\n\n13\\. 设 $z = z(u, v)$ 由方程 $z = e^{ua}$ 确定, $u = u(x)$, $v = v(x)$ 由方程组 $\\begin{cases} u^2 + 2v + e^x = 2, \\\\ u - v + x = 1 \\end{cases}$ 确定, 其中 $u > 0$, 则 $\\left.\\frac{dz}{dx}\\right|_{x=0} =$ ___.\n\n14\\. 设 $t > 0, F(t) = \\int_{-t}^{0} dx \\int_{0}^{t+t} x e^{y^2} dy + \\int_{0}^{t} dx \\int_{0}^{\\sqrt{t-t^2}} x e^{y^2} dy$, 则 $F'(1) =$ ___.\n\n15\\. 设函数 $f(x)$ 可导, $f(0) = 0$, 且 $f(x) = \\sin x^2 + 2x \\int_0^1 x f(x) dx - x \\lim_{x \\to 0} \\frac{f(x)}{x}$, 则 $\\int_0^1 x f(x) dx =$ ___.\n\n16\\. 设 3 阶矩阵 $A = \\begin{pmatrix} a & 2 & 2 \\\\ 0 & 1 & 2 \\\\ 0 & 0 & -1 \\end{pmatrix}$ 不能相似对角化, 则 $a =$ ___.\n"}

## tool · 2026-11-12T01:41:22Z


Script completed
Wall time 0.0 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/33f937311fa91fcf25ca2cb5a268014134c3c456276f6f1eb396eeeaee41140a.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/077ed34f1225a6d3f21bafeee88bcb48a1d1f810f7084c833175ad8174696f90.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/19593c8ee15c0b43b4235b44fa2dd183b70c6bca26dc1f37c39788841a9d3e3a.png",
  "detail": "high"
}

## tool · 2026-11-12T01:41:33Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"ca9a6d","wall_time_seconds":0.04169075,"exit_code":0,"original_token_count":149,"output":"(13) 设z = z u,v\n\n\n由方程z = euα 确定, u = u x\n\n\n, v = v x\n\n\n由方程组\nu2+2v+ex=2,\nu-v+x=1\n\n确定,其中u > 0,\n则dz\ndx x=0 = _____.\n(14) 设t > 0,F t\n\n\n=\n0\n-td\n\nx\nx+t\n0\nx\n\ney2dy +\nt\n0d\nx\nt2-τ2\n0\nx\n\ney2dy,则F1\n\n\n= _____.\n(15) 设函数f x\n\n\n可导, f 0\n\n\n= 0, 且f x\n\n\n= sinx2 + 2x\n1\n0 xf\n\nx\n\n\ndx - xlim\nx→0\nf x\n\n\nx\n, 则\n1\n0 xf\n\nx\n\n\ndx = ____.\n(16) 设3 阶矩阵A =\na\n2\n2\n0\n1\n2\n0\n0\n-1\n\n\n\n\n\n\n\n\n不能相似对角化, 则a = _____.\n第43 页，共94 页\n\n"}
{
  "type": "input_image",
  "image_url": "images/8ec8715f4b5643014c293f59fea590388d4568fee576504df99a51eef031c306.png",
  "detail": "high"
}

## developer · 2026-11-12T01:41:33Z

<image_resize_notice>
Image 1 of 1 in the preceding tool output was resized from 2222x360 to 2048x332 pixels.
</image_resize_notice>

## tool · 2026-11-12T01:42:25Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-11-12T01:42:35Z


Script completed
Wall time 0.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/16a9c1a8116c75b8f0672a51c9eba17e84d8bbb0fca663d297b2cf3e1e089b01.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/921a112e41789709f45409da1f5a2dd139e384a7251b72dbf7b8ff3b5442d66f.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/bb94cd0d2d2d995d5a188ef916b8a58566cb81c7ca1b0b7882c066c4ae94f0fb.png",
  "detail": "high"
}
{"chunk_id":"6f7141","wall_time_seconds":0.000010708,"exit_code":0,"original_token_count":1121,"output":"## 24 超越十套卷· 卷二\n\n### 选择题\n\n1\\. 关于数列 $\\{x_{n}\\}, (y_{n})$ 有以下论断\n①若数列 $\\{x_{2n}\\}$ 和 $\\{x_{2n-1}\\}$ 都收敛，则数列 $\\{x_{n}\\}$ 收敛；\n②若数列 $\\{x_{n}+y_{n}\\}$ 和 $\\{x_{n}-y_{n}\\}$ 都收敛，则数列 $\\{x_{n}\\}, \\{y_{n}\\}$ 均收敛；\n③若数列 $\\{x_{n}\\}$ 和 $\\{y_{n}\\}$ 都发散，则数列 $\\{x_{n}+y_{n}\\}$ 可能收敛；\n④若数列 $\\{x_{n}y_{n}\\}$ 收敛，则数列 $\\{x_{n}\\}$ 和 $\\{y_{n}\\}$ 必有一个收敛.\n以上结论中正确的个数为 (    ).\nA. 1  \nB. 2  \nC. 3  \nD. 4  \n\n2\\. 设 $F(x) = \\int_{-1}^{1} |x - t| e^{-t^2} dt - 1$，则函数 $F(x)$ 在定义域内的零点个数为 (    ).\nA. 0  \nB. 1  \nC. 2  \nD. 3  \n\n3\\. 已知反常积分 $\\int_{0}^{\\frac{\\pi}{2}} \\frac{\\ln x}{\\sin^p x \\cos^q x} dx$ ($p > 0, q > 0$) 收敛，则参数 $p, q$ 的取值范围为 (    ).\nA. $p > 0, q > 1$  \nB. $p > 1, q > 1$  \nC. $0 < p < 1, 0 < q < 1$  \nD. $0 < p \\leq 1, 0 < q \\leq 1$  \n\n4\\. 已知 $f(x)$ 为可导函数, $g(x)$ 为连续函数, 且 $f'(x) = e^{x^2} - 1 + \\int_{0}^{x} g(x-t) dt$, $\\lim_{x \\to 0} \\frac{g(x)}{x} = -3$, 则 (    ).\nA. x = 0 为 $f(x)$ 的极大值点  \nB. x = 0 为 $f(x)$ 的极小值点  \nC. $(0, f(0))$ 为曲线 y = f(x) 的拐点  \nD. x = 0 不是 $f(x)$ 的极值点, $(0, f(0))$ 也不是曲线 y = f(x) 的拐点  \n\n5\\. 设 $y = x e^x + x$ 是方程 $y'' + p y' + q y = a e^x + b$ 的一个特解, 下列函数中也是该方程的特解的是 (    ).\nA. $y = e^{2x} + x e^x + x$  \nB. $y = (x + 1) e^x + x$  \nC. $y = x e^x + 2x$  \nD. $y = 2 x e^x + x$  \n\n6\\. 设函数 $f(x,y)$ 在全平面内具有连续偏导数, 对任意的两点 $(x_1,y_1)$, $(x_2,y_2)$, 不等式 $\\left|f(x_1,y_1)-f(x_2,y_2)\\right|\\leqslant|x_1-x_2|+\\left|y_1-y_2\\right|$ 成立的一个充分条件为 ( ).\nA. $\\left|\\frac{\\partial f}{\\partial x}\\right|\\geqslant1$, $\\left|\\frac{\\partial f}{\\partial y}\\right|\\leqslant1$  \nB. $\\left|\\frac{\\partial f}{\\partial x}\\right|\\leqslant1$, $\\left|\\frac{\\partial f}{\\partial y}\\right|\\geqslant1$  \nC. $\\left|\\frac{\\partial f}{\\partial x}\\right|\\geqslant1$, $\\left|\\frac{\\partial f}{\\partial y}\\right|\\geqslant1$  \nD. $\\left|\\frac{\\partial f}{\\partial x}\\right|\\leqslant1$, $\\left|\\frac{\\partial f}{\\partial y}\\right|\\leqslant1$  \n\n7\\. 将极限 $\\lim_{n \\to \\infty} \\sum_{i=1}^{n} \\sum_{j=1}^{2n} \\frac{2i + j}{n^3}$ 化为二重积分, 不正确的是 ( ).\nA. $\\int_0^1 dx \\int_0^2 (2x + y) dy$  \nB. $\\int_0^2 dx \\int_0^1 (x + 2y) dy$  \nC. $\\int_0^1 dx \\int_0^1 2(x + y) dy$  \nD. $\\int_0^1 dx \\int_0^1 4(x + y) dy$  \n\n8\\. 设 $A$ 为 3 阶非零的反对称矩阵, 矩阵 $B = \\begin{pmatrix} a & 5 & 1 \\\\ 0 & 2 & 0 \\\\ 2 & b & 3 \\end{pmatrix}$, 且 $r(AB-A) = 1$, 则必有 ( ).\nA. $Ax = 0$ 仅有零解, $Bx = 0$ 仅有零解  \nB. $Ax = 0$ 有非零解, $Bx = 0$ 仅有零解  \nC. $Ax = 0$ 仅有零解, $Bx = 0$ 有非零解  \nD. $Ax = 0$ 有非零解, $Bx = 0$ 有非零解  \n\n9\\. 三元二次型 $f(x_1,x_2,x_3) = (x_1 + x_2 + 2x_3)(x_2 + ax_3)$, 则二次型的秩 $r(f) = (\\quad)$.\nA. 1  \nB. 2  \nC. 3  \nD. 依赖于 $a$ 的取值  \n\n10\\. 设 3 阶非零矩阵 $A$ 相似于一个对角阵, $A^*$ 为 $A$ 的伴随矩阵, 已知任意三维列向量均是 $A^*x = 0$ 的解, 则 $A$ 的非零特征值的个数为 ( ).\nA. 1  \nB. 2  \nC. 3  \nD. 不确定  \n\n### 填空题\n\n11\\. 设函数 $x = x(t)$ 由方程 $t \\cos x + x = 0$ 确定, $y = y(x)$ 由 $e^{y-2} - xy = 1$ 确定, 则 $\\left. \\frac{dy}{dt} \\right|_{t=0} = $ ___.\n\n12\\. 已知 $f(x)$ 是微分方程 $x^2f'(x) - xf(x) = \\sin^4x$ 满足初始条件 $f\\left(\\frac{\\pi}{2}\\right) = 0$ 的特解，则 $\\int_0^{\\frac{\\pi}{2}} x f(x) \\, dx =$ ___.\n\n13\\. 设 $f(x, y)$ 具有二阶连续偏导数，且满足 $\\frac{\\partial^2 f}{\\partial x^2} + \\frac{\\partial^2 f}{\\partial y^2} = 0$，$u = f\\left(\\frac{y - x}{xy}, \\frac{z - y}{yz}\\right)$，则 $x^2 \\frac{\\partial^2 u}{\\partial x \\partial y} + z^2 \\frac{\\partial^2 u}{\\partial z \\partial y} = $ ___.\n\n14\\. 设 $f(x, y)$ 在区域 $D:0 \\leq x \\leq 1, 0 \\leq y \\leq 1$ 上可微，且 $f(0,0) = 0, f_x'(0,0) = 1, f_y'(0,0) = 2$，则 $\\lim_{x \\to 0^+} \\frac{\\int_0^x dt \\int_{\\sqrt{x}}^x f(t,u) du}{x^4} = $ ___.\n\n15\\. 曲线 $f(x) = [x] \\sin \\pi x, (0 \\leq x \\leq 12), ([ \\cdot] \\text{表示取整}) \\text{绕} x \\text{轴旋转形成的旋转体的体积记作 } V =$ ___.\n\n16\\. 设 $A$ 是 4 阶实矩阵，$(A + 3E)x = 0$ 的基础解系为 $a_1, a_2, (A - E)x = 0$ 的基础解系为 $a_3$，则 $r(A^2 + 2A - 3E) = $ ___.\n"}

## tool · 2026-11-12T01:42:52Z


Script completed
Wall time 0.2 seconds
Output:

{}
{"chunk_id":"bc1aeb","wall_time_seconds":0.000011042,"exit_code":0,"original_token_count":62,"output":"78:14\\. 设 $f(x, y)$ 在区域 $D:0 \\leq x \\leq 1, 0 \\leq y \\leq 1$ 上可微，且 $f(0,0) = 0, f_x'(0,0) = 1, f_y'(0,0) = 2$，则 $\\lim_{x \\to 0^+} \\frac{\\int_0^{x^2} dt \\int_{\\sqrt{t}}^x f(t,u) du}{x^4} = $ ___.\n206 math expressions rendered\n"}

## tool · 2026-11-12T01:42:59Z




## tool · 2026-11-12T01:43:05Z


Script completed
Wall time 0.1 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/113668315affd7d054f2b13c0191d6defc5fa638a04ab8aa24601ff1e6cb0625.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/4f0d9d21d1bf504e8e300d4ad1e8435688c1996e11f0ecf7b7a18be671dc00e7.png",
  "detail": "high"
}
{
  "type": "input_image",
  "image_url": "images/f3b4181cf4b5b21f1d3d07b10cf337094d1686f6a8ec1182d5e06be37ed459b8.png",
  "detail": "high"
}
{"chunk_id":"7465e8","wall_time_seconds":0.00000975,"exit_code":0,"original_token_count":1107,"output":"## 24 超越十套卷· 卷三\n\n### 选择题\n\n1\\. 曲线 $f(x)=x\\cdot\\left[\\frac{2}{x}\\right](\\cdot)$ 表示取整函数) 的渐近线有( ).\nA. 1 条  \nB. 2 条  \nC. 3 条  \nD. 4 条  \n\n2\\. 对于 $\\{a_n\\}$, $n=1,2,\\cdots$, 以下命题:\n①若 $0<a_n<1$, 则 $\\lim_{n \\to \\infty} a_n^n = 0$; ②若 $\\lim_{n \\to \\infty} \\sqrt[n]{a_n} = 1$, 则 $\\lim_{n \\to \\infty} a_n$ 必存在且大于 0;\n③若 $\\lim_{n \\to \\infty} a_n = +\\infty$, 则 $\\lim_{n \\to \\infty} \\sqrt[n]{a_n} = +\\infty$; ④若 $a_n > 0, \\lim_{n \\to \\infty} a_n$ 存在且大于 0, 则 $\\lim_{n \\to \\infty} \\sqrt[n]{a_n} = 1$.\n不正确的序号为().\nA. ①②  \nB. ②③  \nC. ①③④  \nD. ①②③  \n\n3\\. 设 $f(x)$ 是在 $(-\\infty, +\\infty)$ 内以 T 为周期的连续函数, 以下命题中正确的个数为().\n①若 $\\int_0^T f(x) \\, dx = 0$, 则 $\\int_0^T f(t) \\, dt$ 是以 T 为周期的函数;\n②若 $f(x)$ 是奇函数, 则 $\\int_0^T f(t) \\, dt$ 是以 T 为周期的函数;\n③若 $\\int_0^{+\\infty} f(x) \\, dx$ 收敛, 则 $\\int_0^T f(t) \\, dt$ 是以 T 为周期的函数;\n④函数 $F(x) = \\int_0^T [f(t) - f(-t)] \\, dt$ 是以 T 为周期的函数.\nA. 1  \nB. 2  \nC. 3  \nD. 4  \n\n4\\. 设 $f(x) = x(x \\geqslant 0)$, $g(x) = \\begin{cases} \\cos^3 x, & 0 \\leqslant x \\leqslant \\pi, \\\\ 0, & x > \\pi. \\end{cases}$ $F(x) = \\int_0^T f(t) \\, dt$ (x $\\geqslant 0$), 下列说法正确的是().\nA. $F(x)$ 既有极值点又有拐点  \nB. $F(x)$ 无极值点, 有拐点  \nC. $F(x)$ 有极值点, 无拐点  \nD. $F(x)$ 即无极值点又无拐点  \n\n5\\. 函数 $y = y(x)$ 由参数方程 $\\begin{cases} x = \\lim_{n \\to \\infty} \\sqrt[n]{t^n + t^{2n}} + \\mathrm{e}^{t-1}, & (n > 0) \\text{所确定}, \\text{函数} y = y(x) \\text{在点} x = 2 \\text{处}( )\\text{.} $\nA. 左导数不存在  \nB. 右导数不存在  \nC. 左导数和右导数均存在但不相等  \nD. 可导  \n\n6\\. 设 $a, b$ 为实数, $f(x, y) = \\begin{cases} \\dfrac{a(x+y) + bx^2y}{x^2 + y^2}, & x^2 + y^2 \\neq 0, \\\\ 0, & x^2 + y^2 = 0, \\end{cases}$ 则 $f(x, y)$ 在点 $(0, 0)$ 处连续, 且偏导数存在\n\n的充分必要条件为 (  ).\nA. $a = b = 0$  \nB. $a = 0, b$ 为任意常数  \nC. $b = 0, a$ 为任意常数  \nD. $a, b$ 均为任意常数  \n\n7\\. 极坐标系下二次积分 $\\int_{\\frac{\\pi}{3}}^{\\frac{2\\pi}{3}} d\\theta \\int_0^2 r^2 (1 - \\sin 2\\theta) \\cdot r dr$ 化为直角坐标系下二次积分为 (  ).\nA. $\\int_{-1}^{0} dx \\int_{-\\sqrt{3}x}^{\\sqrt{4-x^2}} (x^2 + y^2) dy$  \nB. $\\int_0^1 dx \\int_{\\sqrt{3}x}^{\\sqrt{4-x^2}} (x^2 + y^2) dy$  \nC. $2 \\int_{-1}^{0} dx \\int_{\\sqrt{3}x}^{\\sqrt{4-x^2}} (x^2 + y^2) dy$  \nD. $2 \\int_0^1 dx \\int_{\\sqrt{3}x}^{\\sqrt{4-x^2}} (x^2 + y^2) dy$  \n\n8\\. 设 $a$ 为 3 维实列向量, 且 $a^T a = 1, B = a a^T, A$ 为 3 阶不可逆矩阵, 且 $A + 2B - AB = 2E$, 则 $A$ 的特征值为 (  ).\nA. 2, 2, 2  \nB. 2, 2, 0  \nC. 1, 1, 0  \nD. 2, 2, 0  \n\n9\\. 设 $A$ 为 3 阶实对称可逆矩阵, 将 $A$ 的第一行的 2 倍加到第三行, 再将第一行乘 2 得到 $B$, 将矩阵 $B$ 的第一列的 2 倍加到第三列, 再将第一列乘 2 得到矩阵 $C$, 则矩阵 $A^*$ 与 $C^*$ (  ).\nA. 合同但不相似  \nB. 相似但不合同  \nC. 合同且相似  \nD. 不合同也不相似  \n\n10\\. 设 $a_1, a_2, a_3$ 是齐次方程组 $A_n x = 0$ 的基础解系, $\\beta_1$ 是非齐次方程组 $A_x = a_1$ 特解, $i = 1, 2, 3$, 则 (  ).\nA. $\\beta_1, \\beta_2, \\beta_3$ 线性相关  \nB. $\\beta_1, \\beta_2, \\beta_3$ 线性无关  \nC. $\\beta_1, \\beta_2, \\beta_3$ 可由 $a_1, a_2, a_3$ 线性表示  \nD. $a_1, a_2, a_3$ 可由 $\\beta_1, \\beta_2, \\beta_3$ 线性表示  \n\n### 填空题\n\n11\\. 当 $x \\to 0$ 时, 若 $1 - \\dfrac{n+1}{1 + e^x + e^{2x} + \\cdots + e^{nx}}$ 与 $\\sin x$ 为等价无穷小, 则自然数 $n = $ ___.\n\n12\\. 设 $f(x)=\\frac{1}{x+\\sqrt{1+x^2}}$，其反函数记作 $f^{-1}(x)$，则 $\\int_{0}^{+\\infty}f^{-1}(x)dx$。\n\n13\\. 设 $F(x)=\\int_{x^2}^{1}\\frac{t}{\\sqrt{1+t^3}}dt$，则 $\\int_{0}^{1}xF(x)dx=$ ___。\n\n14\\. 当 y>0 时，有 $\\frac{\\partial^2 z}{\\partial x \\partial y}=x^2e^{xy}$，且 $\\left.\\frac{\\partial z}{\\partial x}\\right|_{y=0}=x+\\sin x,z(0,y)=-\\frac{1}{y^2}$，则 $z(x,y)=$ ___。\n\n15\\. 设函数 $f(x)$ 连续，且满足 $\\int_{0}^{x}f(t)dt=1-f(x)-e^{-x}$，则 $f^{(n)}(x)=$ ___。\n\n16\\. 设 $A$ 是 3 阶实对称矩阵，$a=(-a,4,a+1)^T$ 与 $\\beta=(a+1,a-3,3)^T$ 分别是齐次线性方程组 $(A-2E)x=0$ 与 $(A+3E)x=0$ 的解，其中 $E$ 为 3 阶单位阵，则 $a=$ ___。\n"}

## tool · 2026-11-12T01:43:45Z


Script completed
Wall time 0.2 seconds
Output:

{}
{}
{"chunk_id":"5f0141","wall_time_seconds":0.000009333,"exit_code":0,"original_token_count":8,"output":"92 math expressions rendered\n"}
