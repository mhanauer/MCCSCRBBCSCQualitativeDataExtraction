# DataCleaningExample
---
title: "DataCleaning"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Here is an example cleaning a data from a survey that we from a local school district in Bloomington, IN.  
```{r}
setwd("~/Desktop")
rbbcsc = read.csv("RBBCSCStaffSurvey.csv", header = TRUE); head(rbbcsc)
mccsc = read.csv("MCCSCStaffSurvey.csv", header = TRUE); head(mccsc)

```
When we exported the data from qualtrics, the first rows, were additionally information that qualtrics provides that is not relevant to the study.  Therefore, we deleted the first two rows across all the variables.
```{r}
rbbcsc = rbbcsc[-c(1:2),]; head(rbbcsc)
mccsc = mccsc[-c(1:2), ]; head(mccsc)

```
Next we select the variables from the dataset that we are interested in analyzing.  In this case, we are interested in evaluting the differences between the perceptions of current professional development for Social and Emotional learning of staff who are exclusively primary and secondary teachers.  Therefore, we must selet the two appropriate variables for this research question.  

```{r}
rbbcsc2 = rbbcsc[c("Q3")]
rbbcsc3 = rbbcsc[c("Q15")]
mccsc2 = mccsc[c("Q3")]
mccsc3 = mccsc[c("Q44")]
```
Now we grab only the responses for exclusively secondary teachers 
```{r}
rbbcsc3 = apply(rbbcsc3, 1, function(x){ifelse(x == "Secondary school teacher", 1, x)}); rbbcsc3
rbbcsc2 = as.data.frame(rbbcsc2); rbbcsc2
mccsc3 = apply(mccsc3, 1, function(x){ifelse(x == "Secondary school teacher", 1, x)}); mccsc3
mccsc3 = as.data.frame(mccsc3); mccsc3
```
Now that we have data coded for each of variables of interest, we can combine them back into one data frame using the cbind funciton.
```{r}
rbbcsc4 = cbind(rbbcsc2, rbbcsc3)
mccsc4 = cbind(mccsc2, mccsc3)
```
Finally, we grab data where a respondent is are primary (1) exclusively.  Because those staff members are coded as 1, we can grab data for that group using the subsetting logic displayed below.
```{r}
rbbcsc5 = rbbcsc4[rbbcsc4$rbbcsc3 %in% c(1), ]
rbbcsc5

mccsc5 = mccsc4[mccsc4$mccsc3 %in% c(1), ]
mccsc5

```
Now we need to change the names
```{r}
names(mccsc5) = c("Barriers", "Category")
names(rbbcsc5) = c("Barriers", "Category")
```
Then we need to append the two data sets together.  We can do that using the rbind function.
```{r}
both.qual = rbind(mccsc5, rbbcsc5); both.qual
write.csv(both.qual, "both.qual.csv")
both.qual2 = read.csv("both.qual.csv", header = TRUE, na.strings = c("", "NA"))
both.qual3 = na.omit(both.qual2)
write.csv(both.qual3, "both.qual3.csv")

```
Get rid of blank spots





