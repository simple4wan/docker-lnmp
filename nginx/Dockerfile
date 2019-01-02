FROM nginx:alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk add --update-cache --no-cache tzdata nginx-mod-http-fancyindex \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime