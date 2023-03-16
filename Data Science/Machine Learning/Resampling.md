**Title: Resampling**
**Created: 13-03-2023**
**Tags:**

## Resampling

Resampling is a statistical technique used in machine learning to estimate the performance of a model on unseen data. It involves creating multiple training and testing sets by randomly sampling from the original dataset, and then training and evaluating the model on each of these sets. The goal of resampling is to obtain a more accurate estimate of a model's performance by reducing the effects of sampling variability and to prevent overfitting by using multiple subsets of the data for training and testing. These techniques differ in terms of how the resampled versions of the data are created and how many iterations of the simulation process are conducted. In each case, a resampling scheme generates a subset of the data to be used for modeling and another that is used for measuring performance. Here, we will refer to the former as the “analysis set” and the latter as the “assessment set”. They are roughly analogous to the training and test sets described at the beginning of the chapter. A graphic of an example data hierarchy with three resamples is shown in Figure.

![](Image/resampling.svg)

Here are some common resampling methods:

### _V_-Fold Cross-Validation and Its Variants

Simple _V_-fold cross-validation creates _V_ different versions of the original training set that have the same approximate size. Each of the _V_ assessment sets contains 1/_V_ of the training set and each of these exclude different data points. The analysis sets contain the remainder (typically called the “folds”) . Suppose _V_ = 10, then there are 10 different versions of 90% of the data and also 10 versions of the remaining 10% for each corresponding resample.

To use _V_-fold cross-validation, a model is created on the first fold (analysis set) and the corresponding assessment set is predicted by the model. The assessment set is summarized using the chosen performance measures (e.g., RMSE, the area under the ROC curve, etc.) and these statistics are saved. This process proceeds in a round-robin fashion so that, in the end, there are _V_ estimates of performance for the model and each was calculated on a different assessment set. The cross-validation estimate of performance is computed by averaging the _V_ individual metrics.

When the outcome is categorical, _stratified_ splitting techniques can also be applied here to make sure that the analysis and assessment sets produce the same frequency distribution of the outcome. Again, this is a good idea when a continuous outcome is skewed or a categorical outcome is imbalanced, but is unlikely to be problematic otherwise.

One other variation, _leave-one-out_ cross-validation, has _V_ equal to the size of the training set. This is a somewhat deprecated technique and may only be useful when the training set size is extremely small (Shao 1993).

### Monte Carlo Cross-Validation

_V_-fold cross-validation produced _V_ sets of splits with mutually exclusive assessment sets. Monte Carlo resampling produces splits that are likely to contain overlap. For each resample, a random sample is taken with $\pi$ proportion of the training set going into the analysis set and the remaining samples allocated to the assessment set. Like the previous procedure, a model is created on the analysis set and the assessment set is used to evaluate the model. This splitting procedure is conducted _B_ times and the average of the _B_ results are used to estimate future performance. _B_ is chosen to be large enough so that the average of the _B_ values has an acceptable amount of precision.

![](Image/v-fold-monte-carlo-cv.svg)

Figure shows Monte Carlo fold cross-validation with 10 resamples and π=0.90�=0.90. Note that, unlike 10-fold cross-validation, some of the same data points are used in different assessment sets.

MCCV can be more computationally efficient than other resampling methods since it does not require pre-defined subsets of the data. but the accuracy of the estimate obtained by MCCV can be sensitive to the quality of the random sampling. If the sampling is not representative of the overall dataset, the estimated performance of the model may not be accurate. It may not be appropriate for imbalanced datasets since the random sampling may result in unrepresentative training and testing sets.

MCCV requires multiple iterations to obtain a reliable estimate of a model's performance. Therefore, it can be computationally expensive when the number of iterations is large.

### The Bootstrap

