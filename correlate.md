## Details on how to do Bivariate analysis

In addition to the bivariate table, you will also have to include a correlation matrix in the bivariate analysis set of tables. This is important as in your research you are using an instrument (the questionnaire) where you have asked your participants questions and they have answered indicating preferences. These preferences ranged from "Totally Agree" to "Totally Disagree", and a "Neutral" in between (See the following table).

| Variable Category | Score Assigned |
|-------------------|----------------|
| Totally Agree     | 1              |
| Agree             | 2              |
| Neutral           | 3              |
| Disagree          | 4              |
| Totally Disagree  | 5              |
| Don't Know        | 6              |

We take out "Don't Know" from the pool and we are left with five categories. Thus there are five categories. Such categories make the response pattern variable an Ordinal variable. Because this is an ordinal variable, therefore you cannot apply the rules of a normally distributed variable to it. As I wrote before, there are two ways to deal with it to make things simple:

1. Convert the ordinal response variables to binary variables (something that you have done before). The risk of doing so is that you lose information contained within the categories.
2. You can treat these variables as if these were continuous variables and report for summary measures their mean values and their 95% confidence intervals.

If you choose to treat these variables as binary variables (that is values of 0 and 1 based on certain categories), then you will use the table similar to the one in Figure 2. Your outcome variable will be on the top and categories will in the columns; your explanatory variables will be in the rows, the categories of the explanatory variables will be in the second column, you will report N and %s, and the pvalues based on their chi-square tests in the last column.

```
# Here are the R codes for writing a bivariate table
# this is for a table assuming that it has five categories
# for y variable, you will need to adjust for other
# number of categories

bivtable <- function(x,y){
  tab1 <- table(x,y)
  tab2 <- round(prop.table(tab1, 1)* 100, 2)
  pval <- prop.test(tab1)$p.value
  tab3 <- cbind(tab1[,1], tab2[,1],
                tab1[,2], tab2[,2],
                tab1[,3], tab2[,3],
                tab1[,4], tab2[,4],
                tab1[,5], tab2[,5])
  tab4 <- cbind(tab3, pval)
  return(tab4)
}

```
Then, when you need to put that into the document, you will need to call it with each pair of variables as follows:

```
bivtable(var1, var2)

```
where var1 is your explanatory variable and var2 is your outcome variable. For example, if you wanted to test Age (categorical variable) with a question, say "Q6", you will do

```
bivtable(Age, Q6)

```

If you choose to treat these variables as continuous variables, then you would need to report Analysis of Variance (or ANOVA) in the bivariate set of tables for these variables.

(I will write more about how to do ANOVA and Correlation Matrix in the next post).  
