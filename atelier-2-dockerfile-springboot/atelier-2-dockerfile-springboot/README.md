# Atelier 2 — Dockerfile et Spring Boot

Reprend l'atelier "Atelier sur Dockerfile et SpringBoot" (EFREI Paris).

## Contenu déjà prêt dans ce dossier

- `pom.xml` — dépendances Spring Boot Web + Test
- `DockerDemoApplication.java` — contrôleur REST qui répond "Hello, World!" sur `/`
- `DockerDemoApplicationTests.java`
- `Dockerfile`
- `.gitignore`

## 1. Prérequis (à vérifier de votre côté)
- **Docker** installé : https://docs.docker.com/get-docker/
- **Compte Docker Hub** : https://hub.docker.com
- **Maven** et **JDK 17** installés sur votre machine

## 2. Récupérer le projet sur votre machine
Si vous travaillez à partir d'un repository GitHub existant (cf. atelier 1) :
```bash
git clone https://github.com/<votre-utilisateur>/<votre-repo>.git
cd <votre-repo>
```
Sinon, copiez simplement ce dossier `atelier-2-dockerfile-springboot` sur votre machine.

## 3. Lancer les tests et construire le .jar
```bash
mvn test
mvn clean package
```
Cela génère un fichier `.jar` dans le répertoire `target/` (ex : `docker-demo-0.0.1-SNAPSHOT.jar`).

## 4. Construire l'image Docker
À la racine du projet (là où se trouve le `Dockerfile`) :
```bash
docker build -t votre-nom-utilisateur-dockerhub/springboot-app .
```
Remplacez `votre-nom-utilisateur-dockerhub` par votre nom d'utilisateur Docker Hub.

Vérifiez que l'image a bien été créée :
```bash
docker images
```

## 5. Tester l'image localement
```bash
docker run -p 8080:8080 votre-nom-utilisateur-dockerhub/springboot-app
```
Ouvrez ensuite http://localhost:8080 dans votre navigateur : vous devez voir **"Hello, World!"**.

## 6. Se connecter à Docker Hub
```bash
docker login
```
Entrez votre nom d'utilisateur et mot de passe Docker Hub.

## 7. Pousser l'image vers Docker Hub
```bash
docker tag votre-nom-utilisateur-dockerhub/springboot-app votre-nom-utilisateur-dockerhub/springboot-app:latest
docker push votre-nom-utilisateur-dockerhub/springboot-app:latest
```

## 8. Vérifier l'image sur Docker Hub
1. Allez sur https://hub.docker.com.
2. Connectez-vous à votre compte.
3. Accédez à votre profil → vous devez voir `springboot-app` dans la liste de vos repositories.

Vous avez maintenant une image Docker contenant votre application Spring Boot, prête à être déployée sur n'importe quel serveur avec Docker installé.
