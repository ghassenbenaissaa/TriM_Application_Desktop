<p align="center">
  <img src="src/main/resources/img/logo.png" alt="TriM Logo" width="200"/>
</p>

<h1 align="center">TriM - Healthcare Management System</h1>

<p align="center">
  Application desktop de gestion de soins de sante multi-roles, developpee avec JavaFX.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-17-orange?style=flat-square&logo=openjdk" alt="Java 17"/>
  <img src="https://img.shields.io/badge/JavaFX-21.0.2-blue?style=flat-square" alt="JavaFX"/>
  <img src="https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL"/>
  <img src="https://img.shields.io/badge/Maven-3.8+-C71A36?style=flat-square&logo=apachemaven&logoColor=white" alt="Maven"/>
</p>

---

## A propos

**TriM** est une application desktop complete pour la gestion des soins de sante. Elle permet aux differents acteurs du domaine medical (medecins, patients, pharmaciens, laborantins) de collaborer efficacement a travers une interface intuitive.

## Fonctionnalites principales

| Module | Description |
|--------|-------------|
| **Authentification** | Connexion securisee avec routage par role (Medecin, Patient, Chef Labo, Pharmacien) |
| **Ordonnances** | Creation, suivi et gestion des ordonnances (pharmacie ou laboratoire) |
| **Rendez-vous** | Prise de rendez-vous avec calendrier interactif (CalendarFX) |
| **Analyses** | Gestion des analyses de laboratoire et suivi des resultats |
| **Medicaments** | Base de donnees des medicaments avec gestion de stock |
| **Maladies** | Repertoire des maladies et diagnostics |
| **Reclamations** | Systeme de reclamations et suivi |
| **Notifications** | Envoi d'emails (JavaMail) et SMS (Twilio) |
| **PDF** | Generation d'ordonnances en PDF (iTextPDF) |
| **Localisation** | Carte interactive des pharmacies et laboratoires (Leaflet) |
| **Statistiques** | Tableaux de bord avec graphiques et indicateurs |

## Architecture

Le projet suit une architecture **MVC** avec couche de services :

```
src/main/java/
├── models/          # Entites metier (Patient, Medecin, Ordonnance...)
├── controllers/     # Controleurs JavaFX (1 par vue FXML)
├── services/        # Acces aux donnees (IService<T> generique)
├── enums/           # TypeOrd, EtatOrd
├── utils/           # Connexion BDD (gitignored)
└── tests/           # Points d'entree

src/main/resources/
├── views/           # Interfaces FXML
├── styles/          # CSS
├── img/             # Images et icones
├── html/            # Templates email
└── leaflet/         # Assets cartographiques
```

> Pour plus de details, consultez la [documentation d'architecture](docs/architecture.md).

## Prerequis

- **Java JDK 17+**
- **Maven 3.8+**
- **MySQL 8.0**

## Installation rapide

```bash
# 1. Cloner le projet
git clone https://github.com/<votre-username>/TriM_Application_Desktop.git
cd TriM_Application_Desktop

# 2. Creer la base de donnees MySQL
mysql -u root -p -e "CREATE DATABASE trim_db;"

# 3. Configurer la connexion (voir docs/setup.md)

# 4. Installer les dependances
mvn clean install -DskipTests

# 5. Lancer l'application
mvn clean javafx:run
```

> Consultez le [guide d'installation complet](docs/setup.md) pour la configuration de la base de donnees.

## Stack technique

| Technologie | Version | Role |
|------------|---------|------|
| Java | 17 | Langage principal |
| JavaFX | 21.0.2 | Framework UI desktop |
| MySQL | 8.0 | Base de donnees relationnelle |
| Maven | 3.8+ | Gestion de build et dependances |
| JavaMail | 1.6.2 | Envoi d'emails |
| Twilio SDK | 10.1.5 | Envoi de SMS |
| iTextPDF | 5.5.13 | Generation de PDF |
| CalendarFX | 11.12.7 | Composant calendrier |
| Leaflet | 1.7.1 | Cartes interactives |
| JUnit 5 | 5.10.0 | Tests unitaires |

## Documentation

| Document | Description |
|----------|-------------|
| [Architecture](docs/architecture.md) | Architecture MVC, couches, flux d'authentification |
| [Base de donnees](docs/database.md) | Schema des entites et relations |
| [Installation](docs/setup.md) | Guide d'installation pas a pas |

## Roles utilisateurs

| Role | Acces |
|------|-------|
| **Medecin** | Profil, ordonnances, maladies, rendez-vous |
| **Patient** | Statistiques, rendez-vous, reclamations |
| **Chef de laboratoire** | Gestion labo, analyses, prelevements |
| **Pharmacien** | Gestion pharmacie, medicaments |
| **Admin** | Administration globale du systeme |

## Licence

Ce projet est developpe dans un cadre academique.
