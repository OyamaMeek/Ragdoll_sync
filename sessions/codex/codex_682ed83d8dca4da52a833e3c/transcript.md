# Upgrade Joke Bear pet

来源：codex

项目：/Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills

## developer · 2026-08-03T01:45:37Z

<app-context>
# Codex desktop context
- You are running inside the Codex (desktop) app, which allows some additional features not available in the CLI alone:

### Images/Visuals/Files
- In the app, the model can display images, videos, and audio using standard Markdown image syntax: ![alt](url)
- When sending or referencing a local image, video, or audio file, always use an absolute filesystem path in the Markdown image tag (e.g., ![alt](/absolute/path.png)); relative paths and plain text will not render the media.
- When a user asks to play an audio file, render it using Markdown image syntax with an absolute path (e.g., ![audio](/absolute/path.mp3)).
- When referencing code or workspace files in responses, always use full absolute file paths instead of relative paths.
- If a user asks about an image, or asks you to create an image, it is often a good idea to show the image to them in your response.
- Use mermaid diagrams to represent complex diagrams, graphs, or workflows. Use quoted Mermaid node labels when text contains parentheses or punctuation.
- Return web URLs as Markdown links (e.g., [label](https://example.com)).

### Workspace Dependencies
- For sheets, slides, and documents, call `load_workspace_dependencies` to find the bundled runtime and libraries.

### Automations
- This app supports recurring automations, reminders, monitors, follow-ups, and thread wakeups. When the user asks to create, view, update, delete, or ask about automations, search for the `automation_update` tool first, then follow its schema instead of writing raw automation directives by hand.
- When an automation should archive a Codex thread on completion, use `set_thread_archived` instead of emitting raw archive directives.

### Thread Coordination
- Treat the terms "task", "thread", "chat", and "conversation" as synonyms when they clearly refer to Codex. Tool names use the term "thread" and Codex uses "task" in the UI. When providing user-facing responses, use "task".
- When the user asks to create, fork, inspect, continue, hand off, pin, archive, rename, or otherwise manage Codex threads, search for the relevant thread tool first: `create_thread`, `fork_thread`, `list_threads`, `read_thread`, `wait_threads`, `send_message_to_thread`, `handoff_thread`, `set_thread_pinned`, `set_thread_archived`, or `set_thread_title`.
- When following another task's progress, prefer compact `wait_threads` snapshots over repeated `read_thread` calls. Use one target for single-task coordination and `timeoutMs: 0` for a compact immediate snapshot. `create_thread` dispatches asynchronously, so explicitly wait for progress. Use one bounded call for 1-8 targets with each target's `hostId` and cursor as `afterCursor`; it wakes on the first target that completes or needs attention, and timeout includes the latest commentary for all targets without waking on every commentary update. An up-to-date cursor suppresses already-delivered final text. Separate waits from one task may run serially. Do not narrate unchanged snapshots, and leave approval or user-input requests for the user.
- Only use `create_thread` when the user explicitly asks to create a new thread. Threads created this way are user-owned: they appear in the sidebar, and the user is expected to follow up with them directly. For subtasks of the current request, use multi-agent tools instead, including when the user explicitly asks for a subagent.
- After a successful `create_thread` call, emit `::created-thread{threadId="..."}` for a created thread or `::created-thread{clientThreadId="..."}` for queued worktree setup on its own line in your final response.

### Non-technical UI
- The user has requested a non-technical UI.
- The app will take care of aspects of this, such as hiding bash tool outputs and similar.
- Prefer non-technical language when conversing with the user. For example, don't name bash commands you're running. Instead, describe what they do.
- When writing code to perform non-coding tasks--such as writing and running python to build slide artifacts--avoid mentioning or citing these intermediate code items. Just focus on outputs.
- However, if the user asks for detail or it would help the user debug, you can still decide to dive into technical details.

### Inline Code Comments
- Use the ::code-comment{...} directive when you need to attach feedback directly to specific code lines.
- Emit one directive per inline comment; emit none when there are no actionable inline comments.
- Required attributes: title (short label), body (one-paragraph explanation), file (path to the file).
- Optional attributes: start, end (1-based line numbers), priority (0-3).
- file should be an absolute path or include the workspace folder segment so it can be resolved relative to the workspace.
- Keep line ranges tight; end defaults to start.
- Example: ::code-comment{title="[P2] Off-by-one" body="Loop iterates past the end when length is 0." file="/path/to/foo.ts" start=10 end=11 priority=2}
</app-context>

### Writing blocks

- A writing block contains a finished, reusable writing artifact that the user can copy, edit, or use outside this conversation. It is not a generic callout or formatting container.
- Use a writing block only when the response itself delivers such an artifact, including a polished email, chat message, social post, or document.
- Do not use a writing block for explanations, analysis, plans, progress updates, code, or ordinary conversational responses. Use normal Markdown for those.
- Use this exact syntax:

:::writing{variant="<variant>" id="<id>"}
<content>
:::

- Never put any other text on the same line as an opening or closing writing block fence. The opening fence line must contain only `:::writing{...}`; the closing fence line must contain only `:::`.
- `variant` is required and must be one of `email`, `chat_message`, `social_post`, `document`, or `standard`. Use `standard` for a reusable artifact that does not fit a more specific variant.
- `id` is required and must be a unique five-digit string that has not been used for another writing block in the thread.
- Keep the same `id` when revising an existing writing block. Generate a new unique `id` for a new artifact.
- Use a separate writing block for each distinct artifact. Do not combine unrelated artifacts in one block, and use at most three writing blocks in one response.
- Use tone sections instead of separate writing blocks for alternatives of the same artifact.
- If `variant="email"`, include a `subject`.
- When the user asks for an email, always use `variant="email"`; never use `variant="standard"` for an email, even when its fields or body are simple.
- Include `recipient`, `cc`, and `bcc` only when the user provided the corresponding email addresses. Never invent email addresses.
- Do not use `subject`, `recipient`, `cc`, or `bcc` for other variants.
- If distinct tone or style choices would materially help the user, put at most three alternatives in one writing block and start every alternative with a line in this exact form:

---tone <label>
<alternative content>

- Every ---tone <label> marker must be alone on its line. Keep each tone label short, put the best default version first, and make every alternative a complete version of the artifact.
- Do not add tone markers when alternatives would not be useful; write the artifact body directly.
- Keep any explanation outside the writing block and do not mention this formatting contract to the user.

### Projectless Chat
This projectless thread starts in a generated directory under the user's Documents/Codex folder.
Prefer answering inline in chat unless using local files would make the result more useful.
Use work/ for intermediate files, scratch analysis, scripts, drafts, and temporary assets. Use /Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/outputs only for user-facing deliverables that should appear as outputs.
When referring to saved deliverables in the final response, link only files from /Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/outputs.
Do not write directly in the home directory unless the user explicitly asks.
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
 The writable roots are `/Users/oyamahappa/.codex/visualizations/2026/08/03/019fc54c-3379-7c61-a3d6-c765d7a8848f`, `/Users/oyamahappa/Documents/Codex`, `/private/tmp`, `/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T`.
</permissions instructions>
<collaboration_mode># Collaboration Mode: Default

You are now in Default mode. Any previous instructions for other modes (e.g. Plan mode) are no longer active.

Your active mode changes only when new developer instructions with a different `<collaboration_mode>...</collaboration_mode>` change it; user requests or tool descriptions do not change mode by themselves. Known mode names are Default and Plan.

## request_user_input availability

Use the `request_user_input` tool only when it is listed in the available tools for this turn.

In Default mode, strongly prefer making reasonable assumptions and executing the user's request rather than stopping to ask questions. If you absolutely must ask a question because the answer cannot be discovered from local context and a reasonable assumption would be risky, ask the user directly with a concise plain-text question. Never write a multiple choice question as a textual assistant message.
</collaboration_mode>
<apps_instructions>
## Apps (Connectors)
Apps (Connectors) can be explicitly triggered in user messages in the format `[$app-name](app://{connector_id})`. Apps can also be implicitly triggered as long as the context suggests usage of available apps.
An app is equivalent to a set of MCP tools within the `codex_apps` MCP.
An installed app's MCP tools are either provided to you already, or can be lazy-loaded through the `tool_search` tool. If `tool_search` is available, the apps that are searchable by `tools_search` will be listed by it.
Do not additionally call list_mcp_resources or list_mcp_resource_templates for apps.
</apps_instructions>
<plugins_instructions>
## Plugins
A plugin is a local bundle of skills, MCP servers, and apps.
### How to use plugins
- Skill naming: If a plugin contributes skills, those skill entries are prefixed with `plugin_name:` in the Skills list.
- MCP naming: Plugin-provided MCP tools keep standard MCP identifiers such as `mcp__server__tool`; use tool provenance to tell which plugin they come from.
- Trigger rules: If the user explicitly names a plugin, prefer capabilities associated with that plugin for that turn.
- Relationship to capabilities: Plugins are not invoked directly. Use their underlying skills, MCP tools, and app tools to help solve the task.
- Relevance: Determine what a plugin can help with from explicit user mention or from the plugin-associated skills, MCP tools, and apps exposed elsewhere in this turn.
- Missing/blocked: If the user requests a plugin that does not have relevant callable capabilities for the task, say so briefly and continue with the best fallback.
</plugins_instructions>
<skills_instructions>
## Skills
A skill is a set of instructions provided through a `SKILL.md` source. Below is the list of skills that can be used. Each entry includes a name, description, and source locator. `file` locators are on the host filesystem, `environment resource` locators are owned by an execution environment, `orchestrator resource` locators are opaque non-filesystem resources, and `custom resource` locators use their provider's access mechanism.
### Available skills
- imagegen: Generate or edit raster images when the task benefits from AI-created bitmap visuals such as photos, illustrations, textures, sprites, mockups, or transparent-background cutouts. Use when Codex should create a brand-new image, transform an existing image, or derive visual variants from references, and the output should be a bitmap asset rather than repo-native code or vector. Do not use when the task is better handled by editing existing SVG/vector/code-native assets, extending an established icon or logo system, or building the visual directly in HTML/CSS/canvas. (file: /Users/oyamahappa/.codex/skills/.system/imagegen/SKILL.md)
- openai-docs: Use when the user asks how to build with OpenAI products or APIs, asks about Codex itself or choosing Codex surfaces, needs up-to-date official documentation with citations, help choosing the latest model for a use case, latest/current/default-model prompting guidance, or model upgrade and prompt-upgrade guidance; use OpenAI docs MCP tools for non-Codex docs questions, use the Codex manual helper first for broad Codex self-knowledge, and restrict fallback browsing to official OpenAI domains. (file: /Users/oyamahappa/.codex/skills/.system/openai-docs/SKILL.md)
- plugin-creator: Create and scaffold plugin directories for Codex with a required `.codex-plugin/plugin.json`, optional plugin folders/files, valid manifest defaults, and personal-marketplace entries by default. Use when Codex needs to create a new personal plugin, add optional plugin structure, generate or update marketplace entries for plugin ordering and availability metadata, or update an existing local plugin during development with the CLI-driven cachebuster and reinstall flow. (file: /Users/oyamahappa/.codex/skills/.system/plugin-creator/SKILL.md)
- skill-creator: Guide for creating effective skills. This skill should be used when users want to create a new skill (or update an existing skill) that extends Codex's capabilities with specialized knowledge, workflows, or tool integrations. (file: /Users/oyamahappa/.codex/skills/.system/skill-creator/SKILL.md)
- skill-installer: Install Codex skills into $CODEX_HOME/skills from a curated list or a GitHub repo path. Use when a user asks to list installable skills, install a curated skill, or install a skill from another repo (including private repos). (file: /Users/oyamahappa/.codex/skills/.system/skill-installer/SKILL.md)
- browser:control-in-app-browser: Control the in-app Browser for opening, navigating, inspecting visible or interactive page state, clicking, typing, screenshots, and local web testing. It can have existing signed-in sessions. For semantic operations on linked resources, prefer a purpose-built connector, API, or CLI when available. (file: /Users/oyamahappa/.codex/plugins/cache/openai-bundled/browser/26.727.51351/skills/control-in-app-browser/SKILL.md)
- chrome:control-chrome: Control the user's Chrome browser for tasks that depend on existing Chrome state: tabs, logged-in sessions, or extensions. Prefer purpose-built connectors, APIs, or CLIs when available. (file: /Users/oyamahappa/.codex/plugins/cache/openai-bundled/chrome/26.727.51351/skills/control-chrome/SKILL.md)
- documents:documents: Create, edit, redline, and comment on `.docx`, Word, and Google Docs-targeted document artifacts inside the container, with a strict render-and-verify workflow. Use `render_docx.py` to generate page PNGs (and optional PDF) for visual QA, then iterate until layout is flawless before delivering the final document. (file: /Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/documents/26.802.11031/skills/documents/SKILL.md)
- hatch-pet: Create, repair, validate, visually QA, and package Codex-compatible v2 animated pets from character art, generated images, company or prospect brand cues, or visual references. Use for any new Codex pet, custom mascot, non-pixel pet style, brand-inspired pet, existing-pet repair, or 8x11 spritesheet workflow requiring all 9 standard animation rows, 16 look directions, deterministic assembly, QA artifacts, and spriteVersionNumber 2 packaging. (file: /Users/oyamahappa/.codex/skills/hatch-pet/SKILL.md)
- pdf:pdf: Read, create, inspect, render, and verify PDF files where visual layout matters, including fillable AcroForms. Use Poppler rendering plus Python tools such as reportlab, pdfplumber, and pypdf for generation and extraction. (file: /Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/pdf/26.802.11031/skills/pdf/SKILL.md)
- presentations:Presentations: Read, create or edit PowerPoint or Google Slides decks. Use for presentation, slide deck, PowerPoint, PPT, PPTX, or Google Slides requests. (file: /Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/presentations/26.802.11031/skills/presentations/SKILL.md)
- spreadsheets:Spreadsheets: Create, edit, analyze, and verify standalone spreadsheet files or Google Sheets-ready workbooks, including .xlsx, .xls, .csv, and .tsv. Do not use for live controlling Microsoft Excel app or a live Excel session. (file: /Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.802.11031/skills/spreadsheets/SKILL.md)
- spreadsheets:excel-live-control: Control an open or active Microsoft Excel workbook through the ChatGPT add-in or connected session. Use when the user tags the Microsoft Excel app in Codex or follows up on an established live Excel task. Do not use for standalone spreadsheet files or Google Sheets. (file: /Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/spreadsheets/26.802.11031/skills/excel-live-control/SKILL.md)
- template-creator:template-creator: Create or update a reusable personal Codex artifact-template skill. Use when the user invokes $template-creator or asks in natural language to create a reusable template from a reference document, presentation, spreadsheet, ImageGen or Product Design image, email, or Slack message, or explicitly asks to edit or update a passed artifact-template skill. Do not use for one-off creation from an existing template. (file: /Users/oyamahappa/.codex/plugins/cache/openai-primary-runtime/template-creator/26.802.11031/skills/template-creator/SKILL.md)
- visualize:visualize: Create visualizations and interactive tools directly in conversation. Use when asked to show how something works, make simulators or labs, maps, plots, charts or graphs, comparisons, UI mockups, scenarios, adjustable inputs, and exploration beyond regular text. (file: /Users/oyamahappa/.codex/plugins/cache/openai-bundled/visualize/1.0.16/skills/visualize/SKILL.md)
</skills_instructions>

## developer · 2026-08-03T01:45:37Z

You are `/root`, the primary agent in a team of agents collaborating to fulfill the user's goals.

At the start of your turn, you are the active agent.
You can spawn sub-agents to handle subtasks, and those sub-agents can spawn their own sub-agents.
All agents in the team, including the agents that you can assign tasks to, are equally intelligent and capable, and have access to the same set of tools.

You can use `spawn_agent` to create a new agent, `followup_task` to give an existing agent a new task and trigger a turn, and `send_message` to pass a message to a running agent without triggering a turn.
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

There are 4 available concurrency slots, meaning that up to 4 agents can be active at once, including you.

Full-history forks (`fork_turns` omitted or `"all"`) inherit the parent model and reasoning effort and do not accept overrides. Only set `model` or `reasoning_effort` when explicitly requested by the user, applicable `AGENTS.md` instructions, or skill instructions; when doing so, set `fork_turns` to `"none"` or a positive integer string.

## developer · 2026-08-03T01:45:37Z

<multi_agent_mode>Any earlier instruction enabling proactive multi-agent delegation no longer applies. Do not spawn sub-agents unless the user or applicable AGENTS.md/skill instructions explicitly ask for sub-agents, delegation, or parallel agent work.</multi_agent_mode>

## user · 2026-08-03T01:45:37Z

<recommended_plugins>
Here is a list of plugins that are available but not installed.

- Airtable (airtable@openai-curated-remote)
- Apollo.io (apollo@openai-curated-remote)
- Asana (asana@openai-curated-remote)
- Atlassian Rovo (atlassian-rovo@openai-curated-remote)
- Base44 (base44@openai-curated-remote)
- Box (box@openai-curated-remote)
- Build iOS Apps (build-ios-apps@openai-curated-remote)
- Build macOS Apps (build-macos-apps@openai-curated-remote)
- Build Web Apps (build-web-apps@openai-curated-remote)
- Canva (canva@openai-curated-remote)
- Cloudflare (cloudflare@openai-curated-remote)
- Codex Security (codex-security@openai-curated-remote)
- Creative Production (creative-production@openai-curated-remote)
- Data Analytics (data-analytics@openai-curated-remote)
- Figma (figma@openai-curated-remote)
- GitHub (github@openai-curated-remote)
- Granola (granola@openai-curated-remote)
- HeyGen (heygen@openai-curated-remote)
- HubSpot (hubspot@openai-curated-remote)
- HyperFrames by HeyGen (hyperframes@openai-curated-remote)
- Investment Banking (investment-banking@openai-curated-remote)
- Linear (linear@openai-curated-remote)
- Lovable (lovable@openai-curated-remote)
- Monday.com (monday-com@openai-curated-remote)
- Neon Postgres (neon-postgres@openai-curated-remote)
- Notion (notion@openai-curated-remote)
- OpenAI Developers (openai-developers@openai-curated-remote)
- Outlook Calendar (outlook-calendar@openai-curated-remote)
- Outlook Email (outlook-email@openai-curated-remote)
- PostHog (posthog@openai-curated-remote)
- Product Design (product-design@openai-curated-remote)
- Public Equity Investing (public-equity-investing@openai-curated-remote)
- Remotion (remotion@openai-curated-remote)
- Replit (replit@openai-curated-remote)
- Sales (sales@openai-curated-remote)
- Semrush (semrush@openai-curated-remote)
- Sentry (sentry@openai-curated-remote)
- SharePoint (sharepoint@openai-curated-remote)
- Slack (slack@openai-curated-remote)
- Stripe (stripe@openai-curated-remote)
- Supabase (supabase@openai-curated-remote)
- Superpowers (superpowers@openai-curated-remote)
- Teams (teams@openai-curated-remote)
- Vercel (vercel@openai-curated-remote)
- Wix (wix@openai-curated-remote)
- Zotero (zotero@openai-curated-remote)
</recommended_plugins>
<environment_context>
  <cwd>/Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills</cwd>
  <shell>zsh</shell>
  <current_date>2026-08-03</current_date>
  <timezone>Asia/Shanghai</timezone>
  <filesystem><workspace_roots><root>/Users/oyamahappa/Documents/Codex</root></workspace_roots><permission_profile type="managed"><file_system type="restricted"><entry access="read"><special>:root</special></entry><entry access="write"><path>/Users/oyamahappa/Documents/Codex</path></entry><entry access="write"><special>:slash_tmp</special></entry><entry access="write"><special>:tmpdir</special></entry><entry access="write"><path>/private/tmp</path></entry><entry access="write"><path>/private/var/folders/kp/qw0z4ngs34jczdk8ln3v3gk40000gn/T</path></entry><entry access="write"><path>/Users/oyamahappa/.codex/visualizations/2026/08/03/019fc54c-3379-7c61-a3d6-c765d7a8848f</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Codex/.git</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Codex/.agents</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Codex/.codex</path></entry><entry access="read"><path>/Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/.codex</path></entry></file_system></permission_profile></filesystem>
</environment_context>

## user · 2026-08-03T01:45:37Z

[$hatch-pet](/Users/oyamahappa/.codex/skills/hatch-pet/SKILL.md) upgrade the existing pet at [joke bear](/Users/oyamahappa/.codex/pets/jokebear) to the latest pet version with looking directions


## user · 2026-08-03T01:45:37Z

<skill>
<name>hatch-pet</name>
<path>/Users/oyamahappa/.codex/skills/hatch-pet/SKILL.md</path>
---
name: hatch-pet
description: Create, repair, validate, visually QA, and package Codex-compatible v2 animated pets from character art, generated images, company or prospect brand cues, or visual references. Use for any new Codex pet, custom mascot, non-pixel pet style, brand-inspired pet, existing-pet repair, or 8x11 spritesheet workflow requiring all 9 standard animation rows, 16 look directions, deterministic assembly, QA artifacts, and spriteVersionNumber 2 packaging.
---

# Hatch Pet

## Overview

Create a Codex-compatible v2 animated pet from a concept, brand cue, company/prospect name, one or more reference images, or any combination of those inputs. Every newly hatched pet is an 8x11 atlas with the 9 standard animation rows plus 16 clockwise look directions and is packaged with `spriteVersionNumber: 2`. The intermediate 8x9 atlas exists only to assemble and review rows 0-8; never package it as a new pet.

User-facing inputs are optional. If the user omits a pet name, infer one from the concept, brand, company, or reference filenames; if that is not possible, choose a short friendly name. If the user omits a description, infer one from the concept or references. If the user omits reference images, generate the base pet from text first, then use that base as the canonical reference for every animation row.

## Existing Inputs And Upgrades

Treat character art, generated images, standard or v2 atlases, contact sheets, and built-in pet art as first-class grounding inputs.

- Preserve user-provided art as a generation reference; do not assume it already has final cell geometry.
- For an existing valid 8x9 atlas, use it as the rows `0-8` intermediate after deterministic and visual validation, then generate rows `9-10` and package the result as v2.
- For an existing 8x11 atlas, preserve approved standard rows. If a look cell fails, correct the complete containing 8-frame row before deterministic reassembly. Never package a newly generated one-off repair cell beside cells from another generation.
- For a built-in pet, extract and use its atlas or neutral/idle cell as the canonical identity reference.
- Include every image that defines head shape, face, palette, markings, material, flame/ears/hair, props, or look mechanics in look-direction generation.
- When a renderer or source provides a dedicated neutral/front frame, pass it through `--neutral-cell`; otherwise use the approved idle/default frame. The 16 directional cells never treat `000` as neutral.

## Generation Delegation

Use `$imagegen` for all normal visual generation.

Before generating base art, row strips, or repair rows, load and follow the installed image generation skill:

```text
${CODEX_HOME:-$HOME/.codex}/skills/.system/imagegen/SKILL.md
```

Do not call the Image API, image CLI, or any other image-generation path directly. Let `$imagegen` choose its own built-in-first path and fallback rules. If `$imagegen` says a fallback requires confirmation, ask the user before continuing.

When invoking `$imagegen`, pass the generated pet prompt as the authoritative visual spec. Pet prompts should stay concise, state-specific, sprite-production oriented, and grounded in the listed input images. Keep longer policy and QA rules in this skill and the deterministic review scripts rather than expanding them into every image prompt. Do not wrap prompts in the generic `$imagegen` shared prompt schema.

Use this skill's scripts for deterministic image work only: preparing layout guides and prompts, mirroring approved `running-left`, extracting frames, validating rows, composing the final atlas, and creating contact-sheet plus motion-preview QA media. Parent-owned shell/`jq` steps handle manifest updates, packaging, and cleanup.

## Runtime Dependencies

Before running any bundled script, call `load_workspace_dependencies`. Set `PYTHON` to the exact Python executable path returned by that tool and use `"$PYTHON"` for every command below. The bundled runtime includes Pillow, which these scripts require. Do not use a bare system `python`; if workspace dependencies are unavailable, stop and report that the bundled runtime is required.

## Storage Controls

The built-in `$imagegen` path stores generated PNG bytes in the rollout that invokes it, even when it also writes a file under `${CODEX_HOME:-$HOME/.codex}/generated_images`. Deleting files later reduces filesystem use, but it does not shrink an already-written rollout. Keep image generation isolated and bounded:

- Use one lightweight generation worker per visual job. Do not batch multiple base/row jobs into the same worker.
- Workers must return only `selected_source=...` and `qa_note=...`; they must not include Markdown image previews, base64, or extra visual attachments in their final response.
- The parent must not open every generated PNG visually. Use worker QA for each job and inspect only the final contact sheet.
- After copying the selected generated output into `decoded/`, remove the selected original from `${CODEX_HOME:-$HOME/.codex}/generated_images` when it lives there, then remove its now-empty generation directory if possible.
- For storage-sensitive full runs, ask the user whether to use the `$imagegen` CLI fallback when available. That path requires local API credentials and explicit user confirmation, but it can avoid built-in image payloads being embedded in rollout events.

## Brand Discovery

If the user provides a brand, company, product, or prospect name rather than a concrete avatar description or reference image, run a lightweight discovery subagent before preparing the pet run. The discovery worker must use web search and prefer official sources such as the brand site, product pages, docs, about pages, press pages, or brand pages. Use reputable secondary sources only when official pages are too thin. Keep the search narrow: enough to extract visual and personality cues, not a market-research brief.

Skip discovery when the user already provides a concrete mascot/avatar description or reference images, unless the user explicitly asks for brand research.

Discovery worker responsibilities:

- search the web for 2-4 relevant sources, preferring official pages
- write an adaptive markdown brief rather than a rigid field dump
- cover identity/category, audience/use context, visual system, personality/tone, product/domain motifs, mascot translation cues, avoidances, and evidence/confidence
- mark mascot guidance that is inferred from sources as inference
- avoid copying logos, readable marks, UI screenshots, slogans, or text
- end with a compact `Generation handoff` section containing only `brand_name`, `brand_brief`, `avatar_seed`, `avoid`, and `brand_sources`
- do not generate images, prepare run folders, or edit unrelated files

Use this discovery worker prompt:

```text
Research a brand for hatch-pet mascot creation.

Brand/product/prospect: <brand name>
User context: <short user request>
Output file: <absolute path to brand-discovery.md>

Use web search. Prefer official brand, product, docs, about, press, or brand pages. Use reputable secondary sources only if official sources are too thin. Write an adaptive markdown brief to the output file. Headings may flex by brand, but the brief must cover:
- identity/category: canonical name, product type, what it does
- audience/use context: who it serves and where it appears
- visual system: palette, shapes, line quality, materials, typography feel, iconography, patterns
- personality/tone: emotional traits, energy, formality, playfulness
- product/domain motifs: objects, workflows, verbs, metaphors, environments
- mascot translation cues: candidate forms, signature traits, props, what must read at pet size
- avoidances: logos/text, trademark-sensitive elements, misleading cues, competitor confusion, poor mascot fits
- evidence/confidence: source URLs plus notes where evidence is weak or inferred

Do not copy logos, readable marks, UI screenshots, slogans, or text. Clearly label mascot guidance that is inferred rather than directly sourced.

End the brief with a `Generation handoff` section containing exactly:
- brand_name=<canonical brand/product name>
- brand_brief=<one sentence, max 45 words, covering palette/tone/domain motifs/personality>
- avatar_seed=<short mascot-safe visual idea, no logo copying>
- avoid=<short comma-separated list>
- brand_sources=<comma-separated source URLs>

Return exactly:
brand_discovery_file=<absolute output file path>
brand_name=<canonical brand/product name>
brand_brief=<same compact sentence from Generation handoff>
avatar_seed=<same short seed from Generation handoff>
avoid=<same short avoid list from Generation handoff>
brand_sources=<same comma-separated URLs from Generation handoff>
```

The parent should save the markdown brief before preparing the run, then pass it to `prepare_pet_run.py` as `--brand-discovery-file` together with `--brand-name`, `--brand-brief`, repeated `--brand-source`, and a concise `--pet-notes` value based on `avatar_seed` when the user did not provide a better avatar description. Keep the full brief for review; only the compact handoff fields should shape prompts. If web search is unavailable and the user gave only a bare brand name, ask for brand cues before generating.

## Generation Contract

### Visual Job Graph

Expect up to 13 visual jobs: 1 base pet, 9 standard row strips, 1 required four-cardinal anchor strip, and 2 required coherent look-direction row strips. The standard states are `idle`, `running-right`, `running-left`, `waving`, `jumping`, `failed`, `waiting`, `running`, and `review`. The only deterministic visual derivation is `running-left`, which may be produced by mirroring `running-right` only after `running-right` has been generated, visually inspected, and explicitly approved as safe to mirror. If mirroring is not appropriate, generate `running-left` as a normal grounded `$imagegen` row.

### Look Direction Sequence

After validating rows 0–8, write qa/look-mechanics.md, then generate and approve one four-pose cardinal strip in this fixed order: 000 up, 090 screen-right, 180 down, and 270 screen-left. Generate row 9 as one coherent eight-pose family from those approved cardinal pose families, interpolating the intermediate directions as even 22.5-degree steps. Deterministically register its eight ordered pose groups, then run final-cell edge, semantic, and continuity QA immediately. Only after row 9 passes, generate row 10 as one coherent eight-pose family, using the approved cardinals for direction meaning and completed row 9 for identity, scale, registration, and boundary continuity. Run the same QA immediately after row 10. Row 9 contains 000, 022.5, 045, 067.5, 090, 112.5, 135, and 157.5; row 10 contains 180, 202.5, 225, 247.5, 270, 292.5, 315, and 337.5. 000 means up, not neutral/front. Never ask $imagegen to generate or repair a complete 8×11 atlas.

### Visual Provenance And Grounding

After selecting a visual output, the parent agent copies that exact image into the job's `decoded/` path, runs its required incremental checks, and only then marks the job complete in `imagegen-jobs.json`. Do not write helper scripts that populate row outputs. The deterministic Python scripts may only process already-generated visual outputs.

Only the base job may be prompt-only. Every row-strip job generated through `$imagegen` must use the input images listed in `imagegen-jobs.json`, including the canonical base reference created after the selected base output is copied. Treat any row generation without attached grounding images as invalid.

## Pet-Safe Styles

Default style is `auto`: infer the pet's style from the user's prompt and references, then preserve that style across every row. If the user names a style, honor it. Supported style presets include `pixel`, `plush`, `clay`, `sticker`, `flat-vector`, `3d-toy`, `painterly`, `brand-inspired`, and `auto`.

Any style is acceptable when it remains pet-safe:

- compact whole-body silhouette readable inside a `192x208` cell
- consistent face, proportions, material, palette, and props across all rows
- clean removable chroma-key background
- details large enough to read at pet size
- no text, labels, UI, or readable logos unless the user explicitly provides approved reference art and asks for them

Non-pixel styles are first-class. Plush, clay, sticker, vector, 3D toy, painterly mascot, ink, and brand-inspired looks should be accepted when they satisfy the atlas and readability constraints.

## Transparency And Effects

Pet rows are processed into transparent `192x208` cells, so every generated pixel must either belong to the pet sprite or be cleanly removable chroma-key background. Prefer pose, expression, and silhouette changes over decorative effects.

The deterministic raster pipeline owns the transparency and chroma-cleanup invariants. Its final edge-local spill-suppression step selects every translucent silhouette-boundary pixel plus opaque boundary pixels whose chroma points toward the known key, then extends clean interior RGB outward through that band in linear light. It preserves alpha exactly, clears hidden RGB under fully transparent pixels, and reports the algorithm and parameters used. The cleanup report plus atlas validator are authoritative for chroma contamination. Once the final report has `ok: true` and atlas validation passes, do not regenerate imagery or add another chroma-cleanup pass.

Fully transparent pixels are allowed outside the sprite silhouette, in unused cells, and in intentional negative-space openings that are part of the pet's design, such as loops or holes in a ribbon body. Reject any generated or repaired cell with accidental 100%-transparent holes inside a filled body, including horizontal bands, seam rows, scanline-like gaps, sliced-tile boundaries, or "see-through" interior stripes. Inspect suspect cells on a high-contrast background or alpha mask before accepting them; ordinary atlas validation is not enough when the hole is inside the silhouette.

Allowed effects must satisfy all of these conditions:

- The effect is state-relevant and helps explain the animation.
- The effect is physically attached to, touching, or overlapping the pet silhouette, not floating nearby.
- The effect is inside the same frame slot as the pet and does not create a separate sprite component.
- The effect is opaque, hard-edged enough for clean extraction, and uses non-chroma-key colors.
- The effect is small enough to remain readable at `192x208` without clutter.

Avoid these by default because they usually break transparent-background cleanup or component extraction:

- wave marks, motion arcs, speed lines, action streaks, afterimages, blur, or smears
- detached stars, loose sparkles, floating punctuation, floating icons, falling tear drops, separated smoke clouds, or loose dust
- cast shadows, contact shadows, drop shadows, oval floor shadows, floor patches, landing marks, impact bursts, glow, halo, aura, or soft transparent effects
- text, labels, frame numbers, visible grids, guide marks, speech bubbles, thought bubbles, UI panels, code snippets, checkerboard transparency, white backgrounds, black backgrounds, or scenery
- chroma-key-adjacent colors in the pet, prop, effects, highlights, or shadows
- stray pixels, disconnected outline bits, speckle/noise, cropped body parts, overlapping poses, or any pose that crosses into a neighboring frame slot

State-specific guidance:

- `idle`: keep this calm and low-distraction. Use only subtle breathing, a tiny blink, a slight head or body bob, a very small material sway, or another quiet persona-preserving motion. The loop must still contain visible micro-variation; do not accept six effectively identical copies. Do not show waving, walking, running, jumping, talking, working, reviewing, emotional reactions, large gestures, item interactions, or new props.
- `waving`: show the wave through paw, hand, wing, or limb pose only. Do not draw wave marks, motion arcs, lines, sparkles, symbols, or floating effects around the gesture.
- `jumping`: show vertical motion through body position only. Do not draw shadows, dust, landing marks, impact bursts, bounce pads, or floor cues.
- `failed`: tears, attached smoke puffs, or attached stars are allowed if they obey the allowed-effects rules; do not use red X marks, floating symbols, detached smoke, detached stars, or separate tear droplets.
- `waiting`: show that Codex needs approval, help, or user input through an expectant asking pose. Keep it distinct from ordinary idle and review.
- `running`: show active task work, processing, thinking, scanning, typing, or focused effort. Do not show literal foot-running, jogging, sprinting, treadmill motion, raised knees, long steps, pumping arms, directional travel, speed lines, dust clouds, floor shadows, motion trails, or detached motion effects.
- `review`: show focus through lean, blink, eyes, head tilt, or paw/hand position. Do not add magnifying glasses, papers, code, UI, punctuation, symbols, or other new props unless they already exist in the base pet identity.
- `running-right` and `running-left`: show directional drag movement through body, limb, and prop movement only. `running-right` must face and travel right; `running-left` must face and travel left. Their cadence must visibly alternate across the loop rather than repeating one nearly static stride. Do not draw speed lines, dust clouds, floor shadows, motion trails, or detached motion effects.

## Visible Progress Plan

For every pet run, keep a visible checklist so the user can see where the work is up to. Create the checklist before starting, keep one step active at a time, and update it as each step finishes.

Use this checklist for every v2 pet run, replacing `<Pet>` with the pet's name or `your pet`:

1. Getting `<Pet>` ready.
2. Imagining `<Pet>`'s main look.
3. Picturing `<Pet>`'s poses.
4. Hatching `<Pet>`.

What each step means:

- `Getting <Pet> ready.` Choose or confirm the pet name, description, source images, style preset, style notes, and working folder. For bare brand/product/company requests, first run the brand discovery worker and capture the compact brand brief, source URLs, and avatar seed.
- `Imagining <Pet>'s main look.` Generate the pet's main reference image. This becomes the visual source of truth.
- `Picturing <Pet>'s poses.` Generate and approve rows `0-8`, write the pet-specific look mechanics plan, then generate rows `9-10`. Only mirror `running-left` if `running-right` clearly works when flipped.
- `Hatching <Pet>.` Assemble the 8x11 atlas, review standard motion plus all 16 look directions, fix every failed cell or row, package `spriteVersionNumber: 2`, and report the output paths.

Only mark a step complete when the real file, image, or decision exists. If this is a repair run, start from the first relevant step instead of restarting the whole checklist.

## Time Budget And Convergence

Aim to complete a normal pet run within 30 minutes while preserving every mandatory acceptance criterion. Treat this as a planning target and an incentive to maximize validated progress per minute, not as permission to weaken QA or package a failing pet.

At the start of the run, allocate an approximate budget:

- preparation: 2 minutes
- base image: 3 minutes
- standard rows: 10 minutes
- look directions: 8 minutes
- final QA and packaging: 5 minutes
- buffer: 2 minutes

Run independent generation jobs concurrently up to the worker limit, start deterministic checks as soon as each dependency is ready, and record actual stage plus repair time. Prefer character and prop constructions that naturally satisfy cell geometry, transparency, component connectivity, and direction semantics; identify likely conflicts such as open interior gaps, detached parts, thin connectors, asymmetric props, or ambiguous faces before row generation.

After every failed attempt:

1. Classify the failure as visual semantics, identity, source-edge geometry, component connectivity, extraction, chroma, continuity, or final visual QA.
2. State the concrete evidence and the root condition the next action will change.
3. Use a deterministic correction for deterministic failures before regenerating imagery.
4. Regenerate only when the source visual is genuinely wrong, and preserve every property that already passed.
5. Compare the new result with the previous one. A repair counts as progress only when it reduces the number or severity of failures without breaking a previously passing gate.

If the same root failure recurs twice, stop varying the prompt and change strategy: strengthen the cardinal pose families or row-level direction instructions, simplify the pose or prop construction, change the deterministic extraction method, or redesign the problematic visual feature. If a repair merely moves a failure to another cell or gate, treat that as a cycle and change strategy immediately.

Use elapsed-time checkpoints:

- At 15 minutes, verify the run is on pace and that the remaining dependency path is bounded.
- At 25 minutes, prioritize the shortest quality-preserving path through remaining blockers and avoid optional polish.
- At 30 minutes, continue only when the remaining work is clearly converging and bounded, such as final validation, one targeted repair, or packaging.
- Keep recording elapsed time, retries, validation failures, and QA cost throughout the run, but do not pause or stop solely because elapsed time crosses 45 or 60 minutes. Continue until the pet passes, the user cancels, or a genuine external blocker prevents further progress.

Never use the time target to skip blind direction QA, labeled semantics, continuity review, atlas validation, despill validation, final visual QA, or any other acceptance criterion.

## Default Workflow

1. Prepare a pet run folder and imagegen job manifest:

```bash
SKILL_DIR="${CODEX_HOME:-$HOME/.codex}/skills/hatch-pet"
"$PYTHON" "$SKILL_DIR/scripts/prepare_pet_run.py" \
  --pet-name "<Name>" \
  --description "<one sentence>" \
  --reference /absolute/path/to/reference.png \
  --output-dir /absolute/path/to/run \
  --pet-notes "<stable pet description>" \
  --brand-discovery-file /absolute/path/to/brand-discovery.md \
  --brand-name "<optional researched brand name>" \
  --brand-brief "<optional compact researched brand cue sentence>" \
  --brand-source "https://example.com/source" \
  --style-preset auto \
  --style-notes "<optional freeform style notes>" \
  --force
```

All arguments above are optional except any flags needed to express user constraints. For text-only requests, pass the concept through `--pet-notes` and omit `--reference`; `prepare_pet_run.py` will infer a name, description, chroma key, and output directory as needed.
For brand-only requests, run the discovery worker first, save the markdown brief, then pass the brief path through `--brand-discovery-file`, `avatar_seed` through `--pet-notes`, `brand_name` through `--brand-name`, `brand_brief` through `--brand-brief`, and each source URL through repeated `--brand-source`.

2. Inspect `imagegen-jobs.json` for the next ready `$imagegen` jobs. A job is ready when its `status` is not `complete` and every id in `depends_on` is already complete. Prefer reading the manifest directly with `jq` or the editor instead of adding helper scripts for status display:

```bash
jq '.jobs[] | {id, kind, status, depends_on, prompt_file, retry_prompt_file, input_images, output_path, derivation_policy}' /absolute/path/to/run/imagegen-jobs.json
```

3. Generate visual jobs with lightweight workers by default:

- Generate and copy `base` first, using a lightweight base worker.
- Generate and copy `idle` and `running-right` next as the identity and gait check, using one lightweight worker per row.
- Inspect `running-right`; mirror `running-left` only when visual identity, prop placement, markings, lighting, and direction semantics remain correct.
- Generate `running-left` normally with a lightweight worker when mirroring would change meaning or identity.
- Generate the remaining rows with lightweight workers, using every input image listed for each job.
- After standard-row QA, generate `look-cardinals` as one four-pose strip, extract it into `decoded/look-anchors/000.png`, `090.png`, `180.png`, and `270.png`, and approve all four. The `090` and `270` anchors must be unmistakable in viewer/screen coordinates and visibly oppose each other.
- Generate look row 9 as one coherent eight-pose synthesis from the approved cardinal strip, interpolating each intermediate direction as an even step between the adjacent cardinal pose families. Deterministically recover the eight ordered pose groups, crop them, normalize them with one shared scale and baseline, and then run final-cell edge diagnostics plus labeled per-direction QA immediately, before row 10 or final atlas assembly.
- Only after row 9 passes, generate row 10 as one coherent synthesis using the approved cardinal strip and completed row 9.

Keep up to three generation workers active whenever three independent jobs are ready and worker capacity permits. Backfill an available slot immediately instead of waiting for a fixed wave to finish. Use two or one worker when the dependency graph exposes fewer ready jobs. Do not exceed three generation workers without explicit user direction.

For each ready visual job, invoke `$imagegen` with the prompt file listed in `imagegen-jobs.json`, every listed input image with its role label, and the default built-in `image_gen` path unless `$imagegen` itself routes otherwise. The parent agent must keep its own image handling minimal: do not open every generated base or row in the parent rollout. Workers return only the selected source path and a one-sentence QA note; the parent records the selected source path in the manifest.

`prepare_pet_run.py` creates matching layout guides under `references/layout-guides/` for the nine standard rows, two look rows, and four-cardinal strip, and both look rows. Visual jobs attach the matching guide as a layout-only input so the model can follow the correct frame count, spacing, centering, and safe padding. Treat these guides as invisible construction references: generated strips must not include visible boxes, borders, center marks, labels, guide colors, or the guide background.

When generating row strips, keep the identity lock in the row prompt authoritative. Preserve the same style, face, markings, palette, materials, prop design, body proportions, and silhouette from the canonical base. Row jobs attach the layout guide and canonical base by default; the decoded base is kept in the run folder for deterministic processing rather than sent as a redundant generation input.

If `$imagegen` returns a transport-level `Bad Request` for a row, retry that same row once with its generated `retry_prompt_file`. The retry prompt preserves the row id, frame count, chroma key, canonical-base identity, and state action. Keep the canonical base attached. If the retry still fails, stop and report the failing row and prompt paths instead of switching to any other generation path.

4. After selecting a generated output for a job, copy it into the decoded output path. For `base`, also create the canonical identity reference:

```bash
RUN_DIR=/absolute/path/to/run
JOB_ID=<job-id>
SOURCE=/absolute/path/to/generated-output.png
OUTPUT_REL=$(jq -r --arg id "$JOB_ID" '.jobs[] | select(.id == $id) | .output_path' "$RUN_DIR/imagegen-jobs.json")
mkdir -p "$(dirname "$RUN_DIR/$OUTPUT_REL")"
cp "$SOURCE" "$RUN_DIR/$OUTPUT_REL"
```

```bash
if [ "$JOB_ID" = "base" ]; then mkdir -p "$RUN_DIR/references"; cp "$RUN_DIR/$OUTPUT_REL" "$RUN_DIR/references/canonical-base.png"; fi
```

For every standard `row-strip` job, immediately extract and inspect only that row before marking the job complete. This overlaps deterministic QA and any repair with generation of other ready rows instead of waiting for all nine rows:

```bash
ROW_QA_DIR="$RUN_DIR/qa/rows/$JOB_ID"
"$PYTHON" "$SKILL_DIR/scripts/extract_strip_frames.py" \
  --decoded-dir "$RUN_DIR/decoded" \
  --output-dir "$ROW_QA_DIR/frames" \
  --states "$JOB_ID" \
  --method auto
"$PYTHON" "$SKILL_DIR/scripts/inspect_frames.py" \
  --frames-root "$ROW_QA_DIR/frames" \
  --json-out "$ROW_QA_DIR/review.json" \
  --states "$JOB_ID" \
  --require-components
```

Treat errors as an immediate repair request. Inspect warnings before accepting the row; do not defer a known clipping, component, or extraction problem to final atlas QA. Chroma cleanup belongs to the deterministic post-assembly despill pass and must not trigger row regeneration. If the only failure is component extraction and the source strip itself has stable scale and placement, use the existing `stable-slots` correction with `--allow-stable-slots` instead of regenerating imagery.

For `look-cardinals`, extract and validate all four anchors before marking the job complete:

```bash
CHROMA_KEY=$(jq -r '.chroma_key.hex' "$RUN_DIR/pet_request.json")
"$PYTHON" "$SKILL_DIR/scripts/extract_cardinal_anchors.py" \
  --strip "$RUN_DIR/decoded/look-cardinals.png" \
  --output-dir "$RUN_DIR/decoded/look-anchors" \
  --chroma-key "$CHROMA_KEY" \
  --json-out "$RUN_DIR/qa/cardinal-anchors.json"
"$PYTHON" "$SKILL_DIR/scripts/compose_cardinal_anchor_strip.py" \
  --anchors-dir "$RUN_DIR/decoded/look-anchors" \
  --output "$RUN_DIR/decoded/look-anchors-approved.png"
```

Approve the four extracted anchors semantically at final pet size. If one cardinal fails, regenerate that individual anchor with `prompts/look-anchor-repairs/<degree>.md`, replace only its extracted file, and rerun `compose_cardinal_anchor_strip.py`. Both final look rows use the approved cardinal strip, and row 10 additionally uses completed row 9. Mark the job complete only after its required deterministic and visual checks pass:

```bash
UPDATED_AT=$(date -u +%Y-%m-%dT%H:%M:%SZ)
TMP_MANIFEST=$(mktemp)
jq --arg id "$JOB_ID" --arg source "$SOURCE" --arg at "$UPDATED_AT" '(.jobs[] | select(.id == $id)) += {status: "complete", source_path: $source, completed_at: $at}' "$RUN_DIR/imagegen-jobs.json" > "$TMP_MANIFEST"
mv "$TMP_MANIFEST" "$RUN_DIR/imagegen-jobs.json"
```

After `decoded/look-anchors-approved.png` exists and all four cardinals have passed semantic review, mark `look-cardinals` complete. Row 9 then becomes ready immediately.

If the copied source is under `${CODEX_HOME:-$HOME/.codex}/generated_images`, delete the original generated file after the decoded copy exists:

```bash
GENERATED_ROOT="${CODEX_HOME:-$HOME/.codex}/generated_images"
case "$SOURCE" in
  "$GENERATED_ROOT"/*)
    rm -f "$SOURCE"
    rmdir "$(dirname "$SOURCE")" 2>/dev/null || true
    ;;
esac
```

5. Derive `running-left` only when it is visually safe:

```bash
"$PYTHON" "$SKILL_DIR/scripts/derive_running_left_from_running_right.py" \
  --run-dir /absolute/path/to/run \
  --confirm-appropriate-mirror \
  --decision-note "<why mirroring preserves this pet's identity>"
```

That script mirrors each generated frame slot in place so the leftward row preserves the rightward row's temporal order. Do not replace it with a whole-strip mirror that reverses animation timing.

6. When all nine incrementally validated standard row jobs are complete, build and review the intermediate rows `0-8`:

```bash
RUN_DIR=/absolute/path/to/run
mkdir -p "$RUN_DIR/final" "$RUN_DIR/qa"
```

```bash
"$PYTHON" "$SKILL_DIR/scripts/extract_strip_frames.py" \
  --decoded-dir "$RUN_DIR/decoded" \
  --output-dir "$RUN_DIR/frames" \
  --states all \
  --method auto
```

```bash
"$PYTHON" "$SKILL_DIR/scripts/inspect_frames.py" \
  --frames-root "$RUN_DIR/frames" \
  --json-out "$RUN_DIR/qa/review.json" \
  --require-components
```

```bash
"$PYTHON" "$SKILL_DIR/scripts/compose_atlas.py" \
  --frames-root "$RUN_DIR/frames" \
  --output "$RUN_DIR/final/spritesheet.png" \
  --webp-output "$RUN_DIR/final/spritesheet.webp"
```

```bash
"$PYTHON" "$SKILL_DIR/scripts/make_contact_sheet.py" \
  "$RUN_DIR/final/spritesheet.webp" \
  --output "$RUN_DIR/qa/contact-sheet.png"
```

```bash
"$PYTHON" "$SKILL_DIR/scripts/render_animation_previews.py" \
  --frames-root "$RUN_DIR/frames" \
  --output-dir "$RUN_DIR/qa/previews"
```

If the preview GIFs show size popping or baseline jumps caused by per-frame fit-to-cell extraction, and the original row strip itself had stable scale and placement, rerun frame extraction with the explicit row-stability mode and then re-run inspection, atlas composition, contact sheet generation, and previews:

```bash
"$PYTHON" "$SKILL_DIR/scripts/extract_strip_frames.py" \
  --decoded-dir "$RUN_DIR/decoded" \
  --output-dir "$RUN_DIR/frames" \
  --states all \
  --method stable-slots
```

```bash
"$PYTHON" "$SKILL_DIR/scripts/inspect_frames.py" \
  --frames-root "$RUN_DIR/frames" \
  --json-out "$RUN_DIR/qa/review.json" \
  --require-components \
  --allow-stable-slots
```

Use `stable-slots` as a deliberate QA-driven correction, not the default. It should reduce extraction-induced motion pops without hiding clipped wide poses or bad source strips.

Expected intermediate output before the required v2 look stage:

```text
run/
  pet_request.json
  imagegen-jobs.json
  prompts/
  decoded/
  frames/frames-manifest.json
  final/spritesheet.webp
  qa/contact-sheet.png
  qa/previews/*.gif
  qa/review.json
```

Inspect `qa/contact-sheet.png` and `qa/previews/*.gif` before generating look rows. `qa/review.json` plus visual motion review are the intermediate gates. The standard contact sheet intentionally predates chroma cleanup, so visible key-color fringe there is not a failure; judge chroma only on the cleaned final v2 atlas. Block progress if any standard row changes identity, style, prop handedness, or silhouette, or if playback pops, reverses cadence, faces the wrong direction, or is visually inert. Do not package or clean up yet.

## Required V2 Look-Direction Stage

Every new pet must complete this stage. After standard-row QA passes, write `qa/look-mechanics.md`, approve the four cardinals, synthesize and validate the complete `look-row-9`, then synthesize `look-row-10`. Row 10 becomes ready only after row 9 is deterministically registered, clears post-registration edge checks, and has no semantic or continuity hard failure; reviewed warnings may remain. It uses row 9 plus the approved cardinal strip as continuity evidence.

Before either look row, run the prepared `look-cardinals` strip job, extract its four cells with `extract_cardinal_anchors.py`, and approve them. Do not let a two-row sweep invent its own left/right basis. `090` must point toward the viewer's screen-right edge and `270` toward the viewer's screen-left edge; for faces, the nose tip and pupils must cross to the corresponding side of the head center. If one cardinal is ambiguous, regenerate only that anchor before continuing.

After copying row 9 into `decoded/look-row-9.png`, register and edge-check it with the same transform used by final assembly:

```bash
"$PYTHON" "$SKILL_DIR/scripts/assemble_extended_atlas.py" \
  --base-atlas "$RUN_DIR/final/spritesheet.webp" \
  --look-row-9 "$RUN_DIR/decoded/look-row-9.png" \
  --neutral-cell "$RUN_DIR/frames/idle/00.png" \
  --chroma-key "$CHROMA_KEY" \
  --chroma-threshold 96 \
  --registered-row-output "$RUN_DIR/qa/look-row-9-registered.png" \
  --registration-manifest-output "$RUN_DIR/qa/look-row-9-registration.json"
```

Inspect the eight registered cells at normal pet size in `000` through `157.5` order. Record the row-9 semantic and adjacent-continuity review, resynthesize the complete row for any hard failure, and mark `look-row-9` complete only after this check passes. That completion makes row 10 ready in `imagegen-jobs.json`.

Generate only the additional look-direction visuals with `$imagegen`:

- Required for new pets: two coherently synthesized 8-frame row strips, one for row 9 and one for row 10.
- Always include the canonical base reference and approved 8x9 contact sheet.
- Keep the body scale, baseline, head size, face, materials, palette, markings, and props consistent with the standard atlas.
- Before prompting, write a short look mechanics decision for this specific pet. First ask: **what is the best natural motion for this character when looking around?** Describe what stays anchored, what leads the gaze, what follows, and what bends, shifts, turns, squashes, stretches, or deforms. Include eyes and props: decide whether eyes rotate as physical eyeballs, irises move on a fixed surface, eyelids reshape, pupils slide, props stay stable, props lag slightly, or props move with the body. Use the character's physical construction as the guide: flexible wire should bend, soft bodies should deform, separate heads should turn, ears/fur/antennae may follow through, physical eyeballs should rotate as whole eye globes in their sockets, flat screen or sticker eyes may change their drawn features on a fixed surface, and rigid or screen-like characters may stay body-locked while facial features move.
- Define a motion budget before generation: each 22.5-degree step should move the same parts by roughly the same visual amount, with no single adjacent pair doing a larger bend, scale change, prop shift, or silhouette change unless the mechanics decision explicitly calls out that asymmetry. Generate row 9 first along `000 -> 090 -> 180`, then give completed row 9 to row 10 so `180` begins exactly one step after `157.5`. Row 10 follows `180 -> 270 -> 000`, and `337.5` in row 10 must land one step before the approved `000` in row 9.
- Do not use whole-sprite rotation, whole-cell rotation, skewing, or affine tilting to fake gaze direction. A direction row built by rotating the entire pet is failed unless the pet is literally a rotating rigid object and the look mechanics decision explicitly says the whole object should rotate. Whole-body tilt that makes the item/background appear to rock left or right is not natural look behavior for ordinary pets.
- Generate a coherent 16-pose gaze set, not 16 unrelated variants. Each direction should feel like a point on one continuous arc around the clock.
- The look mechanics decision must name the natural pose family for each cardinal direction before generation, including which body side becomes more visible, which features become occluded, and how any held prop follows or lags. Do not let the generator infer all directions from one front-facing pose. For characters with a face or head, leftward directions must visibly turn or bend the face/head left, rightward directions must visibly turn or bend right, up/down directions must use the eyes, eyelids, head angle, neck, and upper body as physically appropriate, and diagonals must interpolate between those pose families. A set where every cell remains essentially front-facing, or where all leftward cells still read as front/right-facing, is failed.
- Adjacent direction cells must have continuous body movement. Compare every neighboring pair in direction order, including `157.5 -> 180`, `337.5 -> 000`, and any row-strip boundary. Anchored parts must not jump, flip sides, or teleport between adjacent states; if a body part moves laterally, bends, stretches, or rotates, its position should progress gradually across the intervening directions.
- Do not mirror, re-center, or independently regenerate adjacent direction cells in a way that changes the pet's body registration. Keep a stable anchor, usually the feet/base/torso/lower body or the natural grounded part of the character, and let only the intended look mechanics change around it.
- Every look cell must be visually distinguishable from the neutral/resting frame at final pet size. A direction cell that reads as front-facing, idle, or neutral is failed even when it is non-empty, transparent, and in the correct row/column.
- Cardinal directions must be semantically unmistakable at final pet size, not only numerically or geometrically different. `000` must clearly read as looking up, `090` as looking right, `180` as looking down, and `270` as looking left using the pet's natural mechanism. If the pet has no pupils or physical eyeballs, the head, face surface, eyelids, antennae, ears, or body bend must carry the direction clearly enough that a viewer can identify the cardinal without labels.
- Diagonal and intermediate directions should broadly occupy the intended quadrant and advance naturally through the ordered loop. Minor pupil, nose, eyelid, or feature-placement deviations are not failures by themselves. Reject only gross wrong-quadrant poses, visible reversals, or intermediate cells that break the coherent motion family.
- For eyeless object pets, do not default to literal whole-object rotation just because the object is rigid. First identify whether the object has a natural front, display face, playable surface, readable silhouette, or iconic viewing angle. Preserve that primary readable face unless the user explicitly asks for turntable rotation. Express look direction through subtle object-specific body language: small lean, neck/tip aim, hinge, yaw, pitch, bend, vibration, squash, follow-through, or attached-part motion. The direction should read as attention or orientation, not as the object spinning through all clock angles.
- Preserve the pet's original eye design in look-direction cells. Do not paint new round "googly" eyes, replacement eye whites, floating pupils, detached eye dots, or a second eye layer on top of the source eyes. Eye motion must follow the look mechanics decision. If the pet has physical eyeballs, rotate or redraw the whole eyeball surface so the sclera/eye white, iris, pupil, eyelids, rim, and highlights change together as one physical eye; do not slide only the iris or pupil across a fixed eye white. If the pet has flat printed, sticker, or screen eyes, keep the surface fixed and move/redraw only the features that would physically change on that surface. Do not use procedural pupil/iris compositing unless it is clipped to the original eye aperture and visibly remains inside the head silhouette in every direction. If the original eye design cannot be preserved cleanly, regenerate the whole look cell with the original eye construction instead of compositing new eyes over it.
- Eyes may lead the gaze, but pupil-only motion is an exception, not the default. Use it only when the look mechanics decision explains why whole-eye rotation, eyelid reshaping, body, head, or feature movement would be unnatural for that specific design. Large-eye pets, cyclops pets, and round rigid-body pets with physical eyeballs usually should rotate the whole eye globes, not use pupil-only or googly-eye sliding. Screen-face pets and printed-eye pets may be body-locked with feature motion only. Separate head/body pets should usually combine eye movement with head turn, head tilt, ear/fur/upper-body follow-through, and a stable torso. Rigid object mascots may hinge, flex, slide, or shift attached features without rotating the whole sprite. Flexible wire or paperclip-like mascots should usually keep the feet/base anchored while the upper loop or face area bends toward the target and held props remain stable or lag subtly. Blob or organic pets should usually keep a base anchored while the face/head area stretches subtly toward the target. Other pet types should get their own similarly grounded mechanics.
- Human or humanoid pets need persona-preserving look mechanics. Do not use broad non-rigid raster warps that stretch the skull, brows, mouth, hoodie, hands, or held props just to make a direction read. The eyes should usually lead the gaze with visible eye, eyelid, and eyebrow participation, then the head/neck and upper body should follow subtly; a humanoid row where the head moves but the eyes stay locked in one expression is failed unless the mechanics decision gives a specific physical reason. Use small eye rotation, eyelid/eyebrow changes, head/neck turn, and restrained upper-body follow-through while preserving facial proportions and expression. Programmatic repairs must move anatomical parts with rigid or near-rigid part motion, not displacement fields that change facial feature spacing. For pets with held, worn, or attached props, infer each prop's physical constraints before generating look directions: where it is anchored, whether it is rigid or flexible, whether it leads or lags the body, and how it should occlude or be occluded as the character turns. Props near the face may become more side-on, partly hidden by the head, or reveal different contact points; hand-held tools may swing or lag subtly while staying attached; worn props should follow the body; flexible cords or straps should arc continuously. Do not keep the prop and character in the same front-facing relationship across all look directions. Before packaging a humanoid pet, inspect the normal-size neutral and cardinal cells together and reject identity or facial-proportion drift, or a `270` cardinal that does not unmistakably read as left.
- For every pet, use cardinal anchors instead of trusting a two-row sweep to preserve left/right semantics. Generate `000`, `090`, `180`, and `270` together as one strip, then extract and approve them. The final look rows use those four pose families for direction meaning and interpolate the intermediate directions as a coherent arc. Define directions in viewer/screen coordinates, never character-relative coordinates. Do not require exact pupil or nose placement on intermediate poses; use the ordered loop and overall quadrant motion as the primary evidence.
- Keep motion subtle and pet-safe: preserve volume, baseline, silhouette readability, identity, and material believability. The look pose may involve head, eyes, face, upper body, appendages, or body deformation only when those parts would naturally participate.
- Do not add labels, degree text, arrows, clocks, guide marks, shadows, glows, scenery, or detached effects.

Direction order is fixed:

```text
row 9:  000, 022.5, 045, 067.5, 090, 112.5, 135, 157.5
row 10: 180, 202.5, 225, 247.5, 270, 292.5, 315, 337.5
```

`000` means looking up / 12 o'clock. Neutral/front is the pointer deadzone and should fall back to idle unless the target renderer explicitly uses a neutral cell.

### Direction Acceptance Policy

Judge the completed 16-pose loop as an animation family. Cardinals must match their single axis exactly. Intermediate directions should preserve the intended axes, but isolated blind-review uncertainty is evidence for labeled loop review rather than an automatic regeneration trigger.

Hard failures require row regeneration:

- a cardinal anchor is wrong or ambiguous: `000` up, `090` screen-right, `180` down, or `270` screen-left
- a blind cardinal classification contradicts or cannot confirm `000` up, `090` screen-right, `180` down, or `270` screen-left
- labeled normal-size review confirms that an intermediate pose points into the wrong principal quadrant, reverses the loop, or loses a required axis badly enough to read as a different direction
- the ordered loop visibly reverses, backtracks, crosses into the wrong principal quadrant, or contains a conspicuous snap, identity change, scale pop, registration jump, or broken prop attachment
- the source or atlas has a deterministic structural failure, or visual review confirms clipping, an accidental transparent interior hole, a seam band, replacement eyes, or a materially broken sprite
- whole-sprite rotation, deformation, or eye mechanics visibly break the pet's identity or make the motion feel incoherent

Review warnings do not require regeneration by themselves:

- an intermediate pose is similar to a neighbor, a diagonal cue is subtle, or the pet uses less body movement than the ideal mechanics plan
- blind reviewers disagree, return `ambiguous`, or produce an opposite-sign majority for an intermediate direction, provided labeled normal-size review confirms the intended direction and the ordered loop remains coherent
- continuity metrics report a diff, center, area, or alpha-hole candidate without a visible snap, pop, seam, or broken silhouette in the QA sheet or animation loop

Before accepting the v2 atlas, create a focused direction QA sheet showing the neutral/rest frame next to all 16 look cells, labeled by degree and expected direction, at approximately the in-app display size. Run the adjacent continuity measurement separately and treat its findings as motion-review evidence, not automatic direction failures.

Perform an explicit semantic review for every direction and record `pass`, `warning`, or `fail`, plus separate visible evidence for its horizontal and vertical axes. A warning may accept blind-review uncertainty for an intermediate pose when labeled normal-size review confirms the intended axes and the ordered loop remains coherent. It may not waive a wrong or ambiguous cardinal, a labeled wrong-quadrant pose, or a visible reversal. If a direction receives `fail`, strengthen the containing row's instructions and resynthesize that complete coherent row. Never replace the final normalized cell directly.

Look rows must have transparent backgrounds after assembly. Do not accept or install the pet if `qa/look-directions.png` or `qa/contact-sheet-extended.png` shows chroma-key panels behind any look cell. If generated look rows contain slight chroma-key lighting variation, rerun assembly with a wider `--chroma-threshold` instead of packaging the opaque key color. Validation must pass without opaque chroma-key-pixel errors.

Extended look cells must also keep the same practical scale and body registration as the neutral/default pet. Do not accept a direction set where neutral/default is noticeably larger than the look cells, where the look cells appear to float above the baseline, or where the pet slides left/right within its 192x208 cell while only changing gaze. Extended assembly recovers each pose group from the complete original-resolution row and computes one shared scale from height plus every pose's left and right extents around the shared lower-body anchor, so asymmetric poses remain inside the final cell after alignment. It resizes each original crop exactly once and never enlarges an already-resampled cell. The neutral frame supplies the target body height, lower-body anchor, and baseline. Pass `--neutral-cell` when an external neutral frame is available; otherwise the assembler falls back to the populated neutral/default slot or first visible idle frame in the base atlas. If the focused QA sheet still shows scale or placement drift, repair before packaging.

Assemble the extended atlas from two generated row strips:

Use the run's selected chroma key for every assembly path; omitting it falls back to green and can misclassify a magenta background as clipped sprite pixels.

```bash
CHROMA_KEY=$(jq -r '.chroma_key.hex' "$RUN_DIR/pet_request.json")
```

Extended assembly reuses the approved registered row-9 cells and persisted scale exactly. It removes the chroma background from row 10, detects its eight separated pose groups, preserves their left-to-right order, crops each complete pose without fixed-slot slicing, and fits them against the same neutral-frame scale, lower-body anchor, and baseline. Only then does it apply the near-edge clipping check to row 10's normalized `192x208` cells. If pose-group recovery is ambiguous, or if row 10 cannot fit the approved row-9 transform without failing the post-registration edge check, resynthesize row 10; do not rescale row 9, patch an individual final cell, or relax the threshold for acceptance.

```bash
"$PYTHON" "$SKILL_DIR/scripts/assemble_extended_atlas.py" \
  --base-atlas "$RUN_DIR/final/spritesheet.webp" \
  --registered-row-9 "$RUN_DIR/qa/look-row-9-registered.png" \
  --row-9-registration "$RUN_DIR/qa/look-row-9-registration.json" \
  --look-row-10 "$RUN_DIR/decoded/look-row-10.png" \
  --neutral-cell "$RUN_DIR/frames/idle/00.png" \
  --chroma-key "$CHROMA_KEY" \
  --chroma-threshold 96 \
  --output "$RUN_DIR/final/spritesheet-extended.png" \
  --webp-output "$RUN_DIR/final/spritesheet-extended.webp" \
  --manifest-output "$RUN_DIR/final/spritesheet-extended.json"
```

For repair or upgrade of a user-provided 16-cell source that was already approved as one coherent set, individual-cell assembly remains available. Do not use this path for newly generated repair cells:

```bash
"$PYTHON" "$SKILL_DIR/scripts/assemble_extended_atlas.py" \
  --base-atlas "$RUN_DIR/final/spritesheet.webp" \
  --look-cells-dir /absolute/path/to/look-cells \
  --neutral-cell "$RUN_DIR/frames/idle/00.png" \
  --chroma-key "$CHROMA_KEY" \
  --chroma-threshold 96 \
  --output "$RUN_DIR/final/spritesheet-extended.png" \
  --webp-output "$RUN_DIR/final/spritesheet-extended.webp" \
  --manifest-output "$RUN_DIR/final/spritesheet-extended.json"
```

Run the single deterministic edge-local spill-suppression pass on the assembled v2 atlas, then validate and make a contact sheet:

```bash
"$PYTHON" "$SKILL_DIR/scripts/despill_chroma_edges.py" \
  "$RUN_DIR/final/spritesheet-extended.png" \
  --output "$RUN_DIR/final/spritesheet-extended.png" \
  --webp-output "$RUN_DIR/final/spritesheet-extended.webp" \
  --chroma-key "$CHROMA_KEY" \
  --json-out "$RUN_DIR/qa/chroma-despill-extended.json"
```

Treat `qa/chroma-despill-extended.json` as the authoritative chroma result. When it has `ok: true` and `validate_atlas.py --require-v2` passes, do not fail visual QA for perceived magenta fringe, regenerate any row, rerun despill, tune thresholds, or create an additional chroma-repair script. If either deterministic check fails, stop with a pipeline failure instead of retrying image generation.

This is the only chroma-cleanup invocation in the workflow. The intermediate 8×9 atlas is never despilled; rows `0-8` and the newly assembled look rows `9-10` are cleaned together exactly once in the completed 8×11 atlas.

```bash
"$PYTHON" "$SKILL_DIR/scripts/validate_atlas.py" \
  "$RUN_DIR/final/spritesheet-extended.webp" \
  --json-out "$RUN_DIR/final/validation-extended.json" \
  --chroma-key "$CHROMA_KEY" \
  --require-v2
```

```bash
"$PYTHON" "$SKILL_DIR/scripts/make_contact_sheet.py" \
  "$RUN_DIR/final/spritesheet-extended.webp" \
  --output "$RUN_DIR/qa/contact-sheet-extended.png"
```

Create the focused direction QA sheet:

```bash
"$PYTHON" "$SKILL_DIR/scripts/make_direction_qa_sheet.py" \
  "$RUN_DIR/final/spritesheet-extended.webp" \
  --output "$RUN_DIR/qa/look-directions.png"
```

Create the blind horizontal-and-vertical axis challenge and keep its answer key away from the visual QA worker:

```bash
"$PYTHON" "$SKILL_DIR/scripts/make_direction_blind_qa_sheet.py" \
  "$RUN_DIR/final/spritesheet-extended.webp" \
  --output "$RUN_DIR/qa/direction-blind-pairs.png" \
  --answer-key "$RUN_DIR/qa/direction-blind-answer-key.json"
```

Give three fresh isolated workers only `qa/direction-blind-pairs.png`. Each row states whether to classify the horizontal or vertical axis. Every worker must classify A and B as `screen-left`, `screen-right`, `up`, `down`, or `ambiguous` as appropriate, without seeing degree labels, expected directions, the labeled direction sheet, the answer key, or another worker's verdicts. Write their classifications separately, then combine them by strict per-cell majority:

```bash
"$PYTHON" "$SKILL_DIR/scripts/combine_direction_blind_verdicts.py" \
  --verdicts "$RUN_DIR/qa/direction-blind-verdicts-1.json" \
  --verdicts "$RUN_DIR/qa/direction-blind-verdicts-2.json" \
  --verdicts "$RUN_DIR/qa/direction-blind-verdicts-3.json" \
  --json-out "$RUN_DIR/qa/direction-blind-verdicts.json"
```

Apply the hidden answer key only to the consensus verdict:

```bash
"$PYTHON" "$SKILL_DIR/scripts/validate_direction_blind_verdicts.py" \
  --answer-key "$RUN_DIR/qa/direction-blind-answer-key.json" \
  --verdicts "$RUN_DIR/qa/direction-blind-verdicts.json" \
  --json-out "$RUN_DIR/qa/direction-blind-validation.json"
```

The hidden answer key contains seven horizontal pairs and seven vertical pairs. The cardinal pairs (`000` vs `180` and `090` vs `270`) are hard gates: a mismatch or ambiguous majority keeps validation at `ok: false`. All intermediate pairs are review gates: mismatches, same-direction votes, and ambiguous majorities are preserved as warnings while validation remains `ok: true`. The blind pass is mandatory, but intermediate warnings are resolved by labeled normal-size loop review instead of repeated regeneration by default.

### Blind Review Severity Resolution

After receiving a blind or final visual QA `pass`/`fail` result:

1. If it passes, continue immediately.
2. If it fails, inspect the worker's semantic reasons, repair note, labeled direction sheet, `qa/direction-semantics.json`, and `qa/look-continuity.json` before regenerating anything.
3. Classify the failure as `major` or `minor`:
   - `major`: wrong or ambiguous cardinal; labeled normal-size review confirms a wrong principal quadrant or visible reversal; conspicuous snap, scale pop, identity change, broken attachment, clipping, interior seam/hole, or deterministic validation failure.
   - `minor`: exact pupil or nose placement differs from the numerical ideal; a near-vertical horizontal cue is subtle; isolated reviewers disagree or return `ambiguous`; an intermediate blind majority conflicts but the labeled ordered loop still reads correctly; continuity metrics warn without a visible defect.
4. Major failures require repair. Minor failures may be overridden and the installation pipeline continues.
5. Record every override in `qa/blind-review-resolution.json` with `decision: "accept"`, `severity: "minor"`, the failed checks, the labeled/continuity evidence that makes them acceptable, and `reviewed_by: "parent"` or `"user"`. Never override a major failure.

An override is a deliberate visual judgment, not a way to silence missing evidence. The blind sheet, consensus verdicts, validation output, labeled semantics, continuity report, and resolution file all remain in the final QA artifacts.

Measure adjacent direction continuity:

```bash
"$PYTHON" "$SKILL_DIR/scripts/measure_direction_continuity.py" \
  "$RUN_DIR/final/spritesheet-extended.webp" \
  --json-out "$RUN_DIR/qa/look-continuity.json"
```

Visually QA `qa/contact-sheet-extended.png`, `qa/look-directions.png`, and `qa/look-continuity.json` before accepting. Inspect the 16 normal-size look cells as an ordered loop, not only as isolated stills. For every direction label, compare the expected direction to the visible gaze/body direction and record `pass`, `warning`, or `fail` in `qa/direction-semantics.json`. Reject only the hard failures in the Direction Acceptance Policy. Record subtler semantic or metric concerns as warnings and accept them when the loop remains cohesive, readable, identity-preserving, and visually pleasing at normal pet size.

If a blind or final visual QA worker returns `fail`, apply Blind Review Severity Resolution before queuing a repair. Continue packaging when the failure is minor and `qa/blind-review-resolution.json` records the accepted override.

Only after all deterministic and visual QA passes, package the approved extended spritesheet as a v2 pet. `spriteVersionNumber: 2` is mandatory; without it the app defaults to the 9-row v1 contract and rejects the 2288-pixel-tall asset.

```bash
PET_ID=$(jq -r '.pet_id' "$RUN_DIR/pet_request.json")
DISPLAY_NAME=$(jq -r '.display_name' "$RUN_DIR/pet_request.json")
DESCRIPTION=$(jq -r '.description' "$RUN_DIR/pet_request.json")
PET_DIR="${CODEX_HOME:-$HOME/.codex}/pets/$PET_ID"
mkdir -p "$PET_DIR"
cp "$RUN_DIR/final/spritesheet-extended.webp" "$PET_DIR/spritesheet.webp"
jq -n --arg id "$PET_ID" --arg displayName "$DISPLAY_NAME" --arg description "$DESCRIPTION" \
  '{id: $id, displayName: $displayName, description: $description, spriteVersionNumber: 2, spritesheetPath: "spritesheet.webp"}' \
  > "$PET_DIR/pet.json"
```

Write `qa/run-summary.json` after packaging:

```bash
jq -n --arg run_dir "$RUN_DIR" --arg spritesheet "$RUN_DIR/final/spritesheet-extended.webp" --arg validation "$RUN_DIR/final/validation-extended.json" --arg chroma_despill "$RUN_DIR/qa/chroma-despill-extended.json" --arg contact_sheet "$RUN_DIR/qa/contact-sheet-extended.png" --arg direction_sheet "$RUN_DIR/qa/look-directions.png" --arg direction_semantics "$RUN_DIR/qa/direction-semantics.json" --arg blind_direction_validation "$RUN_DIR/qa/direction-blind-validation.json" --arg blind_review_resolution "$RUN_DIR/qa/blind-review-resolution.json" --arg continuity "$RUN_DIR/qa/look-continuity.json" --arg review "$RUN_DIR/qa/review.json" --arg package "$PET_DIR" '{ok: true, spriteVersionNumber: 2, run_dir: $run_dir, spritesheet: $spritesheet, validation: $validation, chroma_despill: $chroma_despill, contact_sheet: $contact_sheet, direction_sheet: $direction_sheet, direction_semantics: $direction_semantics, blind_direction_validation: $blind_direction_validation, blind_review_resolution: $blind_review_resolution, continuity: $continuity, review: $review, package: $package}' > "$RUN_DIR/qa/run-summary.json"
```

After all QA and packaging succeed, keep `pet_request.json`, `final/spritesheet-extended.webp`, `final/validation-extended.json`, `qa/chroma-despill-extended.json`, `qa/contact-sheet-extended.png`, `qa/look-directions.png`, `qa/direction-semantics.json`, `qa/direction-blind-pairs.png`, `qa/direction-blind-answer-key.json`, `qa/direction-blind-verdicts.json`, `qa/direction-blind-validation.json`, `qa/blind-review-resolution.json` when an override was used, `qa/look-continuity.json`, `qa/previews/`, `qa/review.json`, and `qa/run-summary.json`. Remove prompts, layout guides, generated row strips, extracted frames, PNG intermediates, the 8x9 intermediate atlas, and the imagegen job manifest unless the user wants debug artifacts.

## Lightweight Visual Workers

Use lightweight subagents for image-heavy work by default. This bounds each `$imagegen` rollout to one selected image, keeps contact-sheet vision payloads out of the parent thread, and reduces cost while preserving the full v2 contract.

## Subagent Delegation

Use lightweight workers unless the user specifically prohibits delegation.

Parent responsibilities:

- run the brand discovery worker before preparation when the user provides a bare brand/product/company/prospect name
- prepare the run and inspect `imagegen-jobs.json`
- assign the base job, all standard rows, the four-cardinal strip, coherent look rows, blind direction QA, and final contact-sheet QA to lightweight workers
- copy selected worker outputs into their decoded paths and mark jobs complete in `imagegen-jobs.json`
- create `references/canonical-base.png` from the selected base output
- run the approved `running-left` mirror derivation when appropriate
- write the pet-specific look mechanics plan after standard-row QA
- approve the cardinal semantics and compose `decoded/look-anchors-approved.png`
- require immediate deterministic registration, post-registration edge QA, and labeled semantic QA after each coherent look-row generation
- run deterministic v2 assembly, packaging, repair regeneration, and cleanup

Base worker responsibilities:

- handle only the `base` job
- read `prompts/base-pet.md` and use any listed reference images
- use `$imagegen` only
- honor any compact brand inspiration line in the prompt as broad visual/personality guidance, without copying logos, readable marks, UI screenshots, slogans, or text
- return only `selected_source=/absolute/path/to/selected-output.png` and `qa_note=<one sentence>`

Row worker responsibilities:

- handle exactly one row job
- read the row prompt and use all listed input images
- use `$imagegen` only; do not draw, edit, tile, or synthesize sprites locally
- perform a quick visual sanity check for frame count, identity, chroma background, spacing, clipping, and detached effects
- enforce the row prompt's transparency and effects rules, including no detached effects, no wave marks for `waving`, no speed lines or dust for directional running rows, no literal foot-running for the non-directional `running` row, and only attached opaque sprite-like tears/smoke/stars when allowed by the state prompt
- for a `look-row-strip`, synthesize the complete row as one coherent family from the approved cardinals and never independently restyle individual cells
- for a `look-row-strip`, verify the output contains eight separated pose groups in the required order with no overlap or outer-canvas clipping; deterministic assembly owns exact cell cropping, one shared scale and baseline, recentering, and final-cell edge validation
- return only `selected_source=/absolute/path/to/selected-output.png` and `qa_note=<one sentence>`

Blind direction QA worker responsibilities:

- inspect only `qa/direction-blind-pairs.png`; do not provide the labeled direction sheet, atlas, prompt, degree order, prior verdicts, or hidden answer key
- classify A and B for every pair independently on the axis named in the sheet: `screen-left`, `screen-right`, `up`, `down`, or `ambiguous`, using visible pupils, nose, face surface, head turn, or the pet's natural aiming feature
- never infer from pair order; use `ambiguous` honestly when the requested axis is unreadable. Cardinal ambiguity blocks packaging; intermediate ambiguity becomes labeled-review evidence.
- never inspect or receive another blind worker's classifications; the parent combines exactly three isolated verdict files with `combine_direction_blind_verdicts.py`
- return JSON-ready pair classifications only; do not edit files or inspect unrelated artifacts

Final visual QA worker responsibilities:

- inspect the standard and extended contact sheets, direction QA sheet, row GIFs, semantic verdicts, continuity results, and v2 validation
- verify all 11 rows match the Codex app contract and the same pet identity
- return a compact result: `visual_qa=pass` or `visual_qa=fail`, plus row-specific repair notes when failing
- do not edit files, queue repairs, package, or clean up

Model choice for workers:

- Prefer a smaller capable model for brand discovery, since it returns a compact research brief rather than doing orchestration.
- Prefer a smaller capable model for visual workers, such as `gpt-5.4-mini` with medium reasoning, when model override is available.
- Use the parent/default model only for orchestration or when a smaller worker model is unavailable.
- Dynamically keep up to three generation workers active while at least three independent jobs are ready and capacity permits; backfill slots as workers finish. Use fewer workers when dependencies expose fewer jobs. Run final visual QA as a single worker after deterministic image processing. Close workers after their result has been consumed.
- Once `look-cardinals` passes, start row 9 immediately. Start row 10 only after row 9 has passed deterministic registration, post-registration edge, semantic, and continuity QA; give row 10 the completed row 9 strip as continuity evidence.

Use this base worker prompt:

```text
Generate the hatch-pet base image.

Run dir: <absolute run dir>
Job id: base
Prompt file: <absolute base prompt file>
Input images:
- <absolute path> — <role>

Use $imagegen only. Read the base prompt and attach every listed input image. If the prompt contains brand inspiration, use it only as broad mascot-safe guidance; do not copy logos, readable marks, UI screenshots, slogans, or text. Before returning, visually check that the result is one centered full-body pet on a flat chroma background, with no text, scenery, shadows, or detached effects.

Do not edit manifests, copy into decoded, mark jobs complete, generate rows, run image-processing scripts, repair, package, or open unrelated files.
Do not include Markdown image previews, base64, or extra attachments in the final response.

Return exactly:
selected_source=/absolute/path/to/selected-output.png
qa_note=<one sentence>
```

Use this cardinal-strip worker prompt:

```text
Generate one hatch-pet four-cardinal anchor strip.

Run dir: <absolute run dir>
Job id: look-cardinals
Prompt file: <absolute prompt file>
Input images:
- <absolute path> — <role>

Use $imagegen only. Read the cardinal-strip prompt and attach every listed input image. Read `qa/look-mechanics.md`. Screen-left and screen-right are viewer/image coordinates, never character-relative coordinates. Before returning, verify all four slots in order without relying on their labels: for a face, cite the nose-tip and pupil positions relative to the head center; for other pets, cite the natural aiming feature. Any ambiguous cardinal fails the strip.

Do not edit manifests, copy files, generate rows, assemble, package, or inspect unrelated files. Do not include image previews or attachments in the final response.

Return exactly:
selected_source=/absolute/path/to/selected-output.png
qa_note=<one sentence with concrete landmark evidence for all four cardinals>
```

Use this row worker prompt:

```text
Generate one hatch-pet row.

Run dir: <absolute run dir>
Row id: <row-id>
Prompt file: <absolute prompt file>
Retry prompt file: <absolute retry prompt file>
Input images:
- <absolute path> — <role>
- <absolute path> — <role>

Use $imagegen only. Read the row prompt and attach every listed input image. For a `look-row-strip` job, also read and obey `qa/look-mechanics.md`; use the approved cardinal strip for direction meaning and draw all eight cells together as one coherent family with even intermediate steps. Never paste, reuse, or independently restyle individual cells. If imagegen returns Bad Request, retry once with the retry prompt and the same input images.

Before returning, visually check: exact frame count, same pet identity as canonical base, flat chroma background, complete separated unclipped poses, and no detached effects or guide marks. For a `look-row-strip`, verify there are eight separated pose groups in the required left-to-right order, neighboring poses do not overlap, no foreground is cropped at the outer canvas edge, and the generated family keeps a consistent scale and baseline. Exact cell cropping, shared-scale normalization, recentering, and final-cell edge validation happen deterministically after generation. The prompt's transparency and effects rules are mandatory: no detached effects, no wave marks for `waving`, no speed lines or dust for directional running rows, no literal foot-running for the non-directional `running` row, and only attached opaque sprite-like tears/smoke/stars when allowed by the state prompt.

Do not edit manifests, copy into decoded, mark jobs complete, mirror rows, run image-processing scripts, repair, package, or open unrelated files.
Do not include Markdown image previews, base64, or extra attachments in the final response.

Return exactly:
selected_source=/absolute/path/to/selected-output.png
qa_note=<one sentence>
```

Use this blind direction QA worker prompt in a fresh worker that has not seen the labeled direction sheet. Spawn it without prior conversation context when the worker system supports context isolation (for example, `fork_turns="none"`):

```text
Classify one required gaze axis in an unlabeled hatch-pet A/B challenge.

Blind sheet: <absolute run dir>/qa/direction-blind-pairs.png

Inspect only this sheet. Do not open the atlas, labeled direction sheet, prompts, prior QA, degree order, answer key, or any other file.

Each row contains two normal-size pet cells labeled A and B and identifies the axis to judge. For a horizontal row, classify each cell as exactly `screen-left`, `screen-right`, or `ambiguous`. For a vertical row, classify each cell as exactly `up`, `down`, or `ambiguous`.

Judge only what is readable at the displayed pet size. Use visible landmarks such as pupils, nose tip relative to head center, face surface, head turn, eyelids, or the pet’s natural aiming feature. If the requested axis is not definite without enlarging or guessing, classify it as `ambiguous`; do not invent confidence.

Do not infer from A/B order. If A and B point the same way, report the same classification; do not force one left and one right.

Return exactly one JSON object and nothing else:
{"pairs":[{"pair":"horizontal-1|vertical-1","A":"screen-left|screen-right|up|down|ambiguous","B":"screen-left|screen-right|up|down|ambiguous","reason":"short landmark evidence"}]}

Include every pair shown in the sheet.
```

Use this final visual QA worker prompt:

```text
Visually QA one finalized hatch-pet contact sheet.

Run dir: <absolute run dir>
Contact sheet: <absolute run dir>/qa/contact-sheet.png
V2 contact sheet: <absolute run dir>/qa/contact-sheet-extended.png
Focused direction QA sheet: <absolute run dir>/qa/look-directions.png
Direction semantics JSON: <absolute run dir>/qa/direction-semantics.json
Blind direction validation JSON: <absolute run dir>/qa/direction-blind-validation.json
Look continuity JSON: <absolute run dir>/qa/look-continuity.json
Preview dir: <absolute run dir>/qa/previews
Review JSON: <absolute run dir>/qa/review.json
V2 validation JSON: <absolute run dir>/final/validation-extended.json

Inspect the contact sheet and the preview GIFs visually. Confirm the same pet identity, style, palette, silhouette, face, proportions, and props across all rows:
0 idle, 1 running-right, 2 running-left, 3 waving, 4 jumping, 5 failed, 6 waiting, 7 running, 8 review.

Require `qa/direction-blind-validation.json` to have `ok: true`, or require an explicit accepted minor override in `qa/blind-review-resolution.json`. Cardinal mismatches or ambiguity are major and block packaging. For intermediate warnings or a worker-level fail, inspect the labeled normal-size pose and ordered loop; accept when the issue is minor and there is no wrong-quadrant pose or reversal.

Inspect the 16 direction cells as a labeled ordered loop against the neutral frame and review `qa/look-continuity.json`. Produce a `pass`, `warning`, or `fail` semantic verdict for every expected direction: `000 up`, `022.5 up-right`, `045 up-right`, `067.5 up-right`, `090 right`, `112.5 down-right`, `135 down-right`, `157.5 down-right`, `180 down`, `202.5 down-left`, `225 down-left`, `247.5 down-left`, `270 left`, `292.5 up-left`, `315 up-left`, and `337.5 up-left`. Record separate horizontal and vertical landmark evidence for every diagonal. Fail wrong or ambiguous cardinals, labeled wrong-quadrant poses, and visible reversals. Record blind uncertainty on intermediate poses as warnings when labeled review and loop context confirm the intended direction.

Fail rows with identity drift, missing/blank frames, copied guide marks, white/nontransparent backgrounds, cropped bodies, slot overlap, detached effects, shadows/glows/smears/dust, motion that does not match the row state, unintended size popping, wrong facing direction, reversed or non-alternating gait, or idle loops that are effectively static. Judge chroma only on the cleaned extended contact sheet, not the pre-cleanup standard contact sheet. Do not fail or retry a row for magenta/chroma fringe after the final despill report and v2 atlas validation pass; those deterministic results are authoritative.

Do not edit files, queue repairs, package, clean up, or inspect unrelated files.

Return exactly:
visual_qa=pass|fail
qa_note=<one sentence summary>
direction_semantics=<semicolon-separated labels with pass/warning/fail and short visual reason>
review_warnings=<semicolon-separated accepted warnings, or none>
repair_rows=<comma-separated row ids, or none>
repair_notes=<short row-specific notes, or none>
```

## Repair Workflow

If frame inspection or final visual QA fails, read `qa/review.json`, regenerate the smallest failing row, copy the replacement row into the same decoded output path, and keep that job marked complete with the new `source_path` and `completed_at`. Repair the failed row, not the whole sheet.

## Rules

- Keep `$imagegen` as the primary generation layer.
- For brand/product/company/prospect requests without a concrete avatar description or reference image, run brand discovery before base generation and pass only the compact brief into the run.
- Use `$imagegen` as the only visual generation layer. Do not invoke image APIs, image CLIs, local raster generators, or one-off generation scripts from this skill.
- Keep reference images attached/visible for `$imagegen` whenever the chosen path supports references.
- Attach the row's `references/layout-guides/<state>.png` image to every row-strip job as a layout-only guide, and do not accept outputs that copy guide pixels.
- Use lightweight visual workers for base generation, row-strip visual generation, and final contact-sheet QA by default; the parent owns manifest updates, deterministic image scripts, packaging, and cleanup.
- Generate every normal visual job with `$imagegen`: base plus all row strips that are not explicitly approved `running-left` mirror derivations.
- Treat only the base job as eligible for prompt-only generation; every row job must attach its listed grounding images.
- Generate `running-right` before deciding whether `running-left` can be mirrored.
- When `running-left` is mirrored, preserve frame order and timing semantics; derive it through the deterministic script instead of mirroring an entire strip wholesale.
- Do not derive or reuse `waiting`, `running`, `failed`, `review`, `jumping`, or `waving` from another state; each has distinct app semantics and must be generated as its own row.
- Generate look row 9 directly from the approved cardinal strip, then generate row 10 only after row 9 clears deterministic registration and post-registration edge QA and has no semantic or continuity hard failure. Reviewed warnings do not block row 10. Both rows attach the cardinal strip, and row 10 must also attach completed row 9.
- Final look rows must each originate from one coherent 8-frame row generation. Individually generated repair cells may never be copied into the final atlas.
- If one look direction fails, strengthen the containing row's direction instructions and resynthesize the complete row. Do not patch the final cell directly, even when deterministic assembly supports individual-cell input.
- Deterministically register each coherent look row, then run final-cell edge diagnostics and explicit labeled semantics immediately after generation, before expensive final atlas assembly. Run blind horizontal-and-vertical axis QA as soon as both coherent rows exist.
- Never substitute locally drawn, tiled, transformed, or code-generated row strips for missing `$imagegen` outputs.
- Only mark a visual job complete after its selected output has been copied into the decoded output path.
- Never mark a failed coherent row, diagnostic iteration, or one-off repair cell as packaging eligible.
- Do not rely on generated images for exact atlas geometry; use this skill's deterministic image scripts.
- Use the chroma key stored in `pet_request.json`; do not force a fixed green screen.
- Keep the pet's silhouette, face, materials, palette, style, and props consistent across all rows.
- Treat visual identity or style drift as a blocker even when deterministic validation has no errors.
- Treat a contact sheet that shows cropped references, repeated tiles, white cell backgrounds, or non-sprite fragments as failed.
- Treat preview GIFs that show extraction-induced size popping, reversed directional timing, wrong facing direction, or inert idle loops as failed.
- Apply the Direction Acceptance Policy to look cells. Cardinals are hard gates. Intermediate blind uncertainty is a warning unless labeled normal-size review confirms a wrong quadrant, missing axis, or loop reversal.
- Treat a missing explicit per-direction semantic gaze review as failed even when the focused QA sheet and continuity JSON exist.
- Treat missing `qa/direction-semantics.json` as failed. The file must include every expected direction with `verdict`, `expected`, `observed`, and `reason` fields. Packaging requires no `fail` verdicts; reviewed `warning` verdicts are allowed.
- Treat missing or failed `qa/direction-blind-validation.json` as failed. Each of the three isolated blind reviewers must see only the randomized A/B sheet, never degree labels, the answer key, or another verdict. Cardinal mismatches or ambiguity fail validation; intermediate mismatches or ambiguity remain review warnings.
- Never use the same worker for blind A/B classification after it has seen the labeled direction sheet or direction prompts. Label-conditioned classification is not independent evidence.
- Do not let the parent agent self-approve a repaired look direction. Run an independent final visual QA worker on `qa/look-directions.png` or ask the user to inspect it before packaging.
- After an independent blind or final QA fail, the parent may override only a minor issue under Blind Review Severity Resolution. Record the evidence in `qa/blind-review-resolution.json`; never override a major failure.
- For humanoid cardinal verdicts, record concrete screen-coordinate landmark evidence in `qa/direction-semantics.json`. Intermediate verdicts may use holistic head, face, posture, and ordered-loop evidence; exact pupil or nose placement is advisory rather than mandatory.
- Treat look rows that rotate, skew, or tilt the whole sprite to fake gaze as failed unless the pet is literally a rotating object and the look mechanics decision explicitly justifies whole-object rotation.
- Treat pupil-only motion or underused natural mechanics as a warning unless it visibly breaks identity, direction meaning, or loop cohesion.
- Treat adjacent continuity metrics as review evidence. Fail only when visual QA confirms a conspicuous snap, pop, registration jump, identity change, broken silhouette, or semantic discontinuity.
- Treat forbidden detached effects, shadows, glows, smears, dust, landing marks, wave marks, speed lines, or motion trails as failed rows. Chroma-key-adjacent generation artifacts are handled only by the single deterministic despill pass and never trigger image retries after that pass reports success.
- Treat `qa/review.json` errors as blockers. Warnings require visual review.

## Acceptance Criteria

- Final atlas is PNG or WebP, exactly `1536x2288`, and based on `192x208` cells. The `1536x1872` standard atlas is intermediate-only.
- `pet.json` contains `spriteVersionNumber: 2`, the extended despill report has `ok: true`, and the packaged spritesheet passes `validate_atlas.py --require-v2` with the run's chroma key. These deterministic results close chroma QA; no separate visual chroma-fringe gate or image retry is allowed.
- Used cells are non-empty and unused cells are fully transparent.
- Atlas follows the row/frame counts in `references/animation-rows.md`.
- The four-cardinal strip has been deterministically extracted, its clipping report passes, and all four anchors are semantically approved before look-row generation.
- Both coherent look rows use `decoded/look-anchors-approved.png` as the direction basis, interpolate all intermediate directions as even 22.5-degree steps, and preserve the fixed clockwise order.
- Deterministic pose-group registration, post-registration final-cell edge diagnostics, and labeled per-direction semantic QA pass immediately on each coherent source row before final atlas assembly; blind horizontal-and-vertical axis QA runs after both rows exist.
- Contact sheet and per-row motion previews have been produced and inspected by a lightweight visual QA worker.
- A focused neutral-plus-16-directions QA sheet has been produced and inspected before packaging.
- A randomized unlabeled horizontal-and-vertical axis pair sheet has been classified by three isolated blind workers and combined by strict majority. Both cardinal pairs pass. `qa/direction-blind-validation.json` has `ok: true`, or a worker-level/intermediate failure has an accepted minor resolution in `qa/blind-review-resolution.json` backed by labeled and continuity evidence.
- Every expected direction has an explicit `pass`, `warning`, or `fail` semantic verdict with horizontal and vertical axis evidence where applicable; no wrong cardinal, labeled wrong-quadrant pose, or visible reversal remains.
- `qa/direction-semantics.json` records verdicts for all 16 directions from an independent visual QA worker or explicit user inspection, including review notes for accepted warnings.
- `qa/look-continuity.json` has been reviewed; metric warnings are acceptable when the normal-size ordered loop has no visible snap, pop, identity change, or semantic discontinuity.
- `qa/review.json` has no errors.
- Row-by-row review confirms the animation cycles are complete enough for the Codex app.
- Motion previews do not show unintended size popping, reversed directional cadence, or wrong row semantics.
- Look directions follow the fixed clockwise order and form a cohesive, readable loop at normal pet size. Cardinals must be unmistakable. Intermediate blind uncertainty is acceptable as a reviewed warning when labeled normal-size review confirms the intended direction and the loop does not reverse.
- Non-pixel styles are accepted when readable at pet size and consistent across rows.
- `${CODEX_HOME:-$HOME/.codex}/pets/<pet-name>/pet.json` and `${CODEX_HOME:-$HOME/.codex}/pets/<pet-name>/spritesheet.webp` are staged together for custom pets.

</skill>

## assistant · 2026-08-03T01:45:41Z

I’m using the hatch-pet workflow to upgrade Joke Bear in place: I’ll preserve its approved animation rows, generate and validate the 16 look directions, then package it as version 2.

## tool · 2026-08-03T01:45:43Z


Script completed
Wall time 0.1 seconds
Output:

/Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills
---
name: "imagegen"
description: "Generate or edit raster images when the task benefits from AI-created bitmap visuals such as photos, illustrations, textures, sprites, mockups, or transparent-background cutouts. Use when Codex should create a brand-new image, transform an existing image, or derive visual variants from references, and the output should be a bitmap asset rather than repo-native code or vector. Do not use when the task is better handled by editing existing SVG/vector/code-native assets, extending an established icon or logo system, or building the visual directly in HTML/CSS/canvas."
---

# Image Generation Skill

Generates or edits images for the current project (for example website assets, game assets, UI mockups, product mockups, wireframes, logo design, photorealistic images, or infographics).

## Top-level modes and rules

This skill has exactly two top-level modes:

- **Default built-in tool mode (preferred):** built-in `image_gen` tool for normal image generation, editing, and simple transparent-image requests. Does not require `OPENAI_API_KEY`.
- **Fallback CLI mode:** `scripts/image_gen.py` CLI. Use when the user explicitly asks for the CLI/API/model path, or after the user explicitly confirms a true model-native transparency fallback with `gpt-image-1.5`. Requires `OPENAI_API_KEY`.

Within CLI fallback, the CLI exposes three subcommands:

- `generate`
- `edit`
- `generate-batch`

Rules:
- Use the built-in `image_gen` tool by default for normal image generation and editing requests.
- Do not switch to CLI fallback for ordinary quality, size, or file-path control.
- If the user explicitly asks for a transparent image/background, stay on built-in `image_gen` first: prompt for a flat removable chroma-key background, then remove it locally with the installed helper at `$CODEX_HOME/skills/.system/imagegen/scripts/remove_chroma_key.py`.
- Never silently switch from built-in `image_gen` or CLI `gpt-image-2` to CLI `gpt-image-1.5`. Treat this as a model/path downgrade and ask the user before doing it, unless the user has already explicitly requested `gpt-image-1.5`, `scripts/image_gen.py`, or CLI fallback.
- If a transparent request appears too complex for clean chroma-key removal, asks for true/native transparency, or local removal fails validation, explain that true transparency requires CLI `gpt-image-1.5 --background transparent --output-format png` because `gpt-image-2` does not support `background=transparent`, then ask whether to proceed. Run the CLI fallback only after the user confirms.
- The word `batch` by itself does not mean CLI fallback. If the user asks for many assets or says to batch-generate assets without explicitly asking for CLI/API/model controls, stay on the built-in path and issue one built-in call per requested asset or variant.
- If the built-in tool fails or is unavailable, tell the user the CLI fallback exists and that it requires `OPENAI_API_KEY`. Proceed only if the user explicitly asks for that fallback.
- If the user explicitly asks for CLI mode, use the bundled `scripts/image_gen.py` workflow. Do not create one-off SDK runners.
- Never modify `scripts/image_gen.py`. If something is missing, ask the user before doing anything else.

Built-in save-path policy:
- In built-in tool mode, Codex saves generated images under `$CODEX_HOME/*` by default.
- Do not describe or rely on OS temp as the default built-in destination.
- Do not describe or rely on a destination-path argument (if any) on the built-in `image_gen` tool. If a specific location is needed, generate first and then move or copy the selected output from `$CODEX_HOME/generated_images/...`.
- Save-path precedence in built-in mode:
  1. If the user names a destination, move or copy the selected output there.
  2. If the image is meant for the current project, move or copy the final selected image into the workspace before finishing.
  3. If the image is only for preview or brainstorming, render it inline; the underlying file can remain at the default `$CODEX_HOME/*` path.
- Never leave a project-referenced asset only at the default `$CODEX_HOME/*` path.
- Do not overwrite an existing asset unless the user explicitly asked for replacement; otherwise create a sibling versioned filename such as `hero-v2.png` or `item-icon-edited.png`.

Shared prompt guidance for both modes lives in `references/prompting.md` and `references/sample-prompts.md`.

Fallback-only docs/resources for CLI mode:
- `references/cli.md`
- `references/image-api.md`
- `references/codex-network.md`
- `scripts/image_gen.py`

Local post-processing helper:
- `$CODEX_HOME/skills/.system/imagegen/scripts/remove_chroma_key.py`: removes a flat chroma-key background from a generated image and writes a PNG/WebP with alpha. Prefer auto-key sampling, soft matte, and despill for antialiased edges.

## When to use
- Generate a new image (concept art, product shot, cover, website hero)
- Generate a new image using one or more reference images for style, composition, or mood
- Edit an existing image (inpainting, lighting or weather transformations, background replacement, object removal, compositing, transparent background)
- Produce many assets or variants for one task

## When not to use
- Extending or matching an existing SVG/vector icon set, logo system, or illustration library inside the repo
- Creating simple shapes, diagrams, wireframes, or icons that are better produced directly in SVG, HTML/CSS, or canvas
- Making a small project-local asset edit when the source file already exists in an editable native format
- Any task where the user clearly wants deterministic code-native output instead of a generated bitmap

## Decision tree

Think about two separate questions:

1. **Intent:** is this a new image or an edit of an existing image?
2. **Execution strategy:** is this one asset or many assets/variants?

Intent:
- If the user wants to modify an existing image while preserving parts of it, treat the request as **edit**.
- If the user provides images only as references for style, composition, mood, or subject guidance, treat the request as **generate**.
- If the user provides no images, treat the request as **generate**.

Built-in edit semantics:
- Built-in edit mode is for images already visible in the conversation context, such as attached images or images generated earlier in the thread.
- If the user wants to edit a local image file with the built-in tool, first load it with built-in `view_image` tool so the image is visible in the conversation context, then proceed with the built-in edit flow.
- Do not promise arbitrary filesystem-path editing through the built-in tool.
- If a local file still needs direct file-path control, masks, or other explicit CLI-only parameters, use the explicit CLI fallback only when the user asks for it.
- For edits, preserve invariants aggressively and save non-destructively by default.

Execution strategy:
- In the built-in default path, produce many assets or variants by issuing one `image_gen` call per requested asset or variant.
- In the CLI fallback path, use the CLI `generate-batch` subcommand only when the user explicitly chose CLI mode and needs many prompts/assets.
- For many distinct assets, do not use `n` as a substitute for separate prompts. `n` is for variants of one prompt; distinct assets need distinct built-in calls or distinct CLI `generate-batch` jobs.

Assume the user wants a new image unless they clearly ask to change an existing one.

## Workflow
1. Decide the top-level mode: built-in by default, including simple transparent-output requests; fallback CLI only if explicitly requested or after the user explicitly confirms a transparent-output fallback.
2. Decide the intent: `generate` or `edit`.
3. Decide whether the output is preview-only or meant to be consumed by the current project.
4. Decide the execution strategy: single asset vs repeated built-in calls vs CLI `generate-batch`.
5. Collect inputs up front: prompt(s), exact text (verbatim), constraints/avoid list, and any input images.
6. For every input image, label its role explicitly:
   - reference image
   - edit target
   - supporting insert/style/compositing input
7. If the edit target is only on the local filesystem and you are staying on the built-in path, inspect it with `view_image` first so the image is available in conversation context.
8. If the user asked for a photo, illustration, sprite, product image, banner, or other explicitly raster-style asset, use `image_gen` rather than substituting SVG/HTML/CSS placeholders. If the request is for an icon, logo, or UI graphic that should match existing repo-native SVG/vector/code assets, prefer editing those directly instead.
9. Augment the prompt based on specificity:
   - If the user's prompt is already specific and detailed, normalize it into a clear spec without adding creative requirements.
   - If the user's prompt is generic, add tasteful augmentation only when it materially improves output quality.
10. Use the built-in `image_gen` tool by default.
11. For transparent-output requests, follow the transparent image guidance below: generate with built-in `image_gen` on a flat chroma-key background, copy the selected output into the workspace or `tmp/imagegen/`, run the installed `$CODEX_HOME/skills/.system/imagegen/scripts/remove_chroma_key.py` helper, and validate the alpha result before using it. If this path looks unsuitable or fails, ask before switching to CLI `gpt-image-1.5`.
12. Inspect outputs and validate: subject, style, composition, text accuracy, and invariants/avoid items.
13. Iterate with a single targeted change, then re-check.
14. For preview-only work, render the image inline; the underlying file may remain at the default `$CODEX_HOME/generated_images/...` path.
15. For project-bound work, move or copy the selected artifact into the workspace and update any consuming code or references. Never leave a project-referenced asset only at the default `$CODEX_HOME/generated_images/...` path.
16. For batches or multi-asset requests, persist every requested deliverable final in the workspace unless the user explicitly asked to keep outputs preview-only. Discarded variants do not need to be kept unless requested.
17. If the user explicitly chooses or confirms the CLI fallback, then use the fallback-only docs for model, quality, size, `input_fidelity`, masks, output format, output paths, and network setup.
18. Always report the final saved path(s) for any workspace-bound asset(s), plus the final prompt or prompt set and whether the built-in tool or fallback CLI mode was used.

## Transparent image requests

Transparent-image requests still use built-in `image_gen` first. Because the built-in tool does not expose a true transparent-background control, create a removable chroma-key source image and then convert the key color to alpha locally.

Default sequence:
1. Use built-in `image_gen` to generate the requested subject on a perfectly flat solid chroma-key background.
2. Choose a key color that is unlikely to appear in the subject: default `#00ff00`, use `#ff00ff` for green subjects, and avoid `#0000ff` for blue subjects.
3. After generation, move or copy the selected source image from `$CODEX_HOME/generated_images/...` into the workspace or `tmp/imagegen/`.
4. Run the installed helper path, not a project-relative script path:
   ```bash
   python "${CODEX_HOME:-$HOME/.codex}/skills/.system/imagegen/scripts/remove_chroma_key.py" \
     --input <source> \
     --out <final.png> \
     --auto-key border \
     --soft-matte \
     --transparent-threshold 12 \
     --opaque-threshold 220 \
     --despill
   ```
5. Validate that the output has an alpha channel, transparent corners, plausible subject coverage, and no obvious key-color fringe. If a thin fringe remains, retry once with `--edge-contract 1`; use `--edge-feather 0.25` only when the edge is visibly stair-stepped and the subject is not shiny or reflective.
6. Save the final alpha PNG/WebP in the project if the asset is project-bound. Never leave a project-referenced transparent asset only under `$CODEX_HOME/*`.

Prompt transparent requests like this:

```text
Create the requested subject on a perfectly flat solid #00ff00 chroma-key background for background removal.
The background must be one uniform color with no shadows, gradients, texture, reflections, floor plane, or lighting variation.
Keep the subject fully separated from the background with crisp edges and generous padding.
Do not use #00ff00 anywhere in the subject.
No cast shadow, no contact shadow, no reflection, no watermark, and no text unless explicitly requested.
```

Do not automatically use CLI `gpt-image-1.5 --background transparent --output-format png` instead of chroma keying. Ask the user first when the user asks for true/native transparency, when local removal fails validation, or when the requested image is complex: hair, fur, feathers, smoke, glass, liquids, translucent materials, reflective objects, soft shadows, realistic product grounding, or subject colors that conflict with all practical key colors.

Use a concise confirmation like:

```text
This likely needs true native transparency. The default built-in path uses a chroma-key background plus local removal, but true transparency requires the CLI fallback with gpt-image-1.5 because gpt-image-2 does not support background=transparent. It also requires OPENAI_API_KEY. Should I proceed with that CLI fallback?
```

## Prompt augmentation

Reformat user prompts into a structured, production-oriented spec. Make the user's goal clearer and more actionable, but do not blindly add detail.

Treat this as prompt-shaping guidance, not a closed schema. Use only the lines that help, and add a short extra labeled line when it materially improves clarity.

### Specificity policy

Use the user's prompt specificity to decide how much augmentation is appropriate:

- If the prompt is already specific and detailed, preserve that specificity and only normalize/structure it.
- If the prompt is generic, you may add tasteful augmentation when it will materially improve the result.

Allowed augmentations:
- composition or framing hints
- polish level or intended-use hints
- practical layout guidance
- reasonable scene concreteness that supports the stated request

Not allowed augmentations:
- extra characters or objects that are not implied by the request
- brand names, slogans, palettes, or narrative beats that are not implied
- arbitrary side-specific placement unless the surrounding layout supports it

## Use-case taxonomy (exact slugs)

Classify each request into one of these buckets and keep the slug consistent across prompts and references.

Generate:
- photorealistic-natural — candid/editorial lifestyle scenes with real texture and natural lighting.
- product-mockup — product/packaging shots, catalog imagery, merch concepts.
- ui-mockup — app/web interface mockups and wireframes; specify the desired fidelity.
- infographic-diagram — diagrams/infographics with structured layout and text.
- scientific-educational — classroom explainers, scientific diagrams, and learning visuals with required labels and accuracy constraints.
- ads-marketing — campaign concepts and ad creatives with audience, brand position, scene, and exact tagline/copy.
- productivity-visual — slide, chart, workflow, and data-heavy business visuals.
- logo-brand — logo/mark exploration, vector-friendly.
- illustration-story — comics, children’s book art, narrative scenes.
- stylized-concept — style-driven concept art, 3D/stylized renders.
- historical-scene — period-accurate/world-knowledge scenes.

Edit:
- text-localization — translate/replace in-image text, preserve layout.
- identity-preserve — try-on, person-in-scene; lock face/body/pose.
- precise-object-edit — remove/replace a specific element (including interior swaps).
- lighting-weather — time-of-day/season/atmosphere changes only.
- background-extraction — transparent background / clean cutout. Use built-in `image_gen` with chroma-key removal first for simple opaque subjects; ask before using CLI true transparency for complex subjects.
- style-transfer — apply reference style while changing subject/scene.
- compositing — multi-image insert/merge with matched lighting/perspective.
- sketch-to-render — drawing/line art to photoreal render.

## Shared prompt schema

Use the following labeled spec as shared prompt scaffolding for both top-level modes:

```text
Use case: <taxonomy slug>
Asset type: <where the asset will be used>
Primary request: <user's main prompt>
Input images: <Image 1: role; Image 2: role> (optional)
Scene/backdrop: <environment>
Subject: <main subject>
Style/medium: <photo/illustration/3D/etc>
Composition/framing: <wide/close/top-down; placement>
Lighting/mood: <lighting + mood>
Color palette: <palette notes>
Materials/textures: <surface details>
Text (verbatim): "<exact text>"
Constraints: <must keep/must avoid>
Avoid: <negative constraints>
```

Notes:
- `Asset type` and `Input images` are prompt scaffolding, not dedicated CLI flags.
- `Scene/backdrop` refers to the visual setting. It is not the same as the fallback CLI `background` parameter, which controls output transparency behavior.
- Fallback-only execution notes such as `Quality:`, `Input fidelity:`, masks, output format, and output paths belong in the CLI path only. Do not treat them as built-in `image_gen` tool arguments.

Augmentation rules:
- Keep it short.
- Add only the details needed to improve the prompt materially.
- For edits, explicitly list invariants (`change only X; keep Y unchanged`).
- If any critical detail is missing and blocks success, ask a question; otherwise proceed.
fatal: not a git repository (or any of the parent directories): .git


## tool · 2026-08-03T01:45:49Z


Script completed
Wall time 0.1 seconds
Output:

[{},"Workspace dependencies are available for this local desktop thread.\n\n### Workspace Dependencies\nUse these bundled paths for sheets, slides, documents, PDFs, images, or browser automation:\n- Bundle version: `26.802.11031`\n- Git executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/fallback/git`\n- Node.js executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node`\n- Node.js packages: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/node_modules`\n- pnpm executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/fallback/pnpm`\n- Python executable: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/bin/python3`\n- Python packages: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/python`\n- Override binaries: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/override`\n- Fallback binaries: `/Users/oyamahappa/.cache/codex-runtimes/codex-primary-runtime/dependencies/bin/fallback`",{"chunk_id":"2720d8","wall_time_seconds":0.000003,"exit_code":0,"original_token_count":89,"output":"/Users/oyamahappa/.codex/pets/jokebear/spritesheet.webp\n/Users/oyamahappa/.codex/pets/jokebear/pet.json\ntotal 2536\ndrwxr-xr-x  4 oyamahappa  staff   128B Aug  3 09:44 .\ndrwxr-xr-x  3 oyamahappa  staff    96B Aug  3 09:44 ..\n-rw-r--r--  1 oyamahappa  staff   294B Aug  3 09:44 pet.json\n-rw-r--r--  1 oyamahappa  staff   1.2M Aug  3 09:44 spritesheet.webp\n"}]

## tool · 2026-08-03T01:45:58Z


Script completed
Wall time 3.2 seconds
Output:

{
  "id": "jokebear",
  "displayName": "joke bear",
  "description": "An unofficial implementation of the Joke Bear Codex Pet. Characters by Japanese creator Nagano. Reference: https://en.namu.wiki/w/%EB%86%8D%EB%8B%B4%EA%B3%B0",
  "spritesheetPath": "spritesheet.webp",
  "kind": "creature"
}
/Users/oyamahappa/.codex/pets/jokebear/spritesheet.webp
  pixelWidth: 1536
  pixelHeight: 1872
usage: prepare_pet_run.py [-h] [--pet-name PET_NAME] [--pet-id PET_ID]
                          [--display-name DISPLAY_NAME]
                          [--description DESCRIPTION] [--reference REFERENCE]
                          [--output-dir OUTPUT_DIR] [--pet-notes PET_NOTES]
                          [--brand-name BRAND_NAME]
                          [--brand-brief BRAND_BRIEF]
                          [--brand-source BRAND_SOURCE]
                          [--brand-discovery-file BRAND_DISCOVERY_FILE]
                          [--style-preset {3d-toy,auto,brand-inspired,clay,flat-vector,painterly,pixel,plush,sticker}]
                          [--style-notes STYLE_NOTES]
                          [--chroma-key CHROMA_KEY] [--force]

Create a Codex pet run folder, prompts, and imagegen job manifest.

options:
  -h, --help            show this help message and exit
  --pet-name PET_NAME   User-facing pet name. Ask the user for this when
                        practical; otherwise choose a short appropriate name.
  --pet-id PET_ID       Stable pet folder/id slug. Defaults to the slugified
                        pet name.
  --display-name DISPLAY_NAME
                        Display label. Defaults to the pet name.
  --description DESCRIPTION
  --reference REFERENCE
  --output-dir OUTPUT_DIR
  --pet-notes PET_NOTES
  --brand-name BRAND_NAME
                        Brand, company, or product name used for broad mascot
                        inspiration.
  --brand-brief BRAND_BRIEF
                        Compact researched brand cue sentence for the base pet
                        only.
  --brand-source BRAND_SOURCE
                        Source URL used to produce the brand brief. May be
                        passed multiple times.
  --brand-discovery-file BRAND_DISCOVERY_FILE
                        Optional markdown discovery brief to copy into the run
                        for review.
  --style-preset {3d-toy,auto,brand-inspired,clay,flat-vector,painterly,pixel,plush,sticker}
                        Pet-safe style preset to use across the base and all
                        animation rows.
  --style-notes STYLE_NOTES
  --chroma-key CHROMA_KEY
                        Chroma key as #RRGGBB, or auto to choose a safe key
                        from reference colors.
  --force
/Users/oyamahappa/.codex/skills/hatch-pet/scripts/validate_atlas.py:103: DeprecationWarning: Image.Image.getdata is deprecated and will be removed in Pillow 14 (2027-10-15). Use get_flattened_data instead.
  visible = [value > 0 for value in alpha.getdata()]
/Users/oyamahappa/.codex/skills/hatch-pet/scripts/validate_atlas.py:116: DeprecationWarning: Image.Image.getdata is deprecated and will be removed in Pillow 14 (2027-10-15). Use get_flattened_data instead.
  rgba.getdata(), alpha.getdata(), expanded.getdata()
{
  "ok": false,
  "file": "/Users/oyamahappa/.codex/pets/jokebear/spritesheet.webp",
  "format": "WEBP",
  "mode": "RGBA",
  "columns": 8,
  "rows": 9,
  "sprite_version_number": 1,
  "width": 1536,
  "height": 1872,
  "transparent_rgb_residue_pixels": 1157271,
  "errors": [
    "atlas has 1157271 fully transparent pixels with non-zero RGB residue"
  ],
  "warnings": []
}
{
  "ok": false,
  "file": "/Users/oyamahappa/.codex/pets/jokebear/spritesheet.webp",
  "format": "WEBP",
  "mode": "RGBA",
  "columns": 8,
  "rows": 9,
  "sprite_version_number": 1,
  "width": 1536,
  "height": 1872,
  "transparent_rgb_residue_pixels": 1157271,
  "errors": [
    "atlas has 1157271 fully transparent pixels with non-zero RGB residue"
  ],
  "warnings": [],
  "cells": [
    {
      "state": "idle",
      "row": 0,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 18505,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 18065,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 17730,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 18242,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 18037,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 18110,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "idle",
      "row": 0,
      "column": 6,
      "used": false,
      "nontransparent_pixels": 0,
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
      "nontransparent_pixels": 20045,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 18003,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 20167,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 17053,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 17713,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 18830,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 17562,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-right",
      "row": 1,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 17213,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 17213,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 17562,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 18830,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 17713,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 17053,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 20167,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 18003,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running-left",
      "row": 2,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 20045,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 19999,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 20234,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 20579,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waving",
      "row": 3,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 19681,
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
      "nontransparent_pixels": 22048,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 20433,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 22291,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 20228,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "jumping",
      "row": 4,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 22173,
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
      "nontransparent_pixels": 20164,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 20068,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 22649,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 23141,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 21021,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 26859,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 6,
      "used": true,
      "nontransparent_pixels": 22940,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "failed",
      "row": 5,
      "column": 7,
      "used": true,
      "nontransparent_pixels": 19956,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 0,
      "used": true,
      "nontransparent_pixels": 18510,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 18324,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 18135,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 18405,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 18469,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "waiting",
      "row": 6,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 18034,
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
      "nontransparent_pixels": 19796,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 19170,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 19077,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 19214,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 18980,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "running",
      "row": 7,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 19425,
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
      "nontransparent_pixels": 18112,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 1,
      "used": true,
      "nontransparent_pixels": 17950,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 2,
      "used": true,
      "nontransparent_pixels": 17589,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 3,
      "used": true,
      "nontransparent_pixels": 17716,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 4,
      "used": true,
      "nontransparent_pixels": 19357,
      "opaque_chroma_key_pixels": 0,
      "chroma_fringe_pixels": 0
    },
    {
      "state": "review",
      "row": 8,
      "column": 5,
      "used": true,
      "nontransparent_pixels": 17961,
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
    }
  ]
}


## assistant · 2026-08-03T01:46:04Z

The source is a 9-row (v1) 1536×1872 atlas, so its existing standard animations can be retained. I’m setting up an upgrade run around that atlas and will add only the two coherent look-direction rows.

## tool · 2026-08-03T01:46:11Z


Script completed
Wall time 0.2 seconds
Output:

{
  "ok": true,
  "run_dir": "/Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/work/jokebear-v2-upgrade",
  "request": "/Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/work/jokebear-v2-upgrade/pet_request.json",
  "jobs": "/Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/work/jokebear-v2-upgrade/imagegen-jobs.json",
  "ready_jobs": [
    "base"
  ]
}
{
  "id": "base",
  "kind": "base-pet",
  "status": "pending",
  "depends_on": [],
  "prompt_file": "prompts/base-pet.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    }
  ],
  "output_path": "decoded/base.png"
}
{
  "id": "idle",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/idle.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/idle.png",
      "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/idle.png"
}
{
  "id": "running-right",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/running-right.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/running-right.png",
      "role": "layout guide for 8 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/running-right.png"
}
{
  "id": "running-left",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base",
    "running-right"
  ],
  "prompt_file": "prompts/rows/running-left.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/running-left.png",
      "role": "layout guide for 8 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    },
    {
      "path": "decoded/running-right.png",
      "role": "rightward gait reference for leftward row decision"
    }
  ],
  "output_path": "decoded/running-left.png"
}
{
  "id": "waving",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/waving.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/waving.png",
      "role": "layout guide for 4 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/waving.png"
}
{
  "id": "jumping",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/jumping.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/jumping.png",
      "role": "layout guide for 5 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/jumping.png"
}
{
  "id": "failed",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/failed.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/failed.png",
      "role": "layout guide for 8 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/failed.png"
}
{
  "id": "waiting",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/waiting.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/waiting.png",
      "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/waiting.png"
}
{
  "id": "running",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/running.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/running.png",
      "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/running.png"
}
{
  "id": "review",
  "kind": "row-strip",
  "status": "pending",
  "depends_on": [
    "base"
  ],
  "prompt_file": "prompts/rows/review.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/review.png",
      "role": "layout guide for 6 frame slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    }
  ],
  "output_path": "decoded/review.png"
}
{
  "id": "look-cardinals",
  "kind": "look-cardinal-strip",
  "status": "pending",
  "depends_on": [
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
  "prompt_file": "prompts/look-cardinals.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/look-cardinals.png",
      "role": "layout guide for four cardinal slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    },
    {
      "path": "qa/contact-sheet.png",
      "role": "approved standard-row identity, scale, and baseline reference"
    }
  ],
  "output_path": "decoded/look-cardinals.png"
}
{
  "id": "look-row-9",
  "kind": "look-row-strip",
  "status": "pending",
  "depends_on": [
    "look-cardinals"
  ],
  "prompt_file": "prompts/rows/look-row-9.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/look-row-9.png",
      "role": "layout guide for 8 direction slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    },
    {
      "path": "qa/contact-sheet.png",
      "role": "approved standard-row identity, scale, and baseline reference"
    },
    {
      "path": "decoded/look-anchors-approved.png",
      "role": "approved cardinal reference strip in order 000 up, 090 screen-right, 180 down, 270 screen-left; interpolate intermediate directions evenly"
    }
  ],
  "output_path": "decoded/look-row-9.png"
}
{
  "id": "look-row-10",
  "kind": "look-row-strip",
  "status": "pending",
  "depends_on": [
    "look-cardinals",
    "look-row-9"
  ],
  "prompt_file": "prompts/rows/look-row-10.md",
  "input_images": [
    {
      "path": "references/reference-01.webp",
      "role": "pet reference"
    },
    {
      "path": "references/layout-guides/look-row-10.png",
      "role": "layout guide for 8 direction slots; use for spacing only, do not copy guide lines"
    },
    {
      "path": "references/canonical-base.png",
      "role": "canonical identity reference"
    },
    {
      "path": "qa/contact-sheet.png",
      "role": "approved standard-row identity, scale, and baseline reference"
    },
    {
      "path": "decoded/look-anchors-approved.png",
      "role": "approved cardinal reference strip in order 000 up, 090 screen-right, 180 down, 270 screen-left; interpolate intermediate directions evenly"
    },
    {
      "path": "decoded/look-row-9.png",
      "role": "completed first half of the clockwise look loop for row 10 continuity"
    }
  ],
  "output_path": "decoded/look-row-10.png"
}


