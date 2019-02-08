Dataset - https://drive.google.com/file/d/1bypF5zuUJUP1nLLfMQqac5WEQ_XAtoBK/view?usp=sharing

For more details - https://link.medium.com/8zMSqFI16T


ARIMA
An ARIMA model is a class of statistical models for analyzing and forecasting time series data.

It explicitly caters to a suite of standard structures in time series data, and as such provides a simple yet powerful method for making skillful time series forecasts.

AR: Autoregression. A model that uses the dependent relationship between an observation and some number of lagged observations.
I: Integrated. The use of differencing of raw observations (e.g. subtracting an observation from an observation at the previous time step) in order to make the time series stationary.
MA: Moving Average. A model that uses the dependency between an observation and a residual error from a moving average model applied to lagged observations.


The parameters of the ARIMA model are defined as follows:
p: The number of lag observations included in the model, also called the lag order.
d: The number of times that the raw observations are differenced, also called the degree of differencing.
q: The size of the moving average window, also called the order of moving average.

A linear regression model is constructed including the specified number and type of terms, and the data is prepared by a degree of differencing in order to make it stationary, i.e. to remove trend and seasonal structures that negatively affect the regression model.

A value of 0 can be used for a parameter, which indicates to not use that element of the model. This way, the ARIMA model can be configured to perform the function of an ARMA model, and even a simple AR, I, or MA model.



An ARIMA model can be created using the statsmodels library as follows:
- Define the model by calling ARIMA() and passing in the p, d, and q parameters.
- The model is prepared on the training data by calling the fit() function.
- Predictions can be made by calling the predict() function and specifying the index of the time or times to be predicted.


We can automate the process of evaluating a large number of hyperparameters for the ARIMA model by using a grid search procedure. We can automate the process of training and evaluating ARIMA models on different combinations of model hyperparameters. In machine learning this is called a grid search or model tuning.

The approach is broken down into two parts:
1. Evaluate an ARIMA model.
2. Evaluate sets of ARIMA parameters.


1. Evaluate an ARIMA model.
This approach involves the following steps:

1. Split the dataset into training and test sets.
2. Walk the time steps in the test dataset.
	a.Train an ARIMA model.
	b.Make a one-step prediction.
	c.Store prediction; get and store actual observation.
3. Calculate error score for predictions compared to expected values.



The dataset is split in two: 66% for the initial training dataset and the remaining 34% for the test dataset.

Each time step of the test set is iterated. Just one iteration provides a model that you could use to make predictions on new data. The iterative approach allows a new ARIMA model to be trained each time step.

A prediction is made each iteration and stored in a list. This is so that at the end of the test set, all predictions can be compared to the list of expected values and an error score calculated. In this case, a mean squared error score is calculated and returned.

2. Evaluate sets of ARIMA parameters.
Specify a grid of p, d, and q ARIMA parameters to iterate. A model is created for each parameter and its performance evaluated by calling the evaluate_arima_model() function described in the previous section.

There are two additional considerations. 
	-The first is to ensure the input data are floating point values (as opposed to integers or strings), as this can cause the ARIMA 	procedure to fail.

	-Second, the statsmodels ARIMA procedure internally uses numerical optimization procedures to find a set of coefficients for the 	model. These procedures can fail, which in turn can throw an exception. We must catch these exceptions and skip those 	configurations that cause a problem. This happens more often then you would think

The Least MSE is the best set of parameters.
