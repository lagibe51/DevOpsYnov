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

# Quelques commandes à tester

```
docker images
docker ps -a
docker run -p 80:80 nginx
docker run -d -p 80:80 nginx
```

# Initialisation Git

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



```
docker stop web-volume && docker rm web-volume
docker run -d -p 8080:80 --name web-copy nginx
docker cp index.html web-copy:/usr/share/nginx/html/index.html
```





# MySQL et PhpMyAdmin avec docker run

```
docker pull mysql:5.7
docker pull phpmyadmin/phpmyadmin
docker network create tp-net
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=test --network tp-net mysql:5.7
docker run -d --name phpmyadmin -p 8082:80 --network tp-net -e PMA_HOST=mysql phpmyadmin/phpmyadmin
```












