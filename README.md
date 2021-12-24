# Entraînement au Checkpoint 3 Symfony

Clone ce dépôt en local.

Crée un branche de la forme `NOM_prenom` et bascule dessus pour la suite de l'exercice.

Excécute la commande `symfony` te permettant d'installer les dépendances avec composer

> N'exécute pas composer update !

Teste que le serveur se lance bien et affiche une page d'accueil.

Bienvenue dans OscarWildo, ton site de vente de pièces détachées de voiture !

Les pièces détachées seront classées par catégories et par véhicules.

Mais pour le moment ne t'en soucis pas, tu vas être guidé par ce checkpoint !

## 1. Initialisation de la base de données

Copie le fichier `.env` vers `.env.local` et modifie les informations d'identification à la base de données `checkpoint3_training`.

Excécute les commandes `symfony` te permettant de :
- créer la base de données
- exécuter la migration déjà existante
- exécuter la fixture déjà existante

> Webpack ne sera pas utilisé dans ce checkpoint, pas besoin de t'en soucier !
> De plus, Bootstrap est déjà configuré.

## 2. Les catégories

Ton site possède des catégories, caractérisées par un nom.

Si tu as bien exécuté la migration et l'appel des fixtures, tu dois avoir des catégories déjà présentes en base de données.

Crée un controller te pemettant d'afficher la vue `/categories`, affichant la liste des catégories.

Tu auras besoin de créer la vue correspondante.

Le lien vers la liste des catégorie est déjà présente dans le header du site, il faudra le modifier pour qu'il redirige vers la page `/categories`.