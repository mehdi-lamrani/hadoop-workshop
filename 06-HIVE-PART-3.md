###  ADD JDBC+HIVE INTERPRETER TO ZEPPELIN

###   STEP 1
```
sudo /usr/lib/zeppelin/bin/install-interpreter.sh -n jdbc --artifact org.apache.zeppelin:zeppelin-jdbc:0.9.0-preview1
```

###    STEP 2
```


    Configuration
    Property	        Default	                                         Description
    default.driver	org.apache.hive.jdbc.HiveDriver	Class path of JDBC driver
    default.url	jdbc:hive2://localhost:10000	      Url for connection
    
    Dependencies
    Artifact	
    org.apache.hive:hive-jdbc:0.14.0	
    org.apache.hadoop:hadoop-common:2.6.0	
    
```
###    STEP 3
```
cp /usr/lib/hive/lib/hive-jdbc.jar /usr/lib/zeppelin/
```
###    STEP 4

Restart Zeppelin
```
sudo systemctl restart zeppelin
```
