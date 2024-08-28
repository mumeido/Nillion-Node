# Nillion Network Node
# How to run Nillion Network Node

![1](https://raw.githubusercontent.com/mumeido/Nillion-Node/main/nillion_1.jpeg)


To learn more about Nillion Network, you can go here and read about their Blog [here](https://docs.nillion.com/).

[Nillion](https://nillion.com/) is a secure computation network that decentralizes trust for high value data in the same way that blockchains decentralized transactions. Nillion addresses these challenges by leveraging privacy enhancing technologies (PETs) including Multi-Party Computation (MPC). These PETs enable users to securely store high value data on Nillion's peer-to-peer network of nodes, and allow for computations to be executed on the masked data itself. This eliminates the traditional need to decrypt data ahead of computation, enhancing the high value data's security.


## Step 1: Update System

### Update System
```bash
sudo apt update && sudo apt upgrade -y
```
### Install Prerequisites & Docker
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```
If the response is “Docker not found” then go to [Docker](https://www.docker.com/products/docker-desktop/) for setting it up on your device.

## Step 2: Verify Docker Installation

### Verify Docker Installation
```bash
docker --version
```

## Step 3: Download accuser Image

```bash
docker pull nillion/retailtoken-accuser:v1.0.0
```
## Step 4: Create accuser directory

```bash
mkdir -p nillion/accuser
```
## Step 5: Run the container to initialise accuser & register

```bash
docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
```

This will link your Kepler wallet, produce the information required to register the accuser on the website, and register them below:
- accound_id: Nillion address of the accuser
- public_key: Public Key of the accuser
![2](https://raw.githubusercontent.com/mumeido/Nillion-Node/main/Nillion_2.PNG)

## Step 6: Funding the accuser
To file accusations on Nilchain, you must first fund the accuser account with NIL. You can obtain this from the Nillion [faucet](https://faucet.testnet.nillion.com/)

## Step 7: Running the accuser

```bash
docker run -d -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "http://51.89.195.146:26657" --block-start 5040477
```
To get the block height right before your registered verifier, change the --block-start value. The block height where your validator was registered may be found by looking up the transaction hash of type "Pay For" on the blockchain explorer after checking the address you used to register your verifier on your linked Keplr wallet. You can get your tx via explorer from [NodesGuru](https://testnet.nillion.explorers.guru/)

## Step 8: Check verifier logs

```bash
# List Available Docker Container
docker ps

# Display logs
docker logs -f <container-id>
```

Wait until it synchronizes with the current block height. Once it does, you should see if the status shows "Registered" as true.







