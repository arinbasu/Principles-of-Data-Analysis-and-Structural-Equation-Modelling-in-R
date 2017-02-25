## Principles of Data Analysis

First, read the data into your software. Here, we are going to use R. Load the data in csv format into R using the following code:

```mydata <- read.csv(“somedata.csv”, header = T)
```
The above code tells R to read a file in a CSV format and store the results in a data.frame. Most data contain a mix of four different types of variables. These are:

- Nominal Variables. — Variables whose levels can be named and therefore these levels are distinct from each other. Examples: “Name” as a variable where each name is unique and there is no rank order in the levels.
- Ordinal Variables. — Variables whose levels indicate an inherent rank order. Such variables include the different responses in a likert scale question. For example, almost all responses in your questionnaire are Ordinal Variables as these are based on a likert scale type question (“Strongly Agree” … “Strongly Disagree”)
- Interval Variables. — Variables whose values are expressed in whole numbers on a scale, and where we do not have a concept of an absolute null. For example,  age in years. An age of 0 does not mean someone is unborn or has “no age” or “ageless”.
- Ratio variables. — Variables whose values are numbers similar to interval variables and these numbers are on a scale, plus here is a concept of absolute zero, and indicate absence or null. Example: Temperature measured in Absolute Scale/Kelvin scale.

In your data set, all your variables are either Ordinal (Opinion Variables) or Nominal Scale (Age, Gender, SES). This knowledge is important because if you know this, you can select the right kind of analysis, and statistic.

## Plan of Analysis

## Univariate Analysis

Second, after you read the data, you will need to clean the data and present the statistic of the most important variables in your data set that you will be analysing one by one. This step in the data analysis is referred to as “univariate data analysis”. Depending on the type of your variable, you will choose your statistic accordingly.

```
| Type of Variable    | What to present             |
|---------------------|-----------------------------|
| Nominal and Ordinal | Total Count and Percentages |
| Interval and Ratio  | Total Count and Percentages |
```

For Nominal and Ordinal Variables you should present their total count and the percentage values. This is the code you use in R to generate them:

# For one variable, this is the code:

```
n <- table(x)
pct <- round(prop.table(n) * 100, 2)
n_and_pct <- c(n, pct)
```

Here, x is the variable, pct is percentage, and c() is a function that binds the two objects. You can do by hand for each variable in your data set or you can write a function at one time to accomplish this in R. Below, I have shown you a function that will take a variable x and will output the count and percentage:

# function to do univariate analysis of nominal and ordinal variables

```unitable <- function(x){
n <- table(x)
pct <- round(prop.table(n)*100, 2)
n_pct <- c(n, pct)
return(n_pct)
}
```

Note how to write a function in R:

1. Every function is contained in an object. In this example, that object is “unitable”. Then we declare that it is  a function and start with a variable.
2. We declare the variable on which we are going to work. This can be arbitrary, as in this example this is x. This “x” is the argument that must be passed to the function. The function then begins and closes with a pair of curly brackets.
3. Then you write the logic of the function. Here you can use as many other functions as you like.
4. Lastly, you end the function with a “return” statement to indicate what you want out of that function.
5. You can learn about any in-built function in R by using help(“name of the function”) or ?function name in the console.

You can now apply this function to your variables to produce their count and percentages. To do this, simply type:

unitable(name of your variable)

You will see that this will quickly become tedious to type the names of all the different variables one by one to produce a whole list of variables. Particularly, if you have 50 plus variables, you will not want to do that. Therefore, you will use another in-built function called “sapply”. So subset the data elements that are nominal or ordinal, and run the following function on that data frame or the subset:

```
list_of_results <- sapply(data frame, unitable)
```

When you do that, you will get a list of results. In one shot, you can get a list of counts and percentages of all your nominal and ordinal variables. Note that loosely, nominal and ordinal variables are also referred to as “categorical variables”.

