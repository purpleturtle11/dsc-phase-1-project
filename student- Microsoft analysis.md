# MOVIE ANALYSIS FOR MICROSOFT STUDIO




# Overview

This project analyzes data from IMDb, which is an online database containing information related to movies and other films. Exploratory data analysis including univvariate and multivariate analysis shows that success of a movie depends on the genre, length of the movie and the ratings it has received. The Microsoft studio can use these insights to decide what to allocate resources to and also the kind of movies that would be profitable for them.  


# Business Problem
Microsoft sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies. I have explored the nature of the movies that are currently showing best performance at the box office. I then displayed how length of film, genre and customer feedback translates to good performance of a movie.

# Data Understanding

I will use data from from two files from IMDb.
1. The first dataset contains information on title basics: 'title.basics.csv', referenced as df dataframe.
2. The second dataset contains information on title ratings: 'title.ratings.csv', referenced as df2 dataframe.



## 1. First Dataset 

df=pd.read_csv('title.basics.csv')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action,Crime,Drama</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography,Drama</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0069049</td>
      <td>The Other Side of the Wind</td>
      <td>The Other Side of the Wind</td>
      <td>2018</td>
      <td>122.0</td>
      <td>Drama</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0069204</td>
      <td>Sabse Bada Sukh</td>
      <td>Sabse Bada Sukh</td>
      <td>2018</td>
      <td>NaN</td>
      <td>Comedy,Drama</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0100275</td>
      <td>The Wandering Soap Opera</td>
      <td>La Telenovela Errante</td>
      <td>2017</td>
      <td>80.0</td>
      <td>Comedy,Drama,Fantasy</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Let us find out the dimensions of our dataframe
df.shape
```




    (146144, 6)



The dataframe has 146144 rows and 6 columns


```python
#What columns are present in the dataset?
df.columns
```




    Index(['tconst', 'primary_title', 'original_title', 'start_year',
           'runtime_minutes', 'genres'],
          dtype='object')




```python
#find out the type of information contained in this dataset
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 146144 entries, 0 to 146143
    Data columns (total 6 columns):
     #   Column           Non-Null Count   Dtype  
    ---  ------           --------------   -----  
     0   tconst           146144 non-null  object 
     1   primary_title    146144 non-null  object 
     2   original_title   146123 non-null  object 
     3   start_year       146144 non-null  int64  
     4   runtime_minutes  114405 non-null  float64
     5   genres           140736 non-null  object 
    dtypes: float64(1), int64(1), object(4)
    memory usage: 6.7+ MB
    

Having obtained the summary of the content of the dataset we will explore different columns to further understand our data



```python
df['start_year'].plot.hist(bins = 100, title = 'Start year Distribution', figsize= (10,6))
```




    <AxesSubplot:title={'center':'Start year Distribution'}, ylabel='Frequency'>




    
![png](output_13_1.png)
    



```python
sns.scatterplot(x= df['start_year'], y= df['runtime_minutes']);
```


    
![png](output_14_0.png)
    



```python
df['genres']= df['genres'].str.split(",")

df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>[Action, Crime, Drama]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>[Biography, Drama]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0069049</td>
      <td>The Other Side of the Wind</td>
      <td>The Other Side of the Wind</td>
      <td>2018</td>
      <td>122.0</td>
      <td>[Drama]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0069204</td>
      <td>Sabse Bada Sukh</td>
      <td>Sabse Bada Sukh</td>
      <td>2018</td>
      <td>NaN</td>
      <td>[Comedy, Drama]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0100275</td>
      <td>The Wandering Soap Opera</td>
      <td>La Telenovela Errante</td>
      <td>2017</td>
      <td>80.0</td>
      <td>[Comedy, Drama, Fantasy]</td>
    </tr>
  </tbody>
</table>
</div>




```python
df= df.explode('genres')
print(type(df['genres']))
df
```

    <class 'pandas.core.series.Series'>
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Crime</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Drama</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Drama</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>146139</th>
      <td>tt9916538</td>
      <td>Kuambil Lagi Hatiku</td>
      <td>Kuambil Lagi Hatiku</td>
      <td>2019</td>
      <td>123.0</td>
      <td>Drama</td>
    </tr>
    <tr>
      <th>146140</th>
      <td>tt9916622</td>
      <td>Rodolpho Teóphilo - O Legado de um Pioneiro</td>
      <td>Rodolpho Teóphilo - O Legado de um Pioneiro</td>
      <td>2015</td>
      <td>NaN</td>
      <td>Documentary</td>
    </tr>
    <tr>
      <th>146141</th>
      <td>tt9916706</td>
      <td>Dankyavar Danka</td>
      <td>Dankyavar Danka</td>
      <td>2013</td>
      <td>NaN</td>
      <td>Comedy</td>
    </tr>
    <tr>
      <th>146142</th>
      <td>tt9916730</td>
      <td>6 Gunn</td>
      <td>6 Gunn</td>
      <td>2017</td>
      <td>116.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>146143</th>
      <td>tt9916754</td>
      <td>Chico Albuquerque - Revelações</td>
      <td>Chico Albuquerque - Revelações</td>
      <td>2013</td>
      <td>NaN</td>
      <td>Documentary</td>
    </tr>
  </tbody>
</table>
<p>234958 rows × 6 columns</p>
</div>




```python
df.genres.value_counts().plot.pie(figsize= (10,10), autopct= "%.0f%%",
                                  title = 'Percentage distribution of all the movie genres in the dataset',
                                 rot= 90, sort_columns=True)
                                                 
