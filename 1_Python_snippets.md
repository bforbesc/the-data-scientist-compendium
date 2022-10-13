# <img height=50 src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" /> Python - Snippets

This file compiles snippets of code to deal with day-to-day data science tasks, be it cleaning, processing or visualizing data. Most items should have a link to the source of "salvation" (i.e., the source which solved my problem). If there is no link it means that it is either an original (i.e., I had to figure it out myself) or I simply lost the link. The code ranges from basic knowledge, to more challenging tasks which required some little hacks to get the job done. I frequently recurr to [Pandas](https://pandas.pydata.org/) and [NumPy](https://numpy.org/) so I assume you have previouslly installed the libraries and ran the following code:

```python
import pandas as pd
import numpy as np
```
When other libraries are required, I will specifically mention their use. The use of ```df``` refers to a general Pandas DataFrame object.

# Table of contents
1. [Setting up your working environment](#setting-up-your-working-environment)
2. [Dates and time](#dates-and-time)
3. [Visualization](#visualization)
4. [Working with Pandas DataFrame and NumPy array objects](#Working-with-Pandas-DataFrame-and-NumPy-array-objects)
5. [General Python snippets](#General-Python-snippets)


# Setting up your working environment

[Setting up a global seed for your project](https://www.mikulskibartosz.name/how-to-set-the-global-random_state-in-scikit-learn/)
```python
np.random.seed(31415)
```

Show all columns and rows of a data frame in your output/ notebook
```python
pd.set_option("display.max_columns", None)
pd.set_option("display.max_rows", None)
```

[How to print multiple outputs in the same cell in a Jupyter notebook](https://www.roelpeters.be/jupyter-notebooks-how-to-print-multiple-outputs-in-a-cell/)
```python
from IPython.core.interactiveshell import InteractiveShell 
InteractiveShell.ast_node_interactivity = 'all'
```

[Show a progress for cell being run](https://stackoverflow.com/questions/59953611/how-can-i-get-a-tqdm-progress-apply-bar-in-vs-code-notebooks)
```python
from tqdm.notebook import tqdm
tqdm.pandas()
```

## Dates and time 
For this section you will need to have installed the [```datetime```](https://docs.python.org/3/library/datetime.html) module and run the following code:
```python
# Import datetime library from datetime module (an unfortunate choice of names)
from datetime import datetime
```

[Add months to a date in Python](https://thispointer.com/add-months-to-a-date-in-python/)
```python
given_date = '1/21/2021'

# Convert date string to datetime object
date_format = '%m/%d/%Y'
dtObj = datetime.strptime(given_date, date_format)

# Add, for instance, 10 months to a given datetime object
n = 10
future_date = dtObj + pd.DateOffset(months=n)
```

[Slicing a Pandas dataframe with a "period index" with an array of periods](https://stackoverflow.com/questions/34020777/slicing-a-pandas-dataframe-with-a-period-index-with-an-array)
```python
idx = pd.period_range(1991,1993,freq='A')    
df = pd.DataFrame(np.arange(9).reshape(3,3),index=idx)
df.loc[[pd.Period('1991'), pd.Period('1993')], :]
```

[How to get date index into year-month](https://datascientyst.com/extract-month-and-year-datetime-column-in-pandas/)
```python
dates = ['2021-08-01', '2021-08-02', '2021-08-03']
df = pd.DataFrame({'StartDate': dates})
df['StartDate'] = pd.to_datetime(df['StartDate'])
df['StartDate'].dt.to_period('M')
```

[Drop duplicates, keep most recent date](https://stackoverflow.com/questions/52395820/drop-duplicates-keep-most-recent-date-pandas-dataframe)
```python
df.sort_values('DATE_CHANGED').drop_duplicates('STATION_ID',keep='last')
```

[Check if a date is between dates/ date range](https://stackoverflow.com/questions/47545090/how-can-i-check-if-date-is-on-range-on-python)
```python
TODAY_CHECK = datetime.datetime.now()
start = datetime.datetime(day=26,month=11,year=2017)
end = datetime.datetime(day=30,month=11,year=2017)
if start <= TODAY_CHECK <= end:
    print "PASS!"
else:
    print "YOU SHALL NOT PASS, FRODO."
```

[Force months/ weeks to be 2 digits](https://stackoverflow.com/questions/20990863/python-pandas-add-leading-zero-to-make-all-months-2-digits)
```python
df["Month"] = df.Month.map("{:02}".format)
```

[Combine two columns of numbers as text]()
```python
df["period"] = df["Year"].astype(str) + df["quarter"].astype(str)
```

# Visualization
For this section you will need to have installed the [```matplotlib```](https://matplotlib.org/) and [```seaborn```](https://seaborn.pydata.org/) modules and run the following code:
```python
# Import matplotlib
import matplotlib.pyplot as plt

# Import seaborn
import seaborn as sns
```

Plotting time-series for a specific "column" in a dataframe
```python
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

[Create a graph with different x- and y-axis, which combines two (or more) graphs (ex. two line plots)](https://stackoverflow.com/questions/42734109/two-or-more-graphs-in-one-plot-with-different-x-axis-and-y-axis-scales-in-pyth)

```python
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
```python
columns = ['A', 'B'] 
n = 1 
plt.figure(figsize=(20,15)) 
for column in columns: 
    plt.subplot(4,4,n) 
    n = n + 1 
    sns.boxplot(data[column]) 
    plt.tight_layout()
```

Plot correlation heatmap
```python
corrMatrix = df.corr() 
sn.heatmap(corrMatrix, annot=True) 
plt.show()
```

#  Working with Pandas DataFrame and NumPy array objects
In this subsection we will be doing general computations to create, change or expand DataFrames and NumPy arrays.

Generate a random DataFrame
```python
dates = pd.date_range("20210101", periods=6, freq='MS')
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list("ABCD"))
```

Select columns based on type of variable (i.e., numerical or categorical)
```python
categorical=df.select_dtypes(exclude=['float64','int64']).columns 
numerical=df.select_dtypes(include=['float64','int64']).columns
```
or
```python
numerical=df.select_dtypes(include=np.number).columns 
categorical=df.select_dtypes(exclude=np.number).columns
```

Get index of maximum/ minium values
```python
df.idxmin()
df.idxmax()
```

[Split DataFrame into multiple CSV files based on column value](https://stackoverflow.com/questions/49050455/pandas-split-data-frame-into-multiple-csvs-based-on-column-value)

*Note: need [os](https://docs.python.org/3/library/os.html) module*

```python
# Import os module 
import os 

for i, x in df.groupby('column_value'): 
    p = os.path.join(os.getcwd(), "data_{}.csv".format(i.lower())) 
    x.to_csv(p, index=False)
```

[How to drop rows in which a value in a certain column is NaN](https://stackoverflow.com/questions/13413590/how-to-drop-rows-of-pandas-dataframe-whose-value-in-a-certain-column-is-nan)
```python
df = df[~df['col1'].isna()]
```

[How to keep all columns except for specific ones](https://www.statology.org/pandas-keep-columns/)
```python
# Drop columns 'col3' and 'col4' 
df[df.columns[~df.columns.isin(['col3', 'col4'])]]
```

[How to apply a function to two columns](https://stackoverflow.com/questions/13331698/how-to-apply-a-function-to-two-columns-of-pandas-dataframe)
```python
df['col3'] = df.apply(lambda x: f(x['col1'], x['col2']), axis=1)
# where "f" is the intended function
```

[How to split a string column into two columns?](https://stackoverflow.com/questions/14745022/how-to-split-a-dataframe-string-column-into-two-columns)
```python
df[['A', 'B']] = df['AB'].str.split(' ', 1, expand=True)
```

Remove white spaces from column headers
```python
df.columns = [col.strip() for col in df.columns]
```

[Replace values in a column based on a condition](https://www.geeksforgeeks.org/how-to-replace-values-in-column-based-on-condition-in-pandas/)
```python
df.loc[df["gender"] == "male", "gender"] = 1
```

[How to access a "groupby" group by key](https://stackoverflow.com/questions/14734533/how-to-access-pandas-groupby-dataframe-by-key)
```python
get_foo_group = df.groupby(['col1']).get_group("foo")
```

[Groupby with duplicated values while keeping the first entry](https://stackoverflow.com/questions/12497402/remove-duplicates-by-columns-a-keeping-the-row-with-the-highest-value-in-column)
```python
df.sort_values('col2', ascending=False).drop_duplicates('col1').sort_index()
```

[Check if two DataFrames are equal](https://www.geeksforgeeks.org/python-pandas-dataframe-equals/)
```python
df1.equals(df2)
```

Check if two columns are equal
[(A)](https://moonbooks.org/Articles/How-to-check-if-two-columns-are-equal-identical-with-pandas-/) or [(B)](https://stackoverflow.com/questions/19125091/pandas-merge-how-to-avoid-duplicating-columns)
```python
# Option (A)
for i in ["col1", "col2", "col3"]:
    merged[i+'_x'].equals(merged[i+'_y'])
```
or
```python
# Option (B)
cols_to_use = df2.columns.difference(df.columns)
dfNew = merge(df, df2[cols_to_use], left_index=True, right_index=True, how='outer')
```

[Calculate correlation between columns of strings](https://stackoverflow.com/questions/51241575/calculate-correlation-between-columns-of-strings)
```python
df['col1']=df['col1'].astype('category').cat.codes 
df['col2']=df['col2'].astype('category').cat.codes 
df.corr()
```

[How to flatten a NumPy array](https://numpy.org/doc/stable/reference/generated/numpy.ravel.html)
```python
x = np.array([[1, 2, 3], [4, 5, 6]]) 
np.ravel(x) 
```

[Apply multiple functions to multiple groupby columns](https://stackoverflow.com/questions/14529838/apply-multiple-functions-to-multiple-groupby-columns)
```python
df.groupby('group').agg({'a':['sum', 'max'], 
                         'b':'mean', 
                         'c':'sum', 
                         'd': lambda x: x.max() - x.min()})
```

[Locate first and last non NaN values in a DataFrame](https://stackoverflow.com/questions/22403469/locate-first-and-last-non-nan-values-in-a-pandas-dataframe)
```Python
# first valid index for each column
df.apply(pd.Series.first_valid_index)

# last valid index for each column
df.apply(pd.Series.last_valid_index)
```

[How to get the last value in each group?](https://datascienceparichay.com/article/pandas-groupby-last-value/): also works for getting the last "available" (i.e., non Nan) observation
```Python
df.groupby('group')['colA'].last()
```

[Compare two columns and replace value based on condition](https://stackoverflow.com/questions/27474921/compare-two-columns-using-pandas)
```Python
df['new'] = np.where((df['colA'] >= df['colB']) & (df['colA'] <= df['colC'])
                     , df['colA'], np.nan)
```

[How to convert column (with NaN) to integer](https://stackoverflow.com/questions/62899860/how-can-i-resolve-typeerror-cannot-safely-cast-non-equivalent-float64-to-int6)
```Python
df['A'] = np.floor(pd.to_numeric(df['A'], errors='coerce')).astype('Int64')
```

[How to deal with missing value with LabelEncoder](https://stackoverflow.com/questions/36808434/label-encoder-encoding-missing-values)
```Python
original = df
mask = df.isnull()
df = df.astype(str).apply(LabelEncoder().fit_transform)
df.where(~mask, original)
```

[Generate a dictionary of data type for each column](https://stackoverflow.com/questions/41087887/is-there-a-way-to-generate-the-dtypes-as-a-dictionary-in-pandas)
```python
df.dtypes.to_dict()
```

[Import multiple CSV files into pandas and concatenate them](https://stackoverflow.com/questions/20906474/import-multiple-csv-files-into-pandas-and-concatenate-into-one-dataframe)
```python
all_files = glob.glob(os.path.join(path, "*.csv"))
df = pd.concat((pd.read_csv(f) for f in all_files), ignore_index=True)
```

# General Python snippets
Check Python documentation
```python
dir()
dir(__builtins__)
```

Show locally installed version of Pandas
```python
pd.show_versions()
```

[Remove multiple keys from a dictionary safely](https://stackoverflow.com/questions/8995611/removing-multiple-keys-from-a-dictionary-safely)
```python
entries = ('a', 'b', 'c')
the_dict = {'b': 'foo'}

for key in entries:
    if key in the_dict:
        del the_dict[key]
```

[Save dictionary to disk](https://pythonspot.com/save-a-dictionary-to-a-file/)
```pyython
# define dict
dict = {'Python' : '.py', 'C++' : '.cpp', 'Java' : '.java'}

# open file for writing
f = open("dict.txt","w")

# write file
f.write( str(dict) )

# close file
f.close()
```

[How to create all possible combinations of parameters in a dictionary](https://stackoverflow.com/questions/71488625/how-to-create-all-possible-combinations-of-parameters-in-a-dictionaryp)
```python
import itertools

hyper_params = {
    'penalty': ['l1', 'l2'],
    'class_weight': [None, 'balanced'],
    'max_iter': [500, 1000]
}

combinations = list(itertools.product(*hyper_params.values()))
```


[Convert a list to a dictionary](https://www.geeksforgeeks.org/python-convert-a-list-to-dictionary/)
```python
def convert(lst):
    res_dct = {lst[i]: lst[i + 1] for i in range(0, len(lst), 2)}
    return res_dct
```

[How to merge dictionaries](https://favtutor.com/blogs/merge-dictionaries-python)
```python
dict_1 = {'John': 15, 'Rick': 10, 'Misa' : 12 }
dict_2 = {'Bonnie': 18,'Rick': 20,'Matt' : 16 }
dict_1.update(dict_2)
```

Create X blocks of Y numbers
```python
n = 0 
for i in range(0, X): 
    v = 0 
    for j in range(0, Y): 
        if(v >= Y): 
            pass 
        else: 
            print(n) 
            n +=1  
            v += 1
```

[How to flatten a list of lists](https://www.educative.io/edpresso/how-to-flatten-a-list-of-lists-in-python)
```python
List_2D = [[1,2,3],[4,5,6],[7,8,9]] #List to be flattened 
List_flat = list(itertools.chain(*List_2D))
```

[Create multiple empty dataframes](https://stackoverflow.com/questions/30635145/create-multiple-dataframes-in-loop) & [iterate over them](https://stackoverflow.com/questions/41287310/python-how-to-iterate-over-dataframes-while-using-their-name-as-a-string)
```python
dict = {"df_" + str(i): pd.DataFrame() for i in range(0, 10)}

for df_name, df in dict.items():
    # Computation to be applied to each DataFrame
```

[How to determine a file's encoding type](https://www.kaggle.com/paultimothymooney/how-to-resolve-a-unicodedecodeerror-for-a-csv-file)

*Note: need [chardet](https://chardet.readthedocs.io/en/latest/usage.html) module*
```python
# Import chardet module
import chardet

with open(file, 'rb') as rawdata:
    result = chardet.detect(rawdata.read(100000))
result
```


Display a webpage and a YouTube video in Jupyter notebook

*Note: need [IPython](https://pypi.org/project/ipython/) module*

- Webpage
```python
# Import IPython module
import IPython 

url = 'https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html' 
IPython.display.IFrame(url, 800, 600)
```
- YouTube video
```python
# Import IPython module
from IPython.display import YouTubeVideo 

video_link = 'https://www.youtube.com/watch?v=rfscVS0vtbw' 
YouTubeVideo(video_link, width=500, height=300)
```
