FROM        buildpack-deps:jessie-curl
MAINTAINER  Markus Faerevaag <m@frv.ag>

ENV VERSION=3.4.2

RUN echo 'preparing support packages for bitlbee...'
RUN apt-get update
RUN apt-get install -y --no-install-recommends \
    autoconf automake gettext gcc libtool make dpkg-dev libglib2.0-dev \
    libotr5-dev libpurple-dev libgnutls28-dev libjson-glib-dev libssl-dev

RUN echo 'creating /bitlbee...'
RUN mkdir -p /bitlbee/bin
RUN mkdir -p /bitlbee/state/configs

RUN echo "installing bitlbee-v${VERSION}..."
RUN curl -LO http://get.bitlbee.org/src/bitlbee-$VERSION.tar.gz
RUN tar zxf bitlbee-$VERSION.tar.gz
RUN cd bitlbee-$VERSION && ./configure --ssl=openssl --jabber=1 --otr=1 --purple=1
RUN cd bitlbee-$VERSION && make
RUN cd bitlbee-$VERSION && make install
RUN cd bitlbee-$VERSION && make install-etc
RUN cd bitlbee-$VERSION && make install-dev

RUN echo 'installing skype4pidgin...'
RUN curl -LO https://github.com/EionRobb/skype4pidgin/archive/1.1.tar.gz
RUN tar zxvf 1.1.tar.gz
RUN cd skype4pidgin-1.1/skypeweb && make
RUN cd skype4pidgin-1.1/skypeweb && make install

RUN echo 'installing bitlbee-facebook...'
RUN curl -LO https://github.com/jgeboski/bitlbee-facebook/archive/v1.0.0.tar.gz
RUN tar zxf v1.0.0.tar.gz
RUN cd bitlbee-facebook-1.0.0 && ./autogen.sh
RUN cd bitlbee-facebook-1.0.0 && make
RUN cd bitlbee-facebook-1.0.0 && make install

run echo 'cleaning up...'
run rm -rf bitlbee-$VERSION bitlbee-$VERSION.tar.gz
run rm -rf skype4pidgin-1.1 1.1.tar.gz
run rm -rf bitlbee-facebook-1.0.0 v1.0.0.tar.gz
RUN apt-get autoremove -y --purge autoconf automake gcc libtool make dpkg-dev
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /tmp/*

RUN echo 'finishing...'
ADD run /bitlbee/run
RUN chmod +x /bitlbee/run

EXPOSE 6667
ENTRYPOINT ["/bitlbee/run"]
CMD ["noop"]
