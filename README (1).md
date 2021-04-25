Personal Dataset Project by YuTung Cheng (ID:11678647)

DATA 115 Spring Semester

Date 4/24/2021

# US-presidential-election-2020
## Motivation

## Data Sources

Election results data is collected from [Zenodo open access database](https://zenodo.org/record/3975765#.YIWwUH0zb0o). Both 2016 and 2020 results are downloaded.

Combined with census data provided by [US Census Bureau](https://www.census.gov/acs/www/data/data-tables-and-tools/data-profiles/), we can get the full picture of election results by state.

## Processing Steps
There are two main steps. The first step is cleaning data and the second step is joining two sources of data.

I dealt with census data first. Original data contains more than 100 variables at all. So I glimpse at them and hand-pick interesting variables that might have impact on election results. Since variables are recorded as raw value, I turned them into meaningful percentage to smooth the population difference on the state basis.

Then I dealt with election results data. There is a small problem for 2016 data. It doesn't have full state name so I searched for state abbreviation data and filled the full name. Also, I calculate voting percentage of each party. 

After data cleansing part, I joined census data to election results using state name as primary key. I double checked that there isn't any data duplication or missing value issue. Last but not least, I calculate vote percentage difference between 2020 and 2016 for both parties as an indicator.

## Visualization

I mainly used scatter plots to visualize relationships between variables I am interested in and election results. Both uni-variable and multi-variable scatter plots were used since I wanted to take more than one variable's impact into consideration.

From the plots below, I used Republican Party votes percentage, abbreviated as gop, as my y against other variables. Also, I used point size and point color to further compare the difference.

![race - black and gop]
(https://github.com/Jennnnnnn8133/US-presidential-election-2020/blob/main/final/image/plot_race_one_black.png)

![household - spouse and gop]
(https://github.com/Jennnnnnn8133/US-presidential-election-2020/blob/main/final/image/plot_household_spouse.png)

![education - bachlor and gop]
(https://github.com/Jennnnnnn8133/US-presidential-election-2020/blob/main/final/image/plot_bachelor.png)

![age - 85up and gop]
(https://github.com/Jennnnnnn8133/US-presidential-election-2020/blob/main/final/image/plot_pop_85_up.png)

## Analysis

I trid to use logistic regression to build a descriptive model. The independent variable include marital status, gender composition, age composition, race composition, household composition, educaitional attainment, and 2016 election results. The dependent variable is 2020 election results, and I choose gop vote percentage.

I kicked out several variables to prevent the redundant issue. For example, I only kept male percentage of all population and ruled out female percentage of all population. Additionally, I didn't include change percentage since it may be some data linkage and not be good for describe my data.

From the summary of my model, I noticed that p-value of my variables are large, which indicated that significance level of these variables are not significant. It was understandable since voting behavior is complex, complicated, and may be individual. The global trend is not easy to catch, not to mention the limit of these variables. Using data with static but not diverse, state but not smaller scale such as county, demographic and socioeconomic but not some election related, variables, lessen the explainability of my model.

## Descriptions of Code and Materials

### Data
The raw data downloaded from the sources described above are uploaded in .csv form. There are five .csv can be found in my Github repo, which is 2016 US County Level Presidential Results, 2020 US County Level Presidential Results, states abbreviation, social characteristics, demographic and housing data.

### Code
As I mentioned above, there are pars. The first part is data importing. I use `read_csv()` to import data. The second part is data munging and I use `dplyr` verb to transform and clean them. The third part is data joining and `left_join()` is used. The fourth part is visualizing data with `ggplot()`. The fifth part is using `glm()` from `caret`.

## References
[1] https://www.macromicro.me/collections/2809/us-2020-general-election
[2] https://web.cw.com.tw/us-2020/latest/index.html
[3] https://github.com/tonmcg/US_County_Level_Election_Results_08-20/
[4] https://www.census.gov/acs/www/data/data-tables-and-tools/data-profiles/
[5] https://github.com/jasonong/List-of-US-States/blob/master/states.csv



