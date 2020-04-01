FROM freeway/android

LABEL maintainer="teregulowrustem@gmail.com"

RUN apt-get -qq update && apt-get -qq install graphviz
RUN apt-get autoremove -y && \
    apt-get clean
