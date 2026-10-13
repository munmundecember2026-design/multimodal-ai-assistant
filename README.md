# Prism AI

Bilingual multimodal assistant prototype built with Streamlit and Google's Gemini API.

See [README_BN.md](README_BN.md) for the full Bangla setup, Windows PowerShell commands, API-key safety, features, troubleshooting, and deployment instructions.

Run locally:

```powershell
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

Set `GEMINI_API_KEY` in `.streamlit/secrets.toml` or as an environment variable. Never commit API keys.
