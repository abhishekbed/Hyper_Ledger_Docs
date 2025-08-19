# 🚀 Hyperledger Fabric Guide

## 📌 What is Hyperledger?

Hyperledger is a **private permissioned blockchain framework** for enterprises.  
Unlike public blockchains (Bitcoin, Ethereum, Solana), Hyperledger networks are **restricted** — only authorized members can join via **permissions**.

---

## ❓ Why Hyperledger?

### Issues in Public Blockchains:

- 🔓 **Confidentiality**: Every node can read all transactions.
- 🐢 **Performance**: Block validation requires global consensus.
- 📈 **Scalability**: Limited TPS in public networks.

### Hyperledger Fixes:

- ✅ Privacy via **permissioned access**
- ✅ Faster consensus (Raft, Kafka, etc.)
- ✅ Modular + scalable architecture

---

## 🔑 Hyperledger Fabric

Fabric is the most widely used Hyperledger project.

### Advantages

- 🔗 **Modular** – plug & play components
- 📡 **Scalable** – suited for enterprises
- 🔒 **Secure** – identity-based membership

### Key Features

- **Chaincode** → Smart contracts (Go, Node.js, Java)
- **MSP** → Membership Service Provider (identity/authentication)
- **Channel** → Private communication among orgs
- **ACL** → Access Control Lists for restricting permissions

---

## 🖥️ Types of Nodes

- **Committing Nodes** → Maintain ledger copies
- **Endorsing Nodes** → Execute chaincode
- **Ordering Nodes** → Order transactions into blocks

---

## 🔄 Transaction Flow

1. **Client initiates** → Authenticated via **MSP + ACL**
2. **Proposal sent** → Endorsing nodes simulate chaincode
3. **Endorsements collected** → Client verifies results
4. **Orderer** → Sequences transactions, creates block
5. **Peers validate & commit** → Ledger updated

---

## ⚙️ Prerequisites Setup

Install the following:

```bash
sudo apt-get install curl git python libltdl-dev
sudo apt-get install nodejs
sudo apt-get install docker-ce docker-compose
```

Verify:

```bash
curl --version
node --version
git --version
python --version
docker --version
docker-compose version
```

---

## 🔧 Hyperledger Fabric Installation

Download binaries & samples:

```bash
curl -sSL https://bit.ly/2ysbOFE | bash -s
```

Fix Docker socket issue:

```bash
sudo chmod 666 /var/run/docker.sock
```

---

## 🧪 Test Network

### Start network:

```bash
cd fabric-samples/test-network
./network.sh up
```

Check running containers:

```bash
docker ps
```

### Create a channel:

```bash
./network.sh createChannel -c testchannel
```

### Stop network:

```bash
./network.sh down
```

---

## 📦 Deploy First Application

```bash
./network.sh down
./network.sh up createChannel -c mychannel -ca
./network.sh deployCC -ccn basic -ccp ../asset-transfer-basic/chaincode-javascript/ -ccl javascript
```

Run app:

```bash
cd asset-transfer-basic/application-javascript
npm install
node app.js
```

---

## 🏢 Adding a New Organization

Steps to add **Org3**:

1. Generate crypto material (`cryptogen`)
2. Create Org3 definition (`configtxgen`)
3. Start Org3 peer containers
4. Update channel config (`configtxlator + jq`)
5. Peers join channel & approve chaincode

---

## 🏗️ Important Concepts

### 🔹 Genesis Block

- First block of every channel
- Defines **orgs, policies, consortium info**
- Required for peers & orderers to join

### 🔹 Anchor Peers

- Act as **contact points** between orgs
- Enable **gossip protocol** for data sync
- Needed for **cross-org communication**

### 🔹 System Channel

- Used in **Fabric v1.x – v2.2** for managing new channels
- Replaced in newer Fabric with **channel participation API**

---

## 📜 Useful Commands

```bash
peer channel list
peer channel fetch config channel-artifacts/config_block.pb ...
peer channel update -f org3_update_in_envelope.pb -c channel1 ...
peer lifecycle chaincode package ...
peer lifecycle chaincode install ...
peer lifecycle chaincode approveformyorg ...
peer lifecycle chaincode querycommitted ...
```

---

## 📚 Networks

- **Enterprise Network** → Production setup
- **Test Network** → Development/testing

---

# ✅ Conclusion

Hyperledger Fabric provides a **modular, permissioned, scalable blockchain** for enterprises.
