# AI Chatbot for Live Document Insights

This repository showcases **Sofia**, an Azure-based AI chatbot developed during my internship at Path Infotech to streamline access to policy documents and HR guidelines. It demonstrates the end-to-end pipeline from document ingestion and semantic indexing to conversational Q&A with inline citations.

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Key Features](#key-features)
3. [Architecture](#architecture)
4. [Workflow](#workflow)
5. [Frontend Details](#frontend-details)
6. [Backend Details](#backend-details)
7. [Deployment Guide](#deployment-guide)
8. [Usage](#usage)
9. [Contributing](#contributing)

---

## 🖥 Project Overview

Sofia is an AI-driven chatbot designed to answer natural-language questions over internal PDF policy documents in **real time**, complete with accurate citations. It leverages Microsoft Azure’s AI services—OpenAI for language understanding and Azure Cognitive Search for semantic retrieval—combined with a user-friendly web interface for seamless interaction.

> **Note:** This is a **showcase** repo containing detailed documentation, architecture diagrams, screenshots, and a breakdown of my contributions. The production code and private endpoints are not included to protect confidentiality.

<img width="1193" height="912" alt="image" src="https://github.com/user-attachments/assets/7e6ab4f4-3586-43de-9d91-c3b4e911d773" />

<img width="1198" height="919" alt="image" src="https://github.com/user-attachments/assets/f6d391a3-fe0a-4c94-be29-ff76806e4674" />

<img width="488" height="894" alt="image" src="https://github.com/user-attachments/assets/9ba0f711-74c8-49c7-94b3-dd210d17662f" />

---

## 🚀 Key Features

- **Natural-Language Q&A**: Users ask policy-related questions; Sofia replies conversationally.
- **Semantic Search**: Azure Cognitive Search indexes PDF content (text & images) with custom skillsets.
- **In-Response Citations**: Answers include clickable citations pointing to original documents.
- **Document Upload & Live Indexing**: New PDFs can be uploaded and indexed on the fly.
- **Tagging & Metadata**: MySQL-backed tagging system for categorizing citations (e.g., "Important", "HR").
- **Secure Communication**: HTTPS via SSL/TLS for both frontend (port 3000) and backend (port 7221).

---

## 🏛 Architecture

Sofia follows a **client-server** model with Azure services as backend components. The diagram below illustrates the system’s high-level design:

<img width="940" height="373" alt="image" src="https://github.com/user-attachments/assets/20c69d4a-3daf-425b-ba67-b732fa417013" />


**Components:**

| Layer        | Technology                         | Role                                       |
| ------------ | ---------------------------------- | ------------------------------------------ |
| **Client**   | React, Next.js, Tailwind CSS       | Chat UI, citation panel, tag manager       |
| **Server**   | Python Flask                       | API endpoints (`/send`, `/get-tags`, etc.) |
| **Search**   | Azure Cognitive Search             | Semantic + keyword search                  |
| **AI**       | Azure OpenAI (ChatCompletionSkill) | Query enhancement & summarization          |
| **Storage**  | Azure Blob Storage                 | PDF document repository                    |
| **Database** | MySQL                              | Citation tags & metadata                   |

---

## 🔄 Workflow

1. **User Question:** Frontend sends a query via `/send` endpoint.
2. **Query Enhancement:** Backend calls Azure OpenAI to refine the query.
3. **Semantic Search:** Cognitive Search retrieves top document chunks.
4. **Summarization:** OpenAI summarizes relevant sections.
5. **Retrieve Tags:** Backend fetches existing tags from MySQL.
6. **Response Delivery:** Aggregated answer with clickable citation IDs.
7. **Display:** Frontend renders the chat bubble, citations sidebar, and tagging UI.

<img width="940" height="1058" alt="image" src="https://github.com/user-attachments/assets/6bfe4a97-222c-4740-bb64-43732ca52fe6" />


---

## 🎨 Frontend Details

- **Framework & Styling:** Built with React & Next.js, styled using Tailwind CSS.
- **Main Components:**
  - **ChatInterface** (`pages/page.tsx`): Renders chat history and input.
  - **CitationsSidebar**: Displays full citation text and tagging controls.
  - **FloatingParticles & BackgroundWaves**: Visual effects for engaging UI.
- **Features:** Dark mode toggle, responsive layout, animated elements.

[Paste screenshot of code snippet or UI panels here]

---

## ⚙️ Backend Details

- **API Implementation:** Flask app (`app.py`) exposes endpoints:
  - `/send`: Handles query processing and response assembly.
  - `/get-tags` & `/save-tags`: Manages citation tags in MySQL.
  - `/get-citation-id`: Generates SHA-256–based unique IDs.
- **Azure Integrations:**
  - **OpenAIService**: ChatCompletionSkill & embeddings.
  - **Blob Storage SDK**: Document ingestion and path metadata.
  - **Cognitive Search SDK**: Custom skillset for splitting, image captioning, and embeddings.
- **Security & Logging:** HTTPS with `cert.pem`/`key.pem`; rotating logs for API and frontend events.

---

## 🚀 Deployment Guide

### Frontend (Vercel/Netlify)

1. `npm run build` to generate production assets.
2. Deploy via platform dashboard or CLI.
3. Ensure environment variable or code update for backend API URL.
4. HTTPS is enabled by default on most platforms.

### Backend (Custom Server)

1. Install Python dependencies: `pip install -r requirements.txt`.
2. Configure environment variables (Azure & MySQL credentials).
3. Place `cert.pem` & `key.pem` in the server directory.
4. Run with SSL context:
   ```bash
   python app.py --ssl cert.pem key.pem
   ```
5. Use Gunicorn or similar for production-grade hosting.

### Azure Services Setup

- Provision Azure OpenAI, Blob Storage, Cognitive Search.
- Upload PDF policies to Blob Storage.
- Configure Search indexer and skillset.
- Initialize MySQL schema using `init_database` from `app.py`.

---

## 📦 Usage

1. Open the deployed URL in your browser.
2. Type a policy query (e.g., "What is the leave policy?").
3. View the conversational response with clickable citations.
4. Click citation IDs to open detailed excerpts or tag them.
5. Toggle dark mode or upload new documents via the upload panel.

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork this repo and clone your fork.
2. Install frontend (`npm install`) and backend (`pip install -r requirements.txt`).
3. Configure `.env` for Azure & MySQL.
4. Run frontend (`npm start`) and backend (`python app.py`).
5. Create a feature branch, add tests, and open a pull request.


---

*Developed by Manvik Talwar during an internship at Path Infotech.*

