# 🔐 AI-Powered PII Detection & Redaction System

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![NLP](https://img.shields.io/badge/NLP-spaCy%20%7C%20Transformers-green?style=for-the-badge)
![AI](https://img.shields.io/badge/AI-LLM%20Powered-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-purple?style=for-the-badge)
![Compliance](https://img.shields.io/badge/Compliance-GDPR%20%7C%20HIPAA-red?style=for-the-badge)

**An intelligent, hybrid AI system that automatically detects and redacts Personally Identifiable Information (PII) from documents and live audio conversations — combining the precision of rule-based pattern matching with the contextual intelligence of modern NLP.**

</div>

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Supported PII Types](#-supported-pii-types)
- [Input Formats](#-input-formats)
- [Tech Stack](#-tech-stack)
- [How It Works](#-how-it-works)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Use Cases](#-use-cases)
- [Compliance](#-compliance)

---

## 🧠 Overview

This project addresses one of the most critical challenges in modern data engineering — **protecting sensitive personal information at scale**. Whether processing scanned documents, PDFs, plain text files, or real-time audio conversations, this system intelligently identifies and redacts PII before it can be exposed or misused.

> *"This project taught me how to combine traditional NLP techniques with modern AI models to build a real-world privacy protection system that works across documents and live communication."*

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 📄 **Multi-Format Input** | Supports PDF, TXT, scanned images (OCR), and audio files |
| 🎙️ **Audio PII Detection** | Converts speech to text, then detects sensitive spoken content |
| 🔍 **Hybrid Detection** | Combines Regex (precision) + NLP/LLM (context-awareness) |
| ✂️ **Auto Redaction** | Masks or blacks out sensitive content in documents |
| 🔇 **Audio Silencing** | Silences or alerts when PII is detected in live calls |
| 🌐 **Domain-Aware** | Understands context — not just patterns |
| 📦 **Scalable Pipeline** | Designed to handle large volumes of documents |
| ✅ **Compliance-Ready** | Built with GDPR and HIPAA regulations in mind |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    INPUT LAYER                          │
│        PDF │ TXT │ Scanned Image │ Audio File           │
└────────────────────────┬────────────────────────────────┘
                         │
           ┌─────────────▼─────────────┐
           │     TEXT EXTRACTION       │
           │  PyPDF2 │ OCR │ STT API   │
           └─────────────┬─────────────┘
                         │
           ┌─────────────▼─────────────┐
           │    HYBRID PII DETECTION   │
           │                           │
           │  ┌──────────┐ ┌────────┐  │
           │  │  Regex   │ │  NLP   │  │
           │  │ Patterns │ │  LLM   │  │
           │  └────┬─────┘ └───┬────┘  │
           │       └─────┬─────┘       │
           │       PII Entities        │
           └─────────────┬─────────────┘
                         │
           ┌─────────────▼─────────────┐
           │   REDACTION / ALERTING    │
           │  Mask │ Blackout │ Silence │
           └─────────────┬─────────────┘
                         │
           ┌─────────────▼─────────────┐
           │    CLEAN OUTPUT           │
           │  Redacted Doc │ Safe Audio │
           └───────────────────────────┘
```

---

## 🔎 Supported PII Types

- 🪪 **Aadhaar Numbers** — Indian national identity numbers
- 🏦 **PAN Numbers** — Permanent Account Numbers (India)
- 📱 **Phone Numbers** — Mobile and landline formats
- 💳 **Credit/Debit Card Numbers** — All major card formats
- 📧 **Email Addresses**
- 🏠 **Physical Addresses**
- 👤 **Person Names** *(via NLP context detection)*
- 🏥 **Medical & Financial Information** *(via LLM understanding)*

---

## 📂 Input Formats

```
Documents          Audio
──────────         ──────────
 ✔ PDF              ✔ WAV
 ✔ TXT              ✔ MP3
 ✔ DOCX             ✔ Live Stream
 ✔ Scanned Images (OCR)
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Python 3.8+ |
| **PDF Extraction** | PyPDF2, pdfminer |
| **OCR (Scanned Docs)** | Tesseract OCR / pytesseract |
| **Speech-to-Text** | Google STT / Whisper API |
| **Pattern Matching** | Python `re` (Regex) |
| **NLP** | spaCy, HuggingFace Transformers |
| **LLM Integration** | OpenAI API / Local LLM |
| **Document Redaction** | PyMuPDF (fitz), ReportLab |
| **Audio Processing** | pydub, SpeechRecognition |

---

## ⚙️ How It Works

### Step 1 — Text Extraction
The system accepts multiple input formats. For PDFs, it uses **PyPDF2**. For scanned documents, **Tesseract OCR** converts images to machine-readable text. For audio files, a **Speech-to-Text** engine transcribes the spoken content.

### Step 2 — Hybrid PII Detection

```
Regex  →  Catches structured patterns (e.g., Aadhaar: \d{4}\s\d{4}\s\d{4})
  +
NLP/LLM →  Understands context (e.g., "my card number is..." even without fixed format)
  =
High Accuracy + Low False Positives
```

> **Why both?** Regex alone misses rephrased or context-dependent PII. LLMs alone can be slow and expensive. Together, they cover structured *and* unstructured sensitive data.

### Step 3 — Redaction
- **Documents:** Sensitive spans are masked with `[REDACTED]` or blacked out visually.
- **Audio:** Real-time detection triggers a silence/beep overlay or alerts the operator when PII is spoken.

---

## 📁 Project Structure

```
pii-detection-system/
│
├── extraction/
│   ├── pdf_extractor.py        # PDF text extraction
│   ├── ocr_extractor.py        # OCR for scanned docs
│   └── audio_transcriber.py    # STT for audio files
│
├── detection/
│   ├── regex_detector.py       # Rule-based PII patterns
│   ├── nlp_detector.py         # spaCy NER pipeline
│   └── llm_detector.py         # LLM-based context detection
│
├── redaction/
│   ├── doc_redactor.py         # Mask/blackout in documents
│   └── audio_redactor.py       # Silence/alert in audio
│
├── utils/
│   ├── config.py               # System configuration
│   └── logger.py               # Logging utilities
│
├── main.py                     # Entry point
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/pii-detection-system.git
cd pii-detection-system

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run on a document
python main.py --input sample.pdf --mode document

# 4. Run on an audio file
python main.py --input call_recording.wav --mode audio
```

---

## 🎯 Use Cases

- 📞 **Call Centers** — Prevent agents from accidentally logging customer card/ID numbers
- 🏥 **Healthcare** — Redact patient data from medical reports before sharing
- 🏦 **Banking & Finance** — Mask PAN/Aadhaar in KYC documents
- ⚖️ **Legal** — Anonymize sensitive information in case files
- 🔄 **Data Pipelines** — Scrub PII before feeding data into analytics systems

---

## ✅ Compliance

This system is designed to support compliance with:

| Standard | Coverage |
|---|---|
| **GDPR** | Right to erasure, data minimization, purpose limitation |
| **HIPAA** | PHI detection and redaction in medical documents |
| **India PDPB** | Aadhaar, PAN, and biometric data handling |

> The system is **domain-aware**, **scalable**, and **compliance-ready** — built to work reliably across both structured documents and unstructured real-world conversations.

---

<div align="center">

Made with ❤️ to protect privacy in the age of AI

</div>
<img width="1919" height="896" alt="image" src="https://github.com/user-attachments/assets/0118f664-4bda-44e1-96cc-013e22062e8c" />
