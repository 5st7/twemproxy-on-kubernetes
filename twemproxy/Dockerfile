FROM alpine:latest

RUN apk add --update g++ libtool make automake curl autoconf supervisor

RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN curl -qL https://github.com/twitter/twemproxy/releases/download/0.5.0/twemproxy-0.5.0.tar.gz | tar xzf -
RUN cd  twemproxy-0.5.0 && autoreconf -fvi && ./configure --enable-debug=log && make && make install

RUN apk del g++ libtool make automake curl autoconf

EXPOSE 6379

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

