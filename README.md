# docker-php-mysql

## Update Services
1. To create your service. Use:
> git submodule add <remote_url> <destination_folder>

## After clone this repository.
1. Update `docker-compose.yml` to your preferences includes:
```
 volumes: to your actual repository in service
 extra_hosts, hostname, domainname to your preferences
 port default is 8888 but please update to your preference
```
2. Update your `hosts` file with:
```
127.0.0.1       local.example.com # change to your preference
```
3. In `containers/mysql/initdb`:
Update `init.sql` to your database schema create
To use multi scripts for multi database, update `containers/mysql/Dockerfile` file with more lines:
```
COPY ./containers/mysql/initdb/your_another_script.sql /docker-entrypoint-initdb.d/your_another_script.sql
```
4. Run:
> docker-compose up --build -d
5. To ssh to a container, use:
> docker exec -it $CONTAINER_NAME /bin/bash

## Troubleshooting
1. If you can't access your website, please check `port` in `docker-compose.yml` and see if your browser is using correct port (default config is `8888` that means your local domain should be: https://local.example.com:8888)
2. If you are using linux or macOS computer and counter this error message while buidling:
> failed to solve with frontend dockerfile.v0: failed to create LLB definition: no match for platform in manifest...
Insert `platform: linux/amd64` to `docker-compose.yml` under each services. eg:
```
php-environment:
        container_name: php8
        platform: linux/amd64 # this part
        build: .
```
3. If you build `db` with multi databases and it not running init all of your scripts. Remove everything inside `containers/general-mysql/db_data/` and drop the container. Then build again.