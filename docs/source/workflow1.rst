Workflow 1: Conjugate Inference on Hypergraphs
==================================

Overview
--------
This workflow demonstrates the use of conjugate priors for probabilistic inference 
on hypergraph algorithms using Venuvia.

Objective Definition
-------------------------
We shall begin with an often-used hypergraph algorithm - K-core decomposition. A K-core, when applied to hypergraphs, may be defined in a number of different ways but for now let us go with a single definition: The sum of all weights of hyperedges that a node is a member of - overlapping hyperedges included. Thus a K-core decomposition involves filtering out every node in a hypergraph that does not meet the required number of K-cores - let it be K = n, or K > = n, or K < n, and so on.

Furthermore, in the context of conjugate inference, we will also add an additional criteria: a probabilistic chance P(K) ie to filter the hypergraph for nodes that are 80% likely to have a K-core of at least 5. This is pragmatically useful for 1 - eliminating the need to compute solutions with absolute certainty when high-confidence solutions would already suffice, 2 - allowing flexibility for an algorithm to be used alongside fuzzy or random variables.

For this demonstration we shall settle onto a singular objective for the rest of the workflow: a K-core decomposition where P(K >= 4) = 85%.

Hypergraph Initialization
-------------------------

For this demonstration we shall go with a hypergraph represented as an array of ordered hyperedges. Why ordered hyperedges? Because:
1 - Ordered hyperedges additionally capture hierarchical relationships between nodes - an expression that is extremely important for modelling probabilistic programming models.
2 - Ordered hyperedges can also model unordered hyperedges, which can be interpreted simply as being degenerate ordered hyperedges with zero alternate topological alternatives.
3 - Ordered hyperdges most importantly will allow for additional conditional logic that determines the confidence level of observations, as we will explore shortly in this particular demonstration. 

Let θ represent hyperedge configuration, collectively known as the ordering of a hyperedge as well as the intrinsic property of each node within that hyperedge. The exact formulation is not of relevance - this can be formulated specifically for each individual use case. So for now we will simply say that the true weight produced by each ordered hyperedge is dependent on the value of θ. Hence true_weight=f(weight, θ)

Use case simulation
------------------------

We shall begin with a simulation of a critical use case in power line infrastructure.

Let us imagine we have a network of neighborhood houses. When lightning strikes, excess static voltage will travel from home to home in a chain before being finally absorbed to the ground. Our objective is to identify homes that are 85% likely to receive a power surge, defined by a surge of 4 million volts, in the event of a lightning strike. This will be useful in aiding power line infrastructure providers to prioritize which homes get to receive upgrades in ground wiring in order to reduce the damages caused by lightning strikes. 

Apart from that, we must also include in our analysis that certain homes have weaker ground wiring compared to others, and that the the ordering of the houses in a lighting strike event matters in determining whether or not the voltage actually flowed through.

We can model a lightning strike event to be an ordered hyperedge, the chain of homes that the lightning's voltage flowed through as the nodes of the hyperedge, and the ordering of the homes and the intrinsic ground wiring strength of each home as θ. The weight of the hyperedge will be the observed voltage value of the lighting strike, with the confidence level of such observations determined by θ that we have defined earlier ie homes with poor ground wiring or a chains starting with poorly grounded homes will be more likely to record voltage surges after a lightning strike. 

We can simplify our objective by reducing the 4 million volts number by a million. Thus our objective hence is to identify nodes that satisfy the condition P(K >= 4) = 85%.

Assign Nodes and Their Prior Beliefs
------------------------------------

We shall declare 5 nodes representing 5 homes, and then assign each immediately a prior belief representing their likelihood to receive a power surge in the event of a lightning stirke. This prior belief is not the same value as their true likelihoods, but should be ideally close enough based on past records, a raw Monte-Carlo sampling of a small test data, best guesses, etc in order to facilitate arriving to a posterior belief that closely equates to their true likelihoods.

For now, let us go with a uniform, neutral prior belief for all nodes because we don't have a clear reference of their most likely values. We shall declare for each a Beta conjugate distribution with mean = 0.5 in the middle, kappa = 10 to allow moderate amounts of mean shifting per epoch, sigma = a large value of 0.153 to allow the mean to shift to a wide range of possible values. The other values for each of these Beta distributions will be auto-calculated heuristically so we shall not be concerned about them for now.

nodes = [
    Beta(mean = 0.5, kappa = 10, sigma = 0.153),  
    Beta(mean = 0.5, kappa = 10, sigma = 0.153),  
    Beta(mean = 0.5, kappa = 10, sigma = 0.153),  
    Beta(mean = 0.5, kappa = 10, sigma = 0.153),  
    Beta(mean = 0.5, kappa = 10, sigma = 0.153),
]

Observe formed Hyperedges and Their Weights
-----------------------------------------
We will generate a hypergraph of ordered edges to represent our observations. This can be a representative of past records or a computer simulation of the results of lightning strikes on a chain of homes of various lengths and ordering.

As mentioned previously, each hyperedge will be ordered. Overlaps between hyperedges will also be allowed.

Weights will also be assigned to each hyperedge. It has already been assumed here that each hyperedge's inherent configuration value θ has already been accounted for to influnce the final values of each of these weights. 

obs = [
    {
        "nodes": [0, 1, 2],
        "weight": 3.5,       # observed voltage in million volts
    },
    {
        "nodes": [1, 3],
        "weight": 2.8,
    },
    {
        "nodes": [2, 4],
        "weight": 3.2,
    },
    {
        "nodes": [0, 3, 4],
        "weight": 2.5,
    }
]

Perform Conjugate Inference
---------------------------

.. todo::
   Describe step-by-step updates using conjugate priors.




Compute K-Core Decomposition
----------------------------

.. todo::
   Describe the probabilistic k-core computation workflow.

Output & Analysis
----------------

.. todo::
   Explain output formats, visualization, and downstream analysis.
