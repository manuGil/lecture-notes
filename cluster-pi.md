# OH DELFT WORKSHOP: Working with a Raspberrypi Cluster

Notes for the assembly, set up and testing of a computer cluster using 

organization notes: https://docs.google.com/document/d/1xCHWA1RshWLqRggzt8hcCR9eQZBT_-WdkGyf8CQeplY/edit#

## Learning Objectives

* Build a computer cluster using raspberry pi’s to introduce architectural aspects of computer clusters.
* Get familiar with the general workflow for performing parallel computations in a  computer cluster.

## Cluster Assembly

An guide to assamble the cluster with pictures.

Instructions:
https://clusterctrl.com/setup-assembly


video tutorial
https://youtu.be/fkJnzeigfkc

Important, ssh is disable. How are we going to enable it for the first time?ssssss

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

1. Install Etcher Balena

2. Flash each SD card with the corresponding software:
    * CNAT-Lite Cluster Controler (lagest capacity SD, e.g., 32 GB) for the Rasberry Pi 3 B+
    * Booster P1 for the Pi Zero on slot P1
    * Booster P2 for the Pi Zero on slot P2

3.  Enable SSH on the boot partition of the Cluster Controler.
    * Insert the SD card for the Raspberry Pi 3 in the card reader of the laptop.
    * Navigate to the `/boot/` directory and create a new file with the name `ssh`

4. Enable and configure WiFi on the boot partition.
    * Navigate to the `/boot/` partition and create a `wpa_supplicant.conf` file. *This file disappears once the Pi is booted.
    * Type the following and save the changes. You'll need the name and password of the WiFi network you want to connect to.

```bash
country=NL # Your 2-digit country code
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```

4. Insert the SD cards in the corresponding SD slots of the cluster. The SD card with the Cluster Controller must go to the Raspberry Pi 3. The SD cards with the Boosters P1 and P2 **must go to their corresponting slots on the Pi Zeros.**

5. Connect power supply to Raspberry Pi 3 and boot the cluster.

6. Use a terminal or Putty (Windows) to SSH into the cluster. You must know the IP address of the cluster. Input 'yes' when ask about the ECDSA key, then enter the password for the user 'pi'.

Should we configure unique name for the clusters to avoid the hasle of dealing with Ips?

If using a terminal
```bash
ssh pi@XXX.XXX.XXX.XXXX
```

If using PuTTY

[Add screenshots]


## HPC Computations



### Computing Pi 

This is an example of using a computer cluster to parallelize resource-demanding computatios. Computation of Pi using Monte Carlo Simulation


### Sorting Data

This is a exampel of using a computer cluster to 