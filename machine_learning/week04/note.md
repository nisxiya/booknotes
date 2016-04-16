# Machine Learning Week04

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>


## measure of total cost
 - measure of fit
 - measure of magnitude of efficients

## consider resulting objective
 - $\hat{w}$
 - $RSS(w) + \lambda\cdot||w||_2^2$
 - $||w||_2^2 = \sum_{i=0}^Dw_i$

  if $\lambda$ = 0: reduce to minimizing $RSS(w)$, as before  
  if $\lambda$ = $\infty$: for solutions where $\hat{w}\neq0$, 
      if $\hat{w}$ is $\neq0$, then the total cost should be very large;
      if $\hat{w} = 0$, then $total cost = RSS(0)$ 

## bias-variance tradeoff
 - Large $\lambda$: high bias, low variance (e.g. $\hat{w}$ for $\lambda=\infty$) 
 - Small $\lambda$: low bias, high variance. (e.g. standard least square, RSS fit of high order polynomial for $\lambda=0$)
 
 
 ## Optimizing the ridge objective
  - Step 1
    Rewrite total cost in matrix notation  
    $RSS(w) = \sum_{i=1}^N(y_i - h(x_i)^Tw)^2 = (y-Hw)^T(y-Hw)$  
    
    Rewrite magnitude of coefficients in vector notation  
    $||w||_2^2 = w_0^2 + w_1^2 + w_2^2 + \ldots + w_D^2$ 

  - Step 2
