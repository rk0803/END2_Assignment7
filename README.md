# END2_Assignment7
Assignment 7
### a note on file names
**Assignment7_1LSTM** is part 1 of the assginment which is re-submit of Assignment 5 <br/>
**Assignment7_2qa** and Assignment7_2quora** is part2 of the assignment <br/>
**dataset_gen** is the notebook which collects the SST data, augments it, and stores it by pickling <br/>
**trainset_new.pkl, testset.pkl, valset.pkl** are the files which are used in 5_2 series. <br/>
**test_sent.pkl** is the file which has the test set of sentences out of which 10 are randomly chosen to get the sentiments.

## *Part 1*
#### Background
Part 1 is re_submission of Assignment5 on building a Sentiment Claasifier using Stanford Sentiment Analyis Dataset.
#### Requirements
-The dataset to be built using our pre-processing statements rather than using pytreebank
-The dataset needed to built taking datasetSentences.txt and five classes to be created using the following range of sentiment values:
[0-0.2 : 1, 0.2-0.4 : 2, 0.4-0.6 : 3, 0.6-0.8 : 4, 0.8-1.0: 5] 
-Dataset to be split into Train/Test in 70/30 ratio (and no validation set)
#### Initial Investigations
Readme file stanford dataset revealed <br/>
-The datasetSentences.txt contains the sentence index, followed by the sentence string separated by a tab. These are the sentences of the train/dev/test sets.

-ThedatasetSplit.txt contains the sentence index (corresponding to the index in datasetSentences.txt file) followed by the set label separated by a comma:
	1 = train, 	2 = test, 	3 = dev
 (This division was ignored as one of the requirement listed above specifically says, dividing the dataset into *train* and *test* in 70/30 ratio]
-The *dictionary.txt* contains all phrases and their IDs, separated by a vertical line |
-The *sentiment_labels.txt* contains all phrase ids and the corresponding sentiment labels, separated by a vertical line.
From this we can recover the 5 classes by mapping the positivity probability as described above for very negative, negative, neutral, positive, very positive, respectively.
The dataset was studied and a strategy was formed to create a datase
### Approach
The dataset was thoroughly studied, a strategy was formulated to create complete review sentences with labels.
1. Join on sentence_index to reate a set with sentence_index, Sentence, split_index
2. Join on sentence and phrase to create a set having sentence_index, sentence, phrase, phrase id.
3. Join on phrase id ( of this set) and phrase_ids (from sentiment_labels.txt) to bring in the respective sentiment values.
4. Convert the sentiment values into labels using the positivity probability distributon listed above.
5. Finally split the dataset into train and test in 70/30 ratio.
### Discussion
Now we have the distribution of classes in the training set as shown below (as we have ignored the split specified withthe dataset) :
![image](https://user-images.githubusercontent.com/82941475/120589588-b2be9c80-c456-11eb-8bc3-cc5d444ae2f5.png)
### Model 
LSTM models was built and tested with hyperparameters as given in the table below:
|Hyper parameter| Value|
|---------------|------|
|Size of Vocab  | No of words in the text|
|Embedding Dimension| 300|
|No. of Hidden Nodes| 100|
|No. of output Nodes|5|
|No. of Layers| 2|
|Dropout| 0.2|
Regularisation chosen was L2 with lambda=0.001.
### Results
Best test accuracy achieved was 40.5%
Graph below shows the variation of loss in testing  and training.

### Sample 10 Sentences randomly chosen from test set and their sentiments
|Sentence| Sentiment|
|-------- |-------------|
|Well-shot but badly written tale set in a future ravaged by dragons . |  Very Positive|
|Elicits more groans from the audience than Jar Jar Binks , Scrappy Doo and Scooby Dumb , all wrapped up into one . |  Negative|
|The year 's happiest surprise , a movie that deals with a real subject in an always surprising way . |  Positive |
|... ambition is in short supply in the cinema , and Egoyan tackles his themes and explores his characters ' crises with seriousness and compassion . |  Positive|
|What really surprises about Wisegirls is its low-key quality and genuine tenderness . |  Positive|
|A splendid entertainment , young in spirit but accomplished in all aspects with the fullness of spirit and sense of ease that comes only with experience . |  Positive|
|Almost every scene in this film is a gem that could stand alone , a perfectly realized observation of mood , behavior and intent . | Positive|
|Too sincere to exploit its subjects and too honest to manipulate its audience . | Negative |
|At heart the movie is a deftly wrought suspense yarn whose richer shadings work as coloring rather than substance . |  Positive|
|Although based on a real-life person , John , in the movie , is a rather dull person to be stuck with for two hours . | Positive |


### Group Members
Ritambhra Korpal<br/>
Chaitanya Vanapamala <br/>
Pralay Ramteke <br/>
Pallavi <br/>

