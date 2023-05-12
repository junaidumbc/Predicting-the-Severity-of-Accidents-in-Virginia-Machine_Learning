# Predicting-the-Severity-of-Accidents Crashes-in-Virginia(Machine Learning)
![image](https://raw.githubusercontent.com/junaidumbc/Predicting-the-Severity-of-Accidents-in-Virginia-Machine_Learning/main/Car_img.png)
## Business Goal:
To find any columns that relate to the crash severity, and build predictive models based on said variables.


## Introduction
Our project researched the accident patterns in Virginia, to predict the severity of these accidents. Being able to predict the more severe accidents early are crucial to minimizing lethal or close to lethal accidents. Overall, with this information people can take more measures when driving to avoid high crash severity accidents. For example, our data contains information like distracted drivers, young drivers, old drivers, etc. If a certain archetype of driver is falling under more severe accidents, then this group should be informed that they are at a risk. However, this information is not only crucial to the people it is important to the Virginia government too. The patterns found in our data can illustrate problems with a certain street or intersection. If more severe accidents are happening at a certain intersection, the Virginia government can take measures to keep their drivers safer. Whether it be increasing visibility conditions or adding more stop lights, the Virginia government can always take more measures to keep its drivers safe. Being able to understand accidents and predict the severity of them are important in creating safer roads. 

## Data
Our dataset was from the Virginia Roads government website. Unfortunately, the first dataset we planed to use was removed, but an extremely identical dataset was uploaded. Since most of the column names were different from our previous dataset, we had to redo most of our EDA. This new dataset was from 2015-2022 so it’s constantly being updated and monitored by the Virginia government. We downloaded the data when it was last updated April 28th, 2022. The dataset contains about 892, 211 values with 73 attributes. Compared to our last dataset, this was an increase of around 30 attributes. These attributes are a variety of information such as fatalities, crash date, road location, collision type, weather, drowsy driver, young driver, etc. Extremely detailed data like this made it very easy for us to determine which features were important and which features were not important.  

## Data Cleaning and Pre processing
In terms of cleaning the data we dropped any features with nan-values (also since most were not good features for modeling). After that we went through the database and read the column descriptions and dropped any we didn’t need. Columns like “X”, “Y”, and “OBJECTID” are some examples of the columns we removed due to them not being good modeling features. Columns like “PERSONS_INJURED” and “BELTED_UNBELTED” were already integers and had limited values (Yes or No) so we deemed these good features.  

## Exploratory Data Analysis
* Looking at some of the features we kept we found some interesting patterns. For “CRASH_SEVERITY”, we found that most of the distribution of accidents was Property Damage Only (66.4%), then Visible Injury (19.6%), Nonvisible Injury (8.3%), Severe Injury (5.0%), and Fatal Injury (0.6%). 
* So, most of the accidents are centered around property damage which makes sense. According to the VDOT Crash Data Manual, a property damage crash is reported when “the crash resulted in damage of at least $1,500 to the motor vehicle or other property” (Virginia Department of Transportation 2017). 
* Considering that the other types require an injury, most accidents are occurring without any injuries. Intersection accidents was another interesting variable, due to how split it was across all the data. 
* About 41% of all the accidents happened at an intersection, leaving the other 59% to be not an intersection. We’re not going to go over all the features, but we were left with around 38 attributes for the modeling.  
* Before we touched any One Hot Encoding and modeling, we decided to create a correlation matrix between all the variables. The results of this matrix surprised us. 
* “CRASH_SEVERITY_NEW”, our “CRASH_SEVERITY” column recoded into an integer was showing a high correlation with the PERSONS_INJURED.  PERSONS_INJURED contains the amount of people injured in an accident. 
* On paper, it sounds like a correlation would make sense since Property Damage accidents would have a lower amount of people injured compared to a Severe Injury accident. However, we wanted to see if this variable had an impact on the modeling procedure. 
* For reencoding columns, we had to reencode “DAYOFWEEK”, “MONTH”, and “PLAN_DISTRICT” to be integers. After that we removed the “CRASH_SEVERITY” column since we added “CRASH_SEVERITY_NEW” as a column. For modeling, we wanted to try two types of modeling to measure the importance of the “PERSONS_INJURED” in relation to the crash severity. For data preparation, in both scenarios we removed “CRASH_SEVERITY_DT”, “TIME”, “DATE” since they are not good modeling features. In both scenarios, we also removed 
“CRASH_SEVERITY_NEW” from the X labels since it is our target variable (belongs to the y labels).  The only difference between these modeling scenarios is the involvement of the PERSONS_INJURED column since we kept the model parameters the same. We used a split of about 70% training data and 30% test data, along with a random state number to keep consistent results.  
 
## Modelling
For the models we used Logistic Regression, Decision Tree, and Random Forest. 
* The results we found were reflective of our original thinking about the importance of the PERSONS_INJURED column. Starting out with the models that lack the PERSONS_INJURED column, the results were poor. Logistic Regression gave an accuracy of about 66%, Decision Tree gave a measly accuracy of about 39%, and Random Forest gave us an accuracy of about 66%. 

* However, we are not alarmed by these results since we expected this to happen based on the correlation matrix. Our thinking is correct if the accuracy of all these models should rise when including the PERSONS_INJURED column. When including the PERSONS_INJURED column, the accuracies are much better. Logistic Regression gave us an accuracy about 86%, Decision Tree gave us an accuracy of about 81%, and Random Forest gave us an accuracy of about 87%. Looking at the difference in the modeling scenarios that contain and do not contain the PERSONS_INJURED column, this makes sense. 

* We expected the accuracy to raise tremendously due to how much PERSONS_INJURED related to the crash severity in the correlation matrix. These accuracies including the PERSONS_INJURED column is great, but we wanted to see if we could get an accuracy of at least 90% so we looked towards hyperparameter tuning. We tried hyperparameter tuning for all 3 of the modeling types we used, but the accuracy did not increase.  For each method, the accuracy of the hyperparameter tuned models were extremely close to the non-hyperparameter tuned models.  
 
 ## Results
 ![image](https://raw.githubusercontent.com/junaidumbc/Predicting-the-Severity-of-Accidents-in-Virginia-Machine_Learning/main/Results123.png)
 ## Conclusion
In conclusion, using this Virginia Crash dataset we found that the PERSONS_INJURED column has a large correlation with the Crash Severity column. Looking at the Crash Severity definitions on the Virginia Roads website allows us to get the entire picture of our results. “Crash Severity is coded using the KABCO scale,… based on the most severe injury to any person involved in the crash” (Virginia Department of Transportation 2017). Thinking about it, the crashes with the most severe injuries are likely to have a higher number of people injured compared to other crashes. Like we mentioned earlier, Property Damage Only was the highest type of crash severity. When we look at a distribution of PERSONS_INJURED, 66.8% of the accidents had 0 people injured. Comparing the 66.8% of accidents that had 0 people injured and the 66.4% of accidents that were reported as Property Damage Only, proves the relationship between the two. When we started this project, we had an idea that the crash severity column from the dataset was made up of a multitude of columns. However, from the research we’ve done on the crash severity column shows us that the PERSONS_INJURED column has the most influence compared to the other columns. Although using the amount of people injured to predict the type of crash is impossible, we still got a great insight about the entire dataset. If we had more time, perhaps we could find a dataset that has the crash severity column based on more factors such as fatalities instead of just injuries.   
 
