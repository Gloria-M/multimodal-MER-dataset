# New dataset for multimodal Music Emotion Recognition

This new dataset for multimodal Music Emotion Recognition (MER) contains 9,972 entries, consisting in audio, lyrics and listeners' comments, annotated with scores for **valence** and **arousal**, and also lists of **emotion-related word & count** tuples.

Due to copyright restrictions, the raw audio, lyrics and comments are not released, but the audio can be retrieved using *Deezer API*, and the lyrics and comments are available in list of tokens format, making the dataset easy to experiment with.

### For a complete description of the preprocessing methods, please refer to [new_dataset](https://gloria-m.github.io/new_dataset.html).  

<br/>  

## Files Structure

### data_info.json
&nbsp; &nbsp; &nbsp; **deezer_id**  
&nbsp; &nbsp; &nbsp; | --  **msd_id** *(song id in the MillionSongDataset)*<br>
&nbsp; &nbsp; &nbsp; | --  **song_meanings_id** *(song id on the Song Meanings site)*<br>
&nbsp; &nbsp; &nbsp; | --  **artist_name**<br>
&nbsp; &nbsp; &nbsp; | --  **song_title**

### annotations.json
&nbsp; &nbsp; &nbsp; **deezer_id**  
&nbsp; &nbsp; &nbsp; | --  **valence** <br>
&nbsp; &nbsp; &nbsp; | --  **arousal** <br>
&nbsp; &nbsp; &nbsp; | --  **emotion**  <br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; | --  [**emotion_word**, **count**]

### lyrics.json
&nbsp; &nbsp; &nbsp; **deezer_id**  
&nbsp; &nbsp; &nbsp; | --  list of lyrics tokens <br>

### comments.json
&nbsp; &nbsp; &nbsp; **deezer_id**  
&nbsp; &nbsp; &nbsp; | --  list of comments tokens <br>

## Brief Description

### Annotation

