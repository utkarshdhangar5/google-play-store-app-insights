# Data Dictionary — Google Play Store Analytics

## Overview

This data dictionary describes the columns used in the final Power BI data model.

The final model contains:

- `dim_App` — app-level information and analytical attributes
- `dim_AppName_Final` — unique application key dimension
- `fact_Reviews` — review-level data and sentiment analysis
- `Measures` — DAX measures used for analysis

---

## 1. `dim_App`

| Column | Description |
|---|---|
| `App` | Name of the application. |
| `App_Key` | Standardized application key created from the app name and used to connect app-related records across the model. |
| `Category` | Category assigned to the application. |
| `Rating` | Average user rating of the application, measured on a 1–5 scale. |
| `Reviews` | Number of user reviews associated with the application. |
| `Size_MB` | Application size converted into a numeric value in megabytes (MB). |
| `Installs_Num` | Installation count converted from the original install-range values into a numeric value. |
| `Type` | Indicates whether the application is Free or Paid. |
| `Price_USD` | Application price converted into a numeric USD value. |
| `Content Rating` | Content/audience classification assigned to the application. |
| `Genres` | Genre or genre combination associated with the application. |
| `Last Updated` | Date on which the application was last updated. |
| `Current Ver` | Current version of the application. |
| `Android Ver` | Minimum Android version required to run the application. |
| `Install bin` | Installation range created for binned analysis of installs and ratings. |
| `Install Bin Sort` | Numeric sorting column used to display installation bins in the correct logical order. |
| `Rating Group` | Rating-based classification used for analysis: High Rated, Medium Rated, Low Rated, or Unrated. |

### `Install bin` Categories

| Bin | Meaning |
|---|---|
| `<1K` | Fewer than 1,000 installs |
| `1K–10K` | 1,000 to fewer than 10,000 installs |
| `10K–100K` | 10,000 to fewer than 100,000 installs |
| `100K–1M` | 100,000 to fewer than 1 million installs |
| `1M–10M` | 1 million to fewer than 10 million installs |
| `10M–100M` | 10 million to fewer than 100 million installs |
| `100M+` | 100 million or more installs |

### `Rating Group` Categories

| Group | Meaning |
|---|---|
| `High Rated` | Apps with a rating of 4.0 or higher |
| `Medium Rated` | Apps with a rating greater than 3.0 and less than 4.0 |
| `Low Rated` | Apps with a rating of 3.0 or lower |
| `Unrated` | Apps where the rating is blank |

---

## 2. `dim_AppName_Final`

This table contains the unique application keys used as the central app-level dimension in the final data model.

| Column | Description |
|---|---|
| `App_Key` | Unique standardized application identifier used to connect application records with review records. |
| `App Average Rating` | Average rating calculated for the corresponding `App_Key`. |
| `Rating Group` | Rating classification for the corresponding application key, used to compare app ratings with review sentiment. |

---

## 3. `fact_Reviews`

This table contains individual app review information and sentiment-analysis results.

| Column | Description |
|---|---|
| `App` | Application associated with the review. |
| `App_Key` | Standardized application key used to connect the review to the app dimension. |
| `Sentiment` | Sentiment classification assigned to the review: Positive, Neutral, or Negative. |
| `Sentiment_Polarity` | Numerical score representing the direction and strength of the review's sentiment. |
| `Sentiment_Subjectivity` | Numerical score representing how subjective or opinion-based the review is. |
| `Translated_Review` | Review text used for sentiment and qualitative theme analysis. |

---

## 4. `Measures`

The `Measures` table is a dedicated table created to keep DAX measures organized separately from the data tables.

| Measure | Description |
|---|---|
| `Average App Rating` | Calculates the average rating of apps in the current filter context. |
| `Median App Rating` | Calculates the median rating of apps in the current filter context. |
| `Average Sentiment Polarity` | Calculates the average sentiment polarity of reviews in the current filter context. |
| `Average Days Between Updates` | Calculates the average number of days between consecutive app updates. |
| `Reviews per Install` | Calculates the ratio of total reviews to total installs. |
| Other analytical measures | Additional DAX calculations created to support the project's business questions and dashboard analysis. |

---

## 5. Key Fields

### `App_Key`

`App_Key` is the primary linking field used throughout the final model. It standardizes app names and allows records representing the same application to be connected across tables.

### `Last Updated`

`Last Updated` is stored as a date and is used to analyze app update activity and the time between consecutive updates.

### `Installs_Num`

`Installs_Num` is the numeric version of the original install-range field and is used for install-based comparisons, rankings, and binned analysis.

### `Price_USD`

`Price_USD` is the numeric version of the original price field and is used for price-based analysis.

---

## 6. Data Model Relationship

The final model uses `dim_AppName_Final` as the central application key dimension:

```text
dim_AppName_Final
        |
        | App_Key
        |
   +----+----+
   |         |
   v         v
dim_App   fact_Reviews
```

`App_Key` provides the connection between application-level information and review-level information.

---

## 7. Purpose of the Data Dictionary

This document provides a reference for understanding the meaning, purpose, and analytical use of each field in the final Power BI data model. It is intended to make the dataset easier to understand, maintain, and use for future analysis.
