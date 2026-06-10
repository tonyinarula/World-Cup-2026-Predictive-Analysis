# World-Cup-2026-Predictive-Analysis

## Overview
This project uses data analytics, machine learning, and the Monte Carlo prediction technique to determine potential winners of the 2026 World Cup hosted by the US, Canada, and Mexico. 

## Objectives
- Predict match outcomes using historical data
- Build features useful in separating winning teams from ones that lose
- Build a logic to simulate the World Cup seeding, particularly the third place seeding
- Estimate probabilities of winning the final through Monte Carlo simulation

## Tools
Python (numpy, pandas, os, scikit-learn, fifacodes, Counter)

## Key Insights

- Spain and Morocco emerged as the most likely champions in simulation.
- Recent team performance metrics had greater predictive power than FIFA rankings alone.
- Confederation-adjusted statistics reduced inflation caused by uneven qualification schedules.
- Tournament path and group placement significantly affected championship probabilities.

## Data
- Kaggle World Cup dataset [https://www.kaggle.com/datasets/harrachimustapha/fifa-world-cup-team-dataset?select=test.csv]
- jfjelstul github for past World Cup match data [https://github.com/jfjelstul/worldcup/tree/master]
- For countries not included in the Kaggle dataset (Angola, Togo, Trinidad and Tobago, Honduras), data was manually entered and found from the following sources:
  - pre-tournament FIFA rankings and points: https://inside.fifa.com/fifa-world-ranking/men?dateId=id145
  - goals scored/concedd last 4y, wins/draws/losses last 4y were calculated by adding the 4 calendar years prior to the tournament year from: https://www.11v11.com/
  - World Cup titles before and is_host were all entered as 0.
- areezvisram12 Kaggle for 2026 World Cup match data [https://www.kaggle.com/datasets/areezvisram12/fifa-world-cup-2026-match-data-unofficial]
- Third place seed combinations were sourced from the FIFA tournament regulations, Annex C [https://digitalhub.fifa.com/m/636f5c9c6f29771f/original/FWC2026_regulations_EN.pdf]
- Team confederation info was found at the 538 Kaggle dataset: [https://www.kaggle.com/datasets/fivethirtyeight/fivethirtyeight-fifa-dataset]

## Data Cleaning
I cleaned each table of the Kaggle dataset and jfjelstul dataset by filtering to only men's World Cups from the last 6 tournaments, and filtering on the features I would use in my analysis. 
Additional feature engineering includes:
- Average squad age at time of tournament
- Difference between home and away sides' avg squad age
- Difference between home and away sides' FIFA points
- Difference between home and away sides' FIFA ranking

## Modeling
### Target Variable
Match outcome:
- Home win
- Draw
- Away win

### Model
Random forest classifier (scikit-learn)

### Evaluation Metric
The model used training data from 2002-2018 to predict 2022 results.
away_team_win precision: 0.44
away_team_win recall: 0.5
draw precision: 0.5
draw recall: 0.1
home_team_win precision: 0.54
home_team_win recall: 0.62

## Tournament Simulation
Simulation process:
1. Simulate all group-stage matches
2. Calculate group standings
3. Determine advancing teams
4. Apply FIFA's third-place advancement rules
5. Simulate knockout rounds
6. Record tournament winner

The tournament was simulated 2500 times.

## Limitations
- FIFA rankings may not fully capture current squad strength.
- Injuries and roster changes are not modeled; aside from average squad age, no player-specific data is included.
- Match predictions rely on historical data and may not reflect future tactical changes.
- Confederation strength adjustments are approximations.
- Morocco is likely overweighted by the model due to easier confederation-specific games it plays throughout the year.