```




    <AxesSubplot:title={'center':'Percentage distribution of all the movie genres in the dataset'}, ylabel='genres'>




    
![png](output_17_1.png)
    



```python
#Checking for outliers in the column
sns.boxplot(x= df['runtime_minutes'])
```




    <AxesSubplot:xlabel='runtime_minutes'>




    
![png](output_18_1.png)
    


The column presents outliers that need to be handled as we look at the business case. We will cap the values instead of dropping the outliers altogether because dropping a significant amount of values will affect our analysis. We will consider values that are within 98% of all the records.


```python
# Define the threshold to get the quantiles ie. lower limit and the upper limit.
Q1= df['runtime_minutes'].quantile(0.02)
Q3= df['runtime_minutes'].quantile(0.98)
```


```python
df.loc[:,'runtime_minutes_capped'] = np.where(df.loc[:,'runtime_minutes'] > Q3, Q3,
                                        np.where(df.loc[:,'runtime_minutes']< Q1, Q1, 
                                                 df.loc[:,'runtime_minutes']))
df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
      <th>runtime_minutes_capped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Crime</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Drama</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography</td>
      <td>114.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Drama</td>
      <td>114.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>146139</th>
      <td>tt9916538</td>
      <td>Kuambil Lagi Hatiku</td>
      <td>Kuambil Lagi Hatiku</td>
      <td>2019</td>
      <td>123.0</td>
      <td>Drama</td>
      <td>123.0</td>
    </tr>
    <tr>
      <th>146140</th>
      <td>tt9916622</td>
      <td>Rodolpho Teóphilo - O Legado de um Pioneiro</td>
      <td>Rodolpho Teóphilo - O Legado de um Pioneiro</td>
      <td>2015</td>
      <td>NaN</td>
      <td>Documentary</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>146141</th>
      <td>tt9916706</td>
      <td>Dankyavar Danka</td>
      <td>Dankyavar Danka</td>
      <td>2013</td>
      <td>NaN</td>
      <td>Comedy</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>146142</th>
      <td>tt9916730</td>
      <td>6 Gunn</td>
      <td>6 Gunn</td>
      <td>2017</td>
      <td>116.0</td>
      <td>NaN</td>
      <td>116.0</td>
    </tr>
    <tr>
      <th>146143</th>
      <td>tt9916754</td>
      <td>Chico Albuquerque - Revelações</td>
      <td>Chico Albuquerque - Revelações</td>
      <td>2013</td>
      <td>NaN</td>
      <td>Documentary</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>234958 rows × 7 columns</p>
</div>




```python
#Redraw the boxplot to check whether outliers have been dealt with.
sns.boxplot(x= df['runtime_minutes_capped'])
```




    <AxesSubplot:xlabel='runtime_minutes_capped'>




    
![png](output_22_1.png)
    


We have handled our outliers by capping the values of the running time. 
We will use the new column, runningtime_minutes_capped to continue our analysis. 

## Checking for Duplicates


```python
#Check whether our data contains duplicate records and the total number
df.duplicated().value_counts()
```




    False    234958
    dtype: int64




