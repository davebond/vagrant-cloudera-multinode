# Vagrant Cloudera Multinode

## Provisioning
Edit Vagrantfile and configure node\_count and node\_ram

Then:

    vagrant up

## Installation
SSH into the manager node

		vagrant ssh manager

Run the cloudera installer

		sudo chmod +x ./files/install.sh
		./files/install.sh

After the installation is complete, cloudera will be available at [http://127.0.0.1:7180/](http://127.0.0.1:7180/)

## Adding the nodes
The nodes can be added to cloudera by their hostname, a pattern can be used to find them all.

E.G.

		hadoop-node[1-node_count]

SSH details for logging into the nodes:

		Username: vagrant
		Password: vagrant
