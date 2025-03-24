# GCP CLI Commands

The `gcloud` CLI is the primary command-line tool for interacting with Google Cloud Platform (GCP) services.

## Installation and Setup

### Install Google Cloud CLI (`gcloud`)

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

### Initialize `gcloud`

```bash
gcloud init
```
- Sets up your GCP project, authentication, and default configurations.

### Authenticate with GCP

```bash
gcloud auth login
```
- Opens a browser window to log in with your Google account.

### Set Default Project

```bash
gcloud config set project <project-id>
```

### List Available Projects

```bash
gcloud projects list
```

---

## Basic Commands

### Get Help

```bash
gcloud help
```

### List Available Commands

```bash
gcloud --help
```

### Check `gcloud` Version

```bash
gcloud version
```

### Update `gcloud` CLI

```bash
gcloud components update
```

### Set Default Region and Zone

```bash
gcloud config set compute/region <region>
gcloud config set compute/zone <zone>
```

---

## Compute Engine (VMs)

### Create a VM Instance

```bash
gcloud compute instances create <instance-name> \
  --machine-type <machine-type> \
  --zone <zone> \
  --image-family <image-family> \
  --image-project <image-project>
```

### List VM Instances

```bash
gcloud compute instances list
```

### Start a VM Instance

```bash
gcloud compute instances start <instance-name> --zone <zone>
```

### Stop a VM Instance

```bash
gcloud compute instances stop <instance-name> --zone <zone>
```

### Delete a VM Instance

```bash
gcloud compute instances delete <instance-name> --zone <zone>
```

### SSH into a VM Instance

```bash
gcloud compute ssh <instance-name> --zone <zone>
```

### Create a Snapshot of a Disk

```bash
gcloud compute disks snapshot <disk-name> --snapshot-name <snapshot-name> --zone <zone>
```

#### Additional Commands

- **Create a Disk**:
  ```bash
  gcloud compute disks create <disk-name> --size <size> --zone <zone>
  ```

- **Attach a Disk to a VM**:
  ```bash
  gcloud compute instances attach-disk <instance-name> --disk <disk-name> --zone <zone>
  ```

- **Create an Image from a Disk**:
  ```bash
  gcloud compute images create <image-name> --source-disk <disk-name> --source-disk-zone <zone>
  ```

- **List Images**:
  ```bash
  gcloud compute images list
  ```

---

## Cloud Storage

### Create a Bucket

```bash
gsutil mb gs://<bucket-name>
```

### List Buckets

```bash
gsutil ls
```

### Upload a File to a Bucket

```bash
gsutil cp <local-file> gs://<bucket-name>/<path>
```

### Download a File from a Bucket

```bash
gsutil cp gs://<bucket-name>/<path> <local-file>
```

### Sync a Local Directory with a Bucket

```bash
gsutil rsync -r <local-directory> gs://<bucket-name>/<path>
```

### Delete a Bucket

```bash
gsutil rm -r gs://<bucket-name>
```

### Set Bucket Permissions (Make Public)

```bash
gsutil iam ch allUsers:objectViewer gs://<bucket-name>
```

#### Additional Commands

- **Set Bucket Lifecycle Policy**:
  ```bash
  gsutil lifecycle set <lifecycle-config-file> gs://<bucket-name>
  ```

- **Get Bucket ACL**:
  ```bash
  gsutil acl get gs://<bucket-name>
  ```

- **List Objects in a Bucket**:
  ```bash
  gsutil ls gs://<bucket-name>
  ```

- **Delete an Object**:
  ```bash
  gsutil rm gs://<bucket-name>/<object-path>
  ```

---

## Identity and Access Management (IAM)

### List IAM Roles for a Project

```bash
gcloud projects get-iam-policy <project-id>
```

### Add IAM Policy Binding to a Project

```bash
gcloud projects add-iam-policy-binding <project-id> \
  --member <member> \
  --role <role>
```

### Remove IAM Policy Binding from a Project

```bash
gcloud projects remove-iam-policy-binding <project-id> \
  --member <member> \
  --role <role>
```

### Create a Custom IAM Role

```bash
gcloud iam roles create <role-name> \
  --project <project-id> \
  --title "<role-title>" \
  --description "<description>" \
  --permissions <comma-separated-permissions>
```

#### Additional Commands

- **List Custom IAM Roles**:
  ```bash
  gcloud iam roles list --project <project-id>
  ```

- **Describe an IAM Role**:
  ```bash
  gcloud iam roles describe <role-name> --project <project-id>
  ```

- **Update an IAM Role**:
  ```bash
  gcloud iam roles update <role-name> --project <project-id> --add-permissions <permissions>
  ```

---

## Kubernetes Engine (GKE)

### Create a GKE Cluster

```bash
gcloud container clusters create <cluster-name> \
  --zone <zone> \
  --num-nodes <num-nodes>
```

