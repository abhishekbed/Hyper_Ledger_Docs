<div align="center" style="padding: 24px; border: 1px solid #e5e7eb; border-radius: 16px; background: linear-gradient(180deg,#ffffff, #f8fafc);">
  <h1 style="margin: 0; font-size: 36px; line-height: 1.2;">Hyperledger Fabric Binaries</h1>
  <p style="margin: 8px 0 0; font-size: 16px; color: #475569;">Executable tools to stand up, operate, and manage a Fabric network</p>

</div>

---

## 📘 Overview

**Fabric binaries** are the command‑line executables and helper tools used to interact with and administer a **Hyperledger Fabric** network. They enable you to:

- Manage network components
- Deploy and operate chaincode (smart contracts)
- Perform administrative and lifecycle tasks

> ⚠️ **Note:** Some commands and flags may vary slightly by Fabric version. Always check the docs for your exact release.

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Core Binaries](#-core-binaries)

  - [`peer`](#peer)
  - [`orderer`](#orderer)
  - [`chaincode`](#chaincode)
  - [`configtxgen`](#configtxgen)
  - [`cryptogen`](#cryptogen)

- [Common Commands](#-common-commands)
- [Cheatsheet](#-cheatsheet)
- [Tips](#-tips)

---

## 🧰 Core Binaries

### `peer`

**Purpose:** Manage the lifecycle and operations of **peer nodes**.

Peers endorse and commit transactions, store ledger data, and gossip with other peers.

**Typical uses:**

- Start/stop a peer process
- Install/approve/commit chaincode via lifecycle
- Query the ledger and chaincode

### `orderer`

**Purpose:** Run and configure the **ordering service**.

The orderer sequences transactions into blocks and reliably delivers them to peers.

**Typical uses:**

- Start an orderer node
- Manage ordering service configuration

### `chaincode`

**Purpose:** Developer‑focused helper for building and invoking **chaincode** (smart contracts).

**Typical uses:**

- Package, install, and interact with chaincode
- Support local dev/test loops

### `configtxgen`

**Purpose:** Generate network and channel **configuration artifacts**, including genesis blocks and channel creation transactions.

**Typical uses:**

- Create genesis block for ordering service
- Create channel config transactions

### `cryptogen`

**Purpose:** Generate **cryptographic material** (certificates, MSPs, keys) for organizations, peers, and orderers in dev/test scenarios.

> 📝 For production, consider using a proper CA (e.g., `fabric-ca`) instead of `cryptogen`.

---

## 🧪 Common Commands

```bash
# Start a peer node
./peer node start
```

```bash
# Install chaincode (lifecycle)
./peer lifecycle chaincode install <chaincode-package>
```

> Replace `<chaincode-package>` with the path to your packaged chaincode (e.g., `basic.tar.gz`).

---

## 🗂️ Cheatsheet

<table style="width: 100%; border-collapse: collapse;">
  <thead>
    <tr>
      <th align="left" style="padding: 12px; border-bottom: 1px solid #e5e7eb;">Binary</th>
      <th align="left" style="padding: 12px; border-bottom: 1px solid #e5e7eb;">What it does</th>
      <th align="left" style="padding: 12px; border-bottom: 1px solid #e5e7eb;">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>peer</code></td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;">Operate peers; lifecycle ops; query ledger</td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>./peer node start</code></td>
    </tr>
    <tr>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>orderer</code></td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;">Order transactions; deliver blocks</td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>./orderer</code></td>
    </tr>
    <tr>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>chaincode</code></td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;">Build & interact with smart contracts</td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>./peer lifecycle chaincode install ...</code></td>
    </tr>
    <tr>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>configtxgen</code></td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;">Generate channel & genesis artifacts</td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>./configtxgen -profile SampleDevModeGenesis -outputBlock genesis.block</code></td>
    </tr>
    <tr>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>cryptogen</code></td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;">Create MSPs, certs, and keys</td>
      <td style="padding: 12px; border-bottom: 1px solid #f1f5f9;"><code>./cryptogen generate --config=crypto-config.yaml</code></td>
    </tr>
  </tbody>
</table>

---

## 💡 Tips

- Keep environment variables like `FABRIC_CFG_PATH` and `CORE_PEER_*` organized via a shell script.
- For production deployments, prefer using **Fabric CA** over `cryptogen` for certificate management.
- Use distinct MSP IDs and namespaces per org; version your channel configuration artifacts.
- Always verify binary versions across nodes to avoid subtle incompatibilities.
