# Fibonacci Numbers

A mathematical series of numbers as Fibonacci numbers as to provide a foundation for building a [Golden ratio](https://en.wikipedia.org/wiki/Golden_ratio) number, could be computed in a recurrence relation:

Given function _F<sub>n</sub>_ to denote the n<sup>th</sup> position of a Fibonacci sequence; And,

_F<sub>1</sub>_ = _F<sub>2</sub>_ = 1; _F<sub>n</sub>_ = _F<sub>n-1</sub>_ + _F<sub>n-2</sub>_

## A Naive Algorithm

By adopting _top-down_ recursive approach,

<pre>
<code>
FIBONACCI(n)
  if n &les; 2 return 1
  else
    return FIBONACCI(n-1) + FIBONACCI(n-2)
</code>
</pre>

which comes down to a recurrence relation: &Tau;(n) = &Tau;(n-1) + &Tau;(n-2) + &Omicron;(1) &ges; &straightphi;<sup>n</sup>

&Tau;(n) &ges; 2 &sdot; &Tau;(n-2) + &Omicron;(1) &ges; 2<sup>n/2</sup>

Hence, it takes [exponential time](../asymptotic-analysis.md) to compute the n<sup>th</sup> fibonacci number, wherein lots of repetitive computations are being performed; Specifically in the following diagram,

<figure style="text-align:center">
  <img src="../images/fibonacci.png" />
  <figcaption>Figure 1. Fibonacci Numbers in Recursive Computations</figcaption>
</figure>

To improve upon that, a _memoized_ version of such algorithm is introduced:

<pre>
<code>
memo := {}
FIBONACCI(n)
  if n in memo
    return memo[n]
  else
    if n &les; 2 return 1
    else
      memo[n] := FIBONACCI(n-1) + FIBONACCI(n-2)
      return memo[n]
</code>
</pre>

Therefore, FIBONACCI(k) only takes **one** recursion, &forall; k &isin; n; and all memoized calls use &Theta;(1) time. Thus, the time complexity is &Omicron;(n), space complexity is &Omicron;(1)

What about we don't want to have recursions? Then, we can use an extra linear space to store the FIB(n - 1) and FIB(n - 2) when computing FIB(n), which is to use _iteration_ in replacement of _recursion_ and having the same time complexity but avoid the use of recursion, which is also called **bottom-up DP**.

<pre>
<code>
FIBONACCI(n)
  fib := {}
  for k in 1...n
    if k &les; 2
      f = 1
    else
      f = fib[n - 1] + fib[n - 2]
    fib[k] = f
  return fib[n]
</code>
</pre>
