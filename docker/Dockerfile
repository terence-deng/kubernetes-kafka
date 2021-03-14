FROM ubuntu:18.04
ENV KAFKA_USER=kafka \
KAFKA_DATA_DIR=/var/lib/kafka/data \
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 \
KAFKA_HOME=/opt/kafka \
PATH=$PATH:/opt/kafka/bin

ARG KAFKA_VERSION=2.6.1
ARG KAFKA_DIST=kafka_2.13-2.6.1
RUN set -x \
    && apt-get update \
    && apt-get install -y openjdk-8-jre-headless wget gnupg2 \
	&& wget -q "https://downloads.apache.org/kafka/$KAFKA_VERSION/$KAFKA_DIST.tgz" \
    && wget -q "https://downloads.apache.org/kafka/$KAFKA_VERSION/$KAFKA_DIST.tgz.asc" \
    && wget -q "https://kafka.apache.org/KEYS" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --import KEYS \
    && gpg --batch --verify "$KAFKA_DIST.tgz.asc" "$KAFKA_DIST.tgz" \
    && tar -xzf "$KAFKA_DIST.tgz" -C /opt \
    && apt-get autoremove -y wget gnupg2 \
    && rm -r "$GNUPGHOME" "$KAFKA_DIST.tgz" "$KAFKA_DIST.tgz.asc"
    
COPY log4j.properties /opt/$KAFKA_DIST/config/

RUN set -x \
    && ln -s /opt/$KAFKA_DIST $KAFKA_HOME \
    && useradd $KAFKA_USER \
    && [ `id -u $KAFKA_USER` -eq 1000 ] \
    && [ `id -g $KAFKA_USER` -eq 1000 ] \
    && mkdir -p $KAFKA_DATA_DIR \
    && chown -R "$KAFKA_USER:$KAFKA_USER"  /opt/$KAFKA_DIST \
    && chown -R "$KAFKA_USER:$KAFKA_USER"  $KAFKA_DATA_DIR
  