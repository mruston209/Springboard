
# Capstone 2 - NFL Daily Fantasy Project

The motivation for this project was that I was active on FanDuel during the football season.
Daily fantasy sports can be a lot of fun! Can data science help me construct winning lineups?

## 1. Background on NFL daily fantasy contests
FanDuel has different ways of gambling on sports. One way is DFS (daily fantasy sports) where one chooses a roster of players.
You then win money if your chosen lineup scores enough points compared to other people's lineups.

Example: 10/17/21 was a Sunday, and week 6 of of the 2021 NFL season.
FanDuel had the following contest: "$30K Sun NFL Pooch Punt (150 Entries Max)"
Each lineup entry fee was $0.05. The total size of the entry pool was 658,727 entries!
I entered 4 different lineups for that contest. Here's one example entry:

![This is an image](https://github.com/mruston209/Springboard/blob/main/Capstone2/FanDuel_Entry_Small.jpeg)

## 2. Data Sources
I found RotoGuru, which has data on all 18 weeks of the season.
Here is the link to week 18 data:

http://rotoguru1.com/cgi-bin/fyday.pl?week=18&game=fd&scsv=1

Teams played 17 games during the 2021 season, up from 16 games previously.
Each team also gets one bye week during the season, when they don't play a game.
Thus, the regular season is 18 weeks long.
Any given Sunday, most teams are playing, with just 2-4 on bye that week.

## 3. Data Cleaning
The data was relatively clean, but not perfect.
For example, when looking at the QB's data, three points were missing salary values:

![Image of QB data](https://github.com/mruston209/Springboard/blob/main/Capstone2/QB_data_before_cleaning.png)

The three points on the left were simply deleted, as they were a very small percentage of the overall data.
After those three erroneous points were removed, we were left with the following QB data:

![Image of QB data](https://github.com/mruston209/Springboard/blob/main/Capstone2/QB_data_after_cleaning.png)

We note the following:
The minimum QB salary was $6000.
The maximum QB salary was $9000, though there were only 3 occurences with a QB salary of $9000.
In case you're curious:

* Kyler Murray (the Arizona Cardinals QB) had a salary of $9000 during week 3, when they played against the Jacksonville Jaguars.
* Patrick Mahomes (The KC Chiefs QB) had a salary of $9000 during week 6, when they played against the Washington Football Team.
* Josh Allen (The Buffalo Bills QB) had a salary of $9000 during week 9, when they played the Jacksonville Jaguars.

We note a positive correlation between FD salary and FD points scored.
However, there is a lot of variability here, and a high salary is not a guarantee of a high scoring QB.

Data for Running Backs, Wide Receivers, Tight Ends, and Defenses was cleaned in the same manner.
Just a few observations with missing fantasy salaries were removed from the data set.

## 4. Exploratory Data Analysis
Now that basic data cleaning is done, let's look at the relationship between salary and points scored in more detail.
We will do this for each position group separately (QB, RB, WR, TE, DEF).

### Quarterbacks
Starting with Quarterbacks, here's a graphic showing every datapoint of salary vs. points scored and the best fit line.
The right hand side of this graphic shows average score by salary, as well as the line of best fit through the data.

![Image of QB data](https://github.com/mruston209/Springboard/blob/main/Capstone2/QB_performance_linear.png)

Two things jump out:

* The data includes back-up QB's, who often don't play. They have lower salaries, but frequently score 0. This explains the low average score of the lowest-salaried QBs.
* The relationship between salary and average score appears to flatten out at the high end of the salary range.

Above about $8000 in salary, the relationship between salary and points scored appears to flatten out.

I also tried moving the 0 scores, as a proxy for removing back-up QBs. The take-away message was the same, however.

### Running Backs
Again we look at a graphic showing salary vs points scored, and the best fit line.

![Image of RB data](https://github.com/mruston209/Springboard/blob/main/Capstone2/RB_performance_linear.png)

Running Backs with a salary over $9000 are relatively rare, so there aren't a lot of datapoints on the right side of the plot.
It does appear that above the $8000 level, the relationship between salary and score is fairly flat, though there is significant variance in performance for players with salary over $8000.


### Wide Receivers
The graphic below shows salary vs points scored for Wide Receivers during the 2021 NFL season, as well as the line of best fit.

![Image of WR data](https://github.com/mruston209/Springboard/blob/main/Capstone2/WR_performance_linear.png)

Again, at the high end of Wide Receiver salaries, it appears the relationship between salary and score flattens out.
Most of the WR data points above $9000 in salary fall below the best-fit line.

### Tight Ends
We again look at the relationship between salary and points scored, this time for Tight Ends.

![Image of TE data](https://github.com/mruston209/Springboard/blob/main/Capstone2/TE_performance_linear.png)

Again for Tight Ends the data is sparse above a salary of about $7000.
However, I would say the relationship appears to flatten out for salaries over ~$7000.

### Defenses
Last, but not least, we look at Defenses and the relationship between salary and points scored.
The salary range for defenses is $3000 to $5200, with just a single observation at $5200. The next highest is $5000.
So, all but one Defense data point have salaries between $3000 to $5000 inclusive.

![Image of DEF data](https://github.com/mruston209/Springboard/blob/main/Capstone2/DEF_performance_linear.png)

In this case, the linear relationship doesn't seem to break down for higher salaries. The linear relationship between salary and average score appears to hold across the range of Defense salaries ($3000 to $5200).

### Home vs. Away
We expect home teams to do a little better than away teams, on average. Is this captured by player salaries? I.e. do players playing at home have slightly higher salaries on average than players playing on the road?
To attempt to answer this question, we look salaries by position, but split on home vs away.

![Image of Salaries by Position](https://github.com/mruston209/Springboard/blob/main/Capstone2/Salary_by_Position.png)

Average salaries by position are nearly identical Home vs. Away. Running Backs playing at home are slightly more expensive than Running Backs playing on the road: $5488 vs $5477. For the other four positions, average salaries are even closer.

Now, is there a difference in average performance?

![Image of Scores by Position](https://github.com/mruston209/Springboard/blob/main/Capstone2/Score_by_Position.png)

Yes, it does appear that there's a difference in average performance, home vs away.
The biggest difference appears to be for Defenses and QBs:
* Home Average for Defenses: 6.79
* Away Average for Defenses: 6.16
* Home Average for QBs: 14.08
* Away Average for QBs: 13.71

The differences are small, but it does appear that home Defenses and home QBs outperform road Defenses and road QBs, on average.


## 5. Feature Engineering
Next we look at Feature Engineering. We expect the biggest determinant of a given score to be the player's salary. We expect that despite the high variability, expected score should be an increasing function of salary. We also don't expect that this relationship is perfectly linear, as we saw in the Exploratory Data Analysis section.

Other factors that might be predictive:
* Recent player performance (This might not be fully captured by the weekly updated player salary)
* Opponent's recent performance against (Again, perhaps match-ups are not fully captured by each players' salary)
* Weather (I mention this as a possibility, but the dataset does not include weather info)

Variables related to recent player performance that I included:
* Last Points - The fantasy points scored by the player in the last week, and NaN for their first week in the dataset
* Last Salary - The player's fantasy salary last week, and NaN for their first week in the dataset
* Salary MA3 - The average of the current player salary and the previous 2 weeks' salaries. NaN if less than 3 weeks are available.
* Lagged Points MA3 - The average of the previous 3 weeks' points scored, not including the current week. NaN if less than 3 weeks of data are available.
* Salary CMA - The cumulative average of the player's salary from week 1 to the current week.
* Lagged Points CMA - The cumulative average of the player's weekly scores, not including the current week. NaN for the first week the player plays.
* Lagged Oppt Points - The sum of points given up to the player's position by the current opponent in the opponent's last game. NaN for the first week.
* Lagged Oppt Points CMA - The cumulative average of points given up to the player's position by the current opponent in the opponents previous games.
* Lagged Oppt Points MA3 - The average of points given up to the player's position by the current opponent over that opponent's last 3 games.

## 6. Modeling
* More Needed Here
* More Needed Here
* More Needed Here


## 7. 'Stacking' based on Position Correlations
Because of the nature of how fantasy points are scored, players on the same team will have positively correlated fantasy scores.
When a Quarterback does well, the Wide Receivers on that team will likely do well, too. To look into this, we rank the WR, RB, and TE positions based on fantasy salaries. The highest cost WR on a team on a given week will be given the label of 'WR1'. The second-highest cost WR on a team on a given week will be called 'WR2' and so on for RB's and TE's.
After pivoting the data so each row is a game and each column is the scores of QB, WR1, WR2, WR3, RB1, RB2, TE1, TE2, and Defense, we can investigate the correlation between positions.

Players at the same salary level will can share a ranking. For instance, two Wide Receivers at the same salary level could both be WR2 for a given week. So, when summarizing the data in the format mentioned above, we take the average WR2 score for that week.

![Heatmap of Correlations between Positions](https://github.com/mruston209/Springboard/blob/main/Capstone2/Correlations_Heatmap.png)

This heatmap tells us a lot about how players' scores are correlated. We see that Defensive scoring is not highly correlated with any of the offensive position scoring.

The highest correlation is between a QB and WR1. This correlation is nearly 0.40. Correlations between the QB and WR2 and WR3 are around 0.30, also significantly positive. The correlation between QB and TE1 scoring is also around 0.30.

So, what's the ideal amount of stacking? Should we take the QB, WR1, WR2, WR3, and TE1 all from the same team? Or is this too much stacking?
We can look at the ideal line-up each week and look at the number of different teams represented to get an idea for how much stacking is optimal.
























