## Support vector machine (SVM)

`Supprt vectors` are a subset of training data that are criticla in determining the hyperplane that classify the data. The hyperplane is called `margine` in SVM, and SVM is trained to find the `max margine` between 2 different sets of data such that the wdith between the 2 sets of data is widest. 

To find the max margin, it's a `contrained optimization problem`. We need to optimize the margin while keep no data in the margin. The technique used to solve this problem is `Lagrange Multiplier techniques`. 

More pratically, SVM can be used for semi-supervised learning, where a relatively small set of labelled data is used for model training, the model trained can then be used to classify more unlabelled input data, for example, which in turn can be used as input for a supervised learning model for more optimized learning.

### On SVM
* http://web.mit.edu/6.034/wwwbob/svm-notes-long-08.pdf
* https://www.youtube.com/watch?v=N1vOgolbjSc

### On Semi-supervised learning
* https://bdtechtalks.com/2021/01/04/semi-supervised-machine-learning/

### On Coding
* https://www.kaggle.com/jiayaoli/snorkel-svm
