```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

# Concatenate All Eugene Dataset


```python
eugene_15 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2015noloc.csv")
eugene_16 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2016noloc.csv")
eugene_17 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2017noloc.csv")
eugene_18 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2018noloc.csv")
eugene_19 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2019noloc.csv")
eugene_20 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2020noloc.csv")
eugene_21 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2021noloc.csv", dtype={5: str})
eugene_22 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2022noloc.csv")
eugene_23 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2023noloc.csv")
eugene_24 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2024noloc.csv")
eugene_25 = pd.read_csv("Eugene_CAD_data_noloc/EugeneCAD2025noloc.csv", dtype={6: str})
```


```python
all_eugene = pd.concat([eugene_15, eugene_16, eugene_17, eugene_18,eugene_19, eugene_20, eugene_21, eugene_22,
                       eugene_23, eugene_24, eugene_25], ignore_index=True)
all_eugene.head()
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
      <th>yr</th>
      <th>agency</th>
      <th>service</th>
      <th>inci_id</th>
      <th>calltime</th>
      <th>case_id</th>
      <th>callsource</th>
      <th>nature</th>
      <th>closecode</th>
      <th>closed_as</th>
      <th>secs_to_disp</th>
      <th>secs_to_arrv</th>
      <th>secs_to_close</th>
      <th>disp</th>
      <th>arrv</th>
      <th>priority</th>
      <th>primeunit</th>
      <th>units_dispd</th>
      <th>units_arrived</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15000001</td>
      <td>2015-01-01 00:00:00.000</td>
      <td>NaN</td>
      <td>SELF</td>
      <td>PERSON STOP</td>
      <td>ASST</td>
      <td>ASSISTED</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>217</td>
      <td>1</td>
      <td>1</td>
      <td>6</td>
      <td>_5E48</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15000002</td>
      <td>2015-01-01 00:00:44.000</td>
      <td>NaN</td>
      <td>SELF</td>
      <td>FIGHT</td>
      <td>RSLV</td>
      <td>RESOLVED</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2114</td>
      <td>1</td>
      <td>1</td>
      <td>P</td>
      <td>_3F65</td>
      <td>4</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15000003</td>
      <td>2015-01-01 00:01:05.000</td>
      <td>NaN</td>
      <td>PHONE</td>
      <td>CHECK WELFARE</td>
      <td>ASST</td>
      <td>ASSISTED</td>
      <td>708.0</td>
      <td>1094.0</td>
      <td>1538</td>
      <td>1</td>
      <td>1</td>
      <td>5</td>
      <td>_3J79</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15000007</td>
      <td>2015-01-01 00:03:16.000</td>
      <td>NaN</td>
      <td>W911</td>
      <td>SHOTS FIRED</td>
      <td>PCHK</td>
      <td>PATROL CHECK</td>
      <td>277.0</td>
      <td>576.0</td>
      <td>891</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>_5E48</td>
      <td>2</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15000010</td>
      <td>2015-01-01 00:03:34.000</td>
      <td>NaN</td>
      <td>SELF</td>
      <td>ILLEGAL FIREWORKS</td>
      <td>ADVI</td>
      <td>ADVISED</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>150</td>
      <td>1</td>
      <td>1</td>
      <td>5</td>
      <td>_5K97</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

## Filter Eugene Dataset

### Only use values that pertain to mental health crisis or drug-related crisis AND ended as an arrest


```python
nature_of_call = ["CHECK WELFARE", "DISORDERLY SUBJECT", "ASSIST OUTSIDE AGENCY", "INTOXICATED SUBJECT", "DISORIENTED SUBJECT",
                "OVERDOSE", "SUICIDAL SUBJECT", "SUICIDE", "FOUND SYRINGE", "SUBJECT SCREAMING", "LOCATE MISSING PERSON",
                "CONTROLLED SUBSTANCE VIOLATION", "MENTAL SUBJECT", "DISORDERLY CONDUCT", "DETOXIFICATION", "MENTAL TRANSPORT",
                ]
closed_as = ["ARREST"]
```


