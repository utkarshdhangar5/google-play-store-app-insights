Data Preparation & Modeling Documentation
1. Project Overview

This document describes the data preparation, cleaning, transformation, validation, dimensional modeling, and relationship-building steps performed before developing the Power BI analysis and dashboard.

The project uses two primary source datasets:

Apps dataset — application-level information such as category, rating, reviews, installs, pricing, content rating, genres, and update information.
Reviews dataset — user review information along with sentiment, sentiment polarity, and sentiment subjectivity.

The objective of the preparation phase was to create a reliable analytical model while preserving the original source data for traceability.

2. Power Query Data Preparation

All data preparation was performed using Power Query in Power BI.

The workflow was divided into:

Source Data
    ↓
Staging Tables
    ↓
Data Cleaning & Transformation
    ↓
Data Validation
    ↓
Dimension / Fact Tables
    ↓
Data Modeling

3. Apps Dataset — Data Cleaning

The first dataset was loaded into Power Query and created as the staging table:

stg_Apps

The original dataset contained approximately 10,366 records.

3.1 Rating

The Rating column was investigated for:

Missing values
Invalid values
Data type consistency

The column was converted/validated as a numeric field suitable for analysis.

3.2 Reviews

The Reviews column contained values such as:

118k
18k
3.0M

These values were transformed into numeric values so that review counts could be used in calculations.

Examples:

118k → 118,000
18k  → 18,000
3.0M → 3,000,000
3.3 Size

The Size column contained values represented using units such as:

MB
k

The values were standardized into a numeric MB-based field.

A separate:

Size_MB

field was created for analytical purposes.

3.4 Installs

The Installs column contained values such as:

100,000+
1,000,000+
10,000+

The formatting characters were removed and the values were converted into a numeric field:

Installs_Num

This allows install counts to be used in Power BI calculations and visualizations.

3.5 Price

The original Price column contained values with the $ symbol.

The values were cleaned and converted into a numeric field:

Price_USD

Free applications were represented as:

0

The data was also validated to ensure that the unusual NaN type record did not create an invalid price value.

3.6 Last Updated

The Last Updated column was converted into a proper date field.

This allows the dataset to support:

Update-date analysis
Latest-version analysis
Time-based filtering
3.7 Duplicate App Records

Duplicate records were investigated rather than blindly removed.

The analysis showed that some applications had multiple records with the same or very similar app names but different values such as:

Category
Reviews
Rating
Installs
Price
Version
Last Updated
Genre

Therefore, these records were not treated as simple duplicate rows.

This was particularly evident with records such as:

I am rich
I AM RICH
I Am Rich
i am rich
I am Rich

These records contained materially different attributes and were therefore retained.

3.8 Content Rating

The Content Rating field was reviewed and contained categories including:

Everyone
Everyone 10+
Teen
Mature 17+
Adults only 18+
Unrated

No problematic null or inconsistent categories were identified during the audit.

3.9 Category

The Category field contained 32 distinct categories.

The column was checked for:

Null values
Blank values
Inconsistent category labels

No null or obvious category inconsistencies were identified.

3.10 Genres

The Genres column contained multiple genre values in some records, separated by:

;

For example:

Art & Design;Creativity

The multi-valued nature of this field was identified during the audit and retained for appropriate modeling/analysis rather than treating the combined value as a single independent genre.

3.11 Current Version

The Current Ver field was checked for missing or inconsistent values and retained as an application metadata attribute.

3.12 Android Version

The Android Ver field was audited for:

Null values
Blank values
Different device/version requirements

The field was retained as application metadata.

4. Apps Dataset — Final Dimension

After cleaning and validation, the analytical application table was created as:

dim_App

The table contains approximately:

9,659 application records

The application-level fields include attributes such as:

App
Category
Rating
Reviews
Size
Installs
Type
Price
Content Rating
Genres
Last Updated
Current Version
Android Version
Size_MB
Installs_Num
Price_USD
5. Reviews Dataset — Data Cleaning

The second dataset was loaded into Power Query as:

stg_Reviews

The original staging table contains:

64,295 review records

The review dataset contains:

App
Translated Review
Sentiment
Sentiment Polarity
Sentiment Subjectivity
5.1 Translated Review

The Translated_Review column was investigated for missing values.

There were:

5 blank review records

The records were retained because other information was still available.

5.2 Sentiment

The Sentiment column contained:

Positive
Negative
Neutral
NaN/missing

The three valid sentiment categories were retained.

Missing sentiment values were not artificially assigned to another category.

5.3 Sentiment Polarity

The Sentiment_Polarity field initially contained NaN values represented as text.

