FROM python:3.6

LABEL maintainer="Geverson R. Sarmento <geverson.sarmento@stodev.com.br>"
SHELL ["/bin/bash", "-c"]

RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install apt-utils vim -y && \
    apt-get upgrade -y

#RUN apt-get install python3-pip python3-dev
RUN pip3 install --upgrade virtualenv


RUN adduser --system homeassistant --home /opt/homeassistant && \
    addgroup homeassistant && \
    usermod -G dialout -a homeassistant

#RUN mkdir /opt/homeassistant && \ 
#    chown -R homeassistant:homeassistant /opt/homeassistant 

WORKDIR /opt/homeassistant

USER homeassistant

RUN python3 -m venv /opt/homeassistant && \
    source /opt/homeassistant/bin/activate && \
    pip3 install --upgrade homeassistant

EXPOSE 3218 8123

CMD ["/bin/bash", "-c",  "/opt/homeassistant/bin/hass"]