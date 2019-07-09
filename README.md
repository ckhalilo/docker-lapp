Création d'environnement Docker LAPP
====
*Traduit en Français, voir l'originale dans akira345/docker-lapp*

Docker LAPP : Acronyme de Linux Apache Postgresql PHP est script pour monter son environnement de dev
====
__Dernière mise à jour__: Problèmes résolu (mcrypt, zip, apache HostName)


Il continent PHP7 Adminer PostgreSQL9.6

composer est installer 

```bash
git clone https://github.com/ckhalilo/docker-lapp.git
cd docker-lapp/
docker-compose up -d
```

adminer est le gestionnaire de Postgresql au lieu de phpPgAdmin

On peut le consulter via /adminer

|    |    |
|---------|---------|
|Serveur|PostgreSQL|
|Base de donnée|pgsql|
|Nom utilisateur|postgres|
|Mot de passe|passwd|

Si vous voulez accéder a docker, utiliser composer, etx

```bash
docker exec -it <ID du conteneur> bash
```

