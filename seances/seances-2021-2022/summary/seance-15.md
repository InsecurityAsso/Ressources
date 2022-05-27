# Séance 15 - Obtention d'un tunnel inversé en exploitant la faille CVE-2017-9805
*10/03/2022*

## Explications théoriques
La faille CVE-2017-9805 est du type *Insecure Deserialization*, elle se base sur une version vulnérable de la librairie java `XStream` qui peut exécuter des commandes si on lui envoie une charge utile XML d'un certain type.

Nous avons mis en pratique cette faille pour obtenir d'une manière alternative un *reverse shell* dans la machine *Basic Pentesting* disponible sur vulnhub et tryhackme.

## Ressources
- https://blog.appsecco.com/detecting-and-exploiting-the-java-struts2-rest-plugin-vulnerability-cve-2017-9805-765773921d3d
- https://samsclass.info/124/proj14/p10xstruts.htm
- http://robwillis.info/2017/09/exploiting-apache-struts-cve-2017-9805/
- [Basic Pentesting (tryhackme)](https://tryhackme.com/room/basicpentestingjt)