FROM ubuntu:16.04

ARG walletPackage
ARG walletRepo
ARG walletDaemon
ENV runDaemon $walletDaemon

RUN apt -y update -qq \
    && apt -y install -qq --no-install-recommends \ 
       curl unzip wget git \
       apt-transport-https \ 
       ca-certificates \
       software-properties-common \
    && apt -y autoremove

# install system dependencies
RUN apt -y update -qq \
    && apt -y install -qq --no-install-recommends \
        libminiupnpc-dev \
        build-essential \
        libdb++-dev \
        libboost-all-dev \
        libssl-dev \
    && rm -rf /var/cache/apk/* \
    && apt -y autoremove

# bitcoind dependencies
RUN add-apt-repository ppa:bitcoin/bitcoin \
    && apt -y update -qq \
    && apt -y install -qq libdb4.8-dev libdb4.8++-dev \
    && apt -y autoremove

# build/install the Qt wallet (Staking Wallet)
WORKDIR /app
RUN git clone ${walletRepo}
WORKDIR /app/${walletPackage}/src
RUN make -f makefile.unix && strip ${walletDaemon} && mv ${walletDaemon} /usr/local/bin
WORKDIR /app
RUN rm -rf /app/${walletPackage}

ENTRYPOINT ["sh", "-c", "eval $runDaemon"]
