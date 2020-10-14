

# Comment installer ZAP (proxy d'interception)

## Téléchargement

Rendez-vous sur https://github.com/zaproxy/zaproxy/wiki/Downloads et téléchargez la version correspondant à votre OS. En général les versions *Installer* sont plus faciles à installer que les *Package*.

Exécuter le fichier téléchargé (pour Linux, ne pas oublier de passer un petit `chmod +x` dessus pour donner les droits d’exécution) puis suivez les instructions.

## Configuration

Afin de "connecter" le proxy d'interception avec votre navigateur Web, quelques étapes sont à suivre.

### Ajouter le certificat du proxy à votre navigateur

Afin que les sites HTTPS acceptent d'être interceptés par le proxy, il faudra ajouter le certificat de ZAP à votre navigateur. Pour cela il suffit d'aller dans l'onglet `Tools > Options > Dynamic SSL Certificates` de ZAP, et télécharger le certificat sur votre ordinateur avec `Save`.

Ensuite dans les propriétés de votre navigateur, cherchez une section *Certificat*, ça dépend au cas par cas mais par exemple pour Firefox :

![certificat-firefox](../data/images/certificat-firefox.png)

Et il suffit de cliquer sur `Importer` et on peut upload le fichier certificat que l'on vient de télécharge.

### Configurer le navigateur pour utiliser le proxy

Une fois le certificat installé, il faut littéralement *brancher* le proxy d'interception avec le navigateur. Là encore ça va dépendre au cas par cas du navigateur, mais pour Firefox on a un onglet `Proxy` disponible dans les paramètres réseau :

![certificat-firefox](../data/images/firefox-proxy-1.png)

On le paramètre comme suit pour le bancher au proxy :

![certificat-firefox](../data/images/firefox-proxy-2.png)

Attention, lorsque ZAP est fermé il faut bien penser à désactiver le proxy, car sinon vous ne pourrez pas accéder à internet !**

> Remarque : il existe des extensions permettant de passer rapidement d'une configuration à une autre sans avoir besoin d'aller chercher dans les paramètres du navigateur.
> Par exemple Proxy Switcher, FoxyProxy....

## Utilisation de ZAP

Afin de bloquer les requêtes avec ZAP, il suffit d'appuyer sur un bouton rouge, puis on peut passer pas à pas avec les flèches.

![certificat-firefox](../data/images/zap-utilisation.png)