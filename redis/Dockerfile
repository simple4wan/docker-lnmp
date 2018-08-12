FROM redis:alpine

EXPOSE 6379

COPY redis.conf /usr/local/etc/redis/redis.conf

RUN apk add --update-cache --no-cache tzdata \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]