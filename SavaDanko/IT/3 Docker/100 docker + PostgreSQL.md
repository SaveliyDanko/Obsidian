**1. Скачиваем образ PostgreSQL из [DockerHub](https://hub.docker.com/_/postgres)**
```bash
docker pull postgres:17.4
```

**2 Запускаем Container из Docker Image**
```bash
docker run --rm --name my-postgres \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_DB=savadankoDB \
  -p 5432:5432 \
  -d postgres
```

**3 Получение доступа к контейнеру:**
```bash
docker exec --interactive --tty my-postgres bash
```

###### `POSTGRES_PASSWORD`
This environment variable is required for you to use the PostgreSQL image. It must not be empty or undefined. This environment variable sets the superuser password for PostgreSQL. The default superuser is defined by the `POSTGRES_USER` environment variable.

**Note 1:** The PostgreSQL image sets up `trust` authentication locally so you may notice a password is not required when connecting from `localhost` (inside the same container). However, a password will be required if connecting from a different host/container.

**Note 2:** This variable defines the superuser password in the PostgreSQL instance, as set by the `initdb` script during initial container startup. It has no effect on the `PGPASSWORD` environment variable that may be used by the `psql` client at runtime, as described at [https://www.postgresql.org/docs/14/libpq-envars.html⁠](https://www.postgresql.org/docs/14/libpq-envars.html). `PGPASSWORD`, if used, will be specified as a separate environment variable.
###### `POSTGRES_USER`
This optional environment variable is used in conjunction with `POSTGRES_PASSWORD` to set a user and its password. This variable will create the specified user with superuser power and a database with the same name. If it is not specified, then the default user of `postgres` will be used.

Be aware that if this parameter is specified, PostgreSQL will still show `The files belonging to this database system will be owned by user "postgres"` during initialization. This refers to the Linux system user (from `/etc/passwd` in the image) that the `postgres` daemon runs as, and as such is unrelated to the `POSTGRES_USER` option. See the section titled "Arbitrary `--user` Notes" for more details.

###### `POSTGRES_DB`
This optional environment variable can be used to define a different name for the default database that is created when the image is first started. If it is not specified, then the value of `POSTGRES_USER` will be used.