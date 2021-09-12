# OH DELFT WORKSHOP: Working with a Raspberrypi Cluster

Notes for the assembly, set up and testing of a computer cluster using 

organization notes: https://docs.google.com/document/d/1xCHWA1RshWLqRggzt8hcCR9eQZBT_-WdkGyf8CQeplY/edit#

## Learning Objectives

* Build a computer cluster using raspberry pi’s to introduce architectural aspects of computer clusters.
* Get familiar with the general workflow for performing parallel computations in a  computer cluster.

## Cluster Assembly

An guide to assamble the cluster with pictures.


## Set Up the Cluster

Software:
* [Etcher Balena](https://www.balena.io/etcher/)
* [CNAT-Lite Cluster Controler](https://dist.8086.net/clusterctrl/buster/2020-12-02/2020-12-02-1-ClusterCTRL-armhf-lite-CNAT.zip)
* [Booster P1](https://dist.8086.net/clusterctrl/buster/2020-12-02/2020-12-02-1-ClusterCTRL-armhf-lite-p1.zip)
* [Booster P2](https://dist.8086.net/clusterctrl/buster/2020-12-02/2020-12-02-1-ClusterCTRL-armhf-lite-p2.zip)

Reference: https://medium.com/@dhuck/the-missing-clusterhat-tutorial-45ad2241d738


"The CNAT image will create a subnet for the PI Zeros on the controller pi and this makes set up much easier. It is also more secure as the Nodes will only be visible to the controller image and not to external devices."

1. Install


A guide to install and set up the software


## HPC Computations



### Computing Pi 

This is an example of using a computer cluster to parallelize resource-demanding computatios. Computation of Pi using Monte Carlo Simulation


### Sorting Data

This is a exampel of using a computer cluster to 