# 🏡 Homelab: Repurposed Gaming Rig Turned Virtualized Powerhouse

This homelab repurposes a high-end gaming PC into a flexible, virtualized environment running on **Proxmox VE**. It supports self-hosted cloud storage, smart home automation, ad-blocking, local AI experimentation, and more—all managed from one efficient system.

---

## 🖥️ Hardware Specs

<table>
  <tr>
    <td width="60%">

<b>Component</b> | <b>Description</b>
-- | --
<strong>CPU</strong> | Intel Core i7-8700K (6c/12t @ 3.7GHz)
<strong>Motherboard</strong> | ASUS ROG Strix Z370-E
<strong>RAM</strong> | 32GB G.Skill DDR4 @ 3200MHz
<strong>Boot Drive</strong> | 128GB Samsung MZNLF128 SSD (Proxmox host)
<strong>VM Storage</strong> | 512GB TEAM TM8PS7512 NVMe SSD
<strong>Network Card</strong> | iPolex 10GbE NIC (Intel X540-T2G chipset)
<strong>GPU (Passthrough)</strong> | EVGA RTX 3070
<strong>Wi-Fi</strong> | Eero 6 Mesh Network (Bridge/Pass-Through)
<strong>Switch</strong> | TRENDnet 6-Port 10G Switch (TEG-S762)

</td>
    <td width="40%">
      <img src="https://github.com/AdamHayball/HomeLab/blob/main/rack.png?raw=true" alt="Homelab Rack" width="100%"/>
    </td>
  </tr>
</table>

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
