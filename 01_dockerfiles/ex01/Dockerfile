# To start a TeamSpeak server, accept the license agreement, and map the ports to the host:
# docker run -p 9987:9987/udp -p 10011:10011 -p 30033:30033 -e TS3SERVER_LICENSE=accept teamspeak
# Then you can connect to localhost in your TeamSpeak client. Please write down the server query password, and server admin privilege key that were generated. These are needed to administrate the TeamSpeak server

FROM debian

EXPOSE 9987/udp
EXPOSE 10011/tcp
EXPOSE 30033/tcp

ENV TS3SERVER_LICENSE=accept

RUN apt-get update
RUN apt-get upgrade`
RUN apt install apt-utils
RUN apt-install iproute2
RUN apt-install net-tools

# docker build -t tstest .
# docker run -dpit -p 9987:9987/udp -p 10011:10011 -p 30033:30033 tstest

# detached. publish container's ports to host. interactive mode (accepts stdin from terminal). allocate a pesudo terminal that reads stdin/stdout from user.