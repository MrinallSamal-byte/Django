# Django

This repository contains a comprehensive Django tutorial using MySQL as the database.

## Installation

### Prerequisites

- **Python 3.10+**
- **MySQL 8.0+**
- **pip** (Python package manager)

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/MrinallSamal-byte/Django.git
   cd Django
   ```

2. **Create and activate a virtual environment**

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # Linux / macOS
   venv\Scripts\activate      # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install django mysqlclient
   ```

   > On Ubuntu/Debian you may first need:
   > `sudo apt-get install python3-dev default-libmysqlclient-dev build-essential`

4. **Create a MySQL database**

   ```sql
   CREATE DATABASE my_database CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   ```

5. **Configure the database** in `settings.py` (see [Configuring MySQL](TUTORIAL.md#configuring-mysql) in the tutorial).

6. **Run migrations and start the server**

   ```bash
   python manage.py migrate
   python manage.py runserver
   ```

## Tutorial Contents

All tutorial material is in [TUTORIAL.md](TUTORIAL.md). Below is a high-level overview with links to each section:

| Part | Topics |
|---|---|
| [Part 1: Basics](TUTORIAL.md#part-1-basics) | What is Django, environment setup, creating a project, dev server |
| [Part 2: Models and Databases](TUTORIAL.md#part-2-models-and-databases) | MySQL configuration, defining models, migrations, ORM |
| [Part 3: Views and URLs](TUTORIAL.md#part-3-views-and-urls) | Function-based views, class-based views, URL routing |
| [Part 4: Templates](TUTORIAL.md#part-4-templates) | Template language, inheritance, static files |
| [Part 5: Forms](TUTORIAL.md#part-5-forms) | Django forms, model forms, validation |
| [Part 6: Authentication and Authorization](TUTORIAL.md#part-6-authentication-and-authorization) | User model, login/logout, permissions |
| [Part 7: Django Admin](TUTORIAL.md#part-7-django-admin) | Registering models, customizing the admin |
| [Part 8: REST APIs with Django REST Framework](TUTORIAL.md#part-8-rest-apis-with-django-rest-framework) | Serializers, API views, API authentication |
| [Part 9: Testing](TUTORIAL.md#part-9-testing) | Unit tests, view tests, test client |
| [Part 10: Deployment](TUTORIAL.md#part-10-deployment) | Production prep, Gunicorn + Nginx |

Additional sections: [Exercises](TUTORIAL.md#exercises) · [Projects](TUTORIAL.md#projects) · [Cheat Sheet](TUTORIAL.md#cheat-sheet) · [Further Reading](TUTORIAL.md#further-reading)