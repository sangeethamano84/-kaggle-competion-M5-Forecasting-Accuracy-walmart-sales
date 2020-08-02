# kaggle-competion_M5-Forecasting_Accuracy_walmart-sales

 ***Introduction***
Welcome to an extensive Exploratory Data Analysis for the 5th Makridakis forecasting competitions (M5)! 

***Some Background:*** the Makridakis competitions (or M-competitions), organised by forecasting expert Spyros Makridakis, aim to provide a better understanding and advancement of forecasting methodology by comparing the performance of different methods in solving a well-defined, real-world problem. The first M-competition was held in 1982. The forth competition (M4) ran in 2018 and featured “100,000 time series and 61 forecasting methods”. According to forecasting researcher and practitioner Rob Hyndman the M-competitions “have had an enormous influence on the field of forecasting. They focused attention on what models produced good forecasts, rather than on the mathematical properties of those models”. This empirical approach is very similar to Kaggle’s trade-mark way of having the best machine learning algorithms engage in intense competition on diverse datasets. M5 is the first M-competition to be held on Kaggle.

***The goal***: We have been challenged to predict sales data provided by the retail giant Walmart 28 days into the future. This competition will run in 2 tracks: In addition to forecasting the values themselves in the Forecasting competition, we are simultaneously tasked to estimate the uncertainty of our predictions in the Uncertainty Distribution competition. Both competitions will have the same 28 day forecast horizon.

***The data***: We are working with 42,840 hierarchical time series. The data were obtained in the 3 US states of California (CA), Texas (TX), and Wisconsin (WI). “Hierarchical” here means that data can be aggregated on different levels: item level, department level, product category level, and state level. The sales information reaches back from Jan 2011 to June 2016. In addition to the sales numbers, we are also given corresponding data on prices, promotions, and holidays. Note, that we have been warned that most of the time series contain zero values.

The data comprises 3049 individual products from 3 categories and 7 departments, sold in 10 stores in 3 states. The hierachical aggregation captures the combinations of these factors. For instance, we can create 1 time series for all sales, 3 time series for all sales per state, and so on. The largest category is sales of all individual 3049 products per 10 stores for 30490 time series.

***The training data comes in the shape of 3 separate files:***

***sales_train.csv:*** this is our main training data. It has 1 column for each of the 1941 days from 2011-01-29 and 2016-05-22; not including the validation period of 28 days until 2016-06-19. It also includes the IDs for item, department, category, store, and state. The number of rows is 30490 for all combinations of 30490 items and 10 stores.

***sell_prices.csv:*** the store and item IDs together with the sales price of the item as a weekly average.

***calendar.csv:*** dates together with related features like day-of-the week, month, year, and an 3 binary flags for whether the stores in each state allowed purchases with SNAP food stamps at this date (1) or not (0).

***CNN model with Time Distribution***
Convolutional Neural Network models, or CNNs for short, can be applied to time series forecasting.

There are many types of CNN models that can be used for each specific type of time series forecasting problem.

Let's discover how to develop a suite of CNN models for a range of standard time series forecasting problems.


* CNN models for univariate time series forecasting.
* CNN models for multivariate time series forecasting.
* CNN models for multi-step time series forecasting.

Although traditionally developed for two-dimensional image data, CNNs can be used to model univariate time series forecasting problems.

Univariate time series are datasets comprised of a single series of observations with a temporal ordering and a model is required to learn from the series of past observations to predict the next value in the sequence.

This section is divided into two parts; they are:

Data Preparation
CNN Model
Data Preparation
Before a univariate series can be modeled, it must be prepared.

The CNN model will learn a function that maps a sequence of past observations as input to an output observation. As such, the sequence of observations must be transformed into multiple examples from which the model can learn.

Consider a given univariate sequence:

[10, 20, 30, 40, 50, 60, 70, 80, 90]
1
[10, 20, 30, 40, 50, 60, 70, 80, 90]
We can divide the sequence into multiple input/output patterns called samples, where three time steps are used as input and one time step is used as output for the one-step prediction that is being learned.

X,				y
10, 20, 30		40
20, 30, 40		50
30, 40, 50		60
...
1
2
3
4
5
X,				y
10, 20, 30		40
20, 30, 40		50
30, 40, 50		60
...
The split_sequence() function below implements this behavior and will split a given univariate sequence into multiple samples where each sample has a specified number of time steps and the output is a single time step.

Running the example splits the univariate series into six samples where each sample has three input time steps and one output time step.

[10 20 30] 40
[20 30 40] 50
[30 40 50] 60
[40 50 60] 70
[50 60 70] 80
[60 70 80] 90
1
2
3
4
5
6
[10 20 30] 40
[20 30 40] 50
[30 40 50] 60
[40 50 60] 70
[50 60 70] 80
[60 70 80] 90
Now that we know how to prepare a univariate series for modeling, a CNN model that can learn the mapping of inputs to outputs.



***The Result***

The results of the trained CNN with different epochs. CNN starts to the learn the trend in 50 epochs. After 300 epochs, the predicted trend and real trend has exectly the same ups and downs.

***The metrics:***

The point forecast submission are being evaluated using the Root Mean Squared Scaled Error (RMSE),  metrics are computed for each time series and then averaged accross all time series including weights. The weights are proportional to the sales volume of the item, in dollars, to give more importance to high selling products. Note, that the weights are based on the last 28 days of the training data, and that those dates will be adjusted for the ultimate evaluation data, as confirmed by the organisers.
### The result is measured with RMSE. The score is 1.63440. 

