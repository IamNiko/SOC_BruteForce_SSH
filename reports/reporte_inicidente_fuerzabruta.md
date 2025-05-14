# 🛡️ SOC Incident Report — SSH Brute Force

## 🗓️ Incident Date

May 14, 2025

## 👤 Author

**Nicolás Gentile** — SOC Analyst in training

---

## 1. Introduction

This lab simulates a real-world brute-force attack against an SSH service exposed on a local network. The goal was to detect, analyze, and document the incident from a SOC analyst perspective using network tools, packet capture, and system logs.

---

## 2. Infrastructure Used

| Role     | Device         | Local IP     | Operating System       |
| -------- | -------------- | ------------ | ---------------------- |
| Attacker | Parrot OS (VM) | 192.168.1.24 | Parrot OS Linux        |
| Victim   | Raspberry Pi 4 | 192.168.1.78 | Debian (Raspbian Lite) |

---

## 3. Attack Description

1. A port scan was performed using `nmap` to detect open services.
2. Port `22/tcp` (SSH) was found exposed.
3. A brute-force attack was launched with `hydra` targeting user `bruteuser`.
4. The password `123456` was successfully discovered.
5. SSH access was gained and the `nano` editor was used to create a file named `virus.txt`.
6. All traffic was captured with `tcpdump` and analyzed using Wireshark.

---

## 4. Collected Evidence

### 📄 Key Screenshots:

* **01\_handshake\_start.png** → TCP handshake initiation (SYN)
* **02\_login\_success.png** → Stream of successful SSH session
* **03\_session\_close.png** → Proper session termination (FIN, ACK)
* **04\_TCP\_conversation.png** → TCP conversation details
* **05\_ssh\_traffic.png** → Encrypted traffic spike

### 📦 Files:

* `ssh_bruteforce.pcap` → Full captured traffic
* `auth_bruteforce.log` → System logs (successful login)
* `nmap_ssh_scan.txt` → Port scan result
* `hydra_result.txt` → Brute-force result: `bruteuser:123456`

---

## 5. Incident Analysis

* The attacker successfully authenticated via SSH.
* Interactive activity was observed (PSH, ACK packets, retransmissions, long TCP stream).
* The session was short but active, with simulated file creation.
* The `.pcap` confirms handshakes, encrypted data, and proper session closure.
* System logs confirm the login from IP `192.168.1.24`.

---

## 6. Mitigation Measures Applied

* SSH port closed:

```bash
sudo ufw deny 22
```

* `fail2ban` installed to block automated brute-force attempts:

```bash
sudo apt install fail2ban
```

* Reviewed valid users and enforced strong passwords.

---

## 7. Conclusions

This lab demonstrates the full flow of a real SSH brute-force incident. The login was identified, technical evidence captured and analyzed, and defensive measures implemented. It reflects the kind of investigation and response handled daily by a level 1 SOC analyst.
