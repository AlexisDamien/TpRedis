
# TP Cluster Redis



## Mise en place docker

Je me suis amusé à lire la la docs Redis pour la mise en place de Docker, et j'ai finalement fini par trouver un repo en ligne pour la mise en place d'un cluster Redis, je ne pars donc pas de 0, j'ai remis au goût du jour le Docker-compose.yml pour faire correspondre des adressages.

Puis j'ai build :

```bash
docker-compose build
```
```bash
docker-compose up
```

Mon cluster est enfin prêt.
## Injection et requêtage de données

J'exécute mon docker :

```bash
 docker exec -it no-sql-redis-redis1-1 redis-cli -c -h 173.17.0.2 -p 7000
```

Pour insérer et requêter des données, on utilise différentes commandes selon le type de données:

Pour des strings simples :

```bash
 SET user "Alexis"
```
J'ai SET une clé valeur avec pour clé "user" et valeur "Alexis". Ensuite je récupère la donnée:
```bash
 GET user
```
La commande me retourne donc "Alexis".


Pour des Listes :

```bash
 LPUSH list "apple" "orange" "banana"
```
```bash
 LRANGE list 0 -1
```

Le terminal me renvoi alors :
```bash
1) "banana"
2) "orange"
3) "apple"
```
Il existe d'autres commandes pour récpèrer des données précises de la liste (LINDEX) ou supprimer des données (LPOP) en fonction du besoin.

Pour les hashes :

```bash
 HSET hash "name" "Alexis"
 HSET hash "age" "24"
 HSET hash "city" "Aix"
```
```bash
 HGETALL hash
```
Le terminal me renvoi alors :
```bash
1) "name"
2) "Alexis"
3) "age"
4) "24"
5) "city"
6) "Aix"
```

Je peux aussi récupérer qu'une seule donnée avec un HGET simple ou supprimer avec un HDEL, Je dois juste préciser le hashe en question et le champs voulu.

On peut aussi faire des sortedSets, s'apparentant aux listes mais avec une notion de rangement en plus, pour pouvoir gérer les données que l'on souhaite récupèrer.
Ou bien encore les Sets.
## Evaluations des projets actuels

Évaluation des Projets Actuels :

Identifier des Projets Existants : J'ai examiné mes projets existants pour identifier ceux où l'intégration de Redis pourrait être bénéfique. J'ai pensé l'utiliser pour mon projet incluant un système de gestion des sessions utilisateur

Évaluer les Avantages Potentiels : Redis peut améliorer la réactivité de mes applications en stockant les sessions utilisateur en mémoire, accélérer les requêtes de base de données pour le chat en temps réel en utilisant des structures de données rapides telles que les listes et les ensembles, et optimiser la livraison de contenu en mettant en cache les données statiques.