## tool · 2026-08-03T01:46:15Z


Script completed
Wall time 0.0 seconds
Output:

[{"name":"mcp__node_repl__js","description":"Use `js` to run JavaScript in the persistent Node-backed kernel. When a skill or prompt says to use `node_repl`, call this server's `js` execution tool. Calls default to a 30000 ms (30 seconds) timeout when `timeout_ms` is omitted. The runtime exposes `nodeRepl.cwd`, `nodeRepl.homeDir`, `nodeRepl.tmpDir`, `nodeRepl.requestMeta`, `nodeRepl.setResponseMeta(...)`, and `await nodeRepl.emitImage(...)`. Top-level bindings persist across `js` calls until `js_reset`; do not redeclare existing `const` or `let` names. Reuse existing bindings, use top-level `var` for reusable state that may be assigned again, or choose a fresh descriptive name. Use `js_add_node_module_dir` before `js` when a skill provides an extra package directory, and use dynamic imports like `await import(\"playwright\")` rather than filesystem paths under `./node_modules`.\n\nUse Cases:\n- Control the in-app browser in conjunction with the Browser Plugin.\n- Control the Chrome browser in conjunction with the Chrome Plugin. Prefer this method of controlling Chrome over alternatives (such as Computer Use) unless the user explicitly mentions an alternative.\n- Control desktop apps on macOS through Computer Use.\n\nRun JavaScript in a persistent Node-backed kernel with top-level await. This is the JavaScript execution tool for the `node_repl` MCP server; use it whenever instructions say to use `node_repl`, the Node REPL MCP, or run Node REPL code. If `timeout_ms` is omitted, execution times out after 30000 ms (30 seconds); pass a larger `timeout_ms` for slow browser automation or other long-running operations. Use `nodeRepl.cwd`, `nodeRepl.homeDir`, and `nodeRepl.tmpDir` to inspect host paths. Use `nodeRepl.requestMeta` to inspect the current MCP request `_meta` object during a tool call. Use `nodeRepl.setResponseMeta(meta)` to attach top-level MCP result `_meta`; repeated calls shallow-merge object keys for the current tool call. Use `nodeRepl.write(value)` to add output without a newline. Strings are unchanged; other values use console-style formatting, including BigInt and circular objects. Prefer it over `console.log(...)` for final output; `console.log(...)` remains useful for debugging or multiple values. Use `await nodeRepl.emitImage(imageLike)` to return images; each call adds one image to the outer tool result, so call it multiple times to emit multiple images. Supported image inputs are a data or file URL, inferred PNG/JPEG/WebP bytes, or `{ bytes, mimeType }`. Saved references to `nodeRepl.write(...)` and `nodeRepl.emitImage(...)` stay reusable across calls, but async callbacks that fire after a call finishes still fail because no exec is active. Top-level bindings persist across calls until `js_reset`. If a call throws, prior bindings remain available and bindings that finished initializing before the throw often remain reusable. For reusable names that may be assigned again later, prefer top-level `var name = ...`; `var` can be redeclared across calls. If you hit `SyntaxError: Identifier 'x' has already been declared`, reuse the existing binding if possible, reassign it only if it was declared with `let` or `var`, or pick a new name instead of resetting immediately; a previous `const x` cannot be changed into `var x`. Use a short `{ ... }` block only for temporary scratch names, and do not wrap an entire call in block scope if you want those names reusable later. Use dynamic imports like `await import(\"playwright\")`, `await import(\"pkg\")`, or `await import(\"./file.js\")`; top-level static `import` is not supported. Import packages by package name after installing them into a directory added with `js_add_node_module_dir`, `NODE_REPL_NODE_MODULE_DIRS`, or the working directory. Do not import package entrypoints by filesystem path such as `./node_modules/playwright/index.mjs`. Imported local files must be ESM `.js` or `.mjs` files and run in the context chosen at their dynamic-import boundary, so they can also use `nodeRepl.*`, the captured `console`, and `import.meta` helpers. Bare imports from model code and local files resolve from the REPL-wide search roots (`NODE_REPL_NODE_MODULE_DIRS`, then directories later added with `js_add_node_module_dir`, then cwd); dependencies of trusted ESM packages use Node's package-relative lookup. Imported local files may statically import other local `.js` / `.mjs` files, available packages, and allowed Node builtins. `import.meta.resolve()` returns importable strings such as `file://...`, bare package names, and `node:...` specifiers. Local file modules reload between execs; trusted package entrypoints retain singleton identity. `node:` builtins are generally available via dynamic import, but model code cannot import `process` / `node:process` because the current Rust-server-to-Node-child transport runs over stdio and raw process streams can corrupt it. Trusted modules that import or reference `process` receive only a frozen metadata-only process shim with `arch`, `cwd()`, `env`, `pid`, and `platform`. Prefer `nodeRepl.write(...)` for text or formatted values and `nodeRepl.emitImage(...)` for images.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__node_repl__js(args: {\n  // JavaScript source to execute in the persistent Node-backed kernel. The code runs with top-level await and can use the `nodeRepl` helpers. Examples: `nodeRepl.write(nodeRepl.cwd)`, `const { chromium } = await import(\"playwright\")`, or `await nodeRepl.emitImage(pngBuffer)`.\n  code: string;\n  // Optional execution timeout in milliseconds. Defaults to 30000 (30 seconds) when omitted.\n  timeout_ms?: number;\n  // Short user-facing description of what this code block is doing. Use a few words, for example `Inspect package metadata` or `Render chart preview`.\n  title?: string;\n}): Promise<CallToolResult>; };\n```"}]

