## Markdown Publication Steps

1. Generate HTML from Markdown, include OASIS css styles in header after the pandoc default styles:
```
pandoc -f gfm-tex_math_dollars-tex_math_gfm -t html --include-in-header markdown-styles-2025-template-dk.css -s -o jadn-v2.0.html jadn-v2.0.md
```
2. Print HTML from browser as PDF.  Custom margins 0 left/right, custom 90% scale.

### Alternate: Create Word Doc then Print PDF

2a. Generate Word doc from HTML using reference document:
```
pandoc -f html -t docx --reference-doc=oasis-reference.docx -o jadn-v2.0.docx jadn-v2.0.html
```
Then perform much manual editing.

or:

2b. Upload HTML to Google Drive, Open With Google Docs, Download as Word*

3. Print PDF from Word doc
