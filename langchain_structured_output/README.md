# 🏗️ LangChain Structured Output

> Force LLMs to return clean, typed, structured data — using Pydantic, TypedDict, and JSON Schema.

---

## 📁 Structure

```
langchain_structured_output/
├── pydantic_demo.py                    # Pydantic BaseModel basics — validation & fields
├── typeddict_demo.py                   # TypedDict basics — lightweight typed dicts
├── json_schema.json                    # Sample JSON schema definition
├── students_dataset.csv                # Sample CSV dataset
├── with_structured_output_pydantic.py  # with_structured_output() via Pydantic (OpenAI)
├── with_structured_output_typeddict.py # with_structured_output() via TypedDict (OpenAI)
├── with_structured_output_json.py      # with_structured_output() via raw JSON schema
└── with_structured_output_llama.py     # with_structured_output() via Pydantic (HuggingFace)
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

| Approach | Tool | Best For |
|----------|------|----------|
| **Pydantic** | `BaseModel` + `Field` | Rich validation, descriptions, defaults |
| **TypedDict** | `TypedDict` + `Annotated` | Lightweight, no runtime overhead |
| **JSON Schema** | Raw dict | API-first, language-agnostic schemas |

All approaches use `.with_structured_output()` — LangChain's unified interface to force structured responses from any model.

---

> Built with ❤️ by [Shivanshu](https://github.com/shivanshu1512)
