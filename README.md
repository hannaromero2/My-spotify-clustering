# Clustering my songs on Spotify and my mood prediction


Spotify, the world's largest on-demand music service, has a history of pushing technological boundaries and using big data, artificial intelligence and machine learning to drive success. Although its offering is music, Spotify is a data-driven company and uses data in every part of the organization to make decisions. It is proud to offer over 50 million ad-free tracks to its 130 million Spotify Premium subscribers for £9.99 a month, with each stream learning more about its users. The company now has a market capitalization of $35 billion and from 2014 to the end of 2019, Spotify spent hundreds of millions of dollars acquiring data science consulting firms, music intelligence agencies, personalization feature technology and recommendation, and an artificial intelligence to strengthen its data-centric offer. As the service continues to acquire data points, it uses that information to train algorithms and machines to listen to music and extrapolate information that impacts its business and listener experience. 

The project uses PCA to reduce the dimensions of the list of audio functions before running a K-Means model to classify and visualize my musical tastes and the mood that prevails in my playlist.


## General description

The objective of this project is to be able to discover the mood of my playlist and the type of songs that predominate in my Spotify. The program takes a user's playlist and generates a music taste rating based on it. Which will allow us to know the type of songs that the user likes and the mood. This allows musical tastes to be separated by showing the songs that most align with the listening habits of a particular user.

The data used for this project was collected from a variety of sources: 1) A spotify playlist ( One created by me was used for this program "https://open.spotify.com/playlist/3vgIbym3mQH4pzZQlWHnsq?si=993Wt2ugQEmfl-07JCz36Q "), 2) "https://www.chosic.com/spotify-playlist-analyzer/" This is a page where my spotify playlist dataset was generated.

The methodologies used included data cleaning, outlier imputation, exploratory data analysis (EDA), and data pooling using the KMean method to create the data classification.

# About:

I'm going to group my saved songs into a Spotify playlist. The clusters will be derived due to the KMeans clustering model, which was trained on the Spotify Dataset, which contains approximately 282 songs. Also, all derivative groups will represent a certain mood that I have while listening to my music.

## DATA

In order to generate the .csv file, we will go to the page: https://www.chosic.com/spotify-playlist-analyzer/, and enter the link of the playlist that we want to extract from spotify.
At the end of the site, you can download the playlist in a ".csv" file, which will serve as a dataset.


| KEY              | VALUE TYPE | VALUE DESCRIPTION                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| duration_ms      | int        | The duration of the track in milliseconds.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| key              | int        | The estimated overall key of the track. Integers map to pitches using standard Pitch Class notation . E.g. 0 = C, 1 = C♯/D♭, 2 = D, and so on. If no key was detected, the value is -1.                                                                                                                                                                                                                                                                                                                                                                                         |
| mode             | int        | Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. Major is represented by 1 and minor is 0.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| time_signature   | int        | An estimated overall time signature of a track. The time signature (meter) is a notational convention to specify how many beats are in each bar (or measure).                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Acoustic     | float      | A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic. The distribution of values for this feature look like this:#                                                                                                                                                                                                                                                                                                                                                                                       |
| Dance     | float      | Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable. The distribution of values for this feature look like this:#                                                                                                                                                                                                                                                                       |
| Enery           | float      | Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale. Perceptual features contributing to this attribute include dynamic range, perceived loudness, timbre, onset rate, and general entropy. The distribution of values for this feature look like this:#                                                                                                                          |
| Instrumental | float      | Predicts whether a track contains no vocals. “Ooh” and “aah” sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly “vocal”. The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0. The distribution of values for this feature look like this:#                                                                                                                 |
| Live         | float      | Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live. The distribution of values for this feature look like this:#                                                                                                                                                                                                                                                                                            |
| Loud         | float      | The overall loudness of a track in decibels (dB). Loudness values are averaged across the entire track and are useful for comparing relative loudness of tracks. Loudness is the quality of a sound that is the primary psychological correlate of physical strength (amplitude). Values typical range between -60 and 0 db. The distribution of values for this feature look like this:#                                                                                                                                                                                       |
| Speech      | float      | Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks. The distribution of values for this feature look like this:# |
| valence          | float      | A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry). The distribution of values for this feature look like this:#                                                                                                                                                                                                                                                                  |
| Tempo            | float      | The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration. The distribution of values for this feature look like this:#                                                                                                                                                                                                                                                                                                                         |
| id               | string     | The Spotify ID for the track.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| uri              | string     | The Spotify URI for the track.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| track_href       | string     | A link to the Web API endpoint providing full details of the track.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| analysis_url     | string     | An HTTP URL to access the full audio analysis of this track. An access token is required to access this data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| type             | string     | The object type: “audio_features”                                                                                                                               

## Clusters

- Cluster 0 is tourned out to be very high in terms of speechiness since the mean value over all songs is 0.87. If the speechiness of a song is above 0.66, it is probably made of spoken words, a score between 0.33 and 0.66 is a song that may contain both music and words, and a score below 0.33 means the song does not have any speech. Moreover, it is low in instrumentalness but pretty high in danceability. I assume there are mostly with low instrumental and danceable songs.
- Cluster 1 is relatively high in danceability and energy but low in instrumentalness. I expect to see a lot of energetic songs there.
- Cluster 2 is very high in acousticness but low in instrumentalness and loudness. Moreover, it has quite high danceability magnitude. Therefore, I expect to see more calm, perhaps sad, songs. 
- Cluster 3 is the highest in acousticness and instrumentalness but the lowest in speechiness.
- Cluster 4 is quite high in instrumentalness and energy and average in danceability.


## Conclusion

To conclude, my musical tastes are a bit varied, but the ones that stood out the most were the most moved or energetic.

In the same way, I can notice my different moods and which ones predominate more, as shown below:

<pre>
my saved songs taste/mood:

slow instrumental but danceable: 0.20921985815602837
energetic/dancing: 0.21631205673758866
calm/romantic: 0.1524822695035461
studying/thinking 0.25177304964539005
chill: 0.1702127659574468
</pre>


## Recommendations

I think that one way this project could have been done to make it more accurate is by entering the Spotify API directly, in order to have access to a larger playlist and with more reliable and accurate results.

I think this work is quite interesting and a good practice for people who like to use artificial intelligence and already have basic knowledge of how Kmeans is used, since it includes several fields of Matchine Learning simultaneously. I trained the KMeans clustering algorithm on a dataset of my own Spotify playlist. In addition, I used a classifier that helped me classify the songs I liked into playlists, each of which represented a different style/mood.


## References

> "https://www.chosic.com/spotify-playlist-analyzer/"
> "https://open.spotify.com/playlist/3vgIbym3mQH4pzZQlWHnsq?si=993Wt2ugQEmfl-07JCz36Q"

