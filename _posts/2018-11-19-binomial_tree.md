---
title:  "Pricing Options with Binomial Trees"
date:   2018-11-19
tags: [options, finance, binomial tree]

header:
  image: "images/finance_2.jpg"


excerpt: "Options, Finance, Binomial Trees"
---
# Pricing
## Options
### Binomial Tree

Abaixo vai aparecer a imagem de uma árvore binomial:
<img src="{{ site.url }}{{ site.baseurl }}/images/binomialtree2.png" alt="linearly separable data">

Outra:

<img src="{{ site.url }}{{ site.baseurl }}/images/binomialtree.gif" alt="linearly separable data">

```python
from math import exp
S=100
K=100
dt=1
v=0.3
r=0.03
N=100
h=dt/N
u=math.exp(v*math.sqrt(h))
d=math.exp(-v*math.sqrt(h))
drift=math.exp(r*h)
p=(drift-d)/(u-d)
call = C
# Input stock parameters
# dt = input("Enter the timestep: ")
# S = input("Enter the initial asset price: ")
# r = input("Enter the risk-free discount rate: ")
# K = input("Enter the option strike price: ")
# p = input("Enter the asset growth probability p: ")
# u = input("Enter the asset growth factor u: ")
# N = input("Enter the number of timesteps until expiration: ")

# Input whether this is a call or a put option
#call = raw_input("Is this a call or put option? (C/P) ").upper().startswith("C")

def price(k, us):
    """ Compute the stock price after 'us' growths and 'k - us' decays. """
    return S * (u ** (2 * us - k))

def bopm(k, us):
    """
    Compute the option price for a node 'k' timesteps in the future
    and 'us' growth events. Note that thus there are 'k - us' decay events.
    """

    # Compute the exercise profit
    stockPrice = price(k, us)
    if call: exerciseProfit = max(0, stockPrice - K)
    else:    exerciseProfit = max(0, K - stockPrice)

    # Base case (this is a leaf)
    if k == N: return exerciseProfit

    # Recursive case: compute the binomial value
    decay = exp(-r * dt)
    expected = p * bopm(k + 1, us + 1) + (1 - p) * bopm(k + 1, us)
    binomial = decay * expected

    # Assume this is an American-style option
    return max(binomial, exerciseProfit)

print 'Computed option price: $%.2f' % bopm(0, 0)
```

**Python Code:** [Neural Network from Scratch](https://github.com/jtsulliv/ML-from-scratch/tree/master/Neural-Networks)

The single-layer [Perceptron](https://en.wikipedia.org/wiki/Perceptron) is the simplest of the artificial neural networks (ANNs).  It was developed by American psychologist [Frank Rosenblatt](https://en.wikipedia.org/wiki/Frank_Rosenblatt) in the 1950s.  

Like Logistic Regression, the Perceptron is a linear classifier used for binary predictions.  This means that in order for it to work, the data must be [linearly separable](https://en.wikipedia.org/wiki/Linear_separability).