---
name: add-fold-markers
description: Add or repair balanced {{{* and *}}} folding markers in source and configuration files, including TeX, Wolfram Language, and Makefiles. Use when the user asks to organize code into editor-foldable structural regions.
---

# Add Fold Markers

1. Read the target file and inspect existing fold markers before editing.
2. Infer two local conventions from the file: which structural units become folds and how comments are written. Preserve existing placement and spacing. If there is no precedent, use the language native comment syntax.
3. Add folds only at the requested structural level. Put the opening marker on the unit header when that is valid; otherwise put it in an adjacent comment. Put the closing marker immediately before the next peer unit or the parent fold close/end.
4. Keep nested folds balanced in last-opened, first-closed order. Do not add folds to smaller constructs unless requested.
5. Preserve code behavior and formatting. Change only fold-marker comments unless the user also requests code changes.
6. Verify marker balance, nesting, and the final diff.

Use the literal marker text `{{{*` to open and `*}}}` to close. Adapt only its comment wrapper, for example `% {{{*` in TeX, `# {{{*` in a Makefile, or `(* {{{* *)` in Wolfram Language.

## Wolfram Language

- Do not add a dedicated fold to a definition whose complete code already fits
  readably on one line. Never expand a one-line definition merely to make it
  foldable. It remains covered by any enclosing section fold.
- For an ordinary multiline definition, put the opening marker immediately
  after `:=`: `function[args_] := (* {{{* *)`. If its body starts with
  `Module`, put `Module[` on the following line.
- For an ordinary immediate assignment, put the marker immediately after `=`.
- Use a named adjacent header only for a contiguous overload family (for
  example, `(* Pauli {{{* *)`) or a non-routine grouping fold.
- Treat contiguous definitions for the same symbol as one fold when they form
  one logical overload family. If overloads are separated by another definition,
  fold them separately; do not span an unrelated helper merely to group them.
- Close the fold directly after the definition or final contiguous overload,
  before the next peer definition.
- Validate both the edited region and the whole file. Check equal open/close
  counts and scan nesting depth from the start of the file so enclosing parent
  folds are not mistaken for an imbalance.

## LaTeX

- Put each major section opener inline at the end of its `\section{...}`
  line, for example `\section{Introduction}% {{{*`. Apply the same rule to
  `\subsection{...}` lines.
- Put the closer on a line by itself immediately before the next peer section
  or subsection, or after the final unit's content, keeping nested folds balanced.
- When the user has already adjusted markers in part of a file, use that area
  as the style reference for the rest, including inline placement and nesting.
