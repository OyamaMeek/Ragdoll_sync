# 01a154b8-b815-7642-9e24-92f560b1760e

来源：codex

项目：/Users/oyamahappa/Documents/Agent/Codex

## developer · 2026-10-19T15:12:36Z

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

Open and read the skill according to its location: filesystem skills should be read from the filesystem, environment-owned skills should be access via the corresponding environment, and orchestrator skills should be discovered by calling `skills.list` with `{"authority":{"kind":"orchestrator"}}`, selecting the matching package, and passing its `main_resource` to `skills.read`. Avoid re-reading skills when possible. 

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



## developer · 2026-10-19T15:12:36Z

<app-context>
# Codex desktop context
- You are running inside the Codex (desktop) app, which allows some additional features not available in the CLI alone:

### Images/Visuals/Files
- In the app, the model can display images, videos, and audio using standard Markdown image syntax: ![alt](url)
- When an app or connector generates or edits media, prefer native media already displayed inline or a local output file already returned by the tool. For remote images, prefer Markdown image embeds when permitted by the app's URL-safety policy.
- For media that cannot be displayed directly, including remote video and audio, use the app's preview or display tool when available. Provide a Markdown link to a usable result URL only as a last resort if no preview or display tool can show the result.
- Do not download remote media to work around display restrictions.
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
- This app supports recurring automations, reminders, monitors, follow-ups, and thread wakeups. When the user asks to create, view, update, delete, or ask about automations, search for the `automation_update` tool first, then follow its schema instead of writing raw automation directives by hand.
- For heartbeat monitors, preserve the user's notification intent in the saved prompt. Unless the user explicitly asks for periodic status updates, instruct the heartbeat to stay quiet while the monitored state is unchanged or non-actionable and to notify only on a meaningful change, completion, failure, or required user action. Do not add instructions such as "leave a brief status update" on every run.
- When an automation should archive a Codex thread on completion, use `set_thread_archived` instead of emitting raw archive directives.

### Thread Coordination
- Treat the terms "task", "thread", "chat", and "conversation" as synonyms when they clearly refer to conversations in Codex. Use "chat" when referring to conversations in the product. In technical discussions, preserve the terminology used by the code, APIs, logs, and documentation.
- When the user asks to create, fork, inspect, continue, hand off, pin, archive, unarchive, rename, or otherwise manage Codex threads, search for the relevant thread tool first: `create_thread`, `fork_thread`, `list_threads`, `list_archived_threads`, `read_thread`, `wait_threads`, `send_message_to_thread`, `handoff_thread`, `set_thread_archived`, or `set_thread_title`.
- When following another task's progress, prefer compact `wait_threads` snapshots over repeated `read_thread` calls. Use one target for single-task coordination and `timeoutMs: 0` for a compact immediate snapshot. `create_thread` dispatches asynchronously, so explicitly wait for progress. Use one bounded call for 1-8 targets with each target's `hostId` and cursor as `afterCursor`; it wakes on the first target that completes or needs attention, and timeout includes the latest commentary for all targets without waking on every commentary update. An up-to-date cursor suppresses already-delivered final text. Separate waits from one task may run serially. Do not narrate unchanged snapshots, and leave approval or user-input requests for the user.
- Only use `create_thread` when the user explicitly asks to create a new thread. Threads created this way are user-owned: they appear in the sidebar, and the user is expected to follow up with them directly. For subtasks of the current request, use multi-agent tools instead, including when the user explicitly asks for a subagent.
- After a successful `create_thread` call, emit `::created-thread{threadId="..."}` for a created thread or `::created-thread{clientThreadId="..."}` for queued worktree setup on its own line in your final response.

### Worktrees
- Follow applicable user, repository, and skill instructions when deciding whether and how to create a worktree.
- Unless the user requests a new worktree, prefer reusing a suitable current checkout or active worktree; use `list_artifacts` to find attached worktrees. An existing worktree's name need not match the new task.
- Prefer `create_worktree` for new worktrees. For worktrees created with it, use `archive_worktree` when they are no longer needed. Use `restore_worktree` to recover archived work.

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

### Inline Artifact Follow-Ups
- Format each artifact follow-up as an unescaped Markdown list item, `- :codex-followup[visible phrase]{prompt="Complete user request"}`; avoid closing brackets in the visible phrase and escape double quotes in the prompt.

### Git
- Branch prefix: `codex/`. Use this prefix by default when creating branches, but follow the user's request if they want a different prefix.
</app-context>
<skills_instructions>
## Skills
A skill is a set of local instructions to follow that is stored in a `SKILL.md` file. Below is the list of skills that can be used. Each entry includes a name, description, and a short path that can be expanded into an absolute path using the skill roots table.
### Skill roots
- `r0` = `/Users/oyamahappa/.codex/skills`
- `r1` = `/Users/oyamahappa/.agents/skills`
- `r2` = `/Users/oyamahappa/.codex/skills/.system`
- `r3` = `/Users/oyamahappa/.codex/plugins/cache/ars-codex`
- `r4` = `/Users/oyamahappa/.codex/plugins/cache/openai-bundled`
- `r5` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote`
- `r6` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/google-drive/0.1.22/skills`
- `r7` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/notion/3.0.1/skills`
- `r8` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/superpowers/6.4.2/skills`
- `r9` = `/Users/oyamahappa/.codex/plugins/cache/openai-curated-remote/work-pets/0.1.6/skills`
- `r10` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime`
- `r11` = `/Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.1015.12040/skills`
- `r12` = `/Users/oyamahappa/.codex/plugins/cache/ponytail/ponytail/5.3.2/skills`
- `r13` = `/Users/oyamahappa/.codex/plugins/cache/reverse-skill-local`
- `r14` = `/Users/oyamahappa/.codex/plugins/cache/sepia/sepia/0.12.4/skills`
- `r15` = `/Users/oyamahappa/.codex/plugins/cache/superpowers-dev/superpowers/7.0.0/skills`
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI-created bitmap visuals such as photos, illustrations, textures, sprites, mockups, or transparent-background cutouts. Use when Codex should create a brand-new image, transform an existing image, or derive visual variants from ref (file: r2/imagegen/SKILL.md)
- openai-docs: Use for Codex models/pricing, scheduled tasks, skills, settings, setup, troubleshooting, customization, automations, and self-knowledge—including 'you,' 'your,' 'this app,' or 'this coding agent' when they refer to Codex—and for OpenAI APIs/products and ChatGPT Work. Also use for model c (file: r2/openai-docs/SKILL.md)
- skill-creator: Create or update a Codex skill with appropriately scoped instructions and any needed supporting resources. (file: r2/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list or a GitHub repo path. Use when a user asks to list installable skills, install a curated skill, or install a skill from another repo (including private repos). (file: r2/skill-installer/SKILL.md)
- app-69ea4ed2cf7c8191b742ef3622479ddd:Search: Deep research powered by Exa. Use for lead generation, literature reviews, deep dives, competitive analysis, or any query where one search falls short, including phrases like 'research this', 'find everything about', 'find me all', or 'deep dive on'. (file: r5/app-69ea4ed2cf7c8191b742ef3622479ddd/4.0.1/skills/Search/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, translated for the web. Use when building or reviewing gesture-driven UI, spring animations, drag/swipe/sheet interactions, momentum and interruptible transitions, translucent materials and depth, typography (optical sizing,  (file: r1/apple-design/SKILL.md)
- apple-design: Apple's approach to interface design and fluid, physical motion, translated for the web. Use when building or reviewing gesture-driven UI, spring animations, drag/swipe/sheet interactions, momentum and interruptible transitions, translucent materials and depth, typography (optical sizing,  (file: r0/apple-design/SKILL.md)
- archify: Create polished, validated architecture, workflow, sequence, data-flow, and lifecycle/state diagrams as explorable standalone HTML with inline SVG, dark/light themes, optional trace motion, and PNG/JPEG/WebP/SVG/WebM export. Accept plain-language requirements or pasted Mermaid flowchart, (file: r0/archify/SKILL.md)
- ars-codex:academic-research-suite: ARS-Codex research, writing, manuscript review, study screening, and experiments. Use for deep research, literature or systematic reviews, meta-analysis, research questions, drafts, revisions, roadmaps, abstracts, citations, integrity checks, peer review, research-to-paper. Screen records: (file: r3/ars-codex/3.23.1/skills/academic-research-suite/SKILL.md)
- benchmark-paper-template: Structures Benchmark and Evaluation papers using the five-pillar framework (Research Gap, Construction Pipeline, Evaluation Framework, Empirical Findings, optional Companion Method). Returns a completeness audit, a six-part Introduction logic chain, a Section 2-7 skeleton, and a pre-submis (file: r0/benchmark-paper-template/SKILL.md)
- brandkit: Premium brand-kit image generation skill for creating high-end brand-guidelines boards, logo systems, identity decks, and visual-world presentations. Trained for minimalist, cinematic, editorial, dark-tech, luxury, cultural, security, gaming, developer-tool, and consumer-app brand systems. (file: r0/brandkit/SKILL.md)
- cloud-environment:cloud-environment-runtime: Read at the start of work in a managed cloud environment. Inspect network policy and configured credentials; build and run Docker containers with the session proxy and CA trust; use Tailscale VPN access, configure TCP forwarding, and diagnose access failures. (file: r5/cloud-environment/0.1.2/skills/runtime/SKILL.md)
- contributor: GitHub 开源贡献辅助技能：围绕目标岗位和技术栈发现合适的开源项目与真实问题，评估维护状态、贡献规则和重复风险，准备最小可验证改动，经用户逐项确认后 fork、push、提交 PR，并跟踪 CI、review 和合并状态；当用户输入“/contributor”、想寻找项目、做 first contribution 或提交 PR 时使用。 (file: r0/contributor/SKILL.md)
- convert-documents-to-markdown: Convert Word (.doc, .docx), PowerPoint (.ppt, .pptx), Excel (.xls, .xlsx), OpenDocument (.odt, .ods, .odp), RTF, EPUB, CSV, and PDF files to GitHub-Flavored Markdown. Use when a task needs the contents of an office document, spreadsheet, presentation, ebook, or PDF you cannot read direct (file: r1/convert-documents-to-markdown/SKILL.md)
- deep-research: Runs a deep, survey-grade literature investigation on a research topic: freezes research questions, searches from multiple adversarial perspectives, verifies every citation, synthesizes evidence into a MECE taxonomy with in-sentence cross-comparison, and answers the research questions in (file: r0/deep-research/SKILL.md)
- design-taste-frontend: tasteskill v2, the anti-slop frontend skill. Art direction for websites, distilled from a study of 247 curated gallery sites (One Page Love, Awwwards Sites of the Day). Deals researched directions (idea, composition, type, palette, photographs, section blueprints) from a library, enforces  (file: r0/taste-skill/SKILL.md)
- design-taste-frontend-v1: The original v1 taste-skill, preserved for projects depending on its exact behavior. The current default is `design-taste-frontend` (v2), which is a new skill. Use this v1 install name only if you need exact backward compatibility. (file: r0/taste-skill-v1/SKILL.md)
- design-taste-frontend-v2-experimental: Old v2 (experimental) of taste-skill, the single-file dial-driven version, preserved for projects depending on its exact behavior. The current default is `design-taste-frontend` (v2). Use this install name only if you need the earlier behavior. Anti-slop frontend rules for landing page (file: r0/taste-skill-v2-experimental/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Google Docs-targeted document artifacts inside the container, with a strict render-and-verify workflow. Use `render_docx.py` to generate page PNGs (and optional PDF) for visual QA, then iterate until layout is flawless before del (file: r10/documents/26.1015.12040/skills/documents/SKILL.md)
- drawio-reconstruction: Reconstructs reference images into high-fidelity, editable Draw.io files with rendered previews: native Draw.io elements carry text and structure, SVG covers simple icons that match the reference, and cropped or transparent PNGs preserve complex visuals. Use when the user wants a diagram (file: r0/drawio-reconstruction/SKILL.md)
- drawio-skill: Create, edit, synchronize, inspect, test, and publish editable draw.io diagrams. Use when the user explicitly requests draw.io/diagrams.net, needs a polished architecture, ERD, UML, sequence, C4, SysML, BPMN, network, swimlane, ML, or infrastructure diagram, wants code/IaC/SQL/OpenAPI/ (file: r0/drawio-skill/SKILL.md)
- ego-browser: When you need a browser, read this Skill by default. Use it to open and operate websites, fill forms, click buttons, take screenshots, extract page data, sign in, and perform other browser automation tasks, as well as web app testing, dogfooding, QA, bug investigation, and app-quality re (file: r1/ego-browser/SKILL.md)
- evidence-recap: 把 AI 编程对话和项目交付材料复盘为可核验的九段证据链，区分问题、决策、个人动作、交付阶段、效果证据与责任边界。当用户运行 /evidence-recap、$evidence-recap，或明确要求复盘 AI 编程过程、交付记录、落地状态和证据缺口时使用；仅需简历改写、源码导学或模拟面试时不使用。 (file: r0/evidence-recap/SKILL.md)
- figure-designer: Advises on the design of the three core figures in a technical paper: the Motivated Example (Figure 1), the Solution Overview (Methodology), and the Experimental Results figures. Recommends the right design paradigm, layout, labelling, and tool for each figure type, then runs a quality-c (file: r0/figure-designer/SKILL.md)
- full-output-enforcement: Overrides default LLM truncation behavior. Enforces complete code generation, bans placeholder patterns, and handles token-limit splits cleanly. Apply to any task requiring exhaustive, unabridged output. (file: r0/output-skill/SKILL.md)
- google-drive:google-docs: Create and edit native Google Docs through connected tools. (file: r6/google-docs/SKILL.md)
- google-drive:google-drive: Use connected Google Drive as the single entrypoint for Drive, Docs, Sheets, and Slides work. Use when the user wants to find, fetch, organize, share, export, copy, or delete Drive files, or summarize and edit Google Docs, Google Sheets, and Google Slides through one unified Google Drive  (file: r6/google-drive/SKILL.md)
- google-drive:google-drive-comments: Write, reply to, and resolve Google Drive comments on Docs, Sheets, Slides, and Drive files with evidence-backed location context. Use when the user asks to leave comments, review a file with comments, respond to comment threads, or resolve Drive comments. (file: r6/google-drive-comments/SKILL.md)
- google-drive:google-sheets: Analyze and edit connected Google Sheets with range precision. Use when the user wants to create Google Sheets, find a spreadsheet, inspect tabs or ranges, search rows, plan formulas, create or repair charts, clean or restructure tables, write concise summaries, or make explicit cell-ra (file: r6/google-sheets/SKILL.md)
- google-drive:google-slides: Route Google Slides authoring requests and derive a design system from a native template or reference deck. Use this skill when the user provides an existing native Google Slides deck as a template, reference, or prior-period source, or asks to edit, update, repair, restyle, or clean up (file: r6/google-slides/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt templates from the awesome-gpt-image-2 style library. Use when an agent needs to create, rewrite, classify, or improve image-generation prompts with repository-backed templates, categories, style tags, scene tags, pitfal (file: r1/gpt-image-2-style-library/SKILL.md)
- gpt-image-2-style-library: Choose GPT-Image2 / gpt-image-2 visual styles and industrial prompt templates from the awesome-gpt-image-2 style library. Use when an agent needs to create, rewrite, classify, or improve image-generation prompts with repository-backed templates, categories, style tags, scene tags, pitfal (file: r0/gpt-image-2-style-library/SKILL.md)
- gpt-taste: Elite UX/UI & Advanced GSAP Motion Engineer. Enforces Python-driven true randomization for layout variance, strict AIDA page structure, wide editorial typography (bans 6-line wraps), gapless bento grids, strict GSAP ScrollTriggers (pinning, stacking, scrubbing), inline micro-images, and (file: r0/gpt-tasteskill/SKILL.md)
- great-resume: 中文求职经历提升技能：根据目标岗位把真实经历重组为岗位定位、简历要点、项目亮点和 HR 开场白；当用户输入“/great-resume”“我要酥化”或“简历提升”、要求包装或改写经历、项目，或写 HR 自我介绍时使用。若用户明确要求“阿酥同款”、复刻简历模板或生成对应 HTML/PDF，则交给 /make-resume。 (file: r0/great-resume/SKILL.md)
- high-end-visual-design: Teaches the AI to design like a high-end agency. Defines the exact fonts, spacing, shadows, card structures, and animations that make a website feel expensive. Blocks all the common defaults that make AI designs look cheap or generic. (file: r0/soft-skill/SKILL.md)
- human-writing: 通用中文创作与改稿 Skill。用于知乎回答、论坛长帖、公众号文章、博客、评论、人物故事、历史叙事、新闻与行业解读、科普、教程、评测、个人叙事、小说、故事、对白、口播和演讲稿。默认写成一个见过事、查过材料、愿意把来龙去脉讲清楚的人在说话，重点保留中文互联网长回答与长帖的活人感和自然中文韵律，避免空泛的机构腔、喊口号式演说腔、营销腔和模型腔。非虚构长文先检查材料够不够，材料不足时研究、追问或缩短，绝不用重复解释灌字数。现实内容额外核验事实、引语、数据与用户亲历，虚构内容可以创造人物、场景、对白、心理与情节。成稿正文严禁冒号、破折号、“不是……而是……”及同类翻案句，并 (file: r0/human-writing/SKILL.md)
- idea-evaluator: Evaluates a preliminary research idea against a five-dimension framework (Higher, Faster, Stronger, Cheaper, Broader) plus idea-lifecycle and student-capability matching, paradigm-shift probing, and a fatal-flaws audit. Returns a reviewer-style verdict; non-STEM ideas route to substitu (file: r0/idea-evaluator/SKILL.md)
- image-to-code: Elite website image-to-code skill for Codex. For visually important web tasks, it must first generate the design image(s) itself, deeply analyze them, then implement the website to match them as closely as possible. In Codex, it must prefer large, readable, section-specific images inst (file: r0/image-to-code-skill/SKILL.md)
- imagegen-frontend-mobile: Elite mobile app image-generation skill for creating premium, app-native screen concepts and flows. Designed for iOS, Android, and cross-platform mobile products. Prioritizes clean hierarchy, comfortably readable text, strong multi-screen consistency, controlled color palettes, non-gen (file: r0/imagegen-frontend-mobile/SKILL.md)
- imagegen-frontend-web: Elite frontend image-direction skill for generating premium, conversion-aware website design references. CRITICAL OUTPUT RULE — generate ONE separate horizontal image FOR EVERY section. A landing page with 8 sections produces 8 images. Never compress multiple sections into one image. E (file: r0/imagegen-frontend-web/SKILL.md)
- industrial-brutalist-ui: Raw mechanical interfaces fusing Swiss typographic print with military terminal aesthetics. Rigid grids, extreme type scale contrast, utilitarian color, analog degradation effects. For data-heavy dashboards, portfolios, or editorial sites that need to feel like declassified blueprints. (file: r0/brutalist-skill/SKILL.md)
- interview: 中文简历与目标岗位驱动的面试预测、模拟追问和复练技能：提取需要验证的经历 Claim，按面试轮次建立问题与评分契约，通过一次一问、证据反馈和弱项复练检查真实掌握程度；当用户输入“/interview”、要求面试预测、模拟面试、简历追问、压力面、场景设计题或检查面试掌握程度时使用。 (file: r0/interview/SKILL.md)
- intro-drafter: Drafts the Introduction prose for a technical paper, guided internally by a six-paragraph flowchart: background and running example, existing limitations, problem essence and goal, key challenges, solution overview, contributions. Positions the paper as Technique or New Problem/Setting,  (file: r0/intro-drafter/SKILL.md)
- job-apply: 中文求职申请自动填写技能：使用浏览器读取用户确认的简历资料，逐项填写招聘网站申请表并核对结果；当用户输入“/job-apply”、要求自动填简历或填写求职申请时使用。 (file: r0/job-apply/SKILL.md)
- job-match: 中文岗位匹配分析技能：对照目标 JD 与用户已确认的简历、经历或主张—证据账本，区分已匹配、证据不足和真实缺口，生成可解释的投递建议与后续 skill 交接；当用户输入“/job-match”、要求分析岗位适配度、JD 匹配、简历差距或判断是否值得投递时使用。需要改写简历时交给 /great-resume，需要模拟面试时交给 /interview。 (file: r0/job-match/SKILL.md)
- make-resume: 中文可编辑简历制作技能：默认基于 ASu 单栏高密度技术简历模板，根据用户经历制作或复刻可编辑 HTML/PDF；用户也可以指定仓库内其他模板、本地 HTML 或参考截图。用户输入“/make-resume”“我要阿酥同款简历”或要求制作、修改、复刻简历文件时使用；用户要求 LaTeX、`.tex` 或 Overleaf 版本时，在默认 HTML 交付之外附加导出 `.tex` 源文件。 (file: r0/make-resume/SKILL.md)
- minimalist-ui: Clean editorial-style interfaces. Warm monochrome palette, typographic contrast, flat bento grids, muted pastels. No gradients, no heavy shadows. (file: r0/minimalist-skill/SKILL.md)
- notion:notion-database-designer: Turns scattered notes and recurring work into useful Notion trackers for requests, content plans, or team work. Use to set up or improve a tracker, choosing its fields and views from the user's needs; ordinary record updates belong to the task's workflow. (file: r7/notion-database-designer/SKILL.md)
- notion:notion-meeting-intelligence: Prepares Notion meeting agendas, pre-reads, decision briefs, and follow-up actions. Use for meeting preparation, carrying context into recurring meetings, or turning meeting outcomes into next steps. Simple meeting lookups or saving notes verbatim do not need this workflow. (file: r7/notion-meeting-intelligence/SKILL.md)
- notion:notion-research-documentation: Synthesizes Notion workspace evidence into cited answers, comparisons, briefs, or reports. Use to investigate a question, connect findings across sources, or reconcile conflicting information, with external research when useful. Simple lookups, fetching a known page, or summarizing one su (file: r7/notion-research-documentation/SKILL.md)
- notion:notion-spec-to-implementation: Converts Notion product or technical specs into implementation plans, linked tasks, and evidence-based progress updates. Use for planning or implementing a spec, creating tasks from requirements, or reconciling implementation with spec changes. (file: r7/notion-spec-to-implementation/SKILL.md)
- notion:notion-weekly-project-digest: Produces evidence-based weekly project or team updates by comparing reporting periods, tasks, decisions, and blockers in Notion. Use for recurring status digests; use spec-to-implementation for requirement-level implementation tracking. (file: r7/notion-weekly-project-digest/SKILL.md)
- offer: 中文秋招求职进度管理技能：记录和更新投递、筛选、测评、面试、Offer、拒信及招聘邮件状态，生成可搜索的进度表；当用户输入“/offer”或要求管理秋招进度时使用。 (file: r0/offer/SKILL.md)
- paper-polish: Polishes existing academic prose while preserving the author's meaning: grammar and flow repair, tone calibration against evidence strength, AI-tone removal, and Chinese-to-English rewriting at submission quality. Never fabricates data, citations, or claims, and flags any edit that cou (file: r0/paper-polish/SKILL.md)
- paper-writer: Drafts publishable paper prose from the author's own materials, from a single paragraph to a full manuscript, across STEM and non-STEM fields. Every factual claim traces to user input, verified retrieval, or field common knowledge; citations pass an independent verification ladder; del (file: r0/paper-writer/SKILL.md)
- patent-application: 申请文件：把已有交底写成权利要求书、说明书、摘要与说明书附图。须指定交底目录；仅缺材料才终止。内容争议写入问题清单，不阻塞主文件。交付后请确认须摘要清单。已有产出上改稿则另存新时间戳目录。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-application/SKILL.md)
- patent-disclosure: 中国专利交底书：发明/实用新型/外观设计的专利点挖掘、轻量查新与成文、保护型1+N专利布局。 (file: r0/patent-disclosure-skill/skills/patent-disclosure/SKILL.md)
- patent-disclosure-skill: 中国专利技能：挖掘专利点与编写交底书（发明/实用/外观），把已有交底改写成申请文件四件套，也可按材料交底申请一起做，按著录字段检索公布公告，通俗解读专利，基于已读库打开专利地图，对照审查口径出政策简报，辅助审查答复。| China patents skill: mine patent points and draft disclosures, rewrite an existing disclosure into application documents, or chain disclosure-then-application from inventor mater (file: r0/patent-disclosure-skill/SKILL.md)
- patent-docket: 按发明人/工程师给的材料一趟写出交底书和申请文件；申请问题清单上的缺口最多改三轮。缺技术事实就问人，不编。触发：交底申请一起做、从零出交底和申请、一条龙、帮写交底再出申请、按清单改、会稿、案卷、/patent-docket。 (file: r0/patent-disclosure-skill/skills/patent-docket/SKILL.md)
- patent-exam-policy: 给交底用的政策简报：对照国知局近期口径，说明对交底写法/本稿的影响，并提示申请书式。技能进化仅为旁路，默认只改交底包，须另点名才改文件。 (file: r0/patent-disclosure-skill/skills/patent-exam-policy/SKILL.md)
- patent-map: 专利地图：基于通俗解读已入库的 Obsidian 案例，点名后打开五种图。地形按 bge-small-zh 向量摊开。 (file: r0/patent-disclosure-skill/skills/patent-map/SKILL.md)
- patent-oa: 审查答复辅助：审查意见问答与草稿；库薄时引导案例入库与实务书蒸馏。须显式触发。 (file: r0/patent-disclosure-skill/skills/patent-oa/SKILL.md)
- patent-reader: 中国专利通俗解读：公开号/PDF 成通俗笔记、图谱与 Obsidian 入库。 (file: r0/patent-disclosure-skill/skills/patent-reader/SKILL.md)
- patent-search: 中国专利公布公告著录检索：发明人、申请人、分类号、名称、摘要；也可从单图或权利要求生成名称/摘要关键字后查询。 (file: r0/patent-disclosure-skill/skills/patent-search/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visual layout matters, including fillable AcroForms. Use Poppler rendering plus Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction. (file: r10/pdf/26.1015.12040/skills/pdf/SKILL.md)
- plugin-management:plugin-management: Discover and suggest relevant plugins, inspect app permissions and dependencies, and manage plugin connections or removal. Use when the user asks about plugins or when a task would materially benefit from an external app, account, service, or data source that available tools cannot acce (file: r5/plugin-management/0.1.0/skills/plugin-management/SKILL.md)
- ponytail:ponytail: Lazy senior dev mode: the smallest change that fully solves the task, and a reply a busy human understands in one read. Use on any coding task (writing, fixing, refactoring, reviewing, choosing dependencies) and when the user says "ponytail", "be lazy", "simplest solution", "yagni", or c (file: r12/ponytail/SKILL.md)
- ponytail:ponytail-audit: Quality audit of a whole repo: bugs, security holes, what breaks under real load, risky code without tests, slow paths, and what to delete, merge or split. Ranked, each finding explained in plain English. One-shot report, changes nothing. Use for "audit this codebase", "review the whole  (file: r12/ponytail-audit/SKILL.md)
- ponytail:ponytail-debt: List every `shortcut:` comment (and older `ponytail:` ones) as a debt ledger. One-shot report, changes nothing. Use for "ponytail debt", "what did ponytail defer", "list the shortcuts", /ponytail-debt. (file: r12/ponytail-debt/SKILL.md)
- ponytail:ponytail-gain: Show ponytail's measured savings (code, cost, speed) from the benchmark. One-shot display. Use for /ponytail-gain, "what does ponytail save", "ponytail impact". (file: r12/ponytail-gain/SKILL.md)
- ponytail:ponytail-help: Quick reference for ponytail levels, skills and commands. One-shot display. Use for /ponytail-help, "ponytail help", "how do I use ponytail". (file: r12/ponytail-help/SKILL.md)
- ponytail:ponytail-review: Quality review of a change: is the logic right, is it safe, does it hold under real load, is risky code tested, is it fast enough, and is every line needed. Reads the connected code, not only the diff. Each finding is explained in plain English. Use for "review this", "code review", "r (file: r12/ponytail-review/SKILL.md)
- pre-submission-reviewer: Runs a pre-submission review of a technical paper across five dimensions: macro logic, writing details, English grammar, LaTeX formatting, and figure quality. Uses a reviewer-style severity taxonomy (CRITICAL / MAJOR / MINOR) and flags banned AI-tone vocabulary and em-dash misuse. Use wh (file: r0/pre-submission-reviewer/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use for presentation, slide deck, PowerPoint, PPT, PPTX, or Google Slides requests. (file: r10/presentations/26.1015.12040/skills/presentations/SKILL.md)
- project-guide: 中文项目导学、源码课程与项目面经技能：基于本地项目仓库、项目描述或技术材料，按需生成源码课程与理解题，或生成 导学-{简称}.md、面经-{简称}.md 及交接摘要；当用户输入“/project-guide”、要求项目导学、源码课程、按调用链展开课程、课程练习、项目复盘、项目面经或 STAR 题库时使用。 (file: r0/project-guide/SKILL.md)
- rebuttal-guidance: Provides actionable peer-review rebuttal guidance (not full rebuttal prose) using conditional persuasion P(Z|X,Y): match reviewer mindset X, recommend strategy Y, optionally ground in manuscript evidence and similar successful historical (review, rebuttal) pairs. Use when the user pastes (file: r0/rebuttal-guidance/SKILL.md)
- redesign-existing-projects: Upgrades existing websites and apps to premium quality. Audits current design, identifies generic AI patterns, and applies high-end design standards without breaking functionality. Works with any CSS framework or vanilla CSS. (file: r0/redesign-skill/SKILL.md)
- reverse-engineer-anything: Reverse engineer native, managed, Electron/JavaScript, packaged, firmware, and browser targets with REA. Use shipped-artifact or requested runtime evidence to explain features, compare versions, decompile code, or guide a reconstruction. Skip REA for ordinary source-repository architectu (file: r1/reverse-engineer-anything/SKILL.md)
- reverse-skill:reverse-skill-router: Use the reverse-skill repository from Codex for authorized reverse engineering, security analysis, CTF, and defensive testing tasks. Requires the reverse-skill repository to be available as the current workspace or an explicitly supplied local path. (file: r13/reverse-skill/1.0.1/skills/reverse-skill-router/SKILL.md)
- sepia:sepia: Make AI-generated writing read as human-written, in fiction and in professional prose. Repairs the narrative architecture of fiction and stories (based on StoryScope, arXiv:2604.03136); routes professional text through domain rules for release notes, announcements, PR and issue replies, c (file: r14/sepia/SKILL.md)
- sepia:sepia-hemingway: Use when a user asks to write or revise fiction in the Hemingway manner, or asks for strong de-AI on a story; applies Sepia's built-in Hemingway voice profile. (file: r14/sepia-hemingway/SKILL.md)
- sepia:sepia-recreate: Use when a user explicitly requests Sepia recreate for a full rewrite. (file: r14/sepia-recreate/SKILL.md)
- sepia:sepia-refactor: Use when a user explicitly requests Sepia refactor for minimal in-place prose revision. (file: r14/sepia-refactor/SKILL.md)
- sepia:sepia-review: Use when a user explicitly requests Sepia review to diagnose prose without editing. (file: r14/sepia-review/SKILL.md)
- sepia:sepia-write: Use when a user explicitly requests Sepia write to create new prose. (file: r14/sepia-write/SKILL.md)
- sites:sites: Use Sites when the user wants a website built for them (including a landing page, portfolio, dashboard, portal, tracker, hub, game, event registration, or tool), wants to edit or remix a specific Site built with the Sites plugin, wants to publish a website with Sites, or wants to manage S (file: r5/sites/1.0.2-remix-a.1/skills/sites/SKILL.md)
- spreadsheets:Spreadsheets: Use skill when user requests to create, modify, analyze, visualize, or work with spreadsheet files (`.xlsx`, `.xls`, `.csv`, `.tsv`) or Google Sheets with formulas, formatting, charts, tables, and recalculation. Do not use for live controlling Microsoft Excel app or a live Excel session. (file: r11/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the ChatGPT add-in or connected session. Use when the user tags the Microsoft Excel app in Codex or follows up on an established live Excel task. Do not use for standalone spreadsheet files or Google Sheets. (file: r11/excel-live-control/SKILL.md)
- stitch-design-taste: Semantic Design System Skill for Google Stitch. Generates agent-friendly DESIGN.md files that enforce premium, anti-generic UI standards — strict typography, calibrated color, asymmetric layouts, perpetual micro-motion, and hardware-accelerated performance. (file: r0/stitch-skill/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design before implementation. (file: r8/brainstorming/SKILL.md)
- superpowers:brainstorming: You MUST use this before any creative work - creating features, building components, adding functionality, modifying behavior, or planning anything new, in software or out of it (a talk, a business, a renovation). (file: r15/brainstorming/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner wants to know why — repeated work, ignored plans, stumbles, poor results, a skill that didn't fire, "it took too long", "why is it so expensive", "what is it doing" — or wants to build a bug report for the superpowers mai (file: r8/diagnosing-superpowers/SKILL.md)
- superpowers:diagnosing-superpowers: Use when a superpowers session went wrong and your human partner wants to know why — repeated work, ignored plans, stumbles, poor results, a skill that didn't fire, "it took too long", "why is it so expensive", "what is it doing" — or wants to build a bug report for the superpowers mainta (file: r15/diagnosing-superpowers/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies (file: r8/dispatching-parallel-agents/SKILL.md)
- superpowers:dispatching-parallel-agents: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies (file: r15/dispatching-parallel-agents/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as the implementer yourself — your human partner chose inline execution, or no subagent tool is available (file: r8/executing-plans/SKILL.md)
- superpowers:executing-plans: Use when executing an implementation plan in the current session as the implementer yourself — your human partner chose inline execution, or no subagent tool is available (file: r15/executing-plans/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work (file: r8/finishing-a-development-branch/SKILL.md)
- superpowers:finishing-a-development-branch: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work (file: r15/finishing-a-development-branch/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable - requires technical rigor and verification, not performative agreement or blind implementation (file: r8/receiving-code-review/SKILL.md)
- superpowers:receiving-code-review: Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable - requires technical rigor and verification, not performative agreement or blind implementation (file: r15/receiving-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before merging to verify work meets requirements (file: r8/requesting-code-review/SKILL.md)
- superpowers:requesting-code-review: Use when completing tasks, implementing major features, or before merging to verify work meets requirements (file: r15/requesting-code-review/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in the current session (file: r8/subagent-driven-development/SKILL.md)
- superpowers:subagent-driven-development: Use when executing implementation plans with independent tasks in the current session (file: r15/subagent-driven-development/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes (file: r8/systematic-debugging/SKILL.md)
- superpowers:systematic-debugging: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes (file: r15/systematic-debugging/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing implementation code (file: r8/test-driven-development/SKILL.md)
- superpowers:test-driven-development: Use when implementing any feature or bugfix, before writing implementation code (file: r15/test-driven-development/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current workspace or before executing implementation plans - ensures an isolated workspace exists via native tools or git worktree fallback (file: r8/using-git-worktrees/SKILL.md)
- superpowers:using-git-worktrees: Use when starting feature work that needs isolation from current workspace or before executing implementation plans - ensures an isolated workspace exists via native tools or git worktree fallback (file: r15/using-git-worktrees/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions (file: r8/using-superpowers/SKILL.md)
- superpowers:using-superpowers: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions (file: r15/using-superpowers/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always (file: r8/verification-before-completion/SKILL.md)
- superpowers:verification-before-completion: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always (file: r15/verification-before-completion/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, before touching code (file: r8/writing-plans/SKILL.md)
- superpowers:writing-plans: Use when you have a spec or requirements for a multi-step task, before touching code (file: r15/writing-plans/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifying skills work before deployment (file: r8/writing-skills/SKILL.md)
- superpowers:writing-skills: Use when creating new skills, editing existing skills, or verifying skills work before deployment (file: r15/writing-skills/SKILL.md)
- teach: Socratic teaching loop for any Claude Code session — quiz yourself on what actually happened, confirm mastery item by item, and don't finish until everything's locked in (file: r0/teach/SKILL.md)
- tech-paper-template: Structures a technical paper's full logical skeleton using a thinking-template table (research background, limitations, key idea or goal, challenges, methodology modules, contributions), positions the paper as Technique or New Problem/Setting, and runs a four-point self-consistency check (file: r0/tech-paper-template/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template skill. Use when the user invokes $template-creator or asks in natural language to create a reusable template from a reference document, presentation, spreadsheet, Google Docs, Slides, or Sheets link, ImageGen or Product Desig (file: r10/template-creator/26.1015.12040/skills/template-creator/SKILL.md)
- vibe-research-workflow: Guides AI-assisted research across three sub-flows, Vibe Coding, Vibe Figure, and Vibe Writing, with behavioural rules that keep the user in charge of academic judgment while delegating mechanical work to AI. Recommends the right tool (Cursor, Claude Code, Codex, Figma, Gemini) for the (file: r0/vibe-research-workflow/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conversation. Proactively use to show how something works; explore 'what happens when', 'what changes', or 'help me understand'; compare or inspect; create simulations, maps, charts, graphs, and mockups. Use standard tools for sta (file: r4/visualize/1.0.50/skills/visualize/SKILL.md)
- work-pets:create-pet: Create, repair, validate, preview, upload, or activate an animated v2 pet in ChatGPT Work mode from a character idea, brand cue, or reference image. Use for new ChatGPT Pets, custom mascots, non-pixel styles, and unattached sprite sheets requiring nine animation states plus sixteen look  (file: r9/create-pet/SKILL.md)
- work-pets:pets: List, inspect, select, download, or delete animated pets in ChatGPT Work mode. Use for an explicit pet in ChatGPT or established ChatGPT Pets context. Exclude real-world and other-app pets; clarify before invoking. (file: r9/pets/SKILL.md)
- work-pets:update-pet: Inspect, validate, preview, repair, or update a custom pet in ChatGPT Work mode, including its name, description, or sprite sheet. Use for a pet in ChatGPT or established ChatGPT Pets context. Exclude real-world and other-app pets; clarify before invoking. (file: r9/update-pet/SKILL.md)
</skills_instructions>
<permissions instructions>
Filesystem sandboxing defines which files can be read or written. `sandbox_mode` is `workspace-write`: The sandbox permits reading files, and editing files in `cwd` and `writable_roots`. Editing files in other directories requires approval. Network access is enabled.

`approvals_reviewer` is `auto_review`: Sandbox escalations with require_escalated will be reviewed for compliance with the policy.
If a rejection happens, you can continue with a safer alternative, or carry out checks to prove that the action is authorized or low risk before trying again. Complete unaffected work without asking for confirmation. Report anything that remains blocked, clarify why it was blocked by auto-review, inform the user of the risk and ask for approval.
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb`, `/Users/oyamahappa/Documents/Agent/Codex`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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
- mcp__code_review
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
- mcp__codex_apps__sites: Use Sites to build or modify websites, including landing pages, portfolios, dashboards, portals, trackers, hubs, and internal tools. Use Sites skills for local implementation, source preparation, and artifact packaging. Use this connector for site...
- mcp__codex_apps__wolfram: Add computation & knowledge
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

## developer · 2026-10-19T15:12:36Z

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

## developer · 2026-10-19T15:12:36Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-10-19T15:12:36Z

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

