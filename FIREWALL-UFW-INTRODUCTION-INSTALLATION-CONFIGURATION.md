<div align="center">
  
  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3EFIREWALL_" alt="Titre dynamique FIREWALL" />
  </a>
  
  <br></br>

  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT.</h2>

  <p align="center">
    <a href="https://0xcyberlitech.github.io/">
      <img src="https://img.shields.io/badge/Portfolio-0xCyberLiTech-181717?logo=github&style=flat-square" alt="🌐 Portfolio" />
    </a>
    <a href="https://github.com/0xCyberLiTech">
      <img src="https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square" alt="🔗 Profil GitHub" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Firewall/releases/latest">
      <img src="https://img.shields.io/github/v/release/0xCyberLiTech/Firewall?label=version&style=flat-square&color=blue" alt="📦 Dernière version" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Firewall/blob/main/CHANGELOG.md">
      <img src="https://img.shields.io/badge/📄%20Changelog-Firewall-blue?style=flat-square" alt="📄 CHANGELOG Firewall" />
    </a>
    <a href="https://github.com/0xCyberLiTech?tab=repositories">
      <img src="https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square" alt="📂 Dépôts publics" />
    </a>
    <a href="https://github.com/0xCyberLiTech/Firewall/graphs/contributors">
      <img src="https://img.shields.io/badge/👥%20Contributeurs-cliquez%20ici-007ec6?style=flat-square" alt="👥 Contributeurs Firewall" />
    </a>
  </p>

</div>

<div align="center">
  <img src="https://img.icons8.com/fluency/96/000000/cyber-security.png" alt="CyberSec" width="80"/>
</div>

<div align="center">
  <p>
    <strong>Cybersécurité</strong> <img src="https://img.icons8.com/color/24/000000/lock--v1.png"/> • <strong>Linux Debian</strong> <img src="https://img.icons8.com/color/24/000000/linux.png"/> • <strong>Sécurité informatique</strong> <img src="https://img.icons8.com/color/24/000000/shield-security.png"/>
  </p>
</div>

---

<div align="center">
  
## À propos & Objectifs.

</div>

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

---

# 🔥 Tutoriel UFW – Sécuriser son serveur Debian 12/13 avec UFW

---

## 📑 Sommaire :

