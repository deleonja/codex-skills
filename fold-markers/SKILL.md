---
name: fold-markers
description: Add or update manual code folding markers in source files, using valid comments for the file's language.
---

# Fold markers

Use this skill when asked to add or update manual fold markers in a code file. Markers must be comments and must not change how the file runs.

Use `{{{*` to open a fold and `*}}}` to close it. Write each marker using the file's valid comment syntax. For example:

- Makefile: `# {{{*` and `# *}}}`
- Wolfram Language: `(* {{{* *)` and `(* *}}} *)`
- LaTeX: `% {{{*` and `% *}}}`

Follow the file's structure and existing fold style. Add folds around meaningful blocks, such as configuration groups, functions, or major sections. Avoid folding every line or small statement.

When updating a file, preserve existing folds and content. Add or move markers only where needed.

For LaTeX, put each major section opener inline at the end of its `\section{...}` line, for example `\section{Introduction}% {{{*`. Put its closer on a line by itself immediately before the next peer section, or after the final section’s content. Apply the same rule to subsections: put the opener inline at the end of the `\subsection{...}` line and the closer alone immediately before the next peer subsection, or after the final subsection’s content. When the user has already adjusted markers in part of a file, use that area as the style reference for the rest, including inline placement and nested folds.

Check that every opener has a closer, folds are properly nested, and the diff contains only marker comments unless the user also requested code changes.