- 完成一个独立的逻辑单元，且适用的测试、类型检查等验证通过后，主动创建原子化提交。
- 提交说明严格遵循 Conventional Commits，例如 `feat:`、`fix:`、`refactor:`、`test:`、`docs:`。
- 只暂存本次改动涉及的文件，禁止执行 `git add .`。文件包含用户已有修改时，检查并仅暂存本次修改对应的部分。
- 提交前检查内容，不提交 `.env`、API Keys、密钥、临时调试文件或 `.log` 文件。
- 用户已授权每次自动推送：提交完成后，向当前分支已经配置的远端执行普通 `git push`，无需再次征求用户同意。不强制推送，不擅自更换远端或目标分支。
- 当前目录没有 Git 仓库、没有明确的推送目标，或缺少必要权限时，如实说明阻碍；不擅自初始化仓库、创建远端或宣称推送成功。
- Git 操作仍然遵守文件修改与恢复限制。

## 12. 开发记录

每次完成用户交付的任务时，在 `docs/CHANGELOG.md` 追加开发记录；文件不存在则创建，并与对应代码或文档修改一起提交。
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
  <current_date>2026-10-19</current_date>
  <timezone>Asia/Shanghai</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/Agent/Codex</root><root>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/Agent/Codex</path></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-10-19T15:12:37Z

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


## tool · 2026-10-19T15:12:40Z


Script completed
Wall time 0.1 seconds
Output:

/Users/oyamahappa/Documents/Agent/Codex
rg: output/宋浩下册工科数学分析改编: No such file or directory (os error 2)
.agent/hdu-ocr/local/2026年杭州电子科技大学数学分析+高等代数真题(双科合卷)/003.md
.agent/hdu-ocr/local/2026年杭州电子科技大学数学分析+高等代数真题(双科合卷)/004.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/073.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/123.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/090.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/117.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/006.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/077.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/113.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/127.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/027.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/003.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/052.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/023.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/007.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/129.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/008.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/048.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/009.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/068.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/098.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/125.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/020.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/004.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/093.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/060.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/120.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/005.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/110.md
.agent/hdu-ocr/local/2025年杭州电子科技大学601数学分析考研真题/002.md


## tool · 2026-10-19T15:12:43Z


Script completed
Wall time 0.1 seconds
Output:

---
name: using-superpowers
description: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions
---

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, ignore this skill.
</SUBAGENT-STOP>

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. You cannot rationalize your way out of this.
</EXTREMELY-IMPORTANT>

## The Rule

**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.

**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.

Then announce "Using [skill] to [purpose]" and follow the skill exactly. If it has a checklist, create a todo per item.

## Skill Priority

When multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.

- "Let's build X" → superpowers:brainstorming first, then implementation skills.
- "Fix this bug" → superpowers:systematic-debugging first, then domain skills.

## Red Flags

These thoughts mean STOP—you're rationalizing:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "I can check git/files quickly" | Files lack conversation context. Check for skills. |
| "Let me gather information first" | Skills tell you HOW to gather information. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |
| "This doesn't count as a task" | Action = task. Check for skills. |
| "The skill is overkill" | Simple things become complex. Use it. |
| "I'll just do this one thing first" | Check BEFORE doing anything. |
| "This feels productive" | Undisciplined action wastes time. Skills prevent this. |
| "I know what that means" | Knowing the concept ≠ using the skill. Invoke it. |

## Platform Adaptation

If your harness appears here, read its reference file for special instructions:

- Claude Code: `references/claude-code-tools.md`
- Codex: `references/codex-tools.md`
- Pi: `references/pi-tools.md`
- Antigravity: `references/antigravity-tools.md`
- Hermes Agent: `references/hermes-tools.md`
- Muse: `references/muse-tools.md`

## User Instructions

User instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.
---
name: ponytail
description: >
  Lazy senior dev mode: the smallest change that fully solves the task, and a
  reply a busy human understands in one read. Use on any coding task (writing,
  fixing, refactoring, reviewing, choosing dependencies) and when the user says
  "ponytail", "be lazy", "simplest solution", "yagni", or complains about
  over-engineering or bloat. Levels: lite, full (default), ultra.
argument-hint: "[lite|full|ultra|off]"
license: MIT
---

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
| **lite** | Build what was asked. Name the smaller option in one line and let the user pick. |
| **full** | The rules above. Default. |
| **ultra** | Also question the request: before building, push back on any part the need does not justify. |


## tool · 2026-10-19T15:12:47Z


Script completed
Wall time 0.1 seconds
Output:

第10章
重积分

第一节 二重积分的概念和性质

一、二重积分的概念

定义：$\iint_D f(x,y) \mathrm{d}\sigma = \lim_{\lambda \to 0} \sum_{i=1}^{n} f(\xi_i,\eta_i) \Delta \sigma_i$，其中 $\Delta \sigma_i$ 是分割区域 $D$ 为 $n$ 个子区域时子区域 $\sigma_i$ 的面积，$(\xi_i,\eta_i) \in \sigma_i$，$\lambda$ 为 $n$ 个子区域的直径的最大值.

在平面直角坐标系下，$\iint_D f(x,y) \mathrm{d}\sigma = \iint_D f(x,y) \mathrm{d}x \mathrm{d}y$.

几何意义：若 $f(x,y)$ 在有界闭区域 $D$ 上连续，且 $f(x,y) \geq 0$，则二重积分 $\iint_D f(x,y) \mathrm{d}\sigma$ 表示曲顶柱体的体积，该柱体以曲面 $z=f(x,y)$ 为顶，以 $xOy$ 平面上有界闭区域 $D$ 为底面，以通过 $D$ 的边界且平行于 $z$ 轴的直线为母线.

256 基础题 设 $f(x,y)$ 连续，且 $f(x,y)=xy+\iint_D f(u,v) \mathrm{d}u \mathrm{d}v$，其中 $D$ 是由 $y=0$，$y=x,x=1$ 围成的区域，求 $f(x,y)$.

257 提高题 极限 $\lim_{n \to \infty} \sum_{i=1}^{n} \sum_{j=1}^{n} \frac{n}{(n+i)(n^2+j^2)} =$ (    ).

(A) $\int_0^1 \mathrm{d}x \int_0^x \frac{1}{(1+x)(1+y^2)} \mathrm{d}y$

(B) $\int_0^1 \mathrm{d}x \int_0^x \frac{1}{(1+x)(1+y)} \mathrm{d}y$

(C) $\int_0^1 \mathrm{d}x \int_0^1 \frac{1}{(1+x)(1+y^2)} \mathrm{d}y$

(D) $\int_0^1 \mathrm{d}x \int_0^1 \frac{1}{(1+x)(1+y)} \mathrm{d}y$

258 提高题 求极限 $\lim_{n \to \infty} \frac{\pi}{2n^4} \sum_{i=1}^{n} \sum_{j=1}^{n} i^2 \sin \frac{j\pi}{2n}$.

二、二重积分的性质

性质1（线性性质）：设 $k,l$ 为常数，则
$$\iint_D [k f(x,y)+l g(x,y)] \mathrm{d}\sigma = k \iint_D f(x,y) \mathrm{d}\sigma + l \iint_D g(x,y) \mathrm{d}\sigma.$$270 中等题 计算二重积分 $\iint_D (x^2 + 2y) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D = \{(x, y) | x^2 + y^2 \leqslant 1\}$.

## 第二节 二重积分的计算方法

### 一、交换积分次序

这种类型的题目可以按照如下步骤求解.

第1步：根据已知的积分写出积分区域 $D$ 的坐标描述.

第2步：画出区域 $D$ 的图像.

第3步：根据图像，写出 $D$ 的另一种坐标描述. 若已知将 $D$ 视为 $X$ 型区域，则将其视为 $Y$ 型区域，反之亦然.

第4步：根据坐标描述写出新的积分次序.

271 基础题 已知 $I = \int_0^4 \mathrm{d}x \int_x^{2\sqrt{x}} f(x, y) \mathrm{d}y$，交换其积分次序.

272 基础题 已知 $I = \int_0^1 \mathrm{d}y \int_{-\sqrt{1-y^2}}^{\sqrt{1-y^2}} f(x, y) \mathrm{d}x$，交换其积分次序.

273 基础题 已知 $I = \int_0^1 \mathrm{d}x \int_{-\sqrt{x}}^{\sqrt{x}} f(x, y) \mathrm{d}y + \int_1^4 \mathrm{d}x \int_{x-2}^{\sqrt{x}} f(x, y) \mathrm{d}y$，交换其积分次序.

274 基础题 已知 $I = \int_0^1 \mathrm{d}y \int_0^{2y} f(x, y) \mathrm{d}x + \int_1^3 \mathrm{d}y \int_0^{3-y} f(x, y) \mathrm{d}x$，交换其积分次序.

275 基础题 已知 $I = \int_0^\pi \mathrm{d}x \int_{-\sin \frac{x}{2}}^{\sin x} f(x, y) \mathrm{d}y$，交换其积分次序.

276 基础题 已知 $I = \int_1^2 \mathrm{d}y \int_y^{y^2} f(x, y) \mathrm{d}x + \int_2^8 \mathrm{d}x \int_x^8 f(x, y) \mathrm{d}y$，交换其积分次序.

277 中等题 设 $f(x)$ 为连续函数，$F(t) = \int_1^t \mathrm{d}y \int_y^t f(x) \mathrm{d}x$，求 $F'(3)$.证明 $\iint_D \frac{1}{(1+x^2+y^2)^2} \mathrm{d}x \mathrm{d}y = \frac{\pi}{4}$, 其中 $D = \{(x,y) | 0 \leqslant x,y < +\infty\}$.

### 第三节 三重积分

计算三重积分 $\iiint_\Omega f(x,y,z) \mathrm{d}V$ 的基本方法是将其化为 3 次定积分进行计算.

一、利用空间直角坐标计算三重积分

**坐标面投影法（“先一后二”法）**

若 $\Omega$ 是 $XY$ 型区域，即

$$\Omega = \{(x,y,z) | z_1(x,y) \leqslant z \leqslant z_2(x,y), (x,y) \in D\},$$

且 $D = \{(x,y) | a \leqslant x \leqslant b, y_1(x) \leqslant y \leqslant y_2(x)\}$, 则

$$\iiint_\Omega f(x,y,z) \mathrm{d}V = \iiint_D \mathrm{d}x \mathrm{d}y \int_{z_1(x,y)}^{z_2(x,y)} f(x,y,z) \mathrm{d}z = \int_a^b \mathrm{d}x \int_{y_1(x)}^{y_2(x)} \mathrm{d}y \int_{z_1(x,y)}^{z_2(x,y)} f(x,y,z) \mathrm{d}z.$$

**坐标轴投影法（“先二后一”法、截面法）**

该方法适用于旋转体或垂直于某轴的截面的面积已知的情形.

设 $\Omega = \{(x,y,z) | (x,y) \in D_z, c \leqslant z \leqslant d\}$, 其中 $D_z$ 为竖坐标 $z$ 的平面截闭区域 $\Omega$ 所得到的一个平面闭区域（截面），则

$$\iiint_\Omega f(x,y,z) \mathrm{d}V = \int_c^d \mathrm{d}z \iiint_D_z f(x,y) \mathrm{d}y \mathrm{d}z.$$

**331 中等题** 计算三重积分 $\iiint_\Omega xy^2 z^3 \mathrm{d}x \mathrm{d}y \mathrm{d}z$, 其中 $\Omega$ 是由曲面 $z = xy$ 及平面 $y=x,$ $x=1$ 和 $z=0$ 围成的闭区域.

**332 中等题** 计算三重积分 $\iiint_\Omega \frac{y \sin x}{x} \mathrm{d}x \mathrm{d}y \mathrm{d}z$, 其中 $\Omega$ 是由 $y=\sqrt{x}, y=0,z=0$ 和 $x+z=\frac{\pi}{2}$ 围成的闭区域.

**333 中等题** 计算三重积分 $\iiint_\Omega z^2 \mathrm{d}V$, 其中 $\Omega$ 由 $x^2+\frac{y^2}{4}+\frac{z^2}{9} \leqslant 1, 0 \leqslant z \leqslant 1$ 确定.

二、利用柱面坐标计算三重积分

设 $M(x,y,z)$ 为空间内一点，点 $M$ 在 $xOy$ 平面上的投影点 $P$ 的极坐标为第11章
曲线积分

第一节 对弧长的曲线积分

一、对弧长的曲线积分的定义

定义1：设 $L$ 为 $xOy$ 平面内的分段光滑曲线弧，函数 $f(x,y)$ 在 $L$ 上有界，则 $f(x,y)$ 在 $L$ 上对弧长的曲线积分的定义为

$$\int_L f(x,y) \mathrm{d}s \triangleq \lim_{\lambda \to 0} \sum_{i=1}^n f(\xi_i,\eta_i)\Delta s_i$$

其中 $\Delta s_i$ 表示第 $i$ 小段的弧长，$(\xi_i,\eta_i)$ 为第 $i$ 小段上任取的一点，$\lambda = \max_{1 \leq i \leq n} \Delta s_i$.

定义2：设 $L$ 为空间内的分段光滑曲线弧，函数 $f(x,y,z)$ 在 $L$ 上有界，则 $f(x,y,z)$ 在 $L$ 上对弧长的曲线积分的定义为

$$\int_L f(x,y,z) \mathrm{d}s \triangleq \lim_{\lambda \to 0} \sum_{i=1}^n f(\xi_i,\eta_i,\zeta_i)\Delta s_i$$

其中 $\Delta s_i$ 表示第 $i$ 小段的弧长，$(\xi_i,\eta_i,\zeta_i)$ 为第 $i$ 小段上任取的一点，$\lambda = \max_{1 \leq i \leq n} \Delta s_i$.

评注

(1) 对弧长的曲线积分又称为第一类曲线积分.

(2) 当 $L$ 为封闭曲线时，对弧长的曲线积分常记为 $\oint_L f(x,y) \mathrm{d}s, \oint_L f(x,y,z) \mathrm{d}s$.

(3) 若函数 $f(x,y)$ 在曲线弧 $L$ 上连续，则 $\int_L f(x,y) \mathrm{d}s$ 存在.

356 基础题 设 $L$ 为光滑曲线弧，其弧长为 $a$，$k$ 为常数，则 $\int_L k \mathrm{d}s =$ ____.

357 基础题 若 $\int_L f(x,y) \mathrm{d}s$ 存在，且在 $L$ 上 $f(x,y) \geq 0$，证明 $\int_L f(x,y) \mathrm{d}s \geq 0$.

358 基础题 若 $\int_L f(x,y) \mathrm{d}s$ 和 $\int_L g(x,y) \mathrm{d}s$ 都存在，且在 $L$ 上 $f(x,y) \geq g(x,y)$，则（ ）

(A) $\int_L f(x,y) \mathrm{d}s \leq \int_L g(x,y) \mathrm{d}s$

(B) $\int_L f(x,y) \mathrm{d}s \geq \int_L g(x,y) \mathrm{d}s$

(C) $\int_L f(x,y) \mathrm{d}s = \int_L g(x,y) \mathrm{d}s$

(D) $\int_L f(x,y) \mathrm{d}s, \int_L g(x,y) \mathrm{d}s$ 的大小不定381 中等题 计算 $\oint_{L} \frac{x}{1+y} \mathrm{d}s$，其中 $L$ 是以 $O(0,0), A(1,0), B(0,1)$ 为顶点的三角形.

第二节 对坐标的曲线积分

一、对坐标的曲线积分的定义

定义：设 $L$ 为 $xOy$ 平面内的一条光滑有向曲线弧，函数 $P(x,y), Q(x,y)$ 在 $L$ 上有界，则 $P(x,y), Q(x,y)$ 在 $L$ 上对坐标的曲线积分的定义为

$$\int_{L} P(x,y) \mathrm{d}x \triangleq \lim_{\lambda \to 0} \sum_{i=1}^{n} P(\xi_i, \eta_i) \Delta x_i,$$

$$\int_{L} Q(x,y) \mathrm{d}y \triangleq \lim_{\lambda \to 0} \sum_{i=1}^{n} Q(\xi_i, \eta_i) \Delta y_i,$$

其中 $\Delta x_i, \Delta y_i$ 分别为将 $L$ 分割的有向小弧段 $\Delta s_i$ 在 $x$ 轴及 $y$ 轴上的投影，$(\xi_i, \eta_i)$ 为 $\Delta s_i$ 上任取的一点，$\lambda = \max_{1 \leq i \leq n} \Delta s_i$.

类似地，函数 $P(x,y,z), Q(x,y,z), R(x,y,z)$ 在空间有向曲线弧 $L$ 上对坐标的曲线积分的定义为

$$\int_{L} P(x,y,z) \mathrm{d}x \triangleq \lim_{\lambda \to 0} \sum_{i=1}^{n} P(\xi_i, \eta_i, \zeta_i) \Delta x_i,$$

$$\int_{L} Q(x,y,z) \mathrm{d}y \triangleq \lim_{\lambda \to 0} \sum_{i=1}^{n} Q(\xi_i, \eta_i, \zeta_i) \Delta y_i,$$

$$\int_{L} R(x,y,z) \mathrm{d}z \triangleq \lim_{\lambda \to 0} \sum_{i=1}^{n} R(\xi_i, \eta_i, \zeta_i) \Delta z_i.$$

评注

(1) 对坐标的曲线积分又称为第二类曲线积分.

(2) $\int_{L} P(x,y) \mathrm{d}x + Q(x,y) \mathrm{d}y = \int_{L} P(x,y) \mathrm{d}x + \int_{L} Q(x,y) \mathrm{d}y.$

(3) 若 $L$ 为封闭曲线，则对坐标的曲线积分记为 $\oint_{L} P \mathrm{d}x + Q \mathrm{d}y, \oint_{L} P \mathrm{d}x + Q \mathrm{d}y + R \mathrm{d}z.$

(4) 若 $P(x,y), Q(x,y)$ 在有向曲线弧 $L$ 上连续，则 $\int_{L} P(x,y) \mathrm{d}x + Q(x,y) \mathrm{d}y$ 存在.

382 基础题 设 $L$ 为 $xOy$ 平面内垂直于 $x$ 轴的有向线段，且 $\int_{L} P(x,y) \mathrm{d}x$ 存在，则 $\int_{L} P(x,y) \mathrm{d}x = \_\_\_\_\_.$

383 基础题 设 $L$ 为从点 $A(x_1,y_1)$ 到点 $B(x_2,y_2)$ 的一条光滑有向曲线弧，$k$ 为常数，则 $\int_{L} k \mathrm{d}x = \_\_\_\_\_，\int_{L} k \mathrm{d}y = \_\_\_\_\_.$403 中等题 设 $L$ 是圆锥面 $z = \sqrt{x^2 + y^2}$ 与平面 $y = x$ 的交线上从点 $A(1, 1, \sqrt{2})$ 到点 $B(-1, -1, \sqrt{2})$ 的一段，计算曲线积分 $I = \int_L yz\mathrm{d}x + zx\mathrm{d}y + xy\mathrm{d}z$ .

四、两类曲线积分之间的联系

平面曲线弧上的两类曲线积分的联系
$$\int_L P(x, y)\mathrm{d}x + Q(x, y)\mathrm{d}y = \int_L [P(x, y)\cos \alpha + Q(x, y)\cos \beta]\mathrm{d}s$$
其中 $\cos \alpha, \cos \beta$ 为平面有向曲线弧 $L$ 上任意点 $(x, y)$ 处与 $L$ 同向的切向量的方向余弦.

空间曲线弧上的两类曲线积分的联系
$$\int_L P(x, y, z)\mathrm{d}x + Q(x, y, z)\mathrm{d}y + R(x, y, z)\mathrm{d}z$$
$$= \int_L [P(x, y, z)\cos \alpha + Q(x, y, z)\cos \beta + R(x, y, z)\cos \gamma]\mathrm{d}s$$
其中 $\cos \alpha, \cos \beta, \cos \gamma$ 为空间有向曲线弧 $L$ 上任意点 $(x, y, z)$ 处与 $L$ 同向的切向量的方向余弦.

404 基础题 设 $L$ 是沿圆周 $x^2 + y^2 = 2y$ 从原点到点 $(0, 2)$ 的右半圆弧，则曲线积分
$$\int_L P(x, y)\mathrm{d}x + Q(x, y)\mathrm{d}y = (\quad).$$
(A) $\int_L [(1 - y)P(x, y) + xQ(x, y)]\mathrm{d}s$ (B) $\int_L [(1 - y)P(x, y) - xQ(x, y)]\mathrm{d}s$
(C) $\int_L [xP(x, y) + (1 - y)Q(x, y)]\mathrm{d}s$ (D) $\int_L [xP(x, y) - (1 - y)Q(x, y)]\mathrm{d}s$

405 基础题 设 $L$ 为曲线 $x = t, y = t^2, z = t^3$ 上 $t$ 从 1 变到 0 的曲线弧，若 $L$ 的弧长为 $a$，则 $\int_L \frac{\mathrm{d}x + 2x\mathrm{d}y + 3y\mathrm{d}z}{\sqrt{1 + 4x^2 + 9y^2}} =$ ____ .

406 中等题 设 $f(x, y)$ 连续，$L$ 为曲线 $y = x^2$ 上从点 $(1, 1)$ 到点 $(0, 0)$ 的曲线弧.
(1) 把对坐标的曲线积分 $I = \int_L f(x, y)\mathrm{d}x + 2xf(x, y)\mathrm{d}y$ 转化为对弧长的曲线积分；
(2) 若 $f(x, y) = \frac{1}{x^2 + 3y + 1}$，计算 $I$ 的值.

第三节 格林公式及其应用

一、格林公式

定理（格林公式）：若 $P(x, y), Q(x, y)$ 在闭区域 $D$ 上具有一阶连续偏导数，则

## tool · 2026-10-19T15:12:51Z




## tool · 2026-10-19T15:12:55Z


Script completed
Wall time 0.1 seconds
Output:

.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/003.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/004.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/005.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/006.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/007.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/008.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/009.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/010.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/020.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/023.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/027.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/048.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/052.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/060.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/068.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/073.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/077.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/090.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/093.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/098.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/110.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/113.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/117.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/120.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/123.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/125.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/127.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/129.md
output/HDU/md/数学分析/2016/2016年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2016/2016年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2011/2011年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2011/2011年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2026/2026年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2026/2026年数学分析补充解析.md
output/HDU/md/数学分析/2017/2017年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2017/2017年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2012/2012年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2012/2012年杭州电子科技大学601数学分析考研真题.md
output/HDU/md/数学分析/2015/2015年杭州电子科技大学601数学分析考研真题参考答案.md
output/HDU/md/数学分析/2015/2015年杭州电子科技大学601数学分析考研真题.md


## tool · 2026-10-19T15:12:58Z


Script completed
Wall time 0.1 seconds
Output:

# 2021年杭州电子科技大学601数学分析考研真题

来源：`HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf`。原 PDF 页序：1, 2。

# 杭州电子科技大学

# 2021年攻读硕士学位研究生招生考试

# 《数学分析》试题

