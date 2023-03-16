**Title: Supervised Learning**
**Created: 14-03-2023**
**Tags:**

## How the algorithm works

brief overview of how each algorithm works:

1.  Linear Regression: Linear regression works by finding the line that best fits the data by minimizing the sum of squared errors between the predicted values and actual values. This is done by calculating the coefficients of the line that minimize the sum of squared errors using an optimization algorithm such as gradient descent.
    
2.  Logistic Regression: Logistic regression works by modeling the probability of a binary outcome as a function of the input features using a logistic function. The logistic function maps any real-valued input to the range [0, 1], which can be interpreted as the probability of the positive class. The coefficients of the logistic function are found by maximizing the likelihood of the data given the model parameters.
    
3.  Decision Trees: Decision trees work by recursively splitting the feature space into regions that maximize the separation between the classes. At each split, the algorithm chooses the feature and threshold that maximizes the reduction in impurity (e.g., Gini impurity or entropy) between the two resulting subsets. This process is repeated until the subsets are pure or a stopping criterion is met.
    
4.  Random Forest: Random forests work by building multiple decision trees on bootstrapped samples of the training data and using random subsets of the features at each split. The predictions of the individual trees are then combined by either taking the majority vote (for classification) or averaging the predictions (for regression).
    
5.  Naive Bayes: Naive Bayes works by calculating the posterior probability of each class given the input features using Bayes' theorem and assuming that the features are conditionally independent given the class. The prior probabilities and conditional probabilities are estimated from the training data.
    
6.  Support Vector Machines (SVMs): SVMs work by finding the hyperplane in the feature space that maximizes the margin between the closest points of different classes. The points closest to the hyperplane are called support vectors. In cases where the classes are not linearly separable, the input data can be mapped to a higher-dimensional space using a kernel function, which allows for linear separation.
    ![](Image/svm_illustration.jpg)
    
1.  K-Nearest Neighbors (KNN): KNN works by finding the k closest training examples to the test example in the feature space and predicting the majority class label among those k examples. The distance between examples can be measured using various distance metrics, such as Euclidean distance or Manhattan distance.
    ![](Image/knn_illustration.jpg)
8.  Neural Networks: Neural networks work by using a network of interconnected nodes (neurons) that transform the input features through a series of nonlinear transformations and produce an output. The network is trained using backpropagation, which adjusts the weights of the connections between the neurons to minimize the error between the predicted output and the actual output.
    
9.  Gradient Boosting: Gradient boosting works by sequentially adding weak models to the ensemble and correcting the errors of the previous models. Each new model is trained to minimize the residual error of the previous models using gradient descent or a similar optimization algorithm.
    
10.  Linear Discriminant Analysis (LDA): LDA works by finding the linear combination of the input features that maximizes the separation between the classes, while minimizing the within-class variance. This is done by calculating the eigenvectors of the covariance matrix of the input features and projecting the data onto the subspace spanned by the top eigenvectors.

## Related Notes

## References
