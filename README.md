# A starting workspace for Vault, Postgres, and Docker

This workspace is tied to a blog post that demonstrates a decent starting point of a postgres and vault development workspace.

# How to use

`./scripts/setup-ssl` is required before you start anything. Postgres is configured with SSL so you will need these files first.

`docker-compose up` will start Postgres and Vault and initalize them

# How to connect to Postgres

If you want to drop straight in to the Postgres instance you can execute `docker-compose exec database psql -U admin -d mydb`

# How to get a Username and password from vault

`docker-compose exec vault vault read dbs/creds/mydb-admin`

If you want to get a Vault username, then login directly with that:

```
VAULT_SETTINGS=$(docker-compose exec vault vault read --format=json dbs/creds/mydb-admin)
VAULT_USERNAME=$(echo $VAULT_SETTINGS | docker run --rm -i colstrom/jq -r '.data.username')
docker-compose exec database psql -U $VAULT_USERNAME -d mydb
```
