FROM golang:1.21-alpine
COPY ./build/migration/migrate.sh ./
RUN apk add --no-cache postgresql-client jq && \
apk add --no-cache git && \
CGO_ENABLED=0 go install github.com/rubenv/sql-migrate/...@latest && \
chmod +x migrate.sh
COPY ./build/migration/dbconfig.yml ./
COPY ./migrations ./migrations

ENV POSTGRESQL_HOST="172.18.0.2"
ENV POSTGRESQL_PORT=5432
ENV POSTGRESQL_USER="root"
# POSTGRES_DBPASSWORD="dz1hXCSgxg"
ENV POSTGRESQL_PASSWORD="secret"
ENV POSTGRESQL_DB="simple_bank"

ENTRYPOINT ["./migrate.sh"]
