FROM resin/armv7hf-debian-qemu

RUN [ "cross-build-start" ]

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		bzip2 \
		ca-certificates \
		libffi-dev \
		libgdbm3 \
		libssl-dev \
		libyaml-dev \
		procps \
		zlib1g-dev \
	&& rm -rf /var/lib/apt/lists/*

# skip installing gem documentation
RUN mkdir -p /usr/local/etc \
	&& { \
		echo 'install: --no-document'; \
		echo 'update: --no-document'; \
	} >> /usr/local/etc/gemrc

ENV RUBY_BUILD_DEPS "autoconf bison  dpkg-dev gcc libbz2-dev libgdbm-dev libglib2.0-dev libncurses-dev libreadline-dev libxml2-dev libxslt-dev make ruby wget xz-utils"

RUN set -ex \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $RUBY_BUILD_DEPS \
	&& rm -rf /var/lib/apt/lists/*

RUN [ "cross-build-end" ]
ENTRYPOINT [ "/usr/bin/qemu-arm-static", "/usr/bin/env", "QEMU_EXECVE=1" ]
