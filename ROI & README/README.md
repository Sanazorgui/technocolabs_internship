# Loan-Completion-Prediction
## Predictive Modelling Using Social Profile in Online P2P Lending Market
The goal of the project is to predict if the borrower is going to complete the loan or not.
## Introduction to the project :
> Online peer-to-peer (P2P) lending markets enable individual consumers to
borrow from, and lend money to, one another directly. We study the borrower-,
loan- and group- related determinants of performance predictability in an
online P2P lending market by conceptualizing financial and social strength to
predict borrower rate and whether the loan would be timely paid. The result of
our empirical study, conducted using a database of 9479 completed P2P
transactions in calendar year 2007, provide support for the proposed
conceptual model in this study. The results showed that combing financial files
with social indicators can enhance the performance predictability in P2P
lending market. Although social strength attributes do affect the borrower rate
and status, their effects are very small in comparison to financial strength
attributes. This paper concludes with specific suggestions to borrowers and
lenders to increase their chances of funding to refunding completely in P2P
lending market, and a discussion of future research opportunities.

## Understanding the Dataset :
**Dataset consists of 113,937 samples and 81 features.**

> Features are = { ListingKey, ListingNumber, ListingCreationDate, CreditGrade, Term, LoanStatus, ClosedDate, BorrowerAPR, BorrowerRate, LenderYield, EstimatedEffectiveYield, EstimatedLoss, EstimatedReturn, ProsperRating (numeric), ProsperRating (Alpha), ProsperScore, ListingCategory (numeric), BorrowerState, Occupation, EmploymentStatus, EmploymentStatusDuration, IsBorrowerHomeowner, CurrentlyInGroup, GroupKey, DateCreditPulled, CreditScoreRangeLower, CreditScoreRangeUpper, FirstRecordedCreditLine, CurrentCreditLines, OpenCreditLines, TotalCreditLinespast7years, OpenRevolvingAccounts, OpenRevolvingMonthlyPayment, InquiriesLast6Months, TotalInquiries, CurrentDelinquencies, AmountDelinquent, DelinquenciesLast7Years, PublicRecordsLast10Years, PublicRecordsLast12Months, RevolvingCreditBalance, BankcardUtilization, AvailableBankcardCredit, TotalTrades, TradesNeverDelinquent (percentage), TradesOpenedLast6Months, DebtToIncomeRatio, IncomeRange, IncomeVerifiable, StatedMonthlyIncome, LoanKey, TotalProsperLoans, TotalProsperPaymentsBilled, OnTimeProsperPayments, ProsperPaymentsLessThanOneMonthLate, ProsperPaymentsOneMonthPlusLate, ProsperPrincipalBorrowed, ProsperPrincipalOutstanding, ScorexChangeAtTimeOfListing, LoanCurrentDaysDelinquent, LoanFirstDefaultedCycleNumber, LoanMonthsSinceOrigination, LoanNumber, LoanOriginalAmount, LoanOriginationDate, LoanOriginationQuarter, MemberKey, MonthlyLoanPayment, LP_CustomerPayments, LP_CustomerPrincipalPayments, LP_InterestandFees, LP_ServiceFees, LP_CollectionFees, LP_GrossPrincipalLoss, LP_NetPrincipalLoss, LP_NonPrincipalRecoverypayments, PercentFunded, Recommendations, InvestmentFromFriendsCount, InvestmentFromFriendsAmount, Investors}.
## Data Cleaning :
1) Checking Null values and Printing their missing percentage amd count.
2) Reformatting any feature with datatime with format '%Y-%m-%d %H:%M:%S'
>features = { ListingCreationDate, DateCreditPulled, LoanOriginationDate, FirstRecordedCreditLine, ClosedDate}
3) Handling missing values in FirstRecordedCreditLine, ClosedDate by adding upcoming date.
4) Filling some features by adding the mean in the missing samples.
> Features = { BorrowerAPR, EstimatedEffectiveYield, EstimatedLoss, EstimatedReturn, EmploymentStatusDuration, CreditScoreRangeLower, CreditScoreRangeUpper, RevolvingCreditBalance, BankcardUtilization, AvailableBankcardCredit, TotalTrades, TradesNeverDelinquent (percentage),TradesOpenedLast6Months, DebtToIncomeRatio}.
5) Filling some features by adding 0 in the missing samples.
> Features = { TotalProsperLoans, TotalProsperPaymentsBilled,OnTimeProsperPayments, ProsperPaymentsLessThanOneMonthLate, ProsperPaymentsOneMonthPlusLate, ProsperPrincipalBorrowed, ProsperPrincipalOutstanding, ScorexChangeAtTimeOfListing, CurrentCreditLines, OpenCreditLines, TotalCreditLinespast7years, InquiriesLast6Months, TotalInquiries, CurrentDelinquencies, AmountDelinquent, DelinquenciesLast7Years, PublicRecordsLast10Years, PublicRecordsLast12Months}.
6) Filling null values in BorrowerState with 'CA'.
7) Filling null values in Occupation with 'Other'.
8) Filling null values in EmploymentStatus with 'Unknow'.
9) Filling CreditGrade according to CreditScore.
> CreditScore < 300 will be 'NC'. <br>
> 300 < CreditScore < 559 will be 'HR'. <br>
> 560 < CreditScore < 599 will be 'E'.<br>
> 600 < CreditScore < 639 will be 'D'.<br>
> 640 < CreditScore < 679 will be 'C'.<br>
> 680 < CreditScore < 719 will be 'B'.<br>
> 720 < CreditScore < 759 will be 'A'.<br>
> CreditScore > 759 will be 'AA'.
10) Filling null values in LoanFirstDefaultedCycleNumber by -1.
11) Dropping features that are keys or have alot of null values.
> Features = { GroupKey, LisitingKey, LisitingNumber, LoanKey, MemberKey, LoanNumber}.
13) Dropping samples that have null values in some features.
> Features = { ProsperRating (numeric), ProsperScore, ProsperRating (Alpha)}.

