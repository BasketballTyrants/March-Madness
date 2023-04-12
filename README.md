# March-Madness
![image](https://user-images.githubusercontent.com/118494123/227815119-ab045fa8-28dd-409b-a62b-dad2e5e651f2.png)

## Contributors👨‍👨‍👧‍👦
Zach, Blen, Dawit, Shaheer

## Introduction
We will attempt to predict the winner of the NCAA Division 1 Men's Basketball Tournament more popularly known as March Madness. We maily used the KenPom Adjusted Efficiency as our metric to determine the winner of the Tournament. KenPom's Adjusted Efficiency is a metric that measures a team's overall strength and efficiency, taking into account factors such as strength of schedule and margin of victory. The higher a team's KenPom Efficiency, the stronger they are considered to be. Here's how this metric can be used to predict the winner of a tournament:

## Data Dictionary📖
The columns that we used were:
1. SEED: The seed number of the team in their regional
2. TEAM: The name of the team
3. KENPOM.ADJUSTED.EFFICIENCY: The mean number of their offensive and defensive efficiency during the regular season
4. FREE.THROW.PERCENTAGE: The team percentage of free throws made out of total free throw attempts during regular season
5. TURNOVER.PERCENTAGE: The number of times a team is likely to turn the ball over per 100 possessions

## Data Cleaning🧹

The initial dataset provided to us was a set of projections for the tournament, which included teams that did not make it to the actual tournament. To analyze the actual tournament results, we found a new dataset that included only the teams that were in the actual tournament and their actual seeds.
Therefore, we obtained a new dataset that was cleaned down to the actual teams in the bracket and their actual seeds. From this new dataset, we created four separate data frames for each region (South, Midwest, West, and East) by selecting the teams that belonged to each region and eliminating any duplicate values.
Each of these data frames contained the team's seed, name, and three variables that we chose for analysis: KenPom Adjusted Efficiency, Free Throw Percentage, and Turnover Percentage. These variables were selected because they are key metrics used in evaluating a team's performance in basketball. By cleaning and organizing the data in this way, we were able to focus our analysis on the actual teams that participated in the tournament and compare their performance based on these key metrics.
By selecting only the relevant data, we were able to eliminate extraneous information and focus on the factors that we believe are most important in predicting a team's success in the tournament. This allows us to more accurately compare the performance of each team in these specific categories and make a more informed decision on which team is likely to come out on top based on their statistical performance in these key areas.


## Data Analysis

## 1. Free Throw by Turn Over Rate

ggplot: geom smooth


We made a scatter plot with ggplot showing free throw percentage vs. turnover percentage for all tournament teams, colored by region. The plot includes a linear regression line and team names. To read the plot, teams want to be farthest right on the x-axis and closer to the bottom on the y-axis. The plot is faceted by region and includes various formatting options.The visual is showing a scatter plot of the relationship between the rate of turnovers committed by a team and their success rate at free throws. Each point on the plot represents a different team. The X-axis shows the turnover rate (i.e., the percentage of possessions that result in a turnover) and the Y-axis shows the success rate at free throws (i.e., the percentage of free throws made out of all attempts). The scatter plot allows us to visually identify any patterns or trends in the data. If there is a strong relationship between turnovers and free throws, we would expect to see the points cluster in a particular pattern. For example, if teams that commit more turnovers tend to have a lower success rate at free throws, we would expect to see the points form a downward sloping line. Conversely, if there is no relationship between turnovers and free throws, we would expect to see the points scattered randomly across the plot. 

![image](https://user-images.githubusercontent.com/118494123/227807535-31a099e4-f373-429b-9fbc-5525de91b608.png)

## 2. KenPom Adjusted Efficiency 

The Kenpom adjusted efficiency visual helps us in predicting the winner of a game by providing an estimate of the win probability for each team based on their seed and Kenpom adjusted efficiency. The higher the win probability, the more likely a team is to win the game. This is a visualization that shows the KenPom adjusted efficiency metric for each team in the NCAA basketball tournament grouped by region. The teams are grouped into four regions (South, West, Midwest, East) and their efficiency values are displayed in a bar chart for each region. The y-axis represents the KenPom adjusted efficiency value and the x-axis represents the team names. The y-axis labels are tilted for easier readability. The purpose of the visualization is to compare the efficiency of the teams across different regions of the tournament.


<img width="1440" alt="Screen Shot 2023-03-26 at 6 02 53 PM" src="https://user-images.githubusercontent.com/118494123/227810390-c45cfbf4-8126-40d1-a0ef-326778346ea4.png">

## 3. Power Ranking Metric

This data frame pulled team and kenpom adjusted efficiency from team_data to rank the teams 1 to 64
 ``` 
ranking_metric <- team_data %>%
  select(TEAM, KENPOM.ADJUSTED.EFFICIENCY) %>%
  filter(TEAM %in% c("Alabama", "Arizona", "Baylor", "Virginia", "San Diego St.", "Creighton", "Missouri", "Maryland", "West Virginia", "Utah St.", "North Carolina St.", "College of Charleston", "Furman", "UC Santa Barbara", "Princeton", "Texas A&M Corpus Chris", "Houston", "Texas", "Xavier", "Indiana", "Miami FL", "Iowa St.", "Texas A&M", "Iowa", "Auburn", "Penn St.", "Pittsburgh", "Drake", "Kent St.", "Kennesaw St.", "Colgate", "Northern Kentucky", "Kansas", "UCLA", "Gonzaga", "Connecticut", "Saint Mary's", "TCU", "Northwestern", "Arkansas", "Illinois", "Boise St.", "Arizona St.", "VCU", "Iona", "Grand Canyon", "UNC Asheville", "Howard", "Purdue", "Marquette", "Kansas St.", "Tennessee", "Duke", "Kentucky", "Michigan St.", "Memphis", "Florida Atlantic", "USC", "Providence", "Oral Roberts", "Louisiana Lafayette", "Montana St.", "Vermont", "Fairleigh Dickinson")) %>%
  distinct() %>%
  arrange(desc(KENPOM.ADJUSTED.EFFICIENCY)) 
  
```
Our power ranking metric arranges all 64 teams in the tournament 1 to 64 in terms of their Kenpom Adjusted Efficiency regardless of seed.This visualization is showing the win probability for each team based on their seed and KenPom adjusted efficiency rating. The stacked bar plot represents the win probability for each team, with each bar representing a different seed. The color of each segment within a bar represents the specific seed. The y-axis represents the win probability for each team, while the x-axis represents the team names. The graph title indicates that the win probability is based on both seed and adjusted efficiency. This visual provides a comparison of win probabilities among teams with different seeds and efficiency ratings. It can be used to identify teams with a higher likelihood of winning based on their seeding and adjusted efficiency rating. By comparing the win probabilities of each team, we can also identify the top contenders for the tournament and predict the likely winner. Additionally, the MOE value can help us to determine how confident we can be in our predictions, which is essential for making informed decisions.


  
  <img width="1440" alt="Screen Shot 2023-03-25 at 9 22 06 PM" src="https://user-images.githubusercontent.com/118494123/227751818-bf78dfff-0fc5-4943-a9f6-c944a2a8d73a.png">

## 4. Correlation Matrix

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

- This Shiny app is showing a scatterplot and correlation matrix heatmap of the teams data based on the region selected in the sidebar. The scatter plot  displays the relationship between free throw percentage and turnover percentage, with a linear regression line overlaid. The correlation matrix heatmap shows the correlation coefficients between free throw percentage, turnover percentage, and KenPom adjusted efficiency to predict the winner. The data displayed in the app is filtered based on the region selected in the sidebar. 

![image](https://user-images.githubusercontent.com/118494123/228384063-80d3f4bb-a970-44b3-9e2e-776068805f34.png)


## Conclusion

Based on our model, we predict the winner of March Madness will be Alabama.

