# Analysis of Opinions on Same-Sex Relations

Ariana Olson, Emma Price

## Overview

Public opinion of same-sex relations has changed dramatically in recent years. What was in recent memory something that most people considered to be "always wrong" is now considered by most people to be "always right." This raises the question of how public opinion has changed. Have younger people, who did not experience the AIDs crisis and have grown up with gay role models sufficiently shifted how public opinion appears? Has everyone become less disapproving of same-sex relations overtime? Are young people consistently more accepting and then grow less so as they age? As well, how do demographics like sex, income, location, and religion effect this change in public opinion?

## The General Social Survey Dataset

The General Social Survey, or GSS, is one of the most frequently analyzed data sets in the social sciences. According to the [About page of the GSS website says](https://gssdataexplorer.norc.org/pages/show?page=gss%2Fabout),

> The General Social Survey (GSS) is a project of NORC at the University of Chicago, with principal funding from the National Science Foundation. Since 1972, the GSS has been monitoring societal change and studying the growing complexity of American society.

The codebook for the GSS can be found [here](https://gssdataexplorer.norc.org/documents#doc_441) It provides detailed information about the survey design and variables in the dataset.

### Sample Design

The GSS is sent to 5,200 randomly selected households each year, from which an adult is randomly chosen to respond. Each household represents about 50,000 other households. As well, data collection takes the form of one, 90 minute survey.

The survey contains a wide variety of information including demographic data, opinion on important debates, and more. From this data we selected variables that were specifically relevant to our Age-Period-Cohort analysis as well as demographic information related to the topic. This includes sex, inflation-adjusted income, various political views, martial status, education level, age, and religion.

After completing some exploratory data analysis we narrowed our selection of variables cutting out those that overlapped in content with other we selected (`divorce` and `martial` for example). And some that seemed less relevant (a number of variables connecting to other political opinions). We ultimately selected the variables that are shown below alongside their survey question.

Code | Label | Question
--- | --- | ---
`homosex`   | Homosexual sex relations | What about sexual relations between two adults of the same sex--do you think it is always wrong, almost always wrong, wrong only sometimes, or not wrong at all?
`year`   | GSS year for this respondent | N/A
`age`   | Age of respondent | N/A
`cohort`   | Year of birth | Birth cohort of respondent.
`sex`   | Respondents sex | N/A
`realrinc`   | Income in constant 1986 $ | Respondent's income on 1972-2006 surveys in constant dollars (base = 1986)
`polviews`   | Think of self as liberal or conservative | Where would you place yourself on a seven-point scale on which the political views that people might hold are arranged from extremely liberal--point 1--to extremely conservative--point 7
`relig`   | Religious preference | What is your religious preference? Is it Protestant, Catholic, Jewish, some other religion, or no religion?
`fund`   | How fundamentalist is respondent currently | Fundamentalism/Liberalism of Respondent's Religion
`marital`   | Marital status | Are you currently--married, widowed, divorced, separated, or have you never been married?
`res16`   | Type of place lived in when 16 yrs old | Which of the categories on this card comes closest to the type of place you were living in when you were 16 years old?
`reg16`   | Region of residence, age 16 | In what state or foreign country were you living when you were 16 years old?
`region`   | Region of interview | N/A
`attend`   | How often respondent attends religious services | How often do you attend religious services?

## Analysis
### Age-Period-Cohort
Generational analysis of public opinion can be broken down to look into period effect, cohort effect (effects due to the year that the respondent was born), and age effect (effects due to respondents aging). Completing an age-period-cohort analysis on the public opinion of same-sex relations allows us to identify which of those three items drives the change.

#### Period Effect
Period effects appear as changes across the respondents regardless of whatever groups they are broken down by, but not necessarily to the same amount.
##### Grouped by Age
Below are the graphs of the average disapproval and approval of same-sex relations each year within each age group. Across each year, all of the age groups are becoming more accepting of same-sex relations; however, the exact rate of change definitely varies across groups. Specifically, people who were in their 70s and 80s have a lower rate of change -- moving from about 10% to 20% and 30% accepting for people in their 70s and 80s, relatively. Comparatively, people who were in their 20s moved from 15% to 70% accepting, which is more than double that of older people. From these graphs there seems to be a period effect.
![Plot of 'always wrong' by grouped by age, plotted by year](images/age-year wrong.png)
![Plot of 'never wrong' grouped by age, plotted by year](images/age-year right.png)
##### Grouped by Cohort
Below are the graphs of the average disapproval and approval of same-sex relations each year within each birth decade. These plots are very similar to those in seen when grouped by age, but across all groups there is less change across all groups, each line is a little more flat and they move together a little more consistently. Indicating a period effect.
![Plot of 'always wrong' by grouped by cohort, plotted by year](images/coh-year wrong.png)
![Plot of 'never wrong' grouped by cohort, plotted by year](images/coh-year right.png)

#### Cohort Effect
Below is a graph of average opinion on same-sex relations within each birth year to check for a cohort effect. There is a definite, consistent in crease in people who approve of same-sex relation and decrease in people do disapprove as people are born in more recent years. This indicates a cohort effect.
![Plot of 'always wrong' and 'never wrong' grouped plotted by cohort](images/all_bycohort.png)

#### Age Effect
Age effects indicate that there are differences across generations regardless of cohort and survey year. Age effects appear as changes where all groups move together.
##### Grouped by Year
The graphs below plot the average opinion toward same-sex relations for each age of each seven year grouping. In the same-sex relations is never wrong graph there is a fairly consistent decrease for all ages, but the changes do not move at the same rate within the different 7-year groups. Within the same-sex relations are always wrong graph, the percentages vary in a really inconsistent way across ages from year-to year. $$$$$$$$$$$$$$$$$$$$$
![Plot of 'always wrong' grouped by cohort, plotted by age](images/year-age wrong.png)
![Plot of 'never wrong' grouped by cohort, plotted by age](images/year-age right.png)
##### Grouped by Cohort
Below are the graphs of the average percentage of disapproval (left) and approval (right) of same-sex relations within birth decade, and plotted against the age that the respondents were when they took the survey. Across the decade $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
![Plot of 'always wrong' grouped by cohort, plotted by age](images/coh-age wrong.png)
![Plot of 'never wrong' grouped by cohort, plotted by age](images/coh-age right.png)


### Logistic Regression

To better understand the trends in the data, we created a logistic regression model using a handful of variables we determined influenced whether or not a respondent thought that homosexual sex was wrong or not. The model predicts the likelihood that a respondent thinks that homosexual sex is always wrong. In making this model, we only took into consideration respondents who answered 'Not Wrong at All' or 'Always Wrong'. This is because we needed to model a binary choice. It is worth noting that the majority of respondents who answered this question gave one of these two answers.

The explanatory variables we chose to use in this model are:

1. `year`: The survey year.
2. `cohort`: The year the respondent was born in.
3. `sex`: The sex of the respondent.
4. `reg16`: The region the respondent lived in when they were 16.
5. `relig`: The respondent's religion.
6. `attend`: The frequency with which the respondent attends religious services.

We chose to use these variables in the model to capture several trends that we found during variable exploration.

#### Region

![Plot of 'always wrong' by reg16](images/reg16_proportions_always.png)
![Plot of 'never wrong' by reg16](images/reg16_proportions_never.png)

![Logistic regression plot of reg16](images/reg16_log.png)

#### Religion
We first looked at how the religion of the respondent influenced the likelihood that they would believe homosexual sex was always wrong. We expected to see that Protestant and Catholic respondents were most likely to say that homosexual sex was always wrong, and that Jewish respondents were least likely to answer this way. This is based on the answers for each group in the GSS data. These patterns can be seen below.

![Plot of 'always wrong' by religion](images/relig_proportions_always.png)
![Plot of 'not wrong at all' by religion](images/relig_proportions_never.png)

For this analysis, we generated predictions for each of the 5 most popular religions that respondents reported in the GSS over a range of survey years. These religions are Protestant, Catholic, Jewish, "Other", and "None". All other explanatory variables were held constant. The plot below shows the results.

![Logistic regression plot of relig](images/relig_log.png)

As expected, the model predicts that Protestants are most likely to say that homosexual sex is always wrong while Jewish respondents are least likely. The trend for all groups is negative as year increases. The differences in likelihoods among groups stays fairly consistent year to year, except when the likelihoods approach the asymptotes of 1.0 and 0.0.

#### Frequency of Attendance of Religious Services

![Plot of 'always wrong' by 'attend'](images/attend_proportions_always.png)
![Plot of 'never wrong' by 'attend'](images/attend_proportions_never.png)

![Logistic regression plot of 'attend'](images/attend_log.png)

#### Survey Year

![Plot of 'always wrong' year vs cohort](images/cohort_by_year_always.png)
![Plot of 'never wrong' year vs cohort](images/cohort_by_year_never.png)

![Logistic regression plot of year](images/year_log.png)

## Conclusion

- Survey year matters a lot
- general trend toward acceptance
- any holdout groups or major predictive variables other than survey year
