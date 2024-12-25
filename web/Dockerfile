FROM node:16.20.2

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production

WORKDIR /opt/mcsmanager

RUN wget -nv https://mcsmanager.oss-cn-guangzhou.aliyuncs.com/mcsmanager_linux_release.tar.gz \
	&& tar -zxf mcsmanager_linux_release.tar.gz -o \
	&& rm mcsmanager_linux_release.tar.gz

WORKDIR /opt/mcsmanager/web

RUN npm install --registry=https://registry.npmmirror.com --production --no-fund --no-audit

CMD ["node", "app.js"]
