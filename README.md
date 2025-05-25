# 🩺 Sano: Health Claim Fact-Checker

A prototype built for the **Pristina Healthcare Hackathon 2025**, addressing the challenge 🎯 **“Digital Health Literacy: Empowering Smart Choices”** proposed by **TUM**.  
🔗 [Challenge Description](https://pristina.innovate.healthcare/challenges/)

---

## 🚀 Project Overview

In a world flooded with health advice online, people like Nora — a busy parent looking for help — often end up confused or misinformed. Sano NLP aims to solve this by providing a simple and explainable tool that checks whether health claims are supported by evidence-based sources like **Mayo Clinic**, **PubMed**, and **WHO**.

By analyzing health claims, highlighting suspicious keywords, and comparing them to a trusted corpus, Sano NLP delivers a verdict:  
✅ **Trusted** | ⚠ **Unclear** | ❌ **Risky** — to help users make **smart, informed decisions.**

---

## 🧠 Features

### 📰 Load and Clean Corpus
- Loads 1,000+ Mayo Clinic health articles (`mayo_corpus.json`)
- Cleans raw HTML and extracts readable medical content using `BeautifulSoup`

### 🧬 Biomedical Embeddings
- Uses [`pritamdeka/BioBERT`](https://huggingface.co/pritamdeka/BioBERT-mnli-snli-scinli-scitail-mednli-stsb) via `sentence-transformers`
- Converts both the health claims and corpus into 768-dimensional vectors for comparison

### 🔍 Qdrant Semantic Search
- Vector search engine (`QdrantClient`) indexes and retrieves top-k most relevant articles based on cosine similarity
- Fast, memory-efficient, and supports payload filtering

### 🧼 Claim Analysis Engine
- Preprocesses user claim using `spaCy`: tokenization, stopword removal, lemmatization
- Flags suspicious health keywords (e.g., *detox*, *miracle*, *guaranteed*) that often appear in misinformation
- Identifies named entities (e.g., DISEASE, DRUG, TREATMENT)

### 🧠 Verdict Classifier
- Scores from semantic similarity are interpreted into:
  - **Trusted** (score ≥ 0.7)
  - **Unclear** (0.5 ≤ score < 0.7)
  - **Risky** (score < 0.5)

---

## 🧪 Example Output

**Claim Input**:  
> “Simply exposing your spine to sunlight for 15 minutes resets your DNA and eliminates chronic diseases...”

**System Output**:
- ✅ Claim analyzed and embedded
- ⚠ Detected suspicious word: `detox`
- 🔍 Top 5 matches retrieved from Mayo Clinic
- 🧠 Verdict: **Unclear**

---

## 🛠️ Tech Stack

- **Python 3.8+**
- **sentence-transformers** – BioBERT embeddings for semantic similarity
- **Qdrant** – Vector search engine for document retrieval
- **spaCy** – NLP preprocessing (tokenization, NER, lemmatization)
- **BeautifulSoup** – HTML cleaning
- **Mayo Clinic Corpus** – Trusted medical content for baseline verification

---

## 📁 Project Structure

| File               | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `Sano_NLP.ipynb`   | Main notebook containing the full prototype pipeline                        |
| `mayo_corpus.json` | Cleaned JSON corpus of Mayo Clinic articles (required for local inference)  |

---

## 📌 Future Directions

- 🌐 Add multilingual support (e.g., German, Albanian)
- 📊 Add explainable scores for trust and risk
- 🤖 Integrate with Chat interfaces or WhatsApp bot
- 🔬 Expand corpus with PubMed abstracts, WHO guidelines
- 📱 Turn into a mobile or web app (e.g., via Streamlit or Flask)

---

## 🎓 Hackathon Challenge Summary

**Challenge Title**: *Digital Health Literacy: Empowering Smart Choices*  
**Provided by**: [Technical University of Munich (TUM)](https://www.tum.de/en/)  
**Challenge Description**:  
Design an engaging and accessible solution that helps individuals improve their digital health literacy.  
Equip people like **Nora** — a working mother overwhelmed by online misinformation — with a tool they can **trust**.  
Full description: [https://pristina.innovate.healthcare/challenges/](https://pristina.innovate.healthcare/challenges/)

---

## 🧾 Acknowledgments

Built by **Ayusee Swain** at the **Pristina Healthcare Hackathon 2025**.  
Thanks to the mentors, healthcare experts, and challenge partners from TUM for their guidance and support.
