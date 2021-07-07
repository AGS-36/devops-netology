FROM node
EXPOSE 3000
RUN apt-get update && apt-get install npm git -y
RUN npm install -g npm@7.19.1
WORKDIR /home/
RUN git clone https://github.com/simplicitesoftware/nodejs-demo.git
WORKDIR /home/nodejs-demo 
ENTRYPOINT npm install && npm start
CMD ["bash"]

