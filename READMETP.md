# MDS-2526-B3-DW-SQL

## Liens utiles

- `https://sql.sh` : cours global pour les requêtes
- `https://github.com/Microleadoff/database-installer-py` : lien de l'installateur des 4 BDD en python

### Ordre des mots-clés dans une requête

```sql
SELECT *
FROM table
WHERE condition
GROUP BY expression
HAVING condition
{ UNION | INTERSECT | EXCEPT }
ORDER BY expression
LIMIT count
OFFSET start
```

### Description des instructions

- `SELECT DISCINCT` : supprime les doublons
- `WHERE` : permet de poser une condition - filtrer les résultats. Les opérateurs possibles utilisables avec la clause WHERE :

| Opérateur  | Description                                                       |
|------------|-------------------------------------------------------------------|
| =          | Égale                                                             |
| <>         | Pas égale                                                         |
| !=         | Pas égale                                                         |
| >          | Supérieur à                                                       |
| <          | Inférieur à                                                       |
| >=         | Supérieur ou égale à                                              |
| <=         | Inférieur ou égale à                                              |
| IN         | Liste de plusieurs valeurs possibles                              |
| BETWEEN    | Valeur comprise dans un intervalle donnée (utile pour les nombres ou dates) |
| LIKE       | Recherche en spécifiant le début, milieu ou fin d'un mot          |
| IS NULL    | Valeur est nulle                                                  |
| IS NOT NULL| Valeur n'est pas nulle                                            |

-  `WHERE ... AND ...` : Permet d'ajouter plusieurs conditions 
-  `WHERE ... OR ...` : Permet d'ajouter plusieurs conditions optionnelles
-  `WHERE ... IN ...` : Permet de filtrer sur une liste d'éléments
-  `WHERE ... BETWEEN ...` : Permet de filtrer entre 2 valeurs
-  `WHERE ... IS NULL ...` : Permet de filtrer sur les champs "NULL"
-  `WHERE ... LIKE ...` : Permet de filtrer sur les chaines de caractères. Voici les utilisations possibles

| Modèle        | Description                                                                 | Exemples correspondants       |
|---------------|-----------------------------------------------------------------------------|--------------------------------|
| `LIKE '%a'`   | Recherche toutes les chaînes qui **se terminent par “a”**                   | `pizza`, `salsa`              |
| `LIKE 'a%'`   | Recherche toutes les chaînes qui **commencent par “a”**                     | `avion`, `arbre`              |
| `LIKE '%a%'`  | Recherche toutes les chaînes qui **contiennent “a”**                        | `chat`, `manger`              |
| `LIKE 'pa%on'`| Recherche les chaînes qui **commencent par “pa” et se terminent par “on”**  | `pantalon`, `pardon`          |
| `LIKE 'a_c'`  | Le caractère `_` représente **un seul caractère** (contrairement à `%`)     | `aac`, `abc`, `azc`           |


## Exemples de requetes pour pratique sur la BDD WORLD

- `SELECT DISTINCT state_code FROM cities;` (1185)
- `SELECT * FROM cities WHERE state_code = "07";` (435)
- `SELECT * FROM cities WHERE state_code = "07" AND country_code = "AD";` (0)
- `SELECT * FROM cities WHERE state_code = "07" OR country_code = "AD";` (444)
- `SELECT * FROM cities WHERE latitude > 42 AND longitude > 1.5;` (53085)
- `SELECT * FROM cities WHERE latitude < 20 AND longitude > 50;` (15814)
- `SELECT * FROM cities WHERE latitude > 42 AND longitude > 1.5 OR latitude < 20 AND longitude > 50;` (68899)
- `SELECT * FROM cities WHERE (latitude > 42 AND longitude > 1.5) OR (latitude < 20 AND longitude > 50);` (68899)
- `SELECT * FROM cities WHERE country_code IN ("AD", "AE");` (49)
- `SELECT * FROM cities WHERE latitude BETWEEN 20 AND 30;` (10235)
- `SELECT * FROM countries WHERE wikiDataId IS NULL;` (47)
- `SELECT * FROM countries WHERE wikiDataId IS NOT NULL;` (203)
- `SELECT * FROM cities WHERE name LIKE 'a%';` (9002)
- `SELECT * FROM cities WHERE name LIKE '%a';` (25624)
- `SELECT * FROM cities WHERE name LIKE '%zw%';` (76)
- `SELECT * FROM cities WHERE name LIKE '%c_t%';` (1973)


INNER JOIN
Seulement les lignes en relation avec les table A et B
LEFT JOIN EXCLUSIVE
Toutes les lignes de la table A meme celle sans relation avec la table B
LEFT JOIN INCLUSIVE
Toutes les lignes de la tables A sans relation avec la table B

