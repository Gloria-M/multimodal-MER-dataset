# Building a dataset for multi-modal Music Emotion Recognition

This repository presents a new dataset for the Music Emotion Recognition (MER) task, consisting in audio, lyrics and listeners' comments modalities, created by employing different techniques such as web-scraping, manual cleaning of social tags and manual identification of patterns with the purpose of automatization of a task.

### TO MODIFY
consiting in : deezer_id, song_meanings_id, valence, arousal, list of (emotion_word, count)

## Base Dataset

The largest dataset available that suits a regression approach of MER task is, at the moment of writing, the Deezer [Mood Detection Dataset](https://arxiv.org/abs/1809.07276). For each track, this set contains the corresponding *Deezer ID*, the *MSD ID*, the *artist* and *title* and values for *valence* and *arousal*. This data collected by researchers at Deezer is itself derived from the [Million Song Dataset](https://www.researchgate.net/publication/220723656_The_Million_Song_Dataset), a common support for MIR tasks in general.


## Lyrics and comments

For building the new dataset, the first step is selecting the songs for which lyrics and comments from users are found when scraping the web.

 The [SongMeanings](https://songmeanings.com/) site provides both the lyrics of the songs and comments on the meaning of the lyrics, as they are interpreted by the users.

On the page of each track(listed on the website) the corresponding lyrics are identified by the `<div class_='holder lyric-box' >` tag and the comments section is announced by the `<div class_='text' >` tag.

Acquiring the comments from this website comes with an important advantage that diminish the need for additional filtering: the comments are sorted based on the number of votes in descending order with the most voted comment -the most reliable one- listed first. The comments are displayed on multiple pages, but the first one contains just enough comments of good quality, therefore only the data in the first page is collected.

Starting with the 18,644 tracks selected by the researchers at Deezer, after performing this procedure and removing the tracks that do not appear on the website or do not have comments associated, the dataset size is reduced to 10,923 samples.


## Annotation

The annotation process of the new dataset is performed by following steps similar to  [Hu et al.,2009](https://www.semanticscholar.org/paper/Lyric-Text-Mining-in-Music-Mood-Classification-Hu-Downie/e658ec86e033aae370ba680118a04431071cafe1), making use of the social tags associated with songs by listeners.

Mapping the tracks in the Deezer dataset to the *last.fm* database by their MSD ID, the social tags recorded in year 2011 can be retrieved. Along each tag associated with each song, a normalized value representing the number of listeners choosing the tag is provided.

In order to create the new dataset with information as up-to-date as possible, instead of querying the 2011 tags database, the tags available at the time of writing are acquired using [Last.fm API](https://www.last.fm/api/). This allows access to a maximum of 100 tags per song, sorted by their popularity and the normalized value indicating the count of listeners attributing the respective tag to a song. Using this method, 10,919 tracks with tags are found.

The considerable volume of tags collected (795,368 unique tags) is extremely noisy and contains lot of unusable data. Therefore, to get to a format which allows mapping to emotions space, a thorough cleaning process must be performed.

Although the musical genre, instruments names or similarity tags can be useful for MIR tasks, they do not serve the purpose of this study. Therefore, these, along many others, are removed following the removal criteria presented, reducing the volume of social tags to 390,698:


## Support Images

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/circumplex_model.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/emotions_distribution.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/tags_to_emotions.png" width=100%/>

common support for MIR tasks in general
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/emotions_groups.png" width=100%/>
common support for MIR tasks in general
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/lyrics_repetition_patterns.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/lyrics_structural_patterns.png" width=100%/>
