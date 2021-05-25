# Map+

Map+ is the geographic visualization of all the ongoing missions of an agency.
It allows the agency director to have a clear view of how the workload is distributed within his team.
This view will improve in the long term, to have a better organization of the zones covered by an agency and thus reduce the time and costs of everyday transport.

Table of Contents
-----------------

#### Introduction

- [Prerequisites](#prerequisites)

#### The application

- [Get started](#get-started-with-the-Application)
- [The architecture](#the-architecture)
- [The important files are](#the-important-files-are)
- [Running the MariaDB database](#running-the-postgresql-database)
- [The crontab](#the-crontab)
- [Deployment](#deployment)
- [Logs stream](#logs-stream)

Prerequisites
---------------

These are the dependancies you'll need : 

### 1. First step

* [DOCKER](https://www.docker.com/products/docker-desktop) -
* [VISUAL STUDIO CODE](https://code.visualstudio.com) -
* [GIT](https://git-scm.com) -

Launch Docker now !

### 1. Basic Workflow ./ IMPORTANT !

The workflow here is pretty simple :

1) Clone the repository
2) Create a new branch
```
git checkout -b feat/NEW_FUNCTIONNALITY_NAME
```
4) Add your functionnality
3) When your done don't forget to create a Pull Request with your branch and the Master one.
4) Don't forget to had some reviewers to your Pull Request.

### 1. Set up Env

To setup env create a .env file and use the template in the file .env.dist :
```
/* Template for .env */
/*                   */
/*                   */

/* MariaDB local docker */

MARIADB_DB_PASSWORD=
MARIADB_DB_USERNAME=
MARIADB_DB_HOST=
MARIADB_DB_PORT=
MARIADB_DB_NAME=

/* Template for .env */

SALESFORCE_USER=
SALESFORCE_PASSWORD=
SALESFORCE_SECURITY_TOKEN=
SALESFORCE_DOMAIN=
```

Ask team for password !

Get started
---------------

### 1. Run the docker-compose 

```
docker-compose -f docker-compose.dev.yml up -d
```

you can access application at URL :
	# Jupyter : http://jupyter.localhost
	# Voila : http://voila.localhost
	# PhpMyAdmin : http://pma.localhost

The architecture
---------------

### 1. The stack

* [DOCKER](https://www.docker.com/products/docker-desktop) - 
* [ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html) - 
* [TRAEFIK](https://doc.traefik.io/traefik/) -
* [TRAEFIK_AUTH](https://github.com/thomseddon/traefik-forward-auth) -

### 2. Basic description

Application are conteneurized, only the voila container are deployed in Staging or Production, Jupyter is use only in developpement.
The application is deployed by Terraform see [documentation](https://www.docker.com/products/docker-desktop) for more info about it.

The github Action are here to trigger the deployment

### 3. Use case / DAT / more complex view :

DAT : * [DAT](https://www.docker.com/products/docker-desktop) - 
DEX * [DEX](https://www.docker.com/products/docker-desktop) - 

The important files are
---------------

### 1. * [docker-compose.dev.yml](https://www.docker.com/products/docker-desktop) -
### 2. * [Dockerfile](https://www.docker.com/products/docker-desktop) -
### 3. * [start-voila.sh](https://www.docker.com/products/docker-desktop) -
### 4. * [cron_import_data.sh](https://www.docker.com/products/docker-desktop) -

Running the MariaDB database
---------------

### 1. MariaDB is a part of the docker-compose 

As MariaDB is integrated to the docker-compose you don't need to do anything here simply run the docker-compose see : [Prerequisites](#prerequisites)

### 2. Use case

In developpement (docker) the password for the MariaDB is set to : exemple
you can access the mariadb on port 3306.
For mariadb logs just run :
```
docker logs MARIADB_CONTAINER_ID
```

### 2. PhpMyAdmin

If you want a more visual eye on the DB, you can acces a PhpMyAdmin with the url : http://pma.localhost

The crontab
---------------

The crontab is pretty important, is job are to update data to salesforces, and regenerate Notebook
Two files are important here :
	- [cron_import_data.sh](https://www.docker.com/products/docker-desktop)
	- [import_data_on_start.sh](https://www.docker.com/products/docker-desktop)
	- [import_data.ipynb](https://www.docker.com/products/docker-desktop)

The crontab is executed every 6 hours and executed on start.

Deployment
---------------

* [TERRAFORM](https://www.docker.com/products/docker-desktop) -
* [GITHUB ACTIONS](https://www.docker.com/products/docker-desktop) -

See [documentation](https://www.docker.com/products/docker-desktop) for more info about it.

Logs stream
---------------

### 1. Main Log stream

the main log stream for voila or the other container like Jupyter or Mariadb is accesible via a simple :
```
docker logs CONTAINER_ID
```

to get CONTAINER_ID juste simply run :
```
docker ps
```

### 2. Cron Log stream

The cronjob will go on the main log stream see (#logs-stream) for more details

If you want to check logs on container you can access it with :
```
docker exec -it CONTAINER_ID /bin/bash
cd /var/etc/log
cat cron.log
```
