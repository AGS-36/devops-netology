## Задача 1 

```text
FROM archlinux:latest

RUN pacman -Sy 
 
RUN pacman -S ponysay --noconfirm

ENTRYPOINT ["/usr/bin/ponysay"]
CMD ["Hey, netology”]
```
---
```
docker_images ► docker run stema91/netology:ponysay_netology

 ___________________________
< /bin/sh ["Hey, netology”] >
 ---------------------------
docker_images ► docker run stema91/netology:ponysay_netology
 ___________________________
< /bin/sh ["Hey, netology”] >
 ---------------------------
           \
            \
             \
              \
               ▄▄▄▄
           █▄▄▄▄▄██▄▄▄▄▄
          ▄▄▄▄▄██▄▄▄▄▄█▄▄▄▄
         ████▄█▄▄█▄▄▄███▄▄▄█
 ▀▄▄▄▄▄▄████████▄▄███▄█████▄▄▄▄▄▄▄▄▄▄
   ████▄▄███▄▄▄▄█████████▄███████████▄
   ▀▄▄▄███▄▄█▄█▄███████▄▄████▄▄▄▄▄▄▄▄▄▄
    ▀▄▄█▄▄▄███▄████▄██▄▄█▄██▄▄▄▄▄▄▄▄▄▄▄▄
     ██████▄▄█▄▄▄▄▄████▄▄█▄▄████████████
     █████▄▄█████████████▄▄█▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄
     ▄▄▄▄▄▄▄▄▄▄▄▄▄████▄▄▄█████████▄▄▄▄██▄▄▄▄▄▄
    ▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄████▄▄▄▄████████▄▄███▄▄███▄▄
   ██████████▄▄███▄▄▄▄▄▄▄▄███▄▄▄▄▄▄▄▄▄█▄▄▄▄██████
  ▄█▀ ▀▀▀▄▄▄▄█▄▄▄██████████████████▄▄▄▄▄▄█████████
  █▄       ▀▀████▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄██████▄▄▄██████▄
▄  ▀█         ▄▄▄▄▄▄▄▄▄▄▄▄▄████████▄▄▄▄▄▄████▄▄█▄▄▄
 ▀▀▀▀       ▀▀▀▄▄▀▀▀▀▀▀▀▄▄█▄▄▄▄▄▄▄▄████████▄▄██▄▀▀
               ▄█       █▄▄████████▄▄▄▄▄▄▄▄█▄▄▄█
              █▀  ▄     ▀████▄▄▄▄▀▀    ▄█▀▀▀ █▀  ▄
              ▀▀▀▀       ████                ▀▀▀▀
                          ██
                           ▀

```

https://hub.docker.com/layers/stema91/netology/ponysay_netology/images/sha256-12786a5145e0c278041da401a5bce4d86e95c2925b43c1273fc9ae4241d4a50b?context=repo


## Задача 2 

VER1

# ![Dockerfile](https://github.com/AGS-36/devops-netology/blob/master/homework_part_2/homework_4/ver1/Dockerfile)
# ![Docker image](https://hub.docker.com/layers/157080270/stema91/netology/ver1/images/sha256-9bd02cb50bbb0899379f6280d06062e52d34b0fee45f279360ee83d076f0163e?context=explore)
# ![screenshort](https://github.com/AGS-36/devops-netology/blob/master/homework_part_2/homework_4/ver2/2021-07-06_10-43.png)

```
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
```

```
ver1 ► docker run --name u_j -ti -p 8080:8080  stema91/netology:ver1
Running from: /usr/lib/jenkins/jenkins.war
webroot: $user.home/.jenkins
2021-07-06 07:40:05.568+0000 [id=1]	INFO	org.eclipse.jetty.util.log.Log#initialized: Logging initialized @244ms to org.eclipse.jetty.util.log.JavaUtilLog
2021-07-06 07:40:05.668+0000 [id=1]	INFO	winstone.Logger#logInternal: Beginning extraction from war file
2021-07-06 07:40:06.643+0000 [id=1]	WARNING	o.e.j.s.handler.ContextHandler#setContextPath: Empty contextPath
2021-07-06 07:40:06.692+0000 [id=1]	INFO	org.eclipse.jetty.server.Server#doStart: jetty-9.4.41.v20210516; built:
```
    
VER2

# ![Dockerfile](https://github.com/AGS-36/devops-netology/blob/master/homework_part_2/homework_4/ver2/Dockerfile)
# ![Docker image](https://hub.docker.com/layers/156762135/stema91/netology/ver2/images/sha256-9c445e52556cafde0e1b42d0605858780d25071a00ea7b45de4655e839d27c40?context=explore)
# ![screenshort](https://github.com/AGS-36/devops-netology/blob/master/homework_part_2/homework_4/ver2/2021-07-02_23-17.png)

```
FROM ubuntu:latest
RUN apt-get update && apt-get install wget gnupg2 gnupg1 default-jdk -y
RUN wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | apt-key add -
RUN sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update && apt-get install jenkins -y
WORKDIR /usr/share/jenkins
ENTRYPOINT service jenkins start && bash
EXPOSE 8080
```

