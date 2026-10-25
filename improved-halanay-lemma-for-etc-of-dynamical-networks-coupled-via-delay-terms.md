***Improved Halanay Lemma for ETC of Dynamical Networks Coupled Via Delay Terms***

---


#### Lemma


Fix $`n \in \mathbb{Z}_{\ge 1}`$, $`t_0 \in \mathbb{R}`$, $`\tau > 0`$, and constants $`a_i, \beta_i > 0`$, $`\alpha_i \ge 0`$, $`b_{ij} \ge 0`$ for $`i, j \in [1,n]`$, with $`b_{ii} > 0`$

Define: $`\|V_i\|_t := \sup_{-\tau \le s \le 0}\{V_i(t+s)\}`$ and let $`V_i : [t_0-\tau, \infty) \to \mathbb{R}_{\ge0}`$ be continuous functions such that:

```math
D^+V_i(t) \le -a_iV_i(t) + \sum_{j=1}^{n} c_{ij}\|V_j\|_t + \alpha_i e^{-\beta_i(t-t_0)}, \quad i\in[1,n], \quad \forall t\ge t_0 \quad (C1)
```

Define the directed graph $`\mathcal{G:= (V,E)}`$ where:

```math
\mathcal V:=  \{i \in [1,n]\}, \quad \mathcal E:=\{(i,j) :  i,j \in [1,n], c_{ij} \gt 0\}
```

Define for a node the reachable set of $`i`$ as $`\mathcal R(i)`$, and the directly connected set of nodes to $`i`$ as $`\mathcal N (i)`$. Define further the directly connected nodes for $`i`$ that themselves reach $`i`$, $`\mathcal{D}(i)`$, and the set of directly connected nodes of $`i`$ that do not themselves reach the node $`i`$, $`\mathcal B(i)`$. Formally:

```math
\mathcal D(i) := \{\ j \in \mathcal N(i) : i \in \mathcal{R}(j)\} \cup \{i\}, \quad \mathcal B(i) := \mathcal{N}(i) \setminus\mathcal{D}(i)
```

Define the following equivalence class:

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

It can be proven that the condensation $`\mathcal G^*`$ is asyclic.

Since $`\mathcal G^*`$ is a finite DAG, reachability is a partial order. With the graph being finite we extend this to any arbitrary topological total orderings from this partial ordering, call this arbitrary topological ordering $`\mathcal I`$.

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
a_i = \lambda + \Big( \sum_{j \in  \mathcal D(i)} c_{ij} + \frac{1}{\kappa_i}\sum_{j \in \mathcal B(i)} c_{ij}\,\bar M_j^* \Big)e^{\lambda\tau} + \frac{\alpha_i}{M_i} \quad (E2)
```

Let:

```math
\Lambda_i := \{\lambda_i\} \cup \{\beta_i : \alpha_i > 0\}, \qquad \Lambda_i^* := \min \Lambda_i \cup \bigcup_{j \in \mathcal R(i)} \Lambda_j, \quad \bar M_i^* := \max  \bar M_i \cup \bigcup_{j \in \mathcal R(i)} \bar M_j
```

Then:

```math
V_i(t) \le \bar M_i^*\, e^{-\Lambda_i^*(t-t_0)}, \quad \forall t \ge t_0 \quad (R1)
```

Proof: [removed]

===
