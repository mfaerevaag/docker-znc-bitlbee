FROM        ubuntu:12.04
MAINTAINER  Jeff Smick <jeff@squishtech.com>

env VERSION=1.2

RUN echo 'preparing support packages for znc...'
RUN apt-get update
RUN apt-get install -y libssl-dev
RUN apt-get install -y automake
RUN apt-get install -y gettext
RUN apt-get install -y g++
RUN apt-get install -y make

RUN echo 'creating /znc...'
RUN mkdir -p /znc

RUN echo 'installing vnc-v$VERSION...'
RUN curl -O http://znc.in/releases/znc-$VERSION.tar.gz
RUN tar zxf znc-$VERSION.tar.gz
RUN cd znc-$VERSION && ./configure
RUN cd znc-$VERSION && make
RUN cd znc-$VERSION && make install
RUN rm -rf znc-$VERSION.tar.gz znc-$VERSION

RUN echo 'installing clientaway module...'
RUN curl -O https://raw.github.com/kylef/znc-contrib/master/clientaway.cpp
RUN znc-buildmod clientaway.cpp
RUN mv clientaway.so /usr/local/lib/znc/clientaway.so

RUN echo 'removing support packages for znc...'
RUN apt-get remove -y libssl-dev
RUN apt-get remove -y automake
RUN apt-get remove -y gettext
RUN apt-get remove -y g++
RUN apt-get remove -y make
RUN apt-get autoremove -y
RUN apt-get clean

RUN echo 'running znc...'
ADD run /znc/run
RUN chmod +x /znc/run

ENTRYPOINT ["/znc/run"]
CMD ["noop"]
