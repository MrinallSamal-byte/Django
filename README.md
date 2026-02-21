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
| 1 | **Basics** — Django introduction, MVT architecture, framework comparison | [Part 1: Basics](TUTORIAL.md#part-1-basics) |
| 2 | **Installation & Setup** — Python, virtual environments, MySQL configuration | [Part 2: Installation & Setup](TUTORIAL.md#part-2-installation--setup) |
| 3 | **Django Fundamentals** — Projects vs apps, settings, URL routing | [Part 3: Django Fundamentals](TUTORIAL.md#part-3-django-fundamentals) |
| 4 | **Models & Databases** — Models, fields, relationships, migrations, QuerySet API | [Part 4: Models & Databases](TUTORIAL.md#part-4-models--databases) |
| 5 | **Views & Templates** — FBVs, CBVs, template language, inheritance, static files | [Part 5: Views & Templates](TUTORIAL.md#part-5-views--templates) |
| 6 | **Forms & User Input** — Django forms, ModelForms, validation, file uploads | [Part 6: Forms & User Input](TUTORIAL.md#part-6-forms--user-input) |
| 7 | **Authentication & Security** — Users, permissions, CSRF/XSS protection, HTTPS | [Part 7: Authentication & Security](TUTORIAL.md#part-7-authentication--security) |
| 8 | **Performance Optimization** — Query optimization, caching, pagination, indexing | [Part 8: Performance Optimization](TUTORIAL.md#part-8-performance-optimization) |
| 9 | **Advanced Features** — DRF, signals, management commands, middleware, Celery | [Part 9: Advanced Features](TUTORIAL.md#part-9-advanced-features) |
| 10 | **Real-World Projects & Deployment** — Task manager, blog, Gunicorn, Docker | [Part 10: Real-World Projects & Deployment](TUTORIAL.md#part-10-real-world-projects--deployment) |

Additional sections: [Practice Exercises](TUTORIAL.md#practice-exercises) · [Cheat Sheet](TUTORIAL.md#cheat-sheet) · [Further Reading](TUTORIAL.md#further-reading)