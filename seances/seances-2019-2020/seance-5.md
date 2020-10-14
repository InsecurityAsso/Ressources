# Séance 5 - Sécurité des applications Web, attaque d'une machine virtuelle réaliste (28/11/2019)

## Résumé de la séance

Au cours de cette séance, nous avons continué sur notre lancé des vulnérabilités Web en attaquant la machine virtuelle LAMP Security CTF  4.

Accès à la machine :

- La VM peut être téléchargée directement en .ova ici : https://sourceforge.net/projects/lampsecurity/files/CaptureTheFlag/CTF4/
- Elle est également déployable directement sur RootMe via la section "CTF All The Day"

## Grandes étapes de résolution

L'attaque d'une machine virtuelle suit généralement les étapes suivantes :

- Scan de reconnaissance des services en cours sur la machine via nmap
- Si découvert d'un service web (HTTP/HTTPS) phase d'exploration du site :
  - Parcours de l'intégralité des pages
  - Découverte de pages via le fichier `robots.txt` et force brute via Dirbuster, dirsearch, etc..
  - Examen du code source des pages à la recherche de fonctionnalités sensibles, etc..
  - Examen de la surface d'attaque (quels sont les moyens pour un utilisateur d'envoyer de l'information qui sera traitée par le serveur)
  - Examen des requêtes et éventuelle alteration de ces dernières
- Découverte de vulnérabilités suite à l'exploration
- Exploitation de ces vulnérabilités

L'objectif final est d'obtenir un shell sur la machine, soit via certains protocoles permettant de se connecter comme SSH après découverte d'un mot de passe, soit en exploitant des vulnérabilités.