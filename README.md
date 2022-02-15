# Drivers-Availabilty-Prediction
Trained a model to predict the number of hours individual drivers would be available on each day of the last week of the month given his information about the first 3 weeks.
GO-Jek Assignment  	
-Nishant Gupta  
      	
Data Preparation:
 
Ping timestamps have been converted into number of hours a driver was   available on a particular day. This was done by finding the difference between consecutive timestamps and calculating the hours by counting the differences which were equal to 15sec.    	
         	
Missing days information for a driver were added and 0 hr was assigned to such days.         	
         	
Duplicate rows were dropped in all the csv files provided.(Driver and Test both)
In driver files I found some drivers having same id and duplicate rows so I kept first .
Also in test file there are multiple dates for a particular driver again i kept first only there also.
                  	
In the test data it was found that there were a few drivers whose ping timestamps were not given, so decided to report for them the mean online hours of similar drivers, for which calculations were done  through K means clustering applied as follows:
 Built clusters using Age, Number of Kids and Gender given in the drivers.csv and found that three clusters are formed. 

Age -> Min Max Normalize 
Number of KIds -> Min Max Normalised 
Gender -> One hot encoded 

Driver weekend/ weekday variable could also be taken and frequency of his arrival in a day could also be a role player in K means Clustering .

 Training Single ARIMA model might go on a toss. Why?

Driver behavior not consistent across weeks so can't apply directly stats based methods .
In order to build arima model we have to find out the average of each cluster and then forecast or else not possible. 

Training XGBoost model independently gave us lots of freedom to explicitly create features and also rolling averages , average of week along with other information such as gender, age, cluster_id.

Trying rolling mean 
        	
Methodology:
Created temporal features like mean online hours of each day type i.e Mon, Tues, Wed, etc, along with median and standard deviation. Then week and weekend averages, median and standard deviation were also taken into account. These values were updated with each passing day starting from 1st June to 20th June.

Also, the online_hours of last day have been added to predict the online_hours of current day as it is a general trend that a person working a lot on one day will tend to do reduce the duty hours the next day.


Data Modelling: 
XGBoost was trained to learn these features and predict the online hours of       	drivers for 22nd June to 28th June.
Once the model was trained, online hours were predicted for 22nd June and then again average features were generated for 22nd June to predict for 23rd June and so on upto 28th June.
Scope for improvement:
Rolling mean at different levels like varying window size (rolling mean across days,weeks,months if data is more)  can be taken to see if it improves the predictions.
As ARIMA is also all about moving averages at different lags so it will be fruitful  if we also have different window rolling averages .        	
Parameter Tuning of XGBoost can also help. 
Even more EDA on data will help find better patterns and feature Engineering Ideas.
Provided more Time and RAM , these techniques as well can be implemented to get even better results. 
RMSE I am getting is around 4.7 for half data points probably will be able to report by tomorrow 
	
 


