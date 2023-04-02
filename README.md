# Lokilogs

## Partie 1 - Loki

### Questions

1. Qu’est ce que Loki ?

Loki est un système d'agregation de log inspiré de promtheus. Ce produit est développé par Grafana Labs et s’appuie sur leur produit éponyme pour l’affichage des logs. L’une des principales informations à savoir sur Loki est que seules les métadonnées de vos logs sont indexées. C’est ce qui le différencie d’Elasticsearch et qui lui permet aussi de consommer moins de ressources que ce dernier. 

2. Quelles sont **les différentes composantes** de la stack **Loki** fournie ?

Les fichiers : 
- docker-compose.yml
- loki-config.yaml
- promtail-local-config.yaml

Les différentes composantes : 
- read
- write
- promtail
- minio
- gateway
- flog

3. À quoi servent **chacune des composantes** ?

Les différentes composantes : 
- read
    - pour lire les logs sur minio
- write
    - pour écrire les logs sur minio
- promtail
    - agent qui se charge d'envoyer les logs générés par lees containers docker vers loki 
- minio
    - serveur de stockage d'object compatible avec amazon s3
- gateway
    - il se charge de servir l'API de Loki avec Nginx
- flog
    - générateur de faux logs

4. Qu’est-ce que Minio ? 

MinIO offre un stockage d'objets hautes performances compatible S3. Natif de Kubernetes, MinIO est la seule suite de stockage d'objets disponible sur chaque cloud public, chaque distribution Kubernetes, le cloud privé et la périphérie. MinIO est défini par logiciel et est 100% open source sous GNU AGPL v3.

5. **Réalisez un schéma** (à mettre dans le dossier partie1 du repo) du flux de données entre le moment où un log est écrit dans docker jusqu’au moment où il est visible dans grafana.

![Schéma](/assets/images/schéma.png)

6. À quoi sert le service **gateway** ?

Le service **gateway** :  pk ?


## Partie 2 - Logs

### Questions 

7. L’application a une structure de logs plutôt constante, quels champs sont contenus dans les logs ? Quelle données représentent-il?

Les champs contenus dans les logs :


8. Qu’est-ce qui doit être configuré du coté de la stack loki pour récolter les logs ? 

Pour récolter les logs, ce qui doit être configuré du côté de la stack loki c'est 

9. Dans l’onglet “explorer”, quelle requête permet d’avoir :

A. le volume de logs par couleur

    sum by(level) (count_over_time({container="logapp"} | json [1h]))

B. Filtrer les resultats pour un utilisateur


10. Créer un dashboard qui contiendra la part de paiements en succès et en échec

![Dashboard](/assets/images/dashboard.png)


## Partie 3 - Elasticsearch

### 1. Mise en place d’Elasticsearch et Kibana

#### Questions 

11. qu’est-ce qu’elasticsearch ? 

Elasticsearch un logiciel utilisant Lucene pour l'indexation et la recherche de données. Il fournit un moteur de recherche distribué et multientité à travers une interface REST. C'est un logiciel écrit en Java distribué sous licence Elastic. Il est ouvert pour toutes les données (textuelles, numériques, géospatiales, structurées et non structurées).

12. À quoi sert elasticsearch ? 

Elasticsearch peut être employé dans différents cas d'utilisation : 
* Recherche applicative
* Recherche de site web
* Entreprise Search
* Logging et analytique de log
* Indicateurs d'infrastructure et monitoring de conteneur
* Monitoring des performances applicatives
* Analyse et visualisation de données géospatiales
* L'analyse de la sécurité
* Analyse des données métier

13. Qu’est ce que Kibana ? Sur quel port accéder à Kibana ?

Kibana est une application frontend gratuite et ouverte qui s'appuie sur la Suite Elastic. Elle permet de rechercher et de visualiser les données indexées dans Elasticsearch. 

Pour accéder à Kibana, c'est par défaut le port 5601.

14. Qu’est-ce qu’un index Elasticsearch ? 

Un index Elasticsearch est une collecte de documents en lien les uns avec lea autres. Elasticsearch stocke des données sous forme de documents JSON.

15. Qu’est-ce que Lucene ? Quel est son rapport avec Elasticsearch ? 

Lucene est une bibliothèque open source écrite en Java qui permet d'indexer et de chercher du texte. Il est utilisé dans certains moteurs de recherche. C'est un projet de la fondation Apache mis à disposition sous licence Apache. Il est également disponible pour les langages Ruby, Perl, C++, PHP, C#, Python.

Elasticsearch est basé sur Lucene (couche basse généré par Lucene). il utilise Lucene aussi pour ses requêtes.


### 2. Filebeat

#### Questions

16. Qu’est-ce que Filebeat ?

FileBeat est composé de modules pour des sources de données pour simplifier la collecte, l'analyse et les vues des formats de journaux d'entrées. Il utilise également le protocole de contrôle de flux lors de l'envoi de plusieurs données à Elasticsearch ou Logstash.

17. Quels autres “beats” existent ?

Les beats sont différentes applications que l’on installe sur des machines qui seront chargées de récupérer des logs et des informations et de les envoyer aux sorties compatibles.

* Filebeat qui lit les fichiers.
* Metricbeat en charge de récupérer des indicateurs sur des serveurs (Systèmes d’exploitation, MySQL…)
* Packetbeat pour récupérer des données réseaux.
* Winlogbeat pour récupérer les logs se trouvant dans l’Eventviewer.
* Auditbeat qui récupère des données du framework audit Linux.
* Heartbeat qui va récupérer des données en faisant des tests de disponibilité des services.


### 3. Dashboard

#### Question 

Réalisez le même dashboard. Le dashboard devra être conservé sur Kibana et un lien vers celui-ci devra être rendu.
Pour plus de sécurité vous pouvez exporter les informations du dashboard via management > stack Management > Kibana > Saved Object et les commit dans le repository

## Partie 4 - retour d’expérience

### Question 

Quel est votre avis sur l’usage de Loki et d’Elasticsearch pour la collecte de logs ?


## Sources

- [Getting started with Grafana Loki](https://grafana.com/docs/loki/latest/getting-started/)
- [Run Elasticsearch locally | Elasticsearch Guide [8.6] | Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/run-elasticsearch-locally.html)
- [Elasticsearch](https://www.notion.so/Elasticsearch-48779e80d2b04db4b7e801c94e0ea46d)