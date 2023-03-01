When the outcome is a number, the most common metric is the **root mean squared error (RMSE).** To calculate this value, a model is built and then it is used to predict the outcome. The _residuals_ are the difference between the observed outcome and predicted outcome values. To get the RMSE for a model, the average of the squared residuals is computed, then the square root of this value is taken. Taking the square root puts the metric back into the original measurement units. We can think of RMSE as the average distance of a sample from its observed value to its predicted value. Simply put, the lower the RMSE, the better a model can predict samples’ outcomes.

Another popular metric is the coefficient of determination, usually known as $R^2$ There are several formulas for computing this value (Kvalseth 1985), but the most conceptually simple one finds the standard correlation between the observed and predicted values (a.k.a. $R$) and squares it. The benefit of this statistic is, for linear models, it has a straightforward interpretation:  $R^2$ is the proportion of the total variability in the outcome that can be explained by the model. A value near 1.0 indicates an almost perfect fit while values near zero result from a model where the predictions have no linear association with the outcome. One other advantage of this number is that it makes comparisons between different outcomes easy since it is unitless.

Unfortunately, $R^2$ can be a deceiving metric. The main problem is that it is a measure of correlation and not accuracy. When assessing the predictive ability of a model, we need to know how well the observed and predicted values _agree_.

Regression evaluation metrics.
1.  **Mean Squared Error (MSE):**
	* **Formula**:$$\mathrm{MSE} = \frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{y}_i)^2$$
	* **Advantage:** Punishes large errors heavily, providing a high sensitivity to large deviations in the data.
	* **Disadvantage:** The squared nature of MSE can make it difficult to interpret the metric in terms of the original units of the data.
2.  **Root Mean Squared Error (RMSE):**
	* **Formula:**$$\mathrm{RMSE} = \sqrt{\frac{1}{n}\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}$$
	* ***Advantage:** RMSE is interpretable in the same units as the original data, making it easier to understand the magnitude of the error.
	* **Disadvantage:** Like MSE, RMSE can be heavily influenced by large errors in the data.
3.  **Mean Absolute Error (MAE):**
	* **Formula:**$$\mathrm{MAE} = \frac{1}{n}\sum_{i=1}^{n} |y_i - \hat{y}_i|$$
	* **Advantage:** MAE is less sensitive to outliers compared to MSE and RMSE, making it a more robust metric in the presence of extreme values.
	* **Disadvantage:** As a result of being less sensitive to large errors, MAE may not accurately reflect the true error in the model.
4.  **Mean Absolute Percentage Error (MAPE):**
	* **Formula:** $$\mathrm{MAPE} = \frac{1}{n}\sum_{i=1}^{n} \left|\frac{y_i - \hat{y}_i}{y_i}\right| \times 100\%$$
	* **Advantage:** MAPE provides a measure of the average percentage deviation of the predicted values from the actual values, which can be useful for evaluating performance in cases where the magnitude of the errors is important.
	* **Disadvantage:** MAPE can be problematic when the actual values are close to zero, since division by zero is undefined.
7.  **Mean Squared Log Error (MSLE):**
	* **Formula:**$$\mathrm{MSLE} = \frac{1}{n}\sum_{i=1}^{n} (\log(y_i + 1) - \log(\hat{y}_i + 1))^2$$
	* MSLE measures the average squared difference between the logarithm of the predicted and actual values. It is useful when the target variable has a wide range of values and the goal is to penalize large differences between the predicted and actual values while allowing for some relative error. The disadvantage of MSLE is that it tends to give more weight to underestimation errors than overestimation errors, due to the asymmetrical nature of logarithmic transformations.
8. **Symmetric Mean Absolute Percentage Error (SMAPE):**
	* **Formula:**$$\mathrm{SMAPE} = \frac{1}{n}\sum_{i=1}^{n} \frac{|y_i - \hat{y}_i|}{(|y_i|+|\hat{y}_i|)/2} \times 100\%$$
	* SMAPE measures the average percentage difference between the predicted and actual values, with a twist that it uses the average of the absolute values of the predicted and actual values in the denominator instead of just the actual values. This makes SMAPE a symmetric metric, meaning it equally penalizes overestimation and underestimation errors. It is useful when the scale of the target variable is important, as it measures the percentage deviation in a scale-independent way. However, SMAPE can produce infinite or undefined values when the actual value is zero.
9. Median Absolute Error (MdAE)
	* **Formula:** $$ \mathrm{MdAE} = \mathrm{median}(\sum_{i=1}^{n}|y_i - \hat{y}_i|) $$
	* Median Absolute Error (MdAE) is a metric used in regression analysis to measure the accuracy of a model's predictions. It is similar to Mean Absolute Error (MAE), but instead of taking the mean of the absolute errors between predicted and actual values, it takes the median of the absolute errors.
	* MdAE is expressed in the same units as the target variable, making it easy to interpret. A smaller value of MdAE indicates better predictive accuracy, as it means the model's predictions are closer to the actual target values.
	* MdAE is useful in situations where the data has a skewed distribution, or when there are outliers present. It is also more robust to errors than Mean Absolute Error, as it is less sensitive to extreme values in the data.
10.  **R-Squared ($R^2$):**
	* **Formula:**$$R^2 = 1 - \frac{\sum_{i=1}^{n}(y_i - \hat{y}_i)^2}{\sum_{i=1}^{n}(y_i - \bar{y})^2}$$
	* **Advantage:** $R^2$ is a commonly used metric that provides a measure of the proportion of the variance in the dependent variable that can be explained by the independent variables in the model.
	* **Disadvantage:** $R^2$ can be misleading when applied to models with a large number of predictors, and can sometimes produce artificially high values for models with complex interactions.
11.  **Coefficient of Determination (Adjusted $R^2$):**
	* **Formula:**$$\mathrm{Adjusted};R^2 = 1 - \frac{(1-R^2)(n-1)}{n-p-1}$$
	* **Advantage:** Adjusted $R^2$ addresses some of the issues with $R^2$ by penalizing the model for adding too many predictors that do not improve the model's performance.
	* **Disadvantage:** Adjusted $R^2$ is less intuitive than $R^2$, and may not be easily interpreted by non-experts.

where $n$ is the number of observations, $y_i$ is the actual target value for the $i$th observation, and $\hat{y}_i$ is the predicted target value for the $i$th observation.

