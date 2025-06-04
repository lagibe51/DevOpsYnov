# TP 1

## Installer Docker et Docker-Compose

Ubuntu

```
wsl --install

```

Docker Engine
```
sudo apt update
sudo apt install docker.io docker-compose
```
Vérification que docker fonctionne sur mon Ubuntu

```
docker run hello-world
```

## 

docker run -it ubuntu bash

Dans le bash : exit

# Quelques commandes à tester

```
docker images
docker ps -a
docker run -p 80:80 nginx
docker run -d -p 80:80 nginx
```


# Telechargement de l'image nginx 

```
docker pull nginx
```
## Verification 

```
docker images

```
## Lancement avec un volume 

```
docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html nginx

```

# Étape 4 – Initialisation Git
 
```bash
git init
git add .
git commit -m "Début du TP"
```
Utilisez `git add . && git commit -m "description"` à chaque grande étape.
 
# Étape 5 – Conteneur Web avec volume et docker cp
 
Telechargement de l'image nginx et vérification

```
docker pull nginx
docker images
```
 
 
 
## Lancement avec un volume
 
```
docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html --name Volume-nginx nginx
```
 
 
 ### Arret et supression
```
docker stop Volume-nginx && docker rm Volume-nginx
docker run -d -p 8080:80 --name Volume-nginx nginx
docker cp index.html web-copy:/usr/share/nginx/html/index.html
```




