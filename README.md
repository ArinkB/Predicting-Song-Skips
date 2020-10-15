# Would I Skip it?

*Capstone Final Project for DSI -- Data Classification Modeling and Visualization*
 ##### Arink Bertrand

 <h2><b> This Project is in Progress<span style="font-size:200%;color:red;">&star;</span> </h3><a id='model'></b></h2> 

 <h3>Define the Problem</h3><a id='obj'></a>

 When listening to music, one of the main things that will make me skip a song is if the artist sings their own name at the beginning of the track. 

 Searching online I noticed that I am not the only one who cringes when hearing this.  Jason Derulo is one of these artists who has done it so much that someone decided to make a 57 minute long compilation video of Jason Derulo singing his own name.

<a href = 'https://www.youtube.com/watch?v=Ak-OUYwCbmo'> 57 minutes of Jason Derulo singing his own name </a>

| Navigation | Description |
| --- | --- |
| Notebook ||
|  | [Data Acquisition](./1_Data%20Acquisition.ipynb)|
|  | [Data Cleanup](./2_Data%20Cleanup.ipynb)|
|  | [EDA](./3_EDA.ipynb)|
|  | [Models](./4_Model.ipynb)|
|ReadMe  | |
| | [Define the Problem](#obg)|
| | [Gathering the Data](#gather)|
| | [Cleaning and Target](#clean)|
| | [Data Dictionary](#dict)|
| | [Exploratory Data Analysis](#eda)|
| | [Model](#model)<span style="font-size:200%;color:red;">&star;</span> </h3><a id='model'>|
| | [Dependencies](#depend)|
| | [What's Next](#next)|
| | [Some Fun Libraries](#fun)|


<h3> Gathering the Data</h3><a id='gather'></a>

I gathered my data by doing API pulls from Spotify and Genius. Initially the tracks/songs were pulled from Playlists created by Spotify. The lyrics for each song was pulled from Genius. It became difficult to pull lyrics from Genius while matching the artist name and song, so I changed my approach to selecting 128 artists and pulling songs with lyrics from each artist. Most artists have 100 tracks in my dataset.

<h3> Cleaning the Data & Setting my Target</h3><a id='clean'></a>

Because I requested 100 tracks from each artists, the likeliness of getting duplicates was set. After Genius iterated though songs for the artist, it attempted to fill the requirements with Remixes or different 'versions', but the lyrics were still the same. An example of this was Fischerspooner's Emerge that appeared 10 times, because there were different Remixes, and although instrumental they may have been slightly different, lyrically they were the same. 

Other categories that were dropped, were songs that were instrumental only (no lyrics), artists such as Diplo, MGMT had a lot of these, Christina Perri also does lullabies, so there were a few of those in the list as well. 

Once the rows that needed to be dropped were dropped, I moved on to string cleaning, removing line breaks (/n) and unicode that got embedded in the lyrics in the pull. The media column and featured column came in as html dictionaries that were actually strings. I extracted the necessary information from these using Regex, created an alias column to help identify artists in lyrics (Pitbull calls himself Mr. Worldwide and Mr. 305)

To get the target column I would iterate through the lyrics column, and check if any of the values in the Artist, Featured or Aliases columns were in the lyrics, if true the target would be set to 1 if not then 0.

I then called the Spotify API to fill in the release year for the tracks and create a new column for track explicit.

<h3> Data Dictionary</h3><a id='dict'></a>

The Final Dataframe before Vectorizing / Modeling:

|Column|Description|
|---|---|
|artist|Name of Artist on the Track|
|featured|Name of Artists Featured the Track|
|aliases|Other names the Artist or Featured Artists use, includes first name last name split|
|title|Song Title|
|track_id| Spotify Track ID|
|explicit|Boolean whether the song contains explicit content|
|release_year|The year the album containing the track was released|
|lyrics|Song Lyrics|
|Skip|Boolean whether I am likely to skip song based on if artist has sung their own name near the beginning of the track |


<h3> Exploratory Data Analysis</h3><a id='eda'></a>
My target column is unbalanced at 80% 20% split. I also did have some null values remaining, however since I will not be using these columns for modeling, I was not concerned in attempting to fill them. Columns such as Featured and Aliases' null values implied that there were no Featured Artists and the main artist does not go by any aliases.

Prior to count vectorizing my lyrics, I looked at explicit breakdown of the tracks, how the songs that are skipped compare to the data as a whole. Despite there being more non-explicit songs, I skip heavier on the explicits. 

The songs in my dataset range from 1963 to 2020 and the first incidence of an artist naming themselves within the lyrics was in 1984.

I count vectorized the words in the lyrics to see what the most common words are across all the lyrics in the data, for data exploration purposes I added a few variations of vulgar words into my stop words. These words will be left in my model to predict, however they will be masked as 'vulgar'. 

Finally I looked at word sentiment breakdown for each category for their top 200 words.

I found it surprising that I would NOT skip <a href ='https://www.youtube.com/watch?v=oHg5SJYRHA0'> This Song </a>, but I WOULD skip <a href ='https://www.youtube.com/watch?v=oHg5SJYRHA0'> This One. </a> Which only shows that I need to pay better attention to the lyrics.
 

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
- [x] Some Fun Libraries

<h3> Modeling<span style="font-size:200%;color:red;">&star;</span> </h3><a id='model'></a> 
Where I am now. 
I decided to reuse the pipeline function I made for my Reddit NLP to do some modeling with Naive Bayes, Logistic Regression and AdaBoost. Each of these models were instantiated with Count Vectorizer and TFIDF Vectorizer as their transformers. 

The pipeline function puts the models through a GridSearch to find the best parameters, and outputs those parameters, as well as scores.

As part of my pre-processing, as mentioned in my EDA there were some words that I wanted to keep in my model but I masked them instead of leaving them as is. In addition to this modeling notebook, I reran these models in a separate notebook this time, lemmatizing the lyrics to see if the scores would improve.

Of these models the AdaBoost with CV and TFIDF performed the best in both notebooks. AdaBoost with TFIDF had the best scores overall:

||Score|
|--|--|
|Train Score |88.70%|
|Test Score | 88.51%
|F1- Train Score |0.731|
|F1- Test Score |0.728|
|Precision |84.19%|
|Specificity |96.19%|

All models that ran through the Lemmatizer notebook scored slightly less than their non-lemmatized self, not surprising considering that the word lemmatizer didn't have much to work with in considering the music.

<b>What's next in my modeling?</b>

- Things are going well, let's break something with Neural Networks



<h3> Road Blocks </h3>

In the [scraped - Possible Feature Project](./scraped%20-%20Possible%20Feature%20Project) folder there are 8 Notebooks: 
   - 1.1-1.5 are data acquisition between Spotify and Genius) 
   - 2.1 & 2.2 Is Data Cleanup
   - RESTART is trying to pull lyrics straight from Genius without the LyricGenius library

<b>Where it went wrong:</b>

- I spent a lot of time pulling the data from Spotify with the idea of matching the user behavior, I became attached to the work I put in pulling data, that I was unwilling to completely give it up.

- I tried to use the dataset I had already built to add lyrics column. This became a mess because the Genius API was trying to match the artist and title exactly. I attempted to fix the issue, but the options were limited (re-doing the pull made no difference, and manually cleaning it took 3+ hours for 1700 rows, of which SOMEHOW there were still rows that needed cleaning after), John and I decided that the best would be to put a list of artists together and pull the lyrics independently of the data I had already built. 
- Following John's suggestion and article share I started another notebook to gather lyrics for pre-selected artists, however I couldn't get the functions to work properly. (the Api would pull russian characters, or some dirty dirty lyrics, for band 'CAKE', looking at Genius there were 8+ tracks listed for CAKE, but the API would only pull 3 and only 1 of them belonging to Cake, if I set the song request to 10, it would fill the list as a repeat), this did not change between keeping the code as is (writing to .txt) or my small addition (gathering info to list to write to DF)

In conclusion the data gathering although it seemed easy, was the most time consuming. Now that I have the data in hand I am ready to move forward. Depending on how my models behave with unbalanced data I may have to pull more artists and lyrics, I am coming down to slim pickings. 

<h3> Dependencies </h3><a id='depend'></a>  

- Python 3
- Numpy v.1.18.5
- Pandas v.1.0.5
- Matplotlib v.3.2.2
- Seaborn v.0.10.1
- Plotly v.4.11.0
- time
- lyricsgenius v.2.0.2
- spotipy v.2.16.0
- TextBlob v.0.15.3
- Sklearn v.0.23.1
- Word

<h3> What's Next </h3><a id='next'></a>  
The initial plan was to get in-depth insights of Spotify user behaviors and predict what makes the users skip songs. However due to scope limits on information availability at this time it was not possible. In attempting to do this:

- I gathered datasets from CrowdAI from a Skip Prediction Challenge that they hosted in 2018. the Data was provided to CrowdAI by Spotify and it contained user behavior and audio features, however all identifiable information to the actual song and artist were removed.
- In an attempt to try and use this dataset, I pulled all Playlists created by Spotify (not users), pulled each track from the playlist and gathered all Audi Features for each track. I then compared a column from my gathered dataset to the Spotify supplied dataset to check for any matches.
- Due to minimal matches (6k in a dataset of 103k columns, based on 1 column, the number of matches would decrease as additional column values were matched.), I decided to pivot the skip prediction to a more personal one. Instead of predicting if users would skip, the model will predict if I will skip the song. 

<br>Considering the reason I started this project was, the pivot of the Capstone direction was not a big one and still falls within the project idea.</br>

I plan to work on this data some more as a personal project and feed it through my model to see how well the model for my capstone will do with unseen data. 

<h3> Fun Libraries </h3><a id='fun'></a>  
In addition to the usual libraries that make our Data Science world spin, I found these libraries to be very useful in this Capstone:

-   <a href='https://pypi.org/project/email-notify-magic/'> Email Notify Magic </a>
    - Used for long running cells, will send you an email when cell has completed running.
- <a href='https://pypi.org/project/lyricsgenius/'> LyricsGenius </a>
    - Makes Genius API pulls easy
- <a href='https://spotipy.readthedocs.io/en/2.16.0/'> Spotipy </a>
    - Lightweight Python library for Spotify Web API    
