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
> [!TIP]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> **Guide de Lecture &amp; Progression par Niveau (Firewall)**
> - **Rôle de la brique :** Le **Pare-feu Linux (Nftables / UFW)** filtre les paquets réseau au niveau du sous-système noyau **Netfilter** selon les chaînes d'entrée (`INPUT`), de sortie (`OUTPUT`) et de routage (`FORWARD`) en s'appuyant sur le suivi d'état des connexions (*Connection Tracking* : `NEW`, `ESTABLISHED`, `RELATED`).
> - **Parcours recommandé :** **Niveau 1 (Fondamentaux &amp; Installation initiale)** pour déployer une base saine &rarr; **Niveau 2 (Configuration &amp; Intégration)** &rarr; **Niveau 3 (Haute Disponibilité, Durcissement &amp; Exploitation)**.

<details>
<summary><img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> <b>Synthèse d'Architecture, Standards Officiels &amp; Diagnostic (Niveau 1 : Fondamentaux · Niveau 2 : Repères · Niveau 3 : Diagnostic)</b></summary>

- **Niveau 1 — Fondamentaux &amp; Principe d'Architecture :** Le **Pare-feu Linux (Nftables / UFW)** filtre les paquets réseau au niveau du sous-système noyau **Netfilter** selon les chaînes d'entrée (`INPUT`), de sortie (`OUTPUT`) et de routage (`FORWARD`) en s'appuyant sur le suivi d'état des connexions (*Connection Tracking* : `NEW`, `ESTABLISHED`, `RELATED`).
- **Niveau 2 — Repères Officiels (Ports IANA, Fichiers Debian &amp; Commandes de Validation) :** **Fichiers & Commandes :** `/etc/nftables.conf`, `/etc/ufw/` &nbsp;|&nbsp; **Validation officielle :** `sudo nft -c -f /etc/nftables.conf` (vérification à blanc sans application), `sudo nft list ruleset`, `sudo ufw status verbose`.
- **Niveau 3 — Diagnostic d'Incidents &amp; Ingénierie Avancée :** **Diagnostic & Architecture :** Avant d'appliquer une politique par défaut restrictive (`policy drop` ou `ufw default deny incoming`) sur un serveur distant, validez impérativement la règle autorisant votre port d'administration SSH. Sous Debian 12, 13 et 14, **Nftables** remplace `iptables` en unifiant IPv4/IPv6 (`inet`) et les ensembles d'adresses (*Sets*) haute performance.
- **Sources de Vérité Officielles Éditeurs &amp; Standards :** [Wiki Officiel Netfilter / Nftables](https://wiki.nftables.org/) &nbsp;·&nbsp; [Wiki Officiel Debian Nftables](https://wiki.debian.org/nftables) &nbsp;·&nbsp; [Documentation Ubuntu/Debian UFW](https://wiki.debian.org/Uncomplicated%20Firewall%20%28ufw%29)
- **Livres Blancs &amp; 67 Podcasts Audio R&amp;D :** [Portail 0xCyberLiTech](https://0xcyberlitech.com/) &nbsp;·&nbsp; [Livre Blanc SOC Cockpit v5.5](https://0xcyberlitech.com/soc-rd.html) &nbsp;·&nbsp; [Livre Blanc JARVIS Mark-VII](https://0xcyberlitech.com/jarvis-rd.html) &nbsp;·&nbsp; [Blueprint Logiciel &amp; Matériel RTX 5080](https://0xcyberlitech.com/blueprint-jarvis.html)

</details>
<!-- CIEL-PEDAGOGY-END -->


## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // SOMMAIRE DES DOSSIERS TECHNIQUES — ATELIER FIREWALL // FILTRAGE RÉSEAU
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<div align="center">

| Projet                 | Description                                           | Accès Rapide                                                                                                                                                        |
|------------------------|-------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **IPTABLES**           | Introduction et configuration.                        | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](FIREWALL-IPTABLES-INTRODUCTION-CONFIGURATION.md)         |
| **UFW**                | Installation et configuration sur **Debian 12 & 13**. | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](FIREWALL-UFW-INTRODUCTION-INSTALLATION-CONFIGURATION.md) |
| **UFW EXEMPLES**       | Référentiel d'exemples pratiques & durcissement sur **Debian 12, 13 & 14**. | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](FIREWALL-UFW-EXEMPLES.md) |
| **SECURITE RENFORCEE** | Associer UFW avec Fail2ban.                           | [<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/btn-explore.svg" alt="Ouvrir le dossier" />](FIREWALL-Associer-UFW-avec-Fail2ban-sur-Debian-12-13.md) |

</div>

---

# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> **Qu'est-ce qu'un firewall ?**

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // Définition détaillée d’un Firewall
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Un **firewall** (pare-feu) est un dispositif matériel ou logiciel qui surveille, filtre et contrôle le trafic réseau entre différentes zones de confiance (ex : Internet ↔ réseau interne). Il applique des règles pour autoriser, refuser ou rediriger les paquets selon des critères précis : adresses IP, ports, protocoles, état de connexion, etc.

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Rôles principaux :
- **Filtrage** : Bloquer ou autoriser des flux selon des règles.
- **Journalisation** : Tracer les accès et tentatives.
- **Traduction d’adresses (NAT)** : Masquer ou rediriger des adresses IP.
- **Segmentation** : Isoler des zones (DMZ, LAN, WAN).
- **Inspection d’état** : Suivre l’état des connexions (stateful).

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // 1. Schéma général : Positionnement d’un firewall
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>    [Internet]
>         |
>    +----v----+
>    | Firewall|
>    +----+----+
>         |
>    [Réseau privé]
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // 2. Logique de décision d’un firewall (filtrage)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

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
> +------------------------+
> |  Règle correspondante ?|
> +------------------------+
>    | Oui         | Non
>    v             v
> [Action]     [Bloqué]
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // 3. Filtrage stateless vs stateful
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **Stateless** : Le firewall examine chaque paquet indépendamment, sans tenir compte du contexte.
- **Stateful** : Le firewall garde en mémoire l’état des connexions (ex : TCP SYN/ACK), ce qui permet de n’autoriser que les paquets attendus dans une session.

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Schéma : Suivi d’état (stateful)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> [Client] ---- SYN ----> [Firewall] ----> [Serveur]
>          <--- SYN/ACK --
>          ---- ACK ------>
> ```
<!-- CODE-WINDOW-END -->

Le firewall autorise les paquets de réponse uniquement s’ils correspondent à une connexion initiée.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 06 // 4. Translation d’adresses (NAT)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

La **NAT** (Network Address Translation) permet de faire correspondre des adresses IP privées à une adresse publique, pour masquer le réseau interne ou rediriger des ports.

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Schéma : NAT simple

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> [LAN: 192.168.1.10] --+
> [LAN: 192.168.1.11] --+--> [Firewall NAT] --> [Internet: 203.0.113.5]
> ```
<!-- CODE-WINDOW-END -->

Tous les flux sortants semblent provenir de l’IP publique du firewall.

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Schéma : Redirection de port (Port Forwarding)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> [Internet:203.0.113.5:2222] --> [Firewall NAT] --> [LAN:192.168.1.10:22]
> ```
<!-- CODE-WINDOW-END -->

Le firewall redirige le port 2222 externe vers le port 22 d’une machine interne.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 07 // 5. DMZ (Zone Démilitarisée)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Une **DMZ** est une zone réseau intermédiaire, isolée du LAN, où l’on place les serveurs accessibles depuis Internet (web, mail, etc.).  
Cela limite les risques pour le réseau interne en cas de compromission d’un serveur public.

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Schéma : DMZ

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
>            [Internet]
>                 |
>            +----v----+
>            | Firewall|
>            +----+----+
>                 |
>       +---------+----------+
>       |                    |
>    [DMZ]                [LAN]
> (serveurs web, etc.)   (PC internes)
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 08 // 6. Exemple de règles logiques (table de filtrage)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

| Source           | Destination      | Port | Action    | État connexion |
|------------------|-----------------|------|-----------|---------------|
| Internet         | DMZ (web)       | 80   | Autoriser | NEW/ESTABLISHED|
| Internet         | LAN             | *    | Refuser   | *             |
| LAN              | Internet        | 80   | Autoriser | ESTABLISHED   |
| DMZ              | LAN             | *    | Refuser   | *             |

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 09 // 7. Schéma éclaté : Flux réseau avec firewall, NAT et DMZ
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```yaml
> [Internet]
>     |
>     v
> +-------------------+
> |     Firewall      |
> |-------------------|
> | - Filtrage        |
> | - NAT             |
> | - Suivi d'état    |
> +---+-----------+---+
>     |           |
>    DMZ         LAN
> (serveur web) (PC internes)
> ```
<!-- CODE-WINDOW-END -->

- Le firewall filtre et traduit les adresses.
- Les flux autorisés vers la DMZ n’atteignent pas le LAN.
- Les connexions sortantes du LAN passent par la NAT.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 10 // 8. Résumé pédagogique
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- Un firewall contrôle le trafic selon des règles précises.
- Il peut être stateless (simple) ou stateful (plus sûr).
- Il gère la translation d’adresses (NAT) pour masquer ou rediriger.
- Il permet de segmenter le réseau (DMZ) pour limiter les risques.
- Les schémas aident à visualiser la logique et la circulation des flux.

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