## Feature Engineering :
1) Checking Correlation for numerical variables.
> Printing values in tables and on heatmap.
2) Printing Descriptive Statistics.
> using .describe()
3) Printing info of the dataframe to know the type of each feature.
> using .info()
4) Dropping samples with ListingCreationDate before 2008.
>  There was financial crisis in 2008.
5) Dropping features with datatime type.
6) Changing features with datatype boolean to float.
7) Removing duplications.
8) Visulaization of features with datatype object and detrmine what to do with it dropping or mapping.
> CreditGrade will be dropped as CreditScoreRangeLower & CreditScoreRangeUpper is equivalent to it.<br>
> ProsperRating (Alpha) will be dropped as ProsperRating (numeric) is equivalent to it.<br>
> BorrowerState will be dropped.<br>
> Occupation will be dropped.<br>
> LoanOriginationQuarter will be dropped.<br>
> EmploymentStatus will be mapped as 'Employed', 'Full-time', 'Self-employed', 'Part-time' will be 1 and the rest will be 0.<br>
>  IncomeRange will be mapped as i will put in it the mean of each range of them.<br>
>  LoanStatus will drop samples with 'Current' as it is hard to detrimine if it will complete the loan or not, and will map the rest as 'Completed' will be 1 and the rest will be 0.<br>
9) Dropping some features after looking to the correlation heatmap.
> Features = { EmploymentStatus, Investors, InvestmentFromFriendsAmount, InvestmentFromFriendsCount, Term, ListingCategory (numeric), EmploymentStatusDuration, IsBorrowerHomeowner, CurrentlyInGroup, CurrentCreditLines, OpenCreditLines, TotalCreditLinespast7years, OpenRevolvingAccounts, OpenRevolvingMonthlyPayment, InquiriesLast6Months, TotalInquiries, CurrentDelinquencies, AmountDelinquent, DelinquenciesLast7Years, PublicRecordsLast12Months, PublicRecordsLast10Years, RevolvingCreditBalance, TotalProsperPaymentsBilled, TotalProsperLoans, LP_CustomerPayments, LP_NetPrincipalLoss, EstimatedEffectiveYield, EstimatedLoss, LoanCurrentDaysDelinquent, LP_InterestandFees, LoanFirstDefaultedCycleNumber, Recommendations, PercentFunded }.
10) Handling outliner of the remaining features.
> After removing outliners some features become the same value for all the samples. So, they will be dropped.
> Features = { LP_NonPrincipalRecoverypayments, LP_GrossPrincipalLoss, LP_CollectionFees, ScorexChangeAtTimeOfListing, ProsperPrincipalOutstanding, ProsperPaymentsLessThanOneMonthLate, ProsperPrincipalBorrowed, OnTimeProsperPayments, IncomeVerifiable, DebtToIncomeRatio, TradesOpenedLast6Months, TradesNeverDelinquent (percentage), TotalTrades }.

