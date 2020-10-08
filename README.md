# Would I Skip it?

*Capstone Final Project for DSI -- Data Classification Modeling and Visualization*
 ##### Arink Bertrand

 ### Define The Problem

 When listening to music, one of the main things that will make me skip a song is if the artist sings their own name at the beginning of the track. 

 Searching online I noticed that I am not the only one who cringes when hearing this.  Jason Derulo is one of these artists who has done it so much that someone decided to make a 57 minute long compilation video of Jason Derulo singing his own name.

<a href = 'https://www.youtube.com/watch?v=Ak-OUYwCbmo'> 57 minutes of Jason Derulo singing his own name </a>

### Gathering the Data

I gathered my data by doing API pulls from Spotify and Genius. The tracks/songs were pulled from Playlists created by Spotify. The lyrics for each song was pulled from Genius.

### Cleaning the Data & Setting my Target

There were some duplicated tracks, because songs would appear in different playlists. <a href='https://www.youtube.com/watch?v=oHg5SJYRHA0'> This song</a> might appear in the Playlist '1980s', 'All out 80s', '80s Rock Anthems' and 'Best of the 80s'. Additionally in the pulls some values did not transfer over, some rows which gathered nothing were dropped, while others that had some values, were manually filled based on their searchability. 

The target for my models to predict would be whether I would skip a song or not based on whether the artist has self-announced themselves in the beginning. The lyrics will be Vectorized and put through Natural Language Processing.

### Data Dictionary

The Final Dataframe before Vectorizing / Modeling:

|Column|Description|
|---|---|
|artists|Name of Artists on the Track|
|title|Song Title|
|popularity| Spotify Popularity in U.S. as of Oct 2020|
|explicit|Boolean whether the song contains explicit content|
|release_year|The year the album containing the track was released|
|lyrics|Song Lyrics|
|Skip|Boolean whether I am likely to skip song based on if artist has sung their own name near the beginning of the track |


### Exploratory Data Analysis

Notihing - I have horribly horribly failed in making my datasets work. I am trying to pull the appropriate data now. 
There are 8 Notebooks in this repo (1.1-1.5 are data acquisition between Spotify and Genius) (2.1 & 2.2 Is Data Cleanup)
(RESTART is trying to pull lyrics straight from Genius without the lyricgenius library)(untitled is where I am now)

- Where it went wrong:
    - I spent alot of time pulling the data from Spotify with the idea of matching the user behavior, I became attached to the work I put in pulling data, that I was unwilling to completely give it up.
    - I tried to use the dataset I had already built to add lyrics column. This became a mess because the Genius API was trying to match the artist and title exactly. I attempted to fix the issue, but the options were limited (re-doing the pull made no difference, and manually cleaning it took 3+ hours for 1700 rows, of which SOMEHOW there were still rows that needed cleaning after), John and I decided that the best would be to put a list of artists together and pull the lyrics independently of the data I had already built. 
    - Following John's suggestion and article share I started another notebook to gather lyrics for pre-selected artists, however I couldn't get the functions to work properly. (the Api would pull russian characters, or some dirty dirty lyrics, for band 'CAKE', looking at Genius there were 8+ tracks listed for CAKE, but the API would only pull 3 and only 1 of them belonging to Cake, if I set the song request to 10, it would fill the list as a repeat), this did not change between keepng the code as is (writing to .txt) or my small addition (gathering info to list to write to DF)
 - Where I am now:
     - Using the Lyricsgenius library I am making a call again to the Genius API with my selected artists and gathering the data that way. This method SHOULD not cause any issues, as all it will be matching is the artist name and pulling x number of tracks from them.
 
 

### Steps
- [x] Define the Problem
- [x] Gathering Data
- [x] Cleaning Data & Setting Target
- [ ] EDA
- [ ] Modeling
- [ ] Conclusion
- [ ] Dependencies
- [ ] What's Next
- [x] Other Avenues
- [ ] Some Fun Libraries

## Dependencies
- Python 3
- Numpy
- Pandas
- Matplotlib
- Seaborn
- time
- lyricsgenius
- spotipy

### Other Avenues
The initial plan was to get indepth insights of Spotify user behaviors and predict what makes the users skip songs. However due to scope limits on information availability at this time it was not possible. In attempting to do this:
- I gathered datasets from CrowdAI from a Skip Prediction Challenge that they hosted in 2018. the Data was provided to CrowdAI by Spotify and it contained user behaviour and audio features, however all identifiable information to the actual song and artist were removed.
- In an attempt to try and use this dataset, I pulled all Playlists created by Spotify (not users), pulled each track from the playlist and gathered all Audi Features for each track. I then compared a column from my gathered dataset to the Spotify supplied dataset to check for any matches.
- Due to minimal matches (6k in a dataset of 103k columns, based on 1 column, the number of matches would decrease as additional column values were matched.), I decided to pivot the skip prediction to a more personal one. Instead of predicting if users would skip, the model will predict if I will skip the song. 

Considering the reason I started this project was, the pivot of the Capstone direction was not a big one and still falls within the project idea.

### Some Fun Libraries
In addition to the usual libraries that make our Data Science world spin, I found these libraries to be very useful in this Capstone:
- <a href='https://pypi.org/project/email-notify-magic/'> Email Notify Magic </a>
    - Used for long running cells, will send you an email when cell has completed running.
- <a href='https://pypi.org/project/lyricsgenius/'> LyricsGenius </a>
    - Makes Genius API pulls easy
- <a href='https://spotipy.readthedocs.io/en/2.16.0/'> Spotipy </a>
    - Lightweight Python library for Spotify Web API    



