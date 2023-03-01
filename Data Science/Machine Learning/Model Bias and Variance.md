**_Variance_** is a well-understood concept. When used in regard to data, it describes the degree in which the values can fluctuate. If the same object is measured multiple times, the observed measurements will be different to some degree. In statistics, **_bias_** is generally thought of as the degree in which something deviates from its true underlying value. For example, when trying to estimate public opinion on a topic, a poll could be systematically biased if the people surveyed over-represent a particular demographic. The bias would occur as a result of the poll incorrectly estimating the desired target.

**Variance**, on the other hand, refers to the amount by which the model's predictions vary for different sets of input data. High variance can lead to overfitting, where the model becomes too complex and captures noise in the training data, resulting in good performance on the training data but poor generalization to new data.

**Bias** refers to the error that is introduced by approximating a real-life problem with a simpler model. In other words, it represents the difference between the expected prediction of the model and the true values. High bias can lead to underfitting, where the model is not complex enough to capture the underlying patterns in the data, resulting in poor performance on both the training and test data.

**Model with high variance** is highly sensitive to changes in the input data, resulting in a large variation in the predicted output for different input values.

**Model with high bias** is not complex enough to capture the underlying patterns in the data, resulting in a systematic underestimation or overestimation of the true values.

Examples of models with **low bias and high variance**, as well as **high bias and low variance**:
1. **Low bias and high variance**: A complex decision tree model with many branches and leaves can be an example of a model with low bias and high variance. This is because the model can fit the training data very well, but may not generalize well to new data because it has learned the noise in the training data. Another example, **nearest neighbor models and neural networks.**
2. **High bias and low variance**: A [[linear regression]] model with few features can be an example of a model with high bias and low variance. This is because the model is too simple to capture the complex patterns in the data, resulting in a higher error on the training and test data, but it is less affected by noise in the data, leading to lower variance. Another example, **logistic regression and partial least squares**.

**Model bias and variance can often be in opposition to one another**; in order to achieve low bias, models tend to demonstrate high variance (and vice versa). **The variance-bias trade-off is a common theme in statistics.**

One method of creating a **low-variance, low-bias model** is to augment a low-variance model with appropriate representations of the data to decrease the bias. Start with a simple or low-variance model and then enhance it by incorporating additional representations or features of the data that were not initially considered. By doing so, the model can become more flexible and better able to capture the underlying patterns in the data, reducing the bias.

For example, if a linear regression model is used to predict the price of a house based on the number of bedrooms and square footage, **it may have low variance but high bias** if it is too simple to capture the complexity of the data. **To reduce the bias, additional features such as the age of the house or the location can be added to the model**, allowing it to capture more information and become more flexible.

By augmenting the model with additional representations of the data, the variance can also be reduced because the model can capture more of the underlying patterns in the data, resulting in more consistent predictions for different input values. This can lead to a model that has both low variance and low bias, which can provide more accurate and reliable predictions for new or unseen data.

In a similar manner, **models can have reduced performance due to irrelevant predictors causing excess model variation**. **Feature selection techniques improve models by reducing the unwanted noise of extra variables.**

