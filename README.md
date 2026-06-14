# 🔬 ResearchMind — Multi-Agent AI Research Assistant

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![LangChain](https://img.shields.io/badge/LangChain-Agents-green)
![Streamlit](https://img.shields.io/badge/Streamlit-Web%20App-red?logo=streamlit)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Inference-yellow?logo=huggingface)
![LLM](https://img.shields.io/badge/LLM-Qwen2.5--7B-orange)

---

# 📌 Project Overview

ResearchMind is a multi-agent AI research assistant built with LangChain that autonomously researches a topic, gathers information from the web, extracts detailed content from relevant sources, generates a structured research report, and critiques its own output.

Instead of relying on a single prompt, the system decomposes the task into specialized agents and chains, allowing each component to focus on a specific responsibility in the research workflow.

The project demonstrates practical Agentic AI patterns including tool calling, web search, content retrieval, report generation, and self-evaluation.

---

# 🎯 Problem Statement

Large Language Models often struggle with:

* Accessing up-to-date information
* Verifying claims from external sources
* Producing structured long-form reports
* Evaluating the quality of their own outputs

ResearchMind addresses these limitations by combining LLM reasoning with external tools and a multi-stage workflow.

---

# 🏗️ System Architecture

```text
User Research Query
        │
        ▼
┌─────────────────────┐
│   Search Agent      │
│  (Tavily Search)    │
└─────────────────────┘
        │
        ▼
┌─────────────────────┐
│   Reader Agent      │
│ (Web Scraper Tool)  │
└─────────────────────┘
        │
        ▼
┌─────────────────────┐
│   Writer Chain      │
│ Research Report     │
└─────────────────────┘
        │
        ▼
┌─────────────────────┐
│   Critic Chain      │
│ Quality Evaluation  │
└─────────────────────┘
        │
        ▼
┌─────────────────────┐
│   Streamlit UI      │
└─────────────────────┘
```

---

# 🤖 Agent Workflow

## 1. Search Agent

Built using LangChain's `create_agent()`.

Responsibilities:

* Search the internet for relevant information
* Collect recent and reliable sources
* Return titles, URLs, and snippets

Tool:

```python
web_search_tool()
```

Output:

```text
Title
URL
Snippet
```

---

## 2. Reader Agent

The Reader Agent performs deep content retrieval.

Responsibilities:

* Select relevant URLs
* Scrape webpage content
* Remove noise such as scripts, styles, and navigation elements
* Extract clean text for analysis

Tool:

```python
scrape_url_tool()
```

Output:

```text
Clean article content
```

---

## 3. Writer Chain

Transforms gathered research into a professional report.

Responsibilities:

* Summarize findings
* Organize information
* Generate structured research documents

Report Structure:

* Introduction
* Key Findings
* Conclusion
* Sources

Built using:

```python
ChatPromptTemplate
→ ChatOpenAI
→ StrOutputParser
```

---

## 4. Critic Chain

Acts as an independent reviewer.

Responsibilities:

* Evaluate report quality
* Identify strengths
* Suggest improvements
* Assign a quality score

Output Format:

```text
Score: X/10

Strengths:
- ...

Areas to Improve:
- ...

Verdict:
...
```

---

# 🧠 LLM Configuration

Model:

```python
Qwen/Qwen2.5-7B-Instruct
```

Inference Provider:

```python
Hugging Face Router API
```

Configuration:

```python
temperature=0
```

Using deterministic generation improves consistency across report creation and evaluation stages.

---

# 🔧 Tech Stack

| Layer                  | Technology           |
| ---------------------- | -------------------- |
| Language               | Python               |
| LLM Framework          | LangChain            |
| Model                  | Qwen 2.5 7B Instruct |
| Agent Framework        | LangChain Agents     |
| Search Engine          | Tavily               |
| Web Scraping           | BeautifulSoup        |
| HTTP Requests          | Requests             |
| UI                     | Streamlit            |
| Prompting              | ChatPromptTemplate   |
| Output Parsing         | StrOutputParser      |
| Environment Management | python-dotenv        |

---

# 🚀 Key Features

### Multi-Agent Architecture

Separates responsibilities across independent agents rather than relying on a single prompt.

### Tool Calling

Agents can invoke external tools dynamically using LangChain's tool interface.

### Live Web Research

Searches real-time web content rather than relying solely on model knowledge.

### Automated Content Extraction

Scrapes and cleans webpage content for deeper context.

### AI Report Generation

Creates structured research reports automatically.

### Self-Critique System

Uses a dedicated critic chain to evaluate generated reports.

### Interactive UI

Streamlit-based interface for running the complete workflow from a browser.

### Downloadable Reports

Generated reports can be exported as Markdown files.

---

# 📂 Project Structure

```text
ResearchMind/
│
├── app.py
├── agents.py
├── tools.py
├── .env
├── requirements.txt
│
├── assets/
│
└── outputs/
```

---

# ⚙️ Installation

## Clone Repository

```bash
git clone <repository-url>
cd ResearchMind
```

## Create Environment

```bash
conda create -n researchmind python=3.10 -y
conda activate researchmind
```

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🔑 Environment Variables

Create a `.env` file:

```env
HF_TOKEN=your_huggingface_token
TAVILY_API_KEY=your_tavily_api_key
```

---

# ▶️ Running the Application

Launch Streamlit:

```bash
streamlit run app.py
```

Open:

```text
http://localhost:8501
```

---

# 🖥️ User Workflow

1. Enter a research topic
2. Search Agent gathers information
3. Reader Agent extracts detailed content
4. Writer Chain creates report
5. Critic Chain reviews report
6. Download final report

---

# 💡 Engineering Highlights

### LangChain Tool Integration

Both search and scraping capabilities are exposed as LangChain tools using:

```python
@tool
```

allowing agents to decide when and how to use external capabilities.

### Modular Agent Design

Agents are isolated from business logic, making the system easier to extend and maintain.

### Prompt Chaining

Report generation and evaluation are separated into dedicated chains for better controllability.

### Human-Like Research Workflow

The pipeline mirrors how humans conduct research:

Search → Read → Write → Review

---

# 📈 Future Improvements

* Add LangGraph orchestration
* Multi-source scraping
* Citation verification
* RAG integration
* Report versioning
* PDF export
* Memory-enabled conversations
* Multi-agent debate workflows
* Research source ranking
* Async parallel execution

---

# 🎯 Skills Demonstrated

* Agentic AI Systems
* LangChain Agents
* Tool Calling
* Prompt Engineering
* LLM Application Development
* Web Scraping
* Information Retrieval
* Multi-Step Reasoning Pipelines
* Streamlit Deployment
* AI Product Engineering

---

# 👨‍💻 Author

Shubham Mishra

Built as an Agentic AI project demonstrating how multiple specialized LLM components can collaborate to perform autonomous research and report generation.
