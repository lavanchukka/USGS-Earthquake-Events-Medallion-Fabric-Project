# USGS Earthquake Events - MS Fabric Medallion Project
![MSFabric](https://img.shields.io/badge/MS%20Fabric-Data%20Engineer-lightgreen)
![MSFabric](https://img.shields.io/badge/Medallion%20Architecture-grey)
![MSFabric](https://img.shields.io/badge/Data%20Factory-blue)
![MSFabric](https://img.shields.io/badge/Notebooks-grey)
![PySpark](https://img.shields.io/badge/PySpark-Big%20Data-orange?logo=apache-spark&style=flat-square)
![MSFabric](https://img.shields.io/badge/Lakehouse-blue)
![MSFabric](https://img.shields.io/badge/Data%20Warehouse-blue)
![MSFabric](https://img.shields.io/badge/Semantic%20model-grey)
![MSFabric](https://img.shields.io/badge/PowerBI-yellow)

### 📌<ins>Overview</ins>
This Project 
Ingest Earthquake events data from [usgs](https://earthquake.usgs.gov/)


### 📐<ins>Architecture</ins>

<img width="1739" height="437" alt="USGS Architecture" src="https://github.com/user-attachments/assets/b3e61d96-73b9-47f1-b187-2a7ccff78e52" />

## Implementation Steps
1)	Create a workspace Earthquakes USGS and add Lakehouse earthquakes_lh to the workspace.

### i) <ins>Bronze Layer</ins>

2)	Create a notebook earthquake_events_bronze and Fetch API data using Python requests library.
3)	Check the notebook `earthquake_events_bronze`for the details and code used for bronze layer processing.

### ii) <ins>Silver Layer</ins>
4)	Create a new notebook earthquake_events_silver.
5)	Transform the Json file in the /files path by extracting and renaming the key attributes for easy understanding of the data.
6)	Convert the time columns from UNIX (milliseconds) to time stamp format.
7)	Write the df in append mode and save as table earthquake_events_silver.
8)	Check the notebook `earthquake_events_silver` for the details and code used for silver layer processing.

### iii) <ins>Gold Layer</ins>
9)	Create a new environment to install reverse_geocoder library to make the geo data easier to understand.
10)	 Create a user defined function (udf) to get the latitude and longitude using reverse geocoder search.
11)	 Add country code(cc), significance classification using the udf.
12)	Finally save the df with write mode, append save as table earthquakes_events_gold.
13)	Check the notebook `earthquakes_events_gold` for code and details.


### iv) <ins>Semantic Model</ins>
14)	Open the default semantic model, if does not exists create a new semantic model, attach Lakehouse and select the earthquakes_events_gold table.
    
### v) <ins>PowerBI</ins>
15)	 Create a map visual and add the country code to the map, significance to the bubble size. Customize the colors based on significance.
16)	Add a date range filter and significance filter.
17)	Create a card visual for number of earthquake events.
18)	Save the report as earthquake_events_report.

### vi) <ins>Data Factory</ins>
19)	Create a pipeline and add notebooks bronze, silver and gold.
20)	Configure the base parameters dynamic start_date and end_date for all the 3 notebooks.
   	```
    Start_date: @formatDateTime(adddays(utcNow(), -1), 'yyyy-mm-dd')
   	End_date: @formatDateTime(utcNow(), 'yyyy-mm-dd')
22)	Run the pipeline earthquake_events_pl.