```python
#Display the dataframe of duplicated records
df[df.duplicated(keep=False)].sort_values(by= 'tconst')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
      <th>runtime_minutes_capped</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



Our data does not contain any duplicates.

## Checking for missing values


```python
# Find the null values in each column. Sum the resulting boolean values
#Divide by the length of each column to find the percentage missing values
df.isna().sum()/len(df)
```




    tconst                    0.000000
    primary_title             0.000000
    original_title            0.000089
    start_year                0.000000
    runtime_minutes           0.166217
    genres                    0.023017
    runtime_minutes_capped    0.166217
    dtype: float64



Knowing the percentage of missing values in each column helps us know how to handle the missing values in each column.


 ## a) original_title
Missing %value (0.000089)
The percentage is small therefore we will drop the missing rows without interfering with the analysis. 


```python
#Drop rows where original_title column values are null
df= df.dropna(subset=['original_title'], how='all')
df.isna().sum()
```




    tconst                        0
    primary_title                 0
    original_title                0
    start_year                    0
    runtime_minutes           39037
    genres                     5389
    runtime_minutes_capped    39037
    dtype: int64



## b) runtime_minutes_capped

The missing %value is 0.166217. This is a significant percentage therefore we will explore the data some more in order to decide how to handle the missing values.


```python
#Viewing basic statistical details
df['runtime_minutes_capped'].describe()
```




    count    195900.000000
    mean         85.272231
    std          26.779096
    min          15.000000
    25%          71.000000
    50%          88.000000
    75%         100.000000
    max         149.000000
    Name: runtime_minutes_capped, dtype: float64




```python
df['runtime_minutes_capped'].plot.hist(bins = 100, title = 'Distribution of The Movie Runtime', figsize= (10,5))
```




    <AxesSubplot:title={'center':'Distribution of The Movie Runtime'}, ylabel='Frequency'>




    
![png](output_35_1.png)
    


We will replace them with the median because it is least affected by extreme values. From our statistical assessment, the new data now has a normal distribution


```python
df.loc[:,'runtime_minutes_capped'] =  df.loc[:,'runtime_minutes_capped'].fillna(df.loc[:,'runtime_minutes_capped'].median())
df.isna().sum()
```

    C:\Users\HP\anaconda3\envs\learn-env\lib\site-packages\pandas\core\indexing.py:1745: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      isetter(ilocs[0], value)
    




    tconst                        0
    primary_title                 0
    original_title                0
    start_year                    0
    runtime_minutes           39037
    genres                     5389
    runtime_minutes_capped        0
    dtype: int64



## c) genres 
We have different ways of dealing with this categorical column. Given that the data may be useful we wil not drop the null values. We can fill the missing values with a static value hence treating it as a separate valid category


```python
df.loc[:,'genres']= df.loc[:,'genres'].fillna('No genre')
df.isna().sum()
```




    tconst                        0
    primary_title                 0
    original_title                0
    start_year                    0
    runtime_minutes           39037
    genres                        0
    runtime_minutes_capped        0
    dtype: int64




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
      <th>runtime_minutes_capped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Crime</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Drama</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography</td>
      <td>114.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Drama</td>
      <td>114.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>146139</th>
      <td>tt9916538</td>
      <td>Kuambil Lagi Hatiku</td>
      <td>Kuambil Lagi Hatiku</td>
      <td>2019</td>
      <td>123.0</td>
      <td>Drama</td>
      <td>123.0</td>
    </tr>
    <tr>
      <th>146140</th>
      <td>tt9916622</td>
      <td>Rodolpho Teóphilo - O Legado de um Pioneiro</td>
      <td>Rodolpho Teóphilo - O Legado de um Pioneiro</td>
      <td>2015</td>
      <td>NaN</td>
      <td>Documentary</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>146141</th>
      <td>tt9916706</td>
      <td>Dankyavar Danka</td>
      <td>Dankyavar Danka</td>
      <td>2013</td>
      <td>NaN</td>
      <td>Comedy</td>
      <td>88.0</td>
    </tr>
    <tr>
      <th>146142</th>
      <td>tt9916730</td>
      <td>6 Gunn</td>
      <td>6 Gunn</td>
      <td>2017</td>
      <td>116.0</td>
      <td>No genre</td>
      <td>116.0</td>
    </tr>
    <tr>
      <th>146143</th>
      <td>tt9916754</td>
      <td>Chico Albuquerque - Revelações</td>
      <td>Chico Albuquerque - Revelações</td>
      <td>2013</td>
      <td>NaN</td>
      <td>Documentary</td>
      <td>88.0</td>
    </tr>
  </tbody>
</table>
<p>234937 rows × 7 columns</p>
</div>



## 2. Second Dataset


```python
#Load the dataset
df2=pd.read_csv('title.ratings.csv')
df2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>averagerating</th>
      <th>numvotes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt10356526</td>
      <td>8.3</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt10384606</td>
      <td>8.9</td>
      <td>559</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt1042974</td>
      <td>6.4</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt1043726</td>
      <td>4.2</td>
      <td>50352</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt1060240</td>
      <td>6.5</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Let us find out the dimensions of our dataframe
