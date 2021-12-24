# Entraînement au Checkpoint 3 Symfony

Clone ce dépôt en local.

Crée un branche de la forme `NOM_prenom` et bascule dessus pour la suite de l'exercice.

Excécute la commande `symfony` te permettant d'installer les dépendances avec composer

> N'exécute pas composer update !

Teste que le serveur se lance bien et affiche une page d'accueil.

Bienvenue dans OscarWildo, ton site de vente de pièces détachées de voiture !

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

Le lien vers la liste des catégorie est déjà présent dans le header du site, il faudra le modifier pour qu'il redirige vers la page `/categories`.

## 3. Initialiser les pièces détachées

Maintenant que les catégories sont en place, tu vas pouvoir créer tes pièces détachées.

Crée l'entité `SparePart` qui aura les propriétés suivantes (non nulles) :

- serialNumber (string)
- name (string)
- price (float)

De plus, une pièce détachée sera reliée à une seule catégorie (mais une catégorie pourra posséder plusieurs pièce détachées).

Ajoute la relation `category` correspondante à ton entité `SparePart`.
La relation ne pourra pas être nulle, **sera bidirectionnelle** et sans suppression automatique des orphelins.

Vérifier que `SparePart` soit bien créé et que `Category` possède bien la propriété `$spareParts`.

Si tout est valide, procéder à la création et l'exécution de la migration.

## 4. CRUD des pièces détachées

Utiliser la commande appropriée affiche de générer un CRUD pour les pièces détachées `SparePart` et vérifier que la route `/spare/part/` s'affiche bien.

Actuellement, la création de pièces détachées `/spare/part/new` ne fonctionne pas. Réparer cela en modifiant `SparePartType` de la façon appropriée.

> Tu trouveras une piste ici : https://symfony.com/doc/current/reference/forms/types/entity.html#basic-usage

Une fois le formulaire réparé, crée quelques pièces détachées (ne perd pas de temps, tu peux te concentrer sur une seule catégorie et en ajouter deux ou trois).

## 5. Listes les pièces détachées

Dans `CategoryController`, ajoute une route permettant d'accéder à une catégorie par son nom, de la forme: `/categories/Nom-de-la-catégorie`.

Cette page te permettra d'afficher tous les produits de la catégorie en question.

Il te faudra créer la vue correspondante.

Modifie la vue de la page `/categories` afin d'avoir un lien vers chaque catégorie.

## 6. Formatage du prix

Utilise la méthode Twig appropriée afin de formater le prix des pièces détachées au format français (fr).

> Tu trouveras une piste ici : https://twig.symfony.com/doc/3.x/filters/format_currency.html

## 7. Bouton d'ajout au panier

Pas de panique, nous allons juste faire un faux bouton d'ajout au panier, qui se contentera d'afficher un message avec les Flash Messages de Symfony : https://symfony.com/doc/current/controller.html#flash-messages

Dans la vue de la liste des pièces détachées par catégorie, ajoute un lien pour chaque produit vers la route `/categories/add/Numéro-de-série`, ou le numéro de série et remplacé par la valeur de `serialNumber`.

Crée la route correspondante dans `CategoryController` et afficher un Flash Messages de succès "Vous avez ajouté le produit {Numéro-de-série} à votre panier" puis redige vers la page `/categories`

> Utilise la méthode `addFlash` puis la méthode `redirectToRoute`