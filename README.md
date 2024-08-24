# ITD214_project

---
layout: post
author: Carlin Chow
title: "Applied Data Science Project Documentation"
categories: ITD214
---
## Project Background
Welcome to my ITD214 Github page! In this space, I would be sharing more about my project titled "British Airways: Improving Customer Experience".

Specifically, my team and I have selected the following dataset from Kaggle which contains customer reviews of British Airways scrapped from airlinequality from the period 2015 to 2023. There are 19 columns in this dataset (refer to the dataset using this link: https://www.kaggle.com/datasets/chaudharyanshul/airline-reviews



Here are the four objectives that we focused on:
1. To reduce response time by 10% by identifying common complaints through clustering for automation of replies (Yan)
   
**2. To analyse review topics for the four different seat types for a more targeted marketing approach, improving business by 10% (Carlin (myself))**
3. To identify areas of customer satisfaction for marketing purposes, to improve business by 10% (Bridget)
4. To reduce negative review sentiments by 10% to improve customer satisfaction and demand (Vivienne)

For my business objective (#3), I aim to make use of Topic Modelling and Sentiment Analysis to analyse common topics of interest for the four different seat types offered on flights by British airways, so that areas of improvement can be addressed / areas done well can be continued. Thereafter, I will also use the trigrams column that has been generated to gather further insights into these topics of concern. 

## Work Accomplished
Overall, the steps below have generated insights for bettering the top concerns of passengers who had travelled with British Airways. Specifically, frequent topics from the review ("CleanText") body was extracted using LDA, and picked up to sieve out top trigrams for better understanding about reviews on these aspects. 

### Data Preparation
  First, the relevant libraries were downloaded for use.

  ![1 Importing relevant lib](https://github.com/user-attachments/assets/3dd12992-07ba-4ab2-a5e2-e249296d6f27)

  The dataset looks like this:
  
  ![2 viewing dataset](https://github.com/user-attachments/assets/1940aa50-32eb-4ec2-b612-9671078c8911)

  Next, data preprocessing will be done on this dataset. Prior to my own preprocessing shown in the subsequent steps, our group has done some data preprocessing on the data. That includes the following:
1. Converting fields into appropriate data types
2. Removal of missing values
3. Conversion to lowercase
4. Removal of punctuation, numbers, stop words and domain stop words
5. N-char less than 3 characters
6. Lemmatization
7. Tokenisation
8. Lemmatization
9. POS Tagging and removal of specific parts of speech

As part of further preprocessing, only the main columns that were essential for the analysis were preserved. They consisted of the following - 'SeatType', 'Recommended', 'CleanText' (derived from text after cleaning earlier), 'Tokens', 'Sentiment', 'Bigrams', 'Trigrams' and the 'CleanText2' columns. The rest of irrelevant columns were filtered and dropped. 

![3 removing irrelevant columns and tokenizing ](https://github.com/user-attachments/assets/62c0d6cd-0e67-4eba-85a3-38080eaf8241)

Tokenization was also done for the TF-IDF process in the later steps.

Next, additional stop words were also removed since stop words which involved speaking about the individual classes were not helpful in the analysis. Hence, the additional stop words which were identified for removal were: 'economy', 'premium', 'class', 'business', 'first'. 

![4 removal of additional stop words](https://github.com/user-attachments/assets/6dc93077-36fa-4911-971e-0bcd90ed1d64)



To provide specific analysis for the four seat types (Economy Class, Premium Economy, Business Class and First Class), the dataset was split into four based on seat type. From there, subsequent steps would be done for each seat type separately.


![5 Splitting dataset by seat type](https://github.com/user-attachments/assets/491e02a4-849d-4bc3-8274-550a160bc487)


### Modelling
For this business objective, the model of choice was topic modelling. To enhance findings, I had also done an analysis of the bigrams and trigrams related to the topic words churned. 

Topic modelling was done in Jupyter Notebook using LDA. Perplexity scores and coherence scores were calculated to determine the best number of topics to input for the modelling process. Based on the scores, topic_num = 20 was chosen. 

To prepare dataset for topic modelling, TF-IDF by seat type was first done.

![6 Creating TFIDF by seat type](https://github.com/user-attachments/assets/87b32278-3b52-4b9f-a053-879bead5fed5)


**Topic Modelling Process**

Next, Topic Modelling was done through using LDA function. In this section, I display the LDA done for each of the seat types, and the results generated. 

For Economy Class - 

![7 LDA for economy class](https://github.com/user-attachments/assets/ec1ea8e1-521c-4a19-8176-8e658785f519)
![8 LDA for economy v2](https://github.com/user-attachments/assets/e2c8e282-7cb9-4010-b960-e8bb9d787bd2)


Perplexity and coherence values were obtained to determine the ideal number of topics (20). 

![9 Perplexity and coherence](https://github.com/user-attachments/assets/4204c2c4-9818-47d5-a2ea-8c387b999629)


For Premium Economy - 

![10 LDA for Premium Economy ](https://github.com/user-attachments/assets/c5662d81-b4de-45eb-b55a-471ffcae31c0)
![11 LDA for premium economy v2](https://github.com/user-attachments/assets/263414fc-3cf4-4ffe-b904-c0f1f1567b20)


For Business Class - 

![12 LDA for business](https://github.com/user-attachments/assets/4968fab9-9d13-45a6-b815-046699c6e4d2)
![13 LDA for business v2](https://github.com/user-attachments/assets/79992b0a-9653-4bcc-a01e-1d82ce826bec)


For First Class -

![14 LDA for first](https://github.com/user-attachments/assets/aff5aa6d-cd42-4976-8ca8-888ab96988de)
![15 LDA for first v2](https://github.com/user-attachments/assets/bdd3fc6d-2039-4c9f-a9e6-3d939671bec4)


### Evaluation
As topic words may not be sufficient to gain a deeper understanding of these aspects from customer reviews, reference was also done with the top trigrams. In this case, I had filtered trigrams based on the top topic words to identify top trigrams mentioned concerning these aspects. In gist, rather than only being able to identify 'service' as a top aspect of mention for customers - without any context of what about 'service' that customers were concerned about, we are now able to obtain greater knowledge from some trigrams generated. For example, multiple occurances of trigrams involving the word 'service' in the economy dataset could consist of 'bad customer service' or 'slow custoemr service'. This would help us identify that the service provided by British Airways was an aspect for improvement for its economy class. 

This was how frequent topic words of disucssion can help surface the frequent trigrams in the dataset to understand if they were concerns for improvement for British Airways to address, or areas of compliments for British Airways to keep up their good work in. 

![16 top trigrams](https://github.com/user-attachments/assets/6d563ee6-1360-4404-9a54-3c600f8fbae7)
![17 top trigrams v2](https://github.com/user-attachments/assets/440d402d-7154-44ce-88af-f35fb9a3ae47)
![18 top trigrams v3](https://github.com/user-attachments/assets/7d29223d-adca-4e68-801a-832d0ffcf05e)
![19 top trigrams v4](https://github.com/user-attachments/assets/92dcd786-3598-4c04-bb91-30593b338b3f)

## Recommendation and Analysis
Based on the top 20 topics (specific words) of interest, further evaluation was done through additional analysis of the bigrams and trigrams columns. 

**Some findings from the evaluation for the 4 seat types to improve British Airways service are as follows (examples):**

Economy Class: bad/poor customer service, exit row seat, take long time

Premium Economy: one hour delay, last time fly

Business Class: middle seat block

First Class: one hour delay


**Based on reviews, customers had following (examples of) positive remarks of some of the following topic words:**

Economy Class: leg room enough/plenty/good

Premium Economy: food pretty good, seat comfortable good, cabin crew efficient

Business Class: cabin crew friendly/good cabin crew, new seat comfortable, service food good/food drink good

First Class: lounge excellent service/good food drink

Overall, it could be gathered that British Airways had mainly done well in having a fleet of friendly and efficient cabin crew, as well as facilities that most customers were satisfied with. However, one major areas of improvement was noted, which is the delays of their flight. Additionally, economy class passengers also seemed to have complained about the exit row seat. 

## AI Ethics
For this project, one ethical consideration that would be most straightforward would be the annonymisation of customer reviews. During processing of the dataset, the names of customers were removed to ensure privacy. This ensures that confidentiality was maintained for the study,

Finally, transparency of project is made clear, as the ways of conducting the analysis were documented step by step and explained in detail. This would allow the audience to be clear of procedure and variables involved. This enables openness between data manager and the stakeholders, so that recommendations made subsequently are with basis. For the topic modelling portion, topic modelling was done on four separate datasets that was split from the original dataset, thus eliminating any biases or overgeneralisation of issues or areas performed well by the airline. 

## Source Codes and Datasets
Upload your model files and dataset into a GitHub repo and add the link here. 

GitHub repo - https://github.com/Carlincyj/ITD214_project
