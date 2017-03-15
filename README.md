# MCCSCRBBCSCQualitativeDataExtraction
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
```
When we exported the data from qualtrics, the first rows, were additionally information that qualtrics provides that is not relevant to the study.  Therefore, we deleted the first two rows across all the variables.
```{r}
rbbcsc = rbbcsc[-c(1:2),]; head(rbbcsc)
```
Next we select the variables from the dataset that we are interested in analyzing.  In this case, we are interested in evaluting the differences between the perceptions of current professional development for Social and Emotional learning of staff who are exclusively primary and secondary teachers.  Therefore, we must selet the two appropriate variables for this research question.  

```{r}
rbbcsc2 = rbbcsc[c("Q3")]
rbbcsc3 = rbbcsc[c("Q15")]
```
Now we grab only the responses for exclusively secondary teachers 
```{r}
rbbcsc3 = apply(rbbcsc3, 1, function(x){ifelse(x == "Secondary school teacher", 1, x)}); rbbcsc3
rbbcsc2 = as.data.frame(rbbcsc2); rbbcsc2

```
Now that we have data coded for each of variables of interest, we can combine them back into one data frame using the cbind funciton.
```{r}
rbbcsc4 = cbind(rbbcsc2, rbbcsc3); rbbcsc4
```
Finally, we grab data where a respondent is are primary (1) exclusively.  Because those staff members are coded as 1, we can grab data for that group using the subsetting logic displayed below.
```{r}
rbbcsc5 = rbbcsc4[rbbcsc4$rbbcsc3 %in% c(1), ]
rbbcsc5
```
Now we need to change the names
```{r}
names(mccsc5) = c("PD", "Category")
names(rbbcsc5) = c("PD", "Category")
```
Then we need to append the two data sets together.  We can do that using the rbind function.
```{r}
both = rbind(mccsc5, rbbcsc5); both

```
---
title: "Test"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

# Need to create a new variable that is a one then one for new variable
```{r}
both.qual5 = read.csv("both.qual4.csv", header = TRUE, na.strings = c("", "NA"))
```


# Then do na.omit to get rid of those did not receive a one
# Theme Time, Professional.Development , More.staff.support
```{r}
both.qual6 = both.qual5[c("Time", "Professional.Development", "More.staff.support")]
head(both.qual6)
```

# Now I need create a variable goes through and creates a one in a new variable for any variable that has a one
# Create a new variable that is the sum of the three variables.  Then recode that variable if the variable is greater than zero, than it will be recoded as one
```{r}
index = rowSums(both.qual6, na.rm = TRUE)
head(index)
both.qual7 = cbind(both.qual6, index)
```

# Now I want to select only those values that contain 
both.qual7







