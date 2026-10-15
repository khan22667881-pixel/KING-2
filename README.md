# 📄 ATS Resume Checker

A Streamlit app that scores a resume for ATS (Applicant Tracking System) friendliness and suggests concrete improvements using Google's Gemini Flash model.

## Features
- Upload a resume as **PDF, DOCX or TXT**
- **ATS score (0-100)** = 40% rule-based checks + 60% Gemini review
- Rule-based checklist: contact info, standard sections, length, bullets, quantified results, action verbs, dates
- Gemini review: keyword relevance, content quality, ATS formatting
- Prioritised **improvements**, **missing keywords** and **before/after rewrite examples**
- Optional **job description** for a job-specific keyword match

## Project structure
```
app.py             # the Streamlit app
requirements.txt   # Python dependencies
README.md
```

## Run locally
1. Install Python 3.10+.
2. Get a free Gemini API key at https://aistudio.google.com/apikey
3. Install and run:
   ```bash
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
4. Provide your key, either way:
   - **Option A (recommended):** create `.streamlit/secrets.toml`
     ```toml
     GEMINI_API_KEY = "your-key-here"
     # GEMINI_MODEL = "gemini-3.7-flash"   # optional override
     ```
   - **Option B:** paste it into the sidebar when the app opens.
5. Start the app:
   ```bash
   streamlit run app.py
   ```

## Deploy on Streamlit Community Cloud
1. Push this project to a GitHub repository (never commit `secrets.toml`).
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app**, choose your repo, branch `main` and main file `app.py`.
4. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
5. Click **Deploy**. Your app gets a public `*.streamlit.app` URL.

## Configuration
| Setting | Where | Default |
|---|---|---|
| `GEMINI_API_KEY` | Streamlit secrets or env var | none (or enter in sidebar) |
| `GEMINI_MODEL` | Streamlit secrets or env var | `gemini-3.7-flash` |

If the model name is rejected, check the current list at https://ai.google.dev/gemini-api/docs/models and set `GEMINI_MODEL`.

## Limitations
- The score is an **estimate**; real ATS systems differ.
- Scanned / image-only resumes can't be read (the app tells you to export a text-based file).
- Resume text is sent to the Gemini API for analysis; the app does not store it.
- If you deploy publicly, your API key pays for everyone's usage. Consider quotas or asking users for their own key.# KING-2
