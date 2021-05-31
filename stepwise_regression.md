---
title: Stepwise Regression
parent: Generalised Least Squares
has_children: false
nav_order: 1
mathjax: true 
---

# Stepwise Regression

When we use multiple explanatory variables to perform regression analysis on a dependent variable, there is a great possibility that the problem of multicollinearity will occur. However, multiple linear regression requires that the correlation between the independent variables is not too high, so we need a method to eliminate multicollinearity and select the "optimal" regression equation. That is stepwise regression. It can automatically help us retain the most important explanatory variables and remove relatively unimportant variables from the model. 

$~$

The idea of stepwise regression is to introduce independent variables one by one, and after each independent variable is introduced, the selected variables are tested one by one. If the originally introduced variable is no longer significant due to the introduction of subsequent variables, it is deleted. Repeat this process until the regression equation does not introduce insignificant independent variables and does not remove significant independent variables, then the optimal regression equation can be obtained.

## Keep in Mind


- The purpose of stepwise regression is to find which combination of variables can explain more changes in dependent variables.

- Stepwise regression is to observe statistical values, such as R-square, t-stats, and AIC indicators to identify important variables. 

## Also Consider

- There are three methods of stepwise regression: Forward Selection, Backward Elimination and Stepwise Selection.

- Forward selection starts from the most important independent variable in the model, and then increases the variable in each step. 

- Backward elimination starts with all the independent variables of the model, and then removes the least significant variable at each step.

- The standard Stepwise Selection combines the above two methods, adding or removing independent variables in each step.

# Implementations

## R

We will use the build-in mtcars dataset, and the step() function in package "stats" can help us to do the stepwise regression. 

```r
# Load package

library(stats)

# Load data and take a look at this dataset
data(mtcars)
head(mtcars)

# Define a regression model mpg ~ all other independent variables.
reg_mpg <- lm(mpg ~ ., data=mtcars)

# Define intercept model
intercept <- lm(mpg ~ 1, data=mtcars)
```

$~$

```r
# Forward selection

forward <- step(intercept, direction = c("forward"), scope=formula(reg_mpg))

summary(forward)

```

The optimal equation we get from forward selection is $mpg = 38.752 - 3.167*wt - 0.942*cyl - 0.018 hyp$

$~$

```r
# Backward selection

backward <- step(reg_mpg, direction = c("backward"), scope=formula(reg_mpg))

summary(backward)

```

The optimal equation we get from backward elimination is $mpg = 9.618 - 3.917*wt + 1.226*qsec + 2.936*am$

$~$

```r
# Stepwise selection

stepwise <- step(intercept, direction = c("both"), scope=formula(reg_mpg))

summary(stepwise)

```

The optimal equation we get from stepwise selection is $mpg = 38.752 - 3.167*wt - 0.942*cyl - 0.018 hyp$


