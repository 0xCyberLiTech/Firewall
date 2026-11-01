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


# <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-crypto.svg" width="18" height="18" align="absmiddle" alt="" /> TP — Sécuriser Linux avec `iptables`

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Objectifs pédagogiques
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />
À la fin de ce TP, vous serez capable de :
- Comprendre la logique de fonctionnement de `iptables`.
- Créer un pare-feu basique et progressif.
- Tester et vérifier vos règles sans bloquer votre accès SSH.
- Sauvegarder et restaurer vos configurations.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-network.svg" width="18" height="18" align="absmiddle" alt="" /> 1. Qu’est-ce que `iptables` ?
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

`iptables` est un outil en ligne de commande permettant de **contrôler le trafic réseau** sous Linux.  
Il agit comme un **pare-feu** logiciel :

- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> Autoriser certains flux (web, SSH, ping, etc.)
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ko.svg" width="42" height="16" align="absmiddle" alt="[NON]" /> Bloquer ou rejeter les flux indésirables (attaques, scans, ports inutiles)
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-rd.svg" width="46" height="16" align="absmiddle" alt="[R&D]" /> Rediriger ou modifier des paquets

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> **En résumé :** c’est la "porte de sécurité" de votre machine.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> 2. Structure d’une règle
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

Une règle `iptables` suit cette logique :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> iptables -A [chaîne] [filtres] -j [action]
> ```
<!-- CODE-WINDOW-END -->

| Élément       | Exemple                         | Rôle                                      |
|---------------|---------------------------------|-------------------------------------------|
| `-A`          | `-A INPUT`                      | Ajouter une règle à une chaîne            |
| `-p`          | `-p tcp`                        | Spécifier un protocole (tcp, udp, icmp)   |
| `--dport`     | `--dport 22`                    | Port de destination                       |
| `-s` / `-d`   | `-s 203.0.113.42`               | IP source / IP destination                |
| `-j`          | `-j ACCEPT` / `DROP` / `REJECT` | Action appliquée au paquet                |

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 3. Les chaînes principales
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

`iptables` traite les paquets en fonction de **chaînes** :

| Chaîne    | Rôle                                       |
|-----------|--------------------------------------------|
| `INPUT`   | Trafic entrant vers la machine             |
| `OUTPUT`  | Trafic sortant depuis la machine           |
| `FORWARD` | Trafic traversant la machine (routage)     |

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 4. Les tables principales
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

| Table     | Usage                                      |
|-----------|--------------------------------------------|
| `filter`  | Filtrage classique (par défaut)            |
| `nat`     | Traduction/routage (NAT, redirections)     |
| `mangle`  | Modification avancée des paquets           |

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 5. Mise en pratique pas à pas
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Étape 1 — Vérifier les règles existantes

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -L -v -n
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Vous devriez voir des règles par défaut (souvent `ACCEPT` partout).

---

### Étape 2 — Nettoyer la configuration (<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-alert.svg" width="18" height="18" align="absmiddle" alt="" /> à ne faire que sur une VM/test)

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -F
> sudo iptables -X
> sudo iptables -t nat -F
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Votre pare-feu est maintenant vide.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Étape 3 — Définir une politique par défaut

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -P INPUT DROP
> sudo iptables -P FORWARD DROP
> sudo iptables -P OUTPUT ACCEPT
> ```
<!-- CODE-WINDOW-END -->

- On bloque **tout en entrée** sauf ce que l’on autorise explicitement.
- On autorise **tout en sortie**.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Étape 4 — Autoriser le trafic de base
- **Boucle locale (loopback)** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -i lo -j ACCEPT
> ```
<!-- CODE-WINDOW-END -->

- **Connexions déjà établies** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Ainsi, les réponses aux connexions sortantes (comme `apt update`) passent bien.

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Étape 5 — Autoriser services essentiels
- **SSH (port 22)** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
> sudo iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
> ```
<!-- CODE-WINDOW-END -->

