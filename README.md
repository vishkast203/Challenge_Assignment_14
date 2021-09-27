# Challenge_Assignment_14
Assignment_14: Algorithmic Trading
Executive Summary: The objective of this project was to evaluate & improve the existing algorithmic trading systems and maintain the firm’s competitive advantage in the market. THis was to be done by enhancing the existing trading signals with machine learning algorithms that can adapt to new data. This evaluation was performed comparing the company's existing algorithim against a Logistic Regression Model(LRM). 

The SVC model provided a slightly better accuracy score (55%  vs. 52%). For Negative Reutrns(-1), the LRM shows improved scores for Precision [precision = TPs ÷ (TPs + FPs)] a.k.a the positive predictive value (PPV), a much improved recall [recall = TPs / (TPs + FNs)] &  f1-score [F1 = 2 × (precision × recall) ÷ (precision + recall)]. These results are summarized below:
SKLearn's SVC Classifier Model:
              precision    recall  f1-score   support

        -1.0       0.43      0.04      0.07      1804
         1.0       0.56      0.96      0.71      2288

The precision is 0.43 for the −1.0 class and 0.56 for the 1.0 class. The recall is much higher for the 1.0 class. Based on the higher recall, it seems that the SVC model (based on the training data) is better at predicting the 1 class than the −1 class.

    accuracy                           0.55      4092
   macro avg       0.49      0.50      0.39      4092
weighted avg       0.50      0.55      0.43      4092

Logistic Regression Model(LRM):
              precision    recall  f1-score   support

        -1.0       0.44      0.32      0.37      1804
         1.0       0.56      0.68      0.61      2288
The precision is 0.44 for the −1.0 class and 0.56 for the 1.0 class. The recall is much higher for the 1.0 class. Based on the higher recall, it seems that the LRM model (based on the training data) is also better at predicting the 1.0 class than the −1.0 class.

    accuracy                           0.52      4092
   macro avg       0.50      0.50      0.49      4092
weighted avg       0.51      0.52      0.51      4092

For the Positive Returns(1.0), the LRM Model does not improve upon the SVC algorithm. Therefore it would be prudent to run other algorithms for comparitive purposes (DecisionTree &/or AdaBoost) for further comparisons.

Dependencies,Libraries & Programs:
The  programs used were Python 3.8.

Libraries & Dependencies:  pandas, numpy, Pathlib, hvplot & matplotlib to generate charts. The libraries imported were sklearn (Standard Scalar, Dateoffset, metrics &  Classificaion Reports)

Steps followed to evaluate the model: 

The inital dataframe was downloaded by reading a csv file. This dataframe was then filtered to include the index & close columns. The pct.change function was used to geerate the Actual Returns column.
The next step the Trading Signal windows were generated (Shport = 4 & Long = 100) & the ROlling Avergaes were generated for each window as seperate columns. 
The Signals DF was further  set up to populate a new column for positive (1.0)  & Negative(-1.0) returns. The Strategy Column was based on the product of the "Actual Returns" & the value in the Signal column.

The data was next split into Training & TEsting datasets. The training periods were defined using the Dataoffset functions as Start(2015-04-02 15:00:00) & End(2015-07-02 15:00:00).

The X & y Trains were generated & the Std Scalara model steps were followed to use the SVM learining method to fit the data & the basic classification report was generated. 

              precision    recall  f1-score   support

        -1.0       0.43      0.04      0.07      1804
         1.0       0.56      0.96      0.71      2288

    accuracy                           0.55      4092
   macro avg       0.49      0.50      0.39      4092
weighted avg       0.50      0.55      0.43      4092


Finally a Predictions DF was created &  a Plot of the Actual Returns vs. Strategy Returns was generated using the Plot fucntion. 

The First Step to Tune the Model was to re-define the dataset using the same tools (SVM algorithm) but with a DtaOffset of 4 months. The follwoing improvements were seen: 

           precision    recall  f1-score   support

        -1.0       0.64      0.28      0.39        76
         1.0       0.61      0.88      0.72        97

    accuracy                           0.61       173
   macro avg       0.62      0.58      0.55       173
weighted avg       0.62      0.61      0.57       173

The improved Accuracy score to 0.61. The orecision & f1 scores greatly improved for the Negative Returns (-1.0). The recall value dropped for the positive returns.  

Next we Tuned the trading algorithm by adjusting the SMA input features to set the Short Window = 7 &  the Long Window = 120. The Classification Report was as follows:
             precision    recall  f1-score   support

        -1.0       0.44      0.72      0.55      1734
         1.0       0.56      0.28      0.37      2218

    accuracy                           0.47      3952
   macro avg       0.50      0.50      0.46      3952
weighted avg       0.51      0.47      0.45      3952

THis resulted in  drop in Accuracy to 0.47 from 0.55. This change in the SMA windows shows better outpiu=uts for the Negative Returns vs, the Positive Returns.

A third iteration of the model using SHort =5 periods &  Long = 90 periods resulted in the following:
         precision    recall  f1-score   support

        -1.0       0.44      0.86      0.58      1589
         1.0       0.59      0.15      0.24      2066

    accuracy                           0.46      3655
   macro avg       0.51      0.51      0.41      3655
weighted avg       0.52      0.46      0.39      3655

This seemed to result in a small reduction in the quality of the accuracy scores to the original & previous iterations but a better separation betweenn the Actual vs. Strategy Returns. 


Finally the Logistic regression model was run based offthe original dataset & the results showed a improved precision & reduced accuracy as previously discussed:

              precision    recall  f1-score   support

        -1.0       0.44      0.86      0.58      1544
         1.0       0.60      0.16      0.26      2004

    accuracy                           0.47      3548
   macro avg       0.52      0.51      0.42      3548
weighted avg       0.53      0.47      0.40      3548