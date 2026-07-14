# 🧠 LangChain Models

> Hands-on implementations of LangChain's model layer — LLMs, Chat Models, and Embedding Models.

---

## 📁 Structure

```
langchain models/
├── 1.LLMs/                      # Legacy completion-style models
│   └── 1_llm_demo.py            # OpenAI GPT-3.5 via LLM interface
│
├── 2.ChatModels/                # Conversational chat models
│   ├── 1_chatmodel_openai.py    # GPT-4 via ChatOpenAI
│   ├── 2_chatmodel_anthropic.py # Claude 3.5 Sonnet
│   ├── 3_chatmodel_google.py    # Gemini 1.5 Pro
│   ├── 4_chatmodel_hf_api.py    # HuggingFace Inference API
│   └── 5_chatmodel_hf_local.py  # HuggingFace local pipeline
│
├── 3.EmbeddingModels/           # Vector representations of text
│   ├── 1_embedding_openai_query.py   # Embed a single query
│   ├── 2_embedding_openai_docs.py    # Embed multiple documents
│   ├── 3_embedding_hf_local.py       # HuggingFace sentence-transformers
│   └── 4_document_similarity.py      # Cosine similarity search
│
├── requirements.txt
└── test.py
```

---

## ⚙️ Setup

```bash
pip install -r requirements.txt
```

Create a `.env` file with your API keys:

```env
OPENAI_API_KEY=your_key
ANTHROPIC_API_KEY=your_key
GOOGLE_API_KEY=your_key
HUGGINGFACEHUB_API_TOKEN=your_key
```

---

## 🔑 Key Concepts

| Module | What it covers |
|--------|---------------|
| **LLMs** | Raw text-in, text-out completion models |
| **ChatModels** | Message-based multi-turn conversation models |
| **EmbeddingModels** | Dense vector representations for semantic search |

---

> Built with ❤️ by [Shivanshu](https://github.com/shivanshu1512)
