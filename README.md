# Zerops x EdgeDB

```yaml
#yamlPreprocessor=on
project:
  name: zerops-edgedb
  
services:
  - hostname: edgedb
    type: ubuntu@22.04
    buildFromGit: https://github.com/zeropsio/zerops-edgedb
    enableSubdomainAccess: true
    ports:
      - port: 5656
        httpSupport: true
    verticalAutoscaling:
      minRam: 0.5
    envSecrets:
      EDGEDB_SERVER_BACKEND_DSN: ${db_connectionString}/db
      EDGEDB_SERVER_BINARY_ENDPOINT_SECURITY: optional
      EDGEDB_SERVER_RUNSTATE_DIR: /home/edgedb/edgedb_runstate
      EDGEDB_SERVER_ADMIN_UI: enabled
      EDGEDB_SERVER_PASSWORD: <@generateRandomString(<12>)>
      EDGEDB_SERVER_TLS_CERT_FILE: /etc/zerops-zembed/cert.crt
      EDGEDB_SERVER_TLS_KEY_FILE: /etc/zerops-zembed/cert.key
      EDGEDB_SERVER_BIND_ADDRESS: 0.0.0.0
      EDGEDB_CLIENT_TLS_SECURITY: insecure
      EDGEDB_SERVER_HTTP_ENDPOINT_SECURITY: optional
      EDGEDB_SERVER_INSTANCE_NAME: ${hostname}
      EDGEDB_SERVER_BOOTSTRAP_COMMAND: "ALTER ROLE edgedb { SET password := '${EDGEDB_SERVER_PASSWORD}'; }"

  - hostname: db
    type: postgresql@16
    mode: HA
    priority: 10
```
