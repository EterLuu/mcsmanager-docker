FROM node:14.17

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production
ENV PUID 25565
ENV PGID 25565

WORKDIR /opt/mcsmanager

RUN wget -nv https://gitee.com/mcsmanager/MCSManager/releases/download/release/mcsmanager_linux_release.tar.gz \
	&& tar -zxf mcsmanager_linux_release.tar.gz -o \
	&& rm mcsmanager_linux_release.tar.gz \
	&& groupadd -g ${PGID} minecraft \
	&& useradd -g ${PGID} -u ${PUID} minecraft \
	&& chown -R minecraft:minecraft daemon \
	&& chown -R minecraft:minecraft web

WORKDIR /opt/mcsmanager/web

RUN npm install --registry=https://registry.npmmirror.com --production

USER minecraft

CMD ["node", "app.js"]
