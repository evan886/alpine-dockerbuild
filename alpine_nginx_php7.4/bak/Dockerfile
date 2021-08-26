FROM php:7.4-fpm-alpine3.14
#ADD repositories /etc/apk/repositories
RUN echo "#aliyun" > /etc/apk/repositories
RUN echo "https://mirrors.aliyun.com/alpine/v3.14/main/" >> /etc/apk/repositories
RUN echo "https://mirrors.aliyun.com/alpine/v3.14/community/" >> /etc/apk/repositories

RUN apk add tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone

RUN apk add --update bash  xz   mysql-client   
#RUN apk add --update bash  xz   mysql-client && rm -f /var/cache/apk/*  

ADD  nginx.conf   / 
ADD  default.conf    /

#ADD default.conf /
ADD index.html /
ADD run.sh /
RUN apk update && apk add nginx && \
    apk add m4 autoconf make gcc g++ linux-headers && \
    docker-php-ext-install pdo_mysql opcache mysqli && \
    mkdir -p  /run/nginx && \
    mkdir -p  /etc/nginx/conf.d/ && \
    mv /default.conf /etc/nginx/conf.d/ && \
    mv  /nginx.conf   /etc/nginx/nginx.conf && \ 
    mv /index.html /var/www/html/ && \
    touch /run/nginx/nginx.pid && \
    chmod 755 /run.sh && \
    apk del m4 autoconf make gcc g++ linux-headers


RUN rm -f /var/cache/apk/*  
EXPOSE 80
EXPOSE 9000

ENTRYPOINT ["/run.sh"]
