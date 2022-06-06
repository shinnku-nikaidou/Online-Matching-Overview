# Classic Matching

### Bipartite graph <a href="#firstheading" id="firstheading"></a>

> [https://en.wikipedia.org/wiki/Bipartite\_graph](https://en.wikipedia.org/wiki/Bipartite\_graph)

A bipartite graph (or bigraph) is a graph whose vertices can be divided into two **disjoint** and **independent** **sets** $$U$$ and $$V$$, that is every edge connects a vertex in $$U$$ to one in $$V$$.&#x20;

One often writes $$G=(U, V, E)$$ to denote a bipartite graph whose partition has the parts $$U$$ and $$V$$, with $$E$$ denoting the edges of the graph.&#x20;

#### Lemma

a bipartite graph is a graph that does not contain any oddlength cycles.



### tree

A `forest` is a graph that contains **no cycles**, and a connected forest is a `tree`.



### alternating path and augmenting path

Consider this graph:

```haskell
import Data.Graph (Graph, Vertex, graphFromEdges, path)
import Data.Maybe (fromJust)
import qualified Data.Bifunctor

type Node = String
type Key = String

edgeList :: [(Node, Key, [Key])]
edgeList =
  [ ("a", "a", ["a'", "b'"]),
    ("b", "b", ["a'", "b'"]),
    ("c", "c", ["b'", "c'", "d'"]),
    ("d", "d", ["c'", "d'"]),
    ("a'", "a'", ["a", "b"]),
    ("b'", "b'", ["a", "b", "c"]),
    ("c'", "c'", ["c", "d"]),
    ("d'", "d'", ["c", "d"])
  ]

valFromNode :: (Node, Key, [Key]) -> Node
valFromNode (a, _, _) = a

graph :: Graph
nodeFromVertex :: Vertex -> (Node, Key, [Key])
vertexFromKey :: Key -> Maybe Vertex
(graph, nodeFromVertex, vertexFromKey) = graphFromEdges edgeList

```

This is a bipartite graph and $$U = \{a,b,c,d\}, V = \{a',b',c',d'\}$$,&#x20;

Suppose $$M$$ be the maximum matching.

```haskell
-- an M's example:

m :: Maybe [(Node, Node)]
m = do
  a' <- v "a'"
  b <- v "b"
  b' <- v "b'"
  c <- v "c"
  d <- v "d"
  d' <- v "d'"
  return $
    [ Data.Bifunctor.bimap v2n v2n x
      | x <- [(a', b), (b', c), (d', d)]
    ]
  where
    v = vertexFromKey
    v2n = valFromNode . nodeFromVertex

-- Output: Just [("a'","b"),("b'","c"),("d'","d")]
```



We call a vertex of $$G$$ matched by $$M$$ if $$M$$ touches that vertex. Otherwise, the vertex is unmatched.

alternating path is a path where **alternately, edges from** $$M-E$$ **and** $$M$$.

```haskell

nodes :: Maybe [Node]
nodes = do
  a <- v "a"
  a' <- v "a'"
  b <- v "b"
  b' <- v "b'"
  c <- v "c"
  c' <- v "c'"
  let vertexes = [a, a', b, b', c, c']
  return $ [valFromNode $ nodeFromVertex x | x <- vertexes]
  where
    v = vertexFromKey

main :: IO ()
main = do
  putStr . show . head $ fromJust nodes
  let print_t x = do
        putStr " -> "
        putStr $ show x
  mapM_ print_t . tail $ fromJust nodes
  putChar '\n'
  return ()

-- Output: "a" -> "a'" -> "b" -> "b'" -> "c" -> "c'"
```



We call an alternating path that ends in an unmatched vertex an augmenting path.

For the matching above, the path $$a \to a' \to b \to b' \to c \to c'$$ is an example of both an **alternating path** and an **augmenting path**.



### Lemma: Berge

A matching $$M$$ is maximum _iff_ it does not admit an `augmenting path`.

Note that if a matching $$M$$ admits an augmenting path $$P$$, then $$M$$ can be augmented by flipping the membership of the edges of $$P$$ in and not in $$M$$.

The new matching's size is one more than that of $$M$$.



Theorem

If $$M$$ is a `maximal matching`, and $$M^{*}$$ __ a `maximum matching`, then $$|M| \geq \frac{1}{2}\left|M^{*}\right|$$.











