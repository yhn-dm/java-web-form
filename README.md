# Tea shop — Spring Boot JPA

[![Java](https://img.shields.io/badge/Java-17+-ED8B00?logo=openjdk)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?logo=springboot)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8+-4479A1?logo=mysql)](https://www.mysql.com/)
[![Maven](https://img.shields.io/badge/Maven-3.x-C71A36?logo=apache-maven)](https://maven.apache.org/)

Small web app to manage a tea shop inventory: CRUD, pagination and CSV export. Built with Spring Boot, JPA, Thymeleaf and MySQL — originally an exercise to get a full stack (backend + frontend) around a single **Product** entity.

---

## What it does

- **Business side:** manage a tea shop’s stock (add, edit, delete, list, export).
- **Learning goals:** classic Spring Boot layering (Entity, Repository, Service, Controller), Spring Data JPA + MySQL, Thymeleaf with server-side validation, plus pagination and CSV export.

---

## User flow

1. View the tea list (paginated table).
2. Add a new product or edit / delete an existing one.
3. Export the full list as CSV.

---

## Tech stack

- **Backend:** Java, Spring Boot, Spring Web, Spring Data JPA, Hibernate
- **Database:** MySQL
- **Frontend:** Thymeleaf, HTML, Tailwind CSS (CDN)
- **Build:** Maven

---

## Quick start

You’ll need Java 17+, Maven 3.x, and MySQL 8+ (or equivalent).

```bash
# 1. Clone
git clone https://github.com/yhn-dm/java-web-form.git
cd java-web-form

# 2. Create the DB (in MySQL)
# CREATE DATABASE boutique_thes;

# 3. Set your MySQL password in src/main/resources/application.properties
# spring.datasource.password=your_password

# 4. Run
mvn spring-boot:run
```

Then open [http://localhost:8080/](http://localhost:8080/).

---

## Configuration

Relevant bits in `application.properties`:

| Property | Purpose |
|----------|---------|
| `spring.datasource.url` | `jdbc:mysql://localhost:3306/boutique_thes` |
| `spring.datasource.username` | `root` (change if needed) |
| `spring.datasource.password` | Set it for your local setup |
| `spring.jpa.hibernate.ddl-auto` | `update` — tables are created/updated on startup |
| `server.port` | `8080` |

---

## Data model

Single table: **`produit`**.

| Field | Notes |
|-------|--------|
| `id` | Auto-increment primary key |
| `nom` | Required |
| `typeThe` | Tea type (e.g. Vert, Noir, Oolong, Blanc, Pu-erh) |
| `origine` | Country of origin |
| `prix` | Between 5 and 100 (€) |
| `quantiteStock` | Integer ≥ 0 |
| `description` | Text |
| `dateReception` | Set automatically on insert if not provided |

---

## Architecture

Pretty standard: **Entity** (`Produit`) → **Repository** (`ProduitRepository`, JpaRepository) → **Service** (`ProduitService`, business logic) → **Controller** (`ProduitController`, routes and Thymeleaf views).

---

## Routes

| Method | URL | What it does |
|--------|-----|----------------|
| GET | `/` | Paginated product list (query params: `page`, `size`) |
| GET | `/nouveau` | Add form |
| GET | `/modifier/{id}` | Edit form |
| POST | `/enregistrer` | Save (create or update) |
| GET | `/supprimer/{id}` | Delete (with JS confirm) |
| GET | `/export/csv` | Download list as CSV |

---

## Templates

- **`index.html`** — Product table, pagination, edit/delete buttons, CSV export.
- **`formulaire-produit.html`** — Single form for add and edit; validation errors shown there.

---

## Features

- Full CRUD on products.
- Backend pagination (Spring Data) with UI controls.
- CSV export (works with Excel / LibreOffice).
- Server-side validation and a confirmation step before delete.

---

## UI

Table view for the list and a form for add/edit. Custom “tea” colour palette with Tailwind and Inter font. Nothing fancy.

---

## Troubleshooting

- **MySQL connection failed:** make sure the `boutique_thes` database exists and `spring.datasource.password` in `application.properties` is correct.
- **Port 8080 in use:** change `server.port` in `application.properties` or stop whatever’s using it.
- **Tables missing:** with `ddl-auto=update`, Hibernate creates/updates them on startup — check the SQL in the logs if something’s off.

---

## Possible next steps

- Search and filters (by type, origin, price).
- Add Spring Security for auth.
- Expose a REST API alongside the Thymeleaf pages.
- Unit and integration tests.
