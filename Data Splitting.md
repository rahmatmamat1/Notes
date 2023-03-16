**Title: Data Splitting**
**Created: 13-03-2023**
**Tags:**

Data splitting is a technique used in machine learning to divide a dataset into multiple subsets for different purposes. One common technique is to split the data into two groups typically referred to as the _training_ and _testing_ sets. The training set is used to develop models and feature sets; they are for estimating parameters, comparing models, and all of the other activities required to reach a final model. The test set is used only at the conclusion of these activities for estimating a final, unbiased assessment of the model’s performance. It is critical that the test set not be used prior to this point. Looking at the test sets results would bias the outcomes since the testing data will have become part of the model development process.

There are several ways to split data for machine learning, but the most common approaches are:

1.  Train/Test Split: This approach involves dividing the dataset into two subsets: a training set and a testing set. The training set is used to train the machine learning model, while the testing set is used to evaluate its performance. Typically, the training set contains 70-80% of the data, while the testing set contains the remaining 20-30%.
    
2.  K-Fold Cross Validation: This approach involves dividing the dataset into k equally sized subsets, or "folds". The machine learning model is then trained on k-1 folds and tested on the remaining fold. This process is repeated k times, with each fold serving as the testing set once. The performance of the model is then averaged over the k folds.
    
3.  Stratified Sampling: This approach is used when the dataset is imbalanced, meaning that the classes are not equally represented. Stratified sampling ensures that each subset contains a proportional representation of each class. This is important because if one class is underrepresented in the training set, the machine learning model may not learn to recognize it properly.
    
Data splitting is an important technique in machine learning because it helps to prevent overfitting, which is when the machine learning model memorizes the training data instead of learning the underlying patterns. By testing the model on a separate subset of the data, we can get a more accurate estimate of its performance on new, unseen data.


## Questions

1. **What will happen when dataset are imbalance?**
	 When a dataset is imbalanced, it means that one or more classes are underrepresented in the data compared to the other classes. For example, in a binary classification problem, if the positive class represents only 10% of the dataset, the dataset is considered imbalanced.
	
	Imbalanced datasets can cause problems for machine learning algorithms because they may not be able to learn the minority class properly. Specifically, here are some issues that can arise when dealing with imbalanced datasets:
	1.  Bias: The model may become biased towards the majority class and may ignore the minority class altogether.
	2.  Poor Performance: The model's performance may be poor on the minority class because it does not have enough data to learn the underlying patterns.
	3.  Overfitting: The model may overfit to the majority class and perform poorly on new, unseen data.

2. **Give the example of stratified sampling**
	Here's an example of stratified sampling:
	
	Suppose we have a dataset of 1000 images of cats and dogs, where 800 images are cats and 200 images are dogs. We want to split this dataset into a training set and a testing set, but we want to ensure that both sets have a proportional representation of cats and dogs.
	
	To do this, we can use stratified sampling. First, we count the number of images for each class. In this case, we have 800 cats and 200 dogs. Next, we decide on the proportion of the dataset we want to use for training and testing. Let's say we want to use 70% of the data for training and 30% for testing.
	
	To create the training set, we first divide the cats and dogs into separate groups. Then, we randomly select 70% of the cats and 70% of the dogs to include in the training set. This ensures that the training set has a proportional representation of cats and dogs.
	
	To create the testing set, we take the remaining 30% of the cats and 30% of the dogs that were not included in the training set. This ensures that the testing set also has a proportional representation of cats and dogs.


## Related Notes
* [[Resampling]]
* 

## References
