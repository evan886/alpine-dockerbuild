FROM alpine:3.14
MAINTAINER evan <evan886@gmail.com>

WORKDIR /app
VOLUME /app

RUN echo "#aliyun" > /etc/apk/repositories
RUN echo "https://mirrors.aliyun.com/alpine/v3.14/main/" >> /etc/apk/repositories
RUN echo "https://mirrors.aliyun.com/alpine/v3.14/community/" >> /etc/apk/repositories

RUN apk add tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone

RUN apk add --update   xz  mysql mysql-client && rm -f /var/cache/apk/*  
#RUN apk add --update bash  xz  mysql mysql-client && rm -f /var/cache/apk/*  

# These lines moved to the end allow us to rebuild image quickly after only these files were modified.
COPY startup.sh /startup.sh
COPY my.cnf /etc/mysql/my.cnf
COPY  mariadb-server.cnf /etc/my.cnf.d/mariadb-server.cnf
EXPOSE 3306
CMD ["/startup.sh"]

#  mariadb (10.5.12-r0)
