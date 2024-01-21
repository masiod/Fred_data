# Crime_data

about datasets


This dataset reflects incidents of crime in the City of Los Angeles from 2010 - 2019. This data is transcribed from original crime reports that are typed on paper and therefore there may be some inaccuracies within the data. Some location fields with missing data are noted as (0°, 0°). Address fields are only provided to the nearest hundred block in order to maintain privacy. This data is as accurate as the data in the database. Please note questions or concerns in the comments.



Columns in this Dataset
Column Name	Description	                                                                                                          Type
DR_NO           Division of Records Number: Official file number made up of a 2 digit year, area ID, and 5 digits	                  Plain Text
Date Rptd	MM/DD/YYYY                          										          Date & Time
DATE OCC	MM/DD/YYYY														  Date & Time
TIME OCC	In 24 hour military time.												  Plain Text
AREA	        The LAPD has 21 Community Police Stations referred to as Geographic Areas within the department. These Geographic Areas are sequentially numbered from 1-21.
AREA NAME	The 21 Geographic Areas or Patrol Divisions are also given a name designation that references a landmark or the surrounding community that it is responsible
                for. For example 77th Street Division is located at the intersection of South Broadway and 77th Street, serving neighborhoods in South Los Angeles.
Rpt Dist No	A four-digit code that represents a sub-area within a Geographic Area. All crime records reference the "RD" that it occurred in for statistical comparisons.                  		Find LAPD Reporting Districts on the LA City GeoHub at http://geohub.lacity.org/datasets/c4f83909b81d4786aa8ba8a74a4b4db1_4
Part 1-2																  Number
Crm Cd		Indicates the crime committed. (Same as Crime Code 1)									  Plain Text
Crm Cd Desc	Defines the Crime Code provided.											  Plain Text
Mocodes		Modus Operandi: Activities associated with the suspect in commission of the crime.See attached PDF for list of MO Codes in numerical order. 				https://data.lacity.org/api/views/y8tr-7khq/files/3a967fbd-f210-4857-bc52-60230efe256c?download=true&filename=MO%20CODES%20(numerical%20order).pdf
Vict Age	Two character numeric													  Plain Text
Vict Sex	F - Female M - Male X - Unknown												  Plain Text
Vict Descent	Descent Code: A - Other Asian B - Black C - Chinese D - Cambodian F - Filipino G - Guamanian H - Hispanic/Latin/Mexican I - American Indian/Alaskan Native J - 		Japanese K - Korean L - Laotian O - Other P - Pacific Islander S - Samoan U - Hawaiian V - Vietnamese W - White X - Unknown Z - Asian Indian
Premis Cd	The type of structure, vehicle, or location where the crime took place
Premis Desc	Defines the Premise Code provided.											  Plain Text

Weapon Used Cd	The type of weapon used in the crime											  Plain Text
Weapon Desc	Defines the Weapon Used Code provided.											  Plain Text
Status		Status of the case. (IC is the default)											  Plain Text
Status Desc	Defines the Status Code provided.											  Plain Text
Crm Cd 1	Indicates the crime committed. Crime Code 1 is the primary and most serious one. Crime Code 2, 3, and 4 are respectively less serious offenses. Lower crime 		class numbers are more serious.
Crm Cd 2	May contain a code for an additional crime, less serious than Crime Code 1.						  Plain Text
Crm Cd 3	May contain a code for an additional crime, less serious than Crime Code 1.					          Plain Text
Crm Cd 4	May contain a code for an additional crime, less serious than Crime Code 1.	
LOCATION	Street address of crime incident rounded to the nearest hundred block to maintain anonymity.				  Plain Text
Cross Street	Cross Street of rounded Address												  Plain Text
LAT		Latitude														  float
LON		Longtitude														  float


