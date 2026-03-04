# abes-wud-docker
Contient la configuration du [WUD (aka What's up Docker?)](https://getwud.github.io/wud/#/) déployé sur un nœud docker à l'Abes qui permet la mise à jour des conteneurs

## Installation

```bash
cd /opt/pod
git clone https://github.com/abes-esr/abes-wud-docker.git
cd abes-wud-docker

cp .env-dist .env
```
Personnaliser ensuite les variables souhaitées dans le .env, en particulier :
 - ABES_WUD_VERSION
 - ABES_WUD_PORT
 - ABES_WUD_DOCKERHUB_USER
 - ABES_WUD_DOCKERHUB_PASS
 - ABES_WUD_SLACK_TOKEN
 - ABES_WUD_SLACK_CHANNEL
 - ABES_WUD_SLACK_TITLE

## Démarrage et arret

```bash
# pour démarrer
cd /opt/pod/abes-wud-docker/
sudo docker compose up -d

# pour stopper
cd /opt/pod/abes-wud-docker/
sudo docker compose stop

# pour voir les logs
cd /opt/pod/abes-wud-docker/
sudo docker compose logs -f --tail=50
sudo docker compose logs -f --since 5m
```

## Sauvegardes et restauration

L'unique fichier à sauvegarder et à restaurer est le fichier ``/opt/pod/abes-wud-docker/.env`` qui contient les info pour le déploiement.
En cas de perte de ce fichier, il peut également relativement facilement être recréé depuis zéro car il ne contient aucune informations qu'on ne pourrait pas reconstituer sans les sauvegardes (ex: numéro de version, token slack)

## Mise à jour

```bash
cd /opt/pod/abes-wud-docker/
sudo docker compose pull
sudo docker compose up -d
sudo docker image prune -f
```
