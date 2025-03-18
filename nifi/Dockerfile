FROM apache/nifi:1.20.0
ARG UID
ARG GID
USER root

RUN apt-get update && \
	apt-get install -y python3.10 python3-pip

# Change UID
RUN usermod -u $UID nifi && groupmod -g $GID nifi \
 && chown -R nifi:nifi ${NIFI_BASE_DIR}

USER nifi

# Hive Processor
WORKDIR /opt/nifi/nifi-current/lib
RUN wget https://repository.apache.org/content/repositories/releases/org/apache/nifi/nifi-hive-nar/1.20.0/nifi-hive-nar-1.20.0.nar \
 && wget https://repository.apache.org/content/repositories/releases/org/apache/nifi/nifi-hive-services-api-nar/1.20.0/nifi-hive-services-api-nar-1.20.0.nar \
 && wget https://repository.apache.org/content/repositories/releases/org/apache/nifi/nifi-hive3-nar/1.20.0/nifi-hive3-nar-1.20.0.nar



WORKDIR /opt/nifi/nifi-current


USER root

RUN groupadd -g 11002 incog

COPY ./requirements.txt /opt
RUN pip install --no-cache-dir -r /opt/requirements.txt

RUN groupadd -g 987 docker 
