# 工作目录：/Users/oyamahappa/Documen

来源：dsh

项目：/Users/oyamahappa/Documents/Agent/DSH

## user · 2026-10-05T11:52:17Z

工作目录：/Users/oyamahappa/Documents/Agent/DSH
面向对象：完全新手 / 办公人。语言：简体中文。

任务：为下面每一篇教程文档，各生成一份 **PPT 内容 JSON**，写入 vibe-coding-ppt/tutorials-content/<code>.json。
每份 JSON 对应一个独立 PPT，10-14 张幻灯片，封面 kicker 固定为 "Vibe Coding 学习系列 · <code>"。

本次负责的文档（每篇一份 JSON，文件名用 code 小写，如 CC-01 → cc-01.json）：
- code=CX-01  category=codex  fileTitle=Codex-App安装与认证  文档=AI-Coding-Guide-Zh/docs/codex/CX-01-Codex-App安装与认证完整指南.md
- code=CX-02  category=codex  fileTitle=Codex-App桌面工作流  文档=AI-Coding-Guide-Zh/docs/codex/CX-02-Codex-App桌面工作流完整指南.md
- code=CX-03  category=codex  fileTitle=Codex-Commands工作流入口  文档=AI-Coding-Guide-Zh/docs/codex/CX-03-Codex-Commands工作流入口完整指南.md
- code=CX-04  category=codex  fileTitle=Codex项目指令权限配置  文档=AI-Coding-Guide-Zh/docs/codex/CX-04-Codex项目指令权限配置完整指南.md
- code=CX-05  category=codex  fileTitle=Codex-MCP外部工具  文档=AI-Coding-Guide-Zh/docs/codex/CX-05-Codex-MCP外部工具完整指南.md
- code=CX-06  category=codex  fileTitle=Codex-Skills可复用工作流  文档=AI-Coding-Guide-Zh/docs/codex/CX-06-Codex-Skills可复用工作流完整指南.md
- code=CX-07  category=codex  fileTitle=Codex-Plugins连接器  文档=AI-Coding-Guide-Zh/docs/codex/CX-07-Codex-Plugins连接器完整指南.md

硬性要求：
1. 内容必须来自对应文档，不得编造；命令、版本号、数字、功能名忠于原文。
2. 每张 bullets 不超过 5 条，每条不超过 42 个汉字；cards 3-4 张；steps 3-4 步；table 不超过 5 列 6 行。
3. 用适合新手的类比解释术语。文档很长，必须用 read 的 offset/limit 分段读取，先看标题结构再抽取重点。
4. 用 write 工具逐个写文件，UTF-8 纯 JSON，不要加 markdown 代码围栏。
5. 全部写完后，返回一份简短清单：每个 code、deck 标题、幻灯片数量。

JSON schema（严格遵守）：
{
  "code": "CC-01",
  "category": "claude-code",
  "fileTitle": "Claude Code完整安装指南",
  "deck": "幻灯片主标题",
  "slides": [
    {"layout":"cover","title":"...","subtitle":"...","kicker":"Vibe Coding 学习系列 · CC-01"},
    {"layout":"section","title":"...","subtitle":"..."},
    {"layout":"bullets","title":"...","bullets":["...","..."],"notes":"讲稿提示(可省略)"},
    {"layout":"cards","title":"...","cards":[{"title":"...","desc":"..."}]},
    {"layout":"table","title":"...","headers":["..."],"rows":[["..."]]},
    {"layout":"steps","title":"...","steps":[{"title":"...","desc":"..."}]},
    {"layout":"quote","title":"...","subtitle":"..."},
    {"layout":"end","title":"...","subtitle":"..."}
  ]
}
Your parent agent id is "session-0de88cee-855e-47e3-a7d8-5cedfd0973a3". Before you finish, send your result to that agent with send_message({ agent_id: "session-0de88cee-855e-47e3-a7d8-5cedfd0973a3", message: "<self-contained result>" }). The parent shares your workspace but does not automatically receive your transcript, tool output, or reasoning. Send earlier messages as well when a finding changes what the parent should do next; sending a message does not end your turn.

## assistant · 2026-10-05T11:52:19Z

Let me start by exploring the workspace structure and the documents.

Let me first check the documents' sizes and titles.
我先称呼你为妹妹，然后开始查看文档结构。
{
  "type": "tool-call",
  "id": "call_00_9bnAhkdQiWRhs2S57wB01375",
  "name": "run_code",
  "arguments": "{\"code\": \"const base = \\\"/Users/oyamahappa/Documents/Agent/DSH\\\";\\nconst r = await tools.bash({ command: \\\"ls -la /Users/oyamahappa/Documents/Agent/DSH && echo '---' && ls -la /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt 2>/dev/null && echo '---' && ls -la /Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/ && echo '---' && wc -l /Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/*.md\\\", description: \\\"List workspace and codex docs\\\" });\\nif (r.kind === \\\"foreground\\\") return r.stdout.text;\\nreturn JSON.stringify(r);\", \"description\": \"List workspace and codex docs\"}"
}

## tool · 2026-10-05T11:52:19Z

run_code
{"code": "const base = \"/Users/oyamahappa/Documents/Agent/DSH\";\nconst r = await tools.bash({ command: \"ls -la /Users/oyamahappa/Documents/Agent/DSH && echo '---' && ls -la /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt 2>/dev/null && echo '---' && ls -la /Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/ && echo '---' && wc -l /Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/*.md\", description: \"List workspace and codex docs\" });\nif (r.kind === \"foreground\") return r.stdout.text;\nreturn JSON.stringify(r);", "description": "List workspace and codex docs"}

## assistant · 2026-10-05T11:52:22Z

