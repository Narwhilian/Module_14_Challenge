# Machine Learning Trading Bot

This notebook uses SKlearn to optimize a machine learning model to predict investment performance using dual simple moving averages.

---

## Technologies

This project uses the Python Programming language in a Jupyter Notebook as well as the following libraries
    
    - pandas
    - numpy
    - pathlib
    - hvplot
    - DateOffset
    - sklearn
      - classifcation_report
      - standard scaler
      - svm


---

## Installation Guide

To install you will want to pull the entire Trading_Bot folder from github including its subfolder
    
    * Subfolder
        * Resources (the folder containing the csv data of the stock performance as well as the png files used in the conclusion section)
        * machine_learning_trading_bot.ipynb (the jupyter notebook itself)
    * ReadMe (This file)


---

## How it works

1) First the user will open the machine_learning_trading_bot.ipynb notebook in the Trading_Bot folder (using jupyter labs)
2) Then the user will simply run each cell in the notebook in order to get its output

    i) The app will read the startup data into a dataframe and then clean the data, calculate daily performance, and finally create a short and long sma to use as testing features
    
    
    ii) Then it will break up the data into features and targets and split the data into training and testing data. Finally scaling the features to eliminate bias

    
    iii) Then it will create, test, and save its first itteration
        - This step is repeated using different SMAs and training windows to fine tune the model
    
    
    iv) It will then go on to create another model using LogisticRegression to compare how it performs to the original SVC model
    
    
    v) Finally we will use the output from the various models to identify the best trading model.
    





---

## Usage

Overall it should be a very simple application to use, all you need to do is open the machine_learning_trading_bot.ipynb notebook in the Trading_Bot folder and run each cell in order using the jupyter labs interface.


---

## Conclusion / Evaluation Report

We altered the baseline model a number of times to see how different factors would affect model performance. 

The original baseline model uses a 4 and 100 day SMA and a 3 month training period. 
![Baseline Returns](https://user-images.githubusercontent.com/84096312/132141335-6b2e425d-d79d-4725-8909-0ce92c2c8bd4.png)

We then tried a 4 month training period using the same SMAs 
![return 4 month](https://user-images.githubusercontent.com/84096312/132141352-6cb922ef-20b7-4690-94dc-9b1001f50a85.png)

and a 5 month training period using the same SMAs
![returns 5 month training](https://user-images.githubusercontent.com/84096312/132141358-cbe1cf54-8561-4ff2-a15c-3a68dbf4cc65.png)

We then altered the long SMA from 100 down to 25
![returns 4v25](https://user-images.githubusercontent.com/84096312/132141379-ae6b0805-2a42-43ad-b112-eb12a7e04969.png)

then increased the short sma up to 31 and the long sma up to 155
![returns 31v155](https://user-images.githubusercontent.com/84096312/132141391-0142da69-1f35-4493-8446-9e2bf3294dc6.png)

finally we increased the long sma again up to 223 while keeping the short sma at 31
![returns 31v223](https://user-images.githubusercontent.com/84096312/132141403-2aa05496-e020-4417-b3ad-a37fb779658f.png)

Question: What impact resulted from increasing or decreasing the training window?
Answer: Increasing the training window brought the results more in line with the actual returns which in this case was a negative effect since our original model out performed the actual returns.

Question: What impact resulted from increasing or decreasing either or both of the SMA windows?
Answer: Changing the SMA windows dramatically changed the strategy results. Though it made them difficult to compare to one another exactly in overall cumulative return since different window sizes affected the size of the training and testing data so the results were not run in the exact same conditions. In the future I will have to make accomodations for this so it is easier to tune the strategy

Question: Did this new model (Logistic Regression) perform better or worse than the provided baseline model? Did this new model perform better or worse than your tuned trading algorithm?
Answer: It performed better for the first portion of the test but then dramatically underperformed at the end of the model making its overall performance worse.

Interestingly the version with a shortened longer SMA (4v25 model) performed much more poorly than I had anticipated, I had assumed having more reactive moving averages would give the model a better ability to predict performance. I believe the issue with the two short averages was that there was too much "noise" making it difficult to predict performance, especially in comparison to the longer SMA versions. The ones with the long models (31v155) under performed the ticker it was tracking up until the the last final run up in the market. I believe this happened primarily because the short positions were difficult to execute with such slow moving averages especially in a bullish market. I had the opposite problem with my LogisiticRegression model 
![Logistic Regression returns](https://user-images.githubusercontent.com/84096312/132141583-41d4a5d1-b9b9-4ef6-bdee-a1a705e23ebf.png)
where the strategy over performed the actual returns up until the last run up where it took a position against the run up and lost a large portion of its gains. 

Ideally I will be able to find a way to combine the two models and use the LogisticRegression model pre 2020 and the 31v155 svc model after 2020 with a ML parameter to switch between the two strategies.

---

## Contributors

Colin Benjamin

Linkedin: [Colin Benjamin](https://www.linkedin.com/in/colinbenjamin/)
    
email: cbenjamin33@gmail.com

---

## License

MIT
