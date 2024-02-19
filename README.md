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

# Clean the data to solve the 4 issues corresponding to data quality and tidiness found in the assessing step. **Make sure you include justifications for your cleaning decisions.**
# 
# After the cleaning for each issue, please use **either** the visually or programatical method to validate the cleaning was succesful.
# 
# At this stage, you are also expected to remove variables that are unnecessary for your analysis and combine your datasets. Depending on your datasets, you may choose to perform variable combination and elimination before or after the cleaning stage. Your dataset must have **at least** 4 variables after combining the data.

Make copies of the datasets to ensure the raw dataframes 

``` #are not impacted
data_crime_2019_copy=data_crime_2019.copy()
data_crime_2024_copy=data_crime_2024.copy()

````

#drop columns thats contain 60% or above missing values and Mocodes column bc there is no data source about it 
```
data_crime_2019_copy.drop(columns=['Weapon Used Cd','Weapon Desc','Crm Cd 2','Crm Cd 3','Crm Cd 4','Cross Street','Mocodes'],inplace=True)
```
#change the missing values and - to be  X-unknowing 
```
data_crime_2019_copy['Vict Sex'] = data_crime_2019_copy['Vict Sex'].replace([np.nan, '-'], 'X')
data_crime_2019_copy['Vict Descent'] = data_crime_2019_copy['Vict Descent'].replace([np.nan,'-','unknowing'], 'UN')
```

#exlude the result in Premis Desc thats contain missing values 
```
data_crime_2019_copy=data_crime_2019_copy[data_crime_2019_copy['Premis Desc'].notnull()]
```
# ### Quality Issue 2:  Accuracy  issue




#### Apply the cleaning strategy
```
data_crime_2019_copy=data_crime_2019_copy[data_crime_2019_copy['Vict Age'] >= 1]
data_crime_2024_copy=data_crime_2024_copy[data_crime_2024_copy['vict_age'] >= 1]

```

#### Apply the cleaning strategy
We will change data_crime_2019 columns name from upper case into lower case by lambda func

```
data_crime_2019_copy.rename(columns=lambda x: x.lower(), inplace=True)
data_crime_2019_copy.columns = data_crime_2019_copy.columns.str.replace(' ', '_')
```

#### **Tidiness Issue 2: FILL IN**



```
def clean_and_transform(dataframe):
    # Perform the split and stack operation on 'crm_cd_desc'
    crm_cd_desc_split = dataframe['crm_cd_desc'].str.split(',', expand=True).stack().str.strip().reset_index(level=1, drop=True)
    crm_cd_desc_split.name = 'crime'  # Renaming the resulting Series for clarity

    # Join the expanded 'crm_cd_desc' with the original DataFrame based on the index,
    # which contains 'dr_no' and any other additional columns
    dataframe = dataframe.drop(columns=['crm_cd_desc']).join(crm_cd_desc_split).reset_index(drop=True)

    # Change the new 'crime' column from being the last one to be the tenth column from the left
    columns = list(dataframe.columns)
    # First, remove the 'crime' column name
    columns.remove('crime')
    # Then insert 'crime' at the desired position
    columns.insert(9, 'crime')
    # Now, reindex the DataFrame with the new columns order
    dataframe = dataframe.reindex(columns=columns)
    return dataframe

# Assuming data_crime_2019_copy and data_crime_2024_copy are your DataFrames
data_crime_2019_copy = clean_and_transform(data_crime_2019_copy)
data_crime_2024_copy = clean_and_transform(data_crime_2024_copy)

```

```
#Remove unnecessary variables and combine datasets
data_crime_2019_copy.drop(columns=['crm_cd_1','lat','lon'],inplace=True)
data_crime_2024_copy.drop(columns=['crm_cd_1','crm_cd_2','lat','lon','mocodes','weapon_used_cd','weapon_desc','cross_street','crm_cd_3'],inplace=True)
data_crime_2019_copy.rename(columns={'area_': 'area'}, inplace=True)
data_crime_2019_copy.rename(columns={'part_1-2': 'part_1_2'}, inplace=True)
```

Update your data store

```
rom sqlalchemy import create_engine





cleaned_data_crime=pd.concat([data_crime_2019_copy,data_crime_2024_copy])
cleaned_data_crime.head()





#optimize cleaned data

cleaned_data_crime=cleaned_data_crime.astype({'time_occ':'int8','area':'int8','rpt_dist_no':'int8','part_1_2':'int8','crm_cd':'int8','vict_age':'int8','premis_cd':'int8'})
cleaned_data_crime.info()





#row data 
second_copy_2019=data_crime_2019.copy()
second_copy_2024=data_crime_2020_2024.copy()


# ### Saving Row data




second_copy_2019.rename(columns=lambda x: x.lower(), inplace=True)
second_copy_2019.columns = second_copy_2019.columns.str.replace(' ', '_')
#row data 
row_data=pd.concat([second_copy_2019,second_copy_2024])
#saving_raw_data
row_data.to_csv('row_data.csv',index=False)
# Save DataFrame to SQLite database
engine = create_engine('sqlite:///datacrime.db')  # Replace 'database.db' with your desired SQLite database file name
row_data.to_sql('row_data_2019_2024', engine, index=False, if_exists='replace') 


# ### saving Clean Data crime




#saving cleaned_data_crime to csv file
cleaned_data_crime.to_csv('clean_data_crime.csv',index=False)
#saving cleaned_data_crime to sqlite table
cleaned_data_crime.to_sql('cleaned_data_crime_2019_2024',engine,index=False,if_exists='replace')


```





