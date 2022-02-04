# Google Cloud Engineer Path

compute engine
app engine
cloud storage
cloud pub/sub
big query

resources inherit from parent the policies . downwards

IAM
---- 

who can take action on specific resource ( google account, cloud identity user, service account, google group, cloud identity or G suite domain)

can do what

on which resource

IAM role - collection of permissions

- primitive ( owner / editor / viewer / billing administrator )
- predefined roles / custom roles
- service account - cryptographic keys to access resources



Cloud BigTable - nosql
BigQuery - datewarehouse

Ways to interact with GCP
-----------------------
- GCP console - cloud shell
- Google Cloud SDK - gcloud, gsutil ( CloudStorage ), bq ( BigQuery)
- RESTful APIs - APIs Explorer
- use client libraries to control gcp resources - java, python
- cloud console mobile app


CloudLauncher - CloudMarketPlace
--------------------------------

- ready to deploy solution for applications
- easy to deploy your app on a stack
- practice with qwiklabs
- deployment manager

VPC ( Virtual private cloud)
----------------------------
- define network inside
- connect resources with each other and with internet

Compute Engine
---------------
- persistent disks: standard or SSD storage
- boot image
- define a startup script if you like
- take disk snapshots as backups
- use autoscaling for resilient scalable applications



VPC routing tables, across subnet networks

- firewall rules to control what network traffic is allowed
- vpc peering to interconnect networks in gcp projects
- shared vpc

Cloud Load Balancing
- global https
- global ssl proxy
- global tcp proxy
- regional
- regional internal

8.8.8.8

Cloud DNS
- create managed zones then add,edit,delete DNS records
- programmaticaly manage this


Cloud CDN ( content delivery network)
- lower network latency

```
gcloud compute zones list | grep us-central1
gcloud config set compute/zone us-central1-b


gcloud compute instances create "my-vm-2" \
--machine-type "n1-standard-1" \
--image-project "debian-cloud" \
--image-family "debian-10" \
--subnet "default"


ping my-vm-1.us-central1-a

ssh my-vm-1.us-central1-a



```


Google Cloud Storage services
------------------------

- cloud storage object store service, buckets ; location to minimize latency; ACL (Access control lists); delete objects within a timeframe
- cloud bigtable, nosql, wide-column database service for terrabyte applications ( persistent hashtable, high throughput, compatibility with hadoop, accessed using HBASe API -- scalability ); application api / streaming / batch processing
- Google cloud sql - mysql and postgresqlBeta databases as a service rdbms ; read/failover/replicate; scaling
- Google cloud spanner - transactional consistency on horizontal - petabytes levels; shardding; global data - financial/inventory applications
- Cloud datastore - structured data from app engine apps; horizontally scaling; sharding and replications; designed for application backends
free daily quota for reads/writes and small operations at no charge


vm example of startup script
```
apt-get update
apt-get install apache2 php php-mysql -y
service apache2 restart
```

10.128.0.2 internal
34.133.134.167 external

```
export LOCATION=US

gsutil mb -l $LOCATION gs://$DEVSHELL_PROJECT_ID

gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png my-excellent-blog.png

gsutil cp my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png


```

Google Kubernetes Engine
------------------------

Iaas - Compute Engine
PaaS - App Engine


The nodes in the Kube engine clusters are vms, you can see them in the compute engine -> vm instances


```
export MY_ZONE=us-central1-a
gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
kubectl version

kubectl create deploy nginx --image=nginx:1.17.10
kubectl get pods
kubectl expose deployment nginx --port 80 --type LoadBalancer

kubectl get services
kubectl scale deployment nginx --replicas 3

kubectl get pods
kubectl get services
```

Google App Engine
------------------------

Paas building scalable applications

Standard ( sandbox )

- easily deploy your applications
- free daily usage quota
- usage based pricing
- auto scaling
- sdks for dev/testing and deployment

Flexible

- build and deploy containerized apps with a click


```
gcloud auth list
gcloud config list project
gcloud app create --project=$DEVSHELL_PROJECT_ID
git clone https://github.com/GoogleCloudPlatform/python-docs-samples
cd python-docs-samples/appengine/standard_python3/hello_world
sudo apt-get update
sudo apt-get install virtualenv
virtualenv -p python3 venv
source venv/bin/activate
pip install  -r requirements.txt
python main.py



cd ~/python-docs-samples/appengine/standard_python3/hello_world
gcloud app deploy
gcloud app browse
```

Google Cloud Endpoints and Apigee Edge
------------------------


