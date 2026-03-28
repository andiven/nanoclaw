---
name: web-scraper-advanced
description: Advanced web scraping skill using BeautifulSoup and requests. Use this for fast, lightweight data extraction from static HTML pages when Playwright is not needed.
---

# Advanced Web Scraper

This skill provides fast, lightweight data extraction from web pages using `requests` and `BeautifulSoup`. 

## When to use
- Extracting text, links, or tables from static HTML pages.
- Scraping news articles, blogs, or documentation.
- When you need to scrape many pages quickly (Playwright is too slow).

## When NOT to use
- If the page requires JavaScript rendering (e.g., React/Vue SPAs). Use `webapp-testing` (Playwright) instead.
- If you need to click buttons or fill forms.

## Dependencies
Ensure these are installed in the environment:
```bash
pip install requests beautifulsoup4 lxml
```

## Example Usage

```python
import requests
from bs4 import BeautifulSoup
import json

def scrape_articles(url):
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36'
    }
    
    response = requests.get(url, headers=headers)
    response.raise_for_status()
    
    soup = BeautifulSoup(response.text, 'lxml')
    
    # Example: Extract all h2 titles
    articles = []
    for h2 in soup.find_all('h2'):
        articles.append(h2.get_text(strip=True))
        
    return articles

# Save to JSON
data = scrape_articles('https://example.com/blog')
with open('scraped_data.json', 'w') as f:
    json.dump(data, f, indent=2)
```

## Best Practices
1. **Always use a User-Agent header** to avoid basic bot blocks.
2. **Handle exceptions**: Always use `response.raise_for_status()` or try-except blocks for `requests.exceptions.RequestException`.
3. **Respect robots.txt** and don't overload servers (add `time.sleep()` between multiple requests).
4. Use `lxml` parser as it is much faster than `html.parser`.
