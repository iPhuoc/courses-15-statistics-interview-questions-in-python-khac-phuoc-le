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



---
## Hypothesis Testing Concept

```yaml
type: "FullSlide"
key: "f5c1493478"
center_content: false
```

`@part1`
1. **Define:** **Null Hypothesis** ($H_0$) and **alternative Hypothesis** ($H_A$)
2. **Assume $H_0$ is true** and calculate  the **probability** of our data **under $H_0$**
3. Decide the **level of significance** (usually marked as $\alpha$)
4. If this probability is **smaller than $\alpha$**, **reject $H_0$** in favour of the alternative hypothesis


`@script`
test


---
## Apply Hypothesis Testing - Marketing Campaign

```yaml
type: "FullSlide"
key: "8fd1135ee6"
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
## Campaign Data

```yaml
type: "FullCodeSlide"
key: "acb86aca57"
```

`@part1`
```python
import numpy as np
import pandas as pd

my_data = pd.read_csv("my_data.csv")
my_data.head()
```
```
Out[1]: 
   click_date  campaign  clicked
0  2018-12-01  old_code        1
1  2018-12-01  old_code        1
2  2018-12-01  old_code        0
3  2018-12-01  old_code        0
4  2018-12-01  old_code        0
```
```python
cont = pd.crosstab(my_data["campaign"],
                   my_data["clicked"])
print(cont)

clicked     0    1
campaign          
new_code  484  516
old_code  688  312
```


`@script`



---
## Perform a chi squared test

```yaml
type: "FullCodeSlide"
key: "c7b658c138"
```

`@part1`
```python
from scipy.stats import chi2_contingency

chi2, p, dof, expected = chi2_contingency(cont)

print(p)
3.09025555601e-20

print(p < 0.05)
True
```


`@script`



---
## Final Slide

```yaml
type: "FinalSlide"
key: "640654258a"
```

`@script`


