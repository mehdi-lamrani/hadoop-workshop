# HADOOP - TP 1
# LE SYSTÈME DE GESTION DE FICHIER HDFS


**BUT DU TP**
Prendre en main et apprendre à manipuler des fichiers dans l’environnement HDFS. :heavy_check_mark: 

---
- #### Enoncé 1 : MANIPULATION Part I

:information_source: CONSULTER PREALABLEMENT LA REFERENCE DES COMMANDES USUELLES :<br/>
https://www.formation-bigdata.com/les-commandes-hdfs/

1 - Télécharger le fichier suivant dans le Système linux via la commande WGET :<br/>
https://raw.githubusercontent.com/jpatokal/openflights/master/data/airports.dat
```console
# Commande Wget
```

2 - Créer un répertoire sous HDFS.

```console
# Dans le dossier /user/mon_prenom
```

3 - Insérer le fichier dans ce répertoire HDFS via la commande PUT dans votre répertoire user.

```console
# Toujours dans le dossier /user/mon_prenom
```

4 - Vérifier la présence de ce fichier dans votre répertoire hdfs user via la commande LS (hdfs).

```console
# Voir la doc des commandes HDFS
```

---
- #### Enoncé 2 : MANIPULATION Part II

1 - Créer un répertoire hdfs “data” dans votre répertoire “user/mon_prenom”.

2 - Déplacer le fichier airports.dat depuis hdfs dans ce répertoire data.

3 - Modifier les droits hdfs de ce fichier pour le rendre accessible uniquement à vous.

:information_source: Consulter la doc pour les commandes :  mkdir / mv / chmod / etc.


---
- #### Enconcé 3 : EXPLORATION DES METADATA

Explorer le mapping réel des fichiers HDFS dans EXT4.
Localiser les données relatives au fichier chargé dans HDFS lors de la première partie.

* Blocs du fichier
* Mapping du fichier et des blocs
* Mapping des blocs vers les serveurs

Infos des blocs de fichiers :
  
```console  
$ hdfs fsck /user/mon_prenom/data/airports.dat -files -blocks -locations  
```  
--- 

:information_source: Ressource Utile :   
<!--https://hortonworks.com/blog/hdfs-metadata-directories-explained/--!>
https://www.waitingforcode.com/hdfs/hdfs-on-disk-explained/read