```python
filter1 = all_eugene["nature"].isin(nature_of_call)
filter2 = all_eugene["closed_as"].isin(closed_as)
eugene_arrests = all_eugene[filter1 & filter2]
eugene_arrests.head()
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
      <th>yr</th>
      <th>agency</th>
      <th>service</th>
      <th>inci_id</th>
      <th>calltime</th>
      <th>case_id</th>
      <th>callsource</th>
      <th>nature</th>
      <th>closecode</th>
      <th>closed_as</th>
      <th>secs_to_disp</th>
      <th>secs_to_arrv</th>
      <th>secs_to_close</th>
      <th>disp</th>
      <th>arrv</th>
      <th>priority</th>
      <th>primeunit</th>
      <th>units_dispd</th>
      <th>units_arrived</th>
      <th>month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>83</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15000185</td>
      <td>2015-01-01 03:48:56.000</td>
      <td>1500016.0</td>
      <td>E911</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
      <td>734.0</td>
      <td>734.0</td>
      <td>7772</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>_5B81</td>
      <td>2</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>635</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15001529</td>
      <td>2015-01-02 21:16:05.000</td>
      <td>1500089.0</td>
      <td>W911</td>
      <td>CHECK WELFARE</td>
      <td>ARR</td>
      <td>ARREST</td>
      <td>166.0</td>
      <td>414.0</td>
      <td>15848</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>_5E66</td>
      <td>5</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>636</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15001531</td>
      <td>2015-01-02 21:21:51.000</td>
      <td>1500090.0</td>
      <td>SELF</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
      <td>0.0</td>
      <td>50.0</td>
      <td>5017</td>
      <td>1</td>
      <td>1</td>
      <td>6</td>
      <td>_4U71</td>
      <td>3</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1237</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15003099</td>
      <td>2015-01-05 02:53:52.000</td>
      <td>1500214.0</td>
      <td>E911</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
      <td>192.0</td>
      <td>316.0</td>
      <td>12361</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>_6E35</td>
      <td>4</td>
      <td>4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1510</th>
      <td>2015</td>
      <td>EPD</td>
      <td>LAW</td>
      <td>15003750</td>
      <td>2015-01-05 22:58:39.000</td>
      <td>1500282.0</td>
      <td>W911</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
      <td>203.0</td>
      <td>600.0</td>
      <td>12870</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>_6E19</td>
      <td>4</td>
      <td>4</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### Keep The Necessary Columns: Year, Agency, Nature of Call, and How the Call Was Closed


```python
eugene_arrests = eugene_arrests.drop(columns=["service", "inci_id", "calltime", "case_id", "callsource", "secs_to_disp",
                                              "secs_to_arrv", "secs_to_close", "disp", "arrv", "priority", "primeunit",
                                             "units_dispd", "units_arrived", "month"])

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
      <th>yr</th>
      <th>agency</th>
      <th>nature</th>
      <th>closecode</th>
      <th>closed_as</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>83</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>635</th>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>636</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>1237</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>1510</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
  </tbody>
</table>
</div>




