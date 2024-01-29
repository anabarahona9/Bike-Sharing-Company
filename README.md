The following practical case was developed to obtain the Google Data Analytics Certificate. 

Context: 

The core business of this company is to offer bike share services in Chicago, Illinois. Customer segmentation is divided into two categories: annual members and casual members. 

The main purpose of this analysis is to obtain valuable information about each customer that will allow the company to make decisions to maximize the number of annual memberships. The case established a statement from financial analysts that annual members are more profitable for the company. However, this final statement could not be verified because the data does not contain that information.
This project uses a 6-stage methodology approach: 
1.	Ask: 
This initial stage involves understanding and defining the company’s objectives. In this case, they propose the following question: What is the difference between annual members and casual customers regarding bicycle usage? The aim is to derive recommendations for increasing annual memberships based on this question.
2.	Prepare: 
In this phase, ensuring the reliability, impartiality, credibility, integrity, and ethics of the data. The primary data source was downloaded from the official company website, which hosts public data. Personal information privacy is maintained throughout this process. 
3.	Process: 
The data was distributed monthly in CVS files. Excel was employed as the primary tool for data cleaning and transformation.
4.	Analyze: 
The data was imported from Excel into Power BI to consolidate into a single table. After this process, Dax was used to create new measures and perform various calculations. 
Variables available include: 
-	Ride ID: unique number of ID 
-	Rideable type: Classic, electric, Docked. 
-	Started at: Date and time of the ride. 
-	Ended at: Date and time of the ride.
-	Started station name.
-	Started station id. 
-	Ended station name.
-	Ended station id. 
-	Start latitude.
-	Start longitude. 
-	End latitude 
-	End longitude 
-	User type: member, casual


Measures and calculations: 
-	Total Rides 
-	Busiest Month 
-	Busiest Day 
-	Busiest Hour 
-	Rides per user type 
-	Rides per user and bike type 
-	Mean distance.
-	Mean Duration 
-	Rides per month 
-	Rides per day 
-	Rides per hour 

Python calculated the distance between two points based on their latitude and longitude coordinates. 

Code: 

pip install pandas geopy
from geopy.distance import geodesic
import pandas as pd

from google.colab import files  

from google.colab import drive
drive.mount('/content/drive')

path = '/content/drive/My Drive/month.csv'

data = pd.read_csv(path, delimiter=';', decimal=',')

columns_to_convert = ['start_lat', 'start_lng', 'end_lat', 'end_lng']

for column in columns_to_convert:
    data[column] = data[column].astype(str).str.replace(',', '.')

data[columns_to_convert] = data[columns_to_convert].astype(float)

data['Distancia_km'] = data.apply(lambda row: round(geodesic((row['start_lat'], row['start_lng']), (row['end_lat'], row['end_lng'])).kilometers, 1) if not any(pd.isnull(row)) else None, axis=1)

result_filename = '/content/drive/My Drive/resultado_distancias_month.xlsx'
data.to_excel(result_filename, index=False)


5.	Share: Power BI was chosen as the tool for presenting the data.

6.	Act: 

Findings:
- Users with memberships are more active, with 61.89% and a total of 2,527,7114 trips. In contrast, casual users account for 38.11% and a total of 1,556,553 trips.
- The average time for users with memberships is 12 minutes, while it is 22 minutes for casual users. This measure is directly related to the average distance traveled, as it reinforces the conclusion that casual users make longer trips, as they record an average distance of 2.40 kilometers compared to 2.18 kilometers for users with memberships.
- The month with the highest distance traveled was July, as well as the month with the most journeys for members. On the other hand, the month that recorded the highest distance traveled for casual users was August. Several factors could influence this measure, such as holidays, increased tourism, and climate, among others.
- The day with the highest number of trips was Saturday for casual users, for users with memberships it was Tuesday. 
- The hour with the highest number of trips for both customers was 5 pm.
- In terms of off-peak hours, there was less use at 3 am and 4 am for users with memberships and casual users, respectively.
- Regarding the use of bicycles, both users prefer classic bicycles over electric ones.

Recommendations:
- Seasonal promotion: Since the months with more rides are during the summer seasons, the company could consider offering promotions or discounts during this period to encourage casual users to get an annual subscription.
- Short-term membership: Another strategy is to introduce memberships with short periods like monthly memberships. To make sure about this option, conducting user surveys gives a deeper understanding of their needs.  
- Special packages: Create special packages or discounts for frequent users.
- Reward program for long-distance riders: Implementing a special membership that rewards users who ride longer distances, allowing them to accumulate points that can be redeemed for additional benefits. 


![image](https://github.com/anabarahona9/Bike-Sharing-Company/assets/144052609/e51e80dc-cf1b-4a1e-8c3e-1d65f10e64ce)

For a better visualization of the dashboard access to the following link 

http://surl.li/pxsqx




