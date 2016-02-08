FROM node
MAINTAINER Jesper Veggerby <jesper@veggerby.com>
# heavily inspired by https://github.com/jgarverick/vsoagent/tree/master/node

###########################################################
#  Install node.js and npm dependencies (gulp, bower, vsoagent-installer)
###########################################################

RUN npm install -g vsoagent-installer bower gulp


###########################################################
#  Create a service user as root access throws an error
###########################################################
RUN echo "vsoservice\nvsoservice\n\n\n\n\n\n\n" | adduser vsoservice
RUN su vsoservice
###########################################################
#  Install the agent
###########################################################
RUN mkdir /opt/vsoagent 
RUN mkdir /opt/vsoagent/_work
WORKDIR /opt/vsoagent
RUN vsoagent-installer
WORKDIR /opt/vsoagent/agent
COPY agent.config /opt/vsoagent/agent/.agent
RUN chown -R vsoservice /opt/vsoagent

USER vsoservice
ENTRYPOINT /bin/bash

CMD [ "node", "vsoagent.js" ]