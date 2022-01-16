# Implementation of the Google's Algorithm

The formula of the rank $r$ of a page $P_{i}$ is:

$$r(P_{i}) = \sum_{j \in B_{P_{i})}} \frac{r(P_{j})}{{|P_{j}|}}$$

$r(P_{i})$ is the rank of page $Pi$, $r(Pj) is the rank of page Pj, $Bi$ is the set of back links to node $i$, $|Pj|$ is the number of outlinks of $j$. Thus, the summatory is on each page $Pj$ that has an outer link to the page $Pi$. Note that, giving a probability interpretation to $1/|Pj|$ it can be understood as a Hidden Markov Model.

It can be also matrix represented:

$$[r_{1}...r_{j}... r_{N}] = [\frac{1}{P1}...\frac{1}{P_{j}}...\frac{1}{P_{N}}]^{T}...[\frac{1}{P1}...\frac{1}{P_{j}}...\frac{1}{P_{N}}]^{T}$$

where if there is no relation between nodes $j$ and $k$, $\frac{1}{P_{k}}$ of row $j$ of the matrix is 0. To solve this we are again on a eigenvalue problem, which must be solved by an iterative method because matrixes are too big to do it using the traditional method.

In a real world network, the majority of nodes are not connected between them so it causes that the majority of the $H$ matrix elements are zero so $H$ is a sparse matrix.

Google's founders began with a simple summation equation based on the underlaying idea of **the more pages point me, the more important I am**. The rank got by the PageRank algorithm is based on the random surfer model. The random surfer model in graph is based on the idea as if a random walker was waling through the graph. Obviously this random walker would more likely step in the nodes that have more paths (i.e., more connections). Then, the PR rank is directly the probability of that a random surfer step in a node (i.e., a webpage).

This model has problems though. One of them, relays in the fact that the internet is full of dangling nodes, such as pdfs or images. More formally speaking, a dangling node is a node that have a row of $0$s in the graph's adjacency matrix. The technique that uses the random surfer to solve dangling nodes problem is called _teletransportation_, and consists in adding a correction matrix $A$ to $H$.

$$ \mathbf{S} = \mathbf{H}+\mathbf{A} = \mathbf{H}+\frac{1}{N} \mathbf{a} \mathbf{1}^{T}$$

where $\mathbf{a}$ is a column vector of size $N$ and $[a]_{i}={0,1}$ being $1$ when $i$ is a dangling node and $0$ otherwise.

Great, we solve the problem of dangling nodes. But, with this $S$ matrix as it is right now, we vannot guarantee that the $S$ matrix will converge at some point (or maybe it won't have a fast convergence, which is a very desirable property). This is caused because there are several isolated or losely connected communities which is a problem for a fast convergence. In order to solve this issue, a personalization matrix is added:

$$\mathbf{1}\mathbf{v^{T}}$$

, where $\mathbf{v}$ is the personalizaed vector of size $N$. This vector $\mathbf{v}$ is changed by Google in order to solve the disconnected graphs problem but also to connect people to regions which they may be more interested in. If we do not want to go to some region of the graph, we would have to fill with $0$’s the corresponding positions of the personalized vector $\mathbf{v}$.

## The final Google Matrix

So, the final Google Matrix looks something like this:

$$G = \alpha \mathbf{S} + (1-\alpha)\mathbf{1}\mathbf{v^{T}}$$

where $ \mathbf{S} = \mathbf{H}+\mathbf{A} = \mathbf{H}+\frac{1}{N} \mathbf{a} \mathbf{1}^{T}$ where $\mathbf{H}$ is the adjacency matrix and $\mathbf{H}$ the solution to dangling nodes problem and $\mathbf{v}$ the personalized vector to solve the absorbing nets problem. 

The $\alpha$ factor has interesting effects in the equation:

* Is a trade-off between _topology_ and teleportation.
* Solves the Markov chain problem.
* Provides sensibility to changes in topology.
* Controls the second eigenvalue of the matrix $\mathbf{G}$. The second eigenvalue of $\mathbf{G}$ has to do with how fast Markov Chain goes.