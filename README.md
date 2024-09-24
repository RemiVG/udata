# UData
udata est un logiciel libre de catalogage et de publication de données ouvertes qui propulse la plateforme data.gouv.fr (17 millions de visite en 2021).
Son code est ouvert depuis sa création en 2013 et il est réutilisé et personnalisé par différents pays, administrations, collectivités, etc. 
Il est activement maintenu par Etalab. 
### Repo pour l'exo udata du cours sur les catalogues de données  

### liens de documentation  
tuto de deployement :https://hackmd.io/@ameklou/r1L7h6b1S  
doc : https://udata.readthedocs.io/en/stable/  
git : https://github.com/opendatateam/udata  

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

## publier des données  
https://guides.data.gouv.fr/guide-data.gouv.fr/jeux-de-donnees/publier-un-jeu-de-donnees  

1. création d'une organisation
2. ajout d'un dataset
- administration \-> "+" (en haut à droite) \-> add a dataset  
    1. Publish as Choose who is publishing  
		Choose under which identity you want to publish  
    2. New dataset Describe your dataset  
		 Title  
		Acronym  
		Description 
		License  (choix multiple)
		Update frequency  
		Tags  
		Temporal coverage (debut/fin)  
		Spatial coverage  
		Spatial granularity  (choix multiple)
		Private  (yes/no)  
    3. Resources Add your first resources  
		Drag a file here  
				Title  
				Type
				Description  
				URL  => créé automatiquement mais bug, valider quand même
				Size  
				Format  
				Mime Type  
				Checksum  
				sha1  (n° d'identifiant créé automatiquement)

    4. Share Communicate about your publication 
			Your dataset has been created
			choisir entre see in the administration   ou see on the site
	
