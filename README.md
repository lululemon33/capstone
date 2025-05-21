## Capstone Project Overview

Machine learning has proven to be an effective ancillary tool the field of cyber seucrity when used to detect anomalous activity related to a network breach or a compromise.  It can be used in tandem with other detection methods (e.g. hueristics, signature, etc.) to detect anomalous traffic or activity within intrusion detection systems.  This repository and related notebook demonstrates the use of ML to detect anomalous actvity on the NSL-KDD dataset which contains various fields/features related to network and host telemetry.  A baseline model is built and different classification models are trained and tested on the data within the NSL-KDD dataset.  The resulting models are tuned and trained to identify previously labeled anomalous instances within the dataset.  Models are then tested against a subset of the dataset, whose data is completely seperate from the training dataset, to see the accuracy of the models prediction with regards to classifying the instances are normal or anomalous.

Computer networks and the communications that occur within them, as well as between different networks, needs to be monitored in order to detect any type of external attack or any type of internal malicious activity which would indicate that a breach has occured.  Typically an Intrusion Detection/Prevention System will match traffic against against known patterns related to malicious activity via the use of regular expression pattern matching.  This pattern matching is referred to as signature based detection.  However, this can be prone to error and at times will produce many false positives.

The objective of this project is to see if machine learning can be used as an additional tool to try and detect malicious activity from the data collected related to network telemetry to augment the traditional, signature based detection used by Intrusion Detection/Prevention systems.  Please note, the project will not compare the methods against each other with regard to efficacy, rather it will only measure the efficacy of ML when applied to the same data with the intent of using ML to detect malicious activity that has already been tagged beforehand (supervised learning).  Please note, the use of machine learning to detect malicious activity from network telemetry is typically referred to as "anomaly based detection".

The NSL-KDD dataset has been used for this project: https://www.kaggle.com/datasets/hassan06/nslkdd.  It does not include redundant records in the train set, so the classifiers will not be biased towards more frequent records.  There are no duplicate records in the proposed test sets; therefore, the performance of the learners are not biased by the methods which have better detection rates on more frequent records.  The number of selected records from each difficultylevel group is inversely proportional to the percentage of records in the original KDD data set. As a result, the classification rates of distinct machine learning methods vary in a wider range, which makes it more efficient to have an accurate evaluation of different learning techniques.  The number of records in the train and test sets are reasonable, which makes it affordable to run the experiments on the complete set without the need to randomly select a small portion. Consequently, evaluation results of different research works will be consistent and comparable.^1

## Exploratory Data Analysis of the dataset

The exploratory data analysis reveals the following:
  1) is_host_login feature only has data with values of 0.  This could be dropped but it will be kept because this same field could appear in anomalous labeled activity within a subsequent instance of a similar dataset.
  2) Protocol used within the dataset is mostly TCP.  This is expected.
  3) Most of the malicious activity was identifed as havin place with the "private" application layer protocol.
  4) The data is well balanced between "attack" and "normal" labels.
  5) A number of features do not have any kind of distribution as shown by the bar charts: serror_rate, srv_serror_rate, dst_host_serrror_rate and dst_host_srv_rate.  These features can be dropped.

 ## Modeling

 After scaling and encoding the data, a Logistic regression model was used as a baseline without any optimization of its hyperparameters.  Logistic Regression with cross validation and hyperparameter tuning along with XGBoost and RandomForestClassifier models were used to compare resulting metrics.  The models ran on the reduced feature set resulting from the initial principal component analysis (PCA) performed.  The models produced the following results:

#### 	 Model  		  ROC_AUC    Accuracy  F 1       Precision   Recall <br>
Baseline_Model      0.886264   0.88327   0.874053  0.881413    0.866814 <br>
logistic_regression 0.900135   0.882239  0.875047  0.867775    0.882443 <br>
xgboost             0.999991   0.998571  0.998471  0.99881     0.998131 <br>
randomforestclass   0.99999    0.99869   0.998598  0.999235    0.997961 <br>

## Conclusion

When comparing the above results to the XGBOOST model results the two seem to be very similar, however, the RandomForestClassifier model produced 2 more false negatives then the XGBOOST model. In other words, the XGBOOST model was a little less precise then the RandomForestClassifier model but it had a better recall score. With regards to anomaly detection, recall is a more important metric as it can be used to minimize false negatives which are more dangerous than false positives. Based on the above metrics and confusion matricies, the XGBOOST model seems to slightly outperform the RandomForestClassifier model. In conclusion, both models seem to be very accurate and precise.

In summary machine learning seems to accurately predict anomalous activity when used in a supervised learning example such as the one used in this report. As for the type of classification machine learning models XGBOOST and RandomForestClassifier seem to produce fairly accurate results. XGBOOST seems to be slighlty better at reducing false negatives which ideally need to be minimized to address this prticular use case for machine learning.


## References
1 - https://www.kaggle.com/datasets/hassan06/nslkdd
