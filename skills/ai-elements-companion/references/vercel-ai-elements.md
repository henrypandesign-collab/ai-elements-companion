# Vercel AI SDK Elements — reference (verified 2026-11-13)

Sources: https://elements.ai-sdk.dev/ · https://github.com/vercel/ai-elements
Status: **legacy, deprecating end of November 2026** → replaced by shadcn AI Elements (see `shadcn-ai-elements.md`). Banner: "AI Elements is moving to shadcn/ui." Setup page: new projects should install from shadcn/ui. Still valuable for (a) projects that already use it, (b) components shadcn did **not** rebuild (voice, workflow canvas, artifact, web preview, etc.).

## Facts
- License Apache-2.0 (© Vercel). CLI `ai-elements` 1.9.1 (shows deprecation notice). Loader deprecated → shadcn Spinner (1.8.2).
- Prereqs: Node 18+, React 19, Next.js 14+ (App Router), AI SDK, shadcn/ui initialized, Tailwind 4, CSS-variables mode.
- Install: `npx ai-elements@latest` (all) · `npx ai-elements@latest add <slug>` · `npx shadcn@latest add @ai-elements/<slug>` · `npx shadcn@latest add https://elements.ai-sdk.dev/api/registry/<slug>.json`. Installs to `@/components/ai-elements/`.
- Key deps: ai ^6, @ai-sdk/react, streamdown ^2.4 (+code/math/mermaid/cjk), shiki 3.22, use-stick-to-bottom, motion ^12, @xyflow/react ^12, media-chrome, @rive-app/react-webgl2, tokenlens, react-jsx-parser, ansi-to-react, lucide-react, cmdk (via shadcn Command), Radix.
- Message needs `@source "../node_modules/streamdown/dist/*.js";` in globals.css.

## Full inventory

### Chatbot
| Component | Purpose · key API · micro-interactions |
|---|---|
| Attachments | files/images/video/audio/source docs; grid/inline/list layouts |
| Chain of Thought | steps with `status` complete/active/pending, search-result badges, images; fade+slide transitions; `defaultOpen` false |
| Checkpoint | Separator + BookmarkIcon + ghost "Restore" trigger; restore logic app-side |
| Confirmation | tool approval on Alert; renders by state: approval-requested → Request+Actions; responded → Accepted/Rejected |
| Context | **circular SVG ring** trigger %, hover card with input/output/reasoning/cache token breakdown + **USD cost** (tokenlens), compact numbers (K/M/B) |
| Conversation | stick-to-bottom auto-scroll, scroll-to-bottom button when away, EmptyState (title/description/icon), **Markdown download** |
| Inline Citation | hover pill with count, **source carousel** (prev/next/index), quote |
| Message | `from` user/assistant/system; MessageResponse (streaming-safe markdown, GFM, KaTeX); MessageActions (retry/like/dislike/copy/share, tooltips); **MessageBranch** (prev/next/page "2 of 3" between regenerated versions) |
| Model Selector | cmdk **command-palette dialog** with fuzzy search, provider groups + logos, shortcuts |
| Plan | Card + Collapsible; `isStreaming` shimmers title/description |
| Prompt Input | auto-resizing textarea; Enter/Shift+Enter; **drag-drop & global drop**; `maxFiles`, `maxFileSize`, `accept` with `onError` codes; action menu (add files, **screenshot** via getDisplayMedia); `PromptInputSubmit status` (submitted/streaming/error) + `onStop`; select, hover card, tabs, command; hooks `usePromptInputAttachments`, `usePromptInputController`, `usePromptInputReferencedSources` |
| Question | human-in-the-loop single/multi select + freeform textarea; Submit disabled until valid; async onSubmit |
| Queue | collapsible sections of messages/todos/attachments; completed items strikethrough+opacity; hover reveals item actions |
| Reasoning | auto-opens while streaming, closes when finished; pulsing indicator; `getThinkingMessage(isStreaming, duration)` |
| Shimmer | text shimmer: `duration` 2s, `spread` 2, `as` |
| Sources | collapsible list "Used N sources" |
| Suggestion | horizontal ScrollArea of pills |
| Task | collapsible task with TaskItemFile chips; progressive reveal |
| Tool | collapsible card + status Badge: Pending / Running / Awaiting Approval / Responded / Completed / Error / Denied; chevron rotation; completed & errored open by default; ToolInput formatted JSON |

### Code
Agent (model, instructions, tools accordion, output schema) · Artifact (header/title/description/actions/close/content container) · Code Block (Shiki, copy→check 2s, language selector, line numbers) · Commit (hash, author avatar, file list with added/modified/deleted/renamed, +/- counts) · Environment Variables (masked values, show toggle, copy name/value/export) · File Tree (expanded Set, selectedPath) · JSX Preview (streams JSX, auto-closes tags) · Package Info (major/minor/patch badge) · Sandbox (code/output tabs + state badge) · Schema Display (REST method/path/params/request/response) · Snippet (inline command + copy) · Stack Trace (parsed frames, dims node_modules, clickable paths, maxHeight 400) · Terminal (ANSI streaming, autoScroll, clear, copy) · Test Results (summary + progress, suites, per-test status/duration/error) · Web Preview (iframe, URL bar, back/forward, **Desktop/Tablet/Mobile**, console logs)

### Voice
Audio Player (media-chrome controls, ±10s seek) · Mic Selector (permission on first open, devicechange listener) · **Persona** (Rive WebGL2 orb; states idle/listening/thinking/speaking/asleep; variants obsidian/mana/opal/halo/glint/command) · Speech Input (Web Speech API in Chrome/Edge, MediaRecorder fallback; states default/listening pulse/processing spinner/disabled) · Transcription (click-to-seek segments; active/past/future styling) · Voice Selector (dialog with gender/accent/age attributes, preview play)

### Workflow (React Flow)
Canvas (pan on scroll, Delete removes, fit view) · Node (handles target-left/source-right, header/title/description/action/content/footer) · Edge (Temporary dashed bezier; Animated moving dot 2s) · Connection (animated bezier) · Controls · Panel (6 positions) · Toolbar (NodeToolbar)

### Utilities
Image (AI SDK generated image base64/uint8Array) · Open In Chat (open query in ChatGPT/Claude/T3/Scira/v0/Cursor)

## Strengths / weaknesses
+ Broadest catalog (≈50): voice, workflow, code-agent surfaces; rich behavior (branching, carousel citations, cost-aware context ring, drag-drop composer).
+ Deeply wired to AI SDK UI message parts/tool states.
− Deprecating; new work should start from shadcn. Heavier dependency set (Rive, media-chrome, xyflow, cmdk, tokenlens).
− Some docs examples use older AI SDK shapes (Stack Trace) or internal import paths (`@repo/elements`).
**Rule:** don't force-migrate working code; for missing shadcn patterns, port the *behavior* from here onto shadcn primitives.
