FROM rundeckapp/testdeck:base-latest

ENV RUNDECK_DATABASE_USERNAME ""
ENV RUNDECK_DATABASE_PASSWORD ""

RUN apt-get update && \
    apt-get install -y --no-install-recommends wget && \
    adduser --shell /bin/bash --home /home/rundeck --gecos "" --disabled-password rundeck \
    && passwd -d rundeck \
    && addgroup rundeck sudo

USER rundeck

WORKDIR /home/rundeck

COPY --chown=rundeck:rundeck .build .
COPY --chown=rundeck:rundeck confd /etc/confd

RUN wget https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 && \
    mv confd* confd && \
    chmod u+x confd && \
    java -jar rundeck.war --installonly


ENV RUNDECK_SERVER_ADDRESS=0.0.0.0
ENV RUNDECK_GRAILS_URL="http://127.0.0.1:4440"

VOLUME ["/home/rundeck/server/data"]

CMD ./confd -onetime -backend env && java -jar rundeck.war