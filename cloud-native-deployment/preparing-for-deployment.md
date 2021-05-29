# Preparing for Cloud Native Deployment

## Minimum Requirements

* Owl Web 
  * 1 core
  * 2 GB Memory
  * 10MB PVC Storage
* Owl Agent
  * 1 core
  * 1GB Memory
  * 100MB PVC Storage
* Owl Metastore
  * 1 core
  * 2 GB Memory
  * 10GB PVC Storage
* Spark Compute
  * 2 cores \*
  * 2GB memory \*
  * This is the minimum quantity of resources required to run an a Spark Job in Kubernetes. This amount of resources would only provide the ability to scan a few megabytes of data with no more than a single job running at a given time. Proper sizing of the compute space must take into account the largest dataset that may be scanned, as well as the desired concurrency.

## Network Service Considerations

Owl Web is the only required component that needs to be directly accessed from outside of Kubernetes. History Server is the only other component that can be accessed directly by users, however, it is optional. 

If the target Kubernetes platform supports LoadBalancer service type, the Helm chart can be configured to directly deploy the externally accessible endpoint. It is also possible to configure the Helm Chart to deploy a NodePort service type, however, this is not recommended for anything other than testing purposes. 

If the desired service type is Ingress, the recommended approach is to deploy OwlDQ without an externally accessible service and then attach the Ingress service separately. This applies when a third-party Ingress controller is being used \(NGINX, Contour, ect\). The Helm Chart is able to deploy an Ingress on GKE and EKS platforms, however, there is a wide variety of possible Ingress configurations that have not been tested.

## Obtaining Credentials

Kubernetes stores credentials in the form of Secrets. Secrets are base64 encoded files that can be mounted into application containers and referenced by application components at runtime. Secrets can also be used to access secured container registries to obtain application containers. These types of credentials are referred to as "pull secrets".

### SSL Certificates

In order to enable SSL for secure access to Owl Web, a keystore that contains a signed certificate, keychain, and private key is required. This keystore must be available in the target namespace prior to Owl DQ deployment. It is possible to deploy with SSL disabled, however, that is not recommended. By default, OwlDQ will look for a secret called "owldq-ssl-secret" to find the keystore.

### Cloud Storage Credentials

If History Server is enabled, then a distributed filesystem is required. Currently, OwlDQ supports S3 and GCS for Spark history log storage. Azure Blob and HDFS on the near term roadmap. 

* If S3 is the target storage system, and IAM Role with access to the target bucket needs to be attached to the Kubernetes nodes of the namespace where OwlDQ is being deployed. 
* If GCS is the target storage system, then a secret must be created from the JSON key file of a service account with access the the log bucket. The secret must be available in the namespace prior to deploying OwlDQ. By default, OwlDQ will look for a secret called "spark-gcs-secret", if GCS is enabled for Spark history logs. This can be changed via a helm chart argument.

### Container Pull Secret

OwlDQ containers are stored in a secured repository in Google Container Registry. In order for OwlDQ to successfully pull the containers upon deployment, a pull secret with access to the container registry must be available in the target namespace. By default, OwlDQ will look for a pull secret named "owldq-pull-secret". This can be changed via a helm chart argument.

### Spark Service Account

In order for Owl Agent and Spark driver to create and destroy compute containers, a service account with a Role that allows get/list/create/delete operations on pods/services/secrets/configMaps within the target namespace. By default, OwlDQ will attempt to create the required service account as well as the required RoleBinding to the default role called "Edit". Edit is a default Role that is generally available in a Kubernetes clusters by default. If the Edit Role is not available, then it will need to be created manually.

## Access the Platform

In order to deploy anything to a Kubernetes cluster, the first step is to install the required client utilities and configure access. 

* **kubectl** - the main method of communication with a Kubernetes cluster. All configuration or introspection tasks will be preformed using kubectl.
* **helm** \(V3\) - used to deploy the OwlDQ helm chart without hand coding manifests.

After utilities are installed, the next step is to configure a kube-context that points to and authenticates to the target platform. On cloud platforms like GKE and EKS, this process is completely automated through their respective CLI utilities.

```text
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

```text
gcloud container clusters get-credentials <cluster-name>
```

In private clouds, this process will vary from organization to organization, however, the platform infrastructure team should be able to provide the target kube-context entry.

## Preparing Secrets

Once access to the target platform is confirmed, namespace preparation can begin. Typically the namespace that OwlDQ is going to be deployed into will be pre-allocated by the platform team. 

```text
kubectl create namespace <namespace>
```

There is a lot more that can go into namespace create such as resource quota allocation, but that is generally a task for the platform team.

#### Create SSL Keystore Secret

```text
kubectl create secret generic owldq-ssl-secret \
--from-file /path/to/keystore.jks \
--namespace <namespace>
```

{% hint style="warning" %}
The file name that is passed to the --from-file argument should be keystore.jks. If the file name is anything else, an additional argument specifying the keystore file name must be included in the Helm command.
{% endhint %}

#### Create Container Pull Secret

```text
#Json Key file credential
kubectl create secret docker-registry owldq-pull-secret \
--docker-server=<owldq-registry-server> \
--docker-username=_json_key \
--docker-email=<service-account-email> \
--docker-password="$(cat /path/to/key.json)" \
--namespace <namespace>
```

```text
#Short lived access token
kubectl create secret docker-registry owldq-pull-secret \
--docker-server=<owldq-registry-server> \
--docker-username=oauth3accesstoken \
--docker-email=<service-account-email> \
--docker-password="<access-token-text>" \
--namespace <namespace>
```

{% hint style="warning" %}
GCP Oauth tokens are usually only good for 1 hour. This type of credential is excellent if the goal is to pull containers into a private registry. It can be used as the pull secret to access containers directly, however, the secret would have to be recreated with a fresh token before restarting any of the OwlDQ components. 
{% endhint %}

#### Create GSC Credential Secret

```text
kubectl create secret generic spark-gcs-secret \
--from-file /path/to/keystore.jks \
--namespace <namespace>
```

{% hint style="warning" %}
The file name that is passed to the --from-file argument should be spark-gcs-secret. If the file name is anything else, an additional argument specifying the gcs secret name must be included in the Helm command.
{% endhint %}

