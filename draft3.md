🗣️ Slide 1 — Title
“Hello everyone, I’m Mohammed Yahya. Welcome to my UIC 412 machine-learning project: ‘Document Classification of Research Abstracts.’
Today I’ll show you a small but powerful system that auto-tags scientific papers into six research fields. Why does this matter? Because arXiv alone posts over sixteen-thousand papers every day. No human can read that fire-hose, but a well-trained model can skim titles and abstracts in milliseconds and tell us where each paper belongs. Over the next ten minutes I’ll walk through the problem, the data, the modelling choices, the results, and the lessons I learned along the way.”

🗣️ Slide 2 — The Problem
“Here’s the core pain-point: manual tagging by librarians or junior researchers takes about thirty-five seconds per paper. Multiply that by sixteen-thousand and you burn more than 150 hours every day on clerical work. My goal is to cut that to zero. I focus on six broad labels—Computer Science, Physics, Mathematics, Statistics, Quantitative Biology, and Quantitative Finance. The challenge is multi-label: one paper can span two or three areas, and some labels appear only a handful of times. A good solution must be accurate, fast, and fair to those minority classes.”

🗣️ Slide 3 — Dataset at a Glance
“I collected 29 961 records. The training file holds twenty-thousand nine-hundred seventy-two labeled examples; a hidden test file holds eight-thousand nine-hundred eighty-nine. Each record has a title and an abstract—no full text—to keep computation light. I then carved out ten percent of the training data—about two-thousand papers—for validation. The class distribution is lopsided: Physics dominates, while Quant Bio and Quant Fin each sit below one percent. That imbalance will shape both modelling and evaluation choices later.”

🗣️ Slide 4 — Data Preparation Pipeline
“Text projects live or die on preprocessing, so I built a four-step pipeline.
Step one: clean—strip punctuation, digits, rogue LaTeX, and lowercase everything.
Step two: tokenize and lemmatize with spaCy and NLTK so ‘learning,’ ‘learned,’ and ‘learns’ become a single root.
Step three: convert text to numbers using TF-IDF on one- and two-gram tokens; that yields a 64-thousand-dimensional sparse vector—perfect for linear models.
Step four: tell the classifier to use balanced class weights to stop it from ignoring rare labels. Simple, reproducible, and fast.”

🗣️ Slide 5 — Model Showdown
“I staged a three-model shoot-out.
Baseline: Multinomial Naïve Bayes—great for speed, not so great for nuance.
Champion: a Linear Support-Vector Machine wrapped in a one-vs-rest multi-label strategy. SVMs thrive in high-dimensional sparse space. I grid-searched the penalty parameter C and found 0.5 with balanced weights worked best.
Wildcard: Word2Vec embeddings averaged into a Random Forest—fun experiment but recall lagged. In validation, Naïve Bayes hit 61 % exact-match, the SVM hit 66 %, and the Word2Vec model trailed at 59 %. So the Linear SVM is our workhorse going forward.”

🗣️ Slide 6 — Evaluation Metrics
“Multi-label tasks need more than one score.
First is Exact-Match Accuracy—all predicted labels must be correct, no partial credit.
Second, Micro-averaged Precision, Recall, and F1—treats every label instance equally, so common and rare labels mix.
Third, Macro-averaged F1—gives each label equal weight and therefore highlights minority pain points.
Finally, I inspect a confusion matrix to see where the model mixes topics—Mathematics and Physics overlap the most. Using these four views keeps me honest about both headline performance and edge cases.”

🗣️ Slide 7 — Results Snapshot
“On the validation set, the Linear SVM posts an exact-match accuracy of 66.1 percent and a micro-F1 of 0.83.
Label-by-label F1 scores are solid: Computer Science 0.85, Physics 0.88, Mathematics 0.84, Statistics 0.78.
Even with only a few dozen samples, Quant Finance hits 0.77 thanks to balanced weights. Quant Biology remains the weak link at 0.46—proof that extreme imbalance and shared vocabulary still matter. Overall, the model tags two-thirds of papers perfectly and gets most individual labels right four times out of five—already a huge boost over manual tagging.”

🗣️ Slide 8 — Lessons Learned
“Four lessons.
First: In sparse text, simple linear models beat fancier trees; TF-IDF plus SVM is a killer combo.
Second: Class imbalance distorts macro metrics; balanced weights help but oversampling or focal loss could push further.
Third: Cleaning counts—lemmatization alone gained three F1 points.
Fourth: Word2Vec needed a bigger corpus; semantics help, but only when you feed them enough data. In short: clean aggressively, favor linear, and never ignore your label distribution.”

🗣️ Slide 9 — Roadmap
“Where next? Four concrete steps.
One: fine-tune SciBERT embeddings—pre-trained on scientific text, perfect for our domain.
Two: use classifier chains to model label correlations; Math and Physics often co-tag.
Three: wrap the model in a FastAPI microservice so librarians can auto-tag incoming submissions in real-time.
Four: integrate that service into the campus library search portal so students get instant, accurate filters the day a paper lands.”

🗣️ Slide 10 — Call to Action
“That wraps up my overview. Scan the QR code to try the model live—paste any abstract and watch it predict. I’d love your feedback, especially on boosting those rare categories. Thank you for watching, and I’m happy to take your questions.”

Rehearsal tip: read each block once with a timer; most will clock between 50 and 65 seconds. Adjust pacing or trim adjectives to hit your preferred total. Good luck—your narration will now sync cleanly with each slide.









