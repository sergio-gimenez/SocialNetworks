# Singular Value Decomposition and its properties

If we have dimensions $n \geq k$ and $m \geq k$, $||kA − A_{K}||$ is the minimal best approximation of order $K$. Where $A_{K}$s is the $A$ matrix belonging to dimension $K × K$. This works because SVD works with Gram-Schimdt, $U$ and $V$ are computed by this
method.

## Semantic Projection

Let's keep the first K elements:

$$\mathbf{A} = \mathbf{U_{K}} \mathbf{\Sigma_{K}} \mathbf{V_{K}^{T}}$$

We will use $\mathbf{U_{K}}$ for projecting the rows of $\mathbf{A}$:

$$\mathbf{P}_{k} = \mathbf{d}_{test}^{T} \mathbf{U}_{K}$$

where values inside $\mathbf{P}_{k}$, $\mathbf{p}_{i}$ indicates how similar is $\mathbf{d}_{test}$ to $\mathbf{U}_{i}$.

One of the functions of SVD is to get similarities between terms. With these similarities, we can get: for example, Google AdWords
(The algorithm from Google for selling words).

It follows the Game Theory You want to minimize the price you pay.

With the matrix $\mathbf{A} \mathbf{A}^{T}$ we can find the effective words, and how to buy AdWords.
