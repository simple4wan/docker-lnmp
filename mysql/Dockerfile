FROM mysql:5
ENV MYSQL_ROOT_PASSWORD root

EXPOSE 3306

COPY custom.mysql.cnf /etc/mysql/mysql.conf.d/custom.mysql.cnf

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime