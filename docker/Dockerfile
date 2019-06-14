FROM ubuntu:16.04


RUN apt update && \
    apt install -y python3-click python3-jinja2 python3-markdown lsb-release \
        cython3 python3-dev python3-cffi \
        software-properties-common libsasl2-modules-gssapi-mit npm nodejs \
        libkrb5-dev libldap2-dev libsasl2-dev gawk libncurses5-dev \
        rsync attr wget unzip \
        python3-pip python3-mysql.connector python3-requests python3-pyxattr && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /srv/certidude

COPY . /srv/certidude

COPY docker/client.conf /etc/certidude/client.conf

RUN pip3 install -r requirements.txt && \
    pip3 install -e . && \
    echo "done"

RUN LC_ALL=C.UTF-8 LANG=C.UTF-8 certidude provision authority -cn adamsCA.local


VOLUME [ "/etc/certidude/", "/var/lib/certidude/", "/srv/certidude"]

EXPOSE 443
#add to entrypoint:
#export LC_ALL=C.UTF-8 && export LANG=C.UTF-8

#docker build --add-host adamsCA.local:127.0.0.1  -t certidude -f docker/Dockerfile .
#docker run -it --rm -p 8443:443 --hostname adamsCA.local -p $(pwd)/etc:/etc/certidude/ certidude:latest bash