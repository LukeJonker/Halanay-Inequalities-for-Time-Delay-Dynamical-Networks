***ETC for Networked Time Delay Dynamical Systems of with Arbitrary Network Topology***

---

### Problem Formulation
Let $`N \in \mathbb{N}_+`$ be the number of nodes in this network. Consider the system or arbitrarily many coupled systems with a selection of those systems under event triggered control. 

```math
\begin{aligned}
&\dot x_i(t) = A_i x_i + \sum^N_{j=1}  \Gamma_{ij}  x_j (t- \tau(t)) + K_ix_i(t_{ik}), \quad i = 1,...,N
\end{aligned}
```

Where,
- $`A_i \in \mathbb R^{n\times n}`$ is a nonzero linear transformation modeling linear instantaneous dynamics.
- $`\Gamma_{ij}\in \mathbb R^{n\times n}`$ is a set of linear transformations modeling the linear delay dependance of system $`i`$ on $`j`$. Systems are always self coupled $`\Gamma_{ii} \ne 0`$, but dont need to be coupled with any other particular system so $`\Gamma_{ij} = 0`$ is permitted.
- $`K_i \in \mathbb R^{n \times n}`$ is the linear closed loop control transformation that maps the sampled state to a control response. A system need not be controlled, so $`K_i =0`$ is permitted.
- $`t_{ik}`$ denotes the event subsequence in time of the ETC of system $`i`$. 

Define $`\sigma_i, \alpha_i, \beta_i > 0`$ as engineered parmeters.

Define the ETC as follows for each control independantly:

```math
\begin{aligned}
&\text{ETC Sampling Error:} \quad \epsilon_i(t) := x_i(t_k) - x_i(t), \quad t \in [t_{ik}, t_{ik+1}), \quad \text{for } k\in \mathbb{N}  \\
& \text{Error Measure:} \quad \mathcal C_i (x_i(t), \epsilon_i(t)) := 2x_i^T P_iK_i\epsilon_i(t)- \sigma_i x_i^T P_i x_i \\
& \text{Event Threshold:} \quad \zeta_i := \alpha_i \exp({-\beta_i (t- t_0)}) \\
& \text{Event Subsequence:} \quad t_{ik+1} := \inf\{t_i \gt t_{ik} : \mathcal C_i(x_i(t),\epsilon_i(t)) \ge \zeta_i(t)\}
\end{aligned}
```

Define the directed graph $`\mathcal{G:= (V,E)}`$ where:

```math
\mathcal V:=  \{i \in [1,N]\}, \quad \mathcal E:=\{(i,j) :  i,j \in [1,N], \Gamma_{ij} \ne 0\}
```

Define for a node the reachable set of $`i`$ as $`\mathcal R(i)`$, and the directly connected set of nodes to $`i`$ as $`\mathcal N (i)`$. Define the following equivalence class:

```math
i \sim j \iff i \in \mathcal R(j) \cup \{j\} \text{ and } j \in \mathcal R(i) \cup \{i\}
```

Call these equivalence classes $`[i]`$. Then define $`\mathcal V^* := \mathcal V/\sim`$.

Now define the edges:

```math
\mathcal E^* := \{([i],[j]) : (i,j) \in \mathcal E : [i] \ne [j]\}
```

Define the the quotient graph:

```math
\mathcal G^* := (\mathcal V^*, \mathcal E^*)
```

Define further the reachable set for a supernode on $`\mathcal G^*`$ as $`\mathcal R{([i])}`$ directly connected nodes for $`i`$ that themselves reach $`i`$, $`\mathcal{D}(i)`$, and the set of directly connected nodes of $`i`$ that do not themselves reach the node $`i`$, $`\mathcal B(i)`$. Formally:

```math
\mathcal D(i) := \{\ j \in \mathcal N(i) : i \in \mathcal{R}(j)\} \cup \{i\}, \quad \mathcal B(i) := \mathcal{N}(i) \setminus\mathcal{D}(i)
```

### Results
This section discusses the main results of the paper

#### Lemma 1: $`\mathcal G^*`$ is asyclic

---

It can be proven that the condensation $`\mathcal G^*`$ is asyclic.

