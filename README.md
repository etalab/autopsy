# Autopsy

![](https://images.gr-assets.com/misc/1535611813-1535611813_goodreads_misc.gif)

Ce dépôt contient un ensemble de fichier de configuration docker permettant l'instanciation d'un service de consultation de notebooks python et l'automatisation périodique d'exécution de ces notebooks.

## Usage

```
$ docker-compose up
```

- http://localhost:4000 : interface de consultation statique des notebooks avec [commutter](https://github.com/nteract/commuter)
- http://localhost:8080 : interface d'administration d'[Airflow](https://airflow.apache.org/)

Pour des raisons de sécurité, Airflow est accessible seulement localement. Pour y avoir accès à distance, la méthode préconisée est de faire un pont avec ssh (e.g. `ssh -L 8080:localhost:8080`).

## Workflow

wip

## Persistance de la clé de chiffrage

Par défaut, une nouvelle clé est crée à chaque démarrage de l'image. Afin de faire persister la clé, il faut ajouter un fichier `docker-compose.production.yml` avec le contenu suivant :

```
version: '2.1'
services:
    airflow:
        environment:
            - AIRFLOW__CORE__FERNET_KEY={VOTRE CLÉ}
```

et démarrer les services avec la commande suivante :

```
$ docker-compose -f docker-compose.yml -f docker-compose.production.yml up
```

Il est possible de créer une clé avec la commande suivante :

```
$ docker-compose run airflow python -c "from cryptography.fernet import Fernet; FERNET_KEY = Fernet.generate_key().decode(); print(FERNET_KEY)"
```

## nbviewer

```
$ docker-compose -f docker-compose.yml -f docker-compose.nbviewer.yml up
```

URL : http://localhost:4010/localfile

## Inspiration

- [Beyond Interactive: Notebook Innovation at Netflix](https://medium.com/netflix-techblog/notebook-innovation-591ee3221233)
