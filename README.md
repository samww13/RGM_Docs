#    I.     Description du document

## **Objectif du document**

*Ce document permet aux administrateurs Système et Réseaux la mise en œuvre de la solution d’Hypervision RGM.*

## Destination du document

*Ce document s’adresse toutes personnes souhaitant utiliser la solution « RGM » pour superviser leurs infrastructures SI et métiers.*

## Modification du document

| Date       | Révision | Propriétaire   | Résumé           |
| ---------- | -------- | -------------- | ---------------- |
| 26/03/2020 | V0R1     | Communauté RGM | Version initiale |

#    **II.**      Qu’est-ce que « RGM »



La solution RGM a pour vocation de détecter les incidents, mais aussi de les anticiper pour éviter tout arrêt de service. 

 

L’outil permet de surveiller par une scrutation régulière l’état des équipements réseau, des systèmes ainsi que des applications et services d’infrastructures (DNS, Serveur Web, Serveur de Messagerie, etc.). La disponibilité des services est représentée par équipement surveillé ou par groupes d’équipements. 

 

L’état des hôtes et des services supervisés peut faire l’objet d’alerte par mail, SMS ou autres modélisés suivant des règles de notifications construites en conformité des processus ou suite à l’étude des workflows de l’entreprise. 

L’infrastructure cible est surveillée grâce à des « plug-ins » exécutés régulièrement par RGM. Chaque plug-in est spécialisé dans la surveillance d’un élément particulier du S.I. 

Les informations collectées sont ensuite stockées en base de données et présentées sur l’interface Web de RGM sous forme de cartographie. 

La cartographie représente une vue logique du réseau surveillé ainsi que les équipements défaillants. Une double visualisation au niveau de la cartographie permet de connaître l’état des services d’un équipement et de savoir si l’équipement est « Up » ou « Down ». 



L’Appliance RGM, construite autour d’une pile Automation/Elastic/Nagios/Grafana ce qui fait de RGM une plateforme d’Hypervision qui réunit et simplifie la mise en oeuvre des logiciels libres les plus pertinents pour piloter les architectures : Legacy, Cloud et Serverless. 

 

RGM est agnostique et flexible. La solution se concentre sur la gestion des versions et sur le cycle de vie des données : 

- Gestion simplifiée de la découverte des équipements via API

- Les indicateurs collectés sont découverts au fur et à mesure qu’ils sont remontés sans avoir besoin de les déclarer préalablement 

- Garantir le bon fonctionnement d’une application via l’agrégat et la corrélation des points de surveillance 

  

RGM permet de répondre aux paradigmes suivants : 

- Découverte des métriques au fil de l’eau. Les indicateurs collectés sont découverts au fur et à mesure qu’ils sont remontés sans avoir besoin de les déclarer. 
- Webisation des composants. De plus en plus de composants exposent une interface HTTP (IHM ou API). 
- Cycles de vie courts. Les indicateurs et les composants qui les portent ont des vies très courtes, liées notamment aux déploiements des conteneurs, aux redimensionnements des pools. Reconfigurer le monitoring doit se faire à chaud et très fréquemment. 
- Vision dynamique. Les systèmes de monitoring doivent avoir la capacité à s’intégrer avec des systèmes d’auto-découverte pour s’adapter en permanence aux évolutions de la topologie d’infrastructure. 
- Vision distribuée d’éléments constitués de plusieurs indicateurs. Avoir une vraie garantie du bon fonctionnement d’un service ne peut pas nécessairement se déterminer en regardant localement l’état d’une machine ou d’un processus. Il est parfois nécessaire d’agréger ou corréler des remontées de plusieurs machines. 



Des Tableaux de bord sont proposés et modulables pour l’ensemble des acteurs de la DSI : Techniques, Capacitifs, Applicatifs et Métiers… Cela permet de donner de la visibilité sur l’infrastructure « On-permise et Cloud ». 

Les indicateurs tels que CPU, RAM, DISK vont permettre de gérer le « Capacity planning » et d’anticiper les incidents relatifs à la plateforme. Les ajouts de métriques permettent de mesurer la performance réseau.

**Composants disponibles dans la solution :**

| Briques logiciels | Fonctionnalités                                              |
| ----------------- | ------------------------------------------------------------ |
| rgmweb            | Interface d'administration                                   |
| thruk             | Interface de monitoring (Disponibilité)                      |
| nagios            | Ordonnanceur  de checks                                      |
| nagvis            | Outil de  visualisation des données Nagios                   |
| ged               | Bus  évènementiel                                            |
| nagiosBP          | Outil de  modélisation des applications                      |
| grafana           | Outil de  visualisation et de mise en forme de données métriques |
| mk-livestatus     | Outil  d'accès au moteur Nagios sans accès disque            |
| elasticsearch     | Outil  d'analyse et indexation des données                   |
| kibana            | Outil de  visualisation des données Elasticsearch            |
| beats-oss         | Agent  open source de transfert pour les indicateurs         |
| histou            | Outil  d'ajout de Templates Grafana                          |
| influxDB          | Base de  données Time series                                 |
| mariaDB           | Base de  données MySQL                                       |
| lilac             | Outil de  configuration graphique pour Nagios                |
| nagflux           | Connecteur  de données de performance                        |
| notifier          | Module  de notifications avancées                            |
| nrdp              | Protocole  de transport pour les données Nagios              |
| rgmapi            | API RGM                                                      |
| ansible           | Outil de  management des configuration                       |
| snmptt            | Outil de  capture et traduction des traps SNMP               |
| mod_auth_rgm      | Module  d'authentification pour RGM                          |
| nrpe              | Moteur des agents Nagios pour exécution des scripts locaux   |
| mod_gearman       | Module  pour architecture RGM distribuée                     |
| apache            | Serveur  Web                                                 |

