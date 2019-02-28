# Autopsy

![](https://images.gr-assets.com/misc/1535611813-1535611813_goodreads_misc.gif)

## Usage

```
$ docker-compose up
```


## Persistance de la clé

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
$ docker-compose run airflow python -c "from cryptography.fernet import Fernet; FERNET_KEY = Fernet.generate_key().decode(); print(FERNET_KEY)
```