Since $`\mathcal G^*`$ is a finite DAG, reachability is a partial order. With the graph being finite we extend this to any arbitrary topological total orderings from this partial ordering, call this arbitrary topological ordering $`\pi`$.

#### Lemma 2: Exponential Attractivity

---

Define: $`||V_i||_t := \sup_{-\tau \le s \le 0}\{V_i(t+s)\}`$ and let $`V_i : [t_0-\tau, \infty) \to \mathbb{R}_{\ge0}`$ be continuous functions such that:

```math
D^+V_i(t) \le -a_iV_i(t) + \sum_{j=1}^{n} c_{ij}||V_j||_t + \alpha_i \exp{-\beta_i(t-t_0)}, \quad i\in[1,n], \quad \forall t\ge t_0 \quad (C1)
```

Assume that:

```math
a_i > \sum_{j \in \mathcal D(i)} c_{ij}, \quad i \in [1,n] \quad (C2)
```

Fix in the topological order of supernodes $`\bar M_i := \max\{\, M_i,\; \kappa_i,\; ||V_i||_{t_0} \, : i \in \mathcal V^*_i\}`$, where leafs can be fixed direcetly and non leaves must be fixed by choosing $`M_i, \kappa_i > 0`$ sufficiently large such that:

```math
a_i > \sum_{j \in  \mathcal D(i)} c_{ij} + \frac{1}{\kappa_i}\sum_{j \in \mathcal B(i)} c_{ij}\,\bar M_j^* + \frac{\alpha_i}{M_i} \quad (E1)
```

For each $`i \in \mathcal V^*_i`$ and then determining $`\bar M_i`$. The ordering ensures that $`\bar M^*_j`$ is always defined before this fixing occurs.
 
Let $`\lambda_i`$ which exists and is unique from $`(C2)`$, be the solution to:

```math
a_i = \lambda + \Big( \sum_{j \in  \mathcal D(i)} c_{ij} + \frac{1}{\kappa_i}\sum_{j \in \mathcal B(i)} c_{ij}\,\bar M_j^* \Big)\exp{\lambda\tau} + \frac{\alpha_i}{M_i} \quad (E2)
```

Let:

```math
\Lambda_{[i]} := \{\lambda_i : i \in [i] \}   \cup
\{\beta_i : \alpha_i > 0, i \in [i]\},
\quad \Lambda_{[i]}^* := \min \Lambda_{[i]} \cup \bigcup_{j \in \mathcal R([i])} \Lambda_{[j]} , \quad
 \bar M_i^* := \max  \bar M_i \cup \bigcup_{j \in \mathcal R(i)} \bar M_j
```

Then:

```math
V_i(t) \le \bar M_i^*\, \exp(-\Lambda_{[i]}^*(t-t_0)), \quad \forall t \ge t_0 \quad (R1)
```


#### Theorem

---

Define: $`h_i > 0`$ and $`a_i := \sum_{j \in \mathcal D(i)} b_{ij} + h_i - \sigma_i`$. 

Assume:

```math
h_i > \sigma_i \quad (As.1)
```

Assume that for $`P := Q^{-1}`$, $`Y := KQ`$, and $`W_i :=(A_i + K_i)^T P_i + P_i(A_i + K_i) + (a_i + \sigma_i)P_i`$

```math
\begin{bmatrix} W_i & \Gamma_{i1}Q_1 & \Gamma_{i2}Q_2 & \cdots & \Gamma_{iN}Q_N \\ Q_1\Gamma_{i1}^T & -b_{i1}Q_1 & & & \\ Q_2\Gamma_{i2}^T & & -b_{i2}Q_2 & & \\ \vdots & & & \ddots & \\ Q_N\Gamma_{iN}^T & & & & -b_{iN}Q_N \end{bmatrix} \preceq 0 \quad (As.2)
```

Then you get exponential attractivity of system $`i`$ to the zero energy state$`^{(i)}`$, and there is no zeno behaviour.$`^{(ii)}`$

##### Proof $`(i)`$

---

Each distinct triggering condition gives:

