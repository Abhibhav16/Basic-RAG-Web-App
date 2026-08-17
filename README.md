# Basic RAG Web App

A conversational RAG (Retrieval-Augmented Generation) chatbot built with Streamlit and LangChain. Upload one or more PDFs and ask questions about their content — the app keeps chat history so you can ask follow-up questions naturally.

## Features

- Upload multiple PDFs and chat with their combined content
- Conversation-aware retrieval (follow-up questions are reformulated using chat history)
- Local embeddings via HuggingFace (`all-MiniLM-L6-v2`) — no embedding API costs
- Fast inference via Groq (`openai/gpt-oss-120b`)
- Per-session chat history, keyed by a session ID you set

## Tech stack

- [Streamlit](https://streamlit.io/) — UI
- [LangChain](https://www.langchain.com/) — RAG orchestration
- [Chroma](https://www.trychroma.com/) — vector store
- [HuggingFace](https://huggingface.co/) — embeddings
- [Groq](https://groq.com/) — LLM inference

## Setup

1. Clone the repo:
   ```bash
   git clone https://github.com/Abhibhav16/Basic-RAG-Web-App.git
   cd Basic-RAG-Web-App
   ```

2. Create a virtual environment and install dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate  # on Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Create a `.env` file in the project root with your HuggingFace token:
   ```
   HF_TOKEN=your_huggingface_token_here
   ```

4. Run the app:
   ```bash
   streamlit run app.py
   ```

5. Enter your [Groq API key](https://console.groq.com/keys) in the app, upload a PDF, and start asking questions.

## Deployment

This app is deployed on [Streamlit Community Cloud](https://share.streamlit.io/). To deploy your own copy:

1. Fork or push this repo to your own GitHub account
2. Go to share.streamlit.io → New app → point it at your repo and `app.py`
3. Under **Advanced settings → Secrets**, add:
   ```toml
   HF_TOKEN = "your_huggingface_token_here"
   ```
4. Deploy

## Notes

- The Groq API key is entered by the user at runtime rather than stored as a secret, so each user supplies their own.
- PDFs are processed in-memory per session and are not persisted between deployments.
