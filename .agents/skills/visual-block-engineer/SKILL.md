---
name: visual-block-engineer
description: Build high-fidelity custom WordPress blocks whose fixed composition, parent/child structure, or interaction cannot be represented accurately with core blocks, patterns, or block styles. Do not use for ordinary Gutenberg sections.
---

# Visual Block Engineer

Build the smallest custom-block architecture that preserves the approved design, direct editing, and structural safety. First inspect the repository's WordPress version, block conventions, build setup, tokens, and existing components. Follow repository instructions over generic examples in the references.

## Architecture

1. Confirm that core blocks, a pattern, or a block style/variation cannot meet the design. Otherwise stop using this skill and use the simpler architecture.
2. Default to a static block. Use a parent/child block family for repeatable or independently selectable items such as slides, tabs, or accordion rows. Use server rendering only for runtime WordPress data or server-only logic.
3. Use block attributes and `RichText`/media controls for fixed semantic fields; use constrained `InnerBlocks` when editors need nested block content. Keep text and replaceable media editable on canvas, while locking only structure that must not change.
4. For frontend state, prefer the Interactivity API only when the project's minimum WordPress version and toolchain support it. Keep editor behavior in React and provide semantic, usable HTML before enhancement.

## Reference Router

The references are lookup manuals, not prerequisite reading. Open only the relevant file and search for the listed heading or term; do not load a reference cover to cover.

| Need | Reference | Search first |
| --- | --- | --- |
| Metadata, attributes, supports, assets, variations, registration | [block-json-guide.md](references/block-json-guide.md) | `Quick Reference Table`, `Attributes Schema`, `Supports Catalog`, `Asset Registration`, or the exact field name |
| Editor JSX, direct manipulation, controls, InnerBlocks, data access, migrations | [editor-patterns.md](references/editor-patterns.md) | `useBlockProps`, `RichText`, `MediaUpload`, `InnerBlocks Patterns`, `useSelect`, or `Block Deprecation Patterns` |
| PHP rendering, context, runtime queries, or dynamic InnerBlocks | [dynamic-blocks-guide.md](references/dynamic-blocks-guide.md) | `Static vs Dynamic Decision Guide`, `render PHP File Pattern`, `InnerBlocks with Dynamic Blocks`, or `Escaping` |
| Tabs, accordions, toggles, or other frontend state on WordPress 6.5+ | [interactivity-api-guide.md](references/interactivity-api-guide.md) | `Setup Requirements`, the needed `data-wp-*` directive, `Context vs State`, or `Common Interactivity API Mistakes` |

Combine references only at an actual boundary—for example, an interactive server-rendered parent block may require metadata, dynamic rendering, and Interactivity API lookups. Treat version claims and examples as guidance; verify uncertain APIs against the project's installed WordPress packages or official documentation.

## Implementation Invariants

- Match the approved composition, dimensions, spacing, typography, colors, assets, and responsive intent. Separate full-bleed width, content width, and readable text measure.
- Use only project `theme.json` preset variables in CSS. Avoid one-off inline styles and reusable styling hidden in Additional CSS Classes.
- Use `useBlockProps()` in the editor and the matching saved or server-rendered wrapper API. Keep saved markup stable; add a deprecation before changing existing static markup.
- Never store persistent content only in React state. Never place `<img>` or `<svg>` inside `RichText`; keep media separately selectable and give meaningful images useful alt text.
- A dynamic block with InnerBlocks must serialize `<InnerBlocks.Content />` and render the received `$content`. Validate attributes and escape newly generated PHP output for its context.
- For sliders, tabs, and accordions, use parent/child blocks with keyboard operation, visible focus, accurate ARIA state, and reduced-motion behavior.
- Prevent overflow at 320px and preserve media aspect ratios. Use logical headings with no extra page-level `h1`.

## Work Boundary

Verify proportionally to the change. Run targeted syntax and build checks when available. For visual work, inspect representative editor and frontend renders at the approved desktop width and 320px, then fix issues caused by the implementation. Avoid broad or repetitive review loops. If runtime verification is unavailable, state what remains unverified.