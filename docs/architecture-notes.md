# 🏗️ Technical Architecture Notes: Smart College AI RAG

This document details the backend processing pipelines, chunking models, retrieval algorithms, and frontend APIs implemented in the **Smart College AI Assistant**.

---

## 📂 System Architecture Overview

```
[Document Upload (PDF/TXT)] 
       │
       ▼
[Paragraph-Based Chunker] (600-1000 chars, 150-200 chars overlap)
       │
       ▼
[Indexed Local JSON DB (db.json)]
       │
       ▼
[TF-IDF Relevance Retriever] (Term Frequency / Inverse Document Frequency)
       │
       ├─────────────────────────────────┐
       ▼ (Valid context match)           ▼ (No match / Score = 0)
[synthesized grounded Q&A]        [Grounded Low-Confidence Fallback]
```

---

## ⚙️ Core Modules & Mechanics

### 1. Document Chunking Service (`backend/services/chunker.py`)
To prevent feeding large documents that exceed model contexts or contain irrelevant facts, files are segmented into overlapping text snippets:
*   **Chunk Size**: 600 to 1000 characters.
*   **Overlap**: 150 to 200 characters (retains context across boundaries).
*   **Virtual Pages**: For plain text note uploads without page markers, the chunker automatically calculates virtual page breaks based on word counts (approx. 300 words per page) to support citations.

### 2. TF-IDF Similarity Retrieval (`backend/services/retrieval.py`)
A lightweight, zero-dependency term-weighting vector ranker matching user questions to the active document's chunks:
*   **Stop-words Filter**: Removes English filler words (`the`, `is`, `at`, `which`, etc.) from the query.
*   **Term Frequency (TF)**: Calculates how many times query words appear in a chunk.
*   **Inverse Document Frequency (IDF)**: Calculates the log-ratio of total chunks inside the document containing the query words.
*   **Match Scoring**: Computes the dot product of `TF * IDF` weights. The top 3 highest-scoring paragraphs are returned as context.
*   **Low-Confidence Guardrail**: If the top score is `0.0` (i.e. no words overlap), the system flags low confidence, bypasses model queries, and returns a fallback answer: *"I could not find a confident answer in the uploaded notes."* This completely prevents hallucinations.

### 3. Multi-Provider AI Routing (`backend/services/ai.py`)
The system acts as a secure proxy API router supporting three operation modes:
1.  **Local Mode (Offline Heuristics)**: Default fallback. If no API keys are present, the system runs local heuristic engines to generate summaries, extract flashcards, compile quizzes, and reply to chat questions offline, guaranteeing the app works out-of-the-box.
2.  **Google Gemini API**: Queries `gemini-1.5-flash` using standard HTTP POST requests with a low temperature config (`0.1`) for strict note-adherence.
3.  **Groq API**: Queries `llama3-8b-8192` over standard Open-AI compatible endpoints.

### 4. Multimodal Speech Interfaces (`frontend/components.js`)
*   **Speech-to-Text (STT)**: Built on HTML5 `webkitSpeechRecognition`. Captures student voice queries, maps mic pulse animations, transcribes text, and auto-submits queries for a hands-free experience.
*   **Text-to-Speech (TTS)**: Built on HTML5 `window.speechSynthesis`. Vocalizes flashcards and AI bubbles locally in the student's browser without adding CPU load or bandwidth consumption to the server.

### 5. Client Key Storage & Security
*   **Storage**: API Keys are saved exclusively inside the user's browser `localStorage`.
*   **Transmission**: Passed securely via custom headers (`X-Gemini-Key` and `X-Groq-Key`) to API routes.
*   **Zero Logs Policy**: The server never logs, prints, or stores these key values.
