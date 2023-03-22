**Title: How to Deal with Missing Value**
**Created: 22-03-2023**
**Tags:**

## Why there are missing value

* **By design**: Empty field is allowed, for example e-commerce product rating, not everyone has ever bought the item.
* **Bug in the system**: When data is being collected, it is possible that errors may occur, For example, if a software system is designed to collect data from sensors or other sources, and there is a bug in the system that causes it to miss or drop certain data points, then missing values may occur
* **Delay in data pipelines**

## How to deal with missing value

Before we try to do anything, we should see if theres any way to fill the data. If possible,
- **Wait for the data to be landed**: Maybe there is latency in data pipeline
- **Join with other data sources**: weneed to find out if the data can be filled by other data.

if not possible to fill the data,
- **Omission**: remove data points with missing values or remove features
- **Imputation**: infer missing values by leveraging our prior knowledge on existing data

### Data point omission

- **Missing value is a small percentage**
- **Missing data are random**: It means that missing value is not strongly correlated with certain group or features, and it won't change the distribution features.
- **Be careful when omitting data**: if there is pattern on missing data we should be careful about removing them, that could lead to intresting and meaningful business insights. For example for fraud detection problems it's possible that fraudsters refuse to report some of information and usually we dont have lots of label for fraudsters.

### Feature omission

A feature contain >70% missing value. 
Won't be helpful for modeling, If we try to replace the missing value with default value most of data point will have the same value, so this wont provide much information for model to learn.

### Imputation

if there is only small percentage of missing value and we don't want to remove them we can do imputation.
- Fill with default values
- Depends on data types
	- **Numerical variabel: mean, median or mode**
	- **Categorical variabel: frequent category**
- If the data type is **time series we can do interpolation**. for example, Missing temperature data for particular day it may reasonable to take an average between prior day and the next day.
- **Also we can train supervised model to fill missing values**. Note that this step itself is a sub machine learning project out of main machine learning project which will add complexity. so we need to consider the trade-off here it's feature important enough that we need to predict.

## Questions

1. **When should we use mean, median or mode to fill missing value?**

	The choice between using mean, median or mode to fill missing values depends on the type of variable and the distribution of the data. Here are some general guidelines:
	
	1.  Mean: Use mean imputation when the variable is continuous and normally distributed or when the distribution is roughly symmetrical. Mean imputation can be sensitive to outliers, so it is not recommended when the data contains extreme values.
	2.  Median: Use median imputation when the variable is continuous and the data contains outliers or the distribution is skewed. Median imputation is less sensitive to outliers than mean imputation.
	3.  Mode: Use mode imputation when the variable is categorical or when the variable is continuous but the data is discrete (e.g. counts). Mode imputation is appropriate for variables that have a clearly defined mode, or when the distribution is heavily skewed and the mode is a better representation of the central tendency than the mean or median.
	
	It is important to note that imputing missing values using mean, median, or mode can introduce bias and reduce the variance of the data. Therefore, it is important to consider other methods of imputation, such as regression or multiple imputation, to reduce the potential impact of imputing missing values on the analysis results. Additionally, it is important to carefully consider the underlying assumptions and characteristics of the data before deciding on the imputation method to use.

2. **When we need to use regression imputation?**
	
	Regression imputation: This method is appropriate when the variable with missing data has a strong correlation with other variables in the dataset. Regression imputation involves using a regression model to estimate the missing values based on the values of other variables in the dataset. This method can be more accurate than simpler imputation methods (such as mean or median imputation) when the relationship between the variables is complex.



## Related Notes

## References