```math
2x_i^T P_iK_i\epsilon_i(t) \le \sigma_i x_i^T P_ix_i + \alpha_i e^{-\beta_i (t - t_0)}, \quad \forall t \in [t_{ik}, t_{ik+ 1} ) \quad (Obs.1)
```

Re-writing an arbitrary system in terms of its error, since $`K_ix(t_{ik}) = K_ix(t) + K_i\epsilon_i(t)`$ we can write:

```math
\dot x_i(t) = (A_i + K_i) x_i + \sum^N_{j=1}  \Gamma_{ij} x_j (t- \tau(t)) + K_i\epsilon_i
```

Take the Lyapunov quadratic form:

```math
V_i = x_i^T P_i x_i
```

Take its derivative, let $`\dot V`$ be the right upper dini derivative.

```math
\dot V_i = \dot x_i^T P_i x_i + x_i^T P_i \dot x_i
```

Since a quadratic form is a $`1 \times 1`$ matrix it is symmetric and thus is its own transpose, so we can write it equivalently as:

```math
\begin{aligned}
& \dot V_i = (\dot x_i^T P_i x_i)^T + x_i^T P_i \dot x_i \\
& \dot V_i = x_i^T  P_i^T \dot x_i  + x_i^T P_i \dot x_i \\
& \dot V_i = 2x_i^T  P_i \dot x_i  
\end{aligned}
```

Subbing in the system equation for $`i`$, and the error bound:

```math
\begin{aligned}
&\dot V_i = 2x_i^T  P_i  [ (A_i + K_i) x_i + \sum^N_{j=1} \Gamma_{ij}  x_j (t- \tau(t)) + K_i\epsilon_i]  \\ 
&\dot V_i \le   2x_i^T  P_i (A_i + K_i) x_i +  \sum^N_{j=1}  2x_i^T  P_i \Gamma_{ij} x_j (t- \tau(t)) + \sigma_i x_i^T P_ix_i + \alpha_i e^{-\beta_i (t - t_0)}
\end{aligned}
```

By Young's Inequality:

```math
\sum^N_{j=1}  2x^T P_i \Gamma_{ij} x_j (t - \tau) \le   \sum^N_{j=1} b_{ij}^{-1}x_i^TP_i \Gamma_{ij} Q_j \Gamma_{ij}^TP_i x_i +  \sum^N_{j=1} b_{ij} x_j^T(t - \tau) P_j x_j(t-\tau) \quad (Obs.x)
```

Giving us:

```math
\dot V_i \le   2x_i^T  P_i (A_i + K_i) x_i +   \sum^N_{j=1} b_{ij}^{-1}x_i^TP_i \Gamma_{ij} Q_j \Gamma_{ij}^TP_i x_i +  \sum^N_{j=1} b_{ij} x_j^T(t - \tau) P_j x_j(t-\tau) + \sigma_i x_i^T P_ix_i + \alpha_i e^{-\beta_i (t - t_0)}
```

Notice that for positive coefficients $`b_{ij}`$ and $`a_i`$  with $`\|V_i\| := \sup_{ - \tau \le s \le 0}\{V_i(t+s)\}`$ we can say:

```math
a_iV_i(t)  - \sum_{j=1}^N b_{ij}\|V_j \|_t  \le a_iV_i(t)  - \sum_{j=1}^N b_{ij}V_i(t-\tau) \quad (Obs.x)
```

Which when combined with our main equation gives:

```math
\dot V_i + a_iV_i(t)  - \sum_{j=1}^N b_{ij}\|V_j \|_t   \le   2x_i^T  P_i (A_i + K_i) x_i + a_iV_i(t)  - \sum_{j=1}^N b_{ij}V_i(t-\tau) \\ +    \sum^N_{j=1} b_{ij}^{-1}x_i^TP_i \Gamma_{ij} Q_i \Gamma_{ij}^TP_i x_i  +   \sum^N_{j=1} b_{ij} x_j^T(t - \tau) P_j x_j(t-\tau) + \sigma_i x_i^T P_ix_i + \alpha_i e^{-\beta_i (t - t_0)}
```

By the symmetrization identity:

