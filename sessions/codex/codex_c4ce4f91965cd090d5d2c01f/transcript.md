# 01a1574b-17e6-7830-a6c2-2828d9f05258

来源：codex

项目：/Users/oyamahappa/Documents/Agent/Codex

## developer · 2026-10-20T03:11:44Z

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



## developer · 2026-10-20T03:11:44Z

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

## developer · 2026-10-20T03:11:44Z

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

## developer · 2026-10-20T03:11:44Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-10-20T03:11:44Z

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
  <current_date>2026-10-20</current_date>
  <timezone>Asia/Shanghai</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/Agent/Codex</root><root>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/Agent/Codex</path></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Agent/Codex/.aws</path></entry><entry access="read"><path>/Users/oyamahappa/.codex/visualizations/2026/10/19/01a154a9-640e-7ef2-a22a-802b1ab02dbb/.aws</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## developer · 2026-10-20T03:11:44Z

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


## tool · 2026-10-20T03:11:48Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 10500)
Total output lines: 2

{"chunk_id":"cfbbfc","wall_time_seconds":0.000005875,"exit_code":0,"original_token_count":76,"output":"     461 output/大一数学分析期末复习-上册/chapters/ch01.tex\n     420 output/大一数学分析期末复习-上册/chapters/ch02.tex\n     433 output/大一数学分析期末复习-上册/chapters/ch03.tex\n     432 output/大一数学分析期末复习-上册/chapters/ch04.tex\n    1746 total\n"}
{"chunk_id":"8560c3","wall_time_seconds":0.000007042,"exit_code":0,"original_token_count":9938,"output":"\\section{第1章 函数与极限}\n\\subsection{函数}\n\\begin{exercise}{1}{定义域与参数约束}\n求 $f(x)=\\arccos(2x+1)+\\log_2(3x+2)$ 的定义域。再确定实数 $a$ 的取值范围，使区间 $[a,a+\\frac14]$ 全部包含于该定义域。\n\\end{exercise}\n\\begin{exercise}{2}{复合函数的定义域}\n设 $f(x)=\\frac{x-1}{x+1}$。求 $f(-2)$、$f(f(x))$，并写出复合函数的完整定义域；判断化简后的表达式能否在其自然定义域上与原复合函数视为同一函数。\n\\end{exercise}\n\\begin{exercise}{3}{换元与函数确定范围}\n已知对一切 $x\\ne0$，$f(1/x)=4/x+2x^2+1$。求 $f(t)$ 的已知表达式及其适用范围，再求 $f(x^2+1)$；说明上述条件是否确定了 $f(0)$。\n\\end{exercise}\n\\begin{exercise}{4}{反三角函数与值域}\n设 $f(x)=\\arcsin\\frac4x$。求其定义域及 $f(-4)$、$f(8/\\sqrt2)$、$f(8/\\sqrt3)$，并确定其值域及各端点是否能够取到。\n\\end{exercise}\n\\begin{exercise}{5}{复合函数值域}\n求 $f(x)=\\sin\\frac{\\pi x}{2(1+x^2)}$ 的值域及取到最大值、最小值的全部自变量，并说明为何不能直接把正弦函数的值域作为答案。\n\\end{exercise}\n\\begin{exercise}{6}{反三角函数的主值}\n设 $f(x)=\\arccos2x$、$g(x)=\\arctan x$、$h(x)=\\operatorname{arccot}(x/2)$，其中 $\\operatorname{arccot}$ 取值于 $(0,\\pi)$。求 $f(\\sqrt3/4)g(-1)h(2)$；分别写出三个函数的定义域和值域。\n\\end{exercise}\n\\begin{exercise}{7}{非单射换元与定义域}\n已知对一切非零实数 $x$，$f(x+1/x)=\\frac{4x^2}{x^4+1}$。求条件所能确定的 $f(t)$ 及 $t$ 的范围，并验证 $x$ 与 $1/x$ 给出的函数值一致；说明能否据此确定 $f(0)$。\n\\end{exercise}\n\\begin{exercise}{8}{分段函数与奇偶性}\n设 $f(x)=\\begin{cases}\\frac{x}{\\pi}|\\sin x|,&|x|<\\pi/3,\\\\0,&|x|\\ge\\pi/3.\\end{cases}$ 求 $f(\\pi/6)$、$f(-\\pi/4)$、$f(2)$；判断其奇偶性，并讨论 $x=\\pm\\pi/3$ 两点处能否通过重新赋值使函数连续。\n\\end{exercise}\n\\begin{exercise}{9}{反解复合函数的分支限制}\n设 $f(t)=\\tan2t$，$f(g(x))=x^2-1$，且 $|g(x)|\\le\\pi/8$。求 $g(x)$ 及其最大定义域，说明范围限制在确定反函数分支和定义域时各起什么作用。\n\\end{exercise}\n\\begin{exercise}{10}{最大值函数的分段表达}\n设 $\\varphi(x)=\\max\\{x,x^2,1\\}$。求定义域、分段表达式以及 $\\varphi(-2)$、$\\varphi(-1)$、$\\varphi(0)$；确定该函数的最小值与全部取值点。\n\\end{exercise}\n\\begin{exercise}{11}{复合次序与分段边界}\n设 $f(x)=\\begin{cases}-1,&x<0,\\\\1,&x\\ge0,\\end{cases}$、$g(x)=2x-1$。分别写出 $f(g(x))$、$g(f(x))$ 的分段表达式，并求两者相等的全部 $x$。\n\\end{exercise}\n\\begin{exercise}{12}{复合映射与值域约束}\n设 $f(x)=\\begin{cases}2-x,&x<0,\\\\2+x,&x\\ge0,\\end{cases}$、$g(x)=\\begin{cases}x,&x<0,\\\\x^2,&x\\ge0.\\end{cases}$ 求 $f(g(x))$、$g(f(x))$ 的分段表达式和值域，并判断它们是否为偶函数。\n\\end{exercise}\n\\begin{exercise}{13}{分段函数的四则运算}\n设 $f(x)=\\begin{cases}2x+1,&x<0,\\\\x^2+1,&x\\ge0,\\end{cases}$、$g(x)=\\begin{cases}\\sin x,&x<\\pi,\\\\\\cos x,&x\\ge\\pi.\\end{cases}$ 写出 $f+g$、$fg$ 的分段表达式，并分别讨论二者在 $0$ 与 $\\pi$ 处的连续性。\n\\end{exercise}\n\\begin{exercise}{14}{反函数及端点范围}\n设 $f(x)=\\frac{1-\\sqrt{1+x}}{1+\\sqrt{1+x}}$。确定定义域和值域，证明该函数可逆并求反函数；写出反函数的定义域，解释原函数值域中未包含的端点。\n\\end{exercise}\n\\begin{exercise}{15}{奇偶性的定义域条件}\n设 $a>0$。分别判断下列函数的奇偶性，写明定义域，并对非奇非偶的函数给出依据：$ (x^2+1)\\sin^3x$，$\\ln(x+\\sqrt{x^2+a^2})$，$\\frac{2^{-x}-2^x}{2^{-x}+2^x}$，$x^2\\sec x+\\csc^2x$。讨论第二个函数在何种 $a$ 下成为奇函数。\n\\end{exercise}\n\\begin{exercise}{16}{抽象函数复合的奇偶性}\n设 $f,g:\\mathbb R\\to\\mathbb R$，$f$ 为奇函数，$g$ 为偶函数。判断 $f\\circ f$、$f\\circ g$、$g\\circ f$、$g\\circ g$ 必然具有的奇偶性并证明。说明“偶函数一定不是奇函数”是否成立。\n\\end{exercise}\n\\begin{exercise}{17}{单调性的直接证明}\n不用导数，证明 $f(x)=x^3+2x+3$ 在 $\\mathbb R$ 上严格单调；进一步确定参数 $a$ 的全部取值，使 $x^3+ax+3$ 仍在 $\\mathbb R$ 上严格递增。\n\\end{exercise}\n\\begin{exercise}{18}{区间上的有界性}\n分别判断 $f(x)=\\frac1{x-2}$ 在 $(2,3)$ 和 $(3,+\\infty)$ 上是否有界；有界时求上确界与下确界，无界时按定义构造使函数值任意大的点。\n\\end{exercise}\n\\begin{exercise}{19}{最小正周期}\n求 $f(x)=2+\\cos^2(2x-1)$ 的最小正周期，并证明不存在更小的正周期。讨论常数项与相位平移是否影响该结论。\n\\end{exercise}\n\\begin{exercise}{20}{取整函数与周期}\n记 $\\lfloor x\\rfloor$ 为不超过 $x$ 的最大整数。对 $f(x)=x-\\lfloor x\\rfloor$，确定其值域、最小正周期，并判断有界性、单调性和奇偶性；写出 $f(-x)$ 与 $f(x)$ 在非整数点的关系。\n\\end{exercise}\n\\begin{exercise}{21}{函数关系与反函数}\n设 $f:(0,+\\infty)\\to\\mathbb R$ 满足 $f(x)+2f(1/x)=x$。求 $f(x)$；选取包含 $1$ 的最大区间，使 $f$ 在该区间上一一对应，并求其反函数及定义域。\n\\end{exercise}\n\\begin{exercise}{22}{周期函数的有界条件}\n设 $f:\\mathbb R\\to\\mathbb R$ 以 $T>0$ 为周期。证明 $f$ 在 $\\mathbb R$ 上有界当且仅当它在 $[0,T)$ 上有界；构造一个无界周期函数，并说明“周期函数必有界”遗漏了什么条件。\n\\end{exercise}\n\\subsection{数列的极限}\n\\begin{exercise}{23}{数列极限定义}\n用 $\\varepsilon$--$N$ 定义证明 $\\lim_{n\\to\\infty}\\frac{n}{2n+1}=\\frac12$，给出可取的 $N(\\varepsilon)$；再求误差小于 $10^{-3}$ 时所需的最小正整数 $n$。\n\\end{exercise}\n\\begin{exercise}{24}{幂数列的参数分类}\n对全部实数 $x$，讨论 $x^n$ 的有限极限、正负无穷趋势或振荡情形。对有限极限不存在的情形，用子列或绝对值增长给出理由。\n\\end{exercise}\n\\begin{exercise}{25}{实指数数列}\n对全部实数 $x$，讨论 $n^x$ 在 $n\\to\\infty$ 时的变化。对 $x<0$ 的情形，用极限定义给出 $N(\\varepsilon,x)$；说明固定 $x$ 的分类结论能否直接用于 $x_n=-1/\\ln(n+1)$。\n\\end{exercise}\n\\begin{exercise}{26}{交错符号数列的定义证明}\n设 $x_{2k-1}=-1/(2k)$、$x_{2k}=2^{-k}$（$k\\ge1$）。判断数列的极限是否存在并用定义证明；比较两种符号的子列各自趋零的速度，说明交错符号与不同衰减速度是否阻碍收敛。\n\\end{exercise}\n\\begin{exercise}{27}{奇偶子列与收敛}\n设 $x_n=\\begin{cases}(n+1)/(n+2),&n\\text{ 为偶数},\\\\1,&n\\text{ 为奇数}.\\end{cases}$ 求其极限，并用统一的误差估计验证；若将奇数项改为常数 $a$，求数列收敛的充要条件。\n\\end{exercise}\n\\begin{exercise}{28}{交错排列的子列判据}\n设 $x_n\\to-1$、$y_n\\to1$，把它们交错排列成 $z_{2n-1}=x_n$、$z_{2n}=y_n$。判断 $z_n$ 是否收敛，并求它的全部子列极限；进一步证明一般情形 $x_n\\to a,y_n\\to b$ 下，$z_n$ 收敛当且仅当 $a=b$。\n\\end{exercise}\n\\begin{exercise}{29}{收敛性质的条件辨析}\n判断并证明或举反例：$x_n\\to a$ 则 $|x_n|\\to|a|$；$|x_n|\\to|a|$ 则 $x_n\\to a$；$x_n\\to a$ 则 $x_{n+1}\\to a$；$x_n\\to a$ 则 $1/x_n\\to1/a$。对最后一个断言补充使其成立的必要限制。\n\\end{exercise}\n\\begin{exercise}{30}{周期振荡数列的子列}\n证明 $x_n=(1+1/n)\\sin(n\\pi/4)$ 不收敛；求其全部子列极限，并说明因子 $1+1/n\\to1$ 为何不能消除周期振荡。\n\\end{exercise}\n\\begin{exercise}{31}{收敛与连续变换}\n设实数列 $x_n$ 满足 $x_n^2\\to1$。证明 $|x_n|\\to1$；给出 $x_n$ 不收敛的例子，并证明增加条件“$x_n$ 从某项起同号”后，$x_n$ 必收敛。\n\\end{exercise}\n\\begin{exercise}{32}{差分趋零的适用范围}\n若 $x_n\\to a$，证明 $x_{n+1}-x_n\\to0$。分别构造无界数列和有界数列，说明该结论的逆命题均不成立；有界例子须给出两个极限不同的子列。\n\\end{exercise}\n\\subsection{函数的极限}\n\\begin{exercise}{33}{函数极限的定义证明}\n用 $\\varepsilon$--$\\delta$ 定义证明 $\\lim_{x\\to1/2}\\frac{1-4x^2}{2x-1}=-2$，给出明确的 $\\delta(\\varepsilon)$。若在 $x=1/2$ 任意补定义一个值，说明该极限是否改变。\n\\end{exercise}\n\\begin{exercise}{34}{无穷远左右方向}\n分别求 $e^{2x-1}$ 与 $\\operatorname{arccot}(1-x)$ 在 $x\\to-\\infty$、$x\\to+\\infty$ 时的极限或无穷趋势，其中 $\\operatorname{arccot}\\in(0,\\pi)$；判断各函数是否存在 $x\\to\\infty$（即 $|x|\\to\\infty$）时的有限极限。\n\\end{exercise}\n\\begin{exercise}{35}{分段点的左右极限}\n设 $f(x)=\\begin{cases}(x+1)\\sin x,&x<0,\\\\1-\\cos x,&x\\ge0.\\end{cases}$ 求 $x=0$ 处的左右极限及双侧极限；若把左支改为 $(x+1)\\sin x+a$，确定双侧极限存在的全部 $a$。\n\\end{exercise}\n\\begin{exercise}{36}{分段极限与定义域方向}\n设 $f(x)=\\begin{cases}\\ln(1-x),&x<1,\\\\1/\\sqrt{2x+1},&x\\ge1.\\end{cases}$ 求 $x\\to1$、$x\\to0$、$x\\to2$ 及 $|x|\\to\\infty$ 时的极限或变化趋势，讨论时须区分各方向。\n\\end{exercise}\n\\begin{exercise}{37}{跳跃、可去点与无穷远极限}\n设 $f(x)=\\begin{cases}x+1,&x<0,\\\\3,&x=0,\\\\2-x,&0<x<1,\\\\0,&x=1,\\\\1+1/x,&x>1.\\end{cases}$ 求 $x\\to0^-$、$x\\to0^+$、$x\\to1$、$x\\to2$ 及 $x\\to+\\infty$ 时的极限，并指出哪些结论不能用直接代入函数值获得。\n\\end{exercise}\n\\begin{exercise}{38}{局部保号性与有界性}\n设 $\\lim_{x\\to1}f(x)/x=-1$。证明存在 $1$ 的去心邻域使 $f(x)<0$ 且有界；举例说明“任意去心邻域内均处处 $f(x)<0$”与“任意去心邻域内均有界”不由条件保证。\n\\end{exercise}\n\\begin{exercise}{39}{极限不等式与量词}\n设 $f(x)\\to A$、$g(x)\\to B$（$x\\to x_0$）。证明：若某去心邻域内 $f(x)<g(x)$，则 $A\\le B$；若 $A<B$，则某去心邻域内 $f(x)<g(x)$。分别举例说明第一结论不能加强为 $A<B$，第二结论不能扩大到所有 $x$；说明极限存在是否要求 $f(x_0)$ 有定义。\n\\end{exercise}\n\\begin{exercise}{40}{无穷远振荡与海涅定理}\n用两列趋于 $+\\infty$ 的点证明 $x\\cos x$ 没有有限极限，并证明它也不趋于绝对值无穷大；再判断 $\\cos x/x$ 在同一变化过程中的极限。\n\\end{exercise}\n\\begin{exercise}{41}{局部有界性的准确范围}\n用极限定义证明：若 $\\lim_{x\\to x_0}f(x)=A\\in\\mathbb R$，则 $f$ 在 $x_0$ 的某去心邻域内有界。若 $f(x_0)$ 也有定义，证明可把去心邻域改为邻域；举例说明局部有界不保证极限存在。\n\\end{exercise}\n\\begin{exercise}{42}{复合极限的条件辨析}\n设 $\\lim_{u\\to0}f(u)=2$、$\\lim_{x\\to0}g(x)=0$。构造例子说明未必有 $f(g(x))\\to2$；证明若 $g(x)$ 在 $0$ 的某去心邻域内处处不等于 $0$，该复合极限成立，并讨论把这一条件换成 $f(0)=2$ 的情形。\n\\end{exercise}\n\\begin{exercise}{43}{海涅定理与局部振荡}\n定义 $f(x)=\\sin(1/x)+ax$（$x\\ne0$），其中 $a\\in\\mathbb R$。用两列趋于 $0$ 的非零点证明 $f$ 在 $0$ 处无极限；求 $xf(x)$ 在 $0$ 处的极限，并给出相应的 $\\varepsilon$--$\\delta$ 估计。\n\\end{exercise}\n\\subsection{无穷小与无穷大}\n\\begin{exercise}{44}{有界振荡与无穷小}\n证明 $2x\\sin(1/x)$ 在 $x\\to0$ 时为无穷小。对参数 $p\\in\\mathbb R$，确定 $|x|^p\\sin(1/x)$ 为无穷小的充要条件，并对不成立的参数给出趋零点列。\n\\end{exercise}\n\\begin{exercise}{45}{无界与无穷大的区别}\n判断 $x\\cos x$ 在 $\\mathbb R$ 上是否无界，以及在 $x\\to+\\infty$ 时是否为无穷大（按绝对值趋于无穷解释）；分别构造点列证明，并说明这两个概念的量词差异。\n\\end{exercise}\n\\begin{exercise}{46}{变化过程与单侧趋势}\n对 $f(x)=e^{1/x}$ 与 $g(x)=x\\arctan x$，分别讨论 $x\\to0^-$、$x\\to0^+$、$x\\to-\\infty$、$x\\to+\\infty$ 时的极限或无穷趋势，指出哪些过程中它们是无穷小或无穷大。\n\\end{exercise}\n\\begin{exercise}{47}{无穷大与局部有界}\n设 $f(x)=\\frac{2x}{x-2}$、$g(x)=\\ln(x+1)$。分别讨论 $x\\to0$、$x\\to2$、$x\\to-1^+$、$x\\to+\\infty$ 时两函数的无穷小、无穷大或局部有界性质；对 $x\\to2$ 须区分有符号极限与绝对值趋于无穷。\n\\end{exercise}\n\\begin{exercise}{48}{乘积趋零的充分条件}\n设 $x_ny_n\\to0$。判断下列断言并证明或举反例：$x_n$ 发散则 $y_n$ 收敛；$x_n$ 无界则 $y_n$ 有界；$x_n$ 有界则 $y_n\\to0$；若 $x_n$ 最终非零且 $1/x_n\\to0$，则 $y_n\\to0$。\n\\end{exercise}\n\\begin{exercise}{49}{有界因子估计}\n求 $\\lim_{x\\to0}\\sin x(2+\\cos(3/x))$ 与 $\\lim_{|x|\\to\\infty}\\frac{\\arctan|2x+1|}{2x+1}$，分别写出能保证结论的绝对值估计；讨论第一个式子中的 $2$ 换成任意固定实数后结论是否改变。\n\\end{exercise}\n\\begin{exercise}{50}{无穷小的判定}\n判定下列各量是否为无穷小，并给出相应极限或增长依据：$\\frac{x^2}{\\sqrt{x^3+1}}$（$x\\to+\\infty$），$\\frac{x^3-1}{2x^4+x^2}(3-2\\sin x)$（$|x|\\to\\infty$），$\\frac{\\sin2x}{x\\sqrt x}$（$x\\to0^+$），$\\frac{\\ln(1+x)}x$（$x\\to0$）。\n\\end{exercise}\n\\begin{exercise}{51}{非负数列的极限推断}\n设非负数列 $x_n\\to0$、$y_n\\to1$、$z_n\\to+\\infty$。证明 $x_n<y_n<z_n$ 最终成立，说明为何不能要求对所有 $n$ 成立；判断 $x_nz_n$ 与 $y_nz_n$ 的变化是否由条件唯一确定，未确定时给出两种不同结果。\n\\end{exercise}\n\\begin{exercise}{52}{由组合极限反推函数}\n已知 $\\lim_{x\\to0}\\left(1+2x+\\frac{f(x)}x\\right)=4$。求 $\\lim_{x\\to0}f(x)$ 及 $\\lim_{x\\to0}f(x)/x$，并用小量形式写出 $f(x)$；说明此条件能否确定 $f(0)$。\n\\end{exercise}\n\\begin{exercise}{53}{无界乘子与反例}\n设 $\\alpha(x)\\to0$（$x\\to0$）。证明有界函数 $b(x)$ 满足 $\\alpha(x)b(x)\\to0$；若仅知 $b$ 在任意去心邻域内无界，分别构造乘积趋零、趋于非零常数和无极限的例子。\n\\end{exercise}\n\\begin{exercise}{54}{倒数关系的定义证明}\n设 $f$ 在 $x_0$ 的某去心邻域内非零。用定义证明 $|f(x)|\\to\\infty$ 当且仅当 $1/f(x)\\to0$。再构造一个满足上述结论却既不趋于 $+\\infty$ 也不趋于 $-\\infty$ 的函数。\n\\end{exercise}\n\\subsection{极限的运算法则}\n\\begin{exercise}{55}{无穷大运算的条件}\n设 $|f(x)|\\to\\infty$、$|g(x)|\\to\\infty$（$x\\to x_0$）。判断 $f+g$ 必为无穷大、$f-g\\to0$、$kf$ 必为无穷大（$k\\ne0$）、$1/(f+g)\\to0$ 四个断言，分别证明或举反例；再说明增加 $f,g\\to+\\infty$ 后哪些结论改变。\n\\end{exercise}\n\\begin{exercise}{56}{有限乘积的极限与误差}\n求 $\\lim_{|x|\\to\\infty}(1-1/x)(2+2/x)(3-3/x)$；记乘积为 $P(x)$，再求 $\\lim_{|x|\\to\\infty}x(P(x)-6)$，解释两次求极限所需信息的差异。\n\\end{exercise}\n\\begin{exercise}{57}{直接代入的合法性}\n求 $\\lim_{x\\to1/2}\\frac{2\\sin x+2\\pi/x}{\\cos2x}$，写明分母非零的依据；进一步讨论该表达式在 $x=0$ 处的左右变化趋势。\n\\end{exercise}\n\\begin{exercise}{58}{差式极限与有理化}\n求 $\\lim_{x\\to1}\\left(\\frac1{x+1}-\\frac3{x^3+1}\\right)$ 与 $\\lim_{n\\to\\infty}(\\sqrt{n+2\\sqrt n}-\\sqrt{n-\\sqrt n})$。将第二式中的 $2,-1$ 换成实数 $a,b$，求一般极限。\n\\end{exercise}\n\\begin{exercise}{59}{零比零型的消因子}\n求 $\\lim_{x\\to2}\\frac{x^2+x-6}{x^2-x-2}$ 与 $\\lim_{x\\to0}\\frac{x^2+x}{\\sqrt{1+x}-1}$；分别补定义函数在相应点的值使其连续，并说明约分、乘共轭式时应保留的定义域限制。\n\\end{exercise}\n\\begin{exercise}{60}{振荡项与最高次幂}\n求 $\\lim_{|x|\\to\\infty}\\frac{2x^2+x\\cos x}{x^3-x\\sin x+1}$，并证明分母在 $|x|$ 充分大时非零；再求原商乘以 $x$ 后的极限。\n\\end{exercise}\n\\begin{exercise}{61}{有限和与几何级数}\n求 $\\lim_{n\\to\\infty}\\sum_{k=1}^n\\frac{k}{n^2+1}$ 与 $\\lim_{n\\to\\infty}\\sum_{k=1}^na^{-k}$（$a>1$）；再分类讨论第二个极限在 $a\\in\\mathbb R\\setminus\\{0\\}$ 下存在有限值的全部情形。\n\\end{exercise}\n\\begin{exercise}{62}{望远镜求和与差式}\n求 $\\lim_{n\\to\\infty}\\sum_{k=1}^n\\ln\\frac{k+1}{k+2}$ 及 $\\lim_{n\\to\\infty}\\left(\\sqrt{\\sum_{k=1}^{n+1}k}-\\sqrt{\\sum_{k=1}^nk}\\right)$，区分有限极限与无穷趋势，并说明能否把第一个式子的极限移入不断增加的各项中。\n\\end{exercise}\n\\begin{exercise}{63}{乘积的对数化}\n设 $f(x)=2^x$。求 $\\lim_{n\\to\\infty}\\frac1{n^2}\\ln\\prod_{k=1}^nf(k)$；再将 $f(x)$ 改为 $2^{x+c}$，证明该极限与固定常数 $c$ 无关。\n\\end{exercise}\n\\begin{exercise}{64}{乘积恒等式与参数范围}\n设 $|a|<1$，求 $\\lim_{n\\to\\infty}\\prod_{k=0}^n(1+a^{2^k})$。先证明有限乘积恒等式，再讨论 $a=1$、$a=-1$ 两个边界参数，说明不能直接沿用内部参数的化简结论。\n\\end{exercise}\n\\begin{exercise}{65}{分式约分后的单侧极限}\n讨论 $f(x)=\\frac{x^2-1}{x+1}e^{1/(x+1)}$ 在 $x\\to-1^-$、$x\\to-1^+$ 时的变化，判断双侧极限是否存在；说明消去公因子是否消除了函数在 $-1$ 附近的全部奇异性。\n\\end{exercise}\n\\begin{exercise}{66}{根式与无穷远方向}\n分别求 $\\sqrt{x^2+x+3}-\\sqrt{x^2-x+3}$ 在 $x\\to+\\infty$、$x\\to-\\infty$ 时的极限，判断 $|x|\\to\\infty$ 时是否有极限，并指出提取 $\\sqrt{x^2}$ 时的注意事项。\n\\end{exercise}\n\\begin{exercise}{67}{幂指函数的连续运算}\n求 $\\lim_{x\\to e}(1+\\sin2x)^{\\ln\\ln x}$，验证实数幂在 $e$ 的某邻域内有定义；再把指数改为 $c+\\ln\\ln x$，求极限关于实数 $c$ 的表达式。\n\\end{exercise}\n\\begin{exercise}{68}{底数趋于非单位常数的幂指极限}\n求 $\\left(\\frac{x^2+x\\cos x-1}{2x^2-x\\sin x}\\right)^{x^2+1}$ 与 $\\left(\\frac{3x+2}{2x-1}\\right)^{x^2}$ 在 $|x|\\to\\infty$ 时的极限或无穷趋势。证明底数最终为正，并用固定常数夹住底数来论证。\n\\end{exercise}\n\\begin{exercise}{69}{有限极限反求参数}\n已知 $\\lim_{x\\to2}\\frac{x^2+ax+b}{x^2-4}=3$，求 $a,b$。先证明分子在 $2$ 处必须为零，再求参数；并写出使该商在 $2$ 处连续的补定义。\n\\end{exercise}\n\\begin{exercise}{70}{对数分母的极限反问题}\n设 $a>0$，求全部实数 $a,b$，使 $\\lim_{x\\to0}\\frac{\\sin2x}{\\ln(a+x)}(\\cos x-b)=4$。分别讨论 $a=1$ 与 $a\\ne1$，验证所得参数使原商在充分小去心邻域内有定义。\n\\end{exercise}\n\\begin{exercise}{71}{无穷远根式抵消的参数}\n设 $a>0$ 且 $\\lim_{x\\to-\\infty}(4x+\\sqrt{ax^2-bx-1})=1$。求 $a,b$，先比较一次增长项，再用有理化求剩余常数；检查改…500 tokens truncated…推式始终确定正数 $x_{n+1}$，且数列严格递减、收敛；求其极限。可使用 $e^t>1+t$（$t\\ne0$），不得先假设极限存在。\n\\end{exercise}\n\\begin{exercise}{80}{积分数列的递推与比值极限}\n设 $a_n=\\int_0^1x^n\\sqrt{1-x^2}\\,\\dd x$（$n\\ge0$）。证明 $a_n$ 严格递减且 $a_n=\\frac{n-1}{n+2}a_{n-2}$（$n\\ge2$）；利用递推式和单调性夹逼求 $\\lim_{n\\to\\infty}a_n/a_{n-1}$，写明正性保证的除法条件。\n\\end{exercise}\n\\begin{exercise}{81}{重要极限与无穷远估计}\n设 $f(x)=\\sin2x/(5x)$（$x\\ne0$）。分别求 $x\\to0$ 与 $|x|\\to\\infty$ 时的极限，并给出所用依据；说明为何同一分式在两个变化过程中需要不同的估计。\n\\end{exercise}\n\\begin{exercise}{82}{重要极限与参数}\n求 $\\lim_{x\\to0}\\frac{\\tan3x}{4x}$；推广求 $\\lim_{x\\to0}\\frac{\\tan(ax)}{bx}$（$a\\in\\mathbb R,b\\ne0$），并说明 $a=0$ 时结论是否仍适用。\n\\end{exercise}\n\\begin{exercise}{83}{反三角函数的换元极限}\n不用洛必达法则，求 $\\lim_{x\\to0}\\frac{\\arcsin2x}{x}$ 和 $\\lim_{x\\to0}\\frac{\\arctan x}{2x}$；分别说明换元后自变量趋于零的依据及反三角函数的取值范围。\n\\end{exercise}\n\\begin{exercise}{84}{同一表达式的不同变化过程}\n分别求 $\\frac{2x-\\sin3x}{2x+\\sin4x}$ 在 $x\\to0$ 与 $|x|\\to\\infty$ 时的极限。再确定实数 $a$ 的全部取值，使 $\\lim_{x\\to0}\\frac{ax-\\sin3x}{ax+\\sin4x}$ 有有限值，并求该值。\n\\end{exercise}\n\\begin{exercise}{85}{复合零点的因式分解}\n求 $\\lim_{x\\to3}\\frac{\\sin(x^2-2x-3)}{x-3}$；再讨论 $x\\to-1$ 时同一分式的极限。将正弦的自变量因式分解，说明两个零点处的分母是否同时趋零。\n\\end{exercise}\n\\begin{exercise}{86}{余弦差与阶数}\n求 $\\lim_{x\\to0}\\frac{1-\\cos2x}{x^2}$；进一步分类讨论 $\\lim_{x\\to0}\\frac{1-\\cos2x}{|x|^p}$（$p\\in\\mathbb R$），说明何时为非零有限值。\n\\end{exercise}\n\\begin{exercise}{87}{固定参数与变动参数}\n对固定实数 $x$，求 $\\lim_{n\\to\\infty}n^2\\sin\\frac{x^2+1}{n^2}$。再令 $x=n$，判断能否把固定参数的结论直接用于此时的表达式，并求该表达式除以 $n^2$ 后的极限。\n\\end{exercise}\n\\begin{exercise}{88}{幂指型极限}\n求 $\\lim_{|x|\\to\\infty}(1-2/x)^{2x+100}$，证明底数最终为正；再将指数中的 $100$ 换为 $c x$，求极限关于实数 $c$ 的表达式。\n\\end{exercise}\n\\begin{exercise}{89}{商底数的幂指极限}\n求 $\\lim_{|x|\\to\\infty}\\left(\\frac{x+1}{x-1}\\right)^{2x}$；推广求 $\\lim_{|x|\\to\\infty}\\left(\\frac{x+a}{x+b}\\right)^{cx}$，其中 $a,b,c$ 为固定实数，并说明实数幂的定义条件最终成立。\n\\end{exercise}\n\\begin{exercise}{90}{二次尺度的重要极限}\n求 $\\lim_{|x|\\to\\infty}\\left(\\frac{2x^2-1}{2x^2+1}\\right)^{x^2}$。若把指数 $x^2$ 改为 $|x|^p$，对实数 $p$ 分类讨论极限。\n\\end{exercise}\n\\begin{exercise}{91}{对数等价量与参数}\n设 $k\\ne0$，求 $\\lim_{x\\to0}\\frac{\\sin3x}{\\ln(1+kx)}$；证明对数在 $0$ 的某邻域内有定义。再讨论当 $k>0$、$x\\to+\\infty$ 时该商的极限，区分局部等价量的适用过程。\n\\end{exercise}\n\\begin{exercise}{92}{取对数与符号控制}\n求 $\\lim_{x\\to0}(1+\\tan2x)^{-3/x}$，并验证底数在 $0$ 的某邻域内为正；推广求 $(1+\\tan ax)^{b/x}$ 的极限，其中 $a,b\\in\\mathbb R$。\n\\end{exercise}\n\\begin{exercise}{93}{指数与底数的共同变化}\n求 $\\lim_{x\\to0}(\\cos x)^{-1/\\sin x}$ 和 $\\lim_{x\\to0}\\left(\\frac{\\tan x}{x}\\right)^{1/x}$。将两式的指数分别改为 $-1/\\sin^2x$ 和 $1/x^2$，再求极限，比较一阶与二阶尺度。\n\\end{exercise}\n\\begin{exercise}{94}{幂平均的局部极限}\n设 $a,b>0$，求 $\\lim_{x\\to0}\\left(\\frac{a^x+b^x}{2}\\right)^{1/x}$；推广到 $\\left(\\lambda a^x+(1-\\lambda)b^x\\right)^{1/x}$（$0\\le\\lambda\\le1$），说明端点权重情形。\n\\end{exercise}\n\\begin{exercise}{95}{对数与幂的括号范围}\n设 $a\\ne\\frac12$，求 $\\lim_{n\\to\\infty}\\ln\\left[\\left(\\frac{n-2an-1}{n(1-2a)}\\right)^n\\right]$，说明对数为何最终有定义；再求幂本身的极限。\n\\end{exercise}\n\\begin{exercise}{96}{幂指极限反求参数}\n求全部实数对 $(a,b)$，使 $\\lim_{|x|\\to\\infty}\\left(\\frac{x^2}{(x-a)(x+b)}\\right)^x=e^2$。证明所得条件充分且必要，并检查底数最终为正。\n\\end{exercise}\n\\begin{exercise}{97}{递推极限与初值}\n设 $x_1\\ge0$、$x_{n+1}=\\sqrt{2+x_n}$。分别讨论 $0\\le x_1<2$、$x_1=2$、$x_1>2$ 的单调性，证明数列收敛并求极限；当 $x_1\\ne2$ 时给出 $|x_{n+1}-2|/|x_n-2|$ 的极限。\n\\end{exercise}\n\\begin{exercise}{98}{重要极限中的高阶修正}\n对实数 $a,b$，求 $\\lim_{x\\to0}(1+ax+bx^2)^{1/x}$；当 $a=0$ 时，再求 $\\lim_{x\\to0}(1+bx^2)^{1/x^2}$。各情形均须说明底数在充分小邻域内的正性。\n\\end{exercise}\n\\subsection{无穷小的比较}\n\\begin{exercise}{99}{以根式为基准比较阶数}\n在 $x\\to0^+$ 时，分别求 $e^{\\sqrt x}-1$、$\\ln(1+\\sqrt x)$、$1-\\cos\\sqrt x$、$\\arctan\\sqrt x$ 与 $\\sqrt x$ 的比值极限；对不等价者给出其关于 $\\sqrt x$ 的阶数与首项。\n\\end{exercise}\n\\begin{exercise}{100}{不同阶无穷小的比较}\n当 $x\\to0$ 时，分别求 $\\arctan2x$、$\\sqrt{1+x}-1$、$1-\\cos2x$、$\\tan x-\\sin x$ 的首个非零等价项，按阶数排序并指出最高阶者；说明同阶是否必然等价。\n\\end{exercise}\n\\begin{exercise}{101}{无穷远的等价量}\n求 $\\lim_{|x|\\to\\infty}\\frac{2x-3}{x^2-x+1}$；进一步求 $x\\frac{2x-3}{x^2-x+1}$ 的极限，并写出原商相对于 $1/x$ 的等价关系。\n\\end{exercise}\n\\begin{exercise}{102}{指数差的消去阶数}\n当 $x\\to0$ 时，确定使 $e^{x\\cos x^2}-e^x$ 与 $x^n$ 同阶的正整数 $n$，并求两者比值的极限；论证时须保留指数差中首先不为零的项。\n\\end{exercise}\n\\begin{exercise}{103}{三阶等价无穷小}\n证明 $\\tan x-x\\sim x^3/3$（$x\\to0$）；利用此结论求 $\\lim_{x\\to0}\\frac{\\tan(ax)-a\\tan x}{x^3}$，并讨论实数 $a$ 使极限为零的全部情形。\n\\end{exercise}\n\\begin{exercise}{104}{高阶无穷小与首项}\n证明 $(2^{x^2}-1)\\arctan2x=o(x^2)$（$x\\to0$）；再求其与 $x^3$ 的比值极限，说明“高于二阶”是否意味着“高于三阶”。\n\\end{exercise}\n\\begin{exercise}{105}{等价关系能确定的参数信息}\n求全部实数 $a,b,c$，使 $\\frac1{ax^2+bx+c}\\sim\\frac1{2x^2+1}$（$|x|\\to\\infty$）。若进一步要求两式之差为 $o(x^{-4})$，再求参数；说明增强前后分别约束了哪些系数。\n\\end{exercise}\n\\begin{exercise}{106}{含实参数幂的阶数比较}\n当 $x\\to0^+$ 时，求全部实数 $k$，使 $(\\sqrt{1+x^2}-1)\\ln(1+x^2)=o\\bigl(x(\\arcsin x)^k\\bigr)$；再讨论临界参数时的比值极限。\n\\end{exercise}\n\\begin{exercise}{107}{乘积中的高阶消去}\n求 $\\lim_{x\\to0}\\frac{(\\sin x-\\tan x)(e-e^{\\cos x})}{(2x+1)\\sin^5x}$。分别写出分子两个因子的等价首项，并说明为何不能把 $\\sin x$ 与 $\\tan x$ 都代换成 $x$ 后相减。\n\\end{exercise}\n\\begin{exercise}{108}{等价关系反求两个参数}\n设 $ab\\ne0$，当 $x\\to0$ 时 $x-\\sin(ax)\\sim x^2\\ln(1-bx)$。求 $a,b$ 并验证；说明为何必须先排除分子的一阶项，再比较三阶项。\n\\end{exercise}\n\\begin{exercise}{109}{对数极限反推原函数}\n设 $a>0$、$a\\ne1$，且 $\\lim_{x\\to0}\\frac{\\ln(1+f(x)/\\sin^2x)}{a^2-1}=A\\in\\mathbb R$，原式在充分小去心邻域内有定义。求 $\\lim_{x\\to0}f(x)/x^2$；分别讨论 $A=0$ 与 $A\\ne0$ 时能否直接使用 $\\ln(1+u)\\sim u$。\n\\end{exercise}\n\\begin{exercise}{110}{已知高阶余项反求极限}\n已知 $\\lim_{x\\to0}\\frac{\\sin6x+xf(x)}{x^3}=0$，求 $\\lim_{x\\to0}\\frac{6+f(x)}{x^2}$；再写出 $f(x)$ 到 $x^2$ 阶的渐近表达式，并说明是否能据此确定 $f(0)$。\n\\end{exercise}\n\\begin{exercise}{111}{振荡余项的阶估计}\n求 $\\lim_{x\\to0}\\frac{4\\sin x+3x^2\\cos(1/x^2)}{(1+\\cos x)\\ln(1+2x)}$。若把分子中的 $x^2$ 改为 $|x|^p$，确定极限仍等于原值的全部实数 $p$，对边界情形说明理由。\n\\end{exercise}\n\\begin{exercise}{112}{根式差与三阶比较}\n求 $\\lim_{x\\to0}\\frac{\\sqrt{1+\\tan x}-\\sqrt{1+\\sin x}}{x\\ln(1+x)-x^2}$；指出两个差式各自的首个非零阶，并验证根式和对数在充分小邻域内有定义。\n\\end{exercise}\n\\begin{exercise}{113}{指数相近时的四阶消去}\n求 $\\lim_{x\\to0}\\frac{e^{x^2}-e^{2-2\\cos x}}{x^3\\sin x}$；写出两个指数之差的首个非零项，并说明分别只保留指数到二阶会丢失什么信息。\n\\end{exercise}\n\\begin{exercise}{114}{对数差的等价转化}\n求 $\\lim_{x\\to0}\\frac{\\ln(\\sin^2x+e^{2x})-2x}{\\ln(x^2+e^{3x})-3x}$。先把每个对数差改写为 $\\ln(1+u)$ 型，再说明相减结构下允许等价代换的具体位置。\n\\end{exercise}\n\\begin{exercise}{115}{无穷远复合等价量}\n求 $\\lim_{|x|\\to\\infty}x\\left[\\sin\\ln(1+4/x)-\\sin\\ln(1+1/x)\\right]$；将 $4,1$ 换为实数 $a,b$，求一般结果，并证明两个对数最终有定义。\n\\end{exercise}\n\\begin{exercise}{116}{积分无穷小的阶数比较}\n在 $x\\to0^+$ 时，求 $\\int_0^x(e^t-1)\\,\\dd t$、$\\int_0^x\\ln(1+\\sqrt{t^2})\\,\\dd t$、$\\int_0^x\\sin(t^2)\\,\\dd t$、$\\int_0^x\\sqrt{\\sin^2t}\\,\\dd t$ 的等价首项，按阶数排序并找出最高阶者。说明两个根式在正半轴上如何化简。\n\\end{exercise}\n\\begin{exercise}{117}{极限减去常数后的阶数}\n设 $f(x)=\\frac{1+x}{\\sin x}-\\frac1x$，$a=\\lim_{x\\to0}f(x)$。求 $a$；确定使 $f(x)-a$ 与 $x^k$ 同阶的正整数 $k$，并求比值极限；说明分子分母主项相消后应保留到哪一阶。\n\\end{exercise}\n\\begin{exercise}{118}{积分分母的非零有限极限}\n求全部常数 $a,b,c$（$c\\ne0$），使 $\\lim_{x\\to0}\\frac{ax-\\sin(bx)}{\\int_0^x\\ln(1+t^2)\\,\\dd t}=c$。先比较阶数再确定系数关系，并验证所求关系足以保证极限存在。\n\\end{exercise}\n\\begin{exercise}{119}{加减式中等价代换的限度}\n已知 $\\alpha\\sim\\beta$、$\\gamma\\sim\\delta$（$x\\to0$），说明是否必有 $\\alpha-\\gamma\\sim\\beta-\\delta$，并给出反例。再求 $\\lim_{x\\to0}\\frac{\\sin x-x\\cos x}{\\tan x-x}$，用首项说明相消时需要保留到哪一阶。\n\\end{exercise}\n\\begin{exercise}{120}{参数控制的阶数跃迁}\n设 $F_a(x)=\\ln(1+x)-x+ax^2$。对所有实数 $a$，求 $F_a(x)$ 在 $x\\to0$ 时的首个非零等价项，并确定其阶数；求全部 $(a,c)$，使 $F_a(x)\\sim cx^3$ 且 $c\\ne0$。\n\\end{exercise}\n\\subsection{函数的连续性与间断点}\n\\begin{exercise}{121}{差商极限与连续性}\n已知 $f$ 在 $1$ 处连续，且 $\\lim_{x\\to1}\\frac{f(x)-4}{x-1}=A\\in\\mathbb R$。求 $f(1)$，证明 $f$ 在 $1$ 处可导并求其导数；去掉连续性条件后，说明极限条件还可以推出哪些结论。\n\\end{exercise}\n\\begin{exercise}{122}{连续性的定义证明}\n用 $\\varepsilon$--$\\delta$ 定义证明 $f(x)=2x^2-x+1$ 在任意实数 $x_0$ 处连续，并给出依赖 $\\varepsilon,x_0$ 的明确 $\\delta$；说明该估计是否可在固定闭区间上统一选取。\n\\end{exercise}\n\\begin{exercise}{123}{连续延拓及原式的定义范围}\n设 $f(x)=\\begin{cases}(e^{2x}-1)/\\sin4x,&x\\ne0,\\\\k,&x=0.\\end{cases}$ 在 $0$ 的充分小邻域内定义。求使其在 $0$ 处连续的 $k$；列出非零分母零点，判断仅确定 $k$ 能否使原表达式在整个 $\\mathbb R$ 上有定义且连续。\n\\end{exercise}\n\\begin{exercise}{124}{分段点的连续性与单侧修复}\n设 $f(x)=\\begin{cases}\\frac{\\sin2x}{\\tan x}(1+x^2),&x>0,\\\\2,&x=0,\\\\\\ln\\sqrt{1-2x},&x<0.\\end{cases}$，各支在 $0$ 的充分小邻域内考虑。判断 $f$ 在 $0$ 处的连续性；若只允许给左支加常数 $c$，求能使函数连续的全部 $c$。\n\\end{exercise}\n\\begin{exercise}{125}{振荡因子的连续延拓}\n讨论 $f(x)=\\begin{cases}(x-1)^2\\cos\\frac1{x-1},&x<1,\\\\(x+1)\\ln x,&x\\ge1\\end{cases}$ 在定义域内的连续性；若把左支中的 $(x-1)^2$ 改为 $|x-1|^p$，确定在 $1$ 处连续的全部实数 $p$。\n\\end{exercise}\n\\begin{exercise}{126}{根式与反三角函数的延拓}\n为 $f(x)=\\frac{\\sqrt{1+x^2}-\\sqrt{1-x^2}}{x\\arcsin x}$ 补定义 $f(0)$，使其在 $0$ 处连续；写出延拓后函数的定义域，并判断它在定义域的端点是否连续。\n\\end{exercise}\n\\begin{exercise}{127}{由数列极限定义的函数}\n对 $x>0$，设 $f(x)=\\lim_{n\\to\\infty}\\frac1n\\ln(e^{nx}+x^2)$。求 $f(x)$ 并讨论其连续性；若按同一极限式将定义范围扩大到 $\\mathbb R$，求扩展后的分段表达式并判断 $0$ 处是否连续。\n\\end{exercise}\n\\begin{exercise}{128}{连续函数值的反推}\n设 $f$ 在 $0$ 的某邻域内连续，在充分小的 $x>0$ 时原商有定义，且 $\\lim_{x\\to0^+}\\frac{1-\\cos(\\sqrt x\\,f(x))}{(e^{2x}-1)f(x)}=\\frac12$。求 $f(0)$；证明时须同时考虑 $f(0)=0$ 与 $f(0)\\ne0$，不能未经论证就约去可能趋零的量。\n\\end{exercise}\n\\begin{exercise}{129}{有理函数的间断点}\n求 $f(x)=\\frac{x^2-1}{x^2-3x+2}$ 的全部间断点并分类；对可去间断点作连续延拓，对其余间断点写出左右变化趋势，说明二者不能采用同一补定义方式处理。\n\\end{exercise}\n\\begin{exercise}{130}{指数分式的间断点分类}\n求 $f(x)=\\frac1{e^{x/(x-1)}-1}$ 的全部间断点，计算各自的左右极限或无穷趋势并分类；判断每一点能否通过补定义成为连续点。\n\\end{exercise}\n\\begin{exercise}{131}{可去间断点的参数条件}\n设 $f(x)=\\begin{cases}\\frac{x^2\\sin(1/(2x))}{2^x-1},&x<0,\\\\b,&x=0,\\\\a+\\frac{\\ln(1+3x)}x,&x>0.\\end{cases}$ 求使 $0$ 为可去间断点的全部参数对 $(a,b)$；再求使其在 $0$ 连续的参数对，说明可去间断点与连续点对 $b$ 的要求。\n\\end{exercise}\n\\begin{exercise}{132}{点态极限与间断点}\n设 $f(x)=\\lim_{n\\to\\infty}\\frac{1+x}{1+x^{2n}}$。求其分段表达式、全部连续区间及间断点类型；说明为何不能从各个近似函数连续直接推断 $f$ 连续。\n\\end{exercise}\n\\begin{exercise}{133}{幂平均极限与最大值函数}\n设 $a_1,\\ldots,a_m>0$，证明 $\\lim_{n\\to\\infty}(a_1^n+\\cdots+a_m^n)^{1/n}=\\max_{1\\le i\\le m}a_i$。据此求 $f(x)=\\lim_{n\\to\\infty}\\bigl(1+x^n+(x^2/2)^n\\bigr)^{1/n}$（$x\\ge0$）的分段表达式，并讨论其连续性。\n\\end{exercise}\n\\begin{exercise}{134}{连续与可去间断的参数分类}\n设 $f(x)=\\begin{cases}\\frac{\\ln(1+ax^3)}{x-\\arcsin x},&x<0,\\\\6,&x=0,\\\\\\frac{e^{ax}+x^2-ax-1}{x\\tan(x/4)},&x>0,\\end{cases}$ 各支在 $0$ 的充分小邻域内考虑。求使 $f$ 在 $0$ 连续的全部 $a$，以及使 $0$ 为可去间断点的全部 $a$；给出各情形的左右极限。\n\\end{exercise}\n\\begin{exercise}{135}{参数极限生成函数}\n对 $\\sin x\\ne0$ 的实数 $x$，设 $f(x)=\\lim_{t\\to x}\\left(\\frac{\\sin t}{\\sin x}\\right)^{x/(\\sin t-\\sin x)}$，极限沿表达式有定义的 $t$ 取。求 $f(x)$，找出其定义域边界上的间断点并分类；区分 $x=0$ 与其他 $\\pi$ 的整数倍。\n\\end{exercise}\n\\begin{exercise}{136}{稠密分段与连续点}\n设 $f(x)=\\begin{cases}x^2,&x\\in\\mathbb Q,\\\\ax+b,&x\\notin\\mathbb Q.\\end{cases}$ 求其全部连续点关于参数 $a,b$ 的分类；给出恰有两个连续点的参数，并证明该函数不可能在任何非退化区间上连续。\n\\end{exercise}\n\\begin{exercise}{137}{振荡函数的参数延拓}\n设 $f_{p,c}(x)=\\begin{cases}|x|^p\\sin(1/x),&x\\ne0,\\\\c,&x=0.\\end{cases}$ 对全部实数 $p,c$，讨论 $0$ 处的连续性与间断点类型；对 $p<0$，说明为什么函数在每个邻域内无界仍不构成无穷间断点的充分条件。\n\\end{exercise}\n\\subsection{连续函数的运算与初等函数的连续性}\n\\begin{exercise}{138}{连续运算的分母条件}\n设 $f(x)=\\frac{\\lg(100+x^2)}{a^2+\\arcsin2x}$。分别讨论 $a\\ne0$ 与 $a=0$ 时 $x\\to0$ 的双侧极限或单侧趋势，说明何时可直接使用连续函数商的法则。\n\\end{exercise}\n\\begin{exercise}{139}{间断性在运算中的保留}\n设 $f$ 在 $\\mathbb R$ 上连续且处处非零，$\\varphi:\\mathbb R\\to\\mathbb R$ 有间断点。判断 $\\varphi\\circ f$、$f\\circ\\varphi$、$\\varphi^2$、$\\varphi/f$ 是否必有间断点；必然成立者证明，其余给出满足全部条件的反例。\n\\end{exercise}\n\\begin{exercise}{140}{反函数连续性的条件}\n设 $f$ 在闭区间 $[a,b]$ 上连续且严格递增。证明 $f^{-1}$ 在 $[f(a),f(b)]$ 上连续，端点按单侧连续理解；举例说明仅有严格递增而无连续性时，函数值域可能不是区间。\n\\end{exercise}\n\\begin{exercise}{141}{连续复合与零点集合}\n设 $f$ 在 $[a,b]$ 上连续。证明 $g(x)=\\max\\{f(x),0\\}$ 与 $h(x)=|f(x)|$ 连续；再证明若 $f$ 处处非零，则 $1/f$ 在该区间上连续且有界，并指出闭区间条件在有界性结论中的作用。\n\\end{exercise}\n\\subsection{闭区间上连续函数的性质}\n\\begin{exercise}{142}{三次方程的实根个数}\n证明方程 $x^3-9x-2=0$ 恰有三个不同实根，并将每个根定位在一个长度为 $1$ 且互不相交的开区间内；分别说明“至少三个”与“至多三个”的依据。\n\\end{exercise}\n\\begin{exercise}{143}{零点存在与唯一性}\n证明方程 $x=\\frac12\\cos x$ 在 $\\mathbb R$ 上恰有一个实根，并给出长度不超过 $1/2$ 的含根闭区间；存在性与唯一性须分别论证。\n\\end{exercise}\n\\begin{exercise}{144}{平移差函数与零点}\n设 $f$ 在 $[0,1]$ 上连续且 $f(0)=f(1)$。证明存在 $\\xi\\in[0,1/2]$，使 $f(\\xi+1/2)=f(\\xi)$；说明为何平移差函数只能先定义在 $[0,1/2]$ 上。\n\\end{exercise}\n\\begin{exercise}{145}{半无限区间的有界性}\n设 $f$ 在 $[a,+\\infty)$ 上连续，且 $\\lim_{x\\to+\\infty}f(x)=L\\in\\mathbb R$。证明 $f$ 有界；再分别举例说明它未必取得最大值、未必取得最小值。\n\\end{exercise}\n\\begin{exercise}{146}{加权平均与介值性}\n设 $f$ 在 $[a,b]$ 上连续，$a<x_1<x_2<x_3<b$。证明存在 $\\xi\\in(a,b)$ 使 $f(x_1)+2f(x_2)+3f(x_3)=6f(\\xi)$；若三点函数值不全相同，证明可取 $\\xi\\in(x_1,x_3)$。\n\\end{exercise}\n\\begin{exercise}{147}{开区间端点与有界性}\n设 $f(x)=\\frac{x\\sin(x-2)}{|x|(x-1)(x-2)^2}$。分别判断它在 $(-1,0)$、$(0,1)$、$(1,2)$、$(2,3)$ 内是否有界；有界情形用连续延拓或明确估计证明，无界情形给出导致无界的端点趋势。\n\\end{exercise}\n\\begin{exercise}{148}{等分平移与望远镜求和}\n设 $f$ 在 $[0,1]$ 上连续且 $f(0)=f(1)$。证明对每个正整数 $n$，存在 $x_0\\in[0,1-1/n]$ 使 $f(x_0)=f(x_0+1/n)$。可考虑平移差函数在等分点上的和，并说明 $n=1$ 的情形。\n\\end{exercise}\n\\begin{exercise}{149}{闭区间自映射的不动点}\n设连续函数 $f:[a,b]\\to[a,b]$，其中 $a<b$。证明至少存在一点 $\\xi\\in[a,b]$ 使 $f(\\xi)=\\xi$；若另有 $|f(x)-f(y)|\\le q|x-y|$（$0\\le q<1$），证明不动点唯一；举例说明仅连续时唯一性可能不成立。\n\\end{exercise}\n\\begin{exercise}{150}{严格不等式的统一余量}\n设 $f,g$ 在 $[a,b]$ 上连续且处处 $f(x)<g(x)$。证明存在 $\\eta>0$，使所有 $x\\in[a,b]$ 均满足 $f(x)+\\eta\\le g(x)$；再给出开区间 $(a,b)$ 上的反例，说明逐点严格不等式未必给出统一正余量。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:11:56Z




## tool · 2026-10-20T03:12:01Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 10048)
Total output lines: 2

{"chunk_id":"72f025","wall_time_seconds":0.000008333,"exit_code":0,"original_token_count":1268,"output":"\\begin{exercise}{67}{幂指函数的连续运算}\n求 $\\lim_{x\\to e}(1+\\sin2x)^{\\ln\\ln x}$，验证实数幂在 $e$ 的某邻域内有定义；再把指数改为 $c+\\ln\\ln x$，求极限关于实数 $c$ 的表达式。\n\\end{exercise}\n\\begin{exercise}{68}{底数趋于非单位常数的幂指极限}\n求 $\\left(\\frac{x^2+x\\cos x-1}{2x^2-x\\sin x}\\right)^{x^2+1}$ 与 $\\left(\\frac{3x+2}{2x-1}\\right)^{x^2}$ 在 $|x|\\to\\infty$ 时的极限或无穷趋势。证明底数最终为正，并用固定常数夹住底数来论证。\n\\end{exercise}\n\\begin{exercise}{69}{有限极限反求参数}\n已知 $\\lim_{x\\to2}\\frac{x^2+ax+b}{x^2-4}=3$，求 $a,b$。先证明分子在 $2$ 处必须为零，再求参数；并写出使该商在 $2$ 处连续的补定义。\n\\end{exercise}\n\\begin{exercise}{70}{对数分母的极限反问题}\n设 $a>0$，求全部实数 $a,b$，使 $\\lim_{x\\to0}\\frac{\\sin2x}{\\ln(a+x)}(\\cos x-b)=4$。分别讨论 $a=1$ 与 $a\\ne1$，验证所得参数使原商在充分小去心邻域内有定义。\n\\end{exercise}\n\\begin{exercise}{71}{无穷远根式抵消的参数}\n设 $a>0$ 且 $\\lim_{x\\to-\\infty}(4x+\\sqrt{ax^2-bx-1})=1$。求 $a,b$，先比较一次增长项，再用有理化求剩余常数；检查改为 $x\\to+\\infty$ 时能否有相同结论。\n\\end{exercise}\n\\begin{exercise}{72}{根式渐近展开反求系数}\n求常数 $a,b$，使 $\\lim_{|x|\\to\\infty}(\\sqrt{x^4+2x^2+3}-ax^2-b)=0$；再求所得差式乘以 $x^2$ 后的极限，说明前两个系数确定后尚余何阶误差。\n\\end{exercise}\n\\begin{exercise}{73}{运算法则的逆向条件}\n设 $f(x)+g(x)\\to3$、$f(x)g(x)\\to2$（$x\\to0$）。证明 $f,g$ 在某去心邻域内有界；构造两者均无极限的例子。若再知该邻域内 $f(x)\\le g(x)$，求两者极限。\n\\end{exercise}\n\\begin{exercise}{74}{根式抵消的参数分类}\n对实数 $a,b$，分类讨论 $\\lim_{x\\to+\\infty}(\\sqrt{x^2+ax+b}-x)$，并求 $\\lim_{x\\to+\\infty}x(\\sqrt{x^2+ax+b}-x-a/2)$。证明表达式在充分大的 $x$ 上有实数意义。\n\\end{exercise}\n\\subsection{极限存在准则与两个重要极限}\n\\begin{exercise}{75}{阶乘增长与夹逼}\n求 $\\lim_{n\\to\\infty}\\frac{3^n}{n!}\\sin\\frac1n$；不用斯特林公式，证明存在常数 $C>0$，使充分大的 $n$ 满足 $3^n/n!\\le C(1/2)^n$。\n\\end{exercise}\n\\begin{exercise}{76}{变上限和的统一估计}\n证明 $\\lim_{n\\to\\infty}\\sum_{k=1}^n\\frac{k}{n^2+2n+k}=\\frac12$；给出上下界，并由此估计该和与 $1/2$ 的误差为 $O(1/n)$。\n\\end{exercise}\n\\begin{exercise}{77}{逐渐缩小相位差的夹逼}\n求 $\\lim_{x\\to+\\infty}\\bigl(\\cos\\sqrt{x+1}-\\cos\\sqrt x\\bigr)$。用三角恒等式和根式差估计证明，不得分别给两个振荡项取极限；再讨论将 $1$ 换成固定实数 $a$ 的情形。\n\\end{exercise}\n\\begin{exercise}{78}{递推数列的收敛证明}\n设 $x_1>0$、$x_{n+1}=\\frac12(x_n+4/x_n)$。证明从第二项起 $x_n\\ge2$ 且单调，求其极限；再导出 $x_{n+1}-2$ 与 $x_n-2$ 的精确关系，说明初值小于 $2$ 时第一步的变化。\n\\end{exercise}\n\\begin{exercise}{79}{指数递推与不等式}\n设 $x_1>0$、$x_ne^{x_{n+1}}=e^{x_n}-1$。证明递推式始终确定正数 $x_{n+1}$，且数列严格递减、收敛；求其极限。可使用 $e^t>1+t$（$t\\ne0$），不得先假设极限存在。\n\\end{exercise}\n\\begin{exercise}{80}{积分数列的递推与比值极限}\n设 $a_n=\\int_0^1x^n\\sqrt{1-x^2}\\,\\dd x$（$n\\ge0$）。证明 $a_n$ 严格递减且 $a_n=\\frac{n-1}{n+2}a_{n-2}$（$n\\ge2$）；利用递推式和单调性夹逼求 $\\lim_{n\\to\\infty}a_n/a_{n-1}$，写明正性保证的除法条件。\n\\end{exercise}\n\\begin{exercise}{81}{重要极限与无穷远估计}\n设 $f(x)=\\sin2x/(5x)$（$x\\ne0$）。分别求 $x\\to0$ 与 $|x|\\to\\infty$ 时的极限，并给出所用依据；说明为何同一分式在两个变化过程中需要不同的估计。\n\\end{exercise}\n\\begin{exercise}{82}{重要极限与参数}\n求 $\\lim_{x\\to0}\\frac{\\tan3x}{4x}$；推广求 $\\lim_{x\\to0}\\frac{\\tan(ax)}{bx}$（$a\\in\\mathbb R,b\\ne0$），并说明 $a=0$ 时结论是否仍适用。\n\\end{exercise}\n\\begin{exercise}{83}{反三角函数的换元极限}\n不用洛必达法则，求 $\\lim_{x\\to0}\\frac{\\arcsin2x}{x}$ 和 $\\lim_{x\\to0}\\frac{\\arctan x}{2x}$；分别说明换元后自变量趋于零的依据及反三角函数的取值范围。\n\\end{exercise}\n\\begin{exercise}{84}{同一表达式的不同变化过程}\n分别求 $\\frac{2x-\\sin3x}{2x+\\sin4x}$ 在 $x\\to0$ 与 $|x|\\to\\infty$ 时的极限。再确定实数 $a$ 的全部取值，使 $\\lim_{x\\to0}\\frac{ax-\\sin3x}{ax+\\sin4x}$ 有有限值，并求该值。\n\\end{exercise}\n\\begin{exercise}{85}{复合零点的因式分解}\n求 $\\lim_{x\\to3}\\frac{\\sin(x^2-2x-3)}{x-3}$；再讨论 $x\\to-1$ 时同一分式的极限。将正弦的自变量因式分解，说明两个零点处的分母是否同时趋零。\n\\end{exercise}\n\\begin{exercise}{86}{余弦差与阶数}\n求 $\\lim_{x\\to0}\\frac{1-\\cos2x}{x^2}$；进一步分类讨论 $\\lim_{x\\to0}\\frac{1-\\cos2x}{|x|^p}$（$p\\in\\mathbb R$），说明何时为非零有限值。\n\\end{exercise}\n"}
{"chunk_id":"6bbc5d","wall_time_seconds":0.000007708,"exit_code":0,"original_token_count":8378,"output":"\\section{第2章 导数与微分}\n\\subsection{导数的基本概念}\n\\begin{exercise}{151}{定义求导与线性主部}\n用导数定义求 $f(x)=1+2x+3x^2$ 的 $f'(1)$，并把 $f(1+h)-f(1)$ 写成线性主部与余项之和，验证余项为 $o(h)$。\n\\end{exercise}\n\\begin{exercise}{152}{零因子处的导数}\n设 $f(x)=x(2x+1)(3x+2)(4x+3)$。不展开多项式，求 $f'(0)$；再求 $f'(-1/2)$，说明在单零点处如何利用其余因子的连续性。\n\\end{exercise}\n\\begin{exercise}{153}{定义求导与零点因子}\n设 $f(x)=x(x-2)\\sqrt{\\frac{3x^2+1}{2x^2+1}}$。用导数定义求 $f'(0)$、$f'(2)$，并分别写出曲线在这两点的切线方程。\n\\end{exercise}\n\\begin{exercise}{154}{补定义函数的导数}\n设 $f(x)=\\begin{cases}\\sin^2x/(2x),&x\\ne0,\\\\0,&x=0.\\end{cases}$ 用定义求 $f'(0)$；若把 $f(0)$ 改为参数 $c$，确定在 $0$ 处连续、可导各需要什么条件。\n\\end{exercise}\n\\begin{exercise}{155}{连续因子与乘积可导}\n设 $f(x)=(x^2-1)\\varphi(x-1)$，$\\varphi$ 在 $0$ 处连续。证明 $f$ 在 $1$ 处可导并求 $f'(1)$；构造 $\\varphi$ 在 $0$ 处不可导而该结论仍成立的例子。\n\\end{exercise}\n\\begin{exercise}{156}{平移函数关系的导数}\n设 $f$ 在 $0$ 处可导，$f'(0)=1/2$，且对所有实数 $x$ 有 $f(2+x)=2f(x)$。用定义求 $f'(2)$；进一步证明 $f$ 在所有偶整数点可导，并求 $f'(2n)$（$n\\in\\mathbb Z$）。\n\\end{exercise}\n\\begin{exercise}{157}{差商极限与点值}\n设 $f$ 在 $0$ 处连续，且 $\\lim_{x\\to0}\\frac{f(x)+3}{x}=2$。判断 $f$ 在 $0$ 处是否可导并求导数；若去掉连续性，说明能否保留可导结论，并给出反例。\n\\end{exercise}\n\\begin{exercise}{158}{缩放增量的差商}\n设 $f$ 在 $x_0$ 处可导。求 $\\lim_{h\\to0}\\frac{f(x_0+5h)-f(x_0)}h$ 与 $\\lim_{h\\to0}\\frac{f(x_0)-f(x_0-3h)}h$；用同一方法写出一般系数 $a,b$ 下 $\\lim_{h\\to0}\\frac{f(x_0+ah)-f(x_0+bh)}h$。\n\\end{exercise}\n\\begin{exercise}{159}{双移位差商与逆命题}\n设 $f'(x_0)$ 存在，求 $\\lim_{h\\to0}\\frac{f(x_0+4h)-f(x_0+2h)}h$。若不要求 $f$ 在 $x_0$ 连续，构造一个在该点不可导但上述极限仍存在的函数，说明差分式中没有出现点值的影响。\n\\end{exercise}\n\\begin{exercise}{160}{二次增量下的单侧信息}\n设 $f$ 在 $3$ 处可导，且 $\\lim_{x\\to0}\\frac{f(3)-f(3-3x^2)}{\\ln(1+x^2)}=3$。求 $f'(3)$；说明若仅假设 $f$ 在 $3$ 处连续，给定极限能否保证双侧导数存在。\n\\end{exercise}\n\\begin{exercise}{161}{可导函数的渐近形式}\n设 $f(0)=0$、$f'(0)=1$。求 $\\lim_{x\\to0}\\frac{f(3x)-f(-5x)}x$ 与 $\\lim_{x\\to0}\\frac{f(2x^2)-xf(x)}{x^2}$；分别写明使用 $f(t)=t+o(t)$ 时余项的变化。\n\\end{exercise}\n\\begin{exercise}{162}{可导充分条件的辨析}\n设 $f(0)=0$，分别判断下列极限存在是否足以保证 $f'(0)$ 存在，证明或举反例：$\\lim_{h\\to0}\\frac{f(3h)-f(h)}{2h}$，$\\lim_{h\\to0}\\frac{f(h)-f(-h)}{2h}$，$\\lim_{h\\to0}\\frac{f(h^3)}{h^3}$，$\\lim_{h\\to0}\\frac{f(h^2)}{h^2}$。指出奇次与偶次换元提供的自变量方向有何不同。\n\\end{exercise}\n\\begin{exercise}{163}{二次内增量与已知导数}\n设 $f$ 在 $1$ 处可导，$f(1)=0$、$f'(1)=2$。求 $\\lim_{x\\to0}\\frac{\\ln(1+\\sin^2(3x))-f(\\cos x)}{x^2}$，写出 $f(\\cos x)$ 的首个非零渐近项；说明为何只知道 $f'(1)$ 已足以计算该极限。\n\\end{exercise}\n\\begin{exercise}{164}{内点导数与端点约束}\n分别判断 $|x|$、$\\sqrt x$、$x^2$、$x\\ln x$ 在 $0$ 处是否具有通常的双侧导数。对原式在 $0$ 未定义的函数，先判断能否连续补定义，再讨论其右差商是否有有限极限。\n\\end{exercise}\n\\begin{exercise}{165}{左右导数的拼接}\n设 $f(x)=\\begin{cases}\\cos x,&x>0,\\\\x^2+1,&x\\le0.\\end{cases}$ 求 $f'_-(0)$、$f'_+(0)$ 并判断可导性；再比较两侧二阶导数，判断 $f''(0)$ 是否存在。\n\\end{exercise}\n\\begin{exercise}{166}{指数分段函数的单侧导数}\n设 $f(x)=\\begin{cases}x(1+e^{1/x}),&x\\ne0,\\\\0,&x=0.\\end{cases}$ 分别讨论其在 $0$ 处的左连续性、右连续性与左右导数，区分有限单侧导数与无穷差商；说明一侧导数存在能否推出另一侧连续。\n\\end{exercise}\n\\begin{exercise}{167}{绝对值造成的尖点}\n讨论 $f(x)=x^2|x-1|$ 在 $1$ 处的左右导数与可导性；若将因子 $x^2$ 换为 $(x-1)^2$，重新判断并解释零点因子的作用。\n\\end{exercise}\n\\begin{exercise}{168}{零点消除绝对值尖点}\n讨论 $f(x)=(x^3-1)|x-1|$ 在 $1$ 处的可导性并求导数；进一步判断 $f'$ 在 $1$ 处是否连续、$f''(1)$ 是否存在。\n\\end{exercise}\n\\begin{exercise}{169}{可导的充要条件}\n设 $\\varphi$ 在 $1$ 处连续，$f(x)=|x-1|\\varphi(x)$。证明 $f$ 在 $1$ 处可导当且仅当 $\\varphi(1)=0$，并求此时的导数；说明证明中连续性使用在何处。\n\\end{exercise}\n\\begin{exercise}{170}{绝对值复合的全部不可导点}\n求 $f(x)=(x^2+x-2)|x^2-4x|$ 的全部不可导点及其左右导数；说明绝对值内部多项式的零点是否一定造成不可导。\n\\end{exercise}\n\\begin{exercise}{171}{切线与法线}\n求曲线 $y=2x+\\cos x$ 在 $(0,1)$ 处的切线、法线方程；再确定该曲线是否存在水平切线，并给出依据。\n\\end{exercise}\n\\begin{exercise}{172}{切线垂直的可行性}\n在相同横坐标 $x_0$ 处，曲线 $y=x^2$ 与 $y=x^3$ 的切线互相垂直。求所有 $x_0$，并检查用斜率乘积为 $-1$ 的判据时是否遗漏竖直切线情形。\n\\end{exercise}\n\\begin{exercise}{173}{指定方向的切线}\n直线 $L$ 与 $2x-6y+1=0$ 垂直，且与曲线 $y=x^3+3x^2-5$ 相切。求全部可能的切点及 $L$ 的方程；说明斜率方程的重根是否表示存在两条不同切线。\n\\end{exercise}\n\\begin{exercise}{174}{切线截距与面积不变量}\n证明双曲线 $xy=1$ 上任一点处的切线与坐标轴围成的三角形面积恒为 $2$；写明两截距的符号，并说明点位于第三象限时面积结论为何仍成立。\n\\end{exercise}\n\\begin{exercise}{175}{公共切线的两个条件}\n求 $a,b$，使 $y=1+\\ln x$ 与 $y=x^2+ax+b$ 在 $x=1$ 处具有同一条切线；分别列出点值条件和斜率条件，并求公共切线方程。\n\\end{exercise}\n\\begin{exercise}{176}{偶函数导数与倒数差商}\n设 $f$ 为可导偶函数，且 $\\lim_{h\\to0}\\frac{h}{f(3+h)-f(3)}=-2$。求曲线在 $(-3,f(-3))$ 处的切线斜率；从奇偶性定义证明所使用的导数关系。\n\\end{exercise}\n\\begin{exercise}{177}{可导蕴含连续}\n设 $f$ 在 $2$ 处可导，且 $\\lim_{x\\to2}f(x)=5$。求 $f(2)$；证明所使用的“可导蕴含连续”结论，并构造函数说明连续不足以保证可导。\n\\end{exercise}\n\\begin{exercise}{178}{振荡函数的连续与可导}\n设 $f(x)=\\begin{cases}x\\cos(1/x^2),&x\\ne0,\\\\0,&x=0.\\end{cases}$ 讨论 $0$ 处的连续性与可导性；若将 $x$ 改为 $x^2$，重新讨论，并用点列解释差商无极限的情形。\n\\end{exercise}\n\\begin{exercise}{179}{连续可导的分段拼接}\n设 $f(x)=\\begin{cases}xe^x,&x\\ge0,\\\\x^3+x,&x<0.\\end{cases}$ 判断其在 $0$ 处的连续性、可导性和导函数连续性；进一步判断 $f''(0)$ 是否存在。\n\\end{exercise}\n\\begin{exercise}{180}{先连续再比较导数}\n设 $f(x)=\\begin{cases}x^3+\\ln x,&x\\ge1,\\\\x^3\\ln x,&0<x<1.\\end{cases}$ 判断 $1$ 处的连续性与可导性；若只允许给右支加一个常数 $c$，确定能使函数连续的 $c$，并判断此时是否可导。\n\\end{exercise}\n\\begin{exercise}{181}{可导拼接反求参数}\n求 $a,b$，使 $f(x)=\\begin{cases}x\\sin\\pi x,&x>1,\\\\ax^2+b,&x\\le1\\end{cases}$ 在 $1$ 处可导；再判断此时 $f'$ 在 $1$ 处是否连续及 $f''(1)$ 是否存在。\n\\end{exercise}\n\\begin{exercise}{182}{有界因子能提供的局部信息}\n设 $\\varphi$ 在 $0$ 的某邻域内有界，$f(x)=\\begin{cases}\\ln(1+2x^2)/x^2,&x>0,\\\\x^2\\varphi(x),&x\\le0.\\end{cases}$ 求 $0$ 处左右极限并判断连续性、可导性；说明给 $f(0)$ 重新赋值能否修复该处的间断。\n\\end{exercise}\n\\begin{exercise}{183}{对称差商的条件辨析}\n设 $f$ 在 $0$ 处连续，且 $\\lim_{h\\to0}\\frac{f(h)-f(-h)}{2h}=L$。举例说明 $f'(0)$ 未必存在；若再有 $\\lim_{h\\to0}\\frac{f(h)+f(-h)-2f(0)}h=0$，证明 $f'(0)=L$。\n\\end{exercise}\n\\begin{exercise}{184}{绝对值复合的可导判据}\n设 $g$ 在 $x_0$ 处可导且 $g(x_0)=0$。证明 $|g|$ 在 $x_0$ 处可导当且仅当 $g'(x_0)=0$；再求 $|x^3-3x+2|$ 的全部不可导点，并解释其中重根与单根的区别。\n\\end{exercise}\n\\subsection{函数的求导法则}\n\\begin{exercise}{185}{基本导数与定义域}\n设 $f(x)=3x^2+2e^x-5\\ln x+\\sin1$。求 $f'(x)$、$f'(1)$ 及 $x=1$ 处的切线方程，说明常数项在点值和斜率中的不同作用。\n\\end{exercise}\n\\begin{exercise}{186}{乘积法则与定点导数}\n设 $f(x)=x\\cos x+3x^2$。求 $f'(x)$、$f'(\\pi/2)$；判断表达式 $(x\\cos x)'=\\cos x\\,(x)'$ 是否成立，并写明遗漏项。\n\\end{exercise}\n\\begin{exercise}{187}{指数三角乘积的求导}\n设 $y=e^x(\\cos x-2\\sin x)$。求 $y'$，并求 $x\\in[0,2\\pi)$ 中全部水平切线所对应的横坐标。\n\\end{exercise}\n\\begin{exercise}{188}{对数因子的定义范围}\n设 $y=(1+x^2)\\arctan x-x\\ln x$。求 $y'$；将函数在 $0$ 处连续补定义后，判断其右导数是否为有限值。\n\\end{exercise}\n\\begin{exercise}{189}{商式化简后求导}\n设 $y=\\frac{\\sqrt x+xe^x-3x^3\\sin x}{x^2}$。写出定义域并求 $y'$；比较直接使用商法则与先拆成三项时的表达式，验证结果一致。\n\\end{exercise}\n\\begin{exercise}{190}{商法则与分母零点}\n设 $y=\\frac{\\sin x}{x-\\cos x}$。求 $y'$ 并写明适用条件；证明方程 $x-\\cos x=0$ 只有一个实根，判断该点能否连续补定义。\n\\end{exercise}\n\\begin{exercise}{191}{对数有理式的求导}\n设 $y=\\frac{2\\ln x+x^3}{3\\ln x+x^2}$。求 $y'$、$y'(1)$，并说明导数表达式使用时对 $x$ 及分母的限制；证明正半轴上恰有一个分母零点。\n\\end{exercise}\n\\begin{exercise}{192}{指数有理式的乘商求导}\n设 $y=\\frac{e^x(x^2+1)}{x+1}$。求 $y'$ 并化简，写出定义域；进一步求 $\\lim_{x\\to-1}(x+1)^2y'$，说明奇点处不能直接代入求导公式。\n\\end{exercise}\n\\begin{exercise}{193}{换元确定函数及导数}\n已知对一切 $x\\ne0$，$f(x-1/x)=\\frac{x^4+1}{x^4+x^2+1}$。求 $f(t)$、$f'(t)$，说明换元后 $t$ 的范围；验证不同原像给出的函数值一致。\n\\end{exercise}\n\\begin{exercise}{194}{分段函数的导函数}\n设 $f(x)=\\begin{cases}x/(2x-1),&x<0,\\\\e^x\\sin x,&x\\ge0.\\end{cases}$ 求所有可导点处的 $f'(x)$，单独判断 $0$ 处是否可导，并写出该处左右导数。\n\\end{exercise}\n\\begin{exercise}{195}{反函数导数的取点}\n设可导函数 $f$ 的反函数为 $\\varphi$，已知 $f(1)=2$、$f(2)=3$、$f'(1)=4$、$f'(2)=5$。求 $\\varphi'(2)$、$\\varphi'(3)$，说明为何不能将 $\\varphi'(2)$ 直接写为 $1/f'(2)$。\n\\end{exercise}\n\\begin{exercise}{196}{反函数存在性与导数}\n设 $f(x)=3x^3+2x+1$。证明其在 $\\mathbb R$ 上有反函数 $\\varphi$，求 $\\varphi'(1)$；进一步求 $\\varphi''(1)$，并说明所用分母为何非零。\n\\end{exercise}\n\\begin{exercise}{197}{多层复合的链式法则}\n设 $y=(1-x+2x^3)^4$。求 $y'(0)$、$y'(1)$，并写出导函数；比较内函数在两点处的值及其导数各如何进入结果。\n\\end{exercise}\n\\begin{exercise}{198}{对数三角指数复合}\n设 $y=\\ln(\\cos(e^{-x}))$。求 $y'$，写出函数的完整定义域；确定包含 $x=0$ 的最大定义区间，并说明该区间端点处表达式的变化。\n\\end{exercise}\n\\begin{exercise}{199}{根式反三角函数的求导范围}\n设 $f(x)=\\arcsin\\sqrt{\\frac{1-x}{1+x}}$。求定义域、内部各点的 $f'(x)$ 及 $f'(1/2)$；判断定义域两端点的单侧差商是否有有限极限。\n\\end{exercise}\n\\begin{exercise}{200}{共轭式化简与端点导数}\n设 $y=\\frac{\\sqrt{x+1}-\\sqrt{x-1}}{\\sqrt{x+1}+\\sqrt{x-1}}$。求定义域与内部导数，给出一种先化简再求导的方法；判断 $x=1$ 处右差商是否有有限极限。\n\\end{exercise}\n\\begin{exercise}{201}{多种指数结构的求导}\n设 $y=3^x+x^3+x^{2x}+3^{x^2}$（$x>0$）。求 $y'$、$y'(1)$；分别指出常底指数、常指数幂、幂指函数及复合指数项所用的求导规则。\n\\end{exercise}\n\\begin{exercise}{202}{三角函数乘积与复合}\n设 $y=\\cos3x\\,\\sin^3x$。求 $y'$ 与 $y'(\\pi/6)$；将 $y'$ 在 $\\sin x=0$ 和 $\\cos3x=0$ 的点分别代入，说明不能通过直接除去这些因子求全部驻点。\n\\end{exercise}\n\\begin{exercise}{203}{反三角函数与根式导数}\n设 $y=x\\sqrt{1-x^2}-\\arccos x$。求内部导数并尽量化简，写出适用区间；用差商判断两个端点的单侧导数是否有限。\n\\end{exercise}\n\\begin{exercise}{204}{根式与对数的协同化简}\n设 $y=x^2+x\\sqrt{x^2+1}+\\ln(x+\\sqrt{x^2+1})$。证明对数对所有实数 $x$ 有定义，求 $y'$ 并化简；据此判断该函数在 $\\mathbb R$ 上的单调性。\n\\end{exercise}\n\\begin{exercise}{205}{对数相位的复合导数}\n设 $y=x[\\cos(\\ln x)+\\sin(\\ln x)]$。求 $y'$；将 $y$ 在 $0$ 处连续延拓后，判断右导数是否存在，并给出两列差商证明。\n\\end{exercise}\n\\begin{exercise}{206}{反余切指数复合求导}\n设 $y=-x+\\frac12\\ln(1+e^{2x})-e^{-x}\\operatorname{arccot}e^x$，其中 $\\operatorname{arccot}\\in(0,\\pi)$。求 $y'$ 并化简，再判断该函数在 $\\mathbb R$ 上的单调性。\n\\end{exercise}\n\\begin{exercise}{207}{先取参数极限再求导}\n对每个固定实数 $x$，设 $f(x)=\\lim_{t\\to+\\infty}x\\left(\\frac{t-x}{t+2x}\\right)^t$，实数幂在充分大的 $t$ 上考虑。求 $f(x)$ 及 $f'(x)$；先计算定义函数的极限，不得未经论证交换求导与取极限。\n\\end{exercise}\n\\begin{exercise}{208}{抽象函数的链式法则}\n设 $f$ 可导。分别求 $y=f(3^x+x^2)$ 与 $y=f(x\\ln x)$ 的导数，写明第二式的定义范围；若 $f'(1)=2$，再求第一式…48 tokens truncated… 的全部实数 $x$，指出仅用已知的 $f'(1)$ 还可确定哪些点的 $g'$。\n\\end{exercise}\n\\begin{exercise}{210}{反函数与复合函数求导}\n设 $f(x)=x+e^x$，其反函数为 $\\varphi$。证明反函数在 $\\mathbb R$ 上存在且可导，求 $\\varphi'(1)$；再设 $G(x)=\\varphi(e^x)$，求 $G'(0)$ 与 $G''(0)$。\n\\end{exercise}\n\\begin{exercise}{211}{函数关系的求导约束}\n设 $f:\\mathbb R\\to\\mathbb R$ 可导，满足 $f(x+y)=f(x)+f(y)+2xy$。先求 $f(0)$，再用固定 $x$、令增量趋零的方法证明 $f'(x)=f'(0)+2x$；若 $f'(0)=3$，确定 $f(x)$ 并验证。\n\\end{exercise}\n\\subsection{高阶导数}\n\\begin{exercise}{212}{二阶导数与定义域}\n分别求 $y=\\frac{\\sin x-\\cos x}{\\sin x+\\cos x}$ 与 $y=2x^3\\arctan x+\\ln(1+x^2)$ 的二阶导数；写明前者的定义范围，并求后者的 $y''(0)$。\n\\end{exercise}\n\\begin{exercise}{213}{指数三角函数的二阶导数}\n设 $f(x)=e^{3x}\\sin2x$。求 $f''(\\pi/2)$；进一步找出常数 $a,b$，使 $f''+af'+bf\\equiv0$，并直接验证。\n\\end{exercise}\n\\begin{exercise}{214}{对数根式的二阶求导}\n设 $y=\\ln\\sqrt{\\frac{1+e^{2x}}{e^{2x}}}$。求 $y'(0)$、$y''(0)$，再写出 $y$ 在 $0$ 处到二阶的展开式，并说明余项形式。\n\\end{exercise}\n\\begin{exercise}{215}{反正弦函数的二阶导数}\n设 $y=\\arcsin(x/3)$。求 $y''(\\sqrt5)$ 及 $y''$ 的定义区间；根据 $y''$ 的符号判断其在负、正半区间上的凹凸性。\n\\end{exercise}\n\\begin{exercise}{216}{对数乘积的高阶导数}\n设 $y=x\\ln x$（$x>0$）。求 $y^{(10)}$，再给出 $y^{(n)}$（$n\\ge2$）的通式并用数学归纳法证明，明确符号与阶乘的下标。\n\\end{exercise}\n\\begin{exercise}{217}{三角函数导数的周期性}\n设 $y=(\\sin(x/2)+\\cos(x/2))^2$。先化简再求 $y^{(10)}$；给出 $y^{(n)}$（$n\\ge1$）的统一公式，并核对前两阶。\n\\end{exercise}\n\\begin{exercise}{218}{莱布尼茨公式的简化}\n设 $f(x)=xe^{-x}$。求 $f^{(n)}(x)$（$n\\ge1$）并证明；再求 $f^{(n)}(n)$，说明乘积中仅有两项对高阶导数有贡献的原因。\n\\end{exercise}\n\\begin{exercise}{219}{多项式次数与最高阶导数}\n设 $y=(x^2+1)^5(x^5+1)^2$。不完全展开，求 $y^{(20)}$、$y^{(21)}$；再求 $y^{(19)}(0)$，说明只需检查哪些幂次。\n\\end{exercise}\n\\begin{exercise}{220}{降幂后的任意阶导数}\n设 $f(x)=\\sin^4x+\\cos^4x$。化简并求 $f^{(n)}(x)$（$n>1$）；再求满足 $f^{(n)}(0)=0$ 的全部正整数 $n$。\n\\end{exercise}\n\\begin{exercise}{221}{复合对数的高阶导数}\n设 $f(x)=\\ln(2-3x)$。求 $f^{(n)}(x)$（$n\\ge1$）并用归纳法证明，写出适用区间；再求 $f^{(n)}(0)$。\n\\end{exercise}\n\\begin{exercise}{222}{导数函数关系的继续求导}\n设 $f$ 在 $1$ 的某邻域内可导，满足 $f'=f^2$ 且 $f(1)=2$。证明条件保证 $f''$ 存在，求 $f''(1)$；再求 $f'''(1)$，说明每次求导的合法性。\n\\end{exercise}\n\\begin{exercise}{223}{高阶零点与莱布尼茨公式}\n设 $g$ 在 $a$ 附近有 $n+1$ 阶导数，$F(x)=(x-a)^ng(x)$，其中 $n\\ge1$。求 $F^{(k)}(a)$（$0\\le k\\le n+1$），并用莱布尼茨公式证明；据此求 $(x-1)^5\\ln x$ 在 $1$ 处的六阶导数。\n\\end{exercise}\n\\begin{exercise}{224}{高阶导数的递推公式}\n设 $f(x)=e^{ax}\\sin bx$。证明存在数列 $A_n,B_n$，使 $f^{(n)}(x)=e^{ax}(A_n\\sin bx+B_n\\cos bx)$，写出初值与递推式；取 $a=b=1$，求 $f^{(8)}(0)$，并用相位表示式核对。\n\\end{exercise}\n\\subsection{隐函数及由参数方程所确定的函数的导数}\n\\begin{exercise}{225}{隐函数求导与正则点}\n分别对 $\\cos(xy)+\\ln y-x=1$、$x^2+y^2=6xy$ 求 $\\dd y/\\dd x$，写出公式分母非零的条件；对第二条曲线单独讨论原点的直线分支与切线。\n\\end{exercise}\n\\begin{exercise}{226}{隐函数分支与定点导数}\n方程 $xy-\\sin(\\pi y^2)=0$ 在 $(0,1)$ 附近确定分支 $y=y(x)$。求 $y'(0)$；若改取过 $(0,\\sqrt2)$ 的分支，重新计算并说明只给 $x=0$ 是否足以唯一确定导数。\n\\end{exercise}\n\\begin{exercise}{227}{隐曲线的切线与法线}\n求曲线 $\\tan(x+y+\\pi/4)=y$ 在 $(-1,1)$ 处的切线与法线方程；检查该点满足原方程，并说明求导中 $y$ 对 $x$ 的依赖如何进入。\n\\end{exercise}\n\\begin{exercise}{228}{同一横坐标的多条隐分支}\n求曲线 $y^2+2e^{xy}=3y$ 在横坐标 $x=0$ 对应的全部点及各点的切线方程；检查每一点处隐函数求导式的分母是否非零。\n\\end{exercise}\n\\begin{exercise}{229}{抽象隐函数的定点导数}\n设 $xf(y)=e^y\\ln y$ 确定过 $(0,1)$ 的可导分支，$f$ 可导且 $f(1)=1$。求 $y'(0)$；若再知 $f$ 在 $1$ 附近连续可导且 $f'(1)=c$，求 $y''(0)$，写明所需的连续性与可导性来自何处。\n\\end{exercise}\n\\begin{exercise}{230}{隐显曲线公共切线}\n曲线 $y=x^2+ax+b$ 与 $2y=xy^2-3$ 在 $(1,-1)$ 处有公共切线。求全部参数 $a,b$ 及公共切线方程；分别写明通过指定点和切线斜率相同给出的条件。\n\\end{exercise}\n\\begin{exercise}{231}{隐函数的二阶导数}\n在 $x\\ne0$ 的区域，方程 $\\ln(x^2+y^2)=2\\arctan(y/x)+\\pi/2+\\ln2$ 确定局部可导分支 $y(x)$。求 $y'$、$y''$，写出导数公式的分母条件，并说明原方程的定义范围。\n\\end{exercise}\n\\begin{exercise}{232}{隐函数二阶导数的定点计算}\n设 $e^y+xy=e+1$ 确定过 $(1,1)$ 的局部分支。求 $y'(1)$、$y''(1)$；写出该点处的一阶线性近似，并检查一阶求导式的分母非零。\n\\end{exercise}\n\\begin{exercise}{233}{含导数关系的再次求导}\n设曲线 $y(x)$ 二阶可导，经过 $(1,-1)$，满足 $x^2+y^2+(y')^3=1$。求 $y'(1)$、$y''(1)$；说明为何能在该点附近由再次求导的方程解出 $y''$。\n\\end{exercise}\n\\begin{exercise}{234}{对数求导与正性}\n设 $y=x^{\\ln x}$（$x>0$）。用对数求导法求 $y'$，确定全部驻点及单调区间；说明取自然对数的合法性。\n\\end{exercise}\n\\begin{exercise}{235}{变底变指数的求导}\n在 $1+\\sin x>0$ 的区间内，设 $y=(1+\\sin x)^{x^2}$。求 $y'$ 与 $y'(0)$；说明底数等于零的点为何不能直接代入对数求导公式。\n\\end{exercise}\n\\begin{exercise}{236}{幂指函数与根式乘积}\n设 $y=x^{\\sin x}\\sqrt{e^x-1}$（$x>0$）。求 $y'$，再求 $\\lim_{x\\to0^+}y/\\sqrt x$；据此判断将 $y(0)$ 定义为 $0$ 后右导数是否有限。\n\\end{exercise}\n\\begin{exercise}{237}{变指数的商函数}\n设 $y=(1+2x)^{1/x^2}e^{-x}$，其中 $x>-1/2$、$x\\ne0$。求 $y'$；分别讨论 $x\\to0^+$、$x\\to0^-$ 时 $y$ 的变化，判断能否在 $0$ 处连续补定义。\n\\end{exercise}\n\\begin{exercise}{238}{多因子对数求导}\n设 $y=\\frac{(x+1)^2\\sqrt{2x+2}}{(x-1)^3\\sqrt{3x-3}}$。确定实定义域，用对数求导法求 $y'$ 并化简；根据 $y'/y$ 的符号判断单调性。\n\\end{exercise}\n\\begin{exercise}{239}{幂指函数的一阶导数}\n求 $y=x^x$（$x>0$）的 $y'$，确定其最小值及取值点；再求 $\\lim_{x\\to0^+}x^x$，判断连续延拓后的右导数是否有限。\n\\end{exercise}\n\\begin{exercise}{240}{幂指函数的二阶导数}\n设 $y=x^{2x}$（$x>0$）。求 $y''$，并判断 $y''$ 在定义域内的符号；给出判断中使用的不等式或平方分解。\n\\end{exercise}\n\\begin{exercise}{241}{隐式幂指方程的分支}\n在 $x,y>0$ 且 $1+\\ln y\\ne0$ 的分支上，方程 $x^{1/y}=y^{1/x}$ 确定 $y=y(x)$。求 $y'$、$y''$；说明取对数后方程如何化简，并核对分支 $y=x$ 上的结果。\n\\end{exercise}\n\\begin{exercise}{242}{参数方程求导与例外参数}\n分别求参数曲线 $x=2t/(1+t^2),\\ y=2t^2/(1+t^2)$ 和 $x=\\cos^3t,\\ y=\\sin^3t$ 的 $\\dd y/\\dd x$。列出 $\\dd x/\\dd t=0$ 的参数，并对第一条曲线在这些参数处判断切线方向。\n\\end{exercise}\n\\begin{exercise}{243}{参数导数的定点取值}\n设 $x=t^2e^{2t}$、$y=(t^2+1)e^t$。求 $\\left.\\dd y/\\dd x\\right|_{t=2}$；列出一阶参数求导公式不能直接使用的全部 $t$，并说明原因。\n\\end{exercise}\n\\begin{exercise}{244}{参数曲线切线与双分支}\n求 $x=\\sqrt{t^2+3}$、$y=\\ln(t+\\sqrt{t^2+3})$ 在 $t=1$ 对应点的切线方程；再比较 $t=-1$ 对应点的坐标及切线斜率，说明相同 $x$ 是否对应相同 $y$。\n\\end{exercise}\n\\begin{exercise}{245}{由坐标确定参数}\n求曲线 $x=e^t\\sin2t$、$y=e^t\\cos t$ 在 $(0,1)$ 处的切线和法线方程；先确定该点对应的全部实数参数，检查是否存在多条切线。\n\\end{exercise}\n\\begin{exercise}{246}{参数曲线二阶导数}\n设 $x=\\cos t$、$y=t\\cos t-\\sin t$。求 $\\dd y/\\dd x$ 与 $\\dd^2y/\\dd x^2$，写出公式适用的参数范围；说明求二阶导数时为何还须除以 $\\dd x/\\dd t$。\n\\end{exercise}\n\\begin{exercise}{247}{反三角参数的二阶导数}\n设 $x=\\arctan t$、$y=3t+t^3$。求 $\\left.\\dd^2y/\\dd x^2\\right|_{t=1}$；消去参数写出显函数，并用显函数求导核对。\n\\end{exercise}\n\\begin{exercise}{248}{参数导数与全局单值性}\n设 $x=e^t+t$、$y=\\sin t$。求 $t=0$ 时的一阶、二阶 $x$ 导数；证明参数式在整个实轴上确定单值函数 $y(x)$，并写出其 $x$ 定义域。\n\\end{exercise}\n\\begin{exercise}{249}{隐函数正则点与退化点}\n考虑曲线 $x^2+xy+y^2=3$。求过 $(1,1)$ 的局部分支的一阶、二阶导数及切线；找出曲线上 $\\dd y/\\dd x$ 公式分母为零的点，并判断这些点的切线方向。\n\\end{exercise}\n\\begin{exercise}{250}{参数退化点的导数定义}\n设 $x=t^3$、$y=t^4$。消去参数并讨论原点处的可导性与切线，再讨论二阶导数是否存在；解释为什么 $t=0$ 时参数导数商为 $0/0$ 并不能直接判定不可导。\n\\end{exercise}\n\\subsection{函数的微分}\n\\begin{exercise}{251}{微分与增量的误差}\n设 $y=x^3+x$。在 $x=3$ 处，分别取 $\\Delta x=0.1,0.01$，计算 $\\dd y$、$\\Delta y$ 及二者之差；写出一般增量 $h$ 时的误差表达式，并说明误差相对于 $h$ 的阶。\n\\end{exercise}\n\\begin{exercise}{252}{可微定义与余项}\n已知 $f$ 在每个 $x>-1$ 处的增量可写为 $\\Delta y=\\frac{\\Delta x}{\\sqrt{1+x^3}}+\\alpha$，其中 $\\alpha/\\Delta x\\to0$（$\\Delta x\\to0$）。求 $f'(2)$ 及 $\\dd y|_{x=2}$；说明线性系数唯一的原因。\n\\end{exercise}\n\\begin{exercise}{253}{微分和增量的等价关系}\n设 $f$ 在 $x_0$ 处可导且 $f'(x_0)=1$。比较 $\\dd y$、$\\Delta y$ 与 $\\Delta x$ 在 $\\Delta x\\to0$ 时的等价关系并证明；若 $f'(x_0)=0$，说明还能保留哪些高阶关系。\n\\end{exercise}\n\\begin{exercise}{254}{复合函数的微分}\n求 $y=e^{\\sin^2(1/x)}$ 与 $y=\\arcsin(x/2)+\\sqrt{4-x^2}$ 的微分，并写出公式成立的范围；对第二个函数判断能否把内部微分公式直接用于端点。\n\\end{exercise}\n\\begin{exercise}{255}{定点微分的系数}\n分别求 $y=\\sqrt2+\\sin x$ 在 $x=0$ 处和 $y=\\ln(1+2^{-2x})$ 在 $x=1$ 处的微分；将 $\\dd x=0.01$ 代入，写出相应的函数增量线性近似。\n\\end{exercise}\n\\begin{exercise}{256}{隐函数微分的唯一性}\n设 $2y+\\sin(x+y)=0$ 确定 $y=y(x)$。求 $\\dd y$，证明导数公式的分母恒不为零；在过原点的分支上，求 $x=0$ 处的线性近似。\n\\end{exercise}\n\\begin{exercise}{257}{隐函数的定点微分}\n设 $e^y+xy-e=0$ 在 $x=0$ 附近确定分支 $y(x)$。求该点对应的 $y$ 值及 $\\dd y|_{x=0}$；据此估计 $x$ 增加 $0.01$ 时 $y$ 的增量，说明这是线性近似。\n\\end{exercise}\n\\begin{exercise}{258}{可去点处的微分}\n设 $f(x)=\\begin{cases}(\\cos x-1)/x,&x\\ne0,\\\\0,&x=0.\\end{cases}$ 用定义求 $\\dd f|_{x=0}$；说明为何不能直接把 $x=0$ 代入非零点求导所得的商式。\n\\end{exercise}\n\\begin{exercise}{259}{幂指函数的微分}\n求 $y=(1+e^x)^x$ 的微分，逐项标明对底数与指数求导的贡献；再求 $\\dd y|_{x=0}$，检查是否与原函数在 $0$ 处的线性近似一致。\n\\end{exercise}\n\\begin{exercise}{260}{由微分确定函数}\n在各自定义区间内，求导数分别为 $x^2$、$\\cos3x$、$1/(x\\ln x)$、$e^x/(1+e^{2x})$ 的全部函数。写明任意常数与定义区间的关系，并直接求导核对四个结果。\n\\end{exercise}\n\\begin{exercise}{261}{夹逼条件与可微性}\n设 $f$ 在 $0$ 的某邻域内有定义且 $|f(x)|\\le x^2$。证明 $f$ 在 $0$ 处连续、可导并求 $f'(0)$；构造满足此条件而导函数在 $0$ 附近无界的函数，说明一点可导不能保证邻域内导数有界。\n\\end{exercise}\n\\begin{exercise}{262}{定点导数的结构化计算}\n分别求：$f(x)=3x+\\frac{x^2-1}{x^2+1}\\arctan\\frac{2x}{1+x}$ 的 $f'(0)$；$p(x)=x(x-1)\\cdots(x-100)$ 的 $p'(100)$；$y=\\frac{(x^2+1)\\sqrt{3x+1}}{(x+1)^2e^{2x}}$ 的 $y'(1)$。每式选取合适方法，避免完全展开乘积。\n\\end{exercise}\n\\begin{exercise}{263}{等价差分给出的点值和导数}\n设 $f$ 在 $x_0$ 处可导，且 $f(x_0+3h)-3f(x_0-h)\\sim h$（$h\\to0$）。求 $f(x_0)$、$f'(x_0)$，并用 $f(x_0+t)=f(x_0)+f'(x_0)t+o(t)$ 验证参数条件充分。\n\\end{exercise}\n\\begin{exercise}{264}{可导信息与幂指极限}\n设 $f$ 在 $0$ 附近连续可导，$f(0)=1$、$f'(0)=4$。求 $\\lim_{x\\to0}[f(\\sin x)]^{1/(2x)}$，证明底数最终为正；将指数改为 $1/(cx)$（$c\\ne0$）时写出一般结果。\n\\end{exercise}\n\\begin{exercise}{265}{切线截距构造数列}\n设曲线 $y=f(x)=1/(1+x^2)$ 在 $(n,f(n))$ 处的切线与 $x$ 轴相交于 $(\\xi_n,0)$，其中 $n\\ge1$。求 $\\xi_n$，再求 $\\lim_{n\\to\\infty}f(\\xi_n)$ 及 $\\lim_{n\\to\\infty}n^2f(\\xi_n)$。\n\\end{exercise}\n\\begin{exercise}{266}{复合差商与法线}\n设 $f$ 连续可导，且 $\\lim_{x\\to1}\\frac{f(3x-1)+3}{x-1}=3$。求 $f(2)$、$f'(2)$，再求曲线在 $(2,f(2))$ 处的法线方程，说明复合函数内部系数的作用。\n\\end{exercise}\n\\begin{exercise}{267}{幂根极限与不可导点}\n设 $f(x)=\\lim_{n\\to\\infty}\\frac{x^2}{(1+x^{2n})^{1/n}}$。求其分段表达式，讨论整个实轴上的连续性与可导性；对每个不可导点计算左右导数。\n\\end{exercise}\n\\begin{exercise}{268}{由连续延拓反求点值}\n设 $f$ 连续可导且 $f(1)=0$、$f'(1)=1$。令 $g(x)=\\begin{cases}\\frac{f(e^{2x})+\\ln(1-4x)}x,&x\\ne0,\\\\b,&x=0,\\end{cases}$ 在 $0$ 的充分小邻域内定义。求使 $g$ 在 $0$ 连续的 $b$，并说明现有条件是否足以保证 $g'(0)$ 存在。\n\\end{exercise}\n\\begin{exercise}{269}{极限生成分段函数的可导条件}\n设 $f(x)=\\lim_{n\\to\\infty}\\frac{x^2e^{n(x-1)}+3ax+b}{e^{n(x-1)}+1}$。求分段表达式；确定使其在 $1$ 处可导的全部 $a,b$；在这些参数下求整个实轴上的 $f'$，并判断其连续性。\n\\end{exercise}\n\\begin{exercise}{270}{互补内函数的链式法则}\n设 $f$ 可导，$y=f(\\sin^2x)+f(\\cos^2x)$。求 $y'$、$y'(0)$，再证明该函数以 $\\pi/2$ 为周期；说明这是否保证最小正周期一定等于 $\\pi/2$。\n\\end{exercise}\n\\begin{exercise}{271}{抽象函数的两层复合}\n设 $f:\\mathbb R\\to\\mathbb R$ 可导，$y=f(f(1+3x^2))$。求 $y'$ 与 $y'(0)$；若 $f$ 二阶可导，再求 $y''(0)$。\n\\end{exercise}\n\\begin{exercise}{272}{公共切线与复合平方}\n曲线 $y=f(x)$ 与 $y=(3+\\ln x)/x$ 在横坐标 $1$ 处的切线相同。设 $F(x)=[f(e^x)]^2$，求 $F'(0)$；写明公共切线同时给出的点值信息和导数信息。\n\\end{exercise}\n\\begin{exercise}{273}{二阶可导与极限反推}\n设 $f$ 在 $0$ 处二阶可导，且 $\\lim_{x\\to0}\\frac{e^{f(x)}-1}{1-\\cos x}=2$。依次求 $f(0)$、$f'(0)$、$f''(0)$；说明为何不能直接假定 $f(x)$ 从二阶项开始。\n\\end{exercise}\n\\begin{exercise}{274}{复合二阶导数的正则性条件}\n设 $f$ 在 $0$ 附近连续可导，$y=f(x^2)$。用导数定义求 $y''(0)$，结果用 $f'(0)$ 表示；若仅假设 $f$ 在邻域内可导，判断该结论是否必成立，并构造反例或给出证明。\n\\end{exercise}\n\\begin{exercise}{275}{导数方程与高阶通式}\n设 $f$ 任意阶可导且 $f'=e^f$。求 $f^{(n)}$（$n\\ge1$）关于 $f$ 的表达式，并用数学归纳法证明；若 $f(0)=0$，再求 $f^{(n)}(0)$。\n\\end{exercise}\n\\begin{exercise}{276}{高阶零点与定点导数}\n设 $n$ 为正整数，$f(x)=(x+1)^ne^{-x^2}$。用莱布尼茨公式求 $f^{(n)}(-1)$；再求 $f^{(n+1)}(-1)$，说明绝大多数项消失的原因。\n\\end{exercise}\n\\begin{exercise}{277}{反函数的二阶导数}\n设 $x=\\varphi(y)$ 是 $y=x+\\ln x$（$x>0$）的反函数。证明反函数在 $\\mathbb R$ 上存在，求 $\\dd^2x/\\dd y^2$，并求其在 $y=1$ 处的值。\n\\end{exercise}\n\\begin{exercise}{278}{函数及导函数的逐层正则性}\n设 $f(x)=\\begin{cases}x^3\\sin(1/x)+\\sin x+1,&x\\ne0,\\\\1,&x=0.\\end{cases}$ 判断 $f$ 在 $0$ 处的连续性和可导性；求 $f'$，讨论其在 $0$ 处的连续性与可导性；求 $f''$ 的存在范围及表达式。\n\\end{exercise}\n\\begin{exercise}{279}{隐函数定点导数与无穷远极限}\n方程 $\\ln(x^2+y)=x^2y+\\sin x$ 在 $(0,1)$ 附近确定分支 $y=f(x)$。求 $f'(0)$，再求 $\\lim_{|x|\\to\\infty}x\\left(1-f(2/x)\\right)$；说明无穷远表达式只使用了 $f$ 在哪个点附近的信息。\n\\end{exercise}\n\\begin{exercise}{280}{隐函数与外层抽象函数的复合}\n设 $f$ 二阶可导且 $f'(1)=1$，$xy-e^y+e^x=0$ 确定过原点的分支 $y=y(x)$。令 $z=f(e^{y(x)}-\\sin x)$，求 $z''(0)$；计算中说明为何不需要知道 $f''(1)$ 的具体值。\n\\end{exercise}\n\\begin{exercise}{281}{同一横坐标对应的参数分支}\n设 $x=2t^2+3t+1$、$y=e^t\\sin t+2$。求 $x=0$ 对应的全部参数及各分支的 $\\dd y/\\dd x$；说明题目只给横坐标时，导数是否必为唯一数值。\n\\end{exercise}\n\\begin{exercise}{282}{参数函数的三阶导数}\n设 $x=t-\\ln\\sqrt{1+e^{2t}}$、$y=\\arctan e^t$。求 $\\dd^3y/\\dd x^3$，结果可用 $t$ 表示；证明 $\\dd x/\\dd t$ 恒非零，写出 $x$ 的值域。\n\\end{exercise}\n\\begin{exercise}{283}{极坐标曲线的切线与法线}\n求阿基米德螺线 $\\rho=\\theta$ 在 $(\\rho,\\theta)=(\\pi/2,\\pi/2)$ 处的切线与法线方程，以直角坐标表示；先写出参数式并检查该点切线是否竖直。\n\\end{exercise}\n\\begin{exercise}{284}{线性主部反求复合导数}\n设 $f$ 可微，$y=f(e^{2x})$ 在 $x=0$ 处，当 $\\Delta x=-0.1$ 时，增量的线性主部也为 $-0.1$。求 $f'(1)$；说明这里给出线性主部是否意味着真实增量恰好等于 $-0.1$。\n\\end{exercise}\n\\begin{exercise}{285}{复合函数的定点微分}\n设 $f'(x)=\\arctan(1/x)$（$x\\ne0$），$y=f\\left(\\frac{2x-1}{x+1}\\right)$。求 $\\dd y|_{x=2}$；列出复合求导公式需要排除的 $x$，说明分别来自哪一层函数。\n\\end{exercise}\n\\begin{exercise}{286}{参数函数的微分}\n设 $f$ 可导且 $f'(0)\\ne0$，$x=f(\\ln t)$、$y=f(t^2-1)$（$t>0$）。求 $t=1$ 时的 $\\dd y$，分别用 $\\dd x$ 与 $\\dd t$ 表示，并验证两种写法一致。\n\\end{exercise}\n\\begin{exercise}{287}{线性近似与误差控制}\n用微分估算 $\\sqrt{4.04}$，并利用函数在 $[4,4.04]$ 上的二阶导数给出误差上界；判断近似值偏大还是偏小。说明只有 $o(\\Delta x)$ 信息时，能否直接得到给定步长下的数值误差上界。\n\\end{exercise}\n\\begin{exercise}{288}{隐函数微分与局部近似}\n设方程 $ye^y=x$ 在 $(x,y)=(e,1)$ 附近确定函数 $y(x)$。求该点的 $\\dd y$ 与 $y''$，写出 $x=e+h$ 时到二阶的近似式；说明为什么近似中出现的 $h^2$ 项不属于一阶微分。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:14:48Z


Script completed
Wall time 0.1 seconds
Output:

{}
{}

## tool · 2026-10-20T03:14:53Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"0aa506","wall_time_seconds":0.000007416,"exit_code":0,"original_token_count":126,"output":"\\section{第1章 函数与极限}\n\\subsection{函数}\n\\begin{exercise}{1}{基础·定义域}\n求 $f(x)=\\arccos(2x+1)+\\log_2(3x+2)$ 的定义域。\n\\end{exercise}\n\\begin{exercise}{2}{基础·复合函数}\n设 $f(x)=\\frac{x-1}{x+1}$。求 $f(-2)$ 和 $f(f(x))$，写出复合函数的定义域。\n\\end{exercise}\n\\begin{exercise}{3}{基础·换元求函数}\n已知对一切 $x\\ne0$，$f(1/x)=4/x+2x^2+1$。求 $f(t)$（$t\\ne0$）及 $f(x^2+1)$。\n\\end{exercise}\n\\begin{exercise}{4}{基础·反三角函数}\n"}
{"chunk_id":"eaa634","wall_time_seconds":0.000007709,"exit_code":0,"original_token_count":432,"output":"\\begin{exercise}{207}{先取参数极限再求导}\n对每个固定实数 $x$，设 $f(x)=\\lim_{t\\to+\\infty}x\\left(\\frac{t-x}{t+2x}\\right)^t$，实数幂在充分大的 $t$ 上考虑。求 $f(x)$ 及 $f'(x)$；先计算定义函数的极限，不得未经论证交换求导与取极限。\n\\end{exercise}\n\\begin{exercise}{208}{抽象函数的链式法则}\n设 $f$ 可导。分别求 $y=f(3^x+x^2)$ 与 $y=f(x\\ln x)$ 的导数，写明第二式的定义范围；若 $f'(1)=2$，再求第一式在 $x=0$ 处的导数。\n\\end{exercise}\n\\begin{exercise}{209}{复合求导的取点对应}\n已知 $f$ 可导且 $f'(1)=-2$，$g(x)=f(2x^3-3x)$。求 $g'(-1)$；再求满足 $2x^3-3x=1$ 的全部实数 $x$，指出仅用已知的 $f'(1)$ 还可确定哪些点的 $g'$。\n\\end{exercise}\n\\begin{exercise}{210}{反函数与复合函数求导}\n设 $f(x)=x+e^x$，其反函数为 $\\varphi$。证明反函数在 $\\mathbb R$ 上存在且可导，求 $\\varphi'(1)$；再设 $G(x)=\\varphi(e^x)$，求 $G'(0)$ 与 $G''(0)$。\n\\end{exercise}\n\\begin{exercise}{211}{函数关系的求导约束}\n设 $f:\\mathbb R\\to\\mathbb R$ 可导，满足 $f(x+y)=f(x)+f(y)+2xy$。先求 $f(0)$，再用固定 $x$、令增量趋零的方法证明 $f'(x)=f'(0)+2x$；若 $f'(0)=3$，确定 $f(x)$ 并验证。\n\\end{exercise}\n\\subsection{高阶导数}\n\\begin{exercise}{212}{二阶导数与定义域}\n分别求 $y=\\frac{\\sin x-\\cos x}{\\sin x+\\cos x}$ 与 $y=2x^3\\arctan x+\\ln(1+x^2)$ 的二阶导数；写明前者的定义范围，并求后者的 $y''(0)$。\n\\end{exercise}\n\\begin{exercise}{213}{指数三角函数的二阶导数}\n设 $f(x)=e^{3x}\\sin2x$。求 $f''(\\pi/2)$；进一步找出常数 $a,b$，使 $f''+af'+bf\\equiv0$，并直接验证。\n\\end{exercise}\n"}
{"chunk_id":"bc2da6","wall_time_seconds":0.000007584,"exit_code":0,"original_token_count":4994,"output":"\\section{第3章 微分中值定理与导数的应用}\n\\subsection{中值定理}\n\\begin{exercise}{289}{罗尔定理的条件与结论}\n分别判断函数 $f(x)=|x|$、$f(x)=x^2-1$、$f(x)=x\\mathrm e^{-x}$、$f(x)=1/x$ 在区间 $[-1,1]$、$[-1,1]$、$[0,1]$、$[-1,1]$ 上是否满足罗尔定理的全部条件，逐项指出依据。对满足条件的函数求全部罗尔点；对不满足条件的函数，判断开区间内是否仍有导数为零的点。\n\\end{exercise}\n\\begin{exercise}{290}{罗尔点的存在性与唯一性}\n验证 $f(x)=\\ln\\sin x$ 在 $[\\pi/6,5\\pi/6]$ 上满足罗尔定理，求出全部罗尔点。若将右端点改为 $b\\in(\\pi/6,\\pi)$，求使两个端点函数值相等的全部 $b$，并说明相应罗尔点是否唯一。\n\\end{exercise}\n\\begin{exercise}{291}{辅助函数与导数方程}\n设 $f\\in C[0,1]$，在 $(0,1)$ 可导，$f(0)=0$、$f(1)=\\pi/4$。证明存在 $\\xi\\in(0,1)$ 使 $(1+\\xi^2)f'(\\xi)=1$，写出所用辅助函数。将端点条件改为 $f(1)=c$ 时，求使同一辅助函数的两个端点值相等的 $c$，并解释该方法为何依赖此值。\n\\end{exercise}\n\\begin{exercise}{292}{多项式零点与原函数}\n设实数 $a_0,\\ldots,a_n$ 满足 $\\sum_{k=0}^n a_k/(k+1)=0$。不用定积分，证明多项式 $P(x)=\\sum_{k=0}^n a_kx^k$ 在 $(0,1)$ 内有零点。再说明若 $P$ 不恒为零，则它在 $(0,1)$ 内必同时取正值和负值。\n\\end{exercise}\n\\begin{exercise}{293}{极限条件与二阶罗尔定理}\n设 $f$ 在包含 $[0,1]$ 的开区间内二阶可导，且 $\\lim_{x\\to0}f(x)/x=0$、$f(1)=0$。由极限条件确定 $f(0)$ 与 $f'(0)$，再证明存在 $\\xi\\in(0,1)$ 使 $f''(\\xi)=0$。若仅保留 $f(0)=f(1)=0$，举例说明二阶导数为零的结论是否仍成立。\n\\end{exercise}\n\\begin{exercise}{294}{端点高阶零点与连续使用罗尔定理}\n设 $f$ 在包含 $[0,1]$ 的开区间内三阶可导，$f(0)=f(1)=0$，令 $F(x)=x^3f(x)$。求 $F(0)$、$F'(0)$，证明在 $(0,1)$ 内至少存在一点使 $F''$ 为零。进一步证明 $F'''$ 在 $(0,1)$ 内也至少有一个零点，明确每次应用罗尔定理的区间。\n\\end{exercise}\n\\begin{exercise}{295}{端点匹配与指数辅助函数}\n设 $f\\in C[0,1]$，在 $(0,1)$ 可导，$f(0)=1$、$f(1)=\\mathrm e^{-1}$。证明存在 $\\xi\\in(0,1)$ 使 $f'(\\xi)+\\mathrm e^{-\\xi}=0$。若另知 $f''(x)>\\mathrm e^{-x}$ 对所有 $x\\in(0,1)$ 成立，证明该点唯一；此问假设 $f$ 在 $(0,1)$ 二阶可导。\n\\end{exercise}\n\\begin{exercise}{296}{乘积辅助函数与参数推广}\n设 $a>0$，$f\\in C[0,a]$，在 $(0,a)$ 可导，且 $f(a)=0$。证明存在 $\\xi\\in(0,a)$ 使 $f(\\xi)+\\xi f'(\\xi)=0$。对任意给定 $p>0$，进一步证明存在 $\\eta\\in(0,a)$ 使 $pf(\\eta)+\\eta f'(\\eta)=0$，并说明为何无需假设 $x^pf(x)$ 在 $0$ 处可导。\n\\end{exercise}\n\\begin{exercise}{297}{加权导数零点}\n设 $f\\in C[0,1]$，在 $(0,1)$ 可导，且 $f(1)=0$。证明存在 $\\xi\\in(0,1)$ 使 $f'(\\xi)=-2f(\\xi)/\\xi$。讨论若把区间改为 $[a,1]$，其中 $0<a<1$，且仍只给出 $f(1)=0$，结论是否必然成立；给出证明或反例。\n\\end{exercise}\n\\begin{exercise}{298}{对称乘积与对数导数}\n设 $f\\in C[0,1]$，在 $(0,1)$ 可导，$f(0)=0$，且 $f(x)\\ne0$ 对 $0<x<1$ 成立。证明存在 $\\xi\\in(0,1)$ 使\n\\[\\frac{f'(\\xi)}{f(\\xi)}=\\frac{f'(1-\\xi)}{f(1-\\xi)}.\\]\n分别用对称乘积构造法与取 $\\xi=1/2$ 的方法论证，并说明上述条件中哪些对后一个论证并非必要。\n\\end{exercise}\n\\begin{exercise}{299}{平方辅助函数与非零分母}\n设 $f\\in C[0,1]$，在 $(0,1)$ 可导，$f(0)=f(1/2)=1$、$f(1)=2$。证明存在 $\\xi\\in(0,1)$ 使 $2f(\\xi)f'(\\xi)=\\mathrm e^{\\xi}$，从而 $f'(\\xi)=\\mathrm e^{\\xi}/[2f(\\xi)]$。证明中须说明辅助函数为何取得相同的两个函数值，以及所得点上 $f(\\xi)\\ne0$。\n\\end{exercise}\n\\begin{exercise}{300}{离散函数值约束与驻点}\n设 $f\\in C[0,3]$，在 $(0,3)$ 可导，且 $f(0)+f(1)+f(2)=3$、$f(3)=1$。证明存在 $\\xi\\in(0,3)$ 使 $f'(\\xi)=0$。再判断能否保证这样的点位于 $(0,2)$，并用具体函数支持结论。\n\\end{exercise}\n\\begin{exercise}{301}{介值定理与指数辅助函数}\n设 $f\\in C[0,1]$，在 $(0,1)$ 可导，$f(0)=f(1)=0$、$f(1/2)=1$。证明存在 $\\eta\\in(1/2,1)$ 使 $f(\\eta)=\\eta$。对任意实数 $\\lambda$，证明存在 $\\xi\\in(0,\\eta)$ 使 $f'(\\xi)-\\lambda f(\\xi)+\\lambda\\xi=1$，并写出与所选 $\\eta$ 对应的辅助函数。\n\\end{exercise}\n\\begin{exercise}{302}{三零点与二阶导数}\n设抛物线 $p(x)=-x^2+Bx+C$ 的两个零点为 $a<b$，$f$ 在包含 $[a,b]$ 的开区间内二阶可导，且 $f(a)=f(b)=0$。若存在 $c\\in(a,b)$ 使 $f(c)=p(c)$，证明存在 $\\xi\\in(a,b)$ 使 $f''(\\xi)+2=0$。说明若交点仅允许为端点，为何结论不再得到保证。\n\\end{exercise}\n\\begin{exercise}{303}{拉格朗日中值定理的适用条件}\n分别判断 $\\ln(1+x^2)$、$|x|$、$1/\\sqrt{1-x^2}$、$\\sin(1/x)$ 在 $[-1,1]$ 上是否满足拉格朗日中值定理的条件，指出每项缺失或满足的条件。对第一项求所有中值点；对第二项直接判断中值等式是否存在解。\n\\end{exercise}\n\\begin{exercise}{304}{端点连续性不可省略}\n设 $a<b$，$f$ 在 $[a,b]$ 有定义且在 $(a,b)$ 可导。判断下列四个断言是否必然成立，错误断言须给出反例：若 $f(a)f(b)<0$，则内部有驻点；若 $f(a)=f(b)$，则内部有驻点；存在 $\\xi\\in(a,b)$ 使 $f(b)-f(a)=f'(\\xi)(b-a)$；对任意 $\\xi\\in(a,b)$ 都有 $\\lim_{x\\to b^-}[f(x)-f(\\xi)]=0$。说明加上 $f\\in C[a,b]$ 后，哪些断言变为真。\n\\end{exercise}\n\\begin{exercise}{305}{中值定理证明三角不等式}\n用拉格朗日中值定理证明 $\\sin x/x>\\cos x$ 对 $0<x<\\pi$ 成立。再判断该不等式在 $-\\pi<x<0$ 是否成立，说明奇偶性在推广中的作用。\n\\end{exercise}\n\\begin{exercise}{306}{对数增量的双侧估计}\n设 $a>b>0$。用中值定理证明\n\\[\\frac{a-b}{a}<\\ln\\frac ab<\\frac{a-b}{b}.\\]\n固定 $b$，求 $a\\to b^+$ 时 $\\ln(a/b)$ 与这两个界的比值，说明严格不等号为何不妨碍一阶近似。\n\\end{exercise}\n\\begin{exercise}{307}{对数不等式与余项控制}\n用中值定理证明 $x/(1+x)<\\ln(1+x)<x$ 对 $x>0$ 成立。利用这一结论证明 $0<x-\\ln(1+x)<x^2/(1+x)$，并判断所得上界能否直接用于确定 $[x-\\ln(1+x)]/x^2$ 的精确极限。\n\\end{exercise}\n\\begin{exercise}{308}{指数函数的切线比较}\n用中值定理证明 $\\mathrm e^x>\\mathrm e x$ 对 $x>1$ 成立。进一步确定全部实数 $x$ 上 $\\mathrm e^x-\\mathrm e x$ 的最小值及等号条件，并解释两部分论证的联系。\n\\end{exercise}\n\\begin{exercise}{309}{导数恒等式与端点延拓}\n在 $(-1,1)$ 上用求导与中值定理证明 $\\arcsin x+\\arccos x=\\pi/2$，再将恒等式延拓至 $[-1,1]$。说明在端点不能直接使用通常的反三角函数求导公式，仍可得到等式的依据。\n\\end{exercise}\n\\begin{exercise}{310}{反三角函数的分段恒等式}\n证明 $2\\arctan x+\\arcsin[2x/(1+x^2)]=\\pi$ 对 $x\\ge1$ 成立。进一步求该表达式在 $0\\le x\\le1$ 上的简化式，说明反正弦主值范围为何导致分段。\n\\end{exercise}\n\\begin{exercise}{311}{乘积函数的中值等式}\n设 $f\\in C[a,b]$，在 $(a,b)$ 可导，$a<b$。证明存在 $\\xi\\in(a,b)$ 使\n\\[\\frac{bf(b)-af(a)}{b-a}=f(\\xi)+\\xi f'(\\xi).\\]\n取 $f(x)=x^2$、$[a,b]=[1,2]$ 求全部满足等式的点，并检查它们确实位于开区间内。\n\\end{exercise}\n\\begin{exercise}{312}{导数单调与次可加性}\n设 $c>0$，$f\\in C[0,c]$，在 $(0,c)$ 可导，$f'$ 单调不增，$f(0)=0$。对 $0\\le a\\le b\\le a+b\\le c$，用拉格朗日中值定理证明 $f(a+b)\\le f(a)+f(b)$。若 $f'$ 严格递减，讨论 $a=0$ 与 $a>0$ 两种情况下等号能否成立。\n\\end{exercise}\n\\begin{exercise}{313}{柯西中值定理与导数非零条件}\n对 $f(x)=\\sin x$、$g(x)=1+\\cos x$ 在 $[0,\\pi/2]$ 上验证柯西中值定理，求全部满足\n\\[\\frac{f(\\pi/2)-f(0)}{g(\\pi/2)-g(0)}=\\frac{f'(\\xi)}{g'(\\xi)}\\]\n的 $\\xi$。说明 $g'(0)=0$ 是否妨碍应用定理，以及分母为何在所求点处非零。\n\\end{exercise}\n\\begin{exercise}{314}{倒数变量与柯西中值定理}\n设 $0<a<b$，$f\\in C[a,b]$ 且在 $(a,b)$ 可导。用柯西中值定理证明存在 $\\xi\\in(a,b)$ 使\n\\[\\frac{af(b)-bf(a)}{a-b}=f(\\xi)-\\xi f'(\\xi).\\]\n明确选取的两个辅助函数，并指出 $a>0$ 在此证明中保证了什么。\n\\end{exercise}\n\\begin{exercise}{315}{幂函数参照与加权中值点}\n设 $0<a<b$，$f\\in C[a,b]$ 且在 $(a,b)$ 可导。证明存在 $\\xi\\in(a,b)$ 使\n\\[\\frac{f(b)-f(a)}{b-a}=(a^2+ab+b^2)\\frac{f'(\\xi)}{3\\xi^2}.\\]\n将区间改为 $[-1,1]$，判断上述含商等式是否仍对所有可导函数成立，并说明原证明中哪一条件失效。\n\\end{exercise}\n\\begin{exercise}{316}{对数复合函数的中值点}\n用拉格朗日中值定理证明存在 $\\xi\\in(1,\\mathrm e)$ 使 $\\sin1=\\cos(\\ln\\xi)$，写出中值定理所作用的区间与函数。利用余弦在 $(0,1)$ 上的单调性，证明这样的 $\\xi$ 唯一。\n\\end{exercise}\n\\begin{exercise}{317}{带参数的中值恒等式}\n设 $f\\in C[0,1]$，在 $(0,1)$ 可导，$f(0)=0$、$f(1)=1$。证明对每个实数 $\\lambda$ 都存在 $\\xi\\in(0,1)$ 使 $f'(\\xi)+\\lambda[f(\\xi)-\\xi]=1$。若要求同一个 $\\xi$ 对所有 $\\lambda$ 同时适用，现有条件是否足够？给出证明或反例。\n\\end{exercise}\n\\begin{exercise}{318}{线性插值误差与二阶中值定理}\n设 $f\\in C^2[a,b]$，$a<b$，$L(x)=[(b-x)f(a)+(x-a)f(b)]/(b-a)$。证明对每个 $x\\in(a,b)$ 存在 $\\xi\\in(a,b)$ 使 $f(x)-L(x)=\\tfrac12f''(\\xi)(x-a)(x-b)$。由此在 $|f''|\\le M$ 的条件下给出整个 $[a,b]$ 上的统一误差界，并说明界中常数能否改小。\n\\end{exercise}\n\\subsection{洛必达法则}\n\\begin{exercise}{319}{高阶分母与单侧无穷极限}\n讨论 $\\lim_{x\\to1}(x^3-3x^2+2)/(x^3-x^2-x+1)$ 是否存在，并分别求左右极限。先判断不定式类型，再用因式分解或洛必达法则分析零点阶数，说明不能在分母求导后为零时直接把该步写成有限数值。\n\\end{exercise}\n\\begin{exercise}{320}{基本对数极限与二阶修正}\n用洛必达法则求 $\\lim_{x\\to1}\\ln x/(x-1)$，核对使用条件。再求 $\\lim_{x\\to1}[\\ln x-(x-1)]/(x-1)^2$，说明再次求导前为何必须重新检查是否仍为不定式。\n\\end{exercise}\n\\begin{exercise}{321}{混合函数的一阶极限}\n用洛必达法则求 $\\lim_{x\\to1}[x^3-1+\\ln x]/(\\mathrm e^x-\\mathrm e)$。若将分子中的 $\\ln x$ 改为 $\\alpha\\ln x$，求使极限为零的实参数 $\\alpha$，再求该参数下整个商与 $x-1$ 的比值极限。\n\\end{exercise}\n\\begin{exercise}{322}{指数与多项式的增长比较}\n求 $\\lim_{x\\to+\\infty}(x^4+\\mathrm e^x)/(x\\mathrm e^x)$。进一步对实数 $p$ 讨论 $\\lim_{x\\to+\\infty}(x^4+\\mathrm e^x)/(x^p\\mathrm e^x)$，用洛必达法则或等价增长比较给出分类，不能只凭“指数增长快”省略关键极限。\n\\end{exercise}\n\\begin{exercise}{323}{三阶零点与连续洛必达}\n求 $\\lim_{x\\to0}(x-\\sin x)/(x^2\\sin x)$，每次使用洛必达法则前确认不定式。再求使 $x-\\sin x-cx^3=o(x^3)$ 的 $c$，说明结果与所求极限之间的关系。\n\\end{exercise}\n\\begin{exercise}{324}{对数与任意正幂的比较}\n设 $a>0$，求 $\\lim_{x\\to+\\infty}\\ln(x\\ln x)/x^a$，说明此处 $x$ 应取在什么范围。进一步讨论 $a=0$、$a<0$ 时的极限，展示正参数限制对结论的作用。\n\\end{exercise}\n\\begin{exercise}{325}{根式零点与指数三角相消}\n求 $\\lim_{x\\to0}(\\mathrm e^x-\\sin x-1)/(1-\\sqrt{1-x^2})$，写出实定义邻域。再把分子中的 $\\sin x$ 改为 $\\alpha\\sin x$，求使双侧有限极限存在的全部实数 $\\alpha$，并求相应极限。\n\\end{exercise}\n\\begin{exercise}{326}{反正切差与对数三阶零点}\n求 $\\lim_{x\\to0}(\\arctan x-x)/\\ln(1+2x^3)$，给出对数在零点附近有意义的依据。将分母改为 $\\ln(1+2x^2)$ 后再求极限，并从零点阶数说明两者不同的原因。\n\\end{exercise}\n\\begin{exercise}{327}{多个无穷小因子的主阶}\n求\n\\[\\lim_{x\\to0}\\frac{\\sin^2x-x^2\\cos^2x}{\\sin x(\\mathrm e^{2x}-1)\\ln(1+\\tan^2x)}.\\]\n先分别确定分子与分母的最低非零阶，再选用洛必达法则或等价无穷小完成计算，说明为何分子中的两项不能直接分别替换为 $x^2$ 后相减。\n\\end{exercise}\n\\begin{exercise}{328}{参数导致的零点阶数变化}\n设 $a^2+b^2\\ne0$。求使\n\\[\\lim_{x\\to0}\\frac{a\\tan x+b(1-\\cos x)}{c\\ln(1-2x)+d(1-\\mathrm e^{-x^2})}=2\\]\n成立的全部实参数 $(a,b,c,d)$，分别处理 $c\\ne0$、$c=0,d\\ne0$、$c=d=0$。据此判断 $b=4d$、$b=-4d$、$a=4c$、$a=-4c$ 中哪些是所有可行参数必满足的关系。\n\\end{exercise}\n\\begin{exercise}{329}{对数三角复合的二阶相消}\n求 $\\lim_{x\\to0}(1-\\cos x)[x-\\ln(1+\\tan x)]/\\sin^4x$。先求 $[x-\\ln(1+\\tan x)]/x^2$ 的极限，再组合结果，检查对数真数在零点邻域的正性。\n\\end{exercise}\n\\begin{exercise}{330}{嵌套正弦的等价无穷小}\n求 $\\lim_{x\\to0}[\\sin x-\\sin(\\sin x)]\\sin x/x^4$。明确内变量 $u=\\sin x$ 的使用，并进一步求 $[\\sin x-\\sin(\\sin x)]/x^3$ 的极限，说明这两个极限的联系。\n\\end{exercise}\n\\begin{exercise}{331}{无穷量相减的恒等化简}\n求 $\\lim_{x\\to0}x^{-1}(1/\\sin x-1/\\tan x)$。先合并为一个分式，再用半角公式或洛必达法则求值；说明两个倒数项分别无界时为何不能单独取极限再作减法。\n\\end{exercise}\n\\begin{exercise}{332}{多项式与指数衰减的参数条件}\n设 $n$ 为正整数、$\\lambda>0$，求 $\\lim_{x\\to+\\infty}x^n\\mathrm e^{-\\lambda x}$，给出能处理任意 $n$ 的论证。再讨论 $\\lambda=0$ 与 $\\lambda<0$ 时的极限，说明正参数假设的必要性。\n\\end{exercise}\n\\begin{exercise}{333}{零乘无穷与线性变量替换}\n求 $\\lim_{x\\to1}(1-x)\\tan(\\pi x/2)$，分别说明左右两侧的乘积符号。通过令 $t=\\pi(1-x)/2$ 化为基本三角极限，再用洛必达法则核验。\n\\end{exercise}\n\\begin{exercise}{334}{三角无穷量之差与可去间断}\n求 $\\lim_{x\\to\\pi/2}(\\sec x-\\tan x)$。先用共轭恒等式消去无穷量相减，给出左右极限，并判断原表达式在 $\\pi/2$ 补值后是否可导；可导时求导数。\n\\end{exercise}\n\\begin{exercise}{335}{倒数差的补值与导数}\n设 $h(x)=1/x-1/(\\mathrm e^x-1)$，$x\\ne0$。求 $\\lim_{x\\to0}h(x)$，补定义 $h(0)$ 使其连续，再判断补值后的函数在 $0$ 是否可导并求导数。每次合并分式后说明所用极限方法的条件。\n\\end{exercise}\n\\begin{exercise}{336}{二阶主部消去与偶性}\n求 $\\lim_{x\\to0}[1/x^2-1/(x\\tan x)]$。给出连续补值后函数在 $0$ 的导数，并说明偶性只有在可导性已经建立后才能用于确定导数值。\n\\end{exercise}\n\\begin{exercise}{337}{零的零次幂型极限}\n求 $\\lim_{x\\to0^+}x^x$，通过取对数把它化为可应用洛必达法则的形式。进一步求 $\\lim_{x\\to0^+}(x^x-1)/(x\\ln x)$，说明原底数必须取正的原因。\n\\end{exercise}\n\\begin{exercise}{338}{一的无穷次幂型与符号}\n求 $\\lim_{x\\to1}x^{1/(1-x)}$，明确取对数后分母的符号。对实参数 $a$ 求 $\\lim_{x\\to1}x^{a/(1-x)}$，说明 $a=0$ 时与一般公式是否相容。\n\\end{exercise}\n\\begin{exercise}{339}{三角分母指数的幂极限}\n求 $\\lim_{x\\to0}(1+3x)^{2/\\sin x}$，给出底数为正的邻域。再求对实参数 $a,b$ 的 $\\lim_{x\\to0}(1+ax)^{b/\\sin x}$，说明双侧取极限的合法性与指数为零的情形。\n\\end{exercise}\n\\begin{exercise}{340}{二阶对数之比的幂极限}\n求 $\\lim_{x\\to0}(\\cos x)^{1/\\ln(1+x^2)}$。先确定取实数幂时底数为正的邻域，再处理对数之比。将分母改为 $\\ln(1+ax^2)$、$a>0$ 后给出参数结果。\n\\end{exercise}\n\\begin{exercise}{341}{趋零底数与趋零指数}\n求 $\\lim_{x\\to+\\infty}(x^{1/x}-1)^{1/\\ln x}$，先证明底数在所考虑范围为正。取对数后使用 $\\mathrm e^u-1\\sim u$，分开处理 $\\ln x$ 与 $\\ln\\ln x$ 的增长，不能把指数趋于零直接解释为极限为 $1$。\n\\end{exercise}\n\\begin{exercise}{342}{双指数平均的幂极限}\n设 $a,b>0$，求 $\\lim_{x\\to0}[(a^x+b^x)/2]^{3/x}$。进一步讨论一般实参数 $p$ 下指数改为 $p/x$ 的结果，并核验 $a=b$ 时可由原表达式直接得到同一结论。\n\\end{exercise}\n\\begin{exercise}{343}{复合指数差的无穷小阶数}\n求实数 $n>0$，使 $x\\to0^+$ 时 $\\mathrm e^{\\tan x}-\\mathrm e^x$ 与 $x^n$ 为同阶无穷小，并求两者比值的非零极限。说明若把“同阶”加强为“等价”，是否仍能直接使用 $x^n$，应如何调整主项系数。\n\\end{exercise}\n\\begin{exercise}{344}{分段函数的连续补值与高阶信息}\n设 $f(x)=[\\sin2x+\\mathrm e^{2ax}-1]/x$（$x\\ne0$）、$f(0)=a$。求使 $f$ 在实数轴连续的全部实参数 $a$，再判断相应函数在 $0$ 是否可导并求导数。注意参数同时出现于非零分支和补定义值中，必须解出由连续性产生的参数方程。\n\\end{exercise}\n\\begin{exercise}{345}{幂函数的连续延拓}\n在 $0<|x|<\\pi/2$ 设 $f(x)=(\\cos x)^{x^2}$，令 $f(0)=a$。求使其在 $0$ 连续的 $a$，再求 $\\lim_{x\\to0}[f(x)-a]/x^4$。比较将指数改为 $1/x^2$ 时的连续补值，说明指数中幂次对结果的影响。\n\\end{exercise}\n\\begin{exercise}{346}{端点奇异项的抵消}\n设 $f(x)=1/(\\pi x)+1/\\sin\\pi x-1/[\\pi(1-x)]$，$1/2\\le x<1$。求连续延拓值 $f(1)$，再求 $\\lim_{x\\to1^-}[f(x)-f(1)]/(x-1)$。令 $t=1-x$ 后明确哪些奇异项相消，不能分别代入取值。\n\\end{exercise}\n\\begin{exercise}{347}{迭代数列与相邻项的幂极限}\n设 $0<x_1<\\pi$，$x_{n+1}=\\sin x_n$。证明数列从某项起严格递减且为正，求其极限；再分别求 $\\lim_{n\\to\\infty}(x_{n+1}/x_n)^{1/x_n}$ 与 $\\lim_{n\\to\\infty}(x_{n+1}/x_n)^{1/x_n^2}$，并说明即使 $x_1>\\pi/2$ 也不影响论证。\n\\end{exercise}\n\\begin{exercise}{348}{洛必达法则失效时的原极限}\n设 $f(x)=x+\\sin x$、$g(x)=x$，$x>0$。求 $\\lim_{x\\to+\\infty}f(x)/g(x)$，并证明 $f'(x)/g'(x)$ 没有极限。由此说明洛必达法则的导数比极限条件是应用定理的条件，能否把它当成原商有极限的必要条件。\n\\end{exercise}\n\\begin{exercise}{349}{参数主项消去与幂极限}\n设 $a\\in\\mathbb R$，求 $\\lim_{x\\to0}(1+x+ax^2)^{1/x}$，再讨论 $\\lim_{x\\to0}(1+x+ax^2)^{1/x^2}\\mathrm e^{-1/x}$。说明底数在零点附近为正，并用对数变换解释两问需要的不同展开阶数。\n\\end{exercise}\n\\subsection{泰勒公式}\n\\begin{exercise}{350}{两类泰勒余项与误差估计}\n对任意正整数 $n$，写出 $\\mathrm e^x$ 的 $n$ 阶麦克劳林公式，分别使用拉格朗日型余项与佩亚诺型余项。用三次麦克劳林多项式近似 $\\mathrm e^{0.1}$，给出保证成立的绝对误差上界；说明仅写 $o(x^3)$ 能否直接提供这一数值误差界。\n\\end{exercise}\n\\begin{exercise}{351}{展开阶数与商的极限}\n用泰勒公式求 $\\lim_{x\\to0}x\\ln(1+x)/(\\mathrm e^x-x-1)$，并求\n\\[\\lim_{x\\to0}\\frac1x\\left[\\frac{x\\ln(1+x)}{\\mathrm e^x-x-1}-2\\right].\\]\n说明求第二个极限时分子、分母分别至少需要展开到哪一阶。\n\\end{exercise}\n\\begin{exercise}{352}{三角函数的高阶消去}\n用带佩亚诺余项的展开求 $\\lim_{x\\to0}(\\sin x-x\\cos x)/\\tan^3x$。进一步求分子减去其三次主项后的五次主项，并说明仅将 $\\sin x$ 换为 $x$ 为何会丢失所求信息。\n\\end{exercise}\n\\begin{exercise}{353}{对称展开与偶次误差}\n求 $\\lim_{x\\to0}[\\sqrt{1+x}+\\sqrt{1-x}-2]/x^2$。再求实数 $c$，使 $\\sqrt{1+x}+\\sqrt{1-x}-2-cx^2=o(x^2)$，并计算该差与 $x^4$ 的比值极限。\n\\end{exercise}\n\\begin{exercise}{354}{有限极限确定多项式系数}\n求使 $\\lim_{x\\to0}[\\ln(1+x)-ax-bx^2]/x^2=2$ 的全部实数 $(a,b)$。对所得参数，继续求分子减去 $2x^2$ 后与 $x^3$ 的比值极限，写出保证运算有效的余项阶数。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:15:01Z




## tool · 2026-10-20T03:17:24Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"4623ac","wall_time_seconds":0.000008375,"exit_code":0,"original_token_count":120,"output":"\\section{第2章 导数与微分}\n\\subsection{导数的基本概念}\n\\begin{exercise}{151}{定义求导与线性主部}\n用导数定义求 $f(x)=1+2x+3x^2$ 的 $f'(1)$，并把 $f(1+h)-f(1)$ 写成线性主部与余项之和，验证余项为 $o(h)$。\n\\end{exercise}\n\\begin{exercise}{152}{零因子处的导数}\n设 $f(x)=x(2x+1)(3x+2)(4x+3)$。不展开多项式，求 $f'(0)$；再求 $f'(-1/2)$，说明在单零点处如何利用其余因子的连续性。\n\\end{exercise}\n"}
{}
{}
{"chunk_id":"a68b62","wall_time_seconds":0.000007041,"exit_code":0,"original_token_count":123,"output":"\\end{exercise}\n\\begin{exercise}{286}{常规·参数函数微分}\n设 $f$ 可导且 $f'(0)\\ne0$，$x=f(\\ln t)$、$y=f(t^2-1)$（$t>0$）。求 $t=1$ 时的 $\\dd y$，分别用 $\\dd x$ 与 $\\dd t$ 表示。\n\\end{exercise}\n\\begin{exercise}{287}{基础·微分近似}\n用微分估算 $\\sqrt{4.04}$。\n\\end{exercise}\n\\begin{exercise}{288}{常规·隐函数微分综合}\n设 $ye^y=x$ 在 $(e,1)$ 附近确定 $y(x)$。求该点的微分，并用它估算 $x=e+0.02$ 时的 $y$。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:17:28Z


Script completed
Wall time 0.1 seconds
Output:

Warning: truncated output (original token count: 10643)
Total output lines: 2

{"chunk_id":"5bff25","wall_time_seconds":0.000006791,"exit_code":0,"original_token_count":5330,"output":"\\begin{exercise}{355}{四阶相消与复合展开}\n用泰勒公式求\n\\[\\lim_{x\\to0}\\frac{1+\\tfrac12x^2-\\sqrt{1+x^2}}{(\\cos x-\\mathrm e^{x^2})\\sin(x^2)}.\\]\n再将分母中的 $\\mathrm e^{x^2}$ 改为 $\\mathrm e^{\\alpha x^2}$，讨论极限随实参数 $\\alpha$ 的变化，必要时区分左右极限。\n\\end{exercise}\n\\begin{exercise}{356}{指数与余弦的四阶比较}\n讨论 $\\lim_{x\\to0}[\\cos x-\\mathrm e^{x^2/2}]/x^4$，允许结果为无穷大。进一步确定 $a,b$，使 $\\cos x-\\mathrm e^{ax^2+bx^4}=o(x^4)$，并解释二次项匹配后仍须比较四次项的原因。\n\\end{exercise}\n\\begin{exercise}{357}{隐含余项与函数极限恢复}\n设 $f$ 在 $0$ 的某去心邻域有定义，且 $\\lim_{x\\to0}[\\sin(6x)+xf(x)]/x^3=0$。不用假设 $f$ 可导，求 $\\lim_{x\\to0}[6+f(x)]/x^2$。若已知条件中的分母仅为 $x^2$，这一极限是否仍能唯一确定？给出两个具体函数说明。\n\\end{exercise}\n\\begin{exercise}{358}{高阶无穷小与参数消去}\n求使 $\\mathrm e^x-(ax^2+bx+1)=o(x^2)$ 的全部实数 $(a,b)$。对所得参数，求余项的无穷小阶数和非零主项系数；说明 $o(x^2)$ 与 $O(x^2)$ 两种条件对参数的约束有何不同。\n\\end{exercise}\n\\begin{exercise}{359}{根式差的阶数与连续消去}\n当 $x\\to0$ 时，求 $\\sqrt{1-2x}-\\sqrt[3]{1-3x}$ 相对于 $x$ 的无穷小阶数及主项。进一步求常数 $c$，使减去 $cx^2$ 后成为三阶无穷小，并求相应三阶主项系数。\n\\end{exercise}\n\\begin{exercise}{360}{泰勒系数与高阶导数}\n设 $f(x)=\\ln(1-3x)$。求任意正整数 $n$ 对应的 $f^{(n)}(0)$，并分别用归纳求导和麦克劳林系数验证。写出四阶麦克劳林多项式，说明其在 $0$ 附近的实函数定义范围。\n\\end{exercise}\n\\begin{exercise}{361}{泰勒余项的符号}\n用带拉格朗日余项的泰勒公式证明 $\\mathrm e^x>1+x$ 对 $x\\ne0$ 成立，须同时处理 $x<0$。进一步证明对 $x\\ge0$ 有 $\\mathrm e^x\\ge1+x+x^2/2$，并确定等号成立条件。\n\\end{exercise}\n\\begin{exercise}{362}{两端泰勒公式与三阶中值}\n设 $f\\in C^3[-1,1]$，$f(-1)=0$、$f(1)=1$、$f'(0)=0$。分别在 $0$ 处展开至二阶，证明存在 $\\xi\\in(-1,1)$ 使 $f'''(\\xi)=3$。若将 $f'(0)$ 改为 $m$，推导相应三阶导数中值结论，并给出常数 $3$ 的来源。\n\\end{exercise}\n\\begin{exercise}{363}{最低点与二阶导数下界}\n设 $f\\in C^2[0,1]$，$f(0)=f(1)=0$，且在 $[0,1]$ 上的最小值为 $-1$。证明存在 $\\xi\\in(0,1)$ 使 $f''(\\xi)\\ge8$。构造满足条件且处处 $f''(x)=8$ 的函数，说明常数 $8$ 无法提高；证明中应明确最低点位于内部的依据。\n\\end{exercise}\n\\begin{exercise}{364}{双参数相消与极限分类}\n对实数 $a,b$，讨论 $\\lim_{x\\to0}[\\mathrm e^{ax}-1-ax-bx^2]/x^3$ 何时为有限实数，并求其值。再求使分子为 $o(x^3)$ 的全部 $(a,b)$，包括 $a=0$ 的情形。\n\\end{exercise}\n\\begin{exercise}{365}{中心差分的误差保证}\n设 $f\\in C^3[x_0-h,x_0+h]$，$h>0$，且 $|f'''(x)|\\le M$。用泰勒公式证明中心差分 $[f(x_0+h)-f(x_0-h)]/(2h)$ 与 $f'(x_0)$ 的误差不超过 $Mh^2/6$。构造一个三次多项式使此界取等号，并讨论仅有 $f''(x_0)$ 存在是否足以保证该误差界。\n\\end{exercise}\n\\subsection{函数的单调性与曲线的凹凸性}\n\\begin{exercise}{366}{分数幂的定义域与单调性}\n讨论 $f(x)=x-\\tfrac32x^{2/3}$ 在实数范围内的单调区间，指出驻点与不可导点。若将定义域限制为 $[0,+\\infty)$，说明单调区间的结论应如何表述，并比较两种定义域下 $x=0$ 附近的行为。\n\\end{exercise}\n\\begin{exercise}{367}{逐层求导证明严格不等式}\n用导数证明 $\\tan x>x+x^3/3$ 对 $0<x<\\pi/2$ 成立。进一步证明 $\\tan x-x-x^3/3=o(x^3)$，并解释严格正性与高阶小量这两个结论为何可以同时成立。\n\\end{exercise}\n\\begin{exercise}{368}{函数比较与商的单调性}\n证明当 $x>0$ 时 $\\ln(1+x)>\\arctan x/(1+x)$。将不等式化为一个在 $0$ 处取零值的函数的正性，再证明该函数在 $(0,+\\infty)$ 严格递增，给出导数符号的完整依据。\n\\end{exercise}\n\\begin{exercise}{369}{严格单调与导数符号的逻辑关系}\n设 $f$ 在 $\\mathbb R$ 可导且严格递增。证明 $f'(x)\\ge0$，判断能否进一步断言处处 $f'(x)>0$；分别判断 $f(-x)$、$-f(-x)$ 的严格单调性，以及 $f'(-x)$ 的符号。对不成立的加强结论给出具体反例。\n\\end{exercise}\n\\begin{exercise}{370}{偶函数方程的根数}\n讨论方程 $|x|^{1/4}+|x|^{1/2}-\\cos x=0$ 的实根个数。先将根限制在一个有界区间，再利用偶性与正半轴上的单调性证明结论；不以数值近似代替唯一性证明。\n\\end{exercise}\n\\begin{exercise}{371}{三次函数与零点个数分岔}\n对全部实参数 $a$，讨论方程 $x^3-3x-a=0$ 的不同实根个数，特别求出恰有两个不同实根的参数。给出临界参数下各根的重数，并用单调区间解释根数发生变化的原因。\n\\end{exercise}\n\\begin{exercise}{372}{参数约束与高次方程唯一根}\n设实数 $a,b,c$ 满足 $3a^2-5b<0$。证明方程 $x^5-2ax^3+3bx+4c=0$ 有且仅有一个实根。若条件放宽为 $3a^2-5b\\le0$，判断结论是否仍成立，并处理导数可能为零的情形。\n\\end{exercise}\n\\begin{exercise}{373}{严格凸函数的割线斜率}\n设 $f\\in C^2[a,b]$，$a<b$，且 $f''(x)>0$ 对 $a<x<b$ 成立。令 $F(x)=[f(x)-f(a)]/(x-a)$，$a<x\\le b$。证明 $F$ 严格递增，并给出它在 $a$ 处的连续延拓值。若仅知 $f'(x)>0$，该单调性是否仍有保证？给出反例。\n\\end{exercise}\n\\begin{exercise}{374}{幂指数比较与参数边界}\n设 $a>\\mathrm e$，证明对每个 $x>0$ 有 $(a+x)^a<a^{a+x}$。进一步求使这一严格不等式对所有 $x>0$ 成立的全部 $a>0$，并单独处理临界值 $a=\\mathrm e$。\n\\end{exercise}\n\\begin{exercise}{375}{导数下界与最优统一常数}\n设 $\\mathrm e<a<b<\\mathrm e^2$。证明 $\\ln^2b-\\ln^2a>4(b-a)/\\mathrm e^2$。再证明 $4/\\mathrm e^2$ 是使该不等式对全部上述 $a,b$ 成立的最大常数；说明为何开区间中的严格不等号仍允许最优常数由端点极限确定。\n\\end{exercise}\n\\begin{exercise}{376}{二阶导数不存在处的凹凸变化}\n设 $f(x)=x^{8/3}-x^{5/3}$，其中分数幂按实立方根定义。求定义域、所有凹凸区间和拐点坐标，分别处理二阶导数为零与二阶导数不存在的点。表述凹凸性时同时注明 $f''$ 的符号，避免名称约定造成歧义。\n\\end{exercise}\n\\begin{exercise}{377}{绝对值与三角曲线凹凸}\n设 $f(x)=|1+\\sin x|$。判断它在 $(\\pi,3\\pi/2)$ 内的严格单调性与凹凸性，写出导数符号依据。再讨论 $x=3\\pi/2$ 处的可导性与二阶可导性，说明绝对值能否在全实数范围内直接去掉。\n\\end{exercise}\n\\begin{exercise}{378}{严格凸性与中点不等式}\n证明对实数 $x\\ne y$ 有 $(\\mathrm e^x+\\mathrm e^y)/2>\\mathrm e^{(x+y)/2}$。进一步设 $0<t<1$，用导数或中值定理证明 $t\\mathrm e^x+(1-t)\\mathrm e^y>\\mathrm e^{tx+(1-t)y}$，并完整说明等号出现的条件。\n\\end{exercise}\n\\begin{exercise}{379}{分段曲线的凹凸与不可导点}\n设 $f(x)=|x^2-3x+2|$。写出分段表达式，求二阶导数存在的全部凹凸区间，并检查 $x=1,2$ 的连续性和可导性。本题将拐点定义为曲线上连续且两侧凹凸性发生改变的点，按此定义求全部拐点，并说明它们是否均满足 $f''(x)=0$。\n\\end{exercise}\n\\begin{exercise}{380}{拐点的参数充要条件}\n求使 $(0,1)$ 成为曲线 $y=ax^3+bx^2+c$ 拐点的全部实数 $(a,b,c)$。证明条件的充分性与必要性，并解释为何仅有 $f''(0)=0$ 不能排除退化的直线或常函数。\n\\end{exercise}\n\\begin{exercise}{381}{偶性与各阶导数的符号}\n设 $f\\in C^2(\\mathbb R)$ 为偶函数，在 $(-\\infty,0)$ 有 $f'>0$、$f''<0$。推导 $f'$、$f''$ 的奇偶性，确定它们在 $(0,+\\infty)$ 的符号。判断 $0$ 是否为极值点或拐点，并说明依据。\n\\end{exercise}\n\\begin{exercise}{382}{三阶判别与水平拐点}\n设 $f$ 在 $x_0$ 的邻域三阶可导，$f'(x_0)=f''(x_0)=0$、$f'''(x_0)>0$。证明 $(x_0,f(x_0))$ 为拐点，判断 $x_0$ 是否为极值点。分别通过 $f''$ 的符号变化与泰勒展开说明结论，并指出此处二阶极值判别法不能直接作出判断。\n\\end{exercise}\n\\begin{exercise}{383}{微分关系与局部几何形态}\n设 $f\\in C^2(-\\delta,\\delta)$，$\\delta>0$，满足 $f''(x)+[f'(x)]^2=x$，且 $f'(0)=0$。由该关系证明 $f'''(0)$ 存在并求其值，判断 $0$ 是否为极值点及 $(0,f(0))$ 是否为拐点。论证时须给出足够小邻域内的导数或函数增量符号。\n\\end{exercise}\n\\begin{exercise}{384}{函数图形信息与导函数图形}\n设 $f(x)=x^3-3x$。先由单调区间和驻点说明 $f'$ 应有的符号与零点，再由凹凸性判断 $f'$ 的单调性，据此手绘 $f'$ 的图形。最后计算 $f'$ 核验，说明 $f$ 的极值点与 $f'$ 的零点之间是否总为一一对应。\n\\end{exercise}\n\\begin{exercise}{385}{参数函数的单调区间与严格单调}\n设 $f_a(x)=x^3-3ax$，$a\\in\\mathbb R$。求全部单调区间，确定使 $f_a$ 在整个实数轴上严格递增的参数。对临界参数解释严格递增为何允许导数在孤立点为零，并求该函数的拐点。\n\\end{exercise}\n\\begin{exercise}{386}{凸性与零点定位}\n设 $f\\in C^2[0,1]$，$f(0)=f(1)=0$，且 $f''(x)>0$ 对 $0<x<1$ 成立。证明内部恒有 $f(x)<0$，并证明 $f'$ 在 $(0,1)$ 内恰有一个零点。若将条件改为 $f''\\ge0$，判断两个严格结论分别是否仍成立，给出反例或证明。\n\\end{exercise}\n\\subsection{函数的极值和最值}\n\\begin{exercise}{387}{极大值的必要条件与二阶退化}\n设 $f$ 在 $x_0$ 的邻域二阶可导，并在 $x_0$ 取得局部极大值。证明 $f'(x_0)=0$、$f''(x_0)\\le0$。分别举出二阶导数严格小于零和等于零的例子，说明这两个必要条件能否反过来保证极大值。\n\\end{exercise}\n\\begin{exercise}{388}{驻点与不可导点的极值判别}\n设 $f(x)=2x-\\tfrac32x^{2/3}+1$，分数幂按实立方根定义。求所有驻点、不可导点和极值，用一阶导数符号进行判别。进一步判断该函数在 $\\mathbb R$ 上是否有最大值、最小值，说明极值与最值的区别。\n\\end{exercise}\n\\begin{exercise}{389}{指数乘积的全局最小值}\n求 $f(x)=x2^x$ 的极小值点与极小值，证明该极小值也是全实数范围的最小值。再判断是否存在最大值，并用两端极限支持结论。\n\\end{exercise}\n\\begin{exercise}{390}{导函数符号与极值数量}\n设 $f$ 在 $\\mathbb R$ 可导，且 $f'(x)=x(x+2)(x-1)^2(x-3)$。不用求出 $f$，列出导函数符号表，确定 $f$ 的单调区间以及极大值点、极小值点的数量与位置。说明 $x=1$ 处导数为零却不产生极值的原因，判断仅知导函数能否给出各极值的数值。\n\\end{exercise}\n\\begin{exercise}{391}{微分方程约束下的驻点分类}\n设 $f$ 在实数轴二阶可导，满足 $xf''(x)+3x[f'(x)]^2=1-\\mathrm e^{-x}$。若 $f'(x_0)=0$ 且 $x_0\\ne0$，证明 $x_0$ 必为严格极小值点，并排除拐点的可能性。进一步利用关系式在 $0$ 附近的极限讨论 $f''(0)$ 与 $f'(0)$ 满足的等式。\n\\end{exercise}\n\\begin{exercise}{392}{导数比值极限与极值}\n设 $f$ 在 $a$ 的邻域可导，$f'$ 在 $a$ 连续，且 $\\lim_{x\\to a}f'(x)/(x-a)=-1$。求 $f'(a)$、$f''(a)$，判断 $a$ 处的极值类型。若已知极限改为 $0$，说明极值类型能否确定，并给出例子。\n\\end{exercise}\n\\begin{exercise}{393}{二阶增量极限的信息边界}\n设 $f$ 在 $a$ 的邻域有定义，且 $\\lim_{x\\to a}[f(x)-f(a)]/(x-a)^2=-1$。证明 $f$ 在 $a$ 可导，求 $f'(a)$ 并判断极值类型。判断该极限能否保证 $f''(a)$ 存在；若不能，构造在 $a$ 的邻域可导的反例。\n\\end{exercise}\n\\begin{exercise}{394}{分段指数函数与不可导极值点}\n设 $f(x)=x^{2x}$（$x>0$）、$f(x)=x\\mathrm e^x+1$（$x\\le0$）。求各分支导数并检查 $0$ 处的连续性和可导性，确定所有局部极值。再比较各极小值与两端极限，判断全实数范围的最大值和最小值是否存在。\n\\end{exercise}\n\\begin{exercise}{395}{隐函数驻点与局部分支}\n曲线由 $2y^3-2y^2+2xy-x^2=1$ 给出。在满足隐函数定理条件的点附近把 $y$ 看作 $x$ 的函数，求全部驻点及对应坐标，并判断极值类型。每个候选点均须检验关于 $y$ 的偏导数非零，不能只解 $y'=0$ 的分子。\n\\end{exercise}\n\\begin{exercise}{396}{无极值的参数范围}\n求使 $f(x)=x^3+3ax^2-ax-1$ 在实数轴上无局部极值的全部实参数 $a$。处理导数有两个实根、重根、无实根三种情况，说明临界参数下驻点为何不构成极值。\n\\end{exercise}\n\\begin{exercise}{397}{闭区间最值与根式端点}\n求 $f(x)=x+\\sqrt{1-x}$ 在 $[-5,1]$ 上的最大值和最小值及全部取到位置。列全内部驻点与端点，并说明 $x=1$ 处导数不存在为何不影响闭区间最值的存在。\n\\end{exercise}\n\\begin{exercise}{398}{球外切圆锥的最小体积}\n半径 $r>0$ 的球内切于正圆锥，求圆锥高 $h$ 使体积最小，并求最小体积。先由轴截面建立底面半径与 $h,r$ 的关系及 $h$ 的可行范围，再证明所得驻点给出全局最小值，同时检验可行区间两端的体积极限。\n\\end{exercise}\n\\begin{exercise}{399}{利润最值与整数产量}\n某企业月产量为 $Q$，总成本 $C(Q)=6Q+200$，总收益 $R(Q)=12Q-0.01Q^2$，金额单位均为万元。先把 $Q\\ge0$ 视为连续变量，求利润最大时的产量和最大利润，再在 $Q$ 必须为非负整数时核对结论。求企业盈利的产量范围，并区分利润与收益。\n\\end{exercise}\n\\begin{exercise}{400}{收入成本与边际量的最优条件}\n某企业的总收入为 $R(x)=26x-2x^2-4x^3$，总成本为 $C(x)=8x+x^2$，产量 $x\\ge0$ 视为连续变量。求利润函数、边际收入和边际成本，确定利润最大时的产量与最大利润。核验最优点处边际收入等于边际成本，并说明还需哪些符号或边界检查才能证明为全局最大值。\n\\end{exercise}\n\\begin{exercise}{401}{共轭指数与等号条件}\n设 $p,q>1$ 且 $1/p+1/q=1$。利用函数最值证明对 $x>0$ 有 $x^p/p+1/q\\ge x$，确定等号条件。再推出对 $u,v>0$ 有 $uv\\le u^p/p+v^q/q$，说明代换过程中使用共轭指数关系的位置。\n\\end{exercise}\n\\begin{exercise}{402}{极限给定的切线与严格凸性}\n设 $f\\in C^2(\\mathbb R)$，$\\lim_{x\\to0}f(x)/x=1$，且 $f''(x)>0$ 对所有实数 $x$ 成立。由极限确定 $f(0)$、$f'(0)$，利用最值或中值定理证明 $f(x)\\ge x$，并确定等号条件。若仅有 $f''\\ge0$，说明等号条件会怎样变化。\n\\end{exercise}\n\\begin{exercise}{403}{约束区间与边界最优}\n设 $a\\in\\mathbb R$，$f_a(x)=x^2-2ax$，生产控制量满足 $0\\le x\\le1$。求最小值与全部最小值点随 $a$ 的分段表达式，再求最大值和全部最大值点。解释为何只求驻点会遗漏部分参数下的最优解。\n\\end{exercise}\n\\begin{exercise}{404}{箱体设计与可行域端点}\n从边长为 $L>0$ 的正方形薄板四角各剪去边长为 $x$ 的小正方形，折成无盖长方体。写出体积与严格可行域，求最大体积及对应 $x$，证明全局最优性。若要求底面边长至少为 $L/2$，判断最优方案是否改变并说明依据。\n\\end{exercise}\n\\subsection{函数图形的描绘}\n\\begin{exercise}{405}{水平渐近线与交点}\n求 $y=(x+1)/x$ 在 $x\\to+\\infty$ 与 $x\\to-\\infty$ 时的水平渐近线，并求铅直渐近线。判断曲线是否与水平渐近线相交，分别说明曲线在两支上从哪一侧逼近该直线。\n\\end{exercise}\n\\begin{exercise}{406}{单侧无穷极限与铅直渐近线}\n求 $y=1/(1-x^2)$ 的全部铅直渐近线，分别写出每条直线左右两侧的无穷极限。再求水平渐近线，并说明有界的间断点为何不能仅因函数未定义而判为铅直渐近线。\n\\end{exercise}\n\\begin{exercise}{407}{约分、可去间断与渐近线}\n求 $f(x)=(x^2-x-2)/(x^2-1)$ 的定义域、水平渐近线与铅直渐近线。分别判断 $x=1,-1$ 处的间断类型，并说明代数约分为何不能恢复原函数定义域中缺失的点。\n\\end{exercise}\n\\begin{exercise}{408}{斜渐近线与曲线位置}\n求 $y=x^2/(x-1)$ 的斜渐近线和铅直渐近线，分别检验正负无穷方向的极限。利用函数与斜渐近线的差，判断两支曲线位于该直线的哪一侧，以及是否存在交点。\n\\end{exercise}\n\\begin{exercise}{409}{指数复合函数的单侧渐近线}\n求 $y=(2x-1)\\mathrm e^{1/x}$ 的全部水平、铅直和斜渐近线。重点分别计算 $x\\to0^+$、$x\\to0^-$ 的极限与 $x\\to\\pm\\infty$ 时的斜截距，说明同一铅直渐近线的两侧是否都必须发散。\n\\end{exercise}\n\\begin{exercise}{410}{振荡因子与渐近线判定}\n对定义在 $x>0$ 的函数 $f(x)=x\\sin(1/x)$，求全部水平与铅直渐近线，并讨论 $x\\to0^+$ 时能否连续补值。说明 $\\sin(1/x)$ 的振荡为何不妨碍 $f$ 在右端点有有限极限。\n\\end{exercise}\n\\begin{exercise}{411}{两端斜渐近线与单侧发散}\n求 $f(x)=x\\mathrm e^{1/x}$ 的全部水平、铅直和斜渐近线。写出 $0$ 两侧的极限，并证明在正负无穷处得到的斜渐近线相同。\n\\end{exercise}\n\\begin{exercise}{412}{对数指数函数的渐近线条数}\n求 $f(x)=\\ln(1+\\mathrm e^x)/x$ 的全部渐近线，分别处理 $x\\to0^\\pm$、$x\\to\\pm\\infty$。对正无穷方向先抽出对数中的主导指数，再说明是否还可能存在斜率非零的斜渐近线。\n\\end{exercise}\n\\begin{exercise}{413}{反正切复合与有限间断辨析}\n求 $f(x)=\\mathrm e^{1/x}\\arctan[(x^2-x+2)/((x-1)(x+2))]$ 的定义域及全部渐近线，给出渐近线总条数。分别检查 $x=0,1,-2$ 两侧的极限，区分无穷间断和有限跳跃，并计算正负无穷方向的极限。\n\\end{exercise}\n\\begin{exercise}{414}{有理函数的完整图形分析}\n对 $f(x)=(x-1)^3/(x+1)^2$，求定义域、截距、全部渐近线、单调区间、极值、凹凸区间和拐点，注明关键点及两端趋势，据此手绘图形。用精确计算说明曲线是否能够穿过其斜渐近线；若能，求交点。\n\\end{exercise}\n\\begin{exercise}{415}{周期函数的图形描绘}\n对 $f(x)=\\cos x/\\cos2x$，确定定义域、奇偶性与最小正周期。在 $[-\\pi,\\pi]$ 内求全部铅直渐近线、与坐标轴的交点、单调区间、极值、凹凸区间和拐点，据此手绘该区间图形并说明如何延拓至全定义域。\n\\end{exercise}\n\\begin{exercise}{416}{渐近线可被穿越}\n设 $f(x)=x+\\sin x/x$，$x\\ne0$。求它的全部渐近线，并判断 $0$ 处的间断类型。求与斜渐近线的全部交点，证明在任意充分大的正半轴尾部仍存在交点，说明渐近线的定义实际要求的极限是什么。\n\\end{exercise}\n\\begin{exercise}{417}{参数抵消与渐近线变化}\n设 $f_a(x)=(x^2+ax+1)/(x-1)$，定义域为 $\\mathbb R\\setminus\\{1\\}$。求全部渐近线随 $a$ 的变化，并确定何时 $x=1$ 为可去间断点。对非退化参数，判断曲线能否与其斜渐近线相交，证明结论。\n\\end{exercise}\n\\subsection{曲率}\n\\begin{exercise}{418…643 tokens truncated…$a>0$，判断 $\\ln(ax)$、$a^{-1}\\ln x$、$\\ln(a+x)$、$\\tfrac12(\\ln x)^2$ 中哪些仍为 $f$ 的原函数，必要时给出对 $a$ 的限制。用求导与两原函数之差两种方法核对结论。\n\\end{exercise}\n\\begin{exercise}{426}{不同表达式的原函数与端点}\n证明 $\\arcsin(2x-1)$ 与 $2\\arcsin\\sqrt x$ 在 $(0,1)$ 上为同一函数的原函数，并求两者之差。讨论两个表达式能否连续延拓至 $[0,1]$，以及能否在端点仍按通常意义作为同一函数的可导原函数。\n\\end{exercise}\n\\begin{exercise}{427}{分段原函数的拼接条件}\n设 $f(x)=3x^2+1$（$x>0$），$f(x)=2x$（$x\\le0$）。判断\n\\[F(x)=\\begin{cases}x^3+x+1,&x>0,\\\\x^2,&x\\le0\\end{cases}\\]\n是否为 $f$ 在 $\\mathbb R$ 上的原函数，分别检查连续性与导数。将两个分支各自加上任意常数后，是否可能得到全实数范围的原函数？证明结论。\n\\end{exercise}\n\\begin{exercise}{428}{原函数存在性与连续性的区别}\n设 $F'=f$ 在开区间 $I$ 上成立。判断 $f+F$ 是否必然可导、是否必然连续、是否必然存在原函数、是否必为初等函数，逐项说明依据。证明原函数存在性时，可使用连续函数必有原函数这一结论；不可把 $f$ 的连续性当作已知条件。\n\\end{exercise}\n\\begin{exercise}{429}{跳跃间断与原函数拼接}\n设 $f(x)=x^2$（$x\\ge0$）、$f(x)=\\cos x$（$x<0$），另设 $g(x)=x\\sin(1/x)$（$x\\ne0$）、$g(0)=0$。分别判断两函数在 $\\mathbb R$ 上是否存在原函数。对 $f$ 通过两侧原函数的拼接与 $0$ 处导数给出证明；对 $g$ 验证原函数存在定理所需的条件。\n\\end{exercise}\n\\begin{exercise}{430}{导函数与原函数的关系辨析}\n已知 $\\sin x$ 是 $f(x)$ 的一个原函数，求 $\\int f(x)\\,\\dd x$ 与 $f(x)$。再将条件改为 $f'(x)=\\sin x$，写出此时 $f$ 及其全部原函数，说明两种条件提供的信息有何区别。\n\\end{exercise}\n\\begin{exercise}{431}{切线斜率与初值确定曲线}\n一条可导曲线经过 $(\\mathrm e,-1)$，且在每个 $x>0$ 处的切线斜率为 $\\ln x/x$。求该曲线方程，证明初值条件使积分常数唯一。再求曲线的单调区间与最低点，以检查所得方程与斜率信息相容。\n\\end{exercise}\n\\begin{exercise}{432}{不定积分的微分与量的类型}\n设 $f$ 在 $\\mathbb R$ 上可微。分别求 $\\int f'(x)\\,\\dd x$、$\\dd(\\int f'(x)\\,\\dd x)$、$(\\int f'(x)\\,\\dd x)'$，说明三者中哪些是函数族、哪些是微分或确定函数。用 $f(x)=x^2$ 检验符号及积分常数的处理。\n\\end{exercise}\n\\begin{exercise}{433}{积分、求导与微分的逆运算}\n设 $f\\in C^1(I)$，$I$ 为开区间。判断下列等式在通常不定积分记号下是否成立，错误者改正：$\\dd(\\int f\\,\\dd x)=f$；$(\\int f\\,\\dd x)'=\\int f'\\,\\dd x$；$\\int f'\\,\\dd x=f$；$\\dd(\\int f\\,\\dd x)=f\\,\\dd x$。说明等式两侧的任意常数为何不能随意遗漏。\n\\end{exercise}\n\\begin{exercise}{434}{导数相等与原函数族相等}\n设 $f,g$ 在开区间 $I$ 可导，且 $f'=g'$。证明 $f-g$ 为常数，判断是否必有 $f=g$、$f=g+1$、$(\\int f\\,\\dd x)'=(\\int g\\,\\dd x)'$，并判断 $\\int\\dd f=\\int\\dd g$ 作为函数族是否成立。若再给出一点 $f(x_0)=g(x_0)$，哪些结论随之加强？\n\\end{exercise}\n\\begin{exercise}{435}{嵌套积分微分与常数}\n设 $f$ 在开区间可导，求 $\\int\\dd[\\int\\dd f(x)]$。逐层说明每次积分引入的常数和微分消去的常数，再判断交换两次任意常数的记号是否会改变最终函数族。\n\\end{exercise}\n\\begin{exercise}{436}{复合自变量恢复与定义范围}\n设 $f$ 在 $(0,1)$ 可导，且对 $0<t<\\pi/2$ 有 $f'(\\sin^2t)=\\cos2t+\\tan^2t$。求 $f(x)$，再由 $f(1/2)=0$ 确定常数。解题时说明代换 $x=\\sin^2t$ 在所选区间的值域，不能将 $t$ 与 $x$ 混作同一变量。\n\\end{exercise}\n\\begin{exercise}{437}{基本积分公式与定义域分支}\n求\n\\[\\int\\frac{(x^2-1)\\sqrt{1-x^2}-3x}{x\\sqrt{1-x^2}}\\,\\dd x.\\]\n先化为基本函数之和，再说明最大实定义区间，以及跨过 $x=0$ 时两侧积分常数是否必须相同。\n\\end{exercise}\n\\begin{exercise}{438}{三角恒等变形与原函数核验}\n求 $\\int\\cos2x/(\\sin^2x\\cos^2x)\\,\\dd x$，先把被积函数拆成两个基本三角函数的平方。说明答案在哪些开区间成立，并对结果求导检验拆分时的符号。\n\\end{exercise}\n\\begin{exercise}{439}{半角恒等式与奇点}\n求 $\\int(1-2\\cos x)/(1-\\cos2x)\\,\\dd x$。先写出被积函数的实定义域，再利用 $1-\\cos2x=2\\sin^2x$ 积分。检查哪些被排除的点为真正奇点，积分常数应如何按区间理解。\n\\end{exercise}\n\\begin{exercise}{440}{指数基数与代数约分}\n求 $\\int[1/(5^x\\mathrm e^x)+(1-\\mathrm e^{2x})/(1+\\mathrm e^x)]\\,\\dd x$。先说明指数乘积与分式的化简，再确定满足 $F(0)=0$ 的原函数。若将第一项的 $5$ 改为实参数 $a>0$，说明何时需要单独处理常数被积项。\n\\end{exercise}\n\\begin{exercise}{441}{基本积分与降幂公式}\n求 $\\int[6\\sqrt x+5\\mathrm e^x+\\cos^2(x/2)]\\,\\dd x$，说明余弦平方项的处理。进一步求满足 $F(0)=0$ 的连续原函数，并核验右端点处的右导数。\n\\end{exercise}\n\\begin{exercise}{442}{多项式除法与反三角积分}\n求 $\\int[x^4/(1+x^2)-2/\\sqrt{1-x^2}]\\,\\dd x$。先对有理项作多项式除法，明确共同实定义区间；再确定满足 $F(0)=1$ 的原函数。\n\\end{exercise}\n\\begin{exercise}{443}{不连通定义域上的积分常数}\n在 $\\mathbb R\\setminus\\{0\\}$ 上求 $1/x$ 的全部原函数。证明将答案统一写成 $\\ln|x|+C$ 且只允许一个常数会遗漏原函数，并判断是否存在能连续延拓至 $0$ 的原函数。\n\\end{exercise}\n\\begin{exercise}{444}{拼接处可导性的必要条件}\n设 $f_a(x)=x$（$x<0$）、$f_a(0)=a$、$f_a(x)=2x$（$x>0$）。求使 $f_a$ 在 $\\mathbb R$ 上有原函数的全部实数 $a$，并求满足 $F(0)=1$ 的原函数。分别证明条件的必要性和充分性。\n\\end{exercise}\n\\subsection{换元积分法}\n\\begin{exercise}{445}{线性与二次内函数的凑微分}\n分别求\n\\[\\int\\frac{\\dd x}{\\sqrt{2x+3}},\\qquad \\int\\frac{x+1}{x^2+2x+5}\\,\\dd x,\\qquad \\int\\frac{x}{(2x+3)^2}\\,\\dd x.\\]\n每式写出代换及实定义区间；比较第三式与第一式为何不能使用相同的幂函数积分步骤直接得到答案。\n\\end{exercise}\n\\begin{exercise}{446}{根式内函数与代换值域}\n分别求\n\\[\\int\\frac{\\mathrm e^{2\\sqrt x}}{\\sqrt x}\\,\\dd x,\\qquad \\int\\frac{\\sin\\sqrt x}{\\sqrt x}\\,\\dd x,\\qquad \\int\\frac{\\dd x}{(1+x)\\sqrt x}.\\]\n使用同一个根式代换，写出新变量范围。讨论各被积函数在 $x\\to0^+$ 时的有限性，以及所得原函数能否连续延拓至 $0$。\n\\end{exercise}\n\\begin{exercise}{447}{幂指数、参数与抽象复合换元}\n设 $n\\in\\mathbb R$，$f\\in C^1(\\mathbb R)$。求\n\\[\\int x^2\\mathrm e^{x^3}\\,\\dd x,\\quad \\int\\frac{x}{1+x^4}\\,\\dd x,\\quad \\int\\frac{x^2}{(2x^3-1)^n}\\,\\dd x,\\quad \\int xf(x^2)f'(x^2)\\,\\dd x.\\]\n第三式先限制 $2x^3-1>0$，分别处理 $n=1$ 与 $n\\ne1$；第四式说明原函数中 $f$ 应取何种幂次，并以求导验证。\n\\end{exercise}\n\\begin{exercise}{448}{三角积分的幂次与降幂选择}\n求下列四个不定积分，并分别注明采用的恒等变形或代换：\n\\[\\int\\sin^2x\\cos^2x\\,\\dd x,\\quad \\int\\sin^5x\\cos^2x\\,\\dd x,\\quad \\int\\cot^3x\\csc x\\,\\dd x,\\quad \\int\\sin5x\\sin3x\\,\\dd x.\\]\n对第三式说明为何需要分开理解跨越 $k\\pi$ 的积分常数；其余各式给出可在全实数范围成立的原函数。\n\\end{exercise}\n\\begin{exercise}{449}{平方和与平方差的参数积分}\n对实数 $a\\ne0$，求 $\\int\\dd x/(a^2+x^2)$ 与 $\\int\\dd x/(a^2-x^2)$，答案须对 $a<0$ 仍成立。说明两式的实定义区间和绝对值的必要性；再单独处理 $a=0$，判断能否直接把它代入非零参数公式。\n\\end{exercise}\n\\begin{exercise}{450}{复合指数函数的链式识别}\n求 $\\int\\mathrm e^{\\tan x}\\sec^2x\\,\\dd x$ 与 $\\int(1-x^{-2})\\mathrm e^{x+1/x}\\,\\dd x$。逐式写出内函数及其导数，注明答案成立的区间，并说明第二式中不能跨越 $x=0$ 统一使用一个积分常数的原因。\n\\end{exercise}\n\\begin{exercise}{451}{多层对数代换与实定义域}\n分别求\n\\[\\int\\frac{\\dd x}{x\\sqrt{1-\\ln^2x}},\\quad \\int\\frac{\\dd x}{x\\ln x[1+\\ln(\\ln x)]^2},\\quad \\int\\frac{1+\\ln x}{1+x^2\\ln^2x}\\,\\dd x.\\]\n写出每层代换，并逐式给出实定义域，特别检查第二式中的对数与分母条件。\n\\end{exercise}\n\\begin{exercise}{452}{反三角内函数与链式系数}\n分别求\n\\[\\int\\frac{\\dd x}{\\sqrt{1-x^2}(\\arcsin x)^2},\\quad \\int\\frac{\\arcsin\\sqrt x}{\\sqrt{x(1-x)}}\\,\\dd x,\\quad \\int\\frac{\\arcsin(1-x)}{\\sqrt{2x-x^2}}\\,\\dd x.\\]\n对每式注明实定义区间；通过求导核验第二式中的系数与第三式中的负号。\n\\end{exercise}\n\\begin{exercise}{453}{配方与两个原函数的常数差}\n求 $\\int\\dd x/\\sqrt{x-x^2}$，分别使用配方三角代换和 $x=\\sin^2t$、$0<t<\\pi/2$。说明两种所得表达式在哪一开区间为同一被积函数的原函数，并求两表达式之间的常数差。\n\\end{exercise}\n\\begin{exercise}{454}{有界内函数与反正切原函数}\n求 $\\int\\cos x/(9+\\sin^2x)\\,\\dd x$，并确定满足 $F(0)=0$ 的原函数。说明代换 $u=\\sin x$ 在全实数轴不单调，为何仍可通过求导确认所得表达式在全实数轴成立。\n\\end{exercise}\n\\begin{exercise}{455}{根式分母的拆分代换}\n求 $\\int(1-x)/\\sqrt{9-4x^2}\\,\\dd x$，分别处理常数分子项与一次分子项。明确实定义区间，求满足 $F(0)=0$ 的原函数，并核验两个部分的系数。\n\\end{exercise}\n\\begin{exercise}{456}{三角根式内函数与连通区间}\n求 $\\int(\\sin x+\\cos x)/\\sqrt[3]{\\sin x-\\cos x}\\,\\dd x$，立方根按实数定义。给出被积函数全部实定义区间，并证明原函数在各区间可连续延拓至端点。比较分母改为平方根时实定义域的变化，说明不能给立方根附加非负真数条件。\n\\end{exercise}\n\\begin{exercise}{457}{根式三角复合与负号}\n求 $\\int x\\tan(\\sqrt{1-x^2})/\\sqrt{1-x^2}\\,\\dd x$。写出代换变量的范围并检验正切是否在此范围产生额外奇点，再讨论被积函数在 $x=\\pm1$ 的极限及可补值性。\n\\end{exercise}\n\\begin{exercise}{458}{对数根式的复合积分}\n求\n\\[\\int\\sqrt{\\frac{\\ln(x+\\sqrt{1+x^2})+1}{1+x^2}}\\,\\dd x.\\]\n说明对数真数在全实数范围恒为正，再由外层根式确定实定义范围。选择对数整体作新变量，完成积分并确定满足 $F(0)=0$ 的原函数；说明为何不能忽略根式对定义域的额外限制。\n\\end{exercise}\n\\begin{exercise}{459}{指数根式代换与补值}\n求 $\\int\\mathrm e^{\\sqrt{1+\\sin x}}\\cos x/\\sqrt{1+\\sin x}\\,\\dd x$。在 $1+\\sin x>0$ 的各开区间给出原函数，再讨论被排除点处原函数能否连续、可导延拓，说明根式中零点对链式求导的影响。\n\\end{exercise}\n\\begin{exercise}{460}{拆项与反正切复合}\n求 $\\int[x+(\\arctan x)^2]/(1+x^2)\\,\\dd x$，说明为何应先拆分再分别代换。确定满足 $F(0)=1$ 的原函数，并用求导检验平方项积分后应出现的幂次与系数。\n\\end{exercise}\n\\begin{exercise}{461}{三角幂与有理化}\n求 $\\int\\sin x\\cos^3x/(1+\\cos^2x)\\,\\dd x$，选取代换把它化为有理函数积分。再给出所得原函数的最小正周期，并说明原函数的周期性为何需要实际检查，不能仅由被积函数周期性推出。\n\\end{exercise}\n\\begin{exercise}{462}{正切代换的分支与全局原函数}\n求 $\\int\\dd x/(\\sin^2x+2\\cos^2x)$，先在 $(-\\pi/2,\\pi/2)$ 使用正切代换。讨论直接使用反正切主值表达式为何在 $\\pi/2$ 附近需要调整常数，并说明如何拼接得到全实数范围的一个原函数。\n\\end{exercise}\n\\begin{exercise}{463}{指数代换与两种等价表达式}\n求 $\\int\\dd x/(1+\\mathrm e^x)$，分别用 $u=\\mathrm e^x$ 和 $v=\\mathrm e^{-x}$ 代换。证明两种所得原函数只相差常数，并求满足 $F(0)=0$ 的表达式。\n\\end{exercise}\n\\begin{exercise}{464}{对数差的整体代换}\n求 $\\int[\\ln(x+1)-\\ln x]/[x(x+1)]\\,\\dd x$。先确定实定义域，计算对数差的导数后整体代换。讨论若改成 $\\ln|x+1|-\\ln|x|$，原函数公式可延伸到哪些额外区间。\n\\end{exercise}\n\\begin{exercise}{465}{对数代换后的多项式拆分}\n求 $\\int\\ln^2x/[x(1+\\ln^2x)]\\,\\dd x$，把代换后的有理函数先拆分再积分。求满足 $F(1)=0$ 的原函数，并证明它在 $(0,+\\infty)$ 单调递增，须处理导数为零的点。\n\\end{exercise}\n\\begin{exercise}{466}{共轭有理化与根式分支}\n求 $\\int x/(x-\\sqrt{x^2-1})\\,\\dd x$。先确定实定义域，使用共轭因子化简，分别说明在 $x>1$ 与 $x<-1$ 上计算所得原函数时哪些符号与对数绝对值必须保留。\n\\end{exercise}\n\\begin{exercise}{467}{指数复合与二倍角恒等式}\n求 $\\int\\mathrm e^{\\sin2x}\\sin^2x/\\mathrm e^{2x}\\,\\dd x$。先合并指数，再利用二倍角恒等式将其导数与剩余因子联系，给出在全实数范围成立的原函数，并说明关键系数的来源。\n\\end{exercise}\n\\begin{exercise}{468}{对数正切的整体代换}\n在 $0<x<\\pi/2$ 上求 $\\int\\ln(\\tan x)/\\sin2x\\,\\dd x$。证明 $\\ln\\tan x$ 在该区间严格递增且值域为 $\\mathbb R$，用它作新变量积分，并确定满足 $F(\\pi/4)=0$ 的原函数，须核对二倍角产生的系数。\n\\end{exercise}\n\\begin{exercise}{469}{商函数求导的逆向识别}\n求 $\\int[x+\\sin x\\cos x]/(\\cos x-x\\sin x)^2\\,\\dd x$。通过对 $\\sin x/(\\cos x-x\\sin x)$ 求导寻找原函数，并说明答案应限制在哪些开区间；不要求显式求出所有分母零点。\n\\end{exercise}\n\\begin{exercise}{470}{三角指数乘积的有理结构}\n求 $\\int(\\cos^2x-\\sin x)/\\{\\cos x[1+\\mathrm e^{\\sin x}\\cos x]\\}\\,\\dd x$。以 $u=\\mathrm e^{\\sin x}\\cos x$ 作整体代换，把积分化为有理函数形式；说明各分母非零条件与对数绝对值的作用，不要求显式求解全部奇点。\n\\end{exercise}\n\\begin{exercise}{471}{半角组合与指数乘积导数}\n求 $\\int(1+\\sin x)\\mathrm e^x/(1+\\cos x)\\,\\dd x$。用半角恒等式将被积函数写成 $\\mathrm e^x$ 与正切半角函数的乘积导数，给出最大实定义区间，并核验原函数在每个区间成立。\n\\end{exercise}\n\\begin{exercise}{472}{已知原函数后的复合换元}\n在 $0<u<\\pi$ 已知 $\\int f(u)\\,\\dd u=\\ln(\\sin u)+C$。求 $\\int xf(1-x^2)\\,\\dd x$，给出由 $0<1-x^2<\\pi$ 确定的实定义区间。解释为何先由已知条件恢复 $f$ 或直接使用原函数换元可得到一致结果。\n\\end{exercise}\n\\begin{exercise}{473}{含抽象函数的商法则逆运算}\n设 $f\\in C^1(I)$，$0\\notin I$。证明\n\\[\\int\\frac{xf'(x)-(1+x)f(x)}{x^2\\mathrm e^x}\\,\\dd x=\\frac{f(x)}x\\mathrm e^{-x}+C.\\]\n明确使用的乘积与商法则，并用 $f(x)=x\\mathrm e^x$ 检查两侧。若 $I$ 跨过 $0$，说明公式的适用区间必须如何调整。\n\\end{exercise}\n\\begin{exercise}{474}{偶次余项与根式代换}\n求 $\\int x^3\\sqrt{4-x^2}\\,\\dd x$，使用 $u=4-x^2$ 后先将剩余 $x^2$ 消去。给出实积分区间，并确定满足 $F(0)=0$ 的原函数；说明代换在 $0$ 两侧不单调为何不妨碍最终求导核验。\n\\end{exercise}\n\\begin{exercise}{475}{平方和根式与双曲型对数}\n求 $\\int x^2/(1+x^2)^{3/2}\\,\\dd x$。分别用三角代换与拆成 $1/\\sqrt{1+x^2}-1/(1+x^2)^{3/2}$ 的方法，证明所得答案相差常数；确定满足 $F(0)=0$ 的原函数。\n\\end{exercise}\n\\begin{exercise}{476}{平方差根式与参数绝对值}\n设 $a>0$，求 $\\int x^2/(x^2-a^2)^{3/2}\\,\\dd x$。在 $x>a$ 上使用三角代换，并给出在 $x<-a$ 上也成立的带绝对值表达式，明确两侧常数可独立选择。\n\\end{exercise}\n\\begin{exercise}{477}{根式有理化与变量范围}\n求 $\\int\\dd x/[1+\\sqrt[3]{x+1}]$，立方根按实数定义，采用 $t=\\sqrt[3]{x+1}$ 并写出 $\\dd x$。给出全部最大实定义区间，再检查所得原函数在 $x=-1$ 处是否可导，说明代换的逆函数导数在该点不存在是否妨碍最终答案成立。\n\\end{exercise}\n\\begin{exercise}{478}{不同根指数的统一有理化}\n求 $\\int\\dd x/(\\sqrt x+\\sqrt[3]{x^2})$。先确定实定义区间，再根据两个根指数的最小公倍数选取代换，写出有理化后的完整积分。比较分别只代换平方根或立方根时仍会留下的根式，并检查最终结果的导数。\n\\end{exercise}\n\\begin{exercise}{479}{根式分式的有理代换}\n求 $\\int(3-x)^{-1}\\sqrt{(5-x)/(x-1)}\\,\\dd x$。用根式本身作新变量，写出反解关系及新变量范围；给出被积函数的各个实定义区间，说明 $x=3$ 对积分常数的影响。\n\\end{exercise}\n\\begin{exercise}{480}{指数代换后的部分分式}\n求 $\\int\\dd x/(\\mathrm e^x+\\mathrm e^{2x})$，将它化为新变量的有理函数积分。确定满足 $F(0)=0$ 的原函数，并由被积函数符号判断其单调性。\n\\end{exercise}\n\\begin{exercise}{481}{指数加常数的根式代换}\n求 $\\int\\dd x/\\sqrt{\\mathrm e^x+1}$，令 $t=\\sqrt{\\mathrm e^x+1}$ 后写出完整有理积分。给出新变量范围和实对数表达式，并说明为何不能把 $\\dd x$ 误写为 $2t\\dd t$。\n\\end{exercise}\n\\begin{exercise}{482}{幂代换与不连通区间}\n求 $\\int\\dd x/[x(x^6+1)]$。分别使用 $t=x^6$ 与先拆成 $1/x-x^5/(x^6+1)$ 的方法，比较所得表达式。解释 $x>0$、$x<0$ 两个区间中 $\\ln|x|$ 和积分常数的处理。\n\\end{exercise}\n\\begin{exercise}{483}{倒代换与根式绝对值}\n求 $\\int\\dd x/[x^4\\sqrt{x^2+1}]$。尝试 $t=1/x$，明确 $\\sqrt{x^2+1}$ 变换后出现的绝对值，分别在正负半轴积分；最终给出可在两个半轴分别使用的表达式并求导核验。\n\\end{exercise}\n\\begin{exercise}{484}{对数与代数的混合内函数}\n求 $\\int(1+x)/(x^2+x\\ln x)\\,\\dd x$。选择 $u=x+\\ln x$ 化简，证明分母在正半轴只有一个零点，从而说明答案成立的最大开区间，不要求写出该零点的初等表达式。\n\\end{exercise}\n\\begin{exercise}{485}{配方、三角代换与半圆结构}\n求 $\\int\\sqrt{2x-x^2}\\,\\dd x$，先配方并给出实定义范围。确定满足 $F(1)=0$ 的原函数，并利用被积函数关于 $x=1$ 的对称性检验所得原函数的奇对称关系。\n\\end{exercise}\n\\begin{exercise}{486}{指数根式与两步代换}\n求 $\\int\\dd x/\\sqrt{1+\\mathrm e^{2x}}$，先作指数代换，再选用根式或三角代换。写出对数形式的实数原函数，说明所有对数真数在全实数范围的符号并求导核验。\n\\end{exercise}\n\\begin{exercise}{487}{三角代换后的有理积分}\n求 $\\int\\dd x/[(1+x^2)\\sqrt{1-x^2}]$。在 $(-1,1)$ 作 $x=\\sin t$，再使用正切代换完成积分。明确两次代换的变量范围，避免反函数分支导致常数跳跃。\n\\end{exercise}\n\\begin{exercise}{488}{参数退化与复合换元}\n对 $a\\in\\mathbb R$ 求 $\\int x/(1+ax^2)\\,\\dd x$，完整处理 $a=0$。在包含 $0$ 的最大实定义区间上选取 $F_a(0)=0$ 的原函数，并求 $a\\to0$ 时 $F_a(x)$ 的点态极限，检验参数退化的一致性。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:17:34Z




## tool · 2026-10-20T03:17:40Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"5f576e","wall_time_seconds":0.000007667,"exit_code":0,"original_token_count":640,"output":"\\begin{exercise}{416}{渐近线可被穿越}\n设 $f(x)=x+\\sin x/x$，$x\\ne0$。求它的全部渐近线，并判断 $0$ 处的间断类型。求与斜渐近线的全部交点，证明在任意充分大的正半轴尾部仍存在交点，说明渐近线的定义实际要求的极限是什么。\n\\end{exercise}\n\\begin{exercise}{417}{参数抵消与渐近线变化}\n设 $f_a(x)=(x^2+ax+1)/(x-1)$，定义域为 $\\mathbb R\\setminus\\{1\\}$。求全部渐近线随 $a$ 的变化，并确定何时 $x=1$ 为可去间断点。对非退化参数，判断曲线能否与其斜渐近线相交，证明结论。\n\\end{exercise}\n\\subsection{曲率}\n\\begin{exercise}{418}{显式与参数表示的曲率一致性}\n求曲线 $xy=1$ 在 $(1,1)$ 处的曲率与曲率半径，分别用显式表示 $y=1/x$ 和参数表示 $(x,y)=(\\mathrm e^t,\\mathrm e^{-t})$ 验证。说明曲率为何与参数行进的快慢无关。\n\\end{exercise}\n\\begin{exercise}{419}{星形线的正则参数与曲率半径}\n设 $a>0$，曲线为 $x=a\\cos^3t$、$y=a\\sin^3t$。求满足 $\\sin t_0\\cos t_0\\ne0$ 的点处的曲率和曲率半径，确定第一象限弧上曲率的最小值。讨论 $t_0=k\\pi/2$ 时通常的正则参数曲率公式为何不能直接使用，并求沿相邻弧趋近时的曲率极限。\n\\end{exercise}\n\\begin{exercise}{420}{法向方向与曲率圆}\n求抛物线 $y=2x^2-3x+3$ 在 $M(1,2)$ 处的曲率、曲率中心与曲率圆方程。证明圆心位于该点的法线上，并核验该圆经过 $M$；说明仅知道曲率半径为何还不能确定圆心的位置。\n\\end{exercise}\n\\begin{exercise}{421}{弧长变量的链式求导}\n设 $\\rho(x)$ 是抛物线 $y=\\sqrt x$ 在 $M(x,\\sqrt x)$、$x\\ge1$ 处的曲率半径，$s(x)$ 是从 $A(1,1)$ 到 $M$ 沿曲线的弧长。求 $\\rho(x)$、$\\dd s/\\dd x$，再计算 $3\\rho\\,\\dd^2\\rho/\\dd s^2-(\\dd\\rho/\\dd s)^2$。明确二阶弧长导数的链式法则，不能把它直接替换为关于 $x$ 的二阶导数。\n\\end{exercise}\n\\begin{exercise}{422}{抛物线最大曲率与长度缩放}\n设 $a>0$，曲线为 $y=ax^2$。求曲率函数、最大曲率及对应点，写出该点的曲率圆。若把曲线上所有坐标同时放大 $\\lambda>0$ 倍，证明对应点的曲率变为原来的 $1/\\lambda$，并解释量纲关系。\n\\end{exercise}\n\\begin{exercise}{423}{椭圆曲率的极值}\n设 $a>b>0$，椭圆由 $x=a\\cos t$、$y=b\\sin t$ 表示。求曲率函数及其最大、最小值，给出对应点和曲率半径。再讨论 $a=b$ 时结论的变化，并将结果与圆的几何曲率核对。\n\\end{exercise}\n"}
{"chunk_id":"4abc0f","wall_time_seconds":0.000006333,"exit_code":0,"original_token_count":270,"output":"\\section{第4章 不定积分}\n\\subsection{不定积分的概念与性质}\n\\begin{exercise}{424}{原函数关系与二阶求导}\n设 $f$ 在 $(1,+\\infty)$ 上的一个原函数为 $F(x)=\\ln(x+\\sqrt{x^2-1})$。求 $f(x)$ 和 $f'(x)$，说明两次求导所用的定义域条件。若把原函数改为 $F(x)+C$，说明所求两个函数是否改变。\n\\end{exercise}\n\\begin{exercise}{425}{原函数族与参数退化}\n已知 $\\ln x$ 是 $f$ 在 $(0,+\\infty)$ 上的一个原函数。对 $a>0$，判断 $\\ln(ax)$、$a^{-1}\\ln x$、$\\ln(a+x)$、$\\tfrac12(\\ln x)^2$ 中哪些仍为 $f$ 的原函数，必要时给出对 $a$ 的限制。用求导与两原函数之差两种方法核对结论。\n\\end{exercise}\n\\begin{exercise}{426}{不同表达式的原函数与端点}\n证明 $\\arcsin(2x-1)$ 与 $2\\arcsin\\sqrt x$ 在 $(0,1)$ 上为同一函数的原函数，并求两者之差。讨论两个表达式能否连续延拓至 $[0,1]$，以及能否在端点仍按通常意义作为同一函数的可导原函数。\n\\end{exercise}\n\\begin{exercise}{427}{分段原函数的拼接条件}\n"}
{"chunk_id":"23efe1","wall_time_seconds":0.000007458,"exit_code":0,"original_token_count":4929,"output":"\\begin{exercise}{489}{反三角主值与分支常数}\n在 $(-1,1)$ 上求 $\\int\\dd x/\\sqrt{1-x^2}$。若代换 $x=\\sin t$ 分别取 $t\\in(-\\pi/2,\\pi/2)$ 与 $t\\in(\\pi/2,3\\pi/2)$，写出两种计算过程，并说明 $\\sqrt{\\cos^2t}=|\\cos t|$ 与反函数分支如何共同保证所得函数只相差常数。\n\\end{exercise}\n\\subsection{分部积分法}\n\\begin{exercise}{490}{多项式与指数三角函数的分部积分}\n求 $\\int x\\mathrm e^{ax}\\,\\dd x$、$\\int x^2\\cos x\\,\\dd x$、$\\int(x^2-x)\\sin x\\,\\dd x$，其中 $a\\in\\mathbb R$。第一式须单独处理 $a=0$，其余两式明确每次分部积分中次数降低的部分，并通过求导核验符号。\n\\end{exercise}\n\\begin{exercise}{491}{反函数与对数函数的分部选择}\n求 $\\int x/\\sin^2x\\,\\dd x$、$\\int\\ln(x+\\sqrt{x^2+1})\\,\\dd x$、$\\int\\arctan x\\,\\dd x$。写出每式分部积分中 $u,\\dd v$ 的选择，说明第一式的定义区间与第二式对数真数的符号。\n\\end{exercise}\n\\begin{exercise}{492}{循环积分、恒等式与抽象函数}\n求 $\\int\\mathrm e^{-x}\\cos x\\,\\dd x$ 与 $\\int x\\cot^2x\\,\\dd x$。另设 $\\int f(x)\\,\\dd x=(1+\\sin x)\\ln x+C$（$x>0$），求 $\\int xf'(x)\\,\\dd x$；说明第三式为何可利用已知原函数而不必完整展开 $f'$。\n\\end{exercise}\n\\begin{exercise}{493}{对数移位与多项式分部}\n求 $\\int x\\ln(x+1)\\,\\dd x$，给出实定义区间。分别采用直接分部积分与先令 $u=x+1$ 的方法，验证两种答案之差为常数，再确定满足 $F(0)=0$ 的原函数。\n\\end{exercise}\n\\begin{exercise}{494}{平移反正弦与根式符号}\n求 $\\int\\arcsin(x+1)\\,\\dd x$，明确可导原函数的开区间。将答案连续延拓至实定义域端点，求两个端点的单侧导数，说明被积函数在端点有限与自身导数无界的区别。\n\\end{exercise}\n\\begin{exercise}{495}{凑微分与分部积分的配合}\n求 $\\int x\\cot x/\\sin^2x\\,\\dd x$，先把 $\\cot x/\\sin^2x$ 识别为一个基本函数的导数，再进行分部积分。注明积分成立的区间，并解释只作 $u=\\cot x$ 代换为何仍会留下需要处理的 $x$。\n\\end{exercise}\n\\begin{exercise}{496}{半角恒等式后的分部积分}\n求 $\\int x\\cos^4(x/2)/\\sin^3x\\,\\dd x$。先用半角公式化简三角因子，再选择分部积分；明确原被积函数的定义域，并检查化简是否在原来无定义的点造成表面约分。\n\\end{exercise}\n\\begin{exercise}{497}{对数三角函数与分部积分}\n在 $0<x<\\pi$ 上求 $\\int\\ln(\\sin x)/\\sin^2x\\,\\dd x$。通过分部积分把剩余项化为基本三角积分，并用求导检验。说明若要延伸到 $\\sin x<0$ 的区间，题面中的对数必须作何调整。\n\\end{exercise}\n\\begin{exercise}{498}{根式积分的两种路线}\n求 $\\int x^3/\\sqrt{1+x^2}\\,\\dd x$，分别用整体根式代换与取 $u=x^2$、$\\dd v=x\\dd x/\\sqrt{1+x^2}$ 的分部积分法。证明两种结果等价，并说明本题中哪一步使剩余积分的次数降低。\n\\end{exercise}\n\\begin{exercise}{499}{指数三角循环积分}\n用两次分部积分求 $\\int\\mathrm e^{2x}\\sin3x\\,\\dd x$。进一步推导实参数 $a,b$ 满足 $a^2+b^2>0$ 时 $\\int\\mathrm e^{ax}\\sin bx\\,\\dd x$ 的公式，并检查 $b=0$ 与 $a=0$ 的退化情形。\n\\end{exercise}\n\\begin{exercise}{500}{平方和根式与参数退化}\n设 $a>0$，用分部积分求 $\\int\\sqrt{x^2+a^2}\\,\\dd x$，将出现的同类积分移项求解，说明对数真数的正性。再单独求 $a=0$ 时的 $\\int|x|\\,\\dd x$，并讨论两个半轴上的表达式如何拼接。\n\\end{exercise}\n\\begin{exercise}{501}{平方差根式与区间约束}\n设 $a>0$，求 $\\int\\sqrt{a^2-x^2}\\,\\dd x$，分别用三角代换与分部积分核验。明确实定义域和反正弦的主值范围，再确定满足 $F(0)=0$ 的原函数及其奇偶性。\n\\end{exercise}\n\\begin{exercise}{502}{反正弦与剩余根式积分}\n求 $\\int x\\arcsin x\\,\\dd x$，明确分部积分后的根式积分如何继续化简。选取满足 $F(0)=0$ 的原函数，检验它的奇偶性，并求两端连续延拓值。\n\\end{exercise}\n\\begin{exercise}{503}{反正切乘负幂与对数绝对值}\n求 $\\int x^{-2}\\arctan x\\,\\dd x$，说明 $\\int\\dd x/[x(1+x^2)]$ 的分解。分别给出正负半轴上的原函数族，并讨论被积函数在 $x\\to0$ 的主项是否允许原函数有限连续延拓。\n\\end{exercise}\n\\begin{exercise}{504}{对数分部与内部极点}\n求 $\\int\\ln(1+x)/(2-x)^2\\,\\dd x$。先给出最大实定义区间，再作分部积分并处理所得有理积分。明确 $\\ln(1+x)$ 与 $\\ln|2-x|$ 的适用条件，说明 $x=2$ 两侧的常数为何独立。\n\\end{exercise}\n\\begin{exercise}{505}{指数根式的分部与有理化}\n在 $x>0$ 上求 $\\int x\\mathrm e^x/\\sqrt{\\mathrm e^x-1}\\,\\dd x$。先把指数根式凑为一个微分，再对剩余根式积分换元。确定能连续延拓至 $0$ 且取值为 $0$ 的原函数，并检查右导数。\n\\end{exercise}\n\\begin{exercise}{506}{对数与根式的双重处理}\n求 $\\int\\ln x/\\sqrt{1+x}\\,\\dd x$（$x>0$），用分部积分后作 $t=\\sqrt{1+x}$。说明对数中 $t-1$ 的符号，并讨论所求原函数在 $x\\to0^+$ 时是否具有有限极限。\n\\end{exercise}\n\\begin{exercise}{507}{反正切根式与端点补值}\n求 $\\int\\arctan\\sqrt x\\,\\dd x$，给出在 $x>0$ 上的计算过程。选择满足 $F(0)=0$ 的连续延拓，核验其在 $0$ 的右导数与被积函数在该点的值相等。\n\\end{exercise}\n\\begin{exercise}{508}{有理指数乘积的导数识别}\n求 $\\int x^2\\mathrm e^x/(x+2)^2\\,\\dd x$。把被积函数写成 $\\mathrm e^x$ 与一个有理函数的导数结构，可设原函数为 $\\mathrm e^x(A+B/(x+2))$ 求系数。注明定义区间，并用求导检查该设定确实覆盖本题。\n\\end{exercise}\n\\begin{exercise}{509}{三角有理组合与逆向求导}\n求 $\\int[(1+x)\\sin x+\\cos x]/(1+x)^2\\,\\dd x$。分别用分部积分的消项与识别商函数导数的方法，说明两条路线的等价性，并明确 $x=-1$ 两侧的积分常数。\n\\end{exercise}\n\\begin{exercise}{510}{复合导函数恢复与分部积分}\n设 $f'(\\mathrm e^t)=\\cos t$ 对所有实数 $t$ 成立。求 $f(x)$ 的全部表达式，并由 $f(1)=0$ 确定常数。解题时先写出 $f'$ 的定义区间，再处理含 $\\cos\\ln x$ 的积分。\n\\end{exercise}\n\\begin{exercise}{511}{正割幂的递推与初值}\n在不含 $\\cos x=0$ 的开区间上，令 $I_n=\\int\\sec^nx\\,\\dd x$。对整数 $n\\ge2$ 证明\n\\[I_n=\\frac{\\sin x}{(n-1)\\cos^{n-1}x}+\\frac{n-2}{n-1}I_{n-2},\\]\n其中等式按相差任意常数理解。求 $I_0,I_1$ 并用递推式求 $I_3,I_4$，说明递推为何需要两个初始积分。\n\\end{exercise}\n\\begin{exercise}{512}{参数分部积分与零参数极限}\n对实参数 $a$ 求 $\\int x\\mathrm e^{ax}\\,\\dd x$，选取满足 $F_a(0)=0$ 的原函数。单独处理 $a=0$，并用泰勒公式证明非零参数表达式在 $a\\to0$ 时趋于该结果，解释积分常数选择对极限的影响。\n\\end{exercise}\n\\begin{exercise}{513}{对数幂积分的递推}\n设 $n$ 为非负整数，$J_n=\\int(\\ln x)^n\\,\\dd x$（$x>0$）。建立 $J_n$ 与 $J_{n-1}$ 的递推关系，并求 $J_3$。证明所得表达式可取有限的 $x\\to0^+$ 极限，不能仅以每个对数项都无界判断原函数发散。\n\\end{exercise}\n\\subsection{有理函数的积分}\n\\begin{exercise}{514}{假分式除法与余式积分}\n求 $\\int x^3/(x^2+1)\\,\\dd x$，先写出多项式除法的商与余式。确定满足 $F(0)=0$ 的原函数，再用奇偶性检验该原函数的对称性。\n\\end{exercise}\n\\begin{exercise}{515}{不同一次因子的部分分式}\n求 $\\int(3x-2)/(x^2+3x-4)\\,\\dd x$，写出分母分解和部分分式系数。给出所有最大实定义区间，说明所得对数的绝对值及各区间常数的含义。\n\\end{exercise}\n\\begin{exercise}{516}{三不同实根分母的积分}\n求 $\\int(2x^2-x+1)/[(x+1)(x-3)(x+2)]\\,\\dd x$。用赋值法或待定系数法完整确定三个一次分式系数，再以通分核验分子恒等式，明确原函数的各个定义区间。\n\\end{exercise}\n\\begin{exercise}{517}{简单极点与原函数族}\n求 $\\int\\dd x/[x(x-1)]$。在三个最大定义区间上分别描述全部原函数，判断是否能找到可连续延拓至 $0$ 或 $1$ 的原函数，并由对数主项说明理由。\n\\end{exercise}\n\\begin{exercise}{518}{重一次因子的完整分解}\n求 $\\int(x^2+1)/[(x+1)(x^2-1)]\\,\\dd x$。先按重根结构列全部分分式，说明若只保留 $1/(x+1)$ 与 $1/(x-1)$ 两项为何不足，再求系数并积分。\n\\end{exercise}\n\\begin{exercise}{519}{不可约二次因子的分子形式}\n求 $\\int\\dd x/[(x^2+1)(1+2x)]$。写出包含二次因子对应一次分子的完整分解，积分后同时保留对数与反正切项。说明若把该一次分子擅自设为常数，会遗漏什么约束。\n\\end{exercise}\n\\begin{exercise}{520}{配方与分子拆成导数}\n求 $\\int(3x+1)/(x^2+2x+5)\\,\\dd x$，把分子拆成分母导数的倍数与常数。证明分母对所有实数非零，并确定满足 $F(-1)=0$ 的原函数。\n\\end{exercise}\n\\begin{exercise}{521}{重二次分母与标准积分}\n求 $\\int\\dd x/(x^2+2x+5)^2$，先配方再使用三角代换或分部积分。写出有理项和反正切项，最后对整个表达式求导核验平方分母的系数。\n\\end{exercise}\n\\begin{exercise}{522}{四次分母分解与对称分子}\n求 $\\int(2x^3+2x^2+5x+5)/(x^4+5x^2+4)\\,\\dd x$。先分解分母，再利用分子的结构减少待定系数数量；说明为何答案可在全实数轴使用同一个积分常数。\n\\end{exercise}\n\\begin{exercise}{523}{配方后重二次因子的积分}\n求 $\\int x^2/(x^2+2x+2)^2\\,\\dd x$。先作平移代换，把分子拆成适合积分的三项，并给出完整原函数。通过检查大 $|x|$ 时被积函数的衰减阶，判断所求原函数在两端是否具有有限极限。\n\\end{exercise}\n\\begin{exercise}{524}{高次有理函数的实因式分解}\n求 $\\int(x^4+1)/(1+x^6)\\,\\dd x$。利用 $1+x^6=(x^2+1)(x^4-x^2+1)$，将四次因子进一步分解为两个实不可约二次因子，再作部分分式积分。注明实定义区间，并利用被积函数的偶性检查可取为奇函数的原函数。\n\\end{exercise}\n\\begin{exercise}{525}{高重零点与偶函数分解}\n求 $\\int\\dd x/(x^4-x^6)$。先利用偶性寻找仅含 $1/x^2$、$1/x^4$ 与 $1/(1-x^2)$ 的分解，再积分。列出全部被排除点，说明不能将 $x=0$ 当作普通的简单极点处理。\n\\end{exercise}\n\\begin{exercise}{526}{倒幂代换与重因子结构}\n求 $\\int(1+2x^4)/[x^3(1+x^4)^2]\\,\\dd x$。先作 $t=1/x^2$ 以降低次数，再积分得到实原函数，分别说明正负半轴上的适用性，并通过求导核验重因子对应的有理项。\n\\end{exercise}\n\\begin{exercise}{527}{四次平方和的实分解}\n求 $\\int\\dd x/(x^4+1)$，将分母分解为两个实不可约二次因子后积分。给出在 $0$ 附近连续且取值为 $0$ 的表达式，并讨论合并两个反正切为一个主值反正切时可能需要补加的常数。\n\\end{exercise}\n\\begin{exercise}{528}{原函数存在性与奇偶性}\n逐项判断并证明或举例：初等函数在其连续的定义区间内存在原函数；不连续函数也可能存在原函数；奇函数在关于 $0$ 对称的开区间上的原函数都是偶函数；偶函数在这样的区间上的原函数都是奇函数。对最后一项给出使之成立的积分常数条件，并说明“存在原函数”与“有初等原函数”有何区别。\n\\end{exercise}\n\\begin{exercise}{529}{闭区间连续性保证的结论}\n设 $f\\in C[a,b]$，$a<b$。判断 $f$ 在 $(a,b)$ 内是否必有导函数、原函数、最大值或最小值、局部极值。对必然成立者说明定理依据；对其余结论给出具体反例，注意闭区间最值定理的取值范围。\n\\end{exercise}\n\\begin{exercise}{530}{分段函数原函数的参数拼接}\n设 $f(x)=2(x-1)$（$x<1$）、$f(x)=\\ln x$（$x\\ge1$）。求实数 $a,b$ 使\n\\[F_{a,b}(x)=\\begin{cases}(x-1)^2,&x<1,\\\\x(\\ln x+a)+b,&x\\ge1\\end{cases}\\]\n为 $f$ 在 $\\mathbb R$ 上的原函数。必须分别检查拼接处连续、左右导数及非拼接处导数，不能仅由两侧分别可积确定结论。\n\\end{exercise}\n\\begin{exercise}{531}{反正切指数函数的分部积分}\n求 $\\int\\mathrm e^{-2x}\\arctan(\\mathrm e^x)\\,\\dd x$。先作指数代换，再通过分部积分处理反正切项，明确新变量恒正对对数绝对值的影响。\n\\end{exercise}\n\\begin{exercise}{532}{反正切与有理因子的配合}\n求 $\\int\\arctan x/[x^2(1+x^2)]\\,\\dd x$。先分解 $1/[x^2(1+x^2)]$，再分别采用分部与整体代换；写出在两个半轴上的原函数族，并讨论 $0$ 处是否可连续延拓。\n\\end{exercise}\n\\begin{exercise}{533}{指数有理混合的对数导数}\n求 $\\int(1+x)/[x(1+x\\mathrm e^x)]\\,\\dd x$，尝试将被积函数写成两个对数导数之差。证明 $1+x\\mathrm e^x$ 在全实数范围恒正，从而给出答案的全部最大实定义区间。\n\\end{exercise}\n\\begin{exercise}{534}{对数商函数的逆向求导}\n求 $\\int(1-\\ln x)/(x-\\ln x)^2\\,\\dd x$。尝试对 $x/(x-\\ln x)$ 求导识别原函数，并用最值证明分母在正半轴不为零，确定全实定义区间。\n\\end{exercise}\n\\begin{exercise}{535}{指数根式与反正切分部积分}\n在 $x>0$ 上求 $\\int\\mathrm e^{2x}\\arctan\\sqrt{\\mathrm e^x-1}\\,\\dd x$。先令 $t=\\sqrt{\\mathrm e^x-1}$ 化为多项式乘反正切的积分，再作分部积分。明确代换后 $\\mathrm e^{2x}\\dd x$ 的表达，避免遗漏雅可比因子。\n\\end{exercise}\n\\begin{exercise}{536}{三角商函数的导数结构}\n求 $\\int[x+\\sin x\\cos x]/(x\\sin x+\\cos x)^2\\,\\dd x$。通过求导 $\\cos x/(x\\sin x+\\cos x)$ 寻找原函数，说明答案的适用开区间，不要求用初等函数写出分母的所有零点。\n\\end{exercise}\n\\begin{exercise}{537}{三角有理函数与万能代换}\n求 $\\int\\dd x/(\\sin2x+2\\sin x)$。先因式分解并确定全部奇点，再作 $t=\\tan(x/2)$ 积分。说明万能代换遗漏的点是否都是原函数的奇点，以及积分常数如何在定义区间上选择。\n\\end{exercise}\n\\begin{exercise}{538}{万能代换与可去的参数断点}\n求 $\\int\\dd x/(1+\\sin x+\\cos x)$，用 $t=\\tan(x/2)$ 化为有理函数。列出原被积函数的全部奇点，区别原函数的奇点与代换坐标在奇数倍 $\\pi$ 处的失效，说明如何检验答案。\n\\end{exercise}\n\\begin{exercise}{539}{反正切原函数的跨区间拼接}\n求 $\\int\\dd x/(2+\\cos x)$，先在 $(-\\pi,\\pi)$ 采用万能代换。原被积函数在全实数连续，说明为何得到的反正切主值公式仍需按周期补常数，并给出拼接为全实数原函数的方法。\n\\end{exercise}\n\\begin{exercise}{540}{常数项与对数导数拆分}\n求 $\\int(3\\cos x-\\sin x)/(\\cos x+\\sin x)\\,\\dd x$，把分子拆成分母及其导数的线性组合。给出每个最大定义区间的原函数，并明确对数中绝对值的必要性。\n\\end{exercise}\n\\begin{exercise}{541}{对称拆分的三角积分}\n求 $\\int\\sin x/(\\sin x+\\cos x)\\,\\dd x$，利用分母与其导数拆分。再求对应的 $\\int\\cos x/(\\sin x+\\cos x)\\,\\dd x$，检验两者相加与被积函数恒等式一致，说明常数的合并方式。\n\\end{exercise}\n\\begin{exercise}{542}{根式与线性项的三角代换}\n求 $\\int\\dd x/[2x+\\sqrt{1-x^2}]$，在 $(-1,1)$ 使用 $x=\\sin t$。求出分母在该区间的唯一零点，分别给出两侧原函数，并说明代换中根式为何可写为 $\\cos t$。\n\\end{exercise}\n\\begin{exercise}{543}{奇偶拆分与重二次分母}\n求 $\\int(x^3+1)/(1+x^2)^2\\,\\dd x$，先把奇函数部分与偶函数部分分开处理。确定满足 $F(0)=0$ 的原函数，并说明最终答案中哪些项分别来自这两部分。\n\\end{exercise}\n\\begin{exercise}{544}{反正切指数与根式分母}\n求 $\\int x\\mathrm e^{\\arctan x}/(1+x^2)^{3/2}\\,\\dd x$，先令 $t=\\arctan x$，注意 $\\cos t$ 的符号，再完成指数三角积分。说明该原函数可在全实数范围成立的依据。\n\\end{exercise}\n\\begin{exercise}{545}{指数几何和的因式分解}\n求 $\\int\\dd x/(1+\\mathrm e^{x/2}+\\mathrm e^{x/3}+\\mathrm e^{x/6})$。根据指数分母的最小公倍数选取 $t=\\mathrm e^{x/6}$ 化为有理积分，利用 $1+t+t^2+t^3=(1+t)(1+t^2)$ 作部分分式分解，再积分并给出实定义范围，须明确 $\\dd x$ 中的系数。\n\\end{exercise}\n\\begin{exercise}{546}{三角因子与有理代换}\n求 $\\int\\dd x/[(2+\\cos x)\\sin x]$，先确定全部实定义区间，再用 $u=\\cos x$ 化为有理函数积分。解释代换时 $\\sin^2x=1-u^2$ 的作用，并核验所得对数系数。\n\\end{exercise}\n\\begin{exercise}{547}{反正弦分部与根式多项式}\n求 $\\int x^3\\arcsin x/\\sqrt{1-x^2}\\,\\dd x$。先求不含反正弦因子的原函数，再作分部积分，明确实定义区间。说明若先令 $t=\\arcsin x$，为何会转化为多项式三角幂的分部积分。\n\\end{exercise}\n\\begin{exercise}{548}{隐函数约束下的原函数}\n设 $y=y(x)$ 是关系 $y(x-y)^2=x$ 在某开区间上的可导分支，且 $x-3y\\ne0$。求 $\\int\\dd x/(x-3y(x))$，可引入 $u=x-y$ 作参数。推导 $x,y$ 关于 $u$ 的表达式与 $\\dd x$，并明确参数化需要排除的值及积分公式的分支适用条件。\n\\end{exercise}\n\\begin{exercise}{549}{函数关系的单射区间与换元}\n设 $f(\\sin^2t)=t/\\sin t$ 对 $0<t<\\pi/2$ 成立。求 $\\int\\sqrt x\\,f(x)/\\sqrt{1-x}\\,\\dd x$，明确 $f$ 在 $(0,1)$ 上由条件唯一确定的依据。先作 $x=\\sin^2t$，再完成分部积分，并用直接恢复 $f(x)$ 的方法核验。\n\\end{exercise}\n\\begin{exercise}{550}{已知原函数与高阶导数积分}\n设 $\\int f(x)\\,\\dd x=\\mathrm e^{x^2}+C$。求 $f(x)$、$f'(x)$ 及 $\\int xf''(x)\\,\\dd x$。最后一个积分先用分部积分写为 $xf'(x)-f(x)$ 再代入，说明为什么不必展开 $f''$。\n\\end{exercise}\n\\begin{exercise}{551}{加权原函数恢复与奇点}\n已知 $\\int xf(x)\\,\\dd x=\\arcsin x+C$ 在 $(-1,0)$ 或 $(0,1)$ 上成立。求 $f(x)$ 及 $\\int f(x)\\,\\dd x$，给出带绝对值的实表达式。说明在包含 $0$ 的开区间上是否可能存在连续 $f$ 满足原条件。\n\\end{exercise}\n\\begin{exercise}{552}{指数复合导函数的恢复}\n设 $\\int f'(\\mathrm e^t)\\,\\dd t=-(1+t)\\mathrm e^{-t}+C$，且 $f(1)=0$。求 $f(x)$（$x>0$），分别说明对已知积分式求导和将 $x=\\mathrm e^t$ 代回的步骤，再用初值确定常数。\n\\end{exercise}\n\\begin{exercise}{553}{抽象函数商的平方导数}\n设 $f\\in C^2(I)$，且 $f'(x)\\ne0$。证明\n\\[\\int\\left[\\frac{f(x)}{f'(x)}-\\frac{f^2(x)f''(x)}{[f'(x)]^3}\\right]\\,\\dd x=\\frac12\\left[\\frac{f(x)}{f'(x)}\\right]^2+C.\\]\n逐项检查商法则与链式法则产生的分母幂次，并解释条件 $f'\\ne0$ 的必要性；再用 $f(x)=\\mathrm e^x$ 验证。\n\\end{exercise}\n\\begin{exercise}{554}{线性三角组合的平方分母}\n设实数 $a,b$ 满足 $a^2+b^2>0$。证明\n\\[\\int\\frac{\\dd x}{(a\\sin x+b\\cos x)^2}=-\\frac1{a^2+b^2}\\frac{a\\cos x-b\\sin x}{a\\sin x+b\\cos x}+C.\\]\n给出结果成立的区间条件，并分别检查 $a=0$、$b=0$。再说明若 $a=b=0$，为何问题本身失去定义。\n\\end{exercise}\n\\begin{exercise}{555}{参数因子与部分分式退化}\n对 $a\\in\\mathbb R$ 求 $\\int\\dd x/[(x-1)(x-a)]$，完整区分 $a=1$ 与 $a\\ne1$。再取 $0<a<2$，在公共区间 $x<0$ 选取满足 $F_a(-1)=0$ 的原函数，求 $a\\to1$ 时 $F_a(x)$ 的极限，说明积分常数归一化对该极限的作用。\n\\end{exercise}\n\\begin{exercise}{556}{一次因子与重二次因子的联合分解}\n求 $\\int\\dd x/[x(x^2+1)^2]$，先列全部分分式并利用奇偶性减少系数。给出两个半轴上的全部原函数，最后通过求导及 $x\\to0$ 的主项检查对数系数是否正确。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:20:13Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"555209","wall_time_seconds":0.000007542,"exit_code":0,"original_token_count":120,"output":"\\section{第3章 微分中值定理与导数的应用}\n\\subsection{中值定理}\n\\begin{exercise}{289}{罗尔定理的条件与结论}\n分别判断函数 $f(x)=|x|$、$f(x)=x^2-1$、$f(x)=x\\mathrm e^{-x}$、$f(x)=1/x$ 在区间 $[-1,1]$、$[-1,1]$、$[0,1]$、$[-1,1]$ 上是否满足罗尔定理的全部条件，逐项指出依据。对满足条件的函数求全部罗尔点；对不满足条件的函数，判断开区间内是否仍有导数为零的点。\n\\end{exercise}\n"}
{}
{}
{"chunk_id":"6cca55","wall_time_seconds":0.000005542,"exit_code":0,"original_token_count":81,"output":"\\begin{exercise}{422}{基础·抛物线曲率变式}\n求 $y=2x^2$ 在原点处的曲率及曲率半径。\n\\end{exercise}\n\\begin{exercise}{423}{常规·椭圆曲率综合}\n设椭圆 $x=2\\cos t$、$y=\\sin t$。求 $t=0$ 与 $t=\\pi/2$ 两点的曲率半径并比较大小。可使用参数曲线曲率公式。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:20:30Z




## tool · 2026-10-20T03:22:49Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"35339e","wall_time_seconds":0.000008792,"exit_code":0,"original_token_count":105,"output":"\\section{第4章 不定积分}\n\\subsection{不定积分的概念与性质}\n\\begin{exercise}{424}{原函数关系与二阶求导}\n设 $f$ 在 $(1,+\\infty)$ 上的一个原函数为 $F(x)=\\ln(x+\\sqrt{x^2-1})$。求 $f(x)$ 和 $f'(x)$，说明两次求导所用的定义域条件。若把原函数改为 $F(x)+C$，说明所求两个函数是否改变。\n\\end{exercise}\n\\begin{exercise}{425}{原函数族与参数退化}\n"}
{}
{}
{"chunk_id":"7dcae5","wall_time_seconds":0.000007,"exit_code":0,"original_token_count":131,"output":"\\end{exercise}\n\\begin{exercise}{554}{常规·线性三角组合平方}\n求 $\\int\\dd x/(\\sin x+\\cos x)^2$，在分母非零的开区间上考虑。提示：先写成 $2\\sin^2(x+\\pi/4)$。\n\\end{exercise}\n\\begin{exercise}{555}{基础·部分分式变式}\n求 $\\int\\dd x/[(x-1)(x-2)]$，在不含 $1,2$ 的开区间上考虑。\n\\end{exercise}\n\\begin{exercise}{556}{常规·有理积分小综合}\n求 $\\int\\dd x/[x(x^2+1)^2]$，在两个半轴上分别考虑。提示：先拆为 $1/x-x/(x^2+1)-x/(x^2+1)^2$。\n\\end{exercise}\n"}

## tool · 2026-10-20T03:23:13Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"8b6207","wall_time_seconds":0.000017208,"exit_code":0,"original_token_count":148,"output":"output/大一数学分析期末复习-上册/chapters/ch04.tex:139:\\begin{exercise}{469}{常规·商函数导数识别}\noutput/大一数学分析期末复习-上册/chapters/ch04.tex:248:\\begin{exercise}{505}{常规·指数换元与分部积分}\noutput/大一数学分析期末复习-上册/chapters/ch01.tex:128:\\begin{exercise}{42}{常规·复合极限}\noutput/大一数学分析期末复习-上册/chapters/ch01.tex:415:\\begin{exercise}{136}{常规·有理无理分段函数}\noutput/大一数学分析期末复习-上册/chapters/ch03.tex:218:\\begin{exercise}{360}{基础·对数展开}\n"}
{}
{"chunk_id":"b6144c","wall_time_seconds":0.000006833,"exit_code":0,"original_token_count":375,"output":"output/大一数学分析期末复习-上册/chapters/ch04.tex:139:\\begin{exercise}{469}{常规·商函数导数识别}\noutput/大一数学分析期末复习-上册/chapters/ch04.tex-140-求 $\\int(x\\cos x-\\sin x)/x^2\\,\\dd x$，在两个半轴上分别考虑。提示：计算 $(\\sin x/x)'$。\n--\noutput/大一数学分析期末复习-上册/chapters/ch04.tex:248:\\begin{exercise}{505}{常规·指数换元与分部积分}\noutput/大一数学分析期末复习-上册/chapters/ch04.tex-249-求 $\\int xe^{\\sqrt x}/\\sqrt x\\,\\dd x$（$x>0$）。提示：令 $t=\\sqrt x$，积分化为 $2\\int t^2e^t\\,\\dd t$。\n--\noutput/大一数学分析期末复习-上册/chapters/ch03.tex:218:\\begin{exercise}{360}{基础·对数展开}\noutput/大一数学分析期末复习-上册/chapters/ch03.tex-219-设 $f(x)=\\ln(1-3x)$。写出 $f$ 在 $0$ 处的三阶麦克劳林公式，并求 $f'''(0)$。\n--\noutput/大一数学分析期末复习-上册/chapters/ch01.tex:128:\\begin{exercise}{42}{基础·复合极限}\noutput/大一数学分析期末复习-上册/chapters/ch01.tex-129-已知 $\\lim_{u\\to0}f(u)=2$。求 $\\lim_{x\\to0}f(3x)$ 和 $\\lim_{x\\to0}f(x^2)$，其中只考虑 $x\\ne0$。\n--\noutput/大一数学分析期末复习-上册/chapters/ch01.tex:415:\\begin{exercise}{136}{基础·有理无理分段函数}\noutput/大一数学分析期末复习-上册/chapters/ch01.tex-416-设 $f(x)=x^2$（$x\\in\\mathbb Q$），$f(x)=0$（$x\\notin\\mathbb Q$）。利用 $0\\le f(x)\\le x^2$ 判断 $f$ 在 $0$ 处是否连续。\n"}
{"chunk_id":"d8d4ab","wall_time_seconds":0.000006709,"exit_code":1,"original_token_count":79,"output":"Traceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nImportError: cannot import name 'LatexEnvironmentSpec' from 'pylatexenc.macrospec' (/Users/oyamahappa/Documents/Agent/Codex/.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/macrospec/__init__.py). Did you mean: 'EnvironmentSpec'?\n"}

## tool · 2026-10-20T03:23:25Z




## tool · 2026-10-20T03:23:30Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"02e055","wall_time_seconds":0.000006084,"exit_code":0,"original_token_count":64,"output":"(s, latex_context=None, **kwargs)\n(environmentname, args_parser=MacroStandardArgsParser(argspec='', optional_arg_no_space=False, args_math_mode=None), is_math_mode=False, **kwargs)\n(argspec=None, optional_arg_no_space=False, args_math_mode=None, **kwargs)\n"}
{"chunk_id":"d4b9ec","wall_time_seconds":0.000005125,"exit_code":1,"original_token_count":0,"output":""}
{"chunk_id":"e6fa6f","wall_time_seconds":0.000006041,"exit_code":0,"original_token_count":20,"output":"__pycache__\narchive_plan.py\ncheck_all.py\ncheck_root_math.py\npackage_sources.py\n"}

## tool · 2026-10-20T03:24:17Z


Script completed
Wall time 0.7 seconds
Output:

{}
{"chunk_id":"a0d2ab","wall_time_seconds":0.466638083,"exit_code":1,"original_token_count":209,"output":"{\"status\": \"failed\", \"type\": \"AssertionError\", \"message\": \"\", \"suggestion\": \"修正对应题面或结构后重新运行本只读检查。\"}\nTraceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/final-calibration/check_upper_foundations.py\", line 138, in <module>\n    main()\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/final-calibration/check_upper_foundations.py\", line 129, in main\n    chapters = check_structure()\n               ^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/final-calibration/check_upper_foundations.py\", line 86, in check_structure\n    assert sum(item[\"levels\"].get(\"基础\", 0) for item in summaries) > 278\n           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^\nAssertionError\n"}
