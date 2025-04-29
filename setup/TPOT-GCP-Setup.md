# GCP VM Creation for T-Pot Honeypot

This document outlines the steps to create a virtual machine in Google Cloud Platform (GCP) for deploying the T-Pot honeypot system.

---

## 🖥️ VM Configuration

| Parameter       | Value                |
|----------------|----------------------|
| Machine Type    | `e2-standard-4` (4 vCPU, 16GB RAM) |
| Disk Type       | SSD (Balanced or Extreme)         |
| Disk Size       | 60 GB              |
| OS Image        | Ubuntu     |
| Firewall        | Allow HTTP and HTTPS |
| Region/Zone     | `us-central1-a` *(example)* |

---

## Create via GCP Console

1. Navigate to [GCP Compute Engine](https://console.cloud.google.com/compute/instances)
2. Click **"Create Instance"**
3. Set the following:
   - **Name**: `tpot-vm`
   - **Region / Zone**: Choose your preferred region (e.g., `us-central1-a`)
   - **Machine Type**: Select **E2 → `e2-standard-4`**
   - **Boot Disk**:
     - Click **"Change"**
     - Choose **Ubuntu **
     - Set **Disk Size** to `60 GB`
     - Set **Disk Type** to `SSD (pd-ssd)`
   - **Firewall**:
     - ✅ Check **Allow HTTP**
     - ✅ Check **Allow HTTPS**
4. Click **"Create"**

## 🚀 T-Pot Setup on GCP VM

This section documents the steps to install and configure T-Pot CE (Community Edition) on the GCP VM created earlier.

---

### 🛠️ Installation Steps

```bash
# Switch to root
sudo su

# Update and upgrade system packages
apt-get update && apt-get upgrade -y

# Install Git
apt install git -y

# Clone the T-Pot CE repository
git clone https://github.com/telekom-security/tpotce.git

# Navigate into the T-Pot directory
cd tpotce

# Make directory accessible (if permission denied later)
chmod o+rx /opt/tpot

# Start the installer
./install.sh


## Debugging T-Pot Service Issues
If tpot.service is not starting correctly or is stuck restarting:
# Watch T-Pot service status in real-time
watch -n 2 "systemctl status tpot.service"

# Inspect recent error logs
journalctl -u tpot -b --no-pager | grep "failed" | tail -n 50

Observe failed logs in my case few ports that are needed by Tpot are already in use, SO have updated the ports in cofig file of TPOT.
#Then
sudo systemctl restart tpot.service

## Setup fire wall rules
#Direction:
Ingress
#Source filters:
IP ranges
0.0.0.0/0
#Protocols and ports
tcp:22, 23, 80, 81, 135, 443, 445, 1433, 3306, 5432, 5900, 6379, 9200, 64295, 64297
udp:69, 623, 5000, 5060
