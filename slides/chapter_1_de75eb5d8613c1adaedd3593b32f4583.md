---
title: Insert title here
key: de75eb5d8613c1adaedd3593b32f4583

---
## Hypothesis Testing

```yaml
type: "TitleSlide"
key: "c9b30d949b"
```

`@lower_third`

name: Khac Phuoc Le
title: Data Scientist


`@script`
Welcome to the second Chapter!


---
## Interview Scenario

```yaml
type: "FullSlide"
key: "70c204aea9"
```

`@part1`
- **Marketing department situation**: {{1}} 

 - Idea for new marketing strategy: **new coupon** {{1}} 
 - **Goal**: increase traffic onto website {{1}} 

- **Question** from the head of marketing: {{2}} 
 - **How do we know that the new strategy works?** {{2}}  

- **Answer**: {{3}}
 - Using statistical testing or **Hypothesis testing** (here also called **A/B Testing**) {{3}}


`@script`
Let's now assume that in your Interview there is also the head of the marketing department. He tells you that they are currently thinking about a new marketing strategy. In particular they want to test a new coupon and want to see if the customers will respond better. 

Now he asks you how you would find out if the new strategy works or not.

Your answer should be statistical testing or Hypothesis testing. Another common name for this type of experiment is "A/B Testing".


---
## Hypothesis Testing Concept

```yaml
type: "FullSlide"
key: "f5c1493478"
center_content: false
```

`@part1`
1. **Define:** **Null Hypothesis** ($H_0$) and **alternative Hypothesis** ($H_A$) {{1}} 
2. **Assume $H_0$ is true** and calculate  the **probability** of our data **under $H_0$** {{2}} 
3. Decide the **level of significance** (usually marked as $\alpha$) {{3}} 
4. If this probability is **smaller than $\alpha$**, **reject $H_0$** in favour of the alternative hypothesis {{4}}


`@script`
Now, let's look at the steps on performing a hypothesis test.
First you always have to define your Null Hypothesis and your alternative Hypothesis.
In the second step, you assume that the Null Hypothesis is true and you calculate the probability of the observed data under the Null Hypothesis.
You then have to set a significance level alpha.
If your calculated probability is smaller than your alpha you reject the Null Hypothesis in favour of your alternative hypothesis.


---
## Apply Hypothesis Testing - Marketing Campaign

```yaml
type: "FullSlide"
key: "8fd1135ee6"
center_content: false
```

`@part1`
1. **Define:** **Null Hypothesis** ($H_0$) and **alternative Hypothesis** ($H_A$) 
 - $H_0$: **No difference** between click rates of new and old coupons {{1}} 
 - $H_A$: There is a difference between new and old coupons {{2}} 
2. **Assume $H_0$ is true** and calculate  the **probability** of our data **under $H_0$** {{3}}
 - Use **Chi-Squared test** for binary data (Clicked: Yes/No){{4}} 
3. Decide the **level of significance** (usually marked as $\alpha$) {{5}} 
 - $\alpha = 0.05$ {{5}} 
4. If this probability is **smaller than $\alpha$**, **reject $H_0$** in favour of the alternative hypothesis {{6}}


`@script`
Let's now see how you would apply hypothesis testing on the marketing campaign scenario.
The Null Hypothesis would be that there is no difference between the click rates of the old and the new coupons. The alternative hypothesis is exactly the opposite of the Null hypothesis, meaning that there is a difference between the click rates.
Now we have to calculate the probability under the Null Hypothesis. Since we have binary data, meaning a user can either click on the coupon or not,  we can use the Chi-Squared test. If you want to learn more about which tests to use for which scenarios, DataCamp has a lot of great courses for that.
A common value for the significance level alpha is 0.05 which we have to compare our probability with and then decide whether to reject our Null Hypothesis or not.


---
## Campaign Data 1/2

```yaml
type: "FullCodeSlide"
key: "acb86aca57"
```

`@part1`
```python
# load modules
import numpy as np
import pandas as pd

# load data and display first rows
new_code_campaign = pd.read_csv("new_code_campaign.csv")
new_code_campaign.head()

   click_date  campaign  clicked
0  2018-12-01  old_code        1
1  2018-12-01  old_code        1
2  2018-12-01  old_code        0
3  2018-12-01  old_code        0
4  2018-12-01  old_code        0
```

```python
new_code_campaign["campaign"].value_counts()

old_code    1000
new_code    1000
Name: campaign, dtype: int64
```
{{1}}


`@script`
Let's see how you would do it in Python. 
First we have to import our modules. Here we imported numpy as np and pandas as pd. Then we use pandas read_csv function to load our data to new_code_capaign. Using the method .head() we can display the first 5 rows of our dataframe. In total we have three columns with the click date, the campaign telling us whether it's the old or new code, and the column clicked, which tells us whether the customer clicked on the code or not. 1 means the customer did click on the coupon and 0 if not.
We can use the value_counts() method on our "campaign" column to see how many old and new coupons were sent to the customers. Here 1000 coupons were sent in each case.


---
## Campaign Data 2/2

```yaml
type: "FullSlide"
key: "6962c92a7d"
```

`@part1`
```python
# create Contingency table
cont = pd.crosstab(my_data["campaign"],
                   my_data["clicked"])
print(cont)

clicked     0    1
campaign          
new_code  484  516
old_code  688  312
```

```python
# calculate click rate for each campaign (conversion rate)
cont.apply(lambda r: r/r.sum(), axis=1)

clicked       0      1
campaign              
new_code  0.484  0.516
old_code  0.688  0.312
```
{{1}}


`@script`
In order to see how many people actually clicked on the two different coupons we can create a contingency table using pandas crosstab function. 
We see that 516 people clicked on the new coupon and 312 clicked on the old one.
Sometimes we are also interested in the click rates which are also called conversion rates. We can use apply and lambda functions to divide the previous values by the number of coupons for each campaign.


---
## Perform a Chi Squared test in Python

```yaml
type: "FullCodeSlide"
key: "c7b658c138"
```

`@part1`
```python
# impport chi2_contingency
from scipy.stats import chi2_contingency
```
 
```python
# Perform Chi Squared Test
chi2, p, dof, expected = chi2_contingency(cont)
```
{{2}} 
```python
# Print p-Value
print(p)
3.09025555601e-20
```
{{3}} 
- p is smaller than $\alpha$ => Reject $H_0$ {{4}}


`@script`
In order to perform a Chi-Squared Test in Python, we first have to import the chi2_contingency module from scipy.stats.
We then can use the chi2_contingency function on our previous contingency table which returns the Test Statistic, the p-Value, which is the probability of the observed data under the Null Hypothesis, the degree of Freedoms and the expected contingency table under the Null Hypothesis.
We are interested in the p-Value, so let's print it out.
The probability is below our significance  level of 0.05 and therefore we can reject our Null Hypothesis that there is no difference between the click rates of new and the old coupons.


---
## Let's practice!

```yaml
type: "FinalSlide"
key: "640654258a"
```

`@script`
Now let's practice what you have learnt in the following exercises!

