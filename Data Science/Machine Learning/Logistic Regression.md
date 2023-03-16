**Title: Logistic Regression**
**Created: 16-03-2023**
**Tags:** #SupervisedLearning #Classification 

## What is Logistic Regression?

This type of statistical model (also known as _logit model_) is often used for classification and predictive analytics. Logistic regression estimates the probability of an event occurring, such as voted or didn’t vote, based on a given dataset of independent variables. Since the outcome is a probability, the dependent variable is bounded between 0 and 1. Unlike Linear Regression, Logistic Regression predicts probabilities using a range of 0% to 100%. Note the difference between predictions a linear regression model and logistic regression model make:

![](Image/logreg_logreg_vs_linreg.webp)

Let’s delve deeper into how logistic regression works by determining the probability of selling houses with varying sizes.

We start our process again by collecting data about house sizes in Mark’s neighborhood and seeing if they sold or not.

![](Image/logreg_data.webp)

Now let’s plot these points:

![](Image/logreg_plot-data.webp)

Rather than representing the outcome of the plot as a binary output, it may be more informative to represent it using probabilities since that is the quantity we are trying to predict.

> We represent 100% probability as 1 and 0% probability as 0

![](Image/logreg_plot-data-prob.webp)

We learned about linear regression and its ability to fit a line to our data. But can it work for our problem where the desired output is a probability? Let’s find out by attempting to fit a line using linear regression.

We know that the formula for the best-fitting line is:

![](Image/logreg_linreg-formula.webp)

By following the steps outlined in linear regression, we can obtain optimal values for β₀ and β₁, which will result in the best-fitting line. Assuming we have done so, let’s take a look at the line that we have obtained:

![](Image/logreg_linreg-line.webp)

Based on this line, we can see that a house with a size just below 2700 feet² is predicted to have a 100% probability of being sold:

![](Image/logreg_linreg-line1.webp)

…and a 2200 feet² house is predicted to have a 0% chance of being sold:

![](Image/logreg_linreg-line2.webp)

and a 2300 feet² house is predicted to have about a 20% probability of being sold. Alright, so far so good. But what if we have a house that is 2800 feet² in size?

![](Image/logreg_linreg-line2.webp)

Uh.. what does a probability above 100% mean? Would a house of this size be predicted to sell with a probability of 150%??

Weird. What about a house that’s 2100 feet²?

Okay, clearly we have run into a problem as the predicted probability for a house with a size of 2100 feet² appears to be negative. This definitely does not make sense, and it indicates an issue with using a standard linear regression line.

As we know, the range of probabilities is from 0 to 1, and we cannot exceed this range. So we need to find a way to constrain our predicted output to this range.

To solve this issue, we can pass our linear regression equation through a super cool machine called a *sigmoid function*. This machine transforms our predicted values to fall between 0 and 1. We input our z value (where z = β₀ + β₁size) into the machine…

![](Image/logreg_sigmoid.webp)

…and out comes a fancy-looking new equation.

> NOTE: The **e** in the output is a constant value and is approximately equal to 2.718.

A math-ier way of representing the `sigmoid function:`

![](Image/logreg_sigmoid1.webp)

If we plot this, we see that the sigmoid function squeezes the straight line into an s-shaped curve confined between 0 and 1.

![](Image/logreg_sigmoid-plot.webp)

> Optional note for all my math-heads: You might be wondering why and how we used the sigmoid function to get our desired output. Let’s break it down.
> 
> We started with the incorrect assumption that using the linear regression formula will give us our desired probability.

![](Image/logreg_sigmoid-formula1.webp)

