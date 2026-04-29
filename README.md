# 🧠 AI Review Sentiment Automation (n8n)

This project is an end-to-end automation pipeline that collects Google Maps reviews, classifies them using AI, and generates a visual report sent via email.

---

## 🚀 Overview

This workflow automates:

1. Fetching Google Maps reviews (Brandenburg Gate)
2. Cleaning and preparing text data
3. Classifying reviews into categories using OpenAI:
   - Travel
   - Architecture
   - Service
   - Crowds
   - History
4. Storing results in Google Sheets
5. Aggregating category counts
6. Generating a chart (QuickChart API)
7. Sending a report via Gmail

---

## 🛠️ Tech Stack

- **n8n** – workflow automation
- **OpenAI API** – text classification
- **Google Maps API** – review data
- **Google Sheets API** – data storage
- **QuickChart API** – visualization
- **Gmail API / SMTP** – email delivery

---

## 🔄 Workflow

![Workflow](workflow.png)
> Note: Due to Google Places API limitations, each execution processes up to 5 latest reviews. The system is designed to run repeatedly and accumulate data over time.
---

## 📊 Example Output

- Categorized reviews stored in Google Sheets
- Automated doughnut chart showing distribution
- Email report with attached visualization

---

## ⚙️ Setup Instructions

### 1. Clone repo
```bash
git clone https://github.com/YOUR_USERNAME/ai-review-sentiment-automation.git
## ⚠️ Current Limitation (Important)

The current implementation retrieves only the **latest 5 Google Maps reviews**.

### Why?

This is due to the Google Places API behavior:

- The `Place Details` endpoint returns a **maximum of 5 reviews per request**
- Reviews are not paginated
- There is **no official way to fetch all historical reviews** via the standard API

👉 As a result, the workflow processes only a small sample of recent reviews.

---

## 🧠 Impact on Analysis

- The generated chart reflects **recent sentiment only**
- It does NOT represent full historical trends
- Results may be biased depending on recent activity

---

## 🚀 Scaling Solutions

To scale beyond this limitation, several approaches can be used:

### 1. Incremental Data Collection (Recommended)

Run the workflow on a schedule (e.g., daily) and:

- Append new reviews to Google Sheets
- Avoid duplicates by checking:
  - Review text
  - Timestamp

👉 Over time, you build your own dataset.

---

### 2. Third-Party Data Providers

Use external services that provide extended review access:

Examples:
- SerpAPI
- Outscraper

Pros:
- Access to more reviews

Cons:
- Paid
- External dependency

---

### 3. Web Scraping (Advanced)

Scrape reviews directly from Google Maps UI.

Pros:
- More complete data

Cons:
- Against Google Terms of Service
- Requires maintenance
- Risk of blocking

---

### 4. Switch Data Source

Instead of Google Maps:

- Booking.com
- TripAdvisor
- Yelp

These platforms may offer:
- APIs
- Easier scraping
- Larger datasets

---

## 🔧 Recommended Approach for This Project

This project uses:

👉 **Incremental data collection via scheduled runs**

This allows:

- Building a dataset over time
- Maintaining compliance with API limitations
- Creating trend-based analysis in the future

---

## 📈 Future Improvement

- Add duplicate detection logic
- Store unique review IDs
- Track sentiment changes over time
- Build time-series dashboard
