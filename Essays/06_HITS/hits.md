# Hypertext Induced Topic Search (HITS)

HITS (Hypertext Induced Topic Search) is the Google’s alternative of PageRank. It was published the same year by Prof. Kleinberg. The idea behind HITS is, whereas PageRank produces **one popularity score for each page**, HITS
produces **two**, and whereas PageRank is **query-independent**, HITS is **query dependent**.

HITS is mainly based in a circular statement. Good authorities are pointed by good hubs and good hubs are pointed to good authorities. We will have some sort of bipartite graph (but without strictly being a bipartite graph).Each netowrk node has two scores.: hub, authority.

The hub score is telling us how important an authority node is in centralizing the information (a hub knows who the authorities are i.e. who the webpages are). They are good at telling us which webpages are the best in one topic.

The authority score is telling us if the hubs that are pointing to the node itself are good hubs i.e. the score of authority depends on the score of the hubs.

In a nutshell: **Hubs** are nodes that **distribute information** and **authorities** are nodes that **are referenced by guys that are good at distributing information**.

Each user has:

* Authority score $X_{i}$
* Hub score $Y_{i}$
* Set of edges (directed). $\rho_{i}{j}$ means $i \rightarrow j$.

## Computation of the Authority and Hub score 

To compute the authority score depending on the hub score and vice versa, we have to backpropagate the reputation. The authority score, is defined matematically as:

$$X_{i}^{k+1} = \sum_{j:\rho_{ji}} Y_{j}^{k} $$

The algorithm is iterative: they all start with the same default value, but the connection will make that some nodes accumulate more or less.

Analogously, the hub score looks like the following:

$$Y_{i}^{k+1} = \sum_{j:\rho_{ij}} X_{j}^{k} $$

This equation iterates and converges into the biggest eigenvalue.

We define the adjacency matrix as

$$
\mathbf{L}_{ij} =
\left \{
\begin{aligned}
    1 \quad \rho_{ij} \neq 0\\
    0 \quad Otherwise
\end{aligned}
\right .
$$

Let's express the equations in terms of the adjacency matrixes:

$$
\mathbf{X}^{k+1} = \mathbf{L}^{T} \mathbf{L} \mathbf{x}^{k}
$$

$$
\mathbf{Y}^{k+1} = \mathbf{L} \mathbf{L}^{T} \mathbf{x}^{k}
$$

We have here a crossed autoreference, that is, an eigenvalue problem. If we remember previous lessons, multiplying a vector by a matrix iterativity it is to take the vector to the eigenvector related with the biggest eigenvalue. Moreover, in previous lessons we normalized the vectors because we are interested in the rank, not in the absolute value, so:

$$
\mathbf{X}^{k+1} = \frac{\mathbf{X}^{k+1}}{||\mathbf{X}^{k+1}||}
$$

$$
\mathbf{Y}^{k+1} = \frac{\mathbf{Y}^{k+1}}{||\mathbf{Y}^{k+1}||}
$$

Finally, the meaning of $[ L^{T} L ]_{ij} = \sum_{k}l_{ik} l_{kj}$ so it represents how connected are $i$ and $j$.