> The issue with this assumption is that (β₀ + β₁size) has range (-∞,+∞) and p has a range of [0,1]. So we need to find a value that has a range that matches that of (β₀ + β₁size).
> 
> To overcome this issue, we can equate the line to“log odds” (watch [this video](https://www.youtube.com/watch?v=ARfXDSkQf1Y) to understand log odds better) because we know that the log odds has a range of (-∞,+∞).

![](Image/logreg_sigmoid-formula2.webp)

> Now that we did that, it’s just a matter of rearranging this equation, so that we find what the **p** value should equal.

![](Image/logreg_sigmoid-formula3.webp)

Now that we know how to modify the linear regression line so that it fits our output constraints, we can return to our original problem.

We need to determine the optimal curve for our dataset. To achieve this, we need to identify the optimal values for β₀ and β₁ (because these are the only values in the predicted probability equation that will change the shape of the curve).

Similar to linear regression, we will leverage a cost function and the gradient descent algorithm to obtain suitable values for these coefficients. The key distinction, however, is that we will not be employing the [**MSE** cost function used in linear regression](https://medium.com/towards-data-science/back-to-basics-part-uno-linear-regression-cost-function-and-gradient-descent-590dcb3eee46#e9d3). Instead, we will be using a different cost function called **Log Loss**, which we will explore in greater detail shortly.

Say we used gradient descent and the **Log Loss** cost ([using these steps](https://medium.com/towards-data-science/back-to-basics-part-dos-linear-regression-cost-function-and-gradient-descent-e3d7d05c56fd)) to find that our optimal values are β₀ = -120.6 and β₁ = 0.051, then our predicted probability equation will be:

![](Image/logreg_calc1.webp)

And the corresponding optimal curve is:

![](Image/logreg_calc2.webp)

With this new curve, we can now tackle Mark’s problem. By looking at it, we can see that a house with a size of 2400 feet²…

![](Image/logreg_calc3.webp)

…has a predicted probability of approximately 78%. Therefore, we can tell Mark not to worry because it looks like his house is pretty likely to sell.

We can further enhance our approach by developing a **Classification Algorithm**. A classification algorithm is commonly used in machine learning to categorize data into categories. In our case, we have two categories: houses that will sell and houses that will not sell.

To develop a classification algorithm, we need to define a threshold probability value. This threshold probability value separates the predicted probabilities into two categories, “yes, the house will sell” and “no, the house will not sell.” Typically, 50% (or 0.5) is used as the threshold value.

If the predicted probability for a house size is above 50%, it will be classified as “will sell,” and if it’s below 50%, it will be classified as “won’t sell.”

![](Image/logreg_calc4.webp)

And that’s about it. That’s how we can use logistic regression to solve our problem. Now let’s understand the cost function we used to find optimal values for logistic regression.

## Cost Function

In linear regression, the cost is based on how far off the line was from our data points. And, in logistic regression, the cost function depends on how far off our predictions are from our actual data, _given that we are dealing with probabilities_.

If we used the [**MSE** cost function](https://towardsdatascience.com/back-to-basics-part-uno-linear-regression-cost-function-and-gradient-descent-590dcb3eee46#e9d3) (like we did in linear regression) in logistic regression, we would end up with a **_non-convex_** (fancy term for a _not-so-pretty-curve-that-can’t-be-used-effectively-in-gradient-decsent_) [cost function curve that can be difficult to optimize.](https://medium.com/towards-data-science/back-to-basics-part-dos-linear-regression-cost-function-and-gradient-descent-e3d7d05c56fd#6754)

![](Image/logreg_cost-function1.webp)

And as you may recall from our discussion on gradient descent, it is much easier to optimize a **_convex_** (aka _a curve with a distinct minimum point_) curve like this than a non-convex curve.

![](Image/logreg_cost-function2.webp)
To achieve a convex cost function curve, we use a cost function called **Log Loss**.

To break down the **Log Loss** cost function, we need to define separate costs for when the house actually sold (y=1) and when it did not (y=0).

If `y = 1` and we predicted 1 (i.e., 100% probability it sold), there is no penalty. However, if we predicted 0 (i.e., 0% probability it didn’t sell), then we get penalized heavily.

![](Image/logreg_cost-function3.webp)

Similarly, if `y = 0` and we predicted a high probability of the house selling, we should be penalized heavily, and if we predicted a low probability of the house selling, there should be a lower penalty. The more off we are, the more it costs us.

![](Image/logreg_cost-function4.webp)

To compute the cost for all houses in our dataset, we can average the costs of all the individual predictions like this:

![](Image/logreg_cost-function5.webp)

By cleverly rewriting the two equations, we can combine them into one to give us our **Log Loss** cost function.

![](Image/logreg_cost-function6.webp)

This works because one of those two will always be zero, so only the other one will be used.

And the combined cost graph looks like this:

![](Image/logreg_cost-function7.webp)

Now that we have a good understanding of the math and intuition behind logistic regression, let’s see how Mark’s house size problem can be implemented in Python.

```python
import pandas as pd
import numpy as np
from sklearn.linear_model import LogisticRegression

# Generate our house size dataset
df = pd.DataFrame([[2100,0], [2200,0], [2550,1], [2600,1], [2700,1]], columns=['size', 'sold?'])

# Create a logistic regression classifier
clf = LogisticRegression()

# Fit the classifier to the house dataset
clf.fit(df[['size']], df['sold?'])

# Print the optimal b0 value
print(clf.intercept_)

# Print the optimal b1 value
print(clf.coef_)

# Create a numpy array with Mark's house size (because that's what we're trying to predict)
X_pred = np.array([[2400]])

# Predict the probability of selling the house
prob_sold = clf.predict_proba(X_pred)[0][1]
print("Predicted probability:", prob_sold)

# Predict the classification outcome (the house will sell [1] or it won't [0])
predicted_class = clf.predict(X_pred)[0]
print("Predicted classification:", predicted_class)
```


## Related Notes
* [[Classification Evaluation Metrics]]
* 

## References
* [Back to Basics, Part Tres: Logistic Regression](https://towardsdatascience.com/back-to-basics-part-tres-logistic-regression-e309de76bd66)
* [Logistic Regression — Detailed Overview](https://towardsdatascience.com/logistic-regression-detailed-overview-46c4da4303bc)
* [What is logistic regression?](https://www.ibm.com/topics/logistic-regression#:~:text=Resources-,What%20is%20logistic%20regression%3F,given%20dataset%20of%20independent%20variables.)
* [Logistic Regression from scratch](https://github.com/SSaishruthi/LogisticRegression_Vectorized_Implementation/blob/master/Logistic_Regression.ipynb)