```python
eugene_arrests.head()
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
      <th>yr</th>
      <th>agency</th>
      <th>nature</th>
      <th>closecode</th>
      <th>closed_as</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>83</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>635</th>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>636</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>1237</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>1510</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
  </tbody>
</table>
</div>




```python
eugene_arrests.shape
```




    (5140, 5)



# Concatenate all Springfield Dataset


```python
springfield_15 = pd.read_csv("Springfield_CAD_data/2015_spd_calls.csv")
springfield_16 = pd.read_csv("Springfield_CAD_data/2016_spd_calls.csv")
springfield_17 = pd.read_csv("Springfield_CAD_data/2017_spd_calls.csv")
springfield_18 = pd.read_csv("Springfield_CAD_data/2018_spd_calls.csv")
springfield_19 = pd.read_csv("Springfield_CAD_data/2019_spd_calls.csv")
springfield_20 = pd.read_csv("Springfield_CAD_data/2020_spd_calls.csv")
springfield_21 = pd.read_csv("Springfield_CAD_data/2021_spd_calls.csv")
springfield_22 = pd.read_csv("Springfield_CAD_data/2022_spd_calls.csv")
springfield_23 = pd.read_csv("Springfield_CAD_data/2023_spd_calls.csv")
springfield_24 = pd.read_csv("Springfield_CAD_data/2024_spd_calls.csv")
springfield_25 = pd.read_csv("Springfield_CAD_data/2025_spd_calls.csv")
```




    (54804, 11)



## The Springfield data frames are missing the "Year" variable, so I'll manually add it to each data frame


```python
springfield_15["yr"] = 2015
springfield_16["yr"] = 2016
springfield_17["yr"] = 2017
springfield_18["yr"] = 2018
springfield_19["yr"] = 2019
springfield_20["yr"] = 2020
springfield_21["yr"] = 2021
springfield_22["yr"] = 2022
springfield_23["yr"] = 2023
springfield_24["yr"] = 2024
springfield_25["yr"] = 2025
```

## The Springfield data frames are also missing information about how the call was closed

## Luckily, Dr. Rori Rohlfs provided an excel file with the missing information. 

## The newly acquired data sets contains values as 'Incident Number' which will be used to merge the Springfield CAD data to add a new column. The new column contains information on how the call was closed 


```python
closed_15 = pd.read_csv("2015_spd_close_codes.csv")
closed_16 = pd.read_csv("2016_spd_close_codes.csv")
closed_17 = pd.read_csv("2017_spd_close_codes.csv")
closed_18 = pd.read_csv("2018_spd_close_codes.csv")
closed_19 = pd.read_csv("2019_spd_close_codes.csv")
closed_20 = pd.read_csv("2020_spd_close_codes.csv")
closed_21 = pd.read_csv("2021_spd_close_codes.csv")
closed_22 = pd.read_csv("2022_spd_close_codes.csv")
closed_23 = pd.read_csv("2023_spd_close_codes.csv")
closed_24 = pd.read_csv("2024_spd_close_codes.csv")
closed_25 = pd.read_csv("2025_spd_close_codes.csv")
closed_25.columns
```




    Index(['Incident Number', 'Close Code'], dtype='object')



## Now we merge both data frames using "Incident Number" as the column they both shared

## I'll keep the rows where the shared column values are in BOTH data frames in "Incident Number" column


```python
merged_15 = pd.merge(springfield_15, closed_15, on='Incident Number', how='inner')
merged_16 = pd.merge(springfield_16, closed_16, on='Incident Number', how='inner')
merged_17 = pd.merge(springfield_17, closed_17, on='Incident Number', how='inner')
merged_18 = pd.merge(springfield_18, closed_18, on='Incident Number', how='inner')
merged_19 = pd.merge(springfield_19, closed_19, on='Incident Number', how='inner')
merged_20 = pd.merge(springfield_20, closed_20, on='Incident Number', how='inner')
merged_21 = pd.merge(springfield_21, closed_21, on='Incident Number', how='inner')
merged_22 = pd.merge(springfield_22, closed_22, on='Incident Number', how='inner')
merged_23 = pd.merge(springfield_23, closed_23, on='Incident Number', how='inner')
merged_24 = pd.merge(springfield_24, closed_24, on='Incident Number', how='inner')
merged_25 = pd.merge(springfield_25, closed_25, on='Incident Number', how='inner')
```

## Now I concatenate all dataframes into one


```python
all_springfield = pd.concat([merged_15, merged_16, merged_17, merged_18, merged_19, merged_20, merged_21, merged_22,
                       merged_23, merged_24, merged_25], ignore_index=True)
all_springfield.head()
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
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Responding Agency</th>
      <th>Primary Responding Unit</th>
      <th>Call Creation Time</th>
      <th>First Dispatched Time</th>
      <th>First Arrival Time</th>
      <th>Clear Time</th>
      <th>Priority</th>
      <th>Call Creation Mechanism</th>
      <th>yr</th>
      <th>Close Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15000074</td>
      <td>ALMAUD</td>
      <td>AUDIBLE ALARM</td>
      <td>SPD</td>
      <td>1S18</td>
      <td>16:21.0</td>
      <td>18:28.0</td>
      <td>21:13.0</td>
      <td>32:08.0</td>
      <td>3</td>
      <td>PHONE</td>
      <td>2015</td>
      <td>BLDS</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15000083</td>
      <td>TRFSTP</td>
      <td>DWS</td>
      <td>SPD</td>
      <td>3D2</td>
      <td>22:29.0</td>
      <td>22:29.0</td>
      <td>22:29.0</td>
      <td>34:57.0</td>
      <td>4</td>
      <td>SELF</td>
      <td>2015</td>
      <td>UTC</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15000167</td>
      <td>MVAUNK</td>
      <td>MOTOR VEH ACC UNKNOWN INJ</td>
      <td>SPD</td>
      <td></td>
      <td>15:28.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3</td>
      <td>E911</td>
      <td>2015</td>
      <td>DUP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15000216</td>
      <td>TRFSTP</td>
      <td>DWS</td>
      <td>SPD</td>
      <td>1S22</td>
      <td>27:24.0</td>
      <td>27:24.0</td>
      <td>27:24.0</td>
      <td>38:53.0</td>
      <td>4</td>
      <td>SELF</td>
      <td>2015</td>
      <td>UTC</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15000222</td>
      <td>SUSPVE</td>
      <td>SUSPICIOUS VEHICLE</td>
      <td>SPD</td>
      <td>1S11</td>
      <td>52:53.0</td>
      <td>53:57.0</td>
      <td>56:21.0</td>
      <td>04:04.0</td>
      <td>3</td>
      <td>PHONE</td>
      <td>2015</td>
      <td>INFO</td>
    </tr>
  </tbody>
