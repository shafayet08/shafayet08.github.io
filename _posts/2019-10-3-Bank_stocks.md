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

```python
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

```python
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
```python
     GS.head()
```
 <img src="{{ site.url }}{{ site.baseurl }}/images/Bank/Capture.JPG" alt=" GS data info">

Now I will be joining all the bank's dataframe together but before that I will make a list with the symbols of the banks and call it tickers.

```python
    tickers= ['BAC','C','GS','JPM','MS','WFC']
    bank_stock=pd.concat([BAC,C,GS,JPM,MS,WFC],axis=1,keys=tickers)
    bank_stock.columns.names=['Banks Names','Stock info']
    bank_stock.head()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/columnnames.JPG" alt=" GS data info">

Now I want to explore and look into the data. I want to know the maximum closing of the stock for the last 10 years.

```python
     # Maximum opening value
     bank_stock.xs(key = 'Close', axis = 1, level = 'Stock info').max()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/max_closing_price.JPG" alt=" GS data info">

Now I would like to see the percentage return for each of the bank stocks. For that I will first create a new database and put the return values in it.

```python

     for tick in tickers:
          returns[tick]= bank_stock[tick]['Close'].pct_change()
     returns.head()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/Pctchange_returns.JPG" alt=" GS data info">
