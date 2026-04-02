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
