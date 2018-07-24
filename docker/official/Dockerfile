FROM rundeck/ubuntu-base:latest

RUN true && \
    # Install confd
    wget https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 && \
    mv confd* /usr/local/bin/confd && \
    chmod ugo+x /usr/local/bin/confd && \
    # Setup rundeck user
    adduser --shell /bin/bash --home /home/rundeck --gecos "" --disabled-password rundeck \
    && passwd -d rundeck \
    && addgroup rundeck sudo

USER rundeck

WORKDIR /home/rundeck

COPY --chown=rundeck:rundeck .build .
COPY --chown=rundeck:rundeck confd /etc/confd

RUN java -jar rundeck.war --installonly

VOLUME ["/home/rundeck/server/data"]

CMD confd -onetime -backend env && java -XX:+UnlockExperimentalVMOptions -XX:MaxRAMFraction=1 -XX:+UseCGroupMemoryLimitForHeap -jar rundeck.war