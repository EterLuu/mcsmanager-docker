FROM node:14.17.6

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production
ENV PUID=25565
ENV PGID=25565
ENV PUSERNAME="minecraft"
ENV PGROUPNAME="minecraft"

RUN apt-get install libstdc++6

RUN groupadd --non-unique -g ${PGID} {PGROUPNAME} \
	&& useradd --non-unique -g ${PGID} -u ${PUID} {PUSERNAME} \

WORKDIR /usr/lib/jvm

RUN ARCH='linux*' && dpkgArch="$(dpkg --print-architecture)" \
		&& case "${dpkgArch##*-}" in \
			amd64) ARCH='x64';; \
			arm64) ARCH='aarch64';; \
			*) ;; \
		esac \
	&& JDK17="zulu17.46.19-ca-jdk17.0.9-linux_${ARCH}" \
 	&& JDK8="zulu8.74.0.17-ca-jdk8.0.392-linux_${ARCH}" \
	&& wget -nv https://cdn.azul.com/zulu/bin/${JDK17}.tar.gz \
	&& wget -nv https://cdn.azul.com/zulu/bin/${JDK8}.tar.gz \
	&& tar -zxf ${JDK17}.tar.gz -o \
	&& tar -zxf ${JDK8}.tar.gz -o \
	&& rm ${JDK17}.tar.gz \
	&& rm ${JDK8}.tar.gz \
	&& mv ${JDK17} java17 \
	&& mv ${JDK8} java8 \
	&& ln -s /usr/lib/jvm/java17/bin/java /usr/bin/java \
	&& ln -s /usr/lib/jvm/java8/bin/java /usr/bin/java8

WORKDIR /opt/mcsmanager

RUN wget -nv https://gitee.com/mcsmanager/MCSManager/releases/download/release/mcsmanager_linux_release.tar.gz \
	&& tar -zxf mcsmanager_linux_release.tar.gz -o \
	&& rm mcsmanager_linux_release.tar.gz \
	&& chown -R ${PUID}:${PGID} daemon \
	&& chown -R ${PUID}:${PGID} web

WORKDIR /opt/mcsmanager/daemon

RUN npm install --registry=https://registry.npmmirror.com --production

USER ${PUID}

CMD ["node", "app.js"]
