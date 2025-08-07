# Saiket_Web-Scraper_Project

#  News Scraper App

A Python project to scrape top news headlines from multiple sources (like Inshorts and BBC) and display/save them.

## Features
- GUI app using Tkinter (Inshorts)
- CLI multi-source scraper (Inshorts + BBC)
- Save headlines to TXT, CSV and JSON
- Absolutely! Let's go through a **complete, beginner-friendly explanation** of the code you received earlier for:


# ✅ **Python Code for Task 4: Basic Web Scraper + Save Headlines to Files**

## 📌 What This Code Does:

* Scrapes the **top 10 headlines** from [Inshorts](https://inshorts.com/en/read)
* Prints them
* Saves them in:

  * `.txt` – text file
  * `.csv` – spreadsheet-style
  * `.json` – structured format (used in APIs)


### 📦 Step 1: Import necessary libraries

```python
import requests
from bs4 import BeautifulSoup
import json
import csv
from datetime import datetime
```

* `requests`: Download the webpage
* `BeautifulSoup`: Parse and extract data from HTML
* `json`: Save data in JSON format
* `csv`: Save data in spreadsheet format
* `datetime`: Add timestamps to outputs


### 🔎 Step 2: Define the scraping function

```python
def scrape_headlines():
```

This defines a function that does all the work — scraping + saving.

### 🌐 Fetch the website

```python
url = 'https://inshorts.com/en/read'
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')
```

* `requests.get(url)` → downloads the webpage
* `soup = BeautifulSoup(..., 'html.parser')` → parses the HTML so  can extract specific tags like `<span>` with headlines


### 📰 Extract top 10 headlines

```python
headline_tags = soup.find_all('span', attrs={"itemprop": "headline"})
headlines = [tag.get_text(strip=True) for tag in headline_tags[:10]]
```

* `find_all(...)`: Finds all headline elements on the page
* `.get_text(strip=True)`: Extracts text without extra whitespace
* `[:10]`: Limits to top 10

### 🖨 Print the headlines

```python
print("Top News Headlines:\n")
for i, headline in enumerate(headlines, 1):
    print(f"{i}. {headline}")
```

Displays each headline in the terminal with numbering.

### 🕒 Add timestamp

```python
timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
```

Created a readable timestamp like `2025-08-07 16:15:00`.

## 🗂 Save in Different File Formats

### 📝 Save to `.txt`

```python
with open("headlines.txt", "w", encoding="utf-8") as txt_file:
    txt_file.write(f"Top News Headlines ({timestamp}):\n\n")
    for i, headline in enumerate(headlines, 1):
        txt_file.write(f"{i}. {headline}\n")
```

Creates a plain text file with numbered headlines.

### 📊 Save to `.csv`

```python
with open("headlines.csv", "w", newline='', encoding="utf-8") as csv_file:
    writer = csv.writer(csv_file)
    writer.writerow(["No", "Headline", "Timestamp"])
    for i, headline in enumerate(headlines, 1):
        writer.writerow([i, headline, timestamp])
```

Saved data in spreadsheet format. Useful for Excel or Google Sheets.


### 🧾 Save to `.json`

```python
data = {"timestamp": timestamp, "headlines": headlines}
with open("headlines.json", "w", encoding="utf-8") as json_file:
    json.dump(data, json_file, indent=2, ensure_ascii=False)
```

Saved structured data. Great for APIs, backends or reusing later.


### ✅ Done Message

```python
print("\n Headlines saved to headlines.txt, headlines.csv, and headlines.json")
```


### ▶ Run the function

```python
scrape_headlines()
```

Called the function so everything above actually happens.


## 📂 Output Files  Get

After running the script, the folder will contain:

* `headlines.txt`
* `headlines.csv`
* `headlines.json`





