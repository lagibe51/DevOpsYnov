# TP 1

## Installer Docker et Docker-Compose

Ubuntu

```
wsl --install
```

Docker Engine

````
sudo apt update
sudo apt install docker.io docker-compose
'''

Vérification que docker fonctionne sur mon Ubuntu

```
docker run hello-world
```

## 

docker run -it ubuntu bash
# Dans le bash : exit
docker images
docker ps -a
docker run -p 80:80 nginx
docker run -d -p 80:80 nginx


