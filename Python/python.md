# 🐍 python 

This file compiles snippets of code to deal with day-to-day data science tasks, be it cleaning, processing or visualizing data. Most items should have a link to the source of salvation (i.e., the source which solved my problem). If there is no link it means it is an original (i.e., I had to figure it out myself). They range from basic knowledge (when I started coding), to more challenging tasks which required some little hacks to get the job done. As a true ptyhonist-data-scientist I frequently recurr to [Pandas](https://pandas.pydata.org/) and [NumPy](https://numpy.org/) so I assume you previouslly installed the libraries and ran the following code:

```
import pandas as pd
impor numpy as np
```
When other libraries (ex. datetime) are required, I will specifically mention their use.


### 🕐 dates and time
[Add months to a date in Python:](https://thispointer.com/add-months-to-a-date-in-python/)
```
# Import datetime library
from datetime import datetime

given_date = '1/21/2021'
# Convert date string to datetime object
date_format = '%m/%d/%Y'
dtObj = datetime.strptime(given_date, date_format)
# Add X months to a given datetime object
n = X
future_date = dtObj + pd.DateOffset(months=n)
```

Creat a function to change weeks from week-of-month to week-of-year:
```
def get_52_week(row_c1, row_c2): 
    import datetime 
    week_shift = row_c2 
    new_date = row_c1 + datetime.timedelta(weeks = week_shift - 1) 
    return new_date
```

[Slicing a Pandas dataframe with a period index with an array](https://stackoverflow.com/questions/34020777/slicing-a-pandas-dataframe-with-a-period-index-with-an-array)
```
idx = pd.period_range(1991,1993,freq='A')    
df = pd.DataFrame(np.arange(9).reshape(3,3),index=idx)
df.loc[[pd.Period('1991'), pd.Period('1993')], :]
```
[How to get date index into year-month](https://datascientyst.com/extract-month-and-year-datetime-column-in-pandas/)
```
dates = ['2021-08-01', '2021-08-02', '2021-08-03']
df = pd.DataFrame({'StartDate': dates})
df['StartDate'] = pd.to_datetime(df['StartDate'])
df['StartDate'].dt.to_period('M')
```

### 📊plotting

Plotting time-series for a column in a dataframe
```
# Import matplotlib
import matplotlib.pyplot as plt

# Create a series strating from 0 to the dataframe number of rows, incremented by one, to be used as labels
x = np.arange(0,len(df),1) 

# Create figure and axis (i.e., plot) space
fig, ax = plt.subplots(1,1) 
# Add items to plot space and plot graph
ax.plot(x,df['column']) 
ax.set_xticks(x) 
ax.set_xticklabels(df['date']) # assumes there is a column with dates named 'date'
plt.show()
```

Create a graph with different x- and y-axis, which combines two (or more) graphs (ex. two line plots) (https://stackoverflow.com/questions/42734109/two-or-more-graphs-in-one-plot-with-different-x-axis-and-y-axis-scales-in-pyth)

```
import matplotlib.pyplot as plt

x_values1=[1,2,3,4,5]
y_values1=[1,2,2,4,1]

x_values2=[-1000,-800,-600,-400,-200]
y_values2=[10,20,39,40,50]

x_values3=[150,200,250,300,350]
y_values3=[10,20,30,40,50]


fig=plt.figure()
ax=fig.add_subplot(111, label="1")
ax2=fig.add_subplot(111, label="2", frame_on=False)
ax3=fig.add_subplot(111, label="3", frame_on=False)

ax.plot(x_values1, y_values1, color="C0")
ax.set_xlabel("x label 1", color="C0")
ax.set_ylabel("y label 1", color="C0")
ax.tick_params(axis='x', colors="C0")
ax.tick_params(axis='y', colors="C0")

ax2.scatter(x_values2, y_values2, color="C1")
ax2.xaxis.tick_top()
ax2.yaxis.tick_right()
ax2.set_xlabel('x label 2', color="C1") 
ax2.set_ylabel('y label 2', color="C1")       
ax2.xaxis.set_label_position('top') 
ax2.yaxis.set_label_position('right') 
ax2.tick_params(axis='x', colors="C1")
ax2.tick_params(axis='y', colors="C1")

ax3.plot(x_values3, y_values3, color="C3")
ax3.set_xticks([])
ax3.set_yticks([])

plt.show()
```

Plot boxplot graphs for selected columns side-by-side
```
import seaborn as sns 
import matplotlib.pyplot as plt 
columns = ['A', 'B'] 
n = 1 
plt.figure(figsize=(20,15)) 
for column in columns: 
    plt.subplot(4,4,n) 
    n = n+1 
    sns.boxplot(data[column]) 
    plt.tight_layout()
```

## General snippets

Create X blocks of Y numbers:
```
n = 0 
for i in range(0, X): 
    v = 0 
    for j in range(0, Y): 
        if(v >= 10): 
            pass 
        else: 
            print(n) 
            n +=1  
            v += 1
```
NEED TO REMEMBER purpose
```
# loop through created empty dataframes 
n = 0 
for df_name, df in dict.items(): 
    # loop through parquet files 
    v = 0 
    for j in range(0, 2): 
        if(v >= 2): 
            pass 
        else: 
            chunk = pd.read_parquet(os.path.join(parquet_folder, 'parquet_' + str(n) + '.parquet')) 
            dict[df_name] = pd.concat([dict[df_name] , chunk], ignore_index= True) 
            n +=1  
            v += 1
```
[Create multiple empty dataframes](https://stackoverflow.com/questions/30635145/create-multiple-dataframes-in-loop) & [iterate over them](https://stackoverflow.com/questions/41287310/python-how-to-iterate-over-dataframes-while-using-their-name-as-a-string)
```
# create empty dataframes 
dict = {"df_" + str(i): pd.DataFrame() for i in range(0, 10)}

for df_name, df in dict.items():
```