L’ensemble des services ne seront pas abordés dans ce document.

**Rappel de compétences :**

Sous RGM, l’utilisateur ayant tous les droits est appelé « rgm ». 

Pour disposer de ses droits, il convient de se loguer en tant que « rgm » sur la machine.

**Toutes les commandes** sont donc exécutées en « rgm » ou avec un utilisateur ayant ses droits. 

 

Les principaux répertoires RGM sont : 

/etc Contient les fichiers de configuration de bases 

/srv/rgm Contient les fichiers relatifs à la solution RGM 

/usr Contient les fichiers utilisateurs

#    **III.**      Installation de la solution « RGM »

Pour l'installation de la solution « RGM », se référer au chapitre d'installation.

#    **IV.**      Accès à l'interface « RGMWEB »

## 1. Accès à l'interface Web

Pour accéder à l’interface web, il convient de saisir l’url du serveur web dans un navigateur :

[https://nom_du_serveur/login.php##](https://nom_du_serveur/login.php)

Le login par défaut pour accéder à l’interface est « admin:admin »

![](md_pics/screen_init_install.png)

## 2. Présentation des menus

La solution se décline sous 6 menus principaux :

### a. Tableau de bord

Le menu « Tableaux de bord » propose l’accès à différentes visualisations :  Vue synthétique du SI, Topologie réseau, Cartes Nagvis et performance Grafana.

*Vue synthétique du SI*

![](md_pics/vue_synthetique_RGM.png)

Sur le tableau de bord, il y a 4 types de diagrammes, circulaires et en barre : 

- Celui en haut à gauche représente l’état des équipements « UP/DOWN »
- Celui en haut à droite symbolise les services « CRITICAL/WARNING/UNKNOWN et PENDING » 
- Les 2 graphiques en bas proposent les messages d’erreurs en cours, dénommés « évènements actifs » selon leurs niveaux de criticité.

*Topologie réseau*

![](md_pics/topologie_RGM.png)

Cette cartographie permet une visualisation circulaire ou tabulaire avec divers regroupements (équipements, services, adresses IP…).

*Cartes Nagvis*

![](md_pics/screen_Nagvis_1.png)

Les cartes Nagvis, souples et modulables, permettent de générer des vues métiers issus de la supervision.

*Performance - Grafana* 

![](md_pics/dashboard_grafana_vmware.png)

Grafana permet de générer des tableaux de bord sur la base de métriques et données temporelles. Il est orienté « data visualisation ».

### b. Disponibilités

*Problèmes*

![](md_pics/screen_dispo1.png)

La vue Problèmes permet de visualiser les pannes en cours. Cette vue se décompose en deux sous-menus « Incidents équipements » et « Incidents services » pour une meilleure visualisation.

*Incident équipements*

![](md_pics/incident_assets.png)

*Incident services*

![](md_pics/incident_services.png)

*Groupes d’équipements*

![](md_pics/groupe_equipements.png)

La vue « Groupes d’équipements » permet de trier et classer les équipements par technologie, type ou modèle. Ces regroupements sont utilisés notamment pour limiter les vues de certains utilisateurs. 

*Groupes de services*

La vue « Groupe de services » est similaire à la précédente, et permet également de limiter les vues utilisateurs à certains services spécifiques.

*Évènements*

La vue « Evènements » permet la visualisation des événements actifs et résolus.

Affichage des évènements en cours avec l’état et le descriptif associé. 

![](md_pics/ged_events_1.png)

Il est possible d’interagir sur les événements via la prise en compte ou l’acquittement par exemple et d’afficher plus de détails.

![](md_pics/ged_events2.png)

*Applications*

![](md_pics/application_view.png)

La vue Application fournit un résumé des vues métiers disponibles et du service rendu à l’utilisateur final.

![](md_pics/application_view2.png)

L’icône « Tree » permet de visualiser l’ensemble des services qui sont utilisés pour modéliser l’application. 

### c. Capacité

*Performance*

![](md_pics/capacity_perf.png)

Ce menu permet la visualisation graphique des services par équipements sur une période donnée.

### d. Production

*Arrêts planifiés/récurrents*

![](md_pics/downtime1.png)

Ce menu permet de suspendre temporairement la supervision sur un ou plusieurs équipements et ces services sur une période donnée. 

Il également possible de définir des plages de maintenance récurrentes dans le cadre de campagnes de mises à jour par exemple.

### e. Rapports

*Génération de rapports*

![](md_pics/report1.png)

Ce menu permet de générer automatiquement des rapports de disponibilité des équipements et des services. L’envoi des rapports par mail est possible sous réserve d’une configuration préalable.

Il peuvent être également consultés immédiatement en HTML ou PDF.

![](md_pics/report2.png)

*Évènements*

![](md_pics/events_report.png)

Le sous-menu « Evènements » permet de visualiser les volumes d’incidents sur une période donnée et SLA technique avec les temps moyens de résolution.

*Disponibilité*

![](md_pics/dispo_report.png)

Le menu disponibilité permet de générer à la volée des rapports de disponibilité, tendances et résumés sur une période donnée sur différents critères (groupe d’équipements, services…).

### f. Administration

Ce menu permet la configuration complète de la solution RGM, il sera donc détaillé plus en profondeur dans le chapitre suivant « Paramétrage de la solution ».

#    V.      Paramétrage de la solution « RGM »

**L’Appliance** **RGM** est construite autour d’une pile Automation/Elastic/Nagios/Grafana et un ensemble de composants pour répondre aux besoins d’Hypervision. 

## 1. Configuration des surveillances - Paramètres

