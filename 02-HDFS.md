# HADOOP - TP 1
# LE SYSTÈME DE GESTION DE FICHIER HDFS


**BUT DU TP**
Prendre en main et apprendre à manipuler des fichiers dans l’environnement HDFS. :heavy_check_mark: 

---
- #### Enoncé 1 : MANIPULATION Part I

:information_source: CONSULTER PREALABLEMENT LA REFERENCE DES COMMANDES USUELLES :<br/>
https://www.formation-bigdata.com/les-commandes-hdfs/

1 - Télécharger le fichier suivant dans le Système linux via la commande WGET :<br/>
https://www.gutenberg.org/files/40086/40086-0.txt
```console
wget https://www.gutenberg.org/files/40086/40086-0.txt
```
2 - Renomer le fichier 40086-0.txt en moliere.txt
```console
touch molière.txt
mv 40086-0.txt molière.txt
```

3 - Créer un répertoire sous HDFS.

```console
hdfs dfs -mkdir /user/nom_prénom
```

4 - Insérer le fichier dans ce répertoire HDFS via la commande PUT dans votre répertoire user.

```console
hdfs dfs -put /home/hadoop/molière.txt /user/nom_prénom
```

5 - Vérifier la présence de ce fichier dans votre répertoire hdfs user via la commande LS (hdfs).

```console
hdfs dfs -ls /user/nom_prénom
```

---
- #### Enoncé 2 : MANIPULATION Part II

1 - Créer un répertoire hdfs “data” dans votre répertoire “user/mon_prenom”.
```console
hdfs dfs -mkdir /user/nom_prénom/data
```

2 - Déplacer le fichier 40086-0.txt depuis hdfs dans ce répertoire data.
```console
 hdfs fs -mv /user/nom_prénom/molière.txt /user/nom_prénom/data
```

3 - Modifier les droits hdfs de ce fichier pour le rendre accessible uniquement à vous.
```console
hdfs dfs -chmod 600 /user/nom_prénom/data
 ```

:information_source: Consulter la doc pour les commandes :  mkdir / mv / chmod / etc.)

---
- #### Enconcé 3 : EXPLORATION DES METADATA
Explorer le mapping réel des fichiers HDFS dans EXT4.
Localiser les données relatives au fichier chargé dans HDFS lors de la première partie.
* Blocs du fichier
* Mapping du fichier et des blocs
* Mapping des blocs vers les serveurs

Infos des blocs de fichiers :
```console  
hdfs fsck /user/nom_prénom/data/molière.txt -files -blocks -locations 
```  