```math
2x_i^T  P_i (A_i + K_i) x_i + \sigma_i V_i + a_iV_i = x_i^T[(A_i + K_i)^T P_i + P_i(A_i + K_i) + (a_i + \sigma_i)P_i ]x_i \quad (Obs.x)
```

Combining this with the main equation we get:

```math
\dots \le  x_i^T[(A_i + K_i)^T P_i + P_i(A_i + K_i) + (a_i + \sigma_i)P_i ]x_i   - \sum_{j=1}^N b_{ij}V(t-\tau) \\ +    \sum^N_{j=1} b_{ij}^{-1}x_i^TP_i \Gamma_{ij} Q_j \Gamma_{ij}^TP_i x_i  +   \sum^N_{j=1} b_{ij} x_j^T(t - \tau) P_j x_j(t-\tau)  + \alpha_i e^{-\beta_i (t - t_0)}
```

Simplifying to:

```math
\dots \le  x_i^T \left[(A_i + K_i)^T P_i + P_i(A_i + K_i) + (a_i + \sigma_i)P_i + \sum^N_{j=1} b_{ij}^{-1} P_i \Gamma_{ij} Q_j \Gamma_{ij}^TP_i\right]x_i  +  \alpha_i e^{-\beta_i (t - t_0)}
```

Let:

```math
S_i := \left[(A_i + K_i)^T P_i + P_i(A_i + K_i) + (a_i + \sigma_i)P_i + \sum^N_{j=1} b_{ij}^{-1} P_i \Gamma_{ij} Q_j \Gamma_{ij}^TP_i\right]
```

Taking the congruence with the symmetric and invertible $`Q_i`$, $`Q_i  S_i Q_i`$, and defining $`Y_i:= K_iQ_i`$ yeilds:

```math
\bar S_i := A_iQ_i +Q_i A_i^T + Y_i + Y_i^T + (a_i + \sigma_i) P + \sum_{j = 1}^N b_{ij}^{-1}  \Gamma_{ij} Q_j \Gamma_{ij}^T
```

The BMI term is the sum. Grouping the rest under $`W_i`$ in $`(Q_i, Y_i)`$:

```math
W_i + \sum_{j = 1}^N b_{ij}^{-1}  \Gamma_{ij} Q_j \Gamma_{ij}^T \preceq 0
```

$`-b_{ij}Q_j`$ being negative defininite; since $`b_{ij}`$ is strictly positive and $`Q_i`$ is positive definite, lets us take Shurs compliment:

```math
A - B(-C)^{-1}B^T \preceq 0 \iff \begin{bmatrix} A & B \\ B^T & C \end{bmatrix} \preceq 0, \quad C \preceq 0
```

with $`C = -b_{ij}Q_i`$, $`A= W_i`$ and $`B = \Gamma_{ij}Q_j`$, giving the matrix:

```math
\bar S_i^\circ := \begin{bmatrix} W_i & \Gamma_{i1}Q_1 & \Gamma_{i2}Q_2 & \cdots & \Gamma_{iN}Q_N \\ Q_1\Gamma_{i1}^T & -b_{i1}Q_1 & & & \\ Q_2\Gamma_{i2}^T & & -b_{i2}Q_2 & & \\ \vdots & & & \ddots & \\ Q_N\Gamma_{iN}^T & & & & -b_{iN}Q_N \end{bmatrix}
```

So by congruance and by shurs compliment $`S_i^\circ`$ is negative semidefinite if and only if $`\bar S_i`$ is negative semidefinite which is negative semidefinite if and only if $`S_i`$ is negitive semidefinite. Since we know that $`\bar S_i^\circ`$ is negative semidefininte by $`(As.2)`$, this chain of equivalence means drop $`S_i`$ term without violating the inequality, giving:

```math
\dot V_i + a_iV_i  - \sum_{j=1}^N b_{ij}\|V_j \|_t \le  \alpha_i e^{-\beta_i (t - t_0)}
```

Which reorganizes to:

```math
\dot V_i(t)  \le  - a_iV_i(t)  + \sum_{j=1}^N b_{ij}\|V_j \|_t + \alpha_i e^{-\beta_i (t - t_0)}
```

