# Introduction à Docker

## Présentation générale de Docker

Docker un outil permettant de faire tourner des applications (ainsi que leurs dépendances) dans des environnements isolés appelés **conteneurs** (ou *containers* en anglais).

Docker présente des **avantages similaires à l'utilisation de machines virtuelle**, tels que :

- L'isolation des projets, ce qui permet d'éviter les conflits entre dépendances et plus de sécurité.
- La mise en place d'environnements consistants, c'est à dire qu'une application va tourner de la même manière sur toutes les machines où elle est déployée.

Contrairement aux autres systèmes de virtualisation (à droite sur le schéma ci-dessous), Docker n’embarque pas un système d’exploitation invité mais ne s’occupe que de la partie haut niveau (à gauche). Il utilise le noyau de l'hôte et ne fait fonctionner que le strict nécessaire sur les invités, ce qui permet d'énormes **gains en performance et portabilité par rapport aux machines virtuelles**.

![docker-vs-vm](https://i2.wp.com/blog.docker.com/wp-content/uploads/Blog.-Are-containers-..VM-Image-1-1024x435.png?ssl=1)

## Quelques notions sur la philosophie Docker

### Un processus par conteneur

Dans la vision Docker, un conteneur ne doit faire tourner qu'un seul processus. Ainsi dans le cas d'une stack LAMP (Linux, Apache, MySQL, PHP) nous devrons créer 3 conteneurs différents.

### Immutabilité

Un conteneur ne doit pas stocker de données qui doivent être pérennes, car il les perdra (à moins que vous les ayez pérennisées). Mais si vous souhaitez en local mettre une base de données dans un conteneur Docker, vous devez créer un volume pour que celui-ci puisse stocker les données de façon pérenne.

### Stateless vs Stateful

Dans le monde de Docker, vous allez souvent entendre parler de stateless et stateful, deux catégories de conteneurs, et vous devez savoir à quoi correspond chaque catégorie.

Si nous prenons le cas d'une base de donnée MySQL, celle-ci est stateful car elle stocke un état. Ainsi, si vous éteignez et rallumez votre base de données, vous la retrouverez dans le même état de fonctionnement.

Stateless est donc l'inverse : l'application ne stocke pas d'état. Vous pouvez prendre le cas du protocole HTTP, celui-ci est stateless. À chaque nouvelle requête HTTP, les mêmes séries d'actions seront réalisées.

## Cas d'usage de Docker

Les cas d'usages privilégiés pour l'utilisation de Docker sont les suivants :

- Le déploiement : plutôt que de *pull* un code source et effectuer des scripts de déploiement, il est plus simple de directement déployer un ensemble cohérent et packagé.
- Le développement : "si ça marche quelque part, ça marchera partout", alors on peut utiliser docker pour facilement tester différentes versions de dépendances, etc... Il est également facile de remonter un conteneur si un test vient le casser.
- L'installation d'applications : il est extrêmement rapide d'installer certaines applications livrées directement sous Docker comme nextcloud, bitwarden...

### Du Dockerfile au conteneur Docker

Un conteneur est lancé en exécutant une *image*. Autrement dit, une image est un conteneur statique, que l'on pourrait comparer à une *snapshot* de nos machines virtuelles. Lorsqu'on souhaite travailler avec un conteneur, on le déclare forcément à partir d'une image, qui présente tout ce qui est nécessaire pour lancer l'application (code, a runtime, bibliothèques, variables d'environnement, fichiers de configuration...).

Les images sont définies dans un **dockerfile**, un fichier texte décrivant une liste d'actions à effectuer pour créer l'image, par exemple configurer le système d'exploitation, installer les logiciels nécessaires, copier des fichiers...

![docker-build-run](https://miro.medium.com/max/700/1*p8k1b2DZTQEW_yf0hYniXw.png)

### Le Docker Hub

Afin de servir de base aux Dockerfile, des images prêtes à l'emploi sont mises à disposition sur le [Docker Hub](https://hub.docker.com/). Les plus populaires sont maintenues par Docker (marquées *official*) tandis qu'un grand nombres d'autres images proposées par la communauté. Ces images sont généralement bien documentées et la communauté disponible pour répondre aux questions.

## Installer et lancer Docker

> Nous détaillerons ici l'installation et le lancement de Docker sur un machine Debian, pour plus d'informations sur l'installation de Docker se référer à la [documentation en ligne](https://docs.docker.com/install/).

### Installation de Docker

Docker est disponible dans trois versions, une version *Community* et deux versions *Entreprise*. Nous ne nous intéresserons ici qu'à la version *Community*.

Il y a plusieurs manières d'installer Docker :

- Il est recommandé de mettre en place en répertoire Docker puis utiliser un gestionnaire de paquets comme *apt*.
- On peut également télécharger le paquet DEB et l'installer à la main, mais les mises à jour ne seront pas faites automatiquement.
- Pour d'autres environnements comme une Rasberry Pi Docker met à disposition des scripts d'installation (*convenience scripts*).

C'est la première méthode que nous utiliserons ici.

1. On commence par mettre à jour l'index de paquet *apt* :

```bash
sudo apt-get update
```

2. Installer les paquets qui permettent à *apt* de fonctionner à travers HTTPS :

```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common

```

3. Ajouter la clé PGP officielle de Docker

```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
```

On vérifie qu'on a bien la clé *9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88* en cherchant les 8 derniers caractères :

```bash
sudo apt-key fingerprint 0EBFCD88
```

4. Mettre en place le répertoire *stable*

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
```

> Remarque : pour une architecture un peu plus "exotique" comme un Raspberry Pi, voir https://withblue.ink/2019/07/13/yes-you-can-run-docker-on-raspbian.html

5. Mettre à jour l'index *apt* et installer docker :

```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### Tester Docker

On peut vérifier la version de Docker avec `docker --version` ou `docker --version` pour avoir plus d'informations sur l'installation Docker.

Afin de vérifier que l'installation s'est correctement déroulée, on peut lancer l'image *hello-world* avec :

```bash
sudo docker run hello-world
```

### Mettre à jour Docker

La mise à jour de Docker se fait alors comme n'importe quel paquet *apt* lors du prochain `sudo apt-get upgrade`.

### Désinstaller Docker

La suppression de Docker se fait comme pour tous paquet installé via *apt* avec :

```bash
sudo apt-get purge docker-ce
```

Les images, conteneurs, volumes et fichiers de configuration personnalisés ne sont pas automatiquement supprimés, on peut le faire en supprimant le dossier /var/lib/docker :

```bash
sudo rm -rf /var/lib/docker
```

### Lancement de Docker au démarrage

La plupart des distributions Linux utilisent `systemd` pour gérer les services à lancer au démarrage du système. Pour lancer Docker au démarrage du système on utilisera :

```bash
sudo systemctl enable docker
```

Et à l'inverse pour désactiver son lancement au démarrage :

```bash
sudo systemctl disable docker
```

Par défaut Docker est aussi configuré pour démarrer automatiquement avec `upstart`, ce comportement peut être désactivé avec :

```bash
echo manual | sudo tee /etc/init/docker.override
```

### Configuration optionnelles post-installation

D'autres configurations (nottamment réseau) peuvent être effectuées après installation, plus d'informations sur la [documentation en ligne](https://docs.docker.com/install/linux/linux-postinstall/).

## Gérer ses images et conteneurs

Lister les commandes du CLI Docker :

```bash
sudo docker
sudo docker image --help
sudo docker container --help
```

### Gestion des images

Lister les images :

```bash
sudo docker image ls      # liste uniquement les images en cours
sudo docker image ls -a   # liste toutes les images
```

Supprimer une image :

```bash
sudo docker image rm <image id>   # Supprime l'image spécifiée de la machine
sudo docker image rm $(sudo docker image ls -a -q)    # Supprime toutes les images
```

### Gestion des conteneurs

Lister les conteneurs :

```bash
$ sudo docker container ls      # Liste les conteneurs en cours d'exécution
$ sudo docker ps                # Idem, avec une autre syntaxe
$ sudo docker container ls -a   # Liste tous les conteneurs
```

Arrêter un conteneur :

```bash
sudo docker container stop <hash>   # Stoppe le conteneur spécifié
sudo docker container kill <hash>   # Force l'arrêt du conteneur spécifié
```

Supprimer un conteneur :

```bash
sudo docker container rm <hash>   # Supprime le conteneur spécifié de la machine
sudo docker container rm $(sudo docker container ls -a -q) # Supprime tous les conteneurs
```


## En pratique

Nous allons illustrer les concepts présentés précedemment par la création d'une petite application web Python.

Sans conteneurisation, la première chose à faire aurait été d'installer Python sur sa machine avant de porter l'environnement d'exécution en production. Avec Docker, on va utiliser un environnement d'exécution portable en tant qu'image, sans besoin d'installation. Enfin, nous allons inclure cette image Python avec le code de notre application, de manière à ce que notre code, ses dépendances et son environnement d'exécution soient groupés.

### Définition du Dockerfile

Nous allons commencer par créer le fichier `Dockerfile` suivant :

```dockerfile
# Utilise un environnement d'exécution Python officiel du Docker Hub en tant qu'image parent
FROM python:2.7-slim

# Change le répertoire courrant à /app et le copie dans le conteneur à /app également
WORKDIR /app
COPY . /app

# Installe les paquets Python spécifiés dans le requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Ouvre le port 80
EXPOSE 80

# Définit une variable d'environnement
ENV MESSAGE "Hello World"

# Exécute app.py au lancement du conteneur
CMD ["python", "app.py"]
```

Bien d'autres instructions peuvent entrer dans un Dockerfile telles que :

- ADD
- COPY
- ENV
- EXPOSE
- FROM
- LABEL
- STOPSIGNAL
- USER
- VOLUME
- WORKDIR

### Création de l'application

Toujours dans le même répertoire, on crée le fichier `requirements.txt` qui spécifie les paquets Python requis par notre application :
```
Flask
Redis
```

Puis on crée le fichier `app.py`, qui est une simple page web :
```python
from flask import Flask
from redis import Redis, RedisError
import os
import socket

redis = Redis(host="redis", db=0, socket_connect_timeout=2, socket_timeout=2)

app = Flask(__name__)

@app.route("/")
def hello():
    try:
        visits = redis.incr("counter")
    except RedisError:
        visits = "<i>cannot connect to Redis, counter disabled</i>"

    html = "<h3>Hello {name}!</h3>" \
           "<b>Hostname:</b> {hostname}<br/>" \
           "<b>Visits:</b> {visits}"
    return html.format(name=os.getenv("NAME"), hostname=socket.gethostname(), visits=visits)

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

Notre application se contente d'afficher la variable d'environnement NAME suiviez de la valeur de socket.gethostname(). Enfin, puisque Redis n'est pas entrain de tourner (puisque nous avons simplement installé la bibliothèqe Python, pas Redis en lui même), nous devrions avoir un message d'erreur.

> Remarque : accéder au nom d'hôte dans un conteneur revient à accéder à son ID, qui similaire à l'ID d'un processus en cours sur une machine.

### Build l'application

Afin de construire l'image il suffit de lancer :
```bash
$ sudo docker build -t firstapp .
```

L'argument `-t` (ou `--tag`) permet de nommer l'image que nous allons créer.

L'image officielle Python spécifiée va alors automatiquement être téléchargée depuis le Docker Hub, puis le dossier copié et les *requirements* téléchargés, comme spécifié dans le Dockerfile.

On peut vérifier que l'image a bien été créée en listant les images avec `sudo docker image ls`.

### Exécuter l'image

On lance ensuite le conteneur en exécutant l'image avec :

```bash
$ sudo docker run -p 4000:80 firstapp
```

Ici on a mapé le port 4000 de notre machine hôte avec le port 80 du conteneur à l'aide du paramètre `-p` (ou `--publish`).
On peut vérifier que l'application est bien lancée est accessible en visitant la page http://localhost:4000 :

![running](./Screenshot-20190819163716-399x123.png)

On peut lancer le conteneur en arrière plan en ajoutant l'argument `-d` (pour *detached*) :

```bash
sudo docker run -d --publish 4000:80 firstapp
```

On peut également "rentrer" dans le conteneur avec :

```
docker exec -ti <id_conteneur> <commande>
```


Pour stopper le conteneur on utilisera la commande suivante :
```bash
$ docker container stop firstapp
```

## Partager son image Docker

### La registry Docker

Une registry est un logiciel qui permet de partager des images à d'autres personnes. C’est un composant majeur dans l’écosystème Docker, car il permet :
- A des développeurs de distribuer des images prêtes à l’emploi et de les versionner avec un système de tags
- A des outils d’intégration en continu de jouer une suite de tests, sans avoir besoin d’autre chose que de Docker
- A des systèmes automatisés de déployer ces applications sur vos environnement de développement et de production.

Tout comme GitHub, le Docker Hub nous donne la possibilité de créer des répertoires pour partager nos images. Il est aussi possible d'[héberger soit même ses images](https://docs.docker.com/datacenter/dtr/2.2/guides/).

Pour l'exemple, nous allons simplement utiliser les répertoires publiques mis à disposition par le Docker Hub, pour cela on commence par créer un compte sur https://hub.docker.com/ puis on peut se connecter avec :
```bash
$ sudo docker login
```

### Tagger et uploader l'image

La notation pour associer une image locale à un répertoire est *username/repository:tag*. Le tag est optionnel mais recommandé puisqu'il s'agit du mécanisme utilis épour donner une versions aux images Docker.

Dans notre cas on va simplement placer l'image dans le répertoire *get-started* et l'appeller *part2*, pour cela on utilise la commande :

```bash
$ sudo docker tag image jbedel/get-started:part2
```

Afin d'uploader l'image on utilise ensuite :

```bash
$ sudo docker push jbedel/get-started:part2
```

### Utiliser notre image

On peut ensuite récupérer l'image et la lancer simplement avec :
```bash
$ sudo docker run -p 4000:80 jbedel/get-started:part2
```

C'est là que la magie opère, peu importe d'où est lancée cette commande on retrouvera le même environnement que celui que nous avions lancé localement !

## Stack de conteneurs

De manière générale, une application est constituée de différents services, chacun avec ses fonctionnalités propres. Dans la philosophie de Docker, chaque service va correspondre à une image qui va interagir avec les autres, utiliser les ressources machines, etc.. Nous appelons stack un ensemble de conteneurs Docker lancés via un seul et unique fichier (docker-compose). 

### Principe de Docker Compose

Docker Compose est un outil écrit en Python qui permet de décrire, dans un fichier YAML, plusieurs conteneurs comme un ensemble de services. 

Si vous souhaitez lancer la création de l'ensemble des conteneurs, vous devez lancer la commande `docker-compose up` (pour rappel, vous faites un `docker run` pour lancer un seul conteneur). Comme pour une seule image, vous pouvez ajouter l’argument -d pour faire tourner les conteneurs en tâche de fond.

De même on pourra consulter l'état des stacks courants avec `docker-compose ps`, arrêter notre stack avec `docker-compose stop`, supprimer l'ensemble avec `docker-compose down` et voir les logs des conteneurs avec `docker-compose logs -f --tail 5`.

### Le docker-compose.yml

Vous devez commencer par créer un fichier `docker-compose.yml` à la racine de votre projet. Dans celui-ci, nous allons décrire l'ensemble des ressources et services nécessaires à la réalisation de votre POC.

```YAML
version: '3' # version du Docker Compose, la 3 est la plus répandue

services: # ensemble de nos conteneurs

    wordpress:
        depends_on: # crée une dépendance entre conteneurs et ordre de création
            - db
        image: wordpress:latest
        ports: # expose le port de l'extérieur (machine hôte) vers le conteneur
            - "8000:80"
        restart: always
        environment:
            WORDPRESS_DB_HOST: db:3306
            WORDPRESS_DB_USER: wordpress
            WORDPRESS_DB_PASSWORD: wordpress
            WORDPRESS_DB_NAME: wordpress

    db:
        image: mysql:5.7 # ou build pour indiquer un chemin de Dockerfile
        volumes: # volume pour faire persister les données sur disque
            - db_data:/var/lib/mysql
        restart: always # redémarre automatiquement en cas d'erreyr
        environment:
            MYSQL_ROOT_PASSWORD: somewordpress
            MYSQL_DATABASE: wordpress
            MYSQL_USER: wordpress
            MYSQL_PASSWORD: wordpress

volumes:
    db_data: {}

```

On peut vérifier la syntaxe avec `docker-compose config`.

## Les volumes Docker

Les volumes permettent de persister la donnée, éventuellement pour plusieurs conteneurs.

La manière simple et intuitive de linker les deux est d'utiliser le paramètre `-v <répertoire-hôte>:<répertoire-conteneur>` avec `docker run`.

## Les réseaux Docker

## Bonnes pratiques

https://openclassrooms.com/fr/courses/2035766-optimisez-votre-deploiement-en-creant-des-conteneurs-avec-docker



## Swarm

docker swarm init
docker stack deploy -c docker-compose.yml getstartedlab
docker service ls / docker stack services getstartedlab
docker service ps getstartedlab_web

Un conteneur unique tournant dans un service est appelé *task*. Les tâches ont un ID unique incrémental en fonction du nombre de répliques définies dans le docker-compose.yml. On peut les lister avec: docker service ps getstartedlab_web


## Stack


## Docker Compose

Docker Compose est un outil qui permet de décrire (dans un fichier YAML) et gérer (en ligne de commande) plusieurs conteneurs comme un ensemble de services inter-connectés. Si je travaille sur une application Rails, je vais par exemple décrire un ensemble composé de 3 conteneurs :

- Un conteneur PostgreSQL
- Un conteneur Redis
- Un conteneur pour le code de mon application

Je pourrai alors démarrer mon ensemble de conteneurs en une seule commande docker-compose up. Sans Docker Compose, j’aurais dû lancer 3 commandes docker run avec beaucoup d’arguments pour arriver au même résultat. Par ailleurs, cela aurait  nécessité que je rédige un README plutôt précis pour que les autres membres de mon équipe obtiennent le même résultat. Avec Docker Compose, cette configuration est faite dans un fichier qui est versionné avec le reste du code de l’application.

Dans le fichier docker-compose.yml, chaque conteneur est décrit avec un ensemble de paramètres qui correspondent aux options disponibles lors d’un docker run : l’image à utiliser, les volumes à monter, les ports à ouvrir, etc. Mais on peut également y décrire des éléments supplémentaires, comme la possibilité de « construire » (docker build) une image à la volée avant d’en lancer le conteneur.

https://web.leikir.io/docker-compose-un-outil-desormais-indispensable/ 
https://blog.myagilepartner.fr/index.php/2017/01/27/tutoriel-docker-compose/ 

