# Notes on Secure Communication & VoIP (Preliminary Study)

## 1. Pre-meeting background study

### TLS 1.3
**Transport Layer Security (current standard).**
- Enforces **Perfect Forward Secrecy (PFS)** by design.
- Achieves a **1-RTT handshake**, improving performance compared to earlier versions.

### Perfect Forward Secrecy (PFS)
- Security property mandated by TLS 1.3.
- Compromise of the server’s long-term private key does **not** enable decryption of previously recorded traffic.

### 0-RTT
**Zero Round-Trip Time resumption.**
- Enables faster reconnections for returning clients.
- Trade-off: introduces **replay attack** risks.

### QUIC
**Quick UDP Internet Connections (used by HTTP/3).**
- Built on **UDP** instead of TCP.
- Integrates **TLS 1.3 natively**, reducing handshake latency.

---

## 2. Post-Quantum Cryptography (PQC)

### Motivation
- Classical public-key schemes (RSA, Diffie–Hellman) are vulnerable to large-scale quantum attacks.
- PQC aims to remain secure under quantum adversaries.

### KEM (Key Encapsulation Mechanism)
- A public-key primitive specialized for **secure symmetric key agreement**.
- Well-suited to replacing classical key exchange mechanisms.

### ML-KEM
**Module-Lattice-Based Key Encapsulation Mechanism.**
- NIST-selected standard candidate to replace RSA/DH in key exchange.
- Based on lattice problems believed to be quantum-resistant.

### MLWE (Module Learning With Errors)
- Underlying hardness assumption for ML-KEM.

### Formulation:

As + e = b \pmod{q}
s: secret vector

e: small random error vector

A, b: public

- Coefficients of s and e are small relative to modulus q.

### Security intuition:

- The presence of the small error e prevents recovery of s.

- Standard linear algebra techniques amplify noise.

- The problem reduces to variants of the Shortest Vector Problem (SVP) in high-dimensional lattices, believed to be computationally intractable.

---

## 3. Study after receiving links (VoIP focus)

---

## VoIP architecture overview

### RTP (Real-Time Transport Protocol)

**Purpose: Transport of actual audio data.**

###Process:

### Digitization

- Voice sampled (typically 8 kHz) and encoded using codecs.

### Packetization

- Encoded data wrapped into RTP packets.

### Key properties:

- Sequence numbers: allow reordering of packets.

- Timestamps: ensure correct playback timing and mitigate jitter.

- UDP-based: prioritizes low latency over guaranteed delivery.

---

###SIP (Session Initiation Protocol)

**Purpose: Call signaling and management.**

- Does not carry voice data.

- Handles setup, modification, and teardown of sessions.

### Typical usage:

- Registration: device informs server of its IP address.

- Call setup: INVITE → 200 OK.

- Session modification: e.g., voice → video.

- Termination: BYE message.

---

## 4. GSM modules in VoIP systems

**Purpose: Bridging IP-based VoIP systems with cellular networks.**

- Hardware modules containing SIM cards.

- Enable VoIP systems to place and receive calls via GSM networks.

### Use cases:

- Least Cost Routing (LCR) >> Routing calls through local SIMs to reduce landline-to-mobile costs.

- Redundancy / failover >> GSM acts as backup if the ISP connection fails.

- SMS integration >> Sending and receiving SMS through the VoIP system.

6. Next step

Study: “M-Payments: Issues and Concepts” paper
