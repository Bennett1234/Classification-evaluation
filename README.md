# Classification-evaluation
## The 5 Classification Evaluation metrics every Data Scientist must know
What do we want to optimize for? Most of the businesses fail to answer this simple question.
Every business problem is a little different, and it should be optimized differently.
We all have created classification models. A lot of time we try to increase evaluate our models on accuracy. But do we really want accuracy as a metric of our model performance?
What if we are predicting the number of asteroids that will hit the earth.
Just say zero all the time. And you will be 99% accurate. My model can be reasonably accurate, but not at all valuable. What should we do in such cases?

Designing a Data Science project is much more important than the modeling itself.

### 1. Accuracy, Precision, and Recall:
![](<confusion matrix.png>)

#### A. Accuracy
Accuracy is the quintessential classification metric. It is pretty easy to understand. And easily suited for binary as well as a multiclass classification problem.

*Accuracy = (TP+TN)/(TP+FP+FN+TN)*  
Accuracy is the proportion of true results among the total number of cases examined.

#### When to use?
Accuracy is a valid choice of evaluation for classification problems which are well balanced and not skewed or No class imbalance.  
#### Caveats
Let us say that our target class is very sparse. Do we want accuracy as a metric of our model performance? What if we are predicting if an asteroid will hit the earth? Just say No all the time. And you will be 99% accurate. My model can be reasonably accurate, but not at all valuable.  
#### B. Precision
Let’s start with precision, which answers the following question: what proportion of predicted Positives is truly Positive?
Precision = (TP)/(TP+FP)
In the asteroid prediction problem, we never predicted a true positive.
And thus precision=0
#### When to use?
Precision is a valid choice of evaluation metric when we want to be very sure of our prediction. For example: If we are building a system to predict if we should decrease the credit limit on a particular account, we want to be very sure about our prediction or it may result in customer dissatisfaction.
#### Caveats
Being very precise means our model will leave a lot of credit defaulters untouched and hence lose money.
#### C. Recall
Another very useful measure is recall, which answers a different question: what proportion of actual Positives is correctly classified?
Recall = (TP)/(TP+FN)
In the asteroid prediction problem, we never predicted a true positive.
And thus recall is also equal to 0.
#### When to use?
Recall is a valid choice of evaluation metric when we want to capture as many positives as possible. For example: If we are building a system to predict if a person has cancer or not, we want to capture the disease even if we are not very sure.
#### Caveats
Recall is 1 if we predict 1 for all examples.
And thus comes the idea of utilizing tradeoff of precision vs. recall — F1 Score. 

### 2. F1 Score:
This is my favorite evaluation metric and I tend to use this a lot in my classification projects.
The F1 score is a number between 0 and 1 and is the harmonic mean of precision and recall.
![](<f1score.png>)
Let us start with a binary prediction problem. We are predicting if an asteroid will hit the earth or not.
So if we say “No” for the whole training set. Our precision here is 0. What is the recall of our positive class? It is zero. What is the accuracy? It is more than 99%.
And hence the F1 score is also 0. And thus we get to know that the classifier that has an accuracy of 99% is basically worthless for our case. And hence it solves our problem.
#### When to use? 
We want to have a model with both good precision and recall. Simply stated the F1 score sort of maintains a balance between the precision and recall for your classifier. If your precision is low, the F1 is low and if the recall is low again your F1 score is low.
 
#### How to Use? 
```
from sklearn.metrics import f1_score
y_true = [0, 1, 1, 0, 1, 1]
y_pred = [0, 0, 1, 0, 0, 1]
f1_score(y_true, y_pred)  
```
 
```
# y_pred is an array of predictions
def bestThresshold(y_true,y_pred):
    best_thresh = None
    best_score = 0
    for thresh in np.arange(0.1, 0.501, 0.01):
        score = f1_score(y_true, np.array(y_pred)>thresh)
        if score > best_score:
            best_thresh = thresh
            best_score = score
            
    return best_score , best_thresh
```
#### Caveats
The main problem with the F1 score is that it gives equal weight to precision and recall. We might sometimes need to include domain knowledge in our evaluation where we want to have more recall or more precision. To solve this, we can do this by creating a weighted F1 metric as below where beta manages the tradeoff between precision and recall.
![](<image(1).png>)
