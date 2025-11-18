## Smart Legal Assistant for Contract Analysis and Risk Assessment (SLA-CARA) 
- A lightweight AI assistant designed to help with contract review by breaking long agreements into understandable pieces, identifying key legal clauses, assessing risks, and extracting important details.
SLA-CARA uses a Retrieval-Augmented Generation (RAG) approach built specifically for legal text.
 - The goal is simple:
  - **Reduce manual effort and make contract understanding feel less overwhelming.**

### What SLA-CARA Does
SLA-CARA supports contract reviewers by automating four core legal analysis tasks:
**1. Clause Classification**
  - Identifies the type of clause from 25+ categories (Termination, Indemnification, Confidentiality, Governing Law, etc.).
**2. Clause Summarization**
  - Generates concise, easy-to-read summaries of long legal paragraphs.
**3. Risk Assessment**
  - Assigns a risk label (High, Medium, Low) and highlights which legal risk areas are involved.
**4. Key Legal Insights Extraction**
  - Pulls out Parties, Dates, Obligations, Entities, and other useful details.
**5. Contract Q&A**
  - Allows natural-language questions about a clause or full contract.
**This system is built for clarity, speed, and practical use, not to replace legal teams, but to support them.**

### Tech Stack
#### 1. Core AI & NLP
- Legal-BERT – legal domain embeddings
- FAISS – vector similarity search
- LLaMA 3.2 3B (API) – used for classification, summarization, Q&A, and risk interpretation
- CUAD Dataset – for benchmarking classification and clause-level evaluation
#### 2. Document Processing
- PDFMiner / PyPDF – extract text from contracts
- spaCy (en_core_web_md) – NER for dates, obligations, organizations, etc.
- Regex-based Clause Segmentation – splits contracts into meaningful legal units
#### 3. Backend & Application Layer
- FastAPI – main API layer
- Pydantic – input/output schema definitions
#### 4. Python & Machine Learning Ecosystem
- PyTorch – for model inference
- NumPy / Pandas – data handling
- Scikit-learn – evaluation metrics (accuracy, F1, etc.)
#### 5. Evaluation
- BLEU / ROUGE – summarization quality
- F1-score / Accuracy – clause classification
- Recall@k – retrieval evaluation

### How the System Works
The system follows a complete end-to-end pipeline:
**1. Document Processing**
Contracts (PDF/DOCX) are converted to text and split into clause-level chunks using regex + spaCy-based segmentation.
Entities (names, dates, obligations) are extracted using spaCy’s en_core_web_md.

**2. Embedding Creation**
Each clause is tokenized and converted into Legal-BERT embeddings using mean-pooled hidden states.
Embeddings are L2-normalized for consistent vector magnitude.

**3. Hybrid Retrieval (FAISS + Cosine Similarity)**
A FAISS vector index performs fast top-k retrieval.
Retrieved candidates are re-ranked using cosine similarity for better precision.

**4. LLM-Based Analysis (LLaMA 3.2 3B)**
Task-specific prompts are created for:
  - classification
  - summarization
  - risk scoring
  - entity extraction
Each prompt includes the input clause + retrieved context.
The LLAMA 3.2 3B API (Lambda Labs) generates structured JSON responses.

**5. Output Generation**
Responses are cleaned, formatted, and returned for UI/API consumption—either for a single clause or a full contract.

### What This Project Demonstrates
- End-to-end RAG pipeline for legal documents
- Hybrid retrieval system (FAISS + cosine re-ranking)
- Clause classification and summarization
- Risk analysis modeling
- Legal-BERT + LLaMA integration
- Working with long-form legal text
- FastAPI-based deployment

### Future Improvements
- Improve handling of rare clause types
- Expand risk categories
- Add multilingual support
- Integrate more datasets (SEC/EDGAR)
- Enhance chunking and normalization rules

