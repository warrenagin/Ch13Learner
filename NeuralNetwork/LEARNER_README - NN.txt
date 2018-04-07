"Working with a data file of 743153.0 size. 
successCount: 200000 
failureCount: 200000 
trainingSetSize: 400000.0 
testCount: 30000 
testSetSize: 30000.0 

The median value and cutoff values for the following original data fields will be needed to calculate features for deployment.

median value for REALPROP = 140000; cutoff = 1910000.0 
median value for PERSPROP = 17905; cutoff = 618500.0 
median value for UNSECPR = 0; cutoff = 336900.0 
median value for UNSECNPR = 29797; cutoff = 336900.0 
median value for AVGMNTHI = 3303; cutoff = 36389.03 
median value for AVGMNTHE = 2754; cutoff = 33624.15 

The sample size cutoff for districts is 368 and will be needed for deployment, in conjunction with the success rate for the total training set
The success rate for the total training set is 0.4 

A list of districts and their associated success ratios is saved in the file named DistrictSuccessRates.csv. 13 districts had sample sizes under the cutoff size and were assigned the success rate for the total training set.

The training data file is named trainingFile.csv, the test data file is named testData.csv, and an ordered list of feature names is in the file named featureNames.csv
"
