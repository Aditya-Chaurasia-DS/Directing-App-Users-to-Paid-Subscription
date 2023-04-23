# Directing-App-Users-to-Paid-Subscription
Bussines Problem

The Financial Technology company (Fin-Tech Company) launch there a mobile app. This app used for financial purposes like bank loans, savings, etc. in one place. It has two versions free and premium. The free version app contains basic features and customer wants to use the premium feature then they have to pay some amount to unlock it.
he main goal of the company is to sell the premium version app with low advertisement cost but they don’t know how to do it. That’s a reason they are provided the premium feature in the free version app for 24 hours to collect the customer’s behavior. After that, the company hired the Machine Learning Engineer to find insight from the collected data (customer’s behavior).

The job of the ML engineer is to find or predict new customer who is interested to buy the product or not. If the customers will buy a product anyway so no need to give an offer to that customer and loss the business. Only give offers to those customers who are interested to use premium version app but they can’t afford its cost. So the company will give offers to those customers and earn more money.

Directing-Customers-to-Subscription-Products-through-App-Behavior-Analysis
==> A Fintech Case Study
animated-globe In today's market many companies have a mobile presence. Often, these companies provide free products/services in their mobile apps in an attempt to transition their customers to a paid membership. Some examples of paid products, which originate from free ones, are YouTube Red, Pandora Premium, Audible Subscription, YouTube Premium, and You Need a Budget. Since marketing efforts are never free, these companies need to know exactly who to target with offers and promotions.

Market: The target audience is customers who use a company's free products. In this case study, this refers to users who installed (and used) the companies free mobile app.
Product: The paid memberships often provide enhanced versions of the free products already given for free, alongside new features. For example, Youtube Red allows you to leave the app while still listening to a video.
Goal: The objective of this model is to predict which users will not subscribe to the paid membership, so that greater marketing efforts can go into trying to convert them to paid users. User-Behavior
Business Challenge
In this Case Study we will be working for a fintech company that wants to provide its customers with a paid mobile app subscription that will allow them to track all of their finances in one place. To attract customers, the company releases a free version of their app with some of the main features unlocked.
The company has tasked you to identify which users will mostly likely NOT enroll in paid products, so that additional offers can be given to them. Because of the costs of these offers, the company does not want to offer them to everybody, especially customers who were going to enroll anyways. dd3899043b8f39dd7cbb301db09a19b3
DATA
By working for the company. We have access to each customer's app behavior data. This data allows us to see the date & time of app installation, as well as the features the users engaged with within the app. App behavior is characterized as the list of app screens the user looked at, and whether the user played the financial mini-games available.
The app usage data is only from the user's first day in the app. This limitation exists because users can enjoy a 24-hour free trial of the premium features, and the company wants to target them with new offers shortly after the trail is over.
The Data for this project is from manufacturing fields based on trends found in real world case studies. The fields describe what companies usually track from their users.
Data Description
User : this is Unique id of each perticuter user of app
first_open : this is the date/month/year, time the user frist time open the app
dayofweek : this shows the day out of 7 days a week an user join the app where 0:Sunday & 6:Saturday
hour : This is outoff 24 hour of day the user 1st open the app
age : This is simply the age of the user
screen_list : This describe the every single screen name the user visited in that 1st 24-hour (screen name seperated by comma)
numscreens : The Number of screen the user visited in 1st 24 hour
minigame : The app has minigame feature, this shows whether the player played any minigame of Not (1:Played, 0: Not Played)
liked : There are like button for each feature in the app, shows whether the user cliked any like button of any feature in app or NOT (1: click like button, 0: Not clicked)
used_premium_feature : This shows whether the user used any premium feature (that is for free in 1st 24 hour) or not in 1st 24 hour (1: used, 0: not used)
enrolled : This is target that shows whether the user enrolled to premium after the free trial (1: enrolled, 0: not enrolled)
enrolled_date : date & time of enrollment to premium product if they enrolled to premium agifcolossaltd2opt
Libraries & Data-sets
image image image image Observations:

