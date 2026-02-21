# Django

This repository contains a comprehensive Django tutorial using MySQL as the database.

## Installation

### Prerequisites

- **Python 3.8+** — [python.org/downloads](https://www.python.org/downloads/)
- **MySQL 5.7+** — [dev.mysql.com/downloads](https://dev.mysql.com/downloads/mysql/)
- **pip** — included with Python 3.4+

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/MrinallSamal-byte/Django.git
   cd Django
   ```

2. **Create and activate a virtual environment**

   ```bash
   # Linux/macOS
   python3 -m venv venv
   source venv/bin/activate

   # Windows (Command Prompt)
   python -m venv venv
   venv\Scripts\activate

   # Windows (PowerShell)
   python -m venv venv
   venv\Scripts\Activate.ps1
   ```

3. **Install Python dependencies**

   ```bash
   pip install django mysqlclient
   ```

   > If `mysqlclient` fails to install, install the MySQL development headers first:
   > ```bash
   > # Ubuntu/Debian
   > sudo apt install libmysqlclient-dev
   > # macOS (Homebrew)
   > brew install mysql pkg-config
   > ```

4. **Install and start MySQL server**

   ```bash
   # Ubuntu/Debian
   sudo apt install mysql-server
   sudo systemctl start mysql

   # macOS (Homebrew)
   brew install mysql
   brew services start mysql
   ```

5. **Create the database and user**

   ```sql
   CREATE DATABASE mydatabase CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
   GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
   FLUSH PRIVILEGES;
   ```

6. **Run migrations and start the server**

   ```bash
   python manage.py migrate
   python manage.py runserver
   ```

## Tutorial Contents

The full tutorial is in [TUTORIAL.md](TUTORIAL.md). Click any topic below to jump directly to that section:

| Part | Topic | Key Sections |
|------|-------|--------------|
| 1 | [**Basics**](TUTORIAL.md#part-1-basics) | [What is Django?](TUTORIAL.md#what-is-django) · [MVT Architecture](TUTORIAL.md#the-mvt-architecture) · [Django vs Other Frameworks](TUTORIAL.md#django-vs-other-frameworks) |
| 2 | [**Installation & Setup**](TUTORIAL.md#part-2-installation--setup) | [Installing Python](TUTORIAL.md#installing-python) · [Virtual Environments](TUTORIAL.md#setting-up-a-virtual-environment) · [Django & MySQL Client](TUTORIAL.md#installing-django-and-mysql-client) · [Configuring MySQL](TUTORIAL.md#configuring-mysql) |
| 3 | [**Django Fundamentals**](TUTORIAL.md#part-3-django-fundamentals) | [Project vs App](TUTORIAL.md#project-vs-app) · [Settings](TUTORIAL.md#settings-deep-dive) · [Request/Response Cycle](TUTORIAL.md#the-requestresponse-cycle) · [URL Routing](TUTORIAL.md#url-routing) |
| 4 | [**Models & Databases**](TUTORIAL.md#part-4-models--databases) | [Defining Models](TUTORIAL.md#defining-models) · [Field Types](TUTORIAL.md#field-types-and-options) · [Relationships](TUTORIAL.md#relationships) · [Migrations](TUTORIAL.md#migrations) · [QuerySet API](TUTORIAL.md#queryset-api) · [MySQL SQL Output](TUTORIAL.md#viewing-mysql-query-output-via-the-orm) · [MySQL Errors](TUTORIAL.md#handling-mysql-specific-errors) |
| 5 | [**Views & Templates**](TUTORIAL.md#part-5-views--templates) | [Function-Based Views](TUTORIAL.md#function-based-views) · [Class-Based Views](TUTORIAL.md#class-based-views) · [Template Language](TUTORIAL.md#template-language) · [Inheritance](TUTORIAL.md#template-inheritance) · [Static Files](TUTORIAL.md#static-files-and-media) |
| 6 | [**Forms & User Input**](TUTORIAL.md#part-6-forms--user-input) | [Django Forms](TUTORIAL.md#django-forms) · [ModelForms](TUTORIAL.md#modelforms) · [Validation](TUTORIAL.md#validation) · [File Uploads](TUTORIAL.md#file-uploads) |
| 7 | [**Authentication & Security**](TUTORIAL.md#part-7-authentication--security) | [User Auth](TUTORIAL.md#user-authentication) · [Permissions](TUTORIAL.md#permissions-and-groups) · [CSRF/XSS/SQL Injection](TUTORIAL.md#csrf-xss-and-sql-injection-protection) · [HTTPS](TUTORIAL.md#https-and-security-middleware) |
| 8 | [**Performance Optimization**](TUTORIAL.md#part-8-performance-optimization) | [Query Optimization](TUTORIAL.md#database-query-optimization) · [Caching](TUTORIAL.md#caching) · [Pagination](TUTORIAL.md#pagination) · [MySQL Indexing](TUTORIAL.md#database-indexing) |
| 9 | [**Advanced Features**](TUTORIAL.md#part-9-advanced-features) | [REST Framework](TUTORIAL.md#django-rest-framework) · [Signals](TUTORIAL.md#signals) · [Management Commands](TUTORIAL.md#custom-management-commands) · [Middleware](TUTORIAL.md#middleware) · [Celery](TUTORIAL.md#celery-and-async-tasks) · [Internationalization](TUTORIAL.md#internationalization) |
| 10 | [**Real-World Projects & Deployment**](TUTORIAL.md#part-10-real-world-projects--deployment) | [Task Manager](TUTORIAL.md#project-task-manager) · [Blog Platform](TUTORIAL.md#project-blog-platform) · [E-Commerce Store](TUTORIAL.md#project-e-commerce-store) · [Gunicorn & Nginx](TUTORIAL.md#deploying-with-gunicorn-and-nginx) · [Docker + MySQL](TUTORIAL.md#docker-deployment) |
| — | [**Common Mistakes**](TUTORIAL.md#common-mistakes) | [Migration Mistakes](TUTORIAL.md#migration-mistakes) · [Insecure Settings](TUTORIAL.md#insecure-settings) · [Inefficient Queries](TUTORIAL.md#inefficient-queries) · [Deployment Pitfalls](TUTORIAL.md#deployment-pitfalls) |
| — | [**Comparisons**](TUTORIAL.md#comparisons) | [Django vs Flask vs FastAPI](TUTORIAL.md#django-vs-flask-vs-fastapi) · [MySQL vs NoSQL](TUTORIAL.md#mysql-vs-nosql-databases) · [Scalability](TUTORIAL.md#scalability-considerations) |

**Quick links:** [Practice Exercises](TUTORIAL.md#practice-exercises) · [Cheat Sheet](TUTORIAL.md#cheat-sheet) · [MySQL Quick Reference](TUTORIAL.md#mysql-quick-reference) · [Further Reading](TUTORIAL.md#further-reading)