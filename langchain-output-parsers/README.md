# 🔍 LangChain Output Parsers

> Transform raw LLM text responses into clean, typed, structured Python objects.

---

## 📁 Structure

```
langchain-output-parsers/
├── stroutputparser.py        # Manual chain without parser — step-by-step
├── stroutputparser1.py       # StrOutputParser — clean piping with | operator
├── jsonoutputparser.py       # JsonOutputParser — force JSON output (HuggingFace)
├── structuredoutputparser.py # StructuredOutputParser — schema-driven key-value
└── pydanticoutputparser.py   # PydanticOutputParser — typed Pydantic model output
```

---

## ⚙️ Setup

```bash
pip install langchain langchain-openai langchain-huggingface pydantic python-dotenv
```

Create a `.env` file:

```env
OPENAI_API_KEY=your_key
HUGGINGFACEHUB_API_TOKEN=your_key
```

---

## 🔑 Key Concepts

| Parser | Output Type | Best For |
|--------|-------------|----------|
| `StrOutputParser` | `str` | Clean string, enables chain piping |
| `JsonOutputParser` | `dict` | Free-form JSON from any model |
| `StructuredOutputParser` | `dict` | Key-value schema with `ResponseSchema` |
| `PydanticOutputParser` | Pydantic model | Fully typed, validated Python objects |

All parsers inject format instructions into the prompt via `get_format_instructions()` and parse the response automatically at the end of the chain.

---

> Built with ❤️ by [Shivanshu](https://github.com/shivanshu1512)
