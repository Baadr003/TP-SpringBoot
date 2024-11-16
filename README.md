
# Application de Gestion des Étudiants avec Spring Boot

## Table des Matières
1. [Introduction](#introduction)
2. [Technologies Utilisées](#technologies-utilisées)
3. [Structure du Projet](#structure-du-projet)
4. [Instructions d'Installation](#instructions-dinstallation)
5. [Fonctionnalités de l'Application](#fonctionnalités-de-lapplication)
6. [Test des Endpoints](#test-des-endpoints)
7. [Dépannage](#dépannage)

---

## Introduction
Cette application basée sur Spring Boot permet de gérer une base de données d'étudiants. Elle démontre comment :
- Utiliser Spring Boot avec JPA et MySQL.
- Implémenter des services RESTful pour les opérations CRUD.
- Tester les endpoints REST à l'aide d'outils comme SoapUI.

---

## Technologies Utilisées
- **Java** (Version 8 ou supérieure)
- **Spring Boot** (Dépendances : Web, JPA, Validation, MySQL Driver, REST Repositories)
- **Maven** (Outil de Build)
- **MySQL** (Base de données)
- **Postman/Advanced REST Client** (Pour tester les endpoints)

---

## Structure du Projet
```plaintext
student-management/
├── src/main/java/com/example/student_management/
│   ├── controllers/
│   │   └── StudentController.java
│   ├── entities/
│   │   └── Student.java
│   ├── repositories/
│   │   └── StudentRepository.java
│   ├── services/
│   │   └── StudentService.java
│   └── StudentManagementApplication.java
├── src/main/resources/
│   └── application.properties
├── src/test/java/com/example/student_management/
│   └── StudentControllerTest.java
└── pom.xml
```

---

## Instructions d'Installation

### Étape 1 : Créer le Projet Spring Boot
1. Visitez [Spring Initializr](https://start.spring.io/).
2. Configurez le projet :
   - **Project** : Maven
   - **Language** : Java
   - **Version Spring Boot** : Dernière version stable
   - **Group** : `com.example`
   - **Artifact** : `student-management`
   - **Packaging** : Jar
   - **Version de Java** : 8 ou supérieure
   - **Dépendances** : Web, JPA, Validation, MySQL Driver, REST Repositories
3. Téléchargez et extrayez le projet.
4. Importez le projet dans votre IDE (IntelliJ IDEA, Eclipse, etc.).

### Étape 2 : Configurer la Base de Données MySQL
1. Créez une base de données nommée `studentdb` dans MySQL :
   ```sql
   CREATE DATABASE studentdb;
   ```
2. Ouvrez le fichier `application.properties` dans `src/main/resources` et configurez la connexion à la base de données :
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/studentdb?serverTimezone=UTC
   spring.datasource.username=root
   spring.datasource.password=votre_mot_de_passe
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   spring.jpa.properties.hibernate.format_sql=true
   ```

---

### Étape 3 : Définir les Entités et Référentiels
- **Classe Entité** : `Student`
  - Définit les champs : `id`, `nom`, `prenom`, `dateNaissance`.
  - Annotée avec `@Entity`, `@Id`, `@GeneratedValue`, etc.
- **Interface Référentiel** : `StudentRepository`
  - Étend `JpaRepository` et inclut une requête personnalisée pour regrouper les étudiants par année de naissance.

---

### Étape 4 : Implémenter les Services et Contrôleurs REST
- **Couche Service** : `StudentService`
  - Implémente les opérations CRUD telles que `save`, `delete`, `findAll`, etc.
- **Couche Contrôleur** : `StudentController`
  - Gère les requêtes HTTP avec des méthodes mappées sur des endpoints comme `/students/all` et `/students/save`.

---

### Étape 5 : Tester les Endpoints REST
1. Utilisez des outils comme **Postman** ou **Advanced REST Client** pour tester :
   - **POST** `/students/save` : Ajoute un nouvel étudiant.
   - **GET** `/students/all` : Récupère tous les étudiants.
   - **DELETE** `/students/delete/{id}` : Supprime un étudiant par ID.

---

### Étape 6 : Tests Unitaires avec JUnit et Mockito
- Les tests sont fournis pour les méthodes de `StudentController` en utilisant Mockito pour simuler les dépendances.
- Exemples de méthodes de test :
  - `testSaveStudent()` : Vérifie que l'enregistrement d'un étudiant renvoie un statut `201 CREATED`.
  - `testDeleteStudent()` : Simule la suppression d'un étudiant et vérifie le statut `204 NO CONTENT`.

---

### Étape 7 : Intégration de Swagger
- Ajoutez la dépendance Swagger dans `pom.xml` :
   ```xml
   <dependency>
       <groupId>org.springdoc</groupId>
       <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
       <version>2.0.2</version>
   </dependency>
   ```
- Accédez à l'interface Swagger à : [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html).

---

### Étape 8 : Exécution de l'Application
1. Lancez l'application :
   ```bash
   mvn spring-boot:run
   ```
2. Vérifiez les logs de l'application pour le message :
   ```
   Started DemoApplication in X seconds
   ```

---

## Fonctionnalités de l'Application
- **Opérations CRUD** : Créer, Lire, Mettre à jour et Supprimer des étudiants.
- **Requêtes Personnalisées** : Récupérer les étudiants regroupés par année de naissance.
- **Documentation de l'API** : Générée automatiquement avec Swagger.

---

## Dépannage
- **Problèmes de Connexion à la Base de Données** : Vérifiez les identifiants dans `application.properties`.
- **Erreurs de Dépendances** : Exécutez `mvn clean install` pour rafraîchir les dépendances.
- **Logs** : Utilisez les logs de l'application pour identifier et corriger les erreurs lors de l'exécution.
