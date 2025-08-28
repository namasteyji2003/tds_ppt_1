# Your Text, Your Style – Auto-Generate a Presentation

Turn bulk text or markdown into a fully formatted **PowerPoint** that matches an uploaded template’s look and feel. Bring your own LLM key (OpenAI, Anthropic, Gemini). No AI images—only reuses assets found in the template.

## ✨ Features
- Paste long-form text or markdown
- Optional one-line guidance (e.g., “turn into an investor pitch deck”)
- Use your *own* LLM API key (never stored or logged)
- Upload a `.pptx` or `.potx` template/presentation
- Intelligent slide count & content mapping
- Reuse images from the uploaded file; no generation
- Download a ready `.pptx`

## Quickstart
```bash
pip install -r requirements.txt
streamlit run streamlit_app.py
```
Open the browser link, paste text, choose provider/model, paste your API key, upload a template, and click **Generate Presentation**.

## Deploy (free options)
- **Streamlit Community Cloud**: New app → connect this repo → main file `streamlit_app.py`
- **Render/Heroku/Fly.io**: Use the included `Procfile` or create your own

## How it works (200–300 words)
The app converts long-form text into a slide deck in two stages: **structure** and **style**. First, the structure stage uses the selected LLM (OpenAI, Anthropic, or Gemini) with your supplied API key to transform the raw text into a JSON plan describing slides (title, 3–6 bullets, optional speaker notes). The prompt instructs the model to choose a reasonable slide count based on input length and guidance. If the LLM call fails or returns invalid JSON, a fallback splitter groups paragraphs into slides, ensuring the process is robust. Second, the style stage loads your uploaded PowerPoint file with `python-pptx`, preserving its theme, layouts, colors, and fonts. We start from the template, remove existing slides, and add new ones using best-effort matching: “Title and Content” when bullets exist, “Title Only” otherwise. Text is inserted into placeholders when found; if a content placeholder is missing, a text box is added at a reasonable position. To keep visuals consistent without generating new images, the app extracts images embedded in your template/presentation and reuses them sparingly (e.g., placing an illustrative asset at the bottom-right). Sensitive inputs—including API keys—are never stored or logged; keys live only in the client session during the request. The result is a `.pptx` that mirrors your template’s look and feel, ready for download.

## Configuration
- No server-side persistence. Do **not** log or store API keys.
- Reasonable size limits can be enforced via Streamlit config and reverse proxies.

## License
MIT — see `LICENSE`.
