# 💬 LangChain Prompts

> Hands-on implementations of LangChain's prompt layer — PromptTemplates, ChatPrompts, Messages, and Placeholders.

---

## 📁 Structure

```
langchain_prompts/
├── temperature.py            # Effect of temperature on model output
├── messages.py               # SystemMessage, HumanMessage, AIMessage
├── chatbot.py                # Memory-aware CLI chatbot using chat history
├── prompt_template.py        # PromptTemplate — fill & invoke
├── chat_prompt_template.py   # ChatPromptTemplate — dynamic system + human
├── message_placeholder.py    # MessagesPlaceholder — inject history into prompt
├── prompt_generator.py       # Save a PromptTemplate to template.json
├── prompt_ui.py              # Streamlit research paper summarizer UI
├── template.json             # Serialized PromptTemplate (used by prompt_ui.py)
└── chat_history.txt          # Sample chat history for placeholder demo
```

---

## ⚙️ Setup

```bash
pip install langchain langchain-openai streamlit python-dotenv
```

Create a `.env` file:

```env
OPENAI_API_KEY=your_key
```

---

## 🔑 Key Concepts

| File | What it demonstrates |
|------|---------------------|
| `messages.py` | Structured LangChain message types |
| `prompt_template.py` | Variable injection via `PromptTemplate` |
| `chat_prompt_template.py` | Multi-turn template with system + human roles |
| `message_placeholder.py` | Dynamic history injection with `MessagesPlaceholder` |
| `chatbot.py` | Stateful chatbot loop with memory |
| `prompt_ui.py` | Full Streamlit app with saved prompt |

---

> Built with ❤️ by [Shivanshu](https://github.com/shivanshu1512)
