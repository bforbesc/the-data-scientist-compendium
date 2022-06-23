# Python snippets

Add months to a date in Python
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
