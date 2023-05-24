# DeforestationwithS1
The repository contains the jupyter notebooks developed into the https://sepal.io/ platform for the thesis project "USING SENTINEL-1 TIME SERIES FOR MONITORING DEFORESTATION IN REGIONS WITH HIGH PRECIPITATION RATE" 

# Abstract

Despite nowadays there are many optical sensors out there, meteorological conditions in some places on the Earth makes very difficult to have access to images without clouds. Some of those places have unique ecosystems and landscape with natural forest that should be taken care of. SAR images has proven its capabilities for monitoring deforestation since the first sensors were deployed. Sentinel-1 allows to
have free access to SAR data with high temporal resolution. Therefore, this study explores the use of SAR data for monitoring deforestation in places where the precipitation rate is too high. A time-series approach is used as framework to detect forest disturbances; the work tests if performing a combination of the Sentinel-1 bands through a modified version from the RFDI gets better results than the original bands; two methods for detecting changes along the time focus on deforestation are compared. The results show that VH band is the best input with similar overall accuracy with the two methods, around 80%, the mRFDI showed acceptable results
but it does not prove any improvement on the deforestation events detected. It was concluded that with a workflow optimization, it can be used to overcome the optical images problem to monitor deforestation events.

*** https://run.unl.pt/handle/10362/150968 ***

# Workflow Explanation

The data comes from the **CAMERA DE LISBOA**, they have in their website values that monitor the envoronment in Lisbon city. They have almost 80 sensors across the city.

![image](https://user-images.githubusercontent.com/38009811/155448892-0ef72785-3505-460a-8128-0f76debf86a7.png)

The have a url endpoint where community can access to the almost real time data its updated each hour.

![image](https://user-images.githubusercontent.com/38009811/155449369-8db96a01-2ff5-4102-bce8-daa491a310a4.png)

Using the ETL module we storage information that we extract from that url in a table in a postgres database.

Once the data in in the table, there is a Trigger which runs a database function that performs a spatial intersection in order capture the Fragesia's name and station's address from two spatial tables in the same database.

![image](https://user-images.githubusercontent.com/38009811/155449985-908aa5b5-db96-4704-b44e-064c153309cb.png)

The ETL module runs automatically every day without user supervision, using the task scheduler tool in windows. The lisbon.bat file has the configuration to run the ETL module

Using a webpage users run the scripts in the backend in charge to create the pdf file with the information about the average values for Temprature, Noise and Humidity in Lisbon.
the first part has a map with idw interpolation values for the time period selected and the second part is a bar graph with the average for whole lisbon in each day during the time period selected.


