# Salary Estimator Project: Project Overview

- Created a tool that estimates data science salaries (MAE ~ $ 11K) to help data scientists negotiate their income when they get a job.
- Scraped job descriptions from glassdoor using python and selenium
- Engineered features from the text of each job description to quantify the value companies put on python, excel, aws, and spark.
- Optimized Linear, Lasso, and Random Forest Regressors using GridsearchCV to reach the best model.
- Built a client facing API using flask

## Code and Resources Used

**Python Version:** 3.10 \
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, selenium, flask, json, pickle \
**For Web Framework Requirements:** pip install -r requirements.txt \
**Scraper Github:** https://github.com/arapfaik/scraping-glassdoor-selenium
**Scraper Article:** https://mersakarya.medium.com/selenium-tutorial-scraping-glassdoor-com-in-10-minutes-3d0915c6d905 \
**Flask Productionization:** https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2 \
**Project main feature walk-through:** https://www.youtube.com/watch?v=fhi4dOhmW-g&list=PL2zq7klxX5ASFejJj80ob9ZAnBHdz5O1t&index=4 

## Web Scraping

Tweaked the web scraper github repo (above) to scrape 1000 job postings from glassdoor.com. With each job, we got the following:
- Job title
- Salary Estimate
- Job Description
- Rating
- Company
- Location
- Company Headquarters
- Company Size
- Company Founded Date
- Type of Ownership
- Industry
- Sector
- Revenue
- Competitors

## Data Cleaning and Engineering

I needed to clean it up so that it was usable for our model. I made the following changes and created the following variables:

- **Parsed numeric data out of salary**
  - The original data contains symbles not suit for analysis
- **Made columns for employer provided salary and hourly wages**
- **Removed rows without salary**
- **Parsed rating out of company text**
  - Rating column existed. The company text also contributes in analysis
- **Made a new column for company state**
  - Location, location, location
- **Added a column for if the job was at the company’s headquarters**
- **Transformed founded date into age of company**
- **Made columns for if different skills were listed in the job description:** Python, R, Excel, AWS, Spark
- **Column for simplified job title and Seniority**
- **Column for description length**
  - elaborare description reveals the urgent degree or the earnest of the company, could affect the salary

## EDA
<p >
<img src="https://github.com/JazenH/ds_first_proj/blob/main/Industry.png" width="450" height="450" />
<img src="https://github.com/JazenH/ds_first_proj/blob/main/Job_state.png" width="500" height="400" />
</p>





<p >
  <img src="https://github.com/JazenH/ds_first_proj/blob/main/pivot_1.png" alt="Alt Text" style="float:right" width="300"/>
  <img src="https://github.com/JazenH/ds_first_proj/blob/main/pivot_2.png" alt="Alt Text" style="float:right" width="250"/>

  <img src="https://github.com/JazenH/ds_first_proj/blob/main/salary_state_top20.png" alt="Alt Text" style="float:left" width="200"/>

</p>




