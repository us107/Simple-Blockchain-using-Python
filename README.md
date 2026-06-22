# 🔗 Python Blockchain

A minimal, educational blockchain implementation built with Python and Flask. This project demonstrates the core concepts of a blockchain — proof of work, transaction handling, block mining, and a decentralized consensus mechanism — exposed via a simple REST API.

---

## Features

- **Block Mining** — Proof-of-Work algorithm that finds a valid hash with 4 leading zeroes
- **Transactions** — Create and record sender/recipient/amount transactions
- **Consensus Algorithm** — Resolves chain conflicts across nodes by adopting the longest valid chain
- **Node Registration** — Connect multiple nodes to form a peer-to-peer network
- **SHA-256 Hashing** — Cryptographically secure block hashing
- **REST API** — Interact with the blockchain entirely over HTTP

---

## Requirements

- Python 3.7+
- pip

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-username/python-blockchain.git
cd python-blockchain
```

### 2. Install dependencies

```bash
pip install flask requests
```

### 3. Run the node

```bash
python blockchain.py
```

By default, the server starts on port **5000**. To run on a different port:

```bash
python blockchain.py -p 5001
```

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | List all available endpoints |
| `GET` | `/mine` | Mine a new block |
| `POST` | `/transactions/new` | Submit a new transaction |
| `GET` | `/chain` | Return the full blockchain |
| `POST` | `/nodes/register` | Register new peer nodes |
| `GET` | `/nodes/resolve` | Run the consensus algorithm |

---

## Usage Examples

### Mine a new block

```bash
curl http://localhost:5000/mine
```

### Create a new transaction

```bash
curl -X POST http://localhost:5000/transactions/new \
  -H "Content-Type: application/json" \
  -d '{"sender": "alice", "recipient": "bob", "amount": 10}'
```

### View the full chain

```bash
curl http://localhost:5000/chain
```

### Register peer nodes

```bash
curl -X POST http://localhost:5000/nodes/register \
  -H "Content-Type: application/json" \
  -d '{"nodes": ["http://localhost:5001"]}'
```

### Resolve conflicts (consensus)

```bash
curl http://localhost:5000/nodes/resolve
```

---

## Running Multiple Nodes

To simulate a decentralized network, open multiple terminals and run nodes on different ports:

```bash
# Terminal 1
python blockchain.py -p 5000

# Terminal 2
python blockchain.py -p 5001
```

Then register the nodes with each other and use `/nodes/resolve` to sync chains.

---

## How It Works

1. **Genesis Block** — Created automatically on startup with a hardcoded proof and previous hash.
2. **Transactions** — Stored in a pool until the next block is mined.
3. **Mining** — The Proof-of-Work algorithm increments a `proof` number until `SHA-256(last_proof + proof + last_hash)` starts with `"0000"`.
4. **Consensus** — Each node can query its peers, validate their chains, and adopt the longest valid one.

---

## Project Structure

```
blockchain.py   # Core blockchain logic + Flask API server
README.md
```

---

## License

MIT
