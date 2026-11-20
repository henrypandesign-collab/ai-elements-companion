# Cross-library component matrix (verified 2026-11-13)

Legend: **S** = shadcn AI Elements (maintained, free) · **V** = Vercel AI SDK Elements (deprecating end Nov 2026, Apache-2.0) · **B** = Beautiful UI (MIT, code distribution unverified) · **K** = Kobra (mostly paid; free tier personal-use).
Default stance: build on **S**; port missing behavior from **V**; borrow interaction/visual ideas from **B**/**K**; only install **K** code if the user owns a license.

| User need | S | V | B | K | Recommended starting point |
|---|---|---|---|---|---|
| Thread / scroll | Chat (Message Scroller, user msg = scroll anchor) | Conversation (stick-to-bottom, md download) | Chat (tabbed) | Conversation (free), Chat History | S Chat; add tabs from B if multi-thread |
| Single turn + actions | Message (copy/feedback/retry/edit) | Message + Branch navigator | Streaming Text (follow-ups) | Message | S Message; add V branch nav if regenerations matter |
| Composer | Prompt Input (attachments, model/effort menus) | Prompt Input (drag-drop, limits, screenshot, onStop) | Prompt Bar (@ sources, / commands, dictation) | Composer, Chat Input | S Prompt Input + B's @/ triggers when context selection is a core job |
| Model choice | Model Selector (2 dropdowns) | cmdk dialog w/ search + logos | in Prompt Bar | — | S if ≤ ~8 models; V-style search dialog if many |
| Thinking | Reasoning (auto open/close, duration) | Reasoning, Chain of Thought, Shimmer | Thinking (Steps/Reasoning/Search/Coding), Loading State (elapsed timer) | Reasoning Steps (staged) | S Reasoning; B elapsed timer for long waits |
| Plan before acting | Plan (pending steps, "2 of 4 done") | Plan (Card + shimmer) | — | Plan Card (auto-approve countdown, ⌘Enter) | S Plan + explicit Approve; K countdown only for reversible low-risk |
| Live progress | Task, Queue (to do / done) | Task, Queue | Task Rows (metrics, subtasks, view toggle), Tool Chips | Task List, Trace Waterfall | S Task/Queue; B Tool Chips to collapse noise |
| Tool calls | Tool (full state table) | Tool (status badges) | Tool Chips | — | S Tool |
| Approval / HITL | Confirmation (Approve/Deny) + Questionnaire | Confirmation, Question | Approval Card (paged questions), Recommendation Card | Question Card (rationale per option) | S Confirmation/Questionnaire; K rationale lines improve decisions |
| Sources / grounding | Sources, Inline Citation | Sources, Inline Citation (carousel) | Context Cards (chunks), Streaming Text sources | Inline Citations | S + B Context Cards for RAG-heavy tools |
| Context window | Context (% + progress) | Context (ring + cost) | — | — | V ring/cost if cost matters to user |
| Edit review | File Tree, Code Block | Commit, Code Block, Package Info | **Diff Table**, Code Block diff tab | Code Block | B Diff Table for data; S Code Block for code |
| Structured output / insights | — | Artifact, Web Preview, JSX Preview | **Insight Cards**, Records/Filter Table | Product Cards, Weather, Conversion, Document Agent | B/K inspiration on S Card/Table primitives |
| Inline editing | — | — | **Selection Actions** | AI Editor (free) | B pattern on Popover/Toolbar |
| Recommendation | Suggestion | Suggestion | **Recommendation Card**, follow-ups | — | B, but only show confidence with a real signal |
| Checkpoint / undo | Checkpoint | Checkpoint | — | — | S |
| Dev / coding agent | Terminal, Test Results, Stack Trace, Subagent | + Sandbox, Env Vars, Schema, Snippet, Agent | Code Block | Trace Waterfall | S; V for missing pieces |
| Workflow builder | — | Canvas/Node/Edge (React Flow) | Flowchart | Agent Map | V port on React Flow |
| Voice | — | Persona, Speech Input, Transcription, Mic/Voice Selector, Audio Player | dictation in Prompt Bar | Sound | V (port) |
| Computer use | — | Web Preview | **Agent Screen** | — | B pattern |
| App shell / search | (shadcn Sidebar, Command) | — | Sidebar Nav (gliding hover), Search | Command Menu, Navigation | shadcn primitives + B hover polish |

## Microinteraction library (state → behavior) — reuse when specifying
| Moment | Behavior | Origin |
|---|---|---|
| Submit | Enter sends, Shift+Enter newline; submit disabled when empty; icon → spinner → stop while streaming; Esc/Stop cancels | S/V Prompt Input |
| Streaming scroll | follow only while user is at live edge; manual scroll-up pauses; "jump to latest" button; user's message anchors near top | S Chat |
| Thinking | auto-expand while streaming, auto-collapse on done, user toggle overrides; label Thinking → "Thought for Ns" (server-measured) | S/V Reasoning |
| Running step | shimmer on running line; stop shimmer when agent stops; present tense → past tense; error → "Failed to …" | S Trace/Task |
| Long wait | elapsed-time counter, not fake % | B Loading State |
| Tool approval | inline card with scope ("Run X? runs in this project"), Deny/Approve; chat auto-continues when all answered | S Confirmation |
| Plan approve | ⌘/Ctrl+Enter approve; View/Hide plan; show more/less; countdown only for reversible actions, always cancelable | K Plan Card |
| Copy | icon swaps to check ~2s, aria-live polite | S/V |
| Feedback | 👍/👎 toggle with aria-pressed | S Message |
| Citation | hover/focus opens card (delay ~10ms in, 100ms out); keyboard-focusable trigger | S Inline Citation |
| Data edit | proposed changes sweep through rows; accept/reject per row | B Diff Table |
| Selection | floating toolbar appears on text selection | B Selection Actions |
| Nav hover | gliding highlight between items | B Sidebar Nav |
| Input craft | spring focus ring, staggered sweeps, reduced-motion fallback | K Input OTP |
| Restore | Restore truncates later turns; confirm if destructive | S Checkpoint |
Always: `prefers-reduced-motion` fallback, status not by color alone, focus visible, live-region announcements restrained (completion/errors only).
