# 🔐 Zero Trust Home Lab Architecture

A modern Zero Trust network design for a homelab environment using Cloudflare Access, Tailscale, reverse proxying, and network segmentation.

---

## 📌 Overview

This environment is designed using a Zero Trust model:

- No direct inbound access from the internet
- Identity-aware access controls
- Segmented internal network
- Multiple secure access paths using Cloudflare and Tailscale

---

## 🖼 Architecture Diagram

```text
                Internet
                    |
        +------------------------+
        |   Cloudflare (WAF)     |
        |   Zero Trust Access    |
        +-----------+------------+
                    |
                    v
        +------------------------+
        |  Nginx Proxy Manager   |
        |    Reverse Proxy       |
        +-----------+------------+
                    |
     +--------------+--------------+
     |                             |
     v                             v
+-----------+               +--------------+
| Web Apps  |               | Internal App |
| Services  |               | Services     |
+-----------+               +--------------+

        Private Access Layer
                    |
        +------------------------+
        |      Tailscale         |
        |   Private Overlay VPN  |
        +-----------+------------+
                    |
                    v
              Trusted Devices


🌐 Access Model
External Access
Cloudflare Tunnel
Cloudflare WAF
Cloudflare Access for identity-aware authentication
Private Access
Tailscale for private internal access
Trusted devices can securely reach internal services without exposing them publicly
🔒 Security Layers
Perimeter Security
Cloudflare WAF
DDoS protection
Protected DNS exposure
Identity and Access
Cloudflare Access
Tailscale device trust
Authentication before service access
Network Segmentation
Trusted network
IoT network
Guest network
Default deny between VLANs
🔁 Traffic Flow
External User

User → Cloudflare → Access Authentication → Reverse Proxy → Service

Internal Trusted User

User → Tailscale → Internal Service

🛡 Design Principles
Never expose services directly to the internet
Require authentication before access
Separate networks by trust level
Use layered controls instead of relying on a single boundary
📈 Future Improvements
Add CrowdSec for adaptive blocking
Add centralized logging and alerting
Add service-level authentication
Add policy-based device access controls
🎯 Purpose

This project demonstrates a practical Zero Trust implementation in a homelab environment using modern access controls and segmentation principles.

