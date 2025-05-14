# 🛡️ SOC Lab: Fuerza Bruta SSH / SSH Brute Force Simulation

Este laboratorio simula un ataque real de fuerza bruta SSH contra una máquina en red local. El objetivo es desarrollar habilidades como analista SOC: detectar el escaneo, registrar el intento, analizar los logs y aplicar medidas defensivas.

This lab simulates a real-world SSH brute-force attack against a machine on a local network. The goal is to develop SOC-level skills: detect the scan, log the attempt, analyze system logs, and apply mitigation measures.

---

## 🇪🇸 Descripción en Español

### 🎯 Objetivo
- Realizar un escaneo de puertos con Nmap.
- Detectar un servicio SSH activo.
- Ejecutar un ataque de fuerza bruta.
- Analizar los logs de sistema.
- Capturar el tráfico con tcpdump.
- Documentar el incidente como analista SOC.

### 🛠️ Herramientas usadas
- `nmap`
- `nmap --script ssh-brute`
- `tcpdump`
- `ssh`
- `auth.log`
- `fail2ban` (mitigación)

### 🗂️ Estructura del proyecto

```
/report/       → Informe de incidente + capturas Wireshark
/pcap/         → Archivos .pcap con tráfico capturado
/scripts/      → Comandos o configuraciones útiles
README.md      → Este documento
```

### 🧠 Cómo correr el laboratorio

1. Simular escaneo:
```bash
nmap -Pn -sS -p22 192.168.1.X
```

2. Lanzar fuerza bruta:
```bash
nmap --script ssh-brute -p22 192.168.1.X
```

3. Capturar tráfico:
```bash
tcpdump -i wlan0 port 22 -w pcap/ataque.pcap
```

4. Verificar los registros en `/var/log/auth.log`

5. Aplicar medidas de mitigación:
```bash
sudo ufw deny 22
sudo apt install fail2ban
```

---

## 🇺🇸 English Description

### 🎯 Goal
- Perform Nmap port scan
- Detect active SSH service
- Launch brute force attack
- Analyze `/var/log/auth.log`
- Capture traffic with `tcpdump`
- Mitigate with `ufw` or `fail2ban`

### 🛠️ Tools used
- `nmap`
- `nmap --script ssh-brute`
- `tcpdump`
- `ssh`
- `fail2ban`

### 📂 Project Structure

```
/report/       → Incident report + Wireshark screenshots
/pcap/         → .pcap captured traffic files
/scripts/      → Useful scripts and configs
README.md      → This file
```

---

## ✍️ Autor / Author

**Nicolás Gentile**  
SOC Analyst in training  
GitHub: [IamNiko](https://github.com/IamNiko)
