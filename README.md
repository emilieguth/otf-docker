# otf-docker
Encapsulation docker pour OTF

## usage

Suivez le guide pour une installation directe avec tous les paramètres par défaut.

Cette instance est adaptée pour un test rapide sur votre propre machine, mais **fortement déconseillée** en production pour des raisons de sécurité.

1. Installez docker pour votre OS selon https://docs.docker.com/engine/install/
1. clonez ce repository: ```git clone --filter=blob:none https://github.com/emilieguth/otf-docker.git```  (the _filter_ bit is optional, and prevents the downloading of obsolete files while still enabling later updates/fetches.)
1. ```cd otf-docker```
1. mettre à jour les sous-modules ( src = ouvretaferme): ```git submodule init && git submodule update --remote```
1. ajouter l'adresse IP du serveur de développement dans vos alias DNS du client web pour le domaine "dev-ouvretaferme.org". S'il s'agit de votre machine locale sous unix, c'est généralement dans le fichier ```/etc/hosts``` : _127.0.0.1	localhost  dev-ouvretaferme.org_
1. installez et configurez les dépendances de l'application: ```docker compose up```. Ceci va installer les services _mysql-otf, web-otf, php-fpm-otf_ et _redis-otf_.
1. naviguez vers http://localhost pour tester votre app.


## suppression

Depuis le répertoire de votre app (```cd otf-docker```)
 
- Si vous souhaitez garder Docker mais supprimer l'app et ses dépendances: ```docker compose rm```
- Si vous n'utilisez plus Docker pour d'autres usages: supprimer le répertoire de travail ```rm -rf otf-docker```, et désinstallez Docker selon votre OS en inversant les commandes de https://docs.docker.com/engine/install/


