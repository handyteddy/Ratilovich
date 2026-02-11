---
layout: post
title: "Pivoting SQL Server Access Through SOCKS5 with Commando and Kali"
date: 2025-07-02 11:33:22 +0100
categories: [pentesting, socks5, sql-server, commando, kali]
excerpt: "Tunnelling Commando VM - Kali - Victim - Socks5 + Variations"
permalink: /:categories/tunelling/
---

🧠 **Scenario**

- 💻 **Kali VM**: Has VPN access to the internal network.
- 🛡️ **Commando VM**: Needs to reach SQL Server (10.10.110.58).
- 🗃️ **SQL Server**: Only reachable via VPN from Kali.
- 🎯 **Objective**: Route Commando's traffic (specifically TCP/1433) through Kali using SOCKS5.

---

🛠️ **Step 1: Setting up a SOCKS5 Proxy on Kali**

On Kali, I spun up a SOCKS5 proxy using SSH:

```bash
ssh -D 0.0.0.0:1080 -q -C -N kali@localhost
```

- `-D 0.0.0.0:1080`: Binds the SOCKS proxy to all interfaces
- `-q -C -N`: Quiet, compressed, no command shell

📸 **Screenshot Placeholder**: *Terminal showing SSH SOCKS proxy command running*

---

📡 **Step 2: Confirming the Proxy is Active**

To confirm it's listening:

```bash
sudo ss -tulnp | grep 1080
```

📸 **Screenshot Placeholder**: *Output showing ssh process listening on 0.0.0.0:1080*

---

⚙️ **Step 3: Configure Proxifier on Commando VM**

Installed [Proxifier](https://www.proxifier.com/) on Commando VM and added a proxy:

- 🏠 **Address**: Kali’s IP (e.g., 192.168.56.101)
- 🔌 **Port**: 1080
- 🔄 **Type**: SOCKS5

Then created a rule for traffic to SQL Server on port 1433.

📸 **Screenshot Placeholder**: *Proxifier rule setup with IP, port, and proxy settings*

---

📊 **Step 4: Confirming Proxy Traffic**

Once configured, the Proxifier dashboard showed traffic flowing through the SOCKS5 proxy.

📸 **Screenshot Placeholder**: *Proxifier stats with data on proxy traffic*

---

🧪 **Step 5: PowerUpSQL to Test SQL Access**

From Commando VM, I used PowerUpSQL to query the SQL Server:

```powershell
Invoke-SQLQuery -SQLServer "10.10.110.58" -Username "sa" -Password "P@ssw0rd" -Query "SELECT @@version"
```

📸 **Screenshot Placeholder**: *PowerShell output showing SQL Server version*

Loaded PowerUpSQL:

```powershell
cd C:\Tools\PowerUpSQL\
. .\PowerUpSQL.ps1
```

---

🚫 **Why ICMP (Ping) Fails Over SOCKS**

`ping` uses ICMP, which SOCKS5 doesn’t support. Instead, I used:

```powershell
Test-NetConnection -ComputerName 10.10.110.58 -Port 1433
```

✅ Worked perfectly.

---

✅ **Conclusion**

Using a SOCKS5 proxy via SSH allowed me to pivot Commando VM’s traffic through Kali's VPN connection. With Proxifier and PowerUpSQL, I retained full functionality without modifying Kali.

📸 **Screenshot Placeholder**: *Diagram: Commando → SOCKS5 (Kali) → VPN → SQL Server*

---

💡 **Future Improvements**

- 🔐 Automate SOCKS setup with key-based SSH login
- 📈 Monitor/log SOCKS traffic on Kali
- 🧠 Support DNS-over-proxy for advanced tools

---
