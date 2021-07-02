FROM ubuntu:latest
RUN apt-get update && apt-get install wget gnupg2 gnupg1 default-jdk -y
RUN wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | apt-key add -
RUN sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update && apt-get install jenkins -y
WORKDIR /usr/share/jenkins
ENTRYPOINT service jenkins start && bash
EXPOSE 8080