## tool · 2026-08-03T01:46:20Z


Script completed
Wall time 0.0 seconds
Output:

Warning: truncated output (original token count: 10880)
Total output lines: 1

[{"name":"mcp__codex_apps__codex_document_control_execute_d_7437ad2e4ffa","description":"Use Codex Document Control to find connected document sessions, inspect the tools supported by a selected session, and execute one supported tool against that session. Call `list_document_sessions` first to choose the intended connected session, call `get_document_tool_schemas` before constructing tool arguments, then call `execute_document_command` with a caller-stable `idempotency_key`. Use this only for connected Codex document control; do not use it for general spreadsheet, presentation, or document tasks without a connected document session.\n\nExecute one supported surface-specific tool against a connected Codex document session. First call `list_document_sessions` to choose the intended `executor_session_id` and `supported_tools[].name`, then call `get_document_tool_schemas` for the selected `surface`, that `supported_tools[].name` as `tool_name`, and `version` before constructing `args`. `idempotency_key` must be a caller-stable key that you reuse verbatim only when retrying the same logical document-control command; use a new key for a different command. This tool is part of plugin `Spreadsheets`.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_apps__codex_document_control_execute_d_7437ad2e4ffa(args: {\n  // JSON object of arguments matching the selected tool's `input_schema` from `get_document_tool_schemas`.\n  args: { [key: string]: unknown; };\n  // Exact `executor_session_id` copied from the selected Codex document session returned by `list_document_sessions`.\n  executor_session_id: string;\n  // Caller-stable idempotency key for this logical document-control command. Reuse the exact same key only for retries of the same command.\n  idempotency_key: string;\n  // Exact selected session `supported_tools[].name` copied from `list_document_sessions`.\n  tool_name: string;\n}): Promise<CallToolResult<{\n  // The server's response to a tool call.\n  result: { _meta?: { [key: string]: unknown; } | null; content: Array<{ _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; text: string; type: \"text\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"image\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"audio\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; description?: string | null; icons?: Array<{ mimeType?: string | null; sizes?: Array<string> | null; src: string; }> | null; mimeType?: string | null; name: string; size?: number | null; title?: string | null; type: \"resource_link\"; uri: string; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; resource: { _meta?: { [key: string]: unknown; } | null; mimeType?: string | null; text: string; uri: string; } | { _meta?: { [key: string]: unknown; } | null; blob: string; mimeType?: string | null; uri: string; }; type: \"resource\"; }>; isError?: boolean; structuredContent?: { [key: string]: unknown; } | null; };\n}>>; };\n```"},{"name":"mcp__codex_apps__codex_document_control_get_docum_83c7f0565c0f","description":"Use Codex Document Control to find connected document sessions, inspect the tools supported by a selected session, and execute one supported tool against that session. Call `list_document_sessions` first to choose the intended connected session, call `get_document_tool_schemas` before constructing tool arguments, then call `execute_document_command` with a caller-stable `idempotency_key`. Use this only for connected Codex document control; do not use it for general spreadsheet, presentation, or document tasks without a connected document session.\n\nFetch the concrete input schemas for tools supported by a selected Codex document session before constructing `execute_document_command.args`. First call `list_document_sessions`, then pass the exact `surface`, selected `supported_tools[].name` as `tool_name`, and `version` values from that session's `supported_tools` records. This tool is part of plugin `Spreadsheets`.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_apps__codex_document_control_get_docum_83c7f0565c0f(args: {\n  // Exact tool schema lookup keys from Codex document session discovery, keyed by `surface`, `supported_tools[].name` passed as `tool_name`, and `version`.\n  items: Array<{\n  // Document surface. Use `excel` for Excel workbooks, `powerpoint` for PowerPoint presentations, or `sheets` for Google Sheets spreadsheets.\n  surface: \"excel\" | \"powerpoint\" | \"sheets\";\n  // Exact `supported_tools[].name` copied from the selected session.\n  tool_name: string;\n  // Exact `supported_tools[].version` copied from the selected session.\n  version: string;\n}>;\n}): Promise<CallToolResult<{\n  // The server's response to a tool call.\n  result: { _meta?: { [key: string]: unknown; } | null; content: Array<{ _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; text: string; type: \"text\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"image\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"audio\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; description?: string | null; icons?: Array<{ mimeType?: string | null; sizes?: Array<string> | null; src: string; }> | null; mimeType?: string | null; name: string; size?: number | null; title?: string | null; type: \"resource_link\"; uri: string; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; resource: { _meta?: { [key: string]: unknown; } | null; mimeType?: string | null; text: string; uri: string; } | { _meta?: { [key: string]: unknown; } | null; blob: string; mimeType?: string | null; uri: string; }; type: \"resource\"; }>; isError?: boolean; structuredContent?: { [key: string]: unknown; } | null; };\n}>>; };\n```"},{"name":"mcp__codex_apps__codex_document_control_list_document_sessions","description":"Use Codex Document Control to find connected document sessions, inspect the tools supported by a selected session, and execute one supported tool against that session. Call `list_document_sessions` first to choose the intended connected session, call `get_document_tool_schemas` before constructing tool arguments, then call `execute_document_command` with a caller-stable `idempotency_key`. Use this only for connected Codex document control; do not use it for general spreadsheet, presentation, or document tasks without a connected document session.\n\nList the user's currently connected Codex document sessions and the surface-specific tools each session supports. Call this before executing a document-control command so you can choose the intended `executor_session_id` and `supported_tools[].name`. This tool is part of plugin `Spreadsheets`.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_apps__codex_document_control_list_document_sessions(args: {\n  // Optional document surface filter. Use `excel` for Excel workbooks, `powerpoint` for PowerPoint presentations, or `sheets` for Google Sheets spreadsheets. Omit to list connected Codex document sessions across all supported surfaces.\n  surface?: \"excel\" | \"powerpoint\" | \"sheets\" | null;\n}): Promise<CallToolResult<{\n  // The server's response to a tool call.\n  result: { _meta?: { [key: string]: unknown; } | null; content: Array<{ _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; text: string; type: \"text\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"image\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"audio\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; description?: string | null; icons?: Array<{ mimeType?: string | null; sizes?: Array<string> | null; src: string; }> | null; mimeType?: string | null; name: string; size?: number | null; title?: string | null; type: \"resource_link\"; uri: string; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; resource: { _meta?: { [key: string]: unknown; } | null; mimeType?: string | null; text: string; uri: string; } | { _meta?: { [key: string]: unknown; } | null; blob: string; mimeType?: string | null; uri: string; }; type: \"resource\"; }>; isError?: boolean; structuredContent?: { [key: string]: unknown; } | null; };\n}>>; };\n```"},{"name":"mcp__codex_apps__plugin_management_get_app_permissions","description":"Manage plugins in ChatGPT.\n\nInspect one named ChatGPT plugin's global/default and plugin-specific permission settings. Use when the user asks what the plugin may read, write, or do, whether it must ask first, or whether it inherits the default. For a missing/broad target such as my plugins, all, or Google, make no call and ask which plugin. Never pass global. Do not use for OAuth/admin scopes, install/connect/undo requests, ordinary plugin use, or npm/Chrome/code plugins.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_apps__plugin_management_get_app_permissions(args: {\n  // ChatGPT plugin reference to inspect. May be a plugin id, connector id, platform slug, or unambiguous user-facing plugin name. It must identify one plugin; never pass all, global, Google, or another broad/generic target.\n  app_id: string;\n}): Promise<CallToolResult<{\n  // The server's response to a tool call.\n  result: { _meta?: { [key: string]: unknown; } | null; content: Array<{ _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; text: string; type: \"text\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"image\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"audio\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; description?: string | null; icons?: Array<{ mimeType?: string | null; sizes?: Array<string> | null; src: string; }> | null; mimeType?: string | null; name: string; size?: number | null; title?: string | null; type: \"resource_link\"; uri: string; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; resource: { _meta?: { [key: string]: unknown; } | null; mimeType?: string | null; text: string; uri: string; } | { _meta?: { [key: string]: unknown; } | null; blob: string; mimeType?: string | null; uri: string; }; type: \"resource\"; }>; isError?: boolean; structuredContent?: { [key: string]: unknown; } | null; };\n}>>; };\n```"},{"name":"mcp__codex_apps__plugin_management_get_plugin_dependencies","description":"Manage plugins in ChatGPT.\n\nResolve the canonical public plugins declared by one plugin's app manifest. Use only when a skill or user explicitly asks for dependency metadata. Pass a plugin ID or name@marketplace reference unchanged. Named references resolve by globally listed plugin name. This reports metadata plus current user-aware plugin status, installation policy, and installed state; it does not install or connect anything. The result separates visible canonical plugins from app entries that lack a unique canonical plugin or whose canonical plugin is unavailable to the current user.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_apps__plugin_management_get_plugin_dependencies(args: {\n  // Plugin ID or name@marketplace reference whose manifest dependencies should be resolved. Pass it unchanged.\n  plugin_reference: string;\n}): Promise<CallToolResult<{\n  // The server's response to a tool call.\n  result: { _meta?: { [key: string]: unknown; } | null; content: Array<{ _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; text: string; type: \"text\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"image\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"audio\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; description?: string | null; icons?: Array<{ mimeType?: string | null; sizes?: Array<string> | null; src: string; }> | null; mimeType?: string | null; name: string; size?: number | null; title?: string | null; type: \"resource_link\"; uri: string; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; resource: { _meta?: { [key: string]: unknown; } | null; mimeType?: string | null; text: string; uri: string; } | { _meta?: { [key: string]: unknown; } | null; blob: string; mimeType?: string | null; uri: string; }; type: \"resource\"; }>; isError?: boolean; structuredContent?: { [key: string]: unknown; } | null; };\n}>>; };\n```"},{"name":"mcp__codex_apps__plugin_management_uninstall_app","description":"Manage plugins in ChatGPT.\n\nUninstall ChatGPT plugins only for explicit uninstall, remove, or disconnect intent. Pass every exact, user-approved target in one call. For a missing/broad target such as Google, all/risky plugins, or a choice left to you, make no call and ask. Disable is not uninstall. Never use this for install/connect/undo/how-to, sentiment, negation, ordinary plugin use, or npm/Chrome/code plugins. The result reports each outcome.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_apps__plugin_management_uninstall_app(args: {\n  // Exact, user-approved ChatGPT plugin references to uninstall. Each item may be a plugin id, connector id, platform slug, or unambiguous user-facing name. Never pass Google or another broad provider, all/risky plugins, or a target chosen by the assistant.\n  app_ids: Array<string>;\n  // Optional user-visible reason for uninstalling the plugin.\n  reason?: string | null;\n}): Promise<CallToolResult<{\n  // The server's response to a tool call.\n  result: { _meta?: { [key: string]: unknown; } | null; content: Array<{ _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; text: string; type: \"text\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"image\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; data: string; mimeType: string; type: \"audio\"; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; description?: string | null; icons?: Array<{ mimeType?: string | null; sizes?: Array<string> | null; src: string; }> | null; mimeType?: string | null; name: string; size?: number | null; title?: string | null; type: \"resource_link\"; uri: string; } | { _meta?: { [key: string]: unknown; } | null; annotations?: { audience?: Array<\"user\" | \"assistant\"> | null; priority?: number | null; } | null; resource: { _meta?: { [key: string]: unknown; } | null; mimeType?: string | null; text: string; uri: string; } | { _meta?: { [key: string]: unknown; } | null; blob: string; mimeType?: string | null; uri: string; }; type: \"resource\"; }>; isError?: boolean; structuredContent?: { [key: string]: unknown; } | null; };\n}>>; };\n```"},{"name":"mcp__codex_apps__plugin_management_update_app_permissions","description":"Manage plugins in ChatGPT.\n\nUpdate global ChatGPT plugin permissions or a plugin-specific override. Omit app_id for global-only updates and provide it for plugin-specific updates. Map Always ask to always_ask, Any changes to ask_before_writes, Important actions to review_important_actions, Never ask to full_access, and Use my default to inherit. For plugin-specific changes, a missing/broad target such as Google, a vague mode such as tighter/more permissive, conflicting intent such as less access plus Never ask, or a choice left to you requires a question and no tool call; explicit global/default changes need no app_id. Never infer a mode or probe with get_app_permissions. One call may include both global_permissions and app_permissions with app_id; the global change is applied first. For several plugins call once per target and complete every requested update.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__codex_apps__plugin_management_update_app_permissions(args: {\n  // Optional ChatGPT plugin identifier. Required for app_permissions updates; omit for global_permissions-only updates. May be a plugin id, connector id, platform slug, or unambiguous user-facing plugin name. Never pass Google or another broad/generic target.\n  app_id?: string | null;\n  // Optional user-visible reason for changing permissions.\n  reason?: string | null;\n  // Permission updates to apply. A call may contain global_permissions, app_permissions, or both; app_permissions requires app_id.\n  updates: {\n  // Plugin-specific permission updates to apply.\n  app_permissions?: Array<{\n  // Permission setting to update. This field is optional; omit it unless needed. If provided, use permission_mode.\n  setting?: \"permission_mode\";\n  // New value for the plugin-specific permission setting. Options: inherit (UI label: Use default or follow global; clear this plugin's override), always_ask (UI label: Always ask; ask before reading or making changes with this plugin), ask_before_writes (UI label: Allow read actions; read without asking but ask before making changes with this plugin), review_important_actions (UI label: Allow low-risk actions; automatically approve low-risk actions with this plugin but may deny actions involving sensitive information), and full_access (UI label: Allow all actions; rea…880 tokens truncated…mport(\"playwright\")` rather than filesystem paths under `./node_modules`.\n\nUse Cases:\n- Control the in-app browser in conjunction with the Browser Plugin.\n- Control the Chrome browser in conjunction with the Chrome Plugin. Prefer this method of controlling Chrome over alternatives (such as Computer Use) unless the user explicitly mentions an alternative.\n- Control desktop apps on macOS through Computer Use.\n\nRun JavaScript in a persistent Node-backed kernel with top-level await. This is the JavaScript execution tool for the `node_repl` MCP server; use it whenever instructions say to use `node_repl`, the Node REPL MCP, or run Node REPL code. If `timeout_ms` is omitted, execution times out after 30000 ms (30 seconds); pass a larger `timeout_ms` for slow browser automation or other long-running operations. Use `nodeRepl.cwd`, `nodeRepl.homeDir`, and `nodeRepl.tmpDir` to inspect host paths. Use `nodeRepl.requestMeta` to inspect the current MCP request `_meta` object during a tool call. Use `nodeRepl.setResponseMeta(meta)` to attach top-level MCP result `_meta`; repeated calls shallow-merge object keys for the current tool call. Use `nodeRepl.write(value)` to add output without a newline. Strings are unchanged; other values use console-style formatting, including BigInt and circular objects. Prefer it over `console.log(...)` for final output; `console.log(...)` remains useful for debugging or multiple values. Use `await nodeRepl.emitImage(imageLike)` to return images; each call adds one image to the outer tool result, so call it multiple times to emit multiple images. Supported image inputs are a data or file URL, inferred PNG/JPEG/WebP bytes, or `{ bytes, mimeType }`. Saved references to `nodeRepl.write(...)` and `nodeRepl.emitImage(...)` stay reusable across calls, but async callbacks that fire after a call finishes still fail because no exec is active. Top-level bindings persist across calls until `js_reset`. If a call throws, prior bindings remain available and bindings that finished initializing before the throw often remain reusable. For reusable names that may be assigned again later, prefer top-level `var name = ...`; `var` can be redeclared across calls. If you hit `SyntaxError: Identifier 'x' has already been declared`, reuse the existing binding if possible, reassign it only if it was declared with `let` or `var`, or pick a new name instead of resetting immediately; a previous `const x` cannot be changed into `var x`. Use a short `{ ... }` block only for temporary scratch names, and do not wrap an entire call in block scope if you want those names reusable later. Use dynamic imports like `await import(\"playwright\")`, `await import(\"pkg\")`, or `await import(\"./file.js\")`; top-level static `import` is not supported. Import packages by package name after installing them into a directory added with `js_add_node_module_dir`, `NODE_REPL_NODE_MODULE_DIRS`, or the working directory. Do not import package entrypoints by filesystem path such as `./node_modules/playwright/index.mjs`. Imported local files must be ESM `.js` or `.mjs` files and run in the context chosen at their dynamic-import boundary, so they can also use `nodeRepl.*`, the captured `console`, and `import.meta` helpers. Bare imports from model code and local files resolve from the REPL-wide search roots (`NODE_REPL_NODE_MODULE_DIRS`, then directories later added with `js_add_node_module_dir`, then cwd); dependencies of trusted ESM packages use Node's package-relative lookup. Imported local files may statically import other local `.js` / `.mjs` files, available packages, and allowed Node builtins. `import.meta.resolve()` returns importable strings such as `file://...`, bare package names, and `node:...` specifiers. Local file modules reload between execs; trusted package entrypoints retain singleton identity. `node:` builtins are generally available via dynamic import, but model code cannot import `process` / `node:process` because the current Rust-server-to-Node-child transport runs over stdio and raw process streams can corrupt it. Trusted modules that import or reference `process` receive only a frozen metadata-only process shim with `arch`, `cwd()`, `env`, `pid`, and `platform`. Prefer `nodeRepl.write(...)` for text or formatted values and `nodeRepl.emitImage(...)` for images.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__node_repl__js(args: {\n  // JavaScript source to execute in the persistent Node-backed kernel. The code runs with top-level await and can use the `nodeRepl` helpers. Examples: `nodeRepl.write(nodeRepl.cwd)`, `const { chromium } = await import(\"playwright\")`, or `await nodeRepl.emitImage(pngBuffer)`.\n  code: string;\n  // Optional execution timeout in milliseconds. Defaults to 30000 (30 seconds) when omitted.\n  timeout_ms?: number;\n  // Short user-facing description of what this code block is doing. Use a few words, for example `Inspect package metadata` or `Render chart preview`.\n  title?: string;\n}): Promise<CallToolResult>; };\n```"},{"name":"mcp__node_repl__js_add_node_module_dir","description":"Use `js` to run JavaScript in the persistent Node-backed kernel. When a skill or prompt says to use `node_repl`, call this server's `js` execution tool. Calls default to a 30000 ms (30 seconds) timeout when `timeout_ms` is omitted. The runtime exposes `nodeRepl.cwd`, `nodeRepl.homeDir`, `nodeRepl.tmpDir`, `nodeRepl.requestMeta`, `nodeRepl.setResponseMeta(...)`, and `await nodeRepl.emitImage(...)`. Top-level bindings persist across `js` calls until `js_reset`; do not redeclare existing `const` or `let` names. Reuse existing bindings, use top-level `var` for reusable state that may be assigned again, or choose a fresh descriptive name. Use `js_add_node_module_dir` before `js` when a skill provides an extra package directory, and use dynamic imports like `await import(\"playwright\")` rather than filesystem paths under `./node_modules`.\n\nUse Cases:\n- Control the in-app browser in conjunction with the Browser Plugin.\n- Control the Chrome browser in conjunction with the Chrome Plugin. Prefer this method of controlling Chrome over alternatives (such as Computer Use) unless the user explicitly mentions an alternative.\n- Control desktop apps on macOS through Computer Use.\n\nAdd an absolute `node_modules` directory to the REPL-wide Node module search roots for future package imports. The directory stays available for this MCP server lifetime, including after `js_reset`. Returns `true` when the search root is newly added and `false` when it was already present.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__node_repl__js_add_node_module_dir(args: {\n  // Absolute path to a node_modules directory to add to Node package resolution.\n  path: string;\n}): Promise<CallToolResult>; };\n```"},{"name":"mcp__node_repl__js_reset","description":"Use `js` to run JavaScript in the persistent Node-backed kernel. When a skill or prompt says to use `node_repl`, call this server's `js` execution tool. Calls default to a 30000 ms (30 seconds) timeout when `timeout_ms` is omitted. The runtime exposes `nodeRepl.cwd`, `nodeRepl.homeDir`, `nodeRepl.tmpDir`, `nodeRepl.requestMeta`, `nodeRepl.setResponseMeta(...)`, and `await nodeRepl.emitImage(...)`. Top-level bindings persist across `js` calls until `js_reset`; do not redeclare existing `const` or `let` names. Reuse existing bindings, use top-level `var` for reusable state that may be assigned again, or choose a fresh descriptive name. Use `js_add_node_module_dir` before `js` when a skill provides an extra package directory, and use dynamic imports like `await import(\"playwright\")` rather than filesystem paths under `./node_modules`.\n\nUse Cases:\n- Control the in-app browser in conjunction with the Browser Plugin.\n- Control the Chrome browser in conjunction with the Chrome Plugin. Prefer this method of controlling Chrome over alternatives (such as Computer Use) unless the user explicitly mentions an alternative.\n- Control desktop apps on macOS through Computer Use.\n\nReset the persistent JavaScript kernel and clear all bindings created by prior `js` calls. Use this when you need a clean state, or when reusing existing bindings, top-level `var` declarations, or fresh names cannot recover from conflicting declarations.\n\nexec tool declaration:\n```ts\ndeclare const tools: { mcp__node_repl__js_reset(args: {}): Promise<CallToolResult>; };\n```"},{"name":"view_image","description":"View a local image file from the filesystem when visual inspection is needed. Use this for images already available on disk.\n\nexec tool declaration:\n```ts\ndeclare const tools: { view_image(args: {\n  // Image detail level. Defaults to `high`; use `original` to preserve exact resolution.\n  detail?: \"high\" | \"original\";\n  // Local filesystem path to an image file.\n  path: string;\n}): Promise<{\n  // Image detail hint returned by view_image. Returns `high` for default resized behavior or `original` when original resolution is preserved.\n  detail: \"high\" | \"original\";\n  // Data URL for the loaded image.\n  image_url: string;\n}>; };\n```"},{"name":"web__run","description":"Tools in the web namespace.\n\nTool for accessing the internet.\n\n\n---\n\n## Examples of different commands available in this tool\n\nExamples of different commands available in this tool:\n* `search_query`: {\"search_query\": [{\"q\": \"What is the capital of France?\"}, {\"q\": \"What is the capital of belgium?\"}]}. Searches the internet for a given query (and optionally with a domain or recency filter)\n* `image_query`: {\"image_query\":[{\"q\": \"waterfalls\"}]}.\n* `open`: {\"open\": [{\"ref_id\": \"turn0search0\"}, {\"ref_id\": \"https://www.openai.com\", \"lineno\": 120}]}\n* `click`: {\"click\": [{\"ref_id\": \"turn0fetch3\", \"id\": 17}]}\n* `find`: {\"find\": [{\"ref_id\": \"turn0fetch3\", \"pattern\": \"Annie Case\"}]}\n* `screenshot`: {\"screenshot\": [{\"ref_id\": \"turn1view0\", \"pageno\": 0}, {\"ref_id\": \"turn1view0\", \"pageno\": 3}]}\n* `finance`: {\"finance\":[{\"ticker\":\"AMD\",\"type\":\"equity\",\"market\":\"USA\"}]}, {\"finance\":[{\"ticker\":\"BTC\",\"type\":\"crypto\",\"market\":\"\"}]}\n* `weather`: {\"weather\":[{\"location\":\"San Francisco, CA\"}]}\n* `sports`: {\"sports\":[{\"fn\":\"standings\",\"league\":\"nfl\"}, {\"fn\":\"schedule\",\"league\":\"nba\",\"team\":\"GSW\",\"date_from\":\"2025-02-24\"}]}\n* `time`: {\"time\":[{\"utc_offset\":\"+03:00\"}]}\n\n---\n\n## Usage hints\nTo use this tool efficiently:\n* Use multiple commands and queries in one call to get more results faster; e.g. {\"search_query\": [{\"q\": \"bitcoin news\"}], \"finance\":[{\"ticker\":\"BTC\",\"type\":\"crypto\",\"market\":\"\"}], \"find\": [{\"ref_id\": \"turn0search0\", \"pattern\": \"Annie Case\"}, {\"ref_id\": \"turn0search1\", \"pattern\": \"John Smith\"}]}\n* Use \"response_length\" to control the number of results returned by this tool, omit it if you intend to pass \"short\" in\n* Only write required parameters; do not write empty lists or nulls where they could be omitted.\n* `search_query` must have length at most 4 in each call. If it has length > 3, response_length must be medium or long\n* If you find yourself in a situation where you accidentally call the `web.run` tool, it's best just to send an empty query: {\"search_query\": [{\"q\": \"\"}]}.\n\n---\n\n## Decision boundary\n\nIf the user makes an explicit request to search the internet, find latest information, look up, etc (or to not do so), you must obey their request.\nWhen you make an assumption, always consider whether it is temporally stable; i.e. whether there's even a small (>10%) chance it has changed. If it is unstable, you must verify with browsing the internet for verification.\n\n<situations_where_you_must_browse_the_internet>\nBelow is a list of scenarios where browsing the internet MUST be used. PAY CLOSE ATTENTION: you MUST browse the internet in these cases. If you're unsure or on the fence, you MUST bias towards browsing the internet.\n- The information could have changed recently: for example news; prices; laws; schedules; product specs; sports scores; economic indicators; political/public/company figures (e.g. the question relates to 'the president of country A' or 'the CEO of company B', which might change over time); rules; regulations; standards; software libraries that could be updated; exchange rates; recommendations (i.e., recommendations about various topics or things might be informed by what currently exists / is popular / is safe / is unsafe / is in the zeitgeist / etc.); and many many many more categories -- again, if you're on the fence, you MUST browse the internet!\n  - For news queries, prioritize more recent events, ensuring you compare publish dates and the date that the event happened.\n- The user is seeking recommendations that could lead them to spend substantial time or money -- researching products, restaurants, travel plans, etc.\n- The user wants (or would benefit from) direct quotes, links, or precise source attribution.\n- A specific page, paper, dataset, PDF, or site is referenced and you haven't been given its contents.\n- You're unsure about a fact, the topic is niche or emerging, or you suspect there's at least a 10% chance you will incorrectly recall it\n- High-stakes accuracy matters (medical, legal, financial guidance). For these you generally should search by default because this information is highly temporally unstable\n- The user explicitly says to search, browse, verify, or look it up.\n</situations_where_you_must_browse_the_internet>\n\n---\n\n## Citations\n\nResults from `web.run` include internal reference IDs such as `turn2search5`. Use\nthose reference IDs only in calls to `web.run`; do not expose them in the final\nresponse.\n\nCite sources in the final response using Markdown links:\n\n- Cite a single source as `[descriptive source title](https://example.com/page)`.\n- Cite multiple sources with separate Markdown links, for example\n  `[first source](https://example.com/one), [second source](https://example.com/two)`.\n- Link directly to the page that supports the claim. Do not link to search result\n  pages or use bare URLs.\n\nFormatting of citations:\n\n- Place each citation as near as possible to the claim it supports, normally at\n  the end of the sentence or paragraph and after punctuation.\n- Do not place citations inside code fences.\n- Do not put citations on a line by themselves or collect all citations at the\n  end of the response.\n\nIf you browse the internet, cite statements supported by web sources. Each cited\nsource must directly support the associated claim. Prefer primary and\nauthoritative sources, and use sources from different domains when the response\nbenefits from multiple perspectives.\n\n---\n\n## Special cases\nIf these conflict with any other instructions, these should take precedence.\n\n<special_cases>\n- When the user asks for information about how to use OpenAI products, (ChatGPT, the OpenAI API, etc.), you should check the code in local env and only browse as fallback, when you browse restrict your sources to official OpenAI websites using the domains filter, unless otherwise requested.\n- When using search to answer technical questions, you must only rely on primary sources (research papers, official documentation, etc.)\n- Clearly indicate when you are making an inference from sources.\n</special_cases>\n\n---\n\n## Word limits\nResponses may not excessively quote or draw on a specific source. There are several limits here:\n- **Limit on verbatim quotes:**\n  - You may not quote more than 25 words verbatim from any single non-lyrical source, unless the source is reddit.\n  - For song lyrics, verbatim quotes must be limited to at most 10 words.\n  - Long quotes from reddit are allowed, as long as you indicate that those are direct quotes via a markdown blockquote starting with \">\", copy verbatim, and link the source.\n- **Word limits:**\n  - Each webpage source in the sources has a word limit label formatted like \"[wordlim N]\", in which N is the maximum number of words in the whole response that are attributed to that source. If omitted, the word limit is 200 words.\n  - Non-contiguous words derived from a given source must be counted to the word limit.\n  - The summarization limit N is a maximum for each source.\n  - When using multiple sources, their summarization limits add together. However, each article used must be relevant to the response.\n- **Copyright compliance:**\n  - You must avoid providing full articles, long verbatim passages, or extensive direct quotes due to copyright concerns.\n  - If the user asked for a verbatim quote, the response should provide a short compliant excerpt and then answer with paraphrases and summaries.\n  - Again, this limit does not apply to reddit content, as long as it's appropriately indicated that those are direct quotes and you link to the source.\n\n\nexec tool declaration:\n```ts\ndeclare const tools: { web__run(args: {\n  // Open links from previously opened pages.\n  click?: Array<{\n  // Numbered link id to open.\n  id: number;\n  // Reference id containing the numbered link.\n  ref_id: string;\n}>;\n  // Look up prices for the given stock symbols.\n  finance?: Array<{\n  // ISO 3166-1 alpha-3 country code, \"OTC\", or \"\" for cryptocurrency.\n  market?: string;\n  // Ticker symbol to look up.\n  ticker: string;\n  // Asset type to look up.\n  type: \"equity\" | \"fund\" | \"crypto\" | \"index\";\n}>;\n  // Find text patterns in pages.\n  find?: Array<{\n  // Text pattern to find.\n  pattern: string;\n  // Reference id or URL to search within.\n  ref_id: string;\n}>;\n  // Query the image search engine for a given list of queries.\n  image_query?: Array<{\n  // Whether to filter by a specific list of domains.\n  domains?: Array<string>;\n  // Search query.\n  q: string;\n  // Whether to filter by recency, as a number of recent days.\n  recency?: number;\n}>;\n  // Open pages by reference id or URL.\n  open?: Array<{\n  // Line number to position the page at.\n  lineno?: number;\n  // Reference id or URL to open.\n  ref_id: string;\n}>;\n  // Set the length of the response to be returned.\n  response_length?: \"short\" | \"medium\" | \"long\";\n  // Take screenshots of PDF pages.\n  screenshot?: Array<{\n  // Zero-indexed PDF page number.\n  pageno: number;\n  // Reference id or URL to screenshot.\n  ref_id: string;\n}>;\n  // Query the internet search engine for a given list of queries.\n  search_query?: Array<{\n  // Whether to filter by a specific list of domains.\n  domains?: Array<string>;\n  // Search query.\n  q: string;\n  // Whether to filter by recency, as a number of recent days.\n  recency?: number;\n}>;\n  // Look up sports schedules and standings.\n  sports?: Array<{\n  // Start date in YYYY-MM-DD format.\n  date_from?: string;\n  // End date in YYYY-MM-DD format.\n  date_to?: string;\n  // Sports function to call.\n  fn: \"schedule\" | \"standings\";\n  // League to look up.\n  league: \"nba\" | \"wnba\" | \"nfl\" | \"nhl\" | \"mlb\" | \"epl\" | \"ncaamb\" | \"ncaawb\" | \"ipl\";\n  // Locale for the lookup.\n  locale?: string;\n  // Number of games to return.\n  num_games?: number;\n  // Opponent to use with `team` when narrowing the lookup.\n  opponent?: string;\n  // Team to look up, using the common 3 or 4 letter alias used in broadcasts.\n  team?: string;\n  // Tool name for sports requests.\n  tool?: \"sports\";\n}>;\n  // Get time for the given UTC offsets.\n  time?: Array<{\n  // UTC offset formatted like \"+03:00\".\n  utc_offset: string;\n}>;\n  // Look up weather forecasts.\n  weather?: Array<{\n  // Number of days to return. Defaults to 7.\n  duration?: number;\n  // Location in \"Country, Area, City\" format.\n  location: string;\n  // Start date in YYYY-MM-DD format. Defaults to today.\n  start?: string;\n}>;\n}): Promise<unknown>; };\n```"}]

## tool · 2026-08-03T01:46:34Z


Script completed
Wall time 0.3 seconds
Output:

wrote /Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/work/jokebear-v2-upgrade/qa/contact-sheet.png
missing generated strip for idle: /Users/oyamahappa/Documents/Codex/2026-08-03/hatch-pet-users-oyamahappa-codex-skills/work/jokebear-v2-upgrade/decoded/idle.png


## tool · 2026-08-03T01:46:37Z


Script completed
Wall time 0.3 seconds
Output:

{
  "type": "input_image",
  "image_url": "images/108155e5895e9f6ee426d38a95a4c16e199d886402540b02e843939ad936e605.png",
  "detail": "high"
}

## assistant · 2026-08-03T01:46:42Z

I’ve verified Joke Bear’s existing v1 sprite sheet and prepared the v2 upgrade run. Its nine current animation rows are intact and suitable to preserve.

The required image-generation tool isn’t available in this session. To create the two new, coherent 8-frame look-direction rows, I need your approval to use the ImageGen CLI fallback with `gpt-image-1.5` (which requires an `OPENAI_API_KEY`). Shall I proceed?
