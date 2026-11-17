# 工作目录：/Users/oyamahappa/Documen

来源：dsh

项目：/Users/oyamahappa/Documents/Agent/DSH

## user · 2026-10-05T10:50:38Z


工作目录：/Users/oyamahappa/Documents/Agent/DSH
教程根目录：AI-Coding-Guide-Zh/

任务：阅读指定教程文件，抽取内容，写出一份**PPT 内容 JSON** 文件，供后续用 python-pptx 生成幻灯片。
面向对象：**完全新手 / 办公人**——没有编程基础，怕命令行。要少命令、多概念、多类比、能看懂能上手。
语言：简体中文。

硬性要求：
1. 内容必须来自指定教程文件，不得编造。数字、版本号、命令、功能名称要忠于原文。
2. 每张幻灯片要点不超过 5 条，每条不超过 42 个汉字。表格不超过 5 列、6 行。
3. 生成 15-18 张幻灯片，结构：封面(cover) → 目录或分节(section) → 内容 → 结尾(end)。
4. 用适合新手的类比解释术语（例如 MCP 比作 USB 接口）。
5. 用 write 工具把 JSON 写入指定输出路径（UTF-8，不要加 markdown 代码围栏）。

JSON schema（严格遵守，字段可按 layout 取舍）：
{
  "deck": "幻灯片标题",
  "slides": [
    {"layout":"cover","title":"...","subtitle":"...","kicker":"Vibe Coding 学习系列 · 0X"},
    {"layout":"section","title":"...","subtitle":"..."},
    {"layout":"bullets","title":"...","bullets":["...","..."],"notes":"讲稿提示(可省略)"},
    {"layout":"cards","title":"...","cards":[{"title":"...","desc":"..."}]},
    {"layout":"table","title":"...","headers":["..."],"rows":[["..."]]},
    {"layout":"steps","title":"...","steps":[{"title":"...","desc":"..."}]},
    {"layout":"quote","title":"...","subtitle":"..."},
    {"layout":"end","title":"...","subtitle":"..."}
  ]
}
cards 用 3-4 张，steps 用 3-4 步，table 用于对比。

本次负责：**办公助手主线**（第 04 册），包含 OpenClaw 与 WorkBuddy 两个工具。
阅读这些文件（按需分段读取，这两个工具文档很多，只读列出的）：
- AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md
- AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md
- AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md
- AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md
- AI-Coding-Guide-Zh/docs/workbuddy/WB-00-阅读指南.md
- AI-Coding-Guide-Zh/docs/workbuddy/WB-01-WorkBuddy项目介绍完整指南.md
- AI-Coding-Guide-Zh/docs/workbuddy/WB-02-WorkBuddy安装与登录完整指南.md
- AI-Coding-Guide-Zh/docs/workbuddy/WB-03-WorkBuddy专家与专家团完整指南.md
- AI-Coding-Guide-Zh/docs/workbuddy/WB-05-WorkBuddy连接器与腾讯生态完整指南.md
- AI-Coding-Guide-Zh/docs/workbuddy/WB-07-WorkBuddy自动化与计划任务完整指南.md
- AI-Coding-Guide-Zh/docs/workbuddy/WB-10-WorkBuddy企业账号安全与对比完整指南.md

幻灯片建议覆盖：两条办公助手主线怎么选、OpenClaw 是什么(开源 AI 私人助手，接到消息平台)、OpenClaw 环境与第一个对话、模型配置要点、消息平台接入、技能与记忆、安全注意、WorkBuddy 是什么(腾讯 AI 办公助手，扫码即用)、安装登录、专家与专家团、技能市场、连接器与腾讯生态(腾讯文档/会议/企业微信)、知识库、自动化与定时任务、多端协同、选型建议与安全边界。
输出文件：vibe-coding-ppt/content/04-office-assistant.json
Your parent agent id is "session-0de88cee-855e-47e3-a7d8-5cedfd0973a3". Before you finish, send your result to that agent with send_message({ agent_id: "session-0de88cee-855e-47e3-a7d8-5cedfd0973a3", message: "<self-contained result>" }). The parent shares your workspace but does not automatically receive your transcript, tool output, or reasoning. Send earlier messages as well when a finding changes what the parent should do next; sending a message does not end your turn.

## assistant · 2026-10-05T10:50:42Z

Let me start by reading the tutorial files. I'll read them in parallel using the read tool via run_code. Let me first check the files exist and their sizes.

Let me plan: read the 11 files, extract content, write JSON. Let me read them.

I'll use run_code to call tools.read for multiple files. But output curation — reading full files may be huge. Let me first list files with sizes via bash.

Let me do that.
{
  "type": "tool-call",
  "id": "call_00_fg4zIyOnTGjMTVqQ06Bp2587",
  "name": "run_code",
  "arguments": "{\"code\": \"const files = [\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-00-阅读指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-01-WorkBuddy项目介绍完整指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-02-WorkBuddy安装与登录完整指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-03-WorkBuddy专家与专家团完整指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-05-WorkBuddy连接器与腾讯生态完整指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-07-WorkBuddy自动化与计划任务完整指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-10-WorkBuddy企业账号安全与对比完整指南.md\\\",\\n];\\nconst res = await tools.bash({ command: files.map(f => `wc -l \\\"${f}\\\"`).join(\\\"; \\\"), description: \\\"Show line counts of tutorial files\\\" });\\nreturn res.kind === \\\"foreground\\\" ? res.stdout.text : JSON.stringify(res);\", \"description\": \"Count lines in the 11 tutorial files\"}"
}

