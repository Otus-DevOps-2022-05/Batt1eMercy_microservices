# Batt1eMercy_microservices
Batt1eMercy microservices repository  

## Docker контейнеры. Docker под капотом
VM:
```
yc compute instance create \
  --name docker-host \
  --zone ru-central1-a \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1804-lts,size=15 \
  --ssh-key ~/.ssh/ubuntu.pub
```
  
Docker machine:  
```
docker-machine create \
  --driver generic \
  --generic-ip-address=<pub ip> \
  --generic-ssh-user yc-user \
  --generic-ssh-key ~/.ssh/ubuntu \
  docker-host
```
## Docker образы. Микросервисы

``` docker volume create reddit_db ```
```
docker run -d --network=reddit --network-alias=post_db \
  --network-alias=comment_db -v reddit_db:/data/db mongo:latest
```
```
docker run -d --network=reddit \
  --network-alias=post batt1emercy/post:1.0
```
```
docker run -d --network=reddit \
  --network-alias=comment batt1emercy/comment:1.0
```
```
docker run -d --network=reddit \
  -p 9292:9292 batt1emercy/ui:2.0
```
## Сетевое взаимодействие Docker контейнеров. Docker Compose. Тестирование образов  
  
Задать имена для сущностей docker-compose можно посредством инструкции ```name```  

## Устройство Gitlab CI. Построение процесса непрерывной интеграции 

* Создали композник с gitlab  
* Создали тестовый gitlab-ci
  
## Введение в мониторинг. Модели и принципы работы систем мониторинга
  
dockerhub: `https://hub.docker.com/`  

## Применение системы логирования в инфраструктуре на основе Docker  
VM:  
```
yc compute instance create \
  --name logging \
  --memory 4 \
  --zone ru-central1-a \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1804-lts,size=15 \
  --ssh-key ~/.ssh/ubuntu.pub
```
  
Docker machine:  
```
docker-machine create \
  --driver generic \
  --generic-ip-address=<pub ip> \
  --generic-ssh-user yc-user \
  --generic-ssh-key ~/.ssh/ubuntu \
  logging
```
```
eval $(docker-machine env logging)
docker-machine rm logging
yc compute instance delete logging
```
