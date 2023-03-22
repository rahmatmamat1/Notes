**Title: Data Splitting**
**Created: 13-03-2023**
**Tags: #Sampling**

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

3. **Why do we need to split data into data training, validation, testing. instead of just split it into training and testing?**
	By splitting our data into three sets - training, validation, and testing - we can better monitor and improve model performance. We use the training set to fit the model, the validation set to tune model hyperparameters, and the testing set to evaluate the final performance of the model on new, unseen data. This helps ensure that the model is both accurate and generalizable.

4. **What is the typical ratio of data splitting for training, validation, and testing?**
	The typical ratio of data splitting for training, validation, and testing can vary depending on the size and complexity of the dataset, as well as the specific problem being addressed. However, there are some common ratios that are often used as a starting point:
	-   60/20/20: In this split, 60% of the data is used for training, 20% for validation, and 20% for testing. This is a commonly used split for small to medium-sized datasets.
	-   70/15/15: This split is similar to the 60/20/20 split, but with a slightly larger proportion of data allocated to training. This split is often used for larger datasets.
	-   80/10/10: In this split, 80% of the data is used for training, and 10% each for validation and testing. This split is often used when there is a large amount of data available and the model is relatively simple.

5. **How do you ensure that your data is split randomly and without bias?**
	Ensuring that data is split randomly and without bias is crucial for creating a robust machine learning model. Here are some techniques for achieving a random and unbiased split:

	1.  Random shuffling: Before splitting the data, randomly shuffle the dataset to ensure that the samples are in a random order.
	2.  Stratified sampling: If the dataset has class imbalance, use stratified sampling to ensure that the distribution of classes is roughly equal across the training, validation, and testing sets.
	3.  Time-based splitting: For time-series data, ensure that the data is split in a time-based manner, with data from earlier time periods allocated to the training set, and data from later time periods allocated to the validation and testing sets.
	4.  K-fold cross-validation: Use k-fold cross-validation to randomly split the data into k subsets, where each subset is used for validation once, and the remaining k-1 subsets are used for training. This helps to ensure that the model is trained on a diverse set of data.
	5.  Use a random seed: Use a random seed to ensure that the random split is reproducible. This helps to ensure that the same random split is used each time the code is run.
	6.  Multiple random splits: To ensure that the split is unbiased, it's a good practice to perform multiple random splits and evaluate the model performance on each split. This helps to ensure that the model is not overfitting to a particular random split.

6. **How stratified sampling can help improve model performance?**
	Stratified data splitting can help improve model performance in several ways:
	1.  Better representation of the data: Stratified data splitting ensures that the proportions of classes or categories are the same in both the training and testing sets. This helps to ensure that the model is trained on a representative sample of the data, which can improve its performance.
	2.  Reduced bias: When working with imbalanced datasets, stratified data splitting can help to reduce bias towards the majority class. By ensuring that the training and testing sets have a similar distribution of classes, the model can learn to accurately predict the minority classes.

7. **Can you describe the differences between simple random sampling and systematic sampling, and how they can be used in data splitting?**
	Simple random sampling and systematic sampling are two techniques used for sampling from a larger population of data. In data splitting, these techniques can be used to randomly select subsets of data for training and testing sets.

	Simple random sampling involves randomly selecting a subset of observations from the population, without any specific pattern or order. This can be done by assigning each observation in the population a random number, and then selecting a subset of observations based on their random numbers. Simple random sampling ensures that each observation in the population has an equal chance of being selected and is commonly used when the population is homogeneous.
	
	Systematic sampling, on the other hand, involves selecting observations from the population at regular intervals, based on a pre-specified pattern or order. For example, if you have a population of 100 observations and you want to select a sample of 10 observations, you can select every 10th observation in the population. Systematic sampling is useful when the population is heterogeneous and you want to ensure that the sample is representative of the entire population.
	
	In data splitting, simple random sampling can be used to randomly select a subset of observations for the training and testing sets. This ensures that the selected observations are representative of the entire population and can help prevent bias in the model. Systematic sampling can also be used to split the data into training and testing sets, by selecting every nth observation for the training set and the remaining observations for the testing set. However, this method may not be suitable for time series data or other types of data where the order of the observations is important.
	
	In summary, simple random sampling and systematic sampling are two techniques used for sampling from a larger population of data. Simple random sampling involves randomly selecting a subset of observations without any specific pattern or order, while systematic sampling involves selecting observations from the population at regular intervals based on a pre-specified pattern or order. Both techniques can be used for data splitting, depending on the characteristics of the data and the sampling goals.

8. **Can you give me use case when we should use systematic sampling?**
	Sure! Systematic sampling can be useful in situations where the population of data is large and homogeneous, and a representative sample is needed for analysis. Here are a few use cases where systematic sampling may be appropriate:
	1.  Surveying a large population: When conducting a survey of a large population, it may be impractical or costly to survey every individual in the population. Systematic sampling can be used to select a representative sample of individuals from the population, by selecting every nth individual from a list of the population.
	2.  Analyzing large datasets: When analyzing large datasets, it may be time-consuming or computationally expensive to analyze every observation in the dataset. Systematic sampling can be used to select a representative subset of observations from the dataset, by selecting every nth observation in the dataset.
	3.  Quality control in manufacturing: In manufacturing, it may be necessary to perform quality control inspections on a subset of products to ensure that they meet certain standards. Systematic sampling can be used to select a representative sample of products from the production line, by selecting every nth product for inspection.

## Related Notes
* [[Resampling]]
* 

## References
