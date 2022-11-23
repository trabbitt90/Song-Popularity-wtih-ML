![image.png]([SL-123119-26540-43.jpg](https://www.google.com/imgres?imgurl=https%3A%2F%2Fimg.freepik.com%2Ffree-vector%2Fmusical-pentagram-sound-waves-notes-background_1017-33911.jpg%3Fw%3D2000&imgrefurl=https%3A%2F%2Fwww.freepik.com%2Ffree-photos-vectors%2Fmusic-show&tbnid=QEYRfYMsxIgXnM&vet=12ahUKEwjq0fvfzcT7AhWFl1MKHebcDswQMygBegUIARDVAg..i&docid=sy3DEZTZUYO0ZM&w=2000&h=1142&q=music%20images&ved=2ahUKEwjq0fvfzcT7AhWFl1MKHebcDswQMygBegUIARDVAg))

# Predicting Song Popularity with ML

By: Tim Rabbitt

## Business Understanding
Rabbitt Record Company has signed many new talented music artists with the hope that their acquired talent can create some of the more popular tracks in circulation. Considering todays creative and competitive music industry, the record company would like to get a leg up on the competition by providing its artists with the helpful information they need to produce the next big hit. 

**Stakeholder:** Rabbitt Record Company

**Buisness Problem:** Rabbitt Record Company would like to help their artists write more popular songs.

**Buisness Question:** Can we accurately predict a newly written songs' popularity given certain audio statistics? Which of these statistics are most important in determining popularity?

By analyzing the top songs of the 2000's and the features that contributed to their success, we hope to be able to accurately predict a newly written songs' popularity, specifically whether or not that song will be in the top 20 percent. Additionally, we hope to learn what features contribute the most to it's popularity.

## Data

The data used for this analysis was provided by Kaggle. This dataset contains audio statistics of the top 2000 tracks on Spotify from 2000-2019. The data contains about 18 columns each describing the track and it's qualities.


* `artist`: Name of the Artist.
* `song`: Name of the Track.
* `duration_ms`: Duration of the track in milliseconds.
* `explicit`: The lyrics or content of a song or a music video contain one or more of the criteria which could be considered offensive or unsuitable for children.
* `year`: Release Year of the track.
* `popularity`: The higher the value the more popular the song is.
* `danceability`: Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable.
* `energy`: Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity.
* `key`: The key the track is in. Integers map to pitches using standard Pitch Class notation. E.g. 0 = C, 1 = C♯/D♭, 2 = D, and so on. If no key was detected, the value is -1.
* `loudness`: The overall loudness of a track in decibels (dB). Loudness values are averaged across the entire track and are useful for comparing relative loudness of tracks. Loudness is the quality of a sound that is the primary psychological correlate of physical strength (amplitude). Values typically range between -60 and 0 db.
* `mode`: Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. Major is represented by 1 and minor is 0.
* `speechiness`: Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks.
* `acousticness`: A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic.
* `instrumentalness`: Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly "vocal". The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0.
* `liveness`: Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live.
* `valence`: A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry).
* `tempo`: The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration.
* `genre`: Genre of the track.

Further information on this dataset can found at [Kaggle.com](https://www.kaggle.com/datasets/paradisejoy/top-hits-spotify-from-20002019)

## Methods

While a linear regression model would be appropriate for this analysis, we wanted to build a classification model that would predict whether or not a song's popularity would be in the 80th percentile. We have divided the popularity column into 2 classes (A and B), A represts the 80th percentile, while B represents all songs below the 80th percentile. We then built multiple classification models including Decision Tree, K-Nearest Neighbors, Random Forest and Gradient Boosting. Using an iterative approach beginning with a with a baseline model and followed by hyperparamenter tuning using GridSearchCV, we believe we can produce an adequate model to predict song popularity.

## Results

### Baseline Decision Tree Model

**Class A F1-Score:   0.27**

**Test Accuracy:   0.68**

![image.png](attachment:image.png)

### Tuned K-Nearest Neighbor Model

**Class A F1-Score:   0.32**

**Test Accuracy:   0.69**

![image-2.png](attachment:image-2.png)

### Tuned Random Forest Model

**Class A F1-Score:   0.48**

**Test Accuracy:   0.85**

![image-3.png](attachment:image-3.png)

### Tuned XGBoost Model (Final Model)

**Class A F1-Score:   0.68**

**Test Accuracy:   0.89**

![image-4.png](attachment:image-4.png)

### Feature Importance

![image-5.png](attachment:image-5.png)


## Model Observations:
We created 4 different baseline models: Decision Tree, K-Nearest Neighbors, Random Forest, and XGBoost. After assessing the performance of each model we then used GridSearchCV to select hyperparameters to optimize model performance. We found our tuned XGBoost model to be most effective at predicting song popularity. Here are some observations of our final model:

**Class A (80th percentile):** If we predicted every song to be in Class A, we would have an accuracy of 20%.

**Class B (<80th percentile):** If we predicted every song to be in Class B, we would have an accuracy of 80%.

**Recall:** Our final model correctly identified 61% of the songs that were actually in Class A (true positives), alternatively our model labeled 39% of Class A as Class B (false negatives). 

**Precision:** Of all the times our model predicted a song to be in the 80th percentile, 77% were indeed in Class A (true positives), alternatively 23% were actually in Class B (false positives).

**Accuracy:** Out of all the predictions our model made for Class A and Class B, 89% of them were correct.

**F1-Score:** F1-score is the harmonic mean of precision and recall, meaning both metrics need to be high for the F1-score to be high. The closer this value is to 1, the better your model is overall. With a value of .68, there is room for improvement but it is the highest score of all the models we explored.

**Features:** Hiphop, Rock, and R&B genres have the most influence as features in determining song popularity.

## Conclusion

After our analysis, we can conclude that you can indeed predict song popularity using audio statistics. Our final model had an accuracy of 89%, meaning out of all the predictions our model made, 89% of them were correct. Our model is more likely to produce false negatives, a song that it predicts will be < 80th percentile when it's actually in the 80th percentile, and less likely to produce false positives, a song that it predicts will be in the 80th percentile when it is < 80th percentile. This is good from a business standpoint, as the record company can fund the production of future songs with 77% certainty they will turn out to be popular on the open market.

The feature importance plot above assigns a score to input features based on how useful they are at predicting song popularity. According to this plot a genre of hiphop, R&B, and rock are most important when it comes to predicting song popularity. Pay extra attention to these genres when writing and producing future songs. 

## Limitations and Future Analysis

While we used four different classification models for this project there are several more that may prove to have better performance, a couple that comes to mind would be Naive Bayes and Adaboost. Applying these models to the dataset would make for a more complete exploration of predictive power. We used GridSearchCV to improve the performance of each model, this iterative approach saw each model improve upon its baseline version. However, there are several hyperparameters that we did not address that could help improve model performance. Further analysis that addresses more hyperparameters has the potential to produce improved model performance. Additionally, future analysis and modeling might want to consider a couple of items:

1. The data we used in this analysis was from 2000-2019. Using songs and their audio statistic from 2019-2022 would help to make song popularity predictions in a more present music industry.


2. We wanted to make a classification model for this project, future analysis should look into a regression model and its capabilities in predicting song popularity.

## For More Information
Please check out my [Jupyter Notebook](https://github.com/trabbitt90/Song-popularity-with-ML/blob/main/Predicting%20Song%20Popularity%20with%20ML.ipynb) and [Presentation](https://github.com/trabbitt90/Song-popularity-with-ML/blob/main/Presentation.pdf)

## Navigating the Repository

README.md ---> Document for reviewers of the project

Predicting Song Popularity with ML.ipynb ---> Modeling and methods explaination in Jupyter Notebook

Presentation.pdf ---> PDF of presentation slides