A bootstrap resample of the data is defined to be a simple random sample that is the same size as the training set where the data are sampled _with replacement_ (Davison and Hinkley 1997) This means that when a bootstrap resample is created there is a 63.2% chance that any training set member is included in the bootstrap sample at least once. The bootstrap resample is used as the analysis set and the assessment set, sometimes known as the out-of-bag sample, consists of the members of the training set not included in the bootstrap sample. As before, bootstrap sampling is conducted _B_ times and the same modeling/evaluation procedure is followed to produce a bootstrap estimate of performance that is the mean of _B_ results.

![](Image/bootstrap.svg)

Figure shows an illustration of ten bootstrap samples created from a 20-sample data set. The colors show that several training set points are selected multiple times for the analysis set. The assessment set would consist of the rows that have no color.

The advantage of bootstrap is that it can provide a more accurate estimate of a model's performance by creating multiple datasets that are similar to the original dataset. This can reduce the effects of sampling variability and provide a more representative estimate of the model's performance on unseen data. Additionally, bootstrap can be used with small datasets or datasets where traditional cross-validation methods are not applicable.

However, the disadvantage of bootstrap is that it can result in overfitting since some samples may appear multiple times in the new datasets. Therefore, it's important to use a large number of iterations when performing bootstrap to ensure that the overfitting is properly accounted for. Additionally, bootstrap may not be appropriate for imbalanced datasets since it may result in unrepresentative training and testing sets.

In summary, bootstrap can provide a more accurate estimate of a model's performance by creating multiple datasets that are similar to the original dataset, but it can result in overfitting and may not be appropriate for imbalanced datasets. It's important to consider the advantages and disadvantages of bootstrap when choosing a resampling method for a given problem.

### Rolling Origin Forecasting

This procedure is specific to time-series data or any data set with a strong temporal component [(Hyndman and Athanasopoulos](http://otexts.org/fpp) 2013). If there are seasonal or other chronic trends in the data, random splitting of data between the analysis and assessment sets may disrupt the model’s ability to estimate these patterns

In this scheme, the first analysis set consists of the first _M_ training set points, assuming that the training set is ordered by time or other temporal component. The assessment set would consist of the next _N_ training set samples. The second resample keeps the data set sizes the same but increments the analysis set to use samples 2 through $M+1 while the assessment contains samples $M+2$ to $M+N+1$. The splitting scheme proceeds until there is no more data to produce the same data set sizes. Supposing that this results in _B_ splits of the data, the same process is used for modeling and evaluation and, in the end, there are _B_ estimates of performance generated from each of the assessment sets. A simple method for estimating performance is to again use simple averaging of these data. However, it should be understood that, since there is significant overlap in the rolling assessment sets, the _B_ samples themselves constitute a time-series and might also display seasonal or other temporal effects.

![](Image/resampling_rof.svg)

Figure shows this type of resampling where 10 data points are used for analysis and the subsequent two training set samples are used for assessment.

There are a number of variations of the procedure:
-   The analysis sets need not be the same size. It can cumulatively grow as the moving window proceeds along the training set. In other words, the first analysis set would contain _M_ data points, the second would contain _M_ + 1 and so on. This is the approach taken with the Chicago train data modeling and is described in Chapter [4](https://bookdown.org/max/FES/exploratory-visualizations.html#exploratory-visualizations).
-   The splitting procedure could _skip_ iterations to produce less resamples. For example in the Chicago data, there are daily measurements from 2001 to 2016. Incrementing by one day would produce an excessive value of _B_. For these data, 13 samples were skipped so that the splitting window moves in two-week blocks instead of by individual day.
-   If the training data are unevenly sampled, the same procedure can be used but moves over time increments rather than data set row increments. For example, the window could move over 12-hour periods for the analysis sets and 2-hour periods for the assessment sets.

This resampling method differs from the previous ones in at least two ways. The splits are not random and the assessment data set is not the remainder of the training set data once the analysis set was removed.

## Related Notes
* [[Data Splitting]]
* [[Bootstrapping]]

## References
* Davison, A, and D Hinkley. 1997. _Bootstrap Methods and Their Application_. Cambridge University Press.
* Hyndman, R, and G Athanasopoulos. 2013. _Forecasting: Principles and Practice_. OTexts. http://otexts.org/fpp