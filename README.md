In dieser Datei stehen die einzelnen Schritte zur Demo

# Version prüfen

`docker -v`

# MariaDB & Adminer

## MariaDB im CLI

Führt den Container aus:

` docker run --detach --name demo-mariadb --env MARIADB_USER=demo-user --env MARIADB_PASSWORD=my_password --env MARIADB_ROOT_PASSWORD=very_secure_password mariadb`

Zeigt alle Container an:
`docker ps`

In die Kommandozeile des Containers wechseln:
`docker exec -it demo-mariadb bash`

Zugriff auf die My-SQL Shell:
`mysql -u demo-user -p`

Beispiel-Befehl:
`show databases;`

Shell verlassen:
`exit`

Container stoppen:
`docker stop demo-mariadb`

Alle Container anzeigen, auch gestoppte:
`docker ps -a`
## Adminer verknüpfen

Image herunterladen:
`docker pull adminer`

Container vom Image starten:
`docker run --link demo-mariadb --name adminer -p 8080:8080  adminer`

Adminer im Browser öffnen: http://localhost:8080
> Anmeldendaten: demo-mariadb, demo-user, my_password

Clean Up:
`docker stop demo-mariadb && docker rm demo-mariadb && docker stop adminer  && docker rm adminer`

## Compose

> Check: Im Order mariadb "stehen"

Start:
`docker-compose up`

Adminer im Browser öffnen: http://localhost:8080
> Anmeldendaten: mariadb-db-1, demo-user, my_password

Stoppen: 
`docker-compose down`

Cleanup:
`docker rm mariadb-db-1 && docker rm mariadb-adminer-1`

# Vue.je und Go

## Lokal

Starten des HTTP-Severs lokal:
`npm run serve`
Verfügbar auf localhost:8080

## Image builden

`docker build -t antonengelhardt/my-vue-app .`

## Container vom Image starten

`docker run -it --name my-vue-app -p 8080:8080 antonengelhardt/my-vue-app`

## Push zu DockerHub

> Der Name des Images muss verändert werden und vorher der Login durchgeführt werden:

`docker login`

`docker push antonengelhardt/my-vue-app`

## Image herunterladen

`docker pull antonengelhardt/my-vue-app`

Clean Up:

`docker stop my-vue-app && docker rm my-vue-app`