df2.shape
```




    (73856, 3)



The dataframe has 73856 rows and 3 columns namely: tconst, averagerating and numvotes


```python
#find out the type of information contained in this dataset
df2.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 73856 entries, 0 to 73855
    Data columns (total 3 columns):
     #   Column         Non-Null Count  Dtype  
    ---  ------         --------------  -----  
     0   tconst         73856 non-null  object 
     1   averagerating  73856 non-null  float64
     2   numvotes       73856 non-null  int64  
    dtypes: float64(1), int64(1), object(1)
    memory usage: 1.7+ MB
    

The summary shows that no columns are empty. The datatypes for each column are also appropriate for the data they hold.


```python
#Generating some descriptive statistics in order to futher understand our data
df2.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>averagerating</th>
      <th>numvotes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>73856.000000</td>
      <td>7.385600e+04</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>6.332729</td>
      <td>3.523662e+03</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.474978</td>
      <td>3.029402e+04</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>5.000000e+00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>5.500000</td>
      <td>1.400000e+01</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>6.500000</td>
      <td>4.900000e+01</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7.400000</td>
      <td>2.820000e+02</td>
    </tr>
    <tr>
      <th>max</th>
      <td>10.000000</td>
      <td>1.841066e+06</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Checking how our two numerical columns are related
df2.plot.scatter(x = 'averagerating', y = 'numvotes', color = 'blue', title = 'UnitPrice vs UnitDiscount')
```




    <AxesSubplot:title={'center':'UnitPrice vs UnitDiscount'}, xlabel='averagerating', ylabel='numvotes'>




    
![png](output_48_1.png)
    


## Checking for Duplicates


```python
#Check whether our data contains duplicate records and the total number of the duplicates if present
df2.duplicated().value_counts()
```




    False    73856
    dtype: int64




```python
#Display the dataframe of duplicated records
df2[df2.duplicated(keep=False)].sort_values(by= 'tconst')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>averagerating</th>
      <th>numvotes</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



## Handling outliers


```python
#Checking for outliers in the columns
sns.boxplot(data= df2, color= 'gray', orient= 'h')
```




    <AxesSubplot:>




    
![png](output_53_1.png)
    


The column numvotes has outliers from the boxplot observation. 


```python
df2['numvotes'].plot.hist(bins = 100, title = 'The Distribution of votes', figsize= (10,5))
```




    <AxesSubplot:title={'center':'The Distribution of votes'}, ylabel='Frequency'>




    
![png](output_55_1.png)
    


Given that the distribution is skewed to the right, replacing the outliers with the mean or standard deviation may affect our values. 
Therefore we will cap the values and consider the ones that are within 97% of all the records.


```python
# Define the threshold to get the quantiles ie. lower limit and the upper limit.
Q1= df2['numvotes'].quantile(0.03)
Q3= df2['numvotes'].quantile(0.97)
```


```python
df2['numvotes_capped'] = np.where(df2['numvotes'] > Q3, Q3,
                        np.where(df2['numvotes'] < Q1, Q1, 
                        df2['numvotes']))
df2

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>averagerating</th>
      <th>numvotes</th>
      <th>numvotes_capped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt10356526</td>
      <td>8.3</td>
      <td>31</td>
      <td>31.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt10384606</td>
      <td>8.9</td>
      <td>559</td>
      <td>559.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt1042974</td>
      <td>6.4</td>
      <td>20</td>
      <td>20.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt1043726</td>
      <td>4.2</td>
      <td>50352</td>
      <td>14247.05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt1060240</td>
      <td>6.5</td>
      <td>21</td>
      <td>21.00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73851</th>
      <td>tt9805820</td>
      <td>8.1</td>
      <td>25</td>
      <td>25.00</td>
    </tr>
    <tr>
      <th>73852</th>
      <td>tt9844256</td>
      <td>7.5</td>
      <td>24</td>
      <td>24.00</td>
    </tr>
    <tr>
      <th>73853</th>
      <td>tt9851050</td>
      <td>4.7</td>
      <td>14</td>
      <td>14.00</td>
    </tr>
    <tr>
      <th>73854</th>
      <td>tt9886934</td>
      <td>7.0</td>
      <td>5</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>73855</th>
      <td>tt9894098</td>
      <td>6.3</td>
      <td>128</td>
      <td>128.00</td>
    </tr>
  </tbody>
</table>
<p>73856 rows × 4 columns</p>
</div>




