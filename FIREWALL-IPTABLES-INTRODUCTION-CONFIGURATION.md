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

# 🔒 TP — Sécuriser Linux avec `iptables`

## 🎯 Objectifs pédagogiques
À la fin de ce TP, vous serez capable de :
- Comprendre la logique de fonctionnement de `iptables`.
- Créer un pare-feu basique et progressif.
- Tester et vérifier vos règles sans bloquer votre accès SSH.
- Sauvegarder et restaurer vos configurations.

---

## 🔗 1. Qu’est-ce que `iptables` ?

`iptables` est un outil en ligne de commande permettant de **contrôler le trafic réseau** sous Linux.  
Il agit comme un **pare-feu** logiciel :

- ✅ Autoriser certains flux (web, SSH, ping, etc.)
- ❌ Bloquer ou rejeter les flux indésirables (attaques, scans, ports inutiles)
- 🔄 Rediriger ou modifier des paquets

👉 **En résumé :** c’est la "porte de sécurité" de votre machine.

---

## 🛠️ 2. Structure d’une règle

Une règle `iptables` suit cette logique :

```bash
iptables -A [chaîne] [filtres] -j [action]
```

| Élément       | Exemple                         | Rôle                                      |
|---------------|---------------------------------|-------------------------------------------|
| `-A`          | `-A INPUT`                      | Ajouter une règle à une chaîne            |
| `-p`          | `-p tcp`                        | Spécifier un protocole (tcp, udp, icmp)   |
| `--dport`     | `--dport 22`                    | Port de destination                       |
| `-s` / `-d`   | `-s 203.0.113.42`               | IP source / IP destination                |
| `-j`          | `-j ACCEPT` / `DROP` / `REJECT` | Action appliquée au paquet                |

---

## 📊 3. Les chaînes principales

`iptables` traite les paquets en fonction de **chaînes** :

| Chaîne    | Rôle                                       |
|-----------|--------------------------------------------|
| `INPUT`   | Trafic entrant vers la machine             |
| `OUTPUT`  | Trafic sortant depuis la machine           |
| `FORWARD` | Trafic traversant la machine (routage)     |

---

## 📁 4. Les tables principales

| Table     | Usage                                      |
|-----------|--------------------------------------------|
| `filter`  | Filtrage classique (par défaut)            |
| `nat`     | Traduction/routage (NAT, redirections)     |
| `mangle`  | Modification avancée des paquets           |

---

## 🔬 5. Mise en pratique pas à pas

### Étape 1 — Vérifier les règles existantes
```bash
sudo iptables -L -v -n
```
👉 Vous devriez voir des règles par défaut (souvent `ACCEPT` partout).

---

### Étape 2 — Nettoyer la configuration (⚠️ à ne faire que sur une VM/test)
```bash
sudo iptables -F
sudo iptables -X
sudo iptables -t nat -F
```
👉 Votre pare-feu est maintenant vide.

---

### Étape 3 — Définir une politique par défaut
```bash
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT
```
- On bloque **tout en entrée** sauf ce que l’on autorise explicitement.
- On autorise **tout en sortie**.

---

### Étape 4 — Autoriser le trafic de base
- **Boucle locale (loopback)** :
```bash
sudo iptables -A INPUT -i lo -j ACCEPT
```

- **Connexions déjà établies** :
```bash
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

👉 Ainsi, les réponses aux connexions sortantes (comme `apt update`) passent bien.

---

### Étape 5 — Autoriser services essentiels
- **SSH (port 22)** :
```bash
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
```

- **Web (HTTP/HTTPS)** :
```bash
sudo iptables -A INPUT -p tcp -m multiport --dports 80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp -m multiport --sports 80,443 -m state --state ESTABLISHED -j ACCEPT
```

- **Ping (ICMP)** :
```bash
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```

---

### Étape 6 — Cas pratique : accès limité à un port
👉 Exemple : seul l’hôte `203.0.113.42` peut accéder au port `54321`.

```bash
sudo iptables -A INPUT -p tcp -s 203.0.113.42 --dport 54321 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 54321 -j DROP
```

---

### Étape 7 — Protection contre brute-force SSH
Limiter à **3 tentatives par minute** :

```bash
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update \
--seconds 60 --hitcount 3 --name SSH -j DROP
```

---

### Étape 8 — Activer les logs
```bash
sudo iptables -A INPUT -j LOG --log-prefix "[IPTABLES BLOCK] " --log-level 4
```

👉 Les journaux apparaîtront dans `/var/log/syslog` ou `/var/log/messages`.

---

## 💾 6. Sauvegarder et restaurer

- **Installation de l’outil de persistance (Debian/Ubuntu)** :
```bash
sudo apt install iptables-persistent
```

- **Sauvegarder les règles** :
```bash
sudo iptables-save > /etc/iptables/rules.v4
```

- **Restaurer** :
```bash
sudo iptables-restore < /etc/iptables/rules.v4
```

---

## 📜 7. Exemple de script complet (pare-feu basique)

```bash
#!/bin/bash
# Script de configuration iptables (firewall.sh)

# 🔄 Nettoyage des règles
iptables -F
iptables -X
iptables -t nat -F

# 🔐 Politiques par défaut
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# 🔁 Loopback
iptables -A INPUT -i lo -j ACCEPT

# 🔗 Connexions établies
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# 🔑 SSH sécurisé
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update \
--seconds 60 --hitcount 3 --name SSH -j DROP
iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT

# 🌐 Web
iptables -A INPUT -p tcp -m multiport --dports 80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp -m multiport --sports 80,443 -m state --state ESTABLISHED -j ACCEPT

# 🎯 Port restreint
iptables -A INPUT -p tcp -s 203.0.113.42 --dport 54321 -j ACCEPT
iptables -A INPUT -p tcp --dport 54321 -j DROP

# 📝 Logging
iptables -A INPUT -j LOG --log-prefix "[IPTABLES BLOCK] " --log-level 4
```

Rendre exécutable :
```bash
chmod +x firewall.sh
sudo ./firewall.sh
```

---

## ✅ 8. Bonnes pratiques

- ⚠️ Toujours tester sur une **session SSH secondaire** avant de fermer la session principale.
- 📖 Documenter vos règles dans un fichier versionné (`git` par exemple).
- 🔍 Vérifier l’ordre des règles : `iptables -L -v -n --line-numbers`.
- 🛠️ Préparer un script de remise à zéro si vous vous bloquez :
```bash
#!/bin/bash
iptables -F
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
```

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

