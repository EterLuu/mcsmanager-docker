FROM node:14.17

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production

WORKDIR /opt/mcsmanager

RUN wget -nv https://gitee.com/mcsmanager/MCSManager/releases/download/release/mcsmanager_linux_release.tar.gz \
	&& tar -zxf mcsmanager_linux_release.tar.gz -o \
	&& rm mcsmanager_linux_release.tar.gz \
	&& groupadd -r minecraft \
	&& useradd -r -g minecraft minecraft \
	&& chown -R minecraft:minecraft daemon \
	&& chown -R minecraft:minecraft web

WORKDIR /opt/mcsmanager/web

RUN npm install --registry=https://registry.npmmirror.com --production

USER minecraft

CMD ["node", "app.js"]