### Get Credentials for a GKE Cluster

```bash
gcloud container clusters get-credentials <cluster-name> --zone <zone>
```

### List GKE Clusters

```bash
gcloud container clusters list
```

### Delete a GKE Cluster

```bash
gcloud container clusters delete <cluster-name> --zone <zone>
```

### Scale a GKE Cluster

```bash
gcloud container clusters resize <cluster-name> \
  --node-pool <node-pool-name> \
  --num-nodes <new-num-nodes> \
  --zone <zone>
```

#### Additional Commands

- **Create a Node Pool**:
  ```bash
  gcloud container node-pools create <node-pool-name> --cluster <cluster-name> --zone <zone> --num-nodes <num-nodes>
  ```

- **List Node Pools**:
  ```bash
  gcloud container node-pools list --cluster <cluster-name> --zone <zone>
  ```

- **Update a Cluster**:
  ```bash
  gcloud container clusters update <cluster-name> --zone <zone> --enable-autoscaling --min-nodes <min> --max-nodes <max>
  ```

---

## Cloud SQL

### Create a Cloud SQL Instance

```bash
gcloud sql instances create <instance-name> \
  --database-version <db-version> \
  --tier <machine-type> \
  --region <region>
```

### List Cloud SQL Instances

```bash
gcloud sql instances list
```

### Create a Database in a Cloud SQL Instance

```bash
gcloud sql databases create <database-name> --instance <instance-name>
```

### Connect to a Cloud SQL Instance

```bash
gcloud sql connect <instance-name> --user <user>
```

### Backup a Cloud SQL Instance

```bash
gcloud sql backups create --instance <instance-name> --description "<description>"
```

#### Additional Commands

- **Restore from a Backup**:
  ```bash
  gcloud sql backups restore <backup-id> --restore-instance <instance-name>
  ```

- **List Databases**:
  ```bash
  gcloud sql databases list --instance <instance-name>
  ```

- **Delete a Database**:
  ```bash
  gcloud sql databases delete <database-name> --instance <instance-name>
  ```

---

## Cloud Functions

### Deploy a Cloud Function

```bash
gcloud functions deploy <function-name> \
  --runtime <runtime> \
  --trigger-http \
  --allow-unauthenticated
```

### List Cloud Functions

```bash
gcloud functions list
```

### Describe a Cloud Function

```bash
gcloud functions describe <function-name>
```

### Delete a Cloud Function

```bash
gcloud functions delete <function-name>
```

### View Logs for a Cloud Function

```bash
gcloud functions logs read <function-name>
```

#### Additional Commands

- **Invoke a Cloud Function**:
  ```bash
  gcloud functions call <function-name> --data '{"key": "value"}'
  ```

- **Update a Cloud Function**:
  ```bash
  gcloud functions deploy <function-name> --update-labels <labels>
  ```

---

## App Engine

### Deploy an App to App Engine

```bash
gcloud app deploy <app.yaml>
```

### List App Engine Versions

```bash
gcloud app versions list
```

### Browse the App

```bash
gcloud app browse
```

### Create an App Engine Application

```bash
gcloud app create --region <region>
```

### View App Engine Logs

```bash
gcloud app logs read
```

#### Additional Commands

- **Describe App Engine Service**:
  ```bash
  gcloud app services describe <service-name>
  ```

- **Delete an App Engine Version**:
  ```bash
  gcloud app versions delete <version-id>
  ```

---

## Cloud Run

### Deploy a Container to Cloud Run

```bash
gcloud run deploy <service-name> \
  --image <container-image> \
  --platform managed \
  --region <region>
```

### List Cloud Run Services

```bash
gcloud run services list
```

### Describe a Cloud Run Service

```bash
gcloud run services describe <service-name>
```

### Delete a Cloud Run Service

```bash
gcloud run services delete <service-name>
```

### Get the URL of a Cloud Run Service

```bash
gcloud run services describe <service-name> --format='value(status.url)'
```

#### Additional Commands

- **Set IAM Policy for Cloud Run Service**:
  ```bash
  gcloud run services add-iam-policy-binding <service-name> --member <member> --role <role>
  ```

- **List Revisions**:
  ```bash
  gcloud run revisions list --service <service-name>
  ```

---

## BigQuery

### Create a Dataset

```bash
bq mk <dataset-name>
```

### List Datasets

```bash
bq ls
```

### Create a Table

```bash
bq mk --table <dataset-name>.<table-name> <schema>
```

### Load Data into a Table

```bash
bq load --source_format=CSV <dataset-name>.<table-name> gs://<bucket-name>/<file.csv> <schema>
```

### Query a Table

```bash
bq query --use_legacy_sql=false "SELECT * FROM <dataset-name>.<table-name> LIMIT 10"
```

#### Additional Commands

