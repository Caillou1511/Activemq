# Activemq

## Lancer ActiveMQ avec Docker


### Introduction
Voici comment lancer ActiveMQ à l'aide de Docker pour différentes versions. L'objectif est d'exécuter un serveur ActiveMQ de manière simple et rapide en utilisant Docker. Nous allons détailler les principales commandes Docker, notamment `docker-compose up -d` pour démarrer ActiveMQ en arrière-plan, et `docker container ls` pour vérifier les conteneurs en cours d'exécution.

Pour chaque version d'ActiveMQ, les étapes suivantes restent similaires. Vous pouvez adapter le fichier `docker-compose.yml` en fonction de la version que vous souhaitez utiliser.

---

## Explication des Commandes Docker avec ActiveMQ

### 1. `docker-compose up -d`

- La commande `docker-compose up -d` est utilisée pour démarrer ActiveMQ dans un conteneur Docker, en utilisant un fichier `docker-compose.yml` qui contient la configuration nécessaire.  


### 2. `docker container ls`

- Cette commande permet de lister tous les conteneurs Docker actuellement en cours d'exécution. Elle fournit des informations comme l'ID du conteneur, l'image utilisée, l'état actuel, le port exposé, etc.

## Faire un scan de l'adresse ip d'ActiveMQ.


### 1. `ip a`

- Cette commande permet de lister toutes les interfaces. Elle nous permet d'identifier l'interface qui est active (UP) et voir qu'elle est l'adresse IP associée à celle-ci.

### 2. `nmap -p- 'adresse ip' `

- Cette commande nous permet de faire un scan pour identifier tous les ports utilisée par ActiveMQ

[ActiveMQ_2015](ActiveMQ_2015.md)  
[ActiveMQ_2016](ActiveMQ_2016.md)  
[ActiveMQ_2022](ActiveMQ_2022.md)  
[ActiveMQ_2023](ActiveMQ_2023.md)  
