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
- **Livres Blancs &amp; 67 Podcasts Audio R&amp;D :** [Portail 0xCyberLiTech](https://0xcyberlitech.com/) &nbsp;·&nbsp; [Livre Blanc SOC Cockpit v5.5](https://0xcyberlitech.com/soc-rd.html) &nbsp;·&nbsp; [Livre Blanc JARVIS Mark-VII](https://0xcyberlitech.com/jarvis-rd.html) &nbsp;·&nbsp; [Blueprint Logiciel &amp; Matériel RTX 5080](https://0xcyberlitech.com/blueprint-jarvis.html)

</details>
<!-- CIEL-PEDAGOGY-END -->


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-threat.svg" width="18" height="18" align="absmiddle" alt="" /> Tutoriel UFW – Sécuriser son serveur Debian 12 (Bookworm), Debian 13 (Trixie) & Debian 14 (Forky) avec UFW

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> Sommaire :
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

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

<a id="1-pourquoi-un-pare-feu-"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // 1. Pourquoi un pare-feu ?
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **Filtrage entrant** : seuls les services voulus sont accessibles.
- **Filtrage sortant** : la machine ne parle qu’aux destinations autorisées.
- **Journalisation** : traçabilité des tentatives d’accès.

> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-alert.svg" width="18" height="18" align="absmiddle" alt="" /> Un serveur sans pare-feu expose tous ses services à Internet → c’est comme laisser toutes les portes et fenêtres ouvertes.

---

<a id="2-installation"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // 2. Installation
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt update && sudo apt install ufw -y
> ```
<!-- CODE-WINDOW-END -->

---

<a id="3-poser-les-bases--politique--deny-by-default-"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // 3. Poser les bases : politique « deny by default »
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> a) Tout bloquer en entrée par défaut

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw default deny incoming
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> b) Tout autoriser en sortie par défaut

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw default allow outgoing
> ```
<!-- CODE-WINDOW-END -->

---

<a id="4-autoriser-uniquement-les-services-nécessaires"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // 4. Autoriser Uniquement les Services Nécessaires
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> a) SSH (accès distant)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw allow ssh
> # ou
> sudo ufw allow 22/tcp
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> b) HTTP/HTTPS (serveur web)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw allow 80/tcp
> sudo ufw allow 443/tcp
> ```
<!-- CODE-WINDOW-END -->

---

<a id="5-schéma-explicatif--ouverture-de-ports"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 06 // 5. Schéma explicatif : Ouverture de ports
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> +-------------------+         +-------------------+
> |   Internet        |         |   Votre Serveur   |
> |                   |         |                   |
> |   [Client SSH]----|-------->|   [Port 22]       |
> |   [Client Web]----|-------->|   [Port 80/443]   |
> +-------------------+         +-------------------+
> ```
<!-- CODE-WINDOW-END -->

Seuls les ports explicitement ouverts (22, 80, 443) sont accessibles depuis l’extérieur.

---

<a id="6-limiter-les-tentatives-ssh-anti-brute-force"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 07 // 6. Limiter les Tentatives SSH (Anti-brute-force)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw limit ssh
> ```
<!-- CODE-WINDOW-END -->

---

<a id="7-activer-ufw"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 08 // 7. Activer UFW
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw enable
> ```
<!-- CODE-WINDOW-END -->

---

<a id="8-vérifier-les-règles-actives"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 09 // 8. Vérifier les Règles Actives
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw status verbose
> ```
<!-- CODE-WINDOW-END -->

---

<a id="9-activer-la-journalisation-ufw"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 10 // 9. Activer la Journalisation UFW
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw logging on
> ```
<!-- CODE-WINDOW-END -->

---

<a id="10-consulter-les-logs-ufw"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 11 // 10. Consulter les Logs UFW
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Tous les logs :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo journalctl | grep UFW
> ```
<!-- CODE-WINDOW-END -->

- Logs récents :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo journalctl -e | grep UFW
> ```
<!-- CODE-WINDOW-END -->

- Suivi en temps réel :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo journalctl -f | grep UFW
> ```
<!-- CODE-WINDOW-END -->

---

<a id="11-script-dinstallation-automatique"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 12 // 11. Script d’Installation Automatique
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> #!/bin/bash
>
> # Bloquer toutes les connexions entrantes
> sudo ufw default deny incoming
>
> # Autoriser toutes les connexions sortantes
> sudo ufw default allow outgoing
>
> # Autoriser SSH
> sudo ufw allow ssh
>
> # Limiter les tentatives SSH
> sudo ufw limit ssh
>
> # (Optionnel) Autoriser HTTP/HTTPS si serveur web
> # sudo ufw allow 80/tcp
> # sudo ufw allow 443/tcp
>
> # Activer UFW
> sudo ufw enable
>
> # Afficher le statut
> sudo ufw status verbose
> ```
<!-- CODE-WINDOW-END -->

