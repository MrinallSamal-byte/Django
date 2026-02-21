# Django

This repository contains a comprehensive Django tutorial using MySQL as the database.

## Installation

### Prerequisites

- Python 3.8 or higher
- MySQL 5.7 or higher
- pip (Python package manager)

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/MrinallSamal-byte/Django.git
   cd Django
   ```

2. **Create and activate a virtual environment**

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # Linux/macOS
   venv\Scripts\activate      # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install django mysqlclient
   ```

4. **Set up MySQL**

   Create a database and user in MySQL:

   ```sql
   CREATE DATABASE mydatabase CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
   GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
   FLUSH PRIVILEGES;
   ```

5. **Run migrations and start the server**

   ```bash
   python manage.py migrate
   python manage.py runserver
   ```

## Tutorial Contents

The full tutorial is in [TUTORIAL.md](TUTORIAL.md). It covers the following parts:

| Part | Topic | Link |
|------|-------|------|
| 1 | **Basics** — Django introduction, environment setup, project structure | [Part 1: Basics](TUTORIAL.md#part-1-basics) |
| 2 | **Models and Databases** — MySQL configuration, models, migrations, ORM | [Part 2: Models and Databases](TUTORIAL.md#part-2-models-and-databases) |
| 3 | **Views and URLs** — Function-based views, class-based views, URL routing | [Part 3: Views and URLs](TUTORIAL.md#part-3-views-and-urls) |
| 4 | **Templates** — Template language, inheritance, static files | [Part 4: Templates](TUTORIAL.md#part-4-templates) |
| 5 | **Forms and Validation** — Django forms, ModelForms, custom validation | [Part 5: Forms and Validation](TUTORIAL.md#part-5-forms-and-validation) |
| 6 | **Authentication and Authorization** — Users, login/logout, permissions | [Part 6: Authentication and Authorization](TUTORIAL.md#part-6-authentication-and-authorization) |
| 7 | **Django Admin** — Registering models, customizing the admin interface | [Part 7: Django Admin](TUTORIAL.md#part-7-django-admin) |
| 8 | **REST APIs** — Django REST Framework, serializers, viewsets | [Part 8: REST APIs with Django REST Framework](TUTORIAL.md#part-8-rest-apis-with-django-rest-framework) |
| 9 | **Testing** — Unit tests, integration tests, testing with MySQL | [Part 9: Testing](TUTORIAL.md#part-9-testing) |
| 10 | **Deployment** — Production settings, Gunicorn, Nginx | [Part 10: Deployment](TUTORIAL.md#part-10-deployment) |

Additional sections: [Exercises](TUTORIAL.md#exercises) · [Projects](TUTORIAL.md#projects) · [Cheat Sheet](TUTORIAL.md#cheat-sheet) · [Further Reading](TUTORIAL.md#further-reading)