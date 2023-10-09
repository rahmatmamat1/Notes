**Title: Ensemble Method**
**Created: 22-03-2023**
**Tags:**

## What is ensemble methods?

Ensemble methods are machine learning techniques that combine the predictions of multiple models to improve the overall performance. The main idea of ensemble method is that a group of "weak learners" can come together to form a "strong learner".

if one base learner is erroneous, it can be auto-corrected by others, so the final model is typically less prone to overfitting and more robust, unlikely to be influenced by small changes in the training data.

![](ensemble_concept.png)

There are several types of ensemble methods, including: Bagging, Boosting, Stacking

### Bagging (Bootstrap Aggregation)

Bagging is short for bootstrap aggregation. It build several instances of an estimator on bootstrap samples of the original training data and then aggregate their individual predictions to form a final prediction.

![[bagging_concept.png]]

1. **Create bootstrap samples** (sampling with replacement) from training data.
	- Ensure each samples are independent from others, as it does not depend on previous chosen samples when sampling.
2. **Use single learning algorithm to build a model using each sample**.
	- Those model are build in parallel.
3. **Use multiple model to make predictions and predictions are combined using voting or averaging**
	- **Voting** for classification: the most frequently result (mode) is the final prediction.
	- **Averaging** for regression: average the results produced is the final result.

**Example: Random Forest**

#### Random Forest

![[random_forest_concept.png]]

- Combine a set of decision trees to make predictions
- Decision tree are good candidates for bagging - they can capture complex interactions in the data, and if grown sufficiently deep, have relative low bias.
- Since trees are noisy, they benefit greatly from the voting/averaging

From bias-variance trade-off point of view, random forest start with low bias + high variance (each tree is fully grown) and work towards reducing variance (by taking majority vote or averaging across trees)

### Boosting

Boosting improve prediction power by training weak learners **sequentially**, each compensating the weaknesses of it's predecessors.

- Start with weak learner, gradually turn it into strong learner by letting future weak learner focus on correcting mistakes made by previous learners.
	- Misclassified examples gain a higher weight than examples that are classified correctly, so future learner focus more on the examples that previous learners misclassified.
- Reduce the bias of combined model

![[boosting_concept.png]]

1. Start with weak learner (e.g a shallow tree) better than random guess.
	- Some examples that are correctly classified and some are not
2. In the next iteration, the weights of the **data are re-adjusted** such that tey can be corrected in the succeeding round.
	- **lower weights** to those were **classified correctly**
	- **higher weights** to those were **classified incorrecty**
3. This sequential process of giving higher weights to misclassified predictions continues until a **stopping criterion is reached**.
4. The final prediction is a **weighted result of all weak learners**.

**Example: Gradient Boosted Trees**

#### Gradient Boosted Trees

- Train decision trees sequentially
- **Optimize the residual loss of a tree** by adding another tree
- It appear to outperform bagging on lost problems and become the preferred choice.

From bias-variance trade-off point of view, Gradient boosted trees start with low bias + high variance (first tree is shallow) and work towards reducing bias (by making tree more complicated).


### Bagging vs Boosting

|          | individual learners            | bias-variance   | example                |
| -------- | ------------------------------ | --------------- | ---------------------- |
| Bagging  | Independent, built in parallel | reduce variance | random forest          |
| Boosting | dependent, built sequentially  | reduce bias     | gradient boosted trees | 

Bagging method work best with strong complex models (e.g., fully developed decision trees,), while boosting methods usually work best with weak models (e.g., shallow decision trees).


### Stacking

- Building a meta-model that takes the output of base learners as input.
- Combining estimators to reduce their biases.
- Can applied to classification and regression problems
![[stacking_concept.png]]

**Two-level ensemble:**
- Individual estimators that feed their prediction to the second level.
- A combiner estimator is fit to the level-one estimator predictions to make the final prediction.

**Example:** 
A stacking model for classification task:
- Individual classifier: random forest and SVM
- Stacking classifier: logistic regression

**Pros and Cons**
- In prectice, a stacking predictors predict as good as the best predictor of the base layer and sometimes outperform it by combining the different strength of these predictors.
- Training a stacking predictor is computationally expensive

## Related Notes

## References
