<div align="center">

  <br></br>
  
  <a href="https://github.com/0xCyberLiTech">
  <img src="https://readme-typing-svg.herokuapp.com?font=JetBrains+Mono&size=50&duration=6000&pause=1000000000&color=FF0048&center=true&vCenter=true&width=1100&lines=%3ECYBERSECURITE_" alt="Titre dynamique CYBERSECURITE" />
  </a>
  
  <br></br>

  <h2>Laboratoire numérique pour la cybersécurité, Linux & IT.</h2>
  
  <p align="center">
      <a href="https://0xcyberlitech.github.io/">
        <img src="https://img.shields.io/badge/Portfolio-0xCyberLiTech-181717?logo=github&style=flat-square" alt="Portfolio" />
      </a>
      <a href="https://github.com/0xCyberLiTech">
        <img src="https://img.shields.io/badge/Profil-GitHub-181717?logo=github&style=flat-square" alt="Profil GitHub" />
      </a>
      <a href="https://github.com/0xCyberLiTech/Cybersecurite/releases/latest">
        <img src="https://img.shields.io/github/v/release/0xCyberLiTech/Cybersecurite?label=version" alt="Latest Release" />
      </a>
      <a href="https://github.com/0xCyberLiTech/Cybersecurite/blob/main/CHANGELOG.md">
        <img src="https://img.shields.io/badge/📄%20CHANGELOG-Cybersecurite-blue" alt="Changelog" />
      </a>
      <a href="https://github.com/0xCyberLiTech?tab=repositories">
        <img src="https://img.shields.io/badge/Dépôts-publics-blue?style=flat-square" alt="Dépôts publics" />
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

# 🛡️ TP – Associer UFW avec Fail2ban sur Debian 12/13

---