This is $`(C1)`$ of the Halanay result and $`(As.1)`$ together with the $`(E1–E2)`$ construction the revised Halanay lemma yields $`(R1)`$. $`\quad \square`$

##### Proof $`(ii)`$

---

Recall first that for any arbitrary node $`i`$ that we have established:

```math
\begin{aligned}
&V_i(t) \le \bar M_i^* \exp(-\Lambda_{[i]}^*(t-t_0)) \iff x^TP_ix \le \bar M_i^*\exp(-\Lambda_{[i]}^*(t-t_0)) \\
& \iff \|x_i(t)\|^2 \lambda_{\min}(P_i) \le \bar M_i^* \exp(-\Lambda_{[i]}^*(t-t_0)) \\
&\|x_i(t)\| \le \sqrt{\frac{\bar M_i^*}{\lambda_{\min}(P_i)}} \exp(-\Lambda_{[i]}^*/2(t-t_0))
\end{aligned}
```

So for any $`i`$ controlled or otherwise we have:

```math
\|x_i(t)\| \le \sqrt{\frac{\bar M_i^*}{\lambda_{\min}(P_i)}} \exp(-\Lambda_{[i]}^*/2(t-t_0)) \quad (Obs 3.1)
```

Between arbitrary events $`t\in [t_{ik},t_{ik+1})`$ the system is given by:

```math
\begin{aligned}
&\dot x_i(s) = A_i x_i + \sum^N_{j=1}  \Gamma_{ij}  x_j (t- \tau(s)) + K_ix_i(t_{k}), \quad i = 1,...,N
\\ \\
& \int_{t_{ik}}^t \dot x_i(s) \,ds = \int_{t_{ik}}^t A_i x_i + \sum^N_{j=1}  \Gamma_{ij}  x_j (t- \tau(s)) + K_ix_i(t_{k}) \, ds
\\ \\
&  \| x_i(t_{k}) - x_i(t_{ik}) \| \le \int_{t_{ik}}^t \| A_i x_i + \sum^N_{j=1}  \Gamma_{ij}  x_j (t- \tau(s)) + K_ix_i(t) \| 
\\ \\
&  \| x_i(t) - x_i(t_{ik}) \| \le \int_{t_{ik}}^t \|A_i\| \|x_i\| + \sum^N_{j=1}  \|\Gamma_{ij}\| \|  x_j (t- \tau(s))\| + \|K_i\| \|x_i(t_{ik})\| \,ds
\end{aligned}
```

Let $`C_i := \sqrt{\frac{\bar M_i^*}{\lambda_{\min}(P_i)}}`$, subbing in $`(Obs.3.1)`$:

```math
\begin{aligned}
&\| x_i(t) - x_i(t_{ik}) \| \le \\ 
&\int_{t_{ik}}^t \|A_i\| C_i \exp(-\Lambda_{[i]}^*/2(t-t_0)) + \sum^N_{j=1}  \|\Gamma_{ij}\|  C_j \exp(-\Lambda_{[j]}^*/2(t- \tau - t_0)) + \|K_i\| C_i \exp(-\Lambda_{[i]}^*/2(t_{ik}-t_0))\,ds
\end{aligned}
```

Note that by definition of $`\Lambda_{[i]}^*`$:

```math
\quad \Lambda_{[j]}^* \ge \Lambda_{[i]}^*  \implies  -\Lambda_{[j]}^* \le -\Lambda_{[i]}^* \implies \exp(-\Lambda_{[j]}^*/2(t- \tau - t_0)) \le \exp(-\Lambda_{[i]}^*/2(t- \tau - t_0))
```

So equivalently:

```math
\begin{aligned}
&\| x_i(t) - x_i(t_{ik}) \| \le \\ 
&\int_{t_{ik}}^t \|A_i\| C_i \exp(-\Lambda_{[i]}^*/2(t-t_0)) + \sum^N_{j=1}  \|\Gamma_{ij}\|  C_j \exp(-\Lambda_{[i]}^*/2(t- \tau - t_0)) + \|K_i\| C_i \exp(-\Lambda_{[i]}^*/2(t_{ik}-t_0))\,ds
\end{aligned}
```

