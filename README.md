
How does birth policy affect fertility rate in China
output: html_document
/Zitong Hu
---


【Please see "China Fertility rate paper.pdf" in the repository for the final analysis and paper】
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

1. Introduction/
The dataset contained 11 datasets published by the China General Social Survey from 
2003 to 2018. I cleaned these data and combined them into one dataset. This study investigated the effect on female with different geographical residential status (urban/rural), and on female with different higher 
education background. 

The one child policy was relaxed on 2013 and I used pre-post 2013 as an interaction term in the analysis. The variable Post_2013 indicates whether the interview happened before or after 2013 and the variable Post_2013_123 specifies which year it was after 2013. 2013 is indicated as 0, 2015 is indicated as 1, 2017 is indicated as 2, and 2018 is indicated as 3.

Both variables were closely studied to find out whether the effect of relaxation of OCP was one-off since 2013 or there existed gradual changes since 2013. 

```{r}
final<- read.csv("final.csv")

final$Post_2013 <- as.factor(final$Post_2013)
final$Post_2013_123 <- as.factor(final$Post_2013_123)
```


The result of feature engineering shows that urban/rural status, education level, province, and marital status influence fertility rate the most. 


2. Linear regression model with factor post_2013_123
```{r}

model1 <- lm(two_or_more_kids ~ Post_2013 * Urban, data = final, weight = Weight)
summary(model1)



model2 <- lm(two_or_more_kids ~ Post_2013 * Urban + 
               College_and_above + Married + Province , data = final, weight = Weight)
summary(model2)



model3 <- lm(two_or_more_kids ~ Post_2013 * College_and_above , data = final, weight = Weight)
summary(model3)



model4 <- lm(two_or_more_kids ~ Post_2013 * College_and_above + Urban + Married + Province, 
              data = final, weight = Weight)
summary(model4)

```

3. Linear regression model with factor post_2013
```{r}
model5 <- lm(two_or_more_kids ~ Post_2013 * Urban, data = final, weight = Weight)
summary(model5)

model6 <- lm(two_or_more_kids ~ Post_2013 * Urban + 
               College_and_above + Married + Province , data = final, weight = Weight)
summary(model6)



model7 <- lm(two_or_more_kids ~ Post_2013 * College_and_above , data = final, weight = Weight)
summary(model7)

model8 <- lm(two_or_more_kids ~ Post_2013 * College_and_above + Urban + Married + Province, 
              data = final, weight = Weight)
summary(model8)

```

