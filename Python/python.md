# 🐍 python 

This file compiles snippets of code to deal with day-to-day data science tasks, be it cleaning, processing or visualizing data. Most items should have a link to the source of salvation (i.e., the source which solved my problem). They range from basic knowledge (when I started coding), to more challenging tasks which required some little hacks to get the job done. As true ptyhonist-data-scientist I frequently recurr to [Pandas](https://pandas.pydata.org/) and [NumPy](https://numpy.org/) so I assume you previouslly installed and ran the libraries:

```
import pandas as pd
impor numpy as np
```

## General snippets


[Add months to a date in Python](https://thispointer.com/add-months-to-a-date-in-python/)
```
future_date = dtObj + pd.DateOffset(months=n)
```
Plotting period series in matplotlib pyplot
```
x = np.arange(0,len(df),1) 
fig, ax = plt.subplots(1,1) 
ax.plot(x,df['rev']) 
ax.set_xticks(x) 
ax.set_xticklabels(df['date']) 
plt.show()
```
Slicing a Pandas dataframe with a period index with an array
```
df.loc[[pd.Period('1991'), pd.Period('1993')], :]
```
How to Extract Month and Year from DateTime column in Pandas
```
df['StartDate'] = pd.to_datetime(df['StartDate'])
df['StartDate'].dt.to_period('M')
```
