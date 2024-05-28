See:
* [[DS - What is Data Science?]]
* [[ML - Machine Learning Basics]]
* [[ML - Supervised Learning]]
* [[Py - Math (Hypothesis Testing)]]
* [[Py - Math (Confidence Intervals)]]
* [[Py - Pandas (Methods)]]
* [[Py - Numpy (Methods)]]
Resources
* 

---
# Business Metrics

## Revenue, Cost of goods sold & Margin
* **Revenue** -- the money generated from normal business operations
	* Formula: $$Reven\!ue = (Number\;of\;Units\;So\,ld * Unit\;Price)$$
* **Cost of Goods Sold (COGS)** --  direct (and indirect) costs of producing the goods sold by a company
	* Formula: $$COGS = Starting\;ivemt\!or\!y + P − Ending \;ivemt\!or\!y$$
* **Gross Profit** --  the profit made after deducting the costs associated with producing and selling its products or the costs associated with its services.
	* Formula: $$ Gross\;profit = reven\!ue -  COGS$$
* **Gross Margin** -- the ratio of gross profit to revenue
	* Formula: $$Gross\;Profit\;Margi\!n = (Gross\;profit)/(Net\;sales) * 100$$

## Operating Expenses and Operating Profit
* **Operating Expenses** -- includes all expenses related to the company's business operations such as: salaries, rent, utilities, etc
	* Profit Margin
	* Operating Profit Margin

## Operating Profit
* Operating Profit -- net income from its core operations after accounting for operating expenses
	* **Operating Loss** -- occurs when the operating profit is less than 0 
	* Formula: $$Operating\;profit = Gross\;profit - Operating\;exp\!enses$$
## Operating Profit Margin
* Operating Profit Margin -- the share of the revenue that remains in the company after deducting the cost of goods sold, salaries, rent, marketing, and other expenses related to the main activities
	* Formula: $$Operating\;Profit\;Margi\!n = (Operating\;Profit)/(Revenv\!ue) * 100$$

## Net Profit
* **Net Profit** -- the amount of money a business earns after deducting all operating, interest, and tax expenses over a given period of time.
	* If **Net Profit** is less than 0 (negative), then the company experienced a **Net Loss** (failed to make money)
	* Formula: $$Net\;Profit=Operating\;Profit − Taxes\;and\;loans$$

## Return on Investment (ROI)
* **Return on Investment (ROI)** -- evaluates the efficiency or [profitability](https://www.investopedia.com/terms/p/profitabilityratios.asp) of an investment or compare the efficiency of a number of different investments
	* Formula: $$ ROI = (Net\;Profit - Investment) / (Investment)$$
	* Example: Entrepreneur Aaron sold his apartment and invested $10 million in launching a web design studio. For the first year, the studio earned $2.5 million in net profit. What is the ROI equal to? $$ ROI = (2.5 - 10) / (2.5) = -75\%$$

## Conversion Rate (CVR)
* **Conversion Rate** -- measures the percentage of users who completed a targeted action
	* Formula: $$ CVR = (Num\;of\;Positive) / (Total\;Num)$$
	* Example: The Download-Launch mobile app was installed by 22,755 people, and 555 of them bought the paid version. What is the mobile app conversion rate? $$ CVR = (555)/(22,755) = 2.439\%$$
	* Example: Conversion for the online smartphone store Ph0nz.com is equal to 2.154%. There were 21,824 visitors. How many customers were there? $$ (2.154\%) / 100 * 21,824 = 470$$
	* Example: The conversion rate of the online game World of Dump Trucks is 1.821%, the number of buyers is 712. How many visitors were there? $$  712 / (1.821\%) / 100 = 39,099 $$

## Funnels 
* Funnel -- a model of the customer journey progresses toward purchase
* Funnels display:
	1) The path a user takes to buy a product
	2) The proportion of people who reach each stage
* Calculating a Funnel
	1) Find the number of users at each stage
	2) Calculate the Conversion Rate (CVR) at each stage from the total number of users

