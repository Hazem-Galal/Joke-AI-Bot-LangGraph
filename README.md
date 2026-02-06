# 🤖 Joke AI Bot with LangGraph

An interactive AI-powered joke bot built with **LangGraph** and **OpenAI GPT-4o**, designed to run in **Google Colab**.

The bot uses a stateful graph workflow to greet users, collect joke topics, validate them, generate jokes via GPT-4o, and loop interactively until the user decides to quit.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Hazem-Galal/Joke-AI-Bot-LangGraph/blob/main/Joke_AI_Bot_LangGraph.ipynb)

---

## 📐 Architecture

The bot follows a **LangGraph StateGraph** workflow with 4 nodes and conditional routing:

![Joke Bot Architecture](joke%20bot.png)

| Node | Description |
|------|-------------|
| **Greet User** | Welcomes the user and asks if they want to hear a joke |
| **Get & Check Topic** | Prompts for a topic, validates it with the LLM, and generates a joke if valid |
| **Continue?** | Asks the user if they want another joke |
| **Say Bye** | Displays a farewell message with the total joke count |

### Graph Flow

```
__start__ → Greet User
                ├── (Continue) → Get & Check Topic
                └── (End) ─────→ Say Bye

Get & Check Topic
    ├── (Invalid) → Get & Check Topic  [self-loop]
    ├── (Valid)   → Continue?
    └── (End)     → Say Bye

Continue?
    ├── (Continue) → Get & Check Topic
    └── (End)      → Say Bye

Say Bye → __end__
```

---

## ✨ Features

- **Interactive Loop** — Keep getting jokes until you decide to stop
- **Topic Validation** — The LLM checks if your topic is suitable for a joke
- **Self-Loop on Invalid Topics** — Invalid topics loop back, asking for a new one
- **Conversation History** — Full message history tracked via LangGraph state
- **Joke Counter** — Tracks how many jokes you've heard
- **Graph Visualization** — Renders the workflow graph inline in the notebook

---

## 🚀 Quick Start

### 1. Open in Google Colab

Click the badge above or open the notebook directly:  
[**Joke_AI_Bot_LangGraph.ipynb**](https://colab.research.google.com/github/Hazem-Galal/Joke-AI-Bot-LangGraph/blob/main/Joke_AI_Bot_LangGraph.ipynb)

### 2. Set Up Your API Key

1. In Colab, click the **🔑 Secrets** icon in the left sidebar
2. Add a new secret:
   - **Name:** `OPENAI_API_KEY`
   - **Value:** Your OpenAI API key
3. Toggle **"Notebook access"** ON

### 3. Run All Cells

Execute the cells sequentially (`Runtime` → `Run all`) and follow the interactive prompts.

---

## 📦 Dependencies

| Package | Purpose |
|---------|---------|
| `langgraph` | Graph-based workflow orchestration |
| `langchain-openai` | OpenAI GPT-4o integration |
| `langchain-core` | Core LangChain message types and utilities |

All dependencies are installed automatically in the first notebook cell.

---

## 🛠️ Technologies

- [LangGraph](https://github.com/langchain-ai/langgraph) — Stateful, multi-actor orchestration framework
- [LangChain](https://github.com/langchain-ai/langchain) — LLM application framework
- [OpenAI GPT-4o](https://platform.openai.com/) — Large language model for joke generation and topic validation
- [Google Colab](https://colab.research.google.com/) — Cloud-based Jupyter notebook environment

---

## 📁 Project Structure

```
Joke-AI-Bot-LangGraph/
├── Joke_AI_Bot_LangGraph.ipynb   # Main Colab notebook
├── joke bot.png                  # Architecture diagram
└── README.md                     # This file
```

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).
