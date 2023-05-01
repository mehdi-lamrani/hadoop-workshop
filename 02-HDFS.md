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
wget https://www.gutenberg.org/files/40086/40086-0.txt -o moliere.txt
```
2 - Renomer le fichier 40086-0.txt en moliere.txt
```console
touch molière.txt
mv 40086-0.txt moliere.txt
```

3 - Créer un répertoire sous HDFS.

```console
hdfs dfs -mkdir /user/nom_prénom
```

4 - Insérer le fichier dans ce répertoire HDFS via la commande PUT dans votre répertoire user.

```console
hdfs dfs -put /home/hadoop/moliere.txt /user/nom_prenom
```

5 - Vérifier la présence de ce fichier dans votre répertoire hdfs user via la commande LS (hdfs).

```console
hdfs dfs -ls /user/nom_prenom
```

---
- #### Enoncé 2 : MANIPULATION Part II

1 - Créer un répertoire hdfs “data” dans votre répertoire “user/mon_prenom”.
```console
hdfs dfs -mkdir /user/nom_prenom/data
```

2 - Déplacer le fichier moliere.txt depuis hdfs dans ce répertoire data.
```console
 hdfs dfs -mv /user/nom_prenom/moliere.txt /user/nom_prenom/data
```

3 - Modifier les droits hdfs de ce fichier pour le rendre accessible uniquement à vous.
```console
hdfs dfs -chmod 700 /user/nom_prenom/data
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
hdfs fsck /user/nom_prenom/data/moliere.txt -files -blocks -locations 
```  

```console  
/user/astro/moliere.txt 1429 bytes, replicated: replication=1, 1 block(s):  OK
0. BP-1624421665-172.30.3.247-1682942907253:blk_1073743207_2383 len=1429 Live_repl=1  [DatanodeInfoWithStorage[172.30.3.92:9866,DS-9bf57c96-4389-448c-8bce-a6ac54750aa2,DISK]]


Status: HEALTHY
 Number of data-nodes:	1
 Number of racks:		1
 Total dirs:			0
 Total symlinks:		0

Replicated Blocks:
 Total size:	1429 B
 Total files:	1
 Total blocks (validated):	1 (avg. block size 1429 B)
 Minimally replicated blocks:	1 (100.0 %)
 Over-replicated blocks:	0 (0.0 %)
 Under-replicated blocks:	0 (0.0 %)
 Mis-replicated blocks:		0 (0.0 %)
 Default replication factor:	1
 Average block replication:	1.0
 Missing blocks:		0
 Corrupt blocks:		0
 Missing replicas:		0 (0.0 %)
 Blocks queued for replication:	0

Erasure Coded Block Groups:
 Total size:	0 B
 Total files:	0
 Total block groups (validated):	0
 Minimally erasure-coded block groups:	0
 Over-erasure-coded block groups:	0
 Under-erasure-coded block groups:	0
 Unsatisfactory placement block groups:	0
 Average block group size:	0.0
 Missing block groups:		0
 Corrupt block groups:		0
 Missing internal blocks:	0
 Blocks queued for replication:	0
FSCK ended at Mon May 01 12:50:04 UTC 2023 in 8 milliseconds
```  
-	/user/astro/moliere.txt: This is the HDFS path of the file.
-	1429 bytes: This is the size of the file, in bytes.
-	replicated: replication=1: This indicates the replication factor of the file. In this case, the replication factor is set to 1, which means that there is only one copy of the file stored in the HDFS cluster.
-	1 block(s): OK: This shows that the file is stored in a single HDFS block and that the block status is OK.
-	0.: This is the index of the block information being shown (since there's only one block in this case).
-	BP-1624421665-172.30.3.247-1682942907253: This is the Block Pool ID, a unique identifier for the block pool, which is a collection of blocks that belong to a single namespace (HDFS cluster).
-	blk_1073743207_2383: This is the Block ID, which is a unique identifier for this specific block within the block pool.
-	len=1429: This is the length of the block in bytes, which matches the file size (1429 bytes) as there is only one block.
-	Live_repl=1: This indicates the number of live replicas of this block in the cluster. In this case, it is 1, which corresponds to the replication factor.
-	DatanodeInfoWithStorage[172.30.3.92:9866,DS-9bf57c96-4389-448c-8bce-a6ac54750aa2,DISK]: This provides information about the DataNode where the block is stored. The IP address and port of the DataNode are 172.30.3.92:9866, the storage ID is DS-9bf57c96-4389-448c-8bce-a6ac54750aa2, and the storage type is DISK.


