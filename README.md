# [Comparing Quantity of arrests in Eugene & Springfield]

[The objective of this research is to investigate if emergency calls were escalated to unnecessary measures by the Eugene Police Department after CAHOOTS stopped services. This research project specifically looks at number of arrests between the Eugene Police Department and Springfield Police Department and analyzes any parallel trends to conduct a Difference-In-Differences method.]

Import these modules

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
'''

Read 'eugene_springfield_CAD.csv' file

'''python
calls = pd.read_csv("eugene_springfield_CAD.csv")
calls.head()
'''

Filter by arrests only

'''python
filter_arrest = calls["Final Call Type"].isin(["ARREST"])
calls_arrest = calls[filter_arrest]
calls_arrest.head()
'''

Group number of arrests based on year and responding agency using groupby()

'''python
arrest_count = calls_arrest.groupby(["Year", "Responding Agency"])["Arrest"].sum().reset_index(name="Total Arrests")
arrest_count.head()
'''

Create line plot using seaborn to visualize number of arrests in a yearly timeline

'''python
custom_colors = ["#003f5c", "#ED841A"]
sns.lineplot(data=arrest_count, x="Year", y="Total Arrests", hue="Responding Agency", palette=custom_colors)
plt.title("Yearly Arrests Made By Responding Agency")
'''

Compare most frequent call types that led to arrests in Eugene and in Springfield for years 2024 and 2025. Years where line plot shows Diversion between EPD and SPD number of arrests

'''python
filter_year = calls["Year"].isin([2024, 2025])
filter_type = calls["Final Call Type"].isin(["ARREST"])
calls2425 = calls[filter_year & filter_type]
calls2425.head()
'''

Identify top 10 most frequent initial call types in Eugene

'''python
epd_filter = calls2425["Responding Agency"].isin(["EPD"])
calls2425eug = calls2425[epd_filter]

most_frequent_eugene = calls2425eug["Initial Call Type"].value_counts()
most_frequent_eugene.head()
'''

Convert series to an array

'''python
top_10_eugene = most_frequent_eugene.head(10).index
eugene_array = top_10_eugene.to_numpy()
eugene_array
'''
Identify top 10 most freqent initial call types in Springfield

'''python
spd_filter = calls2425["Responding Agency"].isin(["SPD"])
calls2425spring = calls2425[spd_filter]

most_frequent_spring = calls2425spring["Initial Call Type"].value_counts()
most_frequent_spring.head(10)
'''

Convert series to an array

'''python
top_10_springfield = most_frequent_spring.head(10).index
springfield_array = top_10_springfield.to_numpy()
springfield_array
'''

Filter data set to only top 10 most frequent call types from Eugene and Springfield in 2024 and 2025

'''python
most_frequent = np.concatenate((eugene_array, springfield_array), axis=None)
filter_call_type = calls2425["Initial Call Type"].isin(most_frequent)
filter_agency = calls2425["Responding Agency"].isin(["EPD", "SPD"])
top_calls = calls2425[filter_call_type & filter_agency]
top_calls.head()
'''

