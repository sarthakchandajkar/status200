**Stochastic gradient descent** (often abbreviated **SGD**) is an iterative method for optimizing an [[Objective Function]] with suitable smoothness properties (e.g. differentiable or sub-differentiable). 

It can be regarded as a <span style="background:#fdbfff">stochastic approximation of gradient descent optimization</span>, since it replaces the actual gradient (calculated from the entire data set) by an estimate thereof (calculated from a randomly selected subset of the data). 

Especially in high-dimensional optimization problems this reduces the very high computational burden, achieving faster iterations in exchange for a lower convergence rate.

The basic idea behind stochastic approximation can be traced back to the <span style="background:#fdbfff">Robbins–Monro algorithm</span> of the 1950s. Today, stochastic gradient descent has become an important optimization method in machine learning.