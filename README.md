# Activemq

# Lancer ActiveMQ avec Docker

## Introduction
Voici comment lancer ActiveMQ à l'aide de Docker pour différentes versions. L'objectif est d'exécuter un serveur ActiveMQ de manière simple et rapide en utilisant Docker. Nous allons détailler les principales commandes Docker, notamment `docker-compose up -d` pour démarrer ActiveMQ en arrière-plan, et `docker container ls` pour vérifier les conteneurs en cours d'exécution.

Pour chaque version d'ActiveMQ, les étapes suivantes restent similaires. Vous pouvez adapter le fichier `docker-compose.yml` en fonction de la version que vous souhaitez utiliser.

---

# Explication des Commandes Docker avec ActiveMQ

## 1. `docker-compose up -d`

### Contexte : ActiveMQ
ActiveMQ est un broker de messages, utilisé pour permettre la communication entre différentes applications via des files d'attente et des sujets. En utilisant Docker, on peut facilement déployer un serveur ActiveMQ.

- **Description** :
  La commande `docker-compose up -d` est utilisée pour démarrer ActiveMQ dans un conteneur Docker, en utilisant un fichier `docker-compose.yml` qui contient la configuration nécessaire.  


## 2. `docker container ls`

- **Description** :
  Cette commande permet de lister tous les conteneurs Docker actuellement en cours d'exécution. Elle fournit des informations comme l'ID du conteneur, l'image utilisée, l'état actuel, le port exposé, etc.
