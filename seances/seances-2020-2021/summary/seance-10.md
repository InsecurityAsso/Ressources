# Séance 10 - Introduction au framework Metasploit (08/01/2021)

## Résumé de la séance

Au cours de cette séance, nous avons introduit des notions liés à l'exploitation de vulnérabilité, puis présenté de manière relativement détaillée le célèbre framework Metasploit. Enfin, nous nous sommes entraînés sur la machine virtuelle Metasploitable.

## Présentation

Nous avons présenté ([diapo ici](https://docs.google.com/presentation/d/17dXdPWzqqlOvskSKj08eaO1rygF0B78FrCQeSo7aYV0/edit?usp=sharing)) les grands principes touchant à l'exploitation de vulnérabilité ainsi que le framework Metasploit :

- Présentation générale : qu'est ce que Metasploit ?
- Notions de base : vulnérabilité, exploitation, CVE, exploit, shell, payload, stages, meterpreter, msfvenom
- Mise en pratique : scénario basique (msfconsole -> shell) et scénario avancé (msfvenom->meterpreter)
- Ressources : pour apprendre, pour développer, pour s'entraîner

## Metasploitable

Nous nous sommes ensuite entraînés sur la machine virtuelle Nebula, que l'on peut télécharger [ici](https://download.vulnhub.com/metasploitable/Metasploitable.zip). L'installation s'effectue de la manière suivante :

- On dispose d'un disque (format `.vmdk` ) que l'on peut importer directement sous Virtualbox ou VMWare sans installation
- On attribue les ressources que l'on souhaite à la VM (256Mo de RAM suffisent à la faire tourner)
- On configure son réseau à "Host-Honly" de manière à y accéder depuis l'hôte et éventuellement d'autres VM (ex: Kali)

La VM expose certains services vulnérables, dont certains sont exploitables avec Metasploit. Nous avons procédé de la manière suivante :

- Scan des ports ouverts et des services avec nmap
- Recherche de versions vulnérables et d'exploits (Google, cvedetails, searchsploit, Metasploit)
- Exploitation de la vulnérabilité `distcc` à l'aide de Metasploit
- Essaie de combinaisons de mots de passe par défaut pour le Tomcat présent sur le port 8180
- Une fois accès au panel administrateur de Tomcat, upload d'un payload (fait directement depuis Metasploit, puis avec MSFVenom)

Pour ceux qui aimeraient aller plus loins, des corrections +/- exhaustives se trouvent sur internet en cherchant *Metasploitable Walkthrough* ou *Metasploitable Writeups*. Pour ma part j'ai apprécié celle-ci que j'ai trouvé assez complète : https://charlesreid1.com/wiki/Metasploitable (cf. bas de page).