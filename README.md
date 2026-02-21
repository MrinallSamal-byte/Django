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
| 2 | [**Installation & Setup**](TUTORIAL.md#part-2-installation--setup) | [Installing Python](TUTORIAL.md#installing-python) · [Virtual Environments](TUTORIAL.md#setting-up-a-virtual-environment) · [Django & MySQL Client](TUTORIAL.md#installing-django-and-mysql-client) · [Creating Your First Project](TUTORIAL.md#creating-your-first-project) · [Configuring MySQL](TUTORIAL.md#configuring-mysql) |
| 3 | [**Django Fundamentals**](TUTORIAL.md#part-3-django-fundamentals) | [Project vs App](TUTORIAL.md#project-vs-app) · [Settings Deep Dive](TUTORIAL.md#settings-deep-dive) · [Request/Response Cycle](TUTORIAL.md#the-requestresponse-cycle) · [URL Routing](TUTORIAL.md#url-routing) · [Admin Site](TUTORIAL.md#the-admin-site) · [Sessions](TUTORIAL.md#sessions-framework) · [Messages](TUTORIAL.md#messages-framework) · [Context Processors](TUTORIAL.md#context-processors) |
| 4 | [**Models & Databases**](TUTORIAL.md#part-4-models--databases) | [Defining Models](TUTORIAL.md#defining-models) · [Field Types](TUTORIAL.md#field-types-and-options) · [Relationships](TUTORIAL.md#relationships) · [Migrations](TUTORIAL.md#migrations) · [QuerySet API](TUTORIAL.md#queryset-api) · [Raw SQL](TUTORIAL.md#raw-sql-and-database-functions) · [Model Inheritance](TUTORIAL.md#model-inheritance) · [Custom Model Fields](TUTORIAL.md#custom-model-fields) · [Generic Relations](TUTORIAL.md#generic-relations-and-the-contenttypes-framework) · [Fixtures](TUTORIAL.md#fixtures) |
| 5 | [**Views & Templates**](TUTORIAL.md#part-5-views--templates) | [Function-Based Views](TUTORIAL.md#function-based-views) · [Class-Based Views](TUTORIAL.md#class-based-views) · [Template Language](TUTORIAL.md#template-language) · [Template Inheritance](TUTORIAL.md#template-inheritance) · [Static Files & Media](TUTORIAL.md#static-files-and-media) · [Canonical URLs](TUTORIAL.md#canonical-urls-for-models) · [SEO-Friendly URLs](TUTORIAL.md#seo-friendly-urls) · [Custom Template Tags](TUTORIAL.md#custom-template-tags-and-filters) · [CBV Mixins](TUTORIAL.md#class-based-view-mixins) |
| 6 | [**Forms & User Input**](TUTORIAL.md#part-6-forms--user-input) | [Django Forms](TUTORIAL.md#django-forms) · [ModelForms](TUTORIAL.md#modelforms) · [Validation](TUTORIAL.md#validation) · [File Uploads](TUTORIAL.md#file-uploads) · [Formsets](TUTORIAL.md#formsets) · [Cleaning Form Fields](TUTORIAL.md#cleaning-form-fields) |
| 7 | [**Authentication & Security**](TUTORIAL.md#part-7-authentication--security) | [User Auth](TUTORIAL.md#user-authentication) · [Permissions & Groups](TUTORIAL.md#permissions-and-groups) · [CSRF/XSS/SQL Injection](TUTORIAL.md#csrf-xss-and-sql-injection-protection) · [HTTPS & Security](TUTORIAL.md#https-and-security-middleware) · [Built-in Auth Views](TUTORIAL.md#built-in-authentication-views) · [User Profiles](TUTORIAL.md#user-profiles-and-extending-the-user-model) · [Custom User Model](TUTORIAL.md#custom-user-model) · [Custom Auth Backends](TUTORIAL.md#custom-authentication-backends) · [Social Auth](TUTORIAL.md#social-authentication) |
| 8 | [**Performance Optimization**](TUTORIAL.md#part-8-performance-optimization) | [Query Optimization](TUTORIAL.md#database-query-optimization) · [Caching](TUTORIAL.md#caching) · [Pagination](TUTORIAL.md#pagination) · [MySQL Indexing](TUTORIAL.md#database-indexing) · [Redis](TUTORIAL.md#redis) · [Redisboard](TUTORIAL.md#monitoring-redis-with-django-redisboard) · [Memcached](TUTORIAL.md#memcached) · [Cache Levels](TUTORIAL.md#cache-levels) · [Debug Toolbar](TUTORIAL.md#django-debug-toolbar) |
| 9 | [**Advanced Features**](TUTORIAL.md#part-9-advanced-features) | [DRF](TUTORIAL.md#django-rest-framework) · [Parsers & Renderers](TUTORIAL.md#drf-parsers-and-renderers) · [Nested Serializers](TUTORIAL.md#nested-serializers-in-drf) · [Method Fields](TUTORIAL.md#serializer-method-fields-in-drf) · [Signals](TUTORIAL.md#signals) · [Denormalizing Counts](TUTORIAL.md#denormalizing-counts-with-signals) · [Management Commands](TUTORIAL.md#custom-management-commands) · [Middleware](TUTORIAL.md#middleware) · [Celery](TUTORIAL.md#celery-and-async-tasks) · [Flower](TUTORIAL.md#monitoring-celery-with-flower) · [i18n](TUTORIAL.md#internationalization) · [Sitemaps](TUTORIAL.md#sitemaps) · [RSS Feeds](TUTORIAL.md#rss-feeds) · [Full-Text Search](TUTORIAL.md#full-text-search) · [Sending Emails](TUTORIAL.md#sending-emails) · [PDF Generation](TUTORIAL.md#pdf-generation) · [CSV Export](TUTORIAL.md#csv-export) · [Stripe Payments](TUTORIAL.md#payment-integration-stripe) · [Tagging](TUTORIAL.md#tagging-with-django-taggit) · [Thumbnails](TUTORIAL.md#image-handling-and-thumbnails) · [Channels & WebSockets](TUTORIAL.md#django-channels-and-websockets) · [Follow System](TUTORIAL.md#building-a-follow-system) · [Bookmarklet](TUTORIAL.md#bookmarklet-with-javascript) · [AJAX](TUTORIAL.md#asynchronous-javascript-with-django) · [Reordering via AJAX](TUTORIAL.md#reordering-modules-via-ajax) · [Coupons](TUTORIAL.md#coupon-system) · [Recommendations](TUTORIAL.md#recommendation-engine) · [Extending Admin](TUTORIAL.md#extending-the-admin-site) |
| 10 | [**Projects & Deployment**](TUTORIAL.md#part-10-real-world-projects--deployment) | [Task Manager](TUTORIAL.md#project-task-manager) · [Blog Platform](TUTORIAL.md#project-blog-platform) · [E-Commerce Store](TUTORIAL.md#project-e-commerce-store) · [E-Learning Platform](TUTORIAL.md#e-learning-platform-project) · [Student Enrollment](TUTORIAL.md#student-registration-and-enrollment) · [Gunicorn & Nginx](TUTORIAL.md#deploying-with-gunicorn-and-nginx) · [Docker](TUTORIAL.md#docker-deployment) · [Multi-Env Settings](TUTORIAL.md#managing-settings-for-multiple-environments) · [Docker Compose](TUTORIAL.md#docker-compose-in-depth) · [uWSGI & NGINX](TUTORIAL.md#serving-django-with-uwsgi-and-nginx) · [SSL/TLS](TUTORIAL.md#ssltls-certificates) · [Daphne](TUTORIAL.md#serving-django-channels-with-daphne) |
| — | [**Common Mistakes**](TUTORIAL.md#common-mistakes) | [Migration Mistakes](TUTORIAL.md#migration-mistakes) · [Insecure Settings](TUTORIAL.md#insecure-settings) · [Inefficient Queries](TUTORIAL.md#inefficient-queries) · [Deployment Pitfalls](TUTORIAL.md#deployment-pitfalls) |
| — | [**Comparisons**](TUTORIAL.md#comparisons) | [Django vs Flask vs FastAPI](TUTORIAL.md#django-vs-flask-vs-fastapi) · [MySQL vs NoSQL](TUTORIAL.md#mysql-vs-nosql-databases) · [Scalability](TUTORIAL.md#scalability-considerations) |

**Quick links:** [Practice Exercises](TUTORIAL.md#practice-exercises) · [Cheat Sheet](TUTORIAL.md#cheat-sheet) · [MySQL Quick Reference](TUTORIAL.md#mysql-quick-reference) · [MySQL Data Types](TUTORIAL.md#mysql-data-types-django--mysql) · [Further Reading](TUTORIAL.md#further-reading)