```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
      <th>runtime_minutes_capped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Crime</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Drama</td>
      <td>149.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography</td>
      <td>114.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Drama</td>
      <td>114.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>averagerating</th>
      <th>numvotes</th>
      <th>numvotes_capped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt10356526</td>
      <td>8.3</td>
      <td>31</td>
      <td>31.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt10384606</td>
      <td>8.9</td>
      <td>559</td>
      <td>559.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt1042974</td>
      <td>6.4</td>
      <td>20</td>
      <td>20.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt1043726</td>
      <td>4.2</td>
      <td>50352</td>
      <td>14247.05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt1060240</td>
      <td>6.5</td>
      <td>21</td>
      <td>21.00</td>
    </tr>
  </tbody>
</table>
</div>



# Analysis and Evaluation

## Prefered Movie genres

Some movie genres are produced more than others. This may be due to the great reception in the market. 
We have the Documentary and Drama genres each taking up 21% of all the movies produced.


```python
#Find out the movie with the highest frequency
genre_freq= df['genres'].value_counts()/ len(df['genres'])
genre_freq
```




    Documentary    0.219804
    Drama          0.212325
    Comedy         0.107740
    Thriller       0.050580
    Horror         0.045991
    Action         0.043991
    Romance        0.039887
    Biography      0.037125
    Crime          0.028744
    Adventure      0.027514
    Family         0.026505
    History        0.026496
    No genre       0.022938
    Mystery        0.019831
    Music          0.018362
    Fantasy        0.014966
    Sci-Fi         0.014323
    Animation      0.011914
    Sport          0.009509
    News           0.006602
    Musical        0.006087
    War            0.005980
    Western        0.001988
    Reality-TV     0.000417
    Talk-Show      0.000213
    Adult          0.000106
    Short          0.000047
    Game-Show      0.000017
    Name: genres, dtype: float64



In order to do further analysis on genres and draw meaningful conclusions, we will merge the two datasets, df and df2.
This will give us both details of title basics and title ratings


```python
df3 = pd.merge( df, df2, how="inner", on= 'tconst')
df3
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
      <th>runtime_minutes_capped</th>
      <th>averagerating</th>
      <th>numvotes</th>
      <th>numvotes_capped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action</td>
      <td>149.0</td>
      <td>7.0</td>
      <td>77</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Crime</td>
      <td>149.0</td>
      <td>7.0</td>
      <td>77</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Drama</td>
      <td>149.0</td>
      <td>7.0</td>
      <td>77</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography</td>
      <td>114.0</td>
      <td>7.2</td>
      <td>43</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Drama</td>
      <td>114.0</td>
      <td>7.2</td>
      <td>43</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>129289</th>
      <td>tt9914286</td>
      <td>Sokagin Çocuklari</td>
      <td>Sokagin Çocuklari</td>
      <td>2019</td>
      <td>98.0</td>
      <td>Drama</td>
      <td>98.0</td>
      <td>8.7</td>
      <td>136</td>
      <td>136.0</td>
    </tr>
    <tr>
      <th>129290</th>
      <td>tt9914286</td>
      <td>Sokagin Çocuklari</td>
      <td>Sokagin Çocuklari</td>
      <td>2019</td>
      <td>98.0</td>
      <td>Family</td>
      <td>98.0</td>
      <td>8.7</td>
      <td>136</td>
      <td>136.0</td>
    </tr>
    <tr>
      <th>129291</th>
      <td>tt9914642</td>
      <td>Albatross</td>
      <td>Albatross</td>
      <td>2017</td>
      <td>NaN</td>
      <td>Documentary</td>
      <td>88.0</td>
      <td>8.5</td>
      <td>8</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>129292</th>
      <td>tt9914942</td>
      <td>La vida sense la Sara Amat</td>
      <td>La vida sense la Sara Amat</td>
      <td>2019</td>
      <td>NaN</td>
      <td>No genre</td>
      <td>88.0</td>
      <td>6.6</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>129293</th>
      <td>tt9916160</td>
      <td>Drømmeland</td>
      <td>Drømmeland</td>
      <td>2019</td>
      <td>72.0</td>
      <td>Documentary</td>
      <td>72.0</td>
      <td>6.5</td>
      <td>11</td>
      <td>11.0</td>
    </tr>
  </tbody>
</table>
<p>129294 rows × 10 columns</p>
</div>




```python
# Summary description of the dataset
df3.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 129294 entries, 0 to 129293
    Data columns (total 10 columns):
     #   Column                  Non-Null Count   Dtype  
    ---  ------                  --------------   -----  
     0   tconst                  129294 non-null  object 
     1   primary_title           129294 non-null  object 
     2   original_title          129294 non-null  object 
     3   start_year              129294 non-null  int64  
     4   runtime_minutes         118953 non-null  float64
     5   genres                  129294 non-null  object 
     6   runtime_minutes_capped  129294 non-null  float64
     7   averagerating           129294 non-null  float64
     8   numvotes                129294 non-null  int64  
     9   numvotes_capped         129294 non-null  float64
    dtypes: float64(4), int64(2), object(4)
    memory usage: 10.9+ MB
    

Movies with a single genre on average had a slightly higher rating compared to the ones with multiple genres. Hovever the margin of difference is quite small between the two, in terms of rating.


```python
#create a smaller dataframe to sum the number of genres in a movie
dfa= df3[['tconst', 'genres']].groupby(['tconst']).count()

