---
title: "Test"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Library packages
```{r}
library(MASS)
library(caret)
library(pROC)
library(semTools)
library(lavaan)
```
Set up the data using this website: http://lavaan.ugent.be/tutorial/mediation.html
```{r}
set.seed(1234)
X <- rnorm(100)
M <- 0.5*X + rnorm(100)
Y <- 0.7*M + rnorm(100)
Data <- data.frame(X = X, Y = Y, M = M)
```
Now setting up the model
```{r}
model1 =' 
  #direct effect
  Y ~ c*X
  #mediator
  M ~ a*X
  Y ~ b*M
  #indirect effect 
  ab:= a*b
  # total effect
  total := c+(a*b)
'
fit = sem(model1, data = Data)
summary(fit)
```


