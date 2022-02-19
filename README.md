Voici une implémentation d'une architecture à 3 niveaux

* Niveau frontend: il hébergera l'application Web.
* Niveau intermédiaire : cela hébergera l'API, dans notre cas l'API REST
* Niveau base de données : il hébergera la base de données.

# Frontend et Backend

* frontend contiendra le code du frontend et son Dockerfile
* backend contiendra le code api et son Dockerfile

Nous définissons /usr/src/app comme répertoire de travail ```WORKDIR```. Nous émettons la commande ```COPY``` pour copier package.json dans le ```WORKDIR```, puis effectuons une installation ```npm```. Cela installera toutes les dépendances. Ensuite, nous copions le contenu du répertoire dans l'image. Nous exposons le port voulu avec la commande ```EXPOSE```, puis effectuons une commande ```node, index.js``` à l'aide de la commande ```CMD```.

# Docker-compose

Dans notre ```docker-compose.yml``` nous avons trois services ```web```, ```api``` et ```mongo```.
