# Building a dataset for multi-modal Music Emotion Recognition

This repository presents a new dataset for the Music Emotion Recognition (MER) task, consisting in audio, lyrics and listeners' comments modalities, created by employing different techniques such as web-scraping, manual cleaning of social tags and manual identification of patterns with the purpose of automatization of a task.

### TO MODIFY
consiting in : deezer_id, song_meanings_id, valence, arousal, list of (emotion_word, count)

## Base Dataset

The largest dataset available that suits a regression approach of MER task is, at the moment of writing, the Deezer [Mood Detection Dataset](https://arxiv.org/abs/1809.07276). For each track, this set contains the corresponding *Deezer ID*, the *MSD ID*, the *artist* and *title* and values for *valence* and *arousal*. This data collected by researchers at Deezer is itself derived from the [Million Song Dataset](https://www.researchgate.net/publication/220723656_The_Million_Song_Dataset), a common support for MIR tasks in general.

<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/circumplex_model.png" width=100%/>
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/emotions_distribution.png" width=100%/>
<img src="https://github.com/Gloria-M/multimodal-MER-dataset/blob/main/Images/tags_to_emotions.png" width=100%/>





|                	|                                                            	| No. of unique tags 	|
|:---------------	|:-----------------------------------------------------------	|:------------------:	|
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









| Pattern                         	| Description                                                                                                                                                                                                                                                         	| Action                                                                                                                                  	|
|:--------------------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|-----------------------------------------------------------------------------------------------------------------------------------------	|
| \n\n **[chorus]** \n              	| The first occurrence of this instruction in the lyrics text is usually followed by the text of the chorus, determined by the *newline* character succeeding the **[chorus]** tag and two *newline* characters announcing the end of the chorus text.                	| Memorize the text of the chorus for future replacement in lyrics text.                                                                  	|
| \n\n **[chorus: repeat xN]** \n   	| This instruction  is usually followed by the text of the chorus, determined by the *newline* character succeeding the **[chorus]** tag and two *newline* characters announcing the end of the chorus text. It also means that the chorus is repeated ***N*** times. 	| Memorize the text of the chorus for future replacement in lyrics text and replace the tag with the chorus text, copied ***N-1*** times. 	|
| \n\n **[chorus: repeat xN]** \n\n 	| This instruction announces the presence of the chorus text in the sang lyrics, that is repeated ***N*** times.                                                                                                                                                      	| Replace the tag with the previously memorized chorus text, copied ***N*** times.                                                        	|
| \n\n **[chorus]** \n\n            	| This instruction announces the presence of the chorus text in the sang lyrics.                                                                                                                                                                                      	| Replace the tag with the previously memorized chorus text.                                                                              	|
| \n **[repeat xN]** \n\n           	| This instruction is usually placed at the end of the part of lyrics text to be repeated. This beginning of the sequence to be repeated is marked by two **newline** characters.                                                                                     	| Identify the text to be repeated and replace the repetition tag.                                                                        	|
