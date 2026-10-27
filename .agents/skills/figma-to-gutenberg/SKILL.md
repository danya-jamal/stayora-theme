---
name: figma-to-gutenberg
description: Reproduce an approved Figma frame or section accurately in Gutenberg. Use for Figma-to-WordPress implementation where visual fidelity is the goal.
---

# Figma to Gutenberg
Turn a node-specific Figma design into a responsive WordPress block-theme page. Optimize for three outcomes together: fidelity, editor usability, and development speed.

## Start with evidence

1. Read the repository instructions and inspect the active theme, templates, front-page setting, existing block patterns, CSS tokens, and plugins.
2. Fetch design context for the supplied Figma node before implementation. If the page is too large, use the returned layer IDs and fetch each major section separately.
3. Capture a full-page reference plus section screenshots at useful resolution. Record exact section heights, content widths, spacing, type sizes, colors, radii, shadows, copy, and assets.
4. Download exported Figma assets into the theme. Figma asset URLs expire, so never leave them as production dependencies.

## Choose the editing architecture

Prefer this split unless the project requires another approach:

- Use native core blocks for headings, paragraphs, buttons, lists, cards, links, columns, tables, and details/FAQ content.
- Use dedicated core Image (`core/image`) or Cover/Media & Text blocks for all images—never insert image tags, raw markup, or image links inside Paragraph blocks.
- Use native social blocks for social media elements, such as Social Icons (`core/social-links`) for profile links/sharing and native Embed blocks (`core/embed` or dedicated provider embeds) for social posts and feeds.
- Keep header and footer in template parts.
- Package the initial page as a block pattern and write its blocks into the actual front page, so editors can change content directly.
- Use a small dynamic block only when markup must be functional or intentionally protected, such as a domain-search form.
- Use theme-rendered graphic blocks for complex illustrations that editors should not modify.
- Use ACF only when structured data, validation, conditional fields, or repeated records provide a clear benefit. Do not introduce ACF solely to make ordinary text editable.

The page must remain understandable in List View. Give major groups human-readable `metadata.name` values such as “Hero” and “Domain pricing.”

## Implement accurately

1. Map Figma values to CSS custom properties and `theme.json` presets before styling individual sections.
2. Reproduce desktop dimensions first, then create responsive behavior from the design’s layout intent rather than scaling the whole page.
3. Keep editable copy in block attributes. Do not bake headings, descriptions, prices, or button labels into PHP or CSS.
4. Reuse exported images and icons. Set explicit dimensions to avoid layout shift. Store each editable or replaceable visual as a core Image block. For an icon beside copy, use a flex Group containing an Image block and a Paragraph or Heading block; never embed `<img>` or `<svg>` inside RichText markup. Reserve CSS backgrounds and pseudo-elements for decoration that editors should not select or replace.
5. Use semantic landmarks, one page-level `h1`, logical heading order, real links/buttons, visible focus states, useful form labels, and disclosure elements for FAQs.
6. Connect calls to action to existing project destinations. If a destination is unknown, use an explicit local anchor and document it instead of inventing an external URL.
7. Load fonts locally when licensing permits and include the license alongside the files.
8. When the design introduces a reusable Button treatment beyond WordPress's built-in Fill and Outline choices, register it as a named `core/button` block style in the Register.ly Blocks theme. Style its generated `is-style-*` class for both the editor and front end so clients can select and switch treatments from Gutenberg. Do not leave reusable button treatments as unexplained Additional CSS Classes, one-off inline styles, or selectors tied to page structure.

## Protect layout without harming editing

Use ordinary editable groups by default. Avoid locking the entire page during development because it slows iteration and hides structural problems.

## Verify

1. Run PHP and JavaScript syntax checks and validate block markup through WordPress.
2. Render the actual front page at the Figma desktop width and at mobile/tablet widths.
3. Open Gutenberg and confirm that representative headings, paragraphs, buttons, card copy, prices, and FAQ answers can be edited and saved. Confirm every custom button treatment is registered, named clearly in the Button Styles panel, selectable without editing class names, and visually consistent in the editor and front end. For icon-and-text rows, verify the icon and copy are separate selectable blocks and that editing the copy cannot remove the icon.
4. Test navigation, form validation, FAQ controls, keyboard focus, overflow, console errors, and reduced-motion behavior.
5. Keep a recoverable copy of the prior front-page content before replacing it.