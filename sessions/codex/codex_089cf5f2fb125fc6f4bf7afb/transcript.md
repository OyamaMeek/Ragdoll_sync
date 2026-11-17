# 01a15716-eff1-7313-96e1-f12e40cc8429

来源：codex

项目：/Users/oyamahappa/Documents/Agent/Codex

## developer · 2026-10-20T02:14:46Z

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



## developer · 2026-10-20T02:14:46Z

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

## developer · 2026-10-20T02:14:46Z

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

## developer · 2026-10-20T02:14:46Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-10-20T02:14:46Z

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

## developer · 2026-10-20T02:14:46Z

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


## tool · 2026-10-20T02:14:49Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"ffd0a5","wall_time_seconds":0.000007792,"exit_code":0,"original_token_count":10,"output":"/Users/oyamahappa/Documents/Agent/Codex\n"}
{"chunk_id":"e202cc","wall_time_seconds":0.0000095,"exit_code":0,"original_token_count":35,"output":"001.md\n002.md\n003.md\n004.md\n005.md\n006.md\n007.md\n008.md\n009.md\n010.md\n011.md\n012.md\n013.md\n014.md\n015.md\n016.md\n017.md\n018.md\n019.md\n020.md\n"}
{"chunk_id":"0a9528","wall_time_seconds":0.000010292,"exit_code":0,"original_token_count":14,"output":"ch08.tex\nch09.tex\nch10.tex\nch11.tex\nch12.tex\nch13.tex\n"}

## tool · 2026-10-20T02:14:54Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"2f9e77","wall_time_seconds":0.0000105,"exit_code":0,"original_token_count":842,"output":"Contents\n目录\n\n第1章 函数与极限\n\n第一节 函数·····1\n第二节 数列的极限·····3\n第三节 函数的极限·····4\n第四节 无穷小与无穷大·····6\n第五节 极限的运算法则·····8\n第六节 极限存在准则 两个重要极限·····10\n第七节 无穷小的比较·····13\n第八节 函数的连续性与间断点·····15\n第九节 连续函数的运算与初等函数的连续性·····18\n第十节 闭区间上连续函数的性质·····18\n\n第2章 导数与微分\n\n第一节 导数的基本概念·····20\n第二节 函数的求导法则·····24\n第三节 高阶导数·····26\n第四节 隐函数及由参数方程所确定的函数的导数·····28\n第五节 函数的微分·····30\n\n第3章 微分中值定理与导数的应用\n\n第一节 中值定理·····352 目录\n\n第二节 洛必达法则·····39\n第三节 泰勒公式·····42\n第四节 函数的单调性与曲线的凹凸性·····44\n第五节 函数的极值和最值·····47\n第六节 函数图形的描绘·····50\n第七节 曲率·····52\n\n第4章 不定积分\n\n第一节 不定积分的概念与性质·····54\n第二节 换元积分法·····56\n第三节 分部分积法·····61\n第四节 有理函数的积分·····63\n\n第5章 定积分\n\n第一节 定积分的概念与性质·····67\n第二节 微积分基本公式·····69\n第三节 定积分的换元积分法和分部分积法·····71\n第四节 反常积分·····74\n\n第6章 定积分的应用\n\n第一节 定积分在几何学上的应用·····78\n第二节 定积分在物理学上的应用·····86目录 3\n\n第7章 微分方程\n\n第一节 微分方程的基本概念………………………………………………………88\n第二节 可分离变量的微分方程………………………………………………………89\n第三节 齐次方程……………………………………………………………………………91\n第四节 一阶线性微分方程…………………………………………………………………92\n第五节 可降阶的高阶微分方程………………………………………………………93\n第六节 高阶线性微分方程…………………………………………………………………95\n第七节 常系数齐次线性微分方程………………………………………………………97\n第八节 常系数非齐次线性微分方程………………………………………………………99\n\n答案\n\n第1章 函数与极限………………………………………………………………………101\n第2章 导数与微分……………………………………………………………………………137\n第3章 微分中值定理与导数的应用………………………………………………………166\n第4章 不定积分……………………………………………………………………………196\n第5章 定积分……………………………………………………………………………226\n第6章 定积分的应用……………………………………………………………………………248\n第7章 微分方程……………………………………………………………………………268"}
{"chunk_id":"8600c2","wall_time_seconds":0.000018458,"exit_code":0,"original_token_count":2249,"output":"\\section{第8章 向量代数与空间解析几何}\n\\subsection{向量及其线性运算}\n\\begin{exercise}{1}{线性组合与线性无关}\n设 $\\vec u=\\vec a-\\vec b+\\vec c$，$\\vec v=\\vec a+3\\vec b-2\\vec c$，其中 $\\vec a,\\vec b,\\vec c$ 线性无关。用它们表示 $2\\vec u-\\vec v$，并判断是否存在实数 $s,t$ 使 $s\\vec u+t\\vec v=\\vec c$，说明理由。\n\\end{exercise}\n\\begin{exercise}{2}{坐标运算与正交条件}\n设 $\\vec a=(0,-1,1)$，$\\vec b=(1,2,0)$，$\\vec c=(2,0,1)$。求 $\\vec p=\\vec a-\\vec b+\\vec c$、$\\vec q=\\vec a+2\\vec b-3\\vec c$ 的坐标，并求使 $\\vec p+\\lambda\\vec q$ 与 $\\vec c$ 垂直的实数 $\\lambda$。\n\\end{exercise}\n\\begin{exercise}{3}{三等分点与端点恢复}\n线段 $AB$ 的两个三等分点为 $C(2,0,2)$、$D(5,-2,0)$。求无序端点集 $\\{A,B\\}$ 及线段长度，并说明交换 $C,D$ 的先后次序对结果有何影响。\n\\end{exercise}\n\\begin{exercise}{4}{内外分点与参数范围}\n设 $A(x_1,y_1,z_1)\\ne B(x_2,y_2,z_2)$。对实数 $\\lambda$，讨论线段 $AB$ 上满足距离关系 $|AM|=\\lambda|MB|$ 的点 $M$ 是否存在、是否唯一；存在时求其坐标。再讨论将 $M$ 的范围改为整条直线 $AB$ 时，正参数 $\\lambda$ 对解的个数有何影响。\n\\end{exercise}\n\\begin{exercise}{5}{平行条件与投影}\n设 $A(1,2,3)$、$B(3,5,t)$，$\\vec a=(2,3,-2)$。求使 $\\overrightarrow{AB}$ 与 $\\vec a$ 平行的 $t$，并求此时 $\\overrightarrow{AB}$ 在 $\\vec a$ 方向上的标量投影。\n\\end{exercise}\n\\begin{exercise}{6}{向量平行的参数判定}\n设 $\\vec a=(1,2,3)$、$\\vec b=(2,k,t)$。求使两向量平行的所有 $(k,t)$，并判断是否可能反向。若仅要求 $\\vec b-\\vec a$ 与 $\\vec a$ 平行，参数条件是否改变？证明你的结论。\n\\end{exercise}\n\\begin{exercise}{7}{反向单位向量与定长向量}\n设 $A(-1,2,2)$、$B(1,2,0)$。求与 $\\overrightarrow{AB}$ 反向的单位向量 $\\vec e$，并求满足 $\\vec v\\parallel\\overrightarrow{AB}$、$|\\vec v|=3$ 的全部向量。\n\\end{exercise}\n\\begin{exercise}{8}{方向角及其约束}\n设 $A(1,1,-\\sqrt2)$、$B(2,2,0)$。求 $\\overrightarrow{AB}$ 的模、方向余弦与方向角，并由本题数据验证方向余弦的平方和为 $1$。能否存在方向角均为锐角且三者相等的非零向量？若能，求共同方向角。\n\\end{exercise}\n\\begin{exercise}{9}{标量投影与垂直分解}\n向量 $\\vec a$ 的模为 $9$，与有向 $u$ 轴的夹角为 $\\frac\\pi4$。求其在该轴上的标量投影及垂直于该轴的分量的模。若将轴的正方向反转，这两个结果如何改变？\n\\end{exercise}\n\\begin{exercise}{10}{等模条件与正交}\n设 $\\vec a=(3,-5,8)$、$\\vec b=(-1,1,p)$。求满足 $|\\vec a+\\vec b|=|\\vec a-\\vec b|$ 的 $p$，并证明一般向量的这一等式与 $\\vec a\\cdot\\vec b=0$ 等价。\n\\end{exercise}\n\\begin{exercise}{11}{距离比轨迹与退化情形}\n设 $A(2,0,-3)$、$B(4,-6,6)$。求满足 $|MA|=3|MB|$ 的动点 $M$ 的轨迹方程、球心与半径。再将距离比 $3$ 改为 $1$，求轨迹并说明其几何类型。\n\\end{exercise}\n\\begin{exercise}{12}{向量证明与比例推广}\n在非退化三角形 $ABC$ 中，$M,N$ 分别为 $AB,AC$ 的中点。用向量证明 $MN\\parallel BC$ 且 $|MN|=\\frac12|BC|$。进一步，若 $\\overrightarrow{AM}=t\\overrightarrow{AB}$、$\\overrightarrow{AN}=t\\overrightarrow{AC}$，其中 $0<t<1$，求 $\\overrightarrow{MN}$ 并证明相应的长度关系。\n\\end{exercise}\n\\begin{exercise}{13}{点的线性组合与原点选择}\n设 $A,B$ 的位置向量为 $\\vec a,\\vec b$，以 $\\alpha\\vec a+\\beta\\vec b$ 作为点 $P$ 的位置向量。证明这一构造在任意平移坐标原点后仍表示同一几何点的充要条件是 $\\alpha+\\beta=1$。在此条件下，说明 $P$ 在线段 $AB$ 上的充要条件，其中 $A\\ne B$。\n\\end{exercise}\n\\begin{exercise}{14}{线段参数与交点条件}\n设 $A(0,0,0)$、$B(2,1,1)$、$C(1,0,a)$、$D(1,2,a-2)$。用线性组合分别表示直线 $AB,CD$ 上的点，求两直线相交的参数 $a$；相交时判断交点是否同时在线段 $AB,CD$ 上，并求其对两条线段的分比。\n\\end{exercise}\n\\subsection{内积、向量积与混合积}\n\\begin{exercise}{15}{三种乘积与体积}\n设 $\\vec a=(1,-2,-3)$，$\\vec b=(2,2,-3)$，$\\vec c=(2,1,-3)$。计算 $(2\\vec a)\\cdot\\vec b$、$(3\\vec a)\\times(2\\vec b)$ 及 $[(3\\vec a)\\times(2\\vec b)]\\cdot\\vec c$，并求以 $\\vec a,\\vec b,\\vec c$ 为棱的四面体体积。\n\\end{exercise}\n\\begin{exercise}{16}{混合积的线性性质}\n设 $(\\vec a\\times\\vec b)\\cdot\\vec c=2$。计算 $[(\\vec a+\\vec b)\\times(\\vec b+\\vec c)]\\cdot(\\vec c+\\vec a)$，并求使 $\\vec a+\\vec b,\\vec b+\\vec c,\\vec c+t\\vec a$ 共面的全部实数 $t$。\n\\end{exercise}\n\\begin{exercise}{17}{向量积展开与恒等式}\n化简 $(2\\vec a+\\vec b)\\times(\\vec c-\\vec a)+(\\vec b+\\vec c)\\times(\\vec a+\\vec b)$。若 $\\vec a,\\vec b,\\vec c$ 线性无关，判断该式是否可能为零向量，并证明。\n\\end{exercise}\n\\begin{exercise}{18}{内积消去与充要条件}\n设 $\\vec c\\ne\\vec0$ 且 $\\vec a\\cdot\\vec c=\\vec b\\cdot\\vec c$。证明 $(\\vec a-\\vec b)\\cdot\\vec c=0$，并举例说明能否由此推出 $\\vec a=\\vec b$。若另有 $\\vec a-\\vec b$ 与 $\\vec c$ 平行，结论如何？\n\\end{exercise}\n\\begin{exercise}{19}{共线条件与方向判定}\n设 $\\vec a,\\vec b$ 不共线。求使 $k\\vec a+\\vec b$ 与 $\\vec a+k\\vec b$ 共线的全部实数 $k$，并分别判断这两个向量同向还是反向。\n\\end{exercise}\n\\begin{exercise}{20}{三角形面积与高}\n设 $A(2,-1,2)$、$B(1,1,3)$、$C(1,2,-1)$。用向量积求三角形 $ABC$ 的面积及从 $A$ 到直线 $BC$ 的距离，并说明三个点为何不共线。\n\\end{exercise}\n\\begin{exercise}{21}{面积与等面积轨迹}\n设 $A(2,-1,3)$、$B(1,2,3)$、$C(0,1,4)$。求三角形 $ABC$ 的面积。保持 $A,B$ 固定，令 $C_t=C+t\\overrightarrow{AB}$，证明三角形 $ABC_t$ 的面积与 $t$ 无关。\n\\end{exercise}\n\\begin{exercise}{22}{平行约束与最小模}\n设 $\\vec m=(2,-3,1)$。求与 $\\vec m$ 共线且满足 $\\vec r\\cdot\\vec m=14$ 的 $\\vec r$。若去掉共线条件，证明所有满足该内积条件的向量中，刚求得的向量的模最小。\n\\end{exercise}\n\\begin{exercise}{23}{正交参数与投影系数}\n设 $|\\vec a|=2$，$|\\vec b|=5$，夹角为 $\\frac{2\\pi}3$，$\\vec p=3\\vec a-\\vec b$、$\\vec q=\\lambda\\vec a+17\\vec b$。求使 $\\vec p\\perp\\vec q$ 的 $\\lambda$，并求此时 $\\vec q$ 在 $\\vec a$ 方向上的标量投影。\n\\end{exercise}\n\\begin{exercise}{24}{内外积关系与信息充分性}\n设 $|\\vec a|=3$，$|\\vec b|=26$，$|\\vec a\\times\\vec b|=72$。求 $\\vec a\\cdot\\vec b$ 的所有可能值，并说明还需知道夹角的什么信息才能唯一确定内积。\n\\end{exercise}\n\\begin{exercise}{25}{正交关系联立与夹角}\n非零向量 $\\vec a,\\vec b$ 满足 $(\\vec a+3\\vec b)\\perp(7\\vec a-5\\vec b)$ 及 $(\\vec a-4\\vec b)\\perp(7\\vec a-2\\vec b)$。求 $|\\vec a|:|\\vec b|$ 与两向量夹角，并核验所得数据满足 $|\\cos\\theta|\\le1$。\n\\end{exercise}\n\\begin{exercise}{26}{共面判定与有向体积}\n设 $\\vec a=(3,0,-1)$，$\\vec b=(2,-4,3)$，$\\vec c=(-1,-2,2)$。判断三向量是否共面，求它们所张成的平行六面体体积；再求使 $\\vec a,\\vec b,\\vec c+t\\vec a$ 共面的实数 $t$，或证明不存在。\n\\end{exercise}\n\\begin{exercise}{27}{拉格朗日恒等式与等号}\n证明 $|\\vec a\\times\\vec b|^2+(\\vec a\\cdot\\vec b)^2=|\\vec a|^2|\\vec b|^2$，并由此证明 $|\\vec a\\cdot\\vec b|\\le |\\vec a||\\vec b|$，完整讨论等号成立条件，包括零向量情形。\n\\end{exercise}\n\\begin{exercise}{28}{余弦定理及逆命题}\n设三角形 $ABC$ 的对边长为 $a,b,c$。用向量内积证明三条余弦定理 $a^2=b^2+c^2-2bc\\cos A$、$b^2=a^2+c^2-2ac\\cos B$、$c^2=a^2+b^2-2ab\\cos C$，再据此证明 $A$ 为锐角的充要条件是 $a^2<b^2+c^2$。\n\\end{exercise}\n\\begin{exercise}{29}{三高共点的向量证明}\n用向量证明非退化三角形的三条高所在直线共点。证明中说明两条高为何必有唯一交点，并证明该交点也在第三条高上。\n\\end{exercise}\n\\begin{exercise}{30}{正交分解与最小距离原理}\n设 $\\vec b\\ne\\vec0$。证明函数 $|\\vec a-t\\vec b|^2$ 在实数 $t$ 上有唯一最小值，求极小点并证明此时 $\\vec a-t\\vec b$ 与 $\\vec b$ 垂直。由最小值非负推导内积不等式，并完整讨论等号条件。\n\\end{exercise}\n\\begin{exercise}{31}{混合积的参数讨论}\n设 $\\vec a=(1,1,0)$、$\\vec b=(0,1,1)$、$\\vec c_t=(1,t,1)$。求三向量共面的全部 $t$，共面时将 $\\vec c_t$ 表为 $\\vec a,\\vec b$ 的线性组合；再求以这三向量为棱的平行六面体体积不超过 $2$ 的参数范围，并求对应四面体的最大体积。\n\\end{exercise}\n\\subsection{平面方程}\n\\begin{exercise}{32}{点法式与垂足}\n求过 $A(1,2,3)$ 且垂直于直线 $\\frac{x-2}{2}=\\frac{y+1}{4}=\\frac{z+2}{5}$ 的平面，并求该直线与平面的交点以及 $A$ 到直线的距离。\n\\end{exercise}\n"}
{"chunk_id":"982c4e","wall_time_seconds":0.000006708,"exit_code":0,"original_token_count":1672,"output":"---\nname: using-superpowers\ndescription: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions\n---\n\n<SUBAGENT-STOP>\nIf you were dispatched as a subagent to execute a specific task, ignore this skill.\n</SUBAGENT-STOP>\n\n<EXTREMELY-IMPORTANT>\nIf you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.\n\nIF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.\n\nThis is not negotiable. You cannot rationalize your way out of this.\n</EXTREMELY-IMPORTANT>\n\n## The Rule\n\n**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.\n\n**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.\n\nThen announce \"Using [skill] to [purpose]\" and follow the skill exactly. If it has a checklist, create a todo per item.\n\n## Skill Priority\n\nWhen multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.\n\n- \"Let's build X\" → superpowers:brainstorming first, then implementation skills.\n- \"Fix this bug\" → superpowers:systematic-debugging first, then domain skills.\n\n## Red Flags\n\nThese thoughts mean STOP—you're rationalizing:\n\n| Thought | Reality |\n|---------|---------|\n| \"This is just a simple question\" | Questions are tasks. Check for skills. |\n| \"I need more context first\" | Skill check comes BEFORE clarifying questions. |\n| \"Let me explore the codebase first\" | Skills tell you HOW to explore. Check first. |\n| \"I can check git/files quickly\" | Files lack conversation context. Check for skills. |\n| \"Let me gather information first\" | Skills tell you HOW to gather information. |\n| \"This doesn't need a formal skill\" | If a skill exists, use it. |\n| \"I remember this skill\" | Skills evolve. Read current version. |\n| \"This doesn't count as a task\" | Action = task. Check for skills. |\n| \"The skill is overkill\" | Simple things become complex. Use it. |\n| \"I'll just do this one thing first\" | Check BEFORE doing anything. |\n| \"This feels productive\" | Undisciplined action wastes time. Skills prevent this. |\n| \"I know what that means\" | Knowing the concept ≠ using the skill. Invoke it. |\n\n## Platform Adaptation\n\nIf your harness appears here, read its reference file for special instructions:\n\n- Claude Code: `references/claude-code-tools.md`\n- Codex: `references/codex-tools.md`\n- Pi: `references/pi-tools.md`\n- Antigravity: `references/antigravity-tools.md`\n- Hermes Agent: `references/hermes-tools.md`\n- Muse: `references/muse-tools.md`\n\n## User Instructions\n\nUser instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to.\n---\nname: ponytail\ndescription: >\n  Lazy senior dev mode: the smallest change that fully solves the task, and a\n  reply a busy human understands in one read. Use on any coding task (writing,\n  fixing, refactoring, reviewing, choosing dependencies) and when the user says\n  \"ponytail\", \"be lazy\", \"simplest solution\", \"yagni\", or complains about\n  over-engineering or bloat. Levels: lite, full (default), ultra.\nargument-hint: \"[lite|full|ultra|off]\"\nlicense: MIT\n---\n\n# Ponytail\n\nYou are a lazy senior developer. The best code is the code never written. You solve the whole problem with the least new code. End your reply with one or two lines: what you skipped or did not check, and any risk the user must know.\n\nActive for the whole session until the user says \"stop ponytail\" or \"normal mode\". Switch level: `/ponytail lite|full|ultra`.\n\n## Before you write\n\nRead the task and the code it touches. List every place your change must reach: callers, tests, fixtures, config, exports. Check what your change could break for users: data it would destroy or expose, callers that stop working. That is scope. Extra features are not.\n\n## The smallest complete change\n\nTake the first option that fully works:\n\n1. Does it need to exist? Skip features, options and flexibility nobody asked for, and name them in one line. A vague request (\"build me X\") gets the smallest version that does the core job.\n2. Already in this codebase (a helper, component, service, pattern)? Use it the way the surrounding code does.\n3. Standard library or a platform feature? Use it, unless the project has its own. A house component beats a native widget.\n4. An installed dependency? Use it. Never add a dependency for a few lines.\n5. Can it be one line a reader gets at a glance? One line.\n6. Otherwise: the minimum code that works.\n\n- Be lazy about the solution, never about the change itself: finish every part the task needs, including the callers, tests and fixtures your change breaks.\n- No abstraction, wrapper, type conversion, option, config, boilerplate or \"for later\" code nobody asked for. Keep values in the form the platform already gives you. Deletion beats addition. Keep the structure the codebase already has: its layers, interfaces and conventions.\n- The shortest working diff wins, once you know everything it must touch. A one-liner that needs decoding is not short.\n- Comment only the why the code cannot show, in one line.\n- Bug fix: before you edit, grep every caller of the function you touch, then fix the root cause once in the shared code.\n- Code you move or merge keeps its error handling and validation.\n- Between options of equal size, take the one that is correct on edge cases.\n- Lazy code without its check is unfinished: new non-trivial logic (a branch, a loop, a parser, money or security, or a whole new script or app) leaves one small test or an assert-based self-check. Trivial changes need none.\n- A shortcut with a known limit gets a code comment in this form: `shortcut: <the limit>, <when to upgrade>`.\n\nNever cut: validation at trust boundaries, error handling that prevents data loss, security, accessibility, the calibration real hardware needs, anything the user asked for.\n\n## Levels\n\n| Level | Behavior |\n|-------|----------|\n| **lite** | Build what was asked. Name the smaller option in one line and let the user pick. |\n| **full** | The rules above. Default. |\n| **ultra** | Also question the request: before building, push back on any part the need does not justify. |\n"}

## tool · 2026-10-20T02:15:02Z




## tool · 2026-10-20T02:15:08Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"7c1a85","wall_time_seconds":0.000007917,"exit_code":1,"original_token_count":36,"output":"ls: .agent/math-analysis/upper: No such file or directory\nls: output/工科数学分析逐题训练-上册/chapters: No such file or directory\n"}
{"chunk_id":"909aa9","wall_time_seconds":0.000006333,"exit_code":0,"original_token_count":681,"output":".agent/hdu-ocr/check_math2026.py\n.agent/hdu-ocr/e43b7f46d6f192ef.json\n.agent/hdu-ocr/be2d15e5112d94ec.json\n.agent/hdu-ocr/build.py\n.agent/hdu-ocr/b08aed2582f249fa.json\n.agent/hdu-ocr/acfa1aa51180266a.json\n.agent/hdu-ocr/syntax-check-analysis/results.json\n.agent/hdu-ocr/80362948e7ab6a73.json\n.agent/hdu-ocr/e3e469709b9c871a.json\n.agent/hdu-ocr/11e51f898301adc8.json\n.agent/hdu-ocr/2c29e49c601a658a.json\n.agent/hdu-ocr/f5e95ba433b26042.json\n.agent/hdu-ocr/730ce62de1c053f8.json\n.agent/hdu-ocr/27ea8f6e4eb7355d.json\n.agent/hdu-ocr/918271f5178ca024.json\n.agent/hdu-ocr/81dd8dbba3a7fd94.json\n.agent/hdu-ocr/128a26e7394a073e.json\n.agent/hdu-ocr/syntax-check-2018-2023/results.json\n.agent/hdu-ocr/92a5bd5ef85605e7.json\n.agent/hdu-ocr/check_math_syntax_2018_2023.py\n.agent/hdu-ocr/67f5486ba76670aa.json\n.agent/hdu-ocr/d8ce5bd25864c7be.json\n.agent/hdu-ocr/check_algebra2025.py\n.agent/hdu-ocr/8dd3d46a83f4a8fa.json\n.agent/hdu-ocr/176002d27d3f75a0.json\n.agent/hdu-ocr/5f1a832afe7df592.json\n.agent/hdu-ocr/2206d7cb7039f357.json\n.agent/hdu-ocr/check_pairs.py\n.agent/hdu-ocr/9e64c36cdac10429.json\n.agent/hdu-ocr/8f2812e5a7f76721.json\n.agent/hdu-ocr/a0ed6eec172d6642.json\n.agent/hdu-ocr/compile-results.json\n.agent/hdu-ocr/check_algebra2026.py\n.agent/hdu-ocr/check_analysis_2011_2015.py\n.agent/hdu-ocr/collection-mapping.json\n.agent/hdu-ocr/17d24cef69545777.json\n.agent/hdu-ocr/check_math2024_2025.py\n.agent/hdu-ocr/local_ocr.py\n.agent/hdu-ocr/cd2a7a833ba8f5fa.json\n.agent/hdu-ocr/136a64e93d88bac6.json\n.agent/hdu-ocr/check_math_content_2018_2023.py\n.agent/hdu-ocr/3f7b5ea1df00c613.json\n.agent/hdu-ocr/1abbef1daec3bc92.json\n.agent/hdu-ocr/compile.py\n.agent/hdu-ocr/math-content-check-2018-2023/results.json\n.agent/hdu-ocr/5dad5f846d278490.json\n.agent/hdu-ocr/52d23623a0404647.json\n.agent/hdu-ocr/recognize.py\n.agent/hdu-ocr/e89f4e631d1c748b.json\n.agent/hdu-ocr/f6badbfa1728d169.json\n.agent/hdu-ocr/inventory.json\n.agent/hdu-ocr/huggingface/.agent_harnesses.json\n.agent/hdu-ocr/sample-upload.json\n.agent/hdu-ocr/glm-model/tokenizer_config.json\n.agent/hdu-ocr/glm-model/config.json\n.agent/hdu-ocr/glm-model/tokenizer.json\n.agent/hdu-ocr/glm-model/processor_config.json\n.agent/hdu-ocr/glm-model/generation_config.json\n.agent/hdu-ocr/glm-model/model.safetensors.index.json\n.agent/hdu-ocr/glm-model/preprocessor_config.json\n.agent/hdu-ocr/check_collection.py\n.agent/hdu-ocr/verify.py\n.agent/hdu-ocr/2d6c75fa58bfc5b1.json\n.agent/hdu-ocr/9ced401653581657.json\n.agent/hdu-ocr/sample-state.json\n.agent/hdu-ocr/391fa17a5f0f6f61.json\n.agent/hdu-ocr/22a122cb4a98dc46.json\n.agent/hdu-ocr/jobs.json\n.agent/hdu-ocr/3f56d1c0da59f54e.json\n.agent/hdu-ocr/check_analysis_content.py\n.agent/hdu-ocr/842284019302ba43.json\n.agent/hdu-ocr/85b8c8c41edb8e84.json\n"}

## tool · 2026-10-20T02:15:14Z




## tool · 2026-10-20T02:15:42Z


Wall time: 23.6352 seconds
Sleep interrupted by new input.

## tool · 2026-10-20T02:15:48Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"4071f8","wall_time_seconds":0.000039667,"exit_code":0,"original_token_count":51,"output":"001.md\n002.md\n003.md\n004.md\n005.md\n006.md\n007.md\n008.md\n009.md\n010.md\n011.md\n012.md\n013.md\n014.md\n015.md\n016.md\n017.md\n018.md\n019.md\n020.md\n021.md\n022.md\n023.md\n024.md\n025.md\n026.md\n027.md\n028.md\n029.md\n"}

## tool · 2026-10-20T02:16:55Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-10-20T02:17:09Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"5ab41e","wall_time_seconds":0.000008875,"exit_code":0,"original_token_count":322,"output":"\\section{第6章 定积分的应用}\n\\subsection{定积分在几何学上的应用}\n\\begin{supplement}{6.1-1}{面积、体积与参数约束}\n对 $a>0$，区域 $D_a$ 由 $y=x^2$、$y=ax$ 围成。求其面积及绕 $x$ 轴旋转所得立体的体积；若区域面积等于 $\\frac43$，求 $a$ 与相应体积。\n\\end{supplement}\n\\begin{supplement}{6.1-2}{弧长与旋转曲面面积}\n曲线 $y=\\ln\\cosh x$，$0\\le x\\le\\ln2$，其中 $\\cosh x=(e^x+e^{-x})/2$。求曲线弧长以及绕 $y$ 轴旋转所得曲面的面积，并写出所用弧长微元。\n\\end{supplement}\n\\subsection{定积分在物理学上的应用}\n\\begin{supplement}{6.2-1}{变力做功与功率}\n质量为 $m$ 的物体沿水平直线运动，阻力大小为 $kv^2$，其中 $k>0$、$v$ 为速率。物体仅受此阻力，从速率 $v_0>0$ 减至 $v_0/2$。求此过程中的位移、阻力做功，并核验动能定理。\n\\end{supplement}\n\\begin{supplement}{6.2-2}{液体压力与水深参数}\n竖直薄板为底边水平的等腰三角形，高 $h$、底边长 $b$，顶点在底边上方。薄板顶点距水面 $d\\ge0$，水的密度为 $\\rho$。求单侧静水总压力 $P(d)$；若将薄板翻转使底边在上方且最高点仍在深度 $d$ 处，求压力变化量并解释其符号。\n\\end{supplement}\n"}
{"chunk_id":"b506a6","wall_time_seconds":0.000009416,"exit_code":0,"original_token_count":72,"output":"001.md\n002.md\n003.md\n004.md\n005.md\n006.md\n007.md\n008.md\n009.md\n010.md\n011.md\n012.md\n013.md\n014.md\n015.md\n016.md\n017.md\n018.md\n019.md\n020.md\n021.md\n022.md\n023.md\n024.md\n025.md\n026.md\n027.md\n028.md\n029.md\n030.md\n031.md\n032.md\n033.md\n034.md\n035.md\n036.md\n037.md\n038.md\n039.md\n040.md\n041.md\n"}

## tool · 2026-10-20T02:17:19Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"chunk_id":"48fa5a","wall_time_seconds":0.00000975,"exit_code":0,"original_token_count":325,"output":"\\section{第6章 定积分的应用}\n\\subsection{定积分在几何学上的应用}\n\\begin{supplement}{6.1-1}{面积、体积与参数约束}\n对 $a>0$，区域 $D_a$ 由 $y=x^2$、$y=ax$ 围成。求其面积及绕 $x$ 轴旋转所得立体的体积；若区域面积等于 $\\frac43$，求 $a$ 与相应体积。\n\\end{supplement}\n\\begin{supplement}{6.1-2}{弧长与旋转曲面面积}\n曲线 $y=\\frac{x^2}{4}-\\frac12\\ln x$，$1\\le x\\le2$。求曲线弧长以及绕 $y$ 轴旋转所得曲面的面积，并写出所用弧长微元。\n\\end{supplement}\n\\subsection{定积分在物理学上的应用}\n\\begin{supplement}{6.2-1}{变力做功与动能定理}\n质量为 $m$ 的物体沿水平直线运动，阻力大小为 $kv^2$，其中 $k>0$、$v$ 为速率。物体仅受此阻力，从速率 $v_0>0$ 减至 $v_0/2$。利用 $mv\\dd v=-kv^2\\dd s$ 求此过程中的位移、阻力做功，并核验动能定理。\n\\end{supplement}\n\\begin{supplement}{6.2-2}{液体压力与水深参数}\n竖直薄板为底边水平的等腰三角形，高 $h$、底边长 $b$，顶点在底边上方。薄板顶点距水面 $d\\ge0$，水的密度为 $\\rho$。求单侧静水总压力 $P(d)$；若将薄板翻转使底边在上方且最高点仍在深度 $d$ 处，求压力变化量并解释其符号。\n\\end{supplement}\n"}

## tool · 2026-10-20T02:17:23Z




## tool · 2026-10-20T02:18:25Z


Wall time: 60.0077 seconds
Sleep completed.

## tool · 2026-10-20T02:18:28Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"d6f411","wall_time_seconds":0.000006667,"exit_code":0,"original_token_count":90,"output":"001.md\n002.md\n003.md\n004.md\n005.md\n006.md\n007.md\n008.md\n009.md\n010.md\n011.md\n012.md\n013.md\n014.md\n015.md\n016.md\n017.md\n018.md\n019.md\n020.md\n021.md\n022.md\n023.md\n024.md\n025.md\n026.md\n027.md\n028.md\n029.md\n030.md\n031.md\n032.md\n033.md\n034.md\n035.md\n036.md\n037.md\n038.md\n039.md\n040.md\n041.md\n042.md\n043.md\n044.md\n045.md\n046.md\n047.md\n048.md\n049.md\n050.md\n051.md\n"}
{"chunk_id":"c8ed9e","wall_time_seconds":0.000011209,"exit_code":0,"original_token_count":76,"output":"高等数学（上册）精选750题 (宋浩).pdf\noutput/工科数学分析逐题训练-上册/chapters/ch01.tex\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex\n"}

## tool · 2026-10-20T02:18:32Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"40908a","wall_time_seconds":0.000009084,"exit_code":1,"original_token_count":30,"output":"Traceback (most recent call last):\n  File \"<string>\", line 1, in <module>\nModuleNotFoundError: No module named 'sympy'\n"}
{"chunk_id":"384bc6","wall_time_seconds":0.000007,"exit_code":0,"original_token_count":26,"output":"check.py\nextract.swift\nipad-build\nsection-build\nsonghao\nsource-ocr.txt\nswift-cache\nverify_sections.py\n"}

## tool · 2026-10-20T02:18:35Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"c8edbd","wall_time_seconds":0.000011208,"exit_code":0,"original_token_count":191,"output":"import math\nimport re\nfrom pathlib import Path\n\nroot = Path(\"HDU/大一上数学分析备考\")\nchecks = 0\n\n\ndef near(actual, expected, tolerance=1e-7):\n    global checks\n    assert abs(actual - expected) <= tolerance * max(1, abs(expected)), (actual, expected)\n    checks += 1\n\n\ndef integral(f, a, b, n=2000):\n    step = (b - a) / n\n    return step / 3 * (\n        f(a) + f(b)\n        + 4 * sum(f(a + k * step) for k in range(1, n, 2))\n        + 2 * sum(f(a + k * step) for k in range(2, n, 2))\n    )\n\n\ndef derivative(f, x, h=1e-5):\n    return (f(x + h) - f(x - h)) / (2 * h)\n\n\nfor filename, marker in [(\"模拟试卷.tex\", \"\\\\paper{\"), (\"参考解析.tex\", \"\\\\answerpaper{\")]:\n    source = (root / filename).read_text()\n    sections = source.split(marker)[1:]\n"}
{"chunk_id":"4657af","wall_time_seconds":0.000008625,"exit_code":1,"original_token_count":11,"output":"zsh:1: no matches found: .venv/bin/python*\n"}

## tool · 2026-10-20T02:19:40Z


Wall time: 60.0098 seconds
Sleep completed.

## tool · 2026-10-20T02:19:42Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"0f2a00","wall_time_seconds":0.000010084,"exit_code":0,"original_token_count":11,"output":"058.md\n059.md\n060.md\n061.md\n062.md\n063.md\n"}

