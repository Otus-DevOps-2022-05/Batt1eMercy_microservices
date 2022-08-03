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