These were converted to proper null values before changing the data type to Decimal Number.

The valid range was then checked:

Minimum expected: -1
Maximum expected: +1

Validation results:

Values < -1 = 0
Values > 1  = 0

Therefore, no invalid polarity values were identified.

5.4 Sentiment Subjectivity

The Sentiment_Subjectivity field was also converted from text to a numeric field after handling the NaN values.

The expected range was:

0 to 1

Validation results:

Values < 0 = 0
Values > 1 = 0

Therefore, no invalid subjectivity values were identified.

6. App Key Validation

To connect the Apps and Reviews datasets, a normalized application key was created:

Text.Lower(Text.Trim(Text.Clean([App])))

The resulting field was named:

App_Key

This normalization was applied to both Apps and Reviews.

The purpose was to eliminate false mismatches caused by:

Capitalization
Leading/trailing spaces
Non-printing characters
7. Apps–Reviews Key Validation

The Reviews dataset was compared against the cleaned application dimension.

Results:

Total Reviews                  64,295
Matched Reviews                61,556
Unmatched Reviews               2,739

Therefore:

Match Rate       ≈ 95.74%
Unmatched Rate   ≈ 4.26%

The unmatched reviews corresponded to 54 application names that were not present in the Apps source dataset.

These reviews were not deleted.

This preserves the original review information and prevents source-data loss.

8. Identifying the App Name Grain

During relationship creation, Power BI identified duplicate values in the normalized App_Key.

Further investigation showed that some application names appeared multiple times with materially different records.

For example, I am rich appeared in multiple records with differences in:

Category
Rating
Reviews
Installs
Type
Price
Genre
Last Updated
Android Version

Therefore:

App_Key cannot be used directly as a unique primary key for the application-record table.

This was an important modeling finding.

9. Creating dim_AppName

To solve the application-name duplication issue, a separate dimension was created:

dim_AppName

The table was constructed by:

Referencing dim_App
Extracting the normalized App_Key
Removing duplicate keys
Referencing stg_Reviews
Extracting review-side App_Key
Removing duplicate keys
Appending the two lists
Removing duplicate App_Key values again

The resulting dimension contains:

9,692 unique App_Key values

A final validation confirmed:

Duplicate App_Key values = 0

Therefore, dim_AppName[App_Key] can safely function as the one-side key in the model.

10. Fact Reviews Table

The cleaned Reviews staging table was referenced to create:

fact_Reviews

The table retains the review-level grain.

Approximately:

64,295 review records

Key fields include:

App
App_Key
Translated Review
Sentiment
Sentiment Polarity
Sentiment Subjectivity

Review records were not removed simply because multiple reviews contained identical text, since identical text does not necessarily represent duplicate submissions.

11. Final Power BI Data Model

The final model uses a dimensional/star-schema-oriented structure.

                       dim_AppName
                       9,692 rows
                            │
                   ┌────────┴────────┐
                   │                 │
                  1│                1│
                   │                 │
                  *│                *│
                   ▼                 ▼
                dim_App         fact_Reviews
              9,659 rows        64,295 rows
Relationship 1
dim_AppName[App_Key]
        1
        │
        *
dim_App[App_Key]
Relationship 2
dim_AppName[App_Key]
        1
        │
        *
fact_Reviews[App_Key]

Both relationships use:

Cardinality: One-to-Many
Cross-filter: Single
Status: Active

A direct relationship between dim_App and fact_Reviews was intentionally avoided because the application name is not unique enough to safely serve as a direct key.

12. Staging vs Analytical Tables

The Power Query architecture now follows this structure:

SOURCE
  │
  ├── stg_Apps
  │
  └── stg_Reviews
        │
        ▼
TRANSFORMATION
        │
        ├── dim_App
        ├── dim_AppName
        └── fact_Reviews
        │
        ▼
POWER BI MODEL
        │
        ▼
DAX MEASURES
        │
        ▼
BUSINESS QUESTIONS
        │
        ▼
DASHBOARD

The staging tables are retained for traceability and transformation logic, while the analytical tables form the Power BI semantic model.

13. Data Quality Decisions

The following principles were followed during preparation:

Source records were not deleted without evidence that they were invalid.
Missing sentiment values were retained as missing rather than artificially classified.
Invalid numeric values were investigated before transformation.
Multi-valued fields such as Genres were identified for appropriate modeling.
App-name duplicates were investigated instead of blindly removing them.
Reviews belonging to apps absent from the Apps dataset were retained.
Normalized keys were validated before being used in relationships.
Relationships were created only after validating uniqueness on the one-side.