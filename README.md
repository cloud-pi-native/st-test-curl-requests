# Cronjob d'exexution d'une requete HTTP depuis un Job

Ce chart crée un cronjob qui exécute un job réalisant une requête http vers une cible avec ou sans certificat permettant de tester la connexion vers une destination depuis une namespace.


## Installation / configuration

Ajouter ce repo de code depuis la console.

Dans Vault ajouter un secret nommé test-ines et contenant les secrets : TOKEN, cert.pem et key.pem avec les valeurs associées

Mettre à jour le fichier values-custom.yaml à la racine du projet avec les informations du secret et notamment le nom du projet.

Depuis ArgoCD, configurer le projet en ajoutant en paramètre le fichier values-custom.yaml puis une fois que le projet est déployé lancer un job à partir du cronjob et consulter les logs sur le pod créé.