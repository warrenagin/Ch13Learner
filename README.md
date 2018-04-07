# Ch13Learner
Predicting Chapter 13 Case Results using a Neural Network and Random Forest Decision Tree
Machine learner for predicting success or failure from initial information in Chapter 13 cases.

Developed by Warren E. Agin
Copyright April 1, 2018, Warren E. Agin

Data used is FY 2008 through FY 2017 data downloaded from from the Federal Judicial Center’s Integrated Database at https://www.fjc.gov/research/idb 

Codebook effective January 2008 is available at https://www.fjc.gov/sites/default/files/idb/codebooks/Bankruptcy%20Codebook%202008%20Forward%20%28Rev%20January%202018%29.pdf

All files are released under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. You may obtain a copy of the license at https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode

#Jupyter notebooks dependencies:

	ipython 6.1.0
	jupyter_client 5.1.0
	numpy 1.14.2
	pandas 0.22.0
	pickleshare 0.7.4
	pydot1.2.4
	python 3.6.2	
	scikit-learn 0.19.1
	scipy 1.0.0
	tensorflow 1.5.0


#Data cleaning scripts:

	ExtractCh13Cases.ipynb

The full IDB database contains over 26 million records. This script extracts the Chapter 13 cases filed during fiscal years 2008 and 2009, and saves them to a file called Ch13Extract.csv. At this step, the database is reduced to about 2.9 million records. This dataset was used only for analysis purposes.
 
	ExtractCh13Cases3.ipynb

After initial data analysis, this script was used on the full IDB database based on the results of the analysis. Duplicate entries are eliminated and small numbers of records with null values, unusual termination codes, and no closing date are also excluded from the data set. The records retained are randomly shuffled before writing them to a file named Ch13TrimmedExtract.csv. This script creates a dataset with about 743,000 records, which is used as the base file for feature engineering.
	

#Data extraction and feature development files:

	Ch13GenerateMLSets.ipynb

This file takes the data from Ch13TrimmedExtract.csv, creates the features for use by the machine learning scripts, and assembles a training set and one or more test sets. The training set is engineered to include 50% successful bankruptcy cases, to ensure the models train on equal numbers of successful and unsuccessful cases. The models created use an engineered feature called SUCCESS to evaluate whether or not a bankruptcy case is successful. This script determines the SUCCESS feature value for each record and adds it to the training and test sets. The script creates a file named LEARNER_README.txt that contains information about the feature engineering process needed both for the machine learning scripts and for repeating the engineering process for deployment. Finally, it creates deployment files called DistrictSuccessRates.csv (which includes the calculated success rates for each district) and featureNames.csv (which contains the names of the engineered features).

	DistrictCodes.csv

The IDB database's DISTRICT field contains 94 different codes, one for each judicial district. This csv file contains the codes and the long text description for each court.

#Neural Network:

	Ch13SuccessLearner-DandW.ipynb

This script is based on a Tensorflow tutorial example and provides a logistic classifier, a neural network classifier, and a deep and wide classifier option. The neural network model used a training data size of 400,000 records, a batch size of 20, and no regularization. It is optimally run for 40-60 epochs to reduce overfitting. Five of the dense features are broken into buckets, and some of the available features are omitted from the training set. The model uses four hidden layers of size 256, 128, 64 and 32 ReLU neurons. 

	DistrictSuccessRates - NN.csv

This is the district success rates list generated by Ch13GenerateMLSets.ipynb and used with the neural network model.

	LEARNER_README - NN.txt

This is the learner_readme.txt file generated by CH13GenerateMLSets.ipynb in building datasets used for the neural network model.

#Random Forest:

	Ch13SuccessLearner-RF-Development.ipynb

A preliminary version of the random forests script used to evaluate results when varying parameters. Includes the ability to automatically run the model multiple times while logging results.

	Ch13SuccessLearner-RF-Testing Script.ipynb

This script was used to produce the final random forest decision tree model built on the scikit-learn RandomForestClassifier. This model achieved overall accuracy numbers of 70.33, 69.91 and 69.78 on three test sets, over a baseline of 61.6. When probability numbers expressed by the model are used, the model achieves prediction accuracy above 90% for about one-quarter of chapter 13 cases. The model was built on 420,000 records. With 74.2 accuracy on the training set, overfitting is reasonably low. The model uses 1000 CART estimators and gini impurity to fit the model. The script pickles the model as 'finalRFModel.sav' for later reuse and logs the accuracy, AUC, confusion matrix, and feature importances in a file named LOG.txt. The script also logs for each test record the probability score and actual result.

	DistrictSuccessRates - RF.csv

This is the district success rates list generated by Ch13GenerateMLSets.ipynb and used with the random forests model.

	LEARNER_README - RF.txt

This is the learner_readme.txt file generated by CH13GenerateMLSets.ipynb in building the datasets used for the random forests model.

	LOG for RF.txt

Log file created by the testing script - contains model parameters and the results for the training and test sets.

	finalRFModel.sav

The random forests model pickled. See sample code in the testing script for help in unpickling.
