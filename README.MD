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

