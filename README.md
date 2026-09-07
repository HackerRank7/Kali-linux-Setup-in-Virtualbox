# Kali Linux 2026.2 Setup on VirtualBox

This repository documents the complete process of installing and configuring **Kali Linux 2026.2** on **Oracle VirtualBox** in a secure NAT network environment.

## Prerequisites

Before starting, download and install the following tools on your Windows system:

1. **7-Zip** – File extraction utility
2. **Oracle VirtualBox** – Virtualization software
3. **Kali Linux 2026.2 VirtualBox Image**

---<img width="703" height="226" alt="Capture12" src="https://github.com/user-attachments/assets/0920314f-1b5d-45cd-8eab-21f0bf1f699f" />


## Step 1: Extract Kali Linux Image

1. Locate the downloaded file:

   ```
   kali-linux-2026.2-virtualbox-amd64.7z
   ```
2. Right-click the file and extract it using **7-Zip**.
3. Wait until the extraction process completes.

---

## Step 2: Configure VirtualBox NAT Network

1. Open **VirtualBox**.

2. Navigate to:

   ```
   File → Tools → Network
   ```

3. Select **NAT Networks**.

4. Create or edit a NAT network with the following settings:

   ```
   Name: NatNetwork
   IPv4 Prefix: 10.0.0.0/24
   ```
<img width="1366" height="721" alt="Capture1" src="https://github.com/user-attachments/assets/688946a4-b40c-4dcb-a1e4-9c42942ebe08" />

5. Click **Apply** and close the Network Manager.

---


## Step 3: Import Kali Linux Virtual Machine

1. Open VirtualBox.

2. Click:

   ```
   Machine → Add/Open
   ```

3. Browse to the extracted Kali Linux folder.

4. Select the Kali Linux virtual machine file.
<img width="1061" height="554" alt="646988171-6d335d08-10c5-47aa-8965-8549cf63fc7f" src="https://github.com/user-attachments/assets/5172e972-dab3-438b-945b-e344fdb97ffd" />

5. Click **Open**.

The machine will now appear in VirtualBox.

---


## Step 4: Configure Virtual Machine Resources

Before starting the VM, adjust its hardware settings.

### Memory Allocation

1. Open **Settings**.

2. Switch from **Basic** to **Expert Mode** (if available).

3. Go to:

   ```
   System → Motherboard
   ```

4. Set:

   ```
   Base Memory: 4096 MB
   ```
<img width="903" height="611" alt="Capture3" src="https://github.com/user-attachments/assets/363f3d21-01e0-41d0-8be1-8182b9451e40" />


### Processor Allocation

1. Navigate to:

   ```
   System → Processor
   ```

2. Assign:

   ```
   CPU(s): 1
   ```
<img width="941" height="665" alt="Capture4" src="https://github.com/user-attachments/assets/531e2722-f532-4c38-93c2-f5a96ec43567" />

> Adjust memory and CPU allocation according to your system specifications.

---

## Step 5: Configure Network Adapter

Go to:

```
Settings → Network → Adapter 1
```

Configure the following:

```
Attached To: NAT Network
Name: NatNetwork
Promiscuous Mode: Allow All
```
<img width="949" height="696" alt="Capture5" src="https://github.com/user-attachments/assets/05c1a2a1-eed4-41d9-b78f-1e49f2a28ddc" />


Click **OK** to save the changes.

---


## Step 6: Start Kali Linux

1. Click **Start**.
2. Kali Linux will boot.
3. Log in using the default credentials:

   ```
   Username: kali
   Password: kali
   ```

<img width="633" height="377" alt="Capture 6JPG" src="https://github.com/user-attachments/assets/4116f383-5da0-4426-b997-a6825b366d15" />



## Step 7: Configure Network Settings Inside Kali

1. Click the network icon.

2. Select:

   ```
   Edit Connections
   ```
<img width="513" height="331" alt="Capture6" src="https://github.com/user-attachments/assets/42a39de1-bdee-43d0-acd4-3f0404b1e269" />


3. Open:

   ```
   Wired Connection 1
   ```

4. Click the settings icon.
<img width="727" height="491" alt="Capture7" src="https://github.com/user-attachments/assets/254fc662-8b32-46a4-8797-7efd8e5cc099" />

### IPv4 Configuration

Navigate to:

```
IPv4 Settings
```

Change:

```
Method: Automatic → Manual
```

Add the following:

```
Address: 10.0.0.3
Netmask: 24
Gateway: 10.0.0.1
DNS Server: 8.8.8.8
```
<img width="1223" height="693" alt="Capture9" src="https://github.com/user-attachments/assets/12ff60d3-e8d5-42ef-9545-7182e757c830" />

Click **Save**.

---

## Step 8: Refresh Network Configuration

Open Terminal and execute:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0

sudo nmcli connection down "Wired connection 1"

sudo nmcli connection up "Wired connection 1"
```

These commands reload the network configuration and help establish connectivity.

<img width="1350" height="650" alt="Capture10" src="https://github.com/user-attachments/assets/b99cd2e7-1e3b-4ff1-b7ac-90f00434996b" />


## Step 9: Verify Internet Connectivity

Test network access using:

```bash
ping google.com
```

If replies are received successfully, internet connectivity is working.

You can also verify connectivity by opening Firefox and browsing any website.

---
<img width="1352" height="656" alt="Capture11" src="https://github.com/user-attachments/assets/644f48a9-49b8-4e5d-ae6b-3c696fcaadd8" />

## Result

Kali Linux 2026.2 has been successfully installed and configured on Oracle VirtualBox using a NAT Network setup.

### Environment Summary

| Component               | Configuration     |
| ----------------------- | ----------------- |
| Virtualization Platform | Oracle VirtualBox |
| Operating System        | Kali Linux 2026.2 |
| Network Type            | NAT Network       |
| Network Range           | 10.0.0.0/24       |
| Kali IP Address         | 10.0.0.3          |
| Gateway                 | 10.0.0.1          |
| DNS Server              | 8.8.8.8           |

---

## Author

**Gaurav Bharti**

* GitHub: https://github.com/HackerRank7
* TryHackMe: https://tryhackme.com/p/gk143

---

⚠️ This setup is intended for cybersecurity learning, penetration testing labs, and ethical hacking practice in a controlled    environment.
