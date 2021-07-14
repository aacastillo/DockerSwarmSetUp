# DockerSwarmSetUp
### Description
We are going to build a swarm cluster with one manager node and two worker nodes that all run Docker CE version `5:18.09.5~3-0~ubuntu-bionic`.

### Prerequisites
- You should have the three servers set up. You can do this either by setting up three cloud servers with a cloud provider or if you have a linuxacademy, or acloudguru account.


### Installation
**1. Install Docker CE on all three nodes**
  - `sudo apt-get update`
  - `sudo apt-get -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common`
  - `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
  - `sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`
  - `sudo apt-get update`
  - `sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic containerd.io`
  - verify installation with `docker version`
  - Add username to the Docker group so that you can run docker commands, `sudo usermode -a -G docker $username`
  - Log out and then log back into each server as new user


**2. Configure the swarm manager**
  - On master node run `docker swarm init --advertise-addr <swarm manager private IP>`


**3. join the worker nodes to the cluster**
  - get the join token from the swarm manager, `docker swarm join-token worker`
  - run join command with bash token from docker swarm manager initialization
  - Check the cluster nodes by listing nodes in the swarm manager, `docker node ls`