SELECT [select list] FROM TableA A LEFT OUTER JOIN TableB B ON A.key=B.key
RIGHT JOIN INCLUSIVE
Toutes les lignes de la tables B meme sans relation avec la table A
RIGHT JOIN EXCLUSIVE
Toutes les lignes de la tables B sans relation avec la table A
FULL OUTER JOIN INCLUSIVE
Toutes les lignes de la table A et B même sans relation
FULL OUTER JOIN EXCLUSIVE
Toutes les lignes de la table A et B qui n'ont pas de relations



## TP 1

En individuel, vous allez devoir continuer, ce fichier readme : 

- Vous créez votre propre fichier, a part
- Vous traitez un maximum de cas de figure sur le site sql.sh
- Vous ne faites ni de jointure, ni de procédures stockées, ni de trigger

Vous allez devoir pour chaque instruction que l'on n'a pas vu : 

1. expliquer l'instruction rapidement
2. en vous servant de la base de données "SAKILA", vous allez créer 1 à 3 cas defigure nécessitants une requete. Par exemple :"Récupérer tous les state_code de la table cities sans aucun doublon". Vous devrez ensuite écrire la requete SQL correspondante, par exemple : `SELECT DISTINCT state_code FROM cities;`. Notez le nombre de résultats obtenus par exemple (1185).


IS NULL sert a trouver toutes les lignes qui on une colonne a null
Retourner toutes les address qui n'ont pas de postal_code
- `SELECT * FROM address WHERE postal_code IS NULL;` (4)

GROUP BY
Permet de faire un total sur une liste de resultat par rapport a une colonne
Retourner les sommes des payement part customer_id
- `select customer_id, (SUM(amount)) from payment GROUP BY customer_id` (600)

HAVING
Permet de faire comme le where mais en utilisant des fonctions (Sum, count...)
Retourner les customer_id avec les amount inférieur a 50
- `SELECT customer_id, amount FROM payment HAVING amount < 50` (17122)

ORDER BY 
Ordonner la liste dans un ordre alphabétique ou inversement
Lister toutes les address dans l'order Descendant
- `SELECT * from address ORDER BY address DESC` (603)

AS
Permet de renommer une colonne temporairement
Lister le nombre de colonne de la table addresse et renommer la colonne 
- `select COUNT(*) AS nb_ligne from address ` (1)


LIMIT 
Permet de recuperer les nb premières ligne de la requete
Recuperer les 10 premières lignes de la table address
- `select * from address LIMIT 10;` (10)

UNION
Permet de mettre en relation les données equivalente de deux table sans doublons
Recupère les infos similaire de la table film_actor et film_category
- `select film_id from film_actor UNION select film_id from film_category;`(1000)

INTERSECT 
Permet de recuperer les infos en commun de deux requetes
Recuperer les film_id en commun de la table film_actor et film_category
- `select film_id from film_actor INTERSECT select film_id from film_category;`(997)

EXCEPT
Permet de recuperer les infos que de la premiere requete
Recuperer les film_id qui sont dans la table film_actor mais paèès dans la table film_category
- `select film_id from film_actor EXCEPT select film_id from film_category;`(0)


INSERT INTO
Insert une ligne dans une table
Inserer dans la table film_text
- `insert into film_text VALUES (1, 'ACADEMY DINOSAUR', 'A Epic Drama of a Feminist And a Mad Scientist who must Battle a Teacher in The Canadian Rockies');`

UPDATE
Modifier une ligne en choisissant la valeur
Modifier le title de la ligne que vous avez insérer
- `UPDATE film_text set title = 'DINOSAUR';`

DELETE
Supprimer une ligne avec ou sans conditions
Supprime la ligne que tu a modifié
- `DELETE FROM film_text WHERE title = 'DINOSAUR';`

MERGE 
Permet de mettre a jour un ligne si elle existe sinon elle la crée

TRUNCATE 
Permet de supprimer toutes les lignes d'une table
- `TRUNCATE TABLE "test"`


## TP 2

Refaire les requêtes dans la BDD World (des requêtes qui font sens !) pour qu'on les intègre dans le cours
Idem que TP1, mais sur les jointures. (BDD SAKILA)





```SQL
SELECT * FROM A INNER JOIN B ON A.key = B.key
Recuperer toutes les address qui font partie de la ville avec le city_id à 10
SELECT C.city, A.address FROM city C INNER JOIN address A ON C.city_id = A.city_id WHERE C.city_id = 10

SELECT * FROM B OUTER JOIN A ON A.key = B.key
SELECT C.city, A.address FROM city C FULL OUTER JOIN  address A ON c.city_id = A.city_id WHERE A.city_id IS NULL OR C.city_id IS NULL
Ne fonctionne pas avec Mysql

SELECT * FROM B LEFT JOIN A ON A.key = B.key
Recupere toutes les city avec l adresse associé
SELECT * FROM city C LEFT JOIN address A ON C.city_id = A.city_id

SELECT * FROM A RIGHT JOIN B ON A.key = B.key
Recupere toutes les addresse avec la ville associé
SELECT * FROM city C RIGHT JOIN address A ON C.city_id = A.city_id


```