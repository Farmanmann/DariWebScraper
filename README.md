# VOA Dari Web Scraper

A Python-based web scraping project for extracting and processing articles from darivoa.com. The project includes tools for downloading articles, extracting clean text content, and formatting text with proper handling of Persian/Arabic text.

#Features

Daily Article Collection: Scrapes articles directly from the VOA Dari website.
    Multilingual Text Processing: Handles Persian/Arabic text with proper Unicode support.
    Automated Pipeline:
        Downloads and organizes raw HTML articles into date-based folders.
        Cleans and extracts main text content from the downloaded articles.
        Segments and formats the extracted content for NLP research.
    Output Organization: Saves processed data in structured directories (articles, article_texts, formatted_articles) by date.




## Project Structure

The project consists of three main scripts:
- `articleDownloader.py`: Downloads article HTML from the website, which is saved in articles/YYYY-MM-DD
- `textExtracter.py`: Extracts clean text content from HTML files, which is saved in article_texts/YYYY-MM-DD
- `format_text.py`: Formats and segments the extracted text, which is saved in formatted_texts/YYYY-MM-DD

## Setup

### Virtual Environment
```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Unix or MacOS:
source venv/bin/activate

# Install requirements
pip install -r requirements.txt
```

### Requirements
Create a `requirements.txt` file with the following dependencies:
```
beautifulsoup4==4.12.3
nltk==3.8.1
requests==2.31.0
```

## Component Details

### Article Downloader
`articleDownloader.py` handles the initial web scraping:
- Creates 'articles' directory if it doesn't exist
- Collects unique article URLs from darivoa.com
- Downloads HTML content for each article
- Saves files with UTF-8 encoding for Persian text
- Includes error handling and request delays
- Shows download progress
- Names files using article IDs

### Text Extractor
`textExtracter.py` processes the downloaded HTML:
- Creates 'article_texts' directory for cleaned content
- Processes HTML files from 'articles' directory
- Removes unwanted elements (scripts, styles, nav menus)
- Extracts text from relevant HTML tags
- Cleans whitespace and formatting
- Saves cleaned text to separate files

### Text Formatter
`format_text.py` provides final text processing:
- Uses NLTK for sentence segmentation
- Preserves Persian/Arabic characters (Unicode range \u0600-\u06FF)
- Maintains punctuation in both English and Persian
- Removes unwanted special characters
- Formats text with one sentence per line
- Preserves proper spacing and formatting

## Usage

1. Set up the virtual environment and install requirements
2. Run the scripts in sequence:
```bash
python articleDownloader.py
python textExtracter.py
python format_text.py
```

## Output Structure
```
project/
├── articles/                  # Raw HTML files
│   └── YYYY-MM-DD/            # Organized by date
├── article_texts/             # Extracted plain text files
│   └── YYYY-MM-DD/            # Organized by date
├── formatted_articles/        # Final segmented and formatted text files
│   └── YYYY-MM-DD/            # Organized by date
├── articleDownloader.py       # Script to download articles
├── textExtracter.py           # Script to extract plain text
├── format_text.py             # Script to format and segment text
└── requirements.txt           # Python dependencies
```

## Automation

To automate the pipeline for daily processing, use a task scheduler:
    Linux/Mac: Use cron to schedule the scripts.
    Windows: Use Task Scheduler to automate execution.

    # Download articles daily at 8:00 AM, extract at 9:00 AM
0 8 * * * /usr/bin/python3 /path/to/your/repo/articleDownloader.py
0 9 * * * /usr/bin/python3 /path/to/your/repo/textExtracter.py
0 9 * * * /usr/bin/python3 /path/to/your/repo/format_text.py

## Important Notes
- The scripts include delays between requests to avoid overwhelming the server
- All text is processed with UTF-8 encoding for proper Persian text handling
- The NLTK library will download required data on first run
- Make sure you have proper permissions to create directories and files
