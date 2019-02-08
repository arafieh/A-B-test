## A/B_test
### Analyzing data of a website design changing and making a recommendation for best design based on A/B test.
### by Ali Rafieh

### Project Overview

A/B tests are very commonly performed by data analysts and data scientists. It is important that you get some practice working with the difficulties of these.

For this project, I worked to understand the results of an A/B test run by an e-commerce website. The company has developed a new web page in order to try and increase the number of users who "convert," meaning the number of users who decide to pay for the company's product. My goal was to work through this project (all done in jupyter notebook) to help the company understand if they should implement this new page, keep the old page, or perhaps run the experiment longer to make their decision.

### Dataset Overview

All the project data run for random 294478 user and for 'control' group show old design and for 'treatment' group show new design and if user change from old to new design or vice versa, data had been kept in column named 'converted'. So, for a convert '1' and non-convert '0' saved in this column.

Here is an example of dataset:

| user_id 	| timestamp 	| group 	| landing_page 	| converted 	|
|:-------:	|----------------------------	|-----------	|--------------	|-----------	|
| 851104 	| 2017-01-21 22:11:48.556739 	| control 	| old_page 	| 0 	|
| 804228 	| 2017-01-12 08:01:45.159739 	| control 	| old_page 	| 0 	|
| 661590 	| 2017-01-11 16:55:06.154213 	| treatment 	| new_page 	| 0 	|
| 853541 	| 2017-01-08 18:28:03.143765 	| treatment 	| new_page 	| 0 	|
| 864975 	| 2017-01-21 01:52:26.210827 	| control 	| old_page 	| 1 	|

After assessing and cleaning dataset, 3893 records removed.

### Analysis Process

I first goes with 'Probability' to assess the quality of records and then using an A/B test to which design has higher chance to attract users. And, at the end, I also run a 'logistic regression' to compare result with A/B test.

#### Probability assessment

Here is the result: With attention to %50 chance for an individual to receive 'new page', it is a fair percentage, and almost equal probability for both 'control' and 'treatment' groups, ~ %12, which is near to probability of converting for an individual, regardless of the page they receive, we can say in this fair situation, there is not sufficient evidence for new treatment page is getting more attention rather than the old one to be lead in convention.

#### A/B test

>Note: that because of the time stamp associated with each event, I could technically run a hypothesis test continuously as each observation was observed.  

I assumed that the old page is better unless the new page proves to be definitely better at a Type I error rate of 5%, so null and alternative hypotheses are:

H0 : p(old) – p(new) >= 0

H1 : p(old) – p(new) < 0

Here is the steps and results:

1.computed the observed difference between the metric, click through rate, for the control and experiment group.

2. Simulated a sampling distribution for the difference in proportions (or difference in click through rates).

3. Used this sampling distribution to simulate the distribution under the null hypothesis, by creating a random normal distribution centered at 0 with the same spread and size.

4. Computed the p-value by finding the proportion of values in the null distribution that were greater than our observed difference.

5. Used this p-value to determine the statistical significance of our observed difference.
  
So, after calculated p-value, which is 0.9052 and it is greater than 0.05 (the type I error, maximum error which we can tolerate to reject null), I fail to reject null hypotheses and both old and new pages, based on our data and observation, don't have any priority to be lead in convention.

In other word, in favor of alternative, I fail reject null. It shows new page in converting rate isn't bigger than old page and, based on our observation and statistically, the difference of these two pages is less equal zero.

I also used a built-in to achieve similar results (z test)

#### Regression model

I created intercept and needed dummy variables ('ab_page'), developed and fit model. Then I used Sigmoid function to turn coefficients.

This time, as same result in A/B test, I failed to reject H0 and old and new design had not different to improve website users.

Using one variable is a great way to predict response based on explanatory, when they have great correlation. But, in most of the time, there are other variables which have significant effect on your response variable and predict dependent variable without those, certainly is a mistake.

In other hand, adding additional variables can cause some errors in your equation:

1. Non-linearity of the response-predictor relationships

2. Correlation of error terms

3. Non-constant Variance and Normally Distributed Errors

4. Outliers/ High leverage points

5. Collinearity

For example collinearity in multi factor regression should be check. If two or more of your variable have strong correlation together, the regression equation has bias and can predict response variable.

So, I also added an effect based on which country a user lives, and developed new model and fit it. The final result, stayed same and I failed to reject H0.
