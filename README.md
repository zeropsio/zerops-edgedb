# Zerops x EdgeDB

```yaml
project:
  name: edgedb-test
  
services:
  - hostname: edgedb
    type: ubuntu@22.04
    envSecrets:
      EDGEDB_SERVER_BACKEND_DSN: ${db_connectionString}/db
      EDGEDB_SERVER_BINARY_ENDPOINT_SECURITY: optional
      EDGEDB_SERVER_RUNSTATE_DIR: /home/edgedb_user/edgedb_runstate
      EDGEDB_SERVER_TLS_CERT_MODE: generate_self_signed
    ports:
      - port: 5656
      - 
  - hostname: db
    type: postgresql@16
    mode: HA
```
