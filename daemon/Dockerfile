FROM node:14.17

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production
ENV PUID 25565
ENV PGID 25565

RUN apt-get install libstdc++6

WORKDIR /usr/lib/jvm

RUN wget -nv https://cdn.azul.com/zulu/bin/zulu17.42.21-ca-crac-jdk17.0.7-linux_x64.tar.gz \
	&& wget -nv https://cdn.azul.com/zulu/bin/zulu8.70.0.23-ca-jdk8.0.372-linux_x64.tar.gz \
	&& tar -zxf zulu17.42.21-ca-crac-jdk17.0.7-linux_x64.tar.gz -o \
	&& tar -zxf zulu8.70.0.23-ca-jdk8.0.372-linux_x64.tar.gz -o \
	&& rm zulu17.42.21-ca-crac-jdk17.0.7-linux_x64.tar.gz \
	&& rm zulu8.70.0.23-ca-jdk8.0.372-linux_x64.tar.gz \
	&& mv zulu17.42.21-ca-crac-jdk17.0.7-linux_x64 java17 \
	&& mv zulu8.70.0.23-ca-jdk8.0.372-linux_x64 java8 \
	&& ln -s /usr/lib/jvm/java17/bin/java /usr/bin/java \
	&& ln -s /usr/lib/jvm/java8/bin/java /usr/bin/java8

WORKDIR /opt/mcsmanager

RUN wget -nv https://gitee.com/mcsmanager/MCSManager/releases/download/release/mcsmanager_linux_release.tar.gz \
	&& tar -zxf mcsmanager_linux_release.tar.gz -o \
	&& rm mcsmanager_linux_release.tar.gz \
	&& groupadd -g ${PGID} minecraft \
	&& useradd -g ${PGID} -u ${PUID} minecraft \
	&& chown -R minecraft:minecraft daemon \
	&& chown -R minecraft:minecraft web

WORKDIR /opt/mcsmanager/daemon

RUN npm install --registry=https://registry.npmmirror.com --production

USER minecraft

CMD ["node", "app.js"]
