# UData
Repo pour l'exo udata du cours sur les catalogues de données

## Modop d'utilisation du docker UData

Ouvrir le terminal et se rendre dans le dossier destiné à accueilir les données  
Utiliser la commande indiquée dans le QuickStart :  

```bash
git clone https://github.com/opendatateam/docker-udata  
# clone le GIT de UData
cd docker-udata  
# déplace la console dans le dossier cloné
docker-compose up
#lance le docker-compose.yml
```
Ceci va cloner le repo git, déplacer la console dans le dossier associé puis lancer le docker-compose.yml inclus.  

Les trois images appelées sont :
- Redis
- MongoDB
- UData

Une fois le lancement terminé, il faut initialiser les données dans le container. La commande à utiliser est :

```bash
docker exec -it docker-udata-udata-1 udata init
# cette commande initialise la BD MongoDB et lance la configuration de UData
```
*A noter qu'il y a ici une différence par rapport à la documentation : le nom du container docker créé par le .yml comprend des "-" et non des "_".*

Durant l'exécution de cette commande, il sera proposé de valider plusieurs choses, avec la réponse suggérée (Y/N) :
- SuperUser (Y)
- Références de licence (Y)
- Références spatiales (Y)
- Données de test (N)

Partant de là, si l'on est en contexte de production, la suite se passe dans l'interface graphique. Pour une utilisation en LocalHost, il faut créer un utilisateur en CLI. Cette contrainte est liée à l'absence de serveur mail qui prévient l'envoi des mails de confirmation pour valider les comptes utilisateur.

Les commandes à utiliser sont les suivantes :

``` bash
docker exec -it ['nom ou id du container udata'] bash
# ceci nous fait entrer dans le container en CLI
udata create user
# ceci lance l'utilitaire de création d'utilisateur
```
Il est à présent possible d'utiliser l'interface graphique pour la suite, en LocalHost

Accès à UData via [localhost:7000](localhost:7000)


Si le port 7000 est déjà utilisé par une autre application sur la machine, il faut modifier le fichier docker-compose.yml pour utiliser un port différent ou arrêter les autres services qui l'utilisent.
