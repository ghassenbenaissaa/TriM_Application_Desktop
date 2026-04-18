# Guide d'installation

## Prérequis

- **Java JDK 17** ou supérieur
- **Maven 3.8+**
- **MySQL 8.0**
- Un IDE Java (IntelliJ IDEA recommandé)

## Installation

### 1. Cloner le projet

```bash
git clone https://github.com/<votre-username>/TriM_Application_Desktop.git
cd TriM_Application_Desktop
```

### 2. Configurer la base de données

Créez une base de données MySQL :

```sql
CREATE DATABASE trim_db;
```

### 3. Configurer la connexion

Créez le fichier `src/main/java/utils/MyDataBase.java` :

```java
package utils;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class MyDataBase {
    private static MyDataBase instance;
    private Connection connection;

    private final String URL = "jdbc:mysql://localhost:3306/trim_db";
    private final String USER = "votre_utilisateur";
    private final String PASSWORD = "votre_mot_de_passe";

    private MyDataBase() {
        try {
            connection = DriverManager.getConnection(URL, USER, PASSWORD);
            System.out.println("Connexion etablie");
        } catch (SQLException e) {
            System.err.println("Erreur de connexion: " + e.getMessage());
        }
    }

    public static MyDataBase getInstance() {
        if (instance == null) {
            instance = new MyDataBase();
        }
        return instance;
    }

    public Connection getConnection() {
        return connection;
    }
}
```

> **Important :** Ce fichier est gitignored pour protéger vos identifiants de base de données.

### 4. Installer les dépendances

```bash
mvn clean install -DskipTests
```

### 5. Lancer l'application

```bash
mvn clean javafx:run
```

## Commandes utiles

| Commande | Description |
|----------|-------------|
| `mvn clean compile` | Compiler le projet |
| `mvn clean javafx:run` | Lancer l'application |
| `mvn test` | Exécuter les tests |
| `mvn clean install -DskipTests` | Construire le package |
