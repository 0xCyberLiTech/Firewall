<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-firewall.svg" alt="ATELIER FIREWALL // FILTRAGE RÉSEAU" width="100%" />
</a>

<p align="center">
  <a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-portal.svg" alt="Portail 0xCyberLiTech.com" width="24%" /></a>
  <a href="https://0xcyberlitech.com/soc-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-soc-rd.svg" alt="Livre Blanc SOC Cockpit" width="24%" /></a>
  <a href="https://0xcyberlitech.com/jarvis-rd.html"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-jarvis-rd.svg" alt="Livre Blanc JARVIS IA" width="24%" /></a>
  <a href="https://github.com/0xCyberLiTech?tab=repositories"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-github.svg" alt="Catalogue des 23 Dépôts" width="24%" /></a>
</p>
<p align="center">
  <a href="README.md"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-back-readme.svg" alt="Retour au sommaire du dépôt" width="340" /></a>
</p>

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />
</div>
<!-- MASTER-HEADER-END -->

<!-- DEBIAN-TRUTH-START -->
> [!IMPORTANT]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> ** Matrice Officielle Debian — `Debian 12 (Bookworm)` · `Debian 13 (Trixie)` · `Debian 14 (Forky)`**
> - **Sources Officielles Debian.org (`ufw`) :** `Bookworm (12)` : **`0.36.2-1`** &nbsp;·&nbsp; `Trixie (13 — Stable)` : **`0.36.2-9`** &nbsp;·&nbsp; `Forky (14 — Next-Gen)` : **`0.36.2-10`**
> - **Références Officielles :** [Paquet Debian Trixie (`ufw`)](https://packages.debian.org/trixie/ufw) &nbsp;·&nbsp; [Paquet Debian Forky (`ufw`)](https://packages.debian.org/forky/ufw) &nbsp;·&nbsp; [Documentation Officielle Debian](https://wiki.debian.org/Uncomplicated%20Firewall%20%28ufw%29)
> - **Note d'Ingénierie (Divergence 13 vs 14) :** Sous Debian 13 (Trixie) et Debian 14 (Forky), UFW s'appuie en coulisses sur le backend noyau `nftables` et les blocages kernel se consultent directement via `journalctl -k | grep UFW`.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Afficher les Encarts Ligne de Commande : Debian 13 (Trixie — Stable) vs Debian 14 (Forky — Next-Gen)</b></summary>

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Profil Production Stable — Commandes pour `Debian 13 (Trixie)`
```bash
# Debian 13 (Trixie) — UFW adosse au backend noyau nftables :
sudo apt update && sudo apt install -y ufw nftables
sudo ufw status verbose && sudo nft list ruleset
```

#### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Profil Anticipation Next-Gen — Commandes pour `Debian 14 (Forky)`
```bash
# Debian 14 (Forky) — Journalisation pare-feu via systemd-journald (sans rsyslog) :
sudo journalctl -k | grep -i 'UFW BLOCK'
sudo systemctl status ufw.service
```

</details>
<!-- DEBIAN-TRUTH-END -->

<!-- CIEL-PEDAGOGY-START -->
<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** Le **Pare-feu Linux (Nftables / UFW)** filtre les paquets réseau au niveau du sous-système noyau **Netfilter** selon les chaînes d'entrée (`INPUT`), de sortie (`OUTPUT`) et de routage (`FORWARD`) en s'appuyant sur le suivi d'état des connexions (*Connection Tracking* : `NEW`, `ESTABLISHED`, `RELATED`).
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Fichiers & Commandes :** `/etc/nftables.conf`, `/etc/ufw/` &nbsp;|&nbsp; **Validation officielle :** `sudo nft -c -f /etc/nftables.conf` (vérification à blanc sans application), `sudo nft list ruleset`, `sudo ufw status verbose`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Avant d'appliquer une politique par défaut restrictive (`policy drop` ou `ufw default deny incoming`) sur un serveur distant, validez impérativement la règle autorisant votre port d'administration SSH. Sous Debian 12, 13 et 14, **Nftables** remplace `iptables` en unifiant IPv4/IPv6 (`inet`) et les ensembles d'adresses (*Sets*) haute performance.
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Wiki Officiel Netfilter / Nftables](https://wiki.nftables.org/) &nbsp;·&nbsp; [Wiki Officiel Debian Nftables](https://wiki.debian.org/nftables) &nbsp;·&nbsp; [Documentation Ubuntu/Debian UFW](https://wiki.debian.org/Uncomplicated%20Firewall%20%28ufw%29)

</details>
<!-- CIEL-PEDAGOGY-END -->


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="18" height="18" align="absmiddle" alt="" /> TP – Associer UFW avec Fail2ban sur Debian 12 (Bookworm), Debian 13 (Trixie) & Debian 14 (Forky)

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> Sommaire
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />
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

<a id="1-pourquoi-associer-ufw-et-fail2ban-"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // 1. Pourquoi associer UFW et Fail2ban ?
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<a id="4-intégration-ufw--fail2ban"></a>
### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> UFW
- Définit des **règles réseau statiques** (ports ouverts ou fermés).
- Exemple : « J’autorise SSH, j’interdis tout le reste ».  

<a id="3-installation-de-fail2ban"></a>
<a id="5-configuration-de-base-de-fail2ban"></a>
<a id="7-surveiller-laction-de-fail2ban"></a>
### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Fail2ban
- Surveille les **logs système** (SSH, Apache, FTP, etc.).
- Détecte les comportements suspects (**brute-force**, **scans**, etc.).
- Ajoute **dynamiquement** des règles dans UFW pour bannir les IP malveillantes.

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-alert.svg" width="18" height="18" align="absmiddle" alt="" /> **Sans Fail2ban** : un robot peut faire 1000 tentatives SSH.

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> **Avec Fail2ban** : au bout de 5 échecs → l’IP est bannie automatiquement dans UFW.

---

<a id="2-schéma-de-fonctionnement"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // 2. Schéma de fonctionnement
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>          Internet
>             |
>             v
>       [ Attaquant ] 
>    (brute-force SSH)
>             |
>             v
>    ┌───────────────────┐
>    │       SSHD        │
>    │  (/var/log/auth)  │
>    └───────────────────┘
>             |
>             v
>    ┌───────────────────┐
>    │     Fail2ban      │
>    │ Analyse les logs  │
>    │   "Trop d'échecs" │
>    └───────────────────┘
>             |
>             v
>    ┌───────────────────┐
>    │        UFW        │
>    │ Ajoute une règle  │
>    │ DENY → IP bannie  │
>    └───────────────────┘
>             |
>             v
>       Attaquant bloqué
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> **Résumé visuel** : Fail2ban est l’intelligence qui lit les logs, et UFW applique le blocage réseau.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // 3. Installation de Fail2ban
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Installer le paquet

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt update && sudo apt install fail2ban -y
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Vérifier le service

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> systemctl status fail2ban
> ```
<!-- CODE-WINDOW-END -->

- **Active (running)** → OK, Fail2ban fonctionne.
- Sinon, démarre-le :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo systemctl enable --now fail2ban
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // 4. Intégration UFW ↔ Fail2ban
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Par défaut, Fail2ban utilise `iptables`.  
On va lui dire d’utiliser **UFW comme backend**.

Éditer le fichier `/etc/fail2ban/jail.local` (le créer s’il n’existe pas) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> [DEFAULT]
> banaction = ufw
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> **Astuce** : ainsi, chaque bannissement est directement visible dans :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw status
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 06 // 5. Configuration de base de Fail2ban
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Copie de sécurité :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Exemple minimal pour SSH
Éditer `/etc/fail2ban/jail.local` :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> [sshd]
> enabled  = true
> port     = ssh
> filter   = sshd
> logpath  = /var/log/auth.log
> maxretry = 5
> bantime  = 600
> ```
<!-- CODE-WINDOW-END -->

- **maxretry = 5** → 5 tentatives ratées avant bannissement.  
- **bantime = 600** → IP bannie 10 minutes.  
- **logpath** = chemin des logs surveillés.  

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> **Exemple concret** : un attaquant essaie 20 mots de passe SSH → son IP est bannie pendant 10 min.

---

<a id="6-scénarios-concrets-de-protection"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 07 // 6. Scénarios concrets de protection
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> 6.1 SSH
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Par défaut, Fail2ban protège déjà `sshd`. 
Mais tu peux personnaliser :  

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> [sshd]
> enabled  = true
> port     = 2266
> maxretry = 3
> bantime  = 1800
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Concrètement : ton SSH est sur le port 2266, après 3 échecs l’IP est bannie 30 min.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> 6.2 Nginx / Apache
Protection contre les échecs d’auth HTTP :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> [nginx-http-auth]
> enabled = true
> port    = http,https
> filter  = nginx-http-auth
> logpath = /var/log/nginx/error.log
> maxretry = 3
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Concret : un pirate qui tente 3 mauvais logins via `.htpasswd` est bloqué.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> 6.3 FTP (vsftpd)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```ini
> [vsftpd]
> enabled  = true
> port     = ftp
> filter   = vsftpd
> logpath  = /var/log/vsftpd.log
> maxretry = 5
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Concret : bloque les brute-force FTP.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> 6.4 Autres services
Fail2ban fournit des **filtres prêts à l’emploi** pour :  
- Postfix / Dovecot (mail)  
- ProFTPD / Pure-FTPd  
- Nginx / Apache  
- MySQL / MariaDB  

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Liste disponible dans `/etc/fail2ban/filter.d/`.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 08 // 7. Surveiller l’action de Fail2ban
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Lister les prisons actives

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo fail2ban-client status
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Vérifier SSH

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo fail2ban-client status sshd
> ```
<!-- CODE-WINDOW-END -->

Exemple de sortie :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> Status for the jail: sshd
> |- Filter
> |  |- Currently failed: 2
> |  `- Total failed: 15
> `- Actions
>    |- Currently banned: 1
>    `- Total banned: 3
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Vérifier UFW

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw status
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Concret : tu verras des lignes comme :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> Anywhere DENY IN  from 203.0.113.42
> ```
<!-- CODE-WINDOW-END -->

---

<a id="8-bonnes-pratiques"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 09 // 8. Bonnes pratiques
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **Personnaliser** `maxretry` et `bantime` selon ton contexte.  
- **Ne pas activer toutes les prisons** → seulement celles nécessaires (évite les faux positifs).  
- **Surveiller les logs** de Fail2ban :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   journalctl -u fail2ban -f
> ```
<!-- CODE-WINDOW-END -->

- **Coupler UFW + Fail2ban + Fail2ban-recidive** (bannissements longs pour récidivistes).  
- **Sauvegarder** ton fichier `/etc/fail2ban/jail.local`.  

---

<a id="-conclusion"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Conclusion
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **UFW** = mur statique.  
- **Fail2ban** = vigile intelligent.  
- Ensemble, ils forment une **défense en profondeur** :  
  - UFW ferme les portes.  
  - Fail2ban repère et expulse les intrus insistants.  

    Prochaine étape : intégrer **CrowdSec** pour profiter d’une base communautaire d’attaques connues.

<!-- MASTER-FOOTER-START -->
<div align="center">
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/divider-hud.svg" alt="" width="100%" />

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/footer-master.svg" alt="0xCyberLiTech — Architecture Cyberdéfense, Ingénierie Déterministe & IA Souveraine" width="100%" />
</a>

<p align="center"><a href="https://0xcyberlitech.com/"><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/badge-antigravity.svg" alt="Architecturé par Marc & Antigravity (Google DeepMind)" width="520" /></a></p>

<sub><b>Architecturé &amp; Forgé par Marc &amp; Antigravity (Google DeepMind)</b> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/"><b>0xcyberlitech.com</b></a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/soc-rd.html">Architecture SOC Cockpit v5.5</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/jarvis-rd.html">Architecture JARVIS Mark-VII</a> &nbsp;·&nbsp; <a href="https://0xcyberlitech.com/blueprint-jarvis.html">Blueprint Matériel RTX 5080</a></sub>

</div>
<!-- MASTER-FOOTER-END -->
