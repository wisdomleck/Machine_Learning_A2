================= Term of Use =================

The data has kindly been provided to us, under the provision that any resulting work should cite these three resources:

What Yelp fake review filter might be doing?  A. Mukherjee, V. Venkataraman, B. Liu, and N. S.Glance,ICWSM, 2013.

Collective Opinion Spam Detection:  Bridging Review Networks and Metadata.  Shebuti Rayana,Leman Akoglu,ACM SIGKDD, Sydney, Australia, August 10-13, 2015


================= Files =================

1. review_meta_train.csv
This file contains the meta data and label for training instances.
Number of instances: 28068
Number of columns: 8
The columns are (the column names are in the first row):
	date, review ID, reviewer ID, business ID, vote_funny, vote_cool, vote_useful, rating

The class label is in the last column: rating. There are 3 possible ratings, 1, 3 or 5.

2. review_text_train.csv
This file contains the raw text data for training instances.
Number of instances: 28068
Number of columns: 1
The first row is the column name "review". The rows are corresponding to the meta file

3. review_meta_test.csv
This file contains the meta data for test instances.
Number of instances: 7018
Number of columns: 7
The columns are (the column names are in the first row):
	date, review ID, reviewer ID, business ID, vote_funny, vote_cool, vote_useful

4. review_text_test.csv
This file contains the raw text data for training instances.
Number of instances: 7018
Number of columns: 1
The first row is the column name "review". The rows are corresponding to the meta file

5. review_text_features_*.zip: preprocessed text features for training and test sets, 1 zipped file for each text encoding method

5.1 review_text_features_countvec.zip
(1) train_countvectorizer.pkl
This file contains the CountVectorizer extracted using the review text of the training data.
To load the file in Python:
	vocab = pickle.load(open("train_countvectorizer.pkl", "rb"))
	
To access the list of vocabulary (this will give you a dict):
	vocab_dict = vocab.vocabulary_
	
More about how to use the CountVectorizer can be found: https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html

(2) review_text_train_vec.npz
This file contains a sparse matrix of the Bag-of-Word representation of the review text for training data.
The dense version of this matrix should be [28068 * size of vocabulary], and the element (i,j) in the matrix is the count of each vocabulary term j in an instance i. The vocabulary corresponds to the vocabulary_ attribute in vocab (which can be checked as detailed in (1))

As a lot of elements are zeros in this matrix, it has been compressed to a sparse matrix. After loading, the sparse matrix can be used as a normal matrix for training or testing.

To load the sparse matrix:
	import scipy
	scipy.sparse.load_npz('review_text_train_vec.npz')

(3) review_text_test_vec.npz
This file contains a sparse matrix of the Bag-of-Word representation of the review text for test data. 
The dense version of this matrix should be [7018 * size of vocabulary]. The vocabulary is the one that has been extracted from training, but the elements in this matrix are the counts for each review in the test set.

To load the sparse matrix:
	import scipy
	scipy.sparse.load_npz('review_text_test_vec.npz')

5.2 review_text_features_doc2vec50.zip
(1) review_text_train_doc2vec50.csv
This file contains a matrix of Doc2Vec representation of the review text for training data, with 50 features.
The dimension of this matrix is [28068 * 50], and the element (i,j) in the matrix is a numeric value for feature j of an instance i. 

To load the matrix:
	import pandas as pd
	pd.read_csv(r"review_text_train_doc2vec50.csv", index_col = False, delimiter = ',', header=None)

(2) review_text_test_doc2vec50.csv
This file contains a matrix of Doc2Vec representation of the review text for test data, with 50 features extracted from the training data.
The dimension of this matrix is [7018 * 50], and the element (i,j) in the matrix is a numeric value for feature j of an instance i. 

To load the matrix:
	import pandas as pd
	pd.read_csv(r"review_text_test_doc2vec50.csv", index_col = False, delimiter = ',', header=None)
	
5.3 review_text_features_doc2vec100.zip
Similar to review_text_test_doc2vec50, except that 100 features are used for each instance

5.4 review_text_features_doc2vec200.zip
Similar to review_text_test_doc2vec50, except that 200 features are used for each instance
