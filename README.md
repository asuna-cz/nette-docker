## Installation

```
git clone git@github.com:asuna-cz/nette-docker.git
cd nette-docker

docker run --rm --interactive --tty \
  --volume $PWD/app/:/app \
  --user $(id -u):$(id -g) \
  composer create-project nette/web-project .

chmod a+w app/temp/ app/log/

docker-compose up --build
```

`docker-compose up -d` to run in background

## Config

Setup your own password to database in `docker-compose.yml`

```
  docker-compose.yml
  ...
  image: mariadb
  environment:
    MYSQL_DATABASE: DB_NAME
    MYSQL_USER: DB_USER
    MYSQL_PASSWORD: DB_PASSWORD
    MYSQL_ROOT_PASSWORD: DB_ROOT_PASSWORD
  volumes:
  ...
```

It's also very easy to swap MySQL for MariaDB  \
`image: mysql`

## Possible problems
> Got permission denied ... /var/run/docker.sock: connect: permission denied

Make sure your $USER variable is set ( `echo $USER` ) otherwise just replace `$USER` with your username.

1) `sudo usermod -aG docker $USER` 
2) `logout & login`
3) `sudo systemctl restart docker`

> docker-compose: command not found

Make sure you have docker-compose installed. You can install docker and docker-compose like this. Assuming you are using APT.

`sudo apt update` \
`sudo apt install docker.io docker-compose`

> something is blocking port 80/8080

Change ports in `docker-compose.yml` or stop apps using those ports. That will most likely be Apache or Nginx server.

`sudo systemctl stop apache2` \
`sudo systemctl stop nginx`

> Adminer: SQLSTATE[HY000] [2002] php_network_getaddresses: getaddrinfo failed: Name does not resolve

In adminer change `server` to `database` instead of `db` while logging in.

## What next?

Well, you have installed LEMP stack in docker with [Nette Framewok](https://nette.org/) and you are ready to build something awesome. \
You can find Nette docs [here](https://doc.nette.org/en/3.0/) \
By default nginx is running on port 80: [localhost](http://localhost) and [adminer](https://www.adminer.org/) on [http://localhost:8080](http://localhost:8080)
