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

```
FROM alpine:latest
RUN apk add --no-cache bash
CMD echo 'Hello_netology'
```
    
VER2
![Dockerfile](/ver2/Dockerfile)
![screenshort](/ver2/2021-07-02_23-17.png)
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

