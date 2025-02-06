
Download the Cloud SQL Auth Proxy:
```
curl -o cloud-sql-proxy https://storage.googleapis.com/cloud-sql-connectors/cloud-sql-proxy/v2.14.3/cloud-sql-proxy.darwin.amd64
```

Make the Cloud SQL Auth Proxy executable:
```
chmod +x cloud-sql-proxy
```

```
gcloud sql instances describe INSTANCE_NAME
```

```
docker run -d \\
-v PATH_TO_KEY_FILE:/path/to/service-account-key.json \\
-p 127.0.0.1:3306:3306 \\
gcr.io/cloud-sql-connectors/cloud-sql-proxy:2.14.3 \\
--address 0.0.0.0 --port 3306 \\
--credentials-file /path/to/service-account-key.json INSTANCE_CONNECTION_NAME
```
