# 🔄 LangChain Runnables

> The building blocks of LCEL — composable primitives that power every LangChain pipeline.

---

## 📁 Structure

```
langchain_runnables/
├── runnable_sequence.py    # RunnableSequence — explicit step-by-step chaining
├── runnable_parallel.py    # RunnableParallel — run multiple chains concurrently
├── runnable_passthrough.py # RunnablePassthrough — forward input unchanged
├── runnable_lambda.py      # RunnableLambda — wrap any Python function as a step
└── runnable_branch.py      # RunnableBranch — conditional routing at runtime
```

---

## ⚙️ Setup

```bash
pip install langchain langchain-openai python-dotenv
```

Create a `.env` file:

```env
OPENAI_API_KEY=your_key
```

---

## 🔑 Key Concepts

| Runnable | Purpose | When to Use |
|----------|---------|-------------|
| `RunnableSequence` | Chain steps in order | Any multi-step pipeline |
| `RunnableParallel` | Run branches concurrently | Independent sub-tasks |
| `RunnablePassthrough` | Forward input as-is | Preserve original data alongside transforms |
| `RunnableLambda` | Wrap a plain Python function | Custom logic (e.g. word count, transforms) |
| `RunnableBranch` | Conditional routing | Different paths based on runtime value |

> All runnables implement `.invoke()`, `.stream()`, and `.batch()` — making them fully interoperable via the `|` pipe operator.

---

> Built with ❤️ by [Shivanshu](https://github.com/shivanshu1512)