#plot frequency distribution
dfa.plot.hist(bins=3, figsize= (10,10),grid=True, 
              legend=True, title = 'Frequency distribution of the number of Genres in a movie')
dfa
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>genres</th>
    </tr>
    <tr>
      <th>tconst</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>tt0063540</th>
      <td>3</td>
    </tr>
    <tr>
      <th>tt0066787</th>
      <td>2</td>
    </tr>
    <tr>
      <th>tt0069049</th>
      <td>1</td>
    </tr>
    <tr>
      <th>tt0069204</th>
      <td>2</td>
    </tr>
    <tr>
      <th>tt0100275</th>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>tt9913084</th>
      <td>1</td>
    </tr>
    <tr>
      <th>tt9914286</th>
      <td>2</td>
    </tr>
    <tr>
      <th>tt9914642</th>
      <td>1</td>
    </tr>
    <tr>
      <th>tt9914942</th>
      <td>1</td>
    </tr>
    <tr>
      <th>tt9916160</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>73856 rows × 1 columns</p>
</div>




    
![png](output_69_1.png)
    



```python
# create a smaller dataframe containing the average rating per movie title
dfb= df3[['tconst', 'averagerating']].groupby(['tconst']).mean()
dfb
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>averagerating</th>
    </tr>
    <tr>
      <th>tconst</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>tt0063540</th>
      <td>7.0</td>
    </tr>
    <tr>
      <th>tt0066787</th>
      <td>7.2</td>
    </tr>
    <tr>
      <th>tt0069049</th>
      <td>6.9</td>
    </tr>
    <tr>
      <th>tt0069204</th>
      <td>6.1</td>
    </tr>
    <tr>
      <th>tt0100275</th>
      <td>6.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>tt9913084</th>
      <td>6.2</td>
    </tr>
    <tr>
      <th>tt9914286</th>
      <td>8.7</td>
    </tr>
    <tr>
      <th>tt9914642</th>
      <td>8.5</td>
    </tr>
    <tr>
      <th>tt9914942</th>
      <td>6.6</td>
    </tr>
    <tr>
      <th>tt9916160</th>
      <td>6.5</td>
    </tr>
  </tbody>
</table>
<p>73856 rows × 1 columns</p>
</div>




```python
# merge the two smaller datasets dfa and dfb
dfc= pd.merge( dfa, dfb, how="inner", on= 'tconst')

#Get a small description of the newly formed dataset
print(dfc.info())
dfc
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 73856 entries, tt0063540 to tt9916160
    Data columns (total 2 columns):
     #   Column         Non-Null Count  Dtype  
    ---  ------         --------------  -----  
     0   genres         73856 non-null  int64  
     1   averagerating  73856 non-null  float64
    dtypes: float64(1), int64(1)
    memory usage: 1.7+ MB
    None
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>genres</th>
      <th>averagerating</th>
    </tr>
    <tr>
      <th>tconst</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>tt0063540</th>
      <td>3</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>tt0066787</th>
      <td>2</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>tt0069049</th>
      <td>1</td>
      <td>6.9</td>
    </tr>
    <tr>
      <th>tt0069204</th>
      <td>2</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>tt0100275</th>
      <td>3</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>tt9913084</th>
      <td>1</td>
      <td>6.2</td>
    </tr>
    <tr>
      <th>tt9914286</th>
      <td>2</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>tt9914642</th>
      <td>1</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>tt9914942</th>
      <td>1</td>
      <td>6.6</td>
    </tr>
    <tr>
      <th>tt9916160</th>
      <td>1</td>
      <td>6.5</td>
    </tr>
  </tbody>
</table>
<p>73856 rows × 2 columns</p>
</div>




```python
# group data based on number of genres column then plot
dfc.groupby([ 'averagerating',]).mean()['genres'].plot(figsize= (10,10), title= 'Average rating based on Genres')
plt.xticks(rotation=0)
plt.show()
```


    
![png](output_72_0.png)
    



