# find_offer

Find_Offer — a Python web-scraping application that fetches discounted products from Digikala and displays current offers.

Original project description (translated): "This is my real-world project. I hope this project will be successful :)"

## Project summary

find_offer periodically scrapes product listings from Digikala (or specified categories) and identifies items with active discounts. The application provides a simple UI or API endpoint to list discounted products, their previous and current prices, discount percentage, and links to the original Digikala listing.

Important: Scraping third-party websites must follow their terms of service and robots.txt. For production use, prefer official APIs if available and ensure respectful scraping rates.

## Technologies

- Python 3.8+
- Requests / httpx for HTTP fetching
- BeautifulSoup (bs4) or lxml for HTML parsing
- Optional: Selenium for dynamic pages (if needed)
- SQLite/PostgreSQL for persistence (or simple JSON/CSV export)
- Optional: FastAPI/Flask/Django for serving results (check repo layout)

## Requirements

- Git
- Python 3.8+
- pip
- virtualenv
- (Optional) Chrome/Chromium + chromedriver if using Selenium

## Installation — exact steps (local development)

1. Clone:
   git clone https://github.com/Pouyazadmehr83/find_offer.git
   cd find_offer

2. Create and activate virtual environment
   # macOS / Linux
   python -m venv .venv
   source .venv/bin/activate

   # Windows (PowerShell)
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1

3. Install Python dependencies
   pip install -r requirements.txt

4. Configure scraping targets and rate limits
   - Edit a configuration file (config.yml/.env) or constants in the code to specify Digikala categories, frequency, and polite request headers.
   - Example config:
     BASE_URL=https://www.digikala.com
     CATEGORIES=/akcesories/   # example path
     REQUEST_DELAY=2  # seconds between requests

5. Initialize storage (if required)
   - For SQLite:
     python scripts/init_db.py  # or run migrations if using an ORM
   - Or create an empty `data/` folder for CSV/JSON outputs

6. Run scraping (example command)
   python run_scraper.py --target categories --output data/offers.json

   Or if the project provides a web server:
   uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
   # or
   flask run --host=0.0.0.0 --port=5000

7. View results
   - If CLI/JSON: open data/offers.json or data/offers.csv
   - If web UI/API: open http://localhost:8000 or /offers endpoint

## Best practices and legal/ethical notes

- Respect Digikala's robots.txt and terms of service.
- Use appropriate request headers and rate limiting to avoid overloading the site.
- Cache responses and avoid repeated identical requests.
- Consider using official APIs or partnerships for production-grade data.

## Deployment & Scheduling

- Use a scheduler (cron, systemd timers, or Celery + periodic tasks) to run the scraper at intervals.
- Containerize with Docker for reproducible deployments:
  docker build -t find_offer:latest .
  docker run -e CONFIG=prod -p 8000:8000 find_offer:latest

## Tests & Logging

- Add unit tests for parsers and integration tests with recorded HTML fixtures.
- Log failures and guard against structural changes in Digikala’s pages.

## License & Contact

- Add a LICENSE file to clarify reuse.
- Author: Pouyazadmehr83
