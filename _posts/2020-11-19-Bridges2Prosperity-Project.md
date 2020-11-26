---
layout: post
title: Let's Build Bridges to Create Opportunities
subtitle: 
gh-repo: "https://github.com/JonRivera/bridges-to-prosperity-ds-d"
gh-badge: [star, fork, follow]
tags: [machine learning, database]
comments: true
---

A community benefiting from the construction of a bridge; Credit: https://bridgestoprosperity.mbakerintl.com/Introduction
I worked with a cross-functional team and contributed to Bridges to Prosperity's mission; which is to " work with isolated communities to create access to essential health care, education and economic opportunities by building footbridges over impassable rivers." We contributed to the mission by constructing a web application that helps Bridges to Prosperity(B2P) have a reliable means of accessing their own data. On top of this, we created several machine learning models that can serve as tools by B2P engineers to save time and energy in deciding which bridges to prioritize when doing a technical assessment of whether or not to build a bridge.

Part 1: Making the Data Pretty and Accessible
The product road map for the data science team was broken into exploring, cleaning, and processing of the data. This was followed by the construction of the database and the creation of the machine learning model.
Using the 2018 Bridges to Prosperity (B2P) data set, collected from various villages in Rwanda, we cleaned the data using various Regex techniques. The challenges my team and I were assigned to solve were to parse out the 2013/2014 needs assessment data into current fields (2018 B2P data set) and be able to predict which sites from the field assessments will likely be technically rejected/accepted by a technical engineering review.
The main concerns the data science team encounter were us not having enough relevant data points. This hindered us from creating a strong enough model. In other words, we dealt with a highly imbalanced data set. Needless to say, we compensated by using SMOTE techniques, which helped us create synthetic data based on existing labels based on the existing engineer's assessments.

The product that I help create was a fast API application hosted on AWS (Amazon Web Services) that pulls and returns data from a Postgres SQL database.
I constructed endpoints on a fast API framework to pull all data we had cleaned. This was done by constructing Get and Post requests for the web team.
Several steps went into constructing the database with PostgreSQL, and this database was hosted on AWS. After creating the database, we uploaded the Bridges to Prosperity 2018 data set to the database.
Fast API - Get Request Endpoint to pull data from Postgres SQL Data BaseThe remaining part of the project was to construct a model that helps reduce the time and money wasted by the engineering review team; this is done by guiding them to choose bridges with higher chances of being approved by the engineer. This was done by using a random forest and semi-supervised model.

Part 2: Problem and Challenges - Powering Through
The main features that the data science team worked during our model building were:
bridge_classification
bridge_opportunity_bridge_type
bridge_opportunity_span_m,
days_per_year_river_is_flooded
flag_for_rejection
height_differential_between_banks

The main problem was to clean the data. My teammates and I broke the task of cleaning the data into two parts. The main data came from the 2018 field assessment data and the second part was to parse and clean that from 2013/2014 found in a comments section of the 2018 data set.
Comments Column in the 2018 data set, which ultimately parsed out and clean, representing the 2013/2014 data set.A technical challenge encountered by all the ds members dealing with the high imbalanced nature of the data. We ended created three classes for the engineering review column: positive class, negative class, and an unknown class. The data set consisted of about 1383 unknowns, 65 positives, and 24 negatives. These labels were encoded to numerical representations: 1 represents a positive, 0 represents negatives, and -1 represents unlabeled data. So to tackle this problem we used a semi-supervised model to predict likely labels for the unknowns; however, at the moment we aren't able to validate the precision/recall of the model because of the number of unlabeled points we had to begin with; we can't compare how right we are per se using the semi-supervised model, but as B2P gathers more data they could validate the model and check performance with time.

With that being said, in the short term, we can take advantage of using a random forest model in conjunction with smote and create a model with limited data that can be used to also predict whether a bridge is likely to be rejected or accepted by an engineer. We can at least evaluate performance such as precision/recall and accuracy.

The random forest works well on the existing data set as shown in the confusion matrix below, but keeping in mind that the model was trained on 89 data points, which means that the model is likely overfitting and we would need to gather more data to make the model more generalizable.
0 labels represent negatives and 1 represents positive; a negative represents a bridge likely to be rejected and a 1 represents. a bridge likely to be accepted by the engineer.Part 3: Wrapping things Up

Present
The current state of our product is we have a deployed website: This website pulls data from the Postgres SQL data based discussed earlier.
The main page of the website displays clusters of bridges built. The user can zoom in and see specific data.Furthermore, the web development team constructed a dashboard based on the 2018 clean data as well.

Check out this presentation where both the data science team and web developers come together to discuss our findings and products we created for Bridges to Prosperity

Long-term
Future features could be engineered based on existing data. For example, future cohorts/developer could construct a feature based on longitude/latitude data and combine it with the number of days raining in a certain area; perhaps there are some environmental factors that could be highlighted, leading to creating a better model.

The lack of data points related to an engineer approving or rejecting a bridge site makes the model process difficult. Out of 1472 data points, we only have 89 data points where the engineer actually approved or rejected the initial field assessment. With that being said, perhaps future cohorts of data scientists/web developers can build on our work to construct better models.
Lessons Learned

Throughout this 1 month journey, working with a cross-functional team, I learn various lessons. My peers gave me feedback on working on making pauses when I discussed technical topics, as well as committing more frequently in GitHub. This feedback helped me grow as a data scientist. During this project, I also realize the importance of taking initiative and staying organized with one's work. My data science team and I consistently set up Trello cards and zoom meetings to discuss any discrepancies or inconsistencies we saw with one's code. If a person was using a model, and there were some assumptions being made that seemed wrong we had a technical discussion. My team's priority was to always put the stakeholder's interest first.

Career Enhancement
This project definitely enhanced my skills as a data scientist. I was able to try new regex techniques, and feel more confident in clean text-based data. Additionally, having worked with Elastic Bean Stalk and Postgres SQL, further, enhance my data engineering skillset. The construction of the machine learning model with a new technique called semi-supervised learning was really amazing and helped acquire a new tool to use on imbalanced data. Lastly, working with a highly diverse team I found myself consistently practicing communication with different personalities. During this process, I learned that proposing questions and pointing out inconsistencies is a good way of staying neutral and helping the team move forward. I constantly found myself asking questions to others to see how they reason. From there it was much easier to reach agreements so that ultimately we reach a solution that would lead to a great product for B2P.

LINKS
Website Application Here
Latest Fast Api Deployment Site Here
Github Notebook Here
Main Notebook used for model building Here
