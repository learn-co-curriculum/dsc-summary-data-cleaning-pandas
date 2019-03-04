
# Section Recap - Data Cleaning in Pandas

## Introduction

In this section you saw you to wrangle and clean some data in Pandas! This will be a baseline skill that you will use consistently in your work whether its doing sanity checks, cleaning messy data or transforming raw datasets into useful aggregates and views. Having an understanding of the format of your data is essential to critically thinking about how you can manipulate and shape it into new and interesting forms.

## Objectives

You will be able to:

* Recall various data cleaning techniques
* Explain appropriate use cases for various data cleaning techniques

## Lambda Functions

We started out by introducing lambda functions. These are quick throw away functions that you can write on the fly. They're very useful for transforming a column feature. For example, you might want to extract the day from a date.


```python
import pandas as pd
dates = pd.Series(['12-01-2017', '12-02-2017', '12-03-2017', '12-04-2017'])
dates.map(lambda x: x.split('-')[1])
```




    0    01
    1    02
    2    03
    3    04
    dtype: object



## Combining DataFrames

You can combine dataframes by merging them (joining data by a common field) or concatenating them (appending data at the beginning or end).


```python
df1 = pd.DataFrame(dates)
df2 = pd.DataFrame(['12-05-2017', '12-06-2017', '12-07-2017'])
pd.concat([df1, df2])
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>12-01-2017</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12-02-2017</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12-03-2017</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12-04-2017</td>
    </tr>
    <tr>
      <th>0</th>
      <td>12-05-2017</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12-06-2017</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12-07-2017</td>
    </tr>
  </tbody>
</table>
</div>



## Grouping and Aggregating


```python
df = pd.read_csv('titanic.csv')
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
      <th>Unnamed: 0</th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped = df.groupby(['Pclass', 'Sex'])['Age'].mean().reset_index()
grouped.head()
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
      <th>Pclass</th>
      <th>Sex</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>female</td>
      <td>34.531646</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>male</td>
      <td>41.025474</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>female</td>
      <td>27.757353</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>male</td>
      <td>30.982234</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>female</td>
      <td>21.892857</td>
    </tr>
  </tbody>
</table>
</div>



## Pivot Tables


```python
pivoted = grouped.pivot(index='Pclass', columns = 'Sex', values='Age')
pivoted
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
      <th>Sex</th>
      <th>female</th>
      <th>male</th>
    </tr>
    <tr>
      <th>Pclass</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>34.531646</td>
      <td>41.025474</td>
    </tr>
    <tr>
      <th>2</th>
      <td>27.757353</td>
      <td>30.982234</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21.892857</td>
      <td>26.437942</td>
    </tr>
    <tr>
      <th>?</th>
      <td>32.812500</td>
      <td>32.619048</td>
    </tr>
  </tbody>
</table>
</div>



## Graphing


```python
import matplotlib.pyplot as plt
%matplotlib inline
pivoted.plot(kind='barh')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x108982198>




![png](index_files/index_11_1.png)


## Missing Data


```python
print('Top 5 Values before:\n', df.Cabin.value_counts(normalize=True).reset_index()[:5])
#Not a useful means of imputing in most cases, but a simple example to recap
df.Cabin = df['Cabin'].fillna(value="?")
print('Top 5 Values after:\n', df.Cabin.value_counts(normalize=True).reset_index()[:5])
```

    Top 5 Values before:
              index     Cabin
    0           G6  0.019608
    1  C23 C25 C27  0.019608
    2      B96 B98  0.019608
    3      C22 C26  0.014706
    4         E101  0.014706
    Top 5 Values after:
              index     Cabin
    0            ?  0.771044
    1      B96 B98  0.004489
    2  C23 C25 C27  0.004489
    3           G6  0.004489
    4          F33  0.003367


## Summary

In this lesson you started practicing essential ETL skills that you will use throughout your data work to transform and wrangle data into useful forms.
