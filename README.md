# Meetup Recommendation System

To develop a business case for [meetup.com](https://www.meetup.com/) platform by gaining insights through data analysis and build a recommendation engine using ALS Matrix factorization algorithm to provide improved meetup group recommendations for its users.

Here is the link to the dataset used for this project - https://www.kaggle.com/sirpunch/meetups-data-from-meetupcom

![alt text](https://github.com/snithin13/Meetup-Recommendation-System/blob/master/Images/Build-a-Recommendation-Engine-With-Collaborative-Filtering.png)

## Project Objectives:

1. Identify the “hot” categories to incentivise better quality meetups on this subject
2. Identify the most popular groups to partner with / promote
3. Improve meetup experience for users and companies - by providing suggestions based on customer preferences and by connecting them to popular groups and their target market

## Dataset:
9 csv files comprising of:
* 10.5 Million member data across 3 major cities - New York, San Francisco, Chicago
* 2600 topics, 2500 topics
* 78,000 venues, 5800 events

## Tools and Technologies:
* Tableau
* SQL
* PySpark on Databricks

## Algorithms:
* Matrix Factorization using ALS
* KNN

## Analysis:

**1. Top growing categories (by # of groups)**

![alt text](https://github.com/snithin13/Meetup-Recommendation-System/blob/master/Images/cat_trend.png)

* Inference: Career/Business, Tech, and Socialization are the three most popular and fast growing categories based on the 3 cities data.

* Suggestion: Incentivize growth of better quality groups in these categories by targeting user bases like interested University students or people working in the relevant industry.

**2. Popular groups in New York and in San Francisco (by # of memebers)**

![alt text](https://github.com/snithin13/Meetup-Recommendation-System/blob/master/Images/NK_group_rank.png)

![alt text](https://github.com/snithin13/Meetup-Recommendation-System/blob/master/Images/SF_group_rank.png)

* Suggestion: Now that we have identified the popular groups in New York and San Francisco from the above analysis, we need to attract top relevant company sponsorship into popular groups in exchange for better talent hunting opportunities and crowd connect. This can be monetized by meetup.com as a percentage of the sponsorship from the group.

##  Recommendation System:

**Approach:**

1. Selecting required columns from members, groups, and categories tables onto a spark dataframe.
2. Join all the required columns selected from different tables and split it based on city and finally convert back to pandas dataframe.
3. Now there are 2 types of recommendations:

* For Existing Users

i) Created category codes for members and groups.

ii) Created  2 separate sparse matrix using these category codes with binary interaction representation where 1 is item x user and the other user x item.

iii) Trained 3 models, one for each city using matrix factorization with ALS optimizer. Below hyperparameters were used:
factors = 20, regularization = .01, iterations = 20

iv) Calls the recommend function after checking the city of that the user inputed and display the top 10 recommendations.The results are shown below:

Existing Groups
![alt text](https://github.com/snithin13/Meetup-Recommendation-System/blob/master/Images/recomm%20grps.png)

Recommended Groups
![alt text](https://github.com/snithin13/Meetup-Recommendation-System/blob/master/Images/recomm%20grps.png)

* For New Users:

For a new user, it can be done in 2 ways -

i) Recommend 10 groups based on the top 3 category choices the user has selected at the time of registration, where the top 5 groups are the 5 groups from category 1 with the most members, next 3 are top 3 groups from category 2 with the most members and the last 2 groups are the top 2 groups from category 3 with the most members in that category.

ii) Use KNN model to recommend similar categories to the user from the ones that he already has selected at the time of registration.

## Code:
https://github.com/snithin13/Meetup-Recommendation-System/blob/master/Recommendation%20Engine%20for%20Meetup.ipynb
