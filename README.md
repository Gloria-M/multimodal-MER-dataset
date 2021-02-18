# Building a dataset for multi-modal Music Emotion Recognition

This repository presents a new dataset for the Music Emotion Recognition (MER) task, consisting in audio, lyrics and listeners' comments modalities, created by employing different techniques such as web-scraping, manual cleaning of social tags and manual identification of patterns with the purpose of automatization of a task.

### TO MODIFY
consiting in : deezer_id, song_meanings_id, valence, arousal, list of (emotion_word, count)

## Base Dataset

The largest dataset available that suits a regression approach of MER task is, at the moment of writing, the Deezer [Mood Detection Dataset](https://arxiv.org/abs/1809.07276). For each track, this set contains the corresponding *Deezer ID*, the *MSD ID*, the *artist* and *title* and values for *valence* and *arousal*. This data collected by researchers at Deezer is itself derived from the [Million Song Dataset](https://www.researchgate.net/publication/220723656_The_Million_Song_Dataset), a common support for MIR tasks in general.

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/circumplex_model.png" width=100%/>




<table style="width:100%">
  <col align="left">
  <col align="left">
  <col align="left">
  <tr>
    <th> </th>
    <th> </th>
    <td><b>No. of unique tags</b></td>
  </tr>
<tbody>
  <tr>
    <td>aggressiveness</td>
    <td>aggressive, belligerent, hostile, violent, wild ...</td>
    <td>44</td>
  </tr>
  <tr>
    <td>amusement</td>
    <td>amusing, comical, funny, giggle, hilarious, laugh ...</td>
    <td>118</td>
  </tr>
  <tr>
    <td>anger</td>
    <td>angry, angst, furious, fury, mad, outraged, rage ...</td>
    <td>76</td>
  </tr>
  <tr>
    <td>annoyance</td>
    <td>annoyed, irritated, frustrated, indignant, tired of ...</td>
    <td>23</td>
  </tr>
  <tr>
    <td>anxiety</td>
    <td>anxious, concerned, distressed, jumpy, nervous ...</td>
    <td>37</td>
  </tr>
  <tr>
    <td>bittersweet</td>
    <td>bittersweet, sad yet upbeat, sad but happy ...</td>
    <td>44</td>
  </tr>
  <tr>
    <td>boredom</td>
    <td>bored, tired ...</td>
    <td>7</td>
  </tr>
  <tr>
    <td>calmness</td>
    <td>calm, carefree, chill out, mellow, relaxed, serene ...</td>
    <td>333</td>
  </tr>
  <tr>
    <td>cheerfulness</td>
    <td>cheerful, gleeful, jolly, merry, upbeat ...</td>
    <td>42</td>
  </tr>
  <tr>
    <td>comfort</td>
    <td>comfortable, comforting, cozy, healing, soothing ...</td>
    <td>103</td>
  </tr>
  <tr>
    <td>confidence</td>
    <td>assured, confident, secure, self secure, sure, strong ...</td>
    <td>20</td>
  </tr>
  <tr>
    <td>contemplation</td>
    <td>brooding, contemplative, introspective, reflective ...</td>
    <td>58</td>
  </tr>
  <tr>
    <td>depression</td>
    <td>blue, depressed, depressing, down, low, miserable ...</td>
    <td>117</td>
  </tr>
  <tr>
    <td>desperation</td>
    <td>desperate,self harm, hopeless, trapped, weight ...</td>
    <td>63</td>
  </tr>
  <tr>
    <td>dreamy</td>
    <td>dream, dreamy, lost in the clouds, head in clouds ...</td>
    <td>102</td>
  </tr>
  <tr>
    <td>erotic</td>
    <td>desire, erotic, seductive, sensual, sexual, want ...</td>
    <td>54</td>
  </tr>
  <tr>
    <td>excitement</td>
    <td>aroused, elated, energetic, enthusiastic, excited ...</td>
    <td>79</td>
  </tr>
  <tr>
    <td>fear</td>
    <td>afraid, fearful, frightened, horror, panic, scared ...</td>
    <td>37</td>
  </tr>
  <tr>
    <td>grief</td>
    <td>heartbreak, hurt, mournful, pain, sorrow, suffering ...</td>
    <td>73</td>
  </tr>
  <tr>
    <td>happiness</td>
    <td>content, delighted, glad, happy, joyous, pleased ...</td>
    <td>240</td>
  </tr>
  <tr>
    <td>insecurity</td>
    <td>doubtful, insecure, uncertain, not confident, not sure ...</td>
    <td>5</td>
  </tr>
  <tr>
    <td>loneliness</td>
    <td>abandoned, alone, lonely, solitary ...</td>
    <td>51</td>
  </tr>
  <tr>
    <td>nostalgia</td>
    <td>homesick, longing, miss, nostalgic, yearning ...</td>
    <td>126</td>
  </tr>
  <tr>
    <td>optimism</td>
    <td>encouraging, hopeful, inspirational, motivational ...</td>
    <td>104</td>
  </tr>
  <tr>
    <td>pessimism</td>
    <td>cynical, misanthropic, negative, pessimistic ...</td>
    <td>17</td>
  </tr>
  <tr>
    <td>romanticism</td>
    <td>amor, romantic, sweet, you ...</td>
    <td>109</td>
  </tr>
  <tr>
    <td>sadness</td>
    <td>cry, droopy, gloomy, melancholic, sad, unhappy ...</td>
    <td>400</td>
  </tr>
</tbody>
</table>



|                	|                                                            	| No. of unique tags 	|
|----------------	|:----------------------------------------------------------:	|:------------------:	|
| aggressiveness 	|     aggressive, belligerent, hostile, violent, wild ...    	|         44         	|
| amusement      	|    amusing, comical, funny, giggle, hilarious, laugh ...   	|         118        	|
| anger          	|    angry, angst, furious, fury, mad, outraged, rage ...    	|         76         	|
| annoyance      	|   annoyed, irritated, frustrated, indignant, tired of ...  	|         23         	|
| anxiety        	|     anxious, concerned, distressed, jumpy, nervous ...     	|         37         	|
| bittersweet    	|       bittersweet, sad yet upbeat, sad but happy ...       	|         44         	|
| boredom        	|                      bored, tired ...                      	| 7                  	|
| calmness       	|   calm, carefree, chill out, mellow, relaxed, serene ...   	|         333        	|
| cheerfulness   	|         cheerful, gleeful, jolly, merry, upbeat ...        	|         42         	|
| comfort        	|    comfortable, comforting, cozy, healing, soothing ...    	|         103        	|
| confidence     	|  assured, confident, secure, self secure, sure, strong ... 	|         20         	|
| contemplation  	|   brooding, contemplative, introspective, reflective ...   	|         58         	|
| depression     	|    blue, depressed, depressing, down, low, miserable ...   	|         117        	|
| desperation    	|     desperate,self harm, hopeless, trapped, weight ...     	|         63         	|
| dreamy         	|    dream, dreamy, lost in the clouds, head in clouds ...   	|         102        	|
| erotic         	|    desire, erotic, seductive, sensual, sexual, want ...    	|         54         	|
| excitement     	|    aroused, elated, energetic, enthusiastic, excited ...   	|         79         	|
| fear           	|   afraid, fearful, frightened, horror, panic, scared ...   	|         37         	|
| grief          	|   heartbreak, hurt, mournful, pain, sorrow, suffering ...  	|         73         	|
| happiness      	|    content, delighted, glad, happy, joyous, pleased ...    	|         240        	|
| insecurity     	| doubtful, insecure, uncertain, not confident, not sure ... 	|          5         	|
| loneliness     	|           abandoned, alone, lonely, solitary ...           	|         51         	|
| nostalgia      	|      homesick, longing, miss, nostalgic, yearning ...      	|         126        	|
| optimism       	|    encouraging, hopeful, inspirational, motivational ...   	|         104        	|
| pessimism      	|      cynical, misanthropic, negative, pessimistic ...      	|         17         	|
| romanticism    	|               amor, romantic, sweet, you ...               	|         109        	|
| sadness        	|     cry, droopy, gloomy, melancholic, sad, unhappy ...     	|         400        	|
