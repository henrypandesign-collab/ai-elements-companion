# Beautiful UI — reference (verified 2026-11-13)

Source: https://www.beautifului.dev/ (single page, anchors per component) · /license · /harness ("Ice Cream Harness" demo app with "Fork this").
By Turbo (turbodesign.co), © 2026 Shane Levine. **MIT license**, free. Tagline: "Crafted primitives for AI-native interfaces."
Distribution: "copy-paste ready" (newsletter copy). Framework, install CLI, dependencies and per-component code links are **not shown** on the site — verify code availability before promising direct reuse; otherwise treat as visual/interaction reference and rebuild on the project's primitives.
Strength: polished, *task-centered* AI work surfaces (tables, insights, inspector) rather than chat-only; strong visual craft. Demo content is a fictional ice-cream ops business.

## 21 components
| # | Name (anchor) | Need | Anatomy / states / micro-interactions (as described on site) |
|---|---|---|---|
| 01 | Loading State `#loading-state` | agent is working | pixel-grid loader with **shimmer + elapsed timer** ("Churning 0.0s"); variants Churning, Drive, Dots, Orbit, Surfer |
| 02 | Thinking `#thinking-state` | see intermediate steps | expandable trace grouped Steps / Reasoning / Search / Coding |
| 03 | Streaming Text `#streaming-text` | read answer + verify | streamed answer, inline source icons, "10 sources" cards, **Follow-ups** suggestions |
| 04 | Approval Card `#approval-card` | agent asks before acting | multi-question pager "1 / 3", option list, Skip / Continue |
| 05 | Tool Chips `#tool-chips` | compact activity | single chip "4 tool calls, 2 messages" (collapses activity) |
| 06 | Task Rows `#task-rows` | live task status | numbered rows w/ running/completed/failed, metric sub-lines ("12/12", "68%"), nested subtasks with *draft* badges, **Capsules / List** view toggle |
| 07 | Chat `#chat-composer` | tabbed chat panel | tabs per thread, tool-result chips with durations ("for 4s"), reasoning chips, composer |
| 08 | Prompt Bar `#prompt-bar` | compose | **@ sources, / commands, model picker, dictation**; shapes Rounded / Pill |
| 09 | Recommendation Card `#recommendation-card` | agent proposes action | question + suggestion, "Other options" list with status tags, **confidence meter** ("High confidence"), Alternatives / Accept |
| 10 | Context Cards `#context-cards` | RAG transparency | "All chunks 32", chunk cards w/ char count, source type tag (PDF/CSV), filename |
| 11 | Diff Table `#diff-table` | review AI edits to data | proposed edits **sweep through** table rows |
| 12 | Records Table `#records-table` | CRM grid | tag chips (+3), last interaction, connection strength, footer aggregates ("55% average"), sorting |
| 13 | Filter Table `#filter-table` | filter by status | status chips with counts that **reorganize live data** |
| 14 | Sidebar Nav `#sidebar-nav` | app shell | workspace header, New chat, chat list, Upgrade; collapsible with **gliding hover highlight** |
| 15 | Search `#search` | command palette | live filtering, suggested actions, empty state |
| 16 | Flowchart `#flowchart` | workflow builder | Trigger + If/Else nodes on dotted canvas |
| 17 | Insight Cards `#insight-cards` | proactive analytics | paged insights with **scrub-ready live charts**, @mention entity, follow-up prompt |
| 18 | Code Block `#code-block` | show code | filename tab, Copy, Code / Diff tabs, line numbers |
| 19 | Fine-tune Card `#fine-tune-card` | agent edits design props | inspector (W/H, radius, opacity, type) adjusted by agent |
| 20 | Selection Actions `#selection-actions` | rewrite selected text | floating toolbar on selection: Explain, Improve, Shorten, Tone, Grammar |
| 21 | Agent Screen `#agent-screen` | computer-use visibility | watch agent's screen; Open, teach a task, record; Working/Loading status |

## Use it for
Inspiration and interaction ideas where shadcn has no equivalent: Diff Table, Insight Cards, Selection Actions, Recommendation Card, Context Cards, Agent Screen, Fine-tune Card, Task Rows view toggle, elapsed-time loader.
Caveats: still screenshots/text can't reveal exact timing — never claim specific durations/easing. Confidence meters need a defensible data source.
