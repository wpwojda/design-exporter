# Design Token Exporter

A single-file, browser-based tool for building a project's design tokens — palette, type scales, spacing, padding, and radius — previewing them live, and exporting the same source of truth as CSS variables and a Tailwind config. Built for the design → development handover at the end of the design phase: no manual re-entry, no ambiguity about what a size or colour should be.

No build step, no dependencies to install, no account. It's one HTML file.

## Using it

Open the hosted version, or download `index.html` and open it in any modern browser — it works the same either way.

1. **Palette** — add colours and name them. Names using a `name-100` pattern group automatically into ramps. Mark one colour as **Btn** (the primary/button colour) and one as **Aa** (text) to drive the live preview.
2. **Typography** — pick heading and body fonts from the presets, or upload the project's own typefaces (`.woff2`, `.woff`, `.ttf`, `.otf`). Set a base size and modular ratio per viewport; desktop and mobile each have their own scale. Any step can be overridden by hand — overridden values are highlighted and can be reset back to the computed scale at any time. Line-height, letter-spacing, and text case are set per step, in `%` or `px`.
3. **Spacing, padding, radius** — comma-separated pixel scales with visual previews.
4. **Export** — the right-hand panel always shows the current output. Three formats: **CSS variables** (`tokens.css`), **Tailwind config**, and **Base styles** — a generated element layer (body, headings, body-text classes, and form elements) built from your tokens, intended as the starting point for a project's base stylesheet before it's wrapped and classified per house convention. Base styles can reference tokens as CSS custom properties (import `tokens.css` alongside) or as SCSS variables with the definitions included, for Sass-based theme pipelines (WordPress/Drupal). Copy, download the file, or use **Download all (zip)** to get everything plus a `/fonts` folder for any linked font files. With **Fluid `clamp()` sizing** on, every size exports as a `clamp()` that scales between your mobile and desktop values across the chosen viewport range.

## Things worth knowing

- **Autosave is local to your browser.** The tool saves your session to `localStorage` as you work, so a refresh or a closed tab loses nothing — but it does not sync between people or machines. To hand a setup to someone else (or move between computers), use **Save project**, which downloads a portable `.json`, and **Load project** on the other side. Treat the `.json` as the file of record for a project.
- **New project** clears the local autosave and starts fresh. Save first if you want to keep what's on screen.
- **Uploaded fonts** under 200 KB are embedded into `tokens.css` as base64 so the file is self-contained; larger files are linked instead and included in the zip download. A toggle on each font row switches between the two.
- **Deletions are undoable** for a few seconds via the toast that appears — there's no confirmation dialog, so watch for it.
- Font files you upload never leave your browser; nothing is sent to a server.

## Tech notes

Vanilla HTML/CSS/JS in one file. The only external requests are Google Fonts (the UI face and preset preview fonts) and the JSZip CDN (only needed for **Download all**), so an internet connection is expected but nothing else is. The UI itself runs on its own token system — a small CSS variable ramp for type sizes and control heights — because a design token tool ought to.

UI typeface: [Hanken Grotesk](https://fonts.google.com/specimen/Hanken+Grotesk) (SIL Open Font Licence).

## Contributing / issues

This is a small internal tool shared publicly in case it's useful. Bug reports are welcome via issues; it's maintained as time allows.
