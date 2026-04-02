# 🔐 Zero Trust Home Lab Architecture

A modern Zero Trust network design for a homelab environment using Cloudflare Access, Tailscale, reverse proxying, and network segmentation.

---

## 📌 Overview

This environment is designed using a Zero Trust model:

- No direct inbound access from the internet
- Identity-aware access controls
- Segmented internal network
- Multiple secure access paths using Cloudflare and Tailscale

## 🖼 Architecture Diagram

                Internet
                    |
        +------------------------+
        |   Cloudflare (WAF)     |
        |   Zero Trust Access    |
        +-----------+------------+
                    |
                    v
        +------------------------+
        |   Cloudflare Tunnel    |
        +-----------+------------+
                    |
                    v
        +------------------------+
        |  Nginx Proxy Manager   |
        +-----------+------------+
                    |
     +--------------+--------------+
     |                             |
     v                             v
+-------------+              +--------------+
|   Web Apps  |              |   Services   |
| (Plex, etc) |              | (Internal)   |
+-------------+              +--------------+

        Private Access Layer
                    |
        +------------------------+
        |      Tailscale         |
        +-----------+------------+
                    |
                    v
              Trusted Devices

---

## 🌐 Access Model

### External Access

- Cloudflare Tunnel
- Cloudflare WAF
- Cloudflare Access (identity-aware authentication)

### Private Access

- Tailscale for internal access
- Trusted devices securely reach services without public exposure

---

## 🔒 Security Layers

### Perimeter

- Cloudflare WAF
- DDoS protection
- No open inbound ports (tunnel-based access)

### Identity

- Cloudflare Access (SSO / MFA)
- Device-based trust via Tailscale

### Network

- VLAN segmentation (UniFi):
  - Home
  - IoT
  - Guest
  - VPN
- Default deny between VLANs
- Restricted management access

### Application Layer

- Reverse proxy routing (Nginx Proxy Manager)
- Optional authentication layer (Authelia)

---

## 🔁 Traffic Flow

### External User

User → Cloudflare → Access Authentication → Reverse Proxy → Service

### Internal Trusted User

User → Tailscale → Internal Service

---

## 🛡 Design Principles

- Never expose services directly to the internet
- Require authentication before access
- Separate networks by trust level
- Use layered controls instead of a single boundary

---

## 📈 Future Improvements

- Add CrowdSec for adaptive blocking
- Add centralized logging and alerting
- Add service-level authentication
- Add policy-based device access controls

---

## 🧠 Design Decisions

- Cloudflare Tunnel eliminates the need for port forwarding
- Tailscale provides secure internal access without traditional VPN complexity
- Reverse proxy centralizes routing and certificate management
- VLAN segmentation reduces lateral movement risk
- Multiple access paths (Cloudflare + Tailscale) provide redundancy

---

## 🎯 Purpose

This project demonstrates a practical Zero Trust implementation in a homelab environment using modern access controls and segmentation principles.
