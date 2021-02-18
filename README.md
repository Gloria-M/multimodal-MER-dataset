# Building a dataset for multi-modal Music Emotion Recognition

This repository presents a new dataset for the Music Emotion Recognition (MER) task, consisting in audio, lyrics and listeners' comments modalities, created by employing different techniques such as web-scraping, manual cleaning of social tags and manual identification of patterns with the purpose of automatization of a task.

### TO MODIFY
consiting in : deezer_id, song_meanings_id, valence, arousal, list of (emotion_word, count)

## Base Dataset

The largest dataset available that suits a regression approach of MER task is, at the moment of writing, the Deezer [Mood Detection Dataset](https://arxiv.org/abs/1809.07276). For each track, this set contains the corresponding *Deezer ID*, the *MSD ID*, the *artist* and *title* and values for *valence* and *arousal*. This data collected by researchers at Deezer is itself derived from the [Million Song Dataset](https://www.researchgate.net/publication/220723656_The_Million_Song_Dataset), a common support for MIR tasks in general.

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/circumplex_model.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/emotions_distribution.png" width=100%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/tags_to_emotions.png" width=100%/>

common support for MIR tasks in general
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/emotions_groups.png" width=100%/>
common support for MIR tasks in general
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/lyrics_repetition_patterns.png" width=90%/>

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/lyrics_structural_patterns.png" width=90%/>
