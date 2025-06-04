# TP 1

## Installer Docker et Docker-Compose

Ubuntu

```
wsl --install
```

Docker Engine

```
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
```

Docker

```
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

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


