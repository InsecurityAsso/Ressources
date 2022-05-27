# Séance 6 - Introduction au test d'intrusion
*11/11/2021*

Attaque d'une machine déployée à distance dont on ne connait que l'adresse IP jusqu'à obtenir les droits superutilisateurs dessus.

## Méthodologie mise en oeuvre
- scan de ports avec `nmap`
- énumération de répertoires avec `gobuster`
- obtention d'un *reverse shell* via l'upload d'un fichier `php` (avec contournement de filtre basique)
- élevation des privilèges via un programme au bit `SUID` activé

## Ressources utilisées
- [Salle "RootMe" du site tryhackme.com](https://tryhackme.com/room/rrootme)