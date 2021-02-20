![alt text](https://avatars.githubusercontent.com/u/50934298?s=200&v=4)

# Meter WarringStakes Node (ubuntu 18.04)
## Setting up Docker  
*(This setup can be done on a **user**. To get started, create a user first.)*  

`sudo apt-get update`  
`sudo apt-get install curl apt-transport-https ca-certificates software-properties-common`  
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`  
`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`  
`sudo apt update`  
`apt-cache policy docker-ce`  
`sudo apt install docker-ce`  
`sudo chmod 666 /var/run/docker.sock`  

## Download the latest desktop wallet
https://www.meter.io/wallets/

## Setting up a full node
`mkdir meter-data`  
`cd meter-data`  
`echo "export METER_DATA_PATH=$PWD" >> ~/.bashrc`  
`source ~/.bashrc`  
`docker pull dfinlab/meter-allin:latest`  
`docker run --network host --name meter --restart always -e NETWORK="warringstakes" -v $METER_DATA_PATH:/pos -d dfinlab/meter-allin:latest`  
`docker container start meter`  

## Setting up automatic update for Meter Docker images
`docker run -d --name watchtower --restart always -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --include-stopped --revive-stopped --enable-lifecycle-hooks --interval 10 --cleanup meter`  

## Get in to Meter Docker image  
`docker container exec -it meter bash`  