Computing the integtal yeilds:

```math
\begin{aligned}
&\| x_i(t) - x_i(t_{ik}) \| \le \\
& \frac{2}{\Lambda_{[i]}^*} \left( \|A_i \| C_i + \sum_{j = 1}^N \| \Gamma_{ij}\| C_j \exp({\Lambda_{[i]}^* \bar{\tau}/2}) \right) \left( \exp({-\Lambda_{[i]}^*(t_{ik}-t_0)/2)} - \exp({-\Lambda_{[i]}^*(t-t_0)/2}) \right) \\ 
&+ \| K_i \| C_i(t - t_{ik}) \exp({-\Lambda_{[i]}^*(t_{ik}-t_0)/2})
\end{aligned}
```

Note that by definition of the control architecture at $`t = t_{ik+1}`$:

```math
2\|x_i(t)\|\|P_iK_i\|\|x_i(t) - x_i(t_k)\|\ge 2x_i^T(t) P_iK_i e(t) \ge  \sigma_i x_i^T(t_{k+1}) P_i x_i(t_{k+1}) + \alpha_i  \exp({-\beta_i t_{k+1}}) \ge \alpha_i \exp({-\beta_i t_{k+1}}) \quad (x)
```

So applying $`(Obs \,3.1)`$ at $`t_{ik+1}`$:

```math
\alpha_i \exp({-\beta_i t_{k+1}})  \le 2C_i \exp(-\Lambda_{[i]}^*(t_{ik+1}- t_0)/2)   \|P_iK_i\|\|x_{ik+1}(t) - x_i(t_{ik})\|  \quad (Obs 3.2)
```

Multiply both sides of $`(x)`$ by $`2C_i \exp(-\Lambda_{[i]}^*(t_{ik+1}- t_0)/2)   \|P_iK_i\|`$ and let $`t = t_{ik+1}`$

```math
\begin{aligned}
&\alpha_i \exp({-\beta_i t_{k+1}}) \le 2C_i \exp(-\Lambda_{[i]}^*(t_{ik+1}- t_0)/2)   \|P_iK_i\| \|x_i(t_{ik+1}) - x_i(t_k)\|\\ \\
&\le 2C_i \exp(-\Lambda_{[i]}^*(t_{ik+1}- t_0)/2)   \|P_iK_i\|\\ 
&  (\frac{2}{\Lambda_{[i]}^*} \left( \|A_i \| C_i + \sum_{j = 1}^N \| \Gamma_{ij}\| C_j \exp({\Lambda_{[i]}^* \bar{\tau}/2}) \right) \left( \exp({-\Lambda_{[i]}^*(t_{ik}-t_0)/2)} - \exp({-\Lambda_{[i]}^*(t-t_0)/2}) \right) \\
&+\| K_i \| C_i(t - t_{ik}) \exp({-\Lambda_{[i]}^*(t_{ik}-t_0)/2}))
\end{aligned}
```

Multiply both sides by $`\exp(\Lambda_{[i]}^* t_{ik})`$ and let $`\Delta_{ik} := t_{ik+1} - t_{ik}`$

```math
\begin{aligned}
&\alpha_i e^{-\beta_i \Delta_{ik}} e^{(\Lambda_{[i]}^* - \beta_i)t_{ik}} \le \frac{4C_i\Vert{}P_iK_i\Vert{}}{\Lambda_{[i]}^*} \Big(\Vert{}A_i\Vert{}C_i + \sum_{j=1}^N \Vert{}\Gamma_{ij}\Vert{}C_j e^{\Lambda_{[j]}^* \bar{\tau}/2}\Big) e^{\Lambda_{[i]}^* t_0} (e^{-\Lambda_{[i]}^* \Delta_{ik}/2} - e^{-\Lambda_{[i]}^* \Delta_{ik}})
\\
&+  2C_i^2\Vert{}P_iK_i\Vert{}\Vert{}K_i\Vert{} e^{\Lambda_{[i]}^* t_0} \Delta_{ik} e^{-\Lambda_{[i]}^* \Delta_{ik}/2}
\end{aligned}
```

