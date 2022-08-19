# Daegu-Apartment-Price-Prediction

Created by: Jeffrey Junior Tedjasulaksana

### **Businees Problem Understanding**

**Context**

[Daegu](https://en.wikipedia.org/wiki/Daegu) is South Korea's third-largest urban agglomeration after Seoul and Busan, the third-largest official metropolitan area in the country with over 2.5 million residents and the second-largest city in the Yeongnam region in the southeastern Korean Peninsula after Busan.

Daegu was Korea's economic hub from the 1960s to the 1980s, and it was particularly well-known for its electronics industry. Daegu's humid subtropical climate is ideal for growing high-quality apples, hence the nickname "Apple City." Daegu is also referred to as "Textile City." Textiles were once the city's mainstay industry. Daegu is currently focusing on fostering fashion and high-tech industries.      
        
Because of Daegu's rapid development, the demand for apartment housing has increased. Daegu city [reached 240,000 apartments by 2021](https://www.statista.com/statistics/1303257/south-korea-apartments-in-daegu-by-number-of-stories/#statisticContainer). 

Because Korean citizens are so busy, they do not have enough time to meet with potential buyers, many apartment unit owners entrust property agents with sales transactions. The significance of determining property values can help to simplify property buying and selling transactions. According to [Statista](https://www.statista.com/statistics/1048638/south-korea-number-of-unsold-housings-daegu/) data, the number of properties in Daegu City that have not been sold by 2021 is 2000 property.

According to the [ruhl and ruhl home web](https://www.ruhlhomes.com/selling-a-home/importance-to-price-right/#:~:text=Pricing%20your%20home%20at%20fair,sell%20at%20a%20lower%20price), pricing your property at a reasonable market value will attract potential buyers. The longer a property sits on the market, the lower its perceived value and the likelihood that it will be sold at a lower price. As a result, tools in an application are required to determine the estimated price of a property for property agent.

**Problem Statement**

As the population in Daegu City increases, there will also be an increase in the need for housing, especially apartments in Daegu City. So that property agents must streamline the costs incurred to get maximum revenue.

Based on research conducted by [Onur Demirci from the University of Westminster](https://westminsterresearch.westminster.ac.uk/download/2dae110e45564422696a65c873989232ffbea0a3e58d318a552b963485e4452f/570796/Research%20Paper%20-%20Traditional%20and%20Mass%20%28Advanced%29%20Valuation%20Methods.pdf), valuation is a process that involves defining the fair market. When valuing a group of properties, it is widely acknowledged that traditional valuation has numerous limitations. value of an entity Traditional valuation methods have significant limitations in terms of accuracy, consistency, and speed. 

**Goals**

Based on research conducted by [Onur Demirci](https://westminsterresearch.westminster.ac.uk/download/2dae110e45564422696a65c873989232ffbea0a3e58d318a552b963485e4452f/570796/Research%20Paper%20-%20Traditional%20and%20Mass%20%28Advanced%29%20Valuation%20Methods.pdf), the weakness of Traditional Valuation can be overcome by conducting advance valuation with a regression machine learning model. With an increasing volume of transactions and a changing real estate market, advanced valuation (regression machine learning model) is becoming more applicable.

So that tools in the form of machine learning models that have been made will be used when apartment unit owners want to sell apartment units through property agents, then property agents will enter apartment unit specifications that issue price predictions of apartment units to be marketed. And I as a machine learning engineer from a property agent company will create and maintain the tools that have been created.

**Analytic Approach**

We must analyze features such as the type of hallway, travel time to the subway, facilities in and around the apartment, and the year of construction, all of which may affect the apartment's sale price.

We can create a regression model based on the analysis results to to determine the price of the apartment unit based on the specifications owned.

**Metric Evaluation**

To test the error rate of an already created model, we can use MAE and MAPE.

MAE is the average value of absolute error because its characteristics that are less sensitive to outliers so MAE is better than MSE. 

![MAE](https://github.com/JeffreyJuinior/Daegu-Apartment-Price-Prediction/blob/main/Images/MAE.PNG?raw=true)

MAPE is the average of the recidual absolute results in the form of percentages, just like MAE, MAPE has characteristics that are less sensitive to outliers because the target contains an outlier. Suitable for a very large target value range, the model is better at predicting the selling price of the apartment.

![MAPE](https://github.com/JeffreyJuinior/Daegu-Apartment-Price-Prediction/blob/main/Images/MAPE.PNG?raw=true)

We also use R-Square in model evaluation where R-Square explains how much variation in Y value can be explained by the model, The more the R-Squared value approaches 1, the better the model is at predicting apartment prices.

![R2](https://github.com/JeffreyJuinior/Daegu-Apartment-Price-Prediction/blob/main/Images/r2.png?raw=true)

### **Data Understanding**

- Dataset obtained from the official website of the Korean government, namely [data.go.kr](https://www.data.go.kr/) from 2007 to 2017
- Each row represents information related to the apartment

**Attributes Information**

|**Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| HallwayType | Object | Types of apartment hallways |
| TimeToSubway | Object | Measure time takes from apartment to subway station  |
| Subway Station | Object | Name of subway station nearby apartment |
| N_FacilitiesNearBy(ETC) | Float | number of other facilities such as hotels and special schools |
| N_FacilitiesNearBy(PublicOffice) | Float | Number of public offices nearby apartment |
| N_SchoolNearBy(University) | Float | Number of universities nearby apartment |
| N_Parkinglot(Basement) | Float | Count number of parking spaces on basement |
| YearBuilt | Integer | The year when the apartment was created |
| N_FacilitiesInApt | Integer | Number of facilities for residents like swimming pool, gym, play ground |
| Size(sqf) | Integer | Size of apartment in square feet |
| SalePrice | Integer | Apartment price in US dollar |

### **Data Preprocessing**

**Feature Engineering**

Feature engineering is the process of extracting features from a dataset and assisting the predictive model in better representing underlying problems, which improves the model's accuracy in predicting data.

1. Numeric:

- Feature Scalling : Standard Scaler

    **Feature scaling** is used to change the entire feature to have the same range, for distance-based algorithms this can improve accuracy because any difference in order of magnitude in our different feature values will cause the feature with the widest range to dominate the metric, thus taking most of the importance of the model.

    Although the scalling feature is more suitable for distance-based algorithms but it can also be used on tree-based algorithms and does not reduce the accuracy of the model Significantly. In our case, we use feature scaling for distance and tree-based algorithms to make programming more efficient.

    **Standard Scaler** work with akes our data and makes it follow a Normal distribution, usually of mean 0 and standard deviation 1.

- Power Transform : Yeo-johnson

    Power transform will make features more normally distributed and reduce skew, it will work with calculating the log or square root of the features. we use yeo-johnson because it can shout features that are negative or 0, in our case it is like there is an apartment that does not have a parking lot. While the box-cox method requires features to have a value of more than 0.    

2. Categoric

    Because Machine Learning models cannot handle text data directly, Feature Encoding converts categorical features to numeric values.

- Ordinal Encoding

    Ordinal encoding converts categorical features to numeric features with weights or ratings. For example, in the time to subway feature, the shorter the time required to get to the subway, the greater the weight.

- One Hot Encoding

    one hot encoding is a type of encoding that works by adding the number of columns according to the number of unique values in the feature then giving a value of 1 in the column with that category and the rest of the columns are worth 0. so that the value on the feature has the same position (no one has a higher weight in the other).
    
### **Evaluation Matrix Comparison Model after Tuning**



