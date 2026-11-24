# TP4 : Docker et Docker Compose (Application MERN)


## Architecture du projet

- `Server/` : API Express (port `9000`)
- `Client/` : Application React servie avec `serve` (port `3000`)
- `mongodb` : Base de données MongoDB
- `docker-compose.yml` : Orchestration des 3 services sur le réseau `mern-network`
- `Jenkinsfile` : Pipeline CI/CD Jenkins

## Ce qui a été réalisé

1. **Conteneurisation du serveur (`Server/Dockerfile`)**
   - Image de base `node:lts-alpine`, installation des dépendances avec `npm install`, exposition du port `9000` et démarrage via `npm start`.
   - Connexion à MongoDB à travers la variable d'environnement `MONGO_URI`.

2. **Conteneurisation du client (`Client/Dockerfile`)**
   - Image de base `node:lts-alpine`, installation des dépendances, génération du build React (`npm run build`), installation du serveur léger `serve` et exposition du port `3000`.

3. **Mise en réseau et orchestration (`docker-compose.yml`)**
   - Création du réseau `mern-network` (driver `bridge`) permettant au serveur de communiquer avec MongoDB via le nom de service `mongodb` (`MONGO_URI=mongodb://mongodb:27017/mern`).
   - Lancement de l'ensemble de l'application avec `docker compose up -d --build`.

4. **Automatisation avec Jenkins (`Jenkinsfile`)**
   - Récupération automatique du code depuis GitHub.
   - Construction des images Docker `mern-server` et `mern-client`.
   - Publication des images sur Docker Hub.
   - Déploiement automatique des conteneurs via Docker Compose.

## Accès à l'application

- Frontend React : http://localhost:3000
- Backend Express : http://localhost:9000

## Liens

- Dépôt GitHub : https://github.com/zouhour-hub/MyAppReact
- Image Docker Hub (Server) : https://hub.docker.com/r/zouhourzramdini/mern-server
- Image Docker Hub (Client) : https://hub.docker.com/r/zouhourzramdini/mern-client