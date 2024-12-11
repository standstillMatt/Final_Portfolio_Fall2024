# Is it Worth it to Fire Your Coach in the NFL?  
## Group Members  
Matt Mascavage, Nik Greb, Owen Kim  
## Colab Worksheet  
Linked [here](https://colab.research.google.com/drive/17cAjFsPaYrHx-ixhsSl-JyjIttDtKu-J?usp=sharing)
## Introduction  
We created our own custom data set (linked here) by compiling statistics collected from a number of sources. The final data set contained the following info from the 2002 - 2023 NFL season (we chose this range because the 32nd team, the Texans, were added to the League in 2002):  
  *  **Year** - The season for that entry
  *  **Coach** - The head coach for that season  
     -  There will be separate entries if a coach was fired and replaced midseason, one entry for each coach
     -  This way, the rest of the data all applies to the team’s performance under that specific coach
  *  **Team** - The team for that entry  
  *  **Games Played** - The number of games played under that coach
  *  **Wins**
  *  **Losses**
  *  **Ties**
  *  **Win Percentage** - Calculated as wins/games
  *  **Points Scored**
  *  **Points Against**
  *  **Point Differential** - Points scored minus points against
 
Creating this data set was the bulk of the work for this project. We had to combine data from multiple sources and often had to enter the data manually (this was the case for every year where a team had multiple head coaches in a season).  

Once we had created the data set, the goal was to look at some of the different measures of a team’s performance and compare that to the changes in coaching. Some of the questions we were hoping to answer were:
  *  Does firing a coach and hiring a new one boost the team’s performance? Is it “worth it?”
  *  How do teams who change head coaches often compare in performance to teams that keep the same coach for a long period of time?  

Naturally, there are a lot of confounding factors at work, but we’re really just trying to capture the relationship between coaching changes and team performance.  

Data sources: (MLA citations at end of page)
 *  [NFL.com](https://www.nfl.com/stats/team-stats/) - This is the official NFL website and it had really complete (and reliable) statistics on team performance. We mostly used it to find each team’s record for all of the seasons and to catch tie scores for the “Tie” column.
 *  [pro-football-reference.com](https://www.pro-football-reference.com/years/2023/coaches.htm) - This source was used to find head coaches for each team for a given year. For years with a midseason firing, it showed the week that the firing occurred and how many wins each coach had that season. 
 *  [pro-football-reference.com](https://www.pro-football-reference.com/years/2008/index.htm) - For seasons with midseason firings, we used this data source to calculate “Points Scored” and “Points Against”, which were then used to find “Points Differential.” We used this data source to check game by game data for a team that had a midseason firing, manually calculating the “Points Scored” and “Points Against” from before and after the firing.
 *  [Wikipedia](https://www.wikipedia.org/) - We used wikipedia to make the coaches column, finding all of the coaches for each team for any given year. We would search “[NFL team] head coach history” and wikipedia would provide each head coach for the given team, and also the years when they were the head coach. Midseason firings were shown by two coaches in a single year.  

## Methods and Results  
The bulk of the time dedicated to this project went into finding the data that we wanted to analyze and creating a pristine dataset that we could then analyze through our Colab notebook. We searched for a long time at the beginning of this project looking for an importable data file containing NFL season data along with the names of the head coaches corresponding to the team and years that they coached, and could not find it. So what we decided to do instead was create our own datafile. It took a lot of time looking on the internet to find season and coach data for each team and each year from 2002 to 2023, but we feel it was worth it in the end as we did not have nearly any data cleaning and wrangling to do on the back end once we started our analysis and coding. One of the biggest challenges was determining how to handle seasons in which a team had multiple head coaches in one year. In those instances, we decided to have two rows for that season and team, one row for each head coach, with the teams record that season split up by their record under each head coach. This allowed us to look at some more specific questions such as if firing a head coach specifically in the middle of season makes a difference on team performance. Over the course of one season, the player composition of a team is largely unchanged, so in effect we are keeping more “variables” the same that could impact team performance, and attempting to single out whether a head coaching change makes a difference. The first plot we created was a preliminary scatterplot of the win percentages of NFL teams by number of head coaches they have had since 2002.

<img src="1st Plot.png" alt="Alt Text" />
 
Correlation Coefficient: c = -0.758

The scatter plot above is plotting each team’s total win percentage for each team on the y-axis, with the number of different coaches for each team on the x-axis. The correlation coefficient of -0.758 is showing a strong negative correlation between the two variables; when a team has more coaches, their total win percentage is lower compared to a team with less coaches. Clearly, teams that do not fire their coach as often tend to have more wins, as shown by our linear regression. But do the teams who do fire their coach actually get better following the firing? One way to answer this is by examining win totals of the coach's final seasons with a team compared to win totals in the coach's first seasons with teams. We do this in the following histograms and boxplots:  

<img src="2nd Plot.png" alt="Alt Text" />
Mean win percentage for new coaches (blue graph): 0.42  
Mean win percentage for last coaches (red graph): 0.324  

From these visualizations, we see that, although not guaranteed, teams generally improve in the season after the hiring of a new coach. The mean win percentage for new coaches rose by roughly 10% and even visually you can see the change in the distribution from the histograms. The box plots show that there is a wider range of win percentages among new coaches, but the range extends only in the positive direction compared to previous coaches. In summary, it is common, but not guaranteed, for a team’s win percentage to increase after the hiring of a new coach. This made us wonder what these values would look like for midseason firings, which usually happen in response to a bad start to the season.  

Now we filter the dataframe for only the years in which a team fired their coach in the middle of a season and plot those histograms and calculate their means to determine if there’s a difference in team performance in the middle of a single season by firing their coach, with most other characteristics (i.e. roster composition, assistant coaches, payroll, etc.) held roughly constant during the course of a single season.  

<img src="3rd Plot.png" alt="Alt Text" /> 

In the new Coach distribution, there are two coaches that coached exactly one game and each won that game. We removed those observations from the filtered observations and considered them outliers, the updated visualization is shown below.  

<img src="4th Plot.png" alt="Alt Text" /> 
Mean win percentage for old coaches (red graph): 0.254  
Mean win percentage for new coaches (blue graph): 0.356  

For these visualizations above, the data is only including teams and years when there was a midseason firing. Teams / years without a midseason firing are not included in this dataset. This data set is reduced from 746 observations to just 42. From these visualizations above, we can see that a team's win percentage increases, in most cases, when a team fires their coach in the middle of the season. We can see that in the red graphs, the data is grouped in the lower win percentage range, which makes sense because typically teams will fire their coach when the team is performing poorly, with the hopes that the team improves with a coaching switch. Whereas in the blue graphs, the range of win percentages is much more varied, but only in the positive direction.  

Another measurement of a team’s performance is point differential (points scored - points against). This gives a more complete picture of how a team’s wins and losses actually played out.  

<img src="5th Plot.png" alt="Alt Text" /> 

We can see, once again, that performance improves after the hiring of a new coach. There is an increase of roughly 30 in the mean point differential for teams after hiring a new coach. Ultimately, this leads to the findings below and helps us answer our question of, “Does firing a coach and hiring a new one boost the team’s performance?”  

## Conclusion  
Does firing a coach and hiring a new one boost the team’s performance? Is it “worth it?”
*  Yes, in most cases, it is worth it. Teams typically fire their coach when they are performing poorly, hoping that a coaching switch can change the trajectory of their team. From all of the graphs above that are showing a teams win percentage before and after a firing, we can see that teams have a lower win percentage before they fire their coach (regardless of if they fired their coach at the end of the season or in the middle of the season) than they do after they fire their coach. In other words, in most cases, teams improve after they fire their coach, regardless of when the firing occurred.

How do teams who change head coaches often compare in performance to teams that keep the same coach for a long period of time?
*  From the first graph above in the “Methods and Results” section, showing win percentage on the y-axis and number of head coach switches on the x-axis, we can see that teams with more head coach switches have a lower win percentage than teams with less head coach switches. The correlation coefficient of -0.758 tells us that there is a strong negative correlation between the two variables, when a team has more coaches, their total win percentage is lower compared to a team with less coaches. The patriots, who have only had one coaching switch between 2002 and 2023 have the highest total win percentage in this timeline. Whereas the raiders, who have had 13 different coaches between the same timeline, have the lowest total win percentage in the same timeline. Ultimately, teams who fire their coach more often perform worse than teams who do not change their coach as often.

There are a number of limitations to our analysis. For starters, we solely analyzed wins and points through our data, but there are a lot of other factors that contribute to a team’s success, particularly on the defensive side. Turnovers, and defensive stops, and passing yards are all crucial to a team’s performance, but our analysis really only captures the defensive side of the story in the “Point Differential” column. Additionally, our measures of team performance are all relative to the performance of other teams. If one team’s performance was constant, but the teams it played worsened the next season, it would seem like a coaching change actually improved performance when in reality this was due to the other factors.  

This study could be pushed further to analyze if it is worth it to fire your coach midway through the season in other sports. It would have to be with similar sports to football, where the coach actually has an impact on the performance of their team. Another sport where this study could potentially be used is soccer and basketball because both sports are similar to football in that they require strategic planning and certain adjustments before every game, depending on your opponent. Could also look at college football midseason firings. It would also be interesting to look at the following questions, which could likely be done with this dataset, maybe with some slight modifications: How often do teams with midseason firings make the playoffs, and how does this compare to teams with an end of season firing? How does a midseason firing impact future performance vs firing at the end of a season? Do teams with midseason firings or end of season firings typically do better in the following season (only the coaches who were newly hired, which did better in their first full season, a midseason fire or a fire after the season)?  

## Citations  
Contributors, NFL. “Official Site of the National Football League.” *NFL.Com*, NFL, 2004.

Palmer, Pete. “2023 NFL Coaches.” *Pro Football Reference*, Sports Reference, 2000.  

Pullis, Ken, and Pete Palmer. “2008 NFL Standings & Team Stats.” *Pro Football Reference*, Sports Reference, 2000. 

Wiki, Contributors. “Main Page.” *Wikipedia*, Wikimedia Foundation, 23 May 2001.
