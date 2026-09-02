# Google Play Store Analytics --- Question-Wise Findings & Insights

## Basic Questions

### Q1. What is the average rating of apps?

**Finding:** The average app rating is **4.17 out of 5**, indicating
generally positive user ratings across the dataset.

**Insight:** Overall user satisfaction appears strong, although
individual apps and categories can perform differently.

### Q2. How are apps distributed by size group?

**Finding:** The **\<10 MB** group contains the most apps at
approximately **5.0K**, followed by **10--25 MB (2.1K)** and **25--50 MB
(1.6K)**. Apps above 100 MB are very limited.

**Insight:** The dataset is heavily dominated by smaller-sized apps,
suggesting that developers generally favor lightweight applications.

### Q3. What proportion of apps are free vs. paid?

**Finding:** Approximately **92.17%** of apps are free, while **7.83%**
are paid.

**Insight:** Free apps strongly dominate the dataset, indicating that
the free/freemium model is far more common than paid distribution.

### Q4. What is the distribution of apps by content rating?

**Finding:** **Everyone** apps dominate the dataset with approximately
**7.9K apps**, followed by **Teen (1.0K)** and **Mature 17+ (0.4K)**.

**Insight:** Most apps target a broad audience, while relatively fewer
apps are specifically targeted toward mature users.

### Q5. Which apps have the most installs?

**Finding:** Several major apps---including Facebook, Gmail, Google,
Google Chrome, Google Drive, Google News, Google Photos, Google Play
Books, and Google Play Games---reach approximately **1 billion
installs**.

**Insight:** The highest-install segment is dominated by established
Google services and major social platforms, demonstrating the scale
achieved by widely adopted applications.

> **Note:** Multiple apps share the displayed 1.00B install value, so
> they are tied at the top.

### Q6. How many apps have a rating of 4 or higher?

**Finding:** **6,286 apps** have a rating of **4.0 or higher**.

**Insight:** A substantial portion of rated apps achieves a strong
rating threshold, indicating generally favorable user reception.

### Q7. What is the average number of reviews for free vs. paid apps?

**Finding:** Free apps have an average of approximately **234.27K
reviews**, compared with **8.72K** for paid apps.

**Insight:** Free apps attract substantially greater review engagement,
likely because their lower adoption barrier results in a much larger
user base.

### Q8. Which categories have the largest average app size?

**Finding:** **Game** has the highest average app size at approximately
**42 MB**, followed by **Family (27 MB)**. Travel & Local and Sports
average around **24 MB**.

**Insight:** Game apps tend to require more storage, potentially due to
richer graphics, media, and functionality.

### Q9. How many apps were updated in 2018?

**Finding:** **6,284 apps** were updated during 2018.

**Insight:** A large number of apps received updates in 2018, indicating
substantial maintenance and feature-development activity.

------------------------------------------------------------------------

## Medium Questions

### Q1. How does the number of installs relate to app ratings?

**Finding:** The scatter plot shows a **slight positive relationship**
between installs and ratings, although ratings vary considerably across
install levels.

**Insight:** Higher install volumes are associated with slightly higher
ratings, but installs alone do not strongly determine user satisfaction.

### Q2. Which categories have the highest average ratings?

**Finding:** **Events** has the highest average rating at **4.44**,
followed by Education (4.36), Art & Design (4.36), Books & Reference
(4.34), and Personalization (4.33).

**Insight:** These categories demonstrate strong user satisfaction, with
the top five categories maintaining average ratings above 4.3.

### Q3. What is the relationship between paid app price and ratings?

**Finding:** The trend line shows a **slight negative relationship**
between price and rating, with considerable variation across price
levels.

**Insight:** Higher pricing does not translate into higher ratings;
however, the relationship is weak and price alone is not a strong
predictor of satisfaction.

### Q4. How does average rating vary by content rating?

**Finding:** **Adults Only 18+** has the highest average rating at
approximately **4.3**, while Mature 17+ and Unrated are slightly lower
at approximately **4.1**. Other groups are around 4.2.

**Insight:** Average ratings are relatively consistent across
content-rating groups, suggesting that intended audience has limited
influence on ratings.

### Q5. Which genres have the most apps with over 1M installs?

**Finding:** **Tools** leads with **172 apps** having over 1M installs,
followed by Action (128) and Photography (123). Communication has 99 and
Productivity has 91.

**Insight:** Tools, Action, and Photography have the strongest
representation among highly installed apps.

### Q6. How many apps were updated each year?

**Finding:** App updates increased substantially over time, rising from
negligible levels in the early years to approximately **6.3K apps in
2018**. Growth became particularly noticeable from 2014 onward.

**Insight:** App development and maintenance activity expanded
significantly over time, with 2018 representing the peak update year.

