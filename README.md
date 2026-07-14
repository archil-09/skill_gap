# Skill Gap — Resume Category Prediction & Skill Gap Analyzer

A Streamlit app that takes an uploaded resume (PDF, DOCX, or TXT), predicts the most likely job category using a trained ML classifier, and highlights which skills typically expected for that category are missing from the resume.
use this link to access https://skillga-vtn87igj9rd6towbxcap5x.streamlit.app/
## How it works

1. **Upload** — the user uploads a resume in `.pdf`, `.docx`, or `.txt` format.
2. **Text extraction** — the app pulls raw text out of the file (`PyPDF2` for PDFs, `python-docx` for Word files, plain decoding for text files).
3. **Cleaning** — the resume text is cleaned (URLs, hashtags, mentions, and punctuation stripped) and tokenized with NLTK, with stopwords removed.
4. **Category prediction** — the cleaned text is vectorized and passed to a pre-trained classifier (`clf.pkl` + `vectorizer.pkl` + label encoder `lc.pkl`) to predict the job category (e.g. Data Science, Java Developer, HR, Web Designing, DevOps Engineer, etc.).
5. **Skill extraction** — a keyword-matching pass scans the resume for a predefined list of known technical skills.
6. **Gap analysis** — the skills found in the resume are compared against a curated list of skills expected for the predicted category, and the missing ones are reported back to the user.

## Supported categories

The classifier covers roles including Data Science, HR, Advocate, Arts, Web Designing, Mechanical Engineer, Sales, Health and Fitness, Civil Engineer, Java Developer, Business Analyst, SAP Developer, Automation Testing, Electrical Engineering, Operations Manager, Python Developer, DevOps Engineer, Network Security Engineer, PMO, Database, Hadoop, ETL Developer, .NET Developer, Blockchain, and Testing.

## Tech stack

- **Streamlit** — web UI
- **scikit-learn** (pickled model) — resume category classification
- **NLTK** — tokenization and stopword removal
- **PyPDF2** — PDF text extraction
- **python-docx** — DOCX text extraction

## Project structure

```
skill_gap/
├── app.py              # Streamlit app entry point (UI + prediction + skill gap logic)
├── main.py              # (supporting script)
├── clf.pkl              # Trained classifier model
├── vectorizer.pkl        # Fitted text vectorizer
├── lc.pkl               # Label encoder for category names
├── requirements.txt      # Python dependencies
└── requirement.txt       # (duplicate/alternate requirements file)
```

## Getting started

### Prerequisites

- Python 3.8+

### Installation

```bash
git clone https://github.com/archil-09/skill_gap.git
cd skill_gap
pip install -r requirements.txt
```

The app will automatically download the required NLTK data (`punkt_tab`, `stopwords`) on first run.

### Running the app

```bash
streamlit run app.py
```

Then open the local URL Streamlit prints (typically `http://localhost:8501`) in your browser.

### Usage

1. Launch the app.
2. Upload a resume (PDF, DOCX, or TXT).
3. Optionally check "Show extracted text" to verify the parsed content.
4. View the predicted job category and the list of missing skills for that category.

## Notes

- Skill matching is keyword-based (substring match against a fixed skill list), so results depend on how skills are phrased in the resume.
- The required-skills mapping per category is a static, curated list defined in `app.py` and can be edited directly to add or adjust categories/skills.

## License

No license specified. Add a `LICENSE` file if you intend to make usage terms explicit.
