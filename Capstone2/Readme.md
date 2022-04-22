
## Capstone 2 - NFL Daily Fantasy Project

The motivation for this project was that I was active on FanDuel during the football season.
Daily fantasy sports can be a lot of fun! Can data science help me construct winning lineups?

### 1. Background on NFL daily fantasy contests
FanDuel has different ways of gambling on sports. One way is DFS (daily fantasy sports) where one chooses a roster of players.
You then win money if your chosen lineup scores enough points compared to other people's lineups.

Example: 10/17/21 was a Sunday, and week 6 of of the 2021 NFL season.
FanDuel had the following contest: "$30K Sun NFL Pooch Punt (150 Entries Max)"
Each lineup entry fee was $0.05. The total size of the entry pool was 658,727 entries!
I entered 4 different lineups for that contest. Here's one example entry:

![This is an image](https://github.com/mruston209/Springboard/blob/main/Capstone2/FanDuel_Entry_Small.jpeg)

### 2. Data Sources
I found RotoGuru, which has data on all 18 weeks of the season.
Here is the link to week 18 data:

http://rotoguru1.com/cgi-bin/fyday.pl?week=18&game=fd&scsv=1

Teams played 17 games during the 2021 season, up from 16 games previously.
Each team also gets one bye week during the season, when they don't play a game.
Thus, the regular season is 18 weeks long.
Any given Sunday, most teams are playing, with just 2-4 on bye that week.

### 3. Data Cleaning
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
-Kyler Murray (the Arizona Cardinals QB) had a salary of $9000 during week 3, when they played against the Jacksonville Jaguars.
-Patrick Mahomes (The KC Chiefs QB) had a salary of $9000 during week 6, when they played against the Washington Football Team.
-Josh Allen (The Buffalo Bills QB) had a salary of $9000 during week 9, when they played the Jacksonville Jaguars.

We note a positive correlation between FD salary and FD points scored.
However, there is a lot of variability here, and a high salary is not a guarantee of a high scoring QB.

Data for Running Backs, Wide Receivers, Tight Ends, and Defenses was cleaned in the same manner.
Just a few observations with missing fantasy salaries were removed from the data set.

### 4. Exploratory Data Analysis
Now that basic data cleaning is done, let's look at the relationship between salary and points scored in more detail.
We will do this for each position group separately (QB, RB, WR, TE, DEF).

Starting with Quarterbacks, here's a graphic showing every datapoint of salary vs. points scored and the best fit line.

![Image of QB data](https://github.com/mruston209/Springboard/blob/main/Capstone2/QB_data_after_cleaning.png)










