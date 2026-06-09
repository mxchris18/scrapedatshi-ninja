# scrapedatshi-ninja 🥷

[![API Status](https://img.shields.io/website?url=https%3A%2F%2Fwww.scrapedatshi.com)](https://www.scrapedatshi.com)

A dead-simple API wrapper built to convert raw HTML into clean, token-saving Markdown. Purpose-built for AI Agents, LLM context windows, LangChain, AutoGPT, and vector database retrieval pipelines.

**scrapedatshi** is a fast, lightweight, entirely free alternative to Firecrawl, Jina Reader, and Crawl4AI. It strips away JavaScript bloat, DOM clutter, styles, tracking scripts, and sidebars, handing your LLM pure semantic markdown structure.

---

## 🚀 Core Features

- **Zero Friction:** No credit cards or complex setups. Grab a key from [scrapedatshi.com](https://www.scrapedatshi.com) and go.
- **Targeted Clipping (`selector`):** Isolate specific elements (like `.article-body` or `#main-content`) to slash your LLM token costs.
- **Automated Metadata Extraction:** Every scrape automatically pulls structured OpenGraph tags (`title`, `author`, `description`, `published_date`).
- **Async Engine Architecture:** Built to handle concurrent parallel tracking loops for autonomous AI agent networks.

---

## 🛠️ Developer Usage Guide

### 1. Basic Usage (Python)

```python
import os
import requests

# Get your free key at [https://www.scrapedatshi.com](https://www.scrapedatshi.com)
API_KEY = os.getenv("SCRAPEDATSHI_API_KEY")
ENDPOINT = "[https://www.scrapedatshi.com/scrape](https://www.scrapedatshi.com/scrape)"

params = {
    "url": "[https://news.ycombinator.com/](https://news.ycombinator.com/)"
}
headers = {
    "X-API-Key": API_KEY
}

response = requests.get(ENDPOINT, params=params, headers=headers)
data = response.json()

print(data["markdown"])

Advanced Usage: Target CSS Selectors

params = {
    "url": "[https://en.wikipedia.org/wiki/Ninja](https://en.wikipedia.org/wiki/Ninja)",
    "selector": ".mw-heading" # Extract only section headings
}

response = requests.get(ENDPOINT, params=params, headers=headers)
print(response.json()["markdown"])

Structural API Response Shape

{
  "authenticated_user": "dev_ninja",
  "url": "[https://example.com/](https://example.com/)",
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


