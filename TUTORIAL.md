# Django with MySQL — Comprehensive Tutorial

## Table of Contents

- [Part 1: Basics](#part-1-basics)
  - [What is Django?](#what-is-django)
  - [The MVT Architecture](#the-mvt-architecture)
  - [Django vs Other Frameworks](#django-vs-other-frameworks)
- [Part 2: Installation &amp; Setup](#part-2-installation--setup)
  - [Installing Python](#installing-python)
  - [Setting Up a Virtual Environment](#setting-up-a-virtual-environment)
  - [Installing Django and MySQL Client](#installing-django-and-mysql-client)
  - [Creating Your First Project](#creating-your-first-project)
  - [Configuring MySQL](#configuring-mysql)
- [Part 3: Django Fundamentals](#part-3-django-fundamentals)
  - [Project vs App](#project-vs-app)
  - [Settings Deep Dive](#settings-deep-dive)
  - [The Request/Response Cycle](#the-requestresponse-cycle)
  - [URL Routing](#url-routing)
- [Part 4: Models &amp; Databases](#part-4-models--databases)
  - [Defining Models](#defining-models)
  - [Field Types and Options](#field-types-and-options)
  - [Relationships](#relationships)
  - [Migrations](#migrations)
  - [QuerySet API](#queryset-api)
  - [Raw SQL and Database Functions](#raw-sql-and-database-functions)
- [Part 5: Views &amp; Templates](#part-5-views--templates)
  - [Function-Based Views](#function-based-views)
  - [Class-Based Views](#class-based-views)
  - [Template Language](#template-language)
  - [Template Inheritance](#template-inheritance)
  - [Static Files and Media](#static-files-and-media)
- [Part 6: Forms &amp; User Input](#part-6-forms--user-input)
  - [Django Forms](#django-forms)
  - [ModelForms](#modelforms)
  - [Validation](#validation)
  - [File Uploads](#file-uploads)
- [Part 7: Authentication &amp; Security](#part-7-authentication--security)
  - [User Authentication](#user-authentication)
  - [Permissions and Groups](#permissions-and-groups)
  - [CSRF, XSS, and SQL Injection Protection](#csrf-xss-and-sql-injection-protection)
  - [HTTPS and Security Middleware](#https-and-security-middleware)
- [Part 8: Performance Optimization](#part-8-performance-optimization)
  - [Database Query Optimization](#database-query-optimization)
  - [Caching](#caching)
  - [Pagination](#pagination)
  - [Database Indexing](#database-indexing)
- [Part 9: Advanced Features](#part-9-advanced-features)
  - [Django REST Framework](#django-rest-framework)
  - [Signals](#signals)
  - [Custom Management Commands](#custom-management-commands)
  - [Middleware](#middleware)
  - [Celery and Async Tasks](#celery-and-async-tasks)
  - [Internationalization](#internationalization)
- [Part 10: Real-World Projects &amp; Deployment](#part-10-real-world-projects--deployment)
  - [Project: Task Manager](#project-task-manager)
  - [Project: Blog Platform](#project-blog-platform)
  - [Project: E-Commerce Store](#project-e-commerce-store)
  - [Deploying with Gunicorn and Nginx](#deploying-with-gunicorn-and-nginx)
  - [Docker Deployment](#docker-deployment)
- [Common Mistakes](#common-mistakes)
  - [Migration Mistakes](#migration-mistakes)
  - [Insecure Settings](#insecure-settings)
  - [Inefficient Queries](#inefficient-queries)
  - [Deployment Pitfalls](#deployment-pitfalls)
- [Comparisons](#comparisons)
  - [Django vs Flask vs FastAPI](#django-vs-flask-vs-fastapi)
  - [MySQL vs NoSQL Databases](#mysql-vs-nosql-databases)
  - [Scalability Considerations](#scalability-considerations)
- [Practice Exercises](#practice-exercises)
- [Cheat Sheet](#cheat-sheet)
- [Further Reading](#further-reading)

---

## Part 1: Basics

### What is Django?

> 💡 **Analogy:** Think of Django as a **fully furnished apartment** — it comes with a kitchen (admin panel), plumbing (database ORM), locks on the doors (security), and a mailbox (URL routing). Flask, by contrast, is a **studio apartment with basic utilities** where you choose which furniture to add.

1️⃣ **WHY** — Django exists to solve the problem of building complex, database-driven websites quickly and cleanly. Without a framework, developers must write boilerplate code for URL routing, database access, session handling, and security — Django handles all of this out of the box.

2️⃣ **WHEN** — Use Django when you need a full-featured web application with a database backend, user authentication, an admin panel, or a REST API. It is especially well-suited for content-heavy sites, e-commerce platforms, and internal tools.

3️⃣ **HOW** — Django is a Python package you install with pip. It provides a command-line tool (`django-admin`) that generates project scaffolding, and a development server for local testing.

Key features at a glance:

- **Batteries included** — ORM, authentication, admin, forms, and more are built in.
- **Security by default** — protects against SQL injection, XSS, CSRF, and clickjacking.
- **Scalable** — powers Instagram, Pinterest, Mozilla, and Disqus.
- **Excellent documentation** — one of the best-documented frameworks available.

### The MVT Architecture

> 💡 **Analogy:** Imagine ordering food at a restaurant. The **Model** is the recipe and pantry (data), the **View** is the chef who decides what to cook and how (logic), and the **Template** is the plate presentation the waiter brings you (display). The **URL router** is the waiter taking your order to the kitchen.

Django follows the **Model-View-Template** pattern:

| Layer | Responsibility | File(s) |
|-------|---------------|---------|
| **Model** | Defines data structure and database interactions | `models.py` |
| **View** | Contains business logic, processes requests, returns responses | `views.py` |
| **Template** | Presents data as HTML (or other formats) | `templates/*.html` |

```
Browser Request
      │
      ▼
   urls.py  ──────►  views.py  ──────►  templates/
      │                  │
      │                  ▼
      │              models.py  ◄──────►  MySQL Database
      │                  │
      ▼                  ▼
Browser Response ◄── rendered HTML
```

### Django vs Other Frameworks

| Feature | Django | Flask | Express (Node.js) |
|---------|--------|-------|-------------------|
| ORM | Built-in | SQLAlchemy (separate) | Sequelize (separate) |
| Admin panel | Built-in | Flask-Admin (separate) | None built-in |
| Authentication | Built-in | Flask-Login (separate) | Passport.js (separate) |
| Learning curve | Moderate | Low | Low |
| Best for | Full applications | Microservices, small apps | Real-time, I/O heavy |

✏️ **Practice:** Visit the Django project page at [djangoproject.com](https://www.djangoproject.com/) and read the overview. Then, in your own words, write three sentences explaining why you would choose Django over Flask for a project that requires user authentication, a database, and an admin panel.

---

## Part 2: Installation & Setup

### Installing Python

1️⃣ **WHY** — Django is a Python framework — Python 3.8+ is required.

2️⃣ **WHEN** — Before any Django work begins.

3️⃣ **HOW**

```bash
# Check if Python is installed
python3 --version          # Expected: Python 3.8 or higher

# On Ubuntu/Debian, install if missing
sudo apt update && sudo apt install python3 python3-pip python3-venv

# On macOS (using Homebrew)
brew install python
```

### Setting Up a Virtual Environment

1️⃣ **WHY** — Virtual environments isolate project dependencies, preventing conflicts between projects that require different package versions.

2️⃣ **WHEN** — Always — create one for every new Django project.

3️⃣ **HOW**

```bash
# Create a virtual environment named 'venv'
python3 -m venv venv
#   python3 -m venv  → invoke the venv module
#   venv             → directory name for the environment

# Activate the environment
source venv/bin/activate        # Linux / macOS
# venv\Scripts\activate         # Windows

# Your prompt will now show (venv), confirming activation
```

### Installing Django and MySQL Client

1️⃣ **WHY** — `django` is the framework itself; `mysqlclient` is the Python driver that lets Django communicate with MySQL.

2️⃣ **WHEN** — After activating the virtual environment.

3️⃣ **HOW**

```bash
pip install django mysqlclient
#   pip install       → Python package installer
#   django            → the Django framework
#   mysqlclient       → C-based MySQL driver (fastest option)

# Verify Django installation
python -m django --version
# Expected output: 5.x.x (or your installed version)
```

> **Troubleshooting:** If `mysqlclient` fails to install, ensure MySQL development headers are present:
> ```bash
> # Ubuntu/Debian
> sudo apt install libmysqlclient-dev
> # macOS
> brew install mysql
> ```

### Creating Your First Project

1️⃣ **WHY** — The `startproject` command generates the standard project scaffold with settings, URL config, and entry points.

2️⃣ **WHEN** — Once per project.

3️⃣ **HOW**

```bash
django-admin startproject mysite
#   django-admin      → Django's command-line utility
#   startproject      → command to scaffold a new project
#   mysite            → project name (use lowercase, no hyphens)

cd mysite
python manage.py runserver
#   manage.py         → project-specific CLI wrapper
#   runserver         → starts development server on port 8000
```

Visit `http://127.0.0.1:8000/` — you should see the Django welcome page.

Generated project structure:

```
mysite/                 ← outer project directory
├── manage.py           ← CLI utility for this project
└── mysite/             ← inner Python package
    ├── __init__.py     ← marks this directory as a package
    ├── settings.py     ← all project configuration
    ├── urls.py         ← root URL routing table
    ├── asgi.py         ← ASGI entry point (async servers)
    └── wsgi.py         ← WSGI entry point (traditional servers)
```

### Configuring MySQL

> 💡 **Analogy:** If Django is the application, MySQL is the **filing cabinet** where all your data is stored. Configuring MySQL in `settings.py` is like giving Django the key and address to the cabinet.

1️⃣ **WHY** — By default Django uses SQLite. MySQL is a production-grade relational database that supports concurrent access, replication, and better performance at scale.

2️⃣ **WHEN** — When building any application intended for production or multi-user environments.

3️⃣ **HOW**

First, create the database in MySQL:

```sql
CREATE DATABASE mydatabase
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;
-- utf8mb4 supports full Unicode including emojis

CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';
FLUSH PRIVILEGES;
```

Then edit `mysite/settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        #   ENGINE   → tells Django which database adapter to use

        'NAME': 'mydatabase',
        #   NAME     → the database name created above

        'USER': 'myuser',
        #   USER     → MySQL username

        'PASSWORD': 'mypassword',
        #   PASSWORD → MySQL password (use env vars in production!)

        'HOST': '127.0.0.1',
        #   HOST     → database server address

        'PORT': '3306',
        #   PORT     → MySQL default port

        'OPTIONS': {
            'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
            #   Enforces strict SQL mode for data integrity
        },
    }
}
```

> **Security tip:** Never hard-code credentials. Use environment variables:
> ```python
> import os
> DATABASES = {
>     'default': {
>         'ENGINE': 'django.db.backends.mysql',
>         'NAME': os.environ.get('DB_NAME', 'mydatabase'),
>         'USER': os.environ.get('DB_USER', 'myuser'),
>         'PASSWORD': os.environ.get('DB_PASSWORD', ''),
>         'HOST': os.environ.get('DB_HOST', '127.0.0.1'),
>         'PORT': os.environ.get('DB_PORT', '3306'),
>     }
> }
> ```

Verify the connection:

```bash
python manage.py migrate
# If successful, Django creates its default tables in MySQL
```

✏️ **Practice:** Set up a complete Django development environment from scratch: install Python, create a virtual environment, install Django and mysqlclient, create a MySQL database called `tutorial_db`, configure `settings.py` to connect to it, and run `migrate`. Verify by opening the Django shell (`python manage.py shell`) and running `from django.db import connection; cursor = connection.cursor(); cursor.execute("SELECT VERSION()"); print(cursor.fetchone())` to confirm the MySQL connection.

---

## Part 3: Django Fundamentals

### Project vs App

> 💡 **Analogy:** A Django **project** is like a shopping mall — it is the whole building. Each **app** is a shop inside the mall (bakery, bookstore, salon). Each shop can operate independently or be moved to a different mall.

1️⃣ **WHY** — Django separates concerns into *projects* (the whole site) and *apps* (reusable components). This keeps code modular and testable.

2️⃣ **WHEN** — Every feature or domain area should be its own app (e.g., `blog`, `accounts`, `api`).

3️⃣ **HOW**

```bash
python manage.py startapp blog
#   startapp → creates an app directory with models, views, tests, etc.
#   blog     → app name
```

Generated app structure:

```
blog/
├── __init__.py
├── admin.py        ← register models with the admin site
├── apps.py         ← app configuration
├── migrations/     ← database migration files
│   └── __init__.py
├── models.py       ← data models
├── tests.py        ← unit tests
└── views.py        ← request handlers
```

Register the app in `settings.py`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',                          # ← add your app here
]
```

### Settings Deep Dive

Key settings every developer should know:

```python
# settings.py — annotated highlights

DEBUG = True
#   True  → show detailed error pages (development only)
#   False → return generic error pages (production)

ALLOWED_HOSTS = ['localhost', '127.0.0.1']
#   List of hostnames this site can serve
#   Must be set when DEBUG = False

SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY', 'fallback-dev-key')
#   Cryptographic key used for sessions, tokens, etc.
#   MUST be kept secret in production

LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'UTC'
USE_TZ = True
#   USE_TZ = True → store datetimes as UTC in the database
```

### The Request/Response Cycle

1️⃣ **WHY** — Understanding the cycle helps you debug issues and write efficient middleware.

2️⃣ **WHEN** — Useful knowledge from day one — critical for advanced work.

3️⃣ **HOW** — Every HTTP request flows through these stages:

```
1. Browser sends HTTP request
2. Django's WSGI/ASGI handler receives it
3. Middleware processes the request (security, sessions, etc.)
4. URL resolver matches the URL to a view function/class
5. View runs business logic, queries the database via models
6. View renders a template (or returns JSON)
7. Middleware processes the response
8. Django sends HTTP response to browser
```

### URL Routing

1️⃣ **WHY** — URL routing maps browser URLs to Python view functions — it is the entry point for every request.

2️⃣ **WHEN** — Every time you add a new page or API endpoint.

3️⃣ **HOW**

```python
# blog/urls.py
from django.urls import path
from . import views

app_name = 'blog'                  # namespace for reverse lookups
#   app_name → avoids naming collisions between apps

urlpatterns = [
    path('', views.post_list, name='post_list'),
    #   ''           → matches /blog/ (the root of this app's URLs)
    #   views.post_list → calls the post_list function in views.py
    #   name='post_list' → allows {% url 'blog:post_list' %} in templates

    path('<int:pk>/', views.post_detail, name='post_detail'),
    #   <int:pk>     → captures an integer from the URL as 'pk'
    #   Example: /blog/5/ → calls post_detail(request, pk=5)

    path('category/<slug:slug>/', views.category, name='category'),
    #   <slug:slug>  → captures a URL-safe string (letters, numbers, hyphens)
]
```

Include app URLs in the project:

```python
# mysite/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),
    #   include() → delegates URL matching to the app's urls.py
    #   All blog URLs will be prefixed with /blog/
]
```

✏️ **Practice:** Create a new Django project called `myshop` and two apps: `products` and `accounts`. Register both apps in `INSTALLED_APPS`. In `products/urls.py`, create three URL patterns: a product list at `/products/`, a product detail at `/products/<int:pk>/`, and a search at `/products/search/`. Include these in the project's root `urls.py`. Write stub views that return simple `HttpResponse` text and verify each URL works in the browser.

---

## Part 4: Models & Databases

### Defining Models

> 💡 **Analogy:** A model is a **blueprint** for a house. It describes what rooms (fields) the house has, what type each room is (CharField, IntegerField), and how houses relate to each other (ForeignKey). The ORM is the **construction crew** that reads the blueprint and builds the actual MySQL table.

1️⃣ **WHY** — Models define your data schema in Python. Django translates them into database tables automatically, so you rarely need to write raw SQL.

2️⃣ **WHEN** — Whenever you need to store or retrieve structured data.

3️⃣ **HOW**

```python
# blog/models.py
from django.db import models
from django.utils import timezone

class Category(models.Model):
    name = models.CharField(max_length=100)
    #   CharField      → short text field
    #   max_length=100 → database column is VARCHAR(100)

    slug = models.SlugField(unique=True)
    #   SlugField → URL-safe string (letters, numbers, hyphens)
    #   unique=True → no two categories can have the same slug

    class Meta:
        verbose_name_plural = 'categories'
        #   Fixes the admin panel showing "Categorys"

    def __str__(self):
        return self.name
        #   __str__ → human-readable representation (used in admin, shell, etc.)


class Post(models.Model):
    STATUS_CHOICES = [
        ('draft', 'Draft'),
        ('published', 'Published'),
    ]
    #   A list of (database_value, display_label) tuples

    title = models.CharField(max_length=200)
    slug = models.SlugField(max_length=200, unique_for_date='publish_date')
    #   unique_for_date → slug must be unique for a given publish_date

    body = models.TextField()
    #   TextField → unlimited-length text (LONGTEXT in MySQL)

    category = models.ForeignKey(
        Category,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name='posts',
    )
    #   ForeignKey        → many-to-one relationship
    #   on_delete=SET_NULL → if category is deleted, set this field to NULL
    #   null=True         → allow NULL in the database
    #   blank=True        → allow empty in forms
    #   related_name      → access posts from category: category.posts.all()

    status = models.CharField(max_length=10, choices=STATUS_CHOICES, default='draft')
    #   choices → limits allowed values; renders as a dropdown in forms

    publish_date = models.DateTimeField(default=timezone.now)
    created_at = models.DateTimeField(auto_now_add=True)
    #   auto_now_add → set once when the object is first created
    updated_at = models.DateTimeField(auto_now=True)
    #   auto_now     → updated every time .save() is called

    class Meta:
        ordering = ['-publish_date']
        #   Default ordering: newest first

    def __str__(self):
        return self.title
```

### Field Types and Options

| Field | MySQL Column | Use Case |
|-------|-------------|----------|
| `CharField(max_length=N)` | `VARCHAR(N)` | Names, titles, short text |
| `TextField()` | `LONGTEXT` | Blog posts, descriptions |
| `IntegerField()` | `INT` | Counts, quantities |
| `FloatField()` | `DOUBLE` | Prices, measurements |
| `DecimalField(max_digits, decimal_places)` | `DECIMAL` | Money (exact precision) |
| `BooleanField()` | `TINYINT(1)` | Flags (active, published) |
| `DateTimeField()` | `DATETIME(6)` | Timestamps |
| `EmailField()` | `VARCHAR(254)` | Email addresses |
| `URLField()` | `VARCHAR(200)` | Web URLs |
| `FileField(upload_to='...')` | `VARCHAR(100)` | File upload paths |
| `ImageField(upload_to='...')` | `VARCHAR(100)` | Image upload paths |
| `SlugField()` | `VARCHAR(50)` | URL-safe identifiers |
| `JSONField()` | `JSON` | Structured JSON data |

Common field options:

| Option | Meaning |
|--------|---------|
| `null=True` | Database allows NULL |
| `blank=True` | Forms allow empty values |
| `default=value` | Default value if none provided |
| `unique=True` | No duplicate values |
| `db_index=True` | Create a database index |
| `help_text='...'` | Hint displayed in forms |

### Relationships

```python
# One-to-Many: a post belongs to one category; a category has many posts
category = models.ForeignKey(Category, on_delete=models.CASCADE)
#   on_delete options:
#     CASCADE    → delete post when category is deleted
#     PROTECT    → prevent category deletion if posts exist
#     SET_NULL   → set field to NULL (requires null=True)
#     SET_DEFAULT → set field to its default value
#     DO_NOTHING → do nothing (may break referential integrity)

# Many-to-Many: a post can have many tags; a tag can be on many posts
tags = models.ManyToManyField('Tag', blank=True, related_name='posts')
#   Django automatically creates an intermediary join table

# One-to-One: each user has exactly one profile
user = models.OneToOneField(User, on_delete=models.CASCADE)
#   Access: user.profile (reverse) or profile.user (forward)
```

### Migrations

1️⃣ **WHY** — Migrations version-control your database schema. They let you evolve the schema without losing data and keep every developer's database in sync.

2️⃣ **WHEN** — Every time you change a model.

3️⃣ **HOW**

```bash
# Step 1: Generate migration files from model changes
python manage.py makemigrations blog
#   Inspects blog/models.py and creates a migration file in blog/migrations/

# Step 2: Apply migrations to the database
python manage.py migrate
#   Runs all unapplied migrations against the connected MySQL database

# Useful commands:
python manage.py showmigrations
#   Shows which migrations have been applied (marked with [X])

python manage.py sqlmigrate blog 0001
#   Displays the raw SQL that a migration will execute
```

Example MySQL output from `sqlmigrate blog 0001`:

```sql
--
-- Create model Category
--
CREATE TABLE `blog_category` (
    `id` bigint AUTO_INCREMENT NOT NULL PRIMARY KEY,
    `name` varchar(100) NOT NULL,
    `slug` varchar(50) NOT NULL UNIQUE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
--   ENGINE=InnoDB → MySQL's default transactional storage engine
--   utf8mb4       → full Unicode support (including emojis)

--
-- Create model Post
--
CREATE TABLE `blog_post` (
    `id` bigint AUTO_INCREMENT NOT NULL PRIMARY KEY,
    `title` varchar(200) NOT NULL,
    `slug` varchar(200) NOT NULL,
    `body` longtext NOT NULL,
    `status` varchar(10) NOT NULL,
    `publish_date` datetime(6) NOT NULL,
    `created_at` datetime(6) NOT NULL,
    `updated_at` datetime(6) NOT NULL,
    `category_id` bigint NULL,
    CONSTRAINT `blog_post_category_id_fk` FOREIGN KEY (`category_id`)
        REFERENCES `blog_category` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
--   datetime(6)   → microsecond precision (MySQL 5.6.4+)
--   FOREIGN KEY    → enforced referential integrity at the database level
--   bigint         → Django's default BigAutoField primary key
```

### QuerySet API

> 💡 **Analogy:** The ORM is a **translator** between Python and MySQL. You speak Python (`Post.objects.filter(status='published')`), the ORM translates it to MySQL (`SELECT * FROM blog_post WHERE status = 'published'`), executes the query, and hands you back Python objects. You never need to learn the database's language directly.

1️⃣ **WHY** — The QuerySet API is Django's interface for building database queries in Python. It is lazy (queries execute only when data is needed) and chainable.

2️⃣ **WHEN** — Whenever you read, filter, create, update, or delete data.

3️⃣ **HOW**

```python
from blog.models import Post, Category

# --- Create ---
post = Post.objects.create(
    title='My First Post',
    body='Hello, World!',
    status='published',
)
#   .create() → INSERT INTO blog_post (...) VALUES (...)

# --- Read ---
all_posts = Post.objects.all()
#   Returns a QuerySet of every Post (lazy — no query yet)

published = Post.objects.filter(status='published')
#   .filter() → adds a WHERE clause; still lazy

post = Post.objects.get(pk=1)
#   .get() → returns exactly one object; raises DoesNotExist or MultipleObjectsReturned

# --- Field lookups ---
Post.objects.filter(title__icontains='django')
#   __icontains → case-insensitive LIKE '%django%'

Post.objects.filter(publish_date__year=2026)
#   __year → EXTRACT(YEAR FROM publish_date) = 2026

Post.objects.filter(category__name='Python')
#   __ (double underscore) traverses relationships

# --- Chaining ---
results = (
    Post.objects
    .filter(status='published')          # WHERE status = 'published'
    .exclude(title__startswith='Draft')   # AND title NOT LIKE 'Draft%'
    .order_by('-publish_date')            # ORDER BY publish_date DESC
    [:10]                                 # LIMIT 10
)

# --- Update ---
Post.objects.filter(status='draft').update(status='published')
#   Bulk update — executes a single UPDATE query

# --- Delete ---
Post.objects.filter(created_at__year=2020).delete()
#   Bulk delete — executes DELETE with a WHERE clause

# --- Aggregation ---
from django.db.models import Count, Avg
Post.objects.aggregate(total=Count('id'), avg_length=Avg('body'))
#   Returns a dict: {'total': 42, 'avg_length': 350.5}

# --- Annotation ---
categories = Category.objects.annotate(post_count=Count('posts'))
#   Adds a computed 'post_count' column to each Category
for cat in categories:
    print(cat.name, cat.post_count)
```

### Raw SQL and Database Functions

1️⃣ **WHY** — Occasionally the ORM cannot express a complex query. Raw SQL is the escape hatch.

2️⃣ **WHEN** — Rarely — prefer the ORM for safety and portability. Use raw SQL only when necessary.

3️⃣ **HOW**

```python
# Raw queries (still returns model instances)
posts = Post.objects.raw('SELECT * FROM blog_post WHERE status = %s', ['published'])
#   %s placeholders are safely parameterized — never use f-strings!

# Direct database access (returns dicts/tuples)
from django.db import connection
with connection.cursor() as cursor:
    cursor.execute('SELECT COUNT(*) FROM blog_post')
    row = cursor.fetchone()
    print(row[0])
```

#### Viewing MySQL Query Output via the ORM

Use Django's `connection.queries` or the `query` attribute to see the generated MySQL SQL:

```python
from django.db import connection, reset_queries
from django.conf import settings

# Enable query logging (DEBUG must be True)
settings.DEBUG = True
reset_queries()

posts = list(Post.objects.filter(status='published').order_by('-publish_date')[:5])

# Print the generated MySQL query
print(connection.queries[-1]['sql'])
# Output:
#   SELECT `blog_post`.`id`, `blog_post`.`title`, `blog_post`.`slug`,
#          `blog_post`.`body`, `blog_post`.`status`, `blog_post`.`publish_date`,
#          `blog_post`.`created_at`, `blog_post`.`updated_at`, `blog_post`.`category_id`
#   FROM `blog_post`
#   WHERE `blog_post`.`status` = 'published'
#   ORDER BY `blog_post`.`publish_date` DESC
#   LIMIT 5
```

> **Note:** MySQL uses backtick-quoted identifiers (`` `table`.`column` ``), unlike PostgreSQL which uses double quotes.

#### MySQL EXPLAIN for Query Analysis

```python
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute(
        "EXPLAIN SELECT * FROM blog_post WHERE status = %s ORDER BY publish_date DESC",
        ['published']
    )
    for row in cursor.fetchall():
        print(row)
# Example output:
#   (1, 'SIMPLE', 'blog_post', None, 'ref', 'blog_post_status_idx',
#    'blog_post_status_idx', '42', 'const', 15, 100.0, 'Using filesort')
#
#   Key columns:
#     type='ref'       → index lookup (good)
#     key='blog_post_status_idx' → which index MySQL chose
#     rows=15          → estimated rows to scan
#     Extra='Using filesort' → MySQL must sort results (consider a composite index)
```

#### Handling MySQL-Specific Errors

```python
from django.db import IntegrityError, OperationalError

# Handle duplicate entry (e.g., unique constraint violation)
try:
    Post.objects.create(title='Duplicate', slug='existing-slug')
except IntegrityError as e:
    if 'Duplicate entry' in str(e):
        #   MySQL error 1062: Duplicate entry 'existing-slug' for key 'blog_post.slug'
        print('A post with this slug already exists.')
    else:
        raise

# Handle connection errors
try:
    Post.objects.count()
except OperationalError as e:
    error_code = e.args[0] if e.args else None
    if error_code == 2003:
        #   MySQL error 2003: Can't connect to MySQL server
        print('Cannot connect to MySQL. Is the server running?')
    elif error_code == 1045:
        #   MySQL error 1045: Access denied for user
        print('Database credentials are incorrect.')
    else:
        raise
```

✏️ **Practice:** Create a `Library` app with two models: `Author` (name, birth_date, bio) and `Book` (title, author as ForeignKey, isbn as unique CharField, price as DecimalField, published_date). Run migrations and use `sqlmigrate` to view the MySQL output. Then in the Django shell: create 3 authors and 5 books, query all books by a specific author using the reverse relationship (`author.book_set.all()`), filter books under a certain price, use `select_related('author')` to fetch books with their authors in one query, and annotate each author with their book count.

---

## Part 5: Views & Templates

### Function-Based Views

> 💡 **Analogy:** A view is like a **controller at an information desk**. A visitor (HTTP request) arrives, the controller looks up the answer (queries the database), writes it on a card (renders a template), and hands it back. FBVs are the simplest kind of controller — just a plain function.

1️⃣ **WHY** — FBVs are simple Python functions — easy to understand and debug. They are the best starting point for learning Django.

2️⃣ **WHEN** — For simple or custom logic that does not fit a generic pattern.

3️⃣ **HOW**

```python
# blog/views.py
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    """Display all published posts."""
    posts = Post.objects.filter(status='published')
    #   Query published posts from the database

    return render(request, 'blog/post_list.html', {'posts': posts})
    #   render() → combines a template with a context dict
    #   First arg: the request object
    #   Second arg: template path (relative to templates/)
    #   Third arg: context — variables available inside the template


def post_detail(request, pk):
    """Display a single post by primary key."""
    post = get_object_or_404(Post, pk=pk, status='published')
    #   get_object_or_404 → returns the object or raises Http404
    #   Equivalent to try/except Post.DoesNotExist

    return render(request, 'blog/post_detail.html', {'post': post})
```

### Class-Based Views

1️⃣ **WHY** — CBVs encapsulate common patterns (list, detail, create, update, delete) so you write less code for standard CRUD operations.

2️⃣ **WHEN** — When your view matches a common pattern. Prefer FBVs for highly custom logic.

3️⃣ **HOW**

```python
# blog/views.py
from django.views.generic import ListView, DetailView, CreateView, UpdateView, DeleteView
from django.urls import reverse_lazy
from .models import Post
from .forms import PostForm

class PostListView(ListView):
    model = Post
    #   Tells the view which model to query

    template_name = 'blog/post_list.html'
    #   Path to the template (default would be blog/post_list.html)

    context_object_name = 'posts'
    #   Variable name in the template (default is 'object_list')

    queryset = Post.objects.filter(status='published')
    #   Custom queryset — only show published posts

    paginate_by = 10
    #   Show 10 posts per page; adds page_obj to context


class PostDetailView(DetailView):
    model = Post
    template_name = 'blog/post_detail.html'
    context_object_name = 'post'


class PostCreateView(CreateView):
    model = Post
    form_class = PostForm
    template_name = 'blog/post_form.html'
    success_url = reverse_lazy('blog:post_list')
    #   reverse_lazy → resolves URL at runtime (needed at class level)
```

URL registration for CBVs:

```python
# blog/urls.py
from django.urls import path
from . import views

app_name = 'blog'

urlpatterns = [
    path('', views.PostListView.as_view(), name='post_list'),
    #   .as_view() → converts the class into a callable view function
    path('<int:pk>/', views.PostDetailView.as_view(), name='post_detail'),
    path('new/', views.PostCreateView.as_view(), name='post_create'),
]
```

### Template Language

1️⃣ **WHY** — Django's template language separates presentation from logic, enforcing clean architecture.

2️⃣ **WHEN** — Every time you render HTML.

3️⃣ **HOW**

```html
<!-- blog/templates/blog/post_list.html -->
<h1>Blog Posts</h1>

<ul>
{% for post in posts %}
    {# Loop over each post in the context variable 'posts' #}
    <li>
        <a href="{% url 'blog:post_detail' pk=post.pk %}">
            {# {% url %} → reverse URL resolution; generates /blog/5/ etc. #}
            {{ post.title }}
            {# {{ }} → output a variable's value, auto-escaped for safety #}
        </a>
        <small>{{ post.publish_date|date:"M d, Y" }}</small>
        {# |date:"..." → format a datetime using PHP-style format strings #}
    </li>
{% empty %}
    {# Shown only if the 'posts' list is empty #}
    <li>No posts yet.</li>
{% endfor %}
</ul>

{% if posts.has_next %}
    <a href="?page={{ posts.next_page_number }}">Next Page</a>
{% endif %}
```

Common template tags and filters:

| Syntax | Purpose |
|--------|---------|
| `{{ variable }}` | Output a value (auto-escaped) |
| `{% tag %}` | Logic: `if`, `for`, `block`, `extends`, `include`, `url`, `load` |
| `{# comment #}` | Template comment (not rendered) |
| `{{ value\|filter }}` | Transform a value: `date`, `length`, `default`, `truncatewords`, `lower` |

### Template Inheritance

> 💡 **Analogy:** Template inheritance is like a **company letterhead**. The base template defines the header, footer, and layout (the letterhead). Each page fills in its own content in the middle. If the company logo changes, you update it once in the letterhead and every page reflects the change.

1️⃣ **WHY** — Inheritance eliminates HTML duplication. You define a base skeleton once and override specific blocks in child templates.

2️⃣ **WHEN** — Always — even for simple sites.

3️⃣ **HOW**

Base template:

```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}My Site{% endblock %}</title>
    {% block extra_css %}{% endblock %}
    {# Child templates can inject additional CSS here #}
</head>
<body>
    <nav>
        <a href="{% url 'blog:post_list' %}">Blog</a>
        {% if user.is_authenticated %}
            <a href="{% url 'logout' %}">Logout</a>
        {% else %}
            <a href="{% url 'login' %}">Login</a>
        {% endif %}
    </nav>

    <main>
        {% block content %}{% endblock %}
        {# Each page fills in its own content #}
    </main>

    <footer>&copy; 2026 My Site</footer>
</body>
</html>
```

Child template:

```html
<!-- blog/templates/blog/post_list.html -->
{% extends "base.html" %}
{# extends → this template inherits from base.html #}

{% block title %}Blog — My Site{% endblock %}
{# Overrides the title block defined in base.html #}

{% block content %}
<h1>Blog Posts</h1>
<ul>
{% for post in posts %}
    <li>{{ post.title }}</li>
{% endfor %}
</ul>
{% endblock %}
```

### Static Files and Media

1️⃣ **WHY** — Static files (CSS, JS, images) and user-uploaded media must be served separately from templates.

2️⃣ **WHEN** — Every project needs static files. Media handling is needed when users upload content.

3️⃣ **HOW**

```python
# settings.py

STATIC_URL = '/static/'
#   URL prefix for static files

STATICFILES_DIRS = [BASE_DIR / 'static']
#   Additional directories where Django looks for static files

STATIC_ROOT = BASE_DIR / 'staticfiles'
#   Where collectstatic gathers all files for production

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
#   Upload destination for FileField / ImageField
```

Using static files in templates:

```html
{% load static %}
{# load static → makes the {% static %} tag available #}

<link rel="stylesheet" href="{% static 'css/style.css' %}">
{# Resolves to /static/css/style.css #}

<img src="{% static 'images/logo.png' %}" alt="Logo">
```

✏️ **Practice:** Build a `products` app with a `Product` model (name, description, price, image). Create: (1) a function-based list view showing all products, (2) a class-based `DetailView` for a single product, (3) a base template with a navigation bar and footer, and (4) a child template that extends the base and renders the product list. Add a CSS file in `static/css/` and include it in your base template.

---

## Part 6: Forms & User Input

### Django Forms

> 💡 **Analogy:** A Django form is like a **customs declaration card** at an airport. It defines exactly what information is needed (fields), checks that everything is valid (validation), and presents the card in a standard format (rendering). Without it, you would have to manually parse raw passenger data — messy and error-prone.

1️⃣ **WHY** — Django forms handle rendering HTML inputs, validating data, and displaying errors — reducing boilerplate and preventing common security mistakes.

2️⃣ **WHEN** — Any time you accept user input (contact forms, search bars, settings pages).

3️⃣ **HOW**

```python
# blog/forms.py
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(
        max_length=100,
        widget=forms.TextInput(attrs={'placeholder': 'Your name'}),
        #   widget → customizes the HTML element and its attributes
    )
    email = forms.EmailField()
    #   Validates that input looks like a valid email

    message = forms.CharField(
        widget=forms.Textarea(attrs={'rows': 5}),
        #   Textarea → renders as <textarea> instead of <input>
    )
```

Using the form in a view:

```python
# blog/views.py
from django.shortcuts import render, redirect
from django.core.mail import send_mail
from .forms import ContactForm

def contact(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        #   Bind submitted data to the form

        if form.is_valid():
            #   Runs all field validations and custom clean methods
            name = form.cleaned_data['name']
            #   cleaned_data → dict of validated, type-converted values
            email = form.cleaned_data['email']
            message = form.cleaned_data['message']

            send_mail(
                subject=f'Contact from {name}',
                message=message,
                from_email=email,
                recipient_list=['admin@example.com'],
            )
            return redirect('contact_success')
    else:
        form = ContactForm()
        #   Unbound form — empty, ready for user input

    return render(request, 'blog/contact.html', {'form': form})
```

Rendering in a template:

```html
<form method="post">
    {% csrf_token %}
    {# CSRF token → prevents cross-site request forgery attacks #}

    {{ form.as_p }}
    {# .as_p → renders each field wrapped in <p> tags #}
    {# Alternatives: .as_table, .as_div, or manual rendering #}

    <button type="submit">Send</button>
</form>

{# Manual rendering for full control: #}
<form method="post">
    {% csrf_token %}
    {% for field in form %}
        <div class="field">
            {{ field.label_tag }}
            {{ field }}
            {% if field.errors %}
                <span class="error">{{ field.errors.0 }}</span>
            {% endif %}
        </div>
    {% endfor %}
    <button type="submit">Send</button>
</form>
```

### ModelForms

1️⃣ **WHY** — ModelForms automatically generate form fields from a model, avoiding duplication between `models.py` and `forms.py`.

2️⃣ **WHEN** — Whenever a form directly creates or updates a model instance.

3️⃣ **HOW**

```python
# blog/forms.py
from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        #   The model to generate fields from

        fields = ['title', 'body', 'category', 'status']
        #   Explicit list of fields to include (security best practice)
        #   Never use fields = '__all__' in production

        widgets = {
            'body': forms.Textarea(attrs={'rows': 10}),
            'status': forms.Select(),
        }
        #   Override default widgets for specific fields
```

Using in a view:

```python
def post_create(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            post = form.save(commit=False)
            #   commit=False → creates model instance without saving to DB
            #   Useful when you need to set additional fields first

            post.author = request.user
            post.save()
            #   Now save to the database

            return redirect('blog:post_detail', pk=post.pk)
    else:
        form = PostForm()
    return render(request, 'blog/post_form.html', {'form': form})
```

### Validation

1️⃣ **WHY** — Validation ensures data integrity before it reaches the database. Django provides field-level, form-level, and model-level validation.

2️⃣ **WHEN** — Always — never trust user input.

3️⃣ **HOW**

```python
# blog/forms.py
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'body', 'category', 'status']

    def clean_title(self):
        """Field-level validation — runs for the 'title' field only."""
        title = self.cleaned_data['title']
        if len(title) < 5:
            raise forms.ValidationError('Title must be at least 5 characters long.')
        if Post.objects.filter(title=title).exclude(pk=self.instance.pk).exists():
            raise forms.ValidationError('A post with this title already exists.')
        return title

    def clean(self):
        """Form-level validation — runs after all field-level validations."""
        cleaned_data = super().clean()
        status = cleaned_data.get('status')
        body = cleaned_data.get('body')

        if status == 'published' and body and len(body) < 50:
            raise forms.ValidationError(
                'Published posts must have at least 50 characters in the body.'
            )
        return cleaned_data
```

### File Uploads

1️⃣ **WHY** — Many applications need user-uploaded content (images, documents, etc.).

2️⃣ **WHEN** — Profile pictures, post attachments, document management.

3️⃣ **HOW**

```python
# blog/models.py
class Post(models.Model):
    # ... other fields ...
    image = models.ImageField(upload_to='posts/%Y/%m/', blank=True)
    #   upload_to → subdirectory under MEDIA_ROOT
    #   %Y/%m/   → organizes files by year/month: media/posts/2026/01/photo.jpg
```

```python
# blog/views.py
def post_create(request):
    if request.method == 'POST':
        form = PostForm(request.POST, request.FILES)
        #   request.FILES → contains uploaded files; required for file fields
        if form.is_valid():
            form.save()
            return redirect('blog:post_list')
    else:
        form = PostForm()
    return render(request, 'blog/post_form.html', {'form': form})
```

```html
<!-- The form must use enctype="multipart/form-data" for file uploads -->
<form method="post" enctype="multipart/form-data">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Create Post</button>
</form>
```

✏️ **Practice:** Create a `ProductForm` using `ModelForm` for a `Product` model. Add custom field-level validation: the price must be positive and the name must be at least 3 characters. Create a view that handles both GET (empty form) and POST (validate and save). If valid, redirect to a product list; if invalid, re-render the form with error messages. Add an `ImageField` and ensure the form template uses `enctype="multipart/form-data"`.

---

## Part 7: Authentication & Security

### User Authentication

1️⃣ **WHY** — Most web applications need user accounts. Django's auth system provides a battle-tested implementation covering registration, login, logout, and password management.

2️⃣ **WHEN** — Any application with user-specific data or access control.

3️⃣ **HOW**

Create a superuser:

```bash
python manage.py createsuperuser
#   Prompts for username, email, and password
#   Creates a user with full admin privileges
```

Add login/logout URLs:

```python
# mysite/urls.py
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('login/', auth_views.LoginView.as_view(), name='login'),
    #   Built-in view that displays a login form and handles authentication

    path('logout/', auth_views.LogoutView.as_view(), name='logout'),
    #   Logs the user out and redirects

    path('blog/', include('blog.urls')),
]
```

```python
# settings.py
LOGIN_REDIRECT_URL = '/'        # Where to go after successful login
LOGOUT_REDIRECT_URL = '/login/' # Where to go after logout
LOGIN_URL = '/login/'           # Where to redirect unauthenticated users
```

Protecting views:

```python
# Function-based: use the decorator
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    #   If the user is not logged in, they are redirected to LOGIN_URL
    return render(request, 'dashboard.html')


# Class-based: use the mixin
from django.contrib.auth.mixins import LoginRequiredMixin

class DashboardView(LoginRequiredMixin, ListView):
    model = Post
    template_name = 'dashboard.html'
```

User registration view:

```python
# accounts/views.py
from django.contrib.auth.forms import UserCreationForm
from django.shortcuts import render, redirect

def register(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            #   Creates a new User in the database
            return redirect('login')
    else:
        form = UserCreationForm()
    return render(request, 'registration/register.html', {'form': form})
```

### Permissions and Groups

1️⃣ **WHY** — Fine-grained access control lets you restrict what different users can do.

2️⃣ **WHEN** — Multi-role applications (admin, editor, viewer, etc.).

3️⃣ **HOW**

```python
from django.contrib.auth.decorators import permission_required

@permission_required('blog.add_post', raise_exception=True)
def create_post(request):
    #   Checks that the user has the 'add_post' permission on the blog app
    #   raise_exception=True → returns 403 instead of redirecting to login
    ...
```

```python
# In templates
{% if perms.blog.add_post %}
    <a href="{% url 'blog:post_create' %}">New Post</a>
{% endif %}
```

### CSRF, XSS, and SQL Injection Protection

1️⃣ **WHY** — Web applications are targets for attacks. Django provides protection against the most common vulnerabilities by default.

2️⃣ **WHEN** — Always active — you must understand how to not accidentally disable these protections.

3️⃣ **HOW**

| Threat | Django's Protection | Your Responsibility |
|--------|-------------------|-------------------|
| **CSRF** | `{% csrf_token %}` in forms; `CsrfViewMiddleware` | Always include the token in POST forms |
| **XSS** | Template variables are auto-escaped | Use `{{ var }}`, not `{{ var\|safe }}` unless trusted |
| **SQL Injection** | ORM uses parameterized queries | Never use f-strings in `.raw()` or `.execute()` |
| **Clickjacking** | `X-Frame-Options` header via middleware | Keep `XFrameOptionsMiddleware` enabled |

### HTTPS and Security Middleware

1️⃣ **WHY** — HTTPS encrypts traffic between the browser and server. Additional headers harden the application.

2️⃣ **WHEN** — Always in production.

3️⃣ **HOW**

```python
# settings.py — production security settings

SECURE_SSL_REDIRECT = True
#   Redirect all HTTP requests to HTTPS

SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
#   Cookies only sent over HTTPS

SECURE_HSTS_SECONDS = 31536000
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True
#   HTTP Strict Transport Security — tells browsers to always use HTTPS

SECURE_CONTENT_TYPE_NOSNIFF = True
#   Prevents browsers from MIME-sniffing the content type
```

✏️ **Practice:** Add full authentication to your blog app: create a registration page using `UserCreationForm`, add login/logout views using Django's built-in auth views, and protect the post creation view with `@login_required`. Create two user groups ("Editor" and "Viewer") in the admin panel. Editors can add and edit posts; Viewers can only read. Use `{% if perms.blog.add_post %}` in templates to conditionally show the "New Post" button.

---

## Part 8: Performance Optimization

### Database Query Optimization

1️⃣ **WHY** — Unoptimized queries are the number-one cause of slow Django applications. The ORM makes it easy to accidentally issue hundreds of queries.

2️⃣ **WHEN** — Whenever pages feel slow, or when `django-debug-toolbar` shows excessive queries.

3️⃣ **HOW**

```python
# PROBLEM: N+1 queries
# This issues 1 query for posts + 1 query per post for category
posts = Post.objects.all()
for post in posts:
    print(post.category.name)    # Each access triggers a separate query!

# SOLUTION: select_related (for ForeignKey / OneToOne)
posts = Post.objects.select_related('category').all()
#   Performs a SQL JOIN — fetches posts and categories in ONE query
for post in posts:
    print(post.category.name)    # No extra query — data is already loaded

# SOLUTION: prefetch_related (for ManyToMany / reverse ForeignKey)
categories = Category.objects.prefetch_related('posts').all()
#   Performs 2 queries: one for categories, one for all related posts
#   Then matches them in Python
for category in categories:
    for post in category.posts.all():   # No extra query
        print(post.title)

# Use .only() and .defer() to limit fetched columns
posts = Post.objects.only('title', 'publish_date')
#   SELECT title, publish_date FROM blog_post
#   Other fields are loaded lazily if accessed

# Use .values() or .values_list() when you don't need model instances
titles = Post.objects.values_list('title', flat=True)
#   Returns a flat list: ['Post 1', 'Post 2', ...]
#   Much faster than loading full model instances
```

### Caching

1️⃣ **WHY** — Caching stores expensive results (database queries, API calls, rendered HTML) so they can be reused without re-computation.

2️⃣ **WHEN** — For data that doesn't change on every request (e.g., navigation menus, trending posts, settings).

3️⃣ **HOW**

```python
# settings.py — use Memcached or Redis in production
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.locmem.LocMemCache',
        #   Local memory cache — good for development
        #   Use 'django.core.cache.backends.memcached.PyMemcacheCache' or
        #   'django.core.cache.backends.redis.RedisCache' in production
    }
}
```

```python
# View-level caching
from django.views.decorators.cache import cache_page

@cache_page(60 * 15)   # Cache for 15 minutes
def post_list(request):
    posts = Post.objects.filter(status='published')
    return render(request, 'blog/post_list.html', {'posts': posts})
```

```python
# Low-level caching for fine-grained control
from django.core.cache import cache

def get_popular_posts():
    key = 'popular_posts'
    posts = cache.get(key)
    #   Try to get data from cache

    if posts is None:
        posts = list(Post.objects.filter(status='published').order_by('-views')[:10])
        cache.set(key, posts, timeout=60 * 30)
        #   Store in cache for 30 minutes

    return posts
```

### Pagination

1️⃣ **WHY** — Loading all records at once is slow and wastes memory. Pagination loads data in small chunks.

2️⃣ **WHEN** — Any list view with potentially many items.

3️⃣ **HOW**

```python
# In a function-based view
from django.core.paginator import Paginator

def post_list(request):
    all_posts = Post.objects.filter(status='published')
    paginator = Paginator(all_posts, 10)
    #   10 posts per page

    page_number = request.GET.get('page')
    #   Read ?page=2 from the query string

    page_obj = paginator.get_page(page_number)
    #   Returns a Page object; handles invalid page numbers gracefully

    return render(request, 'blog/post_list.html', {'page_obj': page_obj})
```

```html
<!-- Template pagination controls -->
{% for post in page_obj %}
    <h2>{{ post.title }}</h2>
{% endfor %}

<div class="pagination">
    {% if page_obj.has_previous %}
        <a href="?page={{ page_obj.previous_page_number }}">Previous</a>
    {% endif %}

    <span>Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}</span>

    {% if page_obj.has_next %}
        <a href="?page={{ page_obj.next_page_number }}">Next</a>
    {% endif %}
</div>
```

### Database Indexing

1️⃣ **WHY** — Indexes dramatically speed up queries that filter or sort by a column, at the cost of slightly slower writes.

2️⃣ **WHEN** — On columns frequently used in `filter()`, `order_by()`, or `get()` calls.

3️⃣ **HOW**

```python
class Post(models.Model):
    title = models.CharField(max_length=200, db_index=True)
    #   db_index=True → creates a single-column index on 'title'

    status = models.CharField(max_length=10, choices=STATUS_CHOICES, default='draft')
    publish_date = models.DateTimeField(default=timezone.now)

    class Meta:
        indexes = [
            models.Index(fields=['status', 'publish_date']),
            #   Composite index — speeds up queries that filter by both columns
            #   e.g. Post.objects.filter(status='published').order_by('-publish_date')

            models.Index(fields=['-publish_date'], name='recent_first_idx'),
            #   Descending index — optimized for ORDER BY publish_date DESC
        ]
```

#### MySQL Index Inspection

Verify your indexes directly in MySQL:

```sql
SHOW INDEX FROM blog_post;
-- Displays all indexes on the table, including:
--   Key_name       → index name
--   Column_name    → indexed column
--   Index_type     → BTREE (default for InnoDB) or FULLTEXT
--   Cardinality    → estimated number of unique values (higher = more selective)

EXPLAIN SELECT * FROM blog_post WHERE status = 'published' ORDER BY publish_date DESC;
-- Check the 'key' column to verify MySQL is using the expected index
-- If 'key' is NULL, MySQL is doing a full table scan — add an index!
```

✏️ **Practice:** Install `django-debug-toolbar` and identify all queries on your blog's post list page. Fix any N+1 queries using `select_related` or `prefetch_related`. Add a composite index on `(status, publish_date)` and verify with MySQL's `EXPLAIN` that the index is being used. Then add view-level caching to the post list for 10 minutes and confirm the query count drops to zero on cached requests.

---

## Part 9: Advanced Features

### Django REST Framework

1️⃣ **WHY** — DRF provides a powerful toolkit for building Web APIs — serialization, authentication, throttling, pagination, and browsable API documentation.

2️⃣ **WHEN** — When your application needs to serve JSON (or XML) to mobile apps, SPAs, or third-party integrations.

3️⃣ **HOW**

```bash
pip install djangorestframework
```

```python
# settings.py
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```

Serializer:

```python
# blog/serializers.py
from rest_framework import serializers
from .models import Post

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = ['id', 'title', 'body', 'status', 'publish_date', 'created_at']
        #   fields → which model fields to include in JSON output
        read_only_fields = ['created_at']
        #   read_only_fields → cannot be set via the API
```

ViewSet:

```python
# blog/views.py
from rest_framework import viewsets, permissions
from .models import Post
from .serializers import PostSerializer

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.filter(status='published')
    serializer_class = PostSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly]
    #   Authenticated users can create/update; anyone can read
```

Router:

```python
# blog/urls.py
from rest_framework.routers import DefaultRouter
from .views import PostViewSet

router = DefaultRouter()
router.register(r'posts', PostViewSet)
#   Automatically creates URLs:
#   GET    /api/posts/      → list
#   POST   /api/posts/      → create
#   GET    /api/posts/1/    → retrieve
#   PUT    /api/posts/1/    → update
#   DELETE /api/posts/1/    → destroy

urlpatterns = router.urls
```

### Signals

1️⃣ **WHY** — Signals allow decoupled components to react to events (e.g., auto-create a profile when a user is created).

2️⃣ **WHEN** — When you need side effects that should not pollute the model or view code.

3️⃣ **HOW**

```python
# accounts/signals.py
from django.db.models.signals import post_save
from django.dispatch import receiver
from django.contrib.auth.models import User
from .models import Profile

@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):
    """Automatically create a Profile when a new User is saved."""
    #   sender    → the model class (User)
    #   instance  → the actual User object that was saved
    #   created   → True if this is a new record, False if updated
    if created:
        Profile.objects.create(user=instance)
```

Register the signal in `apps.py`:

```python
# accounts/apps.py
class AccountsConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'accounts'

    def ready(self):
        import accounts.signals
        #   Import signals module so @receiver decorators are registered
```

### Custom Management Commands

1️⃣ **WHY** — Management commands let you run custom scripts via `manage.py`, with access to Django's ORM and settings.

2️⃣ **WHEN** — Data imports, cleanup tasks, report generation, seeding development databases.

3️⃣ **HOW**

```python
# blog/management/commands/seed_posts.py
from django.core.management.base import BaseCommand
from blog.models import Post, Category

class Command(BaseCommand):
    help = 'Seed the database with sample blog posts'
    #   help → shown when running: python manage.py help seed_posts

    def add_arguments(self, parser):
        parser.add_argument('count', type=int, help='Number of posts to create')
        #   Positional argument: python manage.py seed_posts 20

    def handle(self, *args, **options):
        count = options['count']
        category, _ = Category.objects.get_or_create(
            name='General', slug='general'
        )
        for i in range(count):
            Post.objects.create(
                title=f'Sample Post {i+1}',
                body=f'This is the body of sample post {i+1}.',
                category=category,
                status='published',
            )
        self.stdout.write(self.style.SUCCESS(f'Created {count} posts.'))
        #   self.style.SUCCESS → green colored output
```

```bash
python manage.py seed_posts 20
# Output: Created 20 posts.
```

### Middleware

> 💡 **Analogy:** Middleware is like a **security checkpoint** at an airport. Every passenger (request) passes through the same checkpoints on the way in, and the same checkpoints on the way out (response). You can add new checkpoints (middleware classes) for logging, timing, authentication, etc.

1️⃣ **WHY** — Middleware hooks into the request/response cycle. It is the right place for cross-cutting concerns like logging, timing, or custom headers.

2️⃣ **WHEN** — When you need logic that applies to every request or response globally.

3️⃣ **HOW**

```python
# mysite/middleware.py
import time
import logging

logger = logging.getLogger(__name__)

class RequestTimingMiddleware:
    """Log the time taken to process each request."""

    def __init__(self, get_response):
        self.get_response = get_response
        #   get_response → the next middleware or the view itself

    def __call__(self, request):
        start = time.time()
        #   Record start time before the view runs

        response = self.get_response(request)
        #   Call the view (and any remaining middleware)

        duration = time.time() - start
        logger.info(f'{request.method} {request.path} — {duration:.3f}s')
        #   Log the request method, path, and duration

        return response
```

Register in settings:

```python
MIDDLEWARE = [
    'mysite.middleware.RequestTimingMiddleware',   # ← add here
    'django.middleware.security.SecurityMiddleware',
    ...
]
```

### Celery and Async Tasks

1️⃣ **WHY** — Long-running tasks (sending emails, processing images, generating reports) block web requests. Celery offloads them to background workers.

2️⃣ **WHEN** — Any task that takes more than a second or should happen on a schedule.

3️⃣ **HOW**

```bash
pip install celery redis
```

```python
# mysite/celery.py
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')

app = Celery('mysite')
app.config_from_object('django.conf:settings', namespace='CELERY')
#   Read CELERY_* settings from settings.py

app.autodiscover_tasks()
#   Automatically find tasks.py in each installed app
```

```python
# settings.py
CELERY_BROKER_URL = 'redis://localhost:6379/0'
#   Message broker — Redis is the recommended choice
CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'
```

```python
# blog/tasks.py
from celery import shared_task
from django.core.mail import send_mail

@shared_task
def send_notification_email(email, post_title):
    """Send an email notification asynchronously."""
    send_mail(
        subject=f'New post: {post_title}',
        message=f'Check out the new post: {post_title}',
        from_email='noreply@example.com',
        recipient_list=[email],
    )
```

```python
# Usage in a view
from .tasks import send_notification_email

def publish_post(request, pk):
    post = get_object_or_404(Post, pk=pk)
    post.status = 'published'
    post.save()

    send_notification_email.delay('reader@example.com', post.title)
    #   .delay() → sends the task to Celery for background execution
    #   The view returns immediately without waiting for the email to send

    return redirect('blog:post_detail', pk=post.pk)
```

### Internationalization

1️⃣ **WHY** — If your application serves users in multiple countries or languages, Django's i18n framework lets you translate text without duplicating templates or views.

2️⃣ **WHEN** — Any application targeting a multilingual audience (e.g., an e-commerce site serving Europe).

3️⃣ **HOW**

Enable internationalization in settings:

```python
# settings.py
USE_I18N = True
#   Activates Django's translation system

LANGUAGE_CODE = 'en-us'
#   Default language

LANGUAGES = [
    ('en', 'English'),
    ('es', 'Spanish'),
    ('fr', 'French'),
]
#   Languages your site supports

LOCALE_PATHS = [BASE_DIR / 'locale']
#   Directory where translation files (.po) are stored

MIDDLEWARE = [
    ...
    'django.middleware.locale.LocaleMiddleware',
    #   Must be after SessionMiddleware and before CommonMiddleware
    #   Detects the user's preferred language from the request
    ...
]
```

Mark strings for translation in Python code:

```python
# blog/views.py
from django.utils.translation import gettext_lazy as _
#   gettext_lazy → marks a string for translation; evaluated lazily

class Post(models.Model):
    title = models.CharField(verbose_name=_('title'), max_length=200)
    #   verbose_name=_('title') → the field label will be translated

    class Meta:
        verbose_name = _('post')
        verbose_name_plural = _('posts')
```

Mark strings in templates:

```html
{% load i18n %}
{# Load the internationalization template tags #}

<h1>{% trans "Welcome to our blog" %}</h1>
{# {% trans %} → translates a string literal #}

<p>{% blocktrans with count=posts|length %}
    There are {{ count }} posts available.
{% endblocktrans %}</p>
{# {% blocktrans %} → translates a block with variables #}
```

Generate and compile translation files:

```bash
# Generate .po files for Spanish
python manage.py makemessages -l es
#   Creates locale/es/LC_MESSAGES/django.po

# Edit the .po file to add translations, then compile:
python manage.py compilemessages
#   Creates .mo binary files Django uses at runtime
```

✏️ **Practice:** Add Spanish translations to your blog app: mark the three most visible strings for translation, generate a `.po` file, add the Spanish translations, and compile. Switch your browser's language preference to Spanish and verify the translations appear.

---

## Part 10: Real-World Projects & Deployment

### Project: Task Manager

Build a full-featured task management app:

**Requirements:**
- User registration and authentication
- CRUD for tasks: title, description, status (To Do / In Progress / Done), priority, due date
- Filter and sort tasks by status, priority, and due date
- MySQL backend
- REST API for mobile clients

**Suggested models:**

```python
class Task(models.Model):
    PRIORITY_CHOICES = [('low', 'Low'), ('medium', 'Medium'), ('high', 'High')]
    STATUS_CHOICES = [('todo', 'To Do'), ('in_progress', 'In Progress'), ('done', 'Done')]

    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='tasks')
    title = models.CharField(max_length=200)
    description = models.TextField(blank=True)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='todo')
    priority = models.CharField(max_length=10, choices=PRIORITY_CHOICES, default='medium')
    due_date = models.DateField(null=True, blank=True)
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ['due_date', '-priority']
```

**MySQL settings for this project:**

```python
# settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'taskmanager',
        'USER': os.environ.get('DB_USER', 'myuser'),
        'PASSWORD': os.environ.get('DB_PASSWORD', ''),
        'HOST': '127.0.0.1',
        'PORT': '3306',
        'OPTIONS': {
            'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
            'charset': 'utf8mb4',
            #   charset=utf8mb4 → ensures the connection uses full Unicode
        },
    }
}
```

### Project: Blog Platform

Build a production-quality blog:

**Requirements:**
- Public post listing with pagination
- Markdown support for post bodies
- Category and tag filtering
- Comment system with moderation
- RSS feed
- Full-text search using MySQL
- Admin customization
- REST API
- MySQL backend with InnoDB engine

**MySQL full-text search example:**

```python
# blog/models.py — add a full-text index for MySQL search
class Post(models.Model):
    title = models.CharField(max_length=200)
    body = models.TextField()
    # ... other fields ...

    class Meta:
        indexes = [
            # MySQL FULLTEXT index for fast text search
            # Requires InnoDB engine (default in MySQL 5.6+)
        ]

# blog/views.py — use MySQL's MATCH ... AGAINST syntax
from django.db.models import Value
from django.db import connection

def search_posts(request):
    query = request.GET.get('q', '')
    if query:
        # Use MySQL's native full-text search for better performance
        posts = Post.objects.raw(
            "SELECT * FROM blog_post "
            "WHERE MATCH(title, body) AGAINST (%s IN BOOLEAN MODE) "
            "AND status = 'published' "
            "ORDER BY MATCH(title, body) AGAINST (%s IN BOOLEAN MODE) DESC",
            [query, query]
        )
        #   MATCH ... AGAINST → MySQL full-text search
        #   IN BOOLEAN MODE   → supports +required -excluded "exact phrase"
        #   Results are ranked by relevance score
    else:
        posts = Post.objects.filter(status='published')
    return render(request, 'blog/search.html', {'posts': posts, 'query': query})
```

> **MySQL note:** Run this SQL to add the FULLTEXT index:
> ```sql
> ALTER TABLE blog_post ADD FULLTEXT INDEX ft_title_body (title, body);
> -- Requires InnoDB (MySQL 5.6+) or MyISAM engine
> ```

### Project: E-Commerce Store

Build a complete e-commerce storefront using Django and MySQL:

**Requirements:**
- Product catalog with categories, images, and prices stored in MySQL
- Shopping cart using Django sessions
- User registration, login, and order history
- Checkout with form validation and order creation
- Admin interface for managing products and orders
- REST API for product listing

**Core models:**

```python
# shop/models.py
from django.db import models
from django.contrib.auth.models import User

class Category(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)

    class Meta:
        verbose_name_plural = 'categories'

    def __str__(self):
        return self.name


class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    name = models.CharField(max_length=200)
    slug = models.SlugField(max_length=200, unique=True)
    description = models.TextField(blank=True)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    #   DecimalField → DECIMAL(10,2) in MySQL — exact precision for money
    #   Allows values up to 99,999,999.99 — use max_digits=12 for higher-value items
    image = models.ImageField(upload_to='products/%Y/%m/', blank=True)
    stock = models.PositiveIntegerField(default=0)
    available = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        indexes = [
            models.Index(fields=['slug']),
            models.Index(fields=['category', 'available']),
            #   Composite index for filtering by category + availability
        ]
        ordering = ['-created_at']

    def __str__(self):
        return self.name


class Order(models.Model):
    STATUS_CHOICES = [
        ('pending', 'Pending'),
        ('paid', 'Paid'),
        ('shipped', 'Shipped'),
        ('delivered', 'Delivered'),
    ]
    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='orders')
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='pending')
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        ordering = ['-created_at']

    @property
    def total_cost(self):
        return sum(item.get_cost() for item in self.items.all())


class OrderItem(models.Model):
    order = models.ForeignKey(Order, on_delete=models.CASCADE, related_name='items')
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    #   Snapshot of the price at the time of purchase (prices may change later)
    quantity = models.PositiveIntegerField(default=1)

    def get_cost(self):
        return self.price * self.quantity
```

**MySQL settings for this project:**

```python
# settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'ecommerce_db',
        'USER': os.environ.get('DB_USER', 'myuser'),
        'PASSWORD': os.environ.get('DB_PASSWORD', ''),
        'HOST': '127.0.0.1',
        'PORT': '3306',
        'OPTIONS': {
            'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
            'charset': 'utf8mb4',
        },
    }
}
```

**Shopping cart using sessions:**

```python
# cart/cart.py
from decimal import Decimal
from shop.models import Product

class Cart:
    def __init__(self, request):
        self.session = request.session
        cart = self.session.get('cart')
        if not cart:
            cart = self.session['cart'] = {}
        self.cart = cart

    def add(self, product, quantity=1):
        product_id = str(product.id)
        if product_id not in self.cart:
            self.cart[product_id] = {'quantity': 0, 'price': str(product.price)}
        self.cart[product_id]['quantity'] += quantity
        self.save()

    def remove(self, product):
        product_id = str(product.id)
        if product_id in self.cart:
            del self.cart[product_id]
            self.save()

    def get_total_price(self):
        return sum(
            Decimal(item['price']) * item['quantity']
            for item in self.cart.values()
        )

    def save(self):
        self.session.modified = True
```

**Checkout view with MySQL transaction:**

```python
# orders/views.py
from django.db import transaction
from django.contrib.auth.decorators import login_required
from django.core.exceptions import ValidationError

@login_required
def checkout(request):
    cart = Cart(request)
    if request.method == 'POST':
        with transaction.atomic():
            #   transaction.atomic() → wraps everything in a MySQL transaction
            #   If any step fails, all changes are rolled back
            order = Order.objects.create(user=request.user)
            for product_id, item_data in cart.cart.items():
                product = Product.objects.select_for_update().get(id=int(product_id))
                #   select_for_update() → MySQL row-level lock (prevents race conditions)
                #   int(product_id)     → cart stores IDs as strings; convert explicitly
                if product.stock < item_data['quantity']:
                    raise ValidationError(f'Not enough stock for {product.name}')
                    #   ValidationError → handled gracefully; does not crash the server
                product.stock -= item_data['quantity']
                product.save()
                OrderItem.objects.create(
                    order=order,
                    product=product,
                    price=product.price,
                    quantity=item_data['quantity'],
                )
        cart.cart.clear()
        cart.save()
        return redirect('orders:order_detail', pk=order.pk)
    return render(request, 'orders/checkout.html', {'cart': cart})
```

**MySQL query for sales dashboard:**

```python
# orders/views.py — dashboard with real-time MySQL aggregate queries
from django.db.models import Sum, Count, F, DecimalField
from django.db.models.functions import TruncMonth

def sales_dashboard(request):
    # Total revenue using MySQL SUM()
    total_revenue = OrderItem.objects.aggregate(
        total=Sum(F('price') * F('quantity'), output_field=DecimalField())
    )['total'] or 0

    # Monthly sales using MySQL DATE_FORMAT via TruncMonth
    monthly_sales = (
        Order.objects
        .filter(status='paid')
        .annotate(month=TruncMonth('created_at'))
        .values('month')
        .annotate(
            revenue=Sum(F('items__price') * F('items__quantity'),
                        output_field=DecimalField()),
            order_count=Count('id'),
        )
        .order_by('month')
    )
    #   Generated MySQL:
    #   SELECT DATE_FORMAT(`orders_order`.`created_at`, '%Y-%m-01') AS `month`,
    #          SUM(`orders_orderitem`.`price` * `orders_orderitem`.`quantity`) AS `revenue`,
    #          COUNT(`orders_order`.`id`) AS `order_count`
    #   FROM `orders_order`
    #   INNER JOIN `orders_orderitem` ON (...)
    #   WHERE `orders_order`.`status` = 'paid'
    #   GROUP BY `month`
    #   ORDER BY `month` ASC

    # Top 5 best-selling products
    top_products = (
        OrderItem.objects
        .values('product__name')
        .annotate(total_sold=Sum('quantity'))
        .order_by('-total_sold')[:5]
    )

    return render(request, 'orders/dashboard.html', {
        'total_revenue': total_revenue,
        'monthly_sales': monthly_sales,
        'top_products': top_products,
    })
```

### Deploying with Gunicorn and Nginx

1️⃣ **WHY** — The Django development server is single-threaded and insecure. Gunicorn is a production-grade WSGI server, and Nginx serves as a reverse proxy and static file server.

2️⃣ **WHEN** — Deploying to any Linux server.

3️⃣ **HOW**

```bash
pip install gunicorn

# Run Gunicorn
gunicorn mysite.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers 3 \
    --timeout 120
#   --workers 3     → number of worker processes (2 * CPU cores + 1)
#   --timeout 120   → kill workers that are silent for 120 seconds
```

Nginx configuration:

```nginx
server {
    listen 80;
    server_name example.com;

    # Serve static files directly (bypasses Gunicorn)
    location /static/ {
        alias /path/to/staticfiles/;
    }

    location /media/ {
        alias /path/to/media/;
    }

    # Proxy all other requests to Gunicorn
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Production checklist:

```bash
# 1. Set environment variables
export DJANGO_SECRET_KEY='your-very-long-random-secret-key'
export DB_PASSWORD='your-db-password'
export DJANGO_SETTINGS_MODULE='mysite.settings'

# 2. Collect static files
python manage.py collectstatic --noinput

# 3. Run migrations
python manage.py migrate

# 4. Verify security settings
python manage.py check --deploy
#   Reports any security issues with your settings
```

### Docker Deployment

1️⃣ **WHY** — Docker containers ensure your application runs identically across development, staging, and production environments.

2️⃣ **WHEN** — For reproducible deployments, CI/CD pipelines, and cloud hosting.

3️⃣ **HOW**

```dockerfile
# Dockerfile
FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python manage.py collectstatic --noinput

EXPOSE 8000
CMD ["gunicorn", "mysite.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "3"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  db:
    image: mysql:8.0
    environment:
      MYSQL_DATABASE: mydatabase
      MYSQL_USER: myuser
      MYSQL_PASSWORD: mypassword
      MYSQL_ROOT_PASSWORD: rootpassword
    volumes:
      - mysql_data:/var/lib/mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      interval: 10s
      timeout: 5s
      retries: 5
    #   healthcheck → Docker waits until MySQL is ready before starting 'web'

  web:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      db:
        condition: service_healthy
    #   condition: service_healthy → waits for MySQL health check to pass
    environment:
      DB_HOST: db
      DB_NAME: mydatabase
      DB_USER: myuser
      DB_PASSWORD: mypassword

volumes:
  mysql_data:
```

✏️ **Practice:** Containerize the blog application: create a `Dockerfile` and `docker-compose.yml` with Django + MySQL services. Add a health check for MySQL and use `depends_on` with `condition: service_healthy`. Run `docker-compose up` and verify you can access the site at `http://localhost:8000`.

---

## Common Mistakes

### Migration Mistakes

| Mistake | Why It's a Problem | How to Avoid |
|---------|-------------------|--------------|
| Editing migration files manually | Breaks migration history; `migrate` may fail or corrupt data | Always use `makemigrations` to generate changes; use `RunSQL` or `RunPython` for custom operations |
| Deleting migration files | Django loses track of schema state | Use `squashmigrations` to consolidate instead |
| Forgetting `makemigrations` before `migrate` | Model changes are not applied to the database | Always run `makemigrations` after every model change |
| Not committing migrations to version control | Other developers have different schemas | Always commit `migrations/` directories |
| Running `migrate` on production without testing | A bad migration can cause data loss or downtime | Test migrations on a staging MySQL database first; use `--plan` to preview |

```python
# BAD: editing a migration file to rename a field
# This will NOT work — Django tracks migrations by file hash

# GOOD: create a new migration
python manage.py makemigrations blog --name rename_title_to_headline
# Then in the generated migration:
operations = [
    migrations.RenameField(
        model_name='post',
        old_name='title',
        new_name='headline',
    ),
]
```

### Insecure Settings

```python
# ❌ BAD — common in production deployments
DEBUG = True                    # Exposes stack traces, SQL queries, settings
SECRET_KEY = 'hardcoded-key'    # Same key across all environments
ALLOWED_HOSTS = ['*']           # Allows any hostname

# ✅ GOOD — secure production settings
DEBUG = False
SECRET_KEY = os.environ['DJANGO_SECRET_KEY']   # From environment variable
ALLOWED_HOSTS = ['example.com', 'www.example.com']  # Explicit hostnames

# Always run this before deploying:
python manage.py check --deploy
# It will warn about any insecure settings
```

### Inefficient Queries

```python
# ❌ BAD — N+1 query problem (1 query + 1 per post for category)
posts = Post.objects.all()
for post in posts:
    print(post.category.name)    # Triggers a new MySQL query every iteration!
# Total: 101 queries for 100 posts

# ✅ GOOD — single query with JOIN
posts = Post.objects.select_related('category').all()
for post in posts:
    print(post.category.name)    # Already loaded — no extra query
# Total: 1 query

# ❌ BAD — loading all fields when you only need one
all_posts = Post.objects.all()   # Fetches every column from MySQL

# ✅ GOOD — fetch only what you need
titles = Post.objects.values_list('title', flat=True)

# ❌ BAD — counting in Python
count = len(Post.objects.all())  # Loads ALL rows into memory, then counts

# ✅ GOOD — counting in MySQL
count = Post.objects.count()     # SELECT COUNT(*) — fast, no data transfer
```

### Deployment Pitfalls

| Pitfall | Consequence | Solution |
|---------|------------|----------|
| Not running `collectstatic` | CSS/JS files missing in production | Add `python manage.py collectstatic --noinput` to deploy script |
| Using Django's dev server in production | Single-threaded, no HTTPS, insecure | Use Gunicorn or uWSGI behind Nginx |
| Not setting `CONN_MAX_AGE` in MySQL settings | New MySQL connection per request (slow) | Set `'CONN_MAX_AGE': 600` for persistent connections |
| Storing secrets in code or `settings.py` | Credentials exposed in version control | Use environment variables or a secrets manager |
| Not backing up MySQL before migrations | Migration failure can cause data loss | Run `mysqldump` before every production migration |

---

## Comparisons

### Django vs Flask vs FastAPI

| Feature | Django | Flask | FastAPI |
|---------|--------|-------|---------|
| **Type** | Full-stack framework | Micro-framework | Modern async API framework |
| **ORM** | Built-in (Django ORM) | None (use SQLAlchemy) | None (use SQLAlchemy/Tortoise) |
| **Admin panel** | Built-in | None (use Flask-Admin) | None |
| **Authentication** | Built-in | None (use Flask-Login) | None (use custom or libraries) |
| **API support** | DRF (add-on) | Flask-RESTful (add-on) | Native (built-in) |
| **Async support** | Partial (Django 4.1+) | Limited (via extensions) | Full native async/await |
| **Performance** | Good for most apps | Good | Excellent (async I/O) |
| **Learning curve** | Moderate | Low | Low-Moderate |
| **Best for** | Full web apps, CMS, e-commerce | Small apps, microservices, prototypes | High-performance APIs, async workloads |
| **Community** | Very large, mature | Large, mature | Growing rapidly |
| **MySQL support** | Excellent (built-in adapter) | Via SQLAlchemy | Via SQLAlchemy or databases lib |

**When to choose Django:** You need a full-featured application with user auth, admin panel, forms, and a relational database (MySQL). You want batteries included and don't want to assemble components yourself.

**When to choose Flask:** You need a lightweight application or microservice where you want full control over which libraries to use.

**When to choose FastAPI:** You need a high-performance API with native async support, automatic OpenAPI docs, and type validation.

### MySQL vs NoSQL Databases

| Feature | MySQL (Relational) | MongoDB (Document) | Redis (Key-Value) |
|---------|-------------------|-------------------|-------------------|
| **Data model** | Tables with rows and columns | JSON-like documents | Key-value pairs |
| **Schema** | Strict (defined upfront) | Flexible (schema-less) | Schema-less |
| **Relationships** | JOINs and foreign keys | Embedded docs or manual refs | No relationships |
| **Transactions** | Full ACID support | Multi-doc transactions (4.0+) | Single-key atomic |
| **Query language** | SQL | MongoDB Query Language | Simple GET/SET commands |
| **Django support** | Built-in adapter | Via `djongo` (limited) | Via `django-redis` (caching) |
| **Best for** | Structured data, complex queries, financial data | Rapidly changing schemas, content management | Caching, sessions, real-time leaderboards |

**When to use MySQL with Django:**
- You need complex queries with JOINs across multiple tables
- Data integrity and ACID transactions are critical (e.g., e-commerce orders)
- You want the best Django integration (full ORM support, admin, migrations)
- You need a mature, well-documented database with excellent tooling

**When to consider NoSQL:**
- Your data is highly unstructured or varies widely between records
- You need horizontal scaling across many servers
- You're building a caching layer (Redis) alongside your MySQL primary database

### Scalability Considerations

```
Small App (< 1,000 users)
├── Single server: Django + MySQL on one machine
├── SQLite may even suffice for development
└── No caching needed

Medium App (1,000 – 100,000 users)
├── Separate Django and MySQL servers
├── Add Redis for caching and sessions
├── Use CONN_MAX_AGE for persistent MySQL connections
├── Add database indexes on frequently queried columns
└── Use select_related / prefetch_related everywhere

Large App (100,000+ users)
├── Multiple Django instances behind a load balancer (Nginx)
├── MySQL read replicas for heavy read workloads
│   └── Django's DATABASE_ROUTERS can direct reads to replicas
├── Redis cluster for caching
├── Celery workers for background tasks
├── CDN for static files
└── Consider MySQL partitioning for very large tables
```

```python
# Example: Configuring MySQL read replicas in Django
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydb',
        'HOST': 'mysql-primary.example.com',
        # ... credentials ...
    },
    'replica': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydb',
        'HOST': 'mysql-replica.example.com',
        # ... credentials ...
    },
}

# Database router to direct reads to the replica
class PrimaryReplicaRouter:
    def db_for_read(self, model, **hints):
        return 'replica'

    def db_for_write(self, model, **hints):
        return 'default'

    def allow_relation(self, obj1, obj2, **hints):
        return True

    def allow_migrate(self, db, app_label, model_name=None, **hints):
        return db == 'default'
```

---

## Practice Exercises

### Beginner

1. **Hello Django** — Create a new Django project and app. Write a view that returns "Hello, Django!" as an HTTP response. Map it to the URL `/hello/`.

2. **Simple Model** — Create a `Book` model with fields: `title` (CharField), `author` (CharField), `published_date` (DateField). Run migrations and add three books via the Django shell.

3. **Template Basics** — Create a view that passes a list of book titles to a template. Render them as an HTML unordered list.

4. **Static Page** — Create a static "About" page using template inheritance. The page should extend a base template that includes a navigation bar.

### Intermediate

5. **CRUD Blog** — Build a complete blog app with list, detail, create, update, and delete views using class-based views. Use MySQL as the backend.

6. **Contact Form** — Build a contact form with name, email, and message fields. Add custom validation: name must be at least 2 characters, message must be at least 20 characters. Display errors inline.

7. **User Authentication** — Add registration, login, and logout functionality. Restrict blog post creation to authenticated users only.

8. **Search and Filter** — Add a search bar to the blog list view that filters posts by title (case-insensitive). Add category-based filtering via URL parameters.

9. **Pagination** — Paginate the blog list view to show 5 posts per page. Include Previous/Next navigation links.

### Advanced

10. **REST API** — Create a full REST API for the blog using Django REST Framework. Include endpoints for listing, creating, retrieving, updating, and deleting posts. Add token authentication.

11. **Performance Audit** — Use `django-debug-toolbar` to identify N+1 queries in your blog app. Fix them using `select_related` and `prefetch_related`. Document the before/after query counts.

12. **Background Tasks** — Set up Celery with Redis. Create a task that sends a welcome email when a new user registers. Verify the task executes asynchronously.

13. **Custom Middleware** — Write middleware that logs the execution time of every request. Add a custom response header `X-Request-Duration` with the time in milliseconds.

14. **Dockerize** — Containerize your blog application with Docker. Create a `docker-compose.yml` with separate services for Django, MySQL, and Redis. Verify the app runs with `docker-compose up`.

15. **Full Deployment** — Deploy the blog to a Linux server using Gunicorn and Nginx. Configure HTTPS with Let's Encrypt. Run `manage.py check --deploy` and fix all warnings.

---

## Cheat Sheet

### Common Commands

| Command | Description |
|---|---|
| `django-admin startproject <name>` | Create a new project |
| `python manage.py startapp <name>` | Create a new app |
| `python manage.py runserver` | Start the development server |
| `python manage.py makemigrations` | Generate migration files |
| `python manage.py migrate` | Apply migrations to the database |
| `python manage.py createsuperuser` | Create an admin superuser |
| `python manage.py collectstatic` | Collect static files for production |
| `python manage.py test` | Run tests |
| `python manage.py shell` | Open the Django interactive shell |
| `python manage.py showmigrations` | List all migrations and their status |
| `python manage.py check --deploy` | Check production security settings |

### Model Field Quick Reference

| Field | MySQL Type | Example |
|---|---|---|
| `CharField(max_length=N)` | `VARCHAR(N)` | `title = CharField(max_length=200)` |
| `TextField()` | `LONGTEXT` | `body = TextField()` |
| `IntegerField()` | `INT` | `count = IntegerField(default=0)` |
| `DecimalField(max_digits, decimal_places)` | `DECIMAL` | `price = DecimalField(max_digits=8, decimal_places=2)` |
| `BooleanField()` | `TINYINT(1)` | `is_active = BooleanField(default=True)` |
| `DateTimeField()` | `DATETIME(6)` | `created = DateTimeField(auto_now_add=True)` |
| `ForeignKey(Model)` | `BIGINT + FK` | `author = ForeignKey(User, on_delete=CASCADE)` |
| `ManyToManyField(Model)` | Join table | `tags = ManyToManyField(Tag)` |
| `JSONField()` | `JSON` | `metadata = JSONField(default=dict)` |

### QuerySet Quick Reference

| Method | SQL Equivalent | Example |
|---|---|---|
| `.all()` | `SELECT *` | `Post.objects.all()` |
| `.filter()` | `WHERE` | `Post.objects.filter(status='published')` |
| `.exclude()` | `WHERE NOT` | `Post.objects.exclude(status='draft')` |
| `.get()` | `WHERE ... LIMIT 1` | `Post.objects.get(pk=1)` |
| `.create()` | `INSERT` | `Post.objects.create(title='New')` |
| `.update()` | `UPDATE` | `Post.objects.filter(...).update(status='published')` |
| `.delete()` | `DELETE` | `Post.objects.filter(...).delete()` |
| `.order_by()` | `ORDER BY` | `Post.objects.order_by('-created_at')` |
| `.count()` | `COUNT(*)` | `Post.objects.count()` |
| `.exists()` | `EXISTS` | `Post.objects.filter(pk=1).exists()` |
| `.values()` | `SELECT col1, col2` | `Post.objects.values('title')` |
| `.select_related()` | `JOIN` | `Post.objects.select_related('category')` |
| `.prefetch_related()` | Separate query + Python join | `Category.objects.prefetch_related('posts')` |
| `.aggregate()` | `SELECT AGG(...)` | `Post.objects.aggregate(Count('id'))` |
| `.annotate()` | `SELECT ..., AGG(...) AS ...` | `Category.objects.annotate(n=Count('posts'))` |

### MySQL Quick Reference

| Command / SQL | Description |
|---|---|
| `mysql -u myuser -p mydatabase` | Connect to a MySQL database from the terminal |
| `SHOW DATABASES;` | List all databases |
| `SHOW TABLES;` | List all tables in the current database |
| `DESCRIBE blog_post;` | Show column definitions for a table |
| `SHOW INDEX FROM blog_post;` | List all indexes on a table |
| `SHOW CREATE TABLE blog_post;` | Display the full CREATE TABLE statement |
| `EXPLAIN SELECT ...;` | Show the query execution plan |
| `SELECT VERSION();` | Display the MySQL server version |
| `SHOW PROCESSLIST;` | List active connections and queries |
| `SET sql_mode='STRICT_TRANS_TABLES';` | Enable strict mode (recommended for Django) |

### MySQL Data Types (Django ↔ MySQL)

| Django Field | MySQL Type | Notes |
|---|---|---|
| `AutoField` | `INT AUTO_INCREMENT` | Legacy default primary key |
| `BigAutoField` | `BIGINT AUTO_INCREMENT` | Default primary key (Django 3.2+) |
| `CharField(max_length=N)` | `VARCHAR(N)` | Max 65,535 bytes per row |
| `TextField` | `LONGTEXT` | Up to 4 GB |
| `IntegerField` | `INT` | -2,147,483,648 to 2,147,483,647 |
| `BigIntegerField` | `BIGINT` | -9.2×10¹⁸ to 9.2×10¹⁸ |
| `FloatField` | `DOUBLE` | Approximate precision |
| `DecimalField` | `DECIMAL(M,D)` | Exact precision — use for money |
| `BooleanField` | `TINYINT(1)` | `0` = False, `1` = True |
| `DateField` | `DATE` | `YYYY-MM-DD` |
| `DateTimeField` | `DATETIME(6)` | Microsecond precision |
| `DurationField` | `BIGINT` | Stored as microseconds |
| `JSONField` | `JSON` | Native JSON (MySQL 5.7+) |
| `BinaryField` | `LONGBLOB` | Raw binary data |

### MySQL Connection Troubleshooting

| Error | Cause | Fix |
|---|---|---|
| `(2003) Can't connect to MySQL server` | MySQL is not running | Start MySQL: `sudo systemctl start mysql` |
| `(1045) Access denied for user` | Wrong username or password | Verify credentials in `settings.py` |
| `(1049) Unknown database` | Database does not exist | Create it: `CREATE DATABASE mydatabase;` |
| `(2002) Connection refused` | Wrong host or port | Check `HOST` and `PORT` in settings |
| `(1071) Specified key was too long` | Index on a column with `utf8mb4` exceeds 767 bytes | Use `max_length=191` or set `innodb_large_prefix=ON` |

---

## Further Reading

- [Django Official Documentation](https://docs.djangoproject.com/) — the definitive reference
- [Django REST Framework](https://www.django-rest-framework.org/) — API toolkit documentation
- [MySQL Documentation](https://dev.mysql.com/doc/) — database reference
- [Django Girls Tutorial](https://tutorial.djangogirls.org/) — beginner-friendly introduction
- [Two Scoops of Django (book)](https://www.feldroy.com/books/two-scoops-of-django-3-x) — best practices guide
- [Classy Class-Based Views](https://ccbv.co.uk/) — visual reference for all Django CBVs
- [Django Packages](https://djangopackages.org/) — directory of reusable Django apps
- [Django Debug Toolbar](https://django-debug-toolbar.readthedocs.io/) — development profiling tool
- [Celery Documentation](https://docs.celeryq.dev/) — distributed task queue
- [Docker Documentation](https://docs.docker.com/) — containerization platform
