# nlpDisasterTweets
![img](https://github.com/zadealfalah/nlpDisasterTweets/blob/main/kaggle_submission.PNG)

## General Info
In this notebook I attempt to predict whether a given tweet is about a real disaster or not for a small class project.  Some modeling choices were made specifically by the project brief to emphasize the 'small' nature of the project which lead to faster, worse results.  Details of improvements precluded by the brief are given in the [future work](#future-work) section.
This was done as part of a Kaggle challenge which evaluated based on F1 score.  The modeling was done with keras & tensorflow.
The final model F1 score that was received was around 0.774 as displayed in the above image.

The Kaggle challenge is linked [here.](https://www.kaggle.com/competitions/nlp-getting-started/overview/description)

## Data Prep & Model Selection
The data was given in the Kaggle notebook and certain expectations were given for EDA by the class.  Specifically, the balancing of the dataset despite the fact that the F1 score metric would allow for the imbalance in the classes.  
The tweet text was preprocessed with tweet-preprocessor and further cleaned with regular expressions.  

During model selection I ended up choosing to use an LSTM due to their ability to link words across cycles, ignoring 'noisy' words.  For example, 'That scary fire sure did destroy so many buildings' may be broken up by other modeling techniques and lose the connections between 'fire' and 'destroy' due to the intermediary 'sure did' phrase which is avoided with an LSTM.  

Different architectures including adding more layers, changing activation functions, adding dropouts, etc. were tested.  The best model was chosen as the simplest one that still produced 'good' results (high F1 score).  Hyperparameter tuning included the chosen optimizer, number of ngrams to keep, learning rate, etc.  

Model performance was judged based on F1 score, loss/accuracy graphs (esp. for choosing learning rate), and AUC before the final Kaggle submission.  

Our final model chosen used an LSTM as mentioned as well as dense layers with relu activation functions and a final decision with a sigmoid acrivation function.  Because this was a short project for a class, this was taken as our final model despite some obvious possible improvements which are described in the [future work](#future-work) section.


## Future Work
As mentioned already, this was a short project for a class and as such there were multiple ways of making a better model that were not utilized due to project specifications or time constraints.  Listed here are some suggested improvements to the model that could be used if this project were to be revisted.

- Add features.  Specifically the number of words, the number of unique words, and the number of mentions for each tweet seem like they could contain valuable insight as classification features.  EDA and testing would have to be done to make sure of this but these are easy to add and check.  Another possiblity might be the number of punctuation marks, as it would make sense if emergencies got a lot of exclimation points!
- Don't balance classes.  The classes are fairly close to balanced as they were, and the metric used by Kaggle was the F1 score which wouldn't be impacted by the imbalance.  As such we ended up just throwing away data for no reason due to the project brief for the class.  
- Add trigrams.  The models used only looked at uni and bigrams.  Adding trigrams could improve model performance significantly, though it would add a lot to the training time.  
- More text cleaning.  We did a basic preprocessing with the tweet-preprocessor and a small function but adding a more thorough cleaning would presumably drastically improve performance.  Removing special characters, punctuation, urls, common stopwords, replacing common abbreviations and slang, expanding common hashtags (which would not be captured by the embeddings as they are all written without spaces), etc. would all add to the model performance. 
- Using pre-trained models.  Using BERT would definitely allow for much better model performance, but that wasn't the point of the project so it could not be done.  
- Add cross validation.  This was possible to do for the project but was advised against due to it being given as a 'small' project.  Clearly adding cross validation would allow for better model performance.  
