Voici une implémentation d'une architecture à 3 niveaux

* Niveau frontend: il hébergera l'application Web.
* Niveau intermédiaire : cela hébergera l'API, dans notre cas l'API REST
* Niveau base de données : il hébergera la base de données.

# Frontend et Backend

* frontend contiendra le code du frontend et son Dockerfile
* backend contiendra le code api et son Dockerfile

Nous définissons ```/usr/src/app``` comme répertoire de travail ```WORKDIR```. Nous émettons la commande ```COPY``` pour copier package.json dans le ```WORKDIR```, puis effectuons une installation ```npm```. Cela installera toutes les dépendances. Ensuite, nous copions le contenu du répertoire dans l'image. Nous exposons le port voulu avec la commande ```EXPOSE```, puis effectuons une commande ```node, index.js``` à l'aide de la commande ```CMD```.

# Docker-compose

Dans notre ```docker-compose.yml``` nous avons trois services ```web```, ```api``` et ```mongodb```.

* web : La configuration des ports sont au format n:m. Cela mappe le port m des conteneurs sur le port n de l'hôte, exposant ainsi l'application à l'hôte. Notre application de nœud s'exécute sur le port ```3000``` à l'intérieur du conteneur.

La configuration des réseaux n'a que l'interface réseau. Rappelez-vous que cette interface réseau est partagée à la fois par le service ```web``` et ```api```, ce qui signifie que ```web``` et ```api``` s'exécutent sur le même réseau et que ```web``` peut accéder à ```api```.

* api : Le service api a la ligne ```build : ./backend```. Cela indique à Docker de créer l'image API à l'aide du Dockerfile situé dans le répertoire backend.

Notre conteneur db est également connecté à network-backend. Étant donné que les conteneurs partagent le même réseau, le conteneur ```api``` pourra communiquer avec le conteneur ```mongodb```.

La configuration ```depend_on``` indique à docker de composer l'ordre dans lequel afficher les conteneurs. Dans notre cas,```mongodb``` sera démarré en premier suivi de ```api```.

* mongodb : Nous utilisons une image basée sur ```mongo```. La variable ```environment``` indiquent à docker d'initialiser le serveur ```MONGODB``` avec avec l'utilisateur et le mot de passe.

La section volumes mappe le répertoire init_sql_scripts au répertoire ```mongo:/data/db``` dans le conteneur. Tous les fichiers à l'intérieur seront exécutés en séquence une fois la base de données créée.

# Powershell

* Maintenat nous pouvons utiliser la commande ```docker-compose up --build```pour tout lancer. L'indicateur ```--build``` déclenchera la construction d'images si elles ne sont pas déjà construites.

* Pour supprimer nous allons utiliser la commande ```docker image ls``` pour identifier les images puis entrer la commande suivante ```docker image rm``` suivi de l' IMAGE ID ou des IMAGE ID.
pour supprimer les conteneurs on utilise la commande ```docker-compose down```.

* Pour stopper le conteneur, la commande suivante sera ```docker stop```.

