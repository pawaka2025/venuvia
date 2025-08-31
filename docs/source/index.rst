Venuvia
===================================

.. image:: images/venuvia.jpg
   :alt: Venus and Jupiter
   :align: center
   :width: 70%

.. raw:: html

   <p style="text-align: center; font-size: smaller;"><em>Image credit: NASA</em></p>

**Venuvia** is an experimental backend for large-scale hypergraph computation implemented as a CPU-only framework and architected around the Partitioned Global Address Space (PGAS) paradigm.

This backend is primarily aimed at solving hypergraph algorithms using probabilistic inferences and Bayesian decision making while also allowing the native expression of probabilistic programming models as hypergraphs ie structural causal models (SCM) and gaussian mixture models (GSM). 

This backend is designed to be hosted in a CPU-only cluster, utilizing PGAS for the topological arrangement of each computing locale and further optimized for large scale computing with HPC-AI by the use of Bayesian neural networks.

.. note::

   This project is under active development.

Contents
--------

.. toctree::

   introduction
   workflow1
   workflow2
   workflow3
   usecases
   hypergraphalgorithms
   ppmodels
   usage
   api
   roadmap
   challenges
