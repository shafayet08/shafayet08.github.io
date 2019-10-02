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
