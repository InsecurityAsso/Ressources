# Séance 9 - L'élévation de privilèges Linux (17/12/2020)

## Résumé de la séance

Au cours de cette séance, nous avons introduit la notion d'élévation de privilèges sur systèmes Linux, puis nous sommes entraînés sur la machine virtuelle.

## Présentation

Nous avons présenté ([diapo ici](https://docs.google.com/presentation/d/1dD80CMaMEdxmI1-ipBDsdudpNTHWSYxJuIsweyw30Mo/edit#slide=id.ga90b7aca8f_0_150)) les grands principes des privilèges et les vulnérabilités permettant leur élévation :

- Bash (Shell Unix, Commandes, Redirection de flux, Variables d'environnement..)
- Permissions Linux (Principe, Commandes)
- Principes et faiblesses de :
  - Sudo
  - Programmes SUID/GUID
  - Processus avec privilèges
  - cron
  - Exploits Noyaux
- Outils et ressources (Scanners, GTFOBins, Cheat Sheets..)
- Entraînements (OverTheWire, Root Me, Nebula)

## Challenges

Nous nous sommes ensuite entraînés sur la machine virtuelle Nebula, que l'on peut télécharger [ici](https://www.vulnhub.com/entry/exploit-exercises-nebula-v5,31/) (+ quelques instructions pour l'installation [ici](https://sp1icersec.wordpress.com/2018/09/07/exploit-exercises-nebula-setup/)). Il s'agit d'un live CD devant simplement être inséré dans la machine virtuelle pour fonctionner, le tout sans installation.

PS: sous Mac désactiver la carte son peut aider à éviter un crash au lancement.

La VM se présente sous la forme de niveaux, correspondants chacun a un utilisateur dont on veut élever les privilèges. Les instructions pour chaque level se trouvent sur le site "exploit-exercices", mais à l'heure actuelle le site semble être en transfert entre http://exploit-exercises.com/nebula et https://exploit-exercises.lains.space/nebula/..

