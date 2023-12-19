---
title: Recently Graduated Data Professional Seeks Affordable Life Part 2
layout: post
post-image: \assets\images\8UR9R5F-Imgur.jpg
description: EDA and Data Analysis
tags:
- python
- data science
- technology
---

## How It's Going

1. [Introduction](#1-introduction)
2. [Income](#2-income)
3. [Rent](#3-rent)
4. [Path to Homeownership](#4-path-to-homeownership)
5. [Tax Burden](#3-tax-burden)
6. [Conclusion](#6-conclusion)


## 1. Introduction

While many factors contribute to the affordability of a living area, comparing income with housing cost is an effective place to start. For the newly graduated data professional, the greatest concern is likely to be which state will likely have the best salary paired with whether that salary can afford the rent for an apartment. As careers progress, the perspective changes to what salary is possible for the career trajectory in their state and how long it will take to become a homeowner. Additionally, since this data is viewed at a state level, this exploratory data analysis will all cover tax burden. Since the tax burden of rent varies from that of a homeowner, as well as from a junior income earner to a senior income earner, according to state property, income, and sales tax.

A note for user accessibility to data visualizations: At the time of this posting the figures shown have been uploaded in static format, due to technical issues. However, all of these graphs were generated in plotly, which means in their original form there is an ability to hover of areas of the graph to view details for each point. To view this level of data, please see the companion Streamlit dashboard for this analysis.

## 2. Income

The first distribution to explore takes the average salary by state and compares it in violin and strips plots across all industry salary averages, the average salary for Data Analysts, and the average Salary for Data Analysts. This provides a nationwide perspective of salaries by job type. Here we see that the average salary across All Job Industries for most states hovers under $60k, then tapers off steeply in to higher average salaries in certain states. For data analysts, we see not only are they earning more on average overall but that there is a less steep rise to the top of the distribution meaning that there are proportionately higher averages for data analysts across states that have lower average salaries. Data Scientists are unsurprisingly earning a much higher average salary overall, but it is interesting to note that only among a handful of states are they earning a very high salary average over $100k. An aspect of this data visible through the interactive plotly graphs is that the distribution of higher salaries in certain states than others does not necessarily correspond to state with a higher perceived cost of living. For examples, while Data Scientists in California make on average an impressive $120k per year, in Hawaii the make the lowest average of $66k despite both states being associated with high costs of living.

![Figure]({{site.url}}/assets/images/386final_eda/fig3.png)

For a closer inspection of this data, we then inspect a pair of butterfly plots. The first of which compares by State the All Industry Average Salary with the Data Analyst Average Salary, and the second compares by State the All Industry Average Salary with the Data Scientist Average Salary. Both plots share a zero-base line through the center of the graph to create a visual comparison the general average salaries to the job specific salaries, with individual average values shown.

![Figure]({{site.url}}/assets/images/386final_eda/fig1.png)
![Figure]({{site.url}}/assets/images/386final_eda/fig2.png)

Before moving onto the cost of housing, this analysis also compared performance of Job Salary above the State Average Salary to the number of jobs by type in each state using a scatterplot. For the young data professional seeking a first job in the industry, earning a job opportunity is equally important to earning a good size salary. As seen in the graph all data scientist jobs made more than the average salary in their respective state, however not all of data analyst roles made more on average in their state than state average salary, show in the red region on the graph. Additionally, some of highest ratios of job salary above state average salary for data analysts and data scientists also had the fewest number of data analyst and data scientist jobs compared to other states. California, Texas, and New York had both high salary ratios and high job counts for data analysts and scientists. While North Dakota, Vermont, Utah, Alaska, and Colorado had data analysts average salaries below the state average salary with some of the lowest job counts, and Hawaii and Colorado while above the state average had the lowest salaries for data scientist with subsequently also small job counts. 

![Figure]({{site.url}}/assets/images/386final_eda/fig4.png)

## 3. Rent

The next figure moves into an exploration of the cost of rent for that first sweet post-graduation apartment. Using a choropleth plot, this graph explores the average rent cost compared to average apartment size by state. This ratio conveniently measures cost per sq ft which was used to generate a heatmap for the most to least expensive areas. The interactive graph also provides hover detail to explore what the average is for rent and apartment sizes. On inspection, the darkest states on the map hovering around the $3 per sq ft mark not only have higher average rent costs but have the smallest average apartment sizes under 1000 sq ft. Since the heatmap is using a simple ratio, this form of measurement does not provide a comparison of the “best deal” for rent – lowest average with largest apartment size. Some states have both lower rent averages with smaller apartment sizes. Creating a “best” metric for this data would be an excellent additional opportunity for further analysis.

![Figure]({{site.url}}/assets/images/386final_eda/fig5.png)

Getting a good deal on an apartment, however, is not the only factor to consider a new graduate. Financial advisors counsel that housing costs should only cost 30% of a household monthly gross income. In fact, many apartment complexes will enforce this practice by requiring that the total gross monthly income for all adult applicants for an apartment be at least 3 times that of the monthly rent cost. This distribution uses a dot plot to map out by state the average monthly rent next the average monthly gross incomes for data analysts and data scientists. The bar in between these markers shows the amount required to cover 3xs the average rent. States where the data analyst or even data scientist marker fall within that bar region indicates states where our recent graduate will need a roommate to qualify for an apartment. This is the first figure that digs into affordability specific to data professionals, since it clearly displays state where data analysts and even data scientists are making more monthly overall but average rent is high enough that they may still need a roommate to qualify for and afford an apartment.

![Figure]({{site.url}}/assets/images/386final_eda/fig6.png)


## 4. Path to Homeownership

Eventually, there is a good chance that our data professional settles into their career and gets sick of the apartment life. With the present volatile housing landscape the next graph is a bubble chart of simply compares Average Salary by State across All Industries to the Average Monthly House Payment. This chart does not distinguish between data professionals and non-data professionals, but as we have explored already, it is easy to visualize that a data scientist is overall going to have a much easier time qualifying for a home loan than the average salary in the state, and the data analyst will vary depending on the state. The heatmap component of this graph measures median housing price. While this number is almost parallel to monthly house payment, they do vary slightly. The algorithm used to calculate monthly housing payment assumes the first time buyer is using an FHA loan with a down payment of 3.5% and PMI of 1.5% to calculate monthly mortgage cost. However, monthly house payment also include average home insurance cost and state property tax rates. States with lower home insurance and tax rates could potentially show-up in a brighter color due to higher home price, but still cost less monthly overall than a neighboring marker of a darker color. The biggest value of the heatmap here though is making expensive houses for states with lower average salaries more visible.

![Figure]({{site.url}}/assets/images/386final_eda/fig7.png)

Any first-time homebuyer will attest that in this expensive housing market, qualifying for the mortgage is only half the battle with the highest down payment costs in history. Financial advisors counsel to using the 20-30-50 rule for budgeting - 20% savings, 30% wants, 50% needs. The following percentage bar chart shows, average down payment (for a 3.5% FHA loan) to average salary per state. If our data professional is following the 20-30-50 rule then states with closing costs below the red line provided have a down payment low enough to be saved within one year’s salary. State’s above the red line will require multiple years of savings.

![Figure]({{site.url}}/assets/images/386final_eda/fig8.png)



## 5. Tax Burden

The last distribution uses polar bar charts to compare the tax burden by each state according to the data professional is a data analyst or data scientist v renter or homeowner. For this model, this assumes that our data professional has chosen to live paycheck-to-paycheck, simulate that after income tax has been deducted, the remaining amount in a worst case scenario is also being taxed with sales or property tax. The homeowner benefits from a state with lower property tax than the renter, and the data scientist making more on average benefits from lower income tax. 

![Figure]({{site.url}}/assets/images/386final_eda/fig9.png)
![Figure]({{site.url}}/assets/images/386final_eda/fig10.png)
![Figure]({{site.url}}/assets/images/386final_eda/fig11.png)
![Figure]({{site.url}}/assets/images/386final_eda/fig12.png)

## 6. Conclusion

Affordability is complex and multi-faceted. However this EDA does begin to shows patterns in which states have high cost of living with varying benefits of being a data professional. Ideally this analysis could in future be shaped as simulation tool to allow specific analysis of a prospective living area that a recently graduated data professional is considering.