## 📑 Sommaire
- [1. Pourquoi associer UFW et Fail2ban ?](#1-pourquoi-associer-ufw-et-fail2ban-)
- [2. Schéma de fonctionnement](#2-schéma-de-fonctionnement)
- [3. Installation de Fail2ban](#3-installation-de-fail2ban)
- [4. Intégration UFW ↔ Fail2ban](#4-intégration-ufw--fail2ban)
- [5. Configuration de base de Fail2ban](#5-configuration-de-base-de-fail2ban)
- [6. Scénarios concrets de protection](#6-scénarios-concrets-de-protection)
- [7. Surveiller l’action de Fail2ban](#7-surveiller-laction-de-fail2ban)
- [8. Bonnes pratiques](#8-bonnes-pratiques)
- [ Conclusion](#-conclusion)

---

## 1. Pourquoi associer UFW et Fail2ban ?

### UFW
- Définit des **règles réseau statiques** (ports ouverts ou fermés).
- Exemple : « J’autorise SSH, j’interdis tout le reste ».  

### Fail2ban
- Surveille les **logs système** (SSH, Apache, FTP, etc.).
- Détecte les comportements suspects (**brute-force**, **scans**, etc.).
- Ajoute **dynamiquement** des règles dans UFW pour bannir les IP malveillantes.

⚠️ **Sans Fail2ban** : un robot peut faire 1000 tentatives SSH.

✅ **Avec Fail2ban** : au bout de 5 échecs → l’IP est bannie automatiquement dans UFW.

---

## 2. Schéma de fonctionnement

```
         Internet
            |
            v
      [ Attaquant ] 
   (brute-force SSH)
            |
            v
   ┌───────────────────┐
   │       SSHD        │
   │  (/var/log/auth)  │
   └───────────────────┘
            |
            v
   ┌───────────────────┐
   │     Fail2ban      │
   │ Analyse les logs  │
   │   "Trop d'échecs" │
   └───────────────────┘
            |
            v
   ┌───────────────────┐
   │        UFW        │
   │ Ajoute une règle  │
   │ DENY → IP bannie  │
   └───────────────────┘
            |
            v
      Attaquant bloqué
```

💡 **Résumé visuel** : Fail2ban est l’intelligence qui lit les logs, et UFW applique le blocage réseau.

---

## 3. Installation de Fail2ban

### Installer le paquet
```bash
sudo apt update && sudo apt install fail2ban -y
```

### Vérifier le service
```bash
systemctl status fail2ban
```

- **Active (running)** → OK, Fail2ban fonctionne.
- Sinon, démarre-le :
```bash
sudo systemctl enable --now fail2ban
```

---

## 4. Intégration UFW ↔ Fail2ban

Par défaut, Fail2ban utilise `iptables`.  
On va lui dire d’utiliser **UFW comme backend**.

Éditer le fichier `/etc/fail2ban/jail.local` (le créer s’il n’existe pas) :
```ini
[DEFAULT]
banaction = ufw
```

💡 **Astuce** : ainsi, chaque bannissement est directement visible dans :
```bash
sudo ufw status
```

---

## 5. Configuration de base de Fail2ban

Copie de sécurité :
```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

### Exemple minimal pour SSH
Éditer `/etc/fail2ban/jail.local` :
```ini
[sshd]
enabled  = true
port     = ssh
filter   = sshd
logpath  = /var/log/auth.log
maxretry = 5
bantime  = 600
```

- **maxretry = 5** → 5 tentatives ratées avant bannissement.  
- **bantime = 600** → IP bannie 10 minutes.  
- **logpath** = chemin des logs surveillés.  

🎯 **Exemple concret** : un attaquant essaie 20 mots de passe SSH → son IP est bannie pendant 10 min.

---

## 6. Scénarios concrets de protection

### 6.1 SSH
👉 Par défaut, Fail2ban protège déjà `sshd`.  
Mais tu peux personnaliser :  
```ini
[sshd]
enabled  = true
port     = 2266
maxretry = 3
bantime  = 1800
```

➡️ Concrètement : ton SSH est sur le port 2266, après 3 échecs l’IP est bannie 30 min.

---

### 6.2 Nginx / Apache
Protection contre les échecs d’auth HTTP :
```ini
[nginx-http-auth]
enabled = true
port    = http,https
filter  = nginx-http-auth
logpath = /var/log/nginx/error.log
maxretry = 3
```

🎯 Concret : un pirate qui tente 3 mauvais logins via `.htpasswd` est bloqué.

---

### 6.3 FTP (vsftpd)
```ini
[vsftpd]
enabled  = true
port     = ftp
filter   = vsftpd
logpath  = /var/log/vsftpd.log
maxretry = 5
```

🎯 Concret : bloque les brute-force FTP.

---

### 6.4 Autres services
Fail2ban fournit des **filtres prêts à l’emploi** pour :  
- Postfix / Dovecot (mail)  
- ProFTPD / Pure-FTPd  
- Nginx / Apache  
- MySQL / MariaDB  

👉 Liste disponible dans `/etc/fail2ban/filter.d/`.

---

## 7. Surveiller l’action de Fail2ban

### Lister les prisons actives
```bash
sudo fail2ban-client status
```

### Vérifier SSH
```bash
sudo fail2ban-client status sshd
```

Exemple de sortie :
```
Status for the jail: sshd
|- Filter
|  |- Currently failed: 2
|  `- Total failed: 15
`- Actions
   |- Currently banned: 1
   `- Total banned: 3
```

### Vérifier UFW
```bash
sudo ufw status
```

🎯 Concret : tu verras des lignes comme :
```
Anywhere DENY IN  from 203.0.113.42
```

---

## 8. Bonnes pratiques

- **Personnaliser** `maxretry` et `bantime` selon ton contexte.  
- **Ne pas activer toutes les prisons** → seulement celles nécessaires (évite les faux positifs).  
- **Surveiller les logs** de Fail2ban :
  ```bash
  journalctl -u fail2ban -f
  ```
- **Coupler UFW + Fail2ban + Fail2ban-recidive** (bannissements longs pour récidivistes).  
- **Sauvegarder** ton fichier `/etc/fail2ban/jail.local`.  

---

## 🎯 Conclusion

- **UFW** = mur statique.  
- **Fail2ban** = vigile intelligent.  
- Ensemble, ils forment une **défense en profondeur** :  
  - UFW ferme les portes.  
  - Fail2ban repère et expulse les intrus insistants.  

    Prochaine étape : intégrer **CrowdSec** pour profiter d’une base communautaire d’attaques connues.

---

<div align="center">

<table>
<tr>
<td align="center"><b>🖥️ Infrastructure &amp; Sécurité</b></td>
<td align="center"><b>💻 Développement &amp; Web</b></td>
<td align="center"><b>🤖 Intelligence Artificielle</b></td>
</tr>
<tr>
<td align="center">
  <a href="https://www.kernel.org/"><img src="https://skillicons.dev/icons?i=linux" width="48" title="Linux" /></a>
  <a href="https://www.debian.org"><img src="https://skillicons.dev/icons?i=debian" width="48" title="Debian" /></a>
  <a href="https://www.gnu.org/software/bash/"><img src="https://skillicons.dev/icons?i=bash" width="48" title="Bash" /></a>
  <br/>
  <a href="https://nginx.org"><img src="https://skillicons.dev/icons?i=nginx" width="48" title="Nginx" /></a>
  <a href="https://www.docker.com"><img src="https://skillicons.dev/icons?i=docker" width="48" title="Docker" /></a>
  <a href="https://git-scm.com"><img src="https://skillicons.dev/icons?i=git" width="48" title="Git" /></a>
</td>
<td align="center">
  <a href="https://www.python.org"><img src="https://skillicons.dev/icons?i=python" width="48" title="Python" /></a>
  <a href="https://flask.palletsprojects.com"><img src="https://skillicons.dev/icons?i=flask" width="48" title="Flask" /></a>
  <a href="https://developer.mozilla.org/docs/Web/HTML"><img src="https://skillicons.dev/icons?i=html" width="48" title="HTML5" /></a>
  <br/>
  <a href="https://developer.mozilla.org/docs/Web/CSS"><img src="https://skillicons.dev/icons?i=css" width="48" title="CSS3" /></a>
  <a href="https://developer.mozilla.org/docs/Web/JavaScript"><img src="https://skillicons.dev/icons?i=js" width="48" title="JavaScript" /></a>
  <a href="https://code.visualstudio.com"><img src="https://skillicons.dev/icons?i=vscode" width="48" title="VS Code" /></a>
</td>
<td align="center">
  <a href="https://pytorch.org"><img src="https://skillicons.dev/icons?i=pytorch" width="48" title="PyTorch" /></a>
  <a href="https://www.tensorflow.org"><img src="https://skillicons.dev/icons?i=tensorflow" width="48" title="TensorFlow" /></a>
  <a href="https://www.raspberrypi.com"><img src="https://skillicons.dev/icons?i=raspberrypi" width="48" title="Raspberry Pi" /></a>
  <br/><br/>
  <a href="https://ollama.com"><img src="https://img.shields.io/badge/Ollama-000000?style=for-the-badge&logo=ollama&logoColor=white" alt="Ollama" /></a>
  &nbsp;
  <a href="https://anthropic.com"><img src="https://img.shields.io/badge/Anthropic-D97757?style=for-the-badge&logo=anthropic&logoColor=white" alt="Anthropic" /></a>
</td>
</tr>
</table>

<br/>

<b>🔒 Un projet proposé par <a href="https://github.com/0xCyberLiTech">0xCyberLiTech</a> • Développé en collaboration avec <a href="https://claude.ai">Claude AI</a> (Anthropic) 🔒</b>

</div>

