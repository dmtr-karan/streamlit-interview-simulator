# Streamlit Interview Simulator

A minimal, recruiter-friendly Streamlit app that simulates a job interview using the OpenAI API.  
It guides the user through a brief setup, runs a short interview with streamed model responses, supports an immediate **Stop** control (button or **ESC**), and then generates structured feedback.

![Status](https://img.shields.io/badge/status-active-success)
![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Streamlit](https://img.shields.io/badge/Streamlit-1.37+-red)
![OpenAI](https://img.shields.io/badge/OpenAI-Chat_Completions-black)
![License](https://img.shields.io/badge/License-MIT-lightgrey)
![CI](https://github.com/dmtr-karan/streamlit-interview-simulator/actions/workflows/ci.yml/badge.svg)


---

## Features

- **Guided setup**: Candidate details + target role/company.
- **Interview chat**: OpenAI Chat Completions with streaming output.
- **Stop control**: Button on the UI + **ESC** key to halt generation mid-stream.
- **Early-stop rule**: If stopped **before any user message**, feedback will **not** be offered (by design).
- **Post-interview feedback**: Score (1–10) + concise feedback using a fixed format.

---

## Quick Start (Local)

1. **Clone** the repository and move into it.
2. **Create** and activate a Python 3.10+ environment.
3. **Set** your OpenAI key.

   **Windows (PowerShell):**
   ```bash
   setx OPENAI_API_KEY "sk-your-key"
   ```

   **macOS/Linux (bash/zsh):**
   ```bash
   export OPENAI_API_KEY="sk-your-key"
   ```

4. **Install** dependencies:
   ```bash
   pip install -r requirements.txt
   ```

5. **Run** the app:
   ```bash
   python -m streamlit run app.py
   ```

> The app reads `OPENAI_API_KEY` from env vars locally. In Streamlit Cloud, set it under **Advanced settings → Secrets**.

---

## Deployment (Streamlit Community Cloud)

1. Push this repo to **public GitHub** (required by Community Cloud).
2. Go to https://share.streamlit.io → **New app**.
3. Select your repo, branch (`main`), and file path (`app.py`).
4. **Advanced settings → Secrets**:
   ```ini
   OPENAI_API_KEY="sk-your-key"
   ```
5. Deploy. The app will build, then provide a shareable URL.

---

## Usage Notes (UX)

- The flow is: **Setup → Interview → Stop/Complete → Feedback**.
- **Stop**:
  - Click **Stop** (top-right) or press **ESC** to halt generation.
  - If Stop is pressed **before** the first user message, the interview ends and **no Feedback** option appears.
  - If Stop is pressed mid-answer, streaming stops and the session is marked complete.
- **Limits**: The interview accepts up to **5 user messages** in total.

---

## Configuration & Secrets

- **Local**: environment variable `OPENAI_API_KEY`.
- **Streamlit Cloud**: set `OPENAI_API_KEY` under **Advanced settings → Secrets**.
- The app **fails fast** with a clear error if the key is missing.

---

## Tech Stack

- **Frontend**: Streamlit  
- **LLM**: OpenAI Chat Completions API  
- **Language**: Python 3.10+  
- **State**: `st.session_state` (single-file prototype)

---

## Project Structure

```
.
├─ app.py                # Streamlit app (main entrypoint)
├─ requirements.txt      # Minimal, pinned dependencies
├─ .gitignore            # Keeps secrets & caches out of version control
├─ README.md             # Project documentation
├─ LICENSE               # MIT license
├─ tests/                # Smoke tests
│   └─ test_import.py
└─ .github/
    └─ workflows/
        └─ ci.yml        # GitHub Actions workflow (CI)
```


---

## Requirements

Minimal set for fast builds:

```txt
streamlit>=1.37
openai>=1.42
streamlit-js-eval>=0.1.7
```

> Add only what you actually import. Keeping this minimal improves reliability and cold-start time.

---

## Known Limitations / Future Considerations

- This is a lightweight prototype (no database, no authentication).
- Feedback is model-generated and non-deterministic.
- If you add embeddings, RAG, or vector search later, update `requirements.txt` accordingly and document the changes.

---

---

## Acknowledgments

This project originated as part of *The AI Engineer Course 2025: Complete AI Engineer Bootcamp (Udemy)*.  
It has since been refined and deployed independently, with added functionality and deployment polish for portfolio use.

---

## License

MIT — see `LICENSE`
