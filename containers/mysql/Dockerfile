FROM mysql

# run first
COPY ./containers/mysql/initdb/init.sql /docker-entrypoint-initdb.d/init.sql

RUN chmod -R 775 /docker-entrypoint-initdb.d

ENV MYSQL_ROOT_PASSWORD g9BgLNdF
