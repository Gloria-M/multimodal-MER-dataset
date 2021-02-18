# Building a dataset for multi-modal Music Emotion Recognition

This repository presents a new dataset for the Music Emotion Recognition (MER) task, consisting in audio, lyrics and listeners' comments modalities, created by employing different techniques such as web-scraping, manual cleaning of social tags and manual identification of patterns with the purpose of automatization of a task.

### TO MODIFY
consiting in : deezer_id, song_meanings_id, valence, arousal, list of (emotion_word, count)

## Base Dataset

The largest dataset available that suits a regression approach of MER task is, at the moment of writing, the Deezer [Mood Detection Dataset](https://arxiv.org/abs/1809.07276). For each track, this set contains the corresponding *Deezer ID*, the *MSD ID*, the *artist* and *title* and values for *valence* and *arousal*. This data collected by researchers at Deezer is itself derived from the [Million Song Dataset](https://www.researchgate.net/publication/220723656_The_Million_Song_Dataset), a common support for MIR tasks in general.


## Lyrics and comments

For building the new dataset, the first step is selecting the songs for which lyrics and comments from users are found when scraping the web.
<p> The [SongMeanings](https://songmeanings.com/) site provides both the lyrics of the songs and comments on the meaning of the lyrics, as they are interpreted by the users.
</p>
<p> On the page of each track(listed on the website) the corresponding lyrics are identified by the tag *<div class_='holder lyric-box' >* and the comments section is announced by the *<div class_='text' >* tag.
</p>
\p Acquiring the comments from this website comes with an important advantage that diminish the need for additional filtering: the comments are sorted based on the number of votes in descending order with the most voted comment -the most reliable one- listed first. The comments are displayed on multiple pages, but the first one contains just enough comments of good quality, therefore only the data in the first page is collected.
\p Starting with the $18\,644$ tracks selected by the researchers at Deezer, after performing this procedure and removing the tracks that do not appear on the website or do not have comments associated, the dataset size is reduced to 10,923 samples.

## Support Images

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/circumplex_model.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/emotions_distribution.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/tags_to_emotions.png" width=100%/>

common support for MIR tasks in general
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/emotions_groups.png" width=100%/>
common support for MIR tasks in general
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/lyrics_repetition_patterns.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/lyrics_structural_patterns.png" width=100%/>
