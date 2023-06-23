FROM debian:11-slim

RUN apt-get update
RUN apt-get install -y python3-pip wget

RUN mkdir -p /etc/apt/keyrings
RUN wget -q -O /etc/apt/keyrings/mopidy-archive-keyring.gpg https://apt.mopidy.com/mopidy.gpg
RUN wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/bullseye.list

RUN apt-get update
RUN apt-get install -y mopidy mopidy-tunein mopidy-mpd mpc

RUN python3 -m pip install Mopidy-Iris
RUN echo "mopidy  ALL=NOPASSWD:   /usr/local/lib/python3.7/dist-packages/mopidy_iris/system.sh" >> /etc/sudoers

COPY mopidy.conf /var/lib/mopidy/.config/mopidy/mopidy.conf

USER mopidy

VOLUME /var/lib/mopidy

EXPOSE 6600
EXPOSE 6680

CMD ["/usr/bin/mopidy"]