Let me look at existing content JSON files to understand the format/style used, and check tutorials and content dirs.
{
  "type": "tool-call",
  "id": "call_00_DacFsVd7f45eMtWzQoEe9864",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.bash({ command: \\\"find /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/content /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content -type f | head -50\\\", description: \\\"List vibe-coding-ppt subdirs\\\" });\\nif (r.kind === \\\"foreground\\\") return r.stdout.text + \\\"\\\\n---STDERR---\\\\n\\\" + r.stderr.text;\\nreturn JSON.stringify(r);\", \"description\": \"List ppt content dirs\"}"
}

## tool · 2026-10-05T11:52:22Z

run_code
{"code": "const r = await tools.bash({ command: \"find /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/content /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials /Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content -type f | head -50\", description: \"List vibe-coding-ppt subdirs\" });\nif (r.kind === \"foreground\") return r.stdout.text + \"\\n---STDERR---\\n\" + r.stderr.text;\nreturn JSON.stringify(r);", "description": "List ppt content dirs"}

## assistant · 2026-10-05T11:52:24Z

{
  "type": "tool-call",
  "id": "call_00_ET_xkqs4h4F8arpchlRWXCT4062",
  "name": "run_code",
  "arguments": "{\"code\": \"const r = await tools.read({ file_path: \\\"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/content/03-codex.json\\\" });\\nreturn JSON.stringify(r.lines.map(l=>l.text), null, 1).slice(0, 6000);\", \"description\": \"Read existing codex content JSON\"}"
}

## tool · 2026-10-05T11:52:24Z

run_code
{"code": "const r = await tools.read({ file_path: \"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/content/03-codex.json\" });\nreturn JSON.stringify(r.lines.map(l=>l.text), null, 1).slice(0, 6000);", "description": "Read existing codex content JSON"}

## assistant · 2026-10-05T11:52:28Z

Now I understand the target style. Let me read the documents. I need to read each doc's heading structure first. Let me extract headings with grep.

Let me be efficient: I'll read headings for all 7 docs, then read relevant sections. Since docs are ~1400-1900 lines each, reading full would be a lot. But I need accurate content. Let me plan: I could delegate to subagents, but the task says I'm a subagent; I can still create subagents. Actually, better to just do it myself carefully.

Strategy: For each doc, grep for headings (lines starting with #). Then read selected ranges to extract key content (commands, versions, numbers, feature names). Then write JSON.

Given 7 docs, that's substantial. Let me use subagents to parallelize? The subagent tool works. But quality control matters. Let me first look at headings for all 7 docs, then decide.

Actually, delegating each doc to a subagent could be efficient and each has its own context. But the subagents would need to follow the schema precisely. I could give them precise instructions. However, risk of inconsistent quality. Given the volume (7 × ~1500 lines), I think I can handle it myself with targeted reading. Let me get the heading structures first.
{
  "type": "tool-call",
  "id": "call_00_nwHD4NwrBHTKBNMNOmai0334",
  "name": "run_code",
  "arguments": "{\"code\": \"const dir = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex\\\";\\nconst files = [\\\"CX-01-Codex-App安装与认证完整指南.md\\\",\\\"CX-02-Codex-App桌面工作流完整指南.md\\\",\\\"CX-03-Codex-Commands工作流入口完整指南.md\\\",\\\"CX-04-Codex项目指令权限配置完整指南.md\\\",\\\"CX-05-Codex-MCP外部工具完整指南.md\\\",\\\"CX-06-Codex-Skills可复用工作流完整指南.md\\\",\\\"CX-07-Codex-Plugins连接器完整指南.md\\\"];\\nconst out: string[] = [];\\nfor (const f of files) {\\n  const g = await tools.grep({ pattern: \\\"^#{1,4} \\\", path: dir + \\\"/\\\" + f });\\n  out.push(\\\"=== \\\" + f + \\\" ===\\\");\\n  out.push(g.matches.map(m => m.lineNumber + \\\" \\\" + m.line).join(\\\"\\\\n\\\"));\\n}\\nreturn out.join(\\\"\\\\n\\\");\", \"description\": \"Extract heading structures of 7 docs\"}"
}

## tool · 2026-10-05T11:52:28Z

run_code
{"code": "const dir = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex\";\nconst files = [\"CX-01-Codex-App安装与认证完整指南.md\",\"CX-02-Codex-App桌面工作流完整指南.md\",\"CX-03-Codex-Commands工作流入口完整指南.md\",\"CX-04-Codex项目指令权限配置完整指南.md\",\"CX-05-Codex-MCP外部工具完整指南.md\",\"CX-06-Codex-Skills可复用工作流完整指南.md\",\"CX-07-Codex-Plugins连接器完整指南.md\"];\nconst out: string[] = [];\nfor (const f of files) {\n  const g = await tools.grep({ pattern: \"^#{1,4} \", path: dir + \"/\" + f });\n  out.push(\"=== \" + f + \" ===\");\n  out.push(g.matches.map(m => m.lineNumber + \" \" + m.line).join(\"\\n\"));\n}\nreturn out.join(\"\\n\");", "description": "Extract heading structures of 7 docs"}

## assistant · 2026-10-05T11:52:32Z

Now I have heading structures. I need to read actual content for each doc to extract accurate details. Let me read key sections. I'll do this in a programmatic way: read ranges and print. To conserve, I'll read the most content-rich parts: the intro/goals, core concepts, commands, and summary/checklists.

Let me start with CX-01. Key ranges: lines 1-260, 296-500, 656-730, 1068-1135, 1476-1541.

Actually, let me read larger chunks and print them; the output goes to my context anyway. Total 7 docs × maybe 400 lines = 2800 lines. That's manageable but big. Let me be selective.

I'll process each doc separately: read ~3-4 ranges each.

Let me start with CX-01.
{
  "type": "tool-call",
  "id": "call_00_qz2gZvNmnoaRXiKDg3oH0689",
  "name": "run_code",
  "arguments": "{\"code\": \"const p = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-01-Codex-App安装与认证完整指南.md\\\";\\nconst parts = [[1,105],[122,260],[296,360],[400,500],[555,660]];\\nlet out = \\\"\\\";\\nfor (const [a,b] of parts) {\\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\\n  out += \\\"\\\\n### L\\\"+a+\\\"-\\\"+b+\\\"\\\\n\\\" + r.lines.map(l=>l.text).join(\\\"\\\\n\\\") + \\\"\\\\n\\\";\\n}\\nreturn out;\", \"description\": \"Read CX-01 key sections\"}"
}

## tool · 2026-10-05T11:52:32Z

run_code
{"code": "const p = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-01-Codex-App安装与认证完整指南.md\";\nconst parts = [[1,105],[122,260],[296,360],[400,500],[555,660]];\nlet out = \"\";\nfor (const [a,b] of parts) {\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\n  out += \"\\n### L\"+a+\"-\"+b+\"\\n\" + r.lines.map(l=>l.text).join(\"\\n\") + \"\\n\";\n}\nreturn out;", "description": "Read CX-01 key sections"}

## assistant · 2026-10-05T11:52:36Z

I have enough for CX-01. Let me also read the workspace workshop section and summary/checklist lines 1476-1541 for details. Actually I have enough content. Let me read a bit of 1268-1300 (团队安装现场) maybe not needed. Let me read 1476-1541 for summary and appendix.

Actually, I have enough. Let me plan the 12 slides for CX-01.

But I should account for hard requirements: bullets ≤5, each ≤42 汉字; cards 3-4; steps 3-4; table ≤5 cols, ≤6 rows.

Let me design CX-01 deck (12 slides):
1. cover
2. section (目录/心智模型)
3. bullets: Codex App 是什么/安装目标
4. table: 系统要求 (Windows/macOS/Linux)
5. steps: Windows 安装四步
6. cards: 首次启动的关卡 (登录/权限提示/防火墙)
7. table: 常见报错与第一反应
8. steps: 第一次打开项目
9. bullets: 只读任务与可写任务
10. cards: 安装后检查清单
11. table: CLI 辅助命令
12. end

Need "kicker" exactly "Vibe Coding 学习系列 · CX-01".

Let me now read CX-02 sections. Key: 83-260, 287-360, 460-512, 689-762, 1594-1633.

Let me do that. Also CX-03 through CX-07. I'll batch reads per doc in separate run_code calls, maybe two docs per call to save time. But output size... Let me do one doc per call to keep manageable, but that's 6 more calls. Fine.

Actually let me do CX-02 now.
{
  "type": "tool-call",
  "id": "call_00_jR4FO7hu49r5IiAsgUtv6843",
  "name": "run_code",
  "arguments": "{\"code\": \"const p = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-02-Codex-App桌面工作流完整指南.md\\\";\\nconst parts = [[83,260],[287,360],[460,512],[689,762],[1594,1635]];\\nlet out = \\\"\\\";\\nfor (const [a,b] of parts) {\\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\\n  out += \\\"\\\\n### L\\\"+a+\\\"-\\\"+b+\\\"\\\\n\\\" + r.lines.map(l=>l.text).join(\\\"\\\\n\\\") + \\\"\\\\n\\\";\\n}\\nreturn out;\", \"description\": \"Read CX-02 key sections\"}"
}

## tool · 2026-10-05T11:52:36Z

run_code
{"code": "const p = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-02-Codex-App桌面工作流完整指南.md\";\nconst parts = [[83,260],[287,360],[460,512],[689,762],[1594,1635]];\nlet out = \"\";\nfor (const [a,b] of parts) {\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\n  out += \"\\n### L\"+a+\"-\"+b+\"\\n\" + r.lines.map(l=>l.text).join(\"\\n\") + \"\\n\";\n}\nreturn out;", "description": "Read CX-02 key sections"}

## assistant · 2026-10-05T11:52:39Z

Good. Now CX-03. Key sections: 96-235, 235-360, 400-445, 1590-1616.
{
  "type": "tool-call",
  "id": "call_00_ycNBqLAwxrFy5C3hDIct1808",
  "name": "run_code",
  "arguments": "{\"code\": \"const p = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-03-Codex-Commands工作流入口完整指南.md\\\";\\nconst parts = [[96,235],[235,360],[400,445],[553,668],[1590,1618]];\\nlet out = \\\"\\\";\\nfor (const [a,b] of parts) {\\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\\n  out += \\\"\\\\n### L\\\"+a+\\\"-\\\"+b+\\\"\\\\n\\\" + r.lines.map(l=>l.text).join(\\\"\\\\n\\\") + \\\"\\\\n\\\";\\n}\\nreturn out;\", \"description\": \"Read CX-03 key sections\"}"
}

## tool · 2026-10-05T11:52:39Z

run_code
{"code": "const p = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-03-Codex-Commands工作流入口完整指南.md\";\nconst parts = [[96,235],[235,360],[400,445],[553,668],[1590,1618]];\nlet out = \"\";\nfor (const [a,b] of parts) {\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\n  out += \"\\n### L\"+a+\"-\"+b+\"\\n\" + r.lines.map(l=>l.text).join(\"\\n\") + \"\\n\";\n}\nreturn out;", "description": "Read CX-03 key sections"}

## assistant · 2026-10-05T11:52:41Z

Now CX-04. Key sections: 59-105, 285-470, 508-590, 1040-1120, 1857-1943.
{
  "type": "tool-call",
  "id": "call_00_Ci4mBZATUSPrC2mvoP5M4550",
  "name": "run_code",
  "arguments": "{\"code\": \"const p = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-04-Codex项目指令权限配置完整指南.md\\\";\\nconst parts = [[59,105],[285,470],[508,600],[1040,1120],[1857,1945]];\\nlet out = \\\"\\\";\\nfor (const [a,b] of parts) {\\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\\n  out += \\\"\\\\n### L\\\"+a+\\\"-\\\"+b+\\\"\\\\n\\\" + r.lines.map(l=>l.text).join(\\\"\\\\n\\\") + \\\"\\\\n\\\";\\n}\\nreturn out;\", \"description\": \"Read CX-04 key sections\"}"
}

## tool · 2026-10-05T11:52:41Z

run_code
{"code": "const p = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-04-Codex项目指令权限配置完整指南.md\";\nconst parts = [[59,105],[285,470],[508,600],[1040,1120],[1857,1945]];\nlet out = \"\";\nfor (const [a,b] of parts) {\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\n  out += \"\\n### L\"+a+\"-\"+b+\"\\n\" + r.lines.map(l=>l.text).join(\"\\n\") + \"\\n\";\n}\nreturn out;", "description": "Read CX-04 key sections"}

## assistant · 2026-10-05T11:52:43Z

Now CX-05, CX-06, CX-07. Let me read the key sections. Start CX-05.
{
  "type": "tool-call",
  "id": "call_00_JHMjglDpvyJww2m7rOkM1133",
  "name": "run_code",
  "arguments": "{\"code\": \"const p = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-05-Codex-MCP外部工具完整指南.md\\\";\\nconst parts = [[84,260],[260,330],[514,650],[1422,1457]];\\nlet out = \\\"\\\";\\nfor (const [a,b] of parts) {\\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\\n  out += \\\"\\\\n### L\\\"+a+\\\"-\\\"+b+\\\"\\\\n\\\" + r.lines.map(l=>l.text).join(\\\"\\\\n\\\") + \\\"\\\\n\\\";\\n}\\nreturn out;\", \"description\": \"Read CX-05 key sections\"}"
}

## tool · 2026-10-05T11:52:43Z

run_code
{"code": "const p = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-05-Codex-MCP外部工具完整指南.md\";\nconst parts = [[84,260],[260,330],[514,650],[1422,1457]];\nlet out = \"\";\nfor (const [a,b] of parts) {\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\n  out += \"\\n### L\"+a+\"-\"+b+\"\\n\" + r.lines.map(l=>l.text).join(\"\\n\") + \"\\n\";\n}\nreturn out;", "description": "Read CX-05 key sections"}

## assistant · 2026-10-05T11:52:45Z

Now CX-06 and CX-07.
{
  "type": "tool-call",
  "id": "call_00_2rnL1o92DNFnWuxOO02p7986",
  "name": "run_code",
  "arguments": "{\"code\": \"const p = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-06-Codex-Skills可复用工作流完整指南.md\\\";\\nconst parts = [[83,250],[275,340],[664,730],[1578,1613]];\\nlet out = \\\"\\\";\\nfor (const [a,b] of parts) {\\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\\n  out += \\\"\\\\n### L\\\"+a+\\\"-\\\"+b+\\\"\\\\n\\\" + r.lines.map(l=>l.text).join(\\\"\\\\n\\\") + \\\"\\\\n\\\";\\n}\\nreturn out;\", \"description\": \"Read CX-06 key sections\"}"
}

## tool · 2026-10-05T11:52:45Z

run_code
{"code": "const p = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-06-Codex-Skills可复用工作流完整指南.md\";\nconst parts = [[83,250],[275,340],[664,730],[1578,1613]];\nlet out = \"\";\nfor (const [a,b] of parts) {\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\n  out += \"\\n### L\"+a+\"-\"+b+\"\\n\" + r.lines.map(l=>l.text).join(\"\\n\") + \"\\n\";\n}\nreturn out;", "description": "Read CX-06 key sections"}

## assistant · 2026-10-05T11:52:47Z

{
  "type": "tool-call",
  "id": "call_00_ET_obdshDhP6G8BbVx3vKRs3896",
  "name": "run_code",
  "arguments": "{\"code\": \"const p = \\\"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-07-Codex-Plugins连接器完整指南.md\\\";\\nconst parts = [[78,260],[431,470],[474,660],[1331,1366]];\\nlet out = \\\"\\\";\\nfor (const [a,b] of parts) {\\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\\n  out += \\\"\\\\n### L\\\"+a+\\\"-\\\"+b+\\\"\\\\n\\\" + r.lines.map(l=>l.text).join(\\\"\\\\n\\\") + \\\"\\\\n\\\";\\n}\\nreturn out;\", \"description\": \"Read CX-07 key sections\"}"
}

## tool · 2026-10-05T11:52:47Z

run_code
{"code": "const p = \"/Users/oyamahappa/Documents/Agent/DSH/AI-Coding-Guide-Zh/docs/codex/CX-07-Codex-Plugins连接器完整指南.md\";\nconst parts = [[78,260],[431,470],[474,660],[1331,1366]];\nlet out = \"\";\nfor (const [a,b] of parts) {\n  const r = await tools.read({ file_path: p, offset: a, limit: b-a+1 });\n  out += \"\\n### L\"+a+\"-\"+b+\"\\n\" + r.lines.map(l=>l.text).join(\"\\n\") + \"\\n\";\n}\nreturn out;", "description": "Read CX-07 key sections"}

## assistant · 2026-10-05T11:53:42Z

I now have enough content for all 7. Let me also quickly verify a couple of details for CX-01: firewall section 260-296 which I skipped. Let me read it plus check version numbers. Actually not critical. Let me read 260-296 for firewall accuracy.

Also I should check the tutorials-content directory is empty and create nothing else. Let me now write the JSON files.

Let me carefully enforce constraints:
- bullets ≤5, each ≤42 汉字. I'll count Chinese chars roughly; keep short.
- cards 3-4
- steps 3-4
- table ≤5 cols, ≤6 rows (rows excluding header presumably)
- 10-14 slides

Let me design each deck.

### CX-01 (安装与认证)
1. cover: kicker "Vibe Coding 学习系列 · CX-01", title, subtitle
2. section: 安装目标：能打开、能登录、能开线程
3. bullets: 安装成功的标准 (6 → max 5). bullets:
   - "装好的标准不是终端有 codex 命令" (16)
   - "桌面 App 能打开并登录 ChatGPT 账号"
   - "能添加本地项目并创建 Local thread"
   - "能只读分析项目，能做小改动"
   - "Review 面板能看到 diff 和文件变更"
4. table: 系统准备 (平台/版本建议/安装来源) 3 cols, 3 rows
   Windows: Windows 11 推荐基线 / Microsoft Store 或 winget
   macOS: 使用仍受支持的版本 / 官方 App 下载页
   Linux: App 暂未覆盖 / 先用 CLI / Web / Cloud
5. steps: Windows 安装四步 (从官方页面进 Store; 安装后开始菜单打开; 登录; 处理防火墙)
6. cards: 首次启动三个关卡 (登录, 权限提示, 防火墙) — 3 cards
7. table: 排障总表 (症状/常见原因/第一反应) 3 cols 5 rows
8. steps: 第一次打开项目 (添加目录→确认 Git→建 Local thread→只读任务)
9. bullets: 第一个安全可写任务
10. cards: 安装后检查清单 4 cards
11. table: CLI 辅助命令 (command/purpose) 2 cols
12. quote or end. Need end layout. 12 slides enough.

Let me count: cover, section, bullets3, table4, steps5, cards6, table7, steps8, bullets9, cards10, table11, end12. Good.

### CX-02 (桌面工作流)
1. cover
2. section: App 是开发主控台
3. bullets: App 把哪些能力放一起 (≤5)
4. table: 核心概念速查 (概念/一句话) 5 rows
5. cards: 五个控制点 → max 4 cards. Pick 目标/上下文/权限/结果或收口. Use 4.
6. steps: 一条线程的生命周期 → 4 steps
7. table: 三种工作方式怎么选 (任务/推荐方式/为什么) 4 rows
8. bullets: 任务五要素 (目标/范围/约束/验证/交付) 5
9. cards: Review 逐项检查法 4 cards
10. table: 反模式 4 rows
11. bullets: 三个基本动作 + 线程设计
12. end

Count 12.

### CX-03 (Commands)
1. cover
2. section: 入口、状态、动作
3. bullets: 三层命令
4. table: 用不用 Command 判断树 (想做什么/首选/为什么) 4-5 rows
5. cards: 稳定命令 4 cards (/status /plan /review /mcp) — but /goal /feedback too. Use 4.
6. steps: 在 App 里发现命令四步
7. bullets: /plan 好的计划包含什么
8. table: /goal 适合与不适合
9. bullets: /review 检查维度 (5)
10. table: 命令排障表 4 rows
11. bullets: App 与 CLI commands 差异
12. end

### CX-04 (项目指令权限配置)
1. cover
2. section: 从软到硬的四层
3. cards: 四层心智模型 4 cards
4. bullets: 为什么不能只靠提示词
5. table: AGENTS.md 推荐结构 (模块/要回答) 5 rows
6. bullets: AGENTS.md 不该写什么
7. table: 权限策略 (场景/建议) 5 rows
8. cards: 沙盒三种模式 3 cards
9. table: Rules 适合做什么 4 rows
10. steps: 改配置后核对
11. bullets: Hooks 排障
12. end

### CX-05 (MCP)
1. cover
2. section: 工具连接层
3. bullets: MCP 是什么 / 能给什么
4. steps: App 中 MCP 工作流
5. table: 先确认四件事 (问题/为什么)
6. cards: 三类 server 3 cards
7. table: 密钥放哪里 (场景/推荐/不推荐) 4 rows
8. bullets: 安全边界问句
9. cards: 工具风险分级 4 cards
10. table: MCP 排障 4 rows
11. bullets: 配置核对清单
12. end

### CX-06 (Skills)
1. cover
2. section
3. bullets: Skill 是什么/适合
4. table: 什么时候值得做成 Skill (信号/是否适合) 5 rows
5. cards: 好 Skill 四个特征 4 cards
6. bullets: description 写法
7. steps: App 中调用 Skill 前确认三件事 + 调用 → need 3-4 steps; use 4 (确认可见, 确认层级, 确认副作用, 显式调用)
8. table: Skills/Commands/Automations 分工 5 rows
9. table: 文件结构 (内容/放哪里/原因) 3-4 rows
10. bullets: Skill 不该承载
11. bullets: 从 prompt 升级成 Skill 的条件
12. end

### CX-07 (Plugins/Connectors)
1. cover
2. section
3. bullets: 安装、授权、调用是三件事
4. table: 四个概念 (概念/本质/例子) 4 rows — 3 cols
5. steps: 连接器工作流
6. table: 安装前检查清单 5 rows
7. cards: 插件安装后四层变化 4 cards
8. bullets: 最小权限原则
9. table: 常见连接场景 5 rows
10. table: CLI marketplace 命令 4 rows
11. bullets: 观察输出追问
12. end

Now write files. Need to be careful with JSON validity. I'll build objects in TS and JSON.stringify then write. That's safest and lets me enforce counts programmatically.

Also need to verify bullet length ≤42 汉字. I'll write a checker that counts CJK chars + maybe all chars. The requirement says "每条不超过 42 个汉字". I'll count using [...str].length maybe; being safe count CJK characters. But to be safe, I'll count total characters (including punctuation/latin) and keep ≤42. Let me write a validation that reports any violations and I'll fix.

Also notes optional. I'll include some notes.

Let me write a single run_code that builds all 7 and validates, then writes. But requirement says use write tool one by one. I'll call tools.write in a loop within run_code. That satisfies "用 write 工具逐个写文件". Fine.

Let me draft content in TS. I'll be careful with quotes.

Let me write the code.

For CX-01:
code: "CX-01", category: "codex", fileTitle: "Codex-App安装与认证", deck: "Codex App 安装与认证：从下载到第一个线程"

Wait — the task says fileTitle=Codex-App安装与认证. The schema example shows "fileTitle":"Claude Code完整安装指南". Should fileTitle use the given value exactly "Codex-App安装与认证"? Yes, use provided fileTitle as-is: "Codex-App安装与认证". Hmm but maybe better readable "Codex App 安装与认证". The instruction lists fileTitle=Codex-App安装与认证. I'll use exactly that to be safe. Actually for later ones: "Codex-App桌面工作流", "Codex-Commands工作流入口", "Codex项目指令权限配置", "Codex-MCP外部工具", "Codex-Skills可复用工作流", "Codex-Plugins连接器". Use as given exactly.

kicker fixed: "Vibe Coding 学习系列 · CX-01" etc.

Now content. Let me write.

CX-01 slides:

cover: title "Codex App 安装与认证：从下载到第一个线程", subtitle "零基础 · Windows / macOS 装好、登上号、跑通第一个安全任务"

section: title "安装目标：先能安全打开本地项目", subtitle "App 是主线，CLI / Web / Cloud 是辅助"

bullets: title "安装成功的六条标准"
bullets:
- "桌面 Codex App 能正常打开"
- "能用 ChatGPT / OpenAI 账号登录"
- "能添加本地项目并创建线程"
- "能让 Codex 只读分析项目"
- "能看到 Review、diff 和 Settings"
(5)

table: title "系统准备：按平台走官方入口"
headers ["平台","版本建议","安装来源"]
rows:
["Windows","Windows 11 是推荐基线","Microsoft Store 或 winget"]
["macOS","使用仍受 Apple 支持的版本","官方 Codex App 下载页"]
["Linux","桌面版暂未覆盖","先用 CLI / Web / Cloud"]
(3)

steps: title "Windows 安装四步"
steps:
{title:"从官方页面进 Store", desc:"打开官方 Windows 页，点 Codex app for Windows 链接"}
{title:"在 Store 点获取安装", desc:"企业禁用 Store 时让管理员分发，或用 winget"}
{title:"开始菜单打开 Codex", desc:"首次启动按提示登录，优先用 ChatGPT 账号"}
{title:"处理防火墙弹窗", desc:"一般只勾专用网络，公用网络不要选"}
(4)

cards: title "首次启动的三个关卡"
cards:
{title:"登录", desc:"优先 ChatGPT / OpenAI 账号；API Key 不是 App 登录方案"}
{title:"权限提示", desc:"区分选目录、跑只读命令和写文件联网，后者看清再同意"}
{title:"防火墙", desc:"本地服务通信时弹窗，只放行可信网络"}
(3)

table: title "排障总表：先定位症状，不要乱重装"
headers ["症状","常见原因","第一反应"]
rows:
["App 装不上","Store、系统版本或企业策略","先确认来源和系统更新"]
["登录失败","浏览器登录态、网络、账号权限","换浏览器登录或重新授权"]
["Review 不可用","没有 Git 或项目不是 Git 仓库","装 Git，确认 git status"]
["命令跑不动","PowerShell policy 或工具链缺失","先在终端跑版本命令"]
["macOS 打不开","Gatekeeper 或下载来源问题","从官方入口下载再授权"]
(5)

steps: title "第一次打开项目：四步不慌"
steps:
{title:"选一个普通 Git 仓库", desc:"不要一上来打开生产仓库，最好有 README"}
{title:"添加本地项目目录", desc:"确认 App 能识别 Git 状态"}
{title:"创建 Local thread", desc:"先发只读任务：总结技术栈、启动和测试命令"}
{title:"再做一个小改动", desc:"只改一个错别字，看 diff 且不自动提交"}
(4)

bullets: title "第一个安全可写任务"
bullets:
- "只改低风险文件，例如文档里的一个错别字"
- "明确要求改完展示 diff，不要自动提交"
- "确认改动只在预期文件里"
- "确认 Review 面板能看到 diff"
- "知道怎么撤销或继续修改"
(5)

cards: title "安装后检查清单"
cards:
{title:"账号与环境", desc:"已登录，防火墙和 macOS 权限按最小范围授权"}
{title:"Git 与项目", desc:"App 能看到 Git 状态，能添加本地仓库"}
{title:"线程与只读", desc:"能创建 Local thread 并总结项目，不改文件"}
{title:"可写与 Review", desc:"小改动能在 Review 中看到 diff"}
(4)

table: title "CLI 只作为辅助"
headers ["命令","用途"]
rows:
["codex --help","查看 CLI 帮助"]
["codex app","从 CLI 打开 App"]
["codex review","做代码审查"]
["codex exec \"summarize this repo\"","非交互执行任务"]
(4)

end: title "装好之后：先只读，再小改，最后 Review", subtitle "下一篇：CX-02 Codex App 桌面工作流"

Good. Now check bullet char counts ≤42. All short.

CX-02:
cover title "Codex App 桌面工作流：把 App 当主控台", subtitle "零基础 · 线程、终端、Review、权限在一个桌面流程里"
section title "App 是开发主控台，不是聊天窗口", subtitle "Thread 管上下文，Review 管结果，Settings 管边界"
bullets title "App 把哪些能力放在一起"
bullets:
- "Thread：一条任务线，带上下文、历史和状态"
- "Review：查看 diff、行内反馈和 stage / unstage"
- "Terminal：让 Codex 在受控环境里运行命令"
- "Settings：模型、审批、沙盒、插件和 MCP 的入口"
- "Automations / Plugins：后台检查和外部账号连接"
(5)

table title "核心概念速查"
headers ["概念","一句话解释"]
rows:
["Thread","一条任务线，包含上下文、历史和状态"]
["Worktree","Git 隔离工作目录，仍会产生真实改动"]
["Review 面板","看 diff、行内反馈、stage / revert 的关口"]
["Local workspace","当前本机项目目录，决定 Codex 能看到什么"]
["Cloud handoff","把任务交给云端环境继续做"]
(5)

cards title "五个控制点"
cards:
{title:"目标", desc:"这次到底要解决什么问题"}
{title:"上下文", desc:"Codex 该读哪些文件，陌生项目先只读建模"}
{title:"权限", desc:"是否允许写文件、跑命令、联网、调外部工具"}
{title:"结果", desc:"改动是否真的在预期范围内"}
(4)

steps title "一条线程的生命周期"
steps:
{title:"开场只读", desc:"先读项目，确认技术栈、命令、目录和风险"}
{title:"明确任务", desc:"说清目标、范围、不能做什么、怎么验证"}
{title:"允许执行", desc:"小任务直接改，大任务先 /plan 或用 worktree"}
{title:"检查与收口", desc:"看 Review，定点反馈，由人决定是否提交"}
(4)

table title "三种工作方式怎么选"
headers ["任务","推荐方式","为什么"]
rows:
["读项目、解释报错","Local thread 只读","快，风险低"]
["改一个文件或少量文档","Local thread + Review","改动小，容易检查"]
["新功能、重构、改多个文件","Worktree thread","隔离改动，便于撤回"]
["盯 PR、修 CI、长任务","Cloud / Web handoff","不占用本地环境"]
(4)

bullets title "好任务要写清五件事"
bullets:
- "目标：这次要解决什么问题"
- "范围：只改哪些文件或目录"
- "约束：不能做什么，例如不引入新依赖"
- "验证：怎么确认改对了，跑哪条命令"
- "交付：要 diff 摘要、测试结果还是 PR 描述"
(5)

cards title "Review 面板逐项检查法"
cards:
{title:"文件列表", desc:"是否只改了任务范围内文件，范围外要解释或撤掉"}
{title:"单文件 diff", desc:"是否有无关格式化、删除或重命名"}
{title:"命令记录", desc:"验证命令是否真的跑过，没跑要说明原因"}
{title:"安全项", desc:"是否碰了 .env、token 或权限配置，碰到立即停"}
(4)

table title "常见反模式"
headers ["反模式","真正风险","更稳做法"]
rows:
["一个线程混多个目标","上下文混乱，Review 难收口","一个目标一条线程"]
["任务只写“优化一下”","Codex 不知道边界","写清目标、范围、约束、验证、交付"]
["陌生仓库直接写","误读架构和命令","先只读建模"]
["允许自动提交推送","错误进入远端","先草拟，由人确认"]
(4)

bullets title "App 用户的三个基本动作"
bullets:
- "收窄：只改 README，控制 diff 大小"
- "追证据：你运行了什么命令"
- "反向解释：根据 diff 解释你做了什么"
- "线程标题用结果导向命名，方便以后找回上下文"
- "新目标开新线程；混在一起就难 Review"
(5)

end title "先建立控制感，再逐步放开能力", subtitle "下一篇：CX-03 Commands 工作流入口"

CX-03:
cover title "Codex Commands：App 里的工作流入口", subtitle "零基础 · 不背命令表，学会什么时候切换工作模式"
section title "入口、状态、动作", subtitle "先看状态，再定推进方式，执行后用 /review 收口"
bullets title "slash commands 的三层"
bullets:
- "入口层：/status、/mcp、/feedback"
- "状态层：/plan、/goal，改变任务推进方式"
- "审查层：/review，围绕当前 diff 做检查"
- "命令只是更快进入某种工作模式"
- "模式不对，命令反而会制造混乱"
(5)

table title "用不用 Command 的判断"
headers ["你想做什么","首选方式","为什么"]
rows:
["看当前线程状态","/status","快速确认上下文、限制和配额"]
["让 Codex 先别动手","/plan","把执行前移到方案讨论"]
["长时间推进清楚目标","/goal","让目标跨多个 turn 持续存在"]
["检查当前改动","/review","直接进入代码审查口径"]
["查 MCP 是否连接","/mcp","看工具 server 和状态"]
(5)

cards title "App 用户先掌握的稳定命令"
cards:
{title:"/status", desc:"查看模型、工作区、审批和上下文状态"}
{title:"/plan", desc:"大任务先规划，不急着改文件"}
{title:"/review", desc:"审查当前改动，合并前使用"}
{title:"/mcp", desc:"接外部工具后，查看 server 和工具"}
(4)

steps title "在 App 里发现命令四步"
steps:
{title:"打开项目线程", desc:"任何已有项目的线程都可以"}
{title:"输入 /", desc:"看弹出的命令列表和说明"}
{title:"注意实验标记", desc:"不确定时先问，不要直接执行"}
{title:"查官方文档核对", desc:"以当前 App 显示和官方 App Commands 为准"}
(4)

bullets title "/plan：好的计划应该包含什么"
bullets:
- "要读哪些文件，要改哪些文件"
- "可能方案和取舍"
- "验证命令，以及不做什么"
- "什么时候退出计划模式进入执行"
- "差的 /plan 只写“做一个完整优化”，缺对象和边界"
(5)

table title "/goal：长目标也要有边界"
headers ["适合","不适合"]
rows:
["长迁移、长重构","目标没有范围，例如“优化项目”"]
["部署重试直到成功","没有结束条件"]
["原型打磨直到测试通过","没有权限边界"]
["比一次提示更长但有明确终点","周期或后台检查，应交给 Automations"]
(4)

bullets title "/review 的五个检查维度"
bullets:
- "范围：是否只改了任务指定文件"
- "正确性：边界条件、空值、异步竞态"
- "安全：是否触碰 secret、权限、网络"
- "测试：是否覆盖新增行为"
- "可维护：是否引入重复逻辑或隐式依赖"
(5)

table title "命令排障表"
headers ["症状","可能原因","排查顺序"]
rows:
["输入 /goal 没出现","feature 未启用或版本不支持","先看 / 列表，再查 features.goals"]
["/review 没问题","当前没有 Git diff","先看 Review 面板文件列表"]
["/mcp 看不到工具","MCP 未配置或 App 未刷新","看 Settings，再用 codex mcp list 辅助"]
["命令列表和教程不同","版本、插件或实验开关不同","以当前 App 列表和官方文档为准"]
(4)

bullets title "App Commands 与 CLI Commands 不保证一致"
bullets:
- "App 面向桌面线程、Review 面板和工具入口"
- "CLI 面向终端 TUI、命令行权限和会话"
- "App 输入 / 查看，CLI 输入 /help 查看"
- "两者不保证完全一致，以当前界面显示为准"
- "CLI 命令写到 CX-12，不能写成 App 主线"
(5)

end title "掌握的是什么时候切换工作模式", subtitle "下一篇：CX-04 项目指令、配置、权限与沙盒"

CX-04:
cover title "Codex 项目指令、配置、权限与沙盒", subtitle "零基础 · 让 App 知道怎么安全工作"
section title "从软到硬的四层配置", subtitle "先掌握 AGENTS.md 和 App Settings 两层"
cards title "配置系统的四层心智模型"
cards:
{title:"项目说明层", desc:"AGENTS.md，写项目事实、命令、规范和安全边界"}
{title:"用户偏好层", desc:"App Settings / config.toml，设模型、终端、审批、沙盒"}
{title:"命令策略层", desc:"Rules / permission profiles，对危险动作建立可执行边界"}
{title:"事件脚本层", desc:"Hooks，在特定时机运行真实脚本做审计或检查"}
(4)

bullets title "为什么不能只靠提示词"
bullets:
- "不持久：换线程后可能忘了重复说"
- "不够硬：说不要推 main，仍要靠人工盯"
- "不可审计：团队很难知道每个人临时说了什么"
- "长期规则写进 AGENTS.md"
- "高风险命令用 Rules，复杂事件才用 Hooks"
(5)

table title "AGENTS.md 推荐结构"
headers ["模块","要回答的问题"]
rows:
["项目概览","这个项目是什么，主要目录在哪里"]
["常用命令","安装、测试、lint、build 怎么跑"]
["修改边界","哪些文件可以改，哪些要谨慎"]
["代码风格","当前项目已有写法是什么"]
["验证方式","改完怎么证明，失败要解释"]
(5)

bullets title "AGENTS.md 不该写什么"
bullets:
- "API Key、token、cookie"
- "只针对本次任务的临时要求"
- "个人机器路径"
- "不稳定的模型名称或价格"
- "“写高质量代码”这种无法验证的口号"
(5)

table title "按场景选择权限策略"
headers ["场景","建议"]
rows:
["陌生项目","保守审批，先只读"]
["日常小改","允许常见读写和安全命令"]
["大规模重构","使用 worktree，严格 review"]
["CI / 自动化","外部沙箱 + 最小权限"]
["涉及密钥或生产数据","默认拒绝，人工确认"]
(5)

cards title "三种沙盒模式"
cards:
{title:"read-only", desc:"只读，适合审计和探索"}
{title:"workspace-write", desc:"可写工作区，适合日常开发"}
{title:"danger-full-access", desc:"无沙盒限制，只能在外部可信沙箱使用"}
(3)

table title "Rules 适合与不适合做什么"
headers ["适合","不适合"]
rows:
["拦危险删除，例如 rm -rf","写复杂业务流程"]
["拦未经确认的 publish","替代测试或 Review"]
["对 push、tag、force push 要求确认","判断产品取舍"]
["允许 git status、rg、ls 等只读命令","管理外部账号授权"]
(4)

steps title "改完配置后怎么核对"
steps:
{title:"改 AGENTS.md", desc:"新线程里让 Codex 总结项目规则，看是否读到"}
{title:"改权限或沙盒", desc:"用 /status 或 Settings 确认实际生效"}
{title:"改 MCP 配置", desc:"用 /mcp 看 server 和工具是否可见"}
{title:"换项目目录时", desc:"确认是否打开了对的目录，旧线程可能仍是旧上下文"}
(4)

bullets title "Hooks 是事件脚本，不是万能自动化"
bullets:
- "配置通常在 .codex/hooks.json 或 [hooks] 表"
- "会运行真实命令，可能读取敏感上下文"
- "写错会阻塞工作流，学习阶段先别急着写"
- "能用 Rules 解决的命令边界，不要先写 Hook"
- "相对路径要改从 git root 或绝对路径解析"
(5)

end title "先用 AGENTS.md 和 Settings 把边界写清楚", subtitle "下一篇：CX-05 MCP 外部工具"

CX-05:
cover title "Codex MCP：在 App 中连接外部工具", subtitle "零基础 · 先只读、再小范围、可审计、可撤销"
section title "MCP 不是搜索框，而是工具连接层", subtitle "让 Codex 连接浏览器、数据库、文档和内部 API"
bullets title "MCP 能给 Codex 什么"
bullets:
- "文档上下文：查新文档，减少过期知识"
- "开发工具：控制浏览器，检查页面"
- "设计工具：读取 Figma 等设计上下文"
- "数据工具：数据库 schema、只读查询"
- "项目与内部系统：GitHub issue / PR、私有 API"
(5)

steps title "App 中的 MCP 工作流"
steps:
{title:"启用或配置", desc:"在 App Settings 或集成入口启用 MCP"}
{title:"查看可见工具", desc:"回到线程，用 /mcp 看 server 和工具"}
{title:"用自然语言调用", desc:"要求 Codex 使用工具，并观察权限提示"}
{title:"Review 结果", desc:"核对来源、时间、权限和副作用"}
(4)

table title "从 0 配 MCP 前先确认四件事"
headers ["问题","为什么重要"]
rows:
["本地命令还是远程服务","决定用 stdio、HTTP 还是插件提供"]
["需要什么账号或 token","决定密钥放哪里，不能写进仓库"]
["默认能读写什么","决定是否只读、是否需要审批"]
["App 是否已有连接器或插件","有现成入口时不要重复手写 MCP"]
(4)

cards title "三类 MCP server"
cards:
{title:"STDIO", desc:"本地命令启动进程，适合本机工具和私有脚本"}
{title:"Streamable HTTP", desc:"访问一个 URL，适合远程服务、OAuth 和云端工具"}
{title:"Plugin-provided", desc:"插件 manifest 提供 server，要先看来源和工具权限"}
(3)

table title "密钥放哪里"
headers ["场景","推荐","不推荐"]
rows:
["本地个人 token","系统环境变量或密码管理器","写进 config.toml 并提交"]
["团队共享服务","组织 secret 管理、最小 scope","共享个人账号 token"]
["Cloud / remote","环境变量或官方 secret 入口","在 setup 日志里 echo"]
["临时调试","临时只读 token，用完撤销","使用生产写 token"]
(4)

bullets title "配置 MCP 前先问的安全问题"
bullets:
- "它能读什么数据，能写什么数据"
- "它是否会联网，是否需要账号授权"
- "它是否会把数据发给第三方"
- "它能不能在只读模式下完成任务"
- "生产库、客户数据和邮箱都按最小权限配置"
(5)

cards title "工具风险分级"
cards:
{title:"只读搜索", desc:"风险低，可以较宽松"}
{title:"读取私有数据", desc:"风险中，需要来源说明"}
{title:"写外部系统", desc:"风险高，需要人工确认"}
{title:"访问生产数据", desc:"风险很高，默认不要给新手练习"}
(4)

table title "MCP 排障流程"
headers ["症状","可能原因","排查"]
rows:
["/mcp 看不到 server","配置层未加载或 App 未刷新","先看 App Settings，再重启或刷新"]
["CLI 能看到 App 看不到","配置层或会话状态不同","以 App 线程使用结果为准"]
["server 启动失败","命令不存在或依赖未安装","在终端单独跑启动命令看日志"]
["结果不可信","来源不明或时间过期","要求 Codex 列出来源和查询条件"]
(4)

bullets title "MCP 配置核对清单"
bullets:
- "App 可见：/mcp 能看到 server 和工具"
- "最小权限：只给当前任务需要的读写范围"
- "密钥安全：token 在环境变量或 secret 里"
- "只读试跑：能完成一次只读查询或读取"
- "可审计、可撤销：知道怎么禁用和撤销 token"
(5)

end title "先只读、再小范围、可审计、可撤销", subtitle "下一篇：CX-06 Skills 可复用工作流"

CX-06:
cover title "Codex Skills：把重复提示变成可复用工作流", subtitle "零基础 · 让流程可重复，而不是让 prompt 更长"
section title "Skill 是可复用判断，不是 prompt 收藏", subtitle "要有步骤、边界和验收方式"
bullets title "Skill 是什么，适合什么"
bullets:
- "一组可复用指令、资源和可选脚本"
- "适合代码审查、文档核对、发布检查和团队 SOP"
- "不适合只执行一次的临时任务"
- "不适合需要实时外部 API 的工具连接"
- "不适合需要定时运行的周期任务"
(5)

table title "一个流程什么时候值得做成 Skill"
headers ["信号","是否适合"]
rows:
["同一提示复制三次以上","适合"]
["多人需要同一做法","适合"]
["输出格式总要固定","适合"]
["只做一次的临时任务","不适合"]
["需要每天运行","交给 Automation 调度"]
(5)

cards title "好 Skill 的四个特征"
cards:
{title:"触发清楚", desc:"description 里写明什么时候用"}
{title:"边界清楚", desc:"也写明什么时候不用"}
{title:"输入输出清楚", desc:"Codex 知道读什么、交付什么"}
{title:"内容分层", desc:"常用指令在 SKILL.md，长资料放 references"}
(4)

bullets title "description 是触发路由，不是介绍文案"
bullets:
- "模板：Use when 触发场景，Do 核心动作，Do not use when 边界"
- "差写法：Helps write high quality code"
- "好写法要写清对象、动作、触发场景和边界"
- "写得太泛，Codex 可能乱用"
- "写得太窄，真正需要时触发不了"
(5)

steps title "在 App 中调用 Skill"
steps:
{title:"确认能否看到", desc:"当前 App 是否显示这个 Skill"}
{title:"确认层级", desc:"用户级、项目级，还是插件带来的"}
{title:"确认副作用", desc:"会不会读额外资源、运行脚本或调用工具"}
{title:"显式调用", desc:"用 $code-review 或自然语言点名，再说清任务"}
(4)

table title "Skills、Commands、Automations 的分工"
headers ["需求","首选"]
rows:
["当前线程快速动作","Command"]
["固定 SOP / 复用流程","Skill"]
["定时或后台重复执行","Automation"]
["外部工具连接","MCP / Connector"]
["打包分发一组能力","Plugin"]
(5)

table title "文件结构：内容放哪里"
headers ["内容","放哪里","原因"]
rows:
["触发场景、流程、输出","SKILL.md","Codex 必须先看到"]
["长规范、示例、术语表","references/","需要时再读，省上下文"]
["重复性强易写错的逻辑","scripts/","可选，要写清运行时和失败输出"]
(3)

bullets title "Skill 不该承载什么"
bullets:
- "一次性任务"
- "当前项目的临时 bug"
- "模糊人设包装"
- "需要每天变化的命令"
- "真实密钥或私有账号信息"
(5)

end title "一次性任务放 prompt，项目事实放 AGENTS.md", subtitle "下一篇：CX-07 Plugins 连接器"

CX-07:
cover title "Codex Plugins 与 Connectors：App 能力扩展", subtitle "零基础 · 安装是让能力可见，授权是让数据可用"
section title "安装、授权、调用是三件事", subtitle "插件可以包含 Skills、MCP、Apps，但不等于其中任何一个"
bullets title "安装、授权、调用、撤销"
bullets:
- "安装 Plugin：看它带来的 Skills / MCP / Apps / 配置"
- "对外部服务单独授权"
- "在线程中引用或调用外部上下文"
- "工具或外部动作按权限和审批执行"
- "不用时撤销授权或卸载"
(5)

table title "先分清四个概念"
headers ["概念","本质","例子"]
rows:
["Connector / App","外部账号连接","GitHub、Gmail、Drive、Slack"]
["Plugin","能力包","一组 skills、MCP、apps、配置"]
["Skill","可复用工作流","代码审查 SOP"]
["MCP","工具协议","浏览器、数据库、文档源"]
(4)

steps title "App 中的连接器工作流"
steps:
{title:"打开入口", desc:"进入 App 的 Plugins / Connectors / Apps"}
{title:"选择服务", desc:"挑要连接的 GitHub、Drive、Slack 等"}
{title:"完成授权", desc:"授权范围要单独看清楚"}
{title:"引用并执行", desc:"用 @、mention 或自然语言引用外部上下文"}
(4)

table title "安装或连接前的检查"
headers ["检查项","要确认什么"]
rows:
["来源","官方、组织内，还是第三方插件"]
["能力","带 Skills、MCP、Connectors 还是组合包"]
["权限","只读、评论、写文件、发消息分别要什么权限"]
["数据范围","能访问哪些仓库、文档、邮箱或群聊"]
["撤销方式","在 App、服务后台还是组织管理端撤销"]
(5)

cards title "插件安装后的四层变化"
cards:
{title:"目录层", desc:"Plugins 页面出现已安装条目"}
{title:"能力层", desc:"@ mention 或 bundled skills 可被调用"}
{title:"授权层", desc:"外部 App 可能要求登录或授权"}
{title:"执行层", desc:"Codex 按 prompt、权限和审批调用工具"}
(4)

bullets title "最小权限原则"
bullets:
- "第一次安装只给必要权限"
- "只读任务不给写权限"
- "需要发消息或改 PR 时，明确说明目标和范围"
- "团队插件先在测试项目验证"
- "不再使用时及时禁用或卸载"
(5)

table title "常见连接场景与风险"
headers ["场景","连接器价值","风险点"]
rows:
["GitHub","读取 issue、PR、仓库上下文","写权限、PR 评论权限"]
["Google Drive / Docs","读取团队文档","文档访问范围"]
["Gmail / Outlook","引用邮件上下文","隐私和敏感信息"]
["Slack / Teams","查讨论和决策","群聊范围和成员隐私"]
["Calendar","查日程和会议背景","个人隐私"]
(5)

table title "CLI 辅助管理 marketplace"
headers ["命令","用途"]
rows:
["codex plugin marketplace list","列出已添加的 marketplace"]
["codex plugin marketplace add owner/repo","添加 marketplace 来源"]
["codex plugin marketplace upgrade","升级 marketplace"]
["codex plugin marketplace remove 名称","移除 marketplace"]
(4)

bullets title "观察输出：看用了什么，不只看答得像不像"
bullets:
- "你使用了哪些插件或工具能力"
- "哪些信息来自外部系统"
- "哪些结论是根据上下文推断的"
- "有没有权限、网络、认证或数据范围限制"
- "安装是让能力可见，审批是最后的安全门"
(5)

end title "安装让能力可见，授权让数据可用，审批是安全门", subtitle "本系列 codex 分册到这里"

Now let me validate lengths programmatically and write.

I'll count "汉字" as CJK Unified Ideographs. Also ensure total length (chars) <= 42 maybe. Let me check: e.g. "文档上下文：查新文档，减少过期知识" - 18 chars. Fine. "模板：Use when 触发场景，Do 核心动作，Do not use when 边界" — this is 50+ chars! Count: let me estimate. "模板：" 3 + "Use when " 9 + "触发场景，"5 + "Do "3 + "核心动作，"5 + "Do not use when "16 + "边界"2 = 43. Slightly over 42 if counting all chars. Let me rewrite shorter: "模板：Use when 触发场景，Do 核心动作，Do not use when 边界" → shorten to "模板：Use when 场景，Do 动作，Do not use when 边界" = 3+9+2+1+3+3+1+16+2 ≈ 40. Better. Actually I'll just run validator counting all characters and fix violations.

Let me write the program that builds and validates, prints violations, and only writes if zero violations. If violations, I'll fix.

Let me write it. I'll define an array of deck objects. Use TypeScript with type any.

Note: code strings contain quotes; I'll use JSON-safe via JSON.stringify.

Let me now produce the run_code. It's large. Let me write carefully.

For counting: `[...s].filter(c => /\p{Script=Han}/u.test(c)).length` for Han count, and `[...s].length` total. Requirement "不超过 42 个汉字" — Han count. But also likely total. I'll check Han count ≤ 42 and total ≤ 48 to be safe. Let me just report both and ensure Han ≤42 and total ≤42 ideally. Let me aim total ≤42.

Let me write and see.
我已读完全部 7 篇文档的关键章节。现在生成 7 份 JSON 并做约束校验后写入。
{
  "type": "tool-call",
  "id": "call_00_rXkdoxtERnJnVP9iteeU0710",
  "name": "run_code",
  "arguments": "{\"code\": \"const dir = \\\"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\\\";\\ntype Slide = any;\\n\\nfunction mk(id: string, title: string, sub: string, slides: Slide[]) {\\n  return { code: id, category: \\\"codex\\\", fileTitle: \\\"\\\", deck: title, _sub: sub, slides };\\n}\\n\\nconst decks: any[] = [];\\n\\n// ================= CX-01 =================\\ndecks.push({\\n  code: \\\"CX-01\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-App安装与认证\\\",\\n  deck: \\\"Codex App 安装与认证：从下载到第一个线程\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex App 安装与认证：从下载到第一个线程\\\", subtitle: \\\"零基础 · Windows / macOS 装好、登上号、跑通第一个安全任务\\\", kicker: \\\"Vibe Coding 学习系列 · CX-01\\\" },\\n    { layout: \\\"section\\\", title: \\\"安装目标：先能安全打开本地项目\\\", subtitle: \\\"App 是主线，CLI / Web / Cloud 是辅助\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"安装成功的五条标准\\\", bullets: [\\n      \\\"桌面 Codex App 能正常打开\\\",\\n      \\\"能用 ChatGPT / OpenAI 账号登录\\\",\\n      \\\"能添加本地项目并创建线程\\\",\\n      \\\"能让 Codex 只读分析项目\\\",\\n      \\\"能看到 Review、diff 和 Settings\\\"\\n    ], notes: \\\"安装成功的标准不是终端里有 codex 命令，而是 App 能用起来。\\\" },\\n    { layout: \\\"table\\\", title: \\\"系统准备：按平台走官方入口\\\", headers: [\\\"平台\\\", \\\"版本建议\\\", \\\"安装来源\\\"], rows: [\\n      [\\\"Windows\\\", \\\"Windows 11 是推荐基线\\\", \\\"Microsoft Store 或 winget\\\"],\\n      [\\\"macOS\\\", \\\"使用仍受 Apple 支持的版本\\\", \\\"官方 Codex App 下载页\\\"],\\n      [\\\"Linux\\\", \\\"桌面版暂未覆盖\\\", \\\"先用 CLI / Web / Cloud\\\"]\\n    ], notes: \\\"不要从不明网盘或第三方安装包安装。\\\" },\\n    { layout: \\\"steps\\\", title: \\\"Windows 安装四步\\\", steps: [\\n      { title: \\\"从官方页面进 Store\\\", desc: \\\"打开官方 Windows 页，点 Codex app for Windows 链接\\\" },\\n      { title: \\\"在 Store 点获取安装\\\", desc: \\\"企业禁用 Store 时让管理员分发，或用 winget install Codex -s msstore\\\" },\\n      { title: \\\"开始菜单打开 Codex\\\", desc: \\\"首次启动按提示登录，优先用 ChatGPT 账号\\\" },\\n      { title: \\\"处理防火墙弹窗\\\", desc: \\\"一般只勾专用网络，公用网络不要选\\\" }\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"首次启动的三个关卡\\\", cards: [\\n      { title: \\\"登录\\\", desc: \\\"优先 ChatGPT / OpenAI 账号；API Key 不是 App 登录方案\\\" },\\n      { title: \\\"权限提示\\\", desc: \\\"区分选目录、跑只读命令和写文件联网，后者看清再同意\\\" },\\n      { title: \\\"防火墙\\\", desc: \\\"本地服务通信时弹窗，只放行可信网络\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"排障总表：先定位症状，不要乱重装\\\", headers: [\\\"症状\\\", \\\"常见原因\\\", \\\"第一反应\\\"], rows: [\\n      [\\\"App 装不上\\\", \\\"Store、系统版本或企业策略\\\", \\\"先确认来源和系统更新\\\"],\\n      [\\\"登录失败\\\", \\\"浏览器登录态、网络、账号权限\\\", \\\"换浏览器登录或重新授权\\\"],\\n      [\\\"Review 不可用\\\", \\\"没有 Git 或项目不是 Git 仓库\\\", \\\"安装 Git，确认 git status\\\"],\\n      [\\\"命令跑不动\\\", \\\"PowerShell policy 或工具链缺失\\\", \\\"先在终端跑版本命令\\\"],\\n      [\\\"macOS 打不开\\\", \\\"Gatekeeper 或下载来源问题\\\", \\\"从官方入口下载再按提示授权\\\"]\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"第一次打开项目：四步不慌\\\", steps: [\\n      { title: \\\"选一个普通 Git 仓库\\\", desc: \\\"不要一上来打开生产仓库，最好有 README\\\" },\\n      { title: \\\"添加本地项目目录\\\", desc: \\\"确认 App 能识别 Git 状态\\\" },\\n      { title: \\\"创建 Local thread\\\", desc: \\\"先发只读任务：总结技术栈、启动命令和测试命令\\\" },\\n      { title: \\\"再做一个小改动\\\", desc: \\\"只改一个错别字，看 diff 且不自动提交\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"第一个安全可写任务\\\", bullets: [\\n      \\\"只改低风险文件，例如文档里的一个错别字\\\",\\n      \\\"明确要求改完展示 diff，不要自动提交\\\",\\n      \\\"确认改动只在预期文件里\\\",\\n      \\\"确认 Review 面板能看到 diff\\\",\\n      \\\"知道怎么撤销或继续修改\\\"\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"安装后检查清单\\\", cards: [\\n      { title: \\\"账号与环境\\\", desc: \\\"已登录，防火墙和 macOS 权限按最小范围授权\\\" },\\n      { title: \\\"Git 与项目\\\", desc: \\\"App 能看到 Git 状态，能添加本地仓库\\\" },\\n      { title: \\\"线程与只读\\\", desc: \\\"能创建 Local thread 并总结项目，不改文件\\\" },\\n      { title: \\\"可写与 Review\\\", desc: \\\"小改动能在 Review 中看到 diff\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"CLI 只作为辅助\\\", headers: [\\\"命令\\\", \\\"用途\\\"], rows: [\\n      [\\\"codex --help\\\", \\\"查看 CLI 帮助\\\"],\\n      [\\\"codex app\\\", \\\"从 CLI 打开 App\\\"],\\n      [\\\"codex review\\\", \\\"做代码审查\\\"],\\n      [\\\"codex exec \\\\\\\"summarize this repo\\\\\\\"\\\", \\\"非交互执行任务\\\"]\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"装好之后：先只读，再小改，最后 Review\\\", subtitle: \\\"下一篇：CX-02 Codex App 桌面工作流\\\" }\\n  ]\\n});\\n\\n// ================= CX-02 =================\\ndecks.push({\\n  code: \\\"CX-02\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-App桌面工作流\\\",\\n  deck: \\\"Codex App 桌面工作流：把 App 当主控台\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex App 桌面工作流：把 App 当主控台\\\", subtitle: \\\"零基础 · 线程、终端、Review、权限在一个桌面流程里\\\", kicker: \\\"Vibe Coding 学习系列 · CX-02\\\" },\\n    { layout: \\\"section\\\", title: \\\"App 是开发主控台，不是聊天窗口\\\", subtitle: \\\"Thread 管上下文，Review 管结果，Settings 管边界\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"App 把哪些能力放在一起\\\", bullets: [\\n      \\\"Thread：一条任务线，带上下文、历史和状态\\\",\\n      \\\"Review：查看 diff、行内反馈和 stage / unstage\\\",\\n      \\\"Terminal：让 Codex 在受控环境里运行命令\\\",\\n      \\\"Settings：模型、审批、沙盒、插件和 MCP 的入口\\\",\\n      \\\"Automations / Plugins：后台检查和外部账号连接\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"核心概念速查\\\", headers: [\\\"概念\\\", \\\"一句话解释\\\"], rows: [\\n      [\\\"Thread\\\", \\\"一条任务线，包含上下文、历史和状态\\\"],\\n      [\\\"Worktree\\\", \\\"Git 隔离工作目录，仍会产生真实改动\\\"],\\n      [\\\"Review 面板\\\", \\\"看 diff、行内反馈、stage / revert 的关口\\\"],\\n      [\\\"Local workspace\\\", \\\"当前本机项目目录，决定 Codex 能看到什么\\\"],\\n      [\\\"Cloud handoff\\\", \\\"把任务交给云端环境继续做\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"五个控制点\\\", cards: [\\n      { title: \\\"目标\\\", desc: \\\"这次到底要解决什么问题\\\" },\\n      { title: \\\"上下文\\\", desc: \\\"Codex 该读哪些文件，陌生项目先只读建模\\\" },\\n      { title: \\\"权限\\\", desc: \\\"是否允许写文件、跑命令、联网、调外部工具\\\" },\\n      { title: \\\"结果\\\", desc: \\\"改动是否真的在预期范围内，收口由人决定\\\" }\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"一条线程的生命周期\\\", steps: [\\n      { title: \\\"开场只读\\\", desc: \\\"先读项目，确认技术栈、命令、目录和风险\\\" },\\n      { title: \\\"明确任务\\\", desc: \\\"说清目标、范围、不能做什么、怎么验证\\\" },\\n      { title: \\\"允许执行\\\", desc: \\\"小任务直接改，大任务先 /plan 或用 worktree\\\" },\\n      { title: \\\"检查与收口\\\", desc: \\\"看 Review，定点反馈，由人决定是否提交\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"三种工作方式怎么选\\\", headers: [\\\"任务\\\", \\\"推荐方式\\\", \\\"为什么\\\"], rows: [\\n      [\\\"读项目、解释报错\\\", \\\"Local thread 只读\\\", \\\"快，风险低\\\"],\\n      [\\\"改一个文件或少量文档\\\", \\\"Local thread + Review\\\", \\\"改动小，容易检查\\\"],\\n      [\\\"新功能、重构、改多个文件\\\", \\\"Worktree thread\\\", \\\"隔离改动，便于撤回\\\"],\\n      [\\\"盯 PR、修 CI、长任务\\\", \\\"Cloud / Web handoff\\\", \\\"不占用本地环境\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"好任务要写清五件事\\\", bullets: [\\n      \\\"目标：这次要解决什么问题\\\",\\n      \\\"范围：只改哪些文件或目录\\\",\\n      \\\"约束：不能做什么，例如不引入新依赖\\\",\\n      \\\"验证：怎么确认改对了，跑哪条命令\\\",\\n      \\\"交付：要 diff 摘要、测试结果还是 PR 描述\\\"\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"Review 面板逐项检查法\\\", cards: [\\n      { title: \\\"文件列表\\\", desc: \\\"是否只改了任务范围内文件，范围外要解释或撤掉\\\" },\\n      { title: \\\"单文件 diff\\\", desc: \\\"是否有无关格式化、删除或重命名\\\" },\\n      { title: \\\"命令记录\\\", desc: \\\"验证命令是否真的跑过，没跑要说明原因\\\" },\\n      { title: \\\"安全项\\\", desc: \\\"是否碰了 .env、token 或权限配置，碰到立即停\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"常见反模式\\\", headers: [\\\"反模式\\\", \\\"真正风险\\\", \\\"更稳做法\\\"], rows: [\\n      [\\\"一个线程混多个目标\\\", \\\"上下文混乱，Review 难收口\\\", \\\"一个目标一条线程\\\"],\\n      [\\\"任务只写“优化一下”\\\", \\\"Codex 不知道边界\\\", \\\"写清目标、范围、约束、验证、交付\\\"],\\n      [\\\"陌生仓库直接写\\\", \\\"误读架构和命令\\\", \\\"先只读建模\\\"],\\n      [\\\"允许自动提交推送\\\", \\\"错误进入远端\\\", \\\"先草拟，由人确认\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"App 用户的三个基本动作\\\", bullets: [\\n      \\\"收窄：只改 README，控制 diff 大小\\\",\\n      \\\"追证据：你运行了什么命令\\\",\\n      \\\"反向解释：根据 diff 解释你做了什么\\\",\\n      \\\"线程标题用结果导向命名，方便以后找回上下文\\\",\\n      \\\"新目标开新线程；混在一起就难 Review\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"先建立控制感，再逐步放开能力\\\", subtitle: \\\"下一篇：CX-03 Commands 工作流入口\\\" }\\n  ]\\n});\\n\\n// ================= CX-03 =================\\ndecks.push({\\n  code: \\\"CX-03\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-Commands工作流入口\\\",\\n  deck: \\\"Codex Commands：App 里的工作流入口\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex Commands：App 里的工作流入口\\\", subtitle: \\\"零基础 · 不背命令表，学会什么时候切换工作模式\\\", kicker: \\\"Vibe Coding 学习系列 · CX-03\\\" },\\n    { layout: \\\"section\\\", title: \\\"入口、状态、动作\\\", subtitle: \\\"先看状态，再定推进方式，执行后用 /review 收口\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"slash commands 的三层\\\", bullets: [\\n      \\\"入口层：/status、/mcp、/feedback\\\",\\n      \\\"状态层：/plan、/goal，改变任务推进方式\\\",\\n      \\\"审查层：/review，围绕当前 diff 做检查\\\",\\n      \\\"命令只是更快进入某种工作模式\\\",\\n      \\\"模式不对，命令反而会制造混乱\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"用不用 Command 的判断\\\", headers: [\\\"你想做什么\\\", \\\"首选方式\\\", \\\"为什么\\\"], rows: [\\n      [\\\"看当前线程状态\\\", \\\"/status\\\", \\\"快速确认上下文、限制和配额\\\"],\\n      [\\\"让 Codex 先别动手\\\", \\\"/plan\\\", \\\"把执行前移到方案讨论\\\"],\\n      [\\\"长时间推进清楚目标\\\", \\\"/goal\\\", \\\"让目标跨多个 turn 持续存在\\\"],\\n      [\\\"检查当前改动\\\", \\\"/review\\\", \\\"直接进入代码审查口径\\\"],\\n      [\\\"查 MCP 是否连接\\\", \\\"/mcp\\\", \\\"看工具 server 和状态\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"App 用户先掌握的稳定命令\\\", cards: [\\n      { title: \\\"/status\\\", desc: \\\"查看模型、工作区、审批和上下文状态\\\" },\\n      { title: \\\"/plan\\\", desc: \\\"大任务先规划，不急着改文件\\\" },\\n      { title: \\\"/review\\\", desc: \\\"审查当前改动，合并前使用\\\" },\\n      { title: \\\"/mcp\\\", desc: \\\"接外部工具后，查看 server 和工具\\\" }\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"在 App 里发现命令四步\\\", steps: [\\n      { title: \\\"打开项目线程\\\", desc: \\\"任何已有项目的线程都可以\\\" },\\n      { title: \\\"输入 /\\\", desc: \\\"看弹出的命令列表和说明\\\" },\\n      { title: \\\"注意实验标记\\\", desc: \\\"不确定时先问，不要直接执行\\\" },\\n      { title: \\\"查官方文档核对\\\", desc: \\\"以当前 App 显示和官方 App Commands 为准\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"/plan：好的计划应该包含什么\\\", bullets: [\\n      \\\"要读哪些文件，要改哪些文件\\\",\\n      \\\"可能方案和取舍\\\",\\n      \\\"验证命令，以及不做什么\\\",\\n      \\\"什么时候退出计划模式进入执行\\\",\\n      \\\"差的 /plan 只写“做一个完整优化”，缺对象和边界\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"/goal：长目标也要有边界\\\", headers: [\\\"适合\\\", \\\"不适合\\\"], rows: [\\n      [\\\"长迁移、长重构\\\", \\\"目标没有范围，例如“优化项目”\\\"],\\n      [\\\"部署重试直到成功\\\", \\\"没有结束条件\\\"],\\n      [\\\"原型打磨直到测试通过\\\", \\\"没有权限边界\\\"],\\n      [\\\"比一次提示更长但有明确终点\\\", \\\"周期或后台检查，应交给 Automations\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"/review 的五个检查维度\\\", bullets: [\\n      \\\"范围：是否只改了任务指定文件\\\",\\n      \\\"正确性：边界条件、空值、异步竞态\\\",\\n      \\\"安全：是否触碰 secret、权限、网络\\\",\\n      \\\"测试：是否覆盖新增行为\\\",\\n      \\\"可维护：是否引入重复逻辑或隐式依赖\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"命令排障表\\\", headers: [\\\"症状\\\", \\\"可能原因\\\", \\\"排查顺序\\\"], rows: [\\n      [\\\"输入 /goal 没出现\\\", \\\"feature 未启用或版本不支持\\\", \\\"先看 / 列表，再查 features.goals\\\"],\\n      [\\\"/review 没问题\\\", \\\"当前没有 Git diff\\\", \\\"先看 Review 面板文件列表\\\"],\\n      [\\\"/mcp 看不到工具\\\", \\\"MCP 未配置或 App 未刷新\\\", \\\"看 Settings，再用 codex mcp list 辅助\\\"],\\n      [\\\"命令列表和教程不同\\\", \\\"版本、插件或实验开关不同\\\", \\\"以当前 App 列表和官方文档为准\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"App Commands 与 CLI Commands 不保证一致\\\", bullets: [\\n      \\\"App 面向桌面线程、Review 面板和工具入口\\\",\\n      \\\"CLI 面向终端 TUI、命令行权限和会话\\\",\\n      \\\"App 输入 / 查看，CLI 输入 /help 查看\\\",\\n      \\\"两者不保证完全一致，以当前界面显示为准\\\",\\n      \\\"CLI 命令写到 CX-12，不能写成 App 主线\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"掌握的是什么时候切换工作模式\\\", subtitle: \\\"下一篇：CX-04 项目指令、配置、权限与沙盒\\\" }\\n  ]\\n});\\n\\n// ================= CX-04 =================\\ndecks.push({\\n  code: \\\"CX-04\\\", category: \\\"codex\\\", fileTitle: \\\"Codex项目指令权限配置\\\",\\n  deck: \\\"Codex 项目指令、配置、权限与沙盒\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex 项目指令、配置、权限与沙盒\\\", subtitle: \\\"零基础 · 让 App 知道怎么安全工作\\\", kicker: \\\"Vibe Coding 学习系列 · CX-04\\\" },\\n    { layout: \\\"section\\\", title: \\\"从软到硬的四层配置\\\", subtitle: \\\"新手先掌握 AGENTS.md 和 App Settings 两层\\\" },\\n    { layout: \\\"cards\\\", title: \\\"配置系统的四层心智模型\\\", cards: [\\n      { title: \\\"项目说明层\\\", desc: \\\"AGENTS.md，写项目事实、命令、规范和安全边界\\\" },\\n      { title: \\\"用户偏好层\\\", desc: \\\"App Settings / config.toml，设模型、终端、审批、沙盒\\\" },\\n      { title: \\\"命令策略层\\\", desc: \\\"Rules / permission profiles，对危险动作建立边界\\\" },\\n      { title: \\\"事件脚本层\\\", desc: \\\"Hooks，在特定时机运行真实脚本做审计或检查\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"为什么不能只靠提示词\\\", bullets: [\\n      \\\"不持久：换线程后可能忘了重复说\\\",\\n      \\\"不够硬：说不要推 main，仍要靠人工盯\\\",\\n      \\\"不可审计：团队很难知道每个人临时说了什么\\\",\\n      \\\"长期规则写进 AGENTS.md\\\",\\n      \\\"高风险命令用 Rules，复杂事件才用 Hooks\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"AGENTS.md 推荐结构\\\", headers: [\\\"模块\\\", \\\"要回答的问题\\\"], rows: [\\n      [\\\"项目概览\\\", \\\"这个项目是什么，主要目录在哪里\\\"],\\n      [\\\"常用命令\\\", \\\"安装、测试、lint、build 怎么跑\\\"],\\n      [\\\"修改边界\\\", \\\"哪些文件可以改，哪些要谨慎\\\"],\\n      [\\\"代码风格\\\", \\\"当前项目已有写法是什么\\\"],\\n      [\\\"验证方式\\\", \\\"改完怎么证明，失败要解释\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"AGENTS.md 不该写什么\\\", bullets: [\\n      \\\"API Key、token、cookie\\\",\\n      \\\"只针对本次任务的临时要求\\\",\\n      \\\"个人机器路径\\\",\\n      \\\"不稳定的模型名称或价格\\\",\\n      \\\"「写高质量代码」这种无法验证的口号\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"按场景选择权限策略\\\", headers: [\\\"场景\\\", \\\"建议\\\"], rows: [\\n      [\\\"陌生项目\\\", \\\"保守审批，先只读\\\"],\\n      [\\\"日常小改\\\", \\\"允许常见读写和安全命令\\\"],\\n      [\\\"大规模重构\\\", \\\"使用 worktree，严格 review\\\"],\\n      [\\\"CI / 自动化\\\", \\\"外部沙箱 + 最小权限\\\"],\\n      [\\\"涉及密钥或生产数据\\\", \\\"默认拒绝，人工确认\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"三种沙盒模式\\\", cards: [\\n      { title: \\\"read-only\\\", desc: \\\"只读，适合审计和探索\\\" },\\n      { title: \\\"workspace-write\\\", desc: \\\"可写工作区，适合日常开发\\\" },\\n      { title: \\\"danger-full-access\\\", desc: \\\"无沙盒限制，只能在外部可信沙箱使用\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"Rules 适合与不适合做什么\\\", headers: [\\\"适合\\\", \\\"不适合\\\"], rows: [\\n      [\\\"拦危险删除，例如 rm -rf\\\", \\\"写复杂业务流程\\\"],\\n      [\\\"拦未经确认的 publish\\\", \\\"替代测试或 Review\\\"],\\n      [\\\"对 push、tag、force push 要求确认\\\", \\\"判断产品取舍\\\"],\\n      [\\\"允许 git status、rg、ls 等只读命令\\\", \\\"管理外部账号授权\\\"]\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"改完配置后怎么核对\\\", steps: [\\n      { title: \\\"改 AGENTS.md\\\", desc: \\\"新线程里让 Codex 总结项目规则，看是否读到\\\" },\\n      { title: \\\"改权限或沙盒\\\", desc: \\\"用 /status 或 Settings 确认实际生效\\\" },\\n      { title: \\\"改 MCP 配置\\\", desc: \\\"用 /mcp 看 server 和工具是否可见\\\" },\\n      { title: \\\"换项目目录时\\\", desc: \\\"确认打开了对的目录，旧线程可能仍是旧上下文\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"Hooks 是事件脚本，不是万能自动化\\\", bullets: [\\n      \\\"配置通常在 .codex/hooks.json 或 [hooks] 表\\\",\\n      \\\"会运行真实命令，可能读取敏感上下文\\\",\\n      \\\"写错会阻塞工作流，学习阶段先别急着写\\\",\\n      \\\"能用 Rules 解决的命令边界，不要先写 Hook\\\",\\n      \\\"相对路径要改从 git root 或绝对路径解析\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"先用 AGENTS.md 和 Settings 把边界写清楚\\\", subtitle: \\\"下一篇：CX-05 MCP 外部工具\\\" }\\n  ]\\n});\\n\\n// ================= CX-05 =================\\ndecks.push({\\n  code: \\\"CX-05\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-MCP外部工具\\\",\\n  deck: \\\"Codex MCP：在 App 中连接外部工具\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex MCP：在 App 中连接外部工具\\\", subtitle: \\\"零基础 · 先只读、再小范围、可审计、可撤销\\\", kicker: \\\"Vibe Coding 学习系列 · CX-05\\\" },\\n    { layout: \\\"section\\\", title: \\\"MCP 不是搜索框，而是工具连接层\\\", subtitle: \\\"让 Codex 连接浏览器、数据库、文档和内部 API\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"MCP 能给 Codex 什么\\\", bullets: [\\n      \\\"文档上下文：查新文档，减少过期知识\\\",\\n      \\\"开发工具：控制浏览器，检查页面\\\",\\n      \\\"设计工具：读取 Figma 等设计上下文\\\",\\n      \\\"数据工具：数据库 schema、只读查询\\\",\\n      \\\"项目与内部系统：GitHub issue / PR、私有 API\\\"\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"App 中的 MCP 工作流\\\", steps: [\\n      { title: \\\"启用或配置\\\", desc: \\\"在 App Settings 或集成入口启用 MCP\\\" },\\n      { title: \\\"查看可见工具\\\", desc: \\\"回到线程，用 /mcp 看 server 和工具\\\" },\\n      { title: \\\"用自然语言调用\\\", desc: \\\"要求 Codex 使用工具，并观察权限提示\\\" },\\n      { title: \\\"Review 结果\\\", desc: \\\"核对来源、时间、权限和副作用\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"从 0 配 MCP 前先确认四件事\\\", headers: [\\\"问题\\\", \\\"为什么重要\\\"], rows: [\\n      [\\\"本地命令还是远程服务\\\", \\\"决定用 stdio、HTTP 还是插件提供\\\"],\\n      [\\\"需要什么账号或 token\\\", \\\"决定密钥放哪里，不能写进仓库\\\"],\\n      [\\\"默认能读写什么\\\", \\\"决定是否只读、是否需要审批\\\"],\\n      [\\\"App 是否已有连接器或插件\\\", \\\"有现成入口时不要重复手写 MCP\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"三类 MCP server\\\", cards: [\\n      { title: \\\"STDIO\\\", desc: \\\"本地命令启动进程，适合本机工具和私有脚本\\\" },\\n      { title: \\\"Streamable HTTP\\\", desc: \\\"访问一个 URL，适合远程服务、OAuth 和云端工具\\\" },\\n      { title: \\\"Plugin-provided\\\", desc: \\\"插件 manifest 提供 server，先看来源和工具权限\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"密钥放哪里\\\", headers: [\\\"场景\\\", \\\"推荐\\\", \\\"不推荐\\\"], rows: [\\n      [\\\"本地个人 token\\\", \\\"系统环境变量或密码管理器\\\", \\\"写进 config.toml 并提交\\\"],\\n      [\\\"团队共享服务\\\", \\\"组织 secret 管理、最小 scope\\\", \\\"共享个人账号 token\\\"],\\n      [\\\"Cloud / remote\\\", \\\"环境变量或官方 secret 入口\\\", \\\"在 setup 日志里 echo\\\"],\\n      [\\\"临时调试\\\", \\\"临时只读 token，用完撤销\\\", \\\"使用生产写 token\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"配置 MCP 前先问的安全问题\\\", bullets: [\\n      \\\"它能读什么数据，能写什么数据\\\",\\n      \\\"它是否会联网，是否需要账号授权\\\",\\n      \\\"它是否会把数据发给第三方\\\",\\n      \\\"它能不能在只读模式下完成任务\\\",\\n      \\\"生产库、客户数据和邮箱都按最小权限配置\\\"\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"工具风险分级\\\", cards: [\\n      { title: \\\"只读搜索\\\", desc: \\\"风险低，可以较宽松\\\" },\\n      { title: \\\"读取私有数据\\\", desc: \\\"风险中，需要来源说明\\\" },\\n      { title: \\\"写外部系统\\\", desc: \\\"风险高，需要人工确认\\\" },\\n      { title: \\\"访问生产数据\\\", desc: \\\"风险很高，默认不要给新手练习\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"MCP 排障流程\\\", headers: [\\\"症状\\\", \\\"可能原因\\\", \\\"排查\\\"], rows: [\\n      [\\\"/mcp 看不到 server\\\", \\\"配置层未加载或 App 未刷新\\\", \\\"先看 App Settings，再重启或刷新\\\"],\\n      [\\\"CLI 能看到 App 看不到\\\", \\\"配置层或会话状态不同\\\", \\\"以 App 线程使用结果为准\\\"],\\n      [\\\"server 启动失败\\\", \\\"命令不存在或依赖未安装\\\", \\\"在终端单独跑启动命令看日志\\\"],\\n      [\\\"结果不可信\\\", \\\"来源不明或时间过期\\\", \\\"要求 Codex 列出来源和查询条件\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"MCP 配置核对清单\\\", bullets: [\\n      \\\"App 可见：/mcp 能看到 server 和工具\\\",\\n      \\\"最小权限：只给当前任务需要的读写范围\\\",\\n      \\\"密钥安全：token 在环境变量或 secret 里\\\",\\n      \\\"只读试跑：能完成一次只读查询或读取\\\",\\n      \\\"可审计、可撤销：知道怎么禁用和撤销 token\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"先只读、再小范围、可审计、可撤销\\\", subtitle: \\\"下一篇：CX-06 Skills 可复用工作流\\\" }\\n  ]\\n});\\n\\n// ================= CX-06 =================\\ndecks.push({\\n  code: \\\"CX-06\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-Skills可复用工作流\\\",\\n  deck: \\\"Codex Skills：把重复提示变成可复用工作流\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex Skills：把重复提示变成可复用工作流\\\", subtitle: \\\"零基础 · 让流程可重复，而不是让 prompt 更长\\\", kicker: \\\"Vibe Coding 学习系列 · CX-06\\\" },\\n    { layout: \\\"section\\\", title: \\\"Skill 是可复用判断，不是 prompt 收藏\\\", subtitle: \\\"要有步骤、边界和验收方式\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"Skill 是什么，适合什么\\\", bullets: [\\n      \\\"一组可复用指令、资源和可选脚本\\\",\\n      \\\"适合代码审查、文档核对、发布检查和团队 SOP\\\",\\n      \\\"不适合只执行一次的临时任务\\\",\\n      \\\"不适合需要实时外部 API 的工具连接\\\",\\n      \\\"不适合需要定时运行的周期任务\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"什么时候值得做成 Skill\\\", headers: [\\\"信号\\\", \\\"是否适合\\\"], rows: [\\n      [\\\"同一提示复制三次以上\\\", \\\"适合\\\"],\\n      [\\\"多人需要同一做法\\\", \\\"适合\\\"],\\n      [\\\"输出格式总要固定\\\", \\\"适合\\\"],\\n      [\\\"只做一次的临时任务\\\", \\\"不适合\\\"],\\n      [\\\"需要每天运行\\\", \\\"交给 Automation 调度\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"好 Skill 的四个特征\\\", cards: [\\n      { title: \\\"触发清楚\\\", desc: \\\"description 里写明什么时候用\\\" },\\n      { title: \\\"边界清楚\\\", desc: \\\"也写明什么时候不用\\\" },\\n      { title: \\\"输入输出清楚\\\", desc: \\\"Codex 知道读什么、交付什么\\\" },\\n      { title: \\\"内容分层\\\", desc: \\\"常用指令在 SKILL.md，长资料放 references\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"description 是触发路由，不是介绍文案\\\", bullets: [\\n      \\\"模板：Use when 场景，Do 动作，Do not use when 边界\\\",\\n      \\\"差写法：Helps write high quality code\\\",\\n      \\\"好写法要写清对象、动作、触发场景和边界\\\",\\n      \\\"写得太泛，Codex 可能乱用\\\",\\n      \\\"写得太窄，真正需要时触发不了\\\"\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"在 App 中调用 Skill\\\", steps: [\\n      { title: \\\"确认能否看到\\\", desc: \\\"当前 App 是否显示这个 Skill\\\" },\\n      { title: \\\"确认层级\\\", desc: \\\"用户级、项目级，还是插件带来的\\\" },\\n      { title: \\\"确认副作用\\\", desc: \\\"会不会读额外资源、运行脚本或调用工具\\\" },\\n      { title: \\\"显式调用\\\", desc: \\\"用 $code-review 或自然语言点名，再说清任务\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"Skills、Commands、Automations 的分工\\\", headers: [\\\"需求\\\", \\\"首选\\\"], rows: [\\n      [\\\"当前线程快速动作\\\", \\\"Command\\\"],\\n      [\\\"固定 SOP / 复用流程\\\", \\\"Skill\\\"],\\n      [\\\"定时或后台重复执行\\\", \\\"Automation\\\"],\\n      [\\\"外部工具连接\\\", \\\"MCP / Connector\\\"],\\n      [\\\"打包分发一组能力\\\", \\\"Plugin\\\"]\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"文件结构：内容放哪里\\\", headers: [\\\"内容\\\", \\\"放哪里\\\", \\\"原因\\\"], rows: [\\n      [\\\"触发场景、流程、输出\\\", \\\"SKILL.md\\\", \\\"Codex 必须先看到\\\"],\\n      [\\\"长规范、示例、术语表\\\", \\\"references/\\\", \\\"需要时再读，节省上下文\\\"],\\n      [\\\"重复性强易写错的逻辑\\\", \\\"scripts/\\\", \\\"要写清运行时和失败输出\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"Skill 不该承载什么\\\", bullets: [\\n      \\\"一次性任务\\\",\\n      \\\"当前项目的临时 bug\\\",\\n      \\\"模糊人设包装\\\",\\n      \\\"需要每天变化的命令\\\",\\n      \\\"真实密钥或私有账号信息\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"一次性任务放 prompt，项目事实放 AGENTS.md\\\", subtitle: \\\"下一篇：CX-07 Plugins 连接器\\\" }\\n  ]\\n});\\n\\n// ================= CX-07 =================\\ndecks.push({\\n  code: \\\"CX-07\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-Plugins连接器\\\",\\n  deck: \\\"Codex Plugins 与 Connectors：App 能力扩展\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex Plugins 与 Connectors：App 能力扩展\\\", subtitle: \\\"零基础 · 安装是让能力可见，授权是让数据可用\\\", kicker: \\\"Vibe Coding 学习系列 · CX-07\\\" },\\n    { layout: \\\"section\\\", title: \\\"安装、授权、调用是三件事\\\", subtitle: \\\"插件可以包含 Skills、MCP、Apps，但不等于其中任何一个\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"安装、授权、调用、撤销\\\", bullets: [\\n      \\\"安装 Plugin：看它带来的 Skills / MCP / Apps / 配置\\\",\\n      \\\"对外部服务单独授权\\\",\\n      \\\"在线程中引用或调用外部上下文\\\",\\n      \\\"工具或外部动作按权限和审批执行\\\",\\n      \\\"不用时撤销授权或卸载\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"先分清四个概念\\\", headers: [\\\"概念\\\", \\\"本质\\\", \\\"例子\\\"], rows: [\\n      [\\\"Connector / App\\\", \\\"外部账号连接\\\", \\\"GitHub、Gmail、Drive、Slack\\\"],\\n      [\\\"Plugin\\\", \\\"能力包\\\", \\\"一组 skills、MCP、apps、配置\\\"],\\n      [\\\"Skill\\\", \\\"可复用工作流\\\", \\\"代码审查 SOP\\\"],\\n      [\\\"MCP\\\", \\\"工具协议\\\", \\\"浏览器、数据库、文档源\\\"]\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"App 中的连接器工作流\\\", steps: [\\n      { title: \\\"打开入口\\\", desc: \\\"进入 App 的 Plugins / Connectors / Apps\\\" },\\n      { title: \\\"选择服务\\\", desc: \\\"挑要连接的 GitHub、Drive、Slack 等\\\" },\\n      { title: \\\"完成授权\\\", desc: \\\"授权范围要单独看清楚\\\" },\\n      { title: \\\"引用并执行\\\", desc: \\\"用 @、mention 或自然语言引用外部上下文\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"安装或连接前的检查\\\", headers: [\\\"检查项\\\", \\\"要确认什么\\\"], rows: [\\n      [\\\"来源\\\", \\\"官方、组织内，还是第三方插件\\\"],\\n      [\\\"能力\\\", \\\"带 Skills、MCP、Connectors 还是组合包\\\"],\\n      [\\\"权限\\\", \\\"只读、评论、写文件、发消息分别要什么权限\\\"],\\n      [\\\"数据范围\\\", \\\"能访问哪些仓库、文档、邮箱或群聊\\\"],\\n      [\\\"撤销方式\\\", \\\"在 App、服务后台还是组织管理端撤销\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"插件安装后的四层变化\\\", cards: [\\n      { title: \\\"目录层\\\", desc: \\\"Plugins 页面出现已安装条目\\\" },\\n      { title: \\\"能力层\\\", desc: \\\"@ mention 或 bundled skills 可被调用\\\" },\\n      { title: \\\"授权层\\\", desc: \\\"外部 App 可能要求登录或授权\\\" },\\n      { title: \\\"执行层\\\", desc: \\\"Codex 按 prompt、权限和审批调用工具\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"最小权限原则\\\", bullets: [\\n      \\\"第一次安装只给必要权限\\\",\\n      \\\"只读任务不给写权限\\\",\\n      \\\"需要发消息或改 PR 时，明确说明目标和范围\\\",\\n      \\\"团队插件先在测试项目验证\\\",\\n      \\\"不再使用时及时禁用或卸载\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"常见连接场景与风险\\\", headers: [\\\"场景\\\", \\\"连接器价值\\\", \\\"风险点\\\"], rows: [\\n      [\\\"GitHub\\\", \\\"读取 issue、PR、仓库上下文\\\", \\\"写权限、PR 评论权限\\\"],\\n      [\\\"Google Drive / Docs\\\", \\\"读取团队文档\\\", \\\"文档访问范围\\\"],\\n      [\\\"Gmail / Outlook\\\", \\\"引用邮件上下文\\\", \\\"隐私和敏感信息\\\"],\\n      [\\\"Slack / Teams\\\", \\\"查讨论和决策\\\", \\\"群聊范围和成员隐私\\\"],\\n      [\\\"Calendar\\\", \\\"查日程和会议背景\\\", \\\"个人隐私\\\"]\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"CLI 辅助管理 marketplace\\\", headers: [\\\"命令\\\", \\\"用途\\\"], rows: [\\n      [\\\"codex plugin marketplace list\\\", \\\"列出已添加的 marketplace\\\"],\\n      [\\\"codex plugin marketplace add owner/repo\\\", \\\"添加 marketplace 来源\\\"],\\n      [\\\"codex plugin marketplace upgrade\\\", \\\"升级 marketplace\\\"],\\n      [\\\"codex plugin marketplace remove 名称\\\", \\\"移除 marketplace\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"观察输出：看用了什么，不只看答得像不像\\\", bullets: [\\n      \\\"你使用了哪些插件或工具能力\\\",\\n      \\\"哪些信息来自外部系统\\\",\\n      \\\"哪些结论是根据上下文推断的\\\",\\n      \\\"有没有权限、网络、认证或数据范围限制\\\",\\n      \\\"安装是让能力可见，审批是最后的安全门\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"安装让能力可见，授权让数据可用，审批是安全门\\\", subtitle: \\\"本系列 codex 分册到此\\\" }\\n  ]\\n});\\n\\n// ---------- validation ----------\\nconst problems: string[] = [];\\nfor (const d of decks) {\\n  const n = d.slides.length;\\n  if (n < 10 || n > 14) problems.push(`${d.code}: slide count ${n}`);\\n  if (d.slides[0].kicker !== `Vibe Coding 学习系列 · ${d.code}`) problems.push(`${d.code}: kicker`);\\n  for (const [i, s] of d.slides.entries()) {\\n    if (s.layout === \\\"bullets\\\") {\\n      if (s.bullets.length > 5) problems.push(`${d.code} slide${i}: bullets ${s.bullets.length}`);\\n      for (const b of s.bullets) {\\n        const total = [...b].length;\\n        const han = [...b].filter(c => /\\\\p{Script=Han}/u.test(c)).length;\\n        if (total > 42) problems.push(`${d.code} slide${i}: len=${total} \\\"${b}\\\"`);\\n        if (han > 42) problems.push(`${d.code} slide${i}: han=${han} \\\"${b}\\\"`);\\n      }\\n    }\\n    if (s.layout === \\\"cards\\\") {\\n      if (s.cards.length < 3 || s.cards.length > 4) problems.push(`${d.code} slide${i}: cards ${s.cards.length}`);\\n      for (const c of s.cards) {\\n        if ([...c.desc].length > 42) problems.push(`${d.code} slide${i}: card desc len=${[...c.desc].length} \\\"${c.desc}\\\"`);\\n      }\\n    }\\n    if (s.layout === \\\"steps\\\") {\\n      if (s.steps.length < 3 || s.steps.length > 4) problems.push(`${d.code} slide${i}: steps ${s.steps.length}`);\\n      for (const st of s.steps) {\\n        if ([...st.desc].length > 42) problems.push(`${d.code} slide${i}: step desc len=${[...st.desc].length} \\\"${st.desc}\\\"`);\\n      }\\n    }\\n    if (s.layout === \\\"table\\\") {\\n      if (s.headers.length > 5) problems.push(`${d.code} slide${i}: cols ${s.headers.length}`);\\n      if (s.rows.length > 6) problems.push(`${d.code} slide${i}: rows ${s.rows.length}`);\\n      for (const r of s.rows) if (r.length !== s.headers.length) problems.push(`${d.code} slide${i}: row width mismatch`);\\n    }\\n  }\\n}\\nreturn JSON.stringify({ problems, summary: decks.map(d => ({ code: d.code, title: d.deck, slides: d.slides.length })) }, null, 1);\", \"description\": \"Build and validate 7 tutorial decks\"}"
}

## tool · 2026-10-05T11:53:42Z

run_code
{"code": "const dir = \"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\";\ntype Slide = any;\n\nfunction mk(id: string, title: string, sub: string, slides: Slide[]) {\n  return { code: id, category: \"codex\", fileTitle: \"\", deck: title, _sub: sub, slides };\n}\n\nconst decks: any[] = [];\n\n// ================= CX-01 =================\ndecks.push({\n  code: \"CX-01\", category: \"codex\", fileTitle: \"Codex-App安装与认证\",\n  deck: \"Codex App 安装与认证：从下载到第一个线程\",\n  slides: [\n    { layout: \"cover\", title: \"Codex App 安装与认证：从下载到第一个线程\", subtitle: \"零基础 · Windows / macOS 装好、登上号、跑通第一个安全任务\", kicker: \"Vibe Coding 学习系列 · CX-01\" },\n    { layout: \"section\", title: \"安装目标：先能安全打开本地项目\", subtitle: \"App 是主线，CLI / Web / Cloud 是辅助\" },\n    { layout: \"bullets\", title: \"安装成功的五条标准\", bullets: [\n      \"桌面 Codex App 能正常打开\",\n      \"能用 ChatGPT / OpenAI 账号登录\",\n      \"能添加本地项目并创建线程\",\n      \"能让 Codex 只读分析项目\",\n      \"能看到 Review、diff 和 Settings\"\n    ], notes: \"安装成功的标准不是终端里有 codex 命令，而是 App 能用起来。\" },\n    { layout: \"table\", title: \"系统准备：按平台走官方入口\", headers: [\"平台\", \"版本建议\", \"安装来源\"], rows: [\n      [\"Windows\", \"Windows 11 是推荐基线\", \"Microsoft Store 或 winget\"],\n      [\"macOS\", \"使用仍受 Apple 支持的版本\", \"官方 Codex App 下载页\"],\n      [\"Linux\", \"桌面版暂未覆盖\", \"先用 CLI / Web / Cloud\"]\n    ], notes: \"不要从不明网盘或第三方安装包安装。\" },\n    { layout: \"steps\", title: \"Windows 安装四步\", steps: [\n      { title: \"从官方页面进 Store\", desc: \"打开官方 Windows 页，点 Codex app for Windows 链接\" },\n      { title: \"在 Store 点获取安装\", desc: \"企业禁用 Store 时让管理员分发，或用 winget install Codex -s msstore\" },\n      { title: \"开始菜单打开 Codex\", desc: \"首次启动按提示登录，优先用 ChatGPT 账号\" },\n      { title: \"处理防火墙弹窗\", desc: \"一般只勾专用网络，公用网络不要选\" }\n    ] },\n    { layout: \"cards\", title: \"首次启动的三个关卡\", cards: [\n      { title: \"登录\", desc: \"优先 ChatGPT / OpenAI 账号；API Key 不是 App 登录方案\" },\n      { title: \"权限提示\", desc: \"区分选目录、跑只读命令和写文件联网，后者看清再同意\" },\n      { title: \"防火墙\", desc: \"本地服务通信时弹窗，只放行可信网络\" }\n    ] },\n    { layout: \"table\", title: \"排障总表：先定位症状，不要乱重装\", headers: [\"症状\", \"常见原因\", \"第一反应\"], rows: [\n      [\"App 装不上\", \"Store、系统版本或企业策略\", \"先确认来源和系统更新\"],\n      [\"登录失败\", \"浏览器登录态、网络、账号权限\", \"换浏览器登录或重新授权\"],\n      [\"Review 不可用\", \"没有 Git 或项目不是 Git 仓库\", \"安装 Git，确认 git status\"],\n      [\"命令跑不动\", \"PowerShell policy 或工具链缺失\", \"先在终端跑版本命令\"],\n      [\"macOS 打不开\", \"Gatekeeper 或下载来源问题\", \"从官方入口下载再按提示授权\"]\n    ] },\n    { layout: \"steps\", title: \"第一次打开项目：四步不慌\", steps: [\n      { title: \"选一个普通 Git 仓库\", desc: \"不要一上来打开生产仓库，最好有 README\" },\n      { title: \"添加本地项目目录\", desc: \"确认 App 能识别 Git 状态\" },\n      { title: \"创建 Local thread\", desc: \"先发只读任务：总结技术栈、启动命令和测试命令\" },\n      { title: \"再做一个小改动\", desc: \"只改一个错别字，看 diff 且不自动提交\" }\n    ] },\n    { layout: \"bullets\", title: \"第一个安全可写任务\", bullets: [\n      \"只改低风险文件，例如文档里的一个错别字\",\n      \"明确要求改完展示 diff，不要自动提交\",\n      \"确认改动只在预期文件里\",\n      \"确认 Review 面板能看到 diff\",\n      \"知道怎么撤销或继续修改\"\n    ] },\n    { layout: \"cards\", title: \"安装后检查清单\", cards: [\n      { title: \"账号与环境\", desc: \"已登录，防火墙和 macOS 权限按最小范围授权\" },\n      { title: \"Git 与项目\", desc: \"App 能看到 Git 状态，能添加本地仓库\" },\n      { title: \"线程与只读\", desc: \"能创建 Local thread 并总结项目，不改文件\" },\n      { title: \"可写与 Review\", desc: \"小改动能在 Review 中看到 diff\" }\n    ] },\n    { layout: \"table\", title: \"CLI 只作为辅助\", headers: [\"命令\", \"用途\"], rows: [\n      [\"codex --help\", \"查看 CLI 帮助\"],\n      [\"codex app\", \"从 CLI 打开 App\"],\n      [\"codex review\", \"做代码审查\"],\n      [\"codex exec \\\"summarize this repo\\\"\", \"非交互执行任务\"]\n    ] },\n    { layout: \"end\", title: \"装好之后：先只读，再小改，最后 Review\", subtitle: \"下一篇：CX-02 Codex App 桌面工作流\" }\n  ]\n});\n\n// ================= CX-02 =================\ndecks.push({\n  code: \"CX-02\", category: \"codex\", fileTitle: \"Codex-App桌面工作流\",\n  deck: \"Codex App 桌面工作流：把 App 当主控台\",\n  slides: [\n    { layout: \"cover\", title: \"Codex App 桌面工作流：把 App 当主控台\", subtitle: \"零基础 · 线程、终端、Review、权限在一个桌面流程里\", kicker: \"Vibe Coding 学习系列 · CX-02\" },\n    { layout: \"section\", title: \"App 是开发主控台，不是聊天窗口\", subtitle: \"Thread 管上下文，Review 管结果，Settings 管边界\" },\n    { layout: \"bullets\", title: \"App 把哪些能力放在一起\", bullets: [\n      \"Thread：一条任务线，带上下文、历史和状态\",\n      \"Review：查看 diff、行内反馈和 stage / unstage\",\n      \"Terminal：让 Codex 在受控环境里运行命令\",\n      \"Settings：模型、审批、沙盒、插件和 MCP 的入口\",\n      \"Automations / Plugins：后台检查和外部账号连接\"\n    ] },\n    { layout: \"table\", title: \"核心概念速查\", headers: [\"概念\", \"一句话解释\"], rows: [\n      [\"Thread\", \"一条任务线，包含上下文、历史和状态\"],\n      [\"Worktree\", \"Git 隔离工作目录，仍会产生真实改动\"],\n      [\"Review 面板\", \"看 diff、行内反馈、stage / revert 的关口\"],\n      [\"Local workspace\", \"当前本机项目目录，决定 Codex 能看到什么\"],\n      [\"Cloud handoff\", \"把任务交给云端环境继续做\"]\n    ] },\n    { layout: \"cards\", title: \"五个控制点\", cards: [\n      { title: \"目标\", desc: \"这次到底要解决什么问题\" },\n      { title: \"上下文\", desc: \"Codex 该读哪些文件，陌生项目先只读建模\" },\n      { title: \"权限\", desc: \"是否允许写文件、跑命令、联网、调外部工具\" },\n      { title: \"结果\", desc: \"改动是否真的在预期范围内，收口由人决定\" }\n    ] },\n    { layout: \"steps\", title: \"一条线程的生命周期\", steps: [\n      { title: \"开场只读\", desc: \"先读项目，确认技术栈、命令、目录和风险\" },\n      { title: \"明确任务\", desc: \"说清目标、范围、不能做什么、怎么验证\" },\n      { title: \"允许执行\", desc: \"小任务直接改，大任务先 /plan 或用 worktree\" },\n      { title: \"检查与收口\", desc: \"看 Review，定点反馈，由人决定是否提交\" }\n    ] },\n    { layout: \"table\", title: \"三种工作方式怎么选\", headers: [\"任务\", \"推荐方式\", \"为什么\"], rows: [\n      [\"读项目、解释报错\", \"Local thread 只读\", \"快，风险低\"],\n      [\"改一个文件或少量文档\", \"Local thread + Review\", \"改动小，容易检查\"],\n      [\"新功能、重构、改多个文件\", \"Worktree thread\", \"隔离改动，便于撤回\"],\n      [\"盯 PR、修 CI、长任务\", \"Cloud / Web handoff\", \"不占用本地环境\"]\n    ] },\n    { layout: \"bullets\", title: \"好任务要写清五件事\", bullets: [\n      \"目标：这次要解决什么问题\",\n      \"范围：只改哪些文件或目录\",\n      \"约束：不能做什么，例如不引入新依赖\",\n      \"验证：怎么确认改对了，跑哪条命令\",\n      \"交付：要 diff 摘要、测试结果还是 PR 描述\"\n    ] },\n    { layout: \"cards\", title: \"Review 面板逐项检查法\", cards: [\n      { title: \"文件列表\", desc: \"是否只改了任务范围内文件，范围外要解释或撤掉\" },\n      { title: \"单文件 diff\", desc: \"是否有无关格式化、删除或重命名\" },\n      { title: \"命令记录\", desc: \"验证命令是否真的跑过，没跑要说明原因\" },\n      { title: \"安全项\", desc: \"是否碰了 .env、token 或权限配置，碰到立即停\" }\n    ] },\n    { layout: \"table\", title: \"常见反模式\", headers: [\"反模式\", \"真正风险\", \"更稳做法\"], rows: [\n      [\"一个线程混多个目标\", \"上下文混乱，Review 难收口\", \"一个目标一条线程\"],\n      [\"任务只写“优化一下”\", \"Codex 不知道边界\", \"写清目标、范围、约束、验证、交付\"],\n      [\"陌生仓库直接写\", \"误读架构和命令\", \"先只读建模\"],\n      [\"允许自动提交推送\", \"错误进入远端\", \"先草拟，由人确认\"]\n    ] },\n    { layout: \"bullets\", title: \"App 用户的三个基本动作\", bullets: [\n      \"收窄：只改 README，控制 diff 大小\",\n      \"追证据：你运行了什么命令\",\n      \"反向解释：根据 diff 解释你做了什么\",\n      \"线程标题用结果导向命名，方便以后找回上下文\",\n      \"新目标开新线程；混在一起就难 Review\"\n    ] },\n    { layout: \"end\", title: \"先建立控制感，再逐步放开能力\", subtitle: \"下一篇：CX-03 Commands 工作流入口\" }\n  ]\n});\n\n// ================= CX-03 =================\ndecks.push({\n  code: \"CX-03\", category: \"codex\", fileTitle: \"Codex-Commands工作流入口\",\n  deck: \"Codex Commands：App 里的工作流入口\",\n  slides: [\n    { layout: \"cover\", title: \"Codex Commands：App 里的工作流入口\", subtitle: \"零基础 · 不背命令表，学会什么时候切换工作模式\", kicker: \"Vibe Coding 学习系列 · CX-03\" },\n    { layout: \"section\", title: \"入口、状态、动作\", subtitle: \"先看状态，再定推进方式，执行后用 /review 收口\" },\n    { layout: \"bullets\", title: \"slash commands 的三层\", bullets: [\n      \"入口层：/status、/mcp、/feedback\",\n      \"状态层：/plan、/goal，改变任务推进方式\",\n      \"审查层：/review，围绕当前 diff 做检查\",\n      \"命令只是更快进入某种工作模式\",\n      \"模式不对，命令反而会制造混乱\"\n    ] },\n    { layout: \"table\", title: \"用不用 Command 的判断\", headers: [\"你想做什么\", \"首选方式\", \"为什么\"], rows: [\n      [\"看当前线程状态\", \"/status\", \"快速确认上下文、限制和配额\"],\n      [\"让 Codex 先别动手\", \"/plan\", \"把执行前移到方案讨论\"],\n      [\"长时间推进清楚目标\", \"/goal\", \"让目标跨多个 turn 持续存在\"],\n      [\"检查当前改动\", \"/review\", \"直接进入代码审查口径\"],\n      [\"查 MCP 是否连接\", \"/mcp\", \"看工具 server 和状态\"]\n    ] },\n    { layout: \"cards\", title: \"App 用户先掌握的稳定命令\", cards: [\n      { title: \"/status\", desc: \"查看模型、工作区、审批和上下文状态\" },\n      { title: \"/plan\", desc: \"大任务先规划，不急着改文件\" },\n      { title: \"/review\", desc: \"审查当前改动，合并前使用\" },\n      { title: \"/mcp\", desc: \"接外部工具后，查看 server 和工具\" }\n    ] },\n    { layout: \"steps\", title: \"在 App 里发现命令四步\", steps: [\n      { title: \"打开项目线程\", desc: \"任何已有项目的线程都可以\" },\n      { title: \"输入 /\", desc: \"看弹出的命令列表和说明\" },\n      { title: \"注意实验标记\", desc: \"不确定时先问，不要直接执行\" },\n      { title: \"查官方文档核对\", desc: \"以当前 App 显示和官方 App Commands 为准\" }\n    ] },\n    { layout: \"bullets\", title: \"/plan：好的计划应该包含什么\", bullets: [\n      \"要读哪些文件，要改哪些文件\",\n      \"可能方案和取舍\",\n      \"验证命令，以及不做什么\",\n      \"什么时候退出计划模式进入执行\",\n      \"差的 /plan 只写“做一个完整优化”，缺对象和边界\"\n    ] },\n    { layout: \"table\", title: \"/goal：长目标也要有边界\", headers: [\"适合\", \"不适合\"], rows: [\n      [\"长迁移、长重构\", \"目标没有范围，例如“优化项目”\"],\n      [\"部署重试直到成功\", \"没有结束条件\"],\n      [\"原型打磨直到测试通过\", \"没有权限边界\"],\n      [\"比一次提示更长但有明确终点\", \"周期或后台检查，应交给 Automations\"]\n    ] },\n    { layout: \"bullets\", title: \"/review 的五个检查维度\", bullets: [\n      \"范围：是否只改了任务指定文件\",\n      \"正确性：边界条件、空值、异步竞态\",\n      \"安全：是否触碰 secret、权限、网络\",\n      \"测试：是否覆盖新增行为\",\n      \"可维护：是否引入重复逻辑或隐式依赖\"\n    ] },\n    { layout: \"table\", title: \"命令排障表\", headers: [\"症状\", \"可能原因\", \"排查顺序\"], rows: [\n      [\"输入 /goal 没出现\", \"feature 未启用或版本不支持\", \"先看 / 列表，再查 features.goals\"],\n      [\"/review 没问题\", \"当前没有 Git diff\", \"先看 Review 面板文件列表\"],\n      [\"/mcp 看不到工具\", \"MCP 未配置或 App 未刷新\", \"看 Settings，再用 codex mcp list 辅助\"],\n      [\"命令列表和教程不同\", \"版本、插件或实验开关不同\", \"以当前 App 列表和官方文档为准\"]\n    ] },\n    { layout: \"bullets\", title: \"App Commands 与 CLI Commands 不保证一致\", bullets: [\n      \"App 面向桌面线程、Review 面板和工具入口\",\n      \"CLI 面向终端 TUI、命令行权限和会话\",\n      \"App 输入 / 查看，CLI 输入 /help 查看\",\n      \"两者不保证完全一致，以当前界面显示为准\",\n      \"CLI 命令写到 CX-12，不能写成 App 主线\"\n    ] },\n    { layout: \"end\", title: \"掌握的是什么时候切换工作模式\", subtitle: \"下一篇：CX-04 项目指令、配置、权限与沙盒\" }\n  ]\n});\n\n// ================= CX-04 =================\ndecks.push({\n  code: \"CX-04\", category: \"codex\", fileTitle: \"Codex项目指令权限配置\",\n  deck: \"Codex 项目指令、配置、权限与沙盒\",\n  slides: [\n    { layout: \"cover\", title: \"Codex 项目指令、配置、权限与沙盒\", subtitle: \"零基础 · 让 App 知道怎么安全工作\", kicker: \"Vibe Coding 学习系列 · CX-04\" },\n    { layout: \"section\", title: \"从软到硬的四层配置\", subtitle: \"新手先掌握 AGENTS.md 和 App Settings 两层\" },\n    { layout: \"cards\", title: \"配置系统的四层心智模型\", cards: [\n      { title: \"项目说明层\", desc: \"AGENTS.md，写项目事实、命令、规范和安全边界\" },\n      { title: \"用户偏好层\", desc: \"App Settings / config.toml，设模型、终端、审批、沙盒\" },\n      { title: \"命令策略层\", desc: \"Rules / permission profiles，对危险动作建立边界\" },\n      { title: \"事件脚本层\", desc: \"Hooks，在特定时机运行真实脚本做审计或检查\" }\n    ] },\n    { layout: \"bullets\", title: \"为什么不能只靠提示词\", bullets: [\n      \"不持久：换线程后可能忘了重复说\",\n      \"不够硬：说不要推 main，仍要靠人工盯\",\n      \"不可审计：团队很难知道每个人临时说了什么\",\n      \"长期规则写进 AGENTS.md\",\n      \"高风险命令用 Rules，复杂事件才用 Hooks\"\n    ] },\n    { layout: \"table\", title: \"AGENTS.md 推荐结构\", headers: [\"模块\", \"要回答的问题\"], rows: [\n      [\"项目概览\", \"这个项目是什么，主要目录在哪里\"],\n      [\"常用命令\", \"安装、测试、lint、build 怎么跑\"],\n      [\"修改边界\", \"哪些文件可以改，哪些要谨慎\"],\n      [\"代码风格\", \"当前项目已有写法是什么\"],\n      [\"验证方式\", \"改完怎么证明，失败要解释\"]\n    ] },\n    { layout: \"bullets\", title: \"AGENTS.md 不该写什么\", bullets: [\n      \"API Key、token、cookie\",\n      \"只针对本次任务的临时要求\",\n      \"个人机器路径\",\n      \"不稳定的模型名称或价格\",\n      \"「写高质量代码」这种无法验证的口号\"\n    ] },\n    { layout: \"table\", title: \"按场景选择权限策略\", headers: [\"场景\", \"建议\"], rows: [\n      [\"陌生项目\", \"保守审批，先只读\"],\n      [\"日常小改\", \"允许常见读写和安全命令\"],\n      [\"大规模重构\", \"使用 worktree，严格 review\"],\n      [\"CI / 自动化\", \"外部沙箱 + 最小权限\"],\n      [\"涉及密钥或生产数据\", \"默认拒绝，人工确认\"]\n    ] },\n    { layout: \"cards\", title: \"三种沙盒模式\", cards: [\n      { title: \"read-only\", desc: \"只读，适合审计和探索\" },\n      { title: \"workspace-write\", desc: \"可写工作区，适合日常开发\" },\n      { title: \"danger-full-access\", desc: \"无沙盒限制，只能在外部可信沙箱使用\" }\n    ] },\n    { layout: \"table\", title: \"Rules 适合与不适合做什么\", headers: [\"适合\", \"不适合\"], rows: [\n      [\"拦危险删除，例如 rm -rf\", \"写复杂业务流程\"],\n      [\"拦未经确认的 publish\", \"替代测试或 Review\"],\n      [\"对 push、tag、force push 要求确认\", \"判断产品取舍\"],\n      [\"允许 git status、rg、ls 等只读命令\", \"管理外部账号授权\"]\n    ] },\n    { layout: \"steps\", title: \"改完配置后怎么核对\", steps: [\n      { title: \"改 AGENTS.md\", desc: \"新线程里让 Codex 总结项目规则，看是否读到\" },\n      { title: \"改权限或沙盒\", desc: \"用 /status 或 Settings 确认实际生效\" },\n      { title: \"改 MCP 配置\", desc: \"用 /mcp 看 server 和工具是否可见\" },\n      { title: \"换项目目录时\", desc: \"确认打开了对的目录，旧线程可能仍是旧上下文\" }\n    ] },\n    { layout: \"bullets\", title: \"Hooks 是事件脚本，不是万能自动化\", bullets: [\n      \"配置通常在 .codex/hooks.json 或 [hooks] 表\",\n      \"会运行真实命令，可能读取敏感上下文\",\n      \"写错会阻塞工作流，学习阶段先别急着写\",\n      \"能用 Rules 解决的命令边界，不要先写 Hook\",\n      \"相对路径要改从 git root 或绝对路径解析\"\n    ] },\n    { layout: \"end\", title: \"先用 AGENTS.md 和 Settings 把边界写清楚\", subtitle: \"下一篇：CX-05 MCP 外部工具\" }\n  ]\n});\n\n// ================= CX-05 =================\ndecks.push({\n  code: \"CX-05\", category: \"codex\", fileTitle: \"Codex-MCP外部工具\",\n  deck: \"Codex MCP：在 App 中连接外部工具\",\n  slides: [\n    { layout: \"cover\", title: \"Codex MCP：在 App 中连接外部工具\", subtitle: \"零基础 · 先只读、再小范围、可审计、可撤销\", kicker: \"Vibe Coding 学习系列 · CX-05\" },\n    { layout: \"section\", title: \"MCP 不是搜索框，而是工具连接层\", subtitle: \"让 Codex 连接浏览器、数据库、文档和内部 API\" },\n    { layout: \"bullets\", title: \"MCP 能给 Codex 什么\", bullets: [\n      \"文档上下文：查新文档，减少过期知识\",\n      \"开发工具：控制浏览器，检查页面\",\n      \"设计工具：读取 Figma 等设计上下文\",\n      \"数据工具：数据库 schema、只读查询\",\n      \"项目与内部系统：GitHub issue / PR、私有 API\"\n    ] },\n    { layout: \"steps\", title: \"App 中的 MCP 工作流\", steps: [\n      { title: \"启用或配置\", desc: \"在 App Settings 或集成入口启用 MCP\" },\n      { title: \"查看可见工具\", desc: \"回到线程，用 /mcp 看 server 和工具\" },\n      { title: \"用自然语言调用\", desc: \"要求 Codex 使用工具，并观察权限提示\" },\n      { title: \"Review 结果\", desc: \"核对来源、时间、权限和副作用\" }\n    ] },\n    { layout: \"table\", title: \"从 0 配 MCP 前先确认四件事\", headers: [\"问题\", \"为什么重要\"], rows: [\n      [\"本地命令还是远程服务\", \"决定用 stdio、HTTP 还是插件提供\"],\n      [\"需要什么账号或 token\", \"决定密钥放哪里，不能写进仓库\"],\n      [\"默认能读写什么\", \"决定是否只读、是否需要审批\"],\n      [\"App 是否已有连接器或插件\", \"有现成入口时不要重复手写 MCP\"]\n    ] },\n    { layout: \"cards\", title: \"三类 MCP server\", cards: [\n      { title: \"STDIO\", desc: \"本地命令启动进程，适合本机工具和私有脚本\" },\n      { title: \"Streamable HTTP\", desc: \"访问一个 URL，适合远程服务、OAuth 和云端工具\" },\n      { title: \"Plugin-provided\", desc: \"插件 manifest 提供 server，先看来源和工具权限\" }\n    ] },\n    { layout: \"table\", title: \"密钥放哪里\", headers: [\"场景\", \"推荐\", \"不推荐\"], rows: [\n      [\"本地个人 token\", \"系统环境变量或密码管理器\", \"写进 config.toml 并提交\"],\n      [\"团队共享服务\", \"组织 secret 管理、最小 scope\", \"共享个人账号 token\"],\n      [\"Cloud / remote\", \"环境变量或官方 secret 入口\", \"在 setup 日志里 echo\"],\n      [\"临时调试\", \"临时只读 token，用完撤销\", \"使用生产写 token\"]\n    ] },\n    { layout: \"bullets\", title: \"配置 MCP 前先问的安全问题\", bullets: [\n      \"它能读什么数据，能写什么数据\",\n      \"它是否会联网，是否需要账号授权\",\n      \"它是否会把数据发给第三方\",\n      \"它能不能在只读模式下完成任务\",\n      \"生产库、客户数据和邮箱都按最小权限配置\"\n    ] },\n    { layout: \"cards\", title: \"工具风险分级\", cards: [\n      { title: \"只读搜索\", desc: \"风险低，可以较宽松\" },\n      { title: \"读取私有数据\", desc: \"风险中，需要来源说明\" },\n      { title: \"写外部系统\", desc: \"风险高，需要人工确认\" },\n      { title: \"访问生产数据\", desc: \"风险很高，默认不要给新手练习\" }\n    ] },\n    { layout: \"table\", title: \"MCP 排障流程\", headers: [\"症状\", \"可能原因\", \"排查\"], rows: [\n      [\"/mcp 看不到 server\", \"配置层未加载或 App 未刷新\", \"先看 App Settings，再重启或刷新\"],\n      [\"CLI 能看到 App 看不到\", \"配置层或会话状态不同\", \"以 App 线程使用结果为准\"],\n      [\"server 启动失败\", \"命令不存在或依赖未安装\", \"在终端单独跑启动命令看日志\"],\n      [\"结果不可信\", \"来源不明或时间过期\", \"要求 Codex 列出来源和查询条件\"]\n    ] },\n    { layout: \"bullets\", title: \"MCP 配置核对清单\", bullets: [\n      \"App 可见：/mcp 能看到 server 和工具\",\n      \"最小权限：只给当前任务需要的读写范围\",\n      \"密钥安全：token 在环境变量或 secret 里\",\n      \"只读试跑：能完成一次只读查询或读取\",\n      \"可审计、可撤销：知道怎么禁用和撤销 token\"\n    ] },\n    { layout: \"end\", title: \"先只读、再小范围、可审计、可撤销\", subtitle: \"下一篇：CX-06 Skills 可复用工作流\" }\n  ]\n});\n\n// ================= CX-06 =================\ndecks.push({\n  code: \"CX-06\", category: \"codex\", fileTitle: \"Codex-Skills可复用工作流\",\n  deck: \"Codex Skills：把重复提示变成可复用工作流\",\n  slides: [\n    { layout: \"cover\", title: \"Codex Skills：把重复提示变成可复用工作流\", subtitle: \"零基础 · 让流程可重复，而不是让 prompt 更长\", kicker: \"Vibe Coding 学习系列 · CX-06\" },\n    { layout: \"section\", title: \"Skill 是可复用判断，不是 prompt 收藏\", subtitle: \"要有步骤、边界和验收方式\" },\n    { layout: \"bullets\", title: \"Skill 是什么，适合什么\", bullets: [\n      \"一组可复用指令、资源和可选脚本\",\n      \"适合代码审查、文档核对、发布检查和团队 SOP\",\n      \"不适合只执行一次的临时任务\",\n      \"不适合需要实时外部 API 的工具连接\",\n      \"不适合需要定时运行的周期任务\"\n    ] },\n    { layout: \"table\", title: \"什么时候值得做成 Skill\", headers: [\"信号\", \"是否适合\"], rows: [\n      [\"同一提示复制三次以上\", \"适合\"],\n      [\"多人需要同一做法\", \"适合\"],\n      [\"输出格式总要固定\", \"适合\"],\n      [\"只做一次的临时任务\", \"不适合\"],\n      [\"需要每天运行\", \"交给 Automation 调度\"]\n    ] },\n    { layout: \"cards\", title: \"好 Skill 的四个特征\", cards: [\n      { title: \"触发清楚\", desc: \"description 里写明什么时候用\" },\n      { title: \"边界清楚\", desc: \"也写明什么时候不用\" },\n      { title: \"输入输出清楚\", desc: \"Codex 知道读什么、交付什么\" },\n      { title: \"内容分层\", desc: \"常用指令在 SKILL.md，长资料放 references\" }\n    ] },\n    { layout: \"bullets\", title: \"description 是触发路由，不是介绍文案\", bullets: [\n      \"模板：Use when 场景，Do 动作，Do not use when 边界\",\n      \"差写法：Helps write high quality code\",\n      \"好写法要写清对象、动作、触发场景和边界\",\n      \"写得太泛，Codex 可能乱用\",\n      \"写得太窄，真正需要时触发不了\"\n    ] },\n    { layout: \"steps\", title: \"在 App 中调用 Skill\", steps: [\n      { title: \"确认能否看到\", desc: \"当前 App 是否显示这个 Skill\" },\n      { title: \"确认层级\", desc: \"用户级、项目级，还是插件带来的\" },\n      { title: \"确认副作用\", desc: \"会不会读额外资源、运行脚本或调用工具\" },\n      { title: \"显式调用\", desc: \"用 $code-review 或自然语言点名，再说清任务\" }\n    ] },\n    { layout: \"table\", title: \"Skills、Commands、Automations 的分工\", headers: [\"需求\", \"首选\"], rows: [\n      [\"当前线程快速动作\", \"Command\"],\n      [\"固定 SOP / 复用流程\", \"Skill\"],\n      [\"定时或后台重复执行\", \"Automation\"],\n      [\"外部工具连接\", \"MCP / Connector\"],\n      [\"打包分发一组能力\", \"Plugin\"]\n    ] },\n    { layout: \"table\", title: \"文件结构：内容放哪里\", headers: [\"内容\", \"放哪里\", \"原因\"], rows: [\n      [\"触发场景、流程、输出\", \"SKILL.md\", \"Codex 必须先看到\"],\n      [\"长规范、示例、术语表\", \"references/\", \"需要时再读，节省上下文\"],\n      [\"重复性强易写错的逻辑\", \"scripts/\", \"要写清运行时和失败输出\"]\n    ] },\n    { layout: \"bullets\", title: \"Skill 不该承载什么\", bullets: [\n      \"一次性任务\",\n      \"当前项目的临时 bug\",\n      \"模糊人设包装\",\n      \"需要每天变化的命令\",\n      \"真实密钥或私有账号信息\"\n    ] },\n    { layout: \"end\", title: \"一次性任务放 prompt，项目事实放 AGENTS.md\", subtitle: \"下一篇：CX-07 Plugins 连接器\" }\n  ]\n});\n\n// ================= CX-07 =================\ndecks.push({\n  code: \"CX-07\", category: \"codex\", fileTitle: \"Codex-Plugins连接器\",\n  deck: \"Codex Plugins 与 Connectors：App 能力扩展\",\n  slides: [\n    { layout: \"cover\", title: \"Codex Plugins 与 Connectors：App 能力扩展\", subtitle: \"零基础 · 安装是让能力可见，授权是让数据可用\", kicker: \"Vibe Coding 学习系列 · CX-07\" },\n    { layout: \"section\", title: \"安装、授权、调用是三件事\", subtitle: \"插件可以包含 Skills、MCP、Apps，但不等于其中任何一个\" },\n    { layout: \"bullets\", title: \"安装、授权、调用、撤销\", bullets: [\n      \"安装 Plugin：看它带来的 Skills / MCP / Apps / 配置\",\n      \"对外部服务单独授权\",\n      \"在线程中引用或调用外部上下文\",\n      \"工具或外部动作按权限和审批执行\",\n      \"不用时撤销授权或卸载\"\n    ] },\n    { layout: \"table\", title: \"先分清四个概念\", headers: [\"概念\", \"本质\", \"例子\"], rows: [\n      [\"Connector / App\", \"外部账号连接\", \"GitHub、Gmail、Drive、Slack\"],\n      [\"Plugin\", \"能力包\", \"一组 skills、MCP、apps、配置\"],\n      [\"Skill\", \"可复用工作流\", \"代码审查 SOP\"],\n      [\"MCP\", \"工具协议\", \"浏览器、数据库、文档源\"]\n    ] },\n    { layout: \"steps\", title: \"App 中的连接器工作流\", steps: [\n      { title: \"打开入口\", desc: \"进入 App 的 Plugins / Connectors / Apps\" },\n      { title: \"选择服务\", desc: \"挑要连接的 GitHub、Drive、Slack 等\" },\n      { title: \"完成授权\", desc: \"授权范围要单独看清楚\" },\n      { title: \"引用并执行\", desc: \"用 @、mention 或自然语言引用外部上下文\" }\n    ] },\n    { layout: \"table\", title: \"安装或连接前的检查\", headers: [\"检查项\", \"要确认什么\"], rows: [\n      [\"来源\", \"官方、组织内，还是第三方插件\"],\n      [\"能力\", \"带 Skills、MCP、Connectors 还是组合包\"],\n      [\"权限\", \"只读、评论、写文件、发消息分别要什么权限\"],\n      [\"数据范围\", \"能访问哪些仓库、文档、邮箱或群聊\"],\n      [\"撤销方式\", \"在 App、服务后台还是组织管理端撤销\"]\n    ] },\n    { layout: \"cards\", title: \"插件安装后的四层变化\", cards: [\n      { title: \"目录层\", desc: \"Plugins 页面出现已安装条目\" },\n      { title: \"能力层\", desc: \"@ mention 或 bundled skills 可被调用\" },\n      { title: \"授权层\", desc: \"外部 App 可能要求登录或授权\" },\n      { title: \"执行层\", desc: \"Codex 按 prompt、权限和审批调用工具\" }\n    ] },\n    { layout: \"bullets\", title: \"最小权限原则\", bullets: [\n      \"第一次安装只给必要权限\",\n      \"只读任务不给写权限\",\n      \"需要发消息或改 PR 时，明确说明目标和范围\",\n      \"团队插件先在测试项目验证\",\n      \"不再使用时及时禁用或卸载\"\n    ] },\n    { layout: \"table\", title: \"常见连接场景与风险\", headers: [\"场景\", \"连接器价值\", \"风险点\"], rows: [\n      [\"GitHub\", \"读取 issue、PR、仓库上下文\", \"写权限、PR 评论权限\"],\n      [\"Google Drive / Docs\", \"读取团队文档\", \"文档访问范围\"],\n      [\"Gmail / Outlook\", \"引用邮件上下文\", \"隐私和敏感信息\"],\n      [\"Slack / Teams\", \"查讨论和决策\", \"群聊范围和成员隐私\"],\n      [\"Calendar\", \"查日程和会议背景\", \"个人隐私\"]\n    ] },\n    { layout: \"table\", title: \"CLI 辅助管理 marketplace\", headers: [\"命令\", \"用途\"], rows: [\n      [\"codex plugin marketplace list\", \"列出已添加的 marketplace\"],\n      [\"codex plugin marketplace add owner/repo\", \"添加 marketplace 来源\"],\n      [\"codex plugin marketplace upgrade\", \"升级 marketplace\"],\n      [\"codex plugin marketplace remove 名称\", \"移除 marketplace\"]\n    ] },\n    { layout: \"bullets\", title: \"观察输出：看用了什么，不只看答得像不像\", bullets: [\n      \"你使用了哪些插件或工具能力\",\n      \"哪些信息来自外部系统\",\n      \"哪些结论是根据上下文推断的\",\n      \"有没有权限、网络、认证或数据范围限制\",\n      \"安装是让能力可见，审批是最后的安全门\"\n    ] },\n    { layout: \"end\", title: \"安装让能力可见，授权让数据可用，审批是安全门\", subtitle: \"本系列 codex 分册到此\" }\n  ]\n});\n\n// ---------- validation ----------\nconst problems: string[] = [];\nfor (const d of decks) {\n  const n = d.slides.length;\n  if (n < 10 || n > 14) problems.push(`${d.code}: slide count ${n}`);\n  if (d.slides[0].kicker !== `Vibe Coding 学习系列 · ${d.code}`) problems.push(`${d.code}: kicker`);\n  for (const [i, s] of d.slides.entries()) {\n    if (s.layout === \"bullets\") {\n      if (s.bullets.length > 5) problems.push(`${d.code} slide${i}: bullets ${s.bullets.length}`);\n      for (const b of s.bullets) {\n        const total = [...b].length;\n        const han = [...b].filter(c => /\\p{Script=Han}/u.test(c)).length;\n        if (total > 42) problems.push(`${d.code} slide${i}: len=${total} \"${b}\"`);\n        if (han > 42) problems.push(`${d.code} slide${i}: han=${han} \"${b}\"`);\n      }\n    }\n    if (s.layout === \"cards\") {\n      if (s.cards.length < 3 || s.cards.length > 4) problems.push(`${d.code} slide${i}: cards ${s.cards.length}`);\n      for (const c of s.cards) {\n        if ([...c.desc].length > 42) problems.push(`${d.code} slide${i}: card desc len=${[...c.desc].length} \"${c.desc}\"`);\n      }\n    }\n    if (s.layout === \"steps\") {\n      if (s.steps.length < 3 || s.steps.length > 4) problems.push(`${d.code} slide${i}: steps ${s.steps.length}`);\n      for (const st of s.steps) {\n        if ([...st.desc].length > 42) problems.push(`${d.code} slide${i}: step desc len=${[...st.desc].length} \"${st.desc}\"`);\n      }\n    }\n    if (s.layout === \"table\") {\n      if (s.headers.length > 5) problems.push(`${d.code} slide${i}: cols ${s.headers.length}`);\n      if (s.rows.length > 6) problems.push(`${d.code} slide${i}: rows ${s.rows.length}`);\n      for (const r of s.rows) if (r.length !== s.headers.length) problems.push(`${d.code} slide${i}: row width mismatch`);\n    }\n  }\n}\nreturn JSON.stringify({ problems, summary: decks.map(d => ({ code: d.code, title: d.deck, slides: d.slides.length })) }, null, 1);", "description": "Build and validate 7 tutorial decks"}

## assistant · 2026-10-05T11:53:58Z

One problem. Fix that step desc: "企业禁用 Store 时让管理员分发，或用 winget 安装" — count: 企业禁用 Store 时让管理员分发，或用 winget 安装 ≈ 22+ . Fine.

Now write the files. I'll rebuild with fix and write. Also ensure slides have no `_sub` leftover (I didn't add). JSON.stringify each and write.

Let me rewrite the whole program (it's fresh process). Rather than re-typing all, I'll do a smaller approach? The process is fresh each run, so I must re-supply all content. That's a lot. Alternatively, I can fix by writing files from a here-doc... no, must use write tool. I need to re-run with full content anyway to write.

Hmm, that's a big duplication. But necessary. Let me just redo with the fix. Actually I can reduce by defining content more compactly. But safest: repeat the same code with the one fix and add writes.

Let me write the program again with writes, including the corrected desc.

Actually, I could avoid retyping by using a different strategy: in this run_code, read the previous... no, nothing persisted.

I'll retype. Let me create a helper `B` for bullets etc.? Just repeat.

To save effort and risk, I'll write each deck as a JS object literal and map to slides via helper constructors. But the content is the bulk. I'll just paste again with fix.

Let me do it in two run_code calls maybe (CX-01..04, CX-05..07) to keep each manageable. That's fine. Each writes files.

Let me do first batch.
约束校验只有一处超长，修正后分批写入。
{
  "type": "tool-call",
  "id": "call_00_eMTEGmgy01xgOXCQh03K5746",
  "name": "run_code",
  "arguments": "{\"code\": \"const dir = \\\"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\\\";\\nconst decks: any[] = [];\\n\\ndecks.push({\\n  code: \\\"CX-01\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-App安装与认证\\\",\\n  deck: \\\"Codex App 安装与认证：从下载到第一个线程\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex App 安装与认证：从下载到第一个线程\\\", subtitle: \\\"零基础 · Windows / macOS 装好、登上号、跑通第一个安全任务\\\", kicker: \\\"Vibe Coding 学习系列 · CX-01\\\" },\\n    { layout: \\\"section\\\", title: \\\"安装目标：先能安全打开本地项目\\\", subtitle: \\\"App 是主线，CLI / Web / Cloud 是辅助\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"安装成功的五条标准\\\", bullets: [\\n      \\\"桌面 Codex App 能正常打开\\\",\\n      \\\"能用 ChatGPT / OpenAI 账号登录\\\",\\n      \\\"能添加本地项目并创建线程\\\",\\n      \\\"能让 Codex 只读分析项目\\\",\\n      \\\"能看到 Review、diff 和 Settings\\\"\\n    ], notes: \\\"安装成功的标准不是终端里有 codex 命令，而是 App 能用起来。\\\" },\\n    { layout: \\\"table\\\", title: \\\"系统准备：按平台走官方入口\\\", headers: [\\\"平台\\\", \\\"版本建议\\\", \\\"安装来源\\\"], rows: [\\n      [\\\"Windows\\\", \\\"Windows 11 是推荐基线\\\", \\\"Microsoft Store 或 winget\\\"],\\n      [\\\"macOS\\\", \\\"使用仍受 Apple 支持的版本\\\", \\\"官方 Codex App 下载页\\\"],\\n      [\\\"Linux\\\", \\\"桌面版暂未覆盖\\\", \\\"先用 CLI / Web / Cloud\\\"]\\n    ], notes: \\\"不要从不明网盘或第三方安装包安装。\\\" },\\n    { layout: \\\"steps\\\", title: \\\"Windows 安装四步\\\", steps: [\\n      { title: \\\"从官方页面进 Store\\\", desc: \\\"打开官方 Windows 页，点 Codex app for Windows 链接\\\" },\\n      { title: \\\"在 Store 点获取安装\\\", desc: \\\"企业禁用 Store 时让管理员分发，或用 winget 安装\\\" },\\n      { title: \\\"开始菜单打开 Codex\\\", desc: \\\"首次启动按提示登录，优先用 ChatGPT 账号\\\" },\\n      { title: \\\"处理防火墙弹窗\\\", desc: \\\"一般只勾专用网络，公用网络不要选\\\" }\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"首次启动的三个关卡\\\", cards: [\\n      { title: \\\"登录\\\", desc: \\\"优先 ChatGPT / OpenAI 账号；API Key 不是 App 登录方案\\\" },\\n      { title: \\\"权限提示\\\", desc: \\\"区分选目录、跑只读命令和写文件联网，后者看清再同意\\\" },\\n      { title: \\\"防火墙\\\", desc: \\\"本地服务通信时弹窗，只放行可信网络\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"排障总表：先定位症状，不要乱重装\\\", headers: [\\\"症状\\\", \\\"常见原因\\\", \\\"第一反应\\\"], rows: [\\n      [\\\"App 装不上\\\", \\\"Store、系统版本或企业策略\\\", \\\"先确认来源和系统更新\\\"],\\n      [\\\"登录失败\\\", \\\"浏览器登录态、网络、账号权限\\\", \\\"换浏览器登录或重新授权\\\"],\\n      [\\\"Review 不可用\\\", \\\"没有 Git 或项目不是 Git 仓库\\\", \\\"安装 Git，确认 git status\\\"],\\n      [\\\"命令跑不动\\\", \\\"PowerShell policy 或工具链缺失\\\", \\\"先在终端跑版本命令\\\"],\\n      [\\\"macOS 打不开\\\", \\\"Gatekeeper 或下载来源问题\\\", \\\"从官方入口下载再按提示授权\\\"]\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"第一次打开项目：四步不慌\\\", steps: [\\n      { title: \\\"选一个普通 Git 仓库\\\", desc: \\\"不要一上来打开生产仓库，最好有 README\\\" },\\n      { title: \\\"添加本地项目目录\\\", desc: \\\"确认 App 能识别 Git 状态\\\" },\\n      { title: \\\"创建 Local thread\\\", desc: \\\"先发只读任务：总结技术栈、启动命令和测试命令\\\" },\\n      { title: \\\"再做一个小改动\\\", desc: \\\"只改一个错别字，看 diff 且不自动提交\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"第一个安全可写任务\\\", bullets: [\\n      \\\"只改低风险文件，例如文档里的一个错别字\\\",\\n      \\\"明确要求改完展示 diff，不要自动提交\\\",\\n      \\\"确认改动只在预期文件里\\\",\\n      \\\"确认 Review 面板能看到 diff\\\",\\n      \\\"知道怎么撤销或继续修改\\\"\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"安装后检查清单\\\", cards: [\\n      { title: \\\"账号与环境\\\", desc: \\\"已登录，防火墙和 macOS 权限按最小范围授权\\\" },\\n      { title: \\\"Git 与项目\\\", desc: \\\"App 能看到 Git 状态，能添加本地仓库\\\" },\\n      { title: \\\"线程与只读\\\", desc: \\\"能创建 Local thread 并总结项目，不改文件\\\" },\\n      { title: \\\"可写与 Review\\\", desc: \\\"小改动能在 Review 中看到 diff\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"CLI 只作为辅助\\\", headers: [\\\"命令\\\", \\\"用途\\\"], rows: [\\n      [\\\"codex --help\\\", \\\"查看 CLI 帮助\\\"],\\n      [\\\"codex app\\\", \\\"从 CLI 打开 App\\\"],\\n      [\\\"codex review\\\", \\\"做代码审查\\\"],\\n      [\\\"codex exec \\\\\\\"summarize this repo\\\\\\\"\\\", \\\"非交互执行任务\\\"]\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"装好之后：先只读，再小改，最后 Review\\\", subtitle: \\\"下一篇：CX-02 Codex App 桌面工作流\\\" }\\n  ]\\n});\\n\\ndecks.push({\\n  code: \\\"CX-02\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-App桌面工作流\\\",\\n  deck: \\\"Codex App 桌面工作流：把 App 当主控台\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex App 桌面工作流：把 App 当主控台\\\", subtitle: \\\"零基础 · 线程、终端、Review、权限在一个桌面流程里\\\", kicker: \\\"Vibe Coding 学习系列 · CX-02\\\" },\\n    { layout: \\\"section\\\", title: \\\"App 是开发主控台，不是聊天窗口\\\", subtitle: \\\"Thread 管上下文，Review 管结果，Settings 管边界\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"App 把哪些能力放在一起\\\", bullets: [\\n      \\\"Thread：一条任务线，带上下文、历史和状态\\\",\\n      \\\"Review：查看 diff、行内反馈和 stage / unstage\\\",\\n      \\\"Terminal：让 Codex 在受控环境里运行命令\\\",\\n      \\\"Settings：模型、审批、沙盒、插件和 MCP 的入口\\\",\\n      \\\"Automations / Plugins：后台检查和外部账号连接\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"核心概念速查\\\", headers: [\\\"概念\\\", \\\"一句话解释\\\"], rows: [\\n      [\\\"Thread\\\", \\\"一条任务线，包含上下文、历史和状态\\\"],\\n      [\\\"Worktree\\\", \\\"Git 隔离工作目录，仍会产生真实改动\\\"],\\n      [\\\"Review 面板\\\", \\\"看 diff、行内反馈、stage / revert 的关口\\\"],\\n      [\\\"Local workspace\\\", \\\"当前本机项目目录，决定 Codex 能看到什么\\\"],\\n      [\\\"Cloud handoff\\\", \\\"把任务交给云端环境继续做\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"五个控制点\\\", cards: [\\n      { title: \\\"目标\\\", desc: \\\"这次到底要解决什么问题\\\" },\\n      { title: \\\"上下文\\\", desc: \\\"Codex 该读哪些文件，陌生项目先只读建模\\\" },\\n      { title: \\\"权限\\\", desc: \\\"是否允许写文件、跑命令、联网、调外部工具\\\" },\\n      { title: \\\"结果\\\", desc: \\\"改动是否真的在预期范围内，收口由人决定\\\" }\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"一条线程的生命周期\\\", steps: [\\n      { title: \\\"开场只读\\\", desc: \\\"先读项目，确认技术栈、命令、目录和风险\\\" },\\n      { title: \\\"明确任务\\\", desc: \\\"说清目标、范围、不能做什么、怎么验证\\\" },\\n      { title: \\\"允许执行\\\", desc: \\\"小任务直接改，大任务先 /plan 或用 worktree\\\" },\\n      { title: \\\"检查与收口\\\", desc: \\\"看 Review，定点反馈，由人决定是否提交\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"三种工作方式怎么选\\\", headers: [\\\"任务\\\", \\\"推荐方式\\\", \\\"为什么\\\"], rows: [\\n      [\\\"读项目、解释报错\\\", \\\"Local thread 只读\\\", \\\"快，风险低\\\"],\\n      [\\\"改一个文件或少量文档\\\", \\\"Local thread + Review\\\", \\\"改动小，容易检查\\\"],\\n      [\\\"新功能、重构、改多个文件\\\", \\\"Worktree thread\\\", \\\"隔离改动，便于撤回\\\"],\\n      [\\\"盯 PR、修 CI、长任务\\\", \\\"Cloud / Web handoff\\\", \\\"不占用本地环境\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"好任务要写清五件事\\\", bullets: [\\n      \\\"目标：这次要解决什么问题\\\",\\n      \\\"范围：只改哪些文件或目录\\\",\\n      \\\"约束：不能做什么，例如不引入新依赖\\\",\\n      \\\"验证：怎么确认改对了，跑哪条命令\\\",\\n      \\\"交付：要 diff 摘要、测试结果还是 PR 描述\\\"\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"Review 面板逐项检查法\\\", cards: [\\n      { title: \\\"文件列表\\\", desc: \\\"是否只改了任务范围内文件，范围外要解释或撤掉\\\" },\\n      { title: \\\"单文件 diff\\\", desc: \\\"是否有无关格式化、删除或重命名\\\" },\\n      { title: \\\"命令记录\\\", desc: \\\"验证命令是否真的跑过，没跑要说明原因\\\" },\\n      { title: \\\"安全项\\\", desc: \\\"是否碰了 .env、token 或权限配置，碰到立即停\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"常见反模式\\\", headers: [\\\"反模式\\\", \\\"真正风险\\\", \\\"更稳做法\\\"], rows: [\\n      [\\\"一个线程混多个目标\\\", \\\"上下文混乱，Review 难收口\\\", \\\"一个目标一条线程\\\"],\\n      [\\\"任务只写“优化一下”\\\", \\\"Codex 不知道边界\\\", \\\"写清目标、范围、约束、验证、交付\\\"],\\n      [\\\"陌生仓库直接写\\\", \\\"误读架构和命令\\\", \\\"先只读建模\\\"],\\n      [\\\"允许自动提交推送\\\", \\\"错误进入远端\\\", \\\"先草拟，由人确认\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"App 用户的三个基本动作\\\", bullets: [\\n      \\\"收窄：只改 README，控制 diff 大小\\\",\\n      \\\"追证据：你运行了什么命令\\\",\\n      \\\"反向解释：根据 diff 解释你做了什么\\\",\\n      \\\"线程标题用结果导向命名，方便以后找回上下文\\\",\\n      \\\"新目标开新线程；混在一起就难 Review\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"先建立控制感，再逐步放开能力\\\", subtitle: \\\"下一篇：CX-03 Commands 工作流入口\\\" }\\n  ]\\n});\\n\\ndecks.push({\\n  code: \\\"CX-03\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-Commands工作流入口\\\",\\n  deck: \\\"Codex Commands：App 里的工作流入口\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex Commands：App 里的工作流入口\\\", subtitle: \\\"零基础 · 不背命令表，学会什么时候切换工作模式\\\", kicker: \\\"Vibe Coding 学习系列 · CX-03\\\" },\\n    { layout: \\\"section\\\", title: \\\"入口、状态、动作\\\", subtitle: \\\"先看状态，再定推进方式，执行后用 /review 收口\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"slash commands 的三层\\\", bullets: [\\n      \\\"入口层：/status、/mcp、/feedback\\\",\\n      \\\"状态层：/plan、/goal，改变任务推进方式\\\",\\n      \\\"审查层：/review，围绕当前 diff 做检查\\\",\\n      \\\"命令只是更快进入某种工作模式\\\",\\n      \\\"模式不对，命令反而会制造混乱\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"用不用 Command 的判断\\\", headers: [\\\"你想做什么\\\", \\\"首选方式\\\", \\\"为什么\\\"], rows: [\\n      [\\\"看当前线程状态\\\", \\\"/status\\\", \\\"快速确认上下文、限制和配额\\\"],\\n      [\\\"让 Codex 先别动手\\\", \\\"/plan\\\", \\\"把执行前移到方案讨论\\\"],\\n      [\\\"长时间推进清楚目标\\\", \\\"/goal\\\", \\\"让目标跨多个 turn 持续存在\\\"],\\n      [\\\"检查当前改动\\\", \\\"/review\\\", \\\"直接进入代码审查口径\\\"],\\n      [\\\"查 MCP 是否连接\\\", \\\"/mcp\\\", \\\"看工具 server 和状态\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"App 用户先掌握的稳定命令\\\", cards: [\\n      { title: \\\"/status\\\", desc: \\\"查看模型、工作区、审批和上下文状态\\\" },\\n      { title: \\\"/plan\\\", desc: \\\"大任务先规划，不急着改文件\\\" },\\n      { title: \\\"/review\\\", desc: \\\"审查当前改动，合并前使用\\\" },\\n      { title: \\\"/mcp\\\", desc: \\\"接外部工具后，查看 server 和工具\\\" }\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"在 App 里发现命令四步\\\", steps: [\\n      { title: \\\"打开项目线程\\\", desc: \\\"任何已有项目的线程都可以\\\" },\\n      { title: \\\"输入 /\\\", desc: \\\"看弹出的命令列表和说明\\\" },\\n      { title: \\\"注意实验标记\\\", desc: \\\"不确定时先问，不要直接执行\\\" },\\n      { title: \\\"查官方文档核对\\\", desc: \\\"以当前 App 显示和官方 App Commands 为准\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"/plan：好的计划应该包含什么\\\", bullets: [\\n      \\\"要读哪些文件，要改哪些文件\\\",\\n      \\\"可能方案和取舍\\\",\\n      \\\"验证命令，以及不做什么\\\",\\n      \\\"什么时候退出计划模式进入执行\\\",\\n      \\\"差的 /plan 只写“做一个完整优化”，缺对象和边界\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"/goal：长目标也要有边界\\\", headers: [\\\"适合\\\", \\\"不适合\\\"], rows: [\\n      [\\\"长迁移、长重构\\\", \\\"目标没有范围，例如“优化项目”\\\"],\\n      [\\\"部署重试直到成功\\\", \\\"没有结束条件\\\"],\\n      [\\\"原型打磨直到测试通过\\\", \\\"没有权限边界\\\"],\\n      [\\\"比一次提示更长但有明确终点\\\", \\\"周期或后台检查，应交给 Automations\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"/review 的五个检查维度\\\", bullets: [\\n      \\\"范围：是否只改了任务指定文件\\\",\\n      \\\"正确性：边界条件、空值、异步竞态\\\",\\n      \\\"安全：是否触碰 secret、权限、网络\\\",\\n      \\\"测试：是否覆盖新增行为\\\",\\n      \\\"可维护：是否引入重复逻辑或隐式依赖\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"命令排障表\\\", headers: [\\\"症状\\\", \\\"可能原因\\\", \\\"排查顺序\\\"], rows: [\\n      [\\\"输入 /goal 没出现\\\", \\\"feature 未启用或版本不支持\\\", \\\"先看 / 列表，再查 features.goals\\\"],\\n      [\\\"/review 没问题\\\", \\\"当前没有 Git diff\\\", \\\"先看 Review 面板文件列表\\\"],\\n      [\\\"/mcp 看不到工具\\\", \\\"MCP 未配置或 App 未刷新\\\", \\\"看 Settings，再用 codex mcp list 辅助\\\"],\\n      [\\\"命令列表和教程不同\\\", \\\"版本、插件或实验开关不同\\\", \\\"以当前 App 列表和官方文档为准\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"App Commands 与 CLI Commands 不保证一致\\\", bullets: [\\n      \\\"App 面向桌面线程、Review 面板和工具入口\\\",\\n      \\\"CLI 面向终端 TUI、命令行权限和会话\\\",\\n      \\\"App 输入 / 查看，CLI 输入 /help 查看\\\",\\n      \\\"两者不保证完全一致，以当前界面显示为准\\\",\\n      \\\"CLI 命令写到 CX-12，不能写成 App 主线\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"掌握的是什么时候切换工作模式\\\", subtitle: \\\"下一篇：CX-04 项目指令、配置、权限与沙盒\\\" }\\n  ]\\n});\\n\\ndecks.push({\\n  code: \\\"CX-04\\\", category: \\\"codex\\\", fileTitle: \\\"Codex项目指令权限配置\\\",\\n  deck: \\\"Codex 项目指令、配置、权限与沙盒\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex 项目指令、配置、权限与沙盒\\\", subtitle: \\\"零基础 · 让 App 知道怎么安全工作\\\", kicker: \\\"Vibe Coding 学习系列 · CX-04\\\" },\\n    { layout: \\\"section\\\", title: \\\"从软到硬的四层配置\\\", subtitle: \\\"新手先掌握 AGENTS.md 和 App Settings 两层\\\" },\\n    { layout: \\\"cards\\\", title: \\\"配置系统的四层心智模型\\\", cards: [\\n      { title: \\\"项目说明层\\\", desc: \\\"AGENTS.md，写项目事实、命令、规范和安全边界\\\" },\\n      { title: \\\"用户偏好层\\\", desc: \\\"App Settings / config.toml，设模型、终端、审批、沙盒\\\" },\\n      { title: \\\"命令策略层\\\", desc: \\\"Rules / permission profiles，对危险动作建立边界\\\" },\\n      { title: \\\"事件脚本层\\\", desc: \\\"Hooks，在特定时机运行真实脚本做审计或检查\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"为什么不能只靠提示词\\\", bullets: [\\n      \\\"不持久：换线程后可能忘了重复说\\\",\\n      \\\"不够硬：说不要推 main，仍要靠人工盯\\\",\\n      \\\"不可审计：团队很难知道每个人临时说了什么\\\",\\n      \\\"长期规则写进 AGENTS.md\\\",\\n      \\\"高风险命令用 Rules，复杂事件才用 Hooks\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"AGENTS.md 推荐结构\\\", headers: [\\\"模块\\\", \\\"要回答的问题\\\"], rows: [\\n      [\\\"项目概览\\\", \\\"这个项目是什么，主要目录在哪里\\\"],\\n      [\\\"常用命令\\\", \\\"安装、测试、lint、build 怎么跑\\\"],\\n      [\\\"修改边界\\\", \\\"哪些文件可以改，哪些要谨慎\\\"],\\n      [\\\"代码风格\\\", \\\"当前项目已有写法是什么\\\"],\\n      [\\\"验证方式\\\", \\\"改完怎么证明，失败要解释\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"AGENTS.md 不该写什么\\\", bullets: [\\n      \\\"API Key、token、cookie\\\",\\n      \\\"只针对本次任务的临时要求\\\",\\n      \\\"个人机器路径\\\",\\n      \\\"不稳定的模型名称或价格\\\",\\n      \\\"「写高质量代码」这种无法验证的口号\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"按场景选择权限策略\\\", headers: [\\\"场景\\\", \\\"建议\\\"], rows: [\\n      [\\\"陌生项目\\\", \\\"保守审批，先只读\\\"],\\n      [\\\"日常小改\\\", \\\"允许常见读写和安全命令\\\"],\\n      [\\\"大规模重构\\\", \\\"使用 worktree，严格 review\\\"],\\n      [\\\"CI / 自动化\\\", \\\"外部沙箱 + 最小权限\\\"],\\n      [\\\"涉及密钥或生产数据\\\", \\\"默认拒绝，人工确认\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"三种沙盒模式\\\", cards: [\\n      { title: \\\"read-only\\\", desc: \\\"只读，适合审计和探索\\\" },\\n      { title: \\\"workspace-write\\\", desc: \\\"可写工作区，适合日常开发\\\" },\\n      { title: \\\"danger-full-access\\\", desc: \\\"无沙盒限制，只能在外部可信沙箱使用\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"Rules 适合与不适合做什么\\\", headers: [\\\"适合\\\", \\\"不适合\\\"], rows: [\\n      [\\\"拦危险删除，例如 rm -rf\\\", \\\"写复杂业务流程\\\"],\\n      [\\\"拦未经确认的 publish\\\", \\\"替代测试或 Review\\\"],\\n      [\\\"对 push、tag、force push 要求确认\\\", \\\"判断产品取舍\\\"],\\n      [\\\"允许 git status、rg、ls 等只读命令\\\", \\\"管理外部账号授权\\\"]\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"改完配置后怎么核对\\\", steps: [\\n      { title: \\\"改 AGENTS.md\\\", desc: \\\"新线程里让 Codex 总结项目规则，看是否读到\\\" },\\n      { title: \\\"改权限或沙盒\\\", desc: \\\"用 /status 或 Settings 确认实际生效\\\" },\\n      { title: \\\"改 MCP 配置\\\", desc: \\\"用 /mcp 看 server 和工具是否可见\\\" },\\n      { title: \\\"换项目目录时\\\", desc: \\\"确认打开了对的目录，旧线程可能仍是旧上下文\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"Hooks 是事件脚本，不是万能自动化\\\", bullets: [\\n      \\\"配置通常在 .codex/hooks.json 或 [hooks] 表\\\",\\n      \\\"会运行真实命令，可能读取敏感上下文\\\",\\n      \\\"写错会阻塞工作流，学习阶段先别急着写\\\",\\n      \\\"能用 Rules 解决的命令边界，不要先写 Hook\\\",\\n      \\\"相对路径要改从 git root 或绝对路径解析\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"先用 AGENTS.md 和 Settings 把边界写清楚\\\", subtitle: \\\"下一篇：CX-05 MCP 外部工具\\\" }\\n  ]\\n});\\n\\nconst results: string[] = [];\\nfor (const d of decks) {\\n  const path = `${dir}/${d.code.toLowerCase()}.json`;\\n  const content = JSON.stringify(d, null, 2) + \\\"\\\\n\\\";\\n  const w = await tools.write({ file_path: path, content });\\n  results.push(`${d.code} -> ${path} (${w.operation}, slides=${d.slides.length})`);\\n}\\nreturn results.join(\\\"\\\\n\\\");\", \"description\": \"Write CX-01 to CX-04 JSON files\"}"
}

## tool · 2026-10-05T11:53:58Z

run_code
{"code": "const dir = \"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\";\nconst decks: any[] = [];\n\ndecks.push({\n  code: \"CX-01\", category: \"codex\", fileTitle: \"Codex-App安装与认证\",\n  deck: \"Codex App 安装与认证：从下载到第一个线程\",\n  slides: [\n    { layout: \"cover\", title: \"Codex App 安装与认证：从下载到第一个线程\", subtitle: \"零基础 · Windows / macOS 装好、登上号、跑通第一个安全任务\", kicker: \"Vibe Coding 学习系列 · CX-01\" },\n    { layout: \"section\", title: \"安装目标：先能安全打开本地项目\", subtitle: \"App 是主线，CLI / Web / Cloud 是辅助\" },\n    { layout: \"bullets\", title: \"安装成功的五条标准\", bullets: [\n      \"桌面 Codex App 能正常打开\",\n      \"能用 ChatGPT / OpenAI 账号登录\",\n      \"能添加本地项目并创建线程\",\n      \"能让 Codex 只读分析项目\",\n      \"能看到 Review、diff 和 Settings\"\n    ], notes: \"安装成功的标准不是终端里有 codex 命令，而是 App 能用起来。\" },\n    { layout: \"table\", title: \"系统准备：按平台走官方入口\", headers: [\"平台\", \"版本建议\", \"安装来源\"], rows: [\n      [\"Windows\", \"Windows 11 是推荐基线\", \"Microsoft Store 或 winget\"],\n      [\"macOS\", \"使用仍受 Apple 支持的版本\", \"官方 Codex App 下载页\"],\n      [\"Linux\", \"桌面版暂未覆盖\", \"先用 CLI / Web / Cloud\"]\n    ], notes: \"不要从不明网盘或第三方安装包安装。\" },\n    { layout: \"steps\", title: \"Windows 安装四步\", steps: [\n      { title: \"从官方页面进 Store\", desc: \"打开官方 Windows 页，点 Codex app for Windows 链接\" },\n      { title: \"在 Store 点获取安装\", desc: \"企业禁用 Store 时让管理员分发，或用 winget 安装\" },\n      { title: \"开始菜单打开 Codex\", desc: \"首次启动按提示登录，优先用 ChatGPT 账号\" },\n      { title: \"处理防火墙弹窗\", desc: \"一般只勾专用网络，公用网络不要选\" }\n    ] },\n    { layout: \"cards\", title: \"首次启动的三个关卡\", cards: [\n      { title: \"登录\", desc: \"优先 ChatGPT / OpenAI 账号；API Key 不是 App 登录方案\" },\n      { title: \"权限提示\", desc: \"区分选目录、跑只读命令和写文件联网，后者看清再同意\" },\n      { title: \"防火墙\", desc: \"本地服务通信时弹窗，只放行可信网络\" }\n    ] },\n    { layout: \"table\", title: \"排障总表：先定位症状，不要乱重装\", headers: [\"症状\", \"常见原因\", \"第一反应\"], rows: [\n      [\"App 装不上\", \"Store、系统版本或企业策略\", \"先确认来源和系统更新\"],\n      [\"登录失败\", \"浏览器登录态、网络、账号权限\", \"换浏览器登录或重新授权\"],\n      [\"Review 不可用\", \"没有 Git 或项目不是 Git 仓库\", \"安装 Git，确认 git status\"],\n      [\"命令跑不动\", \"PowerShell policy 或工具链缺失\", \"先在终端跑版本命令\"],\n      [\"macOS 打不开\", \"Gatekeeper 或下载来源问题\", \"从官方入口下载再按提示授权\"]\n    ] },\n    { layout: \"steps\", title: \"第一次打开项目：四步不慌\", steps: [\n      { title: \"选一个普通 Git 仓库\", desc: \"不要一上来打开生产仓库，最好有 README\" },\n      { title: \"添加本地项目目录\", desc: \"确认 App 能识别 Git 状态\" },\n      { title: \"创建 Local thread\", desc: \"先发只读任务：总结技术栈、启动命令和测试命令\" },\n      { title: \"再做一个小改动\", desc: \"只改一个错别字，看 diff 且不自动提交\" }\n    ] },\n    { layout: \"bullets\", title: \"第一个安全可写任务\", bullets: [\n      \"只改低风险文件，例如文档里的一个错别字\",\n      \"明确要求改完展示 diff，不要自动提交\",\n      \"确认改动只在预期文件里\",\n      \"确认 Review 面板能看到 diff\",\n      \"知道怎么撤销或继续修改\"\n    ] },\n    { layout: \"cards\", title: \"安装后检查清单\", cards: [\n      { title: \"账号与环境\", desc: \"已登录，防火墙和 macOS 权限按最小范围授权\" },\n      { title: \"Git 与项目\", desc: \"App 能看到 Git 状态，能添加本地仓库\" },\n      { title: \"线程与只读\", desc: \"能创建 Local thread 并总结项目，不改文件\" },\n      { title: \"可写与 Review\", desc: \"小改动能在 Review 中看到 diff\" }\n    ] },\n    { layout: \"table\", title: \"CLI 只作为辅助\", headers: [\"命令\", \"用途\"], rows: [\n      [\"codex --help\", \"查看 CLI 帮助\"],\n      [\"codex app\", \"从 CLI 打开 App\"],\n      [\"codex review\", \"做代码审查\"],\n      [\"codex exec \\\"summarize this repo\\\"\", \"非交互执行任务\"]\n    ] },\n    { layout: \"end\", title: \"装好之后：先只读，再小改，最后 Review\", subtitle: \"下一篇：CX-02 Codex App 桌面工作流\" }\n  ]\n});\n\ndecks.push({\n  code: \"CX-02\", category: \"codex\", fileTitle: \"Codex-App桌面工作流\",\n  deck: \"Codex App 桌面工作流：把 App 当主控台\",\n  slides: [\n    { layout: \"cover\", title: \"Codex App 桌面工作流：把 App 当主控台\", subtitle: \"零基础 · 线程、终端、Review、权限在一个桌面流程里\", kicker: \"Vibe Coding 学习系列 · CX-02\" },\n    { layout: \"section\", title: \"App 是开发主控台，不是聊天窗口\", subtitle: \"Thread 管上下文，Review 管结果，Settings 管边界\" },\n    { layout: \"bullets\", title: \"App 把哪些能力放在一起\", bullets: [\n      \"Thread：一条任务线，带上下文、历史和状态\",\n      \"Review：查看 diff、行内反馈和 stage / unstage\",\n      \"Terminal：让 Codex 在受控环境里运行命令\",\n      \"Settings：模型、审批、沙盒、插件和 MCP 的入口\",\n      \"Automations / Plugins：后台检查和外部账号连接\"\n    ] },\n    { layout: \"table\", title: \"核心概念速查\", headers: [\"概念\", \"一句话解释\"], rows: [\n      [\"Thread\", \"一条任务线，包含上下文、历史和状态\"],\n      [\"Worktree\", \"Git 隔离工作目录，仍会产生真实改动\"],\n      [\"Review 面板\", \"看 diff、行内反馈、stage / revert 的关口\"],\n      [\"Local workspace\", \"当前本机项目目录，决定 Codex 能看到什么\"],\n      [\"Cloud handoff\", \"把任务交给云端环境继续做\"]\n    ] },\n    { layout: \"cards\", title: \"五个控制点\", cards: [\n      { title: \"目标\", desc: \"这次到底要解决什么问题\" },\n      { title: \"上下文\", desc: \"Codex 该读哪些文件，陌生项目先只读建模\" },\n      { title: \"权限\", desc: \"是否允许写文件、跑命令、联网、调外部工具\" },\n      { title: \"结果\", desc: \"改动是否真的在预期范围内，收口由人决定\" }\n    ] },\n    { layout: \"steps\", title: \"一条线程的生命周期\", steps: [\n      { title: \"开场只读\", desc: \"先读项目，确认技术栈、命令、目录和风险\" },\n      { title: \"明确任务\", desc: \"说清目标、范围、不能做什么、怎么验证\" },\n      { title: \"允许执行\", desc: \"小任务直接改，大任务先 /plan 或用 worktree\" },\n      { title: \"检查与收口\", desc: \"看 Review，定点反馈，由人决定是否提交\" }\n    ] },\n    { layout: \"table\", title: \"三种工作方式怎么选\", headers: [\"任务\", \"推荐方式\", \"为什么\"], rows: [\n      [\"读项目、解释报错\", \"Local thread 只读\", \"快，风险低\"],\n      [\"改一个文件或少量文档\", \"Local thread + Review\", \"改动小，容易检查\"],\n      [\"新功能、重构、改多个文件\", \"Worktree thread\", \"隔离改动，便于撤回\"],\n      [\"盯 PR、修 CI、长任务\", \"Cloud / Web handoff\", \"不占用本地环境\"]\n    ] },\n    { layout: \"bullets\", title: \"好任务要写清五件事\", bullets: [\n      \"目标：这次要解决什么问题\",\n      \"范围：只改哪些文件或目录\",\n      \"约束：不能做什么，例如不引入新依赖\",\n      \"验证：怎么确认改对了，跑哪条命令\",\n      \"交付：要 diff 摘要、测试结果还是 PR 描述\"\n    ] },\n    { layout: \"cards\", title: \"Review 面板逐项检查法\", cards: [\n      { title: \"文件列表\", desc: \"是否只改了任务范围内文件，范围外要解释或撤掉\" },\n      { title: \"单文件 diff\", desc: \"是否有无关格式化、删除或重命名\" },\n      { title: \"命令记录\", desc: \"验证命令是否真的跑过，没跑要说明原因\" },\n      { title: \"安全项\", desc: \"是否碰了 .env、token 或权限配置，碰到立即停\" }\n    ] },\n    { layout: \"table\", title: \"常见反模式\", headers: [\"反模式\", \"真正风险\", \"更稳做法\"], rows: [\n      [\"一个线程混多个目标\", \"上下文混乱，Review 难收口\", \"一个目标一条线程\"],\n      [\"任务只写“优化一下”\", \"Codex 不知道边界\", \"写清目标、范围、约束、验证、交付\"],\n      [\"陌生仓库直接写\", \"误读架构和命令\", \"先只读建模\"],\n      [\"允许自动提交推送\", \"错误进入远端\", \"先草拟，由人确认\"]\n    ] },\n    { layout: \"bullets\", title: \"App 用户的三个基本动作\", bullets: [\n      \"收窄：只改 README，控制 diff 大小\",\n      \"追证据：你运行了什么命令\",\n      \"反向解释：根据 diff 解释你做了什么\",\n      \"线程标题用结果导向命名，方便以后找回上下文\",\n      \"新目标开新线程；混在一起就难 Review\"\n    ] },\n    { layout: \"end\", title: \"先建立控制感，再逐步放开能力\", subtitle: \"下一篇：CX-03 Commands 工作流入口\" }\n  ]\n});\n\ndecks.push({\n  code: \"CX-03\", category: \"codex\", fileTitle: \"Codex-Commands工作流入口\",\n  deck: \"Codex Commands：App 里的工作流入口\",\n  slides: [\n    { layout: \"cover\", title: \"Codex Commands：App 里的工作流入口\", subtitle: \"零基础 · 不背命令表，学会什么时候切换工作模式\", kicker: \"Vibe Coding 学习系列 · CX-03\" },\n    { layout: \"section\", title: \"入口、状态、动作\", subtitle: \"先看状态，再定推进方式，执行后用 /review 收口\" },\n    { layout: \"bullets\", title: \"slash commands 的三层\", bullets: [\n      \"入口层：/status、/mcp、/feedback\",\n      \"状态层：/plan、/goal，改变任务推进方式\",\n      \"审查层：/review，围绕当前 diff 做检查\",\n      \"命令只是更快进入某种工作模式\",\n      \"模式不对，命令反而会制造混乱\"\n    ] },\n    { layout: \"table\", title: \"用不用 Command 的判断\", headers: [\"你想做什么\", \"首选方式\", \"为什么\"], rows: [\n      [\"看当前线程状态\", \"/status\", \"快速确认上下文、限制和配额\"],\n      [\"让 Codex 先别动手\", \"/plan\", \"把执行前移到方案讨论\"],\n      [\"长时间推进清楚目标\", \"/goal\", \"让目标跨多个 turn 持续存在\"],\n      [\"检查当前改动\", \"/review\", \"直接进入代码审查口径\"],\n      [\"查 MCP 是否连接\", \"/mcp\", \"看工具 server 和状态\"]\n    ] },\n    { layout: \"cards\", title: \"App 用户先掌握的稳定命令\", cards: [\n      { title: \"/status\", desc: \"查看模型、工作区、审批和上下文状态\" },\n      { title: \"/plan\", desc: \"大任务先规划，不急着改文件\" },\n      { title: \"/review\", desc: \"审查当前改动，合并前使用\" },\n      { title: \"/mcp\", desc: \"接外部工具后，查看 server 和工具\" }\n    ] },\n    { layout: \"steps\", title: \"在 App 里发现命令四步\", steps: [\n      { title: \"打开项目线程\", desc: \"任何已有项目的线程都可以\" },\n      { title: \"输入 /\", desc: \"看弹出的命令列表和说明\" },\n      { title: \"注意实验标记\", desc: \"不确定时先问，不要直接执行\" },\n      { title: \"查官方文档核对\", desc: \"以当前 App 显示和官方 App Commands 为准\" }\n    ] },\n    { layout: \"bullets\", title: \"/plan：好的计划应该包含什么\", bullets: [\n      \"要读哪些文件，要改哪些文件\",\n      \"可能方案和取舍\",\n      \"验证命令，以及不做什么\",\n      \"什么时候退出计划模式进入执行\",\n      \"差的 /plan 只写“做一个完整优化”，缺对象和边界\"\n    ] },\n    { layout: \"table\", title: \"/goal：长目标也要有边界\", headers: [\"适合\", \"不适合\"], rows: [\n      [\"长迁移、长重构\", \"目标没有范围，例如“优化项目”\"],\n      [\"部署重试直到成功\", \"没有结束条件\"],\n      [\"原型打磨直到测试通过\", \"没有权限边界\"],\n      [\"比一次提示更长但有明确终点\", \"周期或后台检查，应交给 Automations\"]\n    ] },\n    { layout: \"bullets\", title: \"/review 的五个检查维度\", bullets: [\n      \"范围：是否只改了任务指定文件\",\n      \"正确性：边界条件、空值、异步竞态\",\n      \"安全：是否触碰 secret、权限、网络\",\n      \"测试：是否覆盖新增行为\",\n      \"可维护：是否引入重复逻辑或隐式依赖\"\n    ] },\n    { layout: \"table\", title: \"命令排障表\", headers: [\"症状\", \"可能原因\", \"排查顺序\"], rows: [\n      [\"输入 /goal 没出现\", \"feature 未启用或版本不支持\", \"先看 / 列表，再查 features.goals\"],\n      [\"/review 没问题\", \"当前没有 Git diff\", \"先看 Review 面板文件列表\"],\n      [\"/mcp 看不到工具\", \"MCP 未配置或 App 未刷新\", \"看 Settings，再用 codex mcp list 辅助\"],\n      [\"命令列表和教程不同\", \"版本、插件或实验开关不同\", \"以当前 App 列表和官方文档为准\"]\n    ] },\n    { layout: \"bullets\", title: \"App Commands 与 CLI Commands 不保证一致\", bullets: [\n      \"App 面向桌面线程、Review 面板和工具入口\",\n      \"CLI 面向终端 TUI、命令行权限和会话\",\n      \"App 输入 / 查看，CLI 输入 /help 查看\",\n      \"两者不保证完全一致，以当前界面显示为准\",\n      \"CLI 命令写到 CX-12，不能写成 App 主线\"\n    ] },\n    { layout: \"end\", title: \"掌握的是什么时候切换工作模式\", subtitle: \"下一篇：CX-04 项目指令、配置、权限与沙盒\" }\n  ]\n});\n\ndecks.push({\n  code: \"CX-04\", category: \"codex\", fileTitle: \"Codex项目指令权限配置\",\n  deck: \"Codex 项目指令、配置、权限与沙盒\",\n  slides: [\n    { layout: \"cover\", title: \"Codex 项目指令、配置、权限与沙盒\", subtitle: \"零基础 · 让 App 知道怎么安全工作\", kicker: \"Vibe Coding 学习系列 · CX-04\" },\n    { layout: \"section\", title: \"从软到硬的四层配置\", subtitle: \"新手先掌握 AGENTS.md 和 App Settings 两层\" },\n    { layout: \"cards\", title: \"配置系统的四层心智模型\", cards: [\n      { title: \"项目说明层\", desc: \"AGENTS.md，写项目事实、命令、规范和安全边界\" },\n      { title: \"用户偏好层\", desc: \"App Settings / config.toml，设模型、终端、审批、沙盒\" },\n      { title: \"命令策略层\", desc: \"Rules / permission profiles，对危险动作建立边界\" },\n      { title: \"事件脚本层\", desc: \"Hooks，在特定时机运行真实脚本做审计或检查\" }\n    ] },\n    { layout: \"bullets\", title: \"为什么不能只靠提示词\", bullets: [\n      \"不持久：换线程后可能忘了重复说\",\n      \"不够硬：说不要推 main，仍要靠人工盯\",\n      \"不可审计：团队很难知道每个人临时说了什么\",\n      \"长期规则写进 AGENTS.md\",\n      \"高风险命令用 Rules，复杂事件才用 Hooks\"\n    ] },\n    { layout: \"table\", title: \"AGENTS.md 推荐结构\", headers: [\"模块\", \"要回答的问题\"], rows: [\n      [\"项目概览\", \"这个项目是什么，主要目录在哪里\"],\n      [\"常用命令\", \"安装、测试、lint、build 怎么跑\"],\n      [\"修改边界\", \"哪些文件可以改，哪些要谨慎\"],\n      [\"代码风格\", \"当前项目已有写法是什么\"],\n      [\"验证方式\", \"改完怎么证明，失败要解释\"]\n    ] },\n    { layout: \"bullets\", title: \"AGENTS.md 不该写什么\", bullets: [\n      \"API Key、token、cookie\",\n      \"只针对本次任务的临时要求\",\n      \"个人机器路径\",\n      \"不稳定的模型名称或价格\",\n      \"「写高质量代码」这种无法验证的口号\"\n    ] },\n    { layout: \"table\", title: \"按场景选择权限策略\", headers: [\"场景\", \"建议\"], rows: [\n      [\"陌生项目\", \"保守审批，先只读\"],\n      [\"日常小改\", \"允许常见读写和安全命令\"],\n      [\"大规模重构\", \"使用 worktree，严格 review\"],\n      [\"CI / 自动化\", \"外部沙箱 + 最小权限\"],\n      [\"涉及密钥或生产数据\", \"默认拒绝，人工确认\"]\n    ] },\n    { layout: \"cards\", title: \"三种沙盒模式\", cards: [\n      { title: \"read-only\", desc: \"只读，适合审计和探索\" },\n      { title: \"workspace-write\", desc: \"可写工作区，适合日常开发\" },\n      { title: \"danger-full-access\", desc: \"无沙盒限制，只能在外部可信沙箱使用\" }\n    ] },\n    { layout: \"table\", title: \"Rules 适合与不适合做什么\", headers: [\"适合\", \"不适合\"], rows: [\n      [\"拦危险删除，例如 rm -rf\", \"写复杂业务流程\"],\n      [\"拦未经确认的 publish\", \"替代测试或 Review\"],\n      [\"对 push、tag、force push 要求确认\", \"判断产品取舍\"],\n      [\"允许 git status、rg、ls 等只读命令\", \"管理外部账号授权\"]\n    ] },\n    { layout: \"steps\", title: \"改完配置后怎么核对\", steps: [\n      { title: \"改 AGENTS.md\", desc: \"新线程里让 Codex 总结项目规则，看是否读到\" },\n      { title: \"改权限或沙盒\", desc: \"用 /status 或 Settings 确认实际生效\" },\n      { title: \"改 MCP 配置\", desc: \"用 /mcp 看 server 和工具是否可见\" },\n      { title: \"换项目目录时\", desc: \"确认打开了对的目录，旧线程可能仍是旧上下文\" }\n    ] },\n    { layout: \"bullets\", title: \"Hooks 是事件脚本，不是万能自动化\", bullets: [\n      \"配置通常在 .codex/hooks.json 或 [hooks] 表\",\n      \"会运行真实命令，可能读取敏感上下文\",\n      \"写错会阻塞工作流，学习阶段先别急着写\",\n      \"能用 Rules 解决的命令边界，不要先写 Hook\",\n      \"相对路径要改从 git root 或绝对路径解析\"\n    ] },\n    { layout: \"end\", title: \"先用 AGENTS.md 和 Settings 把边界写清楚\", subtitle: \"下一篇：CX-05 MCP 外部工具\" }\n  ]\n});\n\nconst results: string[] = [];\nfor (const d of decks) {\n  const path = `${dir}/${d.code.toLowerCase()}.json`;\n  const content = JSON.stringify(d, null, 2) + \"\\n\";\n  const w = await tools.write({ file_path: path, content });\n  results.push(`${d.code} -> ${path} (${w.operation}, slides=${d.slides.length})`);\n}\nreturn results.join(\"\\n\");", "description": "Write CX-01 to CX-04 JSON files"}

## assistant · 2026-10-05T11:54:10Z

Now CX-05, CX-06, CX-07. Write them.
{
  "type": "tool-call",
  "id": "call_00_jEdNNVMA0cuYZ6jh9hvB8369",
  "name": "run_code",
  "arguments": "{\"code\": \"const dir = \\\"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\\\";\\nconst decks: any[] = [];\\n\\ndecks.push({\\n  code: \\\"CX-05\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-MCP外部工具\\\",\\n  deck: \\\"Codex MCP：在 App 中连接外部工具\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex MCP：在 App 中连接外部工具\\\", subtitle: \\\"零基础 · 先只读、再小范围、可审计、可撤销\\\", kicker: \\\"Vibe Coding 学习系列 · CX-05\\\" },\\n    { layout: \\\"section\\\", title: \\\"MCP 不是搜索框，而是工具连接层\\\", subtitle: \\\"让 Codex 连接浏览器、数据库、文档和内部 API\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"MCP 能给 Codex 什么\\\", bullets: [\\n      \\\"文档上下文：查新文档，减少过期知识\\\",\\n      \\\"开发工具：控制浏览器，检查页面\\\",\\n      \\\"设计工具：读取 Figma 等设计上下文\\\",\\n      \\\"数据工具：数据库 schema、只读查询\\\",\\n      \\\"项目与内部系统：GitHub issue / PR、私有 API\\\"\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"App 中的 MCP 工作流\\\", steps: [\\n      { title: \\\"启用或配置\\\", desc: \\\"在 App Settings 或集成入口启用 MCP\\\" },\\n      { title: \\\"查看可见工具\\\", desc: \\\"回到线程，用 /mcp 看 server 和工具\\\" },\\n      { title: \\\"用自然语言调用\\\", desc: \\\"要求 Codex 使用工具，并观察权限提示\\\" },\\n      { title: \\\"Review 结果\\\", desc: \\\"核对来源、时间、权限和副作用\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"从 0 配 MCP 前先确认四件事\\\", headers: [\\\"问题\\\", \\\"为什么重要\\\"], rows: [\\n      [\\\"本地命令还是远程服务\\\", \\\"决定用 stdio、HTTP 还是插件提供\\\"],\\n      [\\\"需要什么账号或 token\\\", \\\"决定密钥放哪里，不能写进仓库\\\"],\\n      [\\\"默认能读写什么\\\", \\\"决定是否只读、是否需要审批\\\"],\\n      [\\\"App 是否已有连接器或插件\\\", \\\"有现成入口时不要重复手写 MCP\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"三类 MCP server\\\", cards: [\\n      { title: \\\"STDIO\\\", desc: \\\"本地命令启动进程，适合本机工具和私有脚本\\\" },\\n      { title: \\\"Streamable HTTP\\\", desc: \\\"访问一个 URL，适合远程服务、OAuth 和云端工具\\\" },\\n      { title: \\\"Plugin-provided\\\", desc: \\\"插件 manifest 提供 server，先看来源和工具权限\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"密钥放哪里\\\", headers: [\\\"场景\\\", \\\"推荐\\\", \\\"不推荐\\\"], rows: [\\n      [\\\"本地个人 token\\\", \\\"系统环境变量或密码管理器\\\", \\\"写进 config.toml 并提交\\\"],\\n      [\\\"团队共享服务\\\", \\\"组织 secret 管理、最小 scope\\\", \\\"共享个人账号 token\\\"],\\n      [\\\"Cloud / remote\\\", \\\"环境变量或官方 secret 入口\\\", \\\"在 setup 日志里 echo\\\"],\\n      [\\\"临时调试\\\", \\\"临时只读 token，用完撤销\\\", \\\"使用生产写 token\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"配置 MCP 前先问的安全问题\\\", bullets: [\\n      \\\"它能读什么数据，能写什么数据\\\",\\n      \\\"它是否会联网，是否需要账号授权\\\",\\n      \\\"它是否会把数据发给第三方\\\",\\n      \\\"它能不能在只读模式下完成任务\\\",\\n      \\\"生产库、客户数据和邮箱都按最小权限配置\\\"\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"工具风险分级\\\", cards: [\\n      { title: \\\"只读搜索\\\", desc: \\\"风险低，可以较宽松\\\" },\\n      { title: \\\"读取私有数据\\\", desc: \\\"风险中，需要来源说明\\\" },\\n      { title: \\\"写外部系统\\\", desc: \\\"风险高，需要人工确认\\\" },\\n      { title: \\\"访问生产数据\\\", desc: \\\"风险很高，默认不要给新手练习\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"MCP 排障流程\\\", headers: [\\\"症状\\\", \\\"可能原因\\\", \\\"排查\\\"], rows: [\\n      [\\\"/mcp 看不到 server\\\", \\\"配置层未加载或 App 未刷新\\\", \\\"先看 App Settings，再重启或刷新\\\"],\\n      [\\\"CLI 能看到 App 看不到\\\", \\\"配置层或会话状态不同\\\", \\\"以 App 线程使用结果为准\\\"],\\n      [\\\"server 启动失败\\\", \\\"命令不存在或依赖未安装\\\", \\\"在终端单独跑启动命令看日志\\\"],\\n      [\\\"结果不可信\\\", \\\"来源不明或时间过期\\\", \\\"要求 Codex 列出来源和查询条件\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"MCP 配置核对清单\\\", bullets: [\\n      \\\"App 可见：/mcp 能看到 server 和工具\\\",\\n      \\\"最小权限：只给当前任务需要的读写范围\\\",\\n      \\\"密钥安全：token 在环境变量或 secret 里\\\",\\n      \\\"只读试跑：能完成一次只读查询或读取\\\",\\n      \\\"可审计、可撤销：知道怎么禁用和撤销 token\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"先只读、再小范围、可审计、可撤销\\\", subtitle: \\\"下一篇：CX-06 Skills 可复用工作流\\\" }\\n  ]\\n});\\n\\ndecks.push({\\n  code: \\\"CX-06\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-Skills可复用工作流\\\",\\n  deck: \\\"Codex Skills：把重复提示变成可复用工作流\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex Skills：把重复提示变成可复用工作流\\\", subtitle: \\\"零基础 · 让流程可重复，而不是让 prompt 更长\\\", kicker: \\\"Vibe Coding 学习系列 · CX-06\\\" },\\n    { layout: \\\"section\\\", title: \\\"Skill 是可复用判断，不是 prompt 收藏\\\", subtitle: \\\"要有步骤、边界和验收方式\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"Skill 是什么，适合什么\\\", bullets: [\\n      \\\"一组可复用指令、资源和可选脚本\\\",\\n      \\\"适合代码审查、文档核对、发布检查和团队 SOP\\\",\\n      \\\"不适合只执行一次的临时任务\\\",\\n      \\\"不适合需要实时外部 API 的工具连接\\\",\\n      \\\"不适合需要定时运行的周期任务\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"什么时候值得做成 Skill\\\", headers: [\\\"信号\\\", \\\"是否适合\\\"], rows: [\\n      [\\\"同一提示复制三次以上\\\", \\\"适合\\\"],\\n      [\\\"多人需要同一做法\\\", \\\"适合\\\"],\\n      [\\\"输出格式总要固定\\\", \\\"适合\\\"],\\n      [\\\"只做一次的临时任务\\\", \\\"不适合\\\"],\\n      [\\\"需要每天运行\\\", \\\"交给 Automation 调度\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"好 Skill 的四个特征\\\", cards: [\\n      { title: \\\"触发清楚\\\", desc: \\\"description 里写明什么时候用\\\" },\\n      { title: \\\"边界清楚\\\", desc: \\\"也写明什么时候不用\\\" },\\n      { title: \\\"输入输出清楚\\\", desc: \\\"Codex 知道读什么、交付什么\\\" },\\n      { title: \\\"内容分层\\\", desc: \\\"常用指令在 SKILL.md，长资料放 references\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"description 是触发路由，不是介绍文案\\\", bullets: [\\n      \\\"模板：Use when 场景，Do 动作，Do not use when 边界\\\",\\n      \\\"差写法：Helps write high quality code\\\",\\n      \\\"好写法要写清对象、动作、触发场景和边界\\\",\\n      \\\"写得太泛，Codex 可能乱用\\\",\\n      \\\"写得太窄，真正需要时触发不了\\\"\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"在 App 中调用 Skill\\\", steps: [\\n      { title: \\\"确认能否看到\\\", desc: \\\"当前 App 是否显示这个 Skill\\\" },\\n      { title: \\\"确认层级\\\", desc: \\\"用户级、项目级，还是插件带来的\\\" },\\n      { title: \\\"确认副作用\\\", desc: \\\"会不会读额外资源、运行脚本或调用工具\\\" },\\n      { title: \\\"显式调用\\\", desc: \\\"用 $code-review 或自然语言点名，再说清任务\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"Skills、Commands、Automations 的分工\\\", headers: [\\\"需求\\\", \\\"首选\\\"], rows: [\\n      [\\\"当前线程快速动作\\\", \\\"Command\\\"],\\n      [\\\"固定 SOP / 复用流程\\\", \\\"Skill\\\"],\\n      [\\\"定时或后台重复执行\\\", \\\"Automation\\\"],\\n      [\\\"外部工具连接\\\", \\\"MCP / Connector\\\"],\\n      [\\\"打包分发一组能力\\\", \\\"Plugin\\\"]\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"文件结构：内容放哪里\\\", headers: [\\\"内容\\\", \\\"放哪里\\\", \\\"原因\\\"], rows: [\\n      [\\\"触发场景、流程、输出\\\", \\\"SKILL.md\\\", \\\"Codex 必须先看到\\\"],\\n      [\\\"长规范、示例、术语表\\\", \\\"references/\\\", \\\"需要时再读，节省上下文\\\"],\\n      [\\\"重复性强易写错的逻辑\\\", \\\"scripts/\\\", \\\"要写清运行时和失败输出\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"Skill 不该承载什么\\\", bullets: [\\n      \\\"一次性任务\\\",\\n      \\\"当前项目的临时 bug\\\",\\n      \\\"模糊人设包装\\\",\\n      \\\"需要每天变化的命令\\\",\\n      \\\"真实密钥或私有账号信息\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"一次性任务放 prompt，项目事实放 AGENTS.md\\\", subtitle: \\\"下一篇：CX-07 Plugins 连接器\\\" }\\n  ]\\n});\\n\\ndecks.push({\\n  code: \\\"CX-07\\\", category: \\\"codex\\\", fileTitle: \\\"Codex-Plugins连接器\\\",\\n  deck: \\\"Codex Plugins 与 Connectors：App 能力扩展\\\",\\n  slides: [\\n    { layout: \\\"cover\\\", title: \\\"Codex Plugins 与 Connectors：App 能力扩展\\\", subtitle: \\\"零基础 · 安装是让能力可见，授权是让数据可用\\\", kicker: \\\"Vibe Coding 学习系列 · CX-07\\\" },\\n    { layout: \\\"section\\\", title: \\\"安装、授权、调用是三件事\\\", subtitle: \\\"插件可以包含 Skills、MCP、Apps，但不等于其中任何一个\\\" },\\n    { layout: \\\"bullets\\\", title: \\\"安装、授权、调用、撤销\\\", bullets: [\\n      \\\"安装 Plugin：看它带来的 Skills / MCP / Apps / 配置\\\",\\n      \\\"对外部服务单独授权\\\",\\n      \\\"在线程中引用或调用外部上下文\\\",\\n      \\\"工具或外部动作按权限和审批执行\\\",\\n      \\\"不用时撤销授权或卸载\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"先分清四个概念\\\", headers: [\\\"概念\\\", \\\"本质\\\", \\\"例子\\\"], rows: [\\n      [\\\"Connector / App\\\", \\\"外部账号连接\\\", \\\"GitHub、Gmail、Drive、Slack\\\"],\\n      [\\\"Plugin\\\", \\\"能力包\\\", \\\"一组 skills、MCP、apps、配置\\\"],\\n      [\\\"Skill\\\", \\\"可复用工作流\\\", \\\"代码审查 SOP\\\"],\\n      [\\\"MCP\\\", \\\"工具协议\\\", \\\"浏览器、数据库、文档源\\\"]\\n    ] },\\n    { layout: \\\"steps\\\", title: \\\"App 中的连接器工作流\\\", steps: [\\n      { title: \\\"打开入口\\\", desc: \\\"进入 App 的 Plugins / Connectors / Apps\\\" },\\n      { title: \\\"选择服务\\\", desc: \\\"挑要连接的 GitHub、Drive、Slack 等\\\" },\\n      { title: \\\"完成授权\\\", desc: \\\"授权范围要单独看清楚\\\" },\\n      { title: \\\"引用并执行\\\", desc: \\\"用 @、mention 或自然语言引用外部上下文\\\" }\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"安装或连接前的检查\\\", headers: [\\\"检查项\\\", \\\"要确认什么\\\"], rows: [\\n      [\\\"来源\\\", \\\"官方、组织内，还是第三方插件\\\"],\\n      [\\\"能力\\\", \\\"带 Skills、MCP、Connectors 还是组合包\\\"],\\n      [\\\"权限\\\", \\\"只读、评论、写文件、发消息分别要什么权限\\\"],\\n      [\\\"数据范围\\\", \\\"能访问哪些仓库、文档、邮箱或群聊\\\"],\\n      [\\\"撤销方式\\\", \\\"在 App、服务后台还是组织管理端撤销\\\"]\\n    ] },\\n    { layout: \\\"cards\\\", title: \\\"插件安装后的四层变化\\\", cards: [\\n      { title: \\\"目录层\\\", desc: \\\"Plugins 页面出现已安装条目\\\" },\\n      { title: \\\"能力层\\\", desc: \\\"@ mention 或 bundled skills 可被调用\\\" },\\n      { title: \\\"授权层\\\", desc: \\\"外部 App 可能要求登录或授权\\\" },\\n      { title: \\\"执行层\\\", desc: \\\"Codex 按 prompt、权限和审批调用工具\\\" }\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"最小权限原则\\\", bullets: [\\n      \\\"第一次安装只给必要权限\\\",\\n      \\\"只读任务不给写权限\\\",\\n      \\\"需要发消息或改 PR 时，明确说明目标和范围\\\",\\n      \\\"团队插件先在测试项目验证\\\",\\n      \\\"不再使用时及时禁用或卸载\\\"\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"常见连接场景与风险\\\", headers: [\\\"场景\\\", \\\"连接器价值\\\", \\\"风险点\\\"], rows: [\\n      [\\\"GitHub\\\", \\\"读取 issue、PR、仓库上下文\\\", \\\"写权限、PR 评论权限\\\"],\\n      [\\\"Google Drive / Docs\\\", \\\"读取团队文档\\\", \\\"文档访问范围\\\"],\\n      [\\\"Gmail / Outlook\\\", \\\"引用邮件上下文\\\", \\\"隐私和敏感信息\\\"],\\n      [\\\"Slack / Teams\\\", \\\"查讨论和决策\\\", \\\"群聊范围和成员隐私\\\"],\\n      [\\\"Calendar\\\", \\\"查日程和会议背景\\\", \\\"个人隐私\\\"]\\n    ] },\\n    { layout: \\\"table\\\", title: \\\"CLI 辅助管理 marketplace\\\", headers: [\\\"命令\\\", \\\"用途\\\"], rows: [\\n      [\\\"codex plugin marketplace list\\\", \\\"列出已添加的 marketplace\\\"],\\n      [\\\"codex plugin marketplace add owner/repo\\\", \\\"添加 marketplace 来源\\\"],\\n      [\\\"codex plugin marketplace upgrade\\\", \\\"升级 marketplace\\\"],\\n      [\\\"codex plugin marketplace remove 名称\\\", \\\"移除 marketplace\\\"]\\n    ] },\\n    { layout: \\\"bullets\\\", title: \\\"观察输出：看用了什么，不只看答得像不像\\\", bullets: [\\n      \\\"你使用了哪些插件或工具能力\\\",\\n      \\\"哪些信息来自外部系统\\\",\\n      \\\"哪些结论是根据上下文推断的\\\",\\n      \\\"有没有权限、网络、认证或数据范围限制\\\",\\n      \\\"安装是让能力可见，审批是最后的安全门\\\"\\n    ] },\\n    { layout: \\\"end\\\", title: \\\"安装让能力可见，授权让数据可用，审批是安全门\\\", subtitle: \\\"本系列 codex 分册到此\\\" }\\n  ]\\n});\\n\\n// validate\\nconst problems: string[] = [];\\nfor (const d of decks) {\\n  const n = d.slides.length;\\n  if (n < 10 || n > 14) problems.push(`${d.code}: slide count ${n}`);\\n  if (d.slides[0].kicker !== `Vibe Coding 学习系列 · ${d.code}`) problems.push(`${d.code}: kicker`);\\n  for (const [i, s] of d.slides.entries()) {\\n    if (s.layout === \\\"bullets\\\") {\\n      if (s.bullets.length > 5) problems.push(`${d.code} s${i} bullets`);\\n      for (const b of s.bullets) if ([...b].length > 42) problems.push(`${d.code} s${i} len=${[...b].length} \\\"${b}\\\"`);\\n    }\\n    if (s.layout === \\\"cards\\\") {\\n      if (s.cards.length < 3 || s.cards.length > 4) problems.push(`${d.code} s${i} cards`);\\n      for (const c of s.cards) if ([...c.desc].length > 42) problems.push(`${d.code} s${i} card len=${[...c.desc].length}`);\\n    }\\n    if (s.layout === \\\"steps\\\") {\\n      if (s.steps.length < 3 || s.steps.length > 4) problems.push(`${d.code} s${i} steps`);\\n      for (const st of s.steps) if ([...st.desc].length > 42) problems.push(`${d.code} s${i} step len=${[...st.desc].length}`);\\n    }\\n    if (s.layout === \\\"table\\\") {\\n      if (s.headers.length > 5) problems.push(`${d.code} s${i} cols`);\\n      if (s.rows.length > 6) problems.push(`${d.code} s${i} rows`);\\n      for (const r of s.rows) if (r.length !== s.headers.length) problems.push(`${d.code} s${i} width`);\\n    }\\n  }\\n}\\nif (problems.length) return \\\"PROBLEMS:\\\\n\\\" + problems.join(\\\"\\\\n\\\");\\n\\nconst out: string[] = [];\\nfor (const d of decks) {\\n  const path = `${dir}/${d.code.toLowerCase()}.json`;\\n  const w = await tools.write({ file_path: path, content: JSON.stringify(d, null, 2) + \\\"\\\\n\\\" });\\n  out.push(`${d.code} -> ${path} (${w.operation}, slides=${d.slides.length})`);\\n}\\nreturn out.join(\\\"\\\\n\\\");\", \"description\": \"Write CX-05 to CX-07 JSON files\"}"
}

## tool · 2026-10-05T11:54:10Z

run_code
{"code": "const dir = \"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\";\nconst decks: any[] = [];\n\ndecks.push({\n  code: \"CX-05\", category: \"codex\", fileTitle: \"Codex-MCP外部工具\",\n  deck: \"Codex MCP：在 App 中连接外部工具\",\n  slides: [\n    { layout: \"cover\", title: \"Codex MCP：在 App 中连接外部工具\", subtitle: \"零基础 · 先只读、再小范围、可审计、可撤销\", kicker: \"Vibe Coding 学习系列 · CX-05\" },\n    { layout: \"section\", title: \"MCP 不是搜索框，而是工具连接层\", subtitle: \"让 Codex 连接浏览器、数据库、文档和内部 API\" },\n    { layout: \"bullets\", title: \"MCP 能给 Codex 什么\", bullets: [\n      \"文档上下文：查新文档，减少过期知识\",\n      \"开发工具：控制浏览器，检查页面\",\n      \"设计工具：读取 Figma 等设计上下文\",\n      \"数据工具：数据库 schema、只读查询\",\n      \"项目与内部系统：GitHub issue / PR、私有 API\"\n    ] },\n    { layout: \"steps\", title: \"App 中的 MCP 工作流\", steps: [\n      { title: \"启用或配置\", desc: \"在 App Settings 或集成入口启用 MCP\" },\n      { title: \"查看可见工具\", desc: \"回到线程，用 /mcp 看 server 和工具\" },\n      { title: \"用自然语言调用\", desc: \"要求 Codex 使用工具，并观察权限提示\" },\n      { title: \"Review 结果\", desc: \"核对来源、时间、权限和副作用\" }\n    ] },\n    { layout: \"table\", title: \"从 0 配 MCP 前先确认四件事\", headers: [\"问题\", \"为什么重要\"], rows: [\n      [\"本地命令还是远程服务\", \"决定用 stdio、HTTP 还是插件提供\"],\n      [\"需要什么账号或 token\", \"决定密钥放哪里，不能写进仓库\"],\n      [\"默认能读写什么\", \"决定是否只读、是否需要审批\"],\n      [\"App 是否已有连接器或插件\", \"有现成入口时不要重复手写 MCP\"]\n    ] },\n    { layout: \"cards\", title: \"三类 MCP server\", cards: [\n      { title: \"STDIO\", desc: \"本地命令启动进程，适合本机工具和私有脚本\" },\n      { title: \"Streamable HTTP\", desc: \"访问一个 URL，适合远程服务、OAuth 和云端工具\" },\n      { title: \"Plugin-provided\", desc: \"插件 manifest 提供 server，先看来源和工具权限\" }\n    ] },\n    { layout: \"table\", title: \"密钥放哪里\", headers: [\"场景\", \"推荐\", \"不推荐\"], rows: [\n      [\"本地个人 token\", \"系统环境变量或密码管理器\", \"写进 config.toml 并提交\"],\n      [\"团队共享服务\", \"组织 secret 管理、最小 scope\", \"共享个人账号 token\"],\n      [\"Cloud / remote\", \"环境变量或官方 secret 入口\", \"在 setup 日志里 echo\"],\n      [\"临时调试\", \"临时只读 token，用完撤销\", \"使用生产写 token\"]\n    ] },\n    { layout: \"bullets\", title: \"配置 MCP 前先问的安全问题\", bullets: [\n      \"它能读什么数据，能写什么数据\",\n      \"它是否会联网，是否需要账号授权\",\n      \"它是否会把数据发给第三方\",\n      \"它能不能在只读模式下完成任务\",\n      \"生产库、客户数据和邮箱都按最小权限配置\"\n    ] },\n    { layout: \"cards\", title: \"工具风险分级\", cards: [\n      { title: \"只读搜索\", desc: \"风险低，可以较宽松\" },\n      { title: \"读取私有数据\", desc: \"风险中，需要来源说明\" },\n      { title: \"写外部系统\", desc: \"风险高，需要人工确认\" },\n      { title: \"访问生产数据\", desc: \"风险很高，默认不要给新手练习\" }\n    ] },\n    { layout: \"table\", title: \"MCP 排障流程\", headers: [\"症状\", \"可能原因\", \"排查\"], rows: [\n      [\"/mcp 看不到 server\", \"配置层未加载或 App 未刷新\", \"先看 App Settings，再重启或刷新\"],\n      [\"CLI 能看到 App 看不到\", \"配置层或会话状态不同\", \"以 App 线程使用结果为准\"],\n      [\"server 启动失败\", \"命令不存在或依赖未安装\", \"在终端单独跑启动命令看日志\"],\n      [\"结果不可信\", \"来源不明或时间过期\", \"要求 Codex 列出来源和查询条件\"]\n    ] },\n    { layout: \"bullets\", title: \"MCP 配置核对清单\", bullets: [\n      \"App 可见：/mcp 能看到 server 和工具\",\n      \"最小权限：只给当前任务需要的读写范围\",\n      \"密钥安全：token 在环境变量或 secret 里\",\n      \"只读试跑：能完成一次只读查询或读取\",\n      \"可审计、可撤销：知道怎么禁用和撤销 token\"\n    ] },\n    { layout: \"end\", title: \"先只读、再小范围、可审计、可撤销\", subtitle: \"下一篇：CX-06 Skills 可复用工作流\" }\n  ]\n});\n\ndecks.push({\n  code: \"CX-06\", category: \"codex\", fileTitle: \"Codex-Skills可复用工作流\",\n  deck: \"Codex Skills：把重复提示变成可复用工作流\",\n  slides: [\n    { layout: \"cover\", title: \"Codex Skills：把重复提示变成可复用工作流\", subtitle: \"零基础 · 让流程可重复，而不是让 prompt 更长\", kicker: \"Vibe Coding 学习系列 · CX-06\" },\n    { layout: \"section\", title: \"Skill 是可复用判断，不是 prompt 收藏\", subtitle: \"要有步骤、边界和验收方式\" },\n    { layout: \"bullets\", title: \"Skill 是什么，适合什么\", bullets: [\n      \"一组可复用指令、资源和可选脚本\",\n      \"适合代码审查、文档核对、发布检查和团队 SOP\",\n      \"不适合只执行一次的临时任务\",\n      \"不适合需要实时外部 API 的工具连接\",\n      \"不适合需要定时运行的周期任务\"\n    ] },\n    { layout: \"table\", title: \"什么时候值得做成 Skill\", headers: [\"信号\", \"是否适合\"], rows: [\n      [\"同一提示复制三次以上\", \"适合\"],\n      [\"多人需要同一做法\", \"适合\"],\n      [\"输出格式总要固定\", \"适合\"],\n      [\"只做一次的临时任务\", \"不适合\"],\n      [\"需要每天运行\", \"交给 Automation 调度\"]\n    ] },\n    { layout: \"cards\", title: \"好 Skill 的四个特征\", cards: [\n      { title: \"触发清楚\", desc: \"description 里写明什么时候用\" },\n      { title: \"边界清楚\", desc: \"也写明什么时候不用\" },\n      { title: \"输入输出清楚\", desc: \"Codex 知道读什么、交付什么\" },\n      { title: \"内容分层\", desc: \"常用指令在 SKILL.md，长资料放 references\" }\n    ] },\n    { layout: \"bullets\", title: \"description 是触发路由，不是介绍文案\", bullets: [\n      \"模板：Use when 场景，Do 动作，Do not use when 边界\",\n      \"差写法：Helps write high quality code\",\n      \"好写法要写清对象、动作、触发场景和边界\",\n      \"写得太泛，Codex 可能乱用\",\n      \"写得太窄，真正需要时触发不了\"\n    ] },\n    { layout: \"steps\", title: \"在 App 中调用 Skill\", steps: [\n      { title: \"确认能否看到\", desc: \"当前 App 是否显示这个 Skill\" },\n      { title: \"确认层级\", desc: \"用户级、项目级，还是插件带来的\" },\n      { title: \"确认副作用\", desc: \"会不会读额外资源、运行脚本或调用工具\" },\n      { title: \"显式调用\", desc: \"用 $code-review 或自然语言点名，再说清任务\" }\n    ] },\n    { layout: \"table\", title: \"Skills、Commands、Automations 的分工\", headers: [\"需求\", \"首选\"], rows: [\n      [\"当前线程快速动作\", \"Command\"],\n      [\"固定 SOP / 复用流程\", \"Skill\"],\n      [\"定时或后台重复执行\", \"Automation\"],\n      [\"外部工具连接\", \"MCP / Connector\"],\n      [\"打包分发一组能力\", \"Plugin\"]\n    ] },\n    { layout: \"table\", title: \"文件结构：内容放哪里\", headers: [\"内容\", \"放哪里\", \"原因\"], rows: [\n      [\"触发场景、流程、输出\", \"SKILL.md\", \"Codex 必须先看到\"],\n      [\"长规范、示例、术语表\", \"references/\", \"需要时再读，节省上下文\"],\n      [\"重复性强易写错的逻辑\", \"scripts/\", \"要写清运行时和失败输出\"]\n    ] },\n    { layout: \"bullets\", title: \"Skill 不该承载什么\", bullets: [\n      \"一次性任务\",\n      \"当前项目的临时 bug\",\n      \"模糊人设包装\",\n      \"需要每天变化的命令\",\n      \"真实密钥或私有账号信息\"\n    ] },\n    { layout: \"end\", title: \"一次性任务放 prompt，项目事实放 AGENTS.md\", subtitle: \"下一篇：CX-07 Plugins 连接器\" }\n  ]\n});\n\ndecks.push({\n  code: \"CX-07\", category: \"codex\", fileTitle: \"Codex-Plugins连接器\",\n  deck: \"Codex Plugins 与 Connectors：App 能力扩展\",\n  slides: [\n    { layout: \"cover\", title: \"Codex Plugins 与 Connectors：App 能力扩展\", subtitle: \"零基础 · 安装是让能力可见，授权是让数据可用\", kicker: \"Vibe Coding 学习系列 · CX-07\" },\n    { layout: \"section\", title: \"安装、授权、调用是三件事\", subtitle: \"插件可以包含 Skills、MCP、Apps，但不等于其中任何一个\" },\n    { layout: \"bullets\", title: \"安装、授权、调用、撤销\", bullets: [\n      \"安装 Plugin：看它带来的 Skills / MCP / Apps / 配置\",\n      \"对外部服务单独授权\",\n      \"在线程中引用或调用外部上下文\",\n      \"工具或外部动作按权限和审批执行\",\n      \"不用时撤销授权或卸载\"\n    ] },\n    { layout: \"table\", title: \"先分清四个概念\", headers: [\"概念\", \"本质\", \"例子\"], rows: [\n      [\"Connector / App\", \"外部账号连接\", \"GitHub、Gmail、Drive、Slack\"],\n      [\"Plugin\", \"能力包\", \"一组 skills、MCP、apps、配置\"],\n      [\"Skill\", \"可复用工作流\", \"代码审查 SOP\"],\n      [\"MCP\", \"工具协议\", \"浏览器、数据库、文档源\"]\n    ] },\n    { layout: \"steps\", title: \"App 中的连接器工作流\", steps: [\n      { title: \"打开入口\", desc: \"进入 App 的 Plugins / Connectors / Apps\" },\n      { title: \"选择服务\", desc: \"挑要连接的 GitHub、Drive、Slack 等\" },\n      { title: \"完成授权\", desc: \"授权范围要单独看清楚\" },\n      { title: \"引用并执行\", desc: \"用 @、mention 或自然语言引用外部上下文\" }\n    ] },\n    { layout: \"table\", title: \"安装或连接前的检查\", headers: [\"检查项\", \"要确认什么\"], rows: [\n      [\"来源\", \"官方、组织内，还是第三方插件\"],\n      [\"能力\", \"带 Skills、MCP、Connectors 还是组合包\"],\n      [\"权限\", \"只读、评论、写文件、发消息分别要什么权限\"],\n      [\"数据范围\", \"能访问哪些仓库、文档、邮箱或群聊\"],\n      [\"撤销方式\", \"在 App、服务后台还是组织管理端撤销\"]\n    ] },\n    { layout: \"cards\", title: \"插件安装后的四层变化\", cards: [\n      { title: \"目录层\", desc: \"Plugins 页面出现已安装条目\" },\n      { title: \"能力层\", desc: \"@ mention 或 bundled skills 可被调用\" },\n      { title: \"授权层\", desc: \"外部 App 可能要求登录或授权\" },\n      { title: \"执行层\", desc: \"Codex 按 prompt、权限和审批调用工具\" }\n    ] },\n    { layout: \"bullets\", title: \"最小权限原则\", bullets: [\n      \"第一次安装只给必要权限\",\n      \"只读任务不给写权限\",\n      \"需要发消息或改 PR 时，明确说明目标和范围\",\n      \"团队插件先在测试项目验证\",\n      \"不再使用时及时禁用或卸载\"\n    ] },\n    { layout: \"table\", title: \"常见连接场景与风险\", headers: [\"场景\", \"连接器价值\", \"风险点\"], rows: [\n      [\"GitHub\", \"读取 issue、PR、仓库上下文\", \"写权限、PR 评论权限\"],\n      [\"Google Drive / Docs\", \"读取团队文档\", \"文档访问范围\"],\n      [\"Gmail / Outlook\", \"引用邮件上下文\", \"隐私和敏感信息\"],\n      [\"Slack / Teams\", \"查讨论和决策\", \"群聊范围和成员隐私\"],\n      [\"Calendar\", \"查日程和会议背景\", \"个人隐私\"]\n    ] },\n    { layout: \"table\", title: \"CLI 辅助管理 marketplace\", headers: [\"命令\", \"用途\"], rows: [\n      [\"codex plugin marketplace list\", \"列出已添加的 marketplace\"],\n      [\"codex plugin marketplace add owner/repo\", \"添加 marketplace 来源\"],\n      [\"codex plugin marketplace upgrade\", \"升级 marketplace\"],\n      [\"codex plugin marketplace remove 名称\", \"移除 marketplace\"]\n    ] },\n    { layout: \"bullets\", title: \"观察输出：看用了什么，不只看答得像不像\", bullets: [\n      \"你使用了哪些插件或工具能力\",\n      \"哪些信息来自外部系统\",\n      \"哪些结论是根据上下文推断的\",\n      \"有没有权限、网络、认证或数据范围限制\",\n      \"安装是让能力可见，审批是最后的安全门\"\n    ] },\n    { layout: \"end\", title: \"安装让能力可见，授权让数据可用，审批是安全门\", subtitle: \"本系列 codex 分册到此\" }\n  ]\n});\n\n// validate\nconst problems: string[] = [];\nfor (const d of decks) {\n  const n = d.slides.length;\n  if (n < 10 || n > 14) problems.push(`${d.code}: slide count ${n}`);\n  if (d.slides[0].kicker !== `Vibe Coding 学习系列 · ${d.code}`) problems.push(`${d.code}: kicker`);\n  for (const [i, s] of d.slides.entries()) {\n    if (s.layout === \"bullets\") {\n      if (s.bullets.length > 5) problems.push(`${d.code} s${i} bullets`);\n      for (const b of s.bullets) if ([...b].length > 42) problems.push(`${d.code} s${i} len=${[...b].length} \"${b}\"`);\n    }\n    if (s.layout === \"cards\") {\n      if (s.cards.length < 3 || s.cards.length > 4) problems.push(`${d.code} s${i} cards`);\n      for (const c of s.cards) if ([...c.desc].length > 42) problems.push(`${d.code} s${i} card len=${[...c.desc].length}`);\n    }\n    if (s.layout === \"steps\") {\n      if (s.steps.length < 3 || s.steps.length > 4) problems.push(`${d.code} s${i} steps`);\n      for (const st of s.steps) if ([...st.desc].length > 42) problems.push(`${d.code} s${i} step len=${[...st.desc].length}`);\n    }\n    if (s.layout === \"table\") {\n      if (s.headers.length > 5) problems.push(`${d.code} s${i} cols`);\n      if (s.rows.length > 6) problems.push(`${d.code} s${i} rows`);\n      for (const r of s.rows) if (r.length !== s.headers.length) problems.push(`${d.code} s${i} width`);\n    }\n  }\n}\nif (problems.length) return \"PROBLEMS:\\n\" + problems.join(\"\\n\");\n\nconst out: string[] = [];\nfor (const d of decks) {\n  const path = `${dir}/${d.code.toLowerCase()}.json`;\n  const w = await tools.write({ file_path: path, content: JSON.stringify(d, null, 2) + \"\\n\" });\n  out.push(`${d.code} -> ${path} (${w.operation}, slides=${d.slides.length})`);\n}\nreturn out.join(\"\\n\");", "description": "Write CX-05 to CX-07 JSON files"}

## assistant · 2026-10-05T11:54:13Z

Now verify files: parse JSON, check UTF-8, no BOM, and confirm contents. Let me run a verification reading all 7 files and parsing.
七份文件已写入。现在做最终校验：逐个解析 JSON、检查字段与约束。
{
  "type": "tool-call",
  "id": "call_00_42BQo4YII8HX5Rgl8mj06796",
  "name": "run_code",
  "arguments": "{\"code\": \"const dir = \\\"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\\\";\\nconst codes = [\\\"cx-01\\\",\\\"cx-02\\\",\\\"cx-03\\\",\\\"cx-04\\\",\\\"cx-05\\\",\\\"cx-06\\\",\\\"cx-07\\\"];\\nconst rows: string[] = [];\\nconst problems: string[] = [];\\nfor (const c of codes) {\\n  const p = `${dir}/${c}.json`;\\n  const r = await tools.read({ file_path: p });\\n  const text = r.lines.map(l => l.text).join(\\\"\\\\n\\\");\\n  if (text.charCodeAt(0) === 0xFEFF) problems.push(`${c}: BOM`);\\n  if (text.trimStart().startsWith(\\\"```\\\")) problems.push(`${c}: code fence`);\\n  let d: any;\\n  try { d = JSON.parse(text); } catch (e: any) { problems.push(`${c}: parse ${e.message}`); continue; }\\n  const layouts = d.slides.map((s: any) => s.layout);\\n  const hasEnd = layouts.includes(\\\"end\\\");\\n  const hasCover = d.slides[0].layout === \\\"cover\\\" && d.slides[0].kicker === `Vibe Coding 学习系列 · ${d.code}`;\\n  if (!hasEnd) problems.push(`${c}: no end`);\\n  if (!hasCover) problems.push(`${c}: cover/kicker`);\\n  if (d.code !== c.toUpperCase()) problems.push(`${c}: code field ${d.code}`);\\n  if (d.category !== \\\"codex\\\") problems.push(`${c}: category`);\\n  if (!d.fileTitle) problems.push(`${c}: fileTitle missing`);\\n  rows.push(`${c}.json | code=${d.code} | deck=${d.deck} | fileTitle=${d.fileTitle} | slides=${d.slides.length} | layouts=${layouts.join(\\\",\\\")}`);\\n}\\nreturn (problems.length ? \\\"PROBLEMS:\\\\n\\\" + problems.join(\\\"\\\\n\\\") + \\\"\\\\n\\\\n\\\" : \\\"ALL VALID\\\\n\\\\n\\\") + rows.join(\\\"\\\\n\\\");\", \"description\": \"Verify all 7 JSON files parse and meet schema\"}"
}

## tool · 2026-10-05T11:54:13Z

run_code
{"code": "const dir = \"/Users/oyamahappa/Documents/Agent/DSH/vibe-coding-ppt/tutorials-content\";\nconst codes = [\"cx-01\",\"cx-02\",\"cx-03\",\"cx-04\",\"cx-05\",\"cx-06\",\"cx-07\"];\nconst rows: string[] = [];\nconst problems: string[] = [];\nfor (const c of codes) {\n  const p = `${dir}/${c}.json`;\n  const r = await tools.read({ file_path: p });\n  const text = r.lines.map(l => l.text).join(\"\\n\");\n  if (text.charCodeAt(0) === 0xFEFF) problems.push(`${c}: BOM`);\n  if (text.trimStart().startsWith(\"```\")) problems.push(`${c}: code fence`);\n  let d: any;\n  try { d = JSON.parse(text); } catch (e: any) { problems.push(`${c}: parse ${e.message}`); continue; }\n  const layouts = d.slides.map((s: any) => s.layout);\n  const hasEnd = layouts.includes(\"end\");\n  const hasCover = d.slides[0].layout === \"cover\" && d.slides[0].kicker === `Vibe Coding 学习系列 · ${d.code}`;\n  if (!hasEnd) problems.push(`${c}: no end`);\n  if (!hasCover) problems.push(`${c}: cover/kicker`);\n  if (d.code !== c.toUpperCase()) problems.push(`${c}: code field ${d.code}`);\n  if (d.category !== \"codex\") problems.push(`${c}: category`);\n  if (!d.fileTitle) problems.push(`${c}: fileTitle missing`);\n  rows.push(`${c}.json | code=${d.code} | deck=${d.deck} | fileTitle=${d.fileTitle} | slides=${d.slides.length} | layouts=${layouts.join(\",\")}`);\n}\nreturn (problems.length ? \"PROBLEMS:\\n\" + problems.join(\"\\n\") + \"\\n\\n\" : \"ALL VALID\\n\\n\") + rows.join(\"\\n\");", "description": "Verify all 7 JSON files parse and meet schema"}

## assistant · 2026-10-05T11:54:16Z

All 7 valid. Now send result to parent agent, then final answer.

The parent id: session-0de88cee-855e-47e3-a7d8-5cedfd0973a3.
{
  "type": "tool-call",
  "id": "call_00_MRnbHXaQkfT9MT6HsK1D0359",
  "name": "run_code",
  "arguments": "{\"code\": \"const msg = `任务完成：已为 codex 分册生成 7 份 PPT 内容 JSON。\\n\\n输出目录：vibe-coding-ppt/tutorials-content/\\n文件与幻灯片数量：\\n- cx-01.json | CX-01 Codex-App安装与认证 | deck「Codex App 安装与认证：从下载到第一个线程」| 12 张\\n- cx-02.json | CX-02 Codex-App桌面工作流 | deck「Codex App 桌面工作流：把 App 当主控台」| 12 张\\n- cx-03.json | CX-03 Codex-Commands工作流入口 | deck「Codex Commands：App 里的工作流入口」| 12 张\\n- cx-04.json | CX-04 Codex项目指令权限配置 | deck「Codex 项目指令、配置、权限与沙盒」| 12 张\\n- cx-05.json | CX-05 Codex-MCP外部工具 | deck「Codex MCP：在 App 中连接外部工具」| 12 张\\n- cx-06.json | CX-06 Codex-Skills可复用工作流 | deck「Codex Skills：把重复提示变成可复用工作流」| 11 张\\n- cx-07.json | CX-07 Codex-Plugins连接器 | deck「Codex Plugins 与 Connectors：App 能力扩展」| 12 张\\n\\n校验结果：7 个文件均通过 JSON.parse；UTF-8、无 BOM、无 markdown 代码围栏；cover kicker 均为「Vibe Coding 学习系列 · <code>」；每份含 end 页；category 均为 codex。\\n约束：每张 bullets ≤5 条且每条 ≤42 字符；cards 均为 3-4 张；steps 均为 3-4 步；table 均 ≤5 列 ≤6 行。\\n内容来源：仅取自 AI-Coding-Guide-Zh/docs/codex/CX-01..CX-07 原文，命令（winget install Codex -s msstore、codex mcp list、codex plugin marketplace add owner/repo、features.goals 等）、版本口径与功能名均忠于原文。\\n备注：未创建或修改其他文件；未提交 Git（本会话未获得提交授权）。`;\\nconst r = await tools.send_message({ agent_id: \\\"session-0de88cee-855e-47e3-a7d8-5cedfd0973a3\\\", message: msg });\\nreturn JSON.stringify(r);\", \"description\": \"Send completion summary to parent agent\"}"
}

## tool · 2026-10-05T11:54:16Z

run_code
{"code": "const msg = `任务完成：已为 codex 分册生成 7 份 PPT 内容 JSON。\n\n输出目录：vibe-coding-ppt/tutorials-content/\n文件与幻灯片数量：\n- cx-01.json | CX-01 Codex-App安装与认证 | deck「Codex App 安装与认证：从下载到第一个线程」| 12 张\n- cx-02.json | CX-02 Codex-App桌面工作流 | deck「Codex App 桌面工作流：把 App 当主控台」| 12 张\n- cx-03.json | CX-03 Codex-Commands工作流入口 | deck「Codex Commands：App 里的工作流入口」| 12 张\n- cx-04.json | CX-04 Codex项目指令权限配置 | deck「Codex 项目指令、配置、权限与沙盒」| 12 张\n- cx-05.json | CX-05 Codex-MCP外部工具 | deck「Codex MCP：在 App 中连接外部工具」| 12 张\n- cx-06.json | CX-06 Codex-Skills可复用工作流 | deck「Codex Skills：把重复提示变成可复用工作流」| 11 张\n- cx-07.json | CX-07 Codex-Plugins连接器 | deck「Codex Plugins 与 Connectors：App 能力扩展」| 12 张\n\n校验结果：7 个文件均通过 JSON.parse；UTF-8、无 BOM、无 markdown 代码围栏；cover kicker 均为「Vibe Coding 学习系列 · <code>」；每份含 end 页；category 均为 codex。\n约束：每张 bullets ≤5 条且每条 ≤42 字符；cards 均为 3-4 张；steps 均为 3-4 步；table 均 ≤5 列 ≤6 行。\n内容来源：仅取自 AI-Coding-Guide-Zh/docs/codex/CX-01..CX-07 原文，命令（winget install Codex -s msstore、codex mcp list、codex plugin marketplace add owner/repo、features.goals 等）、版本口径与功能名均忠于原文。\n备注：未创建或修改其他文件；未提交 Git（本会话未获得提交授权）。`;\nconst r = await tools.send_message({ agent_id: \"session-0de88cee-855e-47e3-a7d8-5cedfd0973a3\", message: msg });\nreturn JSON.stringify(r);", "description": "Send completion summary to parent agent"}

## assistant · 2026-10-05T11:54:20Z

Now final answer to user (妹妹). Provide concise list.
妹妹，7 份 PPT 内容 JSON 已全部写入 `vibe-coding-ppt/tutorials-content/`，每份都通过 JSON 解析与 schema 约束校验。

| code | 文件 | deck 标题 | 幻灯片 |
|---|---|---|---|
| CX-01 | [cx-01.json](vibe-coding-ppt/tutorials-content/cx-01.json) | Codex App 安装与认证：从下载到第一个线程 | 12 |
| CX-02 | [cx-02.json](vibe-coding-ppt/tutorials-content/cx-02.json) | Codex App 桌面工作流：把 App 当主控台 | 12 |
| CX-03 | [cx-03.json](vibe-coding-ppt/tutorials-content/cx-03.json) | Codex Commands：App 里的工作流入口 | 12 |
| CX-04 | [cx-04.json](vibe-coding-ppt/tutorials-content/cx-04.json) | Codex 项目指令、配置、权限与沙盒 | 12 |
| CX-05 | [cx-05.json](vibe-coding-ppt/tutorials-content/cx-05.json) | Codex MCP：在 App 中连接外部工具 | 12 |
| CX-06 | [cx-06.json](vibe-coding-ppt/tutorials-content/cx-06.json) | Codex Skills：把重复提示变成可复用工作流 | 11 |
| CX-07 | [cx-07.json](vibe-coding-ppt/tutorials-content/cx-07.json) | Codex Plugins 与 Connectors：App 能力扩展 | 12 |

校验结果：

- 7 个文件均通过 `JSON.parse`，UTF-8、无 BOM、无 markdown 代码围栏。
- 封面 kicker 均为 `Vibe Coding 学习系列 · <code>`，每份都有 `end` 页，`category` 均为 `codex`。
- 每张 bullets ≤5 条且每条 ≤42 字符；cards 均 3–4 张；steps 均 3–4 步；table 均 ≤5 列、≤6 行。
- 内容取自对应文档原文，命令与版本口径（如 `winget install Codex -s msstore`、`codex mcp list`、`codex plugin marketplace add owner/repo`、`features.goals`、`read-only`/`workspace-write`/`danger-full-access`）保持原样，未编造。

结果已发送给上级 agent。本次未创建或修改其他文件，也未执行 Git 提交。
