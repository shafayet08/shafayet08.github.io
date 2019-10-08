---
title: "Data Analytics Project: Bank Stocks"
date : 2019-10-3
tags: [Data Analytics]
header:
 image: "/images/Bank Stock/wallstreet.jpg"
 excerpt: "Data Analytics, Stock prices"
---
In this new project I wanted to collect data from Yahoo Finance and analyze them. I collected the stock prices of 6 of the biggest banks in the world for the past 11 years and tried to analyze their stock price trends.
This project was done in Jupyter Notebook using Python and its visualization libraries.

Firstly I imported all the libraries I'll be needing for this project.

``` python
      from pandas_datareader import data, wb
      import pandas as pd
      import numpy as np
      import datetime
      import seaborn as sns
      import matplotlib.pyplot as plt
      %matplotlib inline
```
As I would like to get the stock data from Yahoo Finance I set the time period of the data I would like to gather using the datetime function.

```Python
     start = datetime.datetime(2008, 1, 1)
     end = datetime.datetime(2019, 1, 1)
```
Now I will collect the sock price data of the following 6 banks:
Bank of America
Citi group
Goldman Sachs
JPMorgan Chase
Morgan Stanley
Wells Fargo

```Python
     # Bank of America
     BAC = data.DataReader("BAC", 'yahoo', start, end)

     # CitiGroup
     C = data.DataReader("C", 'yahoo', start, end)

     # Goldman Sachs
     GS = data.DataReader("GS", 'yahoo', start, end)

     # JPMorgan Chase
     JPM = data.DataReader("JPM", 'yahoo', start, end)

     # Morgan Stanley
     MS = data.DataReader("MS", 'yahoo', start, end)

     # Wells Fargo
     WFC = data.DataReader("WFC", 'yahoo', start, end)
```
Each of the bank's dataframe contains the following information.
```Python
     GS.head()
```
 <img src="{{ site.url }}{{ site.baseurl }}/images/Bank/Capture.jpg" alt=" GS data info">
