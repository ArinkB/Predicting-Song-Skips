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

There were some duplicated tracks, because songs would appear in different playlists. Britney Spear's 'Baby One More Time' might appear in the Playlist '1990s' and 'Best of the 90s'. Additionally in the pulls some values did not transfer over, some rows which gathered nothing were dropped, while others that had some values, were manually filled based on their searchability. 

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

### Steps
- [x] Define the Problem
- [x] Gathering Data
- [x] Cleaning Data & Setting Target
- [x] EDA
- [ ] Modeling
- [ ] Conclusion
- [ ] Dependencies
- [ ] What's Next
- [x] Other Avenues
- [] Some Fun Libraries

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