- **Show Table Schema**:
  ```bash
  bq show --schema <dataset-name>.<table-name>
  ```

- **Delete a Table**:
  ```bash
  bq rm -t <dataset-name>.<table-name>
  ```

- **Run a Query Job**:
  ```bash
  bq query --destination_table <dataset-name>.<table-name> "SELECT * FROM <source-table>"
  ```

---

## Networking

### Create a VPC Network

```bash
gcloud compute networks create <network-name> --subnet-mode custom
```

### Create a Subnet

```bash
gcloud compute networks subnets create <subnet-name> \
  --network <network-name> \
  --range <cidr-range> \
  --region <region>
```

### List VPC Networks

```bash
gcloud compute networks list
```

### Create a Firewall Rule

```bash
gcloud compute firewall-rules create <rule-name> \
  --network <network-name> \
  --allow tcp:80,tcp:443 \
  --source-ranges 0.0.0.0/0
```

### List Firewall Rules

```bash
gcloud compute firewall-rules list
```

#### Additional Commands

- **Create a Static IP Address**:
  ```bash
  gcloud compute addresses create <address-name> --region <region>
  ```

- **List Static IP Addresses**:
  ```bash
  gcloud compute addresses list
  ```

- **Create a VPN Tunnel**:
  ```bash
  gcloud compute vpn-tunnels create <tunnel-name> --peer-address <peer-ip> --shared-secret <secret> --ike-version 2 --target-vpn-gateway <gateway-name>
  ```

---

## Monitoring and Logging

### List Log Entries

```bash
gcloud logging read "resource.type=gce_instance"
```

### List Metrics

```bash
gcloud monitoring dashboards list
```

### Create an Alert Policy

```bash
gcloud alpha monitoring policies create --policy-from-file <policy.json>
```

### View Logs for a Specific Resource

```bash
gcloud logging read "resource.type=gce_instance AND resource.labels.instance_id=<instance-id>"
```

#### Additional Commands

- **List Log Metrics**:
  ```bash
  gcloud logging metrics list
  ```

- **Create a Log-Based Metric**:
  ```bash
  gcloud logging metrics create <metric-name> --description "<description>" --log-filter "<filter>"
  ```

- **Export Logs to BigQuery**:
  ```bash
  gcloud logging sinks create <sink-name> bigquery.googleapis.com/projects/<project-id>/datasets/<dataset-name> --log-filter "<filter>"
  ```

---

## Cloud Pub/Sub

### Create a Topic

```bash
gcloud pubsub topics create <topic-name>
```

### List Topics

```bash
gcloud pubsub topics list
```

### Publish a Message to a Topic

```bash
gcloud pubsub topics publish <topic-name> --message "Hello, Pub/Sub!"
```

### Create a Subscription

```bash
gcloud pubsub subscriptions create <subscription-name> --topic <topic-name>
```

### Pull Messages from a Subscription

```bash
gcloud pubsub subscriptions pull <subscription-name>
```

#### Additional Commands

- **Delete a Topic**:
  ```bash
  gcloud pubsub topics delete <topic-name>
  ```

- **Delete a Subscription**:
  ```bash
  gcloud pubsub subscriptions delete <subscription-name>
  ```

- **List Subscriptions for a Topic**:
  ```bash
  gcloud pubsub topics list-subscriptions <topic-name>
  ```

---

## Cloud Build

### Submit a Build

```bash
gcloud builds submit --tag gcr.io/<project-id>/<image-name>
```

### List Builds

```bash
gcloud builds list
```

### View Build Logs

```bash
gcloud builds log <build-id>
```

### Cancel a Build

```bash
gcloud builds cancel <build-id>
```

#### Additional Commands

- **Describe a Build**:
  ```bash
  gcloud builds describe <build-id>
  ```

- **Retry a Build**:
  ```bash
  gcloud builds retry <build-id>
  ```

---

## Cloud DNS

### Create a Managed Zone

```bash
gcloud dns managed-zones create <zone-name> --dns-name <dns-name> --description "<description>"
```

### List Managed Zones

```bash
gcloud dns managed-zones list
```

### Add a DNS Record

```bash
gcloud dns record-sets transaction start --zone <zone-name>
gcloud dns record-sets transaction add <ip-address> --name <record-name> --ttl 300 --type A --zone <zone-name>
gcloud dns record-sets transaction execute --zone <zone-name>
```

### List DNS Records

```bash
gcloud dns record-sets list --zone <zone-name>
```

#### Additional Commands

- **Delete a DNS Record**:
  ```bash
  gcloud dns record-sets transaction start --zone <zone-name>
  gcloud dns record-sets transaction remove <ip-address> --name <record-name> --ttl 300 --type A --zone <zone-name>
  gcloud dns record-sets transaction execute --zone <zone-name>
  ```

