<div align="center" style="padding: 24px; border: 1px solid #e5e7eb; border-radius: 16px; background: linear-gradient(180deg,#ffffff, #f8fafc);">
  <h1 style="margin: 0; font-size: 36px; line-height: 1.2;">Hyperledger Fabric — Setup & Quickstart Guide</h1>
  <p style="margin: 8px 0 0; font-size: 16px; color: #475569;">Step-by-step instructions to install prerequisites, launch a Fabric test network, deploy chaincode, and manage Docker resources</p>
</div>

---

## 📘 Overview

This README provides a **complete setup guide** for Hyperledger Fabric, including prerequisites, test network deployment, smart contract installation, and Docker management.

---

## ⚙️ Prerequisites Installation

### Curl

```bash
sudo apt-get install curl
curl --version
```

### Node.js

```bash
sudo apt-get update
sudo apt-get install nodejs
node --version
```

### Git

```bash
sudo apt-get install git
git --version
```

### Python

```bash
sudo apt-get install python
python --version
```

### Lib Tools

```bash
sudo apt-get install libltdl-dev
```

### Docker CE (Community Edition)

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
docker --version
```

### Docker Compose

```bash
sudo apt-get update
sudo apt-get install docker-compose-plugin
docker-compose version
```

---

## 🔧 Hyperledger Fabric Installation

### Step 1: Download and Setup Fabric

```bash
curl -sSL https://bit.ly/2ysbOFE | bash -s
```

> ⚠️ If you see `Got permission denied while trying to connect to the Docker daemon socket`, fix with:

```bash
sudo chmod 666 /var/run/docker.sock
```

---

## 🧪 Running Test Network

### Start Test Network

```bash
cd fabric-samples/test-network
sudo ./network.sh up
```

Check running containers:

```bash
sudo docker ps
```

Check channel list:

```bash
sudo docker exec peer0.org1.example.com peer channel list
```

### Create Channel

```bash
sudo ./network.sh createChannel -c testchannel
```

Verify:

```bash
sudo docker exec peer0.org1.example.com peer channel list
sudo docker exec peer0.org2.example.com peer channel list
```

### Stop Network

```bash
sudo ./network.sh down
```

---

## 🗄️ CouchDB Option

```bash
cd fabric-samples/test-network
sudo ./network.sh up -s couchdb
```

Stop network:

```bash
sudo ./network.sh down
```

---

## 🔑 CA Option

```bash
cd fabric-samples/test-network
sudo ./network.sh up -ca
```

Stop network:

```bash
sudo ./network.sh down
```

---

## 🌀 All-in-One Option

```bash
cd fabric-samples/test-network
sudo ./network.sh up -ca -s couchdb
```

Stop network:

```bash
sudo ./network.sh down
```

---

## 🚀 Launch the Blockchain Network

```bash
cd fabric-samples/test-network
./network.sh down
./network.sh up createChannel -c mychannel -ca
```

This launches:

- 2 peers
- Ordering service
- 3 Certificate Authorities

---

## 📦 Deploy a Smart Contract

```bash
./network.sh deployCC -ccn basic -ccp ../asset-transfer-basic/chaincode-javascript/ -ccl javascript
```

---

## 💻 Prepare the Application

```bash
cd asset-transfer-basic/application-gateway-javascript
npm install
node app.js
```

---

## 📥 Install NVM (Node Version Manager)

```bash
sudo apt update
sudo apt install curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
source ~/.bashrc
nvm --version
nvm install <node version>
```

---

## 📡 Create Channel

```bash
./network.sh up createChannel -c <channelName> -ca
```

---

## 🏢 Add New Organization

```bash
cd addOrg3
./addOrg3.sh up -c <channelName>
```

Set path for chaincode:

```bash
cd /test-network
export PATH=${PWD}/../bin:$PATH
export FABRIC_CFG_PATH=$PWD/../config/
peer version
peer lifecycle chaincode package basic.tar.gz --path ../asset-transfer-basic/chaincode-javascript/ --lang node --label basic_1.0
```

Install chaincode in org3:

```bash
export CORE_PEER_TLS_ENABLED=true
export CORE_PEER_LOCALMSPID="Org1MSP"
export CORE_PEER_TLS_ROOTCERT_FILE=${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt
export CORE_PEER_MSPCONFIGPATH=${PWD}/organizations/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp
export CORE_PEER_ADDRESS=localhost:7051

peer lifecycle chaincode install basic.tar.gz
```

---

## 🏗️ Steps to Create New Org

- Create crypto materials
- Generate definition
- Fetch channel config
- Create config update
- Sign config with org
- Run org3 container
- Join channel
- Check CouchDB
- Invoke transaction

---

## 🐳 Docker Management

Stop container:

```bash
docker stop <container_name_or_id>
```

Delete single container:

```bash
docker rm <container_name_or_id>
```

Delete all containers:

```bash
docker rm -f $(docker ps -aq)
```

Delete single image:

```bash
sudo docker rmi -f <image_name_or_id>
```

Delete all images:

```bash
sudo docker rmi -f $(docker images -a -q)
```

Show containers:

```bash
docker ps -a
```

Show running containers:

```bash
docker ps
```

Show images:

```bash
docker images
```

Delete stopped containers:

```bash
docker container prune
```

Delete unused images:

```bash
docker image prune
```
