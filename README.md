# ML Lab 401: Support Vector Machines
## Overview
In this assignment, you will implement and analyze a Support Vector Machine (SVM).

In this repository, we have included a dataset, `fashion-mnist_train.csv`, containing a sample of the Fashion MNIST benchmark. This dataset consists of 28x28 grayscale images of 10 categories of clothing items (T-shirt/top, Trouser, Pullover, Dress, Coat, Sandal, Shirt, Sneaker, Bag, Ankle boot). In this lab, you will develop predictive models for this data set and write a report on your findings. You will have less guidance in this lab, as you have more experience in the programming environment and we want you to have more ownership of your work. If you have questions, please reach out early and often. 

**Please read through all of the files associated with this Lab Assignment before you start the assignment.**

## Problem Statement
In this lab, you have 5 tasks, which are discussed in greater detail within the notebook `assignment4.ipynb`. Broadly, the tasks are as follows:

1. Train a SVM to perform binary classification with non-linear kernels.
2. Implement a predictive model.
3. Compare the performance of two voting schemes (one-vs-rest and one-vs-one).
4. Discuss your strategy for hyperparameter tuning.
5. Generate multiclass confusion matrices for your model.

## Goals of This Lab
We are asking you to complete this assignment because we want you to:

1. Gain experience constructing and analyzing SVMs.
2. Continue to practice implementing machine learning algorithms from first principles (we'll need this in hardware).
3. Practice writing succinct reports with clear figures on a complex topic.

## Expectations
You are not allowed to import an SVM from, for instance, `scikit-learn` unless specified.

You may, however, use a library (such as `scipy.optimize.minimize` or `cvxopt.solvers.qp`) for the optimization process. The code to install the `cvxopt` library is included in the first code cell, if needed. 

All lab submissions are individual and every item you submit should be a reflection of your own work. You should have ownership over the entirety of any lab you submit in this course. While your work is your own, we understand that it can be helpful in learning machine learning to collaborate with your peers, which can range from high-level discussion of a problem to debugging. Having others look at our code encourages us to write code with readability in mind. In practice, we will never work in a silo, and being able to discuss these topics with others well is a valuable skill. When you collaborate with another student, please cite them appropriately and be respectful of sharing too much. The Academic Honor Principle applies.

We respectfully ask that in the interest in furthering your own understanding of the material, that you refrain from using generative AI to code for you. Your work should be your own and you should feel comfortable justifying each design decision you make. 

Please cite any outside sources you reference.

>[!Important]
> Finally, you will get the most out of this assignment if you give yourself time to be playful and curious in your experimentation. 

## Evaluation
You will be evaluated on the quality of your code and report. Your report must provide summaries of each method's performance and some additional details of your implementation. Compare the relative strengths and weaknesses of the methods based on both the experimental results and your understanding of the algorithms.

### What to Submit
Please submit the following:

1. Your completed notebook: `assignment4.ipynb`, where the output of each cell is clearly displayed.

2. A brief write-up that answers the 5 questions posed in this lab and justifies your model. Ensure that any figures you create are accessible and easy to understand.




##WRITEUP##

t1: i implemented a soft margin kernev svm by solving the dual optimization prolem with cvxopt.solers.qp

i built the ksoft margin svm wthat can use nonlinear kernel trained using the dual fromaultion with a qp solver. the main idea was to learn which training points matter most (supper vectors ) andsotre onlyt those so the model stays efficient at pred time. i also scaled the pixel inputs so that the kernel behaves consistently

t2:
after training, i predict by computing a score for each input based on the weighted influence of the support vectors plus a negative term, the predicted label comes from whether that score is positive or negative. for the bias, i comptue it suing the support vectrors that lie on the margin when possible and i fall back to all suppt vectors if needed
t3: 
since fashino MNIST has 10 classes, extended binary svm to multiclass in two ways, doing one v rest and 1v1,  which used the classifier for each pir of classes and used the majoity voting to decide the final label. 

How i chose c. i tuned the regularization paramater c using a validation split. i made a balanced subset of the training data so the QP training would run in a reasonable amount of time, then did a stratified train/validation split to keep class proportions stable. i tested a log spaced grid of c values and picked the one that gave me the best validation accuracy. after choosing the best c, i retratined the multicalss model on the full balanced subset and evaled it on the test set

finally in t5 ,i created a confusion meatri using the test label sand my final predictions. 