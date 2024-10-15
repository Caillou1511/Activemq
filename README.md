# Activemq

Pour lancer chacune des versions ActiveMQ on utilise un Docker qui nous permet de déployer le server grace a 
# Explication des Commandes Docker avec ActiveMQ

Pour commencer je vais expliquer comment lancer Activemq.

## 1. `docker-compose up -d`

### Contexte : ActiveMQ
ActiveMQ est un broker de messages, utilisé pour permettre la communication entre différentes applications via des files d'attente et des sujets. En utilisant Docker, on peut facilement déployer un serveur ActiveMQ.

- **Description** :
  La commande `docker-compose up -d` est utilisée pour démarrer ActiveMQ dans un conteneur Docker, en utilisant un fichier `docker-compose.yml` qui contient la configuration nécessaire.

- **Exemple avec ActiveMQ** :
  Un fichier `docker-compose.yml` pour ActiveMQ peut ressembler à ceci :
  ```yaml
  version: '3'
  services:
    activemq:
      image: rmohr/activemq
      container_name: activemq
      ports:
        - "8161:8161"  # Port pour l'interface web ActiveMQ
        - "61616:61616"  # Port pour le broker de messages


## Activemq_2015


