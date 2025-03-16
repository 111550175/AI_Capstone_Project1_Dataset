# AI_Capstone_Project1_Dataset
NYCU Spring 2025

## Dataset Documentation
### Data Type:  
1. numbers.csv: The data inside this .csv file is the number of go game number on the website
2. games_data.csv: The data in this file include game ID, black player, white player, result, and moves. To be more specifically, the game ID is the ID number of each go game, black and white player records the player's name of each game. The result notes who wins this game and how much does he/she/it win, the moves recorded every moves on the board of each game.  
3. cleaned_games_data_<150/200/final>.csv: This is the preprocessed dataset that has already removed some unreasonable data (e.g. the game that has no result), also the number on each filename show the maximum moves that this file record.  
4. game_board_info_<150/200/final>.csv: This .csv file is nearly same as cleaned_games_data_<150/200/final>.csv, but this dataset contains a new feature, final board, that convert the moves sequence into a 19x19 game board. (1: black, 2: white, .: empty)  
5. games_feature_<150/200/final>_new.csv: This three datasets extract the feature from the go game board. In these datasets, I extract four features: Board Diff, Corner Diff, Territory Diff, Liberty Diff. The first is board diff, it counts the difference between the numbers of white and black on the final board. Second, the corner diff records the subtraction of black and whites in four corners on the board. Third, the territory diff is actually not the accurate way that calculate the territory of each player. For similarity, I only use BFS to check whether the empty space is closer to black or white so as to decide which this space belongs to. Last but not least, the liberty diff counts the total liberty of both black and white, then minus them and get the feature.  

### External Source:
Every data was referred to the website: <https://www.101weiqi.com/chessbook/>, and I used web crawler to collect those data on this website.

### Amount and Composition:
The dataset I used in my training was: game_board_info_<150/200/final>.csv, and games_feature_<150/200/final>_new.csv.  

- game_board_info<150/200/final>.csv: 
    - Total Samples: 2233
    - Features: The final board situation of the game (19x19 array filled with "1"(black), "2"(white), and "."(empty) )
    - Target: Winner (W for white or B for black)
- games_feature_<150/200/final>_new.csv:
    - Total Samples: 2233
    - Features: Four numerical attributes (Board Diff, Corner Diff, Territory Diff, Liberty Diff)
    - Target: Winner (W for white or B for black)  

### The Condition You Set for Data Collection
The data is from different go game record of different competitions. And I only use web crawler to reach the data that I need on the website. Furthermore, I have extract some basic features that might be the factor that determines the final winner of the game. 

### The Process of Data Collection
1. Find the website that has huge amounts of chess manual of go.
2. Use a python code (web_crawler) to collect the game ID of the go game. 
3. Use those collected game ID to download the games' related data with python code (web crawler of course).
4. Cleaned up the unreasonable data that just collected, for example, remove the game that do not have the result. 
5. Construct the actual go game board with the information from raw data (moves sequence in this case).  
6. Utilize the created game board info. to extract the feature of each game play.  

### Examples:
- numbers.csv:  
    | Number |
    |--------|
    |     197|
- games_data.csv:
    | Game ID| Black Player| White Player| Result| Moves|
    | -------| ------------| ------------| ------| -----|
    |     197|      武宮正樹|      大場惇也|  B+0.5| "[""pd"", ""dd"", ..., ""ao""]"|  
- cleaned_games_data_<150/200/final>.csv (same as games_data.csv):
    | Game ID| Black Player| White Player| Result| Moves|
    | -------| ------------| ------------| ------| -----|
    |     197|      武宮正樹|      大場惇也|  B+0.5| "[""pd"", ""dd"", ..., ""ao""]"| 
- game_board_info_<150/200/final>.csv:
    | Game ID| Black Player| White Player| Result| Winner| Final Board|
    | -------| ------------| ------------| ------| ------| -----------|
    |     197|      武宮正樹|      大場惇也|  B+0.5|      B| ". . . . . . . . 1 . 2 . ., ..., 1 1 2 . ."|
- games_feature_<150/200/final>_new.csv:
    | Game ID| Black Player| White Player| Result| Winner| Board Diff| Corner Diff| Territory Diff| Liberty Diff|
    | -------| ------------| ------------| ------| ------| ----------| -----------| --------------| ------------|
    |     197|      武宮正樹|      大場惇也|  B+0.5|      B|          0|           -4| -2|           -4|