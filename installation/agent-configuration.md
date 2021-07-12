---
description: DQ Agent Configuration Guide
---

# Agent Configuration

## High Level Architecture of Owl Agent setup <a id="high-level-architecture-of-owl-agent-setup"></a>

![High level depiction of DQ Agents using CDH, HDP, and EMR within a single DQ Web App](https://gblobscdn.gitbook.com/assets%2F-L_xJcI5Uc0S1x9JC6xQ%2F-LnU88TjMSmNDQQOzmga%2F-LnUBuNZqRfEFAzVhB0o%2FAgents%20%281%29.jpg?alt=media&token=3452698c-aeae-43e4-b730-b2b19e4dd1c5)

The above image provides a high level depiction of what transpires when using agents within DQ. A job execution is driven by DQ Jobs that are written to an `agent_q` table inside the DQ Metadata Postgres Storage via the Web app or REST API endpoint.  The agents queires the `agent_q` table every 5 seconds to execute the DQ Jobs they are only responsibly for \(EMR agent `Owl-Agent3` in the picture only executes DQ Jobs scheduled to run on EMR. 

When an agent picks up a job to execute, the agent will launch the job either locally on the agent node itself or on a cluster as a spark job \(if the agent is setup as an edge node of a cluster\). Depending on where the job launches, the results of the DQ Job will write back to the DQ Metadata Storage \(`owl-postgres` server\) and displayed on the DQ Web UI.

## Agent Configuration Parameters

| Parameter | Description |
| :--- | :--- |
| **Is Local** | For Hadoop only |
| **Is Livy** | Deprecated. Not used. |
| **Base Path** | This is the location that was provided to the setup command for initial install, i.e. `OWL_BASE`. For example, if setup command was `export OWL_BASE=/home/centos` then the Base Path in the Agent configuration should be set to `/home/centos/` |
| **Owl Core JAR** | The file path to DQ Core jar file located in `$OWL_BASE/owl/bin/` |
| **Deploy Deployment Mode** | The Spark deployment mode that takes one of `Client` or `Cluster` |
| **Default Master** | The Spark Master URL copied from the Spark cluster verification screen \(`spark://...`\)  |
| **Default Queue**  | The default resource queue for YARN |
| **Dynamic Spark Allocation** | Deprecated. Not used. |
| **Spark Conf Key** | Deprecated. Not used. |
| **Spark Conf Value** | Deprecated. Not used. |
| **Number of executor\(s\)** | The default number of executors allocated per DQ Job when using this Agent to run DQ Scan |
| **Executer Memory \(GB\)** | The default RAM per executors allocated per DQ Job when using this Agent to run DQ Scan |
| **Number of Core\(s\)** | The default number of cores per executors allocated per DQ Job when using this Agent to run DQ Scan |
| **Driver Memory \(GB\)** | The default driver RAM allocated per DQ Job when using this Agent to run DQ Scan |
| **Free Form \(Appended\)**  | Other `spark-submit` parameters to append to each DQ Job when using this Agent to run DQ Scan |

![](../.gitbook/assets/screenshot-2021-06-14-at-4.25.09-pm.png)



