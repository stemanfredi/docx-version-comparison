# DOCX Version Comparison

Professional DOCX comparison tool using Pandoc + Python HTML diff.

## Principles

- **DRY** - Don't Repeat Yourself
- **KISS** - Keep It Simple
- **YAGNI** - You Aren't Gonna Need It
- **Specs First** - Update this file before writing code
- **Less is more** - Best code is no code

## Architecture

Google Colab notebook with 2 cells:

| Cell | Title | Purpose |
|------|-------|---------|
| 1 | Setup | Install pandoc, define functions |
| 2 | Compare | Upload files, diff, preview, download |

### Cell Patterns

**Cell 1 - Setup:**
```python
#@title 1. Setup
# apt install pandoc
# Imports: lxml, subprocess, base64, pathlib, tempfile
# Define: convert_docx_to_html(), diff_html(), embed_images(), inject_css()
# End with: print("Ready!")
```

**Cell 2 - Compare:**
```python
#@title 2. Compare Documents
# Upload 2 DOCX files
# Validate extensions
# Convert both to HTML (pandoc --extract-media)
# Diff with lxml.html.diff.htmldiff
# Embed images as base64 for portability
# Inject CSS (legal blackline style)
# Display preview in IFrame (images won't render)
# Download button for full HTML
```

## Structure

```
project/
├── notebook.ipynb   # Main Colab notebook
├── CLAUDE.md        # This file
└── README.md        # User documentation
```

## Commits

Format: `type(scope): description`

Types: feat, fix, docs, refactor, test, chore

Rules: ≤50 chars, lowercase, no period, imperative mood

---

## Specs

### Environment
- **Platform**: Google Colab (Linux)
- **Dependencies**: lxml (pre-installed in Colab)
- **System tools**: pandoc (apt)
- **GPU**: Not required

### Input
- **Formats**: .docx only
- **Validation**: Check file extension, check pandoc succeeds
- **Never overwrite source files**

### Processing
1. User uploads two .docx files (Version A, Version B)
2. Pandoc converts each to HTML, extracting media to temp dir
3. `lxml.html.diff.htmldiff(html_a, html_b)` produces diff with `<ins>`/`<del>` tags
4. Find all `<img src="...">` tags, replace with base64 data URIs
5. Prepend CSS stylesheet (legal blackline style)
6. Wrap in complete HTML document

### Output
- **Format**: Single portable HTML file with embedded images
- **Naming**: `diff_{file_a}_{file_b}.html`
- **Preview**: IFrame in notebook (images may not render)
- **Download**: Full HTML file via `google.colab.files.download()`

### CSS Style (Legal Blackline)
```css
body { font-family: -apple-system, sans-serif; max-width: 900px; margin: 40px auto; line-height: 1.6; padding: 20px; color: #333; }
ins { background: #e6ffed; color: #22863a; text-decoration: none; }
del { background: #ffeef0; color: #cb2431; text-decoration: line-through; }
img { max-width: 100%; height: auto; }
table { border-collapse: collapse; width: 100%; }
td, th { border: 1px solid #ddd; padding: 8px; }
```

### Error Handling
- Validate .docx extension before processing
- Catch pandoc errors, show stderr
- Handle missing images gracefully (skip embed, leave path)

---

## Tasks

### Current

### Backlog

### Done
- [x] Initial spec
- [x] Finalize architecture (2-cell, pandoc+lxml, base64 images)
- [x] Create notebook with 2-cell structure
