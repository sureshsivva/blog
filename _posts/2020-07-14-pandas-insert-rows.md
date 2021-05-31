---
title: Pandas - Insert Rows
author: Suresh Siva
date: 2020-07-14 08:00:00 +0800
categories: [python, pandas]
tags: [python, pandas]
math: true
---

# Inserting rows into pandas dataframe

Let's look into 3 ways to insert rows into an existing data frame, they ways I like are,
1. using loc
2. append() with dictionary
3. append() with Series

Initializing a data frame...


```python
import pandas as pd

df = pd.DataFrame([('1111', 'emp1', '30', '5000'), 
                   ('1112', 'emp2', '38', '5500'), 
                   ('1113', 'emp3', '55', '6000'),
                   ('1114', 'emp4', '40', '7000'),
                   ('1115', 'emp5', '25', '4000')],
                  columns=['id', 'name', 'age', 'salary'])
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
      <th>id</th>
      <th>name</th>
      <th>age</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1111</td>
      <td>emp1</td>
      <td>30</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1112</td>
      <td>emp2</td>
      <td>38</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1113</td>
      <td>emp3</td>
      <td>55</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1114</td>
      <td>emp4</td>
      <td>40</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1115</td>
      <td>emp5</td>
      <td>25</td>
      <td>4000</td>
    </tr>
  </tbody>
</table>
</div>





## 1. Using loc


```python
df.loc[len(df)] = ['1116', 'emp6', '33', '5400']

df.head(10)
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
      <th>id</th>
      <th>name</th>
      <th>age</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1111</td>
      <td>emp1</td>
      <td>30</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1112</td>
      <td>emp2</td>
      <td>38</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1113</td>
      <td>emp3</td>
      <td>55</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1114</td>
      <td>emp4</td>
      <td>40</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1115</td>
      <td>emp5</td>
      <td>25</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1116</td>
      <td>emp6</td>
      <td>33</td>
      <td>5400</td>
    </tr>
  </tbody>
</table>
</div>





## 2. Using append() with Dictionary


```python
df = df.append({'id' : '1116',
                'name' : 'emp6',
                'age' : '33',
                'salary': '5400'} , 
                ignore_index=True)
```


```python
df = df.append(dict({'id' : '1117',
                     'name' : 'emp7',
                     'age' : '33',
                     'salary': '5400'}) , 
                ignore_index=True)
```


```python
df.head(10)
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
      <th>id</th>
      <th>name</th>
      <th>age</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1111</td>
      <td>emp1</td>
      <td>30</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1112</td>
      <td>emp2</td>
      <td>38</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1113</td>
      <td>emp3</td>
      <td>55</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1114</td>
      <td>emp4</td>
      <td>40</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1115</td>
      <td>emp5</td>
      <td>25</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1116</td>
      <td>emp6</td>
      <td>33</td>
      <td>5400</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1117</td>
      <td>emp7</td>
      <td>33</td>
      <td>5400</td>
    </tr>
  </tbody>
</table>
</div>





## 3. Using append() with Series


```python
df = df.append(pd.Series(['1116', 'emp6', '33', '5400'], index=df.columns), ignore_index=True)

df.head(10)
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
      <th>id</th>
      <th>name</th>
      <th>age</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1111</td>
      <td>emp1</td>
      <td>30</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1112</td>
      <td>emp2</td>
      <td>38</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1113</td>
      <td>emp3</td>
      <td>55</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1114</td>
      <td>emp4</td>
      <td>40</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1115</td>
      <td>emp5</td>
      <td>25</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1116</td>
      <td>emp6</td>
      <td>33</td>
      <td>5400</td>
    </tr>
  </tbody>
</table>
</div>





3.1. Inserting multipe rows


```python
df = df.append( [pd.Series(['1116', 'emp6', '33', '5400'], index=df.columns),
                 pd.Series(['1117', 'emp7', '33', '5400'], index=df.columns)], 
                ignore_index=True)

df.head(10)
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
      <th>id</th>
      <th>name</th>
      <th>age</th>
      <th>salary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1111</td>
      <td>emp1</td>
      <td>30</td>
      <td>5000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1112</td>
      <td>emp2</td>
      <td>38</td>
      <td>5500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1113</td>
      <td>emp3</td>
      <td>55</td>
      <td>6000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1114</td>
      <td>emp4</td>
      <td>40</td>
      <td>7000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1115</td>
      <td>emp5</td>
      <td>25</td>
      <td>4000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1116</td>
      <td>emp6</td>
      <td>33</td>
      <td>5400</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1117</td>
      <td>emp7</td>
      <td>33</td>
      <td>5400</td>
    </tr>
  </tbody>
</table>
</div>
