# 🔗 LangChain Chains

> Build powerful pipelines by composing prompts, models, and parsers with the `|` operator.

---

## 📁 Structure

```
langchain-chains/
├── simple_chain.py      # prompt | model | parser — the foundation
├── sequential_chain.py  # Two prompts in series — report → summary
├── parallel_chain.py    # RunnableParallel — notes & quiz generated concurrently
└── conditional_chain.py # RunnableBranch — route by sentiment classification
```

---

## ⚙️ Setup

```bash
pip install langchain langchain-openai langchain-anthropic pydantic python-dotenv
```

Create a `.env` file:

```env
OPENAI_API_KEY=your_key
ANTHROPIC_API_KEY=your_key
```

---

## 🔑 Key Concepts

| Chain Type | Runnable | Pattern |
|------------|----------|---------|
| **Simple** | `|` pipe | `prompt → model → parser` |
| **Sequential** | `|` pipe | Output of chain 1 feeds chain 2 |
| **Parallel** | `RunnableParallel` | Multiple chains run simultaneously |
| **Conditional** | `RunnableBranch` | Dynamic routing based on intermediate output |

All chains expose `.get_graph().print_ascii()` to visualize the execution DAG.

---

> Built with ❤️ by [Shivanshu](https://github.com/shivanshu1512)
