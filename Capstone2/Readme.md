
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










