# Reference — crawl4ai fallback

Used in Phase 1 (research) when the built-in URL fetch tool cannot read a source.

## What it is

crawl4ai v0.9.x — open-source LLM-friendly web crawler (Apache-2.0, Python ≥3.10).
Runs a headless browser (Playwright), so it renders JS-heavy pages and returns
clean Markdown, unlike a plain HTTP fetch.

## Install

```bash
pip install -U crawl4ai
crawl4ai-setup      # downloads/installs the browser
```

## Minimal usage (async API)

```python
import asyncio
from crawl4ai import AsyncWebCrawler

async def main():
    async with AsyncWebCrawler() as crawler:
        result = await crawler.arun(url="https://example.com/article")
        print(result.markdown)   # cleaned markdown of the page

asyncio.run(main())
```

Key objects: `AsyncWebCrawler`, `arun()`, `CrawlResult` (`.markdown`, `.html`,
`.cleaned_html`).

## Rules in the skill

1. Prefer the built-in fetch tool first (zero cost).
2. Escalate to crawl4ai only when fetch returns empty/error or the page is JS-only.
3. Never silently install packages — tell the user the exact commands and wait.
4. If no crawl capability at all, flag the source unverified in `research.md` and
   continue with lower confidence. Never invent findings.
