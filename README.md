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