* Example: 
	* Starting size = 10,000
	![[funnel-example.png]]
	
| Stage         | Quantity | Total Conversion | Conversion to Next Stage |
| ------------- | -------- | ---------------- | ------------------------ |
| Main Page     | 10,000   | 100%             | 100%                     |
| Product Page  | 8,000    | 80%              | 80%                      |
| Added to Cart | 3,000    | 30%              | 38%                      |
| Checkout Page | 1,000    | 10%              | 33%                      |
| Order         | 100      | 1%               | 10%                      |

## Online vs Offline Metrics
* Metric Decomposition -- breaks down metrics into components in order to identify the steps that impact the metrics of interest
	* Example of Metric Decomposition
		![[metric-decomposition-example.png]]
* Evaluation Metrics:
	* **Target Metric** -- a specific performance measure that the system aims to optimize or evaluate
	* **Online Metric** -- metrics evaluated in a live system with real-time user interactions
		* Example: Users
	* **Offline Metrics** -- metrics evaluated from historical data
		* Example: accuracy, MSE


---
---

# Implementing New Functionality
## Basics: A/B Testing (Split Testing)
* **A/B Testing** (**Split Testing**) -- a technique for hypothesis testing that helps to monitor the impact of service or product changes on the users
* How A/B Testing Works:
	* Population is split into a Control Group (A) & Treatment Group (B)
		* Group A -- receives no changes
		* Group B -- receives the new version (the one to be tested)
	* The test runs for a fixed period, while both groups are observed
	* The data is analyzed
		* If the key metric in the treatment group improves, compared to the control group, the metric is implemented
		![[A-B-testing-example.png]]
	
* Factors to consider when comparing metrics
	* Is the difference between the metrics significant or insignificant?
		* If the difference is insignificant, how can cases where it is by chance be identified
	* Is the experiment too long or too short?
		* If the experiment is too long, it slows down the implementation of new functionality. 
		* If an experiment is too short, it can fail to provide reliable results
	* The comparison of the mean values of the metrics doesn't take the dispersion into account. 


## A/B Testing Size & Duration
* Identifying the correct duration for A/B testing is important
	* If the experiment is too long, it slows down the implementation of new functionality. 
	* If an experiment is too short, it can fail to provide reliable results
* A/B Testing tends to suffer from a "Peeking Problem"
	* Peeking Problem -- the overall result is distorted when new data is added at the beginning of the experiment
		* Even a small fragment of new data is LARGE compared to data accumulated, leading to large dispersion, and statistical significance achieved in a short time
		* This results in the the p-value can be incorrectly reached, and the the null hypothesis can be accidentally rejected
