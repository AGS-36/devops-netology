FROM amazoncorretto
USER root
RUN yum install wget -y
RUN wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo 
RUN rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
RUN yum upgrade -y
RUN yum install jenkins -y
RUN yum install java-11-amazon-corretto -y
WORKDIR /usr/lib/jenkins/
ENTRYPOINT java -jar jenkins.war
CMD ["bash"]
EXPOSE 8080
