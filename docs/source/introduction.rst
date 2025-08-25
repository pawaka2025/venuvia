Introduction
===========================

Origin
-----------------------

The name *Venuvia* is inspired by the planets Venus and Jovia (Jupiter), often visible together 
at dawn.

Motivation
-----------------------

This backend has been conceived in order to address a number of use cases:

- **The limits of expressibility of graph systems**: 

  Graphs have become increasingly popular as a modeling tool across domains, from social networks to recommendation systems. Yet their expressive power remains limited when applied to many of today's most critical use cases—such as medicinal research, quantitative analysis, fraud detection, and geophysical surveys.

  Traditional graphs can only capture binary relations between vertices (edges connect two nodes). Hypergraphs, on the other hand, allow hyperedges that connect *sets* of vertices simultaneously, enabling the modeling of higher-order interactions. For example, a single hyperedge can represent a molecular reaction involving multiple compounds, or a coordinated fraud attempt involving several accounts.

  Workarounds in graph databases (such as Neo4j’s use of intermediate “relationship nodes” to mimic hyperedges) quickly become unwieldy. They fail to capture structural nuances like **hyperedge overlaps**, where two hyperedges share subsets of vertices, a property essential for modeling entangled or correlated systems.

  Many of today’s frontier applications depend on these richer structures. For instance:

  - In **tensor-based statistical modeling**, random variables are not always independent or pairwise correlated; they may exhibit *higher-order dependencies* across multiple dimensions, which require hypergraph representations.  
  - In **drug discovery**, reactions often involve more than two molecules at once, with overlapping pathways and cascading effects.  
  - In **fraud detection**, coordinated rings of malicious actors cannot be decomposed into simple pairwise links without losing critical signals.

  Without support for true hypergraph semantics, existing graph systems risk flattening or obscuring this complexity.