* Solving Peeking Problem
	* Calculate the correct duration for the A/B Test 
		* Use a calculator -- [A/B & Split Test Duration Calculator](https://vwo.com/tools/ab-test-duration-calculator/)


## Comparing the Means of A/B Test
* **One-sided Hypotheses** -- used when interested in deviation in only one direction 
	- e.g., improvement
- **T-tests** -- used for comparing means if data is normally distributed
    - Determines if the difference between means is significant
* Mean Metric Analysis -- the mean value is used to assess performance of A/B tests.
* Randomness and Error -- measurement results have random error due to variability. 
	* Statistical methods estimate true values despite this uncertainty.
* Two Types of Errors in Hypothesis Testing
	* Type I Error -- the null hypothesis ($H_0$) is correct but it is rejected (false positive result) 
	* Type II Error -- the null hypothesis ($H_0$) is wrong but it is accepted (false negative result)
		![[hypothesis-type-errors.png]]
* **Significance Level (`α`) and `p-value`**:
	* `p-value` (probability value) – the probability of observing results more extreme than the observed, assuming $H_0$ is true.
	* Significance level (`α`) sets the threshold for rejecting H₀ (commonly 5% or 1%).
* Comparing the  `α` and `p-value`
	* If `p-value > α` -- Fail to reject  $H_0$
	- If `p-value ≤ α` -- Reject $H_0$ (suggests a significant difference)
```Python
import pandas as pd
from scipy import stats as st

# Average purchase amount BEFORE implementation
sample_before = pd.Series([
    436, 397, 433, 412, 367, 353, 440, 375, 414, 410, 434, 356, 377, 403, 434,
    377, 437, 383, 388, 412, 350, 392, 354, 362, 392, 441, 371, 350, 364, 449,
    413, 401, 382, 445, 366, 435, 442, 413, 386, 390, 350, 364, 418, 369, 369,
    368, 429, 388, 397, 393, 373, 438, 385, 365, 447, 408, 379, 411, 358, 368, 
    442, 366, 431, 400, 449, 422, 423, 427, 361, 354])

# Average purchase amount AFTER implementation
sample_after = pd.Series([
    439, 518, 452, 505, 493, 470, 498, 442, 497, 423, 524, 442, 459, 452, 463,
    488, 497, 500, 476, 501, 456, 425, 438, 435, 516, 453, 505, 441, 477, 469,
    497, 502, 442, 449, 465, 429, 442, 472, 466, 431, 490, 475, 447, 435, 482, 
    434, 525, 510, 494, 493, 495, 499, 455, 464, 509, 432, 476, 438, 512, 423,
    428, 499, 492, 493, 467, 493, 468, 420, 513, 427])

print("Mean before:", sample_before.mean())
print("Mean after:", sample_after.mean())

results = st.ttest_ind(sample_before, sample_after)
alpha = 0.05 # critical level of significance

# one-tailed test: p-value will be half as large
pvalue = results.pvalue / 2

print('p-value: ', pvalue)
if pvalue < alpha:
  print("Reject null hypothesis: average purchase amount is likely to increase")
else:
  print("Failed to reject null hypothesis: average purchase amount is unlikely     to increase")
```

```Results
Mean before: 396.9714285714286
Mean after: 470.5285714285714
p-value:  3.090979110409132e-29
Reject null hypothesis: average purchase amount is likely to increase
```

## Confidence Interval 
* **Confidence Interval (CI)** -- the probability that a population parameter will fall between a set of values for a certain proportion of times
	- Common Intervals: 95%, 97.5% or 99% of expected observations
- Calculating the Confidence Interval
	- Formula: 
		- $μ$ -- population mean
		- $σ^2$ -- population variance
		- $X̄$ -- sample mean $$ P(X̄ + t(LP) * SEM(X̄) < mu < X̄ + t(UP) * SEM(X̄) $$
	- Step-by-Step
		1. Calculate the Sample Mean 
			* The mean of the distribution of all sample means will be equal to the true mean of the population $$X ~ N (mu, (sigma^2)/(n))$$
		2. Calculate the Standard Error of the Mean (SEM)
			* The larger the sample size, the smaller the standard error $$SEM(X)=sigma/sqrt(n)$$
		3. Standardize the normal distribution 
			* Make the standard deviation 1 and mean 0 $$ (X - mu) /( SEM(X)) ~ N(0,1) $$
		4. Take the LP (Lower Percentile) & UP (Upper Percentile)
			* $t(LP)$ -- Student T's Lower Percentile
			* $t(UP)$ -- Student T's Upper Percentile


## Bootstrapping
* What is Bootstrapping? 
	* Bootstrapping -- a statistical resampling technique used to estimate the distribution of a sample statistic (such as the mean) by repeatedly sampling from the original dataset with replacement.
		![[bootstrapping-example.png]]
	
* When is Bootstrapping useful?
	* Observations are not described by normal distribution (works for any distribution of data)
	* There are no statistical tests for the target value


## Bootstrapping for Confidence Interval
* Bootstrapping can be used to assess the confidence interval 
	* Samples should be randomly generated with replacement
```Python
from numpy.random import RandomState

data = pd.Series([ 10.7, 9.58, 7.74, 8.3 , 11.82, 9.74, 10.18, 8.43, 8.71, 6.84, 9.26, 11.61, 11.08, 8.94, 8.44, 10.41, 9.36, 10.85, 10.41, 8.37, 8.99, 10.17, 7.78, 10.79, 10.61, 10.87, 7.43, 8.44, 9.44, 8.26, 7.98, 11.27, 11.61, 9.84])

# Creating a random state to change with each call
state = RandomState(12345) 

for i in range(5):
	# Extract 1 random element from sample with replacement
	subsample = data.sample(frac=1, replace=True random_state=state)
	print(subsample.quartile(q=0.90))
```

```Python
import pandas as pd
import numpy as np

data = pd.Series([
    10.7, 9.58, 7.74, 8.3, 11.82, 9.74, 10.18, 8.43, 8.71, 6.84, 9.26, 11.61,
    11.08, 8.94, 8.44, 10.41, 9.36, 10.85, 10.41, 8.37, 8.99, 10.17, 7.78, 
    10.79, 10.61, 10.87, 7.43, 8.44, 9.44, 8.26, 7.98, 11.27, 11.61])

# Creating a random state to change with each call
state = np.random.RandomState(12345)

for i in range(10):
    subsample = data.sample(frac=1, replace=True, random_state=state)
    print(subsample.quantile(q=.99))
```

```Results
19.192200000000003
20.85
19.20660000000001
19.028400000000012
19.42440000000001
19.42440000000001
20.85
19.42440000000001
19.42440000000001
19.19
```

```Python
import pandas as pd
import numpy as np

data = pd.Series([
    10.7 ,  9.58,  7.74,  8.3 , 11.82,  9.74, 10.18, 8.43, 8.71, 6.84, 9.26, 
    11.61, 11.08,  8.94,  8.44, 10.41,  9.36, 10.85, 10.41, 8.37, 8.99, 10.17, 
    7.78, 10.79, 10.61, 10.87,  7.43, 8.44,  9.44, 8.26, 7.98, 11.27, 11.61])

# Creating a random state to change with each call
state = np.random.RandomState(12345)

# Store the 99% quantile values to the values variable
values = []
for i in range(1000):
    subsample = data.sample(frac=1, replace=True, random_state=state)
    values.append(subsample.quantile(0.99)) # Find 99% percentile

# Change the data type of values
values = pd.Series(values)

lower = values.quantile(0.05) # Find the 5% quantile
upper = values.quantile(0.95) # Find the 95% quantile

print(lower) # 19.01140000000002
print(upper) # 20.85
```

## Bootstrapping for A/B Test Analysis
* Bootstrapping can be used to analyze results of A/B Testing
* Process
	* Calculate the difference between the two groups' average (using the observations)
	* Assume that the groups are equal (so observations from both groups can be seen as one sample)
	* Concatenate the observations into one sample
	* Create the subsample by simulating many experiments by drawing two samples (with replacement) from the combined observations (one to represent group A and one to represent group B)
	* Create two subsamples ($A_i$ and $B_i$)
		* $A_i$ -- the sample for group A for the $i^th$ experiment (its size should be equal to the size of the original sample for group A)
		* $B_i$ -- the sample for group B for the $i^th$ experiment (its size should be equal to the size of the original sample for group B)
		* $D_i$ -- the difference for the $i^th$ iteration
	* Calculate the `p-value`, which is the number of times when $D_i$ was no less than $D$ to the number of simulated experiments $$pvalue = P {D_i >= D} = (NUM \;OF\;SIMULATED\;EXPIREMENTS\;WHEN\;D_i >= D)/(NUMBER\;OF\;SIMULATED\;EXPERIMENTS)$$
	* Determine if p-value is less or more than threshold ($alpha$)
```Python

import pandas as pd
import numpy as np

# data for control group A
samples_A = pd.Series([
	98.24, 97.77, 95.56, 99.49, 101.4, 105.35, 95.83, 93.02, 101.37, 95.66, 
	98.34, 100.75, 104.93, 97.00, 95.46, 100.03, 102.34, 98.23, 97.05, 97.76,  
	98.63, 98.82, 99.51, 99.31, 98.58, 96.84, 93.71, 101.38, 100.6, 103.68, 
	104.78, 101.51, 100.89, 102.27,  99.87, 94.83, 95.95, 105.2, 97.00, 95.54, 
	98.38, 99.81, 103.34, 101.14, 102.19,  94.77,  94.74,  99.56, 102.00])

# data for treatment group B
samples_B = pd.Series([
    101.67, 102.27, 97.01, 103.46, 100.76, 101.19, 99.11, 97.59, 101.01, 
    101.45, 94.8, 101.55, 96.38, 99.03, 102.83, 97.32, 98.25, 97.17, 101.1,
    102.57, 104.59, 105.63, 98.93, 103.87, 98.48, 101.14, 102.24, 98.55, 105.61, 
    100.06,  99.00, 102.53, 101.56, 102.68, 103.26, 96.62, 99.48, 107.6 ,  
    99.87, 103.58, 105.05, 105.69,  94.52, 99.51, 99.81, 99.44, 97.35,])

# actual difference between the means in the groups
AB_difference = samples_B.mean() - samples_A.mean()
print("Difference between average purchase amounts:", AB_difference)

alpha = 0.05 # Determine the threshold
state = np.random.RandomState(12345)
bootstrap_samples = 1000 # Determine number of iterations
count = 0 

# For each iteration:
for i in range(bootstrap_samples):
    # Concatenate the two samples
    united_samples = pd.concat([samples_A, samples_B])
    
    # Create subsample
    subsample = united_samples.sample(frac=1, replace=True, random_state=state)
    
    # Split subsample in half to create Ai and Bi
    subsample_A = subsample[:len(samples_A)]
    subsample_B = subsample[len(samples_A):]
    
    # Find the difference between the sammple means
    bootstrap_difference = subsample_B.mean() - subsample_A.mean()
    
    # Compare the difference between the sample mean and the actual mean; if the       difference is not less than actual difference, add "1" to the  counter
    if bootstrap_difference >= AB_difference:
        count += 1

# p-value is equal to the percentage of excess values
pvalue = 1. * count / bootstrap_samples
print('p-value =', pvalue)

if pvalue < alpha:
    print("Reject null hypothesis: average purchase amount is likely to              increase")
else:
    print("Failed to reject null hypothesis: average purchase amount is unlikely     to increase")
```

```Results
Difference between average purchase amounts: 0.7682000000000357
p-value = 0.034
Reject null hypothesis: average purchase amount is likely to increase
```

## Bootstrapping for Models
* Bootstrapping can be used to assess the confidence intervals in ML models
* Process
	* 
* Example
	* The model for predicting the probability of lesson attendance is already trained. Predictions can be found in file `eng_probabilities.csv`, and correct answers are in `eng_target.csv.`
	* One lesson costs 10 dollars. Up to 10 lessons can be scheduled per day. The current daily revenue is 50 dollars (half of the students cancel the lesson).
	* The average daily number of applications received is 25.
	* Target revenue for implementing the new system is 75 dollars. Its probability should be at least 99%.
```Python
import pandas as pd
import numpy as np

# Take '0' index to convert data to pd.Series
target = pd.read_csv('/datasets/eng_target.csv')['0']
probabilities = pd.read_csv('/datasets/eng_probabilites.csv')['0']

# Calculate revenue
def revenue(target, probabilities, count):
    probs_sorted = probabilities.sort_values(ascending=False)
    selected = target[probs_sorted.index][:count]
    return 10 * selected.sum()

# Creating a random state to change with each call
state = np.random.RandomState(12345)    
values = [] # Store values
for i in range(1000):
    target_subsample = target.sample(n=25, replace=True, random_state=state)
    probs_subsample = probabilities[target_subsample.index]
    values.append(revenue(target_subsample, probs_subsample, 10))
    
values = pd.Series(values)
lower = values.quantile(0.01)

mean = values.mean()
print("Average revenue:", mean)
print("1% quantile:", lower)
```