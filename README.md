# dp-rebalance

**dp-rebalance** is a research-oriented Python project that implements a **Dynamic Programming (DP) framework** for optimal portfolio rebalancing under transaction costs, enhanced with a **mean-variance risk penalty**.  
It allows users to input any list of stock tickers, discretizes market states from momentum and volatility, estimates state-conditional returns and risks, and computes the optimal rebalancing policy via the **Bellman equation**.

---

## 🔎 Mathematical Model

We model portfolio rebalancing as a **Markov Decision Process (MDP)**:

- **State**:  
  - Market regime `s` (defined by quantile bins of momentum & volatility)  
  - Current portfolio weight `w`  

- **Action**:  
  Choose a new weight vector `w'` from a discretized simplex grid.  

- **Reward** (risk-adjusted):  

  \[
  u_s(w) = w^\top \mu_s \;-\; \tfrac{1}{2}\lambda\, w^\top \Sigma_s w
  \]

  where  
  - \( \mu_s \): expected returns in state `s`  
  - \( \Sigma_s \): covariance matrix in state `s`  
  - \( \lambda \): risk aversion parameter  

- **Bellman equation**:  

  \[
  V(s,w) = \max_{w'} \{ u_s(w') \;-\; tc \cdot \|w'-w\|_1 + \gamma \cdot \mathbb{E}_{s'|s}[V(s', w')] \}
  \]

This formulation balances **expected returns, risk, and transaction costs**, allowing the policy to learn an **inaction band** (rebalance only when necessary).

---

## 📂 Project Structure

