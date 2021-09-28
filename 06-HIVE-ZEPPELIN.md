
###  COMMAND TO DOWNLOAD DATA LOCALLY : 

````
aws s3 sync s3://transtat .
````

Evidemment seul le capitaine de Binôme le fait :)
(Idem pour les commandes hdfs qui suivront au sein TP Zeppelin)

###  ADD JDBC+HIVE INTERPRETER TO ZEPPELIN

###   STEP 0

Goto : 

http://MY.IP.ADD.RESS:8890

###   STEP 1

In the Terminal :
```
sudo /usr/lib/zeppelin/bin/install-interpreter.sh -n jdbc --artifact org.apache.zeppelin:zeppelin-jdbc:0.9.0-preview1
sudo cp /usr/lib/hive/lib/hive-jdbc.jar /usr/lib/zeppelin/
sudo chown -R zeppelin:zeppelin /usr/lib/zeppelin/
sudo chown -R zeppelin:zeppelin /usr/lib/zeppelin/local-repo/
```

###    STEP 2
Restart Zeppelin
```
sudo systemctl restart zeppelin
```
###    STEP 3

Dans Zeppelin > New Notebook > "TEST" > Roue dentée en haut à droite > lien hypertexte 'interpreter' > JDBC > Edit 

```
Configuration :

    Property	        Default	                               Description
    default.driver	 org.apache.hive.jdbc.HiveDriver	    Class path of JDBC driver
    default.url	        jdbc:hive2://localhost:10000	       Url for connection
    
    Dependencies
    Artifact	
    org.apache.hive:hive-jdbc:0.14.0	
    org.apache.hadoop:hadoop-common:2.6.0	
    
```

Puis : SAVE 

###    STEP 4

Ouvrir la note "TEST" et écrire dans une cellule : 

```
%jdbc
show databases;
```

Executez la cellule avec l'icône flèche ">" tout à droite de la cellule

la Database "default" devrais s'afficher avec succès.


###  LOAD ZEPPELIN NOTEBOOK : 

- Télécharger le notebook qui vous sera remis.
- Dans Zeppelin : 
     - Import Notebook > JSON > Chemin du fichier téléchargé
     - Le Nouveau Notebook apparait dans Zeppelin, cliquez dessus
     - You're good to go
