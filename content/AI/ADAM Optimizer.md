Adaptive Moment Estimation is an algorithm for optimization technique for gradient descent. The method is really efficient when working with large problem involving a lot of data or parameters. It requires less memory and is efficient. Intuitively, it is a combination of the ‘gradient descent with momentum’ algorithm and the ‘RMSP’ algorithm.

## **How Adam works?**

Adam optimizer involves a combination of two gradient descent methodologies:

**Momentum:** 

This algorithm is used to accelerate the gradient descent algorithm by taking into consideration the ‘exponentially weighted average’ of the gradients. Using averages makes the algorithm converge towards the minima in a faster pace. 

wt+1=wt−αmtwt+1​=wt​−αmt​

where,

mt=βmt−1+(1−β)[δLδwt]mt​=βmt−1​+(1−β)[δwt​δL​]

mt = aggregate of gradients at time t [current] (initially, mt = 0) mt-1 = aggregate of gradients at time t-1 [previous] Wt = weights at time t Wt+1 = weights at time t+1 αt = learning rate at time t ∂L = derivative of Loss Function ∂Wt = derivative of weights at time t β = Moving average parameter (const, 0.9)

**Root Mean Square Propagation (RMSP):** 

Root mean square prop or RMSprop is an adaptive learning algorithm that tries to improve AdaGrad. Instead of taking the cumulative sum of squared gradients like in AdaGrad, it takes the ‘exponential moving average’.

wt+1=wt−αt(vt+ε)1/2∗[δLδwt]wt+1​=wt​−(vt​+ε)1/2αt​​∗[δwt​δL​]

where, 

vt=βvt−1+(1−β)∗[δLδwt]2vt​=βvt−1​+(1−β)∗[δwt​δL​]2

Wt = weights at time t Wt+1 = weights at time t+1 αt = learning rate at time t ∂L = derivative of Loss Function ∂Wt = derivative of weights at time t Vt = sum of square of past gradients. [i.e sum(∂L/∂Wt-1)] (initially, Vt = 0) β = Moving average parameter (const, 0.9) ϵ = A small positive constant (10-8)