# Deploying Cloud Native OwlDQ

## Deploy OwlDQ

Once the namespace has been created and all of the required secrets added, deployment of OwlDQ can begin.

#### Minimal Install

Installs Web, Agent, and Metastore. OwlDQ is inaccessible until an Ingress or another type of externally accessible service is added manually.

{% hint style="warning" %}
All of the following examples will pull containers directly from the Collibra DQ secured container registry. In most cases, InfoSec policies requires that containers are sourced from a private container repository controlled by the local Cloud Ops team. Make sure to to add  
--set global.image.repo=&lt;/url/of/private-repo&gt; to make sure that only approved containers are used.
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=ClusterIP \
<deployment-name> \
/path/to/chart/owldq
```

#### Externally Accessible Service

Minimal install, plus preconfigured NodePort or LoadBalancer service to provide access to Web. 

{% hint style="warning" %}
LoadBalancer service type will requires that the Kubernetes platform is integrated with a Software Defined Network solution. This will generally be true of major cloud vendor's Kubernetes service. Private cloud platforms more commonly use Ingress controllers. Check with the infrastructure team before attempting to use LoadBalancer service type. 
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
<deployment-name> \
/path/to/chart/owldq
```

#### Externally Accessible with SSL Enabled

Install with External Service but with SSL enabled.

{% hint style="info" %}
Make sure that a keystore containing a key is already deployed to the target namespace with a secret name that matches global.web.tls.key.secretName argument \(owldq-ssl-secret by default\). Also, make sure that the Secret's key name matches the global.web.tls.key.store.name argument \(dqkeystore.jks by default\). 
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.web.tls.enabled=true \
--set global.web.tls.key.secretName=owldq-ssl-secret \
--set global.web.tls.key.alias=<key-alias> \
--set global.web.tls.key.type=<JKS || PKCS12> \
--set global.web.tls.key.pass=<keystore-pass> \
--set global.web.tls.key.store.name=keystore.jks \ 
<deployment-name> \
/path/to/chart/owldq
```

#### Externally Accessible and History Server \(GCS Log Storage\)

Install with External Service and Spark History server enabled. In this example, the target log storage system is GCS. 

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.spark_history.enabled=true \
--set global.spark_history.logDirectory=gs://logs/spark-history/ \
--set global.spark_history.service.type=<NodePort || LoadBalancer> \
--set global.cloudStorage.gcs.enableGCS=true \
<deployment-name> \
/path/to/chart/owldq
```

#### Externally Accessible and History Server \(S3 Log Storage\)

Install with External Service and Spark History server enabled. In this example, the target log storage system is S3. 

{% hint style="info" %}
In order for OwlDQ to be able to write Spark logs to S3, makes sure that an Instance Profile IAM Role with access to the log bucket is attached to all nodes serving the target namespace.
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.spark_history.enabled=true \
--set global.spark_history.logDirectory=s3a://logs/spark-history/ \
--set global.spark_history.service.type=<NodePort || LoadBalancer> \
--set global.cloudStorage.s3.enableS3=true \
<deployment-name> \
/path/to/chart/owldq
```

#### Externally Accessible with External Metastore

Install with External Service and an External Metastore, for example AWS RDS, Google Cloud SQL, or just plain old PostgresSQL on its own instance. 

{% hint style="warning" %}
OwlDQ currently supports PostgreSQL 9.6 and up
{% endhint %}

```bash
helm upgrade --install --namespace <namespace> \
--set global.version.owl=<owl-version> \
--set global.version.spark=<owl-spark-version> \
--set global.configMap.data.license_key=<owl-license-key> \
--set global.web.service.type=<NodePort || LoadBalancer> \
--set global.metastore.enabled=false                                        
--set global.configMap.data.metastore_url=jdbc:postgresql://<host>:<port>/<database>
--set global.configMap.data.metastore_user=<user> \
--set global.configMap.data.metastore_pass=<password> \
<deployment-name> \
/path/to/chart/owldq
```

