## Markdown Publication Steps

1. Generate HTML from Markdown, include OASIS css styles in header after the pandoc default styles:
```
pandoc -f gfm-tex_math_dollars-tex_math_gfm -t html --include-in-header markdown-styles-2025-template-dk.css -s -o jadn-v2.0.html jadn-v2.0.md
```
2. Generate Word doc from HTML using reference document:
```
pandoc -f html -t docx --reference-doc=oasis-reference.docx --metadata title="JADN Version 2.0" -o jadn-v2.0.docx jadn-v2.0.html
```
3. Print PDF from Word doc