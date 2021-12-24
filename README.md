# Entraînement au Checkpoint 3 Symfony

Clone ce dépôt en local.

Crée un branche de la forme `NOM_prenom` et bascule dessus pour la suite de l'exercice.

Exécute la commande *Symfony CLI* te permettant d'installer les dépendances avec composer.

> N'exécute pas composer update !

Teste que le serveur se lance bien et affiche une page d'accueil.

Bienvenue dans OscarWildo, ton site de vente de pièces détachées de voiture !

## 1. Initialisation de la base de données

Copie le fichier `.env` vers `.env.local` et modifie les informations d'identification à la base de données `checkpoint3_training`.

Excécute les commandes *Symfony CLI* te permettant de :
- créer la base de données
- exécuter la migration déjà existante
- exécuter la fixture déjà existante

> Webpack ne sera pas utilisé dans ce checkpoint, pas besoin de t'en soucier !

> De plus, Bootstrap est déjà configuré.

## 2. Les catégories

Ton site possède des catégories, caractérisées par un nom.

Si tu as bien exécuté la migration et l'appel des fixtures, tu dois avoir des catégories déjà présentes en base de données.

Crée un controller pemettant d'afficher la vue `/category`, listant les catégories.

Tu auras besoin de créer la vue correspondante.

Le lien vers la liste des catégories est déjà présent dans le header du site, il faudra le modifier pour qu'il redirige vers la page `/category`.

## 3. Initialiser les pièces détachées

Maintenant que les catégories sont en place, tu vas pouvoir créer tes pièces détachées.

Crée l'entité `Part` qui aura les propriétés suivantes :

- serialNumber (VARCHAR(255), NOT NULL, UNIQUE)
- name (VARCHAR(255), NOT NULL)
- price (FLOAT, NOT NULL)

De plus, une pièce détachée sera reliée à une seule catégorie (mais une catégorie pourra posséder plusieurs pièces détachées).

Ajoute la relation `category` reliée à l'entité `Category`.
La relation ne pourra pas être nulle, **sera bidirectionnelle** et sans suppression automatique des orphelins.

Vérifie que `Part` est bien créé et que `Category` possède bien la propriété `$parts`.

Si tout est valide, procéde à la création et l'exécution de la migration.

## 4. CRUD des pièces détachées

Utilise la commande appropriée afin de générer un CRUD pour les pièces détachées `Part`, puis vérifie que la route `/part` s'affiche bien.

Actuellement, la création de pièces détachées `/part/new` ne fonctionne pas : répare cela en modifiant `src/Form/PartType` de la façon appropriée.

> Tu trouveras une piste ici : https://symfony.com/doc/current/reference/forms/types/entity.html#basic-usage

Une fois le formulaire réparé, crée quelques pièces détachées (ne perd pas de temps, tu peux te concentrer sur une seule catégorie et n'en ajouter que deux ou trois).

## 5. Listes les pièces détachées

Dans `CategoryController`, ajoute une route permettant d'accéder à une catégorie par son nom, de la forme: `/category/{Nom-de-la-catégorie}`.

Cette page te permettra d'afficher la liste **des noms** des pièces détachées de la catégorie en question.

Il te faudra créer la vue correspondante.

Modifie la vue de la page `/category` afin d'avoir un lien vers chaque catégorie.

## 6. Détail d'une pièce détachée

Dans `CategoryController`, ajoute une route permettant d'accéder à une pièce détachée par son numéro de série, de la forme : `/category/part/{Numéro-de-série}`.

Cette page te permettra d'afficher toutes les informations d'une pièce détachée : **numéro de série, nom, prix**.

Utilise la méthode de Twig te permattant de formater le prix des pièces détachées, au format français (fr).

> Tu trouveras une piste ici : https://twig.symfony.com/doc/3.x/filters/format_currency.html

Modifie la vue de la page `/category/{Nom-de-la-catégorie}` afin d'avoir un lien vers chaque pièces détachées.

## 7. Ajout au panier

Pas de panique, nous allons juste faire un faux lien d'ajout au panier, qui se contentera d'afficher un message avec les Flash Messages de Symfony : https://symfony.com/doc/current/controller.html#flash-messages

Dans `CategoryController`, ajoute une route permettant de simuler l'ajout au panier d'une pièce détachée, de la forme : `/category/buy/{Numéro-de-série}`.

Cette route affichera un Flash Messages de succès "Vous avez ajouté le la pièce détachée {Nom-de-la-pièce-détachée} à votre panier", puis redigera vers la page `/category`.

> Utilise la méthode `addFlash` puis la méthode `redirectToRoute`

> L'affichage des alertes est déjà configurée dans `base.html.twig`, pas besoin de t'en occuper.

Modifie la vue de la page `/category/part/{Numéro-de-série}` afin d'avoir un lien l'ajout au panier.

## 8. Megas promotions !

Afin d'inciter les gens à commander sur ton site dès le lancement, tu vas créer un service te permettant d'appliquer une réduction à l'ensemble de tes pièces détachées.

Cependant, comme tu n'es pas encore sûr le la promotion à appliquer, tu préfères rendre cela paramétrable (pour l'ajuster si besoin).

Crée le service `src/Service/SpecialOffer` et ajoute la méthode `apply` qui prendra en paramètre un prix.

Ajoute dans ta classe la constante `PROMO` initialisée à `30` (correspondant à une réduction de 30%).

Modifie ta méthode `apply` afin d'appliquer la réduction `PROMO` au prix, puis d'en retourner le résultat.

Appelle ton service dans la page d'affichage des détails d'une pièce détachée.

> Bonus: plutôt que d'appeler ta promotion à partir d'une constante, tu peux l'appeler à partir d'un paramètre de service : https://symfony.com/doc/5.3/service_container.html#service-parameters

## 9. Super bonus : les voitures

Crée une entité `Car` qui aura les propriétés suivantes :

- brand (VARCHAR(255), NOT NULL)
- name (VARCHAR(255), NOT NULL)

De plus, une voiture pourra posséder plusieurs pièces détachées et une pièce détachée pourra appartenir à plusieurs voitures.

Ajoute la relation `parts` reliée à l'entité `Part`.

Utilise la commande appropriée afin de générer un CRUD pour les voitures, puis vérifie que la route `/car` s'affiche bien.

Actuellement, la création de voiture `/car/new` ne fonctionne pas : répare cela en modifiant `CarType` de façon à pouvoir sélectionner plusieurs pièces détachées.