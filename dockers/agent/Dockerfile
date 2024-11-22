FROM debian:trixie-slim

LABEL version "4.3.4"
LABEL description "Wazuh Agent"

COPY bin/entrypoint.sh /
COPY config /opt/ossec

#Install pre
RUN apt-get update && apt-get install -y python3 procps curl apt-transport-https gnupg2 inotify-tools gettext-base 

#Install wazuh
RUN curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add - 
RUN echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | tee /etc/apt/sources.list.d/wazuh.list 


RUN apt-get update && apt-get install -y wazuh-agent=4.8.2-1

#To use latest version
#RUN apt-get update && apt-get install -y wazuh-agent=4.8.2-1

#Adding Webserver and ready, metrics 
COPY web /web
RUN chmod +x /web/ready.sh



RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]