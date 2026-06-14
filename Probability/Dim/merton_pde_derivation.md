# Derivation of the Partial Differential Equation (PDE) for the Merton Model

In the Merton (1974) structural model of credit risk, the firm's equity $E$ is conceptualized as a European call option on the firm's underlying assets $V$, with the strike price being the face value of the firm's zero-coupon debt $D$ maturing at time $T$. 

To price this equity and establish the framework for default probability, we formulate a Partial Differential Equation (PDE) analogous to the Black-Scholes-Merton options pricing framework.

## 1. Core Assumptions

1. **Asset Dynamics:** The firm's total asset value $V$ follows a Geometric Brownian Motion (GBM) under the physical measure $\mathbb{P}$:
   $$dV = \mu V dt + \sigma V dW$$
   where $\mu$ is the expected return on assets, $\sigma$ is the asset volatility, and $dW$ is the increment of a standard Wiener process.
2. **Capital Structure:** The firm issues only two classes of claims: Equity ($E$) and a single zero-coupon bond ($D$) maturing at $T$. 
3. **Frictionless Markets:** There are no transaction costs, taxes, or bankruptcy costs. Trading is continuous, and the risk-free rate $r$ is constant.

## 2. Application of Itô's Lemma

Since the equity value $E$ is a function of the underlying asset value $V$ and time $t$, we can express it as $E(V, t)$. Applying Itô's Lemma to expand $dE$:

$$dE = \left( \frac{\partial E}{\partial t} + \mu V \frac{\partial E}{\partial V} + \frac{1}{2}\sigma^2 V^2 \frac{\partial^2 E}{\partial V^2} \right) dt + \sigma V \frac{\partial E}{\partial V} dW$$

## 3. Constructing the Risk-Free Portfolio

We construct a continuously rebalanced hedging portfolio $\Pi$ consisting of one unit of equity and a short position in $\Delta$ units of the underlying asset $V$:

$$\Pi = E - \Delta V$$

The infinitesimal change in the value of this portfolio over time $dt$ is:

$$d\Pi = dE - \Delta dV$$

Substituting the expressions for $dE$ and $dV$ into the portfolio differential:

$$d\Pi = \left( \frac{\partial E}{\partial t} + \mu V \frac{\partial E}{\partial V} + \frac{1}{2}\sigma^2 V^2 \frac{\partial^2 E}{\partial V^2} \right) dt + \sigma V \frac{\partial E}{\partial V} dW - \Delta (\mu V dt + \sigma V dW)$$

By choosing the hedge ratio $\Delta = \frac{\partial E}{\partial V}$, we completely eliminate the stochastic term (the $dW$ terms cancel out), rendering the portfolio locally risk-free:

$$d\Pi = \left( \frac{\partial E}{\partial t} + \frac{1}{2}\sigma^2 V^2 \frac{\partial^2 E}{\partial V^2} \right) dt$$

## 4. The No-Arbitrage Condition

To preclude arbitrage opportunities, a risk-free portfolio must earn exactly the risk-free interest rate $r$. Therefore, the return on the portfolio over time $dt$ must satisfy:

$$d\Pi = r \Pi dt$$

Substitute $\Pi = E - \frac{\partial E}{\partial V} V$ into the no-arbitrage condition:

$$\left( \frac{\partial E}{\partial t} + \frac{1}{2}\sigma^2 V^2 \frac{\partial^2 E}{\partial V^2} \right) dt = r \left( E - V \frac{\partial E}{\partial V} \right) dt$$

## 5. The Merton PDE

Dividing by $dt$ and rearranging the terms to group all derivatives of $E$ on the left side, we obtain the fundamental PDE for the Merton model:

$$\frac{\partial E}{\partial t} + r V \frac{\partial E}{\partial V} + \frac{1}{2} \sigma^2 V^2 \frac{\partial^2 E}{\partial V^2} - rE = 0$$

### Boundary Conditions
To solve this PDE for the equity value $E(V,t)$, we apply the following terminal and boundary conditions:

1. **Terminal Condition (Payoff at Maturity):** At $t = T$, equity holders receive the residual value after paying debt. If $V_T < D$, they receive nothing (limited liability).
   $$E(V, T) = \max(V - D, 0)$$
2. **Absorbing Barrier at Zero:** If the firm's asset value falls to zero, it remains at zero, and equity is worthless.
   $$E(0, t) = 0$$
3. **Asymptotic Behavior:** As the asset value becomes extremely large, the probability of default approaches zero, and equity becomes essentially equal to the firm value minus the present value of the debt.
   $$\lim_{V \to \infty} E(V, t) = V - D e^{-r(T-t)}$$

Solving the PDE subject to these conditions yields the standard Black-Scholes type formula for equity value.
