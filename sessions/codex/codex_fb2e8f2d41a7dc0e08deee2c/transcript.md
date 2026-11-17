# 01a152f0-1647-7660-8e83-2385b9104a39

来源：codex

项目：/Users/oyamahappa/Documents/Agent/Codex

## developer · 2026-10-19T06:53:50Z

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



## developer · 2026-10-19T06:53:50Z

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
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/10/19/01a152e6-2913-7de1-8285-580247378897`, `/Users/oyamahappa/Documents/Agent/Codex`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
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

## developer · 2026-10-19T06:53:50Z

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

## developer · 2026-10-19T06:53:50Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-10-19T06:53:50Z

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
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/Agent/Codex</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/Agent/Codex</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a152e6-2913-7de1-8285-580247378897</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-10-19T06:53:50Z

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


## tool · 2026-10-19T06:53:55Z


Script completed
Wall time 0.0 seconds
Output:

3. 杭州电子科技大学2026年数学分析

一、填空题（每题5分，共40分）

1. $\lim_{n \to \infty} \tan^n \left( \frac{\pi}{4} + \frac{1}{n} \right) = \_\_\_\_\_$

2. $\lim_{(x,y) \to (+\infty,+\infty)} \left( x^2 + y^2 \right) e^{-(x+y)} = \_\_\_\_\_$

3. $\int_0^{\ln 2} \sqrt{e^x - 1} dx = \_\_\_\_\_$

4. $\lim_{n \to \infty} \left[ \frac{f\left( 2026 + \frac{1}{n} \right)}{f(2026)} \right]^n = \_\_\_\_\_$

5. 已知 $f(x,y,z) = xy^2 z^3 e^{xyz}$, $z = z(x,y)$ 由 $x+y+z+xyz=0$ 确定, 求 $f_x(1,1,-1) = \_\_\_\_\_$

6. 设 $f(0) = 0$, $F(t) = \iiint_V \left[ z^2 + f(x^2 + y^2) \right] dxdydz$ ($V: x^2 + y^2 \leq t^2, 0 \leq z \leq 1$), 求 $\lim_{t \to 0^+} \frac{F(t)}{t^2} = \_\_\_\_\_$

7. $\int_L 3x^2 y dx + (x^3 + x - 2y) dy = \_\_\_\_\_$, 其中 $L$ 为沿 $x^2 + y^2 = 2x$ 从 $(0,0) \to (2,0)$, 再沿 $x^2 + y^2 = 4$ 从 $(2,0) \to (0,2)$ 的曲线.

8. $\int_0^{+\infty} \frac{\ln x}{x^2 + a} dx = \_\_\_\_\_$

二、计算题（每题7分，共28分）

1. $\lim_{x \to +\infty} \left( \frac{a^x - 1}{(a-1)x} \right)^{\frac{1}{x}}$ ($a > 0, a \neq 1$).

2. $\int_{\frac{1}{2}}^{\frac{3}{4}} \frac{\arcsin \sqrt{x}}{\sqrt{x(1-x)}} dx$.

3. 已知 $f(x) = \begin{cases} \frac{\sin x}{x}, & x \neq 0 \\ 1, & x = 0 \end{cases}$, 求 $f^{(k)}(0)$ ($k$ 阶导数).

4. $I = \iint_S f(x,y,z) dS$, 其中 $S: x^2 + y^2 + z^2 = 1$, $f(x,y,z) = \begin{cases} \sqrt{x^2 + y^2}, & 0 \leq z \leq \sqrt{x^2 + y^2} \\ 0, & z < 0 \text{ 或 } z > \sqrt{x^2 + y^2} \end{cases}$

三、综合题（每题10分，共40分）

1. 已知 $y = y(x)$ 由 $x = \int_1^{y-x} e^{-u^2} du$ 确定, $y$ 二阶可导, 求 $\lim_{x \to 0} \frac{y - (1+e)x - 1}{x^2}$.2、设 $a_{n}=\frac{1}{2\ln 2}+\frac{1}{3\ln 3}+\cdots+\frac{1}{n\ln n}-\ln \ln n$ ，判断 $a_{n}$ 是否收敛.
3、设 $u=f(z)$ ， $z=x+y\varphi(z)$ ，证明： $\frac{\partial^{n}u}{\partial y^{n}}=\frac{\partial^{n-1}}{\partial x^{n-1}}\left[\varphi(z)^{n}\frac{\partial u}{\partial x}\right].$
4、设 $I(\alpha)=\int_{0}^{+\infty}\frac{e^{-x}}{|\sin x|^{\alpha}}dx$ ，证明 $I(\alpha)$ 对 $\alpha \in[0,b](0<b<1)$ 一致收敛.
四、证明题（1-3题10分，4题12分，共42分）
1、已知 $f(x)$ 一致连续， $\varphi(x)$ 连续，且 $\lim_{x \to +\infty}[f(x)-\varphi(x)]=0$ ，证明 $\varphi(x)$ 在 $[a,+\infty)$ 上一致连续.
2、已知 $f(x)$ 在 $[a,b]$ 连续， $(a,b)$ 可微，且 $f(a)\neq f(b)$ ，证明： $\exists \xi,\eta \in(a,b)$ ，使得 $f^{\prime}(\xi)=\frac{a+b}{2\eta}f^{\prime}(\eta).$
3、已知 $f(x)$ 在 $[0,1]$ 连续， $f_{1}(x)=f(x)$ ， $f_{n+1}(x)=\int_{x}^{1}f_{n}(t)dt$ （ $n\geq 1$ ），证明 $\sum_{n=1}^{\infty}f_{n}(x)$ 在 $0\leq x\leq 1$ 上一致收敛.
4、设 $\varphi(x)$ 在 $\mathbb{R}$ 上周期为1，且 $\int_{0}^{1}\varphi(x)dx=0$ ， $f(x)$ 在 $[0,1]$ 连续可导， $a_{n}=\int_{0}^{1}f(x)\varphi(nx)dx$ ，证明级数 $\sum_{n=1}^{\infty}a_{n}^{2}$ 收敛.

## tool · 2026-10-19T06:54:13Z


Script completed
Wall time 0.1 seconds
Output:

# 3 杭州电子科技大学2026年数学分析

## 一、填空题（每题5分，共40分）

1、 $\operatorname* { l i m } _ { n \to \infty } \tan ^ { n } \left( { \frac { \pi } { 4 } } + { \frac { 1 } { n } } \right)$

2、 $\operatorname * { l i m } _ { ( x , y )  ( + \infty , + \infty ) } ( x ^ { 2 } + y ^ { 2 } ) e ^ { - ( x + y ) } = - \qquad $

3、 $\int _ { 0 } ^ { \ln 2 } { \sqrt { e ^ { x } - 1 } } d x =$

4、 $\operatorname* { l i m } _ { n \to \infty } { \left[ { \frac { f \left( 2 0 2 6 + { \frac { 1 } { n } } \right) } { f ( 2 0 2 6 ) } } \right] } ^ { n }$

5、已知 $f ( x , y , z ) = x y ^ { 2 } z ^ { 3 } e ^ { x y z }$ ，z=z(𝑥,y)由𝑥+y+z+xyz=0确定，求fz(1,1,-1)=

6、设 $f ( 0 ) ~ = ~ 0 , ~ F ( t ) ~ = ~ \iiint ~ [ z ^ { 2 } + f ( x ^ { 2 } + y ^ { 2 } ) ] ~ d x d y d z ~ ( V ~ : ~ x ^ { 2 } + y ^ { 2 } ~ \leq ~ t ^ { 2 } , 0 ~ \leq ~ z ~ \leq ~ 1 )$ 求 $\operatorname* { l i m } _ { t \to 0 ^ { + } } { \frac { F ( t ) } { t ^ { 2 } } } =$

7、 $\int _ { L } 3 x ^ { 2 } y d x + ( x ^ { 3 } + x - 2 y ) d y \ =$ ，其中L为沿 $x ^ { 2 } + y ^ { 2 } = 2 x {  { \mathcal { A } } } ( 0 , 0 ) \to ( 2 , 0 )$ ，再沿 $\cdot x ^ { 2 } + y ^ { 2 } = 4 / \lambda ( 2 , 0 )  ( 0 , 2 )$ 的曲线.

8、 $\int _ { 0 } ^ { + \infty } { \frac { \ln x } { x ^ { 2 } + a } } d x =$

## 二、计算题（每题7分，共28分）

1、 $\operatorname* { l i m } _ { x \to + \infty } \left( { \frac { a ^ { x } - 1 } { ( a - 1 ) x } } \right) ^ { \frac { 1 } { x } } ~ ( { a > 0 , a \not = 1 } )$

2、 $\int _ { \frac { 1 } { 2 } } ^ { \frac { 3 } { 4 } } { \frac { \arcsin { \sqrt { x } } } { \sqrt { x ( 1 - x ) } } } d x .$

3、已知 $f ( x ) = { \left\{ \begin{array} { l l } { \displaystyle { \frac { \sin x } { x } } , } & { x \neq 0 } \\ { 1 , } & { x = 0 } \end{array} \right. }$ ，求f(k)(0）（k阶导数）.

4、 $I = \iint _ { S } f ( x , y , z ) d S$ ，其中s： $x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = 1$ $f ( x , y , z ) = \left\{ \begin{array} { l l } { \sqrt { x ^ { 2 } + y ^ { 2 } } , } & { 0 \leq z \leq \sqrt { x ^ { 2 } + y ^ { 2 } } } \\ { 0 , } & { z < 0 \mathrm { ~ } \bar { x } \mathrm { ~ } z > \sqrt { x ^ { 2 } } } \end{array} \right.$ $z > \sqrt { x ^ { 2 } + y ^ { 2 } }$

## 三、综合题（每题10分，共40分）

1、已知y=y(x）由 $x = \int _ { 1 } ^ { y - x } e ^ { - u ^ { 2 } } d u$ 确定，y二阶可导，求 $\operatorname* { l i m } _ { x \to 0 } { \frac { y - ( 1 + e ) x - 1 } { x ^ { 2 } } }$

2、设 $\cdot a _ { n } = { \frac { 1 } { 2 \ln 2 } } + { \frac { 1 } { 3 \ln 3 } } + \cdots + { \frac { 1 } { n \ln n } } - \ln \ln n$ ，判断 $\dot { \boldsymbol { \mu } } _ { n }$ 是否收敛.

3、设 $\cdot u = f ( z ) , \ z = x + y \varphi ( z )$ ，证明： ${ \frac { \partial ^ { n } u } { \partial y ^ { n } } } = { \frac { \partial ^ { n - 1 } } { \partial x ^ { n - 1 } } } \left[ \varphi ( z ) ^ { n } { \frac { \partial u } { \partial x } } \right]$

4、设 $I ( \alpha ) = \int _ { 0 } ^ { + \infty } \frac { e ^ { - x } } { | \sin x | ^ { \alpha } } d x$ ，证明I(α)对 $\alpha \in [ 0 , b ] ( 0 < b < 1 )$ 一致收敛.

## 四、证明题（1-3题10分，4题12分，共42分）

1、已知f(𝑥)一致连续，(𝑥)连续，且 $\operatorname* { l i m } _ { x  + \infty } [ f ( x ) - \varphi ( x ) ] = 0$ ，证明(𝑥)在[a,+)上一致连续.

2、已知f(x)在[a,b]连续，(a,b)可微，且 $f ( a ) \neq f ( b )$ ，证明： $\exists \xi , \eta \in ( a , b )$ ，使得 $f ^ { \prime } ( \xi ) = \frac { a + b } { 2 \eta } f ^ { \prime } ( \eta )$

3、已知f(𝑥)在[0,1]连续，fi(x）=f(x)， $f _ { n + 1 } ( x ) = \int _ { x } ^ { 1 } f _ { n } ( t ) d t \ ( n \geq 1 )$ ，证明 $\sum _ { n = 1 } ^ { \infty } f _ { n } ( x )$ 在0≤ x≤1上一致收敛.

4、设 $\varphi ( x )$ 在R上周期为1，且 $\int _ { 0 } ^ { 1 } \varphi ( x ) d x = 0 .$ ，f(x)在[0,1]连续可导， $a _ { n } = \int _ { 0 } ^ { 1 } f ( x ) \varphi ( n x ) d x$ ，证 明级数 $: \sum _ { n = 1 } ^ { \infty } a _ { n } ^ { 2 }$ 收敛.

## tool · 2026-10-19T06:54:30Z




## tool · 2026-10-19T06:55:01Z


Script completed
Wall time 10.2 seconds
Output:


## tool · 2026-10-19T06:55:13Z


Script completed
Wall time 0.5 seconds
Output:

{"chunk_id":"ef79d1","wall_time_seconds":0.333755083,"exit_code":0,"original_token_count":43,"output":"I3 2 - pi/2\nII2 7*pi**2/144\nII4 -2*pi*(-1/4 + pi/8) + pi**2/2\narc_upper -pi/2\narc_lower pi/2\narc_quarter pi\nI8_exception_numeric 2.46740110027234 pi²/4 2.46740110027234\n"}

## tool · 2026-10-19T06:55:20Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"ad2dd1","wall_time_seconds":0,"exit_code":1,"original_token_count":9,"output":"zsh:1: operation not permitted: ps\n"}

## tool · 2026-10-19T06:57:37Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-10-19T06:57:48Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"c3ac2f","wall_time_seconds":0.000007459,"exit_code":0,"original_token_count":731,"output":"## 一、填空题\n### 1. 幂指极限\n### 2. 二元无穷远极限\n### 3. 定积分\n### 4. 含函数比值的幂指极限\n**条件说明：** 题面未给出 $f(2026)\\ne0$ 及相应的局部正则性，按原有条件不能确定答案。如果 $f(2026)=0$，式子甚至没有定义。\n### 5. 隐函数参与的偏导数\n### 6. 圆柱体上的三重积分极限\n**条件说明：** $f(0)=0$ 不能保证右侧积分平均值趋于零。例如取 $f(0)=0$、$f(s)=1$（$s>0$），则极限为 $4\\pi/3$；取 $f\\equiv0$，则极限为 $\\pi/3$。所以原题条件不足。\n### 7. 两段圆弧上的第二类曲线积分\n**条件说明：** 题面未指定圆弧，不能唯一确定结果。第二段取第一象限短弧时，第一段走上半圆的答案为 $\\boxed{\\pi/2-4}$，走下半圆则为 $\\boxed{3\\pi/2-4}$。\n### 8. 含参数的无穷积分\n但 $a=-1$ 是例外，此时\n级数与积分交换由非负项的单调收敛定理保证。因此，实参数下普通反常积分恰在 $a>0$ 或 $a=-1$ 时收敛。\n## 二、计算题\n### 1. 含指数参数的幂指极限\n### 2. 反三角函数定积分\n### 3. $\\sin x/x$ 在原点的高阶导数\n### 4. 单位球面上的第一类曲面积分\n## 三、综合题\n### 1. 积分确定的隐函数二阶极限\n### 2. 数列的收敛性\n### 3. 隐函数的高阶偏导恒等式\n**条件说明：** 该恒等式在所需阶数的偏导连续且隐函数分支存在的区域内成立。一个充分条件是 $f,\\varphi$ 具有足够的连续导数，且 $1-y\\varphi'(z)\\ne0$。原题省略了这些常规微分条件；没有相应条件时，式中的偏导可能不存在。\n### 4. 含无限多个奇点的积分一致收敛\n## 四、证明题\n### 1. 渐近接近一致连续函数\n### 2. 两点导数关系及原命题的条件问题\nf'(\\xi)=\\frac{a+b}{2\\eta}f'(\\eta).\n**当 $a+b\\ne0$ 时，命题成立。** 题面没有要求 $\\xi\\ne\\eta$，直接取\n\\xi=\\eta=\\frac{a+b}{2}\\in(a,b).\n此时 $\\eta\\ne0$，且 $(a+b)/(2\\eta)=1$，故等式成立。这个证明表明，在这一情形下，$f(a)\\ne f(b)$ 并非必要条件。\n**当 $a+b=0$ 时，原命题一般不成立。** 取 $[a,b]=[-1,1]$、$f(x)=x$，满足全部已给条件，但任何 $\\eta\\ne0$ 都会使右端等于 $0$，左端恒为 $1$；$\\eta=0$ 时原式没有定义。因此无法证明原题的无条件表述。\n更精确地，在 $a+b=0$ 时，题设等式能成立当且仅当 $(a,b)$ 内存在一点 $\\xi$ 满足 $f'(\\xi)=0$。一旦存在这样的点，任取非零的 $\\eta\\in(a,b)$ 即可。补充 $a+b\\ne0$ 是保证原结论成立的一个简单条件。\n### 3. 迭代积分函数级数一致收敛\n### 4. 零均值周期函数产生的平方可和系数\n## 计算交叉核对\n另使用 mpmath 分段数值积分核对一8的特殊参数 $a=-1$，得到 $2.46740110027234$，与 $\\pi^2/4=2.46740110027234$ 一致。数值核对仅作计算交叉检查，证明以各题推导为依据。\n"}
{"chunk_id":"d9fbcd","wall_time_seconds":0.101967084,"exit_code":1,"original_token_count":23,"output":"Traceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nAssertionError\n"}

## tool · 2026-10-19T06:57:55Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"bbd8cd","wall_time_seconds":0.125828875,"exit_code":0,"original_token_count":21,"output":"heading count 20\ndisplay delimiters 61 60\nsphere 0\nlong arc 0\nidentity [0, 0, 0, 0]\n"}

## tool · 2026-10-19T06:58:05Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"f06ba6","wall_time_seconds":0.165177041,"exit_code":0,"original_token_count":24,"output":"PASS: 20题标题、60组显示公式、球面积分、长圆弧、高阶恒等式n=1..4实例\n"}

## tool · 2026-10-19T06:58:18Z




## assistant · 2026-10-19T06:58:23Z

妹妹，已完成[2026数学分析20题补充解析](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/supplements/数学分析/2026/补充解析.md)。

已标明缺失条件、圆弧歧义、参数例外及四2反例。SymPy、mpmath交叉核对及20题结构检查通过。

未调用视觉工具，未修改其他文件或执行Git操作。

## tool · 2026-10-19T07:15:54Z


Script completed
Wall time 0.2 seconds
Output:

1、（15分）证明： $ 1+\sqrt{3}+\sqrt[3]{9} $为无理数.
2、设 $ \alpha, \beta, \gamma $为三维列向量， $ A_{1}=(\alpha, \beta, \gamma), \left| A_{1}\right|=-2 $ ，且 $ A_{2}=(5\alpha,-3\beta, 2\gamma) $ ，求 $ \left| \begin{array}{cc} 0 & A_{1} \\ A_{2} & 0 \end{array} \right|=? $
3、证明： $ A_{m\times n}X=0 $和 $ B_{z\times n}X=0 $同解充要条件为 $ r(A)=r(B)=r\left( \begin{array}{c} A \\ B \end{array} \right). $1、（15分）证明： $ 1+\sqrt{3}+\sqrt{9} $为无理数.
2、设 $ \alpha, \beta, \gamma $为三维列向量， $ A_{1}=(\alpha, \beta, \gamma), \left| A_{2} \right|=-2 $ ，且 $ A_{2}=(5\alpha,-3\beta, 2\gamma) $ ，求 $ \begin{vmatrix} 0 & A_{1} \\ A_{2} & 0 \end{vmatrix}=? $
3、证明： $ A_{m>n}X=0 $和 $ B_{2<n}X=0 $同解充要条件为 $ r(A)=r(B)=r\left( \begin{array}{c} A \\ B \end{array} \right). $
4、已知 $ A $为正定矩阵，证明： $ A+A^{-1}-2E $为半正定矩阵.
5、若 $ A=\left( \begin{array}{c c c} -10 & 5 & -1 \\ -12 & 5 & 1 \\ -12 & 1 & 9 \end{array} \right). $
（1）是否有 $ A=B^{3} $？
（2）将（1）进行推广，并证明.
6、设二次型
$ f\left( x_{1}, x_{2}, x_{3} \right)=3 x_{1}^{2}+6 x_{2}^{2}+3 x_{3}^{2}-4 x_{1} x_{2}-8 x_{1} x_{3}-4 x_{2} x_{3}, $
在条件 $ x_{1}^{2}+x_{2}^{2}+x_{3}^{2}=1 $下，最小值为多少，求出最小值点 $ \left( x_{1}, x_{2}, x_{3} \right). $(1) $ A=\left[ \begin{array}{c c c c} 1 & 0 & 2 & 1 \\ -1 & 2 & 1 & 3 \\ 1 & 2 & 5 & 5 \\ 2 & -2 & 1 & -2 \end{array} \right] $ ，则 $ \mathcal{A} $的像与核.
(2)在 $ \mathcal{A} $的核中取一组基，把它扩充为 V的一组基，并求 $ \mathcal{A} $在这组基下的矩阵.
(3)在 $ \mathcal{A} $的值域中取一组基，把它扩充为 V的一组基，并求 $ \mathcal{A} $在这组基下的矩阵.
8、若 $ A $为 n阶实对称矩阵， $ W=\left\{x\in R^{n}\mid X^{\top}AX=0\right\} $.
(1)若 $ A $为半正定，证明： $ W $是 $ R^{n} $的子空间，并求W的维数.
(2)若 $ A $为不定矩阵，则W是否满足（1）的结论，若满足给出证明，若不满足，举出反例.# 杭州电子科技大学2025年高等代数真题

1、(15分）证明： $1 + \sqrt { 3 } + \sqrt [ 3 ] { 9 }$ 为无理数.

2、设 $\alpha , \beta , \gamma$ 为三维列向量， $\mathcal { A } _ { 1 } = ( \alpha , \beta , \gamma ) , | \mathcal { A } _ { 1 } | = - 2$ $\mathcal { A } _ { 2 } = ( 5 \alpha , - 3 \beta , 2 \gamma )$ ，求数学考 盗版必究$\begin{array} { r l } { \big | 0 } & { { } \mathcal { A } _ { 1 } \big | } \\ { \mathcal { A } _ { 2 } } & { { } 0 } \end{array}$ 所有 哥数学考研 考研考博

3、证明： $A _ { n \times n } X = 0$ 和 $B _ { s \times n } X = 0$ 同解充要条件为 $r ( A ) = r ( B ) = r { \binom { A } { B } }$

4、已知A为正定矩阵，证明： $\boldsymbol { A } + \boldsymbol { A } ^ { - 1 } - 2 \boldsymbol { E }$ 为半正定矩阵.

5、若 $\begin{array} { r } { A = \left( \begin{array} { l l l } { - 1 0 } & { 5 } & { - 1 } \\ { - 1 2 } & { 5 } & { 1 } \\ { - 1 2 } & { 1 } & { 9 } \end{array} \right) } \end{array}$ 定哥

(1）是否有 $\scriptstyle A = B ^ { 3 } ~ ?$

(2)将（1）进行推广，并证明.

6、设二次型

$$
f { \big ( } x _ { 1 } , x _ { 2 } , x _ { 3 } { \big ) } = 3 x _ { 1 } ^ { 2 } + 6 x _ { 2 } ^ { 2 } + 3 x _ { 3 } ^ { 2 } - 4 x _ { 1 } x _ { 2 } - 8 x _ { 1 } x _ { 3 } - 4 x _ { 2 } x _ { 3 } =
$$

在条件 $x _ { 1 } ^ { 2 } + x _ { 2 } ^ { 2 } + x _ { 3 } ^ { 2 } = 1$ 下，最小值为多少，求出最小值点 $\left( x _ { 1 } , x _ { 2 } , x _ { 3 } \right)$

7、线性空间V上，在基 $\left( \varepsilon _ { 1 } , \varepsilon _ { 2 } , \varepsilon _ { 3 } , \varepsilon _ { 4 } \right)$ 下矩阵为A.

(1) $\begin{array} { r } { A = \left[ \begin{array} { l l l l } { 1 } & { 0 } & { 2 } & { 1 } \\ { - 1 } & { 2 } & { 1 } & { 3 } \\ { 1 } & { 2 } & { 5 } & { 5 } \\ { 2 } & { - 2 } & { 1 } & { - 2 } \end{array} \right] } \end{array}$ ，则的像与核. 研

(2）在√的核中取一组基，把它扩充为V的一组基，并求在这组基下的矩阵 心权 哥数 x 考研

(3)在的值域中取一组基，把它扩充为V的一组基，并求√在这组基下的矩阵. 贩权

8、若A为n阶实对称矩阵， $W = \left\{ x \in R ^ { n } | ~ X ^ { \top } A X = 0 \right\}$

(1）若A为半正定，证明：W是 $R ^ { n }$ 的子空间，并求W的维数.

(2)若A为不定矩阵，则W是否满足（1)的结论，若满足给出证明，若不满足， 举出反例. 考 考研

## tool · 2026-10-19T07:15:58Z




## tool · 2026-10-19T07:16:06Z


Script completed
Wall time 1.9 seconds
Output:

{"chunk_id":"57de02","wall_time_seconds":1.718725917,"exit_code":0,"original_token_count":784,"output":"A char lambda**3 - 4*lambda**2 - 48*lambda + 8\nA eigen [(4/3 + 2*(-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3) + 80/(9*(-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)), 1, [Matrix([\n[335/414 - 20/(27*(-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)) - (4/3 + 2*(-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3) + 80/(9*(-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)))**2/552 - (-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)/6],\n[                                                                                                                                 47/23 - (4/3 + 2*(-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3) + 80/(9*(-1/2 - sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)))**2/46],\n[                                                                                                                                                                                                                                                                                1]])]), (4/3 + 80/(9*(-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)) + 2*(-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3), 1, [Matrix([\n[335/414 - (-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)/6 - (4/3 + 80/(9*(-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)) + 2*(-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3))**2/552 - 20/(27*(-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3))],\n[                                                                                                                                 47/23 - (4/3 + 80/(9*(-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3)) + 2*(-1/2 + sqrt(3)*I/2)*(205/54 + 5*sqrt(951)*I/18)**(1/3))**2/46],\n[                                                                                                                                                                                                                                                                                1]])]), (4/3 + 80/(9*(205/54 + 5*sqrt(951)*I/18)**(1/3)) + 2*(205/54 + 5*sqrt(951)*I/18)**(1/3), 1, [Matrix([\n[335/414 - (205/54 + 5*sqrt(951)*I/18)**(1/3)/6 - (4/3 + 80/(9*(205/54 + 5*sqrt(951)*I/18)**(1/3)) + 2*(205/54 + 5*sqrt(951)*I/18)**(1/3))**2/552 - 20/(27*(205/54 + 5*sqrt(951)*I/18)**(1/3))],\n[                                                                                       47/23 - (4/3 + 80/(9*(205/54 + 5*sqrt(951)*I/18)**(1/3)) + 2*(205/54 + 5*sqrt(951)*I/18)**(1/3))**2/46],\n[                                                                                                                                                                                            1]])])]\nQ eigen [(-2, 1, [Matrix([\n[  1],\n[1/2],\n[  1]])]), (7, 2, [Matrix([\n[-1/2],\n[   1],\n[   0]]), Matrix([\n[-1],\n[ 0],\n[ 1]])])]\nC rank 2\nC rref (Matrix([\n[1, 0,   2, 1],\n[0, 1, 3/2, 2],\n[0, 0,   0, 0],\n[0, 0,   0, 0]]), (0, 1))\nC kernel [Matrix([\n[  -2],\n[-3/2],\n[   1],\n[   0]]), Matrix([\n[-1],\n[-2],\n[ 0],\n[ 1]])]\nC image [Matrix([\n[ 1],\n[-1],\n[ 1],\n[ 2]]), Matrix([\n[ 0],\n[ 2],\n[ 2],\n[-2]])]\nC char lambda**2*(lambda**2 - 6*lambda - 4)\n"}

## tool · 2026-10-19T07:16:37Z


Script completed
Wall time 2.1 seconds
Output:

{"chunk_id":"9242ec","wall_time_seconds":1.808323084,"exit_code":0,"original_token_count":120,"output":"Pk\nMatrix([[-4, -1, 1, 0], [-3, -2, -1, 2], [2, 0, 1, 2], [0, 1, 2, -2]])\ndet\n-8\ntransformed\nMatrix([[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 5, 2], [0, 0, 9/2, 1]])\nPi\nMatrix([[1, 0, -4, -1], [-1, 2, -3, -2], [1, 2, 2, 0], [2, -2, 0, 1]])\ndet\n-8\ntransformed\nMatrix([[5, 2, 0, 0], [9/2, 1, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]])\nAc1\nMatrix([[5], [4], [14], [1]])\nAc2\nMatrix([[2], [0], [4], [2]])\npolynomial lam**3 - 4*lam**2 - 48*lam + 8 values [-64, 72, 8, -43, -120, 128]\ndisc 507200\n"}

## tool · 2026-10-19T07:16:55Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"855f39","wall_time_seconds":0.219640333,"exit_code":2,"original_token_count":38,"output":"rg: .agent/hdu-ocr/supplements/高等代数/2025: No such file or directory (os error 2)\n.agent/hdu-ocr/supplements/数学分析/2026/补充解析.md\n"}

## tool · 2026-10-19T07:17:19Z


Script completed
Wall time 1.9 seconds
Output:

{}
{"chunk_id":"31933d","wall_time_seconds":1.582425542,"exit_code":1,"original_token_count":66,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/check_algebra2025.py\", line 8, in <module>\n    assert sp.expand((r - sp.sqrt(3)) ** 3 - 9) == (\n           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^\nAssertionError\n"}

## tool · 2026-10-19T07:17:28Z


Script completed
Wall time 2.4 seconds
Output:

from pathlib import Path

import mpmath as mp
import sympy as sp


r = sp.symbols("r", real=True)
assert sp.expand((r - sp.sqrt(3)) ** 3 - 9) == (
    r**3 + 9 * r - 9 - 3 * (r**2 + 1) * sp.sqrt(3)
)

A1 = sp.diag(-2, 1, 1)
A2 = A1 * sp.diag(5, -3, 2)
block = sp.BlockMatrix([[sp.zeros(3), A1], [A2, sp.zeros(3)]]).as_explicit()
assert A2.det() == 60 and block.det() == 120


{}
{"chunk_id":"6810c1","wall_time_seconds":1.769185083,"exit_code":0,"original_token_count":42,"output":"PASS: 无理性恒等式、分块行列式、特征多项式、立方根、二次型、两组变基及不定型反例\n立方根数值核对最大残差： 4.27642e-49\n"}

## tool · 2026-10-19T07:19:14Z


Script completed
Wall time 1.6 seconds
Output:

{}
{"chunk_id":"23af13","wall_time_seconds":1.146423958,"exit_code":0,"original_token_count":42,"output":"PASS: 无理性恒等式、分块行列式、特征多项式、立方根、二次型、两组变基及不定型反例\n立方根数值核对最大残差： 4.27642e-49\n"}

## tool · 2026-10-19T07:19:53Z


Script completed
Wall time 1.2 seconds
Output:

{"chunk_id":"60481a","wall_time_seconds":0.000012708,"exit_code":0,"original_token_count":642,"output":"from pathlib import Path\n\nimport mpmath as mp\nimport sympy as sp\n\n\nr = sp.symbols(\"r\", real=True)\nassert sp.simplify(\n    (r - sp.sqrt(3)) ** 3 - 9\n    - (r**3 + 9 * r - 9 - 3 * (r**2 + 1) * sp.sqrt(3))\n) == 0\n\nA1 = sp.diag(-2, 1, 1)\nA2 = A1 * sp.diag(5, -3, 2)\nblock = sp.BlockMatrix([[sp.zeros(3), A1], [A2, sp.zeros(3)]]).as_explicit()\nassert A2.det() == 60 and block.det() == 120\n\nA = sp.Matrix([[-10, 5, -1], [-12, 5, 1], [-12, 1, 9]])\nt = sp.symbols(\"t\")\np = A.charpoly(t).as_expr()\nassert p == t**3 - 4 * t**2 - 48 * t + 8\nassert [p.subs(t, x) for x in (-6, -4, 0, 1, 8, 10)] == [\n    -64, 72, 8, -43, -120, 128\n]\nassert sp.discriminant(p, t) == 507200\n\nmp.mp.dps = 50\nroots = [mp.mpf(str(v)) for v in sp.nroots(p, n=50)]\nAm = mp.matrix(A.tolist())\nidentity = mp.eye(3)\nB = mp.zeros(3)\nfor i, root in enumerate(roots):\n    projector = mp.eye(3)\n    for j, other in enumerate(roots):\n        if i != j:\n            projector = projector * (Am - other * identity) / (root - other)\n    B += mp.sign(root) * mp.root(abs(root), 3) * projector\nresidual = max(abs(value) for value in B**3 - Am)\nassert residual < mp.mpf(\"1e-35\")\n\nQ = sp.Matrix([[3, -2, -4], [-2, 6, -2], [-4, -2, 3]])\nv = sp.Matrix([2, 1, 2])\nassert Q.charpoly(t).as_expr().factor() == (t + 2) * (t - 7) ** 2\nassert Q * v == -2 * v and v.dot(v) == 9\n\nC = sp.Matrix([[1, 0, 2, 1], [-1, 2, 1, 3], [1, 2, 5, 5], [2, -2, 1, -2]])\nk1, k2 = sp.Matrix([-4, -3, 2, 0]), sp.Matrix([-1, -2, 0, 1])\nv1, v2 = sp.Matrix([1, -1, 1, 2]), sp.Matrix([0, 1, 1, -1])\nassert C.rank() == 2 and C * k1 == sp.zeros(4, 1) and C * k2 == sp.zeros(4, 1)\nassert v1 == C[:, 0] and 2 * v2 == C[:, 1]\nassert C * v1 == 5 * v1 + 9 * v2 and C * v2 == v1 + v2\nP = sp.Matrix.hstack(k1, k2, v1, v2)\nR = sp.Matrix.hstack(v1, v2, k1, k2)\nassert P.det() == R.det() == -4\nassert P.inv() * C * P == sp.diag(sp.zeros(2), sp.Matrix([[5, 1], [9, 1]]))\nassert R.inv() * C * R == sp.diag(sp.Matrix([[5, 1], [9, 1]]), sp.zeros(2))\n\nH = sp.diag(1, -1)\nx, y = sp.Matrix([1, 1]), sp.Matrix([1, -1])\nassert (x.T * H * x)[0] == (y.T * H * y)[0] == 0\nassert ((x + y).T * H * (x + y))[0] == 4\n\nsolution = Path(__file__).parent / \"supplements/高等代数/2025/补充解析.md\"\nif solution.exists():\n    lines = solution.read_text().splitlines()\n    assert sum(line.startswith(\"## \") for line in lines) == 8\n    assert lines.count(r\"\\[\") == lines.count(r\"\\]\")\n\nprint(\"PASS: 无理性恒等式、分块行列式、特征多项式、立方根、二次型、两组变基及不定型反例\")\nprint(\"立方根数值核对最大残差：\", mp.nstr(residual, 6))\n"}
{}
{"chunk_id":"c014c2","wall_time_seconds":0.737388916,"exit_code":0,"original_token_count":476,"output":"PASS: 无理性恒等式、分块行列式、特征多项式、立方根、二次型、两组变基及不定型反例\n立方根数值核对最大残差： 4.27642e-49\n# 杭州电子科技大学2025年高等代数真题\n\n## 1.（15分）\n\n证明：$1+\\sqrt3+\\sqrt[3]9$ 为无理数。\n\n## 2.\n\n设 $\\alpha,\\beta,\\gamma$ 为三维列向量，$A_1=(\\alpha,\\beta,\\gamma)$，$|A_1|=-2$，且 $A_2=(5\\alpha,-3\\beta,2\\gamma)$，求\n\n\\[\n\\begin{vmatrix}\n0&A_1\\\\\nA_2&0\n\\end{vmatrix}.\n\\]\n\n## 3.\n\n证明：$A_{m\\times n}X=0$ 和 $B_{s\\times n}X=0$ 同解的充要条件为\n\n\\[\nr(A)=r(B)=r\\begin{pmatrix}A\\\\B\\end{pmatrix}.\n\\]\n\n## 4.\n\n已知 $A$ 为正定矩阵，证明：$A+A^{-1}-2E$ 为半正定矩阵。\n\n## 5.\n\n若\n\n\\[\nA=\\begin{pmatrix}\n-10&5&-1\\\\\n-12&5&1\\\\\n-12&1&9\n\\end{pmatrix}.\n\\]\n\n（1）是否有 $A=B^3$？\n\n（2）将（1）进行推广，并证明。\n\n## 6.\n\n设二次型\n\n\\[\nf(x_1,x_2,x_3)=3x_1^2+6x_2^2+3x_3^2-4x_1x_2-8x_1x_3-4x_2x_3,\n\\]\n\n在条件 $x_1^2+x_2^2+x_3^2=1$ 下，最小值为多少？求出最小值点 $(x_1,x_2,x_3)$。\n\n## 7.\n\n线性空间 $V$ 上的线性变换 $\\mathcal A$ 在基 $(\\varepsilon_1,\\varepsilon_2,\\varepsilon_3,\\varepsilon_4)$ 下的矩阵为\n\n\\[\nA=\\begin{pmatrix}\n1&0&2&1\\\\\n-1&2&1&3\\\\\n1&2&5&5\\\\\n2&-2&1&-2\n\\end{pmatrix}.\n\\]\n\n（1）求 $\\mathcal A$ 的像与核。\n\n（2）在 $\\mathcal A$ 的核中取一组基，把它扩充为 $V$ 的一组基，并求 $\\mathcal A$ 在这组基下的矩阵。\n\n（3）在 $\\mathcal A$ 的值域中取一组基，把它扩充为 $V$ 的一组基，并求 $\\mathcal A$ 在这组基下的矩阵。\n\n## 8.\n\n若 $A$ 为 $n$ 阶实对称矩阵，\n\n\\[\nW=\\{x\\in\\mathbb R^n\\mid x^{\\mathsf T}Ax=0\\}.\n\\]\n\n（1）若 $A$ 为半正定矩阵，证明：$W$ 是 $\\mathbb R^n$ 的子空间，并求 $W$ 的维数。\n\n（2）若 $A$ 为不定矩阵，则 $W$ 是否满足（1）的结论？若满足，给出证明；若不满足，举出反例。\n"}

## tool · 2026-10-19T07:20:01Z




## assistant · 2026-10-19T07:20:10Z

妹妹，2025高代已完成全部8大题及小问：

- [补充解析](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/supplements/高等代数/2025/补充解析.md)
- [准确题面](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/overrides/85b8c8c41edb8e84.md)
- [核对脚本](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/check_algebra2025.py)

SymPy与mpmath检查通过，立方根数值残差约为 $4.28\times10^{-49}$。已明确奇次根推广条件及反例。

未调用视觉工具，未修改builder、最终output或执行Git操作。

## tool · 2026-10-19T07:21:04Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"a336c6","wall_time_seconds":0.000008208,"exit_code":0,"original_token_count":1210,"output":"list\n[{'source': 'HDU/601数学分析/2012/2012年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/22a122cb4a98dc46.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2015/2015年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/d33f5e829fc00d5a.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2016/2016年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/fea9d2b3839c949f.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2017/2017年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/46929cf0f3732438.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/3b3988fabf56aa34.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/44e52faade343b4f.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/05b6f5defd28516d.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/18b9d020a6735f1e.pdf', 'pages': [1, 2]}, {'source': 'HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agen\nRESULTS [{'path': 'latex/数学分析/2011/2011年杭州电子科技大学601数学分析考研真题.tex', 'sha256': '02876dc8efc24b4573721acd6e733729f3f3111f526ae4e9a96996814b0cf204', 'exit_code': 0, 'errors': [], 'log': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/d9b3f6ff33c698f5/command.txt'}, {'path': 'latex/数学分析/2011/2011年杭州电子科技大学601数学分析考研真题参考答案.tex', 'sha256': '6e48e38b854933d6a6e1e37988e62356b41aa15ad4d5a6b98d298b7cc21e05f6', 'exit_code': 1, 'errors': ['学601数学分析考研真题参考答案.tex:107: Missing number, treated as zero.'], 'log': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/46f227213c883308/command.txt'}, {'path': 'latex/数学分析/2012/2012年杭州电子科技大学601数学分析考研真题.tex', 'sha256': 'a19faaf53befc69e006c09912fb22ca15456466875311ec3666771b521bac133', 'exit_code': 0, 'errors': [], 'log': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/e6bbb07c0153214e/command.txt'}, {'path': 'latex/数学分析/2012/2012年杭州电子科技大学601数学分析考研真题参考答案.tex', 'sha256': 'd5c287ceb39cc88e2c8f41e03804b0e18814837d9d7a77e6d84991866a1ed822', 'exit_code': 1, 'errors': ['Missing character: There is no n (\"6E) in font rsfs10!', 'Missing character: There is no n (\"6E) in font rsfs10!'], 'log': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/4252883b91e8ce2e/command.txt'}, {'path': 'latex/数学分析/2013/2013年杭州电子科技大学601数学分析考研真题.tex', 'sha256': 'e1d3c68dde2b81f8bb0615f41e44aa313aa8c7a24f89c5b564e094df3c4e16c6', 'exit_code': 0, 'errors': [], 'log': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/d54d73d019679e99/command.txt'}, {'path': 'latex/数学分析/2013/2013年杭州电子科技大学601数学分析考研真题参考答案.tex', 'sha256': 'da9ecc6eb4df914de25587a02920ad16d1545cde857732040b8299cf0b129241', 'exit_code': 1, 'errors': ['学601数学分析考研真题参考答案.tex:169: Extra }, or forgotten $.'], 'log': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/d1c78468ff548b66/command.txt'}, {'path': 'latex/数学分析/2014/2014年杭州电子科技大学601数学分析考研真题.tex', 'sha256': '43376956d27f608c75984661a1b6f41e6fd3e8c639ca84bc120b4472b0942df5', 'exit_code': 1, 'errors': ['学601数学分析考研真题.tex:161: Extra alignment tab has been changed to \\\\cr.'], 'log': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/7bd84bec5bfce9ea/command.txt'}, {'path': 'latex/数学分析/2014/2014年杭州电子科技大学601数学分析考研真题参考答案.tex', 'sha256': 'd3ce4a48f49185b3b713188c8531171f2e6bf2f09f054d5209749d2934fee9ad', 'exit_code': 0, 'errors': ['Missing character: There is no 𝛼 (U+1D6FC) in font Times New Roman/OT:script=la', 'Missing character: There is no 𝛼 (U+1D6FC) in font Times New Roman/OT:script=la'\n"}

## tool · 2026-10-19T07:21:12Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"88a55b","wall_time_seconds":0.086522042,"exit_code":0,"original_token_count":8400,"output":"Warning: truncated output (original token count: 8400)\nTotal output lines: 31\n\nJOBS\n1abbef1daec3bc92 HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.pdf\n27ea8f6e4eb7355d HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.pdf\nf6badbfa1728d169 HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf\n128a26e7394a073e HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.pdf\n3f7b5ea1df00c613 HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.pdf\n2c29e49c601a658a HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.pdf\ne3e469709b9c871a HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf\nbe2d15e5112d94ec HDU/601数学分析/2023/2023年杭州电子科技大学数分高代(高代不含答案双科版).pdf\ne43b7f46d6f192ef HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.pdf\n9e64c36cdac10429 HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.pdf\n92a5bd5ef85605e7 HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.pdf\n391fa17a5f0f6f61 HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf\n176002d27d3f75a0 HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.pdf\n918271f5178ca024 HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.pdf\n52d23623a0404647 HDU/601数学分析/2023/2023年杭州电子科技大学数分高代真题及答案(双科合卷).pdf\ncd2a7a833ba8f5fa HDU/601数学分析/2022/2022年杭州电子科技大学数分高代真题及答案(双科合卷).pdf\nRESULTS\nlatex/数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.tex 0 []\nlatex/数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.tex 1 []\nlatex/数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.tex 1 []\nlatex/数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.tex 3 ['Missing character: There is no 𝛴 (\"1D6F4) in font rm-lmbx10!']\nlatex/数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.tex 0 []\nlatex/数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.tex 0 ['Missing character: There is no 𝚥 (U+1D6A5) in font Times New Roman/OT:script=la']\nlatex/数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.tex 0 []\nlatex/数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.tex 1 []\nlatex/数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.tex 0 []\nlatex/数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.tex 0 []\nlatex/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.tex 0 ['Missing character: There is no △ (U+25B3) in font Times New Roman/OT:script=lat']\nlatex/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.tex 1 ['Missing character: There is no \\uf047 (U+F047) in font Times New Roman/OT:script=lat', 'Missing character: There is no △ (U+25B3) in font Times New Roman/OT:script=lat']\nlatex/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).tex 1 ['Missing character: There is no ⨏ (U+2A0F) in font [latinmodern-math.otf]/OT:scr', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs5!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no o (\"6F) in font rsfs10!', 'Missing character: There is no 𝜃 (U+1D703) in font Times New Roman/OT:script=la', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman…1400 tokens truncated…, 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no 𝜎 (U+1D70E) in font Times New Roman Bold/OT:scri', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip', 'Missing character: There is no ⊗ (U+2297) in font Times New Roman Bold/OT:scrip']\n"}

## tool · 2026-10-19T07:21:23Z


Script completed
Wall time 1.0 seconds
Output:

{"chunk_id":"ca2227","wall_time_seconds":0.266909708,"exit_code":0,"original_token_count":1092,"output":"1abbef1daec3bc92 4399 HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.pdf\n27ea8f6e4eb7355d 4453 HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.pdf\nf6badbfa1728d169 3709 HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf\n128a26e7394a073e 3860 HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.pdf\n3f7b5ea1df00c613 3705 HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.pdf\n2c29e49c601a658a 4477 HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.pdf\ne3e469709b9c871a 17342 HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf\nbe2d15e5112d94ec 3536 HDU/601数学分析/2023/2023年杭州电子科技大学数分高代(高代不含答案双科版).pdf\ne43b7f46d6f192ef 21498 HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.pdf\n9e64c36cdac10429 20710 HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.pdf\n92a5bd5ef85605e7 20126 HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.pdf\n391fa17a5f0f6f61 21427 HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf\n176002d27d3f75a0 26059 HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.pdf\n918271f5178ca024 32016 HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.pdf\n52d23623a0404647 28119 HDU/601数学分析/2023/2023年杭州电子科技大学数分高代真题及答案(双科合卷).pdf\ncd2a7a833ba8f5fa 27981 HDU/601数学分析/2022/2022年杭州电子科技大学数分高代真题及答案(双科合卷).pdf\nlatex/数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.tex 0 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/264a40299e5af80e/command.txt\nlatex/数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.tex 1 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/987d0950f99979fc/command.txt\nlatex/数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.tex 1 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/630465da14431cc4/command.txt\nlatex/数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.tex 3 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/bdab68f9d0f10c1c/command.txt\nlatex/数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.tex 0 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/fa9fcdbcfbc76592/command.txt\nlatex/数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.tex 0 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/d2a26cbe39d6ce03/command.txt\nlatex/数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.tex 0 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/9bc1de2a60a434f2/command.txt\nlatex/数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.tex 1 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/d3c71ea109b67c64/command.txt\nlatex/数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.tex 0 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/f63f076f471cd037/command.txt\nlatex/数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.tex 0 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/45bd911a4b2e13a3/command.txt\nlatex/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.tex 0 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/92db3d4a166cbc39/command.txt\nlatex/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.tex 1 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/d64a56cfc09b0440/command.txt\nlatex/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).tex 1 [] /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/2914756ed02633a1/command.txt\n"}
{"chunk_id":"15d613","wall_time_seconds":0.195359416,"exit_code":0,"original_token_count":2339,"output":"\\usepackage{amsmath,amssymb,mathtools,mathrsfs,esint,bm,newunicodechar}\n\\allowdisplaybreaks\n\\setlength{\\emergencystretch}{3em}\n\\newunicodechar{∞}{\\ensuremath{\\infty}}\n\\newunicodechar{∈}{\\ensuremath{\\in}}\n\\newunicodechar{∑}{\\ensuremath{\\sum}}\n\\newunicodechar{∫}{\\ensuremath{\\int}}\n\\newunicodechar{≤}{\\ensuremath{\\leq}}\n\\newunicodechar{≥}{\\ensuremath{\\geq}}\n\\newunicodechar{≠}{\\ensuremath{\\neq}}\n\\newunicodechar{→}{\\ensuremath{\\to}}\n\\newunicodechar{⇒}{\\ensuremath{\\Rightarrow}}\n\\newunicodechar{α}{\\ensuremath{\\alpha}}\n\\newunicodechar{β}{\\ensuremath{\\beta}}\n\\newunicodechar{γ}{\\ensuremath{\\gamma}}\n\\newunicodechar{λ}{\\ensuremath{\\lambda}}\n\\newunicodechar{φ}{\\ensuremath{\\varphi}}\n\\newunicodechar{ε}{\\ensuremath{\\varepsilon}}\n\\newunicodechar{σ}{\\ensuremath{\\sigma}}\n\\newunicodechar{θ}{\\ensuremath{\\theta}}\n\\newunicodechar{δ}{\\ensuremath{\\delta}}\n\\newunicodechar{η}{\\ensuremath{\\eta}}\n\\newunicodechar{π}{\\ensuremath{\\pi}}\n\\newunicodechar{ξ}{\\ensuremath{\\xi}}\n\\newunicodechar{Σ}{\\ensuremath{\\Sigma}}\n\\newunicodechar{Δ}{\\ensuremath{\\Delta}}\n\\newunicodechar{∂}{\\ensuremath{\\partial}}\n\\newunicodechar{∀}{\\ensuremath{\\forall}}\n\\newunicodechar{∃}{\\ensuremath{\\exists}}\n\\newunicodechar{√}{\\ensuremath{\\surd}}\n\\newunicodechar{−}{\\ensuremath{-}}\n\\newunicodechar{μ}{\\ensuremath{\\mu}}\n\\newunicodechar{ρ}{\\ensuremath{\\rho}}\n\\newunicodechar{τ}{\\ensuremath{\\tau}}\n\\newunicodechar{ω}{\\ensuremath{\\omega}}\n\\newunicodechar{Ω}{\\ensuremath{\\Omega}}\n\\newunicodechar{χ}{\\ensuremath{\\chi}}\n\\newunicodechar{ψ}{\\ensuremath{\\psi}}\n\\newunicodechar{Γ}{\\ensuremath{\\Gamma}}\n\\newunicodechar{Φ}{\\ensuremath{\\Phi}}\n\\newunicodechar{Λ}{\\ensuremath{\\Lambda}}\n\\newunicodechar{ℝ}{\\ensuremath{\\mathbb{R}}}\n\\newunicodechar{ℤ}{\\ensuremath{\\mathbb{Z}}}\n\\newunicodechar{ℕ}{\\ensuremath{\\mathbb{N}}}\n\\newunicodechar{△}{\\ensuremath{\\triangle}}\n\\newunicodechar{⊗}{\\ensuremath{\\otimes}}\n.agent/hdu-ocr/compile.py\n.agent/hdu-ocr/build.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pymupdf/_build.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pyarrow/tests/test_builder.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pyarrow/tests/test_convert_builtin.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/attrs/converters.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/cffi/recompiler.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/models/nemotron_asr/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pygments/lexers/compiled.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/models/fun_asr_nano/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/codec/models/stepaudio2/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/datasets/builder.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/codec/models/mimo_audio_tokenizer/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/models/parakeet/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/models/moss_music/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/models/mega_asr/convert_router.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/models/mega_asr/convert_lora.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/models/mega_asr/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/lm/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/starlette/convertors.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/tests/mega_asr/test_convert_router.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/tests/mega_asr/test_convert_lora.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/stt/tests/mega_asr/test_convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/datasets/packaged_modules/folder_based_builder/folder_based_builder.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/sts/models/mel_roformer/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/dateutil/zoneinfo/rebuild.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/sts/models/nemotron_voicechat/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/sts/models/dialogue_sidon/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/sts/models/deepfilternet/scripts/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/vad/models/fsmn/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/vad/models/nemotron_diarization/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/vad/models/sortformer/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pip/_internal/build_env.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pip/_internal/wheel_builder.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/plotting/_matplotlib/converter.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/sympy/parsing/autolev/_build_autolev_antlr.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pip/_internal/operations/build/build_tracker.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/jinja2/compiler.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pip/_internal/utils/setuptools_build.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mpmath/tests/test_convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/sympy/parsing/latex/_build_latex_antlr.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/tests/indexes/datetimes/methods/test_tz_convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/numpy/testing/_private/extbuild.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/sympy/tensor/array/expressions/tests/test_convert_array_to_indexed.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/sympy/tensor/array/expressions/tests/test_convert_matrix_to_array.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/sympy/tensor/array/expressions/tests/test_convert_indexed_to_array.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/sympy/tensor/array/expressions/tests/test_convert_array_to_matrix.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/bailingmm/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/attr/converters.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/transformers/convert_slow_tokenizers_checkpoints_to_fast.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/dramabox/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/transformers/convert_slow_tokenizer.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/tests/scalar/timestamp/methods/test_tz_convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/tests/series/methods/test_convert_dtypes.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/melotts/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/confucius4/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/chatterbox/scripts/convert_chatterbox.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/chatterbox/scripts/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/omnivoice/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/zonos2/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/tests/frame/methods/test_tz_convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/tests/frame/methods/test_convert_dtypes.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/models/kitten_tts/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/moge3/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_audio/tts/tests/test_convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/tests/plotting/test_converter.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/ernie_image/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pandas/tests/io/parser/test_converters.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/rt_detr_v2/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/sam3d_body/convert_weights.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/rfdetr/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/ming_image/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/mage_flow/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/sam3_1/convert_weights.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/pp_doclayout_v3/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/qwen_image/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/sam3d_objects/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/yolo11/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/nemotron_voicechat/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/deepseek_v4/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/minimax_h3/convert.py\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/mlx_vlm/models/z_image/convert.py\n"}

## tool · 2026-10-19T07:21:28Z


Script completed
Wall time 0.3 seconds
Output:

Warning: truncated output (original token count: 14791)
Total output lines: 1261

import hashlib
import json
import os
import subprocess
from concurrent.futures import ThreadPoolExecutor
from pathlib import Path

ROOT = Path(__file__).resolve().parents[2]
WORK = ROOT / '.agent/hdu-ocr'
OUT = ROOT / 'output/HDU'
BIN = Path('/Volumes/SamsungSSD990PRO/Application/texlive/2025/bin/universal-darwin')
environment = dict(os.environ, PATH=str(BIN) + os.pathsep + os.environ['PATH'])
def compile_document(path):
    digest = hashlib.sha256(path.read_bytes()).hexdigest()
    target = WORK / 'build' / hashlib.sha256(str(path).encode()).hexdigest()[:16]
    target.mkdir(parents=True, exist_ok=True)
    stamp = target / 'success.json'
    if stamp.exists() and json.loads(stamp.read_text())['sha256'] == digest:
        return json.loads(stamp.read_text())
    result = subprocess.run([str(BIN / 'xelatex'), '-interaction=nonstopmode', '-halt-on-error', '-file-line-error', '-output-directory=' + str(target), str(path)], cwd=path.parent, env=environment, capture_output=True, text=True, timeout=120)
    (target / 'command.txt').write_text(result.stdout + result.stderr)
    lines = result.stdout.splitlines()
    errors = [line for line in lines if line.startswith('!') or ': ' in line and ('Error' in line or 'Undefined' in line or 'Missing' in line or 'Extra' in line or 'Misplaced' in line)]
    record = {'path': str(path.relative_to(OUT)), 'sha256': digest, 'exit_code': result.returncode, 'errors': errors, 'log': str(target / 'command.txt')}
    if result.returncode == 0:
        stamp.write_text(json.dumps(record, ensure_ascii=False, indent=2))
    print(json.dumps(record, ensure_ascii=False), flush=True)
    return record


with ThreadPoolExecutor(max_workers=4) as executor:
    results = list(executor.map(compile_document, sorted((OUT / 'latex').rglob('*.tex'))))
(WORK / 'compile-results.json').write_text(json.dumps(results, ensure_ascii=False, indent=2))
print(json.dumps({'passed': sum(r['exit_code'] == 0 for r in results), 'failed': sum(r['exit_code'] != 0 for r in results)}), flush=True)
import hashlib
import json
import re
import subprocess
import unicodedata
from pathlib import Path

import pypandoc

ROOT = Path(__file__).resolve().parents[2]
WORK = ROOT / '.agent/hdu-ocr'
OUT = ROOT / 'output/HDU'
PANDOC = pypandoc.get_pandoc_path()


def normalize(text):
    text = ''.join(unicodedata.normalize('NFKC', c) if 'MATHEMATICAL' in unicodedata.name(c, '') else c for c in text)
    text = re.sub(r'(?<![\\$])\$(?!\$)([^$\n]+?)\$(?!\$)', lambda m: '$' + m[1].strip() + '$', text)
    text = re.sub(r'\\operatorname\s*\*?\s*\{\s*l\s*i\s*m\s*\}', r'\\lim', text)
    text = re.sub(r'\\operatorname\s*\{\s*r\s*a\s*n\s*k\s*\}', r'\\operatorname{rank}', text)
    text = re.sub(r'\\mathscr\s*\{(\s*[a-z]\s*)\}', r'\\mathit{\1}', text)
    lines = [line for line in text.splitlines() if not re.fullmatch(r'\s*(淘宝[/／]微店.*|专注数学专业历年真题解析.*|微信公众号[：:].*|宝哥\s*1[0-9 ]+(或\s*1[0-9 ]+)?)\s*', line)]
    return '\n'.join(lines).strip() + '\n'


def write_pair(subject, year, name, text, source=None, pages=None):
    md = OUT / 'md' / subject / str(year) / (name + '.md')
    tex = OUT / 'latex' / subject / str(year) / (name + '.tex')
    md.parent.mkdir(parents=True, exist_ok=True)
    tex.parent.mkdir(parents=True, exist_ok=True)
    if source:
        text = '# ' + name + '\n\n来源：`' + source + '`。原 PDF 页序：' + ', '.join(map(str, pages)) + '。\n\n' + text
    text = normalize(text)
    md.write_text(text)
    result = subprocess.run([PANDOC, '-f', 'markdown+tex_math_dollars+tex_math_single_backslash', '-t', 'latex', '--standalone', '-V', 'documentclass=ctexart', '-V', 'classoption=fontset=fandol', '-V', 'mathspec=true', '-V', 'geometry:margin=23mm', '-V', 'fontsize=11pt', '-H', str(WORK / 'header.tex'), str(md), '-o', str(tex)], capture_output=True, text=True)
    if result.returncode:
        raise ValueError({'source': source, 'pandoc': result.stderr})
    return {'md': str(md.relative_to(OUT)), 'latex': str(tex.relative_to(OUT)), 'source': source, 'pages': pages}


def build():
    jobs = json.loads((WORK / 'jobs.json').read_text())
    outputs = []
    for job in jobs:
        source = Path(job['source'])
        year = source.parent.name
        subject = '高等代数' if '双科' in source.name else '数学分析'
        key = hashlib.sha256(job['input'].encode()).hexdigest()[:16]
        raw = WORK / (key + '.md')
        text = raw.read_text()
        local = WORK / 'local' / source.stem
        if year == '2026' and source.name.endswith('601数学分析考研真题.pdf'):
            text = '\n\n'.join((local / f'{n:03d}.md').read_text() for n in job['pages'])
        if year == '2025' and '双科' in source.name:
            text = '\n\n'.join((local / f'{n:03d}.md').read_text() for n in job['pages'])
        if year == '2026' and '双科' in source.name:
            text = text.replace('设是线性空间V上的线性变换', '设$\\varphi$是线性空间V上的线性变换')
        override = WORK / 'overrides' / (key + '.md')
        if override.exists():
            text = override.read_text()
        if subject == '高等代数' and '真题及答案' in source.name:
            marker = re.search(r'^#{1,3}\s*杭州电子科技大学' + year + r'年高等代数真题解析', text, re.M)
            if marker is None:
                raise ValueError('未找到高等代数题目和答案分界: ' + str(source))
            exam_pages = [p for p in job['pages'] if p <= 2]
            answer_pages = [p for p in job['pages'] if p > 2]
            outputs.append(write_pair(subject, year, year + '年高等代数真题', text[:marker.start()], str(source), exam_pages))
            outputs.append(write_pair(subject, year, year + '年高等代数参考答案', text[marker.start():], str(source), answer_pages))
        else:
            name = source.stem if subject == '数学分析' else year + '年高等代数真题' + ('（手写异文版）' if year == '2023' else '')
            outputs.append(write_pair(subject, year, name, text, str(source), job['pages']))
    for supplement in sorted((WORK / 'supplements').glob('*/*/*.md')):
        subject, year = supplement.parts[-3:-1]
        outputs.append(write_pair(subject, year, year + '年' + subject + '补充解析', supplement.read_text()))
    manifest = {'sources': json.loads((WORK / 'inventory.json').read_text()), 'outputs': outputs}
    (OUT / '识别清单.json').write_text(json.dumps(manifest, ensure_ascii=False, indent=2))
    print(json.dumps({'documents': len(outputs), 'markdown': len(list((OUT / 'md').rglob('*.md'))), 'latex': len(list((OUT / 'latex').rglob('*.tex')))}, ensure_ascii=False))


if __name__ == '__main__':
    assert normalize('$ x $') == '$x$\n'
    assert normalize(r'$\operatorname* { l i m } x$') == '$\\lim x$\n'
    build()
This is XeTeX, Version 3.141592653-2.6-0.999997 (TeX Live 2025) (preloaded format=xelatex)
 restricted \write18 enabled.
entering extended mode

(/Users/oyamahappa/Documents/Agent/Codex/output/HDU/latex/数学分析/2018/2018年杭州电子科技
大学601数学分析考研真题参考答案.tex
LaTeX2e <2024-11-01> patch level 2
L3 programming layer <2025-01-18>

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
texart.cls
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctexbackend.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3kern
el/expl3.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3back
end/l3backend-xetex.def))
Document Class: ctexart 2022/07/14 v2.5.10 Chinese adapter for class article (C
TEX)

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
texhook.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
texpatch.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/f
ix-cm.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/t
s1enc.def))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctexopts.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/a
rticle.cls
Document Class: article 2024/06/29 v1.4n Standard LaTeX document class

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/s
ize11.clo))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/e
ngine/ctex-engine-xetex.def
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/xelatex/xecj
k/xeCJK.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3pack
ages/xtemplate/xtemplate.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/fontsp
ec/fontspec.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3pack
ages/xparse/xparse.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/fontsp
ec/fontspec-xetex.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/f
ontenc.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/fontsp
ec/fontspec.cfg)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/xelatex/xecj
k/xeCJK.cfg)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/zhnumb
er/zhnumber.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/zhnumb
er/zhnumber-utf8.cfg))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/s
cheme/ctex-scheme-chinese-article.def
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctex-name-utf8.cfg)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctex.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/xcolor
/xcolor.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs-cfg/color.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs-def/xetex.def)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs/mathcolor.ltx))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/geomet
ry/geometry.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs/keyval.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/ifte
x/ifvtex.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/ifte
x/iftex.sty)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsmath.sty
For additional information on amsmath, use the `?' option.

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amstext.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsgen.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsbsy.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsopn.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/amssymb.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/amsfonts.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/unicod
e-math/unicode-math.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/unicod
e-math/unicode-math-xetex.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3pack
ages/l3keys2e/l3keys2e.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/unicod
e-math/unicode-math-table.tex)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/lmo
dern.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/upquot
e/upquote.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/t
extcomp.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/microtype.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/etoolb
ox/etoolbox.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/microtype-xetex.def)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/microtype.cfg))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/parski
p/parskip.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/kvopti
ons/kvoptions.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/ltxc
mds/ltxcmds.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/kvsetk
eys/kvsetkeys.sty))
Couldn't patch \@startsection
Couldn't patch \@xsect
)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/mathto
ols/…8291 tokens truncated…This is XeTeX, Version 3.141592653-2.6-0.999997 (TeX Live 2025) (preloaded format=xelatex)
 restricted \write18 enabled.
entering extended mode

(/Users/oyamahappa/Documents/Agent/Codex/output/HDU/latex/数学分析/2023/2023年杭州电子科技
大学601数学分析考研真题参考答案.tex
LaTeX2e <2024-11-01> patch level 2
L3 programming layer <2025-01-18>

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
texart.cls
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctexbackend.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3kern
el/expl3.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3back
end/l3backend-xetex.def))
Document Class: ctexart 2022/07/14 v2.5.10 Chinese adapter for class article (C
TEX)

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
texhook.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
texpatch.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/f
ix-cm.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/t
s1enc.def))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctexopts.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/a
rticle.cls
Document Class: article 2024/06/29 v1.4n Standard LaTeX document class

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/s
ize11.clo))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/e
ngine/ctex-engine-xetex.def
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/xelatex/xecj
k/xeCJK.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3pack
ages/xtemplate/xtemplate.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/fontsp
ec/fontspec.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3pack
ages/xparse/xparse.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/fontsp
ec/fontspec-xetex.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/f
ontenc.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/fontsp
ec/fontspec.cfg)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/xelatex/xecj
k/xeCJK.cfg)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/zhnumb
er/zhnumber.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/zhnumb
er/zhnumber-utf8.cfg))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/s
cheme/ctex-scheme-chinese-article.def
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctex-name-utf8.cfg)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/ctex/c
onfig/ctex.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/xcolor
/xcolor.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs-cfg/color.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs-def/xetex.def)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs/mathcolor.ltx))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/geomet
ry/geometry.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs/keyval.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/ifte
x/ifvtex.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/ifte
x/iftex.sty)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsmath.sty
For additional information on amsmath, use the `?' option.

(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amstext.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsgen.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsbsy.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsmat
h/amsopn.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/amssymb.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/amsfonts.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/unicod
e-math/unicode-math.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/unicod
e-math/unicode-math-xetex.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/l3pack
ages/l3keys2e/l3keys2e.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/unicod
e-math/unicode-math-table.tex)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/lmo
dern.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/upquot
e/upquote.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/t
extcomp.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/microtype.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/etoolb
ox/etoolbox.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/microtype-xetex.def)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/microtype.cfg))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/parski
p/parskip.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/kvopti
ons/kvoptions.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/ltxc
mds/ltxcmds.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/kvsetk
eys/kvsetkeys.sty))
Couldn't patch \@startsection
Couldn't patch \@xsect
)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/mathto
ols/mathtools.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/tools/
calc.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/mathto
ols/mhsetup.sty)

Package mathtools Warning: For best results, please load mathtools *before* 
(mathtools)                unicode-math on input line 127.

)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/jknapl
tx/mathrsfs.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/esint/
esint.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/tools/
bm.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/newuni
codechar/newunicodechar.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/bookma
rk/bookmark.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/hyperr
ef/hyperref.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/kvde
finekeys/kvdefinekeys.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/pdfe
scape/pdfescape.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/pdft
excmds/pdftexcmds.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/infw
arerr/infwarerr.sty)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/hycolo
r/hycolor.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/hyperr
ef/nameref.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/refcou
nt/refcount.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/gett
itlestring/gettitlestring.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/stri
ngenc/stringenc.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/hyperr
ef/pd1enc.def)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/intc
alc/intcalc.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/hyperr
ef/puenc.def)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/url/ur
l.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/bits
et/bitset.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/bigi
ntcalc/bigintcalc.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/a
tbegshi-ltx.sty))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/hyperr
ef/hxetex.def
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/rerunf
ilecheck/rerunfilecheck.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/base/a
tveryend-ltx.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/generic/uniq
uecounter/uniquecounter.sty)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/bookma
rk/bkm-dvipdfm.def))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/xurl/x
url.sty)
No file 2023年杭州电子科技大学601数学分析考研真题参考答案.aux.
*geometry* driver: auto-detecting
*geometry* detected driver: xetex

Package unicode-math Warning: Using \overbracket and \underbracket from
(unicode-math)                `mathtools' package.
(unicode-math)                 
(unicode-math)                 Use \Uoverbracket and \Uunderbracket for
(unicode-math)                original `unicode-math' definition.


Package unicode-math Warning: I'm going to overwrite the following commands
(unicode-math)                from the `mathtools' package: 
(unicode-math)                 
(unicode-math)                     \dblcolon, \coloneqq, \Coloneqq, \eqqcolon.
(unicode-math)                
(unicode-math)                 
(unicode-math)                 Note that since I won't overwrite the other
(unicode-math)                colon-like commands, using them will lead to
(unicode-math)                inconsistencies.


(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs/graphicx.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs/graphics.sty
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs/trig.sty)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/graphi
cs-cfg/graphics.cfg)))

Package hyperref Warning: Rerun to get /PageLabels entry.


Package xeCJK Warning: Unknown CJK family `\CJKttdefault' is being ignored.
(xeCJK)                
(xeCJK)                Try to use `\setCJKmonofont[<...>]{<...>}' to define
(xeCJK)                it.


(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/oml
lmm.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/umsa.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/mt-msa.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/umsb.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/mt-msb.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/jknapl
tx/ursfs.fd)

LaTeX Font Warning: Font shape `U/rsfs/m/n' in size <5.475> not available
(Font)              size <5> substituted on input line 108.


(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/esint/
uesint.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/ot1
lmr.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/mt-LatinModernRoman.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/oms
lmsy.fd)

LaTeX Font Warning: Font shape `TU/SongtiSC(0)/m/sl' undefined
(Font)              using `TU/SongtiSC(0)/m/n' instead on input line 151.

[1]
[2]
[3]
Missing character: There is no  (U+F047) in font Times New Roman/OT:script=lat
n;language=dflt;mapping=tex-text;!

[4]
[5]
[6]
Missing character: There is no △ (U+25B3) in font Times New Roman/OT:script=lat
n;language=dflt;mapping=tex-text;!
/Users/oyamahappa/Documents/Agent/Codex/output/HDU/latex/数学分析/2023/2023年杭州电子科技大
学601数学分析考研真题参考答案.tex:432: Argument of \end  has an extra }.
<inserted text> 
                \par 
l.432 ...z ^ { 2 } } } ) \nu + 2 (  \frac   \ \end
                                                  {array}
Output written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/
d64a56cfc09b0440/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf (6 pages).
Transcript written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/bu
ild/d64a56cfc09b0440/2023年杭州电子科技大学601数学分析考研真题参考答案.log.


## tool · 2026-10-19T07:21:38Z


Script completed
Wall time 0.7 seconds
Output:

Underfull \hbox (badness 2644) in paragraph at lines 245--253
[]$[] [] [][][][] [][]$ \TU/TimesNewRoman(0)/m/n/10.95 =v |\TU/SongtiSC(0)/m/n/
10.95 （\TU/TimesNewRoman(0)/m/n/10.95 x\TU/SongtiSC(0)/m/n/10.95 ，| \TU/TimesNe
wRoman(0)/m/n/10.95 y\TU/SongtiSC(0)/m/n/10.95 ）|  是 由 $[]$ 所 确 定 的 隐 函 数 组，|  
在 此 方 程 组 的 两 边 取

Underfull \hbox (badness 5133) in paragraph at lines 245--253
\TU/SongtiSC(0)/m/n/10.95 全 微 分，|  可 得 $[]$ ，|  求 解 这 个 关 于 $[][][] [][]$ 的 方 程
 组，|  可 得

[3]
[4]
[5]
Overfull \hbox (5.2104pt too wide) detected at line 384
[]
/Users/oyamahappa/Documents/Agent/Codex/output/HDU/latex/数学分析/2018/2018年杭州电子科技大
学601数学分析考研真题参考答案.tex:432: Extended mathchar used as mathchar (14799973).
<to be read again> 
                   \relax 
l.432 \(\boldsymbol { x }
                          _ { n } \in \left[ a , b \right]\)
Output written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/
987d0950f99979fc/2018年杭州电子科技大学601数学分析考研真题参考答案.pdf (5 pages).
Transcript written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/bu
ild/987d0950f99979fc/2018年杭州电子科技大学601数学分析考研真题参考答案.log.
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/mt-LatinModernRoman.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/oms
lmsy.fd)

LaTeX Font Warning: Command \scriptsize invalid in math mode on input line 139.




LaTeX Font Warning: Font shape `TU/SongtiSC(0)/m/sl' undefined
(Font)              using `TU/SongtiSC(0)/m/n' instead on input line 152.

[1]
/Users/oyamahappa/Documents/Agent/Codex/output/HDU/latex/数学分析/2019/2019年杭州电子科技大
学601数学分析考研真题.tex:192: Improper alphabetic constant.
<to be read again> 
                   \mitxi 
l.192 \(f ^ { \prime } ( { \boldsymbol { \xi }
                                               } _ { 1 } ) = f ^ { \prime } ...

Output written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/
630465da14431cc4/2019年杭州电子科技大学601数学分析考研真题.pdf (1 page).
Transcript written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/bu
ild/630465da14431cc4/2019年杭州电子科技大学601数学分析考研真题.log.
uesint.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/ot1
lmr.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/mt-LatinModernRoman.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/oms
lmsy.fd)

LaTeX Font Warning: Font shape `TU/SongtiSC(0)/m/sl' undefined
(Font)              using `TU/SongtiSC(0)/m/n' instead on input line 147.

[1]
[2]
[3]
/Users/oyamahappa/Documents/Agent/Codex/output/HDU/latex/数学分析/2021/2021年杭州电子科技大
学601数学分析考研真题参考答案.tex:282: Extended mathchar used as mathchar (14799974).
<to be read again> 
                   \relax 
l.282 f _ { \boldsymbol { y }
                              } ( 0 , 0 ) = \lim _ { \boldsymbol { y } \to 0...

Output written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/build/
d3c71ea109b67c64/2021年杭州电子科技大学601数学分析考研真题参考答案.pdf (3 pages).
Transcript written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/bu
ild/d3c71ea109b67c64/2021年杭州电子科技大学601数学分析考研真题参考答案.log.
杭州电子科技大学2023年数学分析解答

## 一、填空题（每小题5分）

1.已知 $f ( x ) = \frac { x } { \sqrt { 1 + x ^ { 2 } } } , 1 fint _ { x } f _ { n } ( x ) = f \{ f ( \cdots f ( n ) ) \} . \textcircled { n } 1 f _ { 2 0 2 3 } ^ { 1 } ( 0 ) =$

解、由 $f _ { 1 } ( x ) = f ( x ) = \frac { x } { \sqrt { 1 + x ^ { 2 } } }$

$$
f _ { 2 } ( x ) = f ( f ( x ) ) = \frac { x } { \sqrt { 1 + x ^ { 2 } } } / \sqrt { 1 + ( \frac { x } { \sqrt { 1 + x ^ { 2 } } } ) ^ { 2 } } = \frac { x } { \sqrt { 1 + 2 x ^ { 2 } } }
$$

$$
f _ { 0 } ( x ) = \frac { x } { \sqrt { 1 + n x ^ { 2 } } } \qquad \mp \frac { \theta } { x } \frac { f } { 2 0 2 3 } ( x ) = \frac { x } { \sqrt { 1 + 2 0 2 3 x ^ { 2 } } }
$$

$2 ⨏ \limits _ { 2 0 } ^ { 1 } a 3 ( x ) = \frac { 1 } { ( 1 + 2 0 2 3 x ^ { 2 } ) ^ { \frac { 3 } { 2 } } }$ 则 $f ^ { \prime } _ { 2 0 2 3 } ( \pmb { \mathscr { o } } ) = 1$

2. $\lim \limits _ { n  \infty } n ( \sqrt { n ^ { 2 } + 1 } - n ) =$

解： $I = \frac { \min } { \max } = \frac { \min ( \sqrt { n + 1 } - n ) ( \sqrt { n + 1 } + n ) } { \sqrt { n + 1 } + n } = \frac { \min } { \max } = \frac { 1 } { 2 }$

3.设f（x）在[a，b]上连续. $F ( x ) = \int \limits _ { a } ^ { x }$ f(t)(t-x）dt .则 $F ^ { \prime } ( x ) =$

解： $F ( x ) = \int \limits _ { a } ^ { x } f ( t ) \cdot t d t - x \int \limits _ { a } ^ { x } f ( t ) d t$

$$
F ^ { \prime } ( x ) = x f ( x ) - \int \limits _ { a } ^ { x } f ( t ) d t - x f ( x ) = - \int \limits _ { a } ^ { x } f ( t ) d t
$$

$$
4 . \int \limits _ { - \infty } ^ { + \infty } e ^ { - x ^ { 2 } } d x =
$$

解翠： $E u l e r - P O i s s o n$ 积分： $\int \limits _ { 0 } ^ { + \infty } e ^ { - x ^ { 2 } } d x = \frac { \sqrt { \pi } } { 2 }$

$$
\int \limits _ { - \infty } ^ { + \infty } e ^ { - x ^ { 2 } } d x = 2 \int \limits _ { 0 } ^ { + \infty } e ^ { - x ^ { 2 } } d x = 2 \cdot \frac { \sqrt { \pi } } { 2 } = \sqrt { \pi }
$$

5.函数 $f ( x ) = \left\{ \begin{array} { l l } { \cos \frac { x x } { 2 } \cdot \vert x \vert \leq 1 } \\ { \vert x - 1 \vert , \vert x \vert > 1 } \end{array} \right.$ 的间断点为

解： $\vert \lim \limits _ { x  1 } f ( x ) = \frac { \vert \sin \vert x - 1 \vert } { x + 1 ^ { 4 } } = 0 , \frac { \vert \sin \cdot f ( x ) \vert } { x + 1 ^ { 4 } } = \frac { \vert \sin \cdot \cos \frac { x - x } { 2 } } { x + 1 ^ { 2 } } = 0$

$2 f ( 1 ) = \cos \frac { \pi } { 2 } = 0$ 则f（x）在=丨处连续

$$
\operatorname* { l i m } _ { x ( x - 1 ) ^ { \ast } } f ( x ) = \operatorname* { l i m } _ { x + 1 } \cos \frac { x x } { 2 } = 0 , \operatorname* { l i m } _ { x \in 2 - 1 } f ( x ) = \operatorname* { l i m } _ { x \in 2 - 1 } \vert x - 1 \vert = 2
$$

则f（）在x=处间断

6.级数 $\sum \limits _ { n = 2 } ^ { \infty } ( 1 + \frac { 1 } { n } ) ^ { n ( n + 1 ) } x ^ { n }$ 的收敛半径为__

解：记 $U _ { n } = ( 1 + \frac { 1 } { n } ) ^ { n ( n + 1 ) }$

$$
\rho = \operatorname* { l i m } _ { n  \infty } \sqrt [ n ] { \vert u _ { n } \vert } = \operatorname* { l i m } _ { n  \infty } ( 1 + \frac { 1 } { n } ) ^ { n + 1 } = e \cdot R = \frac { 1 } { \rho } = \frac { 1 } { e }
$$

7.设曲线L是圆 $x ^ { 2 } + y ^ { 2 } = r ^ { 2 }$ 在第一象限内的部分，则 $\int \limits _ { L } x y d S =$

解： $\int \limits _ { \Delta } x y d s = \int \limits _ { 0 } ^ { \frac { \pi } { 2 } } r ^ { 3 } \sin \theta \cos \theta d \theta = \frac { 1 } { 2 } r ^ { 3 } \sin ^ { 2 } \theta \cdot \frac { \pi } { 2 } = \frac { 1 } { 2 } r ^ { 3 }$

8. $\int \frac { 1 } { x ( 1 + x ^ { n } ) } d x =$

解：令 $t = x ^ { n }$ 则 $\int \frac { 1 } { x ( 1 + x ^ { n } ) } d x = \int \frac { x ^ { n - 1 } } { x ^ { n } ( 1 + x ^ { n } ) } d x = \frac { 1 } { n } ( \frac { d t } { t ( 1 + t ) } )$ =丨+

## 二.计算题（每小题10分）

1.计算 $\int _ { 2 } ( - 2 x e ^ { - x ^ { 2 } } \sin y ) d x + ( e ^ { - x ^ { 2 } } \cos y + x ^ { 6 } ) d y$

这里为从点（10）到（-1,O）的半圖 $y = \sqrt { 1 - x ^ { 2 } } ( - 1 \leq x \leq 1 )$

解：记L为从（-1,O）到（1，O）的直线段D为 $\angle \Xi \angle ^ { \prime }$ 所围成的封闭区域由Green公式

$$
\begin{array}{c} \frac { I _ { 1 } = \int \limits _ { \varDelta } \int \int \cdots \int \int \cdots \int \int \limits _ { \varDelta } ^ { - x ^ { 2 } } \sin y \mathrm { d } x + ( e ^ { - x ^ { 2 } } \cos y + x ^ { 6 } ) d y } { 2 \cdot \sqrt { \pi } \cdot \sqrt { \pi } \cdot \sqrt { \pi } \cdot \sqrt { \pi } } d x = 0 , \quad \mathrm { ~ f ~ } \quad \frac { \theta } { 1 } = \theta , \quad \mathrm { ~ f ~ o ~ a ~ \theta ~ } ,  \\ { = \frac { \theta \prod \limits _ { \theta = \theta } ^ { \theta } \sin y } { 2 } \frac { \sin ^ { 2 } y } { 2 \cdot \sin y \mathrm { d } x } = \theta \int \limits _ { \theta = \theta } ^ { x ^ { 2 } } \sin ^ { 3 } y \quad \frac { \theta } { 1 } = \theta \int \ _ { \theta = \theta } ^ { 1 } \sin ^ { 3 } y \quad \sin ^ { 3 } z = 0 , } \\ { \geq \int \frac { \theta } { 1 } = \int \int \limits _ { \theta = \theta } ^ { 1 } ( - 2 x \sin y - \sin y ) d x + ( e ^ { - x ^ { 2 } } \cos y + x ^ { 6 } ) d y = 0 , \quad \therefore \ \int \frac { \theta } { 1 } = I _ { 1 } + I _ { 2 } = 0 . } \end{array}
$$

2.求 $\lim \limits _ { x  \infty } [ x - x ^ { 2 } \ln ( 1 + \frac { 1 } { x } ) ]$

$$
\frac { \sin \frac { \pi } { 4 } + \theta } { \sin \alpha } = \frac { 1 } { x _ { 1 } - x _ { 1 } ^ { 2 } } = \frac { 1 } { x _ { 1 } } - \frac { 1 } { 2 x _ { 1 } ^ { 2 } } + \theta \frac { 1 } { x _ { 1 } ^ { 2 } } + \frac { 1 } { \sin \alpha }
$$

3.求 $\sum \limits _ { n = 1 } ^ { \infty } \frac { 2 n } { 3 ^ { n } }$ 的和

解：考虚幂级数 $S ( x ) = \sum \limits _ { n = 1 } ^ { \infty } \frac { 2 n } { 3 ^ { n } } x ^ { n }$ 记 $u _ { n } = \frac { 2 n } { 3 ^ { n } }$

$$
P = \frac { \vert \min - 1 \vert } { \max } = \frac { \vert \sin \cdot \sqrt [ 0 ] { \frac { 2 \pi } { 3 \cdot \sqrt { \frac { 1 } { 3 \cdot \sqrt { \frac { 1 } { 3 \cdot \sqrt { 3 } } } } } } } } { \min } = \frac { 1 } { 3 } \cdot \therefore R = \frac { 1 } { \rho } = 3
$$

当 $x = \pm 3$ 时，幂级数 $\sum \limits _ { n = 1 } ^ { \infty } \frac { 2 n } { 3 ^ { n } } x ^ { n }$ 发散，故其收敛域为 $( - 3 , 3 )$

$$
\begin{array} { r l } & { \frac { \Vert \tilde { \textbf { u } } \rvert } { \Vert \tilde { \textbf { u } } \Vert } \ \hat { \textbf { \ i } } _ { 2 } ^ { \otimes } ( \boldsymbol { \textbf { \ i } } ) = \ \frac { \langle \boldsymbol { \textbf { \sigma } } \rangle } { \Vert \boldsymbol { \textbf { \sigma } } } \ \frac { \langle \boldsymbol { \textbf { \sigma } } \rangle } { \Vert \boldsymbol { \textbf { \sigma } } } \textbf { \otimes } \ \frac { \langle \boldsymbol { \textbf { \sigma } } \rangle } { \Vert \boldsymbol { \textbf { \sigma } } } \ \frac { \langle \boldsymbol { \textbf { \sigma } } \rangle } { \vert \boldsymbol { \textbf { \sigma } } } \times \boldsymbol { \textbf { \sigma } } ^ { - 1 } \ \textbf { \otimes } \boldsymbol { \textbf { \sigma } } \times \boldsymbol { \textbf { \sigma } } ( \boldsymbol { \textbf { \sigma } } ) } \\ & { \frac { \Vert \boldsymbol { \textbf { \sigma } } \vert } { \Vert \boldsymbol { \textbf { \sigma } } \Vert } \left. \boldsymbol { \textbf { \sigma } } \boldsymbol { \textbf { \otimes } } \boldsymbol { \textbf { \sigma } } \right. \ \textbf { \sigma } = \ \left\lceil \begin{array} { l l } { \kappa } { \frac { \langle \boldsymbol { \textbf { \sigma } } \rangle } { \Vert \boldsymbol { \textbf { \sigma } } \Vert } } & { \frac { 2 } { \sqrt { \boldsymbol { \textbf { \sigma } } \cdot 1 } } \textbf { \sigma } \textbf { \otimes } \boldsymbol { \sigma } ^ { - 1 } \textbf { \otimes } \boldsymbol { \sigma } } \\ { \frac { \langle \boldsymbol { \textbf { \sigma } } \rangle } { \Vert \boldsymbol { \textbf { \sigma } } \Vert } } & { \frac { 1 } { \sqrt { \boldsymbol { \textbf { \sigma } } \cdot 1 } } \textbf { \otimes } \boldsymbol { \sigma } } \end{array} \right. = \ \frac { \langle \boldsymbol { \textbf { \sigma } } \rangle } { \Vert \boldsymbol { \textbf { \sigma } } \Vert } \ \left. \frac { \boldsymbol { \sigma } } { \boldsymbol { \textbf { \sigma } } \cdot 1 } \frac { \boldsymbol { \sigma } \boldsymbol { \eta } } { \Vert \boldsymbol { \textbf { \sigma } } \Vert } \boldsymbol { \textbf { \sigma } } \right. } \\ &  \qquad \times \ \frac  \langle \boldsymbol  \end{array}
$$

4.计算 $\phi _ { 2 } x ^ { 2 } y d x + y ^ { 2 } d y + z d z$ ，其中是圆柱 $x ^ { 2 } + y ^ { 2 } = 1$ 与平面 $x + z = 1$ 的交线.从已轴的正向看去，为逆时针方向

解：令 $x = 1 0 0 s \theta$ ，y=sinθ.Z=1-vcosθ.0∈[o,2π]

$$
\frac { 2 x ! \int \limits _ { 0 } ^ { x } \int \limits _ { \frac { 1 } { 2 } } ^ { x } \sin y d x + y ^ { 2 } d y + z d z = \int \limits _ { 0 } ^ { 2 x } \left[ - \cos ^ { 2 } \theta \sin ^ { 2 } \theta + \sin ^ { 2 } \theta \cos \theta + ( 1 - \cos \theta ) \sin \theta \right] d \theta }  = \int \limits _ { 0 } ^ { 2 x } \left( - \frac { 1 + \cos 2 \theta } { 2 } \right) \left( \frac { 1 - \cos 2 \theta } { 2 } \right) d \theta + \int \limits _ { 0 } ^ { 2 x } \sin \theta d \theta = - \frac { 1 } { 4 } \int \limits _ { 0 } ^ { 2 x } \left( \frac { 1 - \cos 2 \theta } { 2 } \right) d \theta = - \frac { x } { 4 }
$$

5.计算 $1 1 1 x ^ { 2 } \sqrt { x ^ { 2 } + y ^ { 2 } } d x d y d z$ ，V是曲面 $z = \sqrt { x ^ { 2 } + y ^ { 2 } }$ 与面 $z = x ^ { 2 } + y ^ { 2 }$ 所围区域.

解：记D为V在平面x0y上的投影，那 $\angle 1 D = \{ ( x , y ) \vert x ^ { 2 } + y ^ { 2 } \leq 1 \}$

$$
\frac  F \frac { 8 } { 4 } \frac { 8 } { x } I = \frac { 1 1 } { 9 } d x d y \int \frac { \sqrt { x + y ^ { 2 } } } { x ^ { 2 } + y ^ { 2 } } \times ^ { 2 } \sqrt { x ^ { 2 } + y ^ { 2 } } d z = \frac { 1 1 } { x + y ^ { 2 } + 1 } d ^ { 2 } - \sqrt { x ^ { 2 } + y ^ { 2 } } ( \sqrt { x + y ^ { 2 } } - x ^ { 2 } - y ^ { 2 } ) d x d y
$$

## 三.证明题（每小题10分)

1.证明： $\sum \limits _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } \frac { x ^ { 2 } + n } { n ^ { 2 } }$ 在住何有限区域[a.b]上-致连收敛，

而在实轴上任何一点都不绝对收敛

证：记 $a _ { n } ( x ) = ( - 1 ) ^ { n } , b _ { n } ( x ) = \frac { x ^ { 2 } + n } { n ^ { 2 } }$

() $\forall x \in [ a , b ] , \forall n$ 有 $\vert \frac { n } { k = 1 } ( - 1 ) ^ { k } \vert \leq 1$

(i) ∀xE[a.b], $\{ b _ { n } ( x ) \} \downarrow$ ;极限函数 $b ( x ) = \lim \limits _ { n  \infty } \frac { x ^ { n } + n } { n ^ { 2 } } = 0$

$$
\lim _ { x  \infty } \operatorname { s u p } _ { x \in [ a , b ] } \vert b _ { n } ( x ) - b ( x ) \vert = \lim _ { n  \infty } \operatorname { s u p } _ { x \in [ 0 , b ] } \frac { x ^ { 2 } + n } { n ^ { 2 } } = 0 \therefore b _ { n } ( x ) \\\Rightarrow 0
$$

由Dirichlet判别法 $\sum \limits _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } \frac { x ^ { 2 } + n } { n ^ { 2 } }$ 在[ab]上-致收敛

另一方面.VXER，有 $\vert ( - 1 ) ^ { n } \frac { x ^ { 2 } + n } { n ^ { 2 } } \vert = \frac { x ^ { 2 } + n } { n ^ { 2 } } \geq \frac { 1 } { n }$ 其中 $\sum \limits _ { n = 1 } ^ { \infty } \frac { 1 } { n }$ 发散

$\therefore \frac { 2 0 } { n } \vert ( - 1 ) ^ { n } \frac { x ^ { 2 } + n } { n ^ { 2 } } \vert$ 发散于是 $\sum \limits _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } \frac { x ^ { 2 } + n } { n ^ { 2 } }$ 在实轴上任何一点都不绝对收敛

2.设奇函数f（x）在[-1，1]上具有=阶导数，且f（1）=1.

证明：（1）存在 $f ( 0 , 1 )$ 使得 $f ^ { \prime } ( \frac { 0 } { 3 } ) = 1$

（2）存在 $\eta \in ( - 1 , 1 )$ 使得 $f ^ { \prime } ( n ) + f ^ { \prime } ( n ) = 1$

证：（1）令F（x）=f（x）-x由题知f（0）=0.f（）=l

那么F（O）=O.F（1）=O.由Rolle定理.3∈（O.1）.5.t $F ^ { \prime } ( \frac { 4 } { 3 } ) = 0$ 即 fig1=1

（2）令 $G ( x ) = e ^ { x } ( f ^ { \prime } ( x ) - 1 )$

由（1）知，g∈（01）.s.tf（g)=1.又f是奇函数 $] 3 , 6 ( - 1 , 0 ) . 5 , + 5 ( 3 , 1 ) = 1$

由Rolle定理 $y _ { 7 } \in ( \{ 3 , - \frac { 3 } { 3 } \} ) C ( - 1 , 1 ) , s + ( - 1 7 ) = 0$

即 $e ^ { 2 } + f ^ { \prime \prime } ( \eta ) + f ^ { \prime } ( \eta ) - 1 7 = 0$ 于是 $f ^ { \prime \prime } ( \eta ) + f ^ { \prime } ( \eta ) = 1$

3.设f（x）在[0，I]上连续，证明： $1 1 f ( 1 - y ) f ( x ) d x d y = \frac { 1 } { 2 } [ \int \limits _ { 0 } ^ { 1 } f ( x ) d x ] ^ { 2 } ,$

其中D是以O(00）.A(OI），B（1O）为顶点的三角形区域

证：由图（1） $( 1 + ( 1 - y ) + ( x ) d x d y = 1 6 + ( x ) d x \int \limits _ { 0 } ^ { 1 - x } + ( 1 - y ) d y$

$$
\frac { \frac { x } { 2 } + ( x - y ) } { 2 } \int \limits _ { 0 } ^ { 1 } + ( x ) d x \int \limits _ { x } ^ { 1 } + ( x ) d t = \int \limits _ { 0 } ^ { 1 } + ( x ) d x \int \limits _ { x } ^ { 1 } + ( y ) d y
$$

<!-- image-->

由图（2）.D=D.有 $1 ^ { 1 } _ { 0 } + \tan d x \int \limits _ { x } ^ { 1 } f ( y ) d y = \int \limits _ { 0 } ^ { 1 } + \tan d x \int \limits _ { 0 } ^ { x } + \tan d y$ 图（1）

是{-）f（ddy[fd{dy+fd{fd=²f(x）dx{fydy{(x²

<!-- image-->  
图（2）

4.已知△表示Laplace算符，证 $Q P : \Delta \phi C ( u v ) = ( \Delta u ) V + 2 \nabla u \nabla v + u ( \Delta v )$

这里Vv表示函数V在点（x，y，Z）处的梯度， $\therefore \angle B$ 表理示点乘

$$
\begin{array} { r l } & { \frac { \hat { \mathbf { y } } _ { i } ^ { \dagger } \mathbb { E } : \quad \dot { \mathbb { Q } } \quad \Delta ( \boldsymbol { u } \boldsymbol { v } ) = \ \frac { \boldsymbol { \hat { q } } ^ { \top } ( \boldsymbol { u } \boldsymbol { v } ) } { \partial \hat { x } ^ { * } } + \ \frac { \partial ^ { 2 } ( \boldsymbol { u } \boldsymbol { v } ) } { \partial \boldsymbol { y } ^ { 2 } } + \ \frac { \partial ^ { 2 } ( \boldsymbol { u } \boldsymbol { v } ) } { \partial \boldsymbol { z } ^ { 2 } } } { \partial \boldsymbol { z } ^ { 2 } } } \\ & { \qquad = \ \boldsymbol { u } \left( \frac { \partial \hat { \mathbf { u } } } { \partial x ^ { * } } + \frac { \partial ^ { 3 } } { \partial \boldsymbol { y } ^ { * } } + \frac { \partial ^ { 3 } } { \partial \boldsymbol { z } ^ { * } } \right) + \ \nabla \left( \frac { \partial \hat { \nabla } } { \partial x ^ { * } } + \frac { \partial ^ { 3 } } { \partial \boldsymbol { y } ^ { * } } + \frac { \partial ^ { 3 } } { \partial \boldsymbol { z } ^ { * } } \right) } \\ & { \qquad + \ 2 \left( \frac { \partial \boldsymbol { u } } { \partial x } \cdot \frac { \partial { \boldsymbol { v } } } { \partial \boldsymbol { x } } + \frac { \partial ^ { 4 } } { \partial \boldsymbol { y } } \cdot \frac { \partial { \boldsymbol { v } } } { \partial \boldsymbol { y } } + \frac { \partial { \boldsymbol { u } } } { \partial \boldsymbol { z } } \cdot \frac { \partial { \boldsymbol { v } } } { \partial \boldsymbol { z } } \right) } \\ & { \qquad = \ \boldsymbol { u } ( \Delta \boldsymbol { v } ) + 2 \nabla \boldsymbol { u } \cdot \nabla \boldsymbol { v } + \nabla ( \Delta \boldsymbol { u } ) } \end{array}
$$

## 四综合题

1.（10分）求两个曲面 $x + 2 y = 1 \textcircled { + } x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 的交线上距离原点最近的点解：在约束条件x+2y=1和 $x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 下求 $d = x ^ { 2 } + y ^ { 2 } + z ^ { 2 } \theta . 7$ 最小值点

设 $L ( x , y , z , \lambda , \mu ) = x ^ { 2 } + y ^ { 2 } + z ^ { 2 } + \lambda ( x + 2 y - 1 ) + \mu ( x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } - 1 )$

$$
\angle x = 2 x + x + 2 \mu x = 0
$$

由Lagranye乘数法

$$
L y = 2 y + 2 \lambda + 4 \lambda y = 0
$$

解得 $( x , y , z ) = ( - \frac { 2 } { 3 } , \frac { 2 } { 3 } , 0 )$

$$
\angle z = 2 z + 2 z M = 0
$$

共就是最小值点

$$
\angle \lambda = x + 2 y - 1 = 0
$$

$$
L _ { M } = x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } - 1 = 0
$$

2.（20分）.设 $f ( x ) = \int \limits _ { 1 } ^ { + \infty } \frac { \cos ( x + 1 ) } { t ( 1 + t ^ { 2 } ) } d t$ $x \in ( - \infty , + \infty )$

(1）试证明积分 $\int \limits _ { 1 } ^ { + \infty } \frac { \cos x + } { t ( 1 + t ^ { 2 } ) }$ dt在 $( - \infty , + \infty )$ 上一致收敛.

（2）试证明f（x）在 $x \in ( - \infty , + \infty )$ 一致连续

证（1）（i) $\forall A > 1$ $\forall x \in ( - \infty , + \infty )$ 有 $1 \int \limits _ { a } ^ { A } \cos x + d t = 2$

lii）对每一个xER. $\frac { 1 } { t ( 1 + t ^ { 2 } ) }$ 为t的单调递减函数

且 $\forall x \in R$ 有 $\lim \limits _ { t  \infty } \frac { 1 } { t ( 1 + t ^ { 2 } ) } = 0$

由抉利克雷判别法 $\int _ { 1 } ^ { + \infty } \frac { \cos x t } { t ( 1 + t ^ { 2 } ) }$ dt在R上致收敛

（2) $\forall x _ { 1 } , x _ { 2 } \in$ R

$$
\frac { \frac { \sqrt { 3 } + \vert f ( u _ { 1 } ) - f ( u _ { 2 } ) \vert = \vert \sqrt { 3 } } { 4 } - \vert \langle x _ { 0 } \rangle \frac { \sqrt { 3 } } { 4 } - \langle x _ { 1 } \rangle \frac { \sqrt { 3 } } { 4 } + \vert x _ { 1 } \rangle } { \frac { \sqrt { 3 } } { 4 } + \vert x _ { 1 } \vert ^ { 2 } + \vert x _ { 2 } \vert ^ { 2 } } d t
$$

那么 $\forall E > 0$ 取 $s = \frac { 4 E } { \pi }$ $\forall x _ { 1 } , x _ { 2 } \in R : \vert x _ { 1 } - x _ { 2 } \vert < 8$

$$
\frac { x } { 3 } \vert f ( x , 1 ) - f ( x _ { 2 } ) \vert \leq \frac { x } { 4 } \vert x _ { 1 } - x _ { 2 } \vert < 8
$$

故f（x）在 $( - \infty , + \infty ) , 5 - \frac { \pi } { 2 } \Re \lambda ^ { \frac { 1 } { 2 } } - \frac { 3 \pi } { 2 }$

## tool · 2026-10-19T07:21:44Z


Script completed
Wall time 0.4 seconds
Output:

{'source': 'HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf', 'input': '/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/inputs/0d9cc42ce426da29.pdf', 'pages': [1, 2, 3, 4, 5, 6]}
# 杭州电子科技大学2023年数学分析真题解析

## 一.填空题

(本大题共 8 小题,每小题 5 分,共 40 分)

1.已知 $f ( x ) = \frac { x } { \sqrt { 1 + x ^ { 2 } } }$ $f _ { n } ( x ) = f ( f ( \cdots f ( x ) ) )$ ，则 $f _ { 2 0 2 3 } ( 0 ) =$

【解答】

注意到f(0)=0, $f _ { n } ( x ) = f ( f ( \cdots f ( x ) ) )$ ，故 $f _ { 2 0 2 3 } ( 0 ) = 0$

2. $\operatorname* { l i m } _ { n \to \infty } n ( { \sqrt { n ^ { 2 } + 1 } } - n ) =$

【解答】

$$
\begin{array} { l } { \displaystyle \operatorname* { l i m } _ { n \to \infty } n ( \sqrt { n ^ { 2 } + 1 } - n ) = \displaystyle \operatorname* { l i m } _ { n \to \infty } \frac { n ( \sqrt { n ^ { 2 } + 1 } - n ) ( \sqrt { n ^ { 2 } + 1 } + n ) } { \sqrt { n ^ { 2 } + 1 } + n } } \\ { = \displaystyle \operatorname* { l i m } _ { n \to \infty } \frac { n } { \sqrt { n ^ { 2 } + 1 } + n } = \displaystyle \operatorname* { l i m } _ { n \to \infty } \frac { 1 } { \sqrt { 1 + \displaystyle \frac { 1 } { n ^ { 2 } } } + 1 } = \frac { 1 } { 2 } } \end{array}
$$

3.设f(x)在[a,b]上连续, $F ( x ) = \int _ { a } ^ { x } f ( t ) ( t - x ) d t$ ，则F(x)在[a,b]上的 导数 $F ^ { \prime } ( x ) =$

## 【解答】

f(x)在[a,b]上连续, $F ( x ) = \int _ { a } ^ { x } f ( t ) ( t - x ) d t = \int _ { a } ^ { x } t f ( t ) d t - x \int _ { a } ^ { x } f ( t ) d t$ ，故 $F ^ { \prime } ( x ) = x f ( x ) - \int _ { a } ^ { x } f ( t ) d t - x f ( x ) = - \int _ { a } ^ { x } f ( t ) d t$

+8 e ²dx= 8

## 【解答】

分两步来计算这个积分.

(1)计算 $\iint _ { D } e ^ { - x ^ { 2 } - y ^ { 2 } } d x d y$ ，其中D是由中心在原点、半径为R的圆周所围成的区域.

<!-- image-->

$$
\iint e ^ { - x ^ { 2 } - y ^ { 2 } } d x d y = \int _ { 0 } ^ { R } e ^ { - r ^ { 2 } } r d r \int _ { 0 } ^ { 2 \pi } d \theta = \pi ( 1 - e ^ { - R ^ { 2 } } )
$$

$e ^ { - x ^ { 2 } - y ^ { 2 } }$ 关于x,y都是偶的，故

$$
\displaystyle \iint _ { x ^ { 2 } + y ^ { 2 } \le R ^ { 2 } , x , y \ge 0 } e ^ { - x ^ { 2 } - y ^ { 2 } } d x d y = \frac { 1 } { 4 } \pi ( 1 - e ^ { - R ^ { 2 } } )
$$

(2）计算反常积分 $\int _ { - \infty } ^ { + \infty } e ^ { - x ^ { 2 } } d x$

$$
( \int _ { - \infty } ^ { + \infty } e ^ { - x ^ { 2 } } d x ) ^ { 2 } = ( \operatorname* { l i m } _ { R  + \infty } \int _ { - R } ^ { R } e ^ { - x ^ { 2 } } d x ) ^ { 2 } = \operatorname* { l i m } _ { R  + \infty } \int _ { - R } ^ { R } e ^ { - x ^ { 2 } } d x \int _ { - R } ^ { R } e ^ { - y ^ { 2 } } d y = \operatorname* { l i m } _ { R  + \infty } \int _ { - R } ^ { R } \int _ { - R } ^ { R } e ^ { - ( x ^ { 2 } + y ^ { 2 } ) } d x d y
$$

$$
\int _ { - R } ^ { R } \int _ { - R } ^ { R } e ^ { - ( x ^ { 2 } + y ^ { 2 } ) } d x d y > \int \int _ { x ^ { 2 } + y ^ { 2 } \leq R ^ { 2 } } e ^ { - ( x ^ { 2 } + y ^ { 2 } ) } d x d y = \pi ( 1 - e ^ { - R ^ { 2 } } )  \pi , R  + \infty \ ,
$$

$$
\int _ { - R } ^ { R } \int _ { - R } ^ { R } e ^ { - ( x ^ { 2 } + y ^ { 2 } ) } d x d y < \int _ { x ^ { 2 } + y ^ { 2 } \leq 2 R ^ { 2 } } e ^ { - ( x ^ { 2 } + y ^ { 2 } ) } d x d y = \pi ( 1 - e ^ { - 2 R ^ { 2 } } ) \to \pi , R \to + \infty \ ,
$$

故 $\operatorname * { l i m } _ { R  + \infty } \int _ { - R } ^ { R } \int _ { - R } ^ { R } e ^ { - ( x ^ { 2 } + y ^ { 2 } ) } d x d y = \pi$ ，故 $( \int _ { - \infty } ^ { + \infty } e ^ { - x ^ { 2 } } d x ) ^ { 2 } = \pi$ ，即 $\int _ { - \infty } ^ { + \infty } e ^ { - x ^ { 2 } } d x = { \sqrt { \pi } }$

5.函数 $f ( x ) = \left\{ \begin{array} { l l } { \displaystyle \cos \frac { \pi x } { 2 } , \big | x \big | \leq 1 } \\ { \big | x - 1 \big | , \big | x \big | > 1 } \end{array} \right.$ 的间断点为 数学考研考 盗版必究宝哥

【解答】

$f ( x ) = { \left\{ \begin{array} { l l } { \displaystyle \cos { \frac { \pi x } { 2 } } , \left| x \right| \leq 1 } \\ { \displaystyle \left| x - 1 \right| , \left| x \right| > 1 } \end{array} \right. }$ A $\left| x \right| \neq 1$ 时，f(x)连续.

$$
f ( 1 ^ { + } ) = \operatorname* { l i m } _ { x  1 ^ { + } } f ( x ) = \operatorname* { l i m } _ { x  1 ^ { + } } | x - 1 | = 0 \ ,
$$

$$
f ( 1 ) = f ( 1 ^ { - } ) = \operatorname* { l i m } _ { x \to 1 ^ { - } } f ( x ) = \operatorname* { l i m } _ { x \to 1 ^ { - } } \cos { \frac { \pi x } { 2 } } = 0 ,
$$

$$
f \Bigl ( ( - 1 ) ^ { + } \Bigr ) = \operatorname * { l i m } _ { x  ( - 1 ) ^ { + } } f ( x ) = \operatorname * { l i m } _ { x  ( - 1 ) ^ { + } } \cos { \frac { \pi x } { 2 } } = 0 \ ,
$$

$$
f { \big ( } ( - 1 ) ^ { - } { \big ) } = \operatorname* { l i m } _ { x \to ( - 1 ) ^ { - } } f ( x ) = \operatorname* { l i m } _ { x \to ( - 1 ) ^ { - } } \left| x - 1 \right| = 4 ,
$$

$f ( 1 ) = f ( 1 ^ { + } ) = f ( 1 ^ { - } ) = 0$ ，故x=1为连续点. $f { \bigl ( } ( - 1 ) ^ { + } { \bigr ) } , f { \bigl ( } ( - 1 ) ^ { - } { \bigr ) }$ 存在而不相等，故$x = - 1$ 为跳跃间断点.

6.级数 $\sum _ { n = 2 } ^ { \infty } ( 1 + { \frac { 1 } { n } } ) ^ { n ( n + 1 ) } x ^ { n }$ 的收敛半径为_

【解答】

$\operatorname* { l i m } _ { n \to \infty } \sqrt [ n ] { ( 1 + \frac { 1 } { n } ) ^ { n ( n + 1 ) } } = \operatorname* { l i m } _ { n \to \infty } ( 1 + \frac { 1 } { n } ) ^ { n + 1 } = e$ 故级数 $\sum _ { n = 2 } ^ { \infty } ( 1 + { \frac { 1 } { n } } ) ^ { n ( n + 1 ) } x ^ { n }$ 的收敛半径为 $\frac { 1 } { e }$ 7.设曲线L是圆 $x ^ { 2 } + y ^ { 2 } = r ^ { 2 }$ 在第一象限内的部分，则 $\int _ { L } x y d l =$

【解答】

曲线L是圆 $x ^ { 2 } + y ^ { 2 } = r ^ { 2 }$ 在第一象限内的部分，其参数方程为$\{ { \begin{array} { l } { x = r \cos t } \\ { y = r \sin t } \end{array} } , t \in [ 0 , { \frac { \pi } { 2 } } ]$ 宝哥数学，故 所有

$$
\begin{array} { l } { \displaystyle { \int _ { L } x y d l = \int _ { 0 } ^ { \frac { \pi } { 2 } } r \cos t r \sin t \sqrt { ( \frac { d x } { d t } ) ^ { 2 } + ( \frac { d y } { d t } ) ^ { 2 } } d t = \int _ { 0 } ^ { \frac { \pi } { 2 } } r \cos t r \sin t \sqrt { ( - r \sin t ) ^ { 2 } + ( r \cos t ) ^ { 2 } } d t } } \\ { \displaystyle { \quad \quad = r ^ { 3 } \int _ { 0 } ^ { \frac { \pi } { 2 } } \cos t \sin t d t = \frac { 1 } { 2 } r ^ { 3 } \sin ^ { 2 } t \left| \frac { \pi } { 2 } = \frac { 1 } { 2 } r ^ { 3 } \right. } } \end{array}
$$

8. $\int { \frac { 1 } { x ( 1 + x ^ { n } ) } } d x =$

## 【解答】

$$
\int { \frac { 1 } { x ( 1 + x ^ { n } ) } } d x = \int { \frac { x ^ { n - 1 } } { x ^ { n } ( 1 + x ^ { n } ) } } d x = { \frac { 1 } { n } } \int ( { \frac { 1 } { x ^ { n } } } - { \frac { 1 } { 1 + x ^ { n } } } ) d x ^ { n } = { \frac { 1 } { n } } \ln \left| { \frac { x ^ { n } } { 1 + x ^ { n } } } \right| + C .
$$

## 二.计算题(本大题共5 小题，每小题10分，共 50 分)

1.计算 $\int _ { L } { ( - 2 x e ^ { - x ^ { 2 } } \sin y ) d x } + { ( e ^ { - x ^ { 2 } } \cos y + x ^ { 6 } ) d y }$ ,这里L为从点(1,0)到(-1,0)的半圆 $y = \sqrt { 1 - x ^ { 2 } } ( - 1 \leq x \leq 1 )$ 学考研 盗版必

【解答】

L为从点(1,0)到(-1,0)的半圆 $y = \sqrt { 1 - x ^ { 2 } } ( - 1 \leq x \leq 1 )$ ，故

$$
\begin{array} { c } { { { \displaystyle { \int _ { L } } ( - 2 x e ^ { - x ^ { 2 } } \sin y ) d x + e ^ { - x ^ { 2 } } \cos y d y = \displaystyle { \int _ { L } } \sin y d e ^ { - x ^ { 2 } } + e ^ { - x ^ { 2 } } d \sin y } } } \\ { { { \displaystyle { = \int _ { L } } d ( e ^ { - x ^ { 2 } } \sin y ) = ( e ^ { - x ^ { 2 } } \sin y ) \displaystyle { \left| ( 1 , 0 ) \right. } = 0 } } } \end{array} .
$$

记 $L _ { \imath }$ 为(-1,0)到(1,0)的有向直线段，D为 $L , L _ { \mathrm { 1 } }$ 围成的平面区域，则 $\int _ { L _ { 1 } } { x ^ { 6 } d y } = 0$ 由格林公式，有 数学 有盗 学考研 盗版

$$
\int _ { L } x ^ { 6 } d y = ( \int _ { L \cup L _ { 1 } } - \int _ { L _ { 1 } } ) x ^ { 6 } d y = \iint \frac { \widehat { \partial } x ^ { 6 } } { \widehat { \partial } x } d x d y = \iint 6 x ^ { 5 } d x d y \quad \stackrel { \cong } { = } \quad 0
$$

2.求 $\operatorname* { l i m } _ { x \to \infty } \left[ x - x ^ { 2 } \ln \left( 1 + { \frac { 1 } { x } } \right) \right]$

【解答】

$$
\operatorname* { l i m } _ { x \to \infty } \left[ x - x ^ { 2 } \ln \left( 1 + { \frac { 1 } { x } } \right) \right] = \operatorname* { l i m } _ { x \to \infty } x ^ { 2 } \left[ { \frac { 1 } { x } } - \ln \left( 1 + { \frac { 1 } { x } } \right) \right] = \operatorname* { l i m } _ { x \to \infty } { \frac { x ^ { 2 } } { 2 x ^ { 2 } } } = { \frac { 1 } { 2 } } .
$$

3.求 $\sum _ { n = 1 } ^ { \infty } { \frac { 2 n } { 3 ^ { n } } }$ 的和.

## 【解答】

幂级数的收敛半径为 $\operatorname* { l i m } _ { n \to \infty } { \frac { n } { n + 1 } } = 1$ ，且其在x=±1处通项都是无穷大量， 故其在x=±1处发散，故幂级数的收敛域为(-1,1).

在(-1,1)内，

$$
\sum _ { n = 1 } ^ { \infty } n x ^ { n - 1 } = \sum _ { n = 1 } ^ { \infty } ( x ^ { n } ) ^ { \prime } = ( \sum _ { n = 1 } ^ { \infty } x ^ { n } ) ^ { \prime } = ( \sum _ { n = 0 } ^ { \infty } x ^ { n } ) ^ { \prime } = ( { \frac { 1 } { 1 - x } } ) ^ { \prime } = { \frac { 1 } { ( 1 - x ) ^ { 2 } } }
$$

$\frac { 1 } { 3 } \in ( - 1 , 1 )$ ，故

$$
\sum _ { n = 1 } ^ { \infty } \frac { 2 n } { 3 ^ { n } } = \frac { 2 } { 3 } \sum _ { n = 1 } ^ { \infty } n ( \frac { 1 } { 3 } ) ^ { n - 1 } = \frac { 2 } { 3 } \frac { 1 } { ( 1 - \frac { 1 } { 3 } ) ^ { 2 } } = \frac { 3 } { 2 } .
$$

4.计算 $\oint _ { \Gamma } x ^ { 2 } y d x + y ^ { 2 } d y + z d z$ ,其中是圆柱 $x ^ { 2 } + y ^ { 2 } = 1$ 与平面x+z=1的交线，从z轴的正向看去，为逆时针方向. 开数学 数学考

## 【解答】

$$
\oint _ { \Gamma } y ^ { 2 } d y + z d z = \oint _ { \Gamma } d ( { \frac { y ^ { 3 } } { 3 } } + { \frac { z ^ { 2 } } { 2 } } ) = 0 .
$$

$$
x ^ { 2 } + y ^ { 2 } = 1
$$

浴版 $\{ \begin{array} { l l } { x = \cos t } \\ { y = \sin t \quad \quad , t : 0  2 \pi } \\ { z = 1 - \cos t } \end{array} $ 故可设其参数方程为宝 所有

$$
\begin{array} { r l } & { \quad \oint _ { \Gamma } x ^ { 2 } y d x = \displaystyle \int _ { 0 } ^ { 2 \pi } \cos ^ { 2 } t \sin t ( \cos t ) ^ { \prime } d t = - \displaystyle \int _ { 0 } ^ { 2 \pi } \cos ^ { 2 } t \sin ^ { 2 } t d t = - 4 \displaystyle \int _ { 0 } ^ { \frac { 1 } { 2 \pi } } \cos ^ { 2 } t \sin ^ { 2 } t d t } \\ & { = - \displaystyle \int _ { 0 } ^ { \frac { 1 } { 2 \pi } } ( 2 \sin t \cos t ) ^ { 2 } d t = - \displaystyle \int _ { 0 } ^ { \frac { 1 } { 2 \pi } } \sin ^ { 2 } 2 t d t = - \displaystyle \frac { 1 } { 2 } \displaystyle \int _ { 0 } ^ { \frac { 1 } { 2 \pi } } \sin ^ { 2 } 2 t d ( 2 t ) = - \displaystyle \frac { 1 } { 2 } \displaystyle \int _ { 0 } ^ { \pi } \sin ^ { 2 } t d t \quad . } \\ & { = - \displaystyle \int _ { 0 } ^ { \frac { 1 } { 2 \pi } } \sin ^ { 2 } t d t = - \displaystyle \frac { \pi } { 4 } } \end{array}
$$

因此， $\oint _ { \Gamma } { x ^ { 2 } y d x } + { y ^ { 2 } d y } + z d z = - { \frac { \pi } { 4 } }$

5.计算 $\iint _ { \Omega } { x ^ { 2 } \sqrt { x ^ { 2 } + y ^ { 2 } } d x d y d z }$ ,其中Ω是曲面 $z = \sqrt { x ^ { 2 } + y ^ { 2 } }$ 与平面 $z = x ^ { 2 } + y ^ { 2 }$ 所围成的区域.

## 【解答】

Ω是曲面 $z = \sqrt { x ^ { 2 } + y ^ { 2 } }$ 与平面 $z = x ^ { 2 } + y ^ { 2 }$ 所围成的区域．联立方程$\left\{ z = \sqrt { x ^ { 2 } + y ^ { 2 } } \right.$ $( x , y , z ) = ( 0 , 0 , 0 )$ 必究 ，或 $\left\{ { \begin{array} { l } { x ^ { 2 } + y ^ { 2 } = 1 } \\ { z = 1 } \end{array} } \right.$ Ω关于平面x＝y是对称的，由轮换对称性，有 学考研 版必究 老博

$$
{ \begin{array} { r l } & { { \underset { \Omega } { \iint } } x ^ { 2 } { \sqrt { x ^ { 2 } + y ^ { 2 } } } d x d y d z = { \underset { \Omega } { \iint } } y ^ { 2 } { \sqrt { x ^ { 2 } + y ^ { 2 } } } d x d y d z = { \frac { 1 } { 2 } } { \underset { \Omega } { \iint } } ( x ^ { 2 } + y ^ { 2 } ) { \sqrt { x ^ { 2 } + y ^ { 2 } } } d x d y d z } \\ & { = { \frac { 1 } { 2 } } { \underset { \varepsilon ^ { 2 } \leq x ^ { 2 } + y ^ { 2 } \leq z } { \iint } } ( x ^ { 2 } + y ^ { 2 } ) { \sqrt { x ^ { 2 } + y ^ { 2 } } } d x d y = { \frac { 1 } { 2 } } { \int } _ { 0 } ^ { 1 } d z { \int } _ { z } ^ { { \sqrt { z } } } r ^ { 3 } \cdot r d r { \int } _ { 0 } ^ { 2 \pi } d \theta } \\ & { = \pi { \int } _ { 0 } ^ { 1 } { \frac { r ^ { 5 } } { 5 } } { \Bigg | } _ { z } ^ { \sqrt { z } } d z = { \frac { \pi } { 5 } } { \int } _ { 0 } ^ { 1 } ( r ^ { \frac { 5 } { 2 } } - r ^ { 5 } ) d z = { \frac { \pi } { 5 } } ( { \frac { 2 } { 7 } } - { \frac { 1 } { 6 } } ) = { \frac { \pi } { 4 2 } } } \end{array} }
$$

## 三.证明题(本大题共4小题，每小题10分，共40 分)

1.证明： $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { x ^ { 2 } + n } { n ^ { 2 } } }$ 在任何有限区域[a,b]上一致收敛，而在实轴上任何一点都不绝对收敛. 宝哥 权所有 宝哥数 权所有

【解答】

对任意 $x \in \left[ a , b \right]$ $\left\{ { \frac { x ^ { 2 } + n } { n ^ { 2 } } } \right\}$ 单调递减.

$$
0 < \frac { x ^ { 2 } + n } { n ^ { 2 } } \leq \frac { \left[ \operatorname* { m a x } ( \left| a \right| , \left| b \right| ) \right] ^ { 2 } + n } { n ^ { 2 } } \to 0 , n \to \infty ,
$$

故 $\left\{ { \frac { x ^ { 2 } + n } { n ^ { 2 } } } \right\}$ 在[a,b]上一致收敛于0．对任意正整数n， $\left| \sum _ { k = 1 } ^ { n } ( - 1 ) ^ { k } \right| \leq 1$ 由狄利克雷版机 宝哥 版权所有判别法，级数 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { x ^ { 2 } + n } { n ^ { 2 } } }$ 在区间[a,b]上一致收敛.

$| ( - 1 ) ^ { n } { \frac { x ^ { 2 } + n } { n ^ { 2 } } } | \sim { \frac { 1 } { n } } , n  \infty$ $\sum _ { n = 1 } ^ { \infty } { \frac { 1 } { n } }$ 发散，故 $\sum _ { n = 1 } ^ { \infty } \left. ( - 1 ) ^ { n } { \frac { x ^ { 2 } + n } { n ^ { 2 } } } \right.$ 发散，故

$$
\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { x ^ { 2 } + n } { n ^ { 2 } } }
$$

2.设奇函数f(x)在[-1,1]上具有二阶导数，且f(1)=1,证明：

(1)存在 $\xi \in ( 0 , 1 )$ ，使得 $f ^ { \prime } ( \xi ) = 1$

(2）存在 $\eta \in ( - 1 , 1 )$ ，使得 $f ^ { \prime \prime } ( \eta ) + f ^ { \prime } ( \eta ) = 1$

## 【解答】

(1）f(x)为[-1,1]上的奇函数，故f(0)=0．奇函数f(x)在[-1,1]上具有二阶导数  
且f(1)=1，由拉格朗日中值定理，存在 $\xi \in ( 0 , 1 )$ ，使得 $f ^ { \prime } ( \xi ) = \frac { f ( 1 ) - f ( 0 ) } { 1 - 0 } = 1$ $f ^ { \prime } ( - \xi ) = 1$ ．问题即证明 $f ^ { \prime \prime } ( x ) + f ^ { \prime } ( x ) - 1$ 考  
在(-1,1)内有零点，即 $e ^ { x } \left[ f ^ { \prime \prime } ( x ) + f ^ { \prime } ( x ) - 1 \right] = \left[ e ^ { x } f ^ { \prime } ( x ) - e ^ { x } \right] ^ { \prime }$   
$F ( x ) = e ^ { x } f ( x ) - e ^ { x } , x \in \left[ - 1 , 1 \right]$ ，则F(𝑥)在[-1,1]上连续，在(-1,1)内可导，且  
$F ( \xi ) = F ( - \xi ) = 0$ $\eta \in ( - \xi , \xi ) \subset ( - 1 , 1 )$ ，使得 $F ^ { \prime } ( \eta ) = 0$   
也就是 $f ^ { \prime \prime } ( \eta ) + f ^ { \prime } ( \eta ) = 1$ 考博 从究 来

3.设f(x)在[0,1]上连续，证明： $\iint f ( 1 - y ) f ( x ) d x d y = { \frac { 1 } { 2 } } { \biggl [ } \int _ { 0 } ^ { 1 } f ( x ) d x { \biggr ] } ^ { 2 }$ ，其中D版权所 宝哥数为以 $O ( 0 , 0 ) , A ( 0 , 1 ) , B ( 1 , 0 )$ 为顶点的三角形所围成的区域. 版权所

## 【解答】

区域D如下图所示：

<!-- image-->

$$
\begin{array} { l } { { \displaystyle \iint f ( 1 - y ) f ( x ) d x d y = \int _ { 0 } ^ { 1 } f ( x ) d x \int _ { 0 } ^ { 1 - x } f ( 1 - y ) d y ~ ^ { y = 1 - y } } } \\ { { \displaystyle = \int _ { 0 } ^ { 1 } f ( x ) d x \int _ { x } ^ { 1 } f ( t ) d t = \int _ { 0 } ^ { 1 } f ( x ) \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] d x = - \int _ { 0 } ^ { 1 } \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] d \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] . } } \\ { { \displaystyle = - \frac { 1 } { 2 } \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] ^ { 2 } \left| 0 - \frac { 1 } { 2 } \biggl [ \int _ { 0 } ^ { 1 } f ( t ) d t \biggr ] ^ { 2 } \right. } } \end{array}
$$

4.已知△表示L2pl2ce算符，即： $\Delta u = \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } ^ { 2 } } + \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } ^ { 2 } } + \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } z ^ { 2 } }$ ．证明：

$$
\begin{array} { r } { \Delta ( u \nu ) = ( \Delta u ) \nu + 2 \nabla u \cdot \nabla \nu + u ( \Delta \nu ) . } \end{array}
$$

这里Vu表示函数u在点 $( x , y , z )$ 处的梯度，“·"表示点乘.

## 【解答】

$$
 \begin{array} { l } { \Delta ( u \nu ) = { \frac { { \hat { \sigma } } ^ { 2 } ( u \nu ) } { { \hat { \sigma } } x ^ { 2 } } } + { \frac { { \hat { \sigma } } ^ { 2 } ( u \nu ) } { { \hat { \sigma } } y ^ { 2 } } } + { \frac { { \hat { \sigma } } ^ { 2 } ( u \nu ) } { { \hat { \sigma } } z ^ { 2 } } } } \\ { = ( { \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } x ^ { 2 } } } \nu + 2 { \frac { { \hat { \sigma } } u } { { \hat { \sigma } } x } } { \frac { { \hat { \sigma } } \nu } { { \hat { \alpha } } x } } + u { \frac { { \hat { \sigma } } ^ { 2 } \nu } { { \hat { \sigma } } x ^ { 2 } } } ) + ( { \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } y ^ { 2 } } } \nu + 2 { \frac { { \hat { \sigma } } u } { \hat { \sigma } } } { \frac { { \hat { \sigma } } \nu } { { \hat { \sigma } } y } } + u { \frac { { \hat { \sigma } } ^ { 2 } \nu } { { \hat { \sigma } } y ^ { 2 } } } ) + ( { \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } z ^ { 2 } } } \nu + 2 { \frac { { \hat { \sigma } } u } { { \hat { \sigma } } z } } { \frac { { \hat { \sigma } } \nu } { { \hat { \sigma } } z } } + u { \frac { { \hat { \sigma } } ^ { 2 } \nu } { { \hat { \sigma } } z ^ { 2 } } } ) } \\  = ( { \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } x ^ { 2 } } } + { \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } y ^ { 2 } } } + { \frac { { \hat { \sigma } } ^ { 2 } u } { { \hat { \sigma } } z ^ { 2 } } } ) \nu + 2 (  \frac   \ \end{array}
$$

## 四.综合题(本大题共2小题，共30 分)

1.(10分）求两个曲面 $x + 2 y = 1$ 和 $x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 的交线上距离原点最近的点.【解答】 所有 哥数学 新有盗 学考 现

任取交线上的一点(x,y,z)，则 $\left\{ { x + 2 y = 1 \atop x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1 } \right.$ ，其到原点的距离平方为  
$d = x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } - y ^ { 2 } = 1 - y ^ { 2 }$ ．这样，问题即转化为求y的最大值了.$x + 2 y = 1$ 双 $x = 1 - 2 y$ ，故 $( 1 - 2 y ) ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 即 $z ^ { 2 } = 4 y - 6 y ^ { 2 } \geq 0$ 考研象  
$0 \leq y \leq \frac { 2 } { 3 }$ $y = \frac { 2 } { 3 }$ $z = 0 , x = 1 - 2 y = - \frac { 1 } { 3 }$ ，故交线上距离原点最近的点为所有司  
$( - \frac { 1 } { 3 } , \frac { 2 } { 3 } , 0 ) .$ 宝哥数学 宝哥数 权所有所有

2.设 $f ( x ) = \int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t , x \in ( - \infty , + \infty )$

(1）试证明积分 $\int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \infty , + \infty )$ 上一致收敛.

(2）试证明函数f(x)在 $( - \infty , + \infty )$ 上一致连续.

【解答】

(1)对任意 $( t , x ) \in \left[ 1 , + \infty \right) \times ( - \infty , + \infty )$ 有 $\left| { \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \right| \leq { \frac { 1 } { 1 + t ^ { 2 } } } . \ \int _ { 1 } ^ { + \infty } { \frac { d t } { 1 + t ^ { 2 } } }$ 收敛，故版权 宝哥数$\int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \infty , + \infty )$ 上一致收敛. 哥数学考研所有

(2）对任意 $\left( t , x \right) \in \left[ 1 , + \infty \right) \times \left( - \infty , + \infty \right)$ ，有 $\left| { \frac { \partial } { \partial x } } \left[ { \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \right] \right| = \left| { \frac { - \sin ( x t ) } { 1 + t ^ { 2 } } } \right| \leq { \frac { 1 } { 1 + t ^ { 2 } } }$ 必究  
$\int _ { 1 } ^ { + \infty } \frac { d t } { 1 + t ^ { 2 } }$ $\int _ { 1 } ^ { + \infty } \frac { \partial } { \partial x } \Bigg [ \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } \Bigg ] d t$ 一致收敛.故f(x)在 $( - \infty , + \infty )$ 可导，且  
宝哥数 学考 盗版  
版权所有 $f ^ { \prime } ( x ) = \int _ { 1 } ^ { + \infty } \frac { \hat { \partial } } { \partial x } \left[ \frac { \cos ( x t ) } { t { ( 1 + t ^ { 2 } ) } } \right] d t = - \int _ { 1 } ^ { + \infty } \frac { \sin ( x t ) } { 1 + t ^ { 2 } } d t ,$ 中哥数

$$
\big | f ^ { \prime } ( x ) \big | = | - \int _ { 1 } ^ { + \infty } { \frac { \sin ( x t ) } { 1 + t ^ { 2 } } } d t | \leq \int _ { 1 } ^ { + \infty } { \frac { | \sin ( x t ) | } { 1 + t ^ { 2 } } } d t < \int _ { 1 } ^ { + \infty } { \frac { 1 } { 1 + t ^ { 2 } } } d t = \arctan t | 1 ^ { + \infty } = { \frac { \pi } { 4 } } + { \frac { 1 } { \pi } } + { \frac { 1 } { \pi } } | \sin ( x t ) | \operatorname { d } t .
$$

故函数f(x)在 $( - \infty , + \infty )$ 上一致连续.

## tool · 2026-10-19T07:21:57Z




## tool · 2026-10-19T07:22:03Z


Script completed
Wall time 0.2 seconds
Output:

35:    result = subprocess.run([PANDOC, '-f', 'markdown+tex_math_dollars+tex_math_single_backslash', '-t', 'latex', '--standalone', '-V', 'documentclass=ctexart', '-V', 'classoption=fontset=fandol', '-V', 'mathspec=true', '-V', 'geometry:margin=23mm', '-V', 'fontsize=11pt', '-H', str(WORK / 'header.tex'), str(md), '-o', str(tex)], capture_output=True, text=True)
/Volumes/SamsungSSD990PRO/Application/texlive/2025/bin/universal-darwin/xelatex
## 杭州电子科技大学2018年数学分析真题解析

## 一.填空题(本大题共8小题，每小题5分，本大题共40分)

1. $\operatorname* { l i m } _ { n  \infty } ( 2 ^ { n } + 3 ^ { n } + 4 ^ { n } ) ^ { \frac { 1 } { n } } = ($

【宝哥解答】

是k个非负常数，则一般地，设 $a _ { 1 } , a _ { 2 } , \cdots , a _ { k }$

$$
\operatorname* { l i m } _ { n \to \infty } \sqrt [ n ] { a _ { 1 } ^ { n } + a _ { 2 } ^ { n } + \cdots + a _ { k } ^ { n } } = \operatorname* { m a x } ( a _ { 1 } , a _ { 2 } , \cdots , a _ { k } )
$$

证明：
# 杭州电子科技大学2019年数学分析真题解析

## 一.填空题（本大蔬英6小题，每小题5分，本大题共40分）

1.极限 $\operatorname* { l i m } _ { n \to \infty } ( { \frac { 1 } { n + { \sqrt { 1 } } } } + { \frac { 1 } { n + { \sqrt { 2 } } } } + \cdots + { \frac { 1 } { n + { \sqrt { n } } } } ) = ($

【宝哥解答】

$$
\frac { 1 } { n + \sqrt { 1 } } + \frac { 1 } { n + \sqrt { 2 } } + \cdots + \frac { 1 } { n + \sqrt { n } } \leq \frac { n } { n + \sqrt { 1 } }  1 , n  \infty ,
$$

$$
{ \frac { 1 } { n + { \sqrt { 1 } } } } + { \frac { 1 } { n + { \sqrt { 2 } } } } + \cdots + { \frac { 1 } { n + { \sqrt { n } } } } \geq { \frac { n } { n + { \sqrt { n } } } } \to 1 , n \to \infty ,
$$
## 杭州电子科技大学2021年数学分析真题解析

## 一.填空题(本大题共8小题，每小题5分，共40分)

$$
\operatorname* { l i m } _ { n  \infty } { \frac { n ^ { 2 } } { 2 ^ { n } } } = (
$$

【宝哥解答】

$$
\operatorname* { l i m } _ { n  \infty } { \frac { n ^ { 2 } } { 2 ^ { n } } } = 0 .
$$

2.设点(0,1)是曲线 $y = x ^ { 3 } + b x ^ { 2 } + 1$ 的拐点，则b=（【宝哥解答】


## tool · 2026-10-19T07:22:08Z




## tool · 2026-10-19T07:22:27Z


Script completed
Wall time 1.4 seconds
Output:

{}
{"chunk_id":"525341","wall_time_seconds":1.002684208,"session_id":52949,"original_token_count":0,"output":""}

## tool · 2026-10-19T07:22:42Z


Script completed
Wall time 5.0 seconds
Output:

{"chunk_id":"95c5e1","wall_time_seconds":5.001878209,"session_id":52949,"original_token_count":239,"output":"{\"key\": \"1abbef1daec3bc92\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"f6badbfa1728d169\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"27ea8f6e4eb7355d\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"128a26e7394a073e\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"2c29e49c601a658a\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"3f7b5ea1df00c613\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n"}

## tool · 2026-10-19T07:22:49Z


Script completed
Wall time 0.4 seconds
Output:

{}
{"chunk_id":"c20d73","wall_time_seconds":0.000020041,"exit_code":0,"original_token_count":2174,"output":"   193\t$$\n   194\t\n   195\t故 $\\left\\{ { \\frac { x ^ { 2 } + n } { n ^ { 2 } } } \\right\\}$ 在[a,b]上一致收敛于0．对任意正整数n， $\\left| \\sum _ { k = 1 } ^ { n } ( - 1 ) ^ { k } \\right| \\leq 1$ 由狄利克雷版机 宝哥 版权所有判别法，级数 $\\sum _ { n = 1 } ^ { \\infty } ( - 1 ) ^ { n } { \\frac { x ^ { 2 } + n } { n ^ { 2 } } }$ 在区间[a,b]上一致收敛.\n   196\t\n   197\t$| ( - 1 ) ^ { n } { \\frac { x ^ { 2 } + n } { n ^ { 2 } } } | \\sim { \\frac { 1 } { n } } , n  \\infty$ $\\sum _ { n = 1 } ^ { \\infty } { \\frac { 1 } { n } }$ 发散，故 $\\sum _ { n = 1 } ^ { \\infty } \\left. ( - 1 ) ^ { n } { \\frac { x ^ { 2 } + n } { n ^ { 2 } } } \\right.$ 发散，故\n   198\t\n   199\t$$\n   200\t\\sum _ { n = 1 } ^ { \\infty } ( - 1 ) ^ { n } { \\frac { x ^ { 2 } + n } { n ^ { 2 } } }\n   201\t$$\n   202\t\n   203\t2.设奇函数f(x)在[-1,1]上具有二阶导数，且f(1)=1,证明：\n   204\t\n   205\t(1)存在 $\\xi \\in ( 0 , 1 )$ ，使得 $f ^ { \\prime } ( \\xi ) = 1$\n   206\t\n   207\t(2）存在 $\\eta \\in ( - 1 , 1 )$ ，使得 $f ^ { \\prime \\prime } ( \\eta ) + f ^ { \\prime } ( \\eta ) = 1$\n   208\t\n   209\t## 【解答】\n   210\t\n   211\t(1）f(x)为[-1,1]上的奇函数，故f(0)=0．奇函数f(x)在[-1,1]上具有二阶导数  \n   212\t且f(1)=1，由拉格朗日中值定理，存在 $\\xi \\in ( 0 , 1 )$ ，使得 $f ^ { \\prime } ( \\xi ) = \\frac { f ( 1 ) - f ( 0 ) } { 1 - 0 } = 1$ $f ^ { \\prime } ( - \\xi ) = 1$ ．问题即证明 $f ^ { \\prime \\prime } ( x ) + f ^ { \\prime } ( x ) - 1$ 考  \n   213\t在(-1,1)内有零点，即 $e ^ { x } \\left[ f ^ { \\prime \\prime } ( x ) + f ^ { \\prime } ( x ) - 1 \\right] = \\left[ e ^ { x } f ^ { \\prime } ( x ) - e ^ { x } \\right] ^ { \\prime }$   \n   214\t$F ( x ) = e ^ { x } f ( x ) - e ^ { x } , x \\in \\left[ - 1 , 1 \\right]$ ，则F(𝑥)在[-1,1]上连续，在(-1,1)内可导，且  \n   215\t$F ( \\xi ) = F ( - \\xi ) = 0$ $\\eta \\in ( - \\xi , \\xi ) \\subset ( - 1 , 1 )$ ，使得 $F ^ { \\prime } ( \\eta ) = 0$   \n   216\t也就是 $f ^ { \\prime \\prime } ( \\eta ) + f ^ { \\prime } ( \\eta ) = 1$ 考博 从究 来\n   217\t\n   218\t3.设f(x)在[0,1]上连续，证明： $\\iint f ( 1 - y ) f ( x ) d x d y = { \\frac { 1 } { 2 } } { \\biggl [ } \\int _ { 0 } ^ { 1 } f ( x ) d x { \\biggr ] } ^ { 2 }$ ，其中D版权所 宝哥数为以 $O ( 0 , 0 ) , A ( 0 , 1 ) , B ( 1 , 0 )$ 为顶点的三角形所围成的区域. 版权所\n   219\t\n   220\t## 【解答】\n   221\t\n   222\t区域D如下图所示：\n   223\t\n   224\t<!-- image-->\n   225\t\n   226\t$$\n   227\t\\begin{array} { l } { { \\displaystyle \\iint f ( 1 - y ) f ( x ) d x d y = \\int _ { 0 } ^ { 1 } f ( x ) d x \\int _ { 0 } ^ { 1 - x } f ( 1 - y ) d y ~ ^ { y = 1 - y } } } \\\\ { { \\displaystyle = \\int _ { 0 } ^ { 1 } f ( x ) d x \\int _ { x } ^ { 1 } f ( t ) d t = \\int _ { 0 } ^ { 1 } f ( x ) \\biggl [ \\int _ { x } ^ { 1 } f ( t ) d t \\biggr ] d x = - \\int _ { 0 } ^ { 1 } \\biggl [ \\int _ { x } ^ { 1 } f ( t ) d t \\biggr ] d \\biggl [ \\int _ { x } ^ { 1 } f ( t ) d t \\biggr ] . } } \\\\ { { \\displaystyle = - \\frac { 1 } { 2 } \\biggl [ \\int _ { x } ^ { 1 } f ( t ) d t \\biggr ] ^ { 2 } \\left| 0 - \\frac { 1 } { 2 } \\biggl [ \\int _ { 0 } ^ { 1 } f ( t ) d t \\biggr ] ^ { 2 } \\right. } } \\end{array}\n   228\t$$\n   229\t\n   230\t4.已知△表示L2pl2ce算符，即： $\\Delta u = \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } ^ { 2 } } + \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } ^ { 2 } } + \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } z ^ { 2 } }$ ．证明：\n   231\t\n   232\t$$\n   233\t\\begin{array} { r } { \\Delta ( u \\nu ) = ( \\Delta u ) \\nu + 2 \\nabla u \\cdot \\nabla \\nu + u ( \\Delta \\nu ) . } \\end{array}\n   234\t$$\n   235\t\n   236\t这里Vu表示函数u在点 $( x , y , z )$ 处的梯度，“·\"表示点乘.\n   237\t\n   238\t## 【解答】\n   239\t\n   240\t$$\n   241\t \\begin{array} { l } { \\Delta ( u \\nu ) = { \\frac { { \\hat { \\sigma } } ^ { 2 } ( u \\nu ) } { { \\hat { \\sigma } } x ^ { 2 } } } + { \\frac { { \\hat { \\sigma } } ^ { 2 } ( u \\nu ) } { { \\hat { \\sigma } } y ^ { 2 } } } + { \\frac { { \\hat { \\sigma } } ^ { 2 } ( u \\nu ) } { { \\hat { \\sigma } } z ^ { 2 } } } } \\\\ { = ( { \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } x ^ { 2 } } } \\nu + 2 { \\frac { { \\hat { \\sigma } } u } { { \\hat { \\sigma } } x } } { \\frac { { \\hat { \\sigma } } \\nu } { { \\hat { \\alpha } } x } } + u { \\frac { { \\hat { \\sigma } } ^ { 2 } \\nu } { { \\hat { \\sigma } } x ^ { 2 } } } ) + ( { \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } y ^ { 2 } } } \\nu + 2 { \\frac { { \\hat { \\sigma } } u } { \\hat { \\sigma } } } { \\frac { { \\hat { \\sigma } } \\nu } { { \\hat { \\sigma } } y } } + u { \\frac { { \\hat { \\sigma } } ^ { 2 } \\nu } { { \\hat { \\sigma } } y ^ { 2 } } } ) + ( { \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } z ^ { 2 } } } \\nu + 2 { \\frac { { \\hat { \\sigma } } u } { { \\hat { \\sigma } } z } } { \\frac { { \\hat { \\sigma } } \\nu } { { \\hat { \\sigma } } z } } + u { \\frac { { \\hat { \\sigma } } ^ { 2 } \\nu } { { \\hat { \\sigma } } z ^ { 2 } } } ) } \\\\  = ( { \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } x ^ { 2 } } } + { \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } y ^ { 2 } } } + { \\frac { { \\hat { \\sigma } } ^ { 2 } u } { { \\hat { \\sigma } } z ^ { 2 } } } ) \\nu + 2 (  \\frac   \\ \\end{array}\n   242\t$$\n   243\t\n   244\t## 四.综合题(本大题共2小题，共30 分)\n   245\t\n   246\t1.(10分）求两个曲面 $x + 2 y = 1$ 和 $x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 的交线上距离原点最近的点.【解答】 所有 哥数学 新有盗 学考 现\n   247\t\n   248\t任取交线上的一点(x,y,z)，则 $\\left\\{ { x + 2 y = 1 \\atop x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1 } \\right.$ ，其到原点的距离平方为  \n   249\t$d = x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } - y ^ { 2 } = 1 - y ^ { 2 }$ ．这样，问题即转化为求y的最大值了.$x + 2 y = 1$ 双 $x = 1 - 2 y$ ，故 $( 1 - 2 y ) ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 即 $z ^ { 2 } = 4 y - 6 y ^ { 2 } \\geq 0$ 考研象  \n   250\t$0 \\leq y \\leq \\frac { 2 } { 3 }$ $y = \\frac { 2 } { 3 }$ $z = 0 , x = 1 - 2 y = - \\frac { 1 } { 3 }$ ，故交线上距离原点最近的点为所有司  \n   251\t$( - \\frac { 1 } { 3 } , \\frac { 2 } { 3 } , 0 ) .$ 宝哥数学 宝哥数 权所有所有\n   252\t\n   253\t2.设 $f ( x ) = \\int _ { 1 } ^ { + \\infty } \\frac { \\cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t , x \\in ( - \\infty , + \\infty )$\n   254\t\n   255\t(1）试证明积分 $\\int _ { 1 } ^ { + \\infty } \\frac { \\cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \\infty , + \\infty )$ 上一致收敛.\n   256\t\n   257\t(2）试证明函数f(x)在 $( - \\infty , + \\infty )$ 上一致连续.\n   258\t\n   259\t【解答】\n   260\t\n   261\t(1)对任意 $( t , x ) \\in \\left[ 1 , + \\infty \\right) \\times ( - \\infty , + \\infty )$ 有 $\\left| { \\frac { \\cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \\right| \\leq { \\frac { 1 } { 1 + t ^ { 2 } } } . \\ \\int _ { 1 } ^ { + \\infty } { \\frac { d t } { 1 + t ^ { 2 } } }$ 收敛，故版权 宝哥数$\\int _ { 1 } ^ { + \\infty } \\frac { \\cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \\infty , + \\infty )$ 上一致收敛. 哥数学考研所有\n   262\t\n   263\t(2）对任意 $\\left( t , x \\right) \\in \\left[ 1 , + \\infty \\right) \\times \\left( - \\infty , + \\infty \\right)$ ，有 $\\left| { \\frac { \\partial } { \\partial x } } \\left[ { \\frac { \\cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \\right] \\right| = \\left| { \\frac { - \\sin ( x t ) } { 1 + t ^ { 2 } } } \\right| \\leq { \\frac { 1 } { 1 + t ^ { 2 } } }$ 必究  \n   264\t$\\int _ { 1 } ^ { + \\infty } \\frac { d t } { 1 + t ^ { 2 } }$ $\\int _ { 1 } ^ { + \\infty } \\frac { \\partial } { \\partial x } \\Bigg [ \\frac { \\cos ( x t ) } { t ( 1 + t ^ { 2 } ) } \\Bigg ] d t$ 一致收敛.故f(x)在 $( - \\infty , + \\infty )$ 可导，且  \n   265\t宝哥数 学考 盗版  \n   266\t版权所有 $f ^ { \\prime } ( x ) = \\int _ { 1 } ^ { + \\infty } \\frac { \\hat { \\partial } } { \\partial x } \\left[ \\frac { \\cos ( x t ) } { t { ( 1 + t ^ { 2 } ) } } \\right] d t = - \\int _ { 1 } ^ { + \\infty } \\frac { \\sin ( x t ) } { 1 + t ^ { 2 } } d t ,$ 中哥数\n   267\t\n   268\t$$\n   269\t\\big | f ^ { \\prime } ( x ) \\big | = | - \\int _ { 1 } ^ { + \\infty } { \\frac { \\sin ( x t ) } { 1 + t ^ { 2 } } } d t | \\leq \\int _ { 1 } ^ { + \\infty } { \\frac { | \\sin ( x t ) | } { 1 + t ^ { 2 } } } d t < \\int _ { 1 } ^ { + \\infty } { \\frac { 1 } { 1 + t ^ { 2 } } } d t = \\arctan t | 1 ^ { + \\infty } = { \\frac { \\pi } { 4 } } + { \\frac { 1 } { \\pi } } + { \\frac { 1 } { \\pi } } | \\sin ( x t ) | \\operatorname { d } t .\n   270\t$$\n   271\t\n   272\t故函数f(x)在 $( - \\infty , + \\infty )$ 上一致连续.\n"}

## tool · 2026-10-19T07:22:59Z


Script completed
Wall time 5.1 seconds
Output:

# 杭州电子科技大学2023年数学分析真题

## 一.填空题 (本大题共8 小题,每小题 5 分，共 40 分)

1.已知 $f ( x ) = { \frac { x } { \sqrt { 1 + x ^ { 2 } } } }$ ，设 $f _ { n } ( x ) = f ( f ( \cdots f ( x ) ) )$ ，则f2023（0)=

2. $\operatorname* { l i m } _ { n \to \infty } n ( { \sqrt { n ^ { 2 } + 1 } } - n ) =$

$F ( x ) = \int _ { a } ^ { x } f ( t ) ( t - x ) d t$ 则F(x)在[a,b]上的 导数F(x)= 考研考傅 贩必究

4. $\int _ { - \infty } ^ { + \infty } { \tt e } ^ { - x ^ { 2 } } d x =$

5.函数 W $f ( x ) = \left\{ \begin{array} { l l } { \displaystyle \cos \frac { \pi x } { 2 } , \big | x \big | \leq 1 } \\ { \big | x - 1 \big | , \big | x \big | > 1 } \end{array} \right.$ 的间断点为

6.级数 $\sum _ { n = 2 } ^ { \infty } ( 1 + { \frac { 1 } { n } } ) ^ { n ( n + 1 ) } x ^ { n }$ 的收敛半径为考

7.设曲线L是圆 $x ^ { 2 } + y ^ { 2 } = r ^ { 2 }$ 在第一象限内的部分，则 $\int _ { L } x y d l =$ 研

8. $\int { \frac { 1 } { x ( 1 + x ^ { n } ) } } d x =$ ·

## 二.计算题(本大题共5小题，每小题10分，共50 分)

1.计算 $\int _ { L } { ( - 2 x e ^ { - x ^ { 2 } } \sin y ) d x } + { ( e ^ { - x ^ { 2 } } \cos y + x ^ { 6 } ) d y }$ ,这里L为从点(1,0)到(-1,0) 的半圆 $y = \sqrt { 1 - x ^ { 2 } } ( - 1 \leq x \leq 1 )$ 無考博 必究

2.求 $\operatorname* { l i m } _ { x \to \infty } \left[ x - x ^ { 2 } \ln \left( 1 + { \frac { 1 } { x } } \right) \right]$

3.求 $\sum _ { n = 1 } ^ { \infty } { \frac { 2 n } { 3 ^ { n } } }$ 的和.

4.计算 $\oint _ { \Gamma } x ^ { 2 } y d x + y ^ { 2 } d y + z d z$ ,其中r是圆柱 $x ^ { 2 } + y ^ { 2 } = 1$ 与平面x+z=1的交线，从z 轴的正向看去，为逆时针方向.

5.计算 $\iint _ { \Omega } { x ^ { 2 } \sqrt { { x ^ { 2 } + y ^ { 2 } } } d x d y d z }$ ,其中Ω是曲面 $z = \sqrt { x ^ { 2 } + y ^ { 2 } }$ 与平面 $z = x ^ { 2 } + y ^ { 2 }$ 所围成有 学考研考 版必究的区域. 老博

## 三.证明题(本大题共4小题，每小题10分，共40 分)

1.证明： $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { x ^ { 2 } + n } { n ^ { 2 } } }$ 在任何有限区域[a,b]上一致收敛，而在实轴上任何一点都不绝对收敛. 版权所

2.设奇函数f(x)在[-1,1]上具有二阶导数，且f(1)=1,证明：

(1)存在 $\xi \in ( 0 , 1 )$ ，使得f(§)=1;

(2)存在η∈(-1,1)，使得 $f ^ { \prime \prime } ( \eta ) + f ^ { \prime } ( \eta ) = 1$

3.设f(x)在[0,1]上连续，证明： $\iint f ( 1 - y ) f ( x ) d x d y = \frac { 1 } { 2 } \Bigl [ \int _ { 0 } ^ { 1 } f ( x ) d x \Bigr ] ^ { 2 }$ 其中D

为以O(0,0),A(0,1),B(1,0)为顶点的三角形所围成的区域.

4.已知△表示L2pl2ce算符，即： $\Delta u = \frac { \hat { \sigma } ^ { 2 } u } { \hat { \sigma } { x } ^ { 2 } } + \frac { \hat { \sigma } ^ { 2 } u } { \hat { \sigma } { y } ^ { 2 } } + \frac { \hat { \sigma } ^ { 2 } u } { \hat { \sigma } { z } ^ { 2 } }$ ．证明：

$$
\begin{array} { r } { \Delta ( u \nu ) = ( \Delta u ) \nu + 2 \nabla u \cdot \nabla \nu + u ( \Delta \nu ) . } \end{array}
$$

这里Vu表示函数u在点(x,y,z)处的梯度，“."表示点乘.

## 四.综合题(本大题共2小题，共30分)

1.(10分)求两个曲面x+2y=1和 $x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 的交线上距离原点最近的点.

2.设 $f ( x ) = \int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t , x \in ( - \infty , + \infty )$

(1）试证明积分 $\int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \infty , + \infty )$ 上一致收敛.

(2）试证明函数f(x)在 $( - \infty , + \infty )$ 上一致连续.(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/umsb.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/mt-msb.cfg)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/jknapl
tx/ursfs.fd)

LaTeX Font Warning: Font shape `U/rsfs/m/n' in size <10.53937> not available
(Font)              size <10.95> substituted on input line 109.


(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/esint/
uesint.fd)

LaTeX Warning: Command \textcircled invalid in math mode on input line 109.


(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/lm/oms
lmr.fd)

LaTeX Warning: Command \textcircled invalid in math mode on input line 109.

/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/syntax-check-2018-2023/e
3e469709b9c871a/document.tex:122: Limit controls must follow a math operator.
l.122 \(2 ⨏ \limits
                    _ { 2 0 } ^ { 1 } a 3 ( x ) = \frac { 1 } { ( 1 + 2 0 2 ...

No pages of output.
Transcript written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/sy
ntax-check-2018-2023/e3e469709b9c871a/document.log.

{"chunk_id":"3e670b","wall_time_seconds":5.003668,"session_id":52949,"original_token_count":416,"output":"{\"key\": \"be2d15e5112d94ec\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学数分高代(高代不含答案双科版).pdf\", \"exit_code\": 1, \"errors\": [\"e2d15e5112d94ec/document.tex:137: Undefined control sequence.\"]}\n{\"key\": \"e3e469709b9c871a\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf\", \"exit_code\": 1, \"errors\": [\"3e469709b9c871a/document.tex:122: Limit controls must follow a math operator.\"]}\n{\"key\": \"e43b7f46d6f192ef\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"9e64c36cdac10429\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"92a5bd5ef85605e7\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 1, \"errors\": [\"2a5bd5ef85605e7/document.tex:487: Argument of \\\\end  has an extra }.\"]}\n{\"key\": \"391fa17a5f0f6f61\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 1, \"errors\": [\"91fa17a5f0f6f61/document.tex:434: Argument of \\\\end  has an extra }.\"]}\n{\"key\": \"176002d27d3f75a0\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"918271f5178ca024\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n"}

## tool · 2026-10-19T07:23:19Z


Script completed
Wall time 0.2 seconds
Output:

2.用一致连续的定义证明：函数$( x ) = \cos { \sqrt { x } }$ 在 $\textstyle { \left[ a , + \infty \right) ( a > 0 ) }$ 上一致连续.  
【宝哥解答】

对任意 $x , y \in \left[ a , + \infty \right)$ 使得 ，由拉格朗日中值定理，存在 $\xi = \theta x + ( 1 - \theta ) y , \theta \in [ 0 , 1 ]$

故

$$
f ( x ) - f ( y ) = f ^ { \prime } ( \xi ) ( x - y ) = - \frac { \sin \sqrt { \xi } } { 2 \sqrt { \xi } } ( x - y ) ,
$$

$$
\left| f ( x ) - f ( y ) \right| = \left| - { \frac { \sin { \sqrt { \xi } } } { 2 { \sqrt { \xi } } } } ( x - y ) \right| \leq { \frac { 1 } { 2 } } { \big | } x - y { \big | } .
$$

对任意 $\varepsilon > 0$ ，取 $\delta = 2 \varepsilon .$ 则对任意$x , y \in \left[ a , + \infty \right)$ 只要 $\vert x - y \vert < \delta$ 就有  
$\vert f ( x ) - f ( y ) \vert < \varepsilon ^ { \ast } ,$ 故函数 $f ( x ) = \cos { \sqrt { x } }$ 在 $\textstyle { \left[ a , + \infty \right) ( a > 0 ) }$ 上一致连续.  
3.设/(x)在[a,b]上连续，在(a,b)内可微，且

$$
f ( a ) f ( b ) > 0 \ , f ( a ) f ( \frac { a + b } { 2 } ) < 0 \ ,
$$

证明：存在一点 $\boldsymbol { \xi } \in ( a , b )$ 使得 $f ^ { \prime } ( \xi ) = f ( \xi )$

【宝哥解答】

f（x）在[a,b]上连续，在（a,b）内可微，

$$
f ( a ) f ( b ) > 0 ~ , ~ f ( a ) f ( \frac { a + b } { 2 } ) < 0 .
$$

不妨假设 $f ( a ) > 0 \%$ 则 $f ( b ) > 0$ $f ( \frac { a + b } { 2 } ) < 0$ 由零点定理，存在

$$
c _ { 1 } \in ( a , \frac { a + b } 2 ) , c _ { 2 } \in ( \frac { a + b } 2 , b ) ,
$$

使得 $f ( c _ { 1 } ) = f ( c _ { 2 } ) = 0$

则F(x)在[a,b]上连续，在（0,b)内可微，且令 $F ( x ) = e ^ { - x } f ( x ) , x \in \left[ a , b \right]$ $a < c _ { 1 } < c _ { 2 } < b$ 使得 $F ( c _ { 1 } ) = F ( c _ { 2 } ) = 0$ 由罗尔中值定理，存在 $\xi \in ( c _ { 1 } , c _ { 2 } ) \subset ( a , b )$ 使得 $0 = F ^ { \prime } ( \xi ) = e ^ { - \xi } \left[ f ^ { \prime } ( \xi ) - f ( \xi ) \right] .$ ,即 f(5)=f(5)

4.证明：含参量反常积分 $\sec e ^ { - \frac { \pi } { \alpha } } d x$ 在 $\big [ \alpha _ { 0 } , + \infty \big ) ( \alpha _ { 0 } > 0 )$ 上一致收敛，但在 $( 0 , + \infty )$ 上非一致收敛.

【宝哥解答】

是收敛的，且对任意 $X > 0$ 和含参量反常积分 $\int _ { 0 } ^ { + \infty } x e ^ { - \alpha x } d x$ 在 $( 0 , + \infty )$ $\alpha \in ( 0 , + \infty )$ 有 耳那购买的必为盗版投诉热线：

杭州电子科技大学数学分析+高等代数真题解D

$$
\overbrace { \int _ { X } ^ { + x } x e ^ { - \alpha x } d x = ( - x \overbrace { \alpha } ^ { e ^ { - \alpha x } } - \overbrace { \alpha } ^ { e ^ { - \alpha x } } ) } ^ { + \alpha } \bigg | _ { X } ^ { + \infty } = X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } }
$$

故

$$
\operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , \boldsymbol { * } ^ { x } ] } \Bigl | \int _ { \boldsymbol { \chi } } ^ { + \alpha } \boldsymbol { x } e ^ { - \alpha \boldsymbol { * } } d \boldsymbol { x } \Bigr | = \operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , + \infty ] } ( X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } } ) = X \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } } + \frac { \varepsilon ^ { - \alpha Y } } { \alpha _ { 0 } ^ { 2 } } ,
$$

$$
\operatorname* { s u p } _ { \alpha \in ( 0 , + \infty ) } \left. \int _ { \mathfrak { r } } ^ { + \infty } x e ^ { - \alpha x } d x \right. = \operatorname* { s u p } _ { \alpha \in ( 0 , + \infty ) } ( X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } } ) = + \infty ,
$$

$$
\operatorname* { l i m } _ { X \to + x } \operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , + \infty ) } \biggl | \int _ { X } ^ { + x } x e ^ { - \alpha x } d x \biggr | = \operatorname* { l i m } _ { X \to + \infty } ( X \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } } + \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } ^ { 2 } } ) = 0 ,
$$

$$
\operatorname * { l i m } _ { X  + x } \operatorname* { s u p } _ { \alpha \in ( 0 , + x ) } | \int _ { X } ^ { + x } x e ^ { - \alpha x } d x | = + \infty ,
$$

故含参量反常积分 $\int _ { 0 } ^ { - x } x e ^ { - a x } d x$ 在 $[ \alpha _ { 0 } , + \infty ) ( \alpha _ { 0 } > 0 )$ )上一致收敛，但在(0,+o0)上非一致收敛.

5.设f（x）在 $\left[ a , b \right] \left( a < b \right)$ 上连续且单调递增.求证：

$$
\int _ { a } ^ { b } x f ( x ) d x \geq { \frac { a + b } { 2 } } { \int _ { a } ^ { b } f ( x ) d x } .
$$

【宝哥解答】

$$
\begin{array} { r l } & { \int _ { 0 } ^ { \infty } ( x ) d x - \frac { a + b } { 2 } \int _ { 0 } ^ { b } \int ( x ) d x [ \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( x ) d x  } \\ & { = \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( x ) d x + ( \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( x ) d x  } \\ & { \qquad - \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( x ) d x  } \\ & { = \frac { a + b } { 2 } ( x - \frac { a + b } { 2 } ) f ( \partial a ) d x - \frac { a + b } { 2 } \int _ { 0 } ^ { \infty } ( a + b - \frac { a + b } { 2 } ) f ( a + b - \frac { a + b } { 2 } ) d x } \\ & { \qquad - \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( x ) d x - \frac { a + b } { 2 } \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( a + b - \frac { b } { 2 } ) d x } \\ & { = \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) \frac { b } { 2 } ( x ) d x - \frac { a + b } { 2 } \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( a + b - \frac { a } { 2 } ) d x } \\ & { = \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) \frac { b } { 2 } ( x ) d x - \frac { a + b } { 2 } \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( a + b - \frac { a } { 2 } ) d x } \\ & { \qquad - \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) f ( x ) d x ] d x } \\ &  = \int _ { 0 } ^ { \infty } ( x - \frac { a + b } { 2 } ) \frac { b } { 2 } ( x - \frac { a + b }  \end{array}
$$

在[a,b]上连续且单调增加，对任意 $x \in \left[ a , { \frac { a + b } { 2 } } \right]$ $a + b - x \geq x$ 故

$f ( x ) - f ( a + b - x ) \leq 0$ ，故 $( x - { \frac { a + b } { 2 } } ) { \big [ } f ( x ) - f ( a + b - x ) { \big ] } \geq 0 , x \in { \left[ \begin{array} { l } { a , { \frac { a + b } { 2 } } } \\ { \qquad 2 } \end{array} \right] }$ ，故

$$
\int _ { a } ^ { b } x f ( x ) d x - { \frac { a + b } { 2 } } \int _ { a } ^ { b } f ( x ) d x = \int _ { a } ^ { { \frac { a + b } { 2 } } } ( x - { \frac { a + b } { 2 } } ) [ { \dot { \mathcal { f } } } ( x ) - f ( a + b - x ) ] d x \geq 0 \ ,
$$

即 $\int _ { a } ^ { b } x f ( x ) d x \geq { \frac { a + b } { 2 } } \int _ { a } ^ { b } f ( x ) d x$

## 【宝哥备注3】

本题见宝哥题解精粹第10讲5.2例4.(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/amsfon
ts/ueuf.fd)
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/microt
ype/mt-euf.cfg)
[8]
/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/syntax-check-2018-2023/9
2a5bd5ef85605e7/document.tex:487: Argument of \end  has an extra }.
<inserted text> 
                \par 
l.487 ...c { b } { 2 } ( x - \frac { a + b }  \end
                                                  {array}
Output written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/syntax
-check-2018-2023/92a5bd5ef85605e7/document.pdf (8 pages).
Transcript written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/sy
ntax-check-2018-2023/92a5bd5ef85605e7/document.log.
2023杭州电子科技大学高等代数

计算行列式 $\left| \begin{array} { c c c c c } { { } } & { { 2 } } & { { 3 } } & { { 4 } } & { { 5 } } \\ { { 2 } } & { { 3 } } & { { 4 } } & { { 5 } } & { { 1 } } \\ { { 3 } } & { { 4 } } & { { 5 } } & { { 1 } } & { { 2 } } \\ { { 4 } } & { { 5 } } & { { 1 } } & { { 2 } } & { { 3 } } \\ { { 5 } } & { { 1 } } & { { 2 } } & { { 3 } } & { { 4 } } \end{array} \right|$

## 二设 $A = ( \frac { 1 } { 4 } - \frac { 1 } { 2 } \frac { 0 } { 6 } - \frac { 3 } { 3 } )$

(1）求4x2阶矩阵B，使得 $A B = 0$ .是B的秧☆又

(山）求矩阵X，使得 $A X = E$ ，这里E九单位阵

## 三.设浅性方程组

$$
\begin{array} { r } { \{ \lambda x _ { 1 } + x _ { 2 } + x _ { 3 } + x _ { 4 } = 1 } \\ { x _ { 1 } + \lambda x _ { 2 } + x _ { 3 } + x _ { 4 } = 1 } \\ { x _ { 1 } + x _ { 2 } + \lambda x _ { 3 } + x _ { 4 } = \lambda } \\ { x _ { 1 } + x _ { 2 } + x _ { 3 } + \lambda x _ { 4 } = \lambda } \end{array}
$$

为入为何值时，该成性方程很有雁一醇，年术其任解

方入为何宜时，该浅性方程细有无穷多个醉，年求其道解

$f ( x _ { 1 } , x _ { 2 } , x _ { 3 } ) = 2 x _ { 1 } ^ { 2 } + 5 x _ { 2 } ^ { 2 } + 5 x _ { 3 } ^ { 2 } + 4 x _ { 1 } x _ { 2 } - 4 x _ { 1 } x _ { 3 } - 8 x _ { 2 } x _ { 3 }$ 用正交变换x:TY将二次型 $f ( x _ { 1 } , x _ { 2 } , x _ { 3 } )$ 化如标准形，求正交矩降T.

五设 $\mathcal { E } _ { 1 } , \mathcal { E } _ { 2 } , \mathcal { E } _ { 3 }$ 是了维浅垃它间V的一细基，浅垃变换在这细基下的$A = ( \frac { 1 } { - 1 } , 2 , \frac { 2 } { 5 } )$

求在基 $T _ { 1 } = C _ { 1 } - 2 C _ { 2 }$ $1 2 = 3 2 _ { 2 } - 2 _ { 3 } , 1 7 _ { 3 } = 2 3$ 下的矩降B.

(2）求 $\angles { V }$ 与 $\alpha ^ { H } ( 0 )$

六.阳A，B.C妇力n价方降，E力A阶单位阵， $D = C + B C A$ $C = ( E - A B ) ^ { - 1 }$ 证明

六降E-BA可送，且 $D = ( E - B A ) ^ { - 1 }$

（2）C=[+ADB

七.没，P水复几维成性它间√上的成故变接，且好 $= \mathcal { B } A + \mathcal { A } \cdot \mathcal { V } _ { 2 } \vert \sin \alpha \vert 3$ 的的有持正值如.  
(2）A与必有么共的持征向量

八.没家尔数多项式 $f ( x ) = ( x - a _ { 1 } ) ( x - a _ { 2 } ) \cdots ( x - a _ { n } )$ 县中 $a _ { 1 } , \ldots , a _ { n }$ 的实数.涵明：

，多设式 $( f ^ { \prime } ( x ) ) ^ { 2 } - f ( x ) f ^ { \prime \prime } ( x )$ 设有候根，息 $\frac { n } { \frac { 1 } { n } } - \frac { F ( x ) } { ( x - a _ { i } ) F ^ { \prime } ( a _ { i } ) } = 1$

（2) $f ^ { \prime } ( x ) = \sum \limits _ { n = 1 } ^ { n } [ \frac { 1 } { x - a _ { 1 } } \cdot ( \frac { a _ { 1 } } { x } ) ^ { k + 1 } + \frac { 1 } { x } \sum \limits _ { i = 1 } ^ { k } ( \frac { a _ { i } } { x } ) ] \{ x \} ( x ) ( k \in [ 2 ]$

（2）任意多改式于（x）用F(x）除得余式 $\partial _ { 1 } \int \limits _ { i = 1 } ^ { n } \frac { f ( a _ { i } ) F ( x ) } { ( x - a _ { i } ) F ^ { \prime } ( a _ { i } ) }$

.设内是数域P几维成性它间V的浅性变换，☆的特征多改式办

$$
f ( x ) = ( \lambda - \lambda _ { 1 } ) ^ { r _ { 1 } } ( \lambda - \lambda _ { 2 } ) ^ { r _ { 2 } } - - ( \lambda - \lambda _ { 3 } ) ^ { r _ { 3 } }
$$

汕明： $V = V _ { 1 } \textcircled { + } V _ { 2 } \textcircled { + } \cdots \textcircled { + } V _ { s }$

是中 $v _ { 2 } = \{ \rho _ { 1 } ( a _ { 1 } - c - d _ { 1 } ) ^ { 2 } \geq 0 \} \neq \frac { - 3 a \sqrt { 1 } } { 2 }$ $i = 1 , 2 , \cdots 5$ 单位变换入1.一两两互异

## tool · 2026-10-19T07:23:27Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"9d1499","wall_time_seconds":0.000030416,"exit_code":0,"original_token_count":294,"output":"1:## 杭州电子科技大学2021年数学分析真题解析\n3:## 一.填空题(本大题共8小题，每小题5分，共40分)\n58:5.曲面 $e ^ { z } - z + x y = 3$ 在点P(2,1,0)处的切平面方程为(宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线： 91\n60:## 【宝哥解答】\n66:## 【宝哥解答】\n76:## 【宝哥解答】\n82:## 【宝哥解答】\n110:## 【宝哥解答】\n120:## 【宝哥备注1】\n124:4.（本小题10分）计算曲线积分 $\\int _ { L } ( x ^ { 2 } + 3 y ) d x + ( y ^ { 2 } - x ) d y$ ，其中L为从点A(4,0)到点0（0,0）的上半圆周 $y = \\sqrt { 4 x - x ^ { 2 } }$\n140:## 三.综合题(本大题共3小题，每小题10分，共30分)\n196:## 【宝哥解答】\n204:## 四.（本大题共5小题，每小题10分，共50分）\n208:## 【宝哥解答】\n265:4.证明：含参量反常积分 $\\sec e ^ { - \\frac { \\pi } { \\alpha } } d x$ 在 $\\big [ \\alpha _ { 0 } , + \\infty \\big ) ( \\alpha _ { 0 } > 0 )$ 上一致收敛，但在 $( 0 , + \\infty )$ 上非一致收敛.\n297:5.设f（x）在 $\\left[ a , b \\right] \\left( a < b \\right)$ 上连续且单调递增.求证：\n319:## 【宝哥备注3】\n"}
{"chunk_id":"dbea1b","wall_time_seconds":0.00002225,"exit_code":0,"original_token_count":132,"output":"{\"key\": \"52d23623a0404647\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学数分高代真题及答案(双科合卷).pdf\", \"exit_code\": 1, \"errors\": [\"2d23623a0404647/document.tex:230: Extra alignment tab has been changed to \\\\cr.\"]}\n{\"key\": \"cd2a7a833ba8f5fa\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学数分高代真题及答案(双科合卷).pdf\", \"exit_code\": 1, \"errors\": [\"d2a7a833ba8f5fa/document.tex:209: Extra alignment tab has been changed to \\\\cr.\"]}\npassed 10 total 16\n"}

## tool · 2026-10-19T07:24:05Z


Script completed
Wall time 0.6 seconds
Output:

{}
{}
{}

## tool · 2026-10-19T07:24:20Z




## tool · 2026-10-19T07:25:23Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"a9ab80","wall_time_seconds":0.000010542,"exit_code":0,"original_token_count":76,"output":"/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf True\n/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf True\n"}
{}

## tool · 2026-10-19T07:25:32Z


Script completed
Wall time 1.4 seconds
Output:

    ], cwd=folder, env=environment, capture_output=True, text=True, timeout=120)
    (folder / "command.txt").write_text(conversion.stderr + result.stdout + result.stderr)
    lines = result.stdout.splitlines()
    errors = [line for line in lines if "document.tex:" in line or line.startswith("!")]
    record = {"key": key, "source": job["source"], "exit_code": result.returncode, "errors": errors}
    print(json.dumps(record, ensure_ascii=False), flush=True)
    return record


jobs = [job for job in json.loads((work / "jobs.json").read_text())
        if "601数学分析" in job["source"] and 2018 <= int(Path(job["source"]).parent.name) <= 2023]
with ThreadPoolExecutor(max_workers=3) as executor:
    records = list(executor.map(check, jobs))
(target / "results.json").write_text(json.dumps(records, ensure_ascii=False, indent=2))
print("passed", sum(record["exit_code"] == 0 for record in records), "total", len(records))
$$

故

$$
\operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , \boldsymbol { * } ^ { x } ] } \Bigl | \int _ { \boldsymbol { \chi } } ^ { + \alpha } \boldsymbol { x } e ^ { - \alpha \boldsymbol { * } } d \boldsymbol { x } \Bigr | = \operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , + \infty ] } ( X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } } ) = X \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } } + \frac { \varepsilon ^ { - \alpha Y } } { \alpha _ { 0 } ^ { 2 } } ,
$$

$$
\operatorname* { s u p } _ { \alpha \in ( 0 , + \infty ) } \left. \int _ { \mathfrak { r } } ^ { + \infty } x e ^ { - \alpha x } d x \right. = \operatorname* { s u p } _ { \alpha \in ( 0 , + \infty ) } ( X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } } ) = + \infty ,
$$

$$
\operatorname* { l i m } _ { X \to + x } \operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , + \infty ) } \biggl | \int _ { X } ^ { + x } x e ^ { - \alpha x } d x \biggr | = \operatorname* { l i m } _ { X \to + \infty } ( X \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } } + \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } ^ { 2 } } ) = 0 ,
$$

$$
\operatorname * { l i m } _ { X  + x } \operatorname* { s u p } _ { \alpha \in ( 0 , + x ) } | \int _ { X } ^ { + x } x e ^ { - \alpha x } d x | = + \infty ,
$$

故含参量反常积分 $\int _ { 0 } ^ { - x } x e ^ { - a x } d x$ 在 $[ \alpha _ { 0 } , + \infty ) ( \alpha _ { 0 } > 0 )$ )上一致收敛，但在(0,+o0)上非一致收敛.

5.设f（x）在 $\left[ a , b \right] \left( a < b \right)$ 上连续且单调递增.求证：

$$
\int _ { a } ^ { b } x f ( x ) d x \geq { \frac { a + b } { 2 } } { \int _ { a } ^ { b } f ( x ) d x } .
$$

【宝哥解答】

【OCR整理补全】以下分段积分与换元等式按本题题面及本题末尾已识别的正确等式恢复。记 $c=(a+b)/2$，有

$$
\begin{aligned}
\int_a^b xf(x)\,dx-c\int_a^b f(x)\,dx
&=\int_a^b(x-c)f(x)\,dx\\
&=\int_a^c(x-c)f(x)\,dx+\int_c^b(x-c)f(x)\,dx\\
&=\int_a^c(x-c)f(x)\,dx+\int_a^c(c-x)f(a+b-x)\,dx\\
&=\int_a^c(x-c)\bigl[f(x)-f(a+b-x)\bigr]\,dx.
\end{aligned}
$$

在[a,b]上连续且单调增加，对任意 $x \in \left[ a , { \frac { a + b } { 2 } } \right]$ $a + b - x \geq x$ 故

$f ( x ) - f ( a + b - x ) \leq 0$ ，故 $( x - { \frac { a + b } { 2 } } ) { \big [ } f ( x ) - f ( a + b - x ) { \big ] } \geq 0 , x \in { \left[ \begin{array} { l } { a , { \frac { a + b } { 2 } } } \\ { \qquad 2 } \end{array} \right] }$ ，故

$$
\int _ { a } ^ { b } x f ( x ) d x - { \frac { a + b } { 2 } } \int _ { a } ^ { b } f ( x ) d x = \int _ { a } ^ { { \frac { a + b } { 2 } } } ( x - { \frac { a + b } { 2 } } ) [ { \dot { \mathcal { f } } } ( x ) - f ( a + b - x ) ] d x \geq 0 \ ,
$$

即 $\int _ { a } ^ { b } x f ( x ) d x \geq { \frac { a + b } { 2 } } \int _ { a } ^ { b } f ( x ) d x$

## 【宝哥备注3】

本题见宝哥题解精粹第10讲5.2例4.
## 【解答】

(1）f(x)为[-1,1]上的奇函数，故f(0)=0．奇函数f(x)在[-1,1]上具有二阶导数  
且f(1)=1，由拉格朗日中值定理，存在 $\xi \in ( 0 , 1 )$ ，使得 $f ^ { \prime } ( \xi ) = \frac { f ( 1 ) - f ( 0 ) } { 1 - 0 } = 1$ $f ^ { \prime } ( - \xi ) = 1$ ．问题即证明 $f ^ { \prime \prime } ( x ) + f ^ { \prime } ( x ) - 1$ 考  
在(-1,1)内有零点，即 $e ^ { x } \left[ f ^ { \prime \prime } ( x ) + f ^ { \prime } ( x ) - 1 \right] = \left[ e ^ { x } f ^ { \prime } ( x ) - e ^ { x } \right] ^ { \prime }$   
$F ( x ) = e ^ { x } f ( x ) - e ^ { x } , x \in \left[ - 1 , 1 \right]$ ，则F(𝑥)在[-1,1]上连续，在(-1,1)内可导，且  
$F ( \xi ) = F ( - \xi ) = 0$ $\eta \in ( - \xi , \xi ) \subset ( - 1 , 1 )$ ，使得 $F ^ { \prime } ( \eta ) = 0$   
也就是 $f ^ { \prime \prime } ( \eta ) + f ^ { \prime } ( \eta ) = 1$ 考博 从究 来

3.设f(x)在[0,1]上连续，证明： $\iint f ( 1 - y ) f ( x ) d x d y = { \frac { 1 } { 2 } } { \biggl [ } \int _ { 0 } ^ { 1 } f ( x ) d x { \biggr ] } ^ { 2 }$ ，其中D版权所 宝哥数为以 $O ( 0 , 0 ) , A ( 0 , 1 ) , B ( 1 , 0 )$ 为顶点的三角形所围成的区域. 版权所

## 【解答】

区域D如下图所示：

<!-- image-->

$$
\begin{array} { l } { { \displaystyle \iint f ( 1 - y ) f ( x ) d x d y = \int _ { 0 } ^ { 1 } f ( x ) d x \int _ { 0 } ^ { 1 - x } f ( 1 - y ) d y ~ ^ { y = 1 - y } } } \\ { { \displaystyle = \int _ { 0 } ^ { 1 } f ( x ) d x \int _ { x } ^ { 1 } f ( t ) d t = \int _ { 0 } ^ { 1 } f ( x ) \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] d x = - \int _ { 0 } ^ { 1 } \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] d \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] . } } \\ { { \displaystyle = - \frac { 1 } { 2 } \biggl [ \int _ { x } ^ { 1 } f ( t ) d t \biggr ] ^ { 2 } \left| 0 - \frac { 1 } { 2 } \biggl [ \int _ { 0 } ^ { 1 } f ( t ) d t \biggr ] ^ { 2 } \right. } } \end{array}
$$

4. 已知 $\Delta$ 表示 Laplace 算符，即
$$
\Delta u=\frac{\partial^2u}{\partial x^2}+
\frac{\partial^2u}{\partial y^2}+
\frac{\partial^2u}{\partial z^2}.
$$
证明：
$$
\Delta(uv)=(\Delta u)v+2\nabla u\cdot\nabla v+u(\Delta v).
$$
这里 $\nabla u$ 表示函数 $u$ 在点 $(x,y,z)$ 处的梯度，“$\cdot$”表示点乘。

【解答；OCR整理补全】原识别文本中的偏导符号及展开末尾损坏。以下依据本题已识别的目标恒等式，按逐项乘积法则恢复相应公式；本说明由助手添加。

$$
\begin{aligned}
\Delta(uv)
&=\frac{\partial^2(uv)}{\partial x^2}
+\frac{\partial^2(uv)}{\partial y^2}
+\frac{\partial^2(uv)}{\partial z^2}\\
&=(u_{xx}v+2u_xv_x+uv_{xx})
 +(u_{yy}v+2u_yv_y+uv_{yy})
 +(u_{zz}v+2u_zv_z+uv_{zz})\\
&=(u_{xx}+u_{yy}+u_{zz})v
 +2(u_xv_x+u_yv_y+u_zv_z)
 +u(v_{xx}+v_{yy}+v_{zz})\\
&=(\Delta u)v+2\nabla u\cdot\nabla v+u(\Delta v).
\end{aligned}
$$

## 四.综合题(本大题共2小题，共30 分)

1.(10分）求两个曲面 $x + 2 y = 1$ 和 $x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 的交线上距离原点最近的点.【解答】 所有 哥数学 新有盗 学考 现

任取交线上的一点(x,y,z)，则 $\left\{ { x + 2 y = 1 \atop x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1 } \right.$ ，其到原点的距离平方为  
$d = x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } - y ^ { 2 } = 1 - y ^ { 2 }$ ．这样，问题即转化为求y的最大值了.$x + 2 y = 1$ 双 $x = 1 - 2 y$ ，故 $( 1 - 2 y ) ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 即 $z ^ { 2 } = 4 y - 6 y ^ { 2 } \geq 0$ 考研象  
$0 \leq y \leq \frac { 2 } { 3 }$ $y = \frac { 2 } { 3 }$ $z = 0 , x = 1 - 2 y = - \frac { 1 } { 3 }$ ，故交线上距离原点最近的点为所有司  
$( - \frac { 1 } { 3 } , \frac { 2 } { 3 } , 0 ) .$ 宝哥数学 宝哥数 权所有所有

2.设 $f ( x ) = \int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t , x \in ( - \infty , + \infty )$

(1）试证明积分 $\int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \infty , + \infty )$ 上一致收敛.

(2）试证明函数f(x)在 $( - \infty , + \infty )$ 上一致连续.

【解答】

(1)对任意 $( t , x ) \in \left[ 1 , + \infty \right) \times ( - \infty , + \infty )$ 有 $\left| { \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \right| \leq { \frac { 1 } { 1 + t ^ { 2 } } } . \ \int _ { 1 } ^ { + \infty } { \frac { d t } { 1 + t ^ { 2 } } }$ 收敛，故版权 宝哥数$\int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \infty , + \infty )$ 上一致收敛. 哥数学考研所有

(2）对任意 $\left( t , x \right) \in \left[ 1 , + \infty \right) \times \left( - \infty , + \infty \right)$ ，有 $\left| { \frac { \partial } { \partial x } } \left[ { \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \right] \right| = \left| { \frac { - \sin ( x t ) } { 1 + t ^ { 2 } } } \right| \leq { \frac { 1 } { 1 + t ^ { 2 } } }$ 必究  
$\int _ { 1 } ^ { + \infty } \frac { d t } { 1 + t ^ { 2 } }$ $\int _ { 1 } ^ { + \infty } \frac { \partial } { \partial x } \Bigg [ \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } \Bigg ] d t$ 一致收敛.故f(x)在 $( - \infty , + \infty )$ 可导，且  
宝哥数 学考 盗版  
版权所有 $f ^ { \prime } ( x ) = \int _ { 1 } ^ { + \infty } \frac { \hat { \partial } } { \partial x } \left[ \frac { \cos ( x t ) } { t { ( 1 + t ^ { 2 } ) } } \right] d t = - \int _ { 1 } ^ { + \infty } \frac { \sin ( x t ) } { 1 + t ^ { 2 } } d t ,$ 中哥数

$$
\big | f ^ { \prime } ( x ) \big | = | - \int _ { 1 } ^ { + \infty } { \frac { \sin ( x t ) } { 1 + t ^ { 2 } } } d t | \leq \int _ { 1 } ^ { + \infty } { \frac { | \sin ( x t ) | } { 1 + t ^ { 2 } } } d t < \int _ { 1 } ^ { + \infty } { \frac { 1 } { 1 + t ^ { 2 } } } d t = \arctan t | 1 ^ { + \infty } = { \frac { \pi } { 4 } } + { \frac { 1 } { \pi } } + { \frac { 1 } { \pi } } | \sin ( x t ) | \operatorname { d } t .
$$

故函数f(x)在 $( - \infty , + \infty )$ 上一致连续.

{}
{"chunk_id":"5e0edc","wall_time_seconds":1.001455292,"session_id":41819,"original_token_count":0,"output":""}

## tool · 2026-10-19T07:25:58Z


Script completed
Wall time 0.3 seconds
Output:

{}
{"chunk_id":"63adaa","wall_time_seconds":0.000037042,"exit_code":0,"original_token_count":546,"output":"{\"key\": \"27ea8f6e4eb7355d\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"1abbef1daec3bc92\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"f6badbfa1728d169\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"3f7b5ea1df00c613\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"128a26e7394a073e\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"2c29e49c601a658a\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"e3e469709b9c871a\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"e43b7f46d6f192ef\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"9e64c36cdac10429\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"92a5bd5ef85605e7\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"391fa17a5f0f6f61\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"176002d27d3f75a0\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"918271f5178ca024\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\npassed 13 total 13\n"}
{"chunk_id":"324e4d","wall_time_seconds":0.000018083,"exit_code":0,"original_token_count":517,"output":"\\documentclass[11pt,fontset=fandol]{ctexart}\n\\usepackage[a4paper,margin=23mm]{geometry}\n\\usepackage{amsmath,amssymb,mathtools,bm,mathrsfs,esint}\n\\usepackage{graphicx,longtable,booktabs,array,calc}\n\\usepackage[normalem]{ulem}\n\\usepackage{xcolor,hyperref}\n\\hypersetup{hidelinks}\n\\setcounter{secnumdepth}{-1}\n\\providecommand{\\tightlist}{\\setlength{\\itemsep}{0pt}\\setlength{\\parskip}{0pt}}\n\\providecommand{\\passthrough}[1]{#1}\n$for(header-includes)$\n$header-includes$\n$endfor$\n\\begin{document}\n$body$\n\\end{document}\nimport hashlib\nimport importlib.util\nimport json\nimport os\nimport subprocess\nfrom concurrent.futures import ThreadPoolExecutor\nfrom pathlib import Path\n\n\nwork = Path(__file__).resolve().parent\nspec = importlib.util.spec_from_file_location(\"hdu_existing_builder\", work / \"build.py\")\nbuilder = importlib.util.module_from_spec(spec)\nspec.loader.exec_module(builder)\nbinary = Path(\"/Volumes/SamsungSSD990PRO/Application/texlive/2025/bin/universal-darwin\")\nenvironment = dict(os.environ, PATH=str(binary) + os.pathsep + os.environ[\"PATH\"])\ntarget = work / \"syntax-check-2018-2023\"\ntarget.mkdir(exist_ok=True)\n\n\ndef check(job):\n    key = hashlib.sha256(job[\"input\"].encode()).hexdigest()[:16]\n    source = work / \"overrides\" / (key + \".md\")\n    if not source.exists():\n        source = work / (key + \".md\")\n    folder = target / key\n    folder.mkdir(exist_ok=True)\n    markdown = folder / \"document.md\"\n    markdown.write_text(builder.normalize(source.read_text()))\n    tex = folder / \"document.tex\"\n    conversion = subprocess.run([\n        builder.PANDOC, \"-f\", \"markdown+tex_math_dollars+tex_math_single_backslash\",\n        \"-t\", \"latex\", \"--standalone\", \"-V\", \"documentclass=ctexart\",\n        \"-V\", \"classoption=fontset=fandol\", \"-V\", \"mathspec=true\",\n        \"-H\", str(work / \"header.tex\"), str(markdown), \"-o\", str(tex),\n    ], capture_output=True, text=True, check=True)\n    result = subprocess.run([\n        str(binary / \"xelatex\"), \"-interaction=nonstopmode\", \"-halt-on-error\",\n        \"-file-line-error\", \"-output-directory=\" + str(folder), str(tex),\n"}

## tool · 2026-10-19T07:26:06Z


Script completed
Wall time 1.4 seconds
Output:

{}
{"chunk_id":"d51ade","wall_time_seconds":1.003995292,"session_id":99126,"original_token_count":0,"output":""}

## tool · 2026-10-19T07:26:26Z


Script completed
Wall time 5.6 seconds
Output:

{"chunk_id":"d70ed7","wall_time_seconds":2.07048475,"exit_code":0,"original_token_count":21,"output":"PASS: 2021换元式5种多项式交叉核对、2023 Laplace乘积公式符号核对\n"}
{"chunk_id":"321975","wall_time_seconds":3.2869365,"exit_code":0,"original_token_count":564,"output":"{\"key\": \"1abbef1daec3bc92\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"f6badbfa1728d169\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"27ea8f6e4eb7355d\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"128a26e7394a073e\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"3f7b5ea1df00c613\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"2c29e49c601a658a\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"e3e469709b9c871a\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf\", \"exit_code\": 1, \"errors\": [\"3e469709b9c871a/document.tex:79: LaTeX Error: No counter 'none' defined.\"]}\n{\"key\": \"9e64c36cdac10429\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"e43b7f46d6f192ef\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"92a5bd5ef85605e7\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"391fa17a5f0f6f61\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"176002d27d3f75a0\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"918271f5178ca024\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\npassed 12 total 13\n"}

## tool · 2026-10-19T07:26:31Z


Script completed
Wall time 0.1 seconds
Output:

     1	\documentclass[11pt,fontset=fandol]{ctexart}
     2	\usepackage[a4paper,margin=23mm]{geometry}
     3	\usepackage{amsmath,amssymb,mathtools,bm,mathrsfs,esint}
     4	\usepackage{graphicx,longtable,booktabs,array,calc}
     5	\usepackage[normalem]{ulem}
     6	\usepackage{xcolor,hyperref}
     7	\hypersetup{hidelinks}
     8	\setcounter{secnumdepth}{-1}
     9	\providecommand{\tightlist}{\setlength{\itemsep}{0pt}\setlength{\parskip}{0pt}}
    10	\providecommand{\passthrough}[1]{#1}
    11	\usepackage{amssymb,mathrsfs,esint,bm,newunicodechar}
    12	\allowdisplaybreaks
    13	\setlength{\emergencystretch}{3em}
    14	\newunicodechar{∞}{\ensuremath{\infty}}
    15	\newunicodechar{∈}{\ensuremath{\in}}
    16	\newunicodechar{∑}{\ensuremath{\sum}}
    17	\newunicodechar{∫}{\ensuremath{\int}}
    18	\newunicodechar{≤}{\ensuremath{\leq}}
    19	\newunicodechar{≥}{\ensuremath{\geq}}
    20	\newunicodechar{≠}{\ensuremath{\neq}}
    21	\newunicodechar{→}{\ensuremath{\to}}
    22	\newunicodechar{⇒}{\ensuremath{\Rightarrow}}
    23	\newunicodechar{α}{\ensuremath{\alpha}}
    24	\newunicodechar{β}{\ensuremath{\beta}}
    25	\newunicodechar{γ}{\ensuremath{\gamma}}
    26	\newunicodechar{λ}{\ensuremath{\lambda}}
    27	\newunicodechar{φ}{\ensuremath{\varphi}}
    28	\newunicodechar{ε}{\ensuremath{\varepsilon}}
    29	\newunicodechar{σ}{\ensuremath{\sigma}}
    30	\newunicodechar{θ}{\ensuremath{\theta}}
    31	\newunicodechar{δ}{\ensuremath{\delta}}
    32	\newunicodechar{η}{\ensuremath{\eta}}
    33	\newunicodechar{π}{\ensuremath{\pi}}
    34	\newunicodechar{ξ}{\ensuremath{\xi}}
    35	\newunicodechar{Σ}{\ensuremath{\Sigma}}
    36	\newunicodechar{Δ}{\ensuremath{\Delta}}
    37	\newunicodechar{∂}{\ensuremath{\partial}}
    38	\newunicodechar{∀}{\ensuremath{\forall}}
    39	\newunicodechar{∃}{\ensuremath{\exists}}
    40	\newunicodechar{√}{\ensuremath{\surd}}
    41	\newunicodechar{−}{\ensuremath{-}}
    42	\newunicodechar{μ}{\ensuremath{\mu}}
    43	\newunicodechar{ρ}{\ensuremath{\rho}}
    44	\newunicodechar{τ}{\ensuremath{\tau}}
    45	\newunicodechar{ω}{\ensuremath{\omega}}
    46	\newunicodechar{Ω}{\ensuremath{\Omega}}
    47	\newunicodechar{χ}{\ensuremath{\chi}}
    48	\newunicodechar{ψ}{\ensuremath{\psi}}
    49	\newunicodechar{Γ}{\ensuremath{\Gamma}}
    50	\newunicodechar{Φ}{\ensuremath{\Phi}}
    51	\newunicodechar{Λ}{\ensuremath{\Lambda}}
    52	\newunicodechar{ℝ}{\ensuremath{\mathbb{R}}}
    53	\newunicodechar{ℤ}{\ensuremath{\mathbb{Z}}}
    54	\newunicodechar{ℕ}{\ensuremath{\mathbb{N}}}
    55	\newunicodechar{△}{\ensuremath{\triangle}}
    56	\newunicodechar{⊗}{\ensuremath{\otimes}}
    57	\begin{document}
    58	\section{杭州电子科技大学2023年数学分析手写详细版：互证整理与识读状态}\label{ux676dux5ddeux7535ux5b50ux79d1ux6280ux5927ux5b662023ux5e74ux6570ux5b66ux5206ux6790ux624bux5199ux8be6ux7ec6ux7248ux4e92ux8bc1ux6574ux7406ux4e0eux8bc6ux8bfbux72b6ux6001}
    59	
    60	\begin{quote}
    61	原PDF共6页。第1---6页均尚未完成逐页可靠识读，现有整份OCR不含可靠页分隔，不能据此把某段内容归属到某一页。本文件由助手将可与同年打印真题、打印参考答案互证的题目及结论整理成索引；不代表手写原作者的逐字转录，也不替代完整手写解析。未能可靠识别的详细推导仍需核对原稿。
    62	\end{quote}
    63	
    64	\begin{itemize}
    65	\tightlist
    66	\item
    67	  \href{/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf}{完整手写原稿PDF，原页1---6}
    68	\item
    69	  \href{/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf}{同年原打印参考答案PDF}
    70	\item
    71	  \href{/Users/oyamahappa/Documents/Agent/Codex/output/HDU/md/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.md}{同年打印参考答案识别整理稿}
    72	\item
    73	  \href{/Users/oyamahappa/Documents/Agent/Codex/output/HDU/md/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.md}{同年打印真题识别稿}
    74	\end{itemize}
    75	
    76	\subsection{原页识读状态}\label{ux539fux9875ux8bc6ux8bfbux72b6ux6001}
    77	
    78	{\def\LTcaptype{none} % do not increment counter
    79	\begin{longtable}[]{@{}lll@{}}
    80	\toprule\noalign{}
    81	原PDF页序 & 状态 & 处理 \\
    82	\midrule\noalign{}
    83	\endhead
    84	\bottomrule\noalign{}
    85	\endlastfoot
    86	1 & 未完成逐页可靠识读 & 保留原PDF，需逐页核对 \\
    87	2 & 未完成逐页可靠识读 & 保留原PDF，需逐页核对 \\
    88	3 & 未完成逐页可靠识读 & 保留原PDF，需逐页核对 \\
    89	4 & 未完成逐页可靠识读 & 保留原PDF，需逐页核对 \\
    90	5 & 未完成逐页可靠识读 & 保留原PDF，需逐页核对 \\
    91	6 & 未完成逐页可靠识读 & 保留原PDF，需逐页核对 \\
    92	\end{longtable}
    93	}
    94	
    95	\subsection{一、填空题互证索引}\label{ux4e00ux586bux7a7aux9898ux4e92ux8bc1ux7d22ux5f15}
    96	
    97	\subsubsection{1.
    98	迭代函数：函数值与导数的识读差异待核对}\label{ux8fedux4ee3ux51fdux6570ux51fdux6570ux503cux4e0eux5bfcux6570ux7684ux8bc6ux8bfbux5deeux5f02ux5f85ux6838ux5bf9}
    99	
   100	两份识别均能确认 \(f(x)=x/\sqrt{1+x^2}\)，\(f_n\) 为 \(f\) 的 \(n\)
uecounter/uniquecounter.sty)))
(/Volumes/SamsungSSD990PRO/Application/texlive/2025/texmf-dist/tex/latex/newuni
codechar/newunicodechar.sty)
(/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/syntax-check-2018-2023/
e3e469709b9c871a/document.aux)
*geometry* driver: auto-detecting
*geometry* detected driver: xetex

/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/syntax-check-2018-2023/e
3e469709b9c871a/document.tex:79: LaTeX Error: No counter 'none' defined.

See the LaTeX manual or LaTeX Companion for explanation.
Type  H <return>  for immediate help.
 ...                                              
                                                  
l.79 \begin{longtable}[]{@{}lll@{}}
                                   
No pages of output.
Transcript written on /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/sy
ntax-check-2018-2023/e3e469709b9c871a/document.log.


## tool · 2026-10-19T07:26:39Z




## tool · 2026-10-19T07:26:53Z


Script completed
Wall time 1.2 seconds
Output:

# 杭州电子科技大学2023年数学分析手写详细版：互证整理与识读状态

> 原PDF共6页。第1—6页均尚未完成逐页可靠识读，现有整份OCR不含可靠页分隔，不能据此把某段内容归属到某一页。本文件由助手将可与同年打印真题、打印参考答案互证的题目及结论整理成索引；不代表手写原作者的逐字转录，也不替代完整手写解析。未能可靠识别的详细推导仍需核对原稿。

- [完整手写原稿PDF，原页1—6](/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf)
- [同年原打印参考答案PDF](/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf)
- [同年打印参考答案识别整理稿](/Users/oyamahappa/Documents/Agent/Codex/output/HDU/md/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.md)
- [同年打印真题识别稿](/Users/oyamahappa/Documents/Agent/Codex/output/HDU/md/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.md)

## 原页识读状态

| 原PDF页序 | 状态 | 处理 |
| --- | --- | --- |
| 1 | 未完成逐页可靠识读 | 保留原PDF，需逐页核对 |
| 2 | 未完成逐页可靠识读 | 保留原PDF，需逐页核对 |
| 3 | 未完成逐页可靠识读 | 保留原PDF，需逐页核对 |
| 4 | 未完成逐页可靠识读 | 保留原PDF，需逐页核对 |
| 5 | 未完成逐页可靠识读 | 保留原PDF，需逐页核对 |
| 6 | 未完成逐页可靠识读 | 保留原PDF，需逐页核对 |

## 一、填空题互证索引

### 1. 迭代函数：函数值与导数的识读差异待核对

两份识别均能确认 $f(x)=x/\sqrt{1+x^2}$，$f_n$ 为 $f$ 的 $n$ 次复合。手写识别可恢复的计算结构为

\[
f_n(x)=\frac{x}{\sqrt{1+nx^2}},\qquad
f_n'(x)=\frac1{(1+nx^2)^{3/2}}.

{}
{"chunk_id":"aabf4f","wall_time_seconds":1.001867166,"session_id":24444,"original_token_count":0,"output":""}

## tool · 2026-10-19T07:27:07Z


Script completed
Wall time 4.2 seconds
Output:

{"chunk_id":"d0716b","wall_time_seconds":4.044151875,"exit_code":0,"original_token_count":546,"output":"{\"key\": \"f6badbfa1728d169\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"1abbef1daec3bc92\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"27ea8f6e4eb7355d\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"128a26e7394a073e\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"2c29e49c601a658a\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"3f7b5ea1df00c613\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"e3e469709b9c871a\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"e43b7f46d6f192ef\", \"source\": \"HDU/601数学分析/2018/2018年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"9e64c36cdac10429\", \"source\": \"HDU/601数学分析/2019/2019年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"92a5bd5ef85605e7\", \"source\": \"HDU/601数学分析/2021/2021年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"391fa17a5f0f6f61\", \"source\": \"HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"176002d27d3f75a0\", \"source\": \"HDU/601数学分析/2022/2022年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\n{\"key\": \"918271f5178ca024\", \"source\": \"HDU/601数学分析/2020/2020年杭州电子科技大学601数学分析考研真题参考答案.pdf\", \"exit_code\": 0, \"errors\": []}\npassed 13 total 13\n"}
{"chunk_id":"93d8a8","wall_time_seconds":0.000020583,"exit_code":0,"original_token_count":31,"output":"92a5bd5ef85605e7 18773\n391fa17a5f0f6f61 20331\ne3e469709b9c871a 7126\nPASS: 手写互证索引19题与全部6页识读限制\n"}

## tool · 2026-10-19T07:27:20Z




## assistant · 2026-10-19T07:27:30Z

妹妹，已完成3份修复稿，并实编译检查2018—2023数学分析共13份文档，全部通过。

- [2021打印答案修复](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/overrides/92a5bd5ef85605e7.md)
- [2023打印答案修复](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md)
- [2023手写版互证索引](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/overrides/e3e469709b9c871a.md)
- [编译记录](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/syntax-check-2018-2023/results.json)

手写版保留19题可靠索引，明确原页1—6均未完成逐页可靠转录。

未修改output、builder或Git；编译通过不代表已全面复核原打印答案的数学正确性。

## tool · 2026-10-19T07:27:59Z




## developer · 2026-10-19T07:28:00Z

The following namespaces are no longer available. Do not call tools in them unless those tools are declared in a later update:
- mcp__cua_repl

## developer · 2026-10-19T07:28:00Z

<tools>
Removed deferred tool namespaces:
- mcp__code_review
</tools>

## tool · 2026-10-19T07:28:04Z


Script completed
Wall time 0.1 seconds
Output:

## 杭州电子科技大学2018年数学分析真题解析

## 一.填空题(本大题共8小题，每小题5分，本大题共40分)

1. $\operatorname* { l i m } _ { n  \infty } ( 2 ^ { n } + 3 ^ { n } + 4 ^ { n } ) ^ { \frac { 1 } { n } } = ($

【宝哥解答】

是k个非负常数，则一般地，设 $a _ { 1 } , a _ { 2 } , \cdots , a _ { k }$

$$
\operatorname* { l i m } _ { n \to \infty } \sqrt [ n ] { a _ { 1 } ^ { n } + a _ { 2 } ^ { n } + \cdots + a _ { k } ^ { n } } = \operatorname* { m a x } ( a _ { 1 } , a _ { 2 } , \cdots , a _ { k } )
$$

证明：

不妨设 $a _ { 1 } = \operatorname* { m a x } ( a _ { 1 } , a _ { 2 } , \cdots , a _ { k } )$ ，则

$$
a _ { 1 } \leq \sqrt [ n ] { a _ { 1 } ^ { n } + a _ { 2 } ^ { n } + \cdots + a _ { k } ^ { n } } \leq \sqrt [ n ] { k a _ { 1 } ^ { n } }  a _ { 1 2 } ^ { , n }  \infty ,
$$

故 $\operatorname* { l i m } _ { n \to \infty } { \sqrt { a _ { 1 } ^ { n } + a _ { 2 } ^ { n } + \cdots + a _ { k } ^ { n } } } = a _ { 1 } = \operatorname* { m a x } ( a _ { 1 } , a _ { 2 } , \cdots a _ { k }$

2,3,4都是正数，于是， $\operatorname* { l i m } _ { n \to \infty } ( 2 ^ { n } + 3 ^ { n } + 4 ^ { n } ) ^ { \frac { 1 } { n } } = \operatorname* { m a x } ( 2 , 3 , 4 ) = 4$

2.设函数f（x）在x=1处可导， $x = 1$ $f ^ { \prime } ( 1 ) = 3$ ，则 $\operatorname* { l i m } _ { x \to 0 } { \frac { f ( 1 + x ) - f ( 1 - 3 x ) } { x } } = ($

$$
\begin{array} { l } { \displaystyle \operatorname* { l i m } _ { x \to 0 } \frac { f ( 1 + x ) - f ( 1 - 3 x ) } { x } = \operatorname* { l i m } _ { x \to 0 } \left[ \frac { f ( 1 + x ) - f ( 1 ) } { x } + 3 \frac { f ( 1 - 3 x ) - f ( 1 ) } { - 3 x } \right] } \\ { = f ^ { \prime } ( 1 ) + 3 f ^ { \prime } ( 1 ) = 4 f ^ { \prime } ( 1 ) = 4 \times 3 = 1 2 } \end{array}
$$

3.已知 $e ^ { x + y } = \sin ( x y )$ 确定了隐函数y=y(x)，则 $\frac { d y } { d x } =$ 研习

## 【宝哥解答】

令 $F ( x , y ) = e ^ { x + y } - \sin ( x y )$ ，由隐函数存在定理的结论，

$$
\frac { d y } { d x } = - \frac { F _ { x } } { F _ { y } } = - \frac { e ^ { x + y } - y \cos ( x y ) } { e ^ { x + y } - x \cos ( x y ) }
$$

4.设 $F ( x ) = \int _ { 0 } ^ { 2 x } x e ^ { t ^ { 2 } } d t$ ，则 $F ^ { \prime } ( x ) = ($

## 【宝哥解答】

$$
F ( x ) = \int _ { 0 } ^ { 2 x } x e ^ { t ^ { 2 } } d t = x \int _ { 0 } ^ { 2 x } e ^ { t ^ { 2 } } d t \ ,
$$

$$
F ^ { \prime } ( x ) = \int _ { 0 } ^ { 2 x } e ^ { t ^ { 2 } } d t + x e ^ { ( 2 x ) ^ { 2 } } \cdot 2 = \int _ { 0 } ^ { 2 x } e ^ { t ^ { 2 } } d t + 2 x e ^ { 4 x ^ { 2 } }
$$

5.设 $u = x ^ { 2 } + y - z ^ { 2 }$ ，则u在(1,-1,1)处的方向导数的最大值为(

## 【宝哥解答】

$$
u = x ^ { 2 } + y - z ^ { 2 } , u _ { x } = 2 x , u _ { y } = 1 , u _ { z } = - 2 z ,
$$

都是连续的，故u在(x,y,z)处的方向导数的最大值就是该点梯度的模，为$\sqrt { u _ { x } ^ { 2 } + u _ { y } ^ { 2 } + u _ { z } ^ { 2 } } = \sqrt { 4 x ^ { 2 } + 1 + 4 z ^ { 2 } }$ ，故u在(1,-1,1)处的方向导数的最大值为$\sqrt { 4 \times 1 ^ { 2 } + 1 + 4 \times 1 ^ { 2 } } = 3$

6.已知(x+ay)dx+(2x+y)dy为某函数的全微分，则a的值是(

## 【宝哥解答】

令P(x，y）=x+ay，Q（x，y）=2x+y，则 $P , \bar { Q }$ 有连续的一阶偏导数.

$P d x + Q d y = ( x + a y ) d x + ( 2 x$ y)dy为某函数的全微分，故 $\frac { \partial P } { \partial y } = \frac { \partial Q } { \partial x }$ ，即a=2.

7.设函数f（x，y）连续，则二次积分 $\int _ { - 2 } ^ { 0 } d x \int _ { 2 x + 4 } ^ { 4 - x ^ { 2 } } f ( x , y ) d y$ 可交换积分次序为

【宝哥解答】

作出积分区域如下图所示：

<!-- image-->

于是，

$$
\int _ { - 2 } ^ { 0 } d x \int _ { 2 x + 4 } ^ { 4 - x ^ { 2 } } f ( x , y ) d y = \int _ { 0 } ^ { 4 } d y \int _ { - \sqrt { 4 - y } } ^ { \frac { y - 4 } { 2 } } f ( x , y ) d x
$$

8.设 $\Sigma : x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = 1$ ，则曲面积分 $( 2 - x ^ { 2 } - y ^ { 2 } - z ^ { 2 } ) d S = ($

## 【宝哥解答】

$\Sigma : x ^ { 2 } + y ^ { 2 }$ +²=1，其面积为 $4 \pi ^ { 2 }$ ，因此，

$$
\oint \limits _ { \Sigma } ( 2 - x ^ { 2 } - y ^ { 2 } - z ^ { 2 } ) d S = \oiint \limits _ { \Sigma } d S = S ( \Sigma ) = 4 \pi
$$

## 二.计算题(本大题共5小题，每小题6分，本大题共30分)

1.求极限值 $\operatorname* { l i m } _ { x  \infty } { \frac { x ^ { 3 } ( 1 - \cos { \frac { 1 } { x ^ { 2 } } } ) } { \sqrt { x ^ { 2 } + 1 } - x } }$

【宝哥解答】

$$
\operatorname* { l i m } _ { x \to + \infty } \frac { x ^ { 3 } ( 1 - \cos \frac { 1 } { x ^ { 2 } } ) } { \sqrt { x ^ { 2 } + 1 } - x } = \overset { \sqrt { \log } } { \underset { x \to + \infty } { \operatorname { d i m } } } x ^ { 3 } ( \frac { \mathbb { L } ^ { 3 } } { 2 } \frac { 1 } { x ^ { 4 } } ) ( \sqrt { x ^ { 2 } + 1 } + x ) = \frac { 1 } { 2 } \operatorname* { l i m } _ { x \to + \infty } ( \sqrt { 1 + \frac { 1 } { x ^ { 2 } } } + 1 ) = \frac { 2 } { 2 } = 1 ,
$$

$$
\operatorname* { l i m } _ { x  - \infty } { \frac { x ^ { 3 } ( 1 - \cos { \frac { 1 } { x ^ { 2 } } } ) } { \sqrt { x ^ { 2 } + 1 } - x } } = \operatorname* { l i m } _ { x  - \infty } { \frac { x ^ { 3 } ( { \frac { 1 } { 2 } } { \frac { 1 } { x ^ { 4 } } } ) } { - 2 x } } = 0 ,
$$

$\operatorname* { l i m } _ { x  + \infty } { \frac { x ^ { 3 } ( 1 - \cos { \frac { 1 } { x ^ { 2 } } } ) } { \sqrt { x ^ { 2 } + 1 } - x } } \neq \operatorname* { l i m } _ { x  - \infty } { \frac { x ^ { 3 } ( 1 - \cos { \frac { 1 } { x ^ { 2 } } } ) } { \sqrt { x ^ { 2 } + 1 } - x } }$ ，因此， $\operatorname* { l i m } _ { x \to \infty } { \frac { x ^ { 3 } ( 1 - \cos { \frac { 1 } { x ^ { 2 } } } ) } { \sqrt { x ^ { 2 } + 1 } - x } }$ 是不存在的.

2.设 $u = u ( x , y )$ $\nu = \nu ( x , y )$ 是由 $\left\{ \begin{array} { l l } { \sin ( u + \nu ) = { \bar { x } } y } \\ { e ^ { u \nu } = 1 - x ^ { 2 } y } \\ { \phantom { } \theta _ { 0 } \leq \nu } \end{array} \right.$ 所确定的隐函数组，求 $\frac { \partial u } { \partial x }$

## 【宝哥解答】

$u = u ( x , y )$ =v（x，y）是由 $\left\{ \begin{array} { l l } { \sin ( u + \nu ) = x y } \\ { e ^ { u \nu } = 1 - x - y } \end{array} \right.$ 所确定的隐函数组，在此方程组的两边取全微分，可得 $\left\{ \begin{array} { l l } { \cos ( u + \nu ) ( d u + d \nu ) = y d x + x d y } \\ { e ^ { u \nu } ( \nu d u + u d \nu ) = - d x - d y } \end{array} \right.$ ，求解这个关于 $d u , d \nu$ 的方程组，可得$d u = \frac { u e ^ { w ^ { w } } ( y d x + x d y ) - \cos ( u + \nu ) ( - d x - d y ) } { u e ^ { w } \cos ( u + \nu ) - \nu e ^ { w ^ { w } } \cos ( u + \nu ) } = \frac { \left[ y u e ^ { w } + \cos ( u + \nu ) \right] d x + \left[ x u e ^ { w } + \cos ( u + \nu ) \right] d y } { \frac { \varkappa e ^ { w } } { \sin ( u - \nu ) e ^ { w } } \cos ( u + \nu ) }$ 故 $\frac { \partial u } { \partial x } = \frac { y u e ^ { u \nu } + \cos ( u + \nu ) } { ( u - \nu ) e ^ { u \nu } \cos ( u + \nu ) }$

3.已知连续函数f（x）满足条件 $t f ( x - t ) d t = 1 - \cos x$ 求 $\int _ { 0 } ^ { \frac { \pi } { 2 } } f ( x ) d x$

## 【宝哥解答】

连续函数f（x）满足条件 $\int _ { 0 } ^ { x } t f ( x - t ) d t = 1 - \cos x$ ，故

$$
\left( \int _ { 0 } ^ { x } t f ( x - t ) d t \right) ^ { \prime } = ( 1 - \cos x ) ^ { \prime } = \sin x
$$

另一方面，

$$
\int _ { 0 } ^ { x } t f ( x - t ) d t = \int _ { 0 } ^ { x } ( x - t ) f ( t ) d t = \int _ { 0 } ^ { x } \int _ { 0 } ^ { x } ( t ) d t - \int _ { 0 } ^ { x } t f ( t ) d t ,
$$

故

$$
\left( \int _ { 0 } ^ { x } t f ( x - t ) d t \right) ^ { \prime } = \left( x \int _ { 0 } ^ { x } \int _ { 0 } ^ { t } t ( t ) d t - \int _ { 0 } ^ { x } t f ( t ) d t \right) ^ { \prime } = x f ( x ) + \int _ { 0 } ^ { x } f ( t ) d t - x f ( x ) = \int _ { 0 } ^ { x } f ( t ) d t ,
$$

故 $\int _ { 0 } ^ { x } f ( t ) d t = \sin { x }$ 代入 $x = \frac { \pi } { 2 }$ ，就可以得到 $\int _ { 0 } ^ { \frac { \pi } { 2 } } f ( x ) d x = \sin { \frac { \pi } { 2 } } = 1$

4.求 $\sum _ { n = 0 } ^ { \infty } { \frac { 1 } { n + 1 } } x ^ { n }$ 的和函数.

## 【宝哥解答】

$\operatorname* { l i m } _ { n \to \infty } { \frac { \frac { 1 } { n } } { \frac { 1 } { n + 1 } } } = 1$ 且其在x=-1收敛，在x=1发散，幂级数 $\sum _ { n = 1 } ^ { \infty } { \frac { x ^ { n } } { n } }$ 的收敛半径为

故其收敛域为[-1,1).记其和函数为S(x)，则对任意 $x \in ( - 1 , 1 )$ ，有

$$
S ( x ) = \sum _ { n = 1 } ^ { \infty } \frac { x ^ { n } } { n ! } = \sum _ { n = 1 } ^ { \infty } \int _ { 0 } ^ { x } t ^ { n - 1 } d t = \int _ { 0 } ^ { x } \sum _ { n = 1 } ^ { \infty } t ^ { n - 1 } d t = \int _ { 0 } ^ { x } \frac { d t } { 1 - t } = - \ln ( 1 - x ) ,
$$

$$
S ( - 1 ) = \operatorname* { l i m } _ { x \to ( - 1 ) ^ { + } } S ( x ) = \operatorname* { l i m } _ { x \to ( - 1 ) ^ { + } } \left[ - \ln ( 1 - x ) \right] = - \ln ( 1 - ( - 1 ) ) ,
$$

故 $S ( x ) = - \ln ( 1 - x ) , x \in [ - 1 , 1 )$

因此， $\sum _ { n = 0 } ^ { \infty } { \frac { 1 } { n + 1 } } x ^ { n } = \sum _ { n = 1 } ^ { \infty } { \frac { 1 } { n } } x ^ { n - 1 }$ 的收敛域也是[-1,1)，且其和函数为

5.计算 $\iiint z ^ { 2 } d \nu$ ，其中Ω是由曲面 $z = x ^ { 2 } + y ^ { 2 }$ 与 $z = \sqrt { x ^ { 2 } + y ^ { 2 } }$ 围成的有界区域.

## 【宝哥解答】

曲面 $z = x ^ { 2 } + y ^ { 2 }$ 与 $z = \sqrt { x ^ { 2 } + y ^ { 2 } }$ 的交线为 $\left\{ { \begin{array} { l } { x ^ { 2 } + y ^ { 2 } = 1 } \\ { z = 1 } \end{array} } \right.$ ，因此，

$$
\iiint z ^ { 2 } d \nu = \int _ { 0 } ^ { 1 } z ^ { 2 } d z \iint \_ d x d y = \pi \int _ { 0 } ^ { 1 } z ^ { 2 } ( z - z ^ { 2 } ) d z = \frac { \sqrt { 2 } } { 2 0 }
$$

## 三.综合题（本大题共3题，每题10分，本大题共30分）

1.设f(0）=0，f(0)存在， $g ( x ) = \left\{ { \frac { f ( x ) } { x } } , x \neq 0 \right.$ ，求 $g ^ { \prime } ( 0 )$

## 【宝哥解答】

f（0）=0, $f ^ { \prime \prime } ( 0 )$ 存在， $g ( x ) = \left\{ { \frac { f ( x ) } { x } } , x \neq 0 \right.$ ，故

$$
g ^ { \prime } ( 0 ) = \operatorname* { l i m } _ { x \to 0 } { \frac { g ( x ) - \underline { { g } } ( 0 ) } { x } } = \operatorname* { l i m } _ { x \to 0 } { \frac { { \underline { { f } } } ( x ) } { x } } - { \underline { { f ^ { \prime } ( 0 ) } } } = \operatorname* { l i m } _ { x \to 0 } { \frac { f ( x ) - f ^ { \prime } ( 0 ) x } { x ^ { 2 } } } = \operatorname* { l i m } _ { x \to 0 } { \frac { f ^ { \prime } ( x ) - f ^ { \prime } ( 0 ) } { 2 x } } = { \frac { f ^ { \prime \prime } ( 0 ) } { 2 } }
$$

2.讨论函数项级数 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x + n } { n ^ { 2 } } }$ 在 $( - \infty , + \infty )$ 上的一致收敛性和绝对收敛性.【宝哥解答】 研考

$$
( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x + n } { n ^ { 2 } } } = ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x } { n ^ { 2 } } } + ( - 1 ) ^ { n } { \frac { 1 } { n } } ,
$$

$$
\left| ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x } { n ^ { 2 } } } \right| \leq { \frac { 1 } { n ^ { 2 } } } ,
$$

$\sum _ { n = 1 } ^ { \infty } \frac { 1 } { n ^ { 2 } }$ 收敛，故 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x } { n ^ { 2 } } }$ 在 $( - \infty , + \infty )$ 上一致收敛. $\left\{ { \frac { 1 } { n } } \right\}$ 单调递减趋于0由莱布尼兹判别法，数项级数 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { 1 } { n } }$ 也是收敛的因此，函数项级数$\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x + n } { n ^ { 2 } } }$ 在 $( - \infty , + \infty )$ 上一致收敛

又对任意 $x \in ( - \infty , + \infty )$ $\{ ( - 1 ) ^ { n } \frac { \sin ^ { 2 } x + n } { n ^ { 2 } } | - \frac { 1 } { n } , n  \infty , \quad \sum _ { n = 1 } ^ { \infty } \frac { 1 } { n }$ 发散，故$\sum _ { n = 1 } ^ { \infty } \left| ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x + n } { n ^ { 2 } } } \right|$ 发散，故 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x + n } { n ^ { 2 } } }$ 在 $( - \infty , + \infty )$ 上处处不绝对收敛3.计算面积分 $\int \limits _ { \Sigma } \int \int x ^ { 2 } d y d z + y ^ { 2 } d z d x + z ( 1 - 2 x - 2 y ) d x d y$ 其中为上半球面研考$x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = 1 , z \geq 0$ 的上侧

【宝哥解答】

记 $\Sigma _ { 1 }$ 为 $\left\{ x ^ { 2 } + y ^ { 2 } \leq 1 \right.$ 取下侧，Ω为 $\Sigma , \Sigma _ { 1 }$ 围成的立体，则 $\int \int x ^ { 2 } d y d z + y ^ { 2 } d z d x + z ( 1 - 2 x - 2 y ) d x d y = 0$

由Gauss公式，

$$
\begin{array} { l } { \displaystyle \frac { \sqrt { x ^ { 2 } + y ^ { 2 } + z } } { \int \int x } d x d x + z ( 1 - 2 x - 2 y ) d x d y = ( \smallint \iint - \iint ) x ^ { 2 } d y d z + y ^ { 2 } d z d x + z ( 1 - 2 x - 2 y ) d x d y } \\ { \displaystyle \quad \frac { \int } { \Sigma } } \\ { = \displaystyle \iint \left. \frac { \hat { \Omega } x ^ { 2 } } { \partial x } + \frac { \hat { \partial } y ^ { 2 } } { \partial y } + \frac { \hat { \partial } \left[ z ( 1 - 2 x - 2 y ) \right] } { \hat { \partial } z } \right. d x d y d z = \allowbreak \iint _ { \Omega } ( 2 x + 2 y + 1 - 2 x - 2 y ) d x d y d z } \\ { = \displaystyle \iint \displaystyle \iint d x d y d z = \frac { 2 } { 3 } \pi } \end{array}
$$

## 四.证明题(本大题共5题，每题10分，本大题共50分) 四.证明题（本大题共5题，每题10分，本人起六

1.设函数f（x）在 $( 0 , + \infty )$ 上满足 $f ( x ) = f ( 3 x )$ 且 $\operatorname* { l i m } _ { x \to + \infty } f ( x ) = 5$ .证明在 $( 0 , + \infty )$ 上 $f ( x ) \equiv 5 .$

## 【宝哥解答】

函数f（x）在（0,+∞0）上满足 $f ( x ) = f ( 3 x )$ $\operatorname* { l i m } _ { x \to + \infty } f ( x ) = 5$ 任取 $x \in ( 0 , + \infty )$ 有 $f ( x ) = f ( 3 x ) = f ( 3 ^ { 2 } x ) = \cdots = f ( 3 ^ { n } x )$ $\operatorname* { l i m } _ { n \to \infty } ( 3 ^ { n } x ) = + \infty$ 故 $\operatorname* { l i m } _ { n \to \infty } f ( 3 ^ { n } x ) = 5$ ，故$f ( x ) = \operatorname* { l i m } _ { n \to \infty } f ( 3 ^ { n } x ) = 5$ 由x的任意性，在 $( 0 , + \infty ) [ f ( x ) \equiv 5$

$f ( x , y ) = \left\{ { \begin{array} { l } { \displaystyle { \frac { x ( x ^ { 2 } + y ^ { 2 } ) } { x ^ { 2 } + y ^ { 4 } } } , ( x , y ) \not = ( 0 , 0 ) } \\ { \displaystyle { 0 , \dots \to \infty } } \end{array} } \right.$ 2.证明：2.设

(1) $\operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } f ( x , \tilde { y } )$ 不存在； （2) $f _ { x } ^ { \prime } ( 0 , 0 )$ 和f(0,0）存在.

## 【宝哥解答】

$$
\operatorname* { l i m } _ { \stackrel { ( x , y )  ( 0 , 0 ) } { x = 0 } } f ( x , y ) = 0 , \quad \operatorname* { l i m } _ { \stackrel { ( x , y )  ( 0 , 0 ) } { x = y ^ { 2 } } } f ( x , y ) = \operatorname* { l i m } _ { y  0 } \frac { y ^ { 2 } ( y ^ { 4 } + y ^ { 2 } ) } { y ^ { 4 } + y ^ { 4 } } = \frac { 1 } { 2 } \stackrel {  } { 5 }
$$

$\operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } f ( x , y ) \neq \operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } f ( x , y )$ ，故limf不存在. (x,y)→（0,0）

（x+0²）(2) $\operatorname* { l i m } _ { x \to 0 } { \frac { f ( x , 0 ) - f ( 0 , 0 ) } { x } } { \frac { \underset { x \to 0 } { \overset { \underset { x ( x , 1 ) } { \ldots } } { \prod } } - 1 } { x } } = 1 , \operatorname* { l i m } _ { y \to 0 } { \frac { f ( 0 , y ) - f ( 0 , 0 ) } { y } } = \operatorname* { l i m } _ { y \to 0 } { \frac { 0 - 0 } { y } } = 0$

故 $f _ { x } ^ { \prime } ( 0 , 0 )$ 和 $f _ { y } ^ { \prime } ( 0 , 0 )$ 存在，且值分别为1,0.

3.设连续函数列 $\{ f _ { n } ( x ) \}$ 在闭区间 $\textstyle { \left[ a , b \right] }$ 上一致收敛于f(x).若 $\boldsymbol { x } _ { n } \in \left[ a , b \right]$ $( n = 1 , 2 , \cdots )$ 且有 $\operatorname* { l i m } _ { n \to \infty } x _ { n } = x _ { 0 }$ ，证明 $\operatorname* { l i m } _ { n \to \infty } f _ { n } ( x _ { n } ) = f ( x _ { 0 } )$

## 【宝哥解答】

连续函数列 $\left\{ f _ { r } ( x ) \right\}$ 在闭区间[a,b]上一致收敛于f(x)，故f(x)也是连续的.$\left\{ f _ { n } ( x ) \right\}$ 在[a,b]上一致收敛于f(x)，故对任意 $\varepsilon > 0$ ，存在 $N > 0$ ，使得对任意 $n > N$ 和 $x \in \left[ a , b \right]$ ，恒有 $| f _ { n } ( x ) - f ( x ) | < \frac { 1 } { 2 } \varepsilon$ .数列 $\{ x _ { n } \} \subset [ a , b ]$ $\operatorname* { l i m } _ { n \to \infty } x _ { n } = x _ { 0 }$ 故 $\left| f _ { n } ( x _ { n } ) - f ( x _ { n } ) \right| < { \frac { 1 } { 2 } } \varepsilon _ { \ast }$ 故

$$
| f _ { n } ( x _ { n } ) { \overset {  } { \operatorname { \circleddash } } } f ( x _ { 0 } ) | \leq | f _ { n } ( x _ { n } ) - f ( x _ { n } ) | + | f ( x _ { n } ) - f ( x _ { 0 } ) | < { \frac { 1 } { 2 } } \varepsilon + | f ( x _ { n } ) - f ( x _ { 0 } ) |
$$

f（x）连续， $\operatorname* { l i m } _ { n \to \infty } x _ { n } = x _ { 0 }$ ，故 $\operatorname* { l i m } _ { n \to \infty } \left[ f ( x _ { n } ) - f ( x _ { 0 } ) \right] = 0$ ，故存在 $N _ { 1 } > N$ ，使得对任意$n > N _ { 1 }$ ，恒有 $\left| f ( x _ { n } ) - f ( x _ { 0 } ) \right| < { \frac { 1 } { 2 } } \varepsilon$ ，故

$$
\left| f _ { n } ( x _ { n } ) - f ( x _ { 0 } ) \right| < { \frac { 1 } { 2 } } \varepsilon + { \frac { 1 } { 2 } } \varepsilon = \varepsilon
$$

故 $\operatorname* { l i m } _ { n \to \infty } f _ { n } ( x _ { n } ) = f ( x _ { 0 } )$

4.设f（x，y）与 $\varphi ( x , y )$ 均在 $( x _ { 0 } , y _ { 0 } )$ 点某邻域内可微，且 $\varphi _ { \nu } ^ { \prime } ( x , y ) \neq 0$ 已知 $( x _ { 0 } , y _ { 0 } )$ 是f（x，y）在约束条件 $\varphi ( x , y ) = 0$ 下的一个极值点.试证当 $f _ { x } ^ { ^ { \prime } } ( x _ { 0 } , y _ { 0 } ) \neq 0$ 时必有$\mathcal { f } _ { \nu } ^ { ^ { \prime } } ( x _ { 0 } , y _ { 0 } ) \not = 0$ 宝哥

## 【宝哥解答】

f（x，y）与 $\varphi ( x , y )$ 均在 $( x _ { 0 } , y _ { 0 } )$ 点某邻域内可微，且 $\varphi _ { y } ^ { \prime } ( x , y ) \neq 0 _ { \ast } ( x _ { 0 } , y _ { 0 } )$ 是 $f ( x , y )$ 在约束条件 $\varphi ( x , y ) = 0$ 下的一个极值点.令

$$
L ( x , y , \lambda ) = f ( x , y ) + \lambda { \widehat { \cal \varphi } } ( x _ { 3 } y ) ,
$$

则存在，使得

$$
\left\{ \begin{array} { l l } { L _ { x } ( x _ { 0 } , y _ { 0 } , \overline { { \lambda ) } } = \overline { { f _ { x } } } ( x _ { 0 } , y _ { 0 } ) + \lambda \varphi _ { x } ( x _ { 0 } , y _ { 0 } ) = 0 } \\ { \overline { { \lambda ( \overline { { \chi \backslash } } _ { 0 } , y _ { 0 } , \overline { { \lambda } } ) } } = f _ { y } ( x _ { 0 } , y _ { 0 } ) + \lambda \varphi _ { y } ( x _ { 0 } , y _ { 0 } ) = 0 } \end{array} \right.
$$

$f _ { x } ^ { ^ { \prime } } ( x _ { 0 } , y _ { 0 } ) \neq 0$ ，故 $\lambda \varphi _ { x } ( x _ { 0 } , y _ { 0 } ) = - f _ { x } ^ { \prime } ( x _ { 0 } , y _ { 0 } ) \neq 0$ ，故 $\lambda \neq 0$ 又 $\varphi _ { y } ^ { \prime } ( x , y ) \neq 0$ 故 $\varphi _ { \nu } ( x _ { 0 } , y _ { 0 } ) \neq 0$ ，故 $f _ { y } ( x _ { 0 } , y _ { 0 } ) = - \lambda \varphi _ { y } ( x _ { 0 } , y _ { 0 } ) \not = 0$ 因此， $\mathcal { f } _ { y } ^ { ' } ( x _ { 0 } , y _ { 0 } ) \neq 0$ $F ( x ) = \int _ { 0 } ^ { + \infty } \frac { \sin { x t } } { 1 + t ^ { 2 } } d t$ 在 $[ 0 , + \infty )$ 上连续，并且在 $( 0 , + \infty )$ 上有连续5.证明函数

的导函数.

## 【宝哥解答】 【玉可日

$\int _ { 0 } ^ { + \infty } \frac { 1 } { 1 + t ^ { 2 } } d t$ 收敛，故 $\int _ { 0 } ^ { + \infty } \frac { \sin { x t } } { 1 + t ^ { 2 } } d t$ $\left| { \frac { \sin x t } { 1 + t ^ { 2 } } } \right| \leq { \frac { 1 } { 1 + t ^ { 2 } } } , \forall ( t , x ) \in \left[ 0 , + \infty \right) \times \left[ 0 , + \infty \right) \quad$ 在 $[ 0 , + \infty )$ 上一致收敛.又 $\frac { \sin { x t } } { 1 + t ^ { 2 } }$ 是 $( t , x ) \in \lbrack 0 , + \infty ) \times \lbrack 0 , + \infty )$ 的连续函数，故函数 $F ( x ) = \int _ { 0 } ^ { + \infty } \frac { \sin { x t } } { 1 + t ^ { 2 } } d t$ 在 $[ 0 , + \infty )$ 上连续.

$\int _ { 0 } ^ { + \infty } \frac { \partial } { \partial x } ( \frac { \sin \lambda t } { 1 7 + t ^ { 2 } } ) d t = \int _ { 0 } ^ { + \infty } \frac { t } { 1 + t ^ { 2 } } \cos x t d t$ ，任取 $\delta > 0$ 和 $x \in \left[ \delta , + \infty \right)$ ，对任意A,B∈R, $\left| \int _ { A } ^ { B } \cos x t d t \right| \leq \frac { 2 } { x } \leq \frac { 2 } { \delta } , \frac { t } { 1 + t ^ { 2 } }$ 在 $[ 1 , + \infty )$ 上单调递减，且 $\operatorname* { l i m } _ { t \to + \infty } \frac { t } { 1 + t ^ { 2 } } = 0$ 由狄利克雷判别法， $\int _ { 0 } ^ { + \infty } \frac { t } { 1 + t ^ { 2 } } \cos { x t d t }$ 在 $\left[ \delta , + \infty \right)$ 上一致收敛，故

$$
F ^ { \prime } ( x ) = \int _ { 0 } ^ { + \infty } \frac { t } { 1 + t ^ { 2 } } { \cos { x t d t } } , x \in \left[ \delta , + \infty \right) ,
$$

又注意到 $\frac { t } { { 1 + t } ^ { 2 } } { \cos { x t } }$ 为 $( t , x ) \in \left[ 0 , + \infty \right) \times \left[ \delta , + \infty \right)$ 的连续函数，故 $F ^ { \prime } ( x )$ 在 $[ \delta , + \infty )$ 上连续.由δ的任意性，F(x)在 $( 0 , + \infty )$ 上连续，故F（x）在 $( 0 , + \infty )$ 上有连续的导函数.

## developer · 2026-10-19T07:28:04Z

This is an incremental tools update. Previously declared tools remain available for direct calls unless explicitly marked unavailable. If a tool is redefined here, its latest definition replaces the earlier one.

## developer · 2026-10-19T07:28:04Z

<tools>
Added deferred tool namespaces:
- mcp__code_review
</tools>

## tool · 2026-10-19T07:28:09Z


Script completed
Wall time 0.1 seconds
Output:

# 杭州电子科技大学

# 2018年攻读硕士学位研究生招生考试

# 《数学分析》试题

（试题共四大题，共2页，总分150分）

姓名 报考专业 准考证号

【所有答案必须写在答题纸上，做在试卷或草稿纸上无效！】

## 一、填空题（本大题共8小题，每小题5分，本大题共40分）

1. $\operatorname* { l i m } _ { n  \infty } ( 2 ^ { n } + 3 ^ { n } + 4 ^ { n } ) ^ { \frac { 1 } { n } } = ($ ）.

2.设函数f(x)在x=1处可导，f(1)=3,则 $\operatorname* { l i m } _ { x \to 0 } { \frac { f ( 1 + x ) - f ( 1 - 3 x ) } { x } } = ($ ）.

3.已知 $e ^ { x + y } = \sin ( x y )$ 确定了隐函数y=y(x)，则 ${ \frac { d y } { d x } } = { }$ （ ）.

4.设 $F ( x ) = \int _ { 0 } ^ { 2 x } x e ^ { t ^ { 2 } } d t$ ，则F'(x)=（ ）.

5.设 $u = x ^ { 2 } + y - z ^ { 2 }$ ，则u在(1,-1,1)处的方向导数的最大值为（ ）

6．已知(x+ay)dx+(2x+y)dy为某函数的全微分，则a的值是（ ）

7．设函数f(x,y)连续，则二次积分 $\int _ { - 2 } ^ { 0 } d x \int _ { 2 x + 4 } ^ { 4 - x ^ { 2 } } f ( x , y ) d y$ 可交换积分次序为（ ）

8.设M $: x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = 1$ ，则曲面积分 $\iiint _ { \Sigma } ( 2 - x ^ { 2 } - y ^ { 2 } - z ^ { 2 } ) d S = ($

## 二、计算题（本大题共5小题，每小题6分，本大题共30分）

1．求极限值 $\operatorname* { l i m } _ { x \to \infty } { \frac { x ^ { 3 } ( 1 - \cos { \frac { 1 } { x ^ { 2 } } } ) } { \sqrt { x ^ { 2 } + 1 } - x } }$

2.设 $u = u ( x , y ) , \nu = \nu ( x , y )$ 是由 $\left\{ \begin{array} { l l } { \sin ( u + v ) = x y } \\ { e ^ { w } = 1 - x - y } \end{array} \right.$ 所确定的隐函数组，求 $\frac { \hat { \alpha } u } { \hat { \alpha } x }$

3.已知连续函数f(x)满足条件 $\int _ { 0 } ^ { x } t f ( x - t ) d t = 1 - \cos x$ ，求 $\int _ { 0 } ^ { \frac { \pi } { 2 } } f ( x ) d x$

4.求 $\scriptstyle \sum _ { n = 0 } ^ { \infty } { \frac { 1 } { n + 1 } } x ^ { n }$ 的和函数.

5.计算 $\iiint z ^ { 2 } d \nu$ ，其中是由曲面 $z = x ^ { 2 } + y ^ { 2 }$ 与 $z = \sqrt { x ^ { 2 } + y ^ { 2 } }$ 围成的有界区域.

## 三、综合题（本大题共3题，每题10分，本大题共30分）

1.设f(0)=0，f"(0)存在， $g ( x ) = \left\{ { \begin{array} { l l } { { f ( x ) } } & { { x \not = 0 } } \\ { { x } } & { { } } \\ { { f ^ { \prime } ( 0 ) , } } & { { x = 0 } } \end{array} } \right.$ .求 $g ^ { \prime } ( 0 )$

2．讨论函数项级数 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n } { \frac { \sin ^ { 2 } x + n } { n ^ { 2 } } }$ 在 $( - \infty , + \infty )$ 上的一致收敛性和绝对收敛性.

3．计算面积分 $\iint _ { \Sigma } { x ^ { 2 } d y d z } + { y ^ { 2 } d x d z } + z ( 1 - 2 x - 2 y ) d x d y$ ，其中£为上半球面$x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = 1$ $z \geq 0$ 的上侧.

## 四、证明题（本大题共5题，每题10分，本大题共50分）

1.设函数f(x)在(0,+∞)上满足f(x)=f(3x)且 $\operatorname* { l i m } _ { x \to \infty } f ( x ) = 5$ ．证明在 $( 0 , + \infty )$ 上$f ( x ) \equiv 5$

2.设 $f ( x , y ) = \left\{ \begin{array} { c c } { { x ( x ^ { 2 } + y ^ { 2 } ) } } & { { ( x , y ) \neq ( 0 , 0 ) } } \\ { { x ^ { 2 } + y ^ { 4 } } } & { { ( x , y ) = ( 0 , 0 ) } } \end{array} \right.$ ，证明：

(1） $\operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } f ( x , y )$ 不存在；（2）f(0,0)和 $f _ { y } ^ { \prime } ( 0 , 0 )$ 存在.

3．设连续函数列 $\{ f _ { n } ( x ) \}$ 在闭区间[a,b]上一致收敛于f(x)．若 $x _ { n } \in [ a , b ]$ $( n = 1 , 2 , 3 , \cdots )$ 且有 $\operatorname* { l i m } _ { n \to \infty } x _ { n } = x _ { 0 }$ ．证明 $\operatorname* { l i m } _ { n \to \infty } f _ { n } ( x _ { n } ) = f ( x _ { 0 } )$

4.设f(x,y）与 $\varphi ( x , y )$ 均在 $( x _ { 0 } , y _ { 0 } )$ 点某邻域内可微，且 $\varphi _ { y } ^ { \prime } ( x , y ) \neq 0$ ，已知$( x _ { 0 } , y _ { 0 } )$ 是f(x,y）在约束条件 $\varphi ( x , y ) = 0$ 下的一个极值点．试证当$f _ { x } ^ { \prime } ( x _ { 0 } , y _ { 0 } ) \neq 0$ 时必有 $f _ { y } ^ { \prime } ( x _ { 0 } , y _ { 0 } ) \neq 0$

5．证明函数 $F ( x ) = \int _ { 0 } ^ { + \infty } \frac { \sin { x t } } { 1 + t ^ { 2 } } d t$ 在 $[ 0 , + \infty )$ 上连续，并且在(0,+∞)上有连续的导函数.# 杭州电子科技大学2019年数学分析真题解析

## 一.填空题（本大蔬英6小题，每小题5分，本大题共40分）

1.极限 $\operatorname* { l i m } _ { n \to \infty } ( { \frac { 1 } { n + { \sqrt { 1 } } } } + { \frac { 1 } { n + { \sqrt { 2 } } } } + \cdots + { \frac { 1 } { n + { \sqrt { n } } } } ) = ($

【宝哥解答】

$$
\frac { 1 } { n + \sqrt { 1 } } + \frac { 1 } { n + \sqrt { 2 } } + \cdots + \frac { 1 } { n + \sqrt { n } } \leq \frac { n } { n + \sqrt { 1 } }  1 , n  \infty ,
$$

$$
{ \frac { 1 } { n + { \sqrt { 1 } } } } + { \frac { 1 } { n + { \sqrt { 2 } } } } + \cdots + { \frac { 1 } { n + { \sqrt { n } } } } \geq { \frac { n } { n + { \sqrt { n } } } } \to 1 , n \to \infty ,
$$

故將 $\operatorname* { l i m } _ { n \to \infty } ( { \frac { 1 } { n + { \sqrt { 1 } } } } + { \frac { 1 } { n + { \sqrt { 2 } } } } + \cdots + { \frac { 1 } { n + { \sqrt { n } } } } ) = 1$

2.设g(0)=g'（0）=0, $f ( x ) = { \left\{ \begin{array} { l l } { g ( x ) \sin { \frac { 1 } { x } } , x \neq 0 } \\ { ~ } \\ { 0 , ~ } \end{array} \right. } x = 0$ 则f'（0）=(

## 【宝哥解答】

$g ( 0 ) = g ^ { \prime } ( 0 ) = 0$ 故 $\operatorname* { l i m } _ { x \to 0 } { \frac { g ( x ) } { x } } = \operatorname* { l i m } _ { x \to 0 } { \frac { g ( x ) - g ( 0 ) } { x } } = g ^ { \prime } ( 0 ) = 0$ ，故

$$
f ^ { \prime } ( 0 ) = \operatorname* { l i m } _ { x \to 0 } { \frac { f ( x ) - f ( 0 ) } { x } } = \operatorname* { l i m } _ { x \to 0 } { \frac { g ( x ) } { x } } \sin { \frac { 1 } { x } } = 0 \ .
$$

这里， $\operatorname* { l i m } _ { x \to 0 } { \frac { g ( x ) } { x } } = 0 , \left| \sin { \frac { 1 } { x } } \right| \leq 1$ $\operatorname* { l i m } _ { x \to 0 } { \frac { g ( x ) } { x } } \sin { \frac { 1 } { x } } = 0 ,$

3.曲线 $L : \left\{ { \begin{array} { l } { x = 1 - t ^ { 2 } } \\ { y = t - t ^ { 2 } } \end{array} } \right.$ 在t=1所对应的法线方程为（

## 【宝哥解答】

$t \neq 0$ 时 $\frac { d y } { d x } = \frac { \displaystyle \frac { d y } { d t } } { \displaystyle \frac { d x } { d t } } = \frac { 1 - 2 t } { - 2 t } = 1 - \frac { 1 } { 2 t } \ , \frac { d y } { d x } \big | _ { t = 1 } = 1 - \frac { 1 } { 2 } = \frac { 1 } { 2 } . t = 1$ 时 ， $x = 0$

$L : \left\{ \begin{array} { l l } { x = 1 - t ^ { 2 } } \\ { y = t - t ^ { 2 } } \end{array} \right.$ 在t=1所对应的法线方程为 $y = - 2 x$ $y = 0$ 故曲线

宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线：15160699421或 15659067618

4.曲线 $y = x ^ { 4 } - 6 x ^ { 3 } + 1 2 x ^ { 2 } - x + 1$ 的拐点有（

【宝哥解答】

$$
y ^ { \prime \prime } ( x ) = 1 2 x ^ { 2 } - 3 6 x + 2 4 = 1 2 ( x - 1 ) ( x - 2 ) ,
$$

$x < 1$ 时，y(x)>0， $1 < x < 2$ 时 $y ^ { \prime } ( x ) < 0 , x > 2$ 小 $y ^ { \prime \prime } ( x ) > 0$ 故 曲线 $y = x ^ { 4 } - 6 x ^ { 3 } + 1 2 x ^ { 2 } - x + 1$ 的拐点有(1,y(1))=(1,7)和(2,y(2))(5).

$$
2 f ( x ) + x = 1 + \int _ { 0 } ^ { 1 } f ( x ) d x
$$

$$
\int \limits _ { 0 } ^ { 1 } f ( x ) d x = 1
$$

$$
2 f ( x ) + x = 1 + \int _ { 0 } ^ { 1 } f ( x ) d x
$$

$$
2 \int _ { 0 } ^ { 1 } f ( x ) d x + \int _ { 0 } ^ { 1 } x d x = 1 + \int _ { 0 } ^ { 1 } f ( x ) d x \ ,
$$

$$
\int _ { 0 } ^ { 1 } f ( x ) d x = 1 - \int _ { 0 } ^ { 1 } x d x = 1 - { \frac { 1 } { 2 } } = { \frac { 1 } { 2 } }
$$

$$
F ( y ) = \int _ { \nu } ^ { \nu ^ { 2 } } \frac { \sin ( x y ) } { x } d x ,
$$

$$
F ^ { \prime } ( y ) = (
$$

【宝哥解答】

$$
E ( y ) = \int _ { y } ^ { y ^ { 2 } } { \frac { \sin ( x y ) } { x } } d x = \int _ { y ^ { 2 } } ^ { y ^ { 3 } } { \frac { \sin ( u ) } { u } } d u \ ,
$$

$$
F ^ { \prime } ( y ) = { \frac { \sin ( y ^ { 3 } ) } { y ^ { 3 } } } 3 y ^ { 2 } - { \frac { \sin ( y ^ { 2 } ) } { y ^ { 2 } } } 2 y = { \frac { 3 \sin ( y ^ { 3 } ) - 2 \sin ( y ^ { 2 } ) } { \nu } }
$$

$$
f ( x , y )
$$

$$
\int _ { 1 } ^ { e ^ { - } } d y \int _ { \ln y ^ { 2 } } ^ { 2 } f ( x , y ) d x
$$

【宝哥解答】积分区域如下图所示：

<!-- image-->

故

$$
\mathcal { f } ( x , y ) d x = \int _ { 0 } ^ { 2 } d x \int _ { 1 } ^ { e ^ { x } } f ( x , y ) d y
$$

8.若L为圆周 $\left\{ { \begin{array} { l } { x ^ { 2 } + { \bar { y } } ^ { 2 } + z ^ { 2 } = a ^ { 2 } } \\ { x + y + z = 0 } \end{array} } \right.$ ，则曲线积分 $\int _ { L } { ( 2 x ^ { 2 } + y ^ { 2 } + 2 x + y + 1 ) d s } = ($

## 【宝哥解答】

L为圆周 $\left\{ { \begin{array} { l } { x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = a ^ { 2 } } \\ { x + y + z = 0 } \end{array} } \right.$ ，其关于平面 $x = y , x = z , y$ 都是对称的，其弧长为2πa.由轮换对称性，有

$$
\int _ { L } { x ^ { 2 } d s } = \int _ { L } { y ^ { 2 } d s } = \int _ { L } { z ^ { 2 } d s } = { \frac { 1 } { 3 } } \int _ { L }  
$$

$$
^ { 2 } ) d s = \frac { 1 } { 3 } \int _ { L } a ^ { 2 } d s = \frac { 1 } { 3 } a ^ { 2 } \cdot 2 \pi a = \frac { 2 } { 3 } \pi a ^ { 3 }
$$

$$
\int _ { L } x d s = \int _ { \log 2 } y d s = \int _ { L } z d s = \frac { 1 } { 3 } \int _ { L } ( x + y + z ) d s = \frac { 1 } { 3 } \int _ { L } 0 d s = 0 \ ,
$$

故

$$
\int _ { L } ( 2 x ^ { 2 } + y ^ { 2 } + 2 x + y + 1 ) d s = 3 \times \frac { 2 } { 3 } \pi a ^ { 3 } + 2 \pi a = 2 \pi a ^ { 3 } + 2 \pi a
$$

## 二.计算题（本大题共5小题，每小题6分，本大题共30分)

1.求极限值 $\operatorname* { l i m } _ { x  0 ^ { + } } ( \frac { \sin x } { x } ) ^ { \frac { 1 } { x ^ { 2 } } }$

【宝哥解答】 3Xsinx-x=lim 6limsin x lim( sin x →0 3 x→0 xx→0x→0 X  
故 $\operatorname* { l i m } _ { x \to 0 } ( { \frac { \sin x } { x } } ) ^ { \frac { 1 } { x ^ { 2 } } } = e ^ { - { \frac { 1 } { 6 } } } .$

$$
y = - y e ^ { x } + 2 e ^ { y } \sin x + 2 x
$$

$$
y ^ { \prime } ( 0 )
$$

【宝哥解答】

令x=0，可得y=0.

令 $F ( x , y ) = y + y e ^ { x } - 2 e ^ { y } \sin x - 2 x$ ，则

$$
F _ { x } ( x , y ) = y e ^ { x } - 2 e ^ { y } \cos x - 2 , F _ { y } ( x , y ) = 1 + e ^ { x } - 2 e ^ { y } \sin x
$$

由隐函数存在定理的结论，有

$$
y ^ { \prime } ( 0 ) = - \frac { F _ { x } ( 0 , 0 ) } { F _ { y } ( 0 , 0 ) } = - \frac { - 4 } { 2 } = 2
$$

3.设 $f ( x ) = \left\{ { x { e ^ { - x ^ { 2 } } } , x \geq 0 } \right.$ ，求 $\int _ { 1 } ^ { x } f ( u - 1 ) d u$ 的表达式.

## 【宝哥解答】

$$
f ( x ) = \left\{ \begin{array} { l l } { x e ^ { - x ^ { 2 } } , x \geq 0 } \\ { 0 , } & { x < 0 } \end{array} \right. , \ \pm \pmb { \mathscr { X } }
$$

$$
\int _ { 1 } ^ { x } f ( u - 1 ) d u \stackrel { \mathrm { \tiny ~ \ast ~ \ast ~ } } { = } \int _ { 0 } ^ { x + \sum _ { j = 1 } ^ { m } } \langle u \rangle d u = \left\{ \int _ { 0 } ^ { x - 1 } u e ^ { - u ^ { 2 } } d u = - \frac { 1 } { 2 } e ^ { - u ^ { 2 } } \left| 0 \right. \right. = - \frac { 1 - e ^ { - ( x - 1 ) ^ { 2 } } } { 2 } , x \ge 1
$$

4.求级数 $\sum _ { n = 1 } ^ { \infty } n { \frac { 2 ^ { \frac { n } { 2 } } } { 3 ^ { n } } }$ 的和

幂级数 $\sum _ { n = 1 } ^ { \infty } n x ^ { n }$ 的收敛半径为 $\operatorname* { l i m } _ { n \to \infty } { \frac { n } { n + 1 } } = 1$ ，且其在x=±1处通项都是无穷 大量，故其在x=±1处发散，故幂级数的收敛域为(-1,1).

在(-1,1)内，

$$
\sum _ { n = 1 } ^ { \infty } n x ^ { n } = x \sum _ { n = 1 } ^ { \infty } n x ^ { n } = x \sum _ { n = 1 } ^ { \infty } { \binom { x ^ { n } } { n } } ^ { \infty } = x \sum _ { n = 1 } ^ { \infty } { \binom { x ^ { n } } { n } } ^ { \prime } = x { \binom { \infty } { n = 1 } } ^ { \prime } = x { \binom { \infty } { n = 0 } } ^ { \prime } = x { \binom { 1 } { 1 - x } } ^ { \prime } = { \frac { x } { ( 1 - x ) ^ { 2 } } }
$$

$\frac { \sqrt { 2 } } { 3 } \in ( 0 , 1 )$ ，故

$$
\sum _ { n = 1 } ^ { \infty } n { \frac { 2 ^ { \frac { n } { 2 } } } { 3 ^ { n } } } = \sum _ { n = 1 } ^ { \infty } n ( { \frac { \sqrt { 2 } } { 3 } } ) ^ { n } = { \frac { \frac { \sqrt { 2 } } { 3 } } { ( 1 - { \frac { \sqrt { 2 } } { 3 } } ) ^ { 2 } } } = { \frac { 3 { \sqrt { 2 } } } { ( 3 - { \sqrt { 2 } } ) ^ { 2 } } }
$$

5.计算 $\iint _ { D } ( x + y + 1 ) ^ { 2 } d x d y$ ，其中 $D = \left\{ ( x , y ) \left. 1 \leq x ^ { 2 } + y ^ { 2 } \leq 4 \right. \right\}$

## 【宝哥解答】

一般地，对任意R>0，有

$$
\mathop { \operatorname { a x } } _ { x ^ { 2 } + y ^ { 2 } \leq R ^ { 2 } } ^ { \geq x } ( x ^ { 2 } + y ^ { 2 } ) d x d y = \int _ { 0 } ^ { R } r ^ { 3 } d r \int _ { 0 } ^ { 2 \pi } d \theta = \frac { 1 } { 2 } \pi R ^ { 4 }
$$

积分区域D关于两坐标轴都是对称的，而x，y,xy分别关于x,y,x是奇函数，故 $\int \int _ { D } x d x d y = \int \int _ { D } y d x d y = \int \int _ { D } x y d x d y = 0$ ，故$\iint ( x + y + 1 ) ^ { 2 } d x d y = \iint ( x ^ { 2 } + y ^ { 2 } + 1 + 2 x y + 2 x + 2 y ) \iint ( x ^ { 2 } + y ^ { 2 } + 1 ) d x d y$ =f (x²+y²）dxdy-（x²+d+π=π.4- 1²+3πx2²+y2≤4

## 三.综合题（本大题共3题，每题10分，本大题共30分）

1.求a的值，使得 $f ( x , y ) = \left\{ \begin{array} { l } { { ( x ^ { 2 } + y ^ { 2 } ) ^ { a } \cos \displaystyle \frac { \cdot \ : 1 } { \left| x \right| + \left| y \right| } , ( x , y ) \neq ( 0 , 0 ) } } \\ { { 0 , \qquad ( x , y ) = ( 0 , 0 ) } } \end{array} \right.$ 在点（0,0）可微.

## 【宝哥解答】

如果f(x,y）在(0,0)可微，则

$$
\operatorname* { l i m } _ { x \to 0 ^ { + } } { \frac { f ( x , 0 ) - f ( 0 , 0 ) } { x } } = \operatorname* { l i m } _ { x \to 0 ^ { + } } { \frac { ( x ^ { 2 } ) ^ { a } \cos { \frac { 1 } { \left| x \right| } } } { x } } = \operatorname* { l i m } _ { x \to 0 ^ { + } } x ^ { 2 a - 1 } \cos { \frac { 1 } { x } }
$$

存在，于是， $\operatorname * { l i m } _ { n  \infty } ( { \frac { 1 } { n \pi } } ) ^ { 2 a - 1 } \cos { \frac { 1 } { \displaystyle { \frac { 1 } { n \pi } } } } = \operatorname * { l i m } _ { n  \infty } ( n \pi ) ^ { 1 - 2 a } ( - 1 ) ^ { n }$ 存在，即 $1 - 2 a < 0$ ，即 $a > \frac { 1 } { 2 }$

$$
a > \frac { 1 } { 2 }
$$

$$
\operatorname* { l i m } _ { \substack { ( x , y )  ( 0 , 0 ) } } \int _ { x } ^ { \infty } \hat { y } _ {  } ^ { \infty , \theta } = \operatorname* { l i m } _ { \substack { ( x , y )  ( 0 , 0 ) } } \frac { ( x ^ { 2 } + y ^ { 2 } ) ^ { a } \cos \frac { 1 } { | x | + | y | } } { \sqrt { x ^ { 2 } + y ^ { 2 } } } = \operatorname* { l i m } _ { \substack { ( x , y )  ( 0 , 0 ) } } ( x ^ { 2 } + y ^ { 2 } ) ^ { a - \frac { 1 } { 2 } } \cos \frac { 1 } { | x | + | y | }
$$

即 $f ( x , y ) - f ( 0 , 0 ) = 0 \cdot x + 0 \cdot y + o ( \sqrt { x ^ { 2 } + y ^ { 2 } } )$ ，故f（x,y）在点(0,0）可微.

2.讨论级数 $\sum _ { n = 1 } ^ { \infty } { \frac { ( x + 1 ) ^ { n } } { ( n + 1 ) 2 ^ { n } } }$ 的敛散性(何时绝对收敛、何时条件收敛及何时发散).

## 【宝哥解答】

幂级数 $\sum _ { n = 1 } ^ { \infty } { \frac { ( x + 1 ) ^ { n } } { ( n + 1 ) 2 ^ { n } } }$ 的收敛半径为 $\displaystyle \operatorname* { \overline { { \operatorname* { m i n } _ { n  \infty } } } } _ { ( n + 2 ) 2 ^ { n + 1 } } = 2$ ，故其在

内绝对收敛.在x=-3处，幂级数为 $\sum _ { n = 1 } ^ { \infty } { \frac { ( - 1 ) ^ { n } } { n + 1 } }$ ，是条件收敛的，在x=1处，幂级数为 $\sum _ { n = 1 } ^ { \infty } { \frac { 1 } { n + 1 } }$ ，是发散的.

综上所述， $\sum _ { n = 1 } ^ { \infty } { \frac { ( x + 1 ) ^ { n } } { ( n + 1 ) 2 ^ { n } } }$ 在（-3，-1）绝对收敛，在 $( - \infty , - 3 ) \cup [ 1 , + \infty )$ 发散，在x=-3处条件收敛.

3.计算曲线积分 $\int _ { L } { \frac { ( e ^ { x } - 2 \chi y ) d x - ( x ^ { 2 } + y ^ { 2 } ) d y } { ( x - 1 ) ^ { 2 } + y ^ { 2 } } }$ 其中L是在圆周 $y = \sqrt { 2 x - x ^ { 2 } }$ 上由  
点O(0,0)到点A(1,1)的一段弧.  
【宝哥解签】

$$
\begin{array} { l } { { \displaystyle \int _ { L } \frac { ( e ^ { x } - 2 x y ) d x - ( x ^ { 2 } + y ^ { 2 } ) d y } { ( x - 1 ) ^ { 2 } + y ^ { 2 } } = \int _ { L } ( e ^ { x } - 2 x y ) d x - ( x ^ { 2 } + y ^ { 2 } ) d y } \ ~ } \\ { { = \displaystyle \int _ { L } ( d e ^ { x } - y d x ^ { 2 } - x ^ { 2 } d y - d \frac { y ^ { 3 } } { 3 } ) = \int _ { L } d ( e ^ { x } - x ^ { 2 } y - \frac { y ^ { 3 } } { 3 } ) = ( e ^ { x } - x ^ { 2 } y - \frac { y ^ { 3 } } { 3 } ) \Big | ( 1 , 1 ) } } \\ { { = e - \displaystyle \frac { 4 } { 3 } ~ } } \end{array}
$$

## 四.证明题(本大题共5题，每题10分，本大题共50分)

1.设连续函数f（x）在 $[ 1 , + \infty )$ 上为正值，且单调递减，令 $a _ { n } = \sum _ { i = 1 } ^ { n } f ( i ) - \int _ { 1 } ^ { n } f ( x ) d x$ 证明 $\left\{ a _ { n } \right\}$ 收敛.

## 【宝哥解答】

连续函数f（x）在 $[ 1 , + \infty )$ 上为正值，且单调递减，故

$$
\begin{array} { r l } & { a _ { n + 1 } - a _ { n } = \left[ \displaystyle \sum _ { i = 1 } ^ { n + 1 } f ( i ) - \displaystyle \int _ { 1 } ^ { n + 1 } f ( x ) d x \right] - \left[ \displaystyle \sum _ { i = 1 } ^ { n } f ( i ) - \displaystyle \int _ { 1 } ^ { n } f ( x ) d x \right] , } \\ & { = f ( n + 1 ) - \displaystyle \int _ { n } ^ { n + 1 } f ( x ) d x \le \int _ { 1 } ^ { n + 1 } f ( n + 1 ) d x = 0 } \end{array}
$$

即 $a _ { n + 1 } \leq a _ { n } , n = 1 , 2 , \cdots$ ，故单调递减.

$$
\begin{array} { l } { { \displaystyle a _ { n } = \sum _ { i = 1 } ^ { n } f ( i ) - \left\{ \begin{array} { l l } { { \displaystyle \int _ { f ( x ) } ^ { n } \ f ( x ) d x = \sum _ { i = 1 } ^ { n } \int _ { i } ^ { i + 1 } f ( i ) d x - \int _ { 1 } ^ { n } f ( x ) d x \ge \sum _ { i = 1 } ^ { n } \int _ { i } ^ { i + 1 } f ( x ) d x - \int _ { 1 } ^ { n } f ( x ) d x } } \\ { { \displaystyle \phantom { \sum _ { i = 1 } ^ { n } \int _ { f ( x ) } ^ { n } \ f ( x ) d x - \int _ { 1 } ^ { n } f ( x ) d x = \sum _ { i = 1 } ^ { n } f ( x ) d x > 0 } } } \end{array} \right. , } } \\ { { \displaystyle \phantom { \sum _ { i = 1 } ^ { n } \int _ { f ( x ) } ^ { n } \ f ( x ) d x - \int _ { 1 } ^ { n } f ( x ) d x = \sum _ { i = 1 } ^ { n } \int _ { f } ^ { n + 1 } f ( x ) d x > 0 } , } } \end{array}
$$

故 $\left\{ a _ { n } \right\}$ 有下界.因此， $\left\{ a _ { n } \right\}$ 收敛.

2.设函数f（x）在区间[a,b]上二阶可导，曲线y=f（x）与过点A（a,f（a））和点$B ( b , f ( b ) )$ 的直线相交于一点 $C ( c , f ( c ) )$ 其中 $a < c < b$ 试证：（1）至少存在一点 $\xi _ { 1 } \in ( a , c )$ 及一点 $\xi _ { 2 } \in ( c , b )$ ，使得 $( \xi _ { 1 } ) = f ^ { \prime } ( \xi _ { 2 } )$ ；(2)至少存在一点 $\xi \in ( a , b )$ 使得 $f ^ { \prime } ( \xi ) = 0$ 宝哥

## 【宝哥解答】

(1）函数f（x)在区间[a,b]上二阶可导，曲线y=f（x)与过点 $A ( a , f ( a ) )$ 和点$B ( b , f ( b ) )$ 的直线相交于一点 $C ( c , f ( c ) )$ ，其中 $a < c < b$ ，于是，

大学数学分析+高等代数其杭 $\frac { f ( c ) = f ( a ) + \frac { f ( b ) - f ( a ) } { b - a } ( c - a ) = f ( b ) + \frac { f ( b ) - f ( a ) } { b - a } ( c - b ) } { f ( c ) = f ( a ) + \frac { f ( b ) - f ( a ) } { b - a } ( c - a ) = f ( b ) + \frac { f ( b ) - f ( a ) } { b - a } ( c - b ) } , \quad \forall a \in ( 0 , 1 ) , \quad a \in ( 0 , 1 ) , \quad a \in ( 0 , 1 ) , \quad a \in ( 0 , 1 ) .$ $\xi _ { 1 } \in ( a , c )$ 及一点 $\xi _ { 2 } \in ( c , b )$ 得由拉格朗日中值定理，至少存在一点$f ^ { \prime } ( \xi _ { 1 } ) = \frac { f ( c ) - f ( a ) } { c - a } = \frac { f ( a ) + \frac { f ( b ) - f ( a ) } { b - a } ( c ^ { \infty } a ) - f ( a ) } { c - a } = \frac { f ( b ) - f ( a ) } { b - a } ,$ $\begin{array} { l } { \displaystyle { \mathcal { S } ^ { \prime } \hat { \mathbf { \Sigma } } ^ { \prime \prime } } \hat { \mathbf { \Sigma } } ^ { C - a } = \frac { \displaystyle \int _ { 0 } ^ { \infty } f ( \bar { \mathbf { \Sigma } } ) - \left[ f ( b ) + \frac { f ( b ) - f ( a ) } { b - a } ( c - b ) \right] } { \displaystyle f ^ { \prime } ( \xi _ { 2 } ) = \frac { f ( b ) - f ( \bar { \mathbf { \Sigma } } ) } { \displaystyle b - a } = \frac { f ( b ) - f ( a ) } { b - a } } , } \end{array}$ 故 $f ^ { \prime } ( \xi _ { 1 } ) = f ^ { \prime } ( \xi _ { 2 } )$

(2）函数f(x)在区间[a,b]上二阶可导， $\xi _ { 1 } \in ( a , c )$ 和 $\xi _ { 2 } \in ( c , b )$ ，使得 $f ^ { \prime } ( \xi _ { 1 } ) = f ^ { \prime } ( \xi _ { 2 } )$ .由罗尔中值定理，存在 $\xi \in ( \xi _ { 1 } , \xi _ { 2 } ) \subset ( a , b )$ ，使得 $f ^ { \prime } ( \xi ) = 0$ 3.设 $1 < a < b$ .证明函数 $F ( x ) = \int _ { e } ^ { + \infty } { \frac { \mathsf { c o s } t } { t ^ { x } } } d t$ 在[a，b]连续且可微

## 【宝哥解答】

$\left| { \frac { \cos t } { t ^ { x } } } \right| \leq { \frac { 1 } { t ^ { a } } } , \forall ( t , x ) \in \left[ e , + \infty \right) \lesssim \left[ a , \tilde { b } \right] ^ { \prime } ,$ 由于 $a > 1$ ，故 $\int _ { e } ^ { + \infty } \frac { 1 } { t ^ { a } } d t$ 收敛，故 $\int _ { e } ^ { + \infty } \frac { \mathsf { c o s } t } { t ^ { x } } d t$ 在[a,6]上一致收敛又 $\frac { c o s t } { t ^ { x } }$ 是 $( t , x ) \in \left[ e , + \infty \right) \times \left[ a , b \right]$ 的连续函数，故F(x）在 $\textstyle { \left[ a , b \right] }$ 上连续.

$$
\int _ { e } ^ { + \infty } { \frac { \partial } { \partial x } } { \frac { \cos t } { t ^ { x } } } d t = - \int _ { e } ^ { + \infty } { \frac { \cos t \ln t } { t ^ { x } } } d t , \quad \left| { \frac { \cos t \ln t } { t ^ { x } } } \right| \leq { \frac { \ln t } { t ^ { a } } } , \forall ( t , x ) \in \left[ e , + \infty \right) \times \left[ a , b \right]
$$

$a > 1$ ，故 $\int _ { e } ^ { + \infty } \frac { \ln t } { t ^ { a } } d t$ 收敛，故 $\int _ { e } ^ { + \infty } \frac { \cos t \ln t } { t ^ { x } } d t$ 在 $[ a , b ] . 5$ 一致收敛，故

$$
F ^ { \prime } ( x ) = - \int _ { e } ^ { + \infty } \frac { \cos \ell \ln \mathcal { T } } { \mathcal { Z } _ { - \ell } ^ { x } } d t \ : ,
$$

故函数 $F ( x ) = \int _ { e } ^ { + \infty } { \frac { \cos t } { t ^ { x } } } d t$ 在a可连续且可微。

4.设 $\sum _ { n = 1 } ^ { \infty } a _ { n }$ 绝对收敛，证明 $\sum _ { n = 1 } ^ { \infty } a _ { n } ( a _ { 1 } + a _ { 2 } + \cdots + a _ { n } )$ 也绝对收敛.

## 【宝哥解答】

$\sum _ { n = 1 } ^ { \infty } a _ { n }$ 绝对收敛，故 $\sum _ { n = 1 } ^ { \infty } a _ { n }$ 收敛，故其部分和有界，即存在正常数M，使得

对任意正整数n，都有 $\left| a _ { 1 } + a _ { 2 } + \cdots + a _ { n } \right| \leq M$ ，故

$$
\left| a _ { n } ( a _ { 1 } + a _ { 2 } + \cdots + a _ { n } ) \right| \leq M | a _ { n } { \big | } , n = 1 , 2 , \cdots
$$

$\sum _ { n = 1 } ^ { \infty } a _ { n }$ 绝对收敛，故 $\sum _ { n = 1 } ^ { \infty } \left| a _ { n } \right|$ 收敛.由比较判别法， $\sum _ { n = 1 } ^ { \infty } \left| a _ { n } { \big ( } a _ { 1 } + a _ { 2 } + \cdots + a _ { n } { \big ) } \right|$ 收敛.即 $\sum _ { n = 1 } ^ { \infty } a _ { n } ( a _ { 1 } + a _ { 2 } + \cdots + a _ { n } )$ 也绝对收敛.

5.设 $R > 0 ; \Omega$ 为曲面 $z = R ^ { 2 } - x ^ { 2 } - y ^ { 2 }$ 与平面z=0所围成的空间闭区域，Σ为Ω表面的外侧，V为Ω的体积.证明

$$
\iint x ^ { 2 } y e ^ { \sin z } d y d z - x y ^ { 2 } e ^ { \sin z } d z d x + z ( 1 + 2 x y z ) d x d y = V
$$

## 【宝哥解答】

由Gauss公式，

$$
\begin{array} { r l } & { \quad \displaystyle \iint _ { s } ^ { 2 } y e ^ { \sin \alpha } d y d z - x y ^ { 2 } e ^ { \sin \alpha } d z d x + \frac { \sqrt { ( \sqrt { 1 + 3 } ) ^ { 2 } } } { 4 } d x d y } \\ & { = \displaystyle \iint _ { s } ^ { 2 } { \left\{ \frac { \partial \left( x ^ { 2 } y e ^ { \sin \alpha } \right) } { \partial x ^ { 2 } } - \frac { \partial \left( \sqrt { 3 } y e ^ { \sqrt { 2 } } e ^ { \sin \alpha } \right) } { \partial y } + \frac { \partial \left[ z \left( 1 + 2 x y z \right) \right] } { \partial z } \right\} } d x d y d z } \\ & { = \displaystyle \iint _ { s } ^ { 2 } \left\{ \frac { \sqrt { 6 } ( 2 x y ) e ^ { \sin \alpha } - 2 x y e ^ { \sin \alpha } + 1 + 4 x y z ) d x d y d z } { \sin \alpha } \right. } \\ & { = \displaystyle \iint _ { s } ^ { 2 } { \left( 1 + 4 x y z \right) d x d y d z \ = \ \frac { \sqrt { 6 } \mu } { \cos \alpha } \mathrm { d } y d z } = { \smallskip \int _ { s } ^ { \alpha } } d x d y d z = { \smallskip \int _ { s } ^ { \alpha } } } \\ &  = \displaystyle \iint _ { s } ^ { 2 } { \left( \frac { \partial \left( x ^ { 2 } y e ^ { \sin \alpha } \right) } { \partial x } + \frac { \partial \left( x ^ { 2 } y e ^ { \alpha } \right) } { \partial y } + \frac { \partial \left[ z \left( 1 + 2 x y z \right) \right] } { \partial z } \right\} d x d y d z } \end{array}
$$

## tool · 2026-10-19T07:28:19Z


Script completed
Wall time 0.1 seconds
Output:

# 杭州电子科技大学2020年数学分析真题解析

一.填空题（本大题共8小题，每小题5分，共40分)

1 $\operatorname* { l i m } _ { n \to \infty } \left( { \frac { 1 } { n ^ { 2 } + n + 1 } } + { \frac { 2 } { n ^ { 2 } + n + 2 } } + { \frac { 3 } { n ^ { 2 } + n + 3 } } + \cdots + { \frac { n } { n ^ { 2 } + n + n } } \right) = 0$

【宝哥解答】

$$
\leq { \frac { 1 + 2 + 3 + \cdots + n } { n ^ { 2 } + n + 1 } } = { \frac { { \frac { 1 } { 2 } } n ( n + 1 ) } { n ^ { 2 } + n + 1 } }  { \frac { 1 } { 2 } } , n  \infty
$$

$$
\frac { n } { n ^ { 2 } + n + n }
$$

$$
\geq { \frac { 1 + 2 + 3 + \cdots + n } { n ^ { 2 } + n + n } } { \frac { \frac { 1 } { 2 } n ( n + 1 ) } { n ^ { 2 } + 9 + n } }  { \frac { 1 } { 2 } } , n  \infty
$$

$$
\operatorname* { l i m } _ { n \to \infty } \left( { \frac { 1 } { n ^ { 2 } + n + 1 } } + { \frac { 2 ^ { 2 } } { n ^ { 2 } + n + 2 } } + { \frac { 3 } { n ^ { 2 } + n + 3 } } + \cdots + { \frac { n } { n ^ { 2 } + n + n } } \right) = { \frac { 1 } { 2 } } .
$$

2.设 $f ( x ) = \arctan x - { \frac { 1 } { 1 + a x ^ { 2 } } }$ ，且 $f ^ { \prime \prime } ( 0 ) = 2$ ，则a=（ ）

【宝哥解答】

$$
f ^ { \prime } ( x ) = \frac { 1 } { 1 + x ^ { 2 } } + \frac { 2 a x } { ( 1 + a x ^ { 2 } ) ^ { 2 } } ;
$$

$$
( \frac { 1 } { 1 + x ^ { 2 } } ) ^ { \prime } \vert _ { x = 0 } = - \frac { 0 . 2 x ^ { 2 } } { ( 1 + x ^ { 2 } ) ^ { 2 } } \vert _ { x = 0 } = 0 ,
$$

$$
[ \frac { 2 a x } { ( 1 + a x ^ { 2 } ) ^ { 2 } } ] ^ { \prime } | _ { x = 0 } = \operatorname * { l i m } _ { x  0 } \frac { \displaystyle \frac { 2 a x } { ( 1 + a x ^ { 2 } ) ^ { 2 } } } { x } = 2 a ,
$$

故 $2 = f ^ { \eta } ( 0 ) = 0 + 2 a$ ，故a=1.

3.设y=f（x）由方程 $y - \sin ( x y ) = e ^ { x ( 1 - y ) }$ 确定，则 $\operatorname* { l i m } _ { n \to \infty } n \biggl [ f ( \frac { 1 } { n } ) - 1 \biggr ] =$

【宝哥解答】

$y - \sin ( x y ) = e ^ { x ( 1 - y ) }$ ，令 $x = 0$ ，可得 $y = 1$

令 $F ( x , y ) = y - \sin ( x y ) - e ^ { x ( 1 - y ) }$ ，则

$$
F _ { x } ( x , y ) = - y \cos ( x y ) - ( 1 - \jmath ) \hat { e } ^ { x ( 1 - y ) } \oint F _ { y } ( x , y ) = 1 - x \cos ( x y ) + x e ^ { x ( 1 - y ) } ,
$$

都是连续的， $F _ { y } ( 0 , 1 ) = 1 \neq 0$ 由隐函数存在定理的结论，

$$
\frac { d y } { d x } \vert _ { x = 0 } = - \frac { F _ { x } ( x , y ) } { F _ { y } ( x , y ) } \vert _ { x = 0 } = - \frac { - 1 } { 1 } = 1 ,
$$

故

$$
\operatorname* { l i m } _ { n \to \infty } n \Bigg [ f ( \frac { 1 } { n } ) - 1 \Bigg ] = \operatorname* { l i m } _ { n \to \infty } \frac { f ( \frac { 1 } { n } ) - 1 } { 1 } = f ^ { \prime } ( 0 ) = 1
$$

4.曲线 $y = x ^ { 2 } + 2 \ln x$ 在其拐点处的切线方程为（

【宝哥解答】

$$
y ^ { \prime } ( x ) = 2 ^ { 2 } x + \frac { 2 0 } { x } , y ^ { n } ( x ) = 2 - \frac { 2 } { x ^ { 2 } } = \frac { 2 ( x ^ { 2 } - 1 ) } { x ^ { 2 } } ,
$$

$0 < x < 1$ 时， $y ^ { \prime \prime } ( x ) < 0$ ，x>1时， $y ^ { \prime \prime } ( x ) > 0$ ，故 $\left( 1 , y ( 1 ) \right) = \left( 1 , 1 \right)$ 为拐点. $y ^ { \prime } ( 1 ) = 4$

故曲线 $y = x ^ { 2 } + 2 \ln x$ 在其拐点处的切线方程为 $y = 1 + 4 ( x - 1 ) = 4 x - 3$

5.已知 $f ( x ) = \int _ { 1 } ^ { x } { \sqrt { 1 + t ^ { 4 } } } d t$ ，则 $\int _ { 0 } ^ { 1 } x ^ { 2 } f ( x ) d x = ($

【宝哥解答】

$$
\begin{array} { l } { { \displaystyle \int _ { 0 } ^ { 1 } { x ^ { 2 } } f ( x ) d x } = \int _ { 0 } ^ { 1 } { x ^ { 2 } } \int _ { 1 } ^ { x } { \sqrt { 1 + t ^ { 4 } } } d t d \dot { x } \dot { \overline { { { \varphi } _ { 2 } } } } - \int _ { 0 } ^ { 1 } { x ^ { 2 } } \int _ { 1 } ^ { 1 } { \sqrt { 1 + t ^ { 4 } } } d t d x } \\ { = - \displaystyle \int _ { 0 } ^ { 1 } { \sqrt { 1 + t ^ { 4 } } } d t \int _ { 0 } ^ { t } { x ^ { 2 } } d \dot { \overline { { { \varphi } _ { 2 } } } } \leq \frac { 1 } { 3 } \int _ { 0 } ^ { 1 } { \sqrt { 1 + t ^ { 4 } } } d t = - \displaystyle \frac { 1 } { 1 2 } \int _ { 0 } ^ { 1 } { \sqrt { 1 + t ^ { 4 } } } d ( 1 + t ^ { 4 } ) } \\ { \displaystyle \left. - \frac { 1 } { 1 2 } \frac { 2 } { 3 } ( 1 + t ^ { 4 } ) \right| _ { 0 } ^ { 1 } = - \frac { 2 \sqrt { 2 } - 1 } { 1 8 } } \end{array}
$$

6.幂级数 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n - 1 } n x ^ { n - 1 }$ 在区间(-1,1)内的和函数S(x)=(

幂级数 $\sum _ { n = 1 } ^ { \infty } n x ^ { n - 1 }$ 的收敛半径为 $\operatorname* { l i m } _ { n \to \infty } { \frac { n } { n + 1 } } = 1$ ，且其在x=±1处通项都是无穷 大量，故其在x=±1处发散，故幂级数的收敛域为(-1,1).

在(-1,1)内，

$$
\sum _ { n = 1 } ^ { \infty } n x ^ { n - 1 } = \sum _ { i = 1 } ^ { \infty } ( x ^ { n } ) ^ { i - 2 } ( \sum _ { n = 1 } ^ { \infty } x ^ { n } ) ^ { i } = ( \sum _ { n = 0 } ^ { \infty } x ^ { n } ) ^ { i } = ( { \frac { 1 } { 1 - x } } ) ^ { i } = { \frac { 1 } { ( 1 - x ) ^ { 2 } } }
$$

故幂级数 2 $1 ) ^ { n - 1 } n x ^ { n - 1 } = \sum _ { n = 1 } ^ { \infty } n ( - x ) ^ { n - 1 }$ 的收敛域为 $\left\{ x \middle | - x \in ( - 1 , 1 ) \right\} = ( - 1 , 1 )$ ，和函数为n=1  
${ \frac { 1 } { \left[ 1 - ( - x ) \right] ^ { 2 } } } = { \frac { 1 } { \left( 1 + x \right) ^ { 2 } } }$

7.对区域 $D = \left\{ ( x , y ) \middle | x ^ { 2 } + y ^ { 2 } < 1 \right\}$ 内任意按段光滑曲线L，若曲线积分 $\int _ { L } \frac { x d x - a y d y } { x ^ { 2 } + y ^ { 2 } - 1 }$ 与路径无关，则a=（

## 【宝哥解答】

依据积分与路径的无关性，有 $\frac { \partial } { \partial y } \frac { x } { x ^ { 2 } + y ^ { 2 } - 1 } = \frac { \partial } { \partial x } \frac { - a y } { x ^ { 2 } + y ^ { 2 } - 1 }$ $- \frac { 2 x y } { \left( x ^ { 2 } + y ^ { 2 } - 1 \right) ^ { 2 } } { = } \frac { 2 a x y } { \left( x ^ { 2 } + y ^ { 2 } - 1 \right) ^ { 2 } } , ( x , y ) \in D \mathrm { ~ , ~ }$

即a=-1.

$$
\Sigma = \left\{ ( x , y , z ) { \big | } x + y + z = 1 , x \geq 0 , y \geq 0 , z \geq 0 \right\}
$$

## 【宝哥解答】

$$
\begin{array} { l } { { \displaystyle \iint y ^ { 2 } d S = \int _ { 0 } ^ { 1 } y ^ { 2 } d y \int _ { 0 } ^ { 1 - y } \sqrt { 1 + { z _ { x } ^ { 2 } } ^ { \frac { 2 } { 2 } } { \hat { x } } ^ { 2 } - { z _ { y } ^ { 2 } } } \overline { { d x } } = \int _ { 0 } ^ { 1 } y ^ { 2 } d y \int _ { 0 } ^ { 1 - y } \sqrt { 1 + ( - 1 ) ^ { 2 } + ( - 1 ) ^ { 2 } } d x } } \\ { { \displaystyle \vphantom { \int _ { 0 } ^ { 1 - y } } \sum _ { j } y ^ { 2 } d y \int _ { 0 } ^ { 1 - y } d x = \sqrt { 3 } \int _ { 0 } ^ { 1 } y ^ { 2 } ( 1 - y ) d y = \frac { \sqrt { 3 } } { 1 2 } } } \end{array}
$$

## 二.计算题（本大题共5小题，每小题6分，共30分)

1.求极限 $\operatorname* { l i m } _ { x \to 0 } { \frac { \ln ( 1 + x ) ^ { \frac { 1 } { x } } - 1 } { \ln ( 1 + x ) } }$

$$
\operatorname* { l i m } _ { x \to 0 } { \frac { \ln ( 1 + x ) ^ { \frac { 1 } { x } } - 1 } { \ln ( 1 + x ) } } = \operatorname* { l i m } _ { x \to 0 } { \frac { x } { x } } = \operatorname* { l i m } _ { x \to 0 } { \frac { \ln ( 1 + x ) - x } { x ^ { 2 } } } = \operatorname* { l i m } _ { x \to 0 } { \frac { - { \frac { 1 } { 2 } } x ^ { 2 } } { x ^ { 2 } } } = - { \frac { 1 } { 2 } }
$$

2.计算积分 $\int _ { - 2 } ^ { 2 } \operatorname* { m i n } \left. \frac { 1 } { \left. x \right. } , x ^ { 2 } \right. d x$ ，其中min表示取最小值.

## 【宝哥解答】

$$
\begin{array} { l } { { \displaystyle \int _ { - \infty } ^ { 2 } \operatorname* { m i n } _ { 0 } ^ { \frac { 1 } { 2 } } ( | x | , x ^ { - 2 } ) d x \ = \ 2 \int _ { 0 } ^ { 2 } \operatorname* { m i n } _ { 0 } \{ \frac { 1 } { | x | } , x ^ { 2 } \} d x = 2 \int _ { 0 } ^ { 1 } x ^ { 2 } d x + 2 \int _ { 1 } ^ { 2 } \frac { 1 } { | x | } d x } } \\ { { \displaystyle  = \frac { 2 } { 3 } x ^ { 3 } | 0 + 2 \int _ { 1 } ^ { 2 } \frac { 1 } { x } d x = \frac { 2 } { 3 } + 2 \ln x | _ { 1 } ^ { 2 } = \frac { 2 } { 3 } + 2 \ln 2 } } \end{array}
$$

3.设 $z = z ( x , y )$ 为方阵 $f ( x - y , y - z , z - x ) = 0$ 所确定的隐函数，求 $\frac { \partial z } { \partial x } , \frac { \partial z } { \partial y }$ 和dz.

## 【宝哥解答】

令 $G ( x , y , z ) = f ( x - y , y - z , z$ x如果f连续可微，且 $f _ { 3 } ^ { \prime } - f _ { 2 } ^ { \prime } \neq 0$ ，由隐函数存在定理的结论，

$$
\frac { \partial Z } { \partial x } = - \frac { G _ { x } } { G _ { z } } = - \frac { f _ { 1 } ^ { \prime } - f _ { 3 } ^ { \prime } } { - f _ { 2 } ^ { \prime } + f _ { 3 } ^ { \prime } } , \frac { \partial z } { \partial y } = - \frac { G _ { y } } { G _ { z } } = - \frac { - f _ { 1 } ^ { \prime } + f _ { 2 } ^ { \prime } } { - f _ { 2 } ^ { \prime } + f _ { 3 } ^ { \prime } } ,
$$

$$
d z = { \frac { \partial z } { \partial x } } d x + { \frac { \partial z } { \partial y } } d y = - { \frac { f _ { 1 } ^ { \prime } - f _ { 3 } ^ { \prime } } { - f _ { 2 } ^ { \prime } + f _ { 3 } ^ { \prime } } } d x - { \frac { - f _ { 1 } ^ { \prime } + f _ { 2 } ^ { \prime } } { - f _ { 2 } ^ { \prime } + f _ { 3 } ^ { \prime } } } d y
$$

4.求函数 $f ( x ) = \arctan { \frac { 2 x } { 1 - x ^ { 2 } } }$ 在x=0处的幂级数展开式

## 【宝哥解答】

对任意 $x \in ( - 1 , 1 )$ ，由倍角公式和反正切函数的麦克劳林展开式，有

$$
f ( x ) = \arctan { \frac { \mathcal { Q } x ^ { 2 } } { 1 - x ^ { 2 } } } = \arctan \tan \tan ( 2 \arctan x ) = 2 \arctan x = 2 \sum _ { n = 1 } ^ { \infty } { \frac { ( - 1 ) ^ { n - 1 } } { 2 n - 1 } } x ^ { 2 n - 1 }
$$

5.设区域 $D = \left\{ ( x , y ) \left| x ^ { 2 } + y ^ { 2 } \leq a x \right. \right\}$ 计算二重积分

$$
I = \iint _ { D } { ( x ^ { 3 } y ^ { 2 0 1 9 } + y ^ { 3 } \sqrt { x ^ { 2 0 2 0 } + y ^ { 2 0 2 0 } } + x \sqrt { x ^ { 2 } + y ^ { 2 } } ) d x d y }
$$

区域D关于x轴对称， $x ^ { 3 } y ^ { 2 0 1 9 } , y ^ { 3 } { \sqrt { x ^ { 2 0 2 0 } + y ^ { 2 0 2 0 } } }$ 关于y都是奇函数，故它们在D上积分都是0.

令 $\{ \begin{array} { l l } { x = r \cos \theta } \\ { y = r \sin \theta } \end{array} , r \geq 0 , \theta \in [ - \pi , \pi ]$ ，代入边界曲线，可得 $r ^ { 2 } = a r \cos \theta$ ，即$r = a \cos \theta \geq 0$ ，故 $\theta \in \left[ \frac { \pi } { 3 } , \frac { \pi } { 2 } \right]$ 事研

$$
\begin{array} { l } { { \displaystyle I = \int \int ( x ^ { \frac { x ^ { 3 } } { 2 \pi ^ { 2 } } \sigma ^ { 2 0 } \sigma ^ { 3 } } + y ^ { \frac { 2 0 2 0 } { 3 } } + y ^ { 2 0 2 0 } + x \sqrt { x ^ { 2 } + y ^ { 2 } } ) d x d y = \int \int x \sqrt { x ^ { 2 } + y ^ { 2 } } d x d y } } \\ { { \displaystyle \varphi ^ { \rho \varphi D } } } \\ { { \displaystyle - \int _ { - \frac { \pi } { 2 } } ^ { \pi } d \theta \int _ { 0 } ^ { \alpha \cos \theta } r \cos \theta \cdot r \cdot d r = \int _ { - \frac { \pi } { 2 } } ^ { \frac { \pi } { 2 } } \cos \theta \frac { \left( a \cos \theta \right) ^ { 4 } } { 4 } d \theta } } \\ { { \displaystyle - \frac { 1 } { 4 } a ^ { 4 } \int _ { - \frac { \pi } { 2 } } ^ { \frac { \pi } { 2 } } \cos ^ { 3 } \theta d \theta = \frac { 1 } { 2 } a ^ { 4 } \int _ { 0 } ^ { \frac { \pi } { 2 } } \cos ^ { 5 } \theta d \theta = \frac { 1 } { 2 } a ^ { 4 } \frac { 4 } { 5 } \frac { 2 } { 3 } = \frac { 4 } { 1 5 } a ^ { 4 } } } \end{array}
$$

## 三.综合题（本大题共3小题，每小题10分，共30分）

1.设 $f ( x ) = { \left\{ \begin{array} { l l } { \displaystyle \left| x \right| ^ { \alpha } \sin { \frac { 1 } { x } } , 0 < \left| x \right| \leq 1 } \\ { 0 , \qquad x = 0 } \end{array} \right. }$

（1)问α在什么条件时，f（0）存在？并求此时f（0）的值.

（2）问α在什么条件时，f（x）在[-1,1]上有界？

（3）问α在什么条件时，f‘（x)在[-1,1]上连续？

## 【宝哥解答】

我们首先引入并证明如下结论：

设 $g ( x ) = \left| x \right| ^ { m } \sin \frac { 1 } { x } , x \neq 0$ 则 $\operatorname* { l i m } _ { x \to 0 ^ { + } } g ( x )$ 存在当且仅当 $m > 0$ ，若 $m > 0$ ，则证明： $\operatorname* { l i m } _ { x \to 0 } g ( x ) = 0$ 宝哥数学必要性

取 $x _ { n } = \frac { 1 } { ( n + \displaystyle \frac { 1 } { 2 } ) \pi } , n = 1 , 2 , \cdots$ ，则 $\operatorname* { l i m } _ { n \to \infty } g ( x _ { n } )$ 存在，即 $\operatorname * { l i m } _ { n  \infty } \frac { ( - 1 ) ^ { n } } { ( n + \displaystyle \frac { 1 } { 2 } ) ^ { m } \pi ^ { m } }$ 存在，

充分性

$m > 0$ 时， $\operatorname* { l i m } _ { x \to 0 } \left| x \right| ^ { \cdot \pi } = 0$ $\left| \sin { \frac { 1 } { x } } \right| \leq 1$ ，故 $\operatorname* { l i m } _ { x \to 0 } g ( x ) = 0$

同理可得：

设 $g ( x ) = \left| x \right| ^ { m } \cos { \frac { 1 } { x } } , x \neq 0$ 则 $\operatorname* { l i m } _ { x  0 ^ { + } } g ( x )$ （x）存在当且仅当 $m > 0$ ，若 $m > 0$ ，则 $\operatorname* { l i m } _ { x \to 0 } g ( x ) = 0$

（）存在， $\operatorname* { l i m } _ { x \to 0 ^ { + } } { \frac { f ( x ) - f ( 0 ) } { x } } = \operatorname* { l i m } _ { x \to 0 ^ { + } } \left| x \right| ^ { \alpha - 1 } \sin { \frac { 1 } { x } }$ 存在，即 $\alpha - 1 > 0$ ，即 $\alpha > 1$ $\dot { \alpha } > 1$ 时， $| { \frac { f ( x ) - f ( 0 ) } { x } } | = | x | ^ { \alpha - 1 } | \sin { \frac { 1 } { x } } | \leq | x | ^ { \alpha - 1 }  0 , x  0$ ，故 $\operatorname* { l i m } _ { x \to 0 } \left. { \frac { f ( x ) - f ( 0 ) } { x } } \right. = 0$ 即 $\operatorname* { l i m } _ { x \to 0 } { \frac { f ( x ) - f ( 0 ) } { x } } = 0$ ，即 $f ^ { \prime } ( 0 ) = 0$

(2)当α>1时，

$\cos \frac { 1 } { x } , 0 < | x | \leq 1$

如果f（x）在[-1,1]上有界，取 $x _ { n } = { \frac { 1 } { 2 n \pi } } , n = 1 , 2 , \cdots$ ，则 $\left\{ f ^ { \prime } ( x _ { n } ) \right\}$ 有界，即$\left\{ \left. { \frac { 1 } { 2 n \pi } } \right. ^ { \alpha - 2 } \right\}$ 有界，即 $\alpha - 2 \geq 0$ ，即 $\alpha \ge 2$

当 $\alpha \ge 2$ 时，对任意x， $0 < \left| x \right| \leq 1$ ，有

$| f ^ { \prime } ( x ) | = | \alpha | x | ^ { \alpha - 1 } \operatorname { s g n } ( x ) \sin { \frac { 1 } { x } } - | x | ^ { \alpha - 2 } \cos { \frac { 1 } { x } } | \leq \alpha |$ ##a+1，

故f'(x)在[-1,1]上有界.

（3)当α>1时， $\operatorname* { l i m } _ { x \to 0 } \alpha \big | x \big | _ { x } ^ { \alpha - 1 } \operatorname { s g n } ( x ) \ \mathrm { s i n } \frac { \ d H } { x } = 0$ .若f‘(x)在[-1,1]上连续，则f(x)在0连续，即 $\operatorname* { l i m } _ { x \to 0 } \left| x \right| ^ { \alpha - 2 } \cos \frac { 1 } { x } = 0$ ，这等价于 $\alpha - 2 > 0$ ，即 $\alpha > 2$

若 $\alpha > 2$ ，则 $f ^ { \prime } ( x ) = { \left\{ \begin{array} { l l } { \alpha \left| x \right| ^ { \alpha - 1 } \operatorname { s g n } ( x ) \sin { \displaystyle \frac { 1 } { x } } - \left| x \right| ^ { \alpha - 2 } \cos { \displaystyle \frac { 1 } { x } } , 0 < \left| x \right| \leq 1 } \\ { 0 , x = 0 } \end{array} \right. }$ 在 $0 < \left| x \right| \leq 1$ H

连续，在𝑥=0也连续，故f(x)在[-1,1]上连续.

因此， $\alpha > 2$ 时，f(（x）在[-1,1]上连续.

2.求参数k取何值时，方程 $k x + \frac { 1 } { x ^ { 2 } } = 1$ 在 $x \in ( 0 , + \infty )$ 上有唯一解？me

【宝哥解答】

方程等价于

$$
k = \frac { 1 - \frac { 1 } { x ^ { 2 } } } { x } = \frac { 1 } { x } - \frac { 1 } { x ^ { 3 } }
$$

令 $f ( x ) = \frac { 1 } { x } - \frac { 1 } { x ^ { 3 } }$ ，则 $f ^ { \prime } ( x ) = - \frac { 1 } { x ^ { 2 } } + \frac { 3 } { x ^ { 4 } } = \frac { 3 - x ^ { 2 } } { x ^ { 4 } }$ .在 $( 0 , \sqrt { 3 } )$ 上， $f ^ { \prime } ( x ) > 0$ ，f（x)单调递增；在 $( { \sqrt { 3 } } , + \infty )$ f‘（x）<0，f（x）单调递减. $\operatorname * { l i m } _ { x  0 + } f ( x ) = - \infty , \operatorname * { l i m } _ { x  + \infty } f ( x ) = 0$ $f ( { \sqrt { 3 } } ) = \frac { x ^ { 2 } - 1 } { x ^ { 3 } } = \frac { 2 } { 3 { \sqrt { 3 } } } = \frac { 2 } { 9 } { \sqrt { 3 } }$ 画出f（x）在（0,+∞）上的图象

<!-- image-->

因此，当 $k \leq 0$ 或 $k = \frac { 2 } { 9 } \sqrt { 3 }$ ，方程有唯一解；当 $k > \frac { 2 } { 9 } \sqrt { 3 }$ ，方程无解；当 $0 < k < \frac { 2 } { 9 } \sqrt { 3 }$ 方程有两个解.

由于方程有且只有一个解，因此，k≤0或 $k = \frac { 2 } { 9 } \sqrt { 3 }$

3.计算曲面积分 $\check { x } = \int \int \frac { \alpha x d y d z + ( z + a ) ^ { 2 } d x d y } { \sqrt { x ^ { 2 } + y ^ { 2 } + z ^ { 2 } } }$ ，其中Σ为下半球面 $z = - \sqrt { a ^ { 2 } - x ^ { 2 } - y ^ { 2 } }$ 的上侧， $a > 0$ 为常数.

## 【宝哥解答】

£为下半球面 $z = - \sqrt { a ^ { 2 } - x ^ { 2 } - y ^ { 2 } }$ 的上侧， $a > 0$ 为上侧，

$$
\iint \frac { a x d y d z + ( z + a ) ^ { 2 } d x d y } { \sqrt { x ^ { 2 } + y ^ { 2 } + z ^ { 2 } } } = \frac { 1 } { a } \iint a x d y d z + ( z + a ) ^ { 2 } d x d y
$$

下面来计算 $\iint _ { \Sigma } a x d y d z + ( z + a ) ^ { 2 } d x d y$

方法一

记 $\Sigma _ { \imath }$ 为 $\left\{ { x ^ { 2 } + y ^ { 2 } \leq a ^ { 2 } } \right.$ ，取下侧，Ω为 $\Sigma , \Sigma _ { 1 }$ 围成的立体，

$$
\iint _ { \Sigma _ { 1 } } a x d y d z + ( z + a ) ^ { 2 } d x d y = - \iint _ { \Sigma _ { 1 } } a ^ { 2 } d x d y = - \pi a ^ { 4 } ,
$$

由Gauss公式，有

$$
\begin{array} { l } { { { \displaystyle { \iint } \int } \{ a x d y d z + ( z \pm a ) ^ { 2 } \frac { a \cdot K \cdot } { c \cdot } \phi ^ { 2 } - ( \int \int - \int ) \chi x d y d z + ( z + a ) ^ { 2 } d x d y } }  \\ { { \le - { \displaystyle { \iint } \int } \left[ \frac { \partial ( \widehat { x } \cdot \widehat { x } ) } { \widehat { x } } - \frac { \partial ( \bar { x } ( z + a ) ^ { 2 } ) } { \partial z } \right] d x d y d z + \pi a ^ { 4 } = - { \displaystyle { \iint } \int } \left( 2 z + 3 a \right) d x d y d z + \pi a ^ { 4 } } } \\ { { = - 2 { \displaystyle { \int } \int } _ { - a } ^ { 0 } z d z { \displaystyle { \iint } \ } \ { d x d y - 3 a \cdot \frac { \int } { 3 } \pi a ^ { 3 } + \pi a ^ { 4 } = - 2 \pi { \displaystyle { \int } \int } _ { - a } ^ { 0 } z ( a ^ { 2 } - z ^ { 2 } ) d z - \pi a ^ { 4 } } } } \\ { { = - 2 \pi ( - \frac { 1 } { 4 } a ^ { 4 } ) - \pi a ^ { 4 } = - \frac { 1 } { 2 } \pi a ^ { 4 } } } \end{array}
$$

## 方法二

$$
\begin{array} { l } { { \sqrt { 2 ^ { 2 R } - 2 } } } \\  { [ \int \displaystyle { a x d y d z } ( { z + a } ) ^ { 2 } d x d y = \displaystyle { \int \int [ \frac { { z \sqrt { 2 } } \ z } { R \sqrt { 2 ^ { 2 } + { z ^ { 2 } } } } ( { z + a } ) ^ { 2 } ] d x d y } = \displaystyle { \int \int \int _ { x ^ { + } } ^ { { \bar { z } } } { ( - a x \frac { x } { z } + { z ^ { 2 } } + 2 a z + a ^ { 2 } ) d x d y } } } \\ { { \mathrm { } } } \\  { \mathrm { } = \displaystyle { \int \int _ { x ^ { + } + { y } } ^ { { \bar { z } } } { ( { z - a } \frac { x ^ { 2 } } { \sqrt { 2 ^ { 2 } - x ^ { 2 } } } - \frac { { a \sqrt { 2 } } \ z } { b { \sqrt { 2 ^ { 2 } + { z ^ { 2 } } } } } ) d x d y } } } \\ { { \displaystyle { \mathrm { } } } } \\  { \displaystyle { \mathrm { } \mathrm { } } x ^ { \mathrm { 2 } } + { { y ^ { 2 } } } \displaystyle { \sum _ { x ^ { + } } ^ { \bar { z } } { ( { z ^ { 2 } } - x ^ { 2 } - \frac { { a \sqrt { 2 } } \ z } { b { \sqrt { 2 ^ { 2 } + { z ^ { 2 } } } } } ) d x d y } } } \\ { { \displaystyle { \mathrm { } } } } \\  { \displaystyle { \mathrm { } } x ^ { \mathrm { 2 } } \displaystyle { \int _ { a } ^ { \bar { z } } { \mathrm { } \sqrt { { a ^ { 2 } } - x ^ { 2 } - y ^ { 2 } } } } } \\ { { \displaystyle { \mathrm { } } } } \\   \displaystyle { \mathrm { } } = \displaystyle { \frac { 1 } { 2 } } { a \frac { \nu ^ { 2 } } { \sqrt { { a ^ { 2 } } - x ^ { 2 } } } } d { \nu } = \displaystyle  \int \int _ { a } ^ { \infty }  \frac { { r ^ { 3 } } } { \sqrt { { a ^ { 2 } } - x ^ { 2 } } }  \end{array}
$$

$\stackrel { \textstyle \iint } { \operatorname { \jmath } ^ { 2 } + y ^ { 2 } } d x d y = \pi a ^ { 2 } , \qquad \int \int ( x ^ { 2 } + y ^ { 2 } ) d x d y = \frac { 1 } { 2 } \pi a ^ { 4 } ,$ $\iint _ { + \infty } \sqrt { a ^ { 2 } - x ^ { 2 } - y ^ { 2 } } d x d y = \int _ { 0 } ^ { a } \sqrt { a ^ { 2 } - r ^ { 2 } } r d r \int _ { 0 } ^ { 2 \pi } d \theta _ { - } = 2 \pi \int _ { 0 } ^ { a } \sqrt { a ^ { 2 } - r ^ { 2 } } r d r = - \frac { 2 \pi } { 3 } ( a ^ { 2 } - r ^ { 2 } ) ^ { \frac { 3 } { 2 } } \Big | a \ \sin ^ { 2 } \theta _ { - } \Big \{ \frac { \pi } { 3 } ( a - b ) ^ { \frac { 3 } { 2 } } \Big | a \Big | ^ { 2 } ,$ 故$\iint a x d y d z + ( z \stackrel { \infty } { \underset {  } { \scriptscriptstyle ( a ) } } ) ^ { 2 } d x d y = - a \frac { 2 } { 3 } \pi a ^ { 3 } + 2 \pi a ^ { 4 } - \frac { 1 } { 2 } \pi a ^ { 4 } - \frac { 4 \pi } { 3 } a ^ { 4 } = - \frac { 1 } { 2 } \pi a ^ { 4 }$ 因此 $\iint _ { z ^ { 2 } } ^ { a x d y d z + ( z + a ) ^ { 2 } d x d y } = - \frac { 1 } { 2 } \pi a ^ { 3 }$

## 四.证明题(本大题共5小题，每小题10分，共50分)

1.设 $\left\{ a _ { n } \right\}$ 是递增有界正数列，求证：级数 $\sum _ { n = 1 } ^ { \infty } ( 1 - \frac { a _ { n } } { a _ { n + 1 } } )$ 收敛.

## 【宝哥解答】

$\left\{ a _ { n } \right\}$ 是递增有界正数列，由单调有界准则 $\because \{ a _ { n } \}$ 收敛，记其极限为a.

$$
a _ { n + 1 }
$$

$$
\sum _ { k = 1 } ^ { \cdot } ( a _ { k + 1 } - a _ { k } ) = a _ { n + 1 } - a _ { 1 } \to a - a _ { 1 } , n \to \infty ,
$$

故正项级数 $\sum _ { n = 1 } ^ { \infty } ( a _ { n + 1 } - a _ { n } )$ 收敛.

对任意正整数n， $0 \leq 1 - \frac { a _ { n } } { a _ { n + 1 } } = \frac { a _ { n + 1 } - a _ { n } } { a _ { n + 1 } } \leq \frac { a _ { n + 1 } - a _ { n } } { a _ { 1 } \sigma } ^ { * }$ 正项级数 $\sum _ { n = 1 } ^ { \infty } ( a _ { n + 1 } - a _ { n } )$ 收敛，由比较判别法，正项级数 $\sum _ { n = 1 } ^ { \infty } ( 1 - \frac { a _ { n } ^ { n } } { a _ { n + 1 } } )$ 收敛.

2.设 $f ( x ) = { \frac { x + 2 } { x + 1 } } \sin { \frac { 1 } { x } }$ a>0为常数，试证：f（x）在（0,a）内非一致连续，而在$[ a , + \infty )$ 上一致连续.

## 【宝哥解答】

首先引入并证明如下结论：

f(x)在有限开区间(a,b)内一致连续当且仅当f(x)在(a.h)内连续

且 $f ( a ^ { + } ) , f ( \xi ^ { - } )$ 存在.

证明：

必要性

f(x)在有限开区间(a,b)内一致连续，故f(x)在(a,b)内连续，对任意 $\varepsilon > 0$ 存在 $\delta \in ( 0 , b - a )$ )，使得对任意x $y \in ( a , b )$ ，只要 $\left| x - y \right| < \delta$ ，就有 $\left| f ( x ) - f ( y ) \right| < \varepsilon$ 故对任意 $x , y _ { 1 } \in \left( a , \dot { a } + \widetilde { \delta } \right)$ 和 $x , y \in ( b - \delta , b )$ ，都有 $\vert f ( x ) - f ( y ) \vert < \varepsilon$ .由柯西收敛准则，f（a）和f（b-）存在.充分性

设f(x)在(a,b)内连续且 $f ( a ^ { + } ) , f ( b ^ { - } )$ 存在，令 $F ( x ) = \left\{ \begin{array} { l l } { f ( x ) , a < x < b } \\ { f ( a ^ { + } ) , x = a } \\ { f ( b ^ { - } ) , x = b } \end{array} \right.$ ，则 F(x)在[a,b]上连续，故F(x）在[a,b]上一致连续，故F（x)在（a,b)内一致连续， 即f(x)在(a,b)内一致连续.

结论证明完毕！#

再引入并证明如下结论：

设f（x）在 $[ a , + \infty )$ 上连续， $\operatorname* { l i m } _ { x \to + \infty } f ( x )$ 存在，则f（x）在 $[ a , + \infty )$ 上一致连续.证明：

$\operatorname* { l i m } _ { x \to + \infty } f ( x )$ 存在，由柯西收敛准则，对任意>0，总存在，便得对任意$x , y \geq X$ ，恒有 $\left| f ( x ) - f ( y ) \right| < \frac { 1 } { 2 } \varepsilon$ 考研

f（x)在[a,+∞)上连续，故f（x）在[a,X]上连续，由康托定理，f（x)在[a,x]$\delta > 0$ ，使得对任意 $x , y \in [ a , X ]$ ，只要 $\vert x - y \vert < \delta$ 就有 $\left| f ( x ) - f ( y ) \right| < \frac { 1 } { 2 } \varepsilon$

现在任取 $x < y \in [ a , + \infty )$ ，使得 $\vert x - y \vert < \delta$

i若 $x , y \in \left[ a , X \right]$ ，则 $\vert f ( x ) - f ( y ) \vert < \frac { 1 } { 2 } \varepsilon$

(ii)若 (ii）右 $x , y \geq X$ ，则 $\left| f ( x ) - f ( y ) \right| < \frac { 1 } { 2 } \varepsilon$

（ii）若 $x \in [ a , X ] , y \in [ X , + \infty )$ )，则 $\vert x - X \vert \leq \left. x - y \right. < \delta$ $\vert X - y \vert \leq \left. x - y \right. < \delta$ ，故

$$
\vert f ( x ) - f ( X ) \vert < \frac { 1 } { 2 } \varepsilon \ , \ \vert f ( X ) - f ( y ) \vert < \frac { 1 } { 2 } \varepsilon
$$

故

$$
\big | f ( x ) - f ( y ) \big | \leq \big | \widehat { \mathcal { f } } ( x ) - f ( X ) \big | + \big | f ( X ) - f ( y ) \big | < \frac { 1 } { 2 } \varepsilon + \frac { 1 } { 2 } \varepsilon = \varepsilon
$$

综上所述，对任意 $x < y \in \left[ a , + \infty \right)$ ，只要 $\left| x - y \right| < \delta$ ，就有 $\vert f ( x ) - f ( y ) \vert < \varepsilon$ 故在[ $[ a , + \infty )$ 上一致连续.结论证明完毕！#

回到本题， $\operatorname* { l i m } _ { x \to 0 ^ { + } } f ( x ) = \operatorname* { l i m } _ { x \to 0 ^ { + } } { \frac { x + 2 } { x + 1 } } \mathrm { s i n } { \frac { 1 } { x } }$ ，故f（x)在(0,a)内不一致连续.

$$
[ a , + \infty )
$$

$$
\operatorname* { l i m } _ { x \to + \infty } f ( x ) = 0
$$

$$
[ a , + \infty )
$$

3.设函数f（x）在区间[0,1]上连续，在开区间（0,1）内可导，且 $f ( 1 ) = 0$ ，证明：存在 $\xi \in ( 0 , 1 )$ ，使得 $f ( \xi ) + ( 1 - e ^ { - \xi } ) f _ { \mathrm { { s } } } ^ { \prime } ( \xi )$

## 【宝哥解答】

即证明 $f ( x ) \pm ( 1 - e ^ { - x } ) f ^ { \prime } ( x )$ 在（0,1)内有零点，即

$$
e ^ { x } \left[ f ( x ) + \overleftarrow { ( 1 - e ^ { - x } ) } f ^ { \prime } ( x ) \right] = e ^ { x } f ( x ) + ( e ^ { x } - 1 ) f ^ { \prime } ( x ) = ( e ^ { x } - 1 ) ^ { \prime } f ( x ) + ( e ^ { x } - 1 ) f ^ { \prime } ( x )
$$

$$
= [ ( e ^ { x } - 1 ) f ( x ) ] ^ { \prime }
$$

在(0,1)内有零点.令 $F ( x ) = ( e ^ { x } - 1 ) f ( x )$ ，则F（x）在区间[0,1]上连续，在开区间（0,1)内可导，且F(0)=F(1)=0.由罗尔中值定理，存在 $\xi \in ( 0 , 1 )$ ，使得 $F ^ { \prime } ( \xi ) = 0$ 即 $f ( \xi ) + ( 1 - e ^ { - \xi } ) f ^ { \prime } ( \xi ) = 0$

4.确定函数 $g ( \alpha ) = \int _ { 0 } ^ { + \infty } \frac { \ln ( 1 + x _ { 1 } ^ { 3 } ) } { x ^ { \alpha } } d x$ 的定义域，并证明g(α)在该定义域上连续.

## 【宝哥解答】

分别考查积分 $\int _ { 0 } ^ { 1 } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } d x$ 和 $\int _ { 1 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } }$ dx的收敛性.

$$
{ \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } \sim { \frac { x ^ { 3 } } { x ^ { \alpha } } } = { \frac { 1 } { x ^ { \alpha - 3 } } } , x  0 ^ { + }
$$

$\int _ { 0 } ^ { 1 } { \frac { d x } { x ^ { \alpha - 3 } } }$ 收敛当且仅当 $\alpha - 3 < 1$ ，即 $\alpha < 4$ ，故 $\int _ { 0 } ^ { 1 } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } d x$ 收敛当且仅当 $\alpha < 4$

$$
\frac { \operatorname* { l i m } _ { x \to \infty } ^ { \infty } \frac { x ^ { \alpha } } { x ^ { \alpha } } } { \ln x } = \operatorname* { l i m } _ { x \to \infty } \frac { \alpha \ln x - \ln \ln ( 1 + x ^ { 3 } ) } { \ln x } = \alpha
$$

由对数判别法，若 $\alpha > 1$ ，则 $\int _ { 1 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } }$ dx收敛，若 $\alpha < 1$ ，则 $\int _ { 1 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } d x$ 发散 $\frac { \ln ( 1 + x ^ { 3 } ) } { x } \geq \frac { \ln 2 } { x } , \forall x \geq 1$ $\int _ { 1 } ^ { + \infty } { \frac { d x } { x } }$ 发散，故 $\int _ { 1 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x } } d x$ 发散.因此， $\int _ { 1 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } }$ dx收敛当且仅当 $\alpha > 1$

综上所述， $\int _ { 0 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } }$ dx的收敛域为（1,4），即 $g ( \alpha )$ 的定义域为(1,4).任取 $\left[ s _ { 0 } , S _ { 0 } \right] \subset \left( 1 , 4 \right) _ { \varepsilon }$ 对在意 $\omega \in \left[ s _ { 0 } , S _ { 0 } \right]$

$$
0 < \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } \leq \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { S _ { 0 } } } , \forall x \in \left( 0 , 1 \right] ,
$$

$$
0 < \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } \leq \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { s _ { 0 } } } , \forall x \in \left[ 1 , + \infty \right)
$$

$\int _ { 0 } ^ { 1 } \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { S _ { 0 } } } d x$ 收敛，故 $\int _ { 0 } ^ { 1 } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } d x$ 在 $\left[ s _ { 0 } , S _ { 0 } \right]$ 上一致收敛 $\int _ { 1 } ^ { + \infty } \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { s _ { 0 } } } d x$ 收敛，故 $\int _ { 1 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } }$ dx在 $[ s _ { 0 } , S _ { 0 } ]$ 上一致收敛故 $\int _ { 0 } ^ { \pi } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } d x$ 在 $\left[ s _ { 0 } , S _ { \scriptscriptstyle 0 } \right]$ 上一致收敛.$\int _ { 0 } ^ { + \infty } { \frac { \operatorname { I n } ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } d x$ 在(1,4)内闭一致收敛.由 $\left[ s _ { 0 } , S _ { 0 } \right]$ 的任意性，

又 $\frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } }$ 是 $( x , \alpha ) \in ( 0 , + \infty ) \times ( 1 , 4 )$ )的连续函数，故g(α)在其定义域(1,4)

5.设 $f ( x , y ) = \left\{ { \begin{array} { l } { { \frac { x ^ { 3 } + y ^ { 3 } } { x ^ { 2 } + y ^ { 2 } } } , ( x , y ) \neq ( 0 , 0 ) } \\ { { 0 , \ } } \end{array} } \right.$

(1)证明f（x,y）在(0,0)处连续；(2）证明f（x,y）在（0,0）处不可微.【宝哥宝哥解答】

（1）对任意（x，y）≠（0,0），有

$$
\begin{array} { l c l } { \displaystyle \mathop { \leq } | \mathcal { J } ( x , y ) | = | \frac { x ^ { 3 } + y ^ { 3 } } { x ^ { 2 } + y ^ { 2 } } | \leq \frac { x ^ { 2 } | x | + y ^ { 2 } | y | } { x ^ { 2 } + y ^ { 2 } } = \frac { x ^ { 2 } } { x ^ { 2 } + y ^ { 2 } } \big | x \big | + \frac { y ^ { 2 } } { x ^ { 2 } + y ^ { 2 } } \big | y \big | } \\ { \displaystyle \leq | x | + | y |  0 , ( x , y )  ( 0 , 0 ) } \end{array}
$$

故 $\operatorname* { l i m } _ { ( x , y )  ( 0 , 0 ) } | f ( x , y ) | { = } 0$ ，即 $\operatorname* { l i m } _ { ( x , y )  ( 0 , 0 ) } f ( x , y ) = 0 = f ( 0 , 0 )$ ，故f（x,y）在(0,0）处连续.

$$
f _ { x } ( 0 , 0 ) = \operatorname* { l i m } _ { x \to 0 } { \frac { f ( x , 0 ) - f ( 0 , 0 ) } { x } } = \operatorname* { l i m } _ { x \to 0 } { \frac { x } { x } } = 1
$$

$$
f _ { y } ( 0 , 0 ) = \operatorname* { l i m } _ { y \to 0 } { \frac { f ( 0 , y ) - f ( 0 , 0 ) } { y } } = \operatorname* { l i m } _ { y \to 0 } { \frac { y } { y } } = 1
$$

对任意（x,y）≠（0,0），有

$$
\begin{array} { r l } & { \frac { f ( x ; \gamma ) ^ { \top - } - f ( 0 , 0 ) - f _ { x } ( 0 , 0 ) x - f _ { y } ( 0 , 0 ) y } { \sqrt { x ^ { 2 } + y ^ { 2 } } } = \frac { \frac { x ^ { 3 } + y ^ { 3 } } { x ^ { 2 } + y ^ { 2 } } - x - y } { \sqrt { x ^ { 2 } + y ^ { 2 } } } } \\ & { = \frac { x ^ { 3 } + y ^ { 3 } - ( x ^ { 2 } + y ^ { 2 } ) \left( x + y \right) } { \left( x ^ { 2 } + y ^ { 2 } \right) ^ { \frac { 3 } { 2 } } } = - \frac { x ^ { 2 } y + x y ^ { 2 } } { \left( x ^ { 2 } + y ^ { 2 } \right) ^ { \frac { 3 } { 2 } } } } \end{array}
$$

$$
\operatorname* { l i m } _ { x = y > 0 \atop x = y > 0 } \frac { x ^ { 2 } y + x y ^ { 2 } } { ( x ^ { 2 } + y ^ { 2 } ) ^ { \frac { 3 } { 2 } } } = \operatorname* { l i m } _ { x  0 ^ { + } } \frac { 1 } { \sqrt { 2 } } = \frac { 1 } { \sqrt { 2 } }
$$

故 $\operatorname* { l i m } _ { ( x , y ) \to 0 } \frac { f ( x , y ) - f ( 0 , 0 ) - f _ { x } ( 0 , 0 ) x - f _ { y } ( 0 , 0 ) \mathcal { D } } { \sqrt { x ^ { 2 } + y ^ { 2 } } } \neq 0$ ，故f(𝑥,y)在(0,0)处不可微.

## tool · 2026-10-19T07:28:23Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 10714)
Total output lines: 668

## 杭州电子科技大学2022年数学分析真题解析

## 一.填空题(5×8=40分)

1 $\operatorname* { l i m } _ { n \to \infty } ( 1 + { \frac { 1 } { 2 } } + \cdots + { \frac { 1 } { n } } ) =$

【宝哥解答】

正项级数 $\sum _ { n = 1 } ^ { \infty } { \frac { 1 } { n } }$ 是发散的，故其部分和数列发散于+，即

$$
\operatorname* { l i m } _ { n \to \infty } ( 1 + { \frac { 1 } { 2 } } + \cdots + { \frac { 1 } { n } } ) = + \infty
$$

2. $( x ^ { 2 } e ^ { - 2 x } ) ^ { ( n ) }$

【宝哥解答】

由莱布尼兹法则，有

$$
\begin{array} { l } { { ( x ^ { 2 } e ^ { - 2 x } ) ^ { ( n ) } = x ^ { 2 } ( e ^ { - 2 x } ) ^ { ( n ) } + n ( x ^ { 2 } ) ^ { \prime } ( e ^ { - 2 x } ) ^ { ( n - 1 ) } + { \displaystyle \frac { n ( n - 1 ) } { 2 } } ( x ^ { 2 } ) ^ { \prime } ( e ^ { - 2 x } ) ^ { ( n - 2 ) } } } \\ { { = x ^ { 2 } ( - 2 ) ^ { n } e ^ { - 2 x } + n \cdot 2 x \cdot ( - 2 ) ^ { n - 1 } e ^ { - 2 x } + { \displaystyle \frac { n ( n - 1 ) } { 2 } } \times 2 \times ( - 2 ) ^ { n - 2 } e ^ { - 2 x } } } \\ { { = ( - 2 ) ^ { n - 2 } \Big \{ 4 x ^ { 2 } - 4 n x + n ( n - 1 ) \Big \} e ^ { - 2 x } } } \end{array} .
$$

3.设 $0 < k < \frac { 1 } { e }$ ，方程lnx-kx=0在 $( 0 , + \infty )$ 内根的个数为

【宝哥解答】

令 $f ( x ) = { \frac { \ln x } { x } } , x > 0$ ，则

$$
f ^ { \prime } ( x ) = { \frac { 1 - \ln x } { x ^ { 2 } } } .
$$

$0 < x < e$ 时， $f ^ { \prime } ( x ) > 0 ; x > e$ 时， $f ^ { \prime } ( x ) < 0$ .于是，f(x)在x=e取得了最大值$f ( e ) = { \frac { 1 } { e } } . f ( 0 ^ { + } ) = - \infty$ $f ( + \infty ) = 0$ .作出f(x)的图像如下：

<!-- image-->

$0 < k < \frac { 1 } { e }$ ，故曲线y=f(x)与直线 $y = k$ 有两个不同的交点，即方程 $\ln x - k x = 0$ 在 $( 0 , + \infty )$ 内根的个数为2.

4. $\int \frac { e ^ { x } - e ^ { - x } } { e ^ { x } + e ^ { - x } } d x =$

【宝哥解答】

$$
\int { \frac { e ^ { x } - e ^ { - x } } { e ^ { x } + e ^ { - x } } } d x = \int { \frac { d ( e ^ { x } + e ^ { - x } ) } { e ^ { x } + e ^ { - x } } } { \tan ( e ^ { x } + e ^ { - x } ) } + C .
$$

5.若正项级数 $\sum _ { n = 1 } ^ { \infty } u _ { n }$ 收敛且所有项 $u _ { n } \leq 3$ ，则级数 $\sum _ { n = 1 } ^ { \infty } \frac { u _ { n } } { \pi - u _ { n } }$ 是否收敛？【宝哥解答】

正项级数 $\sum _ { n = 1 } ^ { \infty } u _ { n }$ 收敛且所有项 $u _ { n } \leq 3$ ，故 $0 \leq \frac { u _ { n } } { \pi - u _ { n } } \leq \frac { u _ { n } } { \pi - 3 } , \forall n \in N ^ { + }$ $\sum _ { n = 1 } ^ { \infty } u _ { n }$ 收敛，由比较判别法，级数 $\sum _ { n = 1 } ^ { \infty } \frac { u _ { n } } { \pi - u _ { n } }$ 收敛.

6.给定方程 $F ( x , y , z ) = 0$ ，则 $\frac { \partial z } { \partial x } \frac { \partial x } { \partial y } \frac { \partial y } { \partial z } =$

【宝哥解答】

按照隐函数存在定理的结论，如果函数 $F ( x , y , z )$ 连续可微，且 $F _ { x } , F _ { y } , F _ { z }$ 均非零，有

$$
\frac { \partial z } { \partial x } = - \frac { F _ { x } } { F _ { z } } , \frac { \partial x } { \partial y } = - \frac { F _ { y } } { F _ { x } } , \frac { \partial y } { \partial z } = - \frac { F _ { z } } { F _ { y } } ,
$$

故

$$
\frac { \partial z } { \partial x } \frac { \partial x } { \partial y } \frac { \partial y } { \partial z } = ( - \frac { F _ { x } } { F _ { \varepsilon } } ) ( - \frac { F _ { y } } { F _ { x } } ) ( - \frac { F _ { x } } { F _ { y } } ) = - 1 .
$$

7.曲线 $y = \ln ( 1 - x ^ { 2 } ) , x \in \left[ 0 , \frac { 1 } { 2 } \right]$ 的弧长为

【宝哥解答】

所求曲线的弧长为

$$
\begin{array} { l } { \displaystyle { \int _ { 0 } ^ { \frac 1 2 } \sqrt { \mathbf { j } + ( \frac { d y } { d x } ) ^ { 2 } } d x = \int _ { 0 } ^ { \frac 1 2 } \sqrt { 1 + ( - \frac { 2 x } { 1 - x ^ { 2 } } ) ^ { 2 } } d x = \int _ { 0 } ^ { \frac 1 2 } \frac { 1 + x ^ { 2 } } { 1 - x ^ { 2 } } d x = \int _ { 0 } ^ { \frac 1 2 } ( \frac { 2 } { 1 - x ^ { 2 } } - 1 ) d x } } \\ { \displaystyle { \quad \quad \quad } } \\ { \displaystyle { \quad \quad = \ln \frac { 1 + x } { 1 - x } \left| \frac { 1 } { 2 } - \frac { 1 } { 2 } = \ln 3 - \frac { 1 } { 2 } \right. } } \end{array} .
$$

8.设C是椭圆 $\frac { x ^ { 2 } } { a ^ { 2 } } + \frac { y ^ { 2 } } { b ^ { 2 } } = 1 ( a > 0 , b > 0 )$ ，则 $\oint _ { C } ( x ^ { 3 } + 2 y ) d x + ( 4 x - 3 y ^ { 2 } ) d y =$ 【宝哥解答】

C是椭圆 $\frac { x ^ { 2 } } { a ^ { 2 } } + \frac { y ^ { 2 } } { b ^ { 2 } } = 1 ( a > 0 , b > 0 )$ ，由格林公式，有

$$
\begin{array}{c} \begin{array} { l } { { \displaystyle \oint _ { c } ( x ^ { 3 } + 2 y ) d x + ( 4 x - 3 y ^ { 2 } ) d y = \left. \iint _ { \frac { x ^ { 2 } + y ^ { 2 } } { a ^ { 2 } + y ^ { 2 } } s ^ { 1 } } \left[ \frac { \partial ( 4 x - 3 y ^ { 2 } ) } { \partial x } - \frac { \partial ( x ^ { 3 } + 2 y ) } { \partial y } \right] d x d y \right.} } \\ { { = \displaystyle \iint _ { \frac { x ^ { 2 } } { a ^ { 2 } + y ^ { 2 } } s ^ { 1 } } 2 d x d y = 2 \pi a b } } \end{array}  .   \end{array}
$$

## 二.计算

1（5分）若 $\lambda > \frac { 1 } { 2 }$ ，计算函数

$$
f ( x , y ) = \left\{ \begin{array} { l l } { ( x ^ { 2 } + y ^ { 2 } ) ^ { \lambda } \sin \frac { 1 } { \sqrt { x ^ { 2 } + y ^ { 2 } } } , ( x , y ) \neq ( 0 , 0 ) } \\ { 0 , \ } & { ( x , y ) = ( 0 , 0 ) } \end{array} \right.
$$

在(0,0)的一阶偏导数 $f _ { \varepsilon } ( \pmb { \theta } , \pmb { 0 } )$ 和 ${ f _ { y } } ( 0 , 0 )$ 以及 $\operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } f ( x , y )$

【宝哥解答】

$\lambda > \frac { 1 } { 2 }$ ，故 $\operatorname* { l i m } _ { ( x , y )  ( 0 , 0 ) } ( x ^ { 2 } + y ^ { 2 } ) ^ { \lambda - \frac { 1 } { 2 } } = 0$ .对任意 $( x , y ) \neq ( 0 , 0 )$ ，有 $\left| \sin \frac { 1 } { \sqrt { x ^ { 2 } + y ^ { 2 } } } \right| \leq 1$ 故

$$
\operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } ( x ^ { 2 } + y ^ { 2 } ) ^ { \lambda - \frac { 1 } { 2 } } \sin \frac { 1 } { \sqrt { x ^ { 2 } + y ^ { 2 } } } = 0 .
$$

因此，

$$
\operatorname* { l i m } _ { ( x , y )  ( 0 , 0 ) } { \frac { f ( x , y ) - f ( 0 , 0 ) } { \sqrt { x ^ { 2 } + y ^ { 2 } } } } = \operatorname* { l i m } _ { ( x , y )  ( 0 , 0 ) } { \cfrac { ( x ^ { 2 } + y ^ { 2 } ) ^ { \lambda } \sin { \frac { 1 } { \sqrt { x ^ { 2 } + y ^ { 2 } } } } } { \sqrt { x ^ { 2 } + y ^ { 2 } } } }  .
$$

故

$$
f ( x , y ) - f ( 0 , 0 ) = 0 \cdot x + 0 \cdot y + o ( \sqrt { x ^ { 2 } + y ^ { 2 } } ) .
$$

由可微的定义， $\scriptstyle f ( x , y )$ 在(0,0)点可微，故 $\pmb { f } ( \pmb { x } , \pmb { y } )$ 在(0,0)点偏导数存在且均为0，$\pmb { f } ( \pmb { x } , \pmb { y } )$ 在(0,0)点连续，即

$$
f _ { x } ( 0 , 0 ) = f _ { y } ( 0 , 0 ) = 0 , \quad \operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } f ( x , y ) = f ( 0 , 0 ) = 0 .
$$

2.求幂级数 $\sum _ { n = 1 } ^ { \infty } { \frac { x ^ { n } } { \alpha ^ { n } + \beta ^ { n } } } \left( \alpha > 0 , \beta > 0 \right)$ 的收敛域.

【宝哥解答】

不妨设 $\beta \geq \alpha$ ，则幂级数 $\sum \limits _ { n = 1 } ^ { \infty } \frac { x ^ { n } } { \alpha ^ { n } + \beta ^ { n } }$ 的收敛半径为

$$
\operatorname* { l i m } _ { n \to \infty } \sqrt [ n ] { \alpha ^ { n } + \beta ^ { n } } = \operatorname* { m a x } ( \alpha , \beta ) = \beta .
$$

$\scriptstyle x = \pm \beta$ 时，

$$
| \frac { x ^ { n } } { \alpha ^ { n } + \beta ^ { n } } | = \frac { \beta ^ { n } } { \alpha ^ { n } + \beta ^ { n } } = \frac { 1 } { 1 + ( \frac { \alpha } { \beta } ) ^ { n } }  \{ \frac { 1 } { 2 } , \alpha < \beta  ,
$$

故 $\operatorname* { l i m } _ { n \to \infty } { \frac { x ^ { n } } { \alpha ^ { n } + \beta ^ { n } } } \neq 0$ ，故 $\sum \limits _ { n = 1 } ^ { \infty } \frac { x ^ { n } } { \alpha ^ { n } + \beta ^ { n } }$ 发散，故幂级数 $\sum _ { n = 1 } ^ { \infty } { \frac { x ^ { n } } { \alpha ^ { n } + \beta ^ { n } } }$ 的收敛域为

$$
( - \beta , \beta ) = \big ( - \operatorname* { m a x } ( \alpha , \beta ) , \operatorname* { m a x } ( \alpha , \beta ) \big ) .
$$

3.计算曲线积分 $\int _ { L } { \frac { d x + d y } { \left| x \right| + \left| y \right| } }$ ,其中L为由A(1,0)出发经由B(0,1)再到C(-1,0)连成的折线.

【宝哥解答】

L为由A(1,0)出发经由B(0,1)再到C(-1,0)连成的折线，其上的点都满足$\left. x \right. + \left. y \right. = 1$ .于是，

$$
\int _ { L } \frac { d x + d y } { \left| x \right| + \left| y \right| } = \int _ { L } d ( x + y ) = ( x + y ) \frac { \left| ( - 1 , 0 ) \right. } { \left| ( 1 , 0 ) \right. } = - 2 .
$$

4.设V是由椭球面 $\frac { x ^ { 2 } } { a ^ { 2 } } + \frac { y ^ { 2 } } { b ^ { 2 } } + \frac { z ^ { 2 } } { c ^ { 2 } } = 1 \left( a > 0 , b > 0 , c > 0 \right)$ 在第一卦限部分的切平面和三个坐标平面所围成的封闭区域的体积，求V取最小值时对应的切平面方程.【宝哥解答】

$F ( x , y , z ) = \frac { x ^ { 2 } } { a ^ { 2 } } + \frac { y ^ { 2 } } { b ^ { 2 } } + \frac { z ^ { 2 } } { c ^ { 2 } } - 1$ ，则 $F _ { x } = \frac { 2 x } { a ^ { 2 } } , F _ { y } = \frac { 2 y } { b ^ { 2 } } , F _ { z } = \frac { 2 z } { c ^ { 2 } }$ ，都是连续的.

任取椭球面 $\frac { x ^ { 2 } } { a ^ { 2 } } + \frac { y ^ { 2 } } { b ^ { 2 } } + \frac { z ^ { 2 } } { c ^ { 2 } } = 1$ 在第一卦限的一点 $( x _ { 0 } , y _ { 0 } , z _ { 0 } )$ ，则该点处的切平面方程为

$$
\frac { 2 x _ { 0 } } { a ^ { 2 } } ( x - x _ { 0 } ) + \frac { 2 y _ { 0 } } { b ^ { 2 } } ( y - y _ { 0 } ) + \frac { 2 z _ { 0 } } { c ^ { 2 } } ( z - z _ { 0 } ) = 0 \ ,
$$

即

$$
\frac { x _ { 0 } } { a ^ { 2 } } x + \frac { y _ { 0 } } { b ^ { 2 } } y + \frac { z _ { 0 } } { c ^ { 2 } } z = 1 .
$$

其在 $x , y , z$ 轴上的截距分别为 $\frac { a ^ { 2 } } { x _ { 0 } } , \frac { b ^ { 2 } } { y _ { 0 } } , \frac { c ^ { 2 } } { z _ { 0 } } > 0$ ，故该切平面与三个坐标面所围成的

$$
\begin{array} { l } { { \displaystyle { V = \frac { 1 } { 6 } \frac { a ^ { 2 } } { x _ { 0 } } \frac { b ^ { 2 } } { y _ { 0 } } \frac { c ^ { 2 } } { z _ { 0 } } = \frac { a b c } { 6 } \frac { 1 } { \frac { x _ { 0 } y _ { 0 } } { a } \frac { z _ { 0 } } { b } } = \frac { a b c } { 6 } \frac { 1 } { \sqrt { \frac { x _ { 0 } ^ { 2 } } { a ^ { 2 } } \frac { y _ { 0 } ^ { 2 } } { b ^ { 2 } } \frac { z _ { 0 } ^ { 2 } } { c ^ { 2 } } } } \stackrel { \ast \overrightarrow { { \lambda } } } { = } \frac { a b c } { 6 } \frac { 1 } { \sqrt { \frac { x _ { 0 } ^ { 2 } } { a ^ { 2 } } + \frac { y _ { 0 } ^ { 2 } } { b ^ { 2 } } + \frac { z _ { 0 } ^ { 2 } } { c ^ { 2 } } } } \stackrel { \ast \overrightarrow { { \lambda } } } { = } \left( \frac { 1 } { a ^ { 2 } } \frac { 1 } { b ^ { 2 } } \frac { z _ { 0 } ^ { 2 } } { 3 } + \frac { z _ { 0 } ^ { 2 } } { c ^ { 2 } } \right) ^ { 3 } } } }  \\ { { \displaystyle { \ } } } \\ { { \displaystyle { \ } { \qquad = \frac { a b c } { 6 } \frac { 1 } { \sqrt { ( \frac { 1 } { 3 } ) ^ { 3 } } } = \frac { 3 \sqrt { 3 } a b c } { 6 } = \frac { \sqrt { 3 } a b c } { 2 } } } } \end{array}
$$

由均值不等式取等号的条件可知上式取等号当且仅当 $\frac { x _ { 0 } ^ { 2 } } { a ^ { 2 } } = \frac { y _ { 0 } ^ { 2 } } { b ^ { 2 } } = \frac { z _ { 0 } ^ { 2 } } { c ^ { 2 } } = \frac { 1 } { 3 }$ ，即$x _ { 0 } = \frac { a } { \sqrt { 3 } } , y _ { 0 } = \frac { b } { \sqrt { 3 } } , z _ { 0 } = \frac { c } { \sqrt { 3 } }$ ，此时，相应的切平面方程为 $\frac { a } { \frac { \sqrt { 3 } } { a ^ { 2 } } } x + \frac { b } { b ^ { 2 } } y + \frac { c } { c ^ { 2 } } z = 1$ 即 $\frac { x } { a } + \frac { y } { b } + \frac { z } { c } = \sqrt { 3 }$

## 三.(3x10=30)

1.求出函数 $f ( x ) = ( x ^ { 2 } + x - 6 ) \left| x ^ { 3 } - 4 x \right|$ 的全部不可导点.

【宝哥解答】

$$
f ( x ) = ( x ^ { 2 } + x - 6 ) \left| x ^ { 3 } - 4 x \right| = ( x - 2 ) ( x + 3 ) \left| x ( x + 2 ) ( x - 2 ) \right| ,
$$

其不可导点只可能是 $\scriptstyle 0 , 2 , - 2$

$$
\begin{array} { l } { { f _ { \ast } ^ { \prime } ( 0 ) = \displaystyle \operatorname* { l i m } _ { x  0 ^ { \ast } } \frac { f ( x ) - f ( 0 ) } { x } = \displaystyle \operatorname* { l i m } _ { x  0 ^ { \ast } } \frac { ( x - 2 ) ( \mathcal { X } + 3 )  x ( x + 2 ) ( x - 2 )  } { x } \ : , } } \\ { { \displaystyle \quad \quad = - 2 4 \displaystyle \operatorname* { l i m } _ { x  0 ^ { \ast } } \frac {  \mathcal { X }  } { x } = - 2 4 \displaystyle \operatorname* { l i m } _ { x  0 ^ { \ast } } \frac { x } { x } = - 2 4 \ : \ :  } } \\ { { \displaystyle   f _ { - } ^ { \prime } ( 0 ) = \operatorname* { l i m } _ { x  0 ^ { \ast } } \frac { f ( x ) - f ( 0 ) } { x } = - 2 4 \displaystyle \operatorname* { l i m } _ { x  0 ^ { \ast } } \frac {  x  } { x } = - 2 4 \displaystyle \operatorname* { l i m } _ { x  0 ^ { \ast } } \frac { - x } { x } = 2 4 \ : . } } \end{array}
$$

f(0),f'(0)都存在而不相等，故x=0为不可导点.

$$
\operatorname* { l i m } _ { x  2 } \frac { f ( x ) - f ( 2 ) } { x - 2 } = \operatorname* { l i m } _ { x  2 } \frac { ( x - 2 ) ( x + 3 ) | x ( x + 2 ) ( x - 2 ) | } { x - 2 } = \operatorname* { l i m } _ { x  2 } ( \bar { x } + \ 3 ) \big \{ x ( x + 2 ) ( x - 2 ) \big | = 0 \ ,
$$

故f(x)在x=2可导.

$$
\begin{array} { l } { { f _ { + } ^ { \prime } ( - 2 ) = \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { f ( x ) - f ( - 2 ) } { x + 2 } = \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { ( x - 2 ) ( x + 3 ) \left| x ( x + 2 ) ( x - 2 ) \right| } { x + 2 } , } } \\ { { = - 3 2 \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { \left| x + 2 \right| } { x + 2 } = - 3 2 \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { x + 2 } { x + 2 } = - 3 2 } } \\ { { f _ { - } ^ { \prime } ( - 2 ) = \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { f ( x ) - f ( - 2 ) } { x + 2 } = \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { ( x - 2 ) ( x + 3 ) \left| x ( x + 2 ) ( x - 2 ) \right| } { x + 2 } } } \\ { { = - 3 2 \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { \left| x + 2 \right| } { x + 2 } = - 3 2 \displaystyle \operatorname* { l i m } _ { x \to ( - 2 ) ^ { * } } \frac { - x - 2 } { x + 2 } = 3 2 } } \end{array}
$$

宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线：宝哥15160699421或15659067618

$f _ { + } ^ { \prime } ( - 2 ) , f _ { - } ^ { \prime } ( - 2 )$ 都存在而不相等，故x=-2为不可导点.

2.给出函数列 $f _ { n } ( x ) = { \frac { x ( \ln n ) ^ { \mu } } { n ^ { x } } } ( n = 2 , 3 , 4 , \cdots )$ ，试问：当 $\pmb { \mu }$ 为何值时， $\{ f _ { n } ( x ) \}$ 在$[ 0 , + \infty )$ 上一致收敛.

【宝哥解答】

$$
\operatorname* { l i m } _ { n \to \infty } f _ { n } ( x ) = \operatorname* { l i m } _ { n \to \infty } { \frac { x ( \ln n ) ^ { \mu } } { n ^ { x } } } = 0 , \forall x \in [ 0 , + \infty ) .
$$

对每个正整数n>1, $f _ { n } ( x ) = { \frac { x ( \ln n ) ^ { \mu } } { n ^ { x } } }$ 都是 $[ 0 , + \infty )$ 上的非负连续函数，

$$
f _ { n } ^ { \prime } ( x ) = ( \ln n ) ^ { \mu } ( n ^ { - x } - x n ^ { - x } \ln n ) = ( \ln n ) ^ { \mu } n ^ { - x } ( 1 - x \ln n ) .
$$

$x < \frac { 1 } { \ln n }$ 时， $f _ { n } ^ { \prime } ( x ) > 0$ $x > \frac { 1 } { \ln n }$ 时， $f _ { n } ^ { \prime } ( x ) < 0$ ，故 $f _ { \kappa } ( \vec { x } )$ 在· $\scriptstyle x = { \frac { 1 } { \ln n } }$ 取得了最大值，为

$$
f _ { n } ( \frac { 1 } { \ln n } ) = \frac { \displaystyle \frac { 1 } { \ln n } ( \ln n ) ^ { \mu } } { n ^ { \frac { 1 } { \ln n } } } = \frac { \displaystyle \frac { 1 } { \ln n } ( \ln n ) ^ { \mu } } { n ^ { \log _ { n } \epsilon } } = \frac { ( \ln n ) ^ { \mu - 1 } } { e } .
$$

$\smash { \left\{ f _ { n } ( x ) \right\} }$ 在[0,+∞)上一致收敛当且仅当 $\operatorname* { l i m } _ { n  \infty } \operatorname* { s u p } _ { x \in [ 0 , + \infty ) } | f _ { n } ( x ) | = 0$ ，即 $\operatorname* { l i m } _ { n \to \infty } { \frac { ( \ln n ) ^ { \mu - 1 } } { e } } = 0$ 即 $\pmb { \mu } - 1 < 0$ ，即 $\mu { < } 1$

3.比较 $\int _ { - \infty } ^ { + \infty } \frac { \sin x } { x } d x$ 和 $\int _ { - \pi } ^ { \pi } { \frac { \sin { x } } { x } } d x$ 的大小，并给出证明

【宝哥解答】

$$
\begin{array} { l } { { \displaystyle { \int _ { - \infty } ^ { + \infty } \displaystyle \frac { \sin x } { x } d x = 2 \int _ { 0 } ^ { + \infty } \displaystyle \frac { \sin x } { x } d x } = 2 \sum _ { n = 0 } ^ { \infty } \int _ { n \pi } ^ { ( n + 1 ) \pi } \displaystyle { \frac { \sin x } { x } d x } = 2 \sum _ { n = 0 } ^ { \infty } \int _ { 0 } ^ { \pi } \displaystyle { \frac { \sin ( x + n \pi ) } { x + n \pi } d x } } } \\ { { = 2 \sum _ { n = 0 } ^ { \infty } ( - 1 ) ^ { n } \displaystyle \int _ { 0 } ^ { \pi } \displaystyle { \frac { \sin x } { x + n \pi } d x } } } \end{array} .
$$

令 $u _ { n } = \int _ { 0 } ^ { \pi } \frac { \sin { x } } { x + n \pi } d x , n = 0 , 1 , 2 , \cdots$ ，则其为严格单调递减趋于0的正数列.级数

$\sum _ { n = 0 } ^ { \infty } ( - 1 ) ^ { n } \int _ { 0 } ^ { \pi } { \frac { \sin x } { x + n \pi } } d x$ 首项为正，由莱布尼兹判别法的结论，有

$$
\int _ { - \infty } ^ { + \infty } \frac { \sin x } { x } d x = 2 \sum _ { n = 0 } ^ { \infty } ( - 1 ) ^ { n } \int _ { 0 } ^ { \pi } \frac { \sin x } { x + n \pi } d x < 2 \int _ { 0 } ^ { \pi } \frac { \sin x } { x } d x = \int _ { - \pi } ^ { \pi } \frac { \sin x } { x } d x .
$$

四.(5×10=50分)

1.若 $\pmb { c } \neq \pmb { 0 }$ ，利用函数极限的定义证明 $\operatorname* { l i m } _ { x \to c } { \frac { 1 } { x } } = { \frac { 1 } { c } }$

【宝哥解答】

我们在 $0 < | x - c | < \frac { 1 } { 2 } |$ c的范围内考虑问题.在此范围内，

$$
\left| \frac { 1 } { x } - \frac { 1 } { c } \right| = \left| \frac { x - c } { c x } \right| < \frac { \left| x - c \right| } { \frac { 1 } { 2 } c ^ { 2 } } .
$$

对任意 $\pmb \varepsilon > 0$ ，取 $\delta = \operatorname* { m i n } ( \frac { 1 } { 2 } | c | , \frac { 1 } { 2 } c ^ { 2 } \varepsilon )$ ，则 $0 < | x - c | < \delta$ 时，有 $\left| { \frac { 1 } { x } } - { \frac { 1 } { c } } \right| < \varepsilon$

故 $\operatorname* { l i m } _ { x \to c } { \frac { 1 } { x } } = { \frac { 1 } { c } }$

2.如果函数f(x)满足条件 $f ^ { \prime } ( 0 ) = 0$ 且 $f ^ { \prime \prime } ( x ) + \left[ f ^ { \prime } ( x ) \right] ^ { 2 } = x$ ，证明(0,f(0))是函数f(x)的拐点.

【宝哥解答】

函数f(x)满足条件f'(0)=0且 $f ^ { \prime \prime } ( x ) + \left[ f ^ { \prime } ( x ) \right] ^ { 2 } = \mathcal { X }$ ，因此， $f ^ { \prime \prime } ( 0 ) { = } 0$

$$
\frac { f ^ { \prime } ( x ) } { x } + \frac { \left[ f ^ { \prime } ( x ) \right] ^ { 2 } } { x } = 1 , x \neq 0 .
$$

$$
\operatorname * { l i m } _ { x \to 0 } { \frac { \left[ f ^ { \prime } ( x ) \right] ^ { 2 } } { x } } = \operatorname * { l i m } _ { x \to 0 } { \frac { f ^ { \prime } ( x ) \left[ f ^ { \prime } ( x ) - f ^ { \prime } ( 0 ) \right] } { x } } = f ^ { \prime } ( 0 ) f ^ { \prime \prime } ( 0 ) = 0 ,
$$

故 $\operatorname* { l i m } _ { x \to 0 } { \frac { f ^ { \prime \prime } ( x ) } { x } } = 1 > 0$ ，由极限的保不等式性，存在x=0的一个去心邻域

(-δ,0)U(0,δ)，在其中，恒有 $\frac { f ^ { \prime \prime } ( x ) } { x } > 0$ ，即 $f ^ { \prime } ( x ) > 0 , x \in ( 0 , \delta )$

宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线：宝哥15160699421或15659067618

$f ^ { \prime \prime } ( x ) < 0 , x \in ( - \delta , 0 )$ ，故 $\left( 0 , f ( 0 ) \right)$ 为函数f(x)的拐点.

3.设实常数 ${ \mathbf { } } _ { \pmb { a } , …714 tokens truncated…frac { 1 } { n } ) ^ { n + \beta }$ 对所有的正整数n成立，证明 $\pmb { \alpha }$ 的最大值为 $\alpha = \frac { 1 } { \ln 2 } - 1$ $\beta$ 的最小值为 $\beta = \frac { 1 } { 2 }$

【宝哥解答】

$( 1 + \frac { 1 } { n } ) ^ { n + \alpha } \leq e \leq ( 1 + \frac { 1 } { n } ) ^ { n + \beta }$ 等价于 $\ln ( 1 + \frac { 1 } { n } ) ^ { n + \alpha } \leq \ln e \leq \ln ( 1 + \frac { 1 } { n } ) ^ { n + \beta }$ ，即

$$
( n + \alpha ) \ln ( 1 + \frac { 1 } { n } ) \leq 1 \leq ( n + \beta ) \ln ( 1 + \frac { 1 } { n } ) \ ,
$$

即

$$
\alpha \leq \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \leq \beta ,
$$

即

$$
\alpha \leq \operatorname* { i n f } _ { n \in N ^ { \ast } } \left\{ \frac { 1 } { \ln ( 1 + \displaystyle \frac { 1 } { n } ) } - n \right\} , \beta \geq \operatorname* { s u p } _ { n \in N ^ { \ast } } \left\{ \frac { 1 } { \ln ( 1 + \displaystyle \frac { 1 } { n } ) } - n \right\} .
$$

$f ( x ) = { \frac { 1 } { \ln ( 1 + x ) } } - { \frac { 1 } { x } } , x > 0$ ，则

$$
{ \begin{array} { r l } & { f ^ { \prime } ( x ) = { \cfrac { 1 } { { x } ^ { 2 } } } - { \cfrac { 1 } { ( 1 + x ) \ln ^ { 2 } ( 1 + x ) } } = { \cfrac { ( 1 + x ) \ln ^ { 2 } ( 1 + x ) - x ^ { 2 } } { x ^ { 2 } ( 1 + x ) \ln ^ { 2 } ( 1 + x ) } } } \\ & { \qquad = { \cfrac { \ln ^ { 2 } ( 1 + x ) - { \cfrac { x ^ { 2 } } { 1 + x } } } { x ^ { 2 } \ln ^ { 2 } ( 1 + x ) } } = { \cfrac { \left[ \ln ( 1 + x ) - { \cfrac { x } { \sqrt { 1 + x } } } \right] \left[ \ln ( 1 + x ) + { \cfrac { x } { \sqrt { 1 + x } } } \right] } { x ^ { 2 } \ln ^ { 2 } ( 1 + x ) } } . } \end{array} }
$$

令 $g ( x ) = \ln ( 1 + x ) - { \frac { x } { \sqrt { 1 + x } } } , x \in [ 0 , + \infty )$ ，则 $g ( x )$ 连续，

$$
\begin{array} { r } { g ^ { \prime } ( x ) = \displaystyle \frac { 1 } { 1 + x } - \frac { \sqrt { 1 + x } - \frac { x } { 2 \sqrt { 1 + x } } } { 1 + x } = \displaystyle \frac { 1 } { 1 + x } - \frac { 2 + x } { 2 ( 1 + x ) ^ { \frac { 3 } { 2 } } } \quad \mathrm { ~ , ~ } } \\ { = \displaystyle \frac { 2 \sqrt { 1 + x } - ( 1 + x ) - 1 } { 2 ( 1 + x ) ^ { \frac { 3 } { 2 } } } = - \frac { ( \sqrt { 1 + x } - 1 ) ^ { 2 } } { 2 ( 1 + x ) ^ { \frac { 3 } { 2 } } } < 0 , x > 0 } \end{array}
$$

故 $g ( x ) ^ { \flat \alpha }$ 格单调递减，故

$$
g ( x ) < g ( 0 ) = 0 , x > 0 ,
$$

故

$$
f ^ { \prime } ( x ) < 0 , x > 0 .
$$

因此，f(x)严格单调递减，故 $\frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n = f ( \frac { 1 } { n } )$ 严格单调递增，故

$$
\begin{array} { c } { { \displaystyle \operatorname* { i n f } _ { n \in N ^ { * } } \left\{ \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \right\} = \frac { 1 } { \ln 2 } - 1 } , }  \\ { { \displaystyle \operatorname* { s u p } _ { n \in N ^ { * } } \left\{ \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \right\} = \operatorname* { l i m } _ { n \to \infty } \left[ \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \right] = \operatorname* { l i m } _ { n \to \infty } \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) \frac { 1 } { n } } = \operatorname* { l i m } _ { n \to \infty } \frac { 1 } { \frac { 1 } { n ^ { 2 } } } = \frac { 1 } { 2 } . } }  \end{array}
$$
## 杭州电子科技大学2021年数学分析真题解析

## 一.填空题(本大题共8小题，每小题5分，共40分)

$$
\operatorname* { l i m } _ { n  \infty } { \frac { n ^ { 2 } } { 2 ^ { n } } } = (
$$

【宝哥解答】

$$
\operatorname* { l i m } _ { n  \infty } { \frac { n ^ { 2 } } { 2 ^ { n } } } = 0 .
$$

2.设点(0,1)是曲线 $y = x ^ { 3 } + b x ^ { 2 } + 1$ 的拐点，则b=（【宝哥解答】

$$
y = x ^ { 3 } + b x ^ { 2 } + 1
$$

$$
y ^ { \prime \prime } ( 0 ) = \overline { { 0 , } }
$$

$$
2 b = 0
$$

$$
b = 0
$$

$$
\scriptstyle { \left\{ \begin{array} { l l } { x = a \cos ^ { 3 } t } \\ { y = a \sin ^ { 3 } t } \end{array} \right. }
$$

$$
\left. { \frac { d y } { d x } } \right| _ { t = { \frac { \pi } { 4 } } } = (
$$

【宝哥解答】

$$
\cfrac { d \gamma } { d x } = \frac { \cfrac { d t } { d t } } { \cfrac { d x } { d t } } = \frac { 3 a \sin ^ { 2 } t \cos t } { - 3 a \cos ^ { 2 } t \sin t } = - \tan t , \frac { d y } { d x } \bigg | _ { t = \frac { \pi } { 4 } } = - 1 .
$$

$$
y = x ( x - 1 ) ( 2 - x )
$$

$$
- \frac { 1 } { 4 } x ^ { 4 } + x ^ { 3 } - x ^ { 2 } + C
$$

曲线 $y = x ( x - 1 ) ( 2 - x )$ 与x轴交点的横坐标为0,1,2，在[0,1]上， $y \le 0$ ，在[1,2]上，  
$y \ge 0$ ，故曲线y=x(xD（2+x）与x轴围成的图形面积为$S = - \int _ { 0 } ^ { 1 } y d x + \int _ { 1 } ^ { 2 } y d x = - ( - \frac { 1 } { 4 } x ^ { 4 } + x ^ { 3 } - x ^ { 2 } ) \left| _ { 0 } + ( - \frac { 1 } { 4 } x ^ { 4 } + x ^ { 3 } - x ^ { 2 } ) \right| _ { 1 } ^ { 2 }$ $= \frac { 1 } { 4 } + \frac { 1 } { 4 } = \frac { 1 } { 2 }$

5.曲面 $e ^ { z } - z + x y = 3$ 在点P(2,1,0)处的切平面方程为(宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线： 91

## 【宝哥解答】

令 $F ( x , y , z ) = e ^ { z } - z + x y - 3$ ，则 $F _ { x } = y$ $F _ { y } = x$ $F _ { z } = e ^ { z } - 1$ 1，都是连续的， $F _ { x } ( 2 , 1 , 0 ) = 1$ $F _ { _ { y } } ( 2 , 1 , 0 ) = 2$ $F _ { z } ( 2 , 1 , 0 ) = 0$ ，故曲面 $e ^ { z } - z + x y = 3$ 在点 $P ( 2 , 1 , 0 )$ 处的切平面方程为 $x - 2 + 2 ( y - 1 ) = 0$ 即 $x + 2 y = 4$

6.设f（x)是周期为2的周期函数，且 $f ( x ) = \left\{ { \begin{array} { l l } { 2 , - 1 < x \leq 0 } \\ { x ^ { 3 } , 0 < x \leq 1 } \end{array} } \right.$ ，则f(x)的傅里叶级数 在x=1处收敛于（

## 【宝哥解答】

$f ( x ) = { \left\{ \begin{array} { l l } { 2 , - 1 < x \leq 0 } \\ { x ^ { 3 } , 0 < x \leq 1 } \end{array} \right. }$ 在[-1,1]上分段光滑，x=0为第一类间断点，故f(x)的傅里叶级数在[-1,1]的和函数为

<!-- image-->

故f(x)的傅里叶级数在x=1处收敛于 $\frac { 3 } { 2 }$

7.设f（u,v）为二元可微函数，若 $z = f ( x ^ { y } , y ^ { x } )$ ，则 $\frac { \partial z } { \partial x } = ($

## 【宝哥解答】

f（u,v）为二元可微函数， $z = f ( x ^ { y } , y ^ { x } ) _ {  }$ 由复合函数的求导法则，有$\frac { \partial z } { \partial x } = f _ { 1 } ^ { \prime } \frac { \partial x ^ { y } } { \partial x } + f _ { 2 } ^ { \prime } \frac { \partial y ^ { x } } { \partial x } = y x ^ { y - 1 } f _ { 1 } ^ { \prime } + y ^ { x } \ln y f _ { 2 } ^ { \prime } .$

8.设 $L : y = x ^ { 2 } ( 0 \leq x \leq \sqrt { 2 } ) ^ { 2 }$ 则 $\int _ { L } x d s = ($

## 【宝哥解答】

L $y = x ^ { 2 } ( 0 \leq x \leq \sqrt { 2 } )$ ，故

$$
\begin{array} { l } { \displaystyle \int _ { L } x d s = \int _ { 0 } ^ { \sqrt { 2 } } x \sqrt { 1 + ( \frac { d y } { d x } ) ^ { 2 } } d x = \int _ { 0 } ^ { \sqrt { 2 } } x \sqrt { 1 + ( 2 x ) ^ { 2 } } d x = \int _ { 0 } ^ { \sqrt { 2 } } x \sqrt { 1 + 4 x ^ { 2 } } d x } \\ { \displaystyle \qquad = \frac { 1 } { 8 } \int _ { 0 } ^ { \sqrt { 2 } } \sqrt { 1 + 4 x ^ { 2 } } d ( 1 + 4 x ^ { 2 } ) = \frac { 1 } { 8 } \times \frac { 2 } { 3 } ( 1 + 4 x ^ { 2 } ) ^ { \frac { 3 } { 2 } } \left| _ { 0 } ^ { \sqrt { 2 } } = \frac { 1 3 } { 6 } \right. } \end{array}
$$

二.计算题(本大题共4小题，共30分)

1.(本小题5分）求极 $\lim \limits _ { x  0 } \frac { \sqrt { x } } { 1 - e ^ { \sqrt { x } } }$

【宝哥解答】

$$
\operatorname* { l i m } _ { x \to 0 ^ { + } } { \frac { \sqrt { x } } { 1 - e ^ { \sqrt { x } } } } = \operatorname* { l i m } _ { x \to 0 ^ { + } } { \frac { \sqrt { x } } { - { \sqrt { x } } } } = - 1 .
$$

2.（本小题5分）计算积分 $\int _ { 0 } ^ { \frac { \pi } { 2 } } \frac { \cos x } { 1 + \sin ^ { 2 } x } d x$

【宝哥解答】

$$
\int _ { 0 } ^ { \frac { \pi } { 2 } } { \frac { \cos x } { 1 + \sin ^ { 2 } x } } d x = \int _ { 0 } ^ { \frac { \pi } { 2 } } { \frac { 1 } { 1 + \sin ^ { 2 } x } } d \sin x = \arctan \sin x \left| { \frac { \pi } { 2 } } = { \frac { \pi } { 4 } } \right|
$$

3.（本小题5分）求幂级数 $\sum _ { n = 1 } ^ { \infty } n x ^ { n - 1 }$ 的收敛域及和函数.

## 【宝哥解答】

$\operatorname* { l i m } _ { n \to \infty } { \frac { n } { n + 1 } } = 1$ ，且其在x=±1处通项都是无穷大量，幂级数的收敛半径为故其在x=±1处发散，故幂级数的收敛域为(-1,1). 2

在(-1,1)内，

$$
\sum _ { n = 1 } ^ { \infty } n x ^ { n - 1 } = \sum _ { n = 1 } ^ { \infty } ( x ^ { n } ) ^ { \prime } = ( \sum _ { n = 1 } ^ { \infty ^ { \infty } } x ^ { n } ) ^ { \prime } = ( \sum _ { n = 0 } ^ { \infty } x ^ { n } ) ^ { \prime } = ( \frac { 1 } { 1 - x } ) ^ { \prime } = \frac { 1 } { \left( 1 - x \right) ^ { 2 } } .
$$

## 【宝哥备注1】

本题见宝哥题解精粹第13讲4.4第一大题第2小题. 本题见玉可题册稍什习

4.（本小题10分）计算曲线积分 $\int _ { L } ( x ^ { 2 } + 3 y ) d x + ( y ^ { 2 } - x ) d y$ ，其中L为从点A(4,0)到点0（0,0）的上半圆周 $y = \sqrt { 4 x - x ^ { 2 } }$

【宝哥解答】

记L为有向直线段 $L _ { 1 }$ $\overrightarrow { O A }$ ，D为 $L , L _ { 1 }$ 围成的平面区域，则

$$
\int \limits _ { L _ { 1 } } ( x ^ { 2 } + 3 y ) d x + ( y ^ { 2 } - x ) d y = \int \limits _ { 0 } ^ { 4 } x ^ { 2 } d x = \frac { 6 4 } { 3 } .
$$

由格林公式，

$$
\begin{array} { l } { \displaystyle { \sum _ { i = 1 } ^ { s \setminus y } \int _ { L } ( x ^ { 2 } + 3 y ) d x \mathrm { t } + ( \widetilde { y } ^ { 2 } - x ) d y = ( \int _ { L \cup L _ { 1 } } - \int _ { L _ { 1 } } ) ( x ^ { 2 } + 3 y ) d x + ( y ^ { 2 } - x ) d y } } \\ { \displaystyle { = - \iint _ { L } \Big [ \frac { \widetilde { \partial } ( y ^ { 2 } - x ) } { \partial x } - \frac { \partial ( x ^ { 2 } + 3 y ) } { \partial y } \Big ] d x d y - \frac { 6 4 } { 3 } = - 4 \iint d x d y - \frac { 6 4 } { 3 } } } \\ { \displaystyle { = - 4 S ( D ) - \frac { 6 4 } { 3 } = - 4 \times \frac { 1 } { 2 } \pi \times 2 ^ { 2 } - \frac { 6 4 } { 3 } = - 8 \pi - \frac { 6 4 } { 3 } } } \end{array}
$$

## 三.综合题(本大题共3小题，每小题10分，共30分)

1.已知函数 $f ( x , y ) = { \sqrt { \left| x y \right| } }$

（1）求f（x,y）在点(0,0）处的偏导数 $f _ { x } ( 0 , 0 )$ 和 $f _ { \ast } ( 0 , \widetilde { 0 } )$

(2）讨论f（x,y）在点(0,0)处的可微性.

【宝哥解答】

$$
f _ { x } ( 0 , 0 ) = \operatorname* { l i m } _ { x \to 0 } { \frac { f ( x , 0 ) - f ( 0 , 0 ) } { x } } = \operatorname* { l i m } _ { x \to 0 } { \frac { 0 - 0 } { x } } = 0 ,
$$

$$
f _ { \boldsymbol { y } } ( 0 , 0 ) = \operatorname* { l i m } _ { \boldsymbol { y } \to 0 } \frac { \boldsymbol { f } ( 0 , \boldsymbol { y } ) - \boldsymbol { f } ( 0 , 0 ) } { \boldsymbol { y } } = \operatorname* { l i m } _ { \boldsymbol { y } \to 0 } \frac { 0 - 0 } { \boldsymbol { y } } = 0 ,
$$

对任意 $( x , y ) \neq ( 0 , 0 )$ $\frac { f ( x , y ) - f ( 0 , 0 ) - f _ { x } ( 0 , 0 ) x - f _ { y } ( 0 , 0 ) } { \sqrt { x ^ { 2 } + y ^ { 2 } } }$ ，取

$x = y \neq 0$ ，则 $\sqrt { \frac { \left| x y \right| } { x ^ { 2 } + y ^ { 2 } } } = \frac { 1 } { \sqrt { 2 } } \neq 0$ 故

$$
\operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } { \frac { f ( x , y ) \overset {  } { \sim } f ( \Theta , 0 ) - f _ { x } ( 0 , 0 ) x - f _ { y } ( 0 , 0 ) } { \sqrt { x ^ { 2 } + y ^ { 2 } } } } \neq 0 ,
$$

故 $f ( x , y )$ 在(0,0)点不可微。

【宝哥备注2】

2.讨论函数项级数 $\sum _ { n = 1 } ^ { \infty } { \frac { x ^ { 2 0 2 1 } } { e ^ { n x } } }$ 在 $[ 0 , + \infty )$ 上的一致收敛性.

【宝哥解答】

对每个正整数n，令 $f _ { n } ( x ) = { \frac { x ^ { 2 0 2 1 } } { e _ { \infty } ^ { m x } } } , x \in [ 0 , + \infty )$ ，则 $f _ { n } ( x )$ 非负连续，

$$
f _ { n } ^ { \prime } ( x ) = 2 0 2 1 x ^ { 2 0 2 0 } e ^ { - n x } - n e ^ { - n x } x ^ { 2 0 2 1 } = e ^ { - n x } x ^ { 2 0 2 0 } ( 2 0 2 1 - n x )
$$

$0 < x < \frac { 2 0 2 1 } { n }$ $\mathcal { F } _ { n } ^ { \prime } ( x ) > 0$ $x > \frac { 2 0 2 1 } { n }$ 时， $f _ { n } ^ { \prime } ( x ) < 0$ ，故 $f _ { n } ( x )$ 在 $x = \frac { 2 0 2 1 } { n }$ 取得了最大值

$$
f _ { n } ( \frac { 2 0 2 1 } { n } ) = \frac { ( \frac { 2 0 2 1 } { n } ) ^ { 2 0 2 1 } } { e ^ { \frac { 2 0 2 1 n } { n } } } = \frac { 2 0 2 1 ^ { 2 0 2 1 } } { e ^ { 2 0 2 1 } } \frac { 1 } { n ^ { 2 0 2 1 } } ,
$$

故

$$
0 \leq f _ { n } ( x ) \leq \frac { 2 0 2 1 ^ { 2 0 2 1 } } { e ^ { 2 0 2 1 } } \frac { 1 \leq 0 \leq n } { n ^ { 2 0 2 1 } } x ^ { \prime } \in [ 0 , + \infty ) , n \in N ^ { + }
$$

$\sum _ { n = 1 } ^ { \infty } { \frac { 1 } { n ^ { 2 0 2 1 } } }$ 收敛，故函数项级数 $\sum _ { n = 1 } ^ { \infty } { \frac { x ^ { 2 0 2 1 } } { e ^ { n x } } } = \sum _ { n = 1 } ^ { \infty } f _ { n } ( x )$ 在 $[ 0 , + \infty )$ 上一致收敛.

3.计算曲面积分 $\iint _ { \Sigma } { x z ^ { 2 } d y d z } + ( x ^ { 2 } y - z ^ { 2 } ) d z d x + ( 2 x y + y ^ { 2 } z ) d x d y$ ，其中Σ为上半球面$z = \sqrt { 1 - x ^ { 2 } - y ^ { 2 } }$ 的上侧

## 【宝哥解答】

取 $\Sigma _ { 1 }$ 为 $\left\{ { x ^ { 2 } } + { y ^ { 2 } } \leq 1 \right.$ 取下侧，Ω为 $\Sigma , \Sigma _ { 1 }$ 围成的立体，则

$$
\begin{array} { r l } & { \frac { \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle } { \partial t } \frac { \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle } { \partial t } } \\ & { \qquad \frac { \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle + \langle \mathcal { X } ( \mathbf { E } ^ { \prime } ) | | t \rangle + \langle \mathcal { X } ( \mathbf { E } ^ { \prime } ) | | t \rangle } { \partial t } } \\ & { \qquad \times \langle | t | \int _ { - \infty } ^ { \infty } \langle | t | \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle + \langle | t | \langle \mathbf { E } ^ { \prime } \rangle | | t \rangle } \\ & { \qquad \times \frac { \langle | t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \mathbf { E } ^ { \prime } | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle \rangle } { \partial t } \Big | t d \phi \rangle } \\ &  \qquad \times \Big [ \int _ { - \infty } ^ { \infty } \frac  \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \mathbf { E } ^ { \prime } | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) \end{array}
$$

## 四.（本大题共5小题，每小题10分，共50分）

1.设 $a > 0 , a _ { 1 } = \frac { 1 } { 2 } ( a + \frac { 1 } { a } ) , a _ { n + 1 } = \frac { 1 } { 2 } ( a _ { n } + \frac { 1 } { a _ { n } } ) , n = 1 , 2 , \cdots$ ，证明：数列 $\left\{ a _ { n } \right\}$ 收敛，并且 其极限为1.

## 【宝哥解答】

对任意x>0，由均值不等式，有（x
# 杭州电子科技大学

# 2020 年攻读硕士学位研究生招生考试

# 《数学分析》试题

（试题共四大题，共3页，总分150分）

姓名 报考专业 准考证号

【所有答案必须写在答题纸上，做在试卷或草稿纸上无效！】

## 一、填空题（本大题共8小题，每小题5分，共40分）

1. $\operatorname* { l i m } _ { n \to \infty } \left( { \frac { 1 } { n ^ { 2 } + n + 1 } } + { \frac { 2 } { n ^ { 2 } + n + 2 } } + { \frac { 3 } { n ^ { 2 } + n + 3 } } + \cdots + { \frac { n } { n ^ { 2 } + n + n } } \right) =$ （ ）.

2.设 $f ( x ) { = } \arctan x - { \frac { 1 } { 1 + a x ^ { 2 } } }$ ，且 $f ^ { \prime \prime } ( 0 ) = 2$ ，则a=（ ）.

3.设y=f(x)由方程 $y - \sin ( x y ) = e ^ { x ( 1 - y ) }$ 确定，则 $\operatorname* { l i m } _ { n \to \infty } n \left[ f \left( { \frac { 1 } { n } } \right) - 1 \right] = ($ ）.

4.曲线 $y = x ^ { 2 } + 2 \ln x$ 在其拐点处的切线方程为( ）.

5.已知 $f ( x ) = \int _ { 1 } ^ { x } { \sqrt { 1 + t ^ { 4 } } } d t$ 则 $\int _ { 0 } ^ { 1 } x ^ { 2 } f ( x ) d x =$ （ ）.

6.幂级数 $\sum _ { n = 1 } ^ { \infty } ( - 1 ) ^ { n - 1 } n x ^ { n - 1 }$ 在区间(-1,1)内的和函数 S(x)=（ ）.

7.对区域 $D { = } \left\{ ( x , y ) \vert x ^ { 2 } + y ^ { 2 } < 1 \right\}$ 内任意按段光滑曲线L，若曲线积分

$\int _ { L } { \frac { x d x - a y d y } { x ^ { 2 } + y ^ { 2 } - 1 } }$ 与路径无关，则a=（ ）.

8.设 $\Sigma = \left\{ ( x , y , z ) \left| x + y + z = 1 , x \geq 0 , y \geq 0 , z \geq 0 \right. \right\}$ ，则 $\iint _ { \Sigma } y ^ { 2 } d S = ($ ）.

## 二、计算题（本大题共5小题，每小题6分，共30分）

1．求极限 $\operatorname* { l i m } _ { x \to 0 } { \frac { \ln ( 1 + x ) ^ { \frac { 1 } { x } } - 1 } { \ln ( 1 + x ) } }$

2．计算积分 $\int _ { - 2 } ^ { 2 } \operatorname* { m i n } \left\{ { \frac { 1 } { \left| x \right| } } , x ^ { 2 } \right\} d x$ ,其中min表示取最小值.

3.设 $z = z ( x , y )$ 为方程 $f ( x - y , y - z , z - x ) = 0$ 所确定的隐函数，求 $\frac { \partial z } { \partial x } , \frac { \partial z } { \partial y }$ 和dz.

4.求函数 $f ( x ) = \arctan { \frac { 2 x } { 1 - x ^ { 2 } } }$ 在x=0处的幂级数展开式.

5.设区域 $D { = } \left\{ \left( x , y \right) \bigm | x ^ { 2 } + y ^ { 2 } \leq a x \right\}$ ，计算二重积分

$$
I = \iint _ { D } \Bigl ( x ^ { 3 } y ^ { 2 0 1 9 } + y ^ { 3 } \sqrt { x ^ { 2 0 2 0 } + y ^ { 2 0 2 0 } } + x \sqrt { x ^ { 2 } + y ^ { 2 } } \Bigr ) d x d y .
$$

## 三、综合题（本大题共3小题，每小题10分，共30分）

1.设 $f ( x ) = { \left\{ \begin{array} { l l } { | x | ^ { \alpha } \sin { \frac { 1 } { | x | } } , 0 < | x | \leq 1 , } \\ { 0 , \qquad x = 0 , } \end{array} \right. }$

(1）问α在什么条件下，f"(0)存在？并求此时f(0)的值.

(2）问α在什么条件下，f'(x)在[-1,1]上有界？

(3）问α在什么条件下，f"(x)在[-1,1]上连续？

2．求参数k取何值时，方程 $k x + \frac { 1 } { x ^ { 2 } } = 1$ 在 $x \in ( 0 , + \infty )$ 上有唯一解？

3.计算曲面积分 $I = \iint _ { \Sigma } \frac { a x d y d z + ( z + a ) ^ { 2 } d x d y } { \sqrt { x ^ { 2 } + y ^ { 2 } + z ^ { 2 } } }$ ，其中Σ为下半球面$z = - \sqrt { a ^ { 2 } - x ^ { 2 } - y ^ { 2 } }$ 的上侧，a>0为常数.

## 四、证明题（本大题共5小题，每小题10分，共 50分)

1.设 $\{ a _ { n } \}$ 是递增有界正数列.求证：级数 $\sum _ { n = 1 } ^ { \infty } \left( 1 - { \frac { a _ { n } } { a _ { n + 1 } } } \right)$ 收敛.

2.设 $f ( x ) = { \frac { x + 2 } { x + 1 } } \mathrm { s i n } { \frac { 1 } { x } } , a > 0$ 为常数.试证：f(x)在(0,a)内非一致连续，而在 [a,+∞)上一致连续.

3.设函数f(x)在区间[0,1]上连续，在开区间(0,1)内可导，且f(1)=0，证明：存在 $\xi \in ( 0 , 1 )$ ，使得 $f ( \xi ) + ( 1 - e ^ { - \xi } ) f ^ { \prime } ( \xi ) = 0$

4.确定函数 $g ( \alpha ) = \int _ { 0 } ^ { + \infty } { \frac { \ln ( 1 + x ^ { 3 } ) } { x ^ { \alpha } } } d x$ 的定义域，并证明g(α)在该定义域上连续.

5.设 $f ( x , y ) = { \left\{ \begin{array} { l l } { { \underline { { x } } } ^ { 3 } + y ^ { 3 } } \\ { { \overline { { x } } } ^ { 2 } + y ^ { 2 } } \\ { 0 , } \end{array} \right. } ( x , y ) \neq ( 0 , 0 )$

(1)证明f(x,y)在(0,0)处连续；(2）证明 $f ( x , y )$ 在(0,0)处不可微.

## tool · 2026-10-19T07:28:28Z


Script completed
Wall time 0.1 seconds
Output:

   249	四.(5×10=50分)
   250	
   251	1.若 $\pmb { c } \neq \pmb { 0 }$ ，利用函数极限的定义证明 $\operatorname* { l i m } _ { x \to c } { \frac { 1 } { x } } = { \frac { 1 } { c } }$
   252	
   253	【宝哥解答】
   254	
   255	我们在 $0 < | x - c | < \frac { 1 } { 2 } |$ c的范围内考虑问题.在此范围内，
   256	
   257	$$
   258	\left| \frac { 1 } { x } - \frac { 1 } { c } \right| = \left| \frac { x - c } { c x } \right| < \frac { \left| x - c \right| } { \frac { 1 } { 2 } c ^ { 2 } } .
   259	$$
   260	
   261	对任意 $\pmb \varepsilon > 0$ ，取 $\delta = \operatorname* { m i n } ( \frac { 1 } { 2 } | c | , \frac { 1 } { 2 } c ^ { 2 } \varepsilon )$ ，则 $0 < | x - c | < \delta$ 时，有 $\left| { \frac { 1 } { x } } - { \frac { 1 } { c } } \right| < \varepsilon$
   262	
   263	故 $\operatorname* { l i m } _ { x \to c } { \frac { 1 } { x } } = { \frac { 1 } { c } }$
   264	
   265	2.如果函数f(x)满足条件 $f ^ { \prime } ( 0 ) = 0$ 且 $f ^ { \prime \prime } ( x ) + \left[ f ^ { \prime } ( x ) \right] ^ { 2 } = x$ ，证明(0,f(0))是函数f(x)的拐点.
   266	
   267	【宝哥解答】
   268	
   269	函数f(x)满足条件f'(0)=0且 $f ^ { \prime \prime } ( x ) + \left[ f ^ { \prime } ( x ) \right] ^ { 2 } = \mathcal { X }$ ，因此， $f ^ { \prime \prime } ( 0 ) { = } 0$
   270	
   271	$$
   272	\frac { f ^ { \prime } ( x ) } { x } + \frac { \left[ f ^ { \prime } ( x ) \right] ^ { 2 } } { x } = 1 , x \neq 0 .
   273	$$
   274	
   275	$$
   276	\operatorname * { l i m } _ { x \to 0 } { \frac { \left[ f ^ { \prime } ( x ) \right] ^ { 2 } } { x } } = \operatorname * { l i m } _ { x \to 0 } { \frac { f ^ { \prime } ( x ) \left[ f ^ { \prime } ( x ) - f ^ { \prime } ( 0 ) \right] } { x } } = f ^ { \prime } ( 0 ) f ^ { \prime \prime } ( 0 ) = 0 ,
   277	$$
   278	
   279	故 $\operatorname* { l i m } _ { x \to 0 } { \frac { f ^ { \prime \prime } ( x ) } { x } } = 1 > 0$ ，由极限的保不等式性，存在x=0的一个去心邻域
   280	
   281	(-δ,0)U(0,δ)，在其中，恒有 $\frac { f ^ { \prime \prime } ( x ) } { x } > 0$ ，即 $f ^ { \prime } ( x ) > 0 , x \in ( 0 , \delta )$
   282	
   283	宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线：宝哥15160699421或15659067618
   284	
   285	$f ^ { \prime \prime } ( x ) < 0 , x \in ( - \delta , 0 )$ ，故 $\left( 0 , f ( 0 ) \right)$ 为函数f(x)的拐点.
   286	
   287	3.设实常数 ${ \mathbf { } } _ { \pmb { a } , { \pmb { b } } }$ 不同时为零，利用二重积分换元法证明
   288	
   289	$$
   290	\iint _ { x ^ { 1 } + y ^ { 2 } \leq 1 } f ( a x + b y ) d x d y = 2 \int _ { - 1 } ^ { 1 } \sqrt { 1 - y ^ { 2 } } f ( \sqrt { a ^ { 2 } + b ^ { 2 } } u ) d u .
   291	$$
   292	
   293	【宝哥解答】
   294	
   295	实常数 $^ { a , \tilde { b } }$ 不同时为零，作正交变换 ${ \binom { u } { \nu } } = { \left( \begin{array} { l l } { \frac { a } { { \sqrt { a ^ { 2 } + b ^ { 2 } } } } } & { \frac { b } { { \sqrt { a ^ { 2 } + b ^ { 2 } } } } } \\ { \frac { b } { { \sqrt { a ^ { 2 } + b ^ { 2 } } } } } & { - \frac { a } { { \sqrt { a ^ { 2 } + b ^ { 2 } } } } } \end{array} \right) } { \left( \begin{array} { l } { x } \\ { y } \end{array} \right) }$ 则 $u = \frac { a x + b y } { \sqrt { a ^ { 2 } + b ^ { 2 } } }$ ，故 $a x + b y = \sqrt { a ^ { 2 } + b ^ { 2 } } u$ ，因此，
   296	
   297	$$
   298	\begin{array} { l } { { \displaystyle \iint _ { x ^ { 2 } + y ^ { 2 } \le 1 } f ( a x + b y ) d x d y = \displaystyle \iint _ { u ^ { 2 } + y ^ { 2 } \le 1 } f ( \sqrt { { a } ^ { 2 } + { b } ^ { 2 } } u ) d u d \nu } } \\ { { \displaystyle = \int _ { - 1 } ^ { 1 } f ( \sqrt { { a } ^ { 2 } + { b } ^ { 2 } } u ) d u \int _ { - \sqrt { 1 - u ^ { 2 } } } ^ { \sqrt { 1 - u ^ { 2 } } } d \nu \equiv 2 \displaystyle \int _ { - 1 } ^ { 1 } \sqrt { 1 - u ^ { 2 } } f ( \sqrt { { a } ^ { 2 } + { b } ^ { 2 } } u ) d u } } .  \end{array} .
   299	$$
   300	
   301	4.设函数f(x)在 $\left[ a , b \right] \left( b > a > 0 \right)$ 上连续，在(a,b)上可导且 $f ( a ) \neq f ( b )$ .证明：存在 $\xi , \eta \in ( a , b )$ ，使得
   302	
   303	$$
   304	f ^ { \prime } ( \xi ) = ( a + b ) ( a ^ { 2 } + b ^ { 2 } ) \frac { f ^ { \prime } ( \eta ) } { 4 \eta ^ { 3 } } .
   305	$$
   306	
   307	【宝哥解答】
   308	
   309	$g ( x ) = x ^ { 4 } , x \in [ a , b ]$ ，则 $g ( x )$ 在 $[ a , b ]$ 上连续，在 $( a , b )$ 内可导．由于 ${ \pmb b } > { \pmb a } > { \pmb 0 }$ 故 $g ^ { \prime } ( x ) = 4 x ^ { 3 } > 0 , x \in ( a , b )$ ．由柯西中值定理，存在 $\pmb { \eta } \in ( a , b )$ ，使得
   310	
   311	$$
   312	\frac { f ( b ) - f ( a ) } { ( b - a ) ( a + b ) ( a ^ { 2 } + b ^ { 2 } ) } = \frac { f ( b ) - f ( a ) } { b ^ { 4 } - a ^ { 4 } } = \frac { f ( b ) - f ( a ) } { g ( b ) - g ( a ) } = \frac { f ^ { \prime } ( \eta ) } { g ^ { \prime } ( \eta ) } = \frac { f ^ { \prime } ( \eta ) } { 4 \eta ^ { 3 } } .
   313	$$
   314	
   315	由拉格朗日中值定理，存在 $\xi \in ( a , b )$ ，使得
   316	
   317	$$
   318	{ \frac { f ( b ) - f ( a ) } { b - a } } = f ^ { \prime } ( \xi ) ,
   319	$$
   320	
   321	因此，
   322	
   323	$$
   324	{ \frac { f ^ { \prime } ( \xi ) } { ( a + b ) ( a ^ { 2 } + b ^ { 2 } ) } } = { \frac { f ^ { \prime } ( \eta ) } { 4 \eta ^ { 3 } } } ,
   325	$$
   326	
   327	故
   328	
   329	$$
   330	f ^ { \prime } ( \xi ) = ( a + b ) ( a ^ { 2 } + b ^ { 2 } ) \frac { f ^ { \prime } ( \eta ) } { 4 \eta ^ { 3 } } .
   331	$$
   332	
   333	5.若两个正数α和 $\beta$ 使得不等式 $( 1 + \frac { 1 } { n } ) ^ { n + \alpha } \leq e \leq ( 1 + \frac { 1 } { n } ) ^ { n + \beta }$ 对所有的正整数n成立，证明 $\pmb { \alpha }$ 的最大值为 $\alpha = \frac { 1 } { \ln 2 } - 1$ $\beta$ 的最小值为 $\beta = \frac { 1 } { 2 }$
   334	
   335	【宝哥解答】
   336	
   337	$( 1 + \frac { 1 } { n } ) ^ { n + \alpha } \leq e \leq ( 1 + \frac { 1 } { n } ) ^ { n + \beta }$ 等价于 $\ln ( 1 + \frac { 1 } { n } ) ^ { n + \alpha } \leq \ln e \leq \ln ( 1 + \frac { 1 } { n } ) ^ { n + \beta }$ ，即
   338	
   339	$$
   340	( n + \alpha ) \ln ( 1 + \frac { 1 } { n } ) \leq 1 \leq ( n + \beta ) \ln ( 1 + \frac { 1 } { n } ) \ ,
   341	$$
   342	
   343	即
   344	
   345	$$
   346	\alpha \leq \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \leq \beta ,
   347	$$
   348	
   349	即
   350	
   351	$$
   352	\alpha \leq \operatorname* { i n f } _ { n \in N ^ { \ast } } \left\{ \frac { 1 } { \ln ( 1 + \displaystyle \frac { 1 } { n } ) } - n \right\} , \beta \geq \operatorname* { s u p } _ { n \in N ^ { \ast } } \left\{ \frac { 1 } { \ln ( 1 + \displaystyle \frac { 1 } { n } ) } - n \right\} .
   353	$$
   354	
   355	$f ( x ) = { \frac { 1 } { \ln ( 1 + x ) } } - { \frac { 1 } { x } } , x > 0$ ，则
   356	
   357	$$
   358	{ \begin{array} { r l } & { f ^ { \prime } ( x ) = { \cfrac { 1 } { { x } ^ { 2 } } } - { \cfrac { 1 } { ( 1 + x ) \ln ^ { 2 } ( 1 + x ) } } = { \cfrac { ( 1 + x ) \ln ^ { 2 } ( 1 + x ) - x ^ { 2 } } { x ^ { 2 } ( 1 + x ) \ln ^ { 2 } ( 1 + x ) } } } \\ & { \qquad = { \cfrac { \ln ^ { 2 } ( 1 + x ) - { \cfrac { x ^ { 2 } } { 1 + x } } } { x ^ { 2 } \ln ^ { 2 } ( 1 + x ) } } = { \cfrac { \left[ \ln ( 1 + x ) - { \cfrac { x } { \sqrt { 1 + x } } } \right] \left[ \ln ( 1 + x ) + { \cfrac { x } { \sqrt { 1 + x } } } \right] } { x ^ { 2 } \ln ^ { 2 } ( 1 + x ) } } . } \end{array} }
   359	$$
   360	
   361	令 $g ( x ) = \ln ( 1 + x ) - { \frac { x } { \sqrt { 1 + x } } } , x \in [ 0 , + \infty )$ ，则 $g ( x )$ 连续，
   362	
   363	$$
   364	\begin{array} { r } { g ^ { \prime } ( x ) = \displaystyle \frac { 1 } { 1 + x } - \frac { \sqrt { 1 + x } - \frac { x } { 2 \sqrt { 1 + x } } } { 1 + x } = \displaystyle \frac { 1 } { 1 + x } - \frac { 2 + x } { 2 ( 1 + x ) ^ { \frac { 3 } { 2 } } } \quad \mathrm { ~ , ~ } } \\ { = \displaystyle \frac { 2 \sqrt { 1 + x } - ( 1 + x ) - 1 } { 2 ( 1 + x ) ^ { \frac { 3 } { 2 } } } = - \frac { ( \sqrt { 1 + x } - 1 ) ^ { 2 } } { 2 ( 1 + x ) ^ { \frac { 3 } { 2 } } } < 0 , x > 0 } \end{array}
   365	$$
   366	
   367	故 $g ( x ) ^ { \flat \alpha }$ 格单调递减，故
   368	
   369	$$
   370	g ( x ) < g ( 0 ) = 0 , x > 0 ,
   371	$$
   372	
   373	故
   374	
   375	$$
   376	f ^ { \prime } ( x ) < 0 , x > 0 .
   377	$$
   378	
   379	因此，f(x)严格单调递减，故 $\frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n = f ( \frac { 1 } { n } )$ 严格单调递增，故
   380	
   381	$$
   382	\begin{array} { c } { { \displaystyle \operatorname* { i n f } _ { n \in N ^ { * } } \left\{ \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \right\} = \frac { 1 } { \ln 2 } - 1 } , }  \\ { { \displaystyle \operatorname* { s u p } _ { n \in N ^ { * } } \left\{ \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \right\} = \operatorname* { l i m } _ { n \to \infty } \left[ \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) } - n \right] = \operatorname* { l i m } _ { n \to \infty } \frac { 1 } { \ln ( 1 + \frac { 1 } { n } ) \frac { 1 } { n } } = \operatorname* { l i m } _ { n \to \infty } \frac { 1 } { \frac { 1 } { n ^ { 2 } } } = \frac { 1 } { 2 } . } }  \end{array}
   383	$$# 杭州电子科技大学

# 2019年攻读硕士学位研究生招生考试

# 《数学分析》试题

（试题共4大题，共2页，总分150分）

姓名 报考专业 准考证号

【所有答案必须写在答题纸上，做在试卷或草稿纸上无效！】

## 一、填空题（本大题共8小题，每小题5分，本大题共40分）

1.极限 $\operatorname* { l i m } _ { n \to \infty } \left( { \frac { 1 } { n + { \sqrt { 1 } } } } + { \frac { 1 } { n + { \sqrt { 2 } } } } + \cdots + { \frac { 1 } { n + { \sqrt { n } } } } \right) = ($ ）.

2.设g(0)=g'(0)=0, $f ( x ) = { \left\{ \begin{array} { l l } { g ( x ) \sin { \frac { 1 } { x } } , } & { x \neq 0 } \\ { 0 , } & { x = 0 } \end{array} \right. }$ ，则f(0)=（ ）.

3.曲线 $L \left\{ { x = 1 - t ^ { 2 } } \right.$ 在t=1所对应点处的法线方程为（ ）.

4.曲线 $y = x ^ { 4 } - 6 x ^ { 3 } + 1 2 x ^ { 2 } - x + 1$ 的拐点有（ ）.

5．设连续函数f(x)满足 $2 f ( x ) + x = 1 + \int _ { 0 } ^ { 1 } f ( x ) d x$ ，则 $\int _ { 0 } ^ { 1 } f ( x ) d x = ($ ）.

6.设 $F ( y ) = \int _ { y } ^ { y ^ { 2 } } \frac { \sin ( x y ) } { x } d x .$ 则F(y)=（ ）.

7．设f(x,y)连续，则累次积分 $\int _ { 1 } ^ { e ^ { 2 } } d y \int _ { \mathrm { \scriptsize ~ l n y } } ^ { 2 } f ( x , y ) d x$ 交换积分次序后的表达式为（ ）

8.若L为圆周 $\left\{ { \begin{array} { l } { x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = a ^ { 2 } } \\ { x + y + z = 0 } \end{array} } \right.$ ，则曲线积分 $\int _ { L } ( 2 x ^ { 2 } + y ^ { 2 } + 2 x + y + 1 ) d s =$ （ ）：

## 二、计算题（本大题共5小题，每小题6分，本大题共30分）

1．求极限值 $\operatorname* { l i m } _ { x  0 ^ { + } } ( { \frac { \sin x } { x } } ) ^ { \frac { 1 } { x ^ { 2 } } }$

2.设y=y(x)为 $y = - y e ^ { x } + 2 e ^ { y } \sin x + 2 x$ 所确定的可导函数．求y(0).

3.设 $f ( x ) = \left\{ { \begin{array} { l l } { x e ^ { - x ^ { 2 } } , } & { x \geq 0 } \\ { 0 , } & { x < 0 } \end{array} } \right.$ ，求 $\int _ { 1 } ^ { x } f ( u - 1 ) d u$ 的表达式.

4.求级数 $\sum _ { n = 1 } ^ { \infty } n \cdot \frac { 2 ^ { \frac { n } { 2 } } } { 3 ^ { n } }$ 的和.

5.计算 $\iint _ { D } ( x + y + 1 ) ^ { 2 } d x d y ,$ 其中 $D = \{ ( x , y ) | 1 \leq x ^ { 2 } + y ^ { 2 } \leq 4 \}$

## 三、综合题（本大题共3题，每题10分，本大题共30分)

1.求a的值，使得 $f ( x , y ) = \left\{ \begin{array} { l l } { { ( x ^ { 2 } + y ^ { 2 } ) ^ { a } \cos \frac { 1 } { \left| x \right| + \left| y \right| } , } } & { { ( x , y ) \neq ( 0 , 0 ) } } \\ { { 0 , } } & { { ( x , y ) = ( 0 , 0 ) } } \end{array} \right.$ 在点(0,0)可微.

2．讨论级数 $\sum _ { n = 1 } ^ { \infty } { \frac { ( x + 1 ) ^ { n } } { ( n + 1 ) 2 ^ { n } } }$ 的敛散性（何时绝对收敛、何时条件收敛及何时发散）.

3．计算曲线积分 $\int _ { L } { \frac { ( e ^ { x } - 2 x y ) d x - ( x ^ { 2 } + y ^ { 2 } ) d y } { ( x - 1 ) ^ { 2 } + y ^ { 2 } } }$ ，其中L是在圆周 $y = \sqrt { 2 x - x ^ { 2 } }$ 上由点O(0,0)到点A(1,1)的一段弧.

## 四、证明题（本大题共5题，每题10分，本大题共50分）

1．设连续函数f(x)在[1,+∞)上为正值，且单调递减．令 $a _ { n } = \sum _ { i = 1 } ^ { n } f ( i ) - \int _ { 1 } ^ { n } f ( x ) d x$ 证明 $\{ a _ { n } \}$ 收敛.

2．设函数f(x)在区间[a,b]上二阶可导，曲线y=f(x)与过点 $A ( a , f ( a ) )$ 和点$B ( b , f ( b ) )$ 的直线相交于一点 $C ( c , f ( c ) )$ ，其中 $a < c < b$ ．试证：（1）至少存在一点 $\xi _ { 1 } \in ( a , c )$ 及一点 $\xi _ { 2 } \in ( c , b )$ ，使得 $f ^ { \prime } ( { \boldsymbol { \xi } } _ { 1 } ) = f ^ { \prime } ( { \boldsymbol { \xi } } _ { 2 } )$ ；（2）至少存在一点 $\xi \in ( a , b )$ ,使得 $f ^ { \prime } ( \xi ) = 0$

3．设1<a<b．证明函数 $F ( x ) = \int _ { e } ^ { + \infty } { \frac { \cos t } { t ^ { x } } } d t$ 在[a,b]连续且可微.

4.设 $\sum _ { i = 1 } ^ { \infty } a _ { n }$ 绝对收敛，证明 $\sum _ { i = 1 } ^ { \infty } a _ { n } ( a _ { 1 } + a _ { 2 } + \cdots + a _ { n } )$ 也绝对收敛.

5．设R>0，Ω为曲面 $z = R ^ { 2 } - x ^ { 2 } - y ^ { 2 }$ 与平面z=0所围成的空间闭区域，Σ为Ω表面的外侧，V为Ω的体积．证明 $\iint x ^ { 2 } y e ^ { \sin z } d y d z - x y ^ { 2 } e ^ { \sin z } d x d z + z ( 1 + 2 x y z ) d x d y = V$## 杭州电子科技大学2022年数学分析真题

## 一.填空题(5×8=40分)

1. $\operatorname* { l i m } _ { n \to \infty } ( 1 + { \frac { 1 } { 2 } } + \cdots + { \frac { 1 } { n } } ) =$

2. $( x ^ { 2 } e ^ { - 2 x } ) ^ { ( n ) }$

3.设 $0 < k < \frac { 1 } { e }$ ，方程 $\ln x - k x = 0$ 在 $( 0 , + \infty )$ 内根的个数为

4. $\int \frac { e ^ { x } - e ^ { - x } } { e ^ { x } + e ^ { - x } } d x =$

5.若正项级数 $\sum _ { n = 1 } ^ { \infty } u _ { n }$ 收敛且所有项 $u _ { n } \leq 3$ ，则级数 $\sum _ { n = 1 } ^ { \infty } \frac { u _ { n } } { \pi - u _ { n } }$ 是否收敛？

6.给定方程 $F ( x , y , z ) = 0$ ，则 $\frac { \partial z } { \partial x } \frac { \partial x } { \partial y } \frac { \partial y } { \partial z } =$

7.曲线 $y = \ln ( 1 - x ^ { 2 } ) , x \in \left[ 0 , \frac { 1 } { 2 } \right]$ 的弧长为

8.设C是椭圆 $\frac { x ^ { 2 } } { a ^ { 2 } } + \frac { y ^ { 2 } } { b ^ { 2 } } = 1 ( a > 0 , b > 0 )$ ，则 $\oint _ { C } ( x ^ { 3 } + 2 y ) d x + ( 4 x - 3 y ^ { 2 } ) d y =$

## 二.计算

1（5分）若 $\lambda > \frac { 1 } { 2 }$ ，钞算函数

$$
f ( x , y ) = \left\{ \begin{array} { l l } { \displaystyle ( x ^ { 2 } + y ^ { 2 } ) ^ { \lambda } \sin \frac { 1 } { \sqrt { x ^ { 2 } + y ^ { 2 } } } , ( x , y ) \neq ( 0 , 0 ) } \\ { 0 , } & { ( x , y ) = ( 0 , 0 ) } \end{array} \right.
$$

在(0,0)的一阶偏导数 $f _ { \mathrm { x } } ( 0 , 0 )$ 和 $f _ { y } ( 0 , 0 )$ 以及 $\operatorname* { l i m } _ { ( x , y ) \to ( 0 , 0 ) } f ( x , y )$

2.求幂级数 $\sum _ { n = 1 } ^ { \infty } { \frac { x ^ { n } } { \alpha ^ { n } + \beta ^ { n } } } ( \alpha > 0 , \beta > 0 )$ 的收敛域.

3.计算曲线积分 $\int _ { L } { \frac { d x + d y } { \left| x \right| + \left| y \right| } }$ ，其中L为由A(1,0)出发经由B(0,1)再到C(-1,0)连成的

折线.

4.设V是由椭球面 $\frac { x ^ { 2 } } { a ^ { 2 } } + \frac { y ^ { 2 } } { b ^ { 2 } } + \frac { z ^ { 2 } } { c ^ { 2 } } = 1 \left( a > 0 , b > 0 , c > 0 \right)$ 在第一卦限部分的切平面和三个坐标平面所围成的封闭区域的体积，求V取最小值时对应的切平面方程.三.(3x10= 30)

1.求出函数 $f ( x ) = ( x ^ { 2 } + x - 6 ) \left| x ^ { 3 } - 4 x \right|$ 的全部不可导点.

2.给出函数列 $f _ { n } ( x ) = { \frac { x ( \ln n ) ^ { \mu } } { n ^ { x } } } ( n = 2 , 3 , 4 , \cdots )$ ，试问：当μ为何值时， $\{ f _ { n } ( x ) \}$ 在$[ 0 , + \infty )$ 上一致收敛.

3.比较 $\int _ { - \infty } ^ { + \infty } { \frac { \sin { x } } { x } }$ dx和 $\int _ { - \pi } ^ { \pi } { \frac { \sin { x } } { x } } d x$ 的大小，并给出证明.

四.(5.×10=50分)

1.若c≠0，利用函数极限的定义证明 $\operatorname* { l i m } _ { \stackrel { . . . } { x }  \epsilon } \frac { 1 } { x } = \frac { 1 } { e }$

2.如果函数f(x)满足条件f'(0)=0且 $f ^ { \prime } ( x ) + \left[ f ^ { \prime } ( x ) \right] ^ { 2 } = x$ ，证明(0,f(0))是函数f(x)的拐点.

3.设实常数a,b不同时为零，利用二重积分换元法证明

$$
\underset { x ^ { 2 } + y ^ { 2 } \leq 1 } { \iint } f ( a x \neq b y ) d x d y = 2 \int _ { - 1 } ^ { 1 } \sqrt { 1 - u ^ { 2 } } f ( \sqrt { a ^ { 2 } + b ^ { 2 } } u ) d u .
$$

4.设函数f（x）在 $\left[ a , b \right] \left( b > a > 0 \right)$ 上连续，在(a,b)上可导且 $f ( a ) \neq f ( b )$ .证明：存在 $5 , 1 7 \in ( a , b )$ ，使得

$$
f ^ { \prime } ( \xi ) = ( a + b ) ( a ^ { 2 } + b ^ { 2 } ) \frac { f ^ { \prime } ( \eta ) } { 4 \eta ^ { 3 } } .
$$

5.若两个正数α和β使得不等式 $( 1 + \frac { 1 } { n } ) ^ { n + \alpha } \leq e \leq ( 1 + \frac { 1 } { n } ) ^ { n + \beta }$ 对所有的正整数n成立，证明α的最大值为 $\alpha = \frac { 1 } { \ln 2 } - 1$ ，β的最小值为 $\beta = \frac { 1 } { 2 }$

## tool · 2026-10-19T07:29:12Z




## tool · 2026-10-19T07:30:05Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"key":"2018","blocks":13,"bytes":9982}

## tool · 2026-10-19T07:31:14Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"key":"9e64c36cdac10429","blocks":13,"chars":8100}

## tool · 2026-10-19T07:32:43Z


Script completed
Wall time 0.6 seconds
Output:

{}
{"key":"918271f5178ca024","blocks":17,"chars":9771}

## tool · 2026-10-19T07:33:01Z


Script completed
Wall time 0.2 seconds
Output:

   198	取 $\Sigma _ { 1 }$ 为 $\left\{ { x ^ { 2 } } + { y ^ { 2 } } \leq 1 \right.$ 取下侧，Ω为 $\Sigma , \Sigma _ { 1 }$ 围成的立体，则
   199	
   200	$$
   201	\begin{array} { r l } & { \frac { \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle } { \partial t } \frac { \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle } { \partial t } } \\ & { \qquad \frac { \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle + \langle \mathcal { X } ( \mathbf { E } ^ { \prime } ) | | t \rangle + \langle \mathcal { X } ( \mathbf { E } ^ { \prime } ) | | t \rangle } { \partial t } } \\ & { \qquad \times \langle | t | \int _ { - \infty } ^ { \infty } \langle | t | \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle + \langle | t | \langle \mathbf { E } ^ { \prime } \rangle | | t \rangle } \\ & { \qquad \times \frac { \langle | t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \mathbf { E } ^ { \prime } | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle \rangle } { \partial t } \Big | t d \phi \rangle } \\ &  \qquad \times \Big [ \int _ { - \infty } ^ { \infty } \frac  \partial \langle t | \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) | | t \rangle - \langle | t | \langle \mathbf { E } ^ { \prime } | | t \rangle - \langle | t | \langle \tilde { \mathcal { X } } ( \mathbf { E } ^ { \prime } ) \end{array}
   202	$$
   203	
   204	## 四.（本大题共5小题，每小题10分，共50分）
   205	
   206	1.设 $a > 0 , a _ { 1 } = \frac { 1 } { 2 } ( a + \frac { 1 } { a } ) , a _ { n + 1 } = \frac { 1 } { 2 } ( a _ { n } + \frac { 1 } { a _ { n } } ) , n = 1 , 2 , \cdots$ ，证明：数列 $\left\{ a _ { n } \right\}$ 收敛，并且 其极限为1.
   207	
   208	## 【宝哥解答】
   209	
   210	对任意x>0，由均值不等式，有（x
   211	
   212	$a > 0 , a _ { 1 } = \frac { 1 } { 2 } ( a + \frac { 1 } { a } ) , a _ { n + 1 } = \frac { 1 } { 2 } ( a _ { n } + \frac { 1 } { a _ { n } } ) , n = 1 , 2 , \cdots$ 由此可见 $a _ { \scriptscriptstyle 1 } \geq 1$
   213	
   214	$a _ { n + 1 } > 0 , n = 1 , 2 ,$ $a _ { n } > 0 , n = 1 , 2 , \cdots$ ，故 $a _ { n + 1 } \geq 1 , n = 1 , 2 , \cdots$ ，故$a _ { n } \geq 1 , n = 1 , 2 , \cdots$
   215	
   216	$$
   217	a _ { n + 1 } - a _ { n } = { \frac { 1 } { 2 } } ( a _ { n } + { \frac { 1 } { a _ { n } } } ) - a _ { n } = { \frac { 1 - a _ { n } ^ { 2 } } { 2 a _ { n } } } \leq 0 , n = 1 , 2 , \cdots ,
   218	$$
   219	
   220	故 $\left\{ a _ { n } \right\}$ 单调递减.由单调有界准则， $\left\{ a _ { n } \right\}$ 收敛.记 $\operatorname* { l i m } _ { n \to \infty } a _ { n } = \lambda$ ，则 $A \geq 1$ 且 $A = \frac { 1 } { 2 } ( A + \frac { 1 } { A } )$ ，即A=1.故数列{a收敛，并且其极限为1.
   221	
   222	2.用一致连续的定义证明：函数$( x ) = \cos { \sqrt { x } }$ 在 $\textstyle { \left[ a , + \infty \right) ( a > 0 ) }$ 上一致连续.  
   223	【宝哥解答】
   224	
   225	对任意 $x , y \in \left[ a , + \infty \right)$ 使得 ，由拉格朗日中值定理，存在 $\xi = \theta x + ( 1 - \theta ) y , \theta \in [ 0 , 1 ]$
   226	
   227	故
   228	
   229	$$
   230	f ( x ) - f ( y ) = f ^ { \prime } ( \xi ) ( x - y ) = - \frac { \sin \sqrt { \xi } } { 2 \sqrt { \xi } } ( x - y ) ,
   231	$$
   232	
   233	$$
   234	\left| f ( x ) - f ( y ) \right| = \left| - { \frac { \sin { \sqrt { \xi } } } { 2 { \sqrt { \xi } } } } ( x - y ) \right| \leq { \frac { 1 } { 2 } } { \big | } x - y { \big | } .
   235	$$
   236	
   237	对任意 $\varepsilon > 0$ ，取 $\delta = 2 \varepsilon .$ 则对任意$x , y \in \left[ a , + \infty \right)$ 只要 $\vert x - y \vert < \delta$ 就有  
   238	$\vert f ( x ) - f ( y ) \vert < \varepsilon ^ { \ast } ,$ 故函数 $f ( x ) = \cos { \sqrt { x } }$ 在 $\textstyle { \left[ a , + \infty \right) ( a > 0 ) }$ 上一致连续.  
   239	3.设/(x)在[a,b]上连续，在(a,b)内可微，且
   240	
   241	$$
   242	f ( a ) f ( b ) > 0 \ , f ( a ) f ( \frac { a + b } { 2 } ) < 0 \ ,
   243	$$
   244	
   245	证明：存在一点 $\boldsymbol { \xi } \in ( a , b )$ 使得 $f ^ { \prime } ( \xi ) = f ( \xi )$
   246	
   247	【宝哥解答】
   248	
   249	f（x）在[a,b]上连续，在（a,b）内可微，
   250	
   251	$$
   252	f ( a ) f ( b ) > 0 ~ , ~ f ( a ) f ( \frac { a + b } { 2 } ) < 0 .
   253	$$
   254	
   255	不妨假设 $f ( a ) > 0 \%$ 则 $f ( b ) > 0$ $f ( \frac { a + b } { 2 } ) < 0$ 由零点定理，存在
   256	
   257	$$
   258	c _ { 1 } \in ( a , \frac { a + b } 2 ) , c _ { 2 } \in ( \frac { a + b } 2 , b ) ,
   259	$$
   260	
   261	使得 $f ( c _ { 1 } ) = f ( c _ { 2 } ) = 0$
   262	
   263	则F(x)在[a,b]上连续，在（0,b)内可微，且令 $F ( x ) = e ^ { - x } f ( x ) , x \in \left[ a , b \right]$ $a < c _ { 1 } < c _ { 2 } < b$ 使得 $F ( c _ { 1 } ) = F ( c _ { 2 } ) = 0$ 由罗尔中值定理，存在 $\xi \in ( c _ { 1 } , c _ { 2 } ) \subset ( a , b )$ 使得 $0 = F ^ { \prime } ( \xi ) = e ^ { - \xi } \left[ f ^ { \prime } ( \xi ) - f ( \xi ) \right] .$ ,即 f(5)=f(5)
   264	
   265	4.证明：含参量反常积分 $\sec e ^ { - \frac { \pi } { \alpha } } d x$ 在 $\big [ \alpha _ { 0 } , + \infty \big ) ( \alpha _ { 0 } > 0 )$ 上一致收敛，但在 $( 0 , + \infty )$ 上非一致收敛.
   266	
   267	【宝哥解答】
   268	
   269	是收敛的，且对任意 $X > 0$ 和含参量反常积分 $\int _ { 0 } ^ { + \infty } x e ^ { - \alpha x } d x$ 在 $( 0 , + \infty )$ $\alpha \in ( 0 , + \infty )$ 有 耳那购买的必为盗版投诉热线：
   270	
   271	杭州电子科技大学数学分析+高等代数真题解D
   272	
   273	$$
   274	\overbrace { \int _ { X } ^ { + x } x e ^ { - \alpha x } d x = ( - x \overbrace { \alpha } ^ { e ^ { - \alpha x } } - \overbrace { \alpha } ^ { e ^ { - \alpha x } } ) } ^ { + \alpha } \bigg | _ { X } ^ { + \infty } = X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } }
   275	$$
   276	
   277	故
   278	
   279	$$
   280	\operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , \boldsymbol { * } ^ { x } ] } \Bigl | \int _ { \boldsymbol { \chi } } ^ { + \alpha } \boldsymbol { x } e ^ { - \alpha \boldsymbol { * } } d \boldsymbol { x } \Bigr | = \operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , + \infty ] } ( X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } } ) = X \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } } + \frac { \varepsilon ^ { - \alpha Y } } { \alpha _ { 0 } ^ { 2 } } ,
   281	$$
   282	
   283	$$
   284	\operatorname* { s u p } _ { \alpha \in ( 0 , + \infty ) } \left. \int _ { \mathfrak { r } } ^ { + \infty } x e ^ { - \alpha x } d x \right. = \operatorname* { s u p } _ { \alpha \in ( 0 , + \infty ) } ( X \frac { e ^ { - \alpha X } } { \alpha } + \frac { e ^ { - \alpha X } } { \alpha ^ { 2 } } ) = + \infty ,
   285	$$
   286	
   287	$$
   288	\operatorname* { l i m } _ { X \to + x } \operatorname* { s u p } _ { \alpha \in [ \alpha _ { 0 } , + \infty ) } \biggl | \int _ { X } ^ { + x } x e ^ { - \alpha x } d x \biggr | = \operatorname* { l i m } _ { X \to + \infty } ( X \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } } + \frac { e ^ { - \alpha _ { 0 } X } } { \alpha _ { 0 } ^ { 2 } } ) = 0 ,
   289	$$
   290	
   291	$$
   292	\operatorname * { l i m } _ { X  + x } \operatorname* { s u p } _ { \alpha \in ( 0 , + x ) } | \int _ { X } ^ { + x } x e ^ { - \alpha x } d x | = + \infty ,
   293	$$
   294	
   295	故含参量反常积分 $\int _ { 0 } ^ { - x } x e ^ { - a x } d x$ 在 $[ \alpha _ { 0 } , + \infty ) ( \alpha _ { 0 } > 0 )$ )上一致收敛，但在(0,+o0)上非一致收敛.
   296	
   297	5.设f（x）在 $\left[ a , b \right] \left( a < b \right)$ 上连续且单调递增.求证：
   298	
   299	$$
   300	\int _ { a } ^ { b } x f ( x ) d x \geq { \frac { a + b } { 2 } } { \int _ { a } ^ { b } f ( x ) d x } .
   301	$$
   302	
   303	【宝哥解答】
   304	
   305	【OCR整理补全】以下分段积分与换元等式按本题题面及本题末尾已识别的正确等式恢复。记 $c=(a+b)/2$，有
   306	
   307	$$
   308	\begin{aligned}
   309	\int_a^b xf(x)\,dx-c\int_a^b f(x)\,dx
   310	&=\int_a^b(x-c)f(x)\,dx\\
   311	&=\int_a^c(x-c)f(x)\,dx+\int_c^b(x-c)f(x)\,dx\\
   312	&=\int_a^c(x-c)f(x)\,dx+\int_a^c(c-x)f(a+b-x)\,dx\\
   313	&=\int_a^c(x-c)\bigl[f(x)-f(a+b-x)\bigr]\,dx.
   314	\end{aligned}
   315	$$
   316	
   317	在[a,b]上连续且单调增加，对任意 $x \in \left[ a , { \frac { a + b } { 2 } } \right]$ $a + b - x \geq x$ 故
   318	
   319	$f(x)-f(a+b-x)\le0$，且 $x-(a+b)/2\le0$，故
   320	$(x-(a+b)/2)[f(x)-f(a+b-x)]\ge0$，其中 $x\in[a,(a+b)/2]$。因此
   321	
   322	$$
   323	\int_a^b xf(x)\,dx-\frac{a+b}{2}\int_a^b f(x)\,dx
   324	=\int_a^{(a+b)/2}\left(x-\frac{a+b}{2}\right)
   325	[f(x)-f(a+b-x)]\,dx\ge0.
   326	$$
   327	
   328	即 $\int _ { a } ^ { b } x f ( x ) d x \geq { \frac { a + b } { 2 } } \int _ { a } ^ { b } f ( x ) d x$
   329	
   330	## 【宝哥备注3】
   331	
   332	本题见宝哥题解精粹第10讲5.2例4.
杭州电子科技大学2023年数学分析解答
一. 填空题 (每小题5分)
1. 已知 $f(x) = \frac{x}{\sqrt{1+x^2}}$, 设 $f_n(x) = f(f(\cdots f(x)))$, 则 $f'_{2023}(0) =$ ____.
解: 由 $f_1(x) = f(x) = \frac{x}{\sqrt{1+x^2}}$
$f_2(x) = f(f(x)) = \frac{x}{\sqrt{1+x^2}} / \sqrt{1 + \left(\frac{x}{\sqrt{1+x^2}}\right)^2} = \frac{x}{\sqrt{1+2x^2}}$
$\cdots \cdots$
$f_n(x) = \frac{x}{\sqrt{1+nx^2}}$ 于是 $f_{2023}(x) = \frac{x}{\sqrt{1+2023x^2}}$
又 $f'_{2023}(x) = \frac{1}{(1+2023x^2)^{\frac{3}{2}}}$, 则 $f'_{2023}(\theta) = 1$
2. $\lim_{n \to \infty} n(\sqrt{n^2+1} - n) =$ _____
解: $I = \lim_{n \to \infty} \frac{n(\sqrt{n^2+1} - n)(\sqrt{n^2+1} + n)}{\sqrt{n^2+1} + n} = \lim_{n \to \infty} \frac{\pi}{\sqrt{n^2+1} + n} = \frac{1}{2}$
3. 设 $f(x)$ 在 $[a,b]$ 上连续. $F(x) = \int_a^x f(t)(t-x)dt$ 则 $F'(x) =$ _____
解: $F(x) = \int_a^x f(t) \cdot t dt - x \int_a^x f(t) dt$
$F'(x) = x f(x) - \int_a^x f(t) dt - x f(x) = -\int_a^x f(t)dt$
4. $\int_{- \infty}^{+ \infty} e^{-x^2} dx =$ _____
解: Euler - Poisson 积分: $\int_{0}^{+ \infty} e^{-x^2} dx = \frac{\pi}{2}$
$\int_{- \infty}^{+ \infty} e^{-x^2} dx = 2 \int_{0}^{+ \infty} e^{-x^2} dx = 2 \cdot \frac{\pi}{2} = \pi$
5. 函数 $f(x) = \left\{ \begin{array}{l l} \cos \frac{\pi x}{2}, |x| \leq 1 \\ |x-1|, |x| > 1 \end{array} \right.$ 的间断点为 ____.
解: $\lim_{x \to 1^+} f(x) = \lim_{x \to 1^+} |x-1| = 0$, $\lim_{x \to 1^-} f(x) = \lim_{x \to 1^-} \cos \frac{\pi x}{2} = 0$
又 $f(1) = \cos \frac{\pi}{2} = 0$. 则 $f(x)$ 在 $x=1$ 处连续
$\lim_{x \to -1^+} f(x) = \lim_{x \to -1^+} \cos \frac{\pi x}{2} = 0$, $\lim_{x \to -1^-} f(x) = \lim_{x \to -1^-} |x-1| = 2$
则 $f(x)$ 在 $x=-1$ 处间断

## tool · 2026-10-19T11:51:14Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"key":"92a5bd5ef85605e7","blocks":11,"chars":9101}

## tool · 2026-10-19T11:52:13Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"key":"176002d27d3f75a0","blocks":16,"chars":15133}

## tool · 2026-10-19T11:53:06Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"key":"391fa17a5f0f6f61","blocks":8,"chars":12222}

## tool · 2026-10-19T11:53:14Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"48e4da","wall_time_seconds":0.16522475,"exit_code":1,"original_token_count":581,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/check_math_syntax_2018_2023.py\", line 51, in <module>\n    records = list(executor.map(check, jobs))\n              ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/concurrent/futures/_base.py\", line 619, in result_iterator\n    yield _result_or_cancel(fs.pop())\n          ^^^^^^^^^^^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/concurrent/futures/_base.py\", line 317, in _result_or_cancel\n    return fut.result(timeout)\n           ^^^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/concurrent/futures/_base.py\", line 456, in result\n    return self.__get_result()\n           ^^^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/concurrent/futures/_base.py\", line 401, in __get_result\n    raise self._exception\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/concurrent/futures/thread.py\", line 59, in run\n    result = self.fn(*self.args, **self.kwargs)\n             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/check_math_syntax_2018_2023.py\", line 35, in check\n    result = subprocess.run([\n             ^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/subprocess.py\", line 548, in run\n    with Popen(*popenargs, **kwargs) as process:\n         ^^^^^^^^^^^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/subprocess.py\", line 1026, in __init__\n    self._execute_child(args, executable, preexec_fn, close_fds,\n  File \"/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/lib/python3.12/subprocess.py\", line 1955, in _execute_child\n    raise child_exception_type(errno_num, err_msg, err_filename)\nFileNotFoundError: [Errno 2] No such file or directory: '/Volumes/SamsungSSD990PRO/Application/texlive/2025/bin/universal-darwin/xelatex'\n"}
6. 级数 $\sum_{n=2}^{\infty} \left(1+\frac{1}{n}\right)^{n(n+1)} x^n$ 的收敛半径为 ____.
解: 记 $u_n = \left(1+\frac{1}{n}\right)^{n(n+1)}$
$\rho = \lim_{n \to \infty} \sqrt[n]{\left|u_n\right|} = \lim_{n \to \infty} \left(1+\frac{1}{n}\right)^{n+1} = e$, $R = \frac{1}{\rho} = \frac{1}{e}$
7. 设曲线 $L$ 是圆 $x^2+y^2=r^2$ 在第一象限内的部分, 则 $\int_{L} xy dS =$ ____.
解: $\int_{L} xy dS = \int_{0}^{\frac{\pi}{2}} r^3 \sin \theta \cos \theta d\theta = \frac{1}{2} r^3 \sin^2 \theta \left|_{0}^{\frac{\pi}{2}} = \frac{1}{2} r^3$
8. $\int \frac{1}{x(1+x^n)} dx =$ ____.
解: 令 $t=x^n$, 则 $\int \frac{1}{x(1+x^n)} dx = \int \frac{x^{n-1}}{x^n(1+x^n)} dx = \frac{1}{n} \int \frac{dt}{t(1+t)}$
$= \frac{1}{n} \ln \left| \frac{t}{1+t} \right| + C = \frac{1}{n} \ln \left| \frac{x^n}{1+x^n} \right| + C$
二. 计算题 (每小题 10分)
1. 计算 $\int_{L} (-2x e^{-x^2} \sin y) dx + (e^{-x^2} \cos y + x^6) dy$
这里 $L$ 为从点 $(1,0)$ 到 $(-1,0)$ 的半圆 $y = \sqrt{1-x^2} (-1 \leq x \leq 1)$
解: 记 $L'$ 为从 $(-1,0)$ 到 $(1,0)$ 的直线段 $D$ 为 $L$ 与 $L'$ 所围成的封闭区域
由 Green 公式
$I_1 = \int_{L+2'} (-2x e^{-x^2} \sin y) dx + (e^{-x^2} \cos y + x^6) dy$
$= 6 \int_{0}^{\pi} x^5 dx dy = 6 \int_{0}^{\pi} d\theta \int_{0}^{1} r^6 \cos \theta d\theta =$
$= 6 \int_{0}^{\pi} x^5 dx dy = 6 \int_{-1}^{1} x^5 dx \int_{0}^{\sqrt{-x^2}} dy = 6 \int_{-1}^{1} x^5 \sqrt{-x^2} dx = 0$
$x I_2 = \int_{L'} (-2x e^{-x^2} \sin y) dx + (e^{-x^2} \cos y + x^6) dy = 0 \therefore I = I_1 + I_2 = 0$
2. 求 $\lim_{x \to \infty} [x-x^2 \ln(1+\frac{1}{x})]$
解: 由 $\ln(1+\frac{1}{x}) = \frac{1}{x} - \frac{1}{2x^2} + o(\frac{1}{x^2})$
$I = \lim_{x \to \infty} [x-x^2(\frac{1}{x} - \frac{1}{2x^2} + o(\frac{1}{x^2}))] = \lim_{x \to \infty} (x-x + \frac{1}{2} + o(1)) = \frac{1}{2}$3. 求 $\sum_{n=1}^{\infty} \frac{2n}{3^n}$ 的和

解：考虚幂级数 $S(x) = \sum_{n=1}^{\infty} \frac{2n}{3^n} x^n$，记 $u_n = \frac{2n}{3^n}$
由 $\rho = \lim_{n \to \infty} \sqrt{\|u_n\|} = \lim_{n \to \infty} \sqrt{\frac{2n}{3^n}} = \frac{1}{3}$，$\therefore R = \frac{1}{\rho} = 3$
当 $x = \pm 3$ 时，幂级数 $\sum_{n=1}^{\infty} \frac{2n}{3^n} x^n$ 发散，故其收敛域为 $(-3, 3)$
由 $S(x) = \sum_{n=1}^{\infty} \frac{2n}{3^n} x^n = x \sum_{n=1}^{\infty} \frac{2n}{3^n} x^{n-1} = x f(x)$
又 $\int_0^x f(t) dt = \int_0^x \sum_{n=1}^{\infty} \frac{2n}{3^n} t^{n-1} dt = \sum_{n=1}^{\infty} \int_0^x \frac{2n}{3^n} t^{n-1} dt$
$= \sum_{n=1}^{\infty} \frac{2x^n}{3^n} = \frac{2x}{3-x}, x \in (-3, 3)$
$\therefore S(x) = x f(x) = x \left(\frac{2x}{3-x}\right)' = \frac{6x}{(3-x)^2}, x \in (-3, 3)$
于是 $\sum_{n=1}^{\infty} \frac{2n}{3^n} = \frac{6}{(3-1)^2} = \frac{3}{2}$

4. 计算 $\Phi_2 x^2 y dx + y^2 dy + z dz$，其中 $L$ 是圆柱 $x^2 + y^2 = 1$ 与平面 $x + z = 1$ 的交线
从 $z$ 轴的正向看去，为逆时针方向.

解：令 $x = \cos \theta, y = \sin \theta, z = 1 - \cos \theta, \theta \in [0, 2\pi]$
则 $\Phi_2 x^2 y dx + y^2 dy + z dz = \int_0^{2\pi} \left[ -\cos^2 \theta \sin^2 \theta + \sin^2 \theta \cos \theta + (1 - \cos \theta) \sin \theta \right] d\theta$
$= \int_0^{2\pi} \left( -\frac{1 + \cos 2\theta}{2} \right) \left( \frac{1 - \cos 2\theta}{2} \right) d\theta + \int_0^{2\pi} \sin \theta d\theta = -\frac{1}{4} \int_0^{2\pi} \left( \frac{1 - \cos 4\theta}{2} \right) d\theta = -\frac{\pi}{4}$

5. 计算 $\iiint_V x^2 \sqrt{x^2 + y^2} dx dy dz, V$ 是曲面 $z = \sqrt{x^2 + y^2}$ 与 $z = x^2 + y^2$ 所围区域.

解：记 $D$ 为 $V$ 在平面 $xoy$ 上的投影，那么 $D = \{(x, y) | x^2 + y^2 \leq 1\}$
于是 $I = \iiint_V x^2 \sqrt{x^2 + y^2} dx dy dz = \iiint_0^{2\pi} x^2 \sqrt{x^2 + y^2} \cos^2 \theta dr = \frac{1}{42} \int_0^{2\pi} \cos^2 \theta d\theta = \frac{\pi}{42}$三. 证明题 (每小题 10分)

1. 证明: $\sum_{n=1}^{\infty} (-1)^n \frac{x^2+n}{n^2}$ 在任何有限区域 $[a,b]$ 上一致收敛
而在实轴上任何一点都不绝对收敛
证: 记 $a_n(x) = (-1)^n, b_n(x) = \frac{x^2+n}{n^2}$
(i) $\forall x \in [a,b], \forall n. \text{有} \left| \sum_{k=1}^{\infty} (-1)^k \right| \leq 1$
(ii) $\forall x \in [a,b], \{b_n(x)\} \downarrow$; 极限函数 $b(x) = \lim_{n \to \infty} \frac{x^n+n}{n^2} = 0$
由 $\lim_{n \to \infty} \sup_{x \in [a,b]} |b_n(x)-b(x)| = \lim_{n \to \infty} \sup_{x \in [a,b]} \frac{x^2+n}{n^2} = 0 \therefore b_n(x) \Rightarrow 0$
由 Dirichlet 判别法, $\sum_{n=1}^{\infty} (-1)^n \frac{x^2+n}{n^2}$ 在 $[a,b]$ 上一致收敛
另一方面, $\forall x \in R. \text{有} \left| (-1)^n \frac{x^2+n}{n^2} \right| = \frac{x^2+n}{n^2} \geq \frac{1}{n}$ 其中 $\sum_{n=1}^{\infty} \frac{1}{n}$ 发散
$\therefore \sum_{n=1}^{\infty} |(-1)^n \frac{x^2+n}{n^2}|$ 发散. 于是 $\sum_{n=1}^{\infty} (-1)^n \frac{x^2+n}{n^2}$ 在实轴上任何一点都不绝对收敛

2. 设奇函数 $f(x)$ 在 $[-1,1]$ 上具有 = 阶导数, 且 $f(1) = 1$
证明: (1) 存在 $y \in (0,1)$. 使得 $f'(y) = 1$
(2) 存在 $y \in (-1,1)$. 使得 $f''(y) + f'(y) = 1$
证: (1) 令 $F(x) = f(x)-x$. 由题知 $f(0) = 0, f(1) = 1$
那么 $F(0) = 0, F(1) = 0$. 由 Rolle 定理, $\exists y \in (0,1), s.t. F'(y) = 0$. 即 $f'(y) = 1$
(2) 令 $G(x) = e^x (f'(x)-1)$
由 (1) 知, $\exists y \in (0,1). s.t. f'(y) = 1$. 又 $f$ 是奇函数, $\exists y_1 \in (-1,0), s.t. f'(y_1) = 1$
由 Rolle 定理, $\exists y \in (y_1, y) \subset (-1,1). s.t. G'(y) = 0$
即 $e^y (f''(y) + f'(y)-1) = 0$. 于是 $f''(y) + f'(y) = 1$3. 设 $f(x)$ 在 $[0,1]$ 上连续, 证明: $\iint_0 f(1-y)f(x)dxdy = \frac{1}{2}[\int_0^1 f(x)dx]^2$
其中 $D$ 是以 $O(0,0), A(0,1), B(1,0)$ 为顶点的三角形区域
证: 由图(1) $\iint_0 f(1-y)f(x)dxdy = \int_0^1 f(x)dx \int_0^{1-x} f(1-y)dy$
令 $t=1-y \int_0^1 f(x)dx \int_0^{1} f(t)dt = \int_0^1 f(x)dx \int_0^{1} f(y)dy$
由图(2) $D_1 = D_2$. 有 $\int_0^1 f(x)dx \int_0^{1} f(y)dy = \int_0^1 f(x)dx \int_0^{x} f(y)dy$
于是 $\iint_0 f(1-y)f(x)dxdy = \frac{1}{2}[\int_0^1 f(x)dx \int_0^{x} f(y)dy + \int_0^1 f(x)dx \int_0^{x} f(y)dy]$
$= \frac{1}{2} \int_0^1 f(x)dx \int_0^{1} f(y)dy = \frac{1}{2}[\int_0^1 f(x)dx]^2$

4. 已知 $\Delta$ 表示 Laplace 算符, 证明: $\Delta(uv) = (\Delta u)V + 2\nabla u\nabla v + u(\Delta v)$
这里 $\nabla v$ 表示函数 $V$ 在点 $(x,y,z)$ 处的梯度, “表理示点乘”
证: 由 $\Delta(uv) = \frac{\partial^2(uv)}{\partial x^2} + \frac{\partial^2(uv)}{\partial y^2} + \frac{\partial^2(uv)}{\partial z^2}$
$= u\left(\frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 v}{\partial y^2} + \frac{\partial^2 v}{\partial z^2}\right) + V\left(\frac{\partial^2 v}{\partial x^2} + \frac{\partial^2 v}{\partial y^2} + \frac{\partial^2 v}{\partial z^2}\right)$
$+ 2\left(\frac{\partial u}{\partial x} \cdot \frac{\partial v}{\partial x} + \frac{\partial u}{\partial y} \cdot \frac{\partial v}{\partial y} + \frac{\partial u}{\partial z} \cdot \frac{\partial v}{\partial z}\right)$
$= u(\Delta v) + 2\nabla u\nabla v + V(\Delta u)$

四. 综合题
1. (10分) 求两个曲面 $x+2y=1$ 和 $x^2+2y^2+z^2=1$ 的交线上距离原点最近的点
解: 在约束条件 $x+2y=1$ 和 $x^2+2y^2+z^2=1$ 下, 求 $d=x^2+y^2+z^2$ 的最小值点
设 $L(x,y,z,\lambda,\mu) = x^2+y^2+z^2+\lambda(x+2y-1)+\lambda(x^2+2y^2+z^2-1)$
由 Lagrange 乘数法
$Lx = 2x+\lambda+2\lambda x = 0$
$Ly = 2y+2\lambda+4\lambda y = 0$
$Lz = 2z+2\lambda M = 0$
$L\lambda = x+2y-1 = 0$
$L\mu = x^2+2y^2+z^2-1 = 0$
解得 $(x,y,z) = \left(-\frac{2}{3}, \frac{2}{3}, 0\right)$
其就是最小值点2. (20分). 设 $f(x) = \int_{1}^{+\infty} \frac{\cos(xt)}{t(1+t^2)} dt, x \in(-\infty, +\infty)$

(1) 试证明积分 $\int_{1}^{+\infty} \frac{\cos xt}{t(1+t^2)} dt$ 在 $(- \infty, +\infty)$ 上一致收敛

(2) 试证明 $f(x)$ 在 $x \in(-\infty, +\infty)$ 上一致连续

证(1) (i) $\forall A > 1, \forall x \in(-\infty, +\infty)$ 有 $|\int_{A}^{A} \cos xt dt| \leq 2$

(ii) 对每一个 $x \in R$. $\frac{1}{t(1+t^2)}$ 为 $t$ 的单调递减函数

且 $\forall x \in R$. 有 $\lim_{t \to \infty} \frac{1}{t(1+t^2)} = 0$

由狄利克雷判别法. $\int_{1}^{+\infty} \frac{\cos xt}{t(1+t^2)} dt$ 在 $R$ 上一致收敛

(2) $\forall x_1, x_2 \in R$

有 $|f(x_1) - f(x_2)| = \left| \int_{1}^{+\infty} \frac{\cos x_1t - \cos x_2t}{t(1+t^2)} dt \right|$

$\leq \int_{1}^{+\infty} \left| \frac{-2 \sin \frac{x_1+x_2}{2} t \cdot \sin \frac{x_1-x_2}{2} t}{t(1+t^2)} \right| dt \leq |x_1-x_2| \int_{1}^{+\infty} \frac{1}{1+t^2} dt$

$= |x_1-x_2| \arctan \left|_{1}^{+\infty} = \frac{\pi}{4} |x_1-x_2|\right.$

那么 $\forall E > 0$. 取 $\delta = \frac{4E}{\pi}$. $\forall x_1, x_2 \in R: |x_1-x_2| < \delta$

有 $|f(x_1) - f(x_2)| \leq \frac{\pi}{4} |x_1-x_2| < E$

故 $f(x)$ 在 $(- \infty, +\infty)$ 上一致连续

## tool · 2026-10-19T11:53:26Z




## tool · 2026-10-19T11:53:32Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"d997b6","wall_time_seconds":0.00000725,"exit_code":1,"original_token_count":29,"output":"Macintosh HD\nls: /Library/TeX/texbin: No such file or directory\nls: /usr/local/texlive: No such file or directory\n"}
{"chunk_id":"5bd02d","wall_time_seconds":0.000006125,"exit_code":0,"original_token_count":165,"output":".agent/hdu-ocr/local/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版)/006.md\n.agent/hdu-ocr/local/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版)/002.md\n.agent/hdu-ocr/local/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版)/003.md\n.agent/hdu-ocr/local/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版)/004.md\n.agent/hdu-ocr/local/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版)/005.md\n.agent/hdu-ocr/local/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版)/001.md\n"}

## tool · 2026-10-19T11:55:52Z


Script failed
Wall time 0.1 seconds
Output:

{"read_chars":4096}
Script error:
apply_patch verification failed: invalid patch: multiple operations target /Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/overrides/e3e469709b9c871a.md

## tool · 2026-10-19T11:56:02Z


Script completed
Wall time 0.1 seconds
Output:

# 杭州电子科技大学2023年数学分析手写详细版：互证整理与识读状态

> 原PDF共6页。第1—6页均尚未完成逐页可靠识读，现有整份OCR不含可靠页分隔，不能据此把某段内容归属到某一页。本文件由助手将可与同年打印真题、打印参考答案互证的题目及结论整理成索引；不代表手写原作者的逐字转录，也不替代完整手写解析。未能可靠识别的详细推导仍需核对原稿。

- [完整手写原稿PDF，原页1—6](/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题解答(手写详细版).pdf)
- [同年原打印参考答案PDF](/Users/oyamahappa/Documents/Agent/Codex/HDU/601数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.pdf)
- [同年打印参考答案识别整理稿](/Users/oyamahappa/Documents/Agent/Codex/output/HDU/md/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题参考答案.md)
- [同年打印真题识别稿](/Users/oyamahappa/Documents/Agent/Codex/output/HDU/md/数学分析/2023/2023年杭州电子科技大学601数学分析考研真题.md)

## 原页识读状态

原PDF第1、2、3、4、5、6页均未完成逐页可靠识读。六页原PDF完整保留，均需对照原稿逐页核对；当前不能提供逐页转录完成的证明。

## 一、填空题互证索引

### 1. 迭代函数：函数值与导数的识读差异待核对

两份识别均能确认 $f(x)=x/\sqrt{1+x^2}$，$f_n$ 为 $f$ 的 $n$ 次复合。手写识别可恢复的计算结构为

\[
f_n(x)=\frac{x}{\sqrt{1+nx^2}},\qquad
f_n'(x)=\frac1{(1+nx^2)^{3/2}}.
\]

因此两个分别成立的结论是 $f_{2023}(0)=0$ 和 $f_{2023}'(0)=1$。打印题面及打印答案当前识别的是前者，手写版识别的是后者。原题究竟询问函数值还是导数，须对照原PDF确认；这里保留该差异，不替原题作出选择。

### 2. 根式极限

\[
\lim_{n\to\infty}n\bigl(\sqrt{n^2+1}-n\bigr)=\frac12.
\]

手写版可辨认出有理化计算方向，打印答案可互证最终结论。

### 3. 变上限积分求导

对 $F(x)=\int_a^x f(t)(t-x)\,dt$，可互证的分解与导数为

\[
F(x)=\int_a^x tf(t)\,dt-x\int_a^x f(t)\,dt,
\qquad F'(x)=-\int_a^x f(t)\,dt.
\]

### 4. Gaussian 积分

\[
\int_{-\infty}^{+\infty}e^{-x^2}\,dx=\sqrt\pi.
\]

### 5. 分段函数间断点

\[
f(x)=\begin{cases}
\cos(\pi x/2),&|x|\le1,\\
|x-1|,&|x|>1.
\end{cases}
\]

可互证的结论为唯一间断点 $x=-1$；在 $x=1$ 处连续。$x=-1$ 处的左、右极限分别为 $2$、$0$。打印识别稿中左极限出现的数字 $4$ 与该题面不符，按函数值直接核算为 $2$。

### 6. 幂级数收敛半径

\[
\sum_{n=2}^{\infty}\left(1+\frac1n\right)^{n(n+1)}x^n,
\qquad R=\frac1e.
\]

### 7. 第一象限四分之一圆弧积分

对 $L:\ x^2+y^2=r^2$ 的第一象限圆弧，按通常的半径条件 $r>0$，

\[
\int_Lxy\,ds=r^3\int_0^{\pi/2}\cos\theta\sin\theta\,d\theta
=\frac{r^3}{2}.
\]

### 8. 不定积分

在被积函数有定义的区间内，且 $n\ne0$，

\[
\int\frac{dx}{x(1+x^n)}
=\frac1n\ln\left|\frac{x^n}{1+x^n}\right|+C.
\]

手写版详细换元末式未可靠识别；以上闭式与打印答案互证，不据此声称已经转录手写末式。

## 二、计算题互证索引

### 1. 上半圆上的第二类曲线积分

题目为沿上半圆从 $(1,0)$ 到 $(-1,0)$ 的积分

\[
\int_L(-2xe^{-x^2}\sin y)\,dx+(e^{-x^2}\cos y+x^6)\,dy.
\]

可互证结论为 $0$。手写版 Green 公式推导段严重损坏，详细步骤参见同年打印参考答案。

### 2. 对数极限

\[
\lim_{x\to+\infty}\left[x-x^2\ln\left(1+\frac1x\right)\right]=\frac12.
\]

手写版展开式未可靠识别；题面与结论由打印版互证。

### 3. 数项级数求和

\[
\sum_{n=1}^{\infty}\frac{2n}{3^n}=\frac32.
\]

手写版可识别出引入幂级数及收敛区间 $(-3,3)$ 的思路，后续求和公式严重损坏；结论由打印答案互证。

### 4. 空间闭曲线积分

对圆柱 $x^2+y^2=1$ 与平面 $x+z=1$ 的交线，从 $z$ 轴正向看为逆时针，有

\[
\oint_\Gamma x^2y\,dx+y^2\,dy+z\,dz=-\frac\pi4.
\]

可互证参数为 $x=\cos\theta$、$y=\sin\theta$、$z=1-\cos\theta$，$0\le\theta\le2\pi$。

### 5. 锥面与抛物面之间的三重积分

对 $z=\sqrt{x^2+y^2}$ 和 $z=x^2+y^2$ 围成的区域 $\Omega$，

\[
\iiint_\Omega x^2\sqrt{x^2+y^2}\,dx\,dy\,dz=\frac\pi{42}.
\]

手写版积分换序部分未可靠识别；结论与区域由打印答案互证。

## 三、证明题互证索引

### 1. 函数项级数的一致收敛与非绝对收敛

\[
\sum_{n=1}^{\infty}(-1)^n\frac{x^2+n}{n^2}
\]

在任意有限区间 $[a,b]$ 上一致收敛，在每个实数点均不绝对收敛。手写版可识别出 Dirichlet 判别法，以及用 $1/n$ 比较绝对值级数的思路。

### 2. 奇函数的两项中值结论

若 $f$ 在 $[-1,1]$ 上为二阶可导奇函数，且 $f(1)=1$，则

\[
\exists\xi\in(0,1):f'(\xi)=1,
\qquad
\exists\eta\in(-1,1):f''(\eta)+f'(\eta)=1.
\]

可互证的辅助函数思路为先处理 $f(x)-x$，再处理 $e^x(f'(x)-1)$。手写版若干变量与求导符号损坏，不能逐字采用。

### 3. 三角区域上的积分恒等式

设 $D=\{(x,y):x\ge0,y\ge0,x+y\le1\}$，$f$ 在 $[0,1]$ 连续，则

\[
\iint_D f(1-y)f(x)\,dx\,dy
=\frac12\left[\int_0^1f(x)\,dx\right]^2.
\]

手写版换元与区域示意图后的公式未可靠识别。题目与结论由打印答案互证，详细推导需核对原稿。

### 4. Laplace 算符乘积公式

\[
\Delta(uv)=(\Delta u)v+2\nabla u\cdot\nabla v+u\Delta v.
\]

手写版逐项展开存在严重乱码。目标恒等式与打印题面互证；打印答案识别稿中的同一展开也有截断，整理稿已明确标注助手依据乘积法则补全。

## 四、综合题互证索引

### 1. 交线上距原点最近的点

约束为 $x+2y=1$ 和 $x^2+2y^2+z^2=1$。打印答案可互证的最近点为

\[
\left(-\frac13,\frac23,0\right).
\]

手写识别中的横坐标为 $-2/3$，不满足约束 $x+2y=1$，不能作为可用结论；原稿该数字仍待核对。

### 2. 含参量积分的一致收敛及函数的一致连续性

题目为

\[
f(x)=\int_1^\infty\frac{\cos(xt)}{t(1+t^2)}\,dt,
\qquad x\in\mathbb R.
\]

结论为积分在全实轴关于 $x$ 一致收敛，且 $f$ 在 $\mathbb R$ 一致连续。打印答案可互证的充分估计为

\[
\left|\frac{\cos(xt)}{t(1+t^2)}\right|\le\frac1{t(1+t^2)},
\qquad
|f(x)-f(y)|\le\frac\pi4|x-y|.
\]

手写版将分子误识为 $\cos(x+1)$，且后续判别法与最终估计有严重乱码。这里采用同年打印题面的 $\cos(xt)$ 进行互证，不声称恢复了手写原证明。

## 尚未完成的原稿转录

原页1—6的逐页对应关系、手写中间计算、区域示意图及被损坏的推导均未完成可靠转录。上述索引只保留可以互证或直接由明确题面核算的内容。需要引用手写作者的证明或比较两版解法时，应回到完整手写PDF核对；不能将本索引当作完整手写解析。


## tool · 2026-10-19T11:57:21Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"chars":7482}

## tool · 2026-10-19T11:58:19Z


Script failed
Wall time 0.3 seconds
Output:

{}
{}
Script error:
Error: 3.设函数f（x）
    at between (exec_main.mjs:7:101)
    at exec_main.mjs:35:3
    at edit (exec_main.mjs:3:42)
    at async exec_main.mjs:34:1

## tool · 2026-10-19T11:58:25Z


Script completed
Wall time 0.1 seconds
Output:

34:3.设y=f（x）由方程 $y - \sin ( x y ) = e ^ { x ( 1 - y ) }$ 确定，则 $\operatorname* { l i m } _ { n \to \infty } n \biggl [ f ( \frac { 1 } { n } ) - 1 \biggr ] =$
117:3.设 $z = z ( x , y )$ 为方阵 $f ( x - y , y - z , z - x ) = 0$ 所确定的隐函数，求 $\frac { \partial z } { \partial x } , \frac { \partial z } { \partial y }$ 和dz.
123:G_x=f_1-f_3,\quad G_y=-f_1+f_2,\quad G_z=-f_2+f_3.
192:3.计算曲面积分 $\check { x } = \int \int \frac { \alpha x d y d z + ( z + a ) ^ { 2 } d x d y } { \sqrt { x ^ { 2 } + y ^ { 2 } + z ^ { 2 } } }$ ，其中Σ为下半球面 $z = - \sqrt { a ^ { 2 } - x ^ { 2 } - y ^ { 2 } }$ 的上侧， $a > 0$ 为常数.
266:3.设函数f（x）在区间[0,1]上连续，在开区间（0,1）内可导，且 $f ( 1 ) = 0$ ，证明：存在 $\xi \in ( 0 , 1 )$ ，使得 $f ( \xi ) + ( 1 - e ^ { - \xi } ) f _ { \mathrm { { s } } } ^ { \prime } ( \xi )$
280:在(0,1)内有零点.令 $F ( x ) = ( e ^ { x } - 1 ) f ( x )$ ，则F（x）在区间[0,1]上连续，在开区间（0,1)内可导，且F(0)=F(1)=0.由罗尔中值定理，存在 $\xi \in ( 0 , 1 )$ ，使得 $F ^ { \prime } ( \xi ) = 0$ 即 $f ( \xi ) + ( 1 - e ^ { - \xi } ) f ^ { \prime } ( \xi ) = 0$
.agent/hdu-ocr/overrides/92a5bd5ef85605e7.md:93:1.(本小题5分）求极 $\lim \limits _ { x  0 } \frac { \sqrt { x } } { 1 - e ^ { \sqrt { x } } }$
.agent/hdu-ocr/overrides/92a5bd5ef85605e7.md:101:2.（本小题5分）计算积分 $\int _ { 0 } ^ { \frac { \pi } { 2 } } \frac { \cos x } { 1 + \sin ^ { 2 } x } d x$
.agent/hdu-ocr/overrides/92a5bd5ef85605e7.md:110:3.（本小题5分）
.agent/hdu-ocr/overrides/92a5bd5ef85605e7.md:112:3.（本小题5分）求幂级数 $\sum _ { n = 1 } ^ { \infty } n x ^ { n - 1 }$ 的收敛域及和函数.
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:33:分两步来计算这个积分.


## tool · 2026-10-19T11:58:41Z


Script completed
Wall time 0.2 seconds
Output:

{}
{}
{}
已补全三处剩余修正

## tool · 2026-10-19T11:58:48Z




## tool · 2026-10-19T11:59:30Z


Script completed
Wall time 1.2 seconds
Output:

{}
{"chunk_id":"e2c644","wall_time_seconds":1.001385666,"session_id":15998,"original_token_count":0,"output":""}

## tool · 2026-10-19T11:59:38Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"6f5667","wall_time_seconds":0.000017542,"exit_code":0,"original_token_count":38,"output":"PASS: 已修正公式的SymPy交叉检查；手写6页、19题（末题分两问）结构检查\nPandoc转换 13 份；本检查未调用TeX编译器\n"}
.agent/hdu-ocr/overrides/9e64c36cdac10429.md:38:宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线：15160699421或 15659067618
.agent/hdu-ocr/overrides/92a5bd5ef85605e7.md:107:=\left[\arctan(\sin x)\right]_0^{\pi/2}=\frac\pi4.
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:87:1.计算 $\int _ { L } { ( - 2 x e ^ { - x ^ { 2 } } \sin y ) d x } + { ( e ^ { - x ^ { 2 } } \cos y + x ^ { 6 } ) d y }$ ,这里L为从点(1,0)到(-1,0)的半圆 $y = \sqrt { 1 - x ^ { 2 } } ( - 1 \leq x \leq 1 )$ 学考研 盗版必
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:97:记 $L _ { \imath }$ 为(-1,0)到(1,0)的有向直线段，D为 $L , L _ { \mathrm { 1 } }$ 围成的平面区域，则 $\int _ { L _ { 1 } } { x ^ { 6 } d y } = 0$ 由格林公式，有 数学 有盗 学考研 盗版
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:100:\int _ { L } x ^ { 6 } d y = ( \int _ { L \cup L _ { 1 } } - \int _ { L _ { 1 } } ) x ^ { 6 } d y = \iint \frac { \widehat { \partial } x ^ { 6 } } { \widehat { \partial } x } d x d y = \iint 6 x ^ { 5 } d x d y \quad \stackrel { \cong } { = } \quad 0
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:136:=-\frac18\int_0^{2\pi}(1-\cos4t)\,dt=-\frac\pi4.
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:149:&=\frac\pi5\int_0^1(z^{5/2}-z^5)\,dz
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:150:=\frac\pi5\left(\frac27-\frac16\right)=\frac\pi{42}.
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:248:宝哥数 学考 盗版  
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:249:版权所有 $f ^ { \prime } ( x ) = \int _ { 1 } ^ { + \infty } \frac { \hat { \partial } } { \partial x } \left[ \frac { \cos ( x t ) } { t { ( 1 + t ^ { 2 } ) } } \right] d t = - \int _ { 1 } ^ { + \infty } \frac { \sin ( x t ) } { 1 + t ^ { 2 } } d t ,$ 中哥数
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:255:=\left[\arctan t\right]_1^\infty=\frac\pi4.


## tool · 2026-10-19T11:59:50Z


Script completed
Wall time 0.2 seconds
Output:

.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:87:1.计算 $\int _ { L } { ( - 2 x e ^ { - x ^ { 2 } } \sin y ) d x } + { ( e ^ { - x ^ { 2 } } \cos y + x ^ { 6 } ) d y }$ ,这里L为从点(1,0)到(-1,0)的半圆 $y = \sqrt { 1 - x ^ { 2 } } ( - 1 \leq x \leq 1 )$ 学考研 盗版必
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:97:记 $L _ { \imath }$ 为(-1,0)到(1,0)的有向直线段，D为 $L , L _ { \mathrm { 1 } }$ 围成的平面区域，则 $\int _ { L _ { 1 } } { x ^ { 6 } d y } = 0$ 由格林公式，有 数学 有盗 学考研 盗版
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:229:1.(10分）求两个曲面 $x + 2 y = 1$ 和 $x ^ { 2 } + 2 y ^ { 2 } + z ^ { 2 } = 1$ 的交线上距离原点最近的点.【解答】 所有 哥数学 新有盗 学考 现
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:233:$0 \leq y \leq \frac { 2 } { 3 }$ $y = \frac { 2 } { 3 }$ $z = 0 , x = 1 - 2 y = - \frac { 1 } { 3 }$ ，故交线上距离原点最近的点为所有司  
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:234:$( - \frac { 1 } { 3 } , \frac { 2 } { 3 } , 0 ) .$ 宝哥数学 宝哥数 权所有所有
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:244:(1)对任意 $( t , x ) \in \left[ 1 , + \infty \right) \times ( - \infty , + \infty )$ 有 $\left| { \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \right| \leq { \frac { 1 } { 1 + t ^ { 2 } } } . \ \int _ { 1 } ^ { + \infty } { \frac { d t } { 1 + t ^ { 2 } } }$ 收敛，故版权 宝哥数$\int _ { 1 } ^ { + \infty } \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } d t$ 关于x在 $( - \infty , + \infty )$ 上一致收敛. 哥数学考研所有
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:246:(2）对任意 $\left( t , x \right) \in \left[ 1 , + \infty \right) \times \left( - \infty , + \infty \right)$ ，有 $\left| { \frac { \partial } { \partial x } } \left[ { \frac { \cos ( x t ) } { t ( 1 + t ^ { 2 } ) } } \right] \right| = \left| { \frac { - \sin ( x t ) } { 1 + t ^ { 2 } } } \right| \leq { \frac { 1 } { 1 + t ^ { 2 } } }$ 必究  
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:248:宝哥数 学考 盗版  
.agent/hdu-ocr/overrides/391fa17a5f0f6f61.md:249:版权所有 $f ^ { \prime } ( x ) = \int _ { 1 } ^ { + \infty } \frac { \hat { \partial } } { \partial x } \left[ \frac { \cos ( x t ) } { t { ( 1 + t ^ { 2 } ) } } \right] d t = - \int _ { 1 } ^ { + \infty } \frac { \sin ( x t ) } { 1 + t ^ { 2 } } d t ,$ 中哥数
.agent/hdu-ocr/overrides/9e64c36cdac10429.md:38:宝哥原创，盗版必究，不是在宝哥那购买的必为盗版投诉热线：15160699421或 15659067618
.agent/hdu-ocr/overrides/e43b7f46d6f192ef.md:176:3.计算面积分 $\int \limits _ { \Sigma } \int \int x ^ { 2 } d y d z + y ^ { 2 } d z d x + z ( 1 - 2 x - 2 y ) d x d y$ 其中为上半球面研考$x ^ { 2 } + y ^ { 2 } + z ^ { 2 } = 1 , z \geq 0$ 的上侧
.agent/hdu-ocr/overrides/176002d27d3f75a0.md:61:5.若正项级数 $\sum _ { n = 1 } ^ { \infty } u _ { n }$ 收敛且所有项 $u _ { n } \leq 3$ ，则级数 $\sum _ { n = 1 } ^ { \infty } \frac { u _ { n } } { \pi - u _ { n } }$ 是否收敛？【宝哥解答】
.agent/hdu-ocr/overrides/176002d27d3f75a0.md:63:正项级数 $\sum _ { n = 1 } ^ { \infty } u _ { n }$ 收敛且所有项 $u _ { n } \leq 3$ ，故 $0 \leq \frac { u _ { n } } { \pi - u _ { n } } \leq \frac { u _ { n } } { \pi - 3 } , \forall n \in N ^ { + }$ $\sum _ { n = 1 } ^ { \infty } u _ { n }$ 收敛，由比较判别法，级数 $\sum _ { n = 1 } ^ { \infty } \frac { u _ { n } } { \pi - u _ { n } }$ 收敛.
.agent/hdu-ocr/overrides/176002d27d3f75a0.md:337:5.若两个正数α和 $\beta$ 使得不等式 $( 1 + \frac { 1 } { n } ) ^ { n + \alpha } \leq e \leq ( 1 + \frac { 1 } { n } ) ^ { n + \beta }$ 对所有的正整数n成立，证明 $\pmb { \alpha }$ 的最大值为 $\alpha = \frac { 1 } { \ln 2 } - 1$ $\beta$ 的最小值为 $\beta = \frac { 1 } { 2 }$

{"chunk_id":"348e14","wall_time_seconds":0.000006209,"exit_code":0,"original_token_count":1,"output":"[]\n"}

## tool · 2026-10-19T12:00:20Z


Script completed
Wall time 1.4 seconds
Output:

{}
{}
{}
已清理最后已定位的水印污染
{"chunk_id":"d3fc47","wall_time_seconds":1.001587625,"session_id":47574,"original_token_count":0,"output":""}

## tool · 2026-10-19T12:00:28Z




## tool · 2026-10-19T12:00:54Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"f1eec4","wall_time_seconds":0.000012458,"exit_code":0,"original_token_count":38,"output":"PASS: 已修正公式的SymPy交叉检查；手写6页、19题（末题分两问）结构检查\nPandoc转换 13 份；本检查未调用TeX编译器\n"}
{"chunk_id":"58ca31","wall_time_seconds":0.000007375,"exit_code":0,"original_token_count":54,"output":"e43b7f46d6f192ef 11790\n9e64c36cdac10429 9856\n918271f5178ca024 12987\n92a5bd5ef85605e7 11551\n176002d27d3f75a0 18044\n391fa17a5f0f6f61 10788\ne3e469709b9c871a 10806\nPASS: 13份转换均无警告；7份修复稿已保存\n"}

## assistant · 2026-10-19T12:01:01Z

妹妹，已实际修正6份打印答案，并将[2023手写版](/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/overrides/e3e469709b9c871a.md)更新为6页、19题的逐页推导全文。

已核正导数、积分界、错误数值和水印污染；无法确定的原题符号保留待核对说明。手写版保留独有解法，并明确标出原证明缺口及助手补充。

SymPy检查通过，13份Pandoc转换均无警告。实编译由主代理统一执行，本次未修改output、builder或Git。