</table>
</div>



## Filter Springfield Dataset

### Only use values that pertain to mental health crisis or drug-related crisis AND ended as an arrest


```python
nature_call = ["CHECK WELFARE", "DISORDERLY SUBJECT", "ASSIST OUTSIDE AGENCY", "INTOXICATED SUBJECT", "DISORIENTED SUBJECT",
                "OVERDOSE", "SUICIDAL SUBJECT", "SUICIDE", "FOUND SYRINGE", "SUBJECT SCREAMING", "LOCATE MISSING PERSON",
                "CONTROLLED SUBSTANCE VIOLATION", "MENTAL SUBJECT", "DISORDERLY CONDUCT", "DETOXIFICATION", "MENTAL TRANSPORT",
                ]
close_code = ["ARR "]
```


```python
filter_spring1 = all_springfield["Final Call Type"].isin(nature_call)
filter_spring2 = all_springfield["Close Code"].isin(close_code)
springfield_arrests = all_springfield[filter_spring1 & filter_spring2]
springfield_arrests.head()
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
      <th>Initial Call Type</th>
      <th>Final Call Type</th>
      <th>Responding Agency</th>
      <th>Primary Responding Unit</th>
      <th>Call Creation Time</th>
      <th>First Dispatched Time</th>
      <th>First Arrival Time</th>
      <th>Clear Time</th>
      <th>Priority</th>
      <th>Call Creation Mechanism</th>
      <th>yr</th>
      <th>Close Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1767</th>
      <td>15004858</td>
      <td>DSRDSU</td>
      <td>DISORDERLY CONDUCT</td>
      <td>SPD</td>
      <td>2S22</td>
      <td>05:51.0</td>
      <td>12:37.0</td>
      <td>16:29.0</td>
      <td>56:57.0</td>
      <td>5</td>
      <td>W911</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>2238</th>
      <td>15006247</td>
      <td>DSRDSU</td>
      <td>DISORDERLY SUBJECT</td>
      <td>SPD</td>
      <td>1S11</td>
      <td>50:34.0</td>
      <td>53:07.0</td>
      <td>58:51.0</td>
      <td>37:18.0</td>
      <td>3</td>
      <td>PHONE</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>3424</th>
      <td>15008548</td>
      <td>DSRDSU</td>
      <td>DISORDERLY SUBJECT</td>
      <td>SPD</td>
      <td>1S12</td>
      <td>41:09.0</td>
      <td>44:26.0</td>
      <td>49:11.0</td>
      <td>33:14.0</td>
      <td>3</td>
      <td>PHONE</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4214</th>
      <td>15010811</td>
      <td>SUISUB</td>
      <td>SUICIDAL SUBJECT</td>
      <td>SPD</td>
      <td>1S23</td>
      <td>02:34.0</td>
      <td>04:14.0</td>
      <td>09:36.0</td>
      <td>27:27.0</td>
      <td>3</td>
      <td>PHONE</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4968</th>
      <td>15012737</td>
      <td>DSPUT</td>
      <td>DISORDERLY SUBJECT</td>
      <td>SPD</td>
      <td>1S21</td>
      <td>55:58.0</td>
      <td>58:43.0</td>
      <td>00:43.0</td>
      <td>51:18.0</td>
      <td>3</td>
      <td>W911</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
  </tbody>
</table>
</div>



### Keep The Necessary Columns: Year, Agency, Nature of Call, and How the Call Was Closed


```python
springfield_arrests = springfield_arrests.drop(columns=["Incident Number", "Initial Call Type", "Primary Responding Unit", "Call Creation Time",
                                                        "First Dispatched Time", "First Arrival Time",
                                              "Clear Time", "Priority", "Call Creation Mechanism"])
