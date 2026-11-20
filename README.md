# AI Elements Companion

An Agent Skill for reviewing and designing AI interfaces. Use it with a screenshot, a Figma file, an existing flow, or a product brief.

- Compare interaction patterns from shadcn AI Elements, Vercel AI Elements, Beautiful UI, and Kobra.
- Specify streaming, citations, approvals, cancellation, and recovery states.
- Map shortlisted patterns to the product's design system, then produce the requested review, editable Figma design, or working code.

## Install

In Codex, ask the skill installer to install the folder:

```text
$skill-installer install https://github.com/henrypandesign-collab/ai-elements-companion/tree/main/skills/ai-elements-companion
```

For a project-local installation, place the entire [skill folder](skills/ai-elements-companion) under `.agents/skills/` in your project. For a personal installation in Codex, place it under `~/.agents/skills/`.

## Try it

```text
$ai-elements-companion Review this AI research flow. Recommend patterns for
streaming, source citations, and partial failure. Map them to our existing
design system and specify the states and keyboard behavior.
```

## Reference material

- [Cross-library component matrix](skills/ai-elements-companion/references/component-matrix.md)
- [Design Resource Library](skills/ai-elements-companion/references/design-resource-library.md)
- [Skill instructions](skills/ai-elements-companion/SKILL.md)

The bundled component notes are dated snapshots. Check upstream documentation for current APIs, access, and licensing. Figma and code delivery depend on the tools and project permissions available in the host agent. Third-party components and assets are governed by their upstream licenses.
