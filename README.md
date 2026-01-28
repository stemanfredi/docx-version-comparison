# DOCX Version Comparison

Compare two Word documents and generate a visual diff report.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/stemanfredi/docx-version-comparison/blob/main/notebook.ipynb)

## Usage

1. Open `notebook.ipynb` in Google Colab
2. Run **Cell 1** (Setup) - installs pandoc
3. Run **Cell 2** (Compare) - upload two `.docx` files
4. Preview the diff in-notebook, then download the HTML report

## Output

Single HTML file with:
- Insertions highlighted in green
- Deletions highlighted in red with strikethrough
- Images embedded as base64 (works offline)

## How It Works

1. Pandoc converts both DOCX files to HTML
2. `lxml.html.diff` computes structural diff
3. Images are embedded as base64 data URIs
4. CSS styles the result as a "legal blackline"

## Requirements

- Google Colab (or local Jupyter with pandoc installed)
- Two `.docx` files to compare

## License

MIT