```python
# create a new column to determine whether a movie title has 
# multiple genres or a single genre.
dfc['multiple_or_single'] = dfc['genres'].apply(lambda x: 'single' if x <= 1 else 'multiple')
dfc
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>genres</th>
      <th>averagerating</th>
      <th>multiple_or_single</th>
    </tr>
    <tr>
      <th>tconst</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>tt0063540</th>
      <td>3</td>
      <td>7.0</td>
      <td>multiple</td>
    </tr>
    <tr>
      <th>tt0066787</th>
      <td>2</td>
      <td>7.2</td>
      <td>multiple</td>
    </tr>
    <tr>
      <th>tt0069049</th>
      <td>1</td>
      <td>6.9</td>
      <td>single</td>
    </tr>
    <tr>
      <th>tt0069204</th>
      <td>2</td>
      <td>6.1</td>
      <td>multiple</td>
    </tr>
    <tr>
      <th>tt0100275</th>
      <td>3</td>
      <td>6.5</td>
      <td>multiple</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>tt9913084</th>
      <td>1</td>
      <td>6.2</td>
      <td>single</td>
    </tr>
    <tr>
      <th>tt9914286</th>
      <td>2</td>
      <td>8.7</td>
      <td>multiple</td>
    </tr>
    <tr>
      <th>tt9914642</th>
      <td>1</td>
      <td>8.5</td>
      <td>single</td>
    </tr>
    <tr>
      <th>tt9914942</th>
      <td>1</td>
      <td>6.6</td>
      <td>single</td>
    </tr>
    <tr>
      <th>tt9916160</th>
      <td>1</td>
      <td>6.5</td>
      <td>single</td>
    </tr>
  </tbody>
</table>
<p>73856 rows × 3 columns</p>
</div>




```python
# group the data to see how single genre and multiple genre compare with their average ratings
compare= dfc[['averagerating', 'multiple_or_single']].groupby([ 'multiple_or_single',]).agg(['count', 'mean'])
compare.plot(kind= 'bar', figsize= (10,15),subplots= True, sharex=False, rot= 0)
compare
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">averagerating</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>multiple_or_single</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>multiple</th>
      <td>36860</td>
      <td>6.259436</td>
    </tr>
    <tr>
      <th>single</th>
      <td>36996</td>
      <td>6.405752</td>
    </tr>
  </tbody>
</table>
</div>




    
![png](output_74_1.png)
    


## Impact of number of votes for a movie on the ratings

Ratings have an impact on the performance of movies created by big companies. High ratings from our analysis increase as the number of votes for them increase. consequently, movies with lower ratings have fewer votes.


```python
#grouping the data we want to assess
df3[['tconst', 'averagerating', 'numvotes_capped']].groupby(['tconst']).mean()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>averagerating</th>
      <th>numvotes_capped</th>
    </tr>
    <tr>
      <th>tconst</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>tt0063540</th>
      <td>7.0</td>
      <td>77.0</td>
    </tr>
    <tr>
      <th>tt0066787</th>
      <td>7.2</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>tt0069049</th>
      <td>6.9</td>
      <td>4517.0</td>
    </tr>
    <tr>
      <th>tt0069204</th>
      <td>6.1</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>tt0100275</th>
      <td>6.5</td>
      <td>119.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>tt9913084</th>
      <td>6.2</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>tt9914286</th>
      <td>8.7</td>
      <td>136.0</td>
    </tr>
    <tr>
      <th>tt9914642</th>
      <td>8.5</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>tt9914942</th>
      <td>6.6</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>tt9916160</th>
      <td>6.5</td>
      <td>11.0</td>
    </tr>
  </tbody>
</table>
<p>73856 rows × 2 columns</p>
</div>




```python
#Scatter plot to show relationship
df3.plot.scatter(x = 'averagerating', y = 'numvotes',
                  color = 'orange',
                 title = 'Correlation between average rating and number of votes', figsize= (10,8))
```




    <AxesSubplot:title={'center':'Correlation between average rating and number of votes'}, xlabel='averagerating', ylabel='numvotes'>




    
![png](output_77_1.png)
    


There's a positive relationship between the two sets of data.


```python
#create a function to show the level of rating in each movie
def level_of_rating(rating):
    if (rating < 4):
        return 'Low'
    elif (rating > 6):
        return 'High'
    else:
        return 'Medium'
