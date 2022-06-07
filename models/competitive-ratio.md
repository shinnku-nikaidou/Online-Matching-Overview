# Competitive Ratio

#### non-adaptive adversary

The adversary will not have access to the outcomes of the random choices made by the algorithm (equivalently, of the random coins of the algorithm),

but will have to fix the input graph in advance.



### stochastic input models

#### 1. Adversarial order

In this model we assume no knowledge of the query sequence, that is, no knowledge of $$V, E$$, and the arrival order of $$V$$.&#x20;

The algorithm begins with only the knowledge of $$U$$, and, at any point in time, it knows only the vertices in $$V$$ which have already arrived, and the edges incident on them.

#### 2. Random order

Here we assume that although the input $$G(U, V, E)$$ is adversarial, the query sequence $$V$$ arrives in a random order.&#x20;

Thus, the adversary can choose the worst graph (after seeing the code of the algorithm), but not the arrival order of $$V$$; vertices of $$V$$ arrive in a `uniform random permutation`.

#### 3. Unknown IID

> IID: Independent and identically distributed random variables

In this model we start with the abstraction of a vertex type, which encodes the set of neighbors in $$U$$, and bids or weights on the incident edges (as relevant to the problem).&#x20;

There is a collection $$\mathcal{T}$$ of types of vertices, and a distribution $$\mathcal{D}$$ on $$\mathcal{T}$$.&#x20;

The query sequence is picked in the following manner: at each time a type $$t \in \mathcal{T}$$ is drawn from $$\mathcal{D}$$, IID, and a vertex $$v \in V$$ of that type $$t$$ is instantiated, and arrives at that time. $$\mathcal{D}$$ is not known to the algorithm before-hand.

#### 4. Known IID

This is identical to the Unknown IID model, except that $$\mathcal{D}$$ is provided to the algorithm in advance.











