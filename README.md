# Affectation de sujets lors de projets scolaires

Ce projet est réalisé dans le cadre de MProjet, dans l'UE "Projet et outils de développement". Il est supervisé par M. Philippe DAVID et réalisé par l'équipe Cyrovini (Cynthia ANDRIAMPARIVONY, Romain BAROU, Victoire LENGLART et Nicolas KIRCHHOFFER).

- [Affectation de sujets lors de projets scolaires](#affectation-de-sujets-lors-de-projets-scolaires)
  - [Rappel du contexte](#rappel-du-contexte)
  - [Présentation de la solution](#présentation-de-la-solution)
  - [Solutions techniques retenues](#solutions-techniques-retenues)
  - [Organisation du développement](#organisation-du-développement)
  - [Retour d'expérience](#retour-dexpérience)
  - [Installation du projet](#installation-du-projet)

## Rappel du contexte

Tous les ans, dans le cadre de multiples projets de cours, l'affectation des sujets aux étudiants est une problématique récurrente. En effet, il faut satisfaire les choix d'un maximum d'étudiants en essayant d'en décevoir le minimum. Un logiciel a été conçu permettant d'optimiser la résolution de ce genre de problématiques. Il repose sur des notions de programmation linéaire. 

Seulement, ce logiciel a été réalisé sur client lourd et a été modifié/réarrangé au cours des années. De plus, de plus en plus de projets requièrent une optimisation dans l'affectation des sujets, ayant causé des polémiques dans certaines promotions.

## Présentation de la solution

Nous sommes parvenus à une solution technique tentant de répondre à un maximum de contraintes. La première, évidente de facto, étant de rendre cette application disponible par plusieurs professeurs, en la rendant disponible en ligne. Il s'agirait donc d'une application web.

Plusieurs aspects bien distincts ont été distingués : 
- La partie "front-office" où l'étudiant indique ses choix de sujets
- La partie "back-office" où le professeur définit les projets, les sujets et accède au résultat de la résolution linéaire
- La partie solveur, effectuant le calcul de répartition des différents sujets aux différents étudiants en fonction des choix d'entrée et de différentes contraintes, définies en fonction du projet
- Le back-end, constituant une API centrale vers laquelle tous les services se tournent afin d'obtenir et de modifier les données, mais également de prouver l'intégrité des utilisateurs accédant à l'application

Du fait de ces aspects distincts, maintenables indépendamment des autres, une architecture par microservices a été choisie. Chaque aspect représente un service, autonome et indépendant. 

## Solutions techniques retenues

Ensuite, pour chaque service, il aura fallu déterminer les technologies à utiliser afin de réaliser le projet. Voici les pistes de réflexion :

- Front-office : Vue, un framework JavaScript, nous permet de réaliser des composants et, ainsi, de réduire la complexité d'implémentation. Etant un framework réactif, Vue nous permet également de réaliser des animations, rendant l'expérience utilisateur plus agréable
- Back-office : Vue, couplé avec son routeur, Vue Router,nous permet une navigation fluide et une récupération des données natives. Vuex nous permet de centraliser les données stockées par l'application et ainsi de minimaliser les requêtes faites à l'API, optimisant de fait l'expérience utilisateur du côté des professeurs
- Solveur : la résolution linéaire se fait via PuLP, une librairie Python permettant de s'interfacer avec des solveurs. Un de ses intérêts majeurs est le fait de pouvoir communiquer avec le solveur en JSON, que ce soit via les données d'entrée ou les données récupérées après la résolution d'un problème.
- Back-end : Spring nous permet une approche plus monolithique mais qui n'entre pas pour autant en contradiction avec les micro-services. L'API, étant centrale à tous les services, se doit de supporter une charge accrue et doit être stable, de prime abord. On profite ainsi d'un framework mature et d'un langage dont le typage garantie la stabilité. De plus, couplé à Hibernate, Spring nous permet de traiter les données très relationnelles avec une complexité de calcul et d'implémentation amoindrie.

Les données seront intégralement stockées sur MariaDB, un fork du projet MySQL, permettant une vitesse améliorée d'accès/écriture aux données, mais surtout une structure relationnelle stable et efficace.

## Organisation du développement

Suivant le framework Scrum, les tâches de développement ont été définies au cours d'un Backlog en début du premier Sprint. Ces tâches ont été enrichies d'une estimation de temps et d'une assignation de développeur.se. 

Ainsi, le nombre de services étant en accord avec le nombre de développeur.se.s, nous avons assigné une personne pour un service. On se retrouve ainsi avec les fonctions suivantes :

- Victoire LENGLART : maquettage/prototypage front-end et développeuse front-end back-office
- Cynthia ANDRIAMPARIVONY : développeuse front-office et support au développement back-end
- Romain BAROU : développeur du solveur et concepteur des échanges entre le back-end et le solveur
- Nicolas KIRCHHOFFER : développeur du back-end, concepteur des données et DevOps du projet (cycles de livraison)

## Retour d'expérience

Ce projet aura été enrichissant pour nous. Il nous a permis de suivre le cycle entier de conception d'un produit, allant de la spécification jusqu'à la livraison. Il nous a aussi permis d'apprendre à nous organiser en autonomie, les tâches étant désignées et réparties par nos propres soins.

Le fait d'estimer le travail à faire et de s'y tenir est sûrement l'un des points les plus complexes de ce projet. Il nous a été quasiment impossible de respecter les estimations faites en premier lieu. Nous avons été forcés de passer du temps à affiner les tâches dans le but de préparer le second Sprint.

De même, nous avons pensé que la structure de la base de données aurait suffi à spécifier le format des données transitant entre les services. Finalement, une mise en place de documentation aurait été favorable en amont du développement des requêtes et de leurs réponses.

## Installation du projet

L'installation du projet a été simplifiée un maximum grâce à l'utilisation de la technologie Docker, permettant de livrer des applications sans tenir compte de l'environnement hôte. 3 services sur 4 ont été livrés sur Docker à l'heure de la rédaction de ce document, et le 4ème, étant le back-end, est en cours de livraison.

*Cette partie est incomplète et sera réalisée lorsque le 4ème service, étant le back-end, sera livré. Les modifications faites à la documentation peuvent être consultées via ce lien : [https://github.com/cyrovini/documentation](https://github.com/cyrovini/documentation)*
