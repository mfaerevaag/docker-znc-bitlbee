FROM        ubuntu:12.04
MAINTAINER  Jeff Smick <jeff@squishtech.com>

ENV VERSION=3.4.2

RUN echo 'preparing support packages...'
RUN apt-get update
RUN apt-get install -y libglib2.0-dev
RUN apt-get install -y libssl-dev
RUN apt-get install -y g++
RUN apt-get install -y make
RUN apt-get install -y xsltproc
RUN apt-get install -y xmlto

RUN echo 'creating /bitlbee dirs...'
RUN mkdir -p /bitlbee/bin
RUN mkdir -p /bitlbee/state/configs

RUN echo 'installing bitlbee-v$VERSION...'
RUN curl -O http://get.bitlbee.org/src/bitlbee-$VERSION.tar.gz
RUN tar zxf bitlbee-$VERSION.tar.gz
RUN cd bitlbee-$VERSION && ./configure --ssl=openssl --otr=1 --purple=1
RUN cd bitlbee-$VERSION && make
RUN cd bitlbee-$VERSION && make install
RUN rm -rf bitlbee-$VERSION bitlbee-$VERSION.tar.gz

RUN echo 'installing bitlbee-facebook...'
RUN curl -LO https://github.com/bitlbee/bitlbee-facebook/releases/download/v1.0.0/bitlbee-facebook-1.0.0.tar.gz
RUN tar zxf bitlbee-facebook-1.0.0.tar.gz
RUN cd bitlbee-facebook-1.0.0 && ./autogen.sh
RUN cd bitlbee-facebook-1.0.0 && make
RUN cd bitlbee-facebook-1.0.0 && make install
RUN rm -rf bitlbee-facebook-1.0.0 bitlbee-facebook-1.0.0.tar.gz

RUN echo 'removing support packages...'
RUN apt-get remove -y libglib2.0-dev
RUN apt-get remove -y libssl-dev
RUN apt-get remove -y g++
RUN apt-get remove -y make
RUN apt-get remove -y xsltproc
RUN apt-get remove -y xmlto
RUN apt-get autoremove -y
RUN apt-get clean

RUN echo 'running...'
ADD run /bitlbee/run
RUN chmod +x /bitlbee/run

EXPOSE 6667
ENTRYPOINT ["/bitlbee/run"]
CMD ["noop"]