Let:

```math
\delta_1 := \frac{4C_i\Vert{}P_iK_i\Vert{}}{\Lambda_{[i]}^*} e^{\Lambda_{[i]}^* t_0} \Big(\Vert{}A_i\Vert{}C_i + \sum_{j=1}^N \Vert{}\Gamma_{ij}\Vert{}C_j e^{\Lambda_{[j]}^* \bar{\tau}/2}\Big), \quad \delta_2 := 2C_i^2\Vert{}P_iK_i\Vert{}\Vert{}K_i\Vert{} e^{\Lambda_{[i]}^* t_0}
```

Then:

```math
\alpha_i e^{-\beta_i \Delta_{ik}} e^{(\Lambda_{[i]}^* - \beta_i)t_{ik}} \le \delta_1 (e^{-\Lambda_{[i]}^* \Delta_{ik}/2} - e^{-\Lambda_{[i]}^* \Delta_{ik}}) + \delta_2 \Delta_{ik} e^{-\Lambda_{[i]}^* \Delta_{ik}/2}
```

Suppose for contradiciton that system $`i`$ exhibits Zeno Behaviour. That is there exists a time $`\bar t_i < \infty`$ with $`t_{ik} \to \bar t_i`$ as $`k\to \infty`$. Then every event satisfies $`t_{ik} \le \bar t_i`$, and since $`\beta_i \ge \Lambda_{[i]}^*`$ we know that $`\Lambda_{[i]}^* - \beta_i \le 0`$, so:

```math
\exp((\Lambda_{[i]}^* - \beta_i) t_{ik}) \ge \exp((\Lambda_{[i]}^* - \beta_i)\bar t_i) \gt 0
```

So:

```math
\alpha_i e^{-\beta_i \Delta_{ik}} e^{(\Lambda_{[i]}^* - \beta_i)\bar t_{i}} \le \delta_1 (e^{-\Lambda_{[i]}^* \Delta_{ik}/2} - e^{-\Lambda_{[i]}^* \Delta_{ik}}) + \delta_2 \Delta_{ik} e^{-\Lambda_{[i]}^* \Delta_{ik}/2}
```

Define $`c_i := \alpha_i\exp((\Lambda_{[i]}^* - \beta_i)\bar t_i)>0`$ and:

```math
g_i(T):= c_i e^{-\beta_i \Delta_{ik}} - \delta_1 (e^{-\Lambda_{[i]}^* \Delta_{ik}/2} - e^{-\Lambda_{[i]}^* \Delta_{ik}}) + \delta_2 \Delta_{ik} e^{-\Lambda_{[i]}^* \Delta_{ik}/2} \le 0 \quad (x)
```

So: $`g_i(T) \le 0, \quad \forall k`$. Consider:

```math
g_i(0) = c_i > 0, \quad g_i(\infty) = \infty
```

The subtracted terms dominating near infinity (for large $`T`$, $`\delta_2 T e^{-\Lambda_{[i]}^* T/2}`$ decays slower than $`c_i e^{-\beta_i T}`$ precisely because $`\beta_i \ge \Lambda_{[i]}^* > \Lambda_{[i]}^*/2`$, so $`g_i(T) < 0`$ for all sufficiently large $`T`$. So $`g_i`$ contains at least one root. Define:

```math
\bar T:= \min\{ T > 0: g_i(T) = 0\}
```

And $`g_i(T) > 0`$ on $`t\in[0, \bar T)`$. 

For every $`k`$, $`(x)`$ tells us that $`g_i(\Delta_{ik}) \le 0`$, so $`\Delta_{ik} \notin [0, \bar{T}_i)`$, i.e.$$\Delta_{ik} = t_{i,k+1} - t_{ik} \ge \bar{T}_i > 0 \quad \text{for all } k.$$But the Zeno hypothesis $`t_{ik} \to \bar{t}_i < \infty`$ forces $`\Delta_{ik} \to 0`$. This is a contradiction. Therefore no finite accumulation point $`\bar{t}_i`$ exists, and agent $`i`$ generates only finitely many events on any bounded interval. $`\quad \square`$

---
