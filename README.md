# CyberSecurity-IDS-Lab

# Projet personnel – Analyse et sécurisation d’un réseau local avec IDS

## 🎯 Objectif
Créer un laboratoire virtuel de cybersécurité pour :
- Capturer et analyser le trafic réseau
- Simuler des attaques internes (scan, brute force)
- Mettre en place un IDS (Snort ou Suricata)
- Configurer des protections (pare-feu, Fail2ban)
- Documenter les résultats et sécurisations appliquées

## 🧰 Outils
- VirtualBox / VMware
- Kali Linux (attaquant)
- Ubuntu Server (serveur cible + IDS)
- Windows 10 (poste utilisateur)
- Wireshark, Nmap, Hydra, Snort/Suricata, iptables, fail2ban

## 🛠️ Étapes
### 1. Mise en place du réseau
- Créer un réseau interne VirtualBox
- Connecter les 3 VMs
- Tester la connectivité (`ping`)

### 2. Analyse réseau
- Lancer Wireshark sur Ubuntu
- Capturer trafic normal
- Identifier ports/services visibles

### 3. Simulation d’attaques
- Scan Nmap depuis Kali
- Bruteforce SSH avec Hydra

### 4. Détection avec IDS
- Installer Snort ou Suricata
- Ajouter règle pour détecter scan Nmap (exemple ci-dessous)
- Observer les logs

### 5. Sécurisation
- Fermer ports avec `iptables`
- Activer Fail2ban
- Modifier configuration SSH

## 🔐 Exemple de règle Snort (scan Nmap)

```
alert tcp any any -> 192.168.56.0/24 any (msg:"Nmap Scan Detected"; flags:S; threshold:type threshold, track by_src, count 20, seconds 5; sid:1000001; rev:1;)
```

## 🔥 Exemple de script iptables de base

```bash
#!/bin/bash

# Vider les règles existantes
iptables -F

# Politique par défaut : bloquer tout
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Autoriser loopback
iptables -A INPUT -i lo -j ACCEPT

# Autoriser SSH depuis ton réseau local
iptables -A INPUT -p tcp --dport 22 -s 192.168.56.0/24 -j ACCEPT

# Autoriser les connexions établies
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

## 🧪 Résultats attendus
- Fichiers de log IDS
- Captures Wireshark
- Scripts de protection
- Rapport final ou documentation GitHub

## 📎 Documents à inclure dans le projet
- `README.md` (ce fichier)
- `iptables.sh`
- `scan_detect.rules`
- `captures.pcapng`
- `rapport.pdf` (final)

---

Projet réalisé dans le cadre d'une préparation au master en cybersécurité.
