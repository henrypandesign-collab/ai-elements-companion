# Kobra — reference (verified 2026-11-13)

Source: https://kobra.systems/components/plan-card (sidebar = full catalog; https://kobra.systems/ and /components show Input OTP, not an index) · https://kobra.systems/pricing
By Harsh Singh. Stack: React (client components), Tailwind, **shadcn-compatible API**, **Base UI** primitives, **Motion** (`motion/react`), Tabler icons, optional **interface sound layer**. Has Figma kit, `/install.md` "one file your agent reads", MCP server (paid).
Install: `npx shadcn@latest add @kobra/<slug>` (shadcn registry). Components expose `data-slot` attributes for styling.

## Licensing / gating — respect it
- Free: 11 components, **personal use only**: Input OTP, Navigation Menu, Video, Carousel, AI Editor, Morphing Icons, Command Menu, Toast, Conversation, Halftone Dots, Sound.
- Paid: Individual $199 one-time (commercial, lifetime), Teams $599 (seats), or single component **$19**. Paid pages show a blurred placeholder source. **Never bypass the gate or reconstruct paid source.** For paid components: use the public demo as interaction inspiration, implement independently, or tell the user to buy it.
- Free tier is personal-use only → flag before using in commercial products.

## Catalog (89 in sidebar; pricing claims 100+)
- **Agents (paid):** Plan Card, Task List, Trace Waterfall, Question Card (Updated), Reasoning Steps, Chat History, Message, Chat Input (Updated)
- **Generative UI (paid):** Agent Map (New), Product Cards (New), Composer (New), Image Generation (Updated), Weather (New), Conversion (New), Document Agent, Streaming Text, Inline Citations, Code Block
- **Free AI-adjacent:** AI Editor, Conversation, Sound, Command Menu, Toast, Morphing Icons
- Also: Content (14), Feedback (5), Form controls (19), Layout (9), Navigation (5), Overlays (8).
- Not deep-read yet: Agent Map, Composer, Document Agent, Streaming Text, Inline Citations, Chat Input, Message, Chat History, AI Editor, Conversation → fetch `https://kobra.systems/components/<slug>` when shortlisted.

## Deep-read components
- **Plan Card** (`@kobra/plan-card`, paid) — "A plan an agent is asking to run." Props: children, className. Demo anatomy: title, description, "To-dos" checklist with count badge, "3 more / Show less", footer **"Auto Approve in 10s" countdown**, View/Hide Plan toggle, **Approve ⌘Enter**. Running/done/error states not shown. ⚠ Auto-approve countdown is unsafe for consequential actions — keep it only for low-risk, reversible plans and make it cancelable.
- **Task List** (`@kobra/task-list`) — "A task list an agent works through." "Tasks 0/5", per-item % complete.
- **Trace Waterfall** (`@kobra/trace-waterfall`, Base UI Popover) — props `spans: TraceSpan[]`, `now`. Live timeline of an agent run: stats (Duration, Cost, Tokens, LLM calls, Tool calls, Errors), time axis, zoom presets 0.5×–4×, ⌘F search with empty state, legend Model call / Tool call / Waiting / Handoff / Failed, "Slowest" tag. Best for developer/observability surfaces, not end users.
- **Question Card** (`@kobra/question-card`, Motion) — "Questions 0 of 3 answered", lettered A–D options each with a rationale line, Skip / **Next ⌘Enter**.
- **Reasoning Steps** (`@kobra/reasoning-steps`, Motion) — props `stages` (req), `sources`, `reasoning`, `stageMs` 1750, `reasonMs` 650, `onDone`. Staged reveal of model work before answering. ⚠ Timed reveal is simulated pacing — drive from real events in production.
- **Input OTP** (free) — exemplary micro-interaction craft: spring focus ring (duration 0.3, bounce 0.18), digit enter `translateY(6px) rotateX(-35deg) blur(2px)` → rest, paste sweep stagger 45ms, success sweep, invalid ring, `useReducedMotion` fallback.

## Strengths / weaknesses
+ Highest micro-interaction polish (Motion springs, keyboard shortcuts, sound), shadcn-compatible install, novel generative-UI cards (Agent Map, Product Cards, Weather, Conversion).
− Mostly paid; free tier personal-use only; minimal prop docs (children/className); state coverage beyond demos not documented.
