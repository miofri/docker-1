# To start a TeamSpeak server, accept the license agreement, and map the ports to the host:
# docker run -p 9987:9987/udp -p 10011:10011 -p 30033:30033 -e TS3SERVER_LICENSE=accept teamspeak
# Then you can connect to localhost in your TeamSpeak client. Please write down the server query password, and server admin privilege key that were generated. These are needed to administrate the TeamSpeak server

FROM debian

EXPOSE 9987/udp
EXPOSE 10011/tcp
EXPOSE 30033/tcp

ENV TS3SERVER_LICENSE=accept

RUN apt-get update && apt-get upgrade -y
RUN apt install apt-utils -y && apt install iproute2 -y && apt install net-tools -y && apt install curl tar bzip2 -y
RUN cd usr/local/etc && curl -O test https://files.teamspeak-services.com/releases/se
rver/3.13.6/teamspeak3-server_linux_amd64-3.13.6.tar.bz2
RUN tar -xf teamspeak3-server_linux_amd64-3.13.6.tar.bz2

WORKDIR /usr/local/etc/teamspeak3-server_linux_amd64/ts3server


# docker build -t tstest .
# docker run -dpit -p 9987:9987/udp -p 10011:10011 -p 30033:30033 tstest
# detached. publish container's ports to host. interactive mode (accepts stdin from terminal). allocate a pesudo terminal that reads stdin/stdout from user.

#  Server Query Admin Account created
#          loginname= "serveradmin", password= "9jDR8sHW"
#          apikey= "BACmCQPJdYF2-PpYfUh82pf5Az0a9YMvz6xFgWO"
#       ServerAdmin privilege key created, please use it to gain
#       serveradmin rights for your virtualserver. please
#       also check the doc/privilegekey_guide.txt for details.

#        token=aVNfNWoGFkagJRV92Z6IedpjuEOOvXFDRK+zIHfW
