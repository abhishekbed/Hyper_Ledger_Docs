<div align="center" style="padding: 24px; border: 1px solid #e5e7eb; border-radius: 16px; background: linear-gradient(180deg,#ffffff, #f8fafc);">
  <h1 style="margin: 0; font-size: 36px; line-height: 1.2;">Hyperledger Fabric — Org3 Cryptographic Material</h1>
  <p style="margin: 8px 0 0; font-size: 16px; color: #475569;">Step-by-step instructions to generate certificates and keys for a new organization (Org3)</p>
</div>

---

## 🔐 Generate Cryptographic Material

### Step 1: Create `crypto-config.yaml`

Open a text editor and create a new file named **crypto-config.yaml** with the following content:

```yaml
OrdererOrgs:
  - Name: Orderer
    Domain: example.com
    Specs:
      - Hostname: orderer

PeerOrgs:
  - Name: Org3
    Domain: org3.example.com
    EnableNodeOUs: true
    Template:
      Count: 2
    Users:
      Count: 1
```

**Explanation:**

- **OrdererOrgs** → Defines the ordering service organization `example.com` with one orderer node.
- **PeerOrgs** → Defines **Org3** with:

  - **2 peer nodes** (`Count: 2`)
  - **1 user** (`Count: 1`)
  - **EnableNodeOUs: true** → Enables organizational unit identification for roles (peer, client, admin, orderer).

---

### Step 2: Run `cryptogen`

Execute the following command to generate the cryptographic material:

```bash
cryptogen generate --config=crypto-config.yaml
```

This will generate:

- **MSP directories** for Org3
- Certificates and keys for:

  - Peers
  - Org3 Admin and User
  - CA (Certificate Authority)

---

### Step 3: Verify Output

After running the command, a **crypto-config/** folder will be created in your working directory.

Inside, you should see:

- `ordererOrganizations/example.com/` → Orderer certificates and MSP.
- `peerOrganizations/org3.example.com/` → Org3 peers, users, and CA certificates.