## tool · 2026-10-05T10:50:42Z

run_code
{"code": "const files = [\n\"AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\",\n\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\",\n\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\",\n\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\",\n\"AI-Coding-Guide-Zh/docs/workbuddy/WB-00-阅读指南.md\",\n\"AI-Coding-Guide-Zh/docs/workbuddy/WB-01-WorkBuddy项目介绍完整指南.md\",\n\"AI-Coding-Guide-Zh/docs/workbuddy/WB-02-WorkBuddy安装与登录完整指南.md\",\n\"AI-Coding-Guide-Zh/docs/workbuddy/WB-03-WorkBuddy专家与专家团完整指南.md\",\n\"AI-Coding-Guide-Zh/docs/workbuddy/WB-05-WorkBuddy连接器与腾讯生态完整指南.md\",\n\"AI-Coding-Guide-Zh/docs/workbuddy/WB-07-WorkBuddy自动化与计划任务完整指南.md\",\n\"AI-Coding-Guide-Zh/docs/workbuddy/WB-10-WorkBuddy企业账号安全与对比完整指南.md\",\n];\nconst res = await tools.bash({ command: files.map(f => `wc -l \"${f}\"`).join(\"; \"), description: \"Show line counts of tutorial files\" });\nreturn res.kind === \"foreground\" ? res.stdout.text : JSON.stringify(res);", "description": "Count lines in the 11 tutorial files"}

## assistant · 2026-10-05T10:50:49Z

Total ~9250 lines. That's a lot but manageable. I should delegate reading to subagents? Actually I'm a subagent myself; I have tools. Let me read strategically. The task says read specified files, only listed ones. I need enough content.

Let me read them in chunks. I'll read the smaller workbuddy files fully, and openclaw files with limits. But content must be faithful. Let me read the workbuddy files first (full), then openclaw guides.

Actually to conserve context, I could dispatch subagents to summarize each tool's docs. But the risk of fabrication... I'll read directly but curate: return only useful extracted text. The read tool returns line-numbered content; via run_code I can process and print trimmed excerpts. But I need to actually see the content to write the JSON. Let me read files and print them, possibly stripping. Total 9000 lines * ~50 chars = 450k chars too much for context maybe. Let me be selective: read key sections.

Alternative: delegate to two subagents (one per tool) that read and return structured summaries with exact numbers. That saves my context. But subagent output may lose detail. The requirement is I produce JSON. I think I can read most of it directly but selectively — say ~2500 lines total across openclaw (intro, quickstart key parts, security key parts) and full workbuddy files (~2600 lines). That's ~5100 lines. Hmm.

Better: use subagents to extract. I am a subagent with subagent tool available. Let me dispatch two subagent tasks in background: one for OpenClaw docs → structured extraction, one for WorkBuddy docs → structured extraction. They run in background; meanwhile I read the workbuddy WB files myself to verify. Actually parallel work: I'll read the workbuddy ones myself (they're smaller, total ~2600 lines) and dispatch a subagent for openclaw (~6600 lines). That balances.

Actually the parent instruction says start independent subagent delegations together. Let me dispatch one subagent for openclaw extraction with precise instructions, and simultaneously read workbuddy files myself.

Let me do that. But note subagent runs in background and I get notified. Meanwhile read workbuddy.

Let me set up todos too. Maybe not necessary but good.

Let me first dispatch the subagent and read the workbuddy files in the same turn? run_code is a single tool; I can only call run_code. Inside run_code I can call tools.subagent and tools.read in parallel via Promise.all. But tools.read results are large; and subagent returns continuable id. Let me do:

- run_code: call tools.subagent({description, prompt, run_in_background:true}) to get subagentId, and return it.

Then separate run_code calls to read workbuddy files.

Actually I could do subagent + reads in one program, printing read contents. But subagent is background so returns immediately. Let me combine: dispatch subagent and read the 4 small workbuddy files? Let's just do reads separately with curation.

