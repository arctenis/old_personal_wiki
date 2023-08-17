# Dockeriser une application avec Django, Postgres, Gunicorn et Nginx

## Prérequis

- Docker
- Docker Compose
- Python 3.6 ou supérieur

## Créer le projet

Créez un nouveau répertoire pour votre nouveau projet Django.

```bash
mkdir django_docker_gunicorn
cd django_docker_gunicorn
mkdir app
cd app
python -m venv .venv --prompt=django
source .venv/bin/activate
pip install -U pip
pip install django
django-admin startproject core .
pip freeze > requirements.txt
python manage.py migrate
python manage.py runserver
```

Visitez http://localhost:8000/ pour vérifier que le projet a bien été créé.

N'oubliez pas de supprimer le fichier *db.sqlite3*.

Votre répertoire devrait ressembler à ceci :

```bash
django_postgres_gunicorn_nginx
└── app
    ├── core
    │   ├── asgi.py
    │   ├── __init__.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    └── manage.py
```

## Docker

Créer un fichier `Dockerfile` dans le répertoire *app*.

```dockerfile
FROM python:3.11.4-slim-buster

WORKDIR /usr/src/app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN pip install -U pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

COPY . .
```

Détaillons ce fichier :

- Les images python slim-buster sont des images légères de python. Elles ne
  contiennent que le strict minimum pour faire fonctionner python.
 
- La commande `WORKDIR` permet de définir le répertoire de travail pour toutes
  les futures instructions RUN, CMO, ENTRYPOINT, COPY et ADD.
  https://docs.docker.com/engine/reference/builder/#workdir

- La variable d'environnement `PYTHONDONTWRITEBYTECODE` permet de ne pas
  générer de fichiers .pyc.
  https://docs.python.org/3/using/cmdline.html#envvar-PYTHONDONTWRITEBYTECODE
 
- Et `PYTHONUNBUFFERED` permet de ne pas mettre en cache les sorties de stdout
  et stderr.
  https://docs.python.org/3/using/cmdline.html#envvar-PYTHONUNBUFFERED

- Puis, on met à jour *pip*, on copie le fichier *requirements.txt* et on
  installe les dépendances.

- Enfin, on copie le reste du projet.

Ajoutez un fichier `compose.yaml` à la racine du projet, à côté du répertoire `app`.

> Attention ! A partir de juillet 2023, Compose V1 ne sera plus supporté. Vous
> trouvez ici des informations légèrement différentes de ce qui vous pouvez
> voir ailleurs, dans d'autres guides pas forcément à jour.
> https://docs.docker.com/compose/

```yaml
services:
  web:
    build: app
    command: python manage.py runserver 0.0.0.0:8000
    ports:
      - '8000:8000'
``` 

Détaillons ce fichier :

- `services` est la clé principale du fichier. Elle contient la liste des services
qui seront créés.

- `web` est le nom du service. Il est arbitraire.

- `build` permet de construire une image à partir d'un Dockerfile. Ici, on lui 
donne le chemin vers le répertoire `app`.

- `command` permet de lancer une commande. Ici, on lance le serveur de développement 
de Django.

- `ports` permet de mapper un port du conteneur vers un port de la machine hôte.

## Postgres

Nous allons maintenant ajouter une base de données Postgres à notre projet.

Installez le module `psycopg2`. Psycopg2 est un adaptateur de base de données
PostgreSQL pour le langage de programmation Python. Il permet aux programmes
Python de faire des requêtes SQL vers une base de données PostgreSQL.

> psycopg2-binary est une version précompilée de psycopg2. Elle est plus facile
> à installer que psycopg2, mais elle est plus lourde. Vous pouvez utiliser
> psycopg2 à la place si vous le souhaitez.


```bash
pip install psycopg2-binary
pip freeze > requirements.txt
```




