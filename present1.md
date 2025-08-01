# Slide 1: Introduction
**Presenter Notes:**

"Hello everyone, my name is Mohammed Yahya, and today I'll be presenting my final project for CS 412, titled 'Document Classification: Predicting Research Topics from Abstracts.' In this project, I explored how machine learning can be used to automatically categorize a vast amount of scientific literature."

# Slide 2: Agenda

"Here's a quick overview of what I'll be covering today. I'll start by defining the problem, then walk through the dataset and the technical approach I took. I'll briefly introduce the two models I compared, present the results, and finally, I'll share my key lessons learned from this project."




# Slide 3: The Problem: An Ocean of Research

"The problem this project tackles is one of information overload. We're living in an age where scientific research is expanding at an incredible rate... This makes it nearly impossible for researchers to keep up. 
This project addresses this problem by asking: Can we teach a machine to read an abstract and assign it to the correct research field? The goal is to build a system that can automate this process, which has huge implications for how we discover and interact with scientific knowledge."

# Slide 4: Dataset
The project starts with a real-world dataset from the arXiv repository. The core challenge is a multi-label classification task: training a model to assign each paper to one or more of six research fields based only on its title and abstract.

# Slide 5: The Approach: From Text to Topics


"My approach followed a standard machine learning pipeline. It starts with the raw data... The most critical step is feature engineering. You can't feed raw text to a model, so I used a technique called TF-IDF which stands for Term Frequency-Inverse Document Frequency. This converts each abstract into a numerical vector that represents its unique vocabulary. Finally, because a paper can belong to multiple fields, I used a MultiOutputClassifier to train and compare two different models."

# Slide 6: The Contenders: Two Distinct Approaches


"To find the best solution, I decided to compare two different types of models. The first is a Linear Support Vector Classifier, or LinearSVC. This model works by finding the best possible boundary to separate the data points... On the other hand, I also used a Multinomial Naive Bayes classifier. This model takes a probabilistic approach... By comparing these two distinct methods, I aimed to see which strategy would be more effective for this specific text classification problem."

# Slide 7: Measures of Performance
"To evaluate the models, I used a standard set of classification metrics, each giving a different perspective on performance:"

*   **Accuracy:** This tells us the percentage of predictions where the model got the *entire* set of labels exactly right.
*   **Precision:** For a given topic, this measures how many of the papers we labeled with that topic were actually correct.
*   **Recall:** This measures how many of the papers that *truly* belong to a topic were correctly identified by our model.
*   **F1-Score:** This is the harmonic mean of precision and recall, providing a single score that balances both concerns.
*   **Averages (Micro, Macro, Weighted):** Since this is a multi-label problem, I calculated different averages of these scores to get a robust overall assessment.




# Slide 8: The Results: A Clear Winner Emerges


"After training both models and evaluating them on the unseen test data, the results were conclusive. As you can see from the chart, the LinearSVC model achieved an overall accuracy of 66.1%, which is a very strong result for a multi-label problem of this nature. The Naive Bayes model was respectable but fell short at 61.3%. Digging deeper into the winning model's performance, it was extremely effective at identifying papers in the larger categories like Physics and Computer Science, achieving F1-scores of 88% and 85% respectively."

# Slide 9: Lessons Learned & Future Work


"Through this project, I learned several important lessons. First, feature engineering is absolutely critical... Second, the choice of model makes a huge difference... Finally, the challenge of class imbalance was very apparent... If I were to continue this project, my immediate next steps would be to address this imbalance and to explore more advanced deep learning models. In conclusion, this project successfully demonstrated that machine learning can be a powerful tool for navigating the vast world of scientific research."