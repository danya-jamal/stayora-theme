# Gutenberg Agent Guidelines

Build responsive, accessible pages that remain easy to edit in Gutenberg.

## Before Building

Inspect the active theme, `theme.json`, existing blocks, variations, styles, patterns, assets, and current page content. Reuse existing solutions before adding code.

## Implementation Order

Use the first suitable option:

1. Core block or existing variation/style
2. Core blocks composed as a pattern
3. New block style for appearance
4. New variation for defaults or an InnerBlocks template
5. Custom parent/child block for complex behavior
6. Dynamic PHP block for server data

Use ACF only for structured data, relationships, validation, or repeaters. Keep normal copy and media in core blocks or `InnerBlocks`.

## Content

- Store editable content in block markup, never PHP, JavaScript, CSS, or pseudo-elements.
- Give major Groups clear `metadata.name` values.
- Use one `h1` and logical heading order.
- Use core Button blocks for CTAs and verified URLs.
- Use patterns for reusable sections.

## Styling

- Define reusable colors, typography, spacing, gradients, and layout widths in `theme.json`.
- Use WordPress preset variables in CSS.
- Avoid inline styles and unexplained Additional CSS Classes for reusable treatments.
- Use flex, grid, and `clamp()` before adding media queries.
- Prevent overflow at 320px.

## Media

- Reuse supplied assets and Media Library items first.
- Store remote design exports locally.
- Use Image or Cover blocks for replaceable media.
- Use CSS backgrounds only for decoration.
- Keep icons separate from RichText.
- Preserve dimensions or aspect ratio.
- Use useful alt text, or empty alt text for decorative images.

## Custom Blocks

- Use `block.json` and register blocks server-side.
- Use parent/child blocks for sliders, tabs, and repeatable panels.
- Keep items editable, reorderable, duplicable, and removable.
- Support keyboard input, visible focus, ARIA, reduced motion, and usable content without JavaScript.

## Validate

- Run relevant syntax and lint checks.
- Confirm every saved block is registered.
- Save and reload in Gutenberg without invalid-block warnings.
- Test representative edits, desktop/mobile layouts, keyboard use, overflow, assets, and console errors.
- Report page ID, status, URLs, changed files, validation, and remaining differences.