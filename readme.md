# MAARS - Multi-Agent AI Research System

> An AI-powered research assistant that coordinates multiple specialized agents to search the web, extract relevant information, generate structured research reports, and critically evaluate the final output.

MAARS is a modular backend-focused AI application built using **LangChain**, **Mistral AI**, and **Tavily Search**. Instead of relying on a single LLM response, the system distributes responsibilities across specialized AI agents, each performing a dedicated task within a research pipeline.

The project demonstrates how multiple AI agents can collaborate to produce higher-quality research by combining web search, content extraction, report generation, and automated review into a single workflow.

---

## Features

- Multi-agent research workflow with specialized AI agents
- Automated web search using Tavily Search API
- Intelligent webpage scraping for deeper information extraction
- AI-generated structured research reports
- Automated report evaluation using a dedicated critic agent
- Modular backend architecture for easy extension
- LangChain tool integration
- Prompt-engineered writer and reviewer workflows
- Environment variable based configuration
- Clean separation between agents, tools, and orchestration logic
- Robust webpage scraping with graceful error handling
- Easily extensible architecture for adding new agents or tools

---

## How It Works

The research workflow follows a sequential multi-agent pipeline:

## Tech Stack

### AI & LLM
- Mistral AI (`mistral-small-latest`)
- LangChain

### Search & Information Retrieval
- Tavily Search API

### Web Scraping
- BeautifulSoup4
- Requests

### Programming Language
- Python

### Configuration
- Python Dotenv

---

## Project Structure

```text
MAARS/
│
├── agents.py          # Creates and configures AI agents
├── pipeline.py        # Main orchestration pipeline
├── tools.py           # Search and scraping tools
├── requirements.txt   # Project dependencies
├── .env               # Environment variables (not committed)
└── README.md
```

---

## System Architecture

The backend follows a modular architecture where each component has a well-defined responsibility.

### Search Agent

The Search Agent is responsible for collecting recent and relevant information from the web. It uses the Tavily Search API through a custom LangChain tool to retrieve reliable search results, including article titles, URLs, and content snippets.

### Reader Agent

Instead of relying only on search snippets, the Reader Agent selects the most relevant resource and extracts its content using BeautifulSoup. The scraped text is cleaned by removing unnecessary HTML elements such as navigation bars, scripts, styles, and footers before being passed to the next stage.

### Writer Agent

The Writer Agent combines search results with the scraped webpage content to generate a comprehensive research report. The report follows a consistent structure:

- Introduction
- Key Findings
- Conclusion
- Sources

This ensures that every generated report is organized, factual, and easy to read.

### Critic Agent

After the report is generated, a dedicated Critic Agent independently reviews it. Instead of rewriting the report, it evaluates its overall quality by providing:

- Numerical score
- Strengths
- Areas for improvement
- Final verdict

Separating report generation from evaluation encourages better output quality and demonstrates a multi-agent workflow where different agents perform specialized tasks.

---

## Backend Design Principles

The project was designed with maintainability and extensibility in mind.

### Modular Components

Business logic is separated into dedicated modules:

- `tools.py` contains reusable tools.
- `agents.py` defines all AI agents.
- `pipeline.py` orchestrates the complete workflow.

This separation makes adding new agents or tools straightforward without affecting the rest of the system.

### Tool-Based Architecture

Instead of embedding every capability inside prompts, the system exposes web search and web scraping as reusable LangChain tools. This makes the agents more flexible and simplifies future expansion.

### Pipeline Orchestration

The complete research process is executed sequentially through a centralized pipeline that maintains the application state between different stages of execution.

This orchestration approach keeps each agent focused on a single responsibility while enabling them to collaborate as part of a larger workflow.

---

## Research Pipeline

The application executes a sequential multi-agent workflow where the output of one agent becomes the input for the next. A shared state object is maintained throughout the execution, allowing every stage to build upon previously collected information.

### Step 1 — Search

The pipeline begins by creating a Search Agent that queries the Tavily Search API for recent and relevant information related to the user's topic.

The search tool returns:

- Article titles
- Source URLs
- Content snippets

This provides the foundation for the remainder of the research process.

---

### Step 2 — Content Extraction

The Reader Agent analyzes the collected search results, identifies the most relevant source, and scrapes its contents using BeautifulSoup.

Before the content is forwarded, unnecessary HTML elements such as:

- Scripts
- Styles
- Navigation bars
- Footers

are removed to produce cleaner text for the language model.

---

### Step 3 — Report Generation

The Writer Agent combines:

- Search results
- Scraped webpage content

to generate a structured research report containing:

- Introduction
- Key Findings
- Conclusion
- References

Prompt templates ensure that every report follows a consistent and professional structure.

---

### Step 4 — Quality Review

Instead of ending with report generation, the system performs an additional validation step using a dedicated Critic Agent.

The generated report is evaluated for:

- Overall quality
- Clarity
- Completeness
- Areas for improvement

The Critic returns:

- Score
- Strengths
- Weaknesses
- Final verdict

This additional review stage demonstrates how multiple specialized AI agents can collaborate to improve overall output quality.

---

## Key Backend Highlights

This project demonstrates several backend engineering concepts commonly used in modern AI applications:

- Modular multi-agent architecture
- LangChain tool integration
- External API integration
- Prompt engineering
- State-driven pipeline execution
- Web scraping and preprocessing
- Environment-based configuration
- Separation of concerns
- Reusable components
- Graceful exception handling during scraping

---

## Installation

Clone the repository:

```bash
git clone https://github.com/JAINSID02/MULTI-AGENT-AI-RESEARCH-SYSTEM-MAARS.git
cd MULTI-AGENT-AI-RESEARCH-SYSTEM-MAARS
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

Create a `.env` file in the project root and add your API keys:

```env
MISTRAL_API_KEY=your_api_key
TAVILY_API_KEY=your_api_key
```

Run the application:

```bash
python pipeline.py
```

---

## Example Workflow

1. User enters a research topic.
2. The Search Agent gathers recent and reliable information from the web.
3. The Reader Agent extracts detailed content from the most relevant source.
4. The Writer Agent generates a structured research report.
5. The Critic Agent reviews the report and provides quality feedback.

---

## Future Improvements

The current version focuses on building a modular backend pipeline. Planned enhancements include:

- Web-based user interface
- Support for additional LLM providers
- Parallel execution of independent agents
- Multi-source content aggregation
- PDF and document research support
- Export reports as PDF or Markdown
- Conversation memory for follow-up research
- Docker support for simplified deployment

---

## Why I Built This

Most AI applications rely on a single prompt to generate an answer. I wanted to explore a more modular approach where multiple specialized AI agents collaborate to solve different parts of a research task.

This project was built to deepen my understanding of agent-based AI systems, tool calling, prompt engineering, and backend architecture while creating a foundation that can be extended with additional agents and capabilities in the future.

---

## Acknowledgements

This project uses several open-source tools and APIs, including:

- LangChain
- Mistral AI
- Tavily Search API
- BeautifulSoup
- Requests

Their excellent ecosystems made it possible to build a modular AI research workflow.

---

## License

This project is intended for educational and portfolio purposes.

---

## Connect With Me

**Sidharth Jain**

- GitHub: https://github.com/JAINSID02
- LinkedIn: www.linkedin.com/in/sidharth-jain-31b0b826a

If you found this project interesting, feel free to ⭐ the repository or connect with me to discuss AI, backend engineering, and multi-agent systems.