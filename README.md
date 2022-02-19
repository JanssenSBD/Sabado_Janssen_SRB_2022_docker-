Voici une implémentation d'une architecture à 3 niveaux

* Niveau frontend: il hébergera l'application Web.
* Niveau intermédiaire : cela hébergera l'API, dans notre cas l'API REST
* Niveau base de données : il hébergera la base de données.

# Frontend et Backend

* frontend contiendra le code du frontend et son Dockerfile
* backend contiendra le code api et son Dockerfile

# Docker-compose

Dans notre ```docker-compose.yml``` nous avons trois services ```web```, ```api``` et ```mongo```.
