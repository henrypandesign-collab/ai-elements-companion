# shadcn/ui AI Elements — reference (verified 2026-11-13)

Source: https://ui.shadcn.com/docs/ai-elements · Changelog entry "October 2026 – Trace, Code Block and AI Elements" (https://ui.shadcn.com/docs/changelog).
Status: **maintained successor** to Vercel AI SDK Elements. Default choice for new projects.

## What it is
- "Patterns for agentic interfaces, built from shadcn/ui components." No npm package — you copy compositions; the code is yours.
- 21 patterns. Every step-type pattern (Reasoning, Tool, Plan, Task, Queue, Sources, Subagent, Terminal, Test Results, Stack Trace, Chain of Thought) is built on **Trace**, so all steps share one shape: `Trace > TraceCollapsible > TraceCollapsibleTrigger (TraceLine + TraceIcon + TraceTitle [+ TraceDescription]) > TraceCollapsibleContent`.
- TraceLine `status`: `"running"` (shimmer while running) · `"error"` · `"pending"` · none (done). Lines can expand, link out, or open a dialog/sheet/drawer/popover.
- Three primitive variants per pattern: Base UI (default, `/docs/ai-elements/base/<slug>`), React Aria (`/aria/`), Radix (`/radix/`).
- Markdown via Streamdown (https://streamdown.ai); fenced code → Code Block (line numbers, copy).
- Starter: https://github.com/shadcn-ui/chatbot-template (Next.js + AI SDK + shadcn).
- Helpers: `@shadcn/helpers/ai-sdk` → `createChat()` (`.user()`, `.assistant(({writer}) => …)`, `needsApproval`, questions). Questionnaire component (Aug 2026) for multi-step question flows.
- Registry files import `cn` from the `cn` package (Sep 2026; `pnpm dlx shadcn@latest migrate cn`).
- Agent-friendly docs: every page has a `.md` version, e.g. `https://ui.shadcn.com/docs/ai-elements/base/reasoning.md`.

## Install commands (pnpm shown; npm/yarn/bun equivalents exist)
| Pattern | Command |
|---|---|
| Chat | `pnpm dlx shadcn@latest add message-scroller message bubble input-group` |
| Message | `… add message bubble tooltip` |
| Prompt Input | `… add input-group attachment dropdown-menu` |
| Model Selector | `… add dropdown-menu input-group` |
| Suggestion | `… add button` |
| Checkpoint | `… add marker button` |
| Confirmation | `… add item button` |
| Context | `… add hover-card progress` |
| Inline Citation | `… add hover-card button` |
| File Tree | `… add collapsible button` |
| Plan, Queue, Reasoning, Sources, Task | `… add trace` |
| Tool, Terminal, Test Results, Stack Trace | `… add trace code-block` |
| Chain of Thought, Subagent | `… add trace code-block badge` |
Project init: `pnpm dlx shadcn@latest init -t next|vite|start|react-router|astro`.

## Patterns by need

### Thread & turns
- **Chat** — thread inside Message Scroller. Parts: MessageScrollerProvider(`autoScroll`), MessageScroller, …Viewport, …Content, MessageScrollerItem(`messageId`, `scrollAnchor`), MessageScrollerButton (jump-to-latest). *Micro:* the user's own message is the scroll anchor → new question settles near the top, reply streams beneath; follows the reply only while the user stays at the live edge. Empty state demo: "What should we build?". Replaces `use-stick-to-bottom`.
- **Message** — one turn. Message(`align`), MessageContent, MessageFooter, Bubble(`align="end" variant="muted"` for user), MessageResponse (Streamdown), MessageToolbar, branch parts. Footer actions: Copy (icon swaps to check for 2s), Good/Bad response (`aria-pressed` toggles), Retry (`regenerate({messageId})`), Edit on user turn (puts text back into field). Icon buttons = Button ghost icon-sm + Tooltip + aria-label.
- **Checkpoint** — Marker(separator) + Button xs outline "Restore". Restore = `setMessages(messages.slice(0, i+1))`. Data part `{type:"data-checkpoint", id, data:{label}}`; same id updates.
- **Suggestion** — Suggestions row of Button outline sm `shrink-0`; horizontal scroll with `scroll-fade-x` edge fade. `sendMessage({text})`.

### Input & controls
- **Prompt Input** — InputGroup + InputGroupTextarea + Attachment + DropdownMenu. Parts: PromptInput, PromptInputTextarea, PromptInputActionMenuTrigger (+ icon, round), PromptInputSubmit (ArrowUp idle → spinner/stop by status), PromptInputHeader (attachment chips with remove), PromptInputSelect, HoverCard, tabs. *Micro:* Enter sends (`requestSubmit`), Shift+Enter newline; submit `disabled={!canSend}`, `aria-label="Send"`; hidden file input; model/effort menus in `block-end` addon.
- **Model Selector** — two DropdownMenus (model, effort) with RadioGroup, `closeOnClick`. No search (old cmdk dialog removed). Sends `body:{model, effort}`.

### Agent activity (Trace-based)
- **Reasoning** — props `isStreaming, open, defaultOpen, onOpenChange, duration`. Title "Thinking" → "Thought for 5s". *Micro:* auto-opens while thinking, closes on finish; user's manual open/close wins; LoaderCircle `animate-spin` while running. Duration must be measured on the server and sent as message metadata.
- **Chain of Thought** — summary that expands into steps. "Researching" → "Researched in N steps"; failed count → error. `open ?? running` so user choice wins; `keepMounted`. Search results as Badge secondary per hostname.
- **Plan** — all steps up front incl. pending; title = goal, description = progress ("2 of 4 done"). TraceLine running while streaming (replaces Shimmer). PlanAction sits beside the trigger (no buttons inside triggers). Data part `data-plan` with fixed id.
- **Task** — steps appear only as taken; present tense while running ("Updating…"), past tense when done, "Failed to…" on error. Data part `data-task`.
  - *Plan vs Task:* Plan = known steps + progress, one per reply. Task = live log of what is happening, one or more.
- **Queue** — todo list split "To do" / "Completed". pending → Circle; in_progress → CircleDot + running only while chat streams (shimmer stops when agent stops); completed → CircleCheck. Reads last `tool-writeTodos` part.
- **Tool** — states: input-streaming/input-available → running "Running …" (→ error "Failed to run…" if chat stopped; client tools stay *waiting*, not failed, until `addToolOutput`); approval-requested → Confirmation Item (not a line); approval-responded → running or "Denied…"; output-available → "Ran …"; output-error → error; output-denied → "Denied …". ToolInput/ToolOutput use CodeBlock sm. Long output → wrap line in SheetTrigger.
- **Subagent** — Agent header "Ran the research agent" + model Badge + run time; content shows tool calls so far; `preliminary: true` output = still running.
- **Terminal** — `output, isStreaming, autoScroll, onClear`; open line once first output arrives; non-zero exit → error. Stream with `data-terminal` part keyed by toolCallId. Drops `ansi-to-react`.
- **Test Results** — "Ran 42 tests, 2 failed"; suites with failures `defaultOpen`.
- **Stack Trace** — error line, frames list (node_modules dimmed), own frames are buttons opening file:line; full error repeated in content. Only send stacks in development.
- **Sources** — "Used 3 sources" trigger; each Source is an `<a>` TraceLine, new tab with sr-only "(opens in a new tab)". Dedupe `source-url` by url, title falls back to hostname.

### Approval
- **Confirmation** — Item outline sm: ItemMedia icon, ItemTitle "Run {command}?", ItemDescription scope, ItemActions Deny (outline) / Approve. `addToolApprovalResponse({id, approved})` + `useChat({sendAutomaticallyWhen: lastAssistantMessageIsCompleteWithApprovalResponses})`. After answering, becomes a Tool line.

### Context & references
- **Context** — HoverCard trigger Button "{percent}% context" (`delay=10, closeDelay=100`); content: used/limit + Progress. Usage via `messageMetadata` on finish; model limit must be supplied by you.
- **Inline Citation** — HoverCard on Button secondary xs (hostname) — Button so it's keyboard-focusable; title + external link.
- **File Tree** — Collapsible folders (chevron `rotate-90` when open), ghost Button files with `onSelect(path)`. Single file → use a Tool line instead.

## Migration from Vercel AI SDK Elements
- "You do not need to migrate." Copied code keeps working. Each pattern page has a migration prompt that rebuilds the file on Trace/Code Block **keeping every export name and prop**.
- Mapping: agent→Subagent, conversation→Chat, question→Questionnaire, shimmer→shimmer utility, commit→Trace(#commit), loader→Spinner; others map 1:1 by name.
- **Not rebuilt** (build yourself from shadcn parts if needed): artifact, audio-player, canvas/connection/controls/edge/node/panel/toolbar (React Flow), environment-variables, image, jsx-preview, mic-selector, voice-selector, open-in-chat, package-info, persona (Rive), sandbox, schema-display, snippet, speech-input, transcription, web-preview.

## Strengths / weaknesses (design judgment)
+ Maintained, free (MIT shadcn), one consistent Trace grammar for all agent steps, strong a11y defaults, AI SDK wiring documented per state, three primitive libraries.
+ Honest state semantics (waiting vs failed, user's open state wins, shimmer stops when agent stops).
− Visually neutral/minimal; little "delight" motion beyond shimmer/spin. No voice, workflow canvas, artifact, web preview.
− Assumes shadcn + Tailwind + AI SDK conventions.
