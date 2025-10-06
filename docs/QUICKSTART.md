# quieo Quick Start Guide

## 🚀 One-Command Demo

```bash
# Complete setup and demo (Windows)
setup.bat

# Complete setup and demo (Linux/Mac)
./setup.sh

# Run automated 2-4 minute demo
python3 demo.py
```

## 🏃 Manual Quick Start

### 1. Prerequisites Check
- ✅ Docker & Docker Compose
- ✅ Node.js 16+
- ✅ Python 3.9+
- ⚠️ Rust (optional, for performance)

### 2. Start Services
```bash
docker-compose up -d
```

### 3. Run Demo Clients

**Terminal 1 - Sakshi (Sender):**
```bash
cd sender && npm install
npm start login        # sakshi/sakshi123
npm start compose      # Send Level-2 message to aryan
```

**Terminal 2 - Aryan (Receiver):**
```bash
cd receiver && npm install
npm start login        # aryan/bob123
npm start fetch        # Decrypt message (shows QKD badge)
```

**Terminal 3 - Security Demo:**
```bash
python3 spoof/spoof.py  # Triggers self-destruct
```

**Desktop UI (Nextron):**
```bash
cd ui-app && npm install
npm run dev               # Launch Nextron development mode

# Or use quickstart script:
./quickstart.sh          # Linux/Mac
quickstart.bat           # Windows

# Or launch with full demo:
python3 demo.py --launch-ui
```

## 🎯 Demo Scenarios

### Scenario 1: Quantum-Aided AES (Level 2)
- Login as sakshi → Compose → Level 2 → Send to aryan
- Login as aryan → Fetch → See "QKD-Secured" badge
- Run spoof script → Key revoked → Message unreadable

### Scenario 2: Post-Quantum Crypto (Level 3)  
- Login as sakshi → Compose → Level 3 → Send to aryan
- Check console for "PQC: Key encapsulation" logs
- Demonstrates Rust crypto module USP

### Scenario 3: Self-Destruct Demo
- Send any message → Note key ID
- Run `python3 spoof/spoof.py --key-id <KEY_ID>`
- Try to decrypt → Shows "Message destroyed"

## 📊 Service URLs
- **Gateway API**: http://localhost:8000
- **Health Check**: http://localhost:8000/health  
- **MailHog UI**: http://localhost:8025
- **API Docs**: http://localhost:8000/docs

## 🔐 Demo Accounts
- **sakshi**: sakshi123 (Sender)
- **aryan**: bob123 (Receiver)
- **admin**: admin123 (Admin access)

## ⚡ Troubleshooting

**Services not starting:**
```bash
docker-compose logs
docker-compose down && docker-compose up -d
```

**Connection errors:**
```bash
curl http://localhost:8000/health
```

**Rust build issues:**
```bash
cd crypto_rust
python3 -m pip install maturin[patchelf]
python3 build.py
```

## 🏗️ Architecture Summary

```
┌─────────────────┐    ┌─────────────────┐
│   Desktop UI    │    │   CLI Clients   │
│   (Nextron)     │    │ (Node.js/npm)   │
└─────────────────┘    └─────────────────┘
         │                       │
         └───────────────────────┼────────────────┐
                                 │                │
                    ┌─────────────────┐          │
                    │   API Gateway   │          │
                    │   (FastAPI)     │          │
                    └─────────────────┘          │
                             │                   │
         ┌───────────────────┼───────────────────┘
         │                   │
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│      KMS        │ │   QKD Simulator │ │ Crypto Engine   │
│   (FastAPI)     │ │   (FastAPI)     │ │    (Rust)       │
└─────────────────┘ └─────────────────┘ └─────────────────┘
         │
┌─────────────────┐
│     Redis       │
│ (Key Storage)   │
└─────────────────┘
```

## 🎬 Demo Script (2-4 minutes)

1. **[30s]** Start services: `docker-compose up -d`
2. **[30s]** Login sakshi: `cd sender && npm start login`
3. **[60s]** Send Level-2 message: `npm start compose`
4. **[30s]** Login aryan: `cd receiver && npm start login` 
5. **[30s]** Decrypt message: `npm start fetch` (show QKD badge)
6. **[60s]** Run attack: `python3 spoof/spoof.py` (show revocation)
7. **[30s]** Show Level-3 PQC: Check Rust logs

**Total: ~4 minutes**

---

**Ready for Monday Demo! 🚀**