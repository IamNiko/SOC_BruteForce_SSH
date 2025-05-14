# 🛡️ Informe de Incidente SOC — Fuerza Bruta SSH

## 🗓️ Fecha del incidente

14 de mayo de 2025

## 👤 Autor

**Nicolás Gentile** — Analista SOC en formación

---

## 1. Introducción

Este laboratorio simula un ataque real de fuerza bruta contra un servicio SSH expuesto en una red local. El objetivo fue detectar, analizar y documentar el incidente desde la perspectiva de un analista SOC, utilizando herramientas de análisis de red, captura de paquetes y registros del sistema.

---

## 2. Infraestructura utilizada

| Rol      | Dispositivo    | IP local     | Sistema operativo      |
| -------- | -------------- | ------------ | ---------------------- |
| Atacante | Parrot OS      | 192.168.1.24 | Parrot OS Linux        |
| Víctima  | Raspberry Pi 4 | 192.168.1.78 | Debian (Raspbian Lite) |

---

## 3. Descripción del ataque

1. Se realizó un escaneo de puertos con `nmap` para detectar servicios abiertos.
2. Se identificó el puerto `22/tcp` correspondiente al servicio SSH.
3. Se lanzó un ataque de fuerza bruta con `hydra` dirigido al usuario `bruteuser`.
4. Se descubrió exitosamente la contraseña `123456`.
5. Se accedió por SSH y se utilizó el editor `nano` para crear un archivo llamado `virus.txt`.
6. Todo el tráfico fue capturado con `tcpdump` y analizado posteriormente con Wireshark.

---

## 4. Evidencia recopilada

### 📄 Capturas clave:

* **01\_handshake\_start.png** → Inicio del handshake TCP (SYN)
* **02\_login\_success.png** → Flujo de la sesión SSH exitosa
* **03\_session\_close.png** → Cierre limpio de la sesión (FIN, ACK)
* **04\_TCP\_conversation.png** → Detalles de la conversación TCP
* **05\_ssh\_traffic.png** → Pico de tráfico cifrado (actividad dentro de la sesión)

### 📦 Archivos incluidos:

* `ssh_bruteforce.pcap` → Tráfico completo capturado
* `auth_bruteforce.log` → Registros del sistema confirmando el acceso
* `nmap_ssh_scan.txt` → Resultado del escaneo de puertos
* `hydra_result.txt` → Resultado de Hydra: credenciales descubiertas `bruteuser:123456`

---

## 5. Análisis del incidente

* El atacante logró autenticarse correctamente por SSH.
* Se identificó actividad interactiva a través de paquetes `PSH, ACK`, retransmisiones y un flujo TCP prolongado.
* La sesión fue breve pero activa, con interacción real y creación de archivo simulada.
* El archivo `.pcap` confirma el inicio del handshake, el flujo de datos cifrados y el cierre correcto de la conexión.
* Los registros del sistema (`auth.log`) confirman el inicio de sesión desde la IP `192.168.1.24`.

---

## 6. Medidas de mitigación aplicadas

* Cierre del puerto SSH con `ufw`:

```bash
sudo ufw deny 22
```

* Instalación de `fail2ban` para prevenir futuros intentos automatizados:

```bash
sudo apt install fail2ban
```

* Revisión de usuarios válidos y refuerzo de las políticas de contraseñas seguras.

---

## 7. Conclusiones

Este laboratorio refleja de manera completa el ciclo de un incidente de fuerza bruta SSH en un entorno controlado. Se logró identificar el acceso, recolectar y analizar evidencia técnica, y aplicar medidas defensivas efectivas. Representa una simulación fiel al trabajo que realiza diariamente un analista SOC de nivel 1.
