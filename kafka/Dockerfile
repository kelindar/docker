FROM misakai/java
MAINTAINER Roman Atachiants "roman@misakai.com"

ENV KAFKA_SCALA_VERSION 2.9.2
ENV KAFKA_VERSION 0.8.1.1

ENV KAFKA_RELEASE $KAFKA_SCALA_VERSION-$KAFKA_VERSION
ENV KAFKA_HOME /opt/kafka_$KAFKA_RELEASE

# Actually download the appropriate kafka release
ADD http://www.eu.apache.org/dist/kafka/0.8.1.1/kafka_$KAFKA_RELEASE.tgz /opt/
#ADD dist/kafka_$KAFKA_RELEASE.tgz /opt/

ADD server.properties $KAFKA_HOME/config/server.properties
ADD start.sh /start.sh

CMD ["/start.sh"]