## tool · 2026-10-20T02:19:56Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"2a937b","wall_time_seconds":0.000028791,"exit_code":0,"original_token_count":1133,"output":"\\section{第7章 微分方程}\n\\subsection{微分方程的基本概念}\n\\begin{supplement}{7.1-1}{解族、奇解与初值唯一性}\n验证 $y=(x-C)^2$ 在 $x\\ge C$ 上满足 $y'=2\\sqrt y$，并验证 $y\\equiv0$ 也是解。对初值 $y(0)=0$，构造至少两个在 $[0,+\\infty)$ 上不同的解，说明直接分离变量可能遗漏什么解。\n\\end{supplement}\n\\begin{supplement}{7.1-2}{消去常数与微分方程阶数}\n消去曲线族 $y=C_1e^x+C_2e^{-x}+x$ 中的任意常数，建立二阶微分方程。再求该方程满足 $y(0)=1$、$y'(0)=0$ 的特解，并核验两个初始条件。\n\\end{supplement}\n\\subsection{可分离变量的微分方程}\n\\begin{supplement}{7.2-1}{平衡解与最大存在区间}\n求初值问题 $y'=y^2$、$y(0)=a$ 的解，包括 $a=0$ 的情形；分别确定 $a>0$ 与 $a<0$ 时包含 $0$ 的最大存在区间，并讨论 $x\\to+\\infty$ 时解是否有意义。\n\\end{supplement}\n\\begin{supplement}{7.2-2}{受限增长与阈值时间}\n种群满足 $N'=rN(1-N/K)$，其中 $r,K>0$、$N(0)=N_0\\in(0,K)$。求 $N(t)$，证明其单调增加且趋于 $K$；当 $N_0<K/2$ 时，求首次达到 $K/2$ 的时间。\n\\end{supplement}\n\\subsection{齐次方程}\n\\begin{supplement}{7.3-1}{齐次代换与不可跨越的奇点}\n求微分方程 $xy'=y+x e^{y/x}$ 在 $x>0$ 上满足 $y(1)=0$ 的解，并确定包含 $1$ 的最大存在区间。证明所得解无法在该区间右端连续延拓为有限值。\n\\end{supplement}\n\\begin{supplement}{7.3-2}{齐次方程与代换遗漏解}\n求 $xy'=y+y^2/x$ 在 $x>0$ 上的全部解，包括代换分离时可能遗漏的解；对初值 $y(1)=a$，确定解的表达式及包含 $1$ 的最大存在区间。\n\\end{supplement}\n\\subsection{一阶线性微分方程}\n\\begin{supplement}{7.4-1}{积分因子与有界解}\n求方程 $y'+2y=1+e^{-x}$ 的通解；确定在整个实轴上有界的解，并说明其唯一性。再求所有解在 $x\\to+\\infty$ 时的极限。\n\\end{supplement}\n\\begin{supplement}{7.4-2}{分段外力与连续拼接}\n某系统满足 $y'+y=u(x)$、$y(0)=0$，其中 $u(x)=1$（$0\\le x<1$）、$u(x)=0$（$x>1$）。分别求两个区间上的解，使 $y$ 在 $x=1$ 连续；判断 $y$ 在 $x=1$ 是否可导，并说明理由。\n\\end{supplement}\n\\subsection{可降阶的高阶微分方程}\n\\begin{supplement}{7.5-1}{不显含因变量的降阶}\n求初值问题 $xy''+y'=x$、$y(1)=0$、$y'(1)=1$ 在 $x>0$ 上的解，判断该解能否以二阶可导方式延拓到 $x=0$，并给出依据。\n\\end{supplement}\n\\begin{supplement}{7.5-2}{不显含自变量与能量积分}\n设 $y''=-y^3$、$y(0)=a>0$、$y'(0)=0$。通过降阶证明 $\\frac12(y')^2+\\frac14y^4=\\frac14a^4$；在解首次降到 $0$ 之前确定 $y'$ 的符号，并用定积分表示首次到达 $0$ 的时间，证明该时间有限。\n\\end{supplement}\n\\subsection{高阶线性微分方程}\n\\begin{supplement}{7.6-1}{解的叠加与初始条件}\n设 $y_1,y_2$ 是方程 $y''+p(x)y'+q(x)y=f(x)$ 的两个解。证明 $\\alpha y_1+(1-\\alpha)y_2$ 仍为解，并说明一般线性组合成为解所需的条件。取 $f\\not\\equiv0$ 时，判断 $y_1+y_2$ 与 $y_1-y_2$ 分别满足什么方程。\n\\end{supplement}\n\\begin{supplement}{7.6-2}{已知解降阶与基本解组}\n已知 $y_1=x$ 是 $x^2y''-2xy'+2y=0$ 在 $x>0$ 上的解。令 $y=xv(x)$ 求通解，证明所得两解线性无关，并求满足 $y(1)=0$、$y'(1)=1$ 的解。\n\\end{supplement}\n\\subsection{常系数齐次线性微分方程}\n\\begin{supplement}{7.7-1}{重根、参数与长期行为}\n求初值问题 $y''+2ay'+a^2y=0$、$y(0)=0$、$y'(0)=1$ 的解。讨论实参数 $a$ 使解在 $[0,+\\infty)$ 上有界或趋于零的条件，并在 $a>0$ 时求其最大值。\n\\end{supplement}\n\\begin{supplement}{7.7-2}{阻尼分类与无零点条件}\n考虑 $y''+2\\zeta y'+y=0$，$y(0)=1$、$y'(0)=0$，其中 $\\zeta\\ge0$。分别求 $0\\le\\zeta<1$、$\\zeta=1$、$\\zeta>1$ 时的解，并确定解在 $x>0$ 上始终为正的参数范围。\n\\end{supplement}\n\\subsection{常系数非齐次线性微分方程}\n\\begin{supplement}{7.8-1}{共振与参数分类}\n对 $\\omega>0$，求初值问题 $y''+y=\\cos\\omega x$、$y(0)=y'(0)=0$ 的解，分别讨论 $\\omega\\ne1$ 与 $\\omega=1$。判断解有界的参数条件，并说明共振时无界项的来源。\n\\end{supplement}\n\\begin{supplement}{7.8-2}{指数多项式外力与特解形式}\n求 $y''-2y'+y=e^x(x+1)$ 的通解及满足 $y(0)=y'(0)=0$ 的特解。先写出待定系数法所需的特解形式，并用 $y=e^xv$ 的代换核验计算结果。\n\\end{supplement}\n"}

## tool · 2026-10-20T02:20:02Z


Script completed
Wall time 0.1 seconds
Output:

{}
{"chunk_id":"cd637b","wall_time_seconds":0.000010708,"exit_code":0,"original_token_count":11,"output":"060.md\n061.md\n062.md\n063.md\n064.md\n065.md\n"}

## tool · 2026-10-20T02:21:04Z


Wall time: 60.0070 seconds
Sleep completed.

## tool · 2026-10-20T02:21:10Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"dd1903","wall_time_seconds":0.000010625,"exit_code":0,"original_token_count":11,"output":"070.md\n071.md\n072.md\n073.md\n074.md\n075.md\n"}

## tool · 2026-10-20T02:21:28Z


Wall time: 15.0064 seconds
Sleep completed.

## tool · 2026-10-20T02:21:31Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"b640a7","wall_time_seconds":0.000008667,"exit_code":0,"original_token_count":918,"output":"第一节 定积分的概念与性质\n\n一、定积分的定义\n\n定义：若函数 $f(x)$ 在闭区间 $[a,b]$ 上有定义，且 $a=x_0<x_1<x_2<\\cdots<x_n=b$，\n则 $\\int_a^b f(x)dx=\\lim_{\\lambda\\rightarrow 0}\\sum_{i=1}^n f(\\xi_i)\\Delta x_i$ （其中 $x_{i-1}<\\xi_i<\\Delta x_i=x_i-x_{i-1},\\lambda=\\max_{\\|x_i-\\|} \\Delta x_i$）\n称为函数 $f(x)$ 在区间 $[a,b]$ 上的定积分.\n\n几何意义：若连续函数 $f(x)\\geq 0$，定积分 $\\int_a^b f(x)dx$ 表示由曲线 $y=f(x)$，直线\n$x=a$，$x=b(a<b)$ 以及 $x$ 轴所围成的曲边梯形面积 $S$. 即 $S=\\int_a^b f(x)dx$.\n\n二、定积分的性质\n\n规定：(1) $\\int_a^b f(x)dx=0$；(2) $\\int_a^b f(x)dx=-\\int_a^b f(x)dx$.\n\n性质 1：（线性性质）$\\int_a^b [a f(x)+\\beta g(x)]dx=\\alpha \\int_a^b f(x)dx+\\beta \\int_a^b g(x)dx$. ($\\alpha,\\beta$均为常数).\n\n性质 2：（区间可加性）$\\int_a^b f(x)dx=\\int_a^c f(x)dx+\\int_a^b f(x)dx$.\n\n性质 3：$\\int_a^b dx=\\int_a^b dx=b-a$.\n\n性质 4：若 $f(x)\\geq 0$，$x\\in [a,b]$，则 $\\int_a^b f(x)dx\\geq 0$.\n\n推论 1：（比较性质）若 $f(x)\\leq g(x)$，$x\\in [a,b]$，则 $\\int_a^b f(x)dx\\leq \\int_a^b g(x)dx$.\n\n推论 2：$\\int_a^b f(x)dx\\leq \\int_a^b f(x)dx$.\n\n性质 5：（估值定理）设 $M$ 和 $m$ 是 $f(x)$ 在区间 $[a,b]$ 上的最大值与最小值，则\n$m(b-a)\\leq \\int_a^b f(x)dx\\leq M(b-a)$.\n\n性质 6：（中值定理）设函数 $f(x)$ 在区间 $[a,b]$ 上连续，则在 $[a,b]$ 上至少存在一个点 $\\xi$，使得 $\\int_a^b f(x)dx=f(\\xi)(b-a)$.\n\n$f(\\xi)=\\frac{1}{(b-a)}\\int_a^b f(x)dx$ 称为函数 $f(x)$ 在区间 $[a,b]$ 上的平均值.\n\n505 基础题 $\\int_a^b \\arcsin xdx^2=(\\quad)$.\n\n(A)arcsinx (B)0 (C) $\\frac{1}{\\sqrt{1-b^2}}-\\frac{1}{\\sqrt{1-a^2}}$ (D) $\\frac{1}{\\sqrt{1-x^2}}$506 基础题 利用定积分的几何意义，求 $ \\int_{-2}^{2} \\sqrt{4-x^2} \\, \\mathrm{d}x $ .\n\n507 基础题 利用定积分的定义，求极限 $ \\lim_{n \\to \\infty} \\left( \\frac{1}{n^2} + \\frac{2}{n^2} + \\cdots + \\frac{n-1}{n^2} \\right) $ .\n\n508 基础题 利用定积分的定义，求极限 $ \\lim_{n \\to \\infty} \\left( \\frac{1}{n+1} + \\frac{1}{n+2} + \\cdots + \\frac{1}{n+n} \\right) $ .\n\n509 基础题 利用定积分的定义，求极限 $ \\lim_{n \\to \\infty} \\left( \\frac{n}{n^2+1^2} + \\frac{n}{n^2+2^2} + \\cdots + \\frac{n}{n^2+n^2} \\right) $ .\n\n510 基础题 下列各选项中满足 $ I_1 \\leqslant I_2 $的是（    ）.\n(A) $ I_1 = \\int_0^1 x^2 \\, \\mathrm{d}x $ (B) $ I_1 = \\int_0^1 x \\, \\mathrm{d}x $ (C) $ I_1 = \\int_1^2 \\ln x \\, \\mathrm{d}x $ (D) $ I_1 = \\int_0^1 e^x \\, \\mathrm{d}x $ (E) $ I_1 = \\int_0^1 (1+x) \\, \\mathrm{d}x $\n\n511 基础题 设 $ I_1 = \\int_0^1 \\sqrt{1+x^2} \\, \\mathrm{d}x $ $ I_2 = \\int_0^1 \\sqrt{1+x^2} \\, \\mathrm{d}x $ ，则 $ I_1 $与 $ I_2 $的大小关系是（    ）.\n(A) $ I_1 > I_2 $ (B) $ I_1 \\geqslant I_2 $ (C) $ I_1 < I_2 $ (D) $ I_1 \\leqslant I_2 $\n\n512 基础题 估计定积分 $ I = \\int_0^\\pi (1+\\cos^2 x) \\, \\mathrm{d}x $的值.\n\n513 中等题 估计定积分 $ I = \\int_0^\\pi \\frac{x^9}{\\sqrt{1+x}} \\, \\mathrm{d}x $的值.\n\n514 综合题 设 $ I = \\int_0^\\pi \\frac{\\sin x}{x} \\, \\mathrm{d}x $，证明 $ \\frac{\\sqrt{2}}{4} \\leqslant I \\leqslant \\frac{\\sqrt{2}}{2} $.\n\n515 中等题 设 $ f(x) $在 $ [a,b] $上连续，在 $ (a,b) $内可导，且 $ \\frac{2}{b-a} \\int_a^b f(x) \\, \\mathrm{d}x = f(b) $证明在 $ (a,b) $内至少存在一点 $ \\xi $，使得 $ f'(\\xi) = 0 $.\n\n516 中等题 设 $ f(x) $在 $ [a,b] $上连续，在 $ (a,b) $内可导，且 $ f'(x) \\leqslant 0 $证明 $ F(x) = \\frac{1}{x-a} \\int_a^x f(t) \\, \\mathrm{d}t $在 $ (a,b) $内满足 $ F'(x) \\leqslant 0 $.\n\n517 基础题 求函数 $ f(x) = \\sqrt{4-x^2} $在 $ [-2,2] $上的平均值."}

## tool · 2026-10-20T02:21:41Z




## tool · 2026-10-20T02:21:53Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"831663","wall_time_seconds":0.000013792,"exit_code":0,"original_token_count":554,"output":"\\section{第5章 定积分}\n\\subsection{定积分的概念与性质}\n\\begin{supplement}{5.1-1}{积分定义与黎曼和}\n设 $f$ 在 $[0,1]$ 上连续。用定积分表示极限\n\\[\n\\lim_{n\\to\\infty}\\sum_{k=1}^n\\frac{n}{n^2+k^2}f\\!\\left(\\frac{k}{n}\\right).\n\\]\n当 $f(x)=x$ 时求极限值；当 $f(x)\\ge0$ 且上述极限为零时，证明 $f\\equiv0$。\n\\end{supplement}\n\\begin{supplement}{5.1-2}{积分不等式与等号条件}\n设 $f$ 在 $[0,1]$ 上连续，且 $0\\le f(x)\\le1$、$\\int_0^1f(x)\\dd x=\\frac12$。证明\n\\[\n\\frac14\\le\\int_0^1f^2(x)\\dd x<\\frac12,\n\\]\n并完整讨论左端等号条件及右端不能取等号的原因。\n\\end{supplement}\n\\subsection{微积分基本公式}\n\\begin{supplement}{5.2-1}{变限积分与极值}\n设 $F(x)=\\int_0^x(t^2-1)e^{-t}\\dd t$，$x\\ge0$。求 $F$ 的单调区间与极值，并计算 $\\lim_{x\\to\\infty}F(x)$；由此确定 $F$ 在 $[0,+\\infty)$ 上的零点个数。\n\\end{supplement}\n\\begin{supplement}{5.2-2}{积分方程与条件恢复}\n设连续函数 $f$ 满足\n\\[\nf(x)=1+\\int_0^x(x-t)f(t)\\dd t\\qquad(x\\in\\mathbb R).\n\\]\n证明 $f$ 二阶可导，求 $f$；再直接代回积分等式核验。\n\\end{supplement}\n\\subsection{定积分的换元积分法和分部积分法}\n\\begin{supplement}{5.3-1}{对称换元与参数积分}\n对 $a>0$，计算\n\\[\nI(a)=\\int_0^{\\pi/2}\\frac{\\sin x}{\\sin x+a\\cos x}\\dd x.\n\\]\n利用 $x\\mapsto\\frac\\pi2-x$ 建立 $I(a)$ 与 $I(1/a)$ 的关系，并单独处理 $a=1$ 的情形。\n\\end{supplement}\n\\begin{supplement}{5.3-2}{分部积分与递推估计}\n记 $I_n=\\int_0^1x^ne^x\\dd x$，$n=0,1,2,\\ldots$。建立 $I_n$ 的递推关系，求 $I_3$，并证明 $\\lim_{n\\to\\infty}(n+1)I_n=e$。\n\\end{supplement}\n\\subsection{反常积分}\n\\begin{supplement}{5.4-1}{双端瑕点与参数判敛}\n对实数 $p,q$，讨论反常积分\n\\[\n\\int_0^1\\frac{\\dd x}{x^p(1-x)^q}\n\\]\n的敛散性，并在 $p=q=\\frac12$ 时计算其值。说明为何必须分别考察两个端点。\n\\end{supplement}\n\\begin{supplement}{5.4-2}{对数因子与临界指数}\n讨论 $\\int_e^{+\\infty}\\frac{\\dd x}{x(\\ln x)^p}$ 与 $\\int_0^{1/e}\\frac{\\dd x}{x|\\ln x|^p}$ 随实参数 $p$ 的敛散性；收敛时分别求值，并用换元解释二者的联系。\n\\end{supplement}\n"}
{"chunk_id":"a4b337","wall_time_seconds":0.000017333,"exit_code":0,"original_token_count":778,"output":"第二节 微积分基本公式\n\n一、积分上限函数及其导数\n\n设函数 $f(x)$ 在区间 $[a,b]$ 上可积，则称\n$$\\Phi(x) = \\int_{a}^{x} f(t) \\mathrm{d}t, x \\in [a,b]$$\n为积分上限函数或变上限积分函数.\n\n定理 1: 如果函数 $f(x)$ 在区间 $[a,b]$ 上连续，则积分上限函数 $\\Phi(x) = \\int_{a}^{x} f(t) \\mathrm{d}t$\n在 $[a,b]$ 上可导，并且\n$$\\Phi'(x) = \\frac{d}{dx} \\int_{a}^{x} f(t) \\mathrm{d}t = f(x), x \\in [a,b].$$\n\n定理 2: （原函数存在定理）如果函数 $f(x)$ 在区间 $[a,b]$ 上连续，则函数\n$$\\Phi(x) = \\int_{a}^{x} f(t) \\mathrm{d}t$$ 是 $f(x)$ 在 $[a,b]$ 上的一个原函数.\n\n518 基础题 设 $f(x) = \\int_{a}^{x} \\sin x^{2} \\mathrm{d}x$ ，求 $\\frac{df}{dx}, \\frac{df}{db}, \\frac{df}{da}$.\n\n519 基础题 设 $y = \\int_{0}^{x} \\sqrt{1+t^{2}} \\mathrm{d}t$ ，求 $\\frac{dy}{dx}$.\n\n520 基础题 设 $y = \\int_{x}^{x^{2}} \\frac{\\mathrm{d}t}{\\sqrt{1+t^{2}}}$ ，求 $\\frac{dy}{dx}$.\n\n521 中等题 求极限 $\\lim_{x \\to 0} \\frac{\\int_{0}^{x} \\cos t^{2} \\mathrm{d}t}{x}$.\n\n522 中等题 求极限 $\\lim_{x \\to 0} \\frac{\\int_{0}^{x} \\arctan t \\mathrm{d}t}{x^{2}}.$\n\n523 中等题 求极限 $\\lim_{x \\to 0} \\frac{\\left(\\int_{0}^{x} \\mathrm{e}^{2 t} \\mathrm{d}t\\right)^{2}}{\\int_{0}^{x} t \\mathrm{e}^{2 t} \\mathrm{d}t}$.\n\n524 中等题 求极限 $\\lim_{x \\to 0} \\frac{\\int_{0}^{x} f(t)(x-t) \\mathrm{d}t}{x^{2}}$ ，其中 $f(x)$ 是 $(-\\infty, +\\infty)$ 内的连续函数.\n\n525 中等题 求极限 $\\lim_{x \\to +\\infty} \\frac{\\int_{0}^{x} \\left(\\arctan t\\right)^{2} \\mathrm{d}t}{\\sqrt{1+x^{2}}}$.526 基础题 求由 $\\int_0^y e^x \\mathrm{d}t + \\int_0^x \\cos t \\mathrm{d}t = 0$ 所确定的隐函数的导数 $\\frac{dy}{dx}$.\n\n527 中等题 设函数 $f(x) = \\int_0^x e^{-\\frac{1}{2}} \\mathrm{d}t (-\\infty < x < +\\infty)$，求 $f(x)$ 的单调区间，并判断其奇偶性.\n\n528 中等题 设函数 $f(x)$ 连续，$\\varphi(x) = \\int_0^x xf(t) \\mathrm{d}t$，若 $\\varphi(1) = 1$，$\\varphi(1) = 5$，求 $f(1)$.\n\n529 综合题 设函数 $f(x)$ 在 $[a, b]$ 上连续，且 $f(x) > 0$.\n证明方程 $\\int_0^x f(t) \\mathrm{d}t + \\int_0^x \\frac{dt}{f(t)} = 0$ 在区间 $(a, b)$ 内有且仅有一个实根.\n\n二、牛顿 - 莱布尼茨公式\n\n定理 3:（微积分基本定理）如果函数 $F(x)$ 是连续函数 $f(x)$ 在区间 $[a, b]$ 上的一个原函数，则\n$$\\int_0^b f(x) \\mathrm{d}x = F(x)\\int_0^b = F(b) - F(a).$$\n此为牛顿 - 莱布尼茨公式，也称微积分基本公式.\n\n530 基础题 求定积分 $\\int_0^1 \\frac{1}{2} e^{2x} \\mathrm{d}x$.\n\n531 基础题 求定积分 $\\int_0^2 \\frac{x}{\\sqrt{1+x^2}} \\mathrm{d}x$.\n\n532 基础题 求定积分 $\\int_0^1 \\frac{dx}{x^2 + 5x + 6}$.\n\n533 基础题 求定积分 $\\int_0^3 |2-x| \\mathrm{d}x$.\n\n534 基础题 求定积分 $\\int_0^{2\\pi} |\\sin x| \\mathrm{d}x$.\n\n535 中等题 设 $f(x) = \\begin{cases} 2x, & 0 \\leq x \\leq 1 \\\\ 2+x, & 1 < x \\leq 2 \\end{cases}$，求积分上限函数 $P(x) = \\int_0^x f(t) \\mathrm{d}t$ 在 $[0, 2]$ 上的表达式.\n\n536 中等题 设 $f(x) = \\frac{1}{1+x^2} + \\sqrt{1-x^2} \\int_0^1 f(x) \\mathrm{d}x$，求 $\\int_0^1 f(x) \\mathrm{d}x$."}

## tool · 2026-10-20T02:22:02Z




## tool · 2026-10-20T02:22:44Z


Script completed
Wall time 0.1 seconds
Output:

{}

## tool · 2026-10-20T02:22:48Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"5818c8","wall_time_seconds":0.000016917,"exit_code":0,"original_token_count":1097,"output":"537 中等题 设 $f(x)$ 在 $[0,1]$ 上连续，且满足 $f(x)=x\\int_{0}^{1}f(t)dt-1$，求 $\\int_{0}^{1}f(x)dx$ 及 $f(x)$.\n\n538 中等题 设 $f\\left(x+\\frac{1}{x}\\right)=\\frac{x+x^{3}}{1+x^{4}}$，求 $\\int_{2}^{2\\sqrt{2}}f(x)dx$.\n\n## 第三节 定积分的换元积分法和分部积分法\n\n### 一、定积分的换元积分法\n\n#### 定理 1：设函数 $f(x)$ 在区间 $[a,b]$ 上连续，若函数 $x=\\varphi(t)$ 满足条件：\n(1) $\\varphi(a)=a$，$\\varphi(\\beta)=b$；\n(2) $\\varphi(t)$ 在区间 $[a,\\beta]$ （或 $[\\beta,a]$）上单调且具有连续导数，\n则 $\\int_{a}^{b}f(x)dx=\\int_{a}^{b}f[\\varphi(t)]\\varphi'(t)dt$.\n\n#### 常用公式\n(1) 设函数 $f(x)$ 在区间 $[-a,a]$ 上连续，则\n$$\\int_{-a}^{a}f(x)dx=\\int_{0}^{a}[f(x)+f(-x)]dx=\\left\\{ \\begin{array}{ll}0&\\text{当 }f(x)\\text{ 为奇函数时} \\\\ 2\\int_{0}^{a}f(x)dx&\\text{当 }f(x)\\text{ 为偶函数时} \\end{array} \\right.$$\n(2) 设函数 $f(x)$ 是以 $T$ 为周期的连续函数，则\n$$\\int_{a}^{a+T}f(x)dx=\\int_{0}^{T}f(x)dx;\\int_{a}^{a+T}f(x)dx=\\int_{-a}^{a+T}f(x)dx.$$\n\n539 基础题 计算 $\\int_{4}^{9}\\frac{\\sqrt{x}}{\\sqrt{x}-1}dx$.\n\n540 基础题 计算 $\\int_{0}^{1}x\\sqrt{3-2x}dx$.\n\n541 基础题 计算 $\\int_{1}^{0}\\frac{1}{x\\sqrt{1+\\ln x}}dx$.\n\n542 中等题 计算 $\\int_{-1}^{0}\\frac{(1+x)e^{x}}{\\sqrt{1+xe^{x}}}dx$.\n\n543 基础题 计算 $\\int_{0}^{\\frac{\\sqrt{2}}{3}}\\sqrt{2-9x^{2}}dx$.\n\n544 基础题 计算 $\\int_{1}^{\\sqrt{2}}\\frac{dx}{x\\sqrt{1+x^{2}}}$.545 基础题 计算 $\\int_{1}^{2} \\frac{\\sqrt{x^2-1}}{x} \\mathrm{d}x$.\n\n546 基础题 计算 $\\int_{-1}^{1} \\frac{\\mathrm{d}x}{1+\\sqrt{x^2}}$.\n\n547 基础题 计算 $\\int_{0}^{1} \\sqrt{2x-x^2} \\mathrm{d}x$.\n\n548 中等题 计算 $\\int_{0}^{-2 \\ln 2} \\sqrt{1-e^{2x}} \\mathrm{d}x$.\n\n549 中等题 设 $f(x) = \\left\\{ \\begin{array}{l l} 1+x^2, & x<0 \\\\ \\mathrm{e}^{-x}, & x \\geqslant 0 \\end{array} \\right.$, 求 $\\int_{1}^{3} f(x-2) \\mathrm{d}x$.\n\n550 中等题 设 $f(x) = \\left\\{ \\begin{array}{l l} x \\mathrm{e}^{x}, & -\\frac{1}{2} \\leqslant x \\leqslant \\frac{1}{2} \\\\ -1, & x \\geqslant \\frac{1}{2} \\end{array} \\right.$, 求 $\\int_{1}^{2} f(x-1) \\mathrm{d}x$.\n\n551 中等题 设连续函数 $f(x)$ 满足 $\\int_{0}^{x} f(x-t) \\mathrm{d}t = \\mathrm{e}^{-2x}-1$, 求定积分 $\\int_{0}^{1} f(x) \\mathrm{d}x$.\n\n552 综合题 设 $f(x)$ 是 $(-\\infty, +\\infty)$ 内的连续函数, 且满足 $\\int_{0}^{x} f(x-t) t \\mathrm{d}t = \\mathrm{e}^{x}-x-1$, 求 $f(x)$.\n\n553 基础题 计算 $\\int_{\\frac{\\pi}{2}}^{\\frac{\\pi}{2}} \\frac{x}{1+\\cos x} \\mathrm{d}x$.\n\n554 基础题 计算 $\\int_{\\frac{\\pi}{2}}^{\\frac{\\pi}{2}} \\sin^2 x \\ln \\left(x+\\sqrt{1+x^2}\\right) \\mathrm{d}x$.\n\n555 中等题 计算 $\\int_{-1}^{1} \\frac{1}{\\sqrt{4-x^2}} \\left(\\frac{1}{1+\\mathrm{e}^{x}}-\\frac{1}{2}\\right) \\mathrm{d}x$.\n\n556 中等题 求 $\\int_{-1}^{1} \\cos x \\arccos x \\mathrm{d}x$.\n\n557 综合题 设 $M = \\int_{\\frac{\\pi}{4}}^{\\frac{\\pi}{4}} \\left(\\frac{\\tan x}{1+x^2}+x^2\\right) \\mathrm{d}x$, $N = \\int_{\\frac{\\pi}{4}}^{\\frac{\\pi}{4}} \\left(\\sin^2 x+\\ln(x+\\sqrt{x^2}+1)\\right) \\mathrm{d}x$, $P = \\int_{\\frac{\\pi}{4}}^{\\frac{\\pi}{4}} \\left(\\tan^8 x+e^x \\cos x-e^{-x} \\cos x\\right) \\mathrm{d}x$, 则有 (    ).\n\n(A) $P > N > M$ (B) $N > P > M$ (C) $N > M > P$ (D) $P > M > N$558 中等题 计算 $\\int_{0}^{n \\pi} \\sqrt{1 - \\sin^2 x} dx$.\n\n559 中等题 计算 $\\int_{a}^{n + n} \\sin^2 x (\\tan x + 1) dx$.\n\n560 综合题 设 $f(x)$ 为连续函数，证明 (1) $\\int_{0}^{\\frac{\\pi}{2}} f(\\sin x) dx = \\int_{0}^{\\frac{\\pi}{2}} f(\\cos x) dx$；\n(2) $\\int_{0}^{\\pi} x f(\\sin x) dx = \\pi \\int_{0}^{\\frac{\\pi}{2}} f(\\sin x) dx$，并由此计算定积分\n$I_n = \\int_{0}^{\\pi} \\frac{x \\sin^2 x}{\\sin^2 x + \\cos^2 x} dx$ ($n$ 为正整数).\n\n二、定积分的分部分法\n\n定理 2: 设 $u = u(x), v = v(x)$ 在区间 $[a, b]$ 上连续可导，则\n$\\int_{a}^{b} u v' dx = u v_{a}^{b} - \\int_{a}^{b} u' v dx$ 或 $\\int_{a}^{b} u dv = u v_{a}^{b} - \\int_{a}^{b} v du$.\n\n561 基础题 计算 $\\int_{0}^{1} \\ln(1 + x^2) dx$.\n\n562 基础题 计算 $\\int_{a}^{1} \\arcsin x dx$.\n\n563 基础题 计算 $\\int_{-1}^{1} x \\arccos x dx$.\n\n564 中等题 计算 $\\int_{0}^{1} \\frac{\\ln(1 + x)}{(2 - x)^2} dx$.\n\n565 中等题 计算 $\\int_{0}^{2} e^{-x} \\sin(2x) dx$.\n\n566 中等题 计算 $\\int_{0}^{1} e^{-\\sqrt{x}} dx$.\n\n567 中等题 计算 $\\int_{0}^{1} \\frac{x^2 \\arcsin x}{\\sqrt{1 - x^2}} dx$.\n\n568 中等题 计算 $\\int_{1}^{16} \\arctan \\sqrt{x - 1} dx$."}

## tool · 2026-10-20T02:23:00Z




