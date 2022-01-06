## Research Questions
1. Is there any difference between the average morning and afternoon trip durations?
2. Is there any difference in the average trip duration between the morning, afternoon, evening, and night?
3. Is there any interaction between PUborough(pick-up point) and TimeOfDay when considering average trip duration?
4. How can one increase tip amounts?
# Data-Analysis
Data Description : Vendor, RateCode, PUborough, DOborough, passenger_count, trip_distance, TimeOfDay, trip_duration,	paymentMethod, fare_amount, extra, mta_tax,	tip_amount,	tolls_amount, improvement_surcharge, total_amount.
## Basic EDA
Let us look into the trip duration of this dataset.
The variable Trip duration is right skewed with very long tail. we will therefore take the log to normalise the Trip Duration distribution.
![1](https://user-images.githubusercontent.com/41823726/147149032-c5cea79e-78b1-4dc9-bbfe-7936976441ee.png)

Let us check the new plot. The log of the trip duration is normally distributed, although with a high peak.
![2](https://user-images.githubusercontent.com/41823726/147149135-a03638cb-7b95-46f6-bdf1-5a2a6f54ec58.png)

Let us see how the tip amounts and total amounts are spread across the vendors 
![3](https://user-images.githubusercontent.com/41823726/147149372-79eb7fc3-3d3c-418c-b328-a77de4f984ed.png)
We can see that among the two types of vendors, VeriFone Inc has received the most tips and has earned few highest Total Amounts compared to Creative Mobile Technologies LLC.

## Analysis 1
**Null hypothesis:** There is no difference between the average morning and afternoon trip durations.

**Alternate Hypothesis:** There is a difference between the average morning and afternoon trip duration.

The independent sample t-test is the appropriate statistic to apply here. The independent sample t-test (also known as the two-sample t-test) can be used to evaluate whether or not two groups unknown population means are equal. If the data values are independent, randomly picked from two normal populations, and the two independent groups have equal variances, this test can be employed. The dataset is made up of trip duration data collected from the New York City Taxi and Limousine Commission in the morning and afternoon.

The current study aims to discover if there was any variation in the duration of trips that took place in the afternoon and morning. There were some outliers in the sample. The Anderson-Darling normality test revealed no group normality,  Levene's test revealed heterogeneity of variance. For 32970 samples, the mean trip duration in the Afternoon was 999.438 (sd = 829.559). For 23743 samples, the mean travel duration in the morning was 836. (sd = 672.425). According to a Welch's independent t-test, t(55926.15) = 25.89833, p 0.0001,d = 1.67, the mean difference in trip duration between morning and afternoon in the collected sample was statistically significant,  with afternoon trip tending to be longer than morning trip .

**Tests applied: Outliers check, Anderson-Darling Normality test for Normality check, levene Test for variance, Independent T_test, Cohens_d.**


## Analysis 2

**Null hypothesis**: There is no difference in the average trip duration between the morning, afternoon, evening, and night.

**Alternate Hypothesis**: There is difference in the average trip duration between the morning, afternoon, evening, and night

The suitable statistic to be used here is one-way ANOVA test. The one-way ANOVA ("analysis of variance") compares the means of two or more independent groups in order to determine whether there is statistical evidence that the associated population means are significantly different. 

The current study seeks to determine whether or not there were any differences in the trip durations at different times of the day. The times in a day are divided into four categories: Morning (n = 32970), Afternoon (n = 32919	), Evening (n = 23743	) and Night (n = 10368). The dataset had outliers. An Anderson-Darling normality test  demonstrated no normality by group and levene's test showed heterogenity of variance. A one-way ANOVA test revealed that the trip duration were significantly different between the four groups, F(3, 99996) = 518.205, p = 0 (p < 0.05) , $\eta^2$ = 0.015. The trip duration in the afternoon (M=999.438, SD=829.559) was higher than the trip duration in the evening (M=868., SD=624.), morning (M=835.815, SD=672.425) and night (M=725.351, SD=519.064). Tukey post-hoc analysis revealed that the differences of the trip duration exists between Afternoon, evening(-131.93295, 95% CI[-145.94824, -117.91765]), Afternoon Morning(-163.62393, 95% CI[ -178.93455, -148.31332]),  Afternoon Night (-274.08702, 95% CI[-294.34080, -253.83325]), Evening Morning(-31.69099 95% CI[-47.00657, -16.37541]), Evening night (-142.15408 95% CI[-162.41161, -121.89655]), and Morning Night (-110.46309 95% CI[-131.63746, -89.28872]) with p < .05. Hence , the null hypothesis was rejected.

**Tests applied: Outliers check, Anderson-Darling Normality test for Normality check, levene Test for variance, One-way ANOVA, tukey_hsd.**

## Analysis 3

Let's determine wether or not there an interaction between PUborough and TimeOfDay when considering average trip duration. The times in a day are divided into
four categories: Morning (n = 32970), Afternoon (n = 32919 ), Evening (n = 23743 ) and Night (n = 10368). 

![image](https://user-images.githubusercontent.com/41823726/148461467-23f33f03-ac4d-4832-9f9b-b37b904eaaa3.png)


The dataset had outliers. An Anderson Darling test demonstrated no normality by group and levene's test showed heterogenity of variance. The ANOVA table indicates that the interaction effect is significant,with p < .05.Hence we reject null hypothesis. An interracted plot was plotted for the available data. All four lines have shown increase for Broklynn, Manhattan, Queens and Staten Island. Further analysis of main effect for "PUBorough" was performed with statistical significance receiving a tukey adjustment. According to ANOVA test there was a  statistically significant interaction effect between the TimeOfDay and PUborough, F(11, 99980) = 149.294, $\eta^2$ = 0.016, p < 0.05. Consequently, an analysis of main effects  was performed with statistical significance receiving  a Bonferroni adjustment. There is a significance difference between Afternoon, PUborough F(4,99980)=2759. p<0.05, Evening, PUborough F(4,99980)=979. p<0.05, Morning, PUborough F(5,99980)=990. p<0.05, Night, PUborough F(3,99980)=72.2, p<0.05. All pairwise comparisions were analysed between the different levels, there were significant difference between PUborough and TimeOfDay when considering average trip duration.

**Tests applied: Outliers check, Anderson-Darling Normality test for Normality check, levene Test for variance, Two-way ANOVA, emmeans test.**

## Analysis 4
**Tests applied : Linear Regression, Lasso Regression, Correlation**

When looking at the estimates, positive estimated variables like the pick-up point in Queens, the drop-off point in Manhattan, credit card payment, and lastly the total amount(higher estimate of all), made an impact on the tips amount. So, in order for the taxi driver to make more tips, he should concentrate more on picking up customers from Queens, customers travelling to Manhattan, customers who like to pay with a credit card, and finally, if he can earn a higher total amount. This is only possible if the trip distance or duration is long, resulting in a higher total amount of money. This maximization of tips are subjective to this dataset.

we shall set up the data frame to show the raw correlations in a table. The highest correlation is sorted first in the data set. Only variables above a certain significance level threshold are selected in order to limit the sheer number of variables (without having to manually pick and choose). As a starting point, it's set at 0.5. After the table is created, it will return the correlation matrix chart below, which has been filtered out. Only correlations with a significant enough level of significance will have a coloured circle. If there are still a lot of variables, this helps to cut out the noise even further. After some feature engineering, the 'corr simple' function can be used again and again, or with varying significance levels.data quickly and to see only the information that is relevant. With more variables, it may be essential to experiment with alternative significance thresholds and/or employ additional feature engineering to limit the number of associated variables before re-running the function until the results are understandable and helpful.The correlation plot also shows the impact of total_amount on tip_amount.
![image](https://user-images.githubusercontent.com/41823726/148463384-6bd72df1-278a-4e29-899c-9c69b0cf0390.png)

