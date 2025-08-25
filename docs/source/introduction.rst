Introduction
===========================

Origin
-----------------------

The name *Venuvia* is inspired by the planets Venus and Jovia (Jupiter), often visible together 
at dawn.

Motivation
-----------------------

This backend has been conceived in order to address a number of pain points:

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

- **Restriction of single-instruction computing architectures**

  SIMD (Single Instruction, Multiple Data) and SIMT (Single Instruction, Multiple Threads) 
  architectures have proven invaluable for accelerating many graph and hypergraph algorithms. 
  However, they suffer from an inherent limitation: they are poorly suited to recursive, 
  stochastic, or branching logic. By design, these paradigms execute the same instruction 
  across multiple data elements in lockstep which makes divergent control flow inefficient 
  or even infeasible.  

  Many critical applications today require algorithms that involve some form of dynamic branching, 
  stochastic decision-making, or recursion. Examples include:

  - **Probabilistic inference** in structural causal models, where the flow of computation 
    depends on stochastic sampling and conditional dependencies between variables.  
  - **Adaptive graph traversal** in fraud detection, where decision paths branch dynamically 
    depending on evolving relational patterns among entities.  
  - **Recursive hypergraph algorithms**, such as multi-level k-core decomposition or 
    hierarchical clustering, which cannot be efficiently flattened into single-instruction streams.

- **All-or-nothing algorithm solving**

  Many contemporary graph and hypergraph algorithms operate in an **all-or-nothing** fashion. 
  That is, computations are typically designed to run to full completion and converge to a 
  deterministic solution before any results can be considered valid. This rigidity is 
  independent of, but exacerbated by, the limitations of single-instruction computing 
  paradigms discussed previously.  

  Such approaches leave little room for approximate, heuristic, or probabilistic solutions, 
  which can be valuable in large-scale, noisy, or partially-observed datasets. For example:

  - Accepting partial solutions where a substantial fraction of nodes (e.g., 80%) satisfy 
    a k-core or other structural property, rather than insisting on global convergence.  
  - Integrating fuzzy, stochastic or random variables alongside deterministic data, 
    enabling richer modeling of uncertainty in real-world systems.  
  - Weighting contributions from highly confident observations more heavily within iterative 
    or temporal computations, rather than treating all data points equally.  

  The all-or-nothing nature of conventional graph algorithms constrains flexibility and 
  expressiveness, particularly when modeling complex, multi-relational or probabilistic 
  systems that are increasingly common in domains such as quantitative finance, fraud 
  detection and scientific simulations.

- **Alignment with ESG goals**

  Venuvia’s CPU-centric, GPU-free architecture offers tangible advantages for corporate 
  Environmental, Social, and Governance (ESG) objectives:

  - **Environmental** – By relying exclusively on CPU clusters, the backend eliminates 
    the need for high-power, specialized GPUs, which require rare earth materials, consume 
    large amounts of electricity, and generate significant heat. This results in a lower 
    environmental footprint for large-scale computation.  

  - **Social / Governance** – The low cost and accessibility of CPU-based PGAS clusters 
    can democratize advanced hypergraph computation, enabling independent researchers and 
    smaller institutions to engage in scalable probabilistic programming and HPC research. 
    This contributes to a more equitable, inclusive, and globally distributed research 
    ecosystem.  

  By demonstrating the feasibility of large-scale, CPU-native hypergraph computation, 
  Venuvia aims to provide organizations with a **cost-effective, environmentally responsible, 
  and socially enabling solution** for their computational analytics needs, aligning directly 
  with ESG principles and facilitating funding for research initiatives.
