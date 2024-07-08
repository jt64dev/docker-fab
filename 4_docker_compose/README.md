# Docker-compose

Permet d'ordonnancer et de lancer plusieurs containers.
Partage un réseau commun entre les containers.

Exemple de technos souvent déployées en une ligne de commande:
* LAMP - Linux, Apache, Mysql, PHP
* MEAN - MongoDB, Express, Angular, Node.js
* VPEN - VueJs, PostgresDB, Express, Node.js
* PREN - PostgresDB, React, Express, Node.js

## Vérifier si présent ou installer le
    
    docker-compose

## Mise en oeuvre en génral

  Ecrire un fichier Dockerfile pour le container    
  
  Ecrire un fichier **docker-compose.yaml** avec l'ensemble des services, ports, ...    
  
  Exécuter la commande **docker-compose up**    


## Commandes de base 

Afficher la liste des commandes (une vingtaine en tout)

    docker-compose

Création et démarrage des containers

    docker-compose up

Start services with detached mode
    
    docker-compose -d up

Start specific service
     
     docker-compose up <service-name>

List images
     
     docker-compose images

List containers
    
    docker-compose ps

Start service
    
    docker-compose start

Stop services
    
    docker-compose stop

Display running containers
    
    docker-compose top

Kill services
   
    docker-compose kill

Remove stopped containers
   
    docker-compose rm

Stop all contaners and remove images, volumes
  
    docker-compose down


## Installons un Wordpress

Créer un dossier worpress

    mkdir worpress
    cd worpress


Tester par vous même en lisant la doc sur: https://hub.docker.com/_/wordpress

donc en résumé créer un fichier **docker-compose.yml**

avec dedans
```
version: '3'

services:
   db:
     image: mysql:latest
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: mybigrootpassword
       MYSQL_DATABASE: wordpress
       MYSQL_USER: userwordpress
       MYSQL_PASSWORD: mysqlbigpass

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: on-failure
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: userwordpress
       WORDPRESS_DB_PASSWORD: mysqlbigpass
```
sauver le :)

puis pour construire et lancer les 2 containers:

    docker-compose up


Vérification

    docker ps

Et puis, aller tester Wordpress depuis votre navigateur sur

    http://localhost:8080


