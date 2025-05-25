
# 📊 Analyzing-Historical-Stock-Revenue-Data-and-Building-a-Dashboard 📈

---

## 🚀 Project Overview

Welcome to the **Analyzing-Historical-Stock-Revenue-Data-and-Building-a-Dashboard** project! This project guides you through the essential steps of extracting stock and revenue data from multiple sources and visualizing it effectively. This is a key skill for data scientists and analysts to make informed decisions based on real-world financial data.

---

## 📚 Table of Contents

1. 🛠️ Define a Graphing Function
2. 🔍 Question 1: Extract Tesla Stock Data using `yfinance`
3. 🌐 Question 2: Extract Tesla Revenue Data via Web Scraping
4. 🔍 Question 3: Extract GameStop Stock Data using `yfinance`
5. 🌐 Question 4: Extract GameStop Revenue Data via Web Scraping
6. 📈 Question 5: Plot Tesla Stock and Revenue Graph
7. 📉 Question 6: Plot GameStop Stock and Revenue Graph

---

## ⏳ Estimated Time Needed

**30 minutes** — A quick yet insightful journey into stock data extraction and visualization!

---

## 🛠️ Setup & Requirements

Before starting, ensure you have the necessary Python libraries installed. If working locally (e.g., Anaconda), run the following commands:

```bash
!pip install yfinance
!pip install bs4
!pip install nbformat
```

---

## 📦 Libraries Used

* `yfinance` — For fetching historical stock data 📅
* `requests` — To download web pages 🌍
* `BeautifulSoup` — For parsing HTML and scraping revenue tables 🕸️
* `pandas` — For data manipulation 🐼
* `plotly` — For interactive visualizations 📊
* `warnings` — To ignore unnecessary warnings ⚠️

---

## 🧩 Step-by-Step Guide

### 1. Define the Graphing Function 🎨

We define a reusable `make_graph()` function to plot **Historical Share Price** and **Historical Revenue** on two subplots for any given stock:

```python
def make_graph(stock_data, revenue_data, stock):
    # Function plots price and revenue side by side
    ...
    fig.show()
```

---

### 2. Question 1: Extract Tesla Stock Data using `yfinance` 🔍

* Create a ticker object for Tesla (`TSLA`)
* Download max period historical stock data
* Reset index and preview the dataset

```python
import yfinance as yf

tesla = yf.Ticker("TSLA")
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)
tesla_data.head()
```

---

### 3. Question 2: Extract Tesla Revenue Data by Web Scraping 🌐

* Fetch Tesla revenue data from a provided URL
* Parse HTML with BeautifulSoup
* Extract revenue table and clean data (remove commas, dollar signs, nulls)

```python
import requests
from bs4 import BeautifulSoup

url = 'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm'
html_data = requests.get(url).text
soup = BeautifulSoup(html_data, 'html.parser')

tables = soup.find_all('table')
tesla_revenue = pd.read_html(str(tables[1]), flavor='bs4')[0]
tesla_revenue.columns = ['Date', 'Revenue']

tesla_revenue['Revenue'] = tesla_revenue['Revenue'].astype(str).str.replace(r'[,$]', '', regex=True)
tesla_revenue.dropna(inplace=True)
tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
tesla_revenue.tail()
```

---

### 4. Question 3: Extract GameStop Stock Data using `yfinance` 🔍

* Repeat the process for GameStop (`GME`) stock data
* Reset index and preview

```python
gme = yf.Ticker("GME")
gme_data = gme.history(period="max")
gme_data.reset_index(inplace=True)
gme_data.head()
```

---

### 5. Question 4: Extract GameStop Revenue Data by Web Scraping 🌐

* Fetch GameStop revenue data from the provided URL
* Parse HTML and extract revenue table
* Clean the revenue data

```python
url = 'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html'
html_data_2 = requests.get(url).text
soup = BeautifulSoup(html_data_2, "html.parser")

tables = soup.find_all("table")
gme_revenue = pd.read_html(str(tables[1]), flavor='bs4')[0]
gme_revenue.columns = ['Date', 'Revenue']

gme_revenue['Revenue'] = gme_revenue['Revenue'].astype(str).str.replace(r'[,$]', '', regex=True)
gme_revenue.tail()
```

---

### 6. Question 5: Plot Tesla Stock and Revenue Graph 📈

Use the predefined `make_graph` function to visualize Tesla’s stock price and revenue history.

```python
make_graph(tesla_data, tesla_revenue, 'Tesla')
```

---

### 7. Question 6: Plot GameStop Stock and Revenue Graph 📉

Similarly, plot GameStop’s stock price and revenue.

```python
make_graph(gme_data, gme_revenue, 'GameStop')
```

---

## 📝 Notes & Tips

* The `make_graph` function plots data only up to mid-2021 for better consistency.
* To avoid clutter, warnings related to deprecated parameters are filtered out.
* Always clean your data (remove special characters, handle missing values) before plotting.
* Use `reset_index(inplace=True)` after downloading data to work with the DataFrame more easily.

---

## 💡 Summary

This project demonstrates:

* How to extract **financial stock data** using APIs like `yfinance`
* How to perform **web scraping** to extract tabular revenue data
* Cleaning and preparing data for analysis
* Creating **interactive plots** to visualize financial trends over time

---

## 🙋🏿‍♂️ Questions?

Feel free to reach out if you want help with any part of the project or data visualization techniques!

---

## 📜 License

This project is open for learning and educational purposes. Use responsibly!

---

✨ Happy Coding & Data Visualizing! 📊🚗💰

---

