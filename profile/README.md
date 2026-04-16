# CAP Projet Undrive

Plateforme d'éco-mobilité gamifiée. L'application détecte les trajets bas carbone, calcule les économies de CO₂ associées et les convertit en jetons utilisables chez des partenaires locaux.

Projet réalisé dans le cadre du Cycle d'Approfondissement Projet (CAP) à l'[ESIEA](https://www.esiea.fr/).

## Équipe

- [@Yoann-CORGNET](https://github.com/Yoann-CORGNET)
- [@ijScrypt](https://github.com/ijScrypt)
- [@K4yan0](https://github.com/K4yan0)
- [@DIDIer5454](https://github.com/DIDIer5454)
- [@GrizruleH](https://github.com/GrizruleH)
- [@ElieFellous](https://github.com/ElieFellous)

## Stack

| Catégorie  | Technologies |
|------------|--------------|
| Langages   | ![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white) ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white) ![HCL](https://img.shields.io/badge/HCL-844FBA?style=for-the-badge&logo=terraform&logoColor=white) |
| Front-end  | ![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white) ![OpenStreetMap](https://img.shields.io/badge/OpenStreetMap-7EBC6F?style=for-the-badge&logo=openstreetmap&logoColor=white) ![Material](https://img.shields.io/badge/Material-757575?style=for-the-badge&logo=materialdesign&logoColor=white) |
| Back-end   | ![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white) ![DRF](https://img.shields.io/badge/DRF-A30000?style=for-the-badge&logo=django&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white) ![PostGIS](https://img.shields.io/badge/PostGIS-336791?style=for-the-badge&logo=postgresql&logoColor=white) ![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white) |
| Infra      | ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white) ![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white) ![Cloud Run](https://img.shields.io/badge/Cloud_Run-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white) ![Cloud Tasks](https://img.shields.io/badge/Cloud_Tasks-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white) ![Cloud SQL](https://img.shields.io/badge/Cloud_SQL-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white) |
| DevOps     | ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![Docker Compose](https://img.shields.io/badge/Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white) ![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white) |

## Architecture

```mermaid
flowchart LR
    MOBILE["App Flutter"] --> API["Django API :8000"]
    API <--> DB[("PostgreSQL + PostGIS")]
    API -->|trip submitted| Q["Cloud Tasks"]
    Q --> VAL["Trip Validation :8001"]
    VAL --> API
```

- **Mobile** : application Flutter (Android, iOS, Web), GPS et accéléromètre, carte OpenStreetMap.
- **API** : Django REST Framework, authentification Google OAuth2 + JWT, persistance PostgreSQL/PostGIS.
- **Validation des trajets** : microservice FastAPI déclenché de manière asynchrone via GCP Cloud Tasks.
- **Infrastructure** : Cloud Run multi-environnements (dev, prod, preview par PR), provisionné en Terraform, livré via GitHub Actions.

## Fonctionnalités

- Détection automatique du mode de transport (marche, vélo, voiture) à partir des capteurs.
- Suivi de trajets en arrière-plan et historique cartographié.
- Marketplace de récompenses : portails partenaires, codes promo, cadeaux physiques.
- Gamification : streaks, classements, dashboard CO₂, quiz éducatifs.
