FROM ubuntu:xenial

ENV SEMAPHORE_VERSION="2.3.0" SEMAPHORE_ARCH="linux_amd64"

RUN apt-get clean && \
    apt-get update && \
    apt-get install -y git \
                    locales \
                    apt-utils \
                    ansible \
                    mysql-client \
                    curl \
                    fping \
                    libcurl3 \
                    python-pip \
                    libffi-dev \
                    libssl-dev \
                    python-dev \
                    libkrb5-dev \
                    krb5-user \
                    openssh-client && \
                    curl -sSfL "https://github.com/ansible-semaphore/semaphore/releases/download/v$SEMAPHORE_VERSION/semaphore_$SEMAPHORE_ARCH" > /usr/bin/semaphore && \
                    chmod +x /usr/bin/semaphore && \
                    mkdir -p /etc/semaphore/playbooks

RUN pip install ansible "pywinrm>=0.2.2"

EXPOSE 3000

VOLUME ["/etc/semaphore/playbooks"]

ADD ./scripts/docker-startup.sh /usr/bin/semaphore-startup.sh
RUN chmod +x /usr/bin/semaphore-startup.sh

ENTRYPOINT ["/bin/bash"]

CMD ["/usr/bin/semaphore-startup.sh", "/usr/bin/semaphore", "-config", "/etc/semaphore/semaphore_config.json"]
