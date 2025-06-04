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

```
docker run -it ubuntu bash
exit
```

## Quelques commandes à tester

```
docker images
docker ps -a
docker run -p 80:80 nginx
docker run -d -p 80:80 nginx
```

## Initialisation Git

```bash
git init
git add .
git commit -m "Début du TP"
```
Pour la suite du TP : `git add . && git commit -m "description" && git push`

# Conteneur Web avec volume et docker cp

Telechargement de l'image nginx et vérification

```
docker pull nginx
docker images
```

Lancement avec un volume

```
docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html --name web-volume nginx
```
 
 
### Arret et supression
```
docker stop Volume-nginx && docker rm Volume-nginx
```

### Utilisation de docker cp
```
docker run -d -p 8080:80 --name Volume-nginx nginx
docker cp index.html Volume-nginx:/usr/share/nginx/html/index.html
```

# Creation d'un dockerFile
```Dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
```

## Build du dockerfile

Commandes :
```bash
docker build -t nginx .
docker run -d -p 8081:80 ginx
```

## Avantages et inconvénients
### Avantages 
#### Volume 
Rapide
#### Dockerfile
Permet de partager et de creer différentes versions

### inconvénients 
#### Volume 
La creation du volume ne permet pas de créer des versions 
#### Dockerfile
Obligation de rebuild à chaque changement 

## MySQL et PhpMyAdmin avec docker run

Installations

```
docker pull mysql:5.7
docker pull phpmyadmin/phpmyadmin
```

Création d'un réseau Docker dédié pour que les conteneurs puissent se parler

```
docker network create tp-net
```

Lancement des conteneurs 

```
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=test --network tp-net mysql:5.7
docker run -d --name phpmyadmin -p 8082:80 --network tp-net -e PMA_HOST=mysql phpmyadmin/phpmyadmin
```

## Docker Compose

Création du fichier `docker-compose.yml` :

QUestions : 


