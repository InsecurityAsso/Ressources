# Séance 14 - Injections SQL *UNION-based* sur la machine `lampCTF4`
*03/03/2022*

## Exploitation d'une injection SQL
La machine LampCTF4 disponible sur root-me possède une faille permettant des injections SQL dans un paramètre GET de sa resource `index.html`. Nous avons exploité ce défaut pour afficher le contenu de la base données, notamment les hachés des mots de passe nous permettant ensuite de se connecter à distance à la machine et de la compromettre.

## Ressources utilisées
- [LampCTF4 sur vulnhub](https://www.vulnhub.com/entry/lampsecurity-ctf4,83/)
- [CTF all the day sur root-me](https://www.root-me.org/fr/Capture-The-Flag/CTF-all-the-day/)
- [Rapport de correction](https://github.com/10v5m1ch9n5/CTF/tree/main/LAMPSecurity/CTF4#sql-injectable-parameters)