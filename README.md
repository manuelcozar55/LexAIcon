<div align="center">

<!-- HEADER -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a2744,100:0f1a2e&height=200&section=header&text=LexAIcon&fontSize=56&fontColor=58A6FF&animation=fadeIn&fontAlignY=40&desc=AI-Powered%20Legal%20Text%20Intelligence%20%7C%20RAG%20%2B%20LLM%20Fine-Tuning&descAlignY=62&descSize=16&descColor=8b949e" width="100%" />

<!-- BADGES -->
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![RAG](https://img.shields.io/badge/RAG-Pipeline-0052CC?style=for-the-badge&logoColor=white)](#architecture)
[![Fine-Tuning](https://img.shields.io/badge/LLM-Fine--Tuning-FF6B6B?style=for-the-badge&logoColor=white)](#fine-tuning)
[![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co)
[![License](https://img.shields.io/badge/License-Apache%202.0-green?style=for-the-badge)](LICENSE)
[![Google Colab](https://img.shields.io/badge/Google_Colab-Ready-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com)

<br/>

> **LexAIcon makes the law understandable for everyone.**
> An AI system that translates, summarizes, and explains legal documents in plain language —
> combining RAG pipelines and custom fine-tuned LLMs trained on real Spanish legal data.

<br/>

[![Open Main Notebook](https://img.shields.io/badge/▶_Open_LexAIcon.ipynb-Run_in_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/manuelcozar55/LexAIcon/blob/main/LexAIcon.ipynb)
[![Open Fine-Tune Notebook](https://img.shields.io/badge/▶_Open_Fine--Tuning.ipynb-Run_in_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/manuelcozar55/LexAIcon/blob/main/FTLexAIcon.ipynb)

</div>

---

## ⚖️ The Problem

Legal language is intentionally complex. A standard traffic fine, a lease clause, or a public complaint form can be incomprehensible to non-lawyers — even in your native language. In Spain alone, millions of citizens interact with legal documents every year without understanding their full implications.

**LexAIcon bridges that gap with AI.**

---

## 🎯 What It Does

| Capability | Input | Output |
|------------|-------|--------|
| **Translate** | Legal jargon in any register | Plain-language equivalent |
| **Summarize** | Full legal documents | Concise, actionable summary |
| **Explain** | Specific clauses or terms | Step-by-step explanation with context |
| **Answer** | Questions about legal content | Grounded answers via RAG (no hallucination) |

---

## 🏗️ Architecture

LexAIcon combines two complementary AI approaches for maximum accuracy:

```mermaid
flowchart TD
    A(["📄 Legal Document"]) --> B & C

    subgraph RAG["🔍 RAG Pipeline"]
        B["Document chunks\n+ embeddings + retrieval"] --> D["Vector Search\nFAISS"] --> E["Grounded QA\nno hallucination"]
    end

    subgraph FT["🧠 Fine-Tuned LLM"]
        C["Spanish Legal Corpora\ndenuncias · multas · admin law"] --> G["Domain-Adapted Response\nMLM fine-tuning"]
    end

    E --> OUT(["📤 Plain-Language Answer"])
    G --> OUT

    style A fill:#1a2744,stroke:#58A6FF,color:#fff
    style B fill:#1f2937,stroke:#58A6FF,color:#ccc
    style D fill:#1f2937,stroke:#58A6FF,color:#ccc
    style E fill:#1f2937,stroke:#3fb950,color:#ccc
    style C fill:#1f2937,stroke:#FF6B6B,color:#ccc
    style G fill:#1f2937,stroke:#FF6B6B,color:#ccc
    style OUT fill:#0d2818,stroke:#3fb950,color:#fff
    style RAG fill:#0f1a2e,stroke:#58A6FF,color:#58A6FF
    style FT fill:#1a0f1a,stroke:#FF6B6B,color:#FF6B6B
```

### Why both RAG and Fine-Tuning?

| Approach | Strength | Used for |
|----------|----------|----------|
| **RAG** | Grounded in source documents, no hallucination | Q&A on specific documents provided by user |
| **Fine-Tuning** | Domain vocabulary, Spanish legal register | Style adaptation, term explanation, summarization |

Using only fine-tuning risks outdated knowledge. Using only RAG lacks legal domain fluency. **LexAIcon uses both.**

---

## 📦 Dataset

The models were trained and evaluated on **real Spanish legal data**:

| File | Content | Records |
|------|---------|---------|
| `denuncias.json` | Police complaints and incident reports (Zaragoza) | ~N complaints |
| `multas_zgz.json` | Municipal traffic fines (Zaragoza) | ~N penalties |
| `MLM_Fine_tunned/` | Masked Language Modeling fine-tuned model artifacts | — |

> **Why Zaragoza data?** Proximity to real, local, verifiable ground truth — not synthetic data. This grounds the model in actual administrative and legal language used in Spanish public institutions.

---

## 🚀 Quick Start

### Option A — Google Colab (recommended, no setup needed)

| Notebook | Purpose |
|----------|---------|
| [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manuelcozar55/LexAIcon/blob/main/LexAIcon.ipynb) **LexAIcon.ipynb** | Main demo: translate, summarize, explain |
| [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/manuelcozar55/LexAIcon/blob/main/FTLexAIcon.ipynb) **FTLexAIcon.ipynb** | Fine-tuning pipeline with your own data |

### Option B — Local

```bash
git clone https://github.com/manuelcozar55/LexAIcon.git
cd LexAIcon
pip install transformers datasets torch accelerate faiss-cpu langchain
jupyter notebook LexAIcon.ipynb
```

---

## 💬 Example Outputs

**Input** (original legal text):
```
"El expediente sancionador incoado al amparo del artículo 91.2 del Real Decreto
Legislativo 6/2015, de 30 de octubre, por el que se aprueba el texto refundido de
la Ley sobre Tráfico..."
```

**LexAIcon output** (plain language):
```
Se ha abierto un procedimiento sancionador contra usted por una infracción
de tráfico. Según la ley española de tráfico (artículo 91.2), usted tiene
derecho a presentar alegaciones en un plazo de 20 días naturales.

En resumen: le han puesto una multa y puede recurrir en 20 días.
```

---

## 📁 Project Structure

```
LexAIcon/
├── LexAIcon.ipynb          # Main notebook — full pipeline demo
├── FTLexAIcon.ipynb        # Fine-tuning notebook (MLM + instruction tuning)
├── MLM_Fine_tunned/        # Saved fine-tuned model artifacts
├── denuncias.json          # Training data: police complaints
├── multas_zgz.json         # Training data: municipal fines (Zaragoza)
└── LICENSE                 # Apache 2.0
```

---

## 🔑 Technical Highlights

- **Masked Language Modeling (MLM) fine-tuning** on Spanish legal corpus to adapt base model vocabulary to legal register
- **RAG implementation** using document chunking, embedding, FAISS vector search, and retrieval-augmented generation
- **Real-world data**: trained on actual municipal and administrative records from Zaragoza public datasets
- **Bilingual capability**: handles both Spanish legal text and plain-language explanations
- **Google Colab compatible**: full pipeline runnable without local GPU

---

## 🗺️ Roadmap

- [ ] Web interface (Streamlit / Gradio demo)
- [ ] Support for EU-level legal documents (GDPR, DORA)
- [ ] Multi-document cross-referencing
- [ ] API endpoint for integration with legal tools
- [ ] Expanded dataset with national legislation

---

## 👤 Author

**Manuel Antonio Cózar Baranguán**
*AI Engineer & Innovation Researcher*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-@manuelcozarb-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/manuelcozarb)
[![GitHub](https://img.shields.io/badge/GitHub-@manuelcozar55-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/manuelcozar55)
[![Email](https://img.shields.io/badge/Email-manuelcozarb@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:manuelcozarb@gmail.com)

---

<div align="center">

*Making the law legible — one document at a time.*

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f1a2e,60:1a2744,100:0d1117&height=100&section=footer" width="100%" />

</div>
