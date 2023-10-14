---
title: Microsoft Introduces Python Integration to Excel in Hopes that You’ll Hate It Less
layout: post
post-image: \datablog2\assets\images\8UR9R5F-Imgur.jpg
#description: Test Post for Github Blog
tags:
- python
- excel
- anaconda
- data science
- technology
---
## Table of Contents

1. [Introduction](#1-introduction)
2. [Easy as PY](#2-easy-as-py)
3. [Create a Data Frame](#3-create-a-data-frame)
4. [Libraries](#4-libraries)
5. [Cleaning](#5-cleaning)
6. [Analysis](#6-analysis)
7. [Visualization](#7-visualization)
8. [Future for Excel and Data Folks](#8-future-for-excel-and-data-folks)

## 1. Introduction

When you got hired as a data scientist you didn’t know you would be a one-stop shop for all things data at your company, but here you are. Most days you’re so busy juggling your data analyst and data engineer hats, you wonder what was the point of getting a masters degree in data science. In fact, when the company hired you, they didn’t even have a data pipeline. You’ve bled, sweat, and shed a few tears to build your company’s data workflow from scratch and if you see one more Excel spreadsheet with its archaic, overly complex interface and inferior, tabular data keeping, so help the wayward soul who brings it across your desk.

![alt text](./meme.png)

Enter Sydney from marketing. She’s a really good friend. She’s had your back time and again. Sydney has been working her butt off to put together a big sales report for the next board meeting. She’s pulled out all the stops and applied every skill in Excel she knows for this report. This thing is gorgeous. Multiple tabbed sheets of tables with bolded, colorful headers and thoughtfully placed gridlines, bulleted and italicized key points, conditional formatting, pivot tables, formulas calculating key information, and some helpful hyperlinks for those seeking additional resources. If there was an art gallery for spreadsheets, Sydney’s report would be the showcase. However, 3 days away from the meeting, the Marketing Director has come back and told Sydney that the analytics and graphs just aren’t going to cut it and she needs to tag in the resident data guru, you.

Obviously, you’re not going hang Sydney out to dry, but you’re going to have to hack this report apart to do your thing. It’s a pain but not the most difficult thing in the world to use pandas or an excel r reading library to clean and flatten the tabs you need or even convert them into CSV files to load into your favorite Python IDE. But by the time you’re done, it’s going to look nothing like Sydney’s report and whatever you compute is going to have sent back to her and awkwardly added back in, hopefully without any adjustments that need to be sent back and forth to get the Marketing Director’s final approval before the eminent deadline.
Realistically though, Sydney’s dataset isn’t a big dataset. It’s a couple thousand lines. It doesn’t need to be handled outside of Excel. However, you need Python to use your core data libraries for cleaning, analytics, and visualization.


## 2. Easy as PY

No really, it’s as easy as “PY”. To convert a cell into a coding block, the user just needs to type “=PY(“.

![alt text](./Py1.png)
![alt text](./Py2.png)

A cell can also be converted to a Python coding block by changing the output of the ribbon from Excel Value to Python Object.

![alt text](./Py3.png)

## 3. Create a Data Frame

After the cell have been converted into a Python coding block, a data frame can be created by selecting cells with the block of data to us	e or by typing the following code in the cell: dataframe = xl( “[replace with cell range]“, headers=True). 

## 4. Libraries

The following open-source libraries are available with Python in Excel by default. They've been imported with the statements listed. 
•	matplotlib. Import statement: import matplotlib.pyplot as plt
•	NumPy. Import statement: import numpy as np
•	pandas. Import statement: import pandas as pd
•	seaborn. Import statement: import seaborn as sns
•	statsmodels. Import statement: import statsmodels as sm
In addition to the core libraries, you can import additional libraries available through Anaconda. Import Python libraries into Excel using a Python import statement in a Python in Excel cell using the following syntax:

```python
import astropy as as
```

## 5. Cleaning

Excel has traditionally struggled with data type classifications, confusing numbers, dates, and text vaguely hidden in the background of the data with clunky drop downs to reassign type. 

## 6. Statistics

## 7. Visualization

## 8. Future for Excel and Data Folks

[back](../)