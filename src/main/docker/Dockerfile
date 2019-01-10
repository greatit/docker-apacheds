FROM openjdk:7-jre-alpine
MAINTAINER David Lakatos <david.lakatos@great-it.com>

EXPOSE 10389
EXPOSE 10636

ARG DS_VERSION=2.0.0-M25
ARG DS_FILENAME=apacheds-2.0.0.AM25.tar.gz
ARG DS_URL=http://xenia.sote.hu/ftp/mirrors/www.apache.org//directory/apacheds/dist/2.0.0.AM25/apacheds-2.0.0.AM25.tar.gz
ARG DS_SHA256=32c9893aa06b293b49b82f89d2f5b92f297e24d3331fd7b196c70dcb07d419df

WORKDIR /tmp

# download compressed artifact
ADD ${DS_URL} /tmp

# verify file integrity
RUN echo -n "${DS_SHA256} *${DS_FILENAME}" > ${DS_FILENAME}.sha256
RUN sha256sum -c  ${DS_FILENAME}.sha256

# uncompress tarball
RUN tar -xvzf apacheds-2.0.0.AM25.tar.gz -C /usr/local

# create symlink for easier use
RUN ln -s /usr/local/apacheds* /usr/local/apacheds

# Bash is required by the ApacheDS start script
RUN apk add "bash=4.4.19-r1"

CMD /usr/local/apacheds/bin/apacheds.sh run