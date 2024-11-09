The **gradient vector** of multivariable function points in the direction of the steepest increase of its slope. Basically, it's the <span style="background:#9254de">generalization of the derivative of a function</span>, to the domain of multivariable functions. As such, it's a foundational term in calculus with many uses - especially for measuring the rate of change of a function, as well so ascending / descending its graph towards its (local) minima / Maxima.

In the case of Machine Learning, the most common use of it, is in the [[Gradient Descent Algorithm]]. More specifically, we use it to decide on how should we change the model parameters, such that we will descent down the cost/loss/objective function - towards its minima. 

The way we do that in practice, is that for each batch of training samples, we calculate the partial derivative of the loss function with respect to each of the parameters, and then we take a small step in the opposite direction to the gradient (since the gradient points towards the steepest increase, and we want to go down).

![](https://qph.cf2.quoracdn.net/main-qimg-40bff2152e149572f65fccd6d0a43629-lq)

The exact step we take, depends on the learning rate, and the optimization function we use to address the problem of "noise" - resulting from the fact that for practical reasons, we don't calculate the loss function for all the training data at once, but rather do it for a small batch at the time.

You might also stumble on some ML algorithms that use gradient ascent to find a Maxima point, rather than minimizing a cost function with gradient decent - especially in object segmentation, and some logistic regression methods - but these are the exception, and not the rule.