<h2><b>Multiclass Classification Using Logistic Regression</b></h2>

By default, logistic regression cannot be used for classification tasks that have more than two class labels, **so-called multi-class classification**.Instead, it requires modification to support multi-class classification problems.

One popular approach for adapting logistic regression to multi-class classification problems is to split the multi-class classification problem into **multiple binary classification problems** and fit a standard logistic regression model on each subproblem. 

Techniques of this type include **one vs all** method. For example, if we have four classes: cars, trucks, bikes, and boats. When we will work on the car, we will use the car as 1 and the rest of the classes as zeros. Again, when we will work on the truck, the element of the truck will be one, and the rest of the classes will be zeros.

Suppose a dataset $\{(\boldsymbol{x}^{(1)}, y^{(1)}), ..., (\boldsymbol{x}^{(m)}, y^{(m)})\}$
with $\boldsymbol{x}^{(i)}$ being a $d-$dimensional vector $\boldsymbol{x}^{(i)} = (x^{(i)}_1, ..., x^{(i)}_d)$ . 
Let , $y^{(i)}$ being the target variable for $\boldsymbol{x}^{(i)}$.

The training procedure of a softmax regression model has following steps :
![title](static/softmax_regression.jpg)

* * * 
### Step 0:
Initialize the weight matrix and bias values with zeros (or small random values).<br>

Shape of **weight matrix** = $(n_{classes}, n_{features})$, **bias matrix** = $(n_{classes},1)$<br>

* * *

### Step 1:
For each class $k$ compute a linear combination of the input features and the weight vector of class $k$.<br>

$\boldsymbol{scores} = \boldsymbol{X} \cdot \boldsymbol{W}^T + \boldsymbol{b}$

where $\boldsymbol{X}$ is a matrix of shape $(n_{samples}, n_{features})$ that holds all training examples, and $\boldsymbol{W}$ is a matrix of shape $(n_{classes}, n_{features})$ that holds the weight vector for each class.



* * * 
### Step 2:
 Apply the softmax activation function to transform the scores into probabilities. The probability that an input vector $\boldsymbol{x}^{(i)}$ belongs to class $k$ is given by : 

$$\hat{p}_k(\boldsymbol{x}^{(i)}) = \frac{\exp(score_{k}(\boldsymbol{x}^{(i)}))}{\sum_{j=1}^{K} \exp(score_{j}(\boldsymbol{x}^{(i)}))}$$

* * *
### Step 3 :
***Compute the cost and gradients.*** <br>
We want our model to predict a high probability for the target class and a low probability for the other classes. This can be achieved using the cross entropy loss function: 

$$J(\boldsymbol{W},b) = - \frac{1}{m} \sum_{i=1}^m \sum_{k=1}^{K} \Big[ y_k^{(i)} \log(\hat{p}_k^{(i)})\Big]$$

In this formula, the target labels are *one-hot encoded*. So $y_k^{(i)}$ is $1$ is the target class for $\boldsymbol{x}^{(i)}$ is k, otherwise $y_k^{(i)}$ is $0$. <br>


**Gradient Descent & Derivatives:** <br>
Compute the gradient of the cost function with respect to each weight vector and bias.
The general formula for class $k$ is given by:
$$
\nabla_{\boldsymbol{w}_{k}} J(\boldsymbol{W}, b)=\frac{1}{m} \sum_{i=1}^{m} \boldsymbol{x}^{(i)}\left[\hat{p}_{k}^{(i)}-y_{k}^{(i)}\right]
$$

For the biases, the inputs $\boldsymbol{x}^{(i)}$ will be given 1.



Expained [HERE](https://shorturl.at/hrDJ9).
* * *

### Step 4 :
Update the weights and biases for each class $k$:

$\boldsymbol{w}_k = \boldsymbol{w}_k - \eta \, \nabla_{\boldsymbol{w}_k} J$  

$b_k = b_k - \eta \, \nabla_{b_k} J$

where $\eta$ is the learning rate.

**So the weight updation becomes W_new = W_old - Learning_rate * Gradient**
**Therefore, W_new = W_old - Learning_rate * Input_features * (Predicted - Target)**
* * *

