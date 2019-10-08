---
title: "Data Analytics Project: Bank Stocks"
date : 2019-10-3
tags: [Data Analytics]
header:
 image: "/images/Bank/wallstreet.jpg"
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
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/max_closing_price.JPG" alt=" Closing prices">

Now I would like to see the percentage return for each of the bank stocks. For that I will first create a new database and put the return values in it.

```python
     for tick in tickers:
          returns[tick]= bank_stock[tick]['Close'].pct_change()
     returns.head()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/Pctchange_returns.JPG" alt=" Returns Dataframe">

 A line chart to show the trend in Return for the banks stocks over the last decade.

```python
     plt.figure(figsize=(10,10))
     for tick in returns:
         returns[tick].plot()
     plt.legend()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/returns_graph.JPG" alt=" Returns trend">

The dates at which the percentage return was the highest and the lowest.

Minimum Returns
```python
     returns.idxmin()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/min_returndate.JPG" alt=" Returns trend">

Maximum Returns
```python
     returns.idxmax()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/max_returndate.JPG" alt=" Returns trend">


Now I would like to know how risky the stocks are. For that I  will have to look at the standard deviation of the returns of the stock prices.

```python
     returns.std()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/standarddeviation.JPG" alt=" Returns trend">

It can be seen that out of all the banks, Bank of America had the riskiest stocks.

For the year 2018,

```python
    returns.ix['2018-01-01':'2018-12-31'].std()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/2018returnstd.JPG" alt=" Returns trend">

For the year 2018 all of the 5 banks were pretty much had the same low risk stocks.

A distribution plot of the percentage Return for Morgan Stanley for the year.
2018:
```python
    sns.distplot(returns.ix['2018-01-01':'2018-12-31']['MS'],color='red')
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/Morganstanely_return2018.JPG" alt=" Returns trend">

2009:
```python
    sns.distplot(returns.ix['2009-01-01':'2009-12-31']['MS'],color='red',bins =50)
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/Morgan2009return.JPG" alt=" Returns trend">

Stock price trend of all 6 banks for the last decade.

```python
    for tick in tickers:
        bank_stock[tick]['Close'].plot(label = tick, figsize=(12,10))
    plt.legend()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/Stock_prices.JPG" alt=" Returns trend">

30 day closing average for the Goldman Sachs for the year 2018.

```python
# Goldman Sachs
    plt.figure(figsize=(12,6))
    GS['Close'].ix['2018-01-01':'2018-12-31'].rolling(window=30).mean().plot(label='30 Day Avg')
    GS['Close'].ix['2018-01-01':'2018-12-31'].plot(label='GS CLOSE')
    plt.legend()

```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/GSmovingA2018.JPG" alt=" Returns trend">


Lastly the correlation between the stocks of the banks.

```python
     bank_stock.xs(key='Close',axis=1,level = 'Stock info').corr()
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/correlation.JPG" alt=" Returns trend">

```python
     sns.clustermap(bank_stock.xs(key='Close',axis=1,level = 'Stock info').corr(),annot = True)
```
<img src="{{ site.url }}{{ site.baseurl }}/images/Bank/corrclustermap.JPG" alt=" clustermap map">
