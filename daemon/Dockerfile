FROM node:14.17.6-alpine

ARG TZ="Asia/Shanghai"
ARG PUID=25565
ARG PGID=25565

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production
ENV PUID ${PUID}
ENV PGID ${PGID}

RUN apk add libstdc++

WORKDIR /usr/lib/jvm

RUN ARCH='linux*' && alpineArch="$(apk --print-arch)" \
		&& case "${alpineArch##*-}" in \
			x86_64) ARCH='x64';; \
			x86) ARCH='i686';; \
			aarch64) ARCH='aarch64';; \
			arm*) ARCH='aarch32hf';; \
			*) ;; \
		esac \
	&& wget -nv https://cdn.azul.com/zulu/bin/zulu17.46.19-ca-jdk17.0.9-linux_${ARCH}.tar.gz \
	&& wget -nv https://cdn.azul.com/zulu/bin/zulu8.74.0.17-ca-jdk8.0.392-linux_${ARCH}.tar.gz \
	&& tar -zxf zulu17.46.19-ca-jdk17.0.9-linux_${ARCH}.tar.gz -o \
	&& tar -zxf zulu8.74.0.17-ca-jdk8.0.392-linux_${ARCH}.tar.gz -o \
	&& rm zulu17.46.19-ca-jdk17.0.9-linux_${ARCH}.tar.gz \
	&& rm zulu8.74.0.17-ca-jdk8.0.392-linux_${ARCH}.tar.gz \
	&& mv zulu17.46.19-ca-jdk17.0.9-linux_${ARCH} java17 \
	&& mv zulu8.74.0.17-ca-jdk8.0.392-linux_${ARCH} java8 \
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
