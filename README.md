# Ipl_SQL_Project

# 📚 Summary of IPL Analysis SQL File

# 1️⃣ Top 5 Players with the Most Player of the Match Awards
	
     # Identifies the top 5 players with the highest number of "Player of the Match" awards.
	    
     select player_of_match,count(*) as awards_count 
    	from matches 
    	group by player_of_match 
	    order by awards_count desc limit 5;
	
 * Insight:
     * Highlights consistent match-winners across IPL seasons.

# 2️⃣ Number of Matches Won by Each Team in Each Season
	
     #Counts the number of matches won by each team in every IPL season.
	   
     select season,winner as team,count(*) as matches_won 
    	from matches group by season,winner;
	
 * Insight:
     * Provides a season-wise breakdown of team performances, useful for identifying dominant teams.

# 3️⃣ Average Strike Rate of Batsmen in IPL
	
     # Computes the overall average strike rate of all batsmen.
	   
     select avg(strike_rate) as average_strike_rate 
    	from (
    	select batsman,(sum(total_runs)/count(ball))*100 as strike_rate
    	from deliveries group by batsman) as batsman_stats;
	
 * Insight:
     * Reflects the league’s scoring rate and helps compare individual performances.

# 4️⃣ Strike Rate of Individual Batsmen
	
     # Calculates the strike rate of individual batsmen based on their total runs and balls faced.
	   
     select batsman,(sum(total_runs)/count(ball))*100 as strike_rate
      from deliveries group by batsman;
	
 * Insight:
     * Identifies aggressive and consistent batsmen, helping teams with player selection.

# 5️⃣ Number of Matches Won Batting First vs. Batting Second
	
    # Compares the number of matches won by teams while batting first versus chasing.
	  
     select batting_first,count(*) as matches_won
    	from (
	          select 
             case when win_by_runs>0 then team1
	            else team2
	            end  as batting_first
	          from matches where winner!="Tie") 
	as batting_first_teams 
	group by batting_first;
	
 * Insight:
     * Analyzes trends and success rates of batting strategies.


# 🎯 Overall Summary:

* Player Insights: Highlights top performers in terms of runs, wickets, and match awards.

* Team Analysis: Analyzes team performance trends across seasons.

* Match Dynamics: Provides insights into winning strategies and umpiring trends.