Rendez-le exécutable et lancez-le :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> chmod +x setup-ufw.sh
> ./setup-ufw.sh
> ```
<!-- CODE-WINDOW-END -->

---

<a id="12-gestion-des-règles-ufw"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 13 // 12. Gestion des Règles UFW
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> a) Lister les règles avec leur numéro

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw status numbered
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> b) Supprimer une règle par son numéro

Exemple : pour supprimer la règle numéro 3 :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw delete 3
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> c) Modifier une règle

Supprimez la règle existante puis ajoutez la nouvelle :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw allow 2222/tcp
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> d) Désactiver UFW (toutes les règles)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw disable
> ```
<!-- CODE-WINDOW-END -->

---

<a id="13-exemples-de-règles-supplémentaires"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 14 // 13. Exemples de Règles Supplémentaires
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Autoriser un port UDP (ex : 1194 pour OpenVPN) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow 1194/udp
> ```
<!-- CODE-WINDOW-END -->

- Autoriser une plage d’IP à accéder à un port :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow from 192.168.1.0/24 to any port 3306
> ```
<!-- CODE-WINDOW-END -->

- Refuser une IP spécifique :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw deny from 203.0.113.42
> ```
<!-- CODE-WINDOW-END -->

- Autoriser un port pour une interface réseau spécifique :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow in on eth0 to any port 8080
> ```
<!-- CODE-WINDOW-END -->

- Autoriser un port pour une IP précise :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow from 10.0.0.5 to any port 22
> ```
<!-- CODE-WINDOW-END -->

- Refuser tout le trafic d’un pays (nécessite une liste d’IP) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   # Exemple avec un fichier d’IP
>   for ip in $(cat ips_country.txt); do sudo ufw deny from $ip; done
> ```
<!-- CODE-WINDOW-END -->

- Autoriser le ping (ICMP) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow proto icmp
> ```
<!-- CODE-WINDOW-END -->

- Refuser tout le trafic sortant sauf HTTP/HTTPS :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw default deny outgoing
>   sudo ufw allow out 80/tcp
>   sudo ufw allow out 443/tcp
> ```
<!-- CODE-WINDOW-END -->

- Autoriser le port SMTP (mail) :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow 25/tcp
> ```
<!-- CODE-WINDOW-END -->

- Autoriser le port FTP :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow 21/tcp
> ```
<!-- CODE-WINDOW-END -->

- Autoriser le port DNS :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow 53
> ```
<!-- CODE-WINDOW-END -->

- Autoriser le port MySQL pour une IP spécifique :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow from 192.168.1.100 to any port 3306
> ```
<!-- CODE-WINDOW-END -->

- Refuser tout sauf une IP sur SSH :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw deny ssh
>   sudo ufw allow from 203.0.113.10 to any port 22
> ```
<!-- CODE-WINDOW-END -->

- Autoriser le port NFS (2049) pour le réseau local :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow from 192.168.1.0/24 to any port 2049
> ```
<!-- CODE-WINDOW-END -->

- Autoriser le port pour une plage d’IP et une interface :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>   sudo ufw allow in on eth1 from 10.10.10.0/24 to any port 8080
> ```
<!-- CODE-WINDOW-END -->

---

<a id="14-schémas--flux-réseau-et-logique-ufw"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 15 // 14. Schémas : Flux réseau et logique UFW
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Schéma 1 : Flux réseau général

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>         +-------------------+
>         |   Internet        |
>         +--------+----------+
>                  |
>          [Ports non autorisés]
>                  X (bloqué)
>                  |
>          [Ports autorisés]
>                  |
>         +--------v----------+
>         |   Serveur UFW     |
>         +-------------------+
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Schéma 2 : Logique de décision UFW

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```yaml
> +-------------------+
> |   Paquet réseau   |
> +-------------------+
>          |
>          v
> +----------------------+
> |  Règle UFW existe ?  |
> +----------------------+
>    | Oui         | Non
>    v             v
> [Action]     [Bloqué]
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Schéma 3 : Exemple de filtrage par IP

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```yaml
> +-------------------+
> |   Internet        |
> +--------+----------+
>          |
>    [IP autorisée] --------> [Port ouvert]
>    [IP refusée]    --X--> [Bloqué]
> ```
<!-- CODE-WINDOW-END -->

---

<a id="15-bonnes-pratiques"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 16 // 15. Bonnes Pratiques
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Toujours tester l’accès SSH avant d’activer UFW sur un serveur distant.
- N’ouvrir que les ports strictement nécessaires.
- Activer la journalisation pour surveiller les accès.
- Mettre à jour régulièrement votre système.
- Documenter les règles appliquées pour faciliter la maintenance.

---

<a id="16-pour-aller-plus-loin"></a>
## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 17 // 16. Pour aller plus loin
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- [Documentation officielle Debian UFW](https://wiki.debian.org/Uncomplicated%20Firewall%20%28ufw%29)
- [Tutoriel DigitalOcean (FR)](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)
- [Manuel officiel Debian `ufw(8)` (Trixie)](https://manpages.debian.org/trixie/ufw/ufw.8.en.html)

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Conclusion du TP
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />
- En **débutant**, tu passes d’un serveur nu à un serveur protégé.  
- En **avancé**, tu transformes ton serveur en **citadelle** : cloisonné, surveillé, renforcé.  

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> La prochaine étape ? Associer UFW avec **Fail2ban** pour bloquer automatiquement les IP agressives <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> 

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
