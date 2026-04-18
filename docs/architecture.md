# Architecture du projet TriM

## Vue d'ensemble

TriM suit une architecture **MVC (Model-View-Controller)** avec une couche de services pour l'accès aux données.

```
src/main/java/
├── models/          # Entités (POJOs)
├── controllers/     # Contrôleurs JavaFX
├── services/        # Couche d'accès aux données (DAO)
├── enums/           # Énumérations
├── utils/           # Utilitaires (DB connection) [gitignored]
└── tests/           # Points d'entrée de l'application

src/main/resources/
├── views/           # Fichiers FXML (interfaces)
├── styles/          # Feuilles de style CSS
├── img/             # Images et icônes
├── html/            # Templates d'email HTML
└── leaflet/         # Assets pour la carte
```

## Couche Model

Les modèles sont des POJOs Java représentant les entités métier :

| Modèle | Description | Champs clés |
|--------|-------------|-------------|
| `Patient` | Patient du système | nom, prenom, age, email, password, adresse, role, genre |
| `Medecin` | Médecin | nom, prenom, email, specialite, hdebut, hfin |
| `Ordonnance` | Ordonnance médicale | type (TypeOrd), description, date, code, etat (EtatOrd) |
| `RendezVous` | Rendez-vous | Lien médecin-patient, date, heure |
| `Analyse` | Analyse de laboratoire | Résultats d'analyse |
| `Medicament` | Médicament | Informations sur les médicaments |
| `Maladie` | Maladie | Base de données des maladies |
| `Laboratoire` | Laboratoire | Informations du laboratoire |
| `Pharmacie` | Pharmacie | Informations de la pharmacie |
| `Reclamation` | Réclamation | Système de plaintes |
| `Admin` | Administrateur | Gestion du système |
| `Chef_Lab` | Chef de laboratoire | Gestion du labo |
| `Pharmacien` | Pharmacien | Gestion de la pharmacie |

## Couche Service

Toutes les services implémentent l'interface générique `IService<T>` :

```java
public interface IService<T> {
    void add(T t);
    void update(T t, int id);
    void delete(int id);
    T getById(int id);
    List<T> getAll();
}
```

Chaque service utilise **JDBC avec PreparedStatement** pour les opérations SQL. La connexion est obtenue via le singleton `MyDataBase.getInstance().getConnection()`.

## Couche Controller

Les contrôleurs JavaFX gèrent les interactions utilisateur. Chaque vue FXML est liée à un contrôleur. Convention de nommage :

- `XxxController` ou `XxxControlleur` - Contrôleur principal
- `AjouterXxxController` - Formulaire d'ajout
- `ModifierXxxController` - Formulaire de modification
- `AfficherXxxController` / `ShowXxxController` - Vue d'affichage

## Flux d'authentification

```
MainApplication (splash screen, 2s)
    └── Main.fxml (page de connexion)
        └── SignInControlleur (authentification)
            ├── Médecin    → medecinProfile.fxml
            ├── Patient    → StatistiqueGui.fxml
            ├── Chef Lab   → home.fxml
            └── Pharmacien → homePhar.fxml
```

## Énumérations

- **TypeOrd** : `Pharmacie`, `Laboratoire` — Type d'ordonnance (vers pharmacie ou laboratoire)
- **EtatOrd** : `En_Attente`, `En_Cours`, `Prete` — État de traitement de l'ordonnance

## Services externes

| Service | Bibliothèque | Utilisation |
|---------|-------------|-------------|
| Email | JavaMail | Notifications par email avec templates HTML |
| SMS | Twilio SDK | Notifications par SMS |
| PDF | iTextPDF / PDFBox | Génération d'ordonnances en PDF |
| Cartes | Leaflet | Localisation des pharmacies/laboratoires |
| Calendrier | CalendarFX | Gestion des rendez-vous |

## Base de données

- **SGBD** : MySQL 8.0
- **Connexion** : Singleton `MyDataBase` dans le package `utils` (gitignored car contient les identifiants de connexion)
- **Accès** : JDBC natif avec PreparedStatement (pas d'ORM)