(试题共四大题，共2页，总分150分）

姓名 报考专业 准考证号

【所有答案必须写在答题纸上，做在试卷或草稿纸上无效！】

## 一、填空题（本大题共8小题，每小题5分，共40分)

1. $\lim _ { n  \infty } \frac { n ^ { 2 } } { 2 ^ { n } } = ($ ）.

2.设点(0,1)是曲线 $y = x ^ { 3 } + b x ^ { 2 } + 1$ 的拐点，则b=（ ）.

3.设 $\left\{ \begin{array} { l } { x = a \cos ^ { 3 } t } \\ { y = a \sin ^ { 3 } t , } \end{array} \right.$ 则 $\left. { \frac { d y } { d x } } \right| _ { x = \frac { \pi } { 4 } } = ($ ）.

4.曲线y=x(x-1)(2-x)与x轴所围图形的面积为( ）.

5.曲面 $e ^ { z } - z + x y = 3$ 在点P(2,1,0)处的切平面方程为( ）.

6.设f(x)是周期为2的周期函数，且 $f ( x ) { = } \left\{ \begin{array} { l l } { { 2 } , \ { - } 1 < x \le 0 } \\ { { x } ^ { 3 } , \quad 0 < x \le 1 , } \end{array} \right.$ 则f(x)的傅里叶级数在x=1处收敛于（ ）.

7.设f(u,v)为二元可微函数，若 $z = f ( x ^ { y } , y ^ { x } )$ ，则 $\frac { \partial z } { \partial x } = ($ ）.

8.设 $L : y = x ^ { 2 } ( 0 \leq x \leq { \sqrt { 2 } } )$ ，则 $\int _ { L } x d s = ($ ）.

## 二、计算题（本大题共4小题，共30分）

1．（本小题5分）求极限 $\lim _ { x \to 0 ^ { + } } { \frac { \sqrt { x } } { 1 - e ^ { \sqrt { x } } } }$

2．（本小题5分）计算积分 $\int _ { 0 } ^ { \frac { \pi } { 2 } } { \frac { \cos x } { 1 + \sin ^ { 2 } x } } d x$

3．（本小题10分）求幂级数 $\sum _ { n = 1 } ^ { \infty } n x ^ { n - 1 }$ 的收敛域及和函数.

4．（本小题10分）计算曲线积分 $\int _ { L } ( x ^ { 2 } + 3 y ) d x + ( y ^ { 2 } - x ) d y$ ,其中L为从点 $\pmb { A } ( 4 , 0 )$ 到点0(0,0)的上半圆周 $y = \sqrt { 4 x - x ^ { 2 } }$

## 三、综合题（本大题共3小题，每小题10分，共30分)

1.已知函数 $f ( x , y ) = { \sqrt { | x y | } }$

(1)求f(x,y)在(0,0)处的偏导数 $f _ { x } ( 0 , 0 )$ 和 ${ f _ { y } } ( 0 , 0 )$

(2)讨论f(x,y)在点(0,0)处的可微性.

2.讨论函数项级数 $\sum _ { n = 1 } ^ { \infty } { \frac { x ^ { 2 0 2 1 } } { e ^ { n x } } }$ 在 $[ 0 , + \infty )$ 上的一致收敛性.

3.计算曲面积分 $\int \int _ { \Sigma } { x z ^ { 2 } d y d z } + ( x ^ { 2 } y - z ^ { 2 } ) d z d x + ( 2 x y + y ^ { 2 } z ) d x d y$ ，其中 $\Sigma$ 为上半球面$z = \sqrt { 1 - x ^ { 2 } - y ^ { 2 } }$ 的上侧.

## 四、证明题（本大题共5小题，每小题10分，共50分）

1.设 $a > 0 , a _ { 1 } = \frac { 1 } { 2 } \left( a + \frac { 1 } { a } \right) , a _ { n + 1 } = \frac { 1 } { 2 } \left( a _ { n } + \frac { 1 } { a _ { n } } \right) , n = 1 , 2 , \cdots$ ．证明：数列 $\{ a _ { n } \}$ 收敛,并且 其极限为1.

2.用一致连续的定义证明：函数 $f ( x ) { = } \cos { \sqrt { x } }$ 在 $[ a , + \infty ) \ ( a > 0 )$ 上一致连续.

3.设f(x)在[a,b]上连续，在(a,b)内可微，且

$$
f ( a ) \cdot f ( b ) > 0 , f ( a ) \cdot f \left( \frac { a + b } { 2 } \right) < 0 .
$$

证明：存在一点 $\xi \in ( a , b )$ ，使得 $f ^ { \prime } ( \xi ) = f ( \xi )$

4．证明：含参量反常积分 $\int _ { 0 } ^ { + \infty } x e ^ { - \alpha x }$ dx在 $\left[ \alpha _ { 0 } , + \infty \right) \left( \alpha _ { 0 } > 0 \right)$ 上一致收敛，但在$( 0 , + \infty )$ 上非一致收敛.

5.设f(x)在 $[ a , b ] ( a < b )$ 上连续且单调递增.求证：

$$
\int _ { a } ^ { b } x f ( x ) d x \geq { \frac { a + b } { 2 } } \int _ { a } ^ { b } f ( x ) d x .
$$
# 2025年杭州电子科技大学601数学分析考研真题

来源：`HDU/601数学分析/2025/2025年杭州电子科技大学601数学分析考研真题.pdf`。原 PDF 页序：1, 2。

# 杭州电子科技大学2025年数学分析真题

> 文字整理说明：根据远程OCR与本地逐页OCR整理数学语法，一6的积分式由本地OCR补全。保留原资料的缺失条件和待讨论结论，不将补充解析中的建议条件写入题干。

## 一、填空（每题5分，共40分）

1. $\displaystyle\lim_{n\to+\infty}\frac{11\times12\times\cdots\times(n+10)}{1\times4\times7\times\cdots\times(3n-2)}=$ ____。

2. $\forall x>0$，$f(x)>0$；$\forall x\ge0$，$\displaystyle f(x)=\sqrt{\int_0^xf(t)\,dt}$，则 $f(x)=$ ____。

3. $\displaystyle\int_\alpha^{\alpha+1}(x-1)(1-x)^{10}\,dx=$ ____。

4. 若 $\displaystyle\lim_{x\to0}(1+x)^{c/x}=\int_{-\infty}^cte^t\,dt$，则 $c=$ ____。

5. $\displaystyle\iiint_V(x+y+z)\,dx\,dy\,dz=$ ____。（$V$ 为 $x+y+z=1$ 和三个坐标轴围成。原资料用词如此，几何含义的说明见补充解析。）

6. $\displaystyle\int_Lx\,dy=$ ____。（$L$ 是 $x^2/4+y^2=1$，逆时针。）

7. 隐函数中拐点，求参数。（原资料未给出具体方程和参数条件。）

8. $\displaystyle\iint_S(x^2+y^2)\,dS=$ ____，$S$ 为 $z=\sqrt{x^2+y^2}$ 和 $z=1$ 所围的外表面。

## 二、计算（每题9分，共36分）

1. 计算 $\displaystyle\iint_Sx^2y^2z\,dx\,dy$，$S$ 为 $x^2+y^2+z^2=1$ 的下半球面，取上侧。

2. $\displaystyle I=\int_LP\,dx+Q\,dy$，其中
   \[
   P=\frac{x}{y}r^\alpha,\quad Q=-\frac{x^2}{y^2}r^\alpha,\quad r=\sqrt{x^2+y^2}.
   \]
   若 $I\equiv0$，则 $\alpha$ 为多少？（现有题面未给出 $L$ 的定义。）

3. 求 $\displaystyle\sum_{n=2}^\infty\frac{(-1)^nx^{n+1}}{n(n-1)}$ 的收敛半径和和函数。

4. 若 $\displaystyle\int_0^\infty e^{-x^2}\,dx=\frac{\sqrt\pi}{2}$，求 $\displaystyle\int_0^\infty\cos(\alpha x)e^{-x^2}\,dx$。

## 三、证明题（每题10分，共50分）

1. 用“$\varepsilon$—$\delta$”语言证明：
   \[
   \lim_{x\to1}\frac{x^2-x}{6x^2-4x-2}=\frac18.
   \]

2. $f(x)$ 二阶连续可导，$f(0)=0$，$\displaystyle M=\max_{x\in[0,1]}f''(x)$，证明：
   \[
   \left|\int_{-1}^1f(x)\,dx\right|\le\frac13M.
   \]
   （$M$ 的区间及未加绝对值的写法均按现有题面保留；命题的条件问题见补充解析。）

3. 证明：
   \[
   u(x,t)=\frac12[f(x-at)+f(x+at)]+\frac1{2a}\int_{x-at}^{x+at}F(z)\,dz
   \]
   满足弦振动方程 $\displaystyle\frac{\partial^2u}{\partial t^2}=a^2\frac{\partial^2u}{\partial x^2}$。

4. 证明函数列 $\displaystyle S_n(x)=\sum_{k=1}^n\frac1n\cos\left(x+\frac kn\right)$ 在 $x\in[a,b]\subset\mathbb R$ 上一致收敛。

5. 若 $f_n(x)$ 在区间 $I$ 上一致连续，且 $f_n\rightrightarrows f$，证明 $f$ 在 $I$ 上一致连续。

## 四、讨论题（每题12分，共24分）

1. 若 $\displaystyle\frac{x^2}{\alpha^2}+\frac{y^2}{\beta^2}+\frac{z^2}{\gamma^2}=1$，切平面与坐标轴围成的四面体体积为 $V$，求 $V_{\max}$。（“最大值”按原资料保留，存在性问题见补充解析。）

2. 讨论函数
   \[
   f(x)=\begin{cases}x(1-x),&x\in\mathbb Q,\\x(1+x),&x\notin\mathbb Q\end{cases}
   \]
   的连续性和可微性。


## tool · 2026-10-19T15:14:14Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-10-19T15:14:21Z


Script completed
Wall time 0.1 seconds
Output:

\section{第10章\quad 重积分}
\subsection{二重积分的概念与性质}

\begin{problem}{256}{43}{积分方程与参数讨论}
设 $D=\{(x,y):0\leq y\leq x\leq1\}$，$\lambda\in\mathbb R$。讨论连续函数方程
\[
 f(x,y)=xy+\lambda\iint_D f(u,v)\,\dd u\dd v
\]
的解是否存在、是否唯一；存在时求出 $f(x,y)$，并给出 $\lambda=1$ 时的结果。
\end{problem}

\begin{problem}{257}{43}{二重和的积分极限}
将下列极限分别表示为二重积分并计算，说明两者积分区域的差别：
\[
 \lim_{n\to\infty}\sum_{i=1}^n\sum_{j=1}^n
 \frac{n}{(n+i)(n^2+j^2)},\qquad
 \lim_{n\to\infty}\sum_{i=1}^n\sum_{j=1}^i
 \frac{n}{(n+i)(n^2+j^2)}.
\]
第二个极限只须化为一个定积分，无须求出初等形式。
\end{problem}

\begin{problem}{258}{43}{黎曼和与误差估计}
计算
\[
 L=\lim_{n\to\infty}\frac{\pi}{2n^4}
 \sum_{i=1}^n\sum_{j=1}^n i^2\sin\frac{j\pi}{2n}.
\]
利用 $x^2$ 与 $\sin y$ 在相应区间上的单调性，说明该和式与 $L$ 之差为 $O(1/n)$。
\end{problem}

\begin{problem}{270}{47}{对称性与圆域积分}
设 $D=\{(x,y):x^2+y^2\leq1\}$。不先作二次积分，利用对称性求
\[
 \iint_D(x^2+2y)\,\dd x\dd y,
\]
并求 $\iint_D(ax^2+by^2+cxy+dy)\,\dd x\dd y$，其中 $a,b,c,d$ 为实常数。
\end{problem}

\subsection{二重积分的计算方法}

\begin{problem}{271}{47}{交换积分次序与计算}
设 $f$ 在 $D=\{(x,y):0\leq x\leq4,\ x\leq y\leq2\sqrt{x}\}$ 上连续。
把 $\int_0^4\dd x\int_x^{2\sqrt{x}}f(x,y)\,\dd y$ 改写成先对 $x$ 积分的累次积分，并用所得表达式计算 $f(x,y)=y$ 时的积分。
\end{problem}

\begin{problem}{272}{47}{半圆域与积分次序}
对连续函数 $f$，将
\[
 \int_0^1\dd y\int_{-\sqrt{1-y^2}}^{\sqrt{1-y^2}}f(x,y)\,\dd x
\]
交换积分次序。再取 $f(x,y)=x^2+y^2$，写出极坐标表达式并计算其值。
\end{problem}

\begin{problem}{273}{47}{分块区域的合并}
设 $f$ 在下式涉及的闭区域上连续，将
\[
 \int_0^1\dd x\int_{-\sqrt{x}}^{\sqrt{x}}f(x,y)\,\dd y
 +\int_1^4\dd x\int_{x-2}^{\sqrt{x}}f(x,y)\,\dd y
\]
改写为一个先对 $x$ 积分的累次积分，并由此求该积分区域的面积。
\end{problem}

\begin{problem}{274}{47}{分段边界与换序}
设 $f$ 连续，把
\[
 \int_0^1\dd y\int_0^{2y}f(x,y)\,\dd x
 +\int_1^3\dd y\int_0^{3-y}f(x,y)\,\dd x
\]
交换积分次序；取 $f(x,y)=y$，计算积分并求该区域的形心纵坐标。
\end{problem}

\begin{problem}{275}{47}{三角函数边界的换序}
设 $f$ 在 $D=\{(x,y):0\leq x\leq\pi,-\sin(x/2)\leq y\leq\sin x\}$ 上连续。
将 $\iint_Df\,\dd x\dd y$ 改为先对 $x$ 积分的表达式，写明必须分段的纵坐标，并求 $D$ 的面积。
\end{problem}

\begin{problem}{276}{47}{不同次序积分的区域辨析}
设 $f$ 连续，记
\[
 I=\int_1^2\dd y\int_y^{y^2}f(x,y)\,\dd x
 +\int_2^8\dd x\int_x^8f(x,y)\,\dd y.
\]
分别用不等式描述两项对应的区域，判断其内部是否相交；将 $I$ 全部改为先对 $x$ 积分，并计算 $f\equiv1$ 时的值。
\end{problem}

\begin{problem}{277}{47}{变限二重积分求导}
设 $f$ 在 $[1,+\infty)$ 上连续，$F(t)=\int_1^t\dd y\int_y^t f(x)\,\dd x$，$t\geq1$。
先交换积分次序，再求 $F'(t)$ 与 $F'(3)$；若 $f$ 处处为正，判断 $F$ 在 $(1,+\infty)$ 上的单调性并说明理由。
\end{problem}

\subsection{三重积分}

\begin{problem}{331}{55}{空间区域与幂函数积分}
设 $\Omega=\{(x,y,z):0\leq y\leq x\leq1,\ 0\leq z\leq xy\}$。
写出先对 $z$ 积分与先对 $y$ 积分的两种累次积分，计算
$\iiint_\Omega xy^2z^3\,\dd x\dd y\dd z$，并说明曲面 $z=xy$ 与 $z=0$ 如何确定区域的下边界 $y=0$。
\end{problem}

\begin{problem}{332}{55}{三重积分的次序选择}
设 $\Omega=\{(x,y,z):0\leq x\leq\pi/2,\ 0\leq y\leq\sqrt{x},\ 0\leq z\leq\pi/2-x\}$。
将 $\sin x/x$ 在 $x=0$ 处作连续延拓，计算
\[
 \iiint_\Omega\frac{y\sin x}{x}\,\dd x\dd y\dd z,
\]
并解释先对 $y,z$ 积分为何能消去分母 $x$ 带来的计算困难。
\end{problem}

\begin{problem}{333}{55}{椭球截面与参数积分}
设 $0<h\leq3$，$\Omega_h=\{(x,y,z):x^2+y^2/4+z^2/9\leq1,\ 0\leq z\leq h\}$。
用水平截面法求 $J(h)=\iiint_{\Omega_h}z^2\,\dd V$，求 $J(1)$，并说明 $J'(h)$ 的几何意义。
\end{problem}
\section{第11章\quad 曲线积分}
\subsection{对弧长的曲线积分}

\begin{problem}{356}{63}{弧长积分与取向}
设分段光滑曲线弧 $L$ 的长度为 $a>0$，$k$ 为常数。从弧长积分的定义求 $\int_Lk\,\dd s$，并判断将曲线反向后结果是否改变；若已知 $\int_L(k+1)\,\dd s=3a$，求 $k$。
\end{problem}

\begin{problem}{357}{63}{弧长积分的保序性}
设 $L$ 为长度非零的分段光滑曲线弧，$f$ 在 $L$ 上连续且非负。证明 $\int_Lf\,\dd s\geq0$；进一步证明，若 $f$ 在 $L$ 的某个内点处为正，则积分严格为正，并据此给出积分等于零的充要条件。
\end{problem}

\begin{problem}{358}{63}{积分比较与严格不等式}
设 $f,g$ 在长度非零的分段光滑曲线弧 $L$ 上连续，且 $f\geq g$。证明
$\int_Lf\,\dd s\geq\int_Lg\,\dd s$。
判断仅有“某一点 $f>g$”能否推出严格不等式，并说明连续性在判断中的作用。
\end{problem}

\begin{problem}{381}{68}{折线上的弧长积分}
设 $L$ 为顶点 $O(0,0),A(1,0),B(0,1)$ 的三角形边界。分边计算
$\oint_L\frac{x}{1+y}\,\dd s$，并求密度为 $\rho(x,y)=1/(1+y)$ 的三角形细丝的质心横坐标。
\end{problem}

\subsection{对坐标的曲线积分}

\begin{problem}{382}{68}{坐标微分与弧长微分}
设 $L$ 为从 $(c,a)$ 到 $(c,b)$ 的有向线段，其中 $a<b$，$P,Q$ 连续。求
$\int_LP(x,y)\,\dd x$ 和 $\int_LQ(x,y)\,\dd y$ 的一元积分表达式；再取 $P\equiv1$，比较 $\int_LP\,\dd x$ 与 $\int_LP\,\dd s$。
\end{problem}

\begin{problem}{383}{68}{常向量场与端点}
设 $L$ 为由 $A(x_1,y_1)$ 到 $B(x_2,y_2)$ 的分段光滑曲线，$k,m$ 为常数。求
$\int_Lk\,\dd x$、$\int_Lk\,\dd y$ 及 $\int_L(k\,\dd x+m\,\dd y)$；据此说明常向量场所做的功与路径无关，并求反向积分。
\end{problem}

\begin{problem}{403}{72}{折点路径与全微分}
设 $L$ 为圆锥面 $z=\sqrt{x^2+y^2}$ 与平面 $y=x$ 的交线上从 $A(1,1,\sqrt2)$ 经原点到 $B(-1,-1,\sqrt2)$ 的曲线弧。
说明 $L$ 在原点处的光滑性，并分别用分段参数法和全微分法计算
$\int_Lyz\,\dd x+zx\,\dd y+xy\,\dd z$。
\end{problem}

\begin{problem}{404}{72}{有向单位切向量}
设 $L$ 是圆周 $x^2+y^2=2y$ 上从原点到 $(0,2)$ 的右半圆弧，$P,Q$ 连续。
求与 $L$ 同向的单位切向量，将 $\int_LP\,\dd x+Q\,\dd y$ 化为对弧长的积分；再取 $P=x,Q=y$ 计算，并检验反向后的符号。
\end{problem}

\begin{problem}{405}{72}{两类曲线积分与方向}
设 $L$ 为 $x=t,y=t^2,z=t^3$ 上 $t$ 从 $1$ 变到 $0$ 的曲线弧，弧长为 $a$。
不用求出 $a$ 的具体数值，计算
\[
 \int_L\frac{\dd x+2x\,\dd y+3y\,\dd z}{\sqrt{1+4x^2+9y^2}}.
\]
再将分子中的三项分别解释为沿正参数方向的单位切向量分量与坐标微分的乘积，说明取向如何决定结果。
\end{problem}

\begin{problem}{406}{72}{抛物线弧上的积分转换}
设 $f$ 连续，$L$ 为 $y=x^2$ 上从 $(1,1)$ 到 $(0,0)$ 的曲线弧。
\begin{enumerate}[label=(\arabic*)]
\item 把 $I=\int_L f(x,y)\,\dd x+2xf(x,y)\,\dd y$ 转化为对弧长的积分，写明符号的来源。
\item 当 $f(x,y)=1/(x^2+3y+1)$ 时计算 $I$。
\item 当 $f$ 在 $L$ 上非负时，判断 $I$ 的符号；给出等号成立的条件。
\end{enumerate}
\end{problem}
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/003.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/004.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/005.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/006.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/007.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/008.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/009.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/010.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/011.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/012.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/013.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/014.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/015.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/016.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/017.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/020.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/023.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/027.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/048.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/052.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/060.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/068.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/073.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/077.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/090.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/093.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/098.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/110.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/113.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/117.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/120.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/123.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/125.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/127.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/129.md


## tool · 2026-10-19T15:14:27Z




## tool · 2026-10-19T15:14:50Z


Script completed
Wall time 0.5 seconds
Output:

{}
from pathlib import Path
import re
import sympy as s

x, y, z, h, t = s.symbols('x y z h t', real=True)

def same(actual, expected):
    assert s.simplify(actual - expected) == 0, (actual, expected)

same(s.integrate(s.integrate(x*y, (y, 0, x)), (x, 0, 1)), s.Rational(1, 8))
same(s.integrate(y+2-y*y, (y, -1, 2)), s.Rational(9, 2))
area274 = s.integrate(2*y, (y, 0, 1)) + s.integrate(3-y, (y, 1, 3))
moment274 = s.integrate(2*y*y, (y, 0, 1)) + s.integrate(y*(3-y), (y, 1, 3))
same(area274, 3)
same(moment274 / area274, s.Rational(4, 3))
same(s.integrate(y*y-y, (y, 1, 2)) + s.integrate(8-x, (x, 2, 8)), s.Rational(113, 6))
same(s.integrate(s.integrate(s.integrate(x*y*y*z**3, (z, 0, x*y)), (y, 0, x)), (x, 0, 1)), s.Rational(1, 364))
same(s.integrate((s.pi/2-x)*s.sin(x)/2, (x, 0, s.pi/2)), s.pi/4-s.Rational(1, 2))
j333 = s.integrate(2*s.pi*z*z*(1-z*z/9), (z, 0, h))
same(j333.subs(h, 1), 28*s.pi/45)
same(s.diff(j333, h), 2*s.pi*h*h*(1-h*h/9))
mass381 = 1 + s.integrate(1/(1+y), (y, 0, 1)) + s.sqrt(2)*s.integrate(1/(1+y), (y, 0, 1))
moment381 = s.Rational(1, 2) + s.sqrt(2)*s.integrate((1-y)/(1+y), (y, 0, 1))
same(mass381, 1+(1+s.sqrt(2))*s.log(2))
same(moment381, s.Rational(1, 2)+s.sqrt(2)*(2*s.log(2)-1))
same(s.integrate((1+4*x*x)/(x*x+3*x*x+1), (x, 1, 0)), -1)
print('Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406')

for chapter in (10, 11):
    path = Path(f'output/宋浩下册工科数学分析改编/chapters/ch{chapter}.tex')
    text = path.read_text()
    numbers = [int(number) for number in re.findall(r'\\begin\{problem\}\{(\d+)\}', text)]
    assert numbers == sorted(set(numbers)), (chapter, numbers)
    assert text.count(r'\begin{problem}') == text.count(r'\end{problem}')
    print(f'Chapter {chapter}: {len(numbers)} unique, ordered problem environments')
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Chapter 10: 14 unique, ordered problem environments
Chapter 11: 10 unique, ordered problem environments


## tool · 2026-10-19T15:14:54Z


Script completed
Wall time 0.1 seconds
Output:

.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/015.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/016.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/017.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/018.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/019.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/020.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/023.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/027.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/048.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/052.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/060.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/068.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/073.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/077.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/090.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/093.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/098.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/110.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/113.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/117.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/120.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/123.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/125.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/127.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/129.md
.agent/hdu-ocr/85b8c8c41edb8e84.json
.agent/hdu-ocr/842284019302ba43.json
.agent/hdu-ocr/local-algebra2023.txt
.agent/hdu-ocr/local-batch.txt
.agent/hdu-ocr/2c29e49c601a658a.md
.agent/hdu-ocr/pip-cache/selfcheck/9a7e5ed7f2912038e816532facfa230cb5b51cb560c6b0994488185b
.agent/hdu-ocr/730ce62de1c053f8.json
.agent/hdu-ocr/compile-run.txt
.agent/hdu-ocr/f5e95ba433b26042.json
.agent/hdu-ocr/be2d15e5112d94ec.md
.agent/hdu-ocr/2c29e49c601a658a.json
.agent/hdu-ocr/model-download.txt
.agent/hdu-ocr/92a5bd5ef85605e7.md
.agent/hdu-ocr/11e51f898301adc8.json
.agent/hdu-ocr/b08aed2582f249fa.md
.agent/hdu-ocr/git-check.txt
.agent/hdu-ocr/85b8c8c41edb8e84.md
.agent/hdu-ocr/collection-ocr.txt
.agent/hdu-ocr/e3e469709b9c871a.json
.agent/hdu-ocr/176002d27d3f75a0.md


## tool · 2026-10-19T15:14:58Z


Script completed
Wall time 0.2 seconds
Output:

宋浩高等数学精选750题下册 (宋浩).pdf
output/宋浩下册工科数学分析改编/main.tex
output/宋浩下册工科数学分析改编/chapters/ch10.tex
output/宋浩下册工科数学分析改编/chapters/ch11.tex
output/宋浩下册工科数学分析改编/chapters/ch08.tex
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/048.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/068.md


## tool · 2026-10-19T15:15:03Z




## tool · 2026-10-19T15:15:06Z


Script completed
Wall time 0.1 seconds
Output:

性质 2 (可加性): 若积分区域 $D$ 被一条曲线分成两个闭区域 $D_1$ 和 $D_2$, 则
$$\iint_D f(x,y) \mathrm{d}\sigma = \iint_{D_1} f(x,y) \mathrm{d}\sigma + \iint_{D_2} f(x,y) \mathrm{d}\sigma.$$

评注
该性质可以推广到积分区域被分成有限个区域的情形.

性质 3: 若在区域 $D$ 上 $f(x,y) \equiv 1$, 则
$$\iint_D f(x,y) \cdot \mathrm{d}\sigma = \iint_D \mathrm{d}\sigma = S_D \leftarrow \text{区域 } D \text{ 的面积}.$$
$$\iint_D k \mathrm{d}\sigma = k \cdot S_D (k \text{ 为常数}).$$

评注
(1) 当 $f(x,y) = k$ ($k$ 为常数) 时, $\iint_D k \mathrm{d}\sigma$ 表示以 $D$ 为底面、高为 $k$ 的平
顶柱体的体积, 其体积 $= \text{底面积} \times \text{高} = S_D \times k$.
(2) 利用该性质可以求平面图形的面积.

性质 4 (比较性): 若在区域 $D$ 上总有 $f(x,y) \leq g(x,y)$, 则
$$\iint_D f(x,y) \mathrm{d}\sigma \leq \iint_D g(x,y) \mathrm{d}\sigma.$$
特别地, 由于
$$-|f(x,y)| \leq f(x,y) \leq |f(x,y)|$$
因此
$$\left| \iint_D f(x,y) \mathrm{d}\sigma \right| \leq \iint_D |f(x,y)| \mathrm{d}\sigma.$$

性质 5 (估值定理): 设 $m$ 和 $M$ 分别是 $z = f(x,y)$ 在区域 $D$ 上的最小值和最
大值, 则
$$m S_D \leq \iint_D f(x,y) \mathrm{d}\sigma \leq M S_D.$$
小平顶柱体的体积 大平顶柱体的体积

性质 6 (积分中值定理): 若函数 $z = f(x,y)$ 在有界闭区域 $D$ 上连续, 则在 $D$
内至少存在一点 $(\xi,\eta)$, 使得
$$\iint_D f(x,y) \mathrm{d}\sigma = f(\xi,\eta) \cdot S_D.$$

评注
(1) 积分中值定理的几何意义: 在有界闭区域 $D$ 上以 $f(x,y)$ 为顶的
曲顶柱体的体积和平顶柱体的体积相等, 该平顶柱体以区域 $D$ 为底面, 以区域
$D$ 上某一点 $(\xi,\eta)$ 的函数值 $f(\xi,\eta)$ 为高.

## tool · 2026-10-19T15:15:10Z


Script completed
Wall time 0.1 seconds
Output:


## tool · 2026-10-19T15:15:14Z


Script completed
Wall time 0.1 seconds
Output:

第一节 对面积的曲面积分（第一类曲面积分）

一、对面积的曲面积分的定义与性质

定义：设 $\Sigma$ 为分片光滑曲面，函数 $f(x,y,z)$ 在 $\Sigma$ 上有界，$f(x,y,z)$ 在曲面 $\Sigma$ 上对面积的曲面积分为 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S \triangleq \lim_{\lambda \to 0} \sum_{i=1}^{n} f(\xi_i,\eta_i,\zeta_i) \Delta S_i$，其中 $\Delta S_i$ 为第 $i$ 个小曲面块的面积．如果 $f(x,y,z)$ 在 $\Sigma$ 上连续，则 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S$ 存在．

性质：积分与曲面 $\Sigma$ 的侧的选取无关，即 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S = \iint_{\Sigma} f(x,y,z) \mathrm{d}S$，其中 $\Sigma^{-}$ 表示曲面 $\Sigma$ 的另外一侧．

奇偶性和对称性

(1) 关于积分曲面的对称性和被积函数的奇偶性

$\textcircled{1}$ 设 $\Sigma$ 关于 $xOy$ 平面（或变量 $z$）对称，$\Sigma_1$ 为 $\Sigma$ 位于 $xOy$ 平面上方（$z \geq 0$）的部分，则 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S = \begin{cases} 0, & f(x,y,z) \text{是关于} z \text{的奇函数} \\ 2 \iint_{\Sigma_1} f(x,y,z) \mathrm{d}S, & f(x,y,z) \text{是关于} z \text{的偶函数} \end{cases}$

$\textcircled{2}$ 设 $\Sigma$ 关于 $yOz$ 平面（或变量 $x$）对称，$\Sigma_1$ 为 $\Sigma$ 位于 $yOz$ 平面前方（$x \geq 0$）的部分，则 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S = \begin{cases} 0, & f(x,y,z) \text{是关于} x \text{的奇函数} \\ 2 \iint_{\Sigma_1} f(x,y,z) \mathrm{d}S, & f(x,y,z) \text{是关于} x \text{的偶函数} \end{cases}$

$\textcircled{3}$ 设 $\Sigma$ 关于 $xOz$ 平面（或变量 $y$）对称，$\Sigma_1$ 为 $\Sigma$ 位于 $xOz$ 平右侧（$y \geq 0$）的部分，则 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S = \begin{cases} 0, & f(x,y,z) \text{是关于} y \text{的奇函数} \\ 2 \iint_{\Sigma_1} f(x,y,z) \mathrm{d}S, & f(x,y,z) \text{是关于} y \text{的偶函数} \end{cases}$

(2) 关于变量的对称性质

$\textcircled{1}$ 如果积分曲面 $\Sigma$ 的方程中某两个变量对调后 $\Sigma$ 的方程不变，则将被积函数中这两个变量对调，曲面积分 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S$ 的值也不变．

例如，若 $\Sigma$ 的方程中 $x,y$ 对调后 $\Sigma$ 的方程不变，则 $\iint_{\Sigma} f(x,y,z) \mathrm{d}S =$

## tool · 2026-10-19T15:15:47Z


Wall time: 30.0046 seconds
Sleep completed.

## tool · 2026-10-19T15:15:51Z


Script completed
Wall time 0.1 seconds
Output:

(2) 性质 6 可变形为 $f(\xi, \eta) = \frac{\iint_D f(x, y) \mathrm{d}\sigma}{S_D} \leftarrow$ 平均高度，即 $f(x, y)$ 在区域 $D$ 上的平均值.

性质 7 (对称性质):

(1) 若区域 $D$ 关于 $x$ 轴对称，$D_1$ 为 $D$ 在 $x$ 轴的上半部分，则
$$\iint_D f(x, y) \mathrm{d}\sigma = \begin{cases} 0, & f(x, y) = -f(x, y) \\ 2 \iint_D f(x, y) \mathrm{d}\sigma, & f(x, y) = f(x, y) \end{cases};$$

(2) 若区域 $D$ 关于 $y$ 轴对称，$D_1$ 为 $D$ 在 $y$ 轴的右半部分，则
$$\iint_D f(x, y) \mathrm{d}\sigma = \begin{cases} 0, & f(-x, y) = -f(x, y) \\ 2 \iint_D f(x, y) \mathrm{d}\sigma, & f(-x, y) = f(x, y) \end{cases};$$

(3) 若区域 $D$ 关于原点对称，$D_1$ 为 $D$ 的右半平面部分，则
$$\iint_D f(x, y) \mathrm{d}\sigma = \begin{cases} 0, & f(-x, y) = -f(x, y) \\ 2 \iint_D f(x, y) \mathrm{d}\sigma, & f(-x, y) = f(x, y) \end{cases};$$

(4) 若区域 $D$ 关于直线 $y = x$ 对称，则
$$\iint_D f(x, y) \mathrm{d}\sigma = \iint_D f(y, x) \mathrm{d}\sigma = \frac{1}{2} \left[ \iint_D f(x, y) \mathrm{d}\sigma + \iint_D f(y, x) \mathrm{d}\sigma \right].$$

评注
利用二重积分的对称性质可以有效减少计算量，但要注意的是，当被积函数的奇偶性及积分区域 $D$ 的对称性两者兼得时，我们才可以使用二重积分的对称性质.

259 基础题 比较积分 $\iint_D \ln(x + y) \mathrm{d}\sigma$ 与 $\iint_D [\ln(x + y)]^2 \mathrm{d}\sigma$ 的大小，其中积分区域 $D$ 是三角形闭区域，3 个顶点分别为 $(1, 0), (1, 1), (0, 1).$

260 基础题 比较积分 $I_1 = \iint_D \frac{x + y}{4} \mathrm{d}\sigma, I_2 = \iint_D \sqrt{\frac{x + y}{4}} \mathrm{d}\sigma, I_3 = \iint_D \sqrt{\frac{x + y}{4}} \mathrm{d}\sigma$ 的大小，其中积分区域 $D$ 是由 $(x - 1)^2 + (y - 1)^2 \leqslant 2$ 围成的闭区域.

261 基础题 估计二重积分 $I = \iint_D \sin^2 x \sin^2 y \mathrm{d}\sigma$ 的值，其中积分区域 $D = \{(x, y) | 0 \leqslant x \leqslant \pi, 0 \leqslant y \leqslant \pi\}$.262 基础题 估计二重积分 $I = \iint_D (x^2 + 4y^2 + 9) \mathrm{d}\sigma$ 的值，其中积分区域 $D = \{(x, y) | x^2 + y^2 \leq 4\}$.

263 基础题 设 $f(x, y) = \begin{cases} 1, & 0 \leq x \leq 3, 0 \leq y \leq 1 \\ 2, & 0 \leq x \leq 3, 1 < y \leq 2 \\ 3, & 0 \leq x \leq 3, 2 < y \leq 3 \end{cases}$，计算 $\iint_D f(x, y) \mathrm{d}\sigma$，其中积分区域 $D = \{(x, y) | 0 \leq x \leq 3, 0 \leq y \leq 3\}$.

264 基础题 设区域 $D$ 是由 $y = 0, y = x, x = 1$ 围成的区域，求函数 $f(x, y) = xy$ 在区域 $D$ 上的平均值.

265 中等题 求极限 $\lim_{r \to 0} \frac{1}{\pi r^2} \iint_D e^{x^2 - y^2} \cos(x + y) \mathrm{d}x \mathrm{d}y$，其中 $D = \{(x, y) | x^2 + y^2 \leq r^2\}$.

266 中等题 设函数 $f(x, y)$ 在点 $(0, 0)$ 的某个邻域内连续，$f(0, 0) = 1$，$g(x)$ 有连续的导数，且 $g(0) = 0, g'(0) = 3$，求极限 $\lim_{r \to 0} \frac{\iint_D f(x, y) \mathrm{d}x \mathrm{d}y}{g(r^2)}$ 的值，其中 $D = \{(x, y) | x^2 + y^2 \leq r^2\}$.

267 基础题 设积分区域 $D$ 是由直线 $x = -1, x = 1, y = -2, y = 2$ 围成的闭区域，则 $\iint_D (x^2 \tan y + \sin x^3) \mathrm{d}\sigma =$ ____.

268 基础题 设积分区域 $D = \{(x, y) | x^2 + y^2 \leq 4, x \leq 0, y \leq 0\}$，$f(x)$ 是区域 $D$ 上的正值连续函数，$a, b$ 为常数，则 $\iint_D \frac{af(x) + bf(y)}{f(x) + f(y)} \mathrm{d}\sigma =$ ____.

269 基础题 设积分区域 $D$ 是以 $A(1, 1), B(-1, 1), C(-1, -1)$ 为顶点的三角形闭区域，$D_1$ 是 $D$ 在第一象限中的部分，则 $\iint_D (x^3 y + \cos x \sin y) \mathrm{d}\sigma =$ (    ).

(A) 0

(B) $4 \iint_D (x^3 y + \cos x \sin y) \mathrm{d}\sigma$

(C) $2 \iint_D x^3 y \mathrm{d}\sigma$

(D) $2 \iint_D \cos x \sin y \mathrm{d}\sigma$二、平面直角坐标系下二重积分的计算

平面直角坐标系下的二重积分 $\iint_D f(x,y) \mathrm{d}x \mathrm{d}y$ 通常要化为两次定积分来进行计算，所以确定两次积分的积分限和选择恰当的积分次序是非常重要的，这两者都取决于积分区域 $D$ 是 $X$ 型区域还是 $Y$ 型区域.

选择积分次序一般遵循以下两个原则：

(1) 积分区域尽量避免分块；

(2) 被积函数第一次积分易得出结果.

一般来说，二重积分的计算按照如下步骤进行.

第1步：画出积分区域 $D$ 的图像.

第2步：写出区域 $D$ 的坐标描述，从而确定两次积分的积分次序和积分限.

第3步：计算两次定积分.

平面直角坐标系下二重积分的计算通常有以下几种情形.

情形1：积分区域 $D = \{(x,y)|a \leq x \leq b,c \leq y \leq d\}$，被积函数 $f(x,y) = f_1(x) \cdot f_2(y)$，此时

$$\iint_D f(x,y) \mathrm{d}x \mathrm{d}y = \int_a^b f_1(x) \mathrm{d}x \cdot \int_c^d f_2(y) \mathrm{d}y.$$

情形2：积分区域 $D = \{(x,y)|a \leq x \leq b,c \leq y \leq d\}$，此时

$$\iint_D f(x,y) \mathrm{d}x \mathrm{d}y = \int_a^b dx \int_c^d f(x,y) \mathrm{d}y = \int_c^d dy \int_a^b f(x,y) \mathrm{d}x.$$

情形3：积分区域 $D$ 是 $X$ 型区域，即 $D = \{(x,y)|a \leq x \leq b,\varphi_1(x) \leq y \leq \varphi_2(x)\}$，此时

$$\iint_D f(x,y) \mathrm{d}x \mathrm{d}y = \int_a^b dx \int_{\varphi_1(x)}^{\varphi_2(x)} f(x,y) \mathrm{d}y.$$

情形4：积分区域 $D$ 是 $Y$ 型区域，即 $D = \{(x,y)|\phi_1(y) \leq x \leq \phi_2(y),c \leq y \leq d\}$，此时

$$\iint_D f(x,y) \mathrm{d}x \mathrm{d}y = \int_c^d dy \int_{\varphi_1(y)}^{\varphi_2(y)} f(x,y) \mathrm{d}x.$$

情形5：当积分区域 $D$ 既不是 $X$ 型区域也不是 $Y$ 型区域时，我们需用平行于 $x$ 轴或 $y$ 轴的直线将区域 $D$ 分割，使每个小区域是 $X$ 型区域或 $Y$ 型区域，然后利用积分的区域可加性进行计算.

279 基础题 计算二重积分 $\iint_D e^{x-y} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=0,x=1,y=0,$ $y=1$ 围成的矩形.

## tool · 2026-10-19T15:16:04Z




## tool · 2026-10-19T15:16:45Z


Script completed
Wall time 0.1 seconds
Output:

\section{第10章\quad 重积分}
\subsection{二重积分的概念与性质}

\begin{problem}{256}{43}{积分方程与参数讨论}
设 $D=\{(x,y):0\leq y\leq x\leq1\}$，$\lambda\in\mathbb R$。讨论连续函数方程
\[
 f(x,y)=xy+\lambda\iint_D f(u,v)\,\dd u\dd v
\]
的解是否存在、是否唯一；存在时求出 $f(x,y)$，并给出 $\lambda=1$ 时的结果。
\end{problem}

\begin{problem}{257}{43}{二重和的积分极限}
将下列极限分别表示为二重积分并计算，说明两者积分区域的差别：
\[
 \lim_{n\to\infty}\sum_{i=1}^n\sum_{j=1}^n
 \frac{n}{(n+i)(n^2+j^2)},\qquad
 \lim_{n\to\infty}\sum_{i=1}^n\sum_{j=1}^i
 \frac{n}{(n+i)(n^2+j^2)}.
\]
第二个极限只须化为一个定积分，无须求出初等形式。
\end{problem}

\begin{problem}{258}{43}{黎曼和与误差估计}
计算
\[
 L=\lim_{n\to\infty}\frac{\pi}{2n^4}
 \sum_{i=1}^n\sum_{j=1}^n i^2\sin\frac{j\pi}{2n}.
\]
利用 $x^2$ 与 $\sin y$ 在相应区间上的单调性，说明该和式与 $L$ 之差为 $O(1/n)$。
\end{problem}

\begin{problem}{270}{47}{对称性与圆域积分}
设 $D=\{(x,y):x^2+y^2\leq1\}$。不先作二次积分，利用对称性求
\[
 \iint_D(x^2+2y)\,\dd x\dd y,

{}
4:\begin{problem}{256}{43}{积分方程与参数讨论}
12:\begin{problem}{257}{43}{二重和的积分极限}
23:\begin{problem}{258}{43}{黎曼和与误差估计}
32:\begin{problem}{259}{45}{积分比较与严格性}
37:\begin{problem}{261}{45}{积分估值与分离变量}
42:\begin{problem}{262}{46}{最优函数界与积分估值}
46:\begin{problem}{263}{46}{分片常值函数的积分}
54:\begin{problem}{264}{46}{平均值与中值点}
58:\begin{problem}{265}{46}{缩小圆域上的平均值极限}
64:\begin{problem}{266}{46}{局部连续性与积分极限}
69:\begin{problem}{267}{46}{对称性使用的存在性条件}
76:\begin{problem}{268}{46}{变量互换与参数积分}
83:\begin{problem}{269}{46}{三角形区域上的对称分解}
88:\begin{problem}{270}{47}{对称性与圆域积分}
98:\begin{problem}{271}{47}{交换积分次序与计算}
103:\begin{problem}{272}{47}{半圆域与积分次序}
111:\begin{problem}{273}{47}{分块区域的合并}
120:\begin{problem}{274}{47}{分段边界与换序}
129:\begin{problem}{275}{47}{三角函数边界的换序}
134:\begin{problem}{276}{47}{不同次序积分的区域辨析}
143:\begin{problem}{277}{47}{变限二重积分求导}
150:\begin{problem}{331}{55}{空间区域与幂函数积分}
156:\begin{problem}{332}{55}{三重积分的次序选择}
165:\begin{problem}{333}{55}{椭球截面与参数积分}


## tool · 2026-10-19T15:16:55Z


Script completed
Wall time 0.1 seconds
Output:

280 基础题 计算二重积分 $\iint_D (x+y) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=0, x=1, y=0, y=1$ 围成的矩形区域.

281 基础题 计算二重积分 $\iint_D x \mathrm{e}^{xy} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=0, x=1, y=0, y=1$ 围成的矩形区域.

282 基础题 计算二重积分 $\iint_D x y \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=2, y=1, y=x$ 围成的区域.

283 基础题 计算二重积分 $\iint_D x \sqrt{y} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由两条抛物线 $y=\sqrt{x}, y=x^2$ 围成的区域.

284 基础题 计算二重积分 $\iint_D (3x+2y) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由两坐标轴及直线 $x+y=2$ 围成的区域.

285 基础题 计算二重积分 $\iint_D x \cos(x+y) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是顶点分别为 $(0,0), (\pi,0), (\pi,\pi)$ 的三角形闭区域.

286 基础题 计算二重积分 $\iint_D \frac{x^2}{y^2} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=2, xy=1, y=x$ 围成的区域.

287 基础题 计算二重积分 $\iint_D (x+6y) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=1, y=x, y=5x$ 围成的区域.

288 基础题 计算二重积分 $\iint_D (1+x) \sin y \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是顶点分别为 $(0,0), (1,0), (0,1)$ 和 $(1,2)$ 的梯形闭区域.

289 基础题 计算二重积分 $\iint_D (x^2+y^2-x) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $y=2, y=x, y=2x$ 围成的区域.290 基础题 计算二重积分 $\iint_D (x^2 + y^2) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $y=1, y=3, y=x, y=x+1$ 围成的区域.

291 中等题 计算二重积分 $\iint_D x \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是顶点分别为 $O(0, 0), A(1, 2), B(2, 1)$ 的三角形闭区域.

292 基础题 已知积分区域 $D$ 是由 $x=1, y=2, y=x-1$ 围成的区域，计算二重积分 $\iint_D \cos y^2 \mathrm{d}x \mathrm{d}y$.

293 基础题 计算二重积分 $\iint_D \frac{\sin x}{x} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由直线 $y=x$ 及抛物线 $y=x^2$ 围成的区域.

294 基础题 已知积分区域 $D$ 是由 $x=0, y=1, y=x$ 围成的区域，计算二重积分 $\iint_D (\mathrm{e}^{-y^2}-1) \mathrm{d}x \mathrm{d}y$.

295 基础题 计算二重积分 $\iint_D x^2 \mathrm{e}^{-y^2} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=0, y=1, y=x$ 围成的区域.

296 基础题 计算二重积分 $\iint_D \mathrm{e}^{x^2} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由 $x=\frac{1}{2}, x=1, y=x, y=x^2$ 围成的区域.

297 中等题 计算二重积分 $I = \int_0^1 \mathrm{d}x \int_x^1 (y+x \mathrm{e}^{y^2}) \mathrm{d}y$.

298 中等题 计算二重积分 $I = \int_0^1 \mathrm{d}x \int_x^1 \frac{xy}{\sqrt{1+y^3}} \mathrm{d}y$.

299 中等题 计算二重积分 $I = \int_0^{\ln 2} \mathrm{d}y \int_{\mathrm{e}^y}^2 \frac{\mathrm{e}^{xy}}{x^x-1} \mathrm{d}x$.

300 提高题 已知 $f(x)$ 具有三阶连续导数，且 $f(0) = f'(0) = f''(0) = -1, f(2) = -\frac{1}{2}$. 计算二重积分 $I = \int_0^2 \mathrm{d}x \int_0^x \sqrt{(2-x)(2-y)} f'''(y) \mathrm{d}y$.301 中等题 已知 $f(x) = g(x) = \begin{cases} a, & 0 \leqslant x \leqslant 1 \\ 0, & \text{其他} \end{cases}$, 且 $a > 0$. 计算二重积分
$I = \iint_D f(x)g(y-x)dxdy$, 其中积分区域 $D$ 表示整个坐标面.

302 中等题 已知函数 $f(x,y) = \begin{cases} x^2y, & 1 \leqslant x \leqslant 2, 0 \leqslant y \leqslant x \\ 0, & \text{其他} \end{cases}$, 计算二重积分
$I = \iint_D f(x,y)dxdy$, 其中积分区域 $D = \{(x,y)|x^2 + y^2 \geqslant 2x\}$.

303 中等题 计算二重积分 $\iint_D |y-x^2|dxdy$, 其中积分区域
$D = \{(x,y)|-1 \leqslant x \leqslant 1, 0 \leqslant y \leqslant 1\}$.

304 中等题 计算二重积分 $\iint_D \max\{xy,1\}dxdy$, 其中积分区域
$D = \{(x,y)|0 \leqslant x \leqslant 2, 0 \leqslant y \leqslant 2\}$.

305 中等题 计算二重积分 $\iint_D e^{\max\{x^2,y^2\}}dxdy$, 其中积分区域 $D$ 是由 $x=0, x=1,$
$y=0, y=1$ 围成的矩形区域.

306 提高题 计算二重积分 $\iint_D (\sqrt{|x|} + \sqrt{|y|})dxdy$, 其中积分区域
$D = \{(x,y)|\sqrt{|x|} + \sqrt{|y|} \leqslant 1\}$.

三、利用极坐标计算二重积分

当积分区域 $D$ 为圆域或圆域的一部分，或扇形区域，或区域 $D$ 的边界方程用极坐标表示极为简单，或被积函数为 $f(x^2+y^2), f\left(\frac{x}{y}\right), f\left(\frac{y}{x}\right)$ 等形式时，通常利用极坐标计算二重积分比较简单.

极坐标和平面直角坐标之间的关系要牢记. 设点 $P$ 在平面直角坐标系和极坐标系下的坐标分别为 $P(x,y)$ 和 $P(\rho,\theta)$, 则
$$\begin{cases} \rho = \sqrt{x^2+y^2} \\ \tan \theta = \frac{y}{x} \end{cases}, \quad \begin{cases} x = \rho \cos \theta \\ y = \rho \sin \theta \end{cases}, \mathrm{d}x\mathrm{d}y = \rho \mathrm{d}\rho \mathrm{d}\theta.$$
从而
$$\iint_D f(x,y)dxdy = \iint_D f(\rho \cos \theta, \rho \sin \theta) \mathrm{d}\rho \mathrm{d}\theta.$$
极坐标系下二重积分的计算步骤与平面直角坐标系下二重积分的计算步骤完全类似，不再赘述.307 基础题 计算二重积分 $\iint_D \arctan \frac{y}{x} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 为圆周 $x^2 + y^2 = 1$，$x^2 + y^2 = 9$，以及直线 $x = \sqrt{3} y, y = \sqrt{3} x$ 围成的第一象限的部分.

308 基础题 计算二重积分 $\iint_D \sqrt{\frac{1 - x^2 - y^2}{1 + x^2 + y^2}} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 为圆周 $x^2 + y^2 = 1$ 及坐标轴围成的第一象限内的闭区域.

309 基础题 设积分区域 $D = \{(x, y) | x^2 + y^2 \leq a^2\}$，且 $\iint_D \sqrt{a^2 - x^2 - y^2} \mathrm{d}x \mathrm{d}y = \pi$，其中 $a > 0$，求 $a$ 的值.

310 中等题 计算二重积分 $\int_0^a \mathrm{d}x \int_0^{\sqrt{a^2 - x^2}} \sqrt{x^2 + y^2} \mathrm{d}y$.

311 中等题 计算二重积分 $\iint_D (x^2 - y) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D = \{(x, y) | x^2 + y^2 \leq 1\}$.

312 中等题 计算二重积分 $\iint_D x^2 \ln(x^2 + y^2) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D = \{(x, y) | 1 \leq x^2 + y^2 \leq e^2\}$.

313 中等题 设平面区域 $D = \{(x, y) | x^2 + y^2 \leq 1, x \geq 0, y \geq 0\}$，计算 $\iint_D \frac{x \cos(x^2 + y^2)}{x + y} \mathrm{d}x \mathrm{d}y$.

314 中等题 计算二重积分 $\iint_D \frac{1}{\sqrt{x^2 + y^2}} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由直线 $x = 1$，$y = 0$ 及 $y = x$ 围成的区域.

315 中等题 计算二重积分 $\iint_D \sqrt{x^2 + y^2} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由直线 $x = 1$，$y = 0$ 及 $y = x$ 围成的区域.

316 中等题 计算二重积分 $\int_0^1 \mathrm{d}x \int_x^x \frac{1}{\sqrt{x^2 + y^2}} \mathrm{d}y$.

317 中等题 计算二重积分 $\iint_D \frac{y^2}{x^2} \mathrm{d}x \mathrm{d}y$，其中积分区域 $D$ 是由直线 $y = 0, y = x$ 及曲线 $y = \sqrt{4x - x^2}, y = \sqrt{9x - x^2}$ 围成的区域.

## tool · 2026-10-19T15:17:14Z




## tool · 2026-10-19T15:18:12Z


Script completed
Wall time 0.2 seconds
Output:

\]
分别用不等式描述两项对应的区域，判断其内部是否相交；将 $I$ 全部改为先对 $x$ 积分，并计算 $f\equiv1$ 时的值。
\end{problem}

\begin{problem}{277}{47}{变限二重积分求导}
设 $f$ 在 $[1,+\infty)$ 上连续，$F(t)=\int_1^t\dd y\int_y^t f(x)\,\dd x$，$t\geq1$。
先交换积分次序，再求 $F'(t)$ 与 $F'(3)$；若 $f$ 处处为正，判断 $F$ 在 $(1,+\infty)$ 上的单调性并说明理由。
\end{problem}

\subsection{三重积分}

\begin{problem}{331}{55}{空间区域与幂函数积分}
设 $\Omega=\{(x,y,z):0\leq y\leq x\leq1,\ 0\leq z\leq xy\}$。
写出先对 $z$ 积分与先对 $y$ 积分的两种累次积分，计算
$\iiint_\Omega xy^2z^3\,\dd x\dd y\dd z$，并说明曲面 $z=xy$ 与 $z=0$ 如何确定区域的下边界 $y=0$。
\end{problem}

\begin{problem}{332}{55}{三重积分的次序选择}
设 $\Omega=\{(x,y,z):0\leq x\leq\pi/2,\ 0\leq y\leq\sqrt{x},\ 0\leq z\leq\pi/2-x\}$。
将 $\sin x/x$ 在 $x=0$ 处作连续延拓，计算
\[
 \iiint_\Omega\frac{y\sin x}{x}\,\dd x\dd y\dd z,
\]
并解释先对 $y,z$ 积分为何能消去分母 $x$ 带来的计算困难。
\end{problem}

\begin{problem}{333}{55}{椭球截面与参数积分}
设 $0<h\leq3$，$\Omega_h=\{(x,y,z):x^2+y^2/4+z^2/9\leq1,\ 0\leq z\leq h\}$。
用水平截面法求 $J(h)=\iiint_{\Omega_h}z^2\,\dd V$，求 $J(1)$，并说明 $J'(h)$ 的几何意义。
\end{problem}

{}
111:\begin{problem}{273}{47}{分块区域的合并}
120:\begin{problem}{274}{47}{分段边界与换序}
129:\begin{problem}{275}{47}{三角函数边界的换序}
134:\begin{problem}{276}{47}{不同次序积分的区域辨析}
143:\begin{problem}{277}{47}{变限二重积分求导}
148:\begin{problem}{279}{48}{矩形域与参数变化}
152:\begin{problem}{280}{49}{区域分割与积分份额}
156:\begin{problem}{281}{49}{含参积分与零参数}
160:\begin{problem}{282}{49}{三角形域与尺度参数}
164:\begin{problem}{283}{49}{曲边域与加权平均}
168:\begin{problem}{284}{49}{线性密度与形心比较}
172:\begin{problem}{285}{49}{三角形积分的参数表达}
176:\begin{problem}{286}{49}{双曲线边界与参数}
180:\begin{problem}{287}{49}{非均匀薄片的一阶矩}
184:\begin{problem}{288}{49}{梯形区域与边界参数}
188:\begin{problem}{289}{49}{缩放区域与积分符号}
193:\begin{problem}{290}{50}{平行四边形上的变量代换}
197:\begin{problem}{291}{50}{三角形薄片的一阶矩}
201:\begin{problem}{292}{50}{积分次序与非初等原函数}
205:\begin{problem}{293}{50}{可去奇点与曲边区域}
209:\begin{problem}{294}{50}{三角形域与符号估计}
213:\begin{problem}{295}{50}{密度积分与高斯型因子}
217:\begin{problem}{296}{50}{曲线间宽度与精确积分}
221:\begin{problem}{297}{50}{换序与线性分解}
225:\begin{problem}{298}{50}{参数上限与积分求导}
229:\begin{problem}{299}{50}{角点反常积分与换序}
237:\begin{problem}{300}{50}{换序与分部积分}
247:\begin{problem}{331}{55}{空间区域与幂函数积分}
253:\begin{problem}{332}{55}{三重积分的次序选择}
262:\begin{problem}{333}{55}{椭球截面与参数积分}


## tool · 2026-10-19T15:18:27Z




## tool · 2026-10-19T15:18:31Z


Script completed
Wall time 0.1 seconds
Output:

318 中等题 计算二重积分 $\iint_D (x-y) \mathrm{d}x \mathrm{d}y$，其中积分区域
$D = \{(x,y)|(x-1)^2 + (y-1)^2 \leqslant 2, y \geqslant x\}$.

319 提高题 计算二重积分 $\iint_D (x+y^2) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D = \{(x,y)|x^2+y^2 \leqslant x\}$.

320 中等题 设闭区域 $D = \{(x,y)|x^2+y^2 \leqslant y, x \geqslant 0\}$，$f(x,y)$ 为闭区域 $D$ 上的连
续函数，且 $f(x,y) = \sqrt{1-x^2-y^2} - \frac{8}{\pi} \iint_D f(u,v) \mathrm{d}u \mathrm{d}v$，求 $f(x,y)$.

321 提高题 计算二重积分 $I = \iint_D \min \left\{ \sqrt{\frac{3}{16}-x^2-y^2}, 2(x^2+y^2) \right\} \mathrm{d}x \mathrm{d}y$，其中积分区
域 $D = \{(x,y)|x^2+y^2 \leqslant \frac{3}{16}\}$.

322 提高题 计算二重积分 $I = \iint_D |x y| \mathrm{d}x \mathrm{d}y$，其中积分区域
$D = \{(x,y)|x^2+y^2 \geqslant x, |x| \leqslant 1, |y| \leqslant 1\}$.

四、二重积分的换元法

定理：设 $f(x,y)$ 在 $xOy$ 平面上的闭区域 $D$ 内连续，若变换
$T: x = x(u,v), y = y(u,v)$
将 $uOv$ 平面上的闭区域 $D'$ 变为 $xOy$ 平面上的 $D$，且满足
(1) $x(u,v), y(u,v)$ 在 $D'$ 上具有一阶连续偏导数.
(2) $D'$ 上雅可比行列式 $J(u,v) = \frac{\partial(x,y)}{\partial(u,v)} \neq 0$.
(3) 变换 $T$ 是 $D'$ 与 $D$ 之间的一个一一对应，则
$\iint_D f(x,y) \mathrm{d}x \mathrm{d}y = \iint_D f[x(u,v), y(u,v)] |J(u,v)| \mathrm{d}u \mathrm{d}v$.

评注
(1) 如果雅可比行列式 $J(u,v)$ 只在 $D'$ 内个别点上或 $D'$ 的一条曲线上
为零，而在其他点上不为零，则上述公式仍然成立.
(2) 将平面直角坐标系下二重积分的计算转化为极坐标进行计算其实是特殊的
换元积分法. 令 $x = \rho \cos \theta, y = \rho \sin \theta$，雅可比行列式$J = \frac{\partial(x,y)}{\partial(\rho,\theta)} = \begin{vmatrix} \frac{\partial x}{\partial \rho} & \frac{\partial x}{\partial \theta} \\ \frac{\partial y}{\partial \rho} & \frac{\partial y}{\partial \theta} \end{vmatrix} = \begin{vmatrix} \cos \theta & -\rho \sin \theta \\ \sin \theta & \rho \cos \theta \end{vmatrix} = \rho$,

其仅在 $\rho = 0$ 时为零，故
$$\iint_D f(x,y) \mathrm{d}x \mathrm{d}y = \iint_D f(\rho \cos \theta, \rho \sin \theta) \rho \mathrm{d} \rho \mathrm{d} \theta.$$

323 基础题 做适当的变换，计算二重积分 $\iint_D (x+y) \sin(x-y) \mathrm{d}x \mathrm{d}y$，其中
$$D = \{(x,y) | 0 \leq x+y \leq \pi, 0 \leq x-y \leq \pi\}.$$

324 基础题 计算二重积分 $\iint_D \left( \frac{x^2}{a^2} + \frac{y^2}{b^2} \right) \mathrm{d}x \mathrm{d}y$，其中 $D = \left\{(x,y) \mid \frac{x^2}{a^2} + \frac{y^2}{b^2} \leq 1 \right\}.$

325 基础题 做适当的变换，计算二重积分 $\iint_D \mathrm{e}^{\frac{x}{x+y}} \mathrm{d}x \mathrm{d}y$，其中
$$D = \{(x,y) | x+y \leq 1, x \geq 0, y \geq 0 \}.$$

326 基础题 设区域 $D$ 是由曲线 $xy = 4, xy = 8, xy^3 = 5, xy^3 = 15$ 围成的第一象限中的闭区域，求 $D$ 的面积.

327 中等题 证明 $\iint_D f(x+y) \mathrm{d}x \mathrm{d}y = \int_{-1}^{1} f(u) \mathrm{d}u$，其中闭区域 $D = \{(x,y) \parallel x| + |y| \leq 1\}$.

五、广义二重积分的计算

广义二重积分的计算方法及步骤参照正常二重积分的计算方法及步骤进行即可.

328 基础题 计算二重积分 $\iint_D x \mathrm{e}^{-y^2} \mathrm{d}x \mathrm{d}y$，其中 $D$ 是由曲线 $y = 4x^2$ 与 $y = 9x^2$ 在第一象限围成的无界区域.

329 中等题 计算二重积分 $\int_0^{+\infty} \mathrm{d}x \int_x^{\sqrt{3}x} \mathrm{e}^{-(x^2+y^2)} \mathrm{d}y$.$P(\rho, \theta)$, 则 $(\rho, \theta, z)$ 叫作点 $M$ 的柱面坐标. 显然, 点 $M$ 的空间直角坐标与柱面坐标的关系式为
$$\begin{cases} x = \rho \cos \theta \\ y = \rho \sin \theta \\ z = z \end{cases}$$
当 $\Omega$ 的投影区域为圆域、环域或环域的一部分, 或被积函数为 $f(x^2 + y^2)$ 时, 三重积分常用柱面坐标来计算. 此时, 应注意确定变量 $\rho, \theta, z$ 的取值范围. 若
$$\Omega: \alpha \leq \theta \leq \beta, \rho_1(\theta) \leq \rho \leq \rho_2(\theta), z_1(\rho, \theta) \leq z \leq z_2(\rho, \theta),$$
则
$$\iiint_{\Omega} f(x, y, z) \mathrm{d}x \mathrm{d}y \mathrm{d}z = \iiint_{\Omega} \rho f(\rho \cos \theta, \rho \sin \theta, z) \mathrm{d} \rho \mathrm{d} \theta \mathrm{d}z$$
$$= \int_{\alpha}^{\beta} \mathrm{d} \theta \int_{\rho_1(\theta)}^{\rho_2(\theta)} \rho \mathrm{d} \rho \int_{z_1(\rho, \theta)}^{z_2(\rho, \theta)} f(\rho \cos \theta, \rho \sin \theta, z) \mathrm{d} z.$$

334 中等题 计算三重积分 $\iiint_{\Omega} z \mathrm{d} V$, 其中 $\Omega$ 是由曲面 $z = \sqrt{2 - x^2 - y^2}$ 和 $z = x^2 + y^2$ 围成的闭区域.

335 中等题 计算三重积分 $\iiint_{\Omega} (x^2 + y^2)^2 \mathrm{d} V$, 其中 $\Omega$ 是由 $z = x^2 + y^2, z = 1, z = 2$ 围成的闭区域.

336 中等题 计算三重积分 $\iiint_{\Omega} (x^2 + y^2 + z^2) \mathrm{d} V$, 其中 $\Omega$ 是由曲线 $\left\{ \begin{array}{l} x = 0 \\ y^2 = 2 z \end{array} \right.$ 绕 $z$ 轴旋转一周而成的曲面与平面 $z = 1$ 围成的区域.

三、利用球面坐标计算三重积分

设 $M(x, y, z)$ 为空间内一点, 则点 $M$ 可以用 3 个有次序的数 $(r, \varphi, \theta)$ 来确定, 其中 $r$ 为原点 $O$ 与点 $M$ 之间的距离, $\varphi$ 为有向线段 $\overline{OM}$ 与 $z$ 轴正方向的夹角, $\theta$ 为从 $z$ 轴正方向来看自 $x$ 轴按逆时针方向转到有向线段 $\overline{OP}$ 的角, 这里的点 $P$ 为点 $M$ 在 $xOy$ 平面上的投影点, $(r, \varphi, \theta)$ 叫作点 $M$ 的球面坐标. 点 $M$ 的空间直角坐标与球面坐标的关系式为
$$\begin{cases} x = r \sin \varphi \cos \theta \\ y = r \sin \varphi \sin \theta, \text{且} \mathrm{d} V = r^2 \sin \varphi \mathrm{d} r \mathrm{d} \varphi \mathrm{d} z. \\ z = r \cos \varphi \end{cases}$$当 $\Omega$ 为球域或球域的一部分，或被积函数为 $f(x^2 + y^2 + z^2)$ 时，三重积分常用球面坐标来计算. 此时，应注意确定变量 $r, \varphi, \theta$ 的取值范围. 若

$$\Omega: \alpha \leqslant \theta \leqslant \beta, \varphi_1(\theta) \leqslant \varphi \leqslant \varphi_2(\theta), r_1(\varphi, \theta) \leqslant r \leqslant r_2(\varphi, \theta),$$

则

$$\iiint_{\Omega} f(x, y, z) \mathrm{d}x \mathrm{d}y \mathrm{d}z$$

$$= \int_{\alpha}^{\beta} \mathrm{d}\theta \int_{\varphi_1(\theta)}^{\varphi_2(\theta)} \mathrm{d}\varphi \int_{r_1(\varphi, \theta)}^{r_2(\varphi, \theta)} f(r \sin \varphi \cos \theta, r \sin \varphi \sin \theta, r \cos \varphi) r^2 \sin \varphi \mathrm{d}r.$$

特殊地，若 $\Omega: x^2 + y^2 + z^2 \leqslant R^2$，则

$$\iiint_{\Omega} f(x, y, z) \mathrm{d}x \mathrm{d}y \mathrm{d}z = \int_0^{2\pi} \mathrm{d}\theta \int_0^{\pi} \mathrm{d}\varphi \int_0^{R} f(r \sin \varphi \cos \theta, r \sin \varphi \sin \theta, r \cos \varphi) r^2 \sin \varphi \mathrm{d}r.$$

若 $\Omega: x^2 + y^2 + z^2 \leqslant 2Rz$，则

$$\iiint_{\Omega} f(x, y, z) \mathrm{d}x \mathrm{d}y \mathrm{d}z = \int_0^{2\pi} \mathrm{d}\theta \int_0^{\pi} \mathrm{d}\varphi \int_0^{2R \cos \varphi} f(r \sin \varphi \cos \theta, r \sin \varphi \sin \theta, r \cos \varphi) r^2 \sin \varphi \mathrm{d}r.$$

337 中等题 计算三重积分 $\iiint_{\Omega} xyz \mathrm{d}x \mathrm{d}y \mathrm{d}z$，其中 $\Omega$ 为球面 $x^2 + y^2 + z^2 = 1$ 及 3 个坐标面围成的第一卦限内的闭区域.

338 中等题 计算三重积分 $\iiint_{\Omega} z^3 \mathrm{d}x \mathrm{d}y \mathrm{d}z$，其中 $\Omega$ 是由曲面 $x^2 + y^2 + z^2 \leqslant 2z$ 及 $z \geqslant \sqrt{x^2 + y^2}$ 围成的区域.

四、利用对称性计算三重积分

合理地利用对称性可以有效地简化三重积分的计算. 比如:

若 $\Omega$ 关于 $xOy$ 平面对称，$f(x, y, z)$ 关于 $z$ 是奇函数，则

$$\iiint_{\Omega} f(x, y, z) \mathrm{d}V = 0.$$

若 $\Omega$ 关于 $xOy$ 平面对称，$\Omega_1$ 为 $\Omega$ 在 $z > 0$ 时的部分，$f(x, y, z)$ 关于 $z$ 是偶函数，则

$$\iiint_{\Omega} f(x, y, z) \mathrm{d}V = 2 \iiint_{\Omega_1} f(x, y, z) \mathrm{d}V.$$

若 $\Omega$ 关于 $x, y$ 对称（即 $x, y$ 互换，$\Omega$ 不变），则

$$\iiint_{\Omega} f(x, y, z) \mathrm{d}V = \iiint_{\Omega} f(x, y, z) \mathrm{d}V.$$339 中等题 设空间闭区域 $\Omega_1 = \{(x,y,z)|x^2+y^2+z^2 \leq R^2,z \geq 0\}$,
$\Omega_2 = \{(x,y,z)|x^2+y^2+z^2 \leq R^2,x \geq 0,y \geq 0,z \geq 0\}$，则（    ）.

(A) $\iiint_{\Omega_1} x \mathrm{d}V = 4 \iiint_{\Omega_2} x \mathrm{d}V$
(B) $\iiint_{\Omega_1} y \mathrm{d}V = 4 \iiint_{\Omega_2} y \mathrm{d}V$
(C) $\iiint_{\Omega_1} z \mathrm{d}V = 4 \iiint_{\Omega_2} z \mathrm{d}V$
(D) $\iiint_{\Omega_1} xyz \mathrm{d}V = 4 \iiint_{\Omega_2} xyz \mathrm{d}V$

340 中等题 计算三重积分 $\iiint_{\Omega} \left( \frac{x^2}{a^2} + \frac{y^2}{b^2} + \frac{z^2}{c^2} \right) \mathrm{d}V$，其中 $\Omega$ 为区域 $x^2+y^2+z^2 \leq 1$.

341 中等题 计算三重积分 $\iiint_{\Omega} y^2 \mathrm{d}V$，其中 $\Omega$ 为区域 $x^2+y^2+z^2 \leq R^2$.

342 提高题 计算三重积分 $\iiint_{\Omega} (x+z) \mathrm{d}V$，其中 $\Omega$ 是由曲面 $z=\sqrt{x^2+y^2}$ 与 $z=\sqrt{1-x^2-y^2}$ 围成的区域.

343 提高题 设函数 $f(x)$ 连续且恒大于零，$F(t) = \frac{\iiint_{\Omega(t)} f(x^2+y^2+z^2) \mathrm{d}V}{\iiint_{D(t)} f(x^2+y^2) \mathrm{d}\sigma}$，其中 $\Omega(t) = \{(x,y,z)|x^2+y^2+z^2 \leq t^2\}$，$D(t) = \{(x,y)|x^2+y^2 \leq t^2\}$。讨论 $F(t)$ 在区间 $(0,+\infty)$ 内的单调性.

344 提高题 设函数 $f(x)$ 具有连续的导数，$f(0)=0$，区域 $\Omega$ 由平面 $z=0,z=1$ 和柱面 $x^2+y^2=t^2(t>0)$ 围成，求极限 $\lim_{t \to 0^+} \frac{1}{t^4} \iiint_{\Omega} f(x^2+y^2) \mathrm{d}V$ 的值.

第四节 重积分的应用

一、曲面的面积

设曲面 $S$ 由方程 $z=f(x,y)$ 给出，$D$ 为曲面 $S$ 在 $xOy$ 平面上的投影区域，函数 $z=f(x,y)$ 在 $D$ 上具有连续偏导数 $\frac{\partial z}{\partial x}, \frac{\partial z}{\partial y}$，则曲面 $S$ 的面积为若曲面的方程为 $x = g(y,z)$ 或 $y = h(z,x)$，则可分别把曲面投影到 $yOz$ 平面上（投影区域记为 $D_{yz}$）或 $zOx$ 平面上（投影区域记为 $D_{zx}$），类似地可得
$A = \iint_{D_{yz}} \sqrt{1 + \left(\frac{\partial z}{\partial x}\right)^2 + \left(\frac{\partial z}{\partial y}\right)^2} \mathrm{d}y \mathrm{d}z$ 或 $A = \iint_{D_{zx}} \sqrt{1 + \left(\frac{\partial y}{\partial x}\right)^2 + \left(\frac{\partial y}{\partial z}\right)^2} \mathrm{d}z \mathrm{d}x$.

345 中等题 求平面 $\frac{x}{a} + \frac{y}{b} + \frac{z}{c} = 1$ 被 3 个坐标面割出的有限部分的面积.

346 中等题 求球面 $x^2 + y^2 + z^2 = a^2$ 含在圆柱面 $x^2 + y^2 = ax$ 内部的面积.

347 中等题 求半径为 $R$ 的球的表面积.

二、质心

平面薄片的质心
设一平面薄片占有 $xOy$ 平面上的闭区域 $D$，在点 $(x,y)$ 处的面密度为 $\mu(x,y)$，假设 $\mu(x,y)$ 在 $D$ 上连续，则该薄片的质心的坐标为
$\bar{x} = \frac{M_y}{M} = \frac{\iint_D x \mu(x,y) \mathrm{d}\sigma}{\iint_D \mu(x,y) \mathrm{d}\sigma}$，$\bar{y} = \frac{M_x}{M} = \frac{\iint_D y \mu(x,y) \mathrm{d}\sigma}{\iint_D \mu(x,y) \mathrm{d}\sigma}$.

评注
(1) 如果薄片是均匀的，即面密度 $\mu(x,y) = \mu$ 为常量，那么其质心的坐标为
$\bar{x} = \frac{1}{S_D} \iint_D x \mathrm{d}\sigma$，$\bar{y} = \frac{1}{S_D} \iint_D y \mathrm{d}\sigma$.
(2) 均匀平面薄片的质心叫作该平面薄片所占平面图形的形心。因此，求平面图形 $D$ 的形心的坐标可用上述公式来计算.

空间立体的质心
设一物体占有空间有界闭区域 $\Omega$，在点 $(x,y,z)$ 处的密度为 $\rho(x,y,z)$，假设 $\rho(x,y,z)$ 在 $\Omega$ 上连续，则该物体的质心的坐标为$$\bar{x} = \frac{\iiint_{\Omega} x \rho(x,y,z) \mathrm{d}V}{\iiint_{\Omega} \rho(x,y,z) \mathrm{d}V}, \bar{y} = \frac{\iiint_{\Omega} y \rho(x,y,z) \mathrm{d}V}{\iiint_{\Omega} \rho(x,y,z) \mathrm{d}V}, \bar{z} = \frac{\iiint_{\Omega} z \rho(x,y,z) \mathrm{d}V}{\iiint_{\Omega} \rho(x,y,z) \mathrm{d}V}.$$

评注
类似地，可得均匀空间物体的形心的坐标为

$$\bar{x} = \frac{\iiint_{\Omega} x \mathrm{d}V}{\iiint_{\Omega} \mathrm{d}V}, \bar{y} = \frac{\iiint_{\Omega} y \mathrm{d}V}{\iiint_{\Omega} \mathrm{d}V}, \bar{z} = \frac{\iiint_{\Omega} z \mathrm{d}V}{\iiint_{\Omega} \mathrm{d}V}.$$

348 中等题 设平面薄片所占的闭区域 $D$ 由抛物线 $y=x^2$ 及直线 $y=x$ 围成，它在点 $(x,y)$ 处的面密度为 $\mu(x,y)=x^2y$，求该薄片的质心.

349 中等题 设球体 $x^2+y^2+z^2 \leqslant z$ 上任意点处的密度等于该点到原点的距离的平方，求此球体的质心的 $z$ 坐标.

350 中等题 设 $\Omega=\{(x,y,z)|x^2+y^2 \leqslant z \leqslant 1\}$，求 $\Omega$ 的形心的竖坐标 $\bar{z}$.

351 提高题 设 $\Omega$ 是由锥面 $x^2+(y-z)^2=(1-z)^2(0 \leqslant z \leqslant 1)$ 与平面 $z=0$ 围成的锥体，求 $\Omega$ 的形心坐标.

三、转动惯量

平面薄片的转动惯量
设一平面薄片占有 $xOy$ 平面上的闭区域 $D$，在点 $(x,y)$ 处的面密度为 $\mu(x,y)$，假设 $\mu(x,y)$ 在 $D$ 上连续，则该薄片对于 $x$ 轴的转动惯量 $I_x$ 及对于 $y$ 轴的转动惯量 $I_y$ 分别为
$$I_x = \iiint_D y^2 \mu(x,y) \mathrm{d}\sigma, I_y = \iiint_D x^2 \mu(x,y) \mathrm{d}\sigma.$$

空间立体的转动惯量
设一物体占有空间有界闭区域 $\Omega$，在点 $(x,y,z)$ 处的密度为 $\rho(x,y,z)$，假设 $\rho(x,y,z)$ 在 $\Omega$ 上连续，则该物体对于 $x$ 轴、$y$ 轴、$z$ 轴的转动惯量分别为
$$I_x = \iiint_{\Omega} (y^2+z^2) \rho(x,y,z) \mathrm{d}V,$$

## tool · 2026-10-19T15:18:37Z


Script completed
Wall time 0.1 seconds
Output:

058
1:318 中等题 计算二重积分 $\iint_D (x-y) \mathrm{d}x \mathrm{d}y$，其中积分区域
4:319 提高题 计算二重积分 $\iint_D (x+y^2) \mathrm{d}x \mathrm{d}y$，其中积分区域 $D = \{(x,y)|x^2+y^2 \leqslant x\}$.
6:320 中等题 设闭区域 $D = \{(x,y)|x^2+y^2 \leqslant y, x \geqslant 0\}$，$f(x,y)$ 为闭区域 $D$ 上的连
9:321 提高题 计算二重积分 $I = \iint_D \min \left\{ \sqrt{\frac{3}{16}-x^2-y^2}, 2(x^2+y^2) \right\} \mathrm{d}x \mathrm{d}y$，其中积分区
12:322 提高题 计算二重积分 $I = \iint_D |x y| \mathrm{d}x \mathrm{d}y$，其中积分区域
059
6:323 基础题 做适当的变换，计算二重积分 $\iint_D (x+y) \sin(x-y) \mathrm{d}x \mathrm{d}y$，其中
9:324 基础题 计算二重积分 $\iint_D \left( \frac{x^2}{a^2} + \frac{y^2}{b^2} \right) \mathrm{d}x \mathrm{d}y$，其中 $D = \left\{(x,y) \mid \frac{x^2}{a^2} + \frac{y^2}{b^2} \leq 1 \right\}.$
11:325 基础题 做适当的变换，计算二重积分 $\iint_D \mathrm{e}^{\frac{x}{x+y}} \mathrm{d}x \mathrm{d}y$，其中
14:326 基础题 设区域 $D$ 是由曲线 $xy = 4, xy = 8, xy^3 = 5, xy^3 = 15$ 围成的第一象限中的闭区域，求 $D$ 的面积.
16:327 中等题 证明 $\iint_D f(x+y) \mathrm{d}x \mathrm{d}y = \int_{-1}^{1} f(u) \mathrm{d}u$，其中闭区域 $D = \{(x,y) \parallel x| + |y| \leq 1\}$.
22:328 基础题 计算二重积分 $\iint_D x \mathrm{e}^{-y^2} \mathrm{d}x \mathrm{d}y$，其中 $D$ 是由曲线 $y = 4x^2$ 与 $y = 9x^2$ 在第一象限围成的无界区域.
24:329 中等题 计算二重积分 $\int_0^{+\infty} \mathrm{d}x \int_x^{\sqrt{3}x} \mathrm{e}^{-(x^2+y^2)} \mathrm{d}y$.
060
27:**331 中等题** 计算三重积分 $\iiint_\Omega xy^2 z^3 \mathrm{d}x \mathrm{d}y \mathrm{d}z$, 其中 $\Omega$ 是由曲面 $z = xy$ 及平面 $y=x,$ $x=1$ 和 $z=0$ 围成的闭区域.
29:**332 中等题** 计算三重积分 $\iiint_\Omega \frac{y \sin x}{x} \mathrm{d}x \mathrm{d}y \mathrm{d}z$, 其中 $\Omega$ 是由 $y=\sqrt{x}, y=0,z=0$ 和 $x+z=\frac{\pi}{2}$ 围成的闭区域.
31:**333 中等题** 计算三重积分 $\iiint_\Omega z^2 \mathrm{d}V$, 其中 $\Omega$ 由 $x^2+\frac{y^2}{4}+\frac{z^2}{9} \leqslant 1, 0 \leqslant z \leqslant 1$ 确定.
061
9:334 中等题 计算三重积分 $\iiint_{\Omega} z \mathrm{d} V$, 其中 $\Omega$ 是由曲面 $z = \sqrt{2 - x^2 - y^2}$ 和 $z = x^2 + y^2$ 围成的闭区域.
11:335 中等题 计算三重积分 $\iiint_{\Omega} (x^2 + y^2)^2 \mathrm{d} V$, 其中 $\Omega$ 是由 $z = x^2 + y^2, z = 1, z = 2$ 围成的闭区域.
13:336 中等题 计算三重积分 $\iiint_{\Omega} (x^2 + y^2 + z^2) \mathrm{d} V$, 其中 $\Omega$ 是由曲线 $\left\{ \begin{array}{l} x = 0 \\ y^2 = 2 z \end{array} \right.$ 绕 $z$ 轴旋转一周而成的曲面与平面 $z = 1$ 围成的区域.
062
19:337 中等题 计算三重积分 $\iiint_{\Omega} xyz \mathrm{d}x \mathrm{d}y \mathrm{d}z$，其中 $\Omega$ 为球面 $x^2 + y^2 + z^2 = 1$ 及 3 个坐标面围成的第一卦限内的闭区域.
21:338 中等题 计算三重积分 $\iiint_{\Omega} z^3 \mathrm{d}x \mathrm{d}y \mathrm{d}z$，其中 $\Omega$ 是由曲面 $x^2 + y^2 + z^2 \leqslant 2z$ 及 $z \geqslant \sqrt{x^2 + y^2}$ 围成的区域.
063
1:339 中等题 设空间闭区域 $\Omega_1 = \{(x,y,z)|x^2+y^2+z^2 \leq R^2,z \geq 0\}$,
9:340 中等题 计算三重积分 $\iiint_{\Omega} \left( \frac{x^2}{a^2} + \frac{y^2}{b^2} + \frac{z^2}{c^2} \right) \mathrm{d}V$，其中 $\Omega$ 为区域 $x^2+y^2+z^2 \leq 1$.
11:341 中等题 计算三重积分 $\iiint_{\Omega} y^2 \mathrm{d}V$，其中 $\Omega$ 为区域 $x^2+y^2+z^2 \leq R^2$.
13:342 提高题 计算三重积分 $\iiint_{\Omega} (x+z) \mathrm{d}V$，其中 $\Omega$ 是由曲面 $z=\sqrt{x^2+y^2}$ 与 $z=\sqrt{1-x^2-y^2}$ 围成的区域.
15:343 提高题 设函数 $f(x)$ 连续且恒大于零，$F(t) = \frac{\iiint_{\Omega(t)} f(x^2+y^2+z^2) \mathrm{d}V}{\iiint_{D(t)} f(x^2+y^2) \mathrm{d}\sigma}$，其中 $\Omega(t) = \{(x,y,z)|x^2+y^2+z^2 \leq t^2\}$，$D(t) = \{(x,y)|x^2+y^2 \leq t^2\}$。讨论 $F(t)$ 在区间 $(0,+\infty)$ 内的单调性.
17:344 提高题 设函数 $f(x)$ 具有连续的导数，$f(0)=0$，区域 $\Omega$ 由平面 $z=0,z=1$ 和柱面 $x^2+y^2=t^2(t>0)$ 围成，求极限 $\lim_{t \to 0^+} \frac{1}{t^4} \iiint_{\Omega} f(x^2+y^2) \mathrm{d}V$ 的值.
19:第四节 重积分的应用
064
4:345 中等题 求平面 $\frac{x}{a} + \frac{y}{b} + \frac{z}{c} = 1$ 被 3 个坐标面割出的有限部分的面积.
6:346 中等题 求球面 $x^2 + y^2 + z^2 = a^2$ 含在圆柱面 $x^2 + y^2 = ax$ 内部的面积.
8:347 中等题 求半径为 $R$ 的球的表面积.
065
8:348 中等题 设平面薄片所占的闭区域 $D$ 由抛物线 $y=x^2$ 及直线 $y=x$ 围成，它在点 $(x,y)$ 处的面密度为 $\mu(x,y)=x^2y$，求该薄片的质心.
10:349 中等题 设球体 $x^2+y^2+z^2 \leqslant z$ 上任意点处的密度等于该点到原点的距离的平方，求此球体的质心的 $z$ 坐标.
12:350 中等题 设 $\Omega=\{(x,y,z)|x^2+y^2 \leqslant z \leqslant 1\}$，求 $\Omega$ 的形心的竖坐标 $\bar{z}$.
14:351 提高题 设 $\Omega$ 是由锥面 $x^2+(y-z)^2=(1-z)^2(0 \leqslant z \leqslant 1)$ 与平面 $z=0$ 围成的锥体，求 $\Omega$ 的形心坐标.
068
1:第11章
4:第一节 对弧长的曲线积分
28:356 基础题 设 $L$ 为光滑曲线弧，其弧长为 $a$，$k$ 为常数，则 $\int_L k \mathrm{d}s =$ ____.
30:357 基础题 若 $\int_L f(x,y) \mathrm{d}s$ 存在，且在 $L$ 上 $f(x,y) \geq 0$，证明 $\int_L f(x,y) \mathrm{d}s \geq 0$.
32:358 基础题 若 $\int_L f(x,y) \mathrm{d}s$ 和 $\int_L g(x,y) \mathrm{d}s$ 都存在，且在 $L$ 上 $f(x,y) \geq g(x,y)$，则（ ）


## tool · 2026-10-19T15:18:46Z




## tool · 2026-10-19T15:20:16Z


Script completed
Wall time 3.1 seconds
Output:

\end{problem}

\begin{problem}{296}{50}{曲线间宽度与精确积分}
设 $0<a<1$，$D_a=\{(x,y):a\leq x\leq1,x^2\leq y\leq x\}$。求 $I(a)=\iint_{D_a}e^{x^2}\,\dd x\dd y$ 的一元积分表达式；在 $a=1/2$ 时将其化为含 $\int_{1/2}^1e^{x^2}\,\dd x$ 的表达式，并证明 $I'(a)<0$。允许保留所指定的非初等定积分。
\end{problem}

\begin{problem}{297}{50}{换序与线性分解}
将 $I=\int_0^1\dd x\int_x^1(y+xe^{y^2})\,\dd y$ 交换积分次序并计算。另求 $y$ 项与 $xe^{y^2}$ 项对积分的贡献，比较两项大小。
\end{problem}

\begin{problem}{298}{50}{参数上限与积分求导}
设 $a>0$，$I(a)=\int_0^a\dd x\int_x^a\frac{xy}{\sqrt{1+y^3}}\,\dd y$。交换次序求 $I(a)$，给出 $I(1)$；由积分表达式与所得公式分别求 $I'(a)$，检验两者一致。
\end{problem}

\begin{problem}{299}{50}{角点反常积分与换序}
设 $D=\{(x,y):1<x\leq2,0\leq y\leq\ln x\}$，定义
\[
 I=\lim_{\varepsilon\to0^+}\int_{1+\varepsilon}^2\dd x\int_0^{\ln x}\frac{e^{xy}}{x^x-1}\,\dd y.
\]
证明该极限存在并计算；写出形式上先对 $x$ 积分的表达式，指出角点 $(1,0)$ 使本题不能直接按连续函数的有界区域积分处理的原因。
\end{problem}

\begin{problem}{300}{50}{换序与分部积分}
设 $f\in C^3[0,2]$，$f(0)=f'(0)=f''(0)=-1$，$f(2)=-1/2$。计算
\[
 I=\int_0^2\dd x\int_0^x\sqrt{(2-x)(2-y)}f'''(y)\,\dd y.
\]
先将 $I$ 化为仅含端点值 $f(0),f'(0),f''(0),f(2)$ 的表达式；说明为什么未知的 $f'(2),f''(2)$ 不影响结果。
\end{problem}

\subsection{三重积分}

\begin{problem}{331}{55}{空间区域与幂函数积分}
设 $\Omega=\{(x,y,z):0\leq y\leq x\leq1,\ 0\leq z\leq xy\}$。
写出先对 $z$ 积分与先对 $y$ 积分的两种累次积分，计算
$\iiint_\Omega xy^2z^3\,\dd x\dd y\dd z$，并说明曲面 $z=xy$ 与 $z=0$ 如何确定区域的下边界 $y=0$。

{}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Chapter 10: 74 unique, ordered problem environments
Chapter 11: 10 unique, ordered problem environments


## tool · 2026-10-19T15:20:32Z


Script completed
Wall time 0.1 seconds
Output:

$I_y = \iiint_\Omega (z^2 + x^2) \rho(x, y, z) \mathrm{d}V,$
$I_z = \iiint_\Omega (x^2 + y^2) \rho(x, y, z) \mathrm{d}V.$

352 中等题 设一均匀平面薄片（面密度为常数 1）所占的闭区域为
$D = \left\{(x, y) \left| \frac{x^2}{a^2} + \frac{y^2}{b^2} \leq 1 \right. \right\}$，求该薄片对于 $y$ 轴的转动惯量.

353 提高题 设一均匀平面薄片（面密度为常数 $\mu$）所占的闭区域 $D$ 由抛物线
$y = x^2$ 及直线 $y = 1$ 围成，求该薄片对于直线 $y = -1$ 的转动惯量.

354 提高题 设一均匀物体（面密度为常数 $\rho$）所占的闭区域 $\Omega$ 由平面 $z = 0$，
$|x| = a, |y| = a$ 和曲面 $z = x^2 + y^2$ 围成，求该物体对于 $z$ 轴的转动惯量.

四、引力

平面薄片对薄片外一质点的引力
设一平面薄片占有 $xOy$ 平面上的闭区域 $D$，在点 $(x, y)$ 处的面密度为 $\mu(x, y)$，
假设 $\mu(x, y)$ 在 $D$ 上连续，则该薄片对于薄片外一点 $P_0(x_0, y_0)$ 处单位质量的质点的引力为
$F = \left(F_x, F_y\right) = \left(\iint_D \frac{G \mu(x, y)(x - x_0)}{r^3} \mathrm{d}\sigma, \iint_D \frac{G \mu(x, y)(y - y_0)}{r^3} \mathrm{d}\sigma\right)$，
其中，$G$ 为引力常数，$r = \sqrt{(x - x_0)^2 + (y - y_0)^2}$.

空间物体对物体外一质点的引力
设空间一物体占有空间有界闭区域 $\Omega$，在点 $(x, y, z)$ 处的密度为 $\rho(x, y, z)$，假设 $\rho(x, y, z)$ 在 $\Omega$ 上连续，则该物体对于物体外一点 $P_0(x_0, y_0, z_0)$ 处单位质量的质点的引力为
$F = \left(F_x, F_y, F_z\right)$
$= \left(\iint_\Omega \frac{G \rho(x, y, z)(x - x_0)}{r^3} \mathrm{d}V, \iint_\Omega \frac{G \rho(x, y, z)(y - y_0)}{r^3} \mathrm{d}V, \iint_\Omega \frac{G \rho(x, y, z)(z - z_0)}{r^3} \mathrm{d}V\right)$，其中, $G$ 为引力常数, $r = \sqrt{(x - x_0)^2 + (y - y_0)^2 + (z - z_0)^2}$.

355 提高题 设一均匀柱体（面密度为常数 1）所占的闭区域为
$\Omega = \{(x, y, z) | x^2 + y^2 \leq R^2, 0 \leq z \leq h\}$, 求它对于点 $M_0(0, 0, a) (a > h)$ 处单位
质量的质点的引力.设 $\alpha>0$。证明并计算
$I(\alpha)=\int_0^{+\infty}\dd x\int_x^{\sqrt3x}e^{-\alpha(x^2+y^2)}\,\dd y$，给出 $I(1)$；利用平面缩放独立说明 $I(\alpha)$ 与 $\alpha$ 的关系。
\end{problem}

\subsection{三重积分}

\begin{problem}{331}{55}{空间区域与幂函数积分}
设 $\Omega=\{(x,y,z):0\leq y\leq x\leq1,\ 0\leq z\leq xy\}$。
写出先对 $z$ 积分与先对 $y$ 积分的两种累次积分，计算
$\iiint_\Omega xy^2z^3\,\dd x\dd y\dd z$，并说明曲面 $z=xy$ 与 $z=0$ 如何确定区域的下边界 $y=0$。
\end{problem}

\begin{problem}{332}{55}{三重积分的次序选择}
设 $\Omega=\{(x,y,z):0\leq x\leq\pi/2,\ 0\leq y\leq\sqrt{x},\ 0\leq z\leq\pi/2-x\}$。
将 $\sin x/x$ 在 $x=0$ 处作连续延拓，计算
\[
 \iiint_\Omega\frac{y\sin x}{x}\,\dd x\dd y\dd z,
\]
并解释先对 $y,z$ 积分为何能消去分母 $x$ 带来的计算困难。
\end{problem}

\begin{problem}{333}{55}{椭球截面与参数积分}
设 $0<h\leq3$，$\Omega_h=\{(x,y,z):x^2+y^2/4+z^2/9\leq1,\ 0\leq z\leq h\}$。
用水平截面法求 $J(h)=\iiint_{\Omega_h}z^2\,\dd V$，求 $J(1)$，并说明 $J'(h)$ 的几何意义。
\end{problem}


## tool · 2026-10-19T15:21:31Z


Script completed
Wall time 3.1 seconds
Output:

{}
\end{problem}

\begin{problem}{350}{60}{抛物体截面的形心}
设 $H>0$，$\Omega_H=\{(x,y,z):x^2+y^2\leq z\leq H\}$。求其体积与全部形心坐标，给出 $H=1$ 的结果；解释形心高度为何不能直接取上下端高度的算术平均值。
\end{problem}

\begin{problem}{351}{60}{斜圆锥的截面与形心}
设 $\Omega=\{(x,y,z):0\leq z\leq1,x^2+(y-z)^2\leq(1-z)^2\}$ 为均匀锥体。求水平截面的面积及圆心，利用截面法求全部形心坐标，并证明形心位于底面圆心与顶点的连线上。
\end{problem}

\begin{problem}{352}{61}{椭圆薄片的惯量}
设 $a,b>0$，$D=\{x^2/a^2+y^2/b^2\leq1\}$，面密度为 $1$。求薄片关于 $y$ 轴、$x$ 轴的转动惯量与关于原点的极惯量；比较前两者并给出相等的充要条件。
\end{problem}

\begin{problem}{353}{61}{平行直线的惯量最小值}
设 $D=\{(x,y):-1\leq x\leq1,x^2\leq y\leq1\}$，面密度为常数 $\mu>0$。求关于直线 $y=c$ 的转动惯量 $I(c)$，给出 $c=-1$ 的结果，并求使 $I(c)$ 最小的 $c$，说明其与质心的关系。
\end{problem}

\begin{problem}{354}{61}{抛物面下立体的轴惯量}
设 $a,\rho>0$，$\Omega=\{(x,y,z):|x|\leq a,|y|\leq a,0\leq z\leq x^2+y^2\}$，体密度为 $\rho$。求质量及关于 $z$ 轴的转动惯量，给出惯量与质量之比，并检验其量纲。
\end{problem}

\begin{problem}{355}{62}{圆柱体的轴向引力}
设 $R,h>0$，均匀圆柱体 $\Omega=\{x^2+y^2\leq R^2,0\leq z\leq h\}$ 的体密度为 $1$，引力常数为 $G$。求其对 $M_0(0,0,a)$（$a>h$）处单位质量质点的引力向量；先用对称性确定方向，再计算非零分量，并检验 $a\to+\infty$ 时引力大小与 $G\pi R^2h/a^2$ 的比值。
\end{problem}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Chapter 10: 96 unique, ordered problem environments
Chapter 11: 10 unique, ordered problem environments


## tool · 2026-10-19T15:21:36Z


Script completed
Wall time 0.1 seconds
Output:

(4) 若区域 $D$ 关于直线 $y=x$ 对称，则
$$\iint_D f(x,y) \mathrm{d}\sigma = \iint_D f(y,x) \mathrm{d}\sigma = \frac{1}{2} \left[ \iint_D f(x,y) \mathrm{d}\sigma + \iint_D f(y,x) \mathrm{d}\sigma \right]$$

评注
利用二重积分的对称性质可以有效减少计算量，但要注意的是，当被积函数的奇偶性及积分区域 $D$ 的对称性两者兼得时，我们才可以使用二重积分的对称性质.

259 基础题 比较积分 $\iint_D \ln(x+y) \mathrm{d}\sigma$ 与 $\iint_D [\ln(x+y)]^2 \mathrm{d}\sigma$ 的大小，其中积分区域 $D$ 是三角形闭区域，3 个顶点分别为 $(1,0),(1,1),(0,1)$.

260 基础题 比较积分 $I_1 = \iint_D \frac{x+y}{4} \mathrm{d}\sigma, I_2 = \iint_D \sqrt{\frac{x+y}{4}} \mathrm{d}\sigma, I_3 = \iint_D \sqrt[3]{\frac{x+y}{4}} \mathrm{d}\sigma$ 的大小，其中积分区域 $D$ 是由 $(x-1)^2 + (y-1)^2 \leqslant 2$ 围成的闭区域.

261 基础题 估计二重积分 $I = \iint_D \sin^2 x \sin^2 y \mathrm{d}\sigma$ 的值，其中积分区域 $D = \{(x,y) | 0 \leqslant x \leqslant \pi, 0 \leqslant y \leqslant \pi\}$.272 基础题 已知 $I = \int_{0}^{1} \mathrm{d}y \int_{-\sqrt{1-y^2}}^{\sqrt{1-y^2}} f(x,y) \mathrm{d}x$ ，交换其积分次序.

273 基础题 已知 $I = \int_{0}^{1} \mathrm{d}x \int_{-\sqrt{x}}^{\sqrt{x}} f(x,y) \mathrm{d}y + \int_{1}^{4} \mathrm{d}x \int_{x-2}^{\sqrt{x}} f(x,y) \mathrm{d}y$ ，交换其积分次序.

274 基础题 已知 $I = \int_{0}^{1} \mathrm{d}y \int_{0}^{2y} f(x,y) \mathrm{d}x + \int_{1}^{3} \mathrm{d}y \int_{0}^{3-y} f(x,y) \mathrm{d}x$ ，交换其积分次序.

275 基础题 已知 $I = \int_{0}^{\pi} \mathrm{d}x \int_{-\sin \frac{x}{2}}^{\sin x} f(x,y) \mathrm{d}y$ ，交换其积分次序.

276 基础题 已知 $I = \int_{1}^{2} \mathrm{d}y \int_{y}^{y^2} f(x,y) \mathrm{d}x$ ，交换其积分次序.

277 基础题 已知 $I = \int_{1}^{2} \mathrm{d}x \int_{x}^{x^2} f(x,y) \mathrm{d}y + \int_{2}^{8} \mathrm{d}x \int_{x}^{8} f(x,y) \mathrm{d}y$ ，交换其积分次序.

278 中等题 设 $f(x)$ 为连续函数， $F(t) = \int_{1}^{t} \mathrm{d}y \int_{y}^{t} f(x) \mathrm{d}x$ ，求 $F'(3)$.
\begin{problem}{275}{47}{三角函数边界的换序}
设 $f$ 在 $D=\{(x,y):0\leq x\leq\pi,-\sin(x/2)\leq y\leq\sin x\}$ 上连续。
将 $\iint_Df\,\dd x\dd y$ 改为先对 $x$ 积分的表达式，写明必须分段的纵坐标，并求 $D$ 的面积。
\end{problem}

\begin{problem}{276}{47}{不同次序积分的区域辨析}
设 $f$ 连续，记
\[
 I=\int_1^2\dd y\int_y^{y^2}f(x,y)\,\dd x
 +\int_2^8\dd x\int_x^8f(x,y)\,\dd y.
\]
分别用不等式描述两项对应的区域，判断其内部是否相交；将 $I$ 全部改为先对 $x$ 积分，并计算 $f\equiv1$ 时的值。
\end{problem}

\begin{problem}{277}{47}{变限二重积分求导}
设 $f$ 在 $[1,+\infty)$ 上连续，$F(t)=\int_1^t\dd y\int_y^t f(x)\,\dd x$，$t\geq1$。
先交换积分次序，再求 $F'(t)$ 与 $F'(3)$；若 $f$ 处处为正，判断 $F$ 在 $(1,+\infty)$ 上的单调性并说明理由。
\end{problem}

\begin{problem}{279}{48}{矩形域与参数变化}
设 $a,b>0$，$D_{a,b}=[0,a]\times[0,b]$。求 $I(a,b)=\iint_{D_{a,b}}e^{x-y}\,\dd x\dd y$，给出 $I(1,1)$，并判断固定 $a$ 时 $I(a,b)$ 随 $b$ 的变化及其极限。
\end{problem}

\begin{problem}{280}{49}{区域分割与积分份额}
设 $D=[0,1]^2$，以直线 $x+y=1$ 分割为 $D_-=\{(x,y)\in D:x+y\leq1\}$ 与 $D_+=D\setminus D_-$。计算 $x+y$ 在 $D,D_-,D_+$ 上的积分，并判断两个等面积部分的积分是否相等。
\end{problem}



## tool · 2026-10-19T15:21:59Z


Script completed
Wall time 0.2 seconds
Output:

{}
37:\begin{problem}{260}{45}{幂函数比较与严格性}
142:\begin{problem}{276}{47}{抛物线区域的分段换序}
147:\begin{problem}{277}{47}{分块区域的重新组合}
156:\begin{problem}{278}{47}{变限二重积分求导}
cat: .agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/060-crop0.0-0.3.md: No such file or directory


## tool · 2026-10-19T15:22:31Z


Script completed
Wall time 1.4 seconds
Output:

设 $D=\{(x,y):0\leq y\leq2,1\leq x\leq y+1\}$。将 $\iint_D\cos(y^2)\,\dd x\dd y$ 写成两种次序的累次积分，选取能直接计算的次序求值，并说明为何无须求 $\cos(y^2)$ 的初等原函数。
\end{problem}

\begin{problem}{293}{50}{可去奇点与曲边区域}
令 $f(x)=\sin x/x$（$x\ne0$），$f(0)=1$。设 $D$ 由 $y=x,y=x^2$ 围成。计算 $\iint_Df(x)\,\dd x\dd y$，并证明在整个 $D$ 上被积函数连续；若仅改变原点处的取值，积分是否改变？
\end{problem}

\begin{problem}{294}{50}{三角形域与符号估计}
设 $D=\{(x,y):0\leq x\leq y\leq1\}$。求 $I=\iint_D(e^{-y^2}-1)\,\dd x\dd y$；不依赖准确结果，直接利用被积函数证明 $-1/2<I<0$，再检验所求值。
\end{problem}

\begin{problem}{295}{50}{密度积分与高斯型因子}
设 $D=\{(x,y):0\leq x\leq y\leq1\}$。求 $\iint_Dx^2e^{-y^2}\,\dd x\dd y$；若薄片密度为 $e^{-y^2}$，再求其关于 $y$ 轴的转动惯量与质量之比。
\end{problem}

\begin{problem}{296}{50}{曲线间宽度与精确积分}
设 $0<a<1$，$D_a=\{(x,y):a\leq x\leq1,x^2\leq y\leq x\}$。求 $I(a)=\iint_{D_a}e^{x^2}\,\dd x\dd y$ 的一元积分表达式；在 $a=1/2$ 时将其化为含 $\int_{1/2}^1e^{x^2}\,\dd x$ 的表达式，并证明 $I'(a)<0$。允许保留所指定的非初等定积分。
\end{problem}

\begin{problem}{297}{50}{换序与线性分解}
将 $I=\int_0^1\dd x\int_x^1(y+xe^{y^2})\,\dd y$ 交换积分次序并计算。另求 $y$ 项与 $xe^{y^2}$ 项对积分的贡献，比较两项大小。
\end{problem}

\begin{problem}{298}{50}{参数上限与积分求导}
设 $a>0$，$I(a)=\int_0^a\dd x\int_x^a\frac{x}{\sqrt{1+y^3}}\,\dd y$。交换次序求 $I(a)$，给出 $I(1)$；由积分表达式与所得公式分别求 $I'(a)$，检验两者一致。
\end{problem}

\begin{problem}{299}{50}{角点反常积分与换序}
设 $D=\{(x,y):1<x\leq2,0\leq y\leq\ln x\}$，定义
\[
 I=\lim_{\varepsilon\to0^+}\int_{1+\varepsilon}^2\dd x\int_0^{\ln x}\frac{e^{xy}}{x^x-1}\,\dd y.
\]
证明该极限存在并计算；写出形式上先对 $x$ 积分的表达式，指出角点 $(1,0)$ 使本题不能直接按连续函数的有界区域积分处理的原因。
\end{problem}

\begin{problem}{300}{50}{换序与分部积分}
from pathlib import Path
import re
import sympy as s

x, y, z, h, t = s.symbols('x y z h t', real=True)

def same(actual, expected):
    assert s.simplify(actual - expected) == 0, (actual, expected)

same(s.integrate(s.integrate(x*y, (y, 0, x)), (x, 0, 1)), s.Rational(1, 8))
same(s.integrate(y+2-y*y, (y, -1, 2)), s.Rational(9, 2))
area274 = s.integrate(2*y, (y, 0, 1)) + s.integrate(3-y, (y, 1, 3))
moment274 = s.integrate(2*y*y, (y, 0, 1)) + s.integrate(y*(3-y), (y, 1, 3))
same(area274, 3)
same(moment274 / area274, s.Rational(4, 3))
same(s.integrate(y*y-y, (y, 1, 2)) + s.integrate(8-x, (x, 2, 8)), s.Rational(113, 6))
same(s.integrate(s.integrate(s.integrate(x*y*y*z**3, (z, 0, x*y)), (y, 0, x)), (x, 0, 1)), s.Rational(1, 364))
same(s.integrate((s.pi/2-x)*s.sin(x)/2, (x, 0, s.pi/2)), s.pi/4-s.Rational(1, 2))
j333 = s.integrate(2*s.pi*z*z*(1-z*z/9), (z, 0, h))
same(j333.subs(h, 1), 28*s.pi/45)
same(s.diff(j333, h), 2*s.pi*h*h*(1-h*h/9))
mass381 = 1 + s.integrate(1/(1+y), (y, 0, 1)) + s.sqrt(2)*s.integrate(1/(1+y), (y, 0, 1))
moment381 = s.Rational(1, 2) + s.sqrt(2)*s.integrate((1-y)/(1+y), (y, 0, 1))
same(mass381, 1+(1+s.sqrt(2))*s.log(2))
same(moment381, s.Rational(1, 2)+s.sqrt(2)*(2*s.log(2)-1))
same(s.integrate((1+4*x*x)/(x*x+3*x*x+1), (x, 1, 0)), -1)
print('Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406')

for chapter in (10, 11):
    path = Path(f'output/宋浩下册工科数学分析改编/chapters/ch{chapter}.tex')
    text = path.read_text()
    numbers = [int(number) for number in re.findall(r'\\begin\{problem\}\{(\d+)\}', text)]
    assert numbers == sorted(set(numbers)), (chapter, numbers)
    assert text.count(r'\begin{problem}') == text.count(r'\end{problem}')
    print(f'Chapter {chapter}: {len(numbers)} unique, ordered problem environments')

{}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Traceback (most recent call last):
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 37, in <module>
    same(max304, 4-c*c/4+c*c*s.log(4/c)/2)
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 8, in same
    assert s.simplify(actual - expected) == 0, (actual, expected)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AssertionError: (-c**2*log(c/2)/2 + c**2*log(2)/2 + 3*c**2/4 + 4, c**2*log(4/c)/2 - c**2/4 + 4)


## tool · 2026-10-19T15:22:39Z


Script completed
Wall time 2.2 seconds
Output:

same(s.integrate((1+4*x*x)/(x*x+3*x*x+1), (x, 1, 0)), -1)
print('Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406')

a, c = s.symbols('a c', positive=True)
same(s.integrate(s.integrate(x*x+y*y-x, (x, y/2, y)), (y, 0, a)), a**3*(19*a-12)/96)
same(s.integrate(y*y*y*s.exp(y*y)/2, (y, 0, 1)), s.Rational(1, 4))
same(s.integrate(y*y/(2*s.sqrt(1+y**3)), (y, 0, a)), (s.sqrt(1+a**3)-1)/3)
same(s.integrate(1/s.Symbol('u', positive=True), (s.Symbol('u', positive=True), 1, 2)), s.log(2))
same(s.integrate(s.Rational(1, 2)-c*x*x+c*c*x**4, (x, -1, 1)), 1-2*c/3+2*c*c/5)
max304 = s.integrate(2*c, (x, 0, c/2)) + s.integrate(c*c/(2*x)+2*x, (x, c/2, 2))
same(max304, 4-c*c/4+c*c*s.log(4/c)/2)
same(s.integrate(16*(x+y)*x*y, (y, 0, 1-x), (x, 0, 1)), s.Rational(8, 15))
same(s.integrate(16*x*y, (y, 0, 1-x), (x, 0, 1)), s.Rational(2, 3))
r = s.symbols('r', nonnegative=True)
split321 = s.Rational(1, 4)
same(s.sqrt(s.Rational(3, 16)-split321**2), 2*split321**2)
u, v = s.symbols('u v', positive=True)
xx, yy = u**s.Rational(3, 2)/s.sqrt(v), s.sqrt(v/u)
jac326 = s.det(s.Matrix([[s.diff(xx,u),s.diff(xx,v)],[s.diff(yy,u),s.diff(yy,v)]]))
same(jac326, 1/(2*v))
mass348 = s.integrate(x*x*y, (y,x*x,x), (x,0,1))
x348 = s.integrate(x**3*y, (y,x*x,x), (x,0,1))/mass348
same(x348, s.Rational(35,48))
mass349 = 2*s.pi*s.integrate(s.sin(t)*s.cos(t)**5/5,(t,0,s.pi/2))
moment349 = 2*s.pi*s.integrate(s.sin(t)*s.cos(t)**7/6,(t,0,s.pi/2))
same(moment349/mass349, s.Rational(5,8))
print('Additional checks passed: 289, 297, 298, 299, 303, 304, 306, 321, 326, 348, 349')

for chapter in (10, 11):

{}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Traceback (most recent call last):
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 42, in <module>
    same(s.sqrt(s.Rational(3, 16)-split321**2), 2*split321**2)
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 8, in same
    assert s.simplify(actual - expected) == 0, (actual, expected)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AssertionError: (sqrt(2)/4, 1/8)


## tool · 2026-10-19T15:22:51Z


Script completed
Wall time 2.1 seconds
Output:

same(s.integrate(s.Rational(1, 2)-c*x*x+c*c*x**4, (x, -1, 1)), 1-2*c/3+2*c*c/5)
max304 = s.integrate(2*c, (x, 0, c/2)) + s.integrate(c*c/(2*x)+2*x, (x, c/2, 2))
same(max304, 4+3*c*c/4+c*c*s.log(4/c)/2)
same(s.integrate(16*(x+y)*x*y, (y, 0, 1-x), (x, 0, 1)), s.Rational(8, 15))
same(s.integrate(16*x*y, (y, 0, 1-x), (x, 0, 1)), s.Rational(2, 3))
r = s.symbols('r', nonnegative=True)
split321 = s.Rational(1, 4)
same(s.sqrt(s.Rational(3, 16)-split321**2), 2*split321**2)
u, v = s.symbols('u v', positive=True)
xx, yy = u**s.Rational(3, 2)/s.sqrt(v), s.sqrt(v/u)
jac326 = s.det(s.Matrix([[s.diff(xx,u),s.diff(xx,v)],[s.diff(yy,u),s.diff(yy,v)]]))
same(jac326, 1/(2*v))
mass348 = s.integrate(x*x*y, (y,x*x,x), (x,0,1))
x348 = s.integrate(x**3*y, (y,x*x,x), (x,0,1))/mass348

{}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Additional checks passed: 289, 297, 298, 299, 303, 304, 306, 321, 326, 348, 349
Chapter 10: 98 unique, ordered problem environments
Chapter 11: 10 unique, ordered problem environments


## tool · 2026-10-19T15:22:56Z




## tool · 2026-10-19T15:23:01Z


Script completed
Wall time 0.1 seconds
Output:

.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/054.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/055.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/056.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/057-crop0.45-1.0.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/057.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/058.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/059-crop0.45-1.0.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/059.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/060.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/061.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/062.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/063.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/064.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/065.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/066.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/067.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/068.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/073.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/077.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/090.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/091.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/092.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/093.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/094.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/095.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/096.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/097.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/098.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/099.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/100.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/110-crop0.45-1.0.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/110.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/113.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/117-crop0.45-1.0.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/117.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/120.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/123.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/125.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/127.md
.agent/hdu-ocr/local/宋浩高等数学精选750题下册 (宋浩)/129.md


## tool · 2026-10-19T15:23:20Z




## user · 2026-10-19T23:46:30Z

<environment_context>
  <current_date>2026-10-20</current_date>
  <timezone>Asia/Shanghai</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/Agent/Codex</root><root>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/Agent/Codex</path></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## tool · 2026-10-19T23:46:35Z


Script completed
Wall time 0.1 seconds
Output:

359 中等题 若函数 $f(x,y,z)$ 在空间光滑曲线弧 $L$ 上连续，证明
$$\left|\int_{L} f(x,y,z) \mathrm{d}s\right| \leqslant \int_{L} \left|f(x,y,z)\right| \mathrm{d}s.$$

二、对弧长的曲线积分的性质

性质 1 (线性性质)：设 $a, b$ 为常数，则
$$\int_{L} \left[ a f(x,y) + b g(x,y) \right] \mathrm{d}s = a \int_{L} f(x,y) \mathrm{d}s + b \int_{L} g(x,y) \mathrm{d}s.$$

性质 2 (积分弧段的可加性)：若积分弧段 $L$ 可分成两段光滑的曲线弧 $L_{1}$ 和 $L_{2}$，即 $L = L_{1} + L_{2}$，则
$$\int_{L} f(x,y) \mathrm{d}s = \int_{L_{1}} f(x,y) \mathrm{d}s + \int_{L_{2}} f(x,y) \mathrm{d}s.$$

性质 3：若积分弧段 $L$ 的弧长为 $s$，$k$ 为常数，则
$$\int_{L} 1 \mathrm{d}s = \int_{L} \mathrm{d}s = s, \int_{L} k \mathrm{d}s = ks.$$

性质 4：对弧长的曲线积分与积分弧段的方向无关，即
$$\int_{\overrightarrow{AB}} f(x,y) \mathrm{d}s = \int_{\overrightarrow{EA}} f(x,y) \mathrm{d}s.$$

性质 5 (比较性质)：若在 $L$ 上 $f(x,y) \leqslant g(x,y)$，则
$$\int_{L} f(x,y) \mathrm{d}s \leqslant \int_{L} g(x,y) \mathrm{d}s.$$

特别地，有
$$\left|\int_{L} f(x,y) \mathrm{d}s\right| \leqslant \int_{L} \left|f(x,y)\right| \mathrm{d}s.$$

性质 6 (保号性)：若在 $L$ 上 $f(x,y) \geqslant 0$，则 $\int_{L} f(x,y) \mathrm{d}s \geqslant 0$；若在 $L$ 上 $f(x,y) \leqslant 0$，则 $\int_{L} f(x,y) \mathrm{d}s \leqslant 0.$

性质 7 (对称性)：对弧长的曲线积分，关于积分弧段的对称性和被积函数的奇偶性有如下结论.

(1) 若积分弧段 $L$ 关于 $x$ 轴对称，被积函数 $f(x,y)$ 关于 $y$ 具有奇偶性，则
$$\int_{L} f(x,y) \mathrm{d}s = \begin{cases} 2 \int_{L_{1}} f(x,y) \mathrm{d}s, & f(x,y) \text{关于 } y \text{为偶函数} \\ 0, & f(x,y) \text{关于 } y \text{为奇函数} \end{cases}$$
其中 $L_{1}$ 为 $L$ 在 $x$ 轴上方的部分.

(2) 若积分弧段 $L$ 关于 $y$ 轴对称，被积函数 $f(x,y)$ 关于 $x$ 具有奇偶性，则
$$\int_{L} f(x,y) \mathrm{d}s = \begin{cases} 2 \int_{L_{1}} f(x,y) \mathrm{d}s, & f(x,y) \text{关于 } x \text{为偶函数} \\ 0, & f(x,y) \text{关于 } x \text{为奇函数} \end{cases}$$
其中 $L_{1}$ 为 $L$ 在 $y$ 轴右方的部分.

(3) 若积分弧段 $L$ 关于直线 $y=x$ 对称，则
$$\int_{L} f(x,y) \mathrm{d}s = \int_{L} f(y,x) \mathrm{d}s.$$对空间弧长的曲线积分也有类似的上述性质.
类似于性质 7 的 (3), 对空间弧长的曲线积分具有如下的轮换对称性.
在空间曲线弧段 $L$ 的方程中依次将 $\begin{cases} x$ 换为 $y \\ y$ 换为 $z$, 若轮换之后 $L$ 的方程保持不变, 则在被积函数中依次将 $\begin{cases} x$ 换为 $y \\ y$ 换为 $z$, 轮换之后对弧长的曲线积分值也不变, 即 $z$ 换为 $x$
$$\int_{L} f(x,y,z) \mathrm{d}s = \int_{L} f(y,z,x) \mathrm{d}s = \int_{L} f(z,x,y) \mathrm{d}s.$$

360 基础题 设平面曲线 $L$ 为下半圆周 $y = -\sqrt{4-x^2}$, 则曲线积分
$$\int_{L} \sqrt{x^2+y^2} \mathrm{d}s =$$ ____.

361 基础题 设平面曲线 $L$ 为连接 $(-1,0)$ 及 $(0,2)$ 两点的直线段, 则曲线积分
$$\int_{L} (2x-y+5) \mathrm{d}s =$$ ____.

362 基础题 设 $L$ 为圆柱面 $x^2+y^2=4$ 与平面 $z=2$ 的交线, 则
$$\oint_{L} \arctan \frac{z^2}{x^2+y^2} \mathrm{d}s =$$ ____.

363 基础题 求 $\oint_{\Gamma} z^2 \mathrm{d}s$, 其中 $\Gamma$ 为球面 $x^2+y^2+z^2=9$ 与平面 $x+y+z=0$ 相交的圆周.

364 中等题 设 $L$ 为椭圆 $\frac{x^2}{4}+\frac{y^2}{3}=1$, 其周长为 $a$, 则 $\oint_{L} (2xy+3x^2+4y^2) \mathrm{d}s =$$ ____.

365 中等题 设 $I_1 = \int_{L_1} (xy^2-|x|+2y) \mathrm{d}s, I_2 = \int_{L_2} x \mathrm{d}s$, 其中积分曲线弧段 $L_1: y=|x|$ $(-1 \leqslant x \leqslant 1), L_2: y=x (0 \leqslant x \leqslant 1)$, 则 (    ).
(A) $I_1=2I_2$ (B) $I_1=4I_2$ (C) $I_2=2I_1$ (D) $I_2=4I_1$

366 中等题 设平面曲线 $L$ 为连接 $(1,0)$ 及 $(0,1)$ 两点的直线段, $I = \int_{L} x^2 \mathrm{d}s,$
$J = \int_{L} (x-y) \mathrm{d}s, K = \int_{L} \frac{x+y}{2} \mathrm{d}s$, 则 (    ).
(A) $I < J < K$ (B) $I < K < J$ (C) $J < I < K$ (D) $K < J < I$367 中等题 设曲线 $L: x^2 + xy + y^2 = R^2$ 的长度为 $a$, 求 $I = \oint_L \frac{2\sin e^x - 3\sin e^y}{\sin e^x + \sin e^y} \mathrm{d}s$.

368 中等题 设 $L$ 为球面 $x^2 + y^2 + z^2 = 1$ 与平面 $x + y + z = 0$ 的交线, 求
$I = \oint_L (xy + z) \mathrm{d}s$.

三、对弧长的曲线积分的计算

积分曲线为平面曲线
(1) 积分曲线用参数方程表示
若积分曲线 $L$ 的参数方程为 $\begin{cases} x = \varphi(t) \\ y = \psi(t) \end{cases}$, $\alpha \leq t \leq \beta$, 则
$$\int_L f(x, y) \mathrm{d}s = \int_a^\beta f[\varphi(t), \psi(t)] \sqrt{\varphi'^2(t) + \psi'^2(t)} \mathrm{d}t.$$
(2) 积分曲线用直角坐标方程表示
若积分曲线 $L$ 的方程为 $y = \varphi(x)$, $a \leq x \leq b$, 则
$$\int_L f(x, y) \mathrm{d}s = \int_a^b f[x, \varphi(x)] \sqrt{1 + \varphi'^2(x)} \mathrm{d}x.$$
若积分曲线 $L$ 的方程为 $x = \psi(y)$, $c \leq y \leq d$, 则
$$\int_L f(x, y) \mathrm{d}s = \int_c^d f[\psi(y), y] \sqrt{1 + \psi'^2(y)} \mathrm{d}y.$$
(3) 积分曲线用极坐标方程表示
若积分曲线 $L$ 的方程为 $\rho = \rho(\theta)$, $\alpha \leq \theta \leq \beta$, 此时可将其化为参数方程
则
$$\int_L f(x, y) \mathrm{d}s = \int_a^\beta f[\rho(\theta) \cos \theta, \rho(\theta) \sin \theta] \sqrt{\rho^2(\theta) + \rho'^2(\theta)} \mathrm{d}\theta.$$
积分曲线为空间曲线
若积分曲线 $L$ 为空间曲线, 其参数方程为 $\begin{cases} x = \varphi(t) \\ y = \psi(t) \\ z = \omega(t) \end{cases}$, 则
$$\int_L f(x, y, z) \mathrm{d}s = \int_a^\beta f[\varphi(t), \psi(t), \omega(t)] \sqrt{\varphi'^2(t) + \psi'^2(t) + \omega'^2(t)} \mathrm{d}t.$$

评注
(1) 对弧长的曲线积分与积分曲线的方向无关.
(2) 将对弧长的曲线积分转化为定积分时, 积分下限一定小于积分上限.
(3) 对于积分曲线 $L$ 的不同方程形式, 牢记弧微分 $\mathrm{d}s$ 的转化公式.369 基础题 已知曲线 $L: y = \mathrm{e}^{x} (0 \leqslant x \leqslant 1)$，则 $\int_{L} \sqrt{1 + y^{2}} \mathrm{d}s =$ ____.

370 基础题 已知曲线 $L: y^{2} = 2x (0 \leqslant y \leqslant \sqrt{3})$，则 $\int_{L} y \mathrm{d}s =$ ____.

371 基础题 计算 $\int_{L} \frac{x + y}{\sqrt{x^{2} + y^{2}}} \mathrm{d}s$，其中 $L$ 为双曲线 $xy = 1$ 上从点 $\left(\frac{1}{2}, 2\right)$ 到点 $(1, 1)$ 的弧段.

372 基础题 计算 $\int_{L} xy \mathrm{d}s$，其中 $L$ 为曲线 $x = a (1 + \cos t), y = a \sin t (a > 0)$ 上 $t$ 从 0 变到 $\frac{\pi}{2}$ 的这段弧.

373 基础题 计算曲线积分 $\oint_{L} (x + y) \mathrm{d}s$，其中圆周 $L$ 的极坐标方程为 $\rho = \cos \theta + \sin \theta \left(-\frac{\pi}{4} \leqslant \theta \leqslant \frac{3\pi}{4}\right)$.

374 基础题 设 $\Gamma$ 为曲线 $x = \mathrm{e}^{t} \cos t, y = \mathrm{e}^{t} \sin t, z = \mathrm{e}^{t}$ 上 $t$ 从 0 变到 2 的一段弧，计算曲线积分 $\int_{\Gamma} \frac{1}{x^{2} + y^{2} + z^{2}} \mathrm{d}s$.

375 基础题 计算 $\int_{L} \frac{\mathrm{e}^{y}}{1 + x^{2}} \mathrm{d}s$，其中 $L$ 为曲线 $y = \ln x$ 上点 $(1, 0)$ 与点 $\left(\sqrt{3}, \frac{\ln 3}{2}\right)$ 之间的一段弧.

376 基础题 计算 $\int_{L} \sqrt{1 + 3y^{2}} \mathrm{d}s$，其中 $L$ 为椭圆 $x^{2} + 4y^{2} = 2x + 3$ 在 $x$ 轴上方的部分.

377 中等题 设 $L$ 为双纽线 $(x^{2} + y^{2})^{2} = a^{2} (x^{2} - y^{2}) (a > 0)$，计算曲线积分 $\oint_{L} |x| - |y| \mathrm{d}s$.

378 中等题 计算 $\int_{L} xyz \mathrm{d}s$，其中 $L$ 为连接 $A (-1, 0, 2)$ 及 $B (3, -2, 1)$ 两点的直线段.

379 中等题 计算 $\oint_{L} (xz + y^{2}) \mathrm{d}s$，其中 $L$ 为曲面 $x^{2} + y^{2} + z^{2} = 6$ 与 $x + z = 2$ 的交线.

380 中等题 计算 $\oint_{L} y \mathrm{d}s$，其中 $L$ 是直线 $y = 2x$ 及抛物线 $y^{2} = x$ 围成的区域的整个边界.

## tool · 2026-10-19T23:47:23Z


Script completed
Wall time 0.1 seconds
Output:

\section{第11章\quad 曲线积分}
\subsection{对弧长的曲线积分}

\begin{problem}{356}{63}{弧长积分与取向}
设分段光滑曲线弧 $L$ 的长度为 $a>0$，$k$ 为常数。从弧长积分的定义求 $\int_Lk\,\dd s$，并判断将曲线反向后结果是否改变；若已知 $\int_L(k+1)\,\dd s=3a$，求 $k$。
\end{problem}

\begin{problem}{357}{63}{弧长积分的保序性}
设 $L$ 为长度非零的分段光滑曲线弧，$f$ 在 $L$ 上连续且非负。证明 $\int_Lf\,\dd s\geq0$；进一步证明，若 $f$ 在 $L$ 的某个内点处为正，则积分严格为正，并据此给出积分等于零的充要条件。
\end{problem}

\begin{problem}{358}{63}{积分比较与严格不等式}
设 $f,g$ 在长度非零的分段光滑曲线弧 $L$ 上连续，且 $f\geq g$。证明
$\int_Lf\,\dd s\geq\int_Lg\,\dd s$。
判断仅有“某一点 $f>g$”能否推出严格不等式，并说明连续性在判断中的作用。
\end{problem}

\begin{problem}{381}{68}{折线上的弧长积分}
设 $L$ 为顶点 $O(0,0),A(1,0),B(0,1)$ 的三角形边界。分边计算
$\oint_L\frac{x}{1+y}\,\dd s$，并求密度为 $\rho(x,y)=1/(1+y)$ 的三角形细丝的质心横坐标。
\end{problem}

\subsection{对坐标的曲线积分}

\begin{problem}{382}{68}{坐标微分与弧长微分}
设 $L$ 为从 $(c,a)$ 到 $(c,b)$ 的有向线段，其中 $a<b$，$P,Q$ 连续。求
$\int_LP(x,y)\,\dd x$ 和 $\int_LQ(x,y)\,\dd y$ 的一元积分表达式；再取 $P\equiv1$，比较 $\int_LP\,\dd x$ 与 $\int_LP\,\dd s$。
\end{problem}

\begin{problem}{383}{68}{常向量场与端点}
设 $L$ 为由 $A(x_1,y_1)$ 到 $B(x_2,y_2)$ 的分段光滑曲线，$k,m$ 为常数。求
$\int_Lk\,\dd x$、$\int_Lk\,\dd y$ 及 $\int_L(k\,\dd x+m\,\dd y)$；据此说明常向量场所做的功与路径无关，并求反向积分。
\end{problem}

\begin{problem}{403}{72}{折点路径与全微分}
设 $L$ 为圆锥面 $z=\sqrt{x^2+y^2}$ 与平面 $y=x$ 的交线上从 $A(1,1,\sqrt2)$ 经原点到 $B(-1,-1,\sqrt2)$ 的曲线弧。
说明 $L$ 在原点处的光滑性，并分别用分段参数法和全微分法计算
$\int_Lyz\,\dd x+zx\,\dd y+xy\,\dd z$。
\end{problem}

\begin{problem}{404}{72}{有向单位切向量}
设 $L$ 是圆周 $x^2+y^2=2y$ 上从原点到 $(0,2)$ 的右半圆弧，$P,Q$ 连续。
求与 $L$ 同向的单位切向量，将 $\int_LP\,\dd x+Q\,\dd y$ 化为对弧长的积分；再取 $P=x,Q=y$ 计算，并检验反向后的符号。
\end{problem}

\begin{problem}{405}{72}{两类曲线积分与方向}
设 $L$ 为 $x=t,y=t^2,z=t^3$ 上 $t$ 从 $1$ 变到 $0$ 的曲线弧，弧长为 $a$。
不用求出 $a$ 的具体数值，计算
\[
 \int_L\frac{\dd x+2x\,\dd y+3y\,\dd z}{\sqrt{1+4x^2+9y^2}}.
\]
再将三个坐标微分的系数解释为沿正参数方向的单位切向量分量，说明取向如何决定结果。
\end{problem}

\begin{problem}{406}{72}{抛物线弧上的积分转换}
设 $f$ 连续，$L$ 为 $y=x^2$ 上从 $(1,1)$ 到 $(0,0)$ 的曲线弧。
\begin{enumerate}[label=(\arabic*)]
\item 把 $I=\int_L f(x,y)\,\dd x+2xf(x,y)\,\dd y$ 转化为对弧长的积分，写明符号的来源。
\item 当 $f(x,y)=1/(x^2+3y+1)$ 时计算 $I$。
\item 当 $f$ 在 $L$ 上非负时，判断 $I$ 的符号；给出等号成立的条件。
\end{enumerate}
\end{problem}
Contents
目录

第8章 向量代数与空间解析几何

第一节 向量及其线性运算····· 1
第二节 内积、向量积和混合积····· 3
第三节 平面与方程····· 6
第四节 空间直线及其方程····· 8
第五节 曲面及其方程····· 12

第9章 多元函数微分法及其应用

第一节 多元函数的基本概念····· 15
第二节 偏导数····· 18
第三节 全微分····· 22
第四节 多元复合函数的求导法则····· 25
第五节 隐函数的求导法则····· 27
第六节 多元函数微分法在几何上的应用····· 31
第七节 方向导数和梯度····· 33
第八节 多元函数的极值及其应用····· 34
第九节 二元函数的泰勒公式····· 37
综合提高题····· 39

第10章 重积分

第一节 二重积分的概念和性质····· 43目录

第二节 二重积分的计算方法····47
第三节 三重积分····55
第四节 重积分的应用····58

第11章 曲线积分

第一节 对弧长的曲线积分····63
第二节 对坐标的曲线积分····68
第三节 格林公式及其应用····72
第四节 曲线积分的应用····78
综合提高题····81

第12章 曲面积分

第一节 对面积的曲面积分（第一类曲面积分）····85
第二节 对坐标的曲面积分（第二类曲面积分）····88
第三节 高斯公式····93
第四节 斯托克斯公式····96
第五节 曲面积分的应用····99
综合提高题····101

第13章 无穷级数

第一节 常数项级数的概念与性质····105
第二节 正项级数····108
{}
101:\begin{problem}{378}{67}{空间线段的弧长积分}
105:\begin{problem}{379}{67}{空间截圆上的二次矩}
109:\begin{problem}{380}{67}{封闭边界与线密度质量}
113:\begin{problem}{381}{68}{折线上的弧长积分}
120:\begin{problem}{382}{68}{坐标微分与弧长微分}
125:\begin{problem}{383}{68}{常向量场与端点}
130:\begin{problem}{403}{72}{折点路径与全微分}
136:\begin{problem}{404}{72}{有向单位切向量}
141:\begin{problem}{405}{72}{两类曲线积分与方向}
150:\begin{problem}{406}{72}{抛物线弧上的积分转换}


## tool · 2026-10-19T23:47:27Z


Script completed
Wall time 0.1 seconds
Output:

二、对坐标的曲线积分的性质

性质 1: 设 $a, b$ 为常数, 则

$$\int_L aP \mathrm{d}x + bQ \mathrm{d}y = a \int_L P \mathrm{d}x + b \int_L Q \mathrm{d}y,$$

$$\int_L (aP_1 + bP_2) \mathrm{d}x + (aQ_1 + bQ_2) \mathrm{d}y = a \int_L P_1 \mathrm{d}x + Q_1 \mathrm{d}y + b \int_L P_2 \mathrm{d}x + Q_2 \mathrm{d}y.$$

性质 2: 若有向曲线弧 $L$ 可分成两段光滑的同向曲线弧 $L_1$ 和 $L_2$, 则

$$\int_L P \mathrm{d}x + Q \mathrm{d}y = \int_L_1 P \mathrm{d}x + Q \mathrm{d}y + \int_L_2 P \mathrm{d}x + Q \mathrm{d}y.$$

性质 3: 若 $L^-$ 是有向曲线弧 $L$ 的反向曲线弧, 则

$$\int_L P \mathrm{d}x + Q \mathrm{d}y = -\int_L P \mathrm{d}x + Q \mathrm{d}y.$$

评注

对坐标的曲线积分与积分弧段的方向有关. 在计算对坐标的曲线积分时, 必须注意积分弧段的方向.

三、对坐标的曲线积分的计算

对坐标的曲线积分的计算是将其转化为定积分进行计算, 具体形式如下.

若有向曲线弧 $L$ 的参数方程为 $\begin{cases} x = \varphi(t) \\ y = \psi(t) \end{cases}$ (t: 单调地由 $\alpha$ 变到 $\beta$), 其中 $t = \alpha$ 对应 $L$ 的起点, $t = \beta$ 对应 $L$ 的终点, 则

$$\int_L P(x, y) \mathrm{d}x + Q(x, y) \mathrm{d}y = \int_\alpha^\beta \left\{ P[\varphi(t), \psi(t)] \varphi'(t) + Q[\varphi(t), \psi(t)] \psi'(t) \right\} \mathrm{d}t.$$

若有向曲线弧 $L$ 的方程为 $y = \varphi(x)$ (x: 单调地由 $a$ 变到 $b$), 其中 $x = a$ 对应 $L$ 的起点, $x = b$ 对应 $L$ 的终点, 则

$$\int_L P(x, y) \mathrm{d}x + Q(x, y) \mathrm{d}y = \int_a^b \left\{ P[x, \varphi(x)] + Q[x, \varphi(x)] \varphi'(x) \right\} \mathrm{d}x.$$

若有向曲线弧 $L$ 的方程为 $x = \psi(y)$ (y: 单调地由 $c$ 变到 $d$), 其中 $y = c$ 对应 $L$ 的起点, $y = d$ 对应 $L$ 的终点, 则

$$\int_L P(x, y) \mathrm{d}x + Q(x, y) \mathrm{d}y = \int_c^d \left\{ P[\psi(y), y] \psi'(y) + Q[\psi(y), y] \psi'(y) \right\} \mathrm{d}y.$$

若空间有向曲线弧 $L$ 的参数方程为 $\begin{cases} x = \varphi(t) \\ y = \psi(t) \\ z = \omega(t) \end{cases}$ (t: 单调地由 $\alpha$ 变到 $\beta$), 其中 $t = \alpha$ 对应 $L$ 的起点, $t = \beta$ 对应 $L$ 的终点, 则

$$\int_L P(x, y, z) \mathrm{d}x + Q(x, y, z) \mathrm{d}y + R(x, y, z) \mathrm{d}z$$

$$= \int_\alpha^\beta \left\{ P[\varphi(t), \psi(t), \omega(t)] \varphi'(t) + Q[\varphi(t), \psi(t), \omega(t)] \psi'(t) + R[\varphi(t), \psi(t), \omega(t)] \omega'(t) \right\} \mathrm{d}t.$$将对坐标的曲线积分转化为定积分时，务必注意：
积分下限对应曲线弧的起点，积分上限对应曲线弧的终点；
积分下限不一定小于积分上限.

384 基础题 设 $L$ 是曲线 $y=\sin x$ 上从原点到点 $(\pi, 0)$ 的一段弧，则
$$\int_{L} \sqrt{1-y^2} \, dx =$$ ____ .

385 基础题 设 $L$ 是抛物线 $y=x^2$ 上从点 $A(-1, 1)$ 到点 $B(1, 1)$ 的一段弧，则
$$\int_{L} (x+e^y) \, dy =$$ ____ .

386 基础题 设 $L$ 是从点 $(3, 0)$ 到点 $(0, 1)$ 的直线段，则 $\int_{L} xy \, dy =$$ ____ .

387 基础题 设 $L$ 是双曲线 $xy=1$ 上从点 $(1, 1)$ 到点 $\left(2, \frac{1}{2}\right)$ 的一段弧，则
$$\int_{L} x \ln y \, dy =$$ ____ .

388 基础题 计算曲线积分 $I=\int_{L} e^y \sin x \, dx+(1-y) \, dy$，其中 $L$ 是曲线 $y=\cos x$ 上从点 $(0, 1)$ 到点 $(\pi, -1)$ 的一段弧.

389 基础题 计算曲线积分 $\int_{L} \frac{xy \, dx-x^2 \, dy}{1+x}$，其中 $L$ 是抛物线 $y^2=x$ 上从点 $A(1, -1)$ 到点 $B(1, 1)$ 的一段弧.

390 基础题 计算 $\int_{L} (2a-y) \, dx+dy$，其中 $L$ 为摆线 $\left\{ \begin{array}{l} x=a(t-\sin t) \\ y=a(1-\cos t) \end{array} \right.$ ($0 \leqslant t \leqslant 2\pi$) 沿 $t$ 增大方向的一拱.

391 基础题 计算曲线积分 $I=\int_{L} y \, dx+z \, dy-x^2 \, dz$，其中 $L$ 是螺旋线 $x=2\cos t$，$y=2\sin t$，$z=t$ 上从 $t=0$ 到 $t=\pi$ 的一段弧.

392 中等题 计算曲线积分 $\int_{L} y \, dx+x \, dy$，其中 $L$ 为椭圆 $x^2+4y^2=4$ 在第一象限的部分，并取逆时针方向.393 中等题 计算曲线积分 $\oint_{L} \frac{y \mathrm{d}x - x \mathrm{d}y}{x^2 + y^2}$，其中 $L$ 为顺时针方向的圆周 $x^2 + y^2 = a^2 (a > 0)$.

394 中等题 设曲线 $L$ 是以点 $(1, 2)$ 为圆心、半径等于 3 的取逆时针方向的圆，计算曲线积分 $I = \oint_{L} \frac{\mathrm{d}x + \mathrm{d}y}{x^2 + y^2 - 2x - 4y}$.

395 中等题 计算 $\int_{L} x \mathrm{d}x + y \mathrm{d}y + z \mathrm{d}z$，其中 $L$ 为从点 $A(1, 2, 3)$ 到点 $B(-1, 4, 0)$ 的直线段.

396 中等题 计算曲线积分 $I = \oint_{\Gamma} y z \mathrm{d}x - \frac{x}{x^2 + y^2} \mathrm{d}y - \frac{y}{x + z} \mathrm{d}z$，其中 $\Gamma$ 为圆柱面 $x^2 + y^2 = 1$ 与平面 $x + z = 1$ 的交线，从 $x$ 轴正方向看去 $\Gamma$ 取顺时针方向.

397 中等题 已知曲线 $L$ 的方程为 $y = 1 - |x|$，$x \in [-1, 1]$，起点是 $(-1, 0)$，终点是 $(1, 0)$，则曲线积分 $\int_{L} y^2 \mathrm{d}x + x^2 \mathrm{d}y = \_\_\_\_\_$.

398 中等题 设 $L$ 为有向闭折线 $OABO$，其中点 $O, A, B$ 分别为 $(0, 0), (1, 0), (1, 2)$，计算曲线积分 $\oint_{L} e^y \mathrm{d}x + e^x \mathrm{d}y$.

399 中等题 设 $L$ 是第一象限中从点 $O(0, 0)$ 沿圆周 $x^2 + y^2 = 2x$ 到点 $A(2, 0)$，再沿圆周 $x^2 + y^2 = 4$ 到点 $B(0, 2)$ 的曲线段，计算曲线积分 $\int_{L} y \mathrm{d}x + (x - 1) \mathrm{d}y$.

400 中等题 设 $L$ 是由原点 $O$ 沿抛物线 $y = \sqrt{x}$ 到点 $A(1, 1)$，再由点 $A$ 沿直线 $y = x$ 回到原点的封闭曲线，计算曲线积分 $\oint_{L} \arctan \frac{x}{y} \mathrm{d}x - \mathrm{d}y$.

401 中等题 设 $L$ 为有向折线 $ABCD$，其中点 $A, B, C, D$ 分别为 $(0, 0, 0), (0, 0, 2), (1, 0, 2), (1, 3, 2)$，则曲线积分 $I = \int_{L} z^2 \mathrm{d}x + x^2 \mathrm{d}y + y^2 \mathrm{d}z = \_\_\_\_\_$.

402 中等题 计算曲线积分 $I = \oint_{L} z \mathrm{d}x + x \mathrm{d}y - \frac{y + z}{2} \mathrm{d}z$，其中 $L$ 为球面 $x^2 + y^2 + z^2 = 6$ 与平面 $y + z = 2$ 的交线，从 $z$ 轴正方向往原点看去 $L$ 取逆时针方向.$$\oint_L P \mathrm{d}x + Q \mathrm{d}y = \iint_D \left( \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right) \mathrm{d}x \mathrm{d}y$$
其中 $L$ 为 $D$ 的边界曲线，且取正向.

评注
当 $L$ 取负向时，$$\oint_L P \mathrm{d}x + Q \mathrm{d}y = -\iint_D \left( \frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y} \right) \mathrm{d}x \mathrm{d}y.$$

利用格林公式，我们可以将曲线积分 $$\oint_L P \mathrm{d}x + Q \mathrm{d}y$$ 转化为二重积分进行计算.

直接利用格林公式 ($P, Q, \frac{\partial Q}{\partial x}, \frac{\partial P}{\partial y}$ 均连续，$L$ 封闭）

407 基础题 设 $L$ 为有向闭曲线，则 $$\oint_L (y - \cos x) \mathrm{d}x + (x + \sin y) \mathrm{d}y =$$ ____.

408 基础题 设 $D$ 为平面有界闭区域，$L$ 为 $D$ 的正向边界曲线，若 $$\oint_L (1 + 3y) \mathrm{d}x + (5x - 1) \mathrm{d}y = 4$$，则 $D$ 的面积为 ____.

409 基础题 设 $L$ 是以点 $(0, 0)$, $(3, 0)$ 和 $(3, 2)$ 为顶点的三角形的边界，方向取顺时针方向，则 $$\oint_L (2x + y - 4) \mathrm{d}x + (5x - 3y + 6) \mathrm{d}y =$$ ____.

410 基础题 计算 $I = \oint_L (2x + y^2) \mathrm{d}x + (3y - x^2) \mathrm{d}y$，其中 $L$ 是由曲线 $xy = 1, y = x, x = 2$ 围成的区域的负向边界.

411 中等题 计算 $$\oint_L x^2 y \mathrm{d}x - xy^2 \mathrm{d}y$$，其中 $L$ 为正向圆周 $x^2 + y^2 = R^2.$

412 中等题 计算 $$\oint_L \frac{1}{x} \arctan \frac{y}{x} \mathrm{d}x + \frac{2}{y} \arctan \frac{x}{y} \mathrm{d}y$$，其中 $L$ 是由曲线 $x^2 + y^2 = 1,$ $x^2 + y^2 = 4,$ $y = x,$ $y = \sqrt{3} x (y > 0)$ 围成的区域的正向边界.

413 中等题 计算 $$\oint_L (\mathrm{e}^x + 2y) \mathrm{d}x - (2\mathrm{e}^y - xy) \mathrm{d}y$$，其中 $L$ 是由曲线 $y^2 = 2x,$ $y = x - 4$ 围成的区域的边界，方向取顺时针方向.

414 中等题 计算曲线积分 $I = \oint_L (x^2 y - xy^3) \mathrm{d}x + (y^2 - 2xy) \mathrm{d}y$，其中 $L$ 是以点 $(1, 0), (0, 1), (-1, 0), (0, -1)$ 为顶点的四边形的边界，方向取逆时针方向.

补线后利用格林公式 ($L$ 不封闭)
若 $L$ 不是封闭曲线，我们应添加有向曲线段 $L_1$，使 $L + L_1$ 为封闭曲线，且方向同为正向或负向，则
$$\int_{L} P \mathrm{d}x + Q \mathrm{d}y = \oint_{L+L_{1}} P \mathrm{d}x + Q \mathrm{d}y - \int_{L_{1}} P \mathrm{d}x + Q \mathrm{d}y$$
然后对 $\oint_{L+L_{1}} P \mathrm{d}x + Q \mathrm{d}y$ 应用格林公式即可.

415 中等题 已知曲线 $L$ 的方程为 $y=1-|x|, x \in[-1, 1]$，起点是 $(-1, 0)$，终点是 $(1, 0)$，则曲线积分 $\int_{L} xy \mathrm{d}x + x^{2} \mathrm{d}y =$ ____.

416 中等题 计算曲线积分 $I = \int_{L} (x^{2}-3y) \mathrm{d}x + (2y^{3}+x) \mathrm{d}y$，其中 $L$ 为上半圆周 $y=\sqrt{4x-x^{2}}$ 从点 $O(0, 0)$ 到点 $A(4, 0)$ 的一段弧.

417 中等题 计算曲线积分 $\int_{L} \frac{(y^{2}+e^{x}) \mathrm{d}x + (x^{2}+y^{4}) \mathrm{d}y}{y^{2}-2x+3}$，其中 $L$ 是抛物线 $y^{2}=2x$ 上从点 $A(2, 2)$ 到点 $B(2, -2)$ 的一段弧.

挖洞后利用格林公式（存在奇点——$P, Q, \frac{\partial Q}{\partial x}, \frac{\partial P}{\partial y}$ 的不连续点）
若 $D$ 内有奇点，使得 $\frac{\partial Q}{\partial x}, \frac{\partial P}{\partial y}$ 不连续，则要在 $D$ 内作封闭曲线 $L_{1}$，即“挖洞”去掉该奇点，然后在外边界 $L$ 和内边界 $L_{1}$ 围成的复连通区域上应用格林公式.

418 中等题 计算曲线积分 $\oint_{L} \frac{x \mathrm{d}y-y \mathrm{d}x}{x^{2}+y^{2}}$，其中 $L$ 为曲线 $y^{2}=x+3$ 及 $x=2$ 围成的区域的边界，方向取逆时针方向.

419 中等题 计算曲线积分 $\oint_{L} \frac{y \mathrm{d}x-x \mathrm{d}y}{4x^{2}+y^{2}}$，其中 $L$ 是以 $(1, 0)$ 为圆心、半径为 $R(R>1)$ 的负向圆周.

二、平面曲线积分与路径无关

曲线积分与路径无关的判定
曲线积分 $\int_{L} P \mathrm{d}x + Q \mathrm{d}y$ 与路径无关
$\Leftrightarrow \frac{\partial Q}{\partial x} = \frac{\partial P}{\partial y}$;
$\Leftrightarrow \oint_{L} P \mathrm{d}x + Q \mathrm{d}y=0$，其中 $L$ 为任意分段光滑的封闭曲线;
$\Leftrightarrow$ 存在函数 $u(x, y)$，使得 $\mathrm{d}u=P \mathrm{d}x+Q \mathrm{d}y$.420 基础题 若曲线积分 $\int_{L} \frac{ax\mathrm{d}x + 2y\mathrm{d}y}{x^2 + y^2 - 1}$ 在区域 $D = \{(x, y) | x^2 + y^2 < 1\}$ 内与路径无关，则 $a =$ ____.

421 基础题 若曲线积分 $\int_{L} (ax^2\cos y - y^3\sin x)\mathrm{d}x + (by^2\cos x + x^3\sin y)\mathrm{d}y$ 与路径无关，则（ ）。
(A) $a = 3, b = -3$
(B) $a = -3, b = 3$
(C) $a = 3, b = 3$
(D) $a = -3, b = -3$

422 基础题 已知 $F(x, y)$ 具有连续导数，$\Gamma$ 为任意有向分段光滑的封闭平面曲线，则曲线积分 $\oint_{\Gamma} F(x, y)(y\mathrm{d}x + x\mathrm{d}y) = 0$ 的充要条件是（ ）。
(A) $F_x'(x, y) = F_y'(x, y)$
(B) $F_x'(x, y) = -F_y'(x, y)$
(C) $xF_x'(x, y) = yF_y'(x, y)$
(D) $yF_x'(x, y) = xF_y'(x, y)$

423 基础题 已知 $\frac{(ay - x)\mathrm{d}x - y\mathrm{d}y}{(x + y)^2}$ 为某个函数 $u(x, y)$ 的全微分，则 $a =$ ____.

424 基础题 设 $f(u)$ 具有一阶连续导数，$L$ 是从点 $A$ 到点 $B$ 的有向分段光滑曲线，证明曲线积分 $\int_{L} f(xy)(y\mathrm{d}x + x\mathrm{d}y)$ 与路径 $L$ 无关.

425 中等题 设函数 $f(x)$ 具有连续导数，且 $f(0) = 1$，曲线积分 $\int_{L} [xy^2 - f(x)]\mathrm{d}x + yf(x)\mathrm{d}y$ 与路径无关，则 $f(x) =$ ____.

426 中等题 设在上半平面 $D = \{(x, y) | y > 0\}$ 内，函数 $f(x, y)$ 具有连续导数，且对任意的 $t > 0$，都有 $f(tx, ty) = t^{-2}f(x, y)$ 成立．证明：对 $D$ 内任意分段光滑的有向简单闭曲线 $L$，都有 $\oint_{L} f(x, y)(y\mathrm{d}x - x\mathrm{d}y) = 0$．

利用曲线积分与路径无关计算曲线积分
若曲线积分 $\int_{L} P\mathrm{d}x + Q\mathrm{d}y$ 与路径 $L$ 无关，只与 $L$ 的起点 $A$ 和终点 $B$ 有关，则计算曲线积分常用下列两种方法．
方法一：改变积分路径．若原路径 $L$ 较复杂，可以改变路径，取一条简单的路径 $L_1$ 来计算（常取从起点 $A$ 到终点 $B$ 的平行于坐标轴的折线），则
$$\int_{L} P\mathrm{d}x + Q\mathrm{d}y = \int_{L_1} P\mathrm{d}x + Q\mathrm{d}y.$$
方法二：找原函数，利用曲线积分的基本公式．若找到 $P\mathrm{d}x + Q\mathrm{d}y$ 的一个原函数 $u(x, y)$，即 $\mathrm{d}u = P\mathrm{d}x + Q\mathrm{d}y$，则

## tool · 2026-10-19T23:47:32Z


Script completed
Wall time 0.1 seconds
Output:

$$\int_{L} P \mathrm{d}x + Q \mathrm{d}y = u(x,y) \bigg|_{A}^{B} = u(B) - u(A),$$
其中 $u(A), u(B)$ 分别为 $u(x,y)$ 在 $A,B$ 两点的函数值.

427 基础题 设 $L$ 为正向椭圆线 $\frac{x^2}{4} + \frac{y^2}{9} = 1$，则曲线积分
$$\oint_{L} (3x^2 \cos x - x^3 \sin x) y \mathrm{d}x + (x^3 \cos x + 2y^2) \mathrm{d}y = \_\_\_\_\_.$$

428 基础题 计算曲线积分 $I = \int_{L} \left( e^x + 2x \sin y \right) \mathrm{d}x + \left( x^2 + e^{-y^2} \right) \cos y \mathrm{d}y$，其中 $L$ 为曲线 $y = \sqrt{2x-x^2}$，取顺时针方向.

429 基础题 设 $L$ 是从点 $A(1,2)$ 到点 $B(-1,1)$ 的任意一段光滑曲线，则曲线积分
$$\int_{L} \left( x^3 - 2xy - y^2 \right) \mathrm{d}x - (x+y)^2 \mathrm{d}y = \_\_\_\_\_.$$

430 基础题 设 $L$ 是曲线 $y = \frac{1}{2} x^3$ 上从点 $O(0,0)$ 到点 $A(2,4)$ 的一段弧，则曲线积分
$$\int_{L} e^{x^2+y^2} (x \mathrm{d}x + y \mathrm{d}y) = \_\_\_\_\_.$$

431 基础题 证明曲线积分 $\int_{(-1,-2)}^{(3,4)} (x+2y) \mathrm{d}x + (2x-y) \mathrm{d}y$ 与路径无关，并计算该积分值.

432 中等题 计算曲线积分 $\int_{(2,0)}^{(4,3)} (xy^2 + x-y) \mathrm{d}x + (x^2y-x+y) \mathrm{d}y.$

三、格林公式的应用

求平面图形的面积
借助格林公式，我们可以利用曲线积分求平面闭区域 $D$ 的面积，公式为
$$S = \frac{1}{2} \oint_{L} x \mathrm{d}y - y \mathrm{d}x$$
其中，$L$ 为 $D$ 的正向边界.

评注
$D$ 的面积计算公式不唯一，可以表示为多种曲线积分的形式，如
$$S = \oint_{L} y \mathrm{d}x + 2x \mathrm{d}y$$
$$S = \oint_{L} x \mathrm{d}y$$
$$S = -\oint_{L} y \mathrm{d}x.$$433 基础题 利用曲线积分求星形线 $\begin{cases} x = a \cos^3 t \\ y = a \sin^3 t \end{cases}$ ($a > 0$) 围成的平面图形的面积.

434 中等题 利用格林公式求双纽线 $(x^2 + y^2)^2 = a^2 (x^2 - y^2)$ ($a > 0$) 围成的平面图形的面积.

求 $Pdx + Qdy$ 的原函数
定义：若 $P(x,y)dx + Q(x,y)dy$ 是某个函数 $u(x,y)$ 的全微分，即
$du(x,y) = P(x,y)dx + Q(x,y)dy$，
则称 $u(x,y)$ 为 $P(x,y)dx + Q(x,y)dy$ 的一个原函数.
原函数存在的判定及求法：
若 $P(x,y), Q(x,y)$ 在单连通区域 $D$ 内具有一阶连续偏导数，则在 $D$ 内
$P(x,y)dx + Q(x,y)dy$ 的原函数存在的充要条件是
$\frac{\partial Q}{\partial x} = \frac{\partial P}{\partial y}$.
并且 $P(x,y)dx + Q(x,y)dy$ 的一个原函数为
$u(x,y) = \int_{(x_0,y_0)}^{(x,y)} P(x,y)dx + Q(x,y)dy$，
其中起点 $(x_0,y_0)$ 为 $D$ 内某一定点，终点 $(x,y)$ 为 $D$ 内任意点.
$P(x,y)dx + Q(x,y)dy$ 的所有原函数为 $u(x,y) + C$，$C$ 为任意常数.

评注
$P(x,y)dx + Q(x,y)dy$ 是某个函数的全微分 $\Leftrightarrow \frac{\partial Q}{\partial x} = \frac{\partial P}{\partial y}$.

435 基础题 验证 $(2x + \sin y)dx + x\cos ydy$ 是某个函数的全微分，并求出一个这样的函数.

436 中等题 求全微分 $\frac{ydx - xdy}{x^2 + y^2}$ 在右半平面 ($x > 0$) 内的原函数.

437 中等题 已知可微函数 $u(x,y)$ 的全微分为
$du(x,y) = (x + a)e^{x+y}dx + (xe^{x+y} + bx - 2y)dy$.
(I) 求常数 $a,b$;
(II) 若 $u(0,0) = 1$，求 $u(x,y)$.

解全微分方程
定义：若 $P(x,y)dx + Q(x,y)dy$ 的原函数存在，则称一阶微分方程$P(x, y) \mathrm{d}x + Q(x, y) \mathrm{d}y = 0$

为全微分方程.

全微分方程的判定及求解:
若 $P(x, y), Q(x, y)$ 在单连通区域 $D$ 内具有一阶连续偏导数，则
$P(x, y) \mathrm{d}x + Q(x, y) \mathrm{d}y = 0$ 为全微分方程 $\Leftrightarrow \frac{\partial Q}{\partial x} = \frac{\partial P}{\partial y}$.

其通解为
$u(x, y) = \int_{(x_0, y_0)}^{(x, y)} P(x, y) \mathrm{d}x + Q(x, y) \mathrm{d}y = C, C$ 为任意常数.

评注
若 $u(x, y)$ 为 $P \mathrm{d}x + Q \mathrm{d}y$ 的一个原函数，则全微分方程 $P \mathrm{d}x + Q \mathrm{d}y = 0$ 的通解为 $u(x, y) = C, C$ 为任意常数.

由此可见，求解全微分方程 $P \mathrm{d}x + Q \mathrm{d}y = 0$ 等同于求 $P \mathrm{d}x + Q \mathrm{d}y$ 的原函数 $u(x, y)$.

438 基础题 下列方程是全微分方程的是 (    ).

(A) $(x^2 + y) \mathrm{d}x - x \mathrm{d}y = 0$
(B) $(\mathrm{e}^y - x) \mathrm{d}x + (y + \mathrm{e}^x) \mathrm{d}y = 0$
(C) $\sin x \cos y \mathrm{d}x + \cos x \sin y \mathrm{d}y = 0$
(D) $xy \mathrm{d}x + (x^2 + y^2) \mathrm{d}y = 0$

439 基础题 求解下列全微分方程.

(1) $(xy^2 - 2x + y) \mathrm{d}x - (2y - x - x^2 y) \mathrm{d}y = 0$;
(2) $(x^2 + \mathrm{e}^{-3y}) \mathrm{d}x + (y - 3x \mathrm{e}^{-3y}) \mathrm{d}y = 0$.

第四节 曲线积分的应用

一、对弧长的曲线积分的应用

求曲线弧的弧长
曲线弧 $L$ 的弧长计算公式为
$s = \int_L \mathrm{d}s$.

440 基础题 计算曲线 $y = \int_0^x \tan t \mathrm{d}t$ 上 $0 \leq x \leq \frac{\pi}{4}$ 的一段弧的弧长.

441 基础题 设 $\Gamma$ 为曲线 $x = \mathrm{e}^t \cos t, y = \mathrm{e}^t \sin t, z = \mathrm{e}^t$ 上 $t$ 从 $0$ 变到 $1$ 的一段弧，则其弧长为 _____.求曲线弧的质量
若平面曲线弧 $L$ 的线密度为 $\rho(x,y)$，则 $L$ 的质量为
$m = \int_{L} \rho(x,y) \mathrm{d}s$.
若空间曲线弧 $L$ 的线密度为 $\rho(x,y,z)$，则 $L$ 的质量为
$m = \int_{L} \rho(x,y,z) \mathrm{d}s$.

442 基础题 设 $L$ 为抛物线 $y=x^2$ 上从点 $(-1,1)$ 到点 $(1,1)$ 的一段弧，其线密度为 $\rho(x,y)=\sqrt{y}$，则 $L$ 的质量为 ____.

443 基础题 求曲线弧 $L$：$x=t,y=\frac{t^2}{2},z=\frac{t^3}{3}(0 \leq t \leq 1)$ 的质量，其线密度为 $\rho(x,y,z)=\sqrt{1+2y+3xz}$.

求曲线弧的质心（重心）
若平面曲线弧 $L$ 的线密度为 $\rho(x,y)$，则 $L$ 的质心（重心）坐标 $(\bar{x},\bar{y})$ 为
$\bar{x} = \frac{\int_{L} x \rho(x,y) \mathrm{d}s}{\int_{L} \rho(x,y) \mathrm{d}s}, \bar{y} = \frac{\int_{L} y \rho(x,y) \mathrm{d}s}{\int_{L} \rho(x,y) \mathrm{d}s}$.
若空间曲线弧 $L$ 的线密度为 $\rho(x,y,z)$，则 $L$ 的质心（重心）坐标 $(\bar{x},\bar{y},\bar{z})$ 为
$\bar{x} = \frac{\int_{L} x \rho(x,y,z) \mathrm{d}s}{\int_{L} \rho(x,y,z) \mathrm{d}s}, \bar{y} = \frac{\int_{L} y \rho(x,y,z) \mathrm{d}s}{\int_{L} \rho(x,y,z) \mathrm{d}s}, \bar{z} = \frac{\int_{L} z \rho(x,y,z) \mathrm{d}s}{\int_{L} \rho(x,y,z) \mathrm{d}s}$.

评注
若曲线弧的质量分布均匀（线密度为常数），则质心（重心或形心）坐标为
$\bar{x} = \frac{\int_{L} x \mathrm{d}s}{\int_{L} \mathrm{d}s}, \bar{y} = \frac{\int_{L} y \mathrm{d}s}{\int_{L} \mathrm{d}s}, \bar{z} = \frac{\int_{L} z \mathrm{d}s}{\int_{L} \mathrm{d}s}$.

444 基础题 一根长度为 1 的细棒位于 $x$ 轴的区间 $[0,1]$ 上，若其线密度为 $\rho(x)=-x^2+x+1$，则该细棒的质心为 ____.

445 中等题 设螺旋形弹簧一圈的方程为 $L$：$\begin{cases} x=2 \cos t \\ y=2 \sin t (0 \leq t \leq 2 \pi) \\ z=3 t \end{cases}$，其线密度为 $\rho(x,y,z)=x^2+y^2+z^2$，求它的重心.求曲线弧的转动惯量
若平面曲线弧 $L$ 的线密度为 $\rho(x,y)$，则 $L$ 对 $x$ 轴、$y$ 轴的转动惯量 $I_x, I_y$ 分别为
$I_x = \int_L y^2 \rho(x,y) \mathrm{d}s, I_y = \int_L x^2 \rho(x,y) \mathrm{d}s.$
若空间曲线弧 $L$ 的线密度为 $\rho(x,y,z)$，则 $L$ 对 $x$ 轴、$y$ 轴、$z$ 轴的转动惯量
$I_x, I_y, I_z$ 分别为
$I_x = \int_L (y^2 + z^2) \rho(x,y,z) \mathrm{d}s,$
$I_y = \int_L (z^2 + x^2) \rho(x,y,z) \mathrm{d}s,$
$I_z = \int_L (x^2 + y^2) \rho(x,y,z) \mathrm{d}s.$

446 基础题 设半圆形铁丝 $L: x^2 + y^2 = 1 (x \geqslant 0)$ 在点 $(x,y)$ 处的线密度为 $\rho(x,y) = |y|$，求它对坐标轴的转动惯量.

447 中等题 设曲线 $\Gamma$ 是球面 $x^2 + y^2 + z^2 = a^2 (a > 0)$ 被平面 $x + y + z = 0$ 所截的圆周，其线密度为 $\rho(x,y,z) = \sqrt{x^2 + y^2 + z^2}$，求 $\Gamma$ 对坐标轴的转动惯量.

二、对坐标的曲线积分的应用

变力沿平面曲线所做的功
设一质点受力 $\vec{F}(x,y) = P(x,y)\vec{i} + Q(x,y)\vec{j}$ 的作用沿平面曲线 $L$ 从点 $A$ 移动到点 $B$，则力 $\vec{F}(x,y)$ 所做的功为
$W = \int_L \vec{F} \cdot \mathrm{d}\vec{r} = \int_L P(x,y) \mathrm{d}x + Q(x,y) \mathrm{d}y.$

变力沿空间曲线所做的功
设一质点受力 $\vec{F}(x,y,z) = P(x,y,z)\vec{i} + Q(x,y,z)\vec{j} + R(x,y,z)\vec{k}$ 的作用沿空间曲线 $L$ 从点 $A$ 移动到点 $B$，则力 $\vec{F}(x,y,z)$ 所做的功为
$W = \int_L \vec{F} \cdot \mathrm{d}\vec{r} = \int_L P(x,y,z) \mathrm{d}x + Q(x,y,z) \mathrm{d}y + R(x,y,z) \mathrm{d}z.$

448 基础题 在力 $\vec{F} = (y,-x,z)$ 的作用下，求质点从点 $A(0,0,0)$ 沿圆锥螺线 $\Gamma: x = t \cos t, y = t \sin t, z = t$ 移动到点 $B\left(0, \frac{\pi}{2}, \frac{\pi}{2}\right)$ 所做的功.

449 中等题 设一质点在点 $M(x,y)$ 处受到力 $\vec{F}$ 的作用，$\vec{F}$ 的大小与点 $M$ 到原点 $O$ 的距离成正比，$\vec{F}$ 的方向指向原点. 若质点沿椭圆 $\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1 (a > 0, b > 0)$ 从点 $A(-a,0)$ 按顺时针方向移动到点 $B(0,b)$，求力 $\vec{F}$ 所做的功.50 中等题 设一质点受力的作用，力的反方向指向原点，力的大小与质点到 $xOy$ 平面的距离成反比. 若质点沿直线 $x=at, y=bt, z=ct (c \neq 0)$ 从点 $M(a,b,c)$ 移动到点 $N(2a,2b,2c)$，求力所做的功.

综合提高题

451 综合题 设 $L$ 为曲线 $y=x^3$ 和 $y=\sqrt[3]{x}$ 在第一象限内围成的区域的整个边界，则 $\oint_L (x-y)^{15} \mathrm{d}s =$ ____.

452 综合题 设 $L$ 为单位圆周 $x^2+y^2=1$，$L_1$ 为 $L$ 在第一象限的部分，$I=\oint_L (x+y+|x|+|y|) \mathrm{d}s, J=\int_{L_1} y \mathrm{d}s.$
(1) 试确定 $I$ 和 $J$ 的关系；
(2) 计算 $I$ 和 $J$ 的值.

453 综合题 计算 $\int_L |\ln(2y-e^x)| \mathrm{d}s$，其中 $L$ 为曲线 $y=\frac{1}{2} (\mathrm{e}^x+\mathrm{e}^{-x})$ 上从点 $\left(-1, \frac{\mathrm{e}^{-1}+\mathrm{e}}{2}\right)$ 到点 $\left(1, \frac{\mathrm{e}^{-1}+\mathrm{e}}{2}\right)$ 的一段弧.

454 综合题 设点 $O, A, B$ 分别为 $(0, 0, 0), (2, 2, 0), (2, 2, 2)$，$L$ 为线段 $OA, AB, BO$ 组成的封闭曲线，计算 $\oint_L z \sin(xy) \mathrm{d}s.$

455 综合题 设 $L$ 为圆周 $x^2+y^2=16$ 与直线 $y=x$ 及 $x$ 轴在第一象限内围成的扇形区域的整个边界，求 $\oint_L e^{\sqrt{x^2+y^2}} \mathrm{d}s.$

456 综合题 设曲线 $L: f(x,y)=1$ （ $f(x,y)$ 具有一阶连续偏导数）过第二象限内的点 $M$ 和第四象限内的点 $N$，$\Gamma$ 为 $L$ 上从点 $M$ 到点 $N$ 的一段弧，则下列小于零的是（ ）

(A) $\int_{\Gamma} f(x,y) \mathrm{d}x$  
(B) $\int_{\Gamma} f(x,y) \mathrm{d}y$  
(C) $\int_{\Gamma} f(x,y) \mathrm{d}s$  
(D) $\int_{\Gamma} f_x'(x,y) \mathrm{d}x+f_y'(x,y) \mathrm{d}y$

457 综合题 计算曲线积分 $\oint_L \frac{1}{\sqrt{1+y}} \mathrm{d}x+x^2 \mathrm{d}y$，其中 $L$ 是抛物线 $y=x^2$ 和 $y^2=x$ 围成的区域的整个边界，且取顺时针方向.458 综合题 在过点 $O(0, 0)$ 和点 $A(\pi, 0)$ 的曲线族 $y = a \sin x (a > 0)$ 中，求一条曲线 $L$ 使沿该曲线从点 $O$ 到点 $A$ 的曲线积分 $I = \int_{L} (1 + y^3) \mathrm{d}x + (2x + y) \mathrm{d}y$ 的值最小.

459 综合题 计算曲线积分 $I = \oint_{\Gamma} \frac{y^2 \mathrm{d}x + z^2 \mathrm{d}y + x^2 \mathrm{d}z}{2x + z^2}$，其中 $\Gamma$ 为球面 $x^2 + y^2 + z^2 = 4$ 和柱面 $x^2 + y^2 = 2x (z > 0)$ 的交线，从 $x$ 轴正方向看去 $\Gamma$ 取逆时针方向.

460 综合题 (1) 已知有向曲线弧 $L$ 的弧长为 $K$，$P(x, y), Q(x, y)$ 在 $L$ 上连续，$M = \max_{(x, y) \in L} \sqrt{[P(x, y)]^2 + [Q(x, y)]^2}$，证明 $\left| \int_{L} P(x, y) \mathrm{d}x + Q(x, y) \mathrm{d}y \right| \leq K M$.

(2) 若 $L$ 为有向圆周 $x^2 + y^2 = R^2$，利用 (1) 中的不等式估计 $I_R = \int_{L} \frac{y \mathrm{d}x - x \mathrm{d}y}{(x^2 + xy + y^2)^2}$，并求极限 $\lim_{R \to +\infty} I_R$.

461 综合题 设 $L$ 为封闭曲线 $|x| + |x + y| = 1$，方向取逆时针方向，则曲线积分 $\oint_L \frac{(x - y) \mathrm{d}x + (x + y) \mathrm{d}y}{|x| + |x + y|} = \_\_\_\_\_$.

462 综合题 设 $F(u, v)$ 具有连续偏导数，连续可微函数 $z = z(x, y)$ 由方程 $F(z + x, z - y) = 0$ 唯一确定，$L$ 为正向单位圆周 $x^2 + y^2 = 1$，计算曲线积分 $\oint_L (z - 3y) \mathrm{d}x + (z + x^2) \mathrm{d}y$.

463 综合题 设 $L$ 是正向圆周 $(x - a)^2 + (y - a)^2 = a^2 (a > 0)$，$f(x)$ 是正值连续函数，证明不等式 $\oint_L xf(y) \mathrm{d}y - \frac{y}{f(x)} \mathrm{d}x \geq 2\pi a^2$.

464 综合题 计算曲线积分 $I = \int_{L} \left(e^x - y^3 + xy^2\right) \mathrm{d}x - (x^2 y + 2x + \sin y) \mathrm{d}y$，其中 $L$ 是曲线 $y = \cos x$ 上从点 $A\left(-\frac{\pi}{2}, 0\right)$ 到点 $B\left(\frac{\pi}{2}, 0\right)$ 的一段弧.

465 综合题 设 $D$ 是平面有界单连通闭区域，$I(D) = \iint_D (4 - x^2 - y^2) \mathrm{d}x \mathrm{d}y$ 取得最大值的积分区域记为 $D_1$.

(I) 求 $I(D_1)$ 的值；

(II) 计算 $\int_{\partial D_1} \frac{(x e^{x^2 + 4y^2} + y) \mathrm{d}x + (4 y e^{x^2 + 4y^2} - x) \mathrm{d}y}{x^2 + 4y^2}$，其中 $\partial D_1$ 是 $D_1$ 的正向边界.466 综合题 设曲线积分 $\int_{L}[f(x)-e^{x}]\sin y\mathrm{d}x-f(x)\cos y\mathrm{d}y$ 与路径无关，其中 $f(x)$ 具有一阶连续导数，且 $f(0)=0$，则 $f(x)$ 等于（    ）.

(A) $\frac{e^{-x}-e^{x}}{2}$
(B) $\frac{e^{x}-e^{-x}}{2}$
(C) $\frac{e^{x}-e^{-x}}{2}-1$
(D) $1-\frac{e^{x}+e^{-x}}{2}$

467 综合题 计算曲线积分 $I=\int_{L}(1-2xy-y^{2})\mathrm{d}x-(x+y)^{2}\mathrm{d}y$，其中 $L$ 是 $x^{2}+y^{2}=2y$ 上从点 $O(0,0)$ 到点 $A(1,1)$ 的一段有向弧.

468 综合题 设曲线积分 $I=\int_{(1,0)}^{(2,3)}yf(x)\mathrm{d}x+[2xf(x)-x^{2}]\mathrm{d}y$ 在右半平面 $(x>0)$ 内与路径无关，其中 $f(x)$ 可导，且 $f(1)=0$.
(I) 求 $f(x)$；
(II) 计算曲线积分 $I$ .

469 综合题 设函数 $Q(x,y)$ 在 $xOy$ 平面上具有一阶连续偏导数，曲线积分 $\int_{L}2xy\mathrm{d}x+Q(x,y)\mathrm{d}y$ 与路径无关，对任意的 $t$, $\int_{(0,0)}^{(t,1)}2xy\mathrm{d}x+Q(x,y)\mathrm{d}y=\int_{(0,0)}^{(1,t)}2xy\mathrm{d}x+Q(x,y)\mathrm{d}y$ 恒成立，求 $Q(x,y)$ .

470 综合题 设函数 $f(x,y)$ 满足 $\frac{\partial f(x,y)}{\partial x}=(2x+1)\mathrm{e}^{2x-y}$，且 $f(0,y)=y+1$，$L_{t}$ 是从点 $(0,0)$ 到点 $(1,t)$ 的光滑曲线.
(1) 求函数 $f(x,y)$；
(2) 计算曲线积分 $I(t)=\int_{L_{t}}\frac{\partial f(x,y)}{\partial x}\mathrm{d}x+\frac{\partial f(x,y)}{\partial y}\mathrm{d}y$；
(3) 求 $I(t)$ 的最小值.

471 综合题 设三角形的 3 个顶点按逆时针方向依次为 $M_{1}(x_{1},y_{1}),M_{2}(x_{2},y_{2})$, $M_{3}(x_{3},y_{3})$，试利用曲线积分证明此三角形的面积为
$S=\frac{1}{2}[(x_{1}y_{2}-x_{2}y_{1})+(x_{2}y_{3}-x_{3}y_{2})+(x_{3}y_{1}-x_{1}y_{3})]$ .

472 综合题 若函数 $u(x,y)$ 可微，且其全微分为
$\mathrm{d}u(x,y)=(xy^{2}+a\sin x\cos x\sin 3y)\mathrm{d}x-(bx^{2}y+\cos 2x\cos 3y)\mathrm{d}y$.
(I) 求常数 $a,b$；
(II) 求 $u(x,y)$ 的表达式；
(III) 求方程 $(xy^{2}+a\sin x\cos x\sin 3y)\mathrm{d}x-(bx^{2}y+\cos 2x\cos 3y)\mathrm{d}y=0$ 的通解.473 综合题 正弦曲线 $L_{1}: y=\sin x$ 一个周期的弧长为 $s_{1}$，椭圆 $L_{2}: x^{2}+2y^{2}=2$ 周长为 $s_{2}$，则（    ）。
(A) $s_{1}<s_{2}$
(B) $s_{1}>s_{2}$
(C) $s_{1}=s_{2}$
(D) $s_{1}=2s_{2}$

474 综合题 设 $y(x)$ 是微分方程 $2xy^{\prime}-4y=2\ln x-1$ 满足 $y(1)=\frac{1}{4}$ 的解，求均匀曲线弧 $L: y=y(x) (1 \leqslant x \leqslant e)$ 的重心.

475 综合题 设质点 $M$ 受到力 $\vec{F}$ 的作用，其中 $\vec{F}$ 的大小与点 $M$ 到原点 $O$ 的距离成反比，比例系数为 2，力的方向为向量 $\overrightarrow{OM}$ 顺时针旋转 $90^{\circ}$ 角的方向。试求质点 $M$ 从点 $A\left(0,\frac{\pi}{2}\right)$ 沿着曲线 $y=\frac{\pi}{2}\cos x$ 移动到点 $B\left(\frac{\pi}{2},0\right)$ 时，力 $\vec{F}$ 所做的功.

## tool · 2026-10-19T23:47:47Z




## tool · 2026-10-19T23:48:28Z


Script completed
Wall time 0.1 seconds
Output:

\subsection{对坐标的曲线积分}

\begin{problem}{382}{68}{坐标微分与弧长微分}
设 $L$ 为从 $(c,a)$ 到 $(c,b)$ 的有向线段，其中 $a<b$，$P,Q$ 连续。求
$\int_LP(x,y)\,\dd x$ 和 $\int_LQ(x,y)\,\dd y$ 的一元积分表达式；再取 $P\equiv1$，比较 $\int_LP\,\dd x$ 与 $\int_LP\,\dd s$。
\end{problem}

\begin{problem}{383}{68}{常向量场与端点}
设 $L$ 为由 $A(x_1,y_1)$ 到 $B(x_2,y_2)$ 的分段光滑曲线，$k,m$ 为常数。求
$\int_Lk\,\dd x$、$\int_Lk\,\dd y$ 及 $\int_L(k\,\dd x+m\,\dd y)$；据此说明常向量场所做的功与路径无关，并求反向积分。
\end{problem}

\begin{problem}{403}{72}{折点路径与全微分}
设 $L$ 为圆锥面 $z=\sqrt{x^2+y^2}$ 与平面 $y=x$ 的交线上从 $A(1,1,\sqrt2)$ 经原点到 $B(-1,-1,\sqrt2)$ 的曲线弧。
说明 $L$ 在原点处的光滑性，并分别用分段参数法和全微分法计算
$\int_Lyz\,\dd x+zx\,\dd y+xy\,\dd z$。
\end{problem}

\begin{problem}{404}{72}{有向单位切向量}
设 $L$ 是圆周 $x^2+y^2=2y$ 上从原点到 $(0,2)$ 的右半圆弧，$P,Q$ 连续。

{}
51


## tool · 2026-10-19T23:49:58Z


Script completed
Wall time 0.1 seconds
Output:


\begin{problem}{405}{72}{两类曲线积分与方向}
设 $L$ 为 $x=t,y=t^2,z=t^3$ 上 $t$ 从 $1$ 变到 $0$ 的曲线弧，弧长为 $a$。
不用求出 $a$ 的具体数值，计算
\[
 \int_L\frac{\dd x+2x\,\dd y+3y\,\dd z}{\sqrt{1+4x^2+9y^2}}.
\]
再将三个坐标微分的系数解释为沿正参数方向的单位切向量分量，说明取向如何决定结果。
\end{problem}

\begin{problem}{406}{72}{抛物线弧上的积分转换}
设 $f$ 连续，$L$ 为 $y=x^2$ 上从 $(1,1)$ 到 $(0,0)$ 的曲线弧。
\begin{enumerate}[label=(\arabic*)]
\item 把 $I=\int_L f(x,y)\,\dd x+2xf(x,y)\,\dd y$ 转化为对弧长的积分，写明符号的来源。
\item 当 $f(x,y)=1/(x^2+3y+1)$ 时计算 $I$。
\item 当 $f$ 在 $L$ 上非负时，判断 $I$ 的符号；给出等号成立的条件。
\end{enumerate}
\end{problem}

{}
84


## tool · 2026-10-19T23:51:17Z


Script completed
Wall time 0.1 seconds
Output:

\end{enumerate}
\end{problem}

\begin{problem}{438}{78}{全微分方程逐项判定}
分别判断下列方程是否为全微分方程，写出偏导数依据，并求其中全微分方程的隐式通解：
\begin{enumerate}[label=(\arabic*)]
\item $(x^2+y)\,\dd x-x\,\dd y=0$；
\item $(e^y-x)\,\dd x+(y+e^x)\,\dd y=0$；
\item $\sin x\cos y\,\dd x+\cos x\sin y\,\dd y=0$；
\item $xy\,\dd x+(x^2+y^2)\,\dd y=0$。
\end{enumerate}
\end{problem}

\begin{problem}{439}{78}{全微分方程与初始等值线}
分别求下列方程的隐式通解，以及经过指定点的等值线方程，并检验所求原函数：
\begin{enumerate}[label=(\arabic*)]
\item $(xy^2-2x+y)\,\dd x-(2y-x-x^2y)\,\dd y=0$，指定点 $(0,1)$；
\item $(x^2+e^{-3y})\,\dd x+(y-3xe^{-3y})\,\dd y=0$，指定点 $(1,0)$。
\end{enumerate}
\end{problem}
设 $a,b>0$，$D_{a,b}=\{0\leq x+y\leq a,0\leq x-y\leq b\}$。求
$\iint_{D_{a,b}}(x+y)\sin(x-y)\,\dd x\dd y$，给出 $a=b=\pi$ 的结果。写出正、逆变换及雅可比绝对值，并解释为何不能遗漏该因子。
\end{problem}

\begin{problem}{324}{54}{椭圆变换与幂参数}
设 $a,b>0$，$p\geq0$，$D=\{x^2/a^2+y^2/b^2\leq1\}$。求
$\iint_D(x^2/a^2+y^2/b^2)^p\,\dd x\dd y$，分别给出 $p=0,1$ 的结果，并从中求原二次函数在椭圆内的平均值。
\end{problem}

\begin{problem}{325}{54}{和与比值变量的变换}
设 $D=\{x\geq0,y\geq0,x+y\leq1\}$。在原点给 $e^{x/(x+y)}$ 任意有限值。用 $u=x+y,v=x/(x+y)$ 计算积分，并求以该函数为面密度时的总质量及 $x+y$ 的加权平均值；说明变换在原点失效是否影响结果。
\end{problem}

\begin{problem}{326}{54}{幂乘积变换与区域面积}
设 $D$ 为第一象限内由 $xy=4,xy=8,xy^3=5,xy^3=15$ 围成的闭区域。取 $u=xy,v=xy^3$，证明逆变换在相应矩形内唯一，求雅可比绝对值并计算 $D$ 的面积；再求 $\iint_Dxy\,\dd x\dd y$。
\end{problem}

\begin{problem}{327}{54}{菱形域的积分恒等式}
设 $f$ 在 $[-1,1]$ 上连续，$D=\{|x|+|y|\leq1\}$。证明
$\iint_Df(x+y)\,\dd x\dd y=\int_{-1}^1f(u)\,\dd u$。
进一步设 $g$ 也连续，推导 $\iint_Df(x+y)g(x-y)\,\dd x\dd y$ 的乘积公式，并检验 $f=g\equiv1$ 时的面积。
\end{problem}

\begin{problem}{328}{54}{无界曲边区域的收敛性}
设 $D=\{(x,y):x\geq0,4x^2\leq y\leq9x^2\}$。先以 $0\leq y\leq R$ 截断，计算 $\iint_Dxe^{-y^2}\,\dd x\dd y$ 并证明其收敛；再判断将 $e^{-y^2}$ 换为 $1$ 后积分是否收敛。
\end{problem}

\begin{problem}{329}{54}{无界扇形上的高斯积分}
设 $\alpha>0$。证明并计算
$I(\alpha)=\int_0^{+\infty}\dd x\int_x^{\sqrt3x}e^{-\alpha(x^2+y^2)}\,\dd y$，给出 $I(1)$；利用平面缩放独立说明 $I(\alpha)$ 与 $\alpha$ 的关系。
\end{problem}

\subsection{三重积分}

\begin{problem}{331}{55}{空间区域与幂函数积分}
设 $\Omega=\{(x,y,z):0\leq y\leq x\leq1,\ 0\leq z\leq xy\}$。
写出先对 $z$ 积分与先对 $y$ 积分的两种累次积分，计算
$\iiint_\Omega xy^2z^3\,\dd x\dd y\dd z$，并说明曲面 $z=xy$ 与 $z=0$ 如何确定区域的下边界 $y=0$。
\end{problem}

\begin{problem}{332}{55}{三重积分的次序选择}
设 $\Omega=\{(x,y,z):0\leq x\leq\pi/2,\ 0\leq y\leq\sqrt{x},\ 0\leq z\leq\pi/2-x\}$。
将 $\sin x/x$ 在 $x=0$ 处作连续延拓，计算
\[
 \iiint_\Omega\frac{y\sin x}{x}\,\dd x\dd y\dd z,
\]
并解释先对 $y,z$ 积分为何能消去分母 $x$ 带来的计算困难。
\end{problem}

\begin{problem}{333}{55}{椭球截面与参数积分}
设 $0<h\leq3$，$\Omega_h=\{(x,y,z):x^2+y^2/4+z^2/9\leq1,\ 0\leq z\leq h\}$。

{}
120


## tool · 2026-10-19T23:51:33Z




## tool · 2026-10-19T23:52:06Z


Script completed
Wall time 0.2 seconds
Output:

设 $a>0$，$D_a=\{(x,y):x^2+y^2\leq ax\}$。求 $\iint_{D_a}(x+y^2)\,\dd x\dd y$，给出 $a=1$ 的结果；分别用平移圆心后的对称性确定两个分项的缩放次数。
\end{problem}

\begin{problem}{320}{53}{圆域积分方程的可解性}
设 $D=\{(x,y):x^2+y^2\leq y,x\geq0\}$，$\lambda\in\mathbb R$。讨论连续函数方程
\[
 f(x,y)=\sqrt{1-x^2-y^2}-\lambda\iint_Df(u,v)\,\dd u\dd v
\]
的存在性与唯一性，存在时求其解；给出 $\lambda=8/\pi$ 的结果。必须算出区域面积及根式项的积分。
\end{problem}

\begin{problem}{321}{53}{最小值函数与径向分区}
设 $D=\{x^2+y^2\leq3/16\}$。求两函数 $\sqrt{3/16-x^2-y^2}$ 与 $2(x^2+y^2)$ 在 $D$ 内的相等点集，计算其最小值的二重积分；再利用“最小值加最大值等于两者之和”求最大值的积分。
\end{problem}

\begin{problem}{322}{53}{绝对值与挖去圆盘}
设 $D=\{(x,y):x^2+y^2\geq x,|x|\leq1,|y|\leq1\}$。把 $D$ 解释为正方形挖去一个圆盘后的区域，求 $\iint_D|xy|\,\dd x\dd y$；同时求 $\iint_Dxy\,\dd x\dd y$，说明两个积分能否使用相同的奇偶性结论。
\end{problem}

\begin{problem}{323}{54}{线性变换与雅可比}
设 $a,b>0$，$D_{a,b}=\{0\leq x+y\leq a,0\leq x-y\leq b\}$。求
设 $f$ 在 $[-1,1]$ 上连续，$D=\{|x|+|y|\leq1\}$。证明
$\iint_Df(x+y)\,\dd x\dd y=\int_{-1}^1f(u)\,\dd u$。
进一步设 $g$ 也连续，推导 $\iint_Df(x+y)g(x-y)\,\dd x\dd y$ 的乘积公式，并检验 $f=g\equiv1$ 时的面积。
\end{problem}

\begin{problem}{328}{54}{无界曲边区域的收敛性}
设 $D=\{(x,y):x\geq0,4x^2\leq y\leq9x^2\}$。先以 $0\leq y\leq R$ 截断，计算 $\iint_Dxe^{-y^2}\,\dd x\dd y$ 并证明其收敛；再判断将 $e^{-y^2}$ 换为 $1$ 后积分是否收敛。
\end{problem}

\begin{problem}{329}{54}{无界扇形上的高斯积分}
设 $\alpha>0$。证明并计算
$I(\alpha)=\int_0^{+\infty}\dd x\int_x^{\sqrt3x}e^{-\alpha(x^2+y^2)}\,\dd y$，给出 $I(1)$；利用平面缩放独立说明 $I(\alpha)$ 与 $\alpha$ 的关系。
\end{problem}

\subsection{三重积分}

\begin{problem}{331}{55}{空间区域与幂函数积分}
设 $\Omega=\{(x,y,z):0\leq y\leq x\leq1,\ 0\leq z\leq xy\}$。
写出先对 $z$ 积分与先对 $y$ 积分的两种累次积分，计算
$\iiint_\Omega xy^2z^3\,\dd x\dd y\dd z$，并说明曲面 $z=xy$ 与 $z=0$ 如何确定区域的下边界 $y=0$。
output/宋浩下册工科数学分析改编/chapters/ch10.tex:2:\subsection{二重积分的概念与性质}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:104:\subsection{二重积分的计算方法}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:387:\subsection{三重积分}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:464:\subsection{重积分的应用}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:2:\subsection{对弧长的曲线积分}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:118:\subsection{对坐标的曲线积分}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:238:\subsection{格林公式及其应用}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:239:\subsubsection{封闭曲线、补线与奇点}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:296:\subsubsection{路径无关、原函数与全微分方程}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:393:\subsection{曲线积分的应用}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:439:\subsubsection{综合提高题}

{}
100


## tool · 2026-10-19T23:52:51Z


Script completed
Wall time 0.1 seconds
Output:

\end{problem}

\begin{problem}{270}{47}{对称性与圆域积分}
设 $D=\{(x,y):x^2+y^2\leq1\}$。不先作二次积分，利用对称性求
\[
 \iint_D(x^2+2y)\,\dd x\dd y,
\]
并求 $\iint_D(ax^2+by^2+cxy+dy)\,\dd x\dd y$，其中 $a,b,c,d$ 为实常数。
\end{problem}

\subsection{二重积分的计算方法}
\subsubsection{积分区域与交换积分次序}

\begin{problem}{271}{47}{交换积分次序与计算}
设 $f$ 在 $D=\{(x,y):0\leq x\leq4,\ x\leq y\leq2\sqrt{x}\}$ 上连续。
把 $\int_0^4\dd x\int_x^{2\sqrt{x}}f(x,y)\,\dd y$ 改写成先对 $x$ 积分的累次积分，并用所得表达式计算 $f(x,y)=y$ 时的积分。
\end{problem}

\begin{problem}{329}{54}{无界扇形上的高斯积分}
设 $\alpha>0$。证明并计算
$I(\alpha)=\int_0^{+\infty}\dd x\int_x^{\sqrt3x}e^{-\alpha(x^2+y^2)}\,\dd y$，给出 $I(1)$；利用平面缩放独立说明 $I(\alpha)$ 与 $\alpha$ 的关系。
\end{problem}

\begin{problem}{330}{55}{第一象限反常积分的参数界限}
设 $p\in\mathbb R$，以半径 $R$ 的第一象限圆盘递增截断定义
$I(p)=\iint_{x,y\geq0}(1+x^2+y^2)^{-p}\,\dd x\dd y$。
求积分收敛的全部 $p$ 及收敛时的值；特别证明 $I(2)=\pi/4$，并分别说明临界值与临界值以下的发散情形。
\end{problem}

\subsection{三重积分}

\begin{problem}{331}{55}{空间区域与幂函数积分}
设 $\Omega=\{(x,y,z):0\leq y\leq x\leq1,\ 0\leq z\leq xy\}$。
写出先对 $z$ 积分与先对 $y$ 积分的两种累次积分，计算
$\iiint_\Omega xy^2z^3\,\dd x\dd y\dd z$，并说明曲面 $z=xy$ 与 $z=0$ 如何确定区域的下边界 $y=0$。
\end{problem}

\begin{problem}{332}{55}{三重积分的次序选择}
设 $\Omega=\{(x,y,z):0\leq x\leq\pi/2,\ 0\leq y\leq\sqrt{x},\ 0\leq z\leq\pi/2-x\}$。

\begin{problem}{354}{61}{抛物面下立体的轴惯量}
设 $a,\rho>0$，$\Omega=\{(x,y,z):|x|\leq a,|y|\leq a,0\leq z\leq x^2+y^2\}$，体密度为 $\rho$。求质量及关于 $z$ 轴的转动惯量，给出惯量与质量之比，并检验其量纲。
\end{problem}

\begin{problem}{355}{62}{圆柱体的轴向引力}
设 $R,h>0$，均匀圆柱体 $\Omega=\{x^2+y^2\leq R^2,0\leq z\leq h\}$ 的体密度为 $1$，引力常数为 $G$。求其对 $M_0(0,0,a)$（$a>h$）处单位质量质点的引力向量；先用对称性确定方向，再计算非零分量，并检验 $a\to+\infty$ 时引力大小与 $G\pi R^2h/a^2$ 的比值。
\end{problem}

{}
2:\subsection{二重积分的概念与性质}
104:\begin{supplement}{10.1-1}{保号性与中值定理的条件}
107:\end{supplement}
109:\begin{supplement}{10.1-2}{双矩积分方程的全部参数分支}
115:\end{supplement}
117:\subsection{二重积分的计算方法}
118:\subsubsection{积分区域与交换积分次序}
175:\subsubsection{直角坐标计算与分区}
301:\subsubsection{极坐标与圆形边界}
376:\subsubsection{一般换元与无界积分}
417:\begin{supplement}{10.2-1}{换元区域与雅可比的双重核查}
419:\end{supplement}
421:\begin{supplement}{10.2-2}{圆域奇点的两个临界指数}
428:\end{supplement}
430:\subsection{三重积分}
507:\begin{supplement}{10.3-1}{球冠的坐标范围与截面验证}
509:\end{supplement}
511:\begin{supplement}{10.3-2}{非均匀抛物体的参数质心}
514:\end{supplement}
516:\subsection{重积分的应用}
562:\begin{supplement}{10.4-1}{曲面面积的投影因子与边界极限}
565:\end{supplement}
567:\begin{supplement}{10.4-2}{椭圆薄片的非对称密度与中心惯量}
570:\end{supplement}


## tool · 2026-10-19T23:53:26Z


Script completed
Wall time 0.2 seconds
Output:


\begin{problem}{380}{67}{封闭边界与线密度质量}
设 $L$ 为直线 $y=2x$ 与抛物线 $y^2=x$ 围成区域的完整边界。求两交点，分段计算 $\oint_Ly\,\dd s$；把 $y$ 视为线密度时，求两段细丝的质量比例，并说明端点密度为零是否妨碍总质量为正。
\end{problem}

\begin{problem}{381}{68}{折线上的弧长积分}
设 $L$ 为顶点 $O(0,0),A(1,0),B(0,1)$ 的三角形边界。分边计算
$\oint_L\frac{x}{1+y}\,\dd s$，并求密度为 $\rho(x,y)=1/(1+y)$ 的三角形细丝的质心横坐标。
\end{problem}

\subsection{对坐标的曲线积分}

\begin{problem}{382}{68}{坐标微分与弧长微分}
设 $L$ 为从 $(c,a)$ 到 $(c,b)$ 的有向线段，其中 $a<b$，$P,Q$ 连续。求
$\int_LP(x,y)\,\dd x$ 和 $\int_LQ(x,y)\,\dd y$ 的一元积分表达式；再取 $P\equiv1$，比较 $\int_LP\,\dd x$ 与 $\int_LP\,\dd s$。
\]
再将三个坐标微分的系数解释为沿正参数方向的单位切向量分量，说明取向如何决定结果。
\end{problem}

\begin{problem}{406}{72}{抛物线弧上的积分转换}
设 $f$ 连续，$L$ 为 $y=x^2$ 上从 $(1,1)$ 到 $(0,0)$ 的曲线弧。
\begin{enumerate}[label=(\arabic*)]
\item 把 $I=\int_L f(x,y)\,\dd x+2xf(x,y)\,\dd y$ 转化为对弧长的积分，写明符号的来源。
\item 当 $f(x,y)=1/(x^2+3y+1)$ 时计算 $I$。
\item 当 $f$ 在 $L$ 上非负时，判断 $I$ 的符号；给出等号成立的条件。
\end{enumerate}
\end{problem}

\subsection{格林公式及其应用}
\subsubsection{封闭曲线、补线与奇点}

\begin{problem}{407}{73}{闭曲线积分与全微分}
设 $L$ 为任意分段光滑有向闭曲线。求 $\oint_L(y-\cos x)\,\dd x+(x+\sin y)\,\dd y$，并找出原函数；说明即使闭曲线自交，原函数法是否仍然适用。
\end{problem}

\begin{problem}{439}{78}{全微分方程与初始等值线}
分别求下列方程的隐式通解，以及经过指定点的等值线方程，并检验所求原函数：
\begin{enumerate}[label=(\arabic*)]
\item $(xy^2-2x+y)\,\dd x-(2y-x-x^2y)\,\dd y=0$，指定点 $(0,1)$；
\item $(x^2+e^{-3y})\,\dd x+(y-3xe^{-3y})\,\dd y=0$，指定点 $(1,0)$。
\end{enumerate}
\end{problem}

\subsection{曲线积分的应用}

\begin{problem}{440}{78}{变限积分曲线的弧长}
设 $0<b<\pi/2$，$L_b:y=\int_0^x\tan t\,\dd t$（$0\leq x\leq b$）。求弧长 $s(b)$，给出 $b=\pi/4$ 的结果，并讨论 $b\to\pi/2^-$ 时弧长是否有有限极限。
\end{problem}

\begin{problem}{441}{78}{空间螺旋弧的长度与位移}
设 $T>0$，$\Gamma:x=e^t\cos t,y=e^t\sin t,z=e^t$（$0\leq t\leq T$）。求弧长并给出 $T=1$ 的结果；计算两端点距离，证明它严格小于弧长，并说明等号为何不可能成立。
\begin{problem}{449}{80}{中心回复力与椭圆路径}
设 $a,b,k>0$，$\bm F(x,y)=-k(x,y)$。质点沿椭圆 $x^2/a^2+y^2/b^2=1$，从 $(-a,0)$ 顺时针移动至 $(0,b)$。求功并讨论其正负；若沿同椭圆反方向到达相同终点，功是否改变？给出原函数依据。
\end{problem}

\begin{problem}{450}{81}{径向斥力与平面距离}
设力方向背离原点，大小为 $k/|z|$，$k>0$。质点沿 $x=at,y=bt,z=ct$（$c\ne0$）从 $t=1$ 移动到 $t=2$。求功，分别核查 $c>0,c<0$ 的表达式；再把终点改为 $t=\lambda>1$，求功关于 $\lambda$ 的关系。
\end{problem}

\subsubsection{综合提高题}

\begin{problem}{451}{81}{边界互换对称性}
设 $L$ 为 $y=x^3$ 与 $y=\sqrt[3]x$ 在第一象限围成区域的完整边界。求 $\oint_L(x-y)^{15}\,\dd s$，并证明将 $15$ 换成任意正奇数结论不变；说明此处不需要指定边界方向的原因。

{}
2:\subsection{对弧长的曲线积分}
118:\begin{supplement}{11.1-1}{弧长平均值与平方积分}
122:\end{supplement}
124:\begin{supplement}{11.1-2}{圆形细丝的非均匀密度}
127:\end{supplement}
129:\subsection{对坐标的曲线积分}
249:\begin{supplement}{11.2-1}{非单调参数与重复经过的弧段}
252:\end{supplement}
254:\begin{supplement}{11.2-2}{路径族与保守场参数}
258:\end{supplement}
260:\subsection{格林公式及其应用}
261:\subsubsection{封闭曲线、补线与奇点}
318:\subsubsection{路径无关、原函数与全微分方程}
415:\begin{supplement}{11.3-1}{环域上的局部条件与全局原函数}
419:\end{supplement}
421:\begin{supplement}{11.3-2}{只检验圆周能否判断路径无关}
428:\end{supplement}
430:\subsection{曲线积分的应用}
476:\begin{supplement}{11.4-1}{细丝惯量的平行轴公式及密度条件}
481:\end{supplement}
483:\begin{supplement}{11.4-2}{半圆细丝的质心与旋转力功}
487:\end{supplement}
489:\subsubsection{综合提高题}


## tool · 2026-10-19T23:59:24Z


Script completed
Wall time 0.5 seconds
Output:

from pathlib import Path
import re
import sympy as s

x, y, z, h, t = s.symbols('x y z h t', real=True)

def same(actual, expected):
    assert s.simplify(actual - expected) == 0, (actual, expected)

same(s.integrate(s.integrate(x*y, (y, 0, x)), (x, 0, 1)), s.Rational(1, 8))
same(s.integrate(y+2-y*y, (y, -1, 2)), s.Rational(9, 2))
area274 = s.integrate(2*y, (y, 0, 1)) + s.integrate(3-y, (y, 1, 3))
moment274 = s.integrate(2*y*y, (y, 0, 1)) + s.integrate(y*(3-y), (y, 1, 3))
same(area274, 3)
same(moment274 / area274, s.Rational(4, 3))
same(s.integrate((y*y-y)**2/2, (y, 1, 2)), s.Rational(31, 60))
same(s.integrate(y*y-y, (y, 1, 2)) + s.integrate(8-x, (x, 2, 8)), s.Rational(113, 6))
same(s.integrate(s.integrate(s.integrate(x*y*y*z**3, (z, 0, x*y)), (y, 0, x)), (x, 0, 1)), s.Rational(1, 364))
same(s.integrate((s.pi/2-x)*s.sin(x)/2, (x, 0, s.pi/2)), s.pi/4-s.Rational(1, 2))
j333 = s.integrate(2*s.pi*z*z*(1-z*z/9), (z, 0, h))
same(j333.subs(h, 1), 28*s.pi/45)
same(s.diff(j333, h), 2*s.pi*h*h*(1-h*h/9))
mass381 = 1 + s.integrate(1/(1+y), (y, 0, 1)) + s.sqrt(2)*s.integrate(1/(1+y), (y, 0, 1))
moment381 = s.Rational(1, 2) + s.sqrt(2)*s.integrate((1-y)/(1+y), (y, 0, 1))
same(mass381, 1+(1+s.sqrt(2))*s.log(2))
same(moment381, s.Rational(1, 2)+s.sqrt(2)*(2*s.log(2)-1))
same(s.integrate((1+4*x*x)/(x*x+3*x*x+1), (x, 1, 0)), -1)
print('Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406')

a, c = s.symbols('a c', positive=True)
same(s.integrate(s.integrate(x*x+y*y-x, (x, y/2, y)), (y, 0, a)), a**3*(19*a-12)/96)
same(s.integrate(y*y*y*s.exp(y*y)/2, (y, 0, 1)), s.Rational(1, 4))
same(s.integrate(y*y/(2*s.sqrt(1+y**3)), (y, 0, a)), (s.sqrt(1+a**3)-1)/3)
same(s.integrate(1/s.Symbol('u', positive=True), (s.Symbol('u', positive=True), 1, 2)), s.log(2))
same(s.integrate(s.Rational(1, 2)-c*x*x+c*c*x**4, (x, -1, 1)), 1-2*c/3+2*c*c/5)
max304 = s.integrate(2*c, (x, 0, c/2)) + s.integrate(c*c/(2*x)+2*x, (x, c/2, 2))
same(max304, 4+3*c*c/4+c*c*s.log(4/c)/2)
same(s.integrate(16*(x+y)*x*y, (y, 0, 1-x), (x, 0, 1)), s.Rational(8, 15))
same(s.integrate(16*x*y, (y, 0, 1-x), (x, 0, 1)), s.Rational(2, 3))
r = s.symbols('r', nonnegative=True)
split321 = s.sqrt(2)/4
same(s.sqrt(s.Rational(3, 16)-split321**2), 2*split321**2)
u, v = s.symbols('u v', positive=True)
xx, yy = u**s.Rational(3, 2)/s.sqrt(v), s.sqrt(v/u)
jac326 = s.det(s.Matrix([[s.diff(xx,u),s.diff(xx,v)],[s.diff(yy,u),s.diff(yy,v)]]))
same(jac326, 1/(2*v))
mass348 = s.integrate(x*x*y, (y,x*x,x), (x,0,1))
x348 = s.integrate(x**3*y, (y,x*x,x), (x,0,1))/mass348
same(x348, s.Rational(35,48))
mass349 = 2*s.pi*s.integrate(s.sin(t)*s.cos(t)**5/5,(t,0,s.pi/2))
moment349 = 2*s.pi*s.integrate(s.sin(t)*s.cos(t)**7/6,(t,0,s.pi/2))
same(moment349/mass349, s.Rational(5,8))
print('Additional checks passed: 289, 297, 298, 299, 303, 304, 306, 321, 326, 348, 349')

for chapter in (10, 11):
    path = Path(f'output/宋浩下册工科数学分析改编/chapters/ch{chapter}.tex')
    text = path.read_text()
    numbers = [int(number) for number in re.findall(r'\\begin\{problem\}\{(\d+)\}', text)]
    assert numbers == sorted(set(numbers)), (chapter, numbers)
    assert text.count(r'\begin{problem}') == text.count(r'\end{problem}')
    print(f'Chapter {chapter}: {len(numbers)} unique, ordered problem environments')

{}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Additional checks passed: 289, 297, 298, 299, 303, 304, 306, 321, 326, 348, 349
Traceback (most recent call last):
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 62, in <module>
    same(s.diff(center103,lam), 3/(2*(2*lam+3)**2))
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 9, in same
    assert s.simplify(actual - expected) == 0, (actual, expected)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AssertionError: (-(lam/4 + 1/3)/(3*(lam/3 + 1/2)**2) + 1/(4*(lam/3 + 1/2)), 3/(2*(2*lam + 3)**2))


## tool · 2026-10-19T23:59:33Z


Script completed
Wall time 0.6 seconds
Output:

same(moment349/mass349, s.Rational(5,8))
print('Additional checks passed: 289, 297, 298, 299, 303, 304, 306, 321, 326, 348, 349')

same(s.integrate(1/s.sqrt(1+t*t), (t,1,a)), s.asinh(a)-s.asinh(1))
lam = s.symbols('lam', real=True)
matrix101 = s.eye(2)-lam*s.Matrix([[s.Rational(1,3),s.Rational(1,4)],[s.Rational(1,4),s.Rational(1,3)]])
same(matrix101.det(), (1-7*lam/12)*(1-lam/12))
same(s.integrate(s.pi*(1-z*z), (z,h,1)), s.pi*(s.Rational(2,3)-h+h**3/3))
center103 = (s.Rational(1,3)+lam/4)/(s.Rational(1,2)+lam/3)
same(s.diff(center103,lam), 3/(2*(2*lam+3)**2))
same(s.integrate(s.cos(t)**2, (t,0,2*s.pi)), s.pi)
same(s.integrate((s.cos(t)+s.sin(t))**2, (t,0,2*s.pi)), 2*s.pi)
same(s.integrate(2*x*s.sqrt(1+4*x*x),(x,0,1)), (5*s.sqrt(5)-1)/6)
same(s.integrate(s.cos(t)**2*s.sin(t), (t,0,s.pi)), s.Rational(2,3))
same(s.integrate(s.sin(t)**3, (t,0,s.pi)), s.Rational(4,3))
same(s.integrate(s.cos(t)**4, (t,0,2*s.pi)), 3*s.pi/4)

same(s.integrate(2*x*x,(x,-1,1)), s.Rational(4,3))
same(s.integrate((1+x*x)*s.cos(x)**2,(x,0,1)), s.Rational(2,3)+s.sin(2)/4+s.cos(2)/4)
same(s.integrate(s.sin(t)**2,(t,0,2*s.pi)), s.pi)
same(s.integrate(s.sqrt(2)*(s.cos(t)-s.sin(t)),(t,0,s.pi/4)), 2-s.sqrt(2))
same(s.integrate(s.sqrt(3)*s.exp(-t)/2,(t,0,2)), s.sqrt(3)*(1-s.exp(-2))/2)
same(s.integrate(1+3*s.sin(t)**2,(t,0,s.pi)), 5*s.pi/2)

param396 = [s.cos(t),s.sin(t),1-s.cos(t)]
field396 = [param396[1]*param396[2],-param396[0],-param396[1]]

{}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Additional checks passed: 289, 297, 298, 299, 303, 304, 306, 321, 326, 348, 349
Traceback (most recent call last):
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 79, in <module>
    same(ccw396, -2*s.pi)
  File "/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/songhao/check_10_11.py", line 9, in same
    assert s.simplify(actual - expected) == 0, (actual, expected)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AssertionError: (-3*pi, -2*pi)


## tool · 2026-10-20T00:16:08Z




## tool · 2026-10-20T00:16:13Z


Script completed
Wall time 0.1 seconds
Output:

% !TeX program = xelatex
\documentclass[12pt,fontset=fandol]{ctexrep}
\usepackage{amsmath,amssymb,geometry,fancyhdr,xcolor,hyperref,catchfile}
\geometry{paperwidth=240mm,paperheight=180mm,left=14mm,right=14mm,top=14mm,bottom=11mm,headheight=14pt,headsep=6pt,footskip=17pt}
\setlength{\parindent}{0pt}
\setlength{\parskip}{5pt}
\raggedbottom
\definecolor{muted}{gray}{0.38}
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\small\color{muted}工科数学分析基础 · 第四版上册}
\fancyfoot[C]{\small\color{muted}\thepage}
\renewcommand{\headrulewidth}{0pt}
\renewcommand{\footrulewidth}{0pt}
\hypersetup{hidelinks,bookmarksopen=false,bookmarksdepth=3,pdftitle={分节课后练习：标准极限横屏版},pdfauthor={原创补充练习},pdfdisplaydoctitle=true}
\newcounter{ipadquestion}
\newcommand{\ipadchapter}{}
\newcommand{\ipadsection}{}
\newcommand{\ipadsubsection}{}
\newcommand{\knowledge}[3]{%
  \expandafter\gdef\csname ipadknowledge@#1\endcsname{%
    \vspace{3mm}{\large\bfseries 重要知识点}\par #2\par
    \vspace{3mm}{\large\bfseries 需要掌握}\par #3\par}}
\input{分节知识点.tex}
\renewcommand{\chapter}[1]{%
  \clearpage\refstepcounter{chapter}\gdef\ipadchapter{#1}%
  \pdfbookmark[0]{第\thechapter 章 #1}{ipad.chapter.\thechapter}}
\renewcommand{\section}[1]{%
  \clearpage\refstepcounter{section}\gdef\ipadsection{#1}%
  \pdfbookmark[1]{\thesection\space #1}{ipad.section.\thesection}}
\renewcommand{\subsection}[1]{%
  \clearpage\refstepcounter{subsection}\gdef\ipadsubsection{#1}%
  \pdfbookmark[2]{\thesubsection\space #1}{ipad.subsection.\thesubsection}%
  {\small\color{muted}第\thechapter 章\quad\ipadchapter\quad /\quad\ipadsection\par}
  \vspace{3mm}{\fontsize{20}{27}\selectfont\bfseries\thesubsection\quad #1\par}}
\newcommand{\goal}[1]{%
  {\color{muted}本节线索：#1\par}%
  \ifcsname ipadknowledge@\thesubsection\endcsname
    \csname ipadknowledge@\thesubsection\endcsname
  \else
    \PackageError{ipad}{Missing knowledge for \thesubsection}{Add the section to the knowledge file.}%
  \fi}
\newcommand{\ipaditem}{%
  \clearpage\stepcounter{ipadquestion}%
  \pdfbookmark[3]{\thesubsection-\arabic{ipadquestion} 第\arabic{ipadquestion}题}{ipad.question.\thesubsection.\arabic{ipadquestion}}%
  {\small\color{muted}\thesubsection\quad\ipadsubsection\hfill 题号 \thesubsection-\arabic{ipadquestion}\par}%
  \vspace{3mm}{\large\bfseries 第\arabic{ipadquestion}题\par}\vspace{2mm}}
\renewenvironment{enumerate}{\setcounter{ipadquestion}{0}\let\item\ipaditem}{\par}
% 直接读取题源，保证横屏版与题目源文件保持一致。
\CatchFileDef{\originalpractice}{分节课后练习.tex}{}
\long\def\printpractice#1\chapter#2\stoppractice{\chapter#2}
\begin{document}
\fontsize{14}{21}\selectfont
\thispagestyle{empty}
\begin{center}
\vspace*{9mm}
{\fontsize{27}{36}\selectfont\bfseries 工科数学分析基础\par}
\vspace{4mm}
{\fontsize{22}{30}\selectfont 第四版上册 · 分节课后练习\par}
\vspace{5mm}
{\Large 标准极限横屏版\par}
\vspace{5mm}
4:3 横屏\quad 每页一道题\quad 下方空白草稿区\par
85个小节知识清单\quad 425道原创补充练习\par
\end{center}
\vspace{5mm}
{\fontsize{11}{17}\selectfont
每小节先复习知识点与掌握要求，再独立完成5道题。题号沿用原题册，答案请查阅同目录的独立答案册。

极限均使用带趋近条件的$\lim$记号，数学比值采用上下分数。正文中的“第1题”“上一题”均指当前小节，可通过PDF书签跳转。$n$默认为正整数，$\ln$为自然对数，积分中的$C$为任意常数。

依据马知恩、王绵森主编教材第四版上册的章节编写。星号内容及第4章按教师授课进度选做；覆盖范围不代表考试范围。建议导入支持PDF手写批注的应用，横向整页显示后书写。\par}
\expandafter\printpractice\originalpractice\stoppractice
% !TeX program = xelatex
\documentclass[11pt,a4paper,fontset=fandol]{ctexart}
\usepackage[margin=23mm]{geometry}
\usepackage{amsmath,amssymb,bm,enumitem,hyperref}
\hypersetup{hidelinks,pdftitle={工科数学分析逐题训练}}
\setlist[enumerate]{label=（\arabic*）,leftmargin=2.6em,itemsep=0.25em}
\newcommand{\dd}{\,\mathrm{d}}
\newenvironment{problem}[3]{%
  \par\medskip\noindent\textbf{第#1题}\quad\textit{#3}\par
  {\small 原题对应：第#1题，原资料第#2页；PDF第\the\numexpr#2+5\relax 页。}\par\smallskip
}{\par\medskip}
\newenvironment{supplement}[2]{%
  \par\medskip\noindent\textbf{补充#1}\quad\textit{#2}\par\smallskip
}{\par\medskip}
\allowdisplaybreaks
\setcounter{secnumdepth}{-1}
\setlength{\emergencystretch}{2em}
\title{工科数学分析逐题训练\\[0.4em]\large 计算、论证与条件辨析}
\author{}
\date{2026年10月20日}
\begin{document}
\maketitle
\section*{使用说明}
本题册覆盖向量与空间几何、多元微分、重积分、曲线积分、曲面积分及无穷级数。按用户提供题源的第8至13章顺序，逐题保留1至750的编号，重新设计题面，难度按工科数学分析期末考试控制。练习既要求完成计算，也关注条件是否充分、定理能否使用、参数变化对结论的影响。

34节各增设两道递进补充题，共68道，以“补充章.节-序号”单独编号。每节先完成原题对应训练，再练习补充题中的条件辨析与参数综合。全册共818道题，补充题不占用原题编号。

各题标注原题开始所在纸页及PDF页序，PDF封面计为第1页；原资料纸页加5即为本次来源PDF页序。跨页原题的后续小问纳入对应改编题。题目所需函数、区域、参数与方向均在题干中给出，可独立使用。未给出本校考试大纲，具体章目仍以授课要求为准。

本册仅包含改编题目，未附答案；按章节练习使用，不代表某一套试卷的题量或时间安排。证明题可使用工科数学分析课堂已学定理，使用时应说明关键条件。
\tableofcontents
\clearpage
\input{chapters/ch08.tex}
\clearpage
\input{chapters/ch09.tex}
\clearpage
\input{chapters/ch10.tex}
\clearpage
\input{chapters/ch11.tex}
\clearpage
\input{chapters/ch12.tex}
\clearpage
\input{chapters/ch13.tex}
\end{document}
output/宋浩下册工科数学分析改编/对应清单.json
output/宋浩下册工科数学分析改编/使用说明.md
output/宋浩下册工科数学分析改编/main.tex
output/宋浩下册工科数学分析改编/chapters/ch13.tex
output/宋浩下册工科数学分析改编/chapters/ch12.tex
output/宋浩下册工科数学分析改编/chapters/ch10.tex
output/宋浩下册工科数学分析改编/chapters/ch11.tex
output/宋浩下册工科数学分析改编/chapters/ch08.tex
output/宋浩下册工科数学分析改编/chapters/ch09.tex


## tool · 2026-10-20T00:16:34Z


Script completed
Wall time 0.1 seconds
Output:

output/宋浩下册工科数学分析改编/chapters/ch13.tex:1:\section{第13章\quad 无穷级数}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:2:\subsection{常数项级数的概念与性质}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:94:\subsection{正项级数}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:199:\subsection{任意项级数}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:282:\subsection{幂级数}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:349:\subsection{函数展开成幂级数}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:398:\subsection{幂级数的应用}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:435:\subsection{傅里叶级数}
output/宋浩下册工科数学分析改编/chapters/ch13.tex:479:\subsubsection{综合提高题}
output/宋浩下册工科数学分析改编/chapters/ch12.tex:1:\section{第12章\quad 曲面积分}
output/宋浩下册工科数学分析改编/chapters/ch12.tex:2:\subsection{第一类曲面积分}
output/宋浩下册工科数学分析改编/chapters/ch12.tex:77:\subsection{第二类曲面积分}
output/宋浩下册工科数学分析改编/chapters/ch12.tex:175:\subsection{高斯公式}
output/宋浩下册工科数学分析改编/chapters/ch12.tex:263:\subsection{斯托克斯公式}
output/宋浩下册工科数学分析改编/chapters/ch12.tex:309:\subsection{曲面积分的应用}
output/宋浩下册工科数学分析改编/chapters/ch12.tex:367:\subsubsection{综合提高题}
output/宋浩下册工科数学分析改编/chapters/ch08.tex:1:\section{第8章 向量代数与空间解析几何}
output/宋浩下册工科数学分析改编/chapters/ch08.tex:2:\subsection{向量及其线性运算}
output/宋浩下册工科数学分析改编/chapters/ch08.tex:45:\subsection{内积、向量积与混合积}
output/宋浩下册工科数学分析改编/chapters/ch08.tex:97:\subsection{平面方程}
output/宋浩下册工科数学分析改编/chapters/ch08.tex:183:\subsection{空间直线}
output/宋浩下册工科数学分析改编/chapters/ch08.tex:266:\subsection{曲面及其方程}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:1:\section{第11章\quad 曲线积分}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:2:\subsection{对弧长的曲线积分}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:129:\subsection{对坐标的曲线积分}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:260:\subsection{格林公式及其应用}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:261:\subsubsection{封闭曲线、补线与奇点}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:318:\subsubsection{路径无关、原函数与全微分方程}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:430:\subsection{曲线积分的应用}
output/宋浩下册工科数学分析改编/chapters/ch11.tex:489:\subsubsection{综合提高题}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:1:\section{第9章 多元函数微分法及其应用}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:2:\subsection{多元函数的基本概念}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:79:\subsection{偏导数}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:153:\subsubsection{高阶偏导数}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:179:\subsection{全微分}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:245:\subsection{多元复合函数的求导法则}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:321:\subsection{隐函数的求导法则}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:370:\subsubsection{方程组确定的隐函数}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:389:\subsection{多元函数微分法在几何上的应用}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:426:\subsection{方向导数和梯度}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:463:\subsection{多元函数的极值及其应用}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:518:\subsection{二元函数的泰勒公式}
output/宋浩下册工科数学分析改编/chapters/ch09.tex:540:\subsubsection{综合提高题}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:1:\section{第10章\quad 重积分}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:2:\subsection{二重积分的概念与性质}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:117:\subsection{二重积分的计算方法}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:118:\subsubsection{积分区域与交换积分次序}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:175:\subsubsection{直角坐标计算与分区}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:301:\subsubsection{极坐标与圆形边界}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:376:\subsubsection{一般换元与无界积分}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:430:\subsection{三重积分}
output/宋浩下册工科数学分析改编/chapters/ch10.tex:516:\subsection{重积分的应用}
ls: output/宋浩下册工科数学分析改编/ipad.tex: No such file or directory


## tool · 2026-10-20T00:17:18Z


Script completed
Wall time 0.1 seconds
Output:

{}
% !TeX program = xelatex
\documentclass[12pt,fontset=fandol]{ctexart}
\usepackage{geometry,amsmath,amssymb,bm,enumitem,xcolor,hyperref,xparse}
\geometry{paperwidth=240mm,paperheight=180mm,left=14mm,right=14mm,top=12mm,bottom=12mm,noheadfoot}
\hypersetup{hidelinks,pdftitle={工科数学分析逐题训练·横屏手写版},pdfauthor={},bookmarksopen=false,bookmarksdepth=2,pdfdisplaydoctitle=true}
\pdfstringdefDisableCommands{\def\quad{ }\def\qquad{ }}
\pagestyle{empty}
\setlength{\parindent}{0pt}
\setlength{\parskip}{3pt}
\setlength{\emergencystretch}{2em}
\setlist[enumerate]{label=（\arabic*）,leftmargin=2.6em,itemsep=2pt,topsep=3pt,parsep=0pt}
\newcommand{\dd}{\,\mathrm{d}}
\definecolor{ipadmuted}{gray}{0.40}

\ExplSyntaxOn
\msg_new:nnn {ipad} {validation-failed} {#1}
\NewDocumentCommand{\ipadFail}{m}{\msg_fatal:nnn {ipad}{validation-failed}{#1}}
\ExplSyntaxOff

\newcounter{ipadexercise}
\newcounter{ipadchapterid}
\newcounter{ipadsectionid}
\newcounter{ipadshippedpages}
\newif\ifipadchapterpending
\newif\ifipadsectionpending
\newcommand{\ipadchapter}{}
\newcommand{\ipadsection}{}
\newcommand{\ipadtopic}{}
\renewcommand{\section}[1]{%
  \stepcounter{ipadchapterid}\setcounter{ipadsectionid}{0}%
  \gdef\ipadchapter{#1}\gdef\ipadsection{}\gdef\ipadtopic{}%
  \global\ipadchapterpendingtrue\global\ipadsectionpendingfalse}
\renewcommand{\subsection}[1]{%
  \stepcounter{ipadsectionid}\gdef\ipadsection{#1}\gdef\ipadtopic{}%
  \global\ipadsectionpendingtrue}
\renewcommand{\subsubsection}[1]{\gdef\ipadtopic{#1}}
\newcommand{\ipadbookmarks}[2]{%
  \ifipadchapterpending
    \pdfbookmark[0]{\ipadchapter}{ipad.chapter.\arabic{ipadchapterid}}%
    \global\ipadchapterpendingfalse
  \fi
  \ifipadsectionpending
    \pdfbookmark[1]{\ipadsection}{ipad.section.\arabic{ipadchapterid}.\arabic{ipadsectionid}}%
    \global\ipadsectionpendingfalse
  \fi
  \pdfbookmark[2]{第#1题\space #2}{ipad.exercise.#1}}

\newsavebox{\ipadquestionbox}
\newlength{\ipadquestionheight}
\newlength{\ipadminblank}
\newlength{\ipadmaxquestionheight}
\newlength{\ipadremainingblank}
\setlength{\ipadminblank}{70mm}
\setlength{\ipadmaxquestionheight}{\dimexpr\textheight-\ipadminblank\relax}

\NewDocumentEnvironment{exercise}{m m +b}{%
  \clearpage
  \stepcounter{ipadexercise}%
  \ifnum#1=\value{ipadexercise}\relax\else
    \ipadFail{Exercise\space #1\space is\space out\space of\space sequence.}%
  \fi
  \ipadbookmarks{#1}{#2}%
  \begin{lrbox}{\ipadquestionbox}%
    \begin{minipage}[t]{\linewidth}
      \fontsize{12.5}{18}\selectfont
      \setlength{\abovedisplayskip}{5pt}%
      \setlength{\belowdisplayskip}{5pt}%
      \setlength{\abovedisplayshortskip}{3pt}%
      \setlength{\belowdisplayshortskip}{3pt}%
      {\fontsize{9}{12}\selectfont\color{ipadmuted}%
        \ipadchapter\quad /\quad\ipadsection
        \ifx\ipadtopic\empty\else\quad /\quad\ipadtopic\fi\par}
      \vspace{2mm}%
      {\fontsize{14}{19}\selectfont\bfseries 第#1题\quad #2\par}
      \vspace{1mm}%
      #3\par
    \end{minipage}%
  \end{lrbox}%
  \setlength{\ipadquestionheight}{\dimexpr\ht\ipadquestionbox+\dp\ipadquestionbox\relax}%
  \setlength{\ipadremainingblank}{\dimexpr\textheight-\ipadquestionheight\relax}%
  \typeout{IPAD-EXERCISE id=#1 height=\the\ipadquestionheight blank=\the\ipadremainingblank limit=\the\ipadmaxquestionheight}%
  \ifdim\ipadquestionheight>\ipadmaxquestionheight
    \ipadFail{Exercise\space #1\space exceeds\space the\space question\space height\space limit;\space at\space least\space 70mm\space blank\space space\space is\space required.}%
  \fi
  \noindent\usebox{\ipadquestionbox}\par
  \vfill\null
}{}

\AddToHook{shipout/after}{\stepcounter{ipadshippedpages}}
\AtEndDocument{%
  \ifnum\value{ipadexercise}=818\relax\else
    \ipadFail{Expected\space 818\space exercises;\space found\space \arabic{ipadexercise}.}%
  \fi}
\AddToHook{enddocument/afterlastpage}{%
  \typeout{IPAD-TOTAL exercises=\arabic{ipadexercise} pages=\arabic{ipadshippedpages}}%
  \ifnum\value{ipadshippedpages}=818\relax\else
    \ipadFail{Expected\space 818\space pages;\space found\space \arabic{ipadshippedpages}.}%
  \fi}

\begin{document}
\input{chapters/ch08.tex}
\input{chapters/ch09.tex}
\input{chapters/ch10.tex}
\input{chapters/ch11.tex}
\input{chapters/ch12.tex}
\input{chapters/ch13.tex}
\end{document}


## tool · 2026-10-20T00:17:29Z




## tool · 2026-10-20T00:17:32Z


Script completed
Wall time 0.1 seconds
Output:

\section{第8章 向量代数与空间解析几何}
\subsection{向量及其线性运算}
\begin{problem}{1}{2}{线性组合与线性无关}
设 $\vec u=\vec a-\vec b+\vec c$，$\vec v=\vec a+3\vec b-2\vec c$，其中 $\vec a,\vec b,\vec c$ 线性无关。用它们表示 $2\vec u-\vec v$，并判断是否存在实数 $s,t$ 使 $s\vec u+t\vec v=\vec c$，说明理由。
\end{problem}
\begin{problem}{2}{2}{坐标运算与正交条件}
设 $\vec a=(0,-1,1)$，$\vec b=(1,2,0)$，$\vec c=(2,0,1)$。求 $\vec p=\vec a-\vec b+\vec c$、$\vec q=\vec a+2\vec b-3\vec c$ 的坐标，并求使 $\vec p+\lambda\vec q$ 与 $\vec c$ 垂直的实数 $\lambda$。
\end{problem}


## tool · 2026-10-20T00:17:55Z


Script completed
Wall time 0.1 seconds
Output:

\geometry{paperwidth=240mm,paperheight=180mm,left=14mm,right=14mm,top=12mm,bottom=12mm,noheadfoot}
\hypersetup{hidelinks,pdftitle={工科数学分析逐题训练·横屏手写版},pdfauthor={},bookmarksopen=false,bookmarksdepth=2,pdfdisplaydoctitle=true}
\pdfstringdefDisableCommands{\def\quad{ }\def\qquad{ }}
\pagestyle{empty}
\setlength{\parindent}{0pt}
\setlength{\parskip}{3pt}
\setlength{\emergencystretch}{2em}
\setlist[enumerate]{label=（\arabic*）,leftmargin=2.6em,itemsep=2pt,topsep=3pt,parsep=0pt}
\newcommand{\dd}{\,\mathrm{d}}
\definecolor{ipadmuted}{gray}{0.40}

\ExplSyntaxOn
  \clearpage
  \stepcounter{ipadexercise}%
  \ifnum#1=\value{ipadexercise}\relax\else
    \ipadFail{Exercise\space #1\space is\space out\space of\space sequence.}%
  \fi
  \ipadbookmarks{#1}{#2}%
  \begin{lrbox}{\ipadquestionbox}%
    \begin{minipage}[t]{\linewidth}
      \fontsize{12.5}{18}\selectfont
      \setlength{\abovedisplayskip}{5pt}%
      \setlength{\belowdisplayskip}{5pt}%
      \setlength{\abovedisplayshortskip}{3pt}%
      \setlength{\belowdisplayshortskip}{3pt}%
      {\fontsize{9}{12}\selectfont\color{ipadmuted}%
        \ipadchapter\quad /\quad\ipadsection
        \ifx\ipadtopic\empty\else\quad /\quad\ipadtopic\fi\par}
      \vspace{2mm}%
      {\fontsize{14}{19}\selectfont\bfseries 第#1题\quad #2\par}
      \vspace{1mm}%
      #3\par
    \end{minipage}%
  \end{lrbox}%
  \setlength{\ipadquestionheight}{\dimexpr\ht\ipadquestionbox+\dp\ipadquestionbox\relax}%
  \setlength{\ipadremainingblank}{\dimexpr\textheight-\ipadquestionheight\relax}%
  \typeout{IPAD-EXERCISE id=#1 height=\the\ipadquestionheight blank=\the\ipadremainingblank limit=\the\ipadmaxquestionheight}%
  \ifdim\ipadquestionheight>\ipadmaxquestionheight
    \ipadFail{Exercise\space #1\space exceeds\space the\space question\space height\space limit;\space at\space least\space 70mm\space blank\space space\space is\space required.}%
  \fi
  \noindent\usebox{\ipadquestionbox}\par
  \vfill\null
}{}

\AddToHook{shipout/after}{\stepcounter{ipadshippedpages}}

{}
\NewDocumentEnvironment{exercise}{m m +b}{%
  \clearpage
  \stepcounter{ipadexercise}%
  \ifnum#1=\value{ipadexercise}\relax\else
    \ipadFail{Exercise\space #1\space is\space out\space of\space sequence.}%
  \fi
  \begin{lrbox}{\ipadquestionbox}%
    \begin{minipage}[t]{\linewidth}
      \fontsize{12.5}{18}\selectfont
      \setlength{\abovedisplayskip}{5pt}%
      \setlength{\belowdisplayskip}{5pt}%
      \setlength{\abovedisplayshortskip}{3pt}%
      \setlength{\belowdisplayshortskip}{3pt}%
      {\fontsize{9}{12}\selectfont\color{ipadmuted}%
        \ipadbookmarks{#1}{#2}%
        \ipadchapter\quad /\quad\ipadsection
        \ifx\ipadtopic\empty\else\quad /\quad\ipadtopic\fi\par}
      \vspace{2mm}%
      {\fontsize{14}{19}\selectfont\bfseries 第#1题\quad #2\par}
      \vspace{1mm}%
      #3\par
    \end{minipage}%
  \end{lrbox}%
  \setlength{\ipadquestionheight}{\dimexpr\ht\ipadquestionbox+\dp\ipadquestionbox\relax}%
  \setlength{\ipadremainingblank}{\dimexpr\textheight-\ipadquestionheight\relax}%
  \typeout{IPAD-EXERCISE id=#1 height=\the\ipadquestionheight blank=\the\ipadremainingblank limit=\the\ipadmaxquestionheight}%
  \ifdim\ipadquestionheight>\ipadmaxquestionheight
    \ipadFail{Exercise\space #1\space exceeds\space the\space question\space height\space limit;\space at\space least\space 70mm\space blank\space space\space is\space required.}%
  \fi
  \nointerlineskip\box\ipadquestionbox
  \vfill\null
}{}

\AddToHook{shipout/after}{\stepcounter{ipadshippedpages}}


## tool · 2026-10-20T00:17:59Z


Script completed
Wall time 0.1 seconds
Output:

\section{第8章 向量代数与空间解析几何}
\subsection{向量及其线性运算}
\begin{problem}{1}{2}{线性组合与线性无关}
设 $\vec u=\vec a-\vec b+\vec c$，$\vec v=\vec a+3\vec b-2\vec c$，其中 $\vec a,\vec b,\vec c$ 线性无关。用它们表示 $2\vec u-\vec v$，并判断是否存在实数 $s,t$ 使 $s\vec u+t\vec v=\vec c$，说明理由。
.agent/math-analysis/verify_sections.py
.agent/math-analysis/ipad-build/compile-pass-1.txt
.agent/math-analysis/ipad-build/fractions-pass-2.txt
.agent/math-analysis/ipad-build/compile-pass-2.txt
.agent/math-analysis/ipad-build/fractions-pass-1.txt
.agent/math-analysis/ipad-build/header-removal-pass-1.txt
.agent/math-analysis/ipad-build/header-removal-pass-2.txt
.agent/math-analysis/ipad-build/分节课后练习-iPad横屏草稿版.pdf
.agent/math-analysis/ipad-build/verification.json
.agent/math-analysis/ipad-build/分节课后练习-标准极限横屏版.log
.agent/math-analysis/ipad-build/分节课后练习-标准极限横屏版.aux
.agent/math-analysis/ipad-build/standard-limits-verification.json
.agent/math-analysis/ipad-build/standard-limits-pass-2.txt
.agent/math-analysis/ipad-build/分节课后练习-iPad横屏草稿版.out
.agent/math-analysis/ipad-build/standard-limits-pass-1.txt
.agent/math-analysis/verify_sections.py:50:    assert source.startswith("% !TeX program = xelatex\n")
.agent/math-analysis/songhao/check_10_11.py:4:from pylatexenc.latexwalker import LatexWalker
.agent/math-analysis/songhao/check_10_11.py:109:    LatexWalker(text, tolerant_parsing=False).get_latex_nodes()
.agent/math-analysis/songhao/check_collection.py:7:from pylatexenc.latexwalker import LatexEnvironmentNode, LatexMacroNode, LatexWalker, get_default_latex_context_db
.agent/math-analysis/songhao/check_collection.py:8:from pylatexenc.macrospec import EnvironmentSpec
.agent/math-analysis/songhao/check_collection.py:15:CONTEXT = get_default_latex_context_db()
.agent/math-analysis/songhao/check_collection.py:24:    nodes, position, length = LatexWalker(text, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()
.agent/math-analysis/songhao/check_collection.py:64:                arguments = [argument.latex_verbatim()[1:-1] for argument in node.nodeargd.argnlist]
.agent/math-analysis/songhao/check_collection.py:70:                body = ''.join(child.latex_verbatim() for child in node.nodelist).strip()
.agent/math-analysis/songhao/check_collection.py:77:            arguments = [argument.latex_verbatim()[1:-1] for argument in node.nodeargd.argnlist]
.agent/math-analysis/songhao/check_collection.py:81:            body = ''.join(child.latex_verbatim() for child in node.nodelist).strip()
.agent/math-analysis/songhao/check_12_13.py:4:from pylatexenc.latexwalker import LatexWalker, get_default_latex_context_db
.agent/math-analysis/songhao/check_12_13.py:5:from pylatexenc.macrospec import EnvironmentSpec, MacroStandardArgsParser
.agent/math-analysis/songhao/check_12_13.py:45:    context = get_default_latex_context_db()
.agent/math-analysis/songhao/check_12_13.py:50:    nodes, position, length = LatexWalker(source, latex_context=context, tolerant_parsing=False).get_latex_nodes()
.agent/math-analysis/songhao/renumber_plan.py:6:from pylatexenc.latexwalker import LatexEnvironmentNode, LatexWalker, get_default_latex_context_db
.agent/math-analysis/songhao/renumber_plan.py:7:from pylatexenc.macrospec import EnvironmentSpec
.agent/math-analysis/songhao/renumber_plan.py:13:CONTEXT = get_default_latex_context_db()
.agent/math-analysis/songhao/renumber_plan.py:23:    nodes, position, length = LatexWalker(source, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()
.agent/math-analysis/songhao/renumber_plan.py:38:        direction = arguments[-1].latex_verbatim()[1:-1]


## tool · 2026-10-20T00:18:08Z


Script completed
Wall time 0.1 seconds
Output:

ipad.tex: strict LaTeX parse passed


## tool · 2026-10-20T00:18:11Z




## tool · 2026-10-20T00:18:44Z


Wall time: 30.0065 seconds
Sleep completed.

## tool · 2026-10-20T00:19:03Z


Script completed
Wall time 0.1 seconds
Output:

\section{第8章 向量代数与空间解析几何}
\subsection{向量及其线性运算}
\begin{problem}{1}{2}{线性组合与线性无关}
设 $\vec u=\vec a-\vec b+\vec c$，$\vec v=\vec a+3\vec b-2\vec c$，其中 $\vec a,\vec b,\vec c$ 线性无关。用它们表示 $2\vec u-\vec v$，并判断是否存在实数 $s,t$ 使 $s\vec u+t\vec v=\vec c$，说明理由。


## tool · 2026-10-20T00:19:07Z




## assistant · 2026-10-20T00:19:14Z

已新增 [ipad.tex](/Users/oyamahappa/Documents/Agent/Codex/output/宋浩下册工科数学分析改编/ipad.tex)。

- 240×180mm 横屏，正文12.5/18pt，每页一道题。
- 题面完整装盒，至少保留70mm连续空白；超高立即报错。
- 延迟章、节书签及逐题书签；强校验818题、818页。
- pylatexenc 严格解析通过。

未编译完整题册：当前章节尚未转换为 `exercise`。实际题面高度及818页结果需转换后构建确认。

## tool · 2026-10-20T00:20:02Z


Script completed
Wall time 7.3 seconds
Output:

{"content":[{"type":"text","text":"{\"path\":\"/Users/oyamahappa/Documents/Agent/Codex/output/工科数学分析逐题训练\",\"mainDocument\":\"/Users/oyamahappa/Documents/Agent/Codex/output/工科数学分析逐题训练/ipad.tex\",\"kind\":\"success\",\"message\":\"The current source compiled successfully with the desktop editor's compiler.\"}"}],"isError":false}
same(s.integrate(2*x*x,(x,-1,1)), s.Rational(4,3))
same(s.integrate(s.sin(t)**2,(t,0,2*s.pi)), s.pi)
same(s.integrate(s.sqrt(2)*(s.cos(t)-s.sin(t)),(t,0,s.pi/4)), 2-s.sqrt(2))
same(s.integrate(s.sqrt(3)*s.exp(-t)/2,(t,0,2)), s.sqrt(3)*(1-s.exp(-2))/2)
same(s.integrate(1+3*s.sin(t)**2,(t,0,s.pi)), 5*s.pi/2)

param396 = [s.cos(t),s.sin(t),1-s.cos(t)]
field396 = [param396[1]*param396[2],-param396[0],-param396[1]]
ccw396 = s.integrate(sum(field396[i]*s.diff(param396[i],t) for i in range(3)),(t,0,2*s.pi))
same(ccw396, -2*s.pi)
param402 = [2*s.cos(t),1+s.sqrt(2)*s.sin(t),1-s.sqrt(2)*s.sin(t)]
field402 = [param402[2],param402[0],-1]
same(s.integrate(sum(field402[i]*s.diff(param402[i],t) for i in range(3)),(t,0,2*s.pi)),4*s.sqrt(2)*s.pi)
same(s.integrate((2-y)*(y+4-y*y/2),(y,-2,4)),18)
same(s.integrate(5*y**4/(4*c),(y,2,-2)),-16/c)
same(s.integrate(1+t*t+t**4,(t,0,1)),s.Rational(23,15))
same(s.integrate(-t*t+t,(t,0,a)),a*a/2-a**3/3)
same(s.integrate((1+a**3*s.sin(x)**3)-2*a*s.sin(x),(x,0,s.pi)),s.pi+4*a**3/3-4*a)

potential472 = x*x*y*y/2-s.cos(2*x)*s.sin(3*y)/3
same(s.diff(potential472,x),x*y*y+s.Rational(4,3)*s.sin(x)*s.cos(x)*s.sin(3*y))
same(s.diff(potential472,y),x*x*y-s.cos(2*x)*s.cos(3*y))
y474 = x*x/4-s.log(x)/2
same(2*x*s.diff(y474,x)-4*y474,2*s.log(x)-1)
same(1+s.diff(y474,x)**2,(x+1/x)**2/4)
print('New checks passed: 316, supplements, 374, 376, 396, 402, 413, 417, 443, 448, 458, 472, 474')

for chapter in (10, 11):
    path = Path(f'output/宋浩下册工科数学分析改编/chapters/ch{chapter}.tex')
    text = path.read_text()
    numbers = [int(number) for number in re.findall(r'\\begin\{problem\}\{(\d+)\}', text)]
    assert numbers == sorted(set(numbers)), (chapter, numbers)
    expected = list(range(256,356)) if chapter == 10 else list(range(356,476))
    assert numbers == expected, (chapter, sorted(set(expected)-set(numbers)))
    assert text.count(r'\begin{problem}') == text.count(r'\end{problem}')
    supplements = re.findall(r'\\begin\{supplement\}\{([^}]+)\}', text)
    assert supplements == [f'{chapter}.{section}-{item}' for section in range(1,5) for item in (1,2)]
    assert text.count(r'\begin{supplement}') == text.count(r'\end{supplement}') == 8
    assert text.count(r'\subsection{') == 4
    LatexWalker(text, tolerant_parsing=False).get_latex_nodes()
    print(f'Chapter {chapter}: {len(numbers)} unique, ordered problem environments')
% !TeX program = xelatex
\documentclass[12pt,fontset=fandol]{ctexart}
\usepackage{geometry,amsmath,amssymb,bm,enumitem,xcolor,hyperref,xparse}
\geometry{paperwidth=240mm,paperheight=180mm,left=14mm,right=14mm,top=12mm,bottom=12mm,noheadfoot}
\hypersetup{hidelinks,pdftitle={工科数学分析逐题训练·横屏手写版},pdfauthor={},bookmarksopen=false,bookmarksdepth=2,pdfdisplaydoctitle=true}
\pdfstringdefDisableCommands{\def\quad{ }\def\qquad{ }}
\pagestyle{empty}
\setlength{\parindent}{0pt}
\setlength{\parskip}{3pt}
\setlength{\topskip}{0pt}
\setlength{\emergencystretch}{2em}
\setlist[enumerate]{label=（\arabic*）,leftmargin=2.6em,itemsep=2pt,topsep=3pt,parsep=0pt}
\newcommand{\dd}{\,\mathrm{d}}
\definecolor{ipadmuted}{gray}{0.40}

\ExplSyntaxOn
\msg_new:nnn {ipad} {validation-failed} {#1}
\NewDocumentCommand{\ipadFail}{m}{\msg_fatal:nnn {ipad}{validation-failed}{#1}}
\ExplSyntaxOff

\newcounter{ipadexercise}
\newcounter{ipadchapterid}
\newcounter{ipadsectionid}
\newcounter{ipadshippedpages}
\newif\ifipadchapterpending
\newif\ifipadsectionpending
\newcommand{\ipadchapter}{}
\newcommand{\ipadsection}{}
\newcommand{\ipadtopic}{}
\renewcommand{\section}[1]{%
  \stepcounter{ipadchapterid}\setcounter{ipadsectionid}{0}%
  \gdef\ipadchapter{#1}\gdef\ipadsection{}\gdef\ipadtopic{}%
  \global\ipadchapterpendingtrue\global\ipadsectionpendingfalse}
\renewcommand{\subsection}[1]{%
  \stepcounter{ipadsectionid}\gdef\ipadsection{#1}\gdef\ipadtopic{}%
  \global\ipadsectionpendingtrue}
\renewcommand{\subsubsection}[1]{\gdef\ipadtopic{#1}}
\newcommand{\ipadbookmarks}[2]{%
  \ifipadchapterpending
    \pdfbookmark[0]{\ipadchapter}{ipad.chapter.\arabic{ipadchapterid}}%
    \global\ipadchapterpendingfalse
  \fi
  \ifipadsectionpending
    \pdfbookmark[1]{\ipadsection}{ipad.section.\arabic{ipadchapterid}.\arabic{ipadsectionid}}%
    \global\ipadsectionpendingfalse
  \fi
  \pdfbookmark[2]{第#1题\space #2}{ipad.exercise.#1}}

\newsavebox{\ipadquestionbox}
\newlength{\ipadquestionheight}
\newlength{\ipadminblank}
\newlength{\ipadmaxquestionheight}
\newlength{\ipadremainingblank}
\setlength{\ipadminblank}{70mm}
\setlength{\ipadmaxquestionheight}{\dimexpr\textheight-\ipadminblank\relax}

\NewDocumentEnvironment{exercise}{m m +b}{%
  \clearpage
  \stepcounter{ipadexercise}%
  \ifnum#1=\value{ipadexercise}\relax\else
    \ipadFail{Exercise\space #1\space is\space out\space of\space sequence.}%
  \fi
  \begin{lrbox}{\ipadquestionbox}%
    \begin{minipage}[t]{\linewidth}
      \fontsize{12.5}{18}\selectfont
      \setlength{\abovedisplayskip}{5pt}%
      \setlength{\belowdisplayskip}{5pt}%
      \setlength{\abovedisplayshortskip}{3pt}%
      \setlength{\belowdisplayshortskip}{3pt}%
      {\fontsize{9}{12}\selectfont\color{ipadmuted}%
        \ipadbookmarks{#1}{#2}%
        \ipadchapter\quad /\quad\ipadsection
        \ifx\ipadtopic\empty\else\quad /\quad\ipadtopic\fi\par}
      \vspace{2mm}%
      {\fontsize{14}{19}\selectfont\bfseries 第#1题\quad #2\par}
      \vspace{1mm}%
      #3\par
    \end{minipage}%
  \end{lrbox}%
  \setlength{\ipadquestionheight}{\dimexpr\ht\ipadquestionbox+\dp\ipadquestionbox\relax}%
  \setlength{\ipadremainingblank}{\dimexpr\textheight-\ipadquestionheight\relax}%
  \typeout{IPAD-EXERCISE id=#1 height=\the\ipadquestionheight blank=\the\ipadremainingblank limit=\the\ipadmaxquestionheight}%
  \ifdim\ipadquestionheight>\ipadmaxquestionheight
    \ipadFail{Exercise\space #1\space exceeds\space the\space question\space height\space limit;\space at\space least\space 70mm\space blank\space space\space is\space required.}%
  \fi
  \nointerlineskip\box\ipadquestionbox
  \vfill\null
}{}

\AddToHook{shipout/after}{\stepcounter{ipadshippedpages}}
\AtEndDocument{%
  \ifnum\value{ipadexercise}=818\relax\else
    \ipadFail{Expected\space 818\space exercises;\space found\space \arabic{ipadexercise}.}%
  \fi}
\AddToHook{enddocument/afterlastpage}{%
  \typeout{IPAD-TOTAL exercises=\arabic{ipadexercise} pages=\arabic{ipadshippedpages}}%
  \ifnum\value{ipadshippedpages}=818\relax\else
    \ipadFail{Expected\space 818\space pages;\space found\space \arabic{ipadshippedpages}.}%
  \fi}

\begin{document}
\input{chapters/ch08.tex}
\input{chapters/ch09.tex}
\input{chapters/ch10.tex}
\input{chapters/ch11.tex}
\input{chapters/ch12.tex}
\input{chapters/ch13.tex}
\end{document}


## tool · 2026-10-20T00:20:06Z


Script completed
Wall time 0.1 seconds
Output:

.agent/math-analysis/songhao/pre-renumber/对应清单.json
.agent/math-analysis/songhao/pre-renumber/使用说明.md
.agent/math-analysis/songhao/pre-renumber/main.tex
.agent/math-analysis/songhao/pre-renumber/chapters/ch13.tex
.agent/math-analysis/songhao/pre-renumber/chapters/ch12.tex
.agent/math-analysis/songhao/pre-renumber/chapters/ch10.tex
.agent/math-analysis/songhao/pre-renumber/chapters/ch11.tex
.agent/math-analysis/songhao/pre-renumber/chapters/ch08.tex
.agent/math-analysis/songhao/pre-renumber/chapters/ch09.tex
.agent/math-analysis/songhao/renumber_plan.py:12:BACKUP = Path(__file__).resolve().parent / 'pre-renumber'
.agent/math-analysis/songhao/check_8_9.py:7:checkpoint = root / ".agent/math-analysis/songhao/pre-renumber/chapters"


## tool · 2026-10-20T00:20:10Z


Script completed
Wall time 0.8 seconds
Output:

{}
Representative checks passed: 256, 273, 274, 276, 331, 332, 333, 381, 406
Additional checks passed: 289, 297, 298, 299, 303, 304, 306, 321, 326, 348, 349
New checks passed: 316, supplements, 374, 376, 396, 402, 413, 417, 443, 448, 458, 472, 474
Chapter 10: 100 unique, ordered problem environments
Chapter 11: 120 unique, ordered problem environments


## tool · 2026-10-20T00:20:14Z




## tool · 2026-10-20T00:20:19Z


Script completed
Wall time 0.1 seconds
Output:

output/工科数学分析逐题训练/ipad.tex

param396 = [s.cos(t),s.sin(t),1-s.cos(t)]
field396 = [param396[1]*param396[2],-param396[0],-param396[1]]
ccw396 = s.integrate(sum(field396[i]*s.diff(param396[i],t) for i in range(3)),(t,0,2*s.pi))
same(ccw396, -3*s.pi)
param402 = [2*s.cos(t),1+s.sqrt(2)*s.sin(t),1-s.sqrt(2)*s.sin(t)]
field402 = [param402[2],param402[0],-1]
same(s.integrate(sum(field402[i]*s.diff(param402[i],t) for i in range(3)),(t,0,2*s.pi)),4*s.sqrt(2)*s.pi)
same(s.integrate((2-y)*(y+4-y*y/2),(y,-2,4)),18)
same(2*x*s.diff(y474,x)-4*y474,2*s.log(x)-1)
same(1+s.diff(y474,x)**2,(x+1/x)**2/4)
print('New checks passed: 316, supplements, 374, 376, 396, 402, 413, 417, 443, 448, 458, 472, 474')

for chapter in (10, 11):
    path = Path(__file__).resolve().parent / 'pre-renumber' / 'chapters' / f'ch{chapter}.tex'
    text = path.read_text()
    numbers = [int(number) for number in re.findall(r'\\begin\{problem\}\{(\d+)\}', text)]
    assert numbers == sorted(set(numbers)), (chapter, numbers)
    expected = list(range(256,356)) if chapter == 10 else list(range(356,476))
    assert numbers == expected, (chapter, sorted(set(expected)-set(numbers)))
    assert text.count(r'\begin{problem}') == text.count(r'\end{problem}')
    supplements = re.findall(r'\\begin\{supplement\}\{([^}]+)\}', text)
    assert supplements == [f'{chapter}.{section}-{item}' for section in range(1,5) for item in (1,2)]
    assert text.count(r'\begin{supplement}') == text.count(r'\end{supplement}') == 8
    assert text.count(r'\subsection{') == 4
    LatexWalker(text, tolerant_parsing=False).get_latex_nodes()
    print(f'Chapter {chapter}: {len(numbers)} unique, ordered problem environments')


## assistant · 2026-10-20T00:20:22Z

`ipad.tex` 完整编译成功，无需修改排版宏。818题、818页、每题至少70mm空白的编译断言全部通过。

`check_10_11.py` 已修正396题预期为 −3π，改读 `pre-renumber` 检查点，数学及结构检查全部通过。

未截图或检查图像；逐题实际高度极值待主代理从导出日志汇总。
