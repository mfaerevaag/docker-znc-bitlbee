FROM        ubuntu:12.04
MAINTAINER  Markus Faerevaag <m@frv.ag>

env VERSION=1.2

RUN echo 'preparing support packages for znc...'
RUN apt-get update
RUN apt-get install -y libssl-dev automake gettext g++ make

RUN echo 'creating /znc...'
RUN mkdir -p /znc

RUN echo "installing vnc-v${VERSION}..."
RUN curl -O http://znc.in/releases/archive/znc-$VERSION.tar.gz
RUN tar zxf znc-$VERSION.tar.gz
RUN cd znc-$VERSION && ./configure
RUN cd znc-$VERSION && make
RUN cd znc-$VERSION && make install

RUN echo 'installing modules...'

RUN curl -LO https://raw2.github.com/Palaver/znc-palaver/master/palaver.cpp
RUN znc-buildmod palaver.cpp
RUN cp palaver.so /usr/local/lib/znc/palaver.so

RUN curl -LO https://raw.github.com/kylef/znc-contrib/master/clientaway.cpp
RUN znc-buildmod clientaway.cpp
RUN cp clientaway.so /usr/local/lib/znc/clientaway.so

RUN echo 'cleaning up...'
RUN apt-get remove -y libssl-dev automake gettext g++ make
RUN apt-get autoremove -y
RUN apt-get clean
RUN rm -rf znc-$VERSION znc-$VERSION.tar.gz

RUN echo 'finishing...'
ADD run /znc/run
RUN chmod +x /znc/run

ENTRYPOINT ["/znc/run"]
CMD ["noop"]
