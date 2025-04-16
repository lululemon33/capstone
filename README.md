## Capstone Project Overview

This is the exploratory data analysis and initial baseline modeling for the Emeritus UC Berkeley School of engineering AI/ML professional certificate program.  Within this phase of the project the objective is to perform initial EDA to see what the data can reveal beyond formal modeling, hypothesis testing task and data training to provide a better understanding of dataset variables and the relationships between them.

Computer networks and the communications that occur within them, as well as between different networks, needs to be monitored in order to detect any type of external attack or any type of internal malicious activity which would indicate that a breach has occured.  Typically an Intrusion Detection/Prevention System will match traffic against against known patterns related to malicious activity via the use of regular expression pattern matching.  This pattern matching is referred to as signature based detection.  However, this can be prone to error and at times will produce many false positives.

The objective of this project is to see if machine learning can be used as an additional tool to try and detect malicious activity from the data collected related to network telemetry to augment the traditional, signature based detection used by Intrusion Detection/Prevention systems.  Please note, the project will not compare the methods against each other with regard to efficacy, rather it will only measure the efficacy of ML when applied to the same data with the intent of using ML to detect malicious activity that has already been tagged beforehand (supervised learning).  Please note, the use of machine learning to detect malicious activity from network telemetry is typically referred to as "anomaly based detection".

The NSL-KDD dataset has been used for this project: https://www.kaggle.com/datasets/hassan06/nslkdd.  It does not include redundant records in the train set, so the classifiers will not be biased towards more frequent records.  There are no duplicate records in the proposed test sets; therefore, the performance of the learners are not biased by the methods which have better detection rates on more frequent records.  The number of selected records from each difficultylevel group is inversely proportional to the percentage of records in the original KDD data set. As a result, the classification rates of distinct machine learning methods vary in a wider range, which makes it more efficient to have an accurate evaluation of different learning techniques.  The number of records in the train and test sets are reasonable, which makes it affordable to run the experiments on the complete set without the need to randomly select a small portion. Consequently, evaluation results of different research works will be consistent and comparable.^1

## Exploratory Data Analysis of the dataset

The exploratory data analysis reveals the following:
  1) is_host_login feature only has data with values of 0.  This can be dropped
  2) Protocol used within the dataset is mostly TCP.  This is expected.
  3) Most of the malicious activity was identifed as havin place with the "private" application layer protocol.
  4) The data is well balanced between "attack" and "normal" labels.
  5) A number of features do not have any kind of distribution as shown by the bar charts: serror_rate, srv_serror_rate, dst_host_serrror_rate and dst_host_srv_rate.  These features can be dropped.

 ## Modeling

 After scaling and encoding the data, a Logistic regression model was used as a baseline without any optimization of its hyperparameters.  The model ran on the reduced feature set resulting from the initial principal component analysis (PCA) performed.  The model produced the following results:

 	   			ROC_AUC	    Accuracy	F1          Precision 	Recall
Baseline_Model	0.933411	0.897361	0.892893	0.871312	0.91557