Let me start.
{
  "type": "tool-call",
  "id": "call_00_oZa8ZmGOp5XkML4qbw6S6473",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.subagent({\\n  description: \\\"Extract OpenClaw docs\\\",\\n  run_in_background: false,\\n  prompt: `你是一名内容抽取员，只做事实抽取，不做创作。工作目录 /Users/oyamahappa/Documents/Agent/DSH。\\n\\n请完整阅读以下 4 个 Markdown 文件（可分段读取，务必读完整）：\\n- AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\\n- AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\\n- AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\\n- AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\\n\\n目标：为一套面向\\\"完全新手/办公人\\\"的中文 PPT 抽取素材。请输出结构化 Markdown，包含以下小节，每条都附上原文中的确切名称、数字、版本号、命令原文（不要改写命令）：\\n1. OpenClaw 是什么：一句话定位、核心特点（3-6 条）、和普通聊天机器人的区别、支持的接入方式（消息平台/客户端名称）。\\n2. 系统与环境要求：操作系统、Node.js 版本等具体版本号、硬件要求、安装方式名称。\\n3. 第一次运行/快速开始流程：要执行的命令原文、配置文件路径、第一个对话怎么发起、常用命令。\\n4. 模型配置：支持哪些模型提供方（如 Anthropic/OpenAI/OpenRouter/本地模型等确切名称）、API Key 配置方式、具体配置项名称、环境变量名。\\n5. 消息平台接入：支持哪些平台（Telegram/Discord/WhatsApp/Slack/iMessage 等确切名称）、接入步骤要点、配对/授权方式。\\n6. 技能与记忆：技能（Skills）是什么、如何安装/启用、记忆机制的术语与存储位置、是否有 ClawHub 之类的市场。\\n7. 安全注意：官方给出的风险与防护建议（列举确切条目）、权限/沙箱/审批相关术语、密钥保护建议。\\n8. 适合人群与限制（原文提到的）。\\n\\n要求：忠实原文，不编造。若某节原文没有，写\\\"原文未提及\\\"。输出控制在 2500 字以内，保留关键数字与专有名词。`,\\n});\\nreturn JSON.stringify(r).slice(0, 500);\", \"description\": \"Dispatch subagent to extract OpenClaw docs\"}"
}

## tool · 2026-10-05T10:50:49Z

run_code
{"code": "const r = await tools.subagent({\n  description: \"Extract OpenClaw docs\",\n  run_in_background: false,\n  prompt: `你是一名内容抽取员，只做事实抽取，不做创作。工作目录 /Users/oyamahappa/Documents/Agent/DSH。\n\n请完整阅读以下 4 个 Markdown 文件（可分段读取，务必读完整）：\n- AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\n- AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\n- AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\n- AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\n\n目标：为一套面向\"完全新手/办公人\"的中文 PPT 抽取素材。请输出结构化 Markdown，包含以下小节，每条都附上原文中的确切名称、数字、版本号、命令原文（不要改写命令）：\n1. OpenClaw 是什么：一句话定位、核心特点（3-6 条）、和普通聊天机器人的区别、支持的接入方式（消息平台/客户端名称）。\n2. 系统与环境要求：操作系统、Node.js 版本等具体版本号、硬件要求、安装方式名称。\n3. 第一次运行/快速开始流程：要执行的命令原文、配置文件路径、第一个对话怎么发起、常用命令。\n4. 模型配置：支持哪些模型提供方（如 Anthropic/OpenAI/OpenRouter/本地模型等确切名称）、API Key 配置方式、具体配置项名称、环境变量名。\n5. 消息平台接入：支持哪些平台（Telegram/Discord/WhatsApp/Slack/iMessage 等确切名称）、接入步骤要点、配对/授权方式。\n6. 技能与记忆：技能（Skills）是什么、如何安装/启用、记忆机制的术语与存储位置、是否有 ClawHub 之类的市场。\n7. 安全注意：官方给出的风险与防护建议（列举确切条目）、权限/沙箱/审批相关术语、密钥保护建议。\n8. 适合人群与限制（原文提到的）。\n\n要求：忠实原文，不编造。若某节原文没有，写\"原文未提及\"。输出控制在 2500 字以内，保留关键数字与专有名词。`,\n});\nreturn JSON.stringify(r).slice(0, 500);", "description": "Dispatch subagent to extract OpenClaw docs"}

## assistant · 2026-10-05T10:50:52Z

No subagents. I must read myself. Let me read strategically. I'll read the workbuddy files fully first (they're small), then openclaw with targeted reads.

Let me read WB-00 (133 lines) and WB-01 (371) together.
{
  "type": "tool-call",
  "id": "call_00_qt9aXQC6WHmh1rvpKncL5088",
  "name": "run_code",
  "arguments": "{\"code\": \"const out: string[] = [];\\nfor (const f of [\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-00-阅读指南.md\\\",\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-01-WorkBuddy项目介绍完整指南.md\\\"]) {\\n  const r = await tools.read({ file_path: f });\\n  out.push(\\\"=== \\\" + f + \\\" (\\\" + r.totalLines + \\\" lines) ===\\\");\\n  out.push(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\\n}\\nconsole.log(out.join(\\\"\\\\n\\\"));\", \"description\": \"Read WorkBuddy guide and intro docs\"}"
}

## tool · 2026-10-05T10:50:52Z

run_code
{"code": "const out: string[] = [];\nfor (const f of [\"AI-Coding-Guide-Zh/docs/workbuddy/WB-00-阅读指南.md\",\"AI-Coding-Guide-Zh/docs/workbuddy/WB-01-WorkBuddy项目介绍完整指南.md\"]) {\n  const r = await tools.read({ file_path: f });\n  out.push(\"=== \" + f + \" (\" + r.totalLines + \" lines) ===\");\n  out.push(r.lines.map(l => l.text).join(\"\\n\"));\n}\nconsole.log(out.join(\"\\n\"));", "description": "Read WorkBuddy guide and intro docs"}

## assistant · 2026-10-05T10:50:55Z

Now read WB-02, WB-03, WB-05, WB-07, WB-10. That's ~2100 lines. Let me read them in two batches. Maybe I can read them and print full — that's a lot of context but okay. Let me read WB-02 and WB-03 first.
{
  "type": "tool-call",
  "id": "call_00_wDNTxK7g6Prtf923niV32341",
  "name": "run_code",
  "arguments": "{\"code\": \"const out: string[] = [];\\nfor (const f of [\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-02-WorkBuddy安装与登录完整指南.md\\\",\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-03-WorkBuddy专家与专家团完整指南.md\\\"]) {\\n  const r = await tools.read({ file_path: f });\\n  out.push(\\\"=== \\\" + f + \\\" (\\\" + r.totalLines + \\\" lines) ===\\\");\\n  out.push(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\\n}\\nconsole.log(out.join(\\\"\\\\n\\\"));\", \"description\": \"Read WorkBuddy install/login and experts docs\"}"
}

## tool · 2026-10-05T10:50:55Z

run_code
{"code": "const out: string[] = [];\nfor (const f of [\"AI-Coding-Guide-Zh/docs/workbuddy/WB-02-WorkBuddy安装与登录完整指南.md\",\"AI-Coding-Guide-Zh/docs/workbuddy/WB-03-WorkBuddy专家与专家团完整指南.md\"]) {\n  const r = await tools.read({ file_path: f });\n  out.push(\"=== \" + f + \" (\" + r.totalLines + \" lines) ===\");\n  out.push(r.lines.map(l => l.text).join(\"\\n\"));\n}\nconsole.log(out.join(\"\\n\"));", "description": "Read WorkBuddy install/login and experts docs"}

## assistant · 2026-10-05T10:50:58Z

Now read WB-05, WB-07, WB-10. Let me do WB-05 and WB-07 first, then WB-10.
{
  "type": "tool-call",
  "id": "call_00_d7fXXvRXTKaOCUK8iJBi0721",
  "name": "run_code",
  "arguments": "{\"code\": \"const out: string[] = [];\\nfor (const f of [\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-05-WorkBuddy连接器与腾讯生态完整指南.md\\\",\\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-07-WorkBuddy自动化与计划任务完整指南.md\\\"]) {\\n  const r = await tools.read({ file_path: f });\\n  out.push(\\\"=== \\\" + f + \\\" (\\\" + r.totalLines + \\\" lines) ===\\\");\\n  out.push(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\\n}\\nconsole.log(out.join(\\\"\\\\n\\\"));\", \"description\": \"Read WorkBuddy connectors and automation docs\"}"
}

## tool · 2026-10-05T10:50:58Z

run_code
{"code": "const out: string[] = [];\nfor (const f of [\"AI-Coding-Guide-Zh/docs/workbuddy/WB-05-WorkBuddy连接器与腾讯生态完整指南.md\",\"AI-Coding-Guide-Zh/docs/workbuddy/WB-07-WorkBuddy自动化与计划任务完整指南.md\"]) {\n  const r = await tools.read({ file_path: f });\n  out.push(\"=== \" + f + \" (\" + r.totalLines + \" lines) ===\");\n  out.push(r.lines.map(l => l.text).join(\"\\n\"));\n}\nconsole.log(out.join(\"\\n\"));", "description": "Read WorkBuddy connectors and automation docs"}

## assistant · 2026-10-05T10:50:59Z

Now WB-10. Then OpenClaw files.
{
  "type": "tool-call",
  "id": "call_00_4gV2KububonfbN7PENaD3655",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/workbuddy/WB-10-WorkBuddy企业账号安全与对比完整指南.md\\\" });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read WorkBuddy enterprise accounts and comparison doc\"}"
}

## tool · 2026-10-05T10:50:59Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/workbuddy/WB-10-WorkBuddy企业账号安全与对比完整指南.md\" });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));", "description": "Read WorkBuddy enterprise accounts and comparison doc"}

## assistant · 2026-10-05T10:51:03Z

Now the OpenClaw docs. 4 files totaling ~6600 lines. Let me read the reading guide (1365) and project intro (1619) first. Actually let me be efficient: read 00 guide first to know structure, then read specific relevant sections of the others.

Let me read 00 fully but it's 1365 lines. Hmm, reading guide might contain directory map. Let me read it with limit 400 and grep headings. Actually better: use grep for headings in each file to navigate.

Let me get headings first.
{
  "type": "tool-call",
  "id": "call_00_VRXc5cHeBVEmQ5oATuNN6757",
  "name": "run_code",
  "arguments": "{\"code\": \"const fs = [\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\\\",\\n\\\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\\\",\\n];\\nconst out: string[] = [];\\nfor (const f of fs) {\\n  const r = await tools.grep({ pattern: \\\"^#{1,3} \\\", path: f });\\n  out.push(\\\"=== \\\" + f + \\\" ===\\\");\\n  out.push(r.matches.map(m => m.lineNumber + \\\": \\\" + m.line).join(\\\"\\\\n\\\"));\\n}\\nconsole.log(out.join(\\\"\\\\n\\\"));\", \"description\": \"List headings in OpenClaw docs\"}"
}

## tool · 2026-10-05T10:51:03Z

run_code
{"code": "const fs = [\n\"AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\",\n\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\",\n\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\",\n\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\",\n];\nconst out: string[] = [];\nfor (const f of fs) {\n  const r = await tools.grep({ pattern: \"^#{1,3} \", path: f });\n  out.push(\"=== \" + f + \" ===\");\n  out.push(r.matches.map(m => m.lineNumber + \": \" + m.line).join(\"\\n\"));\n}\nconsole.log(out.join(\"\\n\"));", "description": "List headings in OpenClaw docs"}

## assistant · 2026-10-05T10:51:06Z

Now I have a good structural view. Let me read key sections.

For 01-OpenClaw项目介绍: sections 1-480 (one-liner, history, architecture, core concepts), 585-730 (model providers, clients, community), 727-800 (fits/doesn't fit). Let me read lines 1-470 and 580-800.

For 03-快速开始: lines 1-180 (first conversation flow), 474-600 (config), 593-870 (scenarios: telegram/slack/whatsapp), 1520-1545 (security baseline).

For 10-安全: lines 1-130 (architecture), 226-300 (sandbox modes), 1238-1300 (best practices checklist & threats), 1836-1900 (FAQ).

For 00-阅读指南: lines 22-250 mainly (terminology, doc map, routes), 1265-1343 (quick card, version).

Let me read in batches. First batch: 01 intro lines 1-470.
{
  "type": "tool-call",
  "id": "call_00_TkQYnca1D4XwLCO671eO7906",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\\\", offset: 1, limit: 470 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw intro sections 1-470\"}"
}

## tool · 2026-10-05T10:51:06Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\", offset: 1, limit: 470 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw intro sections 1-470"}

## assistant · 2026-10-05T10:51:08Z

Good. Now read lines 585-800 (model providers, clients, community, fits).
{
  "type": "tool-call",
  "id": "call_00_ttzwPVGzz1pVA4mpoxaz1036",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\\\", offset: 583, limit: 260 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw model providers and use cases\"}"
}

## tool · 2026-10-05T10:51:08Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\", offset: 583, limit: 260 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw model providers and use cases"}

## assistant · 2026-10-05T10:51:11Z

Now read 01 lines 867-1010 (quick experience, responsibility chain) and 1032-1120 (selection). Actually I have enough for the intro. Let me also get the "quick experience" commands around line 867-895.
{
  "type": "tool-call",
  "id": "call_00_b6LyRN50YHnQxYi4lZpQ5440",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\\\", offset: 864, limit: 130 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\\nconsole.log(\\\"\\\\n\\\\n---- 1577-1616 ----\\\");\\nconst r2 = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\\\", offset: 1577, limit: 45 });\\nconsole.log(r2.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw quick experience and boundaries\"}"
}

## tool · 2026-10-05T10:51:11Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\", offset: 864, limit: 130 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));\nconsole.log(\"\\n\\n---- 1577-1616 ----\");\nconst r2 = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/01-OpenClaw项目介绍.md\", offset: 1577, limit: 45 });\nconsole.log(r2.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw quick experience and boundaries"}

## assistant · 2026-10-05T10:51:13Z

Now the quickstart 03. Read 1-180 (onboarding steps & control UI), 474-600 (config), 593-680 (Telegram scenario), 1520-1560 (security baseline). Let me read 1-180 first.
{
  "type": "tool-call",
  "id": "call_00_6HOWRVyS92kwvldv1CgN1062",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\\\", offset: 1, limit: 180 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw quickstart first 180 lines\"}"
}

## tool · 2026-10-05T10:51:13Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\", offset: 1, limit: 180 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw quickstart first 180 lines"}

## assistant · 2026-10-05T10:51:15Z

Now read config section 474-600, and Telegram scenario 593-680, and security baseline 1520-1575. Also CLI quick reference 339-475 briefly. Let me read 339-600 (261 lines).
{
  "type": "tool-call",
  "id": "call_00_23scuZ9uCG0eDtJQ6PYo1052",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\\\", offset: 339, limit: 265 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw CLI reference and config\"}"
}

## tool · 2026-10-05T10:51:15Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\", offset: 339, limit: 265 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw CLI reference and config"}

## assistant · 2026-10-05T10:51:18Z

Now read 593-680 for Telegram steps summarized, and 1520-1575 security baseline. Also the 00 guide's terminology and routes. Let me read 00 lines 22-160.
{
  "type": "tool-call",
  "id": "call_00_R0maC5vsYmuZt97WwzmF1004",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\\\", offset: 22, limit: 175 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw guide terminology and roadmap\"}"
}

## tool · 2026-10-05T10:51:18Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/00-阅读指南.md\", offset: 22, limit: 175 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw guide terminology and roadmap"}

## assistant · 2026-10-05T10:51:21Z

Great, terminology table is handy for analogies. Now the security doc. Read key sections: 1-130 (why, architecture, zero trust), 226-300 (sandbox modes), 386-470 (gateway auth, DM pairing), 1238-1300 (best practices), 1284-1360 (threats), 1836-1900 (FAQ). Let me read 20-130.
{
  "type": "tool-call",
  "id": "call_00_TXfPC9hEUcSFwIufpEMI4016",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\\\", offset: 20, limit: 110 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\\nconsole.log(\\\"\\\\n---- 226-300 ----\\\");\\nconst r2 = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\\\", offset: 226, limit: 80 });\\nconsole.log(r2.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw security architecture and sandbox\"}"
}

## tool · 2026-10-05T10:51:21Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\", offset: 20, limit: 110 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));\nconsole.log(\"\\n---- 226-300 ----\");\nconst r2 = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\", offset: 226, limit: 80 });\nconsole.log(r2.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw security architecture and sandbox"}

## assistant · 2026-10-05T10:51:23Z

Now security best practices checklist (1238-1300), threats (1284-1360), FAQ (1836-1900). Let me read 1238-1360.
{
  "type": "tool-call",
  "id": "call_00_iq3yMAU5cwLIx4RSWWtu0532",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\\\", offset: 1238, limit: 125 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\\nconsole.log(\\\"\\\\n---- 1836-1900 ----\\\");\\nconst r2 = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\\\", offset: 1836, limit: 65 });\\nconsole.log(r2.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw security checklist and FAQ\"}"
}

## tool · 2026-10-05T10:51:23Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\", offset: 1238, limit: 125 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));\nconsole.log(\"\\n---- 1836-1900 ----\");\nconst r2 = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/10-安全配置指南.md\", offset: 1836, limit: 65 });\nconsole.log(r2.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw security checklist and FAQ"}

## assistant · 2026-10-05T10:51:26Z

I now have plenty. Let me also check the quickstart's Telegram scenario lines 593-680 to capture concrete steps and security baseline 1520-1575. And 03's "三条判断线" not necessary. Let me read 597-680 and 1520-1575.
{
  "type": "tool-call",
  "id": "call_00_2mr6gjP7m1q7LQbFX2Sd8355",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\\\", offset: 597, limit: 80 });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\\nconsole.log(\\\"\\\\n---- 1518-1575 ----\\\");\\nconst r2 = await tools.read({ file_path: \\\"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\\\", offset: 1518, limit: 60 });\\nconsole.log(r2.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read OpenClaw Telegram scenario and security baseline\"}"
}

## tool · 2026-10-05T10:51:26Z

run_code
{"code": "const r = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\", offset: 597, limit: 80 });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));\nconsole.log(\"\\n---- 1518-1575 ----\");\nconst r2 = await tools.read({ file_path: \"AI-Coding-Guide-Zh/docs/openclaw/03-快速开始指南.md\", offset: 1518, limit: 60 });\nconsole.log(r2.lines.map(l => l.text).join(\"\\n\"));", "description": "Read OpenClaw Telegram scenario and security baseline"}

## assistant · 2026-10-05T10:51:30Z

I have enough content now. Let me also quickly verify WorkBuddy version/date facts: WorkBuddy 腾讯 2026年3月正式推出, tutorials written 2026年8月. OpenClaw: Peter Steinberger,开源 MIT, 2025年11月创建, 2026年1月末定名, Node.js 22+. Also WorkBuddy skills/WB-04 not read but WB-00 has skill market info. The task list mentioned "技能市场" for WorkBuddy — I can use WB-00/WB-01 info about 技能市场 (上万个，一键安装). WB-05 mentions MCP as "AI 世界的 USB 接口标准" analogy — good, task explicitly wants MCP ~ USB.

Also knowledge base (WB-06) not read; task wants knowledge base slide. WB-00 says WB-06 links 腾讯文档、ima 知识库. WB-10 mentions 知识库: 把你的资料喂给 AI 当依据. WB-05 Q mentions. That's enough (no fabrication beyond: WB-00 says "把腾讯文档、ima 知识库接进来让 AI 读你的资料"). Good.

多端协同 WB-08: WB-00 says 桌面开了任务，手机/企业微信/小程序继续接. WB-01: 桌面 App（Windows/macOS）, 微信/企业微信远程触发, 微信小程序. WB-07 remote trigger. Enough.

Now check output dir exists. Let's check vibe-coding-ppt/content/ and any existing files for format conventions. Possibly sibling JSONs exist (other 册). Let me list.
{
  "type": "tool-call",
  "id": "call_00_A4Uu9oGx2yzYUUrYRjea3549",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.bash({ command: \\\"ls -la vibe-coding-ppt/ 2>/dev/null; echo '---'; ls -la vibe-coding-ppt/content/ 2>/dev/null\\\", description: \\\"List PPT project directories\\\" });\\nreturn r.kind === \\\"foreground\\\" ? r.stdout.text + r.stderr.text : JSON.stringify(r);\", \"description\": \"List existing PPT project files\"}"
}

## tool · 2026-10-05T10:51:30Z

run_code
{"code": "const r = await tools.bash({ command: \"ls -la vibe-coding-ppt/ 2>/dev/null; echo '---'; ls -la vibe-coding-ppt/content/ 2>/dev/null\", description: \"List PPT project directories\" });\nreturn r.kind === \"foreground\" ? r.stdout.text + r.stderr.text : JSON.stringify(r);", "description": "List existing PPT project files"}

## assistant · 2026-10-05T10:51:33Z

Let me read the existing 01-overview.json to match style/format conventions.
{
  "type": "tool-call",
  "id": "call_00_tFdu022vsZBpaJ4uClq51361",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"vibe-coding-ppt/content/01-overview.json\\\" });\\nconsole.log(r.lines.map(l => l.text).join(\\\"\\\\n\\\"));\", \"description\": \"Read existing overview JSON for format\"}"
}

## tool · 2026-10-05T10:51:33Z

run_code
{"code": "const r = await tools.read({ file_path: \"vibe-coding-ppt/content/01-overview.json\" });\nconsole.log(r.lines.map(l => l.text).join(\"\\n\"));", "description": "Read existing overview JSON for format"}

## assistant · 2026-10-05T10:51:46Z

Good, I have the format. Now design 15-18 slides for 04-office-assistant.json covering OpenClaw + WorkBuddy.

Plan slides (target 17-18):

1. cover — 办公助手主线：OpenClaw 与 WorkBuddy（第 04 册）kicker "Vibe Coding 学习系列 · 04"
2. section — 两条办公助手主线怎么选 (with subtitle)
3. table — 两条主线速览 (OpenClaw vs WorkBuddy): headers 工具/是什么/谁适合/怎么用/门槛. 5 cols max. rows 2-3.
4. section — 第一部分：OpenClaw
   Actually maybe combine. Let's structure:
2. section "先看全局：两条办公助手主线"
3. table 对比（OpenClaw 开源框架 vs WorkBuddy 腾讯 AI 办公助手）— 5 columns: 维度, OpenClaw, WorkBuddy? That's 3 cols. rows: 定位/给谁用/怎么登/主要入口/语言或生态. Let me do headers ["维度","OpenClaw","WorkBuddy"] with rows: 出品与授权, 给谁用, 怎么用(登录/形态), 主要入口, 网络与支付. 5 rows.

Actually let's have:
- slide 2: section "两条办公助手主线"
- slide 3: table "一张表看懂两条主线" (3 cols × 5 rows)
- slide 4: cards "该选哪条线" 3-4 cards? Could be steps. Let me do bullets "怎么选：按场景对号入座".

Then OpenClaw:
- slide 5: section "OpenClaw：开源 AI 私人助手"
- slide 6: bullets "OpenClaw 是什么" (开源 MIT, 跑在自己电脑/服务器, 接 WhatsApp/Telegram/Discord 等, 7x24 AI 员工, 数据本地保存但云端模型仍发消息)
- slide 7: table "OpenClaw 关键术语" or cards (Gateway 前台总机, Agent 员工, Channel 工位电话, Skill 操作手册, Memory 笔记本). table 2 cols × 5 rows.
- slide 8: steps "5 分钟跑起第一个对话" — 安装 script, onboard, gateway status, 打开 Control UI http://127.0.0.1:18789/. 4 steps. Commands verbatim.
- slide 9: bullets "模型配置要点" — 支持 OpenAI/Anthropic/Google/DeepSeek/通义千问/智谱/Ollama 等; API Key 用环境变量; 主模型故障转移; 模型目录变化快以本机为准.
- slide 10: table "消息平台接入" — 平台/认证方式: Telegram Bot Token, Discord Bot Token, Slack OAuth App, WhatsApp 扫码配对, iMessage/BlueBubbles. 5 rows. + 配对模式/DM pairing.
- slide 11: cards "技能与记忆" — 技能三层/Bundled, Managed(ClawHub), Workspace; 记忆 = MEMORY.md + memory/日期.md; memory_search/memory_get; ClawHub 技能市场. Maybe cards 4.
- slide 12: bullets "安全底线（OpenClaw）" — Gateway Token, 绑定 127.0.0.1, DM 配对, API Key 环境变量, 沙箱 mode non-main, 配置文件 600, TLS 1.3. 5 bullets.

Then WorkBuddy:
- slide 13: section "WorkBuddy：腾讯 AI 办公助手"
- slide 14: bullets "WorkBuddy 是什么" (腾讯 2026年3月推出, 微信扫码登录, 无需 API Key/英文/翻墙, 一群有专业身份的 AI 角色交付成品, 与 CodeBuddy 同账号)
- slide 15: cards "五个核心概念" — 专家/专家团/技能/连接器/自动化 (5 cards; requirement says cards 3-4). Hmm requirement: cards 用 3-4 张. So 5 cards violates. Use table 2 cols × 5 rows for five concepts with 类比. Good — table ≤5 cols, ≤6 rows. 5 rows fine.
- slide 16: steps "安装登录三步" — 官网下载(认准腾讯官网, Mac 拖进 Applications), 微信扫码登录, 跑第一个任务"你好，请用一句话介绍你自己". 3 steps (3-4 allowed).
- slide 17: table "连接器与腾讯生态" — 连接器/能干什么: QQ邮箱, 腾讯文档, 腾讯会议, 企业微信, TAPD/腾讯乐享. 5 rows. Mention MCP as USB.
- slide 18: bullets "知识库与多端协同" — 知识库接腾讯文档/ima; 手机小程序; 企业微信远程触发; 桌面开任务手机继续.
- slide 19: steps or bullets "自动化与定时任务" — 定时/触发/远程三类; 例: 每天9点昨日工作摘要推企业微信; 预演再启用.
- slide 20: bullets "专家与专家团" — 单专家=角色化, 专家团=团长拆解并行, 消耗 3-5 倍, 提问五要素 身份+任务+输入+输出格式+边界.

Then selection & end:
- slide 21: table "选型建议" 四工具? Task says "选型建议与安全边界". Include WorkBuddy vs OpenClaw + 与 Claude Code/Codex. Could do table headers ["需求","推荐"]. rows 4-5.
- slide 22: bullets "安全边界" for WorkBuddy: 敏感数据脱敏, 最小授权, 连接器授权看清权限, 定期解绑, 自动化别配删除/自动回复.
- slide 23: end.

That's ~23 slides, too many (need 15-18). Need to compress to 15-18.

Let me target 18 slides total:
1. cover
2. section "两条办公助手主线"
3. table 对比 (OpenClaw vs WorkBuddy) — 3 cols
4. bullets 怎么选
5. section "OpenClaw：开源 AI 私人助手"
6. bullets OpenClaw 是什么
7. steps 5分钟跑起第一个对话（含术语解释可能放 bullets）
8. table 关键术语（Gateway/Agent/Channel/Skill/Memory 类比）
9. bullets 模型配置要点
10. table 消息平台接入
11. cards 技能与记忆
12. bullets OpenClaw 安全底线
13. section "WorkBuddy：腾讯 AI 办公助手"
14. bullets WorkBuddy 是什么
15. table 五个核心概念
16. steps 安装与登录
17. cards 专家与专家团 (3-4 cards)... but need connectors, knowledge base, automation, multi-device too.

That's already 17 with WorkBuddy only partially covered. Need connectors/ecosystem, knowledge base, automation, multi-device, selection, security. Too much for 18.

I need to merge. The task suggested coverage list; I should cover all listed topics but can combine into fewer slides. Let's budget 18 slides:

1. cover
2. section 总览 (两条主线)
3. table 两条主线对比
4. bullets 怎么选（选型建议放在这里 or later）
5. section OpenClaw
6. bullets OpenClaw 是什么
7. steps 5 分钟跑通第一个对话
8. table 关键术语（Gateway/Agent/Channel/Skill/Memory）
9. bullets 模型配置 + 消息平台接入 合并? Hmm. Model config要点 and 消息平台接入 are distinct. Could make slide 9 = table 消息平台接入 (含认证方式), slide 10 = bullets 模型配置要点与安全. Let's keep model as bullets, platform as table.
10. table 消息平台接入
11. cards 技能与记忆 (2 cards? cards 3-4). Use cards 4: 内置技能 / ClawHub 市场 / MEMORY.md 长期记忆 / 每日日志. Good.
12. bullets OpenClaw 安全底线
13. section WorkBuddy
14. bullets WorkBuddy 是什么
15. table 五个核心概念（含连接器）
16. steps 安装与登录（含扫码、免 API Key）
17. bullets 专家与专家团 + 提问模板
18. table 连接器与腾讯生态
19. bullets 知识库、自动化、多端协同（合并）
20. bullets 选型建议与安全边界
21. end

21 slides. Still too many. Compress:

- Merge slide 9 (model config) into slide 10 table? Could make a table with model providers... Actually model config要点 can be a bullets slide; platform接入 combined into a table. Perhaps merge 模型配置 and 消息平台 into one bullets slide "模型与消息平台" with 5 bullets? But then table for platforms lost. Or one table for platforms and put model要点 as one bullet in OpenClaw是什么? Not great.

Let me reconsider: aim 18 total. Remove section slides? Requirement: cover → 目录或分节 → 内容 → 结尾(end). At least one section required presumably. We can have 2 sections.

Proposed 18:
1. cover
2. section "两条办公助手主线"
3. table "两条主线速览"（对比）
4. bullets "怎么选：对号入座"
5. section "OpenClaw：开源 AI 私人助手"
6. bullets "OpenClaw 是什么"
7. table "关键术语（生活类比）" Gateway/Agent/Channel/Skill/Memory
8. steps "5 分钟跑起第一个对话"
9. bullets "模型配置要点"
10. table "消息平台接入"
11. cards "技能与记忆"
12. bullets "OpenClaw 安全底线"
13. section "WorkBuddy：腾讯 AI 办公助手"  → that's 3 sections... maybe only one section for WorkBuddy and put OpenClaw under same? Requirement allows 目录或分节. Multiple sections fine, but slides budget.

Alternative: drop slide 12 (OpenClaw 安全底线) — no, task explicitly wants 安全注意 for OpenClaw and 安全边界 later. Could combine OpenClaw security into slide 6 or 11? Hmm.

Let me carefully count required topic coverage:
- 两条办公助手主线怎么选 ✔ (slides 2-4)
- OpenClaw 是什么 ✔ (6)
- OpenClaw 环境与第一个对话 ✔ (8, +术语 7)
- 模型配置要点 ✔ (9)
- 消息平台接入 ✔ (10)
- 技能与记忆 ✔ (11)
- 安全注意 ✔ (12)
- WorkBuddy 是什么 ✔
- 安装登录 ✔
- 专家与专家团 ✔
- 技能市场 ✔ (part of 五个核心概念)
- 连接器与腾讯生态 ✔
- 知识库 ✔
- 自动化与定时任务 ✔
- 多端协同 ✔
- 选型建议与安全边界 ✔

WorkBuddy needs: 是什么, 安装登录, 专家与专家团, 技能市场, 连接器, 知识库, 自动化, 多端协同, 选型+安全. That's 9 slides if one each, plus 1 section = 10. OpenClaw section: 是什么, 环境/第一对话, 模型, 平台, 技能记忆, 安全 = 6 + 1 section = 7. Plus cover, end, overview section+3 = 4. Total 10+7+... let's count: cover(1) + overview section(1) + table(1) + 怎么选(1) + OpenClaw section(1) + 6 = 11 up to OpenClaw; + WorkBuddy section(1) + 9 = 21; + end = 22. Too many.

Need to merge WorkBuddy topics:
- 技能市场 merge into 专家与专家团? They're distinct. Could make a table "WorkBuddy 能力速查" with rows 专家/专家团/技能市场/知识库/自动化/连接器/多端 — but rows ≤6. Hmm 7 rows too many.
- Use two tables: "五大核心概念" (专家/专家团/技能/自动化/连接器 = 5 rows) which covers 专家、专家团、技能市场、连接器、自动化. Then a separate slide for 知识库+多端协同 (bullets). Then 连接器与腾讯生态 detail
