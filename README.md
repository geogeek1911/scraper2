# Scraper2

Streamlined web crawler for rental listings

![alt tag](https://raw.githubusercontent.com/mxndrwgrdnr/scraper2/master/rentsqft_by_week.png)

### What it does

The `scraper2` directory defines a generalized Craigslist rental listing crawler, and scripts like `test_scraper.py` and `scrape_prior_day.py` instantiate it with particular lists of search domains, time parameters, and other settings. 

Functionality is similar to `ClistRentScraper` (developed by Geoff in 2014), but the operations are now defined explicitly rather than as `Scrapy` projects. This should make the crawler easier to maintain and debug. We use the `Requests` library for HTTP requests and `Lxml` to parse webpage content. 

The crawler begins by loading a page of Craigslist search results, for example http://sfbay.craigslist.org/search/apa. From that page, it parses each listing's title, url, price, characteristics, and timestamp. Next, it visits each listing url to extract addresses and lat-lon coordinates. Then it moves on to the next page of search results and repeats the process. 

The data is saved to a CSV file, and diagnostics and errors are saved to a log file.

`ClistRentScraper` only kept lat-lon coordinates, but Craigslist listings now also include a location accuracy indicator and an address or cross streets, when users have provided it. `Scraper2` saves this data for future analysis.


### Status

This project is on hold while we look into more official access to Craigslist data.


### Task list (higher priority)

- Add Slack status notification.

- Bin the domains/regions into those that need more frequent updates and those that don't. We shouldn't need to scrape regions in Abilene, TX every hour.

- Write unit tests.


### Task list (lower priority)

- Allow for duplicate listings if price has changed (i.e. make a new unique key in psql db)

- Improve log messages.

- Is the list of data fields we're collecting optimal? 

- Check the master list of Craigslist domains that we're crawling, which was compiled by Geoff in 2014. Is there a way to assemble the list programmatically, to make sure it's always up to date?