1. [Pourquoi un pare-feu ?](#1-pourquoi-un-pare-feu-)
2. [Installation](#2-installation)
3. [Poser les bases : politique « deny by default »](#3-poser-les-bases--politique--deny-by-default-)
4. [Autoriser Uniquement les Services Nécessaires](#4-autoriser-uniquement-les-services-nécessaires)
5. [Schéma explicatif : Ouverture de ports](#5-schéma-explicatif--ouverture-de-ports)
6. [Limiter les Tentatives SSH (Anti-brute-force)](#6-limiter-les-tentatives-ssh-anti-brute-force)
7. [Activer UFW](#7-activer-ufw)
8. [Vérifier les Règles Actives](#8-vérifier-les-règles-actives)
9. [Activer la Journalisation UFW](#9-activer-la-journalisation-ufw)
10. [Consulter les Logs UFW](#10-consulter-les-logs-ufw)
11. [Script d’Installation Automatique](#11-script-dinstallation-automatique)
12. [Gestion des Règles UFW](#12-gestion-des-règles-ufw)
13. [Exemples de Règles Supplémentaires](#13-exemples-de-règles-supplémentaires)
14. [Schémas : Flux réseau et logique UFW](#14-schémas--flux-réseau-et-logique-ufw)
15. [Bonnes Pratiques](#15-bonnes-pratiques)
16. [Pour aller plus loin](#16-pour-aller-plus-loin)

---

## 1. Pourquoi un pare-feu ?

- **Filtrage entrant** : seuls les services voulus sont accessibles.
- **Filtrage sortant** : la machine ne parle qu’aux destinations autorisées.
- **Journalisation** : traçabilité des tentatives d’accès.

> ⚠️ Un serveur sans pare-feu expose tous ses services à Internet → c’est comme laisser toutes les portes et fenêtres ouvertes.

---

## 2. Installation

```bash
sudo apt update && sudo apt install ufw -y
```

---

## 3. Poser les bases : politique « deny by default »

### a) Tout bloquer en entrée par défaut

```bash
sudo ufw default deny incoming
```

### b) Tout autoriser en sortie par défaut

```bash
sudo ufw default allow outgoing
```

---

## 4. Autoriser Uniquement les Services Nécessaires

### a) SSH (accès distant)

```bash
sudo ufw allow ssh
# ou
sudo ufw allow 22/tcp
```

### b) HTTP/HTTPS (serveur web)

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

---

## 5. Schéma explicatif : Ouverture de ports

```
+-------------------+         +-------------------+
|   Internet        |         |   Votre Serveur   |
|                   |         |                   |
|   [Client SSH]----|-------->|   [Port 22]       |
|   [Client Web]----|-------->|   [Port 80/443]   |
+-------------------+         +-------------------+
```
Seuls les ports explicitement ouverts (22, 80, 443) sont accessibles depuis l’extérieur.

---

## 6. Limiter les Tentatives SSH (Anti-brute-force)

```bash
sudo ufw limit ssh
```

---

## 7. Activer UFW

```bash
sudo ufw enable
```

---

## 8. Vérifier les Règles Actives

```bash
sudo ufw status verbose
```

---

## 9. Activer la Journalisation UFW

```bash
sudo ufw logging on
```

---

## 10. Consulter les Logs UFW

- Tous les logs :
  ```bash
  sudo journalctl | grep UFW
  ```
- Logs récents :
  ```bash
  sudo journalctl -e | grep UFW
  ```
- Suivi en temps réel :
  ```bash
  sudo journalctl -f | grep UFW
  ```

---

## 11. Script d’Installation Automatique

```bash
#!/bin/bash

# Bloquer toutes les connexions entrantes
sudo ufw default deny incoming

# Autoriser toutes les connexions sortantes
sudo ufw default allow outgoing

# Autoriser SSH
sudo ufw allow ssh

# Limiter les tentatives SSH
sudo ufw limit ssh

# (Optionnel) Autoriser HTTP/HTTPS si serveur web
# sudo ufw allow 80/tcp
# sudo ufw allow 443/tcp

# Activer UFW
sudo ufw enable

# Afficher le statut
sudo ufw status verbose
```

Rendez-le exécutable et lancez-le :
```bash
chmod +x setup-ufw.sh
./setup-ufw.sh
```

---

## 12. Gestion des Règles UFW

### a) Lister les règles avec leur numéro

```bash
sudo ufw status numbered
```

### b) Supprimer une règle par son numéro

Exemple : pour supprimer la règle numéro 3 :

```bash
sudo ufw delete 3
```

### c) Modifier une règle

Supprimez la règle existante puis ajoutez la nouvelle :

```bash
sudo ufw allow 2222/tcp
```

### d) Désactiver UFW (toutes les règles)

```bash
sudo ufw disable
```

---

## 13. Exemples de Règles Supplémentaires

- Autoriser un port UDP (ex : 1194 pour OpenVPN) :
  ```bash
  sudo ufw allow 1194/udp
  ```

- Autoriser une plage d’IP à accéder à un port :
  ```bash
  sudo ufw allow from 192.168.1.0/24 to any port 3306
  ```

- Refuser une IP spécifique :
  ```bash
  sudo ufw deny from 203.0.113.42
  ```

- Autoriser un port pour une interface réseau spécifique :
  ```bash
  sudo ufw allow in on eth0 to any port 8080
  ```

- Autoriser un port pour une IP précise :
  ```bash
  sudo ufw allow from 10.0.0.5 to any port 22
  ```

- Refuser tout le trafic d’un pays (nécessite une liste d’IP) :
  ```bash
  # Exemple avec un fichier d’IP
  for ip in $(cat ips_country.txt); do sudo ufw deny from $ip; done
  ```

- Autoriser le ping (ICMP) :
  ```bash
  sudo ufw allow proto icmp
  ```

- Refuser tout le trafic sortant sauf HTTP/HTTPS :
  ```bash
  sudo ufw default deny outgoing
  sudo ufw allow out 80/tcp
  sudo ufw allow out 443/tcp
  ```

- Autoriser le port SMTP (mail) :
  ```bash
  sudo ufw allow 25/tcp
  ```

- Autoriser le port FTP :
  ```bash
  sudo ufw allow 21/tcp
  ```

- Autoriser le port DNS :
  ```bash
  sudo ufw allow 53
  ```

- Autoriser le port MySQL pour une IP spécifique :
  ```bash
  sudo ufw allow from 192.168.1.100 to any port 3306
  ```

- Refuser tout sauf une IP sur SSH :
  ```bash
  sudo ufw deny ssh
  sudo ufw allow from 203.0.113.10 to any port 22
  ```

- Autoriser le port NFS (2049) pour le réseau local :
  ```bash
  sudo ufw allow from 192.168.1.0/24 to any port 2049
  ```

- Autoriser le port pour une plage d’IP et une interface :
  ```bash
  sudo ufw allow in on eth1 from 10.10.10.0/24 to any port 8080
  ```

---

## 14. Schémas : Flux réseau et logique UFW

### Schéma 1 : Flux réseau général

```
        +-------------------+
        |   Internet        |
        +--------+----------+
                 |
         [Ports non autorisés]
                 X (bloqué)
                 |
         [Ports autorisés]
                 |
        +--------v----------+
        |   Serveur UFW     |
        +-------------------+
```

### Schéma 2 : Logique de décision UFW

```
+-------------------+
|   Paquet réseau   |
+-------------------+
         |
         v
+----------------------+
|  Règle UFW existe ?  |
+----------------------+
   | Oui         | Non
   v             v
[Action]     [Bloqué]
```

### Schéma 3 : Exemple de filtrage par IP

```
+-------------------+
|   Internet        |
+--------+----------+
         |
   [IP autorisée] --------> [Port ouvert]
   [IP refusée]    --X--> [Bloqué]
```

---

## 15. Bonnes Pratiques

- Toujours tester l’accès SSH avant d’activer UFW sur un serveur distant.
- N’ouvrir que les ports strictement nécessaires.
- Activer la journalisation pour surveiller les accès.
- Mettre à jour régulièrement votre système.
- Documenter les règles appliquées pour faciliter la maintenance.

---

## 16. Pour aller plus loin

- [Documentation officielle UFW (EN)](https://help.ubuntu.com/community/UFW)
- [Tutoriel DigitalOcean (FR)](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)
- [UFW man page](https://manpages.ubuntu.com/manpages/bionic/man8/ufw.8.html)

---

## 🎯 Conclusion du TP
- En **débutant**, tu passes d’un serveur nu à un serveur protégé.  
- En **avancé**, tu transformes ton serveur en **citadelle** : cloisonné, surveillé, renforcé.  

👉 La prochaine étape ? Associer UFW avec **Fail2ban** pour bloquer automatiquement les IP agressives 🚀

---

<div align="center">
  <a href="https://github.com/0xCyberLiTech" target="_blank" rel="noopener">
    <img src="https://skillicons.dev/icons?i=linux,debian,bash,docker,nginx,git,vim,python,markdown" alt="Skills" width="440">
  </a>
</div>

<div align="center">
  <b>🔒 Un guide proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Pour des tutoriels accessibles à tous. 🔒</b>
</div>

