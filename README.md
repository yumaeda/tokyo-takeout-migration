# tokyo-takeout-migration
## Preparation
```sh
brew install golang-migrate
```

&nbsp;

## Create migration files
```sh
migrate create -ext sql -dir db/migration -seq <Migration Name>
```

&nbsp;

## Launch MariaDB server inside a Docker container
```sh
docker run --name tokyo_takeout_db -e MYSQL_ROOT_PASSWORD=mypass -p 3306:3306 -d docker.io/library/mariadb:10.6.1
```

&nbsp;

## Connect to MariaDB inside the container
```sh
mysql -h 0.0.0.0 -P 3306 -u root -p
```

## Create `tokyo_takeout` database
```sh
CREATE DATABASE tokyo_takeout;
```

## Run migration
```sh
migrate -path db/migration -verbose -database 'mysql://root:mypass@tcp(0.0.0.0:3306)/tokyo_takeout' up
```

- `schema_migrations` table stores the migration version and the status of the last migration.