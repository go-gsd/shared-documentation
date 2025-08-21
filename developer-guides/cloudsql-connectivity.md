# Cloud SQL Connectivity Guide

This guide provides instructions for connecting to Cloud SQL instances using the Cloud SQL Auth Proxy. The proxy provides secure access to your Cloud SQL instances without requiring authorized networks or SSL certificates.

## Prerequisites

This guide assumes the following infrastructure is already in place:

### Infrastructure Requirements
- **Bastion Host**: A Google Compute Engine VM instance configured as a bastion host must be deployed and accessible
- **Identity-Aware Proxy (IAP)**: IAP must be configured and enabled for secure access to your bastion host
- **Cloud SQL Instance**: Your Cloud SQL instance should be created and configured with private IP networking

### Alternative Approaches
While this guide demonstrates connectivity through a bastion host, you can alternatively use:
- **GKE Cluster**: Deploy the Cloud SQL Proxy as a sidecar container in a Google Kubernetes Engine cluster

**Note**: This example focuses specifically on the bastion host approach for secure, controlled access to Cloud SQL instances.

### Required Software Installation

#### Google Cloud CLI
**IMPORTANT**: You must have gcloud installed and configured before proceeding to step 1, as the environment variable setup requires gcloud commands.

For gcloud CLI installation, authentication, and configuration, follow the comprehensive guide: [Google Cloud CLI Configuration](gcloud-configuration.md).

## Setup

### 1. Environment Variables
First, set up your environment variables. These will be used throughout the connection process:

```bash
# Bastion host VM name
export BASTION_HOST="your-bastion-host"

# Cloud SQL instance name
export INSTANCE_NAME="your-instance-name"

# Cloud SQL connection name (derived from INSTANCE_NAME)
export CONN_NAME=$(gcloud sql instances describe $INSTANCE_NAME --format='value(connectionName)')
```

### 2. Database Client Installation
Install the appropriate database client on your local machine:

**PostgreSQL Client:**
```bash
# MacOS
brew install libpq

# Ubuntu
sudo apt install -y postgresql-client
```

**MySQL Client:**
```bash
# MacOS
brew install mysql-client

# Ubuntu
sudo apt install -y default-mysql-client
```

### 3. Cloud SQL Proxy Installation
SSH into your bastion host and install the Cloud SQL Proxy:

```bash
# Connect to bastion host
gcloud compute ssh $BASTION_HOST --tunnel-through-iap
```

Once connected to the bastion host, run these commands:

```bash
# Download Cloud SQL Auth Proxy
curl -o cloud-sql-proxy https://storage.googleapis.com/cloud-sql-connectors/cloud-sql-proxy/v2.18.0/cloud-sql-proxy.linux.amd64

# Make the Cloud SQL Proxy executable
chmod +x cloud-sql-proxy
```

## Connecting to the Database

### 4. Establish an SSH Tunnel
From your local machine, create an SSH tunnel with port forwarding to connect through the bastion host:

```bash
# Database port (3306 for MySQL, 5432 for PostgreSQL)
gcloud compute ssh $BASTION_HOST \
  -- -L 3306:localhost:3306 \
  "~/cloud-sql-proxy --port 3306 --private-ip $CONN_NAME"
```

This command:
- Creates an SSH tunnel to your bastion host
- Forwards the database port from the bastion host to your local machine
- Starts the Cloud SQL Proxy on the bastion host

### 5. Connect to the Database
Once the tunnel is established, connect to your database from **another terminal**.

Set the following environment variable:

```bash
# Database username
export YOUR_DB_USER="your-database-username"
```

#### MySQL Connection
```bash
mysql --host=127.0.0.1 --port=3306 --user=$YOUR_DB_USER --password
```

#### PostgreSQL Connection
```bash
psql --host=127.0.0.1 --port=5432 --username=$YOUR_DB_USER --password
```

## Additional Resources

### Identity-Aware Proxy (IAP)
- [Concepts overview](https://cloud.google.com/iap/docs/concepts-overview)
- [Using IAP for TCP forwarding](https://cloud.google.com/iap/docs/using-tcp-forwarding)

### Cloud SQL Private IP
- [Configure Private IP](https://cloud.google.com/sql/docs/mysql/configure-private-ip)
- [Connectivity overview (Private IP)](https://cloud.google.com/sql/docs/mysql/connect-overview#private-ip)

### Bastion Host on Google Cloud
- [Set up a bastion host](https://cloud.google.com/compute/docs/instances/connecting-advanced#bastion)
- [Best practices for bastion hosts](https://cloud.google.com/architecture/best-practices-for-using-a-bastion-host)