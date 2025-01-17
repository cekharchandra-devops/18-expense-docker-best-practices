FROM mysql:8.0
ENV MYSQL_ROOT_PASSWORD=ExpenseApp@1
RUN groupadd expense && \
    useradd -g expense expense && \
    # chown -R expense:expense /var/lib/mysql /var/run/mysqld /docker-entrypoint-initdb.d
    chown -R mysql:mysql /var/lib/mysql /var/run/mysqld /docker-entrypoint-initdb.d && \
    chmod 0750 /var/lib/mysql /var/run/mysqld /docker-entrypoint-initdb.d && \
    usermod -aG mysql expense
ADD script/*.sql /docker-entrypoint-initdb.d
USER expense

# FROM mysql:8.0.26
# ENV MYSQL_ROOT_PASSWORD=ExpenseApp@1
# COPY script/*.sql /docker-entrypoint-initdb.d/
