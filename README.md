# Legal Check

> AI-powered legal document analyser — upload any contract, agreement, or form and get an instant, plain-language breakdown of risks, duties, missing terms, and negotiation leverage — before you sign.

---

## What It Does

Legal Check is a multi-agent Streamlit application that reads legal documents and surfaces everything that matters to you — in plain language, no legal background required.

Upload a PDF, DOCX, or TXT file and five autonomous AI agents run immediately:

| Agent | What It Does |
|---|---|
| **Analysis Agent** | Reads the full document and returns a structured report: summary, risks, duties, fraud check, tampering check, missing terms, and a sign / don't sign verdict |
| **Power Position Agent** | Scores who holds more power in the agreement (0–100), maps one-sided obligations, and gives concrete walk-away points and negotiation tactics |
| **Chat Agent** | Lets you ask questions or run what-if scenarios grounded strictly in the document |
| **Courtroom Agent** | Acts as your personal defence attorney across three sample legal cases — always argues in your favour |
| **Form Filler Agent** | Analyses any form and produces a step-by-step guide showing exactly what to enter in each field, with direct quotes from the document as evidence |

---

## Features

**Full Analysis tab**
- Document summary in plain language
- Risk list with severity levels (High / Medium / Low)
- Duties for both parties
- Fraud and tampering check
- Missing Terms flag (missing refund policy, dispute resolution, etc.)
- Final verdict with confidence score
- Favourability Map — which clauses favour which party
- When the Risk Might Occur — 5 real-world scenario simulations
- Better Terms — top 5 clauses to renegotiate with ready-to-send messages
- Truth Check — hidden charges, APR accuracy, zombie fee detection
- Protection from Losing — prepayment penalty and foreclosure analysis
- Error Finder — LC discrepancy detection (UCP 600)
- Conflict Detector — co-lending structure compliance
- Clause Rewriter — pick any risky clause, get 3 rewritten versions
- One-page PDF summary download

**Power Position tab**
- 0–100 power score with colour-coded indicator
- Shared duties, one-sided obligations, hidden strengths
- Walk-away points with fallback strategies
- How to negotiate section

**Ask the Document tab**
- Conversational Q&A grounded in the document
- What-if scenario simulation
- Suggested starter questions

**AI Courtroom tab**
- Three pre-loaded sample cases: theft (IPC 379), wrongful termination (ID Act 1947), cyber access (IT Act 2000)
- AI defence attorney persona — always argues in your favour
- Bilingual (English / Hindi)

**Form Filler tab**
- Upload any form separately from the main document
- Agent extracts only fields that are actually present in the document
- Every field includes an exact quote from the document as evidence

**Language support**
- Full English and Hindi interface — switch at any time from the sidebar

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit |
| AI Model | `llama-3.1-8b-instant` via Groq API |
| Document Parsing | PyMuPDF (`fitz`), python-docx |
| PDF Generation | ReportLab |
| Language | Python 3.10+ |

---

## Project Structure

```
legal-check/
├── app.py                  # Main Streamlit UI — all 5 tabs
├── agent.py                # Orchestrator — imports and re-exports all agents
├── agent_analysis.py       # Analysis Agent — core report + 8 advanced modules
├── agent_leverage.py       # Power Position Agent
├── agent_chat.py           # Chat Agent — Q&A and scenario simulation
├── agent_courtroom.py      # Courtroom Agent — defence attorney chatbot
├── agent_formfill.py       # Form Filler Agent
├── document_parser.py      # PDF / DOCX / TXT text extraction
├── prompts.py              # All bilingual prompt templates
├── requirements.txt        # Python dependencies
└── .env                    # Your API key (never commit this)
```

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Sushmaa2407/legal-check.git
cd legal-check
```

### 2. Create a virtual environment

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up your Groq API key

Create a `.env` file in the root of the project:

```
GROQ_API_KEY=your_groq_api_key_here
```

Get your free API key at [console.groq.com](https://console.groq.com).

### 5. Run the app

```bash
streamlit run app.py
```

The app will open at `http://localhost:8501`.

---

## requirements.txt

Make sure your `requirements.txt` contains at least the following:

```
reportlab
streamlit>=1.35.0
groq>=0.9.0
pymupdf>=1.24.0
python-docx>=1.1.0
python-dotenv>=1.0.0
```

---

## Environment Variables

| Variable | Required | Description |
|---|---|---|
| `GROQ_API_KEY` | Yes | Your Groq API key from console.groq.com |

Never commit your `.env` file. Add it to `.gitignore`:

```
.env
```

---

## Rate Limits

This project uses Groq's free tier by default (`llama-3.1-8b-instant`). The pipeline runs 10 sequential agent calls per document. To avoid hitting rate limits, pauses of 8–10 seconds are built in between calls. If a 429 error occurs, the app automatically retries after 30 seconds.

For production use, consider upgrading to a paid Groq plan or adding your own retry logic in `agent_analysis.py`.

---

## Supported File Types

| Format | Support |
|---|---|
| PDF | Full text extraction via PyMuPDF |
| DOCX | Full text extraction via python-docx |
| TXT | Direct UTF-8 read |

Scanned PDFs (image-only) are not supported — the document must contain selectable text.

---

## Disclaimer

Legal Check is for **informational purposes only**. It is not a substitute for advice from a qualified legal professional. Do not make legal or financial decisions based solely on the output of this tool. Always consult a licensed lawyer before signing any legal document.

---

## Screenshots

<img width="1846" height="781" alt="image" src="https://github.com/user-attachments/assets/9885e487-7b88-476b-a29f-2e7c7f971ae2" />
<img width="1829" height="842" alt="image" src="https://github.com/user-attachments/assets/800d4597-d93b-4044-8c9e-3df891a3de11" />
<img width="1864" height="810" alt="image" src="https://github.com/user-attachments/assets/a9fefdd0-87d9-4d6e-840c-4b303e24c90b" />
<img width="1822" height="832" alt="image" src="https://github.com/user-attachments/assets/1f584007-6a5d-4713-bd22-e1f4ba502282" />
<img width="1843" height="774" alt="image" src="https://github.com/user-attachments/assets/2044fc49-d495-40f0-8cde-34b4e3f95ef6" />
<img width="1833" height="796" alt="image" src="https://github.com/user-attachments/assets/dcd472be-ef24-4e94-873f-8042a6e52d90" />

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add your feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

---


## Author

Built by **Sushma**

- GitHub: https://github.com/Sushmaa2407


---

*Powered by Groq · llama-3.1-8b-instant*
