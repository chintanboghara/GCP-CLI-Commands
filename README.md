# Google Cloud Platform CLI Commands

The `gcloud` CLI is the primary command-line tool for interacting with Google Cloud Platform services.

## Table of Contents
1. [Installation and Setup](#installation-and-setup)
2. [Basic Commands](#basic-commands)
3. [Compute Engine (VMs)](#compute-engine-vms)
4. [Cloud Storage](#cloud-storage)
5. [Identity and Access Management (IAM)](#identity-and-access-management-iam)
6. [Kubernetes Engine (GKE)](#kubernetes-engine-gke)
7. [Cloud SQL](#cloud-sql)
8. [Cloud Functions](#cloud-functions)
9. [App Engine](#app-engine)
10. [Cloud Run](#cloud-run)
11. [BigQuery](#bigquery)
12. [Networking](#networking)
13. [Monitoring and Logging](#monitoring-and-logging)
14. [Cloud Pub/Sub](#cloud-pubsub)
15. [Cloud Build](#cloud-build)
16. [Cloud DNS](#cloud-dns)
17. [Cloud IAM Service Accounts](#cloud-iam-service-accounts)
18. [Cloud Key Management Service (KMS)](#cloud-key-management-service-kms)
19. [Scripting and Automation](#scripting-and-automation)

### Installation and Setup

#### Install Google Cloud CLI (`gcloud`)
- **Linux**:
  ```bash
  curl https://sdk.cloud.google.com | bash
  exec -l $SHELL
  ```
- **macOS**:
  ```bash
  curl https://sdk.cloud.google.com | bash
  exec -l $SHELL
  ```
- **Windows**:
  Download and run the installer from the [official website](https://cloud.google.com/sdk/docs/install).

#### Initialize `gcloud`
```bash
gcloud init
```
- Sets up your GCP project, authentication, and default configurations.

#### Authenticate with GCP
```bash
gcloud auth login
```
- Opens a browser window to log in with your Google account.

#### Set Default Project
```bash
gcloud config set project <project-id>
```

#### List Available Projects
```bash
gcloud projects list
```

---

### Basic Commands

#### Get Help
```bash
gcloud help
```

#### List Available Commands
```bash
gcloud --help
```

#### Check `gcloud` Version
```bash
gcloud version
```

#### Update `gcloud` CLI
```bash
gcloud components update
```

#### Set Default Region and Zone
```bash
gcloud config set compute/region <region>
gcloud config set compute/zone <zone>
```

---

### Compute Engine (VMs)

#### Create a VM Instance
```bash
gcloud compute instances create <instance-name> \
  --machine-type <machine-type> \
  --zone <zone> \
  --image-family <image-family> \
  --image-project <image-project>
```

#### List VM Instances
```bash
gcloud compute instances list
```

#### Start a VM Instance
```bash
gcloud compute instances start <instance-name> --zone <zone>
```

#### Stop a VM Instance
```bash
gcloud compute instances stop <instance-name> --zone <zone>
```

#### Delete a VM Instance
```bash
gcloud compute instances delete <instance-name> --zone <zone>
```

#### SSH into a VM Instance
```bash
gcloud compute ssh <instance-name> --zone <zone>
```

#### Create a Snapshot of a Disk
```bash
gcloud compute disks snapshot <disk-name> --snapshot-name <snapshot-name> --zone <zone>
```

---

### Cloud Storage

#### Create a Bucket
```bash
gsutil mb gs://<bucket-name>
```

#### List Buckets
```bash
gsutil ls
```

#### Upload a File to a Bucket
```bash
gsutil cp <local-file> gs://<bucket-name>/<path>
```

#### Download a File from a Bucket
```bash
gsutil cp gs://<bucket-name>/<path> <local-file>
```

#### Sync a Local Directory with a Bucket
```bash
gsutil rsync -r <local-directory> gs://<bucket-name>/<path>
```

#### Delete a Bucket
```bash
gsutil rm -r gs://<bucket-name>
```

#### Set Bucket Permissions (Make Public)
```bash
gsutil iam ch allUsers:objectViewer gs://<bucket-name>
```

---

### Identity and Access Management (IAM)

#### List IAM Roles for a Project
```bash
gcloud projects get-iam-policy <project-id>
```

#### Add IAM Policy Binding to a Project
```bash
gcloud projects add-iam-policy-binding <project-id> \
  --member <member> \
  --role <role>
```

#### Remove IAM Policy Binding from a Project
```bash
gcloud projects remove-iam-policy-binding <project-id> \
  --member <member> \
  --role <role>
```

#### Create a Custom IAM Role
```bash
gcloud iam roles create <role-name> \
  --project <project-id> \
  --title "<role-title>" \
  --description "<description>" \
  --permissions <comma-separated-permissions>
```

---

### Kubernetes Engine (GKE)

#### Create a GKE Cluster
```bash
gcloud container clusters create <cluster-name> \
  --zone <zone> \
  --num-nodes <num-nodes>
```

#### Get Credentials for a GKE Cluster
```bash
gcloud container clusters get-credentials <cluster-name> --zone <zone>
```

#### List GKE Clusters
```bash
gcloud container clusters list
```

#### Delete a GKE Cluster
```bash
gcloud container clusters delete <cluster-name> --zone <zone>
```

#### Scale a GKE Cluster
```bash
gcloud container clusters resize <cluster-name> \
  --node-pool <node-pool-name> \
  --num-nodes <new-num-nodes> \
  --zone <zone>
```

---

### Cloud SQL

#### Create a Cloud SQL Instance
```bash
gcloud sql instances create <instance-name> \
  --database-version <db-version> \
  --tier <machine-type> \
  --region <region>
```

#### List Cloud SQL Instances
```bash
gcloud sql instances list
```

#### Create a Database in a Cloud SQL Instance
```bash
gcloud sql databases create <database-name> --instance <instance-name>
```

#### Connect to a Cloud SQL Instance
```bash
gcloud sql connect <instance-name> --user <user>
```

#### Backup a Cloud SQL Instance
```bash
gcloud sql backups create --instance <instance-name> --description "<description>"
```

---

### Cloud Functions

#### Deploy a Cloud Function
```bash
gcloud functions deploy <function-name> \
  --runtime <runtime> \
  --trigger-http \
  --allow-unauthenticated
```

#### List Cloud Functions
```bash
gcloud functions list
```

#### Describe a Cloud Function
```bash
gcloud functions describe <function-name>
```

#### Delete a Cloud Function
```bash
gcloud functions delete <function-name>
```

#### View Logs for a Cloud Function
```bash
gcloud functions logs read <function-name>
```

---

### App Engine

#### Deploy an App to App Engine
```bash
gcloud app deploy <app.yaml>
```

#### List App Engine Versions
```bash
gcloud app versions list
```

#### Browse the App
```bash
gcloud app browse
```

#### Create an App Engine Application
```bash
gcloud app create --region <region>
```

#### View App Engine Logs
```bash
gcloud app logs read
```

---

### Cloud Run

#### Deploy a Container to Cloud Run
```bash
gcloud run deploy <service-name> \
  --image <container-image> \
  --platform managed \
  --region <region>
```

#### List Cloud Run Services
```bash
gcloud run services list
```

#### Describe a Cloud Run Service
```bash
gcloud run services describe <service-name>
```

#### Delete a Cloud Run Service
```bash
gcloud run services delete <service-name>
```

#### Get the URL of a Cloud Run Service
```bash
gcloud run services describe <service-name> --format='value(status.url)'
```

---

### BigQuery

#### Create a Dataset
```bash
bq mk <dataset-name>
```

#### List Datasets
```bash
bq ls
```

#### Create a Table
```bash
bq mk --table <dataset-name>.<table-name> <schema>
```

#### Load Data into a Table
```bash
bq load --source_format=CSV <dataset-name>.<table-name> <gs://bucket/file.csv> <schema>
```

#### Query a Table
```bash
bq query --use_legacy_sql=false "SELECT * FROM <dataset-name>.<table-name> LIMIT 10"
```

---

### Networking

#### Create a VPC Network
```bash
gcloud compute networks create <network-name> --subnet-mode custom
```

#### Create a Subnet
```bash
gcloud compute networks subnets create <subnet-name> \
  --network <network-name> \
  --range <cidr-range> \
  --region <region>
```

#### List VPC Networks
```bash
gcloud compute networks list
```

#### Create a Firewall Rule
```bash
gcloud compute firewall-rules create <rule-name> \
  --network <network-name> \
  --allow tcp:80,tcp:443 \
  --source-ranges 0.0.0.0/0
```

#### List Firewall Rules
```bash
gcloud compute firewall-rules list
```

---

### Monitoring and Logging

#### List Log Entries
```bash
gcloud logging read "resource.type=gce_instance"
```

#### List Metrics
```bash
gcloud monitoring dashboards list
```

#### Create an Alert Policy
```bash
gcloud alpha monitoring policies create --policy-from-file <policy.json>
```

#### View Logs for a Specific Resource
```bash
gcloud logging read "resource.type=gce_instance AND resource.labels.instance_id=<instance-id>"
```

---

### Cloud Pub/Sub

#### Create a Topic
```bash
gcloud pubsub topics create <topic-name>
```

#### List Topics
```bash
gcloud pubsub topics list
```

#### Publish a Message to a Topic
```bash
gcloud pubsub topics publish <topic-name> --message "Hello, Pub/Sub!"
```

#### Create a Subscription
```bash
gcloud pubsub subscriptions create <subscription-name> --topic <topic-name>
```

#### Pull Messages from a Subscription
```bash
gcloud pubsub subscriptions pull <subscription-name>
```

---

### Cloud Build

#### Submit a Build
```bash
gcloud builds submit --tag gcr.io/<project-id>/<image-name>
```

#### List Builds
```bash
gcloud builds list
```

#### View Build Logs
```bash
gcloud builds log <build-id>
```

#### Cancel a Build
```bash
gcloud builds cancel <build-id>
```

---

### Cloud DNS

#### Create a Managed Zone
```bash
gcloud dns managed-zones create <zone-name> --dns-name <dns-name> --description "<description>"
```

#### List Managed Zones
```bash
gcloud dns managed-zones list
```

#### Add a DNS Record
```bash
gcloud dns record-sets transaction start --zone <zone-name>
gcloud dns record-sets transaction add <ip-address> --name <record-name> --ttl 300 --type A --zone <zone-name>
gcloud dns record-sets transaction execute --zone <zone-name>
```

#### List DNS Records
```bash
gcloud dns record-sets list --zone <zone-name>
```

---

### Cloud IAM Service Accounts

#### Create a Service Account
```bash
gcloud iam service-accounts create <service-account-name> --display-name "<display-name>"
```

#### List Service Accounts
```bash
gcloud iam service-accounts list
```

#### Create a Service Account Key
```bash
gcloud iam service-accounts keys create <key-file> --iam-account <service-account-email>
```

#### Add IAM Policy Binding to a Service Account
```bash
gcloud projects add-iam-policy-binding <project-id> \
  --member serviceAccount:<service-account-email> \
  --role <role>
```

---

### Cloud Key Management Service (KMS)

#### Create a Key Ring
```bash
gcloud kms keyrings create <keyring-name> --location <location>
```

#### Create a CryptoKey
```bash
gcloud kms keys create <key-name> --keyring <keyring-name> --location <location> --purpose encryption
```

#### Encrypt a File
```bash
gcloud kms encrypt --key <key-name> --keyring <keyring-name> --location <location> --plaintext-file <input-file> --ciphertext-file <output-file>
```

#### Decrypt a File
```bash
gcloud kms decrypt --key <key-name> --keyring <keyring-name> --location <location> --ciphertext-file <input-file> --plaintext-file <output-file>
```

---

### Scripting and Automation

#### Run a Script with `gcloud`
```bash
#!/bin/bash
gcloud config set project <project-id>
gcloud compute instances create <instance-name> --zone <zone> --machine-type <machine-type>
```

#### Export Configuration to a File
```bash
gcloud config configurations export <config-name> --destination <file-path>
```

#### Import Configuration from a File
```bash
gcloud config configurations import <config-name> --source <file-path>
```

#### Use `gcloud` in CI/CD Pipelines
```bash
# Example: Deploy to Cloud Run in a CI/CD pipeline
gcloud builds submit --tag gcr.io/<project-id>/<image-name>
gcloud run deploy <service-name> --image gcr.io/<project-id>/<image-name> --platform managed --region <region>
```
