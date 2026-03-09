

# AI Overview Content Gap Agent

## Overview
This project implements an AI agent that analyzes Google AI Overview sources and identifies content gaps in a client article.

The agent performs the following steps:
1. Searches Google for a keyword
2. Extracts URLs appearing in the AI Overview (or falls back to top organic results)
3. Scrapes the content of those pages
4. Scrapes the client article
5. Uses an LLM (Gemini 2.5 Flash) to compare them
6. Generates a structured content gap report in `.docx` format

The generated report helps SEO writers understand what content formats or sections are missing compared to pages referenced by Google AI Overviews.



## Features

### Search & Extraction
- Fetches search results using SerpAPI
- Extracts AI Overview source URLs

### Web Scraping
- Scrapes page content using BeautifulSoup
- Extracts article text and structural elements

### Content Format Analysis
The agent detects important SEO content structures:
- FAQ sections
- Bullet lists (`ul`)
- Numbered lists (`ol`)
- Tables
- Heading structure (H1, H2, H3)
- Comparison sections
- Calculators

### AI Analysis
- Uses Gemini 2.5 Flash for LLM analysis
- Compares AI Overview sources with the client article
- Identifies content gaps and structural differences

### Report Generation
- Automatically generates a formatted Word report (`gap_report.docx`)



## Example Workflow

Input

Keyword:
what is term insurance

Client URL:
https://www.axismaxlife.com/blog/term-insurance/what-is-term-insurance

Output

gap_report.docx

The report contains:
- AI Overview source URLs
- Content structure analysis
- Client article analysis
- Gap summary
- SEO improvement recommendations



## Project Structure

```
Assignment/
│
├── main.py
├── readme.md
└── gap_report.docx (generated)
```



## Requirements

Python 3.9+

Install dependencies:

```
pip install requests beautifulsoup4 python-docx serpapi google-generativeai python-dotenv
```



## API Keys Required

### SerpAPI
Used to fetch Google search results and AI Overview sources.

Get an API key here:
https://serpapi.com/

### Google Gemini API
Used for AI-powered content gap analysis.

Get an API key here:
https://aistudio.google.com/app/apikey



## Environment Variables

Create a `.env` file in the project directory.

Example:

```
SERPAPI_KEY=your_serpapi_key
GEMINI_API_KEY=your_gemini_api_key
```



## Running the Agent

Run the script:

```
python main.py
```

Then enter the required inputs:

Enter keyword:
Enter client URL:

Example:

Enter keyword: what is term insurance  
Enter client URL: https://example.com/term-insurance-guide

The agent will:
1. Fetch AI Overview sources
2. Scrape their content
3. Analyze the client page
4. Perform AI comparison
5. Generate `gap_report.docx`



## Output Report

### AI Overview Sources
List of URLs that Google used in the AI Overview.

### Content Format Analysis
For each AI Overview page the following are analyzed:
- Word count
- Heading structure
- Bullet lists
- Numbered lists
- Tables
- FAQ presence
- Comparison sections
- Calculators

### Client Article Analysis
The same structural analysis is applied to the client article.

### Gap Analysis
The LLM compares the two sets of content and identifies:
- Missing sections
- Missing formats
- Structural differences
- Content depth gaps

### Recommendations
The system generates 3–5 actionable SEO recommendations for improving the client article.


## Design Decisions

- BeautifulSoup used for scraping due to simplicity and reliability
- Heuristic detection used to identify content formats
- Gemini 2.5 Flash chosen for fast and cost-efficient LLM analysis
- Organic search results fallback ensures the agent runs even if AI Overview sources are unavailable


## Limitations

- Some websites load content dynamically using JavaScript, which `requests` cannot fully render
- Heuristic detection of comparison sections and calculators may not always be perfectly accurate


