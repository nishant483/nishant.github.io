---
layout: post
title:  "Regularisation - Why do we need it ?"
date:   2020-09-18 09:30:32 +0530
usemathjax: true
categories: jekyll update
---

Reference: [https://explained.ai/regularization/index.html](https://explained.ai/regularization/index.html) 

The blog is small writeup from the original blog by Terence Parr which provides a simple and intuitive explanation about regularisation in linear and Logistic Models.

Linear and Logistic models are easy to use, interpretable, and fast models in the machine learning ecosystem. They also form the basis of Deep Learning Neural Networks part of which i have described later in the blog.

- Linear and Logistic Models find the best line or hyperplane that fits the training data.
- They have a tendency to chase outliers (Extreme Points), because of which they don't perform well on the test data (or) don't generalise well.

To produce models that generalize better, we regularise these models.

There are multiple ways of regularisation like dropout or early stopping with deep learning, but with linear models, the two most used regularisation techniques are

- Lasso(L1) Regularisation
- Ridge(L2) Regularisation

## **A quick review on linear regression**

Linear Regression aims to find the best line that fits a set of given points.

- A single-variable linear regression model is for example $y = β0+β1x$ where β0 (coefficient) is the y-intercept and β1 is the slope of the line.
- Let's say we have the following data points and we have to find the best line across these points

<!-- [https://lh4.googleusercontent.com/qb5vD_c44VpHyTQ56P8lZLLKlw6Xu6c_PXMZgQvVLvmFKgI4rYcGexqmDhqBTGOM5owIAXCcr6wfEg81bTzwdkzaaDKxh9T0HQZbxgQe1T9eQVvYHLIlOS8SnbiL5zYM8_ZlPY2_](https://lh4.googleusercontent.com/qb5vD_c44VpHyTQ56P8lZLLKlw6Xu6c_PXMZgQvVLvmFKgI4rYcGexqmDhqBTGOM5owIAXCcr6wfEg81bTzwdkzaaDKxh9T0HQZbxgQe1T9eQVvYHLIlOS8SnbiL5zYM8_ZlPY2_) -->
![image](https://lh4.googleusercontent.com/qb5vD_c44VpHyTQ56P8lZLLKlw6Xu6c_PXMZgQvVLvmFKgI4rYcGexqmDhqBTGOM5owIAXCcr6wfEg81bTzwdkzaaDKxh9T0HQZbxgQe1T9eQVvYHLIlOS8SnbiL5zYM8_ZlPY2_)


- The best line that fit's these data points is $y = -0.17+1.022x$ as shown below where (-0.17,1.022) represents the relationship between x and y

![image](https://lh3.googleusercontent.com/PPgedMcwJooBoQz1AdUXYqnt0A6CSV2xRJ7OVgEe9h7xQrhYEWTmd5sT7uzQI9fTjx1WkfDkuGKJxM9WOvIMdibFokheTKO9iYwpUmcbm5ack_9OoaNl_c1Q0oLmYc53U8eDPf-U)

- You can use sklearn to find a similar relationship using the below code

{% highlight python %}
lm = LinearRegression()
lm.fit(x, y)
optimal_beta0 = lm.intercept_
optimal_beta1 = lm.coef_[0]
{% endhighlight %}

- The idea of finding the best line is to find β0 and β1 such that the average error of the difference between the predicted value of the model and the actual value is minimum

- The orange line is the prediction line $$y = -0.17+1.022x$$ and blue are the points from the above table

- Mathematically, the equation would be

![image](https://lh5.googleusercontent.com/8aXi0ctO8J93z-QRDa5qN5ODb8jhyQFKyjteY4ZC5BCnj-z44zsyVc4cVH2ZLSLPdfMw7_0pOh1S6wcOEzU_1Rq46JH5sA4g-D3CClHl3QrsT9VgbcwEE5IWMIey1PznsbHMu8Ev)

or

![image](https://lh3.googleusercontent.com/qnPDiti6b1flKyY-asAH90vs8kwDmTg5Yd93uQPmgNtXYzL6kJlhatnI3KcTmTMdZYTyEqZbddVcAi10g5Hdwy538p_n5VxdG7yOm9rj69TUF3yCq6Tv0P6Gr9Y5PIrx7sfLqT-T)

- The values for beta can be calculated using the below formulas

![image](https://lh6.googleusercontent.com/uVoKdcvTLM3ByUKSs1dY7neEbCzfFoRuYXULHXaMa5sdZzpdFPjblXYFqnrUsjiSyVqaKrH9AAcsReXlBewSi7aHgXNNEAWdRo7kGTZaHJTE3i8htTsBXQD8sf9Cn_Lfv6INd3Ht)

- The β0 and β1 for which the MSE (Minimum square error is minimum) will describe the best fit relationship between x and y.

## **Need for Regularization**

- Let's tweak the numbers and make the last y value to be 10 times bigger than its original value

    ![image](https://lh5.googleusercontent.com/bXOKtuf1CVWYFDqUJtU0BwpOerIU8LGCQaZaXLU48ua0FpwPFvWkPfB_r_QMLTROa8qZouDBAJpN5iEaanoIOfO0t5WAflh0qqVVbHTosH2aRr-XXtc1sLWkNPPTQzLOcunjnmHT)

- The new prediction line (orange) has tilted a lot towards the outlier to reduce the overall average error.
- Compared to β0 = -0.170 and β1 = 1.022 (coefficients from the last data set without outlier) , the new β0 = 5.402 and β1 = -13.15 have changed a lot because of one outlier.
- In real-world scenarios, we mostly see data with outliers.

**How does regularization help?**

- Before understanding what regularisation does, let's use sklearn to apply regularisation on the above data and see how the prediction line changes.

![image](https://lh5.googleusercontent.com/IFs784gEqbxWJrIh6P1gUUBRM0LFJV6cjx6CrxDQ7a6S7R1iOQuvPozunYqYV7ULGCNbFYewKKw_9x_P4jFc9i-vjVIZz9JMf2A3ZQL3zVDPzXZKV5YuXcS5wS__fJsAGUkfLKGE)

- The premise of regularization is that the extreme coefficients are unlikely to yield models that generalize well, so regularization tries to minimize the size of coefficients.

## **2. How Regularization works conceptually**

- Regularization helps us to generalize our models (fit better on unseen data) by putting a constraint on the coefficients.

![image](https://lh4.googleusercontent.com/jNiUh-vnJYwmPm2YkbSYG8FCgQEHyvSr7qmoIc5FotC-j1eo8WhVNCKNdswPflgBbYKfztirooIW_siVAWxL57nE7XAZATl_e1by14ys1gaFiIKMu2Ht7VW0DCAmsJE8megJPb7X)

# **2.1 L2 Ridge Regression**

- The figure below shows an example of a loss function whose minimum loss value lies at β1 = 7 and β2 = 1.
- Surrounding the origin is a hard constraint on coefficients, the regularization will have to contract the coefficient values in that hard constraint where the loss value is minimum.
- The hard constraint for two variables can be described using $$ \sqrt{β1^2+β2^2} < t$$ where t can be found using grid search (which gives minimum validation error)
- Below is a top view of the loss function where the black dot is a minimum loss without regularization and the big red dot is the minimum loss point within the constraint

![image](https://lh4.googleusercontent.com/4fGQXn8D01pXHbNQFNa1x7AxsnISm1LjZnkUDWyEqxVT1UrwetrXat0aHe78GhgEhqAi9bLriMjgg6JV5Loi8CWM7mzUreA42BF394uLcdxLuX1FKwGm2JE3aFnsyva7Z_n1j_Fk)

The below figure illustrates different locations of constraint coefficients of different hypothetical loss functions projected in 2D.

The black dot point represents minimum loss point without constraint and red point is minimum loss point within constraint.

![image](https://lh5.googleusercontent.com/8Yugirx6drPmlDPCKjQPfssWfausNTMNsGFpFczFtoT1sSeV2U6O0o7KcV8H2OSMETuZNgS7FLu0Yv2p6JLOmZmfUegJHNlZlrpMxlfpecIY3mWaIEQsnjh1maNVnq9kuE_LrCiI)

**Finding the L2 Coefficients**

- The L2 Regularized coefficients will always lie in the constraint circle. We just need to walk around the circle and find the point where the loss is minimum.

Mathematically, L2 Regularization can be summed with

![image](https://lh5.googleusercontent.com/2vILW-J421wyJb2R1ZCilXgzyAKgFldCYj3Xd26jEFP8EipDQ60-UtUZxypEjEJf9-WjmIJuuwT2hxjY6bidmbUDXAf4TTpcNxvGIeR0ZXUi8On4MEa-AUc8P0u8Uzn3zSAEWeqR)

# **2.2 L1 Lasso Regression**

- The only difference between L1 and L2 Regression is the constraint equation and the shape of the constraint.
- The hard constraint for two variables in Lasso Regression can be described using $$ \|β1+β2\| < t$$, so the shape of constraint becomes diamond.

![image](https://lh4.googleusercontent.com/OKZyVs4jr245zlSczsITPc7colKfxi00uuX7vEr1Itgcr6CmhJsduG2SQxRuRVOy0BSlP2VacJnbangRQYhbjZfD4CIyRVea7AMMchSYsRxIK4Slea13y9ferlEpDvN4ojMj3tkm)

The above figure illustrates different locations of constraint coefficients for different hypothetical loss functions projected in 2D.

The black dot point represents minimum loss point without constraint and red point is minimum loss point within constraint.

Mathematically, L1 Regularisation can be summed with

![image](https://lh6.googleusercontent.com/B2PzGxbQXtW4RJBAyPTq2aEbEgYb-Yix_AwMnT99ht2y4eBIm56awugzmZgkM68M9oQF3arLb0ntTpABUbUAn12HIJBOAU1Om-jT_r9cIG9EZY2hynWXDT9N6JoIYLzmZF0PJDoV)

### **3. The difference between L1 and L2 Regularization**

Apart from the different shapes of constraints and equations, there are few other key differences around how L1 and L2 Regularization works.

- L1 tries to shrink the coefficients to zero, so it’s used for the purpose of feature selection

- L2 tries to evenly shrink the coefficient values. L2 is mostly used where the coefficients are co-dependent. Codependent features have high coefficient variance resulting in overfitting of models. L2 reduces the variance helping the models to generalize better.

**3.1 Why is L1 more likely to have more zero coefficients than L2?**

The below figures illustrate a hypothetical loss function with L1 and L2 regularization constraints.

- The black dot represents the minimum loss point without regularization. The red point is the minimum loss point after applying the regularization constraint.

![image](https://lh6.googleusercontent.com/fZHFFM2Ef4JhbHdCTQv4H9vT1u5-RAL_6TIw1040lAaNXUN8n8ZsbnyW288cXCA-tAqMw8qkUgoWyUkGpclpJdCyp69rXe8xoC4mrcCT1_bnpKOV0V9Z6qDA6yOfa1ItvwckflzC)

![image](https://lh4.googleusercontent.com/tqU_q6Gx6saz2DR44LQpZN-luKDbWcTCQZOxxbIH88ziTcRrTSMZTgLEyW7Oh2U4uYu-s0DtQR0mWXZpRAZTmtZy0JX2z4l8egaF8uzYSFwzyQMpyf_VYJAwOTrRK-Nq3YQqlTME)

- Each curved contour line represents the same loss function value, and the closer the contour lines, the steeper the slope across those lines. (Recall these are projections of a 3D bowl or taco shaped surface onto a two-dimensional plane.)

- If we try to find any other point except the purple point in L1 Regularization, we have to move away from the black point towards the origin, which will result in an increase of loss value

- But in L2 Regularization, if we have to find another point, except the one on the x-axis, the shape of the circular constraint allows us to go away from the origin while still being in the constraint region.

![image](https://lh6.googleusercontent.com/67oNzaGlC2tqq99cW_A_-03jai_6VPc7eDtinZkGdRID7QL_TlBfn-xnFd9lVE_wy-dVlSATKcQ2rIKea_2eD2uGF_KkBHAfEX9BqSQGhBB0RpRskacb1XV_zpfZ22Zmmz6GL4RG)

### **Recasting hard constraints as soft constraints**

To implement a loss function with a hard constraint, we could use a gradient descent minimization approach as usual. The problem is that, at each step moving us closer to the loss function minimum, we'd need an IF-statement asking if (β0,β1) had exceeded the constraint. Certainly, that would work, but it would definitely slow down the computation.

An alternative approach is to convert the constraint into just another term of the loss function but at the cost of making it a soft constraint, not a hard constraint.

![image](https://lh6.googleusercontent.com/bzvLij0HDL6VndwaQwsQirvv0KmFx4DKBHLdV_LDeKlZQBQ_zgv1Nv_6vygBg0hIHEzkdoIEHr4jHzfQWh_YSHgvO3clVtQ-vFj-1dfCGvI30fu2pA3EjXrll4xEIA7FwNQpEm1l)

![image](https://lh6.googleusercontent.com/LnUBcg5ACM8M31LQJPVhWXnK_0wtuHgA0Tl92eyaCO7Gus3FiF2roQqt1XjM9BYn8njsWqr0Gdb__gmg0TG4jj--O2XJ668cI5lOZivDJyDUkWR3_yHF5p4S6sPV2onA8XwidfAJ)

where lambda becomes a hyperparameter which can be found through grid search

# **How Linear Regression forms the basis of Deep Learning Neural Networks**

The first thing that we get to learn while starting Neural networks is a perceptron.

A perceptron is a simple Neural Network that takes certain inputs and produces a linear equation which is exactly similar to the linear regression equation.

![image](https://lh4.googleusercontent.com/CG2t8cGZ57m1JBhB_WZtq9v5BPGCtl_PnFX-tOUgvPzgX_g-Mih9KxBe6cSob9YVt9d-ynvEu2TYSs2TreQHoR67BzCO1HRKY-VFHHkmvWnvsY4OBe7cVEU48q031Ai6PpZBwgA_)

At the end of the neuron, if we use a non-linear activation function like sigmoid, it becomes a classifier or else it can be used as regressor. L1 or L2 regularisation can also be applied to the neuron outputs, in a similar way as is done with linear regression.

# **Further Reading**
[https://explained.ai/regularization/index.html](https://explained.ai/regularization/index.html)

[https://medium.com/datadriveninvestor/l1-l2-regularization-7f1b4fe948f2](https://medium.com/datadriveninvestor/l1-l2-regularization-7f1b4fe948f2)

[https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a](https://towardsdatascience.com/regularization-in-machine-learning-76441ddcf99a)

[https://www.kdnuggets.com/2016/06/regularization-logistic-regression.html](https://www.kdnuggets.com/2016/06/regularization-logistic-regression.html)