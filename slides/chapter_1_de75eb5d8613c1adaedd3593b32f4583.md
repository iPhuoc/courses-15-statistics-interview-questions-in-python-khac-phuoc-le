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
title: Data Scientist, Deloitte Consulting


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
Let's now assume that in your Interview there is also the head of the marketing department. He tells you that they are currently thinking about a new marketing strategy. In particular they want to test a new coupon in their newsletters and want to see if the customers will respond better. What they want to achieve is to get more clicks on the new coupon so that the customers will go onto their website.
Now he asks you how you would find out if the new strategy with the new coupon works or not.
You answer should be statistical testing or Hypothesis testing. Another common name for this type of experiment is "A/B Testing".


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

 $H_0$: **No difference** between new and old coupons 

 $H_A$: There is a difference between new and old coupons 

2. **Assume $H_0$ is true** and calculate  the **probability** of our data **under $H_0$**
 
  Use **Chi-Squared test** for binary data (Clicked: Yes/No)
3. Decide the **level of significance** (usually marked as $\alpha$)

     $\alpha = 0.05$
 
4. If this probability is **smaller than $\alpha$**, **reject $H_0$** in favour of the alternative hypothesis


`@script`



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
my_data = pd.read_csv("my_data.csv")
my_data.head()
```
```
   click_date  campaign  clicked
0  2018-12-01  old_code        1
1  2018-12-01  old_code        1
2  2018-12-01  old_code        0
3  2018-12-01  old_code        0
4  2018-12-01  old_code        0
```


`@script`



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
{{1}} 
```python
# calculate click rate for each campaign (conversion rate)
cont.apply(lambda r: r/r.sum(), axis=1)

clicked       0      1
campaign              
new_code  0.484  0.516
old_code  0.688  0.312
```
{{2}}


`@script`



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

# Perform Chi Squared Test
chi2, p, dof, expected = chi2_contingency(cont)

# Print p-Value
print(p)
3.09025555601e-20

print(p < 0.05)
True
```


`@script`



---
## Let's practice!

```yaml
type: "FinalSlide"
key: "640654258a"
```

`@script`


