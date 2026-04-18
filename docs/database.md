# Schema de la base de données TriM

## Diagramme des entités

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   Admin      │     │   Patient     │     │   Medecin    │
├─────────────┤     ├──────────────┤     ├─────────────┤
│ id (PK)      │◄───│ id (PK)       │     │ id (PK)      │
│ nom          │     │ admin_id (FK) │     │ admin_id(FK) │
│ prenom       │     │ nom           │     │ nom          │
│ email        │     │ prenom        │     │ prenom       │
│ password     │     │ age           │     │ n_tel        │
│ role         │     │ ntel          │     │ email        │
└─────────────┘     │ email         │     │ password     │
                     │ password      │     │ adresse      │
                     │ adresse       │     │ specialite   │
                     │ role          │     │ hdebut       │
                     │ genre         │     │ hfin         │
                     │ is_blocked    │     │ role         │
                     └──────┬───────┘     │ genre        │
                            │              │ is_blocked   │
                            │              └──────┬───────┘
                            │                     │
                     ┌──────▼─────────────────────▼──────┐
                     │          Ordonnance                │
                     ├───────────────────────────────────┤
                     │ id (PK)                            │
                     │ type (Pharmacie | Laboratoire)     │
                     │ description                        │
                     │ date                               │
                     │ code                               │
                     │ etat (En_Attente|En_Cours|Prete)  │
                     │ medecin_id (FK)                    │
                     │ patient_id (FK)                    │
                     │ rendez_vous_id (FK)                │
                     │ laboratoire_id (FK)                │
                     │ pharmacie_id (FK)                  │
                     │ analyse_id (FK)                    │
                     └───────────────────────────────────┘
                            │              │
                    ┌───────▼───┐   ┌──────▼──────┐
                    │RendezVous │   │  Analyse     │
                    ├───────────┤   ├─────────────┤
                    │ id (PK)    │   │ id (PK)      │
                    │ ...        │   │ ...          │
                    └───────────┘   └─────────────┘

┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│ Laboratoire   │  │  Pharmacie    │  │  Medicament   │
├──────────────┤  ├──────────────┤  ├──────────────┤
│ id (PK)       │  │ id (PK)       │  │ id (PK)       │
│ ...           │  │ ...           │  │ ...           │
└──────────────┘  └──────────────┘  └──────────────┘

┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  Chef_Lab     │  │  Pharmacien   │  │  Reclamation  │
├──────────────┤  ├──────────────┤  ├──────────────┤
│ id (PK)       │  │ id (PK)       │  │ id (PK)       │
│ ...           │  │ ...           │  │ ...           │
└──────────────┘  └──────────────┘  └──────────────┘

┌──────────────┐
│   Maladie     │
├──────────────┤
│ id (PK)       │
│ ...           │
└──────────────┘
```

## Rôles utilisateurs

| Rôle | Table | Dashboard |
|------|-------|-----------|
| Admin | `Admin` | Administration globale |
| Médecin | `Medecin` | Profil médecin, ordonnances, maladies |
| Patient | `Patient` | Statistiques, rendez-vous, réclamations |
| Chef de laboratoire | `Chef_Lab` | Gestion laboratoire, analyses |
| Pharmacien | `Pharmacien` | Gestion pharmacie, médicaments |

## Configuration

La connexion à la base de données est gérée par la classe `utils.MyDataBase` (singleton, gitignored).

Pour configurer la base de données localement, créez le fichier `src/main/java/utils/MyDataBase.java` avec vos identifiants MySQL.
