# RuggerBot.com

With the Rugby World Cup just around the corner, and the pot for the office SuperBru pool reaching a record high, we decided that the only way to test if predictions can really be accurate at all was to build a deep learning rugby world cup score predictor.

## Gathering the data
The first step of the process is to find some historical data. Luckily [espnscum.com](http://stats.espnscrum.com/statsguru/rugby/stats/index.html) has a great rugby statitics database with players, teams and matches going back to 1896. Using a scrapy spider built by [peloyeje](https://github.com/peloyeje) [here](https://github.com/peloyeje/map536-rugby-data-scraper) (Thanks  [peloyeje](https://github.com/peloyeje)!), with a few [tweaks](https://github.com/resourcedesign/map536-rugby-data-scraper) to get the players scraping properly, we managed to get a decent sample of matches and results, along with player stats for each match to work with.  

## Training the Model
Using our data we have experimented with a number of different machine learning solutions, and settled on using Google's [AI Hub](https://cloud.google.com/ai-hub/) , with our data queried from [Big Query](https://cloud.google.com/bigquery/).

## Selecting which data is important
Rugby's rules have changed significantly enough over the last few years for us to focus on matches from 2000 onwards. We may revisit this assumption at a later stage. That gave our dataset over 1500 matches to work with. We further limited it to the teams that are in the world cup.

### Model V1
Our first model only took into account which teams were playing, the date of the match, the venue and which players were playing.

While the results were better than guesses, we knew we could do better.

### Model V2
We figured that using a some sort of player ranking system might be able to improve the predictions, but unforfunately there isn't really a database that has historical rankings for players for the last 19 years. So we created a simple model for players, and gave them each a score based on factors we determined impacted players ability the most.

Instead of a date and time of the match, we used a season and month of the year, along with whether or not the match fell within a World Cup year.

This is the current deployed version the model

### Model V3
In the latest model we are currently finalising, we plug in all the historical data we have for each player in each position, and a couple of other bits of data we are experimenting with.


## Testing the model
After the model was tested and evaluted, we used it to predict the outcome of some of the warm up games, these were our results:


| Home | Away | Prediction (Home - Away) | Result | Win / Loss | Err |
| --- | --- | --- | --- | --- | --- |
|SA|Japan|18|34|Yes|-16|
|Scotland|Georgia|53.834|27|Yes|26.834|
|England|Italy|29.251|37|Yes|-7.749|
|New Zealand|Tonga|45.306|85|Yes|-39.694|
|Australia|Samoa|38.926|19|Yes|19.926|
|Ireland|Wales|10.379|9|Yes|1.379|

## More Info
For any questions, please feel free to contact us at info@resourcedesign.io



 
