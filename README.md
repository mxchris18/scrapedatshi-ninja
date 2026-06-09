# scrapedatshi-ninja 🥷
A lightweight python wrapper to scrape any website into clean Markdown for AI Agents using scrapedatshi.com.

```python
import requests

url = "[https://www.scrapedatshi.com/scrape](https://www.scrapedatshi.com/scrape)"
headers = {"X-API-Key": "YOUR_KEY_FROM_SCRAPEDATSHI"}
params = {"url": "[https://news.ycombinator.com/](https://news.ycombinator.com/)"}

response = requests.get(url, headers=headers, params=params)
print(response.json()["markdown"])
