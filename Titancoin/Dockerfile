# Set the base image
FROM debian

# Dockerfile author / maintainer 
MAINTAINER Watchdog1023

# Update application repository list and install the deps. 
RUN apt-get update && apt-get install git build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev libminiupnpc-dev

#Building Titancoin Daemon
RUN git clone https://github.com/watchdog1023/titancoin.git
RUN cd titancoin/
RUN ./autogen.sh
RUN ./configure --disable-wallet
RUN make
RUN make install
EXPOSE 1023
CMD ["titancoind", "--printtoconsole"]