The Circumplex Model of Affect, defined in [[Russell, 1980]](https://www.researchgate.net/publication/235361517_A_Circumplex_Model_of_Affect), that maps emotions to a 2D space defined by **valence** and **arousal** dimensions. Valence, displayed as the horizontal axis, represents the energy of emotion, ranging from positive to negative, while arousal, the vertical axis, represents the amount of intensity in emotion, ranging from low to high. This scheme allows for a division of the emotion space in four quadrants.

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/images/circumplex_model.png" width=100%/>

The annotation process of the new dataset is performed by making use of the social tags associated with songs by listeners, acquired using [Last.fm API](https://www.last.fm/api/).

A list of affect-related words is composed using the affective lexicon WordNet Affect [[Valitutti, 2004]](http://corpustext.com/reference/affect_wordnet.html) and the Merriam-Webster online [dictionary](https://www.merriam-webster.com/dictionary/dictionary) and [thesaurus](https://www.merriam-webster.com/thesaurus). These words are grouped according to their meaning in 27 emotional categories, named with a corresponding emotion, using similarity paths defined in WordNet [[Bentivogli et al., 2004]](https://www.researchgate.net/publication/228902778_Revising_the_WORDNET_DOMAINS_Hierarchy_semantics_coverage_and_balancing).

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/images/emotions_groups.png" width=100%/>

The tags containing these stems are manually filtered, as not all tags containing stems of affective words describe an emotion perceived when listening to a particular song.

Afterwards, the remaining tags associated to each song are replaced by the emotion words describing the clusters the tags are part of, taking into account the number of apprearances of each tag.

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/images/tags_to_emotions.png" width=100%/>


Using the [NRC VAD Lexicon](https://www.researchgate.net/publication/334118031_Obtaining_Reliable_Human_Ratings_of_Valence_Arousal_and_Dominance_for_20000_English_Words), the 27 words representing emotions are embedded into valence-arousal space, taking into account their summed count at song-level.
For every song, the valence and arousal scores extracted from the VAD Lexicon for each word are multiplied by the normalized count and the final ratings for the song are obtained by computing the average of the sum of the weighted values for valence and arousal dimensions:

<img src="https://render.githubusercontent.com/render/math?math=Valence(S) = \displaystyle{\frac{\sum_{w} valence_{w}\cdot count_{S,w}}{\sum_{w} count_{S,w}}}">  \
<br/>
<img src="https://render.githubusercontent.com/render/math?math=Arousal(S) = \displaystyle{\frac{\sum_{w} arousal_{w}\cdot count_{S,w}}{\sum_{w} count_{S,w}}}">  ,  where *S* is a song in the dataset and *w* an emotion word in *S*.


This annotation strategy resulted in an unbalanced distribution of the data in the 2D space of emotions, with quadrant 2 appearing heavily underrepresented. This reveals that strong negative emotions such as *'anger', 'aggressivity'* are not frequently perceived in music.

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/images/data_distribution.png" width=100%/>


### Deezer Tracks Selection

Starting from the audio selection in Deezer Mood Detection Dataset [[Delbouys et al., 2018]](https://arxiv.org/abs/1809.07276) and keeping only the samples for which annotations are computed, the outdated Deezer IDs are updated if possible or removed. Another filtering process is performed considering the duration of songs.


### Lyrics and comments

The lyrics and comments are retrieved by scraping the [SongMeanings](https://songmeanings.com/) website .

The raw lyrics data contain a great amount of noise, as they are written by different users and with no set of rules or format to be followed. Therefore, cleaning the lyrics data is a meticulous process that involves manual curating and a considerable amount of time. The lyrics have a particular structure, different than usual text data, which was studied for patterns identification with the scope of finding a set of rule that allow for automatization.

In the raw lyrics text, there are different types of tags, such as repetitive instructions (*'repeat', 'x2', 'repeat once'*, etc.), announcement of artists singing a particular part of the song (*'[eminem]', '[all:]', '2pac'*, etc.), structural information (*'chorus', 'verse', 'bridge', 'pre-chorus'*, etc.).
As a result of a series of manual transformations and removals, different types of patterns are revealed and used for automatization of the cleaning process.
In differentiating between the types of patterns discovered, the *newline* (\n) character has the greatest role.
The most important patterns are ones playing a role in changing the text of lyrics, as described below:

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/images/lyrics_repetition_patterns.png" width=100%/>

These transformations bring the lyrics text to a format that allows applying common preprocessing techniques used in NLP tasks.
Starting with the texts in *string* format, the following transformations are applied:
<ul>
  <li>
  replace words in short form with their extended forms <br>
    - 'm &#8594 am <br>
    - 're &#8594 are <br>
    - 've &#8594 have <br>
    - 'd &#8594 would <br>
    - 'll &#8594 will <br>
    - she's &#8594 she is <br>
    - he's &#8594 he is <br>
    - it's &#8594 it is <br>
    - ain't &#8594 is not <br>
    - n't &#8594 n not <br>
    - n' &#8594 ng <br>
    - 's &#8594 ''
  </li>
  <li>
  remove punctuation symbols (*' . ' , ' , ' , ' ; ' , '!', '', '\*'*, etc.)
  </li>
  <li>
  remove spacing instructions (*'\n', '\t'*)
  </li>
</ul>


The steps presented above conclude with tokenization, converting the texts into lists of words. The preprocessing phase ends after curating the words resulted, as follows:
<ul>
  <li>
  correct identified misspellings (*'urself', 'thered'*, etc.)
  </li>
  <li>
  replace censored words with their uncensored version
  </li>
  <li>
  remove stopwords
  </li>
  <li>
  discard non-english words, using <a href="http://pyenchant.github.io/pyenchant/">pyenchant</a>
  </li>
  <li>
  keep the non-english words that appear in the slangs lexicon <a href="https://arxiv.org/abs/1608.05129">[Wu et al., 2016]</a>
  </li>
</ul>
