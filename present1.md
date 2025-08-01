# Slide 1: Introduction
**Presenter Notes:**

"Hello everyone, my name is Mohammed Yahya, and today I'll be presenting my final project for CS 412, titled 'Document Classification: Predicting Research Topics from Abstracts.' In this project, I explored how machine learning can be used to automatically categorize a vast amount of scientific literature."

# Slide 2: Agenda

Presentation Outline
Problem Definition: The challenge of information overload in scientific research.
Dataset & Approach: Exploring the arXiv dataset and the ML pipeline used.
Models Compared: A look at the two classification strategies.
Results & Evaluation: Announcing the winning model and its performance.
Lessons Learned: Key takeaways and future work.



**Presenter Notes:**

"Here's a quick overview of what I'll be covering today. I'll start by defining the problem, then walk through the dataset and the technical approach I took. I'll briefly introduce the two models I compared, present the results, and finally, I'll share my key lessons learned from this project."


# Slide 3: The Problem: An Ocean of Research
(Visual: An icon or graphic representing a massive stack of papers or a data cloud)



The Challenge
Every day, thousands of new scientific papers are published on platforms like arXiv.

Manually sorting this information is inefficient and time-consuming.

The Question
How can we automatically and accurately classify a research paper into its correct field (e.g., Computer Science, Physics) using only its title and abstract?

Why It Matters
Powers Discovery: Enables smarter search, personalized recommendations, and academic trend analysis.

Project Goal: To build and evaluate machine learning models for this multi-label text classification task.



**Presenter Notes:**

"The problem this project tackles is one of information overload. We're living in an age where scientific research is expanding at an incredible rate... This makes it nearly impossible for researchers to keep up. 
This project addresses this problem by asking: Can we teach a machine to read an abstract and assign it to the correct research field? The goal is to build a system that can automate this process, which has huge implications for how we discover and interact with scientific knowledge."

# Slide 4: The Approach: From Text to Topics
(Visual: A simple, clean flowchart graphic showing the three main steps)



A Three-Step Machine Learning Pipeline
1. Data Cleaning & Preparation

Input: 20,972 unique paper abstracts from the arXiv dataset.

Action: Combined TITLE and ABSTRACT. Cleaned the text by removing punctuation and numbers, and converting to lowercase.

2. Feature Engineering with TF-IDF

Challenge: How do you turn words into numbers?

Solution: Used TF-IDF (Term Frequency-Inverse Document Frequency). This technique identifies the most important and distinctive words for a given topic, not just the most frequent ones.

3. Model Training

Task: Multi-Label Classification (a paper can have multiple topics).

Method: Used MultiOutputClassifier to train a separate classifier for each of the 6 topics.



**Presenter Notes:**

"My approach followed a standard machine learning pipeline. It starts with the raw data... The most critical step is feature engineering. You can't feed raw text to a model, so I used a technique called TF-IDF... This converts each abstract into a numerical vector that represents its unique vocabulary. Finally, because a paper can belong to multiple fields, I used a MultiOutputClassifier to train and compare two different models."

# Slide 5: The Contenders: Two Distinct Approaches
(Visual: Two columns, each with a simple icon and a brief description of the model)



Linear Support Vector Classifier (LinearSVC)

Multinomial Naive Bayes

A Geometric Approach

A Probabilistic Approach

Finds the optimal line or hyperplane to separate the different categories of papers.

Calculates the probability that a paper belongs to a certain category given the words in its abstract.

Strength: Known to be highly effective and robust for high-dimensional text data.

Strength: Very fast, efficient, and provides a great performance baseline for text classification tasks.



**Presenter Notes:**

"To find the best solution, I decided to compare two different types of models. The first is a Linear Support Vector Classifier, or LinearSVC. This model works by finding the best possible boundary to separate the data points... On the other hand, I also used a Multinomial Naive Bayes classifier. This model takes a probabilistic approach... By comparing these two distinct methods, I aimed to see which strategy would be more effective for this specific text classification problem."

# Slide 6: The Results: A Clear Winner Emerges
(Visual: A large, clear bar chart comparing the accuracy scores. Highlight the winning model.)



Performance on the Test Set
Key Performance Metrics (LinearSVC)
Overall Accuracy: 66.1%

Best Categories (F1-Score):

Physics: 88%

Computer Science: 85%

Observation: The LinearSVC model significantly outperformed Naive Bayes, demonstrating its robustness for this task.



**Presenter Notes:**

"After training both models and evaluating them on the unseen test data, the results were conclusive. As you can see from the chart, the LinearSVC model achieved an overall accuracy of 66.1%, which is a very strong result for a multi-label problem of this nature. The Naive Bayes model was respectable but fell short at 61.3%. Digging deeper into the winning model's performance, it was extremely effective at identifying papers in the larger categories like Physics and Computer Science, achieving F1-scores of 88% and 85% respectively."

# Slide 7: Lessons Learned & Future Work
(Visual: Simple icons for each of the three key takeaways)



1. Feature Engineering is King
The success of the project was highly dependent on the TF-IDF vectorization. The quality of the numerical features directly impacts model performance.

2. Model Selection Matters
For complex, high-dimensional text data, the LinearSVC was far more effective than the simpler, probabilistic Naive Bayes model.

3. Class Imbalance is a Key Challenge
The models struggled with underrepresented categories like Quantitative Biology. This is a classic machine learning challenge.

Future Work
Address Class Imbalance: Use techniques like SMOTE (oversampling) to create more training data for minority classes.

Explore Deep Learning: Test a simple neural network or a more advanced model like BERT to see if it can capture deeper semantic meaning and improve accuracy further.



**Presenter Notes:**

"Through this project, I learned several important lessons. First, feature engineering is absolutely critical... Second, the choice of model makes a huge difference... Finally, the challenge of class imbalance was very apparent... If I were to continue this project, my immediate next steps would be to address this imbalance and to explore more advanced deep learning models. In conclusion, this project successfully demonstrated that machine learning can be a powerful tool for navigating the vast world of scientific research."