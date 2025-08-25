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

- **Prohibitive costs of GPU usage for data analytics**

  GPUs have become the default accelerator for graph systems, especially those leveraging
  GraphBLAS and massively parallel computation. Yet, their architecture is inherently
  hostile to clustered computing environments. Unlike CPUs or distributed memory
  systems that are naturally designed to scale across nodes, GPUs remain optimized for
  monolithic single-unit performance.  

  This has driven the industry towards developing increasingly larger and costlier 
  monolithic units (e.g., NVIDIA A100, H100). Such designs concentrate computational 
  power into fragile singular points of failure: when a GPU fails, the entire expensive 
  unit must be replaced, rather than incrementally scaling or swapping smaller, cheaper 
  components. This lack of fault tolerance makes them impractical for sustainable, 
  large-scale distributed analytics.   

  Moreover, GPUs impose further burdens:  

  - **Economic** – their costs are skyrocketing, pricing out smaller institutions.  
  - **Environmental** – high energy draw and electronic waste from rapid obsolescence.  
  - **Accessibility** – cloud providers (Google, Amazon, IBM) frequently impose regional locks, 
    limiting global availability.  
