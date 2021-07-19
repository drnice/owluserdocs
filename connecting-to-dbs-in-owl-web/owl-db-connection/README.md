# Owl DB Connection

## How to Add DB Connection via UI

We will add a connection named `metastore` that connects to local Postgres server \(`localhost:5432/postgres`\)

* Login to DQ Web and navigate to Admin Console.

![Fig 1: Home Page](../../.gitbook/assets/dq-admin-console-1.png)

* From the Admin Console, click on the Connections tile.

![Fig 2: Admin Console](../../.gitbook/assets/dq-admin-console-2.png.png)

* Click on Add button in Postgres box to add a Postgres connection

![Fig 3: List of DB Connections](../../.gitbook/assets/dq-connection-1.png)

Default Postgres JDBC template connection is shown. This modal is populated with basic values what Postgres connection setting should look like.

![Fig 4: Template Postgres connection creation modal](../../.gitbook/assets/dq-connection-2.png)

Replace the Connection URL to point to the Postgres server you want to run DQ Jobs against. In this example, `jdbc:postgresql://localhost:5432/postgres`

Also change Driver Location to the JDBC Driver for Postgres in your installation. Click on the folder icon and click on Postgres driver path. These Driver Directories are default JDBC Drivers provided by DQ installation \(usually in `$OWL_BASE/owl/drivers/*`\)

![Fig 5: Add new driver or select existing from Driver Directories](../../.gitbook/assets/dq-connection-3.png)

Fig 6 is what the new connection setting should look like. Make sure to provide the correct Postgres Username and Password \(if using Username/Password for authentication\). Press Save to continue. _**This action will attempt to establish a connection.**_

![Fig 6: Connection settings to connect to database named &quot;postgres&quot; in Postgres server &quot;localhost&quot; exposed via port 5432](../../.gitbook/assets/dq-connection-4.png)



{% hint style="info" %}
Make sure to [Link DB Connection](https://docs.owl-analytics.com/installation/agent-configuration#how-to-link-db-connection-to-agent-via-ui) to a DQ Agent, if required
{% endhint %}







