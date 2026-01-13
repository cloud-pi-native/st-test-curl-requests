# Cronjob d'exexution d'une requete HTTP depuis un Job

Ce chart crée un cronjob qui exécute un job réalisant une requête http vers une cible avec ou sans certificat permettant de tester la connexion vers une destination depuis une namespace.


## Installation / configuration

Ajouter ce repo de code depuis la console.

Dans Vault ajouter un secret nommé test-ines et contenant les secrets : TOKEN, full_cert.pem, JWT_USER, JWT_PASSWORD  avec les valeurs associées

Mettre à jour le fichier values-custom.yaml à la racine du projet avec les informations du secret et notamment le nom du projet.

Depuis ArgoCD, configurer le projet en ajoutant en paramètre le fichier values-custom.yaml puis une fois que le projet est déployé lancer un job à partir du cronjob et consulter les logs sur le pod créé.

Modifier le fichier values-custom.yaml : 
```yaml
secret:
  mount: mi-serviceteam # MEttre a jour avec le nom du projet
  path: test-st
iddossier: api-gdc/dossiers/
url_to_test: URL_INES
useProxy: true
proxyUrl: PROXY_DC
jwtTokenUrl: URL_JWT
configMap:
  name: st-test-nginx-config-advanced
```

Avec :
 - URL_INES : URL d'accès à INES (propre en passant par la CDS INES)
 - PROXY_DC : proxy du datacenter portant la notion de région
 - URL_JWT : URL d'appel pour récupérer le token JWT

Depuis l'interface ArgoCD, exécuter un job à partir du cronjob et vérifier les logs pour voir le résultat.