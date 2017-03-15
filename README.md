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
head(both.qual7)
```

# Now I want to select only those values that contain 1 for the index 
```{r}
both.qual8 = both.qual7[both.qual7$index %in% c(1), ]
head(both.qual8)
```
Next I want to create three different data sets one with only themes for that theme so it will be easier to develop more in-depth themes from.

