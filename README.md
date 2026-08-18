# Cronjob d'exexution d'une requete HTTP depuis un Job

Ce chart crée un cronjob qui exécute un job réalisant une requête http vers une cible avec ou sans certificat permettant de tester la connexion vers une destination depuis une namespace.


## Installation / configuration

Ajouter ce repo de code depuis la console.

Dans Vault ajouter un secret nommé orion_creds et contenant les clés ORION_USERNAME et ORION_PASSWORD correspondant aux credentials Orion.


Modifier le fichier values.yaml : 
```yaml
image:
  curl: badouralix/curl-jq-yq:ubuntu
url_to_test: https://www.google.fr # Renseigner ici l'URL sur Internet à tester
curlOption: "-k"
command: sh /scripts/kubernetescurljob.sh
secret:
  proxy:
    mount: NOM_PROJET # A Adapter en fonction du nom du projet 
    path: orion-creds
useProxy: true
proxy_host: proxymi # Renseigner ici le hostname du proxy en fonction de la région
proxy_port: 8888 # Renseigner ici le port du proxy
configMap:
  name: st-test-nginx-config
url_to_test_mi: http://demo-cpin-ines.d650.dev.forge.minint.fr # Mettre ici l'URL sur le réseau interne à tester
```

Depuis l'interface ArgoCD, exécuter un job à partir du cronjob et vérifier les logs pour voir le résultat.

le job fait une requete curl vers les 2 URL avec et sans l'utilisation du proxy et affiche le résultat.