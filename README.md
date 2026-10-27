# OrderFlow

OrderFlow is a small web application for a furniture workshop. The workshop can manage its catalog
(products, categories and materials), customers can send inquiries for custom orders, and people can
leave reviews for the products.

Built with **Django 5.2** as an individual project for the Django Basics course at SoftUni.

## Features

- **Catalog** – full CRUD for products, categories and materials
- **Inquiries** – customers send an inquiry for a product with quantity and description; inquiries have a status (New, In Progress, Quoted, Completed)
- **Reviews** – full CRUD for product reviews with a rating from 1 to 5
- Delete confirmation page for every model
- Form validation with custom error messages, labels, help texts and placeholders
- Read-only field (`created_at`) in the product edit form
- Pagination for inquiries and reviews
- Custom template filter `euro` for showing product prices
- Base template with reusable partials (navbar, footer, pagination)
- Custom 404 page
- Navigation bar on every page – all pages are reachable through links

## Project structure

| App | Responsibility | Models |
|-----|----------------|--------|
| `catalog` | Products and everything they are made of | `Product`, `Category`, `Material` |
| `orders` | Customer inquiries for products | `Inquiry` |
| `reviews` | Product reviews | `Review` |

### Relationships

- `Product` → `Category` – many-to-one (ForeignKey)
- `Product` ↔ `Material` – many-to-many
- `Inquiry` → `Product` – many-to-one
- `Review` → `Product` – many-to-one

```
orderflowmanagement/
├── catalog/              # products, categories, materials (+ custom template filter)
├── orders/               # inquiries
├── reviews/              # reviews
├── orderflowmanagement/  # project settings and main urls
├── static/css/           # styles
├── templates/            # base.html, partials/, 404.html and templates for every app
├── requirements.txt
└── .env.example
```

## Requirements

- Python 3.11+
- PostgreSQL

## Installation

1. Clone the repository

   ```bash
   git clone <repo-url>
   cd orderflowmanagement
   ```

2. Create and activate a virtual environment

   ```bash
   python -m venv .venv
   .venv\Scripts\activate        # Windows
   source .venv/bin/activate     # Linux / macOS
   ```

3. Install the dependencies

   ```bash
   pip install -r requirements.txt
   ```

4. Create an empty PostgreSQL database (for example `orderflowapp`)

   ```sql
   CREATE DATABASE orderflowapp;
   ```

5. Create a `.env` file in the project root (next to `manage.py`). You can copy `.env.example` and fill in your values.

6. Apply the migrations

   ```bash
   python manage.py migrate
   ```

7. Start the server

   ```bash
   python manage.py runserver
   ```

8. Open http://127.0.0.1:8000/products/

## Environment variables

All of them are read from the `.env` file in the project root.

| Variable | Description | Example |
|----------|-------------|---------|
| `SECRET_KEY` | Django secret key | any long random string |
| `DB_NAME` | PostgreSQL database name | `orderflowapp` |
| `DB_USER` | PostgreSQL user | `postgres` |
| `DB_PASSWORD` | Password for the PostgreSQL user | `your-password` |
| `DB_HOST` | Database host | `127.0.0.1` |
| `DB_PORT` | Database port | `5432` |

Example `.env`:

```
SECRET_KEY=change-me-to-something-long-and-random
DB_NAME=orderflowapp
DB_USER=postgres
DB_PASSWORD=your-password
DB_HOST=127.0.0.1
DB_PORT=5432
```

## How to use it

The database starts empty. Everything can be created from the UI through the navigation bar:

1. **Categories** → Add Category
2. **Materials** → Add material
3. **Products** → Add Product (choose a category, materials and an image)
4. **Inquiries** → New Inquiry (choose a product)
5. **Reviews** → Create Review (choose a product)

Create categories and materials first, because a product needs them. Inquiries and reviews need at least one product.

## Main pages

| Page | URL |
|------|-----|
| Products | `/products/` |
| Categories | `/categories/` |
| Materials | `/materials/` |
| Inquiries | `/inquiries/` |
| Reviews | `/reviews/` |
