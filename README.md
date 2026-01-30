# HannaWebScraper

HannaWebScraper is a toolchain for enriching the knowledge base of the Hanna AI assistant, which operates in real time on IRC and web chat via n8n workflows.

## GitHub Pages / Project Website
The official project website for this repository is hosted at [https://botinfo.hivenet.dev/](https://botinfo.hivenet.dev/). This domain resolves directly to the `index.html` in this repository, which serves as the canonical bot information page ("botinfo") for the HannaWebScraper user agent. This page provides details about the bot, its user agent, contact information, and instructions for site owners who want to learn more or request exclusion from scraping. The content at this URL is kept up to date with the latest information and policies from this repository.

## How it works

- **Scraping**: The included Python script (`source/scrape_to_n8n.py`) scrapes public web pages and sends their content to an n8n webhook.
- **n8n Workflow**: The n8n workflow receives the text, generates OpenAI embeddings, and stores them in a Qdrant vector database.
- **Retrieval**: When users interact with Hanna (e.g., in IRC), Hanna can retrieve relevant facts from the vector database to answer questions with up-to-date, community-taught knowledge.

## Project Intent

- **Community Knowledge**: Anyone can contribute new facts or explanations by scraping and submitting public content.
- **Live AI Assistant**: Hanna uses this knowledge to provide helpful, accurate, and context-aware responses in chat.
- **Privacy & Security**: Only public web content is collected. No personal or sensitive data is intentionally gathered or stored. See the `legal/` folder for privacy and security details.

## Usage

1. Edit `source/scrape_to_n8n.py` with your URLs and n8n webhook.
2. Run the script to submit new knowledge to Hanna’s database.
3. Hanna will use this knowledge in real time to answer questions in chat.

## User-Agent

```
HannaWebScraper/1.0 (+https://botinfo.hivenet.dev/)
```

## Respect for robots.txt

- This bot checks and obeys `robots.txt` before crawling any site.

## Opt-out

To block this bot, add the following to your `robots.txt`:

```
User-agent: HannaWebScraper
Disallow: /
```

## Exclusion Requests

If you wish to be excluded from scraping, contact the maintainer (see Contact section) and your domain will be added to the `source/excluded_domains.txt` file. The script will automatically skip any domain listed there, including all subdomains (e.g., adding `example.com` will also exclude `sub.example.com`).

This ensures your site will not be scraped, even if included in the URLs list.

## Exclusion List Format

The exclusion list is stored in `source/excluded_domains.json` as an array of objects. Each object should have:

- `domain`: The domain to exclude (all subdomains included)
- `reason`: Reason for exclusion
- `requested_by`: Who requested the exclusion
- `date_added`: Date exclusion was added (YYYY-MM-DD)

Example:

```
[
  {
    "domain": "example.com",
    "reason": "Site owner requested exclusion via email",
    "requested_by": "owner@example.com",
    "date_added": "2026-01-30"
  }
]
```

## Contact

If you have security concerns, please use the contact email below.

**Contact:** pontuzz@protonmail.com
