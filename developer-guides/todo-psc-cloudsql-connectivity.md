To set up the gcloud CLI, follow the steps in Install the gcloud CLI.

# Cloud SQL Connectivity Guide

This guide provides instructions for connecting to Cloud SQL instances using the Cloud SQL Auth Proxy. The proxy provides secure access to your Cloud SQL instances without requiring authorized networks or SSL certificates.

## Prerequisites

To set up the gcloud CLI, follow the steps in [Install the gcloud CLI](https://cloud.google.com/sdk/docs/install).


### Installing the Cloud SQL Auth Proxy
Install the Cloud SQL Auth Proxy by following the [official Google Cloud documentation](https://cloud.google.com/sql/docs/mysql/connect-auth-proxy#install).

### Installing the Database Client

#### PostgreSQL Client

##### MacOS

```bash
brew install libpq
```

After installation, add the PostgreSQL binaries to your PATH:

```bash
echo 'export PATH="/opt/homebrew/opt/libpq/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

##### Ubuntu

```bash
sudo apt update -y
sudo apt install -y postgresql-client
```

#### MySQL Client

##### MacOS

```bash
brew install mysql-client
```

After installation, add the MySQL binaries to your PATH:

```bash
echo 'export PATH="/opt/homebrew/opt/mysql-client/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

##### Ubuntu

```bash
sudo apt update
sudo apt install -y default-mysql-client
```

## Connecting to the Database

### Starting the Cloud SQL Auth Proxy

1. Login to Google Cloud:
```bash
gcloud auth login
```
```bash
gcloud auth application-default login
```

2. Get your instance connection name:
```bash
gcloud sql instances describe INSTANCE_NAME --format='value(connectionName)'
```

For more information, see the [official documentation](https://cloud.google.com/sql/docs/mysql/connect-admin-proxy).

3. # ssh into a vm
gcloud compute ssh vm-ace-dev-bastion-host \
--project=nm-ace-dev-9320 \
--zone=us-central1-a \
--tunnel-through-iap

# install cloud sql proxy
```bash
curl -o cloud-sql-proxy https://storage.googleapis.com/cloud-sql-connectors/cloud-sql-proxy/v2.18.0/cloud-sql-proxy.linux.amd64
```
# Permission the cloud proxy
```bash
chmod +x cloud-sql-proxy
```

# start the cloud proxy
```bash
./cloud-sql-proxy --port 3306 --private-ip nm-ace-dev-9320:us-central1:sql-ace-dev-comic-cattle
```

# establishes the SSH connection to the VM
gcloud compute ssh vm-ace-dev-bastion-host \
--project=nm-ace-dev-9320 \
--zone=us-central1-a \
-- -L 3306:localhost:3306 \
"/home/davidshrader/cloud-sql-proxy --port 3306 --private-ip nm-ace-dev-9320:us-central1:sql-ace-dev-comic-cattle"


gcloud compute ssh vm-ace-dev-bastion-host \
-- -L 3306:localhost:3306 \
"/home/davidshrader/cloud-sql-proxy --port 3306 --private-ip nm-ace-dev-9320:us-central1:sql-ace-dev-comic-cattle"



mysql --host=127.0.0.1 --port=3306 --user=nativemsg --password









## Additional Options

- To specify a different port:
```
./cloud-sql-proxy --port PORT_NUMBER INSTANCE_CONNECTION_NAME
```

- To connect to multiple instances:
```
./cloud-sql-proxy INSTANCE_CONNECTION_NAME_1 INSTANCE_CONNECTION_NAME_2
```


### PostgreSQL Connection Example

```bash
psql --host=127.0.0.1 --port=8888 --username=YOUR_DB_USER --password
```

### MySQL Connection Example

```bash
mysql --host=127.0.0.1 --port=8888 --user=YOUR_DB_USER --password
```

netstat -anp | grep 3306
kX2R(MlU<-p{=BDi
kX2R(MlU<-p{=BDi

~$ ./cloud-sql-proxy --auto-iam-authn bcg-demo-prj-d2a7:us-central1:test-sql-psca0  --psc &
[1] 3879
aman_wolde_greenstdigital_com@connectivity-test-vm1-psc-ai:~$ 2025/06/19 15:45:11 Authorizing with Application Default Credentials
2025/06/19 15:45:12 [bcg-demo-prj-d2a7:us-central1:test-sql-psca0] Listening on 127.0.0.1:5432
2025/06/19 15:45:12 The proxy has started successfully and is ready for new connections!
