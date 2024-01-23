# Crime_data

about datasets





Columns in the two Datasets



![image](https://github.com/masiod/Fred_data/assets/61286495/cbaa9bf8-9ccb-416c-973a-ae250f985e63)


## Data Gathering

### Crime Data

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
about:

Crime Data from 2020 to Presenta;

Public Safety
*********Update 1/18/2024 - LAPD is facing issues with posting the Crime data, but we are taking immediate action to resolve the problem. We understand the importance of providing reliable and up-to-date information and are committed to delivering it.

As we work through the issues, we have temporarily reduced our updates from weekly to bi-weekly to ensure that we provide accurate information. Our team is actively working to identify and resolve these issues promptly.

We apologize for any inconvenience this may cause and appreciate your understanding. Rest assured, we are doing everything we can to fix the problem and get back to providing weekly updates as soon as possible. *********


This dataset reflects incidents of crime in the City of Los Angeles dating back to 2020. This data is transcribed from original crime reports that are typed on paper and therefore there may be some inaccuracies within the data. Some location fields with missing data are noted as (0°, 0°). Address fields are only provided to the nearest hundred block in order to maintain privacy. This data is as accurate as the data in the database. Please note questions or concerns in the comments.
Type: accessing APIs 

Method: Gather data by accessing APIs from source data.lacity.org (e.g., The data was gathered using the "API Access" method from https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8/data_preview source.)




`data=requests.get('https://data.lacity.org/resource/2nrs-mtv8.json').json()
`

data_crime_2020_2024 = pd.DataFrame.from_dict(data)```


 **Dataset 2**

 dataset Data Crime from 2010-2019 (data_cirme_2019):
 
about:

This dataset reflects incidents of crime in the City of Los Angeles from 2010 - 2019. This data is transcribed from original crime reports that are typed on paper and therefore there may be some inaccuracies within the data. Some location fields with missing data are noted as (0°, 0°). Address fields are only provided to the nearest hundred block in order to maintain privacy. This data is as accurate as the data in the database. Please note questions or concerns in the comments.






