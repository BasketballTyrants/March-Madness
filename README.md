# March-Madness

## Contributors
Zach, Blen, Dawit, Shaheer

## Introduction
We will attempt to predict the winner of the NCAA Division 1 Men's Basketball Tournament more popularly known as March Madness.

## Data Dictionary
The columns that we used were:
1. SEED: The seed number of the team in their regional
2. TEAM: The name of the team
3. KENPOM.ADJUSTED.EFFICIENCY: The mean number of their offensive and defensive efficiency during the regular season
4. FREE.THROW.PERCENTAGE: The team percentage of free throws made out of total free throw attempts during regular season
5. TURNOVER.PERCENTAGE: The number of times a team is likely to turn the ball over per 100 possessions

## Data Cleaning
1. Overall Data Frame
- team_data pulls the team, their seed, and the three variables we chose for analysis
```
team_data <- df %>%
  select(SEED, TEAM, KENPOM.ADJUSTED.EFFICIENCY, FREE.THROW.., TURNOVER..) %>%
  arrange(SEED, TEAM, KENPOM.ADJUSTED.EFFICIENCY, FREE.THROW.., TURNOVER..)
```



2. South Region
- Data frame the contains the team in the South Region and removes the duplicate values
```
#Select teams for the South Region and eliminate duplicates for clean data
south_region <- team_data %>%
  filter(TEAM %in% c("Alabama", "Arizona", "Baylor", "Virginia", "San Diego St.", "Creighton", "Missouri", "Maryland", "West Virginia", "Utah St.", "North Carolina St.", "College of Charleston", "Furman", "UC Santa Barbara", "Princeton", "Texas A&M Corpus Chris")) %>%
  distinct()
```

3. Midwest Region
- Data frame the contains the team in the Midwest Region and removes the duplicate values
```
#Select teams for the Midwest Region and eliminate duplicates for clean data
midwest_region <- team_data %>%
  filter(TEAM %in% c("Houston", "Texas", "Xavier", "Indiana", "Miami FL", "Iowa St.", "Texas A&M", "Iowa", "Auburn", "Penn St.", "Pittsburgh", "Drake", "Kent St.", "Kennesaw St.", "Colgate", "Northern Kentucky")) %>%
  distinct()
```

4. West Region
- Data frame the contains the team in the West Region and removes the duplicate values
```
#Select teams for the West Region and eliminate duplicates for clean data
west_region <- team_data %>%
  filter(TEAM %in% c("Kansas", "UCLA", "Gonzaga", "Connecticut", "Saint Mary's", "TCU", "Northwestern", "Arkansas", "Illinois", "Boise St.", "Arizona St.", "VCU", "Iona", "Grand Canyon", "UNC Asheville", "Howard")) %>%
  distinct()
```

5. East Region
- Data frame the contains the team in the East Region and removes the duplicate values
```
#Select teams for the East Region and eliminate duplicates for clean data
east_region <- team_data %>%
  filter(TEAM %in% c("Purdue", "Marquette", "Kansas St.", "Tennessee", "Duke", "Kentucky", "Michigan St.", "Memphis", "Florida Atlantic", "USC", "Providence", "Oral Roberts", "Louisiana Lafayette", "Montana St.", "Vermont", "Fairleigh Dickinson")) %>%
  distinct()

```
6. Power Ranking Metric
- This data frame pulled team and kenpom adjusted efficiency from team_data to rank the teams 1 to 64
```
#This is our power ranking metric that arranges all 64 teams in the tournament 1 to 64 in terms of their Kenpom Adjusted Efficiency regardless of seed
 
ranking_metric <- team_data %>%
  select(TEAM, KENPOM.ADJUSTED.EFFICIENCY) %>%
  filter(TEAM %in% c("Alabama", "Arizona", "Baylor", "Virginia", "San Diego St.", "Creighton", "Missouri", "Maryland", "West Virginia", "Utah St.", "North Carolina St.", "College of Charleston", "Furman", "UC Santa Barbara", "Princeton", "Texas A&M Corpus Chris", "Houston", "Texas", "Xavier", "Indiana", "Miami FL", "Iowa St.", "Texas A&M", "Iowa", "Auburn", "Penn St.", "Pittsburgh", "Drake", "Kent St.", "Kennesaw St.", "Colgate", "Northern Kentucky", "Kansas", "UCLA", "Gonzaga", "Connecticut", "Saint Mary's", "TCU", "Northwestern", "Arkansas", "Illinois", "Boise St.", "Arizona St.", "VCU", "Iona", "Grand Canyon", "UNC Asheville", "Howard", "Purdue", "Marquette", "Kansas St.", "Tennessee", "Duke", "Kentucky", "Michigan St.", "Memphis", "Florida Atlantic", "USC", "Providence", "Oral Roberts", "Louisiana Lafayette", "Montana St.", "Vermont", "Fairleigh Dickinson")) %>%
  distinct() %>%
  arrange(desc(KENPOM.ADJUSTED.EFFICIENCY)) 
```

<img width="1440" alt="Screen Shot 2023-03-25 at 9 22 06 PM" src="https://user-images.githubusercontent.com/118494123/227751818-bf78dfff-0fc5-4943-a9f6-c944a2a8d73a.png">

## Data Summary

## Data Analysis

1. ggplot: scatterplots

![image](https://user-images.githubusercontent.com/118494123/227757907-364857d3-d08a-453c-932f-47ca490489fa.png)

2. ggplot: bar charts

![image](https://user-images.githubusercontent.com/118494123/227757802-dd2d4b75-bc8b-4057-8b1c-2ae5d2ed49f2.png)

3. Correlation Matrix

4. Machine Learning Model


## Conclusion

Based on our model, we predict the winner of March Madness will be (blank)
