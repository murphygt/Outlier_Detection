# Outlier_Detection
## Detect Outliers
#### Have you ever trained a machine learning model on a real-world dataset? If yes, you’ll have likely come across outliers.

Outliers are those data points that are significantly different from the rest of the dataset. They are often abnormal observations that skew the data distribution, and arise due to inconsistent data entry, or erroneous observations.

To ensure that the trained model generalizes well to the valid range of test inputs, it’s important to detect and remove outliers.

In this guide, we’ll explore some statistical techniques that are widely used for outlier detection and removal.

## Why Should You Detect Outliers?
In the machine learning pipeline, data cleaning and preprocessing is an important step as it helps you better understand the data. During this step, you deal with missing values, detect outliers, and more.

As outliers are very different values—abnormally low or abnormally high—their presence can often skew the results of statistical analyses on the dataset. This could lead to less effective and less useful models.

But dealing with outliers often requires domain expertise, and none of the outlier detection techniques should be applied without understanding the data distribution and the use case.

For example, in a dataset of house prices, if you find a few houses priced at around $1.5 million—much higher than the median house price, they’re likely outliers. However, if the dataset contains a significantly large number of houses priced at $1 million and above—they may be indicative of an increasing trend in house prices. So it would be incorrect to label them all as outliers. In this case, you need some knowledge of the real estate domain.

The goal of outlier detection is to remove the points—which are truly outliers—so you can build a model that performs well on unseen test data. We’ll go over a few techniques that’ll help us detect outliers in data.

## How to Detect Outliers Using Standard Deviation
When the data, or certain features in the dataset, follow a normal distribution, you can use the standard deviation of the data, or the equivalent z-score to detect outliers.

In statistics, standard deviation measures the spread of data around the mean, and in essence, it captures how far away from the mean the data points are.

For data that is normally distributed, around 68.2% of the data will lie within one standard deviation from the mean. Close to 95.4% and 99.7% of the data lie within two and three standard deviations from the mean, respectively.

Let’s denote the standard deviation of the distribution by σ, and the mean by μ.

One approach to outlier detection is to set the lower limit to three standard deviations below the mean (μ - 3σ), and the upper limit to three standard deviations above the mean (μ + 3σ). Any data point that falls outside this range is detected as an outlier.

As 99.7% of the data typically lies within three standard deviations, the number of outliers will be close to 0.3% of the size of the dataset.

## How to Detect Outliers Using the Z-Score
Now let's explore the concept of the z-score. For a normal distribution with mean μ and standard deviation σ, the z-score for a value x in the dataset is given by:

z = (x - μ)/σ

From the above equation, we have the following:

When x = μ, the value of z-score is 0.
When x = μ ± 1, μ ± 2, or μ ± 3, the z-score is ± 1, ± 2, or ± 3, respectively.
Notice how this technique is equivalent to the scores based on standard deviation we had earlier. Under this transformation, all data points that lie below the lower limit, μ - 3*σ, now map to points that are less than -3 on the z-score scale.

Similarly, all points that lie above the upper limit, μ + 3*σ map to a value above 3 on the z-score scale. So [lower_limit, upper_limit] becomes [-3, 3].

Let’s use this technique on our dataset of scores.

You can filter the dataframe df_scores to retain points whose z-scores are in the range [-3, 3], as shown below. The filtered dataframe contains 198 records, as expected.

The methods involving standard deviation and z-scores can be used only when the data set, or the feature that you are examining, follows a normal distribution.

Next, we’ll discuss two outlier detection techniques that can be used independently of the data distribution.

## How to Detect Outliers Using the Interquartile Range (IQR)
In statistics, interquartile range or IQR is a quantity that measures the difference between the first and the third quartiles in a given dataset.

 - The first quartile is also called the one-fourth quartile, or the 25% quartile.
- If q25 is the first quartile, it means 25% of the points in the dataset have values less than q25.
- The third quartile is also called the three-fourth, or the 75% quartile.
- If q75 is the three-fourth quartile, 75% of the points have values less than q75.
Using the above notations, IQR = q75 - q25.

## How to Detect Outliers Using Percentile
In the previous section, we explored the concept of interquartile range, and its application to outlier detection. You can think of percentile as an extension to the interquartile range.

As discussed earlier, the interquartile range works by dropping all points that are outside the range [q25 - 1.5 IQR, q75 + 1.5 IQR] as outliers. But removing outliers this way may not be the most optimal choice when your observations have a wide distribution. And you may be discarding more points—than you actually should—as outliers.

Depending on the domain, you may want to widen the range of permissible values to estimate the outliers better. Next, let’s revisit the scores dataset, and use percentile to detect outliers.

## Conclusion
In this guide, we covered what outliers are, and why we need to detect them. We then went over the most common techniques for outlier detection.

Here’s a summary:

- If the data, or feature of interest is normally distributed, you may use standard deviation and z-score to label points that are farther than three standard deviations away from the mean as outliers.
- If the data is not normally distributed, you can use the interquartile range or percentage methods to detect outliers.

In addition, we discussed the best practices in outlier detection. When a large fraction of data is being labeled as outliers, they are not really outliers but can be attributed to a wider data distribution.

In applying all of the above techniques, it's also important to be aware of the current trend to identify how certain values are evolving, and check for permissible lower and upper limits using domain knowledge.


