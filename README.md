# When-Was-the-Golden-Era-of-Video-Games-
![e1a2cc98-afb8-43d7-9cbc-7c3d128ab1c2](https://github.com/user-attachments/assets/a4258af5-2eca-41e7-bdbe-8cd644bcd6d4)


Video games are big business: the global gaming market is projected to be worth more than $300 billion by 2027 according to Mordor Intelligence. With so much money at stake, the major game publishers are hugely incentivized to create the next big hit. But are games getting better, or has the golden age of video games already passed?

In this project, you'll analyze video game critic and user scores as well as sales data for the top 400 video games released since 1977. You'll search for a golden age of video games by identifying release years that users and critics liked best, and you'll explore the business side of gaming by looking at game sales data.

Your search will involve joining datasets and comparing results with set theory. You'll also filter, group, and order data. Make sure you brush up on these skills before trying this project! The database contains two tables. Each table has been limited to 400 rows for this project, but you can find the complete dataset with over 13,000 games on Kaggle.


game_sales table
Column	Definition	Data Type
name	Name of the video game	varchar
platform	Gaming platform	varchar
publisher	Game publisher	varchar
developer	Game developer	varchar
games_sold	Number of copies sold (millions)	float
year	Release year	int
reviews table
Column	Definition	Data Type
name	Name of the video game	varchar
critic_score	Critic score according to Metacritic	float
user_score	User score according to Metacritic	float
users_avg_year_rating table
Column	Definition	Data Type
year	Release year of the games reviewed	int
num_games	Number of games released that year	int
avg_user_score	Average score of all the games ratings for the year	float
critics_avg_year_rating table
Column	Definition	Data Type
year	Release year of the games reviewed	int
num_games	Number of games released that year	int
avg_critic_score	Average score of all the games ratings for the year	float


-- Ten best_selling_games
select * 
from game_sales 
order by games_sold desc
limit 10

[datalab_export_2025-09-09 14_10_17.xlsx](https://github.com/user-attachments/files/22230024/datalab_export_2025-09-09.14_10_17.xlsx)


-- Highest average critics_top_ten_years
select 
    gs.year, 
    count(gs.name) as num_games, 
    round(avg(rv.critic_score),2) as avg_critic_score
from game_sales gs
inner join reviews rv
    on gs.name = rv.name
group by gs.year
having count(gs.name) > 4
order by avg_critic_score desc
limit 10

[datalab_export_2025-09-09 14_10_43.xlsx](https://github.com/user-attachments/files/22230041/datalab_export_2025-09-09.14_10_43.xlsx)


-- Golden_years

select 
	uay.year, 
	uay.num_games, 
	cay.avg_critic_score, 
	uay.avg_user_score, 
	(uay.avg_user_score - cay.avg_critic_score) as diff
from users_avg_year_rating uay 
	inner join critics_avg_year_rating cay
	on uay.year = cay.year
	where cay.avg_critic_score > 9 or uay.avg_user_score > 9
order by uay.year

[datalab_export_2025-09-09 14_11_35.xlsx](https://github.com/user-attachments/files/22230050/datalab_export_2025-09-09.14_11_35.xlsx)
