FROM node:14.17.6-alpine

ARG TZ="Asia/Shanghai"
ARG PUID=25565
ARG PGID=25565

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production
ENV PUID ${PUID}
ENV PGID ${PGID}

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
	&& apk add ttf-dejavu fontconfig libstdc++ eudev-libs gcompat

WORKDIR /usr/lib/jvm

RUN ARCH='linux*' && alpineArch="$(apk --print-arch)" \
		&& case "${alpineArch##*-}" in \
			x86_64) ARCH='x64';; \
			aarch64) ARCH='aarch64';; \
			*) ;; \
		esac \
	&& JDK17="zulu17.46.19-ca-jdk17.0.9-linux_musl_${ARCH}" \
 	&& JDK8="zulu8.74.0.17-ca-jdk8.0.392-linux_musl_${ARCH}" \
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
