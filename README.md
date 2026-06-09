# scrapedatshi-ninja &nbsp;<img src="https://www.scrapedatshi.com/static/favicon-32.png" width="28" height="28" align="center" alt="scrapedatshi logo">

> A dead-simple API wrapper that converts raw HTML into clean, token-saving Markdown — purpose-built for AI agents, LLM context windows, LangChain, AutoGPT, and vector database retrieval pipelines.

**scrapedatshi** strips away JavaScript bloat, DOM clutter, styles, tracking scripts, and sidebars, handing your LLM pure semantic markdown. A fast, lightweight, and entirely **free** alternative to Firecrawl, Jina Reader, and Crawl4AI.

---

## Table of Contents

- [Core Features](#-core-features)
- [Quick Start](#-quick-start)
- [Developer Usage Guide](#%EF%B8%8F-developer-usage-guide)
  - [Basic Usage](#1-basic-usage-python)
  - [Target CSS Selectors](#2-advanced-usage-target-css-selectors)
  - [API Response Shape](#3-api-response-shape)
- [AI Agent Integration](#-ai-agent-integration-langchain)

---

## 🚀 Core Features

| Feature | Description |
|---|---|
| **Zero Friction** | No credit cards or complex setups. Grab a free key at [scrapedatshi.com](https://www.scrapedatshi.com) and go. |
| **Targeted Clipping** | Pass a `selector` (e.g. `.article-body`, `#main-content`) to isolate specific elements and slash LLM token costs. |
| **Auto Metadata Extraction** | Every scrape automatically pulls structured OpenGraph tags — `title`, `author`, `description`, `published_date`. |
| **Async Engine** | Built to handle concurrent parallel requests for autonomous AI agent networks. |

---

## ⚡ Quick Start

```bash
# 1. Get your free API key at https://www.scrapedatshi.com
# 2. Set it as an environment variable
export SCRAPEDATSHI_API_KEY="your_key_here"
```

```python
import os, requests

response = requests.get(
    "https://www.scrapedatshi.com/scrape",
    params={"url": "https://news.ycombinator.com/"},
    headers={"X-API-Key": os.getenv("SCRAPEDATSHI_API_KEY")}
)

print(response.json()["markdown"])
```

---

## 🛠️ Developer Usage Guide

### 1. Basic Usage (Python)

Scrape any public URL and receive clean markdown back in a single call:

```python
import os
import requests

API_KEY = os.getenv("SCRAPEDATSHI_API_KEY")
ENDPOINT = "https://www.scrapedatshi.com/scrape"

params = {"url": "https://news.ycombinator.com/"}
headers = {"X-API-Key": API_KEY}

response = requests.get(ENDPOINT, params=params, headers=headers)
data = response.json()

print(data["markdown"])
```

---

### 2. Advanced Usage: Target CSS Selectors

Pass a `selector` to isolate exactly the content you need, dropping the rest and reducing token overhead significantly:

```python
import os
import requests

API_KEY = os.getenv("SCRAPEDATSHI_API_KEY")
ENDPOINT = "https://www.scrapedatshi.com/scrape"

params = {
    "url": "https://en.wikipedia.org/wiki/Ninja",
    "selector": ".mw-heading"  # Extract only section headings
}
headers = {"X-API-Key": API_KEY}

response = requests.get(ENDPOINT, params=params, headers=headers)
print(response.json()["markdown"])
```

---

### 3. API Response Shape

Every successful response returns a consistent JSON envelope:

```json
{
  "authenticated_user": "dev_ninja",
  "url": "https://example.com/",
  "selector": null,
  "metadata": {
    "title": "Page Title",
    "description": "Page description text...",
    "author": "Author Name",
    "published_date": "2026-06-09",
    "site_name": "Example Platform"
  },
  "markdown": "# Page Title\n\nCore cleaned text content goes here..."
}
```

| Field | Type | Description |
|---|---|---|
| `authenticated_user` | `string` | The API key owner identifier |
| `url` | `string` | The URL that was scraped |
| `selector` | `string \| null` | CSS selector used, if any |
| `metadata` | `object` | Extracted OpenGraph / meta tag data |
| `markdown` | `string` | The cleaned, LLM-ready markdown content |

---

## 🤖 AI Agent Integration (LangChain)

Drop this into any LangChain pipeline to give your agent live web access with clean, token-efficient output:

```python
from langchain.tools import tool
import requests
import os

@tool
def scrapedatshi_web_search(url: str, selector: str = None) -> str:
    """
    Scrapes a live webpage and converts it into optimized markdown for the
    LLM context window. Clean alternative to Firecrawl.
    """
    headers = {"X-API-Key": os.getenv("SCRAPEDATSHI_API_KEY")}
    params = {"url": url}
    if selector:
        params["selector"] = selector

    try:
        response = requests.get(
            "https://www.scrapedatshi.com/scrape",
            params=params,
            headers=headers
        )
        if response.status_code == 200:
            return response.json()["markdown"]
        return f"Error: Received status code {response.status_code}"
    except Exception as e:
        return f"Scraping failed: {str(e)}"
```

Then register it with your agent:

```python
from langchain.agents import initialize_agent, AgentType
from langchain.chat_models import ChatOpenAI

llm = ChatOpenAI(model="gpt-4")
agent = initialize_agent(
    tools=[scrapedatshi_web_search],
    llm=llm,
    agent=AgentType.OPENAI_FUNCTIONS,
    verbose=True
)

agent.run("Summarize the top stories on Hacker News right now.")
```

---

<div align="center">

Built for builders. **[Get your free API key →](https://www.scrapedatshi.com)**

</div>
