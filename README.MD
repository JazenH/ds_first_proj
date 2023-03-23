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

I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the pivot tables.
<p >
<img src="https://github.com/JazenH/ds_first_proj/blob/main/Industry.png" width="450" height="450" />
<img src="https://github.com/JazenH/ds_first_proj/blob/main/Job_state.png" width="500" height="400" />
</p>





<p >
  <img src="https://github.com/JazenH/ds_first_proj/blob/main/pivot_1.png" alt="Alt Text" style="float:right" width="300"/>
  <img src="https://github.com/JazenH/ds_first_proj/blob/main/pivot_2.png" alt="Alt Text" style="float:right" width="250"/>

  <img src="https://github.com/JazenH/ds_first_proj/blob/main/salary_state_top20.png" alt="Alt Text" style="float:left" width="200"/>

</p>

I listed top 20 industries and states that offer data-related jobs most on the first and second images. Biotechnology and pharmaceutical companies offer overwhelmingly more postions than the rest, followed by insurance companies and computer hardware & software industry. IT service, Health care, Enterprice IT solutions stand from 4th to 6th. From 7th to 20th the trend changes slowly. 

With the average life expectancy keep growing and more and more people pay attention to health maintaince, Biotechnology and pharmaceutical companies will stand in the center of data industry for a long time in the near future. It is definitely the top 1 choice for data scientist candidates. We found that IT service and counsulting are both at very high ranks. Although many companies have their own IT department, the repidly change technology requires put the companies in a postion that they have to consult outside IT specialties frequently. Replacing a team could be a big cost, and companies with a relatively large volume may train their employees continously. IT service jobs would be even more popular as a great supply from outside of company. New grads can start the careers in a large company from entry-level and develop skills from case-practice.

We should some details of average salaries of different seniorities and job titles. Senior job gives a decent boost of payment compared to junior title. We noticed that the payment for manager is not necessarily high than the actual specific employees, however the director is paid noticably higher than other job titles, which is reasonable since normal there would only one director in each department and there are many managers connecting each section. The machine learning engineer is paid more than other job titles. Machine learning and AI are the center of the IT industry nowadays. Giant tech companies are competing in integrating the AI into the products to accelarate the work efficiecy. There would be a great need in building and maintaining the AI systems. The auto-driving, automatic robot and AGI are the future goals in the IT field, data scientists could need hard skills in machine learning to survive.

We also list the top 20 states that pay the most to data scientist. DC and CA are no double the top two states considering the politics and economics status. Illinois offer high payment to data scientist. Chicago is a economics center and there are many great IT service and consultant companies there. New York aquires a mid-top rank which is a small surprise. The reason may be that New York is more of a financial state than a technology state.

## Model building
We transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 20%.

We tried four different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.

We also OLS method in Statsmodels api to get an comprehensive understanding the linear model. 

We tried three different models:

Multiple Linear Regression – Baseline for the model
Lasso Regression – Because of the sparse data from the many categorical variables, I thought a normalized regression like lasso would be effective.
Ridge Regreesion - As a comparison to Lasso method
Random Forest – Again, with the sparsity associated with the data, I thought that this would be a good fit.

The baseline model returns a huge cross validation score. From the Statsmodels summary table we can see that there are many features which are irrelevant or should be kicked off based on the p-value. This part of features introduce loads of errors. After applying the penalty terms, both Lasso and Ridge gave
acceptable scores. 

The difference of Lasso and Ridge is the regularization term. The Ridge Regression utilize an absolute penalty term while the lasso makes use of  square penalty term. The absolute-value method punishes the irrelevant features and could reduce the weights to zero. The square-compresssion methond trys to reduce the affects of less important feature, but punishes all feature's weights.

### - Model performance
**Random Forest :** MAE = 15.5 \
**Linear Regression:** MAE = 19.34 \
**Ridge Regression:** MAE = 21.09

The Ridge Regression performed slightly better than the Lasso Regression. As mentioned above that there are many irrelevant features. The Ridge method is more suited in handling abandon features. As we cen see the Random Forest model gave the best score, which surprices no no because there are many categorical variables. 
We also use GridSearchCV to optimize the Random Forest model. We obtained a higher scoer, **17.51**. This can be explained by a bias-variance trade off.

## Productionization
We built a flask API endpoint that was hosted on a local webserver by following along with the TDS tutorial in the reference section above. The API endpoint takes in a request with a list of values from a job listing and returns an estimated salary.