## tool · 2026-10-20T02:23:18Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"9ecd2d","wall_time_seconds":0.000019167,"exit_code":0,"original_token_count":214,"output":"2:\\subsection{定积分的概念与性质}\n28:\\begin{supplement}{5.1-1}{积分定义与黎曼和}\n34:\\end{supplement}\n35:\\begin{supplement}{5.1-2}{积分不等式与等号条件}\n41:\\end{supplement}\n42:\\subsection{微积分基本公式}\n86:\\begin{problem}{536}{79}{积分方程与自洽条件}\n89:\\begin{supplement}{5.2-1}{变限积分与极值}\n91:\\end{supplement}\n92:\\begin{supplement}{5.2-2}{积分方程与条件恢复}\n98:\\end{supplement}\n99:\\subsection{定积分的换元积分法和分部积分法}\n100:\\begin{supplement}{5.3-1}{对称换元与参数积分}\n106:\\end{supplement}\n107:\\begin{supplement}{5.3-2}{分部积分与递推估计}\n109:\\end{supplement}\n110:\\subsection{反常积分}\n111:\\begin{supplement}{5.4-1}{双端瑕点与参数判敛}\n117:\\end{supplement}\n118:\\begin{supplement}{5.4-2}{对数因子与临界指数}\n120:\\end{supplement}\n"}
{"chunk_id":"e3a7d2","wall_time_seconds":0.00001025,"exit_code":0,"original_token_count":1815,"output":"第四节 反常积分\n\n一、无穷限的反常积分\n\n定义 1: 设 $f(x)$ 在 $[a, +\\infty)$ 上有定义，且在任意有界区间 $[a, b]$ 上存在定积\n分 $\\int_{a}^{b} f(x) \\mathrm{d}x$，定义\n\n$$\\int_{a}^{+\\infty} f(x) \\mathrm{d}x = \\lim_{b \\to +\\infty} \\int_{a}^{b} f(x) \\mathrm{d}x$$\n\n定义 2: 设 $f(x)$ 在 $(-\\infty, b]$ 上有定义，且在任意有界区间 $[a, b]$ 上存在定积\n分 $\\int_{a}^{b} f(x) \\mathrm{d}x$，定义\n\n$$\\int_{a}^{+\\infty} f(x) \\mathrm{d}x = \\lim_{b \\to +\\infty} \\int_{a}^{b} f(x) \\mathrm{d}x$$\n\n定义 3: 设 $f(x)$ 在 $(-\\infty, +\\infty)$ 上有定义，定义\n\n$$\\int_{-\\infty}^{+\\infty} f(x) \\mathrm{d}x = \\int_{-\\infty}^{+\\infty} f(x) \\mathrm{d}x + \\int_{0}^{+\\infty} f(x) \\mathrm{d}x = \\lim_{b \\to +\\infty} \\int_{a}^{b} f(x) \\mathrm{d}x + \\lim_{b \\to +\\infty} \\int_{a}^{b} f(x) \\mathrm{d}x$$定义 1 和定义 2 中若右端极限存在，则称该反常积分收敛，否则称为发散；\n定义 3 中要求右端的两个反常积分都收敛，则 $\\int_{-\\infty}^{\\infty} f(x) \\mathrm{d}x$ 收敛。有一个发散，则\n$\\int_{-\\infty}^{\\infty} f(x) \\mathrm{d}x$ 发散.\n\n二、无穷限积分的性质\n\n性质 1: $\\int_{a}^{\\infty} f(x) \\mathrm{d}x$ 与 $\\int_{a}^{\\infty} f(x) \\mathrm{d}x$ 具有相同的敛散性.\n\n性质 2: $\\int_{a}^{\\infty} k f(x) \\mathrm{d}x$ ($k \\neq 0$ 为常数) 与 $\\int_{a}^{\\infty} f(x) \\mathrm{d}x$ 具有相同的敛散性.\n\n性质 3: 若 $\\int_{a}^{\\infty} f(x) \\mathrm{d}x$ 与 $\\int_{a}^{\\infty} g(x) \\mathrm{d}x$ 均收敛，则 $\\int_{a}^{\\infty} [f(x) \\pm g(x)] \\mathrm{d}x$ 收敛，且\n$\\int_{a}^{\\infty} [f(x) \\pm g(x)] \\mathrm{d}x = \\int_{a}^{\\infty} f(x) \\mathrm{d}x \\pm \\int_{a}^{\\infty} g(x) \\mathrm{d}x$.\n\n常用结论: $\\int_{a}^{\\infty} \\frac{\\mathrm{d}x}{x^{p}} \\left\\{p > 1\\right\\}$ 收敛 ($p \\leqslant 1$，发散 ($a > 0$)；$\\int_{a}^{\\infty} \\frac{\\mathrm{d}x}{x \\ln^{2} x} \\left\\{p > 1\\right\\}$ 收敛 ($p \\leqslant 1$，发散 ($a > 1$)).\n\n在实际计算中，反常积分可按照定积分 $\\int_{a}^{\\infty} f(x) \\mathrm{d}x = F(x)^{n}$ 的计算方法进行，只不过要将 $F(b)$ 或 $F(a)$ 改作 $\\lim_{x \\to +\\infty} f(x)$ 或 $\\lim_{x \\to -\\infty} f(x)$ 即可。定积分的换元法和分部积分法在反常积分的计算中也适用.\n\n三、无穷限积分敛散性的判别\n\n比较判别法：设 $0 \\leqslant f(x) \\leqslant g(x)$，则有：\n(1) 当 $\\int_{a}^{\\infty} g(x) \\mathrm{d}x$ 收敛时，$\\int_{a}^{\\infty} f(x) \\mathrm{d}x$ 收敛；\n(2) 当 $\\int_{a}^{\\infty} f(x) \\mathrm{d}x$ 发散时，$\\int_{a}^{\\infty} g(x) \\mathrm{d}x$ 发散.\n\n578 基础题 下列反常积分中收敛的是（ ）。\n(A) $\\int_{a}^{\\infty} \\frac{1}{\\sqrt{x}} \\mathrm{d}x$ (B) $\\int_{a}^{\\infty} \\frac{\\ln x}{x} \\mathrm{d}x$ (C) $\\int_{a}^{\\infty} \\frac{1}{x \\ln x} \\mathrm{d}x$ (D) $\\int_{a}^{\\infty} \\frac{x}{e^{x}} \\mathrm{d}x$\n\n579 基础题 计算 $\\int_{2}^{\\infty} \\frac{1}{x \\ln^{2} x} \\mathrm{d}x$.\n\n580 基础题 计算 $\\int_{-\\infty}^{\\infty} \\frac{1}{x^{2}+4x+5} \\mathrm{d}x$.\n\n581 基础题 计算 $\\int_{1}^{\\infty} \\frac{\\mathrm{d}x}{x^{2}+x}$.\n\n582 中等题 计算 $\\int_{3}^{\\infty} \\frac{1}{(x-1)^{4} \\sqrt{x^{2}-2x}} \\mathrm{d}x$.\n\n583 基础题 计算 $\\int_{-\\infty}^{\\infty} \\frac{e^{x}}{1+e^{2x}} \\mathrm{d}x$.584 中等题 计算 $\\int_{0}^{+\\infty} \\min \\left\\{e^{-x}, \\frac{1}{2}\\right\\} dx$.\n\n585 中等题 计算 $\\int_{1}^{+\\infty} \\frac{\\ln x}{(1+x)^{2}} dx$.\n\n586 中等题 计算 $\\int_{0}^{+\\infty} \\frac{1}{(1+x^{2})^{2}} dx$.\n\n587 中等题 计算 $\\int_{1}^{+\\infty} \\frac{dx}{x\\sqrt{2x^{2}-1}}$.\n\n588 综合题 计算 $\\int_{0}^{+\\infty} \\frac{x e^{-x}}{(1+e^{-x})^{2}} dx$.\n\n589 中等题 关于 $\\int_{-\\infty}^{+\\infty} \\sin(2x) \\cdot e^{i x} dx$，下列结论正确的是（    ）.\n(A) 取值为 0 (B) 取正值 (C) 发散 (D) 取负值\n\n590 基础题 判别 $\\int_{2}^{+\\infty} \\frac{1}{\\ln x} dx$ 的敛散性.\n\n591 中等题 判别 $\\int_{0}^{+\\infty} e^{-x^{2}} dx$ 的敛散性.\n\n592 综合题 求 $c$ 的值，使 $\\lim_{x \\to \\infty} \\left( \\frac{x+c}{x-c} \\right)^{x} = \\int_{-\\infty}^{c} t e^{2 x} d t$.\n\n四、无界函数的反常积分\n\n如果函数 $f(x)$ 在点 $x=x_{0}$ 的任一邻域内都无界，则称点 $x=x_{0}$ 为函数 $f(x)$ 的瑕点，无界函数的反常积分又称为瑕积分.\n\n定义1：设 $f(x)$ 在 $(a, b]$ 上有定义，且在任一区间 $[a+\\varepsilon, b]$ 上可积，其中 $\\varepsilon>0$，\n且 $\\lim_{x \\to a^{+}} f(x)=\\infty$，定义\n\n$$\\int_{a}^{b} f(x) dx = \\lim_{\\varepsilon \\to 0} \\int_{a+\\varepsilon}^{b} f(x) dx$$\n\n定义2：设 $f(x)$ 在 $(a, b)$ 上有定义，且在任一区间 $[a, b-\\varepsilon]$ 上可积，其中 $\\varepsilon>0$，\n且 $\\lim_{x \\to b^{+}} f(x)=\\infty$，定义\n\n$$\\int_{a}^{b} f(x) dx = \\lim_{\\varepsilon \\to 0} \\int_{b+\\varepsilon}^{b-\\varepsilon} f(x) dx$$\n\n定义3：设 $f(x)$ 在 $(a, c)$ 及 $(c, b]$ 上都有定义，且在任一区间 $[a, c-\\varepsilon]$ 及 $[c+\\varepsilon, b]$ 上可积，其中 $\\varepsilon>0$，且 $\\lim_{x \\to b^{+}} f(x)=\\infty$，定义$\\int_{a}^{b} f(x) \\mathrm{d}x = \\int_{a}^{c} f(x) \\mathrm{d}x + \\int_{c}^{b} f(x) \\mathrm{d}x = \\lim_{t \\to 0} \\int_{a}^{t-1} f(x) \\mathrm{d}x + \\lim_{t \\to 0} \\int_{t+1}^{b} f(x) \\mathrm{d}x$\n\n定义1和定义2中若右端极限存在，则称该瑕积分收敛，否则称为发散；定义3中要求右端的两个瑕积分都收敛，则 $\\int_{0}^{b} f(x) \\mathrm{d}x$ 收敛。有一个发散，则 $\\int_{0}^{b} f(x) \\mathrm{d}x$ 发散。\n\n瑕积分的性质、计算方法及敛散性的判别均与无穷积分相类似。\n\n593 基础题 下列积分（    ）是反常积分.\n\n(A) $\\int_{0}^{1} \\frac{\\sin x}{x} \\mathrm{d}x$ (B) $\\int_{0}^{1} x \\ln x \\mathrm{d}x$ (C) $\\int_{-1}^{1} \\frac{\\mathrm{d}x}{\\sqrt{x^2}}$ (D) $\\int_{0}^{1} \\frac{1}{x^2} \\mathrm{d}x$\n\n594 基础题 $I = \\int_{0}^{1} x \\ln^2 x \\mathrm{d}x$ 是（    ）.\n\n(A) 定积分且值为 $\\frac{1}{3}$ (B) 定积分且值为 $\\frac{1}{4}$\n\n(C) 反常积分且发散 (D) 反常积分且值为 $\\frac{1}{2}$\n\n595 基础题 计算 $\\int_{0}^{a} \\frac{\\mathrm{d}x}{\\sqrt{a^2 - x^2}}$.\n\n596 基础题 计算 $\\int_{0}^{1} \\frac{\\mathrm{d}x}{x(\\ln x)^2}$.\n\n597 中等题 讨论瑕积分 $\\int_{a}^{b} \\frac{\\mathrm{d}x}{(x - a)^2}$ 的敛散性.\n\n598 中等题 计算 $\\int_{0}^{\\infty} \\frac{\\ln x}{x^2} + 1 \\mathrm{d}x$.\n\n599 综合题 设函数 $f(x) = \\left\\{ \\begin{array}{l l} \\frac{1}{(x - 1)^{a - 1}}, & 1 < x < e \\\\ \\frac{1}{x \\ln^{a + 1} x}, & x \\geq e \\end{array} \\right.$，若反常积分 $\\int_{1}^{+\\infty} f(x) \\mathrm{d}x$ 收敛，则（    ）.\n\n(A) $\\alpha < -2$ (B) $\\alpha > 2$ (C) $-2 < \\alpha < 0$ (D) $0 < \\alpha < 2$\n\n600 综合题 下列计算正确的是（    ）.\n\n(A) $\\int_{-\\infty}^{x} \\frac{x}{1 - x^2} \\mathrm{d}x = 0$\n\n(B) $\\int_{-\\infty}^{+\\infty} \\sin x \\mathrm{d}x = \\lim_{b \\to \\infty} \\sin x \\mathrm{d}x = \\lim_{b \\to \\infty} \\left(-\\cos x\\right)_{|x|} = \\lim_{b \\to \\infty} \\left[ \\cos(-b) - \\cos b \\right] = 0$\n\n(C) $\\int_{-1}^{1} \\frac{1}{x^2} \\mathrm{d}x = -\\frac{1}{x}|_{-1}^{1} = -2$\n\n(D) $\\int_{0}^{+\\infty} x^{\\frac{3}{2}} \\mathrm{d}x = \\Gamma \\left(\\frac{5}{2}\\right) = \\frac{3}{2} \\Gamma \\left(\\frac{3}{2}\\right) = \\frac{3}{2} \\cdot \\frac{1}{2} \\Gamma \\left(\\frac{1}{2}\\right) = \\frac{3}{4} \\sqrt{\\pi}$"}

## tool · 2026-10-20T02:23:25Z




## tool · 2026-10-20T02:23:32Z


Script completed
Wall time 0.9 seconds
Output:

{"chunk_id":"6b5b60","wall_time_seconds":0.000031709,"exit_code":0,"original_token_count":50,"output":"537 中等题 设 $f(x)$ 在 $[0,1]$ 上连续，且满足 $f(x)=x\\int_{0}^{1}f(t)dt-1$，求 $\\int_{0}^{1}f(x)dx$ 及 $f(x)$.\n\n\n544 基础题 计算 $\\int_{1}^{\\sqrt{2}}\\frac{dx}{x\\sqrt{1+x^{2}}}$."}
{"chunk_id":"8c79e2","wall_time_seconds":0.000020708,"exit_code":0,"original_token_count":35,"output":"545 基础题 计算 $\\int_{1}^{2} \\frac{\\sqrt{x^2-1}}{x} \\mathrm{d}x$.\n\n\n(A) $P > N > M$ (B) $N > P > M$ (C) $N > M > P$ (D) $P > M > N$"}
{"chunk_id":"7f7b3a","wall_time_seconds":0.00002475,"exit_code":0,"original_token_count":32,"output":"558 中等题 计算 $\\int_{0}^{n \\pi} \\sqrt{1 - \\sin^2 x} dx$.\n\n\n568 中等题 计算 $\\int_{1}^{16} \\arctan \\sqrt{x - 1} dx$."}
{"chunk_id":"124be1","wall_time_seconds":0.000018583,"exit_code":0,"original_token_count":65,"output":"第四节 反常积分\n\n\n$$\\int_{-\\infty}^{+\\infty} f(x) \\mathrm{d}x = \\int_{-\\infty}^{+\\infty} f(x) \\mathrm{d}x + \\int_{0}^{+\\infty} f(x) \\mathrm{d}x = \\lim_{b \\to +\\infty} \\int_{a}^{b} f(x) \\mathrm{d}x + \\lim_{b \\to +\\infty} \\int_{a}^{b} f(x) \\mathrm{d}x$$"}
{"chunk_id":"2da7f1","wall_time_seconds":0.000018166,"exit_code":0,"original_token_count":80,"output":"定义 1 和定义 2 中若右端极限存在，则称该反常积分收敛，否则称为发散；\n定义 3 中要求右端的两个反常积分都收敛，则 $\\int_{-\\infty}^{\\infty} f(x) \\mathrm{d}x$ 收敛。有一个发散，则\n\n583 基础题 计算 $\\int_{-\\infty}^{\\infty} \\frac{e^{x}}{1+e^{2x}} \\mathrm{d}x$."}
{"chunk_id":"63116c","wall_time_seconds":0.000030125,"exit_code":0,"original_token_count":75,"output":"584 中等题 计算 $\\int_{0}^{+\\infty} \\min \\left\\{e^{-x}, \\frac{1}{2}\\right\\} dx$.\n\n\n定义3：设 $f(x)$ 在 $(a, c)$ 及 $(c, b]$ 上都有定义，且在任一区间 $[a, c-\\varepsilon]$ 及 $[c+\\varepsilon, b]$ 上可积，其中 $\\varepsilon>0$，且 $\\lim_{x \\to b^{+}} f(x)=\\infty$，定义"}
{"chunk_id":"fd776d","wall_time_seconds":0.000019833,"exit_code":0,"original_token_count":105,"output":"$\\int_{a}^{b} f(x) \\mathrm{d}x = \\int_{a}^{c} f(x) \\mathrm{d}x + \\int_{c}^{b} f(x) \\mathrm{d}x = \\lim_{t \\to 0} \\int_{a}^{t-1} f(x) \\mathrm{d}x + \\lim_{t \\to 0} \\int_{t+1}^{b} f(x) \\mathrm{d}x$\n\n\n(D) $\\int_{0}^{+\\infty} x^{\\frac{3}{2}} \\mathrm{d}x = \\Gamma \\left(\\frac{5}{2}\\right) = \\frac{3}{2} \\Gamma \\left(\\frac{3}{2}\\right) = \\frac{3}{2} \\cdot \\frac{1}{2} \\Gamma \\left(\\frac{1}{2}\\right) = \\frac{3}{4} \\sqrt{\\pi}$"}

## tool · 2026-10-20T02:23:39Z




## tool · 2026-10-20T02:24:52Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-10-20T02:24:56Z


Script completed
Wall time 0.3 seconds
Output:

{"page":"087","result":{"chunk_id":"a50f8f","wall_time_seconds":0.000007959,"exit_code":0,"original_token_count":223,"output":"第6章\n定积分的应用\n\n第一节 定积分在几何学上的应用\n\n一、直角坐标系下平面图形的面积\n\n1. X型区域：图形曲边是关于x的函数.\nX型区域的面积计算口诀是“以上、下曲边的函数差作被积函数”，该分割时就分割.\n由y=f(x),y=g(x)(f(x)≥g(x)),x=a,x=b(a<b)所围成的平面区域（图6-1）\n的面积S=∫a[f(x)-g(x)]dx.\n\n图6-1\n图6-2\n\n评注\n(1) 当g(x)=0时，由y=f(x),y=0(f(x)≥0),x=a,x=b(a<b)所围\n成的平面区域为曲边梯形（图6-2），面积S=∫a⁰f(x)dx.\n(2) 若在[a,b]上，图形的上曲边或者下曲边不能用同一个解析函数表示\n（图6-3），则从x=c处分割，面积S=∫a[f(x)-g(x)]dx+∫a⁰[g(x)-f(x)]dx.\n\n图6-3\n\n2. Y型区域：图形曲边是关于y的函数.\nY型区域的面积计算口诀是：“以右、左曲边的函数差作被积函数”，该分割\n时就分割."}}
{"page":"088","result":{"chunk_id":"8e6ca0","wall_time_seconds":0.000008292,"exit_code":0,"original_token_count":357,"output":"由 $x=\\psi(y), x=\\varphi(y)(\\psi(y)\\geq\\varphi(y)), y=c, y=d(c<d)$ 所围成的平面区域（图 6-4(A)）\n的面积 $S=\\int_{c}^{d}[\\psi(y)-\\varphi(y)]\\mathrm{d}y.$\n\n图 6-4\n\n评注\n若区域的右曲边或左曲边不能用同一个解析函数表示，也需要将平\n面图形分割后再分别列式计算（图 6-4(B)）。\n\n3. 计算平面图形面积的步骤.\n第 1 步：画出围成平面图形的曲线，确定平面区域.\n第 2 步：计算出必要的交点坐标.\n第 3 步：根据平面图形的特点，选择平面图形的区域类型（尽量不分割）。\n第 4 步：确定平面图形的上、下曲边或者右、左曲边，列式计算.\n\n601 基础题 求曲线 $y=\\sqrt{x}, y=0, x=4$ 所围成的平面图形的面积.\n\n602 基础题 求曲线 $x=\\sqrt{y}$ 、直线 $y=x+1, y=1$ 与 $x$ 轴所围成的平面图形的面积.\n\n603 基础题 求曲线 $y=x^2$ 与直线 $y=x$ 所围成的平面图形的面积.\n\n604 基础题 求曲线 $y=-x^2+4$ 与直线 $y=-2x+4$ 所围成的平面图形的面积.\n\n605 基础题 若曲线 $y=\\sqrt{ax}(a>0)$ 与 $x$ 轴及直线 $x=3$ 所围成的图形面积等于 6，\n求常数 $a$.\n\n606 基础题 计算由曲线 $y=2^x$ 和直线 $x+2y=2, x=2$ 所围成的平面图形的面积.\n\n607 中等题 求曲线 $y=x^2-x$ 与 $x$ 轴所围成的平面图形及直线 $y=2x+6$ 、曲线\n$y=x^2-x$ 、 $x$ 轴在 $x>1$ 时所围成的平面图形的面积之和."}}
{"page":"089","result":{"chunk_id":"baa437","wall_time_seconds":0.000008292,"exit_code":0,"original_token_count":455,"output":"608 中等题 求 $ y=x^{2} $ 在点(2,4)处的切线与 $ y=-x^{2}+4x+1 $所围图形的面积.\n\n609 中等题 计算由 $ y^{2}=9-x $ ，直线 $ x=2 $ 及 $ y=-1 $ 所围成的平面图形上面部分（面积大的那部分）的面积.\n\n610 中等题 计算由曲线 $ y=x\\cos(2x)\\left(0\\leq x\\leq \\frac{\\pi}{4}\\right) $ 和直线 $ y=0 $ 所围成的平面图形的面积.\n\n611 中等题 求由曲线 $ y=\\mathrm{e}^{x}(y\\leq 1) $ ， $ y=\\mathrm{e}^{-x}(y\\leq 1) $ 和直线 $ x=1 $ ， $ x=-1 $ ， $ y=0 $ 所围成的平面图形的面积.\n\n612 中等题 求由曲线 $ y=x\\ln x $ 和直线 $ y=x $ ， $ y=0 $ 所围成的平面图形的面积.\n\n613 中等题 求由曲线 $ y=\\sin x $ ， $ y=\\cos x $ 和直线 $ x=0 $ ， $ x=2\\pi $ 所围成的平面图形的面积.\n\n614 中等题 求由曲线 $ y=x^{2} $ ， $ x^{2}+y^{2}=2 $ 和直线 $ y=0 $ 所围成的平面图形的面积.\n\n615 中等题 设由抛物线 $ y=4x-x^{2} $ ， $ y $ 轴和直线 $ y=b(b>0) $ 所围成的平面图形的面积是仅由抛物线 $ y=4x-x^{2} $ 及直线 $ y=b $ 所围图形面积的一半，求 $ b. $\n\n616 中等题 直线 $ y=x $ 将椭圆 $ x^{2}+3y^{2}-6y=0 $ 分成两部分，求直线下方的面积 $ S. $\n\n617 综合题 已知抛物线 $ y=px^{2}+qx $ （其中 $ p<0, q>0 $ ）在第一象限内与直线 $ x+y=5 $ 相切，且抛物线与 $ x $ 轴所围成的平面图形的面积为 $ S. $\n(1) $ p $ 和 $ q $ 为何值时， $ S $ 达到最大值？\n(2) 求出此最大值.\n\n618 综合题 在抛物线 $ y=x^{2}(0\\leq x\\leq 1) $ 上找一点 $ P $ ，使过点 $ P $ 的水平直线与抛物线以及直线 $ x=0 $ ， $ x=1 $ 所围成的平面图形面积最小.\n\n619 综合题 求两抛物线 $ y=x^{2} $ ， $ y=-x^{2}+4x-4 $ 的公切线，并求此公切线与此二抛物线所围图形的面积."}}
{"page":"090","result":{"chunk_id":"36090d","wall_time_seconds":0.000006959,"exit_code":0,"original_token_count":350,"output":"620 综合题 设抛物线 $y=ax^2+bx+c$ 满足下列两个条件: (1) 过 (0,0) 和 (1,2) 两点,\n且 $a<0$; (2) 与抛物线 $y=-x^2+2x$ 围成的图形面积最小, 求 $a,b,c$.\n\n二、极坐标系下平面图形的面积\n\n计算公式\n1. 若平面区域 $D$ 是由曲线 $r=r(\\theta),\\theta=\\alpha,\\theta=\\beta(\\alpha<\\beta)$ 所围成 (图 6-5), 则面积\n$S=\\frac{1}{2}\\int_{\\alpha}^{\\beta}r^2(\\theta)d\\theta$.\n2. 若平面区域 $D$ 是由曲线 $r=r_1(\\theta),r=r_2(\\theta),\\theta=\\alpha,\\theta=\\beta(\\alpha<\\beta)$ 所围成, 如图 6-6,\n则面积 $S=\\frac{1}{2}\\int_{\\alpha}^{\\beta}(r_2^2(\\theta)-r_1^2(\\theta))d\\theta$.\n\n图 6-5 图 6-6\n\n评注\n(1) 极坐标下计算平面图形的面积有两个关键:\n第一是围成平面图形的曲边 $r=r(\\theta)$ 或 $r=r_1(\\theta)$, $r=r_2(\\theta)$ 等;\n第二是平面图形的角度 $\\theta$ 的范围.\n(2) 记住一些极坐标下的常见曲线的图形: 心形线、双纽线、对数螺线和阿基米德螺线等.\n\n621 基础题 求曲线 $\\rho=a\\cos \\theta+b(b\\geq a>0)$ 所围图形的面积.\n\n622 中等题 求由曲线 $\\rho=a\\sin \\theta$, $\\rho=a(\\cos \\theta+\\sin \\theta)(a>0)$ 所围图形公共部分的\n面积.\n\n三、用参数方程表示的曲线所围平面图形的面积\n\n计算公式\n设曲线 $L$ 的参数方程为 $\\begin{cases} x=x(t) \\\\ y=y(t) \\end{cases}$, $\\alpha\\leq t\\leq \\beta$, 其中 $x(t)$, $y(t)$ 都连续."}}
{"page":"091","result":{"chunk_id":"849f44","wall_time_seconds":0.000006333,"exit_code":0,"original_token_count":459,"output":"1. 当 $y(t) \\geq 0$ ， $x(t)$ 可导， $x'(t) > 0$ ，且 $x(\\alpha) = a, x(\\beta) = b$ 时，由 $x = a, x = b, x$ 轴及曲线 $L$ 所围图形的面积为 $S = \\int_{a}^{\\beta} f(x) \\mathrm{d}x = \\int_{a}^{\\beta} y(t) x'(t) \\mathrm{d}t$ 其中 $y = f(x), x \\in [a, b]$ 是 $L$ 的直角坐标方程.\n2. 当 $x(t) \\geq 0$ ， $y(t)$ 可导， $y'(t) > 0$ ，且 $y(\\alpha) = c, y(\\beta) = d$ 时，由 $y = c, y = d, y$ 轴及曲线 $L$ 所围图形的面积为 $S = \\int_{a}^{\\beta} x(t) y'(t) \\mathrm{d}t$.\n\n评注\n上述两个公式可以由定积分换元法得到.\n\n623 基础题 求旋轮线 $L$ ： $\\left\\{ \\begin{array}{l} x = a (t - \\sin t) \\\\ y = a (1 - \\cos t) \\end{array} \\right.$ $t \\in [0, 2 \\pi], (a > 0)$ 与 $x$ 轴所围平面图形的面积.\n\n624 中等题 设 $P$ 为曲线 $\\left\\{ \\begin{array}{l} x = \\cos t \\\\ y = 2 \\sin^2 t \\end{array} \\right.$ $t \\in [0, \\frac{\\pi}{2}]$ 上一点，该曲线与直线 $OP$ 及 $x$ 轴所围成图形的面积为 $S$ ，求函数 $\\frac{\\mathrm{d}S}{\\mathrm{d}t}$ 取得最大值时点 $P$ 的坐标.\n\n四、旋转体的体积\n\n计算公式\n1. 由 $x = a, x = b (0 < a < b), y = f(x) (f(x) > 0), y = 0$ 所围成的曲边梯形（图 6-7）绕 $x$ 轴旋转一周而成的旋转体的体积为 $V_x = \\int_{0}^{\\beta} \\pi [f(x)]^2 \\mathrm{d}x$ ，绕 $y$ 轴旋转一周而成的旋转体的体积为 $V_y = 2 \\pi \\int_{0}^{\\beta} x f(x) \\mathrm{d}x.$\n2. 由 $y = c, y = d (0 < c < d), x = \\varphi(y) (\\varphi(y) > 0), x = 0$ 所围成的曲边梯形（图 6-8）绕 $y$ 轴旋转一周而成的旋转体的体积为 $V_y = 2 \\pi \\int_{0}^{\\beta} y \\varphi(y) \\mathrm{d}y.$\n3. 由 $x = a, x = b (0 < a < b), y = f_1(x), y = f_2(x), (f_2(x) > f_1(x) > 0)$ 所围成的平面图形（图 6-9）\n\n图 6-7 图 6-8 图 6-9\n绕 $x$ 轴旋转一周而成的旋转体的体积为"}}

## tool · 2026-10-20T02:25:11Z




## tool · 2026-10-20T02:25:18Z


Script completed
Wall time 0.3 seconds
Output:

{"page":"092","result":{"chunk_id":"c01047","wall_time_seconds":0.00001875,"exit_code":0,"original_token_count":495,"output":"$V_{x} = \\int_{a}^{b} \\pi[f_{2}(x)]^{2} \\mathrm{d}x - \\int_{a}^{b} \\pi[f_{1}(x)]^{2} \\mathrm{d}x = \\pi \\int_{a}^{b} [f_{2}^{2}(x) - f_{1}^{2}(x)] \\mathrm{d}x.$\n绕 $y$ 轴旋转一周而成的旋转体的体积为\n$V_{y} = 2 \\pi \\int_{a}^{b} x f_{2}(x) \\mathrm{d}x - 2 \\pi \\int_{a}^{b} x f_{1}(x) \\mathrm{d}x = 2 \\pi \\int_{a}^{b} x [f_{2}(x) - f_{1}(x)] \\mathrm{d}x.$\n\n625 基础题 计算曲线 $\\frac{x^{2}}{4} - \\frac{y^{2}}{9} = 1, y = \\pm 3$ 所围平面图形绕 $y$ 轴旋转而成的旋转体的体积.\n\n626 基础题 计算曲线 $xy = 3, x + y = 4$ 所围平面图形绕 $x$ 轴旋转而成的立体体积.\n\n627 基础题 计算曲线 $y = \\mathrm{e}^{-x}$ 在第一象限中的部分分别绕 $x$ 轴和 $y$ 轴旋转而成的旋转体的体积.\n\n628 基础题 计算曲线 $y = \\mathrm{e}^{-x^{2}}, x = 0, x = -1$ 及 $x$ 轴所围平面图形绕 $y$ 轴旋转而成的旋转体的体积.\n\n629 基础题 计算曲线 $x^{2} + (y - 2)^{2} = a^{2} (a > 0)$ 所围平面图形绕 $x$ 轴旋转所得的旋转体的体积.\n\n630 中等题 过原点作曲线 $y = \\ln x$ 的切线，求由切线、曲线及 $x$ 轴所围平面图形分别绕 $x$ 轴和 $y$ 轴旋转所得旋转体的体积.\n\n631 中等题 曲线 $y = x \\mathrm{e}^{-x} (0 \\leqslant x < + \\infty)$ 绕 $x$ 轴旋转一周所得延展到无穷远的旋转体的体积.\n\n632 综合题 求 $y = \\sqrt{1 - (x - 2)^{2}}$ 与 $y = x^{2} - 4x + 3$ 所围平面图形分别绕 $x$ 轴和 $y$ 轴旋转一周所得旋转体的体积 $V_{x}$ 和 $V_{y}$.\n\n633 综合题 设曲线 $\\left\\{ \\begin{array}{l} x = \\cos^{3} t \\\\ y = \\sin^{3} t \\end{array} \\right.$，求曲线所围的平面图形绕直线 $y = 1$ 旋转所成旋转体的体积.\n\n634 综合题 过曲线 $y = \\sqrt{x}$ 上某点 $A$ 做切线，使之与曲线及 $y$ 轴围成的图形面积为 $\\frac{1}{12}$，求 (1) 切点 $A$ 的坐标；(2) 过点 $A$ 的切线方程；(3) 由上述图形绕 $x$ 轴和绕 $y$ 轴旋转所得旋转体的体积."}}
{"page":"093","result":{"chunk_id":"772396","wall_time_seconds":0.000010834,"exit_code":0,"original_token_count":559,"output":"635综合题 设曲线方程 $y=\\mathrm{e}^{-x}(x\\geq 0)$，(1)把曲线 $y=\\mathrm{e}^{-x}(x\\geq 0)$，$x$ 轴，$y$ 轴和直线 $x=\\xi(\\xi>0)$ 所围成的平面图形绕 $x$ 轴旋转一周，得一旋转体，此旋转体的体积为 $V(\\xi)$，求满足 $V(a)=\\frac{1}{2}\\lim_{k\\to\\infty}V(\\xi)$ 的 $a$；(2)在此曲线上找一点，使过该点的切线与两个坐标轴所夹平面图形的面积最大，并求该面积 $S$。\n\n五、旋转体的侧面积（旋转曲面面积）\n\n计算公式\n1. 由曲线 $y=f(x),a\\leqslant x\\leqslant b$ 绕 $x$ 轴旋转而成的旋转体的侧面积\n$S=2\\pi \\int_{a}^{b}|f(x)|\\sqrt{1+[f'(x)]^{2}}dx.$\n2. 由曲线 $y=\\varphi(y),c\\leqslant y\\leqslant d$ 绕 $y$ 轴旋转而成的旋转体的侧面积\n$S=2\\pi \\int_{a}^{b}|\\varphi(y)|\\sqrt{1+[f'(y)]^{2}}dx.$\n3. 曲线方程为 $\\left\\{ \\begin{array}{l}x=x(t)\\\\ y=y(t)\\end{array} \\right.$ $\\alpha\\leqslant t\\leqslant \\beta$，且 $x'(t)\\neq 0$，则该曲线绕 $x$ 轴旋转而成的旋转体的侧面积 $S=2\\pi \\int_{a}^{\\beta}|y(t)|\\sqrt{[x'(t)]^{2}+[y'(t)]^{2}}dt.$\n4. 曲线方程为 $\\left\\{ \\begin{array}{l}x=x(t)\\\\ y=y(t)\\end{array} \\right.$ $\\alpha\\leqslant t\\leqslant \\beta$，且 $y'(t)\\neq 0$，则该曲线绕 $y$ 轴旋转而成的旋转体的侧面积 $S=2\\pi \\int_{a}^{\\beta}|x(t)|\\sqrt{[x'(t)]^{2}+[y'(t)]^{2}}dt.$\n\n636基础题 摆线的参数方程为 $x=a(t-\\sin t),y=a(1-\\cos t),0\\leqslant t\\leqslant 2\\pi$，常数 $a>0$，计算(1)该弧段绕 $x$ 轴旋转一周而成的旋转曲面的面积 $S_{y}$；(2)该弧段绕 $y$ 轴旋转一周而成的旋转曲面的面积 $S_{y}$。\n\n637基础题 曲线 $y^{2}=2x+3(0\\leqslant x\\leqslant 3)$ 绕 $x$ 轴旋转而成的旋转体的侧面积\n\n六、平面曲线的弧长\n\n计算公式\n1. 曲线 $y=f(x),a\\leqslant x\\leqslant b$ 的弧长（其中 $f'(x)$ 连续） $s=\\int_{a}^{b}\\sqrt{1+[f'(x)]^{2}}dx$（直角坐标）.\n2. 曲线 $\\int_{a}^{x=t}|y(t)|\\alpha\\leqslant t\\leqslant \\beta$ 的弧长（其中 $x'(t),y'(t)$ 均连续，且不同时为零） $s=\\int_{a}^{\\beta}\\sqrt{[x'(t)]^{2}+[y'(t)]^{2}}dt$（参数方程）.\n3. 曲线 $r=r(\\theta),\\alpha\\leqslant \\theta\\leqslant \\beta$ 的弧长（其中 $r(\\theta),r'(\\theta)$ 均连续，且不同时为零）"}}
{"page":"094","result":{"chunk_id":"cee95f","wall_time_seconds":0.000014417,"exit_code":0,"original_token_count":496,"output":"$s = \\int_{a}^{\\theta} \\sqrt{r^2(\\theta)} + |r'(\\theta)|^2 \\mathrm{d}\\theta$ (极坐标).\n\n638 基础题 计算曲线 $y = x\\sqrt{x}(0 \\leqslant x \\leqslant 4)$ 的弧长.\n\n639 基础题 计算曲线 $y = \\ln(\\cos x), 0 \\leqslant x \\leqslant \\frac{\\pi}{3}$ 的弧长.\n\n640 基础题 计算曲线 $y = \\int_{0}^{x} \\tan t \\mathrm{d}t, 0 \\leqslant x \\leqslant \\frac{\\pi}{4}$ 的弧长.\n\n641 基础题 计算圆的渐开线 $\\left\\{ \\begin{array}{l} x = a(\\cos t + t\\sin t) \\\\ y = a(\\sin t - t\\cos t) \\end{array} \\right.$ $0 \\leqslant t \\leqslant 2\\pi$ 的弧长 ($a > 0$).\n\n642 基础题 当 $0 \\leqslant \\theta \\leqslant \\pi$ 时，求对数螺线 $r = e^{\\theta}$ 的弧长 $s$.\n\n643 中等题 计算曲线 $\\sqrt{x} + \\sqrt{y} = 1$ 的弧长.\n\n644 中等题 计算曲线 $y = x^2, y = 2 - x$ 及 $y$ 轴围成的平面图形边界曲线的周长.\n\n645 综合题 设 $\\rho = \\rho(x)$ 是抛物线 $y = \\sqrt{x}$ 上任一点 $M(x,y)(x \\geqslant 1)$ 处的曲率半径，$s = s(x)$ 是该抛物线上介于点 $A(1,1)$ 与 $M$ 之间的弧长，计算 $3\\rho \\frac{\\mathrm{d}^2 \\rho}{\\mathrm{d}s^2} - \\left(\\frac{\\mathrm{d}\\rho}{\\mathrm{d}s}\\right)^2$ 的值 (直角坐标系下曲率公式为 $K = \\frac{|y^4|}{(1 + y^2)^2}$).\n\n七、平行截面面积为已知的立体体积\n\n计算公式\n1. 夹在两平行平面 $x = a, x = b(a < b)$ 间的立体的截面面积函数 $A(x)$ 已知，且是 $x \\in [a,b]$ 上的连续函数，则该立体体积为 $V = \\int_{a}^{b} A(x) \\mathrm{d}x$.\n2. 夹在两平行平面 $y = c, y = d(c < d)$ 间的立体的截面面积函数 $A(y)$ 已知，且是 $y \\in [c,d]$ 上的连续函数，则该立体体积为 $V = \\int_{c}^{d} A(y) \\mathrm{d}y$.\n646 中等题 设平面图形 $A$ 由 $x^2 + y^2 \\leqslant 2x$ 与 $y \\geqslant x$ 所确定，求图形 $A$ 绕直线 $x = 2$ 旋转一周所成旋转体的体积.\n647 中等题 求曲线 $y = 3 - |x^2 - 1|$ 与 $x$ 轴围成的封闭图形绕直线 $y = 3$ 旋转一周所成旋转体的体积."}}
{"page":"095","result":{"chunk_id":"ee839b","wall_time_seconds":0.000009375,"exit_code":0,"original_token_count":443,"output":"648 中等题 设有一正椭圆柱体，其底面的长、短轴分别为 $2a, 2b$ ，用过此柱体底面的短轴与底面成 $\\alpha \\left( 0 < \\alpha < \\frac{\\pi}{2} \\right)$ 角的平面截此柱体，得一楔形体（如图 6-10），求此楔形体的体积 $V$ .\n\n图 6-10\n\n649 中等题 过坐标原点作曲线 $y=\\ln x$ 的切线，该切线与曲线 $y=\\ln x$ 及 $x$ 轴围成的平面图形 $D$ . 求 (1) $D$ 的面积 $A$ ; (2) $D$ 绕直线 $x=e$ 旋转一周所得旋转体的体积 $V$ .\n\n第二节 定积分在物理学上的应用\n\n650 综合题 设单位质点在水平面内作直线运动，初速度 $v_{1}|_{x=0}=v_{0}$ . 已知阻力与速度成正比（比例常数为 1），问 $t$ 为多少时此质点的速度为 $\\frac{v_{0}}{3}$？并求到此时刻该点所经过的路程.\n\n651 综合题 为消除井底的污泥，用缆绳将抓斗放入井底，抓起污泥后提出井口（见图 6-11）. 已知井深 $30m$ ，抓斗自重 $400N$ ，缆绳每米重 $50N$ ，抓斗抓起污泥重 $2000N$ ，提升速度为 $3m/s$ . 在提升过程中，污泥以 $20N/s$ 的速率从抓斗缝隙中漏掉，现将抓起污泥的抓斗提升至井口，问克服重力需作多少焦耳的功（说明：$\\textcircled{1}$ $1N \\times 1m=11$；$m,N,sJ$ 分别表示米，牛顿，秒，焦耳；$\\textcircled{2}$ 抓斗的高度、位于井口上方的缆绳长度忽略不计）?\n\n652 综合题 某闸门的形状与大小如图 6-12 所示，其中直线 $l$ 为对称轴，闸门的上部为矩形 $ABCD$，下部由二次抛物线与线段 $AB$ 所围成. 当水面与闸门的上端相平时，欲使闸门矩形部分承受的水压力与闸门下部承受的水压力之比为 5:4，闸门矩形部分的高 $h$ 应为多少 $m$ （米）?"}}
{"page":"096","result":{"chunk_id":"75094c","wall_time_seconds":0.000010125,"exit_code":0,"original_token_count":381,"output":"653综合题 某建筑工程打地基时，需用气锤将桩打进土层. 气锤每次击打，都将克服土层对桩的阻力而作功. 设土层对桩的阻力的大小与桩被打进地下深度成正比（比例系数为 $k,k>0$ ）。气锤第一次击打将桩打进地下 $a$ m. 根据设计方案，要求气锤每次击打桩时所作的功与前一次击打时所作的功之比为常数 $r(0<r<1)$.\n(1) 求气锤击打桩 3 次后，可将桩打进地下多深?\n(2) 若击打次数不限，气锤至多能将桩打进地下多深?\n\n654综合题 一个高为 $l$ 的柱体形贮油罐，底面是长轴为 $2a$，短轴为 $2b$ 的椭圆，现将贮油罐平放，当油罐中油面高度为 $\\frac{3}{2}b$ 时（图 6-13），计算油的质量（长度单位为 $m$，质量单位为 $kg$，油的密度为常数 $\\rho kg/m^3$）。\n\n图 6-13\n\n655综合题 一容器的内侧是由图 6-14 中曲线绕 $y$ 轴旋转一周而成的曲面，该曲线由 $x^2+y^2=2y\\left(y\\geqslant\\frac{1}{2}\\right)$ 与 $x^2+y^2=1\\left(y\\leqslant\\frac{1}{2}\\right)$ 连接而成.\n(1) 求容器的容积.\n(2) 若将容器内盛满的水从容器顶部全部抽走，至少需要做多少功（长度单位为 $m$，重力加速度为 $g m/s^2$，水的密度为 $10^3 kg/m^3$）?\n\n图 6-14\n\n656综合题 设曲线 $L$ 的方程为 $y=\\frac{1}{4}x^2-\\frac{1}{2}\\ln x(1\\leqslant x\\leqslant e)$.\n(1) 求 $L$ 的弧长.\n(2) 设 $D$ 是由曲线 $L$，直线 $x=1,x=e$ 及 $x$ 轴所围平面图形，求 $D$ 的形心的横坐标."}}

