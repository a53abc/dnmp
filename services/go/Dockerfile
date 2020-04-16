ARG GO_VERSION
FROM golang:${GO_VERSION}

ARG TZ
ARG CONTAINER_PACKAGE_URL

#RUN sed -i "s/dl-cdn.alpinelinux.org/${CONTAINER_PACKAGE_URL}/g" /etc/apk/repositories

RUN echo 'deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster main contrib non-free\n\
	deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-updates main contrib non-free\n\
	deb https://mirrors.tuna.tsinghua.edu.cn/debian/ buster-backports main contrib non-free\n\
	deb https://mirrors.tuna.tsinghua.edu.cn/debian-security buster/updates main contrib non-free\n'\
	 > /etc/apt/sources.list \
&&apt-get clean && apt-get update \
&& apt-get install -y zip wget

RUN cp "/usr/share/zoneinfo/$TZ" /etc/localtime \
    && echo "$TZ" > /etc/timezone

RUN mkdir -p /tmp/data /tmp/config /opt
COPY --from=consul:1.6.1 /bin/consul /bin/consul
COPY --from=thrift:0.10.0 /usr/local/bin/thrift /usr/local/bin/thrift