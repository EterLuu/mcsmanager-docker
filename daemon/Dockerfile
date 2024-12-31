FROM node:16.20.2

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV LANG en_US.UTF-8
ENV NODE_ENV=production

RUN apt-get install libstdc++6

WORKDIR /usr/lib/jvm

RUN ARCH='linux*' && dpkgArch="$(dpkg --print-architecture)" \
		&& case "${dpkgArch##*-}" in \
			amd64) ARCH='x64';; \
			arm64) ARCH='aarch64';; \
			*) ;; \
		esac \
  	&& JDK21="zulu21.38.21-ca-jdk21.0.5-linux_${ARCH}" \
	&& JDK17="zulu17.54.21-ca-jdk17.0.13-linux_${ARCH}" \
 	&& JDK8="zulu8.82.0.21-ca-jdk8.0.432-linux_${ARCH}" \
	&& wget -nv https://cdn.azul.com/zulu/bin/${JDK21}.tar.gz \
	&& wget -nv https://cdn.azul.com/zulu/bin/${JDK17}.tar.gz \
	&& wget -nv https://cdn.azul.com/zulu/bin/${JDK8}.tar.gz \
	&& tar -zxf ${JDK21}.tar.gz -o \
	&& tar -zxf ${JDK17}.tar.gz -o \
	&& tar -zxf ${JDK8}.tar.gz -o \
	&& rm ${JDK21}.tar.gz \
	&& rm ${JDK17}.tar.gz \
	&& rm ${JDK8}.tar.gz \
	&& mv ${JDK21} java21 \
	&& mv ${JDK17} java17 \
	&& mv ${JDK8} java8 \
	&& ln -s /usr/lib/jvm/java21/bin/java /usr/bin/java \
	&& ln -s /usr/lib/jvm/java17/bin/java /usr/bin/java17 \
	&& ln -s /usr/lib/jvm/java8/bin/java /usr/bin/java8

WORKDIR /opt/mcsmanager

RUN wget -nv https://mcsmanager.oss-cn-guangzhou.aliyuncs.com/mcsmanager_linux_release.tar.gz \
	&& tar -zxf mcsmanager_linux_release.tar.gz -o \
	&& rm mcsmanager_linux_release.tar.gz

WORKDIR /opt/mcsmanager/daemon

RUN npm install --registry=https://registry.npmmirror.com --production --no-fund --no-audit

CMD ["node", "app.js"]
