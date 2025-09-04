<div align="center">
  
  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
    <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3EFIREWALL_" alt="Titre dynamique FIREWALL" />
  </a>
  
  <br></br>

  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT</h2>

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

## 🚀 À propos & Objectifs

Ce projet propose des solutions innovantes et accessibles en cybersécurité, avec une approche centrée sur la simplicité d’utilisation et l’efficacité. Il vise à accompagner les utilisateurs dans la protection de leurs données et systèmes, tout en favorisant l’apprentissage et le partage des connaissances.

Le contenu est structuré, accessible et optimisé SEO pour répondre aux besoins de :
- 🎓 Étudiants : approfondir les connaissances
- 👨‍💻 Professionnels IT : outils et pratiques
- 🖥️ Administrateurs système : sécuriser l’infrastructure
- 🛡️ Experts cybersécurité : ressources techniques
- 🚀 Passionnés du numérique : explorer les bonnes pratiques

---

# 🔥 TP – Sécuriser son serveur Debian 12/13 avec UFW

---

## 📑 Sommaire
- [🟢 Session Débutant – « Premiers pas avec UFW »](#-session-débutant--premiers-pas-avec-ufw)
  - [1. Pourquoi un pare-feu ?](#1-pourquoi-un-pare-feu-)
  - [2. Installation](#2-installation)
  - [3. Poser les bases : politique « deny by default »](#3-poser-les-bases--politique-deny-by-default)
  - [4. Ne pas se bloquer soi-même → autoriser SSH](#4-ne-pas-se-bloquer-soi-même--autoriser-ssh)
  - [5. Activer le pare-feu](#5-activer-le-pare-feu)
  - [6. Exemple concret : premier serveur web](#6-exemple-concret--premier-serveur-web)
  - [7. Journalisation](#7-journalisation)
- [🔵 Session Avancée – « Devenir maître de son firewall »](#-session-avancée--devenir-maître-de-son-firewall)
  - [1. Cloisonner les flux sortants](#1-cloisonner-les-flux-sortants)
  - [2. Restreindre SSH à ton IP d’admin](#2-restreindre-ssh-à-ton-ip-dadmin)
  - [3. Bloquer les menaces](#3-bloquer-les-menaces)
  - [4. Protection brute-force SSH](#4-protection-brute-force-ssh)
  - [5. Profils applicatifs](#5-profils-applicatifs)
  - [6. Tuning interne (iptables derrière UFW)](#6-tuning-interne-iptables-derrière-ufw)
  - [7. Sauvegarder et restaurer](#7-sauvegarder-et-restaurer)
  - [8. Surveiller en temps réel](#8-surveiller-en-temps-réel)
  - [9. Bonnes pratiques](#9-bonnes-pratiques)
- [🎯 Conclusion du TP](#-conclusion-du-tp)

---

## 🟢 Session Débutant – « Premiers pas avec UFW »

### 1. Pourquoi un pare-feu ?
Un pare-feu limite l’exposition d’un serveur :  
- **Filtrage entrant** : seuls les services voulus sont accessibles.  
- **Filtrage sortant** : la machine ne parle qu’aux destinations autorisées.  
- **Journalisation** : traçabilité des tentatives d’accès.  

⚠️ **Attention** : un serveur sans pare-feu expose *tous ses services* à Internet → c’est comme laisser toutes les portes et fenêtres ouvertes.

---

### 2. Installation
```bash
sudo apt update && sudo apt install ufw -y
```

⚠️ **Conseil sécurité** : garde toujours une **deuxième porte ouverte** (console physique ou accès console VPS) pour éviter de perdre ton SSH.

---

### 3. Poser les bases : politique « deny by default »
```bash
sudo ufw default deny incoming   # bloquer tout ce qui arrive
sudo ufw default allow outgoing  # autoriser ce qui sort
```

💡 **Astuce** : comme une boîte fermée → rien n’entre, sauf ce que tu autorises.

---

### 4. Ne pas se bloquer soi-même → autoriser SSH
```bash
sudo ufw allow 22/tcp
```
👉 Si ton SSH est sur un port personnalisé (exemple : `2266`) :
```bash
sudo ufw allow 2266/tcp
```

---

### 5. Activer le pare-feu
```bash
sudo ufw enable
```

Vérifier l’état :  
```bash
sudo ufw status verbose
```

---

### 6. Exemple concret : premier serveur web
```bash
sudo ufw allow 80,443/tcp
```

🎯 **Exemple concret** :  
- Tu héberges un WordPress → visiteurs accèdent aux ports 80/443.  
- MySQL est présent mais reste **fermé au public**.  

---

### 7. Journalisation
```bash
sudo ufw logging medium
tail -f /var/log/ufw.log
```

🎯 **Exemple concret** : tu verras apparaître des IP étrangères tentant du SSH → bloquées automatiquement.

---

✅ **Bilan Débutant** : ton serveur est déjà bien plus sûr, avec seulement SSH + Web ouverts.

---

## 🔵 Session Avancée – « Devenir maître de son firewall »

Ton serveur héberge plus de services. Tu veux maintenant :  
- Restreindre SSH à une seule IP.  
- Cloisonner les flux sortants (anti-spam).  
- Utiliser les profils applicatifs.  
- Ajuster finement les règles.

---

### 1. Cloisonner les flux sortants
```bash
sudo ufw reset
sudo ufw default deny incoming
sudo ufw default deny outgoing
sudo ufw allow out 53/udp       # DNS
sudo ufw allow out 80,443/tcp   # APT
sudo ufw enable
```

🎯 **Exemple concret** :  
Un malware essaie d’envoyer des mails de spam → bloqué, car port 25 interdit.  

---

### 2. Restreindre SSH à ton IP d’admin
```bash
sudo ufw allow from 198.51.100.5 to any port 2266 proto tcp
```

🎯 **Exemple concret** :  
Seule ton IP fixe d’entreprise peut se connecter → les robots et attaquants sont exclus.  

---

### 3. Bloquer les menaces
- Bloquer une IP qui scanne :  
  ```bash
  sudo ufw deny from 203.0.113.66
  ```
- Bloquer les envois de mails sortants (anti-spam) :  
  ```bash
  sudo ufw deny out 25/tcp
  ```

---

### 4. Protection brute-force SSH
```bash
sudo ufw limit 22/tcp comment "Anti brute-force"
```

🎯 **Exemple concret** : les attaques par dictionnaire sur ton SSH sont ralenties → moins de charge serveur.

---

### 5. Profils applicatifs
```bash
sudo ufw app list
sudo ufw allow "Nginx Full"   # ouvre 80 + 443
```

💡 **Astuce** : plus besoin de mémoriser les ports → UFW connaît déjà Samba, Apache, Postfix, etc.

---

### 6. Tuning interne (iptables derrière UFW)
Exemple : désactiver le ping système (ICMP).  
- Modifier `/etc/ufw/before.rules` (changer `ACCEPT` → `DROP` pour ICMP).  
- Puis :  
  ```bash
  sudo ufw reload
  ```

🎯 **Exemple concret** : ton serveur devient invisible aux scans par ping.

---

### 7. Sauvegarder et restaurer
```bash
sudo ufw export > ufw-backup.conf
sudo ufw import ufw-backup.conf
```

🎯 **Exemple concret** : déploiement identique d’un firewall sur 5 serveurs en un instant.

---

### 8. Surveiller en temps réel
```bash
sudo ufw logging high
tail -f /var/log/ufw.log
```

🎯 **Exemple concret** :  
Tu vois 500 tentatives SSH depuis la Russie → signe qu’un botnet scanne ton IP.

---

### 9. Bonnes pratiques
- Toujours **deny by default**.  
- Tester une règle dans une deuxième session SSH avant `enable`.  
- Sauvegarder régulièrement la configuration.  
- Associer UFW à un **IDS** (Fail2ban, CrowdSec).  

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
