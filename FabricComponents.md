<div align="center" style="padding: 24px; border: 1px solid #e5e7eb; border-radius: 16px; background: linear-gradient(180deg,#ffffff, #f8fafc);">
  <h1 style="margin: 0; font-size: 36px; line-height: 1.2;">Hyperledger Fabric — Components Guide</h1>
  <p style="margin: 8px 0 0; font-size: 16px; color: #475569;">A detailed overview of the core building blocks of Hyperledger Fabric</p>
</div>

---

## 📘 Overview

Hyperledger Fabric is a **permissioned blockchain framework** with a modular architecture. This document provides an overview of its key components, their roles, and how they interact in a Fabric network.

---

## 🧩 Core Components

### 1. Peers

Peers are the **fundamental units** of a Fabric network. They host ledgers, execute chaincode, and handle transaction proposals.

- **Ledger:**

  - **Blockchain:** Immutable chain of blocks storing transactions.
  - **World State:** Latest key-value data (stored in LevelDB or CouchDB).

- **Endorsing Peer:**

  - Simulates transactions using chaincode.
  - Produces endorsements (signatures).
  - Returns read-set and write-set.
  - Example: Transfer 100 tokens (simulation only, no permanent changes yet).

- **Committing Peer:** Validates and commits ordered transactions to the ledger.

- **Anchor Peer:** Communicates across organizations for cross-org communication.

---

### 2. Ordering Service (Orderer)

Responsible for ordering transactions into blocks and delivering them to peers.

- **Consensus:** Ensures all peers have the same transaction order.
- **Mechanisms:** Supports Raft (production) and Solo (development).

---

### 3. Chaincode (Smart Contracts)

Chaincode defines **business logic** for processing transactions.

- Written in Go, Java, or Node.js.
- Executes on peers to simulate transactions.
- **Fabric v2.x Lifecycle:** Decentralized approval & commit by organizations.

---

### 4. Membership Service Provider (MSP)

Manages **identities and roles** of network participants.

- Uses **X.509 certificates** issued by a CA.
- **Local MSP:** Identity of peers/orderers/clients.
- **Channel MSP:** Defines access control on a channel.

---

### 5. Certificate Authority (CA)

Issues and manages certificates for participants.

- **Fabric CA:** Built-in CA service.
- **Alternative:** External CAs (OpenSSL, commercial providers).

---

### 6. Channels

Provide **data privacy and isolation** between different sets of participants.

- Each channel has its own ledger.
- **Private Data Collections:** Subset of organizations share private data.

---

### 7. Clients

External applications that interact with the Fabric network.

- Submit proposals → Collect endorsements → Send to orderer.
- SDKs available: JavaScript, Go, Java.

---

### 8. Consensus

Agreement process for transaction order and correctness.

- **Endorsement Policy:** Defines required endorsers.
- **Validation:** Committing peers verify policies before committing.
- **Protocols:** Raft, Kafka (pluggable consensus).

---

### 9. Policies

Govern network rules:

- **Channel Policies:** Who can read/write.
- **Endorsement Policies:** Whose signatures are required for validity.

---

### 🔑 10. Fabric State Database

Stores ledger world state as a key-value database.

- **LevelDB:** Default, embedded.
- **CouchDB:** Rich JSON query support.

---

### 11. Events

Enable event-driven interactions.

- Clients subscribe to block/transaction events.
- Useful for notifying applications/services.

---

### 12. Hyperledger Fabric CLI

Command-line tool for managing the Fabric network:

- Start/stop network
- Query ledger
- Invoke chaincode
