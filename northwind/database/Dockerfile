FROM mysql@sha256:bf17a7109057494c45fba5aab7fc805ca00ac1eef638dfdd42b38d5a7190c9bb

ENV MYSQL_ROOT_PASSWORD=changeit MYSQL_DATABASE=northwind 

ADD 0-northwind-default-current-timestamp.sql /docker-entrypoint-initdb.d
ADD 1-northwind-data.sql /docker-entrypoint-initdb.d

# get mysql image
FROM mysql:5.7

ENV MYSQL_ROOT_PASSWORD=changeit MYSQL_PORT=3306 MYSQL_DB_PATH=/var/lib/mysql

# copy the SQL files to 
ADD 0-northwind-default-current-timestamp.sql /docker-entrypoint-initdb.d 
ADD 1-northwind-data.sql /docker-entrypoint-initdb.d 

# add healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
        CMD mysqladmin ping -uroot -p{MYSQL_ROOT_PASSWORD} || exit

# expose port
EXPOSE ${MYSQL_PORT}

# volume
VOLUME ${MYSQL_DB_PATH}

EXPOSE 3306
VOLUME /var/lib/mysql

