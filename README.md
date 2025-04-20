# 🏡 Homelab: Repurposed Gaming Rig Turned Virtualized Powerhouse

This homelab repurposes a high-end gaming PC into a flexible, virtualized environment running on **Proxmox VE**. It supports self-hosted cloud storage, smart home automation, ad-blocking, local AI experimentation, and more—all managed from one efficient system.

---

## 🖥️ Hardware Specs

<div style="display: flex; align-items: flex-start; gap: 2rem;">

<table>
  <tr><th>Component</th><th>Description</th></tr>
  <tr><td><strong>CPU</strong></td><td>Intel Core i7-8700K (6c/12t @ 3.7GHz)</td></tr>
  <tr><td><strong>Motherboard</strong></td><td>ASUS ROG Strix Z370-E</td></tr>
  <tr><td><strong>RAM</strong></td><td>32GB G.Skill DDR4 @ 3200MHz</td></tr>
  <tr><td><strong>Boot Drive</strong></td><td>128GB Samsung MZNLF128 SSD (Proxmox host)</td></tr>
  <tr><td><strong>VM Storage</strong></td><td>512GB TEAM TM8PS7512 NVMe SSD</td></tr>
  <tr><td><strong>Network Card</strong></td><td>iPolex 10GbE NIC (Intel X540-T2G chipset)</td></tr>
  <tr><td><strong>GPU (Passthrough)</strong></td><td>EVGA RTX 3070</td></tr>
  <tr><td><strong>Wi-Fi</strong></td><td>Eero 6 Mesh Network (Bridge/Pass-Through)</td></tr>
  <tr><td><strong>Switch</strong></td><td>TRENDnet 6-Port 10G Switch (TEG-S762)</td></tr>
</table>

<img src="https://github.com/AdamHayball/HomeLab/blob/main/rack.png?raw=true" alt="Homelab Rack" width="350"/>

</div>
---

## 🖧 Virtualization Stack

Hosted on **Proxmox VE**, with a mix of full VMs and lightweight LXC containers:

### 🔐 Networking & Security
- **pfSense** *(VM)* – Main router and firewall
- **Pi-hole** *(LXC)* – DNS-level ad-blocking

### ☁️ Cloud & Storage
- **Nextcloud** *(LXC)* – Self-hosted file sync & cloud platform

### 🏠 Home Automation
- **Home Assistant** *(VM)* – Controls and automates smart devices

### 📡 Test Environment
- **MikroTik CHR** *(VM)* – Virtual router used for config testing

### 🎬 Media & Services
- **Ubuntu Server 24.04** *(VM)* – Hosts:
  - **Jellyfin** (media server)
  - **CUPS** (print server)
  - **Ollama** (local AI inference with GPU passthrough)

---

## 🛜 Network Topology

```plaintext
                       [Internet]
                           │
                        [Modem]
                           │
                     [pfSense VM]
                           │
              ┌────────────┴────────────┐
              │                         │
      [Eero 6 Mesh WiFi]       [TRENDnet TEG-S762]
              │                         │
              │                         ├── [Proxmox Host]
              │                         │      ├─ Pi-hole (LXC)
              │                         │      ├─ Nextcloud (LXC)
              │                         │      ├─ Home Assistant (VM)
              │                         │      ├─ Ubuntu: Jellyfin, CUPS, Ollama (VM)
              │                         │      └─ MikroTik CHR (VM)
              │                         ├── [Other Wired Devices / Projects]
              │                         └── [NAS / Backups]
```

---

## 🎯 Goals of This Homelab

- Learn and experiment with advanced networking (routing, VLANs, firewall rules)
- Replace third-party cloud services with self-hosted alternatives
- Host local-first AI/ML services and media streaming
- Test virtualized networking equipment in a safe sandbox
- Automate and secure the home environment

---

## 💡 Future Plans

- Enable ZFS on storage for snapshots and redundancy
- Add Docker or more LXC containers for microservices
- Implement a full monitoring stack (Grafana, Prometheus, Node Exporter)
- Secure services with HTTPS via NGINX reverse proxy
- Introduce CI/CD pipelines using Gitea + Drone or similar

---

## 🧠 Notes

- LXC containers reduce overhead and boot quickly
- GPU passthrough enables fast media encoding and AI inference
- Proxmox host backups go to an external NAS over NFS
- Autostart order ensures pfSense and Pi-hole come up first on boot
