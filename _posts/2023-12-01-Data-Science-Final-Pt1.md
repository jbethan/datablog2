---
title: Recently Graduated Data Professional Seeks Affordable Life Part 1
layout: post
post-image: \assets\images\8UR9R5F-Imgur.jpg
description: Data Collection and Wrangling
tags:
- python
- data science
- technology
---

## How It Started

1. [Introduction](#1-introduction)
2. [The State Conundrum](#2-state-conundrum)
3. [Acquiring the Data](#3-acquiring-data)
4. [Wrangling the Data](#4-wrangling-data)

## 1. Introduction

You did it! Late night study sessions. Midterm madness. Enough hours coding projects to binge every episode of the Office 10 times over. You got your degree and now you're moving onto your first big kid data job! But reality is times are tough for the young aspiring data professional. Your parents paid $6,000 for their entire 4 year education and bought a house for $75,000 in 1990. Meanwhile you're about to be sweating bullets whether $6,000 will cover deposit with first and last months rent for that cute little apartment you scored while leaving enough to afford a decent mattress. 

If you read that last sentence and are from an area with a lower cost of living, you probably think I just have bougie tastes. If you're from San Francisco, you're wondering if that apartment comes with 4 walls and a roof. The place you move to for your first job not only determines whether you're ordering doordash or driving for doordash after your 9 to 5, but what kind of growth is afforable as you build your future. In this economy, a big salary job straight out of school in an expensive metropolitan area could leave you worse off in 10 years than a decent salary in a more affordable area. With the "2.5 kids and a house by 30" American Dream retiring with the Baby Boomer generation, it's never been more important to understand the affordability of the areas where you're job hunting.

This analysis seeks to understand which areas in the United States provide both the best pay for data jobs when measure against their cost of living. Affordability is a broad topic with a lot of factors, but for the scope of this project we will be focusing on measuring income, housing costs, and tax burden by living area. We start to evaluate this topic by answering the questions:

1. Which areas pay the salary for data analysts and data scientists? 
2. How does this pay vary compared to the average wage across all industries in this area?
3. What is the availability of data jobs in this area?
4. How do rent costs compare to average pay for data professionals?
5. What does the path to homeownership look like for a data professional in each area?
6. How do the tax burden in each area impact affordability and does that tax burden change as a data professional earns more income and transitions from renting to home ownership?

The following variables were acquired by state to answer these questions: average wage, average salary for data analysts, average salary for data scientists, job counts, average rent, average apartment size, median house price, average closing costs, average home insurance, mortgage interest rates, and tax rates for income, property, and sales. From these variales it was possible to estimate average monthly mortgage cost, average monthly house payment, monthly gross income and monthly tax adjusted income across all industry wage averages and data professional salaries.

## 2. The State Conundrum

It's not hard to tell that each state in the US has a unique combination of cultural, geographic, and economic characteristics. States are a convenient way to organize and track data. In many cases it's an appropriate way to track data to measure the affects of state governed policies. This level of data is readily and easily available. However, the residents of any given state can attest that the area in which they live likely differs widely from other areas of their state in terms housing costs, job opportunities, and so forth. In terms of affordability, state level fails to be insightful informative especially in larger or more diverse states. 

On the other hand, county and city level datasets can quickly become expansive with 3,168 counties and 19,495 incorporated cities, towns, and villages in the US. Additionally their data can sometimes be redundant between neighboring towns and cities that share similar traits which also can make an analysis less insightful. Within the constraints of this project both of these units are too large to fit within the scope of the project. 

An alternative statistical standard used by the US government is Metropolitan Statistic Areas (MSA), which combine data for towns and counties clustered around major city areas, with populations of at least 50,000. The United States currently has 392 MSAs. One of the failings of this measurement is that the data is biased towards urban living, which not only tend to have a more expensive cost of living but also neglect important information if your dream house is on a 5 acre plot with a couple dogs and a dozen chickens. Another government standard used in response to this is Core-Based Statistical Areas (CBSA). This standard forms micropolitan statistical areas with population of at least 10,000 and less than 50,000 and combines them with MSAs to comprise 939 CSBAs. 

The downside of these units is that they are not used by all government agencies and many private groups. State level data is fundamentally easier to find. To reign in the scope of this project and provide consistency among variables, this dataset will solely focus on state level data. However this project does endeavor to form a framework that not only scratches the surface of analysis living affordability but could potentially serve as the foundation for a larger, more detailed analysis in the future.

## 3. Acquiring the Data

### Libraries Used

```python
import pandas as pd
import requests
from bs4 import BeautifulSoup
from mortgage import Loan
import re
```

## Webscraping Simple Data from Many Sources

Most the data used for this dataset was acquired using requests and BeautifulSoup to scrapes tables of state level data from websites containing only one or two variables. This applied to the variables: 

**Median House Sale Price**
**Average State Wage**
**Average Salary for Data Analysts and Job Count by State**
**Average Salary for Data Scientists and Job Count by State**
**Daily Mortgage Rate**
**Average Home Insurance Price**

All of these variable were listed by state, which served as an easy index value to combine them into a single table. The following is an example of the code used to scrape these variables from their sources. For individual code samples for each variable please view the full code in my [GitHub repository](https://github.com/jbethan/finalproj_state_affordability). 

**Example: Median Sale Price by State**

```python
url = "https://www.bankrate.com/real-estate/median-home-price/#median-price-by-state"
response = requests.get(url)
print(response.status_code)

soup = BeautifulSoup(response.text, 'html.parser')
table = soup.find_all("table")

df = pd.read_html(str(table))
# convert list to dataframe
df = pd.DataFrame(df[0])
df.head()
```

### Tax Burden by State

Tax Rates by State were pulled from [here](https://wallethub.com/edu/states-with-highest-lowest-tax-burden/20494). WalletHub doesn't prohibit webscraping under their /robot.txt policies. However after a handful of tests scraping their website, the firewall blocked my IP address. Fortunately I had made a backup csv file for this data made earlier. I assessed that even though I had been denied access for scraping that since the policies of the site itself did not prohibit the use of their publicly available data to proceed including their tax data into my dataset. I loaded these values into the dataset using the following code

```python
df3 = pd.read_csv("2023_tax_burden_backup.csv")
df3.head()

df_new = df_new.merge(df3, how = 'left', on = "State")
df_new.head()
```

### Average Rent and Apartment Size

Another variable that could not be scraped using requests was average rent and apartment size for each state. The numbers were obtained for RentCafe.com. This site again does not prohibit webscraping in their /robots.txt policies, but when the website was pinged using requests it was denied access. It did however respond to selenium and was scraped using the following code

```python
import pandas as pd
from selenium import webdriver
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.by import By
from bs4 import BeautifulSoup

url = 'https://www.rentcafe.com/average-rent-market-trends/us/?t=638379614756101989&role=renter'

driver = webdriver.Chrome(service=ChromeService(ChromeDriverManager().install()))
driver.get(url)

soup = BeautifulSoup(driver.page_source, 'html.parser')
soup_table = soup.find_all("table")[1]

table = pd.read_html(str(soup_table))
df = table[0]
df.head()

cols = ['Average Rent',	'Average Apartment Size']
df[cols]= df[cols].replace('sq. ft.', '', regex = True)
df[cols]= df[cols].replace('\$', '', regex = True)
df[cols]= df[cols].replace(',', '', regex = True).astype(float)
df.head()

# Read to CSV
df.to_csv('C:\\Users\\betha\\Documents\\stat386\\finalproj_state_affordability\\2023_average_rent_by_state.csv', index=None)

driver.close()
```

### Clean up
### Average Salary by State
Some minor cleaning had to be done to the data read from this set. For some reason the information for the state of Massachusetts was dropped when it was being scraped. However the information was provided by the original so it just had to be added back in manually. After that the values were cleaned of symbols and converted to float types for computation, as shown below.

```python
df_new = df.merge(df2, how = 'left', on = "State")
# Massachusetts in Original Dataset was Dropped from Table on Accident
df_new.at[21, "Annual Average Wage"] = '$76,600'
df_new.at[21, "Average Hourly Wage"] = '$36.83'

# Correct Read Html Error 
df_new["Average Hourly Wage"] = df_new["Average Hourly Wage"].replace('<\/\w+', '', regex = True)
df_new = df_new.dropna()

cols = ['Price',	'Annual Average Wage',	'Average Hourly Wage']
df_new[cols]= df_new[cols].replace('\$', '', regex = True)
df_new[cols]= df_new[cols].replace(',', '', regex = True).astype(float)
```

A similiar cleaning process was used for the data read into the variables for Daily Mortgage Rate. The full code can be viewed in the [GitHub repository](https://github.com/jbethan/finalproj_state_affordability) for this project.

## 4. Wrangling the Data

### Home Insurance Averages by State

While it was possible to find home insurance averages for each state, the average cost of home insurance varies widely by the cost of the home, especially since median house prices varies by state as well. To create an estimate for the average home insurance cost specific to each state's median house price. I calculated a rate from the average insurance cost divided by the house cost for each $100k home value bracket. I took the median house price from each state, searched for the price bracket it fell into, then multiplied it to the rate for the bracket and state it fit to estimate an average home insurance estimate for that price. This number was later divided into 12 payments and factored into the monthly total house payment.

```python
Clean up
cols = ['Average annual rates for $200,000 in dwelling coverage', 'Average annual rates for $300,000 in dwelling coverage',	'Average annual rates for $400,000 in dwelling coverage', 'Average annual rates for $500,000 in dwelling coverage']
df_ins[cols]= df_ins[cols].replace('\$', '', regex = True)
df_ins[cols]= df_ins[cols].replace(',', '', regex = True).astype(float)
df_ins['State']= df_ins['State'].replace('\*', '', regex = True)
df_ins.head()
```

Calculate Insurance Rate by Loan Amount

```python
df_ins["Rate at $200k"] = df_ins["Average annual rates for $200,000 in dwelling coverage"] / 200000
df_ins["Rate at $300k"] = df_ins["Average annual rates for $300,000 in dwelling coverage"] / 300000
df_ins["Rate at $400k"] = df_ins["Average annual rates for $400,000 in dwelling coverage"] / 400000
df_ins["Rate at $500k"] = df_ins["Average annual rates for $500,000 in dwelling coverage"] / 500000
df_ins.head()

for i in range(len(df_new)):
    state = df_new.loc[i, 'State']
    loan = df_new.loc[i, "Mortgage Amount"]

    if loan < 300000:
        rate = df5.loc[df5['State'] == state, 'Rate at $200k'].values.squeeze()
        df_new.loc[i,"Annual Home Insurance"] = loan * rate
    elif loan < 400000:
        rate = df5.loc[df5['State'] == state, 'Rate at $300k'].values.squeeze()
        df_new.loc[i,"Annual Home Insurance"] = loan * rate
    elif loan < 500000:
        rate = df5.loc[df5['State'] == state, 'Rate at $400k'].values.squeeze()
        df_new.loc[i,"Annual Home Insurance"] = loan * rate
    else:
        rate = df5.loc[df5['State'] == state, 'Rate at $500k'].values.squeeze()
        df_new.loc[i,"Annual Home Insurance"] = loan * rate
```

### Calculate Mortgage Loan Amount & Down Payment

For the purpose of this simulation, it was assumed that a recent college graduate would be more likely in the current housing market with high prices and high interest rates to choose an FHA loan with a 3.5% down payment for a 30 yr fixed mortgage. This assumption was used to calculate the approximate down payment and mortage loan amount. Because an FHA loan was assumed, the additional cost of Private Mortgage Insurance (PMI) which is required for FHA loans was also calculated based on the national average rate of 1.5% of the monthly mortgage payment.

```python
# Assume FHA
df_new['Mortgage Amount'] = df_new['Price'] * .965
df_new['Down Payment'] = df_new['Price'] * .035
df_new.head()

...

### PMI
df_new['PMI (1.5%)'] = df_new['Monthly Mortgage'] * 0.015
```

### Monthly Mortage Cost & Monthly House Payment

The 'mortgage' library in python was used to calculate the Monthly Mortgage cost according the number scraped for current FHA mortgage rates, the calculated mortgage loan amount, and the assumed term of 30 years. From there, the monthly estimates for property tax, PMI, house insurance were added to create a total Monthly House Payment.

```python
loan = Loan(principal = 200000, interest=.06, term=30)
loan.monthly_payment

df_new["Monthly Mortgage"] = ''
rate_col = "FHA Rate as of {}".format(date)
df_new.loc[0,"Mortgage Term"]

for i in range(len(df_new)):
    rate_col = "FHA Rate as of {}".format(date)
    principal = df_new.loc[i, "Mortgage Amount"]
    interest =float(df_new.loc[i, rate_col])
    term = df_new.loc[i,"Mortgage Term"]
    loan = Loan(principal = principal, interest = (interest/100), term = term)
    df_new.loc[i, "Monthly Mortgage"] = float(loan.monthly_payment)  

...

df_new["Monthly Housing Payments"] = ''
for i in range(len(df_new)): 
    m_mortgage = float(df_new.loc[i, "Monthly Mortgage"])
    m_propertytx = (df_new.loc[i, "Price"] *0.45* df_new.loc[i, "Property Tax Burden"]) / 1200
    m_pmi = df_new.loc[i, 'PMI (1.5%)']
    m_insurance = df_new.loc[i, 'Annual Home Insurance']/12
    df_new.loc[i,"Monthly Housing Payments"] = m_mortgage + m_propertytx + m_pmi + m_insurance
```

### Monthly Tax Adjusted Income

To generate a monthly income estimate, the annual average wage was divided by 12 months. Then to calculate a value for Monthly Tax Adjusted Income in each state, federal tax estimates were calculated by 2023 tax brackets and rates then subtracted from the monthly income. State tax was also calculated from the income tax rate that was scraped and subtracted from monthly income to generated a tax adjusted estimate. This process was applied to state average wage across all industries, then repeated for data analyst and data scientist average salaries.

```python
df_new["Monthly Individual Income"] = df_new["Annual Average Wage"]/12

df_new["Monthly Tax Adjusted Income"] = ''
for i in range(len(df_new)):
    salary = df_new.loc[i, "Annual Average Wage"]
    if salary < 44725:
        m_income = df_new.loc[i, "Annual Average Wage"]/12
        m_statetx = df_new.loc[i, "Individual Income Tax Burden"]/100
        df_new.loc[i,"Monthly Tax Adjusted Income"] = m_income * (.88 - m_statetx)
    elif salary < 95375:
        m_income = df_new.loc[i, "Annual Average Wage"]/12
        m_statetx = df_new.loc[i, "Individual Income Tax Burden"]/100
        df_new.loc[i,"Monthly Tax Adjusted Income"] = m_income * (.78 - m_statetx)
    else:
        m_income = df_new.loc[i, "Annual Average Wage"]/12
        m_statetx = df_new.loc[i, "Individual Income Tax Burden"]/100
        df_new.loc[i,"Monthly Tax Adjusted Income"] = m_income * (.88 - m_statetx)

```

This analysis used the tax brackets and rates for a single tax filer. This obviously overlooks the portion of married individuals that would be filing jointly. However, including a second household income in this simulation would alter too many variables and therefore was excluded from the scope of this project. Instead, single tax filer numbers were applie to the average income figure used, without accounting for the potential income benefits of joint filing tax status.

## On to Exploratory Data Analysis

The further adventures of our new data professional as they figure out how to afford life can be read in [Recently Graduated Data Professional Seek Afforbable Life Pt 2](https://jbethan.github.io/blog/Data-Science-Final-Pt2).

[back](../)
