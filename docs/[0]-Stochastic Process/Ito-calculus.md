# Ito Calculus

## Ito's Lemma

Let $f(x)$ be a smooth function. We would like to know **what is the differential of $f(B_t)$**.

This problem is of practical use: suppose we want to study the derivative of an asset, whose payoff function is a differentiable function, while the value of underying asset is modelled to follow a Brownian motion.  
(e.g. $f(x)$ is the option value at exercise, $x$ is stock price)

The differential of $f(B_t)$ may be defined as...

* Take 1:
  $$
  df = f'(B_t) \cdot \frac{d B_t}{dt} \cdot dt
  $$
  Doesn't work! $B_t$ is nowhere differentiable.
* Take 2:
  $$
  df = f'(B_t) dB_t
  $$
  Doesn't work! This holds for classical calculus with Taylor expansion, where terms with second or higher orders can be ignored. However, with quadratic variation $(d B_t)^2 = d t$, the second order term cannot be ignored.
* Take 3 (the simplest Ito's Lemma):
  $$
  d f = f'(B_t) d B_t + \frac{f''(B_t)}{2} \underbrace{(d B_t)^2}_{dt}.
  $$

For a more general function $f(t,x)$,
$$
f(t + dt, B_t + dB_t) - f(t,B_t) = f_t dt + f_x dB_t + \frac{1}{2}
\left[f_{tt} (dt)^2 + 2 f_t f_x (dtdB_t) + f_{xx}(dB_t)^2\right].
$$
Therefore,
$$
df = (f_t + \frac{1}{2}f_{xx}) dt + f_x dB_t.
$$

For a more general stochastic process $d X_t = \mu dt + \sigma dB_t$,

\begin{aligned}
f(t + dt, X_t + dX_t) - f(t,X_t) &= f_t dt + f_x (dX_t) + \frac{1}{2}
\left[f_{tt} (dt)^2 + 2 f_t f_x (dtdX_t) + f_{xx}(dX_t)^2\right]\\
&= f_t dt + f_x(\mu dt + \sigma dB_t) + \frac{1}{2}
\left [f_{tt} (dt)^2 + 2f_{xt} (dt)(\mu dt + \sigma dB_t)\right.\\
&+\left. f_{xx} \left(\mu^2 (dt)^2 + 2\mu\sigma dt dB_t + \sigma^2 (dB_t)^2\right )\right],
\end{aligned}

Therefore,
$$
d f = (f_t + \mu f_x + \frac{1}{2}\sigma^2 f_{xx})\ d t + \sigma f_x d B_t.
$$

Ito's Lemma implies that we can no longer use the classic calculus to compute derivatives and integrals.

For example, for stock price model
$$
\frac{d S_t}{S_t} = \sigma dB_t,
$$
$S_t$ is not given by $\exp{(\sigma B_t)}$:  
Let $X_t = \exp{(\sigma B_t)}$, then
$$
\frac{d X_t}{X_t} = \frac{1}{2} \sigma^2 d t + \sigma dB_t
$$
with an extra drift term. Therefore $S_t = \exp{(-1/2) \sigma^2 dt + \sigma dB_t}$.

## Ito Integral

A simple definition of Ito Integral will be the inverse of differentiation.

We define $F(t,B_t)$ as
$$
F(t,B_t) = \int f(t,B_t) d B_t + \int g(t,B_t) dt,
$$
if $dF = f dB_t + g dt$.

Remark: Ito integral is the limit of Riemannian sums when we always take the left-most point of each interval in defining Riemann integral; if not, variance will accumulate because of quadratic variation.
(Intuitively that's because one can only use information up to time $t$.)

## Adapted Process

Let $\{X_t\}$ be a stochastic process. $\Delta(t)$ is said to **be adapted to $X_t$**, if for all $t>0$, $\Delta(t)$ depends only of $\{X_\tau : \tau \in [0,t]\}$.  
Examples:

1. $\{X_t\}$ is adapted to itself;
2. $\{Y_t\}$ where $Y_t = X_{t+1}$ is not adapted to $\{X_t\}$.

**Remark**: In mathematical finance adapted process is often used to model a strategy process.

### Ito Isometry

Suppose $\{\Delta(t)\}$ is adapted to a Brownian motion $\{B_t\}$, then we have
$$
E\left[ \left(\int_0^t \Delta(s)dB_s \right)^2\right] = E\left[ \int_0^t \Delta^2(s)ds \right].
$$

**Applications**:

1. compute variance of random variables that are given as Ito integrals.

2. When is an Ito integral a martingale?  
If $g(t,B_t)$ is adapted to $B_t$, then $\int g(t,B_t)d B_t $ is a martingale *if and only if* $g$ satisfies
    $$
    \int\int g^2(t,B_t)dtdB_t < \infty.
    $$
    Therefore, for Ito process $d X_t = \mu(t,B_t) dt + \sigma(t,B_t) dB_t$, $X_t$ is a martingale if there is no drift, i.e. $\mu = 0$.

## Change of Measure

Let $B_t$ be a Brownian motion with drift $\mu$ and $\widetilde{B}_t$ a Brownian motion without drift, with corresponding probability distributions $P(\omega)$ and $\widetilde{P}(\omega)$.  
Can we switch between the 2 probability distributions by a change of measure?
$$
P(\omega) = Z(\omega) \widetilde{P}(\omega)
$$

### Girsanov's Theorem

The 2 probability distributions above can be switched with each other by a change a measure (i.e. there exists a $Z(\omega)$ such that $P(\omega) = Z(\omega) \widetilde{P}(\omega)$), *if and only if* $P(\omega)$ and $\widetilde{P}(\omega)$ are equivalent, i.e.
$$
P(A) > 0 \iff \widetilde{P}(A)>0,\quad \forall A \subseteq \Omega.$$

Remark: Such $Z(\omega)$ is called **Radon-Nikodym derivative**.

For distributions of Brownian motions $P(\omega)$ and $\widetilde{P}(\omega)$ defined over $[0,T]^\infty$, we have for $Z(\omega)$:
**[To be checked!]**
$$
Z(\omega) = \frac{d \widetilde{P}}{d P} (\omega) = \exp\left(- \mu \omega(T) - \frac{1}{2}\mu^2T \right).
$$

With the Radon-Nikodym derivative, we can transform the expectation of a non-martingale process to the expectation of a martingale, and make use of good properties of martingales.
