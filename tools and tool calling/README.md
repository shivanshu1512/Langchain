# 🛠️ LangChain Tools & Tool Calling

This folder covers **Tools** and **Tool Calling** in LangChain — one of the most powerful features for building intelligent agents that can interact with the real world.

---

## 📌 What are Tools?

In LangChain, a **Tool** is a function that an LLM (Language Model) can invoke to perform specific tasks — such as searching the web, running Python code, querying a database, or calling an API.

Tools bridge the gap between a language model (which only handles text) and the real world (APIs, databases, file systems, etc.).

---

## 🧠 What is Tool Calling?

**Tool Calling** (also called **Function Calling**) is the mechanism by which an LLM decides:

1. **Whether** to call a tool
2. **Which** tool to call
3. **What arguments** to pass to it

Modern LLMs like OpenAI's GPT-4o, Claude, and Gemini support tool/function calling natively.

---

## 🏗️ Core Concepts

### 1. Defining a Tool

You can create a tool in LangChain using:

- **`@tool` decorator** — simplest approach
- **`StructuredTool`** — for tools with complex inputs (Pydantic schemas)
- **`BaseTool` class** — for full control and customization

```python
from langchain_core.tools import tool

@tool
def add_numbers(a: int, b: int) -> int:
    """Adds two numbers together."""
    return a + b
```

### 2. Binding Tools to an LLM

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(model="gpt-4o")
llm_with_tools = llm.bind_tools([add_numbers])
```

### 3. Invoking Tool Calls

```python
response = llm_with_tools.invoke("What is 5 + 7?")
print(response.tool_calls)
# [{'name': 'add_numbers', 'args': {'a': 5, 'b': 7}, 'id': '...'}]
```

### 4. Executing the Tool and Getting Final Response

```python
from langchain_core.messages import ToolMessage

tool_call = response.tool_calls[0]
result = add_numbers.invoke(tool_call["args"])

messages = [
    response,
    ToolMessage(content=str(result), tool_call_id=tool_call["id"])
]
final_response = llm_with_tools.invoke(messages)
```

---

## 📂 Topics Covered in This Folder

| File | Description |
|------|-------------|
| `README.md` | This overview document |
| *(Coming Soon)* `01_basic_tool_creation.ipynb` | Creating tools with `@tool` decorator & `StructuredTool` |
| *(Coming Soon)* `02_tool_calling_with_llm.ipynb` | Binding tools to LLMs and processing tool call responses |
| *(Coming Soon)* `03_built_in_tools.ipynb` | Using LangChain's built-in tools (Tavily Search, Wikipedia, DuckDuckGo, etc.) |
| *(Coming Soon)* `04_custom_tools.ipynb` | Building custom tools with Pydantic schemas & `BaseTool` |
| *(Coming Soon)* `05_tool_calling_agent.ipynb` | Building a ReAct agent that loops through tool calls |

---

## 🔧 Types of Tools in LangChain

### Built-in Tools
LangChain provides many ready-to-use tools out of the box:

| Tool | Package | Description |
|------|---------|-------------|
| `TavilySearchResults` | `langchain-community` | AI-powered web search |
| `WikipediaQueryRun` | `langchain-community` | Query Wikipedia |
| `DuckDuckGoSearchRun` | `langchain-community` | DuckDuckGo web search |
| `PythonREPLTool` | `langchain-experimental` | Run Python code |
| `ShellTool` | `langchain-community` | Run shell commands |
| `RequestsGetTool` | `langchain-community` | Make HTTP GET requests |
| `SQLDatabaseTool` | `langchain-community` | Query SQL databases |
| `ArxivQueryRun` | `langchain-community` | Search academic papers |

### Custom Tools
You can wrap any Python function into a LangChain tool:

```python
from langchain_core.tools import tool
from pydantic import BaseModel

class WeatherInput(BaseModel):
    city: str
    unit: str = "celsius"

@tool(args_schema=WeatherInput)
def get_weather(city: str, unit: str = "celsius") -> str:
    """Get the current weather for a city."""
    # Call a real weather API here
    return f"The weather in {city} is 25°{unit[0].upper()}."
```

---

## 🔄 Tool Calling Flow

```
User Input
    │
    ▼
LLM (with tools bound)
    │
    ├──► Decides to call a tool
    │         │
    │         ▼
    │    Tool Execution (Python function runs)
    │         │
    │         ▼
    │    ToolMessage (result sent back to LLM)
    │
    ▼
LLM generates Final Response
    │
    ▼
User Output
```

---

## 🤖 Tool Calling vs. Agents

| Feature | Tool Calling | Agents (ReAct) |
|---------|-------------|----------------|
| **Loop** | Single call | Multi-step loop |
| **Decision** | LLM decides once | LLM reasons at each step |
| **Complexity** | Simple | Complex tasks |
| **Use case** | Direct task execution | Multi-hop reasoning |

---

## 📦 Required Packages

```bash
pip install langchain langchain-core langchain-openai langchain-community
pip install tavily-python  # for Tavily Search tool
pip install wikipedia      # for Wikipedia tool
```

---

## 🔑 Environment Variables

```bash
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key       # for web search
LANGCHAIN_API_KEY=your_langsmith_api_key  # for tracing (optional)
LANGCHAIN_TRACING_V2=true                 # enable LangSmith tracing
```

---

## 🧩 Practical Example — Multi-Tool Agent

```python
from langchain_openai import ChatOpenAI
from langchain_core.tools import tool
from langchain_community.tools.tavily_search import TavilySearchResults
from langchain.agents import create_react_agent, AgentExecutor
from langchain import hub

# Define tools
search_tool = TavilySearchResults(max_results=3)

@tool
def calculate(expression: str) -> float:
    """Evaluate a mathematical expression."""
    return eval(expression)

tools = [search_tool, calculate]

# Create agent
llm = ChatOpenAI(model="gpt-4o", temperature=0)
prompt = hub.pull("hwchase17/react")
agent = create_react_agent(llm, tools, prompt)
agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True)

# Run
result = agent_executor.invoke({
    "input": "What is the current price of Bitcoin? And what is 1000 * 1.08?"
})
print(result["output"])
```

---

## 🔗 Related Sections in This Repository

- [`langchain models`](../langchain%20models/) — LLM model setup (OpenAI, HuggingFace, Ollama)
- [`langchain_prompts`](../langchain_prompts/) — Prompt templates used in tool-calling agents
- [`langchain-chains`](../langchain-chains/) — Chains that orchestrate tool calls
- [`langchain_runnables`](../langchain_runnables/) — LCEL for composing tool-calling pipelines
- [`langchain_structured_output`](../langchain_structured_output/) — Structured output, closely related to tool schemas

---

## 📚 References

- [LangChain Tools Documentation](https://python.langchain.com/docs/concepts/tools/)
- [LangChain Tool Calling Guide](https://python.langchain.com/docs/how_to/tool_calling/)
- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)
- [LangChain Built-in Tools](https://python.langchain.com/docs/integrations/tools/)

---

> **Next Steps:** Check back for upcoming notebooks in this folder that demonstrate each concept with hands-on code examples!