df3['level_of_rating'] = df3['averagerating'].apply(level_of_rating)
df3
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tconst</th>
      <th>primary_title</th>
      <th>original_title</th>
      <th>start_year</th>
      <th>runtime_minutes</th>
      <th>genres</th>
      <th>runtime_minutes_capped</th>
      <th>averagerating</th>
      <th>numvotes</th>
      <th>numvotes_capped</th>
      <th>level_of_rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Action</td>
      <td>149.0</td>
      <td>7.0</td>
      <td>77</td>
      <td>77.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>1</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Crime</td>
      <td>149.0</td>
      <td>7.0</td>
      <td>77</td>
      <td>77.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tt0063540</td>
      <td>Sunghursh</td>
      <td>Sunghursh</td>
      <td>2013</td>
      <td>175.0</td>
      <td>Drama</td>
      <td>149.0</td>
      <td>7.0</td>
      <td>77</td>
      <td>77.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>3</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Biography</td>
      <td>114.0</td>
      <td>7.2</td>
      <td>43</td>
      <td>43.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>4</th>
      <td>tt0066787</td>
      <td>One Day Before the Rainy Season</td>
      <td>Ashad Ka Ek Din</td>
      <td>2019</td>
      <td>114.0</td>
      <td>Drama</td>
      <td>114.0</td>
      <td>7.2</td>
      <td>43</td>
      <td>43.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>129289</th>
      <td>tt9914286</td>
      <td>Sokagin Çocuklari</td>
      <td>Sokagin Çocuklari</td>
      <td>2019</td>
      <td>98.0</td>
      <td>Drama</td>
      <td>98.0</td>
      <td>8.7</td>
      <td>136</td>
      <td>136.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>129290</th>
      <td>tt9914286</td>
      <td>Sokagin Çocuklari</td>
      <td>Sokagin Çocuklari</td>
      <td>2019</td>
      <td>98.0</td>
      <td>Family</td>
      <td>98.0</td>
      <td>8.7</td>
      <td>136</td>
      <td>136.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>129291</th>
      <td>tt9914642</td>
      <td>Albatross</td>
      <td>Albatross</td>
      <td>2017</td>
      <td>NaN</td>
      <td>Documentary</td>
      <td>88.0</td>
      <td>8.5</td>
      <td>8</td>
      <td>8.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>129292</th>
      <td>tt9914942</td>
      <td>La vida sense la Sara Amat</td>
      <td>La vida sense la Sara Amat</td>
      <td>2019</td>
      <td>NaN</td>
      <td>No genre</td>
      <td>88.0</td>
      <td>6.6</td>
      <td>5</td>
      <td>5.0</td>
      <td>High</td>
    </tr>
    <tr>
      <th>129293</th>
      <td>tt9916160</td>
      <td>Drømmeland</td>
      <td>Drømmeland</td>
      <td>2019</td>
      <td>72.0</td>
      <td>Documentary</td>
      <td>72.0</td>
      <td>6.5</td>
      <td>11</td>
      <td>11.0</td>
      <td>High</td>
    </tr>
  </tbody>
</table>
<p>129294 rows × 11 columns</p>
</div>




```python
df3[['level_of_rating', 'numvotes_capped']].groupby(['level_of_rating']).agg(['count', 'mean'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">numvotes_capped</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>level_of_rating</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>High</th>
      <td>79143</td>
      <td>1312.415804</td>
    </tr>
    <tr>
      <th>Low</th>
      <td>9055</td>
      <td>466.030447</td>
    </tr>
    <tr>
      <th>Medium</th>
      <td>41096</td>
      <td>1190.256849</td>
    </tr>
  </tbody>
</table>
</div>




```python
# plot a bar graph showing how the level of rating is affected by the number of votes
df3[['level_of_rating', 'numvotes_capped']].groupby(
    ['level_of_rating']).agg(['count', 'mean']).plot(
    kind = 'bar', rot= 0, figsize= (8,15),
    subplots= True, sharex=False)
```




    array([<AxesSubplot:title={'center':'(numvotes_capped, count)'}, xlabel='level_of_rating'>,
           <AxesSubplot:title={'center':'(numvotes_capped, mean)'}, xlabel='level_of_rating'>],
          dtype=object)




    
![png](output_81_1.png)
    


## Does the length of a movie affect the rating

Most high rating movies were 90 minutes long and low rating movies had a slightly shorter. Medium rating movies had a higher median than the high rating therefore for a movie to do well, length has to be considered in order to get that optimum sweet spot for consumers.


```python
#plot a line graph
df3[['level_of_rating', 'runtime_minutes_capped', ]].groupby(['level_of_rating']).median().plot()
```




    <AxesSubplot:xlabel='level_of_rating'>




    
![png](output_83_1.png)
    


# Conclusion

This analysis leads to a few recommendations for the head of Microsoft's new movie studio.

1. Produce a genre that the market demands most (as indicated by what producers are producing more of). Documentaries ranking highest, may be prefered by consumers due to the fact that they are based on real life. A single genre will also give the company an edge in the market.

2. Invest in consumer feedback. Movies that had high ratings also had many people accessing them and rating them. Microsoft, being a tech company can leverage that and ensure it has algorithms for fetching feedback from consumers.

3. Have an optimal time for the length of the movie. Many movies that rate highly are 90 minutes long. Therefore this seems to be the optimal length for successful viewership by consumers. 

## Next Steps
Further analysis would give more insights to the Microsoft studio by:
1. Modelling the impact of change in title on the ratings. This data is available in the given dataset.
