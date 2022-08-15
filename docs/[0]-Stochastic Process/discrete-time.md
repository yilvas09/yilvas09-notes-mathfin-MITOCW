# Discrete Time Stochastic Process

## Example: Simple Random Walk

We start by considering a series of random variables independently and identically distributed in Bernoulli distribution:

$$
\left\{Y_{i}: i=1,2, \ldots, t\right\} \text { i.i.d } \sim \operatorname{Ber}(0.5)=\left\{\begin{array}{ll}
1, & p=0.5 \\
-1, & p=0.5
\end{array}\right.
$$

Then $X_t = \sum_{i=1}^t Y_i$ is a **simple random walk**.

### Moments

Moments of $X_t$ for any fixed $t$:

* Mean / first-order moment: $E[X_t] = \sum_{i=1}^t E[Y_i] = 0$;
* Second-order Moment: $E[X^2_t] = \sum_{i=1}^t E[Y^2_i] = t$;
* Variance: $Var[X_t] = E[X_t^2] - E^2 [X_t] = 0$;
* Standard deviation: $\sigma[X_t] = \sqrt{t}$.

### A real-world example: Coin Toss Game

1. A specific Game  
Rules: Keep playing until winning $100 or lossing $100  
Then the player's balance is a simple random walk.  
Final results:
    * win \$100 with probability 0.5
    * lose \$100 with probability 0.5

    Remark: Completely symmetric outcomes! Therefore symmetric probabilities of the results.

2. General Case  
Rules: Keep playing until winning \$B or lossing \$A  
Final results:  
    * win \$B with probability $A/(A+B)$
    * lose \$A with probability $B/(A+B)$  

**Why this prob. distribution?**  
For each $k \in \{k: k = -A, -A+1, ..., B\}$, define
$$
f(k) = \Pr(\text{hit } B \text{ first when started at } k).
$$
Goal: We want to compute $f(0)$.  
What we already knew:  

* boundary values
    $$
    f(B) = 1, f(-A) = 0
    $$  
* difference equation
$$
f(k) = \frac{1}{2} f(k+1) + \frac{1}{2} f(k-1)
$$
Solving the difference equation gives us the resulted prob. distribution.

## Markov Chains

Markov chains are stochastic processes...
> whose effect of the past on the future is summarized *only* by the current state.

Formally, a discrete stochastic process $\{X_t: t=1,2,..\}$ satisfying
$$
\Pr(X_{t+1} = x | X_0, X_1,...,X_t) = \Pr(X_{t+1} = x | X_t)
$$
is a **Markov chain**.

The transition probability $\Pr(X_{t+1} = j | X_t = i)$ can be written in the matrix form, i.e. the (one-step) **transition matrix**:
$$
P = \left(P_{ij}\right)_{S\times S} = \left(\Pr(X_{t+1}=j | X_{t}=i)\right)_{S\times S}
$$
where $S$ is the number of states.

Then the n-step transition probability can be written as
$$
P^{(n)} \doteq \left(\Pr(X_{t+n} = j | X_t=i)\right)_{S\times S} = P^n.
$$

Further question: what is the limit of $P^n$ as $n \to \infty$?

This **stationary distribution**, if it exists, depicts the long-term behavior of a Markov chain, i.e. the steady state, that no longer depends on the initial state $X_0$.  

### Existence of steady state

Given the transition probability matrix $P$ with *all entries positive*, [Perron - Frobenius Theorem](https://en.wikipedia.org/wiki/Perron–Frobenius_theorem) (TODO: add links to useful results in linear algebra) guarantees that

1. $P$ has a largest eigenvalue 1;
2. there exists a steady state vector, $\pi$, which is the eigenvector corresponding to 1.

Remark: Let $\pi = (\pi_1,\pi_2,...,\pi_S)$. Then

\begin{align}
\lim_{n\to\infty} P^n &= (1,...,1)^\top \pi \\
& = \begin{bmatrix}
\pi_1 & \pi_2 & ... & \pi_n\\
... & ... & ... & ...\\
\pi_1 & \pi_2 & ... & \pi_n
\end{bmatrix}
\end{align}

## Martingale

A **martingale** is a stochastic process $\{X_t\}$ that satisfies
$$
X_t = E[X_{t+1} | \mathcal{F_t}] = E[X_{t+1} | X_0,X_1,..,X_t]
$$
where $\mathcal{F}_t$ denotes all the information obtained up to $t$.

Remark: The balance of a *'fair game'* is a martingale, i.e. on average you will not win or lose anything.

## Optimal Stopping Theorem

Given a stochastic process $\{X_t\}$, an integer-valued random variable $\tau$ is called a **stopping time**, if for all $k$, the probability of $\tau \leqslant k$ only depends on $\{X_0,...,X_k\}$.

Intuitively optimal stopping theorem says that:  
> no matter what strategies you use in a martingale game, on average you will not lose or win anything,

where the *'(quitting) strategy'* is a stopping time.

Formally,  
Suppose $\{X_t: t=0,1,2,..\}$ is a martingale and $\tau$ is a stopping time. Furthermore, there exists a constant $T$ s.t. $\tau \leqslant T$. Then
$$
E[X_\tau] = X_0.
$$

### Application: first-hitting probability of simple random walk

* Let $\tau$ be the time of quitting Coin Toss Game.
* By optimal stopping theorem, the expected final balance is exactly the initial balance, i.e.

\begin{align}
E[X_\tau ] &= \Pr(\text{winning}) \cdot B + (1 - \Pr(\text{winning})) \cdot A \\
&=X_0=0.
\end{align}

* Therefore the probability of winning \$B is $A/(A+B)$.