### Q7. What is the relationship between app size and installs?

**Finding:** The scatter plot shows a **slight positive relationship**
between app size and installs, although there is substantial variation.

**Insight:** Larger apps tend to have somewhat higher install volumes,
but app size alone is not a strong predictor of popularity.

### Q8. Which apps have the highest number of reviews, and what are their ratings?

**Finding:** Facebook has the highest number of reviews at approximately
**78.2M**, followed by Instagram (**66.6M**) and Messenger (**56.6M**).
Clean Master has a higher rating of **4.7** despite having fewer
reviews.

**Insight:** High review volume reflects strong user engagement, but
review count does not necessarily correspond to a higher rating.

### Q9. How does the content rating distribution differ between free and paid apps?

**Finding:** Free apps heavily dominate every content-rating group. The
**Everyone** category contains **7,248 free apps** and **655 paid
apps**. Overall, there are **8,902 free apps** compared with **756 paid
apps**.

**Insight:** The dataset is strongly dominated by free applications
across all content-rating groups.

### Q10. What are the top 5 categories with the most installs?

**Finding:** **Game** leads with **13.9B installs**, followed by
Communication (11.0B), Tools (8.0B), Productivity (5.8B), and Social
(5.5B).

**Insight:** Game and Communication are the leading categories by
install volume, highlighting strong user demand for entertainment and
communication applications.

------------------------------------------------------------------------

## Advanced Questions

### Q1. How does content rating distribution differ between free and paid apps?

**Status:** **Needs correction/verification.**

The earlier visual for this question displayed individual apps with
rating, review, and install totals rather than the required
content-rating and free/paid distribution.

**Recommendation:** Use the corrected free-vs-paid content-rating visual
before adding a final business finding for Advanced Q1.

### Q2. Analyze the trend of app updates over time. Are there noticeable patterns or seasonal trends?

**Finding:** App update activity increased sharply over the analyzed
period. Updates were very low from 2010--2012, began increasing from
2013 onward, and reached approximately **6.3K in 2018**.

**Insight:** The upward trend indicates substantial growth in app
development and maintenance activity over time, with 2018 representing
the peak update period.

> **Note:** The data is aggregated by year, so it supports a yearly
> trend analysis but does **not provide enough evidence to confirm
> monthly or seasonal patterns**.

### Q3. How does the average rating of apps change with the number of installs?

**Finding:** Average ratings vary across install ranges, from
approximately **4.04 to 4.37**. The **100M+** install group has the
highest average rating at approximately **4.37**, while the
**10K--100K** group has the lowest at approximately **4.04**.

**Insight:** Very high install volume does not necessarily correspond to
lower ratings. However, the relationship is not consistently linear,
indicating that install volume alone does not determine satisfaction.

### Q4. Perform sentiment analysis on app reviews to determine common patterns in high- and low-rated apps.

**Finding:** Positive sentiment is substantially more prevalent in
high-rated apps (**38.08%**) than in low-rated apps (**13.89%**), while
negative sentiment is higher among low-rated apps (**18.61%**) than
high-rated apps (**12.56%**). Average sentiment polarity is **0.19 for
high-rated**, **0.11 for medium-rated**, and **-0.07 for low-rated**
apps.

**Insight:** Sentiment closely aligns with app ratings: high-rated apps
tend to receive more positive feedback, while low-rated apps show more
negative sentiment. This suggests that review sentiment is a useful
indicator of overall user satisfaction.

> **Note:** Unrated apps show an average polarity of 0.21, but they
> should be excluded when interpreting the relationship between rating
> and sentiment because they do not have a meaningful rating
> classification.

### Q5. What is the relationship between app genre and user ratings?

**Finding:** Ratings vary across genres. **Adventure;Brain Games** has
an average and median rating of **4.60**, while **Art & Design;Pretend
Play** has an average rating of **3.90**. The overall average rating is
**4.17**, with a median of **4.30**.

**Insight:** User ratings are generally positive across genres, but
certain genre combinations perform better or worse than others.
Differences between average and median ratings also indicate that some
genres may contain unusually high or low ratings.

------------------------------------------------------------------------

## Overall Key Takeaways

1.  The dataset is strongly dominated by **free and smaller-sized
    apps**.
2.  **Game and Communication** are among the strongest categories by
    install volume.
3.  **Events** has the highest average rating among the analyzed
    categories.
4.  Install volume has only a **weak relationship with ratings**.
5.  App update activity increased substantially, peaking in **2018**.
6.  **Positive review sentiment is associated with higher-rated apps**,
    while negative sentiment is more common among low-rated apps.
7.  The dataset shows strong adoption of established apps and major
    Google services.
