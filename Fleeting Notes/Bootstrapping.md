**Title: Bootstrapping**
**Created: 18-03-2023**
**Tags:**

## What is Bootstrapping?

Bootstrapping is a statistical procedure that resamples a single data set to create many simulated samples. This process allows for the calculation of standard errors, confidence intervals, and hypothesis testing.

A bootstrapping approach is an extremely useful alternative to the traditional method of hypothesis testing, as it’s fairly simple and it mitigates some of the pitfalls encountered within the traditional approach. 

Statistical inference generally relies on the sampling distribution and the [standard error](https://builtin.com/data-science/difference-between-standard-deviation-standard-error) of the feature of interest. The traditional approach, or large sample approach, draws one sample of size _n_ from the population, and that sample is used to calculate population estimates to then make inferences on. In reality, only one sample has been observed.

> “Bootstrapping is a statistical procedure that resamples a single data set to create many simulated samples.”

Bootstrapping is a useful technique when the assumptions of traditional statistical tests are not met or when your sample size is small. **It can also be used to estimate the bias and variance of a model, compare different models, or validate the performance of a model**.

## How Bootstrapping Statistics Works?

![](Image/bootstrapping_resample.jpeg)
In the bootstrapping approach, a sample of size _n_ is drawn from the population. Let’s call this sample _S_. Then, rather than using theory to determine all possible estimates, the sampling distribution is created by resampling observations with replacement from _S_ _m_ times, with each resampled set having _n_ observations. Now, if sampled appropriately, _S_ should be representative of the population. Therefore, by resampling _S_ _m_ times with replacement, it would be as if _m_ samples were drawn from the original population, and the estimates derived would be representative of the theoretical distribution under the traditional approach. 

Increasing the number of resamples, _m_, will not increase the amount of information in the data. That is, resampling the original set 100,000 times is not more useful than resampling it 1,000 times. The amount of information within the set is dependent on the sample size, _n_, which will remain constant throughout each resample. The benefit of more resamples, then, is to derive a better estimate of the sampling distribution.

## Advantages of Bootstrapping Statistics

Now that we understand the bootstrapping approach, it must be noted that the results derived are basically identical to those of the traditional approach. Additionally, the bootstrapping approach will always work because it doesn’t assume any underlying distribution of the data.

This contrasts with the traditional approach which theoretically assumes that the data are [normally distributed](https://builtin.com/data-science/empirical-rule). Knowing how the bootstrapping approach works, you might wonder, does the bootstrapping approach rely too much on the observed data? This is a good question, given that the resamples are derived from the initial sample. And because of this, it’s logical to assume that an outlier will skew the estimates from the resamples. 

> “The advantages of bootstrapping are that it is a straightforward way to derive the estimates of standard errors and confidence intervals, and it is convenient since it avoids the cost of repeating the experiment to get other groups of sampled data.”

While this is true, if the traditional approach is considered, an outlier within the data set will also skew the mean and inflate the standard error of the estimate. While it might be tempting to think that an outlier can show up multiple times within the resampled data and skew the results and thus, making the traditional approach better, the bootstrapping approach relies as much on the data as the traditional approach. 

“The advantages of bootstrapping are that it is a straightforward way to derive the estimates of standard errors and confidence intervals, and it is convenient since it avoids the cost of repeating the experiment to get other groups of sampled data. Although it is impossible to know the true confidence interval for most problems, bootstrapping is asymptotically consistent and more accurate than using the standard intervals obtained using sample variance and the assumption of normality,” according to author Graysen Cline in their [book](https://www.amazon.com/Nonparametric-Statistical-Methods-Using-Graysen/dp/1788820797), _Nonparametric Statistical Methods Using R._

Both approaches require the use of appropriately drawn samples to make inferences about populations. However, the biggest difference between these two methods is the mechanics behind estimating the sampling distribution. The traditional procedure requires one to have a test statistic that satisfies particular assumptions in order to achieve valid results, and this is largely dependent on the experimental design. The traditional approach also uses theory to tell what the sampling distribution should look like, but the results fall apart if the assumptions of the theory are not met.

The bootstrapping method, on the other hand, takes the original sample data and then resamples it to create many [simulated] samples. This approach doesn’t rely on theory since the sampling distribution can be observed, and you don’t have to worry about any assumptions. This technique allows for accurate estimates of statistics, which is crucial when using data to make decisions.

## Bootstrapping Example

Let’s say you wanted to know how many shoes you have. How would you find out? You would probably just count them—finding out the answer to this question does not require bootstrapping. But what if you wanted to know the average number of shoes that everyone in your office owns? 

You work for a big technology company, so your office is large. After speaking to HR, you’re able to conclude that there are 1,000 people total in the building and 200 people on your floor. This is starting to feel a little more feasible to you, and you’re thinking that you could theoretically ask each person how many shoes they have. This may still be impractical and time-consuming, though. Instead, you decide to bootstrap it. 

On the first day you survey 50 people (without replacement) and record how many shoes each person has. This is your dataset. Instead of repeating this procedure every day, you take those 50 data points and create a whole lot of bootstrapped samples from them. Each bag ([one bootstrapped sample set](https://en.wikipedia.org/wiki/Bootstrap_aggregating)) has 50 randomly chosen samples, with replacement. Using replacement means that any of them are counted more than once and some are never counted at all. For each of these bags, you measure the mean number of shoes owned. 

After you have done this 100 times, you have 100 estimates of the average number of shoes your co-workers own. You can use them to calculate confidence intervals—and be able to conclude something like, “It is 95% likely that the average number of shoes owned by people in this company is between 6 and 10.”

## Implementing Bootstrapping in python

```python
def bootstrapped_conf_interval(data, metric, num_runs=1000, conf=.95):

   # purpose: Calculate confidence interval for model performance (metric)

# Parameters
#  —————-

#  data: list of data points in a format that is acceptable to get_metric

#  metric: options include ‘accuracy’, ‘precision’,’recall’ and ‘f1-score’

#  conf: how certain you want to be about the range of possible values of your metrc

#  num_runs:  int designating how many bootstrapped samples of data you would like

# Returns

#  ———-

# Confidence tuple with floats as entries ex: (.2,.3)

#    “””

    results = []

    # get num _runs bootstrapped samples of unlabeled and labeled data

    for i in range(num_runs):

        bootstrapped_data = np.random.choice(data, len(data))

        results.append(get_metric(bootstrapped_data, metric))

    results.sort()

    bootstrapped_mean = sum(results) / float(len(results))

    x_bar = get_metric(data, metric)

    # how much of the measured metrics do you want to cut off on either end

    left_index = int(num_runs * (1 – conf) / 2)

    # deviations from bootstrapped means

    delta_interval = [results[left_index] – bootstrapped_mean,

                      results[-left_index] – bootstrapped_mean]

    # deviations from mean from actual sample, not bootstrapped sample

    interval = [delta_interval[0] + x_bar, delta_interval[1] + x_bar]

    return interval
```

## Questions

1. **Give me use case of bootstrapping in machine learning.**
	Bootstrapping is a statistical technique that involves resampling data with replacement to estimate the uncertainty of a statistic. In machine learning, bootstrapping can be used in various ways, including:
	
	1.  Model evaluation: Bootstrapping can be used to evaluate the performance of a model. For example, the bootstrap method can be used to estimate the mean and variance of a model's accuracy or error rate by Bootstrap resampling the test set and calculate the accuracy.
	2.  Feature selection: Bootstrapping can also be used to perform feature selection. By repeatedly resampling the data and selecting different subsets of features, we can estimate the stability of each feature and identify the most important ones.
	3.  Ensemble methods: Bootstrapping is a key component of many ensemble methods, such as bagging and random forests. In these methods, multiple models are trained on different subsets of the data to reduce overfitting and improve generalization performance.
	4.  Hypothesis testing: Bootstrapping can be used to test the significance of a hypothesis. By resampling the data and calculating the test statistic many times, we can estimate the distribution of the statistic under the null hypothesis and determine the p-value.
	
	Overall, bootstrapping is a useful technique in machine learning for estimating uncertainties and improving model performance.

## Related Notes
* [[Resampling]]

## References
* [Bootstrapping Statistic](https://builtin.com/data-science/bootstrapping-statistics)
* [What is Bootstrapping](https://www.mastersindatascience.org/learning/machine-learning-algorithms/bootstrapping/)



