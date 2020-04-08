FROM debian
RUN apt update -y && apt upgrade -y && apt install wget bzip2 -y && adduser ts3
WORKDIR /home/ts3
RUN wget https://files.teamspeak-services.com/releases/server/3.7.1/teamspeak3-server_linux_amd64-3.7.1.tar.bz2 && tar xvjf teamspeak3-server_linux_amd64-3.7.1.tar.bz2 && rm teamspeak3-server_linux_amd64-3.7.1.tar.bz2 && mv teamspeak3-server_linux_amd64 ts3server && apt purge wget bzip2 -y
ENV TS3SERVER_LICENSE accept
WORKDIR /home/ts3/ts3server
RUN chmod 755 ts3server_minimal_runscript.sh && chmod 755 ts3server_startscript.sh &&chmod 755 ts3server
CMD ["./ts3server_minimal_runscript.sh"]
EXPOSE 9987/udp 30033 10011
