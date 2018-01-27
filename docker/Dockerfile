FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive

# Usual update / upgrade
RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y

# Install requirements
RUN apt-get install -y curl supervisor git vim

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -
RUN apt-get install --fix-missing -y nodejs

# Get slack-irc
RUN git clone https://github.com/isi-lincoln/slack-irc.git

RUN cd /slack-irc && git pull && npm install && npm run build

# Add supervisor configs
ADD supervisord.conf supervisord.conf

# Add our config file - and our secret token file
ADD config.json /slack-irc/config.json
ADD tokenfile.json /slack-irc/tokenfile.json

CMD ["-n", "-c", "/supervisord.conf"]
ENTRYPOINT ["/usr/bin/supervisord"]
