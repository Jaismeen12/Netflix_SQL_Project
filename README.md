# Netflix SQL Project

📌 Project Overview
This project analyzes Netflix's movie and TV show data using SQL.  
The goal is to uncover interesting insights such as most active actors, content trends across years, genres, and countries, and to perform detailed breakdowns of the Netflix catalog.

✅ Dataset used: **Netflix Titles Dataset** (from Kaggle)  
✅ Tools used: **PostgreSQL**, **pgAdmin4**


🗂️ Dataset Information
The dataset includes details about:
- Show ID
- Type (Movie or TV Show)
- Title
- Director
- Cast
- Country
- Date added
- Release year
- Rating
- Duration
- Genre (listed_in)
- Description


🛠️ Key SQL Operations and Queries Performed

- Table Creation: 
  Created a structured table `Netflix` to hold the dataset.

- General Analysis:
  - Count total content on Netflix
  - Distinguish between Movies vs TV Shows
  - Find most common ratings for both Movies and TV Shows
  - List movies released in a specific year (example: 2020)
  - Find the top 5 countries with most Netflix content
  - Identify the longest movie by duration

- Date and Time Analysis:
  - Find content added in the last 5 years
  - Calculate year-wise content release for India and find top 5 years with highest average content released

- Person and Cast Analysis:
  - Find all movies or TV shows by "Rajiv Chilaka"
  - Find top 10 actors with the highest number of appearances in Indian movies
  - Find number of movies Salman Khan appeared in last 10 years

- Genre and Type Analysis:
  - List all movies categorized as Documentaries
  - Count number of content items per genre
  - Find TV shows with more than 5 seasons

- Missing Data and Categorization:
  - Find all content without a director
  - Categorize content based on keywords like "Kill" and "Violence" into 'Bad Content' and 'Good Content'


📊 Sample Important Queries

sql
-- Find the content added in the last 5 years
SELECT *
FROM netflix
WHERE date_added IS NOT NULL
  AND date_added ~ '^[0-9]{1,2}-[A-Za-z]{3}-[0-9]{2}$'
  AND TO_DATE(date_added, 'DD-Mon-YY') >= CURRENT_DATE - INTERVAL '5 years';

-- Find the top 5 years with highest average content release by India
SELECT 
  EXTRACT(YEAR FROM TO_DATE(date_added, 'DD-Mon-YY')) AS year,
  COUNT(*) AS content_count,
  ROUND(COUNT(*) * 1.0, 2) AS average_content_per_year
FROM netflix
WHERE date_added IS NOT NULL
  AND date_added ~ '^[0-9]{1,2}-[A-Za-z]{3}-[0-9]{2}$'
  AND country ILIKE '%India%'
GROUP BY EXTRACT(YEAR FROM TO_DATE(date_added, 'DD-Mon-YY'))
ORDER BY average_content_per_year DESC
LIMIT 5;

📁 Project Structure
Netflix_SQL_Project/
│
├── netflix_titles.csv   # Dataset
├── queries.sql           # All performed SQL queries
├── README.md             # Project overview and explanation

✨ Key Skills Demonstrated
- Advanced SQL querying
- Data cleaning and handling inconsistent date formats
- Aggregations and grouping
- Text search and string operations
- CTE (Common Table Expressions)
- Pattern matching using Regex (~)
- Ranking functions
- Basic data categorization (Good vs Bad Content)

🔥 Conclusion
This project helped in understanding how to deal with:
- Real-world messy datasets (especially inconsistent dates)
- Complex SQL queries
- Business logic building using SQL only

👩‍💻 Author
Jaismeen Kaur
📍 Data Enthusiast | Business Analyst
🔗 www.linkedin.com/in/jaismeen-kaur-5865401a5
