# Automated-Essay-Evaluation-using-WordEmbeddings


## Aim of the model:
The aim of the model was to construct a NLP model which would automate the task of scoring a given paragraph based on the Content, Grammer and Flow. However for this model Grammar and Flow was kept out of the picture and more focus was directed in understanding the content.


### Steps Involved:
#### 1.	Importing the libraries:
The Libraries majorly involved are: tensorflow, keras, nltk and pandas. Lists were handled by numpy. For practical use, use of genism is recommended, for obtaining the pretrained word vectors. The method used here the use of Word Embedding vectors which is a generalized format of Word2Vec from the genism library.

#### 2.	Importing the Datasets and cleaning the datasets:
Three datasets were imported namely “train.csv”, “test.csv” and “all_prompts.csv”. The third dataset consisted of the prompt questions to which the answers were present in the train and test files. 

Now the approach is such that, we need to assign same word embedding to both test and train sets which is the general working of the Word2Vec with predefined embedding. Hence, to make this able, the dependent variable column was stored in a separate variable as a list and both the datasets are joined. By this, the repeated and rather logically wrong task of passing the datasets two separate times is prevented and the embedding are assigned as per same vocabulary.

To preserve the context of the embedding and hence preserving the data, the questions were concatenated with the paragraphs under essay column and were passed for being embedded. In this way the question and answers both are passed into the models and hence conveying the complete meaning. In addition, since the dataset with the training and test data together was passed, this is only a one-time work.

Next, the vocabulary was obtained and hence we have a count of the number of words and what the words are in a list. 

#### 3.	 Assigning word embedding:
Now a one hot vector representation of every word in the sentences is done which ultimately will be converted to a vector of higher dimension, by the Embedding layer present in the neural network. Here we separate, the original training dataset (which then undergoes train test split) and the test dataset, after the vectors are assigned.

#### 4.	The Neural Network:
The network consists of Embedding layer, which will convert the word vectors to a higher dimension. Next is a series of LSTM layers, the number of layers are decided by the tuner at the end of the hyper parameter tuning. After this comes an optional dropout layer, to prevent overfitting, and the final layer being a dense layer with one neuron.

After the tuning of the model and obtaining the best model, we train the model on the training data (X_train, y_train). Then we find the best epoch index and run it again on the same X and y, upto the particular epoch value. After this, we save the model and evaluate it on X_test and y_test.

Next, we make the prediction on the original dataset for predictions (test.csv) and store the variables in the csv file.


The purpose of using LSTM is because of the purpose of remembering the useful context of the paragraphs and using it further to grade the sentences. If we intent to score on thee grammatical point of view then use of Bidirectional LSTM will be better and faster.
