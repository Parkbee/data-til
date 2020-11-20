---
layout: post
title: Pandas Profiling
tags: [Pandas, EDA, statistics]
author: Ece Degirmenci
comment: false
---

### Background  

I have been doing some research on Pandas tips and tricks to see if I can speed up my analysis and improve my code. 
I came across a [GitHub page](https://github.com/pandas-profiling/pandas-profiling) about Pandas Profiling that could be used for quick, high level exploratory data analysis 
which requires only a with a few lines of code. 

When in need of producing basic summary statistics, Pandas has the .describe() attribute which is pretty limited and basic 
(especially considering what does Excel returns with “data analysis > descriptive statistics” ). 
This module merges .info() and .describe() attributes and returns a more in-depth, interactive report with built-in visualisations, 
and distribution of each variable. You can also share the report with others in HTML format. 

### Installation  

Install with this command: 
```
pip install pandas-profiling
```

To generate the report: 
```
import pandas_profiling
```
```
df.profile_report()
```

Save HTML 
```
df.profile_report().to_file(output_file='output.html')
```

### What I've Liked  

Warnings - shows the variables that contain NaN values, variables with many zeros, categorical variables with high cardinality etc. 
![](/data-til/assets/images/Warnings.png)

Variables -  shows all the Numerical and Categorical columns with complete statistic information 
![](/data-til/assets/images/variables.png)

Visualisations - we can get built-in histograms, or could get a Scatter Plot between two numerical variables you choose 
![](/data-til/assets/images/visualisation.png)

### Limitation

I’ve read couple reviews about this and the one disadvantage I’ve came across is its use with large datasets. 
The bigger the size of the data, the longer it takes to generate the report. A recommended solution to this is to use the minimum mode 
that was introduced in 2.4 of pandas profiling. With the minimum mode a simplified report will be generated with less information. 

```
top_garages_categories.profile_report(minimal = True)
```
