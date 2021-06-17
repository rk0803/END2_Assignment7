# END2_Assignment7
## Assignment 7
### A note on file names
**Assignment7_1LSTM** is part 1 of the assginment which is re-submit of Assignment 5 <br/>
**Assignment7_2qa** and **Assignment7_2quora** is part2 of the assignment <br/>
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
Readme file of stanford dataset revealed <br/>
- The *datasetSentences.txt* contains the sentence_index, sentence separated by a tab.
- The *datasetSplit.txt* contains the sentence_index (corresponding to the index in datasetSentences.txt file) followed by the split_index separated by a comma. split_index are 1, 2 or 3 indicating:<br/>
	1 = train, 	2 = test, 	3 = dev<br/>
 (This division into train/test/dev was ignored as one of the requirement listed above specifically says, dividing the dataset into *train* and *test* in 70/30 ratio)
- The *dictionary.txt* contains phrase_id and phrase, separated by  "|"
- The *sentiment_labels.txt* contains  phrase ids, sentiment_values, separated by "|"
From this we can recover the 5 classes by mapping the positivity probability as described above for "very negative", "negative", "neutral", "positive", "very positive", respectively.

#### Approach
The dataset was thoroughly studied, a strategy was formulated to create dataset of review sentences with labels.
1. Join on sentence_index to create a set with sentence_index, sentence, split_index
2. Join on sentence and phrase to create a set having sentence_index, sentence, phrase, phrase_id.
3. Join on phrase_id ( of this set) and phrase_ids (from sentiment_labels.txt) to bring in the respective sentiment values.
4. Convert the sentiment values into labels using the positivity probability distributon listed above.
5. Select relevant fields (sentence, label) from this set created.
6. Finally split the dataset into train and test in 70/30 ratio.
### Discussion
Now we have the distribution of classes in the training set as shown below (as we have ignored the split specified with the dataset) :
![image](https://user-images.githubusercontent.com/82941475/122326485-00083700-cf4a-11eb-9d37-7e670eb1cbad.png)<br/>
It can be seen that training dataset has sentences with labels other than 5 nearly equal.

### Model 
LSTM model was built and tested with hyperparameters as given in the table below:
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
Best test accuracy achieved was 40.5%<br/>
Graph below shows the variation in loss for testing  and training.<br/>
![image](https://user-images.githubusercontent.com/82941475/122327349-56c24080-cf4b-11eb-93d2-d961b1e1211d.png)

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

## *Part 2*
In part2 of this assignment, we were to train model written in the class on the following two datasets : "
http://www.cs.cmu.edu/~ark/QA-data/ 
https://quoradata.quora.com/First-Quora-Dataset-Release-Question-Pairs
#### Requirements
- For both the datasets, the task is NMT.
- Preprocess these datasets to be used for NMT.
- For the QA-Data, given the a question, generate the answer
- For Quora dataset, given the input question, generate the similar question. [Use only those questions marked as duplicate in the dataset]
#### Initial Investigations
##### QA Dataset
The readme file for this dataset highlighted the following points:
- There are three directories, one for each year of students: S08, S09, and S10.

- The file "question_answer_pairs.txt" contains the questions and answers. The first line of the file contains 
column names for the tab-separated data fields in the file.<br/>

*ArticleTitle    Question        Answer  DifficultyFromQuestioner        DifficultyFromAnswerer  ArticleFile*<br/>

Field 1 is the name of the Wikipedia article from which questions and answers initially came.<br/>
Field 2 is the question.<br/>
Field 3 is the answer.<br/>
Field 4 is the prescribed difficulty rating for the question as given to the question-writer. <br/>
Field 5 is a difficulty rating assigned by the individual who evaluated and answered the question, 
which may differ from the difficulty in field 4. <br/>
Field 6 is the relative path to the prefix of the article files. html files (.htm) and cleaned 
text (.txt) files are provided.<br/>
From this dataset, we selected only **Field 2(Question)** and **Field 3(Answer)** as needed. This data was selected from the three directories *S08, S09, S10* and concatenated to create one dataset.##### QA Dataset

##### Quora Dataset
The highlights of this dataset are:
- Contained a single file quora_duplicate_questions.tsv
- The fields in the dataset are as :<br/>
*id 	qid1	qid2	question1	question2	is_duplicate*
From this dataset, we only selected **question1** and **question2** pairs, for which **is_duplicate is True**

### Group Members
Ritambhra Korpal<br/>
Chaitanya Vanapamala <br/>
Pralay Ramteke <br/>
Pallavi <br/>

