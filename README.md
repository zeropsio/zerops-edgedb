# Zerops x EdgeDB

```yaml
project:
  name: edgedb-test

service:
  - hostname: edgedb
    type: ubuntu@22
    ports:
      - port: 5656

  - hostname: db
    type: postgresql@16
    mode: HA
```
