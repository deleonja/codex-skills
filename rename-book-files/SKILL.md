---
name: rename-book-files
description: Rename book files in PDF or DjVu format in a directory and its subdirectories, verifying bibliographic details against the document and internet sources.
---

# Rename book files

When asked to rename books in a directory, recursively find its PDF and DjVu files and rename the books without asking for extra instructions.

For each file:

1. Identify books from the document. Exclude course notes, exams, solution manuals, and other supplements.
2. Inspect the title page and copyright or publication page. Use OCR if needed. Filenames, embedded metadata, and file timestamps are clues, not proof.
3. Verify the title, author surnames, edition, volume, and year against an internet source. Prefer the publisher; otherwise use a reliable library catalog. Check that the source describes the edition present in the file. Do not rely on search snippets alone. If the document and source conflict or a detail cannot be verified, leave that file unchanged and report the uncertainty.
4. Rename confirmed books using this format, with no spaces and only author surnames:

   `Author_Surnames-Book_Title-Edition-Volume-Year.ext`

   Omit inapplicable fields. Write editions as `2ed`, volumes as `Vol1`, and transliterate accented characters to plain ASCII. Keep the original extension.
5. Check all proposed names for collisions and existing files before changing anything. Then rename the confirmed books, preserving their contents.

Report the old and new names, cite the internet sources used, and list any book files left unchanged with the reason.
