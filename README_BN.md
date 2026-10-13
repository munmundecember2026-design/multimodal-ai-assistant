# Prism AI — সহজ বাংলা Setup Guide

এই project-এ আছে:
- বাংলা/ইংরেজি AI chat
- ছবি বুঝে প্রশ্নের উত্তর
- PDF, DOCX ও TXT text extraction এবং document Q&A
- Voice input (browser microphone) ও browser speech output
- AI image generation integration
- PowerPoint (.pptx) generation
- Optional Veo video-generation integration

## 1) যা লাগবে
- Windows 10/11
- Python 3.11 বা 3.12 (recommended)
- VS Code
- Google AI Studio/Gemini API key: https://aistudio.google.com/app/apikey

কিছু API model, image/video generation বা quota তোমার account/region অনুযায়ী unavailable বা paid হতে পারে। API key থাকলেই প্রতিটি feature free হবে—এমন নয়।

## 2) Project folder খোলো
ZIP extract করে VS Code-এ `prism_ai` folder খুলবে। VS Code-এ Terminal → New Terminal।

```powershell
cd path\to\prism_ai
```

`path\to\prism_ai`-এর জায়গায় তোমার আসল folder path লিখবে। যদি Downloads-এ extract করো, উদাহরণ:

```powershell
cd "$HOME\Downloads\prism_ai"
```

## 3) Virtual environment তৈরি ও চালু করো (PowerShell)
প্রথমে:

```powershell
py -m venv myenv
```

তারপর:

```powershell
.\myenv\Scripts\Activate.ps1
```

যদি `running scripts is disabled` error আসে, শুধু বর্তমান terminal session-এর জন্য চালাও:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

এরপর আবার:

```powershell
.\myenv\Scripts\Activate.ps1
```

Alternative: VS Code terminal dropdown থেকে Command Prompt নির্বাচন করে চালাও:

```cmd
myenv\Scripts\activate.bat
```

## 4) প্রয়োজনীয় library install করো
Virtual environment চালু থাকা অবস্থায়:

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

প্রতিটি command আলাদা করে চালাবে। `cd`-এর সঙ্গে `python -m pip` একই লাইনে লিখবে না।

## 5) API key নিরাপদে রাখো
`.streamlit` folder-এর ভিতরে `secrets.toml.example` ফাইলটির copy করে নাম দাও `secrets.toml`। তারপর key বসাও:

```toml
GEMINI_API_KEY = "তোমার_আসল_API_KEY"
```

অথবা PowerShell-এ বর্তমান terminal-এর জন্য:

```powershell
$env:GEMINI_API_KEY="তোমার_আসল_API_KEY"
```

API key Python code-এ লিখবে না, screenshot/share করবে না, GitHub-এ `secrets.toml` upload করবে না। `.gitignore` ফাইলটি এটি আটকাতে সাহায্য করে।

## 6) App চালাও
Project folder-এর ভিতরে:

```powershell
python -m streamlit run app.py
```

Browser-এ local URL খুলবে, সাধারণত `http://localhost:8501`। বন্ধ করতে terminal-এ `Ctrl+C` চাপবে।

## 7) Model access error হলে
Model name environment variable দিয়ে বদলানো যায়। উদাহরণ:

```powershell
$env:GEMINI_TEXT_MODEL="তোমার account-এ উপলভ্য text model"
$env:GEMINI_IMAGE_MODEL="তোমার account-এ উপলভ্য image model"
$env:GEMINI_VIDEO_MODEL="তোমার account-এ উপলভ্য video model"
```

তারপর app আবার চালাও। Gemini model list ও API access দেখো: https://ai.google.dev/gemini-api/docs/models

## 8) Feature-গুলোর সীমা
- Scanned/image-only PDF থেকে text বের করতে OCR যোগ করতে হবে; বর্তমান prototype selectable text PDF-এর জন্য।
- Voice input browser microphone permission চায়। Voice output browser/OS-এ উপলভ্য voice ব্যবহার করে; সব device-এ বাংলা voice একই রকম নাও হতে পারে।
- Image generation model access ও quota আলাদা হতে পারে।
- Video generation (Veo) account access এবং billing চাইতে পারে; এটি guaranteed free নয়।
- PowerPoint layout basic template; পরে theme, ছবি, chart ও speaker notes যোগ করা যায়।
- এটি prototype; login, rate limits, file-size limits এবং production monitoring যোগ না করে confidential/public production service হিসেবে ব্যবহার কোরো না।

## 9) Free deployment: Streamlit Community Cloud
1. GitHub account-এ repository তৈরি করো।
2. `app.py`, `requirements.txt`, `.streamlit/config.toml`, `README_BN.md` এবং `.gitignore` upload করো। `secrets.toml` upload করবে না।
3. https://share.streamlit.io/ এ গিয়ে repository নির্বাচন করে `app.py` entrypoint দাও।
4. App settings → Secrets-এ নিচের মতো API key বসাও:

```toml
GEMINI_API_KEY = "তোমার_আসল_API_KEY"
```

5. Deploy করো। Free hosting-এ resource/sleep limits থাকতে পারে। Public app হলে অন্যরা API quota ব্যবহার করতে পারে; key ও quota সুরক্ষিত রাখো।

Official docs:
- https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app
- https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/secrets-management
- https://ai.google.dev/gemini-api/docs/get-started
- https://ai.google.dev/gemini-api/docs/image-generation
- https://ai.google.dev/gemini-api/docs/veo
