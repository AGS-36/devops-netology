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

# ![Dockerfile](https://github.com/AGS-36/devops-netology/blob/master/homework_part_2/homework_4/ver2/Dockerfile)
# ![Docker image](https://hub.docker.com/layers/156762135/stema91/netology/ver2/images/sha256-9c445e52556cafde0e1b42d0605858780d25071a00ea7b45de4655e839d27c40?context=explore)
# ![screenshort](https://github.com/AGS-36/devops-netology/blob/master/homework_part_2/homework_4/ver2/2021-07-02_23-17.png)

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
ver1 ► docker run --name u_j -ti -p 8080:8080  stema91/netology:ver3
Running from: /usr/lib/jenkins/jenkins.war
webroot: $user.home/.jenkins
2021-07-06 07:40:05.568+0000 [id=1]	INFO	org.eclipse.jetty.util.log.Log#initialized: Logging initialized @244ms to org.eclipse.jetty.util.log.JavaUtilLog
2021-07-06 07:40:05.668+0000 [id=1]	INFO	winstone.Logger#logInternal: Beginning extraction from war file
2021-07-06 07:40:06.643+0000 [id=1]	WARNING	o.e.j.s.handler.ContextHandler#setContextPath: Empty contextPath
2021-07-06 07:40:06.692+0000 [id=1]	INFO	org.eclipse.jetty.server.Server#doStart: jetty-9.4.41.v20210516; built:```
---
    
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

В данном задании вы научитесь:
- объединять контейнеры в единую сеть
- исполнять команды "изнутри" контейнера

Для выполнения задания вам нужно:
- Написать Dockerfile: 
    - Использовать образ https://hub.docker.com/_/node как базовый
    - Установить необходимые зависимые библиотеки для запуска npm приложения https://github.com/simplicitesoftware/nodejs-demo
    - Выставить у приложения (и контейнера) порт 3000 для прослушки входящих запросов  
    - Соберите образ и запустите контейнер в фоновом режиме с публикацией порта

- Запустить второй контейнер из образа ubuntu:latest 
- Создайть `docker network` и добавьте в нее оба запущенных контейнера
- Используя `docker exec` запустить командную строку контейнера `ubuntu` в интерактивном режиме
- Используя утилиту `curl` вызвать путь `/` контейнера с npm приложением  

Для получения зачета, вам необходимо предоставить:
- Наполнение Dockerfile с npm приложением
- Скриншот вывода вызова команды списка docker сетей (docker network cli)
- Скриншот вызова утилиты curl с успешным ответом

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