## Models :
To predict the target, which is loan eligibility using binary classification, we decided to use our loan data on several models after a lengthy phase of EDA and feature engineering. The models used were: Logistic Regression, Random Forest, and KNN.
1/Logistic Regression
- Logistic Regression helps find how probabilities are changed with actions.
- The function is defined as P(y) = 1 / 1+e^-(A+Bx) 
- Logistic regression involves finding the **best-fit S-curve** where A is the intercept and B is the regression coefficient. The output of logistic regression is a probability score.
2/ Random Forest Classifier
- The random forest is a classification algorithm consisting of **many decision trees.** It uses bagging and features randomness when building each individual tree to try to create an uncorrelated forest of trees whose prediction by the committee is more accurate than that of any individual tree.
**Bagging and Boosting**: In this method of merging the same type of predictions. Boosting is a method of merging different types of predictions. Bagging decreases variance, not bias, and solves over-fitting issues in a model. Boosting decreases bias, not variance.
**Feature Randomness**: In a normal decision tree, when it is time to split a node, we consider every possible feature and pick the one that produces the most separation between the observations in the left node vs. those in the right node. In contrast, each tree in a random forest can pick only from a random subset of features. This forces even more variation amongst the trees in the model and ultimately results in lower correlation across trees and more diversification.
3/KNN 
-The k-nearest neighbors algorithm, also known as KNN or k-NN, is a non-parametric, supervised learning classifier, which uses proximity to make classifications or predictions about the grouping of an individual data point. While it can be used for either regression or classification problems, it is typically used as a classification algorithm, working off the assumption that similar points can be found near one another.
The evaluation was based on the Accuracy metric, and hyperparameter tuning was done using a variety of methods, including RandomizedSearchCV and GridSearchCV, in order to get the best results.
And we received very positive accuracy values of 97%, 98%, and 95%, respectively. 
Additionally, we attempted to solve a regression issue by attempting to predict the ROI (Rate of Interest) using a variety of models. The model that performed the best was the random forest, which attained an r2 score of 99%. 

## Saving Models :
we saved each model and scaler we used to be used later in deployment or at local host.
> All models are saved using pickle.dump except Neural Network was saved using save_model.

# Deployment :
## Flask : 
We created our app by using flask, then deployed it to heroku.<br>
We prepared the needed files to deploy our app sucessfully:<br>
> 1) Procfile: contains run statements for main file.
> 2) requirements.txt: contains the libraries must be downloaded by Heroku to run app file (main.py)  successfully.
> 3) runtime.txt: contains the required python version to let the app work successfully.

The files of this part is in Flask App folder.
> Decision_trees is the model used for prediction.<br>
> scaling_tree is the min_max_scaler used.<br>

You can acess to the app by using the following link :<br>
https://loan-completion-pred-flask.herokuapp.com/

> 3) runtime.txt: contains the required python version to let the app work successfully.

The files of this part is in Django App folder.
> neural_network is the model used for prediction.<br>
> scaling_nn is the min_max_scaler used.<br>

You can acess to the app by using the following link :<br>
https://loan-completion-pred-django.herokuapp.com/ <br>
>The app is deployed but there is an application error. This error occured as we replaced tensorflow with tensorflow-cpu to reduce the size of the app to be able to deploy it on heroku.




