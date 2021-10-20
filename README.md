
# Data Engineering Assignment

Data Analysis on Netflix Dataset



### Import Necessary Libraries

```python
import pandas as pd
import matplotlib.pyplot as plt
```


### Reading CSV File
```python
df = pd.read_csv('netflix_titles.csv')
df.head()
```

### Cleaning up data
#### Removing all rows which have NaN value
```python
df = df.dropna(how='any')
```

### Assignments
#### Question #1: Convert dates into a proper date-time format of your choice
```python
df['date_added'] = pd.to_datetime(df['date_added'])
```

#### Question #2: Finding seasons count from durations columns

2.1 First find the 'season' word from duration column
```python
df['duration'].str.find('Season')
```
2.2 Then add a new column named as 'seasons'
```python
df['season'] = df['duration'].str.find('Season')
```
2.3 Seperate the 'min' from seasons and count the value of only seasons from season column
```python
df[df['season'] != -1].count()
```

#### Question #5: How many movies were released each year.
5.1 Get the all movies from type column and get into movie_result
```python
movie_result = df[df['type'] == 'Movie']
```
5.2 And apply the groupby function on release_year column and calculate the count
```python
movie_result.groupby(['release_year']).count()
```

#### Question #6: Which month is the best month to release it.
6.1 Add/Create the month column and take the month from date_added column
```python
df['month'] = pd.DatetimeIndex(df['date_added']).month
```
6.2 Convert the month's datatype into int from float
```python
df['month'] = df['month'].astype('int32')
df.dtypes
```
6.3 Get the count of the released Movie or TV Show from release_year and groupby with month column
```python
result = df[['month','show_id']].groupby(['month']).count()
result
```

6.4 And output with bar chart using matplotlib library
```python
import matplotlib.pyplot as plt

months = range(1,13)
plt.bar(months, result['show_id'])
plt.xticks(months)
plt.ylabel("No.of Releases")
plt.xlabel("Month")
plt.show()
```

#### Output in HTML File
```python
df.to_html('output.html')
```