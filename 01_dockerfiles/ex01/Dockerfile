FROM	debian

# Installation packages & dépendances
RUN		apt-get update && apt-get upgrade -y
RUN		apt-get install -y bzip2 ca-certificates

# Ouvertures des ports nécessaires à TS3 (voir ts3server.ini)
EXPOSE	9987/udp
EXPOSE	10011
EXPOSE	30033

# Ajout d'un user qui lancera le serveur
RUN		adduser --disabled-login --gecos 'TS3' teamspeak3

# Ouverture des ports
EXPOSE	9987/udp 30033 10011

# Accepation de la license du serveur
ENV		TS3SERVER_LICENSE=accept

# Téléchargement de l'archive d'installation & attribution des droits pour l'user
ADD		http://dl.4players.de/ts/releases/3.0.13.6/teamspeak3-server_linux_amd64-3.0.13.6.tar.bz2 \
			/home/teamspeak3/teamspeak3-server.tar.bz2
# Ajout de tous les droits du fichier ts3.tar.bz2 à l'user crée au dessus : teamspeak3
RUN 	chown -R teamspeak3:teamspeak3 /home/teamspeak3/teamspeak3-server.tar.bz2

# Changement d'user
USER 	teamspeak3
WORKDIR /home/teamspeak3

# Décompression et lancement du serveur
RUN 	tar -jxvf teamspeak3-server.tar.bz2 && rm teamspeak3-server.tar.bz2 \
			&& mv teamspeak3-server_linux_amd64 server
ADD 	ts3server.ini /home/teamspeak/server
WORKDIR	server
CMD		["sh", "ts3server_minimal_runscript.sh", "inifile=ts3server.ini"]

# test-commands:
#docker build -t test .
#docker run -it -d --name ts3 -p 30033:30033 -p 9987:9987/udp -p 10011:10011 test
