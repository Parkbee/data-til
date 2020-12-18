---
layout: post
title: Pandas Profiling
tags: [Pandas, EDA, statistics]
author: Ece Degirmenci
comment: false
---

### Background  

I have been doing some research on Pandas tips and tricks to see if I can speed up my analysis and improve my code. 
I came across a [GitHub page](https://github.com/pandas-profiling/pandas-profiling) about `Pandas Profiling` that 
could be used for quick, high level exploratory data analysis which requires only a few lines of code. 

When in need of producing basic summary statistics, Pandas has the .describe() attribute which is pretty limited and basic 
(especially considering what does Excel returns with “data analysis > descriptive statistics” ). 
This module combines the .info() and .describe() attributes and returns a more in-depth, interactive report with built-in visualisations, 
and distribution of each variable. You can also save and share it in a HTML or JSON format. 

### Installation  

Install with this command: 
```
pip install pandas-profiling
```

To generate the report: 
```
from pandas_profiling import ProfileReport
profile = ProfileReport(df, title="Profiling Report")
```

Saving the report
```
profile.to_file("report.html")
profile.to_file("report.json")
```

### What I've Liked  

* Warnings: shows the variables that contain NaN values, variables with many zeros, categorical variables with high cardinality etc. 
* Variables: shows all the Numerical and Categorical columns with complete statistic information 
* Visualisation: we can get built-in histograms, or could get a Scatter Plot between two numerical variables you choose 

### Limitation

I’ve read couple reviews about this and the one disadvantage I’ve came across is its use with large datasets. 
The bigger the size of the data, the longer it takes to generate the report. A recommended solution to this is to use the minimum mode 
that was introduced in 2.4 of pandas profiling. With the minimum mode a simplified report will be generated with less information. 

```
profile = ProfileReport(large_dataset, minimal=True)
profile.to_file("report.html")
```
