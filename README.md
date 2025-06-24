#  Automated Metadata Generator using Streamlit + OCR

Welcome to the **Automated Metadata Generator**, a powerful and intelligent web application built with Python and Streamlit. This tool is designed to automatically analyze documents (PDFs, DOCX, TXT) and extract **structured metadata** using a combination of **OCR** and **Natural Language Processing (NLP)**.

---

##  Project Objective

The goal of this application is to:
- Help users understand document content without reading entire files
- Support both digital and scanned documents
- Provide instant insights like title, summary, keywords, and named entities

Whether you're processing academic papers, invoices, resumes, or reports — this tool offers a quick, intelligent summary.

---

##  Key Features

| Feature | Description |
|--------|-------------|
|  Multi-format Input | Upload `.pdf`, `.docx`, or `.txt` files |
|  OCR Integration | Extracts text from **scanned PDFs** using `Tesseract OCR` |
|  Named Entity Recognition | Uses spaCy to detect people, locations, dates, organizations, etc. |
|  Summary Generator | Extracts and ranks the most important sentences |
|  Keyword Extractor | Uses TF-IDF to identify the most relevant terms |
|  Instant Web UI | Built with Streamlit for a fast, simple experience |

---

##  What Metadata is Extracted?

### 1.  Title  
The first meaningful line with sufficient content.

### 2.  Summary  
3 top longest or most informative sentences extracted from the document.

### 3.  Keywords  
Top 5 keywords determined using TF-IDF vectorization.

### 4.  Named Entities  
All named entities (like organizations, dates, people) extracted using spaCy's NER model.

---

##  Technologies Used

| Layer        | Tech Stack |
|--------------|------------|
| UI           | Streamlit |
| OCR Engine   | Tesseract OCR + pytesseract |
| PDF/Text Handling | PyMuPDF, pdf2image, python-docx |
| NLP          | spaCy, NLTK, scikit-learn |


##  Getting Started

### Run Locally

```bash
# Clone this repository
git clone https://github.com/WildArpit/Mars_project.git
cd Mars_project

# Install dependencies
pip install -r requirements.txt

# Ensure Tesseract OCR is installed:
# Windows: https://github.com/UB-Mannheim/tesseract/wiki
# Linux: sudo apt install tesseract-ocr
# macOS: brew install tesseract

# Start the app
streamlit run app.py
```

---

## ☁ Deploy on Render

1. Push the project to a **public GitHub repo**
2. Log into [Render.com](https://render.com) and create a new Web Service
3. Link your GitHub repository
4. Set **Start Command**:
   ```bash
   streamlit run app.py --server.port $PORT
   ```
5. Ensure your repo contains `render.yaml`:

```yaml
services:
  - type: web
    name: mars-metadata-app
    env: python
    buildCommand: |
      apt-get update && apt-get install -y tesseract-ocr poppler-utils
      pip install -r requirements.txt
      python -m nltk.downloader punkt
    startCommand: streamlit run app.py --server.port $PORT
```

---

##  Live Example Output

Here’s an example of what you get back after uploading a document:

```json
{
  "Title": "Artificial Intelligence in Modern Medicine",
  "Summary": "AI is transforming diagnostics and predictive analysis... This trend is expected to accelerate...",
  "Keywords": ["ai", "medicine", "diagnostics", "healthcare", "technology"],
  "Named Entities": {
    "ORG": ["WHO", "IBM"],
    "GPE": ["India", "United States"],
    "DATE": ["2023"]
  }
}
```

---

##  Future Enhancements

- [ ] Export metadata to JSON / CSV
- [ ] Upload multiple documents at once
- [ ] Add topic modeling (LDA)
- [ ] Add document-type classifier
- [ ] Add charts to visualize entity types

