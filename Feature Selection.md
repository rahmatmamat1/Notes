**Title: Feature Selection**
**Created: 23-03-2023**
**Tags:**

## Feature Selection

- Select a **subset** of the original features for model training.
- Is usually used as a pre-processing step before doing actual learning.
- There is no best feature selection method

**Advantages:**
- Avoid the curse of dimensionality
- Improve predictive performance and interpretability of models
	- Shorten training times -> improve computational efficient
	- Reduce generalization error of the model by removing irrelevant features or noise
	- Improve predictive power of the model if  a model suffers from overfitting

**Domain knowledge is important!**
- Understand the business problem: know which feature matter and which ones don't
- Consult with domain experts
- Exploratory Data Analysis (EDA)


## Feature Selection Method

### Intrinsic methods
- Embedded method or implicit methods
- Have feature selection naturally embedded with the training process.

![[feature_selection_intrinsic_method.png]]

so which ML algorithm can help us do this?

#### Tree-based models
- Search for the best feature so that the outcomes are more homogeneous with each new partition.
- If feature is not used in any split, it's independent of target variable

#### Regularization models
- L1-regularization penalizes many of estimated coefficients to zero -> only keep features with non-zero coefficient
- Model used regularization, e.g. linear regression, logistic regression, SVMs.

#### Pros and Cons
- ✅ Fast because feature selection is embedded within model fitting process
- ✅ No external feature selection tool is needed
- ✅ Provide a direct connenction between feature selection and the object function in logistic regression which make it easier to make informed choice.
- ❌ Model-dependent and choice of models are limited.


###


## Related Notes

## References