Most of the users join app during weekends
Most of the users 1st open the app around 15 that is around 3PM
Most of users are aged around 30 Years
Most of users visited around 20 screens of app
Not many users played any minigames
Not many users press the like button
Not many user used premium feature in 1st 24 hours image image Observarions:
dayofweek is least positively correlated & says that if you join the app in day 0(sunday) then their is most likely to get enrolled to the premium features
Hour is negatively correlated with target variable shows the earlier the hour(in night) the most likely to get enrolled
age is also negatively correlated reflects that the younger users are most likely to get enrolled
Numscreen is positively correlated with target shows that more the no. of screen user visits more chances of getting enrolled
minigame also shows that more the minigame user play more chances of getting enrolled
liked is very least negative which does not have much impact in target
interestingly used_premium_feature is negatively correlated with response meaning that if user used the premium feature in 1st 24 hour that he/she might not enroll after the trial version of premium features image image All the independent features are having very less correlation among themselves, so their is very less chance of multicollinearity problem
Feature Engineering - Response variable
image image image

Here we observe that most of users enrolled in 1st 2000 Hour but their might be case that most enrollment is in 1st 100 or 500 hours, lets zoom the plot image image
Here we observe that most of users enrolled in 1st 100 Hour but let's zoom the plot again
image image

Here we observe that most of users enrolled in 1st 10 Hour but let's zoom the plot a bit more
image image

Here we observe that most of users enrolled in 1st 1 Hour but let's zoom the plot one more time.
image image

Here we observe that most of users enrolled in 1st 10% of hour that is in 1st 6 minutes but let's zoom again
image image

Here we conclude that most of users (more that 20000 out-off total 50000 users) do not used the 1st 24 hour premium free trial & infact they direcly jumped to the premium at the time of they 1st open the app
We choose cut-off as 48 hours that is whoever difference is less than 48 is classified as enrolled else not
image

Feature Engineering - Independent variables
image

Funnels : Funnels are group of screens that belong to same set There are many screens that are correlated with eachother, and we don''t want correlated screens coz it's not good idea for the model image
Data Preprocessing & Feature Scaling
image image
Logistic Regression Model
Model Training
image image image we will use 'L1' penalty as we might have correlated features like screens & 'L1' penalises any such fields that are strongly correlated with response variable, this is because there will always be one screen that is just before the enrollment screen which imply that the correlation will be higher for that screen with enrollment screen ==> higher weight to that screen image image image image

Model Accuracy = sum of diagonal value of cm/sum of all values of cm(confusion matrix)
We also look for Precision to insure that model accuracy is inceased not because of some overfitting issues
Precision Score = True Positive / (True Positive + False Positive), meaning that out-of all predicted positives what percentage are Actual positives
Recall Score = True Positives / (True Positives + False Negatives, meaning that out-of all Actual Positives What Percentage are predicted to be positives
We will also calculate f1-score as it creates a balance between Precision & Recall coz it is weighted average of Precision & Recall thereby it considers both False Positives & Flase Negative Intuitively f1-score is not easy to understand as accuracy but it is much better metric in case of class imbalanced data as in our case
F1-Score = Precision*Recall / (Precision+Recall) image Sensitivity or TPR = TP/(TP+FN)
Specificity = TN/(TN+FP), (1-Specificity)=FPR image image
Here Area under ROC curve covers 85% which implies that the 85% of time model distinguish the 2 classes correctly
Predictions image image image image

From both the plots we can conclude that both Actual & Predicted values follows same class distribution
Feature Importance image image image image
Conclusion & Final Results
tenor

Positively Affecting features to enrollment: Other_sceens, VerifyPhone, CMCount, VerifyMobile, VerifyDateOfBirth, Rewards, EditProfile, etc, without any doubt all above features are situated to moving towards the enrollment screens.

Negatively Affecting features to enrollment: LoanCount, VerifyCountry, Alerts, age, numscreens, Login, ResendToken, etc, if we see all these features are irritating & no user want to do this. image image


