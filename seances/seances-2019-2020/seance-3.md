# Séance 3 - Sécurité des applications Web, suite (24/10/2019)

## Résumé de la séance

Au cours de cette séance, nous avons continué sur la lancé de la séance 2 d'introduction à la sécurité des applications Web en introduisant plusieurs nouvelles vulnérabilités dont :

- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)
- Directory Traversal
- File Upload (et les contournement de protection

Nous avons également abordé la notion de *shell* à distance, et la manière d'en mettre en place à partir des vulnérabilités précédemment citées. Enfin, différentes ressources ont été présentées afin de s'entraîner.

## Ressources utiles

- [Diapo utilisé pendant la séance](https://docs.google.com/presentation/d/1cIjUMn6p4bEAceIDbxXR7wyppB5SKHCB9dGoYIz9WUE/edit?usp=sharing)
- [Installation de ZAP](../../resources/misc/installation-zap.md) (de plus en plus recommandé au fil des séances Web..)
- [Hacksplaining](https://www.hacksplaining.com/lessons), le site utilisé pour apprendre et s'entraîner pendant la séance
- [Le répertoire Github de DVWA](https://github.com/ethicalhack3r/DVWA)  avec tuto d'installation sur différentes plateformes (en dur, en machine virtuelle, sous Docker). Personnellement, je trouve que Docker est le plus facile et rapide, mais il faut déjà connaître un peu, cf. [tuto d'introduction à Docker](../../resources/misc/introduction-docker.md) (attention l'installation n'est montrée que pour Linux, mais on trouve plein de tutos pour Windows sur internet)
- Les challenges de RootMe correspondant aux vulnérabilités présentés :
  - [File upload - Double extensions](https://www.root-me.org/fr/Challenges/Web-Serveur/File-upload-double-extensions)
  - [File upload - Type MIME](https://www.root-me.org/fr/Challenges/Web-Serveur/File-upload-type-MIME)
  - [File upload - Null byte](https://www.root-me.org/fr/Challenges/Web-Serveur/File-upload-null-byte)
  - [File upload - ZIP](https://www.root-me.org/fr/Challenges/Web-Serveur/File-upload-ZIP)
  - [Local File Inclusion](https://www.root-me.org/fr/Challenges/Web-Serveur/Local-File-Inclusion)
  - [Local File Inclusion - Double encoding](https://www.root-me.org/fr/Challenges/Web-Serveur/Local-File-Inclusion-Double-encoding)
  - [Remote File Inclusion](https://www.root-me.org/fr/Challenges/Web-Serveur/Remote-File-Inclusion)



