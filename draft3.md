🎙️ Slide 1 – Title
“Hello, my name is Mohammed Yahya, and welcome to my UIC 412 Machine Learning project presentation, titled ‘Document Classification of Research Abstracts: Taming Information Overload in Science.’

Every day more than sixteen-thousand new papers appear on pre-print servers like arXiv. That flood makes it nearly impossible for researchers to keep track of what matters to them. My project shows how a lean machine-learning pipeline can read those papers faster than any human and tag them with the right scientific field in seconds.”

🎙️ Slide 2 – The Problem
“Let’s start with the problem.

Manual tagging takes about thirty-five seconds per paper. Multiply that by sixteen-thousand and you get over a hundred and fifty hours of work—every single day. That’s unsustainable. My objective is simple but powerful: automatically assign each paper to one or more of six broad research areas—Computer Science, Physics, Mathematics, Statistics, Quantitative Biology, and Quantitative Finance. If we succeed, literature reviews speed up, search engines get smarter, and human experts can focus on deeper reading instead of clerical work.”

🎙️ Slide 3 – Dataset at a Glance
“Here’s the data we’re working with.

I have twenty-thousand nine-hundred and seventy-two labeled records in the training set, and eight-thousand nine-hundred and eighty-nine unlabeled records held out for testing. Each record contains only a title and an abstract—no full text. That design choice keeps the model lightweight enough for real-time deployment.

From the training pool I carved out a ten-percent validation slice—about two-thousand samples—to measure performance as I iterate. One wrinkle is class imbalance: Physics dominates, while Quant Biology and Quant Finance together account for less than one percent of the data. That imbalance will surface again when we talk about evaluation.”

🎙️ Slide 4 – Data Preparation Pipeline
“Data preparation can make or break a text project, so here’s what I did.

First, I cleaned the text—stripped punctuation, digits, stray LaTeX commands, and forced everything to lowercase.

Second, I tokenised each sentence and lemmatised the words using spaCy and NLTK so that ‘learning,’ ‘learned,’ and ‘learns’ collapse into a single root form.

Third, I converted those tokens into a numeric representation with TF-IDF using one- and two-word-grams. That produced a sparse matrix with roughly sixty-four-thousand features—high dimensional but exactly what linear models love.

Finally, I told the classifier to use balanced class weights so rare labels wouldn’t be ignored.”

🎙️ Slide 5 – Model Showdown
“With features in hand, I staged a three-way model showdown.

The baseline was Multinomial Naïve Bayes. It’s lightning fast but assumes words are independent—an assumption that rarely holds.

My champion contender was a Linear Support-Vector Machine wrapped in a one-versus-rest multi-label strategy. SVMs thrive in high-dimensional sparse spaces, so this pairing was a natural fit. I grid-searched the penalty parameter ‘C’ and found that a value of zero-point-five with class-weight balancing delivered the best validation score.

For a wildcard, I trained Word2Vec embeddings and fed their averages into a Random Forest. The idea was to capture semantic meaning, but in practice it under-performed, especially on recall. So the Linear SVM emerged as the clear winner.”

🎙️ Slide 6 – How We Evaluate
“Measuring success in multi-label problems is a little tricky, so I use three complementary metrics.

First, exact-match accuracy: we only score a hit if the model predicts the entire label set for a paper perfectly.

Second, micro-averaged precision, recall, and F1. Micro treats every label occurrence equally, so it reflects overall token-level performance.

Third, macro-averaged F1, which gives equal weight to each class and therefore punishes us when we miss the rare ones. I also visualize a confusion matrix to see which topics collide most often—Math and Physics, for example, love to overlap.”

🎙️ Slide 7 – Results Snapshot
“Time for results—here’s the snapshot from the validation set.

The Linear SVM with TF-IDF hits an exact-match accuracy of sixty-six point one percent. On a micro level we achieve an F1 of zero-point-eight-three, meaning the model is very reliable at the token level.

Per-label F1 scores tell the fuller story: we’re in the mid-eighties for Computer Science, Physics, and Mathematics. Statistics lags slightly at seventy-eight. Quant Finance, despite having only a couple dozen samples, still reaches point-seven-seven thanks to the balanced weights. Quant Biology is our Achilles’ heel at point-four-six—evidence that extreme class imbalance and vocabulary overlap remain tough nuts to crack.”

🎙️ Slide 8 – Lessons Learned
“What did I learn along the way? Four big take-aways.

First, in sparse text data, simpler linear models often beat fancier deep or tree-based models. The combination of TF-IDF and a linear kernel is hard to top.

Second, class imbalance warps macro metrics and can hide performance cliffs. Balanced class weights help, but oversampling or focal loss could push us further.

Third, meticulous cleaning and lemmatisation gave me a three-point lift in F1—so never ignore preprocessing.

And fourth, Word2Vec offered valuable intuition about semantics, but without a much larger corpus it couldn’t outshine TF-IDF.”

🎙️ Slide 9 – Roadmap
“Where do we go from here? Four concrete next steps.

One: fine-tune SciBERT embeddings. SciBERT is pre-trained on scientific text and should capture domain jargon that TF-IDF misses.

Two: experiment with classifier chains to model label correlations—for instance, papers labeled Mathematics frequently also carry Physics.

Three: wrap the best model in a FastAPI microservice so librarians and researchers can auto-tag new submissions instantaneously.

And four: integrate that service into the campus library search portal, so students see accurate topic filters the day a paper lands in the repository.”

🎙️ Slide 10 – Call to Action
“That brings us to the end.

I invite you to scan the QR code on screen to try the model live in a Colab notebook—paste in any abstract and watch it predict. I’m eager to hear your ideas on boosting rare-label performance or integrating this tool into your own workflows.

Thank you for listening, and I look forward to your questions.”