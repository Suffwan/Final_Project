--
  # Final_Project

--
  ## This project is an Analysis on NBA dataset 

* I took the NBA dataset from Kaggle.
* There were many tables given in that dataset but i selected only two tables for my analysis.
* In that dataset I selected two tables one is fact table and one is dimenssion table, My fact table is contain (games) table and my dimenssion table contain (game_info) table. 
* For the analysis on my dataset i perform all the analysis on MySQL. For the analysis I tried to do it in a way where I did the analysis on my two favoirte teams 
  ('Toronto Raptors vs Golden State Warriors'). 
* I tried to perfome some analysis on it to get some results. 
* Other approch i did for analysis is that I perform the analysis on all the teams and tried to get as much insights as I can from Dataset.


--
 # SQL analysis for Toronto Raptors Vs Golden State Warriors 

 * I have done few numbers of analysis to get insights from the dataset for Match against Toronto Raptors and Golden State Warriors.

 * This is the analysis to find, 'How many games Toronto Raptors won and lose in thier carrier'?
   ```sql
   SELECT
    team_name_home AS team_name,
    COUNT(CASE WHEN wl_home = 'W' THEN 1 ELSE NULL END) AS games_won,
    COUNT(CASE WHEN wl_home = 'L' THEN 1 ELSE NULL END) AS games_lost
FROM final_project.`game`
WHERE team_name_home = 'Toronto Raptors'
GROUP BY team_name_home;


 * This SQL code is to find Raptors performance for playing in Home and Away by calculating Avg points 
      ```sql
      SELECT
    team_name_home,
    AVG(pts_home) AS avg_home_points,
    AVG(pts_away) AS avg_away_points
FROM final_project.game
WHERE team_name_home = 'Toronto Raptors' 
GROUP BY team_name_home;


  * This SQL code is to find Golden State Warriors performance for playing in Home and Away by calculating Avg points 
      ```sql
      SELECT
    team_name_home,
    AVG(pts_home) AS avg_home_points,
    AVG(pts_away) AS avg_away_points
FROM final_project.game
WHERE team_name_home = 'Golden State Warriors' 
GROUP BY team_name_home;



  * This is the analysis to find, 'How many games Golden State Warriors won and lose in thier carrier'?
    ```sql
    SELECT
    team_name_home AS team_name,
    COUNT(CASE WHEN wl_home = 'W' THEN 1 ELSE NULL END) AS games_won,
    COUNT(CASE WHEN wl_home = 'L' THEN 1 ELSE NULL END) AS games_lost
FROM final_project.`game`
WHERE team_name_home = 'Golden State Warriors'
GROUP BY team_name_home;

  * This is the analysis to find, 'Toronto raptors Playing from Home vs Golden State Warriors Playing away and the winner for those matches'?
    ```sql
    SELECT
    g.game_date,
    g.team_name_home AS home_team,
    g.team_name_away AS away_team,
    gi.attendance,
    CASE
        WHEN g.pts_home > g.pts_away THEN g.team_name_home
        WHEN g.pts_home < g.pts_away THEN g.team_name_away
        ELSE 'Tie'
    END AS winner
FROM final_project.`game` g
JOIN final_project.`game_info` gi ON g.game_id = gi.game_id
WHERE g.game_date >= '2019-01-01' AND g.game_date <= '2019-12-31'
    AND (
        (g.team_name_home = 'Toronto Raptors' AND g.team_name_away = 'Golden State Warriors')
        );


  * PowerBi visual for these analysis
    ![image](https://github.com/Suffwan/Final_Project/assets/135911236/5fab3752-9849-4213-9c86-ec3d524ef30a)

-- 
  # Sql Analysis on rest of the teams and dataset

  * This analysis is to perform some other matrics in our dataset like the performance of other teams and Average win or loss rate for the teams.
   
  * To find out the Insights I have done analysis on SQL
   
  * This SQL code is to find Teams Performance Analysis and it will give out insights about which team has hightes avg.points, avg.rebounds and avg.assists
      ```sql
      SELECT
    team_name_home AS team_name,
    AVG(pts_home) AS avg_points,
    AVG(reb_home) AS avg_rebounds,
    AVG(ast_home) AS avg_assists
FROM final_project.`game`
GROUP BY team_name_home
ORDER BY avg_points DESC;

  * This SQL code is to find top 10 teams that played at home and score most points 
    ```sql
    SELECT
    team_name_home AS team_name,
    AVG(pts_home) AS avg_points_home
FROM final_project.game
WHERE YEAR(game_date) BETWEEN 2010 AND 2023
GROUP BY team_name_home
ORDER BY avg_points_home DESC
LIMIT 10;

  * This SQL code is to find top 10 teams that played at away and score most points 
    ```sql
    SELECT
    team_name_away AS team_name,
    AVG(pts_away) AS avg_points_away
FROM final_project.`game`
WHERE YEAR(game_date) BETWEEN 2010 AND 2023
GROUP BY team_name_away
ORDER BY avg_points_away DESC
LIMIT 10;

  * This SQL code is to find the teams that have score highest points in away and at home 
    ```sql
    SELECT
    team_name,
    MAX(pts_home) AS highest_points_at_home,
    MAX(pts_away) AS highest_points_away
FROM (
    SELECT
        team_name_home AS team_name,
        MAX(pts_home) AS pts_home,
        0 AS pts_away
    FROM final_project.game
    GROUP BY team_name_home

    UNION ALL

    SELECT
        team_name_away AS team_name,
        0 AS pts_home,
        MAX(pts_away) AS pts_away
    FROM final_project.game
    GROUP BY team_name_away
) AS combined_data
GROUP BY team_name;


  * This SQL code is to find the overview of the teams with the avg points per game and avg rebound per game 
    ```sql
    SELECT
    team_name_home AS team_name,
    AVG(pts_home + pts_away) AS avg_points_per_game,
    AVG(reb_home + reb_away) AS avg_rebounds_per_game
FROM final_project.game
GROUP BY team_name_home;

  * This SQL code is to find the overview of the teams with total wins and toal loss
    SELECT
    team_name_home AS team_name,
    SUM(CASE WHEN wl_home = 'W' THEN 1 ELSE 0 END) AS total_wins,
    SUM(CASE WHEN wl_home = 'L' THEN 1 ELSE 0 END) AS total_losses
FROM final_project.game
GROUP BY team_name_home;


* I have made a PowerBi dashboard to understand better wht results these analysis will give. I try to use different visuals to have better insights of the datasets.
    ![image](https://github.com/Suffwan/Final_Project/assets/135911236/64e56b6c-389c-462b-ae65-4b5d6d24a8a3)


    

   


