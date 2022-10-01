# HIVE - TP 1 : INGESTION ANALYSE ET TRAITEMENT DE DONNEES
---
## Dans la ligne de commande hadoop

* Chercher un fichier CSV Open Data de taille moyenne   [ici](https://raw.githubusercontent.com/hortonworks/data-tutorials/master/tutorials/hdp/how-to-process-data-with-apache-hive/assets/driver_data.zip)

- Utiliser la commande wget DANS VOTRE REPERTOIRE LOCAL (/home/hadoop/):
```
wget https://raw.githubusercontent.com/hortonworks/data-tutorials/master/tutorials/hdp/how-to-process-data-with-apache-hive/assets/driver_data.zip
```
- Unzipper le fichier :
```
unzip driver_data.zip
```
- se rendre dans le repertoire 
```
cd driver_data
```
- lister pour voir les fihiers csv existants :
```
ls
```
- Ouvrir le fichier : head votrefichier.csv
```
head votrefichier.csv
```
- éditer le fichier : changer le nom de la colonne wage-plan en wage_plan
    - lancer la commande ``` vi votrefichier.csv```
    - cliquer sur i pour insérer
    - modifier
    - echap :wq pour enregistrer et quitter
- Noter le schéma
- Noter le chemin de votre fichier 
```
pwd
```
- Lancer le shell Hive :  ```hive```

OPTIONNEL SI UN MESSAGE PERMISSION DENIED APPARAIT:
```console
$ sudo su hdfs
$ cd /usr/bin
$ hive
```
## Dans la CLI Hive :
- Afficher les bases existantes : 
```
show databases;
```
* Créer une database mon_prenom_db 
```
create database mon_prenom_db;
```
- Vérifier qu'elle a bien été créée
```
show databases;
```
- Rentrer dans cette database (Utiliser la commande use)
```
use mon_prenom_db;
```
- Optionnel : (non nécessaire)
    - Changer les droits de votre database directement sur hdfs : utiliser la commande ‘chown’ pour réattribuer les droits à votre user
- Construire la requête de création et de remplissage d'un tableau dans la base de donnée à partir su fichier .csv sauvegardé :
    - Définir la table associée au fichier csv dans Hive (Create Table) en respectant le schéma noté précédemment, par ewemple: 
         ```
        create table driver_table(
            driverId int,
            name varchar(20),
            ssn int,
            location varchar(20),
            certified char(1),
            wage_plan varchar(20)
         )
    - enregistrer le fichier dans votre repertoire  
        ```
        row format 
        delimited fields terminated by ',' 
        stored as textfile   
        location '/hive/data/votre_prenom_rep'
        ```
    - supprimer l'entête :
        ```
        TBLPROPERTIES('skip.header.line.count'='1');
        ```
- La commande doit donc ressembler à (Attention à la syntaxe) :
```
create table driver_table(
driverId int,
name varchar(20),
ssn int,
location varchar(20),
certified char(1),
wage_plan varchar(20)
)
row format 
delimited fields terminated by ',' 
stored as textfile   
location '/hive/data/votre_prenom_rep'
TBLPROPERTIES('skip.header.line.count'='1');
```
ou bien :
```
CREATE TABLE driver_table (driverId STRING,name STRING,ssn STRING,location STRING,certified STRING,wageplan STRING) ROW FORMAT DELIMITED FIELDS TERMINATED BY ‘,’ STORED AS TEXTFILE tblproperties(“skip.header.line.count”=“1”);
```
SQL n'est pas sensible à la case
- Insérer les données du fichier de votre chemin local dans votre table , par exemple:
    ```
    LOAD DATA LOCAL INPATH '/home/hadoop/driver_data/drivers.csv' OVERWRITE INTO TABLE driver_table;
    ```
- lister les données insérées: 
```
select * from driver_table;
```
- lister toutes les données des drivers certifiés 
```
select * from driver_table
where certified='Y';
```
- compte des drivers non certifiés:
```
select count(*) from driver_table where certified='N';
```
- A votre tour [(resources)](https://people.sc.fsu.edu/~jburkardt/data/csv/csv.html)
- charger le contenu de deux autres fichiers dans deux autres tableaux dans la même base
- ecrire des requêtes select pour filtrer et/ou ordonner.
