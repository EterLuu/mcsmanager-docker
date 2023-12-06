FROM node:14.17.6-alpine

ARG TZ="Asia/Shanghai"
ARG PUID=25565
ARG PGID=25565

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production
ENV PUID ${PUID}
ENV PGID ${PGID}

WORKDIR /opt/mcsmanager

RUN wget -nv https://gitee.com/mcsmanager/MCSManager/releases/download/release/mcsmanager_linux_release.tar.gz \
	&& tar -zxf mcsmanager_linux_release.tar.gz -o \
	&& rm mcsmanager_linux_release.tar.gz \
	&& chown -R ${PUID}:${PGID} daemon \
	&& chown -R ${PUID}:${PGID} web

WORKDIR /opt/mcsmanager/web

RUN npm install --registry=https://registry.npmmirror.com --production

USER ${PUID}

CMD ["node", "app.js"]
