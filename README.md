# predict_SP500_monthly_stock_prices
This
 is a * REGRESSION** problem. It asks you to predict the *SP500 monthly return rate based on a set of indicators that can be: monthly stock prices indexex for the major world Economies (UK, EA, GER, IT, FR, JP, CA), financial market indicators (taken from Goyal and Welch) and macroeconomic indicators.

The SP500 monthly return rate are recorded in the dataset as CRSP_SPvw.

The financial market indicators from Goyal and Welch contains key variables related to the most important stock market features over time.

Extra information about the Goyal and Welch variables can be find at the following link: http://www.hec.unil.ch/agoyal/docs/Predictability_RFS.pdf

Extra information about the macroeconomic series and the meaning of their ticker can be found at the following link: https://s3.amazonaws.com/files.fred.stlouisfed.org/fred-md/Appendix_Tables_Update.pdf

The timeseries_train.csv dataset contains all these 3 groups of monthly variables from January 1970 to December 2009. All the variables have already been properly stationarized. The target variables (y) is the SP500 monthly return rate (CRSP_SPvw) while all the other variables are the predictors (X).

You need to use such predictors to train your algorithms in predicting the target variable.

The * timeseries_test.csv* dataset contains information ONLY about these 3 groups of monthly variables from January 2010 to March 2020. You do not have information about the SP500 monthly return rate (CRSP_SPvw) (target or y).

Following the steps below, you are required to use the timeseries_train.csv dataset to train your algorithms, select the best one with its hypeparameters properly calibrated and then apply such model to the timeseries_test.csv in order to predict the SP500 monthly return rate

A) Upload, Clean and Manipulate the data.
Import all the necessary packages and functions you will need to perform the exercise

Import the dataset using the pd.read_csv() command. (Hint: remeber to specify the separator.)

Compute the percentage of NaN for each column and drop the columns that have less than 10years of observations, hence less than 120 NaN.

Create a list which contains all the names of the columns with at least one NaN value. (Hint: % bigger than zero, use command .loc()).

Fill the NaN using the median or the mean for each variable. If there are NaN at the end of the sample you can fill them using the .ffill(), which fills the NaN using the last available data point.

Check the type of the variables, dividing them among: Categorical, Dummy and Numerical. (Hint: use : select_dtypes(include=[type to include]).

Separate the dates from the dataset (they will be helpful to plot the charts), separate the target SP500 monthly return rate (CRSP_SPvw) (y) from the dataset.

Are there any Categorical variables? If yes, separate them from the Numerical.

Define the matrix of the predictors (X) using only the numerical variables inside the dataset.

Standardize only the predictors. (X)

If the answer to point A.8 is yes, transfor the Categorical vairbales in Dummy Variables and include them into the dataset. ( hint: use drop_first = true)

Compute the correlation of the new dataset and show the top 10 variables correlated with the target, SP500 monthly return rate (CRSP_SPvw).

Separate the dates from the dataset (they will be helpful to plot the charts), separate the target SP500 monthly return rate (CRSP_SPvw) (y) from the dataset, and create the dataframe of the predictors. (X)

Extra: The dataset is quite big, but if you want to show some chart about the data, feel free to do it, sometimes visualize the data can help. You can produce different line plot between the target (SP500 monthly return rate) versus other variable to see if there are some commonalities among the data. (NOTE: the scale of the variables may be different, hence remember to standardize them before create such plots).

B) Fit and Estimate the models using a proper cross-validation exercise.
Split the X and the y obtained in the step above (A.8) into only: training and test sample. The size of the test needs to be = 0.15 use a random_state = 90.

Describe which models are you going to fit starting from the simplest to the most complicated. Explain why you have decided to use such models, which are their hyperparameters that need to be calibrated and which kind of cross-validation are you planning to use. To compare the different models during the training use as metric the ** negative mean squared error **. (Hint: in GridSearchCV the scoring needs to be = “neg_mean_squared_error”)

Create a section for each model you are going to fit. The models have to be fit sequentially and you need to do the following for EACH model you are going to use:

Specify the function of the model you are going to use. (Hint: if the model has a random_state option, i.e. random forest, set it = 90)
Specify a dictionary that contains the list of parameters you are going to cross-validate and the grid on which you intend to cross-validate them
Specify the cross-validation function, GridSearchCV with all its option. The number of cv needs to be at least 5, maximum 10. – Remember to specify return_train_score = True. (HINT: You can build your own cross-validation function, but remebr that you are in a time-series framework hence the blocks should be sequential not random. Otherwise, you can use the function TimeSeriesSplit(n_splits = #num) and use that as input for the “cv” option inside the GridSearchCV function.
Fit the model using the training data. Print the value of the best hyperparameters of the model fitted. (REMEMBER: This is a time series exercise, hence you need to predict the one-step ahead value of the CRSP_SPvw, hence rememebr when you fit the model and also when you predict it to use the X (predictors), from 0 to end-1, and the y (target) from 1 to end.)
Compute the TEST performances (using the test sample) using the mean squared error and the absolute mean squared error as metrics. Comment on these results. How are they in general?
Plot the y_hat_test_insample obtained from the model on the test data versus the real y_test. Does the model capture turning points?
EXTRA 1: If you fit a penalized logistic regression plot the evolution of both the training and test negative log loss with respect to the hyperparameter  𝜆  (which is alpha in Python).

EXTRA 2: If you are not satisfied with the performances of the model, how could you improve them? Propose a solution and try to implement it in Python. (Hint: you can use PolynomialFeatures to add interactions among the variables, maybe among the most correlated one, or you can create new variables by adding different interactions among them (ratios or others).

C) BEST MODEL SELECTION.
Compare all the TEST results for each model you have fitted and select the best model with its own best hyperparameters specification. Why this model is preferred than the others? What could be your intuition?

Load the timeseries_test.csv data, using the best model you have found above with its best hyperparameters (you don’t have to do any cross-validation exercise) produce the prediction for the target (call it y_hat)

Plot the y_hat you have produced.

Assuming you invested 1£ in the SP500 at the beginning of your test set, by applying the SP500 monthly return you have predicted, y_hat, what would be your predicted total return during the test period (from January 2010 to March 2020)?