## tool · 2026-10-20T02:25:36Z




## tool · 2026-10-20T02:27:24Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"3e3711","wall_time_seconds":0.000009083,"exit_code":0,"original_token_count":325,"output":"\\section{第6章 定积分的应用}\n\\subsection{定积分在几何学上的应用}\n\\begin{supplement}{6.1-1}{面积、体积与参数约束}\n对 $a>0$，区域 $D_a$ 由 $y=x^2$、$y=ax$ 围成。求其面积及绕 $x$ 轴旋转所得立体的体积；若区域面积等于 $\\frac43$，求 $a$ 与相应体积。\n\\end{supplement}\n\\begin{supplement}{6.1-2}{弧长与旋转曲面面积}\n曲线 $y=\\frac{x^2}{4}-\\frac12\\ln x$，$1\\le x\\le2$。求曲线弧长以及绕 $y$ 轴旋转所得曲面的面积，并写出所用弧长微元。\n\\end{supplement}\n\\subsection{定积分在物理学上的应用}\n\\begin{supplement}{6.2-1}{变力做功与动能定理}\n质量为 $m$ 的物体沿水平直线运动，阻力大小为 $kv^2$，其中 $k>0$、$v$ 为速率。物体仅受此阻力，从速率 $v_0>0$ 减至 $v_0/2$。利用 $mv\\dd v=-kv^2\\dd s$ 求此过程中的位移、阻力做功，并核验动能定理。\n\\end{supplement}\n\\begin{supplement}{6.2-2}{液体压力与水深参数}\n竖直薄板为底边水平的等腰三角形，高 $h$、底边长 $b$，顶点在底边上方。薄板顶点距水面 $d\\ge0$，水的密度为 $\\rho$。求单侧静水总压力 $P(d)$；若将薄板翻转使底边在上方且最高点仍在深度 $d$ 处，求压力变化量并解释其符号。\n\\end{supplement}\n"}
{}

## tool · 2026-10-20T02:27:28Z


Script completed
Wall time 0.6 seconds
Output:

{"page":"097","result":{"chunk_id":"8ef132","wall_time_seconds":0.000009041,"exit_code":0,"original_token_count":324,"output":"第7章\n微分方程\n\n第一节 微分方程的基本概念\n\n一、微分方程的定义\n\n定义1: 表示未知函数、未知函数的导数与自变量之间关系的方程, 叫作微\n分方程, 有时也简称方程.\n\n评注\n方程中必须出现未知函数的最高阶导数的阶数, 叫作微分方程的阶.\n\n定义2: 微分方程中所出现的未知函数的最高阶导数的阶数, 叫作微分方程的阶.\n\n657 基础题 下列方程是微分方程的是 (    ).\n\n(A) $x^{2}+x+1=0$\n(B) $y^{2}+2x+1=0$\n(C) $x^{2}y^{2}+y=3$\n(D) $x^{2}+y^{2}+y=2$\n\n658 基础题 微分方程 $y^{*}-2x(y^{'})^{3}+y^{2}=0$ 的阶数是 (    ).\n\n659 基础题 微分方程 $xdy+(x+y)dx=0$ 的阶数是 (    ).\n\n二、微分方程解的定义\n\n定义1: 满足微分方程的函数, 称为微分方程的解.\n\n定义2: 如果微分方程的解中含有任意常数, 且任意常数的个数与微分方程\n的阶数相同, 则称之为微分方程的通解.\n\n评注\n通解里所说的任意常数是独立的, 也就是说, 它们不能合并而使得\n任意常数的个数减少.\n\n定义3: 微分方程的不含任意常数的解, 称为特解.\n\n定义4: 由通解确定特解的条件, 称为初始条件.\n\n660 基础题 判断 $y=5x^{2}$ 是否是微分方程 $xy'-2y=0$ 的解, 是通解还是特解?"}}
{"page":"098","result":{"chunk_id":"b0452d","wall_time_seconds":0.000008625,"exit_code":0,"original_token_count":376,"output":"661 基础题 验证 $y = C_1 \\cos x + C_2 \\sin x$ 是微分方程 $y' + y = 0$ 的解，并求满足初始\n条件 $y(0) = 2, y'(0) = 3$ 的特解.\n\n662 中等题 已知函数 $y = \\frac{1}{2} x^2 + x + C$，微分方程 $y' - y' = -x$，下列说法正确的是\n(    )。\n(A) $y$ 是微分方程的通解\n(B) $y$ 是微分方程满足条件 $y|_{x=0} = 1$ 的特解\n(C) $y$ 是微分方程的解\n(D) 以上都不对\n\n663 中等题 判断二元方程 $y = \\ln(xy)$ 所确定的函数是否为微分方程\n$(xy - x)y' + x(y')^2 + yy' - 2y' = 0$ 的解，是通解还是特解？\n\n第二节 可分离变量的微分方程\n\n一、可分离变量微分方程的定义\n\n定义：形如 $\\frac{dy}{dx} = f(x)f_2(y)$ 或 $M_1(x)M_2(y)dx + N_1(x)N_2(y)dy = 0$ 的微分方程称\n为可分离变量的微分方程.\n\n二、可分离变量微分方程的求解方法\n\n第1步：分离变量。一般地，把方程中与 $y$ 有关的项移到左边，与 $x$ 有关的\n项移到右边得\n\n$g(y)dy = f(x)dx$；\n\n第2步：上式两边同时积分，得 $\\int g(y)dy = \\int f(x)dx$，则方程的隐式通解为\n$G(y) = F(x) + C$。\n\n第3步：化简整理。将上面得到的隐式通解尽量化简，能整理出显函数的形式最好，不好整理的，微分方程的通解写成隐函数的形式也是可以的。\n\n664 基础题 下列微分方程不是一阶变量可分离的微分方程的是（    ）。\n(A) $y' + xy = 0$ \n(B) $y^2dx + (2x+1)dy = 0$\n(C) $y' = xy e^{+xy}$ \n(D) $(x-y)dx + (x+y)dy = 0$"}}
{"page":"099","result":{"chunk_id":"d42556","wall_time_seconds":0.000007833,"exit_code":0,"original_token_count":377,"output":"665 基础题 求微分方程 $\\frac{dy}{dx} = \\frac{y(1-x)}{x}$ 的通解.\n\n666 基础题 求微分方程 $\\frac{dy}{dx} = \\frac{\\sin x \\cos x}{y^2}$ 的通解.\n\n667 基础题 求微分方程 $(1+e^x)dy - ye^xdx = 0$ 满足初始条件 $y|_{x=0} = 2$ 的特解.\n\n668 基础题 求微分方程 $(xy^2 + x)dx + (y-x^2)dy = 0$ 满足初始条件 $y|_{x=0} = 1$ 的特解.\n\n669 中等题 求微分方程 $e^{x-y}dx + ydy = 0$ 满足初始条件 $y|_{x=0} = 1$ 的特解.\n\n670 中等题 已知曲线 $y = y(x)$ 上任一点 $P(x,y)$ 处的切线斜率为 $\\frac{y^2}{1+x^2}$，且曲线过 $(0,-1)$ 点，求该曲线的方程.\n\n671 中等题 设 $f(x)$ 为连续函数，且满足 $f(x) = \\int_0^{3x} f\\left(\\frac{t}{3}\\right)dt + 2$，求 $f(x)$.\n\n672 中等题 设当 $x \\geq 0$ 时 $f(x)$有一阶连续导数，并且满足 $f(x) = 2\\int_0^{x}(x-t)f(t)f'(t)dt + x-1$，求当 $x \\geq 0$时的 $f(x)$.\n\n673 中等题 设函数 $f(x)$ 连续，且满足 $\\int_0^{x}f(t)dt = \\int_0^{x}tf(x-t)dt + x$，求 $f(x)$的表达式.\n\n674 中等题 设非零函数 $f(x)$ 连续，且满足 $f(x) = \\int_0^{x}f(t)dt + 2\\int_0^{1}tf^2(t)dt$，求 $f(x)$的表达式.\n\n675 中等题 设函数 $f(x)$ 在 $(-\\infty,+\\infty)$ 内可导，且满足 $f'(x) = \\frac{x}{1+x^2}f(x)$，$f(0) = a$。若 $\\int_0^{\\sqrt{3}}tf(x)dx = 7$，求 $a$的值.\n\n676 中等题 求微分方程 $y' = y^2 + 2(\\sin x - 1)y + \\sin^2 x - 2\\sin x - \\cos x + 1$的通解.\n\n677 中等题 求微分方程 $y(x+1)dx + x(1+xy+x^2y^2)dy = 0$的通解."}}
{"page":"100","result":{"chunk_id":"919b6a","wall_time_seconds":0.000007125,"exit_code":0,"original_token_count":384,"output":"第三节 齐次方程\n\n一、齐次方程的定义\n定义：形如 $\\frac{dy}{dx} = \\varphi\\left(\\frac{y}{x}\\right)$ 的微分方程称为齐次方程.\n\n二、齐次方程的求解方法\n第1步：变量代换. 令 $u = \\frac{y}{x}$，则 $y = xu$，$\\frac{dy}{dx} = u + x\\frac{du}{dx}$. <这一步最关键\n第2步：代入方程并分离变量. $u + x\\frac{du}{dx} = \\varphi(u) \\Rightarrow \\frac{1}{\\varphi(u) - u} du = \\frac{1}{x} dx$.\n第3步：两端积分得. $\\Phi(u) = \\ln|x| + C$.\n第4步：回代整理. 以 $\\frac{y}{x}$ 代替 $u$，并化简整理，即可得原齐次方程的通解.\n\n678 基础题 下列方程是齐次方程的是（    ）\n(A) $y' + y = 0$\n(B) $y^2 dx + x dy = 0$\n(C) $y' + xy = e^x$\n(D) $x^2 y' + xy = y^2$\n\n679 基础题 求微分方程 $\\frac{dy}{dx} = 2\\sqrt{\\frac{y}{x}} + \\frac{y}{x}$ 的通解.\n\n680 基础题 求微分方程 $\\frac{dy}{dx} = \\sec \\frac{y}{x} + \\frac{y}{x}$ 的通解.\n\n681 基础题 求微分方程 $\\frac{dy}{dx} = \\frac{x^2 + y^2}{xy}$ 满足初始条件 $y|_{x=1} = 2$ 的特解.\n\n682 基础题 已知曲线 $y = y(x)$ 通过点 $(1, 0)$，且每一点 $(x, y)$ 处切线的斜率等于 $1 + \\frac{y}{x} + \\left(\\frac{y}{x}\\right)^2$，求该曲线的方程.\n\n683 中等题 求微分方程 $y(x - y)dx + x^2dy = 0$ 满足初始条件 $y|_{x=1} = 1$ 的特解.\n\n684 中等题 求微分方程 $xy' + y(\\ln x - \\ln y) = 0$ 满足初始条件 $y(1) = e^3$ 的特解.\n\n685 中等题 求微分方程 $(1 + 2e^{\\frac{x}{y}})dx + 2e^{\\frac{x}{y}}(1 - \\frac{x}{y})dy = 0$ 的通解."}}
{"page":"101","result":{"chunk_id":"ded04a","wall_time_seconds":0.000007333,"exit_code":0,"original_token_count":442,"output":"686 中等题 求微分方程 $\\left( 2 y \\sin \\frac{x}{y} + 3 x \\cos \\frac{x}{y} \\right) \\mathrm{d} y - 3 y \\cos \\frac{x}{y} \\mathrm{d} x = 0$ 的通解.\n\n第四节 一阶线性微分方程\n\n一、一阶线性齐次方程的定义\n\n定义：形如 $\\frac{\\mathrm{d} y}{\\mathrm{d} x} + P (x) y = 0$ 的微分方程称为一阶线性齐次方程.\n\n评注 一阶线性齐次方程其实是特殊的变量可分离方程.\n\n二、一阶线性齐次方程的求解方法\n\n方法1：分离变量，两端积分，化简整理.\n\n方法2：套公式 $y = C \\mathrm{e}^{- \\int P (x) \\mathrm{d} x}$，$C$ 为任意常数.\n\n687 基础题 求微分方程 $\\frac{\\mathrm{d} y}{\\mathrm{d} x} + 2 x y = 0$ 的通解.\n\n688 基础题 求微分方程 $\\frac{\\mathrm{d} y}{\\mathrm{d} x} = y \\tan x$ 满足初始条件 $y \\big|_{x=0} = 1$ 的特解.\n\n三、一阶线性非齐次方程的定义\n\n定义：形如 $\\frac{\\mathrm{d} y}{\\mathrm{d} x} + P (x) y = Q (x)$，$Q (x) \\neq 0$ 的微分方程称为一阶线性非齐次方程.\n\n四、一阶线性非齐次方程的求解方法\n\n方法1：常数变易法。把齐次方程通解 $y = C \\mathrm{e}^{- \\int P (x) \\mathrm{d} x}$ 中的 $C$ 换成关于 $x$ 的未知函数 $C (x)$，将 $y = C (x) \\mathrm{e}^{- \\int P (x) \\mathrm{d} x}$ 代入方程 $\\frac{\\mathrm{d} y}{\\mathrm{d} x} + P (x) y = Q (x)$ 中，求出 $C (x)$ 即可.\n\n方法2：套公式，$y = \\mathrm{e}^{- \\int P (x) \\mathrm{d} x} \\left( \\int Q (x) \\mathrm{e}^{ \\int P (x) \\mathrm{d} x} \\mathrm{d} x + C \\right)$，$C$ 为任意常数.\n\n689 基础题 下列方程是一阶线性微分方程的是（    ）.\n\n(A) $y' + y^2 = 0$\n\n(B) $\\left( \\frac{\\mathrm{d} y}{\\mathrm{d} x} \\right)^2 = \\sqrt {x y}$\n\n(C) $y' + x y = \\mathrm{e}^4 y + x^2$\n\n(D) $y' + \\sin (x y) = 1$"}}
{"page":"102","result":{"chunk_id":"25c1fd","wall_time_seconds":0.000007875,"exit_code":0,"original_token_count":329,"output":"690 基础题 求微分方程 $\\frac{dy}{dx} + 2xy = 4x$ 的通解.\n\n691 基础题 求微分方程 $y' + y\\cos x = e^{-\\sin x}$ 的通解.\n\n692 基础题 求微分方程 $(x+1)\\frac{dy}{dx} - y = e^x(x+1)^2$ 满足 $y(0) = 2$ 的特解.\n\n693 基础题 求微分方程 $y' + y\\cos x - e^{-\\sin x}\\ln x = 0$ 满足 $y(1) = 0$ 的特解.\n\n694 中等题 求微分方程 $(y^2 - 6x)y' + 2y = 0$ 的通解.\n\n695 中等题 求微分方程 $y^3dx + (2xy^2 - 1)dy = 0$ 的通解.\n\n696 中等题 求微分方程 $ydx + (x - 3y^2)dy = 0$ 满足初始条件 $y|_{x=1} = 1$ 的特解.\n\n697 中等题 求微分方程 $y' = \\frac{1}{x+y}$ 的通解.\n\n698 中等题 求微分方程 $ydx + (x+y)dy = 0$ 的通解.\n\n699 中等题 已知曲线 $y = f(x)$ 过 $(0,1)$ 点，且它在任意一点 $(x,y)$ 处的切线斜率等于 $\\sec x - f(x)\\tan x$，求该曲线方程.\n\n700 中等题 已知 $f(x)$ 为连续函数，且满足 $f(x) = \\int_0^x f(t)dt - x^2$，求函数 $f(x)$.\n\n701 中等题 设函数 $f(x)$ 连续，且满足 $\\int_0^x f(x-t)dt = \\int_0^x (x-t)f(t)dt + e^{-x} - 1$，求 $f(x)$ 的表达式.\n\n第五节 可降阶的高阶微分方程\n\n一、$y^{(k)} = f(x)$ 型的微分方程的求解方法\n\n解法：方程两边对 $x$ 积分 $n$ 次，即可求通解.\n\n702 基础题 求微分方程 $y^{(4)} = x$ 的通解."}}
{"page":"103","result":{"chunk_id":"f0e8c4","wall_time_seconds":0.000010166,"exit_code":0,"original_token_count":313,"output":"$y^{m} = e^{3x} + \\sin 2x$ 的通解.\n\n求微分方程 $y^{m} = xe^{x}$ 的通解.\n\n求微分方程 $y^{m} = \\frac{1}{1+x^{2}}$ 的通解.\n\n求微分方程 $y^{m} = e^{2x}$ 满足初始条件 $|y|_{x=1} = y'|_{x=1} = y''|_{x=1} = 0$ 的特解.\n\n已知一曲线经过点 $(0,1)$ 并在此点与直线 $y = \\frac{x}{2}$ + 1 相切，且满足 $y'' = x$，\n求此曲线方程.\n\n二、$y' = f(x,y')$ 型的微分方程的求解方法\n\n第 1 步：换元. 令 $y' = p$, 则 $y'' = p'$, 则原方程变为 $p' = f(x,p)$, 此方程为一阶方程.\n\n第 2 步：解方程 $p' = f(x,p)$. 设其解为 $p = \\varphi(x,C_1)$, 即 $y' = \\varphi(x,C_1)$.\n\n第 3 步：两端积分. 对 $y' = \\varphi(x,C_1)$ 两端积分即可得到原方程的通解为\n$y = \\int \\varphi(x,C_1) \\mathrm{d}x + C_2$.\n\n第 4 步：换元. 令 $y' = p$, 则 $y'' = 2y'^2 = 0$ 满足初始条件 $|y|_{x=0} = 0$, $y'|_{x=0} = -1$ 的特解.\n\n第 5 步：解方程 $2xy' = 2xy$ 满足初始条件 $|y|_{x=0} = 1$, $y'|_{x=0} = 3$ 的特解.\n\n三、$y' = f(y,y')$ 型的微分方程的求解方法\n\n第 1 步：换元. 令 $y' = p$, 则 $y'' = \\frac{dp}{dx} = \\frac{dp}{dy} = \\frac{dy}{dx} = p\\frac{dp}{dy}$, 则原方程变为\n$p\\frac{dp}{dy} = f(y,p)$, 此方程为一阶微分方程."}}
{"page":"104","result":{"chunk_id":"aaa389","wall_time_seconds":0.000006333,"exit_code":0,"original_token_count":448,"output":"第2步：解方程 $p \\frac{dp}{dy} = f(y,p)$.设其解为 $p=\\varphi(y,C_1)$，即 $y'=\\varphi(y,C_1)$.\n第3步：解方程 $y'=\\varphi(y,C_1)$.对 $y'=\\varphi(y,C_1)$分离变量可得 $\\frac{dy}{\\varphi(y,C_1)}=dx$，两端积分即可得到原方程的通解为 $\\int \\frac{1}{\\varphi(y,C_1)} dy=x+C_2$.\n\n评注\n注意方程 $y'=\\varphi(y,y')$ 与 $y'=\\varphi(y,y')$的区别，前者最大的特点是不含 $x$，故换元时，令 $y'=p$，要把 $p$ 看成 $y$ 的函数，从而 $y'=\\frac{dp}{dx}=\\frac{dp}{dy}=\\frac{dp}{dy}$.\n\n713基础题 求微分方程 $yy'+2(y')^2=0$ 的通解.\n\n714基础题 求微分方程 $yy'+(y')^2=0$ 满足初始条件 $y|_{x=0}=1$， $y'|_{x=0}=\\frac{1}{2}$ 的特解.\n\n715中等题 求微分方程 $y^3 y''-1=0$ 的通解.\n\n716中等题 求微分方程 $y''+(y')^2=1$ 满足初始条件 $y|_{x=0}=0$， $y'|_{x=0}=0$ 的特解.\n\n第六节 高阶线性微分方程\n\n一、二阶线性微分方程的定义\n\n定义：形如 $\\frac{d^2y}{dx^2}+P(x)\\frac{dy}{dx}+Q(x)y=f(x)$ 的方程称为二阶线性微分方程。当右端 $f(x)\\neq 0$ 时，方程叫作齐次的；当 $f(x)\\neq 0$ 时，方程叫作非齐次的.\n\n二、二阶线性微分方程解的结构\n\n定理1：如果函数 $y_1(x)$ 与 $y_2(x)$ 是方程 $\\frac{d^2y}{dx^2}+P(x)\\frac{dy}{dx}+Q(x)y=0$ 的两个解，则 $y=C_1y_1(x)+C_2y_2(x)$ 也是方程的解，其中 $C_1,C_2$ 为任意常数.\n\n定理2：如果函数 $y_1(x)$ 与 $y_2(x)$ 是方程 $\\frac{d^2y}{dx^2}+P(x)\\frac{dy}{dx}+Q(x)y=0$ 的两个线性无关的解，则 $y=C_1y_1(x)+C_2y_2(x)$ （ $C_1,C_2$ 为任意常数）是方程的通解.\n\n评注\n(1) 注意定理1 和定理2的区别：一个是解，一个是通解；\n(2) 函数 $y_1(x)$ 与 $y_2(x)$ 线性无关 $\\Leftrightarrow \\frac{y_1(x)}{y_2(x)}\\neq$ 常数."}}
{"page":"105","result":{"chunk_id":"403f90","wall_time_seconds":0.000006667,"exit_code":0,"original_token_count":415,"output":"定理 3: 如果函数 $y'(x)$ 是二阶非齐次线性方程 $\\frac{d^2y}{dx^2} + P(x)\\frac{dy}{dx} + Q(x)y = f(x)$ 的一个特解, $Y(x)$ 是对应的齐次方程 $\\frac{d^2y}{dx^2} + P(x)\\frac{dy}{dx} + Q(x)y = 0$ 的通解, 则 $y = y'(x) + Y(x)$ 是二阶非齐次线性方程的通解.\n\n评注\n(1) 由上述定理可得, 二阶非齐次线性方程的通解 = 它的一个特解 + 对应齐次方程的通解, 而要找二阶齐次方程的通解, 需要找到它的两个线性无关的解.\n(2) 上面的结论可推广到 $n$ 阶线性微分方程.\n\n定理 4: (叠加性) 设 $y_1^*(x)$ 与 $y_2^*(x)$ 分别是方程 $\\frac{d^2y}{dx^2} + P(x)\\frac{dy}{dx} + Q(x)y = f_1(x)$ 与 $\\frac{d^2y}{dx^2} + P(x)\\frac{dy}{dx} + Q(x)y = f_2(x)$ 的特解, 则 $y_1^*(x) + y_2^*(x)$ 是 $\\frac{d^2y}{dx^2} + P(x)\\frac{dy}{dx} + Q(x)y = f_1(x) + f_2(x)$ 的特解.\n\n717 基础题 下列函数组, 在其定义区间内线性无关的是 (    ).\n\n(A) $x^2, 2x^2$ (B) $\\sin x, \\cos x$\n(C) $\\sin 2x, \\sin x\\cos x$ (D) $e^{2x}, 3e^{2x}$\n\n718 基础题 方程 $(x-1)y'-xy'+y=0$ 的两个线性无关的解是 (    ).\n\n(A) $x, 2x$ (B) $e^x, 8e^x$\n(C) $x, x^2$ (D) $x, e^x$\n\n719 基础题 已知 $y_1(x)$ 是一阶线性非齐次方程 $y'+p(x)y=f(x)$ 的一个解, $y_2(x)\\neq 0$ 是对应的齐次方程的一个解, 则方程 $y'+p(x)y=f(x)$ 的通解是 (    ).\n\n(A) $y=Cy_1(x)+y_2(x)$ (B) $y=Cy_1(x)-y_2(x)$\n(C) $y=y_1(x)-Cy_2(x)$ (D) $y=y_1(x)+y_2(x)+C$\n\n720 基础题 已知 $y_1(x)$ 与 $y_2(x)$ 是方程 $y'+p(x)y=0$ 的两个不同的解, 则该方程的通解是 (    ).\n\n(A) $y=Cy_1(x)$ (B) $y=Cy_2(x)$\n(C) $y=C_1y_1(x)+C_2y_2(x)$ (D) $y=C(y_1(x)-y_2(x))$"}}
{"page":"106","result":{"chunk_id":"db9b87","wall_time_seconds":0.00000825,"exit_code":0,"original_token_count":544,"output":"已知 $f_{1}(x)$ 与 $f_{2}(x)$ 是方程 $y'' + py' + qy = 0$ 的两个不同的非零解，$C_{1}, C_{2}$ 为任意常数，则 $y = C_{1}f_{1}(x) + C_{2}f_{2}(x)$ 是该方程通解的充分条件是（    ）\n(A) $f_{1}(x)f_{2}'(x) - f_{2}(x)f_{1}'(x) = 0$\n(B) $f_{1}(x)f_{2}'(x) + f_{2}(x)f_{1}'(x) = 0$\n(C) $f_{1}(x)f_{2}'(x) - f_{2}(x)f_{1}'(x) \\neq 0$\n(D) $f_{1}(x)f_{2}'(x) + f_{2}(x)f_{1}'(x) \\neq 0$\n\n722 基础题 验证 $y_{1} = \\cos ax$，$y_{2} = \\sin ax$ 都是方程 $y'' + a^{2}y = 0$ ($a \\neq 0$) 的解，并写出该方程的通解.\n\n723 基础题 验证 $y = C_{1}e^{x} + C_{2}e^{2x} + \\frac{1}{12}e^{5x}$ ($C_{1}, C_{2}$ 为任意常数）是方程 $y'' - 3y' + 2y = e^{5x}$ 的通解.\n\n724 基础题 设 $y_{1}(x)$，$y_{2}(x)$，$y_{3}(x)$ 是方程 $y'' + p(x)y' + q(x)y = f(x)$ 的三个线性无关的解，$C_{1}, C_{2}$ 为任意常数，证明 $y = 2C_{1}y_{1} + (C_{2} - C_{1})y_{2} + (1 - C_{1} - C_{2})y_{2}$ 是该方程的通解.\n\n第七节 常系数齐次线性微分方程\n\n一、二阶常系数齐次线性微分方程的定义\n\n定义：形如 $y'' + py' + qy = 0$ （其中 $p, q$ 为常数）的微分方程称为二阶常系数齐次线性微分方程.\n\n二、二阶常系数齐次线性微分方程的解法\n\n第1步：写出特征方程 $r^{2} + pr + q = 0$ .\n第2步：求出特征方程的两个根（特征根） $r_{1}, r_{2}$ .\n第3步：根据特征方程的两个根的不同情形，按照下表写出通解.\n\n| 特征方程 $r^{2} + pr + q = 0$ 的两个根 $r_{1}, r_{2}$ | 微分方程 $y'' + py' + qy = 0$ 的通解 |\n| :--- | :--- |\n| 两个不相等的实根 $r_{1} \\neq r_{2}$ | $y = C_{1}e^{x} + C_{2}e^{2x}$ |\n| 两个相等的实根 $r_{1} = r_{2}$ | $y = (C_{1} + C_{2})e^{x}$ |\n| 一对共轭复根 $r_{1,2} = \\alpha \\pm \\beta i$ | $y = e^{\\alpha x} (C_{1} \\cos \\beta x + C_{2} \\sin \\beta x)$ |\n\n评注\n\n二阶常系数齐次线性微分方程的概念、求解方法和通解的形式，可推广到 $n$ 阶常系数齐次线性微分方程.\n\n725 基础题 下列函数可以作为方程 $y'' + 2y' = 0$ 的特解的是（    ）。\n(A) $y = e^{x}$\n(B) $y = e^{2x}$\n(C) $y = 1 + e^{-2x}$\n(D) $y = xe^{-2x}$"}}
{"page":"107","result":{"chunk_id":"6aa01a","wall_time_seconds":0.000006458,"exit_code":0,"original_token_count":507,"output":"726 基础题 通解为 $y = c_{1} \\mathrm{e}^{6 x} + c_{2} \\mathrm{e}^{-8 x}$ 的二阶常系数齐次线性微分方程为（ ）。\n(A) $y^{\\prime \\prime} + 2 y^{\\prime} + 4 8 y = 0$\n(B) $y^{\\prime \\prime} + 2 y^{\\prime} - 4 8 y = 0$\n(C) $y^{\\prime \\prime} - 2 y^{\\prime} + 4 8 y = 0$\n(D) $y^{\\prime \\prime} - 2 y^{\\prime} - 4 8 y = 0$\n\n727 基础题 以 $y_{1} = \\mathrm{e}^{2 x} \\sin 3 x$，$y_{2} = \\mathrm{e}^{2 x} \\cos 3 x$ 为特解的二阶常系数齐次线性微分方程为（ ）。\n(A) $y^{\\prime \\prime} + 4 y^{\\prime} + 1 3 y = 0$\n(B) $y^{\\prime \\prime} - 4 y^{\\prime} - 1 3 y = 0$\n(C) $y^{\\prime \\prime} + 4 y^{\\prime} - 1 3 y = 0$\n(D) $y^{\\prime \\prime} - 4 y^{\\prime} + 1 3 y = 0$\n\n728 基础题 已知 $y = \\mathrm{e}^{2 x}$ 是二阶常系数齐次线性微分方程 $y^{\\prime} + p y^{\\prime} + q y = 0$ 的一个特解，求 $p$ 和 $q$ 的值.\n\n729 基础题 求方程 $y^{\\prime \\prime} + 5 y^{\\prime} + 4 y = 0$ 的通解.\n\n730 基础题 求方程 $y^{\\prime \\prime} + 4 y^{\\prime} + 3 y = 0$ 满足初始条件 $y|_{x=0} = 2$，$y^{\\prime}|_{x=0} = 6$ 的特解.\n\n731 基础题 求方程 $4 y^{\\prime \\prime} - 1 2 y^{\\prime} + 9 y = 0$ 的通解.\n\n732 基础题 求方程 $\\frac{d^{2} s}{d r^{2}} + 2 \\frac{d s}{d t} + s = 0$ 满足初始条件 $s|_{t=0} = 2$，$s^{\\prime}|_{t=0} = -1$ 的特解.\n\n733 基础题 求方程 $y^{\\prime \\prime} + 8 y^{\\prime} + 1 7 y = 0$ 的通解.\n\n734 基础题 求方程 $y^{\\prime \\prime} + 1 0 y^{\\prime} + 2 9 y = 0$ 满足初始条件 $y|_{x=0} = 1$，$y^{\\prime}|_{x=0} = -1$ 的特解.\n\n735 基础题 求方程 $y^{\\prime \\prime} + y^{\\prime} - y^{\\prime} - y = 0$ 的通解.\n\n736 基础题 求方程 $y^{(4)} - y^{\\prime \\prime} - y^{\\prime} - 2 y = 0$ 的通解.\n\n737 中等题 已知函数 $f(x)$ 满足 $f^{\\prime}(x) = f\\left(\\frac{\\pi}{2} - x\\right)$，且 $f(0) = f^{\\prime}(0) = 1$，求 $f(x)$.\n\n738 中等题 已知函数 $f(x)$ 满足方程 $f^{\\prime}(x) + f^{\\prime}(x) - 2 f(x) = 0$ 及 $f^{\\prime}(x) + f(x) = 2 \\mathrm{e}^{x}$，求 $f(x)$."}}
{"page":"108","result":{"chunk_id":"bdff63","wall_time_seconds":0.000008125,"exit_code":0,"original_token_count":469,"output":"第八节 常系数非齐次线性微分方程\n\n一、二阶常系数非齐次线性微分方程的定义\n\n定义：形如 $y'' + py' + qy = f(x)$ （其中 $p, q$ 为常数）的微分方程称为二阶常系\n数非齐次线性微分方程.\n\n二、二阶常系数非齐次线性微分方程的解法\n\n第1步：求 $y'' + py' + qy = f(x)$ 的一个特解 $y'(x)$.\n\n第2步：求出对应齐次方程的通解 $Y(x)$.\n\n第3步：写出方程 $y'' + py' + qy = f(x)$ 的通解 $y = y'(x) + Y(x)$.\n\n三、二阶常系数非齐次线性微分方程特解的求法\n\n情形一：若 $f(x) = P_{n}(x)$，$P_{n}(x)$ 是 $x$ 的 $n$ 次多项式，则\n\n(1) 当 $0$不是特征方程的根时，设\n$y'' = R_{n}(x) = a_{0} + a_{1}x + a_{2}x^{2} + \\cdots + a_{n}x^{n}$;\n\n(2) 当 $0$是特征方程的单根时，设\n$y'' = xR_{n}(x) = a_{0}x + a_{1}x^{2} + a_{2}x^{3} + \\cdots + a_{n}x^{n+1}$;\n\n(3) 当 $0$是特征方程的重根时，设\n$y'' = x^{2}R_{n}(x) = a_{0}x^{2} + a_{1}x^{3} + a_{2}x^{4} + \\cdots + a_{n}x^{n+2}$.\n\n739 基础题 求方程 $y'' - 4y' + 3y = x$ 的一个特解.\n\n740 基础题 求方程 $y'' + 5y' + 4y = 3 - 2x$ 的通解.\n\n741 基础题 求方程 $2y'' + 5y' = 5x^{2} - 2x - 1$ 的通解.\n\n742 中等题 若二阶常系数线性齐次微分方程 $y'' + ay' + by = 0$ 的通解为 $y = (C_{1} +$\n$C_{2}x)e^{x}$，求非齐次方程 $y'' + ay' + by = x$ 满足初始条件 $y(0) = 2$，$y'(0) = 0$ 的特解.\n\n情形二：若 $f(x) = e^{\\alpha x}P_{n}(x)$，$P_{n}(x)$ 是 $x$ 的 $n$ 次多项式，则\n\n(1) 当 $\\alpha$不是特征方程的根时，设\n$y'' = e^{\\alpha x}R_{n}(x) = e^{\\alpha x}(a_{0} + a_{1}x + a_{2}x^{2} + \\cdots + a_{n}x^{n})$;\n\n(2) 当 $\\alpha$是特征方程的单根时，设\n$y'' = xe^{\\alpha x}R_{n}(x) = e^{\\alpha x}(a_{0}x + a_{1}x^{2} + a_{2}x^{3} + \\cdots + a_{n}x^{n+1})$;\n\n(3) 当 $\\alpha$是特征方程的重根时，设"}}
{"page":"109","result":{"chunk_id":"378d74","wall_time_seconds":0.000006125,"exit_code":0,"original_token_count":459,"output":"$y^{*} = x^{2}e^{\\alpha x}R_{n}(x) = e^{\\alpha x}(a_{0}x^{2} + a_{1}x^{3} + a_{2}x^{4} + \\cdots + a_{n}x^{n+2})$.\n\n743 基础题 设 $a,b,c$ 为常数，则微分方程 $y^{*} - 5y^{*} + 6y = 3x + 2e^{2x}$ 的特解形式为\n(    ).\n(A) $e^{2x}(ax + b)$\n(B) $x e^{2x}(ax + b)$\n(C) $ax + b + c e^{2x}$\n(D) $ax + b + c x e^{2x}$\n\n744 基础题 求方程 $y^{*} - 3y^{*} + 2y = x e^{2x}$ 的通解.\n\n745 基础题 已知 $y = e^{-2x} + (x^{2} + 2)e^{x}$ 是二阶常系数线性非齐次微分方程 $y^{*} + ay^{*} +$\n$by = (cx + d)e^{x}$ 的一个解，求 $a,b,c,d$ 的值.\n\n746 中等题 已知 $y_{1} = e^{2x} + x e^{x}$, $y_{2} = e^{-x} + x e^{x}$, $y_{3} = e^{2x} - e^{-x} + x e^{x}$ 是某二阶常系\n数线性非齐次微分方程的三个解，求此微分方程.\n\n情形三：若 $f(x) = e^{\\alpha x}[P_{1}(x)\\cos \\beta x + Q_{2}(x)\\sin \\beta x]$, 则\n(1) 当 $\\alpha \\pm \\beta i$不是特征方程的根时，设 $y^{*} = e^{\\alpha x}(R_{m}^{(1)} \\cos \\beta x + R_{m}^{(2)} \\sin \\beta x)$；\n(2) 当 $\\alpha \\pm \\beta i$是特征方程的根时，设 $y^{*} = x e^{\\alpha x}(R_{m}^{(1)} \\cos \\beta x + R_{m}^{(2)} \\sin \\beta x)$，\n其中，$R_{m}^{(1)}$、$R_{m}^{(2)}$是 $m$ 次多项式，$m = \\max \\{l, n\\}$.\n\n747 基础题 微分方程 $y^{*} - 2y^{*} + 5y = e^{x} \\cos 2x$ 有特解 (    ).\n(A) $y^{*} = x e^{x}(\\cos 2x + \\sin 2x)$\n(B) $y^{*} = e^{x}(\\cos 2x + \\sin 2x)$\n(C) $y^{*} = \\frac{1}{4} x e^{x} \\cos 2x$\n(D) $y^{*} = \\frac{1}{4} x e^{x} \\sin 2x$\n\n748 基础题 设 $a,b,c$ 为常数，微分方程 $y^{*} + 4y = \\cos^{2} x$ 有特解 (    ).\n(A) $y^{*} = a \\cos^{2} x$\n(B) $y^{*} = x(a + b \\cos 2x + c \\sin 2x)$\n(C) $y^{*} = b \\sin^{2} x$\n(D) $y^{*} = a + b(x \\cos 2x + c \\sin 2x)$\n\n749 基础题 求方程 $y^{*} + 4y = x \\cos x$ 的通解.\n\n750 中等题 求方程 $y^{*} - y = e^{x} + 4 \\cos x$ 的通解."}}

