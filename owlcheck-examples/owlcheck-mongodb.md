# OwlCheck MongoDB

## Browse MongoDB like any other relational database

Using Owl's file tree explorer browse Mongo "collections" like "tables".  Then use the wizard to create standard DQ scans. 

![](../.gitbook/assets/screen-shot-2020-08-01-at-10.11.41-am.png)

### CMD Line

Copy paste-able cmdline example for simple spark submit job.

```bash
-lib "/opt/owl/drivers/mongodb/" 
-h localhost:5432/postgres 
-master local[*] 
-ds tpch.lineitem_7 
-br 10 -deploymode client 
-q "select * from tpch.lineitem where l_shipdate between '${rd} 00:00:00.000+0000' 
and '${rdEnd} 00:00:00.000+0000' " 
-bhlb 10 -rd "1998-12-01" 
-driver "mongodb.jdbc.MongoDriver" 
-loglevel INFO -cxn MongoDB -rdEnd "1998-12-02"
```

## Drivers and Config

In order to make this possible OwlDQ requires 2 drivers, MongoDB driver and UnityJDBC Driver.  Out of the box OwlDQ comes preconfigured with these drivers.  You simply open the MongoDB connection template and paste in your JDBC URL.

```text
driverClass: mongodb.jdbc.MongoDriver

path: /opt/owl/drivers/mongodb/
    +-- mongoJdbc.jar
    +-- unityJDBC.jar
```

### Simply paste in JDBC Info

![](../.gitbook/assets/screen-shot-2020-08-01-at-10.09.20-am.png)

### Discover Correlations, Relationships, DQ issues and Much More... 

![](../.gitbook/assets/screen-shot-2020-08-01-at-10.10.45-am.png)

The following table presents the various SQL statements related to table-level actions and the corresponding MongoDB statements.[https://docs.mongodb.com/manual/reference/sql-comparison/](https://docs.mongodb.com/manual/reference/sql-comparison/)

![](../.gitbook/assets/screen-shot-2020-08-02-at-2.17.34-pm.png)

### Limiting Collections in the JDBC URL

```text
jdbc:mongodb://<dbuser>:<password>@datalake0-dza1q.a.query.mongodb.net/<mydatabase>?ssl=true&authSource=admin&rebuildschema=true&tables=orders
```

There are 3 collections in this mongodb atlas lake.  By adding &tables=orders in the URL params you can see only order collections show up in the explorer.

![](../.gitbook/assets/screen-shot-2021-07-22-at-1.54.04-pm.png)

### 3 Collections in MongoDB Atlas

The total number of collections in mongodb atlas lake.

![](../.gitbook/assets/screen-shot-2021-07-22-at-1.57.29-pm.png)

