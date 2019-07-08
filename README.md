
[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

# Contexte du projet

## Point de départ

<img src="https://www.monprojetpourlaplanete.gouv.fr/media/cache/default_profile/default/0001/01/3b76a871f1976cf21fcdfb9b4dea828ce98c1828.png" alt="Sunshare Logo" align="right" style="margin-right: 25px" height=130></a>
Dans le cadre d'un projet d'expérimentation pour l'école IMIE, le projet "Sunshare" nous a été soumis.
Pour bien comprendre l'existant voici quelques liens :
1. [Contexte du projet & Consignes](http://imie.sunshare.fr/)
2. [Projet de base sur Git (Serious Game)](https://github.com/sunsharebox) <img src="https://github.blog/wp-content/uploads/2013/04/074d0b06-a5e3-11e2-8b7f-9f09eb2ddfae.jpg?resize=1234%2C701" alt="Git Logo" style="margin-top: 5px" height=30></a>
3. [Dashboard, interface locale utilisateur (Boxénergie)](https://github.com/sunsharebox/sunshare-APP)<img src="https://github.blog/wp-content/uploads/2013/04/074d0b06-a5e3-11e2-8b7f-9f09eb2ddfae.jpg?resize=1234%2C701" alt="Git Logo" style="margin-top: 5px" height=30></a>
4. [Connexion en javascript aux capteurs (Boxénergie)](https://github.com/sunsharebox/sunshare-API)<img src="https://github.blog/wp-content/uploads/2013/04/074d0b06-a5e3-11e2-8b7f-9f09eb2ddfae.jpg?resize=1234%2C701" alt="Git Logo" style="margin-top: 5px" height=30></a>


Les objectifs concrets de ce projet sont :
1. Créer une démo fonctionnelle du "Serious Game"
  - Créer une interface utilisateur/équipe/administrateur
  - Créer une base de données utilisateurs
  - Créer une API sur l'interface de développement de la société ENEDIS
  - Création d'un portail sécurisé
  - Création d'un mode simplifié
  - Établir les règles du jeu
2. Améliorer les couches existantes sur la partie Boxénergie
  - Changement graphique de l'interface utilisateur actuelle
  - Connexion en JavaScript avec les capteurs (TIC et compteur à impulsions)
  - Mettre en place l'API ENEDIS pour le point de livraison de l'utilisateur.
  - Création d'une alerte sonore et/ou visuelle
3. Réaliser certaines des fonctionnalités supplémentaires (si le temps nous le permet)
  - Création de compte, nouvel utilisateur
  - Commande de déclenchement électrique (réalisation d'effacement de puissance)


## Architecture

<a href="https://www.raspberrypi.org"><img src="https://www.raspberrypi.org/wp-content/uploads/2012/03/raspberry-pi-logo.png" alt="Raspberry Pi Logo" align="right" style="margin-left: 25px; margin-bottom: 10px" height=100></a>

<p align="justify">
Dans le but de réaliser ce projet l'école nous a fourni deux RaspberryPi V3B+. La demande initiale était d'utiliser ces deux RaspberryPi en tant qu' "utilisateurs". Au vu de la demande de produire un code "écoconception",nous avons choisi de les exploiter de manière différentes. La demande initiale concernait la mise en place d'un serveur MongoAtlas. Au vu de l'implantation des serveurs (US) et de la route de l'ensemble des paquets, il ne nous parrait pas judicieux d'utiliser cette architecture. Nous avons donc utilisé le premier comme base de données No-SQL (MogoDB). Le second est utilisé comme serveur web avec Docker. L'enjeu sur le second est de mettre en place deux containers. Le premier conteneur servira à faire tourner la Boxénergie et le second le Serious Game. L'avantage est de créer un environnement facilement réplicable et simple à mettre en oeuvre. De plus docker étant opensource et adaptable à n'importe quel environnement de développement les différents hackathons suivants ne seront pas pénalisés par le choix d'une technologie fermée.
</p>
[MongoDB](https://www.mongodb.com/)
[Docker](https://www.docker.com/)
### Architecture initiale

Voici un schéma de l'architecture envisagée en sa version initiale :

<p align="center" style="margin-bottom: 10px; margin-top: 30px">
<img src="https://raw.githubusercontent.com/MaximeNico/SunShare/master/ArchitectureV0.png" alt="ArchitectureV0" align="center" style="margin-bottom: 10px; margin-top: 30px">
<em>Architecture V0 </em>
</p>

### Architecture V1
Voici un schéma de l'architecture envisagée(V1) :

<p align="center" style="margin-bottom: 10px; margin-top: 30px">
<img src="https://raw.githubusercontent.com/MaximeNico/SunShare/Kevin/Ressources%20graphique/ArchitectureV1.png" alt="ArchitectureV1" align="center" style="margin-bottom: 10px; margin-top: 30px">
<em>Architecture V1 </em>
</p>

### Architecture V2

<p align="justify">
Cette architecture est l'architecture finale pour le projet. Nous concervons l'utilisation de docker pour conserver l'indépendance des services. Un service sera dédié au serious game et l'autre à la partie Boxénergie. Cette architecture se veux autonome. Si le service Serious Game ne fonctionne pas pour cause de défaut de connexion internet, le service Boxénergie continuera lui de fonctionner. La réciproque est vraie. Il y aura également une base locale pour la Boxénergie (partie TIC et compteur à impulsions). Cette base sera liée au mode dégradé (off-line) si l'utilisateur ne veux pas participer au serious game.
</p>

Voici un schéma de l'architecture retenue pour le projet(V2) :

<p align="center" style="margin-bottom: 10px; margin-top: 30px">
<img src="https://raw.githubusercontent.com/MaximeNico/SunShare/Kevin/Ressources%20graphique/ArchitectureV2.png" alt="ArchitectureV1" align="center" style="margin-bottom: 10px; margin-top: 30px">
<em>Architecture V2 </em>
</p>

# Serious Game

## Création des visuels
Pour cette partie il nous a été demandé de créer deux interfaces graphiques distinctes :
- Une dédiée à l'utilisateur
- Une dédiée à l'équipe
### Page  utilisateur

Voici la maquette de la page :
<p align="center" style="margin-bottom: 10px; margin-top: 30px">
<img src="https://raw.githubusercontent.com/MaximeNico/SunShare/develop/ressource/Web%201920%20%E2%80%93%20Interface%20utilisateur%20(Dashboard).png" alt="Maquette User" align="center" style="margin-bottom: 10px; margin-top: 30px" height = 500>
</p>
Cette page comprend un menu, des encarts de conseil pour améliorer son score et des graphiques.

### Page groupes
Voici la maquette de la page :
<p align="center" style="margin-bottom: 10px; margin-top: 30px">
<img src="https://raw.githubusercontent.com/MaximeNico/SunShare/develop/ressource/Web%201920%20%E2%80%93%20Interface%20utilisateur%20(TeamBoard).png" alt="Maquette Team" align="center" style="margin-bottom: 10px; margin-top: 30px" height = 500>
</p>
Cette page comprend le classement de son équipe avec le podium de l'équipe et un classement global avec l'affichage des 3 meilleures équipes.

## Base de données

En attente d'éléments de Nico

## API ENEDIS

<p align="justify">
La société ENEDIS souhaite disposer d'une IP fixe pour envoyer ses données vers un serveur. Le matériel mis à disposition par l'école ne nous permet pas de réaliser cette demande. Deux solutions sont alors possible :

- L'entreprise Sunshare met en place un serveur OVH commum à l'ensemble des groupes. Cette initiative permet d'ouvrir une base de données MongoDB avec une IP fixe. De part la nature des bases No-SQL, l'entreprise Sunshare pourra créer une collection par groupe et ainsi rendre autonome chacun des groupes.

- La première possibilité n'est pas possible à mettre en place. Dans ce cas nous prendrons l'initiative d'utiliser une infrastructure personnelle avec le raspberrypi dédié à la base de données (DBPI).
</p>

### Choix final ?

- [x] solution 1 (validé le 05/07/19)
- [ ] solution 2

## Portail sécurisé

Afin d'éviter la mise en place de technique douteuse pour flouer le système nous avons mis en oeuvre plusieurs items :

- <p align="justify">A la création du compte utilisateur récupération de l'ID du point de livraison (Identifiant du compteur). Cet identifiant sera stocké en base. Il ne peux y avoir deux numéro de compteur identique. A la création du compte nous interrogerons la base des compteurs pour savoir si celui-ci n'existe pas dans la base. Le cas échéant l'utilisateur ne pourra pas créer son compte. Il pourra utiliser les fonctions locales du raspberrypi mais ne pourra pas participer au Serious Game.</p>

- <p align="justify">Pour éviter la modification des consommations et/ou production, on comparera les valeurs de références reçues par Enedis. On positionnera un seuil de tolérance avec la valeur certifiée par ENEDIS. Si l'écart est trop important les données locales ne seront pas prise en compte mais seulement les données ENEDIS</p>


## Création d'un mode simplifié

<p align="justify">On distingue deux types d'utilisateurs pour le Serious Game. Une première catégorie utilise à la fois la Boxénergie et le Serious Game. Pour répondre à l'utilisation de la Boxénergie l'utilisateur doit à minima posséder une insallation de panneau solaire et disposer d'un contrat de revente pour son électricité. Si l'utilisateur ne répond pas à cela il a alors la possibilité de créer un compte uniquement pour le Serious Game. Il pourra ainsi participer au jeu et rapporter des points à son équipe sans passer par la Boxénergie. L'ensemble des points seront collectés à travers les divers challenge que nous verrons dans la partie suivante.</p>

## Établir les règles du jeu

<p align="justify">Dans une logique vertueuse pour l'environnement un principe de challenges et d'objectifs seront mis en place. On distinguera deux catégories. Ceux possédant la Boxénergie auront accès à l'ensemble des challenges et objectifs. Pour les utilisateurs en mode simplifié seul certains challenges et objectifs seront possibles.</p>

## Règles soumisses

### Tirelire solaire
Les joueurs disposant de panneaux solaires effectuent un total annuel/mensuel/quotidien de leur production / consommation d’énergie.
La tirelire décompte les kwh soutirés (-) et injectés (+) sur le réseau.

Pour les foyers n’ayant pas de toiture solaire, on devra construire un autre mode de jeu (voir plus bas).

### Concours d’autoconsommation
On lance un défi sur plusieurs semaines auprès de tous les joueurs qui réussirons à transférer leur profil de consommation dans les périodes de production solaire.
On minimise le ratio entre énergie soutirée du réseau et énergie totale consommée en la période précédant le jeu et la période de jeu.

Malus : pour les foyers consommant beaucoup d’électricité par individu.

### Défis d’économie d’énergie
Dans cette partie, les économies d’énergie sont réparties par domaines (chauffage, eau chaude, appareils électriques,…) et chaque joueur part de sa situation actuelle et engage des actions qui le font avancer dans le jeu. On atteint un niveau lorsque qu’on a effectué une grappe d’actions dans chaque domaine. Exemple :

- Niveau 1 : Sobriété (conseils de grand mère) - baisser la température du logement à 19°C et 15°C en cas d’absence, mettre des mousseurs pour économiser l’eau chaude, dégivrer son congélateur une fois par an, brancher ses appareils sur des multiprises à interupteur, fermer les volets la nuit, éteindre la clim l’été, jeter toutes les lampes halogènes du foyer…
- Niveau 2 : Efficacité 1 (investissement modéré) : investire dans un thermostat d’ambiance programmable, raccorder ses équipements ménagers sur l’eau chaude centrale, supprimer 1 appareil de plus de 1000W (micro-onde, four, plaque induction, grille pain, seche linge, seche cheveux …),
- Niveau 3 : Efficacité 2 : Remplacer son chauffe eau (par un solaire, gaz ou thermodynamique), inverstir dans un poele à bois
- Niveau 4 : isoler ses combles et ses murs en BBC rénovation
- Malus : changer les fenètres sans isoler vos murs vous fait perdre des points, acheter une piscine chauffée…

## Règles créées

### Effacement de puissance

<p align="justify">Une des fonctionnalités supplémentaire est de pouvoir faire commuter des relais de puissance. Grâce à cette fonctionnalité et en ayant renseigner la puissance active des appareils connectés sur ce relais nous serions capable de calculer la puissance effacée sur le réseau. En fonction de la puissance totale effacée, de la période et du temps d'effacement l'utilisateur reporterai plus ou moins de points. Nous savons que les pics de puissance se produissent le soir aux alentours de 19h. Si l'utilisateur efface une grande partie de sa puissance à ce moment précis alors il remportera un maximum de point. On y appliquera un coefficient multiplicateur. Après une heure d'effacement passe en x2, si effacement à des heures "pic" x3, etc</p>

### Autres ???

# EnergyBox

Développement sur la deuxième semaine.

## Changement graphique de l'interface utilisateur actuelle

Soon...

## Connexion en JavaScript avec les capteurs (TIC et compteur à impulsions)

Soon...
Préparer les éléments (GCE Electronics USB TIC & GPIO compteur à impulsions)

## Mettre en place l'API ENEDIS pour le point de livraison de l'utilisateur.

Soon...

## Création d'une alerte sonore et/ou visuelle

Soon...

## Boitier 3D

<p align="justify">Pour répondre à la demande du boitier du raspberry pi, il y'a deux solutions possible. La première étant la conception d'un boitier imprimable en série par une entreprise. La seconde est la réalisation d'un boitier par une imprimante 3D. Pour répondre à la seconde solution nous pouvons partir d'un [modèle existant](https://www.thingiverse.com/make:529106) qui répondra à la demande. Pour y greffer le buzzer il reste suffisament de place dans le boitier pour en intégrer un. POur répondre à la demande de l'éco-conception on imprimera la pièce en [PLA](http://www.green-desk.net/le-pla-cest-quoi/). Ce boitier permettra à l'utilisateur, grâce à l'écran, de visualiser directement les dashboards. Cette option reste la plus "propre" et écologique.</p>

# Réalisation

## Installation et configuration des Raspberrypi

<p align="justify">Pour commencer il faut installer Raspbian (distrubution Linux pour le raspberry). Pour ce faire, rendez-vous [ici](https://www.raspberrypi.org/downloads/raspbian/) et télécharger la version lite.
Une fois le .zip téléchargé ne pas de le dézipper.
Télécharger [Ethcer](https://www.balena.io/etcher/) pour monter l'iso sur la carte SD.
Créer un fichier 'ssh' sans extension sur la racine boot pour initialiser la connexion SSH.
Une fois termniné mettre la carte dans le slot SD prévu sur le raspberrypi.

Se connecter en SSH sur le raspberrypi (Mac OS et Linux pas de logiciel additionnel nécessaire).

Si vous êtes sous windows télécharger la dernière version de [putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

Une fois connecté mettre à jour la dernière version des paquets avec la ligne :</p>

```
sudo apt-get update && sudo apt-get upgrade
```
Répéter l'opération pour le second raspberrypi

### Partie base de données

**EDIT : Cette partie n'est plus nécessaire avec la mise en place sur le serveur OVH.**

Pour installer la base de données il faut faire les commandes suivantes :

```
sudo apt install mongodb
sudo systemctl enable mongodb
```

Pour tester si la base est bien active effectuer la commande :

```
mongo
```

Voila pour la partie base de données :thumbsup:

EDIT : Cette partie n'est plus nécessaire avec la mise en place sur le serveur OVH.

### Partie serveur web (Docker)

Commencer par installer la dépendance ffi :

```
libffi-dev
```

Pour installer Docker et Docker-compose utiliser les ligne suivantes :
```
sudo apt install docker-ce
sudo usermod -aG docker pi
sudo apt-get install -y python python-pip
sudo pip install docker-compose
```

Nico la suite pour les deux composants

Voila pour la partie docker :thumbsup:

## Base de données MongoDB sur serveur OVH

Soon...

## Mise en oeuvre de l'API Enedis

<p align="justify">Pour mettre en oeuvre l'API Enedis il est nécessaire de posséder un compte sur le site [data-collect](https://datahub-enedis.fr/data-connect/)

Après inscription, il faut créer une application. Plusieurs étapes sont nécessaire :
- Renseigner le nom de l'application
- Renseigner la description de l'application
- L'adresse de redirection des données (Redirect URI), attention ça doit être une IP fixe uniquement :heavy_exclamation_mark:
- Fournir une illustration de l'application (favicon), elle pourra être modifiée plus tard.
- Données souhaitées, affichées au client
- Un email de contact
- Un numéro de téléphone portable

L'inscription terminée, il faut renseigner les développeurs actifs qui travailleront sur le sujet. Attention l'acceptation d'Enedis est très longue ! :zzz::zzz::zzz:

Le fait de renseigner les développeurs permet de concevoir l'API dans un bac à sable. Les développeurs peuvent ainsi tester et développer l'ensemble de l'API avant la mise en production.</p>

### Test bac à sable

#### Consentement client et token
En premier lieu il faut récupérer le consentement client matérialisé par un "code" pour ce faire il faut renseigner les éléments dans l'URL suivante :
```
https://gw.hml.api.enedis.fr/group/espace-particuliers/consentement-linky/oauth2/authorize?client_id=[client_id]&state=[state]&duration=[duration]&response_type=code&redirect_uri=[redirect_URI]
```
- client-id : identifiant unique client
- state : chaine de caractère aléatoire
- duration : durée du consentement (format ISO8601)
- redirect_uri : Url de redirection vers lequel l'utilisateur accedera à l'application.

Dans l'url de sortie on obtient les informations suivantes (les valeurs ne sont plus actives) :
```
https://linky.sunshare.fr/?code=5ruXvt7eM2w262Hhf5IW7fGWExr82V&state=abcdef&usage_point_id=22516914714270
```
On récupère le code qui nous permettra de faire la demande de Token et l'usage_point_id qui correspond à l'identifiant client.

La troisème étape est l'obtention du Token

Pour ce faire utiliser PostMan, dispo [ici](https://www.getpostman.com/).

On renseigne les paramètres suivants :
<p align="center" style="margin-bottom: 10px; margin-top: 30px">
<img src="https://raw.githubusercontent.com/MaximeNico/SunShare/Kevin/Ressources%20graphique/R%C3%A9cup%C3%A9rationTokenPostman.png" alt="PostMan" height = 500>
</p>

<p align="justify">Il est important de conserver les données suivantes :

- access_token : c'est le token qui sera utilisé dans toutes les demandes d'informations à destination de l'API d'Enedis. Attention il est valide uniquement pendant 3h30
- refresh_token : c'est le token qui sera utilisé pour faire une nouvelle demande d'access_token quand celui-ci sera expiré. Le refresh_token est valable un an.

Nous avons donc maintenant en notre possesion l'ensemble des entrées nécessaire pour mettre en place la demande de données</p>

#### Test récupération de données

Pour valider la bonne implémentation on essaie de récupérer les données de consommation par jour.

En voici le retour :

```json
{
    "usage_point": [
        {
            "meter_reading": {
                "usage_point_id": "XXXXXXXXXXXXXX",
                "start": "2019-07-06",
                "end": "2019-07-08",
                "reading_type": {
                    "measurement_kind": "energy",
                    "interval_length": "86400",
                    "unit": "Wh",
                    "aggregate": "sum"
                },
                "interval_reading": [
                    {
                        "value": "8357",
                        "rank": "1"
                    },
                    {
                        "value": "8851",
                        "rank": "2"
                    },
                    {
                      "value": "12498",
                      "rank": "3"
                  }
              ]
          }
      }
  ]
}

```
Puis toutes les 30min :

```json
{
    "usage_point": [
        {
            "meter_reading": {
                "usage_point_id": "XXXXXXXXXXXXXX",
                "start": "2019-07-07",
                "end": "2019-07-08",
                "reading_type": {
                    "measurement_kind": "power",
                    "interval_length": "1800",
                    "unit": "W",
                    "aggregate": "average"
                },
                "interval_reading": [
                    {
                        "value": "2723",
                        "rank": "1"
                    },
                    {
                        "value": "110",
                        "rank": "2"
                    },
                    {
                        "value": "179",
                        "rank": "3"
                    },
                    {
                        "value": "64",
                        "rank": "4"
                    },
                    {
                        "value": "79",
                        "rank": "5"
                    },
                    {
                        "value": "97",
                        "rank": "6"
                    },
                    {
                        "value": "64",
                        "rank": "7"
                    },
                    {
                        "value": "113",
                        "rank": "8"
                    },
                    {
                        "value": "63",
                        "rank": "9"
                    },
                    {
                        "value": "46",
                        "rank": "10"
                    },
                    {
                        "value": "112",
                        "rank": "11"
                    },
                    {
                        "value": "48",
                        "rank": "12"
                    },
                    {
                        "value": "48",
                        "rank": "13"
                    },
                    {
                        "value": "109",
                        "rank": "14"
                    },
                    {
                        "value": "1175",
                        "rank": "15"
                    },
                    {
                        "value": "895",
                        "rank": "16"
                    },
                    {
                        "value": "254",
                        "rank": "17"
                    },
                    {
                        "value": "314",
                        "rank": "18"
                    },
                    {
                        "value": "309",
                        "rank": "19"
                    },
                    {
                        "value": "280",
                        "rank": "20"
                    },
                    {
                        "value": "95",
                        "rank": "21"
                    },
                    {
                        "value": "110",
                        "rank": "22"
                    },
                    {
                        "value": "63",
                        "rank": "23"
                    },
                    {
                        "value": "48",
                        "rank": "24"
                    },
                    {
                        "value": "192",
                        "rank": "25"
                    },
                    {
                        "value": "97",
                        "rank": "26"
                    },
                    {
                        "value": "114",
                        "rank": "27"
                    },
                    {
                        "value": "255",
                        "rank": "28"
                    },
                    {
                        "value": "160",
                        "rank": "29"
                    },
                    {
                        "value": "159",
                        "rank": "30"
                    },
                    {
                        "value": "219",
                        "rank": "31"
                    },
                    {
                        "value": "227",
                        "rank": "32"
                    },
                    {
                        "value": "300",
                        "rank": "33"
                    },
                    {
                        "value": "206",
                        "rank": "34"
                    },
                    {
                        "value": "260",
                        "rank": "35"
                    },
                    {
                        "value": "239",
                        "rank": "36"
                    },
                    {
                        "value": "227",
                        "rank": "37"
                    },
                    {
                        "value": "147",
                        "rank": "38"
                    },
                    {
                        "value": "205",
                        "rank": "39"
                    },
                    {
                        "value": "211",
                        "rank": "40"
                    },
                    {
                        "value": "250",
                        "rank": "41"
                    },
                    {
                        "value": "93",
                        "rank": "42"
                    },
                    {
                        "value": "242",
                        "rank": "43"
                    },
                    {
                        "value": "229",
                        "rank": "44"
                    },
                    {
                        "value": "236",
                        "rank": "45"
                    },
                    {
                        "value": "287",
                        "rank": "46"
                    },
                    {
                        "value": "2164",
                        "rank": "47"
                    },
                    {
                        "value": "3586",
                        "rank": "48"
                    }
                ]
            }
        }
    ]
}
```

<p align="justify">maintenant que nous avons compris comment fonctionne la chaine de données à travers le bac à sable, il faut réaliser les scripts nécessaire à la récupération des données.</p>

### Mise en oeuvre de l'API

Voir fichier dispo dans le dossier 'API ENEDIS'

<p align="justify">Il faut bien comprendre que l'ensemble de cette chaine nécessite des interractions avec l'utilisateur. Le receuil du consentement sera liée à une page spécifique sur le serveur (linky.sunshare.fr). Il devra collecter les données sur cette page pour les renseigner ensuite sur l'interface utilisateur. Un encart spécifique est mis à disposition à la création du compte. L'objectif est de faciliter le parcours utilisateur. L'aspect token est géré via l'application et la collecte de données également.
Si tout ce passe bien et que le service Enedis fonctionne (peu stable, constaté sur plusieurs sites) les requêtes devrait renvoyer les informations attendues.</p>

## API application
