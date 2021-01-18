# Séance 11 - Exercices sur TryHackMe (15/01/2021)

## Résumé de la séance

Au cours de cette séance, nous avons brièvement rappelé la méthodologie du test d'intrusion avant de passer l'attaque d'une machine virtuelle sur la plate-forme TryHackMe.

## Présentation

Nous sommes très rapidement passés sur le diapo de présentation du test d'intrusion ([dispo ici](https://docs.google.com/presentation/d/1S5Y8R5eJz3e_1dX639O5KEr1VdxCJ2Bn4gjLhS9p1cI/edit?usp=sharing)), en nous attardant sur :

- La méthodologie standard PTES  (Penetration Testing Execution Standard) et plus particulièrement :
  - Information Gathering
  - Vulnerability Analysis
  - Exploitation (cf. [séance 10](./seance-10.md))
  - Post-Exploitation (cf. [séance 9](./seance-9.md))
- Quelques outils indispensables pour attaquer le test d'intrusion
- La présentation du concept de Cheat Sheet

## TryHackMe

Nous sommes ensuite partis mettre en pratique les acquis des séances précédentes sur la room "Basic Pentesting" de TryHackMe (disponible [ici](https://tryhackme.com/room/basicpentestingjt)).

**Setup de la machine attaquante**

Comme c'était pour certain la première attaque de VM, nous avons pris le temps de discuter un peu du setup des outils.

Le plus pratique reste d'avoir une Kali (ou Parrot) à disposition avec toute la suite d'outils pré-installés ou facilement accessibles dans les dépôts, pour cela plusieurs options selon les goûts de chacun :

- Dans une machine virtuelle, très simple mais peut être coûteux en ressource
- Dans le WSL2, pratique et léger mais peut occasionner quelques galères car pas toujours au point, et les paquets sont à installer
- Bootable sur clé USB (soit "Live" soit installée en dur dessus)
- Directement sous TryHackMe dans le navigateur (1 fois par jour uniquement pour les non-premiums)

La plupart des outils étant ouverts et dans des langages multi-plateformes, il reste aussi la solution de les installer manuellement !

**Setup du VPN**

 TryHackMe utilise une connexion VPN pour joindre ses machines virtuelles, c'est un moyen de disposer d'instances séparées entre joueurs, et de mettre en place facilement des reverse-shell (entre autres avantages).

L'idée est donc de télécharger un fichier de configuration OpenVPN depuis son profil puis de l'utiliser avec un client OpenVPN (`$ sudo openvpn username.ovpn` sous linux).

**Attaque de la machine**

Nous avons ensuite effectués les actions suivantes sur la machine virtuelle "Basic Pentesting"

- Scan des ports ouverts avec `nmap`
- Scan des services tournant sur ces ports, toujours avec `nmap`
- Énumération de répertoires à l'aide de `gobuster` sur le serveur web du port 80
- Énumération d'utilisateurs à l'aide d'un partage SMB ouvert
- Bruteforce des credentials SSH à l'aide de `hydra`
- Récupération sur le serveur d'une clé SSH protégée par un mot de passe, crack avec `john`
- Élévation de privilèges avec un simple `sudo su`

Il existait plusieurs autres manières pour root la machine, disponibles sur des Walkthrough en ligne (Google "Basic Pentesting 1 VM walkthrough" devrait faire l'affaire si ça vous intéresse).

**Remarques**

La machine "Basic Pentesting" est également disponible en téléchargement sur VulnHub [ici](https://www.vulnhub.com/entry/basic-pentesting-1,216/).