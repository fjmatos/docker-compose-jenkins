FROM h1kkan/jenkins-docker:2.303.1

LABEL Owner="jms@gmail.com"

# if we want to install via apt

USER root

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update &&  apt-get install -y apt-utils sshpass vim dialog
RUN apt-get install -y sudo


# Cambiamos la zona horaria del contenedor
ENV TZ=Europe/Madrid
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


# Añadimos el repo Debian Testing para instalar python 3.8 ya que Debian Stable esta python  3.6
#
RUN echo "deb http://ftp.de.debian.org/debian testing main" >> /etc/apt/sources.list

# Desactivo esta seccion porque me da fallo con las keys
RUN apt install -y gnupg2
#RUN gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 04EE7237B7D453EC


# Instalamos python3 pero es necesario desactivar el repor Inmmediate

RUN apt-get update
RUN apt-get -t testing install -y python3 -o APT::Immediate-Configure=0
RUN apt-get -t testing install -y python3-setuptools -o APT::Immediate-Configure=0
RUN apt-get -t testing install -y python3-pip -o APT::Immediate-Configure=0
RUN apt-get -t testing install -y python3-venv -o APT::Immediate-Configure=0

RUN pip3 install ansible
RUN pip3 install wheel
RUN pip3 install twine


# Añadimos el modulo de python para desplegar desde Ansible a Windows con winrm

RUN apt-get -t testing install -y libkrb5-dev -o APT::Immediate-Configure=0
RUN apt-get -t testing install -y krb5-user -o APT::Immediate-Configure=0

RUN pip3 install pywinrm
RUN pip3 install pykerberos
RUN pip3 install requests_kerberos

COPY krb5.conf /etc/

#  Add  NODEJS

RUN apt-get -t testing install -y nodejs -o APT::Immediate-Configure=0
RUN apt-get -t testing install -y npm -o APT::Immediate-Configure=0

USER jenkins

