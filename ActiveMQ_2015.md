## ActiveMQ_2015

### Scan du réseau
Dans le cas d'ActiveMQ_2015 l'adresse ip est 172.18.0.1
![Capture d'écran 2024-10-01 121316](https://github.com/user-attachments/assets/8d40d00b-0967-452f-8e6e-0fdf3dcc81e7)

Grace à notre scan on en déduit que le port qui nous intéresse est le 8161.
Pour se rediriger sur le site le lien est donc `http://localhost:8161`

### Version d'ActiveMQ 
Pour savoir la version il faut se connecter:  
- Login: admin
- Mot de passe: admin  
![Capture d'écran 2024-10-01 115916](https://github.com/user-attachments/assets/1cc0ec1d-9c63-4438-8c34-dd006a92ac7b)

### CVE Score
CVE-2015-1830  
![Capture d'écran 2024-10-01 121800](https://github.com/user-attachments/assets/0566d3f7-64a6-470f-9ca1-1b5049191008)  
Cette vulnérabilité est lié à une mauvaise gestion des autorisations dans la console web d'administration d'Apache ActiveMQ. En particulier, les utilisateurs non autorisés pourraient potentiellement accéder à des informations sensibles ou exécuter certaines actions de gestion sans authentification adéquate.

### Stratégie de compromission
[Stratégie de compromission 2015](stratégie_compromission_2015.rb)   

### Exploitation/Explication  
### 1. `Objectif du module`  
Le module permet de téléverser un fichier JSP malaveillant en coutournant les restrictions de chemin grâce à ..//.  Il permet aussi d'obtenir un accès shell a distance.

### 2. `Fonctionnement`
Tout d'abord on utilise les identifiants par défaut (admin:admin)   
Ensuite on vérifié si la cible est vulnérable.   
Puis ensuite il téléverse le payload JSP et l'éxecute.   
Cela permet donc d'avoir l'accès au shell.  

