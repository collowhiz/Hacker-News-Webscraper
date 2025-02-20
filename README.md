# Hacker News Web Scraper

## 📌 Overview

This project is a Hacker News Scraper that extracts and analyzes top stories from Hacker News. It is built using Python, BeautifulSoup, Requests, and Pandas. The script fetches the latest articles, sorts them by upvotes, and stores the data for further analysis.

## 🚀 Features

✅ Web Scraping: Extracts article titles, links, and upvotes from Hacker News.

✅ Data Processing: Stores scraped data in a structured Pandas DataFrame.

✅ Sorting & Analysis: Ranks articles by upvotes to identify trending topics.

✅ Automation: Runs on a schedule to update the dataset continuously.

✅ Visualization: Generates bar charts of the most popular articles.

## 🔧 Tech Stack

Python: Core programming language.

BeautifulSoup: HTML parsing and web scraping.

Requests: Fetches data from Hacker News.

Pandas: Data manipulation and analysis.

Matplotlib: Data visualization.

## 📂 Installation

Clone the repository and install the required dependencies:

git clone https://github.com/your-username/hacker-news-scraper.git
cd hacker-news-scraper
pip install -r requirements.txt

## 🏗 How It Works

The script fetches the Hacker News homepage and extracts data using BeautifulSoup.

from bs4 import BeautifulSoup
import requests
import pandas as pd

response = requests.get("https://news.ycombinator.com/news")
soup = BeautifulSoup(response.text, "html.parser")

### Extract article titles and links
articles = soup.find_all("span", class_="titleline")
titles = [article.getText() for article in articles]
links = [article.find("a")["href"] for article in articles]

### Extract upvotes
upvotes = [int(score.getText().split()[0]) for score in soup.find_all("span", class_="score")]

### Create DataFrame
df = pd.DataFrame({"Title": titles, "Link": links, "Upvotes": upvotes})
df_sorted = df.sort_values(by="Upvotes", ascending=False)

## 🏋️‍♂️ Running the Scraper

Run the script manually:

python scraper.py

Or schedule it to run automatically using schedule:

import schedule
import time

schedule.every(30).minutes.do(scrape_hacker_news)

while True:
    schedule.run_pending()
    time.sleep(1)

## 📊 Data Visualization

The script generates a bar chart of the top 10 trending stories based on upvotes.

import matplotlib.pyplot as plt

def visualize_top_stories(df):
    top_n = 10
    df_top = df.head(top_n)
    plt.figure(figsize=(10, 6))
    plt.barh(df_top["Title"], df_top["Upvotes"], color="skyblue")
    plt.xlabel("Upvotes")
    plt.ylabel("Article Title")
    plt.title("Top Trending Hacker News Stories")
    plt.gca().invert_yaxis()
    plt.tight_layout()
    plt.savefig("hacker_news_top_trending.png")
    plt.show()

## 🛠 Future Improvements

Enhance error handling and logging.

Store historical data for trend analysis.

Deploy as a web application for real-time updates.

## 👨‍💻 Author

## Collins M. Muturi

📜 License

This project is open-source under the MIT License.

## ⭐ If you found this project useful, please star the repository! ⭐
