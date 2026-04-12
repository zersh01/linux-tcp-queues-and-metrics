
[Русский](README.md) | [English](README_EN.md) | [**Français**]
---

# Files d'attente et métriques TCP sous Linux

Schéma détaillé du chemin de connexion TCP dans le noyau Linux : trafic entrant et sortant, files d'attente, raisons des abandons, métriques TcpExt, points d'entrée netfilter, conntrack et points d'optimisation.

![Schéma de la pile TCP Linux - Connexions entrantes et sortantes, files d'attente, métriques TcpExt](images/tcp-stack-ru.png)

## Éléments principaux du schéma

- **Connexion entrante** : Carte réseau → Tampon circulaire de réception → Netfilter (PREROUTING/INPUT) → File d'attente SYN → File d'attente d'acceptation → accept() → application

- **Connexion sortante** : application → send() → File d'attente de transmission → Netfilter (OUTPUT/POSTROUTING) → Carte réseau

- **Files d'attente et goulots d'étranglement clés** :

- Tampon circulaire de réception/transmission (ethtool -g)

- net.core.netdev_max_backlog

- File d'attente SYN TCP (tcp_max_syn_backlog)

- File d'attente d'acceptation TCP (somaxconn)

- Débordement de la table conntrack
- **Métriques** : TcpExt_* de /proc/net/netstat (ExtStats, ListenOverflows, ListenDrops, TCPBacklogDrop, etc.)

- **Causes des pertes et retransmissions** : délais d’attente, saturation de la mémoire, TFO, SACK, PAWS, etc.

Ce diagramme est conçu pour comprendre et déboguer rapidement les serveurs TCP à forte charge (Nginx, HAProxy, Envoy et similaires).

## Utilisation
- Téléchargez le fichier PNG/SVG pour vos présentations, articles, chaînes Telegram ou documentation.

- Il est recommandé de l’ouvrir en plein écran ou de le redimensionner (surtout pour le format SVG).

## Licence
Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)

Vous pouvez copier, distribuer et modifier ce document à condition de mentionner l’auteur et d’appliquer la même licence.

## Auteur
zersh01[](https://github.com/zersh01)

Projets associés :

- [iptables_interactive_scheme](https://github.com/zersh01/iptables_interactive_scheme) — diagramme interactif iptables/netfilter