- **Web (HTTP/HTTPS)** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -p tcp -m multiport --dports 80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
> sudo iptables -A OUTPUT -p tcp -m multiport --sports 80,443 -m state --state ESTABLISHED -j ACCEPT
> ```
<!-- CODE-WINDOW-END -->

- **Ping (ICMP)** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Étape 6 — Cas pratique : accès limité à un port
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Exemple : seul l’hôte `203.0.113.42` peut accéder au port `54321`.

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -p tcp -s 203.0.113.42 --dport 54321 -j ACCEPT
> sudo iptables -A INPUT -p tcp --dport 54321 -j DROP
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Étape 7 — Protection contre brute-force SSH
Limiter à **3 tentatives par minute** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
> sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update \
> --seconds 60 --hitcount 3 --name SSH -j DROP
> ```
<!-- CODE-WINDOW-END -->

---

### <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-target.svg" width="18" height="18" align="absmiddle" alt="" /> Étape 8 — Activer les logs

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables -A INPUT -j LOG --log-prefix "[IPTABLES BLOCK] " --log-level 4
> ```
<!-- CODE-WINDOW-END -->

<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Les journaux apparaîtront dans `/var/log/syslog` ou `/var/log/messages`.

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 6. Sauvegarder et restaurer
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- **Installation de l’outil de persistance (Debian/Ubuntu)** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo apt install iptables-persistent
> ```
<!-- CODE-WINDOW-END -->

- **Sauvegarder les règles** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables-save > /etc/iptables/rules.v4
> ```
<!-- CODE-WINDOW-END -->

- **Restaurer** :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> sudo iptables-restore < /etc/iptables/rules.v4
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> 7. Exemple de script complet (pare-feu basique)
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> #!/bin/bash
> # Script de configuration iptables (firewall.sh)
>
> # [R&D] Nettoyage des règles
> iptables -F
> iptables -X
> iptables -t nat -F
>
> #  Politiques par défaut
> iptables -P INPUT DROP
> iptables -P FORWARD DROP
> iptables -P OUTPUT ACCEPT
>
> #  Loopback
> iptables -A INPUT -i lo -j ACCEPT
>
> #  Connexions établies
> iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
>
> #  SSH sécurisé
> iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
> iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update \
> --seconds 60 --hitcount 3 --name SSH -j DROP
> iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
> iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
>
> #  Web
> iptables -A INPUT -p tcp -m multiport --dports 80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
> iptables -A OUTPUT -p tcp -m multiport --sports 80,443 -m state --state ESTABLISHED -j ACCEPT
>
> #  Port restreint
> iptables -A INPUT -p tcp -s 203.0.113.42 --dport 54321 -j ACCEPT
> iptables -A INPUT -p tcp --dport 54321 -j DROP
>
> #  Logging
> iptables -A INPUT -j LOG --log-prefix "[IPTABLES BLOCK] " --log-level 4
> ```
<!-- CODE-WINDOW-END -->

Rendre exécutable :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> chmod +x firewall.sh
> sudo ./firewall.sh
> ```
<!-- CODE-WINDOW-END -->

---

## <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-ok.svg" width="42" height="16" align="absmiddle" alt="[OK]" /> 8. Bonnes pratiques
<img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-section-cyan.svg" width="100%" alt="" />

- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-alert.svg" width="18" height="18" align="absmiddle" alt="" /> Toujours tester sur une **session SSH secondaire** avant de fermer la session principale.
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Documenter vos règles dans un fichier versionné (`git` par exemple).
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-doc.svg" width="18" height="18" align="absmiddle" alt="" /> Vérifier l’ordre des règles : `iptables -L -v -n --line-numbers`.
- <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/icons/wire-puzzle.svg" width="18" height="18" align="absmiddle" alt="" /> Préparer un script de remise à zéro si vous vous bloquez :

<!-- CODE-WINDOW-START -->
> [!CAUTION]
> <img src="https://raw.githubusercontent.com/0xCyberLiTech/0xcyberlitech/main/assets/glow-code-red.svg" width="100%" alt="TERMINAL // BLOC DE CODE" />
>
> ```bash
> #!/bin/bash
> iptables -F
> iptables -P INPUT ACCEPT
> iptables -P FORWARD ACCEPT
> iptables -P OUTPUT ACCEPT
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
