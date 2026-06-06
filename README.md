```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
calls = pd.read_csv("eugene_springfield_CAD.csv")
calls.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15000001</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>PERSON STOP</td>
      <td>ASSISTED</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15000002</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>FIGHT</td>
      <td>RESOLVED</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15000003</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ASSISTED</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15000007</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>SHOTS FIRED</td>
      <td>PATROL CHECK</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15000010</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>ILLEGAL FIREWORKS</td>
      <td>ADVISED</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



### Filter by arrests only


```python
filter_arrest = calls["Final Call Type"].isin(["ARREST"])
calls_arrest = calls[filter_arrest]
calls_arrest.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20</th>
      <td>15000043</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>ASSAULT</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>59</th>
      <td>15000116</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>FIGHT</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>60</th>
      <td>15000117</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>FIGHT</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>78</th>
      <td>15000175</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>83</th>
      <td>15000185</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### Group number of arrests based on year and agency


```python
arrest_count = calls_arrest.groupby(["Year", "Responding Agency"])["Arrest"].sum().reset_index(name="Total Arrests")
arrest_count.head()
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
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Total Arrests</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>EPD</td>
      <td>3756</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>SPD</td>
      <td>3023</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016</td>
      <td>EPD</td>
      <td>3995</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016</td>
      <td>SPD</td>
      <td>3575</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017</td>
      <td>EPD</td>
      <td>4027</td>
    </tr>
  </tbody>
</table>
</div>



### Create line plot using seaborn to visualize number of arrests in a yearly timeline


```python
custom_colors = ["#003f5c", "#ED841A"]
sns.lineplot(data=arrest_count, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Yearly Arrests Made By Responding Agency")
```




    Text(0.5, 1.0, 'Yearly Arrests Made By Responding Agency')




    
![png](experimental_analysis_files/experimental_analysis_7_1.png)
    


### Compare most frequent call types that led to arrests in Eugene and in Springfield for years 2024 and 2025. Years where line plot shows Diversion between EPD and SPD number of arrests


```python
filter_year = calls["Year"].isin([2024, 2025])
filter_type = calls["Final Call Type"].isin(["ARREST"])
calls2425 = calls[filter_year & filter_type]
calls2425.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1196033</th>
      <td>24000059</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196034</th>
      <td>24000063</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196038</th>
      <td>24000076</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>CITIZEN CONTACT</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196064</th>
      <td>24000139</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196086</th>
      <td>24000215</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>PROWLER</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### Find out top 10 most frequent initial call types in Eugene


```python
epd_filter = calls2425["Responding Agency"].isin(["EPD"])
calls2425eug = calls2425[epd_filter]
calls2425eug.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1196033</th>
      <td>24000059</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196034</th>
      <td>24000063</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196038</th>
      <td>24000076</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>CITIZEN CONTACT</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196064</th>
      <td>24000139</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196086</th>
      <td>24000215</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>PROWLER</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
most_frequent_eugene = calls2425eug["Initial Call Type"].value_counts()
most_frequent_eugene.head()
```




    Initial Call Type
    PATROL CHECK          1444
    DISPUTE                907
    TRESPASS               860
    DISORDERLY SUBJECT     709
    PERSON STOP            487
    Name: count, dtype: int64



### Convert series to an array


```python
top_10_eugene = most_frequent_eugene.head(10).index
eugene_array = top_10_eugene.to_numpy()
eugene_array
```




    array(['PATROL CHECK', 'DISPUTE', 'TRESPASS', 'DISORDERLY SUBJECT',
           'PERSON STOP', 'TRAFFIC STOP', 'LOCATION WANTED SUBJECT',
           'SHOPLIFT', 'CHECK WELFARE', 'THEFT'], dtype=object)



### Find out top 10 most frequent initial call types in Springfield


```python
spd_filter = calls2425["Responding Agency"].isin(["SPD"])
calls2425spring = calls2425[spd_filter]
calls2425spring.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1922181</th>
      <td>24000009</td>
      <td>2024-01-01 00:00:00</td>
      <td>2024</td>
      <td>SPD</td>
      <td>TRAFFIC STOP</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1922209</th>
      <td>24000154</td>
      <td>2024-01-01 00:00:00</td>
      <td>2024</td>
      <td>SPD</td>
      <td>ATLDRK</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1922212</th>
      <td>24000176</td>
      <td>2024-01-01 00:00:00</td>
      <td>2024</td>
      <td>SPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1922213</th>
      <td>24000177</td>
      <td>2024-01-01 00:00:00</td>
      <td>2024</td>
      <td>SPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1922223</th>
      <td>24000246</td>
      <td>2024-01-01 00:00:00</td>
      <td>2024</td>
      <td>SPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
most_frequent_spring = calls2425spring["Initial Call Type"].value_counts()
most_frequent_spring.head(10)
```




    Initial Call Type
    TRAFFIC STOP                 717
    TRESPASS                     484
    DISPUTE                      394
    LOCATION SUBJECT             286
    PERSON STOPPED               247
    PROPERTY LOCKOUT             241
    DEATH SCENE INVESTIGATION    223
    THEFT                        210
    FOLLOW UP                    174
    WARSER                       136
    Name: count, dtype: int64



### Convert series to an array


```python
top_10_springfield = most_frequent_spring.head(10).index
springfield_array = top_10_springfield.to_numpy()
springfield_array
```




    array(['TRAFFIC STOP', 'TRESPASS', 'DISPUTE', 'LOCATION SUBJECT',
           'PERSON STOPPED', 'PROPERTY LOCKOUT', 'DEATH SCENE INVESTIGATION',
           'THEFT', 'FOLLOW UP', 'WARSER'], dtype=object)



### Filter data set to only top 10 most frequent call types in Eugene and Springfield for 2024 and 2025


```python
most_frequent = np.concatenate((eugene_array, springfield_array), axis=None)
filter_call_type = calls2425["Initial Call Type"].isin(most_frequent)
filter_agency = calls2425["Responding Agency"].isin(["EPD", "SPD"])
top_calls = calls2425[filter_call_type & filter_agency]
top_calls.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1196033</th>
      <td>24000059</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196034</th>
      <td>24000063</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196064</th>
      <td>24000139</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196200</th>
      <td>24000551</td>
      <td>2024-01-01</td>
      <td>2024</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1196329</th>
      <td>24000928</td>
      <td>2024-01-02</td>
      <td>2024</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### Create a bar plot to compare EPD and SPD most frequent call types

### Group number of arrests based on agency and initial call type


```python
group_calls = top_calls.groupby(["Responding Agency", "Initial Call Type", "Final Call Type"]).size().reset_index(name="Total Arrests")
group_calls.head()
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
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Total Arrests</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARREST</td>
      <td>185</td>
    </tr>
    <tr>
      <th>1</th>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARREST</td>
      <td>709</td>
    </tr>
    <tr>
      <th>2</th>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>907</td>
    </tr>
    <tr>
      <th>3</th>
      <td>EPD</td>
      <td>FOLLOW UP</td>
      <td>ARREST</td>
      <td>131</td>
    </tr>
    <tr>
      <th>4</th>
      <td>EPD</td>
      <td>LOCATION WANTED SUBJECT</td>
      <td>ARREST</td>
      <td>300</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.barplot(group_calls, x="Total Arrests", y="Initial Call Type", hue="Responding Agency", palette=custom_colors)
plt.title("Initial Call Types January 1st 2024 - December 31st 2025")
```




    Text(0.5, 1.0, 'Initial Call Types January 1st 2024 - December 31st 2025')




    
![png](experimental_analysis_files/experimental_analysis_25_1.png)
    


### Create a new array with the most frequent SHARED call types between EPD and SPD


```python
common_array = np.array(["CHECK WELFARE", "DISPUTE", "FOLLOW UP", "THEFT", "TRAFFIC STOP", "TRESPASS"])
common_array
```




    array(['CHECK WELFARE', 'DISPUTE', 'FOLLOW UP', 'THEFT', 'TRAFFIC STOP',
           'TRESPASS'], dtype='<U13')



### Create a line plot for each shared call type from 2015 - 2025. Comparing Number of arrests between agencies.
### Purpose of this is to check for parallel trends


```python
filter_common_calls = calls["Initial Call Type"].isin(common_array)
common_calls = calls[filter_common_calls & filter2]
common_calls.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>78</th>
      <td>15000175</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>389</th>
      <td>15000912</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>579</th>
      <td>15001396</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>633</th>
      <td>15001518</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>635</th>
      <td>15001529</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### Convert date column to pd.datetime


```python
common_calls.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>78</th>
      <td>15000175</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>389</th>
      <td>15000912</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>579</th>
      <td>15001396</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>633</th>
      <td>15001518</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>TRESPASS</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
    <tr>
      <th>635</th>
      <td>15001529</td>
      <td>2015-01-02</td>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARREST</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_common_calls = common_calls.groupby(["Year", "Responding Agency", "Initial Call Type", "Final Call Type"]).size().reset_index(name="Total Arrests")
group_common_calls.head()
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
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Total Arrests</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARREST</td>
      <td>39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISPUTE</td>
      <td>ARREST</td>
      <td>298</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015</td>
      <td>EPD</td>
      <td>FOLLOW UP</td>
      <td>ARREST</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015</td>
      <td>EPD</td>
      <td>THEFT</td>
      <td>ARREST</td>
      <td>98</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>EPD</td>
      <td>TRAFFIC STOP</td>
      <td>ARREST</td>
      <td>244</td>
    </tr>
  </tbody>
</table>
</div>



### Create line plot for 'Check Welfare' calls


```python
filter_welfare = group_common_calls["Initial Call Type"].isin(["CHECK WELFARE"])
group_welfarecheck = group_common_calls[filter_welfare]

sns.lineplot(data=group_welfarecheck, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Check Welfare' Ending in Arrests")
```




    Text(0.5, 1.0, "Call Types labeled as 'Check Welfare' Ending in Arrests")




    
![png](experimental_analysis_files/experimental_analysis_34_1.png)
    


### Create line plot for 'Theft' calls


```python
filter_theft = group_common_calls["Initial Call Type"].isin(["THEFT"])
group_theft = group_common_calls[filter_theft]

sns.lineplot(data=group_theft, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Theft' Ending in Arrests")
```




    Text(0.5, 1.0, "Call Types labeled as 'Theft' Ending in Arrests")




    
![png](experimental_analysis_files/experimental_analysis_36_1.png)
    


### Create line plot for 'Traffic Stop' calls


```python
filter_traffic_stop = group_common_calls["Initial Call Type"].isin(["TRAFFIC STOP"])
group_traffic_stop = group_common_calls[filter_traffic_stop]

sns.lineplot(data=group_traffic_stop, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Traffic Stop' Ending in Arrests")
```




    Text(0.5, 1.0, "Call Types labeled as 'Traffic Stop' Ending in Arrests")




    
![png](experimental_analysis_files/experimental_analysis_38_1.png)
    


### Create line plot for 'Follow Up' calls


```python
filter_followup = group_common_calls["Initial Call Type"].isin(["FOLLOW UP"])
group_followup = group_common_calls[filter_followup]

sns.lineplot(data=group_followup, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Follow Up' Ending in Arrests")
```




    Text(0.5, 1.0, "Call Types labeled as 'Follow Up' Ending in Arrests")




    
![png](experimental_analysis_files/experimental_analysis_40_1.png)
    


### Create line plot for 'Dispute' calls


```python
filter_dispute = group_common_calls["Initial Call Type"].isin(["DISPUTE"])
group_dispute = group_common_calls[filter_dispute]

sns.lineplot(data=group_dispute, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Dispute' Ending in Arrests")
```




    Text(0.5, 1.0, "Call Types labeled as 'Dispute' Ending in Arrests")




    
![png](experimental_analysis_files/experimental_analysis_42_1.png)
    


### Create line plot for 'Trespass' calls


```python
filter_trespass = group_common_calls["Initial Call Type"].isin(["TRESPASS"])
group_trespass = group_common_calls[filter_trespass]

sns.lineplot(data=group_trespass, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Trespass' Ending in Arrests")
```




    Text(0.5, 1.0, "Call Types labeled as 'Trespass' Ending in Arrests")




    
![png](experimental_analysis_files/experimental_analysis_44_1.png)
    


### Calculate arrests rate per week, comparing them before April 7th 2025 and after. The Date CAHOOTS stopped services in Eugene


```python
# make a copy of 'calls' dataframe
calls_copy = calls.copy()
calls_copy.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15000001</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>PERSON STOP</td>
      <td>ASSISTED</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15000002</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>FIGHT</td>
      <td>RESOLVED</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15000003</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ASSISTED</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15000007</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>SHOTS FIRED</td>
      <td>PATROL CHECK</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15000010</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>ILLEGAL FIREWORKS</td>
      <td>ADVISED</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
split_date = pd.to_datetime('2025-04-07')
calls_copy['Date'] = pd.to_datetime(calls_copy['Date'], format='mixed')
calls_copy['Period'] = np.where(calls_copy['Date'] < split_date, 'Before 04/07/2025', '04/07/2025 And After')

calls_copy.head()
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
      <th>Incident Number</th>
      <th>Date</th>
      <th>Year</th>
      <th>Responding Agency</th>
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Arrest</th>
      <th>Period</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15000001</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>PERSON STOP</td>
      <td>ASSISTED</td>
      <td>0</td>
      <td>Before 04/07/2025</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15000002</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>FIGHT</td>
      <td>RESOLVED</td>
      <td>0</td>
      <td>Before 04/07/2025</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15000003</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ASSISTED</td>
      <td>0</td>
      <td>Before 04/07/2025</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15000007</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>SHOTS FIRED</td>
      <td>PATROL CHECK</td>
      <td>0</td>
      <td>Before 04/07/2025</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15000010</td>
      <td>2015-01-01</td>
      <td>2015</td>
      <td>EPD</td>
      <td>ILLEGAL FIREWORKS</td>
      <td>ADVISED</td>
      <td>0</td>
      <td>Before 04/07/2025</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Group by Period, Responding agency, and weekly intervals
weekly_rates = calls_copy.groupby([
    'Period', 
    'Responding Agency', 
    pd.Grouper(key='Date', freq='W')
])['Arrest'].mean().reset_index()

weekly_rates.rename(columns={'Arrest': 'Arrest Rate'}, inplace=True)

overall_comparison = weekly_rates.groupby(['Responding Agency', 'Period'])['Arrest Rate'].mean().reset_index()
overall_comparison
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
      <th>Responding Agency</th>
      <th>Period</th>
      <th>Arrest Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CAHE</td>
      <td>04/07/2025 And After</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CAHE</td>
      <td>Before 04/07/2025</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>EPD</td>
      <td>04/07/2025 And After</td>
      <td>0.043771</td>
    </tr>
    <tr>
      <th>3</th>
      <td>EPD</td>
      <td>Before 04/07/2025</td>
      <td>0.028048</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SPD</td>
      <td>04/07/2025 And After</td>
      <td>0.043304</td>
    </tr>
    <tr>
      <th>5</th>
      <td>SPD</td>
      <td>Before 04/07/2025</td>
      <td>0.053357</td>
    </tr>
  </tbody>
</table>
</div>



### Remove Cahoots call and convert rate to %


```python
police_filter = overall_comparison["Responding Agency"].isin(["EPD", "SPD"])
arrest_rate = overall_comparison[police_filter]
arrest_rate["Average Arrests(%)"] = overall_comparison["Arrest Rate"] * 100
arrest_rate.head()
```

    C:\Users\comed\AppData\Local\Temp\ipykernel_14608\1776491878.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      arrest_rate["Average Arrests(%)"] = overall_comparison["Arrest Rate"] * 100
    




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
      <th>Responding Agency</th>
      <th>Period</th>
      <th>Arrest Rate</th>
      <th>Average Arrests(%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>EPD</td>
      <td>04/07/2025 And After</td>
      <td>0.043771</td>
      <td>4.377127</td>
    </tr>
    <tr>
      <th>3</th>
      <td>EPD</td>
      <td>Before 04/07/2025</td>
      <td>0.028048</td>
      <td>2.804775</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SPD</td>
      <td>04/07/2025 And After</td>
      <td>0.043304</td>
      <td>4.330379</td>
    </tr>
    <tr>
      <th>5</th>
      <td>SPD</td>
      <td>Before 04/07/2025</td>
      <td>0.053357</td>
      <td>5.335714</td>
    </tr>
  </tbody>
</table>
</div>



### Create a bar graph to compare the arrests rate across ALL call types between Springfield and Eugene


```python
plt.figure(figsize=(10, 6))
ax = sns.barplot(data=arrest_rate, x='Period', y='Average Arrests(%)', hue='Responding Agency', palette=custom_colors,
                order=['Before 04/07/2025', '04/07/2025 And After'])

# Labels to each bar container
for container in ax.containers:
    ax.bar_label(container, padding=3, fmt='%.2f')

# Labels and title
plt.title('Responding Agencies With and Without CAHOOTS in Eugene')
plt.ylabel('Arrest Rate Per Week (%)')
plt.xlabel('Period')
plt.legend(loc='upper left')
plt.ylim(0,6.5)
plt.show()
```


    
![png](experimental_analysis_files/experimental_analysis_52_0.png)
    


### Create a diverging bar graph for DiD arrests rate


```python
arrests_rate = pd.DataFrame({
    'Responding Agency': ['EPD', 'SPD'],
    'Difference': [(0.015723 * 100), (-0.010053 * 100)]
})

colors = ['#e74c3c' if x < 0 else '#3498db' for x in arrests_rate['Difference']]

plt.figure(figsize=(10,6))
ax = sns.barplot(data=arrests_rate, x='Difference', y='Responding Agency', palette=colors)

# Labels to each bar container
for container in ax.containers:
    ax.bar_label(container, padding=3, fmt='%.2f')
plt.axvline(0, color='black', linewidth=1) # Add baseline
plt.title("Difference-in-Differences Arrest Rate Per Week")
plt.xlabel("Difference (%)")

plt.xlim(-2, 2) 
plt.show()
```

    C:\Users\comed\AppData\Local\Temp\ipykernel_14608\1039540543.py:9: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `y` variable to `hue` and set `legend=False` for the same effect.
    
      ax = sns.barplot(data=arrests_rate, x='Difference', y='Responding Agency', palette=colors)
    


    
![png](experimental_analysis_files/experimental_analysis_54_1.png)
    


### Call Types showing parallel trends: Follow-Up, Check Welfare, Trespass, Dispute

### Create a bar graph to compare Arrest rates for 'Follow Up' calls


```python
filter_follow_up = calls_copy["Initial Call Type"].isin(["FOLLOW UP"])
follow_up_calls = calls_copy[filter_follow_up]

# Group by Period, Responding agency, and weekly intervals
weekly_rates = follow_up_calls.groupby([
    'Period', 
    'Responding Agency', 
    pd.Grouper(key='Date', freq='W')
])['Arrest'].mean().reset_index()

weekly_rates.rename(columns={'Arrest': 'Arrest Rate'}, inplace=True)

followup_comparison = weekly_rates.groupby(['Responding Agency', 'Period'])['Arrest Rate'].mean().reset_index()
followup_comparison['Arrest Rate Per Week (%)'] = followup_comparison['Arrest Rate'] * 100


# Create the barplot
plt.figure(figsize=(10, 6))
ax = sns.barplot(data=followup_comparison, x='Period', y='Arrest Rate Per Week (%)', hue='Responding Agency', palette=custom_colors,
                order=['Before 04/07/2025', '04/07/2025 And After'])

# Labels to each bar container
for container in ax.containers:
    ax.bar_label(container, padding=3, fmt='%.2f')

# Labels and title
plt.title('Call Type: Follow Up')
plt.ylabel('Arrest Rate Per Week (%)')
plt.xlabel('Period')
plt.legend(loc='upper left')
plt.ylim(0,8)
plt.show()
```


    
![png](experimental_analysis_files/experimental_analysis_57_0.png)
    


### Create a bar graph to compare arrest rates for 'Check Welfare' calls


```python
filter_welfare = calls_copy["Initial Call Type"].isin(["CHECK WELFARE"])
police_filter = calls_copy["Responding Agency"].isin(["EPD", "SPD"])
check_welfare_calls = calls_copy[filter_welfare & police_filter]

# Group by Period, Responding agency, and weekly intervals
weekly_rates = check_welfare_calls.groupby([
    'Period', 
    'Responding Agency', 
    pd.Grouper(key='Date', freq='W')
])['Arrest'].mean().reset_index()

weekly_rates.rename(columns={'Arrest': 'Arrest Rate'}, inplace=True)

welfare_comparison = weekly_rates.groupby(['Responding Agency', 'Period'])['Arrest Rate'].mean().reset_index()
welfare_comparison['Arrest Rate Per Week (%)'] = welfare_comparison['Arrest Rate'] * 100

# Create barplot
plt.figure(figsize=(10, 6))
ax = sns.barplot(data=welfare_comparison, x='Period', y='Arrest Rate Per Week (%)', hue='Responding Agency', palette=custom_colors,
                order=['Before 04/07/2025', '04/07/2025 And After'])

# Labels to each bar container
for container in ax.containers:
    ax.bar_label(container, padding=3, fmt='%.2f')

# Labels and title
plt.title('Call Type: Check Welfare')
plt.ylabel('Arrest Rate Per Week (%)')
plt.xlabel('Period')
plt.legend(loc='upper left')
plt.ylim(0,4)
plt.show()
```


    
![png](experimental_analysis_files/experimental_analysis_59_0.png)
    


### Create a bar graph to compare Arrest rates for 'Trespass' calls


```python
filter_trespass = calls_copy["Initial Call Type"].isin(["TRESPASS"])
trespass_calls = calls_copy[filter_trespass]

# Group by Period, Responding agency, and weekly intervals
weekly_rates = trespass_calls.groupby([
    'Period', 
    'Responding Agency', 
    pd.Grouper(key='Date', freq='W')
])['Arrest'].mean().reset_index()

weekly_rates.rename(columns={'Arrest': 'Arrest Rate'}, inplace=True)

trespass_comparison = weekly_rates.groupby(['Responding Agency', 'Period'])['Arrest Rate'].mean().reset_index()
trespass_comparison['Arrest Rate Per Week (%)'] = trespass_comparison['Arrest Rate'] * 100

# Create the barplot
plt.figure(figsize=(10, 6))
ax = sns.barplot(data=trespass_comparison, x='Period', y='Arrest Rate Per Week (%)', hue='Responding Agency', palette=custom_colors,
                order=['Before 04/07/2025', '04/07/2025 And After'])

# Labels to each bar container
for container in ax.containers:
    ax.bar_label(container, padding=3, fmt='%.2f')

# Labels and title
plt.title('Call Type: Trespass')
plt.ylabel('Arrest Rate Per Week (%)')
plt.xlabel('Period')
plt.legend(loc='upper left')
plt.ylim(0,15)
plt.show()
```


    
![png](experimental_analysis_files/experimental_analysis_61_0.png)
    


### Create a bar graph to compare Arrest rates for 'Dispute' calls


```python
filter_dispute = calls_copy["Initial Call Type"].isin(["DISPUTE"])
dispute_calls = calls_copy[filter_dispute]

# Group by Period, Responding agency, and weekly intervals
weekly_rates = dispute_calls.groupby([
    'Period', 
    'Responding Agency', 
    pd.Grouper(key='Date', freq='W')
])['Arrest'].mean().reset_index()

weekly_rates.rename(columns={'Arrest': 'Arrest Rate'}, inplace=True)

dispute_comparison = weekly_rates.groupby(['Responding Agency', 'Period'])['Arrest Rate'].mean().reset_index()
dispute_comparison['Arrest Rate Per Week (%)'] = dispute_comparison['Arrest Rate'] * 100

# Create the barplot
plt.figure(figsize=(10, 6))
ax = sns.barplot(data=dispute_comparison, x='Period', y='Arrest Rate Per Week (%)', hue='Responding Agency', palette=custom_colors,
                order=['Before 04/07/2025', '04/07/2025 And After'])

# Labels to each bar container
for container in ax.containers:
    ax.bar_label(container, padding=3, fmt='%.2f')

# Labels and title
plt.title('Call Type: Dispute')
plt.ylabel('Arrest Rate Per Week (%)')
plt.xlabel('Period')
plt.legend(loc='upper left')
plt.ylim(0,10)
plt.show()
```


    
![png](experimental_analysis_files/experimental_analysis_63_0.png)
    



```python

```
