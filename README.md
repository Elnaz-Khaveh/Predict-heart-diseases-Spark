# Predict-heart-diseases-Spark
Predicting Heart Diseases via Decision Trees & Random Forests 
Problem 1. Consider the “Key Indicators of Heart Disease” dataset as it is available from Kaggle:
https://www.kaggle.com/datasets/kamilpytlak/personal-key-indicators-of-heart-disease
You may download the dataset (in CSV format) from the above URL. This openly
available dataset captures 18 variables (9 booleans, 5 strings and 4 decimals) related to possible indicators of
heart diseases from about 320K patients in the U.S. The first (boolean) variable captures whether a patient
suffers from a heart disease (yes/no) and should be used as the target label for the following supervised
classification steps. Follow the general methodology provided in RunDecisionsTrees-shell.scala to
solve the following tasks.
(a) Load the entire CSV file into a corresponding DataFrame either directly via spark.read.option(
"inferSchema", true).option("header", true).csv(...) or via spark.createDataFrame(rdd)
.toDF(...) from an initial RDD within your Spark session. In case you chose the latter option,
also explicitly apply a proper schema (see the header of the CSV file) to this DataFrame with
meaningful attribute names for this dataset, either by providing the attribute names directly within
the toDF(...) method or by defining a new StructType with respective StructField entries to
provide the attribute names and their datatypes1.
(b) In the next step, we wish to include the form of cross-validations as they were introduced in the
lecture (Chapter 3) in order to more systematically learn the hyper-parameters of a Decision Tree
classifier. To do so, extend the given shell script by the following steps:
(i) Instead of applying a static 80%/10%/10% split, create a random split of the DataFrame
you constructed in (a) into 90% training and 10% testing data. Define a basic ML Pipeline2
consisting of the necessary stages to train a Decision Tree model by using the 90% split as
training data.
(ii) Consider the ML Tuning3 guide of Spark to implement a fully automatic hyper-parameter tuning
step into your script. Specifically, use your pipeline to initialize a 5-fold cross-validation loop
over a fixed hyper-parameter setting (using impurity="entropy","gini", depth=5,10,15
and bins=20,50,100 as parameter ranges).
(iii) Instead of the MulticlassMetrics package used in the Moodle script, use the BinaryClassificationMetrics in your pipeline to measure the average accuracy over the two possible labels
of heart disease for each of the cross-validation and hyper-parameter iterations. Then fit the
model to the training data (caution: this step is expensive!), and finally save the best obtained
Decision Tree model into a file.
(iv) Finally, measure precision, recall and accuracy over the two possible labels of heart disease for
your best ML model and hyper-parameter setting over the 10% test split you created in (i) by
using again the BinaryClassificationMetrics package of Spark.
(c) Repeat the methodology described in (b) by training a Random Forest classifier instead of a single
Decision Tree. Investigate the additional range of numTrees=5,10,20 to also find the best amount
of trees (using "automatic" training mode) in your Random Forest.
Once more, identify the best overall choice of hyper-parameters you obtain from the cross-validations
as described in (i)–(iv) and measure the final accuracy you obtain for these hyper-parameters with
the one that was obtained by the simpler 80%/10%/10% split of the original script. Also here, use
the 10% testing set to measure the accuracy of your final model.
Report the resulting parameters and the Spark runtimes of this experiment in your Problem 1.txt file.
