# Docker

#### Содержание 
* **Basic info**
* **Tools**
* **Commands**
* **Commands for few**
* **Стоит обрать внимание**
* **Docker push and pull image**
* **Dockerfile - собираем образ на основе инструкций**
* **Docker compose - обьеденяем образы и собираем в один**
* **Вопросы и Ответы**


--- 


## Basic info
* **Образ** - это набор файлов, необходимых для работы приложения на голой машине с установленным Docker.
* **Контейнер** - это запущенный образ. Из образов создаються и запускаютьс контейнеры.
* **Dockerfile** -  инструкции для построения образа. Это простой способ автоматизировать процесс создания образа.
* **docker-compose.yml** - инструкции для сборки нескольких контейнеров


## Tools
* FromLatest - https://www.fromlatest.io/#/ - для оптимизации `Dockerfile`
* Docker Toolbox - десктопное приложение для Windows и Mac
* Docker Client (CLI) -  только для Linux

## Commands
* **docker run -d -P [image-name]** - запустить образ, тем самым создаеться контейнер, если образ не находитьс локально тогда исчет на докер хабе и скачиваеться, запускаеться. `-d` -  открепить процес от консоли,  `-P` - призначить рандомный порт к порту приложения внутри Docker
* **docker run -it [image-name] sh** - запустить образ и зайти внутрь контейнера 
* **docker run -it --rm [image-name] sh** - запустить образ и зайти внутрь контейнера + удалить контейнер после закрытия
* **docker build -t [image-name] .** - забилдить образ на основе `Dockerfile`
* **docker logs [container-id]** - получить логи с контейнера
* **docker exec -it [container-id] /bin/bash** - войти в контейнер 
* **docker pull [image-name]** - Скачать образ с docker hub
* **docker images** - покажет сколько образов есть локально
* **docker rmi [image-name] [image-name] -f** - удалить  или образы
* **docker ps** - покажет контейнеры
* **docker ps -a** - покажет контейнеры + которые были запущены
* **docker run [image-name] [command]** - запустить образ и выполнить внутри команду
* **docker run -it [image-name] sh** - зайти внутрь контейнера и открыть консоль контейнера. Команда run с флагом -it подключает интерактивный tty в контейнер.
* **docker rm $(docker ps -a -q -f status=exited)** - удалить все контейнеры с статусом exited
* **docker run -d -P --name [your-name-to-container] [image-name]** - Флаг `-d` открепит (detach) терминал, флаг `-P` сделает все открытые порты публичными и случайными, и, наконец, флаг `--name` это имя, которое мы хотим дать контейнеру.
* **docker port [container-name]** - просмотреть порты контейнера
* **docker run -p 8000:3000 [image-name]** - запустить контейнер с перебросом запроса с 0.0.0.0:8000 -> 3000. Слева порт локальный - справа порт Докера, указанный в `Dockerfile (expose)` на который будет переброс запросов
* **docker push [nickname]/[image-name]** - запушить свой образ на свой репозиторий 

## Commands for few
* **sudo docker kill $(sudo docker ps -q)** - убить все контейнеры. `-q` - показать только ID 
* **sudo docker rm $(sudo docker ps -q -a)** - удалить все контейнеры
* **sudo docker rmi $(sudo docker images -q)** - удалить все образы

## Стоит обрать внимание 
* при создание образа командой `docker build -t [image-name] .` в конце - Не забудьте точку !
* Приложение которое переносите в docker-образ меняйте хост с `localhost` -> `0.0.0.0`
* `CMD`  может быть только одно в Dockerfile
* Когда тестируете на Windows то порт будет - `192.168.99.100`, а на Linux - `127.0.0.1` OR `localhost`

## Docker push and pull image
```bash
# Enter your credentials
docker login

# Rename your image if it is not like: nickanme/image-name
docker tag my_image nickname/my_image

# Push your image to your repositories
docker push nickname/my_image

# Pull this image
docker pull nickname/my_image
```

## Dockerfile - собираем образ на основе инструкций
Построить образ на основе `Dockerfile`
```bash
docker build -t [your-image-name] .
# OR
docker build -t [your-nickname]/[your-image-name] .
```

## Docker compose - обьеденяем образы и собираем в один
Если ваше приложение Docker включает более одного контейнера (например, веб-сервер и база данных, работающие в отдельных контейнерах), создание, запуск и подключение контейнеров из отдельных файлов Docker файлов является громоздким и трудоемким. Docker Compose решает эту проблему, позволяя вам использовать файл YAML для определения приложений с несколькими контейнерами. Вы можете настроить столько контейнеров, сколько хотите, как они должны быть построены и подключены и где должны храниться данные. Когда файл YAML будет завершен, вы можете запустить одну команду для создания, запуска и настройки всех контейнеров.

## Вопросы и Ответы
**1)** Как уменьшить размер образа? допустим nodejs official весит 400 мб в свернутом состоянии. 
> * Использовать еще меньший отцовский образ, например: `ubuntu - 43mb` или `alpine - 5mb`
> * Попробовать найти уже нужный образ с наименьшим размером, например: `alpine-node - 67mb`
> * Не устанавливать отладочные иструменты, например: `vim` или `curl`
> * Больше здесь: https://hackernoon.com/tips-to-reduce-docker-image-sizes-876095da3b34