- **Describe a Managed Zone**:
  ```bash
  gcloud dns managed-zones describe <zone-name>
  ```

---

## Cloud IAM Service Accounts

### Create a Service Account

```bash
gcloud iam service-accounts create <service-account-name> --display-name "<display-name>"
```

### List Service Accounts

```bash
gcloud iam service-accounts list
```

### Create a Service Account Key

```bash
gcloud iam service-accounts keys create <key-file> --iam-account <service-account-email>
```

### Add IAM Policy Binding to a Service Account

```bash
gcloud projects add-iam-policy-binding <project-id> \
  --member serviceAccount:<service-account-email> \
  --role <role>
```

#### Additional Commands

- **Delete a Service Account**:
  ```bash
  gcloud iam service-accounts delete <service-account-email>
  ```

- **List Service Account Keys**:
  ```bash
  gcloud iam service-accounts keys list --iam-account <service-account-email>
  ```

- **Disable a Service Account**:
  ```bash
  gcloud iam service-accounts disable <service-account-email>
  ```

---

## Cloud Key Management Service (KMS)

### Create a Key Ring

```bash
gcloud kms keyrings create <keyring-name> --location <location>
```

### Create a CryptoKey

```bash
gcloud kms keys create <key-name> --keyring <keyring-name> --location <location> --purpose encryption
```

### Encrypt a File

```bash
gcloud kms encrypt --key <key-name> --keyring <keyring-name> --location <location> --plaintext-file <input-file> --ciphertext-file <output-file>
```

### Decrypt a File

```bash
gcloud kms decrypt --key <key-name> --keyring <keyring-name> --location <location> --ciphertext-file <input-file> --plaintext-file <output-file>
```

#### Additional Commands

- **List Key Rings**:
  ```bash
  gcloud kms keyrings list --location <location>
  ```

- **List CryptoKeys**:
  ```bash
  gcloud kms keys list --keyring <keyring-name> --location <location>
  ```

- **Rotate a CryptoKey**:
  ```bash
  gcloud kms keys versions create --key <key-name> --keyring <keyring-name> --location <location> --primary
  ```

---

## Cloud Spanner *(New Section)*

### Create a Spanner Instance

```bash
gcloud spanner instances create <instance-name> --config <config> --description "<description>" --nodes <node-count>
```

### List Spanner Instances

```bash
gcloud spanner instances list
```

### Create a Database

```bash
gcloud spanner databases create <database-name> --instance <instance-name>
```

### Execute a SQL Query

```bash
gcloud spanner databases execute-sql <database-name> --instance <instance-name> --sql "SELECT * FROM <table-name>"
```

#### Additional Commands

- **Delete a Database**:
  ```bash
  gcloud spanner databases delete <database-name> --instance <instance-name>
  ```

- **List Databases**:
  ```bash
  gcloud spanner databases list --instance <instance-name>
  ```

---

## Cloud Dataflow *(New Section)*

### Run a Dataflow Job

```bash
gcloud dataflow jobs run <job-name> --gcs-location <template-location> --region <region>
```

### List Dataflow Jobs

```bash
gcloud dataflow jobs list --region <region>
```

### Describe a Dataflow Job

```bash
gcloud dataflow jobs describe <job-id> --region <region>
```

### Cancel a Dataflow Job

```bash
gcloud dataflow jobs cancel <job-id> --region <region>
```

---

## Cloud Composer *(New Section)*

### Create a Composer Environment

```bash
gcloud composer environments create <environment-name> --location <location> --zone <zone>
```

### List Composer Environments

```bash
gcloud composer environments list --locations <location>
```

### Describe a Composer Environment

```bash
gcloud composer environments describe <environment-name> --location <location>
```

### Delete a Composer Environment

```bash
gcloud composer environments delete <environment-name> --location <location>
```

---

## Scripting and Automation

### Run a Script with `gcloud`

```bash
#!/bin/bash
gcloud config set project <project-id>
gcloud compute instances create <instance-name> --zone <zone> --machine-type <machine-type>
```

### Export Configuration to a File

```bash
gcloud config configurations export <config-name> --destination <file-path>
```

### Import Configuration from a File

```bash
gcloud config configurations import <config-name> --source <file-path>
```

### Use `gcloud` in CI/CD Pipelines

```bash
# Example: Deploy to Cloud Run in a CI/CD pipeline
gcloud builds submit --tag gcr.io/<project-id>/<image-name>
gcloud run deploy <service-name> --image gcr.io/<project-id>/<image-name> --platform managed --region <region>
```

#### Additional Commands

- **Set Environment Variables for Scripts**:
  ```bash
  export PROJECT_ID=$(gcloud config get-value project)
  export ZONE=$(gcloud config get-value compute/zone)
  ```

- **Use `gcloud` with Service Account Keys**:
  ```bash
  gcloud auth activate-service-account --key-file <key-file>
  ```
