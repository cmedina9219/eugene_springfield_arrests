# Comparing Quantity of arrests in Eugene & Springfield

My research investigates how the Eugene Police Department is handling calls without CAHOOTS assistance. This research project specifically looks at number of arrests which is an indication of unnecessary escalation from the Eugene Police Department





### Import pandas, numpy, matplotlib, and seaborn


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


### Read the clean CAD data set from Eugene and Springfield


```python
calls = pd.read_csv("eugene_springfield_CAD.csv")
calls.head()
```


### Filter by arrests only


```python
filter_arrest = calls["Final Call Type"].isin(["ARREST"])
calls_arrest = calls[filter_arrest]
calls_arrest.head()
```


### Group number of arrests based on year and agency


```python
arrest_count = calls_arrest.groupby(["Year", "Responding Agency"])["Arrest"].sum().reset_index(name="Total Arrests")
arrest_count.head()
```


### Create line plot using seaborn to visualize number of arrests in a yearly timeline


```python
custom_colors = ["#003f5c", "#ED841A"]
sns.lineplot(data=arrest_count, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Yearly Arrests Made By Responding Agency")
```


### Compare most frequent call types that led to arrests in Eugene and in Springfield for years 2024 and 2025. Years where line plot shows Diversion between EPD and SPD number of arrests


```python
filter_year = calls["Year"].isin([2024, 2025])
filter_type = calls["Final Call Type"].isin(["ARREST"])
calls2425 = calls[filter_year & filter_type]
calls2425.head()
```


### Identify top 10 most frequent initial call types in Eugene


```python
epd_filter = calls2425["Responding Agency"].isin(["EPD"])
calls2425eug = calls2425[epd_filter]
calls2425eug.head()
most_frequent_eugene = calls2425eug["Initial Call Type"].value_counts()
most_frequent_eugene.head()
```


### Convert series to an array


```python
top_10_eugene = most_frequent_eugene.head(10).index
eugene_array = top_10_eugene.to_numpy()
eugene_array
```


### Identify top 10 most frequent initial call types in Springfield


```python
spd_filter = calls2425["Responding Agency"].isin(["SPD"])
calls2425spring = calls2425[spd_filter]
most_frequent_spring = calls2425spring["Initial Call Type"].value_counts()
most_frequent_spring.head(10)
```


### Convert series to an array


```python
top_10_springfield = most_frequent_spring.head(10).index
springfield_array = top_10_springfield.to_numpy()
springfield_array
```


### Filter data set to only top 10 most frequent call types in Eugene and Springfield for 2024 and 2025


```python
most_frequent = np.concatenate((eugene_array, springfield_array), axis=None)
filter_call_type = calls2425["Initial Call Type"].isin(most_frequent)
filter_agency = calls2425["Responding Agency"].isin(["EPD", "SPD"])
top_calls = calls2425[filter_call_type & filter_agency]
top_calls.head()
```


### Create a bar plot to compare EPD and SPD most frequent call types by grouping number of arrests based on agency and initial call type


```python
group_calls = top_calls.groupby(["Responding Agency", "Initial Call Type", "Final Call Type"]).size().reset_index(name="Total Arrests")
sns.barplot(group_calls, x="Total Arrests", y="Initial Call Type", hue="Responding Agency", palette=custom_colors)
plt.title("Initial Call Types January 1st 2024 - December 31st 2025")
```


### Create a new array with the most frequent SHARED call types between EPD and SPD


```python
common_array = np.array(["CHECK WELFARE", "DISPUTE", "FOLLOW UP", "THEFT", "TRAFFIC STOP", "TRESPASS"])
common_array
```


### Create a line plot for each shared call type from 2015 - 2025. Comparing Number of arrests between agencies.
### Purpose of this is to check for parallel trends


```python
filter_common_calls = calls["Initial Call Type"].isin(common_array)
common_calls = calls[filter_common_calls & filter_type]
common_calls.head()
```


### Group by year, responding agency, call type, and final call type


```python
group_common_calls = common_calls.groupby(["Year", "Responding Agency", "Initial Call Type", "Final Call Type"]).size().reset_index(name="Total Arrests")
group_common_calls.head()
```


### Create line plot for 'Check Welfare' calls


```python
filter_welfare = group_common_calls["Initial Call Type"].isin(["CHECK WELFARE"])
group_welfarecheck = group_common_calls[filter_welfare]

sns.lineplot(data=group_welfarecheck, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Check Welfare' Ending in Arrests")
```


### Create line plot for 'Theft' calls


```python
filter_theft = group_common_calls["Initial Call Type"].isin(["THEFT"])
group_theft = group_common_calls[filter_theft]

sns.lineplot(data=group_theft, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Theft' Ending in Arrests")
```


### Create line plot for 'Traffic Stop' calls


```python
filter_traffic_stop = group_common_calls["Initial Call Type"].isin(["TRAFFIC STOP"])
group_traffic_stop = group_common_calls[filter_traffic_stop]

sns.lineplot(data=group_traffic_stop, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Traffic Stop' Ending in Arrests")
```


### Create line plot for 'Follow Up' calls


```python
filter_followup = group_common_calls["Initial Call Type"].isin(["FOLLOW UP"])
group_followup = group_common_calls[filter_followup]

sns.lineplot(data=group_followup, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Follow Up' Ending in Arrests")
```


### Create line plot for 'Dispute' calls


```python
filter_dispute = group_common_calls["Initial Call Type"].isin(["DISPUTE"])
group_dispute = group_common_calls[filter_dispute]

sns.lineplot(data=group_dispute, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Dispute' Ending in Arrests")
```


### Create line plot for 'Trespass' calls


```python
filter_trespass = group_common_calls["Initial Call Type"].isin(["TRESPASS"])
group_trespass = group_common_calls[filter_trespass]

sns.lineplot(data=group_trespass, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Call Types labeled as 'Trespass' Ending in Arrests")
```
    

### Calculate arrests rate per week, comparing them before April 7th 2025 and after. The Date CAHOOTS stopped services in Eugene


```python
# make a copy of 'calls' dataframe
calls_copy = calls.copy()
calls_copy.head()
```


```python
split_date = pd.to_datetime('2025-04-07')
calls_copy['Date'] = pd.to_datetime(calls_copy['Date'], format='mixed')
calls_copy['Period'] = np.where(calls_copy['Date'] < split_date, 'Before 04/07/2025', '04/07/2025 And After')

calls_copy.head()
```


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


### Remove Cahoots call and convert rate to %


```python
police_filter = overall_comparison["Responding Agency"].isin(["EPD", "SPD"])
arrest_rate = overall_comparison[police_filter]
arrest_rate["Average Arrests(%)"] = overall_comparison["Arrest Rate"] * 100
arrest_rate.head()
```


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
