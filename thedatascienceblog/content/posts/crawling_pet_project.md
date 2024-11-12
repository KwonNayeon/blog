+++
title = 'Web Scraping and Text Analysis of Travel Trends on Blogs'
date = '2024-11-12'
summary = "A data-driven exploration of Taiwan travel trends using Naver blog analysis and web scraping"
description = 'A comprehensive analysis of Korean travel trends in Taiwan through web scraping, text preprocessing, and analysis of Naver blog posts'
toc = false
readTime = true
autonumber = false
math = false
tags = ["data-analysis", "web-scraping", "python", "text-analysis", "travel"]
showTags = false
hideBackToTop = false
hidePagination = true
+++
## Objective

This project explores travel trends on Naver blogs through web scraping and text analysis.

Recently, while texting with a friend who had just started exploring AI, I realized that I had no experience in crawling and scraping for data analysis. Although data pre-processing has been my specialty, I often took on data pre-processing roles in team projects and mostly relied on public data and Kaggle for my work. This realization led me to start this project.

I chose to scrape Naver blog posts about "Taiwan Travel" because I'm planning a trip to Taipei soon and wanted to understand the trends and popular keywords around this topic. (Naver is a Korean search engine, often referred to as "Korean Google.")

This pet project focuses on scraping topic-related blog posts, pre-processing the data, and conducting text analysis. I believe it's valuable to document the objective, troubleshooting process, and analysis results.

### Technologies Used
- Naver API
- Python
- Google Colab
- Basic text preprocessing techniques
- Key methods: TF-IDF, sentiment analysis, topic modeling (LDA), word cloud

While I won't explain the code line by line, you can find the complete code in my GitHub repository: [KwonNayeon/medium-post-projects](https://github.com/KwonNayeon/medium-post-projects/tree/main).

## Web Scraping with Naver API

### Legal Considerations

Before starting the project, I researched the legality of web crawling. Crawling for commercial purposes is generally not recommended, so it's essential to check each website's specific rules. Even for academic or personal projects, developers must take care to avoid causing server stress.

I initially considered X (formerly Twitter) as a data source, but their API is no longer free, and they banned crawling and scraping in 2023. Ultimately, I chose Naver's platform because they provide an official API upon application, and this aligned with my goal of analyzing Korean travel trends in Taiwan.

### Crawling Process

Following dev-woo's ["Python-based Naver blog crawling tutorial"](https://developer-woo.tistory.com/60), the process involves:

1. Fetching blog URLs for desired keywords using the Naver API (you need to apply for API access)
2. Opening URLs through Selenium to retrieve the HTML content
3. Extracting the title, content, and post date from the HTML
4. Saving the data to a CSV file

### Troubleshooting: Setting Up Selenium in Colab

I encountered issues with mounting the Chrome driver in Colab. Here's the simplified, working setup code:

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from bs4 import BeautifulSoup
import pandas as pd

# Chrome options setup
chrome_options = Options()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--no-sandbox')
chrome_options.add_argument('--disable-dev-shm-usage')

# Initialize webdriver
driver = webdriver.Chrome(options=chrome_options)
```

You can verify the setup with:

```python
try:
    driver.get('https://www.google.com')
    print("Page title:", driver.title)
    print("Setup complete!")
except Exception as e:
    print("Error:", e)
finally:
    driver.quit()
```

## Text Pre-processing and Analysis

### Pre-processing Methodology

I applied several text preprocessing techniques, including HTML tag removal, special character cleaning, case normalization, tokenization, and morphological analysis. Through this process, I learned that selecting appropriate stopwords is crucial regardless of language.

Even after using [stopwords-ko.txt](https://gist.github.com/spikeekips/40eea22ef4a89f629abd87eed535ac6a) from spikeekips' Gist on GitHub, the crawled data contained unexpected technical terms like 'pzp', 'pc', 'hdp', and 'hd' that required additional cleaning. This experience reinforced that thorough preprocessing is essential for accurate analysis.

### Text Analysis Results

#### Keyword Analysis
The most frequently appearing terms included Taiwan, Taipei, travel, tour, night market, hotel, photo, and people.

#### Sentiment Distribution
Most posts exhibited positive sentiment, focusing on travel experiences and recommendations. Representative examples included:
- Neutral: "4 nights and 5 days in Taiwan, traveling around and eating nonstop…"
- Positive: "A 3-day tour of Taiwan, a free tour around Taipei packed with experiences…"
- Positive: "Visiting the Taipei Fun Pass, with a summary of travel expenses and photos…"

#### Topic Categories
The content fell into five main categories:

1. **City Tours** — Popular destinations like Jiufen and Shifen
2. **Food & Dining** — Local cuisine and restaurant recommendations
3. **Cultural Sites** — Night markets, National Palace Museum, and historical locations
4. **Travel Tips** — Itinerary planning, tour suggestions, and essential items
5. **Travel Logistics** — Transportation guidance, eSIM information, and accommodation details

#### Word Cloud

It showed similar keywords to those in other analyses, such as Taiwan, travel, Taipei, hotel, night markets, tours, airport, and photos.
![Taiwan Travel Word Cloud](/images/wordcloud_taiwan.png)

## Key Findings

From a data analysis perspective, the results closely matched my expectations. When searching for travel information in Korean, I found a strong emphasis on food, travel tips, must-bring items, and detailed itinerary suggestions. This aligns with the types of content I anticipated encountering.

From a technical perspective, this project reinforced that text preprocessing is critical for any data analysis. While I performed basic text cleaning for this pet project, I recognized that for larger-scale or corporate projects aimed at deriving meaningful customer insights, comprehensive and accurate data cleaning is a necessity.

## Future Directions

Although this is a small-scale project, I believe the experience gained in web scraping, text preprocessing, and text analysis will be invaluable for future projects. If I get the opportunity to work on text analysis again, I plan to explore more advanced techniques for text data visualization and implement more sophisticated text cleaning methods to improve the accuracy and depth of the analysis.

While I didn't delve into explaining the code in detail in this post, you can check out the full code in my GitHub repository: [KwonNayeon/medium-post-projects](https://github.com/KwonNayeon/medium-post-projects/tree/main).

## References

- [Naver Developer API](https://developers.naver.com/main/) for web scraping
- [Python-based Naver blog crawling tutorial](https://developer-woo.tistory.com/60) by dev-woo
- [stopwords-ko.txt](https://gist.github.com/spikeekips/40eea22ef4a89f629abd87eed535ac6a) from spikeekips' Gist on GitHub
- [합법적으로 '웹 크롤링'하는 방법 (上)](https://brunch.co.kr/@8d1b089f514b4d5/33) by 삼더하기일