```


```python
springfield_arrests.head()
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
      <th>Final Call Type</th>
      <th>Responding Agency</th>
      <th>yr</th>
      <th>Close Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1767</th>
      <td>DISORDERLY CONDUCT</td>
      <td>SPD</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>2238</th>
      <td>DISORDERLY SUBJECT</td>
      <td>SPD</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>3424</th>
      <td>DISORDERLY SUBJECT</td>
      <td>SPD</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4214</th>
      <td>SUICIDAL SUBJECT</td>
      <td>SPD</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4968</th>
      <td>DISORDERLY SUBJECT</td>
      <td>SPD</td>
      <td>2015</td>
      <td>ARR</td>
    </tr>
  </tbody>
</table>
</div>



## Next, I'll organize rename 'springfield_arrests' columns to  match 'eugene_arrests' data frame


```python
eugene_arrests.columns
```




    Index(['yr', 'agency', 'nature', 'closecode', 'closed_as'], dtype='object')




```python
springfield_arrests = springfield_arrests[["yr", "Responding Agency", "Final Call Type", "Close Code"]]
springfield_arrests.head()
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
      <th>yr</th>
      <th>Responding Agency</th>
      <th>Final Call Type</th>
      <th>Close Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1767</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY CONDUCT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>2238</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>3424</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4214</th>
      <td>2015</td>
      <td>SPD</td>
      <td>SUICIDAL SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4968</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
  </tbody>
</table>
</div>




```python
springfield_arrests = springfield_arrests.rename(columns={"Responding Agency": "agency", "Final Call Type": "nature", "Close Code": "closecode"})
springfield_arrests
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
      <th>yr</th>
      <th>agency</th>
      <th>nature</th>
      <th>closecode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1767</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY CONDUCT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>2238</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>3424</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4214</th>
      <td>2015</td>
      <td>SPD</td>
      <td>SUICIDAL SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4968</th>
      <td>2015</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>565501</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY CONDUCT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>565505</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>566125</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY CONDUCT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>566510</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>566937</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
  </tbody>
</table>
<p>1587 rows × 4 columns</p>
</div>



# I concatenate the clean and filtered Springfield dataframe with the clean and filtered Eugene dataframe


```python
eugene_springfield = pd.concat([eugene_arrests, springfield_arrests], ignore_index=True)
eugene_springfield.head()
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
      <th>yr</th>
      <th>agency</th>
      <th>nature</th>
      <th>closecode</th>
      <th>closed_as</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
      <td>ARREST</td>
    </tr>
  </tbody>
</table>
</div>



## Finally, I inspect the concatenated dataframe to ensure all values match and there is no null values


```python
eugene_springfield["yr"].unique()
```




    array([2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2025])




```python
eugene_springfield["agency"].unique()
```




    array(['EPD ', 'SPD '], dtype=object)




```python
eugene_springfield["nature"].unique()
```




    array(['DISORDERLY SUBJECT', 'CHECK WELFARE', 'ASSIST OUTSIDE AGENCY',
           'INTOXICATED SUBJECT', 'SUICIDAL SUBJECT', 'OVERDOSE',
           'LOCATE MISSING PERSON', 'CONTROLLED SUBSTANCE VIOLATION',
           'DETOXIFICATION', 'SUBJECT SCREAMING', 'DISORIENTED SUBJECT',
           'DISORDERLY CONDUCT', 'MENTAL SUBJECT', 'MENTAL TRANSPORT'],
          dtype=object)




```python
eugene_springfield["closecode"].unique()
```




    array(['ARR '], dtype=object)




```python
eugene_springfield["closed_as"].unique()
```




    array(['ARREST', nan], dtype=object)



## I noticed I don't need the "closed_as" column, so I'll just drop it


```python
eugene_springfield = eugene_springfield.drop(columns=["closed_as"])
```


```python
eugene_springfield
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
      <th>yr</th>
      <th>agency</th>
      <th>nature</th>
      <th>closecode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>EPD</td>
      <td>CHECK WELFARE</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>EPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>6722</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY CONDUCT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>6723</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>6724</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY CONDUCT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>6725</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
    <tr>
      <th>6726</th>
      <td>2025</td>
      <td>SPD</td>
      <td>DISORDERLY SUBJECT</td>
      <td>ARR</td>
    </tr>
  </tbody>
</table>
<p>6727 rows × 4 columns</p>
</div>



# I'll convert this final data frame into a csv file


```python
eugene_springfield.to_csv('eugene_springfield_calls.csv', index=False)
```


```python

```