```
ver2 ► docker run --name u_j -ti -p 8080:8080  stema91/netology:ver2 
Correct java version found
 * Starting Jenkins Automation Server jenkins                                                                   [ OK ] 
root@65ef978451cf:/usr/share/jenkins# 
```

## Задача 3 

```
FROM node
EXPOSE 3000
RUN apt-get update && apt-get install npm git -y
RUN npm install -g npm@7.19.1
WORKDIR /home/
RUN git clone https://github.com/simplicitesoftware/nodejs-demo.git
WORKDIR /home/nodejs-demo
RUN npm install && npm start
CMD ["bash"]
```

```
task3 ► docker network inspect bridge-network
[
    {
        "Name": "bridge-network",
        "Id": "bcaff2fc87c24c6b93ba24c032a7a619c9cd198d70628156b74fc46eb6959e46",
        "Created": "2021-07-07T01:34:49.956611081+03:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "1cd35fd1653e5318bcc59d26a2a94aceffa9757fff5f725a9df2542e558f5bec": {
                "Name": "ubuntu",
                "EndpointID": "b199f2ac913c4cc5de47a1054084b31c36c503967a7f9ac1b8950262b9bf4bdf",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            },
            "3e7f0cfd91ab1f2574257d0f58cb8bce4c5265c163f127858d66ab264fe2921a": {
                "Name": "node",
                "EndpointID": "30578f9b1196e90b1fbbdbaffbc9110f94164a777d5b37a8074543ec94745a9d",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
```

```
root@1cd35fd1653e:~# curl 172.18.0.3:3000/curl
скопировал часть вывода
ctumst aliquam duis convallis scelerisque est parturient ullamcorper aliquet fusce suspendisse nunc hac eleifend amet blandit facilisi condimentum commodo scelerisque faucibus aenean ullamcorper ante mauris dignissim consectetuer nullam lorem vestibulum habitant conubia elementum pellentesque morbi facilisis arcu sollicitudin diam cubilia aptent vestibulum auctor eget dapibus pellentesque inceptos leo egestas interdum nulla consectetuer suspendisse adipiscing pellentesque proin lobortis sollicitudin augue elit mus congue fermentum parturient fringilla euismod feugiat</p>\n<p>Aliquam vestibulum nam curae maecenas sed integer cras phasellus suspendisse quisque donec dis praesent accumsan bibendum pellentesque condimentum adipiscing etiam consequat vivamus dictumst aliquam duis convallis scelerisque est parturient ullamcorper aliquet fusce suspendisse nunc hac eleifend amet blandit facilisi condimentum commodo scelerisque faucibus aenean ullamcorper ante mauris dignissim consectetuer nullam lorem vestibulum habitant conubia elementum pellentesque morbi facilisis arcu sollicitudin diam cubilia aptent vestibulum auctor eget dapibus pellentesque inceptos leo egestas interdum nulla consectetuer suspendisse adipiscing pellentesque proin lobortis sollicitudin augue elit mus congue fermentum parturient fringilla euismod feugiat</p>","demoPrdBrochure":"10585","demoPrdOnlineDoc":null,"demoPrdComments":"[2021-05-20 10:04 - Designer DESIGNER]\n[2021-03-22 17:46 - Designer DESIGNER]\n[2021-03-16 10:19 - Designer DESIGNER]\n[2020-06-08 14:23 - Designer]\ntest\n\n[2020-06-08 14:23 - Designer]\ntest\n\n[2021-03-16 10:19 - Designer DESIGNER]\n[2020-06-08 14:23 - Designer]\ntest\n\n[2020-06-08 14:23 - Designer]\ntest\n\n[2021-03-22 17:46 - Designer DESIGNER]\n[2021-03-16 10:19 - Designer DESIGNER]\n[2020-06-08 14:23 - Designer]\ntest\n\n[2020-06-08 14:23 - Designer]\ntest\n\n[2021-03-16 10:19 - Designer DESIGNER]\n[2020-06-08 14:23 - Designer]\ntest\n\n[2020-06-08 14:23 - Designer]\ntest"}];
    var pc = $('#nodejs-demo-products');
    for (var i = 0; i < ps.length; i++) {
      var p = ps[i];
      pc.append(
        $('<li/>')
          .append($('<img/>', { title: p.demoPrdReference, src: 'data:' + p.demoPrdPicture.mime + ';base64,' + p.demoPrdPicture.content }))
          .append($('<h1/>').append(p.demoPrName))
          .append($('<h2/>').append(p.demoPrdReference))
          .append($('<p/>').append(p.demoPrdDescription))
        );
    }
});</script></head><body><div id="nodejs-demo"><div class="text-center" id="header"><img src="/logo.svg" alt="Logo"></div><ul id="nodejs-demo-products"></ul><p class="text-right">&copy; Simplict&eacute; Software, powered by&nbsp;<a href="https://expressjs.com" target="_blank">Express</a></p></div></body></html>root@1cd35fd1653e:~#
```
