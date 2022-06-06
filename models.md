# Models

### Online Bipartite Matching

> \[63] R. M. Karp, U. V. Vazirani, and V. V. Vazirani, “An optimal algorithm for on-line bipartite matching,” in STOC, pp. 352–358, 1990.

there is a bipartite graph $$G(U,V,E)$$ where one side $$U$$ is known to us in advance and the other $$V$$arrives online, one vertex at a time. When a vertex $$v \in V$$ arrives, its neighbors in $$U$$ are revealed.



### Online vertex-weighted bipartite matching

A generalization of Online Bipartite Matching, in which each vertex $$u \in U$$ has a non-negative weight $$w_u$$, goal is to maximize the sum of weight of vertices in $$U$$

> Clearly, if for all $$u\in U$$, $$w_u=1$$, gives us the unweighted version as a special case.



### Adwords

Each vertex $$u \in U$$ has a budget $$B_{u}$$, and edges $$(u, v) \in E$$ have bids $$\text{bid }_{u v}$$. When we match an arriving vertex $$v$$ to a neighbor $$u$$, then $$u$$ depletes $$\text{bid }_{u v}$$ amount of its budget.&#x20;

When a vertex depletes its entire budget, then it becomes unavailable.&#x20;

The goal is to maximize the total budget spent.



#### The small bids assumption

For each $$u, v$$ , $$\text{bid }_{u v}$$ is very small compared to $$B_u$$.



`On-line vertex-weighted bipartite matching` is a special case of Adwords in which $$B_u = w_u$$ for every $$u$$, and $$\text{bid }_{u v} = w_u$$ for each $$(u,v) \in E$$.

> Note: However, `online vertex-weighted matching` and `online bipartite matching` are not special cases of `Adwords` once we make `the small-bids assumption`.



### Display Ads

Each vertex $$u \in U$$ has an integral capacity $$c_{u}$$, which is an upper bound on **how many** vertices $$v \in V$$ can be matched to $$u$$. Each edges $$(u, v) \in E$$ has a weight $$w_{u v}$$.&#x20;

The goal is to maximize the total weight of edges matched. Again, we can identify an important special case:

#### The large capacity assumption:&#x20;

For each $$u, c_{u}$$ is a large number.



With $$c_u = 1 ,\forall u$$ and $$w_{uv} = w_u,\forall (u,v) \in E$$, this problem tranform into Online vertex-weighted bipartite matching.

> Adwords and Display Ads are unrelated problems
>
> since Adwords has a constraint on the budget
>
> while Display Ads has a constraint on the capacity.



### Online Submodular Welfare Maximization

Vertex $$u \in U$$ has a non-negative **monotone** **submodular** valuation function $$f_{u}: 2^{V} \rightarrow \mathbb{R}^{+}$$.&#x20;

> A set function is called non-negative if $$f(S) \geq 0 \quad \forall S \subseteq V$$. It is called **monotone** if $$f(S) \leq f(T), \quad \forall S \subseteq T \subseteq V$$.&#x20;
>
> It is called **submodular** if for any two sets $$X$$ and&#x20;
>
> $$
> Y: f(X \cup Y)+f(X \cap Y) \leq f(X)+f(Y)
> $$
>
> This is also equivalent to the following:&#x20;
>
> $$
> \forall S \subseteq T \subseteq V, x \notin T: f(S+x)-f(S) \geq f(T+x)-f(T)
> $$

The goal is to maximize the sum of values of the allocation.&#x20;

More precisely, the online allocation produces a partition of $$V$$, where $$V_{u}$$ is the set of vertices allocated to $$u$$.&#x20;

The goal is to maximize&#x20;

$$
\sum_{u} f_{u}\left(V_{u}\right)
$$

> vertices in $$U$$ are agents, and vertices in $$V$$ are items, Items arrive online; each item has to be allocated to one agent as soon as it arrives.