For scale variables (interval and ratio variables), you will generate their mean and standard deviation. You will not have to write a function but it will be helpful. When you apply mean function to any object in R, remember to include the na.rm = T option, which means you instruct R to remove all missing values.

In summary, your first task is to produce a neat table of values for all relevant single variables (univariate statistics) one by one. For some, you will produce a simple table of N and %s, and for other you will just produce their mean and standard deviation.

This table will also contain how many values are missing for each of the categorical variables, and mean and standard deviation must be calculated after excluding missing values for the continuous variables.

## Bivariate Analysis

After you have done univariate analysis, you will need to report bivariate analysis. Bivariate analysis means that you will need to analyse two variables at a time. This time, you will need to be careful about two things:

1. Remember that you are actually now conducting a hypothesis test so you must carefully examine your assumptions and select only the most relevant variables for your study.
Think about your own case. You have collected information about age, gender, SES, other nominal variables, and a whole lot of questions using likert scale that are ordinal variables. Also, that you are interested to study adolescent alcohol attitude, parental attitudes, captured by the likert scale questions. Even though you have collected information on age and gender, and SES, it is not critical that you present age * gender as separate bivariate tables, this is not critical for your study.

Your hypotheses will be drawn from your theory. Only you can draw your hypotheses based on your theory.

This is a good time to think about your hypotheses and select your variables. In bivariate analyses, there are different classes of variables:


- Response or Outcome Variables. — Those variables that you will explain
- Explanatory Variables. — Those variables that you will USE to explain Outcome Variables

Note that there are different types of variables (Categorical or Continuous Variables), and now we have two different classes of variables.

2. The second thing that you should be careful is that your outcome variable should always be in the column (when it is a categorical variable), or on the top of a table, and your explanatory variables will ALWAYS be in the rows. What kind of analyses to do? Here is a chart that you will need to remember:
```
|               | Outcome           |  Variable           |
|----------     |-----------        |-----------          |
|Explanatory    | Continuous        | Categorical         |
| Continuous    | Linear Regression | Logistic Regression |
| Categorical   | ANOVA             | Cross Tables        |
```

In your case, you have four levels in your age variable, two levels in your gender variables, and so on. You can treat these as nominal variables. On the other hand, while it is correct to treat your opinion variables as Ordinal variables and therefore analyse their data accordingly, there are are two possibilities:

1. You can treat the opinion variables as continuous variables. If you do this, then you can use the opinion variables as if they are on a continuous scale. This way you can justify your use of confirmatory factor analysis and structural equation models for analyses.
2. You can also collapse the categories of the opinion variables with reasonable explanations and use them as categorical variables with two categories. That way these variables will become binary variables (with values 0 and 1) and you can use what is referred to as binary logistic regression. It will be up to you to collapse the categories to 0s and 1s for further analysis.

I will go over the steps where we will describe what you can do in order to convert your variables. But here are the rules to remember when you set up your bivariate data analysis:

1. Think in terms of your theory first and think which variables will make up the components of your theory. As your theory is that, parental communication styles will influence the adolescent's opinion or intention of their accessing alcohol before the age of 18 years (or legal age of drinking), therefore first of all, think which variables that you have used in your survey will capture these two ideas best. Make a list of those variables.
2. Next, you'd also like to use other variables as confounding variables that would explain the association between your explanatory variables and the outcome variables. In your case, these will be age of the student, their socioeconomic status, and gender.
3. Your analyses cannot be "fishing expeditions", rather, they'd all have to be well thought out and with a plan to analyse a given theory. In your case, the theory is that, parental attitudes or communication styles influence adolescents' life decisions. In a subsequent section, we will see that you can actually collapse the many variables to one or two single variables using exploratory and confirmatory factor analyses, but for now, we will keep some variables together and in the thesis, anyway, you will need to describe all variables and questions in the survey.

Review the conceptual diagram below to understand what I mean by confounding variable.
