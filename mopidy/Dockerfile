FROM debian:11-slim

RUN apt-get update
RUN apt-get install -y --fix-missing gcc curl python-crypto python3-setuptools python-pip wget git

RUN mkdir -p /etc/apt/keyrings
RUN wget -q -O /etc/apt/keyrings/mopidy-archive-keyring.gpg https://apt.mopidy.com/mopidy.gpg
RUN wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/bullseye.list

RUN apt-get update
RUN apt-get install -y mopidy mopidy-tunein mopidy-mpd mpc

RUN git clone https://github.com/jaedb/Iris.git
RUN cd Iris
RUN python3 setup.py install
RUN cd ..

RUN echo "mopidy ALL=NOPASSWD: /usr/local/lib/python3.7/dist-packages/Mopidy_Iris-3.44.0-py3.7.egg/mopidy_iris/system.sh" >> /etc/sudoers

RUN chown mopidy:audio -R /var/lib/mopidy/.config

COPY mopidy.conf /var/lib/mopidy/.config/mopidy/mopidy.conf

USER mopidy

VOLUME /var/lib/mopidy

EXPOSE 6600
EXPOSE 6680

CMD ["/usr/bin/mopidy"]