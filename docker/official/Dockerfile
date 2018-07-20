FROM rundeckapp/testdeck:base-latest

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

VOLUME ["/home/rundeck/server/data"]

CMD ./confd -onetime -backend env && java -jar rundeck.war