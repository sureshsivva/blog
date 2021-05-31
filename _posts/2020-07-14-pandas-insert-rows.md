# Inserting a row into pandas dataframe


```python
import pandas as pd

pd.DataFrame([('1111', 'emp1', '30', '5000'), 
              ('1112', 'emp2', '38', '5500'), 
              ('1113', 'emp3', '55', '6000'),
              ('1114', 'emp4', '40', '7000'),
              ('1115', 'emp5', '25', '4000')],
            columns=['id', 'name', 'age', 'salary'])
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


