---
description: DQ Agent Configuration Guide
---

# Agent Configuration

## High Level Architecture of Owl Agent setup <a id="high-level-architecture-of-owl-agent-setup"></a>

![Fig 1: High level depiction of DQ Agents using CDH, HDP, and EMR within a single DQ Web App](https://gblobscdn.gitbook.com/assets%2F-L_xJcI5Uc0S1x9JC6xQ%2F-LnU88TjMSmNDQQOzmga%2F-LnUBuNZqRfEFAzVhB0o%2FAgents%20%281%29.jpg?alt=media&token=3452698c-aeae-43e4-b730-b2b19e4dd1c5)

Fig 1 shows provides a high level depiction of how agents work within DQ. A job execution is driven by DQ Jobs that are written to an `agent_q` table inside the DQ Metadata Postgres Storage \(`Owl-Postres` database in Fig 1\) via the Web UI or REST API endpoint.  Each agent available and running queries the `Owl-Postgres` table every 5 seconds to execute the DQ Jobs the agent is responsible for. For example, the EMR agent `Owl-Agent3` in Fig 1 only executes DQ Jobs scheduled to run on EMR. 

When an agent picks up a DQ Job to execute, the agent will launch the job either locally on the agent node itself or on a cluster as a spark job \(if the agent is setup as an edge node of a cluster\). Depending on where the job launches, the results of the DQ Job will write back to the DQ Metadata Storage \(`Owl-Postgres` database\). The results are then displayed on the DQ Web UI, exposed as REST API, and available for direct SQL query against `Owl-Postgres` database.

## Agent Configuration Parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Is Local</b>
      </td>
      <td style="text-align:left">For Hadoop only</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Is Livy</b>
      </td>
      <td style="text-align:left">Deprecated. Not used.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Base Path</b>
      </td>
      <td style="text-align:left">
        <p>The installation folder path for DQ. All other paths in DQ Agent are relative
          to this installation path</p>
        <p></p>
        <p>This is the location that was set as <code>OWL_BASE</code> in Full Standalone
          Setup and other installation setups followed by <code>owl/</code> folder.
          <br
          />
          <br />For example, if setup command was <code>export OWL_BASE=/home/centos</code> then
          the <b>Base Path</b> in the Agent configuration should be set to <code>/home/centos/owl/</code>.</p>
        <p>Default: <code>/opt/owl/</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Owl Core JAR</b>
      </td>
      <td style="text-align:left">The file path to DQ Core jar file.
        <br />Default <code>&lt;Base Path&gt;/owl/bin/</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Owl Core Logs</b>
      </td>
      <td style="text-align:left">The folder path where DQ Core logs are stored. Logs from DQ Jobs are stored
        in this folder.
        <br />Default: <code>&lt;Base Path&gt;/owl/log</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Owl Web Logs</b>
      </td>
      <td style="text-align:left">The folder path where DQ Web logs are stored. Logs from DQ Web App is
        stored in this folder.
        <br />Default: <code>&lt;Base Path&gt;/owl/log</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Owl Script</b>
      </td>
      <td style="text-align:left">The file path to DQ execution script <code>owlcheck.sh</code>. This script
        is used to run DQ Job via command line without using agent. Using<code>owlcheck.sh</code>for
        running DQ Jobs is superseded by DQ Agent execution model.
        <br />Default: <code>&lt;Base Path&gt;/owl/bin/owlcheck</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Deploy Deployment Mode</b>
      </td>
      <td style="text-align:left">The Spark deployment mode that takes one of <code>Client</code> or <code>Cluster</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Default Master</b>
      </td>
      <td style="text-align:left">The Spark Master URL copied from the Spark cluster verification screen
        (<code>spark://...</code>)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Default Queue</b>
        <br />
      </td>
      <td style="text-align:left">The default resource queue for YARN</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Dynamic Spark Allocation</b>
      </td>
      <td style="text-align:left">Deprecated. Not used.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Spark Conf Key</b>
      </td>
      <td style="text-align:left">Deprecated. Not used.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Spark Conf Value</b>
      </td>
      <td style="text-align:left">Deprecated. Not used.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Number of executor(s)</b>
      </td>
      <td style="text-align:left">The default number of executors allocated per DQ Job when using this Agent
        to run DQ Scan</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Executer Memory (GB)</b>
      </td>
      <td style="text-align:left">The default RAM per executors allocated per DQ Job when using this Agent
        to run DQ Scan</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Number of Core(s)</b>
      </td>
      <td style="text-align:left">The default number of cores per executors allocated per DQ Job when using
        this Agent to run DQ Scan</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Driver Memory (GB)</b>
      </td>
      <td style="text-align:left">The default driver RAM allocated per DQ Job when using this Agent to run
        DQ Scan</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Free Form (Appended)<br /></b>
      </td>
      <td style="text-align:left">Other <code>spark-submit</code> parameters to append to each DQ Job when
        using this Agent to run DQ Scan</td>
    </tr>
  </tbody>
</table>

![Fig 2: Edit DQ Agent mode in D](../.gitbook/assets/screenshot-2021-06-14-at-4.25.09-pm.png)

## How to Install a New DQ Agent

### Setting up a DQ Agent using `setup.sh` as part of DQ package

Use `setup.sh` script located in `/opt/owl/` \(or other [**Base Path**](https://docs.owl-analytics.com/installation/agent-configuration#agent-configuration-parameters) that your installation used\). See example code block for installing a DQ Agent with Postgres server running `localhost` on port `5432` with database `postgres` and Postgres username/password combo `postgres`/`password`

```text
# PATH TO DIR THAT CONTAINS THE INSTALL DIR
export BASE_PATH=/opt

# PATH TO AGENT INSTALL DIR
export INSTALL_PATH=/opt/owl

# DQ Metadata Postgres Storage settings 
export METASTORE_HOST=localhost
export METASTORE_PORT=5432
export METASTORE_DB=postgres
export METASTORE_USER=postgres
export METASTORE_PASSWORD=password 

cd $INSTALL_PATH

# Install DQ Agent only
./setup.sh \
    -owlbase=$BASE_PATH \
    -options=owlagent \
    -pguser=$METASTORE_USER \
    -pgpassword=$METASTORE_PASSWORD \
    -pgserver=${METASTORE_HOST}:${METASTORE_PORT}/${METASTORE_DB}
```

The setup script will automatically generate the `/opt/owl/config/owl.properties` file and encrypt the provided password.

### Setting up a DQ Agent manually

* Passwords to DQ Metadata Postgres Storage should be encrypted before being stored in `/opt/owl/config/owl.properties`file. 

```text
# PATH TO AGENT INSTALL DIR
export INSTALL_PATH=/opt/owl

cd $INSTALL_PATH

# Encrypt DQ Metadata Postgres Storage password
./owlmanage.sh encrypt=password
```

`owlmanage.sh` will generate an encrypted string for the plain text password input. The encrypted string can be used in the `/opt/owl/config/owl.properties`configuration file to avoid exposing the DQ Metadata Postgres Storage password.

* To complete Owl Agent configuration, edit the `/opt/owl/config/owl.properties`configuration file with basic agent values:

```text
vi $INSTALL_PATH/config/owl.properties
```

* and add the following properties

```text
spring.datasource.url=jdbc:postgresql://{DB_HOST}:{DB_PORT}/{METASTORE_DB}
spring.datasource.username={METASTORE_USER}
spring.datasource.password={METASTORE_PASSWORD}
spring.datasource.driver-class-name=com.owl.org.postgresql.Driver
 
spring.agent.datasource.url=jdbc:postgresql://{DB_HOST}:{DB_PORT}/{METASTORE_DB}
spring.agent.datasource.username={METASTORE_USER}
spring.agent.datasource.password={METASTORE_PASSWORD}
spring.agent.datasource.driver-class-name=org.postgresql.Driver
```

* Restart the web app

## How To Configure Agent via UI

* Login to DQ Web and navigate to Admin Console.

![Fig 1: Home Page](../.gitbook/assets/dq-admin-console-1.png)

* From the Admin Console, click on the Remote Agent tile.

![Fig 2: Admin Console](../.gitbook/assets/dq-admin-console-2.png.png)

* Identify the row with the agent to edit . 

![Fig 3: Agent Management Table](../.gitbook/assets/dq-admin-console-3.png)

* Click on the pencil icon to edit.

![Fig 4: DQ Agent with default values](../.gitbook/assets/dq-admin-console-4.png)

## How To Link DB Connection to Agent via UI

When you add a new[ Database Connection](https://docs.owl-analytics.com/connecting-to-dbs-in-owl-web/owl-db-connection#how-to-add-db-connection-via-ui), the DQ Agent must be given the permission to run DQ Job via the specified agent.

From Fig 3, select the chain link icon next to the DQ Agent to establish link to DB Connection. A modal to add give that agent permission to run DQ Jobs by DB Connection name will show \(Fig 5\). The left-side panel is the list DB Connection names that has not been linked to the DQ Agent. The right-side panel is the list of DB Connection names that has the permission to run DQ Job.

Double click the DQ Connection name to move from left to right. In Fig 5, DB Connection named "metastore" is being added to DQ Agent. Click the "Update" button to save the new list of DB Connections.

![Fig 5: Adding DB Connection named &quot;metastore&quot; to the DQ Agent](../.gitbook/assets/screenshot-2021-06-14-at-5.04.25-pm.png)

![Fig 6: How to add all connections to the selected DQ Agent](../.gitbook/assets/dq-agent-config-hint-1.png)

## Setting up an HA Group <a id="setting-up-an-ha-group"></a>

If you have multiple DQ Agents, then you can establish them as an HA Group. When doing so, make sure both DQ Agents have the same connections established to them. 

* Click on the "AGENT GROUPS \(H/A\)" Tab name your HA Group and add the Agents you'd like to participate as Group. NOTE: HA GROUPS will execute jobs in a round robin fashion.

![](https://gblobscdn.gitbook.com/assets%2F-L_xJcI5Uc0S1x9JC6xQ%2F-LnUsmCFG-tKOAMRkqvx%2F-LnV8ur7dy_09xGAIsA8%2FScreen%20Shot%202019-08-29%20at%209.18.40%20PM.png?alt=media&token=92b1ecfb-b8a0-4f9c-ad6d-7d22601cafd5)

* When the Agents have been registered, associated with DB connections, users can now execute a job via the explorer page.

![Fig 7: Executing an Ad Hoc job via DQ Web Explorer](https://gblobscdn.gitbook.com/assets%2F-L_xJcI5Uc0S1x9JC6xQ%2F-LnUsmCFG-tKOAMRkqvx%2F-LnVCneYAUxjqA84p5Fq%2FScreen%20Shot%202019-08-29%20at%209.45.42%20PM.png?alt=media&token=06e9d717-d75d-430c-8a2c-a68720189a78)











