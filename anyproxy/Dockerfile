FROM node:alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk add --update-cache --no-cache tzdata \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && npm install --global --production anyproxy \
    && anyproxy-ca -g

EXPOSE 8001
EXPOSE 8002

CMD ["anyproxy", "--intercept"]