## tool · 2026-10-20T02:27:38Z




## tool · 2026-10-20T02:29:17Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"bda979","wall_time_seconds":0.000008291,"exit_code":0,"original_token_count":1136,"output":"\\section{第7章 微分方程}\n\\subsection{微分方程的基本概念}\n\\begin{supplement}{7.1-1}{解族、奇解与初值唯一性}\n验证 $y=(x-C)^2$ 在 $x\\ge C$ 上满足 $y'=2\\sqrt y$，并验证 $y\\equiv0$ 也是解。对初值 $y(0)=0$，构造至少两个在 $[0,+\\infty)$ 上不同的解，说明直接分离变量可能遗漏什么解。\n\\end{supplement}\n\\begin{supplement}{7.1-2}{消去常数与微分方程阶数}\n消去曲线族 $y=C_1e^x+C_2e^{-x}+x$ 中的任意常数，建立二阶微分方程。再求该方程满足 $y(0)=1$、$y'(0)=0$ 的特解，并核验两个初始条件。\n\\end{supplement}\n\\subsection{可分离变量的微分方程}\n\\begin{supplement}{7.2-1}{平衡解与最大存在区间}\n求初值问题 $y'=y^2$、$y(0)=a$ 的解，包括 $a=0$ 的情形；分别确定 $a>0$ 与 $a<0$ 时包含 $0$ 的最大存在区间，并讨论 $x\\to+\\infty$ 时解是否有意义。\n\\end{supplement}\n\\begin{supplement}{7.2-2}{受限增长与阈值时间}\n种群满足 $N'=rN(1-N/K)$，其中 $r,K>0$、$N(0)=N_0\\in(0,K)$。求 $N(t)$，证明其单调增加且趋于 $K$；当 $N_0<K/2$ 时，求首次达到 $K/2$ 的时间。\n\\end{supplement}\n\\subsection{齐次方程}\n\\begin{supplement}{7.3-1}{齐次代换与不可跨越的奇点}\n求微分方程 $xy'=y+x e^{y/x}$ 在 $x>0$ 上满足 $y(1)=0$ 的解，并确定包含 $1$ 的最大存在区间。证明所得解无法在该区间右端连续延拓为有限值。\n\\end{supplement}\n\\begin{supplement}{7.3-2}{齐次方程与代换遗漏解}\n求 $xy'=y+y^2/x$ 在 $x>0$ 上的全部解，包括代换分离时可能遗漏的解；对初值 $y(1)=a$，确定解的表达式及包含 $1$ 的最大存在区间。\n\\end{supplement}\n\\subsection{一阶线性微分方程}\n\\begin{supplement}{7.4-1}{积分因子与有界解}\n求方程 $y'+2y=1+e^{-x}$ 的通解；判断是否存在在整个实轴上有界的解，证明你的判断。再求所有解在 $x\\to+\\infty$ 时的极限。\n\\end{supplement}\n\\begin{supplement}{7.4-2}{分段外力与连续拼接}\n某系统满足 $y'+y=u(x)$、$y(0)=0$，其中 $u(x)=1$（$0\\le x<1$）、$u(x)=0$（$x>1$）。分别求两个区间上的解，使 $y$ 在 $x=1$ 连续；判断 $y$ 在 $x=1$ 是否可导，并说明理由。\n\\end{supplement}\n\\subsection{可降阶的高阶微分方程}\n\\begin{supplement}{7.5-1}{不显含因变量的降阶}\n求初值问题 $xy''+y'=x$、$y(1)=0$、$y'(1)=1$ 在 $x>0$ 上的解，判断该解能否以二阶可导方式延拓到 $x=0$，并给出依据。\n\\end{supplement}\n\\begin{supplement}{7.5-2}{不显含自变量与能量积分}\n设 $y''=-y^3$、$y(0)=a>0$、$y'(0)=0$。通过降阶证明 $\\frac12(y')^2+\\frac14y^4=\\frac14a^4$；在解首次降到 $0$ 之前确定 $y'$ 的符号，并用定积分表示首次到达 $0$ 的时间，证明该时间有限。\n\\end{supplement}\n\\subsection{高阶线性微分方程}\n\\begin{supplement}{7.6-1}{解的叠加与初始条件}\n设 $y_1,y_2$ 是方程 $y''+p(x)y'+q(x)y=f(x)$ 的两个解。证明 $\\alpha y_1+(1-\\alpha)y_2$ 仍为解，并说明一般线性组合成为解所需的条件。取 $f\\not\\equiv0$ 时，判断 $y_1+y_2$ 与 $y_1-y_2$ 分别满足什么方程。\n\\end{supplement}\n\\begin{supplement}{7.6-2}{已知解降阶与基本解组}\n已知 $y_1=x$ 是 $x^2y''-2xy'+2y=0$ 在 $x>0$ 上的解。令 $y=xv(x)$ 求通解，证明所得两解线性无关，并求满足 $y(1)=0$、$y'(1)=1$ 的解。\n\\end{supplement}\n\\subsection{常系数齐次线性微分方程}\n\\begin{supplement}{7.7-1}{重根、参数与长期行为}\n求初值问题 $y''+2ay'+a^2y=0$、$y(0)=0$、$y'(0)=1$ 的解。讨论实参数 $a$ 使解在 $[0,+\\infty)$ 上有界或趋于零的条件，并在 $a>0$ 时求其最大值。\n\\end{supplement}\n\\begin{supplement}{7.7-2}{阻尼分类与无零点条件}\n考虑 $y''+2\\zeta y'+y=0$，$y(0)=1$、$y'(0)=0$，其中 $\\zeta\\ge0$。分别求 $0\\le\\zeta<1$、$\\zeta=1$、$\\zeta>1$ 时的解，并确定解在 $x>0$ 上始终为正的参数范围。\n\\end{supplement}\n\\subsection{常系数非齐次线性微分方程}\n\\begin{supplement}{7.8-1}{共振与参数分类}\n对 $\\omega>0$，求初值问题 $y''+y=\\cos\\omega x$、$y(0)=y'(0)=0$ 的解，分别讨论 $\\omega\\ne1$ 与 $\\omega=1$。判断解有界的参数条件，并说明共振时无界项的来源。\n\\end{supplement}\n\\begin{supplement}{7.8-2}{指数多项式外力与特解形式}\n求 $y''-2y'+y=e^x(x+1)$ 的通解及满足 $y(0)=y'(0)=0$ 的特解。先写出待定系数法所需的特解形式，并用 $y=e^xv$ 的代换核验计算结果。\n\\end{supplement}\n"}
{}

## tool · 2026-10-20T02:29:58Z




## tool · 2026-10-20T02:31:06Z


Script completed
Wall time 0.0 seconds
Output:

{}

## tool · 2026-10-20T02:31:12Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"234e02","wall_time_seconds":0.000017083,"exit_code":0,"original_token_count":160,"output":"013-crop0.0-0.55.md\n013-crop0.45-1.0.md\n014-crop0.0-0.55.md\n014-crop0.45-1.0.md\n015-crop0.0-0.55.md\n015-crop0.45-1.0.md\n019-crop0.0-0.55.md\n019-crop0.45-1.0.md\n023-crop0.0-0.55.md\n023-crop0.45-1.0.md\n024-crop0.0-0.55.md\n024-crop0.45-1.0.md\n044-crop0.0-0.55.md\n044-crop0.45-1.0.md\n045-crop0.0-0.55.md\n045-crop0.45-1.0.md\n048-crop0.0-0.55.md\n048-crop0.45-1.0.md\n049-crop0.0-0.55.md\n049-crop0.45-1.0.md\n050-crop0.0-0.55.md\n050-crop0.45-1.0.md\n076-crop0.0-0.55.md\n076-crop0.45-1.0.md\n077-crop0.0-0.55.md\n077-crop0.45-1.0.md\n078-crop0.0-0.55.md\n078-crop0.45-1.0.md\n079-crop0.0-0.55.md\n079-crop0.45-1.0.md\n080-crop0.0-0.55.md\n080-crop0.45-1.0.md\n"}
{"chunk_id":"8adae9","wall_time_seconds":0.00001425,"exit_code":0,"original_token_count":3738,"output":"Warning: truncated output (original token count: 3738)\nTotal output lines: 178\n\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{660}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{661}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{662}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{663}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{665}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{666}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{667}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{669}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{670}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{671}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{672}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{673}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{674}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{675}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{676}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{678}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{679}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{680}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{681}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{682}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{683}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{684}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{685}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{686}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{687}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{688}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{690}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{691}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{692}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{693}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{694}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{695}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{696}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{697}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{698}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{699}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{700}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{701}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{702}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{715}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{716}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{717}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{718}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{719}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{720}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{721}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{722}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{723}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{724}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{725}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{726}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{727}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{729}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{730}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{731}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{732}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{733}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{734}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{739}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{740}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{741}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{742}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{743}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{744}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{745}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{746}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{747}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{748}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{749}\noutput/工科数学分析逐题训练-上册/chapters/ch07.tex:\\begin{problem}{750}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{601}\noutput/工科数学分析逐题训…738 tokens truncated…pters/ch06.tex:\\begin{problem}{641}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{642}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{643}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{644}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{645}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{646}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{647}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{648}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{649}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{650}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{651}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{653}\noutput/工科数学分析逐题训练-上册/chapters/ch06.tex:\\begin{problem}{656}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{506}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{507}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{508}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{509}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{512}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{516}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{517}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{519}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{520}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{521}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{522}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{523}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{524}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{525}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{530}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{531}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{532}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{533}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{534}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{535}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{536}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{537}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{538}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{539}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{540}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{542}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{543}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{544}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{545}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{546}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{547}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{549}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{551}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{552}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{555}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{556}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{558}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{561}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{563}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{564}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{565}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{566}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{567}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{578}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{579}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{580}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{581}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{583}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{584}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{585}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{586}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{587}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{588}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{590}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{591}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{593}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{595}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{597}\noutput/工科数学分析逐题训练-上册/chapters/ch05.tex:\\begin{problem}{599}\n"}

## tool · 2026-10-20T02:31:19Z


Script completed
Wall time 0.6 seconds
Output:

{"page":"076","result":{"chunk_id":"555efb","wall_time_seconds":0.000016167,"exit_code":0,"original_token_count":373,"output":"二、定积分的性质\n\n规定: (1) $\\int_{a}^{a} f(x) \\mathrm{d}x = 0$; (2) $\\int_{a}^{b} f(x) \\mathrm{d}x = -\\int_{b}^{a} f(x) \\mathrm{d}x$.\n\n性质 1: (线性性质) $\\int_{a}^{b} [\\alpha f(x) + \\beta g(x)] \\mathrm{d}x = \\alpha \\int_{a}^{b} f(x) \\mathrm{d}x + \\beta \\int_{a}^{b} g(x) \\mathrm{d}x$. ($\\alpha, \\beta$均为常数).\n\n性质 2: (区间可加性) $\\int_{a}^{b} f(x) \\mathrm{d}x = \\int_{a}^{c} f(x) \\mathrm{d}x + \\int_{c}^{b} f(x) \\mathrm{d}x$.\n\n性质 3: $\\int_{a}^{b} 1 \\mathrm{d}x = \\int_{a}^{b} \\mathrm{d}x = b - a$.\n\n性质 4: 若 $f(x) \\geq 0$, $x \\in [a, b]$, 则 $\\int_{a}^{b} f(x) \\mathrm{d}x \\geq 0$.\n\n推论 1: (比较性质) 若 $f(x) \\leq g(x)$, $x \\in [a, b]$, 则 $\\int_{a}^{b} f(x) \\mathrm{d}x \\leq \\int_{a}^{b} g(x) \\mathrm{d}x$.\n\n推论 2: $\\left| \\int_{a}^{b} f(x) \\mathrm{d}x \\right| \\leq \\int_{a}^{b} \\left| f(x) \\right| \\mathrm{d}x$.\n\n性质 5: (估值定理) 设 $M$ 和 $m$ 是 $f(x)$ 在区间 $[a, b]$ 上的最大值与最小值, 则 $m(b-a) \\leq \\int_{a}^{b} f(x) \\mathrm{d}x \\leq M(b-a)$.\n\n性质 6: (中值定理) 设函数 $f(x)$ 在区间 $[a, b]$ 上连续, 则在 $[a, b]$ 上至少存在一个点 $\\xi$, 使得 $\\int_{a}^{b} f(x) \\mathrm{d}x = f(\\xi)(b-a)$.\n\n$f(\\xi) = \\frac{1}{(b-a)} \\int_{a}^{b} f(x) \\mathrm{d}x$ 称为函数 $f(x)$ 在区间 $[a, b]$ 上的平均值.\n\n505 基础题 $[\\int_{a}^{b} \\arcsin x \\mathrm{d}x]' =$ (    ).\n\n(A) $\\arcsin x$ (B)0 (C) $\\frac{1}{\\sqrt{1-b^2}} - \\frac{1}{\\sqrt{1-a^2}}$ (D) $\\frac{1}{\\sqrt{1-x^2}}$"}}
{"page":"077","result":{"chunk_id":"935005","wall_time_seconds":0.000013292,"exit_code":0,"original_token_count":285,"output":"511 基础题 设 $ I_{1}=\\int_{0}^{\\pi} \\sqrt{1+x^{2}} \\mathrm{d} x, I_{2}=\\int_{0}^{\\pi} \\sqrt{1+x^{3}} \\mathrm{d} x $ ，则 $ I_{1} $与 $ I_{2} $的大小关系是（    ）\n(A) $ I_{1}>I_{2} $\n(B) $ I_{1}\\geqslant I_{2} $\n(C) $ I_{1}<I_{2} $\n(D) $ I_{1}\\leqslant I_{2} $\n512 基础题 估计定积分 $ I=\\int_{\\frac{\\pi}{4}}^{\\pi}(1+\\cos^{2} x) \\mathrm{d} x $的值.\n513 中等题 估计定积分 $ I=\\int_{0}^{1} \\frac{x^{9}}{\\sqrt{1+x}} \\mathrm{d} x $的值.\n514 综合题 设 $ I=\\int_{\\frac{\\pi}{4}}^{\\frac{\\pi}{2}} \\frac{\\sin x}{x} \\mathrm{d} x $，证明 $ \\frac{\\sqrt{2}}{4}\\leqslant I\\leqslant\\frac{\\sqrt{2}}{2} $\n515 中等题 设 $ f(x) $在 $ [a,b] $上连续，在 $ (a,b) $内可导，且 $ \\frac{2}{b-a}\\int_{a}^{a+b} f(x) \\mathrm{d} x=f(b) $\n证明在 $ (a,b) $内至少存在一点 $ \\xi $，使得 $ f^{\\prime}(\\xi)=0 $\n516 中等题 设 $ f(x) $在 $ [a,b] $上连续，在 $ (a,b) $内可导，且 $ f^{\\prime}(x)\\leqslant0 $\n证明 $ F(x)=\\frac{1}{x-a}\\int_{a}^{x} f(t) \\mathrm{d} t $在 $ (a,b) $内满足 $ F^{\\prime}(x)\\leqslant0 $\n517 基础题 求函数 $ f(x)=\\sqrt{4-x^{2}} $在 $ [-2,2] $上的平均值."}}
{"page":"078","result":{"chunk_id":"58b5d1","wall_time_seconds":0.000015083,"exit_code":0,"original_token_count":207,"output":"519 基础题 设 $ y=\\int_{0}^{x^{2}}\\sqrt{1+t^{2}}\\mathrm{d}t $ ，求 $ \\frac{\\mathrm{d}y}{\\mathrm{d}x} $ .\n520 基础题 设 $ y=\\int_{x^{2}}^{x^{2}}\\frac{\\mathrm{d}t}{\\sqrt{1+t^{2}}} $ ，求 $ \\frac{\\mathrm{d}y}{\\mathrm{d}x} $ .\n521 中等题 求极限 $ \\lim_{x\\to 0}\\frac{\\int_{0}^{x}\\cos t^{2}\\mathrm{d}t}{x} $ .\n522 中等题 求极限 $ \\lim_{x\\to 0}\\frac{\\int_{0}^{x}\\arctan t\\mathrm{d}t}{x^{2}}. $\n523 中等题 求极限 $ \\lim_{x\\to 0}\\frac{\\left(\\int_{0}^{x}\\mathrm{e}^{t^{2}}\\mathrm{d}t\\right)^{2}}{\\int_{0}^{x}t\\mathrm{e}^{2t^{2}}\\mathrm{d}t} $ .\n524 中等题 求极限 $ \\lim_{x\\to 0}\\frac{\\int_{0}^{x}f(t)(x-t)\\mathrm{d}t}{x^{2}} $ ，其中 $ f(x) $ 是 $ (-\\infty,+\\infty) $ 内的连续函数.\n525 中等题 求极限 $ \\lim_{x\\to+\\infty}\\frac{\\int_{0}^{x}(\\arctan t)^{2}\\mathrm{d}t}{\\sqrt{1+x^{2}}} $"}}
{"page":"079","result":{"chunk_id":"85ff53","wall_time_seconds":0.000013417,"exit_code":0,"original_token_count":215,"output":"$\\int_{a}^{b} f(x) \\mathrm{d}x = F(x) \\big|_{a}^{b} = F(b) - F(a).$\n此为牛顿-莱布尼茨公式，也称微积分基本公式.\n\n530 基础题 求定积分 $\\int_{0}^{\\frac{1}{2}} \\mathrm{e}^{2x} \\mathrm{d}x$.\n\n531 基础题 求定积分 $\\int_{0}^{2} \\frac{x}{\\sqrt{1+x^{2}}} \\mathrm{d}x$.\n\n532 基础题 求定积分 $\\int_{0}^{1} \\frac{\\mathrm{d}x}{x^{2}+5x+6}$.\n\n533 基础题 求定积分 $\\int_{-1}^{3} |2-x| \\mathrm{d}x$.\n\n534 基础题 求定积分 $\\int_{0}^{2\\pi} |\\sin x| \\mathrm{d}x$.\n\n535 中等题 设 $f(x) = \\left\\{ \\begin{array}{ll} 2x, & 0 \\leqslant x \\leqslant 1 \\\\ 2+x, & 1 < x \\leqslant 2 \\end{array} \\right.$，求积分上限函数 $P(x) = \\int_{0}^{x} f(t) \\mathrm{d}t$ 在 $[0, 2]$ 上的表达式.\n\n536 中等题 设 $f(x) = \\frac{1}{1+x^{2}} + \\sqrt{1-x^{2}} \\int_{0}^{1} f(x) \\mathrm{d}x$，求 $\\int_{0}^{1} f(x) \\mathrm{d}x$."}}
{"page":"080","result":{"chunk_id":"63d762","wall_time_seconds":0.000023959,"exit_code":0,"original_token_count":239,"output":"(2) 设函数 $f(x)$ 是以 $T$ 为周期的连续函数，则\n$$\\int_{-a}^{a} f(x) \\mathrm{d}x = \\int_{0}^{a} [f(x) + f(-x)] \\mathrm{d}x = \\left\\{ \\begin{array}{ll} 0 & \\text{当 } f(x) \\text{为奇函数时} \\\\ 2 \\int_{0}^{a} f(x) \\mathrm{d}x & \\text{当 } f(x) \\text{为偶函数时} \\end{array} \\right.$$\n$$\\int_{a}^{a+T} f(x) \\mathrm{d}x = \\int_{0}^{T} f(x) \\mathrm{d}x ; \\int_{a}^{a+T} f(x) \\mathrm{d}x = \\int_{- \\frac{T}{2}}^{\\frac{T}{2}} f(x) \\mathrm{d}x.$$\n\n539 基础题 计算 $\\int_{4}^{9} \\frac{\\sqrt{x}}{\\sqrt{x}-1} \\mathrm{d}x$.\n\n540 基础题 计算 $\\int_{0}^{1} x \\sqrt{3-2x} \\mathrm{d}x$.\n\n541 基础题 计算 $\\int_{1}^{e} \\frac{1}{x \\sqrt{1+\\ln x}} \\mathrm{d}x$.\n\n542 中等题 计算 $\\int_{-1}^{0} \\frac{(1+x) \\mathrm{e}^{x}}{\\sqrt{1+x \\mathrm{e}^{x}}} \\mathrm{d}x$.\n\n543 基础题 计算 $\\int_{0}^{\\frac{\\sqrt{2}}{3}} \\sqrt{2-9 x^{2}} \\mathrm{d}x$.\n\n544 基础题 计算 $\\int_{1}^{\\sqrt{3}} \\frac{\\mathrm{d}x}{x \\sqrt{1+x^{2}}}$."}}
{"page":"077top","result":{"chunk_id":"37073f","wall_time_seconds":0.000019084,"exit_code":0,"original_token_count":336,"output":"506 基础题 利用定积分的几何意义，求 $ \\int_{-2}^{2} \\sqrt{4-x^{2}} \\mathrm{d} x. $\n507 基础题 利用定积分的定义，求极限 $ \\lim_{n \\to \\infty} \\left( \\frac{1}{n^{2}}+\\frac{2}{n^{2}}+\\cdots+\\frac{n-1}{n^{2}} \\right). $\n508 基础题 利用定积分的定义，求极限 $ \\lim_{n \\to \\infty} \\left( \\frac{1}{n+1}+\\frac{1}{n+2}+\\cdots+\\frac{1}{n+n} \\right). $\n509 基础题 利用定积分的定义，求极限 $ \\lim_{n \\to \\infty} \\left( \\frac{n}{n^{2}+1^{2}}+\\frac{n}{n^{2}+2^{2}}+\\cdots+\\frac{n}{n^{2}+n^{2}} \\right). $\n510 基础题 下列各选项中满足 $ I_{1} \\leqslant I_{2} $的是（    ）.\n(A) $ I_{1}=\\int_{0}^{1} x^{2} \\mathrm{d} x, I_{2}=\\int_{0}^{1} x^{3} \\mathrm{d} x $\n(B) $ I_{1}=\\int_{0}^{1} x \\mathrm{d} x, I_{2}=\\int_{0}^{1} \\tan x \\mathrm{d} x $\n(C) $ I_{1}=\\int_{1}^{2} \\ln x \\mathrm{d} x, I_{2}=\\int_{1}^{2} \\ln^{2} x \\mathrm{d} x $\n(D) $ I_{1}=\\int_{0}^{1} \\mathrm{e}^{x} \\mathrm{d} x, I_{2}=\\int_{0}^{1}(1+x) \\mathrm{d} x $\n511 基础题 设 $ I_{1}=\\int_{0}^{1} \\sqrt{1+x^{2}} \\mathrm{d} x, I_{2}=\\int_{0}^{1} \\sqrt{1+x^{3}} \\mathrm{d} x $ ，则 $ I_{1} $与 $ I_{2} $的大小关系是（    ）.\n(A) $ I_{1}>I_{2} $\n(B) $ I_{1}\\geqslant I_{2} $\n(C) $ I_{1}<I_{2} $\n(D) $ I_{1}\\leqslant I_{2} $\n512 基础题 估计定积分 $ I=\\int_{\\pi}^{\\pi}(1+\\cos^{2} x) \\mathrm{d} x $的值."}}
{"page":"079top","result":{"chunk_id":"e003e4","wall_time_seconds":0.00001675,"exit_code":0,"original_token_count":266,"output":"526 基础题 求由 $\\int_{0}^{y} \\mathrm{e}^{\\prime} \\mathrm{d} t+\\int_{0}^{x} \\cos t \\mathrm{d} t=0$ 所确定的隐函数的导数 $\\frac{\\mathrm{d} y}{\\mathrm{d} x}$.\n\n527 中等题 设函数 $f(x)=\\int_{0}^{x} \\mathrm{e}^{-\\frac{1}{2} t^{2}} \\mathrm{d} t(-\\infty < x < +\\infty)$，求 $f(x)$ 的单调区间，并判断其奇偶性.\n\n528 中等题 设函数 $f(x)$ 连续，$\\varphi(x)=\\int_{0}^{x^{2}} x f(t) \\mathrm{d} t$，若 $\\varphi(1)=1$，$\\varphi^{\\prime}(1)=5$，求 $f(1)$.\n\n529 综合题 设函数 $f(x)$ 在 $[a,b]$ 上连续，且 $f(x)>0$.\n证明方程 $\\int_{a}^{x} f(t) \\mathrm{d} t+\\int_{b}^{x} \\frac{\\mathrm{d} t}{f(t)}=0$ 在区间 $(a,b)$ 内有且仅有一个实根.\n\n二、牛顿-莱布尼茨公式\n\n定理3:（微积分基本定理）如果函数 $F(x)$ 是连续函数 $f(x)$ 在区间 $[a,b]$ 上的一个原函数，则\n$$\\int_{a}^{b} f(x) \\mathrm{d} x=F(x)\\big|_{a}^{b}=F(b)-F(a).$$\n此为牛顿-莱布尼茨公式，也称微积分基本公式.\n\n530 基础题 求定积分 $\\int_{-1}^{\\frac{1}{2}} \\mathrm{e}^{2 x} \\mathrm{d} x$."}}

## tool · 2026-10-20T02:31:32Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"71c4ae","wall_time_seconds":0.000034875,"exit_code":0,"original_token_count":267,"output":"第二节 微积分基本公式\n\n一、积分上限函数及其导数\n\n设函数 $f(x)$ 在区间 $[a,b]$ 上可积，则称\n\n$$\\Phi(x) = \\int_{a}^{x} f(t) \\mathrm{d}t, x \\in [a,b]$$\n\n为积分上限函数或上限积分函数.\n\n定理1：如果函数 $f(x)$ 在区间 $[a,b]$ 上连续，则积分上限函数 $\\Phi(x) = \\int_{a}^{x} f(t) \\mathrm{d}t$ 在 $[a,b]$ 上可导，并且\n\n$$\\Phi'(x) = \\frac{\\mathrm{d}}{\\mathrm{d}x} \\int_{a}^{x} f(t) \\mathrm{d}t = f(x), x \\in [a,b].$$\n\n定理2：（原函数存在定理）如果函数 $f(x)$ 在区间 $[a,b]$ 上连续，则函数 $\\Phi(x) = \\int_{a}^{x} f(t) \\mathrm{d}t$ 是 $f(x)$ 在 $[a,b]$ 上的一个原函数.\n\n518 基础题 设 $f(x) = \\int_{a}^{b} \\sin x^{2} \\mathrm{d}x$，求 $\\frac{\\mathrm{d}f}{\\mathrm{d}x}, \\frac{\\mathrm{d}f}{\\mathrm{d}b}, \\frac{\\mathrm{d}f}{\\mathrm{d}a}$.\n\n519 基础题 设 $y = \\int_{0}^{x^{2}} \\sqrt{1+t^{2}} \\mathrm{d}t$，求 $\\frac{\\mathrm{d}y}{\\mathrm{d}x}$.\n\n520 基础题 设 $y = \\int_{0}^{x^{2}} \\frac{\\mathrm{d}t}{\\sqrt{1+t^{2}}}$，求 $\\frac{\\mathrm{d}y}{\\mathrm{d}x}$."}
{"page":"081","result":{"chunk_id":"057f16","wall_time_seconds":0.000010375,"exit_code":1,"original_token_count":30,"output":"cat: .agent/hdu-ocr/local/高等数学（上册）精选750题 (宋浩)/081-crop0.45-1.0.md: No such file or directory\n"}}
{"page":"082","result":{"chunk_id":"c87946","wall_time_seconds":0.000017709,"exit_code":1,"original_token_count":30,"output":"cat: .agent/hdu-ocr/local/高等数学（上册）精选750题 (宋浩)/082-crop0.45-1.0.md: No such file or directory\n"}}
{"page":"083","result":{"chunk_id":"387627","wall_time_seconds":0.000014375,"exit_code":1,"original_token_count":30,"output":"cat: .agent/hdu-ocr/local/高等数学（上册）精选750题 (宋浩)/083-crop0.45-1.0.md: No such file or directory\n"}}

## tool · 2026-10-20T02:32:12Z


Script completed
Wall time 0.2 seconds
Output:

{}
{"chunk_id":"fa7b46","wall_time_seconds":0.000017708,"exit_code":1,"original_token_count":97,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 97, in <module>\n    totals = check_structure()\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 59, in check_structure\n    assert \"TODO\" not in text and \"待补\" not in text and \"略\" not in text\nAssertionError\n"}

