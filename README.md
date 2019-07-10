Création d'environnement Docker LAPP
====

*Fork de la version akira345/docker-lapp*

#### Docker LAPP : Acronyme de Linux Apache Postgresql PHP est script pour monter son environnement de dev

__Dernière mise à jour__: 
* Problèmes résolu (mcrypt, zip, apache HostName)
* Isoler adminer dans un contenaire
* Ajouter networks (Relation Réseau)


Il continent PHP7 Adminer PostgreSQL

composer est installer 

```bash
git clone https://github.com/ckhalilo/docker-lapp.git
cd docker-lapp/
docker-compose up -d
```

adminer est le gestionnaire de Postgresql au lieu de phpPgAdmin

On peut le consulter via http://127.0.0.1:8080

|    |    |
|---------|---------|
|Serveur|pgsql|
|Nom utilisateur|postgres|
|Mot de passe|passwd|

Si vous voulez accéder a docker, utiliser composer, etx

```bash
docker-compose exec php bash
```

