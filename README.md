# March-Madness

## Contributors
Zach, Blen, Dawit, Shaheer

## Introduction
We will attempt to predict the winner of the NCAA Division 1 Men's Basketball Tournament more popularly known as March Madness.

## Data Dictionary 
1. KenPom efficiency: 
2. Free Throw:
3. Turn over:
4. Match up Data:

## Data Cleaning
team_data <- df %>%
  select(SEED, TEAM, KENPOM.ADJUSTED.EFFICIENCY, FREE.THROW.., TURNOVER..) %>%
  arrange(SEED, TEAM, KENPOM.ADJUSTED.EFFICIENCY, FREE.THROW.., TURNOVER..)

south_region <- team_data %>%
  filter(TEAM %in% c("Alabama", "Arizona", "Baylor", "Virginia", "San Diego St.", "Creighton", "Missouri", "Maryland", "West Virginia", "Utah St.", "North Carolina St.", "College of Charleston", "Furman", "UC Santa Barbara", "Princeton", "Texas A&M Corpus Chris")) %>%
  distinct()

midwest_region <- team_data %>%
  filter(TEAM %in% c("Houston", "Texas", "Xavier", "Indiana", "Miami FL", "Iowa St.", "Texas A&M", "Iowa", "Auburn", "Penn St.", "Pittsburgh", "Drake", "Kent St.", "Kennesaw St.", "Colgate", "Northern Kentucky")) %>%
  distinct()

west_region <- team_data %>%
  filter(TEAM %in% c("Kansas", "UCLA", "Gonzaga", "Connecticut", "Saint Mary's", "TCU", "Northwestern", "Arkansas", "Illinois", "Boise St.", "Arizona St.", "VCU", "Iona", "Grand Canyon", "UNC Asheville", "Howard")) %>%
  distinct()

east_region <- team_data %>%
  filter(TEAM %in% c("Purdue", "Marquette", "Kansas St.", "Tennessee", "Duke", "Kentucky", "Michigan St.", "Memphis", "Florida Atlantic", "USC", "Providence", "Oral Roberts", "Louisiana Lafayette", "Montana St.", "Vermont", "Fairleigh Dickinson")) %>%
  distinct()
