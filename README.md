# Analyse-SonarQube-d-un-Projet-Maven
# README – Analyse SonarQube d’un Projet Maven
#  1. Prérequis

Avant de lancer l’analyse SonarQube, assurez-vous d’avoir installé :

Docker Desktop (ou Docker Engine)

Java JDK 17 (ou la version requise par le projet)

Apache Maven (3.9 ou plus)

Un projet Maven valide contenant pom.xml

#  2. Lancer SonarQube avec Docker
# 2.1 Créer les volumes persistants
docker volume create sonarqube_data
docker volume create sonarqube_logs
docker volume create sonarqube_extensions

# 2.2 Démarrer SonarQube (Community Edition)
docker run -d --name sonarqube -p 9000:9000 ^
  -v sonarqube_data:/opt/sonarqube/data ^
  -v sonarqube_logs:/opt/sonarqube/logs ^
  -v sonarqube_extensions:/opt/sonarqube/extensions ^
  sonarqube:lts-community

# 2.3 Accéder à SonarQube

URL : http://localhost:9000

Identifiants par défaut :

admin / admin

Changez le mot de passe lors de la première connexion

# 3. Préparation du projet
#  3.1 Créer le fichier sonar-project.properties

À placer dans la racine du projet Maven (où se trouve pom.xml) :

sonar.projectKey=Student_class
sonar.projectName=Student_class
sonar.host.url=http://localhost:9000
sonar.login=VOTRE_TOKEN
sonar.sourceEncoding=UTF-8


⚠️ Remplacer VOTRE_TOKEN par un token généré dans SonarQube :
My Account → Security → Generate Token

⚠️ Le fichier doit s’appeler exactement :
sonar-project.properties
(et pas .txt)

#  4. Lancer l’analyse

Dans un terminal, se placer dans le dossier du projet :

cd C:\serviceA-jersey1\serviceA-jersey


Puis exécuter :

mvn clean verify sonar:sonar


 Le scanner Maven va automatiquement lire le fichier sonar-project.properties.

#  5. Consulter les résultats

Après une analyse réussie, SonarQube affiche :

Bugs

Code Smells

Vulnerabilities

Duplications

Coverage (si tests unitaires)

Quality Gate (Passed/Failed)

Accès :

👉 http://localhost:9000/dashboard?id=Student_class

# 6. Dépannage (Erreurs courantes)
Problème	Solution
Not authorized	Le token est incorrect → générer un nouveau et mettre à jour sonar-project.properties
No POM found	Vous n’êtes pas dans le bon dossier → placer Maven dans le dossier contenant pom.xml
mvn n’est pas reconnu	Ajouter Maven dans PATH → C:\Program Files\apache-maven-3.9.x\bin
invalid target release 21	Modifier pom.xml pour utiliser <maven.compiler.release>17</maven.compiler.release>
# 7. Exemple de structure finale
serviceA-jersey1/
 └── serviceA-jersey/
      ├── pom.xml
      ├── sonar-project.properties
      ├── src/
      └── target/

#  8. Conclusion

Ce projet a été analysé avec SonarQube via Maven afin d’évaluer :

La qualité du code

Les vulnérabilités

La maintenabilité

Le respect des règles de qualité définies par le Quality Gate

L’usage de SonarQube permet de garantir une meilleure qualité logicielle dans un contexte professionnel.
