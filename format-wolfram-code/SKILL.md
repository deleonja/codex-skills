---
name: format-wolfram-code
description: Reformat Wolfram Language routines, public or private definitions, and general code in .wl and .wls files for readable algorithmic structure while preserving semantics. Use for style cleanup, pseudocode-like layout, indentation, spacing, or column-limit requests.
---

# Format Wolfram Code

Reformat only the requested scope. Inspect nearby code first and retain established
conventions unless the user asks to replace them.

## Preserve Meaning

- Treat formatting as semantics-preserving. Retain patterns, conditions,
  attributes, scoping, evaluation order, operator precedence, messages, and
  comments.
- Do not rename public symbols, correct spelling, change APIs, or replace an
  expression with a merely equivalent implementation unless requested.
- Introduce meaningful local variables only when they expose genuine algorithmic
  stages and their evaluation behavior remains unchanged.
- Preserve existing fold markers. Do not add new folds unless requested; when
  requested, use the `add-fold-markers` skill.

## Shape the Code

- Use the user's column limit. Otherwise infer the local limit, defaulting to 80
  columns when none is evident.
- Treat that limit as a ceiling, not an early wrapping target. Use the available
  width when a natural phrase or expression fits; unnecessarily short fragments
  compromise readability. Short lines are still appropriate at real structural
  boundaries.
- Make the routine read like pseudocode: one meaningful stage per statement,
  descriptive local names, and a blank line before the final result when it
  separates setup from output.
- Prefer the most compact readable form that fits the column limit. If an entire
  definition is clear on one line, keep its head and body on that line:
  `MatrixCommutator[A_, B_] := A . B - B . A`.
- Apply the one-line rule after accounting for indentation and any comments that
  must remain on the line. Do not split a definition merely to emphasize its
  body, make it visually match longer peers, or attach a fold marker.
- Do not staircase nested single-argument wrappers merely because they are
  nested. Keep a clear expression such as
  `N[Chop[Total[ck phases eigenvectors]]]` on one line when it fits.
- Break expressions where structure becomes easier to scan: long definition
  heads and conditions, multi-stage `Module` bodies, tables and iterators,
  matrices, associations, option sets, and long function arguments.
- Break a definition only when the complete line exceeds the limit or when
  multiline layout materially clarifies genuine internal stages, branching,
  iterators, structured data, or repeated subexpressions.
- Use consistent spaces after commas and around infix operators. Preserve
  meaningful Wolfram juxtaposition when it is clearer than explicit `Times`.
- Align indentation by syntactic nesting, not by visual columns. Follow the
  file's indentation width.

For `Module`, `Block`, and `With`, keep the local declaration with the
construct header when it fits. Put initialization and transformation stages on
separate lines, but keep compact final expressions compact.

## Public Definitions and Messages

- Preserve the evaluated string contents and escape sequences exactly, including
  intentional newlines between usage forms.
- Prefer one string literal with Wolfram's backslash-newline continuation when a
  literal needs source wrapping. Do not introduce `<>` solely to wrap prose.
  Keep `<>` when concatenation is semantically meaningful or already required
  by dynamic pieces.
- A backslash-newline removes only the physical newline. Wolfram retains spaces
  and tabs at the start of the continuation line as string content. Start
  continuation text at column 1 when indentation is not part of the intended
  output; do not indent it merely to align with surrounding code.
- Break near the column limit at natural phrase boundaries. Use the available
  width and avoid chains of short continued lines, while keeping long box-form
  escapes and usage signatures easy to recognize.
- Preserve an intentional displayed newline as a real newline in the literal or
  as `\n`; do not place a continuation backslash there.
- After editing, evaluate the old and new right-hand sides in isolation and
  compare the resulting strings exactly when the original is available.

## Verify

1. Review the diff for accidental refactors and unrelated changes.
2. Check every line in the requested scope against the column limit.
3. Run whitespace or repository checks when available.
4. When `wolframscript` is available, parse without evaluating package code:

   ```wl
   source = Import["path/to/file.wl", "Text"];
   ToExpression[source, InputForm, HoldComplete];
   ```

5. If the file contains fold markers, confirm that formatting preserved their
   whole-file balance and nesting.