## tool · 2026-10-20T02:32:18Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"8f7165","wall_time_seconds":0.00001275,"exit_code":0,"original_token_count":313,"output":"import json\nimport math\nimport re\nfrom pathlib import Path\n\nROOT = Path(__file__).resolve().parents[3]\nCHAPTERS = ROOT / \"output/工科数学分析逐题训练-上册/chapters\"\nEXPECTED = {\n    5: [(505, 517), (518, 538), (539, 577), (578, 600)],\n    6: [(601, 649), (650, 656)],\n    7: [(657, 663), (664, 677), (678, 686), (687, 701),\n        (702, 716), (717, 724), (725, 738), (739, 750)],\n}\n\n\n        y = lambda t: math.log(math.cosh(t))\n        near(second(y, x) + derivative(y, x)**2, 1, 2e-6)\n        y = lambda t: math.exp(-2*t) + (t*t+2)*math.exp(t)\n        near(second(y, x) + derivative(y, x) - 2*y(x), (6*x+2)*math.exp(x), 2e-6)\n        y = lambda t: 0.25*t*math.exp(t)*math.sin(2*t)\n        near(second(y, x) - 2*derivative(y, x) + 5*y(x), math.exp(x)*math.cos(2*x), 2e-6)\n    return \"积分换元、对称性、面积体积、做功、曲率与微分方程代表计算通过\"\n\n\nif __name__ == \"__main__\":\n    mathematics = check_mathematics()\n    totals = check_structure()\n    print(json.dumps({\"status\": \"passed\", \"type\": \"read_only_check\",\n                      \"message\": mathematics, \"counts\": totals,\n                      \"suggestion\": \"本检查不替代排版编译与全部题目的逐项数学审查\"}, ensure_ascii=False))\n"}
{}
{"chunk_id":"1368f0","wall_time_seconds":0.000012334,"exit_code":1,"original_token_count":382,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 97, in <module>\n    totals = check_structure()\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 61, in check_structure\n    assert not errors, json.dumps(errors, ensure_ascii=False)\nAssertionError: [{\"chapter\": 5, \"section\": 1, \"missing\": [505, 510, 511, 513, 514, 515], \"extra\": [], \"in_order\": true}, {\"chapter\": 5, \"section\": 2, \"missing\": [518, 526, 527, 528, 529], \"extra\": [], \"in_order\": true}, {\"chapter\": 5, \"section\": 3, \"missing\": [541, 548, 550, 553, 554, 557, 559, 560, 562, 568, 569, 570, 571, 572, 573, 574, 575, 576, 577], \"extra\": [], \"in_order\": true}, {\"chapter\": 5, \"section\": 4, \"missing\": [582, 589, 592, 594, 596, 598, 600], \"extra\": [], \"in_order\": true}, {\"chapter\": 6, \"section\": 1, \"missing\": [602, 614, 624, 629], \"extra\": [], \"in_order\": true}, {\"chapter\": 6, \"section\": 2, \"missing\": [652, 654, 655], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 1, \"missing\": [657, 658, 659], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 2, \"missing\": [664, 668, 677], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 4, \"missing\": [689], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 5, \"missing\": [703, 704, 705, 706, 707, 708, 709, 710, 711, 712, 713, 714], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 7, \"missing\": [728, 735, 736, 737, 738], \"extra\": [], \"in_order\": true}]\n"}

## tool · 2026-10-20T02:32:24Z




## tool · 2026-10-20T02:33:11Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"f4f627","wall_time_seconds":0.000011709,"exit_code":0,"original_token_count":1014,"output":"\\section{第5章 定积分}\n\\subsection{定积分的概念与性质}\n\\begin{problem}{506}{77}{几何意义与尺度变换}\n利用定积分的几何意义求 $\\int_{-2}^{2}\\sqrt{4-x^2}\\dd x$，并推广计算 $\\int_{-r}^{r}\\sqrt{r^2-x^2}\\dd x$（$r>0$）。若仅将积分区间改为 $[0,r]$，解释结果与原积分的关系。\n\\end{problem}\n\\begin{problem}{507}{77}{黎曼和与端点影响}\n利用定积分定义求 $\\lim_{n\\to\\infty}\\sum_{k=1}^{n-1}\\frac{k}{n^2}$。对 $a>0$，再求 $\\lim_{n\\to\\infty}\\sum_{k=1}^{\\lfloor an\\rfloor}\\frac{k}{n^2}$，说明取整及有限个端点项为何不影响极限。\n\\end{problem}\n\\begin{problem}{508}{77}{黎曼和与积分夹逼}\n将 $\\sum_{k=1}^n\\frac1{n+k}$ 写成黎曼和并求其极限。再利用 $f(x)=1/(1+x)$ 的单调性，证明该和与其极限的差的绝对值不超过 $1/(2n)$。\n\\end{problem}\n\\begin{problem}{509}{77}{黎曼和与误差控制}\n利用定积分定义求 $S_n=\\sum_{k=1}^n\\frac{n}{n^2+k^2}$ 的极限。将 $S_n$ 与相应积分比较，确定误差符号，并证明误差的绝对值不超过 $1/(2n)$。\n\\end{problem}\n\\begin{problem}{512}{77}{积分估值与严格不等式}\n不求原函数，先证明 $\\pi<\\int_0^\\pi(1+\\cos^2x)\\dd x<2\\pi$。再计算积分的准确值，说明被积函数在有限个点达到最值为何不能使上述估值取等号。\n\\end{problem}\n\\begin{problem}{516}{77}{积分平均值的单调性}\n设 $f$ 在 $[a,b]$ 上连续、在 $(a,b)$ 内可导，且 $f'\\le0$。证明\n\\[\nF(x)=\\frac1{x-a}\\int_a^xf(t)\\dd t\n\\]\n在 $(a,b)$ 内满足 $F'(x)\\le0$。对固定的 $x_0\\in(a,b)$，证明 $F'(x_0)=0$ 当且仅当 $f$ 在 $[a,x_0]$ 上为常数。\n\\end{problem}\n\\begin{problem}{517}{77}{函数平均值与中值点}\n求 $f(x)=\\sqrt{4-x^2}$ 在 $[-2,2]$ 上的平均值，并求使函数值等于平均值的全部点。将半径 $2$ 改为 $r>0$ 后，求相应中值点与 $r$ 的比例关系。\n\\end{problem}\n\\begin{supplement}{5.1-1}{积分定义与黎曼和}\n设 $f$ 在 $[0,1]$ 上连续。用定积分表示极限\n\\[\n\\lim_{n\\to\\infty}\\sum_{k=1}^n\\frac{n}{n^2+k^2}f\\!\\left(\\frac{k}{n}\\right).\n\\]\n当 $f(x)=x$ 时求极限值；当 $f(x)\\ge0$ 且上述极限为零时，证明 $f\\equiv0$。\n\\end{supplement}\n\\begin{supplement}{5.1-2}{积分不等式与等号条件}\n设 $f$ 在 $[0,1]$ 上连续，且 $0\\le f(x)\\le1$、$\\int_0^1f(x)\\dd x=\\frac12$。证明\n\\[\n\\frac14\\le\\int_0^1f^2(x)\\dd x<\\frac12,\n\\]\n并完整讨论左端等号条件及右端不能取等号的原因。\n\\end{supplement}\n\\subsection{微积分基本公式}\n\\begin{problem}{519}{78}{积分上限函数与凹凸性}\n设 $y=\\int_0^x\\sqrt{1+t^2}\\dd t$。求 $y'$、$y''$，判断 $y$ 的奇偶性及单调性，并确定图像的凹凸区间和拐点。\n\\end{problem}\n43:\\begin{problem}{519}{78}{积分上限函数与凹凸性}\n44-设 $y=\\int_0^x\\sqrt{1+t^2}\\dd t$。求 $y'$、$y''$，判断 $y$ 的奇偶性及单调性，并确定图像的凹凸区间和拐点。\n45-\\end{problem}\n46-\\begin{problem}{520}{78}{双变限积分的求导}\n--\n55:\\begin{problem}{523}{78}{变限积分商的极限}\n56-求\n57-\\[\n58-\\lim_{x\\to0}\\frac{\\left(\\int_0^xe^{2t}\\dd t\\right)^2}{\\int_0^xte^{2t}\\dd t}.\n--\n68:\\begin{problem}{530}{79}{基本公式与参数积分}\n69-计算 $\\int_0^1\\frac12e^{2x}\\dd x$。对实参数 $a$，计算 $J(a)=\\int_0^1\\frac12e^{ax}\\dd x$，单独处理 $a=0$，并证明所得表达式在 $a=0$ 连续。\n70-\\end{problem}\n71-\\begin{problem}{531}{79}{原函数与参数上限}\n--\n77:\\begin{problem}{533}{79}{绝对值积分与参数最值}\n78-计算 $\\int_0^3|2-x|\\dd x$。对实数 $a$ 求 $H(a)=\\int_0^3|a-x|\\dd x$ 的分段表达式，并求 $H$ 的最小值及取到最小值的全部 $a$。\n79-\\end{problem}\n80-\\begin{problem}{534}{79}{绝对值积分与周期性}\n--\n118:\\begin{problem}{544}{80}{三角换元与无穷上限}\n119-计算 $\\int_1^{\\sqrt2}\\frac{\\dd x}{x\\sqrt{1+x^2}}$。求 $J(a)=\\int_1^a\\frac{\\dd x}{x\\sqrt{1+x^2}}$（$a\\ge1$），并求 $\\lim_{a\\to+\\infty}J(a)$。\n120-\\end{problem}\n121-\\begin{problem}{545}{81}{根式积分与反三角函数}\n"}
{}

## tool · 2026-10-20T02:34:19Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"085451","wall_time_seconds":0.000013083,"exit_code":0,"original_token_count":173,"output":"3:\\begin{problem}{601}{88}{平面面积与形心}\n6:\\begin{problem}{603}{88}{区域面积与旋转体积}\n36:\\begin{problem}{613}{89}{三角曲线之间的面积}\n39:\\begin{problem}{615}{89}{面积比与参数范围}\n63:\\begin{problem}{623}{91}{摆线参数积分与尺度关系}\n66:\\begin{problem}{625}{92}{双曲线截面与旋转体积}\n75:\\begin{problem}{628}{92}{负半轴区域与柱壳半径}\n78:\\begin{problem}{630}{92}{切线确定与双轴旋转}\n141:\\begin{supplement}{6.1-2}{弧长与旋转曲面面积}\n148:\\begin{problem}{651}{95}{漏失载荷与变力做功}\n151:\\begin{problem}{653}{96}{变力做功与几何级数}\n154:\\begin{problem}{656}{96}{弧长与均匀薄片形心}\n"}
{}
{"chunk_id":"d662a9","wall_time_seconds":0.000011208,"exit_code":1,"original_token_count":93,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 97, in <module>\n    totals = check_structure()\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 54, in check_structure\n    assert len(problems) == section.count(r\"\\end{problem}\")\nAssertionError\n"}

## tool · 2026-10-20T02:34:26Z


Script completed
Wall time 0.5 seconds
Output:

{"chunk_id":"0cac78","wall_time_seconds":0.000009459,"exit_code":0,"original_token_count":1049,"output":"     1\t\\section{第5章 定积分}\n     2\t\\subsection{定积分的概念与性质}\n     3\t\\begin{problem}{505}{76}{积分变量与参数求导}\n     4\t设常数 $-1<a<b<1$，记 $I=\\int_a^b\\arcsin t\\dd t$。分别求 $I$ 对无关变量 $x$、上限 $b$、下限 $a$ 的导数。若 $a=a(x),b=b(x)$ 为可导函数，写出 $\\frac\\dd{\\dd x}\\int_{a(x)}^{b(x)}\\arcsin t\\dd t$，说明哑变量命名不影响结果。\n     5\t\\end{problem}\n     6\t\\begin{problem}{506}{77}{几何意义与尺度变换}\n     7\t利用定积分的几何意义求 $\\int_{-2}^{2}\\sqrt{4-x^2}\\dd x$，并推广计算 $\\int_{-r}^{r}\\sqrt{r^2-x^2}\\dd x$（$r>0$）。若仅将积分区间改为 $[0,r]$，解释结果与原积分的关系。\n     8\t\\end{problem}\n     9\t\\begin{problem}{507}{77}{黎曼和与端点影响}\n    10\t利用定积分定义求 $\\lim_{n\\to\\infty}\\sum_{k=1}^{n-1}\\frac{k}{n^2}$。对 $a>0$，再求 $\\lim_{n\\to\\infty}\\sum_{k=1}^{\\lfloor an\\rfloor}\\frac{k}{n^2}$，说明取整及有限个端点项为何不影响极限。\n    11\t\\end{problem}\n    12\t\\begin{problem}{508}{77}{黎曼和与积分夹逼}\n    13\t将 $\\sum_{k=1}^n\\frac1{n+k}$ 写成黎曼和并求其极限。再利用 $f(x)=1/(1+x)$ 的单调性，证明该和与其极限的差的绝对值不超过 $1/(2n)$。\n    14\t\\end{problem}\n    15\t\\begin{problem}{509}{77}{黎曼和与误差控制}\n    16\t利用定积分定义求 $S_n=\\sum_{k=1}^n\\frac{n}{n^2+k^2}$ 的极限。将 $S_n$ 与相应积分比较，确定误差符号，并证明误差的绝对值不超过 $1/(2n)$。\n    17\t\\end{problem}\n    18\t\\begin{problem}{510}{77}{积分比较与严格大小关系}\n    19\t不计算原函数，分别比较以下各组积分：$\\int_0^1x^2\\dd x$ 与 $\\int_0^1x^3\\dd x$；$\\int_0^1x\\dd x$ 与 $\\int_0^1\\tan x\\dd x$；$\\int_1^2\\ln x\\dd x$ 与 $\\int_1^2\\ln^2x\\dd x$；$\\int_0^1e^x\\dd x$ 与 $\\int_0^1(1+x)\\dd x$。给出每组严格不等式的依据，并指出端点相等是否影响结论。\n    20\t\\end{problem}\n    21\t\\begin{problem}{511}{77}{根式积分的比较与区间影响}\n    22\t不求原函数，比较 $I_1=\\int_0^1\\sqrt{1+x^2}\\dd x$ 与 $I_2=\\int_0^1\\sqrt{1+x^3}\\dd x$，证明严格大小关系。若积分区间同时改为 $[1,2]$，关系如何变化？说明理由。\n    23\t\\end{problem}\n    24\t\\begin{problem}{512}{77}{积分估值与严格不等式}\n    25\t不求原函数，先给出 $\\int_{\\pi/4}^{\\pi}(1+\\cos^2x)\\dd x$ 的严格上、下界，所用界仅由被积函数最值与区间长度构成。再计算准确值，说明被积函数在有限个点达到最值为何不能使估值取等号。\n    26\t\\end{problem}\n    27\t\\begin{problem}{513}{77}{带权积分估值}\n    28\t不求原函数，证明 $\\frac1{10\\sqrt2}<\\int_0^1\\frac{x^9}{\\sqrt{1+x}}\\dd x<\\frac1{10}$。把 $x^9$ 改为 $x^n$（$n$ 为非负整数），给出相应严格界，并求 $\\lim_{n\\to\\infty}(n+1)\\int_0^1\\frac{x^n}{\\sqrt{1+x}}\\dd x$。\n    29\t\\end{problem}\n    30\t\\begin{problem}{514}{77}{三角积分估值与单调性}\n    31\t设 $I=\\int_{\\pi/4}^{\\pi/2}\\frac{\\sin x}{x}\\dd x$。证明 $\\frac{\\sqrt2}{4}\\le I\\le\\frac{\\sqrt2}{2}$，并判断两端能否取等号。再利用 $\\sin x/x$ 的单调性给出更紧的一组上下界。\n    32\t\\end{problem}\n    33\t\\begin{problem}{515}{77}{积分中值定理与罗尔定理}\n    34\t设 $a<b$，$f$ 在 $[a,b]$ 上连续、在 $(a,b)$ 可导，且 $\\frac2{b-a}\\int_a^{(a+b)/2}f(x)\\dd x=f(b)$。证明存在 $\\xi\\in(a,b)$ 使 $f'(\\xi)=0$，并说明可先在左半区间选出哪个中值点，再在哪个区间应用罗尔定理。\n    35\t\\end{problem}\n    36\t\\end{problem}\n    37\t\\begin{problem}{516}{77}{积分平均值的单调性}\n    38\t设 $f$ 在 $[a,b]$ 上连续、在 $(a,b)$ 内可导，且 $f'\\le0$。证明\n    39\t\\[\n    40\tF(x)=\\frac1{x-a}\\int_a^xf(t)\\dd t\n    41\t\\]\n    42\t在 $(a,b)$ 内满足 $F'(x)\\le0$。对固定的 $x_0\\in(a,b)$，证明 $F'(x_0)=0$ 当且仅当 $f$ 在 $[a,x_0]$ 上为常数。\n    43\t\\end{problem}\n    44\t\\begin{problem}{517}{77}{函数平均值与中值点}\n    45\t求 $f(x)=\\sqrt{4-x^2}$ 在 $[-2,2]$ 上的平均值，并求使函数值等于平均值的全部点。将半径 $2$ 改为 $r>0$ 后，求相应中值点与 $r$ 的比例关系。\n"}
{"chunk_id":"eab149","wall_time_seconds":0.000007792,"exit_code":0,"original_token_count":521,"output":"569 中等题 计算 $ \\int_{1}^{2} \\frac{1}{x^{3}} e^{\\frac{1}{x}} d x $ .\n570 中等题 计算 $ \\int_{0}^{\\pi^{2}} \\sqrt{x} \\cos \\sqrt{x} d x $ .\n571 基础题 设 $ f(0)=1 $ $ f(2)=3 $ $ f^{\\prime}(2)=5 $ ，求 $ \\int_{0}^{2} x f^{\\prime \\prime}(x) d x $ .\n572 中等题 设 $ F(x)=\\int_{x}^{x+2 \\pi} e^{\\sin t} \\sin t d t $ ，则 $ F(x) $ 为（ ）。\n(A) 正常数 (B) 负常数 (C) 恒为零 (D) 非常数\n573 中等题 已知 $ f(x) $ 的一个原函数为 $ e^{x^{2}} $ ，求 $ \\int_{1}^{e} \\frac{\\ln x f^{\\prime}(\\ln x)}{x} d x $ .\n574 综合题 设 $ f(x) $ 连续，且 $ f(x)=x+2 \\int_{0}^{\\frac{\\pi}{2}} f(x) \\cos x d x $ ，求 $ \\int_{0}^{1} f(x) d x $ .\n575 综合题 设 $ f(x)=\\int_{0}^{x} \\frac{\\sin t}{\\pi-t} d t $ ，计算 $ \\int_{0}^{\\pi} f(x) d x $ .\n576 综合题 设 $ f(x)=\\int_{1}^{x} e^{-y^{2}} d y $ ，求 $ \\int_{0}^{1} x^{2} f(x) d x $ .575 综合题 设 $f(x)=\\int_{0}^{x}\\frac{\\sin t}{\\pi-t}\\mathrm{d}t$ ，计算 $\\int_{0}^{\\pi}f(x)\\mathrm{d}x$ .\n\n576 综合题 设 $f(x)=\\int_{1}^{x}\\mathrm{e}^{-y^{2}}\\mathrm{d}y$ ，求 $\\int_{0}^{1}x^{2}f(x)\\mathrm{d}x$ .\n\n577 综合题 设 $f(x)$ 一阶连续可导，且 $f(x)=x-\\int_{0}^{x}f^{\\prime}(t)\\cos t\\mathrm{d}t$ ，求 $\\int_{0}^{\\frac{\\pi}{2}}f(x)\\mathrm{d}x$ .\n\n第四节 反常积分\n\n一、无穷限的反常积分\n\n定义1：设 $f(x)$ 在 $[a,+\\infty)$ 上有定义，且在任意有界区间 $[a,b]$ 上存在定积\n分 $\\int_{a}^{b}f(x)\\mathrm{d}x$ ，定义\n\n$$\\int_{a}^{+\\infty}f(x)\\mathrm{d}x=\\lim_{b\\rightarrow+\\infty}\\int_{a}^{b}f(x)\\mathrm{d}x$$\n\n定义2：设 $f(x)$ 在 $(-\\infty,b]$ 上有定义，且在任意有界区间 $[a,b]$ 上存在定积\n分 $\\int_{a}^{b}f(x)\\mathrm{d}x$ ，定义\n\n$$\\int_{-\\infty}^{b}f(x)\\mathrm{d}x=\\lim_{a\\rightarrow-\\infty}\\int_{a}^{b}f(x)\\mathrm{d}x$$\n\n定义3：设 $f(x)$ 在 $(-\\infty,+\\infty)$ 上有定义，定义\n\n$$\\int_{-\\infty}^{+\\infty}f(x)\\mathrm{d}x=\\int_{-\\infty}^{0}f(x)\\mathrm{d}x+\\int_{0}^{+\\infty}f(x)\\mathrm{d}x=\\lim_{a\\rightarrow-\\infty}\\int_{a}^{0}f(x)\\mathrm{d}x+\\lim_{b\\rightarrow+\\infty}\\int_{0}^{b}f(x)\\mathrm{d}x.$$"}
{"chunk_id":"063b78","wall_time_seconds":0.239851416,"exit_code":0,"original_token_count":12413,"output":"Warning: truncated output (original token count: 12413)\nTotal output lines: 326\n\n.agent/math-analysis/upper/finish.py:8:from pylatexenc.latexwalker import LatexEnvironmentNode, LatexMacroNode, LatexWalker, get_default_latex_context_db\n.agent/math-analysis/upper/finish.py:9:from pylatexenc.macrospec import EnvironmentSpec\n.agent/math-analysis/upper/finish.py:22:    nodes, position, length = LatexWalker(source, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()\n.agent/math-analysis/upper/check_draft.py:6:from pylatexenc.latexwalker import LatexEnvironmentNode, LatexMacroNode, LatexWalker, get_default_latex_context_db\n.agent/math-analysis/upper/check_draft.py:7:from pylatexenc.macrospec import EnvironmentSpec\n.agent/math-analysis/upper/check_draft.py:26:    nodes, position, length = LatexWalker(source, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()\n.agent/math-analysis/songhao/check_10_11.py:4:from pylatexenc.latexwalker import LatexWalker\n.agent/math-analysis/songhao/check_10_11.py:109:    LatexWalker(text, tolerant_parsing=False).get_latex_nodes()\n.agent/math-analysis/songhao/check_collection.py:7:from pylatexenc.latexwalker import LatexEnvironmentNode, LatexMacroNode, LatexWalker, get_default_latex_context_db\n.agent/math-analysis/songhao/check_collection.py:8:from pylatexenc.macrospec import EnvironmentSpec\n.agent/math-analysis/songhao/check_collection.py:24:    nodes, position, length = LatexWalker(text, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()\n.agent/math-analysis/songhao/check_12_13.py:4:from pylatexenc.latexwalker import LatexWalker, get_default_latex_context_db\n.agent/math-analysis/songhao/check_12_13.py:5:from pylatexenc.macrospec import EnvironmentSpec, MacroStandardArgsParser\n.agent/math-analysis/songhao/check_12_13.py:50:    nodes, position, length = LatexWalker(source, latex_context=context, tolerant_parsing=False).get_latex_nodes()\n.agent/math-analysis/songhao/check_final.py:7:from pylatexenc.latexwalker import LatexEnvironmentNode, LatexMacroNode, LatexWalker, get_default_latex_context_db\n.agent/math-analysis/songhao/check_final.py:8:from pylatexenc.macrospec import EnvironmentSpec\n.agent/math-analysis/songhao/check_final.py:21:    nodes, position, length = LatexWalker(source, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()\n.agent/math-analysis/songhao/renumber_plan.py:6:from pylatexenc.latexwalker import LatexEnvironmentNode, LatexWalker, get_default_latex_context_db\n.agent/math-analysis/songhao/renumber_plan.py:7:from pylatexenc.macrospec import EnvironmentSpec\n.agent/math-analysis/songhao/renumber_plan.py:23:    nodes, position, length = LatexWalker(source, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__main__.py:74:                        version='pylatexenc {}'.format(version_str),\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/_uni2latexmap.py:305:# chars in linguistics, thanks @roedoejet (https://github.com/roedoejet/pylatexenc)\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__init__.py:33:  >>> from pylatexenc.latexencode import unicode_to_latex\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__init__.py:44:  >>> from pylatexenc.latexencode import UnicodeToLatexEncoder\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__init__.py:57:  >>> from pylatexenc.latexencode import UnicodeToLatexEncoder, \\\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__init__.py:79:   and classes were introduced in `pylatexenc 2.0`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__init__.py:82:   `pylatexenc 1.x` is still provided unchanged, so code written for `pylatexenc\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__init__.py:187:# Don't change pylatexenc 1.x function:\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latexencode/__init__.py:195:    #     _util.pyla…10413 tokens truncated…er.LatexCharsNode`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1114:        # have been inserted by LatexWalker() in some occasions to keep\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1129:        :py:class:`~pylatexenc.latexwalker.LatexCommentNode`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1158:        :py:class:`~pylatexenc.latexwalker.LatexGroupNode`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1169:        :py:class:`~pylatexenc.latexwalker.LatexMacroNode`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1196:        :py:class:`~pylatexenc.latexwalker.LatexEnvironmentNode`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1217:        :py:class:`~pylatexenc.latexwalker.LatexSpecialsNode`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1243:        :py:class:`~pylatexenc.latexwalker.LatexMathNode` or a\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1244:        :py:class:`~pylatexenc.latexwalker.LatexEnvironmentNode`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1429:        Convenience function for code that used `text_replacements=` in `pylatexenc\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1432:        If you used custom `text_replacements=` in `pylatexenc 1.x` then you\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1435:          # pylatexenc 1.x with text_replacements\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1442:          # pylatexenc 2 text_replacements compatibility code\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1451:        unwanted results.)  See :py:class:`pylatexenc.macrospec.SpecialsSpec`\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1456:           The `apply_text_replacements()` method was introduced in `pylatexenc\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1458:           existing code run as it did in `pylatexenc 1.x`.  Its use is however\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1508:    _util.pylatexenc_deprecated_ver(\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1510:        \"The module-level function `pylatexenc.latex2text.latex2text()` is deprecated \"\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1511:        \"in favor of the `pylatexenc.latex2text.LatexNodes2Text` class.\"\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1527:    :py:func:`pylatexenc.latexwalker.get_latex_nodes()`.\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1533:    _util.pylatexenc_deprecated_ver(\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1535:        \"The module-level function `pylatexenc.latex2text.latexnodes2text()` is \"\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/latex2text/__init__.py:1536:        \"deprecated in favor of the `pylatexenc.latex2text.LatexNodes2Text` class.\"\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/version.py:34:#       - tests pass: https://travis-ci.org/github/phfaist/pylatexenc\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/version.py:36:#       - LGTM looks good: https://lgtm.com/projects/g/phfaist/pylatexenc/\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/version.py:39:#         dist/pylatexenc-xxx.tar.gz)\n.agent/hdu-ocr/venv/lib/python3.12/site-packages/pylatexenc/version.py:55:#   8) upload package to PyPI (twine upload dist/pylatexenc-X.X.tar.gz -r realpypi)\n"}

## tool · 2026-10-20T02:34:30Z


Script failed
Wall time 0.1 seconds
Output:

{"chunk_id":"37afc9","wall_time_seconds":0.000009834,"exit_code":0,"original_token_count":1054,"output":"import hashlib\nimport json\nimport re\nfrom pathlib import Path\n\nfrom pylatexenc.latexwalker import LatexEnvironmentNode, LatexMacroNode, LatexWalker, get_default_latex_context_db\nfrom pylatexenc.macrospec import EnvironmentSpec\n\nROOT = Path(__file__).resolve().parents[3]\nPROJECT = ROOT / 'output/工科数学分析逐题训练-上册'\nOCR = ROOT / '.agent/hdu-ocr/local/高等数学（上册）精选750题 (宋浩)'\nRANGES = [(1, 130), (131, 258), (259, 379), (380, 504), (505, 600), (601, 656), (657, 750)]\nSECTIONS = [10, 5, 7, 4, 4, 2, 8]\nCONTEXT = get_default_latex_context_db()\nCONTEXT.add_context_category('upper', environments=[EnvironmentSpec('problem', '{{{'), EnvironmentSpec('supplement', '{{')], prepend=True)\nproblems = []\nsupplements = []\nerrors = []\nfor chapter, ((first, last), expected_sections) in enumerate(zip(RANGES, SECTIONS), 1):\n    path = PROJECT / f'chapters/ch{chapter:02d}.tex'\n    if not path.is_file():\n        errors.append({'chapter': chapter, 'missing_file': str(path)})\n        continue\n    source = path.read_text()\n    assert not re.search(r'宋浩|TODO|TBD|待补|待核|候选式|占位|同原题|参照原题', source), str(path)\n    nodes, position, length = LatexWalker(source, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()\n    assert position == 0 and length == len(source)\n    chapter_ids = []\n    chapter_supplements = []\n    section = 0\n    for node in nodes:\n        if isinstance(node, LatexMacroNode) and node.macroname == 'subsection':\n            section += 1\n        if not isinstance(node, LatexEnvironmentNode) or node.environmentname not in ('problem', 'supplement'):\n            continue\n        arguments = [argument.latex_verbatim()[1:-1] for argument in node.nodeargd.argnlist]\n        assert arguments[-1].strip()\n        body = ''.join(child.latex_verbatim() for child in node.nodelist)\n        assert len(body.strip()) >= 20, arguments\n        row = {'chapter': chapter, 'section': section, 'direction': arguments[-1], 'file': path.relative_to(PROJECT).as_posix(),\n               'line': source.count('\\n', 0, node.pos) + 1, 'body_sha256': hashlib.sha256(body.encode()).hexdigest()}\n        if node.environmentname == 'problem':\n            number, page = map(int, arguments[:2])\n            assert first <= number <= last and 10 <= page <= 109, arguments\n            row.update(number=number, source_pdf_page=page)\n            chapter_ids.append(number)\n            problems.append(row)\n        else:\n            assert arguments[0] in (f'{chapter}.{section}-1', f'{chapter}.{section}-2'), arguments\n            row['number'] = arguments[0]\n            chapter_supplements.append(arguments[0])\n            supplements.append(row)\n    expected = list(range(first, last + 1))\n    if chapter_ids != expected:\n        errors.append({'chapter': chapter, 'missing': sorted(set(expected) - set(chapter_ids)), 'unordered_or_duplicate': len(chapter_ids) != len(set(chapter_ids)) or chapter_ids != sorted(chapter_ids)})\n    assert section == expected_sections, (chapter, section, expected_sections)\n    assert chapter_supplements == [f'{chapter}.{part}-{item}' for part in range(1, expected_sections + 1) for item in (1, 2)]\nfor number in range(10, 110):\n    assert (OCR / f'{number:03d}.md').is_file(), number\nassert hashlib.sha256((ROOT / '高等数学（上册）精选750题 (宋浩).pdf').read_bytes()).hexdigest() == '789f962dda7463ca0596f381c12be57013ea9f0b40100d96a7366425dcb8ea28'\nassert not (ROOT / '.agent/math-analysis/songhao/tex-runtime').exists()\nassert not (ROOT / '.agent/math-analysis/songhao/tex-cache').exists()\nprint(json.dumps({'problems': len(problems), 'supplements': len(supplements), 'errors': errors}, ensure_ascii=False))\nassert not errors, errors\nassert len(problems) == 750 and len(supplements) == 80\nrecord = {'source_sha256': '789f962dda7463ca0596f381c12be57013ea9f0b40100d96a7366425dcb8ea28', 'problems': problems, 'supplements': supplements}\n(Path(__file__).resolve().parent / '原题对应审计.json').write_text(json.dumps(record, ensure_ascii=False, indent=2) + '\\n')\nprint('PASS: all 750 original problems and 80 progressive questions; strict syntax, section placement, original hash and TeX cleanup')\n"}
Script error:
apply_patch verification failed: Failed to find expected lines in /Users/oyamahappa/Documents/Agent/Codex/output/工科数学分析逐题训练-上册/chapters/ch05.tex:
再利用 $\sin x/x$ 的单调性给出更紧的一组上下界。

## tool · 2026-10-20T02:34:40Z


Script completed
Wall time 0.3 seconds
Output:

{}
{"chunk_id":"a239a8","wall_time_seconds":0.000006834,"exit_code":0,"original_token_count":70,"output":"import json\nimport math\nimport re\nfrom pathlib import Path\n\nROOT = Path(__file__).resolve().parents[3]\nCHAPTERS = ROOT / \"output/工科数学分析逐题训练-上册/chapters\"\nEXPECTED = {\n    5: [(505, 517), (518, 538), (539, 577), (578, 600)],\n    6: [(601, 649), (650, 656)],\n"}
{}
{"chunk_id":"e6d911","wall_time_seconds":0.000010042,"exit_code":1,"original_token_count":298,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 105, in <module>\n    totals = check_structure()\n             ^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 69, in check_structure\n    assert not errors, json.dumps(errors, ensure_ascii=False)\n           ^^^^^^^^^^\nAssertionError: [{\"chapter\": 5, \"section\": 3, \"missing\": [548, 550, 553, 554, 557, 559, 560, 562, 568, 569, 570, 571, 572, 573, 574, 575, 576, 577], \"extra\": [], \"in_order\": true}, {\"chapter\": 5, \"section\": 4, \"missing\": [582, 589, 592, 594, 596, 598, 600], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 1, \"missing\": [657, 658, 659], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 2, \"missing\": [664, 668, 677], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 4, \"missing\": [689], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 5, \"missing\": [703, 704, 705, 706, 707, 708, 709, 710, 711, 712, 713, 714], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 7, \"missing\": [728, 735, 736, 737, 738], \"extra\": [], \"in_order\": true}]\n"}

## tool · 2026-10-20T02:37:35Z




## tool · 2026-10-20T02:37:39Z


Script completed
Wall time 0.3 seconds
Output:

{"page":"081","result":{"chunk_id":"215a67","wall_time_seconds":0.00001225,"exit_code":0,"original_token_count":507,"output":"545 基础题 计算 $ \\int_{1}^{2} \\frac{\\sqrt{x^{2}-1}}{x} \\mathrm{d} x. $\n546 基础题 计算 $ \\int_{-1}^{1} \\frac{\\mathrm{d} x}{1+\\sqrt{1-x^{2}}}. $\n547 基础题 计算 $ \\int_{0}^{1} \\sqrt{2 x-x^{2}} \\mathrm{d} x. $\n548 中等题 计算 $ \\int_{0}^{- \\ln 2} \\sqrt{1-e^{2 x}} \\mathrm{d} x. $\n549 中等题 设 $ f(x)=\\left\\{ \\begin{array}{ll} 1+x^{2}, & x<0 \\\\ \\mathrm{e}^{-x}, & x\\geqslant 0 \\end{array} \\right. $ ，求 $ \\int_{1}^{3} f(x-2) \\mathrm{d} x. $\n550 中等题 设 $ f(x)=\\left\\{ \\begin{array}{ll} x \\mathrm{e}^{x^{2}}, & -\\frac{1}{2} \\leqslant x \\leqslant \\frac{1}{2} \\\\ -1, & x \\geqslant \\frac{1}{2} \\end{array} \\right. $ ，求 $ \\int_{\\frac{1}{2}}^{2} f(x-1) \\mathrm{d} x. $\n551 中等题 设连续函数 $ f(x) $满足 $ \\int_{0}^{x} f(x-t) \\mathrm{d} t=\\mathrm{e}^{-2 x}-1 $ ，求定积分 $ \\int_{0}^{1} f(x) \\mathrm{d} x. $551 中等题 设连续函数 $ f ( x ) $满足 $ \\int_{0}^{x} f ( x - t ) \\mathrm{d} t=\\mathrm{e}^{-2 x}-1 $，求定积分 $ \\int_{0}^{1} f ( x ) \\mathrm{d} x $.\n\n552 综合题 设 $ f ( x ) $是 $ (-\\infty , +\\infty ) $内的连续函数，且满足 $ \\int_{0}^{x} f ( x - t ) \\mathrm{d} t=\\mathrm{e}^{x}-x-1 $求 $ f ( x ) $.\n\n553 基础题 计算 $ \\int_{-\\frac{\\pi}{2}}^{\\frac{\\pi}{2}} \\frac{x}{1+\\cos x} \\mathrm{d} x $.\n\n554 基础题 计算 $ \\int_{-\\frac{\\pi}{2}}^{\\frac{\\pi}{2}} \\sin^{2} x \\ln \\left( x+\\sqrt{1+x^{2}} \\right) \\mathrm{d} x $.\n\n555 中等题 计算 $ \\int_{-1}^{1} \\frac{1}{\\sqrt{4-x^{2}}} \\left( \\frac{1}{1+e^{x}}-\\frac{1}{2} \\right) \\mathrm{d} x $.\n\n556 中等题 求 $ \\int_{-1}^{1} \\cos x \\arccos x \\mathrm{d} x $.\n\n557 综合题 设 $ M=\\int_{-\\frac{\\pi}{4}}^{\\frac{\\pi}{4}} \\left( \\frac{\\tan x}{1+x^{4}}+x^{8} \\right) \\mathrm{d} x $， $ N=\\int_{-\\frac{\\pi}{4}}^{\\frac{\\pi}{4}} \\left( \\sin^{8} x+\\ln \\left( x+\\sqrt{x^{2}+1} \\right) \\right) \\mathrm{d} x $， $ P=\\int_{-\\frac{\\pi}{4}}^{\\frac{\\pi}{4}} \\left( \\tan^{8} x+e^{x} \\cos x-e^{-x} \\cos x \\right) \\mathrm{d} x $，则有（    ）.\n\n(A) $ P>N>M $ (B) $ N>P>M $ (C) $ N>M>P $ (D) $ P>M>N $"}}
{"page":"082","result":{"chunk_id":"72b321","wall_time_seconds":0.00000975,"exit_code":0,"original_token_count":372,"output":"558 中等题 计算 $\\int_{0}^{n\\pi}\\sqrt{1-\\sin^{2}x}\\mathrm{d}x$.\n\n559 中等题 计算 $\\int_{a}^{a+\\pi}\\sin^{2}x(\\tan x+1)\\mathrm{d}x$.\n\n560 综合题 设 $f(x)$ 为连续函数，证明 (1) $\\int_{0}^{\\frac{\\pi}{2}}f(\\sin x)\\mathrm{d}x=\\int_{0}^{\\frac{\\pi}{2}}f(\\cos x)\\mathrm{d}x$；\n(2) $\\int_{0}^{\\pi}xf(\\sin x)\\mathrm{d}x=\\pi \\int_{0}^{\\frac{\\pi}{2}}f(\\sin x)\\mathrm{d}x$，并由此计算定积分\n$I_{n}=\\int_{0}^{\\pi}\\frac{x\\sin^{2n}x}{\\sin^{2n}x+\\cos^{2n}x}\\mathrm{d}x$ ($n$ 为正整数).\n\n二、定积分的分部积分法\n\n定理 2: 设 $u=u(x),v=v(x)$ 在区间 $[a,b]$ 上连续可导，则\n$\\int_{a}^{b}uv^{\\prime}\\mathrm{d}x=uv|_{a}^{b}-\\int_{a}^{b}u^{\\prime}\\mathrm{d}x$ 或 $\\int_{a}^{b}u\\mathrm{d}v=uv|_{a}^{b}-\\int_{a}^{b}v\\mathrm{d}u$.\n\n561 基础题 计算 $\\int_{0}^{1}\\ln(1+x^{2})\\mathrm{d}x$.\n\n562 基础题 计算 $\\int_{0}^{\\frac{1}{2}}\\arcsin x\\mathrm{d}x$.561 基础题 计算 $ \\int_{0}^{1} \\ln(1+x^{2})\\mathrm{d}x. $\n562 基础题 计算 $ \\int_{0}^{\\frac{1}{2}} \\arcsin x\\mathrm{d}x. $\n563 基础题 计算 $ \\int_{-1}^{1} x\\arccos x\\mathrm{d}x. $\n564 中等题 计算 $ \\int_{0}^{1} \\frac{\\ln(1+x)}{(2-x)^{2}}\\mathrm{d}x. $\n565 中等题 计算 $ \\int_{0}^{\\frac{\\pi}{2}} \\mathrm{e}^{-x}\\sin(2x)\\mathrm{d}x. $\n566 中等题 计算 $ \\int_{0}^{1} \\mathrm{e}^{-\\sqrt{x}}\\mathrm{d}x. $\n567 中等题 计算 $ \\int_{0}^{1} \\frac{x^{2}\\arcsin x}{\\sqrt{1-x^{2}}}\\mathrm{d}x. $\n568 中等题 计算 $ \\int_{1}^{16} \\arctan \\sqrt{\\sqrt{x}-1}\\mathrm{d}x. $"}}
{"page":"084","result":{"chunk_id":"9d1c0b","wall_time_seconds":0.00001025,"exit_code":0,"original_token_count":689,"output":"定义1和定义2中若右端极限存在，则称该反常积分收敛，否则称为发散；\n定义3中要求右端的两个反常积分都收敛，则 $\\int_{-\\infty}^{+\\infty} f(x) \\mathrm{d}x$ 收敛. 有一个发散，则\n$\\int_{-\\infty}^{+\\infty} f(x) \\mathrm{d}x$ 发散.\n\n二、无穷限积分的性质\n\n性质1：$\\int_{a}^{+\\infty} f(x) \\mathrm{d}x$ 与 $\\int_{b}^{+\\infty} f(x) \\mathrm{d}x$ 具有相同的敛散性.\n\n性质2：$\\int_{a}^{+\\infty} k f(x) \\mathrm{d}x (k \\neq 0$ 为常数)与 $\\int_{a}^{+\\infty} f(x) \\mathrm{d}x$ 具有相同的敛散性.\n\n性质3：若 $\\int_{a}^{+\\infty} f(x) \\mathrm{d}x$ 与 $\\int_{a}^{+\\infty} g(x) \\mathrm{d}x$ 均收敛，则 $\\int_{a}^{+\\infty} [f(x) \\pm g(x)] \\mathrm{d}x$ 收敛，且\n$\\int_{a}^{+\\infty} [f(x) \\pm g(x)] \\mathrm{d}x = \\int_{a}^{+\\infty} f(x) \\mathrm{d}x \\pm \\int_{a}^{+\\infty} g(x) \\mathrm{d}x$.\n\n常用结论：$\\int_{a}^{+\\infty} \\frac{\\mathrm{d}x}{x^{p}} \\left\\{ \\begin{array}{l l} p > 1, & \\text{收敛} \\\\ p \\leqslant 1, & \\text{发散} \\end{array} (a > 0); \\int_{a}^{+\\infty} \\frac{\\mathrm{d}x}{x \\ln^{p} x} \\left\\{ \\begin{array}{l l} p > 1, & \\text{收敛} \\\\ p \\leqslant 1, & \\text{发散} \\end{array} (a > 1). \\right.$\n\n在实际计算中，反常积分可按照定积分 $\\int_{a}^{b} f(x) \\mathrm{d}x = F(x) \\bigg|_{a}^{b}$ 的计算方法进行，只不过要将 $F(b)$ 或 $F(a)$ 改作 $\\lim_{x \\to \\infty} f(x)$ 或 $\\lim_{x \\to \\infty} f(x)$ 即可. 定积分的换元法和分部积分法在反常积分的计算中也适用.\n\n三、无穷限积分敛散性的判别\n\n比较判别法：设 $0 \\leqslant f(x) \\leqslant g(x)$，则有：\n(1) 当 $\\int_{a}^{+\\infty} g(x) \\mathrm{d}x$ 收敛时 $\\int_{a}^{+\\infty} f(x) \\mathrm{d}x$ 收敛；三、无穷限积分敛散性的判别\n\n比较判别法：设 $0 \\leqslant f(x) \\leqslant g(x)$，则有：\n(1) 当 $\\int_{a}^{+\\infty} g(x) \\mathrm{d}x$ 收敛时，$\\int_{a}^{+\\infty} f(x) \\mathrm{d}x$ 收敛；\n(2) 当 $\\int_{a}^{+\\infty} f(x) \\mathrm{d}x$ 发散时，$\\int_{a}^{+\\infty} g(x) \\mathrm{d}x$ 发散.\n\n578 基础题 下列反常积分中收敛的是（    ）.\n(A) $\\int_{2}^{+\\infty} \\frac{1}{\\sqrt{x}} \\mathrm{d}x$\n(B) $\\int_{2}^{+\\infty} \\frac{\\ln x}{x} \\mathrm{d}x$\n(C) $\\int_{2}^{+\\infty} \\frac{1}{x \\ln x} \\mathrm{d}x$\n(D) $\\int_{2}^{+\\infty} \\frac{x}{e^{x}} \\mathrm{d}x$\n\n579 基础题 计算 $\\int_{2}^{+\\infty} \\frac{1}{x \\ln^{2} x} \\mathrm{d}x$.\n\n580 基础题 计算 $\\int_{-\\infty}^{+\\infty} \\frac{1}{x^{2}+4x+5} \\mathrm{d}x$.\n\n581 基础题 计算 $\\int_{1}^{+\\infty} \\frac{\\mathrm{d}x}{x^{2}+x}$.\n\n582 中等题 计算 $\\int_{3}^{+\\infty} \\frac{1}{(x-1)^{4} \\sqrt{x^{2}-2x}} \\mathrm{d}x$.\n\n583 基础题 计算 $\\int_{-\\infty}^{+\\infty} \\frac{\\mathrm{e}^{x}}{1+\\mathrm{e}^{2x}} \\mathrm{d}x$."}}
{"page":"085","result":{"chunk_id":"b1b348","wall_time_seconds":0.000012459,"exit_code":0,"original_token_count":488,"output":"584 中等题 计算 $ \\int_{0}^{+\\infty} \\min \\left\\{e^{-x}, \\frac{1}{2} \\right\\} dx. $\n585 中等题 计算 $ \\int_{1}^{+\\infty} \\frac{\\ln x}{(1+x)^{2}} dx. $\n586 中等题 计算 $ \\int_{0}^{+\\infty} \\frac{1}{(1+x^{2})^{2}} dx. $\n587 中等题 计算 $ \\int_{1}^{+\\infty} \\frac{d x}{x \\sqrt{2 x^{2}-1}}. $\n588 综合题 计算 $ \\int_{0}^{+\\infty} \\frac{x e^{-x}}{(1+e^{-x})^{2}} dx. $\n589 中等题 关于 $ \\int_{-\\infty}^{+\\infty} \\sin(2 x) \\cdot e^{|x|} d x $ ，下列结论正确的是（    ）.\n(A) 取值为0 (B) 取正值 (C) 发散 (D) 取负值\n590 基础题 判别 $ \\int_{2}^{+\\infty} \\frac{1}{\\ln x} d x $ 的敛散性.\n591 中等题 判别 $ \\int_{0}^{+\\infty} e^{-x^{2}} d x $ 的敛散性.590 基础题 判别 $\\int_{2}^{+\\infty}\\frac{1}{\\ln x}\\mathrm{d}x$ 的敛散性.\n\n591 中等题 判别 $\\int_{0}^{+\\infty}\\mathrm{e}^{-x^{2}}\\mathrm{d}x$ 的敛散性.\n\n592 综合题 求 $c$ 的值，使 $\\lim_{x\\to+\\infty}\\left(\\frac{x+c}{x-c}\\right)^{x}=\\int_{-\\infty}^{c}t\\mathrm{e}^{2i}\\mathrm{d}t$.\n\n四、无界函数的反常积分\n\n如果函数 $f(x)$ 在点 $x=x_{0}$ 的任一邻域内都无界，则称点 $x=x_{0}$ 为函数 $f(x)$ 的瑕点，无界函数的反常积分又称为瑕积分.\n\n定义1：设 $f(x)$ 在 $(a,b]$ 上有定义，且在任一区间 $[a+\\varepsilon,b]$ 上可积，其中 $\\varepsilon>0$ 且 $\\lim_{x\\to a^{+}}f(x)=\\infty$，定义\n\n$$\\int_{a}^{b}f(x)\\mathrm{d}x=\\lim_{\\varepsilon\\to0^{+}}\\int_{a+\\varepsilon}^{b}f(x)\\mathrm{d}x$$\n\n定义2：设 $f(x)$ 在 $[a,b)$ 上有定义，且在任一区间 $[a,b-\\varepsilon]$ 上可积，其中 $\\varepsilon>0$，且 $\\lim_{x\\to b^{-}}f(x)=\\infty$，定义\n\n$$\\int_{a}^{b}f(x)\\mathrm{d}x=\\lim_{\\varepsilon\\to0^{+}}\\int_{a}^{b-\\varepsilon}f(x)\\mathrm{d}x$$\n\n定义3：设 $f(x)$ 在 $[a,c)$ 及 $(c,b]$ 上都有定义，且在任一区间 $[a,c-\\varepsilon]$ 及 $[c+\\varepsilon,b]$ 上可积，其中 $\\varepsilon>0$，且 $\\lim_{x\\to c}f(x)=\\infty$，定义"}}
{"page":"086","result":{"chunk_id":"3e756e","wall_time_seconds":0.000010459,"exit_code":0,"original_token_count":621,"output":"$ \\int_{a}^{b} f(x) \\mathrm{d} x=\\int_{a}^{c} f(x) \\mathrm{d} x+\\int_{c}^{b} f(x) \\mathrm{d} x=\\lim_{e_{1} \\to 0^{+}} \\int_{a}^{c-e_{1}} f(x) \\mathrm{d} x+\\lim_{e_{2} \\to 0^{+}} \\int_{c+e_{2}}^{b} f(x) \\mathrm{d} x $\n定义1和定义2中若右端极限存在，则称该瑕积分收敛，否则称为发散；定义3中要求右端的两个瑕积分都收敛，则 $ \\int_{a}^{b} f(x) \\mathrm{d} x $收敛。有一个发散，则 $ \\int_{a}^{b} f(x) \\mathrm{d} x $发散.\n瑕积分的性质、计算方法及敛散性的判别均与无穷限积分相类似.\n\n593 基础题 下列积分（    ）是反常积分.\n(A) $ \\int_{0}^{1} \\frac{\\sin x}{x} \\mathrm{d} x $\n(B) $ \\int_{0}^{1} x \\ln x \\mathrm{d} x $\n(C) $ \\int_{-1}^{1} \\frac{\\mathrm{d} x}{\\sqrt{2} x^{2}} $\n(D) $ \\int_{0}^{1} \\frac{1}{x^{-2}} \\mathrm{d} x $\n594 基础题 $ I=\\int_{0}^{1} x \\ln^{2} x \\mathrm{d} x $是（    ）.\n(A) 定积分且值为 $ \\frac{1}{3} $\n(B) 定积分且值为 $ \\frac{1}{4} $\n(C) 反常积分且发散\n(D) 反常积分且值为 $ \\frac{1}{2} $\n595 基础题 计算 $ \\int_{0}^{a} \\frac{\\mathrm{d} x}{\\sqrt{a^{2}-x^{2}}} $\n596 基础题 计算 $ \\int_{0}^{1} \\frac{\\mathrm{d} x}{x(\\ln x)^{2}} $\n597 中等题 讨论瑕积分 $ \\int_{a}^{b} \\frac{\\mathrm{d} x}{(x-a)^{p}} $的敛散性.596 基础题 计算 $ \\int_{0}^{+\\infty} \\frac{1}{x(\\ln x)^{2}} \\, \\mathrm{d}x $\n597 中等题 讨论瑕积分 $ \\int_{a}^{b} \\frac{\\mathrm{d}x}{(x-a)^{p}} $的敛散性.\n598 中等题 计算 $ \\int_{0}^{+\\infty} \\frac{\\ln x}{x^{2}+1} \\, \\mathrm{d}x $\n599 综合题 设函数 $ f(x)=\\left\\{ \\begin{array}{l l} \\frac{1}{(x-1)^{\\alpha-1}}, & 1<x<e \\\\ \\frac{1}{x\\ln^{\\alpha+1} x}, & x\\geqslant e \\end{array} \\right. $ ，若反常积分 $ \\int_{1}^{+\\infty} f(x) \\mathrm{d}x $收敛，则（    ）。\n(A) $ \\alpha<-2 $\n(B) $ \\alpha>2 $\n(C) $ -2<\\alpha<0 $\n(D) $ 0<\\alpha<2 $\n600 综合题 下列计算正确的是（    ）。\n(A) $ \\int_{-\\infty}^{+\\infty} \\frac{x}{1-x^{2}} \\mathrm{d}x=0 $\n(B) $ \\int_{-\\infty}^{+\\infty} \\sin x \\mathrm{d}x=\\lim_{b\\rightarrow+\\infty} \\int_{-b}^{b} \\sin x \\mathrm{d}x=\\lim_{b\\rightarrow+\\infty} \\left|-\\cos x\\right|_{-b}=\\lim_{b\\rightarrow+\\infty}[\\cos(-b)-\\cos b]=0 $\n(C) $ \\int_{-1}^{1} \\frac{1}{x^{2}} \\mathrm{d}x=-\\frac{1}{x}\\bigg|_{-1}^{1}=-2 $\n(D) $ \\int_{0}^{+\\infty} x^{\\frac{3}{2}} \\mathrm{e}^{-x} \\mathrm{d}x=\\Gamma\\left(\\frac{5}{2}\\right)=\\frac{3}{2} \\Gamma\\left(\\frac{3}{2}\\right)=\\frac{3}{2} \\cdot \\frac{1}{2} \\Gamma\\left(\\frac{1}{2}\\right)=\\frac{3}{4} \\sqrt{\\pi} $"}}

## tool · 2026-10-20T02:39:20Z


Script completed
Wall time 0.4 seconds
Output:

{"chunk_id":"3aa7a9","wall_time_seconds":0.000015375,"exit_code":0,"original_token_count":1106,"output":"160:\\begin{problem}{546}{81}{绝对值与对称积分}\n161-计算 $\\int_{-1}^1\\frac{\\dd x}{1+\\sqrt{x^2}}$。对实数 $a$ 求 $J(a)=\\int_{-a}^a\\frac{\\dd x}{1+|x|}$，正确处理 $a<0$ 时的积分方向，并判断 $J$ 的奇偶性。\n162-\\end{problem}\n163:\\begin{problem}{547}{81}{配方换元与圆面积}\n164-计算 $\\int_0^1\\sqrt{2x-x^2}\\dd x$。利用被积函数关于 $x=1$ 的对称性求 $\\int_0^2x\\sqrt{2x-x^2}\\dd x$，并说明不必另求原函数的理由。\n165-\\end{problem}\n166:\\begin{problem}{549}{81}{平移换元与分段积分}\n167-设 $f(x)=1+x^2$（$x<0$），$f(x)=e^{-x}$（$x\\ge0$）。求 $\\int_1^3f(x-2)\\dd x$；令 $J(c)=\\int_1^3f(x-c)\\dd x$，证明 $J$ 在 $c=2$ 可导并求 $J'(2)$。\n168-\\end{problem}\n--\n172:\\begin{problem}{552}{81}{含参积分与二次求导}\n173-设 $f$ 在实轴上连续，且 $\\int_0^xf(x-t)t\\dd t=e^x-x-1$。通过换元和微积分基本定理求 $f$，并直接核验原等式。说明推导时为何不需要预先假设 $f$ 可导。\n174-\\end{problem}\n--\n178:\\begin{problem}{556}{81}{反三角函数的对称关系}\n179-计算 $\\int_{-1}^1\\cos x\\arccos x\\dd x$。证明对任意连续偶函数 $g$，$\\int_{-1}^1g(x)\\arccos x\\dd x=\\frac\\pi2\\int_{-1}^1g(x)\\dd x$，并说明本题如何应用此式。\n180-\\end{problem}\n181:\\begin{problem}{558}{82}{周期函数与绝对值}\n182-对正整数 $n$，计算 $\\int_0^{n\\pi}\\sqrt{1-\\sin^2x}\\dd x$。再求 $\\int_a^{a+n\\pi}\\sqrt{1-\\sin^2x}\\dd x$，证明结果与实数 $a$ 无关，并指出去掉根号而直接写成 $\\cos x$ 的错误。\n183-\\end{problem}\n184:\\begin{problem}{561}{82}{分部积分与参数恒等式}\n185-计算 $\\int_0^1\\ln(1+x^2)\\dd x$。对 $a>0$ 计算 $\\int_0^a\\ln(1+x^2)\\dd x$，再对所得结果求导核验。\n186-\\end{problem}\n--\n199:\\begin{problem}{567}{82}{三角换元与端点处理}\n200-计算 $\\int_0^1\\frac{x^2\\arcsin x}{\\sqrt{1-x^2}}\\dd x$，在计算中说明 $x=1$ 处无界因子为何不导致发散；再求 $\\int_0^1\\frac{\\arcsin x}{\\sqrt{1-x^2}}\\dd x$ 作为对照。\n201-\\end{problem}\n--\n213:\\begin{problem}{578}{84}{无穷积分分类与判敛}\n214-取 $a>1$，分别判断 $\\int_a^{+\\infty}x^{-1/2}\\dd x$、$\\int_a^{+\\infty}\\frac{\\ln x}{x}\\dd x$、$\\int_a^{+\\infty}\\frac{\\dd x}{x\\ln x}$、$\\int_a^{+\\infty}xe^{-x}\\dd x$ 的敛散性，给出理由；对收敛者求值。\n215-\\end{problem}\n--\n222:\\begin{problem}{581}{84}{拆项积分与无穷端点抵消}\n223-计算 $\\int_1^{+\\infty}\\frac{\\dd x}{x^2+x}$。说明为何部分分式分解后不能将积分写为两个发散积分之差；再求下限改为 $a>0$ 时的值及 $a\\to0^+$ 时的极限。\n224-\\end{problem}\n--\n240:\\begin{problem}{588}{85}{反常分部积分与对数积分}\n241-计算 $\\int_0^{+\\infty}\\frac{xe^{-x}}{(1+e^{-x})^2}\\dd x$。先用比较法证明收敛，再选择使无穷端边界项为零的分部方式；最后计算将 $x$ 同时替换为 $ax$（$a>0$）后的积分。\n242-\\end{problem}\n--\n246:\\begin{problem}{591}{85}{高斯型积分的收敛性}\n247-不用高斯积分的准确值，证明 $\\int_0^{+\\infty}e^{-x^2}\\dd x$ 收敛。对 $a\\in\\mathbb R$ 讨论 $\\int_0^{+\\infty}e^{-ax^2}\\dd x$ 的敛散性，并在 $a>0$ 时给出它与 $a=1$ 时积分的关系。\n248-\\end{problem}\n249:\\begin{problem}{593}{86}{瑕点识别与可去间断点}\n250-分别考察 $\\int_0^1\\frac{\\sin x}{x}\\dd x$、$\\int_0^1x\\ln x\\dd x$、$\\int_{-1}^1\\frac{\\dd x}{\\sqrt{x^2}}$、$\\int_0^1x^{-2}\\dd x$。指出未定义点，区分可作连续延拓的情形与无界瑕点，判断敛散性，并计算收敛积分中 $\\int_0^1x\\ln x\\dd x$ 的值。\n251-\\end{problem}\n252:\\begin{problem}{595}{86}{端点瑕积分与参数条件}\n253-对 $a>0$，计算 $\\int_0^a\\frac{\\dd x}{\\sqrt{a^2-x^2}}$，用极限说明上端点的处理。再讨论 $\\int_0^a(a^2-x^2)^{-p}\\dd x$ 随实参数 $p$ 的敛散性。\n254-\\end{problem}\n255:\\begin{problem}{597}{86}{瑕积分的幂次判别}\n256-设 $a<b$，判断 $\\int_a^b\\frac{\\dd x}{(x-a)^2}$ 的敛散性。推广讨论 $\\int_a^b\\frac{\\dd x}{(x-a)^p}$（$p\\in\\mathbb R$），收敛时求值，并明确临界指数。\n257-\\end{problem}\n258:\\begin{problem}{599}{86}{分段反常积分与双重条件}\n259-设 $f(x)=(x-1)^{1-\\alpha}$（$1<x<e$），$f(x)=1/[x\\ln^{\\alpha+1}x]$（$x\\ge e$）。求使 $\\int_1^{+\\infty}f(x)\\dd x$ 收敛的全部实数 $\\alpha$，并在收敛范围内求积分值。说明两个端点分别给出什么参数条件。\n260-\\end{problem}\n"}
{}
{"chunk_id":"13f38a","wall_time_seconds":0.089587917,"exit_code":1,"original_token_count":230,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 105, in <module>\n    totals = check_structure()\n             ^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 69, in check_structure\n    assert not errors, json.dumps(errors, ensure_ascii=False)\n           ^^^^^^^^^^\nAssertionError: [{\"chapter\": 7, \"section\": 1, \"missing\": [657, 658, 659], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 2, \"missing\": [664, 668, 677], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 4, \"missing\": [689], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 5, \"missing\": [703, 704, 705, 706, 707, 708, 709, 710, 711, 712, 713, 714], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 7, \"missing\": [728, 735, 736, 737, 738], \"extra\": [], \"in_order\": true}]\n"}

## tool · 2026-10-20T02:39:25Z




## tool · 2026-10-20T02:39:29Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"47437d","wall_time_seconds":0.000009375,"exit_code":1,"original_token_count":0,"output":""}
{"chunk_id":"0c2471","wall_time_seconds":0.000008375,"exit_code":1,"original_token_count":60,"output":"cat: .agent/hdu-ocr/local/高等数学（上册）精选750题 (宋浩)/103-crop0.0-0.55.md: No such file or directory\ncat: .agent/hdu-ocr/local/高等数学（上册）精选750题 (宋浩)/103-crop0.45-1.0.md: No such file or directory\n"}

## tool · 2026-10-20T02:39:37Z




## tool · 2026-10-20T02:39:42Z


Script completed
Wall time 0.6 seconds
Output:

{"chunk_id":"434e52","wall_time_seconds":0.34073025,"exit_code":0,"original_token_count":2,"output":"1.14.0\n"}
{"chunk_id":"99d688","wall_time_seconds":0.00000825,"exit_code":0,"original_token_count":2260,"output":"在实轴上分别判断 $\\{x^2,2x^2\\}$、$\\{\\sin x,\\cos x\\}$、$\\{\\sin2x,\\sin x\\cos x\\}$、$\\{e^{2x},3e^{2x}\\}$ 的线性相关性。对无关者给出证明；说明将定义区间缩小为任意非空开区间是否改变结论。\n\\end{problem}\n\\begin{problem}{718}{105}{已知解验证与基本解组}\n对方程 $(x-1)y''-xy'+y=0$，分别判断 $\\{x,2x\\}$、$\\{e^x,8e^x\\}$、$\\{x,x^2\\}$、$\\{x,e^x\\}$ 能否构成 $x>1$ 上的基本解组。求通解，并说明为何需要把“两个解”与“两个线性无关的解”分开检验。\n\\end{problem}\n\\begin{problem}{719}{105}{一阶非齐次方程的解结构}\n设 $p,f$ 在区间 $I$ 上连续，$y_1$ 是 $y'+py=f$ 的一个解，$y_2\\ne0$ 是对应齐次方程的解。证明全部解恰为 $y=y_1+Cy_2$，并用初值 $y(x_0)=a$ 表示 $C$。说明若误把 $C$ 乘在 $y_1$ 前会产生什么条件限制。\n\\end{problem}\n\\begin{problem}{720}{105}{一阶齐次解与冗余常数}\n设连续系数方程 $y'+p(x)y=0$ 在同一区间上有两个不同解 $y_1,y_2$。证明 $y=C(y_1-y_2)$ 为通解。判断 $C_1y_1+C_2y_2$ 中两常数是否独立，并讨论其中一个已知解为零函数的情形。\n\\end{problem}\n\\begin{problem}{721}{106}{朗斯基行列式与通解判据}\n设 $f_1,f_2$ 是 $y''+py'+qy=0$ 的两个非零解，$p,q$ 为常数。记 $W=f_1f_2'-f_2f_1'$。证明若某点 $W\\ne0$，则 $C_1f_1+C_2f_2$ 是通解；推导 $W'=-pW$，并说明为什么“两个不同的非零解”本身还不足够。\n\\end{problem}\n\\begin{problem}{722}{106}{三角基本解组与退化参数}\n验证 $\\cos ax,\\sin ax$ 是 $y''+a^2y=0$（$a\\ne0$）的线性无关解并写出通解。若 $a=0$，说明该函数组为何失效并另写通解；求两种情况下满足 $y(0)=0,y'(0)=1$ 的解。\n\\end{problem}\n\\begin{problem}{723}{106}{非齐次通解的完整性验证}\n验证 $y=C_1e^x+C_2e^{2x}+\\frac1{12}e^{5x}$ 是 $y''-3y'+2y=e^{5x}$ 的通解。除代入验证外，还须证明齐次部分线性无关；再求满足 $y(0)=y'(0)=0$ 的特解。\n\\end{problem}\n\\begin{problem}{724}{106}{三个非齐次解构造通解}\n设 $p,q,f$ 在区间 $I$ 上连续，$y_1,y_2,y_3$ 是 $y''+py'+qy=f$ 的三个线性无关的解。证明\n\\[\ny=2C_1y_1+(C_2-C_1)y_2+(1-C_1-C_2)y_3\n\\]\n为通解，并说明两个齐次方向的独立性。再证明此假设蕴含 $f\\not\\equiv0$。\n\\end{problem}\n\\begin{supplement}{7.6-1}{解的叠加与初始条件}\n设 $y_1,y_2$ 是方程 $y''+p(x)y'+q(x)y=f(x)$ 的两个解。证明 $\\alpha y_1+(1-\\alpha)y_2$ 仍为解，并说明一般线性组合成为解所需的条件。取 $f\\not\\equiv0$ 时，判断 $y_1+y_2$ 与 $y_1-y_2$ 分别满足什么方程。\n\\end{supplement}\n\\begin{supplement}{7.6-2}{已知解降阶与基本解组}\n已知 $y_1=x$ 是 $x^2y''-2xy'+2y=0$ 在 $x>0$ 上的解。令 $y=xv(x)$ 求通解，证明所得两解线性无关，并求满足 $y(1)=0$、$y'(1)=1$ 的解。\n\\end{supplement}\n\\subsection{常系数齐次线性微分方程}\n\\begin{problem}{725}{106}{候选特解验证与有界解}\n分别判断 $e^x$、$e^{2x}$、$1+e^{-2x}$、$xe^{-2x}$ 是否为 $y''+2y'=0$ 的解，给出代入依据。求此方程通解，并确定全实轴上的全部有界解。\n\\end{problem}\n\\begin{problem}{726}{107}{由解族恢复方程}\n求以 $y=C_1e^{6x}+C_2e^{-8x}$ 为通解的首项系数为 $1$ 的二阶常系数齐次方程，证明系数唯一。确定通解中在 $x\\to+\\infty$ 时趋于零的全部解。\n\\end{problem}\n\\begin{problem}{727}{107}{共轭特征根与方程恢复}\n求以 $e^{2x}\\sin3x,e^{2x}\\cos3x$ 为基本解组的首项系数为 $1$ 的二阶常系数齐次方程。求满足 $y(0)=0,y'(0)=1$ 的特解，并判断其在 $[0,+\\infty)$ 上是否有界。\n\\end{problem}\n\\begin{problem}{729}{107}{不同实根与初值问题}\n求 $y''+5y'+4y=0$ 的通解。再求满足 $y(0)=1,y'(0)=0$ 的解，证明该解在 $x\\ge0$ 上恒正且不增加，并求其极限。\n\\end{problem}\n\\begin{problem}{730}{107}{初值解与极值}\n求 $y''+4y'+3y=0$、$y(0)=2,y'(0)=6$ 的特解。确定它在 $[0,+\\infty)$ 上的零点及极值，并求最大值。\n\\end{problem}\n\\begin{problem}{731}{107}{重复特征根与独立解}\n求 $4y''-12y'+9y=0$ 的通解，证明所取两个解线性无关。再确定全部满足 $\\lim_{x\\to+\\infty}y(x)=0$ 的解，并说明只消去指数项中的一个系数为何不够。\n\\end{problem}\n\\begin{problem}{732}{107}{临界阻尼型初值问题}\n求 $s''+2s'+s=0$（自变量为 $t$），$s(0)=2,s'(0)=-1$ 的解。证明它在 $t\\ge0$ 上恒正且严格减少，求其极限，并说明极限值是否在有限时刻取到。\n\\end{problem}\n\\begin{problem}{733}{107}{复特征根与零点间隔}\n求 $y''+8y'+17y=0$ 的通解。证明任意非零解在 $x\\ge0$ 上有无穷多个零点，求相邻零点间距，并判断其是否趋于零。\n\\end{problem}\n\\begin{problem}{734}{107}{衰减振荡与初值确定}\n求 $y''+10y'+29y=0$、$y(0)=1,y'(0)=-1$ 的特解。把三角部分化为单一余弦形式，确定其振幅包络，并求第一个正零点。\n\\end{problem}\n\\begin{supplement}{7.7-1}{重根、参数与长期行为}\n求初值问题 $y''+2ay'+a^2y=0$、$y(0)=0$、$y'(0)=1$ 的解。讨论实参数 $a$ 使解在 $[0,+\\infty)$ 上有界或趋于零的条件，并在 $a>0$ 时求其最大值。\n\\end{supplement}\n\\begin{supplement}{7.7-2}{阻尼分类与无零点条件}\n考虑 $y''+2\\zeta y'+y=0$，$y(0)=1$、$y'(0)=0$，其中 $\\zeta\\ge0$。分别求 $0\\le\\zeta<1$、$\\zeta=1$、$\\zeta>1$ 时的解，并确定解在 $x>0$ 上始终为正的参数范围。\n\\end{supplement}\n\\subsection{常系数非齐次线性微分方程}\n\\begin{problem}{739}{108}{多项式特解与通解}\n求 $y''-4y'+3y=x$ 的一个一次多项式特解及通解。证明一次多项式特解唯一，并求满足 $y(0)=y'(0)=0$ 的特解。\n\\end{problem}\n\\begin{problem}{740}{108}{多项式外力与长期行为}\n求 $y''+5y'+4y=3-2x$ 的通解。证明所有解与同一个一次多项式之差在 $x\\to+\\infty$ 时趋于零，并写出该多项式。\n\\end{problem}\n\\begin{problem}{741}{108}{零特征根与待定系数形式}\n求 $2y''+5y'=5x^2-2x-1$ 的通解。先说明特解为何需要三次多项式；再求满足 $y(0)=y'(0)=0$ 的特解，并核验常数项可并入齐次解。\n\\end{problem}\n\\begin{problem}{742}{108}{由齐次通解恢复系数与求特解}\n已知 $y''+ay'+by=0$ 的通解为 $(C_1+C_2x)e^x$。求 $a,b$，再求 $y''+ay'+by=x$ 满足 $y(0)=2,y'(0)=0$ 的解，分别核验方程及初值。\n\\end{problem}\n\\begin{problem}{743}{109}{混合外力与共振特解形式}\n对 $y''-5y'+6y=3x+2e^{2x}$，说明为何可设特解为 $Ax+B+Cxe^{2x}$，求出系数并写出通解。解释指数项前乘 $x$ 的原因，以及单设 $Ce^{2x}$ 为什么无效。\n\\end{problem}\n\\begin{problem}{744}{109}{指数多项式与单根共振}\n求 $y''-3y'+2y=xe^{2x}$ 的通解。先写出最小的待定系数特解形式，再求满足 $y(0)=y'(0)=0$ 的特解，并用代换 $y=e^{2x}v$ 核验。\n\\end{problem}\n\\begin{problem}{745}{109}{已知非齐次解反求常系数}\n已知 $y=e^{-2x}+(x^2+2)e^x$ 是 $y''+ay'+by=(cx+d)e^x$ 的解，其中 $a,b,c,d$ 为常数。求全部系数并证明其唯一性，再写出该方程通解。\n\\end{problem}\n\\begin{problem}{746}{109}{三个解恢复方程与外力}\n某首项系数为 $1$ 的二阶常系数非齐次方程有三个解 $y_1=e^{2x}+xe^x$、$y_2=e^{-x}+xe^x$、$y_3=e^{2x}-e^{-x}+xe^x$。求方程及通解，并说明如何先从解的差恢复齐次部分，再恢复外力项。\n\\end{problem}\n\\begin{problem}{747}{109}{复根共振与候选解验证}\n对 $y''-2y'+5y=e^x\\cos2x$，分别检验 $xe^x(\\cos2x+\\sin2x)$、$e^x(\\cos2x+\\sin2x)$、$\\frac14xe^x\\cos2x$、$\\frac14xe^x\\sin2x$ 是否为特解。选出成立者，写出通解，并说明共振所需的 $x$ 因子。\n\\end{problem}\n\\begin{problem}{748}{109}{倍角分解与三角共振}\n求 $y''+4y=\\cos^2x$ 的一个特解及通解。先把外力分解为常数项与三角项，分别说明其待定系数形式；再求满足 $y(0)=y'(0)=0$ 的解。\n\\end{problem}\n\\begin{problem}{749}{109}{多项式三角外力}\n求 $y''+4y=x\\cos x$ 的通解。说明特解中为何必须同时包含一次多项式乘 $\\cos x$ 与一次多项式乘 $\\sin x$，并求满足 $y(0)=y'(0)=0$ 的特解。\n\\end{problem}\n\\begin{problem}{750}{109}{外力叠加与指数共振}\n求 $y''-y=e^x+4\\cos x$ 的通解。分别处理两种外力并说明指数项的共振，再求满足 $y(0)=y'(0)=0$ 的特解，判断其在 $[0,+\\infty)$ 上是否有界。\n\\end{problem}\n\\begin{supplement}{7.8-1}{共振与参数分类}\n对 $\\omega>0$，求初值问题 $y''+y=\\cos\\omega x$、$y(0)=y'(0)=0$ 的解，分别讨论 $\\omega\\ne1$ 与 $\\omega=1$。判断解有界的参数条件，并说明共振时无界项的来源。\n\\end{supplement}\n\\begin{supplement}{7.8-2}{指数多项式外力与特解形式}\n求 $y''-2y'+y=e^x(x+1)$ 的通解及满足 $y(0)=y'(0)=0$ 的特解。先写出待定系数法所需的特解形式，并用 $y=e^xv$ 的代换核验计算结果。\n\\end{supplement}\n"}

## tool · 2026-10-20T02:40:49Z


Script completed
Wall time 0.7 seconds
Output:

{"chunk_id":"f14ae3","wall_time_seconds":0.000025125,"exit_code":0,"original_token_count":630,"output":"\\section{第7章 微分方程}\n\\subsection{微分方程的基本概念}\n\\begin{problem}{660}{97}{特解验证与通解区分}\n验证 $y=5x^2$ 是 $xy'-2y=0$ 的解，说明它是通解还是特解。求该方程在 $x>0$ 上的通解及满足 $y(1)=5$ 的解，并解释为何讨论通解时需要指定区间。\n\\end{problem}\n\\begin{problem}{661}{98}{解族验证与初值确定}\n验证 $y=C_1\\cos x+C_2\\sin x$ 是 $y''+y=0$ 的解，并证明两个常数独立。求满足 $y(0)=2$、$y'(0)=3$ 的特解及其最大值。\n\\end{problem}\n\\begin{problem}{662}{98}{任意常数个数与通解判定}\n验证 $y=x^2/2+x+C$ 满足 $y''-y'=-x$。判断该一参数解族是否为通解；求完整通解，并给出一个不属于上述一参数族的解。说明仅验证代入成立为何还不能判定为通解。\n\\end{problem}\n\\begin{problem}{663}{98}{隐函数解与正则分支}\n在 $x>0$、$y>0$、$y\\ne1$ 的正则分支上，验证 $y=\\ln(xy)$ 所确定的函数满足\n\\[\nx(y-1)y''+x(y')^2+(y-2)y'=0.\n\\]\n说明该隐式关系给出通解还是特解，并解释为何必须排除 $y=1$ 处直接视作 $y(x)$ 求导。\n\\end{problem}\n\\begin{supplement}{7.1-1}{解族、奇解与初值唯一性}\n验证 $y=(x-C)^2$ 在 $x\\ge C$ 上满足 $y'=2\\sqrt y$，并验证 $y\\equiv0$ 也是解。对初值 $y(0)=0$，构造至少两个在 $[0,+\\infty)$ 上不同的解，说明直接分离变量可能遗漏什么解。\n\\end{supplement}\n\\begin{supplement}{7.1-2}{消去常数与微分方程阶数}\n消去曲线族 $y=C_1e^x+C_2e^{-x}+x$ 中的任意常数，建立二阶微分方程。再求该方程满足 $y(0)=1$、$y'(0)=0$ 的特解，并核验两个初始条件。\n\\end{supplement}\n\\subsection{可分离变量的微分方程}\n\\begin{problem}{665}{99}{变量分离与奇点两侧解}\n求 $y'=y(1-x)/x$ 在 $x>0$ 上的通解，包括零解；求满足 $y(1)=e^{-1}$ 的解。讨论该特解能否延拓为在全实轴上满足 $xy'=(1-x)y$ 的可导解。\n\\end{problem}\n\\begin{problem}{666}{99}{变量分离与解的定义区间}\n求 $y'=\\sin x\\cos x/y^2$ 的隐式通解。求满足 $y(0)=1$ 的解及其在实轴上的有界性；说明为什么通解中必须限制 $y\\ne0$，而不能把零函数补作解。\n100:\\begin{problem}{687}{101}{齐次线性方程与初值符号}\n106:\\begin{problem}{690}{102}{一阶线性方程与平衡解}\n209:\\begin{problem}{729}{107}{不同实根与初值问题}\n224:\\begin{problem}{734}{107}{衰减振荡与初值确定}\n227:\\begin{supplement}{7.7-1}{重根、参数与长期行为}\n"}
{}
{"chunk_id":"645803","wall_time_seconds":0.31833775,"exit_code":1,"original_token_count":180,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 105, in <module>\n    totals = check_structure()\n             ^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 69, in check_structure\n    assert not errors, json.dumps(errors, ensure_ascii=False)\n           ^^^^^^^^^^\nAssertionError: [{\"chapter\": 7, \"section\": 2, \"missing\": [668, 677], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 5, \"missing\": [703, 704, 705, 706, 707, 708, 709, 710, 711, 712], \"extra\": [], \"in_order\": true}, {\"chapter\": 7, \"section\": 7, \"missing\": [735, 736], \"extra\": [], \"in_order\": true}]\n"}

## tool · 2026-10-20T02:45:49Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"c2df64","wall_time_seconds":0.000066292,"exit_code":0,"original_token_count":384,"output":"第7章\n微分方程\n\n第一节 微分方程的基本概念\n\n一、微分方程的定义\n\n定义1：表示未知函数、未知函数的导数与自变量之间关系的方程，叫作微分方程，有时也简称方程.\n\n评注\n方程中必须出现未知函数的导数或微分才能称为微分方程.\n\n定义2：微分方程中所出现的未知函数的最高阶导数的阶数，叫作微分方程的阶.\n\n657 基础题 下列方程是微分方程的是（    ）.\n\n(A) $ x^{2}+x+1=0 $\n(B) $ y^{2}+2x+1=0 $\n(C) $ x^{2}y^{2}+y=3 $\n(D) $ x^{2}+y^{\\prime}+y=2 $657 基础题 下列方程是微分方程的是（    ）.\n(A) $ x^{2}+x+1=0 $ (B) $ y^{2}+2x+1=0 $\n(C) $ x^{2} y^{2}+y=3 $ (D) $ x^{2}+y^{\\prime}+y=2 $\n658 基础题 微分方程 $ y^{\\prime\\prime}-2 x \\left( y^{\\prime} \\right)^{3}+y^{2}=0 $的阶数是（    ）.\n659 基础题 微分方程 $ x \\mathrm{d} y+(x+y) \\mathrm{d} x=0 $的阶数是（    ）.\n\n二、微分方程解的定义\n定义1：满足微分方程的函数，称为微分方程的解.\n定义2：如果微分方程的解中含有任意常数，且任意常数的个数与微分方程的阶数相同，则称之为微分方程的通解.\n评注\n通解里所说的任意常数是独立的，也就是说，它们不能合并而使得任意常数的个数减少.\n定义3：微分方程的不含任意常数的解，称为特解.\n定义4：由通解确定特解的条件，称为初始条件.\n660 基础题 判断 $ y=5 x^{2} $是否是微分方程 $ x y^{\\prime}-2 y=0 $的解，是通解还是特解？"}
{"chunk_id":"9e85b9","wall_time_seconds":0.000026417,"exit_code":0,"original_token_count":956,"output":"    for chapter, ranges in EXPECTED.items():\n        text = (CHAPTERS / f\"ch{chapter:02d}.tex\").read_text()\n        _, position, length = LatexWalker(text, latex_context=CONTEXT, tolerant_parsing=False).get_latex_nodes()\n        assert position == 0 and length == len(text)\n        sections = re.split(r\"\\\\subsection\\{[^}]+\\}\", text)[1:]\n        assert len(sections) == len(ranges), (chapter, len(sections))\n        count = 0\n        for index, (section, (first, last)) in enumerate(zip(sections, ranges), 1):\n            problems = re.findall(r\"\\\\begin\\{problem\\}\\{(\\d+)\\}\\{(\\d+)\\}\\{([^}]+)\\}\", section)\n            ids = [int(item[0]) for item in problems]\n            expected = list(range(first, last + 1))\n            if ids != expected:\n                errors.append({\"chapter\": chapter, \"section\": index,\n                               \"missing\": sorted(set(expected) - set(ids)),\n                               \"extra\": sorted(set(ids) - set(expected)),\n                               \"in_order\": ids == sorted(set(ids))})\n            supplements = re.findall(r\"\\\\begin\\{supplement\\}\\{([^}]+)\\}\", section)\n            assert supplements == [f\"{chapter}.{index}-1\", f\"{chapter}.{index}-2\"], supplements\n            assert len(problems) == section.count(r\"\\end{problem}\")\n            assert len(supplements) == section.count(r\"\\end{supplement}\")\n            assert all(76 <= int(page) <= 109 and direction for _, page, direction in problems)\n            assert section.rfind(r\"\\end{problem}\") < section.find(r\"\\begin{supplement}\")\n            count += len(problems) + len(supplements)\n        assert not any(marker in text for marker in [\"TODO\", \"待补\", \"题目略\", \"同上题\"])\n        totals[chapter] = count\n    assert not errors, json.dumps(errors, ensure_ascii=False)\n    return totals\n\n\ndef check_mathematics():\n    near(integral(lambda x: x / (1 + x * x), 0, 1), math.log(2) / 2)\n    near(integral(lambda x: x / (x * x - 2), 2, 2 * math.sqrt(2)), math.log(3) / 2)\n    for a in [0.2, 1, 3]:\n        f = lambda x: math.sin(x) / (math.sin(x) + a * math.cos(x))\n        g = lambda x: math.sin(x) / (math.sin(x) + math.cos(x) / a)\n        near(integral(f, 0, math.pi / 2) + integral(g, 0, math.pi / 2), math.pi / 2)\n    near(integral(lambda x: 2 * x - x * x, 0, 2), 4 / 3)\n    near(integral(lambda x: (2 * x)**2 - x**4, 0, 2), 64 / 15)\n    near(integral(lambda x: 0.25 - x*x, 0, 0.5)\n         + integral(lambda x: x*x - 0.25, 0.5, 1), 0.25)\n    near(integral(lambda x: ((x + 1) / 2)**2 - x, 0, 1), 1 / 12)\n    near(2 * integral(lambda x: x * ((x + 1) / 2 - math.sqrt(x)), 0, 1), 1 / 30)\n    near(integral(lambda s: 400 + 2000 - 20*s/3 + 50*(30-s), 0, 30), 91500)\n    for x in [0.2, 0.7, 2]:\n        radius = (4*x + 1)**1.5 / 2\n        near(3 * radius * 6 / math.sqrt(4*x+1) - (6*math.sqrt(x))**2, 9)\n        f = lambda t: -1 / (1+t)\n        near(derivative(f, x), f(x)**2)\n        y = lambda t: math.sqrt(1+t*t)\n        near(y(x)**3 * second(y, x), 1, 2e-6)\n        y = lambda t: math.log(math.cosh(t))\n        near(second(y, x) + derivative(y, x)**2, 1, 2e-6)\n        y = lambda t: math.exp(-2*t) + (t*t+2)*math.exp(t)\n        near(second(y, x) + derivative(y, x) - 2*y(x), (6*x+2)*math.exp(x), 2e-6)\n        y = lambda t: 0.25*t*math.exp(t)*math.sin(2*t)\n        near(second(y, x) - 2*derivative(y, x) + 5*y(x), math.exp(x)*math.cos(2*x), 2e-6)\n    return \"积分换元、对称性、面积体积、做功、曲率与微分方程代表计算通过\"\n\n\nif __name__ == \"__main__\":\n    mathematics = check_mathematics()\n    totals = check_structure()\n    print(json.dumps({\"status\": \"passed\", \"type\": \"read_only_check\",\n                      \"message\": mathematics, \"counts\": totals,\n                      \"suggestion\": \"本检查不替代排版编译与全部题目的逐项数学审查\"}, ensure_ascii=False))\n"}

## tool · 2026-10-20T02:46:10Z


Script completed
Wall time 0.2 seconds
Output:

{"chunk_id":"2aa711","wall_time_seconds":0.000009292,"exit_code":0,"original_token_count":448,"output":"703 基础题 水 $ y'' = e^{3x} + \\sin 2x $的通解.\n\n704 基础题 求微分方程 $ y'' = x e^{x} $的通解.\n\n705 基础题 求微分方程 $ y'' = \\frac{1}{1+x^{2}} $的通解.\n\n706 中等题 求微分方程 $ y'' = e^{2x} $满足初始条件 $ y \\big|_{x=1} = y' \\big|_{x=1} = y'' \\big|_{x=1} = 0 $的特解.\n\n707 中等题 已知一曲线经过点(0,1)并在此点与直线 $ y = \\frac{x}{2} + 1 $相切，且满足 $ y'' = x $求此曲线方程.\n\n二、$ y'' = f(x,y') $型的微分方程的求解方法\n\n第1步：换元. 令 $ y' = p $，则 $ y'' = p' $，则原方程变为 $ p' = f(x,p) $，此方程为一阶方程.\n\n第2步：解方程 $ p' = f(x,p) $. 设其解为 $ p = \\varphi(x,C_{1}) $，即 $ y' = \\varphi(x,C_{1}) $.\n\n第3步：两端积分. 对 $ y' = \\varphi(x,C_{1}) $两端积分即可得到原方程的通解为 $ y = \\int \\varphi(x,C_{1}) \\mathrm{d} x + C_{2} $.第 2 步：解方程 $p' = f(x,p)$. 设其解为 $p = \\varphi(x,C_1)$, 即 $y' = \\varphi(x,C_1)$.\n\n第 3 步：两端积分. 对 $y' = \\varphi(x,C_1)$ 两端积分即可得到原方程的通解为 $y = \\int \\varphi(x,C_1) \\mathrm{d}x + C_2$.\n\n708 基础题 求微分方程 $y'' = y' + x$ 的通解.\n\n709 基础题 求微分方程 $y'' + (y')^2 + 1 = 0$ 的通解.\n\n710 基础题 求微分方程 $xy'' + 3y' = 0$ 的通解.\n\n711 基础题 求微分方程 $y'' - 2y'^2 = 0$ 满足初始条件 $y|_{x=0} = 0$, $y'|_{x=0} = -1$ 的特解.\n\n712 基础题 求微分方程 $(1+x^2)y'' = 2xy'$ 满足初始条件 $y|_{x=0} = 1$, $y'|_{x=0} = 3$ 的特解.\n\n三、$y'' = f(y,y')$ 型的微分方程的求解方法\n\n第 1 步：换元. 令 $y' = p$, 则 $y'' = \\frac{dp}{dx} = \\frac{dp}{dy} \\cdot \\frac{dy}{dx} = p \\frac{dp}{dy}$, 则原方程变为 $p \\frac{dp}{dy} = f(y,p)$, 此方程为一阶微分方程."}
{"chunk_id":"c9c0b4","wall_time_seconds":0.000009333,"exit_code":0,"original_token_count":529,"output":"665 基础题 求微分方程 $\\frac{\\mathrm{d}y}{\\mathrm{d}x} = \\frac{y(1-x)}{x}$ 的通解.\n\n666 基础题 求微分方程 $\\frac{\\mathrm{d}y}{\\mathrm{d}x} = \\frac{\\sin x\\cos x}{y^2}$ 的通解.\n\n667 基础题 求微分方程 $(1 + \\mathrm{e}^x)\\mathrm{d}y - y\\mathrm{e}^x\\mathrm{d}x = 0$ 满足初始条件 $y|_{x=0} = 2$ 的特解.\n\n668 基础题 求微分方程 $(xy^2 + x)\\mathrm{d}x + (y - x^2y)\\mathrm{d}y = 0$ 满足初始条件 $y|_{x=0} = 1$ 的特解.\n\n669 中等题 求微分方程 $\\mathrm{e}^{x-y}\\mathrm{d}x + y\\mathrm{d}y = 0$ 满足初始条件 $y|_{x=0} = 1$ 的特解.\n\n670 中等题 已知曲线 $y = y(x)$ 上任一点 $P(x,y)$ 处的切线斜率为 $\\frac{y^2}{1+x^2}$，且曲线过 (0,-1) 点，求该曲线的方程.\n\n671 中等题 设 $f(x)$ 为连续函数，且满足 $f(x) = \\int_0^{3x} f\\left(\\frac{t}{3}\\right)\\mathrm{d}t + 2$，求 $f(x)$.\n\n672 中等题 设当 $x \\geqslant 0$ 时 $f(x)$ 有一阶连续导数，并且满足 $f(x) = 2\\int_0^{x}(x-t)f(t)f'(t)\\mathrm{d}t + x - 1$，求当 $x \\geqslant 0$ 时的 $f(x)$.671 中等题 设 $ f(x) $为连续函数，且满足 $ f(x)=\\int_{0}^{3 x} f\\left(\\frac{t}{3}\\right) \\mathrm{d} t+2 $，求 $ f(x). $\n672 中等题 设当 $ x\\geqslant 0 $时 $ f(x) $有一阶连续导数，并且满足 $ f(x)=2 \\int_{0}^{x} \\left(x-t\\right) f(t) f^{\\prime}(t) \\mathrm{d} t+x-1 $，求当 $ x\\geqslant 0 $时的 $ f(x). $\n673 中等题 设函数 $ f(x) $连续，且满足 $ \\int_{0}^{x} f(t) \\mathrm{d} t=\\int_{0}^{x} t f(x-t) \\mathrm{d} t+x $，求 $ f(x) $的表达式.\n674 中等题 设非零函数 $ f(x) $连续，且满足 $ f(x)=\\int_{0}^{x} f(t) \\mathrm{d} t+2 \\int_{0}^{1} t f^{2}(t) \\mathrm{d} t $，求 $ f(x) $的表达式.\n675 中等题 设函数 $ f(x) $在 $ (-\\infty,+\\infty) $内可导，且满足 $ f^{\\prime}(x)=\\frac{x}{1+x^{2}} f(x) $， $ f(0)=a. $\n若 $ \\int_{0}^{\\sqrt{3}} x f(x) \\mathrm{d} x=7 $，求 $ a $的值.\n676 中等题 求微分方程 $ y^{\\prime}=y^{2}+2(\\sin x-1) y+\\sin^{2} x-2 \\sin x-\\cos x+1 $的通解.\n677 中等题 求微分方程 $ y(xy+1) \\mathrm{d} x+x(1+xy+x^{2} y^{2}) \\mathrm{d} y=0 $的通解."}
{"chunk_id":"099c54","wall_time_seconds":0.000007625,"exit_code":0,"original_token_count":436,"output":"\\section{第7章 微分方程}\n\\subsection{微分方程的基本概念}\n\\begin{problem}{657}{97}{微分方程辨识与阶数}\n设 $y=y(x)$，分别判断 $x^2+x+1=0$、$y^2+2x+1=0$、$x^2y''+y=3$、$x^2+y^2+y'=2$ 是否为微分方程；对符合者给出阶数及是否线性的判断，说明未知函数的代数幂次为何不能用来判定阶数。\n\\end{problem}\n\\begin{problem}{658}{97}{导数阶数与非线性}\n判断 $y'''-2x(y')^3+y^2=0$ 的阶数及线性性质。若给定 $y(0),y'(0),y''(0)$，指出还需要多少个独立初值才能形成通常的三阶初值问题；解释 $(y')^3$ 的指数与三阶导数的区别。\n\\end{problem}\n\\begin{problem}{659}{97}{微分形式与标准形式}\n将 $x\\dd y+(x+y)\\dd x=0$ 在 $x>0$ 上写为标准形式并判断阶数。求通解及满足 $y(1)=0$ 的解，说明化为标准形式时对 $x=0$ 作了什么限制。\n\\end{problem}\n\\begin{problem}{660}{97}{特解验证与通解区分}\n验证 $y=5x^2$ 是 $xy'-2y=0$ 的解，说明它是通解还是特解。求该方程在 $x>0$ 上的通解及满足 $y(1)=5$ 的解，并解释为何讨论通解时需要指定区间。\n\\end{problem}\n164:\\begin{problem}{702}{102}{连续积分与初值数目}\n165-求 $y^{(4)}=x$ 的通解，说明四个积分常数独立。再求满足 $y(0)=y'(0)=y''(0)=0$、$y'''(0)=1$ 的特解，并核验四个条件。\n166-\\end{problem}\n167:\\begin{problem}{713}{104}{不显含自变量与常值解}\n168-求 $yy''+2(y')^2=0$ 在 $y\\ne0$ 区间上的通解，并检查常值解是否包含其中。采用 $p=y'$ 降阶，或利用 $y^3$ 的二阶导数求解；说明非常值解为何不能以可导方式跨越其零点。\n169-\\end{problem}\n170-\\begin{problem}{714}{104}{乘积求导与正值初始分支}\n"}

## tool · 2026-10-20T02:47:01Z


Script completed
Wall time 0.3 seconds
Output:

{}
{"chunk_id":"28e982","wall_time_seconds":0.008592834,"exit_code":1,"original_token_count":128,"output":"Traceback (most recent call last):\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 105, in <module>\n    totals = check_structure()\n             ^^^^^^^^^^^^^^^^^\n  File \"/Users/oyamahappa/Documents/Agent/Codex/.agent/math-analysis/upper/check_5_7.py\", line 69, in check_structure\n    assert not errors, json.dumps(errors, ensure_ascii=False)\n           ^^^^^^^^^^\nAssertionError: [{\"chapter\": 7, \"section\": 7, \"missing\": [735, 736], \"extra\": [], \"in_order\": true}]\n"}
{"chunk_id":"f8b6fe","wall_time_seconds":0.000006709,"exit_code":0,"original_token_count":10,"output":"107-crop0.0-0.55.md\n107-crop0.45-1.0.md\n"}

## tool · 2026-10-20T02:47:05Z


Script completed
Wall time 0.1 seconds
Output:

{"chunk_id":"d2bc78","wall_time_seconds":0.000010625,"exit_code":0,"original_token_count":558,"output":"726 基础题 通解为 $ y=C_{1} \\mathrm{e}^{6 x}+C_{2} \\mathrm{e}^{-8 x} $的二阶常系数齐次线性微分方程为（    ）.\n(A) $ y^{\\prime \\prime}+2 y^{\\prime}+4 8 y=0 $ (B) $ y^{\\prime \\prime}+2 y^{\\prime}-4 8 y=0 $\n(C) $ y^{\\prime \\prime}-2 y^{\\prime}+4 8 y=0 $ (D) $ y^{\\prime \\prime}-2 y^{\\prime}-4 8 y=0 $\n727 基础题 以 $ y_{1}=\\mathrm{e}^{2 x} \\sin 3 x $， $ y_{2}=\\mathrm{e}^{2 x} \\cos 3 x $为特解的二阶常系数齐次线性微分方程为（    ）.\n(A) $ y^{\\prime \\prime}+4 y^{\\prime}+1 3 y=0 $ (B) $ y^{\\prime \\prime}-4 y^{\\prime}-1 3 y=0 $\n(C) $ y^{\\prime \\prime}+4 y^{\\prime}-1 3 y=0 $ (D) $ y^{\\prime \\prime}-4 y^{\\prime}+1 3 y=0 $\n728 基础题 已知 $ y=x \\mathrm{e}^{2 x} $是二阶常系数齐次线性微分方程 $ y^{\\prime \\prime}+p y^{\\prime}+q y=0 $的一个特解，求 $ p $和 $ q $的值.\n729 基础题 求方程 $ y^{\\prime \\prime}+5 y^{\\prime}+4 y=0 $的通解.\n730 基础题 求方程 $ y^{\\prime \\prime}+4 y^{\\prime}+3 y=0 $满足初始条件 $ y \\big|_{x=0}=2 $， $ y^{\\prime} \\big|_{x=0}=6 $的特解.\n731 基础题 求方程 $ 4 y^{\\prime \\prime}-1 2 y^{\\prime}+9 y=0 $的通解.730 基础题 求方程 $ y^{\\prime}+4 y^{\\prime}+3 y=0 $满足初始条件 $ y\\left|_{x=0}=2, y\\left|_{x=0}=6 \\right. $的特解.\n\n731 基础题 求方程 $ 4 y^{\\prime\\prime}-1 2 y^{\\prime}+9 y=0 $的通解.\n\n732 基础题 求方程 $ \\frac{\\mathrm{d}^{2} s}{\\mathrm{d} t^{2}}+2 \\frac{\\mathrm{d} s}{\\mathrm{d} t}+s=0 $满足初始条件 $ s\\left|_{t=0}=2, s^{\\prime}\\left|_{t=0}=-1 \\right. $的特解.\n\n733 基础题 求方程 $ y^{\\prime\\prime}+8 y^{\\prime}+1 7 y=0 $的通解.\n\n734 基础题 求方程 $ y^{\\prime\\prime}+1 0 y^{\\prime}+2 9 y=0 $满足初始条件 $ y\\left|_{x=0}=1, y^{\\prime}\\left|_{x=0}=-1 \\right. $的特解.\n\n735 基础题 求方程 $ y^{\\prime\\prime}+y^{\\prime}-y^{\\prime}-y=0 $的通解.\n\n736 基础题 求方程 $ y^{(4)}-y^{\\prime\\prime}-y^{\\prime}-2 y=0 $的通解.\n\n737 中等题 已知函数 $ f(x) $满足 $ f^{\\prime}(x)=f\\left( \\frac{\\pi}{2}-x \\right) $，且 $ f(0)=f^{\\prime}(0)=1 $，求 $ f(x). $\n\n738 中等题 已知函数 $ f(x) $满足方程 $ f^{\\prime\\prime}(x)+f^{\\prime}(x)-2 f(x)=0 $及 $ f^{\\prime\\prime}(x)+f(x)=2 \\mathrm{e}^{x}, $求 $ f(x). $"}
{"chunk_id":"0267ac","wall_time_seconds":0.000007083,"exit_code":0,"original_token_count":270,"output":"第2步：解方程 $p \\frac{\\mathrm{d}p}{\\mathrm{d}y} = f(y,p)$. 设其解为 $p = \\varphi(y,C_1)$, 即 $y' = \\varphi(y,C_1)$.\n\n第3步：解方程 $y' = \\varphi(y,C_1)$. 对 $y' = \\varphi(y,C_1)$ 分离变量可得 $\\frac{\\mathrm{d}y}{\\varphi(y,C_1)} = \\mathrm{d}x$, 两端积分即可得到原方程的通解为 $\\int \\frac{1}{\\varphi(y,C_1)} \\mathrm{d}y = x + C_2$.\n\n评注\n注意方程 $y'' = f(y,y')$ 与 $y'' = f(x,y')$ 的区别, 前者最大的特点是不含 $x$, 故换元时, 令 $y' = p$, 要把 $p$ 看成 $y$ 的函数, 从而 $y'' = \\frac{\\mathrm{d}p}{\\mathrm{d}x} = \\frac{\\mathrm{d}p}{\\mathrm{d}y} \\cdot \\frac{\\mathrm{d}y}{\\mathrm{d}x} = p \\frac{\\mathrm{d}p}{\\mathrm{d}y}$.\n\n713基础题 求微分方程 $yy'' + 2(y')^2 = 0$ 的通解.\n\n714基础题 求微分方程 $yy'' + (y')^2 = 0$ 满足初始条件 $y|_{x=0} = 1$, $y'|_{x=0} = \\frac{1}{2}$ 的特解.\n\n715中等题 求微分方程 $y^3 y'' - 1 = 0$ 的通解.\n\n716中等题 求微分方程 $y'' + (y')^2 = 1$ 满足初始条件 $y|_{x=0} = 0$, $y'|_{x=0} = 0$ 的特解.\n\n第六节 高阶线性微分方程"}

## tool · 2026-10-20T02:47:25Z


Script completed
Wall time 0.3 seconds
Output:

{"chunk_id":"c77c64","wall_time_seconds":0.000008416,"exit_code":0,"original_token_count":482,"output":"661 基础题 验证 $ y=C_{1}\\cos x+C_{2}\\sin x $是微分方程 $ y^{\\prime\\prime}+y=0 $的解，并求满足初始条件 $ y(0)=2, y^{\\prime}(0)=3 $的特解.\n\n662 中等题 已知函数 $ y=\\frac{1}{2}x^{2}+x+C $，微分方程 $ y^{\\prime\\prime}-y^{\\prime}=-x $，下列说法正确的是（    ）\n(A) $ y $是微分方程的通解\n(B) $ y $是微分方程满足条件 $ y\\left|_{x=0}=1 \\right. $的特解\n(C) $ y $是微分方程的解\n(D) 以上都不对\n\n663 中等题 判断二元方程 $ y=\\ln(xy) $所确定的函数是否为微分方程 $ (xy-x)y^{\\prime\\prime}+x(y^{\\prime})^{2}+yy^{\\prime}-2y^{\\prime}=0 $的解，是通解还是特解？\n\n第二节 可分离变量的微分方程\n\n一、可分离变量微分方程的定义\n\n定义：形如 $ \\frac{dy}{dx}=f_{1}(x)f_{2}(y) $或 $ M_{1}(x)M_{2}(y)\\mathrm{d}x+N_{1}(x)N_{2}(y)\\mathrm{d}y=0 $的微分方程称为可分离变量的微分方程.一、可分离变量微分方程的定义\n定义：形如 $ \\frac{\\mathrm{d} y}{\\mathrm{d} x}=f_{1}(x) f_{2}(y) $或 $ M_{1}(x) M_{2}(y) \\mathrm{d} x+N_{1}(x) N_{2}(y) \\mathrm{d} y=0 $的微分方程称为可分离变量的微分方程.\n\n二、可分离变量微分方程的求解方法\n第1步：分离变量. 一般地，把方程中与 y有关的项移到左边，与 x有关的项移到右边得\n$ g(y) \\mathrm{d} y=f(x) \\mathrm{d} x $\n第2步：上式两边同时积分，得 $ \\int g(y) \\mathrm{d} y=\\int f(x) \\mathrm{d} x $，则方程的隐式通解为 $ G(y)=F(x)+C $\n第3步：化简整理. 将上面得到的隐式通解尽量化简，能整理出显函数的形式最好，不好整理的，微分方程的通解写成隐函数的形式也是可以的.\n\n664基础题 下列微分方程不是一阶变量可分离的微分方程的是（    ）.\n(A) $ y^{\\prime}+xy=0 $\n(B) $ y^{2} \\mathrm{d} x+(2 x+1) \\mathrm{d} y=0 $\n(C) $ y^{\\prime}=x y \\mathrm{e}^{x+y} $\n(D) $ (x-y) \\mathrm{d} x+(x+y) \\mathrm{d} y=0 $"}
{"chunk_id":"f67c41","wall_time_seconds":0.000007875,"exit_code":0,"original_token_count":203,"output":"284:\\begin{problem}{734}{107}{衰减振荡与初值确定}\n285-求 $y''+10y'+29y=0$、$y(0)=1,y'(0)=-1$ 的特解。把三角部分化为单一余弦形式，确定其振幅包络，并求第一个正零点。\n286-\\end{problem}\n287:\\begin{problem}{737}{107}{反射导数关系与降阶恢复}\n288-设 $f$ 在实轴上可导，满足 $f'(x)=f(-x)$、$f(0)=1$。证明 $f$ 二阶可导并求 $f$，再代回反射关系核验，说明只满足导出的二阶方程为何还不足以完成验证。\n289-\\end{problem}\n290:\\begin{problem}{738}{107}{两个微分关系的相容性}\n291-设 $f$ 同时满足 $f''+f'-2f=0$ 与 $f'+f=2e^x$。求 $f$，先分别给出两个方程解的形式，再确定公共解，并证明其唯一性。\n292-\\end{problem}\n293-\\begin{supplement}{7.7-1}{重根、参数与长期行为}\n"}
{}
{"chunk_id":"8a617f","wall_time_seconds":0.000006417,"exit_code":0,"original_token_count":70,"output":"{\"status\": \"passed\", \"type\": \"read_only_check\", \"message\": \"积分换元、对称性、面积体积、做功、曲率与微分方程代表计算通过\", \"counts\": {\"5\": 104, \"6\": 60, \"7\": 110}, \"suggestion\": \"本检查不替代排版编译与全部题目的逐项数学审查\"}\n"}

## tool · 2026-10-20T02:47:32Z




## tool · 2026-10-20T02:47:37Z




## tool · 2026-10-20T02:48:49Z


Script completed
Wall time 0.6 seconds
Output:

{"chunk_id":"f45c6e","wall_time_seconds":0.0000125,"exit_code":0,"original_token_count":561,"output":"import json\nimport math\nimport re\nfrom pathlib import Path\n\nfrom pylatexenc.latexwalker import LatexWalker, get_default_latex_context_db\nfrom pylatexenc.macrospec import EnvironmentSpec\n\nROOT = Path(__file__).resolve().parents[3]\nCHAPTERS = ROOT / \"output/工科数学分析逐题训练-上册/chapters\"\nCONTEXT = get_default_latex_context_db()\nCONTEXT.add_context_category(\"upper_5_7\", environments=[\n    EnvironmentSpec(\"problem\", \"{{{\"), EnvironmentSpec(\"supplement\", \"{{\")], prepend=True)\nEXPECTED = {\n    5: [(505, 517), (518, 538), (539, 577), (578, 600)],\n    6: [(601, 649), (650, 656)],\n    7: [(657, 663), (664, 677), (678, 686), (687, 701),\n        (702, 716), (717, 724), (725, 738), (739, 750)],\n}\n\n\ndef near(actual, expected, tolerance=1e-7):\n    assert abs(actual - expected) <= tolerance * max(1, abs(expected)), (actual, expected)\n\n\n        near(derivative(f, x), f(x)**2)\n        y = lambda t: math.sqrt(1+t*t)\n        near(y(x)**3 * second(y, x), 1, 2e-6)\n        y = lambda t: math.log(math.cosh(t))\n        near(second(y, x) + derivative(y, x)**2, 1, 2e-6)\n        y = lambda t: math.exp(-2*t) + (t*t+2)*math.exp(t)\n        near(second(y, x) + derivative(y, x) - 2*y(x), (6*x+2)*math.exp(x), 2e-6)\n        y = lambda t: 0.25*t*math.exp(t)*math.sin(2*t)\n        near(second(y, x) - 2*derivative(y, x) + 5*y(x), math.exp(x)*math.cos(2*x), 2e-6)\n    return \"积分换元、对称性、面积体积、做功、曲率与微分方程代表计算通过\"\n\n\nif __name__ == \"__main__\":\n    mathematics = check_mathematics()\n    totals = check_structure()\n    print(json.dumps({\"status\": \"passed\", \"type\": \"read_only_check\",\n                      \"message\": mathematics, \"counts\": totals,\n                      \"suggestion\": \"本检查不替代排版编译与全部题目的逐项数学审查\"}, ensure_ascii=False))\n166:\\begin{problem}{653}{96}{变力做功与几何级数}\n167-桩入土深度为 $x$ 时阻力为 $kx$（$k>0$）。气锤首次击打将桩打入 $a>0$，以后每次做功均为前一次的 $r$ 倍（$0<r<1$）。求击打 $3$ 次后的总深度及无限次击打可达到的极限深度；再求达到给定深度 $d$ 所需的最少击打次数，说明哪些 $d$ 无法在有限次内达到。\n168-\\end{problem}\n"}
{}
{"chunk_id":"d0d8d1","wall_time_seconds":0.319193625,"exit_code":0,"original_token_count":76,"output":"{\"status\": \"passed\", \"type\": \"read_only_check\", \"message\": \"严格LaTeX解析、积分换元、对称性、面积体积、抽水功、曲率与微分方程代表计算通过\", \"counts\": {\"5\": 104, \"6\": 60, \"7\": 110}, \"suggestion\": \"本检查不替代排版编译与全部题目的逐项数学审查\"}\n"}

## tool · 2026-10-20T02:49:01Z




## assistant · 2026-10-20T02:49:07Z

妹妹，第5—7章已完成，共274题：246道原题逐题改编、28道补充题。三个章文件已稳定，可统一编号。

核验脚本 `check_5_7.py` 已通过严格 LaTeX 解析、完整覆盖、节归属与代表数学计算。

未编译、下载 TeX、截图或执行 Git；排版效果尚未验证。
