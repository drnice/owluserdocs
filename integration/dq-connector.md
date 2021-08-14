# Collibra Native DQ Connector

## Benefits

The Native DQ Connector brings intelligence from **Collibra Data Quality** into **Collibra Data Intelligence Cloud**. Once this integration is established, you will be able to bring in your Data Quality user-defined rules, metrics, and dimensions into **Collibra Data Catalog**.

_Please note: Only data sources ingested by both Collibra Data Catalog and Collibra Data Quality will be able to synchronize Data Quality assets_

## Step 0: Prerequisites

| **Resource** | Notes |
| :--- | :--- |
| Collibra Edge Site | DQ Connector is a capability of Edge |
| Collibra Data Intelligence Cloud | 2021.07 Release \(or newer\) |
| Collibra Data Quality | 2.15 \(or newer\) |
| Database\(s\) and Driver\(s\) | Proper Access and Credentials \(Username / Password\) |

{% hint style="success" %}
Let's proceed after gathering all prerequisites!
{% endhint %}

## Step 1: Create and Configure Edge and DQ Connector

**1A. Create Edge site and Add Name e.g. 'Collibra-DQ-Edge' and Description \(One-Time\)**

![Where: Collibra Data Intelligence Cloud Settings -&amp;gt; Edge -&amp;gt; Click &#x2018;Create Edge site&#x2019;](https://lh6.googleusercontent.com/H7aAEkqf4L0RK6xhTSG4yONGafGKhUvHiSz1SPh9c7kyEPfXmhkwWKtr3twcZt6SMo_KBWj4JNStxURftlc3qeQ7VCyZXng3gUu6GHTCKjoIgMSYwy2tAcyRP_KFUImGVrYN2tYC)

![](https://lh3.googleusercontent.com/Eyo8SV3nasLqqvXPw0zanZopx7sTV0G7SBcuYt63aI4YmZBXW9DgAHalQWfifNFwhTI5e9Qc3SpsfM3MWFHB6oVLBCeAHlkicRQ9FsBEEKnZ6KJZKuNyF7rmIOKVDch-unS4oAFJ)

{% hint style="info" %}
**Please see:** [**https://productresources.collibra.com/docs/cloud-edge/latest/Default.htm**](https://productresources.collibra.com/docs/cloud-edge/latest/Default.htm) **for more detailed information on Edge installation and configuration**
{% endhint %}

**1B. Establish Edge’s Connection To Each Data Source \(One-Time For Each Source\)**

Additional Steps in Collibra DG include:

* Provide Connection Name which exactly matches Connection / System Name in Collibra DQ
* Select Connection type e.g. Username / Password JDBC driver
* Input Username and Password to connect to your data source 
* Input fully qualified driver class name 
* Upload Driver jar \(to reduce potential conflicts, use same driver jar from Collibra DQ\) 
* Input Connection String Input credentials e.g. username / password or Kerberos config file 
* Reminder: All of the above information should be the same as in Collibra DQ

Additional Steps in Collibra DQ include:

* Verify Connection ‘Name’ in DGC matches Connection ‘Name’ in Collibra DQ
* Verify ‘Connection string’ in DGC matches ‘Connection URL’ in Collibra DQ
* Verify ‘Driver class name’ in DGC matches ‘Driver Name’ in Collibra DQ
* Verify ‘Driver jar’ in DGC matches Driver used in ‘Driver Location’ in Collibra DQ \(may require SSH\)

![Where: Settings -&amp;gt; Edge -&amp;gt; Select Edge site -&amp;gt; JDBC Connections -&amp;gt; Select &#x2018;Create connection&#x2019;](https://lh5.googleusercontent.com/-3FpYTn4vo4kWogSJNgPi4afMwty1a8pk-2_m-bYYTAz195caF4jRbB0OF2bC0U1t559jNLOvXVAgRLt32EpWL5IEjpB8nqUZ0R1A98ODxKmC9GGCavw0Ad5iXTHss0nhCtcsK1W)

{% hint style="warning" %}
**Important: Connection / System name \(in this example, ‘postgres-gcp’\) must exactly match the Connection / System Name in Collibra DQ**
{% endhint %}

**1C. Establish Catalog JDBC Ingestion Capability On Edge \(One-Time For Each Data Source\)**

![Where: Settings -&amp;gt; Edge -&amp;gt; Capabilities -&amp;gt; Input Name -&amp;gt; &apos;Catalog JDBC Ingestion&apos; ](https://lh3.googleusercontent.com/7To6AMTiyioNVZeZwK9pzi14Y7D1vCbAyRV4vj7iteI0wz30cGJI4jNaXO9gtLDSEwhltZnHwr48-NWSbFYtU9LJot7UBovm6-yyEoURnol-ksZ0F-Q81tRVOwYYKvnzesWKB19s)

**1D: Configure Destinations For DQ Assets \(Rules, Metrics, Dimensions\) Within DQ Connector \(One-Time\)**

Option A: Create New Destinations

* Create New Rulebook Domain \(suggested domain type\) for DQ Rules
  * Global Create -&gt; Search for and select 'Rulebook' under 'Governance Asset Domain' -&gt; Select desired 'Community' e.g. 'Data Governance Council' -&gt; Input name of Rulebook domain e.g. 'CDQ Rules'

{% hint style="info" %}
Record your domain resource ID e.g. 2xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx \(can be found in your URL\) for Step 1G
{% endhint %}

* Create New Business Asset Domains \(suggested domain type\) for DQ Metrics and DQ Dimensions
  * Global Create -&gt; Search for and select 'Business Asset Domain' under 'Business Asset Domain' -&gt; Select desired 'Community' e.g. 'Data Governance Council' -&gt; Input name of domain e.g. 'Collibra DQ Metrics'
  * Record your domain resource ID e.g. 2xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx \(can be found in your URL\)

Option B: Use Existing Domains from existing Rulebook and Asset domains

{% hint style="info" %}
Record your domain resource ID e.g. 2xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx \(can be found in your URL\) for Step 1G
{% endhint %}

![](https://lh3.googleusercontent.com/LOR_nFMAjSrFUPNoOLqjEvDAxwBoeHsjYU_c_QsgH3QgRH-y8_Uvtn2kfMesE68VcYDrpp1raPKOumsOAyoVek32I2x-e9OskR-JUDV8GxdmtFNOMK6iKTvcDejs56PXpmvh6pa1)

{% hint style="success" %}
You have now established destinations for where Collibra should ingest your User-Defined Rules, Metrics, and Dimensions
{% endhint %}

**1E. Assign Permissions for New Domains of DQ Assets \(Rules, Metrics, Dimensions\) \(One-Time\)**

![](https://lh3.googleusercontent.com/U5NnQT6ncu6XbL7YKWe8A0caumHxodHBCgU_vJeJjWCyxYSzvGsRWWzH2HjjeVKYih4hvGXvDM7J1_DB72EgdxoVLrRTNEQsg4enZotY7fEgjfxfI-cbz4vmFHxxzxEBQfUq_ZpF)

{% hint style="success" %}
This step provides Edge with the proper permissions to create and update assets into the domains from the previous step
{% endhint %}

**1F. Allow DQ Assets To Attach To Tables and Column Assets \(One-Time\)**

Now we need to add a few relations and update global assignment characteristics

* **Table**: Settings -&gt; Operating Model -&gt; Relations -&gt; Search in any column for 'Table' -&gt; Global Assignment -&gt; Characteristics -&gt; Edit \(larger of the two buttons\) on right -&gt; Add characteristic -&gt; Search for and select 'governed by Governance Asset' -&gt; Save

![](https://lh5.googleusercontent.com/RYKx_CdwVsVauaJPmjP7yDlZzzTVCeLzcTQHix2wSOmgo8taapeg8lU87L5qatGIrbPKATLMEvN7skj7JHtqGJjMXGuJcVpWD5BToX1W92Q2edGs3ODi3CZ1C4WQX9MMW9bdmKFw)

* **Column**: Settings -&gt; Operating Model -&gt; Relations -&gt; Search in any column for 'Column' -&gt; Global Assignment -&gt; Characteristics -&gt; Edit \(larger of the two buttons\) on right -&gt; Add characteristic -&gt; Search for and select 'is governed by Data Quality Rule' -&gt; Save

![](https://lh5.googleusercontent.com/JhUNVCCoHxkamUgeLsQ98tWPPvHeUNiGB6EjH_wEugZ5OaenbQbTEL6bVv6W2EiyqtnivaDjCsoHagW0Q6U6s5GDpC37_vnVND_qhPGaZDw9GoUry6vrBqiSUwAABfi1npUO18_E)

**1G. Establish DQ Connector \(One-Time\)**

DQ Connector is an Edge capability that will facilitate communication with your Collibra DQ instance

* Settings -&gt; Edge -&gt; Capabilities -&gt; Add Capability -&gt; Select 'DQ Connector' -&gt; Input your Collibra DQ URL e.g. 'customerdq.collibra.com:port' input username and password

{% hint style="info" %}
Remember from previous step 1D, you will need to provide your resource / UUIDs for your specified domains for DQ Rules, Metrics, and Dimensions
{% endhint %}

![](https://lh4.googleusercontent.com/nRWd59wkPl_yXKwCsgfvBuFMdiAwlW6nBoN1eV7c2YHN-Y2cHbC82TwGRiub297mQ0uBphUL4vewsBzFOKhesF5gaY6W3Beft2VC4ILmrJZuW8oiqEa45JrvHPFI1QiFtlC4kgs_)

{% hint style="success" %}
Excellent! We've now completed the initial one-time configuration!
{% endhint %}

## Step 2: Register Edge Connections to Collibra Catalog

**2A. Create System Asset Within Collibra Catalog To Connect To Edge** 

![Global Create -&amp;gt; &apos;System&apos; -&amp;gt; Select Domain -&amp;gt; Enter Name e.g. &apos;postgres-gcp&apos;](https://lh4.googleusercontent.com/e19f1vFffMGQDzgHD1m83C66pG9MwOeJwrd8-Jl42oC9ArjXaCGrwfu_baSzdP4u1xelfB0YWHYA90tsT9g3NFHIE2ULhIdWnkZRUYi8f1sq8EIltYnm_BhC-yVDSknI_9ndGpB0)

{% hint style="warning" %}
**Important: Connection / System name \(in this example, ‘postgres-gcp’\) must exactly match the Connection / System Name in Collibra DQ**
{% endhint %}

**2B. Register Edge Data Source to Collibra Catalog**

![Where: Catalog -&amp;gt; Global &apos;Create&apos; -&amp;gt; Register Data Source with Edge](https://lh6.googleusercontent.com/NsIO-7QVn8gMLJi0YJmhC-gs-r26nPQWwQUY8-S2oQa-pWQAjMeJvo2ZvX5FYG3KqfrbuVE5U5aEeCj25kX19TuDL9MR4ves52EcMyadYgfbWIrC86rHinl7a_ZUnv2gW9IPRlIZ)

## **Step 3: Start Ingesting Collibra Data Quality Into Catalog**

{% hint style="info" %}
**Prerequisite: Catalog will have ingested schemas on Edge**
{% endhint %}

![Where: Catalog -&amp;gt; Data Sources -&amp;gt; Select Database e.g. &apos;postgres&apos; -&amp;gt; Configuration](https://lh6.googleusercontent.com/HgMjwe6cR3ne_GpzqhHQNdB5tMWhIsfg-mU5iLUq7oBZnuomANBVhPGdMSH8kCHBwonZQVp2EhFMQ6H4eH_P5t7lIGJrboU2y71Hy0HVvenK6uu8PeaxRCSQbEX1LbeKdSlBcdd7)

{% hint style="info" %}
**Prerequisite: Ensure targeted schemas have User-defined Rules, Metrics, and/or Dimensions within Collibra DQ**
{% endhint %}

**3A. Synchronize Data Quality for Selected Schemas**

![Catalog -&amp;gt; Data Sources -&amp;gt; Select Database -&amp;gt; Configuration -&amp;gt; Quality Extraction](https://lh4.googleusercontent.com/Xt8y_PfQ3UZAWBdW6PTWTSX0ZU2830Z-MJykaugTuaWIFIyJR3Hdy0WmijTlFn47yhozmxVe-idXGk7u8wVlfCbk7qIAJMItx44pYVvDIDgjeL62DZ3i38ZrnBjTfwKhB9qa8Irs)

**3B. Verify Data Quality Results in Collibra Catalog**

![](https://lh4.googleusercontent.com/syFKZtlFsc0QAv2OwFx10oVNSfgUaA6fe004elBAWo8DXKXDKUdCpsuOyVK5zVNmhKwnYLLQi_XdKV7B4BcTKLqtov4QCK2b_MoSHDneKm0abhXv0BE33pQjtOfWb2IE4nJIpWNd)

