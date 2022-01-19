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