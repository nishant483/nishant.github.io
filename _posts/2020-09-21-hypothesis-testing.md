---
layout: post
title:  "Hypothesis Testing"
date:   2020-09-21 11:30:32 +0530
usemathjax: false
categories: jekyll update
---

# Hypothesis Testing

Hypothesis Testing is used in statistics to understand the population distribution behavior by looking at a few testing samples.

In the Testing process, we use concepts like p-value, alpha value, and significance levels to make sure our test results are statistically significant which we will understand later in this blog.

### **Example**

Imagine we have two coins and we are running a Head/Tails game. If it’s a Head, we win 5$ and if we get Tail, we lose 5$.

While tossing the coin twice, let's say we get tails both times.

Would you consider the coin is rigged and both sides of the coin are tails?

You can, but the probability of getting two tails in a fair coin is also 25% as shown in the picture below.

![image](https://lh6.googleusercontent.com/hqIrE7aGbILsYkkTlKA3iGpiRuFdQDjFFcccf14KWcneY5LC67dXaTnMV2oz3uJR93EGRk7Idtukt64xWLLz_80v4duIHnsR5ycN_KTRZHMufAM-4ua_A05U67QUhqbnsJoZ4smv)

So now, let's say we toss it 5 times and we get tails all the time.

The probability of getting 6 tails on a fair coin is 1.56% which is more unlikely. At this point, we can consider that our coin is rigged.

![image](https://lh6.googleusercontent.com/R4Jgd3_Clp_ADm_Ddl9sP61mkXmMwDYsXvaqb-wdF0iJZ4H6MlykKVw_Y3Fi1xUvvfa7E_PnPbdSUWEVlpGGcG16WcQUhV1T8NdBjopfz915jDkf9WrMqb6LTg9nJn0Y5r2RF5p8)

Generally, we will set a threshold (ex - 5%) and if the probability goes below that point, we can consider that the coin is rigged.

### **Understanding Terminologies**

**Null Hypothesis:** The null hypothesis is the assumption that we set at the start of taking samples. The null hypothesis tends to state that there is no change in testing samples as compared to the original population and things are fair.

The null hypothesis in our example is that the coin is not rigged and that the observations are purely from chance.

**Alternate Hypothesis:** The assumption that something has changed in testing samples because of some outside non-random cause.

The alternate hypothesis in the above example is that the coin is rigged and it is always returning tails.

**P-value**: The probability value of obtaining the observed values assuming the null hypothesis is correct. For example - in the above coin toss example, the p-value of tossing two coins and both landing on tails is 25%, and tossing 6 coins and all landing up on tails is 1.56%.

**Alpha Value:** The significance level or threshold beyond which we can consider the null hypothesis to be incorrect.

In the above coin toss example, we set that to 5%. Any p-value below 5% results in rejecting the null hypothesis and considering alternate hypothesis to be correct.

The p-value can differ depending on the domain. In clinical studies, the p-value is set at 1% or lesser.

**Rejecting or not rejecting the null hypothesis?**

If the p-value is less then threshold, we reject the null hypothesis and accept the alternate hypothesis

But if the p-value is greater than then threshold, we accept the null hypothesis.

References and further reading

[https://towardsdatascience.com/hypothesis-testing-explained-as-simply-as-possible-6e0a256293cf](https://towardsdatascience.com/hypothesis-testing-explained-as-simply-as-possible-6e0a256293cf)

[https://statisticsbyjim.com/hypothesis-testing/hypothesis-tests-significance-levels-alpha-p-values/](https://statisticsbyjim.com/hypothesis-testing/hypothesis-tests-significance-levels-alpha-p-values/)