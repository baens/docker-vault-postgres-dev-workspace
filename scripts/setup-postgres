#!/bin/sh

echo "Setting up postgres hba settings"
cat <<EOM > ${PGDATA}/pg_hba.conf
local     all  all       trust
hostnossl all  all  all  reject
hostssl   all  all  all  password
EOM

echo "Adding SSL settings to postgresql.conf file"
cat <<EOM >> ${PGDATA}/postgresql.conf
ssl = on
ssl_cert_file = '/var/ssl/server-cert.pem'
ssl_key_file = '/var/ssl/server-key.pem'
ssl_ca_file = '/var/ssl/ca.pem'
EOM
