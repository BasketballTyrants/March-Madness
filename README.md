# March-Madness
![image](https://user-images.githubusercontent.com/118494123/227815119-ab045fa8-28dd-409b-a62b-dad2e5e651f2.png)

## Contributors👨‍👨‍👧‍👦
Zach, Blen, Dawit, Shaheer

## Introduction
We will attempt to predict the winner of the NCAA Division 1 Men's Basketball Tournament more popularly known as March Madness.

## Data Dictionary📖
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

## Data Summary

## Data Analysis

## 1. ggplot: geom smooth


- We did a geom smoooth visual for the Regions where the x variable is free throw percentage and the y variable is a team's turnover percentage
- This plot evaluates all teams on the same level, there is no weight assigned
- To properly read this visual, a team wants to be farthest to the right on the x variable and closer to the bottom on the y variable

![image](https://user-images.githubusercontent.com/118494123/227807535-31a099e4-f373-429b-9fbc-5525de91b608.png)

## 2. ggplot: Bar Charts

- Then we did a bar chart of the Regions that shows the team's Kenpom adjusted efficinecy compared to the rest of the region

<img width="1440" alt="Screen Shot 2023-03-26 at 6 02 53 PM" src="https://user-images.githubusercontent.com/118494123/227810390-c45cfbf4-8126-40d1-a0ef-326778346ea4.png">

## 3. Power Ranking Metric

- This data frame pulled team and kenpom adjusted efficiency from team_data to rank the teams 1 to 64
```
- This is our power ranking metric that arranges all 64 teams in the tournament 1 to 64 in terms of their Kenpom Adjusted Efficiency regardless of seed
 
ranking_metric <- team_data %>%
  select(TEAM, KENPOM.ADJUSTED.EFFICIENCY) %>%
  filter(TEAM %in% c("Alabama", "Arizona", "Baylor", "Virginia", "San Diego St.", "Creighton", "Missouri", "Maryland", "West Virginia", "Utah St.", "North Carolina St.", "College of Charleston", "Furman", "UC Santa Barbara", "Princeton", "Texas A&M Corpus Chris", "Houston", "Texas", "Xavier", "Indiana", "Miami FL", "Iowa St.", "Texas A&M", "Iowa", "Auburn", "Penn St.", "Pittsburgh", "Drake", "Kent St.", "Kennesaw St.", "Colgate", "Northern Kentucky", "Kansas", "UCLA", "Gonzaga", "Connecticut", "Saint Mary's", "TCU", "Northwestern", "Arkansas", "Illinois", "Boise St.", "Arizona St.", "VCU", "Iona", "Grand Canyon", "UNC Asheville", "Howard", "Purdue", "Marquette", "Kansas St.", "Tennessee", "Duke", "Kentucky", "Michigan St.", "Memphis", "Florida Atlantic", "USC", "Providence", "Oral Roberts", "Louisiana Lafayette", "Montana St.", "Vermont", "Fairleigh Dickinson")) %>%
  distinct() %>%
  arrange(desc(KENPOM.ADJUSTED.EFFICIENCY)) 
  
```
  
  <img width="1440" alt="Screen Shot 2023-03-25 at 9 22 06 PM" src="https://user-images.githubusercontent.com/118494123/227751818-bf78dfff-0fc5-4943-a9f6-c944a2a8d73a.png">

## 4. Correlation Matrix:

```
team_corr <- cor(df[,c("FREE.THROW..", "TURNOVER..", "KENPOM.ADJUSTED.EFFICIENCY")])
team_corr_df <- as.data.frame(team_corr)
team_corr_df$Var1 <- rownames(team_corr_df)
team_corr_melt <- reshape2::melt(team_corr_df, id.vars = "Var1")

Create heatmap using ggplot2
ggplot(team_corr_melt, aes(x = Var1, y = variable, fill = value)) +
  geom_tile() +
  scale_fill_gradient2(low = "blue", mid = "white", high = "red",
                       midpoint = 0, limit = c(-1,1), space = "Lab",
                       name = "Pearson\nCorrelation") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90, vjust = 1,
                                   size = 10, hjust = 1)) +
  coord_fixed()

```


![image](https://user-images.githubusercontent.com/118494123/227817530-d091a18d-c1ee-4fd4-bc6d-efcbd3921fe6.png)


## 5. Shinyapp


## Conclusion

Based on our model, we predict the winner of March Madness will be (blank)

