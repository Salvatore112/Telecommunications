FROM ubuntu:22.04

ENV DOMAIN=example.com \
    HOSTNAME=mail.example.com
    USERNAME=user \
    PASSWORD=qwerty

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    postfix \
    telnet \
    && rm -rf /var/lib/apt/lists/*


RUN echo "postfix postfix/mailname string $DOMAIN" | debconf-set-selections && \
    echo "postfix postfix/main_mailer_type string 'Internet Site'" | debconf-set-selections && \
    postconf -e "myhostname = $HOSTNAME" && \
    postconf -e "mydomain = $DOMAIN" && \
    postconf -e "myorigin = \$mydomain" && \
    postconf -e "inet_interfaces = all" && \
    postconf -e "mydestination = \$myhostname, localhost.\$mydomain, localhost, \$mydomain" && \
    postconf -e "mynetworks = 0.0.0.0/0" && \
    postconf -e "maillog_file = /var/log/mail.log" && \
    sed -i 's/^#submission/submission/' /etc/postfix/master.cf

RUN useradd -m -s /bin/bash $USERNAME && \
    echo "$USERNAME:$PASSWORD" | chpasswd

EXPOSE 25 587

CMD ["/usr/sbin/postfix", "start-fg"]