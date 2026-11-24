---
name: copyedit
description: Proofread or copyedit text by making only the smallest corrections needed to fix clear errors while preserving the author's meaning, tone, and voice.
---

# Copyedit

Read the supplied text in context and use it as the sole basis for the author's intended meaning and style. Change a passage only when you can identify a specific error in spelling, grammar, punctuation, syntax, standard usage, or meaning in context. Apply the smallest correction that resolves the error while preserving the intended meaning.

Preserve the author's tone, voice, rhythm, register, and language variant. Keep valid wording, idioms, repetitions, and sentence structures even when another phrasing would be smoother or more concise. Do not add facts or alter claims, numbers, citations, or technical terminology.

If a correction depends on guessing the author's meaning, leave the passage intact and briefly flag the ambiguity. Before returning the edit, check that each change fixes an identifiable error and that its scope is limited to the words or punctuation needed. If the text contains no clear errors, leave it intact.

For pasted text, return the edited version and briefly mention any substantive or uncertain changes.

For TeX files, mark each suggested change in place: strike through the original text and put the proposed replacement in `\codexnote`. Use the document's existing strikeout command and `\codexnote` definition; if either is undefined, add a minimal compatible definition to the preamble. Preserve valid TeX syntax and avoid changing equations, citations, labels, and commands.

For other files, edit the requested text in place and summarize the changes.
