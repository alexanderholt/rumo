# Editing .docx files: redlines and clean copies

Lessons from producing tracked-change redlines and accepted clean copies by editing `word/document.xml` directly. Read this before touching an existing .docx, especially one that came from a law firm.

## Rule 1: The clean copy is the accepted redline, never a separate file

Build the tracked redline first. Generate the clean copy by accepting every change programmatically (remove `w:del`, unwrap `w:ins`, drop paragraphs and rows whose marks are deleted). Never hand-build a clean copy alongside a redline; the two drift, and the founder ends up sending counsel a redline that does not accept to the document they approved.

Before delivering, run the accept step and diff its text against the intended clean text. This catches tracked deletions that stop short of the old text (half of a struck phrase surviving, a doubled party name, an orphaned word after an insertion).

## Rule 2: Deleting a whole paragraph means deleting its paragraph mark

Wrapping every run in `w:del` leaves an empty paragraph behind. On accept, a numbered list shows a stray "5." and a deleted appendix leaves an empty table. Add `<w:del>` inside `w:pPr/w:rPr` for every paragraph whose only content is deleted runs. For table rows, add `<w:del>` inside `w:trPr`. Word then removes them on accept, and the programmatic accept must do the same.

## Rule 3: Every inserted run needs explicit `w:rPr`

A run without `w:rPr` inherits the document defaults in `styles.xml`. That default often differs from the body text, so inserted text renders in the wrong font or size. Copy `w:rPr` from the adjacent run when splitting a run for a tracked edit; for new paragraphs or table rows, build the `w:rPr` explicitly (fonts, size, bold for label cells).

Paragraph marks matter too: list numbers and empty paragraphs render in the paragraph-mark font (`w:pPr/w:rPr`). Give them the same explicit fonts. If the body font differs from `docDefaults`, change `docDefaults` to the body font so nothing can fall back.

## Rule 4: Preserve edge whitespace

Any `w:t` or `w:delText` whose text starts or ends with a space needs `xml:space="preserve"`, or Word trims the space. Set it on every text node you create or touch.

## Rule 5: Unique `w:id` values

`w:ins` and `w:del` ids must be unique in the document. Read the current maximum and start a fresh block well above it (for example 901+, 1001+, 1201+ per editing pass) so later passes never collide.

## Rule 6: Law-firm template artifacts

- Document-management trailers (document ID numbers from systems like iManage) sit in footer text boxes. Strip them from the clean copy. Leave them in the redline, which is a comparison against the firm's original.
- Bracketed drafting instructions stay in a template and must be removed per counterparty.
- An empty paragraph that preceded a removed appendix can push a blank trailing page. Check the page count of the render.

## Rule 7: Verify by rendering, not by text extraction

`soffice --headless --convert-to pdf` then `pdftoppm -png` and look at the page images. Text extraction alone misses font-size problems, overlapping footers, blank pages, and stray list numbers. Text extraction also invents spacing artifacts that are not in the file; confirm against the XML before "fixing" them.

Also confirm the XML parses (lxml) and re-extract the tracked changes from the saved file to prove each edit landed where intended.

## Rule 8: The founder's open Word window

A `~$filename.docx` lock file next to the document means Word has it open. Edits written to disk are invisible in that window, and if the founder saves from Word the on-disk edit is overwritten. Never script Word to close or save. Tell the founder to close the document with Don't Save, wait for the lock file to disappear, then open the file again.

## Technique: surgical tracked edit inside a run

To delete or insert a phrase mid-run without disturbing the rest: split the run into before / target / after, each carrying a deep copy of the original `w:rPr`; wrap the target in `w:del` (converting `w:t` to `w:delText`) or place the new text in a `w:ins` run between the halves. Keep the counterparty's or counsel's wording where it can be preserved; reasoning goes in a comment or the matter log, not into strike-and-rewrite.
