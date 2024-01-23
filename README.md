# Crime_data

about datasets





Columns in the two Datasets



![image](https://github.com/masiod/Fred_data/assets/61286495/cbaa9bf8-9ccb-416c-973a-ae250f985e63)


## 1-Data Gathering


We fetch crime data from the [Los Angeles Open Data Platform](https://data.lacity.org/resource/2nrs-mtv8.json) using the `requests` library in Python. Here is an example of how to retrieve and load the data into a Pandas DataFrame:

```python
import requests
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px
import missingno as msno
from folium import plugins
from folium.plugins import HeatMap

plt.style.use('fivethirtyeight')
pd.set_option('display.max_rows', 500)
```





 **Dataset 1**

**about:**

***Crime Data from 2020 to Present:***

Update 1/18/2024 - LAPD is facing issues with posting the Crime data, but we are taking immediate action to resolve the problem. We understand the importance of providing reliable and up-to-date information and are committed to delivering it.

As we work through the issues, we have temporarily reduced our updates from weekly to bi-weekly to ensure that we provide accurate information. Our team is actively working to identify and resolve these issues promptly.

We apologize for any inconvenience this may cause and appreciate your understanding. Rest assured, we are doing everything we can to fix the problem and get back to providing weekly updates as soon as possible.


This dataset reflects incidents of crime in the City of Los Angeles dating back to 2020. This data is transcribed from original crime reports that are typed on paper and therefore there may be some inaccuracies within the data. Some location fields with missing data are noted as (0°, 0°). Address fields are only provided to the nearest hundred block in order to maintain privacy. This data is as accurate as the data in the database. Please note questions or concerns in the comments.
Type: accessing APIs 

Method: Gather data by accessing APIs from source data.lacity.org . The data was gathered using the "API Access" method from (https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8/data_preview) source.




```
data=requests.get('https://data.lacity.org/resource/2nrs-mtv8.json').json()

data_crime_2020_2024 = pd.DataFrame.from_dict(data)
#store the raw data in your local data store
data_crime_2020_2024.to_csv('data_crime_2024',index=False)
#retrive the data form my local device 
data_crime_2024=pd.read_csv('data_crime_2024')
```


 **Dataset 2**

 ***dataset Data Crime from 2010-2019 (data_cirme_2019):***
 
**about:**

This dataset reflects incidents of crime in the City of Los Angeles from 2010 - 2019. This data is transcribed from original crime reports that are typed on paper and therefore there may be some inaccuracies within the data. Some location fields with missing data are noted as (0°, 0°). Address fields are only provided to the nearest hundred block in order to maintain privacy. This data is as accurate as the data in the database. Please note questions or concerns in the comments.

Type: CSV File

Method: The data was gathered using the Download data manually method from (https://data.lacity.org/) source.


```
#2nd data gathering and loading method 
data_crime_2019=pd.read_csv('Crime_Data_from_2010_to_2019_20240118.csv')
```

## 2-Assess data

****Quality Issue 1: completeness => Missing data both datasets****

its completeness issue Quality issue there is a lot of missing values in both datasets :
data_crime_2019 dataset : there is missing values in Crm Cd 2 ,Crm Cd 3 ,Crm Cd 4 most of the columns are missing values and vict_sex,vict_descent, weapon_used_cd ,weapon_desc more than 100 K missing values
data_crime_2024 dataset : there is missing values incrm_cd_2 ,cross_street most of the columns are minssing values and weapon_used_cd , weapon_desc half of the columns are missing values.


****Quality Issue 2: Uniqueness   => duplicates values both datasets****

its Uniqueness issue in data Quality issues there is 230021 rows duplicte depand in dr_no column in data_crime_2019 dataset.


****Tidiness Issue 1: uppercase letters are used for column names in data_crime_2019 and lowercase letters are used for column names in data_crime_2024****
we have to change data_crime_2019 columns name to lower case letters and change columns to snake_case so we can index it easliy.


****Tidiness Issue 2:its Multiple variables are stored in one column****

there is muliple variables in the same cell in one columns crm cd desc the crime description and grand and many crimes


## 3-Cleaning data






