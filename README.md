## 🍺 Beer Review Analysis & Recommendation System
## 📌 Project Overview

This project analyzes a large-scale beer review dataset (~500K+ records) to uncover patterns in user preferences, product characteristics, and review behavior. The analysis focuses on transforming raw event-level review data into meaningful insights and building foundations for recommendation systems.

## 📊 Dataset Summary
Rows: 528,870
Columns: 13
Source: Public beer review dataset
Key Features:
Beer attributes: beer_ABV, beer_style, beer_brewerId
Review scores: review_overall, review_taste, review_aroma, review_palette, review_appearance
User info: review_profileName
Text data: review_text
Timestamp: review_time

Each row represents a review event, meaning users can review the same beer multiple times.

## ⚙️ Data Preprocessing
🔹 Cleaning Steps
Removed invalid ratings (e.g., zeros in key fields)
Dropped missing values
Reduced dataset to 508,355 clean observations
🔹 Handling Duplicate Reviews 

Users can review the same beer multiple times. To avoid bias:

df_sorted = df_cleaned.sort_values(by="review_overall", ascending=False) \
    .drop_duplicates(subset=["review_profileName", "beer_beerId"], keep="first")

Final dataset: 503,697 rows

## 📈 Key Analyses & Results
⭐ Q1: Strongest Breweries (by ABV)
Aggregated mean ABV per brewery
Ranked top producers of high-alcohol beers

Top 3 Breweries:

Brewer 6513 → Avg ABV: 19.23
Brewer 736 → Avg ABV: 13.75
Brewer 24215 → Avg ABV: 12.47

⭐ Q2: Best Year for Beer Ratings
Extracted year from timestamps
Computed average rating per year

Key Insight:

Year 2000 had highest average rating but insufficient data
2010 identified as most reliable peak year due to larger sample size

⭐ Q3: What Drives Beer Ratings?

Used correlation analysis between attributes and overall rating.

Findings:

Aroma → strongest predictor (~0.87 correlation)
Taste → second strongest
Palette → moderate
Appearance → least important

⭐ Q4: Beer Recommendation Strategy

Goal: recommend beers based on both quality and popularity

Approach:

Aggregate mean rating + number of reviews
Filter beers with >200 reviews to ensure reliability

Top Recommended Beers:

Heady Topper
Citra DIPA
Founders CBS Imperial Stout

⭐ Q5: Favorite Beer Style (NLP Analysis)

Used VADER sentiment analysis on review text.

Top Style:

Quadrupel (Quad)

Insight:

Sentiment vs rating correlation ≈ 0.26 (low but positive)

## 🧠 Key Data Science Concepts Demonstrated
Event → Entity transformation
Handling duplicate user interactions
Bias from small sample sizes
Feature importance via correlation
Ranking with confidence thresholds
NLP sentiment analysis (VADER)
Recommendation system foundations
