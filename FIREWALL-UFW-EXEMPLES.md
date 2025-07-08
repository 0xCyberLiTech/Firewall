<!-- MASTER-HEADER-START -->
<div align="center">

<a href="https://0xcyberlitech.com/">
  <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/headers/header-firewall.svg" alt="0xCyberLiTech // Firewall" width="100%" />
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


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-shield.svg" width="20" height="20" align="absmiddle" alt="" /> FIREWALL UFW — Référentiel d'Exemples Pratiques & Durcissement sur Debian 12, 13 (Trixie) & 14 (Forky)

> **Objectif Opérationnel :** Disposer d'un catalogue complet de règles **UFW (Uncomplicated Firewall)** adossé au backend noyau **`nftables`** sous **Debian 12 (Bookworm)**, **Debian 13 (Trixie — Stable)** et **Debian 14 (Forky — Next-Gen)** : politiques par défaut Zero-Trust, limitation anti-brute-force SSH, filtrage par interface et sous-réseau VLAN, profils applicatifs et audit des journaux noyau via `journalctl`.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 01 // Initialisation Zero-Trust (Politique par Défaut)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Avant d'ouvrir des ports spécifiques, appliquez une politique implicite qui bloque tout trafic entrant et autorise le trafic sortant :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt update && sudo apt install -y ufw nftables
> sudo ufw default deny incoming
> sudo ufw default allow outgoing
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 02 // Protection du Service SSH (Port Standard ou Personnalisé & Anti-Brute-Force)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Toujours autoriser SSH **avant** d'activer UFW (`ufw enable`). La directive `limit` bloque automatiquement toute adresse IP effectuant plus de 6 tentatives de connexion en moins de 30 secondes :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> # Autoriser et limiter SSH sur le port standard 22/TCP :
> sudo ufw limit 22/tcp comment 'SSH Rate-Limit Anti-BruteForce'
>
> # Exemple sur un port SSH durci (ex: 2277/TCP) restreint a un sous-reseau d'administration :
> sudo ufw limit in on eth0 from 192.168.1.0/24 to any port 2277 proto tcp comment 'SSH Admin LAN'
> ```
<!-- CODE-WINDOW-END -->

Activez ensuite le pare-feu :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw enable
> sudo ufw status numbered
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 03 // Exemples par Rôles Serveurs (Web, DNS, Supervision, Base de Données)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Serveur Web (Apache2 / Nginx / Reverse Proxy)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw allow 80/tcp comment 'HTTP Web'
> sudo ufw allow 443/tcp comment 'HTTPS TLS'
> sudo ufw allow 443/udp comment 'HTTP/3 QUIC'
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Serveur de Supervision (Zabbix 7.4 / Nagios Core 4.5 / Checkmk 2.3+)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> # Zabbix Server (Agents Actifs sur 10051/TCP depuis le LAN) :
> sudo ufw allow from 192.168.1.0/24 to any port 10051 proto tcp comment 'Zabbix Active Checks'
>
> # Agent Zabbix 2 sur un hote supervise (uniquement depuis l'IP du serveur Zabbix) :
> sudo ufw allow from 192.168.1.100 to any port 10050 proto tcp comment 'Zabbix Server Poll'
>
> # Agent Checkmk TLS (6556/TCP) :
> sudo ufw allow from 192.168.1.100 to any port 6556 proto tcp comment 'Checkmk Agent TLS'
> ```
<!-- CODE-WINDOW-END -->

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Serveur de Base de Données (MariaDB / PostgreSQL — Accès Restreint)

Ne jamais exposer `3306/tcp` ou `5432/tcp` sur `Anywhere` (`0.0.0.0/0`). Autorisez exclusivement l'adresse IP du serveur applicatif :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo ufw allow from 192.168.1.50 to any port 3306 proto tcp comment 'MariaDB depuis App-Server'
> sudo ufw allow from 192.168.1.50 to any port 5432 proto tcp comment 'PostgreSQL depuis App-Server'
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 04 // Filtrage Avancé : Plages de Ports, Sous-Réseaux et Blocage Explicite (`deny` / `reject`)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> # Autoriser une plage de ports TCP (ex: ports passifs FTP ou WebRTC) :
> sudo ufw allow 50000:50100/tcp comment 'Plage Ports Passifs'
>
> # Bloquer silencieusement (DROP) une adresse IP malveillante en tete de liste (position 1) :
> sudo ufw insert 1 deny from 203.0.113.45 to any comment 'SOC Ban IP Malveillante'
>
> # Rejeter avec paquet TCP RST / ICMP Unreachable :
> sudo ufw reject out to 198.51.100.0/24 comment 'Blocage Sortie Reseau Tiers'
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-plan.svg" width="18" height="18" align="absmiddle" alt="" /> 05 // Administration, Suppression Numérotée et Audit `nftables` / `journalctl`
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> # Afficher toutes les regles avec leur numero d'ordre :
> sudo ufw status numbered
>
> # Supprimer la regle numero 4 :
> sudo ufw delete 4
>
> # Activer la journalisation UFW (low / medium / high) :
> sudo ufw logging low
>
> # Consulter en temps reel les paquets bloques par le noyau sous Debian 13 (Trixie) & Debian 14 (Forky) :
> sudo journalctl -k -f | grep -i 'UFW BLOCK'
> ```
<!-- CODE-WINDOW-END -->

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
