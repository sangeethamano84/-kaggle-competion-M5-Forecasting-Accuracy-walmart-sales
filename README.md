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

***The metrics:***

The point forecast submission are being evaluated using the Root Mean Squared Scaled Error (RMSSE), which is derived from the Mean Absolute Scaled Error (MASE) that was designed to be scale invariant and symmetric. In a similar way to the MASE, the RMSSE is scale invariant and symmetric, and measures the prediction error (i.e. forecast - truth) relative to a “naive forecast” that simply assumes that step i = step i-1. In contrast to the MASE, here both prediction error and naive error are scaled to account for the goal of estimating average values in the presence of many zeros.

The uncertainy distributions are being evaluated using the Weighted Scaled Pinball Loss (WSPL). We are asked to provide the 50%, 67%, 95%, and 99% uncertainty intervals together with the forecasted median.

Both metrics are computed for each time series and then averaged accross all time series including weights. The weights are proportional to the sales volume of the item, in dollars, to give more importance to high selling products. Note, that the weights are based on the last 28 days of the training data, and that those dates will be adjusted for the ultimate evaluation data, as confirmed by the organisers.
