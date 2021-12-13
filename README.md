# Predicting Sales Growth with ARIMA in Python

## **Objectives:**

  Use the ARIMA model to forcast sales for any business.
  
## **Method:**

  This product uses the ARIMA model to predict future sales. ARIMA stands for Autoregressive Integrated Moving Average and it used greatly for time series forcasting.
  There are 3 parameters for this model which are p: order for the autoregressive term, q: order for the Move Average term, and d: the number of differencing required
  to make the data stationary. Below is the equation the ARIMA model uses.
  
![image](https://user-images.githubusercontent.com/81201081/143964538-7a10a3d2-b500-4519-a414-c550f730f5b4.png)

## **Software Requirements: You will need to have these to work with the code.**

  Python: To install click the following link https://www.python.org/downloads/
  Jupyter: To install click the following link https://jupyter.org/
  If you need more help, please see the resources below.
  
  
 
## **Steps for Python Code: You are able to copy and paste the code into your own Jupyter Notebook.**

  ### **Step 1:** Import all libraries needed for the code.
  
  ### **Step 2:** Install ARIMA package

## **O - Obtaining our data**

  - For my data, I got it from a companies database. You will need to obtain the data from your business in a way that it can be exported in a Excel or CSV file. 
  - My data is included above name= "DATASET"

  ### **Step 3:** Load the data and split it into a Train and Test set. 
   - The data should have two varaibles: Date and Sales (Be sure the title of the columns are changed to match these exactly)
   - You can use any amount of lines of data but the data used here has 175,190 lines that run from year 2016-2021.
   - For the data, you will need to delete or fix lines of data where there are "0" values, duplicate values, and/or blank values.
   - The data needs to be saved as a CSV file and found in the place where your python code is looking which is the first line of code in step 3.
   - You can save the CSV file as "DATASET"
   - You need to split the data into a train set and a test set. I split my data into 2016-2020 for the train set and 2021 for the test set.
      The value 133316 is the line number in the CSV file that splits these. So choose the point in your file where you would like to divide.
     
        
  ![image](https://user-images.githubusercontent.com/81201081/143965759-e8fac98d-09f9-441f-ac3d-e9de267b82e8.png)

 
## **S - Scrubbing/Cleaning our data**

  Your data should not have any missing values, duplicate values, and/or "0" values from the last step.
  
### **Step 4:** Make sure the Date and Sales columns are the correct type. 
   - The Date should be changed to datetime64[ns] and the Sales variable should be changed to a int.
   - Then run the info on both sets of data to make sure the TRAIN and TEST sets say the correct Dtypes.
    
  ![image](https://user-images.githubusercontent.com/81201081/143968814-8886217b-d57d-40bb-8505-9d3ac399ef40.png)

   
 ### **Step 5:** Create Index for both TRAIN and TEST set. 
  
  ### **Step 6:** Group the Data. 

## **E - Exploring/Visualizing our data - THis will allow us to find patterns and trends**

  ### **Step 7:** Visualize the data: You will be able to see the trends and patterns of the TRAIN set.
  
  
  ![image](https://user-images.githubusercontent.com/81201081/143968777-59fefcfd-0aa8-4994-93b1-11ca50a19371.png)

  
  ### **Step 8:** Visualize the seasonal decompose graphs. 
  These will show you the data, the trend, the seasonality, and the residuals. This will be important for making sure 
  the data is stationary for the ARIMA model so note if you see you a trend or patterns. A trend is present when there is a increase or decrease in the value over time. 
  Seasonality is present when a value repeats over the same time interval. For my data, I can see a trend as it continuely increases and a season pattern
  as it has similar spikes around the same month for each year.
  
  ![image](https://user-images.githubusercontent.com/81201081/143969056-80e42a87-a3b3-4b69-8ea2-6f4031e72d8c.png)

  
### **Step 9: (OPTIONAL):** I created a data set that totals the months by year. This allows you to compare the months to see more of a pattern per month. We can see in my graph that were the sales increases in February, June and September.
    
  You will need to create a seperate CSV file with sales totaled by month and save it as 'monthly'. The column titles should be the years and the row titles should
  be the months like shown below:
    
    
![image](https://user-images.githubusercontent.com/81201081/143968999-49faf024-d843-402d-a985-05b4f7620ec8.png)
    

![image](https://user-images.githubusercontent.com/81201081/143969028-da6b573e-a25c-4527-819c-e3366ec22406.png)


  -The data for this is included above named "monthly".
  
  -If you want to visualize your data further, there is a option to visualize your data in Tableau below.
  
## **M - Modeling our data**

  Like mentioned before, we are going to use the ARIMA to forcast sales. For this model, we need to the data to be stationary. Stationary means that the properties of the
  time series does not change over time. This is important when fitting a ARIMA model. First, it is important to check if the data is stationary and to do this we can use the 
  Dickey Fuller test. From the seasonal decompose graphs, we can make a educated guess by visualizing if there is patterns, trends, or seasonality by looking at these graphs, 
  but using this test can verfiy these conclusions. To make the data stationary, we can difference the series. 

 ### **Step 10:** Test for stationary using the Dickey Fuller Test.
   - This will give you an output for the p-value.
   - If the p-value is less than 0.05 then your data is stationary, if the p-value is greater than 0.05 then your data is non-stationary
   - **If your data is stationary you need to skip Step 11 and if your data is not stationary then please move to step 11.**
      
      
      ![image](https://user-images.githubusercontent.com/81201081/143970663-21719aa9-b554-432e-bfb1-d49d0c9e0fa1.png)
      

   - My p-value was 0.98, therefore my data is not stationary so I need to move onto Step 11.
    
   ### **Step 11:** Make data stationary by rolled and differenced data
   - You will run these cells in order to make your data stationary. You can tell by the graphs that the time series has removed the trends.
   - You then need to verify that the data is stationary by running the ADFuller test again to make sure it is less than 0.05.
      
      
      ![image](https://user-images.githubusercontent.com/81201081/143971076-77427c67-43fb-4ee5-b376-1d82a2e01d8d.png)
      

![image](https://user-images.githubusercontent.com/81201081/143971107-20e1585d-b48f-4073-bfdb-3febd5d93f49.png)


 ### **Step 12:** Run the auto ARIMA model
   - This will output the best model parameters. The best model comes from the output with the lowest AIC value.
   - **If you had to complete Step 11, you will need to move onto Step 13. If you skipped step 11, you can move to Step 14.**
   - These paramters will be used in step 13 for the SARIMA model.
    
 ![image](https://user-images.githubusercontent.com/81201081/143971333-cd9f286d-aefb-4fac-ba70-0f49fabaa4d4.png)

 ### **Step 13:** We will use this output and place these values within the SARIMA model. This model is the Seasonal ARIMA.
   This will be the second model to fit.
  
 ![image](https://user-images.githubusercontent.com/81201081/143971631-6b766c6a-72fc-4245-bc60-ba845fe080a7.png)

    
## **N - Interpreting our data**

 ### **Step 14:** This will be a summary of the auto ARIMA. You will want to look at the p-values to see if they are less than 0.05 which means that those coef are significant.
    
 ![image](https://user-images.githubusercontent.com/81201081/143972181-43945677-7fe4-40f0-8fb8-cf736d9b65fe.png)

 ### **Step 15:** This is the summary of the SARIMAX model. (only for those who needed to make their data stationary)

 ![image](https://user-images.githubusercontent.com/81201081/143972241-4779b198-6321-4e91-b84e-4ff91d4dd610.png)

### **Step 16:** You can visualize the ARIMA diagnostic plots.
  - Top Left: You want the residual errors to fluctuate around zero.
  - Top Right: You want a density plot of a normal distributtion and a mean of 0.
  - Bottom Left: All dots should be around the red line. If there are dots not on the red line, this means the distribution is skewed.
  - Bottom Right: This is a ACF plot. This shows if the residual error is autocorrelated.
    
  - My plots are below which would indicate that my model seems to be a good fit.
    
![image](https://user-images.githubusercontent.com/81201081/143972825-deff3b1d-a3ae-4b34-9378-859bc89ca982.png)

###  **Step 17:** Visualize the predicted forcast from the ARIMA
  - This will allow you to compare how well the model predicted the values for the future based on your TEST set. 
  - My prediction is below:
    
![image](https://user-images.githubusercontent.com/81201081/143973281-b78113b5-b5be-413f-8feb-d649506811ea.png)

 ### **Step 18:** Plotting predictions and actual values 
   - This allows you look closer at how accuarte the model is predicting. As you can see below, my model did a fairly good job as they are very close to the actual values.
    
 ![image](https://user-images.githubusercontent.com/81201081/143973416-d08f0bb8-b3a0-4580-a9b1-d40d7e128064.png)

 ### **Step 19:** Forecast for the next 3 years
   - You are able to change how many years you want to predict by changing the 3 to how ever many years you want to predict in the code.
    
 ![image](https://user-images.githubusercontent.com/81201081/143973574-10420d52-7c83-4dc0-b49c-3ec06bc1fc92.png)

###  **Step 20:** Find the error value (MAPE - Mean Absolute Percentage Error)
   - This value will tell you the percentage error. Therefore, the accuray of your model is 1 - error%.
   - The formula is below but you can run it in Python.
   - My error percentage was 0.0511 meaning my model is 95% accurate for predicting sales.
    
 ![image](https://user-images.githubusercontent.com/81201081/143973878-d8d79ca4-a0c3-4783-a5d4-0c27485bfb44.png)

 ![image](https://user-images.githubusercontent.com/81201081/143974014-e07340d9-e677-4dd7-8f13-2b5d2f77af24.png)


## **Conclusions:**
  The ARIMA models forcasted sales at a 95% accuracy level. This can be used for any sales data of your choice.
  
## **Optional Data Exploration in Tableau:**
   - **WARNING: ANY DATA YOU PUT INTO TABLEAU PUBLIC CAN BE ACCESSED BY ANYONE. PLEASE DO NOT ENTER ANY PRIVACY INFORMATION!!**
   - You will need to download Tableau Public and create an account. The link is here: https://public.tableau.com/en-us/s/
   - You can access my data exploration in Tableau here: https://public.tableau.com/app/profile/melissa.lahoud/viz/Capstone-DataExploration-Final/Dashboard1?publish=yes
   - If you need help creating your own, there is a great video to help: https://www.youtube.com/watch?v=Aql27yGqHkE

## **Resources & Additional Help:**
   - Install Python/Jupyter:
      https://www.youtube.com/watch?v=Vn_6kZjInfE
   - Python/ARIMA model:
      https://coderzcolumn.com/tutorials/data-science/how-to-remove-trend-and-seasonality-from-time-series-data-using-python-pandas#7
      https://www.machinelearningplus.com/time-series/arima-model-time-series-forecasting-python/#2introductiontoarimamodels
      https://www.geeksforgeeks.org/python-arima-model-for-time-series-forecasting/
      https://medium.com/analytics-vidhya/predicting-sales-time-series-analysis-forecasting-with-python-b81d3e8ff03f
   - Install Tableau Public: https://www.youtube.com/watch?v=hsEwSmdv0Y8
   - Tableau: 
      https://www.youtube.com/watch?v=Aql27yGqHkE
   - Security Laws: https://iclg.com/practice-areas/data-protection-laws-and-regulations/usa

