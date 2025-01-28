# Fused-Specht-Polynomials

This repository aims to implement numerically a combinatorial formula for a novel class of polynomials called Fused Specht polynomials that I introduced with Augustin Lafay and Eveliina Peltola in https://arxiv.org/abs/2410.09798.

These polynomials generalize the celebrated Specht polynomials, introduced in the first half of the XXth century to describe irreducible representations of the symmetric group.

The $\textbf{first part}$ is to implement the monomials defined in Proposition 2.22. More precisely, to a Young tableau $U$ (that we consider rectangular for simplicity) we associate the monomial

\begin{equation} \label{monomial}
m_U(x_1,\dots,x_d) := \prod_{k=1}^d \frac{(-1)^{\binom{s_k}{2}} \text{sgn}(\tau_{U;k})}{s_k!} \, S_{\lambda^U(k)}(1^{s_k}) \, x_k^{|\lambda^U(k)|}.
\end{equation}

Below we define the relevant quantities at play:

$\bullet$ $s_k$ is the number of times the integer $k$ appears in the tableau $U$.

$\bullet$ We denote by $(r_i^U(k))_{i=1}^{s_k}$ the sequence of row numbers of boxes of $U$ containing the entry $k$, 
ordered by column-reading $U$. Moreover, let $(r_i^{U,\text{ord}}(k))_{i=1}^{s_k}$ be the ordering of $(r_i^U(k))_{i=1}^{s_k}$ in decreasing order. Then, $\tau_{U;k}$ denotes a permutation that sends $(r_i^U(k))_{i=1}^{s_k}$ to $(r_i^{U,\text{ord}}(k))_{i=1}^{s_k}$, that is, $(r_{\tau_{U;k}(i)}^U(k))_{i=1}^{s_k} = (r_i^{U,\text{ord}}(k))_{i=1}^{s_k}$. 
Finally, we define $\lambda^U(k)$ to be the partition
\begin{align} \label{eq:defpartitionlambda}
\lambda^U(k) := \big( r_i^{U,\text{ord}}(k)-s_k+i-1 \big)_{i=1}^{s_k}.
\end{align} 

$\bullet$ $S_{\lambda^U(k)}(1^{s_k})$ denotes the Schur polynomial associated with the partition $\lambda^U(k)$ and evaluated at 1 in each of its $s_k$ variables:
\begin{align*}
S_{\lambda^U(k)}(1^{s_k}) = \prod_{1\leq i < j \leq s_k} \frac{\lambda^U_i(k)-\lambda^U_j(k)+j-i}{j-i}.
\end{align*} 

The $\textbf{second part}$ implements the combinatorial formula for the fused Specht polynomial:

\begin{align} 
\mathcal F_F = |\text{Stab}{\mathfrak{Q}_\lambda}{F}| \sum_{U \in(\mathfrak{Q}_\lambda.F) \backslash W_F} \text{sign}(\sigma_{F;U}) \; m_U .
\end{align}

The various objects involved require some definitions. 

$\bullet$ $F$ is a $\textit{filling}$: it's is a tableau where the entry $k$ appears freely $s_k$ number of times.  

$\bullet$ In words, the set $(\mathfrak{Q}_\lambda.F) \backslash W_F$ consists of all tableaux obtained from F by permuting different entries within columns, except those where the same entry $k$ appears more than once in any given row.

$\bullet$ Finally, $|\text{Stab}{\mathfrak{Q}_\lambda}{F}| = \prod_{k=1}^d\prod_{i=1}^{n_{\text{col}}} p_{i,k}!$, where $n_{\text{col}}$ is the number of columns of the tableau F, and where $p_{i,k}$ is the number of times that the number $k$ appears in the column $i$.
