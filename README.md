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

Création du fichier `docker-compose.yml` 

**Questions :**

## a. Qu’apporte le fichier `docker-compose.yml` par rapport aux commandes `docker run` ?

### Lisibilité et maintenabilité
- Centralisation de la configuration (images, ports, variables d’environnement, réseaux…)
- Versionnable avec Git

### Execution simplfié
- Tous les conteneurs sont lancés avec une seule commande : `docker-compose up`

### Dépendances entre services
- Gestion des réseaux, volumes, ordre de démarrage et liens entre services

### Exemple :

**Sans compose** :
```bash
docker run -d --name mysql ...
docker run -d --name phpmyadmin ...
```

**Avec compose** :
```bash
docker-compose up -d
```

---

## b. Quel moyen permet de configurer (utilisateur, base, mot de passe root…) MySQL au lancement ?

C’est fait grâce aux **variables d’environnement** utilisées dans `docker-compose.yml` :

```yaml
environment:
  MYSQL_ROOT_PASSWORD: root       # Mot de passe utilisateur
  MYSQL_DATABASE: test            # Base de données créée
```

> Ces variables sont interprétées automatiquement par l’image `mysql` au démarrage.

**Cela évite d’avoir à écrire manuellement des commandes SQL d’initialisation !**




# Question 9 

## Lancement du compose de la question 9 

```
docker compose -f question9.yml up -d
```

## ping 

Connexion à la partie web 

```
docker exec -it 162 bash
```

Ping de app et de db 

```bash
ping app 
ping db 
```
**Le ping vers app fonctionne** 
**Le ping vers db de fonctionne pas**

### Analyse via docker inspect

On utilise docker inspect pour vérifier les networks présents 
```
docker inspect web 
docker inspect app 
docker inspect db 
```
On remarque que:
web à accés uniquement au front 
app au front et au back 
db uniquement au back 

## Cas d'usage 
Dans une appli web 
On peut utiliser :
-Le front avec Nginx (web)
-Le front et le back pour lier le web et la db avec php par exemple (app)
-Le back avec Mysql (DB)

Cette configuration permet d'isoler les différentes parties de l'application,
avec plusieurs avantages tels que la sécurité,
empêcher l'accès à la base de données depuis le web,
et permettre de modifier l'application ainsi que de changer certains éléments plus facilement,
en rendant l'application plus "modulaire"

