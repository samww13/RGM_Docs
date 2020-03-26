#    **I.**      Description du document

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

![](.\md_pics\rgm_module.png)



